# AI Project Context

このファイルはAIが作業前に読む唯一の文脈集約ファイル。
**常に最新を保つこと。古い内容はAIの誤推論につながる。**

---

## プロジェクト概要

**名称:** project-as-code  
**目的:** プロジェクト情報（前提・要件・判断・成果物・タスク）を Markdown / YAML / Issue で構造化し、AIと人間が共に参照・更新できる状態を維持する。  
**フェーズ:** フェーズ2「実戦1つ」進行中（2026-07-07〜。土台=フェーズ1は完了。最初の実戦 = CAPM 挑戦を PaC の型で運用: `docs/tasks/active/2026-07-07-capm-pac-live-run.md`。成長フェーズの正本は `docs/02_architecture.md#成長フェーズ`）

**リポジトリの位置づけ:** owner（新米リーダー・PM・コンサル見習い）の成長関連プロジェクトを分散させず、本リポジトリを親として統合管理する（`docs/adr/ADR-002-monorepo-growth-policy.md`）。

**子プロジェクト:** `src/` 配下で育てる。子配下の作業は各子の `CLAUDE.md`（あれば）を併読する。

| 子 | 役割 |
|---|---|
| `src/leader-skill/` | 資格戦略・学習教材（CAPM 最優先）。旧 `study-leader-skill` を吸収（ADR-001） |
| `src/pmbok/` | PMBOK を軸とした PM 知識体系の正本整理 |
| `src/project-as-code/` | PaC 自体を持ち出し可能な成果物として育てる |

---

## 現在の状態

| 項目 | 内容 |
|------|------|
| アクティブタスク | `docs/tasks/active/` を確認すること |
| 直近の決定 | `docs/decisions/` を確認すること |
| ブロッカー | CAPM の 23 contact hours 講座が未選定（W0、講座購入は owner 判断） |
| 次の一手 | `docs/tasks/active/2026-07-07-capm-pac-live-run.md` の W0（講座候補比較）→ W1（教材00-01） |

---

## AIへの指示

### やっていいこと

- `docs/` 配下のドキュメントを参照・生成・更新する
- イシューツリーで曖昧な論点を分解し、ヒアリング質問に変換する
- 要件・仕様・テスト観点・Issueのドラフトを生成する（人間がレビューする前提）
- ADRドラフトを作成し、判断理由・却下理由・未決事項を整理する
- WBSで作業を分解し、1時間〜半日粒度のIssueに落とす
- As-Is / To-Be でギャップを整理する
- RACI / RAIDログの雛形を埋める

### やってはいけないこと（人間が握る）

```yaml
human_decision_required:
  - money              # 予算・見積もりのコミット
  - contract           # 契約・スコープ変更
  - schedule           # 納期コミット
  - client_commitment  # 顧客向け約束
  - production_release # 本番リリース判断
  - priority_final     # 優先順位の最終決定
  - conflict_resolution # 利害対立の解消
  - acceptance_criteria # 完了条件の確定
```

---

## ロール定義

| ロール | 主な責務 |
|--------|---------|
| コンサル / PM | Context・Decision・Scopeを定義する |
| テックリード | Skeleton・Issue・Testを設計する |
| AIエージェント | ドキュメントを読んで成果物をドラフトする |
| PMO | リスク・課題・承認フローを参照する |

---

## 参照フレームワーク

**原則: 独自フレームワーク・独自用語を発明しない。デファクトを忠実に組み合わせる（ADR-003）。** 優先順位の正本は `docs/01_requirements.md#参照フレームワーク`（PMBOK > WBS > RACI/DACI > RAID > ステークホルダー分析 > MECE > … の15項目）。

組み合わせはカニバリズムを起こさないよう対象ごとに濃淡を変える。テーラリング（選定・重み調整・削減・再構成）は AI の担当、目的・制約・判断基準・破綻条件は人間の担当（ADR-004）。AI は既存 PaC 資産を参照して再編成し、フレームワークを発明しない。

作業時に使う型。詳細は `docs/01_requirements.md#参照フレームワーク` を参照。

| フレームワーク | いつ使うか |
|---|---|
| イシューツリー | 要件の曖昧さ検出・論点分解 |
| So What? / Why So? | ADR根拠の掘り下げ・技術課題のPM翻訳 |
| ピラミッドストラクチャー | 仕様・報告ドキュメントの出力構造 |
| WBS | 作業分解・Issue粒度への落とし込み |
| MoSCoW | Issue優先度の分類（Must / Should / Could / Won't） |
| RACI | 役割・責任の境界整理 |
| RAIDログ | Risks / Assumptions / Issues / Dependencies の管理 |
| As-Is / To-Be | 現状と理想状態の差分整理 |

---

## ドキュメント構造（参照先）

| ドキュメント | 内容 |
|---|---|
| `docs/01_requirements.md` | 目的・範囲・ユーザー・ユースケース |
| `docs/02_architecture.md` | 6層構成・AI責任分界 |
| `docs/03_domain_model.md` | 用語・ドメイン概念 |
| `docs/04_workflows.md` | 作業コマンド・運用フロー |
| `docs/05_data_model.md` | データ・スキーマ |
| `docs/06_error_policy.md` | エラー処理・リトライ |
| `docs/07_test_strategy.md` | テスト方針・品質ゲート |
| `docs/08_release_runbook.md` | リリース・復旧 |
| `docs/decisions/` | ADR（意思決定記録） |
| `docs/tasks/active/` | 現在進行中のタスク |
| `docs/tasks/backlog/` | 積み残しタスク |
| `src/leader-skill/` | 子プロジェクト: 資格戦略・学習教材（正本は `src/leader-skill/doc/`） |

---

## 更新ルール

- 決定事項は会議後24時間以内に反映する。
- 「現在の状態」セクションは作業開始時・終了時に更新する。
- このファイルに仕様の正本を書かない。正本は各 `docs/` ファイルに置く。
- 古くなったセクションは削除するか `[要更新]` でマークする。
