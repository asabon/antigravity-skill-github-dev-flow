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