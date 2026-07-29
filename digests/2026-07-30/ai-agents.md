# OpenClaw 生态日报 2026-07-30

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-29 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，以下是为您生成的 OpenClaw 项目动态日报。

---

# OpenClaw 项目动态日报 (2026-07-30)

## 1. 今日速览

OpenClaw 项目今日保持极高活跃度，过去24小时内共有 **1000 条** Issues 和 PRs 更新。其中，新开/活跃的 Issue 达 **423 条**，待合并的 PR 达 **416 条**，显示社区贡献和问题反馈非常积极。P1 级别（高优先级）的问题占据了讨论的主体，核心矛盾集中在会话（Session）稳定性、消息丢失（Message Loss）、认证（Auth）故障以及因进程泄漏/内存溢出导致的崩溃循环（Crash Loop）。尽管未发布新版本，但多个针对关键 Bug 的修复 PR 已进入“等待维护者审查”阶段，表明项目正在积极解决当前的稳定性危机。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日无重要 PR 被合并。项目整体状态停留在“修复问题”的攻坚阶段，核心工作围绕大量 P1 级别的 Bug 报告展开。虽然无新功能落地，但有多项修复 PR 已经提交并标记为“ready for maintainer look”，显示出社区对改善项目稳定性的积极努力。

- **关键修复 PR 动态：**
    - **PR #116109** (`fix(hooks): route mapped wakes to configured sessions`): 解决Issue #64556，修复 webhook 映射中 `action="wake"` 时，`agentId` 和 `sessionKey` 配置被忽略，导致事件错误进入默认会话的问题。这解决了多代理配置下的路由混乱问题。([链接](https://github.com/openclaw/openclaw/pull/116109))
    - **PR #115617** (`fix(xai): follow OAuth default model automatically`): 修复 xAI OAuth 初始化时固定模型的问题，确保后续模型更新可以自动适配。([链接](https://github.com/openclaw/openclaw/pull/115617))
    - **PR #95662** (`feat(mattermost): auto-engage on replies to the bot's own thread`): 改进 Mattermost 渠道体验，使机器人能够自动回复其所在线程内的用户回复，无需再依赖 @-mention。([链接](https://github.com/openclaw/openclaw/pull/95662))
    - **PR #95830** (`fix(telegram): route poll answers into sessions`): 修复 Telegram 投票功能，确保用户的投票选择能够正确路由回发起投票的代理会话。([链接](https://github.com/openclaw/openclaw/pull/95830))

## 4. 社区热点

今日社区焦点高度集中在几个高优先级、影响广泛的稳定性问题上。

1.  **工具输出渲染为图片，代理无法读取文本 (Issue #99241)**
    - **热度:** 26条评论，已被关闭。
    - **内容:** 在长时间运行的 ANSI 密集型工具工作流中，工具返回的文本结果会被压缩成一个“图片附件”占位符（如 `(see attached image)`），导致代理无法读取原始的 stdout/stderr 文本，从而失去了关键证据。此问题对依赖文本工具输出的自动化工作流影响巨大。([链接](https://github.com/openclaw/openclaw/issues/99241))

2.  **Codex 钩子进程 CPU 满载导致网关 RPC 死锁 (Issue #91009)**
    - **热度:** 18条评论，仍为开启状态。
    - **内容:** Codex 集成会生成大量短暂的 `openclaw-hooks` 进程，这些进程消耗100% CPU，最终导致网关 RPC 调用完全卡死。这揭示了 Codex 集成中严重的资源管理和进程生命周期问题。([链接](https://github.com/openclaw/openclaw/issues/91009))

3.  **崩溃循环断路器永久禁用 Discord/WhatsApp 且恢复失败 (Issue #115326)**
    - **热度:** 16条评论，仍为开启状态。
    - **内容:** 一个回归 Bug，导致网关成功启动后，崩溃循环断路器永久性地抑制了 Discord 和 WhatsApp 渠道的通讯。官方文档提供的恢复路径 (`channels.start`) 因 WebSocket 1006 错误而失效，使得渠道通信陷入彻底的不可恢复状态。这严重影响了终端的核心通信能力。([链接](https://github.com/openclaw/openclaw/issues/115326))

4.  **代理回复文本被静默截断 (Issue #84516)**
    - **热度:** 11条评论，仍为开启状态。
    - **内容:** 通过 API (`openclaw message`) 调用时，模型回复在约1000-1100字符处被静默截断，且无任何错误提示。这给依赖 api 构建的用户带来了隐蔽且严重的数据丢失问题。([链接](https://github.com/openclaw/openclaw/issues/84516))

## 5. Bug 与稳定性

今日报告的 Bug 主要集中在会话中断、消息丢失和进程稳定性方面，问题严重性普遍较高，已形成一些明显的复现模式。

**P0/P1 严重 Bug 列表：**

- **网关 OOM 导致核心转储风暴 (Issue #115424)**
    - **严重程度:** P1
    - **描述:** 长时间运行的会话导致 V8 堆内存溢出（OOM），而自动恢复机制将单次崩溃转换为多达7次的核心转储循环，导致更大的服务中断。([链接](https://github.com/openclaw/openclaw/issues/115424))

- **架构降级恢复不应删除状态数据库 (Issue #115421)**
    - **严重程度:** P0
    - **描述:** 当状态数据库 schema 版本不匹配时，降级恢复逻辑（Schema downgrade recovery）会直接清空或隔离旧的数据库文件（如 `openclaw.sqlite`），导致所有 cron 任务等持久化状态完全丢失。([链接](https://github.com/openclaw/openclaw/issues/115421))

- **子代理完成通知被静默丢弃 (Issue #92433)**
    - **严重程度:** P1
    - **描述:** 当子代理完成时，如果其容器端的运行（run）在投递通知前结束，该通知会被静默丢弃。([链接](https://github.com/openclaw/openclaw/issues/92433))

- **OpenClaw 泄漏子进程导致僵尸进程堆积 (Issue #97616)**
    - **严重程度:** Bug
    - **描述:** 从钩子和工具执行产生的子进程未被正确回收，导致大量僵尸进程堆积，最终运行时性能下降。([链接](https://github.com/openclaw/openclaw/issues/97616))

- **MCP 回环传输断连后无法自动重连 (Issue #98435)**
    - **严重程度:** P1
    - **描述:** 网关重启后，MCP 回环传输不会自动重新握手，导致下一个工具调用直接失败，但会话恢复状态却显示 `recovered=1`，信息具有误导性。([链接](https://github.com/openclaw/openclaw/issues/98435))

## 6. 功能请求与路线图信号

尽管修复 Bug 是当前主题，但仍有几项清晰的功能请求出现，暗示了项目的功能演进方向。

- **记忆信任标记 (Memory Trust Tagging - Issue #7707):** 用户提出基于记忆条目的来源（用户指令、网页抓取、第三方技能）进行信任标记，以防范隐藏在不可信内容中的“记忆投毒”攻击。这是一个重要的安全增强方向，已有 PR 正在处理。([链接](https://github.com/openclaw/openclaw/issues/7707))
- **全动态模型发现 (Fully Dynamic Model Discovery - Issue #10687):** 用户需求强烈，希望针对 OpenRouter 等模型更新频繁的提供商，实现动态模型发现，而不是依赖静态的生成目录。这表明用户对模型集的灵活性和最新性有较高要求。([链接](https://github.com/openclaw/openclaw/issues/10687))
- **网关生命周期钩子 (Gateway Lifecycle Hooks - Issue #43454):** 用户希望在工作区内增加自动响应代理生命周期的钩子（如子代理完成、工具调用阈值、轮次完成），以实现更高级的自动化和监控逻辑。虽然该 PR 已关闭，但其设计思路可能被纳入后续架构。([链接](https://github.com/openclaw/openclaw/issues/43454))

## 7. 用户反馈摘要

从今日的讨论中，可以提炼出以下用户痛点和诉求：

- **稳定性是第一要务：** 大量反馈集中于服务不可用（渠道被抑制）、消息丢失（静默截断、未送达）、以及崩溃重现（OOM、进程泄漏）。用户希望项目优先解决这些导致服务中断的问题。
- **故障恢复体验差：** 无论是 OOM 后的核心转储风暴、Schema 降级时的数据清空，还是崩溃循环后的渠道不可恢复，都表明系统的故障恢复机制不仅不完善，甚至加剧了问题。用户期望更优雅、更健壮的恢复方案。
- **配置和状态管理存在风险：** MCP 重连虚假的成功状态、Schema 降级导致数据丢失，都指向状态管理中存在设计缺陷。用户希望状态迁移和恢复流程有更清晰、更安全的保障。
- **对 Codex/App-server 集成有稳定性质疑：** 多个 P1 级别问题（#91009, #84516, #86215）都指向 Codex 集成路径，显示了该功能的复杂度和稳定性风险。用户期望更可靠的消息处理和资源管理。

## 8. 待处理积压

以下为长期未解决或今日未得到有效回应的重要问题，建议维护团队重点关注。

- **Issue #7707: Memory Trust Tagging by Source:** 这是一个从2026年2月就开始的 P2 功能请求，关于防范记忆投毒，具有重要的安全意义，但长时间处于 `needs-product-decision` 和 `needs-maintainer-review` 状态。([链接](https://github.com/openclaw/openclaw/issues/7707))
- **Issue #10687: Models: fully dynamic model discovery:** 同样是一个长期开放的需求，用户对模型更新的灵活性有持续呼声，但进展缓慢。([链接](https://github.com/openclaw/openclaw/issues/10687))
- **Issue #73537: Feature Request: Add production-readiness stability label to releases:** 用户建议为版本发布增加生产就绪的稳定性标签，以便用户评估风险，这反映了社区对版本稳定性的担忧和明确需求。([链接](https://github.com/openclaw/openclaw/issues/73537))
- **PR #81208: fix(amazon-bedrock-mantle): dedupe the IAM token-failure diagnostic per region:** 这个修复 AWS 凭证无效时日志泛滥的 PR 从5月份开始就处于 `waiting on author` 状态，急需推动。([链接](https://github.com/openclaw/openclaw/pull/81208))

---

## 横向生态对比

好的，作为您的资深技术分析师，我已根据您提供的六份项目动态日报，为您生成了一份全面的横向对比分析报告。报告旨在为技术决策者和开发者提供清晰、有数据支撑的生态洞察。

---

### AI 智能体与个人 AI 助手开源生态横向对比分析报告 (2026-07-30)

#### 1. 生态全景

当前，个人 AI 助手与自主智能体开源生态正处于 **高速迭代与分化并存** 的关键期。项目普遍在 **稳定性、性能、安全性** 三大核心矛盾中寻求突破。一方面，以 OpenClaw、Hermes Agent 为代表的大型项目正承受着规模增长带来的“成长的烦恼”，核心稳定性问题（如内存溢出、会话中断、配置隔离）成为社区热议焦点；另一方面，基础设施与工具链项目（如 LiteLLM、Temporal）则在积极填补生态空白，围绕 MCP (Model Context Protocol) 集成、成本控制、跨平台兼容性等方向快速演进。整体而言，社区对“开箱即用且稳定可靠”的 Agent 体验需求极为迫切，这正成为决定项目能否从“实验室玩具”走向“生产就绪”的核心分水岭。

#### 2. 各项目活跃度对比

| 项目名称 | 今日 Issue 更新数 | 今日 PR 更新数 | 版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 1000 (423新开/活跃) | 1000 (416待合并) | 无 | **危机修复期** - 极度活跃但因大量P1 Bug陷入被动响应，稳定性问题突出。 |
| **Hermes Agent** | 500 | 500 | 无 | **攻坚迭代期** - 高活跃度，积极修复性能与配置隔离问题，社区反馈良好。 |
| **OpenHands SDK** | 25 | 50 | v1.39.0 | **稳步增强期** - 活跃度适中，版本发布节奏稳健，重点在安全、CI和MCP治理。 |
| **Pi** | 75 | 23 | v0.83.0 | **快速演进期** - 活跃度高，兼顾功能开发与跨平台兼容性修复，响应迅速。 |
| **LiteLLM** | 70 | 236 | 无 | **核心功能巩固期** - PR数量巨大，聚焦MCP集成和成本计算等关键功能修复与增强。 |
| **Temporal** | 1 | 39 | 无 | **稳定增强期** - 社区互动冷清，但内部开发推进扎实，聚焦SAA、负载均衡等底层能力。 |

#### 3. OpenClaw 在生态中的定位

- **优势与定位**：OpenClaw 在其生态中是 **体量最大、社区最活跃的“旗舰”项目**。其内部涌现的 Bug（如会话丢失、进程泄漏）和功能请求（如记忆信任标记、动态模型发现），往往代表着整个行业面临的前沿挑战。它是生态中“压力最大”的探路者，问题解决的路径对其他项目有重要参考价值。
- **技术路线差异**：与 **Hermes Agent** 注重性能优化和配置隔离不同，OpenClaw 面临的核心问题是 **大规模部署下的系统韧性**（如 OOM 崩溃循环、网关死锁）。与 **LiteLLM** 相比，后者专注做“模型路由网关”，而 OpenClaw 则是试图构建包含记忆、工具、会话管理的“全能型 Agent 框架”，其复杂度远高于单一网关。
- **社区规模对比**：从 Issue/PR 数量级（1000条）来看，OpenClaw 的社区活跃度是其他项目的 2-10 倍。这说明其用户基数和贡献者数量巨大，但也意味着维护压力空前，当前正处于“规模扩大”到“质量巩固”的阵痛期。

#### 4. 共同关注的技术方向

1.  **安全性增强 (Memory/Agent Safety)**
    - **涉及项目**：OpenClaw, OpenHands SDK, Hermes Agent
    - **具体诉求**：社区提出“记忆信任标记”(OpenClaw #7707) 以防范记忆投毒；请求“MCP 工具首次调用审批”(Hermes #16462)；以及“OWASP Agent Memory Guard”(OpenHands #4251)。这表明随着 Agent 权限和能力的增强，**安全从可选变成必备**。

2.  **MCP (Model Context Protocol) 集成与治理**
    - **涉及项目**：LiteLLM, OpenHands SDK, OpenClaw
    - **具体诉求**：LiteLLM 在一天内提交多个 PR 增强 MCP 的权限控制、参数扫描；OpenHands SDK 合并了 `MCPServer.enabled` 开关（PR #4307）；OpenClaw 关注 MCP 回环重连问题 (#98435)。**MCP 正在成为 Agent 工具和模型交互的“标准化”层**，各项目都在抢占这一生态位。

3.  **跨平台与终端兼容性**
    - **涉及项目**：Hermes Agent, Pi, OpenHands SDK
    - **具体诉求**：Hermes Agent 修复了 Windows 下 `search_files` 静默失败 (#63177)；Pi 修复了 WSL 路径处理错误 (#7064) 和 Wayland 下的剪贴板粘贴 (#7248)。**对非主流环境（Windows, WSL, Wayland）的支持，正成为项目走向大众市场必须补足的短板**。

4.  **成本可观测性与控制**
    - **涉及项目**：LiteLLM, Hermes Agent
    - **具体诉求**：LiteLLM 用户反复抱怨流式响应成本丢失 (#16021) 和提示缓存成本计算错误 (#27191)；Hermes Agent 报告 Preflight Token 估算严重不准 (#73298)。**精细化成本管控是 Agent 从个人玩具走向企业级应用的关键**。

#### 5. 差异化定位分析

| 项目 | 核心功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | 全能型 Agent 框架 (会话、记忆、工具) | 追求高度自定义的 Agent 开发者和重度用户 | 模块化、插件化、强调系统韧性，但当前稳定性是最大挑战。 |
| **Hermes Agent** | 高性能、多配置、安全隔离的 Agent | 需要多环境/多 profile 隔离的专业用户和团队 | 强调性能优化（如只读配置加载）和配置隔离（`multiplex_profiles`），几乎是一个“多 Agent 管理系统”。 |
| **OpenHands SDK** | 面向企业的 Agent 开发与治理 SDK | 希望构建安全、可控、可审计 Agent 产品的开发者 | 提供 `MCPServer` 开关等治理原语，强调结构化输出和策略守卫，更像一个“企业级 Agent 构建工具包”。 |
| **Pi** | 终端用户体验优化的个人 Agent | 追求极致终端交互体验的个人用户 | 专注于 TUI/CLI 的细节打磨（如 Sixel 图像、Wayland 剪贴板），类似一个“高级终端 Agent 客户端”。 |
| **LiteLLM** | 模型路由、成本与安全网关 | 需要统一管理多个 LLM 提供商的企业和开发者 | 核心是“代理/网关”，负责请求转发、成本计算和访问控制，是 Agent 的“网络基础设施”组成部分。 |
| **Temporal** | 分布式工作流引擎 | 构建高可靠性、长时间运行 Agent 应用的开发者 | 定位为 Agent 的“底层基础设施”，负责工作流的编排、状态管理、重试和恢复，与上层 Agent 逻辑解耦。 |

#### 6. 社区热度与成熟度

- **第一梯队（快速迭代与质量巩固期）**：
    - **OpenClaw & Hermes Agent**: 处于绝对的 **活跃中心**，日更新量级极大。但两者阶段不同：**OpenClaw** 更像是“被动修复阶段”，社区热度由大量 Bug 驱动；**Hermes Agent** 则是“主动优化阶段”，社区在性能和安全方面有更多建设性讨论。两者都面临从“功能驱动”向“质量驱动”转型的压力。
- **第二梯队（快速功能演进期）**：
    - **Pi & LiteLLM**: 处于 **高速功能开发期**。**Pi** 版本发布频繁，聚焦于终端体验和跨平台修复，社区反馈积极。**LiteLLM** 则在一个版本周期内积累了海量 PR，专注于 MCP 等新功能的集成与 Bug 修复，显示出强大的工程交付能力。
- **第三梯队（稳定增强与工具定位期）**：
    - **OpenHands SDK & Temporal**: 社区互动相对冷清，但技术演进预期明确。**OpenHands SDK** 作为企业级 SDK，其社区更偏专业用户。**Temporal** 作为基础设施，其开发模式更偏向内部计划驱动，社区主要关注稳定性和长期路线图。

#### 7. 值得关注的趋势信号

1.  **稳定性成为核心壁垒**：从 OpenClaw 的“崩溃循环”到 Hermes Agent 的“配置不生效”，再到 LiteLLM 的“字符污染”，大量高优先级 Bug 都指向 **系统可靠性**。这警示开发者，在功能竞赛之外，**谁能先解决“用了不出错”的问题，谁就能赢得市场信任**。
2.  **“安全性”从后知后觉变为主动设计**：多个项目同时提出“记忆投毒”、“MCP 首次审批”等概念，表明社区意识正在觉醒。**未来的 Agent 将不再是“黑盒”，而必须是一个“可解释、可审计、可控”的实体**。这对涉及到代码执行、文件访问、财务操作的 Agent 应用尤其关键。
3.  **跨平台兼容性是扩大用户基数的关键**：Pi 对 WSL 和 Wayland 的修复，Hermes Agent 对 Windows 的修复，都指向一个趋势——**Agent 开发者的主流环境是多样的，终端用户的环境更是碎片化的**。忽视兼容性，将限制项目的受众和影响力。
4.  **成本量化与管理迫在眉睫**：LiteLLM 社区的呼声表明，**成本不再是事后统计，而是实时、精准的运营指标**。对于企业用户，成本控制是部署 Agent 的决定性因素之一。
5.  **MCP 正在成为 Agent 生态的“HTTP”**：从 LiteLLM 到 OpenHands SDK 再到 OpenClaw，几乎所有主流项目都在围绕 MCP 进行集成。**投资于 MCP 生态的工具、库和基础设施，将是未来构建 Agent 应用的“正确”选择**。

**对开发者的建议**：在选择技术栈时，应审慎评估各项目的“稳定性信号”。如果追求快速原型，Hermes Agent 或 Pi 可能比 OpenClaw 更“开箱即用”；如果构建企业级应用，OpenHands SDK 和 Temporal 的治理与可靠性设计值得投入；而 LiteLLM 则几乎是任何需要统一管理模型成本与安全的中大型 Agent 应用的必备组件。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我已根据您提供的 Hermes Agent 项目数据，为您生成 2026-07-30 的项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026-07-30

## 1. 今日速览

今日项目活跃度极高，过去 24 小时内收到并处理了 500 条 Issues 和 500 条 PR，社区参与度和开发节奏均处于高水平。尽管无新版本发布，但项目核心聚焦于性能优化、稳定性修复和安全性增强。值得关注的是，大量与多配置文件隔离、会话状态持久化、以及特定平台（Windows、macOS）相关的 Bug 被集中报告和修复，这表明项目在扩展用户基数的同时，正面临着复杂环境下的兼容性挑战。与此同时，社区对新功能（如多后端终端、Turn-level 时间上下文）的呼声依然强烈，显示出项目在核心能力扩展上的巨大潜力。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日合并/关闭了 158 个 PR，项目在性能、稳定性和功能完整性方面持续迈进。以下为今日推进的关键进展：

- **性能与架构优化**：
    - **[PR #73094]**：修复了 `hermes -w` 命令因网络不稳定导致卡顿 30-60 秒的问题。通过跳过冗余的 `git fetch` 并设置超时回退机制，显著提升了命令响应速度。[查看详情](https://github.com/NousResearch/hermes-agent/pull/73094)
    - **[PR #74322]**：在 16 个 `agent/` 模块的 29 个只读配置调用点中，用 `load_config_readonly()` 替换了 `load_config()`，将所有只读操作的性能提升了 28 倍（从 332µs 降至 12µs）。这是对先前 PR #56085 和 #57096 的重新整合和修复构建。[查看详情](https://github.com/NousResearch/hermes-agent/pull/74322)
    - **[PR #57096]** 和 **[PR #56085]**：分别修复了配置归一化函数的副作用问题，并为多个模块引入了只读配置加载器，为上述性能优化奠定了安全基础。[PR #57096](https://github.com/NousResearch/hermes-agent/pull/57096) | [PR #56085](https://github.com/NousResearch/hermes-agent/pull/56085)

- **API 与插件生态**：
    - **[PR #70931]**：修复了 API 服务器与原生网关在 Agent 运行时解析上的三个关键分歧，包括：会话模型现在能在聊天轮次中被正确应用、模型解析失败时能优雅恢复而非报 400 错误、以及 Provider 认证失败时能返回可处理的错误响应。[查看详情](https://github.com/NousResearch/hermes-agent/pull/70931)
    - **[PR #74413]**：为桌面端插件 SDK 增加了 `ctx.download` 功能，使插件能够向用户提供文件下载，进一步完善了插件的文件处理能力。[查看详情](https://github.com/NousResearch/hermes-agent/pull/74413)
    - **[PR #74407]**：完成了对 Buzz Desktop 模型选择器的 ACP 文档记录，明确了其菜单来源及 ID 映射规则，有助于用户理解和使用该功能。[查看详情](https://github.com/NousResearch/hermes-agent/pull/74407)

- **安装与配置修复**：
    - **[PR #74409]** 和 **[PR #74414]**：针对 #74373 问题，修复了在安装和更新过程中，`distribution_owned` 配置清单允许列表被忽略的 Bug，确保分发包的文件权限得到正确执行。[PR #74409](https://github.com/NousResearch/hermes-agent/pull/74409) | [PR #74414](https://github.com/NousResearch/hermes-agent/pull/74414)

## 4. 社区热点

以下 Issue 和 PR 成为今日讨论的焦点，反映了社区的核心关切：

- **[Issue #10421] Turn-level live time context for current date/time awareness**：获得 15 条评论和 9 个👍。社区普遍反映 Agent 缺乏对“当前时刻”的感知，导致其在需要时间敏感信息的任务中表现不佳。这并非功能缺失，而是对代理智能程度的根本要求。[查看详情](https://github.com/NousResearch/hermes-agent/issues/10421)
- **[Issue #16462] feat(security): Add first-invoke approval for MCP server tools**：获得 12 条评论。该请求涉及 MCP 工具的安全管控，要求增加首次调用时的用户审批步骤。这反映了社区对 Agent 调用外部工具安全性的高度关注，避免模型在无授权情况下执行敏感操作。[查看详情](https://github.com/NousResearch/hermes-agent/issues/16462)
- **[Issue #29849] `no_agent=True` cronjob script execution ignores `terminal.backend`**：获得 10 条评论。该 Bug 导致设置为远程后端的定时任务脚本仍在本地执行，严重影响了远程工作流的可靠性。此问题直接关联到 CI/CD 和自动化部署场景的稳定性。[查看详情](https://github.com/NousResearch/hermes-agent/issues/29849)
- **[Issue #73298] Preflight token estimate counts reasoning_details envelope at chars/4**：获得 8 条评论。此 Bug 导致在 thinking 模型上，预检 Token 估算极不准确，自动压缩逻辑在真实使用量仅达阈值约 27% 时就会被错误触发。这对高端模型的计费和性能影响重大，是今日最受关注的性能 Bug 之一。[查看详情](https://github.com/NousResearch/hermes-agent/issues/73298)

## 5. Bug 与稳定性

今日报告了大量 Bug，多集中在配置隔离、会话状态和平台兼容性上。按严重程度排列如下：

- **P1 级 (重点)**
    - **[Issue #73298]**：Preflight Token 估算在 thinking 模型上严重不准（压缩过早触发）。讨论热烈，暂无直接修复 PR。[查看详情](https://github.com/NousResearch/hermes-agent/issues/73298)
    - **[Issue #60197]**：调用 `/exit` 时，MCP 服务器任务出现 `RuntimeError: Event loop is closed`。该 Issue 已被关闭，相关修复已在合并的 PR 中体现。[查看详情](https://github.com/NousResearch/hermes-agent/issues/60197)
    - **[Issue #72348]**：Discord 适配器的允许/拒绝通道列表是进程全局的，破坏了 `multiplex_profiles` 下的隔离性。这是一个严重的安全边界问题。[查看详情](https://github.com/NousResearch/hermes-agent/issues/72348)

- **P2 级 (重要)**
    - **[Issue #29849]**：`no_agent=True` 的 cron 任务忽略远程 `terminal.backend` 配置。暂无直接修复 PR。[查看详情](https://github.com/NousResearch/hermes-agent/issues/29849)
    - **[Issue #42961]**：`terminal.cwd` 配置对本地后端无效。暂无修复 PR。[查看详情](https://github.com/NousResearch/hermes-agent/issues/42961)
    - **[Issue #63177]**：在 Windows 上，`search_files` 在传入绝对路径时由于 `rg` + `MSYS_NO_PATHCONV` 冲突而静默返回 0 结果。暂无修复 PR。[查看详情](https://github.com/NousResearch/hermes-agent/issues/63177)
    - **[Issue #25402]**：切换 `terminal.backend` 为 local 后，残留的 Docker 配置仍会导致 Docker 被使用。暂无修复 PR。[查看详情](https://github.com/NousResearch/hermes-agent/issues/25402)
    - **[Issue #67605]**：桌面端/仪表盘的配置文件切换是部分生效的（MCP 工具不加载，环境变量解析错误）。暂无修复 PR。[查看详情](https://github.com/NousResearch/hermes-agent/issues/67605)
    - **[Issue #71744]**：`browser_console` eval 的快路径可能在错误的浏览器/标签页中执行。暂无修复 PR。[查看详情](https://github.com/NousResearch/hermes-agent/issues/71744)

- **P3 级 (一般)**
    - **[Issue #59877]**：在 Python 3.14.6 上安装失败，约束条件 `<3.14` 过于严格。暂无修复 PR。[查看详情](https://github.com/NousResearch/hermes-agent/issues/59877)
    - **[Issue #68545]**：macOS virtiofs 文件系统导致 `state.db` 损坏。虽有 `checkpoint_fullfsync` 但未在 Linux 容器内生效。暂无修复 PR。[查看详情](https://github.com/NousResearch/hermes-agent/issues/68545)

## 6. 功能请求与路线图信号

社区提出的新功能需求主要为改善 Agent 的智能感知、扩展性和生态系统集成。

- **核心智能与上下文**：
    - **Turn-level 实时时间感知 ([Issue #10421](https://github.com/NousResearch/hermes-agent/issues/10421))**：呼声最高。社区希望 Agent 能像人类一样理解“现在”是何时，而不是依赖工具调用。这可能是改善 Agent 基础能力的重要方向。
    - **多后端终端支持 ([Issue #1855](https://github.com/NousResearch/hermes-agent/issues/1855))**：允许同时使用本地和多个远程终端。该请求获得 11 个👍，并与今日合并的 **[PR #64190](https://github.com/NousResearch/hermes-agent/pull/64190) (Tenki 云沙箱后端)** 形成协同，表明项目正致力于终端后端的多样化和灵活组合。

- **安全与权限**：
    - **MCP 工具首次调用审批 ([Issue #16462](https://github.com/NousResearch/hermes-agent/issues/16462))**：社区对安全性的关注度极高。此功能请求很可能被优先考虑，以增强用户对 Agent 行为的控制感。

- **扩展性与平台支持**：
    - **Xiaomi MiMo V2 TTS 支持 ([Issue #8830](https://github.com/NousResearch/hermes-agent/issues/8830))**：针对中文高质量 TTS 的需求，显示了社区对母语和非英语支持的兴趣，是项目国际化发展的重要信号。
    - **Ant Ling Provider ([Issue #70085](https://github.com/NousResearch/hermes-agent/issues/70085))**：增加新的 AI 模型提供商，体现了社区对模型源多样化的需求。

## 7. 用户反馈摘要

从今日的 Issues 评论中，可以提炼出以下用户反馈和痛点：

- **配置不生效与隔离性问题（严重不满）**：用户对“配置文件设置被静默忽略”感到失望。多个 Bug（`terminal.cwd`, `terminal.backend` 切换，profile 切换不完整）表明配置系统在复杂场景下的可靠性存在问题，特别是在多 profile、多后端环境下。`Issue #67605` 的用户直言“选择 profile 并不会真正给你那个 profile”。
- **会话状态丢失（核心痛点）**：用户抱怨 Agent 在会话重启后丢失项目上下文，甚至错误地认为自己在做另一个项目 (`Issue #27013`)。这表明状态持久化和跨会话记忆是当前用户体验的一个明显短板。
- **工具行为不一致**：`search_files` 在 Windows 上静默失败 (`Issue #63177`) 和 `browser_console` 在错误标签页执行 (`Issue #71744`) 的 Bug，让用户对工具的可信赖度产生怀疑。这些 Bug 往往难以排查，严重损害用户体验。
- **对安全性的高度期待**：用户提出了 `first-invoke approval for MCP` 这类前瞻性安全需求，显示了社区不仅关注功能，更关注安全边界和用户授权，尤其是在 Agent 能够调用外部工具并执行代码的背景下。
- **对性能优化表示认可**：虽然 Bug 报告多，但针对 `hermes -w` 卡顿问题的快速修复 (`PR #73094`) 和大幅度的配置读取性能优化 (`PR #74322`) 也体现了项目团队对用户体验的积极回应。

## 8. 待处理积压

以下为长期未响应的、可能被忽视的重要 Issue 或 PR，需提醒维护者关注：

- **[Issue #25402] terminal.backend=local can still use Docker**：此 Bug 从 5 月 14 日创建至今已持续两个半月，且与配置切换这个核心操作相关，严重影响用户体验。应被提升优先级并分配资源处理。[查看详情](https://github.com/NousResearch/hermes-agent/issues/25402)
- **[Issue #1855] feat(terminal): Multi-backend terminal**：这是一个备受期待的功能请求（11个👍）。鉴于项目已开始添加新的终端后端（Tenki），规划一个统一的、支持多后端的终端架构似乎是符合路线图的下一步。应明确是否将其纳入下一阶段开发计划。[查看详情](https://github.com/NousResearch/hermes-agent/issues/1855)
- **[Issue #418] Feature: Pokémon Play History Dashboard**：尽管是一个游戏相关功能，但获得了 6 条评论且长期活跃。该 Issue 提出的 Web GUI 监控和回放功能，实际上可以抽象为一种通用的 Agent 活动监控面板，对项目调试和功能演示有潜在价值，值得社区讨论其通用化可能性。[查看详情](https://github.com/NousResearch/hermes-agent/issues/418)

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-07-30

## 今日速览
过去 24 小时项目保持高度活跃：共处理 25 条 Issue（新开/活跃 22 条，关闭 3 条）和 50 个 PR（待合并 46 个，合并/关闭 4 个），并发布 v1.39.0 版本。安全加固、CI 稳定性与 MCP 治理是今日社区讨论的核心主题，同时多项长期积压的 Bug 与功能提案获得实质性进展。整体健康度良好，但需关注并发控制、事件序列化容错等回归风险。

## 版本发布

### v1.39.0
- **主要内容**：
  - CI：移除集成和工作流示例中无人监管的 nightly 调度（PR #4291）
  - 修复（LLM）：泛化模型能力解析逻辑，提高对不同模型配置的兼容性（PR #4200）
  - 测试：补充相关测试用例
- **破坏性变更**：无明确标记，无迁移指南。
- **建议**：若使用自定义 LLM 配置，建议验证模型能力检测是否仍符合预期。

## 项目进展 — 今日合并/关闭的 PR
以下 4 个 PR 已被合并或关闭，代表具体的功能推进或修复：

| PR | 标题 | 状态 | 作用 |
|----|------|------|------|
| [#4280](https://github.com/OpenHands/software-agent-sdk/pull/4280) | fix(security): stop logging runtime command contents | 已合并 | 安全：停止记录运行时命令内容，防止敏感信息泄露 |
| [#4305](https://github.com/OpenHands/software-agent-sdk/pull/4305) | fix(ci): bind release smoke container port | 已合并 | CI：修复发布冒烟测试的容器端口绑定，确保流程正确 |
| [#4307](https://github.com/OpenHands/software-agent-sdk/pull/4307) | feat: add MCPServer.enabled to switch a server off without removing it | 已合并 | 功能：新增 `MCPServer.enabled` 字段，允许临时关闭 MCP 服务器而无需删除配置 |
| [#3951](https://github.com/OpenHands/software-agent-sdk/pull/3951) | Rotate integration test tracker issue | 已关闭 | 运维：轮换集成测试结果跟踪 Issue，解决单一 Issue 过大无法加载的问题 |

这些合并在安全审计、CI 可靠性、MCP 配置灵活性等方面向前迈进了关键一步。

## 社区热点
今日讨论热度最高的 Issues：

1. **[#1787] Proposal: Fork conversation when tools change**（评论 23 条，已关闭）  
   - 提议在工具变更时 fork 对话而非修改系统提示，以保持事件日志不可变。虽已关闭但社区讨论深入，涉及事件模型设计哲学。

2. **[#4251] Security: OWASP Agent Memory Guard integration**（评论 21 条）  
   - 用户提出集成 OWASP 内存防护以抵御记忆投毒攻击，反映部署方对自主 Agent 安全性的迫切需求。目前标记为 needs-triage。

3. **[#4019] ACP profiles inject workspace project skills that duplicate**（评论 13 条）  
   - bug 报告：ACP 配置文件中项目技能被重复注入，导致行为异常，影响使用 ACP 协议的 CLI 用户。

4. **[#4249] Support passing reasoning_content back to API for DeepSeek V4**（评论 11 条）  
   - 功能请求：要求 SDK 传递 DeepSeek V4 “思考模式”返回的 `reasoning_content` 字段，提升推理透明度。

5. **[#4063] max_concurrent_runs does not limit native async conversations**（评论 10 条）  
   - Bug：文档声明的并发限制配置对原生异步对话无效，导致实际并发可无限增长，可能引发资源耗尽。

## Bug 与稳定性
按严重程度排列今日报告的 Bug：

| 严重性 | Issue | 描述 | 状态 | 是否有 Fix PR |
|--------|-------|------|------|---------------|
| **严重** | [#4080](https://github.com/OpenHands/software-agent-sdk/issues/4080) | 单个未注册事件类型导致整个对话加载失败，静默丢失 | OPEN, needs-triage | 无 |
| **严重** | [#3992](https://github.com/OpenHands/software-agent-sdk/issues/3992) | 无工具调用的内容响应被不对称处理，弱模型/本地模型驱动的 Agent 提前终止 | OPEN, needs-triage | 无 |
| **较高** | [#4157](https://github.com/OpenHands/software-agent-sdk/issues/4157) | LLMSecurityAnalyzer 信任模型自评风险等级，低风险动作绕过人工确认 | OPEN, needs-triage | 无 |
| **较高** | [#4063](https://github.com/OpenHands/software-agent-sdk/issues/4063) | max_concurrent_runs 对原生异步对话无效 | OPEN, needs-triage | 无 |
| **中等** | [#4208](https://github.com/OpenHands/software-agent-sdk/issues/4208) (已关闭) | `.pr/` 目录泄漏到 main，fork PR 的 CI 工作流因 403 硬失败 | CLOSED | 已由 PR #4290 等修复？实际上 issue 描述包含两个问题，尚未有明确 fix PR 关闭 |
| **中等** | [#4093](https://github.com/OpenHands/software-agent-sdk/issues/4093) | ACP 0.11 移除 Gemini 模型状态字段，导致会话设置失败 | OPEN, needs-triage | 无 |
| **低** | [#3746](https://github.com/OpenHands/software-agent-sdk/issues/3746) | max_input_tokens 在 headless CLI 模式不生效 | Stale | 无 |
| **低** | [#3753](https://github.com/OpenHands/software-agent-sdk/issues/3753) | browser-use 0.11.9 分离 iframe 导致整个 DOM 提取失败 | OPEN | 无 |

此外，PR [#4282](https://github.com/OpenHands/software-agent-sdk/pull/4282) 报告了 VSCode URL 端点未验证工作区目录的安全漏洞（中等），仍为 OPEN 状态。

## 功能请求与路线图信号
今日接收的新功能请求及可能纳入下一版本的信号：

- **治理与安全**  
  - [#4251](https://github.com/OpenHands/software-agent-sdk/issues/4251) OWASP Agent Memory Guard（记忆投毒防御）  
  - [#4273](https://github.com/OpenHands/software-agent-sdk/issues/4273) 企业级治理层：文件访问控制、命令白名单、成本预算、审计证据  
  - [#2854](https://github.com/OpenHands/software-agent-sdk/issues/2854) OPA 策略守卫（Stale 但仍有讨论）

- **LLM 兼容性**  
  - [#4249](https://github.com/OpenHands/software-agent-sdk/issues/4249) DeepSeek V4 reasoning_content 透传  
  - [#4064](https://github.com/OpenHands/software-agent-sdk/issues/4064) run-scoped LLM 额外请求头  
  - PR [#4150](https://github.com/OpenHands/software-agent-sdk/pull/4150) 添加 Kimi Code 模型支持（待合并）

- **技能与执行模型**  
  - [#2053](https://github.com/OpenHands/software-agent-sdk/issues/2053) Skills Epic：子 Agent 执行、模型路由、隔离  
  - PR [#4207](https://github.com/OpenHands/software-agent-sdk/pull/4207) 结构化输出（基于 #2566，待合并）  
  - PR [#4160](https://github.com/OpenHands/software-agent-sdk/pull/4160) prompt-based evaluation（待合并）

- **MCP 治理**  
  - PR [#4307](https://github.com/OpenHands/software-agent-sdk/pull/4307) 已合并：MCPServer.enabled 开关  
  - Issue [#4293](https://github.com/OpenHands/software-agent-sdk/issues/4293)（已关闭）要求原子化的 MCP 创建/修改/删除端点（已通过 PR 实现？需确认）

以上功能中，DeepSeek 兼容、MCP 开关、结构化输出优先级较高，可能在 v1.40.0 中出现。

## 用户反馈摘要
从 Issue 评论中提炼的真实用户痛点：

- **弱模型体验差**（#3992）：使用本地/较弱 LLM 时，Agent 经常因无工具调用而被终止，使这类模型几乎不可用。用户 @Rkaplounov 建议对称处理内容响应。
- **动态切换 Agent 失败**（#4158）：调用 `switch_profile` 后状态文件更新但会话仍使用旧 Agent，导致配置漂移。
- **凭证旋转失效**（#4170）：在顺序 ACP 会话中，Codex 凭证旋转后无法传播到新会话，需手动干预。
- **超时重置**（#4032）：Agent Server 重启后 LLM 超时配置丢失，迫使每次重启后重新设置。
- **浏览器 DOM 提取失败**（#3753）：browser-use 库分离 iframe（广告/小部件）导致整个页面分析崩溃。
- **安全性担忧**：多位用户（#4157、#4251、#4273）表达了对 Agent 自评估安全风险的信任问题，要求更多外部策略机制。
- **CI 稳定性**（#4208、#4304）：依赖未锁定导致的 CI 红绿反转让贡献者困扰，@simonrosenberg 发起了整体审计。

## 待处理积压
以下重要 Issue/PR 长期未得到维护者关注或合并，需优先处理：

| 类型 | 编号 | 标题 | 创建时间 | 最后更新 | 备注 |
|------|------|------|----------|----------|------|
| PR | [#1160](https://github.com/OpenHands/software-agent-sdk/pull/1160) | Add VNC token-based authentication | 2025-11-13 | 2026-07-29 | 未合并，安全改进 |
| PR | [#1399](https://github.com/OpenHands/software-agent-sdk/pull/1399) | Python package-based plugin loading | 2025-12-15 | 2026-07-29 | 早期 POC，可能被替代 |
| Issue | [#2854](https://github.com/OpenHands/software-agent-sdk/issues/2854) | OPA-based policy guard | 2026-04-02 | 2026-07-29 | Stale 标签，缺少进展 |
| Issue | [#3046](https://github.com/OpenHands/software-agent-sdk/issues/3046) | Enforce AgentSkills spec properties at runtime | 2026-05-03 | 2026-07-29 | Stale，无关联 PR |
| Issue | [#3746](https://github.com/OpenHands/software-agent-sdk/issues/3746) | max_input_tokens in headless CLI not effective | 2026-06-16 | 2026-07-29 | Stale，低优先级但在影响用户 |
| Issue | [#4308](https://github.com/OpenHands/software-agent-sdk/issues/4308) | Discussion: how to prevent loose CI dependencies | 2026-07-29 | 2026-07-29 | 刚开，但值得立即决策 |

建议维护者针对上述积压项进行 triage，合并或关闭陈旧 PR，对 Stale 标记的 Issue 重新评估优先级。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目日报 | 2026-07-30

---

## 1. 今日速览

过去24小时项目保持极高活跃度：共处理75条Issue（新开/活跃13条，关闭62条）和23个PR（待合并6个，已合并/关闭17个），并发布了v0.83.0版本。核心团队在修复和功能开发上均衡发力，社区贡献积极，尤其针对WSL、Wayland、OpenAI兼容性等跨平台问题进行了多项针对性修复。整体项目健康度良好，但积压的长期未响应用户需求仍需关注。

---

## 2. 版本发布

### v0.83.0
- **新增功能**：
  - **凭据导出**：新增 `pi auth print-api-key` 和 `pi auth print-bearer-token` 命令，允许外部客户端获取已配置的凭据，并支持自动OAuth刷新和最小有效期强制检查。
  - **无头OpenRouter登录**：支持通过SSH完成 `/login` 流程，用户只需粘贴重定向链接即可完成认证。
- **破坏性变更**：本次发布未注明明显破坏性变更，但凭据导出命令可能影响已集成自动化脚本的认证流程，需确认是否引入新的环境变量或配置文件字段。
- **迁移注意事项**：若使用OpenRouter作为主力提供商，建议更新至v0.83.0以体验无头登录；使用外部客户端调用Pi API的用户应优先升级。

---

## 3. 项目进展

今日合并/关闭的重要PR体现了多个关键领域的推进：

| PR | 标题 | 说明 |
|----|------|------|
| #7288 | fix(ai): preserve function arguments with empty custom payloads | 修复OpenAI兼容提供商发送空custom对象时函数参数被丢弃的问题，由社区贡献者@sunnyyoung提供补丁。 |
| #7122 | fix(tools): correct byte count, false limit warning, surrogate pairs | 三项工具层修复：write工具UTF-8字节计数、find工具错误限制警告、truncateLine代理对处理。 |
| #7272 | preserve providers raw stop reason | 添加 `AssistantMessage.rawStopReason` 保留提供商原始停止原因，改进Mistral等模型错误报告。 |
| #7266 | fix(coding-agent): show system prompt files in startup context | 交互式启动时正确显示文件背书的SYSTEM.md和APPEND_SYSTEM.md条目。 |
| #7245 | feat(tui): inline images under tmux via sixel | 为tmux环境添加sixel后端支持，解除此前tmux下图像显示的完全禁用。 |
| #7261 | fix(coding-agent): read clipboard via wl-paste on Wayland | 解决Wayland下Ctrl+V粘贴失效问题，采用wl-paste/xclip/xsel多途径方案。 |
| #7258 | fix(coding-agent): enable streaming usage for llama.cpp | 让llama.cpp提供商支持流式token使用量统计，修复会话统计显示0 token的bug。 |
| #7243 | fix(ai): update TypeBox nullable array validation | 升级TypeBox至1.3.7，修复nullable数组模式验证错误，但可能带来弃用API的微小破坏。 |

此外，多个长期悬挂的PR（如#7022 WIP，#6216 Bedrock Mantle）仍在等待进一步评审，但整体进展积极。

---

## 4. 社区热点

以下为过去24小时讨论最活跃的Issue/PR（基于评论数）：

- **#7064** [OPEN] [bug] WSL absolute windows paths are mishandled（9条评论）  
  [链接](https://github.com/earendil-works/pi/issues/7064)  
  用户反馈在WSL2环境下，`read`/`write`/`edit`工具因路径处理错误频繁回退到全量写入。该问题吸引了大量WSL用户关注，目前尚无修复PR，社区期待官方方案。

- **#6951** [CLOSED] qwen3.8-max-preview reasoning effort配置不符（8条评论）  
  [链接](https://github.com/earendil-works/pi/issues/6951)  
  用户指出Qwen官方推荐的是`low/medium/xhigh`而非Pi默认的`minimal/low/medium/high`，已在讨论中被标记为已关闭，但未说明是否已修复。

- **#1871** [CLOSED] 并行启动锁争用导致误导性认证错误（7条评论）  
  [链接](https://github.com/earendil-works/pi/issues/1871)  
  这是一个自3月起的长期议题，在多个进程并发启动时锁文件争用会报“No API key found”误导信息。虽然已关闭，但社区仍在讨论最佳实践。

- **#3432** [CLOSED] 请求可自定义read工具的行数和字节限制（6条评论）  
  [链接](https://github.com/earendil-works/pi/issues/3432)  
  用户希望将默认读取限制改为可配置值，并允许limit参数超过最大行数。该需求获得支持，但尚未看到对应PR。

---

## 5. Bug 与稳定性

按严重程度排列今日报告的关键Bug：

| 严重度 | Issue | 问题描述 | 是否有Fix PR |
|--------|-------|----------|-------------|
| **严重** | #7064 | WSL绝对Windows路径被错误处理，导致读写工具反复失败 | 无 |
| **严重** | #7035 | 大规模grep操作间歇性崩溃（Slackware环境） | 无 |
| **高** | #7130 | Kitty终端中退格键删除两个字符（Kitty协议释放事件未过滤） | 无 |
| **高** | #7248 | Wayland下Ctrl+V粘贴无响应（readClipboardText仅支持X11） | ✅ #7261 已合并 |
| **中** | #7253 | `/compact`在上下文窗口达到90%时触发两次，陷入无限循环 | 无 |
| **中** | #7179 | `autocompleteMaxVisible`重启后重置为默认值 | 无 |
| **中** | #7187 | 包解析时因未捕获的异常导致静默崩溃，影响所有聊天会话 | 无 |
| **低** | #7232 | TUI中折行超链接打开截断的URL | 无 |
| **低** | #7255 | Google Vertex丢失Gemini的finishReason，统一报“未知错误” | ✅ #7272 已合并 |

值得注意：多个Bug已有对应修复PR并在当日合并，如#7248 (Wayland粘贴)、#7255 (Vertex finishReason)、#7160 (空custom参数) 等，表明团队响应迅速。

---

## 6. 功能请求与路线图信号

今日涌现的明确功能需求：

- **#7199** [inprogress] 支持Kimi K3 on Fireworks（5条评论）  
  用户请求增加Kimi K3模型支持，已有关联PR？未直接匹配，但社区活跃。
- **#7010** [OPEN] 标准化OpenAI兼容提供商的可选对象工具Schema（5条评论）  
  修复工具JSON Schema中未规范化`required`字段的问题，提升兼容性。
- **#5329** [OPEN] 暴露Pi等待用户输入的状态给主机集成（3条评论，👍5）  
  需求来自cmux集成场景，希望区分“运行中”与“等待用户输入”，获得较高点赞，表明外部集成开发者关注此功能。
- **#7264** [CLOSED] 支持LaTeX数学渲染（3条评论）  
  用户期望Markdown组件解析`$$...$$`和`$...$`，该PR/Issue已被标记为“untriaged”后关闭，但可能进入后续迭代。
- **#7237** [CLOSED] 限制bash输出存档并容忍临时存储失败（3条评论）  
  要求改进bash工具的完整输出归档行为，避免因临时存储失败终止会话。
- **#7163** [OPEN] 基于SQLite的搜索索引（PR）  
  社区贡献了`SessionRepo.search()`的SQLite FTS5实现，初始版本仍全量加载，但为后续优化奠基。

路线图信号：v0.83.0的凭据导出和无头登录表明项目正强化企业级集成能力；工具层修复（字节计数、剪贴板）则注重底层准确性。长期看，搜索索引和可配置工具限制是社区呼声较高的方向。

---

## 7. 用户反馈摘要

从今日Issues评论中提炼的核心用户声音：

- **WSL用户**（#7064）：“agent无法正常使用read/write工具，不得不回退到命令行全量写入，体验极差。” 该问题影响了大量WSL2环境用户，优先级应提高。
- **OpenRouter用户**（#6951）：“Qwen官方文档明确说只有low/medium/xhigh，Pi的默认映射不对。” 虽然已关闭，但用户可能期望官方确认修复或提供配置覆盖。
- **大规模操作用户**（#7035）：“broad grep导致瞬间崩溃，没有任何错误日志。” 用户环境为Slackware，需进一步复现。
- **Wayland用户**（#7248）：“Ctrl+V粘贴完全没反应，原来是因为clipboard-rs只处理X11。” 该修复（#7261）获得用户感谢。
- **并行启动开发者**（#1871）：“pi-subagents并发时锁争用报错极具误导性，新手会以为API key没配置。” 建议增加更友好的错误提示。
- **/compact行为**（#7253）：“手动compact后自动触发第二次，而且死循环，只能按Esc取消。” 用户对上下文管理的稳定性期待较高。

整体用户满意度中等偏上，修复速度值得肯定，但WSL路径等基础问题存在时间较长。

---

## 8. 待处理积压

以下为长期未响应或评估中的关键条目，建议维护者优先关注：

| 类型 | 编号 | 标题 | 创建时间 | 最后更新 | 备注 |
|------|------|------|----------|----------|------|
| Issue | #5329 | 暴露Pi等待用户输入的状态 | 2026-06-02 | 2026-07-29 | 获得5个👍，无assignee，无PR |
| Issue | #7130 | Kitty终端退格键删除两个字符 | 2026-07-26 | 2026-07-29 | 影响特定终端，修复难度可能较低 |
| Issue | #7064 | WSL绝对路径处理不当 | 2026-07-24 | 2026-07-29 | 严重影响WSL用户，社区关注度高 |
| Issue | #7035 | 大量grep间歇性崩溃 | 2026-07-23 | 2026-07-29 | 稳定性和数据安全性问题 |
| PR | #6216 | 添加Amazon Bedrock Mantle OpenAI Responses提供商 | 2026-07-01 | 2026-07-29 | 长期等待review，集成价值高（AWS用户） |
| PR | #7163 | 基于SQLite的搜索索引 | 2026-07-27 | 2026-07-29 | 社区贡献，需要设计讨论 |
| PR | #7022 | WIP: 保护响应期间的树导航 | 2026-07-23 | 2026-07-29 | 状态为WIP但需明确是否继续 |

---

*数据来源：GitHub (earendil-works/pi)，统计截至2026-07-29 23:59 UTC。*

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

好的，作为您的 AI 智能体与个人 AI 助手领域开源项目分析师，我已根据您提供的 LiteLLM GitHub 数据，为您生成了 2026-07-30 的项目动态日报。

---

### **LiteLLM 项目日报 | 2026-07-30**

#### **1. 今日速览**

今日项目活跃度极高，共产生 70 条 Issue 更新和 236 条 PR 更新，但无新版本发布。开发团队在 Bug 修复和功能增强方面均投入了大量精力，尤其是在 **MCP (Model Context Protocol)** 集成、**Rust 原生桥接** 和 **成本计算** 方面有显著进展。值得关注的是，社区反馈的 **流式响应成本丢失**、**多请求内容污染** 等关键 Bug 正在被积极处理。项目整体处于高速迭代状态，工程团队响应迅速，社区参与度活跃。

#### **2. 版本发布**
*（今日无新版本发布）*

#### **3. 项目进展**

今日项目在多个模块取得了实质性进展，共有 57 个 PR 被合并或关闭，主要推进了以下领域：

- **MCP (Model Context Protocol) 集成增强**：团队今日提交了多个关键 PR，显著提升了 MCP 的安全性和功能性。
    - `#35149`: 修复了 Bedrock Guardrail 在 MCP 工具调用 (`during_mcp_call`) 模式下未生效的问题。
    - `#35142`: 实现了对 MCP 工具调用参数的扫描和脱敏，增强了数据安全。
    - `#35146`: 新增了基于用户的 MCP 工具调用权限控制。
    - `#35147`: 实现了从用户存储的 SSO 断言中获取 ID-JAG 认证信息。
    - 这些 PR 表明 LiteLLM 正将 MCP 作为核心能力进行深度打磨，补全了其安全策略、审计和权限控制。

- **Rust 原生桥接推进**：`#35046` 提交了为 Rust 原生桥接和 Axum 主机添加提供者调试日志的功能，以提高对后端调用的可观测性，预示着 Rust 化改造正在稳步进行。

- **核心功能修复与成本计算修正**：
    - `#35114`: 修复了流式 `/v1/messages` 接口的成本计算不准确问题，特别是针对提示缓存 (prompt caching) 场景。
    - `#35144`: 修复了 Claude 4.6 模型在 `/v1/messages` 中忽略 `thinking.budget_tokens` 参数的问题。

#### **4. 社区热点**

今日社区讨论最热烈的问题集中在 **流式响应成本计算** 和 **QPS/并发限制** 上：

- **#16021 [Bug]: OpenRouter 成本信息在流式响应中丢失**
  - **链接**: [Issue #16021](https://github.com/BerriAI/litellm/issues/16021)
  - **热度**: 评论 17 | 👍 4
  - **分析**: 用户指出在使用 OpenRouter 进行流式（streaming）调用时，响应中丢失了 `usage.cost` 字段，而非流式模式则正常。这表明成本计算与流式传输的解码逻辑之间存在脱节。此问题与今日修复的 `#35114` PR 高度相关，表明社区最关心的痛点之一正在被解决。

- **#16011 [Bug]: 最大并行请求 (Max Parallel Requests) 限制不一致**
  - **链接**: [Issue #16011](https://github.com/BerriAI/litellm/issues/16011)
  - **热度**: 评论 11 (已关闭)
  - **分析**: 用户报告了 API Key 级别的“最大并行请求”限制未能有效执行，导致大量并发请求涌入后端。此 Bug 直接关系到代理的稳定性和资源控制能力，目前已关闭，暗示可能已有相关修复。

- **#35023 [Bug]: CJK 字符在多并发请求中交叉污染**
  - **链接**: [Issue #35023](https://github.com/BerriAI/litellm/issues/35023)
  - **热度**: 评论 5 (已关闭)
  - **分析**: 当推理型模型通过 LiteLLM 网关流式输出时，不同请求间的中文等 CJK 字符会发生“串流”污染。这是一个非常严重的稳定性和数据正确性 Bug，已在 `v1.93.0` 和 `v1.94.0` 中确认存在。该 Issue 今日被关闭，推测已有热修复版本或 PR 来应对此问题。

#### **5. Bug 与稳定性**

今日报告的 Bug 数量较多，按严重程度排列如下：

- **数据污染（严重）**:
    - `#35023` **[已关闭]**: CJK 字符跨请求污染流式响应。严重性：**危急**。直接影响输出结果的正确性。**今日已关闭，推测已有修复。**

- **核心功能故障（高）**:
    - `#35124` & `#35126` **[新开/已关闭]**: 流式 `/v1/messages` 路由到 `openai/` 后端时，不会触发日志回调（`litellm_logging_obj`）。这会破坏所有依赖于日志的审计、监控和成本追踪系统。**新开 Issue 和后一个疑似重复的 Issue 均在今日创建，后者被标记为“潜在重复”和“已关闭”，说明团队已迅速识别并可能正在处理。**
    - `#33167` **[开放]**: `v1.92.0` 版本启动时尝试下载 Prisma 二进制文件。对于需要离线或严格网络策略的环境，这是个严重问题，可能导致服务无法启动。目前已有 PR `#35139` 解决了 FastAPI 版本兼容性崩溃问题，但未直接关联此 Issue。

- **功能异常（中）**:
    - `#34105` **[开放]**: Bedrock Converse 对非 Anthropic/Nova2 模型（如 Qwen3）静默丢弃 `reasoning_effort` 参数。
    - `#27191` **[开放]**: 自定义定价下，提示缓存令牌（prompt-cache tokens）的成本计算和追踪有 Bug。
    - `#24640` **[已关闭]**: 图片生成端点忽略了 `response_format` 参数。

#### **6. 功能请求与路线图信号**

基于今日提交的 PR 和 Issue，以下功能请求很可能被纳入下一版本：

- **Cloudflare Workers AI 扩展**:
    - `#21115` **[开放]**: 社区请求同步更新 Cloudflare Workers AI 提供者，以支持其最新 API 中的图像和音频生成模型。
    - `#35056` & `#35055` **[新开]**: 同一个用户（@prdai）今日提交了两个 Feature Request，分别要求添加 **音频** 和 **图像** 支持。这表明 Cloudflare 提供者的扩展是下阶段明确的功能方向。

- **Tag 路由增强**:
    - `#35097` **[新开]**: 提出了“必需-AND” (`required-AND`) 的 tag 路由功能，允许用户要求模型必须匹配**所有**指定的 tag。这对于需要精细化路由策略的用户来说是一个重要的增强。

#### **7. 用户反馈摘要**

- **痛点**:
    - **成本可观测性不足**: 多位用户反复提及成本信息在流式响应中丢失（#16021），或在特定场景下计算不准确（#27191），这是影响用户信任的核心问题。
    - **升级维护困难**: 用户（#23941）反馈在 LiteLLM 版本升级时，尤其在 Prisma 数据库迁移方面，缺少清晰的文档和指引，导致升级过程痛苦。
    - **配置与文档不符**: 用户（#35064）反馈在 UI 中找不到 `background_health_checks` 选项，暗示可能存在文档与实现的不一致。

- **使用场景**:
    - **高并发代理**: 多个 Bug（如 #16011, #35023）和 Feature Request（如 #35097）均来自需要承载大量并发的用户，他们强调了对稳定、安全、高效的网关（Proxy）的强需求。
    - **多云/多模型管理**: 用户（#21115, #25668, #25372）寻求对特定云平台（Cloudflare, Vertex AI, Azure Foundry）新模型和新功能的支持，体现了企业级用户对统一管理和接入更多模型的需求。

#### **8. 待处理积压**

以下为长时间未关闭或未获得优先级，但值得关注的 Issue：

- **#23348 [MCP 集成问题]** ([链接](https://github.com/BerriAI/litellm/issues/23348)): 提出了 MCP 工具注册表查找、OpenAPI 路径回退等多个集成问题。鉴于团队今日在 MCP 上投入巨大，此 Issue 应得到高度重视。
- **#23941 [升级指南需求]** ([链接](https://github.com/BerriAI/litellm/issues/23941)): 用户对版本升级（特别是数据库迁移）的困惑长期存在。提供一个详细的升级指南将极大改善开发者体验。
- **#26774 [UI 无法更新预算]** ([链接](https://github.com/BerriAI/litellm/issues/26774)): 用户报告在 UI 管理面板中无法更新虚拟密钥的预算，这是一个影响运营功能的 Bug。

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目日报 — 2026-07-30

## 1. 今日速览
过去 24 小时项目保持高活跃度，共更新 39 条 PR（其中 11 条已合并/关闭），但仅有 1 条 Issue 更新（已关闭）。开发重心集中在 **Standalone Activity (SAA) 修复与对齐**、**CHASM 增强**、**客户端负载均衡优化** 以及 **基础设施稳定性改进**（如 gRPC 连接缓存、健康检查聚合）。社区反馈较少，唯一活跃 Issue 为长期关注的 PostgreSQL 索引膨胀问题已关闭。整体来看，项目健康度良好，核心功能迭代加速，社区互动偏冷但技术推进扎实。

## 2. 版本发布（无）

## 3. 项目进展
今日合并/关闭的 11 条 PR 中，以下 5 条最为关键（其余多为测试或文档更新），推动了 SAA 能力对齐、版本工作流稳定性及测试覆盖：

| PR | 标题 | 状态 | 要点 |
|----|------|------|------|
| [#11199](https://github.com/temporalio/temporal/pull/11199) | activity-parity: allow SAA to be manually completed by ID | 已合并 | 允许通过 `RespondActivityTaskCompletedById` 在 `Scheduled` 状态下强制完成 SAA，补齐与普通活动行为的一致性。 |
| [#11339](https://github.com/temporalio/temporal/pull/11339) | Disable standalone activity on-conflict request ID attachment | 已合并 | 拒绝使用 `attach_request_id=true` 的独立活动启动，保留仅链路模式的附加，暂时跳过相关功能测试，为后续原子性更新做准备。 |
| [#9966](https://github.com/temporalio/temporal/pull/9966) | fix: allow version workflow CaN when history grows too large, despite pending signals | 已合并 | 修复版本工作流在历史过大（≥4MB 或 ≥4K 事件）时无法继续作为新实例的问题，即使有挂起信号也能安全执行。 |
| [#9219](https://github.com/temporalio/temporal/pull/9219) | Test unsetting current or ramping version with `AllowNoPollers=true` | 已合并 | 新增功能测试，覆盖之前未测试的场景。 |
| [#10469](https://github.com/temporalio/temporal/pull/10469) | test MaxDeployments error is exposed correctly | 已合并 | 为 `MaxDeployments` 错误暴露测试分配独立命名空间，确保错误正确返回。 |

此外，Issue [#10145](https://github.com/temporalio/temporal/issues/10145)（PostgreSQL 索引膨胀）被关闭，标志着该长期稳定性问题得到解决或已给出止损方案。

## 4. 社区热点
今日无高评论量或高赞的 PR/Issue。唯一活跃的 Issue [#10145](https://github.com/temporalio/temporal/issues/10145) 获得 2 个 👍 和 6 条评论，讨论高吞吐量工作流下 PostgreSQL 数据库持续膨胀（即使设置了保留期）。该问题最终于今日关闭，推测已通过近期变更或配置建议修复。社区对此关注点集中在**存储成本与保留策略的有效性**，反映出用户对大规模生产部署下的长期数据管理有强烈需求。

## 5. Bug 与稳定性
- **严重**：PR [#11325](https://github.com/temporalio/temporal/pull/11325) 修复 SAA 终端超时未链接前置失败的 Bug，导致 SDK 用户只能看到超时而丢失真正原因。已提交修复（待合并）。
- **中等**：PR [#11344](https://github.com/temporalio/temporal/pull/11344) 修复独立活动重试去重逻辑，防止延迟重试在活动已关闭后错误处理。已提交修复（待合并）。
- **低**：Issue [#10145](https://github.com/temporalio/temporal/issues/10145) 已关闭，索引膨胀问题得到处理。
- **性能优化**：PR [#11290](https://github.com/temporalio/temporal/pull/11290) 将已到期的任务直接放入立即队列而非定时队列，避免不必要的延迟。

## 6. 功能请求与路线图信号
以下开放 PR 反映出下一阶段的重要功能方向，有望进入下一个版本：

- **客户端负载均衡**：[#10955](https://github.com/temporalio/temporal/pull/10955) 引入 backlog-aware 的 add-task 负载均衡，根据分区积压量偏置新任务，提升大规模写入稳定性。
- **gRPC 连接缓存**：[#11341](https://github.com/temporalio/temporal/pull/11341) 缓存前端内部 gRPC 连接，减少重复拨号开销，对齐已有 HTTP 客户端行为。
- **健康检查标准化**：[#11343](https://github.com/temporalio/temporal/pull/11343) 集中化健康检查逻辑，基于延迟分位数和错误率作为指标，可用于多个端点。
- **可见性增强**：[#10998](https://github.com/temporalio/temporal/pull/10998) 新增 `TemporalPriorityKey` 和 `TemporalFairnessKey` 预定义搜索属性；[#11346](https://github.com/temporalio/temporal/pull/11346) 增加 `wf_reported_problems_set/cleared` 计数器指标，便于用户监控。
- **任务队列管理**：[#11347](https://github.com/temporalio/temporal/pull/11347) 允许在达到任务队列家族上限时仍可注册新的队列类型（同名不同类型），提升版本部署灵活性。
- **SAA 指标对齐**：[#11328](https://github.com/temporalio/temporal/pull/11328) 补全 SAA 的 payload-size、heartbeat-count 等指标，消除与 WFA 的差异。
- **时间跳跃优化**：[#11223](https://github.com/temporalio/temporal/pull/11223) 实现时间跳跃完成轮询 API，提升测试与重放场景效率。

## 7. 用户反馈摘要
来自 Issue [#10145](https://github.com/temporalio/temporal/issues/10145) 的用户反馈：
> 在高吞吐量（数十万工作流/小时）环境下，PostgreSQL 数据库持续增长，即使设置了保留期也无效。实际表大小仅 46...（数据截断）。用户期望数据库大小与表大小保持相近。

该反馈反映了用户对**存储资源使用效率**的担忧，尤其是在长时间运行、高并发的生产集群中，后台数据清理或索引回收机制可能未按预期工作。该问题已关闭，建议关注后续相关变更或配置文档更新。

## 8. 待处理积压
- **[#8975](https://github.com/temporalio/temporal/pull/8975)** — [stale] Link to sections in docs tree  
  创建于 2026-01-08，已标记为 stale，至今未合并。该 PR 仅为文档 README 增加内部链接，风险低但长期搁置。建议维护者尽快处理或关闭。

- **[#10955](https://github.com/temporalio/temporal/pull/10955)** — Backlog-aware client add-task load balancing  
  创建于 2026-07-07，已存在近一个月，仍处于 review 状态。该 PR 涉及复杂负载均衡逻辑，可能需更多评审时间，但建议优先推进以避免 blocking 其他依赖 PR。

- **[#10998](https://github.com/temporalio/temporal/pull/10998)** — Add TemporalPriorityKey and TemporalFairnessKey to Visibility Schema  
  创建于 2026-07-09，同样已停留三周。该功能对用户定制可见性体验很有价值，可考虑加速合并。

- **[#11223](https://github.com/temporalio/temporal/pull/11223)** — add poll time-skipping ff completion  
  创建于 2026-07-22，一周未更新，涉及新轮询 API，需持续推动。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*