# Test 01-1 Human Review Record

- Test: Test 01-1: Presentation Artifact — Generation Provenance Unknown
- Report: [../audit/test-01-1-public.md](../audit/test-01-1-public.md)（公開版。原本は Private Evidence Layer）
- Date: 2026-10-06
- Reviewer: Human Reviewer（リポジトリ管理者）
- 記録作成: Claude Opus 5.5（Human の判断を記録したもの。AI は判断していない）

---

## 1. Human Review Decisions

### HR-01: Test 01-1 の位置づけ

- 判断: 監査対象はプレゼンテーション資料だが、AI 生成であることは確認できなかった。`AI-Generated Presentation` とは確定せず、Test 01-1 を **Test 01-1: Presentation Artifact — Generation Provenance Unknown** として扱う
- Generation Tool: `UNKNOWN`
- PFC-004（生成過程の来歴）はそのまま維持する
- 影響: Test 01（AI-Generated Presentation）の本来の目的は、生成過程の分かる資料を使う次回以降のテストで検証する

### HR-02: Public Repository Policy

- 判断: 今回の目的は第三者企業の公開評価ではなく、Meaning Audit Workflow v1.0 のフィールドテストである。実名入りの Report を公開リポジトリに push しない
- 次の二層構造にする

| 層 | 置き場所 | 内容 |
|---|---|---|
| Private Evidence Layer | ローカルのみ（git の管理対象外） | 元の PDF、実名入りの Audit Report、実名入りの Finding、Source の情報、ハッシュ値、ページの対応表、元の比較レビュー |
| Public Test Layer | GitHub | 匿名化した Audit Report・Finding、Failure Pattern、Post-Freeze Candidate、Test Log、Human Review の結果 |

匿名化の方針: 第三者を直接特定する固有名詞を、Company A、Service A、Group B、Client A〜C、Representative A〜D、Public Source 1〜3 に置き換える。ページ番号、Finding ID、数値、Status、情報状態は維持する。長い引用・特徴的な言い回しは、意味を変えない範囲で言い換える。

---

## 2. R-1〜R-9 の Human Review 状況

| # | 対象 | 状況 | Human Decision |
|---|---|---|---|
| R-1 | Test 01 の前提（AI 生成か） | HR-01 で判断済み | Provenance Unknown として扱う |
| R-2 | 公開の可否 | HR-02 で判断済み | 実名入りは非公開。匿名化版のみ公開 |
| R-3 | F-01 の読み方 | 未判断 | |
| R-4 | F-04 の判定 | 未判断 | |
| R-5 | F-07, F-12 の Visual Claim の解釈 | 未判断 | |
| R-6 | F-14, F-20, F-22, F-24 | 下の 4 で再確認を整理。判断は未了 | |
| R-7 | F-03, F-18 の Source との対応 | 未判断 | |
| R-8 | Run 01A を実行するか | 未判断 | |
| R-9 | Report の粒度（Finding 26 件、Human Review 17 項目） | 未判断（FP-006 として保持） | |

---

## 3. FP-005 の暫定判断

- 問い: 資料内の数値を検算することは、External Knowledge の導入に当たるか
- Human Review の暫定判断: **成果物内部に存在する数値のみを使った算術的検算は、External Knowledge の導入とはみなさない**
- 理由: 外部から新しい Evidence を加えているのではなく、Artifact 内部の整合性を検査しているため
- 扱い: Workflow v1.0 には反映しない。Workflow 改訂の候補として保持する（[../../../tests/failure-patterns.md](../../../tests/failure-patterns.md) の FP-005 に、この判断の記録先を追記した）
- 範囲の注意: この判断は「成果物内の数値のみを使った算術」に限られる。為替レートや制度の知識など、成果物の外の情報を使う検算は対象外

---

## 4. R-6 対象 Finding の再確認

Finding は削除・修正していません。各 Finding について、成果物から確認できる部分と推測の部分を分けて整理しました。Human Review Recommendation は AI による整理で、Human Decision ではありません。

### F-14

| 項目 | 内容 |
|---|---|
| Finding 原文（公開版） | 成約率の分母（小さな社数）は「興味を持つ顧客にだけ案内する」という施策の記述と並び、事前に絞られた母数である可能性がある。単価・期間・当事者は示されていない |
| Status / 情報状態 | UNTRACEABLE / INFERRED（母数の性質）・UNKNOWN（その他） |
| Inference の部分 | 「分母の社が事前に絞り込まれた母数である」という読み |
| Artifact から確認できる範囲 | p23 に分数で示された成約率があること。施策欄に「興味を持つ顧客にだけ案内する」趣旨の記述があること。単価・期間・当事者の記載が無いこと |
| 推測が始まる地点 | 施策欄の記述と成約率の分母を結びつけるところ。資料は分母の社がどう選ばれたかを述べていない |
| Human Review Recommendation | 「単価・期間・当事者が示されていない」部分は成果物から確認できる。母数の性質は INFERRED と明記されており、推測を事実として扱ってはいない。確認すべきは、推測部分を Finding の主な内容にしてよいか、Finding Type を SELECTION とするのが妥当か（「母数の選び方が示されていない」なら INFERENCE_GAP とも読める） |
| Human Decision | |

### F-20

| 項目 | 内容 |
|---|---|
| Finding 原文（公開版） | 非対応という制約を、助成金の利用と「不正受給のリスク」を結びつけることで利点として提示している。「即決しやすく利益に直結」の因果の根拠は示されていない |
| Status / 情報状態 | UNTRACEABLE / INFERRED |
| Inference の部分 | 「制約を利点として提示している」という Framing の判定と、読み手がそこから受け取る含意 |
| Artifact から確認できる範囲 | p31 の FAQ で、助成金非対応の説明の中に「審査の手間や不正受給のリスクを避け」という趣旨の記述があること。「即決しやすく利益に直結」の根拠が書かれていないこと |
| 推測が始まる地点 | 「不正受給のリスク」への言及が、助成金を使う選択肢を不利に見せる効果を持つ、という解釈 |
| Human Review Recommendation | 記述が存在することと、因果の根拠が無いことは KNOWN として扱える。「利点として Framing している」は作成者の意図ではなく表現の効果についての解釈であり、INFERRED の扱いは妥当。確認すべきは、この解釈を Finding として残すか、因果の根拠が無い部分（INFERENCE_GAP）だけに絞るか |
| Human Decision | |

### F-22

| 項目 | 内容 |
|---|---|
| Finding 原文（公開版） | p14 のレッスン名はツール・機能別が中心で、p1 のカテゴリも同様。「職種別・業務別」の構成は成果物の中では確認できない（p14 に業務別の講座が 1 件ある）。「高単価で提案できる」の根拠も無い |
| Status / 情報状態 | PARTIALLY TRACEABLE / INFERRED |
| Inference の部分 | p14 の 1 講座（16 レッスン）と p1 の画面から、カリキュラム全体の構成を推し量っている点 |
| Artifact から確認できる範囲 | p14 の 1 講座のレッスン名、p1 の画面に見えるカテゴリ、p32 の「職種別・業務別」の記述、「高単価」の根拠が無いこと |
| 推測が始まる地点 | 「○○本以上」とされるカリキュラムのうち、成果物に見えているのは一部だけであり、見えない部分の構成は分からない |
| Human Review Recommendation | 「成果物の中では確認できない」という Traceability の表現にとどまっており、主張が誤りだとは言っていない。ただし根拠は一部のサンプルに限られ、読み手が「職種別ではない」と受け取る恐れがある。確認すべきは、Status を UNKNOWN（見えている範囲では判定できない）とする方が適切か |
| Human Decision | |

### F-24

| 項目 | 内容 |
|---|---|
| Finding 原文（公開版） | 「一員」の具体的な関係、Company A との関係が示されていない。設立年月と事例・導入企業の声・実績数との時期の関係が示されていない。p14 の画面キャプチャ内の社名は p36 の社名と表記が異なる |
| Status / 情報状態 | PARTIALLY TRACEABLE / UNKNOWN（関係・時期）・CONFLICTING（社名表記） |
| Inference の部分 | 設立年月と実績の時期の関係を問題として取り上げること自体（実績がこの会社のものである、という前提を置いている） |
| Artifact から確認できる範囲 | p36 の設立年月、p34 の「グループの一員」の記述、p14 の画面キャプチャ内の社名表記が p36 と異なること |
| 推測が始まる地点 | 実績の主体と時期。前身事業、個人としての実績、グループ会社の実績、デモ環境の表示である可能性などは、成果物の外の情報であり判断できない |
| Human Review Recommendation | 3 つの別の所見（グループとの関係、時期の関係、社名表記）が 1 つの Finding に入っている。社名表記の違いは KNOWN だが、デモ環境やテスト用の表示である可能性もあり、意味は UNKNOWN。時期の関係は UNKNOWN として扱われており、断定はしていない。確認すべきは、1 つの Finding に複数の所見をまとめることの扱い（Workflow の論点として記録するか） |
| Human Decision | |

---

## 5. Public / Private の境界

Private Evidence Layer は、このリポジトリとは別の非公開の Evidence Vault（git 管理外）に保管しています。Test ごとに同じ構成を使います。

| Vault 内の場所 | 内容 |
|---|---|
| `test-01-1/source/` | 元の資料（第三者の著作物。ファイル名・内容は無変更） |
| `test-01-1/private-audit/` | AI が出力した Report の原本（実名入り・無編集） |
| `test-01-1/review/` | 匿名化する前の比較レビュー・Test 記録 |
| `test-01-1/metadata/` | manifest（SHA-256、ページ数、権利・公開の扱い、関連記録）、ページの対応表、匿名化の対応表 |

公開リポジトリにあるもの:

| ファイル | 内容 |
|---|---|
| [../audit/test-01-1-public.md](../audit/test-01-1-public.md) | 匿名化した Report |
| [mode-comparison.md](mode-comparison.md) | 匿名化した比較レビュー |
| この文書 | Human Review の記録 |

元の資料は、公開リポジトリにコピー・commit・push しません。`.gitignore` の `private/` は、ローカルで誤ってコミットするのを防ぐために残しています。
