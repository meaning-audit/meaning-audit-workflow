# skills/

Meaning Audit Workflow を Claude Code の Agent Skill として使うためのディレクトリです。

- Current Skill version: **meaning-audit v1.1**（installable implementation of Meaning Audit Workflow v1.1）
- この Skill は v1.1 の 1 つのパッケージです。v1.0 の Skill の references（`workflow.md`、`output-format.md`）は含めていません
- インストール方法はリポジトリの [README.md](../README.md) の「Install as a Claude Code Skill」を参照してください。v1.0 の Skill から更新するときは、以前の `meaning-audit` フォルダを取り除いてからコピーしてください

## meaning-audit

| ファイル | 内容 | 元の文書 |
|---|---|---|
| [meaning-audit/SKILL.md](meaning-audit/SKILL.md) | 実行の層（execution layer）の指示：入力の受け取り、表現の扱い、実行、検証、Runtime Record、保存 | — |
| [meaning-audit/references/prompt-v1.1.md](meaning-audit/references/prompt-v1.1.md) | Minimum Audit Prompt v1.1。BEGIN〜END の本文を監査の実行の指示として使う | [prompts/minimum-audit-v1.1.md](../prompts/minimum-audit-v1.1.md) |
| [meaning-audit/references/workflow-v1.1.md](meaning-audit/references/workflow-v1.1.md) | Workflow v1.1 ＋ 付録 A〜D（Document Classes、Human Review、Audit Modes、Terminology の v1.1） | [workflow/meaning-audit-workflow-v1.1.md](../workflow/meaning-audit-workflow-v1.1.md) ほか |
| [meaning-audit/references/output-contract-v1.1.md](meaning-audit/references/output-contract-v1.1.md) | Output Contract v1.1（Report の構造と欄） | [workflow/meaning-audit-output-contract-v1.1.md](../workflow/meaning-audit-output-contract-v1.1.md) |
| [meaning-audit/references/runtime-validation-v1.1.md](meaning-audit/references/runtime-validation-v1.1.md) | Runtime Validation v1.1（表現と範囲、検証規則、自動修正の境界、Runtime Record） | [runtime/meaning-audit-runtime-validation-v1.1.md](../runtime/meaning-audit-runtime-validation-v1.1.md) |
| [meaning-audit/references/finding-types.md](meaning-audit/references/finding-types.md) | Finding Types v1.1 | [workflow/finding-types-v1.1.md](../workflow/finding-types-v1.1.md) |
| [meaning-audit/references/limitations.md](meaning-audit/references/limitations.md) | Limitations v1.1 | [docs/limitations-v1.1.md](../docs/limitations-v1.1.md) |

## 振る舞いの要点

- **Prompt の識別：** Skill から実行した Report のヘッダーの Prompt 欄は `skill: meaning-audit (minimum-audit-v1.1)`。Prompt の本文は直接実行と同じで、Prompt のファイルは 1 つ
- **表現と Visual：** 意味が配置・色・強調・順序などに依存しうる場合は、描画された表現を確認する。OCR を義務にしない。描画と抽出テキストを同じと仮定しない。読めないものは推測で復元せず Limitations に書く。条件に当たる場合は、実際に調べた表現と範囲を Runtime Record に記録する
- **Runtime Validation：** 出力の前に VR-01〜VR-27 で Report を確かめる。意味に関わらず一義的に決まる修正（ID の書式など）だけを機械的に直す。Status・Finding Type・情報状態などの意味の判断は自動で直さない。未解決の ERROR が残る場合は `VALIDATION FAILED — REPORT DRAFT` として示し、検証済みの Report として示さない
- **Runtime Record：** Report の後に示す。Report のセクションでも Audit Object Metadata でもない
- **保存：** Report は会話に出力する。利用者が保存を求めた場合だけ、指定の場所に保存する。それ以外の永続的なファイルを自動で作らない
- **Human Review：** Human Decision の欄は空欄のまま返す。検証は Report の構造と語彙の整合を確かめるもので、監査の判断が正しいことを示さず、Human Review を置き換えない

## 方針

- Skill は `workflow/`・`prompts/`・`runtime/`・`docs/` の v1.1 の内容を実行しやすくする包装であり、新しい手順・概念を追加しない
- 仕様の正は、上の表の「元の文書」。`references/` は、Skill を単体でインストールしても読めるように、それらの内容を複製したもの。各ファイルの冒頭に元のファイル名を記載している
- `references/` には Packaging Revision だけを加えている。リポジトリ内のパスへの参照と、リポジトリ管理者向けの記録先の指示を、Skill の中で完結する表現に置き換えた。方法・Status・Finding Type・値・Workflow の STEP は変えていない
- 仕様を改訂するときは、元の文書を修正してから `references/` を作り直し、Packaging Revision を当て直す
- この Skill は Workflow v1.1 の installable implementation であり、実行ごとに同じ結果を出す監査エンジンではない。同じ入力でも、Finding の数・まとめ方・Finding Type・Status は実行ごとに変わりうる
- コードや補助ツールを追加する場合のライセンスは Apache-2.0 を候補とする（最終確定は Human Review）
