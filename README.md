# 🎯 RSI Divergence — 3-Target Quantitative Backtest
### ETHUSDT Perpetual Futures · Binance · 5-Minute Timeframe

> **Strategy type:** Proprietary RSI-based divergence system with structured 3-target exit architecture and dynamic stop-loss trailing  
> **Author:** Akshat Vaishya · Associate, Trade Operations · SS&C GlobeOp  
> **Status:** Backtested · Paper trading in progress

---

## 📊 Live Interactive Dashboard

**[→ Open Full Interactive Dashboard](https://akshatvaishya16-hub.github.io/rsi-divergence-backtest/dashboard.html)**

The dashboard is fully interactive — no download required. Open it in any browser to:
- Toggle between **LB 20 / LB 25 / LB 30** lookback configurations
- Switch fee scenarios (Taker/Taker · Maker/Taker · Maker/Maker)
- Browse the complete **Trade Log** — filter by Bull / Bear / Wins / Losses / TP3 / Year
- View the **Trade P&L Chart** with SL risk (below zero) and TP gains (above zero) per trade
- Download trade CSVs and generate a PDF stakeholder report — all at **$10,000/trade fixed**

---

## 📋 Backtest Specifications

| Parameter | Value |
|---|---|
| Asset | ETHUSDT Perpetual Futures |
| Exchange | Binance |
| Timeframe | 5-Minute |
| Data range | Jan 1 2020 → Sep 14 2026 |
| Total candles | 704,566 |
| Years tested | 6.7 years |
| Strategy type | Proprietary RSI divergence |
| Exit structure | 3-target scaled exit (5% / 75% / 20%) |
| Stop-loss mode | Trail after TP2 — remaining 20% becomes risk-free |
| Position sizing | Fixed $10,000 per trade (for reporting) |
| Best configuration | LB 30 ⭐ |

---

## 📈 Key Results — LB 30 (Best Configuration)

| Metric | Value |
|---|---|
| Total Trades | 2,515 |
| Win Rate | **74.12%** |
| Gross P&L ($10k/trade) | **$140,714** |
| Net P&L after Taker fees | **$115,564** |
| Net P&L after Maker fees | **$130,654** |
| Profit Factor | **2.72×** |
| Max Drawdown | $1,358 (13.58%) |
| Best Single Trade | +$1,151 |
| Worst Single Trade | -$681 |
| Avg Win | +$119 |
| Avg Loss | -$126 |
| TP1 Hit Rate | 88.7% |
| TP2 Hit Rate | **74.1%** (primary exit) |
| TP3 Hit Rate | 34.6% |
| Max Win Streak | 25 consecutive |
| Max Loss Streak | 6 consecutive |
| Avg Hold Time | 52.9 candles (4.4 hours) |

---

## 🏦 Institutional Ratios

| Ratio | Value | Benchmark | Verdict |
|---|---|---|---|
| Sharpe Ratio | **7.776** | >3.0 = Institutional | ✅ Institutional |
| Sortino Ratio | **12.06** | >3.0 = Excellent | ✅ Excellent |
| Calmar Ratio | **15.49** | >3.0 = Strong | ✅ Excellent |
| Recovery Factor | **103.6** | >5.0 = Strong | ✅ Strong |
| Expectancy | **$55.95/trade** | Must be > 0 | ✅ Positive edge |
| Payoff Ratio | **0.948** | >1.5 = Favourable | ⚠ Neutral |
| Annual Return | **210.38%** | — | ✅ Excellent |
| Ulcer Index | **1.7976** | Lower = smoother | ✅ Very smooth |

---

## 🎲 Monte Carlo Simulation — 10,000 Bootstrap Runs

Resamples actual trade P&Ls with replacement 10,000 times. Tests whether results are structural edge or lucky sequencing.

| Scenario | P&L ($10k/trade) |
|---|---|
| Worst 5% of orderings | $129,060 |
| Median outcome | $140,623 |
| Best 5% of orderings | $151,888 |
| Probability of profit | **100%** |

**Interpretation:** Across all 10,000 random orderings of actual trades, not a single simulation produced a loss. The edge is structural — not sequence-dependent.

---

## 📸 Dashboard Screenshots

### Tab 1 — Backtest Results
Exit architecture, performance overview, streak analysis, profit bifurcation, target hit rates

![Backtest Results](assets/tab1_backtest_results.png)

### Tab 1 — Charts (continued)
P&L over time (weekly/monthly/6-monthly toggle), cumulative equity curve, lookback comparison

![Charts & Equity Curve](assets/tab1_charts.png)

### Tab 3 — Institutional Ratios
All 8 institutional ratios with verdicts, Monte Carlo distribution, Sharpe/Sortino/Calmar comparison across lookbacks

![Institutional Ratios](assets/tab3_institutional_ratios.png)

### Tab 4 — Export
Download all trades, wins only, or losses only as CSV at $10,000/trade. Generate PDF stakeholder report.

![Export Tab](assets/tab4_export.png)

---

## 📋 Exit Architecture

```
ENTRY (100%) → TP1 (50% swing) → TP2 (100% swing ★) → TP3 (1.618× swing)
  Close 5%         Close 75%            Close 20%

SL Behaviour:
  Entry → TP1  :  SL at original divergence swing point — full position at risk
  TP1  → TP2   :  SL unchanged — 95% still fully exposed
  After TP2    :  SL trails to TP1 price — remaining 20% is risk-free
```

**Why this structure works:** TP2 hits 74.1% of the time — the same rate as the overall win rate. This means every winning trade reaches the primary exit where 75% of capital is closed. Once TP2 fires, the trade cannot close at a net loss.

---

## 📁 Repository Structure

```
rsi-divergence-backtest/
├── README.md                        ← This file
├── dashboard.html                   ← Full interactive dashboard (open in browser)
└── assets/
    ├── tab1_backtest_results.png    ← Backtest Results tab screenshot
    ├── tab1_charts.png              ← Charts & equity curve screenshot
    ├── tab3_institutional_ratios.png← Institutional Ratios tab screenshot
    └── tab4_export.png              ← Export tab screenshot
```

---

## 🔍 What's Intentionally Not Disclosed

This repository shares full backtest results, institutional ratios, trade-level data, and methodology — but keeps the following proprietary:

- Exact entry trigger logic
- RSI threshold parameters
- Swing detection lookback values used in signal generation
- Any Pine Script or live implementation code

---

## 🛠️ Methodology Notes

- **Data source:** Binance OHLCV via public API — real tick-accurate 5-minute candles
- **No lookahead bias:** Signal detection uses only closed candles; entry occurs on the close of the trigger candle
- **No curve fitting:** Exit structure (5/75/20 split, TP levels, SL mode) was set logically and validated — not optimised to the data
- **Fee scenarios tested:** Taker/Taker (0.10%), Maker/Taker (0.07%), Maker/Maker (0.04%)
- **Strategy is profitable under all fee scenarios**
- **Recency check:** 2024+ performance comparable to pre-2024 on a per-trade basis — edge has not decayed

---

## 👤 About

**Akshat Vaishya**  
Associate — Trade Operations, SS&C GlobeOp, Navi Mumbai  
Servicing Citadel across equities, derivatives, fixed income, and crypto/digital assets reconciliation  
Previously: Senior Analyst, Global Custody Reconciliation, eClerx (Goldman Sachs client)  
Education: BAF, Pillai's College, Mumbai University

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://linkedin.com/in/akshat-vaishya)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=flat&logo=github)](https://github.com/akshatvaishya16-hub)

---

*Backtest conducted on real Binance OHLCV data. Past performance does not guarantee future results. This is not financial advice.*
