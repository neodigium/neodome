# Tech Stack

## Why I Use What I Use

```
╔══════════════════════════════════════════════════════════════════════════════════════╗
║                                                                                      ║
║                              NEO DOME TECH STACK                                    ║
║                         ┌─────────────────────────────────┐                         ║
║                         │  PRESENCE │ INTELLIGENCE │ CONNECTION │ CONTINUITY │      ║
║                         └─────────────────────────────────┘                         ║
║                                                                                      ║
╚══════════════════════════════════════════════════════════════════════════════════════╝
```

## The Stack at a Glance

```
┌──────────────────────────────────────────────────────────────────────────────────────┐
│                                                                                      │
│  ┌─────────────┐   ┌─────────────┐   ┌─────────────┐   ┌─────────────┐              │
│  │  REACT 19   │   │    VITE     │   │  TYPESCRIPT │   │   FIREBASE  │              │
│  └─────────────┘   └─────────────┘   └─────────────┘   └─────────────┘              │
│        ▲               ▲               ▲               ▲                            │
│        │               │               │               │                            │
│        │         ┌────┴────┐     ┌────┴────┐   ┌─────┴─────┐                      │
│        │         │         │     │         │   │           │                      │
│  ┌─────┴─────┐   │  BUILD  │     │  TYPE   │   │   AUTH +  │                      │
│  │    UI     │   │  FAST   │     │  SAFE   │   │  DATABASE │                      │
│  │ COMPONENTS│   │  HMR    │     │  CODE   │   │  REAL TIME│                      │
│  └───────────┘   └─────────┘     └─────────┘   └───────────┘                      │
│                                                                                      │
└──────────────────────────────────────────────────────────────────────────────────────┘
```

## Technology Decisions

```
┌────────────────────────────────────────────────────────────────────────────────────┐
│                                                                                    │
│  ┌────────────────┬─────────────────────────────────────────────────────────────┐ │
│  │   CATEGORY     │                      WHY I CHOSE IT                          │ │
│  ├────────────────┼─────────────────────────────────────────────────────────────┤ │
│  │                │  • Concurrent mode for async rendering                       │ │
│  │   React 19     │  • Built-in form handling & validation                       │ │
│  │                │  • Server Components ready                                    │ │
│  │                │  • Largest ecosystem, proven at scale                         │ │
│  ├────────────────┼─────────────────────────────────────────────────────────────┤ │
│  │                │  • Catches type errors at compile time                        │ │
│  │  TypeScript    │  • Self-documenting code via interfaces                       │ │
│  │                │  • Refactoring confidence                                     │ │
│  │                │  • IDE autocomplete everywhere                                │ │
│  ├────────────────┼─────────────────────────────────────────────────────────────┤ │
│  │                │  • Sub-second hot module replacement                         │ │
│  │  Vite          │  • Native ESM, no bundle during dev                           │ │
│  │                │  • Optimized production builds                                │ │
│  │                │  • Framework agnostic (React, Svelte, Vue all work)          │ │
│  ├────────────────┼─────────────────────────────────────────────────────────────┤ │
│  │                │  • Zero-server auth with Firebase Auth                       │ │
│  │                │  • Managed identity providers (Google, email, etc)           │ │
│  │  Firebase      │  • SDK handles security tokens automatically                 │ │
│  │                │  • Scales to millions without infrastructure                  │ │
│  ├────────────────┼─────────────────────────────────────────────────────────────┤ │
│  │                │  • Real-time sync across all clients                         │ │
│  │  Firestore     │  • Offline-first with automatic reconnection                  │ │
│  │                │  • Serverless — no database ops needed                       │ │
│  │                │  • Security rules enforce access control                      │ │
│  ├────────────────┼─────────────────────────────────────────────────────────────┤ │
│  │                │  • Visual workflow builder for non-coders                     │ │
│  │                │  • Self-hosted = full control, no per-execution costs         │ │
│  │  N8N           │  • 400+ integrations (CRMs, email, APIs)                      │ │
│  │                │  • Webhook triggers connect frontend to backend              │ │
│  ├────────────────┼─────────────────────────────────────────────────────────────┤ │
│  │                │  • Local LLMs — no data leaves your network                   │ │
│  │  LMStudio      │  • OpenAI-compatible API — drop-in replacement               │ │
│  │                │  • Run any model (Llama, Mistral, Phi, etc)                  │ │
│  │                │  • GPU acceleration when available                            │ │
│  ├────────────────┼─────────────────────────────────────────────────────────────┤ │
│  │                │  • Global CDN — fast load times worldwide                     │ │
│  │  Cloudflare    │  • DDoS protection by default                                 │ │
│  │                │  • Workers for serverless edge functions                     │ │
│  │                │  • Pages for static hosting with git deploy                  │ │
│  └────────────────┴─────────────────────────────────────────────────────────────┘ │
│                                                                                    │
└────────────────────────────────────────────────────────────────────────────────────┘
```

## Force to Technology Mapping

```
┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│    PRESENCE ───────────────────────────────────────────────────► React  │
│                              ─────────────────────────────────► Vite   │
│                              ─────────────────────────────────► TS    │
│                              ─────────────────────────────────► Three  │
│                                                                         │
│    INTELLIGENCE ───────────────────────────────────────────────► N8N   │
│                              ─────────────────────────────────► LM    │
│                                                 Studio ─────────► OpenAI│
│                              ─────────────────────────────────► Webhooks│
│                                                                         │
│    CONNECTION ────────────────────────────────────────────────► Firebase│
│                              ─────────────────────────────────► Firestore│
│                              ─────────────────────────────────► Auth   │
│                                                                         │
│    CONTINUITY ────────────────────────────────────────────────► Cloudflare│
│                              ─────────────────────────────────► Workers │
│                              ─────────────────────────────────► Pages  │
│                              ─────────────────────────────────► Tunnel │
│                              ─────────────────────────────────► R2      │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

## Data Flow Architecture

```
                    ┌─────────────────────────────────────┐
                    │                                     │
                    │          USER BROWSER               │
                    │                                     │
                    │    React App ←→ Firebase Auth       │
                    │         ↓                            │
                    │    HTTPS (WSS for real-time)        │
                    │                                     │
                    └──────────────────┬──────────────────┘
                                       │
                                       │ Cloudflare CDN
                                       │ + DDoS Protection
                                       │
                    ┌──────────────────┴──────────────────┐
                    │                                     │
                    │  ┌─────────────────────────────┐   │
                    │  │      CLOUDLARE EDGE          │   │
                    │  │                              │   │
                    │  │  • Pages (static assets)     │   │
                    │  │  • Workers (edge functions) │   │
                    │  │  • Tunnel (secure tunnels)   │   │
                    │  └─────────────────────────────┘   │
                    │                                     │
                    └──────────────┬─────────────────────┘
                                   │
           ┌───────────────────────┼───────────────────────┐
           │                       │                       │
           ▼                       ▼                       ▼
    ┌─────────────┐        ┌─────────────┐        ┌─────────────┐
    │  FIRESTORE  │        │     N8N     │        │   LMSTUDIO  │
    │  (Database) │        │ (Workflows) │        │  (Local AI) │
    └─────────────┘        └─────────────┘        └─────────────┘
         ▲                       ▲                       ▲
         │                       │                       │
         │ Webhook triggers ─────┘                       │
         │                                               │
         └───────────────────────────────────────────────┘
                        OpenAI-compatible API
```

## Build & Deploy Pipeline

```
┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐
│  WRITE  │───►│  BUILD  │───►│ PUSH    │───►│ DEPLOY  │───►│  LIVE   │
│  CODE   │    │  (Vite) │    │ (Git)   │    │(Wrangler)│   │  SITE   │
└─────────┘    └─────────┘    └─────────┘    └─────────┘    └─────────┘
     │             │              │              │
     │             │              │              ▼
     │         ┌────┴────┐        │        ┌─────────────┐
     │         │  Type   │        │        │ Cloudflare  │
     └────────►│  Check  │◄───────┘        │ Pages       │
               │  (TSC)  │                 │ Workers     │
               └─────────┘                 └─────────────┘
```

## Key Principles

| Principle | Implementation |
|-----------|----------------|
| **No Vendor Lock-in** | All code in client repos. Data exportable from Firestore anytime |
| **Self-Healing** | N8N workflows retry on failure. Cloudflare monitors uptime |
| **Transparency** | Public repos, real-time status pages, audit logs |
| **Zero Infrastructure** | Serverless where possible. Firebase, Cloudflare, N8N handle scaling |

---

*Built with autonomy. Delivered with transparency.*
