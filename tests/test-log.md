# Test Log

Meaning Audit Workflow v1.0 のテスト実行記録です。1 回の監査実行につき 1 エントリを追加します。

テストケースは代表的な文書種類を集めたものではなく、異なる Meaning Transformation を観察するためのものです。

## テストケース一覧

| Test | 対象 | 想定 Class | 想定 Mode | 状態 |
|---|---|---|---|---|
| 01-1 | Presentation Artifact — Generation Provenance Unknown | A | Artifact-Only | FROZEN — FIELD EVIDENCE |
| 01-2 | NotebookLM Presentation — Human-Directed Focus | A（主）/ C（副次） | Source-Grounded（Source Set: PARTIALLY KNOWN）＋ Artifact-Only（Blind） | FROZEN — FIELD EVIDENCE |
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
- Human Review Status: 一部実施（HR-01, HR-02、FP-005 の暫定判断）。R-3〜R-9 は整理済みで Human Decision 待ち。公開版と原本の Meaning Preservation は AI による照合済み（UNCERTAIN 2 件）で Human 確認待ち
- Public 版の一般化: 2026-10-06 に、Finding の成立に不要な原値（金額・割合・件数など）を一般化した。同日、一般化する前の版を git の履歴からも除去した（`git filter-repo` による履歴の書き換えと force-with-lease push）。書き換え前のコミットは、GitHub 上で SHA を直接指定すると引き続き表示される

```text
Test 01-1 Status:
FREEZE CANDIDATE — HUMAN REVIEW REQUIRED
```

#### 観察

- Key Observation: Source が無くても、成果物の中の検算とページをまたいだ照合で、具体的な Finding が多く得られた。一方、事例・実績・お客様の声といった影響の大きい主張ほど UNTRACEABLE / UNKNOWN になった。資料を画像で入力すれば、Visual Claim（グラフと数値の不一致、見出しとグラフのずれ、象限図、目盛りの無い比較）も監査できた
- Workflow どおりに動いたこと: 13 セクションがすべて揃った。Mode B の定型文があり、誤りの断定・修正案・点数は無かった。Human Decision 欄は空欄のまま。Meaning Trace の 7 Stage はすべて埋まった。主セッションが 5 ページで読み取りを照合し、すべて一致した
- Workflow Failure: FP-001〜FP-006（[failure-patterns.md](failure-patterns.md)）。確定判定はしていない
- 新しい概念の候補: PFC-003, PFC-004（[post-freeze-candidates.md](post-freeze-candidates.md)）。採用はしていない
- テスト設計上の問題: Run 01A / 01B の比較を前提にしたが、Source が無く比較できなかった。AI 生成であることが確認できず、Test 01 本来の対象（AI-Generated Presentation）の条件を満たさなかった

#### Workflow / Prompt の修正

- 修正しない。FP-005 の Human Review 暫定判断（成果物内部の数値のみを使った算術的検算は External Knowledge とみなさない）は、Workflow 改訂の候補として保持する

### 2026-10-06 Test 01-1 Skill Compatibility Check

- 目的: `skills/meaning-audit` と既存 Prompt（`prompts/artifact-only-audit.md`）の互換性を確認する（新しい Finding を正解として扱わない）
- 対象: Test 01-1 と同じ監査対象・同じ入力形式
- Audit Model: Claude Opus 5.5（文脈を持たない subagent。SKILL.md と references/ のみを参照）
- 結果: 13 セクション、Mode B の自動判定と定型文、禁止事項の遵守、Human Decision の空欄はすべて一致。Run 01B の Finding 26 件中、一致 21・一部一致 4・不一致 1。Skill Run のみの Finding 4 件。KS は 7 件中 5 件が一致。Document Class の主副が逆になった
- 記録: [test-01-1-skill-compatibility.md](../examples/01-ai-presentation/review/test-01-1-skill-compatibility.md)。Skill Run の Report 原本は Private Evidence Vault
- Human Review Status: 未実施（SC-1〜SC-4）

### 2026-10-06 Skill Runtime and Variance Validation

- 目的: Skill の実行ごとのばらつきの観察（S2, S3 を追加）と、実際の Claude Code へのインストールでの動作確認
- Human Review Decisions: SC-1 ACCEPT（Workflow compatible。output equivalent とは表現しない）、SC-2 ACCEPT、SC-3 HOLD（Run Variance / Compatibility Delta として記録）、SC-4 REVISE（Packaging Revision として実施）
- Variance Test: Run 01B と Skill Run S1〜S3 の 4 Run を cluster で比較。34 cluster のうち 23 が 4/4、3 が 3/4、2 が 2/4、6 が 1/4。Status は 4/4 の cluster のうち 11 で変動した。Finding 数は 26〜31
- Runtime Test: Personal Skill としてインストールし、`/meaning-audit` と自然言語の依頼（「Meaning Audit」を含む）の両方で Skill が動き、13 セクションの Report を出した
- 記録: [skill-runtime-validation.md](../examples/01-ai-presentation/review/skill-runtime-validation.md)。各 Run の Report 原本は Private Evidence Vault
- Skill の調整: していない（観察のみ）
- Human Review Status: RV-1〜RV-5 未実施

### 2026-10-06 Test 01-1 Final Human Decision Preparation

- Human Decision: F-05 → REVISE、F-23 → REVISE（どちらも公開版に反映済み）。Meaning Preservation は YES 26 / UNCERTAIN 0 / NO 0
- R-3〜R-9 は [test-01-1-final-decision-packet.md](../examples/01-ai-presentation/review/test-01-1-final-decision-packet.md) にまとめた（12 件、Human Decision 待ち）
- 書き換え前の履歴の扱いについての Human Decision は Private Evidence Vault に記録した

```text
Test 01-1 Status:
FREEZE CANDIDATE — HUMAN REVIEW REQUIRED
```

### 2026-10-06 Meaning Audit Skill Final Human Review

- Human Decision: RV-1 ACCEPT（表現を限定）、RV-2 HOLD（Runtime Variance Observation として保持）、RV-3 INVESTIGATE（Prompt Run P2・P3 を実施）、RV-4 HUMAN REVIEW REQUIRED / HOLD、RV-5 ACCEPT。Skill 固有の運用上の指示 A〜D は ACCEPT
- Prompt Run P2・P3: 主 Class は P2 が C、P3 が A。既存 Prompt の 3 Run は A・C・A、Skill の 3 Run は C・C・C。RV-3 は Case B（A / C が混在）
- Skill Public Status: PUBLICLY USABLE — WORKFLOW v1.0 IMPLEMENTATION（installable implementation of Meaning Audit Workflow v1.0。Release tag は未作成）
- 記録: [skill-runtime-validation.md](../examples/01-ai-presentation/review/skill-runtime-validation.md) の 9〜12

### 2026-10-06 Test 01-1 Freeze

- Human Decision（R-3〜R-9）: F-01 ACCEPT、F-04 ACCEPT、F-07 ACCEPT、F-12 REVISE、F-14 REVISE、F-20 REVISE、F-22 REVISE、F-24 HOLD、F-03 NO ACTION、F-18 HOLD、Run 01A NO ACTION、Finding Granularity HOLD
- 公開版 Report に反映した修正: F-12（情報状態 CONFLICTING → KNOWN）、F-14（母数の推測を外し、情報状態 UNKNOWN）、F-20（Observation と Interpretation を分離）、F-22（Status → UNKNOWN）。F-24 は Human Review 注記のみ。Finding 番号は変更していない
- 公開履歴: 書き換え前のコミットを指す SHA の文字列を、公開リポジトリの履歴から除いた（git filter-repo と force-with-lease push）。Public repository history から旧コミットへの公開上の発見経路を除去した。GitHub 内部に参照されないオブジェクトが残っている可能性はあり、GitHub Support への削除依頼はしていない
- 維持したもの: FP-001〜FP-006、PFC-003、PFC-004、Skill Runtime Variance Observation、Generation Provenance UNKNOWN、Run 01A 未実行

```text
Test 01-1 Status:
FROZEN — FIELD EVIDENCE
```

FROZEN — FIELD EVIDENCE は、このテストで起きたこと、AI の Audit Report、Human Review、Finding の修正、失敗の観察、Unknown を Field Evidence として固定したことを意味する。Workflow v1.0 が validated されたこと、Finding が普遍的に正しいこと、AI Audit の再現性が保証されたこと、Method が final であることは意味しない。


### 2026-10-06 Test 01-2: NotebookLM Presentation — Human-Directed Focus

- 対象: [examples/01-ai-presentation](../examples/01-ai-presentation/)
- Date: 2026-10-06
- Audit Object: NotebookLM で生成されたプレゼンテーション資料。リポジトリには置いていない
- Generation Tool: NotebookLM ／ Post-generation Human Editing: NONE（いずれも Human の申告）
- Human-directed Focus: あり（Human 由来の編集意図。Test Metadata として記録）
- Source Set: PARTIALLY KNOWN（既知の Source 2 点 ＋ 特定できていない Web Source）
- Run 02A: Mode A（Source-Grounded） — COMPLETED。Prompt: `prompts/source-grounded-audit.md`（無改変）
- Run 02B: Mode B（Artifact-Only、Blind） — COMPLETED。Source・Generation Provenance・Run 02A の結果を渡さずに実行。Skill `meaning-audit` を使用
- Comparison（Run 02A / 02B）: COMPLETED
- Human Review: COMPLETED（Human Visual Confirmation を含む）
- Document Class: Presentation / Visualization（主）/ Proposal / Analysis / Decision Document（副次）
- Evidence / Reports: すべて Private（PUBLIC SUMMARY ONLY。Public Summary は未作成）

#### 観察（一般化）

- Workflow どおりに動いたこと:
  - Source Set が一部しか既知でない状態でも、Mode A のまま進め、既知の Source で確認できない Claim を `UNKNOWN` として保持する運用が機能した
  - Generation Provenance と Human-directed Focus が既知であることで、Human が与えた Focus 自体を Framing の Finding にせず、その内側の Meaning Shift だけを対象にできた
  - Source がある場合、Meaning Trace の Evidence / Source 欄に原文を置けるため、Stage 間の差が特定しやすかった
- 記録した課題（Failure Pattern・Post-Freeze Candidate としては登録していない）:
  - Source と Artifact の間で規範的な強さが変化する例があった。既存の Status では、「Source が同じ論点をより弱く扱っている」場合と「Source に記述が無い」場合が同じラベルになりうる
  - Source Set が PARTIALLY KNOWN のときの UNSUPPORTED の使い方。Human Decision: 成果物が特定の既知 Source に明示的に帰属している場合は UNSUPPORTED を使用でき、帰属が明示されていない Claim は UNKNOWN を優先する
  - Finding ID の枝番、Finding Type 欄への Status の語の記入、1 Finding に複数 Status といった Runtime Deviation が Run 02A にあった（原本は変更せず、正式な表記としては採用しない）
  - テキスト層の無い成果物で、転記と図の読み取りが Run 間で分かれた（Errata で訂正。原本は変更しない）
  - 同じ現象を、一方の Run は Meaning Trace に記述し、もう一方は Finding として起票するという記録の差があった
- Comparison で挙がった Failure Pattern 候補 7 件は、すべて HOLD（採番しない、既存の FP 系列へ統合しない、Workflow へ反映しない）。Test 01-2 の Field Evidence としてのみ保持する
- Candidate Interpretations（Artifact-Only Audit の検出範囲、Source による判定の分解、Traceability と Support の違い、Source による疑念の解消）は Human-reviewed interpretation candidate として保持し、理論上の結論にはしない。Traceability と Support の違いは、Workflow の既存定義の確認でもある

#### Limitations

- Run 02A は完全な独立コンテキストではない（記録構造の作成のため本 test-log と Test 01 の README を読んだ同一コンテキストで実行）
- Run 02B は、開始前の計画と異なる Prompt（Skill）と入力解像度で実行した
- Comparison は Run 02B と同じ監査者・同じセッションで実施した

#### Workflow / Prompt / Skill の修正

- 修正しない。failure-patterns.md と post-freeze-candidates.md も変更していない

```text
Test 01-2 Status:
FROZEN — FIELD EVIDENCE
```

FROZEN — FIELD EVIDENCE は、Run 02A、Run 02B、Comparison、Human Review、Errata、Runtime Deviations、Remaining Unknowns、Candidate Interpretations、Failure Pattern 候補を Field Evidence として固定したことを意味する。Workflow v1.0 が validated されたこと、Source-Grounded Audit が完全であること、Artifact-Only Audit の再現性が保証されたこと、Failure Pattern 候補が正式に採用されたこと、Candidate Interpretations が理論として確定したこと、未特定の Web Source が存在しないことは意味しない。
