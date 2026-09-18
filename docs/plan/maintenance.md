# 计划维护规则（Living Roadmap Rules）

> 计划是活的。本文规定 StudyOS 计划系统如何更新、何时更新、按什么流程更新，以及链接与文档的规范。
> 计划入口见 [README.md](README.md)，总路线见 [roadmap.md](roadmap.md)，历史决策见 [decisions.md](decisions.md)。

## 三个层级，三种更新频率

| 层级 | 文件 | 什么时候写 / 更新 |
| --- | --- | --- |
| Level 1 总路线 | [roadmap.md](roadmap.md)、product / architecture / learning 三份路线图 | 每个 Phase 结束时复核；出现方向性变更时立即更新 |
| Level 2 阶段计划 | `phase-XX/README.md` | 进入该 Phase 前刷新为当前版本；阶段中只做小幅修订并记录原因 |
| Level 3 详细任务计划 | `phase-XX/plan.md` | **仅进入该 Phase 时创建**；任务粒度的拆解、每日安排、具体实现步骤都放这里 |

不允许在 Level 1 塞具体任务，也不允许在尚未进入的 Phase 提前展开 Level 3（防止计划过细、迅速过时）。

## 进入 Phase 的标准流程

当开发者说“进入 Phase X”时，严格按以下顺序执行，**不得跳过规划直接写代码**：

1. **重读总路线**：[roadmap.md](roadmap.md) 中该 Phase 的目标、前置与产出。
2. **读取当前 Phase 计划**：`phase-X/README.md`，确认是最新版本。
3. **检查实际代码**：前置 Phase 的产出是否真实存在、可运行；当前架构与计划描述是否一致。
4. **检查学习状态**：前置知识是否真正掌握（用前一 Phase 的学习验收标准核对）。
5. **检查旧计划适用性**：范围、技术选型、数据模型是否仍合理；识别技术债与新约束。
6. **必要时更新路线**：方向性变化先写入 [decisions.md](decisions.md)，再更新受影响文档。
7. **生成 Level 3 详细计划**：创建 `phase-X/plan.md`，拆解到功能 → 模块 → 任务粒度（不是口号），包含验证方式与 Git 节点。
8. **建立 / 校对链接**：确认与总路线、三条路线、相邻 Phase 的双向链接有效。
9. **等待开发者确认计划**，确认后才开始编码。

## 阶段结束（Exit）流程

每个 Phase 完成后、进入下一 Phase 前：

1. 逐条执行该 Phase 的功能 / 技术 / 知识 / 工程验收，记录结果。
2. 写阶段复盘：学到了什么、计划与现实的偏差、技术债清单。
3. 更新总路线状态图例（⬜ → ✅），在下一 Phase 文档标注前置已满足。
4. 复核 Level 1 文档：下一阶段目标是否需要根据实际成果调整。
5. 把复盘暴露的新方向 / 新约束记入 [decisions.md](decisions.md) 或 Horizon。
6. 提交一个表达清晰的 Git 节点（如 `phase-1: complete learning loop mvp`）。

## 更新触发条件

出现以下任一情况，必须更新计划而不是将错就错：

- 实际开发发现 Phase 顺序或技术依赖不成立；
- 产品理念变化（核心实体、核心闭环、AI 边界改变）；
- 某功能在两个 Phase / 两份文档中重复定义；
- 计划中的技术选型被证明不必要或出现更合理替代；
- 开发者实际能力与学习目标明显脱节（计划过快或过慢）；
- Scope Creep：出现与学习闭环无关的新功能诉求。

更新原则：**方向性变更先决策、后改文档**；小的措辞与事实修正可直接改，但要在相关 Phase 文档的“变更记录”小节注明日期与原因。

## 决策记录格式（decisions.md）

每条决策一个编号，永久保留、可追溯：

```text
### D-XXX 标题
- 日期：YYYY-MM-DD
- 背景：当时遇到的问题 / 冲突
- 决策：最终选择
- 原因：为什么这样选，放弃了什么方案
- 影响：影响哪些 Phase / 文档 / 代码
```

## 链接规范

- 全部使用 **Markdown 相对路径内部链接**，不使用外部 URL 指向仓库内文档。
- 链接表达**结构关系**（归属、前置 / 后续、产品 / 技术 / 学习映射、细节展开），不为普通句子加链接。
- 双向链接必须成对：Phase 链接到总路线，总路线必须链接回 Phase。
- 新建 / 重命名 / 删除文档后，立即检查引用该文档的所有链接。
- 锚点链接只用于确实需要定位到具体小节的场景，锚点文本与标题保持一致。
- 每个 Phase README 顶部固定一个导航区：总路线、三条路线、上一 Phase、下一 Phase、维护规则、决策记录。

标准导航关系：

```text
roadmap ←→ phase-XX ←→ product / architecture / learning
phase-(XX-1) ←→ phase-XX ←→ phase-(XX+1)
phase-XX/README ←→ phase-XX/plan（进入阶段后）
```

## 反模式清单（发现即纠正）

| 反模式 | 表现 | 纠正方式 |
| --- | --- | --- |
| Scope Creep | 顺手加与闭环无关的功能 | 退回 Horizon，注明真实需求出现再评估 |
| Over-engineering | 为假想的未来需求建复杂抽象 | 只留职责接缝，不写抽象层（见 [architecture-roadmap.md](architecture-roadmap.md)） |
| Premature Abstraction | P1 就引入框架 / 图谱 / 微服务 | 严格执行各 Phase“不做什么”清单 |
| AI for AI's sake | 没有数据与场景就接 LLM | AI 不早于 P8；P1 先用规则引擎占位 |
| 计划过细 | 未进入就排“第一天 / 第二天” | 细节只进当前 Phase 的 plan.md |
| 计划过粗 | Phase 文档无法判断做完没有 | 补齐目标、范围、验证标准、产出 |
| 学习与开发脱节 | 功能做了但讲不清原理 | 五类验收缺一不可，AI 不代写未学部分 |
| 任务与知识脱节 | Task 变成普通 Todo | 任务必须关联 Knowledge，完成必须产生记录 |
| 静默 AI 控制 | AI 直接改数据 / 替用户决定 | 一律提案化：接受 / 修改 / 拒绝 |
| 多份计划互相矛盾 | 旧文档未随理念更新 | 按本文流程更新并在 decisions.md 留痕 |

## 文档变更记录

- 2026-09-17：建立计划系统（Level 1 四份路线 + Phase 0–12 Level 2 计划 + 维护规则），旧 PLAN/PHASE 文档移入 [archive/](archive/README.md)。详见 [D-001](decisions.md)。
