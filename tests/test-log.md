# Test Log

Meaning Audit Workflow v1.0 のテスト実行記録です。1 回の監査実行につき 1 エントリを追加します。

テストケースは代表的な文書種類を集めたものではなく、異なる Meaning Transformation を観察するためのものです。

## テストケース一覧

| Test | 対象 | 想定 Class | 想定 Mode | 状態 |
|---|---|---|---|---|
| 01 | AI-Generated Presentation | A | 未定（元資料の有無による） | 未実施 |
| 02 | Published Article | B | 未定 | 未実施 |
| 03 | Proposal / Analysis Document | C | 未定 | 未実施 |

## 記録テンプレート

```markdown
### <YYYY-MM-DD> Test <番号>-<実行番号>

- 対象: <examples/ のディレクトリ名>
- Prompt: <ファイル名 / バージョン>
- Model: <モデル名・環境（Claude Code / ChatGPT など）>
- Audit Mode（AI の判定）:
- Document Class（AI の判定）:
- Report: <audit/ 内のファイル名>
- Human Review: <review/ 内のファイル名 / 未実施>

#### 観察

- Workflow どおりに動いたこと:
- 動かなかったこと（→ failure-patterns.md）:
- 新しい概念が必要に見えたこと（→ post-freeze-candidates.md）:

#### Workflow / Prompt の修正

- 修正した / 修正しない（理由）:
```

## 実行記録

### 2026-10-06 Test 01-1: Presentation Artifact — Generation Provenance Unknown

- 対象: [examples/01-ai-presentation](../examples/01-ai-presentation/)
- Date: 2026-10-06
- Audit Object: 第三者企業（Company A）のサービス紹介資料（PDF, 36 ページ）。匿名化して記録し、原本は Private Evidence Layer に保管（HR-02）
- Generation Provenance: UNKNOWN（AI 生成であることは確認できなかった。HR-01）
- Generation Tool: UNKNOWN
- Audit Model: Claude Opus 5.5（Claude Code の subagent。この会話の文脈を持たない状態で実行）
- Input Format: ページ画像（PNG 110 dpi × 36）＋ PDF テキスト層（一部のページのみ）
- Prompt: `prompts/artifact-only-audit.md`（無改変）
- Audit Mode: Artifact-Only
- Document Class: Presentation / Visualization（AI の判定では Class C を副次 Class として併記）
- Run 01A（Source-Grounded）: 未実行（Source が提供されなかった）
- Run 01B（Artifact-Only）: 実行
- 件数: Meaning Unit 32、Finding 26（PARTIALLY TRACEABLE 14、UNTRACEABLE 12、TRACEABLE 0、UNKNOWN 0）、Key Meaning Shift 7、Critical Unknown 8、Source Verification Required 14、Human Review Required 17
- Public Report: [test-01-1-public.md](../examples/01-ai-presentation/audit/test-01-1-public.md)（匿名化）
- Human Review: [test-01-1-human-review.md](../examples/01-ai-presentation/review/test-01-1-human-review.md)
- Comparison: [mode-comparison.md](../examples/01-ai-presentation/review/mode-comparison.md)（Run 01A が無いため限定的）
- Human Review Status: 一部実施（HR-01, HR-02、FP-005 の暫定判断）。R-3〜R-9 は未判断

#### 観察

- Key Observation: Source が無くても、成果物の中の検算とページをまたいだ照合で、具体的な Finding が多く得られた。一方、事例・実績・お客様の声といった影響の大きい主張ほど UNTRACEABLE / UNKNOWN になった。資料を画像で入力すれば、Visual Claim（グラフと数値の不一致、見出しとグラフのずれ、象限図、目盛りの無い比較）も監査できた
- Workflow どおりに動いたこと: 13 セクションがすべて揃った。Mode B の定型文があり、誤りの断定・修正案・点数は無かった。Human Decision 欄は空欄のまま。Meaning Trace の 7 Stage はすべて埋まった。主セッションが 5 ページで読み取りを照合し、すべて一致した
- Workflow Failure: FP-001〜FP-006（[failure-patterns.md](failure-patterns.md)）。確定判定はしていない
- 新しい概念の候補: PFC-003, PFC-004（[post-freeze-candidates.md](post-freeze-candidates.md)）。採用はしていない
- テスト設計上の問題: Run 01A / 01B の比較を前提にしたが、Source が無く比較できなかった。AI 生成であることが確認できず、Test 01 本来の対象（AI-Generated Presentation）の条件を満たさなかった

#### Workflow / Prompt の修正

- 修正しない。FP-005 の Human Review 暫定判断（成果物内部の数値のみを使った算術的検算は External Knowledge とみなさない）は、Workflow 改訂の候補として保持する
