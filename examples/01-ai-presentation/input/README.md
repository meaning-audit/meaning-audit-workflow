# input/

監査対象（Audit Object）と元資料（Source）を置きます。

| ファイル | 内容 |
|---|---|
| （配置せず） | 下記の理由により、監査対象ファイルはリポジトリに置いていない |

- 監査対象と元資料は、ファイル名で区別してください（例: `object-*.md`, `source-*.pdf`）
- 著作権・機密性の理由で公開できない資料は置かず、このファイルに出典情報（名称、URL、取得日）だけを記録してください
- 元資料が無い場合は、その旨をこのファイルに記録してください（Mode B で監査します）

---

## Test 01-1 の監査対象（公開版）

| 項目 | 内容 |
|---|---|
| 種類 | 第三者企業（Company A）のサービス紹介資料（プレゼンテーション） |
| 形式 | PDF、36 ページ、16:9 |
| 入手経路 | Human Reviewer から提供 |
| AI 生成か | UNKNOWN（Generation Provenance Unknown。HR-01） |
| リポジトリへの配置 | しない。第三者の著作物であり、公開リポジトリでは第三者の公開評価を避ける（HR-02） |

資料名、発行元、ハッシュ値、ページの対応表は Private Evidence Layer に保管しています（[../review/test-01-1-human-review.md](../review/test-01-1-human-review.md) の 5）。

## 監査への投入形式

- ページ画像: PDF を 110 dpi の PNG に変換（36 枚）
- テキスト層: PDF から抽出。テキストがあるのは一部のページのみで、多くのページは画像だけ
- 変換したファイルはリポジトリに含めていない

## Source（元資料）

なし。資料内で言及されている外部資料（Public Source 1〜3）の中身は提供されていない。このため Run 01A（Source-Grounded Audit）は実行していない。

---

## Test 01-2 の監査対象と Source

リポジトリにはいずれのファイルも置いていません。公開方針は PUBLIC SUMMARY ONLY で、監査対象と Source は Private Evidence Layer に保管しています。

| 項目 | 内容 |
|---|---|
| 監査対象 | NotebookLM で生成されたプレゼンテーション資料（Generation Tool: NotebookLM、Post-generation Human Editing: NONE。いずれも Human の申告） |
| Human-directed Focus | あり（Human 由来の編集意図） |
| Source Set | PARTIALLY KNOWN。公的機関が公開している資料 2 点が既知。生成時にはそれ以外の Web Source も使われていたが、特定できていない |
| リポジトリへの配置 | しない（監査対象・Source とも） |
