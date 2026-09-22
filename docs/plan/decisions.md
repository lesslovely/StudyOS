# 规划决策与变更日志（Decisions & Changelog）

> 记录 StudyOS 计划系统中所有方向性决策、冲突裁决与变更原因。新增决策按格式追加，不覆盖历史。
> 维护流程见 [maintenance.md](maintenance.md)，计划入口见 [README.md](README.md)。

## 2026-09-17 旧计划整合分析

整合范围：根 `README.md`、旧 `docs/plan/PLAN.md`、旧 `PHASE-00.md` ~ `PHASE-12.md`（共 15 份文档）。原始文件已通过 `git mv` 移入 [archive/](archive/README.md)，未删除。

### 发现的冲突

1. **核心实体重定位（最重要冲突）**：旧计划以 Dashboard / Learning Records / Learning Tasks / **Projects** 为中心，Knowledge Base 只是未来的资料仓库；新产品基线以 **Knowledge Node 为唯一核心实体**，Task 必须挂在 Knowledge 上，学习闭环围绕掌握度变化运转。两套模型不能并存。
2. **Phase 1 范围冲突**：旧 P1 做“记录 + 任务 + 项目 + Dashboard”；新 P1 必须证明“知识 → 掌握度 → 薄弱点 → 关联任务 → 记录 → 掌握度更新 → 建议”的完整闭环。
3. **AI 出现时机冲突**：旧计划 AI 最早出现在 P7（LLM），此前产品没有任何建议能力；新基线要求 P1 就用**规则引擎**模拟 AI 建议，让建议交互闭环先成立。
4. **状态标记不一致**：旧 README 标记 Phase 0 为 🟨 当前阶段，旧 PLAN.md 称 Phase 0 已完成方向定义。
5. **测评系统缺位**：新产品基线用整节描述测试 / 测评体系（单知识 + 关联综合测试、多题型、多信号掌握度），旧 13 个 Phase 中没有任何阶段承载它。
6. **测试工程化位置问题**：旧计划把测试 / Git 放到 Phase 10，但新基线要求 P1 学习目标就包含 Git 与基础工程实践；事实上旧 PHASE-01 自己也要求“手动测试记录”，前后矛盾。

### 发现的重复

- 根 README 与 PLAN.md 各有一份 Phase 0–12 路线图，内容大量重复且无链接关系。
- 每份 PHASE 文档的“核心功能”与 README“核心功能规划”两处维护，已经出现表述漂移。
- “技术学习路线”在 README、PLAN.md、各 PHASE 文档中各写一遍。

### 发现的过时内容

- “Projects 项目管理”作为核心模块（旧 P1–P5、P9 反复出现）与知识核心定位不符。
- 旧 README 的功能清单（学习记录分类 / 时间查询、任务优先级 / 截止时间等通用 Todo 能力）缺少“关联知识”约束。
- 旧 README“未来项目结构 frontend/ backend/ docker-compose.yml”与当前 `src/` 脚手架缺少过渡说明。
- 旧文档无知识内容 / 用户状态分离、无掌握度模型、无知识关系模型、无模板定位、无 Advisor 边界。

### 发现的顺序问题

- Docker（旧 P11）与 Linux 部署（旧 P12）对单人学习项目是一条连续链路，拆成两个阶段都偏薄，且旧 P11 自述目的只是“为部署准备”。
- LLM（旧 P7）→ RAG（旧 P8）→ Agent（旧 P9）的顺序依赖正确，保留。
- 测评必须在 LLM 之前：AI 分析建议需要结构化掌握度信号，否则只能空谈。

### 决策记录

### D-001 建立分层计划系统并归档旧文档
- 日期：2026-09-17
- 背景：旧计划为 15 份扁平文档，路线图重复维护、无双向链接、与新产品理念冲突。
- 决策：建立 Level 1（四份路线）/ Level 2（phase-XX/README.md）/ Level 3（进入阶段才建的 plan.md）三层结构；旧文档移入 [archive/](archive/README.md) 只读保留。
- 原因：计划需要长期维护与可追溯，而非每次重写一份大文档。
- 影响：全部规划文档；根 README 降级为入口。

### D-002 核心实体切换为 Knowledge，Projects 移出核心产品
- 日期：2026-09-17
- 背景：见“冲突 1”。学习闭环以知识状态改变为目标，项目管理与闭环无直接关系。
- 决策：以 Knowledge Node（内容 / 状态 / 关系 / 学习数据四组）为核心重建所有 Phase 的功能描述；Projects 不进入任何近期 Phase；未来如有真实需求，只能以“知识的应用记录”形态回归评估。
- 原因：保留 Projects 会让 P1 同时服务两个产品方向，是典型 Scope Creep；通用项目管理已有大量成熟工具，不构成学习价值。
- 影响：P1–P5、P10 的功能范围；产品路线；根 README。

### D-003 Phase 1 重定义为“知识学习闭环 MVP”
- 日期：2026-09-17
- 决策：P1 功能固定为 Knowledge CRUD + 层级 + 简单关系、Knowledge Detail、关联 Task、Learning Record、规则 Recommendation、localStorage；通用 Dashboard 降级为服务闭环的“知识总览”。
- 原因：MVP 的唯一使命是证明核心闭环成立。
- 影响：[phase-01](phase-01/README.md)；技术与学习路线中 P1 章节。

### D-004 新增 Phase 7“测评系统与多信号掌握度”
- 日期：2026-09-17
- 背景：测评体系是产品路线 Assessment 阶段的载体，旧计划缺位。
- 决策：在认证（P6）之后、LLM（P8）之前插入测评 Phase；P1 仅保留用户自评，P7 做规则化测评与掌握度聚合，AI 出题留给 P8 之后。
- 原因：测评需要结构化存储（依赖 P4）与个人数据隔离（依赖 P6）；又必须先于 AI 建议（P8）以提供可信信号。
- 影响：旧 P7–P10 整体后移一位。

### D-005 原 Docker 与部署两阶段合并为 Phase 12
- 日期：2026-09-17
- 决策：容器化与 Linux/Nginx/HTTPS/部署合并为一个 Phase，内部分“容器化”“生产部署”两个里程碑。
- 原因：容器化对本项目的唯一目的就是一致地交付，二者依赖连续、各自单独成阶段都偏薄。
- 影响：旧 PHASE-11、PHASE-12 → 新 [phase-12](phase-12/README.md)。

### D-006 测试与 Git 改为横向实践，Phase 11 只负责体系化
- 日期：2026-09-17
- 决策：Git 提交习惯与手动验证从 P1 开始；可测试的纯函数（store / rules）从 P1 就按可测方式组织；P11 建立自动化测试金字塔与工程化体系。
- 原因：质量实践最后补是常见失败模式；但体系化框架学习仍需足够复杂的系统作为对象。
- 影响：[phase-01](phase-01/README.md)、[phase-11](phase-11/README.md)、architecture / learning 路线“横向实践”章节。

### D-007 掌握度模型：1~100，P1 仅自评，多信号逐步融合
- 日期：2026-09-17
- 决策：掌握度与重点标记独立；P1 用自评（不强迫精确数字），P7 加入测试信号，P8 加入 AI 对话信号，Horizon 考虑衰减与自适应；任何阶段都不对外宣称系统能精确判分。
- 影响：P1 数据模型、P7、product-roadmap 测评演进表。

### D-008 AI 边界：Advisor 提案制 + P1 规则引擎占位
- 日期：2026-09-17
- 决策：所有 AI 输出以提案（接受 / 修改 / 拒绝）呈现；P1 用纯函数规则引擎（mastery < 40 重新学习，40–70 练习，70+ 复习 / 综合应用）作为智能层接缝，P8 替换为 LLM，P10 写操作仍需确认。
- 原因：先让交互闭环成立，再换智能内核；同时保证用户最终决定权。
- 影响：P1、P8、P10 与架构路线“演进接缝”。

### D-009 知识结构：层级 + 三种关系，复杂图谱推迟
- 日期：2026-09-17
- 决策：P1 仅 parent / related / prerequisite；depends-on / contrast / application / 自定义关系与图数据库进 Horizon；关系型查询够用就不引入图库。
- 影响：P1 数据模型、P4、Horizon。

### D-010 知识模板定位为脚手架，P1 只带最小示例数据
- 日期：2026-09-17
- 决策：不建设完整语言知识库；P1 可附带一份极小的 JavaScript 示例知识（函数 / 作用域 / 闭包）用于走通闭环，模板导入导出与 AI 生成模板后续再排。
- 影响：P1 范围、Horizon。

### D-011 阶段状态统一
- 日期：2026-09-17
- 决策：Phase 0 标记为 ✅（产出为本计划系统）；Phase 1 为 ⬜ 待进入，需先走进入流程生成 plan.md；其余 ⬜ 规划中。

## 新旧 Phase 编号映射

| 旧 | 新 | 说明 |
| --- | --- | --- |
| PHASE-00 | [phase-00](phase-00/README.md) | 保留刷新 |
| PHASE-01 | [phase-01](phase-01/README.md) | 范围重定义（D-003） |
| PHASE-02 | [phase-02](phase-02/README.md) | 保留，围绕知识实体重构 |
| PHASE-03 | [phase-03](phase-03/README.md) | 保留，资源对象更换 |
| PHASE-04 | [phase-04](phase-04/README.md) | 保留，增加层级 / 关系建模 |
| PHASE-05 | [phase-05](phase-05/README.md) | 保留 |
| PHASE-06 | [phase-06](phase-06/README.md) | 保留 |
| — | [phase-07](phase-07/README.md) | 新增测评（D-004） |
| PHASE-07 | [phase-08](phase-08/README.md) | LLM，后移 |
| PHASE-08 | [phase-09](phase-09/README.md) | RAG，后移 |
| PHASE-09 | [phase-10](phase-10/README.md) | Agent，后移 |
| PHASE-10 | [phase-11](phase-11/README.md) | 测试工程化，后移且改为横向（D-006） |
| PHASE-11 + PHASE-12 | [phase-12](phase-12/README.md) | 合并（D-005） |

### D-012 Phase 1 进入决策（M1 前置决策）
- 日期：2026-09-19
- 背景：正式进入 Phase 1，需要关闭进入前的待确认问题，确定 M1 数据与存储里程碑的工作边界。
- 决策：
  1. M1 附带最小示例知识集：`JavaScript（领域）→ 函数 → 闭包`、`JavaScript → 作用域`，共 4 个节点，并建立 1 条“闭包 prerequisite 作用域”关系（落实 D-010）。
  2. knowledge status 枚举确定为：`未学习 / 学习中 / 复习中 / 已掌握`，默认 `未学习`。
  3. mastery 数据范围确定为 1~100（M1 种子数据默认 0，表示未评）；**mastery 与 status 是两个独立字段**，不互相推导。
  4. 三视图（知识总览 / 知识详情 / 任务与记录）属于 M2 之后的 UI 决策，**不阻塞 M1**，进入 M2/M3 时再确认。
  5. 掌握度自评控件形态（滑块 vs 档位）属于 M4 UI 决策，**不阻塞 M1**，进入 M4 时确认。
  6. M0 基线已完成：提交 `61e6ddb chore: establish project baseline`，并补齐手动验证清单（[phase-01/manual-checklist.md](phase-01/manual-checklist.md)）。
- 影响：[phase-01/plan.md](phase-01/plan.md) 的 M1 任务拆解；M1 只做数据契约、store、工厂校验、种子数据，不做 UI。

### D-013 Phase 1 开发分支
- 日期：2026-09-19
- 决策：Phase 1 开发在 `feature/knowledge` 分支进行，里程碑提交留在该分支；合并回 `main` 的时机在 Phase 1 收尾（M7）时决定。
- 原因：基线已在 main 上，功能开发走特性分支便于 Review 与回退。
- 影响：phase-01/README.md 的 Git 节点说明同步更新。

## 待确认问题处理结果（2026-09-19）

| # | 原问题 | 结论 | 依据 |
| --- | --- | --- | --- |
| 1 | 是否附带 JavaScript 最小示例知识集 | ✅ 已确认：附带，4 节点（JavaScript / 函数 / 作用域 / 闭包）+ 1 条前置关系 | D-010、D-012 |
| 2 | status 枚举是否接受 | ✅ 已确认：未学习 / 学习中 / 复习中 / 已掌握 | D-012 |
| 3 | 三视图是否接受 | ⏸ 推迟：不阻塞 M1，进入 M2/M3 时确认 | D-012 |
| 4 | 掌握度控件形态 | ⏸ 推迟：范围 1~100 已确认；控件形态进入 M4 时确认 | D-007、D-012 |
| 5 | 空脚手架是否提交为 M0 基线 | ✅ 已完成：`61e6ddb` | D-012 |

当前没有阻塞 M1 的未决问题。下一批待确认项出现在 M2（视图）与 M4（自评控件）进入时。
