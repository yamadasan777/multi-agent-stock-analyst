# Agent Catalog - Stock Analyst Routing Map

This file defines which agents to select based on user request type.
The coordinator reads this to make agent selection decisions.

## Agent Definitions

| Agent ID | File | Specialty | Best For |
|---|---|---|---|
| `gs-screener` | `~/.claude/agents/gs-screener.md` | Stock screening & fundamental quality ranking | Finding investment candidates, top picks by criteria |
| `ms-technical` | `~/.claude/agents/ms-technical.md` | Technical analysis, chart patterns, momentum | Entry/exit timing, trend analysis, trade setups |
| `bw-risk` | `~/.claude/agents/bw-risk.md` | Risk assessment, volatility, drawdown, hedging | Risk evaluation, portfolio protection, stress testing |
| `jpm-earnings` | `~/.claude/agents/jpm-earnings.md` | Earnings analysis, EPS estimates, post-earnings plays | Earnings events, quarterly results, EPS beat/miss |
| `br-dividend` | `~/.claude/agents/br-dividend.md` | Dividend analysis, income projection, yield safety | Income investing, dividend stocks, passive income |
| `citadel-sector` | `~/.claude/agents/citadel-sector.md` | Sector rotation, economic cycle positioning | Sector allocation, which sectors to buy/avoid |
| `ren-quant` | `~/.claude/agents/ren-quant.md` | Quantitative multi-factor screening | Data-driven ranking, factor analysis, systematic screening |
| `vanguard-etf` | `~/.claude/agents/vanguard-etf.md` | ETF portfolio construction, asset allocation | Building diversified portfolios, ETF selection |
| `mck-macro` | `~/.claude/agents/mck-macro.md` | Macroeconomic analysis, Fed policy, global risks | Market outlook, economic environment, macro impact |
| `ms-dcf` | `~/.claude/agents/ms-dcf.md` | DCF valuation, intrinsic value, WACC | Fair value estimation, undervalued/overvalued verdict |

---

## Selection Rules

### Rule 1: Minimum 2, Maximum 5 agents per request
- Never invoke fewer than 2 agents
- Never invoke more than 5 agents (avoid over-analysis)
- Choose the most relevant agents for the request type

### Rule 2: Always include bw-risk for individual stock analysis
- Any single-stock analysis should include risk assessment

### Rule 3: Sequential execution (exceptions only)
- Default: parallel execution of all selected agents
- Sequential only when: gs-screener results must feed into ms-dcf (explicit screening → valuation flow)

---

## Use Case → Agent Selection Patterns

### Individual Stock Comprehensive Analysis
**Triggers**: "[TICKER] を分析", "[TICKER] analysis", "buy or sell [TICKER]", "[TICKER] の投資判断"
**Agents**: `ms-technical` + `bw-risk` + `ms-dcf` (core 3)
**Add if relevant**:
- + `jpm-earnings` if earnings mentioned or upcoming
- + `br-dividend` if dividend/income mentioned

### Earnings Analysis
**Triggers**: "決算", "earnings", "EPS", "quarterly results", "earnings date"
**Agents**: `jpm-earnings` + `ms-technical` + `bw-risk`

### Valuation / Fair Value
**Triggers**: "割安", "割高", "fair value", "intrinsic value", "DCF", "undervalued", "overvalued", "price target"
**Agents**: `ms-dcf` + `bw-risk` + `ms-technical`

### Investment Candidate Screening
**Triggers**: "スクリーニング", "screen", "find stocks", "best stocks", "おすすめ銘柄", "どの株"
**Agents**: `gs-screener` + `ren-quant` (+ `mck-macro` if market context needed)

### Dividend / Income Investing
**Triggers**: "配当", "dividend", "income", "passive income", "yield", "配当株"
**Agents**: `br-dividend` + `bw-risk` (+ `vanguard-etf` if portfolio construction needed)

### Portfolio Construction
**Triggers**: "ポートフォリオ", "portfolio", "asset allocation", "ETF", "diversify", "build portfolio"
**Agents**: `vanguard-etf` + `bw-risk` + `citadel-sector`

### Market / Macro Outlook
**Triggers**: "市場環境", "market outlook", "economy", "Fed", "inflation", "macro", "recession", "今の相場"
**Agents**: `mck-macro` + `citadel-sector` (+ `ren-quant` for quantitative confirmation)

### Sector Analysis
**Triggers**: "セクター", "sector", "industry rotation", "which sector to buy"
**Agents**: `citadel-sector` + `mck-macro` + `bw-risk`

### Technical Trading
**Triggers**: "テクニカル", "chart", "support", "resistance", "entry point", "trade setup", "RSI", "MACD"
**Agents**: `ms-technical` + `bw-risk`

---

## Decision Priority

When request type is ambiguous, apply this priority:
1. Check for specific ticker → use individual stock pattern
2. Check for earnings keywords → use earnings pattern
3. Check for screening keywords → use screening pattern
4. Check for portfolio/ETF keywords → use portfolio pattern
5. Default to: `ms-technical` + `bw-risk` + `ms-dcf` (general stock analysis)
