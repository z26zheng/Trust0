# Product Requirements Document

| Field | Value |
|---|---|
| **Product Name** | TrustAI *(working name — finalize)* |
| **Document Version** | 0.1 (draft for design partner review) |
| **Owner** | Founding team |
| **Status** | Draft — pre-engineering |
| **Last Updated** | May 28, 2026 |
| **Target GA** | August 2026 (V1) |

---

## 1. Executive Summary

TrustAI is the **trust-and-compliance evidence layer for fintech AI companies**. A drop-in SDK records every AI agent action with full identity, provenance, and policy context; the platform automatically produces auditor-grade SOC 2 evidence, fills enterprise AI security questionnaires from runtime data, and publishes a live trust center that unblocks enterprise sales.

V1 targets fintech AI startups in active enterprise sales cycles — companies losing $50K-$500K deals to security reviews they can't pass. The wedge is one demo: *paste your enterprise buyer's AI security questionnaire, get auditor-grade answers and a branded trust page in 10 minutes*. The expansion is a multi-framework compliance evidence platform mapped to runtime agent behavior — a category no incumbent (Vanta, Arcade, SafeBase, Composio, Natoma) currently serves.

---

## 2. Problem Statement

### The User Problem

Fintech AI startups face a binding constraint: every enterprise sales cycle now includes an **AI-specific security review** with 50-200 questions auditors and procurement teams demand answers to. Today, founders:

- Spend 2-6 weeks per deal hand-writing answers
- Submit incomplete responses that stall negotiations
- Engage $20K+ consultants to draft policies they don't have
- Lose deals (or close at discount) because their controls evidence is weak
- Repeat the entire cycle for every new customer's annual vendor review

### The Market Problem

In May 2026, no product combines all four of:
1. **Runtime evidence collection** (actual agent activity, not policy claims)
2. **AI-specific control mapping** (SOC 2, EU AI Act, ISO 42001 interpreted for agents)
3. **Developer-installable** (5-minute SDK, not enterprise procurement)
4. **Founder-priced** ($99-$2,500/month, not $50K+ ACVs)

Vanta and Drata sell generic SOC 2 automation with no agent data. SafeBase (HubSpot) sells generic trust centers. Arcade and Composio sell agent OAuth with no compliance layer. Natoma sells enterprise MCP gateways top-down. Delve is an AI-native audit *firm*, not a product. The space between these players is wide open and growing as the EU AI Act enforcement clock ticks (Aug 2026 GPAI, Aug 2027 high-risk).

### Why Now

- **EU AI Act enforcement starts August 2026** — fintech AI vendors selling into EU need conformity evidence within 90 days
- **SOC 2 auditors have hardened AI expectations in 2026** — point-in-time policy attestations no longer pass; runtime evidence is required
- **Enterprise procurement has institutionalized AI security questionnaires** — every Fortune 500 has a standard 100-question intake
- **The agent stack standardized in 2025-2026 around MCP + OAuth 2.1** — making runtime instrumentation tractable for the first time

---

## 3. Goals & Non-Goals

### V1 Goals

1. Ship a Python + TypeScript SDK that captures runtime agent activity with one-line integration
2. Ship a SOC 2 control library mapped to the 54 questions auditors actually ask in 2026
3. Ship the questionnaire auto-fill engine as the primary acquisition demo
4. Ship a live, branded trust center as the primary retention artifact
5. Ship a one-click SOC 2 Evidence Pack export for auditor handoff
6. Capture 50 paying fintech customers in 90 days post-launch
7. Lock 1 Big 4 audit firm "preferred format" relationship within 12 months

### V1 Non-Goals

- Multi-framework support beyond SOC 2 + EU AI Act (HIPAA, FINRA, ISO 42001 deferred to V1.1)
- Customer-authored controls (we provide the library; they don't extend it)
- On-prem / VPC deployment
- Multi-tenant white-label
- AI safety / bias testing (out of scope — different product)
- Generic SOC 2 automation (Vanta-style policies/training/scans) — we are agent-runtime-specific
- Selling to enterprise CISOs (V1 buyer is founder/CEO)

---

## 4. Target Customer (ICP)

### Primary V1 ICP

**Fintech AI startup, Series Seed to Series B (5-150 employees), with at least one enterprise customer in active sales cycle or signed within the last 12 months.**

Signals:
- Building agents that touch financial data (banking, payments, accounting, compliance, lending)
- Selling to banks, credit unions, fintechs, or enterprise finance teams
- Has been asked to complete at least one vendor security questionnaire in the last 6 months
- No dedicated CISO yet, no Vanta or has Vanta but it doesn't cover agents

### V1 ICP Exclusions

- Pre-revenue startups with no enterprise sales motion (will not convert)
- Pure consumer AI products with no enterprise buyers (wrong buyer)
- Enterprise companies (>1,000 employees) with existing GRC programs (wrong sales motion)
- Non-fintech verticals in V1 (refused for vertical concentration discipline)

### Key Buyer Persona: "The Founding Sales Engineer"

- Title: CTO / Head of Eng / Founding SE / CEO at sub-50-person fintech AI startup
- Pain: Has 3-5 enterprise deals stuck in security review; spends 10+ hours/week on questionnaires
- Budget authority: Can swipe a credit card up to $500/month without approval
- Procurement path: Self-serve signup, no sales calls required, monthly billing acceptable
- Trigger event: Specific enterprise buyer sends a multi-page AI security questionnaire

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

### Year 1 Strategic Metrics

| Metric | Target |
|---|---|
| Paying customers | 150 |
| ARR | $300K |
| Big 4 partnership (signed MoU or written endorsement) | 1 |
| Fintech AI questionnaires in corpus | 200 |
| SOC 2 audits passed using our evidence | 20+ |
| Logo churn (annualized) | < 15% |

### Anti-Metrics (Things to Refuse to Optimize)

- Total signups across all verticals (we'd rather have 100 fintech than 1000 mixed)
- Free tier conversion rate (we'd rather have fewer high-intent paying customers)
- Feature breadth (we'd rather ship 5 features well than 20 poorly)

---

## 6. Competitive Positioning

| Player | What they do | Why TrustAI wins |
|---|---|---|
| **Vanta / Drata** | Generic SOC 2 automation | We have runtime agent data; they don't |
| **SafeBase (HubSpot)** | Generic trust centers | AI-specific sections, runtime evidence backing |
| **Arcade / Composio** | Agent OAuth + tool catalog | Compliance positioning, founder buyer |
| **Delve** | AI-native SOC 2 audit firm | Product not service; always-on |
| **Natoma** | Enterprise MCP gateway | SMB pricing, dev-first install, founder buyer |
| **Microsoft Entra Agent ID** | Free agent identity on MS stack | Multi-cloud, agnostic, fintech-vertical |

---

## 7. User Stories

### Acquisition Stories
- **As a fintech AI founder**, I want to paste my buyer's 100-question AI security questionnaire and receive 70+ auto-filled answers in 10 minutes, so I can stop losing deals to slow procurement.
- **As a fintech AI founder**, I want a branded public trust page that buyers can self-serve before our first call, so they enter sales pre-qualified on security.
- **As a head of engineering at an AI startup**, I want to install an SDK in <30 minutes and immediately see runtime evidence captured, so I can validate the product before committing budget.

### Operational Stories
- **As an engineering lead**, I want to register the models, prompts, and providers we use *once*, so my team doesn't think about compliance in every code change.
- **As an engineer**, I want my agent's tool calls to be approved by a human when they exceed risk thresholds, so I can claim "human oversight" controls truthfully.
- **As a CTO**, I want my SDK to detect runaway agent loops and stop them before they hit budget thresholds, so I avoid bill-shock incidents that auditors flag.

### Audit / Sales-Cycle Stories
- **As a founder facing SOC 2 audit**, I want a one-click Evidence Pack mapped to control IDs my auditor recognizes, so I save 3 weeks of evidence collection.
- **As a founder responding to enterprise procurement**, I want to invite my buyer's auditor to view evidence directly, so I bypass repeated email exchanges.
- **As a founder hit with a GDPR DSAR**, I want to query every agent decision that touched a specific data subject and produce a deletion proof, so I respond within the 30-day legal window.

---

## 8. Product Overview

TrustAI consists of **four user-facing surfaces** sharing one backend:

```
┌─────────────────────────────────────────────────────────────┐
│  SURFACES                                                    │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   SDK        │  │  Dashboard   │  │  Trust Page  │      │
│  │  (Python+TS) │  │  (admin UI)  │  │  (public)    │      │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘      │
│         │                  │                  │              │
│  ┌──────▼──────────────────▼──────────────────▼──────────┐  │
│  │  TRUSTAI API + EVIDENCE PIPELINE                       │  │
│  │  (events, controls, evidence, registries)              │  │
│  └────────────────────────────────────────────────────────┘  │
│         │                                                     │
│  ┌──────▼──────┐                                             │
│  │ Auditor     │  ← read-only access for customer's auditor │
│  │ Portal      │                                             │
│  └─────────────┘                                             │
└─────────────────────────────────────────────────────────────┘
```

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

### 9.2 Core API

**Existing-style endpoints** (carried forward):
- `POST /v1/agents` — register agent
- `POST /v1/grants` — create OBO delegation grant
- `POST /v1/grants/{id}/verify` — runtime check + evidence emission
- `POST /v1/grants/{id}/revoke` — revoke grant
- `POST /v1/approvals` + `POST /v1/approvals/{id}/decide` — human oversight
- `GET /v1/audit/events` — query audit log

**New registry endpoints** (driven by SOC 2 CC8 + CC9):
- `POST /v1/models` — Model Registry (provider, version, eval, approver, rollback)
- `POST /v1/prompts` — Prompt Registry (versioned, content-hashed)
- `POST /v1/vendors` — Vendor Registry (providers, contracts, BAA/DPA metadata)
- `POST /v1/guardrails` — Guardrail Registry (declarative rules)
- `POST /v1/eval-runs` — Eval Gate records
- `POST /v1/changes` + approve/deploy/rollback — Change Request workflow
- `POST /v1/redaction-policies` — Declarative redaction rules

**New compliance endpoints**:
- `GET /v1/controls` — Control library (read)
- `GET /v1/questions` — Auditor question knowledge base (read)
- `POST /v1/questionnaires` — Submit a questionnaire for auto-fill
- `GET /v1/questionnaires/{id}` — Retrieve answered questionnaire
- `GET /v1/evidence/export?framework=SOC2&period=...` — Generate Evidence Pack
- `GET /v1/decisions/{id}` — Reconstruct full decision context
- `POST /v1/data-subjects/{id}/request` — DSAR handling
- `POST /v1/incidents` — Log incidents + IR tests

**New admin endpoints**:
- `POST /v1/agents/{id}/decommission`
- `POST /v1/credentials/rotate`
- `POST /v1/anomalies`
- `POST /v1/acknowledgments` (policy/AUP)

### 9.3 Registries (the SOC 2 CC8 backbone)

**FR-REG-1: Model Registry**. Every model used must be registered with provider, version, evaluation metrics, approver, deployment timestamp, rollback target. SDK auto-resolves model name in API calls to a registered ID; calls referencing unregistered models log a warning and require dashboard registration before evidence is auditor-grade.

**FR-REG-2: Prompt Registry**. Prompts stored with content hash, version, parent_version (DAG), approver. SDK helper `client.prompts.get("name")` returns the current version. Prompt changes go through Change Request flow.

**FR-REG-3: Vendor Registry**. Model providers, vector DBs, MCP servers, tools registered with contract metadata (DPA, BAA, MSA), allowed data categories, subprocessor lists. Every call's vendor IDs auto-attach to evidence.

**FR-REG-4: Guardrail Registry**. Guardrails (regex, classifier, scope rule) declared centrally; SDK references by name. Guardrail block events captured automatically.

### 9.4 Questionnaire Engine (the acquisition magnet)

**FR-Q-1**: Accept questionnaire upload in formats: SIG, CAIQ, Word, PDF, plain text, custom CSV.

**FR-Q-2**: Parse each question, classify against the knowledge base (200+ canonical AI security questions), and propose 1-3 candidate matches with confidence scores.

**FR-Q-3**: Auto-fill answers by querying the customer's evidence pipeline. Each answer cites evidence event IDs.

**FR-Q-4**: Flag gaps where insufficient evidence exists, with a 30-minute "fix plan" linking to specific product features that close the gap.

**FR-Q-5**: Allow human edit before export. Edits feed back to the canonical knowledge base (anonymized) to improve future auto-fills.

**FR-Q-6**: Export filled questionnaire as branded PDF, DOCX, or original format.

**FR-Q-7**: Maintain a customer-specific question library so repeated requests from different buyers reuse polished answers.

### 9.5 Trust Page

**FR-TP-1**: Auto-generated public URL: `trust.{customername}.com` (custom domain) or `{customername}.trustpage.ai` (default).

**FR-TP-2**: Sections: AI Agent Inventory, Models in Use, Data Flows, Frameworks Claimed, Live Activity Stats, Incident Log, Approval Stats, Certifications, Change Log, Subprocessors.

**FR-TP-3**: Updates live from runtime evidence (no manual refresh).

**FR-TP-4**: Permanent persistent "Secured by TrustAI" badge with audit-link verification (brand network effect).

**FR-TP-5**: Allow gated sections (NDA-required, log-in required) for sensitive evidence.

**FR-TP-6**: Embeddable badge for customer's own marketing site.

### 9.6 SOC 2 Evidence Pack Export

**FR-EP-1**: Generate a zip containing: control-by-control evidence files, hash-chain proof, auditor cover sheet, event ID indexes, manifest CSV.

**FR-EP-2**: Support period filters (Q1, Q2, custom date range, point-in-time).

**FR-EP-3**: Map evidence to control IDs in the format the customer's auditor specifies (default: AICPA TSC IDs; configurable for Big 4 firm preferences).

**FR-EP-4**: Include cryptographic proof of completeness (Merkle root, signed by TrustAI KMS).

**FR-EP-5**: Auditor Portal access — invite the customer's auditor by email; they get a read-only seat with their own dashboards and saved queries.

### 9.7 Approval Flow

**FR-APR-1**: Configurable triggers: scope pattern, cost threshold, data category, agent risk class.

**FR-APR-2**: Notification channels: Slack, email, webhook, hosted UI link.

**FR-APR-3**: Approver responds via single-click hosted UI; SDK blocks the agent until decision or timeout.

**FR-APR-4**: Every approval recorded with reviewer identity, timestamp, reason, decision.

**FR-APR-5**: Timeout behavior configurable (auto-approve, auto-deny, escalate).

### 9.8 Dashboard

**FR-DSH-1**: Sections: Activity Feed, Agents, Grants, Models/Prompts/Vendors/Guardrails, Audit Log, Approvals Queue, Anomalies, Trust Page Settings, Evidence Exports, Questionnaires, Frameworks, Team, Billing.

**FR-DSH-2**: Filter audit log by every dimension (agent, user, task, model, vendor, framework, control, date range, decision outcome).

**FR-DSH-3**: Real-time anomaly feed with Slack/PagerDuty integration.

**FR-DSH-4**: Use Clerk for dashboard auth; SAML/SSO deferred to V1.1.

---

## 10. SOC 2 Compliance Mapping

Every functional requirement above traces to a specific auditor question. This table is partial — the full mapping ships as the Control Library product.

| Auditor Question (from 54) | TSC | Mapped Feature | Evidence Source |
|---|---|---|---|
| Q2: AI agent inventory | CC1 | Agent registry | `GET /v1/agents` |
| Q3: Risk classification per agent | CC1 | `agent.risk_classification` field | Agent record |
| Q4: AUP acknowledgment | CC1 | Policy Acknowledgment endpoint | `POST /v1/acknowledgments` |
| Q9: Unique agent identity | CC6 | DID + Agent ID, no shared accounts | Agent record |
| Q11: Least-privilege scope | CC6 | `agent.max_scopes` + grant scoping | Grant record |
| Q12: OBO preservation | CC6 | `user_proof` + JWT `sub`/`act` claims | Grant + token JWT |
| Q14: Credential rotation | CC6 | Rotation event log | `POST /v1/credentials/rotate` |
| Q17: Agent decommissioning | CC6 | Decommission workflow | `POST /v1/agents/{id}/decommission` |
| Q19: Action logging | CC7 | Every verify call → audit event | `GET /v1/audit/events` |
| Q20: Immutable logs | CC7 | Hash chain + signed timestamps | Audit event signature |
| Q22: Anomaly detection | CC7 | Loop detection + drift events | Anomaly endpoint |
| Q25: Input/output redaction | CC7 | Redaction Policy applied in SDK | `POST /v1/redaction-policies` |
| Q26: Decision reconstruction | CC7 | Full decision replay | `GET /v1/decisions/{id}` |
| Q28: Model change mgmt | CC8 | Change Request flow | `POST /v1/changes` |
| Q29: Model registry | CC8 | Model Registry | `POST /v1/models` |
| Q30: Tested rollback | CC8 | `model.rollback_tested_at` | Model record |
| Q32: Prompt version control | CC8 | Prompt Registry | `POST /v1/prompts` |
| Q34: AI risk assessment | CC9 | Annual assessment workflow | `POST /v1/risk-assessments` |
| Q35: Vendor risk assessment | CC9 | Vendor Registry + scoring | Vendor record |
| Q36: BAA/DPA coverage | CC9 | Contract metadata on vendor | `vendor.contracts[]` |
| Q49: Guardrail outcomes | New | Guardrail Registry + events | Guardrail event log |
| Q51: Human oversight | New | Approval flow records | `POST /v1/approvals` |
| Q53: Prompt injection defense | New | Injection event log + guardrails | Anomaly event |
| Q54: "No human request" gap | New | `originating_human_request` required field | Verify event |

(Full mapping for all 54 questions ships in the Control Library product — `GET /v1/controls`.)

---

## 11. Non-Functional Requirements

### Performance
- SDK hot-path overhead: ≤ 5ms p99 added to LLM call latency
- API verify endpoint: ≤ 50ms p99 (rarely hit; SDK is local-first)
- Evidence Pack export: ≤ 60 seconds for 1 year of evidence
- Trust page load: ≤ 1.5s p95

### Reliability
- 99.9% API uptime SLA (paid tiers)
- Multi-region read replicas (US + EU) by V1.1
- Graceful SDK degradation on backend outage (local cache + safety multiplier)

### Security (our own product must be exemplary)
- SOC 2 Type II within 6 months of GA (using our own product — dogfood proof point)
- All evidence storage encrypted at rest with AWS KMS / GCP CMEK
- Hash-chained audit log with WORM storage tier for paid customers
- Per-tenant data residency (US or EU) selectable at signup
- All employee access to customer evidence MFA-required, audited
- Public bug bounty within 90 days of GA

### Compliance (frameworks we ourselves attest to)
- SOC 2 Type II (target Q1 2027)
- ISO 27001 (target Q2 2027)
- GDPR-compliant (day 1 — required to serve EU fintechs)

### Scalability
- Support 1M agent actions/day per tenant in V1
- Support 1,000 tenants in V1; 10,000 by V2

---

## 12. Data Model (Core Objects)

```
Agent
├── id, did, name, owner_user_id, environment, risk_classification
├── compliance { frameworks[], purpose, data_categories_allowed, owner_legal_entity, data_residency }
└── relationships: Grants[], Decommission?

Grant
├── id, agent_id, user_id, user_proof, scopes[], expires_at
├── budget, rate_limit, compliance_context
└── relationships: VerifyEvents[], Approvals[], Revocation?

VerifyEvent  (the central evidence atom)
├── id, decision_id, grant_id, action, allowed, reason
├── model_id, prompt_id, vendor_ids[], guardrail_ids[], redaction_policy_id
├── input_hash, output_hash, cost_usd, tokens_in, tokens_out
├── audit_chain { prev_hash, this_hash, signature, position }
├── compliance_questions_evidenced[]  ← the reverse index
└── originating_human_request_id

Model
├── id, provider, name, version, training_data_snapshot
├── evaluation_metrics, approved_by, approved_at, deployment_change_id
└── rollback_target_id, rollback_tested_at

Prompt
├── id, name, version, content_hash, parent_version_id
├── approved_by, approved_at, deployment_change_id

Vendor
├── id, name, service_type, data_categories_allowed
├── contracts[] { type, signed_at, expires_at, url }
└── risk_assessment_date, subprocessors_url

Guardrail
├── id, name, type, rule_definition
└── deployment_change_id

ChangeRequest
├── id, type (model|prompt|guardrail|tool), payload
├── requested_by, approved_by, approved_at
├── deployed_at, rollback_target_id, eval_run_id

EvalRun
├── id, model_id_under_test, metrics, passed, evaluator
└── change_request_id

Approval
├── id, grant_id, decision_id, summary, approvers[]
├── decision, decided_by, decided_at, reason

Anomaly
├── id, type (loop|drift|injection|cost_spike), grant_id, severity
└── auto_remediation_taken

Questionnaire
├── id, customer_id, source_buyer, raw_text
├── questions[] { id, text, matched_canonical_id, answer, evidence_event_ids[], status }
└── exported_at, exported_format
```

---

## 13. Technical Architecture

**Stack (recommended for fast V1 ship)**
- Backend: TypeScript on Node 22 (Fastify) or Go (preference: TypeScript for shared types with SDK)
- DB: Postgres (Neon) + ClickHouse (audit events, high-volume)
- Object storage: S3 (evidence packs, signed)
- KMS: AWS KMS for evidence signing keys
- Queue: SQS for async ingestion
- Dashboard: Next.js + Clerk
- SDKs: TypeScript (primary), Python (auto-generated via openapi-generator + hand-tuning)
- Hosting: Fly.io or Railway initially; AWS by scale

**Key architectural decisions**
1. **Audit events live in ClickHouse**, not Postgres — volume mandates it from day 1
2. **Hash chain computed at write time** with batch Merkle root snapshots every 1000 events
3. **Evidence Pack generation is async** (queued) and notified via webhook on completion
4. **SDK uses signed JWTs** for capability tokens; backend signs with HSM-backed KMS keys
5. **Multi-tenancy via row-level Postgres + tenant-prefixed ClickHouse tables**
6. **Per-tenant region pinning** at signup; no cross-region data movement

---

## 14. UX Flows (Top 3)

### Flow 1: First-time install → first evidence event (target: < 10 min)
1. Sign up at trustai.com → choose plan (Starter $149/mo) → enter Stripe card
2. Onboarding wizard asks: company name, vertical (fintech), primary model provider, primary tool integrations
3. Wizard auto-creates Model + Vendor registry entries from declared providers
4. Wizard provides install snippet for primary language
5. Developer pastes 3 lines into agent code, runs once
6. Dashboard shows first event within 30 seconds with celebration confetti
7. Trust page auto-published at `{tenant}.trustpage.ai`

### Flow 2: Questionnaire auto-fill → exported PDF (target: < 30 min)
1. Customer uploads questionnaire (drag-drop or paste)
2. Parsing screen: shows extracted questions, customer confirms scope
3. Auto-fill runs; progress bar with per-question status
4. Review screen: customer sees each answer with evidence citations, can edit
5. Gaps surfaced inline with "Fix this" action links
6. Customer clicks "Export" → branded PDF/DOCX downloaded
7. Saved to customer library for re-use on next buyer

### Flow 3: Auditor invitation → Evidence Pack pickup (target: < 5 min for auditor)
1. Customer invites auditor by email from Dashboard
2. Auditor receives email → click → SSO into Auditor Portal
3. Auditor sees customer's controls dashboard, period selector, framework selector
4. Auditor clicks "Generate Evidence Pack" → zip + signed manifest
5. Auditor can re-query specific events directly without re-asking customer

---

## 15. Pricing & Packaging

| Tier | Price | Includes |
|---|---|---|
| **Free** | $0 | SDK install, 30 days evidence retention, default trust page, 1 questionnaire/mo, 100K events/mo |
| **Starter** | $149/mo (or $1,490/yr) | Custom-branded trust page, 1yr retention, SOC 2 questionnaire engine, unlimited questionnaires, 1M events/mo, Slack alerts |
| **Growth** | $599/mo (or $5,990/yr) | + EU AI Act, custom domain, 3yr retention, 3 auditor portal seats, 10M events/mo, approval flow unlimited |
| **Scale** | $2,500/mo (or $25K/yr) | + multi-framework (HIPAA, FINRA), 7yr retention, white-glove evidence prep, dedicated CSM, custom controls, EU/US residency choice, unlimited events |

Pricing principles:
- Annual contracts get 17% discount (incentivize stickiness)
- Event-volume tiers prevent abuse without taxing growth
- "Compliance" tier ($599+) unlocks the high-value sales features

---

## 16. Launch Plan

### Pre-Launch (Weeks 1-8)

| Week | Engineering | GTM |
|---|---|---|
| 1 | Spec lock | 10 design partner calls; collect 30+ questionnaires |
| 2-3 | SDK + Agent/Grant/Verify | Build knowledge base; recruit 5 design partners |
| 4 | Audit log + hash chain + registries | Lock fintech-specific GTM messaging |
| 5 | Approval flow + redaction + anomaly | Launch landing page; build waitlist |
| 6 | Questionnaire engine + Evidence Pack | Onboard design partners; gather testimonials |
| 7 | Trust page + Stripe billing | Draft launch content (HN, PH, blog series) |
| 8 | Polish, docs, dogfood our own SOC 2 | Show HN + Product Hunt + outbound to 100 YC AI fintechs |

### Launch Week
- Day 0: Show HN, Product Hunt, Twitter announcement
- Day 1-2: Outbound to 200 fintech AI founders (YC alumni network, LinkedIn)
- Day 3-7: Founder calls, urgent design-partner conversions

### Post-Launch (Weeks 9-12)
- Iterate based on first 50 customer issues
- Big 4 outbound starts (founder time: 30%)
- Begin fintech-specific content marketing (1 post/week)
- Recruit first compliance-domain hire/advisor

---

## 17. Risks & Mitigations

| Risk | Severity | Mitigation |
|---|---|---|
| Customers cancel after closing one deal (one-time use) | High | Vertical ICP (fintech = continuous compliance need), annual contracts, retention features (multi-customer questionnaire pipeline, always-on trust page) |
| Big 4 partnership doesn't materialize in 12 months | High | Plan B: 2-3 mid-tier audit firm partnerships (Schellman, A-LIGN); Plan C: direct sell with auditor portal lowering Big 4 friction |
| Vanta or SafeBase enters with AI module | Medium | Speed: ship weekly; vertical depth they won't pursue; runtime evidence they can't retrofit cheaply |
| Anthropic/OpenAI ship native compliance evidence | Medium | Position as cross-provider neutral; build on top of native primitives where they exist |
| Auditors reject our evidence format | High | Co-design with 1-2 auditors before V1 ships; align with AICPA TSC IDs strictly |
| SDK adoption friction kills install funnel | High | Obsessive DX investment; office hours; public Discord; live install demos |
| Compliance hire impossible to find | Medium | Fractional advisor in Month 1; full-time in Month 6-9; cofounder-eligible if right person |
| EU AI Act enforcement timeline slips | Low | Don't depend solely on EU AI Act in messaging; SOC 2 + procurement reviews are evergreen drivers |

---

## 18. Open Questions

1. **Brand name** — TrustAI is a placeholder. Candidates: Beacon, Conform, Provenance, Ledger, Sentinel. Need to lock before launch.
2. **Open-source strategy** — SDK MIT-licensed? Control library open? Decision needed by Week 4.
3. **Pricing of free tier** — 100K events/month might be too generous OR too restrictive. Validate with design partners.
4. **First non-fintech expansion vertical** — healthtech or HR-tech in V1.1? Decide by Month 9.
5. **Native MCP gateway** — should V1.1 include a hosted MCP gateway mode (vs SDK-only), or stay SDK-pure?
6. **Bedrock and Vertex SDK priority** — V1 launches Anthropic + OpenAI; when does Bedrock/Vertex land?
7. **Auditor invitation pricing** — included in Growth tier or charged per seat?
8. **Co-marketing rights with Big 4** — what do we offer in exchange for endorsement?

---

## 19. Out of Scope (V1)

Explicit non-asks to prevent scope creep:
- Multi-framework beyond SOC 2 + EU AI Act
- Customer-authored control extensions
- AI bias / fairness testing
- Native chatbot / Copilot integration
- On-prem / VPC / self-hosted
- White-label embedded version
- Multi-language SDK beyond Python + TypeScript
- Anomaly detection ML models (rules-based only in V1)
- Generic SOC 2 automation (policies, training, scans) — Vanta does this
- Real-time WebSocket budget streaming (V1.1)
- Mobile dashboard

---

## 20. Appendix: Control Library Schema (sample — first 10 controls)

```yaml
controls:
  - id: SOC2.CC6.UNIQUE_AGENT_IDENTITY
    tsc: CC6.1
    auditor_question: "Does every AI agent have a unique, attributable identity?"
    severity: critical
    auto_satisfied_by: trustai.agents.create
    evidence_required: [agent_record_unique_id]
    evidence_query: SELECT id, did FROM agents WHERE tenant_id = $1
    documentation_url: /docs/controls/CC6.UNIQUE_AGENT_IDENTITY

  - id: SOC2.CC6.OBO_PRESERVATION
    tsc: CC6.1
    auditor_question: "When an agent acts on behalf of a user, is the user's identity preserved?"
    severity: critical
    auto_satisfied_by: trustai.grants.create with user_proof
    evidence_required: [grant_with_user_proof, jwt_with_sub_and_act]

  - id: SOC2.CC6.LEAST_PRIVILEGE
    tsc: CC6.3
    auditor_question: "Is agent access least-privilege?"
    severity: high
    auto_satisfied_by: agent.max_scopes + grant scope intersection
    evidence_required: [agent_max_scopes, grant_scopes_subset]

  - id: SOC2.CC6.CREDENTIAL_ROTATION
    tsc: CC6.1
    auditor_question: "How are agent credentials rotated?"
    severity: high
    auto_satisfied_by: credential rotation events
    evidence_required: [rotation_event_history]

  - id: SOC2.CC7.IMMUTABLE_AUDIT_LOG
    tsc: CC7.2
    auditor_question: "Are agent audit logs immutable / tamper-evident?"
    severity: critical
    auto_satisfied_by: hash-chain + signed timestamps
    evidence_required: [merkle_root_signature, chain_verification]

  - id: SOC2.CC7.ANOMALY_DETECTION
    tsc: CC7.3
    auditor_question: "How do you detect anomalous agent behavior?"
    severity: high
    auto_satisfied_by: anomaly events from SDK
    evidence_required: [anomaly_event_log, alert_routing_record]

  - id: SOC2.CC8.MODEL_REGISTRY
    tsc: CC8.1
    auditor_question: "Do you maintain a model registry with versions, evals, approvers?"
    severity: critical
    auto_satisfied_by: trustai.models registry
    evidence_required: [model_record_with_eval_metrics]

  - id: SOC2.CC8.ROLLBACK_TESTED
    tsc: CC8.1
    auditor_question: "Is there a tested rollback procedure for AI models?"
    severity: high
    auto_satisfied_by: model.rollback_tested_at populated
    evidence_required: [rollback_test_event]

  - id: SOC2.CC8.PROMPT_VERSION_CONTROL
    tsc: CC8.1
    auditor_question: "Are prompt changes version-controlled and reviewed?"
    severity: medium
    auto_satisfied_by: trustai.prompts registry + change_request linkage
    evidence_required: [prompt_record_with_change_request]

  - id: SOC2.CC9.VENDOR_CONTRACTS
    tsc: CC9.2
    auditor_question: "Do you have BAAs/DPAs with every upstream model provider?"
    severity: critical
    auto_satisfied_by: vendor.contracts populated
    evidence_required: [vendor_record_with_signed_contract]
```

Full library: 54 controls in V1 (covers the 54 auditor questions documented in research), expanding to 200+ by Year 2.

---

## 21. Approval

| Stakeholder | Role | Status |
|---|---|---|
| Founder/CEO | Final decision | Pending |
| Founding Engineer | Technical feasibility | Pending |
| Compliance Advisor (TBD) | Control library validation | Pending hire |
| Design Partner 1 (TBD) | ICP validation | Pending |
| Design Partner 2 (TBD) | ICP validation | Pending |

---

*End of PRD v0.1. Next review: after first 10 design-partner calls (target: 2 weeks).*
