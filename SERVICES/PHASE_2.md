# Phase 2 — Hybrid Services
### Your business, automated. Monitored. Visible.

---

## What this phase is

Phase 2 is when your website stops being static and starts being alive. You add automated services that run without you — lead capture, AI scoring, live dashboards, health monitoring. I manage the infrastructure, but you own the code and see everything.

**Hybrid model:** You own the workflows (they're in your GitHub), but they run on my N8N until Phase 3. You see everything through your admin panel. You control the logic.

---

## Phase Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              PHASE 2                                         │
│                        "Hybrid Services"                                    │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│    ┌─────────────────────────────────────────────────────────────────┐     │
│    │                         BI DASHBOARD                             │     │
│    │  Live data visualization ──► Health status ──► Lead pipeline   │     │
│    └─────────────────────────────────────────────────────────────────┘     │
│                                    │                                         │
│           ┌────────────────────────┼────────────────────────┐              │
│           ▼                        ▼                        ▼              │
│    ┌─────────────┐        ┌─────────────┐        ┌─────────────┐         │
│    │ SMART FORMS │        │ AI WORKFLOWS│        │AI ASSISTANT │         │
│    │ + Lead Gen  │───────►│   + N8N      │───────►│ + LMStudio   │         │
│    └─────────────┘        └─────────────┘        └─────────────┘         │
│           │                        │                        │              │
│           └────────────────────────┼────────────────────────┘              │
│                                    ▼                                         │
│                           ┌─────────────┐                                   │
│                           │  SECURITY   │                                   │
│                           │  SENTINEL   │                                   │
│                           │ + Monitor   │                                   │
│                           └─────────────┘                                   │
│                                                                             │
│    OWNERSHIP: Code in your repo │ Running on shared infrastructure         │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Service Cards

---

### 📊 BI Dashboard

**Branch:** `bi-dashboard` | PRESENCE Force | Phase 2

```
┌─────────────────────────────────────┐
│  ┌─────────────────────────────┐    │
│  │     📊 BI DASHBOARD         │    │
│  │                             │    │
│  │  Active Services: ●●●●○○    │    │
│  │  Health: ✓ All Systems      │    │
│  │  Leads Today: 3 (2 Hot)     │    │
│  │  Tree Maturity: 45%         │    │
│  │                             │    │
│  │  [Service Health] [Leads]  │    │
│  │  [Uptime] [AI Scores]       │    │
│  └─────────────────────────────┘    │
└─────────────────────────────────────┘
```

**What it is:**
A live data interface showing the state of your business at a glance — active services, health indicators, lead pipeline, system uptime. Not a static report. A living screen.

**The problem it solves:**
Business owners make decisions on outdated information. A live dashboard turns data into instant visibility — you see what's happening before you have to ask.

**Dependencies:**
| Dependency | Required By |
|------------|-------------|
| Firebase | Data storage for dashboard |
| Smart Forms | Lead data source |
| N8N | Workflow execution logging |
| Web Setup | Active service status |

**Autonomy Boost:**
- Full visibility into all systems
- Real-time data, not delayed reports
- Tree maturity score shows growth

---

### 📝 Smart Forms + Lead Generation

**Branch:** `smart-forms` | CONNECTION Force | Phase 2

```
┌─────────────────────────────────────┐
│  ┌─────────────────────────────┐    │
│  │     📝 SMART FORMS           │    │
│  │                             │    │
│  │  Form Submit ─► N8N ─► You  │    │
│  │           ─► AI Score       │    │
│  │           ─► Auto-Reply     │    │
│  │           ─► Lead Logged    │    │
│  │                             │    │
│  │  Fields: Name, Email,      │    │
│  │  Phone, Service, Budget,    │    │
│  │  Timeline, Message          │    │
│  └─────────────────────────────┘    │
└─────────────────────────────────────┘
```

**What it is:**
A contact form that doesn't just collect data — it triggers an automated response chain. The moment someone submits, N8N captures it, processes it, emails you, replies to the visitor, and logs the lead.

**The problem it solves:**
A standard form sends you an email and stops. You manually reply, manually log the lead, manually follow up. Smart Forms automates the entire chain.

**Dependencies:**
| Dependency | Required By |
|------------|-------------|
| Web Setup | Form lives on website |
| Google Setup | Gmail for notifications |
| N8N | Workflow execution |
| (Optional) LMStudio | AI lead scoring |

**Autonomy Boost:**
- Form code in your repo
- N8N workflow JSON in your repo
- You control what happens after submission

---

### ⚙️ AI Workflow Engineering

**Branch:** `ai-workflows` | INTELLIGENCE Force | Phase 2

```
┌─────────────────────────────────────┐
│  ┌─────────────────────────────┐    │
│  │     ⚙️ AI WORKFLOWS          │    │
│  │                             │    │
│  │  Trigger ─► Process ─► Act  │    │
│  │                             │    │
│  │  ┌─────┐  ┌─────┐  ┌─────┐  │    │
│  │  │Form │─►│N8N  │─►│Email│  │    │
│  │  └─────┘  └─────┘  └─────┘  │    │
│  │           ┌─────┐            │    │
│  │           │ LM  │ (optional) │    │
│  │           └─────┘            │    │
│  │                             │    │
│  │  Your logic. Your flow.     │    │
│  └─────────────────────────────┘    │
└─────────────────────────────────────┘
```

**What it is:**
Automated logic that runs between your tools — triggered by events, processing data, sending notifications, updating records. Built in N8N.

**The problem it solves:**
Every business has recurring tasks that follow the same pattern. That entire chain can be automated. Once built, it runs forever without your attention.

**Dependencies:**
| Dependency | Required By |
|------------|-------------|
| Google Setup | Gmail for notifications |
| N8N | Workflow engine |
| Firebase | Data storage (optional) |
| (Optional) LMStudio | AI processing |

**Autonomy Boost:**
- Every workflow is a JSON file in your repo
- Logic is yours, not locked in a subscription
- You can modify any workflow

---

### 🤖 AI Assistant

**Branch:** `ai-assistant` | INTELLIGENCE Force | Phase 2

```
┌─────────────────────────────────────┐
│  ┌─────────────────────────────┐    │
│  │     🤖 AI ASSISTANT          │    │
│  │                             │    │
│  │  Visitor ─► Chat Widget     │    │
│  │           ─► N8N Webhook   │    │
│  │           ─► LMStudio      │    │
│  │           ─► Response      │    │
│  │                             │    │
│  │  "Not a script. Reasoning." │    │
│  │                             │    │
│  │  Your tone. Your knowledge. │    │
│  │  Your business context.     │    │
│  └─────────────────────────────┘    │
└─────────────────────────────────────┘
```

**What it is:**
An AI that lives on your website and answers questions as you would — using your knowledge, your tone, your context. Not a script. Not an FAQ chatbot. A reasoning model.

**The problem it solves:**
Potential clients visit at 11pm when you're not there. They have a question. They hit a contact form and wait 24 hours — or they leave. The AI Assistant closes that gap.

**Dependencies:**
| Dependency | Required By |
|------------|-------------|
| Web Setup | Widget lives on website |
| N8N | Webhook handler |
| LMStudio | Local AI model |
| System Prompt | Business context |

**Autonomy Boost:**
- System prompt is editable by you
- Model runs locally (no cloud dependency)
- Conversation logic in your N8N

---

### 🔒 Security Sentinel

**Branch:** `security` | SECURITY Force (cross-cutting) | Phase 2

```
┌─────────────────────────────────────┐
│  ┌─────────────────────────────┐    │
│  │     🔒 SECURITY SENTINEL     │    │
│  │                             │    │
│  │  Audit ─► Monitor ─► Alert  │    │
│  │                             │    │
│  │  ┌─────┐  ┌─────┐  ┌─────┐  │    │
│  │  │Check│─►│Watch│─►│Escal│  │    │
│  │  └─────┘  └─────┘  └─────┘  │    │
│  │                             │    │
│  │  Firebase rules             │    │
│  │  GitHub secrets             │    │
│  │  Cloudflare config          │    │
│  │  Credential rotation        │    │
│  └─────────────────────────────┘    │
└─────────────────────────────────────┘
```

**What it is:**
An audit of your digital stack — what's exposed, what's misconfigured, what's vulnerable. Then automated monitoring that watches for those issues continuously.

**The problem it solves:**
Most businesses have security gaps they don't know about — open Firebase rules, API keys in public repos, Cloudflare misconfigured. The audit finds them before they become a crisis.

**Dependencies:**
| Dependency | Required By |
|------------|-------------|
| Web Setup | Website security check |
| Firebase | Database rules check |
| N8N | Health check workflows |

**Autonomy Boost:**
- Audit report in your repo
- Security rules in your repo
- You control the monitoring schedule

---

## What Phase 2 Delivers

| Deliverable | Description |
|-------------|-------------|
| Dashboard live | Visible tree, health status, lead pipeline |
| Multiple services active | At least 3 branches |
| All workflows in repo | JSON files you own |
| Health monitoring | 15-min checks on all services |
| Full knowledge base | Setup guides for every tool |

---

## Cost Structure

Phase 2 services follow the **hybrid model**:

| Model | What it includes |
|-------|-----------------|
| **Managed** | Dashboard, monitoring, maintenance included |
| **Transparent** | You see everything, own the code |

See [FOR_PARTNERS/DEPENDENCIES.md](../FOR_PARTNERS/DEPENDENCIES.md) for full pricing.

---

## Service Dependency Table (Phase 2)

| Service | Depends On | Enables |
|---------|-----------|---------|
| BI Dashboard | Smart Forms, Firebase | Full visibility |
| Smart Forms | Web Setup, Google Setup | Lead Generation |
| AI Workflows | Google Setup, N8N | AI Assistant |
| AI Assistant | AI Workflows, LMStudio | Chat widget |
| Security Sentinel | Web Setup, Firebase | Monitoring |

---

## Toward Phase 3

At Phase 2, you already own most of what you need — the code, the workflows, the documentation. Phase 3 is the final step: transferring the infrastructure from my hosting to yours.

The question "what would it take to run this myself?" becomes answerable — because the documentation is already there.

---

## Related Files

- [PHASE_1.md](./PHASE_1.md) — One-Time Setup
- [PHASE_3.md](./PHASE_3.md) — Full Ownership
- [ARCHITECTURE/AUTONOMY_MODEL.md](../ARCHITECTURE/AUTONOMY_MODEL.md)