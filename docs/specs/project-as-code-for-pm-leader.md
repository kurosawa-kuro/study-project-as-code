# Project as Code for PM / Leader

PM / リーダー業務を Project as Code で管理するための適用ガイド。

## 目的

PM / リーダー業務の価値は、会議や調整そのものではなく、曖昧な状況を構造化し、判断可能な成果物へ変換することにある。

Project as Code では、それを次のように扱う。

```text
口頭・チャット・会議
  -> context
  -> requirements
  -> decisions
  -> tests
  -> skeleton
  -> issues
```

## PM 成果物と PaC

| PM成果物 | PaCでの置き場 | 内容 |
|---|---|---|
| ヒアリングメモ | `.ai/project_context.md` / docs | 背景、前提、制約、関係者 |
| 要件定義 | `docs/01_requirements.md` | 目的、スコープ、ユースケース |
| 判断理由 | `docs/decisions/` | 採用・却下・保留の理由 |
| 受入条件 | `docs/07_test_strategy.md` / specs | 完了条件、検証観点 |
| 実装前構造 | `docs/specs/` | skeleton、境界、責務 |
| タスク分解 | `docs/tasks/` / issues | 1時間〜半日単位の作業 |

## 上半分PMで使う

上半分PMは、次の問いを PaC に落とす。

| 問い | 成果物 |
|---|---|
| 何が問題か | context / requirements |
| なぜ今やるのか | requirements / decisions |
| 何をやらないのか | requirements / decisions |
| どの案を採用するのか | decisions |
| 成功条件は何か | test strategy / acceptance criteria |
| どう実装可能な形にするか | specs / skeleton |

## 下半分PMで使う

下半分PMは、次の問いを PaC に落とす。

| 問い | 成果物 |
|---|---|
| 誰が何をいつまでにやるか | tasks / issues |
| 進捗はどう確認するか | workflows / tasks |
| 品質はどう確認するか | test strategy |
| リスクはどこにあるか | decisions / tasks |
| 完了したと言えるか | verification / acceptance criteria |

## AIとの役割分担

| 領域 | 人間 | AI |
|---|---|---|
| 目的 | 最終判断する | 論点候補を出す |
| 課題 | 優先順位を決める | 分解・分類する |
| 戦略 | 採用案を選ぶ | 複数案とリスクを出す |
| 戦術 | 実行可能性を判断する | skeleton / tasks に落とす |
| 品質 | 合否を決める | テスト観点を洗い出す |
| 進捗 | 調整する | 状態を整理する |

AIに任せるのは、整理、比較、下書き、検証補助。
人間が持つのは、目的、優先順位、採用判断、責任。

## 職務経歴書・面談への展開

PaC の成果物は、職務経歴書や面談で次のように使える。

| PaC成果物 | 説明に使える価値 |
|---|---|
| context | 顧客課題の整理力 |
| requirements | 要件定義力 |
| decisions | 判断力、トレードオフ説明力 |
| tests | 品質・受入条件の定義力 |
| skeleton | 実装可能な設計への落とし込み |
| issues | 実行計画、見積もり、進捗管理 |

## 運用ルール

- PM / リーダーの判断は、可能な限り `docs/decisions/` に残す。
- 未定義な相談は、すぐタスク化せず context / requirements に落とす。
- 資格や肩書きではなく、成果物で上半分PMを示す。
- `pm-leader-skill` の文章は素材、PaC 側の specs は運用モデルとして扱う。
