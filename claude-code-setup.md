# Claude Code セットアップ手順

## 1回だけやること（初回セットアップ）

### ① Claude Code をインストール
```bash
npm install -g @anthropic-ai/claude-code
```

### ② GitHubの認証を設定（これが肝心）
```bash
# GitHubのPersonal Access Tokenを使って認証
git config --global credential.helper store
git clone https://<YOUR_TOKEN>@github.com/Ken5InvestmentLab/cyberpunk-trade-os.git
```
一度cloneしたら以降はトークン不要。

### ③ リポジトリに入ってClaude Codeを起動
```bash
cd cyberpunk-trade-os
claude
```
CLAUDE.md が自動で読み込まれる。

---

## 毎週の使い方（記事追加）

### Claude Codeを起動
```bash
cd cyberpunk-trade-os
claude
```

### プロンプトをそのまま貼る

**記事1本追加：**
```
以下のキーワードでSEOブログ記事を1本追加して。
CLAUDE.mdのルールに従って。

キーワード：[ここにキーワード]

完了したらgit add / commit / pushまでやって。
```

**記事3本まとめて追加：**
```
以下のキーワードで記事を3本作成して。
CLAUDE.mdのルールに従って。
3本とも完成したらblog/index.htmlとindex.htmlのLatest from the Labも更新して、
sitemap.xmlも更新して、最後にgit pushまでやって。

キーワード：
1. [キーワード1]
2. [キーワード2]
3. [キーワード3]
```

---

## よく使うコマンド

```bash
# Claude Code起動
claude

# 途中で終わった作業を再開
claude --continue

# 特定のファイルだけ渡して指示
claude -f blog/index.html "このファイルに新記事カードを追加して"
```

---

## トラブルシューティング

**pushで認証エラーが出る場合：**
```bash
git remote set-url origin https://<NEW_TOKEN>@github.com/Ken5InvestmentLab/cyberpunk-trade-os.git
```

**CLAUDE.mdが読み込まれてない感じがする場合：**
```bash
# リポジトリのルートから起動してるか確認
pwd  # → /path/to/cyberpunk-trade-os になってるはず
```
