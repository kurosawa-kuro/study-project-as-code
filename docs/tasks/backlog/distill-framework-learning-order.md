# 役割別必須セットと学習順4層の蒸留判断

Task Contract Lite（`docs/templates/task-contract-lite.md`）。

## Goal

`docs/archive/framework-priority-brainstorm.md` の未蒸留部分（§3 役割別必須セット A〜D、§5 学習順4層）を、正本化する・しない・どこに置くかを owner が判断し、確定分だけ蒸留する。

## Value

必須コア15表（蒸留済み、`docs/01_requirements.md#参照フレームワーク`）に対し、役割別の内訳と学習順が素材のまま archive に眠っている。学習順は CAPM 学習計画（`src/leader-skill/`）と接続すれば実行計画になる。

## Scope

- §3 役割別必須セット（バックエンド / MLOps / PM / コンサル）の正本化要否の判断
- §5 学習順4層（PM上流 → 説明・コンサル → 技術リーダー → MLOps専門性）の正本化要否と置き場所の判断
  - 候補: `src/leader-skill/doc/`（学習ロードマップの管轄）または `docs/01_requirements.md` の参照フレームワーク節配下

## Non-scope

- 必須コア15表そのもの（蒸留済み・ADR-003）
- §2 理由・§4 破綻条件（思考過程の素材として archive 保持のまま）
- 新しいフレームワークの追加検討

## Done

- 各未蒸留部分について「正本化した / 素材のまま archive 保持」のどちらかが決まり、正本化分は置き場所へ反映済み
- archive 冒頭の「未蒸留」注記を結果に合わせて更新済み

## Evidence

- 蒸留先ドキュメントの diff、または「archive 保持」の判断記録

## Stop / Ask Owner If

- 学習順を `src/leader-skill/` の既存ロードマップ（`doc/02_移行ロードマップ.md`）と統合する場合、優先順位（CAPM 最優先）と矛盾が出たとき
