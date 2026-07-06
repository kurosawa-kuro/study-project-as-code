# tailoring-policy — 対象別に何を重く/軽くするか（正本）

固定セットではなく、対象（案件・役割）ごとにフレームワークの濃淡を変える（ADR-004）。テーラリング（選定・重み調整・削減・再構成）は AI が行い、人間は目的・制約・判断基準・破綻条件を与える。

現在採用中の stack と重みは [`framework-stack.yaml`](framework-stack.yaml) が正本。本ポリシーは対象が変わったときに stack をどう組み替えるかの基準表。

## 対象別テーラリング表

| 対象 | 重くするフレームワーク | 軽くする / 省くもの |
|---|---|---|
| 小規模Webアプリ | WBS、ADR、C4、RAID、KPI | PMBOK全量、重いRACI |
| 業務委託PM支援 | PMBOK、WBS、RACI、RAID、ステークホルダー分析 | DDD詳細、MLOps詳細 |
| MLOps案件 | MLOps Lifecycle、Data Contract、Model Monitoring、SRE、RAID | 事業戦略系フルセット |
| クラウドネイティブ基盤 | SRE、SLI/SLO、GitOps、ADR、C4、RAID | マーケ系フレーム |
| コンサル提案 | MECE、Issue Tree、SCQA、Pyramid、As-Is/To-Be | 実装詳細フレーム |
| 技術リード | ADR、C4、DDD、Clean Architecture、SRE、CI/CD | コンサル資料系の過剰運用 |

## 適用手順

1. 対象を特定し、上表の該当行を起点にする（該当行がなければ最も近い行 + 差分を owner に確認）。
2. `framework-stack.yaml` の `target` / `frameworks` / 重みを対象に合わせて再編成する。
3. 組み合わせが役割重複・抽象度衝突を起こさないか [`anti-cannibalism-rules.md`](anti-cannibalism-rules.md) で確認する。
4. 結果を Project as Code として残し（stack の更新 + 判断は decision-log / ADR）、次回以降の再利用資産にする。

## 破綻条件（このポリシーが壊れるとき）

- AI に自由発明させる（デファクトから外れて独自理論化する）
- フレームワークを全部盛りする（PaC が重くなり死ぬ）
- 人間が判断基準を渡さない（AI が一般論で組み合わせる）
- 再利用資産がない（毎回ゼロから作り直し）
- PaC が更新されない（実態と乖離して台帳化する）
