# Failure Patterns

Workflow またはプロンプトが、仕様どおりに動かなかった事例を記録します。目的は Workflow v1.0 を修正可能にすることで、AI モデルの優劣を比べることではありません。

## 記録の対象

- プロンプトの指示に従わなかった（例: Mode B で「誤り」と断定した、修正案を出した、点数を付けた）
- UNKNOWN が推測で埋められた
- INFERRED が KNOWN として扱われた
- 13 セクションが欠けた・順序が崩れた
- Meaning Trace の Stage が空欄になった
- Audit Mode / Document Class の判定が不適切だった
- Workflow の手順自体が曖昧・矛盾していて、実行できなかった

## 記録テンプレート

```markdown
### FP-<番号>: <短い名前>

- 初出: <test-log.md のエントリ>
- 発生した STEP / セクション:
- 内容:
- 再現性: <1 回のみ / 複数回 / 未確認>
- 原因の見立て: <プロンプトの指示不足 / 仕様の曖昧さ / モデル固有 / 不明>
- 対応: <プロンプト修正 / 仕様修正 / 保留 / 対応しない>
- 対応状況:
```

## 記録

### FP-001: Meaning Unit の一覧を書く場所が無い

- 初出: Test 01-1
- 発生した STEP / セクション: STEP 1 → output-format（13 セクション）
- 内容: STEP 1 で Meaning Unit を抽出して ID を振るが、Report に Meaning Unit の一覧を書くセクションが無い。監査者は Finding Ledger の列に ID と引用を併記して対応した。Finding に関わらない Meaning Unit は Report に残らない
- 再現性: 1 回のみ（仕様上は毎回起きる）
- 原因の見立て: 仕様の曖昧さ（STEP と出力形式の対応漏れ）
- 対応: 保留（Human Review 待ち）
- 対応状況: 未対応

### FP-002: 1 つの Finding に複数の情報状態がある

- 初出: Test 01-1
- 発生した STEP / セクション: Finding Ledger「情報状態」列
- 内容: 1 つの Finding の中で、検算結果（KNOWN）と読み替えの解釈（INFERRED）が混在することが多く、「KNOWN／INFERRED」のような複合表記が 7 件使われた。どの要素がどの情報状態かは、内容欄を読まないと分からない
- 再現性: 1 回のみ
- 原因の見立て: 仕様の曖昧さ
- 対応: 保留
- 対応状況: 未対応

### FP-003: 情報状態 CONFLICTING と Status の関係が定義されていない

- 初出: Test 01-1
- 発生した STEP / セクション: STEP 7、Finding Ledger
- 内容: 成果物の中で数値・表記が食い違う場合（CONFLICTING）、Mode B の Status を PARTIALLY TRACEABLE にするか UNKNOWN にするかの基準が無い。監査者は PARTIALLY TRACEABLE を選んだ
- 再現性: 1 回のみ
- 原因の見立て: 仕様の曖昧さ
- 対応: 保留
- 対応状況: 未対応

### FP-004: Stage が 1 つに決まらない Meaning Shift

- 初出: Test 01-1
- 発生した STEP / セクション: Key Meaning Shifts、Finding Ledger の Stage 列
- 内容: 定義されている Stage の値は 5 つだが、「Interpretation → Context」「Evidence → Interpretation」「Inference → Commitment」のような範囲の表記が使われた。Shift が Stage をまたいで進む場合の書き方が定義されていない
- 再現性: 1 回のみ
- 原因の見立て: 仕様の曖昧さ
- 対応: 保留
- 対応状況: 未対応

### FP-005: 成果物の中の検算が「外部知識」に当たるかが不明

- 初出: Test 01-1
- 発生した STEP / セクション: STEP 0（Evidence Boundary）、Mode B の原則
- 内容: 成果物の中の数値どうしの四則演算（合計・比率の検算）が、Evidence Boundary の「持ち込んだ外部知識」に当たるかが定義されていない。また「一般知識で真偽を判定しない」と「一般知識から照合すべき点を Source Verification Required に挙げる」の境界も曖昧（例: 公的な制度、他社の会社情報）。監査者は、検算は許されるとして扱い、その旨を明記した
- 再現性: 1 回のみ
- 原因の見立て: プロンプトの指示不足
- 対応: 保留
- 対応状況: 未対応（Workflow v1.0 には反映しない）
- Human Review 暫定判断（2026-10-06）: 成果物内部に存在する数値のみを使った算術的検算は、External Knowledge の導入とはみなさない。理由は、外部から Evidence を加えるのではなく、Artifact 内部の整合性を検査しているため。Workflow 改訂の候補として保持する。記録: [test-01-1-human-review.md](../examples/01-ai-presentation/review/test-01-1-human-review.md) の 3

### FP-006: Finding 数が多いときの Report の粒度

- 初出: Test 01-1
- 発生した STEP / セクション: 6. Overall Finding、12. Human Review Required
- 内容: Finding 26 件に対し、Overall Finding の「3〜6 文」に収めるため 1 文が非常に長くなった。Human Review Required は 17 件で、レビュー担当者の負担が大きい。Finding 数・レビュー項目数の目安や、優先度の付け方が定義されていない
- 再現性: 1 回のみ
- 原因の見立て: プロンプトの指示不足（スコアリングを導入せずに優先度を示す方法が無い）
- 対応: 保留
- 対応状況: 未対応
