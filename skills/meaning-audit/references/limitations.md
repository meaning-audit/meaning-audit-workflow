<!-- Packaged from Meaning Audit Workflow v1.0 (canonical source: https://github.com/meaning-audit/meaning-audit-workflow, docs/limitations.md). Packaging revision: repository-specific paths and maintainer instructions were replaced so that this skill is self-contained. Method, Status, Finding Types, and Workflow steps are unchanged. -->

# Limitations

Meaning Audit Workflow v1.0 の既知の限界です。テストを通じて更新します。

## 方法としての限界

- Meaning Audit は Meaning Shift の所在を追跡するもので、成果物の内容が正しいかどうかを保証しない
- Mode B（Artifact-Only Audit）では、元資料への忠実性を判定できない。成果物内で Traceable であっても、内容が正しいとは限らない
- Mode A（Source-Grounded Audit）でも、判定は提供された Source の範囲に限られる。Source 自体の正確性は判定しない
- Finding Type は運用ラベルであり、すべての Meaning Shift を網羅する分類ではない

## AI 実行に伴う限界

- AI が図・画像・グラフ・レイアウトを正しく読めない場合がある。特に Class A では、Visual Claim の監査が不完全になり得る
- AI が自身の一般知識を判定に持ち込むことがある。この Skill では Evidence Boundary への記録を求めているが、完全には防げない
- 長い文書では、Meaning Unit の抽出漏れが起きやすい
- 同じ入力でも、実行ごと・モデルごとに Finding が変わり得る（v1.0 では再現性を検証していない）
- AI は UNKNOWN を推測で埋める傾向がある。Human Review で確認する

## v1.0 で扱わないもの

- スコアリング、等級付け、ランキング
- 自動 Rewrite、自動意思決定
- 複数文書間の横断的な監査
- Engine 実装、Knowledge Graph 化、SaaS 化

## 運用上の注意

- 監査対象・元資料に機密情報や個人情報が含まれる場合、AI サービスへの投入可否を事前に確認する
- 監査対象や Report を公開する場合は、著作権と利用許諾を確認する
