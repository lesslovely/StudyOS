# StudyOS 全局路线图

## 项目愿景

StudyOS 是一个个人学习与知识管理系统，也是项目驱动式软件工程学习主线。目标不是尽快堆叠技术，而是在真实需求中逐步形成独立分析、设计、开发、调试、测试、部署和维护全栈 AI 应用的能力。

## 学习目标

通过 StudyOS 逐步连接 HTML、CSS、JavaScript、React、TypeScript、前端工程化、HTTP、FastAPI、REST API、SQL、PostgreSQL、ORM、认证、LLM、Embedding、向量检索、RAG、Tool Calling、Agent、测试、Git、Docker、Linux、Nginx、HTTPS、云部署和架构设计。

## 技术演进逻辑

StudyOS 先用浏览器原生能力验证核心学习管理需求；当页面复杂、状态管理和可维护性成为问题时，引入 React、TypeScript 与前端工程化；当数据需要跨页面、跨设备和持久化共享时，引入 HTTP、FastAPI、SQL、PostgreSQL 与 ORM；当系统需要个人数据隔离时，引入用户系统；当积累了足够的学习数据后，引入 LLM、知识库、RAG 和 Agent；随着系统复杂度增加，再引入测试、Git 工程化、容器化、Linux 和部署。

技术由需求推动，不预先锁定具体框架、模型、向量数据库、云厂商或 Agent 工具。

## 功能演进路线

1. 基础学习管理：Dashboard、学习记录、学习任务、项目管理和本地保存。
2. 应用工程化：组件化界面、类型约束、真实 API 和云端数据。
3. 多用户能力：身份认证、数据隔离和个人空间。
4. AI 学习辅助：总结、知识点提取、复习问题和学习分析。
5. 个人知识库：资料管理、检索、基于个人内容的问答。
6. Agent 能力：查询数据、分析状态、制定计划和更新任务。
7. 工程交付：测试、容器化、服务器运行、HTTPS 和持续维护。

## Phase 总览

| 阶段 | 主题 | 状态 |
| --- | --- | --- |
| Phase 0 | 项目定义与工程准备 | 已完成方向定义 |
| Phase 1 | HTML + CSS + JavaScript 前端 MVP | 待开始 |
| Phase 2 | React + TypeScript + Vite | 规划 |
| Phase 3 | HTTP + FastAPI + REST API | 规划 |
| Phase 4 | SQL + PostgreSQL + ORM | 规划 |
| Phase 5 | 前后端完整集成 | 规划 |
| Phase 6 | 用户系统与认证 | 规划 |
| Phase 7 | LLM / AI 能力 | 规划 |
| Phase 8 | Embedding + Vector Database + RAG | 规划 |
| Phase 9 | AI Agent + Tool Calling | 规划 |
| Phase 10 | 测试、工程化与 Git | 规划 |
| Phase 11 | Docker 与容器化 | 规划 |
| Phase 12 | Linux、Nginx、HTTPS 与云部署 | 规划 |

## 阶段依赖

Phase 0 明确边界与学习方式；Phase 1 验证最小产品；Phase 2 解决前端复杂度；Phase 3 建立服务通信；Phase 4 建立持久化数据基础；Phase 5 完成全栈闭环；Phase 6 引入数据隔离；Phase 7 在真实数据基础上引入 AI；Phase 8 让 AI 使用个人知识；Phase 9 让 AI 使用受控工具；Phase 10 至 Phase 12 解决质量、运行环境与交付问题。

阶段可以因实际需求插入前置知识，但必须说明原因，不能跳过理解直接堆叠技术。

## 当前状态

仓库当前尚未正式开发。Phase 0 已完成项目方向定义，Phase 1 待开始，其余阶段处于规划状态。本次文档只建立全局地图，不包含具体小任务、编码步骤或实现代码。

## 推进机制

进入某个 Phase 后，再为该阶段补充详细计划；随后拆成小任务，逐项学习、实现、测试、Review、修复、知识验收和复盘。功能完成不等于学习完成，必须同时满足功能、技术、知识、Debug 和工程验收。
