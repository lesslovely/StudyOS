# StudyOS 产品路线图（Product Roadmap）

> 层级：Level 1 的产品视角。回答“StudyOS 让用户逐步获得什么能力与价值”。
> 总路线见 [roadmap.md](roadmap.md)，技术实现见 [architecture-roadmap.md](architecture-roadmap.md)，开发者能力成长见 [learning-roadmap.md](learning-roadmap.md)。

## 产品定位

StudyOS 是 Personal Learning Operating System：以**个人知识**为核心实体，以**学习闭环**运转方式，以 **AI** 为跨系统智能层，以**用户自主决策**为不可越过的边界。

它明确**不做**的东西：普通 Todo（任务不挂知识就没有意义）、纯笔记堆（没有状态与闭环）、在线课程平台（不提供标准化课程）、纯 AI Chatbot（AI 没有入口页、不替用户做决定）。

## 核心学习闭环

```text
知识 → 学习 → 任务 → 学习记录 → 掌握度变化 → 发现薄弱点
                                              ↓
        新任务 ← 用户决定 ← AI 建议 ← AI 分析 ←┘
          ↓
         学习 ↺
```

产品验收的第一标准永远是：**这次改动是否让闭环转得更完整、更可信？** 闭环之外的功能（例如旧计划中的“项目管理”）默认不做，裁决记录见 [decisions.md](decisions.md)。

## 核心实体模型（产品视角）

```text
Knowledge（知识）
├── Content 知识内容：定义、我的理解、示例/代码示例、使用场景、常见错误、疑问、学习资料
├── User State 用户状态：掌握度(1~100)、重点标记、当前学习状态
├── Relations 知识关系：parent（层级）/ related / prerequisite（初期三种）
└── Learning Data 学习数据：关联任务、学习记录、测试记录（衍生数据）

Task（任务）            ：必须关联至少一个 Knowledge；完成后产生 Learning Record
Learning Record（记录） ：时间、行为、关联知识、结果、掌握度变化（如 62 → 75）
Assessment（测评）      ：单知识测试 + 关联知识综合测试（P7 起系统化）
Recommendation（建议）  ：P1 规则生成；P8 起 AI 生成；均须给出理由并由用户决定
```

关键产品规则：

- **掌握度 ≠ 重点标记**：掌握度是状态量，重点是用户主观标注，二者独立。
- **掌握度 1~100，但不强迫精确输入**：P1 只支持用户自评（滑块/档位）；多信号融合是未来方向，不在早期假装系统能准确判分。
- **任务完成不是终点**：Task → Learning Record → Knowledge State Update 是一条强制链路。
- **知识结构 = 轻量层级 + 关系**，不是只有树。例：`JavaScript/函数/闭包` 属于层级，`闭包 ↔ 作用域 ↔ 作用域链` 属于关系。
- **模板只是脚手架**：内置模板（如 Python / JavaScript 骨架）帮助起步，用户可使用模板、建空白领域、导入内容，未来由 AI 生成骨架；最终形成的是个人知识系统。

## 产品演进阶段

| # | 产品阶段 | 用户价值 | 关键能力 | 对应 Phase |
| --- | --- | --- | --- | --- |
| 1 | Personal Knowledge | 知识不再零散，有结构、有内容、有状态 | 知识增删改查、层级、简单关系、知识详情、自评掌握度、重点标记 | [P1](phase-01/README.md) |
| 2 | Knowledge + Task | 每个学习动作都有明确指向 | 任务必须关联知识；完成任务回写知识 | [P1](phase-01/README.md) |
| 3 | Knowledge + Learning Record | 看得见自己的学习历史与掌握度变化 | 学习记录时间线、掌握度变化轨迹、薄弱点发现 | [P1](phase-01/README.md) → [P5](phase-05/README.md)（本地 → 跨设备持久化） |
| 4 | Assessment | 用检验代替“感觉学会了” | 单知识测试 → 关联知识综合测试；理论/代码/Debug/应用等题型；掌握度获得多信号输入 | 自评始于 [P1](phase-01/README.md)，系统化于 [P7](phase-07/README.md) |
| 5 | Recommendation | 知道下一步学什么、为什么 | 规则建议（P1）→ AI 分析与可解释建议（P8）→ 建议可接受/修改/拒绝 | [P1](phase-01/README.md)、[P8](phase-08/README.md) |
| 6 | AI Learning Assistant | AI 帮我整理、分析、出题、复盘，但决定权在我 | 建知识、理结构、建议关系、测评、分析薄弱点、推荐任务、复盘、解释理由 | [P8](phase-08/README.md)、[P9](phase-09/README.md) |
| 7 | Personal Learning OS | 个人学习空间可长期、安全、随处使用 | 账户与数据隔离、知识模板成熟、线上可访问、持续维护 | [P6](phase-06/README.md)、[P12](phase-12/README.md) |
| 8 | Agentic Learning System | AI 在授权范围内代办学习流程，人保留审批权 | 受控工具调用、查询分析、制定计划、确认后创建/更新任务 | [P10](phase-10/README.md) + Horizon |

## Phase 1 的产品边界（MVP）

必须完整证明以下链条可跑通（详见 [phase-01/README.md](phase-01/README.md)）：

```text
创建知识 → 设置掌握度 → 查看知识状态 → 发现薄弱知识
→ 创建关联任务 → 完成任务 → 产生学习记录
→ 更新掌握度 → 得到下一步建议 ↺
```

**P1 功能范围**：Knowledge（增删改查、层级、简单关系）、Knowledge Detail（基本信息 / 我的理解 / 知识内容 / 掌握度 / 重点 / 相关知识 / 关联任务 / 学习记录）、Task（创建 / 查看 / 完成 / 关联知识）、Learning Record（创建 / 查看 / 掌握度变化）、Recommendation（简单规则模拟 AI）、localStorage 持久化。

**P1 明确不做**：React/Vue/TypeScript、后端、数据库、认证、AI API、Agent、云部署、复杂知识图谱、向量库、RAG、多用户、权限、高级分析、间隔重复、高级测评。完整禁止清单与原因见 [phase-01/README.md](phase-01/README.md#不做什么范围边界)。

## AI 的产品原则：Advisor，不是 Controller

```text
AI 产出建议
    ↓
用户查看（必须能看到理由与依据）
    ↓
接受 / 修改 / 拒绝
    ↓
执行（写操作在 Agent 阶段仍需用户确认）
```

- AI 是**跨系统智能层**，不是一个孤立页面：建知识、理结构、建议关系、测评、分析掌握度与记录、找薄弱点、推荐任务、制定计划、复盘、解释理由，都属于 AI 层。
- Phase 1 的规则建议引擎是这一智能层的**占位与雏形**：它让“建议 → 用户决定 → 新任务”的交互闭环先成立，P8 再把规则替换 / 增强为 LLM，产品交互不推倒重来。
- 任何阶段都不允许 AI 静默修改用户知识数据。

## 测评产品演进（Assessment）

| 阶段 | 形态 | 掌握度信号 |
| --- | --- | --- |
| P1 | 用户自评 | 自评单一信号 |
| P7 | 单知识测试 + 关联知识综合测试（如：闭包 → 函数 → 作用域 → 作用域链） | 测试结果 + 自评 |
| P7 之后 | 理论理解、代码实现、Debug、实际应用、场景分析、知识迁移 | 多信号聚合（规则聚合，不伪装精确） |
| P8 起 | AI 出题、AI 对话式测评、AI 复盘 | 增加 AI 对话信号 |
| Horizon | 自动判题、间隔重复调度、自适应计划 | 趋势与衰减模型 |

## 被放弃 / 推迟的产品想法

记录在 [decisions.md](decisions.md)，摘要：

- **Projects（项目管理）模块移出核心产品**：旧 P1–P5、P9 均包含“项目管理”，它与学习闭环无直接关系，属于通用 PM 工具范畴；未来最多以“知识的应用记录”形式回归，不进入近期任何 Phase。
- **通用 Dashboard 统计面板降级**：P1 只保留服务于闭环的“知识总览 / 薄弱点 / 建议 / 待办 / 最近记录”，不做与知识无关的统计卡片。
- **复杂知识图谱、间隔重复、高级分析**：明确推迟到 Horizon，避免 Over-engineering。
