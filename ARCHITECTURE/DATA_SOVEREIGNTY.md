# Data Sovereignty — The Arboretum Architecture

*How NeoDome guarantees your data stays yours — structurally, not just promised.*

---

## The Problem with Shared Systems

Most "shared" platforms mean your data mingles with everyone else's:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        THE SHARED DATABASE PROBLEM                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│    Client A's data ──┐                                                      │
│                      ├──▶ Same database ──▶ Can I see Client B's data?     │
│    Client B's data ──┘         │                    ↑                     │
│                                 │                    │                     │
│                                 ▼              Depends on code, not         │
│                         Rules say "no"...         architecture               │
│                         But it's one DB                                   │
│                                                                             │
│    ═══════════════════════════════════════════════════════════              │
│    Your data's security is a PROMISE, not a STRUCTURE.                     │
│    ═══════════════════════════════════════════════════════════              │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

The problem: most multi-tenant systems rely on **code rules** to keep data separate. 
Rules can have bugs. Rules can be misconfigured. Rules can be bypassed.

---

## The Arboretum Solution

NeoDome's architecture uses **Arboretum** — a multi-tenant model where data isolation 
is **structural**, not just promised.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         THE ARBORETUM MODEL                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│         🌳 Client A                   🌳 Client B                   🌳 Client C │
│        ┌─────────┐                 ┌─────────┐                 ┌─────────┐  │
│        │ BRANCHES │                 │ BRANCHES│                 │ BRANCHES│  │
│        │   A₁     │                 │   B₁    │                 │   C₁    │  │
│        │   A₂     │                 │   B₂    │                 │   C₂    │  │
│        │   A₃     │                 │   B₃    │                 │   C₃    │  │
│        └────┬─────┘                 └────┬─────┘                 └────┬─────┘  │
│             │                           │                           │        │
│         ════╧═══════════════════════════╧═══════════════════════════╧════   │
│                                    │                                           │
│                               ┌────┴────┐                                     │
│                               │  ROOTS  │                                     │
│                               │ (shared │ ← Shared infrastructure: N8N,       │
│                               │ engine) │   Firebase, Cloudflare — BUT         │
│                               └─────────┘   isolated at the DATA layer        │
│                                                                             │
│    ═══════════════════════════════════════════════════════════════════        │
│    The engine is shared. The data is not.                                   │
│    Your branches grow in your own soil.                                      │
│    ═══════════════════════════════════════════════════════════════════        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## How It Works

### The Three Layers

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                          THE THREE LAYERS                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│    ┌─────────────────────────────────────────────────────────────────┐     │
│    │                    🌳 THE BRANCHES (Your Data)                    │     │
│    │  • Your leads, clients, workflows, credentials                    │     │
│    │  • Strictly isolated — only your system can read/write            │     │
│    │  • Your Firebase namespace, your Firestore paths                  │     │
│    └─────────────────────────────────────────────────────────────────┘     │
│                                    │                                         │
│                                    │ (isolated by architecture)               │
│                                    ▼                                         │
│    ┌─────────────────────────────────────────────────────────────────┐     │
│    │                    🔧 THE ENGINE (Shared)                        │     │
│    │  • N8N workflows (logic runs the same for everyone)               │     │
│    │  • Firebase infrastructure (but with data isolation)               │     │
│    │  • Cloudflare edge network (fast, secure, shared)                 │     │
│    └─────────────────────────────────────────────────────────────────┘     │
│                                    │                                         │
│                                    │ (isolated by architecture)               │
│                                    ▼                                         │
│    ┌─────────────────────────────────────────────────────────────────┐     │
│    │                    🏠 THE ROOTS (Your Hardware)                  │     │
│    │  • Phase 3 only: you run the engine on your own servers           │     │
│    │  • Complete isolation — even the roots are yours                   │     │
│    │  • No shared infrastructure at all                                │     │
│    └─────────────────────────────────────────────────────────────────┘     │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## The Isolation Mechanism

NeoDome uses **Firebase Custom Claims** — a structural layer that embeds 
client identity directly into the authentication token:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                     FIREBASE CUSTOM CLAIMS                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│    When you log in, your token contains:                                    │
│                                                                             │
│    {                                                                          │
│      "uid": "user_abc123",                                                   │
│      "client_id": "client_a",    ←─── Your identity, baked in               │
│      "role": "client"                                                         │
│    }                                                                          │
│                                                                             │
│    This claim is:                                                            │
│    • Cryptographically signed (can't be faked)                               │
│    • Verified on EVERY database request                                       │
│    • Enforced at the Firebase Security Rules level                          │
│                                                                             │
│    Result: Even if someone hacks the code, they can't read your data        │
│    because the architecture itself says "no."                               │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## What This Means For You

| Scenario | Without Arboretum | With Arboretum |
|----------|------------------|----------------|
| Code has a bug | Your data exposed | Data stays isolated |
| Admin makes a mistake | Cross-client leak possible | Architecturally prevented |
| Someone tries to hack | They might see other data | They physically can't |
| You're on shared N8N | Your workflows mix | Your workflows are separate |
| You export your data | Data mixed with others | Clean, complete export |

---

## The Guarantee

> **"Your data is not just protected by rules. It's protected by architecture."**

This is the difference between:
- "We promise not to look at your data" 
- "Our system is built so we physically can't see your data"

---

## Phase 3: Complete Isolation

When you reach Phase 3, you don't just own your data — you own the entire infrastructure:

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    PHASE 3: COMPLETE SOVEREIGNTY                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│    Your servers ──▶ Your N8N ──▶ Your Firebase ──▶ Your everything        │
│                                                                             │
│    The shared engine is gone. The roots are yours.                          │
│    The arboretum becomes YOUR forest.                                       │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## The Bigger Picture

Arboretum is why NeoDome can offer **true multi-tenancy** without compromising 
security. Every client — from SEED stage to FOREST stage — has their data 
isolated structurally.

This is the architecture that lets me honestly say:
> *"Your data is yours. Not just promised. Architecturally guaranteed."*

---

*NeoDome — Your digital sovereignty, engineered.*
