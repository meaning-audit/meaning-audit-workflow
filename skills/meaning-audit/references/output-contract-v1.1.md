<!-- Packaged from Meaning Audit v1.1 canonical assembly (workflow/meaning-audit-output-contract-v1.1.md). Packaging revision: repository-specific paths and maintainer instructions were replaced so that this skill is self-contained. Method, Status, Finding Types, values, and Workflow steps are unchanged. -->

# Meaning Audit Report / Output Contract v1.1

- Name: Meaning Audit Report / Output Contract
- Version: v1.1
- Status: RELEASED（v1.1、2026-10-09）
- Basis: Output Format v1.0（`workflow/output-format.md`）に、Human-approved Output Contract v1.1 Concept を適用したもの
- 監査の手順: [workflow-v1.1.md](workflow-v1.1.md)（Workflow v1.1）

v1.1 の標準成果物は Meaning Audit Report です。ヘッダーと以下の 14 セクションを、この順序で必ず含めます。該当する内容が無いセクションも省略せず、「該当なし」と書きます。任意の欄は、値が無ければ省いてよい。任意の欄を省くことと、必須のセクションを省くことは別です。

この文書は Report の構造と欄を定めます。Formal schema ではありません。

---

## 1. 構造

| v1.1 | 内容 |
|---|---|
| ヘッダー | Workflow version、Output Contract version、Prompt、Auditor、Date、Review status |
| 1. Audit Object | 名称、形式、作成者 / 生成元、作成日、監査範囲 ＋ Audit Object Metadata（任意） |
| 2. Audit Mode | Mode、判定理由、Mode B の定型文 |
| 3. Document Class | Class、判定理由、重点観点 |
| 4. Audit Purpose | 目的（既定値を使った旨） |
| 5. Evidence Boundary | 参照した Source、参照できなかった Source、監査対象の範囲、監査者が持ち込んだ外部知識 |
| 6. Overall Finding | 要約 |
| 7. Key Meaning Shifts | #、Meaning Unit、Shift の内容、Primary Stage、Finding |
| 8. Meaning Units | MU ID、内容、Location、Primary Claim Type |
| 9. Meaning Trace | Key Meaning Shift ごとの Stage の追跡 |
| 10. Finding Ledger | 10.1 Finding Summary、10.2 Finding Detail |
| 11. Critical Unknowns | 判定結果を左右する Unknown |
| 12. Source Verification Required | 元資料と照合すべき Source・事実 |
| 13. Human Review Required | レビューで確認すべき問い |
| 14. Limitations | 監査の限界 |

読む順序：Overall Finding → Key Meaning Shifts → Meaning Units → Meaning Trace → Finding Ledger。§7 の Meaning Unit の欄は、§8 の MU ID を参照します。

---

## 2. テンプレート

```markdown
# Meaning Audit Report

- Workflow version: Meaning Audit Workflow v1.1
- Output Contract version: v1.1
- Prompt: <使用した Prompt の識別子>
- Auditor: <AI モデル名 / 人間の監査者名>
- Date: <YYYY-MM-DD>
- Review status: Human Review 未実施

## 1. Audit Object

| 項目 | 内容 |
|---|---|
| 名称 | |
| 形式 | |
| 作成者 / 生成元 | |
| 作成日 | |
| 監査範囲 | |

### Audit Object Metadata（任意）

- Generation Tool: <既知の値 / UNKNOWN / NOT APPLICABLE>
- Post-generation Human Editing: <既知の値 / UNKNOWN / NOT APPLICABLE>
- Source Set Status: <COMPLETE / PARTIALLY KNOWN / UNKNOWN / NOT APPLICABLE>

## 2. Audit Mode

- Mode: <Mode A: Source-Grounded Audit / Mode B: Artifact-Only Audit>
- 判定理由:
- （Mode B の場合）Source verification は実施できない。外部 Evidence がないため、本 Report は成果物内部の Traceability のみを判定し、誤りの断定は行わない。

## 3. Document Class

- Class: <A / B / C>
- 判定理由:
- 重点観点:

## 4. Audit Purpose

- 目的:
- （指定がなかった場合）既定値「Meaning Shift の所在を明らかにする」を使用した。

## 5. Evidence Boundary

| 区分 | 内容 |
|---|---|
| 参照した Source | |
| 参照できなかった Source | |
| 監査対象の範囲 | |
| 監査者が持ち込んだ外部知識 | なし / あり（該当 Finding:） |

## 6. Overall Finding

<3〜6 文。どこで、どのような Meaning Shift が起きているかの要約。点数・等級・ランキングは付けない。>

## 7. Key Meaning Shifts

| # | Meaning Unit | Shift の内容 | Primary Stage | Finding |
|---|---|---|---|---|
| KS-1 | MU-xx | | | F-xx |

## 8. Meaning Units

<Meaning Unit ごとに：MU ID、内容。任意で Location、Primary Claim Type>

## 9. Meaning Trace

### KS-1: <短い名前>

| Stage | Trace |
|---|---|
| Evidence / Source | |
| Interpretation | |
| Inference / Warrant | |
| Context / Pragmatics | |
| Commitment / Presented Meaning | |
| Finding | |
| Status | |

（Key Meaning Shift ごとに繰り返す）

## 10. Finding Ledger

### 10.1 Finding Summary

| Finding | MU | Location | Primary Stage | Finding Type | Status | Human Review |
|---|---|---|---|---|---|---|
| F-01 | MU-xx | | | | | |

### 10.2 Finding Detail

<Finding ごとに 1 つのブロック：Finding ID、Content、Information State by Element、Evidence Note。任意で Annotation、Stage Path。該当する場合は Review / Verification Note>

## 11. Critical Unknowns

| # | Unknown | 影響する Finding | なぜ判定に重要か |
|---|---|---|---|
| U-1 | | | |

## 12. Source Verification Required

| # | 確認すべき Source / 事実 | 対象 Meaning Unit | 対象 Finding | 確認方法の候補 |
|---|---|---|---|---|
| SV-1 | | | | |

## 13. Human Review Required

| # | 対象 Finding | レビューで確認すべき問い | Human Decision |
|---|---|---|---|
| HR-1 | F-xx | | （人間が記入: accept / revise / investigate / hold / reject / no action） |

## 14. Limitations

- 
```

---

## 3. 各セクションの記入規則

### ヘッダー

- すべて必須。Output Contract version は `v1.1`
- Prompt は、使用した Prompt の識別子（自由記述）。Prompt を直接使う場合と Skill から実行する場合の値は、Prompt と Skill / Runtime の仕様に従う
- Auditor・Date が分からなければ `UNKNOWN`

### 1. Audit Object

分からない項目は推測で埋めず `UNKNOWN` と書きます。

Audit Object Metadata は任意の小節です（記録しない場合は省いてよい）。

| 欄 | 値 |
|---|---|
| Generation Tool | 既知の値 / `UNKNOWN` / `NOT APPLICABLE` |
| Post-generation Human Editing | 既知の値 / `UNKNOWN` / `NOT APPLICABLE` |
| Source Set Status | `COMPLETE` / `PARTIALLY KNOWN` / `UNKNOWN` / `NOT APPLICABLE` |

| Source Set Status | 意味 |
|---|---|
| COMPLETE | 宣言された／境界を定めた Source Set が、関係する監査または生成の文脈について完全に特定されている。世界中の関係しうる Source がすべて発見・提供されたことは意味しない |
| PARTIALLY KNOWN | Source Set の一部の構成要素は特定されているが、関係する Source Set の完全な構成は確立されていない |
| UNKNOWN | Source Set Status そのものを確立できない |
| NOT APPLICABLE | その Audit Object／文脈に Source Set Status が当てはまらない |

上の 4 つ以外の Source Set Status の値は使いません。Metadata があることは Audit Mode を決めません。Renderer、モデルの版、実行環境、中間表現などの拡張来歴は求めません。

### 2. Audit Mode

Mode B の場合、「Source verification は実施できない」旨を必ず書きます。Source が一部だけ提供されている場合は Mode A とし、Source の無い範囲を Evidence Boundary と Source Verification Required に書きます。

### 3. Document Class

Class の欄には、Canonical の Class の値（A / B / C）を 1 つだけ書きます。複数に該当する場合は主たる Class を選びます。副次 Class の欄、Class の配列、複合値、Class の中の括弧書きは使いません。他の Class の性質が監査に関係する場合は、判定理由などの自由記述に書きます。

### 4. Audit Purpose

指定が無い場合は既定値を使い、そのことを明記します。

### 5. Evidence Boundary

監査者（AI）が自身の一般知識を判定に使った場合は、「あり」とし、該当 Finding を列挙します。外部知識に依存した情報状態の付け方は §10.2 の規則に従います（Finding 全体ではなく、関係する要素を `INFERRED` とする）。

### 6. Overall Finding

- 点数・等級・ランキング・「良い／悪い」の総合評価は書きません
- Mode B では「誤り」「虚偽」「不正確」と断定しません

### 7. Key Meaning Shifts

すべての Finding ではなく、監査目的に照らして重要なものを選びます。目安は 3〜7 件です。

| 欄 | 区分 | 種類 |
|---|---|---|
| # | 必須 | ID（`KS-1` から） |
| Meaning Unit | 必須 | MU ID |
| Shift の内容 | 必須 | 自由記述 |
| Primary Stage | 必須 | Canonical（1 つ） |
| Finding | 必須 | Finding ID |

Primary Stage には、Finding Summary と同じ Stage の語彙から 1 つだけを書きます。複合の Stage 値（矢印・範囲・複数の値）を書きません。Shift が複数の Stage にまたがる場合は、関連する Finding の Detail の Stage Path に書きます。Key Meaning Shifts には Stage Path を求めません。

### 8. Meaning Units

STEP 1 で抽出した Meaning Unit を一覧にします。すべての文を Meaning Unit にする必要はありません。抽出しなかった範囲は Limitations に書きます。

| 欄 | 区分 | 種類 | 規則 |
|---|---|---|---|
| MU ID | 必須 | ID | `MU-01` から。Report の中で一意。Report の中でのみ意味を持つ。ID に意味（スライド番号、種類など）を埋め込まない。枝番を使わない。1 つの ID を別の内容に使わない。他の Run の MU ID と対応しない |
| 内容 | 必須 | 自由記述 | 原文の引用、要約、または図の記述 |
| Location | 任意 | 自由記述 | 成果物の中の位置 |
| Primary Claim Type | 任意 | Canonical（最大 1 つ） | 下の規則 |

Primary Claim Type：

- 値は Workflow STEP 1 の 6 つ：`事実` / `解釈` / `推論` / `推奨` / `視覚的主張` / `引用`
- この日本語の値をそのまま使います。Report の出力言語が日本語以外でも訳しません。英語の対応語、併記、コード、新しい種類を作りません
- 主たる値を最大 1 つ。複合値、複数の値、副次の種類を書きません。1 つに決められない場合は分類を強制せず、この欄を省きます。必要な補足は内容の欄に書きます
- Primary Claim Type は Meaning Unit の性質で、Finding の Stage とは別の次元です。「解釈」「推論」は Stage の Interpretation、Inference / Warrant を意味しません。一方から他方を推定しません
- Run 間の同一性・比較可能性を意味しません

### 9. Meaning Trace

Meaning Trace は標準成果物です。Key Meaning Shift ごとに 1 表を作ります。Meaning がどう動き・変わったかを書きます。

| Stage | 記入内容 |
|---|---|
| Evidence / Source | Mode A: Source の該当箇所と、Source が言っていること。Mode B: 成果物内で根拠として示されているもの（外部 Source は無いことを明記） |
| Interpretation | 根拠がどう読まれ、何が選ばれ・落とされたか |
| Inference / Warrant | どんな推論が使われたか。Warrant は明示されているか。監査者が Inference / Warrant を補った・再構成した場合は、そのことを記述として明記する（その推論が Finding の判断に関係する場合、その要素の情報状態は Finding Detail に `INFERRED` として記録する。Meaning Trace には情報状態を書かない） |
| Context / Pragmatics | 見出し・配置・図・語彙・想定読者によって、意味がどう変わるか |
| Commitment / Presented Meaning | 最終的に提示された Meaning と、その強さ（断定 / 推奨 / 可能性 / 留保付き） |
| Finding | 対応する Finding ID と要約 |
| Status | Mode A: SUPPORTED / PARTIALLY SUPPORTED / UNSUPPORTED / UNKNOWN。Mode B: TRACEABLE / PARTIALLY TRACEABLE / UNTRACEABLE / UNKNOWN |

- 情報状態の行・列を加えません。情報状態は §10.2 にだけ書きます
- 該当する変化がない Stage は「変化なし」と書き、空欄にしません
- Stage の内容を確立できない場合は、単独の `UNKNOWN` を汎用の placeholder として使いません。「Not established within the Evidence Boundary.」（Evidence Boundary の中で確立できない）のような説明の自由記述を書きます。これは新しい Canonical 値ではなく、情報状態としても読みません
- Status の行には、Finding の Status と同じ Canonical の Status を 1 つ書きます。Status の `UNKNOWN` はここで正規の値として使えます
- Meaning Trace を Finding の完全な一覧として使いません

### 10. Finding Ledger

Finding Ledger は、Finding Summary と Finding Detail の 2 層です。

#### 10.1 Finding Summary

1 Finding 1 行のコンパクトな表です。分類欄には Canonical 値だけを書きます。

| 欄 | 区分 | 種類 |
|---|---|---|
| Finding | 必須 | ID（`F-01` から連番。Report の中で一意。枝番を使わない。他の Run の Finding ID と対応しない） |
| MU | 必須（1 つ以上） | §8 に存在する MU ID のリスト。1 対 1 を強制しない。主・副の区別を付けない |
| Location | 欄は必須。具体的な位置の値は条件付き | 実際の位置（ページ、スライド、セクション、段落、セル、領域など。自由記述）／ `UNKNOWN`（関係する位置が存在する、または特定できるはずだが、Evidence Boundary の中で確立できない）／ `NOT APPLICABLE`（その Finding にとって位置に意味が無い） |
| Primary Stage | 必須 | Canonical（1 つ）：Evidence / Source、Interpretation、Inference / Warrant、Context / Pragmatics、Commitment |
| Finding Type | 必須 | Canonical（主たる 1 つ。[finding-types.md](finding-types.md)） |
| Status | 必須 | Canonical（1 つ。Mode に対応したもの） |
| Human Review | 条件付き | §13 に挙げた場合の HR ID。それ以外は「—」 |

Location の `UNKNOWN` は位置の値が確立できないことを表し、情報状態や Status の `UNKNOWN` ではありません。

#### 10.2 Finding Detail

Finding ごとに 1 つのブロックを作ります。1 つの大きな表にしません。ブロックの見た目の書式は定めません。

| 欄 | 区分 | 種類 |
|---|---|---|
| Finding ID | 必須 | ID |
| Content | 必須 | 自由記述 |
| Information State by Element | 必須（判断に関係する要素を少なくとも 1 つ） | 親の要素（Canonical）＋ 情報状態（Canonical） |
| 部分（sub-element）の分解 | 条件付き（判断に必要な最小限の分解がある場合） | 部分のラベル（自由記述）＋ 情報状態（Canonical） |
| Evidence Note | 必須 | 自由記述 |
| Annotation | 任意 | 自由記述 |
| Stage Path | 任意（Finding が実質的に複数の Stage にまたがる場合） | 自由記述 |
| Review / Verification Note | 条件付き（該当する場合） | 自由記述（HR・SV の番号など） |

Content：その Finding が何か、なぜ Meaning Audit の Finding になるのかを、読み手が判断を理解できる程度に書きます。通常は 1〜2 文で簡潔に。両方の説明に必要なら長くてよい（1〜2 文は目安であり、上限・下限ではありません）。修正案は書きません。

Evidence Note：その Finding を支える・限定する・食い違う Evidence と、その箇所（Mode A: Source の箇所、Mode B: 成果物内の箇所）を書きます。

Annotation：Canonical の分類欄に入れるべきでない nuance を書く任意の欄です。分類ではありません。分類値と矛盾させず、誤った分類値を補わず、隠れた 2 つめの Status・Finding Type・情報状態として使いません。Rationale の専用欄は設けません。

Stage Path：Primary Stage の補足として、Finding が実質的にまたがる Stage の流れを書きます（例：Evidence → Interpretation → Inference / Warrant）。複合の Canonical Stage 値ではありません。すべての Finding に求めません。

Information State by Element：

- 置き場所は Finding Detail だけです
- 各 Finding に、判断に関係する要素を少なくとも 1 つ、その情報状態とともに記録します。5 つすべては求めません。Report を埋めるためだけに無関係な要素を加えません
- 親の要素：Evidence / Source、Interpretation、Inference / Warrant、Context / Pragmatics、Commitment（Canonical）
- 部分：判断に必要な最小限の分解のときだけ。ラベルは自由記述で、Canonical な taxonomy はありません
- 値：`KNOWN` / `INFERRED` / `UNKNOWN` / `CONFLICTING` のうち 1 つ（要素または部分ごと）。複合ラベルを書きません
- Finding 単位の集約した情報状態を作りません
- 判断に関係する要素が、Evidence Boundary の中で確立された Evidence ではなく外部・一般の知識に依存する場合、その要素を `INFERRED` とします（例：`Interpretation: INFERRED`）。Finding 全体を `INFERRED` にしません。Evidence Boundary がその判断について外部知識の使用を認めていない場合、外部知識を Evidence の代わりにしません。`INFERRED` は認識上の出所を記録するもので、Evidence Boundary を広げません

例：

```text
Information State by Element:
- Evidence / Source
  - numerical value: KNOWN
  - population scope: UNKNOWN
- Inference / Warrant: INFERRED
```

### 11. Critical Unknowns

判定結果を左右する Unknown だけを書きます。Unknown を埋めるための推測は書きません。要素ごとの `UNKNOWN`、文章の解釈に関わる不確かさ、Limitations の項目を、それだけの理由でここに入れません。

### 12. Source Verification Required

- Mode B では、Traceability の判定とは別に、元資料と照合すべき主張をここに挙げます
- すべての引用・帰属を照合しません。成果物が Claim を特定の Source に明示的に帰属させ、その Source が Evidence Boundary の中にあり、その帰属が Finding にとって material な場合、照合が必要・関係することを示せます。照合できない・Evidence Boundary の外・Mode B の場合はここに挙げます
- 対象 Finding の欄は、material な明示的帰属に関わる場合に書きます（条件付き）

### 13. Human Review Required

- AI は「レビューで確認すべき問い」まで書きます
- Human Decision 列は空欄のまま出力します（AI が選ばない）
- 少なくとも次のような場合を挙げます（これ以外の正当な理由でもよい）：Status を 1 つに決められない、`CONFLICTING` が Support / Traceability の判断に影響している、明示的な帰属の materiality が不明確で結果に影響しうる、Finding の粒度が分類に影響している

### 14. Limitations

最低限、以下を確認して該当するものを書きます。

- Evidence Boundary の外側にある範囲
- AI が読めなかった要素（画像、図、表、PDF のレイアウトなど）
- Meaning Unit として抽出しなかった範囲
- 監査者の外部知識に依存した判定
- 監査が AI のみで行われ、Human Review 前であること

---

## 4. 欄の区分

### 必須・任意・条件付き

| 区分 | 欄 |
|---|---|
| 必須 | ヘッダーのすべて、§1〜§14 のすべてのセクション（無ければ「該当なし」）、Audit Object の 5 項目、Mode と判定理由、Class と判定理由と重点観点、Audit Purpose、Evidence Boundary の 4 区分、Overall Finding、KS の 5 欄、MU ID と内容、Meaning Trace（KS ごと）、Finding Summary の Finding・MU・Location 欄・Primary Stage・Finding Type・Status、Finding Detail の Finding ID・Content・Information State by Element（1 要素以上）・Evidence Note、Limitations |
| 任意 | Audit Object Metadata、Meaning Unit の Location、Primary Claim Type、Annotation、Stage Path |
| 条件付き | Mode B の定型文、既定の目的の記載、外部知識を使った Finding の列挙、Finding の具体的な位置の値、部分の分解、Human Review の参照、Review / Verification Note、Critical Unknowns・Source Verification Required・Human Review Required の項目、material な帰属の対象 Finding |

### Canonical 欄と自由記述欄

| 区分 | 欄 |
|---|---|
| Canonical（決まった値を 1 つ） | Mode、Class、Primary Stage（KS・Finding Summary）、Finding Type、Status、情報状態の値、親の要素のラベル、Primary Claim Type、Source Set Status、Metadata の一般的な状態（UNKNOWN、NOT APPLICABLE）、Human Decision（Human が記入） |
| ID | MU ID、Finding ID、KS／U／SV／HR の ID |
| 自由記述 | Meaning Unit の内容、Location の具体的な値、Content、Evidence Note、Annotation、Stage Path、部分のラベル、Meaning Trace の記述、Overall Finding、Critical Unknowns・Source Verification・Human Review の問い、Limitations、Review / Verification Note、Generation Tool などの既知の値 |

Canonical 欄に、括弧書き・注記・疑問符・複数の値を入れません。補足は自由記述の欄に書きます。

### Stage、情報状態、Status

| 次元 | 何を表すか | 置き場所 |
|---|---|---|
| Stage | Meaning Shift がどの段階で起きたか | KS と Finding Summary の Primary Stage、Finding Detail の Stage Path |
| 情報状態 | 判断に関係する要素について、Evidence Boundary の中で何が分かっているか | Finding Detail だけ |
| Status | Mode ごとの監査の判断の結果 | Finding Summary、Meaning Trace の Status 行 |

`UNKNOWN` が使われる場所は、情報状態の値、Status の値（Mode A・Mode B）、欄の一般的な状態（Audit Object の項目、Audit Object Metadata、Source Set Status、Finding の Location）に限ります。どれも欄によって意味が決まります。Meaning Trace の Stage の行では分類の値として使いません。

この一覧は、分類・状態として定義された `UNKNOWN` の使い方を示します。ヘッダーの Auditor・Date のような記述・メタデータの欄の `UNKNOWN` は、その欄の文脈で解釈するもので、Canonical な `UNKNOWN` の区分を増やすものではありません。

---

## 5. Mode A と Mode B

Report の構造は共通です。

| 項目 | Mode A | Mode B |
|---|---|---|
| Status の語彙 | SUPPORTED / PARTIALLY SUPPORTED / UNSUPPORTED / UNKNOWN | TRACEABLE / PARTIALLY TRACEABLE / UNTRACEABLE / UNKNOWN |
| §2 の定型文 | なし | 必須 |
| Evidence Note、Trace の Evidence / Source の行 | Source の箇所 | 成果物の中の根拠 |
| 明示的な帰属の照合 | Finding の Status と Evidence Note に書ける | Source Verification Required に挙げる |

1 つの Report の中で、2 つの Status の語彙を混ぜません。

---

## 6. v1.0 との関係（Backward compatibility）

| v1.0 | v1.1 |
|---|---|
| 13 セクション | 14 セクション。新しい §8 Meaning Units。v1.0 の §8〜§13 は v1.1 の §9〜§14 |
| ヘッダー | Output Contract version を追加 |
| Finding Ledger（9 列の 1 つの表） | Finding Summary ＋ Finding Detail。「内容」→ Content、「根拠」→ Evidence Note |
| Finding 単位の「情報状態」列 | deprecated。判断に関係する要素ごとの記録に置き換える |
| 複合の情報状態の値（例：KNOWN / INFERRED） | 自動で変換しない。v1.0 の Report の Finding 単位の情報状態を v1.1 の要素ごとの表現に移すときは、Human の解釈が必要になりうる。自動移行は約束しない |
| Meaning Trace の「確認できない Stage は `UNKNOWN` と書く」 | 意味の曖昧さを避けるため、説明の自由記述に変更 |
| Ledger の Location 列 | 維持（必須）。値に `UNKNOWN`／`NOT APPLICABLE` を明示 |
| 「内容」の 1〜2 文 | 拘束力の無い目安として維持 |
| §5 の「外部知識による判定は、情報状態を `INFERRED` とします」 | 関係する要素を `INFERRED` とする規則に置き換え |
| KS の Stage 欄（書き方の規定なし） | Primary Stage 1 つ |
| Class（副次 Class を併記） | Class の欄は Canonical の値 1 つだけ。他の Class の性質は自由記述（判定理由など）に |
