# SDS 履修ガイドブック

一橋大学ソーシャル・データサイエンス学部（SDS）の非公式履修ガイドブックの編集用リポジトリです。

**サイトURL**: https://sds-info.github.io/SDSwiki/

## サイト概要

| 項目 | 内容 |
|------|------|
| 対象年度 | 2026年度 |
| 技術構成 | 静的 HTML/CSS/JS（ビルド不要） |
| ホスティング | GitHub Pages（`docs/` フォルダ） |
| 外部依存 | Google Fonts（Noto Sans JP）のみ |

## 公開ページ

| ページ | ファイル | 主な機能 |
|--------|----------|----------|
| トップページ | `docs/index.html` | サイト案内、各ページへのリンク |
| 科目一覧 | `docs/courses.html` | キーワード検索、カテゴリ／科目区分フィルタ、科目カード、詳細モーダル（成績分布グラフ付き） |
| 履修の基本情報 | `docs/rishu.html` | 学年暦・時間割・単位計算・GPA 等（`guide.md` をレンダリング） |

### 予定ページ（未実装）

- 進学・卒業要件
- 学内手続きガイド
- キャリア・進路情報
- ゼミ情報（`ゼミ情報.csv` にデータ収集済み）

## データソース

| ファイル | 内容 | 規模 |
|----------|------|------|
| `courses.csv` | 科目データ（名称、日時、教員、評価基準、難易度、成績分布） | 71科目・14カラム |
| `guide.md` | 履修ガイド本文（学年暦、授業形態、単位計算、GPA） | 約480行 |
| `ゼミ情報.csv` | ゼミ情報（活動日時、進学率、設備、学生構成など） | 18教員分 |

`docs/courses.csv` と `docs/guide.md` はルートへのシンボリックリンクです。**編集はルートのファイルを直接編集してください。**

## ファイル構成

```
/
├── courses.csv              ← 科目データ（編集はここ）
├── guide.md                 ← 履修ガイド本文（編集はここ）
├── ゼミ情報.csv              ← ゼミ情報データ
├── docs/                    ← GitHub Pages サイト
│   ├── index.html               トップページ
│   ├── courses.html             科目一覧ページ
│   ├── rishu.html               履修の基本情報ページ
│   ├── app.js                   共通スクリプト（CSV読み込み・描画・フィルタ・モーダル・MDパーサ）
│   ├── style.css                共通スタイル（レスポンシブ対応）
│   ├── images/                  画像素材
│   ├── courses.csv              → ../courses.csv（シンボリックリンク）
│   ├── guide.md                 → ../guide.md（シンボリックリンク）
│   └── .nojekyll                Jekyll 無効化
├── raw/                     ← 元データ・参考資料
│   ├── courses_2026.csv         2026年度の科目データ（下書き）
│   └── grades_2024.csv          2024年度の成績分布
├── 公式情報/                 ← 公式参考ドキュメント
├── changelog.md             ← 変更履歴（2025→2026年度）
├── TASKS.md                 ← タスク管理
├── SITE_STATUS.md           ← サイト現状レポート
└── README.md
```

## 編集・デプロイ

```
1. courses.csv / guide.md をルートで編集
2. git commit & push
3. GitHub Pages に自動反映（ビルド不要）
```

### データの流れ

```
courses.csv ──symlink──→ docs/courses.csv ──fetch──→ app.js ──render──→ 科目カード + モーダル
guide.md    ──symlink──→ docs/guide.md    ──fetch──→ app.js ──parse───→ 履修ガイドセクション
```

## 主な機能

- **科目検索**: キーワード・カテゴリ（SDS / 社会科学 / DS / PACE）・科目区分で絞り込み
- **科目カード**: カテゴリバッジ、日時、教員、難易度（5段階）、成績ミニバー
- **詳細モーダル**: 評価基準、成績分布グラフ（A+/A/B/C/F 横棒）
- **Markdown レンダリング**: `guide.md` をクライアント側で HTML 変換＋サイドバーナビ
- **レスポンシブ**: モバイル対応（768px ブレークポイント）、ハンバーガーメニュー

## 関連ドキュメント

- [changelog.md](changelog.md) — 2025→2026年度の変更履歴（時間割・教員・成績分布の差分）
- [TASKS.md](TASKS.md) — タスク管理
- [SITE_STATUS.md](SITE_STATUS.md) — サイト現状の詳細レポート
