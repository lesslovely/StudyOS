# StudyOS 技术架构路线图（Architecture Roadmap）

> 层级：Level 1 的技术视角。回答“架构与数据模型按什么依赖关系演进、每个技术为什么在这个阶段引入”。
> 总路线见 [roadmap.md](roadmap.md)，产品能力见 [product-roadmap.md](product-roadmap.md)，对应要学的技术见 [learning-roadmap.md](learning-roadmap.md)。

## 技术演进总逻辑

```text
浏览器原生单体（P1）
  → 组件化前端（P2）
    → 后端服务 / API（P3）
      → 关系型持久化（P4）
        → 全栈集成（P5）
          → 认证与数据隔离（P6）
            → 测评引擎（P7）
              → AI 服务层（P8）
                → 检索增强层 RAG（P9）
                  → Agent 编排层（P10）
                    → 质量工程（P11）
                      → 容器化与生产部署（P12）
```

每一步只解决上一步真实暴露的问题：

| 阶段 | 触发引入的真实痛点 | 引入的技术 | 明确不引入 |
| --- | --- | --- | --- |
| [P1](phase-01/README.md) | 先验证闭环是否成立 | HTML/CSS/JS、DOM API、localStorage、JSON、基础模块化（无构建工具） | 框架、TS、npm、后端、数据库、UI 库 |
| [P2](phase-02/README.md) | DOM 操作重复、状态分散、复用困难 | React、TypeScript、Vite | 后端、复杂状态库、过早抽象 |
| [P3](phase-03/README.md) | 本地数据无法跨设备 / 共享 / 集中处理 | HTTP、REST、Python、FastAPI（临时内存存储） | 数据库、部署、锁框架版本 |
| [P4](phase-04/README.md) | 临时存储不可靠，知识层级 / 关系需要结构化表达 | SQL、PostgreSQL、ORM、迁移 | 缓存、分布式、微服务、图数据库 |
| [P5](phase-05/README.md) | 分层建立后必须验证真实数据流协作 | API 客户端、异步状态、错误 / 空 / 加载态 | 微服务、复杂缓存、状态框架 |
| [P6](phase-06/README.md) | 个人数据需要身份与隔离 | 注册登录、Session/Token、密码哈希、归属校验 | 企业级身份、SSO、复杂权限 |
| [P7](phase-07/README.md) | 自评不足以判断掌握度，需要结构化测评 | 题库 / 试卷 / 作答数据模型、评分与掌握度聚合（规则） | AI 自动判题（留给 P8+） |
| [P8](phase-08/README.md) | 有了记录与测评数据，需要智能分析建议 | LLM API、Prompt、结构化输出、AI 服务模块 | RAG、Agent、无确认写操作 |
| [P9](phase-09/README.md) | 模型不掌握用户长期积累的个人知识 | Embedding、向量存储（pgvector 或独立向量库，届时再定）、检索 / 重排 / 上下文组装 | Agent、锁定向量库厂商 |
| [P10](phase-10/README.md) | 问答不够，需要跨工具多步工作流 | Tool Calling、工具注册、确认门、审计日志、失败恢复 | 无限制数据库 / 系统权限、无人值守写操作 |
| [P11](phase-11/README.md) | 系统复杂后手动验证无法防回归 | 单元 / 集成 / E2E / API 测试、静态检查、格式化、Git 工作流 | 为覆盖率而测、复杂 CI 平台 |
| [P12](phase-12/README.md) | 多服务需要一致环境并真实交付 | Docker、Compose、Linux、Nginx、HTTPS、日志、备份、监控 | Kubernetes、平台工程 |

不提前锁定具体框架版本、模型、向量数据库、云厂商与 Agent 工具；进入对应 Phase 时按当时需求选择并记入 [decisions.md](decisions.md)。

## Phase 1 架构基线

P1 是**纯浏览器原生单体**，技术目的是让开发者理解 Web 应用的本质（结构 / 表现 / 行为 / 状态 / 持久化），而不是尽快上框架。

```text
src/
├── index.html          # 页面结构（语义化 HTML）
├── css/                # 样式（布局、响应式）
└── js/                 # 行为与数据（按职责分文件的基础模块化，<script> 引入）
    ├── store 概念      # localStorage 读写、JSON 序列化、schema 版本号
    ├── model 概念      # Knowledge / Task / LearningRecord 的创建与校验
    ├── rules 概念      # 规则建议引擎（未来 AI 层的占位与接缝）
    └── view 概念       # DOM 渲染、事件、视图切换、数据与 UI 同步
```

> 上面是**职责划分示意，不是 P1 的最终文件清单**；实际文件在进入 Phase 1 生成 plan.md 时确定，且必须保持初学者能完全理解。

**localStorage 键规划（概念级）**：`studyos:knowledge`、`studyos:tasks`、`studyos:records`、`studyos:meta`（含 schema version，用于体验最简单的数据迁移思想）。

**P1 必须预留的两个“演进接缝”（只是代码职责边界，不允许写抽象层）**：

1. **存储接缝**：所有读写经过同一组 store 函数，P2/P3 只替换这一层，视图代码不直接碰 localStorage。
2. **建议接缝**：规则引擎是独立的纯函数模块（输入知识状态，输出建议 + 理由），P8 用 AI 服务替换其内部实现，交互流程不变。

## 数据模型演进

P1 即按“内容 / 状态 / 关系 / 学习数据”四组**分组建模**（存在同一对象中即可，不提前规范化），为后续拆分留路：

```text
P1 localStorage 对象（分组但不拆表）
  KnowledgeNode { 基本信息, Content, UserState, 关系引用[], 学习数据引用[] }
        │
        ├─ P4 PostgreSQL：内容与状态拆表，层级用 parent_id，关系进 relations 表
        │     knowledge_nodes / node_contents / relations / tasks / learning_records
        │
        ├─ P6：所有业务表加 user_id 归属，查询强制隔离
        │
        ├─ P7：questions / assessments / attempts / mastery_events
        │     掌握度 = 自评 + 作答结果的规则聚合
        │
        └─ P9：知识内容与资料生成 embeddings，进入向量索引（与关系库并存，不替代）
```

关系基数在 P1 保持克制：`parent`（树形归属）、`related`（互相关联）、`prerequisite`（前置）。未来扩展 `depends-on / contrast / application / 自定义关系`，但不提前设计。在关系型查询被证明不够用之前，不引入图数据库。

## 架构安全边界（随阶段生效）

- **P1–P5**：无认证，默认单用户本地 / 自用；输入校验与 XSS 基础意识从 P1 DOM 渲染开始建立（不使用不安全的 HTML 拼接插入用户内容）。
- **P6**：密码哈希存储、凭证校验、按归属过滤查询；不自己发明密码方案。
- **P8**：AI 输出必须校验与降级处理；建议作为 **proposal（提案）** 持久化，用户接受 / 修改 / 拒绝后才影响业务数据；密钥不进前端、不进仓库。
- **P9**：检索遵守用户数据权限；RAG 回答带出处。
- **P10**：工具分读写权限；写操作走确认门；关键操作可审计、可回滚；Agent 永不获得无限制数据库或系统权限。

## 横向工程实践（不等到 P11）

| 实践 | 起步阶段 |
| --- | --- |
| Git 初始化、语义化提交、每里程碑一个提交节点 | P0/P1 |
| 手动验证清单、控制台与断点调试 | P1 |
| 模块化与可独立测试的纯函数 | P1（store / rules） |
| 类型约束、构建流程 | P2 |
| 接口契约与错误码约定 | P3 |
| 数据迁移脚本 | P4 |
| 自动化测试（先核心纯函数 / API，再 UI） | 具备模块基础后尽早，P11 体系化 |
| 配置与密钥管理 | P3 起步，P6/P8 加强 |
| 容器化、CI、日志监控、备份 | P11/P12 |

## 当前架构状态

- 代码：`src/index.html` 为空脚手架，`src/css`、`src/js` 仅占位；无依赖、无构建工具、无后端。
- 下一步：等待“进入 Phase 1”指令，按 [maintenance.md](maintenance.md#进入-phase-的标准流程) 产出 Level 3 计划后再动代码。
