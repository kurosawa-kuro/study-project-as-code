# 03 ドメインモデル

## 用語

| 用語 | 意味 |
|---|---|
| Project as Code | プロジェクト情報を Markdown / YAML / Issue / コードとして構造化し、AI と人間が共に参照・更新できる状態を維持するフレームワーク。 |
| Context as Code | 前提、用語、関係者、制約、背景を構造化して残すこと。 |
| Requirement as Code | 要件、スコープ、業務フロー、ユースケースを構造化して残すこと。 |
| Decision as Code | 採用・却下・保留などの判断と理由を残すこと。 |
| Test as Code | 受入条件、品質観点、検証方法を先に定義すること。 |
| Skeleton as Code | 実装前に責務境界、構造、ファイル配置、インターフェースを固定すること。 |
| Issue as Code | 1時間〜半日単位の実行可能なタスクとして分解すること。 |
| 上半分PM | 目的管理、課題管理、戦略管理、戦術管理を担う PM。未定義な状態から何をやるべきかを決める。 |
| 下半分PM | 品質管理、進捗管理、メンバー管理、タスク管理を担う PM。決まったことを壊さず進める。 |
| PM / Leader Skill | PM / リーダーとしての判断、構造化、説明、実行管理のスキル体系。 |

## 状態 / ライフサイクル

```text
曖昧な相談 / チャット / 会議
  -> Context as Code
  -> Requirement as Code
  -> Decision as Code
  -> Test as Code
  -> Skeleton as Code
  -> Issue as Code
  -> 実行 / 検証 / 改善
```

## 関連タスク

- 用語、状態、ライフサイクルの変更は task に背景と影響範囲を残してから反映する。
- 未確定の業務ルールはこの文書へ入れず、`docs/tasks/backlog/` で調査対象として管理する。
- 確定したドメイン判断は、必要なら `docs/adr/` にも残す。
