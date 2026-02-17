## リポジトリ概要

Zenn・Qiita向けの外部記事執筆用リポジトリ。Markdown記事の品質チェックが自動化されています。

## ディレクトリ構造

- `articles/` - Zenn用記事
- `public/` - Qiita用記事
- `images/` - 共用画像

## Lint ツール

**pre-commitフック**と**GitHub Actions**で品質を強制します。`git commit`時にステージされたMarkdownファイルが自動チェックされます。

### 利用可能なコマンド

| コマンド | 説明 |
|---------|------|
| `npm run lint` | 全リンター実行 |
| `npm run lint:md` | Markdown構文チェック（markdownlint） |
| `npm run lint:text` | 日本語文章校正（textlint） |
| `npm run lint:links` | リンク切れチェック（遅め、手動実行用） |
| `npm run lint:fix` | 自動修正できるものを修正 |

### 設定ファイル

- `.markdownlint.json` - Markdown構文ルール
- `.textlintrc.json` - 日本語文章ルール（preset-ja-technical-writing）
- `.linkcheck.json` - リンク検証ルール

### Pre-commitのスキップ

Pre-commitフックをスキップする場合（非推奨）：

```bash
git commit --no-verify
```

---

## 自動デプロイ

### Zenn

- **方式**: GitHub連携（Pull型）
- `articles/` 配下の `published: true` 記事を自動公開
- 初回セットアップ: ZennのGitHub連携設定を実施

### Qiita

- **方式**: GitHub Actions（Push型）
- `public/` 配下の `private: false` 記事を自動投稿
- Lint成功後のみ実行
- 初回セットアップ: リポジトリSecretsに `QIITA_TOKEN` を設定

### CIフロー

```
push → Lint → (成功) → Qiita自動投稿
            ↓
          Zenn自動同期
```

---

## プレビュー

| プラットフォーム | コマンド |
|-----------------|----------|
| Zenn | `npx zenn preview` |
| Qiita | `npx qiita preview` |
