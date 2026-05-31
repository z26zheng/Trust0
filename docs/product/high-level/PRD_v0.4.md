# Product Requirements Document

| Field | Value |
|---|---|
| **Product Name** | **Trust0** |
| **Buyer-facing tagline** | *Close the enterprise deal that's stuck in AI security review.* |
| **Category narrative (internal)** | The evidence layer for AI agents — "Layer 0" of the agent security stack |
| **Document Version** | 0.4 (applies `prd-v0.3-review.md`; fixes positioning, moat honesty, hidden assumptions) |
| **Owner** | Founding team |
| **Status** | Draft — pre-engineering, **spec lock gated on validation tests (see §12)** |
| **Last Updated** | May 31, 2026 |
| **Target GA (V1)** | August 2026 |
| **Supersedes** | `PRD_v0.3.md` |
| **Source inputs** | `MarketAnalysis.md`, `PRD_v0.1.md`, `PRD_v0.2.md`, `product-brainstorming_v1.md`, `prd-v0.3-review.md` |

### Changelog from v0.3 → v0.4 (each item traces to a review finding)

- **SPLIT POSITIONING (C1).** Buyer-facing headline is now the painkiller ("close the stuck deal"). **"Layer 0" demoted** from the tagline to an internal category narrative (§1, §8). We stop letting the investor story drive the buyer message.
- **MADE THE MOAT HONEST (C2).** §10 now leads with the *robust* moats (auditor-recognized format + badge); states the corpus moat as **conditional on retention + scale and limited to the agent-specific slice**; names the LLM-erosion counterpoint.
- **COUNTED ALL LETHAL ASSUMPTIONS (C3).** §12 adds **A7 (Layer-0 category), A8 (corpus compounds), A9 (EU AI Act Art. 19 applicability — promoted from a research OQ), A10 (evidence→deal causality)** and re-ranks lethality.
- **RECONCILED WINDOW vs. DEFER (H1, H2).** The 6–12mo window is stated as an explicit dated bet; the read-seam is **exercised internally in Phase 1** (our own trust page + auditor portal read through it) to validate it cheaply; the *heavy* ecosystem stays deferred.
- **RESOLVED THE FINTECH CONTRADICTION (H3).** Fintech is now a **committed V1 focus bet** (not "open"); healthtech is the leading **V2 expansion** candidate with a one-call Phase-0 sanity check.
- **SCOPED FR-CONF to agent-specific conformity and moved it to P1 (H4, M4)** pending A1. The **trust page (P0)** carries the continuous-value story at launch.
- **RE-DERIVED METRICS (H5).** §7 separates acquisition / retention / acceptance metrics and states an explicit **tier-mix assumption** behind the MRR target.
- **FIXED THE SOC 2 CLAIM (M1).** Type I @ ~6 months, Type II @ ~12 months.
- **ADDED §11 "Detractors" (M2)** — who would actively resist, with mitigations.
- **RECORDED WHY THE SDK STAYS P0 (Provoke)** despite being "not the moat," and logged SDK-optional ingestion as a P2 alternative.

> **Reading note:** Sections marked **⚠️ UNVALIDATED** rest on assumptions not yet tested. Do not lock the spec or build those areas until §12's tests pass. This document is honest about what it does *not* yet know — that is a feature, not a gap.

---

## 1. Executive Summary

**Trust0 helps fintech AI startups close the enterprise deals that stall in AI security review.** A drop-in SDK records every AI agent action with identity, provenance, and policy context. That evidence powers three artifacts the founder can put in front of a buyer this week: an **auto-filled AI security questionnaire**, a live **branded trust page**, and an auditor-grade **SOC 2 / EU AI Act evidence pack**.

**The wedge (acquisition):** enterprise sales cycles now include a 50–200 question AI security review. Founders lose weeks and deals to it. Trust0's demo answers it — *paste the questionnaire, get evidence-cited answers and a trust page in minutes.*

**The anchor (retention):** the same evidence stream keeps the trust page live (an inbound-qualifying asset between deals) and — for customers it legally applies to — maintains agent-specific conformity (EU AI Act Article 19 agent-log retention; continuous SOC 2 for the agent slice). **Whether this retention demand is real is the #1 thing we test before building it (A1, §12).**

**The category narrative (internal / investor — not the buyer headline):** longer term, identity, gateway, runtime, and governance tools (`MarketAnalysis` §4.1) all need a trustworthy agent event record. Trust0 aims to be that substrate — "Layer 0." We hold this as the long game, **but we do not lead the buyer with it** (it's vendor language; the buyer buys the painkiller). See §8 and the review's finding C1.

**Deferred by design:** the open ecosystem (public API, OAuth server, MCP server, OSS connectors, standards body) is real strategy but **out of the V1 critical path**. We build — and in Phase 1 *internally exercise* — the read-seam, and defer the heavy surface until the wedge is proven.

**What gates everything (§12):** a short, cheap battery of tests on the assumptions that would kill us — retention (A1), auditor acceptance (A2), and now also the category bet (A7), the corpus moat (A8), Article 19 applicability (A9), and the evidence→deal causal link (A10). We test before we lock.

---

## 2. Problem Statement

### The user problem
Fintech AI startups face a binding constraint: every enterprise sales cycle now includes an **AI-specific security review** of 50–200 questions. Founders spend 2–6 weeks per deal hand-writing answers, hire $20K+ consultants for policies they don't have, stall negotiations with incomplete responses, and repeat for every customer's annual re-review.

### The causal claim we must verify (A10)
The wedge assumes **evidence quality is the binding constraint** on the deal. It may not be — the real gate may be the enterprise's **procurement queue latency**, in which case better answers still sit for weeks. "Unblock in minutes" overpromises if so. We test this directly in the A1/A2 interviews (§12).

### The two-sided trust problem
The **buyer** (founder, card-swipe, self-serve) is **not** the **acceptor** (enterprise security reviewer + SOC 2 auditor). Value only exists if the acceptor recognizes the evidence as auditor-grade (A2). This is the central GTM risk, treated as a first-class assumption.

### The structural driver (`MarketAnalysis` §2.4)
Agents are non-deterministic, select tools at runtime, fail silently, and run as fleets — traditional logging doesn't satisfy auditors or regulators. Point-in-time policy attestations no longer pass in 2026; runtime evidence with cryptographic proof is required. No incumbent supplies this for agents as a shared record.

### Why now — and the window bet (H1)
- **EU AI Act enforcement begins August 2, 2026** — Art. 19 retention; Art. 99 penalties to €15M / 3% of turnover. *(Applicability to our ICP is assumption A9 — not yet confirmed.)*
- **SOC 2 auditors hardened AI expectations in 2026**; **procurement institutionalized AI questionnaires**; **the agent stack standardized on MCP + OAuth 2.1**.
- **The window is an explicit, dated bet:** we estimate **~6–12 months** before an incumbent (e.g., Vanta acquiring a runtime-observability player) ships agent compliance natively (`MarketAnalysis` consolidation data; Brainstorm A4). **This bet has a consequence the review flagged (H1):** we cannot defer *all* ecosystem/moat work to post-PMF and still exploit the window — so the cheap read-seam is exercised inside Phase 1 (§13), even as the heavy surface waits.

---

## 3. Goals & Non-Goals

### V1 Goals
1. Python + TypeScript SDK capturing runtime agent activity with one-line integration.
2. SOC 2 control library mapped to the 54 questions auditors ask in 2026.
3. **Questionnaire auto-fill engine** — the acquisition demo.
4. Live, branded **trust page** — the P0 continuous-value artifact.
5. One-click **SOC 2 / EU AI Act evidence pack** for auditor handoff.
6. **Commit to fintech** as the V1 focus vertical (H3) — a deliberate concentration bet, not an open question.
7. Build the read-seam and **exercise it internally in Phase 1** (validate the interface before any external exposure).
8. Validate the gating assumptions (§12) **before** spec lock; then 50 paying fintech customers in 90 days (tier-mix caveat, §7).
9. Lock 1 auditor "preferred format" relationship (mid-tier ok) within 12 months.

### Non-Goals (V1) — with rationale

| Non-goal | Why |
|---|---|
| Building the **heavy** ecosystem surface (public API, OAuth server, MCP server, OSS connectors, standards submission) | Strategy outrunning evidence; `MarketAnalysis` §5.2. Deferred to Phase 3. *(The cheap read-seam is exercised internally in Phase 1 — that is not the same as building the surface.)* |
| **Generic SOC 2 automation** (Vanta-style policies/training/scans) | Incumbent home field. **FR-CONF is scoped to the agent-specific slice only** to stay out of this fight (H4). |
| Multi-framework beyond SOC 2 + EU AI Act (HIPAA/FINRA/ISO 42001) | Focus; HIPAA arrives with the healthtech V2 expansion. |
| Customer-authored controls; on-prem/VPC/white-label; AI safety/bias testing; selling to CISOs | Wrong scope or wrong buyer for V1. |
| Treating the SDK as the moat | The SDK is the wedge + data tap; the moat is §10. |

---

## 4. Target Customer (ICP)

### Primary V1 ICP — committed bet (H3)
**Fintech AI startup, Seed–Series B (5–150 employees), with ≥1 enterprise customer in an active cycle or signed in the last 12 months.** Fintech is a **deliberate concentration choice** (founder familiarity + `MarketAnalysis` vertical-discipline), not a placeholder pending a bake-off. Healthtech is the leading **V2 expansion** candidate, sanity-checked with one Phase-0 call (§12/§13), not a parallel V1 track.

Signals: agents touching financial data; selling to banks/credit unions/fintechs/enterprise finance; asked for ≥1 vendor security questionnaire in 6 months; no dedicated CISO, or has Vanta but it doesn't cover agents.

### Buyer persona — "The Founding Sales Engineer"
CTO / Head of Eng / founding SE / CEO at a sub-50-person fintech AI startup. 3–5 enterprise deals stuck in security review; 10+ hrs/week on questionnaires. Card authority ~$500/mo. **Trigger:** a specific buyer sends a multi-page AI security questionnaire.

### The acceptor (decisive, doesn't pay)
Enterprise **security/procurement reviewer** + the customer's **SOC 2 auditor**. Their requirements drive FR-EP and assumption A2. (They can also be *detractors* — see §11.)

### Exclusions
Pre-revenue/no enterprise motion; consumer AI; >1,000-employee enterprises with existing GRC; non-fintech verticals in V1.

---

## 5. User Stories

### Acquisition (acute) — the wedge
- As a fintech AI founder, I paste my buyer's 100-question AI security questionnaire and get 70+ evidence-cited answers in minutes, so I stop losing deals to slow procurement.
- As a head of engineering, I install an SDK in <30 min and immediately see runtime evidence, so I can validate before paying.

### Retention (continuous) — anchor, pending A1
- As a fintech founder, I want my trust page to stay live with zero effort, so inbound buyers arrive pre-qualified and I keep seeing value between deals. *(P0 — the launch retention story.)*
- As an EU-selling engineering lead, I want Trust0 to maintain agent-log retention for EU AI Act Art. 19, so conformity is standing, not a scramble. *(P1, pending A9.)*

### Acceptor — two-sided trust
- As a SOC 2 auditor, I want evidence mapped to control IDs I recognize with tamper-evident proof, so I accept it without a custom per-client process.
- As an enterprise security reviewer, I want to self-serve and verify a vendor's trust page, so I clear the gate faster.

### Operational
- As an engineering lead, I register models/prompts/providers once, so my team doesn't think about compliance on every change.
- As a CTO, I want the SDK to catch runaway agent loops before budget blowouts.

---

## 6. Functional Requirements (P0 / P1 / P2)

Ruthlessly prioritized (`write-spec`: "if everything is P0, nothing is P0"). Detailed endpoint/registry specs carry forward from `PRD_v0.1.md` §9 / `PRD_v0.2.md` §9 except as changed.

### P0 — Must-have (minimum viable wedge + the *launch* retention artifact)

**FR-SDK-1 — One-line LLM client wrapping** (Py + TS) for `anthropic`, `openai`, `bedrock`, `vertex`.
- *Why P0 despite "SDK is not the moat" (review Provoke):* the SDK is the **data tap** — it produces the input/output **hashing and provenance** that generic OTel/LangSmith traces cannot, which is what makes evidence *auditor-grade*. That provenance is the reason to wrap the client rather than ingest existing traces (logged as a P2 alternative).
- *Acceptance:* replacing the client constructor yields evidence events in the dashboard within 30s, zero other code changes.

**FR-SDK-3 — Auto-capture per call:** agent/user/task/model/prompt/guardrail/vendor IDs, scopes, tool calls, input/output hashes, cost, latency, timestamps.
- *Acceptance:* a completed call records all fields and links to its session.

**FR-SDK-4 — Local-first, async batched upload.** Target 0ms hot-path; **p99 ≤ 5ms** (A6).
- *Acceptance:* over 10k calls, added p99 ≤ 5ms; graceful degradation ≥60s on backend outage.

**FR-REG — Registries** (Model, Prompt, Vendor, Guardrail) — SOC 2 CC8 backbone.
- *Acceptance:* a call to an unregistered model flags evidence "not auditor-grade" until registered; registered entities auto-attach.

**FR-Q — Questionnaire auto-fill engine** (acquisition magnet). SIG/CAIQ/Word/PDF/CSV; classify; auto-fill from evidence with cited event IDs; gap fix-plan; human edit; export branded PDF/DOCX/original.
- *Acceptance:* ≥70% of questions get a candidate answer with ≥1 cited event; gaps listed with remediation. *(Target % pending A2 calibration.)*

**FR-TP — Trust page** (the P0 continuous-value artifact — now carrying the retention story at launch, per H4/M4). Public URL; agent inventory, models, data flows, frameworks, live stats, incident log, certs, subprocessors; live from runtime evidence; permanent **"Secured by Trust0" badge** with audit-link verification; embeddable.
- *Acceptance:* a buyer sees stats reflecting the last 24h with no manual refresh; the badge links to verifiable proof.

**FR-EP — Evidence pack export** (the acceptor artifact). Control-by-control evidence, hash-chain proof, auditor cover sheet, event-ID index, manifest CSV; period filters; control-ID mapping in the auditor's format; Merkle-root proof signed by KMS; auditor portal invite.
- *Acceptance:* a signed zip in ≤60s for 1 year of evidence, mapped to AICPA TSC IDs (configurable to a firm's format). **⚠️ UNVALIDATED until A2** — exact format is auditor-driven.

**FR-SEAM — Read/write credential separation, internally exercised (H2).** SDK creds write; a structurally separate read-credential class is reserved for the future external surface **and is consumed internally in Phase 1 by our own trust page + auditor portal** to validate the interface. **No external read credentials are issuable in V1.**
- *Acceptance:* any non-SDK credential attempting a write is rejected at middleware regardless of scope; our trust page and auditor portal read exclusively through the read-seam in staging by end of Phase 1.

### P1 — Should-have

- **FR-CONF — Agent-specific conformity monitor (scoped per H4; priority per M4).** Continuously evaluate the customer's **agent** evidence against **EU AI Act Art. 19 agent-log retention** and the **agent slice** of SOC 2 — explicitly **not** generic SOC 2 automation. Standing "conformity status" + drift alerts.
  - *Acceptance:* on an agent-evidence retention/control gap, the dashboard shows red and alerts via Slack/email within the configured window. **⚠️ Gated by A1 (is retention demand real?) and A9 (does Art. 19 bind our ICP?).** Do not build before both clear.
- **FR-APR — Approval flow** (HITL on risk/cost/scope; Slack/email/webhook/hosted UI; blocking; recorded).
- **FR-SDK-5 — Local loop/anomaly detection**; **FR-SDK-6 — Redaction policies** (PII/PHI redacted before upload).
- **FR-DSH — Dashboard** (activity, agents, registries, filterable audit log, approvals, anomalies, trust-page settings, exports, questionnaires, frameworks, team, billing; Clerk auth).
- **FR-Q-7 — Customer question library** (compounds the corpus — §10).

### P2 — Future (design-for, don't build)
- **SDK-optional ingestion** (OTel/LangSmith/Helicone) — the brainstorm's "remove the SDK" option, recorded as a real alternative; deferred because it can't yet produce auditor-grade provenance (see FR-SDK-1 rationale).
- Open public read API, OAuth 2.1, MCP server, OSS connectors, open "Agent Compliance Event" schema + standards submission — the deferred ecosystem (`PRD_v0.2.md` §9.9–9.12). Seams kept (FR-SEAM, versioned schemas, webhook primitives).
- Decision-reconstruction API, GDPR DSAR workflow, WORM tier, multi-region EU residency.

---

## 7. Success Metrics (re-derived from the v0.4 thesis, H5)

### Acquisition (leading)
| Metric | Target | Measurement |
|---|---|---|
| Signup → SDK install | < 30 min (p50) | Funnel timestamps |
| Install → first evidence event | < 10 min (p50) | Event pipeline |
| Questionnaire auto-fill coverage | ≥ 70% cited | Per-questionnaire telemetry *(calibrate to A2)* |
| **Deal actually moved after answers (A10)** ⚠️ | qualitative: majority say "yes, faster" | Founder interviews — tests the causal claim |

### Retention (the A1 battleground)
| Metric | Target | Measurement |
|---|---|---|
| Trust pages published | ≥ 30 of first 50 | Trust-page service |
| **Day-60 active usage (no open deal)** ⚠️ | ≥ 60% | Retention cohort — A1 proxy |
| **Logo churn (annualized)** ⚠️ | < 15% | Billing cohort — the true A1 test |

### Acceptance (the A2 battleground)
| Metric | Target | Measurement |
|---|---|---|
| **Evidence packs accepted by an auditor** ⚠️ | ≥ 10 in year 1 | Customer-reported + auditor portal |
| Auditor "preferred format" relationship | 1 (mid-tier ok) | Partnerships |

### Commercial — with explicit tier-mix assumption (H5)
| Metric | Target | Note |
|---|---|---|
| Paying customers (90 days) | 50 | ≥ 80% fintech |
| MRR (90 days) | $10K | **Assumes a Starter-heavy mix (~$200 avg).** If retention/conformity value lands, the strategy *should* pull mix toward Growth ($599) — track **avg revenue/account** as the leading signal that the new thesis is monetizing. |
| Questionnaire corpus (agent-specific) | 200 canonical questions | The defensible slice (§10) |

### Anti-metrics
Total cross-vertical signups; free-tier conversion; feature breadth; integration count.

---

## 8. Product Overview

```
BUYER SEES (V1 surfaces, built):  SDK  ·  Dashboard  ·  Trust Page  ·  Auditor Portal
                                          │
CORE BACKEND: evidence pipeline · control library · corpus · hash-chain · registries
              · questionnaire engine · agent-conformity monitor (P1)
              · auth middleware (write = SDK-only;  read-seam = internally exercised in Ph.1)
                                          ┆ (heavy surface NOT built in V1)
DEFERRED (Phase 3): public read API · OAuth 2.1 · MCP server · OSS connectors
```

**Positioning discipline (C1):** the **buyer headline is the painkiller** ("close the stuck deal"). **"Layer 0"** — Trust0 as the agent-evidence substrate the four security layers reference (`MarketAnalysis` §4.1) — is the **internal category narrative and long game**, used with investors and to guide architecture, **not** as the lead buyer message. In V1 the substrate is expressed only through our own artifacts.

---

## 9. Non-Functional Requirements

- **Performance:** SDK hot-path ≤ 5ms p99 (A6); evidence pack ≤ 60s/yr; trust page ≤ 1.5s p95.
- **Reliability:** 99.9% API uptime (paid); graceful SDK degradation.
- **Security (must be exemplary — we're a security vendor):** **SOC 2 Type I within ~6 months of GA; Type II at ~12 months** (M1 — Type II needs a 6–12mo observation window; the v0.3 "Type II in 6 months" claim was infeasible and would hurt us with the auditors we're courting). Encryption at rest (KMS/CMEK); hash-chained log + WORM tier (paid); per-tenant US/EU residency; employee access MFA'd + audited; public bug bounty within 90 days.
- **Compliance:** GDPR day 1; ISO 27001 target Q2 2027.
- **Scalability:** 1M agent actions/day/tenant; 1,000 tenants in V1.

---

## 10. Defensibility / Moat (made honest, C2)

The SDK is the **wedge + data tap**, not the moat. Ranked by *robustness* (least dependent on unproven scale first):

1. **Auditor-recognized format (most robust).** A "preferred format" relationship with even one respected audit firm makes our evidence the path of least resistance. It doesn't need scale to bite, and it directly de-risks A2. **Invest here first.**
2. **The "Secured by Trust0" badge network effect.** Every live trust page is a billboard + a visible switching cost. Compounds with customer count, but each badge stands alone.
3. **The corpus — conditional, and agent-specific only.** A canonical knowledge base + matching engine + human-edited answers. **Honest caveats the review forced (C2):**
   - It **only compounds if customers stay and the base scales** — i.e., it is *downstream of A1*. If retention is weak, this moat never forms.
   - **Foundation models may erode it:** as LLMs answer security questionnaires from raw evidence directly, a curated answer-corpus depreciates. We bet on the *agent-specific* slice + provenance citations, which raw LLMs can't fabricate — **not** on generic answer text.
   - Incumbents (Vanta/Drata) hold larger *general* SOC 2 corpora; we are only defensible on the **agent** slice.
4. **Cross-customer anonymized evidence patterns** — the true data network effect, but the most scale-dependent; treat as upside, not a V1 claim.

**Sequencing implication:** since we intend to eventually open-source the schema, we must own (1) and (2) *before* doing so — open-sourcing the format while auditor relationships and corpus are weak is self-commoditization (Brainstorm §5; review C1/C2).

---

## 11. Detractors — who would actively resist, and how we answer (M2)

| Detractor | Why they push back | Mitigation |
|---|---|---|
| **The founder (buyer)** | Latency paranoia about an unknown vendor wrapping the LLM hot path | Publish the A6 benchmark; local-first design; redaction off the hot path; test-mode keys; open-source the SDK so the hot path is auditable |
| **The enterprise security reviewer (acceptor)** | Distrust of a tiny vendor *holding their evidence* (`MarketAnalysis` §6.2: a security product must itself be secure) | Our own SOC 2 Type I early (§9); customer-held keys / residency choice; hash-chain they can verify independently; bug bounty |
| **The auditor (acceptor)** | Antipathy to learning yet another vendor's format | Co-design (A2); map to AICPA TSC IDs they already use; "preferred format" partnership makes us their easy path |
| **Incumbent (Vanta/Drata)** | We touch continuous SOC 2 | Stay strictly on the **agent slice** (H4 scoping of FR-CONF); keep the listening-call open for partner-vs-build intel |

---

## 12. Validation Plan — assumptions that gate spec lock ⚠️

Re-ranked to include the assumptions the review found hidden (C3). **Lethal** = if false, the direction breaks. Run before locking §6.

| ID | Assumption | Class | Cheapest test | Pass bar |
|---|---|---|---|---|
| **A1** | Customers keep paying after the first deal closes | Business-model **lethal** | ≥10 design-partner interviews: *"After the deal closed, would you still pay next month? For what?"* | Majority name a continuous reason (trust-page inbound, conformity, next audit) |
| **A2** | Auditors/reviewers accept our evidence as auditor-grade | GTM **lethal** | Show the sample pack (`PRD_v0.1.md` §20 + §22) to **3 auditors + 1 reviewer**; "Would you accept this? What's missing?" | ≥2 auditors accept w/ minor changes; capture format reqs |
| **A7** | "Layer 0 / agent-evidence substrate" is a category buyers value | Positioning **lethal** | In the A1 calls, test *both* messages: painkiller vs. "Layer 0." Which earns the meeting/the card? | Painkiller wins the buyer; Layer 0 reserved for investors |
| **A9** | EU AI Act Art. 19 actually binds our ICP's systems (not just Annex III high-risk) | Retention-anchor **lethal** (promoted from OQ) | One regulatory/legal read + ask in A1 calls whether EU buyers demand it | Clear yes for a meaningful ICP slice — else re-anchor retention |
| **A10** | Better/faster evidence actually moves the deal (vs. procurement-queue latency) | Wedge causal **lethal** | Add to A1/A2 calls: *"When you had good answers, did the deal move — or still sit in their queue?"* | Majority report faster movement attributable to evidence |
| **A8** | The corpus compounds into real defensibility | Moat **high** | Desk test: can a frontier LLM answer 20 sample questions from raw evidence *without* our corpus? | If it can't match our cited/provenanced answers, the agent-slice corpus holds |
| **A6** | SDK hot-path ≤5ms p99 | Feasibility | 2-day spike vs. a real agent loop | p99 ≤ 5ms, else move work off hot path |

> **Gate:** Do not lock §6 P0 acceptance criteria (FR-EP, FR-Q) until **A1, A2, A10** clear. Do not build **FR-CONF (P1)** until **A1 and A9** clear. Do not put "Layer 0" in buyer-facing copy until **A7** clears.

---

## 13. Timeline Considerations

### Phase 0: Validation (Week 0–1) — gates the spec
Run A1, A2, A7, A9, A10 (one interview round covers most — see §12) + the A6 spike + the A8 desk test. One Phase-0 call to sanity-check healthtech as the V2 expansion. **Only then** finalize §6 acceptance criteria.

### Phase 1: V1 wedge + launch retention artifact (Weeks 1–8)
SDK + registries + evidence pipeline + hash chain → questionnaire engine + evidence pack → **trust page (the P0 retention artifact)** + Stripe billing → polish, docs, **dogfood our own SOC 2 (targeting Type I)**. **Exercise the read-seam internally** (trust page + auditor portal read through it — H2). GTM in parallel: design-partner calls, agent-specific knowledge base, **fintech** messaging, Show HN / Product Hunt, outbound to YC AI fintechs. FR-CONF is **not** built here unless A1+A9 cleared in Phase 0.

### Phase 2: Prove PMF + auditor relationship (Months 3–6)
Iterate on first 50; convert the A2 auditor to "preferred format"; grow the agent-specific corpus toward 200; build FR-CONF if its gates cleared; **one listening call** with a Vanta/Drata/Hyperproof product lead (partner-vs-build intel + window calibration — directly informs the H1 bet).

### Phase 3: Ecosystem (post-PMF, deferred) — formerly v1.5
Only after the wedge is proven: public read API, OAuth 2.1, MCP server, OSS connectors, open-schema/standards submission (`PRD_v0.2.md` §9.9–9.12). Because the read-seam was *exercised* in Phase 1 (not just declared), this is genuinely additive.

### Hard dates / dependencies
- **EU AI Act enforcement: Aug 2, 2026** — informs FR-CONF/residency; we don't let one date carry demand (SOC 2 + procurement are evergreen).
- **Auditor co-design (A2) blocks FR-EP.**
- **The 6–12mo window (H1)** is the clock on Phase 3 value — re-calibrated by the Phase-2 listening call.

---

## 14. Out of Scope (V1)
Multi-framework beyond SOC 2 + EU AI Act; customer-authored controls; AI bias/fairness; native chatbot/Copilot; on-prem/VPC/self-hosted; white-label; SDK languages beyond Py+TS; ML-based anomaly detection (rules only); **generic** SOC 2 automation; real-time WebSocket budget streaming; mobile dashboard.

**Deferred (not cancelled) — Ecosystem phase:** public write endpoints (never to external keys — the one permanent rule from v0.2), open read API, OAuth server, MCP server, OSS connectors, standards submission.

---

## 15. Open Questions

1. **[Founder] Brand/positioning** — confirm "Trust0"; confirm painkiller-led messaging with "Layer 0" reserved for investors (A7).
2. **[Founder] V2 expansion vertical** — healthtech (HIPAA) the lead candidate; confirm via Phase-0 call. *(Fintech-for-V1 is now committed, not open — H3.)*
3. **[Product] Retention mechanic if A1 is weak** — trust-page-inbound vs. conformity vs. continuous-audit; which leg do we lean on?
4. **[Eng] OAuth build-vs-buy** — deferred with the ecosystem; not a V1 decision.
5. **[Eng] Bedrock/Vertex SDK timing** — V1 ships Anthropic + OpenAI.
6. **[Founder] Auditor invitation pricing** — bundled in Growth or per-seat?

*(v0.3's OQ #1 "vertical choice" and OQ #2 "Art. 19 applicability" were promoted to a committed bet (H3) and a gating assumption (A9) respectively.)*

---

## 16. Approval

| Stakeholder | Role | Status |
|---|---|---|
| Founder/CEO | Final decision + positioning (A7) + brand | Pending |
| Founding Engineer | Feasibility (V1 architecture + A6 spike + read-seam dogfood) | Pending |
| Compliance Advisor (TBD) | Control library + **A2 auditor reviews** + **A9 regulatory read** | Pending hire / fractional |
| Design Partners (TBD) | **A1 retention + A7 messaging + A10 causality interviews** | Pending |

---

*End of PRD v0.4. **Next action: run §12 (A1, A2, A7, A9, A10) before locking §6.** This document applies `prd-v0.3-review.md`; where it overrode a finding, the changelog says why.*
