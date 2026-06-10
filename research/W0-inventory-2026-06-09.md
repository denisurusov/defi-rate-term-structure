# W0 Foundations — Candidate-Rate Inventory

_Refresh as-of: 2026-06-09. Scope: observation and characterization only.
No role, fitness, or borrow/avoid decisions are made here — those are W1 inputs._

## Layer A — Figures snapshot (volatile; disposable, re-run each refresh)

Macro anchor (TradFi reference, 2026-06-05): SOFR overnight ~3.62%;
Treasury curve upward-sloping — 3m 3.72% · 1y 3.85% · 2y 4.17% · 5y 4.29%.
Context only; the dollar frame is not assumed here.

| Class | Liquidity / size | Live yield | Where it trades | Confidence |
|---|---|---|---|---|
| Native staking (ETH) | Very deep; ~32% of supply staked | ~2.78% base + 0.5–1% MEV | overnight | range (2.78–3.4% across sources) |
| Native staking (SOL) | Very deep | ~5.7–5.9% APY | overnight | firm |
| Tokenized T-bills | ~$13.5B total; BUIDL ~$2.4B, USYC ~$3.0B, BENJI ~$0.84B, WTGXX ~$0.86B | ~4.0–5.3% (USDY ~5.3%) | short-end cluster | firm (USYC issuer attribution contested) |
| Lending rates | Aave ~$20–26B TVL (deepest) | Aave USDC 3–5%, Morpho 4–8%, Compound 3–5% | floating, short end | firm (variable by design) |
| Tokenized-yield implied (Pendle) | TVL ~$1.5B, down from ~$13.1B (Sep-2025 peak) | heterogeneous: PT-sUSDe ~9%, stETH ~6.2%, rETH ~2.3%; stUSDS pool ~16.8% (incentive-boosted) | 3/6/9/12m; bunched short; long-dated barely trades | contested (TVL range $1.5–3.5B) |
| Savings-rate tokens (sUSDS) | USDS supply >$9B | SSR ~3.75–4.5% | floating | firm |

Confidence legend: firm = corroborated/stable · range = sources diverge, recorded as a band · contested = trackers conflict materially.

## Layer B — Structural & characterization (slow-moving; changes only with a stated reason)

- **Native staking (ETH/SOL):** variable, carries slashing/operator risk; denominated in the native unit (ETH/SOL), not USD.
- **Tokenized T-bills:** economically the cleanest, but carries wrapper/redemption/oracle/issuer risk; secondary access is thin and KYC-gated; tracks Treasuries (circular to the TradFi anchor).
- **Lending rates:** utilization-driven; reflexive and manipulable.
- **Pendle implied:** fixed-term quote on a dirty floating underlying; heterogeneous across underlyings (not one homogeneous series); depth is concentrated in Ethena-linked products and is concentration-fragile.
- **Savings-rate tokens:** a governance-set parameter, not market-cleared.
