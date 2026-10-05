# skills/

Meaning Audit Workflow v1.0 を Claude Code の Agent Skill として使うためのディレクトリです。

## meaning-audit

| ファイル | 内容 |
|---|---|
| [meaning-audit/SKILL.md](meaning-audit/SKILL.md) | 実行仕様（モード判定、クラス判定、Evidence Boundary、Meaning Unit、Meaning Trace、Finding Ledger、Unknown Policy、Human Review、出力形式） |
| [meaning-audit/references/workflow.md](meaning-audit/references/workflow.md) | `workflow/meaning-audit-workflow-v1.0.md` の内容に、`docs/document-classes.md`、`workflow/human-review.md`、`docs/audit-modes.md` を付録として加えたもの |
| [meaning-audit/references/output-format.md](meaning-audit/references/output-format.md) | `workflow/output-format.md` の内容 |
| [meaning-audit/references/finding-types.md](meaning-audit/references/finding-types.md) | `workflow/finding-types.md` の内容 |
| [meaning-audit/references/limitations.md](meaning-audit/references/limitations.md) | `docs/limitations.md` の内容 |

インストール方法はリポジトリの [README.md](../README.md) の「Install as a Claude Code Skill」を参照してください。

## 方針

- Skill は `workflow/`・`prompts/`・`docs/` の内容を実行しやすくする包装であり、新しい手順・概念を追加しない
- 仕様の正は `workflow/` と `docs/`。`references/` は、Skill を単体でインストールしても読めるように、それらの内容をリンクだけ調整して複製したもの。各ファイルの冒頭に元のファイル名を記載している
- Workflow を改訂するときは、元のファイルを修正してから `references/` を作り直す
- コードや補助ツールを追加する場合のライセンスは Apache-2.0 を候補とする（最終確定は Human Review）
