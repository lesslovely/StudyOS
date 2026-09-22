# Phase 1 · Level 3 任务计划 — M1 数据与存储

> 本文件是 Phase 1 的 Level 3 计划（层级说明见 [../README.md](../README.md)）。**当前只拆解 M1**；M2–M7 在进入对应里程碑时再按 [maintenance.md 进入流程](../maintenance.md#进入-phase-的标准流程)展开，不提前细化。
>
> **导航**：[Phase 1 总计划](README.md) · [手动验证清单](manual-checklist.md) · [总路线](../roadmap.md) · [产品路线](../product-roadmap.md) · [技术路线](../architecture-roadmap.md) · [学习路线](../learning-roadmap.md) · [决策记录](../decisions.md)

## 当前状态

| 项 | 状态 |
| --- | --- |
| Phase 1 | 🟨 进行中（2026-09-19 进入，依据 [D-012](../decisions.md)） |
| M0 基线 | ✅ 完成（提交 `61e6ddb`，[手动验证清单](manual-checklist.md)已补齐） |
| M1 数据与存储 | ⬜ 待开始（本计划待开发者确认后动手） |
| M2–M7 | ⬜ 未展开，里程碑级计划见 [README.md 开发顺序](README.md#开发顺序里程碑level-2) |
| 分支 | `feature/knowledge`（[D-013](../decisions.md)） |

## M1 目标（固定，不扩张）

做出四类对象的数据结构与统一存储层，让 StudyOS 的数据在浏览器中可写入、可持久化、刷新可恢复，并自带一份最小示例知识集。**M1 没有界面**，验证全部在浏览器控制台完成；`index.html` 的 `<body>` 保持空白，只允许通过 `<script>` 引入 js 文件以支持控制台验证。

- 四类对象结构：KnowledgeNode / Relation / Task / LearningRecord
- store 统一读写 + JSON 序列化 + schema 版本
- 最小示例知识集（seed）：JavaScript / 函数 / 作用域 / 闭包
- 验收原文：控制台可读写数据，刷新后数据恢复（[README.md M1 行](README.md#开发顺序里程碑level-2)）

## M1 前置决策（已确认，不再讨论）

依据 [D-012](../decisions.md)：

1. seed = 4 节点 + 1 条前置关系（见下“种子数据规格”）。
2. status 枚举：`未学习 / 学习中 / 复习中 / 已掌握`，默认 `未学习`。
3. mastery 范围 1~100，seed 默认 0（未评）；mastery 与 status 是两个独立字段，互不推导。
4. 三视图不阻塞 M1；掌握度控件形态不阻塞 M1（M4 再定）。

## T1 产出：数据契约（本文件即契约，确认后冻结）

> 字段设计继承 [README.md 数据模型](README.md)，此处是 M1 实现的唯一依据。M1 不做的字段不删除，按默认值预留，保证后续里程碑无需迁移结构（schema version 仍为 1）。

### KnowledgeNode（知识节点）

| 分组 | 字段 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- | --- |
| 基本信息 | id | string | 工厂生成 | `k_` 前缀 |
| 基本信息 | title | string | 必填 | 知识名称 |
| 基本信息 | domain | string | 必填 | 所属领域，如 `JavaScript` |
| 基本信息 | parentId | string \| null | null | 层级归属；根领域为 null |
| 基本信息 | description | string | `''` | 一句话描述 |
| Content | definition | string | `''` | 定义 |
| Content | myUnderstanding | string | `''` | 我的理解 |
| Content | examples | string[] | `[]` | 示例 |
| Content | useCases | string | `''` | 使用场景（M1 预留文本字段） |
| Content | commonMistakes | string[] | `[]` | 常见错误 |
| Content | questions | string[] | `[]` | 疑问 |
| Content | references | string[] | `[]` | 学习资料 |
| UserState | mastery | number | 0 | 0~100 整数；0 = 未评 |
| UserState | starred | boolean | false | 重点标记，与 mastery 独立 |
| UserState | status | enum | `未学习` | 未学习 / 学习中 / 复习中 / 已掌握 |
| Learning Data | taskIds | string[] | `[]` | 关联任务 id（见下方“引用一致性”） |
| Learning Data | recordIds | string[] | `[]` | 关联记录 id |
| 元信息 | createdAt | string | 工厂生成 | ISO 时间字符串 |
| 元信息 | updatedAt | string | 工厂生成 | ISO 时间字符串 |

### Relation（知识关系，独立存储）

| 字段 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| id | string | 工厂生成 | `rel_` 前缀 |
| sourceId | string | 必填 | 关系起点知识 id |
| targetId | string | 必填 | 关系终点知识 id |
| type | enum | 必填 | M1 仅 `related` / `prerequisite`；层级关系用 parentId，不写进 Relation（[D-009](../decisions.md)） |
| createdAt | string | 工厂生成 | ISO 时间字符串 |

### Task（任务）

| 字段 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| id | string | 工厂生成 | `t_` 前缀 |
| title | string | 必填 | 任务标题 |
| note | string | `''` | 备注 |
| knowledgeId | string | **必填，工厂强制校验** | 不允许无知识归属的任务（闭环红线） |
| status | enum | `todo` | `todo` / `done` |
| createdAt | string | 工厂生成 | |
| completedAt | string \| null | null | 完成时填写 |

### LearningRecord（学习记录）

| 字段 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| id | string | 工厂生成 | `rec_` 前缀 |
| timestamp | string | 工厂生成 | 行为发生时间 |
| knowledgeId | string | 必填 | 关联知识 |
| taskId | string \| null | null | 来源任务；自评等手动行为为空 |
| behavior | enum | 必填 | 完成任务 / 学习 / 练习 / 自评 / 复习 |
| result | string | `''` | 结果备注，可空 |
| masteryBefore | number | 必填 | 变化前掌握度，允许与 after 相等 |
| masteryAfter | number | 必填 | 变化后掌握度 |

### 引用一致性规则

- Task 与 LearningRecord 自身持有 knowledgeId / taskId，是关系的**事实来源**；KnowledgeNode.taskIds / recordIds 是方便读取的缓存数组，由创建任务 / 记录时同步维护。
- M5 若发现缓存数组可完全由查询派生，按 [maintenance.md 变更流程](../maintenance.md)决定是否移除，不在 M1 提前优化。

### 存储布局（localStorage）

| 键 | 内容 |
| --- | --- |
| `studyos:knowledge` | KnowledgeNode 数组的 JSON 字符串 |
| `studyos:relations` | Relation 数组 |
| `studyos:tasks` | Task 数组 |
| `studyos:records` | LearningRecord 数组 |
| `studyos:meta` | 元信息对象：`schemaVersion`（M1 = `1`）、`seeded`（布尔）、`updatedAt` |

约束：

- 所有数据必须是 JSON 可序列化的（无函数、无 undefined 字段值）。
- 任何模块读写 localStorage 必须经过 store；视图与工厂不得直接访问 localStorage（存储接缝，P3/P4 后端化时整体替换，见[技术路线 Phase 1 架构基线](../architecture-roadmap.md#phase-1-架构基线)）。
- ID 规则：类型前缀（`k_` / `rel_` / `t_` / `rec_`）+ 时间戳的 36 进制 + 短随机串，保证同毫秒不冲突；具体实现由开发者在 T3 亲手写并能解释。

### 种子数据规格（seed）

层级（parentId）：

```text
JavaScript（领域根，parentId = null）
├── 函数
│   └── 闭包
└── 作用域
```

关系（独立存储，1 条）：闭包 `prerequisite` 作用域。

所有种子节点 mastery = 0、status = `未学习`、starred = false、Content 字段为空；仅 title / domain / parentId 有值。

初始化规则：仅当 `studyos:knowledge` 无数据且 `meta.seeded !== true` 时写入；写入后置 `seeded = true`。重复加载、已有用户数据时绝不重写。

## 建议文件组织（M1 结束时的状态）

按职责最小拆分，不提前建框架（[README.md 风险与反模式](README.md#风险与反模式本阶段重点防范)）：

| 文件 | 职责 | 对应任务 |
| --- | --- | --- |
| `src/js/store.js` | 五个键的读写、JSON 序列化、异常回退、meta | T2 |
| `src/js/model.js` | 四类对象工厂、默认值、必填与枚举校验、ID 生成 | T3 |
| `src/js/seed.js` | 种子数据与幂等初始化 | T4 |
| `src/js/main.js` | 启动入口：初始化 store → 必要时 seed；M1 不做渲染 | T4 |
| `src/index.html` | 仅增加对上述脚本的 `<script>` 引用，body 保持空白 | T4 |

## M1 任务列表

### T1 数据契约定稿（不写代码）

- **学习目标**：JS 数据类型（原始值 / 对象 / 数组）、对象结构设计、JSON 可序列化约束、单一事实来源思想。
- **实现目标**：阅读并确认本文件全部契约表（字段、类型、默认值、枚举、存储键、ID 规则、seed 规格）；有异议在动手前提出并走决策记录。
- **验证方式**：开发者能不看文档复述四类对象的字段分组与两条关系（parentId 层级 / Relation 关系）；AI 就“为什么 Content 与 UserState 分组”“为什么 taskIds 是缓存”提问通过。
- **产出**：契约冻结（开发者在对话中确认即完成）。

### T2 store 存储层

- **学习目标**：localStorage API 与同步存储特性、`JSON.stringify` / `JSON.parse`、存储容量与异常、try/catch 错误处理、模块职责边界。
- **实现目标**：实现 `store.js`：五个键的读取与保存、JSON 序列化与解析、读取到非法 JSON 时安全回退为空集合并给出可理解提示、meta 中 schemaVersion 的读写；除 store 外任何文件不得出现 localStorage 调用。
- **验证方式**：[manual-checklist.md](manual-checklist.md) M1 第 2–6 项全部勾选；控制台演示“写入 → 刷新 → 读回一致”和“篡改 JSON 不白屏”。
- **产出**：`src/js/store.js`。

### T3 对象工厂与校验

- **学习目标**：函数（参数、返回值）、对象创建与默认值、Date 与时间字符串、ID 生成、输入校验思想。
- **实现目标**：实现 `model.js`：四类对象的工厂函数，自动生成 id 与时间戳、填好默认值；枚举值非法时拒绝；**Task 工厂在缺少 knowledgeId 时必须报错**。
- **验证方式**：清单 M1 第 1、7、8 项；控制台逐一创建四类对象检查字段完整、默认值正确；故意缺 knowledgeId 创建任务被拒绝。
- **产出**：`src/js/model.js`。

### T4 种子数据与初始化

- **学习目标**：层级建模（parentId 与 domain 的配合）、层级与关系的区别、初始化幂等概念、脚本加载顺序。
- **实现目标**：实现 `seed.js`（按种子数据规格用工厂创建 4 节点 + 1 关系）与 `main.js`（启动时检查、仅空库写入、置 seeded 标记）；在 `index.html` 中以 `<script>` 按依赖顺序引入，body 不增加任何界面元素。
- **验证方式**：清单 M1 第 9、10 项；清空存储后刷新得到 4 节点与关系；再次刷新数量不变；手动写入一条数据后刷新不被覆盖。
- **产出**：`src/js/seed.js`、`src/js/main.js`、`index.html` 脚本引用。

### T5 M1 验证、Review 门与提交

- **学习目标**：手动验证纪律、Git 暂存与提交、提交信息规范。
- **实现目标**：完整跑一遍清单 M1 全部项目；走 Review 门（开发者自述实现 → AI 原理提问 → AI Review diff → **开发者本人修复** → 重跑清单）；由开发者本人执行 git add / commit（AI 不代提交）。
- **验证方式**：清单 M1 全绿；提交存在且工作区干净；提交信息建议：`phase-1: m1 data model, localStorage store and seed knowledge`。
- **产出**：M1 提交（留在 `feature/knowledge`）。

## M1 完成定义（DoD）

1. [manual-checklist.md](manual-checklist.md) M1 小节全部勾选；
2. 控制台可演示读写、刷新恢复、损坏回退、seed 幂等四件事；
3. Review 门走完，修复由开发者本人完成；
4. 一个表达清晰的 M1 提交；
5. 未引入禁止清单中的任何技术（无框架、无依赖、无后端、无 AI API）；
6. 页面无 UI 提前实现（M2 才开始 DOM 渲染）。

## M2–M7（不展开）

里程碑级目标与验收见 [README.md 开发顺序表](README.md#开发顺序里程碑level-2)。进入下一里程碑时：重读该表与本阶段实际代码 → 更新本文件（追加 M2 小节）→ 确认后动手。已知的两个待确认时点：M2 进入时确认三视图（[D-012](../decisions.md)），M4 进入时确认掌握度控件形态。

## M1 风险提示

- 在视图 / seed 里直接读写 localStorage，绕过 store——会堵死 P3/P4 的存储替换，Review 直接打回。
- seed 不做幂等导致每次刷新重复写入。
- 提前写 DOM 渲染 / 样式（M2 的内容），让 M1 失焦。
- 工厂不校验 knowledgeId，埋下“无主任务”隐患（闭环红线）。
- 数据里放函数等不可序列化内容，刷新后静默丢失。

## 变更记录

- 2026-09-19：进入 Phase 1，创建本文件，仅拆解 M1；决策依据 [D-012](../decisions.md)、[D-013](../decisions.md)。
