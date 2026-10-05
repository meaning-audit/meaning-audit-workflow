# Audit Modes

v1.0 では 2 つの監査モードを使います。どちらのモードも同じ STEP 0〜8 を実行します。違いは、STEP 2（Evidence / Source Trace）で何を根拠として扱うかと、使う Status です。

## Mode A: Source-Grounded Audit

元資料または Evidence が利用可能な場合。

- Source と成果物を照合し、提示された Meaning が Source にどこまで支えられているかを判定する
- Status: `SUPPORTED` / `PARTIALLY SUPPORTED` / `UNSUPPORTED` / `UNKNOWN`
- `UNSUPPORTED` は「提供された Source では支えられていない」という意味で、それだけで「虚偽」を意味しない
- プロンプト: [../prompts/source-grounded-audit.md](../prompts/source-grounded-audit.md)

## Mode B: Artifact-Only Audit

最終成果物しか利用できない場合。

- 元資料への忠実性は判定しない
- 成果物の内部で、Claim、Meaning Shift、Inference、Framing、Traceability を見る
- Status: `TRACEABLE` / `PARTIALLY TRACEABLE` / `UNTRACEABLE` / `UNKNOWN`
- 外部 Evidence なしに「誤り」と断定してはならない
- 元資料と照合すべき主張は Source Verification Required に挙げる
- プロンプト: [../prompts/artifact-only-audit.md](../prompts/artifact-only-audit.md)

## モードの判定

| 状況 | Mode |
|---|---|
| Source が提供されている | Mode A |
| Source が提供されていない（none、空欄、名前や URL だけ） | Mode B |
| Source が一部だけ提供されている | Mode A。Source の無い Meaning Unit は `UNKNOWN` とし、Source Verification Required に記載 |

Mode が決まっていない場合は [../prompts/minimum-audit-v1.0.md](../prompts/minimum-audit-v1.0.md) を使います。このプロンプトはモードを自動判定し、元資料が無い場合は Source verification ができないことを明示して Mode B に切り替えます。

## Status の対応

Mode A と Mode B の Status は、同じ意味の言い換えではありません。

| Mode A | Mode B | 違い |
|---|---|---|
| SUPPORTED | TRACEABLE | A は Source が支えているか。B は成果物内で道筋が示されているか |
| PARTIALLY SUPPORTED | PARTIALLY TRACEABLE | |
| UNSUPPORTED | UNTRACEABLE | B では「根拠が示されていない」だけで、内容の正誤は言えない |
| UNKNOWN | UNKNOWN | |

1 つの Report の中で、両方の Status を混在させません。
