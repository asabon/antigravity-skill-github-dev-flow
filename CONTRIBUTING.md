# 開発・貢献の仕方

`antigravity-skill-github-dev-flow` への貢献（改善、不具合修正、ドキュメントの更新など）に興味を持っていただきありがとうございます！

このプロジェクトでは、Antigravity AI エージェントと人間が効率的に協力できるよう、以下の開発フローを定義しています。

## 開発フロー

本リポジトリの `main` ブランチは保護されており、直接のプッシュは禁止されています。
変更を加える際は、必ず以下の **Issue 駆動開発フロー** に従って PR を作成してください。

このスキルを親プロジェクトのサブモジュールとして運用しながら改善する場合、以下の手順を遵守してください。

1. **Issue の起票**: スキルリポジトリに対して改善内容を記した Issue を作成します。
2. **ブランチの作成**: サブモジュールディレクトリ内で、Issue ID を含めた開発用ブランチを作成します。
   ```bash
   cd .agent/skills/github-dev-flow
   gh issue develop <Issue番号> --name "<Issue番号>-fix-description" --checkout
   ```
3. **修正と試用**: `SKILL.md` 等を修正し、親プロジェクトでの動作を確認します。
4. **進捗管理**: 作業中はスキルリポジトリ内に一時的な `docs/progress/task.md` を作成して進捗を管理します。
5. **PR の作成**: `task.md` を削除・コミットした後、スキルリポジトリに対して PR を作成します。
   ```bash
   git rm docs/progress/task.md
   git add .
   git commit -m "feat: 〇〇の改善 (Issue #xxx)"
   git push origin <branch-name>
   gh pr create --repo asabon/antigravity-skill-github-dev-flow
   ```
6. **親プロジェクトへの反映**: スキル側の PR がマージされた後、親プロジェクトでサブモジュールのポインタを更新します。

## 成功の定義
- 修正が `SKILL.md` の他の命令と矛盾していないこと。
- PR 本文に `Fixes #xxx` が含まれ、Issue と正しく紐付いていること。
- `task.md` が PR に含まれていないこと。
