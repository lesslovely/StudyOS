# StudyOS

Personal Learning & Knowledge Management System

> **Project Status: Planning**

## 项目简介

StudyOS 是一个个人学习与知识管理系统，同时也是一个长期的软件工程学习项目。未来计划用于管理学习记录、学习计划、项目进度、知识库、AI 学习辅助、RAG 与 AI Agent。

**当前项目还没有实现这些功能，目前只是项目规划阶段。** 本次只完成项目定义、项目方向、学习路线和 README，不开始实际开发。

## Project-driven Learning

本项目采用项目驱动的学习方式：

```text
项目需求 → 发现问题 → 学习对应知识 → 应用到项目 → 测试与验证 → 继续迭代
```

而不是“先把所有知识学完，最后才做项目”。项目本身就是学习载体；每一个技术都应该在真实需求中逐渐引入，不为了炫技提前加入复杂技术。

## 项目动机

StudyOS 用于把零散学习的知识真正连接起来，通过一个真实、持续迭代的项目逐步建立完整的软件工程认知：

```text
HTML / CSS / JavaScript → Frontend → HTTP / API → Backend → Database → AI → RAG → Agent → Deployment
```

## 核心功能规划

以下内容全部是未来规划，当前不会实现任何功能。

### Dashboard

- 今日学习情况
- 学习任务
- 最近学习记录
- 项目进度
- 学习统计

### Learning Records

- 创建、查看、修改、删除学习记录
- 分类
- 时间查询

### Learning Tasks

- 创建、查看、修改、删除学习任务
- 完成任务
- 优先级
- 截止时间

### Projects

- 项目列表
- 项目进度
- 当前阶段
- 技术栈
- 项目笔记

### AI Learning Assistant

- 自动总结学习记录
- 提取知识点
- 生成复习问题
- 根据历史学习内容提供学习辅助

### Knowledge Base

- 保存个人学习资料
- 保存 Markdown / 笔记
- 建立个人知识库
- 对知识进行检索

### RAG

- 查询历史学习内容
- 根据个人知识库回答问题
- 分析已经掌握的知识
- 找出知识缺口

### AI Agent

- 查询学习记录、学习任务和项目
- 分析学习状态
- 制定学习计划
- 创建和更新学习任务

## 技术学习路线

```text
Frontend
- HTML
- CSS
- JavaScript
- React
- TypeScript
- Vite

Backend
- Python
- FastAPI

Database
- SQL
- PostgreSQL
- ORM
- Database Design

AI
- LLM API
- Prompt Engineering

Knowledge
- Embedding
- Vector Database
- RAG

Agent
- Tool Calling
- Agent Workflow

Engineering
- Git
- GitHub
- Testing
- Docker
- Linux
- Nginx
- Deployment
```

> 以上技术是长期路线，不代表现在全部使用。

## 完整 Roadmap

状态标记：`🟨 当前阶段` · `⬜ 未开始` · `✅ 已完成`

```text
Phase 0  🟨  项目定义
Phase 1  ⬜  前端 MVP
Phase 2  ⬜  React + TypeScript
Phase 3  ⬜  HTTP + FastAPI
Phase 4  ⬜  PostgreSQL + 数据库
Phase 5  ⬜  前后端联调
Phase 6  ⬜  用户系统
Phase 7  ⬜  AI
Phase 8  ⬜  RAG
Phase 9  ⬜  Agent
Phase 10 ⬜  测试与工程化
Phase 11 ⬜  Docker
Phase 12 ⬜  Linux + 部署
```

每个阶段都遵循“阶段目标 → 主要学习内容 → 未来准备实现的功能”的顺序；以下只描述规划，不代表已经实现。

### Phase 0 — 项目定义 🟨

**阶段目标：** 明确项目定位、长期目标、学习方向和迭代原则。

**主要学习内容：** 需求分析、产品定位、学习路线规划、GitHub 项目管理、README 文档编写。

**未来准备实现的功能：** 为 Dashboard、Learning Records、Learning Tasks、Projects 和知识库建立需求基础。当前只完成规划。

### Phase 1 — 前端 MVP ⬜

**阶段目标：** 使用 HTML、CSS、JavaScript 完成第一个可运行版本。

**主要学习内容：** DOM、Event、JavaScript、localStorage、模块化。

**未来准备实现的功能：** Dashboard、Learning Records、Learning Tasks、Projects。

### Phase 2 — React + TypeScript ⬜

**阶段目标：** 将前端演进为可维护的组件化应用。

**主要学习内容：** React、组件与状态、TypeScript、数据流、Vite、前端工程化。

**未来准备实现的功能：** 可复用页面和组件，以及学习记录、任务和项目界面。

### Phase 3 — HTTP + FastAPI ⬜

**阶段目标：** 理解前后端通信并规划后端 API。

**主要学习内容：** HTTP、REST API、JSON、Python、FastAPI、API 设计与错误处理。

**未来准备实现的功能：** 学习记录、任务、项目 API 和基础前后端通信。

### Phase 4 — PostgreSQL + 数据库 ⬜

**阶段目标：** 将数据迁移到结构化数据库。

**主要学习内容：** SQL、PostgreSQL、数据库设计、关系与约束、ORM、数据迁移。

**未来准备实现的功能：** 持久化保存并查询学习记录、任务和项目。

### Phase 5 — 前后端联调 ⬜

**阶段目标：** 形成基础全栈应用闭环。

**主要学习内容：** API 集成、加载与错误状态、数据校验、基础安全意识。

**未来准备实现的功能：** Dashboard 数据展示和记录、任务、项目的完整管理流程。

### Phase 6 — 用户系统 ⬜

**阶段目标：** 理解用户身份、权限和个人数据隔离。

**主要学习内容：** 注册登录、认证、Session 或 Token、权限控制、密码安全。

**未来准备实现的功能：** 个人账户、数据隔离、登录后的学习空间和基础设置。

### Phase 7 — AI ⬜

**阶段目标：** 在真实学习场景中引入 LLM。

**主要学习内容：** LLM API、Prompt Engineering、上下文设计、输出校验、成本与安全。

**未来准备实现的功能：** 总结学习记录、提取知识点、生成复习问题和 AI 学习辅助。

### Phase 8 — RAG ⬜

**阶段目标：** 让 AI 基于个人知识库检索并回答问题。

**主要学习内容：** 文档切分、Embedding、向量数据库、相似度检索、RAG 与评估。

**未来准备实现的功能：** 查询历史内容、回答知��库问题、分析掌握情况、发现知识缺口。

### Phase 9 — Agent ⬜

**阶段目标：** 理解 Agent 如何通过工具和工作流完成任务。

**主要学习内容：** Tool Calling、Agent Workflow、权限设计、状态管理、任务分解与验证。

**未来准备实现的功能：** 查询数据、分析学习状态、制定计划、创建和更新任务。

### Phase 10 — 测试与工程化 ⬜

**阶段目标：** 提高可靠性、可维护性和持续迭代能力。

**主要学习内容：** 单元测试、集成测试、API 测试、前端测试、代码质量、Git 工作流。

**未来准备实现的功能：** 为核心业务建立测试覆盖和稳定的验证流程。

### Phase 11 — Docker ⬜

**阶段目标：** 理解容器化并建立一致的运行环境。

**主要学习内容：** 镜像、容器、Dockerfile、Docker Compose、环境变量与配置管理。

**未来准备实现的功能：** 容器化运行应用和数据库，为部署准备运行方式。

### Phase 12 — Linux + 部署 ⬜

**阶段目标：** 部署到真实服务器，形成软件交付闭环。

**主要学习内容：** Linux、Nginx、域名、HTTPS、日志、监控、发布与回滚。

**未来准备实现的功能：** 部署可访问的 StudyOS 并��续维护线上环境。

## 最终学习能力地图

```text
Web 基础
   ↓
HTML / CSS / JavaScript
   ↓
Frontend Engineering
   ↓
HTTP / API
   ↓
Backend Engineering
   ↓
Database
   ↓
Full-Stack Application
   ↓
AI Application
   ↓
RAG
   ↓
Agent
   ↓
Testing
   ↓
Docker
   ↓
Linux
   ↓
Deployment
   ↓
Software Architecture
```

最终目标是通过一个项目逐步建立完整的 Full-Stack + AI 工程能力。

## 项目发展原则

### 1. Incremental Development

逐阶段开发，不一次性实现所有内容。

### 2. Learn by Building

通过实际需求学习技术。

### 3. Keep It Simple

优先简单、清晰、容易理解的设计。

### 4. Avoid Premature Engineering

不提前引入没有实际需求的复杂技术。

### 5. Understand Before Abstraction

先理解，再抽象。

### 6. AI as Assistant

AI 可以用于解释、Debug、Code Review、方案分析和学习辅助，但项目主人必须理解最终代码和架构。

## 当前项目状态

```text
Project Status: Planning

项目代码：未开始
前端：未开始
后端：未开始
数据库：未开始
AI：未开始
RAG：未开始
Agent：未开始
测试：未开始
Docker：未开始
部署：未开始
```

当前唯一完成内容：项目定义、项目方向、学习路线、README。

## 未来项目结构

```text
StudyOS/
├── frontend/
├── backend/
├── docs/
├── README.md
└── docker-compose.yml
```

> 以上只是未来规划结构，目前不要创建这些文件和目录。

## 最终目标

StudyOS 不只是一个学习记录网站，而是一个长期的软件工程实践项目：

```text
StudyOS
= 个人学习系统
+ 长期全栈学习项目
+ AI 应用项目
+ RAG 实践项目
+ Agent 实践项目
+ 软件工程实践项目
+ 最终可部署的完整项目
```

## 项目边界

当前阶段只进行项目规划，不创建实现代码，不初始化技术栈，不安装依赖，不创建前端、后端、数据库、配置、Docker、测试或 GitHub Actions。本阶段完成后停止，等待后续阶段根据真实需求逐步开始。
