# skills/

将来、Meaning Audit Workflow を Claude Code の Skill などとしてパッケージ化するための置き場です。

## v1.0 の状態

v1.0 では Skill を実装していません。監査は [../prompts/](../prompts/) のプロンプトを AI に直接投入して実行します。

## 方針

- Skill 化は、`examples/` の 3 テストケースで Workflow とプロンプトが安定してから検討する
- Skill は `prompts/` と `workflow/` の内容を実行しやすくする包装であり、新しい手順・概念を追加しない
- コードや補助ツールを追加する場合のライセンスは Apache-2.0 を候補とする（最終確定は Human Review）
