# Mamba-3 Financial Forecasting

Financial forecasting system using [Mamba-3](https://arxiv.org/abs/2603.15569) as a causal feature extractor over historical price, volume, indicator, and fundamentals data (US and Canadian equities), paired with a GRPO reinforcement-learning decision head that selects top-k portfolio allocations.

<!-- TODO: architecture diagram -->

## Planned Deliverables

- Runnable exported inference model
- Model inference wrapper with data preprocessing and output postprocessing
- Backtested results (Sharpe ratio, returns vs. benchmark, directional accuracy, RMSE, simulated portfolio holdings)
- Bill of materials

## Architecture

- **Feature extractor:** Mamba-3, causal encoder over price/volume/indicator sequences.
- **Modification:** number of "complex-capable" positions in the state space made learnable and gated ("dynamic RoPE split"), vs. fixed in the original architecture.
- **Decision head:** GRPO-based, outputs top-k portfolio allocation. Can always hold cash or a reference ETF instead of forcing a trade.
- **Currency handling:** prices normalized to a common currency via historical USD/CAD rates before feature extraction.

## Bill of materials

Backtests built on data that excludes delisted/bankrupt/acquired companies (survivorship bias) overestimate returns. The dataset only contains the surviving equities that are still listed today. This is a well-known source of error in financial ML, and is the primary cost driver. Norgate's Platinum tier is priced specifically for including delisted securities and historically accurate index constituents, which cheaper tiers and most free/low-cost data APIs omit entirely.

| Item | Cost (CAD) | Source |
|---|---|---|
| Norgate US Stocks — Platinum, 6mo (delisted stocks + historical index constituents + fundamentals | $480.34 | [norgatedata.com](https://norgatedata.com/stockmarketpackages.php) |
| Norgate Canadian Stocks — Platinum, 6mo (same tier, same fundamentals methodology) | $346.50 | [norgatedata.com](https://norgatedata.com/stockmarketpackages.php) |
| **Total** | **$827.20** | |

## License

Apache License 2.0. Builds on [Mamba-3](https://github.com/state-spaces/mamba) (Apache 2.0).

## Citation

```
Lahoti, A., Li, K.Y., Chen, B., Wang, C., Bick, A., Kolter, J.Z., Dao, T., Gu, A. (2026).
Mamba-3: Improved Sequence Modeling using State Space Principles.
arXiv:2603.15569
```
