# 02 アーキテクチャ（基礎設計）

## 概要

```text
人間の曖昧な業務判断
  → Context / Requirement / Decision as Code で構造化
  → AIが処理可能な中間コードへ変換
  → Issue as Code で分解
  → 仕様・設計・テスト観点・Skeletonを生成
  → 人間がレビュー・意思決定
  → 実行・更新ループ
```

PaCは「AIにPMを丸投げする仕組み」ではなく、**人間の意思決定領域を明示し、AIに渡せる作業領域を構造化する設計思想**。

---

## 構成要素（6層）

| 層 | 名称 | 役割 | 主なファイル |
|----|------|------|-------------|
| 1 | **Context as Code** | 前提・用語・関係者・制約を定義する | `glossary.md`, `stakeholders.md`, `context.md` |
| 2 | **Requirement as Code** | 要件・業務フロー・スコープをMarkdown化する | `requirements.md`, `scope.md` |
| 3 | **Decision as Code** | 意思決定・却下理由・未決事項を記録する | `decisions/ADR-NNN-title.md` |
| 4 | **Test as Code** | 仕様からテスト観点・受入条件へ変換する | `test_strategy.md`, `test-cases.md` |
| 5 | **Skeleton as Code** | 実装前に構造だけを先に固定する | `skeleton/` |
| 6 | **Issue as Code** | 1時間〜半日単位でAI実装可能な粒度へ分解する | `issues/TASK-NNN.md` |

各層は独立していないため、**Layer 1→2→3の順に固めてからLayer 4→5→6へ進む**。

---

## ディレクトリ設計

```
docs/
  00_project_charter.md      プロジェクト憲章（目的・期限・ステークホルダー）
  01_requirements.md         要件（本ファイルの親）
  02_architecture.md         基礎設計（本ファイル）
  03_domain_model.md         用語・ドメイン概念
  04_workflows.md            運用フロー・コマンド
  05_data_model.md           データ・スキーマ
  06_error_policy.md         エラー処理・リトライ
  07_test_strategy.md        テスト方針と品質ゲート
  08_release_runbook.md      リリース・復旧
  decisions/
    ADR-NNN-title.md         意思決定記録（ADR形式）

.ai/
  project_context.md         AIへ渡す文脈の集約（最重要。常に最新を保つ）
  coding_rules.md            コーディング規約
  review_rules.md            レビュー観点
  pm_rules.md                PM・スコープ判断ルール
  decision_rules.md          AIに意思決定させない境界の定義

issues/
  EPIC-NNN.md                エピック（大きな機能単位）
  TASK-NNN.md                タスク（1時間〜半日単位）
  BUG-NNN.md                 バグ
```

### 最小テンプレート（プロジェクト立ち上げ時）

```
docs/problem_statement.md   ← 課題・背景
docs/requirements.md        ← 要件
docs/scope.md               ← やること / やらないこと
docs/risks.md               ← リスク登録
docs/decisions/ADR-template.md
docs/backlog.md
.ai/project_context.md      ← AIへの文脈（最重要）
.ai/review_checklist.md
```

---

## AIと人間の責任分界

### AIが担う領域

| 作業 | 具体例 |
|------|--------|
| 曖昧さ検出 | 要件の抜け漏れ、未定義の前提を洗い出す |
| 質問化 | ヒアリング質問を生成する（人間が2〜3個を選ぶ） |
| 分類・整形 | 課題・リスク・選択肢を比較可能な形にまとめる |
| 成果物ドラフト | 仕様・Issue・テスト観点・報告文を生成する |
| 整合性チェック | 仕様とコードの差分、要件とテストの接続を確認する |

### 人間が握る領域（AIに渡さない）

```yaml
human_decision_required:
  - money                          # 予算
  - contract                       # 契約・スコープ変更
  - schedule_commitment            # 納期コミット
  - client_facing_commitment       # 顧客向け約束
  - production_release             # 本番リリース判断
  - priority_tradeoff              # 優先順位の最終決定
  - political_conflict             # 利害対立の解消
  - acceptance_criteria_finalization  # 完了条件の確定
```

### ヒアリングフロー（AIを使う場合）

```yaml
hearing_flow:
  input:
    - client_statement             # 顧客発言
    - meeting_note                 # 会議メモ
    - current_issue                # 現在の課題
    - existing_system_context      # 既存システム文脈
  ai_tasks:
    - detect_ambiguity             # 曖昧さを分類
    - generate_questions           # ヒアリング質問を生成
    - map_questions_to_decisions   # 質問と意思決定を紐付け
    - propose_priority_hypotheses  # 優先順位の仮説
    - draft_decision_materials     # 判断材料を整形
  human_tasks:
    - select_2_to_3_key_questions  # 今聞くべき2〜3問を選ぶ
    - confirm_business_priority    # 優先順位を決定
    - own_final_decision           # 最終判断に責任を持つ
```

---

## 役割マッピング

| 作業 | コンサル | PM | リーダー | メンバー |
|------|:--------:|:--:|:--------:|:--------:|
| PaC設計・導入判断 | ◎ | ○ | | |
| Context / Decision 定義 | ◎ | ○ | | |
| Requirement / Scope 整理 | ○ | ◎ | ○ | |
| Issue分解・粒度設計 | | ○ | ◎ | |
| Skeleton / Test 設計 | | | ◎ | ○ |
| ai_context.md 維持 | | ◎ | ○ | |
| AI委譲境界の設定 | ◎ | ◎ | | |
| ドキュメント日次更新 | | | ○ | ◎ |

---

## 参照フレームワーク

| フレームワーク | PaCでの使い方 |
|---------------|--------------|
| **Documentation as Code** | 基盤思想。Markdownで仕様・意思決定・運用を管理する |
| **ADR（Architecture Decision Records）** | Decision as Codeの型。`decisions/ADR-NNN.md` で実装する |
| **PMBOK** | 成果物辞書として使う（全部は作らない）。プロジェクト憲章・リスク登録・要件文書・WBSを選択的に採用する |
| **GitOps** | Gitを単一ソースとして状態管理する。PaCの更新はcommitで追跡する |
| **IaC（Infrastructure as Code）** | 命名・思想の類似元。「状態をコードで表現し、再現可能にする」をプロジェクト管理へ転用する |

---

## 破綻条件

| パターン | 何が起きるか |
|---------|-------------|
| ドキュメントが会議後に更新されない | AIが古い文脈を正として推論する |
| 決定理由がADRに残っていない | 同じ議論を繰り返す |
| 要件とテストが接続していない | 実装は速いが品質保証できない |
| PMBOKの全成果物を作ろうとする | 重すぎて運用停止する |
| `ai_role: project_manager` のように雑に定義する | AIが勝手に優先順位・スコープ・顧客向け文面を決める |
| Issue / ADR / Spec の粒度がバラバラ | AIが文脈を誤認する |
| 意思決定者不在のままAIに整理させ続ける | ステークホルダー調整で破綻する |

---

## 関連タスク

- 構造変更・責務移動・adapter 追加・共通化は、実装前に `docs/tasks/active/` へ task を作る。
- 中規模以上の変更では、task に Skeleton / Plan / Acceptance Criteria を書いてから実装する。
- 確定した設計判断は task から `docs/decisions/ADR-NNN.md` またはこの文書へ昇格する。
