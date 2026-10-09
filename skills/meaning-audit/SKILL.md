---
name: meaning-audit
description: Run a Meaning Audit (Meaning Audit Workflow v1.1) on a document, AI-generated presentation, article, report, proposal, or analysis. Traces where meaning is added, transformed, inferred, and committed between Evidence/Source and the presented Meaning, and outputs a Meaning Audit Report (Output Contract v1.1) with Meaning Units, Meaning Trace, and a two-layer Finding Ledger for Human Review. Use when the user asks to "meaning audit" a file, to trace claims back to sources, to check how an AI-generated slide deck or summary changed the meaning of its source, or says 「Meaning Auditして」「意味監査して」「この資料の主張の根拠をたどって」「元資料からどこで意味が変わったか見て」. Not a fact-checker, scorer, or rewriter.
---

# Meaning Audit (Workflow v1.1)

Meaning Audit Workflow v1.1 に従って監査し、Output Contract v1.1 の Meaning Audit Report を出力する。この Skill は実行の層（execution layer）であり、新しい概念・分類・Status・Finding Type・情報状態・手順を追加しない。

Meaning Audit はファクトチェックではない。根拠から提示された Meaning までの間で、どこで意味が加わり、変形され、推論され、判断として採用されたかを追跡する。

## 正とする文書

監査の手順・判断・出力は、次の references に従う。この SKILL.md に手順の要約を置かない（references と食い違う別の版を作らないため）。

| ファイル | 内容 | 使い方 |
|---|---|---|
| [references/prompt-v1.1.md](references/prompt-v1.1.md) | Minimum Audit Prompt v1.1 | BEGIN〜END の本文を、そのまま監査の実行の指示として使う |
| [references/workflow-v1.1.md](references/workflow-v1.1.md) | Workflow v1.1（STEP 0〜8、Status と情報状態の定義、付録） | 定義を確かめるとき |
| [references/output-contract-v1.1.md](references/output-contract-v1.1.md) | Report の構造と欄（ヘッダー＋14 セクション） | 出力の形と欄の区分 |
| [references/finding-types.md](references/finding-types.md) | Finding Type 14 種と OTHER の扱い | 分類の値 |
| [references/runtime-validation-v1.1.md](references/runtime-validation-v1.1.md) | 表現と範囲、検証の規則、自動修正の境界、Runtime Record | 実行と検証 |
| [references/limitations.md](references/limitations.md) | 方法と AI 実行の既知の限界 | Limitations を書くとき |

## 役割と境界

- 役割は trace / expose / question / classify。最終判断はしない
- 監査対象を書き直さない、修正案を出さない。点数・等級・ランキング・総合評価を付けない。採否・意思決定をしない
- Human Decision を選ばない。Human Review Required に問いを書き、Human Decision 欄は空欄のまま返す
- Evidence Boundary の外の情報を、ユーザーの許可なく追加しない（自ら検索・取得して判定に使わない）。ユーザーが外部検索・取得を Evidence として明示的に許可した場合は、その範囲を Evidence Boundary に含めて記録したうえで利用できる
- UNKNOWN と CONFLICTING を、検証や整形の名目で消したり別の値に置き換えたりしない

## 入力の受け取り

1. 監査対象（Audit Object）、元資料（Source。無くてもよい）、監査目的（Audit Purpose。無くてもよい）、Report の言語を会話から受け取る。Prompt の INPUT 欄の代わりにこれらを使う。不足していても監査は拒否しない。Source が無ければ Mode B として実行する
2. ファイルを読み、監査に使う表現を決める。表現と Visual の扱いは [references/runtime-validation-v1.1.md](references/runtime-validation-v1.1.md) §2 に従う：
   - テキストがあっても、意味がレイアウト・色・強調・大きさ・順序・空間の関係・切れ・視覚の階層に依存しうる場合は、描画された表現を確認する
   - 画像があっても OCR を義務にしない。描画と抽出テキストを同じと仮定しない
   - 読めないものは推測で復元せず、Limitations に書く
3. 範囲の記録が必要な条件（runtime-validation §3）に当たる場合は、実際に調べた表現と範囲を Runtime Record に記録する

## 実行

1. [references/prompt-v1.1.md](references/prompt-v1.1.md) の本文に従って STEP 0〜7 を実行し、Report を作る
2. Report ヘッダーの Prompt 欄は `skill: meaning-audit (minimum-audit-v1.1)` とする（Prompt の本文は変えない。runtime-validation §1）
3. 出力の前に、runtime-validation §8 の検証規則（VR-01〜VR-27）で Report を確かめる
   - 意味に関わらず一義的に決まる修正だけを機械的に直す（runtime-validation §9）
   - Status、Finding Type、情報状態、Primary Stage、Finding・MU の境界、materiality、Mode の語彙、複合値のどれを残すかは自動で直さず、監査の判断に戻すか Human Review Required に挙げる
4. 未解決の ERROR が残る場合は、Report を検証済みの最終 Report として示さない。`VALIDATION FAILED — REPORT DRAFT` として、draft と未解決の ERROR を示す（runtime-validation §10）
5. Report の後に Runtime Record を示す（runtime-validation §11）。Runtime Record は Report のセクションではなく、Audit Object Metadata とも別

検証は Report の構造と語彙の整合を確かめるもので、監査の判断が正しいことを証明しない。Human Review を置き換えない。

## 出力と保存

- Report は会話に出力する。思考過程の全文は出力しない
- ユーザーが保存を求めた場合だけ、指定の場所に Markdown ファイルとして保存する。Runtime Record を含め、それ以外の永続的なファイルを自動で作らない

## 注記

この Skill は Meaning Audit Workflow v1.1 をインストールして使える形にしたもの（installable implementation）であり、実行ごとに同じ結果を出す監査エンジンではない。同じ入力でも、Finding の数・まとめ方・Finding Type・Status は実行ごとに変わりうる。
