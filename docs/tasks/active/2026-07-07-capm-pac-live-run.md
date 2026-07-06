# CAPM 挑戦を PaC 最初の実戦プロジェクトとして運用する

Task Contract Lite / Standard。フェーズ2「実戦1つ」の実行 task（owner 承認 2026-07-07、経緯は `docs/tasks/done/capm-as-first-live-project.md`）。

## Goal

CAPM 挑戦（`src/leader-skill/`）を PaC の型（WBS / RAID / KPI / Issue as Code）で運用し、受験判断（要件充足 + 模擬問題の安定度）まで完走する。同時に PaC の型の過不足を実負荷で検証する。

## Value

docs canonicalization / dev speed（PaC フェーズ2の完了条件を満たす。型の実地検証で骨格の過剰・不足を発見する）

## Context

- 資格戦略の正本: `src/leader-skill/doc/02_移行ロードマップ.md`（CAPM = 挑戦予定。23時間教育要件を満たしたうえで受験判断へ進む）
- 教材: `src/leader-skill/src/CAPM/`（10章・合計目安26時間・推奨学習順あり）
- 受験判断基準: 要件充足（23 contact hours）+ 模擬問題の安定度（`00_試験概要と学習ロードマップ.md`。合格ラインの市場目安は正解率60〜65%）

## WBS（教材ベース・最小）

| WP | 内容 | 目安 | 前提 |
|---|---|---|---|
| W0 | 23 contact hours 講座の選定（購入判断は owner） | - | なし（先行ブロッカー） |
| W1 | 基礎固め: 00 試験概要 + 01 PM基礎 | 4h | なし |
| W2 | 予測型: 02 計画とコントロール（EVM/CPM 計算習得）+ 03 リスク・品質・変更 | 8h | W1 |
| W3 | 適応型とBA: 04 アジャイル + 05 ビジネス分析（比率47%の中核） | 6h | W1 |
| W4 | 06 ステークホルダー + 07 実務ケース | 4h | W2, W3 |
| W5 | 08 問題演習21問 + 09 直前チェックリスト | 4h | W4 |
| W6 | 受験判断（W0 充足 + 模擬安定度を owner が判断） | - | W0, W5 |

実行粒度: 各 WP を着手時に1時間〜半日の学習タスク（Issue as Code）へ分解し、本ファイル末尾の進捗ログに記録する。

## RAID（軽量）

| 種別 | 内容 | 対応 |
|---|---|---|
| Risk | 他コミットメント（実案件・Kaggle 等）との時間衝突 | 週次で進捗ログを見て WP の順序・粒度を調整 |
| Risk | 管理過剰（型張りが学習時間を圧迫） | 型を削る側に倒し、削った事実を decision-log へ |
| Assumption | 教材26時間は初回読了の想定（演習反復は含まず） | W5 で反復分を再見積もり |
| Issue | 23 contact hours 講座が未選定 | W0 を最初に着手。候補比較まで AI 可、購入は owner |
| Dependency | 受験可否は要件充足 + 模擬安定度で判断（挑戦予定であり受験確定ではない） | W6 で owner 判断 |

## KPI

- 教材完走: 10/10 章
- 演習正解率: 08章21問 + 模擬で **65%超を安定して上回る**（受験判断の入力。市場目安60〜65%に基づく）
- 受験要件: 23 contact hours 充足

## Scope

- W0〜W6 の実行と進捗ログ運用
- tailoring-policy への「学習プロジェクト」濃淡の追記（実績として）
- 型の過不足のフィードバック（decision-log / framework-stack）

## Non-scope

- CAPM 教材の内容改訂（`src/leader-skill/doc/05_CAPM資料改善計画.md` の管轄）
- PMBOK 全成果物の生成・重い RACI 等の型張り（単独学習に不要）
- PMLE / PSM I / Databricks（移行ロードマップのスコープ境界どおり対象外）

## Plan

1. W0: 講座候補の比較表を作り owner へ（購入判断材料）
2. W1 から推奨学習順どおりに進め、着手 WP ごとに Issue 粒度へ分解
3. 週次: 進捗ログ更新、RAID 見直し、型の過不足を記録
4. W5 完了時: KPI 判定 → W6 の owner 判断へ

## Acceptance Criteria

- [ ] W0: 講座候補比較が owner に提示され、選定済み
- [ ] W1〜W5: 各 WP の完了が進捗ログに証跡つきで記録されている
- [ ] KPI: 演習・模擬 65%超の安定 or 未達なら弱点と追加計画が記録されている
- [ ] W6: 受験可否の owner 判断が decision-log に記録されている
- [ ] tailoring-policy に「学習プロジェクト」行が追記されている（本 task で実施済みかを確認）

## Stop / Ask Owner If

- 講座の購入・受験申込み（金銭を伴う判断はすべて owner。`.ai/project_context.md` の human_decision_required: money）
- 型張りが学習時間を圧迫し始めた（削る方向の変更は可、型の追加は不可）
- KPI 未達が2回連続し、計画の前提（26時間想定）が崩れたとき

## 進捗ログ

- 2026-07-07: task 開始。W0 が先行ブロッカー。
