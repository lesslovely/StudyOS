# StudyOS 计划系统（Plan Network）

这里是 StudyOS 长期开发与学习规划的唯一入口。计划不是一次性文档，而是随项目演进持续更新的 **Living Roadmap**：总计划定义方向，Phase 计划负责当前阶段，实际开发结果反过来修正总计划。

> 当前状态：**计划系统已建立，Phase 0 已完成，Phase 1 待进入。尚未编写任何业务代码。**

## 文档导航

### Level 1 — 长期路线（回答“StudyOS 最终发展到哪里”）

| 文档 | 回答的问题 |
| --- | --- |
| [roadmap.md](roadmap.md) | 总路线：Phase 总览、阶段依赖、核心闭环、可追溯关系 |
| [product-roadmap.md](product-roadmap.md) | 产品路线：能力如何逐步演进，用户价值如何增长 |
| [architecture-roadmap.md](architecture-roadmap.md) | 技术路线：架构与数据模型如何按真实依赖演进 |
| [learning-roadmap.md](learning-roadmap.md) | 学习路线：开发者能力如何随 Phase 成长，如何验证学会 |

### Level 2 — Phase 计划（回答“这个阶段怎么完成”）

| 阶段 | 主题 | 状态 |
| --- | --- | --- |
| [phase-00](phase-00/README.md) | 项目定义与计划系统 | ✅ 已完成 |
| [phase-01](phase-01/README.md) | 知识学习闭环 MVP（HTML + CSS + JavaScript + localStorage） | ⬜ 待进入 |
| [phase-02](phase-02/README.md) | 前端工程化（React + TypeScript + Vite） | ⬜ 规划中 |
| [phase-03](phase-03/README.md) | 后端服务（HTTP + FastAPI + REST API） | ⬜ 规划中 |
| [phase-04](phase-04/README.md) | 数据库与关系建模（SQL + PostgreSQL + ORM） | ⬜ 规划中 |
| [phase-05](phase-05/README.md) | 全栈集成 | ⬜ 规划中 |
| [phase-06](phase-06/README.md) | 用户系统与认证 | ⬜ 规划中 |
| [phase-07](phase-07/README.md) | 测评系统与多信号掌握度 | ⬜ 规划中 |
| [phase-08](phase-08/README.md) | AI Advisor（LLM 集成） | ⬜ 规划中 |
| [phase-09](phase-09/README.md) | 个人知识检索（Embedding + RAG） | ⬜ 规划中 |
| [phase-10](phase-10/README.md) | AI Agent（受控 Tool Calling） | ⬜ 规划中 |
| [phase-11](phase-11/README.md) | 质量工程（测试与工程化） | ⬜ 规划中 |
| [phase-12](phase-12/README.md) | 容器化与生产部署（Docker + Linux + Nginx + HTTPS） | ⬜ 规划中 |

> Phase 12 之后的未锁定方向（间隔重复、高级分析、成熟知识图谱、自适应学习等）见 [roadmap.md](roadmap.md#未来演进方向horizon)。

### 规则与记录

| 文档 | 内容 |
| --- | --- |
| [maintenance.md](maintenance.md) | 计划维护规则：进入 Phase 的标准流程、更新时机、链接规范、反模式清单 |
| [decisions.md](decisions.md) | 规划决策与变更日志：旧计划整合结论、冲突裁决、编号映射、待确认问题 |
| [archive/](archive/README.md) | 2026-09-17 整合前的历史计划，只读保留 |

## 状态图例

- ⬜ 未开始 / 规划中
- 🟨 进行中
- ✅ 已完成
- 🚧 已进入但受阻（需在对应 Phase 文档记录阻塞原因）

## 怎么使用这套计划

1. **想了解全局** → 从 [roadmap.md](roadmap.md) 开始，再按兴趣进入产品 / 技术 / 学习三条路线。
2. **准备开始一个阶段** → 必须按 [maintenance.md](maintenance.md#进入-phase-的标准流程) 的标准流程执行：重读总路线、检查代码与能力、更新 Phase 计划、生成 Level 3 详细计划、等待确认，再开发。
3. **计划与现实冲突时** → 不将就地执行旧计划，也不悄悄改方向；先记录到 [decisions.md](decisions.md)，再更新相关文档与双向链接。
4. **想了解为什么这么规划** → 查 [decisions.md](decisions.md) 中对应决策编号。

## 计划文档的三个层级

```text
Level 1  Long-Term Roadmap（本目录顶层四份路线文档）
            只写方向：Phase、核心目标、演进、产出、前置与后续
   ↓
Level 2  Phase Plan（phase-XX/README.md）
            写清当前阶段：目标、范围、数据模型、页面/模块规划、里程碑、验证标准
   ↓
Level 3  Task Plan（phase-XX/plan.md，进入该阶段时才创建）
            才拆具体任务：页面 → 模块 → DOM/事件 → 数据 → 存储
```

当前只维护 Level 1 和 **Phase 1 的 Level 2 计划**；其他 Phase 保持高层规划，不提前展开任务细节。
