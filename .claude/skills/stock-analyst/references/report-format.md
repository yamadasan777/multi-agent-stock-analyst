# Integrated Stock Analysis Report Template

Use this template when assembling the final integrated report from multiple agent outputs.
The coordinator fills in the Executive Summary and Integrated Insights sections.
Agent outputs are inserted verbatim into the Agent Details section.

---

## Template

```markdown
# 株式分析統合レポート

**分析日時**: {DATE_TIME}
**分析対象**: {TARGET} ({TICKER if applicable})
**実行エージェント**: {AGENT_LIST}
**分析タイプ**: {ANALYSIS_TYPE}

---

## エグゼクティブサマリー

| 観点 | 判断 | 信頼度 |
|---|---|---|
| テクニカル | {BULLISH/NEUTRAL/BEARISH} | {HIGH/MEDIUM/LOW} |
| リスク | {LOW/MEDIUM/HIGH} | {HIGH/MEDIUM/LOW} |
| バリュエーション | {UNDERVALUED/FAIR/OVERVALUED} | {HIGH/MEDIUM/LOW} |
| 決算 | {BEAT/IN-LINE/MISS EXPECTED} | {HIGH/MEDIUM/LOW} |
| 配当 | {SAFE/WATCH/DANGER} | {HIGH/MEDIUM/LOW} |

*(Include only rows relevant to executed agents)*

**総合評価**: {1-2 sentence overall verdict in Japanese}

**最終推奨**: {STRONG BUY / BUY / HOLD / SELL / STRONG SELL}

**投資期間**: {SHORT-TERM (< 3months) / MEDIUM-TERM (3-12months) / LONG-TERM (> 1year)}

---

## エージェント別詳細分析

{INSERT EACH AGENT OUTPUT VERBATIM HERE}

*(Each agent's output begins with its ### [agent-id] header)*

---

## 統合見解

### 強気サイン（複数エージェント一致）
- {Bullish signal confirmed by 2+ agents}
- {Bullish signal confirmed by 2+ agents}

### 弱気サイン（複数エージェント一致）
- {Bearish signal confirmed by 2+ agents}
- {Bearish signal confirmed by 2+ agents}

### エージェント間の意見の相違
- {Agent A} vs {Agent B}: {Description of disagreement and how to interpret it}

### リスク・リワード評価
- **上値余地**: {Upside potential with price target if available}
- **下値リスク**: {Downside risk with stop-loss level if available}
- **リスク・リワード比**: {Ratio if calculable}

### アクションプラン
1. **即時アクション**: {What to do right now}
2. **監視事項**: {What to watch and when to act}
3. **出口戦略**: {When/how to exit the position}

---

## 免責事項

本レポートはAIエージェントによる分析であり、投資アドバイスではありません。
投資判断は自己責任で行い、必要に応じて認定ファイナンシャルアドバイザーにご相談ください。
過去のパフォーマンスは将来の結果を保証するものではありません。
```

---

## Coordinator Writing Guidelines

### Executive Summary
- Write in Japanese
- Be decisive — give a clear recommendation, not "it depends"
- Confidence level: HIGH = multiple agents agree, MEDIUM = mixed signals, LOW = significant disagreement
- Overall verdict: synthesize all agent inputs into 1-2 clear Japanese sentences

### Integrated Insights
- Bullish/Bearish signs: only include signals confirmed by 2+ agents
- Disagreements: acknowledge honestly — don't paper over conflicts
- Action plan: concrete, specific, actionable — not vague advice
- Keep each bullet point to 1-2 sentences max

### Tone
- Professional but accessible
- Use Japanese for all user-facing text
- Agent section headers remain in English (as defined by each agent's output format)
