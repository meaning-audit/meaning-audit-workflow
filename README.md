# Meaning Audit Workflow

> 次の理論を書く前に、今の理論を動かす。

Meaning Audit Workflow は、文書・AI 生成物・提案・記事・プレゼンテーションを、Claude Code や ChatGPT などの AI に投入して実際に監査するための Operational Workflow です。

- Current version: **v1.1**
- Previous version: v1.0（引き続き参照できます）
- Organization: `meaning-audit`
- Repository: `meaning-audit-workflow`

---

## Versions

### Current: v1.1

| 文書 | ファイル |
|---|---|
| Workflow v1.1 | [workflow/meaning-audit-workflow-v1.1.md](workflow/meaning-audit-workflow-v1.1.md) |
| Output Contract v1.1（Report の構造と欄） | [workflow/meaning-audit-output-contract-v1.1.md](workflow/meaning-audit-output-contract-v1.1.md) |
| Minimum Audit Prompt v1.1 | [prompts/minimum-audit-v1.1.md](prompts/minimum-audit-v1.1.md) |
| Runtime Validation v1.1（Skill 実行時の検証と Runtime Record） | [runtime/meaning-audit-runtime-validation-v1.1.md](runtime/meaning-audit-runtime-validation-v1.1.md) |
| Finding Types v1.1 | [workflow/finding-types-v1.1.md](workflow/finding-types-v1.1.md) |
| Human Review v1.1 | [docs/human-review-v1.1.md](docs/human-review-v1.1.md) |
| Audit Modes v1.1 / Document Classes v1.1 | [docs/audit-modes-v1.1.md](docs/audit-modes-v1.1.md) / [docs/document-classes-v1.1.md](docs/document-classes-v1.1.md) |
| Terminology v1.1 / Limitations v1.1 | [docs/terminology-v1.1.md](docs/terminology-v1.1.md) / [docs/limitations-v1.1.md](docs/limitations-v1.1.md) |
| Claude Code Skill（v1.1） | [skills/meaning-audit/](skills/meaning-audit/) |
| v1.0 から v1.1 への移行 | [docs/migration-v1.0-to-v1.1.md](docs/migration-v1.0-to-v1.1.md) |
| 変更履歴 | [CHANGELOG.md](CHANGELOG.md) |

### Previous: v1.0

v1.0 の仕様は削除していません。v1.0 の Report を読む・比べるときに使えます。v1.0 のリンクは v1.0 の文書を指したままです。

| 文書 | ファイル |
|---|---|
| Workflow v1.0 | [workflow/meaning-audit-workflow-v1.0.md](workflow/meaning-audit-workflow-v1.0.md) |
| Output Format v1.0（13 セクション） | [workflow/output-format.md](workflow/output-format.md) |
| Prompts v1.0 | [prompts/minimum-audit-v1.0.md](prompts/minimum-audit-v1.0.md)、[prompts/source-grounded-audit.md](prompts/source-grounded-audit.md)（Mode A）、[prompts/artifact-only-audit.md](prompts/artifact-only-audit.md)（Mode B） |
| Finding Types v1.0 / Human Review v1.0 | [workflow/finding-types.md](workflow/finding-types.md) / [workflow/human-review.md](workflow/human-review.md) |
| Audit Modes / Document Classes / Terminology / Limitations（v1.0） | [docs/audit-modes.md](docs/audit-modes.md) / [docs/document-classes.md](docs/document-classes.md) / [docs/terminology.md](docs/terminology.md) / [docs/limitations.md](docs/limitations.md) |

公開リポジトリの Skill（`skills/meaning-audit/`）は v1.1 の 1 つのパッケージです。v1.0 の Skill の references は含めていません。

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

Pragmatics と Audience / Context は概念上は別のものですが、Minimum Workflow では同じ operational step（STEP 5）で扱います。

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

監査は AI だけで完結しません。最終判断は必ず Human Review で行います（[docs/human-review-v1.1.md](docs/human-review-v1.1.md)）。

## クイックスタート（v1.1）

1. [prompts/minimum-audit-v1.1.md](prompts/minimum-audit-v1.1.md) の `BEGIN PROMPT` から `END PROMPT` までをコピーする
2. 末尾の `INPUT` 欄に、監査対象（Audit Object）、元資料（無ければ `none`）、監査目的（空欄可）を書く
3. Claude Code / ChatGPT などに投入する
4. 出力された Meaning Audit Report を [docs/human-review-v1.1.md](docs/human-review-v1.1.md) の手順で人間がレビューする

v1.1 の Prompt は `minimum-audit-v1.1` の 1 つで、Mode A と Mode B のどちらにも使います。Audit Mode は Prompt の中で判定します。元資料が無い場合は、Source verification ができないことを明示して Mode B で監査します。v1.1 には Mode 別の Prompt はありません。

## Install as a Claude Code Skill

Meaning Audit は Claude Code の Agent Skill としても使えます。Skill の本体は [skills/meaning-audit/](skills/meaning-audit/) で、位置づけは **installable implementation of Meaning Audit Workflow v1.1** です。方法・Status・Finding Type・STEP は Workflow v1.1 と同じで、Skill は新しい手順や概念を加えません。詳しくは [skills/README.md](skills/README.md)。

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

**v1.0 の Skill から更新する場合：** 以前の `meaning-audit` フォルダを取り除いてから、新しいフォルダをコピーしてください。上書きのコピーだけでは、v1.0 の `references/workflow.md` と `references/output-format.md` が残り、v1.0 と v1.1 の references が混在します。

### 3. 使い方

Claude Code で、`/meaning-audit` を呼び出すか、Meaning Audit を依頼します。

```text
/meaning-audit slides.pdf を監査して。元資料は source-report.pdf
```

```text
この提案書（proposal.docx の内容を貼り付け）を Meaning Audit して。元資料はありません
```

- 元資料があれば Mode A（Source-Grounded）、無ければ Mode B（Artifact-Only）で監査します。元資料が無くても監査は行い、Source に対する正しさは判定しません
- 出力は、ヘッダーと 14 セクションの Meaning Audit Report（Output Contract v1.1）です。Report のヘッダーの Prompt 欄は `skill: meaning-audit (minimum-audit-v1.1)` になります
- Skill は出力の前に Runtime Validation v1.1 で Report の構造と語彙を確かめ、Report の後に Runtime Record（実行と検証の記録）を示します。検証は Report の形を確かめるもので、監査の判断が正しいことは示しません
- Human Decision 欄は空欄で返ってきます。[docs/human-review-v1.1.md](docs/human-review-v1.1.md) に従って人間が判断してください
- Report は、保存を求めた場合だけファイルに保存されます
- 更新するときは `git pull` してから、上の手順でもう一度入れ直してください

## Audit Modes

| Mode | 条件 | Status |
|---|---|---|
| A: Source-Grounded Audit | 元資料・Evidence が利用可能 | SUPPORTED / PARTIALLY SUPPORTED / UNSUPPORTED / UNKNOWN |
| B: Artifact-Only Audit | 最終成果物しか利用できない | TRACEABLE / PARTIALLY TRACEABLE / UNTRACEABLE / UNKNOWN |

1 つの Report の中で 2 つの Status の体系を混ぜません。Artifact-Only Audit では、外部 Evidence なしに「誤り」と断定しません。元資料が一部だけの場合、提供された Source の中に支えが見つからないことだけで `UNSUPPORTED` も `UNKNOWN` も決めません。詳細は [docs/audit-modes-v1.1.md](docs/audit-modes-v1.1.md)。

## Document Classes

| Class | 対象例 | 重点 |
|---|---|---|
| A: Presentation / Visualization | AI 生成プレゼン、NotebookLM 生成資料、図解、要約スライド | Selection, Compression, Framing, Visualization, Visual Claim, Causal implication, Meaning amplification |
| B: Article / Report / Explanatory Document | 雑誌記事、Web 記事、論文、学生レポート、解説記事 | Evidence と Interpretation の境界, Narrative, Editorial framing, Quote handling, Context preservation, Title-body relationship |
| C: Proposal / Analysis / Decision Document | Web 改善提案、AI 事業分析、企画書、戦略資料、コンサルティング提案 | Evidence, Inference, Warrant, Recommendation, Commitment |

v1.1 では、Class の欄に書く値は 1 つだけです。他の Class の性質は判定理由などの自由記述に書きます。詳細は [docs/document-classes-v1.1.md](docs/document-classes-v1.1.md)。

## Minimum Workflow

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

仕様本体: [workflow/meaning-audit-workflow-v1.1.md](workflow/meaning-audit-workflow-v1.1.md)

## 標準成果物: Meaning Audit Report（Output Contract v1.1）

ヘッダー（Workflow version、Output Contract version、Prompt、Auditor、Date、Review status）と、次の 14 セクションです。

1. Audit Object
2. Audit Mode
3. Document Class
4. Audit Purpose
5. Evidence Boundary
6. Overall Finding
7. Key Meaning Shifts
8. Meaning Units
9. Meaning Trace
10. Finding Ledger（10.1 Finding Summary ／ 10.2 Finding Detail）
11. Critical Unknowns
12. Source Verification Required
13. Human Review Required
14. Limitations

フォーマット: [workflow/meaning-audit-output-contract-v1.1.md](workflow/meaning-audit-output-contract-v1.1.md)

## Information State と Unknown Policy

Stage（意味の変化がどの段階で起きたか）、情報状態（Evidence Boundary の中で何が分かっているか）、Status（Mode ごとの判断の結果）は別の次元です。

情報状態は `KNOWN` / `INFERRED` / `UNKNOWN` / `CONFLICTING` で、判断に関係する要素ごとに記録します（Finding 全体に 1 つではありません）。Meaning Trace には情報状態を書きません。

`UNKNOWN` は Evidence に基づいて選ぶ値であり、判断の難しさに基づいて選ぶ値ではありません。

禁止: `UNKNOWN → plausible assumption → fact`

## v1.1 の確認の範囲

v1.1 について行ったのは次のことです。

- Canonical v1.1 パッケージの検証（ファイルの完全性、リンク、語彙、Report の構造、検証規則、模擬の入力による検証の dry-run）
- Claude Code の Skill としてのローカルへのインストールと、インストールしたパッケージの検証
- 1 件の範囲を限った Field Test（Field Test 02-1：既存の Test と同じ 1 つの成果物に対する Mode A・Mode B 各 1 Run。`examples/02-published-article/` の Published Test 02 とは別のテスト）。Human Review の判定は **HUMAN-REVIEWED / PASS WITH NOTES**

Field Test 02-1 が示したのは、この範囲で、インストールした v1.1 の Skill が承認済みの仕様を実行し、実装の実質的な退行は確認されなかったことだけです。Notes として、Visual を確認しても Visual の読み取りが正しいとは限らないこと、Status の判断が以前の Human Review の判断と異なる場合があったことなどを記録しています（[CHANGELOG.md](CHANGELOG.md)）。

v1.1 は、次のことを示していません。

- 監査の正確さ
- 実行ごとの再現性
- 方法の有効性
- v1.0 より優れていること
- 一般的な妥当性

## リポジトリ構成

```text
docs/       監査モード・文書クラス・Human Review・限界・用語（v1.1 は -v1.1 付き、v1.0 は版なしの名前）、原則、移行ガイド
workflow/   Workflow 仕様、Output Contract / Output Format、Finding 種別（v1.1 と v1.0）
prompts/    AI に直接投入する監査プロンプト（v1.1：minimum-audit-v1.1、v1.0：3 種）
runtime/    Skill 実行時の検証規則と Runtime Record（v1.1）
examples/   テストケース
tests/      テストログ、失敗パターン、Post-Freeze 候補
skills/     Claude Code の Agent Skill（meaning-audit、v1.1）
```

## 範囲外

v2.0 設計、新理論の追加、スコアリング、SaaS 化、Engine 実装、Knowledge Graph 化、自動 Rewrite、自動意思決定、Publication ranking、AI 品質ランキング。

新しい概念が必要に見えた場合は、本仕様に採用せず [tests/post-freeze-candidates.md](tests/post-freeze-candidates.md) に候補として記録します。

## ライセンス

方法論・ドキュメントは CC BY 4.0 を候補としています（最終確定前）。詳細は [LICENSE](LICENSE)。

## 引用

[CITATION.cff](CITATION.cff) を参照してください。

## 貢献

[CONTRIBUTING.md](CONTRIBUTING.md) を参照してください。
