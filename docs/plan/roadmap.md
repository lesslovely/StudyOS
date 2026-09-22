# StudyOS 长期路线图（Long-Term Roadmap）

> 层级：Level 1。本文只定义方向与阶段依赖，不展开具体任务。当前阶段的细节见各 [Phase 计划](README.md)（计划层级定义见 [计划文档的三个层级](README.md#计划文档的三个层级)）。
> 维护规则见 [maintenance.md](maintenance.md)，规划决策与变更原因见 [decisions.md](decisions.md)。

## 项目定位

StudyOS 是**以个人知识为核心、以学习闭环为基础、以 AI 为智能层、以用户自主决策为原则的 Personal Learning Operating System（个人学习操作系统）**。

它**不是**：普通 Todo、普通笔记软件、单纯知识库、在线课程平台、单纯 AI Chatbot。

## 核心学习闭环

StudyOS 的一切产品设计与阶段规划都服务于同一个循环：

```text
知识 → 学习 → 任务 → 学习记录 → 掌握度变化 → 发现薄弱点
                                              ↓
        新任务 ← 用户决定 ← AI 建议 ← AI 分析 ←┘
          ↓
         学习 ↺
```

两条不可动摇的原则：

1. **Task 是手段，Knowledge State（知识状态）的改变才是目标。** 任务完成本身不代表学会，掌握度与理解的变化才代表学会。
2. **AI 是 Advisor，不是 Controller。** AI 只产出建议，用户查看后选择接受 / 修改 / 拒绝，再执行；用户始终拥有最终决定权。

同一闭环在 [product-roadmap.md](product-roadmap.md#核心学习闭环) 与 [phase-01/README.md](phase-01/README.md#阶段目标) 中保持一致表述。Phase 1 用**简单规则**模拟“AI 分析 / 建议”两个环节，Phase 8 起由真实 LLM 承担，Phase 10 起 Agent 可在受控确认下执行操作。

## 规划原则

- **需求驱动技术**：每个技术都在真实痛点出现时引入，不为炫技堆叠（避免 Premature Engineering）。
- **先理解再抽象**：开发者必须理解自己写出的每一部分，不复制不理解的 AI 代码。
- **简单优先**：优先选择当前阶段能理解、能验证的最简单方案。
- **内容与状态分离**：知识内容（定义、理解、示例）与用户状态（掌握度、重点、学习状态）从第一天起分组建模，为未来后端 / 数据库 / 多用户演进留路，但不在 Phase 1 提前建表。
- **知识模板只是脚手架**：Template → Personal Knowledge → 用户修改 → 个人知识系统；StudyOS 不追求成为“完整语言知识数据库”。
- **层级 + 关系并存**：Hierarchy 负责归类，Relationship 负责连接；Phase 1 只做 parent / related / prerequisite，不做复杂知识图谱。
- **AI 角色固定**：Product Advisor、Architecture Advisor、Teacher、Code Reviewer、Debug Assistant、Research Assistant；不是全自动开发者。

## Phase 总览

| 阶段 | 核心目标 | 产品演进 | 技术演进 | 学习重点 | 主要产出 | 前置 |
| --- | --- | --- | --- | --- | --- | --- |
| [P0](phase-00/README.md) ✅ | 定方向、立计划系统 | 明确产品定位与边界 | 仅文档 | 需求分析、项目驱动学习、Git 文档习惯 | 计划网络（本目录） | — |
| [P1](phase-01/README.md) 🟨 | 跑通知识学习闭环 | 知识 CRUD、知识详情、关联任务、学习记录、规则建议、薄弱点 | HTML/CSS/JS、DOM、localStorage | JS 核心、DOM/Event、数据建模、状态、本地存储、基础模块化、Git | 可离线运行的学习闭环 MVP | P0 |
| [P2](phase-02/README.md) ⬜ | 前端可维护化 | 闭环体验组件化重建 | React、TypeScript、Vite | 组件、状态、类型、构建 | 组件化前端 | P1 |
| [P3](phase-03/README.md) ⬜ | 建立后端服务 | 知识 / 任务 / 记录 API 化 | HTTP、REST、FastAPI（临时存储） | HTTP、Python、FastAPI、API 设计 | 可调用的后端原型 | P2 |
| [P4](phase-04/README.md) ⬜ | 可靠持久化与关系 | 知识层级与关系落库 | SQL、PostgreSQL、ORM、迁移 | 数据建模、SQL、事务、关系 | 后端数据层 | P3 |
| [P5](phase-05/README.md) ⬜ | 全栈闭环 | 本地数据向服务端迁移、跨页面一致 | 前后端联调、异步状态、错误处理 | 数据流追踪、契约、校验 | 可长期使用的全栈版 | P4 |
| [P6](phase-06/README.md) ⬜ | 个人空间与隔离 | 账户、登录、按用户隔离数据 | 认证、授权、Session/Token | 密码安全、权限边界 | 多用户安全基线 | P5 |
| [P7](phase-07/README.md) ⬜ | 测评与多信号掌握度 | 单知识测试、关联知识综合测试 | 题库与测评引擎（规则为主） | 测评建模、统计、掌握度聚合 | 测评系统 | P6 |
| [P8](phase-08/README.md) ⬜ | 引入 AI Advisor | AI 分析、建议、解释理由（可接受/修改/拒绝） | LLM API、Prompt、结构化输出 | 上下文设计、输出校验、成本与安全 | AI 建议层 | P7 |
| [P9](phase-09/README.md) ⬜ | AI 基于个人知识回答 | 个人知识检索问答、缺口发现 | Embedding、向量库、RAG | 切分、检索、重排、RAG 评估 | 个人知识检索能力 | P8 |
| [P10](phase-10/README.md) ⬜ | 受控 Agent 工作流 | AI 查询状态、制定计划、确认后执行 | Tool Calling、Agent 工作流 | 工具定义、权限、确认门、审计 | 受控 AI Agent | P8、P9 |
| [P11](phase-11/README.md) ⬜ | 质量工程体系 | 核心流程有回归保护 | 测试金字塔、静态检查、Git 工作流 | 各类测试、可观测性 | 可安全迭代的代码库 | P10（实践自 P1 起） |
| [P12](phase-12/README.md) ⬜ | 交付上线 | 可访问、可维护的线上 StudyOS | Docker、Linux、Nginx、HTTPS | 容器、运维、发布回滚、备份监控 | 生产环境 | P11 |

## 阶段依赖图

主链是严格的能力依赖顺序；测试与 Git 是贯穿始终的横向实践，不是 P11 才开始：

```text
P0 计划系统
 └─> P1 闭环 MVP（Vanilla Web + localStorage）
      └─> P2 前端工程化（React + TS）
           └─> P3 后端服务（FastAPI，临时存储）
                └─> P4 数据库（PostgreSQL，知识层级/关系建模）
                     └─> P5 全栈集成
                          └─> P6 用户与认证
                               └─> P7 测评系统（多信号掌握度）
                                    └─> P8 AI Advisor（LLM）
                                         ├─> P9 RAG（依赖 P8 的生成能力 + 自 P1 积累的知识语料）
                                         └─> P10 Agent（依赖 P8/P9，写操作必须用户确认）
                                              └─> P11 质量工程（系统化测试；手动验证自 P1 开始）
                                                   └─> P12 容器化与生产部署
                                                        └─> Horizon（未锁定，见下）

横向贯穿（不单独占阶段）：
  Git 与提交习惯        ：P0/P1 起步，逐阶段加强
  手动验证 / 调试       ：P1 起步
  自动化测试            ：具备模块基础后尽早引入，P11 体系化
  数据模型演进意识       ：P1 分组对象 → P4 关系表 → P9 向量索引
```

关键依赖说明：

- **P7 测评位于 AI 之前**：AI 建议质量依赖结构化的掌握度信号；先用规则化测评建立信号，再让 LLM 消费这些信号，避免“让 AI 在没有数据时空谈分析”。
- **P8 → P9 → P10 不可颠倒**：RAG 的生成环节依赖 LLM 基础；Agent 的检索 / 问答能力依赖 RAG。
- **P12 合并了旧计划的 Docker 与部署两个阶段**：容器化的唯一目的就是一致地交付，二者对单人学习项目是一条连续链路，在 [phase-12](phase-12/README.md) 内分两个里程碑。
- 阶段可因真实需求插入前置知识，但必须在 [decisions.md](decisions.md) 说明原因，不能跳过理解直接堆技术。

## 可追溯关系（Traceability）

每个 Phase 都必须能沿双向链接完成以下导航：

```text
roadmap.md（总路线）
  ↕
phase-XX/README.md（阶段计划）
  ├─ 产品目标 → product-roadmap.md
  ├─ 技术目标 → architecture-roadmap.md
  ├─ 学习目标 → learning-roadmap.md
  ├─ 前置阶段 → phase-(XX-1)/README.md
  ├─ 后续阶段 → phase-(XX+1)/README.md
  └─ 详细任务 → phase-XX/plan.md（仅进入该阶段时创建）
```

链接表达**结构关系**，不是装饰；没有真实关系的内容不建立链接。链接规范与检查清单见 [maintenance.md](maintenance.md#链接规范)。

## 未来演进方向（Horizon）

以下方向已被识别但**未锁定、不编号、不承诺顺序**，在对应前置能力成熟、且出现真实需求时再提升为正式 Phase：

- **间隔重复（Spaced Repetition）**：基于学习记录与掌握度衰减安排复习。
- **高级测评**：编程题自动判题、Debug 题、场景分析、知识迁移、AI 对话式测评。
- **掌握度多信号融合**：自评、测试、实践、AI 对话、历史趋势的加权模型（Phase 1 仅自评，不假装系统能准确判断能力）。
- **知识图谱成熟化**：depends-on / contrast / application / 自定义关系；在关系型查询被证明不够用之前，不引入图数据库。
- **知识模板生态**：模板导入导出、AI 生成模板骨架。
- **高级分析与学习趋势**：Learning History → Trend → Analysis。
- **多设备 / PWA / 移动端**、**多人协作**（StudyOS 默认坚持个人单用户定位）。

## 当前状态与下一步

- 已完成：Phase 0（项目定义）与 2026-09-17 计划系统整合；Phase 1 的 M0 基线（提交 `61e6ddb`）。
- 进行中：Phase 1（2026-09-19 进入，[D-012](decisions.md)、[D-013](decisions.md)）。M1 数据与存储的 Level 3 计划已生成（[phase-01/plan.md](phase-01/plan.md)），待开发者确认后开始编码；M2–M7 不提前展开。
- 仓库现状：`src/` 仅有空脚手架，无业务代码；M1 完成前不写任何 UI。
