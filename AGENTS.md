# AGENTS.md

AI コーディングエージェント（Claude Code / Codex / GitHub Copilot 等）共通の作業ガイド。
Codex は作業前にこのファイルを読むため、ここには repo 共通方針のみ記す。
ツール固有の指示は各ツールのファイル（例: Claude Code は `CLAUDE.md`）に置く。

## プロジェクト概要

- 目的: プロジェクト情報（前提・要件・判断・成果物・タスク）を Markdown / YAML / Issue / コードとして構造化し、AIと人間が共に参照・更新できる状態を維持する（Project as Code）
- 構成: 6層モデル（Context / Requirement / Decision / Test / Skeleton / Issue as Code）
- 詳細: `docs/01_requirements.md`（要件）、`docs/02_architecture.md`（基礎設計）

### 作業前に必ず読むファイル

- `.ai/project_context.md` — AIへ渡す文脈の集約（最重要）
- `docs/02_architecture.md` — 6層構造とAI/人間の責任分界

### AIが担う領域 / 担わない領域

AIが担う: 曖昧さ検出、質問生成、成果物ドラフト、整合性チェック。  
人間が握る: 予算・契約・納期コミット・本番リリース判断・優先順位の最終決定。

## セットアップ / 主要コマンド

```bash
make setup    # 依存取得 + ビルド
make dev      # 開発サーバー
make test     # テスト
make fmt      # フォーマット
```

## コーディング規約

- 既存のコード・命名・パターンに合わせる。新規導入より既存の再利用を優先する。
- 変更後はテストとフォーマッタを実行してから完了とする。
- 非機密の設定値は `env/config.yaml`、ローカル秘密情報は `env/secret.yaml`、チーム共有・本番クレデンシャルは Doppler (`doppler.yaml`)。秘密情報をコミットしない。

## ドキュメント

設計・仕様・運用は `docs/` 配下を参照。更新規約と権威順位は `docs/00_index.md` に従う。
仕様レベルの変更は連動するドキュメントを同一 PR でまとめて直す。

## Codex / Claude Code

- `AGENTS.md` は Codex / 他エージェント共通ガイド。
- `CLAUDE.md` は Claude Code の司令塔。
- `.claude/rules/` と `.claude/skills/` は Claude Code 用。Codex が読む前提にしない。
- Codex 向けに永続させたい recurring な指摘やミス防止は、この `AGENTS.md` または nested `AGENTS.md` に小さく追加する。

## Task / Skill

- 一回性の作業計画・調査メモ・実装タスクは `docs/tasks/` に置く。
- Claude Code で繰り返し使う作業手順は `.claude/skills/` に置く。
- Codex repo skills を本格運用する場合は `.agents/skills/` を任意追加する。標準生成物には含めない。
- task note を仕様の正本にしない。確定した仕様は `docs/specs/`、判断理由は `docs/adr/`、運用手順は `docs/runbooks/` に昇格する。
