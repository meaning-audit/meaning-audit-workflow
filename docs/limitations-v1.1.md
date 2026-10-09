# Limitations

- Name: Limitations
- Version: v1.1
- Status: RELEASED（v1.1、2026-10-09）
- Basis: Limitations v1.0 に、Human-approved Skill / Runtime v1.1 の追加（V-15、Governance note）を加えたもの

Meaning Audit Workflow v1.1 の既知の限界です。テストを通じて更新します。

## 方法としての限界

- Meaning Audit は Meaning Shift の所在を追跡するもので、成果物の内容が正しいかどうかを保証しない
- Mode B（Artifact-Only Audit）では、元資料への忠実性を判定できない。成果物内で Traceable であっても、内容が正しいとは限らない
- Mode A（Source-Grounded Audit）でも、判定は提供された Source の範囲に限られる。Source 自体の正確性は判定しない
- Finding Type は運用ラベルであり、すべての Meaning Shift を網羅する分類ではない

## AI 実行に伴う限界

- AI が図・画像・グラフ・レイアウトを正しく読めない場合がある。特に Class A では、Visual Claim の監査が不完全になり得る
- 監査に使う表現（抽出テキスト、描画されたページ、画像など）によって、読み取れる意味が変わり得る。テキストがあっても、描画された表現と同じとは限らない
- AI が作った監査出力、比較出力、派生した要約、件数、その他の二次的な記録は、それ自体が誤りを含み得て、Human Review を要し得る。Runtime の検証はこれを減らすが、Human Review を置き換えない
- AI が自身の一般知識を判定に持ち込むことがある。プロンプトでは Evidence Boundary への記録を求めているが、完全には防げない
- 長い文書では、Meaning Unit の抽出漏れが起きやすい
- 同じ入力でも、実行ごと・モデルごとに Finding が変わり得る（v1.0 では再現性を検証していない）
- AI は UNKNOWN を推測で埋める傾向がある。Human Review で確認する

## v1.1 で扱わないもの

- スコアリング、等級付け、ランキング
- 自動 Rewrite、自動意思決定
- 複数文書間の横断的な監査
- Engine 実装、Knowledge Graph 化、SaaS 化

## 運用上の注意

- 監査対象・元資料に機密情報や個人情報が含まれる場合、AI サービスへの投入可否を事前に確認する
- 公開リポジトリに監査対象を置く場合は、著作権と利用許諾を確認する
