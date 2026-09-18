# 历史计划归档（Archive）

本目录保存 StudyOS 在 **2026-09-17 计划系统整合之前** 的原始规划文档，作为历史基础保留，不再维护、不再代表当前计划。

- 归档方式：`git mv`（Git 历史完整保留，可随时追溯每次变更）。
- 当前有效计划请回到计划系统入口：[../README.md](../README.md)。
- 整合时发现的冲突、重复、过时内容及处理结论，见 [../decisions.md](../decisions.md)。

## 归档文件

| 历史文件 | 当时内容 |
| --- | --- |
| [PLAN.md](PLAN.md) | 旧版全局路线图（Phase 0–12，以记录 / 任务 / 项目为核心） |
| [PHASE-00.md](PHASE-00.md) ~ [PHASE-12.md](PHASE-00.md) | 旧版各阶段计划 |

## 新旧 Phase 编号映射

> 注意：整合后阶段编号发生变化，引用旧文档时务必对照本表，不要按编号直接对应。

| 旧计划 | 新计划 | 关系 |
| --- | --- | --- |
| PHASE-00 项目定义 | [phase-00](../phase-00/README.md) | 保留，刷新为“项目定义 + 计划系统” |
| PHASE-01 前端 MVP（记录/任务/项目/Dashboard） | [phase-01](../phase-01/README.md) | **范围重定义**：知识学习闭环 MVP（Knowledge 为核心） |
| PHASE-02 React + TypeScript | [phase-02](../phase-02/README.md) | 保留，围绕知识实体重构 |
| PHASE-03 HTTP + FastAPI | [phase-03](../phase-03/README.md) | 保留，资源对象改为知识 / 任务 / 记录 |
| PHASE-04 PostgreSQL | [phase-04](../phase-04/README.md) | 保留，增加知识层级与关系建模 |
| PHASE-05 前后端集成 | [phase-05](../phase-05/README.md) | 保留 |
| PHASE-06 用户系统 | [phase-06](../phase-06/README.md) | 保留 |
| —（不存在） | [phase-07](../phase-07/README.md) | **新增**：测评系统与多信号掌握度 |
| PHASE-07 LLM / AI | [phase-08](../phase-08/README.md) | 后移一位，定位为 AI Advisor |
| PHASE-08 RAG | [phase-09](../phase-09/README.md) | 后移一位，围绕个人知识检索重构 |
| PHASE-09 Agent | [phase-10](../phase-10/README.md) | 后移一位，强化“受控工具 + 用户确认” |
| PHASE-10 测试与工程化 | [phase-11](../phase-11/README.md) | 后移一位；测试与 Git 改为从 Phase 1 起的横向实践 |
| PHASE-11 Docker + PHASE-12 部署 | [phase-12](../phase-12/README.md) | **合并**：容器化与生产部署 |
| 根 README 中的 Roadmap 章节 | [../roadmap.md](../roadmap.md) | 拆分到四条路线文档，根 README 只做入口 |

## 阅读建议

旧文档的写作结构（阶段目标 / 为什么学习 / 核心知识 / 核心功能 / 技术范围 / 验收方向 / 阶段关系）仍然有效，新版 Phase 计划继承了这一结构。阅读旧文档时请以上表中的新计划为准。
