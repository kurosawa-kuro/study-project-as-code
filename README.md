# Project as Code (PaC)

プロジェクト情報（前提・要件・判断・成果物・タスク）を Markdown / YAML / Issue / コードとして構造化し、**AIと人間が共に参照・更新できる状態を維持する**フレームワーク。

解決する課題:
- プロジェクト情報の分散（口頭・チャット・議事録に散在しAIに渡せない）
- 意思決定の属人化（判断理由が残らず同じ議論を繰り返す）
- 上流のボトルネック（開発速度が上がるほど「何を作るか」の決定が詰まる）

## このリポジトリの位置づけ

新米リーダー・PM・コンサル見習いとしての成長に関連するプロジェクトを、リポジトリを分散させずここで統合管理する。project-as-code を親とし、以下を `src/` 配下の子プロジェクトとして育てる（[ADR-002](docs/adr/ADR-002-monorepo-growth-policy.md)）。

オリジナリティは意図して出さない。PMBOK・WBS・PDCA・MECE・ピラミッドストラクチャー等、デファクトのフレームワークを忠実に「組み合わせる」のが黒澤流（[ADR-003](docs/adr/ADR-003-defacto-framework-policy.md)。優先順位は [`docs/01_requirements.md#参照フレームワーク`](docs/01_requirements.md#参照フレームワーク)）。

| 子プロジェクト | 役割 |
|---|---|
| [`src/leader-skill/`](src/leader-skill/README.md) | リーダースキル資格戦略と学習教材（CAPM / PSPO I） |
| [`src/pmbok/`](src/pmbok/README.md) | PMBOK を軸とした PM 知識体系の正本整理 |
| [`src/project-as-code/`](src/project-as-code/README.md) | PaC フレームワーク自体を持ち出し可能な成果物として育てる |

## 構成（6層モデル）

| 層 | 名称 | 内容 |
|----|------|------|
| 1 | Context as Code | 前提・用語・関係者・制約 |
| 2 | Requirement as Code | 要件・業務フロー・スコープ |
| 3 | Decision as Code | 意思決定・却下理由・未決事項（ADR形式） |
| 4 | Test as Code | テスト観点・受入条件 |
| 5 | Skeleton as Code | 実装前の構造固定 |
| 6 | Issue as Code | 1時間〜半日単位のタスク分解 |

## セットアップ

```bash
make setup    # 依存取得 + ビルド
make dev      # 開発サーバー起動
make test     # テスト
```

設定は `env/config.yaml`（非機密）、`env/secret.yaml`（ローカル秘密情報）、Doppler（チーム共有・本番秘密情報）で管理する。
`env/secret.yaml` は `.gitignore` で除外されるためコミットしない。

## ディレクトリ構成

```
.
├── .ai/                  # AIへ渡す文脈（project_context.md が最重要）
├── docs/
│   ├── 00_index.md       # ドキュメント索引・権威順位
│   ├── 01_requirements.md
│   ├── 02_architecture.md
│   ├── decisions/        # ADR（意思決定記録）
│   └── tasks/            # 日次作業計画・実装タスク
├── issues/               # Epic / Task / Bug（Issue as Code）
├── src/                  # PaC が親として管理する子プロジェクト
│   ├── leader-skill/     # リーダースキル資格戦略（旧 study-leader-skill を吸収）
│   ├── pmbok/
│   └── project-as-code/
├── env/
│   ├── config.yaml       # 非機密設定
│   └── secret.yaml       # ローカル秘密情報（コミット禁止）
└── .claude/rules/        # Claude Code パス別作業ルール
```

## ドキュメント

設計・仕様・運用の詳細は [`docs/00_index.md`](docs/00_index.md) を参照。

- [`docs/01_requirements.md`](docs/01_requirements.md) — 目的・範囲・ユーザー・ユースケース
- [`docs/02_architecture.md`](docs/02_architecture.md) — 6層構造・AIと人間の責任分界・破綻条件
- [`docs/specs/pm-leader-skill-model.md`](docs/specs/pm-leader-skill-model.md) — 上半分PM / 下半分PMモデル
- [`docs/specs/project-as-code-for-pm-leader.md`](docs/specs/project-as-code-for-pm-leader.md) — PM / リーダー業務への PaC 適用
- [`docs/external-links.md`](docs/external-links.md) — 関連リポジトリとの役割分担
- [`src/leader-skill/README.md`](src/leader-skill/README.md) — 子プロジェクト: リーダースキル資格戦略と学習教材
- [`docs/04_workflows.md`](docs/04_workflows.md) — 運用フロー・コマンド
- [`docs/07_test_strategy.md`](docs/07_test_strategy.md) — テスト方針
