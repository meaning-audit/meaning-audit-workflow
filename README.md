# Meaning Audit Workflow

> 次の理論を書く前に、今の理論を動かす。

Meaning Audit Workflow は、文書・AI 生成物・提案・記事・プレゼンテーションを、Claude Code や ChatGPT などの AI に投入して実際に監査するための Operational Workflow です。

- Version: v1.0（初期構築中・Human Review 前）
- Organization: `meaning-audit`
- Repository: `meaning-audit-workflow`

---

## Meaning Audit とは

Meaning Audit は、Evidence または Source から、最終的に提示された Meaning までの間で、

- どこで意味が加わったか
- どこで変形されたか
- どこで推論されたか
- どこで判断として採用されたか

を追跡する方法論です。

```text
Evidence / Source
  → Interpretation
  → Inference / Warrant
  → Context / Pragmatics
  → Commitment
  → Integration
  → Human Review
```

Pragmatics と Audience / Context は概念上は別のものですが、v1.0 の Minimum Workflow では同じ operational step（STEP 5）で扱います。

## 何をしないか

このリポジトリは、文書を採点したり、書き直したり、判断を代行したりしません。

| AI の役割 | Human の役割 |
|---|---|
| trace（追跡する） | accept（受け入れる） |
| expose（露出させる） | revise（修正する） |
| question（問いを立てる） | investigate（調査する） |
| classify（分類する） | hold（保留する） |
| | reject（却下する） |
| | no action（対応しない） |

監査は AI だけで完結しません。最終判断は必ず Human Review で行います。

## クイックスタート

1. [prompts/minimum-audit-v1.0.md](prompts/minimum-audit-v1.0.md) のプロンプト本文をコピーする
2. 末尾の `INPUT` 欄に、監査対象（Audit Object）、元資料（あれば）、監査目的を貼り付ける
3. Claude Code / ChatGPT などに投入する
4. 出力された Meaning Audit Report を [workflow/human-review.md](workflow/human-review.md) の手順で人間がレビューする

元資料がない場合、プロンプトは Source verification ができないことを明示し、Artifact-Only Audit に切り替えます。

監査モードが最初から決まっている場合は、専用プロンプトを使えます。

- [prompts/source-grounded-audit.md](prompts/source-grounded-audit.md) — Mode A（元資料あり）
- [prompts/artifact-only-audit.md](prompts/artifact-only-audit.md) — Mode B（成果物のみ）

## Install as a Claude Code Skill

Meaning Audit Workflow v1.0 は、Claude Code の Agent Skill としても使えます。Skill の本体は [skills/meaning-audit/](skills/meaning-audit/) で、位置づけは **installable implementation of Meaning Audit Workflow v1.0** です。方法・Status・Finding Type・STEP は Workflow v1.0 と同じで、新しい手順や概念は加えていません（Skill として動かすための運用上の指示だけを `SKILL.md` に加えています）。

> 同じ入力でも、Finding の件数、まとめ方、Finding Type、Status などは実行ごとに変わる可能性があります。Meaning Audit Skill は Human Review を前提としています。

### 1. リポジトリを取得する

```bash
git clone https://github.com/meaning-audit/meaning-audit-workflow.git
```

### 2a. 個人用 Skill として入れる（すべてのプロジェクトで使える）

`skills/meaning-audit` を `~/.claude/skills/` にコピーします。

macOS / Linux:

```bash
mkdir -p ~/.claude/skills
cp -R meaning-audit-workflow/skills/meaning-audit ~/.claude/skills/
```

Windows（PowerShell）:

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills" | Out-Null
Copy-Item -Recurse -Force .\meaning-audit-workflow\skills\meaning-audit "$HOME\.claude\skills\"
```

### 2b. Project Skill として入れる（そのプロジェクトだけで使える）

監査したいプロジェクトのルートで、`.claude/skills/` にコピーします。チームで共有する場合は、このディレクトリをプロジェクトのリポジトリにコミットします。

macOS / Linux:

```bash
mkdir -p .claude/skills
cp -R /path/to/meaning-audit-workflow/skills/meaning-audit .claude/skills/
```

Windows（PowerShell）:

```powershell
New-Item -ItemType Directory -Force ".claude\skills" | Out-Null
Copy-Item -Recurse -Force C:\path\to\meaning-audit-workflow\skills\meaning-audit ".claude\skills\"
```

コピー後、`<skills ディレクトリ>/meaning-audit/SKILL.md` があることを確認し、Claude Code を起動し直してください。

### 3. 使い方

Claude Code で、`/meaning-audit` を呼び出すか、Meaning Audit を依頼します。

```text
/meaning-audit slides.pdf を監査して。元資料は source-report.pdf
```

```text
この提案書（proposal.docx の内容を貼り付け）を Meaning Audit して。元資料はありません
```

```text
article.md の主張の根拠をたどって、元資料 data.csv からどこで意味が変わったか見て
```

- 元資料があれば Mode A（Source-Grounded）、無ければ Mode B（Artifact-Only）で監査します。元資料が無くても監査は行い、Source に対する正しさは判定しません
- 出力は 13 セクションの Meaning Audit Report です。Human Decision 欄は空欄で返ってくるので、[workflow/human-review.md](workflow/human-review.md) に従って人間が判断してください
- 更新するときは `git pull` してから、もう一度コピーしてください

## Audit Modes

| Mode | 条件 | 主な判定 |
|---|---|---|
| A: Source-Grounded Audit | 元資料・Evidence が利用可能 | SUPPORTED / PARTIALLY SUPPORTED / UNSUPPORTED / UNKNOWN |
| B: Artifact-Only Audit | 最終成果物しか利用できない | TRACEABLE / PARTIALLY TRACEABLE / UNTRACEABLE / UNKNOWN |

Artifact-Only Audit では、外部 Evidence なしに「誤り」と断定しません。詳細は [docs/audit-modes.md](docs/audit-modes.md)。

## Document Classes

| Class | 対象例 | 重点 |
|---|---|---|
| A: Presentation / Visualization | AI 生成プレゼン、NotebookLM 生成資料、図解、要約スライド | Selection, Compression, Framing, Visualization, Visual Claim, Causal implication, Meaning amplification |
| B: Article / Report / Explanatory Document | 雑誌記事、Web 記事、論文、学生レポート、解説記事 | Evidence と Interpretation の境界, Narrative, Editorial framing, Quote handling, Context preservation, Title-body relationship |
| C: Proposal / Analysis / Decision Document | Web 改善提案、AI 事業分析、企画書、戦略資料、コンサルティング提案 | Evidence, Inference, Warrant, Recommendation, Commitment |

詳細は [docs/document-classes.md](docs/document-classes.md)。

## Minimum Workflow v1.0

| STEP | 名称 |
|---|---|
| 0 | Frame |
| 1 | Claim / Meaning Unit Detection |
| 2 | Evidence / Source Trace |
| 3 | Interpretation Audit |
| 4 | Inference / Warrant Audit |
| 5 | Context / Pragmatics Audit |
| 6 | Commitment Audit |
| 7 | Integration |
| 8 | Human Review |

仕様本体: [workflow/meaning-audit-workflow-v1.0.md](workflow/meaning-audit-workflow-v1.0.md)

## 標準成果物: Meaning Audit Report

1. Audit Object
2. Audit Mode
3. Document Class
4. Audit Purpose
5. Evidence Boundary
6. Overall Finding
7. Key Meaning Shifts
8. Meaning Trace
9. Finding Ledger
10. Critical Unknowns
11. Source Verification Required
12. Human Review Required
13. Limitations

フォーマット: [workflow/output-format.md](workflow/output-format.md)

## Unknown Policy

Unknown は欠陥ではなく情報状態です。情報状態は `KNOWN` / `INFERRED` / `UNKNOWN` / `CONFLICTING` で記録します。

禁止: `UNKNOWN → plausible assumption → fact`

## リポジトリ構成

```text
docs/       原則・監査モード・文書クラス・限界・用語
workflow/   v1.0 Workflow 仕様、出力フォーマット、Finding 種別、Human Review 手順
prompts/    AI に直接投入する監査プロンプト
examples/   テストケース（01 AI 生成プレゼン / 02 公開記事 / 03 提案・分析文書）
tests/      テストログ、失敗パターン、Post-Freeze 候補
skills/     Claude Code の Agent Skill（meaning-audit）
```

## v1.0 の範囲外

v2.0 設計、新理論の追加、スコアリング、SaaS 化、Engine 実装、Knowledge Graph 化、自動 Rewrite、自動意思決定、Publication ranking、AI 品質ランキング。

新しい概念が必要に見えた場合は、本仕様に採用せず [tests/post-freeze-candidates.md](tests/post-freeze-candidates.md) に候補として記録します。

## ライセンス

方法論・ドキュメントは CC BY 4.0 を候補としています（最終確定前）。詳細は [LICENSE](LICENSE)。

## 引用

[CITATION.cff](CITATION.cff) を参照してください。

## 貢献

[CONTRIBUTING.md](CONTRIBUTING.md) を参照してください。
