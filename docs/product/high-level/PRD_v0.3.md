# Product Requirements Document

| Field | Value |
|---|---|
| **Product Name** | **Trust0** *(formerly working name "TrustAI"; resolves the brand open question)* |
| **Tagline** | The evidence layer for AI agents — Layer 0 of the agent security stack |
| **Document Version** | 0.3 (adopts `product-brainstorming_v1.md`; re-sequences the ecosystem) |
| **Owner** | Founding team |
| **Status** | Draft — pre-engineering, **spec lock gated on two validation tests (see §12)** |
| **Last Updated** | May 31, 2026 |
| **Target GA (V1)** | August 2026 |
| **Supersedes** | `MarketResearch/AgentSecurity/PRD_v0.2.md` |
| **Source inputs** | `MarketAnalysis.md`, `PRD_v0.1.md`, `PRD_v0.2.md`, `product-brainstorming_v1.md` |

### Changelog from v0.2 → v0.3

- **RENAMED** `TrustAI` → **`Trust0`**; adopts **"Layer 0 / evidence substrate"** positioning (Brainstorm §6.1).
- **RE-SEQUENCED** the v1.5 ecosystem (public API, OAuth 2.1 server, MCP server, OSS connectors, standards-body submission) from core roadmap to a **deferred, post-PMF phase**. We *architect the seams* now; we *do not build* the surface before product-market fit (Brainstorm §6.2, echoing `MarketAnalysis` §5.2's warning against premature platform-building).
- **REFRAMED retention** around **continuous conformity** (EU AI Act Article 19 rolling retention + continuous SOC 2 monitoring) instead of the episodic questionnaire engine (Brainstorm §2).
- **REWROTE the moat** (new §10): defensibility = **corpus + auditor-recognized format + "Secured by Trust0" badge network effect + cross-customer evidence patterns**. The SDK is reframed as the *wedge and data tap*, not the moat.
- **ADDED §12 Validation Plan**: marks the two lethal, unvalidated assumptions — **A1 (post-deal retention)** and **A2 (auditor/procurement acceptance of the evidence format)** — as **explicit risks that gate spec lock**, each with a cheap test.
- **REORGANIZED functional requirements** into **P0 / P1 / P2 (MoSCoW)** with acceptance criteria.
- **SPLIT success metrics** into leading and lagging indicators with targets and measurement methods.

> **Reading note:** This PRD adopts the brainstorm's direction *pending validation*. Sections marked **⚠️ UNVALIDATED** rest on assumptions not yet tested with real users/auditors. Do not lock the spec or begin the build of those areas until §12's tests pass.

---

## 1. Executive Summary

**Trust0 is the runtime evidence layer for AI agents — "Layer 0" of the agent security stack.** A drop-in SDK records every AI agent action with full identity, provenance, and policy context. That evidence powers three customer-facing artifacts: a continuously-updated **trust page**, an **auto-filled enterprise AI security questionnaire**, and an auditor-grade **SOC 2 / EU AI Act evidence pack**.

The `MarketAnalysis` describes a real, urgent, but fiercely-funded market organized into four security layers (identity, gateway, runtime, governance). Trust0 does not compete inside those layers. It supplies the **trustworthy event substrate the other four layers reference** — the zeroth layer beneath them. This positioning is both a wedge (it avoids head-to-head combat with $50–200M-funded incumbents) and a category claim.

**V1 wedge (the acquisition pain):** fintech AI founders lose enterprise deals to AI security reviews. Trust0's demo unblocks a stalled deal in minutes — *paste the buyer's questionnaire, get auditor-cited answers and a branded trust page.*

**V1 retention (the continuous job):** the same evidence stream keeps customers continuously **conformant** (EU AI Act Article 19 mandates 6-month rolling audit-log retention; SOC 2 has moved to continuous monitoring) and keeps their trust page live as an inbound-qualifying asset. Retention is designed into first-run, not bolted on via annual contracts.

**Deferred by design:** the open-ecosystem strategy from v0.2 (open APIs, OAuth, MCP server, OSS connectors, standards body) remains the long-term moat-and-distribution narrative, but it is **explicitly out of the V1 critical path**. We build the architectural seams; we defer the surface until the wedge is proven.

**Two assumptions gate everything (see §12):** that customers keep paying after their first deal closes (**A1**), and that real auditors and enterprise reviewers accept our evidence format (**A2**). Both are cheap to test and lethal if false. We test them *before* locking this spec.

---

## 2. Problem Statement

### The user problem (carried from v0.1/v0.2, tightened)

Fintech AI startups face a binding constraint: every enterprise sales cycle now includes an **AI-specific security review** of 50–200 questions. Today founders spend 2–6 weeks per deal hand-writing answers, hire $20K+ consultants for policies they don't have, submit incomplete responses that stall negotiations, and repeat the cycle for every customer's annual vendor re-review.

### The two-sided trust problem (elevated in v0.3)

The buyer (the founder, card-swipe, self-serve) is **not** the acceptor (the enterprise's procurement team and the SOC 2 auditor). Trust0 only creates value if the *acceptor* recognizes the evidence as auditor-grade. This two-sidedness is the central go-to-market risk and is treated as a first-class assumption (**A2**, §12), not an afterthought.

### The structural driver (from `MarketAnalysis` §2.4)

Agents are non-deterministic, select tools dynamically, fail silently, and operate as fleets — so traditional logging does not satisfy auditors or regulators. Point-in-time policy attestations no longer pass in 2026; **runtime evidence with cryptographic proof is required.** No incumbent supplies this as a shared substrate.

### Why now

- **EU AI Act enforcement begins August 2, 2026** — Article 19 requires rolling audit-log retention; Article 99 penalties reach €15M / 3% of global turnover.
- **SOC 2 auditors hardened AI expectations in 2026** — runtime evidence required.
- **Enterprise procurement institutionalized AI security questionnaires.**
- **The agent stack standardized around MCP + OAuth 2.1 (2025–26)**, making runtime instrumentation tractable.
- **The competitive window is finite.** `MarketAnalysis` documents active consolidation ($96B M&A). Trust0's realistic strategic asset is the **6–12 month window** before an incumbent (e.g., Vanta acquiring a runtime-observability player) ships agent compliance natively (Brainstorm §5/A4).

---

## 3. Goals & Non-Goals

### V1 Goals (the wedge + the retention anchor)

1. Ship a Python + TypeScript SDK that captures runtime agent activity with one-line integration.
2. Ship a SOC 2 control library mapped to the 54 questions auditors actually ask in 2026.
3. Ship the **questionnaire auto-fill engine** as the primary acquisition demo.
4. Ship a live, branded **trust page** as a continuous, inbound-qualifying asset.
5. Ship a one-click **SOC 2 / EU AI Act evidence pack** export for auditor handoff.
6. **Make continuous conformity the retention core** — the product is valuable on day 60 with no active deal, because it maintains rolling-retention conformity and a live trust page.
7. **Architect for open reads from day 1** (separate auth namespace, versioned schemas, webhook primitives) — built as seams, **internally scoped, not exposed**.
8. Validate the two lethal assumptions (§12) *before* spec lock; then capture 50 paying fintech customers in 90 days post-launch.
9. Lock 1 auditor "preferred format" relationship (mid-tier acceptable; Big 4 aspirational) within 12 months.

### Non-Goals (V1) — with rationale

| Non-goal | Why it's out of scope for V1 |
|---|---|
| **Building the open ecosystem surface** (public API, OAuth server, MCP server, OSS connectors, standards submission) | Strategy outrunning evidence; `MarketAnalysis` warns a small team against platform-building. Deferred to a post-PMF phase (§11, §13). Seams only. |
| Multi-framework beyond SOC 2 + EU AI Act (HIPAA, FINRA, ISO 42001) | Focus; deferred to V2 unless the vertical test (§11 OQ) flips us to healthtech. |
| Customer-authored controls | We provide the library; extensibility is a V2 question. |
| On-prem / VPC / white-label | Wrong motion for a self-serve founder buyer. |
| AI safety / bias testing | Different product. |
| Generic SOC 2 automation (Vanta-style policies/training/scans) | We are agent-runtime-specific; competing here invites the incumbents' strength. |
| Selling to enterprise CISOs | V1 buyer is the founder/CEO. |
| Treating the SDK as the moat | Reframed: the SDK is the wedge + data tap. The moat is §10. |

---

## 4. Target Customer (ICP)

### Primary V1 ICP

**Fintech AI startup, Seed–Series B (5–150 employees), with at least one enterprise customer in an active sales cycle or signed in the last 12 months.**

Signals: building agents that touch financial data; selling to banks/credit unions/fintechs/enterprise finance teams; asked to complete ≥1 vendor security questionnaire in the last 6 months; no dedicated CISO, or has Vanta but it doesn't cover agents.

### Buyer persona: "The Founding Sales Engineer"

CTO / Head of Eng / founding SE / CEO at a sub-50-person fintech AI startup. Has 3–5 enterprise deals stuck in security review; spends 10+ hrs/week on questionnaires. Can swipe a card up to ~$500/mo without approval. **Trigger event:** a specific enterprise buyer sends a multi-page AI security questionnaire.

### The acceptor (not the buyer, but decisive)

The enterprise's **security/procurement reviewer** and the customer's **SOC 2 auditor**. They never pay us, but they must accept our evidence. Their requirements drive §6 (FR-EP) acceptance criteria and assumption **A2**.

### Exclusions

Pre-revenue startups with no enterprise motion; consumer AI with no enterprise buyers; >1,000-employee enterprises with existing GRC programs; non-fintech verticals in V1 (vertical discipline — revisit per §11 OQ).

---

## 5. User Stories

### Acquisition (episodic, acute) — the wedge
- As a fintech AI founder, I want to paste my buyer's 100-question AI security questionnaire and receive 70+ auto-filled, evidence-cited answers in 10 minutes, so I stop losing deals to slow procurement.
- As a head of engineering, I want to install an SDK in <30 minutes and immediately see runtime evidence captured, so I can validate the product before committing budget.

### Retention (continuous) — the anchor *(new emphasis in v0.3)*
- As a fintech founder, I want my trust page to stay live and current with zero effort, so inbound enterprise buyers arrive pre-qualified on security and I keep seeing value between deals.
- As an engineering lead selling into the EU, I want Trust0 to continuously satisfy EU AI Act Article 19 retention, so conformity is a standing state, not a per-deal scramble.
- As a founder facing annual SOC 2, I want continuous monitoring so my next audit is a one-click evidence pack, not a three-week fire drill.

### Acceptor stories — the two-sided trust *(elevated in v0.3)*
- As a SOC 2 auditor, I want evidence mapped to control IDs I recognize, with tamper-evident proof, so I can accept it without a custom per-client process.
- As an enterprise security reviewer, I want to self-serve a vendor's trust page and verify claims, so I can clear the security gate faster.

### Operational
- As an engineering lead, I want to register models, prompts, and providers once, so my team doesn't think about compliance on every code change.
- As a CTO, I want the SDK to detect runaway agent loops and stop them before budget blowouts, so I avoid incidents auditors flag.

---

## 6. Functional Requirements (P0 / P1 / P2)

Requirements are prioritized MoSCoW-style. **P0 = cannot ship V1 without it.** Detailed endpoint/registry specifications are carried forward from `PRD_v0.1.md` §9 and `PRD_v0.2.md` §9 except where changed below.

### P0 — Must-have (the minimum viable wedge + retention anchor)

**FR-SDK-1 — One-line LLM client wrapping** (Python + TS) for `anthropic`, `openai`, `bedrock`, `vertex`.
- *Acceptance:* Given a developer with an API key, when they replace their client constructor with the Trust0 wrapper, then runtime evidence events appear in the dashboard within 30 seconds, with zero other code changes.

**FR-SDK-3 — Auto-capture per call:** agent/user/task/model/prompt/guardrail/vendor IDs, scopes, tool calls, input/output hashes, cost, latency, timestamps.
- *Acceptance:* Given an instrumented agent call, when it completes, then an evidence event records all listed fields and links to the originating session.

**FR-SDK-4 — Local-first, async batched upload.** Target 0ms added on the hot path; **p99 ≤ 5ms** (see assumption A6, §12).
- *Acceptance:* Given a benchmarked agent loop, when measured over 10k calls, then added latency p99 ≤ 5ms; on backend outage the SDK degrades gracefully for ≥60s on last-known-good state.

**FR-REG — Registries** (Model, Prompt, Vendor, Guardrail) — the SOC 2 CC8 backbone.
- *Acceptance:* Given a call referencing an unregistered model, when evidence is generated, then it is flagged "not auditor-grade" until the model is registered; registered entities auto-attach to evidence.

**FR-Q — Questionnaire auto-fill engine** (the acquisition magnet). Accept SIG/CAIQ/Word/PDF/CSV; classify each question; auto-fill from the customer's evidence with cited event IDs; flag gaps with a 30-minute fix plan; allow human edit; export branded PDF/DOCX/original.
- *Acceptance:* Given an uploaded real-world questionnaire, when auto-fill runs, then ≥70% of questions receive a candidate answer with ≥1 cited evidence event, and gaps are listed with a remediation link. *(Target % pending A2 calibration.)*

**FR-TP — Trust page** (the continuous retention artifact). Auto-generated public URL; sections for agent inventory, models, data flows, frameworks, live activity stats, incident log, certifications, subprocessors; updates live from runtime evidence; permanent **"Secured by Trust0" badge** with audit-link verification; embeddable badge.
- *Acceptance:* Given runtime evidence flowing, when a buyer visits the trust page, then stats reflect activity from the last 24h with no manual refresh; the badge links to a verifiable proof.

**FR-EP — Evidence pack export** (auditor handoff; the acceptor artifact). Control-by-control evidence, hash-chain proof, auditor cover sheet, event-ID index, manifest CSV; period filters; control-ID mapping in the auditor's format; Merkle-root completeness proof signed by KMS; auditor portal invite.
- *Acceptance:* Given a selected period and framework, when export runs, then a signed zip is produced in ≤60s for 1 year of evidence, mapped to AICPA TSC IDs (configurable to a firm's preferred format). **⚠️ UNVALIDATED until A2 passes** — the exact accepted format is an auditor-driven requirement.

**FR-CONF — Continuous conformity monitor** *(new in v0.3 — the retention core).* Continuously evaluate the customer's live evidence against EU AI Act Article 19 retention requirements and SOC 2 continuous-monitoring controls; surface a standing "conformity status" with alerts on drift.
- *Acceptance:* Given a tenant with retention/monitoring requirements, when evidence falls out of conformance (e.g., retention gap, missing control evidence), then the dashboard shows a red status and alerts via Slack/email within the configured window. **⚠️ Depends on A1** (that customers value this continuously) and a research item (does Article 19 apply to our ICP — §11).

**FR-AUTH-SEAM — Read/write credential separation** *(architected, internally scoped).* SDK credentials can write; a structurally separate credential class is reserved for future external reads but **is not exposed to any external consumer in V1.**
- *Acceptance:* Given the auth middleware, when any non-SDK credential attempts a write, then it is rejected at the middleware layer regardless of scope; no external read credentials are issuable in V1.

### P1 — Should-have (high-value fast follows)

- **FR-APR — Approval flow** (human-in-the-loop on risk/cost/scope triggers; Slack/email/webhook/hosted UI; blocking until decision/timeout; every decision recorded).
- **FR-SDK-5 — Local loop/anomaly detection** (repeated tool args, tokens/sec, max turns) emitting anomaly events off the hot path.
- **FR-SDK-6 — Redaction policies** applied before upload (PII/PHI never leaves the customer process unredacted).
- **FR-DSH — Dashboard**: activity feed, agents, registries, audit log (filterable on every dimension), approvals queue, anomalies, trust-page settings, evidence exports, questionnaires, frameworks, team, billing. Clerk auth.
- **FR-Q-7 — Customer question library** so repeated buyer requests reuse polished answers (compounds the corpus — see §10).

### P2 — Future considerations (design-for, don't build)

- Open public read API, OAuth 2.1 delegated access, MCP compliance server, OSS reference connectors (Vanta/Drata/SafeBase), open "Agent Compliance Event" schema + standards-body submission. **All deferred to the post-PMF Ecosystem phase (§13).** Carried forward from `PRD_v0.2.md` §9.9–9.12 as the future spec; we keep the seams (FR-AUTH-SEAM, versioned schemas, webhook primitives) so we can build these without rework.
- Decision-reconstruction API, GDPR DSAR workflow, WORM storage tier, multi-region EU residency.

---

## 7. Success Metrics

### Leading indicators (days → weeks)

| Metric | Target | Measurement |
|---|---|---|
| Signup → SDK install | < 30 min (p50) | Onboarding funnel timestamps |
| Install → first evidence event | < 10 min (p50) | Event pipeline |
| Questionnaire auto-fill coverage | ≥ 70% of questions answered with citation | Per-questionnaire telemetry *(calibrate to A2)* |
| Questionnaires auto-filled / customer / month | ≥ 2 | Product analytics |
| Trust pages published | ≥ 30 (of first 50 customers) | Trust-page service |
| **Day-60 active usage (no open deal)** ⚠️ | ≥ 60% of customers active | Retention cohort — **the A1 proxy metric** |

### Lagging indicators (weeks → months)

| Metric | Target | Measurement |
|---|---|---|
| Paying customers (90 days) | 50 | Billing |
| MRR (90 days) | $10K | Billing |
| % customers in fintech | ≥ 80% | CRM |
| **Logo churn (annualized)** ⚠️ | < 15% | Billing cohort — **the true A1 test** |
| NPS (paying) | ≥ 50 | Survey |
| **Evidence packs accepted by an auditor** ⚠️ | ≥ 10 in year 1 | Customer-reported + auditor portal — **the true A2 test** |
| Auditor "preferred format" relationship | 1 (mid-tier ok) | Partnerships |
| Questionnaire corpus size | 200 canonical questions | Corpus DB |

### Anti-metrics (refuse to optimize)
Total signups across verticals; free-tier conversion rate; feature breadth; number of integrations.

---

## 8. Product Overview

One backend, V1 surfaces, **ecosystem seams architected but not exposed:**

```
┌──────────────────────────────────────────────────────────────┐
│  V1 SURFACES (built)                                          │
│   SDK (Py+TS)   │   Dashboard   │   Trust Page   │  Auditor   │
│                 │               │   (public)     │  Portal    │
└────────┬────────────────┬───────────────┬─────────────┬───────┘
         │                │               │             │
┌────────▼────────────────▼───────────────▼─────────────▼───────┐
│  CORE TRUST0 BACKEND                                          │
│  Evidence pipeline · Control library · Corpus · Hash-chain    │
│  Registries · Questionnaire engine · Continuous conformity    │
│  Auth middleware (write=SDK-only; read-seam reserved)         │
└────────┬───────────────────────────────────────────────────────┘
         ┆  (seams only — NOT exposed in V1)
┌────────▼───────────────────────────────────────────────────────┐
│  POST-PMF ECOSYSTEM PHASE (deferred)                          │
│  Public read API · OAuth 2.1 · MCP server · OSS connectors    │
└──────────────────────────────────────────────────────────────┘
```

**Positioning — "Layer 0":** identity, gateway, runtime, and governance tools (`MarketAnalysis` §4.1) all need a trustworthy event record. Trust0 is the substrate they reference — the zeroth layer. This is the category claim and the eventual integration surface, but in V1 it is expressed only through our own artifacts.

---

## 9. Non-Functional Requirements

- **Performance:** SDK hot-path ≤ 5ms p99 (A6); evidence pack ≤ 60s for 1 year; trust page ≤ 1.5s p95.
- **Reliability:** 99.9% API uptime (paid); graceful SDK degradation on outage.
- **Security (our own posture must be exemplary):** SOC 2 Type II within 6 months of GA (dogfood); evidence encrypted at rest (AWS KMS/GCP CMEK); hash-chained audit log with WORM tier for paid; per-tenant US/EU residency at signup; employee access MFA'd + audited; public bug bounty within 90 days.
- **Compliance:** GDPR day 1; SOC 2 Type II target Q1 2027; ISO 27001 target Q2 2027.
- **Scalability:** 1M agent actions/day/tenant; 1,000 tenants in V1.

---

## 10. Defensibility / Moat *(rewritten in v0.3)*

v0.2 called the SDK the moat. It isn't — wrapping an LLM client is a days-long task, and v0.2 simultaneously open-sourced the schema. The SDK is the **wedge and the data tap.** The real, compounding moat is:

1. **The corpus.** The canonical knowledge base of auditor questions + matching engine + polished, human-edited answers. Every customer and every edit makes it better. Hard to copy; improves with scale.
2. **Auditor-recognized format.** A "preferred format" relationship with even one respected audit firm is a genuine moat — it makes our evidence the path of least resistance. Invest here early (it also de-risks A2).
3. **The "Secured by Trust0" badge network effect.** Every live trust page is a billboard and a switching cost — removing Trust0 visibly breaks a public commitment buyers can see.
4. **Cross-customer anonymized evidence patterns.** Aggregated (privacy-safe) patterns improve auto-fill quality for everyone — the true data network effect.

**Implication for sequencing:** because we intend to eventually open-source the schema (category leadership over format lock-in), we must own (1)–(4) *first*. Open-sourcing the format while the corpus and auditor relationships are weak would be self-commoditization (Brainstorm §5, inversion pass).

---

## 11. Open Questions

Tagged by who must answer.

1. **[Founder] Vertical choice** — fintech vs. healthtech. Fintech reads as familiarity, not evidence; healthtech (HIPAA) may carry harder forcing functions. *Resolve via the §12 vertical pain comparison.*
2. **[Legal/Research] EU AI Act Article 19 applicability** — does rolling retention actually bind our ICP's systems, or only Annex III high-risk? This determines whether FR-CONF's retention anchor is real. **Blocking for FR-CONF.**
3. **[Auditor/Product] Accepted evidence format** — exact artifacts, control-ID schemes, and proof formats auditors will accept. **Blocking for FR-EP; = assumption A2.**
4. **[Product] Retention mechanic** — if A1 is weak, which continuous job do we anchor to (conformity vs. inbound trust-page value vs. continuous SOC 2)? **Blocking for FR-CONF priority.**
5. **[Founder] Brand** — confirm "Trust0" and lock the "Layer 0" positioning line.
6. **[Eng] OAuth build-vs-buy** — `ory/hydra` vs. direct — *deferred with the ecosystem phase; not a V1 decision.*
7. **[Eng] Bedrock/Vertex SDK timing** — V1 ships Anthropic + OpenAI; when do the others land?
8. **[Founder] Auditor invitation pricing** — bundled in Growth tier or per-seat?

---

## 12. Validation Plan — assumptions that gate spec lock ⚠️

Per the chosen direction, the converged strategy is adopted **pending validation**. The two assumptions below are lethal and external; both are cheap to test and must be run **before** locking this spec or building the dependent areas.

### A1 — Post-deal retention *(business-model lethal)*
- **Assumption:** Customers keep paying after their first enterprise deal closes.
- **Why lethal:** The acquisition job is episodic. If nothing makes day-60 valuable, annual contracts only defer churn. Drives FR-CONF and the entire retention thesis.
- **Cheapest test:** Structured interviews with the existing design-partner pipeline: *"After the deal closed, would you still pay next month? For what?"* Target ≥ 10 conversations. **Proxy metric:** Day-60 active usage ≥ 60% (§7). **Pass bar:** a majority articulate a continuous reason to pay (conformity, trust-page inbound, next audit).
- **If it fails:** re-anchor retention (OQ #4) before building FR-CONF as specified.

### A2 — Auditor / procurement acceptance *(go-to-market lethal)*
- **Assumption:** Real auditors and enterprise reviewers accept Trust0's evidence pack as auditor-grade.
- **Why lethal:** The buyer ≠ the acceptor. If the acceptor shrugs, the founder's pain isn't solved and they churn and warn peers. Drives FR-EP and FR-Q targets.
- **Cheapest test:** Put the sample evidence pack (`PRD_v0.1.md` §20 controls + §22 schema) in front of **3 SOC 2 auditors** and **1 enterprise security reviewer**. Ask: "Would you accept this? What's missing?" **Highest information-per-hour action available.** **Pass bar:** ≥ 2 auditors say they'd accept with minor changes, and we capture their format requirements.
- **If it fails:** rework FR-EP format to the auditors' stated requirements before committing the questionnaire-engine acceptance criteria.

### A6 — SDK hot-path overhead *(feasibility, not strategy)*
- **Test:** 2-day SDK spike against a real agent loop; measure p99 honestly against the ≤5ms target. **If it fails:** revisit local-first batching / move redaction off the hot path.

> **Gate:** Do not lock §6 P0 acceptance criteria for FR-EP, FR-Q, and FR-CONF until A1 and A2 have results.

---

## 13. Timeline Considerations

### Phase 0: Validation (Week 0–1) — *gates the spec*
Run A1 (retention interviews) and A2 (auditor format reviews) from §12. Lock vertical (OQ #1) and Article 19 applicability (OQ #2). **Only then** finalize §6 acceptance criteria.

### Phase 1: V1 wedge + retention (Weeks 1–8)
SDK + registries + evidence pipeline + hash chain → questionnaire engine + evidence pack → trust page + **continuous conformity monitor** + Stripe billing → polish, docs, dogfood our own SOC 2. GTM in parallel: design-partner calls, knowledge-base build, fintech messaging, Show HN / Product Hunt, outbound to YC AI fintechs. *(Mirrors `PRD_v0.1.md` §16, with FR-CONF added and ecosystem removed.)*

### Phase 2: Prove PMF + auditor relationship (Months 3–6)
Iterate on the first 50 customers; convert the A2 auditor into a "preferred format" relationship; grow the corpus toward 200 questions; *one* listening call with a Vanta/Drata/Hyperproof product lead (intel on the build-vs-partner question / window length — A4).

### Phase 3: Ecosystem (post-PMF, deferred) — formerly v1.5
Only after the wedge is proven: build the public read API, OAuth 2.1, MCP server, OSS connectors, and open-schema/standards submission per `PRD_v0.2.md` §9.9–9.12. The seams (FR-AUTH-SEAM, versioned schemas, webhook primitives) are in place so this is additive, not a rewrite.

### Hard dates / dependencies
- **EU AI Act enforcement: August 2, 2026** — informs FR-CONF and EU residency, but per §12 we don't let a single regulatory date carry demand (SOC 2 + procurement are evergreen).
- Auditor co-design (A2) is a **blocking dependency** for FR-EP.

---

## 14. Out of Scope (V1)

Multi-framework beyond SOC 2 + EU AI Act; customer-authored controls; AI bias/fairness testing; native chatbot/Copilot integration; on-prem/VPC/self-hosted; white-label; multi-language SDK beyond Python + TS; ML-based anomaly detection (rules only); generic SOC 2 automation; real-time WebSocket budget streaming; mobile dashboard.

**Explicitly deferred (not cancelled) — the Ecosystem phase:** public write endpoints (never to external keys — the one permanent rule we keep from v0.2's doctrine), open read API, OAuth server, MCP server, OSS connectors, standards-body submission. Carried as the §6 P2 / §13 Phase 3 spec.

---

## 15. Approval

| Stakeholder | Role | Status |
|---|---|---|
| Founder/CEO | Final decision + vertical (OQ #1) + brand (OQ #5) | Pending |
| Founding Engineer | Technical feasibility (V1 architecture + A6 spike) | Pending |
| Compliance Advisor (TBD) | Control library validation + **A2 auditor reviews** | Pending hire / fractional |
| Design Partners (TBD) | ICP validation + **A1 retention interviews** | Pending |

---

*End of PRD v0.3. **Next action: run §12 (A1 + A2) before locking §6.** This document adopts `product-brainstorming_v1.md` pending those results.*
