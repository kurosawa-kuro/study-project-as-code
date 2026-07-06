# CLAUDE.md

このファイルは Claude Code がこのリポジトリで作業する際の最小ガイド。

## Source of Truth

- Project overview: `README.md`
- Documentation index: `docs/00_index.md`
- Requirements: `docs/01_requirements.md`
- Architecture: `docs/02_architecture.md`
- Test strategy: `docs/07_test_strategy.md`
- Task notes: `docs/tasks/`

## コマンド

```bash
make setup    # 初期セットアップ (依存取得 + ビルド)
make build    # ビルド
make run      # 実行
make dev      # 開発サーバー / ホットリロード
make test     # テスト
make fmt      # フォーマット
make lint     # 静的解析
```

## アーキテクチャ

このリポジトリは **Project as Code（PaC）** を実装する。プロジェクト情報を6層（Context / Requirement / Decision / Test / Skeleton / Issue as Code）で構造化し、AIと人間が共に参照・更新できる状態を維持する。詳細は `docs/02_architecture.md` を参照。

- AIへ渡す文脈は `.ai/project_context.md` に集約する。作業前に必ず読む。
- 意思決定の記録は `docs/decisions/ADR-NNN-title.md`（ADR形式）に残す。
- PaC が親として管理する子プロジェクトは `src/` 配下に置く（`leader-skill` / `pmbok` / `project-as-code`）。リポジトリは分散させず、関連テーマは子として追加する（ADR-002）。子配下の作業ルールは各子の `CLAUDE.md` を併読する。
- 非機密の設定は `env/config.yaml`、ローカル秘密情報は `env/secret.yaml`、チーム共有・本番クレデンシャルは Doppler (`doppler.yaml`) で管理する。
- 設計・運用ドキュメントは `docs/` 配下。権威順位と更新規約は `docs/00_index.md` に従う。
- パス別ルールは `.claude/rules/` 配下に置く。
- 一回性の作業計画は `docs/tasks/`、繰り返し使う作業手順は `.claude/skills/` に置く。

## 作業ルール

- 独自フレームワーク・独自用語を発明しない。PMBOK / WBS / PDCA / MECE / ピラミッドストラクチャー等、デファクトを忠実に組み合わせる（ADR-003、優先順位は `docs/01_requirements.md#参照フレームワーク`）。
- 推測でコードを書かない。コマンドを書いたら実際に実行して確認する。
- 仕様変更は連動する `docs/` とテストを同一 PR で直す。drift を作らない。
- 既存の関数・ユーティリティ・パターンを優先的に再利用する。
- task note を仕様の正本にしない。確定内容は `docs/specs/`、`docs/adr/`、`docs/runbooks/` に昇格する。

## ハーネス（AI 制御）

このリポジトリの AI エージェント制御一式は `.claude/README.md`（Kurosawa Thin Harness Architecture の実装）。アーキ本体は `docs/specs/kurosawa-thin-harness-architecture.md`（tool-agnostic マスター）、repo 固有の脅威モデルは `docs/specs/{runtime-protocol,capability-boundary,change-boundary,evidence-policy,judgment-memory}.md`。判断日誌は `docs/decisions/decision-log.md`、蒸留記憶は `docs/memory/`。

- **Scope invariant（常時）**: 作業中に Goal/Scope 外の変更・前提崩れ・追加副作用・docs と実装の矛盾を見つけたら即実装しない。`control-change` で分類するか follow-up task に残す。「ついで修正/共通化/改名」は scope creep。
- permissions（`.claude/settings.json`）は安全既定: 生インフラ/DBツールは ask、不可逆破壊のみ deny。このプロジェクトの脅威モデルに合わせ `docs/specs/capability-boundary.md` と一緒に調整する。

### AI Runtime Protocol（薄い・常時）

詳細は `.claude/README.md` と `docs/specs/runtime-protocol.md`、停止条件は同 §「停止して owner に確認する」。

1. Goal / Scope / Done を言い直す。
2. Weight Class を判定（Light / Standard / Heavy → `classify-task`）。Light は以降の重い手順をスキップしてよい。
3. owner-only 判断・保護 capability・allowed/forbidden paths を確認（`scan-decisions` / `capability-boundary.md` / `change-boundary.md`）。
4. Standard/Heavy は skeleton + TDD contract を先に（`plan-skeleton`）。
5. scope 内で最小変更を当てる。複数 attempt が要るなら停止条件付きで回す（`reconcile-task`）。
6. 必要 Evidence Level（≥2、本番は4）で検証（`verify-completion` / `evidence-policy.md`）。
7. scope 拡大・保護境界接触・二度違う理由で検証失敗 → 停止して owner へ。
8. 非自明な判断を下した時だけ記録（`log-decision`）。
