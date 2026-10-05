<!-- Packaged from Meaning Audit Workflow v1.0 (canonical source: https://github.com/meaning-audit/meaning-audit-workflow, workflow/meaning-audit-workflow-v1.0.md, docs/document-classes.md, workflow/human-review.md, docs/audit-modes.md, docs/terminology.md). Packaging revision: repository-specific paths and maintainer instructions were replaced so that this skill is self-contained. Method, Status, Finding Types, and Workflow steps are unchanged. -->

# Meaning Audit Workflow v1.0

Status: v1.0 初期構築版（Human Review 前）

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

詳細は付録 D（Terminology）。

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
| Source が一部だけ提供されている | Mode A。ただし Source が無い Meaning Unit は `UNKNOWN` とし、Source Verification Required に記載する |

Mode B に切り替えるときは、Report 冒頭で「Source verification は実施できない」ことを明示します。

### Document Class の判定

| Class | 判定の目安 |
|---|---|
| A: Presentation / Visualization | スライド、図解、要約資料など、選択・圧縮・視覚化で意味を伝える |
| B: Article / Report / Explanatory Document | 記事、論文、レポート、解説など、文章の叙述で意味を伝える |
| C: Proposal / Analysis / Decision Document | 提案、分析、企画、戦略など、判断や推奨を導く |

複数に該当する場合は、主たる Class を 1 つ選び、副次的な Class を併記します（例: `Class C（主）/ Class A（副：提案スライド形式）`）。Class によって監査手順は変わりません。変わるのは各 STEP で重点的に見る観点です（付録 A（Document Classes））。

### Evidence Boundary

監査で参照した範囲と、参照していない範囲を書きます。

- 参照した Source（名称・範囲）
- 参照できなかった Source（言及はあるが提供されていない、読めない形式、など）
- 監査対象の範囲（全体か、一部か）
- 監査者が持ち込んだ外部知識の有無（使った場合は、どの Finding で使ったかを明記する）

Evidence Boundary の外側にあるものについては、判定せず `UNKNOWN` とします。

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

各 Meaning Unit について記録すること:

- Location（ページ、スライド番号、段落など）
- 原文（または図の記述）
- 主張の種類（事実 / 解釈 / 推論 / 推奨 / 視覚的主張 / 引用）

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
- 出典名が書かれていても、その中身は確認できないため `UNKNOWN` として扱う

各要素には情報状態（`KNOWN` / `INFERRED` / `UNKNOWN` / `CONFLICTING`）を付けます。

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

v1.0 では、Pragmatics と Audience / Context を同じ STEP で扱います。

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

STEP 1〜6 の結果を統合し、Meaning Audit Report を作成します（[output-format.md](output-format.md)）。

1. Finding を Finding Ledger にまとめる（ID: `F-01`, `F-02`, …）
2. 各 Finding に Finding Type（[finding-types.md](finding-types.md)）、Stage、Status、情報状態を付ける
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
| UNSUPPORTED | Evidence Boundary 内の Source を確認したが、支える記述が無い、または Source と矛盾する |
| UNKNOWN | Source が範囲外・読めない・不十分などの理由で判定できない |

`UNSUPPORTED` は「提供された Source では支えられていない」という意味であり、それだけで「虚偽」を意味しません。Source と矛盾する場合は、情報状態に `CONFLICTING` を付けます。

Mode B（Artifact-Only）:

| Status | 意味 |
|---|---|
| TRACEABLE | 成果物の中で、根拠から主張までの道筋が示されている |
| PARTIALLY TRACEABLE | 根拠は示されているが、主張までの道筋に欠落がある |
| UNTRACEABLE | 成果物の中に、その主張の根拠が示されていない |
| UNKNOWN | 判定できない（読めない図、意味が曖昧、など） |

`UNTRACEABLE` は「誤り」を意味しません。Mode B では、外部 Evidence なしに誤りと断定してはなりません。

### 情報状態（Unknown Policy）

| 情報状態 | 意味 |
|---|---|
| KNOWN | 利用可能な資料で直接確認できる |
| INFERRED | 監査者の推論による。推論であることを明記する |
| UNKNOWN | 利用可能な資料では分からない |
| CONFLICTING | 資料同士、または資料と成果物が食い違っている |

Unknown は欠陥ではなく情報状態です。次の変換を禁止します。

```text
UNKNOWN → plausible assumption → fact
```

- UNKNOWN をもっともらしい推測で埋めない
- INFERRED を後の STEP で KNOWN として扱わない
- 判定に必要な情報が無いときは、無いことを記録して先に進む

---

## STEP 8: Human Review

AI の監査は STEP 7 で終わります。STEP 8 は人間が行います。

- Human Review Required に挙がった項目を中心に、Finding ごとに対応を決める
- 対応は `accept` / `revise` / `investigate` / `hold` / `reject` / `no action` のいずれか
- AI は対応を選びません。AI はレビューで確認すべき問いを示すところまでを担います

手順と記録形式は 付録 B（Human Review）。

---

## v1.0 で行わないこと

- スコアリング、等級付け、ランキング
- 自動 Rewrite（修正文の提示を含む）
- 自動意思決定
- 新しい Finding Type や新概念の自動採用（必要に見えたら Human Review Required に挙げ、必要に応じて Human Review で記録する）

---

## 付録 A: Document Classes

v1.0 では 3 つの Document Class を使います。Class によって Workflow の STEP は変わりません。変わるのは、各 STEP で重点的に見る観点です。

### Class A: Presentation / Visualization

対象例: AI 生成プレゼンテーション、NotebookLM 生成資料、図解、要約スライド

重点:

| 観点 | 主に見る STEP | 対応する Finding Type |
|---|---|---|
| Selection | 3 | SELECTION |
| Compression | 3 | COMPRESSION |
| Framing | 5 | FRAMING |
| Visualization | 5 | VISUAL_CLAIM |
| Visual Claim | 1, 5 | VISUAL_CLAIM |
| Causal implication | 4 | CAUSAL_IMPLICATION |
| Meaning amplification | 6 | AMPLIFICATION |

### Class B: Article / Report / Explanatory Document

対象例: 雑誌記事、Web 記事、論文、学生レポート、解説記事

重点:

| 観点 | 主に見る STEP | 対応する Finding Type |
|---|---|---|
| Evidence と Interpretation の境界 | 2, 3 | EVIDENCE_INTERPRETATION_BLUR |
| Narrative | 5 | NARRATIVE |
| Editorial framing | 5 | NARRATIVE / FRAMING |
| Quote handling | 3 | QUOTE_HANDLING |
| Context preservation | 5 | CONTEXT_LOSS |
| Title-body relationship | 5 | TITLE_BODY_GAP |

### Class C: Proposal / Analysis / Decision Document

対象例: Web 改善提案、AI 事業分析、企画書、戦略資料、コンサルティング提案

重点:

| 観点 | 主に見る STEP | 対応する Finding Type |
|---|---|---|
| Evidence | 2 | （Status で記録） |
| Inference | 4 | INFERENCE_GAP / CAUSAL_IMPLICATION |
| Warrant | 4 | INFERENCE_GAP |
| Recommendation | 6 | COMMITMENT_ESCALATION |
| Commitment | 6 | COMMITMENT_ESCALATION / AMPLIFICATION |

### 判定のしかた

- 成果物の主な目的で判定する（見せる → A、説明する → B、判断を導く → C）
- 複数に該当する場合は、主たる Class を 1 つ選び、副次的な Class を併記する
  - 例: 提案スライド → `Class C（主）/ Class A（副）`
- 重点観点以外の Finding も、見つけたら記録する（重点は優先順位であり、制限ではない）

---

## 付録 B: Human Review

Meaning Audit は AI だけで完結しません。STEP 8 の Human Review で、人間が Finding ごとの対応を決めて、初めて監査が完了します。

---

### 役割

| AI | Human |
|---|---|
| trace / expose / question / classify | accept / revise / investigate / hold / reject / no action |

AI は Human Decision を選びません。AI の出力に Human Decision が書かれていた場合、それは無効とし、人間が改めて決めます。

### Human Decision の定義

| Decision | 意味 | 次の行動の例 |
|---|---|---|
| accept | Finding を妥当と認め、成果物の問題として受け入れる | 成果物の修正・注記を検討する |
| revise | Finding の内容・Status・Finding Type を修正する | Finding Ledger を書き換え、理由を記録する |
| investigate | 判断に追加の確認が必要 | Source を確認する、作成者に問い合わせる |
| hold | 現時点では判断しない | 保留理由と再検討の条件を記録する |
| reject | Finding を妥当でないと判断する | 却下理由を記録する |
| no action | Finding は妥当だが、対応は不要と判断する | 不要と判断した理由を記録する |

`accept` は「Finding を受け入れる」という意味で、成果物の修正方法までは決めません。修正方法を決めるのは、Meaning Audit の外側の作業です。

### 手順

1. Report の Audit Mode と Evidence Boundary を確認する（Mode B なのに誤りと断定していないか）
2. Human Review Required の項目を順に確認する
3. Finding Ledger の残りの Finding を確認する
4. Critical Unknowns と Source Verification Required のうち、自分で確認できるものを確認する
5. Finding ごとに Human Decision を記録する
6. 監査全体についての所見を記録する
7. Workflow や Skill の不具合、新しい概念が必要に見えた点に気づいた場合は、Human Review の記録（下の「Workflow / Prompt へのフィードバック」欄）に残す

### レビューで確認する観点

- UNKNOWN が、もっともらしい推測で埋められていないか
- INFERRED が、後の記述で事実（KNOWN）として扱われていないか
- Mode B で「誤り」「虚偽」と断定していないか
- AI が修正案・採点・推奨判断を出していないか
- Meaning Trace の各 Stage が空欄になっていないか
- 監査者の外部知識に依存した判定が、Evidence Boundary に記録されているか

### 記録形式

Human Review の記録は、以下の形式で残せます（保存するかどうか、保存先は利用者が決める）。

```markdown
# Human Review Record

- Report: <Report の名前・保存場所>
- Reviewer: <名前>
- Date: <YYYY-MM-DD>

## Decisions

| Finding | Decision | 理由 | 次の行動 |
|---|---|---|---|
| F-01 | | | |

## Source Verification Results

| SV | 結果 | 備考 |
|---|---|---|
| SV-1 | | |

## 監査全体についての所見

## Workflow / Prompt へのフィードバック

- Workflow や Skill の不具合として記録した項目:
- 新しい概念の候補として記録した項目:
```

---

## 付録 C: Audit Modes

v1.0 では 2 つの監査モードを使います。どちらのモードも同じ STEP 0〜8 を実行します。違いは、STEP 2（Evidence / Source Trace）で何を根拠として扱うかと、使う Status です。

### Mode A: Source-Grounded Audit

元資料または Evidence が利用可能な場合。

- Source と成果物を照合し、提示された Meaning が Source にどこまで支えられているかを判定する
- Status: `SUPPORTED` / `PARTIALLY SUPPORTED` / `UNSUPPORTED` / `UNKNOWN`
- `UNSUPPORTED` は「提供された Source では支えられていない」という意味で、それだけで「虚偽」を意味しない

### Mode B: Artifact-Only Audit

最終成果物しか利用できない場合。

- 元資料への忠実性は判定しない
- 成果物の内部で、Claim、Meaning Shift、Inference、Framing、Traceability を見る
- Status: `TRACEABLE` / `PARTIALLY TRACEABLE` / `UNTRACEABLE` / `UNKNOWN`
- 外部 Evidence なしに「誤り」と断定してはならない
- 元資料と照合すべき主張は Source Verification Required に挙げる

### モードの判定

| 状況 | Mode |
|---|---|
| Source が提供されている | Mode A |
| Source が提供されていない（none、空欄、名前や URL だけ） | Mode B |
| Source が一部だけ提供されている | Mode A。Source の無い Meaning Unit は `UNKNOWN` とし、Source Verification Required に記載 |

この Skill は STEP 0 でモードを判定し、元資料が無い場合は Source verification ができないことを明示して Mode B に切り替えます。

### Status の対応

Mode A と Mode B の Status は、同じ意味の言い換えではありません。

| Mode A | Mode B | 違い |
|---|---|---|
| SUPPORTED | TRACEABLE | A は Source が支えているか。B は成果物内で道筋が示されているか |
| PARTIALLY SUPPORTED | PARTIALLY TRACEABLE | |
| UNSUPPORTED | UNTRACEABLE | B では「根拠が示されていない」だけで、内容の正誤は言えない |
| UNKNOWN | UNKNOWN | |

1 つの Report の中で、両方の Status を混在させません。

---

## 付録 D: Terminology

v1.0 で使う用語です。用語の追加は Human Review を経て行います（この Skill では用語を追加しません）。

### 構造

| 用語 | 定義 |
|---|---|
| Evidence / Source | 成果物の元になった資料・データ・証拠。Mode B では外部 Source は無く、成果物内で根拠として示されたものを扱う |
| Interpretation | Evidence / Source を読み、選び、まとめること |
| Inference / Warrant | 解釈から主張・結論へ進む推論と、根拠と結論をつなぐ理由 |
| Context / Pragmatics | 見出し・配置・語彙・図・想定読者など、表現の置かれ方によって生じる意味。v1.0 では Audience / Context と同じ STEP で扱う（概念上は分離） |
| Commitment | 成果物がある Meaning を判断・結論・推奨として採用すること |
| Integration | 各 STEP の結果を Report にまとめること |
| Human Review | 人間が Finding ごとの対応を決めること |

### 監査の単位と記録

| 用語 | 定義 |
|---|---|
| Audit Object | 監査対象の成果物 |
| Audit Purpose | 監査の目的。指定が無い場合の既定値は「Meaning Shift の所在を明らかにする」 |
| Evidence Boundary | 監査で参照した範囲と、参照していない範囲の境界 |
| Meaning Unit | 監査の単位となる、意味を担う主張・表現（`MU-01`〜） |
| Meaning Shift | 根拠から提示された Meaning までの間で、意味が加わる・変形される・強められる・弱められる・採用されること |
| Key Meaning Shift | 監査目的に照らして重要な Meaning Shift（`KS-1`〜） |
| Meaning Trace | 1 つの Key Meaning Shift を、Stage ごとに追跡した表 |
| Finding | 監査で記録する個別の指摘（`F-01`〜） |
| Finding Ledger | すべての Finding の一覧表 |
| Finding Type | Finding の種類を表す運用ラベル（[finding-types.md](finding-types.md)） |
| Critical Unknown | 判定結果を左右する Unknown |
| Source Verification Required | 元資料との照合が必要な主張の一覧 |
| Human Review Required | 人間の判断が必要な Finding と、確認すべき問いの一覧 |

### 監査モードと Status

| 用語 | 定義 |
|---|---|
| Mode A: Source-Grounded Audit | 元資料と照合する監査 |
| Mode B: Artifact-Only Audit | 成果物だけで行う監査。元資料への忠実性は判定しない |
| SUPPORTED / PARTIALLY SUPPORTED / UNSUPPORTED / UNKNOWN | Mode A の Status |
| TRACEABLE / PARTIALLY TRACEABLE / UNTRACEABLE / UNKNOWN | Mode B の Status |

定義の詳細は この文書の STEP 7。

### 情報状態

| 用語 | 定義 |
|---|---|
| KNOWN | 利用可能な資料で直接確認できる |
| INFERRED | 監査者の推論による |
| UNKNOWN | 利用可能な資料では分からない |
| CONFLICTING | 資料同士、または資料と成果物が食い違う |

### Human Decision

| 用語 | 定義 |
|---|---|
| accept | Finding を妥当と認める |
| revise | Finding の内容・Status・種類を修正する |
| investigate | 追加の確認を行う |
| hold | 現時点では判断しない |
| reject | Finding を妥当でないと判断する |
| no action | Finding は妥当だが対応は不要と判断する |
