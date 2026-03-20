# Service Dependencies

## Overview

Every NeoDome service is built on a foundation of open-source or widely-adopted tools. Your data and accounts are yours from day one.

---

## Tool × Service Matrix

```
                         N8N    Firebase  Cloudflare  LMStudio  ComfyUI  Google WS
────────────────────────────────────────────────────────────────────────────────────
1. Web App              REQ    REQ       REQ         —         —        —
2. AI Assistant         REQ    OPT       OPT         REQ       OPT      —
3. BI Dashboard         OPT    REQ       —           —         —        —
4. AI Workflows         REQ    REQ       —           OPT       —        OPT
5. Google Setup         REQ    —         —           OPT       —        REQ
6. Smart Forms          REQ    REQ       —           —         —        —
7. Lead Generation      REQ    REQ       —           OPT       —        —
8. Security             REQ    REQ       REQ         REQ*      REQ*     REQ
                                                  (* Phase 3 only)

REQ = Required to deliver the service
OPT = Optional — enhances but not required
 —  = Not used
```

---

## Service → Needs → Delivers

| Service | What It Needs | What You Get |
|---------|---------------|--------------|
| **Web App** | Your GitHub repo, Cloudflare account | Live website on your domain, auto-deploys |
| **AI Assistant** | N8N + LMStudio (or OpenAI) | Chatbot that qualifies leads and answers questions |
| **BI Dashboard** | Firebase project | Real-time KPI dashboard with charts |
| **Smart Forms** | N8N + Firebase | Forms that route data to your systems automatically |
| **Lead Generation** | N8N + Firebase + CRM | Automated lead pipeline from contact to close |
| **AI Workflows** | N8N + LMStudio/OpenAI | Custom AI automations for your business |
| **Google Setup** | Google account | Configured Gmail, Drive, Calendar, Sheets |
| **Security** | All above | 24/7 monitoring, health checks, audit reports |

---

## Architecture Diagram

```
┌──────────────────────────────────────────────────────────────────────────────┐
│                          NEODOME PARTNER ECOSYSTEM                           │
├──────────────────────────────────────────────────────────────────────────────┤
│                                                                              │
│    ┌─────────────────────────────────────────────────────────────────┐      │
│    │                        YOUR BUSINESS                              │      │
│    │   ┌───────────┐  ┌───────────┐  ┌───────────┐  ┌───────────┐   │      │
│    │   │  Website  │  │Lead Forms │  │ Dashboard │  │AI Assistant│  │      │
│    │   └─────┬─────┘  └─────┬─────┘  └─────┬─────┘  └─────┬─────┘   │      │
│    └─────────┼──────────────┼──────────────┼──────────────┼──────────┘      │
│              │              │              │              │                   │
│              ▼              ▼              ▼              ▼                   │
│    ┌─────────────────────────────────────────────────────────────────┐      │
│    │                    NEODOME INFRASTRUCTURE                         │      │
│    │                                                                  │      │
│    │   ┌─────────────────────────────────────────────────────────┐   │      │
│    │   │                      N8N                                  │   │      │
│    │   │   Workflows • Webhooks • Automation • Lead Routing       │   │      │
│    │   └──────────────────────────┬──────────────────────────────┘   │      │
│    │                               │                                  │      │
│    │   ┌───────────────────┐ ┌──────┴──────┐ ┌───────────────────┐   │      │
│    │   │    Firebase      │ │   LMStudio  │ │   Cloudflare      │   │      │
│    │   │   Firestore       │ │   Local AI  │ │   Pages/Workers  │   │      │
│    │   │   Auth            │ │   Local API │ │   Tunnel          │   │      │
│    │   │   Database        │ │   (Phase 3) │ │   CDN             │   │      │
│    │   └───────────────────┘ └──────────────┘ └───────────────────┘   │      │
│    │                                                                  │      │
│    └──────────────────────────────────────────────────────────────────┘      │
│                                                                              │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

## Connection Flow

```
User Action          NeoDome Systems           Your Systems
────────────         ───────────────           ─────────────

Contact Form ──────▶ N8N Webhook ─────────────▶ Firebase (leads)
                         │
                         ▼
                   Email Notification ────────▶ Your Gmail
                         │
                         ▼
                   Dashboard Update ─────────▶ BI Dashboard

AI Query ──────────▶ N8N AI Agent ────────────▶ LMStudio (local AI)
                         │
                         ▼
                   Response + Qualification ──▶ Lead Score Updated

Dashboard View ────▶ Firebase Query ──────────▶ Firestore Data
                         │
                         ▼
                   Charts Rendered ───────────▶ Partner Portal
```

---

## Tool Details

| Tool | Type | What It Does | You Own It? |
|------|------|--------------|-------------|
| **N8N** | Open Source | Workflow automation — connects everything | Yes (self-hosted) |
| **Firebase** | Google Cloud | Database + Auth — stores your data | Yes (your project) |
| **Cloudflare** | SaaS | CDN + Tunnel — hosts your site securely | Yes (your account) |
| **LMStudio** | Local App | Local LLM — AI without API costs | Yes (your hardware) |
| **ComfyUI** | Local App | Image generation — local visuals | Yes (your hardware) |
| **Google Workspace** | SaaS | Business suite — Gmail, Drive, Calendar | Yes (your org) |

---

## Phase 3 Stack (Full Ownership)

```
┌─────────────────────────────────────────────────────────────┐
│                    YOUR HARDWARE                             │
│  ┌─────────────────┐  ┌─────────────────┐                   │
│  │     N8N         │  │    LMStudio     │                   │
│  │  (Docker)       │  │   (Local API)   │                   │
│  │  Local Network  │  │   Local LLM     │                   │
│  └─────────────────┘  └─────────────────┘                   │
│                                                             │
│  ┌─────────────────┐  ┌─────────────────┐                   │
│  │    ComfyUI      │  │   Your Data     │                   │
│  │  (Local Images) │  │   (Always)      │                   │
│  └─────────────────┘  └─────────────────┘                   │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                    YOUR CLOUD ACCOUNTS                       │
│  ┌─────────────────┐  ┌─────────────────┐                   │
│  │   Firebase     │  │   Cloudflare    │                   │
│  │  (Your Project) │  │  (Your Account) │                   │
│  └─────────────────┘  └─────────────────┘                   │
│                                                             │
│  ┌─────────────────┐                                        │
│  │ Google Workspace│                                        │
│  │  (Your Org)    │                                        │
│  └─────────────────┘                                        │
└─────────────────────────────────────────────────────────────┘
```

---

## Frequently Asked Questions

| Question | Answer |
|----------|--------|
| Do I need to buy software? | No. Every tool is either your existing account or free open-source. |
| Is there AI cost at Phase 3? | No. LMStudio runs locally — no API fees ever. |
| What if I leave NeoDome? | Your accounts are yours. Data is in your Firebase project. |
| Do I need a developer? | Phase 2: No — that's what the service covers. Phase 3: No — systems are self-running. |
| What is ComfyUI? | Local image generation. Replaces Adobe/Midjourney at Phase 3. |

---

## Exit-Proof by Design

Every tool can stand alone without NeoDome:

| Tool | Standalone? | Notes |
|------|-------------|-------|
| N8N | Yes | Self-hosted Docker, credentials yours |
| Firebase | Yes | Your Google project, you log in |
| Cloudflare | Yes | Your domain, DNS, workers |
| LMStudio | Yes | Free app, runs locally |
| ComfyUI | Yes | Open source, runs locally |
| Google Workspace | Yes | Your org, you own everything |

**Your data. Your accounts. Your stack. Always.**
