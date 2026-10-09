# Terminology

- Name: Terminology
- Version: v1.1
- Status: RELEASED（v1.1、2026-10-09）
- Basis: Terminology v1.0（`docs/terminology.md`）に、Human-approved な v1.1 の変更だけを反映したもの。新しい定義は作っていない。各用語の正は、右の欄に示した Workflow v1.1・Output Contract v1.1 の箇所

Meaning Audit Workflow v1.1 で使う用語です。用語の追加は Human Review を経て行います。

## 構造

| 用語 | 定義 |
|---|---|
| Evidence / Source | 成果物の元になった資料・データ・証拠。Mode B では外部 Source は無く、成果物内で根拠として示されたものを扱う |
| Interpretation | Evidence / Source を読み、選び、まとめること |
| Inference / Warrant | 解釈から主張・結論へ進む推論と、根拠と結論をつなぐ理由 |
| Context / Pragmatics | 見出し・配置・語彙・図・想定読者など、表現の置かれ方によって生じる意味。Audience / Context と同じ STEP で扱う（概念上は分離） |
| Commitment | 成果物がある Meaning を判断・結論・推奨として採用すること |
| Integration | 各 STEP の結果を Report にまとめること |
| Human Review | 人間が Finding ごとの対応を決めること |

## 3 つの次元

Stage、情報状態、Status は別の次元です（[Workflow v1.1](../workflow/meaning-audit-workflow-v1.1.md) STEP 2）。

| 用語 | 定義 |
|---|---|
| Stage | Meaning Shift がどの段階で起きたか（Evidence / Source、Interpretation、Inference / Warrant、Context / Pragmatics、Commitment） |
| Primary Stage | Finding・Key Meaning Shift ごとに記録する Stage の値 1 つ（[Output Contract v1.1](../workflow/meaning-audit-output-contract-v1.1.md) §7・§10.1） |
| Stage Path | Finding が実質的に複数の Stage にまたがる場合に、Finding Detail に任意で書く Stage の流れ。複合の Stage 値ではない（Output Contract v1.1 §10.2） |
| 情報状態（Information State） | 判断に関係する要素について、Evidence Boundary の中で何が分かっているか（`KNOWN` / `INFERRED` / `UNKNOWN` / `CONFLICTING`） |
| Information State by Element | 情報状態を、Finding 全体にまとめず、判断に関係する要素ごとに付けること。1 つの要素に 1 つの値。判断に必要な範囲でだけ要素を部分に分ける（Workflow v1.1 STEP 2） |
| Status | Mode ごとの監査の判断の結果（Mode A：`SUPPORTED` / `PARTIALLY SUPPORTED` / `UNSUPPORTED` / `UNKNOWN`、Mode B：`TRACEABLE` / `PARTIALLY TRACEABLE` / `UNTRACEABLE` / `UNKNOWN`） |

要素の名前には Stage と同じ語を使いますが、ある要素に情報状態を付けても、その要素で Meaning Shift が起きたことは意味しません。

## 監査の単位と記録

| 用語 | 定義 |
|---|---|
| Audit Object | 監査対象の成果物 |
| Audit Object Metadata | Audit Object の任意の記録（Generation Tool、Post-generation Human Editing、Source Set Status）。Audit Mode を決めない（Output Contract v1.1 §3） |
| Source Set Status | Source Set の特定の状態。`COMPLETE`（宣言された／境界を定めた Source Set が、関係する文脈について完全に特定されている。世界中の関係しうる Source がすべて見つかったことは意味しない）／ `PARTIALLY KNOWN`（一部は特定されているが、完全な構成は確立されていない）／ `UNKNOWN`（Source Set Status そのものを確立できない）／ `NOT APPLICABLE`（当てはまらない） |
| Audit Purpose | 監査の目的。指定が無い場合の既定値は「Meaning Shift の所在を明らかにする」 |
| Evidence Boundary | 監査で参照した範囲と、参照していない範囲の境界 |
| Meaning Unit | 監査の単位となる、意味を担う主張・表現（`MU-01`〜）。ID は Report の中だけで有効で、他の Run の MU ID と対応しない |
| Primary Claim Type | Meaning Unit の主たる主張の種類。任意。`事実` / `解釈` / `推論` / `推奨` / `視覚的主張` / `引用` のうち最大 1 つ（日本語の値のまま）。Stage とは別の次元（Output Contract v1.1 §8） |
| Meaning Shift | 根拠から提示された Meaning までの間で、意味が加わる・変形される・強められる・弱められる・採用されること |
| Key Meaning Shift | 監査目的に照らして重要な Meaning Shift（`KS-1`〜） |
| Meaning Trace | 1 つの Key Meaning Shift を、Stage ごとに追跡した表。情報状態は書かない |
| Finding | 監査で記録する個別の指摘（`F-01`〜） |
| Finding Ledger | すべての Finding の記録。Finding Summary と Finding Detail の 2 層（Output Contract v1.1 §10） |
| Finding Summary | Finding ごとの分類を 1 行にまとめた表（Finding ID、MU、Location、Primary Stage、Finding Type、Status、Human Review の参照） |
| Finding Detail | Finding ごとのブロック（Content、Information State by Element、Evidence Note、任意の Annotation・Stage Path） |
| Evidence Note | その Finding を支える・限定する・食い違う Evidence と、その箇所 |
| Annotation | Canonical の分類欄に入れるべきでない nuance を書く任意の自由記述の欄。分類ではない |
| Finding Type | Finding の種類を表す運用ラベル（[../workflow/finding-types-v1.1.md](../workflow/finding-types-v1.1.md)） |
| Critical Unknown | 判定結果を左右する Unknown |
| Source Verification Required | 元資料との照合が必要な主張の一覧 |
| Human Review Required | 人間の判断が必要な Finding と、確認すべき問いの一覧 |

## 監査モードと Status

| 用語 | 定義 |
|---|---|
| Mode A: Source-Grounded Audit | 元資料と照合する監査 |
| Mode B: Artifact-Only Audit | 成果物だけで行う監査。元資料への忠実性は判定しない |
| SUPPORTED / PARTIALLY SUPPORTED / UNSUPPORTED / UNKNOWN | Mode A の Status |
| TRACEABLE / PARTIALLY TRACEABLE / UNTRACEABLE / UNKNOWN | Mode B の Status |
| UNSUPPORTED | 判断に十分な Evidence Boundary の中で、提示された Meaning が、提供された Source の Evidence に支えられていない。それだけで「虚偽」を意味しない。`CONFLICTING` があっても自動的に `UNSUPPORTED` にはならない |

定義の詳細は [../workflow/meaning-audit-workflow-v1.1.md](../workflow/meaning-audit-workflow-v1.1.md) の STEP 7。

## 情報状態

| 用語 | 定義 |
|---|---|
| KNOWN | 利用可能な資料で直接確認できる |
| INFERRED | 監査者の推論による |
| UNKNOWN | 利用可能な資料では分からない |
| CONFLICTING | Evidence Boundary の中で、同じ判断に関係する 2 つ以上の要素が意味上両立せず、その判断にとって互いに整合するものとして扱えない（例：資料同士、成果物と資料、成果物の中の要素同士、見出しと本文、数値の記述と注記）。違いがあるだけでは該当しない。Evidence の状態を表し、Status を自動的に決めるものではない |

`UNKNOWN` は、Evidence に基づいて選ぶ値であり、判断の難しさに基づいて選ぶ値ではありません。この原則は、情報状態の `UNKNOWN` と、Mode A・Mode B の Status の `UNKNOWN` に共通です（Workflow v1.1 Unknown Policy）。`UNKNOWN` の意味は欄によって決まります：情報状態、Status、Source Set Status、Location などの欄の値（Output Contract v1.1 §4）。

## Human Decision

| 用語 | 定義 |
|---|---|
| accept | Finding を妥当と認める |
| revise | Finding の内容・Status・種類を修正する |
| investigate | 追加の確認を行う |
| hold | 現時点では判断しない |
| reject | Finding を妥当でないと判断する |
| no action | Finding は妥当だが対応は不要と判断する |
