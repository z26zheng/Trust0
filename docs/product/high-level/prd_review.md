# PRD Review — The Problem-Space Question

| Field | Value |
|---|---|
| **Purpose** | Step back from scope/architecture and confront the prior question: *what specific scenario are we actually solving?* |
| **Trigger** | Founder observation: with AI, building is fast; the genuine ambiguity is in the **problem/domain space**, not the implementation. "Vanta just does SOC 2 — what's our equivalent crisp scenario?" |
| **Applies to** | All Trust0 PRDs (`PRD_v0.4.md`, `PRD_v1.md`, `milestones/`) |
| **Context** | Lean team: 1–3 people |
| **Status** | Open decision — requires a founder call (see §7) |
| **Date** | May 31, 2026 |

> This is the highest-leverage decision on the table. Scope, architecture, and milestones are all downstream of it. None of the prior PRDs resolved it; they refined *how* to build before settling *exactly what scenario* we solve.

---

## 1. The core diagnosis: building is no longer the bottleneck

With AI, you can build an SDK, a pipeline, a questionnaire engine, a trust page in days. That **inverts the risk**: when building is cheap, the danger is building the *wrong specific thing* quickly and confidently.

So the vagueness the founder is sensing is not a detail to tidy up later — **it is the unresolved core question.** Effort spent sharpening the problem now is worth more than any amount of build speed.

---

## 2. The specific failure in our own docs

Every Trust0 document so far defines the product by its **mechanism** or its **strategy**, never by a **bounded scenario in the customer's words**:

- "Runtime evidence layer for AI agents"
- "Layer 0 — the substrate other tools reference"
- "Agent compliance evidence"

Those are how *we* think about it. They are not how a buyer describes a problem they have. The tell: nobody describes Vanta as "a continuous controls-evidence aggregation substrate." They say **"get your SOC 2 done."** Trust0 has been avoiding that one plain sentence — and that avoidance *is* the ambiguity.

---

## 3. Why Vanta is crisp (and we are not)

Vanta's scenario has four properties Trust0 currently lacks:

| Property | Vanta | Trust0 today |
|---|---|---|
| **A named framework** buyers already search for | SOC 2 | "AI agent compliance" — not yet a named, searched thing |
| **An existing budget line** | Audit + compliance tooling | New category → no pre-existing budget |
| **A recurring, dated trigger** | The annual audit; a deal requiring the report | Mixed (a deal event, a regulation date) — inconsistent |
| **A specific painful task** | Stop screenshotting AWS configs; auto-collect evidence | Spread across SDK + questionnaire + trust page + conformity |

**Root cause:** *"AI agent compliance" is not yet a named, budgeted, searched category.* That is simultaneously the **opportunity** (category creation) and the **source of the vagueness** (no existing demand to attach to). We've been covering the gap with positioning language instead of confronting it.

---

## 4. The fix: commit to ONE concrete scenario

The ambiguity dissolves the moment we pick **one user × one moment × one named outcome** and let everything else be "later." A concrete scenario decides — in one stroke — the framework, the buyer, the first demo, the first feature, and the metrics.

---

## 5. Three concrete candidate scenarios

These are **three different companies**, not three features. Choosing among them is the strategic act.

### Scenario A — "The AI controls in your SOC 2 / security review"
- **Who/when:** a Series A–B company already doing SOC 2 ships AI agents; the auditor asks AI-specific questions (model governance, agent access, prompt-change control) they can't evidence.
- **One sentence:** *"Trust0 is the AI module for your SOC 2 audit."*
- **Strength:** most Vanta-like — rides an existing framework, budget, and recurring trigger.
- **Risk:** adjacent to / dependent on Vanta; narrower; a candidate for Vanta to build or buy (the A4 risk).

### Scenario B — "The AI security questionnaire blocking your deal"
- **Who/when:** a fintech founder mid-deal receives a 100-question AI security review.
- **One sentence:** *"Trust0 answers the questionnaire blocking your enterprise deal."*
- **Strength:** sharpest acute pain; best demo; immediate willingness to pay.
- **Risk:** it's an **event, not a budgeted process** — which is exactly the source of the retention/churn problem (assumption A1). Hard to build a durable company on alone.

### Scenario C — "The black-box recorder for production AI agents"
- **Who/when:** an eng team runs agents touching money/data; one misbehaves (the DB wipe, the $300 silent spend from `MarketAnalysis`) or an auditor/regulator asks what happened.
- **One sentence:** *"Trust0 is the flight recorder for your AI agents."*
- **Strength:** most defensible and technical; closest to a true new category.
- **Risk:** drifts toward observability (Laminar, Geordie); the "compliance" framing softens; demand is less named/budgeted than A.

---

## 6. Opinionated read

If the goal is Vanta-like crispness, a durable **scenario needs an existing budget and a recurring trigger** — which points to **A** (or C), not B.

- **B is a superb wedge but not a company on its own** (episodic, no budget line).
- **Recommendation: commit to A as the spine — "the AI evidence for your SOC 2 / security review" — and use B (the questionnaire) as the acute entry trigger.** This buys Vanta's crispness *and* keeps the best demo.
- **C is the bet to make if defensibility matters more than riding existing demand** — it's a real category, but you'd be creating the budget line, not capturing one.

---

## 7. The decision to make

This is a founder call. Two linked choices:

**7a. Which scenario is V1?**
- **A** — AI controls in your SOC 2 (most Vanta-like)
- **B** — the deal-blocking questionnaire (sharpest pain, episodic)
- **C** — black-box recorder (most defensible, observability-adjacent)
- **A via B** — A as the spine, entered through B *(recommended)*

**7b. The strategic fork underneath:**
- **Ride existing demand** — attach to a named framework buyers already budget for. Lower risk, more derivative, exposed to incumbents.
- **Create a new category** — own "AI agent compliance/evidence" before it has a name. Higher risk, more defensible, you must generate the demand.

> A and B lean "ride existing demand." C leans "create a category." Pick the scenario and the fork together — they must agree.

---

## 8. Why this matters before any more building

Picking one scenario collapses everything that has felt ambiguous:
- **Framework:** SOC 2 first — *not* "SOC 2 + EU AI Act + questionnaires + safety" at once.
- **Buyer:** one persona, one trigger.
- **First demo & first feature:** decided by the scenario, not by the architecture.
- **Metrics:** the scenario's outcome becomes the metric.

Until this is decided, every PRD below it is building on sand. After it's decided, the existing PRDs (`PRD_v1.md` scope, `milestones/`) can be re-pointed at the chosen scenario in an afternoon.

---

## 9. Next steps
1. **Founder decides** §7a + §7b (the two are one decision).
2. Re-cut `PRD_v1.md` so its problem statement opens with the **one-sentence scenario** (the "get your SOC 2 done" equivalent), and demote everything outside it to "later."
3. Validate the chosen scenario's core assumption first (A's auditor-acceptance, B's deal-causality, or C's "would you pay to record this?") — cheaply, before building.
4. The lean-team reality (1–3 people) still argues for a **concierge-first** test of the chosen scenario before committing engineering months (see prior scope discussion).

---

*This review deliberately stops at the decision. The point is not to pick for you — it's to make the choice unavoidable and concrete, because no amount of fast building substitutes for it.*
