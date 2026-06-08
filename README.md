# DeFi Rate Term-Structure System

Importing the fixed-income yield-curve discipline into DeFi, where interest-rate data points exist (staking yields, tokenized T-bills, lending rates, tokenized-yield markets) but no agreed risk-free anchor and no coherent curve connect them. The raw ingredients exist; the term structure does not.

## The thesis

A conventional curve assumes one unit of account, uniform instrument quality, and observed prices across all maturities. On-chain, all three fail at once. The result is not a worse curve — it is a different object: a **term-structure system**. Being honest about that distinction is the source of credibility with a fixed-income desk head.

## The framework — Frame / Strip / Zone / Basis

1. **Frame** — the unit of account (numeraire). A family of parallel curves, one per frame; none privileged. Everything below happens inside a frame.
2. **Strip** — within a frame, decompose every observed rate into a pure time-value *core* (feeds the curve) plus tracked *premia* (each its own series). A curve point is always the output of a strip, never a raw quote.
3. **Zone** — split each curve into an *anchored* zone (points that trade) and a *modeled* zone (openly inferred), with a confidence flag on every point. The boundary is shown, not buried.
4. **Basis** — the connective tissue across curves: cross-frame basis and spreads between premia. Often the most informative output.

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
