# OpenClaw 生态日报 2026-07-20

> Issues: 352 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-20 02:14 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，以下是根据您提供的 OpenClaw 项目数据生成的 **2026-07-20 项目动态日报**。

---

## OpenClaw 项目日报 | 2026-07-20

### 1. 今日速览

过去 24 小时，OpenClaw 社区活跃度极高：Issues 更新 352 条（新开/活跃 234 条，关闭 118 条），Pull Requests 更新 500 条（待合并 351 条，已合/关闭 149 条），项目整体处于高频迭代状态。安全、会话状态与消息丢失相关的话题持续成为焦点；大量 PR 集中在文件读取限界、通道连接稳定性等方面。当日无新版本发布，但多领域的修复与功能提案正在密集推进。

### 2. 版本发布

（无）

### 3. 项目进展

今日有多项重要 PR 被合并或关闭，以下是值得关注的关键变动：

- **Discord Activity 边界保护** – PR [#108901](https://github.com/openclaw/openclaw/pull/108901) 已关闭：为 Discord Activity shell 请求添加超时，防止网关挂起导致 Activity 卡死在加载状态。
- **LINE 媒体轮询修复** – PR [#111057](https://github.com/openclaw/openclaw/pull/111057) 已合并：修复 LINE 频道在响应体清理失败时停止轮询的问题，确保 HTTP 202 场景下的持续拉取。
- **DuckDuckGo 高亮词截断修复** – PR [#111460](https://github.com/openclaw/openclaw/pull/111460) 已合并：修复搜索结果中因高亮切割导致单词中间出现空格（如 `caf é`）的显示异常。
- **QQ 频道消息丢失修复** – PR [#109997](https://github.com/openclaw/openclaw/pull/109997) 处于 `ready for maintainer look` 状态，解决网关重连后排队中的消息静默丢失问题，对中文用户影响较大。
- **Venice 模型上下文窗口动态更新** – PR [#111237](https://github.com/openclaw/openclaw/pull/111237) 新增：使 Venice 模型列表显示当前实时的上下文限制而非静态缓存值。

此外，多个涉及文件读取限界的安全加固 PR 正在排队（如 [#111586](https://github.com/openclaw/openclaw/pull/111586)、[#111591](https://github.com/openclaw/openclaw/pull/111591)），表明团队正在系统性地治理资源滥用风险。

### 4. 社区热点

以下 Issues 和 PR 在过去 24 小时内获得了最多的讨论与关注：

- **#75 – Linux/Windows Clawdbot Apps** ([链接](https://github.com/openclaw/openclaw/issues/75))  
  评论 114 条，👍 80 个。用户强烈呼吁补齐 Linux 与 Windows 平台的 Clawdbot 桌面应用，与已有 macOS/iOS/Android 对齐。该 Issue 持续活跃近 7 个月，仍无定论，社区期待度极高。

- **#7707 – Feature Request: Memory Trust Tagging by Source** ([链接](https://github.com/openclaw/openclaw/issues/7707))  
  评论 17 条。用户担心来自网页、第三方技能的输入可能污染 agent 记忆，要求按来源标记信任等级。该功能直接呼应近期频发的“记忆投毒”安全事件。

- **#10659 – Masked Secrets: Prevent Agent from Accessing Raw API Keys** ([链接](https://github.com/openclaw/openclaw/issues/10659))  
  评论 14 条，👍 4 个。提出“掩码密钥”机制：让 agent 能使用密钥但不直接看到明文，避免提示注入导致凭据泄露。高安全性诉求。

- **#13583 – Pre-response enforcement hooks (hard gates)** ([链接](https://github.com/openclaw/openclaw/issues/13583))  
  评论 14 条。要求在关键工作流（金融、运维）中强制 agent 必须先调用指定工具才能回复，不能仅靠 prompt 中的“软指令”。用户来自量化/安全领域。

- **#79077 – Support for Telegram bot-to-bot and guest-bot modes** ([链接](https://github.com/openclaw/openclaw/issues/79077))  
  评论 11 条，👍 8 个。Telegram 2026-05-07 发布的新特性（Guest Bots、Bot-to-Bot Communication），社区希望 OpenClaw 及时跟进。

**分析**：当前社区热点高度集中在两个方向：**安全加固**（记忆投毒、密钥屏蔽、强制工具调用）与**渠道扩展**（Linux/Windows App、Telegram 新特性）。安全类需求多获得“diamond lobster”等高优先级评级，表明维护者已将其列入重点。

### 5. Bug 与稳定性

以下按严重程度排列今日报告的 Bug 与回归问题（附是否有对应 fix PR）：

| 严重等级 | Issue / PR | 描述 | 状态 |
|----------|------------|------|------|
| **P1 回归** | [#108075](https://github.com/openclaw/openclaw/issues/108075) | 2026.7.1 版本 agent 启动时 LLM 请求失败：provider 拒绝请求 schema 或工具 payload | 已关闭，待查 fix |
| **P1 回归** | [#108238](https://github.com/openclaw/openclaw/issues/108238) | 会话上下文用量将累计 cacheRead 计入 totalTokens，导致误报上下文超限并触发压缩失败（中文用户反馈） | 已关闭，关联 PR 已开 |
| **P1 行为** | [#109490](https://github.com/openclaw/openclaw/issues/109490) | codex app-server: 客户端委托的 message 工具返回 terminate:true 后，后续承诺的工作永远不会执行 | OPEN，无 fix PR |
| **P1 行为** | [#92076](https://github.com/openclaw/openclaw/issues/92076) | 子 agent 完成交付在请求者会话不活跃时可能失败，导致消息丢失 | OPEN，标签 `fix-shape-clear` |
| **P1 崩溃** | [#102006](https://github.com/openclaw/openclaw/issues/102006) | exec 工具中止后，同会话中后续 exec 调用无限挂起（PR #94412 引入回归） | OPEN，无 fix PR |
| **P1 行为** | [#111519](https://github.com/openclaw/openclaw/issues/111519) | Telegram DM 回复降级：2026.7.2-beta.3 中 DM 作用域清理后丢失源回复所有权 | OPEN，需更多信息 |
| **P2 行为** | [#94846](https://github.com/openclaw/openclaw/issues/94846) | Cron 隔离 agentTurn 中已恢复的早期工具错误被误判为致命错误，跳过最终交付 | OPEN，`fix-shape-clear` |
| **P2 行为** | [#93139](https://github.com/openclaw/openclaw/issues/93139) | write 工具和 exec heredocs 在字符串内容中插入字面 `\n` 而非换行符 | OPEN |
| **P2 安全** | [#97970](https://github.com/openclaw/openclaw/issues/97970) | `openclaw update` 自动补全 `gateway.bind:lan` 与 `auth.mode:none` 冲突导致 exit 78（中文用户反馈） | 已关闭 |

**关键发现**：当日新增两个中文社区反馈的回归 Bug（#108238、#97970），表明近期版本对中文配置用户存在兼容性问题。exec 工具回归（#102006）严重阻碍自动化工作流，急需修复。

### 6. 功能请求与路线图信号

以下功能需求获得高优先级标签或社区高赞，可能进入下一版本：

- **Memory Trust Tagging by Source** (#7707) – 按来源标记记忆信任度，防投毒。已有多个关联 PR 讨论，安全优先级高。
- **Masked Secrets** (#10659) – 密钥掩码机制。直接解决提示注入提取凭据的痛点，可能配合“Skill Permission Manifest” (#12219) 形成完整权限体系。
- **Pre-response enforcement hooks** (#13583) – 硬性前置工具调用门控。金融/安全场景刚需，已有 PR 提案雏形。
- **Webhook hook sessions multi-turn** (#11665) – 让 `/hooks/agent` 支持真正的多轮对话（目前每次新建 session）。已有 PR 打开但未合并，修复意愿明确。
- **Exec-approvals denylist** (#6615) – 除允许列表外增加拒绝列表，支持“除了 X 全允许”策略。社区👍高，解决日常操作繁琐问题。
- **Everything is a cron** (#110950) – 将心跳、监视器、定时任务统一为 cron 原语。由维护者 @steipete 提出，可能成为后续架构重构方向。
- **Group session 合并** (#7524) – 允许群聊会话合并到主会话（类似 dmScope），解决碎片化问题。标签 `linked-pr-open`，表明已有对应 PR。

**路线图信号**：安全与权限体系 (#7707/#10659/#13583) 显然是目前路线图的第一优先级；渠道功能（Telegram 新模式、WhatsApp 监听模式）紧随其后；架构层面的“cron 统一化”可能在中长期规划中。

### 7. 用户反馈摘要

从当日 Issues 评论中可提炼出以下用户真实痛点与场景：

- **“软指令不可靠”**（#13583）：用户指出在金融交易等场景中，仅靠 prompt 要求 agent “必须先调用风控工具”无法刚性保障，必须机械性阻止最终回复。
- **“子 agent 无声无息就没了”**（#92076、#39248）：多名用户反映子 agent（spawn）的完成结果经常丢失，或者无法执行，且无错误提示，非常困惑。
- **“Telegram 更新后回复乱了”**（#111519）：使用新版 beta 后 DM 回复出现延迟或分配给错误的对话，影响日常聊天体验。
- **“更新后 Gateway 直接挂了”**（#97970）：中文用户因为 update 自动修改配置导致 exit 78，被迫回滚，信任度下降。
- **“WebChat 图片发不出去”**（#103198）：用户通过 WebChat 发送图片，agent 只收到 `image_0` 字符串而无法获取实际文件路径，基本不可用。
- **“TUI 不能换行”**（#10118）：多位终端重度用户呼吁支持 Shift+Enter 换行，目前 Enter 直接发送导致无法编辑多行提示。
- **“Cron 任务结果被静默丢弃”**（#87182）：记忆核心的梦境叙事文本因为竞态条件丢失，用户无法查看 agent 的自我总结。

**总体情绪**：用户对安全与可靠性改进持积极态度，但对近期回归的稳定性问题（exec 工具挂起、会话上下文误判、配置冲突）感到不满。功能需求方面，Linux/Windows 桌面应用呼声最高，但长期未响应。

### 8. 待处理积压

以下 Issue 或 PR 长期未取得进展，或缺少维护者关注，建议优先响应：

| 项目 | 说明 | 建议行动 |
|------|------|----------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | Linux/Windows Clawdbot Apps，评论 114 条，7 个月无实质进展 | 至少给出 roadmap 或暂时不做的明确说明 |
| [#85246](https://github.com/openclaw/openclaw/issues/85246) | UI Update 按钮导致 Gateway 崩溃（npm global + launchd），P1 但 stale | 需要 maintainer review 或确认是否已修复 |
| [#83337](https://github.com/openclaw/openclaw/issues/83337) | 插件与核心版本不匹配导致频道静默失效，P1、`needs-maintainer-review` | 建立版本一致性机制或升级时自动检查 |
| [#82540](https://github.com/openclaw/openclaw/issues/82540) | 微信热重载时账号丢失，PR 已存在但超过 2 个月未合并（`needs proof`） | 协调 reviewer 完成验证 |
| [#99910](https://github.com/openclaw/openclaw/issues/99910) | Memory dreaming 占满 Gateway 事件循环 ~10 分钟，P1、`needs-live-repro` | 尝试复现并挂钩 profiling，降级用户影响 |
| [#92405](https://github.com/openclaw/openclaw/issues/92405) | 子 agent 深度 2 冷启动丢失执行上下文，有 fix 建议但未合并 | 检查 #57326 的剩余两个未修补调用点 |
| [#110950](https://github.com/openclaw/openclaw/issues/110950) | “Everything is a cron” 重构倡议，维护者提出但无后续 | 如认可方向，应开始 RFC 讨论 |

---

**日报总结**：OpenClaw 当前处于高频活跃期，社区贡献与质量反馈双高。安全与可靠性是主线，但部分 P1 回归已影响实际使用，建议短期内优先修复 exec 工具挂起（#102006）、会话上下文误判（#108238）及配置冲突（#97970）等直接影响用户体验的问题。同时，对长期积压的桌面应用需求、微信热重载 PR 等需要维护者给出明确回应。

---

## 横向生态对比

好的，作为专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师，以下是我基于您提供的五个项目（OpenClaw, Hermes Agent, OpenHands SDK, Pi, LiteLLM）及一个生态相关项目（Temporal）的日报，为您生成的横向对比分析报告。

---

### **2026-07-20 个人 AI 智能体开源生态横向对比分析报告**

#### **1. 生态全景**

当前，个人 AI 助手与自主智能体开源生态正处于 **“高频迭代、安全焦虑、分化加剧”** 的十字路口。一方面，核心项目（如 OpenClaw, Hermes Agent）的社区贡献异常活跃，每日数百条 PR/Issue 的更新表明行业正疯狂吞噬功能与修复；另一方面，用户对**记忆安全、密钥防护、工具调用可靠性**的呼声达到顶峰，形成了对“软指令”不信任、要求“硬门控”的刚性需求。同时，生态内部出现明显分化：**全能型Agent框架（OpenClaw, Hermes）** 与 **特定场景工具（Pi, LiteLLM）** 及 **基础设施（Temporal）** 正走向不同的成熟路径。

#### **2. 各项目活跃度对比**

| 项目 | 负责人/组织 | 24h Issue活跃/新增 | 24h PR活跃/新增 | 今日版本 | 合并效率 (PR关闭/总活跃) | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | openclaw | 352 | 500 | 无 | 29.8% (149/500) | **重提交、重讨论，合并瓶颈明显** |
| **Hermes Agent** | NousResearch | 500 | 500 | 无 | 待定 (数据未明确区分新旧) | **极高强度，脉冲式增长，合并压力大** |
| **OpenHands SDK** | OpenHands | 13 | 34 | 无 | **0% (0/34)** | **“重提交、轻合并”，积压风险高** |
| **Pi** | earendil-works | 29 (关闭) | 8 (已合并) | 无 | **88.9% (8/9)** | **高响应、高效率、状态极佳** |
| **LiteLLM** | BerriAI | 28 | 75 | v1.93.0 | 27.2% (28/103) | **集成紧、发布勤，但积压与回归并存** |
| **Temporal** | temporalio | 1 | 5 (待合并) | 准备中 | 28.6% (2/7) | **成熟稳健，专注底层基础，节奏平稳** |

**分析**：
- **OpenClaw** 和 **Hermes Agent** 社区规模庞大，但“提交量大、合并量小”的模式可能导致贡献者热情受挫和高质量代码滞留。
- **Pi** 的合并效率异常突出（88.9%），表明其维护者投入度高，社区治理流程简洁高效。
- **OpenHands SDK** 的合并效率为0%，是一个值得警惕的信号，说明项目核心团队可能在资源分配或审查流程上遇到瓶颈。
- **LiteLLM** 虽有小版本发布，但合并效率不高，且同时报告了严重回归，表明其快速迭代模式牺牲了部分稳定性。

#### **3. OpenClaw 在生态中的定位**

OpenClaw 是当前生态中**社区规模最大、功能最全面的全能型 Agent 框架**。其核心优势在于：
- **多平台渠道支持：** 对 Discord、LINE、QQ、Telegram 等社交通道原生支持，这是其他项目难以比拟的。
- **强大的社区生态：** 拥有最高的 Issue 和 PR 活跃度，意味着更广泛的第三方贡献和功能提议。
- **安全优先级高：** 对于“记忆投毒”、“密钥掩码”等高级安全议题的讨论最为深入，体现了其面向生产级用户的定位。

与同类相比：
- **vs Hermes Agent**: OpenClaw 更侧重**渠道集成与终端用户体验**，而 Hermes 更侧重**核心 Agent 性能优化（如 TTFT）和本地模型支持**。
- **vs Pi**: Pi 是一个**极客向的终端产品**，专注于无缝的 IDE/终端体验；而 OpenClaw 是一个**通用开发框架**，需更多配置和集成。

#### **4. 共同关注的技术方向**

多个项目不约而同地指向以下核心痛点，表明行业共识正在形成：

| 技术方向 | 涉及项目 | 具体诉求 (来自Issue标题) |
| :--- | :--- | :--- |
| **安全与权限控制** | OpenClaw, Hermes, OpenHands | “Memory Trust Tagging by Source”、 “Masked Secrets”、“Pre-response enforcement hooks”、“PreToolUse enforcement hook” |
| **会话状态与可靠性** | OpenClaw, Hermes, Pi, LiteLLM | “消息丢失修复”、“会话空白”、“会话内容错乱”、“`assistant.usage` undefined导致崩溃” |
| **本地模型与性能优化** | Hermes, Pi, OpenHands | “KV cache invalidation on compression hurts local MoE models”、“高CPU占用”、“LiteLLM-backed provider abstraction” |
| **生态集成与标准化** | LiteLLM, OpenClaw, Pi | “MCP 服务器 `static_headers` 被忽略”、“ACP模式功能合入”、“支持 Gemini 多模态嵌入” |

#### **5. 差异化定位分析**

| 对比维度 | OpenClaw | Hermes Agent | OpenHands SDK | Pi | LiteLLM |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **功能侧重** | 全能Agent框架，多通道集成 | 高性能Agent核心，本地模型优化 | 标准化 Agent 开发SDK | 终端原生 AI IDE 助手 | 通用模型 API 网关 / 代理 |
| **目标用户** | 社区开发者、重度自动化用户 | 模型研究者、性能追求者 | Agent 应用开发者 | 软件工程师、开发者 | 企业、开发者、模型供应商 |
| **技术架构** | 插件式、事件驱动，通道适配层厚 | 高性能核心，MoE优化，强耦合 | 标准化协议(ACP)，关注API设计 | 高质量终端UI，低延迟内核 | 轻量级反向代理，模型兼容性核心 |
| **核心痛点解决** | 社交通道消息丢失、记忆安全 | 首个令牌生成时间（TTFT）、竞态条件 | LLM响应处理不对称、并发控制 | 终端滚动、大文件CPU占用、企业兼容 | Python3.14支持、UI路由、代理兼容 |

#### **6. 社区热度与成熟度**

- **第一梯队 (快速迭代 / 成长型)**:
  - **OpenClaw, Hermes Agent**: 处于 **高速扩张** 阶段，社区贡献积极，但稳定性是当前最大挑战。它们正在从“能用”向“好用”演进，但频繁的回归问题表明成熟度仍有待提高。
  - **Pi**: 处于 **精益化打磨** 阶段，社区小而精，维护者响应迅速，用户体验是其绝对核心。成熟度较高，但对创新性功能的接纳度需观察。

- **第二梯队 (稳定发展 / 质量巩固型)**:
  - **LiteLLM**: 处于 **快速迭代与集成** 阶段，通过频繁发布新版本快速吸收社区贡献，但缺乏足够的质量控制，导致回归频发。
  - **Temporal**: 处于 **成熟稳健** 阶段，节奏稳定，专注于核心基础设施的可靠性。它是生态的“地基”，而非“上层建筑”。

- **第三梯队 (潜在风险 / 停滞型)**:
  - **OpenHands SDK**: 处于 **积压风险** 阶段。社区有提交意愿，但维护者审核效率低下，若不改变，可能会导致社区热情消退，项目边缘化。

#### **7. 值得关注的趋势信号**

1. **“安全门控”从防御走向强制执行**: 社区普遍认为，仅靠提示词（Prompt）来约束 Agent 行为是“软指令”，不可靠。**强制工具调用前检查、硬性的记忆信任标签** 等功能需求标志着 Agent 安全范式正在从“教育模型”向“架构约束”演进。
2. **会话状态持久化成为“刚需”**: 从多个项目的 Bug 和功能请求看，**会话丢失、上下文混乱** 是用户最痛的体验问题。未来，基于不可变事件日志（Event Sourcing）或更健壮的会话管理系统将具有巨大竞争力。
3. **“终端原生”成为差异化战场**: Pi 的快速崛起表明，**无缝、低延迟、高颜值的本地IDE体验** 是吸引开发者用户的关键。这提示全能型框架（如 OpenClaw）应考虑提供更优质的终端或桌面端参考实现。
4. **企业级需求在开源社区涌现**: LiteLLM 的“组织管理员无法查看全组织使用数据”、Pi 的“Copilot Enterprise 下无法压缩”等 Issue 表明，**预算管理、审计追踪、企业SSO集成** 等企业级功能正成为开源项目需要认真对待的“非功能需求”。
5. **MCP/ACP 协议标准化趋势初现**: LiteLLM 和 OpenHands SDK 对 MCP/ACP 的修复与支持，预示着 **Agent 工具与模型的调用接口正在走向标准化**。这将极大降低开发者接入不同模型和工具生态的成本。

---

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是为Hermes Agent项目生成的2026-07-20项目动态日报。

---

## Hermes Agent 项目动态日报 | 2026-07-20

### 1. 今日速览

今日项目活跃度**极高**。24小时内产生了500条Issue更新与500条PR更新，代码仓库与社区讨论均呈现出显著的脉冲式增长。尽管新版本发布数为0，但社区贡献者表现非常积极，针对大量会话状态（Session State）、多配置（Profiles）、性能及兼容性相关问题提交了修复方案。项目整体处于高强度的“修复与迭代”周期中，重点关注系统稳定性与极端故障场景的修复。

### 2. 版本发布

*今日无新版本发布*

---

### 3. 项目进展

今日合并/关闭的重要PR及项目整体推进：

- **核心性能优化**：PR [#67788](https://github.com/NousResearch/hermes-agent/pull/67788) 已被关闭并合并。该PR对每个API调用的关键路径进行了优化，移除了多余的base64重新序列化操作，预计将显著改善**首个令牌生成时间（TTFT）**，并为本地MoE模型用户带来直接性能提升。
- **关键Bug修复方向确立**：多个影响会话状态（Session State）的严重Bug已进入修复流程。例如，针对桌面端首个消息导致空白会话的Bug [#63078](https://github.com/NousResearch/hermes-agent/issues/63078) 以及桌面端因非默认配置创建新会话的Bug [#65384](https://github.com/NousResearch/hermes-agent/issues/65384) 已被关闭，表明相关修复已合并。针对会话切换后内容显示错乱的问题 [#62170](https://github.com/NousResearch/hermes-agent/issues/62170) 和 [#62726](https://github.com/NousResearch/hermes-agent/issues/62726)，均有对应的PR在推进中。
- **安全与兼容性加固**：PR [#67814](https://github.com/NousResearch/hermes-agent/pull/67814) 提升了项目中多个直接与间接依赖库的安全性，以应对已知的高危漏洞，并增加了回归测试覆盖。PR [#67779](https://github.com/NousResearch/hermes-agent/pull/67779) 修复了在Windows平台下`vision_analyze`功能无法正确处理`file:///` URI的问题，解决了跨平台兼容性痛点。
- **新功能集成**：PR [#67808](https://github.com/NousResearch/hermes-agent/pull/67808) 提议集成内置的VOICEVOX兼容TTS提供商，为语音相关功能提供了新的本地化选择，虽然仍在开放状态，但反映了项目在TTS能力上的扩展方向。

总体而言，项目在性能优化、关键Bug修复和跨平台/安全兼容性方面均取得了实质性进展。

---

### 4. 社区热点

今日讨论活跃度极高的Issues/PRs：

- [#4505 - Optimize Ollama Integration](https://github.com/NousResearch/hermes-agent/issues/4505) (13条评论)
  - **分析**：虽为4月提出的Issue，但今日获得了最高评论数。社区对Ollama集成的性能优化需求强烈，特别是希望利用Ollama原生`/api/chat`端点以获取更高效的流式传输。这反映了本地模型用户对交互体验和延迟的极致追求。
- [#64934 - Two turns can run concurrently on one gateway session](https://github.com/NousResearch/hermes-agent/issues/64934) (9条评论)
  - **分析**：这是一个已关闭的P0级严重Bug。揭示了Gateway会话在特定时序下会绕过繁忙检测，导致两个会话轮次并行执行，进而引发转录刷入混乱和永久性陷阱。社区的热烈讨论表明这是一个隐晦且破坏力极强的竞态条件问题，其修复对服务稳定性至关重要。
- [#3523 - hermes update regressions](https://github.com/NousResearch/hermes-agent/issues/3523) (8条评论)
  - **分析**：一个持续了近四个月的回归问题。用户对`hermes update`命令的体验非常敏感，即使是一个小问题（如Git输出静默、不必要的stash）也引发了大量关注，这提示CLI体验的稳定性是用户满意度的重要基础。
- [#40662 - PreToolUse enforcement hook](https://github.com/NousResearch/hermes-agent/issues/40662) (8条评论)
  - **分析**：用户深度反映了当前大模型的核心痛点——LLM在深度调试场景下极易偏离系统提示中的规则。社区热切希望项目能提供“强制”机制（如PreToolUse钩子）来确保模型行为始终符合预设的记忆和规则，而不仅仅是依赖模型自身的遵从性。

---

### 5. Bug 与稳定性

今日报告的Bug及稳定性问题，按严重度排列：

- **P0 (极高严重度)**:
  - [#4319 - KV cache invalidation on compression hurts local MoE models](https://github.com/NousResearch/hermes-agent/issues/4319): 本地MoE模型在长会话中因上下文压缩导致KV缓存失效，引起严重性能下降。项目已存在`area/compression`相关PR [#27579](https://github.com/NousResearch/hermes-agent/issues/27579) 提议空闲触发压缩，可能为解决此问题提供了方向。
  - [#64934 - Two turns run concurrently on a gateway session](#)（已修复，但问题本身具有P0严重性）

- **P1 (高严重度)**:
  - [#30387 - hermes -z aborts with exit 134](https://github.com/NousResearch/hermes-agent/issues/30387): CLI单次请求模式`-z`在成功响应后，进程关闭时崩溃。这会导致Shell脚本误判任务失败。

- **P2 (中高严重度)**:
  - [#67600 - Desktop session sidebar empty for default profile](https://github.com/NousResearch/hermes-agent/issues/67600): 桌面端`default`配置文件的会话列表为空，但后台数据正常。该Bug已被复现，与配置/Profile系统相关。
  - [#67012 - keepalive_expiry=20s breaks streaming via Cloudflare/OpenRouter](https://github.com/NousResearch/hermes-agent/issues/67012): 特定版本引入的`keepalive_expiry`配置导致通过Cloudflare代理的流式连接异常中断，影响海外用户的使用。
  - [#67277 - Webhook multiplexing loads default profile's skills](https://github.com/NousResearch/hermes-agent/issues/67277): Webhook多路复用功能在解析URL中的Profile后，未能正确加载对应Profile的Skills，导致功能错乱。
  - [#63078 - First message leaves a blank session](https://github.com/NousResearch/hermes-agent/issues/63078) (已修复)
  - [#65384 - Desktop creates new session on every message](https://github.com/NousResearch/hermes-agent/issues/65384) (已修复)

**当前已有关联Fix PR的活跃Bug**:
- [#46593 - kanban: worker exits rc=0 without calling kanban_complete](https://github.com/NousResearch/hermes-agent/issues/46593) (P3)
- [#59386 - delegate_task schema causes HTTP 400](https://github.com/NousResearch/hermes-agent/issues/59386) (P2)
- [#62170 - TUI shows stale session content](https://github.com/NousResearch/hermes-agent/issues/62170) (P2)
- [#62726 - Dashboard cross-tab session bleed](https://github.com/NousResearch/hermes-agent/issues/62726) (P2)
- [#67187 - MCP server reconnects but does not re-register tools](https://github.com/NousResearch/hermes-agent/issues/67187) (P2)

---

### 6. 功能请求与路线图信号

今日提出的核心功能请求及路线图信号：

- **会话上下文共享**：[#4335 - Cross-platform session context sharing](https://github.com/NousResearch/hermes-agent/issues/4335) 和 [#27013 - Agents lose project context across session restarts](https://github.com/NousResearch/hermes-agent/issues/27013) 反映了用户对**会话连续性和上下文穿透性**的强烈需求。用户期望Agent能够跨平台、跨生命周期地记住并理解项目背景，而非每次重启都“失忆”。这与项目`area/sessions`和高级记忆功能直接相关。
- **认知记忆操作**：[#509 - Cognitive Memory Operations](https://github.com/NousResearch/hermes-agent/issues/509) 是一个由创始人提出的长期功能请求，旨在为记忆系统增加LLM驱动的编码、整合、自适应回忆和矛盾检测能力。今日仍获得社区共鸣，表明这是用户公认的“下一代”核心能力。
- **强制执行钩子**：[#40662 - PreToolUse enforcement hook](https://github.com/NousResearch/hermes-agent/issues/40662) 和 [#25061 - pre-turn memory health hook](https://github.com/NousResearch/hermes-agent/issues/25061) 均指向同一诉求：由于LLM的**近因偏差**，需要系统级别的“强制执行点”来确保记忆规则和系统提示不被忽略。
- **与外部知识库集成**：[#2736 - Obsidian Vault as Persistent Shared Memory](https://github.com/NousResearch/hermes-agent/issues/2736) 建议将Obsidian笔记库作为持久化的共享内存层。这代表了将AI Agent与用户个人知识管理系统深度融合的用例。
- **Idle-Triggered Context Compression**：[#27579 - Idle-triggered context compression](https://github.com/NousResearch/hermes-agent/issues/27579) 提议在用户空闲时后台进行上下文压缩，以避免在用户下次输入时产生“预飞”延迟。这是对现有压缩机制（仅在token超限时触发）的一次关键优化。

**路线图信号**：上述功能（如跨平台会话、强制执行钩子、丰富的记忆操作）与当前`area/sessions`、`area/memory`标签下的多个Issue和PR相呼应，有望成为下一版本的核心特性。

---

### 7. 用户反馈摘要

- **对桌面端和CLI稳定性不满**：用户反馈显示桌面端（Electron）和CLI工具在更新或特定操作后，容易出现会话异常（空白、错乱、创建新会话）和进程崩溃等问题，这严重破坏了核心工作流，用户期望更高的稳定性。
- **对模型“创造力”的问责**：用户对LLM在关键任务（如调试）中“不听话”（Ignoring System Prompt）感到沮丧。他们希望项目层面提供**机制性保证**，而非依赖模型本身的随机行为。
- **本地模型用户对性能敏感**：Ollama集成优化的Issue（#4505）和MoE模型KV缓存问题（#4319）表明，本地模型用户非常关注**延迟和效率**，期望有更专门的硬件级或协议级优化。
- **欢迎安全与兼容性改进**：社区对依赖库版本提升（#67814）和跨平台BUG修复（#67779）给出了积极信号，认为这是项目健康发展的基石。

---

### 8. 待处理积压

- **[#509 - Cognitive Memory Operations](https://github.com/NousResearch/hermes-agent/issues/509)** (创建于2026-03-06, P3): 由创始人提出，社区反应热烈（6条评论，4个👍）。这是一个重大的功能特性，但至今无Assignee，长期处于开放状态。建议项目维护者评估将其纳入下一阶段路线图的可行性。
- **[#2736 - Obsidian Vault as Persistent Shared Memory](https://github.com/NousResearch/hermes-agent/issues/2736)** (创建于2026-03-24, P3): 用户明确指出了`obsidian_vault:`配置项已存在但无代码读取的问题。这阻碍了一个深受欢迎的个人知识用例，需要开发人员关注并实现这个“已预留”的接口。
- **[#3523 - hermes update regressions](https://github.com/NousResearch/hermes-agent/issues/3523)** (创建于2026-03-28, P2): 已开放数月的CLI回归问题，虽非功能阻断，但社区活跃度高，反映出频繁反馈此问题的用户群体。长期未能修复可能削弱用户对新版本更新的信任。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 OpenHands SDK 项目数据，为您生成一份专业、客观、数据驱动的 2026-07-20 项目动态日报。

---

# OpenHands SDK 项目动态日报 | 2026-07-20

## 1. 今日速览

本日项目整体处于 **中度活跃** 状态。社区贡献热情较高，共提交了 34 个 Pull Request (PR)，但均处于待合并状态，且无任何已合并或关闭的 PR/Issue，显示出项目维护节奏有所放缓，存在 **“重提交、轻合并”的积压趋势**。Bug 报告数量较多（13 个新 Issue 均为活跃状态），主要集中在 SDK 核心逻辑、LLM 交互及 Agent 控制流方面，部分由社区贡献者提出的修复性 PR 正在等待审查合并。无新版本发布。

## 2. 版本发布

*(无)*

## 3. 项目进展

**关键进展:** 尽管今日未有 PR 被合并，但多个重要的功能性和修复性 PR 在今日获得了更新并等待合并，标志着项目在多条关键线路上取得了实质性的进展。

- **核心 SDK 功能增强:**
    - **PR #4066 (feat(sdk): support conversation-scoped LLM headers):** 引入了对话级别的 LLM 头部支持，允许在单个 Agent 运行过程中传播请求 ID 等自定义头部，避免对全局 LLM 配置的修改。
    - **PR #4147 (feat(tool): add structured outcome to FinishAction for infeasible tasks):** 为 `FinishAction` 添加了结构化结果，使 Agent 在面临无法完成的任务时，能向编排器发送明确的错误或未完成信号，增强了构建全自主 Agent 的能力。
- **安全与稳定性:**
    - **PR #3944 (feat(security): AST-backed shell command-name resolution):** 旨在解决由正则表达式引起的 shell 指令检测绕过漏洞，通过引入抽象语法树 (AST) 进行解析，提升了命令安全检测的鲁棒性。
    - **PR #4153 (fix(llm): allow security_risk param on read-only tools like finish):** 修复了 LLM 在调用 `finish` 等只读工具时，因 `security_risk` 参数产生错误输出的问题，提升了 LLM 兼容性。
- **错误修复与优化:**
    - **PR #4035 (fix(conversation): read persisted base_state.json as UTF-8 on resume):** 修复了因未指定 UTF-8 编码读取状态文件而导致的潜在兼容性问题。
    - **PR #4003 (fix: normalize content to "" instead of dropping it for assistant too...):** 针对部分 LLM (如 Gause) 因 `content=null` 而返回 HTTP 422 错误的问题进行了修复，优化了兼容性。

**小结:** 项目在安全加固、LLM 兼容性、Agent 控制力等关键方面均有修复和新功能等待落地，显示出社区的活跃贡献度。但核心维护者的审查和合并压力较大。

## 4. 社区热点

本日讨论最活跃的议题集中在 **LLM 兼容性与响应处理** 和 **项目核心架构** 上。

- **#3992 - Asymmetric handling of content-without-tool-call responses** ([链接](https://github.com/OpenHands/software-agent-sdk/issues/3992))
    - **热度:** 6条评论
    - **诉求:** 用户反映 SDK 对无工具调用的 LLM 回复处理不对称，会导致弱模型驱动的 Agent 执行中断。这是在追求模型多样性与开发体验之间矛盾的典型体现，反映出社区对**更包容、更鲁棒的 LLM 响应处理机制**的迫切需求。
- **#4063 - max_concurrent_runs does not limit native async conversations** ([链接](https://github.com/OpenHands/software-agent-sdk/issues/4063))
    - **热度:** 6条评论
    - **诉求:** 这是一个严重的设计缺陷。`max_concurrent_runs` 配置项不能限制原生异步对话的并发，导致并发控制机制形同虚设，可能引发资源耗尽和服务不稳定。这直接关系到 **生产环境下的稳定性和资源管理**。
- **#1787 - Proposal: Fork conversation when tools change** ([链接](https://github.com/OpenHands/software-agent-sdk/issues/1787))
    - **热度:** 22条评论（长期活跃）
    - **诉求:** 关于在对话中增删工具时，应“分叉（fork）”对话而非修改原有对话的提案。此历史 Issue 讨论依旧热烈，反映了社区对**不可变事件日志**和**更安全、可追溯的 Agent 状态管理**的深度关切。

## 5. Bug 与稳定性

今日报告了 13 个活跃 Bug，按严重程度排列如下：

- **严重 (Critical):**
    - **#4080 - One unregistered event kind fails the entire conversation load** ([链接](https://github.com/OpenHands/software-agent-sdk/issues/4080)): 单个事件反序列化失败会导致整个对话加载失败。**无关联 Fix PR**。
    - **#4063 - max_concurrent_runs does not limit native async conversations** ([链接](https://github.com/OpenHands/software-agent-sdk/issues/4063)): 并发控制失效。**无关联 Fix PR**。

- **中等 (Major):**
    - **#4107 - TaskToolSet does not propagate parent interruption to active subagents** ([链接](https://github.com/OpenHands/software-agent-sdk/issues/4107)): 父任务中断无法传递子 Agent，导致状态不一致。**无关联 Fix PR**。
    - **#4093 - ACP 0.11 drops Gemini model state from NewSessionResponse** ([链接](https://github.com/OpenHands/software-agent-sdk/issues/4093)): ACP 库版本升级导致与 Gemini CLI 的兼容性断裂。**无关联 Fix PR**。
    - **#4052 - fix(settings): restore MCP schema migration** ([链接](https://github.com/OpenHands/software-agent-sdk/issues/4052)): MCP 配置迁移未正确执行，影响现有用户。**已有修复 PR #4013**。

- **一般 (Minor):**
    - **#4133 - WindowsTerminal does not submit multiline PowerShell commands** ([链接](https://github.com/OpenHands/software-agent-sdk/issues/4133)): Windows 平台下多行 PowerShell 命令执行超时。**无关联 Fix PR**。
    - **#4098 - Avoid unauthenticated model-info lookup for managed OpenHands models** ([链接](https://github.com/OpenHands/software-agent-sdk/issues/4098)): 无 API Key 时仍会发起不必要的模型信息查询。**无关联 Fix PR**。

## 6. 功能请求与路线图信号

- **#4130 - Feature: search_tool** ([链接](https://github.com/OpenHands/software-agent-sdk/issues/4130)): 随着 MCP 工具数量增长，系统提示（System Prompt）变得臃肿。用户提议引入 `search_tool` 的概念，以动态发现和调用工具。这可能会成为 **下一版本核心重构的信号**，旨在解决 Agent 的工具发现与上下文窗口管理问题。
- **#1787 - Proposal: Fork conversation when tools change** ([链接](https://github.com/OpenHands/software-agent-sdk/issues/1787)): 此提案若被采纳，将根本性地改变 `Conversation` 的生命周期管理，是 **仓库设计方向的重大信号**。
- **#2371 - feat: add per-MCP server graceful degradation** ([链接](https://github.com/OpenHands/software-agent-sdk/pull/2371)): 该长期开放的 PR 正是为了解决 MCP 服务器单点故障导致整个系统启动失败的问题。它与 #4130 的 `search_tool` 需求相辅相成，共同指向 **MCP 生态的健壮性** 将是下一阶段的重点。

## 7. 用户反馈摘要

从本周期的 Issues 评论中，可以提炼出以下用户痛点和使用场景：

- **“弱模型”兼容性痛点 (#3992)**: 用户反映，当使用功能较弱的本地模型时，SDK 对 LLM 响应的严格处理逻辑会导致 Agent 频繁中断，这严重影响了低资源场景下的用户体验。**用户期望 SDK 在处理各种 LLM 输出时能更宽容、更健壮**。
- **配置管理混乱 (#4019, #4052)**: 用户报告 ACP 配置文件中，项目技能（Project Skills）的注入逻辑导致配置重复 (#4019)。同时，MCP 配置迁移的 Bug 导致用户已有的配置不生效 (#4052)。**用户对 SDK 配置模块的稳定性和清晰度感到困扰**。
- **并发控制失效 (#4063)**: 用户发现 `max_concurrent_runs` 设置不生效，这可能导致生产环境下的资源瓶颈。**用户需要一个真正可靠的控制机制来管理 Agent 服务的并发负载**。

## 8. 待处理积压

以下 PR 和 Issue 已长期挂起且极其重要，强烈建议项目维护者优先关注：

- **PR #2371 - feat: add per-MCP server graceful degradation** ([链接](https://github.com/OpenHands/software-agent-sdk/pull/2371)): 创建于 3 月，旨在提升 MCP 的健壮性，是解决生产环境高可用问题的关键。当前评论数未知，但无合并进展。
- **PR #2363 - refactor(llm): add LiteLLM-backed provider abstraction** ([链接](https://github.com/OpenHands/software-agent-sdk/pull/2363)): 创建于 3 月，为 LLM 配置管理提供根本性的架构抽象。此 PR 的合并被多次提及为其他功能的基础，但至今仍为开放状态。
- **Issue #4080 - One unregistered event kind fails the entire conversation load** ([链接](https://github.com/OpenHands/software-agent-sdk/issues/4080)): 一个严重 Bug，会导致用户数据完全丢失在 UI 中，影响面极大，目前无任何修复关联。

**总结:** 项目社区活跃度（提交 PR 和 Bug 报告）很高，但维护端的合并与发布流程似乎遇到了瓶颈。多个关键架构重构和严重的稳定性 Bug 处于长期待处理状态，这需要项目维护者投入更多精力进行审查和合并，以避免社区贡献热情的流失和项目健康度的下滑。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，以下是根据您提供的 Pi 项目 GitHub 数据生成的 2026-07-20 项目动态日报。

---

# Pi 项目动态日报 | 2026-07-20

## 今日速览

今日项目活动密集，社区反馈处理效率极高。过去24小时内，共有 **32 条 Issue 更新**，其中 **29 条被关闭**，仅 3 条新开或活跃，显示维护者对问题的响应和修复非常迅速。PR 方面同样高效，9 条 PR 中 **8 条已合并/关闭**，仅有 1 条待处理。尽管没有新版本发布，但项目在 Bug 修复和功能引入上均有实质性进展。整体来看，项目处于 **高活跃、高响应** 的健康状态，维护者正积极解决社区反馈的稳定性、性能及兼容性问题。

## 项目进展

今日项目核心进展集中在模型兼容性、核心错误处理和功能扩展上。一共合并了 **8 个 PR**，主要亮点包括：

- **修复了因 `assistant.usage` 可能为 `undefined` 导致的会话崩溃问题** ([PR #6818](https://github.com/earendil-works/pi/pull/6818))。此问题会直接导致使用 DeepSeek V4 等部分提供商的会话永久损坏，修复后大幅提升了核心稳定性。
- **新增 Upstage (Solar LLMs) 作为内置提供商** ([PR #6824](https://github.com/earendil-works/pi/pull/6824), [PR #6823](https://github.com/earendil-works/pi/pull/6823))，为用户提供了更多开箱即用的模型选项，降低了配置门槛。
- **对齐 GPT-5.6 Codex 上下文窗口** ([PR #6837](https://github.com/earendil-works/pi/pull/6837))，将默认上下文窗口调整为 272K，与官方客户端保持一致，避免因错误配置导致的成本和性能问题。
- **统一了 UUIDv7 生成逻辑，并用于 Codex 提供商** ([PR #6834](https://github.com/earendil-works/pi/pull/6834))，有助于改善请求追踪和日志排查。
- **OpenCode Go 模型兼容性修复** ([PR #6828](https://github.com/earendil-works/pi/pull/6828))，确保了对 Grok 4.5 模型的支持。
- **新增共享的 `contentText` 工具函数** ([PR #6840](https://github.com/earendil-works/pi/pull/6840))，为代码复用和统一文本处理提供基础设施。
- **ACP模式（Agent Client Protocol）功能合入主线** ([PR #836](https://github.com/earendil-works/pi/pull/836))，这意味着 Pi 现在能够集成支持 ACP 协议的编辑器（如 Zed、JetBrains IDE），是项目连接开发者生态的重要一步。

## 社区热点

今日社区讨论热度最高的问题集中在用户体验和核心功能上：

1. **终端无故滚动问题** ([#5023](https://github.com/earendil-works/pi/issues/5023)): 这是今日评论数最多（9条）的 Issue，尽管已关闭，但反映了用户对终端交互稳定性的高度关注。用户报告在模型工作时终端会“随机”跳动，严重干扰阅读体验。
2. **模型选择器无法处理含括号的ID** ([#6210](https://github.com/earendil-works/pi/issues/6210)): 此问题为 OPEN 状态，评论数8条，是当前最活跃的讨论。用户期望 `scoped-models` 命令能正确匹配 `custom/bracketed-model[1m]` 这类 ID，但由于括号被解析为特殊字符而失败，暴露了输入解析的局限性。
3. **高CPU占用问题** ([#6792](https://github.com/earendil-works/pi/issues/6792)): 用户反馈在编辑大文件（500+行）时 CPU 占用达到 100%，这是一个严重影响生产力的性能问题，关闭速度很快，说明团队已经或正在处理。
4. **Copilot Enterprise 下无法压缩（Compaction）** ([#6768](https://github.com/earendil-works/pi/issues/6768)): 获得2个👍，是企业级用户报告的集成问题，也可能与未来类似特性有关。

**社区诉求分析**: 用户的核心诉求非常集中：**交互稳定性**（终端滚动）、**功能可用性**（模型选择器）、**性能**（高CPU占用）和**企业兼容性**（Copilot）。维护者对这些问题普遍给予了快速响应。

## Bug 与稳定性

今日报告的 Bug 较多，按严重程度排列如下：

- **致命/崩溃级**:
  - **内存泄漏导致系统崩溃 (CRITICAL)** ([#6841](https://github.com/earendil-works/pi/issues/6841)): 长时间运行的会话内存不受控增长，最终导致系统 Swap 抖动和进程卡死。这是当前最严重的稳定性问题，需要优先排查。**（无修复PR）**
  - **`assistant.usage` 为 `undefined` 导致会话永久崩溃 (CRITICAL)** ([#6819](https://github.com/earendil-works/pi/issues/6819)): 已通过 **[PR #6818](https://github.com/earendil-works/pi/pull/6818)** 修复。
  - **孤儿 toolResult 导致 `400` 错误 (CRITICAL)** ([#6832](https://github.com/earendil-works/pi/issues/6832)): 回归问题，会导致会话“永久不可恢复”。需关注是否修复彻底。**（无修复PR）**

- **重要/功能受损级**:
  - **高CPU占用（大文件编辑）(HIGH)** ([#6792](https://github.com/earendil-works/pi/issues/6792)): 已关闭，表明已修复或定位。
  - **升级(`pi update`)单次网络失败即放弃 (HIGH)** ([#6675](https://github.com/earendil-works/pi/issues/6675)): 影响了用户升级的体验和成功率。**（无修复PR）**
  - **`find` 工具在 Windows 上匹配路径模式失败 (HIGH)** ([#6817](https://github.com/earendil-works/pi/issues/6817)): 影响 Windows 用户的文件搜索功能，破坏性较大。**（无修复PR）**
  - **`--system-prompt` 标志无效 (HIGH)** ([#6825](https://github.com/earendil-works/pi/issues/6825)): 核心功能失效。已关闭，可能已修复。

- **一般/阻碍级**:
  - **会话恢复后模型选择错误 (MEDIUM)** ([#6822](https://github.com/earendil-works/pi/issues/6822)): 无声地覆盖用户模型选择。
  - **并行启动锁竞争导致误导性鉴权错误 (MEDIUM)** ([#1871](https://github.com/earendil-works/pi/issues/1871)): 老问题，需要评估修复计划。
  - **`SessionManager.open()` 不必要的文件读取导致性能问题 (LOW)** ([#6793](https://github.com/earendil-works/pi/issues/6793)): 已关闭，应为已修复。

## 功能请求与路线图信号

今日涌现了多种功能请求，结合已有 PR 可捕捉到一些路线图信号：

- **扩展性与集成**:
  - **支持 ACP 模式** ([PR #836](https://github.com/earendil-works/pi/pull/836)): **已合并**。这是迈向深度编辑器集成的关键一步。
  - **远程容器/SSH 支持** ([#5341](https://github.com/earendil-works/pi/issues/5341)): 呼声很高，是扩展使用场景的关键。
  - **新的 LLM 提供商 (Upstage, OpenCode Go)** ([PR #6824](https://github.com/earendil-works/pi/pull/6824), [PR #6828](https://github.com/earendil-works/pi/pull/6828)): **已合并**。这表明项目正在积极扩大模型选择范围。
  - **为扩展提供“批量工具调用”的钩子 (Batch Hook)** ([#6816](https://github.com/earendil-works/pi/issues/6816)): 开发者用户希望获得更细粒度的控制能力。

- **用户体验优化**:
  - **可隐藏的滚动导航帮助** ([#6833](https://github.com/earendil-works/pi/issues/6833)): 用户希望界面更简洁。
  - **可配置的文本读取行数限制** ([#6835](https://github.com/earendil-works/pi/issues/6835)): 开发者的灵活性需求。
  - **新手友好的本地模型连接配置** ([#6305](https://github.com/earendil-works/pi/issues/6305)): 降低使用门槛是长期任务。
  - **`/retry` 手动重试命令** ([#6810](https://github.com/earendil-works/pi/issues/6810)): 用户希望在自动重试耗尽后有机会手动干预。

**路线图信号**: 项目正聚焦于 **扩展 AI 提供商生态**、**提升核心稳定性**（特别是长会话和内存管理）以及 **连接更广泛的开发者工具生态**（通过 ACP）。用户对 **可观测性**（如重试生命周期）和 **自定义能力**的需求也在增长。

## 用户反馈摘要

从今日的 Issues 中可以提炼出以下真实用户痛点：

- **性能与稳定性是核心痛点**: 用户抱怨“100% CPU usage” ([#6792](https://github.com/earendil-works/pi/issues/6792)) 和“无法在16GB机器上运行多个长会话” ([#6841](https://github.com/earendil-works/pi/issues/6841))，这严重影响了开发工作流。有用户直接将此描述为 “swap thrashing”。
- **配置复杂与易用性**: 新用户会感到配置本地模型很困难，希望“automatic discovery” ([#6305](https://github.com/earendil-works/pi/issues/6305))。
- **企业环境兼容性**: “Copilot Enterprise 用户无法使用压缩功能” ([#6768](https://github.com/earendil-works/pi/issues/6768))，反映了企业级用户在特定网络或鉴权环境下的障碍。
- **用户对 Bug 修复的迫切性**: 对于 `--system-prompt` 不生效的问题，用户给出了详细的复现步骤，表明用户是重度使用者，且对核心功能的可靠性有很高期待。
- **对回归问题的沮丧**: “[#6832](https://github.com/earendil-works/pi/issues/6832) 是 #4570 的回归” 这类反馈表明，用户会主动追踪旧 Bug，对稳定性的要求极高。

## 待处理积压

- **`pi update --self` 失败无重试** ([#6675](https://github.com/earendil-works/pi/issues/6675)): 创建于7月15日，至今无维护者回应或 PR。这是一个相对简单但影响升级体验的关键问题。
- **`/scoped-models` 无法选择含括号ID** ([#6210](https://github.com/earendil-works/pi/issues/6210)): 已活跃超过两周，目前为 OPEN 状态且讨论较多，需要明确是设计限制还是 Bug，并给出解决方案。
- **Tab 补全后无法触发参数补全** ([#5593](https://github.com/earendil-works/pi/issues/5593)): 6月10日创建，标记为 `inprogress`，但近期无更新。这是一个影响日常命令行交互的 Bug，亟待跟进。
- **远程容器/SSH 支持** ([#5341](https://github.com/earendil-works/pi/issues/5341)): 作为一项长期功能请求，虽未标记为 `inprogress`，但多次被提及，建议维护者评估其在路线图中的优先级。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-07-20

---

## 1. 今日速览

过去24小时项目保持高活跃度：共更新 **39 条 Issue**（新开/活跃 28，关闭 11）和 **103 条 PR**（待合并 75，合并/关闭 28），并发布 **4 个小版本**（v1.90.6 → v1.93.0）。社区关注焦点集中在 **Python 3.14 支持回归**、**UI 路由 404 问题** 以及 **MCP 服务器配置兼容性** 上。PR 合并速度较快，但仍有 **75 个 PR 处于待合并状态**，积压压力有所增加。整体项目在持续迭代修复与功能扩展，稳定性需重点关注。

---

## 2. 版本发布

今日发布了 4 个新版本（v1.90.6, v1.91.4, v1.92.1, v1.93.0），均为补丁级别。Release Notes 仅统一说明了 Docker 镜像签名验证方式（使用 cosign），未提供具体变更日志。建议用户升级前查看 [GitHub Releases 页面](https://github.com/BerriAI/litellm/releases) 获取详细改动。  
**⚠️ 注意事项**：v1.92.0+ 的 Anthropic 代理存在不兼容问题（详见 Bug 部分），如使用 Anthropic 格式的推理请暂缓升级至 v1.92.x。

---

## 3. 项目进展

今日共合并/关闭 **28 个 PR**，涵盖性能优化、UI 修复、适配器增强和稳定性改进。重点合并如下：

| PR | 摘要 | 状态 |
|----|------|------|
| [#23421](https://github.com/BerriAI/litellm/pull/23421) | 修复 UI 使用量页面中 OpenAI 模型缓存令牌始终显示为零的问题 | 已合并 |
| [#24418](https://github.com/BerriAI/litellm/pull/24418) | 为 Anthropic 和 Google GenAI 直通端点添加同步流适配器 | 已合并 |
| [#25086](https://github.com/BerriAI/litellm/pull/25086) | 修复仓库级格式和 lint 问题 | 已合并 |
| [#25476](https://github.com/BerriAI/litellm/pull/25476) | 修复 Anthropic→OpenAI 格式转换中工具结果图像块丢失 | 已合并 |
| [#25565](https://github.com/BerriAI/litellm/pull/25565) | 修复 `aspeech`/`atranscription` 双次调用、`get_running_loop` 瓶颈及异步流缓存问题 | 已合并 |
| [#25617](https://github.com/BerriAI/litellm/pull/25617) | 修复组织管理员在 UI 中无法查看全组织使用数据的问题 | 已合并 |
| [#25639](https://github.com/BerriAI/litellm/pull/25639) | 为 Redis 消费计数器设置 30 天 TTL，防止内存泄漏 | 已合并 |
| [#25648](https://github.com/BerriAI/litellm/pull/25648) | 允许 OVH 音频转录在 verbose_json 格式下返回 `segments` 和 `language` | 已合并 |
| [#25654](https://github.com/BerriAI/litellm/pull/25654) | 修复 aiohttp 传输层超时被默认 300 秒限制的问题 | 已合并 |

这些 PR 推进了 **UI 准确性、代理兼容性、性能与内存管理** 的改进。此外，仍有 **75 个待合并 PR**，包括路由优化、预算管理、Web 搜索拦截等，预计未来几天会持续合并。

---

## 4. 社区热点

| Issue/PR | 热度指标 | 核心诉求 |
|----------|---------|----------|
| [#26343](https://github.com/BerriAI/litellm/issues/26343) Support Python 3.14 | 15 评论，30 👍 | 用户反馈 1.83.7 版本曾支持 Python 3.14，后续版本却移除了支持，要求重新加入 |
| [#24037](https://github.com/BerriAI/litellm/issues/24037) `/ui/chat` 返回 404 | 5 评论，26 👍 | UI 子路由（chat/logs/models）在静态导出后全部失效，影响网页端访问 |
| [#26056](https://github.com/BerriAI/litellm/issues/26056) `litellm[proxy]` 安装失败 | 7 评论，3 👍 | Python 3.14 环境下 `orjson` 构建失败，导致无法安装代理组件 |
| [#18169](https://github.com/BerriAI/litellm/issues/18169) `static_headers` 被 MCP 服务器忽略 | 6 评论，1 👍 | 基于 OpenAPI 的 MCP 服务器配置无法携带自定义标头，影响需要认证的 API 连接 |
| [#32335](https://github.com/BerriAI/litellm/issues/32335) `/responses` API 推理项丢失 | 4 评论 | v1.83.7 升级后，Azure OpenAI 的多轮对话中推理内容被丢弃，导致 400 错误 |

分析：社区对 **Python 3.14 兼容性** 的呼声最高，该特性曾被实现后被撤回，目前尚无明确路线图。**UI 404 问题** 影响大量使用仪表盘的用户，急需修复。**MCP 和 Anthropic 代理** 的兼容性问题是当前集成企业工具链的主要痛点。

---

## 5. Bug 与稳定性

按严重程度排列，标注是否已有 Fix PR 或修复版本：

| 严重程度 | Issue | 问题描述 | Fix 状态 |
|---------|-------|---------|----------|
| 🔴 严重 | [#33824](https://github.com/BerriAI/litellm/issues/33824) | v1.92.0+ 中 Anthropic 代理 `/v1/messages` 不兼容，Claude CLI 集成失败 | 未发现对应 Fix PR |
| 🔴 严重 | [#32335](https://github.com/BerriAI/litellm/issues/32335) | `/responses` API 在多轮对话中丢失推理内容，v1.83.7 回归 | 未发现对应 Fix PR |
| 🟠 高 | [#33764](https://github.com/BerriAI/litellm/issues/33764) | 转录 `response_format=json` 导致 Pydantic 校验失败，影响 SDK 和代理 | 未发现对应 Fix PR |
| 🟠 高 | [#25553](https://github.com/BerriAI/litellm/issues/25553) | `update_cache` 在缓存失效后复活陈旧密钥，绕过 `/key/update` 更改（已关闭，可能已修复） | 已关闭 |
| 🟠 高 | [#33941](https://github.com/BerriAI/litellm/issues/33941) | `/customer/update` 静默丢弃 `budget_duration` 当终端用户无现有预算时 | 未发现对应 Fix PR |
| 🟡 中 | [#33923](https://github.com/BerriAI/litellm/issues/33923) | `fail_closed_budget_enforcement` 在原子预算预留失败时不拒绝请求 | 未发现对应 Fix PR |
| 🟡 中 | [#33871](https://github.com/BerriAI/litellm/issues/33871) | 项目费用从未被追踪，导致项目预算和告警不生效 | 未发现对应 Fix PR |
| 🟢 低 | [#26113](https://github.com/BerriAI/litellm/issues/26113) | `remove_custom_field_from_tools()` 移除 `defer_loading`，导致 Bedrock 工具搜索浪费令牌 | 未发现对应 Fix PR |

**回归问题突出**：v1.83.7 和 v1.92.0+ 均引入了关键回归，建议维护者优先排查并发布热修复。

---

## 6. 功能请求与路线图信号

| Issue | 功能描述 | 社区支持 | 可能的路线图信号 |
|-------|---------|---------|----------------|
| [#26343](https://github.com/BerriAI/litellm/issues/26343) | 重新支持 Python 3.14 | 30 👍，15 评论 | 高优先级，但需解决 `orjson` 等依赖兼容性 |
| [#24393](https://github.com/BerriAI/litellm/issues/24393) | `gemini-embedding-2-preview` 多模态嵌入支持 | 5 评论 | 潜力较大，Google 新模型需求增长 |
| [#29367](https://github.com/BerriAI/litellm/issues/29367) | 添加 FunASR 作为音频转录提供商 | 3 评论 | 社区贡献可能性高，需评估许可证 |
| [#33916](https://github.com/BerriAI/litellm/issues/33916) | 在模型价格表中添加 Claude Gemma 系列 | 1 评论 | 例行更新，预计很快合并 |
| [#26079](https://github.com/BerriAI/litellm/issues/26079) | `/spend/logs/v2` 增加 `model_group` 过滤 | 1 评论 | 企业用户常见需求，易于实现 |
| [#26093](https://github.com/BerriAI/litellm/issues/26093) | 禁止 SEP-986 MCP 工具名称前缀的选项 | 1 评论 | MCP 集成场景特定需求 |

目前项目组尚未对上述功能请求做出公开承诺，但 Python 3.14 支持和多模态嵌入是短期内最可能被优先处理的。

---

## 7. 用户反馈摘要

从今日活跃的 Issue 评论中，提炼出以下真实用户痛点：

- **Python 3.14 支持反复**：用户 @Jxlle 指出 v1.83.7 曾支持，后续版本“静默移除”支持，导致无法在新环境部署。多位用户表达失望。
- **UI 界面稳定性**：@nestorcolt 反映 `/ui/chat` 等子路由在静态导出下全部 404，认为这是一个“严重的问题”，影响日常使用。
- **代理不兼容**：@dota20505 反馈 v1.92.0 之后 Anthropic 代理失效，导致 Claude CLI 无法通过 LiteLLM 转发到其他模型，开发流程中断。
- **预算与费用管理失效**：@emerzon 报告项目预算“从未被追踪”，团队无法有效控制成本；@impr3ssi0n 发现 `/customer/update` 静默丢弃 `budget_duration`，导致预算设置无效。
- **缓存与性能困惑**：@dkindlund 描述了一个罕见的缓存复活陈旧密钥的 bug，该问题虽已关闭但用户表示“花了数小时调试”。

总体而言，用户对 LiteLLM 的功能深度和扩展性认可度较高，但对 **版本迭代中的回归** 和 **配置一致性** 存在不满。

---

## 8. 待处理积压

以下为长期未闭环的重要 Issue 或 PR，可能影响项目健康度，提醒维护者关注：

| 类型 | 编号 | 标题 | 创建时间 | 最后更新 | 说明 |
|------|------|------|---------|---------|------|
| Issue | [#15360](https://github.com/BerriAI/litellm/issues/15360) | Bulk inserts 导致 Postgres 执行计划重复（随机列序） | 2025-10-09 | 2026-07-19（已关闭） | 虽已关闭，但根本原因（Prisma bug）未解决，可能复发 |
| Issue | [#18169](https://github.com/BerriAI/litellm/issues/18169) | `static_headers` 被 MCP 服务器忽略 | 2025-12-18 | 2026-07-20（已关闭） | 已关闭但未提供最终解决方案说明 |
| PR | [#23924](https://github.com/BerriAI/litellm/issues/23924) | 修复 least-busy 路由总是选择同一部署 | 2026-03-18 | 2026-07-20 (OPEN) | 4 个月未合并，路由性能关键修复 |
| PR | [#25560](https://github.com/BerriAI/litellm/issues/25560) | 支持单独成员预算的 `budget_duration` 设置 | 2026-04-11 | 2026-07-20 (OPEN) | 3 个月未合并，预算管理核心功能 |
| PR | [#25722](https://github.com/BerriAI/litellm/issues/25722) | Web 搜索拦截默认启用所有提供商 | 2026-04-14 | 2026-07-20 (OPEN) | 影响 Web 搜索功能的多模型支持 |
| Issue | [#23924](https://github.com/BerriAI/litellm/issues/23924)（同名 PR）| 同上 | 2026-03-18 | 2026-07-20 | 长时间未响应，需 Code Review |

建议维护者对超过 **3 个月未合并的 PR** 进行优先级评估，对 **关键回归 issue** 分配责任人并制定修复时间线。

---

*本日报由 AI 自动生成，基于 2026-07-20 的 GitHub 公开数据。所有链接已内嵌至标题中。*

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 开源项目日报 — 2026-07-20

## 1. 今日速览

- 项目今日活跃度中等，24小时内新增/活跃 Issue 1 条，新增/更新 PR 7 条，其中 2 条已合并/关闭（均为 CI/CD 自动化 PR），5 条待合并（含 1 条草稿）。
- 社区关注点集中在**虚拟时间跳跃功能**（#11141）和**自动补全令牌跨框架转换**（#11035），后者为近期修复 HSM/CHASM Nexus 操作一致性的关键补丁。
- 无新版本发布，但关闭了一个 1.32.0 版本分支准备 PR（#11140），表明下一个版本正在准备中。
- 长期 Issue #10177（迁移至 ScyllaDB GoCQL 驱动）今日获得更新，作者补充了性能测试意向，但尚未提供具体数据，社区讨论热度一般。
- 项目整体健康度良好，核心功能开发与测试修复同步推进，未见严重回归或阻塞性问题。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日合并/关闭的 PR 多为 CI/CD 自动化流程，但其中一条标志着版本分支的创建：

- **#11140 [已关闭]** `1.32.0: Prepare release branch` — 由 CI 机器人自动创建，覆盖了 governance 文件并更新了依赖。说明 Temporal 团队已启动 1.32.0 版本的发布流程，后续将进入 QA 和候选阶段。  
  [查看 PR](https://github.com/temporalio/temporal/pull/11140)

- **#11135 [已关闭]** `Update test shard salt` — 由 `optimize-test-sharding` 工作流自动生成的测试分片盐值更新，属于常规测试优化。  
  [查看 PR](https://github.com/temporalio/temporal/pull/11135)

其他待合并 PR 包括：
- **#11141 (草稿)** 虚拟时间跳跃功能（描述、轮询、最大跳过）— 为客户端提供查询虚拟时间和快进完成的能力，尚处于早期开发阶段。
- **#10106** 独立活动的暂停/恢复/重置/更新选项 — 实现服务端控制 API，已持续开发近3个月，可能是 1.32.0 的目标功能之一。
- **#11139** 解除 7 项 CHASM Nexus 工作流测试的跳过，并修复了 CHASM 异步完成中的 handler rehydration 错误。
- **#11035** Nexus 完成令牌在 HSM 与 CHASM 之间的自动转换 — 解决重建逃生路径下令牌失效的问题。

**项目推进总结**：1.32.0 版本准备工作已启动；Nexus 子系统的 HSM/CHASM 双框架兼容性修复进入收尾；独立活动控制 API 仍处于开放状态，接近最终验收。

## 4. 社区热点

今日最受关注的 Issue 和 PR 如下：

- **Issue #10177** `[enhancement] 迁移至 ScyllaDB GoCQL 驱动`  
  - 评论数 7，更新日期 2026-07-19（今日）。作者 @mykaul 声明已经完成性能测试并将结果发布于后续评论，强调迁移改动小且速度更快，但不再支持 Cassandra 3.x（已 EOL）。  
  - 背后诉求：社区用户希望 Temporal 能利用 ScyllaDB 的高性能 GoCQL 驱动提升存储层吞吐量，且作者愿意贡献补丁。该 Issue 自 5 月提出至今未关闭，今日更新可能意味着维护者开始评估。  
  [查看 Issue](https://github.com/temporalio/temporal/issues/10177)

- **PR #11141 (草稿)** `虚拟时间跳跃：describe、poll 与 max skip`  
  - 今日新建，作者 @feiyang3cat。虽然评论数为 0，但其功能涉及测试时间加速和防止无限跳过循环，属于 Temporal 工作流测试体验的重要改进，受到测试开发者的关注。  
  [查看 PR](https://github.com/temporalio/temporal/pull/11141)

## 5. Bug 与稳定性

今日未报告新的显式 Bug 或崩溃类 Issue。但以下 PR 涉及潜在稳定性修复：

- **#11139** 解除 CHASM Nexus 测试跳过 + 修复 CHASM 异步完成中的 handler 重新水合失败（rehydrate handler failure）  
  - 严重程度：中等 — 该 bug 仅在 CHASM 模式下触发，影响 Nexus 异步完成的正确性。该 PR 已包含一次小的生产补丁。  
  [查看 PR](https://github.com/temporalio/temporal/pull/11139)

- **#11035** 修复 Nexus 完成令牌因重建（reset/conflict-resolution）导致的 `NotFound` 问题，通过跨框架转换自动重试。该问题在 HSM/CHASM 双框架并存时可能导致操作丢失，属于功能性回归。  
  [查看 PR](https://github.com/temporalio/temporal/pull/11035)

**综合评估**：当前版本未见重大稳定性问题，但 CHASM 相关的异步调用修复仍在待合并状态，建议 1.32.0 包含上述两个补丁。

## 6. 功能请求与路线图信号

- **虚拟时间跳跃（#11141）**：为 `DescribeWorkflowExecution` 添加虚拟时间、运行状态和快进完成信息，可用于测试自动化。该功能与 Temporal 长期规划的“测试工具增强”路线吻合，有望在未来小版本中集成。
- **独立活动操作 API（#10106）**：暂停/恢复/重置/更新选项的独立活动支持，是社区常见的操作需求（如运维手动干预活动）。该 PR 已处于开放状态近 3 个月，作者持续更新，很可能纳入 1.32.0。
- **ScyllaDB 驱动迁移（#10177）**：若性能测试结果明确且维护者认可，该功能可能作为未来可选存储后端支持。当前仍处于讨论阶段，暂无明确版本计划。

## 7. 用户反馈摘要

根据 Issue #10177 的评论，用户 @mykaul 表达了对 ScyllaDB 性能提升的正面体验，并指出迁移成本极低（“very little changes”）。其隐含痛点在于使用 Cassandra 3.x 的遗留用户面临 EOL 风险，而 Temporal 官方尚未正式宣布对 ScyllaDB 的支持。该用户希望社区能推动此迁移，并愿意亲自提交补丁。

此外，从 PR #11139 的描述可看出测试维护者曾被 Nexus 测试跳过困扰，此次解跳是社区测试可靠性的积极信号。

## 8. 待处理积压

- **Issue #10177**（2026-05-05 创建）—— 建议迁移至 ScyllaDB GoCQL 驱动，已获得作者性能测试承诺但未更新测试结果。已有 7 条评论，无维护者回复。标签：`enhancement`。  
  [查看 Issue](https://github.com/temporalio/temporal/issues/10177)

- **PR #10106**（2026-04-28 创建）—— 独立活动暂停/恢复/重置/更新，至今未合并，累计 0 条评论（可能通过其他渠道交流）。此为重大功能，但缺乏可见的代码审查进展，建议维护者协调时间进行 Review。  
  [查看 PR](https://github.com/temporalio/temporal/pull/10106)

- **PR #11035**（2026-07-13 创建，最后更新 2026-07-19）—— Nexus 令牌跨框架转换，与 #11139 紧密相关，同样待审。建议在 1.32.0 分支创建后尽快合并，避免版本分歧。  
  [查看 PR](https://github.com/temporalio/temporal/pull/11035)

---

*报告生成时间：2026-07-20 UTC*  
*数据来源：GitHub API / Temporalio/temporal 仓库*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*