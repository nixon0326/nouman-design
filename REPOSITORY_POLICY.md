# NouMan Repository Policy
## リポジトリ運用ルール — Single Source of Truth

> このドキュメントは NouMan 関連リポジトリの役割・保存場所・禁止事項を定める。
> ファイルの保存先で迷ったときは、必ずこのドキュメントを参照すること。

---

## 1. リポジトリ定義

### `nixon0326/nouman-os` — 思想・Research の本丸（非公開）

NouManの思想・Research・AI Team OS・Brand思想・派生ブランド構想を管理する。
**ソースコードは置かない。公開情報は置かない。**

```
nouman-os/
├── research/          ← Research 001〜（思想・仮説・構想）
│   └── Brand/         ← Brand思想・Design Archive・Design DNA
├── ai/                ← AI Team 設定（chatgpt / claude / gemini / manus）
├── product/           ← プロダクト定義・ページ構成・ロール
├── references/        ← 設計判断・色仕様・レビュー履歴
├── principles.md      ← 不変の原則
├── SKILL.md           ← AI Team OS エントリーポイント
└── README.md
```

---

### `nixon0326/nouman-ios` — アプリ実装（非公開）

iOS / Android / Expo アプリの実装コードのみを管理する。
**思想・Research・デザイン素材の正規保管場所としては使わない。**

```
nouman-ios/
├── src/               ← アプリ実装コード（正規）
├── ios/               ← iOS native
├── android/           ← Android
├── assets/brand/      ← アプリが直接参照するSVGアイコン原本
├── app.json / eas.json / package.json
└── README.md
```

---

### `nixon0326/nouman-design` — 公開デザインCDN（公開）

公開可能なデザイン素材・Creative Director System・Manus共有用CDNを管理する。
**非公開の思想・事業戦略・実装コードは置かない。**

```
nouman-design/
├── appstore/          ← App Store スクリーンショット
├── icon/ logo/ splash/ favicon/ social/  ← ブランド素材
├── brand/             ← ブランド憲法画像
├── creative/          ← Creative Director System一式
│   ├── README_CREATIVE.md   ← Manus への入口
│   ├── BRAND_CONSTITUTION.md
│   ├── CREATIVE_DIRECTOR_SYSTEM.md
│   ├── CREATIVE_DNA.md
│   ├── CREATIVE_REVIEW.md
│   ├── APPSTORE_GUIDELINE.md
│   └── LEARNING_LOG.md
├── brand-guide-public.md
├── index.md           ← CDN資産一覧
└── share-template.md  ← Manus共有テンプレート
```

---

## 2. 正規保存場所

| コンテンツ種別 | 正規リポジトリ | 正規パス |
|---|---|---|
| iOSアプリ実装コード | `nouman-ios` | `src/` |
| アプリ直需アセット（SVG等） | `nouman-ios` | `assets/brand/` |
| Research（思想・仮説・構想） | `nouman-os` | `research/NNN-*.md` |
| Brand思想ドキュメント | `nouman-os` | `research/Brand/` |
| 彩り / 派生ブランド構想 | `nouman-os` | `research/` |
| AI Team 設定 | `nouman-os` | `ai/` |
| プロダクト定義・ページ構成 | `nouman-os` | `product/` |
| 設計判断ログ | `nouman-os` | `references/` |
| 公開デザイン素材 | `nouman-design` | `appstore/` `icon/` `logo/` 等 |
| Creative Director System | `nouman-design` | `creative/` |
| Manus共有テンプレート | `nouman-design` | `share-template.md` |
| ブランド憲法（公開版） | `nouman-design` | `creative/BRAND_CONSTITUTION.md` |
| ブランド憲法画像（原本） | `nouman-design` | `brand/` |

---

## 3. 禁止事項

| 禁止 | 理由 |
|---|---|
| `nouman-ios` に思想・Researchを新規追加する | 実装リポジトリに思想が混入すると分散が再発する |
| `nouman-design` に非公開思想・事業戦略を置く | 公開CDNに内部情報が混入する |
| 同じファイルを複数リポジトリに重複保存する | 更新漏れ・バージョン分岐が必ず起きる |
| 一時コピーを正規ファイルとして扱う | `/tmp/` 等のローカルパスを本番参照先にしない |
| `git push` 前にリモートを確認しない | 誤ったリポジトリへのpushが起きる（過去に発生） |

---

## 4. 作業前チェック（必須）

ファイルを編集・コミット・プッシュする前に、必ず以下を確認すること。

```bash
pwd                        # 現在のディレクトリ
git remote -v              # どのリポジトリに接続しているか
git branch --show-current  # 現在のブランチ
git status                 # 変更・未追跡ファイルの確認
```

**特に注意:** シェルのカレントディレクトリは前のコマンドから引き継がれる。
意図したリポジトリで作業しているか、`git remote -v` で必ず確認する。

---

## 5. 迷ったときの判断基準

```
このファイルは公開してよいか？
    YES → nouman-design

このファイルはアプリの動作に必要か？
    YES → nouman-ios

思想・Research・AI判断基準・ブランド思想・派生ブランド構想か？
    YES → nouman-os
```

---

## 6. Research 番号ルール

- 番号は `nouman-os/research/` を正として連番管理する
- 新規 Research は `nouman-os/research/NNN-*.md` に直接追加する
- 現在の最終番号: **025**（次は 026）
- 欠番（007〜017は別セッションで作成済み、018〜025は今回統合）

---

## 7. このポリシーの更新ルール

- 保存場所の変更・リポジトリ追加が生じた場合は、**このファイルを先に更新してからファイルを移動する**
- 3リポジトリすべてのルートに同一ファイルを配置する
- バージョン管理はしない（常に最新版が正）

---

*NouMan Repository Policy v1.0*
*作成: 2026-07-10*
*適用リポジトリ: nouman-os / nouman-ios / nouman-design*
