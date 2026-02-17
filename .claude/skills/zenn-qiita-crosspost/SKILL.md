---
name: "zenn-qiita-writing"
description: "ZennまたはQiitaの記事を執筆する。ユーザーが「記事を書きたい」「Zenn用にまとめて」「Qiitaに投稿したい」などと言ったときに使用する。各プラットフォームのFront Matter形式に沿った記事作成をサポートする。"
---

# Zenn × Qiita 記事執筆

Zenn または Qiita 用の Markdown 記事を作成する。

## Front Matter 形式

Zenn / Qiitaの記事として認識させるには、それぞれ以下のようなFrontMatterを設定する必要がある。

### Zenn（`articles/*.md`）

```yaml
---
title: "記事タイトル"
emoji: "🔥"           # 絵文字（1文字）（Unicode 14.0までに収録されている絵文字）
type: "tech"          # tech / idea
topics:               # タグ（配列, 全て小文字）
  - claude
  - tech              # tech or idea どちらかは必須
published: true       # true: 公開 / false: 下書き
published_at: 2050-06-12 09:03  # 予約公開（任意）
---
```

### Qiita（`public/*.md`）

```yaml
---
title: "記事タイトル"
tags:                 # タグ（配列, 全て小文字の制約はない）
  - GitHub
  - TypeScript
private: false        # false: 公開 / true: 限定共有
updated_at: ""        # 投稿時に自動入力
id: null              # 投稿時にUUIDが自動入力
organization_url_name: null
slide: false
ignorePublish: false  # trueでpublish対象外
---
```

## 記事の配置場所

```text
repo-root/
  articles/        # Zenn用（Zennがここを見る）
  public/          # Qiita用（Qiita CLIがここを見る）
  images/          # Zenn / Qiita 画像用
```

## 記事作成の流れ

1. ユーザーからテーマをヒヤリング

2. ユーザーから、メインメッセージと記事のコンテンツ構成の全体イメージをヒヤリング。必要に応じてユーザーに提案してもよい（こうした方がより閲覧者に親切です / こうした方が伸びます などなど）

3. ユーザーからそれぞれのプラットフォームにおける公開 / 非公開 設定をヒヤリング

4. 執筆

5. LINT系コマンドをすべて実行し、形式的な品質チェック -> 修正

6. ユーザーにレビュー依頼をし追加修正があれば修正。完成するまで繰り返す

7. 感性の合意が取れたら最後にもう一度LINT系を実行し、問題なければCommit,Push（mainブランチでOK）

## 重要: 記事執筆の心構え

- AI感を出さない（あえて全体のバランスを崩す）
- 人間が読むものであるため、人に寄り添うような記事を書く
- 文体: うるさすぎず、落ち着きすぎない。丁寧な日本語をベースとしつつ、「自然に崩す」（丁寧すぎるとAI感が増す）
- 絵文字禁止
- 全体構成は論理的に構造化する。`1.`,`1.1`, `2.`等の章建てを使う
- 画像があった方が良ければプレースホルダとしてPATHを記載しておく。ユーザーが撮影し`images/`配下に格納します。
  - 画像の命名規則：`記事ファイル名01` (`01`部分は記事が出てくる順に採番)(例: `zenn-qiita-crosspost01.png`)

---

## 【参考】CLIについて

### Zenn

```bash
# CLIで雛形作成（任意）
npx zenn new:article

# ローカルプレビュー
npx zenn preview

# push で自動デプロイ（GitHub連携設定済の場合）
git push
```

### Qiita

```bash
# CLIで雛形作成
npx qiita init

# 手動投稿
npx qiita publish

# 全記事投稿
npx qiita publish --all
```

## 【参考】自動投稿の仕組み

GitHub を正本にして Zenn と Qiita に自動投稿する仕組みの詳細は、`reference/AUTO_DEPLOY_SETUP.md` を参照してください。

| プラットフォーム | 方式 |
|------------------|------|
| **Zenn** | Pull型（ZennがGitHubをチェック） |
| **Qiita** | Push型（GitHub Actionsで投稿） |

---

## 公式リファレンス

- [Zenn: GitHub 連携](https://zenn.dev/zenn/articles/connect-to-github)
- [Zenn: Zenn CLI ガイド](https://zenn.dev/zenn/articles/zenn-cli-guide)
- [Qiita: Qiita CLI](https://qiita.com/Qiita/items/666e190490d0af90a92b)
- [Qiita CLI: GitHub](https://github.com/increments/qiita-cli)
