# W0 Foundations — Prior-Art Profile: IPOR

_As-of: 2026-06-09. Factual profile only. Borrow/avoid evaluation is a W1 input._

## The index
IPOR Index is computed on-chain block-by-block from DeFi money-market lending
rates (USDC, USDT, DAI, stETH), published as a public good via oracle, and
positioned as a SOFR/LIBOR analogue. It is single-class: anchored on the
lending-rate class only.

## The swap product
Peer-to-pool interest-rate swaps at 28-, 60-, and 90-day tenors. The AMM uses
Hull-White and jump-diffusion models. Tenor coverage stops at 90 days; there is
no belly or long end, and no clean-core / premia separation (no Strip-equivalent).

## Current state
Commercial focus has migrated to IPOR Fusion — a meta-DeFi aggregation and
asset-management (yield-optimizer vault) product: ~$11.7M TVL / ~$55M TVM,
~5.4% average APY across 35 pools. The index and swaps are maintained as
"core" but are no longer the growth driver.

## Adjacent attempts (survey)
- Pendle / Boros: reaching toward an on-chain fixed-income map, including
  funding-rate and reference-rate trading ("if there is a rate, Pendle can
  make a market").
- Term Finance: auction-based fixed-rate lending, without yield-splitting.
- None constructs a coherent multi-tenor risk-free curve.
