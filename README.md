# StudyOS

Personal Learning Operating System（个人学习操作系统）

> **项目状态：Phase 1 进行中（M0 基线已完成，M1 数据与存储计划就绪、代码未开始）；当前无业务代码。**

## 项目定位

StudyOS 是**以个人知识为核心、以学习闭环为基础、以 AI 为智能层、以用户自主决策为原则**的 Personal Learning Operating System。

它**不是**普通 Todo、笔记软件、单纯知识库、在线课程平台或 AI Chatbot。

核心学习闭环：

```text
知识 → 学习 → 任务 → 学习记录 → 掌握度变化 → 发现薄弱点
                                              ↓
        新任务 ← 用户决定 ← AI 建议 ← AI 分析 ←┘
          ↓
         学习 ↺
```

- **Task 是手段，Knowledge State 的改变才是目标。**
- **AI 是 Advisor，不是 Controller**：建议 → 用户查看 → 接受 / 修改 / 拒绝 → 执行。

## 文档导航

完整的产品 / 技术 / 学习规划与 Phase 计划都在计划系统中：

- **[docs/plan/README.md](docs/plan/README.md)** —— 计划系统总入口（建议从这里开始）
- [长期路线图](docs/plan/roadmap.md) · [产品路线图](docs/plan/product-roadmap.md) · [技术架构路线图](docs/plan/architecture-roadmap.md) · [学习路线图](docs/plan/learning-roadmap.md)
- [计划维护规则](docs/plan/maintenance.md) · [规划决策与变更日志](docs/plan/decisions.md)
- [历史计划归档](docs/plan/archive/README.md)

## 项目驱动学习

```text
项目需求 → 发现问题 → 学习对应知识 → 应用到项目 → 测试与验证 → 继续迭代
```

技术由真实需求推动，按依赖顺序逐步引入：Vanilla Web（P1）→ 前端工程化（P2）→ 后端 API（P3）→ 数据库（P4）→ 全栈集成（P5）→ 认证（P6）→ 测评（P7）→ AI Advisor（P8）→ RAG（P9）→ Agent（P10）→ 质量工程（P11）→ 容器化与部署（P12）。详见[技术架构路线图](docs/plan/architecture-roadmap.md)与[学习路线图](docs/plan/learning-roadmap.md)。

## 项目原则

1. **Incremental Development**：逐阶段开发，不一次性实现所有内容。
2. **Learn by Building**：通过真实需求学习技术。
3. **Keep It Simple**：优先简单、清晰、可理解的设计。
4. **Avoid Premature Engineering**：不提前引入没有实际需求的复杂技术。
5. **Understand Before Abstraction**：先理解，再抽象；开发者必须理解写出的每一部分。
6. **AI as Advisor**：AI 负责解释、Review、Debug、建议与教学，不做全自动代写者；用户始终拥有决定权。

## 当前状态与边界

```text
Phase 0 项目定义与计划系统：✅ 已完成
Phase 1 知识学习闭环 MVP：🟨 进行中（M0 ✅，M1 数据与存储待开始）
Phase 2–12：⬜ 规划中
代码：src/ 仅有空脚手架，无业务代码
```

Phase 1 按[进入 Phase 标准流程](docs/plan/maintenance.md#进入-phase-的标准流程)推进：M1 详细任务计划见 [phase-01/plan.md](docs/plan/phase-01/plan.md)，确认后才开始编码；M1 只做数据与存储，不写 UI。

## 仓库结构

```text
StudyOS/
├── docs/
│   └── plan/            # 计划系统（路线图、Phase 计划、维护规则、决策记录、归档）
├── src/                 # Phase 1 的家园（空脚手架；P2 起演进为前端工程结构）
│   ├── index.html
│   ├── css/
│   └── js/
└── README.md
```

> 未来的 backend / 数据库 / docker-compose 等结构在对应 Phase 真实需要时才创建，不提前建目录。
