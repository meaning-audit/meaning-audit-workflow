# Test Log

Meaning Audit Workflow v1.0 のテスト実行記録です。1 回の監査実行につき 1 エントリを追加します。

テストケースは代表的な文書種類を集めたものではなく、異なる Meaning Transformation を観察するためのものです。

## テストケース一覧

| Test | 対象 | 想定 Class | 想定 Mode | 状態 |
|---|---|---|---|---|
| 01 | AI-Generated Presentation | A | 未定（元資料の有無による） | 未実施 |
| 02 | Published Article | B | 未定 | 未実施 |
| 03 | Proposal / Analysis Document | C | 未定 | 未実施 |

## 記録テンプレート

```markdown
### <YYYY-MM-DD> Test <番号>-<実行番号>

- 対象: <examples/ のディレクトリ名>
- Prompt: <ファイル名 / バージョン>
- Model: <モデル名・環境（Claude Code / ChatGPT など）>
- Audit Mode（AI の判定）:
- Document Class（AI の判定）:
- Report: <audit/ 内のファイル名>
- Human Review: <review/ 内のファイル名 / 未実施>

#### 観察

- Workflow どおりに動いたこと:
- 動かなかったこと（→ failure-patterns.md）:
- 新しい概念が必要に見えたこと（→ post-freeze-candidates.md）:

#### Workflow / Prompt の修正

- 修正した / 修正しない（理由）:
```

## 実行記録

（まだ実行記録はありません）
