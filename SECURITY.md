# Security

## My Security Philosophy

```
╔══════════════════════════════════════════════════════════════════════════════════════╗
║                                                                                      ║
║                              NEO DOME SECURITY                                       ║
║                                                                                      ║
║                    ┌─────────────────────────────────────┐                           ║
║                    │           PROTECTION LAYERS          │                           ║
║                    │                                      │                           ║
║                    │   ┌────────────────────────────┐    │                           ║
║                    │   │     CLOUD INFRASTRUCTURE    │    │                           ║
║                    │   │  (Cloudflare DDoS + WAF)    │    │                           ║
║                    │   └────────────────────────────┘    │                           ║
║                    │              ▲                        │                           ║
║                    │              │                        │                           ║
║                    │   ┌────────────────────────────┐    │                           ║
║                    │   │       APPLICATION LAYER      │    │                           ║
║                    │   │    (Auth + Firestore Rules)  │    │                           ║
║                    │   └────────────────────────────┘    │                           ║
║                    │              ▲                        │                           ║
║                    │              │                        │                           ║
║                    │   ┌────────────────────────────┐    │                           ║
║                    │   │         DATA LAYER         │    │                           ║
║                    │   │  (Encryption + Isolation)   │    │                           ║
║                    │   └────────────────────────────┘    │                           ║
║                    │                                      │                           ║
║                    └─────────────────────────────────────┘                           ║
║                                                                                      ║
╚══════════════════════════════════════════════════════════════════════════════════════╝
```

> **Transparency without secrets**: This document explains HOW I protect your data — not the actual credentials.

---

## What I Protect

```
┌────────────────────────────────────────────────────────────────────────────────────┐
│                                                                                    │
│   ┌─────────────────┐   ┌─────────────────┐   ┌─────────────────┐                  │
│   │  DATA ISOLATION │   │ AUTHENTICATION  │   │   ENCRYPTION    │                  │
│   └────────┬────────┘   └────────┬────────┘   └────────┬────────┘                  │
│            │                     │                      │                            │
│            ▼                     ▼                      ▼                            │
│   ┌─────────────────┐   ┌─────────────────┐   ┌─────────────────┐                  │
│   │                 │   │                 │   │                 │                  │
│   │  Each client    │   │  Firebase Auth  │   │  TLS 1.3 for    │                  │
│   │  in separate    │   │  OAuth 2.0 +    │   │  all traffic    │                  │
│   │  Firestore      │   │  JWT tokens     │   │                 │                  │
│   │  namespaces     │   │                 │   │  Server-side    │                  │
│   │                 │   │  Google, email  │   │  encryption at  │                  │
│   │  Client A ─ ✗ ─│   │  providers       │   │  rest           │                  │
│   │      ─ ─ ─ ─    │   │                 │   │                 │                  │
│   │  Client B ─ ✗ ─│   │  Session expiry  │   │  Field-level    │                  │
│   │                 │   │  enforced        │   │  encryption for │                  │
│   │                 │   │                 │   │  sensitive data │                  │
│   │                 │   │  MFA support     │   │                 │                  │
│   │                 │   │                 │   │                 │                  │
│   └─────────────────┘   └─────────────────┘   └─────────────────┘                  │
│                                                                                    │
└────────────────────────────────────────────────────────────────────────────────────┘
```

---

## Security Architecture

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                                                                                     │
│                              INCOMING REQUESTS                                       │
│                                    │                                                 │
│                                    ▼                                                 │
│                         ┌──────────────────┐                                        │
│                         │   CLOUDFLARE     │                                        │
│                         │                  │                                        │
│                         │  ┌────────────┐  │                                        │
│                         │  │ DDoS Shield│  │                                        │
│                         │  │ WAF Rules  │  │                                        │
│                         │  │ Rate Limit │  │                                        │
│                         │  │ Bot Manage  │  │                                        │
│                         │  └────────────┘  │                                        │
│                         └────────┬─────────┘                                        │
│                                  │                                                   │
│                    ┌─────────────┼─────────────┐                                     │
│                    │             │             │                                     │
│                    ▼             ▼             ▼                                     │
│           ┌────────────┐  ┌────────────┐  ┌────────────┐                             │
│           │  VALID     │  │  BLOCKED   │  │  BLOCKED   │                             │
│           │  REQUESTS  │  │  (Attacks) │  │  (Bots)    │                             │
│           └─────┬──────┘  └────────────┘  └────────────┘                             │
│                 │                                                                   │
│                 ▼                                                                   │
│        ┌─────────────────┐                                                          │
│        │  FIREBASE AUTH  │                                                          │
│        │                 │                                                          │
│        │  ┌───────────┐  │                                                          │
│        │  │ Validate  │  │                                                          │
│        │  │ JWT Token │  │                                                          │
│        │  └───────────┘  │                                                          │
│        │        │        │                                                          │
│        │        ▼        │                                                          │
│        │  ┌───────────┐  │                                                          │
│        │  │ Auth UID  │  │                                                          │
│        │  │ Claims    │  │                                                          │
│        │  └───────────┘  │                                                          │
│        └────────┬────────┘                                                          │
│                 │                                                                   │
│                 ▼                                                                   │
│        ┌─────────────────┐                                                          │
│        │   FIRESTORE     │                                                          │
│        │                 │                                                          │
│        │  ┌───────────┐  │                                                          │
│        │  │ Security  │  │                                                          │
│        │  │ Rules     │  │                                                          │
│        │  │ Validate  │  │                                                          │
│        │  └───────────┘  │                                                          │
│        │        │        │                                                          │
│        │        ▼        │                                                          │
│        │  ┌───────────┐  │                                                          │
│        │  │ Read/Write│  │                                                          │
│        │  │ if allowed│  │                                                          │
│        │  └───────────┘  │                                                          │
│        └─────────────────┘                                                          │
│                                                                                     │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## Firebase Auth Security

| Measure | How It Works |
|---------|--------------|
| **OAuth 2.0** | Industry-standard authorization flow |
| **JWT Tokens** | Cryptographically signed, tamper-proof |
| **Token Expiry** | Short-lived access tokens (1hr), long-lived refresh tokens |
| **Provider Security** | Google OAuth uses Google's security infrastructure |
| **Password Policy** | Enforced minimum length, no common passwords |
| **Session Management** | Automatic sign-out on suspicious activity |

```
┌─────────────────────────────────────────────────────┐
│                                                     │
│   ┌─────────────────────────────────────────────┐   │
│   │           AUTHENTICATION FLOW                │   │
│   └─────────────────────────────────────────────┘   │
│                                                     │
│   User ──► [Google/Email] ──► Firebase Auth         │
│                             │                       │
│                             ▼                       │
│                      ┌──────────────┐               │
│                      │  Verify User │               │
│                      └──────┬───────┘               │
│                             │                       │
│                             ▼                       │
│                      ┌──────────────┐               │
│                      │  JWT Token   │               │
│                      │  Generated   │               │
│                      └──────┬───────┘               │
│                             │                       │
│         ┌───────────────────┼───────────────────┐     │
│         │                   │                   │     │
│         ▼                   ▼                   ▼     │
│   ┌──────────┐       ┌──────────┐       ┌──────────┐
│   │ Firestore│       │  App     │       │  API     │
│   │ (data)   │       │  State   │       │  Calls   │
│   └──────────┘       └──────────┘       └──────────┘
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

## Firestore Security Rules

```
┌────────────────────────────────────────────────────────────────────────────────────┐
│                                                                                    │
│   match /databases/{database}/documents {                                           │
│                                                                                    │
│       // ═══════════════════════════════════════════════════════════                │
│       // RULE: Authenticated users can only read/write their own data              │
│       // ═══════════════════════════════════════════════════════════                │
│                                                                                    │
│       match /users/{userId} {                                                       │
│           allow read, write: if request.auth != null                               │
│                            && request.auth.uid == userId;                          │
│       }                                                                             │
│                                                                                    │
│       // ═══════════════════════════════════════════════════════════                │
│       // RULE: Client data is isolated by client namespace                         │
│       // ═══════════════════════════════════════════════════════════                │
│                                                                                    │
│       match /clients/{clientId}/{document=**} {                                     │
│           allow read, write: if request.auth != null                                │
│                            && request.auth.token.client_id == clientId;            │
│       }                                                                             │
│                                                                                    │
│       // ═══════════════════════════════════════════════════════════                │
│       // RULE: Admin role bypasses all restrictions                                │
│       // ═══════════════════════════════════════════════════════════                │
│                                                                                    │
│       match /admin/{document=**} {                                                  │
│           allow read, write: if request.auth != null                               │
│                            && request.auth.token.admin == true;                    │
│       }                                                                             │
│                                                                                    │
│   }                                                                                 │
│                                                                                    │
└────────────────────────────────────────────────────────────────────────────────────┘
```

### Key Rule Principles

| Principle | Implementation |
|-----------|----------------|
| **User Isolation** | `request.auth.uid == userId` ensures users access only their own data |
| **Client Isolation** | Custom claims (`client_id`) restrict cross-client data access |
| **Admin Gates** | Separate `/admin/` path with elevated permissions |
| **Validate on Write** | Rules verify data structure and values before accepting writes |
| **No Wildcard Access** | Granular paths, never `match /{document=**}` at root |

---

## Cloudflare Protection Layers

```
┌─────────────────────────────────────────────────────────────────────────────────────┐
│                                                                                     │
│                              EDGE NETWORK                                           │
│                                                                                     │
│    ┌───────────────────────────────────────────────────────────────────────────┐   │
│    │                                                                           │   │
│    │   LAYER 3/4 ─────────────────────────────────────────────────────────    │   │
│    │   │   DDoS Protection (volumetric attacks)                               │   │
```

---

## Public vs Private Documentation Policy

- `public-neodome/` is the only content shared on the public repo (`https://github.com/neodigium/neodome`).
- NO sensitive client or partner data is allowed in `public-neodome`.
- NO private operational email addresses are allowed in `public-neodome` (e.g., `neodigia@gmail.com`, `mazariegosc@neodigium.com`).
- Sensitive client docs live in the private repo (`https://github.com/neodigium/neodigia`) and in `clients/records/` that is not published.
- All public docs are scanned via `scripts/check-public-docs.sh` before merge.

Approved public contact channels:
- `mazariegosc@neodigium.com` (primary professional contact)

Forbidden patterns (non-exhaustive):
- `neodigia`, `neodigium` when mapped to internal client names (avoid disclosure of client IDs for active clients)
- `@gmail.com`, `@neodigium.com` (internal roles)
- Firebase project IDs (e.g., `n8n-neodigia`), N8N workflow IDs, API keys, secret tokens

---

│    │   │   Traffic rate limiting                                               │   │
│    │   │   Geographic blocking                                                 │   │
│    │                                                                           │   │
│    │   LAYER 7 ────────────────────────────────────────────────────────────   │   │
│    │   │   Web Application Firewall (WAF)                                     │   │
│    │   │   OWASP Top 10 rules                                                  │   │
│    │   │   Custom firewall rules                                               │   │
│    │   │   Challenge pages for suspicious requests                             │   │
│    │                                                                           │   │
│    │   BOT MANAGEMENT ────────────────────────────────────────────────────    │   │
│    │   │   Machine learning bot detection                                     │   │
│    │   │   JS challenge for browser verification                                │   │
│    │   │  整───threat score per request                                         │   │
│    │                                                                           │   │
│    │   SSL/TLS ───────────────────────────────────────────────────────────    │   │
│    │   │   TLS 1.3 (minimum)                                                   │   │
│    │   │   Full encryption mode                                                │   │
│    │   │   Certificate management                                              │   │
│    │                                                                           │   │
│    └───────────────────────────────────────────────────────────────────────────┘   │
│                                                                                     │
└─────────────────────────────────────────────────────────────────────────────────────┘
```

---

## What I DON'T Do (Anti-Patterns I Avoid)

```
┌────────────────────────────────────────────────────────────────────────────────────┐
│                                                                                    │
│   ✗  NO hardcoded credentials in code                                             │
│   ✗  NO secrets in environment variables committed to git                         │
│   ✗  NO API keys in client-side JavaScript                                        │
│   ✗  NO plain-text storage of sensitive data                                      │
│   ✗  NO cross-tenant data access                                                  │
│   ✗  NO unvalidated user input in database queries                                │
│                                                                                    │
└────────────────────────────────────────────────────────────────────────────────────┘
```

---

## The Security Sentinel — Autonomous Breach Detection

NeoDome doesn't just build walls — it deploys automated sentinels that patrol the perimeter 24/7.

```
┌────────────────────────────────────────────────────────────────────────────────────┐
│                         THE SECURITY SENTINEL WORKFLOW                             │
├────────────────────────────────────────────────────────────────────────────────────┤
│                                                                                    │
│    ┌─────────────┐         ┌─────────────┐         ┌─────────────┐              │
│    │   PULSE     │────────▶│   SCOUT     │────────▶│  INSPECTOR  │              │
│    │  (Hourly)   │         │  HTTP GET   │         │ Regex Check │              │
│    └─────────────┘         └─────────────┘         └──────┬──────┘              │
│                                                            │                      │
│                                               ┌────────────┴────────────┐        │
│                                               │                         │        │
│                                               ▼                         ▼        │
│                                        ┌──────────┐              ┌──────────┐   │
│                                        │  CLEAN  │              │ BREACH   │   │
│                                        │ Silence │              │   🚨     │   │
│                                        └──────────┘              └────┬─────┘   │
│                                                                     │         │
│                                                                     ▼         │
│                                                            ┌────────────────┐    │
│                                                            │    ALERT      │    │
│                                                            │ Slack/Telegram │    │
│                                                            └────────────────┘    │
│                                                                                    │
└────────────────────────────────────────────────────────────────────────────────────┘
```

### How It Works

| Step | Component | What It Does |
|------|-----------|--------------|
| **1. Pulse** | CRON Trigger | Runs every hour, 24/7 |
| **2. Scout** | HTTP Request | Visits your public site as anonymous visitor |
| **3. Inspector** | Regex Node | Searches for leaked sensitive data patterns |
| **4. Judge** | IF Node | Evaluates: clean or breached? |
| **5. Alarm** | Webhook | If breached → immediate alert to admin |

### What It Detects

- Admin dashboard elements visible in public bundle
- Internal email addresses leaking into frontend
- API keys or tokens in source code
- Deep links to internal/admin routes
- Any restricted DOM elements exposed publicly

### The 3Angle Delivery

When clients ask *"how do I know my site is secure?"* — I show them the Sentinel graph and say:

> *"My automated systems deliberately try to break into your public footprint every hour, 24/7. If your site ever leaks an internal link or sensitive data, my phone rings before a customer even clicks it."*

This isn't theoretical security — it's **proven security**. The Sentinel runs on the same infrastructure that runs your business.

---

## Incident Response

| Phase | Action |
|-------|--------|
| **Detection** | Cloudflare analytics, Firestore audit logs, Uptime monitoring |
| **Containment** | Automatic blocking at edge, session revocation in Firebase |
| **Investigation** | Access logs, request traces, Cloudflare logpush |
| **Notification** | Affected users informed within 72 hours per policy |
| **Remediation** | Patch, rotate credentials, update rules |

---

## Credential Management

| Credential Type | Storage Location | Access |
|-----------------|------------------|--------|
| Firebase Keys | Environment variables (not in repo) | Server-side only |
| API Keys | Cloudflare Workers secrets | Edge runtime |
| Database URLs | Environment variables | App config |
| Webhook URLs | N8N credential storage (encrypted) | Workflow runtime |

**Credentials are NEVER:**
- Committed to git repositories
- Exposed in client-side code
- Logged in console output
- Shared in documentation

---

## Third-Party Security Audits

I use:
- **Cloudflare** for infrastructure security (DDoS, WAF, SSL)
- **Firebase** for application security (Auth, Firestore rules)
- **N8N** (self-hosted) for workflow isolation

Each provider maintains their own security certifications:
- Firebase: SOC 2, ISO 27001, GDPR compliant
- Cloudflare: SOC 2, ISO 27001, PCI DSS

---

## Reporting Security Issues

Found a vulnerability? I take security seriously.

**Contact:** `mazariegosc@neodigium.com`

I respond within 48 hours and work with reporters on disclosure.

---

*Built with security. Delivered with trust.*
