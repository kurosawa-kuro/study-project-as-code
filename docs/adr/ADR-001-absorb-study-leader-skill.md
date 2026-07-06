# ADR-001: study-leader-skill を src/leader-skill/ へ吸収する

- Status: Accepted
- Date: 2026-07-06
- Revised: 2026-07-06 — owner 指示により配置を `projects/leader-skill/` から `src/leader-skill/` へ変更。`src/` は「PaC が親として管理する子プロジェクトの置き場」と再定義（`pmbok` / `project-as-code` も同列に置く）。

## Context

`study-leader-skill` はリーダースキル資格戦略（CAPM / PSPO I 等）のドキュメントと学習教材を持つ独立リポジトリだった。一方 `study-project-as-code`（PaC）はプロジェクト運用の型・ハーネス・判断記録を持つ。両者を別リポジトリで育てると、ハーネス・秘密情報管理・作業ルールが二重管理になり、資格戦略側は PaC の運用モデル（タスク化・判断記録・スキル）を使えない。

キャリア戦略上、CAPM は最優先の取り組みであり、PaC の運用モデルを実際に適用する最初の子プロジェクトとして扱う価値が高い。

## Decision

- `study-leader-skill` を PaC リポジトリの `src/leader-skill/` へ **git subtree マージ（履歴保持）** で吸収する。
- PaC を親、`src/leader-skill/` を子とし、ハーネス（`.claude/`）・秘密情報管理（`env/` + Doppler）・コミット規約は親に一本化する。子配下に独自の Makefile / env / doppler.yaml / AGENTS.md は置かない。
- 子固有の作業ルールは `src/leader-skill/CLAUDE.md` に置き、親 `CLAUDE.md` と併読する。
- 子のドキュメント権威順位（`doc/02_移行ロードマップ.md` > `doc/01_仕様と設計.md` > README）は子の内部で維持する。
- 旧リポジトリは READ ONLY（移設告知のみ残しアーカイブ）。

## Alternatives Rejected

- **git submodule**: 「統合管理して育てる」目的に反し、更新が二重コミットになるため却下。
- **ファイルコピーのみ（履歴破棄)**: 教材・戦略文書の変遷が判断記録として価値を持つため却下。
- **projects/ の新設**: 当初 `projects/` を新設して配置したが、owner 指示により同日 `src/` 配下へ変更（ディレクトリを増やさず `src/` を子プロジェクトの置き場とする）。

## Consequences

- 今後の資格戦略・教材の更新はすべて `src/leader-skill/` で行い、PaC のタスク運用（`docs/tasks/`）・判断記録（`docs/decisions/`）に乗せる。
- 新たな子プロジェクトを吸収する場合も同じ手順（subtree マージ → scaffolding 重複削除 → 子 CLAUDE.md 整備 → ADR）を踏む。
- 旧 `study-leader-skill` の GitHub リポジトリはアーカイブする（owner 作業）。
