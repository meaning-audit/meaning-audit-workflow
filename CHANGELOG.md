# Changelog

このファイルは、Meaning Audit Workflow の変更を記録します。

## v1.1 — 2026-10-09

v1.1 は、v1.0 の Field Test で観察された記録上の問題をもとに、Workflow・Report の形式・Prompt・Skill の実行規則を改訂した版です。新しい理論は加えていません。v1.0 の仕様は削除せず、v1.1 の文書は版付きのファイル名で追加しています。移行の要点は [docs/migration-v1.0-to-v1.1.md](docs/migration-v1.0-to-v1.1.md)。

### Added

- Output Contract v1.1（[workflow/meaning-audit-output-contract-v1.1.md](workflow/meaning-audit-output-contract-v1.1.md)）：ヘッダー＋ 14 セクションの Report。欄ごとに必須・任意・条件付き、Canonical の値と自由記述を区別
- Meaning Units の出力（Report §8）：MU ID と内容。Location と Primary Claim Type は任意
- 要素ごとの情報状態（Information State by Element）：判断に関係する要素ごとに `KNOWN` / `INFERRED` / `UNKNOWN` / `CONFLICTING` を 1 つ記録する。必要な場合だけ部分に分ける
- Finding Ledger の 2 層：Finding Summary（1 Finding 1 行の分類）と Finding Detail（Content、要素ごとの情報状態、Evidence Note、任意の Annotation・Stage Path）
- Primary Stage（1 つ）と任意の Stage Path、任意の Primary Claim Type（日本語の 6 値）
- 任意の Audit Object Metadata（Generation Tool、Post-generation Human Editing、Source Set Status）。Audit Mode は決めない
- Runtime Validation v1.1（[runtime/meaning-audit-runtime-validation-v1.1.md](runtime/meaning-audit-runtime-validation-v1.1.md)）：Skill 実行時の検証規則 VR-01〜VR-27、段階（ERROR / WARNING / INFO）、全体の結果（PASS / PASS WITH WARNING / FAIL）、自動修正の境界、未解決の ERROR の扱い
- Runtime Record：実行と検証の記録。Report のセクションでも Audit Object Metadata でもない
- 表現と範囲の扱い：意味が提示に依存しうる場合は描画された表現を確認する。OCR を義務にしない。描画と抽出テキストを同じと仮定しない。条件に当たる場合は調べた表現と範囲を記録する
- 版付きの補助文書：Finding Types、Limitations、Terminology、Document Classes、Audit Modes、Human Review の v1.1

### Changed

- Document Class：Class の欄は Canonical の値 1 つだけ。他の Class の性質は自由記述に書く
- `UNKNOWN` の扱い：Evidence に基づいて選ぶ値であり、判断の難しさで選ばない（情報状態と両 Mode の Status に共通）。`UNKNOWN` の意味は欄で決まる。Canonical の値を意図しない記述では、単独の `UNKNOWN` ではなく「Evidence Boundary の中で確立できない」と書く
- Mode A の `UNSUPPORTED` / `UNKNOWN` の定義と判断の観点（明示的な帰属の有無、Source Set の範囲、要素の一部の支え、要約版の Source、食い違い）。元資料が一部だけの場合、提供された Source の中に支えが見つからないことだけで `UNSUPPORTED` も `UNKNOWN` も決めない
- `CONFLICTING` の定義：同じ判断に関係する 2 つ以上の要素が意味上両立しない場合。違いがあるだけでは該当しない。Status を自動的に決めない
- Prompt v1.1：1 つの Prompt（`minimum-audit-v1.1`）で Mode A・Mode B の両方を扱う。Report は Output Contract v1.1 の 14 セクション
- Human Review との関係：Human Review Required に挙げる場合の例（Status を 1 つに決められない、`CONFLICTING` が判断に影響する、material な帰属があいまい、Finding の粒度が分類に影響する）を明記。AI は Human Decision を書かない
- Skill：Workflow v1.1 の installable implementation として作り直した。references は v1.1 の内容だけで、v1.0 の references を含まない。Skill から実行した Report の Prompt 欄は `skill: meaning-audit (minimum-audit-v1.1)`

### Deprecated / Replaced（v1.0 の文書は残す）

- Finding 単位の集約した情報状態（v1.0 の Finding Ledger の「情報状態」列）→ 要素ごとの情報状態
- Meaning Trace の確立できない Stage を `UNKNOWN` と書く書き方 → 説明の自由記述。Meaning Trace に情報状態を書かない
- 複合の分類の値（副次 Class の併記、複数の Status、複合の情報状態など）→ 各欄に Canonical の値 1 つ
- v1.0 の Output Format（13 セクション）→ Output Contract v1.1（14 セクション）
- v1.0 の Mode 別の Prompt（`source-grounded-audit.md`、`artifact-only-audit.md`）は v1.0 の文書として残す。v1.1 には Mode 別の Prompt は無い

### Validation / Evidence

- Canonical v1.1 パッケージの検証を完了した（ファイルの完全性、リンク、版の表記、語彙、`UNKNOWN`、Report の構造、検証規則、Runtime Record、Skill パッケージ、Prompt の識別、模擬の入力による検証と自動修正の dry-run）
- Skill をローカルにインストールし、インストールしたパッケージがステージングのパッケージとバイト単位で一致すること、v1.0 と v1.1 の references が混在しないことを確認した
- Field Test 02-1 — v1.1 Runtime Conformance / Regression Check を実施した（既存の Test と同じ 1 つの成果物に対して、Mode A・Mode B 各 1 Run。`examples/02-published-article/` の Published Test 02 とは別のテスト）。Human Review の判定は **PASS WITH NOTES**
  - 両 Run で Runtime Validation は PASS。実装の実質的な退行は確立されなかった
  - Notes：Visual を確認しても、Visual の解釈が正しいことは保証されない（1 Run で、以前に訂正された図の読みが繰り返された）。Status の判断は、以前の Human Review の判断と異なる場合があった（Status の較正の変動として記録）。`CONFLICTING` を含む Finding が Human Review Required に挙がらない場合があった（実装の欠陥は確立されていない）。Mode B の Finding の粒度は以前の Run と異なった
- これらは、監査の正確さ、実行ごとの再現性、方法の有効性、v1.0 より優れていること、一般的な妥当性を示すものではない

## v1.0 — 2026-10-06

公開リポジトリの v1.0 の状態は commit `8774018`（Git の履歴で、v1.0 のすべてのコミットの日付は 2026-10-06）。以下はその初期構築の記録。

### Added

- リポジトリの初期ディレクトリ構成
- README.md 初稿
- `workflow/meaning-audit-workflow-v1.0.md`（Minimum Workflow STEP 0–8）
- `workflow/output-format.md`（Meaning Audit Report の標準フォーマット）
- `workflow/finding-types.md`、`workflow/human-review.md`
- `prompts/minimum-audit-v1.0.md`、`prompts/source-grounded-audit.md`、`prompts/artifact-only-audit.md`
- `docs/` 配下の原則・監査モード・文書クラス・限界・用語
- `examples/` 配下の 3 テストケースの枠組み（監査はまだ実施していない）
- `tests/` 配下の記録ファイル（test-log / failure-patterns / post-freeze-candidates）

### Pending Human Review

- LICENSE（CC BY 4.0 / Apache-2.0 は候補段階）
- CITATION.cff の著者情報
