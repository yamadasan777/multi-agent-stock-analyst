# Agent Catalog — Quick Reference

> Note: Full catalog is now inlined in SKILL.md. This file is kept for reference only.

| Agent ID | subagent_type | Specialty |
|---|---|---|
| `gs-screener` | gs-screener | Stock screening & fundamental quality ranking |
| `ms-technical` | ms-technical | Technical analysis, chart patterns, momentum |
| `bw-risk` | bw-risk | Risk assessment, volatility, drawdown, hedging |
| `jpm-earnings` | jpm-earnings | Earnings analysis, EPS estimates, post-earnings plays |
| `br-dividend` | br-dividend | Dividend analysis, income projection, yield safety |
| `citadel-sector` | citadel-sector | Sector rotation, economic cycle positioning |
| `ren-quant` | ren-quant | Quantitative multi-factor screening |
| `vanguard-etf` | vanguard-etf | ETF portfolio construction, asset allocation |
| `mck-macro` | mck-macro | Macroeconomic analysis, Fed policy, global risks |
| `ms-dcf` | ms-dcf | DCF valuation, intrinsic value, WACC |

## Selection Rules

1. Min 2, Max 5 agents per request
2. Always include `bw-risk` for individual stock analysis
3. Parallel execution by default
