<!-- Packaged from Meaning Audit v1.1 canonical assembly (runtime/meaning-audit-runtime-validation-v1.1.md). Packaging revision: repository-specific paths and maintainer instructions were replaced so that this skill is self-contained. Method, Status, Finding Types, values, and Workflow steps are unchanged. -->

# Meaning Audit Runtime Validation v1.1

- Name: Meaning Audit Runtime Validation（Runtime Record を含む）
- Version: v1.1
- Status: RELEASED（v1.1、2026-10-09）
- Basis: Human-approved Skill / Runtime v1.1（SQ-1〜SQ-7）。Canonical v1.1 Candidate Backlog の V-13、V-14、V-15、V-18、N-2、Governance note
- 対象：Meaning Audit Workflow v1.1、Output Contract v1.1、Minimum Audit Prompt v1.1 を Skill / Runtime で実行するときの、実行と検証の規則

この文書は execution layer の規則です。新しい監査理論、Status、Finding Type、情報状態、Workflow の STEP、taxonomy、Human の判断規則を加えません。

**Runtime の検証は Meaning Audit の分類ではありません。** ERROR／WARNING／INFO、PASS／PASS WITH WARNING／FAIL は Runtime だけの語であり、Report の分類の語彙（Finding Type、Status、情報状態、Human Decision）に入れません。

**検証は監査の意味の正しさを証明しません。** 件数・ID・語彙が整っていることは、Finding の判断、Status、情報状態が正しいことを意味しません。検証は Human Review を置き換えません。AI が作った監査出力、比較出力、派生した要約、件数、その他の二次的な記録は、それ自体が誤りを含みえて、Human Review を要しうります（Governance note）。

---

## 1. Prompt の識別

| 実行の経路 | Report ヘッダーの Prompt 欄 |
|---|---|
| Minimum Audit Prompt v1.1 を直接使う | `minimum-audit-v1.1`（Prompt の本文が示す値） |
| Skill（meaning-audit）から実行する | `skill: meaning-audit (minimum-audit-v1.1)` |

Skill は Prompt v1.1 の本文をそのまま実行の指示として使い、Report ヘッダーの Prompt 欄だけを上の値で記入します。Prompt のファイルは 1 つで、本文は変えません。Prompt 欄に実行環境の情報を入れません。Skill・Runtime の版は Runtime Record に書きます。

## 2. 表現と Visual（V-15）

監査に使う表現（rendered PDF のページ、スライド画像、ページのスクリーンショット、抽出テキスト、OCR 風の転記、構造化データ、変換された形式、元の文書のテキストなど）によって、読める意味が変わりうる。

- テキストが存在することを、Visual の確認が不要な理由にしない。意味が提示（レイアウト、色、強調、大きさ、順序、空間の関係、切れ、視覚の階層）に依存しうる場合は、実行環境で可能な範囲で、描画された表現を直接確認する
- 画像が存在することを、OCR が必要な理由にしない。OCR を義務にしない。信頼できるテキスト層・抽出表現があれば使う
- 描画された表現と抽出された表現を、同じと仮定しない
- 純粋にテキストの判断で、Visual の提示が関係しない場合は、Visual の確認を求めない
- 確実に読めないテキストを推測で復元しない。読めないことを Limitations に書く
- 直接の文書の確認で足りる場合に、スクリーンショットを求めない。特定のツールを指定しない

## 3. 範囲の記録（V-18、N-2）

次のどれか 1 つ以上に当たるとき、実際に調べた表現と範囲（ページ、ファイル、画像）を記録する。

1. Visual の主張が関係する
2. Artifact の一部だけを調べた
3. Run の比較が、調べた範囲に依存する
4. 表現・範囲の違いが解釈に影響しうる

- どれにも当たらなければ、詳しい範囲の記録は要らない。網羅的なページの記録をすべての監査の義務にしない
- 表現・範囲は自由記述で書く。Canonical な表現の taxonomy は無い
- 範囲が一部の場合は、網羅的に調べたと読める書き方をしない
- 主な置き場所は Runtime Record。一部の範囲が監査を実質的に限定する場合は Report §14 Limitations にも書き、結果に影響しうる場合は Report §13 Human Review Required にも挙げる

## 4. Human Review への escalation

Prompt と Output Contract が既に認める場合に、Human Review Required に挙げる（例：Status を 1 つに決められない、materiality が不明確、`CONFLICTING` が結果に実質的に影響する、粒度が分類を変える、表現の曖昧さが監査に実質的に影響する）。Skill / Runtime は Human Decision を書かない。

---

## 5. 検証の段階

| 段階 | 意味 | 出力への影響 |
|---|---|---|
| ERROR | 構造の違反、または Output Contract の違反で、その出力を有効な v1.1 Report として扱えないもの | 未解決の ERROR が残る限り、検証済みの最終 Report として扱わない（Runtime §10 未解決の ERROR） |
| WARNING | Report を出してよいが、確認・注意が要る状態 | 最終の出力を自動では止めない |
| INFO | 実行の記録、または止めない範囲の情報 | 止めない |

## 6. 全体の検証結果

| 値 | 条件 |
|---|---|
| PASS | 未解決の ERROR も WARNING も無い |
| PASS WITH WARNING | 未解決の ERROR は無いが、WARNING が 1 つ以上残る |
| FAIL | 未解決の ERROR が残る |

## 7. 欄ごとの Canonical 値（検証用）

検証は欄を見て行う。句読点・記号で一律に分けない：`Evidence / Source`、`Inference / Warrant`、`Context / Pragmatics` の「/」は 1 つの Canonical ラベルの一部で、複合値ではない。自由記述の欄（Content、Evidence Note、Annotation、Stage Path、部分のラベル、Location の具体的な値、Meaning Unit の内容、Meaning Trace の記述など）は列挙値として検証しない。

| 欄 | 許す値 |
|---|---|
| Mode | Mode A: Source-Grounded Audit／Mode B: Artifact-Only Audit |
| Document Class | A／B／C のうち 1 つ |
| Primary Stage（Report §7、Report §10.1） | Evidence / Source、Interpretation、Inference / Warrant、Context / Pragmatics、Commitment のうち 1 つ |
| Finding Type | SELECTION、COMPRESSION、EVIDENCE_INTERPRETATION_BLUR、QUOTE_HANDLING、INFERENCE_GAP、CAUSAL_IMPLICATION、FRAMING、VISUAL_CLAIM、NARRATIVE、TITLE_BODY_GAP、CONTEXT_LOSS、AMPLIFICATION、COMMITMENT_ESCALATION、OTHER のうち 1 つ |
| Status（Report §9 の Status 行、Report §10.1） | Mode A：SUPPORTED、PARTIALLY SUPPORTED、UNSUPPORTED、UNKNOWN ／ Mode B：TRACEABLE、PARTIALLY TRACEABLE、UNTRACEABLE、UNKNOWN（Report §2 の Mode に対応する方だけ） |
| 情報状態（要素・部分ごと） | KNOWN、INFERRED、UNKNOWN、CONFLICTING のうち 1 つ |
| 親の要素 | Evidence / Source、Interpretation、Inference / Warrant、Context / Pragmatics、Commitment |
| Primary Claim Type（任意） | 事実、解釈、推論、推奨、視覚的主張、引用 のうち 1 つ（日本語のまま） |
| Source Set Status（任意） | COMPLETE、PARTIALLY KNOWN、UNKNOWN、NOT APPLICABLE |
| Generation Tool、Post-generation Human Editing（任意） | 既知の値（自由記述）、UNKNOWN、NOT APPLICABLE |
| Finding の Location | 具体的な位置（自由記述）、UNKNOWN、NOT APPLICABLE |
| Human Decision | 空欄（AI は書かない） |

## 8. 検証規則

「修正」の列：**機械的修正可**＝意味に関わらず一義的に決まる修正だけ。**戻す**＝監査の判断のステップに戻して生成し直すか、Human Review へ。

| ID | 規則 | 段階 | 修正 |
|---|---|---|---|
| VR-01 | ヘッダーに Workflow version、Output Contract version: v1.1、Prompt、Auditor、Date、Review status がある。Prompt 欄は Runtime §1 の値 | ERROR | 欠けた版の値・Prompt 欄の値は機械的修正可。Auditor・Date が分からなければ UNKNOWN（推測しない） |
| VR-02 | Report §1〜§14 がすべて、順序どおりにある。内容の無いセクションは「該当なし」 | ERROR | 戻す。順序の入れ替えだけなら機械的修正可 |
| VR-03 | 任意の欄（Annotation、Stage Path、Primary Claim Type、Meaning Unit の Location、Audit Object Metadata）が無いことを違反にしない | 段階なし（誤検出を防ぐ確認） | — |
| VR-04 | MU ID が Report の中で一意。枝番なし | ERROR | 戻す。書式の揺れ（`mu-3` → `MU-03`）で対応が一義的なら機械的修正可 |
| VR-05 | Finding ID が一意。枝番なし | ERROR | 戻す。`F1` → `F-01` は一義的なら機械的修正可 |
| VR-06 | 各 Finding が MU ID を 1 つ以上参照し、参照先が Report §8 にある | ERROR | 戻す |
| VR-07 | KS、HR、SV、U が参照する Finding ID・MU ID が存在する | ERROR | 戻す |
| VR-08 | Finding Summary の各行に Finding ID、MU ID、Location、Primary Stage、Finding Type、Status がある | ERROR | 戻す |
| VR-09 | 各 Finding Detail に Finding ID、Content、Information State by Element（1 要素以上）、Evidence Note がある | ERROR | 戻す |
| VR-10 | Canonical 欄の値が Runtime §7 の値だけ | ERROR | 大文字・小文字・空白だけの揺れで値が一義的なら機械的修正可。それ以外は戻す |
| VR-11 | 複合値が無い（欄の中の複数の値、括弧・注記付きの値、疑問符） | ERROR | 戻す。どの値を残すかを自動で選ばない |
| VR-12 | Claim Type と Primary Stage の機械的な写しの疑い（「解釈」と Interpretation、「推論」と Inference / Warrant の組で、Stage の独立した根拠が Trace・Content・Evidence Note に見当たらない）。組み合わせが同じこと自体は違反にしない。値が異なることを求めない | WARNING | 戻して確かめ直す。自動で値を変えない |
| VR-13 | Status が Report §2 の Mode の語彙だけ | ERROR | 戻す。一方の Mode の語彙を他方に自動で置き換えない |
| VR-14 | 情報状態が要素・部分ごとに 1 つ。Finding 単位の集約した情報状態が無い | ERROR | 戻す |
| VR-15 | 親の要素のラベルが Canonical の 5 つ。部分のラベルは自由記述として受け入れる | ERROR | 空白・大文字小文字だけの揺れ（`Evidence/Source` → `Evidence / Source`）は機械的修正可。それ以外は戻す |
| VR-16 | Meaning Trace に情報状態が無い | ERROR | 戻す |
| VR-17 | Meaning Trace の Stage の行に単独の `UNKNOWN` が無い。Status 行の Status 値 `UNKNOWN` と、「Evidence Boundary の中で確立できない」などの自由記述は許す | ERROR | 戻す |
| VR-18 | Primary Claim Type がある場合、日本語の 6 値のどれか 1 つ。訳した値・英語の対応語・併記・コードが無い | ERROR | 戻す。英語の値から日本語の値への変換は自動で行わない |
| VR-19 | `UNKNOWN` の意味を欄で判断する（Location・Audit Object・Metadata の UNKNOWN、情報状態の UNKNOWN、Status の UNKNOWN は別）。語の一致だけで数えたり移したりしない | 段階なし（検証の前提） | — |
| VR-20 | Critical Unknowns に、要素ごとの UNKNOWN が機械的に写されているように見える | WARNING | 戻して確かめ直す |
| VR-21 | Human Decision 欄が空欄 | ERROR | AI が書いた値を空欄に戻すのは機械的修正可。修正を Validation result に残す |
| VR-22a | 本文（Overall Finding、Limitations など）で述べた件数と、実際の数（Finding、MU、KS、表の行・項目）の不一致 | WARNING | 正しい数が一義的な場合だけ、本文の数を実数に合わせる機械的修正可（修正後は INFO として記録） |
| VR-22b | 連番の飛び（例：F-07 の次が F-09） | WARNING | 振り直さない（参照に影響しうる）。重複は VR-04・VR-05 |
| VR-22c | KS の 3〜7 件の目安 | 段階なし（検証しない） | — |
| VR-23 | Mode B の Report で、成果物の主張を「誤り」「虚偽」「不正確」と断定していない（語の一致ではなく、断定しているかで判断する） | ERROR | 戻す |
| VR-24 | 点数・等級・ランキング・修正案が無い | ERROR | 戻す |
| VR-25 | Visual の範囲が一部なのに、網羅的に確認したと読める記述 | WARNING | 戻して記述を直す |
| VR-26 | 表現の食い違いの可能性（抽出テキストと描画された表現が、意味に関わる点で異なりうるのに、一方だけで判断している） | WARNING | 戻して確かめ直す |
| VR-27 | Runtime §3 の条件に当たる場合に、調べた表現・範囲が Runtime Record に記録されている | INFO（記録）／ 記録が無い場合は WARNING | 戻して記録する |

件数の検証（VR-22）は機械的な整合だけで、一般的な meta-audit に広げない。件数が正しいことを意味の正しさとして扱わない。

## 9. 自動修正の境界

| 区分 | 内容 |
|---|---|
| 機械的修正可 | 空白、明らかな Markdown の書式、意図する ID が一義的な場合の ID の書式（`F1` → `F-01`）、値が一義的な場合の大文字・小文字の正規化、機械的に確かめられる本文中の件数の修正、ヘッダーの版の値・Prompt 欄の値、AI が書いた Human Decision を空欄に戻すこと |
| 行わない | 参照に影響しうる連番の全体の振り直し |
| 自動修正しない（意味の判断） | Status、Finding Type、情報状態、Primary Stage、Finding の境界、MU の境界、materiality、Mode の語彙の対応付け、複合の分類値のどれを残すか、意味の解釈が要る英語 → 日本語の Claim Type の変換 |

意味の修正が必要な場合は、監査の判断のステップに戻すか Human Review へ。機械的修正を行った場合は Runtime Record の Validation result に残す。

## 10. 未解決の ERROR

- 未解決の ERROR が残る Report を、検証済みの最終 Report として扱わない。出力全体は止めない
- 安全に直せない ERROR が残った場合は、有用であれば次の形で出す：
  1. Report の前に `VALIDATION FAILED — REPORT DRAFT` と示す（Report の外。Report の欄・Review status は変えない）
  2. Report の draft
  3. Runtime Record：Validation result `FAIL`、未解決の ERROR の一覧、影響するセクション・欄、必要な再生成または Human Review
- この Report を validated final v1.1 output として示さない
- WARNING は最終の出力を自動では止めない。INFO は止めない
- これは Runtime の有効性の規則であり、Meaning Audit の Status ではない

---

## 11. Runtime Record

Runtime Record は、監査がどう実行されたか（実行の来歴と検証）を記録する。Report は Meaning Audit の結果を記録する。両者を厳密に分ける。

- Runtime Record を Report のセクションに加えない（Report §15 などを作らない）
- Audit Object Metadata（監査対象と生成の文脈）と統合しない
- 実行の条件またはユーザーの依頼で保存が必要な場合を除き、自動で永続化しない

| 欄 | 区分 | 内容 |
|---|---|---|
| Skill version | 常に記録 | 例：meaning-audit v1.1 |
| Prompt version | 常に記録 | 例：Minimum Audit Prompt v1.1 |
| Workflow version | 常に記録 | Meaning Audit Workflow v1.1 |
| Output Contract version | 常に記録 | v1.1 |
| Mode | 常に記録 | Report §2 と同じ値 |
| Validation result | 常に記録 | PASS／PASS WITH WARNING／FAIL。残った WARNING・ERROR の一覧、機械的修正の内容 |
| Representation inspected | 関係する場合（Runtime §3） | 実際に調べた表現の層（自由記述） |
| Coverage note | 関係する場合（Runtime §3） | 範囲の注記（自由記述） |
| Pages / files inspected | 関係する場合（Runtime §3） | 調べたページ・ファイル・画像（自由記述） |
| Visual coverage note | 関係する場合（Runtime §3） | Visual の範囲が一部であることなど |
| Experimental provenance | 明示的な依頼・Field Test の場合 | モデルの版、OS、CLI の版、実行環境、Renderer の版など。通常の監査では求めない |

例（中立的な placeholder）：

```text
Runtime Record
- Skill version: meaning-audit v1.1
- Prompt version: Minimum Audit Prompt v1.1
- Workflow version: Meaning Audit Workflow v1.1
- Output Contract version: v1.1
- Mode: Mode A: Source-Grounded Audit
- Validation result: PASS WITH WARNING
  - WARNING VR-25: <partial visual coverage wording>
  - mechanical corrections: <F1 → F-01>
- Representation inspected: <rendered PDF pages; extracted text>
- Pages / files inspected: <pages 1–8 of 20>
- Visual coverage note: <partial>
```
