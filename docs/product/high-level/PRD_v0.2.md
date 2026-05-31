# Product Requirements Document

| Field | Value |
|---|---|
| **Product Name** | TrustAI *(working name — finalize)* |
| **Document Version** | 0.2 (adds ecosystem & extensibility architecture) |
| **Owner** | Founding team |
| **Status** | Draft — pre-engineering |
| **Last Updated** | May 28, 2026 |
| **Target GA (V1)** | August 2026 |
| **Target GA (V1.5 open APIs)** | November 2026 |
| **Supersedes** | `PRD_v0.1.md` |

### Changelog from v0.1 → v0.2

- **NEW** Section 9.9: "Open Public API — Read Endpoints for External GRC Tools"
- **NEW** Section 9.10: "OAuth 2.1 Delegated Access for GRC Integrations"
- **NEW** Section 9.11: "MCP Server for Compliance Data"
- **NEW** Section 11.5: "Ecosystem & Standards Architecture" (the doctrine)
- **NEW** Functional requirements FR-API-1 through FR-API-7
- **UPDATED** Executive Summary: dual positioning as product + infrastructure layer
- **UPDATED** Goals & Non-Goals: ecosystem objectives added
- **UPDATED** Competitive Positioning: shifts Vanta/Drata/SafeBase from competitors to partner candidates
- **UPDATED** Launch Plan: adds V1.5 phase (Weeks 12-20) for ecosystem launch
- **UPDATED** Risks & Mitigations: adds commoditization + invisible-plumbing risks
- **UPDATED** Data Model: adds API keys, webhook subscriptions, OAuth grants
- **UPDATED** Open Questions: ecosystem-specific items

---

## 1. Executive Summary

TrustAI is the **runtime evidence layer for AI agent compliance**. A drop-in SDK records every AI agent action with full identity, provenance, and policy context. The platform serves two complementary audiences:

1. **Direct product surface** — fintech AI companies install TrustAI to auto-fill enterprise AI security questionnaires, publish branded trust centers, and generate SOC 2 evidence packs. This is the V1 wedge and primary revenue driver.

2. **Ecosystem layer** — open public APIs let existing GRC tools (Vanta, Drata, SafeBase, Hyperproof) read TrustAI's runtime evidence, transforming them from competitors into distribution channels. This is the V1.5 expansion and the moat-defining play.

**The architecture doctrine: "Open Reads, Closed Writes."** External tools can read every event, decision, control mapping, and evidence pack through a versioned public API. They cannot write events, register agents, or generate evidence. The SDK install remains the sole path to runtime evidence creation — preserving the data network effect, customer relationship, and brand moat while enabling ecosystem distribution.

V1 targets fintech AI startups in active enterprise sales cycles. V1.5 transforms competitive dynamics: instead of fighting Vanta for the customer surface, TrustAI becomes the AI-agent runtime layer Vanta reads from. This shifts the realistic outcome from "$50-300M acqui-hire" to "category-defining infrastructure with multi-channel distribution."

---

## 2. Problem Statement

### The User Problem

Fintech AI startups face a binding constraint: every enterprise sales cycle now includes an **AI-specific security review** with 50-200 questions auditors and procurement teams demand answers to. Today, founders:

- Spend 2-6 weeks per deal hand-writing answers
- Submit incomplete responses that stall negotiations
- Engage $20K+ consultants to draft policies they don't have
- Lose deals (or close at discount) because their controls evidence is weak
- Repeat the entire cycle for every new customer's annual vendor review

### The Integration Fragmentation Problem (new in v0.2)

Even when customers adopt compliance tooling, they end up with a fractured stack:
- **Vanta or Drata** for general SOC 2 automation (no agent data)
- **Arcade or Composio** for agent OAuth (no compliance context)
- **LangSmith or Helicone** for LLM observability (no evidence emission)
- **SafeBase** for trust centers (no AI specifics)
- **Spreadsheets** for vendor security questionnaires (no automation)

No layer connects these. Each customer rebuilds the same integration glue badly. The market lacks an **agent runtime evidence layer** that all these tools could share — analogous to how Plaid became the shared bank-data layer for fintech apps.

### The Market Problem

In May 2026, no product combines all four of:
1. **Runtime evidence collection** (actual agent activity, not policy claims)
2. **AI-specific control mapping** (SOC 2, EU AI Act, ISO 42001 interpreted for agents)
3. **Developer-installable** (5-minute SDK, not enterprise procurement)
4. **Founder-priced** ($99-$2,500/month, not $50K+ ACVs)

And no product has positioned itself as **the open infrastructure layer** other GRC tools consume.

### Why Now

- **EU AI Act enforcement starts August 2026** — fintech AI vendors selling into EU need conformity evidence within 90 days
- **SOC 2 auditors have hardened AI expectations in 2026** — point-in-time policy attestations no longer pass; runtime evidence is required
- **Enterprise procurement has institutionalized AI security questionnaires** — every Fortune 500 has a standard 100-question intake
- **The agent stack standardized in 2025-2026 around MCP + OAuth 2.1** — making runtime instrumentation tractable for the first time
- **GRC consolidation is accelerating** ($96B in M&A in 2026) — incumbents are looking for AI-runtime modules they don't want to build

---

## 3. Goals & Non-Goals

### V1 Goals (the wedge)

1. Ship a Python + TypeScript SDK that captures runtime agent activity with one-line integration
2. Ship a SOC 2 control library mapped to the 54 questions auditors actually ask in 2026
3. Ship the questionnaire auto-fill engine as the primary acquisition demo
4. Ship a live, branded trust center as the primary retention artifact
5. Ship a one-click SOC 2 Evidence Pack export for auditor handoff
6. **Architect for open APIs from day 1** — separate auth namespace, versioned schemas, webhook primitives, all built but internally-scoped
7. Capture 50 paying fintech customers in 90 days post-launch
8. Lock 1 Big 4 audit firm "preferred format" relationship within 12 months

### V1.5 Goals (the ecosystem expansion)

1. Launch open public API with OAuth 2.1 delegated access
2. Ship 3 OSS reference connectors: Vanta, Drata, SafeBase
3. Publish "Agent Compliance Event v1" schema as a public spec
4. Sign 1 formal integration partnership with a major GRC tool
5. Ship MCP server for compliance data (`mcp://compliance.trustai.io`)
6. Reach 150 paying direct customers + 1 integration-partner customer base

### V1 + V1.5 Non-Goals

- Multi-framework support beyond SOC 2 + EU AI Act (HIPAA, FINRA, ISO 42001 deferred to V2)
- Customer-authored controls (we provide the library; they don't extend it)
- On-prem / VPC deployment
- Multi-tenant white-label
- AI safety / bias testing (out of scope — different product)
- Generic SOC 2 automation (Vanta-style policies/training/scans) — we are agent-runtime-specific
- Selling to enterprise CISOs (V1 buyer is founder/CEO)
- **Opening write endpoints to external consumers** — the "Closed Writes" half of the doctrine is non-negotiable

---

## 4. Target Customer (ICP)

### Primary V1 ICP (Direct Customers)

**Fintech AI startup, Series Seed to Series B (5-150 employees), with at least one enterprise customer in active sales cycle or signed within the last 12 months.**

Signals:
- Building agents that touch financial data (banking, payments, accounting, compliance, lending)
- Selling to banks, credit unions, fintechs, or enterprise finance teams
- Has been asked to complete at least one vendor security questionnaire in the last 6 months
- No dedicated CISO yet, no Vanta or has Vanta but it doesn't cover agents

### Secondary V1.5 ICP (Integration Partners)

**GRC tools serving 1,000+ customers who are being asked for "AI compliance" features.**

Target list:
- **Vanta** — largest SOC 2 automation platform; customers demanding AI coverage
- **Drata** — direct competitor to Vanta; same pressure
- **SafeBase** (HubSpot) — trust center platform; needs AI-specific surfaces
- **Hyperproof** — mid-market GRC; less direct competition with Vanta
- **Anecdotes, Secureframe, Sprinto** — second-tier GRC; faster to integrate

### V1 ICP Exclusions

- Pre-revenue startups with no enterprise sales motion (will not convert)
- Pure consumer AI products with no enterprise buyers (wrong buyer)
- Enterprise companies (>1,000 employees) with existing GRC programs (wrong sales motion)
- Non-fintech verticals in V1 (refused for vertical concentration discipline)

### Key Buyer Personas

**"The Founding Sales Engineer"** (V1 direct buyer)
- Title: CTO / Head of Eng / Founding SE / CEO at sub-50-person fintech AI startup
- Pain: Has 3-5 enterprise deals stuck in security review; spends 10+ hours/week on questionnaires
- Budget authority: Can swipe a credit card up to $500/month without approval
- Trigger event: Specific enterprise buyer sends a multi-page AI security questionnaire

**"The GRC Tool Product Lead"** (V1.5 partner buyer)
- Title: Head of Product / VP Eng at Vanta, Drata, SafeBase, Hyperproof
- Pain: Customers asking for "AI compliance coverage"; building it natively would require 12-18 months of agent runtime engineering
- Decision: Integrate TrustAI as their AI module vs. build vs. acquire
- Trigger event: 10th+ customer asks for AI agent evidence in a quarterly review

---

## 5. Success Metrics

### V1 Launch Metrics (Day 1 → Day 90 post-launch)

| Metric | Target |
|---|---|
| Signups | 500 |
| SDK installations | 300 |
| Paying customers | 50 |
| MRR | $10K |
| % customers in fintech | ≥ 80% |
| Time from signup → SDK install | < 30 min (p50) |
| Time from install → first evidence event | < 10 min (p50) |
| Questionnaires auto-filled per customer/month | ≥ 2 |
| NPS (paying customers) | ≥ 50 |
| Trust pages published | ≥ 30 |

### V1.5 Launch Metrics (Day 90 → Day 180)

| Metric | Target |
|---|---|
| Public API keys issued | 50+ |
| External webhook subscriptions active | 20+ |
| OSS reference connector downloads | 500+ |
| GRC partnership signed (LOI or MoU) | 1 |
| Schema spec public on GitHub | Yes |
| Customers reached via partner channel | 10+ |

### Year 1 Strategic Metrics

| Metric | Target |
|---|---|
| Paying direct customers | 150 |
| ARR (direct) | $300K |
| Big 4 partnership (signed MoU or written endorsement) | 1 |
| Major GRC partnership (Vanta/Drata/SafeBase/Hyperproof) | 1 |
| Fintech AI questionnaires in corpus | 200 |
| SOC 2 audits passed using our evidence | 20+ |
| Open spec submitted to standards body (AICPA/NIST) | 1 |
| Logo churn (annualized) | < 15% |

### Anti-Metrics

- Total signups across all verticals
- Free tier conversion rate
- Feature breadth
- Number of integrations (we'd rather have 3 deep than 30 shallow)

---

## 6. Competitive Positioning (v0.2 — reshaped by ecosystem strategy)

The V1.5 open-API strategy transforms the competitive matrix. Most "competitors" become partner candidates.

| Player | V1 view (closed product) | V1.5 view (open ecosystem) |
|---|---|---|
| **Vanta / Drata** | Direct competitor; threat | **Integration partner**; their customers ask for AI coverage they can't build |
| **SafeBase (HubSpot)** | Direct competitor on trust centers | **Integration partner**; we provide live runtime data their static trust pages lack |
| **Arcade / Composio** | Adjacent; agent auth | Adjacent; potential bidirectional integration (they auth, we attest) |
| **Delve** | Service competitor | **Channel partner**; auditor firms become resellers |
| **Natoma** | Enterprise MCP gateway | Adjacent; potential MCP-layer cross-integration |
| **Microsoft Entra Agent ID** | Free agent identity (MS stack) | Adjacent; we sit above identity, providing evidence |
| **Hyperproof, Anecdotes, Secureframe** | Mid-market GRC tools | **Integration partners**; smaller players move faster than Vanta |
| **Auditing firms (Big 4, Schellman, A-LIGN)** | N/A | **Channel partners**; recommend our format to clients |

**True direct competitors after V1.5:**
- Any new entrant attempting the same "runtime + AI compliance + founder-buyer + vertical" wedge
- Anthropic/OpenAI if they ship native compliance evidence inside their SDKs (mitigated by cross-provider neutrality)

---

## 7. User Stories

### Direct Customer Stories
- **As a fintech AI founder**, I want to paste my buyer's 100-question AI security questionnaire and receive 70+ auto-filled answers in 10 minutes, so I can stop losing deals to slow procurement.
- **As a fintech AI founder**, I want a branded public trust page that buyers can self-serve before our first call.
- **As a head of engineering at an AI startup**, I want to install an SDK in <30 minutes and immediately see runtime evidence captured.
- **As an engineering lead**, I want to register the models, prompts, and providers we use *once*, so my team doesn't think about compliance in every code change.
- **As a CTO**, I want my SDK to detect runaway agent loops and stop them before they hit budget thresholds.
- **As a founder facing SOC 2 audit**, I want a one-click Evidence Pack mapped to control IDs my auditor recognizes.
- **As a founder hit with a GDPR DSAR**, I want to query every agent decision that touched a specific data subject and produce a deletion proof.

### Ecosystem / Integration Stories (new in v0.2)
- **As a Vanta product manager**, I want to ingest TrustAI's agent runtime evidence into our SOC 2 audit log, so our customers can claim "AI-ready" compliance without us building agent infrastructure.
- **As a customer using both Vanta and TrustAI**, I want to connect them via OAuth so my Vanta dashboard shows my agent evidence alongside my regular SOC 2 evidence.
- **As an auditor**, I want to query a single MCP endpoint for any TrustAI customer's evidence — using my own AI tools — without learning a custom dashboard per client.
- **As an enterprise CISO**, I want to push TrustAI events into our SIEM (Splunk, Sentinel) via webhooks, so AI agent activity sits in the same investigation surface as our other logs.
- **As a fintech founder**, I want to keep my existing GRC tool but plug TrustAI in for the AI parts, so I don't have to choose between paying for two overlapping platforms.

### Standards / Public Good Stories
- **As an AICPA AI Assurance Task Force member**, I want a candidate schema for "agent compliance event" that I can evaluate as a potential reference standard.
- **As an open-source community member**, I want to fork the TrustAI schema and write a connector for a GRC tool TrustAI hasn't covered.

---

## 8. Product Overview

TrustAI now has **two product surfaces** sharing one backend:

```
┌─────────────────────────────────────────────────────────────────┐
│  V1 DIRECT PRODUCT SURFACE                                      │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │   SDK        │  │  Dashboard   │  │  Trust Page  │          │
│  │  (Python+TS) │  │  (admin UI)  │  │  (public)    │          │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘          │
└─────────┼──────────────────┼──────────────────┼─────────────────┘
          │                  │                  │
┌─────────▼──────────────────▼──────────────────▼─────────────────┐
│  CORE TRUSTAI BACKEND                                           │
│  • Evidence pipeline  • Control library  • Corpus              │
│  • Hash-chained audit  • Registries  • Questionnaire engine    │
└─────────┬───────────────────────────────────────────────────────┘
          │
┌─────────▼───────────────────────────────────────────────────────┐
│  V1.5 OPEN ECOSYSTEM SURFACE                                    │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │  Public API  │  │   Webhooks   │  │  MCP Server  │          │
│  │  (OAuth 2.1) │  │  (signed)    │  │  (compliance)│          │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘          │
└─────────┼──────────────────┼──────────────────┼─────────────────┘
          │                  │                  │
┌─────────▼──────────────────▼──────────────────▼─────────────────┐
│  EXTERNAL CONSUMERS                                             │
│  Vanta │ Drata │ SafeBase │ Hyperproof │ Datadog │ Auditors    │
└─────────────────────────────────────────────────────────────────┘
```

**Architectural doctrine** (see Section 11.5):
- All write/runtime operations remain SDK-only and proprietary
- All read operations are exposed through versioned public APIs
- The SDK install is the only path to evidence creation, even when the evidence is consumed downstream by external tools
- Versioned schemas published on GitHub establish TrustAI as the reference implementation

---

## 9. Functional Requirements

### 9.1 SDK (Python + TypeScript)

**FR-SDK-1**: Wrap the major LLM clients (`anthropic`, `openai`, `bedrock`, `vertex`) with one line:
```python
from trustai import TrustAnthropic
client = TrustAnthropic(api_key="...", trust_api_key="...")
```

**FR-SDK-2**: Provide a session context manager that binds agent + user + task + framework context to all calls inside it.

**FR-SDK-3**: Auto-capture per model call: agent ID, user ID, task ID, model ID, prompt ID, guardrail IDs, vendor ID, scopes, tool calls, input hash, output hash, cost, latency, timestamps.

**FR-SDK-4**: Implement local-first state with async batched upload to backend (target: 0ms added latency on hot path, p99 < 5ms).

**FR-SDK-5**: Run loop detection locally (same tool args repeated N times, tokens/second exceeded, max turns reached) and emit anomaly events without blocking the hot path.

**FR-SDK-6**: Apply registered redaction policies to logged inputs/outputs before upload (PII/PHI never leaves customer process unredacted).

**FR-SDK-7**: Operate in test mode (`trust_test_*` keys) without billable usage.

**FR-SDK-8**: Survive network partitions with last-known-good budget/policy state for up to 60 seconds.

**FR-SDK-9 (new)**: SDK-issued auth credentials are structurally separated from external API keys at the auth layer. SDK credentials can write events; external API keys cannot, regardless of scope.

### 9.2 Core API (Internal — V1)

**Existing-style endpoints** (carried forward):
- `POST /v1/agents` — register agent (SDK only)
- `POST /v1/grants` — create OBO delegation grant (SDK only)
- `POST /v1/grants/{id}/verify` — runtime check + evidence emission (SDK only)
- `POST /v1/grants/{id}/revoke` — revoke grant (SDK only)
- `POST /v1/approvals` + `POST /v1/approvals/{id}/decide` — human oversight
- `GET /v1/audit/events` — query audit log (will be exposed publicly in V1.5)

**Registry endpoints** (SDK + dashboard only):
- `POST /v1/models` — Model Registry
- `POST /v1/prompts` — Prompt Registry
- `POST /v1/vendors` — Vendor Registry
- `POST /v1/guardrails` — Guardrail Registry
- `POST /v1/eval-runs` — Eval Gate records
- `POST /v1/changes` + approve/deploy/rollback — Change Request workflow
- `POST /v1/redaction-policies` — Declarative redaction rules

**Compliance endpoints**:
- `GET /v1/controls` — Control library (read; will be exposed publicly in V1.5)
- `GET /v1/questions` — Auditor question knowledge base (read; subset exposed publicly in V1.5)
- `POST /v1/questionnaires` — Submit questionnaire for auto-fill (closed; proprietary engine)
- `GET /v1/questionnaires/{id}` — Retrieve answered questionnaire (read; exposed publicly in V1.5)
- `GET /v1/evidence/export?framework=SOC2&period=...` — Generate Evidence Pack (read; exposed publicly in V1.5)
- `GET /v1/decisions/{id}` — Reconstruct full decision context (will be exposed publicly in V1.5)
- `POST /v1/data-subjects/{id}/request` — DSAR handling
- `POST /v1/incidents` — Log incidents + IR tests

**Admin endpoints**:
- `POST /v1/agents/{id}/decommission`
- `POST /v1/credentials/rotate`
- `POST /v1/anomalies`
- `POST /v1/acknowledgments` (policy/AUP)

### 9.3 Registries (the SOC 2 CC8 backbone)

**FR-REG-1: Model Registry**. Every model used must be registered with provider, version, evaluation metrics, approver, deployment timestamp, rollback target. SDK auto-resolves model name in API calls to a registered ID.

**FR-REG-2: Prompt Registry**. Prompts stored with content hash, version, parent_version (DAG), approver. SDK helper `client.prompts.get("name")` returns the current version.

**FR-REG-3: Vendor Registry**. Model providers, vector DBs, MCP servers, tools registered with contract metadata (DPA, BAA, MSA), allowed data categories, subprocessor lists.

**FR-REG-4: Guardrail Registry**. Guardrails (regex, classifier, scope rule) declared centrally; SDK references by name.

### 9.4 Questionnaire Engine (the acquisition magnet)

**FR-Q-1**: Accept questionnaire upload in formats: SIG, CAIQ, Word, PDF, plain text, custom CSV.

**FR-Q-2**: Parse each question, classify against the knowledge base, propose 1-3 candidate matches with confidence scores.

**FR-Q-3**: Auto-fill answers by querying the customer's evidence pipeline. Each answer cites evidence event IDs.

**FR-Q-4**: Flag gaps where insufficient evidence exists, with a 30-minute "fix plan."

**FR-Q-5**: Allow human edit before export. Edits feed back to the canonical knowledge base (anonymized).

**FR-Q-6**: Export filled questionnaire as branded PDF, DOCX, or original format.

**FR-Q-7**: Maintain a customer-specific question library so repeated requests reuse polished answers.

### 9.5 Trust Page

**FR-TP-1**: Auto-generated public URL: `trust.{customername}.com` or `{customername}.trustpage.ai`.

**FR-TP-2**: Sections: AI Agent Inventory, Models in Use, Data Flows, Frameworks Claimed, Live Activity Stats, Incident Log, Approval Stats, Certifications, Change Log, Subprocessors.

**FR-TP-3**: Updates live from runtime evidence.

**FR-TP-4**: Permanent persistent "Secured by TrustAI" badge with audit-link verification.

**FR-TP-5**: Allow gated sections (NDA-required, log-in required).

**FR-TP-6**: Embeddable badge for customer's own marketing site.

### 9.6 SOC 2 Evidence Pack Export

**FR-EP-1**: Generate a zip with control-by-control evidence files, hash-chain proof, auditor cover sheet, event ID indexes, manifest CSV.

**FR-EP-2**: Support period filters (Q1, Q2, custom date range, point-in-time).

**FR-EP-3**: Map evidence to control IDs in the format the customer's auditor specifies.

**FR-EP-4**: Include cryptographic proof of completeness (Merkle root, signed by TrustAI KMS).

**FR-EP-5**: Auditor Portal access — invite the customer's auditor by email.

### 9.7 Approval Flow

**FR-APR-1**: Configurable triggers: scope pattern, cost threshold, data category, agent risk class.

**FR-APR-2**: Notification channels: Slack, email, webhook, hosted UI link.

**FR-APR-3**: Approver responds via single-click hosted UI; SDK blocks the agent until decision or timeout.

**FR-APR-4**: Every approval recorded with reviewer identity, timestamp, reason, decision.

**FR-APR-5**: Timeout behavior configurable.

### 9.8 Dashboard

**FR-DSH-1**: Sections: Activity Feed, Agents, Grants, Models/Prompts/Vendors/Guardrails, Audit Log, Approvals Queue, Anomalies, Trust Page Settings, Evidence Exports, Questionnaires, Frameworks, Team, Billing, **API Keys**, **Webhooks**, **Integrations**.

**FR-DSH-2**: Filter audit log by every dimension.

**FR-DSH-3**: Real-time anomaly feed with Slack/PagerDuty integration.

**FR-DSH-4**: Use Clerk for dashboard auth.

---

### 9.9 Open Public API — Read Endpoints for External GRC Tools (NEW — V1.5)

**FR-API-1**: All read endpoints in Section 9.2 are exposed to external consumers via a separate auth path (OAuth 2.1 or scoped API keys). Internal SDK and external consumers cannot use each other's credentials.

**FR-API-2**: Read endpoints exposed publicly (with appropriate scopes):
- `GET /v1/events` — query audit events
- `GET /v1/events/{id}` — single event detail
- `GET /v1/controls` — control library (TrustAI's reference mapping)
- `GET /v1/controls/{id}` — single control detail
- `GET /v1/agents` — agent inventory (read)
- `GET /v1/grants` — grant records (read)
- `GET /v1/decisions/{id}` — decision reconstruction
- `GET /v1/evidence/export` — generate evidence pack
- `GET /v1/questionnaires/{id}` — answered questionnaire (customer's own only)
- `GET /v1/trust-summary` — public-facing summary suitable for trust page embed
- `GET /v1/models`, `GET /v1/prompts`, `GET /v1/vendors`, `GET /v1/guardrails` — registry reads
- `GET /v1/approvals` — approval history (read)
- `GET /v1/anomalies` — anomaly log (read)

**FR-API-3**: All public events emit using a versioned schema `agent-compliance-event/v1` (see Section 11.5 for spec governance). Every event payload includes `spec_version` field.

**FR-API-4**: All public endpoints support pagination (`cursor`-based, not offset), filter parameters, and `If-Modified-Since` headers for efficient polling.

**FR-API-5**: Rate limits per scope:
- Standard read: 100 req/min per API key
- Bulk export: 10 req/min
- Real-time event subscription: webhook preferred over polling

**FR-API-6**: Public API endpoints versioned via URL prefix (`/v1/`, `/v2/`); deprecation window minimum 12 months with monthly customer notifications during deprecation.

**FR-API-7**: All public reads are **read-only**. No mutation endpoints exposed to external API keys, regardless of scope grants. This is enforced at the auth-middleware layer, not at the route layer.

#### Authentication for External Consumers

Two modes supported:

**Mode A — Customer-issued API keys**
- Created in dashboard under "Integrations → API Keys"
- Scoped: `read:events`, `read:controls`, `read:evidence`, `read:agents`, `read:approvals`, `subscribe:webhooks`
- IP allowlist optional
- Auto-rotated reminder at 90 days
- Each key trackable in audit log (every request logs `api_key_id`)
- Format: `tai_pub_*` (vs SDK keys: `tai_sk_*`)

**Mode B — OAuth 2.1 delegated access (recommended for SaaS integrations)**
- Standard OAuth 2.1 flow with PKCE
- GRC tool registers as OAuth client; customer authorizes from dashboard
- Refresh tokens, scoped access tokens
- Tokens are JWT-formatted, signed by TrustAI KMS
- Discovery endpoint: `/.well-known/oauth-authorization-server`
- This is the path Vanta/Drata/SafeBase would use

#### Webhook Subscriptions

```http
POST /v1/webhooks
{
  "url": "https://vanta.com/webhooks/trustai",
  "events": ["evidence.created", "control.violation", "approval.decided", "anomaly.detected"],
  "framework_filter": ["SOC2"],
  "agent_filter": null,
  "signing_secret": "auto-generated-hmac-secret",
  "active": true
}
```

- Standard webhook patterns: HMAC-SHA256 signing, exponential retry with jitter, replay-protection nonce, idempotency keys
- Webhook log accessible to customer (Integrations → Webhooks → Log)
- Failed delivery alerts to integrator
- Replay endpoint for last 7 days

### 9.10 OAuth 2.1 Delegated Access for GRC Integrations (NEW — V1.5)

**FR-OAUTH-1**: Implement OAuth 2.1 + PKCE as the primary delegated-access mechanism.

**FR-OAUTH-2**: GRC integrators register as confidential clients via dashboard (V1.5) or programmatically (V2). Each client gets a client ID, secret, and a configurable list of allowed redirect URIs.

**FR-OAUTH-3**: Scope taxonomy:
- `read:events.audit`
- `read:events.evidence`
- `read:controls`
- `read:agents`
- `read:approvals`
- `read:evidence.export`
- `subscribe:webhooks`
- `read:trust-summary` (intentionally minimal, suitable for public trust pages)

**FR-OAUTH-4**: Consent UI is hosted by TrustAI, branded, and shows the customer exactly which GRC tool is requesting what scopes. Consent is revocable at any time from the dashboard.

**FR-OAUTH-5**: Refresh tokens valid 90 days; access tokens valid 1 hour. Tokens revocable mid-session.

**FR-OAUTH-6**: All OAuth events (grant, refresh, revoke) logged in the customer's audit trail.

### 9.11 MCP Server for Compliance Data (NEW — V1.5)

**FR-MCP-1**: Host a public MCP server at `mcp://compliance.trustai.io` (or appropriate URI scheme per MCP spec at launch time).

**FR-MCP-2**: Authentication via the same OAuth 2.1 flow as the public REST API.

**FR-MCP-3**: Tools exposed:
- `get_control_status(customer_id, control_id)` → live evidence status
- `query_evidence(customer_id, framework, period, control_id?)` → list of evidence records
- `get_trust_summary(customer_id)` → public-facing summary
- `get_decision(customer_id, decision_id)` → reconstruct a decision
- `list_agents(customer_id)` → agent inventory
- `list_approvals(customer_id, period)` → human oversight records

**FR-MCP-4**: Each MCP call logs to the customer's audit trail with caller identity (auditor, GRC tool, internal AI agent).

**FR-MCP-5**: MCP server respects the same rate limits and scopes as REST API.

**Why MCP matters**: Any AI agent (Claude, GPT, internal copilots) can natively query a customer's compliance status as a tool. Auditors increasingly use AI assistants; TrustAI becomes the canonical tool they call. Competitors not shipping MCP servers fall behind in the agent-tooling world.

### 9.12 Reference OSS Connectors (NEW — V1.5)

We ship and maintain three OSS reference connectors at V1.5 launch:

**FR-CONN-1**: `trustai/vanta-connector` (TypeScript) — pulls TrustAI events via OAuth and pushes them into Vanta's audit log API. MIT-licensed.

**FR-CONN-2**: `trustai/drata-connector` (TypeScript) — same for Drata. MIT-licensed.

**FR-CONN-3**: `trustai/safebase-connector` (TypeScript) — pushes runtime evidence into SafeBase trust center UIs. MIT-licensed.

Future (V2): Hyperproof, Anecdotes, Secureframe, Datadog, Splunk SIEM connectors — community-contributed encouraged.

Each connector:
- Documented for one-command install
- Includes a Docker image for self-hosted deployment
- Includes a hosted deployment option (TrustAI runs it; customer pays a small surcharge)

---

## 10. SOC 2 Compliance Mapping

*(Identical to v0.1 — see PRD_v0.1.md Section 10 for the full 54-question → feature mapping table. No changes in v0.2.)*

---

## 11. Non-Functional Requirements

### 11.1 Performance
- SDK hot-path overhead: ≤ 5ms p99 added to LLM call latency
- API verify endpoint: ≤ 50ms p99 (rarely hit; SDK is local-first)
- **Public API read endpoints**: ≤ 200ms p99 (new in v0.2)
- **MCP server tool calls**: ≤ 300ms p99 (new in v0.2)
- Evidence Pack export: ≤ 60 seconds for 1 year of evidence
- Trust page load: ≤ 1.5s p95

### 11.2 Reliability
- 99.9% API uptime SLA (paid tiers)
- 99.5% Public API uptime SLA (V1.5; integration partners get higher SLA)
- Multi-region read replicas (US + EU) by V1.5
- Graceful SDK degradation on backend outage

### 11.3 Security
- SOC 2 Type II within 6 months of GA
- All evidence storage encrypted at rest with AWS KMS / GCP CMEK
- Hash-chained audit log with WORM storage tier for paid customers
- Per-tenant data residency (US or EU) selectable at signup
- All employee access to customer evidence MFA-required, audited
- Public bug bounty within 90 days of GA
- **External API keys MFA'd for issuance** (new in v0.2)
- **OAuth consent flow with explicit scope display** (new in v0.2)

### 11.4 Compliance
- SOC 2 Type II (target Q1 2027)
- ISO 27001 (target Q2 2027)
- GDPR-compliant (day 1)

### 11.5 Ecosystem & Standards Architecture (NEW — the doctrine)

This subsection codifies the architectural rules that prevent V1's openness from drifting during execution.

**11.5.1 The "Open Reads, Closed Writes" doctrine**

- **All write/mutation operations remain SDK-only and proprietary.** No external API key, OAuth scope, or MCP tool can create, modify, or delete records. Enforced at the auth-middleware layer, not at the route layer (defense in depth).
- **All read operations are eligible for public exposure**, gated by per-tenant scope grants. Exposure decisions are explicit, never default.
- **SDK install is the sole path to evidence creation.** This is the moat. Never compromise this even when integration partners request it.
- **The questionnaire engine and corpus remain proprietary.** External tools can read auto-filled questionnaires (the *output*) but cannot access the corpus, matching logic, or knowledge base directly.

**11.5.2 Schema governance**

- All public schemas live in `github.com/trustai/spec` (or a vendor-neutral org if we successfully donate to a standards body)
- Schema versioning follows SchemaVer: `model-major.revision.addition`
- Backwards-incompatible changes only at major version bumps, with 12-month deprecation windows
- Reference implementations of consumers ship as OSS at each major version
- We publish the spec under a permissive license (MIT/Apache 2.0) to enable broad adoption

**11.5.3 Standards body engagement**

- By Month 9: submit "Agent Compliance Event v1" to AICPA AI Assurance Task Force as candidate reference schema
- By Month 12: engage NIST AI Safety Institute about evidence schema standardization
- By Month 18: aim for adoption as informal industry reference, with TrustAI cited as originator
- Goal: become the reference implementation auditors recognize, even when the spec is officially vendor-neutral

**11.5.4 Partnership tiers**

| Tier | Who | What they get | What we get |
|---|---|---|---|
| **Open** | Anyone with customer API key | Read access, OSS connectors, public docs | Distribution, validation |
| **Listed** | Verified GRC tools | Logo placement, listed in integrations dir | Co-marketing |
| **Certified** | Tools that meet spec test suite | "TrustAI Certified" badge, deeper API features | Quality control, brand reinforcement |
| **Strategic** | Vanta, Drata, SafeBase, Hyperproof | Co-marketing, dedicated solutions engineering, joint roadmap, joint customer references | Distribution at scale, defensibility against build-vs-buy decisions |

**11.5.5 The non-compete principle**

- We do not build features that overlap with our strategic partners' core surface (e.g., we don't add Vanta-style general SOC 2 automation)
- They do not build features that overlap with our runtime/SDK layer (negotiated as part of strategic tier)
- Both sides commit to integration depth instead of feature parity

### 11.6 Scalability
- Support 1M agent actions/day per tenant in V1; 10M in V1.5
- Support 1,000 tenants in V1; 10,000 by V2
- Support 500 active OAuth integrations in V1.5; 5,000 by V2

---

## 12. Data Model (Core Objects)

*(v0.1 objects preserved — Agent, Grant, VerifyEvent, Model, Prompt, Vendor, Guardrail, ChangeRequest, EvalRun, Approval, Anomaly, Questionnaire. See PRD_v0.1.md Section 12 for full definitions.)*

### New objects in v0.2:

```
PublicApiKey
├── id, tenant_id, name, key_hash, key_prefix (tai_pub_xxxxxx)
├── scopes[], ip_allowlist[], expires_at
├── created_by, created_at, last_used_at
└── revoked_at, revoke_reason

OAuthClient
├── id, name, owner_email, client_id, client_secret_hash
├── allowed_redirect_uris[], allowed_scopes[]
├── homepage_url, privacy_policy_url, logo_url
├── tier (open|listed|certified|strategic)
├── verified_at, verification_method
└── created_at, last_used_at

OAuthGrant
├── id, oauth_client_id, tenant_id, user_id_consenting
├── granted_scopes[], access_token_jti, refresh_token_jti
├── access_token_expires_at, refresh_token_expires_at
├── consented_at, revoked_at, revoke_reason
└── relationships: AuditEvents[] (every use logged)

WebhookSubscription
├── id, tenant_id, target_url, signing_secret_hash
├── event_filters[], framework_filters[], agent_filters[]
├── active, last_delivery_at, last_failure_at
├── consecutive_failures, retry_policy
└── created_via (dashboard|api|oauth_client_id)

WebhookDelivery
├── id, subscription_id, event_id, payload_hash
├── target_url, response_code, response_body_truncated
├── attempted_at, succeeded, attempt_number
└── next_retry_at

McpSession
├── id, tenant_id, oauth_grant_id, calling_agent_id?
├── tool_calls_count, started_at, last_call_at
└── disconnect_at
```

---

## 13. Technical Architecture

### Stack
- Backend: TypeScript on Node 22 (Fastify)
- DB: Postgres (Neon) for transactional + ClickHouse for audit events
- Object storage: S3 (evidence packs, signed)
- KMS: AWS KMS for evidence signing keys + OAuth token signing
- Queue: SQS for async ingestion + webhook delivery
- Dashboard: Next.js + Clerk
- SDKs: TypeScript (primary), Python (auto-generated + hand-tuning)
- **OAuth provider**: build on `ory/hydra` or implement directly (decide week 4)
- **MCP server**: TypeScript implementation of MCP spec
- Hosting: Fly.io or Railway initially; AWS by scale

### Key architectural decisions (v0.2 additions in bold)
1. Audit events live in ClickHouse, not Postgres
2. Hash chain computed at write time with batch Merkle root snapshots every 1000 events
3. Evidence Pack generation is async, notified via webhook on completion
4. SDK uses signed JWTs for capability tokens
5. Multi-tenancy via row-level Postgres + tenant-prefixed ClickHouse tables
6. Per-tenant region pinning at signup
7. **Auth middleware enforces "write only with SDK creds" rule structurally — every route declares which credential type it accepts; external API keys cannot satisfy SDK-credential routes**
8. **Public API + SDK API run on separate hostnames** (`api.trustai.io` for SDK, `public.trustai.io` for external consumers) to enforce separation at infrastructure layer
9. **OAuth token signing uses separate KMS key from SDK capability token signing** (key isolation prevents accidental cross-pollination)
10. **Webhook delivery is a separate service** with its own queue, retry, and observability; failures don't block the main API

---

## 14. UX Flows

### Flow 1: First-time install → first evidence event (target: < 10 min) — unchanged from v0.1

### Flow 2: Questionnaire auto-fill → exported PDF (target: < 30 min) — unchanged from v0.1

### Flow 3: Auditor invitation → Evidence Pack pickup (target: < 5 min for auditor) — unchanged from v0.1

### Flow 4: Customer connects TrustAI to Vanta (NEW — V1.5, target: < 5 min)
1. Customer in Vanta dashboard sees "AI Agent Coverage" panel → "Connect TrustAI"
2. Redirected to TrustAI consent screen showing requested scopes
3. Customer clicks "Authorize"
4. Returned to Vanta; AI evidence now appears in Vanta's audit log
5. Confirmation event logged in TrustAI audit trail

### Flow 5: GRC integrator registers an OAuth client (NEW — V1.5, target: < 15 min)
1. Integrator visits trustai.io/developers
2. Signs up for developer account
3. Creates OAuth client: name, redirect URIs, requested scopes, branding
4. Gets client ID + secret; immediately usable in "open" tier
5. Optional: applies for "Listed" tier (manual review, ~1 week)

### Flow 6: Auditor uses MCP server via Claude Desktop (NEW — V1.5)
1. Auditor configures Claude Desktop with TrustAI MCP server URL
2. Authenticates via OAuth (one-time)
3. In Claude: *"Show me all SOC 2 CC6 evidence for Acme Corp for Q3 2026"*
4. Claude calls TrustAI MCP tools; returns evidence with citations
5. Auditor follows up: *"Were there any approval timeouts?"* → Claude queries more
6. Auditor exports findings without ever logging into TrustAI dashboard

---

## 15. Pricing & Packaging

### Direct Customer Tiers (V1)

| Tier | Price | Includes |
|---|---|---|
| **Free** | $0 | SDK install, 30 days evidence retention, default trust page, 1 questionnaire/mo, 100K events/mo |
| **Starter** | $149/mo (or $1,490/yr) | Custom-branded trust page, 1yr retention, SOC 2 questionnaire engine, unlimited questionnaires, 1M events/mo, Slack alerts, **basic public API access** |
| **Growth** | $599/mo (or $5,990/yr) | + EU AI Act, custom domain, 3yr retention, 3 auditor portal seats, 10M events/mo, **OAuth integrations, webhooks, MCP server access** |
| **Scale** | $2,500/mo (or $25K/yr) | + multi-framework (HIPAA, FINRA), 7yr retention, white-glove evidence prep, dedicated CSM, custom controls, EU/US residency choice, unlimited events, **strategic-tier integration support** |

### Integration Partner Tiers (V1.5 — NEW)

| Tier | Cost to integrator | What they get |
|---|---|---|
| **Open** | Free | Public API + OSS connectors + community Discord |
| **Listed** | Free | "Listed in TrustAI Integrations" + co-marketing post + 1 founder call/quarter |
| **Certified** | $1K/mo | "TrustAI Certified" badge, priority API support, joint logo placement, monthly roadmap call |
| **Strategic** | Negotiated (likely revenue-share or per-event) | Co-marketing campaigns, joint customer references, joint roadmap planning, dedicated SE, paid co-development |

Pricing principles:
- Direct customer pays for direct usage
- Integration partners pay for partnership-grade support and co-marketing, not for API access itself (this keeps the ecosystem open)
- Strategic tier pricing tied to either revenue share or per-event pricing depending on volume

---

## 16. Launch Plan

### Phase 1: V1 (Weeks 1-8) — the direct product wedge

| Week | Engineering | GTM |
|---|---|---|
| 1 | Spec lock; auth middleware architecture decision | 10 design partner calls; collect 30+ questionnaires |
| 2-3 | SDK + Agent/Grant/Verify | Build knowledge base; recruit 5 design partners |
| 4 | Audit log + hash chain + registries | Lock fintech-specific GTM messaging |
| 5 | Approval flow + redaction + anomaly | Launch landing page; build waitlist |
| 6 | Questionnaire engine + Evidence Pack | Onboard design partners; gather testimonials |
| 7 | Trust page + Stripe billing | Draft launch content (HN, PH, blog series) |
| 8 | Polish, docs, dogfood our own SOC 2 | Show HN + Product Hunt + outbound to 100 YC AI fintechs |

### Phase 1.5: V1.5 (Weeks 12-20) — the ecosystem expansion (NEW)

| Week | Engineering | GTM |
|---|---|---|
| 12-13 | Public API keys + OAuth 2.1 server | Outbound to Vanta/Drata/SafeBase product leads |
| 14 | Webhook subscription + delivery service | Publish "Agent Compliance Event v1" spec on GitHub |
| 15-16 | MCP server for compliance | Recruit 3 OSS connector partners (Vanta, Drata, SafeBase) |
| 17 | Vanta + Drata + SafeBase reference connectors | Sign 1 strategic-tier MoU |
| 18 | Developer portal (trustai.io/developers) | Show HN: "We open-sourced the agent compliance schema" |
| 19 | Documentation + integration guides | Co-marketing post with first strategic partner |
| 20 | V1.5 launch | Submit spec to AICPA AI Assurance Task Force |

### Phase 2: V2 (Months 6-12) — multi-framework + standards

- Add HIPAA, FINRA, ISO 42001 control libraries
- Decision reconstruction API, GDPR DSR workflow
- WORM storage mode, EU data residency
- Engage NIST AI Safety Institute about evidence schema
- Recruit 5+ certified integrations
- Healthtech vertical V1 readiness assessment

---

## 17. Risks & Mitigations

| Risk | Severity | Mitigation |
|---|---|---|
| Customers cancel after closing one deal | High | Vertical ICP (fintech), annual contracts, retention features, always-on trust page |
| Big 4 partnership doesn't materialize in 12 months | High | Plan B: 2-3 mid-tier firms; Plan C: direct sell with auditor portal |
| Vanta or SafeBase enters with AI module | Medium | **V1.5 partnership strategy reduces this risk significantly**: convert competitor to integrator |
| Anthropic/OpenAI ship native compliance evidence | Medium | Position as cross-provider neutral; MCP server gives us a native hook into their ecosystem |
| Auditors reject our evidence format | High | Co-design with 1-2 auditors before V1; align with AICPA TSC IDs strictly; submit spec to standards body |
| SDK adoption friction kills install funnel | High | Obsessive DX investment; office hours; public Discord; live install demos |
| Compliance hire impossible to find | Medium | Fractional advisor in Month 1; full-time in Month 6-9 |
| EU AI Act enforcement timeline slips | Low | SOC 2 + procurement reviews carry the demand |
| **(NEW) Commoditization via open API** | Medium | Open only reads; runtime layer + corpus + control authoring stay closed; charge integration partners for premium support |
| **(NEW) Customer relationship captured by partner (invisible plumbing)** | Medium | Always retain SDK install + branded trust page; sell direct AND via partners; ensure consent UI is TrustAI-branded |
| **(NEW) Open spec gets forked or ignored** | Low | If forked, we've already won category visibility; if ignored, we still control the dominant implementation |
| **(NEW) Webhook delivery failures damage partner trust** | Medium | Separate service with SLA, retries, replay, observability; transparent delivery log for partners |
| **(NEW) OAuth consent flow has security incident** | Critical | Standard OAuth 2.1 + PKCE; HSM-backed token signing; external pen test before V1.5 launch |
| **(NEW) Strategic partner builds against us anyway** | Medium | Non-compete principle in strategic-tier agreement; M&A optionality at favorable terms; speed |

---

## 18. Open Questions

### V1 questions (carried from v0.1)
1. Brand name — TrustAI is placeholder
2. Open-source strategy details — SDK MIT-licensed? Control library publication terms?
3. Free tier event volume validation
4. First non-fintech expansion vertical (healthtech vs HR-tech)
5. Native MCP gateway in V2?
6. Bedrock and Vertex SDK timing
7. Auditor invitation pricing
8. Co-marketing rights with Big 4

### V1.5 ecosystem questions (NEW)
9. Which 3 GRC tools first? Recommendation: **Vanta** (largest distribution), **Hyperproof** (mid-market, less defensive), **Drata** (parity with Vanta)
10. Do we charge for premium API support (rate limits, dedicated infra)? Recommendation: yes at Certified tier
11. OAuth: build directly or use `ory/hydra`? Recommendation: hydra to ship faster, replace later if needed
12. MCP server: ship at V1.5 or V2? Recommendation: V1.5 — small build, huge positioning win
13. Schema spec licensing: MIT vs CC0 vs Apache 2.0? Recommendation: Apache 2.0 (patent grant matters)
14. Standards body engagement strategy: AICPA first or NIST first? Recommendation: AICPA — closer to SOC 2 reality
15. Should we white-label the SDK for strategic partners (e.g., "Vanta Agent Evidence" SDK is actually TrustAI under the hood)? Recommendation: no in V1.5, revisit in V2
16. Non-compete clauses with strategic partners: how do we enforce? Recommendation: contractual + transparency + roadmap-sharing
17. Partner co-development pricing model — revenue share vs flat fee vs per-event?

---

## 19. Out of Scope (V1 + V1.5)

- Multi-framework beyond SOC 2 + EU AI Act
- Customer-authored control extensions
- AI bias / fairness testing
- Native chatbot / Copilot integration
- On-prem / VPC / self-hosted
- White-label embedded version
- Multi-language SDK beyond Python + TypeScript
- Anomaly detection ML models (rules-based only)
- Generic SOC 2 automation (Vanta does this)
- Real-time WebSocket budget streaming
- Mobile dashboard
- **(V1.5 exclusions)** Write endpoints exposed to external API keys — non-negotiable
- **(V1.5 exclusions)** Direct corpus access for external tools — proprietary
- **(V1.5 exclusions)** White-labeled OAuth consent (must show TrustAI brand for trust)

---

## 20. Appendix A: Control Library Schema (sample)

*(Identical to v0.1 — see PRD_v0.1.md Section 20 for the sample 10 controls. No changes in v0.2; full 54-control library still planned.)*

---

## 21. Appendix B: Open Spec Schema — "Agent Compliance Event v1" (NEW)

Initial draft of the spec to be published on `github.com/trustai/spec`:

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://trustai.io/specs/agent-compliance-event/v1.json",
  "title": "Agent Compliance Event",
  "type": "object",
  "required": ["spec_version", "event_id", "event_type", "timestamp", "agent", "tenant_id"],
  "properties": {
    "spec_version": {
      "const": "agent-compliance-event/v1.0.0"
    },
    "event_id": {
      "type": "string",
      "description": "Unique event identifier (ULID recommended)"
    },
    "event_type": {
      "type": "string",
      "enum": [
        "agent.action.allowed",
        "agent.action.denied",
        "agent.grant.created",
        "agent.grant.revoked",
        "agent.approval.requested",
        "agent.approval.decided",
        "agent.anomaly.detected",
        "agent.credential.rotated",
        "agent.decommissioned",
        "model.changed",
        "prompt.changed",
        "vendor.changed",
        "guardrail.triggered"
      ]
    },
    "timestamp": {
      "type": "string",
      "format": "date-time"
    },
    "tenant_id": {
      "type": "string",
      "description": "Opaque tenant identifier"
    },
    "agent": {
      "type": "object",
      "required": ["id"],
      "properties": {
        "id": { "type": "string" },
        "did": { "type": "string" },
        "owner_user_id": { "type": "string" },
        "environment": { "enum": ["prod", "staging", "dev"] }
      }
    },
    "delegated_by": {
      "type": "object",
      "properties": {
        "user_id": { "type": "string" },
        "user_proof_type": {
          "enum": ["oidc_id_token", "hosted_consent", "signed_challenge"]
        }
      }
    },
    "action": {
      "type": "object",
      "properties": {
        "tool": { "type": "string" },
        "operation": { "type": "string" },
        "resource_id": { "type": "string" },
        "estimated_cost_usd": { "type": "number" }
      }
    },
    "compliance": {
      "type": "object",
      "properties": {
        "controls_evidenced": {
          "type": "array",
          "items": { "type": "string" },
          "description": "Control IDs this event satisfies (e.g., SOC2.CC6.OBO_PRESERVATION)"
        },
        "frameworks": {
          "type": "array",
          "items": { "type": "string" }
        },
        "data_categories": {
          "type": "array",
          "items": { "type": "string" }
        }
      }
    },
    "model": {
      "type": "object",
      "properties": {
        "id": { "type": "string" },
        "provider": { "type": "string" },
        "name": { "type": "string" },
        "version": { "type": "string" }
      }
    },
    "audit_chain": {
      "type": "object",
      "properties": {
        "previous_hash": { "type": "string" },
        "this_hash": { "type": "string" },
        "merkle_root_id": { "type": "string" },
        "signature": { "type": "string" }
      }
    },
    "_links": {
      "type": "object",
      "properties": {
        "self": { "type": "string", "format": "uri" },
        "decision_reconstruction": { "type": "string", "format": "uri" }
      }
    }
  }
}
```

This spec is the foundation for the AICPA / NIST submission and the canonical format for all OSS connectors.

---

## 22. Appendix C: Strategic Partner Outreach Plan (NEW)

### Vanta (priority 1)

- **Why first**: largest distribution (~10K customers), most existential threat if they build against us, biggest co-marketing payoff if partnered
- **Pitch angle**: "Your customers are getting hammered with AI security questionnaires you can't answer. We handle the runtime agent layer; you keep the customer relationship for general SOC 2."
- **Target contact**: VP Product (LinkedIn outreach + warm intro via YC network)
- **Timing**: outbound starts Week 9 (post-V1 launch when we have proof points)
- **Win condition**: signed LOI by Month 6 for strategic-tier integration

### Hyperproof (priority 2)

- **Why second**: mid-market, less competitive with Vanta, faster decision-making
- **Pitch angle**: same as Vanta but with "we make you the AI-ready alternative to Vanta"
- **Target contact**: Head of Partnerships (typically open to inbound)
- **Timing**: Week 11
- **Win condition**: shipped certified integration by Month 4

### Drata (priority 3)

- **Why**: parity with Vanta, can't let Vanta exclusivity define the category
- **Pitch angle**: similar to Vanta
- **Timing**: Week 13
- **Win condition**: at minimum, listed-tier integration by Month 5

### SafeBase (priority 4)

- **Why**: trust center category — direct overlap, integration is mutually defensive
- **Pitch angle**: "Your static trust pages need a runtime evidence backbone. We're it."
- **Timing**: Week 15
- **Win condition**: bidirectional integration (we read their trust page schema, they read our events)

---

## 23. Approval

| Stakeholder | Role | Status |
|---|---|---|
| Founder/CEO | Final decision | Pending |
| Founding Engineer | Technical feasibility (V1 + V1.5 architecture) | Pending |
| Compliance Advisor (TBD) | Control library validation | Pending hire |
| Design Partner 1 (TBD) | ICP validation | Pending |
| Design Partner 2 (TBD) | ICP validation | Pending |
| **Strategic Partner Contact (TBD)** | V1.5 partnership feasibility | Pending outreach |

---

*End of PRD v0.2. Next review: after first 10 design-partner calls (target: 2 weeks) AND after first Vanta/Drata/SafeBase exploratory call (target: 4 weeks).*
