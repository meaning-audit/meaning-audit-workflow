# Test 01: AI-Generated Presentation

- Status: 準備完了（監査対象は未選定・監査は未実施）
- Workflow: Meaning Audit Workflow v1.0
- 想定 Document Class: Class A: Presentation / Visualization

---

## テストの原則

Test 01 の目的は、「Meaning Audit が正しいことを証明すること」ではありません。

目的は、Meaning Audit Workflow v1.0 を実際の AI 生成プレゼンに投入したとき、

- 何が見えるか
- 何が見えないか
- どこで Workflow が壊れるか

を観察することです。

- 監査がうまくいかなかったことも、テスト結果として記録します
- 新しい概念が必要に見えても、Workflow・Prompt・Finding Types には追加しません。[../../tests/post-freeze-candidates.md](../../tests/post-freeze-candidates.md) に候補として記録します
- テスト中に Prompt を書き換えません。改善案は記録だけ残し、修正は Human Review の後に行います

---

## 1. Test Metadata

監査を実行する前に記入します（Audit Mode と Document Class は、監査後に AI の判定と人間の確認を併記します）。

| 項目 | 内容 |
|---|---|
| Test ID | Test 01-<実行番号>（例: `Test 01-1`） |
| Date | <YYYY-MM-DD> |
| Audit Object | <名称・スライド枚数・ファイル名（`input/` 内）> |
| Generation Tool | <生成に使った AI ツール・モデル名（例: NotebookLM、Gamma、ChatGPT など）。不明なら UNKNOWN> |
| Input Format | <AI に投入した形式: PDF / 画像 / テキスト抽出 / PPTX など> |
| Audit Mode | AI の判定: <Mode A / Mode B> ／ Human 確認: <同意 / 不同意（理由）> |
| Document Class | AI の判定: <A / B / C（副次 Class）> ／ Human 確認: <同意 / 不同意（理由）> |
| Source Availability | <あり（全部）/ あり（一部）/ なし>。ありの場合は Source の名称と `input/` 内のファイル名 |
| Audit Purpose | <目的。空欄で実行した場合は「既定値を使用」と記入> |
| Audit Prompt | <使用したプロンプトのファイル名（例: `prompts/minimum-audit-v1.0.md`）> |
| Audit Model | <監査に使った AI・環境（例: Claude Code / ChatGPT とモデル名）> |
| Human Reviewer | <名前> |

注: Generation Tool（プレゼンを生成した AI）と Audit Model（監査した AI）は分けて記録します。

---

## 2. Test Objective

このテストでは、主に次の観点を観察します。各観点について、Finding が出たかどうかだけでなく、Workflow で扱えたかどうかを記録します。

| 観点 | 対応する Finding Type | Finding の有無 | Workflow で扱えたか | メモ |
|---|---|---|---|---|
| Selection | SELECTION | | 扱えた / 一部 / 扱えなかった | |
| Compression | COMPRESSION | | | |
| Framing | FRAMING | | | |
| Visualization | VISUAL_CLAIM | | | |
| Visual Claim | VISUAL_CLAIM | | | |
| Causal implication | CAUSAL_IMPLICATION | | | |
| Meaning amplification | AMPLIFICATION | | | |

---

## 3. Test Questions

監査と Human Review が終わった後に記入します。回答には、根拠となる Report の箇所（Finding ID、KS 番号など）を付けます。

| # | Question | 観察結果 | 根拠 |
|---|---|---|---|
| Q1 | AI 生成プレゼンでは、どのような Meaning Shift が検出されるか | | |
| Q2 | Artifact-Only Audit でも有用な Finding が得られるか | | |
| Q3 | Visual 表現に由来する Meaning が監査できるか | | |
| Q4 | Meaning Trace はプレゼン資料でも機能するか | | |
| Q5 | 現行 Prompt で不足する質問は何か | | |
| Q6 | 冗長な監査ステップは何か | | |
| Q7 | Human Review が必要になる地点はどこか | | |

補足:

- Q2 は、Source がある場合でも、比較のために Mode B（[../../prompts/artifact-only-audit.md](../../prompts/artifact-only-audit.md)）でも実行すると観察しやすくなります。実行するかは Human が決めます
- Q3 では、Input Format によって AI が図を読めたかどうかを必ず記録します
- Q5・Q6 の回答は、Prompt の修正案ではなく観察として書きます

---

## 4. 実行手順

1. 監査対象（AI 生成プレゼン）を Human が選び、`input/` に置く。公開できない場合は、出典情報だけを [input/README.md](input/README.md) に書く
2. Source があれば `input/` に置く
3. 「1. Test Metadata」の監査前の項目を記入する
4. [../../prompts/minimum-audit-v1.0.md](../../prompts/minimum-audit-v1.0.md) で監査を実行する（Mode が決まっていれば専用プロンプトも可）
5. AI の出力を編集せずに `audit/` に保存する
6. [../../workflow/human-review.md](../../workflow/human-review.md) に従って Human Review を行い、`review/` に保存する
7. 「1. Test Metadata」の残り、「2. Test Objective」、「3. Test Questions」を記入する
8. テスト全体と、失敗パターン・概念候補を `tests/` に記録する

---

## 5. Test Outputs

| 保存先 | 内容 |
|---|---|
| [input/](input/) | 監査対象（と Source） |
| [audit/](audit/) | AI による Meaning Audit Report（無編集） |
| [review/](review/) | Human Review の記録 |
| [../../tests/test-log.md](../../tests/test-log.md) | テスト全体の記録 |
| [../../tests/failure-patterns.md](../../tests/failure-patterns.md) | 再発する失敗パターン |
| [../../tests/post-freeze-candidates.md](../../tests/post-freeze-candidates.md) | 新しい概念の候補 |

---

## 6. 完了条件

次がすべて揃ったら、Test 01 の 1 回の実行は完了です。

- [ ] `input/` に監査対象（または出典情報）がある
- [ ] `audit/` に Meaning Audit Report がある
- [ ] `review/` に Human Review の記録がある
- [ ] このファイルの「1」〜「3」が記入されている
- [ ] `tests/test-log.md` にエントリがある
- [ ] 失敗パターン・概念候補があった場合、`tests/` に記録されている（無ければ「なし」と test-log に書く）

---

## 記録: Test 01-1: Presentation Artifact — Generation Provenance Unknown（2026-10-06）

Status: AI による実行・比較準備と、Human Review の一部（HR-01, HR-02, FP-005 の暫定判断）まで完了。下の観察結果は暫定です。

HR-01: 監査対象が AI 生成であることは確認できなかったため、Test 01-1 は「AI-Generated Presentation」とは確定せず、Generation Provenance Unknown のプレゼンテーション資料として扱います。

HR-02: 公開版は匿名化しています。実名入りの原本は Private Evidence Layer に保管し、公開していません。

### Test Metadata

| 項目 | 内容 |
|---|---|
| Test ID | Test 01-1 |
| Date | 2026-10-06 |
| Audit Object | 第三者企業（Company A）のサービス紹介資料（PDF, 36 ページ）。リポジトリには置いていない（[input/README.md](input/README.md)） |
| Generation Tool | UNKNOWN（Generation Provenance Unknown） |
| Input Format | ページ画像 PNG（110 dpi × 36）＋ PDF テキスト層 |
| Audit Mode | AI の判定: Mode B（Artifact-Only） ／ Human 確認: Source が無いため妥当 |
| Document Class | AI の判定: Class A（主）/ Class C（副） ／ Human 確認: 未 |
| Source Availability | なし（Run 01A は実行していない） |
| Audit Purpose | 既定値を使用 |
| Audit Prompt | `prompts/artifact-only-audit.md`（Run 01B） |
| Audit Model | Claude Opus 5.5（Claude Code の subagent。この会話の文脈を持たない状態で実行） |
| Human Reviewer | リポジトリ管理者 |

### Test Objective（暫定）

| 観点 | Finding の有無 | Workflow で扱えたか | メモ |
|---|---|---|---|
| Selection | あり（F-14、KS-2） | 扱えた | |
| Compression | 明示的な Finding は無し | 一部 | Source が無いため、何が落ちたかは判定できない |
| Framing | あり（F-11, F-20, p9） | 扱えた | |
| Visualization | あり（F-07, F-12） | 扱えた | 象限図、目盛りの無い棒グラフ |
| Visual Claim | あり（F-01） | 扱えた | グラフと数値パネルの不一致 |
| Causal implication | あり（F-15） | 扱えた | |
| Meaning amplification | あり（F-06, F-08, F-21） | 扱えた | |

### Test Questions（暫定）

| # | 観察結果 | 根拠 |
|---|---|---|
| Q1 | 見出しによる強化、グラフと数値の不一致、マクロ統計から事業結論への Warrant の欠落、前提の書かれていないシミュレーション、因果の帰属のずれ、絶対的な表現。ただし AI 生成に特有の Shift かどうかは判別できない（HR-01） | KS-1〜KS-7 |
| Q2 | 得られた。成果物の中の検算とページをまたいだ照合で 26 件。ただし事例・実績の真偽は扱えない | [review/mode-comparison.md](review/mode-comparison.md) の 4・8 |
| Q3 | 画像として入力すれば監査できた（p6, p8, p10, p29）。小さな文字は読み取りの確度が下がる | 公開版 Report の 13 |
| Q4 | 機能した。7 Stage がすべて埋まった。ただし Stage をまたぐ Shift の書き方が定義されていない | FP-004 |
| Q5 | 成果物の中の検算の位置づけ、CONFLICTING のときの Status、生成過程の来歴 | FP-003, FP-005, PFC-004 |
| Q6 | 冗長なステップは特定できなかった。Finding が多く、Report の粒度が問題になった | FP-006 |
| Q7 | 外部統計の引用（p6〜p8）、事例・お客様の声、Visual Claim の解釈、過剰に推定した可能性のある INFERRED | [review/test-01-1-human-review.md](review/test-01-1-human-review.md) |

### ファイル

| ファイル | 内容 |
|---|---|
| [audit/test-01-1-public.md](audit/test-01-1-public.md) | 匿名化した Audit Report |
| [review/test-01-1-human-review.md](review/test-01-1-human-review.md) | Human Review の記録（HR-01, HR-02, FP-005, R-6） |
| [review/mode-comparison.md](review/mode-comparison.md) | モード比較（Run 01A 未実行のため限定的） |
