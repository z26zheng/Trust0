# Adversarial Review — `PRD_v0.3`

| Field | Value |
|---|---|
| **Reviewing** | `Trust0/docs/product/PRD_v0.3.md` |
| **Method** | `product-brainstorming` skill — Assumption Testing mode + Provoke phase, run *against* the PRD |
| **Stance** | Deliberately adversarial. The job is to attack the assumptions the brainstorm and the PRD now **share**, not to re-validate them. |
| **Date** | May 31, 2026 |
| **Output** | Red-team findings (ranked) → prioritized revision list → what survives → feeds `PRD_v0.4` |

> **Why this review is necessary:** `PRD_v0.3` was *built from* `product-brainstorming_v1.md`. That means its self-critique (the §12 validation plan, the ⚠️ flags) only covers the assumptions the brainstorm already doubted. The dangerous assumptions are the ones the brainstorm and PRD now **agree on** — those have no skeptic. This pass supplies one.

---

## 0. The headline provocation

**The brainstorm warned against becoming "invisible plumbing" (`product-brainstorming_v1.md` §5, inversion pass). Then v0.3 made "the invisible substrate the other layers reference" its headline positioning.** We adopted the warning and the failure mode in the same document. That single contradiction is the most important thing in this review.

---

## 1. Frame

- **What we're reviewing:** whether v0.3's *converged* direction (Trust0 / Layer-0, continuous-conformity retention, corpus moat, defer-the-ecosystem) is internally consistent and whether its risk accounting is honest.
- **What I'm explicitly NOT re-litigating:** A1 (retention) and A2 (auditor acceptance) are already correctly flagged. I assume those tests will run. I'm hunting the *unflagged* assumptions.
- **Success for this review:** surface the shared blind spots, find the internal contradictions, re-rank what's actually lethal, and hand `PRD_v0.4` a concrete change list.

---

## 2. Red-team findings (ranked by severity)

### 🔴 CRITICAL

#### C1 — The positioning contradicts the brainstorm's own commoditization warning
- **In v0.3:** the tagline and §1/§8 lead with *"Layer 0 — the trustworthy event substrate the other four layers reference."*
- **The challenge:** "substrate other tools reference" **is** invisible-plumbing positioning — the exact outcome the brainstorm's inversion pass said would commoditize us. Worse, it's **vendor language, not buyer language**. The fintech founder does not wake up wanting to buy "the zeroth layer"; they want *this deal unblocked*. v0.3 fuses two audiences into one headline: the **buyer** (wants a painkiller) and the **investor/category narrative** (wants infrastructure). Conflating them weakens both.
- **Who'd hate it:** the buyer (it doesn't speak to their pain); ironically, *not* investors — which is the tell that this positioning serves the pitch, not the customer.
- **Severity rationale:** positioning errors propagate into messaging, pricing, and the whole funnel. Critical.

#### C2 — The moat is circular: it depends on the single most unvalidated assumption
- **In v0.3 §10:** the moat = corpus (#1) + auditor-recognized format (#2) + badge network effect (#3) + cross-customer evidence patterns (#4).
- **The challenge:** moats #1 and #4 **only compound if customers stay and the base scales** — i.e., they are *downstream of A1 (retention)*, the riskiest assumption in the whole doc. If A1 is weak, the corpus never reaches scale and the "data network effect" never ignites. **We've placed the moat on top of the trapdoor.** Two more unstated erosions:
  - **LLM erosion:** as foundation models get better at answering security questionnaires directly from raw evidence, a curated answer-corpus is a *depreciating* asset, not a compounding one.
  - **Incumbent corpus:** Vanta/Drata already hold vastly larger SOC 2 answer corpora across thousands of customers. Our corpus is only defensible on the *agent-specific* slice — which should be stated explicitly.
- **Severity rationale:** if the moat is conditional on an unproven assumption and threatened by the underlying tech trend, calling it "the moat" is overconfidence. Critical to make honest.

#### C3 — The PRD under-counts its lethal assumptions (only 2 of ~5 are flagged)
v0.3 flags A1, A2 (and A6 feasibility). It silently treats these as settled:
- **A7 — "Layer 0 is a category buyers will pay for."** No evidence. Pure positioning bet. (See C1.)
- **A8 — "The corpus compounds into defensibility."** Contested by C2. Currently asserted in §10 as fact.
- **A9 — "EU AI Act Article 19 binds our ICP."** v0.3 demotes this to a *research open question* (OQ #2) — but the **entire continuous-conformity retention anchor (FR-CONF) rests on it.** If Art. 19 only bites Annex III high-risk systems and most seed-stage fintech AI doesn't qualify, the retention thesis loses a leg. An assumption that load-bearing is **lethal, not a footnote.** Promote it.
- **A10 — "Better/faster evidence actually unblocks the deal."** The wedge's causal claim. If the real bottleneck is *procurement queue latency* (a process artifact), then perfect answers still sit for weeks and "unblock in minutes" overpromises. Untested.
- **Severity rationale:** a validation plan that omits half the lethal assumptions gives false comfort. Critical.

---

### 🟠 HIGH

#### H1 — "The window is 6–12 months" contradicts "defer the ecosystem to post-PMF"
- **In v0.3:** §2 says the realistic strategic asset is the **6–12 month window** before an incumbent ships agent compliance. §13 defers the ecosystem (the distribution + defensibility play) to **Phase 3, post-PMF (Months 6+).**
- **The challenge:** we plan to start building the moat-and-distribution layer *exactly as the window closes*. If PMF takes ~6 months, Phase 3 begins the moment the incumbents are most likely to have moved. Either the window is longer than we claim (then say so and justify it), or deferring the whole ecosystem is wrong, or — most likely — **the cheap parts of the ecosystem need to move earlier.**
- **Severity:** this is a strategy-sequencing incoherence between two sections of the same doc.

#### H2 — "Architect the seams now, build later, no rework" is unfalsifiable optimism
- **In v0.3:** §6 (FR-AUTH-SEAM), §8, §13 repeatedly promise the deferred ecosystem will be "additive, not a rewrite" because we built the seams.
- **The challenge:** **unexercised seams rot.** You do not know an interface is right until a real consumer uses it. "No rework" is a hope, not a design guarantee — and it's the kind of claim engineering teams regret. 
- **The fix (cheap):** exercise the read-seam *internally* in Phase 1 — make our own trust page and auditor portal read through the reserved read path. That converts the seam from a belief into a tested interface at near-zero extra cost, and it partially addresses H1 (the cheapest ecosystem validation happens inside the window).

#### H3 — Fintech is simultaneously "locked" and "open"
- **In v0.3:** ICP (§4), the ≥80% fintech metric (§7), and "fintech messaging" in Phase 1 (§13) all **assume fintech**. Yet OQ #1 + §12 frame the vertical as **unvalidated, to be compared against healthtech.**
- **The challenge:** you cannot run an 8-week build with fintech-locked messaging *and* hold the vertical genuinely open. This is having it both ways. Pick one: **commit** to fintech as a deliberate focus bet (and stop calling it open), or **actually hold it open** (and don't lock Phase-1 messaging until Phase 0 resolves it).
- **Recommendation:** commit to fintech as the V1 bet (founder familiarity + the `MarketAnalysis` vertical-concentration discipline are legitimate reasons), and reframe healthtech as the leading **V2 expansion** candidate with a one-call Phase-0 gut-check — not a full bake-off that stalls the build.

#### H4 — The retention anchor drifts onto the incumbent's home field
- **In v0.3:** Non-goals (§3) explicitly exclude "generic SOC 2 automation (invites incumbents' strength)." But FR-CONF (§6) = **"continuous SOC 2 monitoring,"** which is precisely Vanta/Drata's core.
- **The challenge:** the retention core, as written, walks straight into the fight the PRD says to avoid. 
- **The fix:** scope FR-CONF to **agent-specific conformity only** (agent runtime evidence retention, agent control drift, Art. 19 agent-log retention) — the slice incumbents *don't* cover — and let the live trust page carry the general "continuous value" story.

#### H5 — Success metrics were inherited across three strategic pivots
- **In v0.3 §7:** "50 paying / $10K MRR / 90 days" is copied verbatim from `PRD_v0.1`/`v0.2`, through a rename and two strategy changes.
- **The challenge:** $10K ÷ 50 = **$200 avg** ≈ the **Starter** tier — but the continuous-conformity value the new strategy sells lives in **Growth ($599)**. The targets quietly assume the cheap tier while the strategy pitches the expensive one. Metrics should be *re-derived from the new thesis*, with an explicit tier-mix assumption, or they'll misdirect the team.

---

### 🟡 MEDIUM

#### M1 — "SOC 2 Type II within 6 months" is likely infeasible
- Type II requires an **observation window** (commonly 6–12 months) *after* controls are operating. From a standing start, 6 months realistically yields **Type I**. This is also an A2 credibility claim — overstating it undercuts the "exemplary posture" argument with the very auditors we're courting. Fix to Type I @ ~6 months, Type II @ ~12.

#### M2 — "Who would hate this?" is unaddressed
The Provoke phase demands it; v0.3 has no detractor analysis. At least three:
- **The founder** — latency paranoia about wrapping the LLM client on the hot path (we promise ≤5ms but they'll fear the unknown vendor in the critical path).
- **The security reviewer** — distrust of a *tiny, unknown vendor holding their evidence*. `MarketAnalysis` §6.2 is explicit: a security product must itself be secure, and solo/small-team provenance is a hard sell to security buyers.
- **The auditor** — antipathy to learning yet another vendor's format (this is A2, but framed as a person who actively resists, not a neutral gate).

#### M3 — The wedge's causal claim is untested (ties to A10)
"Unblock a stalled deal in minutes" assumes evidence quality is the binding constraint. If procurement *process latency* is the real gate, we speed up one step of a slow pipeline and the headline promise overreaches. Add a question to the A1/A2 interviews: *"When you had good answers, did the deal actually move faster — or did it still sit in their queue?"*

#### M4 — P0 is too heavy for 8 weeks, and it builds the retention core before validating retention
- **In v0.3:** P0 = SDK (4 FRs) + registries + questionnaire engine + trust page + evidence pack + **FR-CONF** + auth seam. That's essentially all of `PRD_v0.1` *plus* the new conformity monitor.
- **The challenge:** the `write-spec` skill says be *ruthless* about P0 ("if everything is P0, nothing is P0"). More pointedly: **FR-CONF is the retention core, and A1 — whether retention demand exists — is unproven.** Building the retention engine before the gate that validates retention demand **inverts the PRD's own sequencing discipline.** Move FR-CONF to P1 (pending A1); the trust page (already P0) carries the continuous-value story for launch.

---

## 3. Provocations (the Provoke phase)

- **"What is the 10x version?"** If "Layer 0" is genuinely real, the ambitious move isn't selling forms to fintech founders — it's becoming the **default evidence format emitted by agent frameworks and provider SDKs** (LangChain, the model SDKs). v0.3's product is *timid relative to its positioning*. Resolution: either raise product ambition to match "Layer 0," or **lower the positioning to match the wedge** (lead with the painkiller; keep Layer 0 as a stated long-game). I favor the latter for V1.
- **"What if we did the opposite?"** The brainstorm floated *killing the SDK* for V1 (ingest existing OTel/LangSmith/Helicone traces instead). v0.3 silently kept the SDK as P0 — yet also declares the SDK *"not the moat"* and *"the #1 adoption friction."* So we've made our highest-friction component a hard dependency for the wedge. v0.4 should at least **record why the SDK stays P0** (answer: it's the data tap that produces *provenance/hashing* generic traces can't — that's a real reason, but it must be stated, not assumed).
- **"Name the pattern."** Two PM traps are present: **solution-anchoring** (the SDK survived three pivots unquestioned) and **narrative-led positioning** (Layer 0 chosen because it sounds category-defining, before any buyer validated it).

---

## 4. What survives the challenge (do NOT change these)

These are genuinely strong and should carry into v0.4 intact:
- **The A1/A2 gating discipline** — validation-before-spec-lock is exactly right.
- **SDK reframed as wedge + data tap, not moat** — correct (just don't then make a contradictory moat claim; see C2).
- **Deferring the *heavy* ecosystem build** (OAuth server, MCP, OSS connectors, standards body) — correct per `MarketAnalysis`. (The *cheap* read-seam should be exercised early — H2 — but the heavy surface stays deferred.)
- **The two-sided buyer/acceptor framing** — a real insight; keep it central.
- **Auditor-recognized format + badge network effect** — the two most *robust* moats (less dependent on scale than the corpus). Lead the moat section with these.

---

## 5. Prioritized revision list for `PRD_v0.4`

Ordered by leverage. ✅ = apply now as a doc change; 🔬 = convert into a tracked assumption/test rather than silently "fixing."

1. ✅ **Split the positioning (C1).** Buyer-facing headline = the painkiller ("close the enterprise deal stuck in AI security review"). Demote "Layer 0" from tagline to a §1 *strategic narrative* line. 
2. 🔬 **Promote the hidden lethal assumptions (C3).** Add **A7 (category), A8 (corpus compounds), A9 (Art.19 applicability), A10 (evidence→deal causality)** to §12 and re-rank lethality. Promote A9 out of "research OQ" into a gating assumption for FR-CONF.
3. ✅ **Make the moat honest (C2).** Lead with auditor-format + badge (robust); state the corpus moat as **conditional on retention + scale and limited to the agent-specific slice**; name the LLM-erosion counterpoint.
4. ✅ **Reconcile window vs. defer (H1+H2).** State the 6–12mo window as a dated, explicit bet; **exercise the read-seam internally in Phase 1** (our own trust page/auditor portal read through it) to validate it cheaply; keep the heavy ecosystem deferred.
5. ✅ **Resolve the fintech contradiction (H3).** Commit to fintech as the V1 focus bet; reframe healthtech as the V2 expansion candidate with a one-call Phase-0 sanity check. Remove "open" framing from the vertical.
6. ✅ **Scope FR-CONF to agent-specific conformity (H4)** and **move FR-CONF to P1 pending A1 (M4).** Trust page (P0) carries the continuous-value story at launch.
7. ✅ **Re-derive metrics from the new thesis (H5).** Separate acquisition / retention / acceptance metrics; align the MRR target with the tier the strategy sells (state the tier-mix assumption).
8. ✅ **Fix the SOC 2 claim (M1):** Type I @ ~6 months, Type II @ ~12 months; keep the dogfood narrative.
9. ✅ **Add a "Detractors / who would hate this" subsection (M2)** with mitigations (latency proof, our-own-security posture, auditor co-design).
10. ✅ **Record why the SDK stays P0 despite being "not the moat" (Provoke/opposite)** — provenance/hashing that generic traces can't provide — and log SDK-optional ingestion as a P2 alternative considered.
11. ✅ **Add the causal question to the A1/A2 interview scripts (M3/A10).**

---

## 6. Verdict

`PRD_v0.3` is a **structurally sound, honestly-hedged document with one systemic flaw: its self-critique stops exactly where the brainstorm's did.** The validation plan is excellent for the two assumptions it names and silent on three or four that are equally lethal. The positioning ("Layer 0") is the single biggest risk — it's the commoditization failure mode the team already warned itself about, dressed up as a category claim.

**None of this kills the direction.** The wedge is still good, the gating discipline is still right. The fixes are: be honest about the moat, count *all* the lethal assumptions, resolve the internal contradictions (window/defer, fintech open/locked, conformity vs. non-goal), and stop letting the investor narrative drive the buyer headline.

→ Applied in `PRD_v0.4.md`.

---

*End of adversarial review. This document is meant to be disagreed with too — if a finding is wrong, say why in v0.4's changelog rather than silently dropping it.*
