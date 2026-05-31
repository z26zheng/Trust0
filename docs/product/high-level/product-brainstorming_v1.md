# Product Brainstorming — Trust0 (v1)

| Field | Value |
|---|---|
| **Working product name** | Trust0 *(evolves the `TrustAI` placeholder from the PRDs)* |
| **Purpose** | Fine-tune the AgentSecurity product direction before locking a `PRD_v0.3` |
| **Inputs** | `MarketResearch/AgentSecurity/MarketAnalysis.md`, `PRD_v0.1.md`, `PRD_v0.2.md` |
| **Mode** | Strategy Exploration + Assumption Testing (with Solution Ideation) |
| **Date** | May 31, 2026 |
| **Status** | Thinking artifact — generates options, not decisions |

> This is a brainstorm, not a spec. It is deliberately opinionated and adversarial to the current plan. The goal is to find the weak points and the sharper wedge *before* engineering starts — not to validate what's already written.

---

## 0. The one-line provocation

**v0.1 was a knife. v0.2 turned it into a Swiss Army platform before anyone proved the knife cuts.** The single most important question this brainstorm should resolve: *are we sharpening a wedge, or are we decorating a vision?*

---

## 1. Frame

**What we're exploring:** Whether Trust0's wedge, buyer, and moat are the sharpest available read of the market — and where the current PRDs have drifted from the evidence.

**Why now:**
- Spec is *not* locked; this is the cheapest moment to change direction.
- The market window is closing fast — `MarketAnalysis` documents active consolidation ($96B M&A), a free Microsoft baseline, and 20+ funded vendors. Tempo matters (this is an OODA market, not a deliberation market).
- v0.2 nearly **doubled the surface area** (public API, OAuth 2.1 server, MCP server, OSS connectors, standards-body engagement) *before a single paying customer exists*. That is the classic moment to stop and re-frame.

**What we already know (from the three docs):**
- The market is real, urgent, and **explicitly not greenfield**. The research's own verdict for a solo/small team: win only via a *narrow, developer-facing, OSS-friendly* wedge — and **avoid building a platform** that competes with Microsoft + the funded startups.
- v0.1 picked a genuinely good wedge: **runtime evidence → questionnaire auto-fill → trust page → SOC 2 evidence pack**, sold to fintech AI founders (card-swipe buyer, not CISO).
- v0.2 kept that and layered an **"Open Reads, Closed Writes" ecosystem doctrine** on top, reframing Vanta/Drata/SafeBase from competitors to channels.

**Constraints (the honest ones):**
- Founding team, ~$0 vs competitors' $50–200M. Extreme asymmetry.
- Security product → the trust bar on our *own* posture is brutal.
- The buyer self-serves, but the *value* is only realized if a third party (enterprise procurement / auditor) **accepts the evidence**. That two-sidedness is underweighted in both PRDs.

**What a great outcome from this session looks like:** a sharpened wedge, a renamed/positioned product, and a ranked list of the 2–3 assumptions that would kill us — each with the cheapest possible test, runnable *this week*.

---

## 2. Reframing the buyer (JTBD)

Before generating options, get the job right. The PRDs describe the job as *"auto-fill my security questionnaire."* That's the **task**, not the **job**.

| Job layer | What the fintech founder is actually hiring Trust0 for |
|---|---|
| **Functional** | "Get *this specific* stalled enterprise deal unblocked **this week**." |
| **Emotional** | "Stop feeling exposed and amateur in front of a buyer 50x my size." |
| **Social** | "Look enterprise-ready to my buyer *and* to my board." |
| **Fired to hire us** | The $20K consultant, 2–6 weeks of founder time, the half-finished spreadsheet, the deal-slipping-a-quarter. |

**The trap hiding in plain sight:** the functional job is **episodic** — it spikes during a deal and *subsides the moment the deal closes*. The PRD rates "customers cancel after closing one deal" as **High risk**, then answers it with asserted retention features (annual contracts, always-on trust page). That's a pricing patch on a product-shaped problem.

**Insight:** retention has to attach to a *continuous* job, not the episodic one. Candidate continuous jobs that already exist in the market:
- "Stay **audit-ready** year-round" (SOC 2 has shifted to continuous monitoring).
- "Prove **EU AI Act Article 19** conformity" — which is literally a *6-month rolling retention mandate*, i.e. continuous by law (the strongest forcing function in the whole `MarketAnalysis`).
- "Keep my **trust page live** so inbound enterprise deals arrive pre-qualified" — turns compliance from cost center into pipeline.

> If Trust0's retention anchor is the questionnaire engine, we will churn. If it's continuous conformity + an inbound-generating trust page, we might not. **This should change which feature we call "the core."**

---

## 3. Diverge — seven distinct wedges

Generated along varied dimensions (buyer, artifact, episodic vs. continuous, SDK depth, GTM). Including one "do the opposite" and one "remove something." No judgment yet.

1. **The Deal-Unblocker** *(v0.1, sharpened).* Questionnaire auto-fill is the hero. Sell acute pain, high willingness-to-pay, self-serve. Risk: episodic churn.
2. **The Always-On Conformity Layer** *(retention-first).* Lead with continuous EU AI Act + SOC 2 monitoring and a live trust page; questionnaire becomes a *feature* of the evidence, not the headline. Bets the whole company on continuity.
3. **The Audit-Trail Compliance SaaS** *(MarketAnalysis Option B, pure).* "EU AI Act audit compliance in 2 lines of code — every agent action signed, queryable, retention-compliant." Regulation-forced demand, least dependent on sales theater.
4. **The Auditor-Side Wedge** *(do the opposite).* Don't sell to the company being audited — **arm the auditors** (Delve, Schellman, A-LIGN, eventually Big 4). They bring their whole client book. Flips GTM from one-at-a-time founders to channel-led. Slower start, much steeper distribution curve.
5. **"Evidence, not SDK"** *(remove something).* Cut the deep runtime SDK from V1. Ingest evidence from what teams *already* run — OTel traces, LangSmith/Helicone, cloud logs — and do the control-mapping + auto-fill + trust page on top. Kills the #1 adoption friction; weakens the moat. Forces the question: *is the SDK actually load-bearing for the wedge, or for the moat?*
6. **Layer 0 / MCP-native compliance** *(10x ambition).* Position as the **substrate** the other four security layers reference, exposed natively as an MCP tool every agent and auditor can call. The futuristic bet from v0.2's §9.11 — but as the *center*, not a side quest.
7. **Vertical-deep, not horizontal** *(10x focus).* Pick ONE fintech sub-vertical (e.g., AI agents in lending/underwriting) and own its *entire* compliance surface — including the human-process controls. Defensible via domain depth the horizontal players won't match.

---

## 4. Organizing the options (Opportunity Solution Tree)

```
DESIRED OUTCOME: Fintech AI teams close enterprise deals without compliance becoming the bottleneck — and keep paying after.
│
├── OPP A: "My deal is stalled on a security review" (acute, episodic) — STRONGEST evidence in PRDs
│   ├── Sol A1: Questionnaire auto-fill (Wedge 1)        → Exp: 10 founders paste a real questionnaire; measure % auto-filled + time saved
│   └── Sol A2: Auditor-side pull (Wedge 4)              → Exp: 1 mid-tier audit firm pilots our evidence format with 3 clients
│
├── OPP B: "I must stay conformant continuously" (EU AI Act, continuous SOC 2) — STRONGEST retention story
│   ├── Sol B1: Always-on conformity layer (Wedge 2)     → Exp: do 3 design partners keep the dashboard open on day 60?
│   └── Sol B2: 2-line audit trail (Wedge 3/5)           → Exp: ingest one partner's existing traces; produce a retention-compliant log
│
└── OPP C: "Compliance tooling is fragmented; nothing connects" (the v0.2 thesis) — WEAKEST near-term evidence
    ├── Sol C1: Open API + connectors (v0.2 ecosystem)   → Exp: NONE YET — this is a belief, not an observation
    └── Sol C2: Layer-0 / MCP substrate (Wedge 6)        → Exp: would any auditor actually query via MCP in 2026?
```

**What the tree exposes:** OPP A and OPP B are grounded in evidence from the research and the founder pain. **OPP C — the entire v0.2 expansion — has no experiment attached because it rests on an unvalidated belief about how incumbents will behave.** That's the tell.

---

## 5. Provoke — the assumptions that can kill us

Ranked by lethality. For each: the claim, the challenge, and the *cheapest test runnable now*.

### A1 — Episodic churn *(business-model lethal)*
- **Claim:** "Customers retain after their first deal closes."
- **Challenge:** The core job is per-deal. Nothing in the product makes day-60 valuable when no deal is active. Annual contracts hide churn; they don't prevent it.
- **Cheapest test:** Interview the existing design-partner pipeline: *"After you closed the deal, would you still pay next month? For what?"* If the honest answer is "the trust page maybe," the retention thesis is unproven — redesign around OPP B before building.

### A2 — Two-sided evidence acceptance *(go-to-market lethal, and external)*
- **Claim:** Auditors and enterprise procurement will accept Trust0's evidence pack as auditor-grade.
- **Challenge:** The buyer (founder) is not the acceptor (auditor/procurement). If the acceptor shrugs, the founder's pain isn't solved and they churn *and* tell others. The PRD *plans* auditor co-design but hasn't done it.
- **Cheapest test:** Put the sample Evidence Pack (already drafted in `PRD_v0.1.md` §20 + the §22 schema) in front of **3 real SOC 2 auditors** and one enterprise security reviewer. Ask: "Would you accept this? What's missing?" This is external, cheap, and the single highest-information action available. **Do it before locking the spec.**

### A3 — "The SDK is the moat" *(strategy-incoherent)*
- **Claim (v0.2 §11.5):** "SDK install is the sole path to evidence creation" = the moat.
- **Challenge:** Wrapping `anthropic`/`openai` clients is a *days-long* engineering task, not a moat. "Closed Writes" protects our API from external writes — but it does **nothing** to stop Vanta from shipping *their own* SDK to *their own* backend once they see this work. And v0.2 simultaneously **open-sources the event schema** and pushes it to a standards body — deliberately making the format non-proprietary. **You cannot call the SDK+schema your moat while open-sourcing the schema.** These two doctrines contradict.
- **Where the moat actually lives:** (1) the **corpus** — the canonical question knowledge base + matching engine + polished answers that compound with every customer; (2) **auditor-recognized "preferred format" status** (a Big 4 / Schellman endorsement is a real moat); (3) the **"Secured by Trust0" badge** as a brand network effect — every trust page is a billboard; (4) **cross-customer anonymized evidence patterns** improving auto-fill — *that's* the real data network effect, not the SDK.
- **Cheapest test:** none needed — this is a positioning correction. Rewrite the moat narrative around corpus + auditor trust + badge, and invest there *first*.

### A4 — "Competitors become channels" *(the optimistic core of v0.2)*
- **Claim:** Vanta/Drata/SafeBase integrate Trust0 rather than build or buy.
- **Challenge:** Incumbents with $50–200M and customers actively demanding a capability **build or acquire** far more often than they integrate a tiny vendor into their core surface. The likeliest move: Vanta acquires a runtime-observability player (Laminar, Geordie) and bolts on AI compliance in ~6 months. The realistic strategic asset isn't "partnership" — it's the **6–12 month window** before they do.
- **Cheapest test:** One exploratory call with a Vanta/Drata/Hyperproof product lead. Are they thinking "partner" or "build"? (Bonus: the answer also tells you how much runway the window has.)

### A5 — "Fintech is the right vertical"
- **Claim:** Fintech first.
- **Challenge:** Reads as founder-familiarity, not evidence. Healthtech (HIPAA) and the EU AI Act high-risk list arguably carry *harder* legal forcing functions. Why fintech specifically?
- **Cheapest test:** Compare 3 fintech vs 3 healthtech founders on one question — "what happens to your deal in 30 days without this?" Pick the vertical with the most acute, most frequent pain.

### A6 — "0ms hot path while wrapping every call + redaction + loop detection locally"
- **Claim:** SDK adds ≤5ms p99.
- **Challenge:** Feasibility, not strategy — but if false, the "5-minute frictionless install" promise breaks.
- **Cheapest test:** A 2-day SDK spike against a real agent loop. Measure p99 honestly.

### Inversion pass — "How would we *guarantee* Trust0 becomes invisible, commoditized plumbing?"
Run the reverse-brainstorm; each item is a self-inflicted risk **already present in v0.2**:
- Open-source the schema so anyone can implement it. *(v0.2 does this.)*
- Make all reads free and open so integrators capture the customer relationship. *(v0.2 does this.)*
- Let partners put their brand on the consent/UX surface. *(v0.2 guards against this — good, keep it.)*
- Hinge demand on a single regulatory date. *(Partially mitigated — keep SOC 2 + procurement as evergreen drivers.)*
- Build broad (APIs, MCP, connectors) before proving the wedge. *(v0.2's central risk.)*

**Reversing those gives the guardrails:** keep the corpus closed, keep the badge on every page, own the auditor relationship, diversify demand drivers, and **sequence breadth after PMF.**

---

## 6. Converge — the sharpened direction

My opinionated read. The brainstorm generates options; this is the one I'd defend.

**1. Rename and reposition as `Trust0`.** The workspace already says it. Lean in — it resolves Open Question #1 from both PRDs and it's *better* than "TrustAI":
- **"Trust-Zero"** → zero-trust security posture applied to AI agents. Native to the security buyer's vocabulary.
- **"Layer 0"** → the foundational *evidence substrate* beneath the four security layers in `MarketAnalysis` §4.1. Identity, gateway, runtime, and governance tools all need a trustworthy event record — Trust0 is the layer they reference. That's a category-defining line, and it doesn't require building their products.
- Positioning candidate: **"Trust0 — the evidence layer for AI agents. Layer 0 of the agent security stack."**

**2. Cut the v1.5 ecosystem out of the critical path.** *Architect* for open reads (cheap, keep the clean read/write separation) — but do **not** build the OAuth server, MCP server, OSS connectors, or standards-body submission before PMF. The `MarketAnalysis` explicitly warned a small team against platform-building; v0.2 quietly re-platformized. Keep ecosystem as a **Year-2 investor narrative**, not a Weeks 12–20 build.

**3. Make the wedge "Deal-Unblocker that *installs* an Always-On layer."** Acquire on the acute pain (questionnaire auto-fill — the painkiller), but design **first-run** to stand up the continuous artifacts (live trust page + conformity monitoring) so retention is structural, not a pricing trick. Attach retention to OPP B (continuous EU AI Act / SOC 2), not to questionnaires.

**4. Move the moat investment to corpus + auditor trust + badge.** Stop describing the SDK as the moat. The SDK is the *wedge and the data tap*. Spend the scarce founder hours on the question corpus and on locking 1–2 auditor "preferred format" relationships early.

**5. Sequence with OODA, not a Gantt chart.** Two external, lethal assumptions (A1 retention, A2 auditor acceptance) are cheap to test and gate everything. *Orient with what we have, test those two this week, then decide the spec.* Don't out-deliberate a market that's consolidating in real time.

### Top 3 to pursue, with the biggest unknown + cheapest resolution

| Direction | Biggest unknown | Cheapest way to resolve |
|---|---|---|
| **Deal-Unblocker wedge (sharpened v0.1)** | Will auditors accept the evidence? (A2) | Show the sample pack to 3 auditors this week |
| **Always-On conformity as the retention anchor (OPP B)** | Is day-60 valuable without a live deal? (A1) | "Would you still pay next month?" interviews |
| **Auditor-side channel (Wedge 4)** | Will one firm pilot our format? | One pilot conversation with Schellman/A-LIGN/Delve |

---

## 7. Capture

### Key reframes (the takeaways)
- The job is **"unblock this deal,"** but the *business* lives or dies on attaching to a **continuous** job (conformity), not the episodic one.
- The wedge is healthy; **the v0.2 ecosystem is strategy outrunning evidence** — defer it.
- **The SDK is not the moat.** Corpus + auditor-recognized format + badge network effect are.
- **Trust0 = "Layer 0," the evidence substrate** the four security layers reference — a sharper category than "AI compliance tool."

### Assumptions to test (ranked, all cheap, all this week)
1. Post-deal retention behavior (A1) — interviews.
2. Auditor/procurement acceptance of the evidence format (A2) — 3 auditor reviews. **Highest information per hour.**
3. Incumbent intent: partner vs. build (A4) — 1 product-lead call.
4. Vertical choice: fintech vs. healthtech pain (A5) — 6 founder calls.
5. SDK hot-path overhead (A6) — 2-day spike.

### Questions that need *research*, not brainstorming
- What exact evidence artifacts do SOC 2 auditors accept for AI agents *today* (vs. what we imagine)?
- Does EU AI Act Article 19 retention actually apply to our ICP's systems, or only Annex III high-risk? (Determines whether the continuous-conformity anchor is real.)
- Is anyone already piloting "auditor queries compliance via MCP," or is that purely speculative for 2026?

### Suggested next steps
1. Run the two lethal tests (A1, A2) before any spec work.
2. Draft `PRD_v0.3` that: adopts the Trust0 / Layer-0 positioning, **demotes v1.5 ecosystem to a future appendix**, makes continuous conformity the retention core, and rewrites the moat section.
3. Lock the brand and the one-line positioning.

### Explicitly parked (good ideas, not now)
- Open public API, OAuth 2.1 server, MCP server, OSS connectors, AICPA/NIST standards submission — **keep the architectural seams, defer the build to post-PMF.**
- Strategic partnerships with Vanta/Drata/SafeBase — worth *one* listening call now (intel), not a roadmap commitment.
- Multi-framework breadth (HIPAA/FINRA/ISO 42001) — V2, unless the vertical test flips us to healthtech.

---

*End of Product Brainstorming v1. This document is meant to be argued with. Next: run the A1/A2 tests, then fold the survivors into `PRD_v0.3`.*
