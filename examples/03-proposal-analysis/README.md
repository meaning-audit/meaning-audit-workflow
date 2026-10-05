# Test 03: Proposal / Analysis Document

- Status: 未実施（監査対象は未選定）
- 想定 Document Class: Class C: Proposal / Analysis / Decision Document
- 想定 Audit Mode: 未定（元資料が入手できれば Mode A、できなければ Mode B）

## このテストケースの目的

このテストケースは、代表的な文書種類の見本を集めるためのものではありません。次の Meaning Transformation を観察するためのものです。

- Evidence から推奨までの推論で、どの Warrant が示され、どれが示されていないか
- 分析上の可能性が、判断・推奨として採用されるところ（Commitment）
- 推奨の強さが、根拠の状態に見合っているか

## 重点観点（Class C: Proposal / Analysis / Decision Document）

- Evidence
- Inference / Warrant
- Recommendation
- Commitment

## ディレクトリ

| ディレクトリ | 置くもの |
|---|---|
| [input/](input/) | 監査対象（Audit Object）と、あれば元資料（Source） |
| [audit/](audit/) | AI が出力した Meaning Audit Report |
| [review/](review/) | Human Review の記録 |

## 実行手順

1. 監査対象を選び、`input/` に置く（公開できないものは出典情報だけを `input/README.md` に書く）
2. 元資料があれば `input/` に置く
3. [../../prompts/minimum-audit-v1.0.md](../../prompts/minimum-audit-v1.0.md) を使って監査する
4. 出力を `audit/` に保存する
5. [../../workflow/human-review.md](../../workflow/human-review.md) に従ってレビューし、`review/` に保存する
6. [../../tests/test-log.md](../../tests/test-log.md) に記録する

## 監査対象の選定メモ

- 対象:（未定）
- 出典:（未定）
- 元資料の有無:（未定）
- 公開可否:（未定）
