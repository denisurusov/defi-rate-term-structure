# Research Plan

## Why workstreams, not one-conversation-per-layer

The four layers (Frame / Strip / Zone / Basis) are the right unit for the *deliverable* but the wrong unit for *research*. They form a sequential pipeline with hard dependencies:

- **Basis** is defined as cross-frame — it cannot be studied until Frame is fixed and at least two curves exist. A standalone Basis thread opened now would sit empty.
- **Zone**'s anchored/modeled boundary depends on what Strip produced and which Frame you're in.
- **Strip**'s premia categories depend on knowing the "dirt" in each candidate rate.

A strict layer-per-thread split opens conversations that can't move until their upstream dependency resolves.

The heaviest research is also not layer-shaped. The candidate-rate inventory (refreshed liquidity + live yields) and the prior-art read are shared substrate every layer draws on; scattered across four threads they get duplicated or orphaned. And the layers are uneven in weight — Strip is the core quant contribution and needs more than one conversation, Frame is a fork to resolve once, Zone is as much credibility/presentation framing as open research.

So research is organized as **workstreams sequenced by dependency**. The per-layer files under `research/` are the *homes* for settled output; the active work happens in these workstreams.

## Dependency ordering

```
W0 Foundations ──> W1 Frame ──> W2 Strip ──> W3 Zone ──┐
                                                        ├──> W4 Basis
                                  (needs >=2 curves) ────┘

W5 Tooling runs in parallel (largely independent of W0–W4)
```

W0 is the empirical floor. W1 gates everything downstream. W4 cannot start until W1 is locked and W2/W3 have produced at least two curves. W5 proceeds alongside and firms up as W2–W3 settle.

---

## W0 — Foundations

**Purpose:** establish the empirical floor — what rates exist, how liquid, how clean, and what prior art already attempts this.

**Key open questions**
- Refresh the candidate-rate inventory with current liquidity and live yields: native staking yield, tokenized T-bill yields, lending-protocol rates, tokenized-yield implied rates, savings-rate tokens.
- For each: depth/liquidity, secondary-market access/gating, the specific "dirt" (credit, optionality, governance-set, oracle/wrapper/redemption risk), and which tenor region it pins.
- Prior art: IPOR (on-chain benchmark + swap curve) — what it anchors on, where it's thin, what to borrow vs avoid. Survey other attempts.

**Inputs:** on-chain data sources, protocol docs, IPOR methodology.

**Exit criteria:** a refreshed candidate table (liquidity / cleanliness / spanning / verdict) plus a 1–2 page prior-art memo, with structural properties kept separate from volatile figures.

**Depends on:** nothing.

---

## W1 — Frame (numeraire)

**Purpose:** resolve the numeraire fork and decide the initial set of frames.

**Key open questions**
- Native-unit (right liquidity, volatile unit) vs dollar (right unit, imported anchor) — or both, as parallel frames with a basis between them?
- If dollar: is tethering to Treasuries (via tokenized T-bills) philosophically acceptable, given the circularity?
- What is the minimal set of frames for v1 (likely >=2, so Basis has something to connect)?

**Inputs:** W0 inventory.

**Exit criteria:** a decided, documented initial frame set with rationale; the numeraire fork closed.

**Depends on:** W0.

---

## W2 — Strip (the core quant contribution)

**Purpose:** define how to decompose a dirty, non-homogeneous observed rate into a clean time-value core plus tracked premia.

**Key open questions**
- The spread-stripping method: how to model spreads between differently-risked rates to back out a clean core.
- Premia taxonomy: which premia are tracked as their own series (credit, liquidity, oracle/wrapper, governance) and how each is estimated.
- Handling non-homogeneity across tokenized-yield markets (heterogeneous quotes bunched ~3m).
- Validation: how do we know a stripped core is genuinely "clean"?

**Inputs:** W0 dirt characterization, W1 frame choice.

**Exit criteria:** a specified, testable stripping procedure per candidate class; premia series defined; a worked example on real data.

**Depends on:** W1 (and W0). **Budget at least two conversations.**

---

## W3 — Zone

**Purpose:** define the anchored/modeled boundary and the confidence-flag scheme; specify long-end extrapolation.

**Key open questions**
- Where does "observed" end and "modeled" begin per frame (the empty long end past ~6–12 months)?
- The long-end extrapolation model — and how it is labelled as modeled, not observed.
- The confidence-flag scheme: what each point carries, how it's computed and displayed.

**Inputs:** W2 stripped cores, W1 frame.

**Exit criteria:** a boundary rule + extrapolation method + confidence schema, with the boundary shown rather than buried.

**Depends on:** W2.

---

## W4 — Basis

**Purpose:** the connective tissue across curves.

**Key open questions**
- Cross-frame basis (e.g. native vs dollar): definition, estimation, what it reveals.
- Spreads between premia series across frames.
- Which basis outputs are the most informative (Basis is flagged as often the most informative output).

**Inputs:** at least two constructed curves from W1–W3.

**Exit criteria:** defined basis measures with a worked cross-frame example.

**Depends on:** W1 locked + at least two curves from W2/W3.

---

## W5 — Tooling (parallel track)

**Purpose:** settle the deterministic-core / agentic-shell boundary and the knob-UI design.

**Key open questions**
- The exact boundary: what is fixed, versioned math vs what agents touch (ingestion/normalization, classification, cleaning triage as proposals, narration).
- Reproducibility guarantees: how agents are prevented from re-deriving math at runtime.
- Which knobs the UI exposes (anchor choice, stripping method, observed/modeled boundary, long-end extrapolation), and the frontend framework + build environment (a Cowork/Claude Code/Cursor-style shell hosting a real frontend).
- Notion's role limited to the doc/brief layer (no live computation).

**Inputs:** the emerging methodology from W0–W4 (loose coupling).

**Exit criteria:** an architecture note (core/shell contract, reproducibility rules) plus a knob inventory mapped to methodology assumptions.

**Depends on:** largely independent; firms up as W2–W3 settle.

---

## Sequencing summary

1. Start **W0** and **W5** now — both have no hard upstream.
2. W0 resolves → decide **W1**.
3. W1 locked → open **W2** (deep, multi-conversation).
4. W2 settles → **W3**.
5. W1 + at least two curves → **W4**.
6. Draft the `docs/` brief + charter once W0–W1 settle and Strip has a worked example.
