# Post-Freeze Candidates

v1.0 の仕様は凍結されています。新しい概念・分類・手順が必要に見えた場合、仕様には採用せず、ここに候補として記録します。

ここに記録された項目は、v1.0 の一部ではありません。採否は Human Review で決めます。

## 記録テンプレート

```markdown
### PFC-<番号>: <短い名前>

- 記録日:
- きっかけ: <test-log.md のエントリ、または作業内容>
- 観察されたこと:
- 現行 v1.0 での扱い: <OTHER で記録した / 既存の Finding Type で代用した / 扱えなかった>
- 候補の内容:
- 状態: 未検討 / 検討中 / 不採用 / 次版候補
```

## 候補

### PFC-001: 部分的に Source がある場合の扱い

- 記録日: 2026-10-06
- きっかけ: v1.0 初期構築（workflow / prompts の作成時）
- 観察されたこと: 仕様は Mode A（Source あり）と Mode B（成果物のみ）の 2 つを定義しているが、一部の主張にだけ Source がある場合の扱いは定義されていない
- 現行 v1.0 での扱い: Mode A として監査し、Source の無い Meaning Unit は `UNKNOWN` とし、Source Verification Required に記載する（新しいモードは作らない）
- 候補の内容: 混在ケースを独立したモードとして扱うかどうか
- 状態: 未検討

### PFC-002: AI が図・画像を読めない場合の Visual Claim の扱い

- 記録日: 2026-10-06
- きっかけ: v1.0 初期構築（Class A の重点観点をプロンプト化する際）
- 観察されたこと: Class A では Visual Claim が重点だが、実行環境によっては AI が図を読めない、またはテキスト抽出のみになる
- 現行 v1.0 での扱い: 読めない要素は推測で記述せず、Limitations に記載する
- 候補の内容: 図の記述を人間が事前に用意する入力欄を設けるかどうか
- 状態: 未検討

### PFC-003: 成果物の中の不整合を表す Finding Type

- 記録日: 2026-10-06
- きっかけ: Test 01-1（Run 01B）
- 観察されたこと: 提供数の表記（「○○本以上」「○○種類以上」と画面上の件数表示）、社名表記の違い、「契約書の雛形」と「申込書雛形」など、意味の変形というより成果物の中の数量・表記・時期の食い違いが複数見つかった
- 現行 v1.0 での扱い: OTHER で記録した（F-23, F-26）。他の一部は CONTEXT_LOSS（F-24）や VISUAL_CLAIM（F-01）で代用した
- 候補の内容: 成果物の中の不整合を Finding Type として独立させるか、情報状態 CONFLICTING で足りるとするか
- Test 01-1 の Evidence: F-23（提供本数の表記、OTHER）、F-26（雛形の種類、OTHER）、F-24（社名表記、CONTEXT_LOSS で代用）、F-01（数値の不一致、VISUAL_CLAIM で代用）。公開版 Report: [test-01-1-public.md](../examples/01-ai-presentation/audit/test-01-1-public.md)
- 状態: 未検討

### PFC-004: 生成過程の来歴（Provenance）の記録

- 記録日: 2026-10-06
- きっかけ: Test 01-1（Audit Object が AI 生成かどうかを資料から判別できなかった）
- 観察されたこと: Test 01 は「AI 生成プレゼン」を対象にしているが、生成ツール・AI の関与の範囲・人による編集の有無は成果物から特定できない。監査者は、作成過程による Meaning Shift と編集の意図による Meaning Shift を区別できないことを Limitations に書いた
- 現行 v1.0 での扱い: Audit Object の「作成者 / 生成元」欄を UNKNOWN とし、Limitations に記載した
- 候補の内容: 生成過程の来歴（どの部分を AI が生成し、どこを人が編集したか）を、監査の入力または Report の項目として扱うかどうか
- Test 01-1 の Evidence: 公開版 Report の 1. Audit Object（作成者 / 生成元 UNKNOWN）と 13. Limitations。Human Review HR-01 で、Test 01-1 は Generation Provenance Unknown として扱うことになった（[test-01-1-human-review.md](../examples/01-ai-presentation/review/test-01-1-human-review.md)）
- 状態: 未検討（HR-01 により維持）
