# Decision Log（判断日誌 / trade journal）

AI エージェント（と人間）が**実行中に下した判断**を時系列で残す append-only の日誌。
トレードで言う「売買日誌」に当たる: 何を・なぜそのサイズで賭けたか、損切りラインはどこか、結果はどうだったか。

## これは何で、ADR / task note と何が違うか

| | レンズ | 寿命 | 例 |
|---|---|---|---|
| `adr/` | **戦略** = アーキ決定（正本） | 長命 | 「runtime state はどこに置くか」 |
| `tasks/` | **個別建玉メモ** = 1タスクの作業記憶 | タスク中 | このタスクの Goal/Scope/証拠 |
| `decisions/`（ここ） | **売買日誌** = 通時の判断の振る舞い | 永続・追記専用 | 「曖昧 Goal にこの既定値で突っ込んだ」「scope外をdeferした」 |

task note は1タスクに閉じるので「最近このエージェントは曖昧スペックにフルレバで入りがち」といった**通時のレビュー**ができない。この日誌はそこを埋める。

## 運用ルール

- **append-only**。過去エントリは書き換えない。結果が後で判明したら `結果` 行だけ追記更新してよい。
- 新しいエントリは**末尾に足す**（古い順・上から下）。
- `--- session boundary <ts> ---` 行はセッション終了時に Stop hook が自動で挿入する。判断ゼロのセッションでは挿入されない。
- 何を書くかの引き金と手順は `.claude/skills/log-decision/` が正本。
- **secret・トークン・cookie・個人パス・実データを書かない**（`.claude/rules/security.md`）。判断の構造だけ残す。

## エントリ形式

```markdown
## <UTCタイムスタンプ> — <判断の一行要約>
- type: default-taken | scope-cut | approach-choice | rollback | risk-accepted | approval-deferred
- 根拠 (why): なぜこの判断か（＝建玉理由 / entry thesis）
- 影響範囲 (blast radius): 何が壊れうるか・可逆性（＝レバ/ロットサイズ）
- 撤退条件 (stop/revert): 何が起きたら戻すか・どう戻すか（＝損切りライン）
- 結果 (outcome): win | loss | open | 塩漬け（後追い更新可）
- link: task note / ADR / PR（任意）
```

---

## 2026-07-06T15:23:03Z — フェーズを「土台作成中」から「実戦投入前」へ判定し、追加の土台磨きを止めた
- type: approach-choice
- 根拠 (why): owner の「まだ土台作成中なのか?」という問いに対し、As-Is 棚卸し（ADR-002/003/004、優先順位15項目、framework-stack 一式、skills 16個）で土台の欠落がほぼないこと、一方で PaC が実プロジェクトを1つも回しておらず全作業がメタ作業だったことを確認。tailoring-policy 自身の破綻条件（全部盛り・台帳化）を回避するには、次は「作る」ではなく「1つ使う」が正しいと判断。owner が記録を承認。
- 影響範囲 (blast radius): ドキュメント上のフェーズ定義のみ（02_architecture に成長フェーズ4段階を新設、project_context のフェーズ更新）。コード・運用資産は不変更で可逆。
- 撤退条件 (stop/revert): 実戦投入で土台の重大な欠落（例: 型が実負荷に耐えない）が判明したら、フェーズを1へ戻し欠落だけを補う（全面作り直しはしない）。
- 結果 (outcome): open — 最初の実戦プロジェクトの選定待ち（有力候補 CAPM、`docs/tasks/backlog/capm-as-first-live-project.md`）
- link: `docs/02_architecture.md#成長フェーズ` / ADR-002〜004
