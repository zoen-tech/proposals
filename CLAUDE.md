# zoen-tech-proposals リポジトリ

## Why（目的）
対外共有するHTMLドキュメント（クライアント向け提案書＋取引先向け資料）を格納し、GitHub Pagesで公開するリポジトリ（**publicリポ**、GitHub リポ名は `zoen-tech/proposals`）。URL共有だけで相手が閲覧できる。**public-safe（第三者に読まれても致命傷にならない内容）なドキュメントのみ**を置く。

## Structure（構成）
```
assets/            ← 共通アセット（ロゴ等）。各案件から ../assets/ で参照
<クライアント名>/   ← 提案書の案件ごとのフォルダ（例: marubashi-ladies/）。英語名kebab-case
├── index.html     ← パスワード入力画面（本体ではない）
└── content.html   ← 提案書本文
partners/<ランダム12文字>/  ← 取引先向けの短命な商談資料（価格相談等）。パスに相手名を入れない
└── index.html
```
- `index.html` のパスワードは**簡易的な導線制御であってアクセス制御ではない**（`content.html` は直リンクで開ける。パスワードハッシュも `index.html` 内にある）

## 対外共有ドキュメントの機密3区分（2026-07-18決定）
どこに置くかは内容の機密度で決める。詳細な背景 → `repo_zoen-tech/docs/decisions/2026-07-18-external-docs-hosting-rules.md`

| 区分 | 内容 | 置き場 |
|------|------|--------|
| Tier A | 第三者に読まれても問題ない提案書・説明資料・匿名化済み資料 | 本リポ（恒久掲載可） |
| Tier B | 商談用の短命資料。**相手自身が既に知る情報＋匿名化した相場水準のみ**で構成できるもの | 本リポ `partners/`（削除前提の短命掲載） |
| Tier C | 実名の他社見積比較・原価表の全量・粗利・交渉記録・個人情報・認証情報 | **GitHub Pages禁止**。Google Drive特定アカウント共有 or 対面提示。原本は各事業privateリポ |

### Tier B（partners/）の必須条件
- パスは**ランダム12文字以上**（相手名・事業名を入れない）。`<meta name="robots" content="noindex, nofollow">` 必須
- **noindex・ランダムURLは偶然アクセス防止であって機密保護ではない**（パスワード画面と同じ位置づけ）。Tier Cの内容は条件を満たしても置けない
- 競合・他取引先は実名を書かず匿名化（A社/B社）。自社の販売価格・粗利・原価の全量一覧は書かない
- 正データはprivateリポ側（例: `repo_kabukuri/medical/pricing/`）。ページ先頭のHTMLコメントに出典ファイル・作成日・削除予定を記す（転記ミス・二重管理防止のため、更新時は正データから再転記して全数字を照合する）
- 公開したら `repo_zoen-tech/docs/public-docs-register.md`（private台帳）に登録し、**商談決着後すみやかに削除**して台帳に削除日を記録する

## Rules
- **publicリポジトリ**である。第三者に読まれる前提で、以下は `content.html` 含めどこにも書かない:
  - 他クライアントの情報・横断的な単価表・原価情報
  - 認証情報・内部URL・個人情報
  - 読まれて困る営業情報（パスワード画面は防御にならない）
- クライアントに共有するURLは GitHub Pages 形式のみ: `https://zoen-tech.github.io/proposals/<クライアント名>/`（github.com のソースURLは共有しない）
- トンマナは `repo_zoen-tech/.claude/skills/zoen-slide-rules/`（隣接リポジトリ）のブランドガイドラインに準拠。参照できない環境では既存案件のCSS変数・ロゴ利用に合わせる
- 外部リンクは `target="_blank"` に `rel="noopener noreferrer"` を付け、調査データには時点を記載する
- 共通テンプレートは未整備（現時点では既存案件フォルダの複製が起点。テンプレ整備後は `templates/` に置きここに追記する）

## Workflow
1. 既存案件フォルダを複製 → フォルダ名をクライアント英語名（kebab-case）に変更
2. `index.html`（タイトル・パスワードハッシュ）と `content.html`（本文・日付・リンク）を差し替え
3. ブラウザでパスワード画面→本文の導線と表示を確認してからpush
4. Pages反映後、`https://zoen-tech.github.io/proposals/<クライアント名>/` をクライアントに共有
5. 終了した案件は原則残す（実績参照用）。ただし失注・クライアント要望・情報陳腐化時の公開停止はユーザーに判断を仰ぐ
