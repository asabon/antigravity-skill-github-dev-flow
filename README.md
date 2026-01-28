# antigravity-skill-github-dev-flow

Antigravity AI エージェント向けの GitHub 開発フロー管理スキルです。

## 概要
このスキルは、以下のステップを自動化・標準化します：
1. Issue の作成
2. 規約に沿った作業ブランチの作成
3. 開発内容の追跡
4. プルリクエストの作成（Issue との紐付け）

## 導入方法
プロジェクトの `.agent/skills/` ディレクトリでサブモジュールとして追加してください。

```bash
git submodule add https://github.com/asabon/antigravity-skill-github-dev-flow .agent/skills/github-dev-flow
```

## 構成
- `SKILL.md`: エージェント向けの命令定義
- `scripts/`: スキルを補助するスクリプト（予定）
- `examples/`: 参考テンプレートなど

## 開発・貢献の仕方

このスキルを親プロジェクトのサブモジュールとして運用しながら改善する場合、以下の手順を推奨します。

1. **ブランチの作成**: サブモジュールディレクトリ内で開発用ブランチを作成します。
   ```bash
   cd .agent/skills/github-dev-flow
   git checkout -b fix-contribution-guide  # または Issue 番号を含める
   ```
2. **修正と試用**: `SKILL.md` 等を修正し、親プロジェクトでの動作を確認します。
3. **PR の作成**: サブモジュール単体でスキルリポジトリに対して PR を作成します。
   ```bash
   git add .
   git commit -m "docs: 開発・貢献フローを追記"
   git push origin <branch-name>
   gh pr create --repo asabon/antigravity-skill-github-dev-flow
   ```
4. **親プロジェクトへの反映**: スキル側の PR がマージされた後、親プロジェクトでサブモジュールのポインタを更新し、親プロジェクト側で PR を作成します。