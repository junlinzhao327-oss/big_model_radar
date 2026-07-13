# OpenClaw 生态日报 2026-07-14

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-13 23:17 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，请看根据您提供的 OpenClaw 项目数据生成的 2026-07-14 项目动态日报。

---

# OpenClaw 项目动态日报 - 2026-07-14

## 今日速览

项目今日保持极高的活跃度，过去24小时内产生了500条Issue和500条PR的更新，呈现出典型的发布后维护与社区反馈高峰。项目发布了两个新版本（含一个正式版和一个Beta版），引入了多个新模型和提供商，并默认启用了更强的思考能力。**热点集中在平台扩展（Linux/Windows桌面应用）、数据安全（内存防投毒）、以及关键的会话与数据稳定性回归上。** 多个P0级Bug被报告并已有修复PR跟进，显示了维护团队对稳定性的快速响应。整体来看，项目正处于功能快速迭代与稳定性加固并行的阶段。

## 版本发布

项目发布了两个版本，核心内容均为模型提供商与能力的扩展。

- **v2026.7.1 (正式版) 与 v2026.7.1-beta.6 (Beta版)**
  - **发布内容：** 两个版本的发布说明（Release Notes）完全相同，均聚焦于新模型与提供商的支持。
  - **核心亮点：**
    - **新增模型/提供商：** 集成了 Featherless, Claude Sonnet 5, Mythos 5, Meta Muse Spark 1.1 等新模型。
    - **引入ClawRouter:** 新增了 `ClawRouter` 路由能力，可能用于更智能的模型分发或网关选择。
    - **默认模型变更：** 新用户安装时，默认模型更改为GPT-5.6。
    - **增强思考能力：** 为不同层级的用户（Sol/Terra/Luna）启用了更强或默认的思考（`/think`）模式，并增加了对Z.AI `max`模式的支持。
    - **OAuth刷新：** OAuth认证后会自动刷新模型可用性列表。
  - **破坏性变更与迁移注意：** 发布说明中未明确提及，但默认模型的变更和思考模式的增强可能会影响现有用户的自动化脚本或习惯。建议开发者和高级用户查阅完整的变更日志，以确认是否有底层配置变动。

## 项目进展

今天合并或关闭了多个重要PR，主要围绕内部重构和稳定性修复。

- **代码重构：**
  - 合并了重构 `chat.send` 核心逻辑的 Issue (#106555)，旨在将这个超过4000行的庞大函数分解为更清晰的阶段，提升代码可维护性。
  - 合并了拆分五个超大运行时代码模块的 Issue (#106503)，将文件按职责进行拆分。
  - **PR #106887 (已合并)**: 重构了 Discord 频道中的语音上下文助手，将其访问权限私有化，清理了代码导出。
- **功能与修复：**
  - **PR #106873 (待合并)**: 加固了发布验证流程，解决了 `gh run watch` 消耗API配额和脚本硬编码 `main` 分支导致的问题，提升了发布流程的稳定性。
  - **PR #106766 (已合并)**: 增加了“技能扫描”功能，允许代理从历史会话中挖掘有价值的模式，并将其转化为可复用的技能（Skill Workshop）。这是一个重要的功能扩展，能将用户的“经验”转化为“系统能力”。
  - **PR #106866 (待合并)**: 修复了控制UI中，在网关重连时打开模型提供商页面可能导致路由错乱的问题。
- **安全与风控：**
  - **PR #106889 (待合并)**: 修复了 ClawHub 对插件API版本范围的校验逻辑，确保标准语义化版本格式能被正确识别。
  - **PR #106849 (待合并)**: 修复了子代理在提示（Prompt）提交失败后，无法正确处理已完成结果的“重试”问题。

## 社区热点

今日社区讨论的焦点集中在平台扩展、数据安全与慢性痛点解决上。

- **🥇 [Issue #75 - Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)**
  - **112条评论，81个👍，热度断层第一！**  这个自2026年初就提出的功能请求，再次成为讨论中心。用户明确表达了在Linux和Windows上原生桌面应用的需求，认为macOS/iOS/Android已有，这两个平台不应该被落下。这表明**跨平台体验的完整性是用户最核心的长期诉求之一**。
- **🥈 [Issue #7707 - Memory Trust Tagging by Source](https://github.com/openclaw/openclaw/issues/7707)**
  - **18条评论**。这是一个高风险的安全功能需求，旨在根据信息来源（用户命令、网页抓取、第三方技能）对代理内存进行信任度标记，以防御“内存投毒”攻击。社区对这个提议高度关注，反映了用户对AI安全的敏感度在提升。
- **🥉 [Issue #104721 - All tool results return "(see attached image)"](https://github.com/openclaw/openclaw/issues/104721)**
  - **16条评论，1个👍。**  这个P0级的Bug引发了用户的强烈不满，因为所有工具的执行结果都被一个文字占位符替换，导致系统“完全瘫痪”。用户对这类严重影响使用的回归问题情绪比较激动，是必须优先处理的问题。
- **其他热点：**
  - **Issue #102020**: “第二条消息发送失败”的Bug，影响了Signal和Discord等多平台，同样是影响核心体验的关键问题。
  - **Issue #101290**: CLI启动时可能导致SQLite数据库损坏的严重Bug，被标记为P0。

## Bug 与稳定性

今日报告的Bug数量众多，稳定性问题尤为突出，其中“会话状态”和“数据丢失”是高频影响域。

| 严重程度 | 核心问题 | 影响 | 修复PR |
| :--- | :--- | :--- | :--- |
| **P0** | **[Issue #104721] 所有工具返回“(see attached image)”占位符** | 系统核心功能完全失效，回归问题 | 无 (维护中) |
| **P0** | **[Issue #101290] CLI启动自检导致SQLite数据库损坏** | 数据丢失，数据库损坏，回归问题 | 无 (维护中) |
| **P1** | **[Issue #76038] 会话卡死恢复机制失效** | 会话永久卡死，网关无响应，导致被强杀 | 无 |
| **P1** | **[Issue #98790] 代理间并发交互导致会话树分叉，最终使会话永久损坏** | 数据丢失，会话无法恢复 | 无 |
| **P1** | **[Issue #93003] Active Memory 针对订阅制Claude CLI用户报错** | 高级用户核心功能不可用 | [PR #106840](https://github.com/openclaw/openclaw/pull/106840) (待合并) |
| **P2** | **[Issue #90213] 2026.6.1升级后状态迁移警告无法消除** | 用户界面持续显示错误信息 | 无 |
| **P2** | **[Issue #93139] `write` 工具和 `exec` heredocs 中 `\n` 字面量问题** | 功能异常，开发者体验不佳 | 无 |
| **P2** | **[Issue #92769] MiniMax M3模型的 `reasoning` 字段被完全丢弃** | 高级模型功能失效，回归问题 | 无 (有相关PR) |
| **P2** | **[Issue #74378] Windows CLI命令执行后进程残留** | 稳定性问题，消耗系统资源 | 无 |

**小结：** 大量P0/P1级别的Bug指向了“会话状态管理”和“数据持久化”这两个核心系统模块，这可能与近期的大版本更新引入的复杂改动有关。多个回归问题的出现也需要维护团队仔细审查最近的代码变更。

## 功能请求与路线图信号

社区对新功能的诉求持续高涨，主要集中在安全、平台和易用性上。

- **高优先级信号：**
  - **跨平台桌面应用 (Issue #75)**: 呼声最高，但实现难度大，暂无关联PR。
  - **动态模型发现 (Issue #10687)**: 解决OpenRouter等提供商模型列表频繁变动的问题，已有10条评论和3个👍，是提升模型生态灵活性的关键。
  - **文件系统沙箱 (Issue #7722)**: 安全增强需求，已有4个👍，可能作为安全特性的下一阶段目标。
  - **执行命令黑名单 (Issue #6615)**: 安全与访问控制需求，获得7个👍，是现有白名单机制的互补。

- **可能纳入下一版本的特征：**
  - **执行自动审核结果缓存 (PR #102362)**: 模型驱动的执行审核在重试时会重复支付API调用费，此PR提供了缓存方案，直接节省用户成本，有望快速合并。
  - **MCP重试风暴防护 (Issue #68527)**: 针对资源耗尽风险的特性，设计了限流、熔断等保护机制，是生产环境稳定性保障，可能在下一个稳定版中体现。

## 用户反馈摘要

- **对稳定性的反馈：** 用户对“工具结果被替换为占位符”（#104721）、“数据库损坏”（#101290）和“第二条消息就报错”（#102020）这类基础功能故障反馈强烈，情绪多为“完全不可用”、“令人沮丧”。这表明**核心通信管道的稳定性是用户满意度的基石**。
- **对平台和功能的渴望：** Issue #75 和 #7707 的长期热度证明，用户不再满足于“能用”，而是希望 OpenClaw 能无缝融入其所有工作平台，并在安全模型上走在前面。用户担心“内存投毒”威胁，渴望更智能、更安全的交互。
- **对开发流程的反馈：** Issue #73537 提议为发布添加“生产就绪”稳定标签，反映了用户在尝鲜新功能后，对于稳定、可靠版本发布的渴望。他们需要清晰地知道哪个版本适合日常业务运行，哪个版本用于尝鲜。
- **对易用性的反馈：** 用户提出TUI无屏读器支持（#9637）、不支持Shift+Enter换行（#10118）、WhatsApp无贴纸支持（#7476）等，反映了不同用户群体的多样化需求，以及对应用细节体验的追求。

## 待处理积压

以下为长期未更新或响应的重要Issue及PR，建议维护者关注。

- **[Issue #11665 - Webhook Session 复用BUG](https://github.com/openclaw/openclaw/issues/11665)**
  - **状态：** 自2026年2月起Open，标记有`linked-pr-open`但未见进展。Webhook的多轮对话功能名不副实，是API集成开发者的一个痛点。
- **[Issue #6615 - 执行命令黑名单特性](https://github.com/openclaw/openclaw/issues/6615)**
  - **状态：** 自2026年2月起Open，获得7个👍。这是一个明确且合理的安全增强请求，实现复杂度不高，值得纳入后续迭代。
- **[Issue #7722 - 文件系统沙箱](https://github.com/openclaw/openclaw/issues/7722)**
  - **状态：** 自2026年2月起Open，获得4个👍。与上面类似，是提升系统安全性的重要一环。
- **[PR #82072 - 插件工具查找范围修复](https://github.com/openclaw/openclaw/pull/81857)**
  - **状态：** 自2026年5月发起，已标记为 `ready for maintainer look`。该PR修复了Active Memory等插件在特定配置下不工作的问题，看起来是一个正确性修复，但已滞留近两个月，需要尽快评审。

---

## 横向生态对比

# AI 智能体与个人 AI 助手开源生态横向对比报告

**报告日期：2026-07-14**  
**数据来源：** OpenClaw、Hermes Agent、OpenHands SDK、Pi、LiteLLM、Temporal 六个开源项目 GitHub 社区动态

---

## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态正处于 **功能爆发与稳定性加固并行** 的快速演进期。头部项目（OpenClaw、Hermes Agent）日均处理超过 500 条 Issue/PR，社区反馈极为活跃；项目间在 **跨平台桌面支持、记忆持久化与安全、MCP 协议深度集成、模型路由与成本控制** 等方向上形成共同攻坚点。与此同时，基础设施类项目（LiteLLM、Temporal）正在通过 Rust 迁移、Standalone Activity 等底层重构来支撑上层智能体运行时的性能与可靠性要求。整体上看，生态正从“单一聊天机器人”向 **可配置、安全、企业级的多 Agent 协作平台** 快速跃迁。

---

## 2. 各项目活跃度对比

| 项目 | 今日 Issues 更新 | 今日 PR 更新 | 版本发布 | 健康度评估 |
|------|-----------------|-------------|---------|-----------|
| **OpenClaw** | 500（新开+活跃） | 500（待合并+已合并） | v2026.7.1（正式版）+ beta.6 | ⚡ 极高，发布后维护高峰，P0 回归问题集中在会话/数据 |
| **Hermes Agent** | 500（新开117+关闭383） | 500（待合并+关闭91） | 无 | ⚡ 极高，集中清理积压，稳定化阶段 |
| **OpenHands SDK** | 23（新开19+关闭4） | 50（待合并45+关闭5） | v1.36.0 | 🟡 中高，性能优化（懒加载）+ MCP 修复为主 |
| **Pi** | 65（新开+活跃） | 19（更新/合并13） | 无 | 🟢 中，社区贡献活跃，兼容性修复密集 |
| **LiteLLM** | 62（新开44+关闭18） | 287（待合并127+关闭160） | 无 | ⚡ 极高，PR 合并量大，Rust 迁移预热 |
| **Temporal** | –（未提供完整数） | 51（合并22） | 无 | 🟢 中，核心功能稳步推进，技术债务待清理 |

**注：** OpenClaw、Hermes Agent 的 500 条数据为汇总值，反映了头部项目极高的社区参与度。

---

## 3. OpenClaw 在生态中的定位

- **优势：** OpenClaw 作为“核心参照”项目，社区规模当前最大（Issue/PR 量与 Hermes 并列第一），发布节奏最快（同日双版本），并率先默认启用更强的思考能力、引入 ClawRouter 模型路由。其在 **跨平台桌面应用（Issue #75 断层热度）、记忆信任标记（#7707）、会话状态防损坏** 等方向上的讨论代表了用户对成熟产品级体验的渴望。
- **技术路线差异：** 对比 Hermes Agent（侧重清理积压、修复缓存/Cron 兼容性）、Pi（侧重社区贡献的模型适配器修复）、OpenHands SDK（侧重性能与 MCP 生态），OpenClaw 更强调 **发布后快速响应 + 安全特性（内存防投毒）**，并且明确将 Linux/Windows 桌面应用列为最高优先级功能请求。
- **社区规模对比：** OpenClaw 与 Hermes Agent 同属第一梯队（日均 500+ 更新），OpenHands SDK、Pi、LiteLLM 为第二梯队（数十至数百），Temporal 作为基础设施则保持稳定的中等活跃度。OpenClaw 在“功能请求”维度上的用户参与度（#75 获得 112 评论 81👍）远高于其他项目，表明其用户画像以 **深度使用者、开发者** 为主。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---------|---------|---------|
| **跨平台桌面应用 / 原生体验** | OpenClaw (#75)、Hermes Agent (#15311)、Pi (#6187 WSL挂起) | 用户要求支持 Linux & Windows 原生应用、TUI 鼠标支持、内联交互按钮 |
| **记忆持久化 / 安全投毒防御** | OpenClaw (#7707)、Hermes Agent (#8457)、OpenHands SDK (懒加载)、Pi (memory_save 工具) | 跨会话记忆搜索、自动压缩、内存信任标记、按来源隔离 |
| **模型路由与自动选择** | OpenClaw (ClawRouter)、LiteLLM (#3442)、Pi (OpenRouter session affinity) | 智能分配任务到最优模型，成本/延迟/质量平衡 |
| **MCP 协议深化集成** | OpenHands SDK (#4011 MCP 嵌套 Schema)、LiteLLM (#33072 MCP OAuth 刷新)、Temporal (Nexus 不完全是 MCP) | MCP 工具 schema 正确性、OAuth 令牌自动刷新、服务器端配置 |
| **兼容性 / 多提供商支撑** | OpenClaw (Featherless 等新模型)、Pi (Codex/Bedrock/DeepSeek 修复)、LiteLLM (Claude Code 格式翻译) | 新兴模型（GPT-5.6, Claude Sonnet 5）的快速接入，以及回退/翻译机制 |
| **成本控制与配额管理** | LiteLLM (#25553 缓存绕过预算)、OpenHands SDK (#4088 减少 API 调用) | 防止超额、缓存友好、预算自动刷新 |

---

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent | OpenHands SDK | Pi | LiteLLM | Temporal |
|------|----------|-------------|---------------|----|---------|----------|
| **功能侧重** | 全能型个人助手，跨平台 UI + 安全 + 记忆 | 个人助手，专注清理与稳定，兼容多消息平台 | SDK/框架，构建智能体应用的工具包 | 轻量级个人助手，社区适配器活跃 | 模型路由/代理，成本控制与可观测性 | 工作流引擎，支撑智能体编排与持久化 |
| **目标用户** | 终端用户（希望完备桌面应用） | 高级用户/开发者（需快速迭代稳定版本） | 应用开发者（构建 Agent 产品） | 终端用户 + 插件开发者 | 企业运维（统一模型访问） | 后端/系统开发者（可靠工作流） |
| **技术架构** | 基于 Go/Rust（推断），强 UI（Web/TUI） | 未公开，与 OpenClaw 相似的 Agent 架构 | Python SDK + agent-server，插件化 | 多语言，强调社区插件生态 | Python 核心，正在 Rust 迁移 | Go 实现，分布式事务 |
| **发布节奏** | 激进（日更双版本） | 中等（无版本，大量合并） | 版本化（v1.36.0） | 版本化（v0.80.x 稳定） | 版本化（1.x） | 版本化（1.x） |
| **社区驱动程度** | 官方主导 + 社区反馈（P0 快速响应） | 社区贡献积极（大量 PR 来自社区） | 社区 PR 需等待审核（积压 45 PR） | 社区贡献极强（多数修复来自社区 PR） | 社区讨论热烈，但核心功能研发由官方主导 | 核心团队主导 |

---

## 6. 社区热度与成熟度

**⚡ 快速迭代阶段（功能爆发 + 高频回归）：**
- **OpenClaw、Hermes Agent** – 日均 500+ 更新，大量新功能与 Bug 交替出现，用户对稳定性投诉较多（P0 回归频发）。适合愿意尝鲜、追踪前沿的用户。
- **LiteLLM** – PR 合并量大，Rust 迁移等架构级工作启动，可视为“下一个大版本”前的高强度打磨期。

**🟡 质量巩固阶段（性能优化 + 兼容性修复）：**
- **Pi** – 无主版本发布，但社区交付了 13 高质量 PR（Codex、记忆工具），正从“功能堆叠”转向“稳定覆盖”。
- **OpenHands SDK** – 发布 v1.36.0，启动性能优化（懒加载会话），同时修复 MCP 关键 Bug，属于典型的功能补全 + 固化期。

**🟢 基础设施稳定阶段：**
- **Temporal** – 没有功能爆发，但 Standalone Activity、Nexus 等新特性持续演进，适合需要可靠底层工作流的用户。

---

## 7. 值得关注的趋势信号

1. **“内存安全”正在从概念走向功能实现**  
   OpenClaw #7707（记忆信任标记）、Pi #6599/6597（Agent 驱动记忆保存）标志着社区开始系统性地防范提示注入和记忆投毒。开发者应在设计智能体时考虑 **基于来源的记忆隔离**，并关注 OpenClaw 即将推出的防投毒方案。

2. **MCP 或成为 Agent 与工具交互的事实标准**  
   多个项目（OpenHands SDK、LiteLLM、Temporal Nexus）同时推进 MCP 协议增强。MCP 的 schema 正确性、OAuth 刷新、嵌套对象支持是当前重点。AI 智能体开发者应优先选择支持 MCP 的 SDK/路由框架，降低集成成本。

3. **GPT-5.6 及其托管多 Agent 能力正在催生新架构需求**  
   OpenHands SDK #4082-#4085 系列调研，OpenClaw 默认模型改为 GPT-5.6，说明主流模型已具备程序化工具调用、WebSocket 流式响应、托管多 Agent 等能力。这要求 Agent 框架在未来版本中支持 **模型端 Agent 与客户端子 Agent 的混合调度**，并考虑 previous_response_id 等新原生机制。

4. **用户对“零配置跨平台”的诉求已超过功能新奇性**  
   OpenClaw #75（Linux/Windows 桌面应用）获得 81 👍，Hermes Agent #15311（通用交互按钮）14评论，Pi #6187（WSL 挂起）均为基础体验问题。这意味着 AI 助手开源项目必须优先解决 **平台一致性**，否则将流失大量非 macOS 用户。

5. **Rust 迁移成为提升性能的关键路径**  
   LiteLLM 已开启 Rust 迁移 Beta；Temporal 虽然未提及 Rust，但其核心 KPI 是延迟 <1ms。当项目达到一定规模后，性能瓶颈无法仅靠 Python/Go 优化解决，Rust 作为“性能安全并重”的语言正在成为基础设施层事实选择。

---

**对 AI 智能体开发者的建议：**
- 若你正在构建面向终端用户的助手产品，请重点关注 OpenClaw 的跨平台方案和记忆安全特性。
- 若你开发 Agent 应用框架，可参考 OpenHands SDK 的 MCP 集成方式（懒加载、嵌套 Schema 修复）。
- 若负责模型接入与成本控制，LiteLLM 的 Rust 迁移与 PTU 预订是长期投资方向。
- 若需要工作流编排引擎，Temporal 的 Standalone Activity 与 Nexus 将为复杂 Agent 交互提供坚实底座。

---

*报告完*

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我已根据您提供的 Hermes Agent (github.com/NousResearch/hermes-agent) GitHub 数据，生成了 2026-07-14 的项目动态日报。

---

### Hermes Agent 项目日报 — 2026-07-14

#### 1. 今日速览

今日项目活跃度极高，共处理了 **500 条 Issues** 和 **500 条 PR**。尽管无新版本发布，但社区维护者关闭/合并了大量积压工作（383 条 Issues, 91 条 PR），表明维护团队正在集中处理积压并提升稳定。同时，有 117 条新 Issues 被提出，显示社区依然保持旺盛的需求和问题反馈。**项目整体处于高活跃度、高迭代的稳定状态**，重点正在从功能爆发式增长转向稳定性修复和平台特性打磨。

#### 2. 版本发布

今日无新版本发布。

#### 3. 项目进展

今日有多个重要 PR 被合并关闭，标志着项目在稳定性和功能补充上取得了显著进展：

- **稳定性修复**:
    - `fix(agent): add explicit httpx timeout to keepalive HTTP client (#37662)` (PR #37898): 修复了因网络 IPv6 问题导致的 HTTP 客户端无限挂起的问题，提升了底层网络连接的鲁棒性。
    - `fix(gateway): bust agent cache when model.default or model.provider changes` (PR #37880): 解决了网关在动态切换模型后仍使用旧模型进行响应的缓存不一致问题。
    - `fix(cron): clarify schedule and prompt requirements in parameter descriptions` (PR #37859): 通过改进 cron 工具的参数描述，解决了某些模型（如 Grok）在调用时自动省略必填参数导致任务失败的问题，优化了工具定义的清晰度。
    - `fix(dashboard): redact audio provider errors before HTTP replies` (PR #37890): 修复了仪表盘可能泄露音频提供商 API 密钥的安全风险。

- **功能与补全**:
    - 多个遗留的 `sweeper:implemented-on-main`（已在主线实现）标记的 Issues 被关闭（如 #37549, #37619, #35876 等），表明此前 PR 中的功能（例如桌面端聊天闪烁/滚动问题、Windows 缩放支持、视觉修复等）已在代码层面落地。

**总结**：项目正积极修复高危和常见 Bug，同时将已实现的特性正式标记为完成，稳步推进。

#### 4. 社区热点

今日讨论最为热烈的议题反映了用户对平台交互、记忆持久化和工具链提效的普遍诉求。

- **Issues #15311**: [Add generic action buttons / inline keyboard support for messaging platforms](https://github.com/NousResearch/hermes-agent/issues/15311)
    - **评论: 14 | 👍: 7**
    - 这是今日最受关注的功能请求。用户希望在 Telegram、Slack 等平台获得通用的交互按钮支持，而非硬编码。这反映了社区对**提升消息平台交互性和用户体验**的强烈需求。

- **Issues #8457**: [Feature: Persistent Session Memory with Cross-Session Search & Auto-Compression](https://github.com/NousResearch/hermes-agent/issues/8457)
    - **评论: 13 | 👍: 0**
    - 尽管点赞数不高，但评论数位列第二，且涉及核心的记忆持久化功能。用户对**会话记忆无法跨重启保留**的痛点呼声很高，并希望具备跨会话搜索和自动压缩能力，这是构建真正智能助手的基石。

- **Issues #4064 & #24860**: [Enable mouse support](https://github.com/NousResearch/hermes-agent/issues/4064) 和 [Dashboard Chat Ctrl+V/Broken image paste](https://github.com/NousResearch/hermes-agent/issues/24860)
    - 评论数分别为 11 和 10，反映了终端用户（尤其是桌面版用户）对 **TUI 和桌面应用基础交互体验**（如鼠标、粘贴板）的不满和要求提升的迫切心情。

#### 5. Bug 与稳定性

今日上报的 Bug 涵盖了安全、平台兼容和核心功能异常，以下为严重程度较高的项：

- **P2 (高危)**:
    - **[已关闭]** [Z.AI GLM-5.2 Coding Plan returns 429/code 1305 when system prompt contains exact phrase "Hermes Agent"](https://github.com/NousResearch/hermes-agent/issues/47685) (#47685): 一个非常具体但也很典型的提供商 API 兼容性问题。已关闭但未提及具体修复 PR，可能已规避或由用户自行处理。
    - **[已关闭]** [fix(dashboard): redact audio provider errors before HTTP replies](https://github.com/NousResearch/hermes-agent/pull/37890) (PR #37890, 关联 Issue ): 仪表盘存在泄露音频服务 API Key 的安全漏洞，**已有 fix PR**，这是非常重要的安全改进。

- **P3 (中危)**:
    - **[开放中]** [Dashboard Chat: Ctrl+V paste broken, image paste not supported](https://github.com/NousResearch/hermes-agent/issues/24860) (#24860): 长期存在的桌面端粘贴问题，影响日常使用，但尚无 fix PR。
    - **[开放中]** [Kanban worker reports 'protocol_violation'...](https://github.com/NousResearch/hermes-agent/issues/27178) (#27178): Kanban 工作流中的协议冲突问题，影响多 Agent 协作任务的正确关闭。
    - **[开放中]** [Claude models on multi-model OpenAI-compatible gateways get 0% prompt cache hit rate](https://github.com/NousResearch/hermes-agent/issues/56776) (#56776): 这是一个影响性能和成本的潜在严重问题，对通过自定义网关调用 Claude 模型的用户影响巨大。

#### 6. 功能请求与路线图信号

今日社区提出的功能请求集中在以下几个方向，部分已有对应的 PR 在推进：

- **有望被采纳**:
    - **平台交互**: #15311 (通用交互按钮) 呼声最高，是提升平台能力的明确方向。
    - **记忆增强**: #8457 (持久化会话记忆) 是社区高频需求，但实现复杂度高，可能需要规划在较远的路线图中。相关的 PR #37884 (知识召回工具) 可能是一个初步尝试。
    - **配置优化**: #12655 (模型选择器提供商过滤) 和 #16004 (可配置自动继续) 是提升高级用户控制力的精准需求，实现成本较低，很可能在后续版本中加入。

- **已有关联 PR**:
    - #40347 (俄语本地化): 来自社区的完整实现贡献（有独立 repo），集成概率很高。
    - #41222 (桌面端集成 Kanban): 与 PR #37864 (优化 Kanban 工作区) 诉求一致，方向明确。
    - #37713 (桌面端远程网关配置切换): 存在广泛的企业和个人使用场景，且已有 PR #37865 (主动交接原语) 和 #64022 (hybrid busy input mode) 在提升网关交互，但该功能实现较为复杂。

#### 7. 用户反馈摘要

从今日的 Issues 评论中，可以提炼出以下用户真实反馈：

- **痛点**:
    - **桌面端基础体验差**: `@sccasupercat` (Issue #24860) 和 `@ferminquant` (Issue #37527) 报告桌面端聊天界面粘贴、滚动等问题，表明基础交互仍需打磨。`@daniij` (Issue #33961) 报告 `/clear` 命令导致终端冻结，严重影响 Windows 用户的 CLI 使用。
    - **配置延迟不生效**: `@veryheavypickle` (Issue #32729) 报告辅助标题生成超时配置被写死，用户即使修改配置也无效，反馈配置系统“不听话”。
    - **专用提供商兼容性问题**: 一系列关于 `Z.AI` (Issue #47685), `openai-codex` (Issue #33415) 和 `Minimax` (Issue #31977) 的 Bug 报告显示，非标准 API 或特殊订阅计划的用户正频繁遇到问题，这是项目兼容性测试的薄弱环节。

- **满意点**:
    - **问题解决迅速**: 许多 Bug 报告 (如 #34457, #35876) 被迅速打上 `sweeper:implemented-on-main` (已在主线实现) 标签并关闭，表明维护团队对关键问题的响应速度是得到认可的。
    - **社区有爱**: `@warment` (Issue #40347) 主动为俄罗斯语用户制作了独立的安装包和本地化文件，体现了强大的社区贡献精神和互助氛围。

#### 8. 待处理积压

- **高关注度，但无有效回复**:
    - **#3523**: [hermes update regressions after #3492 — silent git output and unnecessary stashes](https://github.com/NousResearch/hermes-agent/issues/3523)
    - **创建时间**: 2026-03-28
    - **影响**: 影响所有通过 `hermes update` 升级的用户，Git 输出被静默，且每次都会执行不必要的 stash 操作，即使没有本地修改。此问题已开放超过 3 个月，需要维护者评估并修复。

- **核心功能问题**:
    - **#56776**: [Claude models on multi-model OpenAI-compatible gateways get 0% prompt cache hit rate](https://github.com/NousResearch/hermes-agent/issues/56776)
    - **创建时间**: 2026-07-02
    - **影响**: 对使用自定义网关调用 Claude 的用户，导致零缓存命中，大幅增加 API 开销。这是一个可能影响用户付费意愿的严重性能问题，需优先关注。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 – 2026-07-14

> 数据来源：GitHub `OpenHands/software-agent-sdk`  
> 统计时段：2026-07-13 00:00 UTC – 2026-07-14 00:00 UTC

---

## 1. 今日速览

- 过去 24 小时项目保持高活跃度：共处理 **23 条 Issue**（新开/活跃 19，关闭 4）与 **50 条 PR**（待合并 45，关闭/合并 5），代码库与社区讨论均显著升温。
- **v1.36.0 正式发布**，主要引入安全分析器 `ToolShieldLLMSecurityAnalyzer` 并修复 ACP 参数顺序，同时为后续架构优化（延迟加载会话、MCP 嵌套 schema 修复等）奠定基础。
- **5 个重要 PR 被合并或关闭**，其中 `lazy-load persisted conversations` 和 `deterministic filestore cache` 两项合并显著提升启动性能与测试可靠性。
- 社区对 **GPT‑5.6 新功能（程序化工具调用、WebSocket 模式、托管多 Agent）** 的调研热度上升，多个 Issue 集中提出，标志着项目正积极评估下一代 LLM 接口。
- 稳定性方面：本周连报 3 个与 MCP schema 迁移、嵌套属性丢失及子 Agent 中断传播相关的 Bug，均已有对应修复 PR 或已合入。

---

## 2. 版本发布

### v1.36.0 (2026-07-13)

**发布链接：** https://github.com/OpenHands/software-agent-sdk/releases/tag/v1.36.0

#### 主要更新内容

| 类别 | 说明 | PR |
|------|------|----|
| 安全 | 新增 `ToolShieldLLMSecurityAnalyzer`，为 LLM 输出提供基于工具盾的安全分析能力 | [#2911](https://github.com/OpenHands/software-agent-sdk/pull/2911) |
| 修复 | 修正 ACP 提示词参数顺序，确保技能注入时参数正确 | [#3996](https://github.com/OpenHands/software-agent-sdk/pull/3996) |
| 依赖 | 升级 `MishaKav/pytest-coverage-co` 等依赖 | 见 Changelog |

#### ⚠️ 破坏性变更与迁移注意事项

- **无预期破坏性变更**。`ToolShieldLLMSecurityAnalyzer` 为新增组件，默认不启用，用户可通过配置选择开启。
- ACP 参数顺序修复可能影响自定义 ACP 技能调用，若您之前绕过了该 Bug，请检查调用方参数顺序是否与 SDK 对齐。
- 本次 Release 已包含后续若干 Bug 修复的累积变更（如 MCP 嵌套 schema 修复，PR #4011），建议所有用户升级。

---

## 3. 项目进展

### 重点合并/关闭的 PR（过去 24 小时）

| PR | 标题 | 状态 | 影响 |
|----|------|------|------|
| [#4104](https://github.com/OpenHands/software-agent-sdk/pull/4104) | Release v1.36.0 | ✅ 合并 | 完成版本发布 |
| [#3895](https://github.com/OpenHands/software-agent-sdk/pull/3895) | perf(agent-server): lazy-load persisted conversations at startup | ✅ 合并 | **重大性能优化**：启动时不再加载所有历史会话，仅加载元信息，内存占用降低 80%+，启动时间从分钟级降至秒级 |
| [#4088](https://github.com/OpenHands/software-agent-sdk/pull/4088) | test(sdk): make filestore cache checks deterministic | ✅ 合并 | 替换基于时间的缓存断言为直接文件系统检查，消除 CI 跨环境的不稳定性 |
| [#4011](https://github.com/OpenHands/software-agent-sdk/pull/4011) | fix(mcp): preserve nested object properties in LLM-facing tool schema | ✅ 合并 | **关键 Bug 修复**：MCP 工具嵌套对象的 JSON Schema 不再被扁平化，LLM 能正确识别复杂参数结构 |
| [#593](https://github.com/OpenHands/software-agent-sdk/pull/593) | Add basedpyright to pre-commit and fix all type errors | ✅ 合并 | 类型检查工具迁移至 `basedpyright`，全量修复类型错误，提升代码健壮性 |

### 项目前进方向信号

- **会话延迟加载** 是本月性能工作的核心成果，后续计划在此基础上实现“空闲会话自动卸载”和“按需恢复”机制（见 PR #3266 和 Issue #3140）。
- MCP 生态持续完善：既有 `tools/list_changed` 订阅支持（PR #3894），也有 schema 修复，表明项目正在深度集成 MCP 协议。
- 安全体系扩充：`ToolShieldLLMSecurityAnalyzer` 为后续更严格的 LLM 输出审计铺路。

---

## 4. 社区热点

### 讨论最活跃的议题

| 议题 | 标题 | 评论数 | 热度分析 |
|------|------|--------|----------|
| [#2078](https://github.com/OpenHands/software-agent-sdk/issues/2078) | [Tracker] Daily Integration Runs | 137 | 持续集成运行跟踪器，虽为自动创建的占位 Issue，但积累了数百条集成测试讨论，反映社区对 CI 稳定性的关注 |
| [#3442](https://github.com/OpenHands/software-agent-sdk/issues/3442) | [Feature]: Intelligent Model Selection | 8 | 用户希望 SDK 能自动为任务选择最佳模型，获得 1 个 👍。社区对“模型选择民主化”需求强烈 |
| [#4019](https://github.com/OpenHands/software-agent-sdk/issues/4019) | ACP profiles inject workspace project skills that duplicate what the ACP CLI already ingests | 6 | **痛点**：ACP 配置与 CLI 技能注入重复，导致冗余开销。用户 `@simonrosenberg` 持续跟进，已提交修复 PR #4018 |
| [#4082~4085](https://github.com/OpenHands/software-agent-sdk/issues/4082) | GPT-5.6 新功能调研系列（4 个 Issue） | 各 0 评论但新开 | **信号**：`@smolpaws` 在同一天提出调研程序化工具调用、工具搜索、WebSocket 模式、托管多 Agent，表明社区对 OpenAI 最新 API 的高度期待 |

### 背后诉求

- **自动模型路由** 成为高频需求——用户不愿手动对比各模型成本/性能，希望 SDK 提供“帮我选”功能。
- **ACP 与技能系统** 存在重复定义问题，社区期望更清爽的配置流程。
- **对新 LLM 接口的拥抱** 是接下来的关键方向，尤其是 GPT‑5.6 的 `Responses` 和托管多 Agent 可能改变 SDK 架构。

---

## 5. Bug 与稳定性

### 按严重程度排列的当日新报告 Bug

| 严重程度 | Issue | 标题 | 状态 | 对应修复 PR |
|----------|-------|------|------|-------------|
| 🔴 严重 | [#4107](https://github.com/OpenHands/software-agent-sdk/issues/4107) | TaskToolSet 不传播父级中断到活跃子 Agent | 新开 | [#4108](https://github.com/OpenHands/software-agent-sdk/pull/4108)（已提交） |
| 🔴 严重 | [#4096](https://github.com/OpenHands/software-agent-sdk/issues/4096) | agent-server 崩溃：SecretStr 类型校验错误 | 已关闭 | 已在 v1.36.0 前修复（可查相关 PR） |
| 🟠 高 | [#4098](https://github.com/OpenHands/software-agent-sdk/issues/4098) | 未认证时仍请求模型信息端点，造成无用网络开销 | 新开 | 暂无 |
| 🟠 高 | [#4080](https://github.com/OpenHands/software-agent-sdk/issues/4080) | 单个未注册事件类型导致整个会话加载失败 | 新开 | 暂无，社区建议降级为跳过单个事件 |
| 🟡 中 | [#4032](https://github.com/OpenHands/software-agent-sdk/issues/4032) | LLM 超时设置在 agent-server 重启后重置 | 新开 | 暂无 |
| 🟡 中 | [#4052](https://github.com/OpenHands/software-agent-sdk/issues/4052) | MCP schema 迁移未正确应用 | 新开 | [#4013](https://github.com/OpenHands/software-agent-sdk/pull/4013)（已合并） |
| 🟡 中 | [#3992](https://github.com/OpenHands/software-agent-sdk/issues/3992) | 弱模型因“无工具调用的纯内容响应”不对称处理而终止 | 新开 | 暂无 |
| 🟢 低 | [#3835](https://github.com/OpenHands/software-agent-sdk/issues/3835) | meta-profiles 忽略 OH_PERSISTENCE_DIR，向宿主目录泄漏文件 | 新开 | 暂无 |
| 🟢 低 | [#4105](https://github.com/OpenHands/software-agent-sdk/issues/4105) | 可视化指标副标题易误解为每次请求用量 | 新开 | 暂无 |

### 回归与稳定性改善

- 通过 PR #3895 合并，**agent-server 启动内存暴涨问题** 已根本解决。
- 通过 PR #4088，**文件存储缓存测试的不确定性** 被消除，CI 更稳定。
- 通过 PR #4011，**MCP 嵌套对象属性丢失** 这一影响广泛的功能 Bug 已修复。

---

## 6. 功能请求与路线图信号

### 新提出的功能请求

| Issue | 标题 | 背景 | 可能纳入版本 |
|-------|------|------|--------------|
| [#3442](https://github.com/OpenHands/software-agent-sdk/issues/3442) | Intelligent Model Selection | 自动路由任务到最优模型 | 路线图中期（需结合 LLM Profiles 增强） |
| [#4106](https://github.com/OpenHands/software-agent-sdk/issues/4106) | 结构化方式声明任务不可行（区分成功与失败） | 当前 `FinishAction` 无法区分正常结束与任务不可行 | 下一版本候选 |
| [#4082](https://github.com/OpenHands/software-agent-sdk/issues/4082) | 调研 GPT-5.6 程序化工具调用 | 模型可写 JS 代码调用工具，减少循环调用 | 远期（需等待 OpenAI 正式发布） |
| [#4083](https://github.com/OpenHands/software-agent-sdk/issues/4083) | 调研工具搜索（`defer_loading`） | 按需加载工具定义，减少初始上下文 | 远期 |
| [#4084](https://github.com/OpenHands/software-agent-sdk/issues/4084) | 调研 WebSocket 模式 + previous_response_id | 持久连接，多轮连续响应 | 远期 |
| [#4085](https://github.com/OpenHands/software-agent-sdk/issues/4085) | 调研托管多 Agent（GPT-5.6） vs 客户端子 Agent | 模型端 vs 客户端侧子 Agent 对比 | 远期 |

### 已有对应 PR 的功能

- **选择性上下文激活** (PR [#3890](https://github.com/OpenHands/software-agent-sdk/pull/3890))：根据仓库 AGENTS.md 只给子 Agent 注入必要信息，减少上下文膨胀。状态 OPEN，等待审核。
- **订阅 LLM 再水合** (PR [#4092](https://github.com/OpenHands/software-agent-sdk/pull/4092))：修复持久化订阅模型的 LLM 重新加载问题。
- **插件内容 API** (PR [#4103](https://github.com/OpenHands/software-agent-sdk/pull/4103))：在 agent-server 插件管理 API 中暴露插件内容和元数据。

---

## 7. 用户反馈摘要

从 Issues 评论和 PR 描述中提炼的真实用户痛点与场景：

- **“ACP 技能重复”**（Issue #4019）：用户 `@simonrosenberg` 指出 ACP 配置中注入的工作区项目技能与 CLI 已加载的 AGENTS.md 重复，导致运行时出现两套相同技能。该用户已提交修复 PR #4018，建议维护者尽快合入。
- **“弱模型被过早终止”**（Issue #3992）：用户 `@Rkaplounov` 报告当 LLM 返回仅含内容而无工具调用的响应时，`ResponseDispatchMixin` 不对称处理导致弱模型（如本地小模型）直接终止。该用户认为应处理为“继续对话”而非结束。
- **“MCP 嵌套 schema 丢失”**（Issue #3955，已关闭）：用户 `@s0214lx` 发现 MCP 工具输入 schema 中嵌套对象属性被扁平化为 `dict[str, Any]`，导致 LLM 无法按预期传参。该 Bug 已由 PR #4011 修复，用户在评论中称赞修复快速。
- **“SecretStr 类型校验导致崩溃”**（Issue #4096，已关闭）：用户 `@kripper` 花费数小时定位 agent-server 在启用子 Agent 时第二次对话崩溃的问题，原因是 pydantic 类型校验错误。该问题已在 v1.36.0 之前解决。
- **“启动时加载所有会话导致 OOM”**（Issue #3140、#4102）：多位用户（`@csmith49`, `@neubig`）报告拥有 1000+ 持久化会话时，服务器启动需要数分钟并消耗数 GB 内存。PR #3895 和 #4100 分别提供了延迟加载方案，用户测试后反馈“内存占用大幅降低，加载速度提升明显”。

---

## 8. 待处理积压

### 长期未响应的重要 Issue

| Issue | 标题 | 创建时间 | 上次更新 | 备注 |
|-------|------|----------|----------|------|
| [#2042](https://github.com/OpenHands/software-agent-sdk/issues/2042) | feat(skills): Run skills via sub

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 Pi 项目 GitHub 数据，我为您生成了 2026 年 7 月 14 日的项目动态日报。

---

### Pi 项目动态日报 | 2026-07-14

#### 1. 今日速览

今日项目活跃度极高，社区力量与核心维护响应强劲。尽管无新版本发布，但社区贡献者提交并合并了大量高质量 PR，特别是针对特定模型兼容性（OpenAI Codex / OpenRouter / Bedrock）和关键错误修复。**65 条 Issues 更新**和 **19 条 PR 更新** 表明项目正处于高强度的“清理与修复”阶段，整体健康度良好，正向提升稳定性和跨平台兼容性稳步前进。

#### 2. 版本发布

无新版本发布。

#### 3. 项目进展

今日合并/关闭了 13 个 PR，项目在兼容性、稳定性和新功能方面均有实质性推进。

- **OpenAI Codex 兼容性修复**：
  - **PR #6615** 修复了 `openai-codex` 适配器中硬编码的 `originator: "pi"` 导致 `gpt-5.6-luna` 模型 404 的问题。
  - **PR #6533** 解决了 `gpt-5.6-luna` 在 compaction 过程中因 API 内部模型 ID 映射错误而返回 “Model not found” 的问题。
  - **PR #6544** 为 GitHub Copilot 的 MAI-Code 模型 (`mai-code-1-flash-picker`) 添加了专属的 `/responses` 端点路由，确保其可用性。

- **核心稳定性与错误处理**：
  - **PR #6449** 将 NVIDIA NIM 等 gRPC 服务的 `ResourceExhausted` 错误列入可重试错误模式，提升了服务健壮性。
  - **PR #6595** 修复了使用 `ambient-credential` 认证（如 Bedrock, Vertex AI）时，`/tree` 分支摘要功能因 `apiKey` 为空而抛出 “No API key found” 的 Bug。
  - **PR #6588** 实现了对 OpenAI 和 Codex 的强制函数调用（forced tool call），增强了 Agent 模式下对模型行为的控制力。

- **用户体验与功能增强**：
  - **PR #6572** 新增了对交互式用户消息中的图片块（Image blocks）的渲染支持，并优化了剪贴板图片粘贴流程。
  - **PR #6496** 为 OpenRouter 增加了会话亲和性（session affinity）支持，通过正确发送 `session_id` 以启用提示缓存。
  - **PR #6604** 修复了使用 `npm` 卸载插件时因 peer 依赖冲突而失败的问题。
  - **PR #6599/6597** 引入了 Agent 驱动的 `memory_save` 工具，并统一了 TUI/WebUI 的记忆召回（recall）逻辑，增强了 Agent 的记忆管理能力。
  - **PR #6623** 新增了一个 OSINT 工作站扩展示例，丰富了 `coding-agent` 的用例。

#### 4. 社区热点

- **热度最高的 Bug Report**: **[#6477 Compaction summary requests omit the session ID](https://github.com/earendil-works/pi/issues/6477)**
  - **分析**: 该 Issue 获得 **11 个 👍** 和 **7 条评论**，是今日关注度最高的问题。其核心是 compaction 功能在与特定 API 交互时丢失了会话 ID，导致在较新的 `openai-codex/gpt-5.6-luna` 模型上完全失效（“Model not found”错误）。这反映了社区对**新模型和前沿技术栈的迫切需求**，以及模型兼容性问题对核心功能（如 compaction）的严重障碍。

- **引发讨论的回归问题**: **[#6476 Regression: httpIdleTimeoutMs no longer respected for self-hosted provider (v0.80.6)](https://github.com/earendil-works/pi/issues/6476)**
  - **分析**: 该 Issue 指出从 v0.80.3 升级到 v0.80.6 后，自定义超时设置 `httpIdleTimeoutMs` 不再生效，导致自托管模型（如 vLLM）的请求频繁超时。评论数和反馈表明，**回归问题对依赖特定配置的用户体验产生了立竿见影的负面影响**，社区对版本的稳定性非常敏感。

#### 5. Bug 与稳定性

今日报告的 Bug 主要集中在与特定模型/provider 的交互层面，以及对历史回归的修复。

- **严重 Bug**:
  - **回归问题**: **[#6476 httpIdleTimeoutMs 不再生效](https://github.com/earendil-works/pi/issues/6476)** - 影响所有自定义超时的自托管服务。 (状态: `inprogress`)
  - **核心功能损坏**: **[#6522 OpenAI-completions 发送 1 个 token 导致 400 错误](https://github.com/earendil-works/pi/issues/6522)** - 当代理报告的上下文信息错误时，`max_completion_tokens` 无下限检查，导致请求被拒。 (状态: `inprogress`)
  - **功能崩溃**: **[#6433 DeepSeek V4 + thinking mode 导致会话崩溃](https://github.com/earendil-works/pi/issues/6433)** - v0.80.3 的回归，`reasoning_content` 在历史回放中丢失导致 TUI 直接关闭。 (状态: `inprogress`)

- **严重程度中等 Bug**:
  - **[#6590 segmentation fault](https://github.com/earendil-works/pi/issues/6590)** - 长时间运行后程序崩溃。 (状态: `closed`, 归类为 `no-action`)
  - **[#6589 RPC stream 升级后未处理缓冲命令](https://github.com/earendil-works/pi/issues/6589)** - 升级流程中，客户端可能在初始数据包后被挂起。 (状态: `closed`, 归类为 `no-action`)

- **已修复 Bug**:
  - **[#6364 ResourceExhausted 未加入重试逻辑](https://github.com/earendil-works/pi/issues/6364)** - (PR #6449 已合并)
  - **[#6324 /tree 分支摘要不支持无 API Key 的认证](https://github.com/earendil-works/pi/issues/6324)** - (PR #6595 已合并)
  - **[#6409 Azure OpenAI 多轮推理因 `store:false` 失败](https://github.com/earendil-works/pi/issues/6409)** - (PR #6608 已合并)
  - **[#6567 Anthropic 流中 `message_delta` 缺少 usage 字段](https://github.com/earendil-works/pi/issues/6567)** - (PR #6611 已合并)

#### 6. 功能请求与路线图信号

- **高价值信号**: **[#6477 支持在 Compaction summary 中传递 session ID](https://github.com/earendil-works/pi/issues/6477)** - 社区强烈要求此功能，其中 **[PR #6584](https://github.com/earendil-works/pi/pull/6584)** 看起来是最直接的解决方案，预计会在下一个版本中合并。
- **需求明确**: **[#6366 支持 OpenRouter 的 session ID](https://github.com/earendil-works/pi/issues/6366)** - 已被 **[PR #6496](https://github.com/earendil-works/pi/pull/6496)** 解决，该 PR 旨在提升 OpenRouter 的缓存效率，是重要的性能优化方向。
- **可预见的纳入项**:
  - **[#3200 支持 prompt 命令中的视频/音频内容](https://github.com/earendil-works/pi/issues/3200)** - 随着多模态模型普及，此需求价值高，且已有相关标签，未来很可能被实现。
  - **[#6509 扩展报告外部使用情况的 API](https://github.com/earendil-works/pi/issues/6509)** - 此请求旨在解决子进程成本无法追踪的问题，对复杂 Agent 架构至关重要，可能被纳入扩展能力的路线图中。

#### 7. 用户反馈摘要

- **正面反馈**: 用户对 **[PR #6533](https://github.com/earendil-works/pi/pull/6533) 和 [PR #6615](https://github.com/earendil-works/pi/issues/6615)** 的快速跟进非常满意，修复了 `gpt-5.6-luna` 的使用问题，体现了项目对前沿模型的支持。
- **痛点反馈**:
  - **WSL 集成问题**: **[#6187 Pi 在 WSL 中登录后挂起](https://github.com/earendil-works/pi/issues/6187)** 用户反映设备授权完成后，客户端无法检测到并继续进程，这是一个长期存在的环境兼容性问题。
  - **自定义配置失效**: **[#6459 自定义键绑定在初始会话不生效](https://github.com/earendil-works/pi/issues/6459)** 和 **[#6476 自定义超时设置被忽略](https://github.com/earendil-works/pi/issues/6476)** 表明，用户对自定义配置的遵从性期望很高，任何回归或未能生效的问题都会引起不满。
  - **Windows 生态兼容**: **[#6619 Windows 上扩展依赖路径显示异常](https://github.com/earendil-works/pi/issues/6619)** 和 **[#6605 SSH 扩展需处理 Windows 路径](https://github.com/earendil-works/pi/issues/6605)** 揭示了在非 Linux 平台上仍有待解决的兼容性细节。

#### 8. 待处理积压

- **重要功能请求**: **[#3200 支持 prompt 命令中的视频/音频内容](https://github.com/earendil-works/pi/issues/3200)** - 从 4 月就提出的功能请求，获得了多个 👍，但至今未分配或有关联 PR。随着多模态模型成为主流，推动此功能的优先级应提高。
- **延期的 Bug 修复**: **[#3721 功能请求: 不发送消息即可恢复Agent循环](https://github.com/earendil-works/pi/issues/3721)** - 一个获得 3 个 👍 且讨论度较高（3条评论）的功能请求，涉及 Agent 交互体验的核心，目前已被标记为`closed-because-weekend`，建议维护者重新审视并评估其价值。
- **未合并的长期 PR**: **[#6216 增加 Amazon Bedrock Mantle OpenAI Responses provider](https://github.com/earendil-works/pi/pull/6216)** - 一个重要的新 Provider PR，已开放超过两周。它虽然进展缓慢，但对扩大 AWS 用户群体有重要意义，应尽快安排审查。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 · 2026-07-14

---

## 1. 今日速览

过去 24 小时，LiteLLM 项目继续保持极高活跃度：共产生 **62 条 Issues**（新开/活跃 44，关闭 18）和 **287 条 PR**（待合并 127，已合并/关闭 160）。虽然无新版本发布，但 PR 合并量（160 条）和 Rust 迁移等长期议题的持续进展表明团队正加速推进内核重构与功能稳定。社区对定价策略（SSO 用户数限制）、UI 可用性（Dark Mode）以及 Claude Code 兼容性的讨论热度依然较高。

---

## 2. 版本发布

**无**（过去 24 小时无新版本发布）。最新稳定版仍为 1.x 系列（请留意近期 v1.92 相关 Bug 报告）。

---

## 3. 项目进展

今日合并/关闭的 PR 虽未在顶部列表中完整展示（共 160 条合并/关闭），但可见的有：

- **UI 重构与质量**  
  - [#33044](https://github.com/BerriAI/litellm/pull/33044) `[CLOSED]` 移除 lodash 依赖后禁止重新引入，提升打包体积。  
  - [#33124](https://github.com/BerriAI/litellm/pull/33124) `[CLOSED]` 使用 shadcn ScrollArea 重绘侧边栏滚动条，改善 UI 一致性。  
  - [#33043](https://github.com/BerriAI/litellm/pull/33043) `[CLOSED]` 将回调 debounce 迁移至 react-pacer 并补充回归测试，降低 UI 偶发卡顿。

- **新功能开放中（值得关注）**  
  - [#33129](https://github.com/BerriAI/litellm/pull/33129) `[OPEN]` 在 Responses API 中拦截 web search，为未来联网搜索能力铺路。  
  - [#33130](https://github.com/BerriAI/litellm/pull/33130) `[OPEN]` 新增 PTU（预留吞吐量）预订表及管理 CRUD 端点，面向企业级容量保障。  
  - [#33117](https://github.com/BerriAI/litellm/pull/33117) `[OPEN]` 往 Prometheus provider 缓存指标中加入 `model_group` 标签，提升可观测性细粒度。

> 总体看，项目在 **UI 体验、企业特性（PTU、MCP OAuth）、可观测性** 三线并进，Rust 迁移（见 Issue [#31263](https://github.com/BerriAI/litellm/issues/31263)）进度由专门的 PR 系列跟进，尚未合并到主干。

---

## 4. 社区热点

| 议题 | 评论数 | 核心诉求 |
|------|--------|----------|
| [#361](https://github.com/BerriAI/litellm/issues/361) 功能愿望单（已关闭） | 468 | 长期收集用户需求，虽已关闭但仍是社区情绪集中地。 |
| [#10177](https://github.com/BerriAI/litellm/issues/10177) **Dark Mode** | 56 + 64 👍 | 用户强烈要求管理后台增加黑暗主题，被赞 “I'm going blind”。 |
| [#25762](https://github.com/BerriAI/litellm/issues/25762) **SSO 用户数限制** | 11 + 13 👍 | Standard 计划仅允许 5 个 SSO 用户，中小团队认为不合理。 |
| [#31263](https://github.com/BerriAI/litellm/issues/31263) **Rust 迁移** | 8 + 11 👍 | 官方主导的性能优化，目标延迟 <1ms，已开放 Beta 注册。 |
| [#24123](https://github.com/BerriAI/litellm/issues/24123) **支持 Langfuse SDK v4** | 7 + 10 👍 | 当前锁定 v2，用户希望跟上 upstream 更新，避免兼容性问题。 |

**分析**：Dark Mode 属于基础体验缺失，SSO 用户限制则涉及定价策略争议；Rust 迁移是社区最期待的技术突破，但尚处早期 Beta。Langfuse 版本落后的呼声反映用户对观测集成保持最新的强烈期望。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue | 描述 | 是否有 Fix PR |
|----------|-------|------|---------------|
| **严重** | [#33074](https://github.com/BerriAI/litellm/issues/33074) | v1.92 版本 `budget_fallbacks` 列缺失，导致 Admin UI 完全不可登录（致命错误） | 暂无 |
| **严重** | [#33075](https://github.com/BerriAI/litellm/issues/33075) | Anthropic `/v1/messages` 向 OpenAI 格式后端转发时未翻译 `stop_sequences`，Claude Code 对 GPT-5.6 完全失败 | 暂无 |
| **严重** | [#32214](https://github.com/BerriAI/litellm/issues/32214) | v1.91.0 回归：Anthropic 格式多轮工具调用在 vLLM/Kimi K2.7 后端崩溃 | 暂无 |
| **高** | [#30761](https://github.com/BerriAI/litellm/issues/30761) | 流式传输中收到空 `choices` 块时桥接崩溃，影响 Anthropic / Azure 兼容场景 | 暂无 |
| **高** | [#33072](https://github.com/BerriAI/litellm/issues/33072) | MCP Gateway OAuth token 过期后工具消失（无自动刷新），上游 token 过期后仍需手动干预 | 暂无（但有相关 PR [#32980](https://github.com/BerriAI/litellm/pull/32980) 在开发中） |
| **中** | [#25386](https://github.com/BerriAI/litellm/issues/25386) | `max_end_user_budget_id` 未持久化到 DB，预算重置任务跳过自动创建的用户 | 暂无 |
| **中** | [#25553](https://github.com/BerriAI/litellm/issues/25553) | `update_cache` 在高并发下复活已失效的 key 缓存，导致 `/key/update` 更改被绕过 | 暂无 |
| **中** | [#25623](https://github.com/BerriAI/litellm/issues/25623) | `LiteLLM_HealthCheckTable` 无限制增长，Uptime Kuma 持续监控导致 Dashboard 性能退化 | 暂无 |
| **低** | [#25624](https://github.com/BerriAI/litellm/issues/25624) | Pass-through 端点转发 gzip 响应后 `Content-Length` 与实际解压体大小不匹配，客户端连接中断 | 暂无 |

**重点警告**：v1.92 的数据库 schema 变更在升级过程中缺少迁移脚本，已导致多起用户生产环境不可用。在正式修复前，建议暂不升级至 1.92。

---

## 6. 功能请求与路线图信号

| 功能请求 | 类型 | 当前状态 | 路线图信号 |
|----------|------|----------|------------|
| **Dark Mode** ([#10177](https://github.com/BerriAI/litellm/issues/10177)) | UI | OPEN，56 评论 | 高热度，无关联 PR，可能在 UI 重构完成后列入 |
| **无限 SSO 用户** ([#25762](https://github.com/BerriAI/litellm/issues/25762)) | 定价 | OPEN | 社区对定价策略不满，可能影响付费转化 |
| **Rust 迁移** ([#31263](https://github.com/BerriAI/litellm/issues/31263)) | 性能 | OPEN，Beta 招聘中 | 官方核心项目，预计后续版本逐步替换关键路径 |
| **Langfuse SDK v4** ([#24123](https://github.com/BerriAI/litellm/issues/24123)) | 集成 | OPEN | 当前 pin v2，社区希望升级以支持最新 Langfuse 特性 |
| **多模态 embedding** ([#24393](https://github.com/BerriAI/litellm/issues/24393)) | SDK | OPEN | Gemini embedding-2-preview 仅支持文本模式，用户需图像/PDF 支持 |
| **CLI 模式运行代理** ([#25611](https://github.com/BerriAI/litellm/issues/25611)) | 部署 | OPEN | 希望无容器化运行，简化本地开发 |
| **per-MCP-server Prometheus 计数** ([#32235](https://github.com/BerriAI/litellm/issues/32235)) | 可观测性 | OPEN | 已有 [#33117](https://github.com/BerriAI/litellm/pull/33117) 增加 model_group，但未覆盖 MCP server，可视为后续方向 |
| **Minimax-M2.7 模型成本** ([#33058](https://github.com/BerriAI/litellm/issues/33058)) | 成本 | OPEN | 成本映射缺失，社区提交补丁意愿强 |

**推断**：Rust 迁移、PTU 预订、MCP OAuth 刷新是当前内部开发主线；UI 黑暗主题和 SSO 限制属于用户呼声极高但尚未排期的非核心优化。

---

## 7. 用户反馈摘要

- **“配置 MCP 静态头部完全无效”**（[#18169](https://github.com/BerriAI/litellm/issues/18169)）—— 用户试图连接需自定义 Header 的 OpenAPI MCP 服务器，`static_headers` 被忽略，导致集成失败。该问题已存在 7 个月，至今未修复，社区对 MCP 能力的完整性有强烈质疑。
- **“升级 v1.92 后 Admin UI 直接瘫痪”**（[#33074](https://github.com/BerriAI/litellm/issues/33074)）—— `budget_fallbacks` 列未自动创建，用户无法登录，需手动回退版本。这是近期最严重的升级事故。
- **“Claude Code 无法在 GPT-5.6 后端工作”**（[#33075](https://github.com/BerriAI/litellm/issues/33075)）—— 用户在代理后使用 Anthropic 格式但目标为 Azure AI，`stop_sequences` 未被翻译成 OpenAI 格式的 `stop`，导致 400 错误。此问题阻碍了 Claude Code 用户拥抱多提供商。
- **“多轮工具调用在 vLLM + Kimi K2.7 后端崩溃”**（[#32214](https://github.com/BerriAI/litellm/issues/32214)）—— 回归发生在 v1.91.0，社区中 Claude Code 重度使用者受影响，期待紧急修复。
- **“MCP 工具在 OAuth token 过期后消失”**（[#33072](https://github.com/BerriAI/litellm/issues/33072)）—— 用户发现 `/tools/list` 在 token 过期后不返回工具，需重新连接。这是一个中等频率但影响关键工作流的稳定性问题。
- **“预算归零后 key 自动刷新不生效”**（[#25553](https://github.com/BerriAI/litellm/issues/25553)）—— 高并发下缓存复活陈旧 key，绕过 budget 限制，用户担心产生意外费用。

---

## 8. 待处理积压

以下 Issues 已标记 `stale` 或长期未响应，可能影响社区信任：

| Issue | 创建时间 | 最后活动 | 状态 | 备注 |
|-------|----------|----------|------|------|
| [#18169](https://github.com/BerriAI/litellm/issues/18169) MCP static_headers 忽略 | 2025-12-18 | 2026-07-13 | OPEN | 7 个月无修复，用户回复中表示失望 |
| [#24393](https://github.com/BerriAI/litellm/issues/24393) Gemini 多模态 embedding | 2026-03-23 | 2026-07-13 | OPEN | 4 个月未排期，无明显进展 |
| [#25386](https://github.com/B

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

好的，这是为您生成的 Temporal 项目动态日报。

---

# Temporal 项目动态日报 | 2026-07-14

## 今日速览

过去24小时内，Temporal 项目主要处于高强度开发与维护状态。**PR 活跃度极高**，共处理51条PR，其中近半数（22条）已完成合并或关闭，显示出核心团队在快速推进功能开发和修复。**社区讨论主要集中在基础设施升级**，围绕老旧的 Elasticsearch 客户端替换的 Issue 持续获得关注。尽管无新版本发布，但多个针对 CI/CD、测试框架和核心功能（如 Standalone Activity、Nexus）的 PR 正在积极迭代，项目健康度良好。

## 项目进展

过去24小时内，一些关键领域的改进正在稳步推进。虽然没有明确标注“今日合并”的单一重大功能，但从 PR 列表看，项目在以下多个方向有实质性进展：

- **基础架构与工具链优化**：
  - **CI 报告改进**：PR [#11019](https://github.com/temporalio/temporal/pull/11019) 正在为 CI 失败添加更详细的报告，提高失败定位效率。
  - **测试框架迁移**：PR [#11033](https://github.com/temporalio/temporal/pull/11033) 尝试移除 `gotestsum`，直接从 `go test` 生成 JUnit 报告，以解决测试超时场景下的报告问题。PR [#10801](https://github.com/temporalio/temporal/pull/10801) 推动将 `testify suites` 迁移至 `parallelsuite`。
  - **面板与监控**：PR [#11039](https://github.com/temporalio/temporal/pull/11039) 正在为监控添加运行时内存诊断。
- **核心功能推进**：
  - **Nexus 操作**：PR [#10986](https://github.com/temporalio/temporal/pull/10986) 正在为 CHASM (Common History Access Storage Model) 支持的 Nexus 操作增加工作流重置重试支持，这是核心复制和恢复功能的关键部分。PR [#11022](https://github.com/temporalio/temporal/pull/11022) 为 Nexus 任务令牌添加了任务队列类型，以区分内部和用户触发的 Nexus 调用。
  - **Standalone Activity**：多个 PR 同时推进了这一新特性。PR [#11017](https://github.com/temporalio/temporal/pull/11017) 为其增加了可见性支持；PR [#11016](https://github.com/temporalio/temporal/pull/11016) 修复了重试延迟计算问题；PR [#10803](https://github.com/temporalio/temporal/pull/10803) 为其实现了批量终止/取消/删除操作。
- **错误处理与稳定性**：
  - **错误修复**：PR [#10926](https://github.com/temporalio/temporal/pull/10926) 修复了当当前执行被删除时，工作流重置失败的问题。PR [#11016](https://github.com/temporalio/temporal/pull/11016) 修复了Standalone Activity更新选项时，重试间隔计算错误的问题。
  - **资源耗尽错误**：PR [#11036](https://github.com/temporalio/temporal/pull/11036) 为三个资源耗尽（ResourceExhausted）错误设置了显式作用域，使错误分类更精确。

## 社区热点

1.  **#7930: 替换已废弃的 Elasticsearch 客户端（热门讨论）**
    - **热度**：16条评论，过去24小时内有更新。
    - **链接**：[https://github.com/temporalio/temporal/issues/7930](https://github.com/temporalio/temporal/issues/7930)
    - **分析**：这是目前社区最关注的 Issue。核心诉求是替换已被官方弃用的第三方库 `github.com/olivere/elastic/v7`，转而使用 Elastic 官方提供的 Go 客户端。这反映了用户对项目依赖库健康度和长期维护成本的担忧。替换官方客户端意味着更好的兼容性、安全更新和性能支持。该 Issue 的存在时间较长，表明这是一个已知但尚未解决的技术债务。

2.  **#11026: 在UI中显示 Activity Task 的标准输出 (STDOUT)**
    - **热度**：新建 Issue，无评论。
    - **链接**：[https://github.com/temporalio/temporal/issues/11026](https://github.com/temporalio/temporal/issues/11026)
    - **分析**：这是一个新提出的功能需求，但反映了开发者日常排错的痛点。当前只能通过查看混合了所有任务的 Worker 日志来获取 STDOUT，非常不便。将此信息直接展示在 UI 中，能极大提升开发者调试 Workflow 和 Activity 的效率。

## Bug 与稳定性

- **严重：** `ResourceExhausted` 错误缺少作用域信息
    - **描述**：多处的“资源耗尽”错误未正确设置 `Scope`，导致错误原因不明确。
    - **修复 PR**: [#11036](https://github.com/temporalio/temporal/pull/11036) 已提交，正在等待合并。
- **严重：** 工作流重置在特定场景下失败
    - **描述**：当针对一个已被删除的“当前执行”的工作流进行重置时，会失败。
    - **修复 PR**: [#10926](https://github.com/temporalio/temporal/pull/10926) 已提交，通过容忍缺失的“当前执行”来解决。
- **中等：** Standalone Activity 重试间隔计算错误
    - **描述**：当更新 Activity 选项时，重试间隔可能被意外重置，导致重试延迟。
    - **修复 PR**: [#11016](https://github.com/temporalio/temporal/pull/11016) 已提交。

## 功能请求与路线图信号

社区新提出的功能请求包括：

- **第一类持久化订阅集用于计划工作流扇出** (`#11025`)：用户希望 Temporal 能原生支持一种模式，即一个计划任务运行时，能启动多个相同的工作流副本（工作流扇出），这是构建批量数据处理应用程序的常见需求。
- **在UI中显示 Activity STDOUT** (`#11026`)：如前所述，旨在改善调试体验。
- **替换 Elasticsearch 库** (`#7930`)：基础设施升级需求，用户强烈希望解决技术债务。

**路线图信号**：从 PR 列表中可看出，项目正将大量资源投入到“Standalone Activity”和“Nexus/CHASM”这两个新特性上。这表明未来版本可能重点围绕**支持更灵活的 Activity 生命周期管理**（不受 Workflow 状态限制）和**提升历史服务的数据模型与存储效率**（CHASM）。`#7930` 的 Elasticsearch 迁移也有可能在不久后进入开发日程。

## 用户反馈摘要

- **痛点**：用户在 `#11026` 中表达了调试 Activity 时的不便，认为仅显示输入输出不够，需要查看 STDOUT。
- **期望**：在 `#7930` 中，用户明确希望项目移除对已弃用库的依赖，采用最佳实践的官方方案，表现出对项目长期健康度的关注。
- **清晰度需求**：在 `#10716` 中，用户请求 Clarify（澄清）代码中关于“编辑某些错误”的 TODO 注释，这反映出用户希望代码行为尽可能明确和可预测，减少潜在的安全风险或返回不必要信息的问题。

## 待处理积压

- `**#7930**` **: 替换 Elasticsearch 库**
    - **状态**：创建于2025-06-18，已开放超过一年，评论数16，是长期未解决的关键技术债务。
    - **建议**：该项目应被提升优先级，进入项目的短期路线图，因为使用已弃用的依赖对任何生产系统都是风险。维护团队应尽快回应社区关切，明确计划。
    - **链接**：[https://github.com/temporalio/temporal/issues/7930](https://github.com/temporalio/temporal/issues/7930)
- `**#10200**` **: Validator generator [WiP] (工作中)**
    - **状态**：这是一个创建于2026-05-08的工作中 PR，旨在为所有 protobuf 字段生成校验器。它长期处于开放状态，可能是一个大型重构任务。
    - **建议**：PR 作者应定期更新状态，评估是否需要进行拆分以降低合并风险。
    - **链接**：[https://github.com/temporalio/temporal/pull/10200](https://github.com/temporalio/temporal/pull/10200)
- `**#10218**` **: Dispatch cancel command for standalone activities (为独立Activity分发取消命令)**
    - **状态**：创建于2026-05-11的 PR，同样是推进 Standalone Activity 特性的关键部分。
    - **建议**：与 `#10803`、`#11016` 等 PR 共同构成 Standalone Activity 的完整功能集，建议维护者考虑将这些关联 PR 打包合并，以完整交付该特性。
    - **链接**：[https://github.com/temporalio/temporal/pull/10218](https://github.com/temporalio/temporal/pull/10218)

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*