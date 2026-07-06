# AI Project Context

このファイルはAIが作業前に読む唯一の文脈集約ファイル。
**常に最新を保つこと。古い内容はAIの誤推論につながる。**

---

## プロジェクト概要

**名称:** project-as-code  
**目的:** プロジェクト情報（前提・要件・判断・成果物・タスク）を Markdown / YAML / Issue で構造化し、AIと人間が共に参照・更新できる状態を維持する。  
**フェーズ:** テンプレート整備中（ドキュメント骨格の確立段階）

**子プロジェクト:** `projects/leader-skill/` — リーダースキル資格戦略と学習教材（CAPM 最優先）。旧 `study-leader-skill` リポジトリを吸収したもの（`docs/adr/ADR-001-absorb-study-leader-skill.md`）。子配下の作業は `projects/leader-skill/CLAUDE.md` を併読する。

---

## 現在の状態

| 項目 | 内容 |
|------|------|
| アクティブタスク | `docs/tasks/active/` を確認すること |
| 直近の決定 | `docs/decisions/` を確認すること |
| ブロッカー | なし（随時更新） |

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
| `projects/leader-skill/` | 子プロジェクト: 資格戦略・学習教材（正本は `projects/leader-skill/doc/`） |

---

## 更新ルール

- 決定事項は会議後24時間以内に反映する。
- 「現在の状態」セクションは作業開始時・終了時に更新する。
- このファイルに仕様の正本を書かない。正本は各 `docs/` ファイルに置く。
- 古くなったセクションは削除するか `[要更新]` でマークする。
