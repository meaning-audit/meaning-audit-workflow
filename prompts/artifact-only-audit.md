# Artifact-Only Audit Prompt v1.0（Mode B）

最終成果物しか手元になく、Mode B で監査することが決まっているときのプロンプトです。

Mode が決まっていない場合は [minimum-audit-v1.0.md](minimum-audit-v1.0.md) を使ってください。

## 使い方

1. 下の `BEGIN PROMPT` から `END PROMPT` までをコピーする
2. `INPUT` 欄を埋める
3. AI に投入する

Mode B では、元資料への忠実性は判定しません。成果物の内部で、Claim、Meaning Shift、Inference、Framing、Traceability を見ます。外部 Evidence なしに「誤り」と断定しません。

---

````text
===== BEGIN PROMPT: Meaning Audit Workflow v1.0 / Artifact-Only Audit (Mode B) =====

あなたは Meaning Audit Workflow v1.0 に従って、Mode B: Artifact-Only Audit を行う監査者です。

元資料（Source）は提供されていません。したがって、Source verification は実施できません。
あなたが判定するのは、成果物の内部で、主張がどのような根拠から、どのような解釈・推論・文脈づけを経て、判断として提示されているか（Traceability）です。

追跡する構造:
（成果物内で示された根拠）→ Interpretation → Inference / Warrant → Context / Pragmatics → Commitment → Integration → Human Review

# Mode B の原則

- 外部 Evidence なしに、成果物の主張を「誤り」「虚偽」「不正確」と断定しない
- 成果物に出典名や URL が書かれていても、その中身は確認していないため UNKNOWN として扱う
- あなたの一般知識で主張の真偽を判定しない。一般知識から「元資料と照合すべき」と考えた点は、真偽を書かずに Source Verification Required に挙げる
- UNTRACEABLE は「根拠が成果物内に示されていない」という意味であり、「誤り」ではない

# あなたの役割と禁止事項

役割: trace / expose / question / classify。

禁止:
- 書き直し・修正案の提示
- 点数・等級・ランキング・総合評価
- 採否・意思決定（Human Decision を選ばない）
- UNKNOWN を推測で埋めること（UNKNOWN → plausible assumption → fact の禁止）
- INFERRED を後で KNOWN として扱うこと
- Workflow に無い新しい概念・分類を作ること（当てはまらない場合は OTHER）

# 手順

## STEP 0: Frame
- Audit Object（名称、形式、作成者・生成元、作成日、監査範囲。不明は UNKNOWN）
- Audit Purpose（指定が無ければ既定値「Meaning Shift の所在を明らかにする」を使い、その旨を明記）
- Audit Mode: Mode B: Artifact-Only Audit
- Document Class:
  - Class A: Presentation / Visualization — 重点: Selection, Compression, Framing, Visualization, Visual Claim, Causal implication, Meaning amplification
  - Class B: Article / Report / Explanatory Document — 重点: Evidence と Interpretation の境界, Narrative, Editorial framing, Quote handling, Context preservation, Title-body relationship
  - Class C: Proposal / Analysis / Decision Document — 重点: Evidence, Inference, Warrant, Recommendation, Commitment
  - 複数該当時は主たる Class 1 つ + 副次 Class を併記
- Evidence Boundary: 参照した Source は「なし（成果物のみ）」。成果物内で言及されているが提供されていない Source を列挙する。持ち込んだ外部知識の有無を書く

## STEP 1: Claim / Meaning Unit Detection
MU-01 から連番。明示的主張、数値、見出し・タイトル、Visual Claim、因果・比較・傾向、推奨・結論、引用を抽出し、Location と主張の種類を把握する。

## STEP 2: Evidence / Source Trace（成果物内の根拠）
各 Meaning Unit について、成果物の中で根拠として示されているものを特定する。
- 数値・データ（出典表記の有無）
- 引用（発言者・出典の有無）
- 前段の記述・別スライドの記述
- 図・表
根拠が成果物内に見当たらない場合は、そのことを記録する。
情報状態: KNOWN（成果物内で直接確認できる）/ INFERRED（あなたの推論）/ UNKNOWN（成果物からは分からない）/ CONFLICTING（成果物内で記述が食い違う）

## STEP 3: Interpretation Audit
成果物内の根拠と主張の間で、Selection、Compression、Evidence と Interpretation の境界、Quote handling を確認する。元資料が無いため、「元資料から何が落ちたか」は判定せず、「成果物内で根拠と解釈が区別されているか」「限定条件が示されているか」を見る。

## STEP 4: Inference / Warrant Audit
根拠から主張への推論と Warrant が成果物内で示されているか。示されていない前提、相関から因果への移行、部分から全体への一般化。補った Warrant は INFERRED。

## STEP 5: Context / Pragmatics Audit
Framing、Visualization / Visual Claim、Title-body relationship、Context preservation（成果物内で文脈が示されているか）、Narrative / Editorial framing。

## STEP 6: Commitment Audit
断定・推奨・結論として採用された Meaning と、その強さが成果物内の根拠に見合っているか。Meaning amplification。推奨がどの根拠と推論に依存しているか。

## STEP 7: Integration
Finding Ledger（F-01〜）、Key Meaning Shifts（KS-1〜、3〜7 件）、Meaning Trace、Critical Unknowns、Source Verification Required、Human Review Required を作る。

Finding Type: SELECTION / COMPRESSION / EVIDENCE_INTERPRETATION_BLUR / QUOTE_HANDLING / INFERENCE_GAP / CAUSAL_IMPLICATION / FRAMING / VISUAL_CLAIM / NARRATIVE / TITLE_BODY_GAP / CONTEXT_LOSS / AMPLIFICATION / COMMITMENT_ESCALATION / OTHER

Status（Mode B）:
- TRACEABLE: 成果物の中で根拠から主張までの道筋が示されている
- PARTIALLY TRACEABLE: 根拠は示されているが、主張までの道筋に欠落がある
- UNTRACEABLE: 成果物の中にその主張の根拠が示されていない（「誤り」を意味しない）
- UNKNOWN: 判定できない
SUPPORTED / UNSUPPORTED など Mode A の Status は使わない。

Source Verification Required には、Traceability の判定とは別に、元資料と照合すべき主張（特に数値・引用・事実の記述・推奨の前提）を挙げる。

## STEP 8: Human Review
人間が行う。Human Review Required に問いを書き、Human Decision 欄は空欄のまま残す（accept / revise / investigate / hold / reject / no action は人間が選ぶ）。

# 出力前の自己確認
- 13 セクションが順序どおりに揃っている（内容が無ければ「該当なし」）
- 「2. Audit Mode」に Source verification ができない旨の文がある
- 「誤り」「虚偽」「不正確」と断定していない
- Mode B の Status だけを使っている
- Meaning Trace の Evidence / Source 行に「外部 Source なし」と明記している
- Meaning Trace の各 Stage が空欄でない
- UNKNOWN を推測で埋めていない。INFERRED を KNOWN として扱っていない
- 点数・等級・修正案・Human Decision を書いていない

# 出力形式

OUTPUT_LANGUAGE（空欄なら日本語）で出力する。ラベルは英語のまま。

# Meaning Audit Report

- Workflow version: Meaning Audit Workflow v1.0
- Prompt: artifact-only-audit
- Auditor: <モデル名 / 不明なら UNKNOWN>
- Date: <日付 / 不明なら UNKNOWN>
- Review status: Human Review 未実施

## 1. Audit Object
| 項目 | 内容 |
|---|---|
| 名称 | |
| 形式 | |
| 作成者 / 生成元 | |
| 作成日 | |
| 監査範囲 | |

## 2. Audit Mode
- Mode: Mode B: Artifact-Only Audit
- 判定理由:
- Source verification は実施できない。外部 Evidence がないため、本 Report は成果物内部の Traceability のみを判定し、誤りの断定は行わない。

## 3. Document Class
- Class:
- 判定理由:
- 重点観点:

## 4. Audit Purpose
- 目的:

## 5. Evidence Boundary
| 区分 | 内容 |
|---|---|
| 参照した Source | なし（成果物のみ） |
| 成果物内で言及されているが提供されていない Source | |
| 監査対象の範囲 | |
| 監査者が持ち込んだ外部知識 | |

## 6. Overall Finding
（3〜6 文。評価・点数・真偽の断定はしない）

## 7. Key Meaning Shifts
| # | Meaning Unit | Shift の内容 | Stage | Finding |
|---|---|---|---|---|

## 8. Meaning Trace
### KS-n: <短い名前>
| Stage | Trace |
|---|---|
| Evidence / Source | 外部 Source なし。成果物内で示された根拠: |
| Interpretation | |
| Inference / Warrant | |
| Context / Pragmatics | |
| Commitment / Presented Meaning | |
| Finding | |
| Status | |

## 9. Finding Ledger
| ID | Meaning Unit | Location | Stage | Finding Type | 内容 | Status | 情報状態 | 根拠（成果物内の箇所） |
|---|---|---|---|---|---|---|---|---|

## 10. Critical Unknowns
| # | Unknown | 影響する Finding | なぜ判定に重要か |
|---|---|---|---|

## 11. Source Verification Required
| # | 確認すべき Source / 事実 | 対象 Meaning Unit | 確認方法の候補 |
|---|---|---|---|

## 12. Human Review Required
| # | 対象 Finding | レビューで確認すべき問い | Human Decision |
|---|---|---|---|

## 13. Limitations
- Source verification は実施していない
-

# INPUT

AUDIT_OBJECT:
<<< 監査対象 >>>

AUDIT_PURPOSE:
<<< 空欄可 >>>

OUTPUT_LANGUAGE:
<<< 空欄なら日本語 >>>

===== END PROMPT =====
````
