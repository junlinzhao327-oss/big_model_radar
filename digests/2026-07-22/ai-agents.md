# OpenClaw 生态日报 2026-07-22

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-21 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我已根据您提供的 OpenClaw 项目 GitHub 数据，为您整理了 2026 年 7 月 22 日的项目动态日报。

---

### **OpenClaw 项目动态日报 | 2026-07-22**

#### **1. 今日速览**

过去 24 小时，OpenClaw 项目呈现出极高的活跃度，共产生约 1000 条 Issue 与 PR 更新（含新增与交互），显示出社区高度的参与热情和维护团队的积极回应。尽管未发布新的版本，但项目在 **macOS 隐私保护**、**UI/UX 体验** 以及 **核心 Agent 性能** 方面取得了显著进展，合并了多项关键修复。安全性与稳定性依然是社区讨论的核心焦点，多个高优先级问题正得到积极跟进。

#### **2. 版本发布**

*（无新版本发布。）*

#### **3. 项目进展**

今日有 **161 个 Pull Request** 被合并或关闭，项目整体向前迈进了坚实一步。以下是最值得关注的合并项：

- **macOS 隐私与权限模型重塑:** `#112321` 已完成合并，此项修复解决了 macOS 平台上隐私权限请求不当的问题，包括阻止非预期的终端自动化弹窗、确保语音唤醒功能符合隐私承诺，以及解耦主动计算报告功能，是提升平台安全性的重要一步。
- **核心 Agent 性能优化:** `#107935` 在关闭前已合并，它通过优化子代理注册表的读取范围，显著降低了控制器和子会话查找时的性能开销，直接解决了 `#105423` 中报告的性能瓶颈。
- **语义路由与配置修复:** `#112429` 合并了修复，确保 `cron` 投递目标在标准化后能保留渠道特定的语义前缀，解决了 Slack 等渠道中直接投递失败的回归问题。`#112334` 的合并则增强了配置验证的幂等性，允许对捆绑的模型提供商进行重新验证。
- **UI/UX 持续改进:** 合并了 `#112340` (自动化语言包更新) 和 `#112426` (Android 分支计数的本地化修复)。

#### **4. 社区热点**

今日讨论热度最高的议题高度集中在系统的安全性、稳定性和核心功能缺陷上：

- **安全与模式创新 - 掩码密钥 (Masked Secrets):** `#10659` 以 15 条评论位居榜首，社区正热烈讨论如何让 Agent **使用** API 密钥而非**看到**它们，以防止注入攻击和意外泄露。这一特性需求反映了用户对 AI Agent 安全性的核心关切。
- **稳定性危机 - 数据库损坏:** `#101290` 的 13 条评论记录了一场由 `preflight` 命令引发生产环境 SQLite 数据库损坏的严重事故。用户“databases corrupted four times”的描述显示出其对项目稳定性的强烈不信任感，此问题被标记为 **P0** 级，是当前最紧迫的稳定性 bug。
- **决策瘫痪与性能瓶颈:** `#86996` 和 `#85030` 分别有 11 条评论。前者描述了使用特定配置组合时导致的严重延迟和启动失败，后者则详细报告了 MCP 工具无法注入子 Agent 会话的架构性问题，这直接攻击了 OpenClaw 核心的灵活扩展能力。
- **紧急的兼容性问题:** `#106779` 有 11 条评论，报告了 `2026.7.1` 版本与 `llama.cpp` 本地方案不兼容的紧急问题。作为开源项目，对自托管模型的支持是核心功能，此问题影响范围广泛，社区反应强烈。

#### **5. Bug 与稳定性**

今日报告的 Bugs 严重性普遍较高，集中在 P0 和 P1 级别，项目整体的稳定性面临严峻考验。

| 严重程度 | 问题编号 | 核心问题 | Fix PR 状态 |
| :--- | :--- | :--- | :--- |
| **P0 / 紧急** | #101290 | CLI 启动检查命令 (preflight) 会损坏运行中 Gateway 的 SQLite 数据库，导致“database disk image is malformed”错误。 | 暂无关联 PR |
| **P1 / 高** | #86996 | 在特定内存、上下文引擎与模型组合下，导致长响应延迟、Hook 超时、启动中断及 Gateway 事件循环停滞。 | 暂无关联 PR |
| **P1 / 高** | #85030 | MCP 工具的详细配置在子 Agent 会话中被完全忽略，导致子 Agent 无法使用任何 MCP 工具。 | 暂无关联 PR |
| **P1 / 高** | #106779 | `2026.7.1` 版本与 `llama.cpp` 本地部署的 LLM 完全不兼容，请求返回 `400` 错误。 | 暂无关联 PR |
| **P1 / 高** | #90840 | 子 Agent 运行时 (sessions_spawn)，其原始输出被错误地直接发送给用户，而不是返回给父 Agent 进行总结，导致消息混乱。 | 暂无关联 PR |
| **回归** | #108473 | `cron` 工具的 JSON Schema 定义（包含非锚定的正则表达式）破坏了 `llama.cpp` 原生工具调用功能。 | 暂无关联 PR |

此外，还有多个 P1 级别 Bug 被再次重申，如 `#90840` (子 Agent 输出泄露) 等，表明这些问题的修复工作尚未完成。`#111498` 报告了一个新的回归问题：在 Anthropic 认证恢复后，Agent 被持久化的旧工作区状态迁移阻塞。

#### **6. 功能请求与路线图信号**

今日涌现的功能请求呈现出用户对 **安全性、可观测性、部署便利性** 的强烈需求。

- **安全与权限管理 (核心诉求):** `#10659` (掩码密钥), `#7722` (文件系统沙箱), `#12678` (基于能力的权限模型), `#13751` (飞书插件权限最小化) 等多个 Issue 都在围绕构建更细粒度的安全模型。结合已有的 `#112321` (macOS 隐私修复) PR，**安全加固是当前路线的重中之重**。
- **成本与效率优化:** `#14785` (减少工具 Schema Token 开销) 和 `#13219` (按模型用量计费日志) 反映出用户对运营成本的关注。已有 `#112412` (从提供商处动态发现模型) 的 PR 在推进，这表明项目在提升模型管理灵活性的同时，也在为后续的成本优化铺路。
- **开发者体验与运营:** `#13616` (备份/恢复工具), `#12855` (内置自动更新), `#13597` (AWS 部署指南) 等需求，表明项目正在从小众工具向需要成熟运维体系的企业级应用迈进。`#14438` (插件热重载) 更是直接触及了插件开发者的核心痛点。

#### **7. 用户反馈摘要**

- **对稳定性的担忧:** 在 `#101290` 中，用户 `@jarvis1982oc` 详细描述了数据库四次损坏的过程，情绪沮丧且困惑，强调“vanilla SQLite control does NOT reproduce”，这指向了 OpenClaw 独有的交互逻辑存在问题。**用户对核心数据安全产生了不信任。**
- **对缺失功能的急切期待:** 在 `#10659` 中，用户 `@jmkritt` 提出的“掩码密钥”方案获得了 4 个 👍，表明社区对简单、有效的安全方案有高度共识。用户们期望在不重写架构的前提下，解决 API 密钥泄露的燃眉之急。
- **对新版本兼容性的抱怨:** `#106779` 的创建者 `@delimir` 在升级到最新版后无法使用核心功能，反映了从稳定状态到功能崩溃的巨大落差。此类问题对用户体验的伤害最大，会快速降低用户对版本的信任。
- **对新交互范式的需求:** `#84527` 的提案（支持 Antigravity CLI）获得了 **11 个 👍**，这是今日最高的社交证明。用户 `@haofeif` 敏锐地捕捉到了 Google Gemini CLI 的退役风险，并主动为项目的兼容性铺路，体现了社区积极的反馈和贡献精神。**积极响应外部生态变化是保持项目活力的关键。**

#### **8. 待处理积压**

以下问题长期未获维护者明确回应，但严重性极高，建议优先关注：

- **#7722 - 文件系统沙箱配置 (Diamond Lobster，2026-02-03):** 用户早在 2 月就提出了一整套文件访问控制的实现方案，但至今仍停留在 `needs-maintainer-review` 阶段。这是构建 AI Agent 安全基石的长期需求。
- **#20786 - Telegram Business Bot 支持 (Diamond Lobster，2026-02-19):** 作为核心通信渠道，对 Telegram 新业务模式的支持请求搁置数月，可能会让部分潜在的企业用户流失。
- **#13616 - 备份/恢复工具 (Off-meta Tidepool，2026-02-10):** 在 `#101290` 数据库损坏报告之后，此功能请求的重要性不言而喻。提供一个官方、可靠的备份工具是重建用户信任的必要手段。

---

## 横向生态对比

# 个人 AI 助手与自主智能体开源生态横向对比分析报告 (2026-07-22)

## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态呈现出 **“基础夯实、安全先行、能力分化”** 的态势。各项目普遍在修复稳定性和安全性缺陷上投入大量精力（数据库损坏、凭证泄露、权限模型等），同时向**本地模型支持**、**插件/协议扩展**、**跨平台部署**等方向快速推进。社区对“可控、可观测、可自托管”的诉求高度一致，但各项目在技术路线上的定位差异日益明显——从 SDK 到完整 Agent 框架再到通用编排引擎，生态正在形成层级分明的供给链。整体活跃度极高，但部分项目面临积压与响应速度的挑战。

## 2. 各项目活跃度对比

| 项目 | 新开/活跃 Issues | 合并/关闭 Issues | 开放 PR | 合并/关闭 PR | 版本发布 | 健康度评估 |
|------|------------------|------------------|---------|-------------|---------|------------|
| OpenClaw | ~1000 条总更新 | 未具体说明 | 未说明 | **161** | 无 | **极高活跃，修复密集，稳定性危机** |
| Hermes Agent | **262** 活跃 | 51 关闭 | **384** 待合并 | **116** | 无 | **极高活跃，合并追赶提交，社区呼声强** |
| OpenHands SDK | 13 新开/活跃 | 3 关闭 | 30 开放 | **仅 1** | 无 | **中等活跃，PR 积压严重，依赖少数贡献者** |
| Pi | 未明确新开 | **53** 关闭 | 未说明开放数 | **15** | **v0.81.0, v0.81.1** | **高活跃，版本节奏快，本地模型里程碑** |
| LiteLLM | **52** 新开 | 18 关闭 | **138** 待合并 | **108** | 无 | **极高活跃，PR 吞吐量大，Bug 多样** |
| Temporal | 未明确新开 | 未说明 | **53** 待合并 | 22 | 无 | **高活跃，调度器重构为主轴，可靠性修复多** |

**解读**:
- **Hermes Agent** 和 **LiteLLM** 在 PR 数量上远超其他项目，但待合并库也最大，反映社区贡献热情高于核心维护者审查能力。
- **OpenHands SDK** 合并数仅 1 个，严重滞后；**Pi** 虽合并数仅 15 但版本发布两次，表明团队更倾向于通过版本统一推进。
- **OpenClaw** 的 Issues/PR 总数（约 1000）遥遥领先，但未细分新开/关闭，其 P0/P1 Bug 密集度最高。

## 3. OpenClaw 在生态中的定位

OpenClaw 在生态中扮演 **“核心参照系统”** 角色，定位为通用 AI Agent 框架。其优势与差异：

- **优势**：Issue/PR 总量最大（千级），社区反馈最激烈，安全修复响应迅速（如 macOS 权限模型重塑 #112321）。其对数据库损坏（#101290）等生产级问题的曝光，反而凸显了项目被广泛使用于真实场景。
- **技术路线差异**：与 Hermes Agent 强调插件接口扩展不同，OpenClaw 更侧重**内核安全与性能**（如掩码密钥、子代理注册表优化），功能请求偏向**运维工具**（备份/恢复、热重载），显示其正在从“玩具”向“企业级”过渡。
- **社区规模对比**：虽然无法精确对比 Stars，但仅从评论密度看，OpenClaw 单 Issue 评论数（最高 15 条）略低于 Hermes Agent（最高 15 条）和 LiteLLM（最高 58 条），但 Bug 严重等级（P0/P1）最集中。社区对稳定性的信任度正经历危机（用户四次数据库损坏）。

**结论**：OpenClaw 处于生态**技术领先但稳定性拖后腿**的阶段，若不能迅速解决 P0 级 Bug，可能流失用户至 Hermes Agent 等竞品。

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|----------|----------|----------|
| **本地/自托管模型支持** | Pi, OpenClaw, LiteLLM | Pi 发布了 llama.cpp 管理；OpenClaw 有 #106779 兼容性问题；LiteLLM 治理自托管端点。去云端依赖成趋势。 |
| **安全与凭证管理** | OpenClaw, Hermes Agent, OpenHands SDK, LiteLLM | 掩码密钥、文件沙箱、凭证生命周期、SCIM 同步、Authorization 头泄露。安全从“可选”变“核心”。 |
| **插件/工具扩展体系** | Hermes Agent, OpenClaw, OpenHands SDK, Pi | 插件接口扩展（#64182）、热重载（#14438）、QuestionTool（#2697）。Agent 能力通过生态提升。 |
| **会话/内存持久化** | OpenHands SDK, Hermes Agent, Pi | 跨会话记忆、可配置内存后端、会话 ID 稳定化。长期记忆是 Agent 进化的关键。 |
| **跨平台部署与可观测性** | Hermes Agent, OpenClaw, Temporal, LiteLLM | 桌面客户端独立安装、成员/预算监控指标、备份工具。企业运维需求提升。 |
| **协议兼容与网关** | LiteLLM, OpenHands SDK, Hermes Agent | OpenAI 兼容网关、ACP 协议扩展、SCIM/SCIM for groups。标准化接口趋同。 |

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent | OpenHands SDK | Pi | LiteLLM | Temporal |
|------|----------|--------------|---------------|----|---------|----------|
| **核心功能** | 全栈 Agent 框架 | Agent 框架 + 多平台客户端 | Agent 通信协议 (ACP) 及 SDK | 终端 UI 个人助手 | LLM 代理/网关 | 通用工作流编排 |
| **目标用户** | Agent 开发者、企业部署 | 高级用户、插件生态贡献者 | SDK 集成者、Agent 互联场景 | 命令行 + 本地模型爱好者 | 企业 API 网关运维 | 微服务编排、复杂状态管理 |
| **架构侧重** | 模块化（子 Agent、语义路由） | 插件 + 多界面（TUI/桌面/Telegram） | 标准化协议栈、凭证处理 | 终端交互 + 本地模型 | 多供应商路由 + 计费 + 安全 | 持久化工作流 + 容错 |
| **当前主要矛盾** | 稳定性漏洞 vs 用户信任 | PR 积压 vs 社区创新活力 | 合并瓶颈 vs 关键功能亟待落地 | 本地模型体验 vs 桌面端完善 | Bug 多样性 vs 企业级特性复杂度 | 调度器重构 vs 历史遗留性能 |
| **社区成熟度** | 高速迭代，但稳定性危机 | 高速迭代，社区贡献活跃 | 早期/中型，依赖核心维护者 | 稳定版本节奏，用户口碑好 | 极高热度，但 Bug 量大 | 成熟核心，社区偏运维 |

**关键差异**：Temporal 不直接面向 AI Agent 用户，而是作为底层编排引擎，但在 AI Agent 生态中被大量使用（作为agent的工作流引擎）。Pi 专注于终端用户体验和本地模型，更像“AI 终端”。OpenHands SDK 专注协议层，适合构建多 Agent 系统。LiteLLM 退化为纯网关，不涉及 Agent 智能。

## 6. 社区热度与成熟度

**第一梯队·极高热度（日活 Issue/PR >100 条）**：OpenClaw、Hermes Agent、LiteLLM  
- 特点：社区贡献爆炸式增长，同时 Bug 密集，维护者疲于应对。反映项目处于**快速迭代期**，但稳定性风险高。

**第二梯队·高活跃（20-100 条）**：Pi、Temporal  
- 特点：有稳定的版本节奏（Pi 双版本发布），Temporal 更聚焦在特定技术难点（调度器）。处于**功能深入期**。

**第三梯队·中等活跃（<20 条）**：OpenHands SDK  
- 特点：Issue 少但 PR 积压严重，核心功能（内存、ACP）推进缓慢，处于**早期孵化期**，依赖少数活跃贡献者。

**成熟度评估**：
- **最成熟**：Temporal（已稳定运行多年，社区关注运维增强）。
- **快速成长**：Pi（版本成熟度较高，用户粘性强）。
- **爆发增长**：Hermes Agent、LiteLLM、OpenClaw。
- **需加速**：OpenHands SDK（关键 PR 停滞 2 个月以上）。

## 7. 值得关注的趋势信号

1. **“本地优先”成为标配**：Pi 发布 llama.cpp 模型管理、OpenClaw 出现兼容性召回、LiteLLM 需处理本地端点 —— 即使是大规模私有化部署，用户对自托管的需求也在逼迫项目必须支持多种本地后端。**对 AI Agent 开发者**：在设计 Agent 架构时，需内置对本地模型的适配层，避免绑定云端。

2. **安全从“建议”升级为“准入”**：OpenClaw 的掩码密钥（#10659）、LiteLLM 的 Authorization 头泄露（#32202）、OpenHands SDK 的凭证生命周期 —— 安全不再只是功能，而是用户能否信任系统的基础。**对开发者**：任何涉及 API 密钥的操作都必须默认采用最小权限原则，并引入审计日志。

3. **插件/工具生态争夺战白热化**：Hermes Agent 的“插件接口扩展”Tacking Issue（#64182）和 OpenHands SDK 的“QuestionTool”（#2697）显示，各项目都在争夺第三方生态的核心控制点。谁能让插件开发最便捷、最安全，谁就可能成为下一个“Agent 的 App Store”。**对开发者**：密切关注各项目的插件 SDK 文档，选择生态潜力最大的框架。

4. **运维可观测性需求爆发**：Temporal 要求暴露成员等级指标（#11146），LiteLLM 希望有 Token 级成本归属（#26159），OpenClaw 需要备份工具和自动更新 —— 随着 Agent 系统进入实际生产，运营者需要知道“谁在用、用了多少、是否健康”。**对开发者**：在开发 Agent 初期就加入 Prometheus/OpenTelemetry 埋点，降低日后运维压力。

5. **协议标准化初步显现**：ACP（Agent Communication Protocol）在 OpenHands SDK 中成为核心；LiteLLM 推广 OpenAI 兼容网关；Hermes Agent 支持 MCP。这些标准化努力可能催生跨项目 Agent 互联的能力。**对开发者**：优先选择遵循开放协议（如 MCP、ACP）的工具，避免被锁在单一生态。

**总结**：当前生态正处于从“能跑就行”向“安全、可靠、可运维、可扩展”转型的关键期。短期内，稳定性问题（如 OpenClaw 的数据库损坏）会加速洗牌；长期看，具备良好插件生态和本地模型支持的项目将获得更持久的竞争力。建议技术决策者优先关注**安全修复速度**和**插件扩展开放度**，而不仅是功能列表的丰富程度。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目日报 — 2026-07-22

## 1. 今日速览

过去 24 小时内，Hermes Agent 仓库保持了极高的活跃度：共产生 **313 条 Issue 更新**（新开/活跃 262，已关闭 51）和 **500 条 PR 更新**（待合并 384，已合并/关闭 116）。社区讨论集中在**插件接口扩展**（#64182）、**会话状态稳定性**（#63078、#68358）以及**桌面客户端独立安装**（#38602）等方向。修复类 PR 密集涌现，覆盖租约泄漏、终端重写、MCP 工具发现等多个系统层面。**无新版本发布**，但合并/关闭的 PR 总数达到 116 条，表明合并速度正在追赶社区提交节奏。

## 2. 版本发布

无。

## 3. 项目进展

今日共有 **116 个 PR 被合并或关闭**，涵盖以下关键推进：

- **Web 工具插件初始化缺陷修复**：关闭 #27683，`web_tools.py` 缺少 `_ensure_plugins_discovered()` 调用导致搜索/提取/爬取静默失败的问题已随 `sweeper:implemented-on-main` 标记进入主线。
- **Matrix E2EE 设备验证问题**：关闭 #6174，Element 客户端发起的 SAS 验证无法得到 Hermes 响应的问题已被解决，加密消息解密恢复。
- **Claude 模型提示缓存命中率为 0%**：关闭 #56776，通过修复自定义 OpenAI 兼容网关的缓存启用逻辑，Claude 用户的路由缓存命中率恢复正常。
- **桌面端“删除配置文件”失败**：关闭 #47368，UI 侧隐藏但磁盘保留且重新出现的问题已修复。
- **Dashboard 聊天输入/输出不可见**：关闭 #53641，xterm.js 滚动偏移漂移问题已修复。
- **多重网关令牌解析越权**：关闭 #54675，多 profile 场景下次级 profile 错误使用默认 bot token 的安全漏洞已修复。
- **MCP 服务器重连后工具未注册**：关闭 #67187，Streamable HTTP MCP 服务器恢复连接后工具注册缺失的问题已修复。
- **桌面端冷启动超时**：PR #68958 增加了 Windows 冷启动超时，解决 `Hermes backend did not become ready` 错误（关联 #68705）。
- **会话租约泄漏**：PR #68947 与 #68949 分别优化了桌面/TUI 的会话租约释放逻辑，避免 `max_concurrent_sessions` 耗尽。

项目整体在**会话状态可靠性、安全边界、核心工具可用性**三个维度上迈出了扎实的一步。

## 4. 社区热点

今日讨论热度最高的议题集中在插件系统与会话管理：

| Issue/PR | 标题 | 评论数 | 核心诉求 |
|----------|------|--------|----------|
| [#64182](https://github.com/NousResearch/hermes-agent/issues/64182) | Tracking: Plugin Interface Expansion — community ideas, July 2026 | **15** | 从社区 Discord 讨论中提炼的插件接口扩展路线图，旨在让积压的插件 PR 能够稳定落地，涉及生命周期钩子、网关 UX 钩子等子项。 |
| [#47349](https://github.com/NousResearch/hermes-agent/issues/47349) | Feature: Configurable Memory Backends — disable memory.md, use honcho/fact_store only | **13** | 用户要求将硬编码的 `MEMORY.md` 改造为可配置后端，支持只使用 `honcho`/`fact_store` 而不是全量注入。 |
| [#38602](https://github.com/NousResearch/hermes-agent/issues/38602) | [Feature]: Desktop Client-Only Installation | **13** | 桌面应用目前强制引导 Hermes 运行时，用户希望支持纯客户端模式连接远程服务。该 Issue 获得 **50 个 👍**，是社区最强呼声之一。 |
| [#63078](https://github.com/NousResearch/hermes-agent/issues/63078) | bug(desktop): first message in a new session leaves a blank session | **9** | 桌面新会话第一条消息导致空白会话，右上角无响应、无错误，严重影响首次使用体验。 |
| [#6174](https://github.com/NousResearch/hermes-agent/issues/6174) | [Bug]: Matrix E2EE device verification fails | **9** | 老问题（4月提交），因影响面广（加密消息完全无法工作）而持续受关注，今日已被关闭。 |
| [#68358](https://github.com/NousResearch/hermes-agent/issues/68358) | Bug: New desktop session message routed into stale TUI session | **7** | 被 `TTFB` 超时后桌面消息错误路由到旧 TUI 会话，导致跨界面会话混乱。 |

## 5. Bug 与稳定性

今日报告的 Bug 中，按严重程度排列如下：

| 严重度 | Issue | 描述 | 状态 | 关联修复 |
|--------|-------|------|------|----------|
| **P1** | [#63078](https://github.com/NousResearch/hermes-agent/issues/63078) | 桌面新会话空白，无消息无响应 | OPEN | 暂无明确 Fix PR，但 #68947/#68949 的租约释放修复可能缓解相关路径。 |
| **P2** | [#67187](https://github.com/NousResearch/hermes-agent/issues/67187) | MCP 服务器重连后工具未注册 | CLOSED | 已修复（sweeper:implemented-on-main） |
| **P2** | [#27683](https://github.com/NousResearch/hermes-agent/issues/27683) | Web 工具因插件未初始化而静默失败 | CLOSED | 已修复 |
| **P2** | [#68358](https://github.com/NousResearch/hermes-agent/issues/68358) | 桌面消息路由到旧 TUI 会话 | OPEN | #68947 针对会话租约的修复可能降低此类漂移概率。 |
| **P2** | [#56776](https://github.com/NousResearch/hermes-agent/issues/56776) | Claude 模型 0% 缓存命中率 | CLOSED | 已修复 |
| **P2** | [#47368](https://github.com/NousResearch/hermes-agent/issues/47368) | 删除配置文件未从磁盘移除 | CLOSED | 已修复 |
| **P2** | [#67762](https://github.com/NousResearch/hermes-agent/issues/67762) | `agent.session_estimated_cost_usd` 在网关重启后重置为 0 | OPEN | 需决策（needs-decision），暂无 PR |
| **P3** | [#68592](https://github.com/NousResearch/hermes-agent/issues/68592) | Cron agent 被强制加上 Kanban 协议导致 `task_id is required` 错误 | OPEN | 新报（2026-07-21） |

今日提交的修复 PR 中也包括：
- [#68948](https://github.com/NousResearch/hermes-agent/pull/68948) — 修复终端后台复合命令重写产生非法 bash 导致 worker 死锁（对应 #68915）
- [#68950](https://github.com/NousResearch/hermes-agent/pull/68950) — 修复 `delegate_task(background=True)` 在子任务完成前返回完成状态
- [#68961](https://github.com/NousResearch/hermes-agent/pull/68961) — 修复多个高严重性三方依赖安全问题

## 6. 功能请求与路线图信号

社区功能请求热度分布清晰，有望被纳入近期路线的包括：

| Issue | 标题 | 点赞 | 说明 |
|-------|------|------|------|
| [#38602](https://github.com/NousResearch/hermes-agent/issues/38602) | Desktop Client-Only Installation | **50 👍** | 社区最强呼声，与 #64182 插件扩展配合可用于构建远程 agent 的薄客户端。 |
| [#47349](https://github.com/NousResearch/hermes-agent/issues/47349) | Configurable Memory Backends | 1 👍 | 虽然点赞数不高（P2），但讨论热度高（13 评论），且是长期用户痛点。 |
| [#13332](https://github.com/NousResearch/hermes-agent/issues/13332) | Hybrid Tool Pre-Selection (Semantic + Keyword) | 4 👍 | 通过 RAG 风格 Schema 注入减少 token 开销（约 14K → ），已有前期提案 #6839。 |
| [#25083](https://github.com/NousResearch/hermes-agent/issues/25083) | Immutable/protected skills | 0 👍 | 用户要求阻止 agent 自主修改关键技能，对应 `skill_manage` 工具的安全性扩展。 |
| [#64182](https://github.com/NousResearch/hermes-agent/issues/64182) | Tracking: Plugin Interface Expansion | 0 👍 | 路线图式的跟踪 Issue，包含多个子项（#64231、#64176、#64204、#64181），可能成为 0.19 版本核心。 |
| [#64900](https://github.com/NousResearch/hermes-agent/issues/64900) | Allow plugins to extend send_message | 0 👍 | 让插件可以为 `send_message` 工具添加平台特定 schema 和处理器。 |

值得注意的是，**插件接口扩展**（#64182 及其子 Issue）在社区 Discord 讨论中已形成共识，Teknium 主导的这批 Issue 很可能会在下一个小版本中集中落地。

## 7. 用户反馈摘要

从 Issue 评论中提炼的真实用户痛点与使用场景：

- **“第一次使用就被空白会话吓到”** — #63078 举报用户在桌面端创建新会话后看到空白界面，怀疑软件安装失败或崩溃。该问题 P1 且发生在核心 UX 路径上，用户不满情绪强烈。
- **“每天都在用 Hermes，Matrix 加密问题持续几个月”** — #6174 用户在 4 月提交后一直等待修复，评论中多个用户表示因此无法在工作群中使用 Hermes。今日关闭后社区表示欣慰。
- **“希望桌面版能独立运行，而不是每次都要先启动一个本地服务”** — #38602 的 50 个 👍 反映了用户对**企业级部署**（远程 agent + 薄客户端）的强烈需求，用户希望在不同设备上共享一个 Hermes 实例。
- **“删除 profile 后它又回来了，感觉像闹鬼”** — #47368 用户在评论中描述了 UI 删除成功但目录残留且重启后重现的诡异行为，该问题今日已修复。
- **“Dashboard 输入不可见就像在用盲打字机”** — #53641 用户在长时间会话后新消息漂移到可视区域上方，必须手动滚动才能看到自己的输入，严重影响工作效率。
- **“飞书卡片的内容无法获取”** — #33090 用户引用飞书卡片消息 @ 机器人，机器人只能拿到标题和摘要，关键内容丢失。该 issue 自 5 月 27 日以来未获官方回复，用户表达了对国际 IM 平台支持不足的失望。

## 8. 待处理积压

以下 Issue 或 PR 长期未获里程碑指派或官方回复，维护者应考虑优先处理：

| 项目 | 类型 | 创建时间 | 最后更新 | 备注 |
|------|------|----------|----------|------|
| [#2788](https://github.com/NousResearch/hermes-agent/issues/2788) | Bug: Cron jobs never run or no useful error info | 2026-03-24 | 2026-07-20 | 已有 6 条评论，P2 但 4 个月未分配决策。 |
| [#33090](https://github.com/NousResearch/hermes-agent/issues/33090) | Bug: 飞书 Gateway 无法获取卡片内容 | 2026-05-27 | 2026-07-21 | P3 且标记 `sweeper:risk-message-delivery`，但无回复。 |
| [#34385](https://github.com/NousResearch/hermes-agent/issues/34385) | Bug: Kanban DB 索引并发损坏（WAL 模式） | 2026-05-29 | 2026-07-21 | P3，`needs-decision`，涉及 Kanban 核心数据安全。 |
| [#34372](https://github.com/NousResearch/hermes-agent/issues/34372) | Bug: BlueBubbles 消息重复处理 | 2026-05-29 | 2026-07-21 | 重复 Issue（已标记 duplicate），但原始问题未关闭。 |
| [#3944](https://github.com/NousResearch/hermes-agent/issues/3944) | Bug: Slack 网关集成失败 — `slack-bolt not installed` | 2026-03-30 | 2026-07-20 | P2，用户通过 curl 脚本安装后报错，部分用户因依赖缺失无法使用 Slack。 |
| [#4335](https://github.com/NousResearch/hermes-agent/issues/4335) | Feature: 跨平台会话上下文共享（CLI ↔ Telegram） | 2026-03-31 | 2026-07-21 | P3，8 条评论，讨论合理但未进入路线图。 |
| [#13332](https://github.com/NousResearch/hermes-agent/issues/13332) | Feature: Hybrid Tool Pre-Selection | 2026-04-21 | 2026-07-21 | P3，已有 8 条评论和 4 个 👍，但缺乏官方回应。 |

**建议**：上述 Issue 中 #2788（Cron 不运行）和 #33090（飞书卡片）应尽快分配责任人并明确修复方向，避免社区对国际平台支持丧失信心；#34385（Kanban 并发损坏）虽标记 P3，但涉及数据持久化风险，建议提升至 P2。

---

*数据截止：2026-07-22 08:00 UTC。所有链接点击可直接跳转 GitHub 原文。*

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 ｜ 2026-07-22

## 1. 今日速览

过去 24 小时项目保持高活跃度：16 个 Issue 产生更新（13 个新开/活跃，3 个关闭），31 个 PR 中有 30 个仍处于开放状态，仅 1 个 PR 完成合并。社区讨论焦点集中在 **ACP（Agent Communication Protocol）凭证生命周期**、**持久化内存** 以及 **OpenAI 兼容网关** 等方向，多个相关 PR 处于评审/待合并阶段，表明项目正密集推进基础设施与稳定性增强。无新版本发布。

## 2. 版本发布

无。

## 3. 项目进展

今日仅合并 1 个 PR，但多个重要 PR 进入可评审状态，标志着关键功能的实质性推进。

### 已合并/关闭的 PR

- **chore(deps): bump laminar to latest version, fix compat issues**  
  作者: @dinmukhamedm  
  更新依赖 `lmnr` SDK 至最新版本并修复兼容性问题。  
  [#4179](https://github.com/OpenHands/software-agent-sdk/pull/4179)

### 已关闭的 Bug Issue（代表修复已完成）

- **fix(acp): preserve refreshed Codex credentials across Cloud conversations**  
  Issue [#4121](https://github.com/OpenHands/software-agent-sdk/issues/4121) 已关闭，对应 ACP 凭证刷新持久化问题得到修复。

### 值得关注的开放 PR（等待合并）

- **feat(acp): add versioned credential bindings**（#4124）—— 解决 Codex 凭证在跨会话中的权威性，标记为“review-this”。
- **feat(agent-server): add GET /api/llm/balance endpoint**（#4154）—— 允许 UI 显示 OpenRouter 信用余额。
- **feat: add opt-in persistent memory across sessions**（#4178）—— 实现跨会话持久化记忆功能（跟踪 #2037）。
- **fix(agent-server): default bind host to loopback without a session API key**（#4180）—— 安全修复，未设置会话 API 密钥时默认绑定到本地回环地址。
- **fix(agent-server): keep secrets out of workspace persistence**（#3990）—— 防止明文凭据泄漏到工作区目录。

> 这些 PR 一旦合并，将显著提升 Agent Server 的安全性、跨会话一致性及可用性。

## 4. 社区热点

今日讨论最活跃的 Issue 集中在 **ACP 协议扩展** 与 **智能体交互能力** 上：

- **[Feature] OpenAI-compatible /v1/chat/completions gateway for the agent-server**（#3540）  
  23 条评论。由 @enyst 的 AI 代理代表提出，建议为 agent-server 添加 OpenAI 兼容的聊天接口，使任意 OpenAI 协议客户端能直接与 OpenHands 智能体交互。诉求清晰：降低集成门槛，扩大生态兼容性。  
  [#3540](https://github.com/OpenHands/software-agent-sdk/issues/3540)

- **[Feature] QuestionTool – let the agent ask the user structured questions mid-task**（#2697）  
  7 条评论。用户 @adityavkk 提出智能体在任务中途遇到歧义时，缺乏结构化提问用户的能力，希望新增 QuestionTool。反映了用户对“人机协作交互粒度”的更高要求。  
  [#2697](https://github.com/OpenHands/software-agent-sdk/issues/2697)

- **Proposal: extend defense_in_depth PatternSecurityAnalyzer**（#3176）  
  12 条评论。@eeee2345 提议扩展安全分析器以覆盖更多 Agent 威胁模式（如 curl-pipe-sh 等），社区在讨论签名设计的平衡性。  
  [#3176](https://github.com/OpenHands/software-agent-sdk/issues/3176)

- **Track the Codex subscription credential lifecycle across ACP conversations**（#4169）  
  由 @simonrosenberg 创建，当天即产生 6 个子 Issue，显示社区对 ACP 凭证生命周期管理的高度关注。  
  [#4169](https://github.com/OpenHands/software-agent-sdk/issues/4169)

## 5. Bug 与稳定性

当日报告多个 Bug，按严重程度排列如下：

| 严重度 | Issue | 摘要 | 已有 Fix PR |
|--------|-------|------|-------------|
| **高** | [#4170](https://github.com/OpenHands/software-agent-sdk/issues/4170) | Phase 1: 顺序 ACP 会话中 Codex 凭证未传播，导致后续会话认证失败 | 是（#4177 规划，#4124 待合并） |
| **高** | [#4171](https://github.com/OpenHands/software-agent-sdk/issues/4171) | Phase 2: 多个并发 ACP 会话同时刷新凭证时出现竞争条件 | 规划中 |
| **高** | [#3532](https://github.com/OpenHands/software-agent-sdk/issues/3532) | gemini-cli 0.45.x 忽略 `set_session_model`，初始模型未生效，导致 404 | 无 |
| **中** | [#4121](https://github.com/OpenHands/software-agent-sdk/issues/4121) | Codex 凭证在 Cloud 会话间刷新后丢失（**已关闭**，已修复） | 已合并 |
| **中** | [#3991](https://github.com/OpenHands/software-agent-sdk/issues/3991) | Webhook 速率限制导致任务挂起，409 冲突无法自动恢复 | [#3991](https://github.com/OpenHands/software-agent-sdk/pull/3991) 开放中 |
| **低** | [#3990](https://github.com/OpenHands/software-agent-sdk/issues/3990) | 工作区 settings.json 中含有明文凭据 | [#3990](https://github.com/OpenHands/software-agent-sdk/pull/3990) 开放中 |

> 核心风险集中在 ACP 凭证延迟/并发问题上，已有多位贡献者投入修复。

## 6. 功能请求与路线图信号

以下新功能请求近期呼声高，且已有对应 PR 或详细设计文档，很可能进入下一版本：

- **OpenAI 兼容网关**（#3540）：打开 LLM 生态对接，社区关注度高。
- **跨会话持久化记忆**（#2037，PR #4178、#2810）：已有多项实践，PR #4178 今日新开，预示即将落地。
- **QuestionTool**（#2697）：提升智能体交互主动性，已有讨论但尚无 PR，可能后续进入路线图。
- **Agent Server 端 telemetry**（#4172）：添加产品分析遥测，满足运营需求。
- **自动加载独立 Marketplace Skills**（#4176）：改善云部署体验。
- **LLM 余额查询接口**（#4154）：提升用户可见性。
- **支持 run-scoped LLM extra headers**（#4064）：方便嵌入场景附加元数据。
- **通用 ACP session 配置选项暴露**（#4062）：增强协议灵活性。

## 7. 用户反馈摘要

从 Issues 评论中提炼出以下真实用户声音（直接引用或转述）：

> **“When Codex rotates auth.json in a conversation, the next conversation gets the old secret – authentication fails silently.”**  
> —— @neubig 在 [#4121](https://github.com/OpenHands/software-agent-sdk/issues/4121) 中描述 ACP 凭证丢失场景，该问题已修复。

> **“gemini-cli 0.45.1 ignores set_session_model, always runs built-in gemini-3-flash, causing 404 on Vertex.”**  
> —— @simonrosenberg 在 [#3532](https://github.com/OpenHands/software-agent-sdk/issues/3532) 中报告模型选择无效，影响 Vertex AI 用户。

> **“When the agent hits genuine ambiguity mid-task, it has no structured way to ask the user – it either guesses or fails.”**  
> —— @adityavkk 在 [#2697](https://github.com/OpenHands/software-agent-sdk/issues/2697) 中表达对结构化提问的迫切需求。

> **“We caught the trigger in the wild: app server rate-limits its own sandbox webhook (429), stock poster gives up, the transcript freezes, and the lingering run task answers 409 forever.”**  
> —— @shanemort1982 在 [#3991](https://github.com/OpenHands/software-agent-sdk/issues/3991) 中描述 webhook 限速导致任务永久挂起的生产级故障。

整体反馈表明，用户对 ACP 稳定性、模型兼容性、人机交互粒度和异常恢复有较高期待。

## 8. 待处理积压

以下 Issue/PR 长期未获得核心维护者响应或合并，可能影响项目健康度：

| 类目 | 标识 | 创建时间 | 备注 |
|------|------|----------|------|
| Issue | [Memory: Persistent auto-learning across sessions](https://github.com/OpenHands/software-agent-sdk/issues/2037) | 2026-02-13 | 核心功能，已有 PR #2810，但数月未合并 |
| PR   | [Memory: Research & Implementation Plan](https://github.com/OpenHands/software-agent-sdk/pull/2810) | 2026-04-13 | 同上，需推动 |
| Issue | [Feature: QuestionTool](https://github.com/OpenHands/software-agent-sdk/issues/2697) | 2026-04-03 | 无对应 PR，社区讨论已趋于冷淡 |
| PR   | [feat: propagate per-server MCP timeout](https://github.com/OpenHands/software-agent-sdk/pull/3254) | 2026-05-14 | 等待 review 两个月以上 |
| PR   | [fix: write and read installation metadata as utf-8](https://github.com/OpenHands/software-agent-sdk/pull/3336) | 2026-05-20 | 小修复，长期未合并 |
| PR   | [fix(sdk): respect subscription validator composition](https://github.com/OpenHands/software-agent-sdk/pull/3953) | 2026-07-02 | 需维护者决策 |
| PR   | [fix(agent-server): survive webhook rate limiting](https://github.com/OpenHands/software-agent-sdk/pull/3991) | 2026-07-04 | 生产级问题修复，应优先合并 |
| PR   | [fix(agent-server): keep secrets out of workspace persistence](https://github.com/OpenHands/software-agent-sdk/pull/3990) | 2026-07-04 | 安全相关，建议加速 |

> 建议维护团队在本周内对上述积压进行 triage，尤其关注影响安全与稳定性的 PR（#3990、#3991）以及长期停滞的核心功能（#2037/#2810）。

---

**报告生成时间**：2026-07-22  
**数据源**：GitHub repository OpenHands/software-agent-sdk，过去 24 小时活动。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，以下是根据您提供的 Pi 项目数据生成的 2026-07-22 项目动态日报。

---

# Pi 项目日报 | 2026-07-22

### 1. 今日速览

Pi 项目今日维护活跃度极高，社区贡献与问题修复并行。过去24小时内，团队成功解决了大部分积压问题（关闭了53个 Issues 和 15个 PRs），效率显著。两个新版本的发布（v0.81.0, v0.81.1）为项目引入了关键的本地模型管理能力和更安全的发布流程。社区讨论热点集中在本地 LLM 集成、模型兼容性以及自托管提供者的连接稳定性上。总体来看，项目正处于快速迭代、注重稳定性与用户体验改善的良性阶段。

### 2. 版本发布

**v0.81.1**
- **链接**: https://github.com/earendil-works/pi/releases/tag/v0.81.1
- **主要内容**: 新增 **可验证的发布源归档**。现在 GitHub Release 包含确定性、带校验和的源代码归档，并附有从源码构建独立二进制文件的说明。这极大地增强了软件供应链的透明度和安全性，是项目迈向成熟的重要一步。
- **破坏性变更**: 无。
- **迁移注意事项**: 无。这是一个正向增强，不影响现有功能。

**v0.81.0**
- **链接**: https://github.com/earendil-works/pi/releases/tag/v0.81.0
- **主要内容**: 引入 **本地 llama.cpp 模型管理**。允许用户连接到本地运行的 llama.cpp 路由，搜索并下载 Hugging Face 上的模型，并支持显式加载/卸载模型，带有实时进度显示。这对于希望完全离线运行或使用开源模型的用户而言是一项核心功能。
- **破坏性变更**: 无。
- **迁移注意事项**: 这是新增功能，用户可通过 `pi --list-models` 查看新支持的模型。首次使用需先配置并运行本地 llama.cpp 服务。

### 3. 项目进展

今日合并/关闭了多个重要 PR，显著提升了项目的健壮性和功能性：
- **稳定性修复**: 修复了因 OpenAI/Anthropic SDK 的 `Retry-After` 机制导致的进程假死问题（PR #6912），并修复了 `wl-copy` 在沙箱环境下的错误成功反馈（PR #6925）。合并了对 `brace-expansion` 依赖的紧急安全更新（PR #6896）。
- **功能迭代**: 添加了 `/resume` 会话选择器的 `Ctrl+A` 归档快捷键（PR #6917），以及会话 ID 稳定化机制（PR #6909），为更复杂的会话管理奠定基础。
- **流程改进**: 实现并验证了可验证的发布源归档流程（PR #6913），并修复了 CI 中的 flaky 测试（PR #6905）。同时，对内部命名进行了清理（如 “orchestrator” 重命名为 “server”），体现了代码库的持续工程化提升。
- **关键进展**: 针对紧急的 v0.81.0 崩溃问题（Issue #6915），虽然 Issue 已关闭，但相关修复逻辑大概率已纳入版本。针对 Compaction 失败无重试的问题，多个 PR（如 #6901, #6775）已被关闭，表明该逻辑已得到修复。

### 4. 社区热点

- **官方本地 LLM 提供者扩展 (#3357)**
  - **链接**: https://github.com/earendil-works/pi/issues/3357
  - **热度**: 30条评论, 43个 👍
  - **分析**: 作为历史上最受关注的功能请求之一，此 Issue 探讨了如何动态获取本地模型列表。其高热度直接催生了今日 v0.81.0 中 `llama.cpp` 的集成。它反映了社区对摆脱云端依赖、拥抱开源模型的强烈诉求。

- **新版 Claude 模型编辑工具兼容性问题 (#6278)**
  - **链接**: https://github.com/earendil-works/pi/issues/6278
  - **热度**: 23条评论, 9个 👍
  - **分析**: 用户报告 Claude 新模型在使用 Pi 的编辑工具时，约20%的编辑会因生成无效字段而失败。这揭示了 Pi 的 “edit” 工具对模型输出的格式校验较为严格，而不同模型/版本的行为存在差异。维护者可能需要考虑更宽松的解析策略或增加模型特定的适配层。

- **移除 Shrinkwrap 的讨论 (#5653)**
  - **链接**: https://github.com/earendil-works/pi/issues/5653
  - **热度**: 19条评论
  - **分析**: 此 Issue 讨论了因 npm 包 `shrinkwrap` 导致的依赖重复和模块状态不一致问题。这触及了包管理的核心，长期的讨论表明维护者正在认真权衡是否应放弃 `shrinkwrap` 以换取更简洁的依赖结构和更好的插件兼容性，这可能会是未来的一个重大架构变更。

### 5. Bug 与稳定性

- **【严重 - 已修复】更新至 v0.81.0 后崩溃 (#6915)**:
  - **链接**: https://github.com/earendil-works/pi/issues/6915
  - **描述**: 用户在恢复会话时，因 `streamFunction is not a function` 导致崩溃。此 Bug 影响升级后用户的正常使用。
  - **状态**: 已关闭（CLOSED），表明已通过热修复或后续小版本解决。

- **【严重】自托管模型超时回归 (#6476)**:
  - **链接**: https://github.com/earendil-works/pi/issues/6476
  - **描述**: 自 v0.80.6 起，用户自定义的 `httpIdleTimeoutMs` 设置不再对自托管 OpenAI 兼容 API 生效，导致请求提前超时。
  - **状态**: 开放中（OPEN），社区正等待修复。

- **【高】OpenAI SDK 重试机制导致进程无响应 (#6911)**:
  - **链接**: https://github.com/earendil-works/pi/issues/6911
  - **描述**: 当 API 返回长时间的 `Retry-After` 头时，SDK 的重试会陷入长时间睡眠且无法通过 `Escape` 取消，导致 Pi 假死。
  - **状态**: 已关闭（CLOSED）。对应修复 PR #6912 也已合并。

- **【中】`pi update --self` 无重试机制 (#6675)**:
  - **链接**: https://github.com/earendil-works/pi/issues/6675
  - **描述**: 自更新因一次性的网络波动而失败，缺乏重试机制，用户体验不佳。
  - **状态**: 开放中（OPEN）。

- **【中】macOS 下 TUI 渲染宽度计算错误 (#6704)**:
  - **链接**: https://github.com/earendil-works/pi/issues/6704
  - **描述**: 在特定终端宽度下，输入框宽度计算出现 “off-by-one” 错误，触发断言导致 TUI 崩溃。
  - **状态**: 已关闭（CLOSED），标记为 “no-action”，可能已在下游修复。

- **【低】Beta 广告注销导致模型选择错误 (#6748)**:
  - **链接**: https://github.com/earendil-works/pi/issues/6748
  - **描述**: 内置的 Together.ai 模型列表中仍包含已废弃的 Beta 模型，误导用户选择。
  - **状态**: 已关闭（CLOSED）。

### 6. 功能请求与路线图信号

- **扩展能力增强**:
  - **Agent 消息 Markdown 增强 API (#6747)**: 允许扩展修改消息展示形式，但不影响发送给 LLM 的内容。这为UI自定义打开了大门，如支持公式渲染等。很可能进入下一版本迭代。
  - **请求延迟规范重载 (#6552)**: 允许扩展请求一个“延迟的”规范重载，解决了某些场景下无法安全重载的问题。这是对扩展生态系统的必要补充。

- **新提供商集成**:
  - **Amazon Bedrock Mantle 支持 (PR #6216)**: 一个新的提供商 PR 正在等待合并，为使用 AWS Bedrock Mantle 服务的用户提供原生支持。
  - **OpenRouter OAuth 支持 (PR #6927)**: 增加了原生的 OpenRouter OAuth 登录流程，简化了用户的 API 密钥管理。
  - **Kimi Code OAuth 登录 (#6870)**: 社区提议为 Kimi Code 提供 OAuth 登录，对订阅用户友好。虽然已关闭，但提案内容具有价值。

- **平台支持改进**:
  - **Termux 安装文档 (#6899)**: 社区贡献了通过 Termux glibc-runner 安装 Linux arm64 二进制文件的方法，提升了在 Android 设备上的使用体验。

### 7. 用户反馈摘要

- **对本地模型支持的热切期盼**: 从今日多个讨论中（#3357, #6278）可以看出，用户对集成并稳定使用本地/开源 LLM（如通过 llama.cpp、Ollama 等）有非常强烈的需求。v0.81.0 的发布直接回应了这一诉求。
- **版本升级带来的创伤**: #6915 和 #6476 显示，部分用户在新版本升级后遇到了严重的兼容性或回归问题，影响了工作流。这要求项目在发布前加强测试，并提供更平缓的升级指南。
- **对更新机制的吐槽**: #6675 的反馈“`pi update --self` 有时会失败”非常直接，暴露了当前更新逻辑不够健壮。用户期望任何关键操作都应有重试机制以应对短暂的网络故障。
- **对安全性和依赖管理的关注**: #6882 关于更新 `brace-expansion` 依赖的 Issue 显示了社区对供应链安全的高度敏感，并能主动识别并报告安全风险。

### 8. 待处理积压

- **【核心架构】移除 Shrinkwrap (#5653)**:
  - **链接**: https://github.com/earendil-works/pi/issues/5653
  - **说明**: 该 Issue 已开放超过一个月，讨论了包管理器的核心问题，但解决方案尚未定论。随着插件生态扩大，依赖复制的矛盾会更加突出，需要维护者尽快做出决策。

- **【用户体验】Tab 补全会话命令时插入多余空格 (#5593)**:
  - **链接**: https://github.com/earendil-works/pi/issues/5593
  - **说明**: 一个存在已久的交互细节 Bug。在补全斜杠命令时自动追加的空格，阻止了后续的参数补全。此问题虽小，但对日常使用频率高，影响流畅性。

- **【多平台】Windows 文件路径模式匹配错误 (#6817)**:
  - **链接**: https://github.com/earendil-works/pi/issues/6817
  - **说明**: Windows 用户反馈 `find` 工具无法匹配带路径分隔符的模式，这是对非 Unix 平台支持的一个明显盲点。虽然评论数不多，但严重影响了 Windows 用户的核心功能使用。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

好的，请查收这份基于您提供的 GitHub 数据生成的 LiteLLM 项目动态日报。

---

# LiteLLM 项目动态日报 | 2026-07-22

## 1. 今日速览

**项目活跃度：极高**
今日项目更新极为密集，共处理 70 个 Issue 与 246 个 Pull Request，显示出社区与核心团队的极高参与度。PR 的合并/关闭数量（108）显著高于 Issue 关闭数（18），表明项目团队在推进代码合并和功能落地方面投入了大量精力。然而，待合并 PR 积压（138）和新开 Issues（52）数量均较高，健康度虽有强劲的基础但面临一定的审查和响应压力。
- **核心信号**：项目正处于高速迭代期，功能开发和问题修复并行推进，但版本发布暂停，可能是在为下一个大版本做积蓄。

## 2. 版本发布

*（无更新）*

## 3. 项目进展

今日项目在功能、自动化及底层依赖方面有若干重要推进，合计合并/关闭 108 个 PR，展示了显著的实质性进展。

- **代理配置灵活性增强**：PR [#34130](https://github.com/BerriAI/litellm/pull/34130)（已合并）使数据库配置重载间隔变为可配置参数，允许运维人员根据自身需求调整代理的配置热加载频率，提升了对动态配置场景的支持。
- **UI 基础设施升级与重构**：团队在 UI 方面动作频繁。PR [#34170](https://github.com/BerriAI/litellm/pull/34170)（已合并）引入了 `react-hook-form` + `zod` 的表单验证基础架构，为后续更健壮、更统一的 Web UI 交互奠定基础。同时，PR [#34169](https://github.com/BerriAI/litellm/pull/34169)（已合并）对 MCP、回调、防护等模块的 Logo 展示进行了组件化重构，提升了 UI 的维护性和一致性。
- **测试体系与自动化**：测试覆盖面进一步扩大。PR [#34175](https://github.com/BerriAI/litellm/pull/34175) 与 [#34052](https://github.com/BerriAI/litellm/pull/34052)（均为开放状态）分别新增了 UI 单元测试和 A2A Agent 端到端测试，后者由 AI 自动生成，显示出团队在测试自动化上的创新尝试。PR [#34166](https://github.com/BerriAI/litellm/pull/34166)（开放）则提议增加对真实提供商的周级异常负载测试，旨在提升系统的生产环境可靠性。
- **企业级特性打磨**：PR [#34162](https://github.com/BerriAI/litellm/pull/34162)（开放）旨在修复 SCIM 组权限同步问题，将 `members_with_roles` 作为真实组员来源，这对于依赖 SCIM 进行权限管理的企业用户至关重要。
- **依赖维护**：PR [#34168](https://github.com/BerriAI/litellm/pull/34168)（已合并）将 `gitpython` 依赖升级至 3.1.52；PR [#33284](https://github.com/BerriAI/litellm/pull/33284)（开放）提议对 GitHub Actions 依赖包（`actions/checkout`等）进行大规模（19个）更新，以跟上 CI/CD 工具链的安全与功能迭代。

## 4. 社区热点

- **热度最高：UI 暗色模式的呼声**：[Issue #10177](https://github.com/BerriAI/litellm/issues/10177)（开放，58 评论，68 👍）是关于“暗色模式”的请求。作者以“I‘m going blind”直白地表达了当前亮色 UI 对用户视力的困扰。该 Issue 获得大量点赞和讨论，反映出社区对提升管理后台可访问性和视觉体验的强烈需求。尽管该 Issue 并非今日新开，但持续的热度使其成为社区的焦点。
- **历史遗留：用户心愿单**：[Issue #361](https://github.com/BerriAI/litellm/issues/361)（已关闭，471 评论）是一个用户长期累积的需求收集帖，尽管今日无新评论，但其庞大的讨论量依然是社区需求的重要风向标。它表明社区对项目的参与度和贡献意愿很高，但其中许多建议是否已由后续版本满足或纳入路线图，值得团队梳理和跟进。

## 5. Bug 与稳定性

今日报告的 Bug 呈现多样化，部分问题较为严重，涉及代理可靠性和核心功能路径。

- **【严重】预算控制路径缺失**：[Issue #34101](https://github.com/BerriAI/litellm/issues/34101)（开放）指出“项目预算”未纳入原子性预调用预算预留流程。这意味着对于拥有多个项目的大客户，预算超限风险可能无法被精准控制，是潜在的财务风险点。
- **【高】端点信息遗漏与不一致**：[Issue #33347](https://github.com/BerriAI/litellm/issues/33347)（开放）指出新的 `/v2/user/info` 接口遗漏了用户的 `rpm_limit` 和 `tpm_limit` 信息；[Issue #20999](https://github.com/BerriAI/litellm/issues/20999)（关闭）则报告了 `/model/info` 返回数据不一致的问题。这两个 Bug 直接影响了管理员对用户和模型状态的精确监控。
- **【高】代理健康检查与级联故障**：[Issue #26066](https://github.com/BerriAI/litellm/issues/26066)（开放）揭示了针对 Azure Responses API 的健康检查使用了错误的格式，导致误报不健康状态。[Issue #15526](https://github.com/BerriAI/litellm/issues/15526)（关闭）则报告了在高负载下，因上游提供商 429 错误导致代理 Pod 健康检查失败并引发级联重启的严重可靠性问题，虽然已关闭，但其暴露的架构风险值得关注。
- **【中】数据泄露风险**：[Issue #32202](https://github.com/BerriAI/litellm/issues/32202)（开放）报告了一个严重的安全缺陷：当启用 `forward_headers: true` 时，`pass_through_endpoints` 会错误地将代理自身的 `Authorization` 头（API Key）转发给下游，导致密钥泄露，且未按文档说明移除 `x-pass-` 前缀。这是一个明确的配置与安全漏洞。
- **【低】** 其他 Bug 还包括工具调用失败（[#22637](https://github.com/BerriAI/litellm/issues/22637)，[#26156](https://github.com/BerriAI/litellm/issues/26156)）、成本计算问题（[#20228](https://github.com/BerriAI/litellm/issues/20228)）等，均与特定模型或供应商集成相关。

## 6. 功能请求与路线图信号

- **对多模型与高级路由的持续渴望**：用户对更精细的成本归属（[#26159](https://github.com/BerriAI/litellm/issues/26159)）和多后端路由（PR [#33340](https://github.com/BerriAI/litellm/pull/33340)）功能表现出兴趣。这表明社区对 LiteLLM 作为“LLM 网关”的核心价值非常认可，希望其路由和成本分析能力不断增强。
- **新时代模型与架构的支持**：对 Google Gemma-4 的官方支持请求（[#25489](https://github.com/BerriAI/litellm/issues/25489)）和 Moonshot Kimi K2.6 的 Bug 报告（[#26156](https://github.com/BerriAI/litellm/issues/26156)），表明社区正积极将 LiteLLM 用于最新的前沿模型。同时，MCP（Model Context Protocol）相关 PR（[#33190](https://github.com/BerriAI/litellm/pull/33190)）的活跃，预示未来可能在 Agent 互联和工具调用生态上有更深布局。
- **企业级增强**：Azure 无密码认证（PR [#30633](https://github.com/BerriAI/litellm/pull/30633)）和 SCIM 组同步修复（PR [#34162](https://github.com/BerriAI/litellm/pull/34162)）的提出，明确指向了企业用户在安全性和权限管理上的核心需求，这很可能被纳入即将到来的版本。

## 7. 用户反馈摘要

- **对 UI 改进的急切期待**：用户“I’m going blind”（详见 Issue #10177）这一幽默而直白的评论，是今日最突出的用户反馈，核心诉求是提升管理后台的可用性和视觉舒适度。
- **对代理可靠性的深切关注**：[Issue #15526](https://github.com/BerriAI/litellm/issues/15526) 中描述的因上游限流导致代理“级联崩溃”的场景，真实地反映了生产环境中用户对代理稳定性的严苛要求。用户期望代理不仅是功能转换层，更是一个健壮、能够优雅处理上游故障的“保险”。
- **配置与预期的偏差**：多个 Bug 报告（如 [#32202](https://github.com/BerriAI/litellm/issues/32202) 的头部泄露、[#26066](https://github.com/BerriAI/litellm/issues/26066) 的健康检查误报）都指向了文档描述与实际行为不符的情况，让用户在配置时产生困惑，甚至带来安全风险。用户期望配置行为能有更高的可预期性和一致性。
- **对未来功能的明确兴趣**：有用户明确提出了对“Token级成本归属”（[#26159](https://github.com/BerriAI/litellm/issues/26159)）的需求，这反映了大型团队或 MLOps 团队在成本分摊和优化方面的成熟需求。

## 8. 待处理积压

- **长期“静默”的关键 Bug**：
  - [[bug] cpu utilization is high when streaming](https://github.com/BerriAI/litellm/issues/13505)：该 Bug 报告于近一年前，涉及核心流式推理性能问题（CPU 占用率高达 75%），对高吞吐生产环境至关重要，但目前仍标记为 `stale` 且处于开放状态。建议维护者评估其优先级。
  - [[Bug] Bedrock Converse fails with parallel_tool_calls on Claude 4.5+](https://github.com/BerriAI/litellm/issues/22637)：影响最新的 Claude 4.5 模型工具调用功能，阻碍用户使用前沿模型，同样处于开放状态。
- **未关联 issue 的大型新功能 PR**：
  - [feat: multi-backend Anthropic passthrough with health-aware routing](https://github.com/BerriAI/litellm/pull/33340)：这是一个由社区贡献者提出的、复杂度较高且与项目核心路由功能紧密相关的新功能 PR（多后端 Anthropic 传递与健康感知路由）。它的合并将为需要在多个 Anthropic 账户/端点间负载均衡的用户带来巨大价值，但需要核心团队投入大量审查精力。

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 Temporal 项目数据，生成 2026-07-22 的客观专业日报。

---

### Temporal 项目动态日报 | 2026-07-22

**项目整体状态：** 项目在 7 月 21 日表现极为活跃，尤其在 Pull Request 方面达到了近期峰值，显示了高强度迭代和快速响应社区问题的能力。虽然当天无新版本发布，但大量待合并的 PR 和已关闭的热修复表明项目正同时推进多个功能开发与稳定性修复。社区围绕调度器、成员管理和内存泄漏等核心领域展开了深度讨论。

#### 1. 今日速览

- **开发活跃度极高**：过去 24 小时内 PR 处理量高达 75 条，其中 `53` 条等待合并，暗示即将有大批功能与修复落地。
- **双线作战**：社区既在积极解决长期存在的性能问题（如 `#6323` 内存泄漏），也在快速响应升级后发现的回归问题（如 `#9987`）。
- **Scheduler 重写进入攻坚期**：多条涉及 `CHASM`（基于 Nexus 的新调度器）、Backfill 和迁移的 PR 同时推进，表明调度器架构重构是当前开发重点。
- **稳定性警报**：新披露的 `#112` 系列 Issue 指出历史服务在处理队列积压时存在竞态条件崩溃，需密切关注其修复进展。

#### 2. 版本发布

无新版本发布。

#### 3. 项目进展

今日有 22 个 PR 被合并或关闭，有效推动了项目在以下方面的进展：

- **热修复与回归修复**：
    - `#11187` & `#11185`: 紧急合并了两条针对全局命名空间集群移除操作的 **热修复** PR，以应对昨日报告的线上事故，显示了项目对生产环境稳定性的高度重视。
    - `#11163`: 修复了调度器在取消/终止工作流时错误地触发了 `PauseOnFailure` 逻辑的问题，这是对调度器行为的精细化调整。
    - `#11190`: 合并了对 `sqlparser` 依赖的更新，并同步回溯到 `v1.31.3`, `v1.30.7`, `v1.29.8` 多个维护分支，体现了对长期支持版本的维护承诺。
    - `#11137`: 修复了独立活动在重试截止时间时的超时类型报告问题，使其正确上报 `SCHEDULE_TO_CLOSE`，提高了故障诊断的准确性。
- **功能与非功能性改进**：
    - `#11132`: 对 `Matching` 服务的动态分区客户端进行了重构，旨在简化代码并提高 `matching->matching` 转发的性能，是重要的基础设施优化。

**总结：** 项目团队在解决紧急线上问题方面响应迅速，同时保持了对核心功能和基础设施的持续打磨，项目整体向前迈出了稳健的一步。

#### 4. 社区热点

- **调度器(Scheduler) 重构讨论集群 (多条 PR)**
    - 链接: [#11162](https://github.com/temporalio/temporal/pull/11162), [#11165](https://github.com/temporalio/temporal/pull/11165), [#11191](https://github.com/temporalio/temporal/pull/11191), [#11192](https://github.com/temporalio/temporal/pull/11192), [#11193](https://github.com/temporalio/temporal/pull/11193), [#11197](https://github.com/temporalio/temporal/pull/11197), [#11198](https://github.com/temporalio/temporal/pull/11198)
    - **分析**：今日评论数最多的虽未公布，但从 PR 数量看，调度器（Scheduler）无疑是今日的绝对焦点。社区核心贡献者 `@davidporter-id-au` 提交了关于 Backfill 逻辑边界条件的修复，而 `@chaptersix` 则提交了多条关于 Scheduler V1 到 V2 迁移的边界修复。这组 PR 涉及 Backfill、暂停逻辑、截止时间边界、迁移时的回调与游标处理等复杂细节，表明社区正全力打磨新调度器（CHASM）的可靠性和兼容性，这是当前最核心的技术挑战。
- **长期未决的内存泄漏问题获新关注 (`#6323`)**
    - 链接: [#6323](https://github.com/temporalio/temporal/issues/6323)
    - **分析**：此 Issue 创建于 2024 年，但在近两天仍有更新，且获得 16 条评论。用户 `@uritig` 报告了 Frontend Service 的 Goroutine 和内存泄漏，可能导致服务最终中断。这个长期悬而未决的关键性能问题持续受到社区关注，是社区对高负载下系统稳定性的核心忧虑。

#### 5. Bug 与稳定性

**严重级别：高**
- **Issue `#112` - 历史服务队列竞态条件崩溃 (潜在 Bug)**
    - 链接: [#11188](https://github.com/temporalio/temporal/issues/11188)
    - 描述：用户 `@roshchha` 报告，当 `history.queuePendingTaskCriticalCount` 阈值被触发后，队列缓解逻辑 (`actionQueuePendingTask`) 会导致历史服务崩溃。
    - 状态：**无评论，无关联 PR，应视为紧急问题。** 需项目组确认并优先处理。
- **Issue `#6323` - Frontend 服务 Goroutine 与内存泄漏 (潜在 Bug)**
    - 链接: [#6323](https://github.com/temporalio/temporal/issues/6323)
    - 描述：自 2024 年报告的堆内存持续增长，导致 CPU 和内存占用缓慢上升并最终引发服务中断。
    - 状态：**长期未解，仍需关注。** 暂无明确修复方案。

**严重级别：中**
- **Issue `#9987` - 升级到 v1.30.x 后的 Ringpop 成员关系紊乱 (潜在 Bug)**
    - 链接: [#9987](https://github.com/temporalio/temporal/issues/9987)
    - 描述：用户 `@shankarkc` 报告从 v1.29.x 升级后，集群成员（Frontend, History 等）无法正确收敛。
    - 状态：**有 8 条评论，近期活跃。** 问题未被完全解决，可能是影响用户升级路径的关键障碍。
- **Issue `#11051` - Matching 服务任务队列分区管理器泄漏 (潜在Bug，已关闭)**
    - 链接: [#11051](https://github.com/temporalio/temporal/issues/11051)
    - 描述：用户 `@harrisleesh` 发现并发加载同一任务队列时，竞态失败的管理器未被释放，导致内存泄漏。
    - 状态：**已关闭**。表明该问题已被修复，是提升稳定性的积极信号。

#### 6. 功能请求与路线图信号

- **增强成员管理的可观测性 (`#11146`)**
    - 链接: [#11146](https://github.com/temporalio/temporal/issues/11146)
    - 信号强度：强。此功能请求直接关联到近期修复的 `#10730`（路由至draining成员），旨在暴露每个服务的 reachable/available/draining 成员指标。这**很可能被纳入后续版本**，作为提升运维能力、解决灰度重启问题的关键一环。
- **调度器功能增强：**
    - `#11171`: **每会话最大跳过次数**，为时间跳跃功能增加细粒度控制。
    - `#11198`: **Scheduler 使用 CHASM WithRequestID**，为调度器更新操作提供幂等性保证。
    - `#10999`: **新增 `partition_scale_target` 指标**，提升动态分区伸缩过程的透明度。
    - **上述调度器相关 PR 的密集提交，强烈暗示一个全新的、功能更完善的调度器版本（基于 CHASM）正接近完成，其包含的诸多改进很可能随下一大版本发布。**

#### 7. 用户反馈摘要

- **升级降级体验受阻**：`#9987` 的用户 `@shankarkc` 明确表达了在升级到 `v1.30.x` 后遇到成员关系紊乱的困扰，这直接影响了用户安全升级的信心。虽然没有抱怨，但其“问题描述”中详细期望的“收敛秒级”行为未能实现，构成了隐性的不满。
- **运维监控需求迫切**：`#11146` 的用户 `@wankhede04` 在调查 `#10730` 和 `#11108` 时，发现了缺乏运营视角监控指标的痛点，这反映了大型企业用户对集群可观测性（特别是灰度发布与故障排除场景）的强烈需求。
- **高负载场景稳定性是核心痛点**：`#6323` 和已修复的 `#11051` 本质上都指向了系统在并发压力下的资源管理问。用户 `@uritig` 和 `@harrisleesh` 的反馈表明，对于高吞吐、长时间运行的 Temporal 集群，内存泄漏和资源竞争是造成重大故障的首要风险。

#### 8. 待处理积压

- **`#6323` - Frontend 服务 Goroutine 与内存泄漏**
    - 链接: [#6323](https://github.com/temporalio/temporal/issues/6323)
    - 提醒：该问题从 2024 年 7 月 22 日报告至今已近两年，被标记为 `potential-bug` 且有 16 条评论。尽管可能有部分隐性修复，但问题本身未被明确关闭。作为影响 Frontend 服务的关键稳定性问题，建议维护团队给予更高优先级，更新状态或给出明确的修复路线图，以安抚社区用户。
- **`#607` - 为 `parentclosepolicy` 工作流添加测试**
    - 链接: [#607](https://github.com/temporalio/temporal/issues/607)
    - 提醒：这是一个标记为 `good first issue` 和 `testing` 的 Issue，创建于 2020 年。虽非高优先级 Bug，但长期挂起容易让社区感到维护者对此类基础质量保障工作不够重视。若此类需求有专人认领或标记为“已计划”，将有助于提升项目健康度。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*