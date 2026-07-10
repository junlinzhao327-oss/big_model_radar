# OpenClaw 生态日报 2026-07-11

> Issues: 414 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-10 23:17 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，以下是基于您提供的 GitHub 数据生成的 OpenClaw 项目动态日报。

---

# OpenClaw 项目动态日报 — 2026-07-11

## 1. 今日速览

过去 24 小时，OpenClaw 项目保持 **极高活跃度**，共处理了 **414 条 Issues** 和 **500 条 PRs**。社区讨论主要集中在 **关键稳定性问题（内存泄漏、会话状态丢失）** 和 **平台集成 Bug（Discord 重连、WhatsApp 卡死）** 上。一个积极的信号是，多个高优先级（P1/P0）的 Bug 修复 PR（#99756, #102189）正在等待合并，表明项目团队正在集中精力解决最为棘手的问题。尽管今日无新版本发布，但社区的贡献与维护者的响应速度表明项目整体健康状况良好，正处于一个重要的 **“修复与加固”** 阶段。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日合并/关闭的重要 PR 和 Issues 推动了多项关键修复与功能改进：

- **稳定性与可靠性提升**：
    - **ACP 协议兼容性**：PR #103958 修复了 ACP 会话启动失败的问题，该问题影响所有使用不提供 `thinking` 配置的后端（如 OpenCode）的用户。这是一个重要的兼容性修复。
    - **任务系统兼容性**：PR #103174 已被合并，它解决了来自旧版本（pre-2026.6.11）的遗留任务数据库中的状态兼容性问题，确保升级过程平滑。
    - **安全与行为修复**：Issue #91283 和 #68691 已关闭。前者修复了 `minSecurity` 配置逻辑颠倒的安全问题；后者解决了沙箱环境中僵尸进程不断累积的问题。
- **用户体验优化**：
    - 虽然未合并，但 PR #103706 着手修复了 `bash` 命令输出中 ANSI 控制序列片段泄漏的问题，这对提升终端用户体验至关重要。

项目整体正沿着 **修复严重 Bug、增强跨平台/跨协议兼容性、清理技术债务** 的方向稳步推进。

## 4. 社区热点

以下议题在过去 24 小时内引发了最热烈的讨论：

- **#99241: 工具输出渲染为图片附件导致 Agent 无法读取**（20 条评论）
    - **链接**：[https://github.com/openclaw/openclaw/issues/99241](https://github.com/openclaw/openclaw/issues/99241)
    - **核心诉求**：在长时间运行或包含大量 ANSI 转义码的任务中，工具的结果会被错误地转换成图片附件，导致 AI Agent 无法读取关键词信息。这直接影响了 Agent 处理复杂任务的可靠性。
    - **分析**：这是一个影响核心 Agent 工作流的严重问题。用户和贡献者共同定义了问题边界，并且 PR #99756 已经提供了修复方案，表明社区和团队反应迅速。

- **#102175: 嵌入式提示缓存跨越多种边界时失效**（16 条评论）
    - **链接**：[https://github.com/openclaw/openclaw/issues/102175](https://github.com/openclaw/openclaw/issues/102175)
    - **核心诉求**：在复杂的多会话、多策略场景下，用于提升模型响应速度和降低成本的关键特性——提示缓存（Prompt Cache）会失效，导致性能下降和成本增加。
    - **分析**：这个问题揭示了 OpenClaw 在复杂的上下文管理中面临的挑战。关联的 PR #102189 表明了开发团队正在从架构层面解决这个根本性问题。

- **#91588: 网关内存泄漏导致 OOM 崩溃（P0）**（15 条评论）
    - **链接**：[https://github.com/openclaw/openclaw/issues/91588](https://github.com/openclaw/openclaw/issues/91588)
    - **核心诉求**：一个长期存在的、严重等级为 **P0（最高）** 的性能 Bug。网关进程的内存在 2-3 天内从 350MB 增长到 15.5GB，最终被系统 OOM 杀手杀死，导致服务崩溃重启。
    - **分析**：这是影响项目稳定性的最大威胁。该 Issue 持续活跃，社区成员在积极提供日志和复现步骤，流量相关 PR 可能正在内部评审中。这是项目当前需要解决的头号问题。

## 5. Bug 与稳定性

今日报告的 Bug 和稳定性问题按严重程度排列如下：

| 优先级 | Issue ID | 摘要 | 是否有 Fix PR | 链接 |
| :--- | :--- | :--- | :--- | :--- |
| **P0 (Critical)** | #91588 | **网关内存泄漏：RSS 从 350MB 增长至 15.5GB 导致 OOM 崩溃** | 状态未明 | [链接](https://github.com/openclaw/openclaw/issues/91588) |
| **P1 (High)** | #99241 | **工具输出渲染为图片，Agent 无法读取文本** | 有 (#99756) | [链接](https://github.com/openclaw/openclaw/issues/99241) |
| **P1 (High)** | #101763 | **Hosted Molty 模型选择器无法持久化，API 始终调用无效模型 ID** | 无 | [链接](https://github.com/openclaw/openclaw/issues/101763) |
| **P1 (High)** | #89278 | **Codex OAuth 刷新因超时导致 Crontab/Heartbeat 失败** | 无 | [链接](https://github.com/openclaw/openclaw/issues/89278) |
| **P1 (High)** | #84569 | **WhatsApp 会话在处理长模型调用时卡死，回复无法送达** | 无 | [链接](https://github.com/openclaw/openclaw/issues/84569) |
| **P1 (High)** | #83959 | **Codex 应用服务器启动重试耗尽，导致服务不可用** | 无 | [链接](https://github.com/openclaw/openclaw/issues/83959) |
| **P2 (Mid)** | #102175 | **嵌入式提示缓存跨边界失效** | 有 (#102189) | [链接](https://github.com/openclaw/openclaw/issues/102175) |

此外，Issue #103332 报告了一个 **回归问题**，涉及 `codex/gpt5.6` 模型在 `pi` 运行时无法工作。

## 6. 功能请求与路线图信号

今日新增/活跃的功能请求显示出社区对 **可观测性、控制能力和平台集成** 的强烈需求：

- **Agent 行为的精细化控制**：
    - **#9912**：请求 `maxTurns` / `maxToolCalls` 配置，以限制 Agent 的无限制循环。这与 `#6890`（Ralph Loop 最大迭代次数）方向一致，可能被整合进 Agent 配置体系中。
    - **#8299**：请求增加配置选项，以抑制子 Agent（sub-agent）完成任务后的主动性播报。
- **更好的可观测性与成本控制**：
    - **#9797**: 请求 `queue_status` 工具，让 Agent 本身能了解队列负载，实现智能任务调度。
    - **#9865**：请求为后台任务提供 Batch API 支持，以降低 API 使用成本（约 50%）。
- **平台集成与可扩展性**：
    - **#12602**: 请求支持 **Slack Block Kit**，以使 Agent 消息更丰富、交互性更强。
    - **#8287**：请求支持 **Node 注册 Agent 工具**，使连接节点可以无需开发插件即可扩展 Agent 能力。

结合已有 PR（如 #103811 增强 Google Meet 功能、#96120 刷新 MCP OAuth Token），可以判断下个版本将重点提升 **混合架构（MCP）集成能力** 和 **群组/会议场景的丰富度**。

## 7. 用户反馈摘要

从今日的 Issues 评论中，可以听到以下真实用户的声音：

- **痛点**：
    - **稳定性焦虑**：“我的网关在运行 2-3 天后必然 OOM”（#91588）。
    - **体验割裂**：“Agent 在 Slack 发消息，但在 DM 里却看不到自己发过的内容”（#7359），这暴露了跨会话上下文管理的缺失。
    - **配置复杂**：插件安装后需手动修改配置（#6792），且部分配置（如 Cron 的默认投递目标，见 #9155）没有默认值，导致重复劳动。
- **使用场景**：用户不仅将 OpenClaw 用于个人助手，还用于：
    - **内容创作与演示**：请求“私密模式”隐藏个人工作空间数据（#7403）。
    - **无障碍访问**：屏幕阅读器用户反馈 TUI 中的 emoji 和符号造成困扰（#9637）。
- **满意度**：社区对项目的投入度很高，愿意提供详细的 Bug 复现步骤和解决方案。虽然有严重 Bug，但用户仍积极贡献，表明项目本身的价值和社区粘性较高。

## 8. 待处理积压

以下是最应得到维护者关注的老旧/重要 Issue 和 PR：

- **#7722 [Feature] Filesystem Sandboxing Config** (创建于 2026-02-03, 10 条评论)
    - **链接**：[https://github.com/openclaw/openclaw/issues/7722](https://github.com/openclaw/openclaw/issues/7722)
    - **原因**：一个长期开放的安全相关功能请求，关于文件系统沙箱配置。该功能对安全敏感用户至关重要，但缺乏来自维护者的明确决策。

- **#90583 及相关 PR #95311**: 关于 DeepSeek 兼容性的 Promt Cache 修复（PR 创建于 2026-06-20, 状态: 📣 needs proof）
    - **链接**：[https://github.com/openclaw/openclaw/pull/95311](https://github.com/openclaw/openclaw/pull/95311)
    - **原因**：该 PR 提供了一个解决特定模型（DeepSeek）兼容性的关键补丁，涉及提示缓存（Prompt Cache），这是成本和性能的关键特性。尽管有 6 条评论，但状态还停留在“需要证据”，可能会影响相关用户的体验。

- **#40527 [Bug] 远程技能二进制探测超时（macOS）** (创建于 2026-03-09, 5 条评论)
    - **链接**：[https://github.com/openclaw/openclaw/issues/40527](https://github.com/openclaw/openclaw/issues/40527)
    - **原因**：一个影响 macOS 用户的特定 Bug。当 macOS App 作为 Node 与同一台机器上的 Gateway 连接时，`skills-remote` 探测会超时。该 Issue 被标记为 `P2`，但长期未解决，影响了特定配置下的用户体验。

---

## 横向生态对比

好的，作为资深技术分析师，以下是根据您提供的五个核心开源项目（OpenClaw, Hermes Agent, OpenHands SDK, Pi, LiteLLM, Temporal）今日动态摘要生成的横向对比分析报告。

---

### 个人 AI 助手与自主智能体开源生态横向分析报告 (2026-07-11)

#### 1. 生态全景

当前，个人 AI 助手与自主智能体开源生态正处于 **由“能力探索”向“生产级可靠性”过渡的关键时期**。一方面，项目普遍表现出极高的社区活跃度和对新模型（如GPT-5.6）、新协议（如MCP）的快速跟进能力；另一方面，**稳定性、可观测性和成本控制**成为社区最普遍的痛点。多个项目（如OpenClaw, LiteLLM）出现了严重的内存泄漏或计费Bug，而用户对远程访问、多平台集成和精细化行为控制的需求日益强烈。这表明生态的“骨架”已基本搭建完成，但“血肉”（稳定性、易用性、运维工具）仍需大量填充。Temporal作为底层工作流引擎，其自身向更易用、更可观测方向的演进，为上层智能体应用提供了更坚实的基础。

#### 2. 各项目活跃度对比

| 项目名称 | 核心定位 | 今日Issues活跃数 | 今日PR数(活动/合并) | 版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 通用AI Agent框架 | 414 | 500 / 活跃 | 无 | **高活跃，重点关注**。社区规模极大，但P0级内存泄漏、P1级Agent工作流Bug突出，处于“修复与加固”期。 |
| **Hermes Agent** | 多平台Agent运行时 | 213 (新+活跃) / 81 (关闭) | 420 / 活跃 | 无 | **极高活跃，贡献火爆**。社区贡献热情极高，但大量PR积压，核心Bug (路由错乱、模型卡死) 亟待解决。 |
| **OpenHands SDK** | Agent开发工具包 | 中 | 中 / 数个 | **v1.35.0** | **健康稳定，稳步迭代**。聚焦于核心功能 (Agent Profiles) 的打磨与稳定性，版本发布节奏良好。 |
| **Pi** | 通用LLM交互客户端 | 57 | 12 / 10 | **v0.80.6** | **高速迭代，前沿跟进**。快速响应新模型(GPT-5.6)和新特性(约束采样)，发布频繁。回归Bug需警惕。 |
| **LiteLLM** | 模型网关/代理 | 78 | 253 / 100 | **v1.93.0-dev.3** | **高活跃，架构转型期**。PR处理量大，计费与连接稳定性Bug突出。Rust迁移计划标志着重大架构变更。 |
| **Temporal** | 工作流编排引擎 | 1 (关闭) | 46 / 18 | 无 | **稳定成熟，关注点明确**。核心功能开发（独立活动操作、Nexus）持续推进，社区活跃度相对稳重。 |

#### 3. OpenClaw 在生态中的定位

OpenClaw 在生态中扮演着 **“全栈AI Agent参考实现”** 的角色，其社区规模和问题复杂度在所有项目中首屈一指。

- **优势**：拥有最大的社区讨论量（414 Issues, 500 PRs），覆盖了从底层内存泄漏到上层用户体验的完整问题域。其在ACP协议兼容性、多平台（Discord, WhatsApp）集成方面的投入，使其成为功能最全面的框架之一。
- **差异化定位**：与**Hermes Agent**（侧重多平台Agent运行时）相比，OpenClaw更像一个“一站式解决方案”；与**Pi**（侧重用户交互客户端）相比，OpenClaw更强调Agent的自动化后台任务与工具调用能力。
- **技术路线**：OpenClaw通过多种协议（ACP, MCP）连接后端模型，并通过“技能”和“网关”架构实现可扩展性。其当前面临的核心挑战（内存泄漏、Agent工作流可靠性）是生态中所有复杂Agent系统都会遇到的共性问题，因此其修复过程对其他项目极具参考价值。

#### 4. 共同关注的技术方向

以下需求在多个项目中同时涌现，标志着行业共识的形成：

- **新模型（GPT-5.6）与高阶推理的适配**：
    - **涉及项目**：**Pi**、**OpenClaw**、**OpenHands SDK**、**LiteLLM**。
    - **具体需求**：社区强烈要求支持最新的GPT-5.6系列模型，并为其引入新的“思考级别”（如`max`, `ultra`）。这代表了对更高阶模型能力（推理、深度思考）的追求，是当前最热门的趋势。

- **远程访问、多平台集成与稳定连接**：
    - **涉及项目**：**OpenClaw** (WhatsApp/Discord)、**Hermes Agent** (仪表板远程访问、QQBot重连)、**Pi**。
    - **具体需求**：用户不满足于本地运行，要求通过VPN(CORS配置)安全访问仪表板，并稳定集成更多聊天平台（QQ、Slack Block Kit），且修复连接中断和消息丢失问题。这反映了从个人开发者向团队/家庭场景演进的刚需。

- **成本控制与可观测性**：
    - **涉及项目**：**OpenClaw** (队列状态、Batch API)、**LiteLLM** (成本精确计算、OTel事件)。
    - **具体需求**：用户希望智能体自己能感知资源开销（队列状态），并需要更精确的计费（修复流式成本丢失）和日志追踪。这表明项目已进入生产级运维阶段，成本与监控是核心痛点。

- **Agent 行为的精细控制与灵活扩展**：
    - **涉及项目**：**OpenClaw** (`maxTurns`)、**OpenHands SDK** (Agent Profiles)、**Hermes Agent** (远程Agent+本地工具)。
    - **具体需求**：用户需要精确限制Agent的循环次数、配置其行为模式（Profile）、并实现解耦的扩展（如MCP）。这反映了社区对Agent“可控性”和“可组合性”的追求，而非黑盒使用。

#### 5. 差异化定位分析

| 维度 | **OpenClaw** | **Hermes Agent** | **Pi** | **LiteLLM** | **Temporal** |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **功能侧重** | 全栈Agent开发与部署 | 多Agent运行时与平台连接 | LLM交互客户端 | 模型路由、计费与代理 | 工作流编排与状态管理 |
| **目标用户** | Agent 开发者/高级用户 | Agent 运维者/多平台集成者 | 个人用户/模型探索者 | 需要统一模型网关的开发/运维团队 | 微服务/分布式系统开发者 |
| **技术架构亮点** | 协议抽象层(ACP) + 网关 | Kanban工作流 + Telegram集成 | 深度思考级别阶梯 | Rust迁移计划 + Provider Registry | 多集群容错 + Nexus协议 |
| **核心挑战** | 系统稳定性（内存泄漏） | 海量PR积压与核心Bug | 新模型适配的兼容性问题 | 计费准确性与超时处理 | 新功能(独立活动)的成熟度 |

#### 6. 社区热度与成熟度

- **快速迭代期（极高热度，追求功能与速度）**：
    - **Pi**：对新模型、新特性响应最快，迭代版频繁，社区活跃于功能探索。
    - **LiteLLM**：PR处理量巨大，正在进行架构转型（Rust），整体处于快速“攻城略地”阶段。
    - **OpenClaw** / **Hermes Agent**：社区规模庞大，但被大量Bug和积压的PR/Issue所困，呈现出“高速运转但伴生摩擦”的状态。

- **质量巩固期（稳定迭代，聚焦核心与可靠性）**：
    - **Temporal**：项目成熟度高，开发节奏稳健，无大规模Bug风暴。当前精力集中在特定功能的完善（独立活动操作）和新协议的接入（Nexus）。
    - **OpenHands SDK**：作为底层SDK，版本发布与功能迭代节奏清晰，是生态中较为稳定的一环。

#### 7. 值得关注的趋势信号

- **“Rust化”浪潮初现**：**LiteLLM** 的Rust迁移计划是当日最重要的架构信号之一。这表明在AI基础设施层，性能（延迟、吞吐量）和内存安全成为首要考量，传统Python的性能瓶颈可能通过核心组件重写来解决。这对所有Python基础的项目提出了未来的技术和成本挑战。
- **“安全与沙箱”成为刚需**：**OpenClaw** 的沙箱僵尸进程修复以及**OpenHands SDK** 的 `ToolShieldLLMSecurityAnalyzer` PR，都指向了智能体在生产环境中安全运行的问题。当Agent开始执行原生代码和文件操作时，安全的沙箱环境不再是可选项，而是必需品。
- **“可编程Agent”时代到来**：**OpenHands SDK** 的 `Agent Profiles`、**Pi** 的 `maxTurns` 和约束采样，以及**Hermes Agent** 的 `远程Agent+本地工具`，都指向同一个趋势：用户不再满足于开箱即用的Agent，而是要求通过配置、Profile或架构分离，对Agent的行为、能力和资源进行**精确编程和控制**。这对开发者来说是巨大的机遇，意味着需要提供更精细的配置模型和扩展接口。
- **模型适配的“军备竞赛”不可持续**：**Pi** 和 **LiteLLM** 在新模型支持上的快速迭代，反映出社区对前沿能力的极大热情。但这也导致了大量与API兼容性相关的Bug和开发资源消耗。一个值得思考的趋势是，未来项目是否会转向更通用的模型协议抽象层（如ACP），以减少对特定模型API的频繁适配。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，遵照您的指示。以下是为 Hermes Agent 开源项目生成的 2026年7月11日项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026-07-11

## 1. 今日速览

今日项目活跃度依然维持在**极高**水平，社区提交及维护者处理工作量巨大。过去24小时内，项目新增/活跃了213个Issue，并有81个旧Issue被关闭，同时收到了高达420个待合并的PR，显示出社区贡献热情高涨，但也给项目的代码审查和合并工作带来了显著压力。值得关注的是，关于TheWon运行时强化和Kanban看板特性的一系列PR正在密集推进，表明项目进入了功能完善和系统鲁棒性提升的关键阶段。然而，用户也报告了多个关于连接稳定性、会话状态和仪表板配置的Bug，这些问题需要维护团队优先处理。

## 2. 版本发布

无

## 3. 项目进展

今日项目在功能开发和问题修复上均有不小进展，尤其集中在强化系统稳定性、修复定价问题及完善Kanban工作流方面。

*   **TheWon运行时强化**：`#62343` (`feat: harden TheWon runtime rollout gates`) PR已合并，内容涵盖了TheWon KH + LLM Wiki预检查、网关生命周期重启防护及Slack集成，显著提升了TheWon场景的稳定性。该PR最初打开后又关闭，其核心功能已由同作者的`#62345` (当前为OPEN) 承接。
*   **定价模型修正**：`#62334` (`fix(pricing): correct deepseek-v4-pro rates (4x overcharge) and add v4-flash`) PR已合并。该PR修正了DeepSeek V4-Pro模型定价被错误乘以4倍的问题，并添加了V4-Flash模型的价格数据，这对于使用该模型的用户至关重要。
*   **Kanban功能完善**：
    *   `#59937` (`fix(kanban): preserve completion artifact evidence`) 和 `#59939` (`test(kanban): cover durable completion evidence regressions`) 已关闭，两项PR共同确保了Kanban看板完成任务后的证据留存和回归测试覆盖。
    *   `#61937` (`fix(kanban): add boards restore for archived boards`) 目前为OPEN状态，为误删除或归档的看板提供了恢复命令，完善了Kanban的数据管理能力。
*   **开发体验提升**：
    *   `#62217` (`feat(dev): add isolated sandbox script for local dev`) 已合并，新增的本地沙箱脚本允许开发者在不影响主环境的情况下进行测试，是提升开发效率的良好设计。
    *   `#62245` (`ci: advisory eslint + autofix-on-merge with security hardening`) 为OPEN状态，旨在通过CI引入ESLint并实现自动修复，加强代码质量和安全性。
*   **Vertex AI支持**：`#61933` (`fix(auth): register vertex in PROVIDER_REGISTRY for auxiliary clients`) 为OPEN状态，它向PROVIDER_REGISTRY注册了Vertex AI的配置，解决了仅使用Vertex AI部署时后台辅助任务（如标题生成、压缩）无法使用的问题。

## 4. 社区热点

今日社区讨论焦点集中在几个关键问题和特性上，反映出用户对**连接稳定性**、**远程访问**和**多平台支持**的强烈诉求。

*   **QQBot无限重连Bug (#52914)**：此已关闭的Bug（17条评论）引发了广泛关注。用户报告在更新版本后，QQBot网关陷入无限重连循环，直接影响了该平台用户的正常使用。该问题已被快速修复并关闭，体现了团队对核心平台问题的响应速度。

*   **仪表板远程访问与CORS配置 (#10567)**：该特性请求（13条评论，13个👍）要求为Hermes Dashboard添加 `--host` 和CORS配置，以便通过Tailscale/VPN进行远程访问。这是用户从个人使用走向团队或远程协作的刚需，反映了项目在易用性和部署灵活性上的增长瓶颈。

*   **原生Google Cloud Vertex AI支持 (#13484)**：该特性请求（11条评论，14个👍）表达了用户对原生集成Vertex AI的强烈愿望。用户指出现有的配置入口缺乏实际的认证机制。结合今日合并的修复PR #61933，说明社区和团队正在积极解决此问题，是热度最高的路线图信号之一。

*   **远程Agent与本地工具执行 (#18715)**：此特性请求（8条评论，20个👍）是目前点赞数最高的功能。用户希望将Agent部署在远程服务器上，而工具执行（如文件操作、代码运行）保留在本地。这是对现有“胖客户端”模式的重要补充，体现了用户对更复杂、更安全的工作流的需求。

## 5. Bug 与稳定性

今日报告的Bug主要集中在**网关连接、会话管理和特定模型兼容性**上，其中部分问题已有对应的修复PR。

| 问题ID | 标题 | 严重性 | 状态 | 说明 |
| :--- | :--- | :--- | :--- | :--- |
| #54527 | 网关消息路由在多TUI会话间错乱 | **P1** | 开放 | 用户在Desktop应用中打开多个TUI会话时，输入消息可能被路由到错误的会话中，导致输入丢失。影响用户体验，属于严重问题。 |
| #52914 | QQBot adapter无限重试循环 | P2 | 已关闭 | 影响核心平台连接的问题，已被修复。 |
| #52496 | Dashboard模型切换器覆盖自定义provider | P2 | 开放 | 仪表板的模型切换功能会将名为 `custom:*` 的自定义provider错误地改写为openrouter，影响配置准确性。 |
| #61265 | Agent发送超大prompt导致长时间卡顿 | P2 | 开放 | 用户报告本地模型收到了异常巨大的prompt，导致多分钟级别的卡顿，影响本地部署用户的效率。 |
| #27038 | Codex API拒绝回复带有长id的assistant消息 | P1 | 开放 | 在恢复或继续会话时，如果包含长ID的assistant消息，会导致Codex API拒绝请求，影响会话连续性。 |
| #26489 | 使用LiteLLM代理Ollama时Hermes挂起 | P2 | 开放 | 特定配置组合（custom provider + LiteLLM + Ollama）下，Agent在探测模型时完全挂起，无法正常使用。 |
| #49253 | 通过Photon iMessage发送的Markdown导致Unicode损坏 | P2 | 开放 | Markdown格式的文本在通过iMessage发送时，Unicode字符被替换为乱码，影响特定平台的消息显示。 |

## 6. 功能请求与路线图信号

除了上述社区热点中提及的需求外，今日其他功能请求信号如下：

*   **定价覆盖与合约定价** (`#9403`): 该功能请求已开放多时，希望添加自定义定价目录和企业合约价格覆盖功能。这通常是企业级部署的需求，表明项目正在向更复杂的商业化场景演进。
*   **Gemini集成 Antigravity** (`#52657`): 用户希望Hermes能通过Antigravity服务使用Gemini Pro订阅，这表明用户希望获得更多的模型提供商和订阅渠道选择。
*   **WhatsApp消息模板支持** (`#45935`): 这是来自真实生产环境的需求，用户希望在24小时窗口外通过预授权的消息模板与客户重新互动，是WhatsApp商业用途的关键功能。
*   **基于事件的通用通知子系统** (`#49190`): 一个深层次的功能请求，提议将当前的Kanban通知泛化为事件订阅系统，允许任何平台或组件注册为事件的接收者，这将是项目架构的一次重要升级。
*   **支持远程Agent + 本地工具执行** (`#18715`): 如前所述，这是当前点赞最多的功能，很可能成为下一阶段的开发重点。结合已有相关PR判断，该功能实现难度较高，可能会在多个版本中逐步落地。

## 7. 用户反馈摘要

*   **痛点：微信多账号支持** (`#9756`): 中文用户在#9756中反馈，目前网关设置只能绑定一个微信账号，无法满足家庭或团队内多人使用的场景，希望尽快支持。
*   **痛点：飞书插件问题** (`#7675`): 飞书用户报告了三个问题：卡片交互被误识别为命令、审批按钮失效、以及卡片消息不支持流式回复。这表明飞书平台的集成仍需大量打磨。
*   **痛点：Kanban死锁任务** (`#22926`): Kanban用户报告，当工作进程意外死亡时，其占用的任务锁无法自动释放，导致任务永久卡死，需要管理员手动干预。这是一个常见的分布式系统问题，影响Kanban作为任务系统的可靠性。
*   **满意点：ml.ink Skill** (`#495`): 用户对通过MCP协议将Hermes Agent与ml.ink部署平台集成表示满意，这为Agent提供了一种更便捷的生产级应用部署路径。

## 8. 待处理积压

以下为创建时间较长、但至今仍为开放状态且未收到有效直接回复或解决的重要Issue/PR，建议项目维护者优先审视。

*   **`#10567`**: `Add --host and CORS config for hermes dashboard to enable Tailscale/VPN access`
    *   **创建时间**: 2026-04-15
    *   **现状**: 高赞的Feature Request，对远程工作至关重要，尚无明确实现计划。
    *   **链接**: https://github.com/NousResearch/hermes-agent/issues/10567

*   **`#13484`**: `Feature: native Google Cloud Vertex AI provider support`
    *   **创建时间**: 2026-04-21
    *   **现状**: 高赞的Feature Request，已有相关修复PR #61933，但较完整的原生支持仍需进一步规划。
    *   **链接**: https://github.com/NousResearch/hermes-agent/issues/13484

*   **`#18715`**: `Support remote Hermes agent with local tool execution`
    *   **创建时间**: 2026-05-02
    *   **现状**: 目前点赞数最高的Feature，对架构影响深远，需要社区深入讨论和设计。
    *   **链接**: https://github.com/NousResearch/hermes-agent/issues/18715

*   **`#9403`**: `feat(pricing): add pricing overrides, contract pricing, and sync CLI`
    *   **创建时间**: 2026-04-14
    *   **现状**: 企业级功能，代表了社区对商业化部署的呼声，宜早做规划。
    *   **链接**: https://github.com/NousResearch/hermes-agent/issues/9403

*   **`#26489`**: `Hermes hangs when provider=custom + LiteLLM proxy + Ollama (no chat completion call after probing 404s)`
    *   **创建时间**: 2026-05-15
    *   **现状**: 一个影响特定但常见配置组合（Ollama用户）的严重Bug，长期未解决可能会影响用户对自托管模型的信心。
    *   **链接**: https://github.com/NousResearch/hermes-agent/issues/26489

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

好的，这是根据您提供的 OpenHands SDK GitHub 数据生成的 2026-07-11 项目动态日报。

---

## OpenHands SDK 项目日报 — 2026-07-11

### 1. 今日速览

今日项目活跃度较高，主要围绕 v1.35.0 版本的发布与适配，以及 Agent Profiles（Agent 配置文件）相关功能的持续优化和问题修复。社区讨论集中在 Agent Profile 的复杂性与模型统一上，同时有多项针对会话恢复、工具解析和流式处理的 Bug 被提出和修复。团队在功能完善与稳定性方面表现出均衡推进的态势。

### 2. 版本发布

**v1.35.0 已发布**
- **链接**: [Release v1.35.0](https://github.com/OpenHands/software-agent-sdk/releases/tag/v1.35.0)
- **更新内容**:
    - **修复技能关键字匹配 (`fix(skills): match keyword triggers on whole words only`)**: 通过 PR [#4008](https://github.com/OpenHands/software-agent-sdk/pull/4008) 修复，确保技能触发仅匹配完整单词，避免了部分匹配造成的误触发。
    - **修复远程会话 WebSocket 重连 (`fix(sdk): reconnect remote conversation websocket`)**: 通过 PR [#3987](https://github.com/OpenHands/software-agent-sdk/pull/3987) 修复，增强了远程会话在网络波动下的稳定性。
    - **CI 版本升级流程 (`ci(version-bump-`)**: 版本发布流程中的自动化脚本或配置有相应更新。
- **破坏性变更与迁移**: 未提及。此次发布主要为 Bug 修复和小幅改进，预计不会引入破坏性变更。建议用户更新以避免目标 Bug。

### 3. 项目进展

今日有多项功能修复和基础设施优化工作完成，项目在稳定性和开发者体验上有所提升。

- **Agent Profiles 功能持续推进**：多个关于 Agent Profiles 的 Issue 和 PR 进入收尾或合并阶段。例如，简化配置文件解析模型 ([#4017](https://github.com/OpenHands/software-agent-sdk/issues/4017)) 和修复配置文件启动后流式处理失效 ([#4014](https://github.com/OpenHands/software-agent-sdk/issues/4014)) 的问题均已关闭，表明此核心功能正在走向成熟。
- **新增 Commit History API**：PR [#4075](https://github.com/OpenHands/software-agent-sdk/pull/4075) 合并，为 Agent Server 新增了查看提交历史和差异的 API，增强了项目的版本控制集成能力。
- **测试与 CI 改进**：
    - 修复了因日志链接错误导致的不稳定问题 ([PR #4065](https://github.com/OpenHands/software-agent-sdk/pull/4065))。
    - 对会话树 Fork/Navigate 的测试进行了消抖处理 ([PR #4074](https://github.com/OpenHands/software-agent-sdk/pull/4074))，提升了测试可靠性。
    - 将 QA 变更工作流切换到评估模型代理，以避免触及团队预算限制 ([PR #4081](https://github.com/OpenHands/software-agent-sdk/pull/4081))。
- **生态兼容性**：支持了最新的 GPT-5.6 模型并通过 Codex ACP 认证 ([PR #4056](https://github.com/OpenHands/software-agent-sdk/pull/4056))，保持了与主流模型和工具的兼容性。

### 4. 社区热点

今日社区讨论的焦点是 **Agent Profiles 的复杂性与模型统一**。

- **[#2078] [OPEN] Daily Integration Runs**：这是一个长期的集成测试跟踪 Issue，持续收到新的评论。它虽然不直接涉及功能讨论，但作为项目持续集成状态的晴雨表，反映了社区对项目稳定性的持续关注。
  - **链接**: [#2078](https://github.com/OpenHands/software-agent-sdk/issues/2078)
- **[#3713] [OPEN] Agent Profiles 主题**：该议题及其相关的一系列子议题（如 [#3710](https://github.com/OpenHands/software-agent-sdk/issues/3710), [#3979](https://github.com/OpenHands/software-agent-sdk/issues/3979), [#4017](https://github.com/OpenHands/software-agent-sdk/issues/4017)）收到了最多的评论。社区成员，特别是核心贡献者 `@simonrosenberg`，正在深入讨论如何简化 Agent Profiles 的架构，解决技能模型重复 (`skill_refs` vs `embedded skills`) 以及配置解析过程中的各种边缘案例。
  - **链接**: [#3713](https://github.com/OpenHands/software-agent-sdk/issues/3713)
  - **分析**: 社区（尤其是高级用户）对 Agent Profiles 这一功能抱有很高期望，但也对其设计复杂性提出了细致反馈。诉求是希望该功能能提供清晰、简洁且无副作用的配置体验，避免因模型设计缺陷导致多种工作场景下的错误。这表明社区深度参与了项目核心功能的迭代。

### 5. Bug 与稳定性

今日报告了多个 Bug，主要集中在配置恢复、流式处理和数据解析方面，部分已有修复方案。

| 严重程度 | Issue/PR | 问题描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **高** | [#4080](https://github.com/OpenHands/software-agent-sdk/issues/4080) | 单个未注册事件导致整个会话加载失败 | 待处理 (needs-triage) |
| **高** | [#4032](https://github.com/OpenHands/software-agent-sdk/issues/4032) | LLM Profile 的超时设置在 agent-server 重启后被重置 | 待修复，已有关联PR [#4028](https://github.com/OpenHands/software-agent-sdk/pull/4028) |
| **中** | [#4077](https://github.com/OpenHands/software-agent-sdk/issues/4077) | 流式处理 (Streaming) 的 token/delta 管道存在正确性和资源安全性 Bug | 待处理 (Bug) |
| **中** | [#4063](https://github.com/OpenHands/software-agent-sdk/issues/4063) | `max_concurrent_runs` 配置未能限制原生异步会话 | 待处理 (needs-triage) |
| **低** | [#4079](https://github.com/OpenHands/software-agent-sdk/issues/4079) | 当 ACP 命令未被识别时，可能因缺少 token 计数导致会话失败 (已关闭) | **已修复** (PR [#4056](https://github.com/OpenHands/software-agent-sdk/pull/4056)) |
| **低** | [#4072](https://github.com/OpenHands/software-agent-sdk/issues/4072) | 针对 `browser_use` 库的日志补丁需在依赖库修复后移除 | 待处理，有明确后续安排 |

### 6. 功能请求与路线图信号

除了正在密集开发的 **Agent Profiles**，社区还提出了几个值得关注的新功能方向，可能被纳入未来版本。

- **运行时可配置的 LLM 附加请求头**：用户 `@bozhnyukAlex` 提出 [#4064](https://github.com/OpenHands/software-agent-sdk/issues/4064)，希望能在单个会话的 LLM 请求中附加请求范围的元数据。这暗示了用户对细粒度监控和定制化需求的浮现。
- **从 Agent Server 映像中分离 ACP 提供商**：`@simonrosenberg` 在 [#4067](https://github.com/OpenHands/software-agent-sdk/issues/4067) 中提议，将 Claude Code、Codex 等 ACP 工具包从默认的 agent-server 镜像中拆分出来，以减小镜像体积。这反映了对部署效率和资源优化的关注，可能成为基础设施优化方向。
- **公开 ACP 会话配置选项**：`@neubig` 提出的 [#4062](https://github.com/OpenHands/software-agent-sdk/issues/4062)，希望 Agent Server 能原生支持 ACP 代理广告的 `configOptions`。这将增强 Agent Server 的灵活性和可配置性。

### 7. 用户反馈摘要

从今日的 Issues 和 PR 评论中，可以提炼出以下用户反馈：

- **对 Agent Profiles 的复杂模型感到困扰**：用户 `@simonrosenberg` 在多个议题中详细描述了因 Profile 模型设计（如 `skill_refs` 与`embedded skills` 共存）导致的各类问题（[#3979](https://github.com/OpenHands/software-agent-sdk/issues/3979), [#4017](https://github.com/OpenHands/software-agent-sdk/issues/4017)），表达了对功能简单性和一致性的强烈需求。
- **对重启后配置丢失的担忧**：用户 `@kripper` 报告 LLM Profile 超时设置在服务重启后丢失 ([#4032](https://github.com/OpenHands/software-agent-sdk/issues/4032))，这是一个典型的稳定性痛点，直接影响用户对服务的信任。
- **对会话恢复鲁棒性的期望**：用户 `@smolpaws` 指出单个事件解析失败会导致整个会话无法恢复 ([#4080](https://github.com/OpenHands/software-agent-sdk/issues/4080))，用户期望系统能有更优雅的降级处理。

### 8. 待处理积压

以下是一些需要维护者重点关注，尤其是期待社区响应的长期未解决问题。

- **[#2911] [OPEN] feat(security): add ToolShieldLLMSecurityAnalyzer**：这是一个从 4 月就打开的 PR，旨在增加 LLM 安全分析工具，对于项目安全性至关重要，但长期未有实质性合并或关闭的进展。
  - **链接**: [#2911](https://github.com/OpenHands/software-agent-sdk/pull/2911)
- **[#3841] [OPEN] LLMProfile / AgentProfile identity asymmetry**：这个于 6 月 22 日提出的 Issue 指出了两个 Profile 类型在身份标识上的不对称问题，是 Agent Profiles 核心功能的一个潜在设计缺陷，至今只有一个评论。
  - **链接**: [#3841](https://github.com/OpenHands/software-agent-sdk/issues/3841)
- **[#3894] [OPEN] feat(mcp): subscribe to tools/list_changed for progressive-disclosure servers**：支持 MCP 服务器的渐进式工具列表变化，是一个有价值的增强，自 6 月 26 日起未收到更多关注。
  - **链接**: [#3894](https://github.com/OpenHands/software-agent-sdk/pull/3894)

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据提供的数据为您生成的 Pi 项目动态日报。

---

### Pi 项目动态日报 | 2026-07-11

**项目名称:** Pi (github.com/earendil-works/pi)
**报告周期:** 2026-07-10 至 2026-07-11
**数据来源:** GitHub Issues / PRs / Releases

---

#### 1. 今日速览

今日项目活跃度极高，共处理 **57 条 Issues** 和 **12 条 PR**，并发布了新版本 v0.80.6。社区围绕 **GPT-5.6 系列模型** 的集成产生了集中讨论，相关的新功能请求和缺陷修复构成了今日活动的核心。项目维护者响应迅速，大量PR被合并，有效解决了模型适配、会话亲和性及用户自托管环境下的关键回归问题。总体而言，项目处于高速迭代的“快车道”上，对技术前沿（如新模型、新API）的跟进非常及时。

#### 2. 版本发布

**发布版本: v0.80.6**
- **更新时间:** 近期发布
- **核心亮点:**
    - **引入 `max` 思考级别**: 新增了位于 `xhigh` 之上的最高思考级别 `max`。这主要为了原生支持 GPT-5.6 及适配后的 Claude 模型，使得 Pi 的思考级别阶梯 (`off / minimal / low / medium / high / xhigh / max`) 与最新模型 API 对齐。
    - **全平台支持**: `max` 级别已集成到 CLI (`--thinking max`)、SDK、RPC 及模型选择器中。
    - **主题自定义**: 用户可通过自定义主题定义 `thinkingMax` 行为。
- **破坏性变更/迁移注意**: 无明确破坏性变更，但使用旧版本 CLI 或 SDK 的程序可能无法识别新的 `max` 级别。更新后建议检查自定义主题配置。

#### 3. 项目进展

今日项目进展以 **Bug 修复** 和 **新模型/API 适配** 为主，共合并/关闭了 10 个 PR，项目向前迈进了坚实的一步。

- **核心功能推进**:
    - **约束采样 (Constrained Sampling)**: **#6341** PR 引入了对工具(Tools)的可选约束采样支持。这意味着模型在生成工具参数时，将能更好地遵循 JSON schema 或语法规则，是提升工具调用可靠性的重要特性。
    - **动态工具加载 (Message-Anchored Tool Loading)**: **#6474** 合并，允许在对话中途动态引入新的工具，而无需在初始请求中就列出所有工具。这对于在复杂工作流中按需添加工具的场景非常关键。

- **稳定性与兼容性修复**:
    - **OpenRouter 会话亲和性**: **#6496** 修复了 OpenRouter 提供者无法发送正确的 `session_id` 头信息的问题，解决了缓存失效和会话追踪的痛点。
    - **嵌入式库支持**: **#6501** 修复了将 Pi 作为库嵌入时，主题初始化和扩展运行时复用存在的问题，提升了嵌入场景的稳定性。
    - **Bun 运行时超时问题**: **#6503** 通过升级 Bun 版本并支持环境变量来覆盖其内置的 HTTP 空闲超时，直接关联并修复了 **#6476** 报告的回归问题。
    - **模型目录修正**: **#6490** 和 **#6481** 分别修复了 Fable-5 提供者的思考级别错误和 OpenRouter 模型的上下文长度计算错误。

#### 4. 社区热点

今日社区讨论的焦点几乎都集中在 **GPT-5.6 模型家族** 上，这反映了社区对前沿模型的强烈关注度。

- **[#6475] Add GPT-5.6 (Sol/Terra/Luna) to the GitHub Copilot provider catalog** (👍 6, 评论 8)
    - **链接:** [Issue #6475](https://github.com/earendil-works/pi/issues/6475)
    - **分析:** 该 Issue 要求在 GitHub Copilot 提供者目录中添加 GPT-5.6 的三个变体模型。这是社区对最新模型支持的最直接呼声，评论集中在新模型在 Copilot 中的实际访问方法。
- **[#6097] Add support for 'max' thinking level** (👍 17, 评论 2)
    - **链接:** [Issue #6097](https://github.com/earendil-works/pi/issues/6097)
    - **分析:** 这个获得了 17 个赞的 Issue 是 v0.80.6 上新功能的发源地。它代表了一组用户对最高级别推理能力的需求，与 OpenAI 和 Anthropic 的新模型能力直接挂钩。社区通过此功能请求，成功驱动了项目核心特性的演进。
- **[#6489] feat(ai): add ultra thinking level** (已关闭)
    - **链接:** [PR #6489](https://github.com/earendil-works/pi/pull/6489)
    - **分析:** 有趣的是，在 `max` 级别的基础上，社区快速响应并提出了 `ultra` 级别，试图抢占未来可能出现的更高阶思考能力。这说明部分用户对模型能力的追求是无止境的，也显示了社区在模型能力分级上的前瞻性思考。

#### 5. Bug 与稳定性

今日报告的 Bug 主要集中在 **模型适配、回归问题及 Windows 兼容性** 上。部分严重问题已有对应的修复 PR。

- **严重**:
    - **[#6476] Regression: httpIdleTimeoutMs no longer respected for self-hosted provider** (新开, **已有 PR #6503**)
        - **链接:** [Issue #6476](https://github.com/earendil-works/pi/issues/6476)
        - **分析:** 用户在升级至 v0.80.6 后，自托管模型的请求超时。这是一个典型的**回归问题**，好在项目已通过升级 Bun 运行时的方式快速定位并提供修复，目前该问题应已解决。
    - **[#6477] Compaction summary requests omit the session ID, breaking compaction on some OpenAI-Codex models** (新开)
        - **链接:** [Issue #6477](https://github.com/earendil-works/pi/issues/6477)
        - **分析:** GPT-5.6 模型在使用 compaction 功能时失败，原因是压缩请求缺少 session ID。这影响了新模型的功能完整性，是目前需要优先处理的 Bug。
- **中等**:
    - **[#6300] Windows: Input line is redrawn on every keystroke** (未关闭)
        - **链接:** [Issue #6300](https://github.com/earendil-works/pi/issues/6300)
        - **分析:** Windows 平台下的 TUI 输入回显问题，严重影响 Windows 用户的使用体验。该问题已存在多日，影响范围有限但体验较差，建议优先处理。
    - **[#6472] compaction.enabled=false bypassed by overflow recovery path** (未关闭)
        - **链接:** [Issue #6472](https://github.com/earendil-works/pi/issues/6472)
        - **分析:** 用户显式禁用了自动压缩，但溢出恢复路径仍会触发，导致设置项“形同虚设”，逻辑缺陷明显。
- **轻微**:
    - **[#6206] Clamping to context window prevents artificial context limits** (未关闭)
        - **链接:** [Issue #6206](https://github.com/earendil-works/pi/issues/6206)
        - **分析:** 一个设计上的取舍问题，用户试图设置比模型上下文窗口更小的 `max_tokens`，但当前逻辑会强制将其钳制到上下文窗口大小。

#### 6. 功能请求与路线图信号

除了对 GPT-5.6 的支持外，今日还浮现了一些其他有价值的功能请求。

- **长期功能确定**:
    - **[#6341] Support Strict Tools / Grammar (PR #6341)** (已合并)
        - **链接:** [PR #6341](https://github.com/earendil-works/pi/pull/6341)
        - **信号**: 支持“严格工具”和“语法感知探测”的功能已通过 PR 落地，这将是 Pi SDK 的一大增强，为未来构建更可靠、更结构化的 AI Agent 奠定了基础。
- **潜在未来方向**:
    - **[#6485] Preserve unhandled Bedrock ConverseStream stop reasons** (未关闭)
        - **链接:** [Issue #6485](https://github.com/earendil-works/pi/issues/6485)
        - **信号**: 用户要求对 Bedrock 的异常停止原因进行更友好地展示，这体现了对生产环境中可观测性的需求。
    - **[#6504] Add goal extension example for autonomous multi-turn task execution** (已关闭, 对应 PR #6505 已合并)
        - **链接:** [Issue #6504](https://github.com/earendil-works/pi/issues/6504)
        - **信号**: 社区期望 Pi 能更好地支持多轮自主任务执行。作为示例扩展，它可能不是核心功能，但为生态系统的丰富提供了案例，吸引更多开发者构建复杂 Agent。

#### 7. 用户反馈摘要

从今日的 Issue 和 PR 中，可以提炼出以下用户声音：

- **对前沿技术的渴望与痛点**: 用户急切地想要使用 GPT-5.6 模型，但适配过程（如 #6475, #6465, #6477）中暴露了 `model catalog` 更新不及时、新模型 API 细节差异等问题。这既是痛点，也是项目价值所在。
- **对自托管用户的挑战**: #6476 反映了自托管用户在使用新版本时遇到的兼容性风险，他们依赖稳定且可预测的配置行为。Bun 升级带来的隐性问题值得警惕。
- **扩展生态的初现**: 多个关于扩展的 Issue（#6504，#6509, #4586）和 PR 表明，Pi 的扩展生态正在萌芽。开发者正在积极探索如何通过扩展来增强 Pi 的功能，例如成本显示、多轮任务等。
- **Beta 用户的抱怨**: #6259 中描述的 `content is not iterable` 错误，直接导致了某些模型的工具使用功能完全失效，这反映了用户在面对不稳定模型时对主项目稳定性的高要求。

#### 8. 待处理积压

以下为长期未更新或未解决的关键议题，提醒维护者关注。

- **[#6306] [OPEN] Support Strict Tools / Grammar** (评论 22, 创建 7 天)
    - **链接:** [Issue #6306](https://github.com/earendil-works/pi/issues/6306)
    - **状态**: 讨论了 7 天，评论数最多。虽然已有 PR #6341 解决了部分问题，但原始 Issue 仍在开放，可能涉及更广泛的讨论和遗留问题，需要最终关闭。
- **[#6101] [CLOSED] Embedded library: shared extension runtime is poisoned across sessions** (已关闭，但提醒关注)
    - **链接:** [Issue #6101](https://github.com/earendil-works/pi/issues/6101)
    - **状态**: 虽然该 Issue 已关闭，且其关联的 PR #6501 已部分修复。但由于其复杂性，建议在后续版本中继续关注“嵌入场景”的稳定性，以防有未覆盖的边界情况。
- **[#6216] [OPEN] feat: Add Amazon Bedrock Mantle OpenAI Responses provider** (创建 10 天)
    - **链接:** [PR #6216](https://github.com/earendil-works/pi/pull/6216)
    - **状态**: 这是一个重要的新 provider PR，但已存在 10 天未合并。考虑到今日活动繁忙，可能是被新模型适配工作淹没。该 PR 对 AWS 用户很重要，建议尽快安排审查。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

好的，遵照您的指示。以下是为您生成的 LiteLLM 项目动态日报。

---

# LiteLLM 项目动态日报 | 2026-07-11

## 1. 今日速览

过去 24 小时内，LiteLLM 项目活动保持极高活跃度。共处理 78 条 Issue 和 253 个 PR，显示出强大的开发者参与度和社区反馈规模。特别是 **Rust 迁移计划 (Issue #31263)** 和 **OpenRouter 流式成本丢失 (Issue #16021)** 成为社区讨论焦点。我们注意到，尽管处理了大量 PR，仍有超过 150 个 PR 等待合并，项目核心团队的合并能力面临考验。总体来看，项目处于快速迭代期，方向明确，但积压工作也逐渐增多。

- **活跃度评分**: 9/10 (极高)
- **今日关注**: Rust 迁移 (重大架构变更)、OpenRouter 成本问题 (关键计费 Bug)、大量 PR 积压 (项目瓶颈)

## 2. 版本发布

- **v1.93.0-dev.3**: 作为开发版本发布，主要引入了 Docker 镜像签名验证功能，增强了用户在生产环境中对官方镜像的安全信任。此版本没有提及破坏性变更或迁移注意事项。从上下文看，该版本可能针对此前报告的一系列 Stream 响应和 OpenRouter 成本问题进行了修复。

## 3. 项目进展

今日合并/关闭了 100 个 PR，展示了项目在多个方向上的持续进步。以下是一些关键进展：

- **基础设施与成本优化**:
    - **PR #32662** (已关闭): 将协调 Redis 提升为 Helm Chart 和 Terraform 的一等公民，增强了部署的灵活性。
    - **PR #32661** (已关闭): 允许独立配置协调 Redis，不依赖于响应缓存，优化了分布式部署架构。
    - **PR #32655** (已关闭): 在 OpenTelemetry 集成中，新增了 `gen_ai.client.operation.exception` 事件，用于追踪失败的 LLM 调用，提升了可观测性。

- **功能修复与增强**:
    - **PR #32837**: `fix(responses)`: 修复了在 Chat Completions 到 Responses API 转换过程中丢失 `reasoning_tokens` 的问题。
    - **PR #32833**: `fix(anthropic)`: 修复了 Vertex AI 上 Anthropic 模型版本后缀解析问题，确保能正确启用自适应思考 (Adaptive Thinking) 功能。
    - **PR #32836**: `fix(model_cost)`: 为 Gemini 图像生成模型添加了 `supports_reasoning: false` 标签，修正了成本计算。

- **新功能探索**:
    - **PR #32841**: `feat(ui)`: 新增从 UI 配置面板编辑 fallback 链的功能，提升了用户体验。
    - **多个 MCP 相关 PR (#32794, #32804)**: 正在为 MCP (Model Context Protocol) 集成开发 `dcr_bridge` 模块，显示项目正在拥抱最新的开放协议。

**总结**: 项目在架构现代化（Redis、OTel）、API 兼容性修复（Responses、Anthropic）和功能扩展（MCP、UI）上均有实质性进展，核心功能趋于稳定。

## 4. 社区热点

- **热度最高**: **[Issue #31263] LiteLLM Rust Migration** (评论 7, 👍 9)
    - **链接**: [https://github.com/BerriAI/litellm/issues/31263](https://github.com/BerriAI/litellm/issues/31263)
    - **分析**: 这是近期最重大的社区讨论。用户对用 Rust 重写以降低延迟、提升性能表现出极大兴趣。该 Issue 作为“母题”被创建，标志着项目技术路线的一次关键转向。社区的关注点集中在性能提升幅度、初始特性覆盖度以及与现有 Python 生态的集成方式。

- **计费问题引关注**: **[Issue #16021] OpenRouter 流式响应成本信息丢失** (评论 15, 👍 3)
    - **链接**: [https://github.com/BerriAI/litellm/issues/16021](https://github.com/BerriAI/litellm/issues/16021)
    - **分析**: 该问题持续引发讨论。用户发现在流式模式下，OpenRouter 返回的 `usage.cost` 字段会被丢弃，导致成本无法准确记录。对于依赖精准计费的企业用户，这是一个关键的 Bug。社区强烈要求解决方案，因为非流式模式工作正常，表明这是一个特定实现路径上的逻辑缺陷。

- **超时错误困扰**: **[Issue #14635] "Connection timed out after None seconds"** (评论 7, 👍 8)
    - **链接**: [https://github.com/BerriAI/litellm/issues/14635](https://github.com/BerriAI/litellm/issues/14635)
    - **分析**: 该 Bug 因显示“None seconds”的奇怪错误信息而获得大量点赞。它暴露了超时处理机制中的严重缺陷，不仅影响功能，还带来了糟糕的调试体验，用户强烈希望修复。

## 5. Bug 与稳定性

- **严重级别: 高**
    - **[Issue #16021] OpenRouter 流式成本丢失** (计费准确性)
        - **状态**: OPEN，已有多次讨论，但无明确 Fix PR。
        - **链接**: [https://github.com/BerriAI/litellm/issues/16021](https://github.com/BerriAI/litellm/issues/16021)
    - **[Issue #14635] 超时时间显示为 None** (系统稳定性)
        - **状态**: OPEN，已标记为 stale，需维护者回应。
        - **链接**: [https://github.com/BerriAI/litellm/issues/14635](https://github.com/BerriAI/litellm/issues/14635)

- **严重级别: 中**
    - **[Issue #25390] Anthropic 兼容接口流式模式丢失 tool_use.input** (功能异常)
        - **描述**: 使用 Gemma 模型时，流式 Tool Call 的输入参数丢失。
        - **状态**: OPEN
        - **链接**: [https://github.com/BerriAI/litellm/issues/25390](https://github.com/BerriAI/litellm/issues/25390)
    - **[Issue #27184] Bedrock Claude 4.6 API 错误** (兼容性问题)
        - **描述**: 使用新版 Claude 模型时，出现 `tool_choice.type: Field required` 错误。
        - **状态**: OPEN
        - **链接**: [https://github.com/BerriAI/litellm/issues/27184](https://github.com/BerriAI/litellm/issues/27184)
    - **[Issue #32787] `model_info` 中成本值类型问题** (数据不一致)
        - **描述**: 成本值在数据库往返后可能变为字符串，导致计算错误。
        - **状态**: OPEN，已由社区成员提出，但未指定 Fix PR。
        - **链接**: [https://github.com/BerriAI/litellm/issues/32787](https://github.com/BerriAI/litellm/issues/32787)

## 6. 功能请求与路线图信号

- **Rust 迁移 (路线图核心)**: **[Issue #31263]** 被定位为未来架构的核心，展示了项目追求极致性能的决心。这将是未来版本的基石。
    - **链接**: [https://github.com/BerriAI/litellm/issues/31263](https://github.com/BerriAI/litellm/issues/31263)

- **Langfuse Python SDK v4 支持**: **[Issue #24123]**
    - **分析**: 用户强烈要求更新对 Langfuse 回溯集成的支持，以使用最新的 SDK 功能。该项目已获得 6 个 👍，说明有明确需求。但当前未看到相关 PR，可能在等待版本规划。
    - **链接**: [https://github.com/BerriAI/litellm/issues/24123](https://github.com/BerriAI/litellm/issues/24123)

- **MCP (Model Context Protocol) 集成**: 今日有 2 个相关 PR (**[#32794](https://github.com/BerriAI/litellm/pull/32794)**, **[#32804](https://github.com/BerriAI/litellm/pull/32804)**) 被打开，涉及 `dcr_bridge` 模块。这表明 LiteLLM 正在积极拥抱 MCP 这一新兴标准，有望在未来版本中作为 Gateway 的核心特性推出。

- **其他值得关注的功能请求**:
    - 自定义分词器计费 ([#19332](https://github.com/BerriAI/litellm/issues/19332))。
    - 基于 Session ID 过滤日志 ([#22973](https://github.com/BerriAI/litellm/issues/22973))。
    - 流式心跳消息 ([#14953](https://github.com/BerriAI/litellm/issues/14953))。

## 7. 用户反馈摘要

- **痛点**:
    - **计费不准确**：`OpenRouter` 流式成本丢失 (Issue #16021) 和 `ElevenLabs` 模型成本计算失败 (Issue #18058) 是影响用户付费决策的严重问题。
    - **调试困难**：超时时间显示为 `None` (Issue #14635) 和随机出现 `No API key passed in` 错误 (Issue #25063) 让用户难以定位问题根源。
    - **服务器端负载**：有用户反映服务器在高峰期出现大量 429 错误 (Issue #32775) 和因负载超时 (Issue #29351)。
    - **API 兼容性**：`Responses API` 在流式和非流式下的行为不一致 (Issue #25390)、`Bedrock` 跨账号角色被忽略 (Issue #25884) 等问题增加了集成的复杂度。

- **满意之处**:
    - **功能丰富**：用户认可 LiteLLM 支持的模型和功能（如文件理解）广度。
    - **项目活性**：Rust 迁移计划和频繁的版本发布让用户看到了项目的长期生命力。

## 8. 待处理积压

以下为长期未响应或已关闭但未完全解决的重要问题，建议维护者重点关注：

| 问题 | 问题标签 | 是否存在 Fix PR | 推荐行动 | 链接 |
| :--- | :--- | :--- | :--- | :--- |
| [Issue #8244] 精确 Token 计数 | `stale`, `enhancement` | 否 (已关闭) | 重新评估必要性，因其影响计费准确性，可能需要在 Rust 重写中考虑。 | [查看](https://github.com/BerriAI/litellm/issues/8244) |
| [Issue #14635] 超时显示 `None` | `stale`, `bug` | 否 | 核心 Bug，影响用户体验，需标记优先级并分配开发者。 | [查看](https://github.com/BerriAI/litellm/issues/14635) |
| [Issue #18058] ElevenLabs 成本计算 | `stale`, `bug` | 否 | 特定模型 Bug，影响使用该模型的部分用户。 | [查看](https://github.com/BerriAI/litellm/issues/18058) |
| [Issue #15360] 数据库插入重复计划 | `stale`, `bug` | 否 | 属于数据库层面的性能与稳定性问题，可能在大规模部署中引发问题。 | [查看](https://github.com/BerriAI/litellm/issues/15360) |

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-07-11

## 1. 今日速览
过去24小时项目保持高活跃度：**46条** Pull Request 更新（其中18条已合并/关闭），**1条** Issue 关闭（依赖安全漏洞修复），无新版本发布。开发重点集中在 **CHASM Nexus** 功能完善、**独立活动操作**（Pause/Unpause/Reset）的稳定性修补、以及 **CI 报告**与**基础设施工具**的优化。项目整体健康，社区协作节奏稳定。

## 2. 版本发布
无新版本发布。

## 3. 项目进展
今日合并/关闭的 **18条** PR 中，以下关键变更推动了项目前进：

- **发布分支准备 & API 更新**  
  - [#11015](https://github.com/temporalio/temporal/pull/11015) 准备 **v1.32.0** 发布分支（覆盖治理文件、更新依赖）。  
  - [#11011](https://github.com/temporalio/temporal/pull/11011) 升级 API 至 `v1.63.3`（旧版本替换）——保障云端与社区版本同步。

- **活动操作功能修复**  
  - [#11010](https://github.com/temporalio/temporal/pull/11010) 修复 `UpdateActivityExecutionOptions` 传入 `nil` 重试策略时使用默认策略的行为。  
  - [#11013](https://github.com/temporalio/temporal/pull/11013) 禁止对缺少快照的独立活动执行 `restore_original`，防止崩溃。  
  - [#11016](https://github.com/temporalio/temporal/pull/11016) 保留待处理活动的下一次重试延迟，避免更新选项时意外缩短重试时间。  
  - [#11020](https://github.com/temporalio/temporal/pull/11020) 修复活动暂停/取消暂停的场景下去重逻辑，避免重复取消导致状态错误。

- **WCP 工作流分页**  
  - [#10880](https://github.com/temporalio/temporal/pull/10880) 合并 `RespondWorkflowTaskCompleted` 服务端分页支持（动态配置关闭），提升大规模任务场景稳定性。

- **集群管理**  
  - [#10997](https://github.com/temporalio/temporal/pull/10997) 修复集群删除校验边缘情况：仅当被删除集群仍被当前集群参与的命名空间引用时才阻止删除。

- **测试与工具**  
  - [#11008](https://github.com/temporalio/temporal/pull/11008) 捕获测试集群创建事件并输出 JSON，便于分析资源使用。  
  - [#11018](https://github.com/temporalio/temporal/pull/11018) 抽取可复用的 GitHub 辅助函数至公共包。

项目在 **独立活动生命周期管理**、**CHASM Nexus** 和 **多集群容错** 三个维度均有显著推进。

## 4. 社区热点
今日虽无明确评论数（数据显示为 `undefined`），但以下 PR 因内容重要或涉及敏感变更，值得关注：

- [#11019](https://github.com/temporalio/temporal/pull/11019) “Report final failures in CI notifications” —— 作者 `stephanos` 连续提交多条 CI 与工具优化，该 PR 旨在让 CI 通知包含失败详情，提升社区和开发者排查效率。  
- [#11012](https://github.com/temporalio/temporal/pull/11012) “[NOT READY] Add Nexus tenant rate-limit interceptor” —— 首次引入租户级别限流接口（无操作默认），标志着 Nexus 功能向生产级多租户方向演进，可能引发后续容量规划讨论。  
- [#10106](https://github.com/temporalio/temporal/pull/10106) “Implement Pause/Unpause/Reset/UpdateOptions for standalone activities” —— 已开放 **两个多月**，仍未合并。该 PR 是活动操作功能的基础，今日有多个关联修复 PR（#11010、#11013、#11016、#11020）密集合并，表明核心部分正在稳定化，预计近期可合并。

社区诉求集中在 **独立活动管理** 的完整性与正确性，以及 **CHASM** 路径的调试能力增强。

## 5. Bug 与稳定性
- **严重**：依赖 `pgx v5.9.2` 存在认证降级漏洞（CWE-306）  
  - Issue [#10676](https://github.com/temporalio/temporal/issues/10676) 已于今日关闭（未产生新评论），表明已通过升级至 `v5.10.0` 或加入补丁修复。  
- **中等**：活动暂停去重逻辑缺陷  
  - PR [#11020](https://github.com/temporalio/temporal/pull/11020) 修复了在取消暂停与重复请求之间可能错误恢复暂停状态的问题。  
- **中等**：集群删除误拦  
  - PR [#10997](https://github.com/temporalio/temporal/pull/10997) 纠正了删除远程集群时过于严格的校验逻辑。  
- **低**：任务验证器未传递尝试计数  
  - PR [#10985](https://github.com/temporalio/temporal/pull/10985) 增加 `attempt count` 到任务属性，并补充 standby 校验，提升容错决策精度。

所有已知严重问题已有对应修复或已在最新发布中包含。

## 6. 功能请求与路线图信号
以下 PR 明确指向 **v1.32.0** 或未来版本的新功能：

- **Nexus 多租户限流**（[#11012](https://github.com/temporalio/temporal/pull/11012)）—— 定义 `TenantRateLimitInterceptor` 接口，配有错误码和 FX provider，为云服务与本地部署提供统一限流扩展点。  
- **结构化事件框架**（[#10890](https://github.com/temporalio/temporal/pull/10890)）—— 引入可插拔的 `events.Handler`，支持类型化编码、全局事件注册及生命周期事件（命名空间、复制）。  
- **CHASM 一致性级别选项**（[#10957](https://github.com/temporalio/temporal/pull/10957)）—— 新增 `RefConsistencyLevel` 过渡选项，允许调用方指定多版本状态检查的粒度。  
- **独立活动 ExecutionTime 可见性**（[#11017](https://github.com/temporalio/temporal/pull/11017)）—— 为独立活动暴露 `ExecutionTime` 字段，已有 `ListActivityExecutions` 支持。  
- **被动集群任务再生**（[#11005](https://github.com/temporalio/temporal/pull/11005)）—— 当时间跳过被复制到被动集群时，重新生成 CHASM 任务，保障多数据中心一致性。

这些特性共同勾画出 **Nexus 生态完善**、**可观测性增强** 和 **跨区域容错** 的路线图。

## 7. 用户反馈摘要
今日无 Issue 或 PR 评论中包含显式用户反馈。近期唯一用户参与的 Issue（#10676）为自动依赖通知，未产生讨论。社区活跃度主要体现在贡献者的代码提交与修复，尚无明显用户使用痛点或投诉。

## 8. 待处理积压
- **PR [#10106](https://github.com/temporalio/temporal/pull/10106)**（开放超过70天）  
  实现独立活动的 Pause/Unpause/Reset/UpdateOptions。尽管今日有多条关联修复合并，但该主 PR 仍未合并。建议维护者尽快评估并推动合并，以免修复与基础功能脱节。  
- **PR [#10985](https://github.com/temporalio/temporal/pull/10985)**（开放2天）  
  添加尝试计数到任务属性，需在 standby 执行器中校验。未收到反对意见，建议尽快完成测试并合并。  
- **其他状态为 OPEN 的 PR** 共28条，其中不少是今日提交的新功能（如 #11019、#11012），尚在早期审查阶段，未见长时间阻塞。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*