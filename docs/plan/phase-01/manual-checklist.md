# Phase 1 手动验证清单（Manual Checklist）

> 本文件是 Phase 1 的 M0 产出之一（见 [README.md#开发顺序](README.md#开发顺序里程碑level-2)）。Phase 1 不引入测试框架，所有验证由开发者在浏览器中手动完成并能口头解释。
>
> **使用方式**：每完成一个里程碑，勾选对应小节全部项目，再走 Review 门（开发者自述 → AI 原理提问 → Review diff → 开发者修复 → 重跑清单）。发现失败项时，修复后从该小节第一项重跑。
>
> **导航**：[Phase 1 计划](README.md) · [M1 任务计划](plan.md) · [维护规则](../maintenance.md) · [决策记录](../decisions.md)

## 验证环境

- 浏览器：当前主流桌面浏览器（Chrome / Edge 任一），打开开发者工具（Console / Application → Local Storage）。
- 数据位置：当前源站点的 localStorage；每个里程碑开始前记录初始状态，需要时可清空 `studyos:*` 键后重新加载。
- 禁止项核查：全程不得出现 React / Vue / TypeScript / 后端 / 数据库 / AI API（见 [README.md 不做什么](README.md)）。

## M0 基线（已完成）

- [x] 目录结构存在：`src/index.html`、`src/css/`、`src/js/`，无依赖文件（无 package.json、node_modules）。
- [x] 基线提交存在：`61e6ddb chore: establish project baseline`，提交时工作区干净。
- [x] 本手动验证清单文件已建立。

## M1 数据与存储

> 对应任务拆解见 [plan.md](plan.md)。M1 没有 UI，验证在浏览器控制台完成。

- [ ] 四类对象（KnowledgeNode / Relation / Task / LearningRecord）字段与 plan.md 数据契约一致，无多余字段、无缺失字段。
- [ ] 所有 localStorage 读写只经过统一 store 模块；代码中不存在视图 / 其他模块直接调用 localStorage。
- [ ] 控制台写入一组示例数据后刷新页面，数据完整恢复（JSON 往返无丢失、无类型错误）。
- [ ] 存储键为约定的五个：`studyos:knowledge`、`studyos:relations`、`studyos:tasks`、`studyos:records`、`studyos:meta`。
- [ ] `studyos:meta` 中可读到 schema version；当前版本号与 plan.md 一致。
- [ ] 手动把某个键改成非法 JSON 后刷新，页面不白屏、不报错中断，store 按约定回退到空数据（或安全默认值），控制台有可理解的错误提示。
- [ ] 对象工厂产出的新对象：ID 唯一、默认值正确（mastery 默认 0、status 默认“未学习”、starred 默认 false、时间戳存在）。
- [ ] 创建 Task 时不传 knowledgeId 会被拒绝并给出明确错误；不存在无知识归属的任务。
- [ ] 种子数据：清空存储后首次加载，出现 4 个节点（JavaScript / 函数 / 作用域 / 闭包），层级为 JavaScript → 函数 → 闭包、JavaScript → 作用域；存在 1 条“闭包 prerequisite 作用域”关系。
- [ ] 再次刷新不重复写入种子数据（幂等）；已有用户数据不被种子覆盖。
- [ ] 开发者能口头解释：对象如何变成字符串存入 localStorage、刷新后如何还原、为什么所有读写要经过 store。

## M2 知识 CRUD 与层级

> 进入 M2 时，依据 [README.md 里程碑表](README.md#开发顺序里程碑level-2) 与当时 plan.md 展开填写，不提前细化。

- [ ] 待 M2 进入时展开（知识树渲染、创建 / 编辑 / 删除、领域归属、持久化）。

## M3 详情与关系

- [ ] 待 M3 进入时展开（详情视图、内容字段编辑、重点与状态、related / prerequisite 关系建立与双向跳转、删除知识时的关系处理规则）。

## M4 自评与记录

- [ ] 待 M4 进入时展开（自评控件、自评即生成 Learning Record、before→after 一致）。

## M5 关联任务

- [ ] 待 M5 进入时展开（任务必须挂知识、任务列表、完成任务自动生成记录并引导更新掌握度）。

## M6 规则建议

- [ ] 待 M6 进入时展开（规则引擎纯函数、薄弱点与建议区、理由展示、建议→任务的确认门、用户可拒绝 / 忽略）。

## M7 端到端闭环走查（阶段验收）

以下 9 步必须由开发者独立操作并解释，原文依据 [README.md#验证标准](README.md#验证标准)：

1. [ ] 创建知识 `闭包`（挂在 `JavaScript / 函数` 下），补充定义与理解；
2. [ ] 设置掌握度为 30，标记重点；
3. [ ] 在总览看到它出现在薄弱知识区；
4. [ ] 基于建议创建任务“完成 3 道闭包代码题”，确认任务关联到 `闭包`；
5. [ ] 完成任务，系统生成学习记录；
6. [ ] 将掌握度更新为 65，记录显示 `30 → 65`（含任务带来的变化）；
7. [ ] 规则建议从“重新学习”变为“练习”；
8. [ ] 刷新浏览器，全部数据与状态仍在；
9. [ ] 建立 `闭包` 与 `作用域链` 的 related 关系，详情页可互相跳转。

### 四类验收速查

- [ ] **功能**：9 步走查全程可用；知识 / 任务 / 记录增删改查正确；空数据有引导而非报错。
- [ ] **技术**：存储只经 store 层；规则引擎是独立纯函数；无不安全 HTML 拼接（XSS 基础意识）；数据与 UI 同步正确。
- [ ] **知识**：能讲清“点击事件 → 数据变化 → 重新渲染 → localStorage”链路；能解释 JSON 序列化、掌握度与重点的区别、层级与关系的区别、规则引擎为何是 AI 接缝。
- [ ] **工程**：js 文件按职责划分、命名清晰、无大段重复；本清单全部通过；每个里程碑至少一个表达清晰的提交；未引入禁止清单中的任何技术。

## 变更记录

- 2026-09-19：M0 阶段建立清单，M1 小节展开，M2–M7 按计划留占位（依据 [D-012](../decisions.md)）。
