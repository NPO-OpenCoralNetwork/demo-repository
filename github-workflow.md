# GitHub ワークフロー・ガイド

## 基本的なワークフロー

### 1. リポジトリのクローン
```bash
# SSHの場合
git clone git@github.com:organization/repository.git

# HTTPSの場合
git clone https://github.com/organization/repository.git
```

### 2. ブランチの作成と切り替え
```bash
# 新しいブランチを作成して切り替え
git checkout -b feature/your-feature-name

# 既存のブランチに切り替え
git checkout branch-name
```

### 3. 変更の追跡と確認
```bash
# 変更状態の確認
git status

# 変更内容の確認
git diff

# 変更をステージングに追加
git add file-name     # 特定のファイル
git add .             # すべての変更
```

### 4. コミットの作成
```bash
# 変更をコミット
git commit -m "feat: 変更内容の説明"
```

#### コミットメッセージの規則
- feat: 新機能の追加
- fix: バグ修正
- docs: ドキュメントの更新
- style: コードスタイルの修正
- refactor: リファクタリング
- test: テストコードの追加・修正
- chore: ビルドプロセスやツールの変更

### 5. リモートへのプッシュ
```bash
# 最初のプッシュ
git push -u origin feature/your-feature-name

# 2回目以降のプッシュ
git push
```

### 6. プルリクエストの作成

#### GitHub CLIを使用する場合
```bash
# GitHub CLIでプルリクエストを作成
gh pr create --title "タイトル" --body "説明文" --base main --head feature/your-feature-name
```

#### Webブラウザを使用する場合
1. GitHub.comでリポジトリを開く
2. 「Pull requests」タブをクリック
3. 「New pull request」ボタンをクリック
4. ベースブランチとフィーチャーブランチを選択
5. 「Create pull request」をクリック
6. タイトルと説明を入力
7. 再度「Create pull request」をクリック

### 7. レビュー後のマージ
1. レビューアーを指定
2. レビューコメントに対応
3. 承認後にマージ
4. ブランチを削除（オプション）

## 便利なコマンド集

### ブランチ操作
```bash
# ブランチ一覧表示
git branch

# リモートブランチも含めて表示
git branch -a

# ブランチの削除
git branch -d branch-name
```

### 変更の取り消し
```bash
# 直前のコミットの修正
git commit --amend

# ステージングの取り消し
git reset HEAD file-name

# 変更の破棄
git checkout -- file-name
```

### リモートとの同期
```bash
# リモートの変更を取得
git fetch

# リモートの変更を取得してマージ
git pull

# リモートブランチの削除を反映
git fetch --prune
```

## GitHub CLI のセットアップ

### 1. インストール
```bash
# macOS (Homebrew)
brew install gh

# Windows (Scoop)
scoop install gh
```

### 2. 認証
```bash
# ログイン
gh auth login

# ステータス確認
gh auth status

# ログアウト
gh auth logout
```

### 3. プルリクエスト操作
```bash
# プルリクエスト一覧
gh pr list

# プルリクエスト作成
gh pr create

# プルリクエストの確認
gh pr view

# プルリクエストのチェックアウト
gh pr checkout
```

## トラブルシューティング

### 1. コンフリクトの解決
```bash
# mainブランチの最新変更を取得
git checkout main
git pull

# 作業ブランチに戻ってrebase
git checkout feature/your-feature-name
git rebase main

# コンフリクトを解決後
git add .
git rebase --continue
```

### 2. 誤ったコミットの修正
```bash
# 直前のコミットを修正
git commit --amend

# 複数のコミットをまとめる
git rebase -i HEAD~3  # 直近3つのコミットを操作
```

### 3. プッシュの失敗
```bash
# リモートの変更を取得してrebase
git pull --rebase

# 強制プッシュ（注意: チーム開発では使用を避ける）
git push --force-with-lease
```

## ベストプラクティス

1. **頻繁にコミット**
   - 小さな単位で論理的なコミットを作成
   - 変更内容が明確になるようコミットメッセージを記述

2. **ブランチ戦略**
   - メインブランチ（main）は常に安定した状態を維持
   - 機能開発は必ず新しいブランチで行う
   - ブランチ名は目的が分かるように命名

3. **プルリクエスト**
   - レビューしやすい大きさに保つ
   - 目的と変更内容を明確に説明
   - スクリーンショットや動作説明を追加

4. **コードレビュー**
   - 建設的なフィードバックを心がける
   - レビューコメントには迅速に対応
   - 承認前に全てのコメントが解決されていることを確認
