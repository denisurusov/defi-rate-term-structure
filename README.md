# DeFi Rate Term-Structure System

Importing the fixed-income yield-curve discipline into DeFi, where interest-rate data points exist (staking yields, tokenized T-bills, lending rates, tokenized-yield markets) but no agreed risk-free anchor and no coherent curve connect them. The raw ingredients exist (we'd need to choose which ones to use); the term structure does not.

## The thesis

A conventional curve assumes one unit of account, uniform instrument quality, and observed prices across all maturities. On-chain, all three fail at once. The result is not a worse curve — it is a different object: a **term-structure system**.

## The framework — Frame / Strip / Zone / Basis

The four nouns map one-to-one onto the three assumptions that fail (Frame ↔ unit of account, Strip ↔ uniform quality, Zone ↔ observed prices) plus the seam that holds the pieces together (Basis). Frame, Strip, and Zone all operate *within* a single curve; Basis is the one layer that works *across* curves.

### 1. Frame — the unit of account (numeraire)

A frame is the denomination a curve is expressed in. The defining feature of the on-chain problem is that there is more than one plausible numeraire and none is privileged as "the real one": a native-unit anchor has the deepest liquidity but a volatile unit, while a dollar anchor has the right unit but is effectively imported from off-chain Treasuries. So the system holds a *family of parallel curves*, one per frame, that genuinely coexist rather than one master curve with the others treated as error.

This is the first decision and everything downstream hangs on it — a rate only has meaning once you fix the frame it lives in. In practice the program may need to carry two frames at once (native and dollar) plus the spread between them, rather than forcing a single choice. Choosing the frame is the step that resolves the numeraire fork.

### 2. Strip — decomposition into a clean core plus premia

Within a frame, every observed rate is treated as a *composite*, not a quote: a pure time-value-of-money **core** wrapped in one or more risk **premia** (the "dirt"). Strip pulls these apart explicitly — the clean core is what feeds the curve, and each premium is tracked as its own series (staking/slashing, utilization/liquidation, wrapper/redemption/oracle, governance-set, and so on). A point on a curve is therefore always the *output* of a strip, never a raw market number.

This is the step a conventional rates desk gets for free and the on-chain builder must do and defend. In TradFi, clean instruments are abundant and homogeneous, so the curve is built by near-simple aggregation of like-for-like quotes. On-chain, nearly every candidate rate is dirty and the candidates are *non-homogeneous* (a staking rate, a lending rate, and a wrapped-Treasury rate carry different risks and cannot be strung together naively). The contribution is to model the spreads between these dirty rates and back out a clean curve — spread-stripping rather than aggregation. This is the real quant work of the project.

### 3. Zone — the observed/modeled split along each curve

Each curve is divided into an **anchored zone**, built from maturities that actually trade, and a **modeled zone**, openly inferred where nothing trades. On-chain liquidity clusters at the short end (roughly the 3-month region), and almost nothing trades past ~6–12 months, so the long end is *modeled, not observed*. The boundary between the two zones is part of the structure and is shown rather than buried, with a confidence flag riding alongside every point so a reader always knows how much is real.

This is the layer that earns the project its credibility with a desk head. The honest pitch is not "I rebuilt the risk-free curve on-chain" but "the long end is a model and here is exactly where it begins." In the thin and modeled regions, manipulation-resistance (aggregation, liquidity-weighting, outlier rejection) does the work that market depth does in the conventional world.

### 4. Basis — the connective tissue across curves

Basis is the only layer that operates *between* curves rather than within one. It tracks two kinds of spread explicitly: **cross-frame basis** (the spread between one unit-of-account curve and another — e.g. native vs dollar, which is itself a clean analog of the conventional cross-currency basis) and **premium spreads** (the spreads between the premia stripped out in layer 2). These are not byproducts; they are often the most informative outputs of the whole system, because they are what it reveals about the cost of moving between units of account and between risk profiles.

---

Pipeline: choose a **Frame** → **Strip** each rate to its core → mark the **Zones** → connect with **Basis**.

Descriptive register for prose: Denomination → Decomposition → Horizon → Basis. Short names are internal vocabulary; spell out on first use in the brief.

## Architecture stance

Deterministic, versioned curve-math core (bootstrapping, premium-stripping, near/far split, basis) plus a thin agentic shell limited to the dirty edges: data ingestion/normalization, instrument classification and cleaning triage (proposing, not executing, cleaning choices), and plain-language narration of curve changes. Agents must never re-derive the math at runtime — reproducibility is the whole game.

Strongest deliverable: a knob-driven UI that turns each non-obvious assumption (anchor choice, stripping method, observed/modeled boundary, long-end extrapolation) into a control a quant can move and see the system respond. Built as the vehicle for a settled methodology, not the place to discover it.

## Repo layout

- `research-plan.md` — workstream index, dependency ordering, exit criteria (**start here**)
- `research/` — one file per workstream (W0–W5)
- `docs/` — research brief & one-page charter, drafted from research outputs
- `engine/` — deterministic curve-math core (later)
- `ui/` — knob-driven interactive tool (later)

## Status

Research phase. The naming gate (Frame/Strip/Zone/Basis) is cleared; methodology is being settled before any build.
