# CAPM 挑戦を PaC 最初の実戦プロジェクトにする（承認済み・完了）

> **結果（2026-07-07）:** owner 承認。実行 task を `docs/tasks/active/2026-07-07-capm-pac-live-run.md` として作成（WBS 7 WP / RAID / KPI 込み）。tailoring-policy に「学習プロジェクト」行を追記。本 note は選定判断の記録として done へ。

Task Contract Lite（`docs/templates/task-contract-lite.md`）。フェーズ2（実戦1つ）の候補選定（以下、選定時の推薦内容）。

## Goal

CAPM 挑戦（`src/leader-skill/`）を PaC の型に乗せ、実負荷で型の過不足を検証しながら学習を完走する。

## Value

- フェーズ2の完了条件（実プロジェクト1つを PaC で回す）を満たす最有力候補:
  - 本物の目標（優先度最上位・挑戦予定）で、締切・成果物・リスクが実在する
  - PaC の型がそのまま張れる: WBS（教材10章の学習分解）、RAID（追い込み期と他コミットの衝突リスク）、KPI（模試スコア・合格基準）、Issue as Code（1時間〜半日の学習タスク）
  - tailoring-policy の実地テストになる（「学習プロジェクト」は濃淡表にない対象。軽量構成の組成が最初のテーラリング実績）
  - 失敗しても外部に迷惑がかからない

## Scope

- 学習プロジェクトの task 化（`create-task`）と WBS / RAID / KPI の最小セット組成
- 「学習プロジェクト」対象の濃淡を tailoring-policy の表へ追記（実績として）
- 型の過不足のフィードバック（decision-log / framework-stack への反映）

## Non-scope

- CAPM 教材の内容改訂そのもの（`src/leader-skill/doc/05_CAPM資料改善計画.md` の管轄）
- PMBOK 全成果物の生成（01_requirements の非対象・非機能要件「軽量性」に反する）

## Done

- CAPM 学習が PaC の型（task / WBS / RAID / KPI / Issue as Code）で運用開始されている
- テーラリング結果（何を重く・何を省いたか）が記録されている

## Evidence

- 学習 task 群と RAID / KPI の実体、tailoring-policy の追記 diff

## Stop / Ask Owner If

- PaC の型張りが学習時間そのものを圧迫し始めたとき（管理過剰は破綻条件。型を削る側に倒す）
- `docs/tasks/backlog/distill-framework-learning-order.md`（学習順4層の蒸留判断）と統合すべきか迷ったとき — 学習順の第1〜2層は CAPM 学習計画とほぼ重なるため、本 task 承認時に一緒に判断するのが効率的

## 参照

- フェーズ判定: `docs/02_architecture.md#成長フェーズ` / decision-log 2026-07-06T15:23:03Z
- 資格戦略の正本: `src/leader-skill/doc/`（CAPM は挑戦予定 / PSPO I は受験見送り）
