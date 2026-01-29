---
name: github-dev-flow
description: GitHub Issue の起票からブランチ作成、PR 作成までの一連の開発ライフサイクルを管理する
---

# GitHub 開発フロー・スキル (github-dev-flow)

## 概要
このスキルは、プロジェクトにおける標準的な開発サイクルを効率化し、一貫性を保つための手順を定義します。
Issue の起票、作業ブランチの作成、実装、コミット、そしてプルリクエスト（PR）の作成までをサポートします。
進捗管理としてプロジェクト内の **`docs/progress/task.md`** を使用し、常に「現在のタスク」の状態を反映させます。
これにより、**セッションを中断しても次回開始時に続きから再開可能**です。

## 手順

### 1. Issue の起票 (Issue Creation)
タスクが発生したら、まず `gh issue create` を使用して Issue を起票します。
- タイトルは内容がわかる簡潔なものにする。
- 本文には `examples/issue_template.md` を使用し、目的と進捗管理用のタスクリストを含める。
- 作成された Issue 番号を取得して記録する。

### 2. ブランチの作成と紐付け (Branching & Linking)
`gh issue develop` コマンドを使用して、Issue に紐付いた作業用ブランチを作成します。
- コマンド例: `gh issue develop <Issue番号> --name "<Issue番号>-<short-description>" --base main --checkout`
  - **重要**: `--name` 引数には、必ず **Issue 番号を含めた形式** (`xxx-short-description`) を指定してください。自動的には付与されません。
- これにより、GitHub 上で Issue とブランチが明示的に紐付き、進捗状況が管理しやすくなります。

### 3. 実装と進捗管理 (Implementation & Tracking)
- `examples/task_template.md` を参考に **`docs/progress/task.md`** を更新し、現在のタスクを管理する。
  - **運用方針**: `task.md` は常に「現在進行中のタスク」を記述します。新しいタスクを開始する際は内容を上書きしますが、**`task.md` はブランチごとに管理される**ため、ブランチを切り替える（作業を中断して別のIssueに移る）際は、必ずその時点の状態をコミットするかスタッシュしてください。これにより、ブランチを戻した際に進捗状況も自動的に復元されます。
  - 過去のタスク履歴は Git のコミットログやクローズされた Issue/PR から参照可能です。
- 作業の進捗に合わせて、GitHub 上の **Issue のチェックボックスを随時更新**する。
  - `gh issue edit <Issue番号> --body-file <更新後の本文>` を使用するか、ブラウザで更新する。
- 修正が完了したら、適切なツール（lint, test等）で品質を確認する。

### 4. コミットとプッシュ (Commit & Push)
- 変更内容をステージングする。
- コミットメッセージには必ず Issue 番号を含める。
  - 例: `feat: ログイン機能の実装 (Issue #123)`
- リモートブランチへプッシュする。

### 5. プルリクエストの作成 (PR Creation)
`gh pr create` を使用して PR を作成します。
- **作成前の確認事項（この順序を守ること）**:
  1. **Issue の最終更新**: 作成予定の PR 自体に関する項目を含め、Issue のすべてのタスクを完了（チェック済み）状態に更新し、GitHub へ反映（`gh issue edit`）する。
  2. **`docs/progress/task.md` の削除とコミット**: `main` ブランチをクランチに保つため、`task.md` を物理的に削除し、その削除を `git add` および `git commit` で記録し、リモートブランチへプッシュする。
  3. PR 本文のチェックリストも、作成時に**すべて完了状態**で作成する。
- タイトルに Issue ID を含める。
- 本文には `examples/pr_template.md` を使用し、`Fixes #xxx` を含めて Issue と紐付ける。
- 実装内容と検証結果を簡潔に記載する。

### 6. クリーンアップ (Cleanup - After Merge)
PR がマージされたら（**ユーザーからの報告により開始**）、ローカル環境を最新の状態に戻し、不要になった作業ブランチを削除します。
- **手順**:
  1. `main` ブランチへ移動する: `git checkout main`
  2. 最新のリモート変更を取得する: `git pull origin main`
  3. 作業が完了したローカルブランチを削除する: `git branch -d <branch-name>`
  4. リモートから削除されたブランチ情報を整理する: `git remote prune origin`

## 成功の定義
- Issue と PR が正しく紐付いている。
- **すべてのタスク（Issue/PR）がチェック済み**で、完了状態が反映されている。
- 作業ブランチが規約通りの名前になっている。
- PR のマージにより Issue が自動的にクローズされる状態になっている。
- マージ後、ローカル環境が `main` の最新状態に更新され、作業ブランチが削除されている。
