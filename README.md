# uniswap_3pools_analysis
Analyze 3 pools at Uniswap

This project compares three Ethereum mainnet Uniswap v3 pools:
- USDC/ETH (0.05%)
- DAI/USDC (0.01%)
- WETH/WBTC (0.05%)

Goal: quantify how **risk regimes (volatility / drawdowns)** interact with **fee generation** and **v3 range/out-of-range risk**, using a lightweight but interview-ready framework.

## Data
- **Prices (daily, USD):** CoinGecko API (ETH, WBTC, DAI, USDC)
- **Pool activity (daily):** Dune export (swaps, volume_usd, estimated_fees_usd)

## Method
### A) Volatility / Risk Regime
- Build pool price proxies:
  - USDC/ETH ≈ ETH_USD
  - DAI/USDC ≈ DAI_USD / USDC_USD
  - WETH/WBTC ≈ ETH_USD / WBTC_USD
- Metrics: 30d/90d annualized realized volatility, max drawdown, worst 1d/7d returns, BTC vs ETH return correlation.

### B) Fee Rate & Fee Stability (pool-level)
- fee_rate = estimated_fees_usd / volume_usd
- fees_per_swap = estimated_fees_usd / num_swaps
- stability: CV (std/mean), worst/best 7d rolling fee sums
- plots: daily fees + 7d rolling fees.

### C) v3 Range / Out-of-range Risk (proxy) + IL baseline
- Define range strategies (±5%, ±10%, ±20%) with periodic rebalancing.
- time-in-range = share of days price stays within band.
- range-adjusted fees = fees * in_range (out-of-range → 0) as a fee-capture proxy.
- IL baseline: V2 50/50 IL formula applied to price ratio (clearly marked as approximation).
- Extensions: stress scenarios (ETH shock, correlation break, stablecoin depeg), risk-return frontier (expected vs downside vs volatility), regime-shift comparison (LOW_VOL vs HIGH_VOL).

## Key Outputs
- Cross-pool ranking on risk (vol/drawdown) vs reward (fees) vs sustainability (time-in-range).
- Evidence that higher volatility can increase fee spikes but may reduce fee capture via out-of-range behavior.

## Notes / Limitations
- Fees are pool-level (not wallet/position-level); range results are a proxy.
- IL uses a V2 approximation; primary v3 risk focus is out-of-range + fee capture.































