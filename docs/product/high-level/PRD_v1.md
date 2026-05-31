# Product Requirements Document — Trust0 v1

| Field | Value |
|---|---|
| **Product Name** | **Trust0** |
| **Buyer-facing tagline** | *Close the enterprise deal that's stuck in AI security review.* |
| **Category narrative (internal)** | The evidence layer for AI agents — "Layer 0" of the agent security stack |
| **Document Version** | 1.0 — the canonical build PRD |
| **Owner** | Founding team |
| **Status** | Draft — MVP scope locked behind Phase-0 validation (§11) |
| **Last Updated** | May 31, 2026 |
| **Target GA (MVP / V1)** | August 2026 |
| **Authoring skill** | `product-management/write-spec` |
| **Consolidates** | `PRD_v0.4.md` (strategy + gates), the `milestones/` component PRDs, and the MVP scope cuts |
| **Supersedes** | `PRD_v0.4.md` as the build doc (v0.4 retained as the fuller strategic target) |

> **What's new in v1 vs. v0.4.** v1 keeps v0.4's validated strategy and gates, then (a) applies an **MVP scope cut** to the P0 set, and (b) introduces a **two-level flow model** — the *overall* product flows (the full vision) and the *MVP* flows (what we build first) — with the **difference called out explicitly** (§6–§8). The MVP is milestones **M0–M3**; the full vision adds **M4–M5**.

---

## 1. Executive Summary

**Trust0 helps fintech AI startups close enterprise deals that stall in AI security review.** A drop-in SDK records every AI agent action with identity, provenance, and tamper-evident proof. That evidence powers the artifacts a founder puts in front of a buyer: an **auto-filled AI security questionnaire**, a live **trust page**, and an auditor-grade **evidence pack**.

This document defines **two levels of scope**:

- **The overall product** (the full vision): acquisition + retention + auditor acceptance + continuous conformity + human oversight + (eventually) an open ecosystem. This is what Trust0 becomes.
- **The MVP** (what we build first): the smallest slice that **acquires a paying fintech customer and tests the lethal assumptions** — the questionnaire wedge, a core trust page, a downloadable evidence pack, and the SDK that feeds them.

The difference between the two is deliberate and documented (§8). We resist building the full vision before the MVP validates that customers pay, retain, and that auditors accept the evidence (§11).

---

## 2. Problem Statement

**User problem.** Every enterprise sales cycle now includes an AI-specific security review (50–200 questions). Fintech AI founders lose 2–6 weeks per deal hand-writing answers, hire $20K+ consultants, stall negotiations with weak responses, and repeat for each customer's annual re-review.

**Two-sided trust.** The **buyer** (founder, self-serve) is not the **acceptor** (enterprise security reviewer + SOC 2 auditor). Value exists only if the acceptor recognizes the evidence as auditor-grade. This is the central GTM risk (assumption A2).

**Causal claim to verify.** The wedge assumes *evidence quality* is the binding constraint on the deal — it might instead be procurement-queue latency (assumption A10).

**Why now.** EU AI Act enforcement (Aug 2, 2026); auditors hardened AI expectations in 2026; procurement institutionalized AI questionnaires; the agent stack standardized on MCP + OAuth 2.1. The competitive window before an incumbent ships agent compliance is an estimated **6–12 months**.

---

## 3. Goals & Non-Goals

### Goals
1. **MVP:** ship the questionnaire wedge + trust page + evidence pack + SDK that acquire a paying fintech customer.
2. Validate the lethal assumptions (§11) **before** locking full scope.
3. Make the evidence **auditor-grade** (cited + tamper-evident) — the differentiator vs. a generic form-filler.
4. Commit to **fintech** as the V1 vertical; healthtech is the V2 expansion candidate.
5. Reach 50 paying fintech customers in 90 days post-launch (tier-mix caveat, §9).

### Non-Goals (V1) — with rationale
| Non-goal | Why |
|---|---|
| Open ecosystem surface (public API, OAuth server, MCP, OSS connectors, standards body) | Strategy outrunning evidence; deferred to M5/post-PMF. |
| Generic SOC 2 automation (policies/training/scans) | Incumbent turf; we stay on the **agent slice**. |
| Multi-framework beyond SOC 2 + EU AI Act | Focus; HIPAA arrives with healthtech (V2). |
| Customer-authored controls; on-prem/VPC/white-label; CISO sales motion | Wrong scope or buyer for V1. |
| Treating the SDK as the moat | SDK = wedge + data tap; moat = auditor-format + badge + agent-corpus. |

---

## 4. User Stories (by persona)

### Buyer — the fintech AI founder / eng lead (pays)
- As a founder, I paste my buyer's questionnaire and get evidence-cited answers in minutes, so I stop losing deals to slow procurement.
- As an eng lead, I install an SDK in <30 min and see runtime evidence immediately, so I can validate before paying.
- As a founder, I want a live trust page so inbound buyers arrive pre-qualified and I keep getting value between deals.

### Acceptor — auditor & enterprise security reviewer (decides, doesn't pay)
- As a SOC 2 auditor, I want evidence mapped to control IDs I recognize, with tamper-evident proof, so I accept it without a custom process.
- As an enterprise reviewer, I want to self-serve and verify a vendor's trust page, so I clear the gate faster.

### Operator — eng lead / CTO (full vision)
- As an eng lead, I register models/vendors once, so my team doesn't think about compliance on every change.
- As a CTO, I want continuous conformity + human approval on risky actions, so compliance is a standing state and audits aren't fire drills.

---

## 5. (intentionally merged into §6–§8 — flows follow)

---

## 6. User Flows — OVERALL (the full vision)

These are the end-to-end journeys Trust0 supports at full build. Each is tagged with the milestone that delivers it.

**OF-1 · Install → first evidence** *(M1)*
Sign up → onboarding wizard captures company/vertical/providers → auto-creates registry entries → paste SDK snippet → first evidence event in <30s → trust page auto-published.

**OF-2 · Stalled deal → auto-filled questionnaire → export** *(M3)* — the wedge
Upload questionnaire (SIG/CAIQ/Word/PDF/CSV) → parse + classify → auto-fill from evidence with citations → gaps flagged with a 30-min fix plan → human edit → export branded PDF/DOCX/original → saved to a reusable library.

**OF-3 · Publish & maintain trust page** *(M3)* — retention
Trust page live from runtime evidence across ~10 sections → "Secured by Trust0" badge with verify link → gated sections for sensitive evidence → embeddable badge on the customer's site.

**OF-4 · Stay continuously conformant** *(M4, gated)* — retention core
Trust0 continuously evaluates agent evidence against EU AI Act Art. 19 retention + the agent slice of SOC 2 → standing conformity status → drift alerts via Slack/email.

**OF-5 · Human approval on a risky action** *(M4)* — oversight
Agent hits a trigger (cost/scope/data-category) → SDK blocks → approver decides via Slack/hosted UI → decision recorded as evidence.

**OF-6 · Audit time → auditor portal → evidence pack** *(M3 pack + M4 portal)* — acceptance
Founder invites auditor by email → auditor SSOs into a read-only portal → selects period/framework → generates a signed evidence pack → re-queries events without re-asking the customer.

**OF-7 · GRC tool / auditor reads via open API or MCP** *(M5, deferred)* — ecosystem
A connected GRC tool (Vanta/Drata) or an auditor's AI assistant reads Trust0 evidence through the public API / MCP server under "Open Reads, Closed Writes."

---

## 7. User Flows — MVP (what we build first)

The MVP is the smallest set of flows that **acquires a paying customer and tests the lethal assumptions**. It corresponds to milestones **M0–M3**.

**MVP-F1 · Install → first evidence** *(lean OF-1)*
Sign up → declare models + vendors (simple inventory) → paste **Python** SDK snippet (Anthropic; OpenAI fast-follow) → first evidence event in <30s.

**MVP-F2 · Stalled deal → auto-fill → export** *(lean OF-2)* — **the core wedge**
Paste questionnaire (text or one format, e.g. PDF) → auto-fill from evidence with **citations** → human edit → export PDF. *(This is the demo that acquires and the test of A10.)*

**MVP-F3 · Publish trust page** *(lean OF-3)* — retention signal
Auto-published trust page with **core sections** (agent/model inventory, frameworks, live stats) + **"Secured by Trust0" badge** with verify link.

**MVP-F4 · Audit time → download evidence pack** *(lean OF-6)* — acceptance
Founder selects period/framework → downloads a **signed evidence-pack zip** (hash-chain proof) → **hands it to their auditor directly** (no portal).

> **Not in the MVP:** OF-4 (continuous conformity), OF-5 (approval flow), the **portal** half of OF-6, and OF-7 (ecosystem) — see §8 for why.

---

## 8. The DIFFERENCE — Overall vs. MVP (read this)

The MVP is the full vision with the *scale, breadth, and future-proofing* removed — but **never** the two differentiators (cited answers + tamper-evidence). Cuts are reversible and scheduled, not abandoned.

### 8.1 Flow-level difference

| Flow | Overall (full vision) | MVP | What's deferred & why |
|---|---|---|---|
| Install (OF-1/F1) | 4 providers; auto-built registries with versioning/approval | 1–2 providers (Python-first); declared model+vendor inventory | Bedrock/Vertex + the CC8 versioning machinery are audit-maturity, not needed to demo |
| Questionnaire (OF-2/F2) | All formats; ranked matches; auto fix-plans; corpus feedback loop | Paste/1 format; fill + cite + export | Multi-format parsing & fix-plan automation are a long tail; add on demand |
| Trust page (OF-3/F3) | ~10 sections; gated sections; embeddable badge | Core sections + verifiable badge | Long-tail sections are fillers; add per customer request |
| Conformity (OF-4) | Continuous Art. 19 + SOC 2 drift monitoring | **Not built** | Gated by A1 (retention demand) + A9 (Art. 19 applicability) — unproven |
| Approval (OF-5) | HITL gating + recorded decisions | **Not built** | Safety/maturity feature; wedge ships without it |
| Audit (OF-6) | Evidence pack **+ auditor portal** | Evidence pack **zip only** | A2 is validated with a *sample* pack; portal isn't needed to acquire or to test acceptance |
| Ecosystem (OF-7) | Public API / OAuth / MCP / connectors | **Not built** | Premature platform-building pre-PMF |

### 8.2 The principle behind the cuts
- **Test the lethal assumptions with research, not code.** A1 (retention) and A2 (auditor acceptance) are validated by interviews + a *sample* evidence pack — **zero build** (§11). So the MVP build targets the **wedge** (acquire + test A10), not completeness.
- **Keep the two differentiators intact.** Evidence-**cited** answers and **tamper-evident** proof are what make Trust0 "auditor-grade" rather than "a nicer form." Their *implementation* is simplified (app-level hash chain; defer Merkle/KMS), but they are never cut from scope.
- **Defer future-proofing of deferred layers.** The formal read-seam exists to de-risk the ecosystem (M5) — so building it now is premature. MVP keeps the cheap **write = SDK-only** guard and lets internal surfaces read directly.

### 8.3 Lean architecture for the MVP (build note)
Collapse the v0.2 stack to a founder-sized system: **one Postgres** (events in a partitioned/JSONB table — defer ClickHouse), **a Postgres-backed worker** (defer SQS), **app-level SHA-256 hash chain** signed with a managed secret (defer Merkle + KMS), **one region**, **Python SDK first**, deployed as **one monolith + one worker** on Fly/Railway. Keep managed Clerk + Stripe + S3/R2.

---

## 9. Functional Requirements (P0-MVP / P1 / P2)

Detailed specs carry forward from the `milestones/` component PRDs and `PRD_v0.4` §6.

### P0 — MVP must-haves
**FR-SDK-1 — One-line Python wrapping** (Anthropic; OpenAI fast-follow).
- *Acceptance:* replacing the client constructor yields evidence in <30s, zero other code changes.

**FR-SDK-3 — Per-call capture** incl. input/output **hashes**, model/vendor refs, cost, latency, timestamps.
- *Acceptance:* a completed call records all fields, linked to its session.

**FR-INV — Declared inventory** of Models + Vendors (lean registry; no versioning DAG/approval in MVP).
- *Acceptance:* a call to an undeclared model flags evidence "not auditor-grade" until declared.

**FR-CTL — Control library + mapping** (54 controls; agent slice tagged; AICPA TSC default).
- *Acceptance:* each control resolves to an evidence query; status cites the satisfying event IDs.

**FR-Q — Questionnaire auto-fill (lean)** — paste/one format → classify → fill with **citations** → edit → export PDF.
- *Acceptance:* ≥70% of questions get a cited candidate answer *(target pending A2)*.

**FR-TP — Trust page (core)** — public URL, core sections, live from evidence, **verifiable badge**.
- *Acceptance:* stats reflect the last 24h with no manual refresh; badge links to verifiable proof.

**FR-EP — Evidence pack zip** — control-by-control evidence, **hash-chain proof**, cover sheet, manifest; period filters; **no portal**.
- *Acceptance:* a signed zip in ≤60s for 1 year of evidence, mapped to TSC IDs *(format pending A2)*.

**FR-AUTHZ — Write = SDK-credential-only** (middleware guard) + Clerk dashboard auth + Stripe billing + a minimal "first event / keys / billing" dashboard.
- *Acceptance:* any non-SDK credential attempting a write is rejected at middleware.

### P1 — Fast-follow (post-validation)
- **FR-CONF** — continuous agent-conformity monitor *(gated by A1 + A9)*.
- **FR-APR** — approval flow (HITL).
- **FR-EP-PORTAL** — auditor portal (invite, read-only seats, saved queries).
- **FR-REG-FULL** — Prompt + Guardrail registries; versioning/approval/eval-gate workflow.
- **FR-Q-FULL** — multi-format parsing, ranked matches, fix-plan automation, corpus feedback loop, reusable library.
- **FR-TP-FULL** — incident/change logs, approval stats, gated sections, embeddable badge.
- **FR-SDK-TS** — TypeScript SDK; **FR-SDK-5/6** — loop/anomaly detection + redaction.
- **FR-DSH** — rich dashboard.

### P2 — Future (design-for, don't build)
- SDK-optional ingestion (OTel/LangSmith); the open ecosystem (public API/OAuth/MCP/connectors/schema/standards); Merkle batching + KMS/HSM signing; multi-region EU residency; ClickHouse/SQS at scale.

---

## 10. Success Metrics

### Acquisition (leading)
| Metric | Target |
|---|---|
| Signup → SDK install (p50) | < 30 min |
| Install → first evidence (p50) | < 10 min |
| Questionnaire auto-fill coverage | ≥ 70% cited |
| **Deal moved after answers (A10)** ⚠️ | majority "yes, faster" (interviews) |

### Retention (A1 battleground)
| Metric | Target |
|---|---|
| Trust pages published | ≥ 30 of first 50 |
| **Day-60 active (no open deal)** ⚠️ | ≥ 60% |
| **Logo churn (annualized)** ⚠️ | < 15% |

### Acceptance (A2 battleground)
| Metric | Target |
|---|---|
| **Evidence packs accepted by an auditor** ⚠️ | ≥ 10 in year 1 |
| Auditor "preferred format" relationship | 1 (mid-tier ok) |

### Commercial (tier-mix caveat)
| Metric | Target | Note |
|---|---|---|
| Paying customers (90 days) | 50 | ≥ 80% fintech |
| MRR (90 days) | $10K | Assumes Starter-heavy (~$200 avg); track **avg revenue/account** as the signal the retention thesis monetizes |

### Anti-metrics
Total cross-vertical signups; free-tier conversion; feature breadth; integration count.

---

## 11. Milestones & Sequencing

**MVP = M0–M3. Full vision adds M4–M5.** Milestones sequence by dependency; calendar mirrors `PRD_v0.4` §13. Detailed per-component scope lives in `../milestones/`.

| Milestone | Theme | Scope level | Delivers flows | Calendar | Gate |
|---|---|---|---|---|---|
| **M0** | Validation | MVP prerequisite | (research — no build) | Week 0–1 | A1, A2, A7, A9, A10, A6 |
| **M1** | Evidence foundation | MVP | MVP-F1 | Weeks 1–2 | M0 |
| **M2** | Compliance core | MVP | (enables F2/F4) | Weeks 3–4 | M1 |
| **M3** | Wedge launch | **MVP complete** | MVP-F2, F3, F4 | Weeks 5–8 | M2 + A2 |
| **M4** | Retention & oversight | Full vision | OF-4, OF-5, OF-6 portal | Months 3–6 | M3 + (A1 & A9 for conformity) |
| **M5** | Ecosystem | Full vision | OF-7 | Post-PMF | PMF proven |

**Critical path to MVP launch:** `01 SDK → 02 lean pipeline → 04 control library → (05 questionnaire, 07 pack-zip) → 08 auth/billing`. Trust page (06) parallelizes; lean inventory (03) sits in M2.

**M0 details (do this before locking P0):** run the A1/A2/A7/A9/A10 interviews + sample-pack auditor reviews + the A6 SDK spike. Only then finalize §9 acceptance criteria.

---

## 12. Validation Plan — gates (from PRD_v0.4 §12)

| ID | Assumption | Class | Cheapest test | Gates |
|---|---|---|---|---|
| **A1** | Customers keep paying after the first deal | lethal | ≥10 design-partner interviews | FR-CONF; the retention thesis |
| **A2** | Auditors/reviewers accept the evidence format | lethal | sample pack → 3 auditors + 1 reviewer | FR-EP, FR-Q format |
| **A7** | "Layer 0" is a buyer category | lethal | test painkiller vs. Layer-0 message in A1 calls | buyer-facing copy |
| **A9** | EU AI Act Art. 19 binds our ICP | lethal | legal read + EU-buyer demand check | FR-CONF Art. 19 leg |
| **A10** | Better evidence actually moves the deal | lethal | ask in A1/A2 calls | the wedge promise (FR-Q) |
| **A6** | SDK ≤5ms p99 | feasibility | 2-day spike | FR-SDK-4 design |

> **Gate:** don't lock §9 P0 acceptance criteria (FR-Q, FR-EP) until A1 + A2 + A10 clear. Don't build FR-CONF until A1 + A9 clear. Don't put "Layer 0" in buyer copy until A7 clears.

---

## 13. Open Questions
1. **[Founder]** Confirm painkiller-led messaging; "Layer 0" reserved for investors (A7).
2. **[Founder]** V2 expansion vertical — healthtech (confirm via a Phase-0 call).
3. **[Product]** Retention mechanic if A1 is weak — trust-page-inbound vs. conformity vs. continuous-audit.
4. **[Eng]** First questionnaire format to support (PDF vs. paste-text vs. CSV).
5. **[Eng]** OpenAI SDK timing relative to Anthropic.
6. **[Founder]** Auditor invitation pricing (when the portal lands).

---

## 14. Out of Scope (V1)
Multi-framework beyond SOC 2 + EU AI Act; customer-authored controls; AI bias/fairness; on-prem/VPC; white-label; ML anomaly detection; generic SOC 2 automation; mobile dashboard. **Deferred (not cancelled):** external write endpoints (never to external keys), the open ecosystem, Merkle/KMS, multi-region.

---

## 15. Approval

| Stakeholder | Role | Status |
|---|---|---|
| Founder/CEO | Final decision + positioning (A7) | Pending |
| Founding Engineer | Lean-architecture feasibility + A6 spike | Pending |
| Compliance Advisor (TBD) | A2 auditor reviews + A9 regulatory read | Pending |
| Design Partners (TBD) | A1 retention + A10 causality interviews | Pending |

---

*End of PRD v1. **Next action: run M0 (§11/§12) before locking the §9 P0 criteria.** MVP = M0–M3; full vision adds M4–M5.*
