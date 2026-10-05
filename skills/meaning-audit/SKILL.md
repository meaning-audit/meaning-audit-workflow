---
name: meaning-audit
description: Run a Meaning Audit (Meaning Audit Workflow v1.0) on a document, AI-generated presentation, article, report, proposal, or analysis. Traces where meaning is added, transformed, inferred, and committed between Evidence/Source and the presented Meaning, and outputs a Meaning Audit Report with Meaning Trace and Finding Ledger for Human Review. Use when the user asks to "meaning audit" a file, to trace claims back to sources, to check how an AI-generated slide deck or summary changed the meaning of its source, or says 「Meaning Auditして」「意味監査して」「この資料の主張の根拠をたどって」「元資料からどこで意味が変わったか見て」. Not a fact-checker, scorer, or rewriter.
---

# Meaning Audit (Workflow v1.0)

Meaning Audit Workflow v1.0 に従って監査し、Meaning Audit Report を出力する。仕様の正は v1.0 であり、この Skill は新しい概念・分類・手順を追加しない。

追跡する構造:

```text
Evidence / Source → Interpretation → Inference / Warrant → Context / Pragmatics → Commitment → Integration → Human Review
```

Meaning Audit はファクトチェックではない。根拠から提示された Meaning までの間で、どこで意味が加わり、変形され、推論され、判断として採用されたかを追跡する。

## いつ使うか

- 文書・AI 生成プレゼン・記事・レポート・提案書・分析資料の主張が、何に基づき、どこで強められ・変えられたかを知りたいとき
- AI が生成した要約・スライドが、元資料の意味をどう変えたかを見たいとき
- 元資料が無く、成果物だけで根拠の示され方を点検したいとき

## 役割と禁止事項

あなたの役割は trace / expose / question / classify。最終判断はしない。

禁止:

- 書き直し・修正案の提示、点数・等級・ランキング・総合評価、採否・意思決定
- UNKNOWN を推測で埋めること（`UNKNOWN → plausible assumption → fact` の禁止）。INFERRED を後で KNOWN として扱うこと
- Mode B で成果物の主張を「誤り」「虚偽」「不正確」と断定すること
- Workflow に無い概念・分類・Finding Type を作ること（当てはまらなければ `OTHER` を使い、内容を具体的に書く）
- Evidence Boundary の外の情報を、自ら検索・取得して判定に使うこと。ユーザーが Source として指定したものだけを取得する

## 入力の受け取り

1. 監査対象（Audit Object）、元資料（Source。無くてもよい）、監査目的（Audit Purpose。無くてもよい）を確認する。不足していても監査は拒否しない
2. ファイルは Read で読む。PDF やスライドでテキスト層が無いページは、ページ画像として読む。図・グラフ・画像が読めない場合は推測で記述せず、Limitations に書く
3. Audit Purpose の指定が無ければ、既定値「Meaning Shift の所在を明らかにする」を使い、そのことを明記する
4. Report の言語はユーザーの指定に従う。指定が無ければ日本語。見出し・Status・Finding Type・情報状態のラベルは英語のまま

## 手順

詳細は [references/workflow.md](references/workflow.md)。以下は実行時の要点。

### STEP 0: Frame

**Audit Mode の判定**

| 状況 | Mode |
|---|---|
| Source が提供されている | Mode A: Source-Grounded Audit |
| Source が無い、または名前・URL だけで中身が無い | Mode B: Artifact-Only Audit |
| Source が一部だけ提供されている | Mode A。Source の無い Meaning Unit は UNKNOWN とし、Source Verification Required に記載 |

Source が無くても監査を拒否しない。Mode B として実行し、Report の「2. Audit Mode」に必ず次の文を書く:
「Source verification は実施できない。外部 Evidence がないため、本 Report は成果物内部の Traceability のみを判定し、誤りの断定は行わない。」

**Document Class の判定**

| Class | 対象例 | 重点 |
|---|---|---|
| A: Presentation / Visualization | AI 生成プレゼン、図解、要約スライド | Selection, Compression, Framing, Visualization, Visual Claim, Causal implication, Meaning amplification |
| B: Article / Report / Explanatory Document | 記事、論文、レポート、解説 | Evidence と Interpretation の境界, Narrative, Editorial framing, Quote handling, Context preservation, Title-body relationship |
| C: Proposal / Analysis / Decision Document | 提案、分析、企画、戦略資料 | Evidence, Inference, Warrant, Recommendation, Commitment |

複数に該当する場合は主たる Class を 1 つ選び、副次 Class を併記する。Class は手順を変えず、重点観点だけを変える。

**Evidence Boundary**

参照した Source、参照できなかった Source（言及はあるが提供されていない、読めない等）、監査対象の範囲、持ち込んだ外部知識の有無を書く。外部知識を判定に使った場合は該当 Finding を列挙し、情報状態を INFERRED とする。境界の外側は判定せず UNKNOWN とする。

### STEP 1: Meaning Unit Detection

意味を担う単位を抽出し、`MU-01` から連番を振る。対象: 明示的な主張（事実・数値・評価）、見出し・タイトル、図・グラフ・配置による主張（Visual Claim）、因果・比較・傾向の表現、推奨・結論、引用。各単位の Location と種類を把握する。抽出しなかった範囲は Limitations に書く。

### STEP 2〜6: Trace

| STEP | 見ること |
|---|---|
| 2 Evidence / Source Trace | Mode A: Source の該当箇所と「Source が言っていること」を並べる。Mode B: 成果物内で根拠として示されたもの。出典名だけのものは UNKNOWN |
| 3 Interpretation | 何が選ばれ・落ちたか、限定条件の消失、Evidence と解釈の境界、引用の扱い |
| 4 Inference / Warrant | 示されていない前提、相関・並置から因果へ、部分から全体へ。補った Warrant は INFERRED |
| 5 Context / Pragmatics | 見出し・順序・語彙・強調、図・色・配置、タイトルと本文、想定読者、文脈の保持、物語構成（v1.0 では Pragmatics と Audience / Context を同じ STEP で扱う） |
| 6 Commitment | 断定・推奨・結論として採用された Meaning と、その強さが根拠に見合っているか（Meaning amplification） |

各要素に情報状態を付ける。

### Unknown Policy

| 情報状態 | 意味 |
|---|---|
| KNOWN | 利用可能な資料で直接確認できる |
| INFERRED | 監査者の推論による。推論であることを明記する |
| UNKNOWN | 利用可能な資料では分からない |
| CONFLICTING | 資料同士、または資料と成果物が食い違う |

Unknown は欠陥ではなく情報状態である。埋めずに記録して先に進む。

### STEP 7: Integration

- Finding を `F-01` から連番で Finding Ledger にまとめ、Stage、Finding Type（[references/finding-types.md](references/finding-types.md)）、Status、情報状態、根拠の箇所を付ける
- 監査目的に照らして重要な Meaning Shift を Key Meaning Shifts として 3〜7 件選ぶ（`KS-1`〜）
- Key Meaning Shift ごとに Meaning Trace（Evidence / Source、Interpretation、Inference / Warrant、Context / Pragmatics、Commitment / Presented Meaning、Finding、Status）を作る。変化が無い Stage は「変化なし」、分からなければ UNKNOWN。空欄にしない

Status（1 つの Report では、Mode に対応するものだけを使う）:

| Mode A | Mode B |
|---|---|
| SUPPORTED: 範囲・強さを含めて Source に支えられている | TRACEABLE: 成果物内で根拠から主張までの道筋が示されている |
| PARTIALLY SUPPORTED: 一部は支えられているが、範囲・強さ・限定条件・因果などに差がある | PARTIALLY TRACEABLE: 根拠はあるが道筋に欠落がある |
| UNSUPPORTED: 境界内の Source を確認したが、支える記述が無い、または矛盾する（「虚偽」と同義ではない） | UNTRACEABLE: 成果物内に根拠が示されていない（「誤り」を意味しない） |
| UNKNOWN: 判定できない | UNKNOWN: 判定できない |

### STEP 8: Human Review

STEP 8 は人間が行う。Human Review Required に「レビューで確認すべき問い」を書き、Human Decision 欄は空欄のまま返す。人間が選ぶのは `accept` / `revise` / `investigate` / `hold` / `reject` / `no action`。

## 出力: Meaning Audit Report

[references/output-format.md](references/output-format.md) のテンプレートどおり、次の 13 セクションをこの順で出力する。内容が無いセクションも省略せず「該当なし」と書く。

1. Audit Object / 2. Audit Mode / 3. Document Class / 4. Audit Purpose / 5. Evidence Boundary / 6. Overall Finding / 7. Key Meaning Shifts / 8. Meaning Trace / 9. Finding Ledger / 10. Critical Unknowns / 11. Source Verification Required / 12. Human Review Required / 13. Limitations

Report の冒頭に、Workflow version（Meaning Audit Workflow v1.0）、Prompt（`skill: meaning-audit`）、Auditor（モデル名）、Date、Review status（Human Review 未実施）を書く。思考過程の全文は出力しない。ユーザーが保存を求めた場合だけ、指定の場所に Markdown で保存する。

## 出力前の自己確認

- 13 セクションが順序どおりに揃っている
- Audit Mode、Document Class、Evidence Boundary が明示されている。Mode B なら定型文がある
- Mode B で誤りを断定していない。Status は Mode に対応したものだけ
- Meaning Trace の各 Stage が空欄でない
- UNKNOWN を推測で埋めていない。INFERRED を KNOWN として扱っていない
- 点数・等級・修正案・Human Decision を書いていない

## References

| ファイル | 内容 |
|---|---|
| [references/workflow.md](references/workflow.md) | STEP 0〜8 の全文、Status と情報状態の定義、付録（Document Classes、Human Review、Audit Modes） |
| [references/output-format.md](references/output-format.md) | Report のテンプレートと各セクションの記入規則 |
| [references/finding-types.md](references/finding-types.md) | Finding Type 14 種と OTHER の扱い |
| [references/limitations.md](references/limitations.md) | 方法と AI 実行の既知の限界 |
