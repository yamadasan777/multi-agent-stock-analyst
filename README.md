# マルチエージェント株式分析システム

Claude Code のマルチエージェント基盤を活用した株式分析システム。
1つの要求に対してコーディネーターが関連する専門エージェントを自動選択・並列実行し、統合レポートとして返します。

## アーキテクチャ

```
ユーザー: "/stock-analyst AAPLの決算を分析して"
    ↓
コーディネーター (SKILL.md)
    ↓ エージェント自動選択
    ├─ jpm-earnings (決算分析)  ─┐
    ├─ ms-technical (テクニカル) ┤→ 並列実行 → 結果を統合
    └─ bw-risk (リスク評価)    ──┘
    ↓
統合レポート（エグゼクティブサマリー + 各エージェント詳細）
```

## セットアップ

### 前提条件

- [Claude Code](https://claude.ai/code) がインストール済みであること

### インストール

```bash
git clone <このリポジトリ>
cd stock-analyst
```

Claude Code でこのディレクトリを開くと、`.claude/` 配下のスキル・エージェント定義が自動的に読み込まれます。

## 使い方

Claude Code のチャットで `/stock-analyst` コマンドを使います。

### 基本構文

```
/stock-analyst <分析したい内容>
```

### 使用例

#### 個別銘柄の総合分析

```
/stock-analyst AAPLを分析して
/stock-analyst NVDAの投資判断をして
/stock-analyst TSLAは今買いか教えて
```

→ **起動エージェント**: テクニカル分析 + リスク評価 + DCFバリュエーション

#### 決算分析

```
/stock-analyst AAPLの決算を分析して
/stock-analyst GOOGLの今期決算はどうだった？
```

→ **起動エージェント**: 決算分析 + テクニカル分析 + リスク評価

#### 配当・インカム投資

```
/stock-analyst 配当株をスクリーニングして
/stock-analyst JNJの配当は安全か確認して
```

→ **起動エージェント**: 配当分析 + リスク評価（+ ETFポートフォリオ）

#### 投資候補スクリーニング

```
/stock-analyst 割安な成長株をスクリーニングして
/stock-analyst テクノロジーセクターのおすすめ銘柄を教えて
```

→ **起動エージェント**: Goldmanスクリーナー + Renaissanceクオンツ

#### ポートフォリオ構築

```
/stock-analyst ETFポートフォリオを作って
/stock-analyst 30代向けのポートフォリオを提案して
```

→ **起動エージェント**: ETFポートフォリオ + リスク評価 + セクターローテーション

#### 市場全体の分析

```
/stock-analyst 今の市場環境を教えて
/stock-analyst 今後6ヶ月の相場見通しは？
```

→ **起動エージェント**: マクロ分析 + セクターローテーション + クオンツ

## 専門エージェント一覧

| エージェントID | 金融機関モデル | 専門領域 |
|---|---|---|
| `gs-screener` | Goldman Sachs | 銘柄スクリーニング・ファンダメンタル評価 |
| `ms-technical` | Morgan Stanley | テクニカル分析・チャートパターン・モメンタム |
| `bw-risk` | Bridgewater Associates | リスク評価・ボラティリティ・ヘッジ戦略 |
| `jpm-earnings` | JPMorgan Chase | 決算分析・EPS予測・決算後トレード戦略 |
| `br-dividend` | BlackRock | 配当分析・インカム投資・配当安全性評価 |
| `citadel-sector` | Citadel | セクターローテーション・経済サイクル分析 |
| `ren-quant` | Renaissance Technologies | クオンツ多因子スクリーニング・因子分析 |
| `vanguard-etf` | Vanguard | ETFポートフォリオ構築・アセットアロケーション |
| `mck-macro` | McKinsey Global Institute | マクロ経済分析・Fed政策・グローバルリスク |
| `ms-dcf` | Morgan Stanley | DCFバリュエーション・適正株価算出 |

コーディネーターが要求内容に応じて2〜5のエージェントを自動選択・並列実行します。

## ファイル構成

```
stock-analyst/
├── README.md
├── agents/                          # エージェント定義の原典（参照用）
│   ├── 1. The Goldman Sachs Stock Screener.md
│   ├── 2. The Morgan Stanley Technical Analysis Dashboard.md
│   └── ... (10ファイル)
└── .claude/
    ├── agents/                      # サブエージェント定義（Claude Code が自動読み込み）
    │   ├── gs-screener.md
    │   ├── ms-technical.md
    │   ├── bw-risk.md
    │   ├── jpm-earnings.md
    │   ├── br-dividend.md
    │   ├── citadel-sector.md
    │   ├── ren-quant.md
    │   ├── vanguard-etf.md
    │   ├── mck-macro.md
    │   └── ms-dcf.md
    └── skills/
        └── stock-analyst/
            ├── SKILL.md             # コーディネーター（エントリポイント）
            └── references/
                ├── agents-catalog.md    # エージェント選択ルーティングマップ
                └── report-format.md     # 統合レポートテンプレート
```

## 出力形式

統合レポートは以下の構成で出力されます：

1. **エグゼクティブサマリー** — テクニカル・リスク・バリュエーション等の判断を表形式で要約
2. **総合評価** — STRONG BUY / BUY / HOLD / SELL / STRONG SELL の明確な推奨
3. **エージェント別詳細分析** — 各専門エージェントの完全な分析レポート
4. **統合見解** — 複数エージェントが一致する強気・弱気サイン、意見の相違、アクションプラン
5. **免責事項**

## 注意事項

- 本システムの分析は投資アドバイスではありません
- 投資判断は自己責任で行ってください
- 必要に応じて認定ファイナンシャルアドバイザーにご相談ください
- 過去のパフォーマンスは将来の結果を保証するものではありません
