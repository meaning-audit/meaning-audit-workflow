# Document Classes v1.1

- Name: Document Classes
- Version: v1.1
- Status: RELEASED（v1.1、2026-10-09）
- Basis: Document Classes v1.0（`docs/document-classes.md`）に、Human-approved な v1.1 の変更（AQ-1：Class の欄は Canonical の Class の値 1 つだけ）だけを反映したもの。3 つの Class、重点観点、対応する Finding Type は変更していない。v1.0 のファイルは変更していない

v1.1 では 3 つの Document Class を使います。Class によって Workflow の STEP は変わりません。変わるのは、各 STEP で重点的に見る観点です。判定の規則は [Workflow v1.1](../workflow/meaning-audit-workflow-v1.1.md) の STEP 0、Report の書き方は [Output Contract v1.1](../workflow/meaning-audit-output-contract-v1.1.md) の §3 です。

## Class A: Presentation / Visualization

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

## Class B: Article / Report / Explanatory Document

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

## Class C: Proposal / Analysis / Decision Document

対象例: Web 改善提案、AI 事業分析、企画書、戦略資料、コンサルティング提案

重点:

| 観点 | 主に見る STEP | 対応する Finding Type |
|---|---|---|
| Evidence | 2 | （Status で記録） |
| Inference | 4 | INFERENCE_GAP / CAUSAL_IMPLICATION |
| Warrant | 4 | INFERENCE_GAP |
| Recommendation | 6 | COMMITMENT_ESCALATION |
| Commitment | 6 | COMMITMENT_ESCALATION / AMPLIFICATION |

## 判定のしかた

- 成果物の主な目的で判定する（見せる → A、説明する → B、判断を導く → C）
- 複数に該当する場合は、主たる Class を 1 つ選ぶ。Class の欄には Canonical の Class の値（A / B / C）を 1 つだけ書く。副次 Class の欄、Class の配列、複合値、Class の中の括弧書きは使わない。他の Class の性質が監査に関係する場合は、Class の欄の外の自由記述（判定理由など）に書く
  - 例: 提案スライド → Class の欄は `C`。スライド形式であることは判定理由に書く
- 重点観点以外の Finding も、見つけたら記録する（重点は優先順位であり、制限ではない）

上の重点の表の「対応する Finding Type」の列にある `/` は、その観点に対応しうる Finding Type を並べたものです。Finding Type の欄に書く値は、Finding ごとに 1 つです（[Finding Types v1.1](../workflow/finding-types-v1.1.md)）。
