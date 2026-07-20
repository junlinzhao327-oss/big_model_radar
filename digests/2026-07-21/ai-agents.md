# OpenClaw 生态日报 2026-07-21

> Issues: 357 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-20 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 OpenClaw GitHub 数据，生成一份客观、数据驱动的项目动态日报。

---

## OpenClaw 项目动态日报 | 2026-07-21

### 1. 今日速览

过去24小时，OpenClaw 项目保持了极高的活跃度。Issue 和 PR 的更新数量均处于高位，其中新 Issue 占比超过65%，表明社区用户正积极反馈问题与提出需求；PR 方面，待合并的 PR 接近400条，反映出项目贡献渠道畅通但维护者审核压力较大。今日无新版本发布，但涉及“会话状态”、“消息丢失”、“安全”和“认证提供者”等核心领域的 PR 和 Issue 讨论非常热烈，表明项目当前正处于关键的稳定性与安全性加固阶段。整体来看，项目生态繁荣，但维护者需要加快 PR 审核速度，以缓解积压。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

以下为今日合并/关闭的、对项目有实质推动的 PR 与 Issue 分析。虽然今日无明确合并的 PR 数据，但通过已关闭的 Issue 状态，可以判断项目向前的步伐。

- **会话与会话管理**：多个关于会话状态和上下文管理的 Issue 被关闭，例如 #63216 (重复硬重置) 和 #59618 (压缩中断任务执行)。这表明会话机制的稳定性和健壮性有所提升。相关 Issue #96684 (子代理唤醒导致父级压缩) 也在持续追踪中，并有对应的 PR #110297 正在等待审核，显示出维护者正在从系统层面解决核心问题。
- **跨平台与渠道兼容性**：针对 Google Chat 空间消息被静默忽略的 Issue (#58514) 和 Slack 多工作区 DM 回复失败的问题 (#58523) 仍在开放中，但已有 PR #109583 尝试修复 QQ 机器人端的 WebSocket 内存问题，表明项目对不同平台的适配工作在持续推进。
- **基础设施与工具链**：关于 SQLite 运行时增强的多个 Issue ( #79904, #79903, #79905 ) 在今日被标记为已关闭，这标志着围绕 SQLite 会话存储和检索的配套工具链取得了阶段性成果，为构建更强大的数据分析和会话恢复能力打下了基础。此外，PR #100845 修复了 `--local` 模式下 OTel 遥测无法导出的问题，提升了项目的可观测性。

### 4. 社区热点

今日讨论最热烈、反映社区核心关切的 Issue/PR 如下：

- **#99241: 工具输出渲染为图像附件** (23条评论)
  - **链接**: `https://github.com/openclaw/openclaw/issues/99241`
  - **分析**: 这是今日讨论度最高的 Issue。用户反馈在长时间运行或包含大量 ANSI 字符的工具工作流中，工具结果会坍缩成 `(see attached image)` 占位符，导致 Agent 无法读取关键的 `stdout/stderr` 文本。这触及了 `message-loss` 和 `session-state` 两个核心痛点，强烈影响了用户体验。

- **#7707: 内存信任标签功能请求** (19条评论)
  - **链接**: `https://github.com/openclaw/openclaw/issues/7707`
  - **分析**: 社区对安全性的关注度极高。该功能请求提出为记忆条目打上基于来源的信任级别标签，以防止提示词注入攻击。这是对 Agent 安全性的一个前沿思考，代表了用户对 AI Agent 核心安全机制的更高要求。

- **#10659: 掩码密钥功能请求** (15条评论)
  - **链接**: `https://github.com/openclaw/openclaw/issues/10659`
  - **分析**: 用户希望 Agent 能“使用”API 密钥，但“看不到”它们。这与 #7707 同属安全工作流，旨在防止 agent 在被攻击时泄露敏感凭证。社区对此需求反应强烈，表明生产环境中用户对安全边界的重视。

### 5. Bug 与稳定性

今日报告的 Bug 和稳定性问题主要集中在会话上下文管理和渠道通信方面，严重程度较高。

- **P1 级 - 会话上下文误报** (#108238): `2026.7.1` 版本中，会话上下文用量错误地将 `cacheRead` 计入 `totalTokens`，导致误触发压缩。此问题严重影响了 Agent 的正常工作流。**状态: 已关闭，有待核实修复来源。**
- **P1 级 - 子代理交付失败** (#92076): 当请求者的会话已失效或被锁定时，子代理的完成结果无法送达用户，导致消息丢失。这在高并发或长时间会话场景下是严重问题。**状态: 开放中，尚未有对应 Fix PR。**
- **P1 级 - 上下文用量异常下降** (#108215): 会话上下文用量在短时间内从57%跌至13%，但压缩计数为0，表明存在未跟踪的、潜在的数据丢失或状态切换。**状态: 开放中。**
- **P1 级 - exec 工具中断后“卡死”** (#102006): 这是一个Regression问题。`exec` 工具调用被中止后，会导致同一会话中后续所有 `exec` 调用无限期挂起。**状态: 开放中，相关用户已标记为“maturity:stable”，影响范围可能很广。**
- **P2 级 - OOM 风险** (#111760): PR 指出 MXC 扩展中的策略文件读取未做大小限制，存在内存耗尽的风险。**状态: 有对应 Fix PR。**
- **稳定性新增 - Agent 创建的Cron任务权限固化** (#101349): Agent 创建的 Cron 任务会继承创建时的 `toolsAllow` 权限，且后续无法通过更新清除，这在安全审计上是潜在风险。**状态: 开放中。**

### 6. 功能请求与路线图信号

社区对新功能的呼吁聚焦于自动化统一、安全沙箱和智能Agent行为控制，这些可能成为下个版本的重点。

- **Everything is a cron** (#110950): 用户提出将Heartbeat、Watcher、定时任务等所有自动化形式统一为 `cron job` 的概念，以简化设计和增强灵活性。这是一个对系统架构影响深远的提案，维护者 (`maintainer`) 已参与讨论，可能成为下个大版本的核心特性。
- **Agent 执行沙箱隔离** (#58730): 受 Claude Code 源码泄露事件启发，用户强烈建议引入 `exec()` 沙箱隔离和更细粒度的工具权限模型。此 Feature Request 结合了安全( `impact:security` )和会话状态( `impact:session-state` )，反映了业界对 Agent 安全性的普遍担忧。
- **抑制子Agent/工具错误通知** ( #8299, #39406 ): 用户希望获得更多配置选项来抑制子Agent的完成任务宣布和工具的瞬时错误警告。这表明精细化的用户界面控制是提升用户体验的关键。
- **添加 Antigravity CLI (agy) 后端** (#84527): 随着 Google Gemini CLI 的退役，社区已开始推动对新替代品 `agy` 的支持。该需求获得了11个点赞，显示其紧迫性。

### 7. 用户反馈摘要

从今日的 Issue 讨论中，可以提炼出以下用户声音：

- **核心痛点：工具输出不可读** (`#99241`): 用户对 `(see attached image)` 的反馈非常强烈，他们认为“原始输出往往是关键证据”，这种“图形化占位”机制严重损害了 Agent 作为“工具者”的效用。
- **关键诉求：Autonomous Agent 应被“看见”** (`#58450`): 用户指出了AI Agent的一个典型的“幻觉”行为：“承诺稍后跟进”但并未启动任何实际操作。这是一个关键的UX问题，用户希望Agent的决策和行为过程更加透明和可验证。
- **复杂环境下的部署痛点** (`#94032`): macOS 用户在使用 `exec` 工具时无法访问私有局域网的主机，而同一用户的其他 GUI 程序却可以。这表明新引入的沙箱或权限模型与现有系统环境存在兼容性问题，对普通开发者而言定位困难。
- **对安全性的普遍不信任** (`#10659`, `#7707`, `#12219`): 多个 Issue 的核心都是围绕“不让 Agent 看到它‘不该看’的东西”，包括 API 密钥、记忆条目等。这表明社区用户对 AI Agent 的安全边界有高度警觉，并期望项目提供强大的安全内建机制。

### 8. 待处理积压

以下为长期未响应或卡在某个关键步骤的重要 Issue/PR，提醒维护者关注。

- **古老且重要的功能请求**:
  - `#7707` (记忆信任标签): 创建于2026-02-03，至今有19条评论，但未进入实施阶段。
  - `#6615` (exec-approvals 拒绝列表): 创建于2026-02-01，获得8个赞，但仍在等待产品决策。
  - `#12219` (技能权限清单): 创建于2026-02-09，直接关联安全“供应链”问题，亟需推动。

- **关键 Bug 待诊断**:
  - `#56733` (Gateway 事件循环冻结): 这是一个 P1 级、标记为 `maturity:stable` 的久远 Bug，可能导致生产环境服务静默挂起，目前仍然需要实时复现 (`needs-live-repro`)。
  - `#79752` (gzip 解压失败): 影响macOS Node v26用户，涉及 Discord 等多个 HTTP 服务，虽已关闭，但根本原因可能未在代码层面根治。

- **等待维护者审核的 PR**:
  - `#110297` (修复工具密集型会话中的合成溢出): 关联 P1 级 Bug #107655，由维护者提出的关键修复，目前状态为 `👀 ready for maintainer look`，应优先处理。
  - `#100845` (fix cli: one-shot agent --local OTel): 虽然优先级为 P2，但它解决了 `--local` 模式下用户完全无法获取遥测数据的空白，应尽早合并。

---

## 横向生态对比

# 2026-07-21 AI 智能体与个人 AI 助手开源生态横向对比分析报告

## 1. 生态全景

个人 AI 助手与自主智能体开源生态正处于爆发增长期，项目迭代速度极快，社区参与度空前高涨。各项目普遍面临三大共性问题：**安全与隐私**（记忆信任标签、API 密钥掩码、沙箱隔离）、**会话状态稳定性**（消息丢失、上下文溢出、数据一致性）以及**跨平台兼容性**（Windows、macOS、特定终端环境）。同时，**模型快速迭代**（GPT-5.6、Qwen 新思路层级）要求项目持续适配；**多 Agent 编排**（统一 ACP 客户端、子代理中断传播）成为下一阶段的核心探索方向。维护者精力瓶颈开始显现，多个项目出现高质量 PR 和关键 Issue 积压。

---

## 2. 各项目活跃度对比

| 项目 | 活跃评估 | 今日新开/活跃 Issue | 今日 PR 总数 | 版本发布 | 健康度评估（源自日报） |
|------|----------|-------------------|------------|--------|----------------------|
| **OpenClaw** | 极高 | 新 Issue 占比 >65%（约26+） | 待合并约400条 | 无 | 生态繁荣，但 PR 积压严重，维护压力大 |
| **Hermes Agent** | 极高 | 超百条 | 超百条 (合并/关闭25+条) | **v0.19.0** (Quicksilver) | 架构重构进行中，桌面端稳定性薄弱 |
| **OpenHands SDK** | 中高 | 27条 (新开/活跃26条) | 31条 (合并4条) | 无 | 健康度良好，长期增强请求积压 |
| **Pi** | 极高 | 95条动态 (新开/活跃11条，关闭84条) | 28条 (合并/关闭25条) | 无 | 修复效率极高，健康度良好 |
| **LiteLLM** | 极高 | 53条 (新开39条，关闭14条) | 194条 (合并/关闭54条) | **v1.94.0-rc.2** | 极其活跃，正在全面加固测试与安全 |
| **Temporal** | 高 | 3条 | 41条 (合并/关闭16条) | 无 | 稳定开发，重点在混沌测试和 SAA 增强 |

*数据来源：各项目日报原始统计*

---

## 3. OpenClaw 在生态中的定位

OpenClaw 专注于 **个人 AI 助手的核心数据平面**：会话状态管理、记忆持久化、工具调用安全。与同类项目相比：

**优势**：
- **技术深度**：对会话上下文溢出、消息丢失、同步问题等底层稳定性的探讨在生态中最深入，相关 Issue 涉及 `impact:session-state`、`message-loss` 等关键标签。
- **社区共识强**：关于记忆信任标签 (#7707)、API 密钥掩码 (#10659) 等功能请求获得大量点赞和讨论，引领了 AI 助手安全边界的需求定义。
- **用户场景明确**：面向需要长期运行、频繁工具调用的高级用户，工程化程度高。

**劣势与挑战**：
- **维护者瓶颈**：待合并 PR 近 400 条，大量高质量贡献悬而未决（如 #110297 关键修复），影响社区信心。
- **跨平台适配稍弱**：相比 Pi 和 Hermes Agent，OpenClaw 的 Windows/QQ 等平台问题更突出，且修复进度较慢。
- **用户界面（UX）欠佳**：工具输出坍缩为图像（#99241）等问题触及核心体验，社区反馈强烈。

与同类对比（差异化详见第5节），OpenClaw 的生态位更接近 **“极致技术型的个人 Agent 内核”**，而非 Hermes Agent 的框架层或 LiteLLM 的代理层。

---

## 4. 共同关注的技术方向

以下方向在多个项目中同时涌现，具有显著生态共性：

| 技术方向 | 涉及项目 | 具体诉求表现 |
|----------|----------|--------------|
| **会话状态一致性与持久化** | OpenClaw, Hermes Agent, OpenHands SDK, Pi, Temporal | 会话上下文溢出、消息丢失、子代理中断传播、KV 缓存失效 |
| **安全与权限控制** | OpenClaw, Hermes Agent, OpenHands SDK, LiteLLM, Pi | 记忆信任标签、API 密钥掩码、沙箱隔离、安全分析器可信度、认证绕过 |
| **跨平台与终端兼容性** | Hermes Agent, OpenHands SDK, Pi, OpenClaw | Windows PowerShell 多行、Feishu Markdown、Kitty 终端双击、QQ WebSocket 内存 |
| **模型快速集成与适配** | LiteLLM, Pi, OpenClaw | GPT-5.6 函数调用问题、Qwen/Kimi 思考层级、OpenRouter OAuth |
| **可观测性与成本透明度** | LiteLLM, Pi, OpenClaw, Temporal | UI 数据显示、成本计算误差、遥测导出本地模式、成员状态指标 gauge |
| **通知/告警精细化管理** | OpenClaw, OpenHands SDK, LiteLLM | 抑制子 Agent 错误通知、审核摘要、电子邮件通知未发送 |

---

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent | OpenHands SDK | Pi | LiteLLM | Temporal |
|------|----------|--------------|---------------|----|---------|----------|
| **核心功能** | 个人会话AI引擎（记忆/工具/安全） | 通用Agent框架（插件/多Profile/多租户） | 开发者Agent SDK（ACP协议/轻量） | 终端优先的个人助手（TUI/快速迭代） | AI API代理网关（路由/安全/监控） | 分布式工作流引擎（可靠性/韧性） |
| **目标用户** | 高级个人用户、AI爱好者、开发者 | 企业DevOps/工程团队、复杂Agent场景 | 应用开发者、系统集成商 | 终端用户、开发者（日常编程助手） | 企业AI基础设施管理者、平台团队 | 后端开发者、SRE团队（微服务编排） |
| **技术架构** | 插件+会话管理层（Node.js） | 模块化插件系统（Typescript） | 异步事件驱动（Python） | TUI+模型层（Go/TypeScript） | 代理+守卫+缓存（Python） | 事件溯源+分布式共识（Go） |
| **生态侧重点** | 会话层稳定性、安全边界 | 插件统一、多会话隔离 | ACP兼容、子代理编排 | 交互体验、Provider扩展 | API兼容性、企业安全 | 测试覆盖、混沌工程 |

---

## 6. 社区热度与成熟度分层

**第一梯队：极度活跃、快速迭代型**
- **Hermes Agent**: 社区贡献者450+，v0.19.0版本发布体现指数级增长，但重构带来较多迁移问题。
- **LiteLLM**: 24小时PR达194条，测试覆盖率大幅提升，进入质量巩固期与功能拓展并行的阶段。

**第二梯队：高活跃、稳定迭代型**
- **Pi**: 每日大量bug修复（关闭84个Issue），对用户反馈响应极快，生态处于“快修快发”状态。
- **OpenClaw**: 社区讨论深度高，Issue质量高，但维护速度远不及Pi，导致积压严重，需警惕社区热情消退。

**第三梯队：中等活跃、质量巩固型**
- **OpenHands SDK**: 活动相对平稳，重点在修复已知bug和跟进ACP协议演进，长期增强请求（如持久化记忆、异步解耦）仍未突破。
- **Temporal**: 项目本身成熟度较高，当前聚焦混沌测试和独立活动功能增强，社区讨论偏技术性问题，无重大创新功能推出。

---

## 7. 值得关注的趋势信号

1. **安全与隐私从“附加功能”变为“核心要求”**  
   OpenClaw 的记忆信任标签、Hermes Agent 的多租户隔离、LiteLLM 的密钥泄露风险、OpenHands SDK 的安全分析器可信度 —— 安全不再只是合规问题，而是决定用户是否信任Agent自主执行的关键门槛。

2. **多Agent协作与编排成为兵家必争之地**  
   Hermes Agent 的“通用化ACP客户端”呼声最高；OpenHands SDK 的子代理中断传播修复；Temporal 的独立活动增强 —— 都指向未来Agent将从单兵作战走向混合智能体协作。

3. **终端用户体验成为瓶颈**  
   Pi 的终端随机滚动、Hermes Desktop 侧边栏空白、OpenClaw 的工具输出坍缩为图像 —— 在模型能力快速提升的背景下，U I/交互细节的打磨成为项目能否被广泛采用的决定性因素。

4. **开源维护者生态压力显现**  
   OpenClaw 近400条待合并PR、OpenHands SDK 中长期未合并的 #3574 —— 社区贡献的热情面临“投进去但无人审核”的困境。项目组需要引入更多维护者或自动化工具（如Dependabot、Release Please）来缓解瓶颈。

5. **模型快速迭代带来的适配成本剧增**  
   GPT-5.6、Qwen Token Plan、Gemini CLI退役 —— 每个新模型都带来新的API兼容性、参数行为变化（如 reasoning_effort），项目团队需要建立自动化测试套件和模型适配模板，否则将面临持续的功能退化和用户流失。

6. **本地/离线部署需求不可忽视**  
   LiteLLM 的 v1.92.0 启动联网下载问题、OpenClaw 的 `--local` OTel 导出缺失 —— 企业用户对内网隔离、离线运行的需求强烈，项目应预置离线配置路径和降级策略。

---

*以上分析基于 2026-07-21 各项目公开数据，所有链接见各项目日报原文。*

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，根据您提供的 Hermes Agent 项目数据，我将为您生成一份结构清晰的 2026-07-21 项目动态日报。

---

## Hermes Agent 项目动态日报 | 2026-07-21

### 1. 今日速览

项目活跃度极高，Issues 和 PR 均超百条，社区与核心贡献者深度参与。v0.19.0 “Quicksilver Release” 的发布是项目重大里程碑，展现了极强的开发动能。当前主要关注点集中在 **插件系统统一性**、**多租户与多会话管理**、**桌面端稳定性** 以及 **平台兼容性（特别是 Feishu 和 Windows）** 上。项目健康状况良好，正向更成熟、更健壮的 Agent 框架迈进。

### 2. 版本发布

**Hermes Agent v0.19.0 (v2026.7.20) — The Quicksilver Release**

- **发布日期:** 2026年7月20日
- **核心亮点:** 自 v0.18.0 以来，项目经历了指数级的增长：完成了 **~2,245 次提交**，合并了 **~1,065 个 PR**，关闭了 **~3,300 个 Issue**，并有 **450+ 社区贡献者** 参与。代号“水银”暗示了本次版本追求的更快速、更流动的体验。
- **潜在变更与迁移注意:**
    - 发布说明中提及 “Hermes is the mess”，暗示了本次版本可能对核心架构进行了大幅重构或引入了颠覆性变更。
    - 结合 Issue 讨论，建议用户在升级前重点关注以下可能受影响的配置项或行为：
        - **配置根键白名单:** 迁移至更严格的配置验证 (`_EXTRA_KNOWN_ROOT_KEYS`)，自定义非标准配置项需显式声明。
        - **插件热加载机制:** 新版本强调“对称式”插件重载，旧版插件注册/注销路径可能失效。
        - **状态数据库 Schema:** FTS5 索引优化可能要求数据库迁移 (`schema v23`)。
        - **网络连接管理:** `keepalive_expiry` 参数变更影响部分代理服务 (Cloudflare/OpenRouter)，需确认配置兼容性。

### 3. 项目进展

今日合并/关闭的重要 PR 主要集中在修复关键 Bug、提升系统稳定性以及改善平台兼容性，标志着项目正快速从快速迭代期进入稳定打磨期。

- **关键 Bug 修复与稳定性提升:**
    - **[PR #68249]** `fix: register vertex provider in CLI menus` / **[PR #67090]** `fix(nix): include apps/shared in TUI source filter` / **[PR #68251]** `fix(dashboard): accept HERMES_DASHBOARD_PUBLIC_URL hostname` 等，修复了多项平台和组件的配置与兼容性问题，提升了整体健壮性。
    - **[Issue #4319]** `[Performance] KV cache invalidation on compression...` 被关闭，标志着对本地 MoE 模型性能优化问题已有解决方案落地。
    - **[Issue #44100]** `Telegram: assistant responses not persisted to session DB` 等长期困扰用户的会话持久化问题也已解决。

- **社区热点推进:** 大量围绕 **插件统一接口** (Issues #64182, #64178, #64174, #64161) 的讨论和 PR，表明项目正集中力量解决插件系统在不同执行环境（CLI、Gateway、Cron等）下的行为一致性问题，这是迈向架构成熟的关键一步。

- **Windows 兼容性进展:** **[PR #68252]** `fix(cli): preserve worktree quarantine on Windows` 和 **[PR #66769]** `fix(cron): prefer Git Bash for Windows shell scripts` 显示出项目显著加大了在 Windows 平台上的投入和修复力度。

### 4. 社区热点

今日讨论热度最高的问题反映了社区对系统可靠性、跨平台体验和高级功能集成的核心诉求。

- **通用化 ACP 客户端 (Issue #5257):** **17条评论, 20 👍**
    - **链接:** [#5257](https://github.com/NousResearch/hermes-agent/issues/5257)
    - **分析:** 这是社区最期待的功能之一。用户不满足于 Hermes 仅作为 Copilot 的客户端，而是希望它能成为 **“Agent 的 Orchestrator”**，通过统一的 ACP 协议协调和管理包括 Claude 在内的任何 ACP 兼容 Agent。这代表了从“单一 AI 工具”向“多 Agent 管理中心”的范式转变。

- **桌面端会话侧边栏Bug (Issue #67600):** **9条评论**
    - **链接:** [#67600](https://github.com/NousResearch/hermes-agent/issues/67600)
    - **分析:** 此 Bug 在更新后立即暴露，严重影响桌面端用户体验。尽管后端数据正常，但前端 UI 渲染失败，属于典型的“前后端不同步”问题，反映了在快速迭代中前端测试和回归的薄弱环节。

- **Feishu 插件兼容性 (Issue #9549):** **13条评论, 9 👍**
    - **链接:** [#9549](https://github.com/NousResearch/hermes-agent/issues/9549)
    - **分析:** 多个 Feishu 相关 Issue 的集中讨论，显示出使用飞书作为主要工作流平台的用户群体庞大。社区反馈的 Markdown 表格渲染问题是一个经典痛点，开发者已提供了详细的修复背景，解决方案较为明确。

### 5. Bug 与稳定性

今日报告的 Bug 按严重程度排序如下：

| 严重程度 | Issue链接 | 标题 | 状态 | 对应 Fix/PR |
| :--- | :--- | :--- | :--- | :--- |
| **P1** | [#67953](https://github.com/NousResearch/hermes-agent/issues/67953) | Gateway executor does not load mcp_servers config | **已关闭** | 与 PR #68249 等类似，属于配置加载路径问题，已修复。 |
| **P2** | [#67600](https://github.com/NousResearch/hermes-agent/issues/67600) | Desktop session sidebar is empty for the `default` profile only | **打开** | 暂无直接 Fix PR |
| **P2** | [#59305](https://github.com/NousResearch/hermes-agent/issues/59305) | Chat tab messages leak across sessions (Desktop) | **打开** | 暂无直接 Fix PR |
| **P2** | [#67762](https://github.com/NousResearch/hermes-agent/issues/67762) | `agent.session_estimated_cost_usd` resets to $0 on gateway restart | **打开** | **[PR #68250]** 部分相关，修复了重连认证问题，但未直接解决成本重置。 |
| **P3** | [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) | Skills index is stale or degraded | **打开** | 暂无直接 Fix PR |
| **P3** | [#67012](https://github.com/NousResearch/hermes-agent/issues/67012) | keepalive_expiry=20s breaks streaming via Cloudflare/OpenRouter | **打开** | 暂无直接 Fix PR |
| **P2** | [#68095](https://github.com/NousResearch/hermes-agent/issues/68095) | Desktop input box shrinks + desktop build stuck on v0.15.1 | **打开** | 暂无直接 Fix PR |

**小结:** 桌面客户端 (Desktop) 出现多个 P2 级别 Bug，影响了核心交互和会话管理，是当前的稳定性薄弱环节。同时，网络配置变更引发的代理兼容性问题也需要重点关注。

### 6. 功能请求与路线图信号

社区提出的新功能需求，与项目现有 PR 方向高度重合，预示着下一版本将聚焦于以下领域：

- **插件系统架构升级 (很可能纳入 v0.20.0):**
    - **Issue #5257:** 通用化 ACP 客户端，使其成为多 Agent 编排器。
    - **Issue #64182:** 插件接口扩展，统一所有执行表面的 hook/middleware 行为。
    - **Issue #64161 & #64174:** 为插件增加流式 LLM 输出钩子和辅助模型路由能力。
    - **关联 PR:** **[PR #65161]** `feat(skills): add opt-in routed loading`， **[PR #63791]** `docs(memory): list Nexusyn standalone memory provider plugin`。

- **多租户与权限模型 (路线图优先级高):**
    - **Issue #34352:** 提出“多租户 Hermes”问题，这是服务化部署的关键能力。核心挑战在于内存操作绕过 hook 系统导致租户隔离难以实现。
    - **关联 PR:** **[PR #68203]** `fix: scope private URL policy per multiplexed profile`，直接针对多 profile 场景下的 URL 策略隔离问题。

- **工具和 MCP 生态增强:**
    - **Issue #5257** 和 **[PR #67807]** / **[PR #68246]** (`feat(computer_use): align/add cua-driver contracts & permission modes`) 显示出社区正在积极将计算机使用 (CUA) 能力与 MCP 协议进行深度整合。

### 7. 用户反馈摘要

从今日的 Issue 讨论中，可以听到用户的真实声音：

- **对“多 Agent 编排”的渴望（来自 #5257）:** 用户不仅满足于一个 Copilot，而是希望 Hermes 成为大脑，指挥各种专用 Agent 工作。这是对 Agent 生态互联互通的强烈需求。
- **多租户部署的痛点（来自 #34352）:** 企业用户在生产环境中面临多租户难题。他们提出了“在不 fork 核心代码的情况下实现租户隔离”的诉求，并分享了已运行的通用解决方案，显示出先进用户的深度参与和极强的工程能力。
- **桌面端体验的挫折（来自 #67600, #59305, #68095）:** 多名用户报告了桌面端的各种体验问题，从侧边栏空白到“聊炸天”的消息串扰，再到输入框异常缩小，严重影响了日常使用。这些反馈表明桌面客户端的质量监控和回归测试急需加强。
- **对配置和安装的困惑（来自 #29866, #66868）:** “brew upgrade 后所有平台失效”、Cron 任务莫名 401 认证失败，这类基础配置和部署问题是最消耗用户耐心的。用户清晰地指出了根本原因（`cacert.pem` 缺失/配置作用域问题），方案明确，应优先响应。

### 8. 待处理积压

以下 Issue 和 PR 长期未获得核心维护者的明确回应，可能形成项目发展的路障，需引起关注。

- **P1 级别 Bug 积压:**
    - **[Issue #67953]** `Gateway executor does not load mcp_servers config` — **已关闭**
    - **[Issue #29866]** `brew upgrade breaks certifi...` — 创建于5月，核心配置问题。

- **P2 级别，影响核心体验的 Bug:**
    - **[Issue #59305]** `[Desktop] Chat tab messages leak across sessions` — 报告于7月6日，严重影响会话正确性。
    - **[Issue #67600]** `Desktop session sidebar is empty for the default profile` — 报告于7月19日，用户刚更新就遇到。

- **长期搁置且重要的 Feature Request:**
    - **[Issue #933]** `Feature Request: Support multiple OAuth tokens with automatic fallback` — 创建于3月，获得4个 👍，但至今未实现。对用户处理多账号和速率限制至关重要。

- **长期未合并的 PR:**
    - **[PR #45334]** `fix(redact): exclude shell substitutions from env-assignment secret matching` — 创建于6月13日，涉及安全红线，修复一个明显的 Regex 误匹配问题，却近一个月无人合入。
    - **[PR #39790]** `fix(auxiliary): rebuild closed cached clients` — 创建于6月5日，一个明确的稳定性修复，同样等待合入超过40天。

**结论:** 项目开发活跃度极高，核心团队推进有力，但维护者精力可能面临瓶颈，导致部分高质量 PR 和关键 Issue 长期无人问津。建议项目组优化 Issue 和 PR 的 Review 优先级，特别是针对用户体验（Desktop Bug）和安全（Redact 误匹配）类问题，建立更迅速的响应与处理机制。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目日报  
**日期：2026-07-21**  
**数据来源：GitHub 仓库 [OpenHands/software-agent-sdk](https://github.com/OpenHands/software-agent-sdk)**  

---

## 1. 今日速览

过去 24 小时项目保持高度活跃，共产生 27 条 Issue 更新（新开/活跃 26 条，关闭 1 条）和 31 条 PR 更新（待合并 27 条，合并/关闭 4 条）。社区讨论集中在 **ACP 协议兼容性**、**Windows 终端稳定性**、**子代理中断传播**及**安全分析器可信度**等关键问题上。核心贡献者提交了多项重构与修复 PR，整体项目健康度良好，但长期积压的增强请求（如持久化记忆、异步解耦）仍需持续关注。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

### 合并/关闭的重要 PR

- **[#4147] feat(tool): add structured outcome to FinishAction for infeasible tasks**  
  为 `FinishAction` 添加结构化结果字段，使代理在任务不可行时能向编排器明确传递错误或未完成状态，解决了全自动无人工干预场景下的反馈缺失问题。  
  [PR #4147](https://github.com/OpenHands/software-agent-sdk/pull/4147)

- **[#4161] Support concurrency-safe local Codex auth writeback**  
  解决了本地与 Docker 部署下 `CODEX_AUTH_JSON` 写入时的并发安全问题，确保每个 ACP 会话拥有独立可写的工作副本。  
  [Issue #4161](https://github.com/OpenHands/software-agent-sdk/issues/4161)（已关闭）

- 另有 3 条其他 PR 被合并/关闭（列表中未完整展示），整体推进了 SDK 在工具结构化输出、并发安全性及配置迁移方面的基础能力。

---

## 4. 社区热点

| 议题 | 评论数 | 核心诉求 |
|------|--------|----------|
| [#2078] Daily Integration Runs | **142** | 集成测试运行占位符，长期高评论量，反映社区对持续集成稳定性的关注。 |
| [#4019] ACP profiles inject duplicate skills | 10 | ACP 配置下技能被重复注入，影响启动效率与配置清晰度。 |
| [#3992] Asymmetric handling of content-without-tool-call | 7 | 弱模型返回纯文本无工具调用时，代理被非对称处理逻辑异常终止。 |
| [#4063] max_concurrent_runs 不限制原生异步会话 | 7 | 并发控制仅对同步 `conversation.run()` 生效，原生异步调用可绕过限制。 |

**分析：** 评论最密集的议题集中在**ACP 配置兼容性**（#4019）、**模型响应解析不对称**（#3992）和**并发控制漏洞**（#4063），显示出用户在多模型部署和异步高并发场景下的真实痛点。  
[Issues 列表](https://github.com/OpenHands/software-agent-sdk/issues?q=is%3Aissue+updated%3A%3E%3D2026-07-20)

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重性 | Issue | 描述 | 已有修复 PR |
|--------|-------|------|-------------|
| 🔴 高 | [#4080] 单个未注册事件类型导致整个对话加载失败 | 若某个持久化事件反序列化失败（如 `observation.kind` 未注册），整个对话被静默丢弃，不再出现在服务列表中。 | 无 |
| 🔴 高 | [#3992] 弱模型因内容无工具调用被错误终止 | `ResponseDispatchMixin` 对 `CONTENT` 类型响应处理不对称，导致弱模型（如本地模型）被提前终结。 | 无 |
| 🟡 中 | [#4063] `max_concurrent_runs` 不限制原生异步会话 | 文档声称限制并发，但仅对同步线程池生效，`EventService.run()` 可绕过。 | 无 |
| 🟡 中 | [#4133] WindowsTerminal 无法执行多行 PowerShell 命令 | 多行命令停留在 `>>` 续行提示符，最终超时，PS1 元数据后缀被当作输入回显。 | [#4155](https://github.com/OpenHands/software-agent-sdk/pull/4155) |
| 🟡 中 | [#4156] Windows 下通过 uvx 启动 agent-server 报 ModuleNotFoundError | `libtmux` / `openhands.tools` 未正确安装，导致服务崩溃。 | [#4115](https://github.com/OpenHands/software-agent-sdk/pull/4115) |
| 🟡 中 | [#4107] 任务中断未传播到子代理 | `LocalConversation.arun()` 被中断时父对话进入 `PAUSED`，但子代理仍继续运行。 | [#4108](https://github.com/OpenHands/software-agent-sdk/pull/4108) |
| 🟢 低 | [#4052] MCP  schema 迁移未正确应用 | 已有 MCP 配置的用户升级后设置丢失。 | 已关联 PR #4013 |
| 🟢 低 | [#4093] ACP 0.11 移除 `models` 字段导致 Gemini 状态丢失 | 依赖无上界，ACP Python SDK 0.11.0 破坏性变更导致 Pydantic 验证失败。 | 无 |

**小结：** 今日报告的 Bug 覆盖了 Windows 兼容性、异步并发、事件反序列化等核心路径，其中 #4080 和 #3992 影响面较广，建议优先处理。

---

## 6. 功能请求与路线图信号

| Issue | 类型 | 描述 | 关联 PR |
|-------|------|------|---------|
| [#4130] Feature: search_tool | Enhancement | 提议新增 `search_tool`，将工具搜索从系统提示中剥离，减轻提示膨胀并改善缓存。 | 无 |
| [#4162] Adopt Release Please | Enhancement | 建议采用 Release Please 实现自动化版本发布，减少人工协调成本。 | [#3939](https://github.com/OpenHands/software-agent-sdk/pull/3939)（已提PR） |
| [#3988] Support OS keyring for secret storage | Enhancement | 提议使用 OS 密钥环存储 LLM 密钥，替代当前明文持久化方式。 | 无 |
| [#3612] Prompt registry Phase 4 | Enhancement | 提示注册表第四阶段，实现 Shell-aware prompt 和交互变体功能。 | 无 |
| [#2047] Non-blocking background subagent execution | Enhancement | 允许父代理在子代理后台运行时继续执行其他工作，提升并发效率。 | 无 |

**路线图信号：** 社区对**工具搜索机制**、**自动化发布流程**、**秘密管理**的需求日益明确。其中 Release Please 已有对应 PR（#3939）在推进，预计可能进入下一版本；`search_tool` 尚无实现，但讨论热度上升，值得路线图关注。

---

## 7. 用户反馈摘要

从 Issue 评论中提炼的真实用户场景与痛点：

- **“弱模型断连”**：用户 `@Rkaplounov` 报告，使用本地模型（如 LLaMA）时，当 LLM 返回纯文本（无工具调用），SDK 会触发错误逻辑直接终止代理，导致会话无法继续。用户认为这是对非主流模型的不友好对待。  
  [Issue #3992](https://github.com/OpenHands/software-agent-sdk/issues/3992)

- **“Windows 上的 PowerShell 噩梦”**：用户 `@LDlornd` 描述在 Windows 下执行多行 PowerShell 命令时，终端卡在 `>>` 续行提示，最终超时，原命令不执行。该问题严重影响了 Windows 用户的使用体验。  
  [Issue #4133](https://github.com/OpenHands/software-agent-sdk/issues/4133)

- **“安全分析器信任模型自我评估风险”**：用户 `@AUTHENSOR` 指出，当设置 `security_analyzer: llm` 且 `confirmation_mode: true` 时，LLM 自我标记为 LOW 风险的操作会自动执行，无需人工确认。用户认为这存在安全隐患，应增加更多验证机制。  
  [Issue #4157](https://github.com/OpenHands/software-agent-sdk/issues/4157)

- **“ACP 配置重复注入技能”**：用户 `@simonrosenberg` 发现 ACP 配置下，`AGENTS.md` 中的项目技能被重复注入，导致工作空间混乱且影响性能。  
  [Issue #4019](https://github.com/OpenHands/software-agent-sdk/issues/4019)

---

## 8. 待处理积压

以下 Issue / PR 长期未得到响应或合并，建议维护者优先关注：

| 议题 | 创建时间 | 最后更新 | 备注 |
|------|----------|----------|------|
| [#2037] Memory: Persistent auto-learning across sessions | 2026-02-13 | 2026-07-20 | 增强请求，已有关联设计 PR #2810 但尚未合并 |
| [#2697] QuestionTool — 代理向用户提问 | 2026-04-03 | 2026-07-20 | 功能请求，社区呼声较高 |
| [#2755] Implement HookType.PROMPT | 2026-04-08 | 2026-07-20 | 与提示注册表相关，有 PR #4160 刚提交 |
| [#3353] Refactor: dedup async/sync code | 2026-05-21 | 2026-07-20 | 大型重构 PR，减少约 1000 行重复代码，仍在审查中 |
| [#3574] Web UI 的 POST 请求缺少 X-Session-API-Key 导致 401 | 2026-06-08 | 2026-07-20 | Bug，影响前端所有 POST 操作，尚未有修复 PR |
| [#3560] Supply-chain typosquat detection | 2026-06-07 | 2026-07-20 | 安全增强，无关联 PR |

**建议：** #3574 直接影响 Web UI 的正常使用，且已超过一个月未修复，应列为 P0 级积压。

---

*以上日报基于 GitHub 公开数据自动生成，所有链接为原始 Issue/PR 地址。如有遗漏，请参考完整仓库。*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 (2026-07-21)

## 今日速览
过去 24 小时内，项目社区活跃度极高：共产生 95 条 Issue 动态（新开/活跃 11 条，关闭 84 条）和 28 条 PR 动态（待合并 3 条，已合并/关闭 25 条）。无新版本发布。大量 Bug 被快速修复并关闭，同时多个功能性 PR 也已合并，项目健康度良好。社区反馈集中在终端体验优化、高性能场景稳定性、以及 Provider 集成扩展上。

---

## 版本发布
无

---

## 项目进展
今日合并/关闭了 25 个 PR，以下为关键进展：

- **会话管理增强**：[PR #6874](https://github.com/earendil-works/pi/pull/6874) 为会话选择器添加 `Ctrl+A` 快捷键，可一键归档选中的会话文件至 `.pi/archive/YYYY-MM/`，提升会话清理效率。
- **Provider 生态扩展**：[PR #6858](https://github.com/earendil-works/pi/pull/6858) 新增 Qwen Token Plan 作为内置 API-Key Provider（国际版与国内版），填补了阿里云模型集成空白；[PR #6786](https://github.com/earendil-works/pi/pull/6786) 暴露了 Kimi Coding K3 的 `low`/`high`/`max` 思考层级，提升开发者调参灵活性。
- **成本计算优化**：[PR #6881](https://github.com/earendil-works/pi/pull/6881)（OPEN）尝试直接使用 Provider 返回的 billed cost 替代本地计算，未来可提高费用显示准确度。
- **Bug 修复**：[PR #6864](https://github.com/earendil-works/pi/pull/6864) 修复了 `env` 配置段在 auth.json 中被忽略的回归；[PR #6854](https://github.com/earendil-works/pi/pull/6854) 修复了切换模型时 tool_call_id 冲突导致的崩溃；[PR #6859](https://github.com/earendil-works/pi/pull/6859) 修复了 Bun 环境下包更新检查失效的问题；[PR #6837](https://github.com/earendil-works/pi/pull/6837) 与 [PR #6853](https://github.com/earendil-works/pi/pull/6853) 共同修正了 GPT-5.6 系列模型的上下文窗口值（272K）。
- **基础设施改进**：[PR #6812](https://github.com/earendil-works/pi/pull/6812) 移除了 `./` 前缀，避免 lockfile 反复变动；[PR #6865](https://github.com/earendil-works/pi/pull/6865) 新增 `get_available_thinking_levels` RPC，便于扩展动态查询可用思考层级。

项目在** Provider 兼容性、成本管理、用户交互便捷性**三个方向均有实质推进。

---

## 社区热点
以下 Issues/PR 在过去 24 小时引发最多讨论（按评论数排序）：

1. **[#5023](https://github.com/earendil-works/pi/issues/5023) [终端随机滚动到开头]** — 9 条评论，已关闭。用户报告终端会在模型工作时无征兆跳转到会话开头并快速滚动至缓冲区末尾，影响阅读与操作。该问题已被标记为 bug 并关闭，推测有对应修复。
2. **[#5263](https://github.com/earendil-works/pi/issues/5263) [默认临时化模型与思考层级变更]** — 8 条评论，8 个 👍，目前仍为 OPEN。用户希望将会话内的模型切换和思考层级选择默认视为临时更改，仅影响当前会话；并在 `/settings` 中添加“默认模型”选项用于永久设置。社区对此功能呼声较高，或将成为下一版本重点。
3. **[#6792](https://github.com/earendil-works/pi/issues/6792) [编辑 500+ 行大文件时高 CPU]** — 8 条评论，已关闭。用户反馈在生成和编辑 1000+ 行 Markdown 文件时出现 100% CPU 占用，附件提供了 CPU profile，问题已被定位并关闭，修复可期。
4. **[#6210](https://github.com/earendil-works/pi/issues/6210) [`/scoped-models` 无法选择含括号的模型 ID]** — 8 条评论，OPEN。由于选择器未正确处理模型 ID 中的特殊字符（如 `[1m]`），导致显示“No models match pattern”。用户期望支持转义或引用语法。

**分析**：社区核心诉求集中在**用户体验一致性**（终端滚动、临时设置、模型选择）、**边缘场景稳定性**（大文件、特殊字符）以及**成本透明度**（费用计算、定价准确性）。

---

## Bug 与稳定性
按严重程度排列，标注是否已有修复 PR：

| Issue | 严重性 | 状态 | 修复 PR |
|-------|--------|------|---------|
| [#6792](https://github.com/earendil-works/pi/issues/6792) 写大文件 CPU 100% | **严重** | 已关闭 | 未明确链接，但已知已修复 |
| [#5023](https://github.com/earendil-works/pi/issues/5023) 终端随机滚动 | **严重** | 已关闭 | 未知 |
| [#5407](https://github.com/earendil-works/pi/issues/5407) Kitty 键盘双击 | **中** | 已关闭 | 未知 |
| [#6725](https://github.com/earendil-works/pi/issues/6725) Copilot 定价少算 cacheWrite | **中** | 已关闭 | 未知 |
| [#6794](https://github.com/earendil-works/pi/issues/6794) 启动极慢（模型目录刷新卡死） | **中** | 已关闭 | 未知 |
| [#6801](https://github.com/earendil-works/pi/issues/6801) OpenAI Responses 退化解码无限流 | **高** | 已关闭 | 未知 |
| [#6825](https://github.com/earendil-works/pi/issues/6825) `--system-prompt` 失效 | **中** | 已关闭 | 未知 |
| [#6820](https://github.com/earendil-works/pi/issues/6820) 自动压缩期间消息丢失 | **中** | 已关闭 | 未知 |
| [#6675](https://github.com/earendil-works/pi/issues/6675) `pi update --self` 单次网络失败即放弃 | **低** | OPEN | 无 PR |
| [#6652](https://github.com/earendil-works/pi/issues/6652) crash 日志硬编码路径 | **低** | OPEN | 无 PR |
| [#6768](https://github.com/earendil-works/pi/issues/6768) Copilot Enterprise 下压缩失败 | **中** | OPEN | 无 PR |
| [#6774](https://github.com/earendil-works/pi/issues/6774) Ctrl+G 外部编辑器慢（tmpdir 拥堵） | **低** | OPEN | 无 PR |
| [#6819](https://github.com/earendil-works/pi/issues/6819) `assistant.usage` 为 undefined 导致崩溃 | **高** | 已关闭 | 未知 |
| [#6851](https://github.com/earendil-works/pi/issues/6851) pi-agent-core 静态导入 /compat 导致多余 Provider 被打包 | **中** | 已关闭 | 未知 |

**小结**：今日修复效率极高，多数严重 Bug 均在 24 小时内被关闭。但仍存在 4 个 OPEN bug，涉及更新容错、日志路径、企业版兼容性和编辑器启动性能，建议维护团队安排后续版本修复。

---

## 功能请求与路线图信号

以下新功能需求获得较高关注，部分已有对应 PR 实现：

- **临时化模型层级变更** ([#5263](https://github.com/earendil-works/pi/issues/5263))：8 👍，OPEN。需求明确且社区共识强，可纳入下一版本规划。
- **支持视频/音频内容输入** ([#3200](https://github.com/earendil-works/pi/issues/3200))：4 👍，OPEN（自 4 月 15 日）。多模态模型日益普及，建议优先考虑。
- **扩展报告外部 LLM 成本** ([#6509](https://github.com/earendil-works/pi/issues/6509))：已关闭，但理念被 PR #6671 部分实现（为分支摘要和压缩条目添加 usage 元数据）。
- **防止动态 system prompt 意外清空缓存** ([#6621](https://github.com/earendil-works/pi/issues/6621))：1 👍，已关闭，相关建议已接收。
- **添加 OpenRouter OAuth 支持** ([#6814](https://github.com/earendil-works/pi/issues/6814))：已关闭，未说明是否实现，但社区表达了简化连接流程的期望。
- **隐藏滚动导航帮助** ([#6833](https://github.com/earendil-works/pi/issues/6833))：已关闭，需求较小但体现用户对 TUI 整洁度的关注。
- **扩展挂钩原始流** ([#3605](https://github.com/earendil-works/pi/issues/3605))：OPEN，对希望深度自定义进度显示的用户有价值。

**路线图信号**：项目正在深化 Provider 集成（Qwen Token Plan 已合并），同时优化成本与使用数据可视化。会话体验的临时/永久分离、多模态支持是值得关注的长期方向。

---

## 用户反馈摘要

从 Issues 评论中提炼的真实用户感受：

- **积极反馈**：  
  - 多位用户感谢快速修复，例如 [#6792](https://github.com/earendil-works/pi/issues/6792) 作者在关闭后未再投诉，暗示修复已测试通过。  
  - 对于 [#6621](https://github.com/earendil-works/pi/issues/6621)，用户感谢维护者关注局部内存设备（如 AMD Strix Halo）的预填充慢问题。

- **痛点**：  
  - **终端行为异常**：Kitty 终端的双击 Enter/Backspace 问题 ([#5407](https://github.com/earendil-works/pi/issues/5407)) 以及随机滚动 ([#5023](https://github.com/earendil-works/pi/issues/5023)) 严重影响日常使用。  
  - **大文件性能**：编辑 1000+ 行文件导致 CPU 占满，用户表示“今天无法工作”([#6792](https://github.com/earendil-works/pi/issues/6792))。  
  - **配置迁移不便**：crash 日志忽略 `PI_CODING_AGENT_DIR` 导致在自定义目录下产生 `.pi` 脏目录 ([#6652](https://github.com/earendil-works/pi/issues/6652))。  
  - **Cut/Copy 体验**：复制 TUI 输出时引入多余空格和换行 ([#5931](https://github.com/earendil-works/pi/issues/5931))，用户期望“所见即所得”。  
  - **成本不透明**：Copilot 定价少算 ([#6725](https://github.com/earendil-works/pi/issues/6725)) 和本地计算误差导致用户对费用存疑。

- **使用场景**：用户广泛使用 Pi 进行代码生成、文档编写、多模型测试，且有部分用户依赖 Pi 作为 Day-to-day 生产力工具，稳定性要求高。

---

## 待处理积压

以下 Issue/PR 长期未响应或更新较少，建议维护者优先关注：

| 编号 | 标题 | 创建时间 | 最近更新 | 状态 | 备注 |
|------|------|----------|----------|------|------|
| [#3200](https://github.com/earendil-works/pi/issues/3200) | 支持视频/音频内容输入 | 2026-04-15 | 2026-07-20 | OPEN | 已 3 个月，虽有 comment 但无分配标签 |
| [#2616](https://github.com/earendil-works/pi/issues/2616) | SessionManager 同步阻塞，无法异步持久化 | 2026-03-26 | 2026-07-20 | **CLOSED** | 虽已关闭，但核心架构问题是否已彻底解决？需二次验证 |
| [#3605](https://github.com/earendil-works/pi/issues/3605) | 提供扩展挂钩原始响应的 hook | 2026-04-23 | 2026-07-19 | OPEN | 无 label，未分配 |
| [#6675](https://github.com/earendil-works/pi/issues/6675) | `pi update --self` 网络失败即放弃 | 2026-07-15 | 2026-07-20 | OPEN | 需增加重试或 fallback |
| [#6768](https://github.com/earendil-works/pi/issues/6768) | Copilot Enterprise 压缩失败 | 2026-07-17 | 2026-07-20 | OPEN | 3 个 👍，可能有较多企业用户受影响 |
| [#6652](https://github.com/earendil-works/pi/issues/6652) | crash 日志路径硬编码 | 2026-07-14 | 2026-07-20 | OPEN | 简单修复，可考虑快速合并 |

**建议**：针对 [#6675] 和 [#6652] 此类低风险高收益的修复，可尽快安排 PR；对 [#6768] 企业版兼容问题需主动联系报告者获取更多日志。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我已根据您提供的 GitHub 数据，为您生成了 2026年7月21日 的 LiteLLM 项目动态日报。

---

# LiteLLM 项目动态日报 | 2026-07-21

## 1. 今日速览

项目今日活跃度极高，社区讨论与开发活动均处于高峰状态。过去24小时内，共产生53条 Issue 更新和194条 PR 更新，显示了社区的高度参与与团队的快速响应。新版本 v1.94.0-rc.2 发布，持续优化用户体验与系统稳定性。尽管存在一些值得关注的 Bug 和功能请求，但项目整体健康度良好，正朝着更稳定、功能更丰富的方向快速演进。

- **活跃度评估**: ⭐⭐⭐⭐⭐ (极高)
- **版本发布**: 1 个候选版本
- **关键数据**: Issues 净新增 25 条 (新开/活跃 39 减 关闭 14)，PR 待合并与合并中状态活跃 (待合并 140，已合并/关闭 54)。

## 2. 版本发布

- **[v1.94.0-rc.2](https://github.com/BerriAI/litellm/releases/tag/v1.94.0-rc.2)**
    - **发布说明**: 这是一个候选发布版本。主要新特性是引入了 Docker 镜像签名，所有 LiteLLM Docker 镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 进行签名，增强了供应链安全。
    - **破坏性变更**: 无。
    - **迁移注意事项**: 此版本为候选版（Release Candidate），建议测试环境先行验证。生产环境请关注后续正式版本。

## 3. 项目进展

项目今日在测试、功能完善和 Bug 修复方面均有显著推进，体现出团队对质量与稳定性的高度重视。

- **基础设施与安全加固**:
    - **[#34032](https://github.com/BerriAI/litellm/pull/34032)**: 修复 CI，升级 `brace-expansion` 依赖以解决安全漏洞 (GHSA-3jxr-9vmj-r5cp)。
    - **[#33284](https://github.com/BerriAI/litellm/pull/33284)**: 批量更新 GitHub Actions 依赖，涵盖 `actions/checkout`、`setup-python`、`cache` 等19个组件，确保 CI/CD 流程的现代性与安全性。
- **功能增强与适配**:
    - **[合并]** [#33733](https://github.com/BerriAI/litellm/pull/33733): 新增 `bedrock_tags` 参数支持，允许在 Bedrock 的批量任务 (CreateModelInvocationJob) 中传递标签。
    - **[合并]** [#33885](https://github.com/BerriAI/litellm/pull/33885): 优化 UI，当只有一个守卫组有条目时，隐藏守卫组标题，提升界面整洁度。
    - **[#34036](https://github.com/BerriAI/litellm/pull/34036)**: 新增 `AgentGuards` 作为新的守卫提供商，提供越狱检测、PII 检测和数据泄露防护功能。
    - **[#34038](https://github.com/BerriAI/litellm/pull/34038)**: 在 MCP 服务器表单中新增 `ID-JAG` (Okta Cross App Access) 认证类型。
- **性能与稳定性**:
    - **[合并]** [#34037](https://github.com/BerriAI/litellm/pull/34037): 修复了 `model_info` 端点测试的不稳定性，解决了 CI 环境下的随机失败。

## 4. 社区热点

今日社区讨论焦点集中于两大方向：经典功能请求的持续关注，以及对新模型/功能的迫切需求。

- **⚡ 功能请求热点：动态 wishlist 持续增长**
    - **讨论焦点**: [#361](https://github.com/BerriAI/litellm/issues/361) “我希望 LiteLLM 能... Wishlist”
    - **数据**: 评论 470, 更新时间 2026-07-20
    - **分析**: 这个长期存在的 Issue 汇集了社区对项目的众多期望。尽管近期关闭，但它依然是社区反馈的“蓄水池”，持续获得470条评论，证明其作为社区需求总揽的重要性。新进用户会在此留下对新功能的想法，对于项目规划有极高参考价值。

- **💬 高互动 Bug 与功能请求**:
    - **[Bug]** [#33221](https://github.com/BerriAI/litellm/issues/33221): 用户报告 `OpenAI gpt-5.6` 系列模型在使用 `Function tools` 时失败，引发了5条评论。这表明社区对前沿模型的集成适配非常敏感。
    - **[Feature]** [#33893](https://github.com/BerriAI/litellm/issues/33893): 请求为 GitHub Copilot 添加 GPT-5.6 支持，显示了企业用户对集成最新模型能力的热切期望。
    - **[Bug]** [#32357](https://github.com/BerriAI/litellm/issues/32357): 关于 `/v1/messages` 适配器对推理模型（如GLM/DeepSeek-R1）的流式传输编码错误，引起了使用 Claude Code 开发者的高度关注。

## 5. Bug 与稳定性

今日报告的 Bug 类型多样，覆盖了代理功能、模型适配、UI 交互和关键性能问题，部分高危问题已有对应的修复 PR，显示团队的快速响应能力。

- **严重**:
    - **[#33221](https://github.com/BerriAI/litellm/issues/33221)**: `gpt-5.6` 系列模型函数工具调用失败，影响核心代理功能。**状态: 待处理**。
    - **[#33969](https://github.com/BerriAI/litellm/issues/33969)**: 代理出现 `InternalServerError` 并触发异常，导致偶发性的连接错误，影响服务可用性。**状态: 待处理**。
    - **[#33952](https://github.com/BerriAI/litellm/issues/33952)**: `/utils/transform_request` 端点为阻塞 I/O 操作，可能冻结整个代理事件循环，对高并发环境是严重风险。**状态: 待处理**。
    - **[#33167](https://github.com/BerriAI/litellm/issues/33167)**: v1.92.0 版本启动时尝试下载 Prisma 二进制文件，在无互联网的离线/企业环境中导致启动失败。**状态: 待处理**。

- **中/高风险**:
    - **[#33984](https://github.com/BerriAI/litellm/issues/33984)**: Cloudflare 适配器无法翻译 OpenAI 格式的 `content-part` 消息，导致多模态或复杂消息接口不兼容。**状态: 待处理**。
    - **[#32202](https://github.com/BerriAI/litellm/issues/32202)**: `pass_through_endpoints` 转发代理的 `Authorization` 标头，存在严重的**密钥泄露风险**。**状态: 待处理**。
    - **[#33324](https://github.com/BerriAI/litellm/issues/33324)**: `allowed_ips` 功能在 `X-Forwarded-For` 多跳代理场景下完全失效，导致 IP 限制功能被绕过。**状态: 待处理**。

- **低风险/已修复**:
    - **[#25624](https://github.com/BerriAI/litellm/issues/25624)** (已关闭): 透传端点在 gzip 解压缩后转发了错误的 `Content-Length` 标头。
    - **[#25553](https://github.com/BerriAI/litellm/issues/25553)** (已关闭): `update_cache` 导致缓存了旧密钥对象，绕过对密钥的更改。
    - **[#25623](https://github.com/BerriAI/litellm/issues/25623)** (已关闭): 健康检查表无限增长导致仪表盘性能下降。
    - **[#34013](https://github.com/BerriAI/litellm/pull/34013)**: 修复了内存和磁盘缓存递增操作的非原子性问题 (**有 Fix PR**)。

## 6. 功能请求与路线图信号

今日用户提出的新功能请求主要集中在与最新基础模型的兼容性、企业级集成和本地化体验上。

- **🎯 明确信号：紧跟前沿模型**
    - **GPT-5.6 系列**: [#33893](https://github.com/BerriAI/litellm/issues/33893) 请求为 GitHub Copilot 支持 GPT-5.6，结合 Bug [#33221](https://github.com/BerriAI/litellm/issues/33221) 来看，用户对 `gpt-5.6` 的集成有极高的需求。**行动号角**: 加速修复 `gpt-5.6` 的函数调用适配。
    - **Python 3.14**: [#26343](https://github.com/BerriAI/litellm/issues/26343) 用户请求重新支持 Python 3.14，表明社区对前沿开发环境的追求，尽管该 Issue 已关闭，但涉及的30个 👍 说明需求依旧存在。

- **🎯 企业级与高阶功能**
    - **外部认证集成**: [#34038](https://github.com/BerriAI/litellm/pull/34038) 新增 ID-JAG (Okta) MCP Server 认证类型，显示项目向企业级 SSO 能力扩展的决心。
    - **高级 Guardrails**: [#34036](https://github.com/BerriAI/litellm/pull/34036) 新增 AgentGuards 安全提供商，表明安全防护是项目持续投入的重点方向，也是企业客户的核心需求。

- **🔭 路线图推论**:
    从今日的 PR/Issue 综合来看，项目的短期路线图将聚焦于：
    1.  **AI 模型适配**: 紧急适配 `gpt-5.6` 等前沿模型，尤其是其新的工具调用特性。
    2.  **稳定性与安全性**: 解决事件循环阻塞、密钥泄露、连接超时等高危急 Bug，并持续加固 CI/CD 与部署安全 (如 Prisma 下载)。
    3.  **测试覆盖**: 大量合并/新开的 e2e 测试 PR (如 #34010, #34007 等)，显示团队正全力通过增加测试覆盖率来提升项目可靠性。

## 7. 用户反馈摘要

从今日的 Issues 中，可以提炼出用户的几类核心痛点与反馈：

- **😠 痛点：配置复杂性与不透明**
    - **UI 数据显示**: [#23636](https://github.com/BerriAI/litellm/issues/23636) 用户虽已启用 `store_prompts_in_spend_logs`，但 UI 仍显示“数据不可用”，反映了后端配置与前端展示之间存在同步或逻辑错误，打击用户对配置系统的信任。
    - **模型适配细节**: [#33221](https://github.com/BerriAI/litellm/issues/33221) 用户在尝试使用新模型时，由于版本升级导致的推理参数变化（`reasoning_effort`）与工具调用功能冲突，体验中断，暴露出在模型版本演进过程中的兼容性问题。

- **😍 满意：新功能呼声高**
    - **基础模型扩展**: [#33893](https://github.com/BerriAI/litellm/issues/33893) 用户明确要求支持 Github Copilot 模式的 `GPT-5.6`，这是一种对“与开发工具生态更好结合”的期望，也侧面印证了 LiteLLM 在开发者中的广泛使用。
    - **多模态 Embedding**: [#24393](https://github.com/BerriAI/litellm/issues/24393) 用户提出支持谷歌新的多模态嵌入模型，反映了 AI 应用场景从纯文本向多模态发展的趋势，用户希望 LiteLLM 能跟上这个潮流。

- **🤔 使用场景**:
    - **企业级代理部署**: 用户 (如 #33324, #33167) 展示了在企业内网、有防火墙限制、使用复杂网络拓扑 (多跳代理) 等环境下部署代理的困难。他们需要更健壮、更安全的网络集成能力。
    - **MCP 服务器集成**: 用户通过 `pass_through_endpoints` 整合第三方服务 (如 #18169, #32202)，说明 LiteLLM 正在作为中心化 API 网关被广泛使用，与外部服务的无缝、安全集成至关重要。

## 8. 待处理积压

以下是需重点关注、长期未响应但仍有关键影响的 Issue 和 PR：

- **⚠️ 高风险 Bug 待响应**:
    - [#25778](https://github.com/BerriAI/litellm/issues/25778) **UI 邮件通知**: 用户报告“UI 从未发送邀请邮件”，因后端端点未被 UI 调用。这是一个基础的可用性问题，长期存在会影响组织开通新用户。
    - [#32202](https://github.com/BerriAI/litellm/issues/32202) **关键安全**: 透传端点会泄露代理 `Authorization` 标头，这是一个严重的**密钥泄露风险**和**安全漏洞**，应给予最高优先级处理。
    - [#33167](https://github.com/BerriAI/litellm/issues/33167) **离线环境部署**: v1.92.0 引入的启动时联网下载行为使 LiteLLM 完全无法在安全隔离的企业内网环境中使用。

- **🔁 功能请求待评估**:
    - **[Feature]** [#26343](https://github.com/BerriAI/litellm/issues/26343): **Python 3.14 支持**。虽然 Issue 已关闭，但获得30个 👍 表明这是强大社区呼声，项目组应在其路线图中阐明对此的长期支持策略。
    - **[Feature]** [#24393](https://github.com/BerriAI/litellm/issues/24393): **多模态 Embedding**。支持 `gemini-embedding-2-preview` 是推动 LiteLLM 成为真正多模态代理网关的关键一步。此功能请求有明确的 PR 实现需求，建议集成进未来版本。

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是 2026-07-21 的 Temporal 项目动态日报。

---

### **Temporal (github.com/temporalio/temporal) 项目动态日报**
**日期**: 2026-07-21
**分析师**: AI 智能体

---

### **1. 今日速览**

Temporal 项目今日保持稳定而高强度的开发节奏。社区与核心团队的贡献集中在两大领域：一是对**独立活动 (SAA)** 的全面修复与功能完善，包括重试逻辑、描述响应和测试框架；二是持续强化**混沌测试**与**系统弹性**，特别是针对 Nexus、混合脑（mixedbrain）等系统模块。尽管有 3 个新 Issues 被提出，但团队在 24 小时内处理了 41 个 PR，显示了极高的解决效率。项目整体健康度良好，对即将到来的版本发布（如 v1.33.x 或 v1.34.x）做好了技术和稳定性准备。

### **2. 版本发布**

无。

---

### **3. 项目进展**

今日有 16 个 PR 被合并或关闭，项目在以下关键领域取得了实质性进展：

- **核心修复：** `#10899` 修复了在 closed workflow 上重新应用事件时的重启锚点，确保在特定边缘情况下不会因 `EmptyEventID` 而失败。`#11153` 修复了 Nexus 长轮询返回空响应的问题，使其与工作流/活动轮询行为一致，对 Nexus 接口的稳定性至关重要。

- **功能完善：** `#11130` 将独立活动（SAA）的 `PAUSED` 状态正确暴露在 visibility 和 describe API 中，使查询暂停活动成为可能。`#11154` 是 #11153 的 Cherry-pick，已合并到云版本分支。

- **系统清理与测试：** `#10319` 进行了一次重要的代码库重构，将旧的 “onebox” 测试图中的服务启动方式统一为通过 `temporal.NewServer`，减少了维护成本，并使测试更贴近生产环境。`#11001` 引入了混合脑进程混沌测试，自动重启服务器进程以验证系统韧性。

---

### **4. 社区热点**

- **`#9987`: Ringpop membership churn after upgrade to v1.30.x**
  - **状态**: 开放 (Open)
  - **热度**: 6 条评论，3 个 👍
  - **诉求**: 用户在升级到 v1.30.x 后发现 Ringpop 成员关系环出现波动（churn），导致服务发现不稳定和 gRPC 调用失败。问题高度具体，描述详尽（含日志和配置），表明用户在生产环境中遇到了严重的稳定性问题。社区可能存在持续的痛点，此 Issue 需要核心团队高度关注并给出明确路线图。

- **`#10899`: Reset to pending workflow task when reapplying to a closed workflow**
  - **状态**: 已关闭 (Closed)
  - **热度**: 尽管已关闭，但该 PR 解决了反馈给 #9987 类似问题背后的潜在逻辑缺陷。它处理了复制（replication）场景下的边缘情况，这通常是分布式系统稳定性的关键一环。

- **`#11146`: Membership: emit per-service reachable/available/draining member gauges**
  - **状态**: 开放 (Open)
  - **热度**: 0 条评论，0 个 👍
  - **诉求**: 这是对可观测性的直接需求。用户希望成员服务组件能暴露按服务（如 frontend, history）划分的、更细粒度的成员状态指标（reachable, available, draining），以便在滚动升级或故障排查时获得更清晰的可观测性。这反映了用户从“能用”到“能更好地排障”的进阶需求。

---

### **5. Bug 与稳定性**

- **严重 Bug：** `#11051` (Matching: task queue partition managers leaked on concurrent load) - 这是一个内存泄漏问题，由并发加载任务队列分区时产生“失败者”管理器未被清理导致。这些问题会通过动态配置订阅持续占用内存，在无流量的集群上也会发生。**严重性高**，有 open PR `#11081` 试图解决并发安全问题，但直接的内存泄漏修复尚未关联。

- **中等 Bug：** `#9987` (Ringpop membership churn) - 这是一个升级后引发的回归问题，影响服务发现和通信稳定性。**严重性高**，目前无直接 fix PR，需要排查。

- **低等 Bug：** `#10050` (fix: mark idempotent CQL queries for driver-level retry) - 这是一个长期存在的问题，标记了 Cassandra 的幂等查询以允许驱动重试。**严重性中等**，无争议但进展缓慢。`#11150` 修复了独立活动（SAA）的 `DescribeWorkflowExecution` 响应中关于下次重试间隔的错误。

---

### **6. 功能请求与路线图信号**

- **可观测性增强：**
  - `#11146` (Membership gauges) - **强烈信号**。直接关联到对 `#10730` 和 `#11108` 的调查，表明团队正在进行提升成员管理和可见性的专项工作。很可能被纳入下一版本（如 v1.33.x）。
  - `#11144` (VTS: add TimeSkippingInfo to DescribeWorkflowExecution) - 为虚拟时间服务（VTS）增加可观测性，对调试测试场景和特定时间线问题非常实用。

- **系统弹性与治理**
  - `#11001` (Add mixedbrain process chaos) - 混沌工程能力的扩展，表明团队主动提升系统健壮性。
  - `#11012` (Add caller rate-limit interceptor) - 引入按调用者进行速率限制的扩展点，这是一个重要的治理和防护机制，未来版本很可能会集成。

- **独立活动（SAA）全面增强：**
  - `#11137`， `#11149`， `#11150`， `#11152` 等。这一系列 PR 表明 SAA 功能正在从基础实现走向精细化运营，包括重试逻辑、错误类型、描述响应和测试框架。这是路线图上的一个重点项目。

---

### **7. 用户反馈摘要**

- **`#9987` 的评论者**：用户在升级后遇到了“严重的成员关系波动”，观察到 services 频繁变为 unhealthy 并重新注册。用户已确认未更改任何与成员相关的配置，并提供了详细的诊断日志。回滚到 v1.29.x 后问题消失，这进一步确认了这是一个回归问题。用户的沮丧感明显，但问题报告非常专业，有助于高效定位根因。

- **`#11051` 的评论者**：社区对内存泄漏的分析非常精准，并且明确指出了这是通过动态配置订阅 `pinned` 的，即使在上游 goroutine 失败后也无法被 GC。这直接指出了现有代码中对 goroutine 生命周期和资源释放的管理缺陷。

---

### **8. 待处理积压**

- **`#10050` (Cassandra idempotent CQL):** 自 2026-04-24 创建，长期未合并。虽然是低风险的优化，但能提升使用 Cassandra 后端的稳定性。提醒维护者评估社区对齐情况并考虑合并。
  - 链接： https://github.com/temporalio/temporal/pull/10050

- **`#10319` (Delete onebox fx graph):** 自 2026-05-18 创建，长期开放。由于是对测试框架的重大重构，可能正在等待更广泛的测试覆盖。这是减少维护债和提升测试可靠性的关键 PR。维护者应调整优先级，避免该 PR 持续过时。
  - 链接： https://github.com/temporalio/temporal/pull/10319

- **`#10251` (mixedbrain: exercise standalone Nexus):** 自 2026-05-13 创建，长期未解决。作为混沌测试的一部分，此 PR 的停滞可能意味着更复杂的依赖或设计决策。建议维护者明确其状态和未来计划。
  - 链接： https://github.com/temporalio/temporal/pull/10251

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*