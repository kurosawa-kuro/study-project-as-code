# 黒澤流 PaC フレームワークテーラリング — 生ブレスト（archive）

> **退避元:** `docs/tasks/idea/2026-07-07_kurosawa-style-project-as-code-framework-tailoring.md`（2026-07-07 退避）
> **蒸留先:** §1 黒澤流の完全定義（カニバリズム回避・AI委譲の役割分担）→ `docs/adr/ADR-004-ai-assisted-framework-tailoring.md` と `docs/01_requirements.md#参照フレームワーク`
> **未蒸留:** §3 対象別濃淡表・§5 最小構成（framework-stack.yaml 等）→ `docs/tasks/backlog/implement-framework-tailoring-skeleton.md` で判断待ち
> **権威:** archive は権威順位の最下位。ここを正本として参照しない。

---

## 1. 結論

かなり完成度が上がりました。

黒澤流の本質は、こうです。

黒澤流とは、デファクトのフレームワークを忠実に採用し、互いにカニバリズムを起こさないように組み合わせ、意図してフレームワーク層でオリジナリティを出さない実務設計思想である。

独自性は、フレームワークを発明することではなく、対象に応じて適切な組み合わせ・重み・削減を行い、それを Project as Code として再利用可能な形に落とし込む点にある。

その組み合わせ調整は、人間の知能だけで安定運用するには限界があるため、生成AIに委譲する。人間は判断基準・制約・目的・破綻条件を与え、生成AIは既存の Project as Code 資産を参照しながら、対象に最適化された実務構成へ再編成する。

## 2. 理由

これはかなり現実的です。

フレームワークは、単体では強いですが、複数を雑に混ぜると衝突します。

| 問題    | 例                                      |
| ----- | -------------------------------------- |
| 役割重複  | RACI と DACI を両方入れて責任者が二重化する            |
| 過剰管理  | PMBOK、Scrum、OKR、RAIDを全部フル運用して重くなる      |
| 抽象度衝突 | MECE、Issue Tree、Pyramidを同じ用途で使って混乱する   |
| 技術偏重  | DDD/Clean ArchitectureばかりでPM・予算・責任が漏れる |
| 管理偏重  | PMBOKばかりで技術設計・運用品質が裁けない                |

だから、人間がやるべきなのは、
**フレームワーク発明ではなく、目的別の組み合わせ設計**です。

そして、その組み合わせ最適化は、生成AI向きです。

---

## 3. 有力シナリオ

黒澤流を運用に落とすと、こうなります。

| 対象          | 重くするフレームワーク                                             | 軽くする/省くもの      |
| ----------- | ------------------------------------------------------- | -------------- |
| 小規模Webアプリ   | WBS、ADR、C4、RAID、KPI                                     | PMBOK全量、重いRACI |
| 業務委託PM支援    | PMBOK、WBS、RACI、RAID、ステークホルダー分析                          | DDD詳細、MLOps詳細  |
| MLOps案件     | MLOps Lifecycle、Data Contract、Model Monitoring、SRE、RAID | 事業戦略系フルセット     |
| クラウドネイティブ基盤 | SRE、SLI/SLO、GitOps、ADR、C4、RAID                          | マーケ系フレーム       |
| コンサル提案      | MECE、Issue Tree、SCQA、Pyramid、As-Is/To-Be                | 実装詳細フレーム       |
| 技術リード       | ADR、C4、DDD、Clean Architecture、SRE、CI/CD                 | コンサル資料系の過剰運用   |

つまり、**固定セットではなく、対象ごとにフレームワークの濃淡を変える**。

ここを生成AIに任せるのは合理的です。

---

## 4. 破綻条件

この黒澤流が壊れる条件は、主に5つです。

| 破綻条件                   | 内容                     |
| ---------------------- | ---------------------- |
| 生成AIに自由発明させる           | デファクトから外れて独自理論化する      |
| フレームワークを全部盛りする         | Project as Codeが重くなり死ぬ |
| 人間が判断基準を渡さない           | AIが一般論で組み合わせる          |
| 再利用資産がない               | 毎回ゼロから作り直しになる          |
| Project as Codeが更新されない | 実態と乖離して台帳化する           |

特に重要なのは、
**生成AIを「発明者」にしないこと**です。

生成AIの役割は、

> デファクトの選定、重み調整、削減、再構成、既存資産の再利用

であって、

> 俺様フレームワークの創造

ではないです。

---

## 5. 実務・行動への影響

黒澤流を Project as Code にするなら、最小構成はこれです。

```text
project-as-code/
  framework-stack.yaml        # 採用フレームワーク一覧と重み
  tailoring-policy.md         # 対象別に何を重く/軽くするか
  anti-cannibalism-rules.md   # 役割衝突を避けるルール
  templates/
    pmbok/
    wbs/
    raci/
    raid/
    adr/
    c4/
    sre/
    mlops/
    consulting/
  profiles/
    backend-lead.yaml
    mlops-pm.yaml
    cloud-native-consultant.yaml
    small-poc.yaml
  generated/
    current-project-plan.md
    current-raid-log.yaml
    current-responsibility-matrix.yaml
```

一番重要なのは `framework-stack.yaml` です。

```yaml
target: mlops_cloud_native_backend_pm
principle:
  originality_at_framework_layer: false
  use_de_facto_frameworks: true
  avoid_framework_cannibalism: true
  project_as_code_first: true
  ai_assisted_tailoring: true

frameworks:
  pmbok:
    role: project_management_language
    weight: high
  wbs:
    role: work_decomposition
    weight: high
  raci:
    role: responsibility_boundary
    weight: high
  raid:
    role: risk_issue_assumption_dependency_management
    weight: high
  adr:
    role: technical_decision_record
    weight: high
  c4:
    role: architecture_explanation
    weight: medium
  sre:
    role: reliability_operation
    weight: high
  mlops_lifecycle:
    role: model_data_operation_lifecycle
    weight: high
  mece:
    role: issue_structuring
    weight: medium
  pyramid_structure:
    role: executive_communication
    weight: medium

anti_cannibalism:
  raci_vs_daci: choose_one_primary
  okr_vs_kpi: separate_goal_and_metric
  mece_vs_issue_tree: mece_as_principle_issue_tree_as_artifact
  pmbok_vs_scrum: pmbok_as_management_language_scrum_as_delivery_method
  adr_vs_decision_log: adr_for_architecture_decision_log_for_business_pm_decision
```

黒澤流の強みは、ここです。

**人間は「目的・制約・判断基準・破綻条件」を握る。
生成AIは「組み合わせ・重み調整・削減・再利用」を支援する。
成果物はProject as Codeとして残し、次回以降の判断資産にする。**

これは、上流・PM・技術リード・MLOps・コンサルを横断するうえで、かなり強い型になります。
