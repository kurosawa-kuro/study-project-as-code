# CLAUDE.md — src/leader-skill

`src/leader-skill/` は Project as Code（親リポジトリ）が管理する子プロジェクト。リーダースキル資格戦略のドキュメントと学習教材を扱う。

## 親リポジトリとの関係

- ハーネス（skills / rules / permissions）、秘密情報管理、コミット規約はすべて親リポジトリの `CLAUDE.md` と `.claude/` に従う。この配下に独自の env / Makefile / doppler.yaml は置かない。
- 親側の位置づけ・取り込みルールは `docs/external-links.md` と `docs/adr/` の該当 ADR を参照する。

## この配下の構成

- `doc/` — 資格戦略の正本（仕様・ロードマップ・カタログ・運用）
- `src/CAPM/` — CAPM 学習教材（最優先。挑戦予定）
- `src/PSPO-I/` — PSPO I 学習教材（受験見送り。必要語彙のみ回収する方針）

## ドキュメント優先順位

矛盾した場合は以下の順で扱う。

```text
doc/02_移行ロードマップ.md
> doc/01_仕様と設計.md
> README.md（この配下の）
```

更新規約の詳細は `doc/README.md` を参照する。

## 作業ルール

- 推測で具体仕様を書かない。判断材料がない箇所は TODO のまま残すか、前提を明記する。
- スコープや採否の変更は `doc/02_移行ロードマップ.md` を先に直し、その後 `doc/01_仕様と設計.md` と README を合わせる。
- 実体の追加や構成変更は `doc/03_実装カタログ.md`、手順や日常運用の変更は `doc/04_運用.md` を更新する。
- 関連ドキュメントは同一変更でまとめて更新し、drift を作らない。
