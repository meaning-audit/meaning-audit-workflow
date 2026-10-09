# Meaning Audit Workflow v1.1

- Name: Meaning Audit Workflow
- Version: v1.1
- Status: RELEASED（v1.1、2026-10-09）
- Basis: Meaning Audit Workflow v1.0 に、Human-approved Workflow v1.1 Definition Delta（D-1〜D-11）を適用したもの
- Report の形式: [meaning-audit-output-contract-v1.1.md](meaning-audit-output-contract-v1.1.md)（Output Contract v1.1）

この文書は、Meaning Audit を実行するための手順仕様です。理論の説明ではなく、監査者（AI または人間）が上から順に実行できることを目的にしています。

---

## 0. 前提

### 0.1 追跡する構造

```text
Evidence / Source
  → Interpretation
  → Inference / Warrant
  → Context / Pragmatics
  → Commitment
  → Integration
  → Human Review
```

Meaning Audit は、この流れのどこで意味が加わり、変形され、推論され、判断として採用されたかを追跡します。

### 0.2 役割分担

| | 行うこと | 行わないこと |
|---|---|---|
| AI | trace / expose / question / classify | 最終判断、書き直し、採点、意思決定 |
| Human | accept / revise / investigate / hold / reject / no action | — |

AI の監査結果は、Human Review を経るまで「未確定」です。

### 0.3 用語の最小定義

- Audit Object: 監査対象の成果物（スライド、記事、提案書など）
- Source: Audit Object の元になった資料・データ・Evidence
- Meaning Unit: 監査の単位となる、意味を持つ主張・表現（文、見出し、図、グラフ、推奨など）
- Meaning Shift: Source（Mode B では成果物内の根拠）から提示された Meaning への間で、意味が加わる・変形される・強められる・弱められる・採用されること
- Finding: 監査で記録する個別の指摘

詳細は [../docs/terminology-v1.1.md](../docs/terminology-v1.1.md)。

---

## STEP 0: Frame

監査の枠組みを、本文を読み込む前に確定します。

1. Audit Object を特定する（名称、形式、作成者・生成元、日付、範囲。分からない項目は `UNKNOWN`）
2. Audit Purpose を記録する（何のための監査か。指定がなければ「Meaning Shift の所在を明らかにする」を既定値とし、既定値を使ったことを明記する）
3. Audit Mode を判定する（下表）
4. Document Class を判定する（下表）
5. Evidence Boundary を明示する

### Audit Mode の判定

| 状況 | Mode |
|---|---|
| Source が提供されている | Mode A: Source-Grounded Audit |
| Source が提供されていない | Mode B: Artifact-Only Audit |
| Source が一部だけ提供されている | Mode A。ただし Source が無い Meaning Unit は「Evidence Boundary の中で確立できない」とし、Source Verification Required に記載する |

Mode B に切り替えるときは、Report 冒頭で「Source verification は実施できない」ことを明示します。Mode の詳細は [../docs/audit-modes-v1.1.md](../docs/audit-modes-v1.1.md)。

### Document Class の判定

| Class | 判定の目安 |
|---|---|
| A: Presentation / Visualization | スライド、図解、要約資料など、選択・圧縮・視覚化で意味を伝える |
| B: Article / Report / Explanatory Document | 記事、論文、レポート、解説など、文章の叙述で意味を伝える |
| C: Proposal / Analysis / Decision Document | 提案、分析、企画、戦略など、判断や推奨を導く |

複数に該当する場合は、主たる Class を 1 つ選びます。Class の欄には Canonical の Class の値を 1 つだけ書きます。他の Class の性質が監査に関係する場合は、Class の欄の外の自由記述（判定理由など）に書きます。Class によって監査手順は変わりません。変わるのは各 STEP で重点的に見る観点です（[../docs/document-classes-v1.1.md](../docs/document-classes-v1.1.md)）。

### Evidence Boundary

監査で参照した範囲と、参照していない範囲を書きます。

- 参照した Source（名称・範囲）
- 参照できなかった Source（言及はあるが提供されていない、読めない形式、など）
- 監査対象の範囲（全体か、一部か）
- 監査者が持ち込んだ外部知識の有無（使った場合は、どの Finding で使ったかを明記する）

Evidence Boundary の外側にあるものについては、判定せず「Evidence Boundary の中で確立できない」とします。

Source Set が一部だけの場合、判断は提供された Source の範囲に限ります。提供された Source の中に支えが見つからないことを、Evidence Boundary の外側に支える Source が存在しないことの証拠として扱ってはなりません。

Mode 判定の表の「Source が無い Meaning Unit」は、その Meaning Unit に対応する Source が提供されていないことを指します。提供された Source の中に支えが見つからないことは、それだけで `UNKNOWN` も `UNSUPPORTED` も決めません。Status の判断は STEP 7 のとおりです。

---

## STEP 1: Claim / Meaning Unit Detection

Audit Object から Meaning Unit を抽出し、ID を振ります（`MU-01`, `MU-02`, …）。

抽出対象:

- 明示的な主張（事実の記述、数値、評価）
- 見出し・タイトル・キャッチコピー
- 図・グラフ・表・配置が伝える主張（Visual Claim）
- 因果・比較・傾向を示す表現
- 推奨・結論・判断
- 引用

各 Meaning Unit について、監査の中で次を特定します:

- Location（ページ、スライド番号、段落など）
- 原文（または図の記述）
- 主張の種類（事実 / 解釈 / 推論 / 推奨 / 視覚的主張 / 引用）

Report への出力は Output Contract の規則に従います。MU ID と内容（原文または図の記述）は必須、Location と Primary Claim Type は任意です。すべての Meaning Unit に Location や主張の種類の出力を求めません。Primary Claim Type は、上の 6 つの値から主たるものを 1 つに決められる場合だけ 1 つ出力し、決められない場合は省きます。

すべての文を Meaning Unit にする必要はありません。監査目的に照らして、意味を担っている単位を優先します。抽出しなかった範囲がある場合は Limitations に書きます。

---

## STEP 2: Evidence / Source Trace

各 Meaning Unit について、その根拠をたどります。

Mode A:

- 対応する Source の箇所を特定する
- Source に書かれていること（Source が言っていること）と、Meaning Unit が言っていることを並べる
- 対応する Source が見つからない場合、Evidence Boundary の内側で見つからないのか、外側なのかを区別する

Mode B:

- 成果物の中で、その Meaning Unit の根拠として示されているもの（数値、引用、出典表記、前段の記述）を特定する
- 出典名が書かれていても、その中身は確認できないため、その要素の情報状態は `UNKNOWN` とする

情報状態（`KNOWN` / `INFERRED` / `UNKNOWN` / `CONFLICTING`）は、判断に関係する要素ごとに付けます（Information State by Element）。Finding 全体にまとめて 1 つ付けるものではありません。

要素とは、Meaning Trace の中の意味の構成部分のうち、その Finding の判断に関係するものです。典型的な要素の種類は Evidence / Source、Interpretation、Inference / Warrant、Context / Pragmatics、Commitment ですが、すべての Finding に必ず置く欄ではありません。情報状態は、関係する要素にだけ付けます。

- 1 つの要素には、情報状態を 1 つ付けます。複数の情報状態を 1 つのラベルに合成しません
- 1 つの要素の中で、判断にとって実質的に異なる部分が異なる情報状態を持つ場合は、判断に必要な範囲でだけ要素を分けます（例：Evidence のうち、数値は `KNOWN`、母集団の範囲は `UNKNOWN`）
- 判断に影響しない区別のために、要素を細かく分けすぎません（判断に必要な最小限の分解）

Stage、情報状態、Status は別の次元です。

- Stage：Meaning Shift がどの段階で起きたか
- 情報状態：判断に関係する要素について、Evidence Boundary の中で何が分かっているか（`KNOWN` / `INFERRED` / `UNKNOWN` / `CONFLICTING`）
- Status：Mode ごとの監査の判断の結果（Mode A：`SUPPORTED` / `PARTIALLY SUPPORTED` / `UNSUPPORTED` / `UNKNOWN`、Mode B：`TRACEABLE` / `PARTIALLY TRACEABLE` / `UNTRACEABLE` / `UNKNOWN`）

要素の名前には Stage と同じ語を使いますが、ある要素に情報状態を付けても、その要素で Meaning Shift が起きたことは意味しません。情報状態の `UNKNOWN` と Status の `UNKNOWN` は、同じ語ですが別の次元の値です。

---

## STEP 3: Interpretation Audit

Source（または成果物内の根拠）が、どのように解釈されて Meaning Unit になったかを見ます。

確認すること:

- 何が選ばれ、何が落とされたか（Selection）
- 限定条件・範囲・例外が要約で消えていないか（Compression）
- Evidence の記述と、作成者の解釈が区別されているか
- 引用が元の文脈・発言者・意図を保っているか（Quote handling）

---

## STEP 4: Inference / Warrant Audit

Interpretation から結論・主張へ進むとき、どんな推論が使われ、それを支える Warrant（根拠と結論をつなぐ理由）が示されているかを見ます。

確認すること:

- 根拠と結論の間に、明示されていない前提がないか
- 相関・並置・時系列が、因果として提示されていないか（Causal implication）
- 一部の事例が、全体の傾向として提示されていないか
- Warrant が示されていない場合、監査者が補った Warrant は `INFERRED` と明記する（補った Warrant を事実として扱わない）

---

## STEP 5: Context / Pragmatics Audit

Pragmatics と Audience / Context を同じ STEP で扱います。

確認すること:

- 見出し・順序・語彙・強調によって、意味づけが変わっていないか（Framing）
- 図・グラフ・色・大きさ・配置が、本文以上の主張をしていないか（Visualization / Visual Claim）
- タイトルと本文の主張の強さ・範囲が一致しているか（Title-body relationship）
- 想定読者が、その表現からどう受け取るか。また、元の文脈が保たれているか（Context preservation）
- 物語的な構成が、根拠にない意味を加えていないか（Narrative / Editorial framing）

---

## STEP 6: Commitment Audit

成果物が、どの Meaning を判断・結論・推奨として採用（Commit）しているかを見ます。

確認すること:

- 断定・推奨・結論として提示されている Meaning Unit はどれか
- その Commitment の強さ（断定 / 推奨 / 可能性の提示 / 留保付き）が、STEP 2〜5 で確認した根拠の状態に見合っているか
- 確度・範囲・強度が、Source または成果物内の根拠より強くなっていないか（Meaning amplification）
- 推奨（Recommendation）が、どの Evidence と Inference に依存しているか

---

## STEP 7: Integration

STEP 1〜6 の結果を統合し、Meaning Audit Report を作成します（[meaning-audit-output-contract-v1.1.md](meaning-audit-output-contract-v1.1.md)）。

1. Finding を Finding Ledger にまとめる（ID: `F-01`, `F-02`, …）
2. 各 Finding に Finding Type（主たる 1 つ。[finding-types-v1.1.md](finding-types-v1.1.md)）、Stage、Status（1 つ）を付け、情報状態は関係する要素ごとに記録する（STEP 2）
   - Status を 1 つに決められない場合は、複数の Status を併記せず、Finding の範囲が適切かを見直し、判断に必要な情報の不足や食い違いを記録したうえで、Human Review Required に挙げる
3. 監査目的に照らして重要な Meaning Shift を Key Meaning Shifts として選ぶ
4. Key Meaning Shift ごとに Meaning Trace を作る
5. Critical Unknowns、Source Verification Required、Human Review Required を書き出す
6. Overall Finding を書く（点数・等級・ランキングは付けない）

### Status の定義

Mode A（Source-Grounded）:

| Status | 意味 |
|---|---|
| SUPPORTED | 提示された Meaning が、範囲・強さを含めて Source に支えられている |
| PARTIALLY SUPPORTED | 一部は Source に支えられているが、範囲・強さ・限定条件・因果などに差がある |
| UNSUPPORTED | 判断に十分な Evidence Boundary の中で、提示された Meaning が、提供された Source の Evidence に支えられていない。支える記述が無い場合と、Source が提示された Meaning と食い違う場合がある。評価する Meaning には、判断の一部である場合、成果物が明示した Source への帰属を含めてよい |
| UNKNOWN | Evidence Boundary の中で、Support の判断を確立できない（Unknown Policy を参照） |

`UNSUPPORTED` は「提供された Source では支えられていない」という意味であり、それだけで「虚偽」を意味しません。

食い違いのある要素には、情報状態 `CONFLICTING` を付けます（Unknown Policy の表）。`CONFLICTING` は Evidence の状態であり、Status を自動的に決めるものではありません（CONFLICTING does not mechanically imply UNSUPPORTED）。`CONFLICTING` がある場合も、Status は Evidence Boundary と文脈に照らして別に判断します。

Mode A の Status は、次の点に照らして判断します。これは判断の観点であり、機械的な対応表ではありません。

- 成果物が特定の Source に明示的に帰属させている Claim か、帰属の示されていない Claim か
- Source Set の範囲（分かっている場合）。Source Set が完全と分かっていても、提供された Source に記述が無いことだけで自動的に `UNSUPPORTED` とはしない。Source Set が一部だけの場合は STEP 0 の Evidence Boundary に従う
- Claim の一部の要素だけが Source に支えられている、または一部の要素が Source に無い場合
- Source が要約・概要版などで、範囲や詳しさが限られている場合
- 判断に関係する要素の間に食い違いがある場合（`CONFLICTING`。Status は上のとおり別に判断する）

判断が Status の選択を左右するほど不確かな場合は、Human Review Required に挙げます。

Mode B（Artifact-Only）:

| Status | 意味 |
|---|---|
| TRACEABLE | 成果物の中で、根拠から主張までの道筋が示されている |
| PARTIALLY TRACEABLE | 根拠は示されているが、主張までの道筋に欠落がある |
| UNTRACEABLE | 成果物の中に、その主張の根拠が示されていない |
| UNKNOWN | Evidence Boundary の中で、Traceability の判断を確立できない（例：読めない図、意味が曖昧。Unknown Policy を参照） |

`UNTRACEABLE` は「誤り」を意味しません。Mode B では、外部 Evidence なしに誤りと断定してはなりません。

### 情報状態と UNKNOWN（Unknown Policy）

| 情報状態 | 意味 |
|---|---|
| KNOWN | 利用可能な資料で直接確認できる |
| INFERRED | 監査者の推論による。推論であることを明記する |
| UNKNOWN | 利用可能な資料では分からない |
| CONFLICTING | Evidence Boundary の中で、同じ判断に関係する 2 つ以上の要素が意味上両立せず、その判断にとって互いに整合するものとして扱えない（例：資料同士、成果物と資料、成果物の中の要素同士、見出しと本文、数値の記述と注記）。違いがあるだけでは該当しない。Evidence の状態を表し、Status を自動的に決めるものではない |

Unknown は欠陥ではなく情報状態です。次の変換を禁止します。

```text
UNKNOWN → plausible assumption → fact
```

- UNKNOWN をもっともらしい推測で埋めない
- INFERRED を後の STEP で KNOWN として扱わない
- 判定に必要な情報が無いときは、無いことを記録して先に進む

`UNKNOWN` は、Evidence に基づいて選ぶ値であり、判断の難しさに基づいて選ぶ値ではありません。この原則は、情報状態の `UNKNOWN` と、Mode A・Mode B の Status の `UNKNOWN` に共通です。

- `UNKNOWN` は、その判断に必要な情報を Evidence Boundary の中で確立できない場合に使う
- 判断が難しい場合は、不足している情報と、該当する場合は食い違っている情報を特定し、Evidence Boundary を保ったまま判断する。必要なら Human Review Required に挙げる
- 判断が難しいというだけで、自動的に `UNKNOWN` を選ばない
- 十分な Evidence が無いのに、`UNKNOWN` 以外の Status を選ばない。`UNKNOWN` は正規の値である

---

## STEP 8: Human Review

AI の監査は STEP 7 で終わります。STEP 8 は人間が行います。

- Human Review Required に挙がった項目を中心に、Finding ごとに対応を決める
- 対応は `accept` / `revise` / `investigate` / `hold` / `reject` / `no action` のいずれか
- AI は対応を選びません。AI はレビューで確認すべき問いを示すところまでを担います

手順と記録形式は [../docs/human-review-v1.1.md](../docs/human-review-v1.1.md)。

---

## v1.1 で行わないこと

- スコアリング、等級付け、ランキング
- 自動 Rewrite（修正文の提示を含む）
- 自動意思決定
- 新しい Finding Type や新概念の自動採用（必要に見えたら [../tests/post-freeze-candidates.md](../tests/post-freeze-candidates.md) へ記録）
