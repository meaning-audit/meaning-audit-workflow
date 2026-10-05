# Test 02: Published Article

- Status: 未実施（監査対象は未選定）
- 想定 Document Class: Class B: Article / Report / Explanatory Document
- 想定 Audit Mode: 未定（元資料が入手できれば Mode A、できなければ Mode B）

## このテストケースの目的

このテストケースは、代表的な文書種類の見本を集めるためのものではありません。次の Meaning Transformation を観察するためのものです。

- 記事の中で、Evidence の記述と書き手の解釈がどう区別（または混合）されているか
- 引用が元の文脈から切り離されて、別の意味を担っていないか
- タイトル・見出しと本文の主張の強さが一致しているか

## 重点観点（Class B: Article / Report / Explanatory Document）

- Evidence と Interpretation の境界
- Narrative / Editorial framing
- Quote handling
- Context preservation
- Title-body relationship

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
