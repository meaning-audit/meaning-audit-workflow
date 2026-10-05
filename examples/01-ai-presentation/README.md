# Test 01: AI-Generated Presentation

- Status: 未実施（監査対象は未選定）
- 想定 Document Class: Class A: Presentation / Visualization
- 想定 Audit Mode: 未定（元資料が入手できれば Mode A、できなければ Mode B）

## このテストケースの目的

このテストケースは、代表的な文書種類の見本を集めるためのものではありません。次の Meaning Transformation を観察するためのものです。

- 元資料からスライドへの選択・圧縮で、限定条件や不確実性がどう扱われるか
- 図・グラフ・配置が、本文や元資料以上の主張をしていないか
- 要約の過程で、意味が強められていないか（Meaning amplification）

## 重点観点（Class A: Presentation / Visualization）

- Selection / Compression
- Framing
- Visualization / Visual Claim
- Causal implication
- Meaning amplification

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
