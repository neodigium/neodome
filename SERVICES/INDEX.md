# Services Index

The NeoDome service model is built around three phases — each building on the last, each adding autonomy. This directory documents every service available across all phases.

---

## Service Overview

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                            NEO DOME SERVICES                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   PHASE 1 ───► PHASE 2 ───► PHASE 3                                        │
│   One-Time   ─►  Hybrid    ─►  Full Ownership                             │
│                                                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   ┌─────────────┐  ┌─────────────┐  ┌─────────────┐                         │
│   │   WEB SETUP │  │BI DASHBOARD │  │   LOCAL     │                        │
│   │  GitHub +   │─►│  + Health   │─►│   STACK     │                        │
│   │ Cloudflare  │  │   Monitor   │  │ n8n + LM    │                        │
│   └─────────────┘  └─────────────┘  └─────────────┘                         │
│         │                │                │                                 │
│         ▼                ▼                ▼                                 │
│   ┌─────────────┐  ┌─────────────┐  ┌─────────────┐                         │
│   │   GOOGLE    │  │SMART FORMS │  │TRANSFER     │                        │
│   │   SETUP     │─►│ + Lead Gen │─►│  COMPLETE   │                        │
│   └─────────────┘  └─────────────┘  └─────────────┘                         │
│                              │                                               │
│                              ▼                                               │
│                      ┌─────────────┐                                       │
│                      │    AI       │                                       │
│                      │ WORKFLOWS   │                                       │
│                      │ + Assistant │                                       │
│                      └─────────────┘                                       │
│                              │                                               │
│                              ▼                                               │
│                      ┌─────────────┐                                       │
│                      │  SECURITY   │                                       │
│                      │  SENTINEL   │                                       │
│                      └─────────────┘                                       │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Phase Overview

| Phase | Model | Services | Autonomy |
|-------|-------|----------|----------|
| **Phase 1** | One-Time | Web Setup, Google Ecosystem | You own infrastructure from day one |
| **Phase 2** | Hybrid | BI Dashboard, Smart Forms, Lead Gen, AI Workflows, AI Assistant, Security Sentinel | Shared management, dashboard visibility |
| **Phase 3** | Full Ownership | Local Stack Transfer | Complete ownership, self-hosted |

---

## Service Dependency Table

| Service | Depends On | Enables |
|---------|-----------|---------|
| **Web Setup (Phase 1)** | GitHub, Cloudflare | All other services |
| **Google Ecosystem (Phase 1)** | Google Account | Smart Forms, AI Workflows, Health Monitor |
| **Smart Forms (Phase 2)** | Web Setup, Google Setup | Lead Generation |
| **BI Dashboard (Phase 2)** | Web Setup, Smart Forms | Full visibility |
| **Lead Generation (Phase 2)** | Smart Forms | Pipeline management |
| **AI Workflows (Phase 2)** | Google Setup, N8N | Lead scoring, automation |
| **AI Assistant (Phase 2)** | AI Workflows, LMStudio | Chat widget |
| **Security Sentinel (Phase 2)** | Web Setup, Firebase | Monitoring |
| **Local Stack (Phase 3)** | All Phase 2 services | Self-hosted n8n + LMStudio |

---

## Service Cards

### Phase 1 — One-Time Setup
- [Web Development](./PHASE_1.md#web-development) — GitHub + Cloudflare
- [Google Ecosystem](./PHASE_1.md#google-ecosystem-setup) — Your Google account

### Phase 2 — Hybrid Services
- [BI Dashboard](./PHASE_2.md#bi-dashboard) — Live data visualization
- [Smart Forms](./PHASE_2.md#smart-forms) — Contact form + lead capture
- [Lead Generation](./PHASE_2.md#lead-generation) — AI-scored pipeline
- [AI Workflows](./PHASE_2.md#ai-workflows) — N8N automation
- [AI Assistant](./PHASE_2.md#ai-assistant) — Chat widget
- [Security Sentinel](./PHASE_2.md#security-sentinel) — Monitoring + audit

### Phase 3 — Full Ownership
- [Local Stack](./PHASE_3.md) — Self-hosted transfer

---

## Related Documents

- [ARCHITECTURE/4_PILLARS.md](../ARCHITECTURE/4_PILLARS.md) — The four forces
- [ARCHITECTURE/AUTONOMY_MODEL.md](../ARCHITECTURE/AUTONOMY_MODEL.md) — Ownership progression
- [FOR_PARTNERS/DEPENDENCIES.md](../FOR_PARTNERS/DEPENDENCIES.md) — Full dependency chain