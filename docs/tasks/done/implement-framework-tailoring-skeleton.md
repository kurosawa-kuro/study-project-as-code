# フレームワークテーラリング骨格の実装判断

Task Contract Lite（`docs/templates/task-contract-lite.md`）。

## Goal

`docs/archive/kurosawa-style-framework-tailoring-brainstorm.md` §3・§5 の未蒸留素材（対象別濃淡表、最小構成案）をもとに、テーラリングの具体構造を `src/project-as-code/` に実装するかを owner が判断し、確定分だけ骨格を作る。

## Value

ADR-004 で「テーラリングは AI に委譲、人間は判断基準を握る」と決めたが、AI が参照する再利用資産（採用フレームワーク一覧と重み・対象別方針・カニバリズム回避ルール・役割別プロファイル）の実体がまだない。これが `src/project-as-code/` の最初の中核成果物の有力候補。

## Scope

- 生メモ §5 の最小構成案の採否判断:
  - `framework-stack.yaml`（採用フレームワーク一覧・役割・重み）
  - `tailoring-policy.md`（対象別に何を重く/軽くするか。§3 の濃淡表が初期素材）
  - `anti-cannibalism-rules.md`（役割衝突回避。ADR-004 Consequences の初期判断例が種）
  - `templates/` / `profiles/` / `generated/` の要否と粒度
- 採用時の置き場所（`src/project-as-code/src/` 配下）とファイル名の確定

## Non-scope

- 黒澤流の原則・役割分担そのもの（ADR-003 / ADR-004 で確定済み）
- 全テンプレート（pmbok/wbs/raci/…）の中身の一括作成（骨格判断が先）
- 親 `docs/templates/` との統合判断（`src/project-as-code/README.md` の既存 TODO で別途）

## Done

- 最小構成案の各要素について「実装した / 見送り」が決まり、実装分が `src/project-as-code/` にコミットされている
- `src/project-as-code/README.md` の位置づけ・TODO が結果と一致している
- archive 冒頭の「未蒸留」注記を結果に合わせて更新済み

## Evidence

- 実装した骨格ファイルの diff、または見送り理由の記録（decision-log か本 task への追記）

## Stop / Ask Owner If

- YAML スキーマ（role / weight 等）の項目設計で生メモに根拠がない拡張をしたくなったとき（推測で仕様化しない）
- 親 `docs/templates/` と役割が衝突する構成になったとき

## 参照

- 方針: `docs/adr/ADR-004-ai-assisted-framework-tailoring.md`
- 素材: `docs/archive/kurosawa-style-framework-tailoring-brainstorm.md` §3・§5

---

## 結果（2026-07-07 完了）

owner 承認を受けて実装。判断と実装内容:

| 要素 | 判断 | 実体 |
|---|---|---|
| `framework-stack.yaml` | **実装** | `src/project-as-code/src/framework-stack.yaml`。生メモ §5 の YAML に忠実（target / principle / frameworks 10項目 / anti_cannibalism 5ルール）。優先順位15項目のうち未収載5項目の重み付けは生メモに根拠がないため owner 判断待ちとしてファイル冒頭に注記 |
| `tailoring-policy.md` | **実装** | `src/project-as-code/src/tailoring-policy.md`。§3 濃淡表6行を正本化 + 適用手順 + §4 破綻条件5つ |
| `anti-cannibalism-rules.md` | **実装** | `src/project-as-code/src/anti-cannibalism-rules.md`。症状5類型と解消3パターン（主を一つ / 目的分離 / レイヤー分離）。マッピングの正本は yaml 側に一本化し重複させない |
| `profiles/` | **スタブのみ** | README で「スキーマの根拠が生メモにない（ファイル名の案のみ）」ため owner 確定待ちと明記（Stop 条件どおり推測で仕様化しない） |
| `templates/` | **見送り** | 親 `docs/templates/` との棲み分けが未決（既存 TODO）。決めてから |
| `generated/` | **見送り** | テーラリングの実運用が始まってから。今作ると空のまま台帳化する |

Evidence: コミット diff（本 task の done 移動と同一コミット）。`framework-stack.yaml` は PyYAML でパース検証済み。
