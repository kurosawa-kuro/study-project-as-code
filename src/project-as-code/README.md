# project-as-code

Project as Code（PaC）フレームワーク自体を成果物として育てる子プロジェクト。親リポジトリが管理する。

親リポジトリの `docs/` は「このリポジトリを PaC で運用するための正本」であるのに対し、この子プロジェクトは「PaC を他プロジェクトへ持ち出せる形（テンプレート・雛形・導入手順）」として切り出し、育てる場所とする（この位置づけは仮置き。確定時に本文を更新する）。

## 位置づけ（暫定）

- 主対象: PaC の6層モデル（Context / Requirement / Decision / Test / Skeleton / Issue as Code）を再利用可能なテンプレート群にすること
- 主眼: 親リポジトリでの運用実績から得た型を、プロジェクト非依存の形へ蒸留する
- 親との役割分担:

| 置き場 | 役割 |
|---|---|
| 親 `docs/` | PaC の仕様・アーキテクチャの正本と、本リポジトリ自身の運用 |
| 親 `docs/templates/` | 親のハーネス運用で使う各 Layer のテンプレ |
| `src/project-as-code/` | 持ち出し可能な PaC 一式（テンプレート・導入手順・サンプル） |

## 構成

```text
src/project-as-code/
├── doc/    # 切り出し方針・親 docs との棲み分けルール
└── src/
    ├── framework-stack.yaml       # 採用フレームワーク一覧と重み（正本）
    ├── tailoring-policy.md        # 対象別に何を重く/軽くするか
    ├── anti-cannibalism-rules.md  # 役割衝突を避けるルール
    └── profiles/                  # 役割別プリセット（スキーマ確定待ち）
```

## ステータス

テーラリング資産の骨格を実装済み（2026-07-07、owner 承認。方針は ADR-004、経緯は `docs/tasks/done/implement-framework-tailoring-skeleton.md`）。

以下が未確定（TODO）。

- [ ] `framework-stack.yaml` の未収載5項目（ステークホルダー分析 / イシューツリー / KPI・KGI・OKR / DDD系 / CI・CD・GitOps）の重み付け
- [ ] `profiles/` のスキーマ確定と役割別プリセットの作成
- [ ] `templates/`（pmbok/wbs/raci/…）の要否 — 親 `docs/templates/` との重複をどちらへ寄せるか決めてから
- [ ] `generated/`（テーラリング結果の出力置き場）の要否 — 実運用が始まってから判断
