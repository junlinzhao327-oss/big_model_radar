# OpenClaw 生态日报 2026-07-26

> Issues: 318 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-25 23:16 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，现根据 OpenClaw 项目在 2026-07-25 的 GitHub 数据，为您呈现 2026-07-26 的项目动态日报。

---

## OpenClaw 项目动态日报 | 2026-07-26

### 今日速览

今日 OpenClaw 项目社区极其活跃，24小时内产生了 318 条 Issue 讨论和 500 条 Pull Request，但无新版本发布。**项目活跃度评估：极高。** 尽管社区贡献热情高涨，但大量 `P0` 和 `P1` 级别的关键 Bug（包括启动崩溃、数据损坏、配置丢失）仍未解决，且大量 PR 卡在需要维护者评审或产品决策的状态，显示了项目在高速发展期面临的稳定性与效率挑战。安全性与内存管理是今天社区关注的两大核心主题。

### 版本发布
无

### 项目进展

尽管无新版本发布，但今日有 205 个 PR 被合并或关闭，项目仍在稳步推进。以下是几个关键修复与改进：

- **修复 Control UI 渲染崩溃**：[PR #113702](https://github.com/openclaw/openclaw/pull/113702) 修复了在长期运行的聊天会话中，代理创建的 widget 因认证问题停止渲染，变为显示“Unauthorized”原始 JSON 的错误。该 PR 已被合并。
- **修复 TUI 终端输入问题**：[PR #113872](https://github.com/openclaw/openclaw/pull/113872) 解决了 TUI 中 Ctrl+D 无法向前删除字符的问题，提升了用户在终端的编辑体验。该 PR 已被合并。
- **优化内存模块稳定性**：[PR #113471](https://github.com/openclaw/openclaw/pull/113471) 修复了内存核心 (Memory Core) 在切换嵌入（embedding）提供商时，旧提供者未能完全关闭导致进程重叠的 Bug，尤其对使用本地 `llama.cpp` 嵌入的用户影响较大。该 PR 正在等待评审。
- **统一模型发现逻辑**：[PR #113903](https://github.com/openclaw/openclaw/pull/113903) 提出将七个不同提供商扩展中的模型发现逻辑重构为共享的钩子（hook），旨在减少代码重复和降低维护成本。

### 社区热点

今日社区讨论的核心在于 **安全性与系统稳定性**。评论数最多、反应最强烈的几个 Issue 反映了用户在关键场景下的焦虑：

1.  **Memory 安全**：[Issue #7707](https://github.com/openclaw/openclaw/issues/7707) 提出的“按来源的内存信任标签”（Memory Trust Tagging by Source）获得了 21 条评论，是今日讨论最热烈的议题。社区普遍担忧通过网页抓取或第三方技能进行“内存投毒”（Memory Poisoning）攻击，要求系统能区分可信和不可信上下文来源。（👍 0）
2.  **MCP 工具调用审批**：[Issue #78308](https://github.com/openclaw/openclaw/issues/78308) 是关于为 MCP 工具调用引入“渠道中介审批”（Channel-mediated approval）功能的讨论，获得了 15 条评论。用户希望为那些会修改外部状态的敏感 MCP 调用增加一个 `/approve` 确认环节，以提升安全性。（👍 1）
3.  **重大性能与稳定性问题**：[Issue #86996](https://github.com/openclaw/openclaw/issues/86996) 报告了在使用特定模型和内存后端时，系统响应延迟极高、导致钩子超时、启动失败和事件循环停滞的严重问题，获得了 14 条评论和 2 个 👍。这是影响系统核心可用性的关键 Bug。（👍 2）

### Bug 与稳定性

今日报告的 Bug 数量众多，且严重程度较高。以下是按严重性排列的关键问题：

- **P0 (关键)**
    - **启动崩溃**：[Issue #108435](https://github.com/openclaw/openclaw/issues/108435) - 升级到版本 2026.7.1 后，Gateway 因配置问题无法启动。（👍 2）
    - **数据损坏**：[Issue #95515](https://github.com/openclaw/openclaw/issues/95515) - 从版本 6.8 升级到 6.9 时，邮箱频道配置被损坏。**已有修复 PR**。
    - **启动失败**：[Issue #109145](https://github.com/openclaw/openclaw/issues/109145) - v2026.7.1-beta.5 版本中，Gateway HTTP 服务器监听后无法接受连接。
    - **文档与版本脱节**：[Issue #48920](https://github.com/openclaw/openclaw/issues/48920) - 在线文档中描述的 `IsolatedSessions` 配置项在已发布的版本中不存在。（👍 3）

- **P1 (高)**
    - **内存泄漏**：[Issue #87109](https://github.com/openclaw/openclaw/issues/87109) - macOS 上 Gateway 的堆内存空闲时增长至 1GB+, 导致 Cron 任务静默失败。（👍 1）
    - **SQLite 块级事件循环**：[Issue #112423](https://github.com/openclaw/openclaw/issues/112423) - 清理大型 SQLite 事务记录时阻塞了 Gateway 的事件循环。
    - **会话模型锁定**：[Issue #92776](https://github.com/openclaw/openclaw/issues/92776) - 会话模型固定功能永久有效，即使目标模型已恢复，回弹探测机制因上游错误而失效。（👍 1）

- **P2 (中)**
    - **内存管理混乱**：[Issue #43747](https://github.com/openclaw/openclaw/issues/43747) - 不同用户的内存存储方式不一致，有的在 SQLite，有的在文件，导致状态混乱。
    - **富文本渲染回归**：[Issue #112906](https://github.com/openclaw/openclaw/issues/112906) - 在 v2026.7.1 中，打开富文本消息后， markdown 代码块渲染出现问题。
    - **数据丢失风险**：[Issue #113306](https://github.com/openclaw/openclaw/issues/113306) - SQLite 快照恢复过程中，存在崩溃和身份保证缺失的问题。（👍 0，共 13 条评论）

### 功能请求与路线图信号

用户对安全性和权限精细控制的需求非常强烈，这些功能的诉求清晰明确，很可能影响下一版本的规划。

1.  **安全增强**：
    - **内存信任标签**：[Issue #7707](https://github.com/openclaw/openclaw/issues/7707) - 按来源标记内存的可信度，防范投毒攻击。
    - **文件系统沙盒**：[Issue #7722](https://github.com/openclaw/openclaw/issues/7722) - 为工具的文件访问提供可配置的路径白名单和黑名单。（👍 4）
    - **子代理权限控制**：[Issue #15032](https://github.com/openclaw/openclaw/issues/15032) - 支持在生成子代理时为它们单独配置可用的工具，防止权限扩散。

2.  **用户体验与功能优化**：
    - **Control UI 布局改进**：[PR #113712](https://github.com/openclaw/openclaw/pull/113712) 提出添加灵活的多侧边栏聊天布局，以解决会话讨论与其他面板抢占空间的问题。
    - **Codex 用户免 API Key 使用 GPT Live**：[PR #113354](https://github.com/openclaw/openclaw/pull/113354) 提议允许已登录 Codex OAuth 的用户直接在浏览器和 iOS 上体验 GPT Realtime，无需额外配置 API 密钥。这极大了降低了 Talk 功能的使用门槛。
    - **外部验证审批插件**：[PR #113517](https://github.com/openclaw/openclaw/pull/113517) 实现了社区期盼已久的插件外部验证审批合约，为需要更高安全性的操作提供了标准化接口。

### 用户反馈摘要

- **对复杂配置和升级的挫败感**：用户在 [Issue #95515](https://github.com/openclaw/openclaw/issues/95515) 和 [Issue #85844](https://github.com/openclaw/openclaw/issues/85844) 等中表达了升级过程可能导致配置损坏或应用状态不一致的沮丧。特别是 [Issue #48920](https://github.com/openclaw/openclaw/issues/48920) 指出“文档超前于版本”，让用户无法按照文档配置本应存在的功能。
- **对性能问题的严重关切**：[Issue #86996](https://github.com/openclaw/openclaw/issues/86996) 和 [Issue #87109](https://github.com/openclaw/openclaw/issues/87109) 中描述的严重延迟、内存泄漏和任务静默失败，直接影响了核心功能的可靠性，用户的评论充满了紧迫感。
- **对安全性的长期诉求**：多个高互动 Issue（如 #7707， #78308， #7722）都指向对安全的渴求。用户非常担心恶意数据或第三方工具会破坏代理的完整性和安全边界。

### 待处理积压

以下为长期未获得有效处理，但影响重大的 Issue，需提请维护者关注：

- **[P0] [Bug]: Live Docs are ahead of release** [`#48920`](https://github.com/openclaw/openclaw/issues/48920) - 该问题自 2026 年 3 月被提出，至今已超过 4 个月，仍未解决。官方文档与发布版本不匹配，极易误导用户。
- **[P1] [Bug]: Auto-update can leave running gateway with stale hashed bundle imports** [`#85844`](https://github.com/openclaw/openclaw/issues/85844) - 自 5 月下旬报告至今，自动更新可能导致的内部状态不一致问题仍未解决，降低了用户对 OTA 更新机制的信任。
- **[P1] [Bug]: Update 2026.3.24 silently drops config when `HOME` changes** [`#54634`](https://github.com/openclaw/openclaw/issues/54634) - 该 bug 自 3 月底被报告，描述了一个影响服务器部署稳定性的灾难性问题（环境变量变化导致配置静默丢失），但至今未被分配或处理，处于“stale”状态。

---

## 横向生态对比

好的，作为资深技术分析师，我已仔细审阅了今日五个核心开源项目的动态日报。以下是为您生成的横向对比分析报告，旨在为技术决策者和开发者提供宏观洞察与决策参考。

---

### **AI 智能体与个人 AI 助手开源生态横向对比报告**

**报告日期：** 2026-07-26
**分析师：** 资深技术分析师

---

#### **1. 生态全景**

今日，个人AI助手与自主智能体开源生态呈现出**高活跃度与快速迭代**的总体态势，社区贡献热情空前高涨。然而，这种高速发展也伴随着显著的“成长的烦恼”：**稳定性问题（尤其是内存泄漏、启动崩溃、并发处理）和安全性诉求（内存投毒、工具调用审批、凭证管理）成为跨项目的核心痛点**。整体来看，生态正从“功能实现”阶段，加速向“生产级可靠性”和“企业级安全”阶段过渡。开发者社区对**跨模型推理参数统一性、精细化的成本与权限控制、以及无缝的跨平台体验**表现出强烈且一致的渴望。

---

#### **2. 各项目活跃度对比**

| 项目名称 | 核心功能 | 24h Issues 更新数 | 24h PR 更新数 | 新版本发布 | 核心 Bug 数量 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 个人 AI 助手平台 | 318 | 500 | 无 | 极高 (P0 多，大量积压) | **高速发展，但稳定性承压** |
| **Hermes Agent** | 通用 Agent 框架 | 500+ | 500+ | 无 | 高 (P0/P1 有修复响应) | **密集迭代，修复响应快** |
| **OpenHands SDK** | 智能体 SDK | 12 | 12 | 无 | 中 (流式处理问题待解决) | **稳健推进，架构优化期** |
| **Pi** | 终端编码 Agent | 56 | 18 | **v0.82.1** | 中 (TUI/WSL/模型切换) | **活跃健康，维护响应好** |
| **LiteLLM** | LLM API 网关 | 74 | 197 | 无 | 高 (多 P0/P1，合并效率待提升) | **高频修复，待合并队列长** |
| **Temporal** | 工作流引擎 | 0 | 26 | 无 | 低 (已通过 PR 快速修复) | **质量巩固，聚焦新架构稳定性** |

**分析**：
- **Hyper-active & Stressed (超活跃但承压)：** `OpenClaw` 和 `Hermes Agent` 社区体量巨大，贡献者众多，但也因此面临严重的 Bug 积压和 PR 审阅瓶颈。
- **Active & Focused (活跃且聚焦)：** `LiteLLM` 和 `Pi` 在各自的领域（API 网关、编码Agent）内高度活跃，修复效率高。
- **Stable & Solid (稳健且扎实)：** `OpenHands SDK` 和 `Temporal` 虽然活跃度相对较低，但项目把控力强，专注于架构优化和核心系统巩固，体现了成熟项目的特点。

---

#### **3. OpenClaw 在生态中的定位**

- **定位：** 个人AI助手的**核心参照实现**与**综合平台**。其目标是为用户提供一个功能完整、可高度定制的端到端个人AI助手。
- **优势：**
    - **功能广度：** 相较 `Pi`（专注编码）、`Hermes Agent`（通用框架），OpenClaw 集成了对话、记忆、技能、MCP工具、多Agent协作等更为全面的个人助手能力。
    - **社区规模与影响力：** 从 Issue 和 PR 的绝对数量（318 Issues, 500 PRs）来看，其社区活跃度远超其他项目，是生态中“吸引火力”最多的焦点。
- **技术路线差异：**
    - 强调 **`Memory Core`**（记忆核心）作为一等公民，这与 `Hermes Agent` 的插件式记忆管理、`Pi` 的会话压缩式记忆形成对比。
    - 内置 **`Control UI`** 和 **`TUI`**，提供开箱即用的可视化交互，而 `LiteLLM` 和 `Temporal` 则更偏向 API 和后台服务。
- **短板：** 当前最大的挑战是**稳定性与迭代速度的失衡**。大量的 P0/P1 Bug（如启动崩溃、数据损坏）和积压的待处理Issue（如“文档超前于版本”），说明其在快速扩张的同时，质量保障体系（QA 和代码审查）有所滞后。项目正处在一个“为了生存必须解决核心 Bug，为了发展必须快速上线功能”的矛盾期。

---

#### **4. 共同关注的技术方向**

多个项目不约而同地将焦点投向以下领域，这预示着行业未来的发展方向：

| 技术方向 | 涉及项目 | 具体诉求与信号 |
| :--- | :--- | :--- |
| **安全与信任** | **OpenClaw**, **Hermes Agent**, **LiteLLM**, **Pi** | - **内存投毒防范**: 要求按来源区分内存可信度 (OpenClaw #7707) <br> - **工具调用审批**: 为敏感操作引入二次确认 (OpenClaw #78308, Hermes Agent #71616) <br> - **凭证安全**: 零知识证明代理、避免凭证泄露 (Hermes Agent #4656) <br> - **MCP 安全**: 阻止凭证泄露 (LiteLLM #34340) |
| **推理控制与统一** | **OpenHands SDK**, **Pi**, **LiteLLM** | - **`reasoning_effort` 统一**: 要求在所有模型/提供商/代理间标准化“推理努力程度”参数 (OpenHands SDK #3701, #3699)。 |
| **成本与资源管理** | **OpenHands SDK**, **LiteLLM**, **Pi** | - **精细预算与限流**: 多窗口预算、按模型/用户配额管理 (LiteLLM #34500) <br> - **成本归因与追踪**: 流式模式下成本信息不能丢失 (LiteLLM #16021) <br> - **资源使用控制**: 限制Context窗口、可配置工具输出截断 (Pi #7066) |
| **可观测性与调试** | **OpenClaw**, **OpenHands SDK**, **Temporal** | - **监控指标**: 新增队列积压时长等运维指标 (Temporal #11255) <br> - **追踪**: 支持会话级 LLM 调用追踪 (OpenHands SDK #4066) |
| **跨平台与易用性** | **Pi**, **Hermes Agent**, **OpenClaw** | - **WSL 支持**: 处理路径分隔符、权限问题 (Pi #7112, #7064) <br> - **登录与认证**: 简化SSH/远程环境的OAuth流程 (Pi #7114) <br> - **配置自动升级**: 解决升级后配置损坏问题 (OpenClaw #95515) |

---

#### **5. 差异化定位分析**

| 维度 | **OpenClaw** | **Hermes Agent** | **OpenHands SDK** | **Pi** | **LiteLLM** | **Temporal** |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **功能侧重** | 个人助手全功能平台 | 通用 Agent 运行时与框架 | 开发者工具 / SDK | 终端编码 Agent | LLM API 统一网关 | 分布式工作流编排 |
| **目标用户** | 终端用户、自托管爱好者 | Agent 开发者、集成商 | Agent 应用程序开发者 | 软件开发者、工程师 | 平台运维、AI 应用开发者 | 后端/系统工程师 |
| **技术架构** | 单体+模块化，内置 UI | 模块化，插件驱动 | 库/SDK，无 UI | Python TUI 客户端 | 中间件/代理层 | 集群式后台服务 |
| **记忆管理** | 核心特色，分类存储（SQLite/文件） | 插件式，灵活但分散 | `load_memory` 接口，待完善 | 会话压缩，单文件上下文 | 不直接管理 | 不管理（工作流状态） |
| **多模型支持** | 通过 Provider 插件 | 通过 Provider 插件 | 通过 `LLM` 对象抽象 | 集成特定服务（Anthropic等） | **核心卖点**，200+提供商 | 不直接处理 |
| **当前挑战** | 稳定性与 Bug 积压 | PR 审阅瓶颈，桌面端脆弱 | 流式处理正确性 | TUI 性能，WSL/模型兼容性 | 多提供者兼容性，安全与成本追踪 | CHASM 新引擎的边界情况 |

---

#### **6. 社区热度与成熟度**

- **第一梯队 (Hyper-growth with Pain):** **OpenClaw**, **LiteLLM**
    - **特征:** 拥有庞大的社区基础和极高的 Issue/PR 吞吐量。处于快速迭代阶段，功能不断增多，但稳定性问题突出，Bug 修复速度难以追赶社区反馈速度。项目处于“飞速成长但四处漏水的阶段”。
- **第二梯队 (Active Maturation):** **Hermes Agent**, **Pi**
    - **特征:** 社区活跃，功能迭代和 Bug 修复并重。项目方对社区反馈响应迅速，具有清晰的迭代节奏，并开始关注架构优化和测试基础设施。处于从“能用”到“好用”的过渡期。
- **第三梯队 (Stable & Polishing):** **OpenHands SDK**, **Temporal**
    - **特征:** 活跃度相对平稳，但项目演进方向明确，专注于核心架构的巩固、API 的规范化和测试体系的完善。Bug 通常能较快被修复，对新的功能请求持审慎态度。处于质量巩固和长期稳健发展的阶段。

---

#### **7. 值得关注的趋势信号**

1.  **从“对话”到“自主执行”：安全是第一道门槛。** 当 Agent 被赋予执行代码、操作数据库、控制外部系统的能力时，社区对**内存投毒**、**工具调用审批**、**子代理权限隔离**、**文件系统沙盒**等安全机制的呼声达到顶峰。开发者必须将安全作为 Agent 系统的“一等公民”来设计，而非事后补丁。

2.  **从“模型黑盒”到“可控推理”：** 社区不再满足于简单的“提问-回答”。开发者渴望通过 `reasoning_effort` 等标准化参数，像控制 CPU 频率一样精细地控制 AI 的“思考深度”，这是 Agent 从玩具走向生产力的关键一步。**统一的推理控制接口**将是下一代 Agent 框架的核心竞争力。

3.  **从“单点胜利”到“成本与可观测性治理”：** 随着 Agent 的普及，**成本失控**和**调试困难**正成为大规模部署的拦路虎。社区对精细预算（LiteLLM）、流式成本追踪（LiteLLM）以及会话级调试追踪（OpenHands SDK）的需求强烈，表明行业正在为 AI 智能体的商业化落地做准备。

4.  **从“API 聚合”到“全链路管理”：** `LiteLLM` 的繁荣表明，简单的 API 聚合已不能满足需求。开发者需要的是一个集**路由、限流、安全、成本、可观测性**于一体的全生命周期管理平台。这预示着未来 API 网关形态的演进方向。

5.  **基础设施与上层应用的分化：** `Temporal`（工作流引擎）和 `LiteLLM`（API 网关）这类基础设施项目，与 `OpenClaw`、`Hermes Agent`、`Pi` 等上层应用项目正在形成明确的分工。底层的稳定性与高可用性将为上层的创新提供坚实底座。

**对 AI 智能体开发者的参考价值：**
- **短期（1-3个月）：** 优先解决 Agent 的安全性（审批、沙盒）和稳定性（内存泄漏、崩溃恢复）。同时评估和集成统一的推理控制参数。
- **中期（3-6个月）：** 构建或选择成熟的可观测性和成本治理体系。关注 `Temporal` 等底层基础设施的成熟度，考虑用其编排复杂的 Agent 工作流。
- **长期（6-12个月）：** 拥抱平台化趋势，区分“基础设施”与“应用”。选择像 `LiteLLM` 这样能提供全链路管理能力的网关，并将核心业务逻辑构建在 `OpenClaw` 或 `Hermes Agent` 等社区活跃、持续进化的平台之上。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，这是为您生成的 Hermes Agent 开源项目动态日报。

---

# Hermes Agent 项目动态日报 — 2026-07-26

### 1. 今日速览

今日 Hermes Agent 项目活跃度极高，Issue 与 PR 的更新数量均达到 500 条，显示出社区参与热情和项目维护强度的双重高峰。虽然新版本发布数为零，但项目在核心功能修复上取得了显著进展，多个关键 Bug 得到了修复性 PR 的响应。社区讨论焦点集中在**插件接口扩展**、**Ollama 集成优化**以及 **Buzz 即时通讯集成**等方向，反映出用户对扩展性和易用性的强烈诉求。总体来看，项目处于密集迭代与社区共创阶段，Bug 修复速度与社区需求响应能力均在稳步提升。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日一批重要的 Pull Request 被合并或关闭，标志着项目在稳定性和功能性上均有推进：

- **桌面应用稳定性提升**：
    - `#68776` **已关闭**，`#71632` **已关闭**: 修复了桌面端 `/goal` 命令的四个复合 Bug，包括参数编辑、队列冲突和指令渲染问题，显著提升了 `/goal` 功能的可靠性和用户体验。
    - `#71617` **已关闭**: 修复了网关在 `launchd` 进程管理下的监督状态报告错误，使运维诊断信息更加准确。
- **平台兼容性修复**：
    - `#71381` **已关闭**: 修复了在 Windows ARM64 (WoA) 上更新的完整性检查误报问题，解决了特定硬件上更新的阻塞。
- **插件与集成**：
    - `#71616` **已关闭**: 新增了 Telegram 适配器中针对邮件审批的确定性操作回调路由，增强了邮件管理插件的可控性。
    - `#71623` **已关闭**: 工件工具（Artifact Tool）现在支持 `html` 类型，允许 Agent 维护和渲染自包含的 HTML 文档（如仪表盘、报告），拓宽了 Agent 的输出形式。
- **核心系统修复**：
    - `#71631` **已合并**: 修复了 `hermes update` 在遇到有漏洞的 SQLite 版本时，无法自动提供修复版 Python 运行时的问题。

### 4. 社区热点

今日讨论最热烈的议题体现了社区对项目未来架构和集成能力的深度思考：

- **插件接口扩展** (`#64182`， 16 条评论): 这枚追踪 Issue 集中了社区对插件接口的期望，是长队列 PR 上线的参考蓝图。核心诉求是**官方化插件开发标准，解决长期存在的阻塞问题**。这标志着社区从使用插件转向了定义插件生态。
    [链接](https://github.com/NousResearch/hermes-agent/issues/64182)
- **Ollama 集成优化** (`#4505`， 14 条评论): 开发者们热烈讨论通过 Ollama 原生 API (`/api/chat`) 替代 OpenAI 兼容端点 (`/v1/chat/completions`)，以获得真正的增量流式传输和更优的功能支持。反映了用户对**极致本地推理性能和功能完整性**的追求。
    [链接](https://github.com/NousResearch/hermes-agent/issues/4505)
- **Buzz 消息集成** (`#68871`， 11 条评论， 10 👍): 社区对集成 Block 公司开源的工作空间 “Buzz” 呼声很高。用户期望 Agent 能直接加入 Buzz 的群组，实现**人机同室协作**，这是一个典型的、面向未来的团队协作场景需求。
    [链接](https://github.com/NousResearch/hermes-agent/issues/68871)

### 5. Bug 与稳定性

今日报告的 Bug 数量较多，但大部分已有修复 PR 进行响应，项目整体响应能力良好。按严重程度排列如下：

- **P0 (严重)**
    - `#64934` **（已关闭）** : **并发会话损坏**。两个回合可能会在同一个网关节点的会话上并发运行，导致日志交织、永久错乱。这是严重的并发问题，已被修复并关闭。
    [链接](https://github.com/NousResearch/hermes-agent/issues/64934)

- **P1 (高)**
    - `#63078` **（已关闭）** : 桌面端新会话第一条消息导致空白会话，现已修复。
    [链接](https://github.com/NousResearch/hermes-agent/issues/63078)

- **P2 (中)**
    - `#67600` : 桌面端默认配置下的会话侧边栏为空，但后端数据正常。这是一个前端渲染问题。
    [链接](https://github.com/NousResearch/hermes-agent/issues/67600)
    - `#63047` : macOS 27 beta 上桌面应用在发送约5条消息后完全无响应，包括设置界面。
    [链接](https://github.com/NousResearch/hermes-agent/issues/63047)
    - `#69078` : xAI Grok 4.5 模型因 “Invalid PNG image” 错误导致会话永久损坏。问题在于图像处理与错误恢复机制。
    [链接](https://github.com/NousResearch/hermes-agent/issues/69078) (已有 `#71635` PR 修复类似图像生成问题)
    - `#71514` : 桌面端连接远程网关时，若 OAuth 已持有cookie，仍会在 `/api/health` 接口上因 401 错误陷入就绪性检查死循环。
    [链接](https://github.com/NousResearch/hermes-agent/issues/71514) (已有 `#71628` PR 提议延迟启动流会话直到 SSE 就绪)

- **修复 PR 已就绪的高优先 Bug**:
    - `#71629` **（开放中）** : 提供了非破坏性的 `state.db` 恢复方案，修复了会话数据库损坏时只能「原地修复」或「无提示失败」的问题。
    [链接](https://github.com/NousResearch/hermes-agent/pull/71629)
    - `#71635` **（开放中）** : 修复了 Codex 认证下的图像生成功能对所有账户都失效的 Bug，并修正了误导用户的错误信息。
    [链接](https://github.com/NousResearch/hermes-agent/pull/71635)

### 6. 功能请求与路线图信号

除了社区热点的插件扩展和 Buzz 集成，以下新功能请求信号强烈，可能被纳入后续版本：

- **凭证代理守护进程** (`#4656`): 提出了一个零知识证明的 HTTP/HTTPS 代理方案，以解决凭证泄露的风险，这将是**安全架构上的重大升级**。
    [链接](https://github.com/NousResearch/hermes-agent/issues/4656)
- **MCP 智能加载** (`#66473`): 提出了延迟连接、工具预算和按会话范围的 MCP 服务器加载方式，旨在**解决资源浪费和上下文窗口限制**，这是 MCP 集成走向成熟的必经之路。
    [链接](https://github.com/NousResearch/hermes-agent/issues/66473)
- **Phi-4 Vision 集成** (`#70384`): 一个被广泛关注的 PR，尽管需要功能评审，但显示了社区对多模态模型支持的渴望。
    [链接](https://github.com/NousResearch/hermes-agent/pull/70384)

### 7. 用户反馈摘要

从 Issue 评论和 Bug 描述中，可以提炼出以下用户痛点：

- **“我的 PR 在队列里吃灰”**: `#64182` 的发起人和评论者明确表达了大量积压 PR 的痛点，核心诉求是项目方加快插件接口标准的制定，以便长期等待的贡献能够落地。
- **“桌面应用太容易坏了”**: 多个关于桌面端会话空白 (`#63078`)、无响应 (`#63047`)、侧栏消失 (`#67600`) 的反馈，集中反映了用户对桌面客户端稳定性的不满。
- **“我的会话怎么突然就废了？”**: 用户对因图片格式错误 (`#69078`) 或并发问题 (`#64934`) 导致的“会话永久损坏”感到极度沮丧，因为唯一的恢复方法是删除会话，意味着丢失所有历史记录。
- **“配置和 UI 总对不上”**: 用户抱怨 CLI 和 GUI 之间存在配置不一致的问题 (`#71298`)，例如 `providers` 和 `custom_providers` 的分离存储导致显示混乱，增加了配置的困惑。
- **“认证流程链断掉了”**: 用户在使用远程网关和 OAuth 时遇到死循环 (`#71514`) 或认证请求无法弹出 (`#51873`)，表明认证流程的健壮性有待提升。

### 8. 待处理积压

以下 Issue 持续开放且未曾得到充分回应，提醒维护者关注：

- **`needs-repro` & `needs-decision` 标记的旧 Issue**:
    - `#58458` (26天前): Windows 上 Matrix 后端因 `python-olm` 编译需要 `make` 而失败。该问题缺少维护者的决策和 Windows 上的复现引导。
    [链接](https://github.com/NousResearch/hermes-agent/issues/58458)
    - `#66868` (7天前): Cron 任务调用主模型时出现 401 认证失败，即使配置正确。此问题影响了自动化工作流的核心功能，需要维护者介入判断。
    [链接](https://github.com/NousResearch/hermes-agent/issues/66868)

- **长期未合并的 PR**:
    - `#55295` (26天前): 一个小而关键的可用性修复，当 basic_auth 配置但 basic 插件被禁用时提供提示。该 PR 已标记为 `invalid`，但问题本身仍可能对用户造成困扰，需要明确是修复方向错误还是已被标记为暂不处理。
    [链接](https://github.com/NousResearch/hermes-agent/pull/55295)

- **重大功能讨论与决策**:
    - `#66473` (8天前): MCP 智能加载的讨论。这是一个有潜力的架构改进，但需要维护者给出反馈，以决定社区贡献的努力方向。
    [链接](https://github.com/NousResearch/hermes-agent/issues/66473)
    - `#4656` (近4个月): 凭证代理守护进程。这是一个影响深远的安全架构提案，长期未得到正式回复，可能会影响贡献者的积极性。
    [链接](https://github.com/NousResearch/hermes-agent/issues/4656)

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是根据您提供的OpenHands SDK（software-agent-sdk）GitHub数据生成的2026年7月26日项目动态日报。

---

## OpenHands SDK 项目动态日报 | 2026年07月26日

---

### 1. 今日速览

今日项目动态活跃，共处理了12条Issue和12条PR，开发与维护节奏稳健。**核心亮点**在于PR合并与关闭数量（4个）虽然不算多，但解决了文档易用性（Action摘要展示）和核心架构（Schema字段治理与状态恢复权威性）等关键问题。此外，社区对**推理（Reasoning）effort参数统一**、**ACP代理配置**以及**流式处理稳定性**等话题表现出浓厚兴趣，是未来版本演进的重要方向。项目整体健康度良好，待合并的PR数量（8个）略多，需关注其审阅与集成进度。

### 2. 版本发布

**（无）**
过去24小时内无新版本发布。

### 3. 项目进展

今日合并/关闭了4个重要的PR，推动了项目在易用性、架构健壮性和API规范化方面的进步：

- **增强用户确认体验**:
    - **[#4211 (CLOSED)](https://github.com/OpenHands/software-agent-sdk/pull/4211) & [#4218 (CLOSED)](https://github.com/OpenHands/software-agent-sdk/pull/4218)**: 这两个紧密相关的PR（来自不同作者，内容近似）均致力于改进确认模式（confirmation mode）下的用户界面。它们将原来显示原始Action数据转储的预览，替换为更友好的LLM-provided action summary，**直接解决了社区反馈的“操作模糊”问题**，提升了用户交互的可理解性。

- **API架构规范化**:
    - **[#4220 (CLOSED)](https://github.com/OpenHands/software-agent-sdk/pull/4220)**: 该PR致力于显式地整理嵌套的Schema字段。这通常意味着更好地控制API的生成与序列化行为，是API走向稳定与清晰的重要一环。

- **状态恢复机制改进**:
    - **[#4205 (CLOSED)](https://github.com/OpenHands/software-agent-sdk/pull/4205)**: 在Agent Settings Schema中暴露了 `agent_context.load_memory`。这为在不同场景下（如会话恢复或复制）更精细地控制“记忆加载”行为奠定了基础，增强了框架的灵活性。

这些合并表明，项目团队正在积极回应社区反馈，并稳步推进底层架构的精细化工作。

### 4. 社区热点

今日讨论最活跃、社区反应最强烈的议题主要集中在以下两个方向：

- **AI推理能力（effort参数）的统一与暴露**:
    - **[#3701 (OPEN)](https://github.com/OpenHands/software-agent-sdk/issues/3701)** 与 **[#3699 (OPEN)](https://github.com/OpenHands/software-agent-sdk/issues/3699)** 成为今日关注焦点。这两个Issue分别提出了将`reasoning effort`（推理努力程度）参数**统一为provider-agnostic（与供应商无关）** 的LLM参数，以及**作为ACP代理（如Claude Code）的一等公民参数暴露**。这反映出社区不再满足于各模型内部的自有配置，而是渴望一个更简洁、统一的编程接口来控制AI的“思考深度”，是提升Agent可控性的核心诉求。

- **长期追踪的“每日集成运行”**:
    - **[#2078 (OPEN)](https://github.com/OpenHands/software-agent-sdk/issues/2078)**: 虽然这是一个长期存在的追踪Issue，但其**148条评论**使其成为评论区最活跃的话题。它代表了项目持续集成与测试的稳定性保障。社区在此讨论集成测试的执行情况、遇到的问题以及失败的根源，是项目健康度的重要晴雨表。

### 5. Bug 与稳定性

今日报告的Bug数量较少，且已有相应的修复在审或已提交，总体稳定性良好。按严重等级排列如下：

- **中高严重性 - 流式处理正确性与资源安全Bug**:
    - **[#4077 (OPEN)](https://github.com/OpenHands/software-agent-sdk/issues/4077)**: 报告者在审计`token/event streaming pipeline`时发现了正确性和资源安全方面的问题。虽然最终持久化记录是正确的，但流式传输中间过程的bug可能影响前端用户体验或资源消耗。此问题需要深入了解流处理逻辑，影响面可能较广。

- **中低严重性 - LLM模型兼容性与配置问题**:
    - **[#3500 (CLOSED)](https://github.com/OpenHands/software-agent-sdk/issues/3500)**: 报告了 **Anthropic Opus 4.8** 模型在OpenHands中不支持的问题（已关闭）。这表明已在社区反馈或内部测试中识别并处理了与特定LLM模型的兼容性问题。
    - **[#4032 (关联PR)](https://github.com/OpenHands/software-agent-sdk/pull/4221)**: 虽然未直接出现在数据中，但PR [#4221](https://github.com/OpenHands/software-agent-sdk/pull/4221) 旨从根本上修复**agent-server重启后LLM超时恢复**的bug，说明该问题已被定位并有了解法。

**已有对应修复的Bug**：
- 针对流式处理的`#4077`，目前尚无直接的Fix PR，但有PR [#4221](https://github.com/OpenHands/software-agent-sdk/pull/4221) 试图解决与LLM配置持久化相关的问题，可能间接改善部分场景的稳定性。

### 6. 功能请求与路线图信号

今日的新需求集中在增加Agent的自主性和可控性上，结合已有PR，可以判断以下功能有望进入未来版本：

- **“Ask Oracle”工具 (Agent自主求助)**: **[#3672 (OPEN)](https://github.com/OpenHands/software-agent-sdk/issues/3672)** 提出当Agent卡住或不确定时，可以**请求一个预配置的“Oracle”LLM给出第二意见**。这定义了Agent在复杂决策场景下的回退与优化策略，有潜力成为Agent工具箱中的一个重要能力。

- **统一推理effort参数**: 如前所述，**[#3701](https://github.com/OpenHands/software-agent-sdk/issues/3701)** 和 **[#3699](https://github.com/OpenHands/software-agent-sdk/issues/3699)** 是路线图中的明确信号。它们与 **[#4159 (OPEN)](https://github.com/OpenHands/software-agent-sdk/pull/4159)**（集中化LLM调用上下文）的目标一致，都旨在将LLM的配置和调用逻辑标准化、集中化。这两点极有可能被纳入下一版本的规划。
- **Conversation级别的LLM Headers**: **[#4066 (OPEN)](https://github.com/OpenHands/software-agent-sdk/pull/4066)** 提出支持 conversation-scoped 的LLM Headers，允许在一次对话中跟踪所有LLM调用，便于调试和审计，是增强可观测性的重要信号。

### 7. 用户反馈摘要

从今日的Issues评论中可以提炼出以下用户反馈：

- **痛点：操作反馈不直观**:
    - 用户在 [#4210 (CLOSED)](https://github.com/OpenHands/software-agent-sdk/issues/4210) 中反馈，在确认模式下，预览的操作是“raw action dumps”（原始Action数据转储），难以理解。**对应的修复PR [#4211](https://github.com/OpenHands/software-agent-sdk/pull/4211) 和 [#4218](https://github.com/OpenHands/software-agent-sdk/pull/4218) 已经合并**，直接回应了此痛点。这表明项目对用户反馈的响应非常迅速。

- **使用场景：无缝集成前端体验**:
    - 用户在 [#3658 (CLOSED)](https://github.com/OpenHands/software-agent-sdk/issues/3658) 中描述了安装SDK后只能得到headless API server，需要额外安装Node.js包才能获得前端UI的场景。这表明社区对“**安装即用**”的集成前端体验有强烈需求。

- **问题排查：模型参数支持不足**:
    - 用户在 [#3500 (CLOSED)](https://github.com/OpenHands/software-agent-sdk/issues/3500) 中遇到新Anthropic模型不被支持的问题。这提醒项目组需要持续跟进并更新对主流LLM提供商新模型的支持，以避免用户因模型选择受限而产生挫败感。

### 8. 待处理积压

以下项目存在长时间未响应或未解决的迹象，值得维护者关注：

- **[#2667 (CLOSED)](https://github.com/OpenHands/software-agent-sdk/issues/2667)**: 关于“研究在保持与持久化会话向后兼容性的同时更新工具集的策略”。虽然标记为已关闭，但所讨论的“如何演进工具而不断档”是一个长期且架构性的挑战，其解决方案直接影响项目的稳定性。该Issue可能已内部消化，但社区仍可能关注其后续进展。
- **[#3503 (OPEN)](https://github.com/OpenHands/software-agent-sdk/pull/3503)**: 为`AgentSettingsBase`添加公共`from_persisted()`入口点的PR，自6月4日创建以来已超过50天仍在开放状态。该PR解决的是一个重要的API迁移和易用性问题，长期积压可能会影响下游开发者的工作流程。需要评估其阻塞原因，是功能上存在争议还是缺少审阅者。
- **[#2078 (OPEN)](https://github.com/OpenHands/software-agent-sdk/issues/2078)**: 作为**每日集成运行追踪器**，148条评论本身就是一种“积压”信号，意味着日常集成过程中不断产生问题或需要人工干预。虽然属于常规工作，但高评论数可能暗示集成测试的稳定性或自动化程度有待提升。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，这是为您生成的 Pi 项目动态日报。

---

# Pi 项目动态日报 | 2026-07-26

## 今日速览

过去 24 小时内，Pi 项目在修复关键 Bug 的同时，也发布了新版本并持续推进新功能。社区反馈活跃，共处理了 56 条 Issue 和 18 个 PR，其中一半以上的 Issue 和 PR 已关闭/合并。核心围绕 **TUI 稳定性**、**模型切换/兼容性** 和 **WSL 路径处理** 等真实痛点展开。新版本 v0.82.1 已发布，重点引入了 **Claude Opus 5** 支持。项目整体活跃度极高，维护者响应迅速，健康度良好。

## 版本发布

### v0.82.1
- **链接**: [https://github.com/earendil-works/pi/releases/tag/v0.82.1](https://github.com/earendil-works/pi/releases/tag/v0.82.1)
- **主要更新内容**:
    - **新增模型支持**: 正式在 Anthropic 和 Amazon Bedrock 上集成 **Claude Opus 5**。该模型支持自适应思考（`xhigh` 级别）、推理配置文件和提示缓存。
- **已知问题与迁移注意事项**:
    - 当前版本依赖的 `brace-expansion@5.0.7` 存在一个 DoS 漏洞 (`CVE-2026-14257`)，官方建议升级到 `5.0.8+`。
    - 部分用户报告从 v0.82.0 升级后出现 `bash` 工具验证报错，项目团队正跟踪处理 (#7069)。

## 项目进展

今日合并/关闭的关键 PR 清晰地展示了项目在 **稳定性、跨平台兼容性和测试基础设施** 上的投入：

- **核心稳定性与 Bug 修复**:
    - [#7116 - fix(tui): truncate over-width lines instead of crashing](https://github.com/earendil-works/pi/pull/7116): 修复了当渲染行超过终端宽度时，TUI 会直接崩溃的严重问题，改为安全截断。
    - [#7106 - fix(coding-agent): exclude directories from resource loader](https://github.com/earendil-works/pi/pull/7106): 修复了将目录作为资源文件读取时产生 `EISDIR` 警告的问题。
    - [#7091 - fix(coding-agent): reject overlapping user bash commands](https://github.com/earendil-works/pi/pull/7091): 拒绝在用户 `bash` 命令执行期间发起的新 RPC 请求，防止状态混乱。
    - [#7112 - fix(coding-agent): normalize path separators in formatCwdForFooter for cross-platform footer display](https://github.com/earendil-works/pi/pull/7112): 修复了 Windows 路径在终端底部状态栏显示为 `~\project` 而非正确格式 `~/project` 的跨平台 Bug。
    - [#7032 - fix(coding-agent): expose unavailable scoped models](https://github.com/earendil-works/pi/pull/7032): 改进了当配置的模型不可用时（如未上线）的用户体验，使其在 `/models` 列表中明确显示为“不可用”状态。
- **新模型与集成**:
    - [#7081 - feat(ai): support Claude Opus 5 on Bedrock](https://github.com/earendil-works/pi/pull/7081): 完成在 Amazon Bedrock 上对 Claude Opus 5 的适配，并启用了必需的“自适应思考”功能。
- **测试与评估基础设施**:
    - [#7085 - feat(coding-agent): add vitest eval harness](https://github.com/earendil-works/pi/pull/7085): 新增了基于 `vitest-evals` 的正式评估测试框架，为未来质量保障奠定基础。

## 社区热点

今日最受关注的 Issue 反映了用户在特定企业环境下的核心痛点：

- **Issue #6768: `[bug] Compaction using Copilot Enterprise not possible`**
    - **作者**: @MojangPlsFix | **评论**: 13 | **👍**: 11
    - **链接**: [https://github.com/earendil-works/pi/issues/6768](https://github.com/earendil-works/pi/issues/6768)
    - **分析**: 这是今日评论最多、反响最强烈的问题。用户报告在使用 Copilot Enterprise 许可证时，Pi 的 Context 压缩功能完全失效，无论是通过 OpenAI 还是 Anthropic 模型都会报错。背后是 **企业对 Key 管理和成本控制** 的强需求，Copilot Enterprise 是许多企业用户的选择，此问题严重阻碍了这些用户使用 Pi 进行长时间连续对话。它的高赞和高评论数凸显出这是影响面很广的关键阻塞性问题。

## Bug 与稳定性

| # | 严重程度 | 问题描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **#6768** | ★★★★★ (严重) | 使用 Copilot Enterprise 时，Context 压缩功能完全失效，导致无法进行长对话。 | 未关闭，无 PR |
| **#6665** | ★★★★ (高) | TUI 在流式输出时，因未缓存的 `Intl.Segmenter` 导致一个核心被占满至 100%，性能极差。 | 未关闭，正在处理中 |
| **#7064** | ★★★★ (高) | WSL 环境下，绝对路径处理错误，导致 `read`、`write`、`edit` 等核心工具频繁失败，退化为全量重写（慢且浪费 Token）。 | 未关闭，无 PR |
| **#7052** | ★★★ (中) | 当会话接近上下文窗口上限时，错误地显示“达到输出 Tokens 上限”，可能打断正常推理流程，令用户困惑。 | 已关闭 |
| **#7020** | ★★★ (中) | 部分长时间运行的“协调”类会话在 Context 压缩后无响应，表现为“卡死”，Beta 用户反馈影响大。 | 未关闭，正在处理中 |
| **#5990** | ★★ (低) | 当确认/选择对话框内容超出终端高度时，TUI 持续闪烁、重绘。 | 未关闭，正在处理中 |
| **#5593** | ★★ (低) | Tab 补全斜杠命令后自动插入空格，导致无法正确触发参数补全，影响操作流畅度。 | 未关闭，正在处理中 |

## 功能请求与路线图信号

本周的功能请求呈现出明显的 **三大方向**：

1.  **优化会话控制与效率**:
    - 用户 @yychyo 提出 [#7066 **将工具输出截断限制可配置化**](https://github.com/earendil-works/pi/issues/7066)，希望在上下文管理上给予用户更多控制权，并已有关联的关闭PR。这可能在下个版本中关注。
    - 用户 @misunders2d 建议 [#5137 **增加头部栏工具折叠输出模式**](https://github.com/earendil-works/pi/issues/5137)，以更紧凑的方式展示工具调用，减少视觉噪音。

2.  **外部生态系统集成**:
    - 多位用户（@smakosh, @steebchen）及自动化机器人建议 [#7108, #7107, #7104 **为自定义 provider 转发会话亲和性头**](https://github.com/earendil-works/pi/issues/7108)，表明社区对公司内部自建成本地网关的强烈需求。
    - 用户 @rgarcia 提交了 [PR #7114 **为 OpenRouter OAuth 登录增加手动 URL 回退功能**](https://github.com/earendil-works/pi/pull/7114)，这直接解决了远程机器上无法使用本地回调的痛点，极有可能被合并。

3.  **模型管理与切换**:
    - 用户 @rock3r 希望 [#7087 **通过 RPC 调用强制模型刷新**](https://github.com/earendil-works/pi/issues/7087)，不再等待固定冷却期。这背后反映了高级用户对动态管理模型列表的需求。

## 用户反馈摘要

- **对 TUI 性能的不满**: 多位用户明确指出了 TUI 的性能和稳定性问题，如全核心占用 (#6665) 和崩溃 (#6050, #7116)，这直接影响核心使用体验。有用户形容“滚动条跳到对话开始处”的现象很恼人 (#6050)。
- **WSL 用户的困境**: WSL 用户的反馈 (#7064) 非常具体，指出“路径处理失败”导致日常的读写编辑操作效率低下，是一个影响生产力的硬伤。
- **对登录流程的期待**: SSH 或远程环境下的用户（@rgarcia）对 OpenRouter 登录流程提出了现实的改进需求（#7114, #7078），表明 Pi 的远程使用场景正在增加。
- **对模型切换困惑**: 用户 @dust617 详细描述了切换模型导致会话崩溃的多种情况 (#7067, #7065)，并提供了清晰的复现步骤，抱怨“切换模型会频繁地搞坏会话”，说明此场景下的健壮性有待加强。

## 待处理积压

- **#6768 - Compaction using Copilot Enterprise not possible**
    - 这是目前社区情绪最高、影响最广的 Issue。11个👍和13条评论的高热度表明这不仅仅是个别问题，而是社区急需解决的硬需求。建议优先处理。
- **#5990 - TUI flickers when dialog is taller than terminal**
    - 这是一个自6月23日就存在的旧 Issue，虽已标记为“inprogress”，但长时间未解决。持续近一个月，影响用户观感。
- **#5593 - Tab-completing a slash command inserts trailing space**
    - 自6月10日报告，影响日常交互流畅性，同样标记为“inprogress”但超期一个月，值得关注。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 | 2026-07-26

基于 GitHub 数据（过去 24 小时），BerriAI/litellm 保持极高活跃度，社区反馈密集，团队合并/关闭 PR 效率显著提升，但待合并队列仍偏长。以下为详细分析。

---

## 1. 今日速览

- **Issue 活跃**：74 条更新（新开/活跃 55，关闭 19），其中 DeepSeek V4 Pro 多轮对话 Bug 已被关闭，但仍有大量开放性缺陷报告。
- **PR 吞吐**：197 条更新（待合并 115，已合并/关闭 82），修复面覆盖成本归属、流式处理、MCP 安全、测试稳定性等关键领域。
- **发布状态**：无新版本发布，项目正处于高频 fix 阶段，下一个候选版本（或 hotfix）预计很快推出。
- **总体健康度**：社区热情高涨，但稳定性问题（特别是多模型兼容性、caching 和 guardrails 方面）仍需持续投入。待合并 PR 数量偏多（115），合并效率有待观察。

---

## 2. 版本发布

**无** – 过去 24 小时未发布任何新版本。

---

## 3. 项目进展

今日合并/关闭了 82 个 PR，重要进展包括：

| PR | 内容 | 影响 |
|----|------|------|
| [#34453](https://github.com/BerriAI/litellm/pull/34453) | fix(cost-optimization): 固定成本优化图表纵轴起点，避免单日数据点显示为孤立点 | 提升 UI 体验 |
| [#34664](https://github.com/BerriAI/litellm/pull/34664) | fix(e2e): 阻止测试破坏共享代理的 Redis 状态 | 测试基础稳定化 |
| [#34192](https://github.com/BerriAI/litellm/pull/34192) | fix(batches): 使用 unified_object_id 游标分页管理批处理列表 | 解决批次遗漏与翻页错误 |
| [#34340](https://github.com/BerriAI/litellm/pull/34340) | fix(mcp): 停止在工具调用 403 错误中泄漏上游服务器凭证 | **安全修复** |
| [#34456](https://github.com/BerriAI/litellm/pull/34456) | fix(batches): 将 Vertex passthrough 批次成本正确关联到 key/team/tags | 成本归属准确性提升 |
| [#34637](https://github.com/BerriAI/litellm/pull/34637) | fix(bedrock): 防止重新播放已过期的 Google OIDC 令牌 | 强化 AWS STS 认证可靠性 |

项目整体在**安全性、成本归属、测试基础**三个维度向前迈进了实质性一步。

---

## 4. 社区热点

| Issue / PR | 讨论热度 | 核心诉求 |
|------------|---------|----------|
| [#26395](https://github.com/BerriAI/litellm/issues/26395) **[CLOSED]** | 22 评论, 👍25 | DeepSeek V4 Pro 多轮对话失败 – 用户高度期待该模型，已关闭说明已有修复 |
| [#16021](https://github.com/BerriAI/litellm/issues/16021) | 16 评论, 👍3 | OpenRouter 流式成本信息丢失 – 用户对成本准确性敏感，长期未解决 |
| [#25762](https://github.com/BerriAI/litellm/issues/25762) | 15 评论, 👍14 | **SSO 用户数限制** – Standard Plan 仅限 5 名 SSO 用户，用户不满，强烈要求放开限制 |

**分析**：用户对主流模型（DeepSeek V4 Pro）的集成质量要求很高；成本可见性（流式模式）仍是痛点；企业级用户对 SSO 配额有明显抵触情绪。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue | 描述 | 是否有 Fix PR |
|---------|-------|------|--------------|
| 🔴 P0 / 阻塞 | [#14052](https://github.com/BerriAI/litellm/issues/14052) | `x-litellm-tags` 未能路由到正确模型，且无 fallback 优先级 | 无 |
| 🔴 P0 / 阻塞 | [#26398](https://github.com/BerriAI/litellm/issues/26398) | MCP Tool 调用返回 400 “超过64字符” | 无 |
| 🟠 高 | [#33820](https://github.com/BerriAI/litellm/issues/33820) | aiohttp 3.14.x 连接池污染导致跨提供者超时 | 无 |
| 🟠 高 | [#26413](https://github.com/BerriAI/litellm/issues/26413) | `think: false` 被忽略，仍返回 reasoning_content | 无 |
| 🟠 高 | [#24152](https://github.com/BerriAI/litellm/issues/24152) | Key 级别 per-model 限流不触发 fallback | 无 |
| 🟡 中 | [#32903](https://github.com/BerriAI/litellm/issues/32903) | `GET /v1/models` 所有模型显示 `owned_by: "openai"` | 无 |
| 🟡 中 | [#34636](https://github.com/BerriAI/litellm/issues/34636) | Redis 缓存测试在使用 `url` 字段时失败 | 无 |
| 🟢 低 | [#20078](https://github.com/BerriAI/litellm/issues/20078) | Qwen3-TTS 的 `voice` 参数强制 | 无 |

已有对应修复 PR 的 Bug（部分在开放 PR 中）：
- [#33665](https://github.com/BerriAI/litellm/pull/33665) – MCP 工具按 `server_id` 路由，避免名称冲突
- [#34660](https://github.com/BerriAI/litellm/pull/34660) – Compresr 保留 cache_control 断点
- [#34658](https://github.com/BerriAI/litellm/pull/34658) – Azure Realtime WebSocket 支持 Entra ID 无 api-key 认证
- [#33002](https://github.com/BerriAI/litellm/pull/33002) – 将异步流终结从事件循环卸载（性能改进）

---

## 6. 功能请求与路线图信号

| 功能请求 | 需求描述 | 是否有对应 PR / 可能纳入 |
|---------|----------|--------------------------|
| [#25762](https://github.com/BerriAI/litellm/issues/25762) | **无限制 SSO**（取消 Standard Plan 5 用户限制） | 无，但呼声极高 |
| [#34662](https://github.com/BerriAI/litellm/issues/34662) | 提供凭证的**定期可用性计划**（类似定时上下线） | 无（新提交） |
| [#33960](https://github.com/BerriAI/litellm/issues/33960) | RoutingGroup 支持 `allowed_fails`、`cooldown_time` 等字段 | 无，但设计合理 |
| [#34357](https://github.com/BerriAI/litellm/issues/34357) | 集成 **OpenInfer** 提供者 | 无（社区贡献请求） |
| [#34500](https://github.com/BerriAI/litellm/pull/34500) | 为用户添加多窗口预算（budget_limits） | **已开放 PR**，很可能进入下一版本 |
| [#34630](https://github.com/BerriAI/litellm/pull/34630) | `/key/list` 新增按用户邮箱过滤 | **已开放 PR** |
| [#33002](https://github.com/BerriAI/litellm/pull/33002) | 流式终结卸载到工作线程 | **已开放 PR** |

**路线图信号**：多窗口预算（#34500）和 UI 查询能力（#34630）是短期内最可能落地的功能；OpenInfer 提供者代表社区拓展生态的意愿。

---

## 7. 用户反馈摘要

从 Issue 评论中提取的真实用户声音：

- **“DeepSeek V4 Pro 第一轮成功，后续每轮都失败”**（#26395）——该问题已关闭，但暴露出模型切换场景的测试覆盖不足。
- **“Streaming 模式丢掉 cost，非流式正常”**（#16021）——用户对成本数据一致性敏感，期望 LLM 网关提供精确计费。
- **“Standard Plan 的 5 个 SSO 用户限制对我们完全不够用”**（#25762）——中小企业对上量有迫切需求。
- **“GET /v1/models 所有模型都显示 owned_by: openai，我们在做审计时完全混乱”**（#32903）——接口语义错误影响下游工具。
- **“aiohttp 升级后随机出现 Connection timed out”**（#33820）——依赖包变更带来的稳定性回归。
- **“langfuse 日志 token 为 0”**（#29575）——观测性集成仍需打磨。
- **“python-dotenv 被锁定导致无法修复 CVE”**（#26333）——依赖版本策略急需改进。
- **“Admin UI 路由设置页面在字典格式 fallback 条目下崩溃”**（#26473）——UI 与后端数据格式不同步。

用户总体反馈积极，但**对成本追踪、模型兼容性、UI 一致性**的满意度有待提升。

---

## 8. 待处理积压

以下 Issue / PR 长期未获得充分响应或合并，建议维护者重点关注：

| 类型 | 编号 | 问题 | 备注 |
|------|------|------|------|
| Issue P0 | [#14052](https://github.com/BerriAI/litellm/issues/14052) | `x-litellm-tags` 无法路由到正确模型 | 用户标记 P0，已开放近一年 |
| Issue P0 | [#26398](https://github.com/BerriAI/litellm/issues/26398) | MCP Tool 400 错误 | 影响 Claude Code 集成 |
| Issue 高频 | [#16021](https://github.com/BerriAI/litellm/issues/16021) | 流式成本丢失 | 评论 16，已有 9 个月历史 |
| Issue 安全 | [#26333](https://github.com/BerriAI/litellm/issues/26333) | python-dotenv CVE 无法修复 | 依赖锁定问题 |
| Issue 安全 | [#26190](https://github.com/BerriAI/litellm/issues/26190) | aiohttp 3.13.3 存在 10 个 CVE | 版本回退 |
| PR 待合并 | [#33002](https://github.com/BerriAI/litellm/pull/33002) | 异步流终结卸载 | 提升性能，已开放 14 天 |
| PR 待合并 | [#34029](https://github.com/BerriAI/litellm/pull/34029) | Cursor 代理模式兼容 | 社区热门请求 |
| PR 待合并 | [#34509](https://github.com/BerriAI/litellm/pull/34509) | Guardrail judge_model 凭证懒加载 | 修复潜在崩溃 |

---

*以上分析基于公开 GitHub 数据，客观呈现项目动态。建议维护团队关注 P0 Issue 的闭环以及待合并 PR 的 review 吞吐。*

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据您提供的 GitHub 数据生成的 Temporal 项目动态日报。

---

### Temporal 项目动态日报
**日期：** 2026-07-26
**分析师：** AI 项目分析师

---

### 1. 今日速览

今日项目整体活跃度**较高**，主要集中在对 **CHASM (下一代调度引擎)** 和 **版本工作流服务 (VTS)** 的密集修复与优化上，显示出项目团队正在为下一个重要版本的稳定性进行冲刺。虽然过去24小时内无新Issue产生，但有**26条**活跃的 Pull Request，其中5条已被合并或关闭，流水线处理效率尚可。大量来自核心贡献者 `@davidporter-id-au` 的 PR 专注于增强 CHASM 调度的健壮性、边界情况处理和安全性，表明当前开发重心在于巩固新架构。此外，一个关于 VTS 功能细化的 PR 也获得了关注，表明分布式版本管理功能仍在持续迭代。

### 2. 版本发布

**无新版本发布。**

### 3. 项目进展

今日有5个 PR 被合并或关闭，主要推进了以下工作：

- **发布准备**：为即将发布的 **1.32.0** 版本创建了发布分支，包括覆盖管理文件及更新依赖等准备工作。([#11287](https://github.com/temporalio/temporal/pull/11287))
- **CHASM 核心修复**：合并了关键的测试引擎 Bug 修复，解决了导致版本转换（VT）不匹配的逻辑错误 ([#11288](https://github.com/temporalio/temporal/pull/11288))。同时，修正了 CHASM Nexus 完成事件的时间戳问题，确保使用回调报告的真实关闭时间，提升了时间线的准确性 ([#10915](https://github.com/temporalio/temporal/pull/10915))。
- **可靠性提升**：修复了匹配分区管理器测试中的一个导入错误，保证了测试流程的正常运行 ([#11285](https://github.com/temporalio/temporal/pull/11285))。
- **测试优化**：自动优化测试分片路由 (Salt) 的 PR 已合入，有助于更均匀地分配测试负载，缩短 CI 时间 ([#11261](https://github.com/temporalio/temporal/pull/11261))。

总体来看，项目在**质量与稳定性**方面迈出了坚实一步，特别是对 CHASM 调度引擎的 Bug 修复和边界情况处理，为后续功能的平稳运行奠定了基础。

### 4. 社区热点

今日讨论的热点集中于 **CHASM 调度器** 和 **VTS (版本工作流服务)** 两大新功能领域。

- **VTS 功能细化**：PR [#11259](https://github.com/temporalio/temporal/pull/11259) 为 `DescribeWorkflowExecution` API 增加了“最大跳过时间”和“快进”运行时字段。这显示出用户对于在工作流运行时能实时查询 Versioning 状态有强烈需求。该 PR 的贡献者 `@feiyang3cat` 正在解决 API 兼容性等问题，这表明社区正积极参与到新功能的打磨中。
- **CHASM 调度器补丁**：核心贡献者 `@davidporter-id-au` 发起了一系列针对 CHASM 调度器的修复，涵盖了从阻止空 Patch 请求、校验协议缓冲区格式、正确处理暂停/恢复、到确保版本覆盖能够正常传递给通过 Schedule 启动的工作流等众多细节。这些 PR 的大量涌现，反映出构建一个健壮、无懈可击的调度引擎是当前社区和开发团队的首要任务。

**分析**：社区和开发团队正在集中精力解决 CHASM 调度器和 VTS 在测试和边界场景下的问题，目标是使其达到生产级可靠性。

### 5. Bug 与稳定性

今日报告的 Bug 均通过代码审查后直接修复，无严重或回归性问题遗留。

- **严重 Bug - 逻辑错误**：CHASM 测试引擎存在一个 Bug，导致“下一次转换计数”在读取时被意外修改，以及组件在更新后未被标记为脏数据，从而引起版本转换（VT）不匹配。**(已修复，PR #11288)**
- **中等 Bug - 数据不一致**：CHASM Nexus 操作使用服务端的回调处理时间而非操作的实际关闭时间，导致终端历史事件时间戳不准确。**(已修复，PR #10915)**
- **低等 Bug - 功能缺失**：
    - 通过 Schedule 启动的工作流无法携带 `VersioningOverride` 参数。**(已修复，PR #11283 待合并)**
    - Schedule 的 `PatchSchedule` 和 `UpdateSchedule` 操作未进行请求去重（Deduplication），可能导致重复操作。**(已修复，PR #11284)**
    - 一些边界情况处理不当，例如接受格式错误的 `Duration` 协议缓冲区、在 `request == nil` 时发生空指针恐慌等。**(已修复，PR #11275, #11276, #11282 等待合并)**
- **稳定性提升**：在复制场景下，如果“当前执行记录”丢失，系统现在会尝试重建而非直接失败，增强了集群间复制的鲁棒性。(PR [#11257](https://github.com/temporalio/temporal/pull/11257) 待合并)

### 6. 功能请求与路线图信号

虽然没有直接的新功能请求 Issue，但从待合并的 PR 中可以清晰地看到路线图信号：

- **强化 CHASM 调度引擎**：大量的 PR 表明项目正在全力完善 CHASM，这是 Temporal 未来调度功能的核心。功能上包括：
    - **暂停/恢复的即时生效**：在创建 Schedule 时应用 `InitialPatch` 中的暂停/恢复指令。
    - **重试策略改进**：将重试次数上限改为包含性边界，并在重试前重新检查追赶截止时间，避免在无意义的失败上浪费时间。
    - **兼容性保障**：确保 CHASM 调度器在 V2 与 V1 版本迁移、不同机制间的一致性处理。
- **增强可观测性**：新增 `shardinfo_immediate_queue_backlog_age` 指标，让用户能够监控即时队列的积压时长，这是运维和排查性能瓶颈的关键指标 (PR [#11255](https://github.com/temporalio/temporal/pull/11255) 待合并)。

这些 PR 很可能会被纳入下一个版本（1.32.0）中，共同构成一次重大的稳定性与功能更新。

### 7. 用户反馈摘要

今日无新的 Issue 被提出，因此缺乏直接的用户反馈。然而，从活跃的 PR 中可以推断出用户的潜在需求：

- **对工作流状态的深度可见性**：VTS 的 PR [#11259](https://github.com/temporalio/temporal/pull/11259) 表明，用户在执行复杂的工作流版本转换时，希望有更详细的运行时状态信息，以便于调试和监控。
- **对 Schedule 功能可靠性的高要求**：`@davidporter-id-au` 修复的一系列关于 Schedule 的边界情况和空指针问题，间接反映了用户在实际使用中可能遇到了难以排查的偶发性错误。这些修复旨在提升用户体验的平滑度。

### 8. 待处理积压

今日无长期未响应的重要 Issue 或 PR。所有 PR 都在近几天内被活跃关注和评论。项目的 backlog 管理状况良好。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*