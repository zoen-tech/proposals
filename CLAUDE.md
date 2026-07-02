# zoen-tech-proposals リポジトリ

## Why（目的）
クライアント向け提案書をHTML形式で格納し、GitHub Pagesで公開するリポジトリ（**publicリポ**、GitHub リポ名は `zoen-tech/proposals`）。URL共有だけでクライアントが提案書を閲覧できる。

## Structure（構成）
```
assets/            ← 共通アセット（ロゴ等）。各案件から ../assets/ で参照
<クライアント名>/   ← 案件ごとのフォルダ（例: marubashi-ladies/）。英語名kebab-case
├── index.html     ← パスワード入力画面（本体ではない）
└── content.html   ← 提案書本文
```
- `index.html` のパスワードは**簡易的な導線制御であってアクセス制御ではない**（`content.html` は直リンクで開ける。パスワードハッシュも `index.html` 内にある）

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
