# External Links

関連リポジトリとの役割分担。

## study-leader-skill（吸収済み）

旧 `study-leader-skill` リポジトリは 2026-07-06 に本リポジトリの `src/leader-skill/` へ履歴ごと吸収した（[ADR-001](adr/ADR-001-absorb-study-leader-skill.md)）。以後の正本は `src/leader-skill/` であり、旧リポジトリは更新しない。

## pm-leader-skill

| 項目 | 内容 |
|---|---|
| パス | `/Users/kurosawa/Dev/pm-leader-skill` |
| 役割 | PM / リーダースキルの素材、記事、自己説明、キャリア言語化 |
| PaC 側の取り込み先 | `docs/specs/pm-leader-skill-model.md` |
| PaC 側の適用ガイド | `docs/specs/project-as-code-for-pm-leader.md` |

## 関係

```text
pm-leader-skill
  = 素材 / 記事 / キャリア説明

project-as-code
  = 運用モデル / 成果物化 / AIと人間が使う型
```

## 取り込みルール

- `pm-leader-skill` の文章を、そのまま PaC の正本にしない。
- PaC 側では、再利用可能な概念、用語、運用ルールへ蒸留する。
- 職務経歴書、面談、記事へ展開する場合は `pm-leader-skill` 側で育てる。
- プロジェクト運用、AI協働、タスク化、判断記録へ使う場合は `project-as-code` 側で育てる。

## 現在の対応

| pm-leader-skill | project-as-code |
|---|---|
| `01-upper-lower-pm-model.md` | `docs/specs/pm-leader-skill-model.md` |
| `01-upper-lower-pm-model.md` | `docs/specs/project-as-code-for-pm-leader.md` |
