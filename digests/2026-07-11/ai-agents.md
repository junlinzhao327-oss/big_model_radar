# OpenClaw 生态日报 2026-07-11

> Issues: 407 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-10 22:36 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我将根据您提供的 OpenClaw 项目数据，为您呈现 2026-07-11 的项目动态日报。

---

### OpenClaw 项目动态日报 | 2026-07-11

---

#### 1. 今日速览

OpenClaw 项目今日继续保持极高的活跃度，24小时内共有超过900条 Issues 和 PR 的更新。社区讨论焦点集中于内存泄漏、会话状态丢失、嵌入式提示缓存（prompt cache）跨边界失效等关键稳定性问题，以及大量围绕 Slack Block Kit、WhatsApp 贴纸、文件沙箱等功能增强的讨论。尽管无新版本发布，但项目在修复遗留任务状态、优化 Discord 插件重连机制方面取得了实质进展。整体看，项目处于密集开发与维护期，急需解决数个 P0/P1 级别的严重 Bug。

---

#### 2. 版本发布

无新版本发布。

---

#### 3. 项目进展

今日项目主要推进了以下修复工作，提升了稳定性和兼容性：

- **修复遗留任务状态**：PR [#103946](https://github.com/openclaw/openclaw/pull/103946) 修复了从遗留侧载（sidecar）升级任务状态时，因 `delivery_status` 值不匹配导致所有持久化任务丢失的问题。此修复解决了用户在升级过程中的数据迁移痛点，保护了任务数据的完整性。
- **优化 Discord 插件重连**：虽然相关 Issue `#99681` 今日关闭，但之前已有 PR 被合并或正在处理中。这解决了 Discord Bot 因 WebSocket 异常断开（1006）后无法自动重连，导致需要重启整个网关（Gateway）并杀死正在执行任务的严重问题。
- **修复 Windows 环境兼容性**：PR [#103907](https://github.com/openclaw/openclaw/pull/103907) 修复了 Windows 开发环境中脚本 `run-with-env.mjs` 可能错误引用 PATH 中不同 Node.js 版本的问题，提升了跨平台开发的体验。
- **优化 ACP 启动流程**：PR [#103958](https://github.com/openclaw/openclaw/pull/103958) 修复了当 ACP 后端（如 OpenCode）未声明支持 `thinking` 配置时，`sessions_spawn` 启动失败的问题，增强了与不同后端的兼容性。

这些进展表明，项目正积极应对用户报告的数据迁移、平台兼容性及核心插件稳定性问题。

---

#### 4. 社区热点

今日讨论最热烈、关注度最高的议题集中反映了社区对**核心稳定性**和**功能交互体验**的深切关注：

1.  **工具输出图像化导致Agent不可读**：Issue [#99241](https://github.com/openclaw/openclaw/issues/99241) 以20条评论高居榜首。用户描述了在长时间运行或包含 ANSI 字符的工具工作流中，工具结果被渲染为图片附件，导致 Agent 无法读取原始 stdout/stderr 文本。这严重影响了 LLM 的决策能力，是社区公认的“铂金级”高价值 Bug。**诉求**：希望彻底解决工具输出的渲染逻辑，确保 Agent 始终能访问到原始、可解析的文本输出。

2.  **内存泄漏导致进程被 OOM 杀死**：Issue [#91588](https://github.com/openclaw/openclaw/issues/91588) 虽然创建于一个月前，但今日仍有更新，评论数达到15条。用户报告网关进程内存占用从 350MB 暴涨至 15.5GB，最终被操作系统 OOM killer 杀死，触发 `launchd-handoff` 重启循环。**诉求**：社区迫切需要开发团队定位并修复这个灾难级的 P0 内存泄漏，这直接关系到服务的可用性。

3.  **嵌入式提示缓存（prompt cache）失效**：Issue [#102175](https://github.com/openclaw/openclaw/issues/102175) 讨论了跨各种边界（房间事件、策略变更、队列重建等）时，长会话的 prompt cache 连续性丢失的问题。这会导致性能下降和Token浪费。**诉求**：希望实现一个健壮的缓存机制，使其在复杂的会话生命周期中保持稳定。

---

#### 5. Bug 与稳定性

今日报告的 Bug 主要集中在回归问题和严重的稳定性隐患上，按严重程度排列如下：

- **P0 (Critical)**:
    - **Model 选择器不持久化**：Issue [#101763](https://github.com/openclaw/openclaw/issues/101763) 报告基于 `usemolty.com` 的托管实例中，模型选择器无法持久化，API 始终收到错误的模型 ID。这被标记为 Beta 版本发布阻塞器，严重影响线上服务。**尚无 Fix PR**。
    - **文档与Schema不匹配**：Issue [#103162](https://github.com/openclaw/openclaw/issues/103162) 指出 `channels.telegram.streaming.preview.toolProgress` 配置项在文档中存在，但被 6.11 的 Schema 校验器拒绝，导致所有 CLI 命令失效。这是一个严重的文档/代码不同步问题。**尚无 Fix PR**。
    - **网关内存泄漏**：Issue [#91588](https://github.com/openclaw/openclaw/issues/91588) 如前所述，是一个持续存在的P0级内存泄漏，亟待解决。

- **P1 (High)**:
    - **Codex OAuth 超时**：Issue [#89278](https://github.com/openclaw/openclaw/issues/89278) 报告 Codex OAuth 刷新成功但后续心跳/cron任务因10秒超时而失败。**尚无 Fix PR**。
    - **WhatsApp 会话卡死**：Issue [#84569](https://github.com/openclaw/openclaw/issues/84569) 报告长时间模型调用会导致 WhatsApp 会话停滞，后续消息排队无人处理。**有相关PR链接，但未注明已修复**。
    - **Agent 最终回复遗失**：Issue [#85714](https://github.com/openclaw/openclaw/issues/85714) 描述了 Agent 在最后一步忘记调用配置的交付工具，导致最终消息“漂浮”并丢失。**尚无 Fix PR**。
    - **空错误重试被阻塞**：Issue [#97877](https://github.com/openclaw/openclaw/issues/97877) 解释了 `hadPotentialSideEffects` 标志阻止了 Agent 对临时 5xx 错误的自动重试，导致任务静默失败。**该 Issue 今日已关闭**，推测已有 PR 修复。

---

#### 6. 功能请求与路线图信号

大量功能请求仍在热烈讨论中，从社区关注度可以窥见项目未来演进方向：

- **集成与平台扩展**：
    - **[Slack] Block Kit 支持**：Issue [#12602](https://github.com/openclaw/openclaw/issues/12602) 获得14条评论，用户希望 Agent 能发送更富交互性的 Slack Block Kit 消息（如 CRM 摘要、数据库查询结果等）。
    - **[WhatsApp] 贴纸发送**：Issue [#7476](https://github.com/openclaw/openclaw/issues/7476) 请求支持发送 `.webp` 格式图片为 WhatsApp 贴纸，而非普通图片附件。

- **Agent 能力与配置**：
    - **Per-agent 记忆 Wiki 配置**：Issue [#63829](https://github.com/openclaw/openclaw/issues/63829) 虽然已关闭，但其13条评论和10个👍表明社区对多 Agent 环境下私有知识库（Vault）的隔离需求非常强烈。
    - **Max Turns/Calls 限制**：Issue [#9912](https://github.com/openclaw/openclaw/issues/9912) 请求增加 `maxTurns` 或 `maxToolCalls` 配置，以应对某些模型忽略系统提示、无限循环调用工具的问题。

- **安全与治理**：
    - **文件系统沙箱配置**：Issue [#7722](https://github.com/openclaw/openclaw/issues/7722) 请求通过配置文件（`tools.fileAccess`）实现文件系统的白名单/黑名单访问控制。这是一个被广泛讨论的安全性增强需求。
    - **Node 注册工具**：Issue [#8287](https://github.com/openclaw/openclaw/issues/8287) 请求允许连接的节点向网关注册自己的工具，以便网关能将这些工具暴露给 LLM，拓展 Agent 能力。

结合已有的 PR，`feat(slack): allow configurable App Home views`（[#103963](https://github.com/openclaw/openclaw/pull/103963)）表明 Slack 功能的增强正在开发中，可能会进入下一版本。

---

#### 7. 用户反馈摘要

从 Issues 评论中提炼出的真实用户声音：

- **痛点**：
    - **被不可靠性困扰**：用户反复报告内存泄漏 (`#91588`)、WebSocket 断连 (`#99681`)、静默丢消息 (`#97877`， `#84569`) 等导致服务不稳定问题，严重影响了对其个人 AI 助手的信任感。
    - **被上下文溢出困扰**：`#9409` 的评论显示，用户在面对“Context overflow”错误时感到困惑和无助，因为错误信息没有提供具体的 token 用量或上下文大小，难以排查问题。
    - **首次设置体验不佳**：`#103962` 描述新用户在首次设置时，因 AI 配置未完成前就遇到了“Crestodian”状态，导致流程受阻，体验不透明。

- **期望**：
    - **更精细的控制**：用户希望获得对 Agent 行为的更精细控制，如 `#8299` 中的“抑制子 Agent 发布通告”和 `#88913` 中的“为不同频道自定义思考块格式”。
    - **更好的信息透明度**：`#7006` 期望在使用 `openrouter/auto` 时，Agent 能知晓实际调用了哪个模型及其费用，以便向用户报告。`#7379` 请求在 `/usage` 命令中添加更多细节。

---

#### 8. 待处理积压

以下为长期未解决或近日重新活跃的关键 Issue，急需维护团队关注：

1.  **[P0] Critical: Gateway Memory Leak**：Issue [#91588](https://github.com/openclaw/openclaw/issues/91588) 自 6月9日提出以来已有一个月，严重影响服务稳定性，但至今未有明确的 Fix PR。这是目前项目最亟待解决的积压问题。
2.  **[P1] Gateway idle heap growth**：Issue [#87109](https://github.com/openclaw/openclaw/issues/87109) 描述了 macOS 上网关在空闲状态下堆内存仍持续增长的问题，导致后台 cron 任务静默失败。该问题与 `#91588` 可能同源，但更侧重于空闲状态和特定平台。
3.  **[P2] Feature Request: Filesystem Sandboxing Config**：Issue [#7722](https://github.com/openclaw/openclaw/issues/7722) 作为一个创建于2月初的重要安全特性请求，至今仍停留在讨论阶段，未进入开发。考虑到安全性的重要性，建议评估其优先级并考虑实现。
4.  **[P3] 因 minSecurity 逻辑导致的安全降级**：Issue [#91283](https://github.com/openclaw/openclaw/issues/91283) 指出 `minSecurity` 函数的安全等级顺序是反的，这可能导致用户设置的“full”安全级别被错误地覆盖为“allowlist”。该 Issue 于6月8日提出，7月10日刚关闭，需确认其所指的逻辑是否已被修正。

---

## 横向生态对比

# AI 智能体与个人助手开源生态横向对比分析
**报告日期：2026-07-11**

---

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态进入 **“工程化与规模化”** 阶段。社区焦点从最初的“能否运行”转向 **“稳定可靠、成本可溯、多平台可用、安全可控”**。各项目普遍面临内存泄漏、流式传输一致性、配置持久化等“成长痛”，但迭代响应速度极快。同时，**多模态支持（GPT-5.6）、远程协作、细粒度配置管理** 成为共性演进方向。值得注意的是，LiteLLM 宣布的 Rust 迁移预示着行业对 **代理层极致性能** 的追求正从概念走向落地。

---

## 2. 各项目活跃度对比

| 项目 | 近24h Issue 更新数 | 近24h PR 活动数 | 版本发布 | 健康度评估 | 社区活跃度评级 |
|------|-------------------|------------------|----------|------------|--------------|
| **OpenClaw** | ~900 条（含评论） | 密集合并/关闭 | 无 | ⚠️ 中（多个P0/P1未修复） | ★★★★★ 极高 |
| **Hermes Agent** | ~800 条（含评论） | 73条 PR 合并/关闭 | 无 | ⚠️ 中（P1积压较多） | ★★★★★ 极高 |
| **OpenHands SDK** | 17 条 Issue，14 条 PR 关闭 | 17 条 PR 新开/关闭 | v1.35.0 ✅ | ✅ 良好 | ★★★★ 高 |
| **Pi** | 57 条 Issue | 15 条 PR 提交，13 合并 | v0.80.6 ✅ | ✅ 良好（快速响应回归） | ★★★★ 高 |
| **LiteLLM** | 49 条 Issue（新开/活跃） | 96 条 PR 合并/关闭 | v1.93.0-dev.3 | ⚠️ 中（流式成本等长期 Bug） | ★★★★★ 极高 |
| **Temporal** | 1 条 Issue 关闭 | 47 条 PR，19 合并/关闭 | 无 | ✅ 良好（专注基础设施） | ★★★ 中等 |

> **说明**：Issue 更新数含评论变动，PR 活动数含新提交、合并、关闭。OpenClaw/Hermes 的“900+/800+”为总更新量（包括评论、标签变更等），实际纯 Issue/PR 数量亦属前列。

---

## 3. OpenClaw 在生态中的定位

- **优势**：社区规模最大、功能最全面（覆盖多平台、工具调用、记忆管理等），是生态中最具“平台化”特征的项目。今日 900+ 活动量印证其核心地位。
- **技术路线差异**：相比 Hermes Agent 侧重 IM 平台集成（QQBot、飞书、WhatsApp），OpenClaw 更强调 **通用智能体框架**，支持侧载（sidecar）和灵活的 ACP 后端。相比 Pi，OpenClaw 不局限于终端界面，而是作为后台服务运行。
- **痛点**：稳定性问题突出（内存泄漏、会话丢失、WebSocket 断连）被社区反复诟病，P0 级 Bug 长期未修复可能削弱用户信任。而 Pi 和 OpenHands 的 Bug 修复速度更快。
- **社区规模**：从活动量看，OpenClaw 与 Hermes 并列第一梯队，但 OpenClaw 的问题讨论更偏向核心稳定性，Hermes 更偏向平台适配。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---------|---------|----------|
| **流式传输一致性** | OpenClaw (工具输出渲染)、Hermes (飞书表格)、LiteLLM (流式成本/工具字段丢失)、Pi (无显著问题) | 确保流式模式下工具调用字段、成本、格式化信息的完整传递 |
| **成本计算与透明度** | LiteLLM (OpenRouter 流式成本丢失、ElevenLabs 不计算)、Hermes (定价修复) | 用户对 Token 消耗和费用的准确追踪需求强烈 |
| **内存与稳定性** | OpenClaw (P0 内存泄漏)、Temporal (OOM 诊断)、Pi (Windows 终端重绘 Bug) | 长期运行服务的 OOM 风险是各项目共性挑战 |
| **配置持久化** | OpenHands SDK (LLM timeout 重启丢失)、OpenClaw (模型选择器不持久化) | 用户期望配置在服务重启后保持，尤其部署场景 |
| **多平台/多提供商适配** | OpenClaw (Slack/WhatsApp)、Hermes (微信/飞书/QQBot)、Pi (Copilot/Vertex AI)、LiteLLM (Anthropic/Bedrock) | 社区对多种 IM 平台和云服务商的原生支持需求旺盛 |
| **安全沙箱与访问控制** | OpenClaw (文件系统沙箱)、Hermes (工具权限护栏)、LiteLLM (Docker 镜像签名)、Temporal (认证漏洞修复) | 从文件访问到 API 凭据保护，安全治理意识提升 |
| **远程访问与协作** | Hermes (Dashboard CORS)、OpenClaw (远程 Agent+本地工具) | 本地运行、远程团队协作场景成刚需 |

---

## 5. 差异化定位分析

| 项目 | 核心定位 | 目标用户 | 技术架构关键差异 |
|------|---------|---------|----------------|
| **OpenClaw** | 通用智能体平台 | 个人开发者、团队、企业 | 支持侧载、ACP 后端、高度插件化，社区驱动的功能膨胀 |
| **Hermes Agent** | 多 IM 平台适配的智能体 | 消息平台重度用户、社区运营 | 深度集成 QQBot/飞书/微信等，网关稳定性是生命线 |
| **OpenHands SDK** | 智能体开发工具包（SDK） | 开发者、平台集成商 | 提供 Agent Profiles、事件系统、MCP 支持，强调可观测性 |
| **Pi** | 终端用户交互体验优先 | 个人效率用户、极客 | 极简 CLI、丰富的思考级别、约束采样前沿探索，轻量级 |
| **LiteLLM** | AI 代理层/网关 | 企业基础设施团队 | 模型路由、成本核算、Rust 迁移追求 sub-1ms 延迟 |
| **Temporal** | 工作流编排引擎（基础设施） | 后端开发、SRE | 独立活动控制、多集群复制、可插拔事件框架，非前端 Agent |

> **注**：Temporal 虽不直接面向个人 AI 助手，但作为工作流引擎正被越来越多 Agent 项目引入（如管理长时间任务）。

---

## 6. 社区热度与成熟度

**第一梯队（极高活跃，快速迭代）**：OpenClaw、Hermes Agent、LiteLLM  
- 每日 Issue/PR 更新量均在数百条，但伴随较多稳定性问题，处于“功能优先，质量随后”的阶段。  
- 社区贡献者活跃，但维护者对关键 Bug 的响应效率参差不齐（OpenClaw 内存泄漏一月未修 vs LiteLLM 流式成本问题也长期未解决）。

**第二梯队（高活跃，质量巩固）**：OpenHands SDK、Pi  
- 活动量适中，但产出效率高（如 OpenHands SDK 当日合并 17 条 PR，Pi 发布新版本）。  
- Bug 修复响应快，健康度良好，社区讨论集中在对新功能的精准打磨。

**第三梯队（中等活跃，基础设施定位）**：Temporal  
- 活动量较低但开发集中，专注于独立活动控制、多集群等企业级特性。  
- 适合作为下游依赖，而非直接面向终端用户的 Agent 项目。

---

## 7. 值得关注的趋势信号

1. **Rust 迁移浪潮（LiteLLM）**：AI 代理层性能竞争加剧，LiteLLM 公开启动 Rust 重写，目标“sub-1ms 开销”。这预示未来网关/代理层项目可能普遍转向系统级语言，OpenClaw、Hermes 等若未跟进可能面临性能瓶颈。

2. **约束采样/严格格式输出（Pi）**：Pi 社区对 `Strict Tools / Grammar` 的热议，以及关联的开放 PR，表明开发者和用户对 **LLM 输出可靠性** 的焦虑已超过对通用性的追求。未来智能体框架将内置 JSON Schema 校验、工具调用约束等能力。

3. **“独立活动控制”成为基础设施标配（Temporal）**：Temporal 在独立活动（Standalone Activities）上的投入，说明工作流引擎正在向更细粒度的运行时控制演进。这将影响上层 Agent 框架如何管理长时间任务（如代码编译、数据爬取），值得 OpenClaw、Hermes 借鉴。

4. **远程 Agent + 本地工具（Hermes、OpenClaw）**：用户希望在云端运行 Agent 但保留本地计算能力（如代码编译、文件操作），这催生“远程推理 + 本地执行”的混合架构。目前 Hermes 已有详细讨论，可能成为下一个热门功能。

5. **可观测性与成本透明化**：OpenHands SDK 增加 trace 元数据、LiteLLM 修复成本计算问题、OpenClaw 社区要求 `/usage` 细节——用户不再接受“黑盒”，对 Token 消耗、模型调用、资源使用情况的透明化需求正在从“锦上添花”变为“基本要求”。

6. **“Agent Profiles”式配置管理（OpenHands SDK）**：将 Agent 行为（技能、模型、安全策略）打包为可复用的配置文件，是解决多场景下配置复杂性的关键模式。OpenHands 的 Agent Profiles 若推广成功，可能成为行业事实标准。

---

*总结：当前生态处于从“野蛮生长”向“精细化运营”过渡的关键时期。稳定性（尤其是内存和流式）是短期最大痛点，而性能优化（Rust）、输出可控性（约束采样）、可观测性、配置管理则构成中长期竞争壁垒。对于技术决策者，建议优先评估项目的 Bug 修复速度和社区治理成熟度，而非仅看功能数量。*

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，这是为您生成的 Hermes Agent 项目动态日报。

---

### **Hermes Agent 项目动态日报 (2026-07-11)**

#### **1. 今日速览**

今天 Hermes Agent 项目社区活动达到极高热度，过去24小时内累计有近800条 Issue 和 PR 更新。这表明项目正处于快速迭代和社区广泛参与的关键时期。虽然当日没有新版本发布，但大量活跃的 PR（427条待合并）预示着下一次发布将包含重大功能更新和众多错误修复。社区讨论焦点集中在增强多平台适配能力（如微信、飞书、QQBot）、改进远程访问体验和解决关键的性能瓶颈（如极长提示词导致的模型卡顿）。

#### **2. 版本发布**

今日无新版本发布。

#### **3. 项目进展**

尽管无版本发布，但项目内在的核心代码推进非常积极。73条 PR 已成功合并或关闭，推动了多项关键改进：

- **核心Agent机制优化**:
    - **[已合并]** PR [#2792](https://github.com/NousResearch/hermes-agent/pull/2792) 修复了一个导致 `provider: custom` 被静默重定向到 `openrouter` 的认证问题，确保用户自定义配置得到尊重。
    - **[新提交]** PR [#62332](https://github.com/NousResearch/hermes-agent/pull/62332) 通过增加防护逻辑，解决了 Gemini 模型回退失败以及 Honcho 内存上下文注入时的可靠性问题，直接回应了社区关于 provider 切换和外部集成稳定性的反馈。
    - **[新提交]** PR [#62334](https://github.com/NousResearch/hermes-agent/pull/62334) 修正了 `deepseek-v4-pro` 模型定价的4倍错误，并增加了对新的 `v4-flash` 模型的支持，体现项目对定价透明度和最新模型支持的快速响应。

- **网关与平台适配**:
    - **[已关闭]** Issue [#52914](https://github.com/NousResearch/hermes-agent/issues/52914) 被关闭，确认解决了 QQBot 网关因 `is_reconnect` 参数缺失导致的无限重试循环问题，修复了核心的平台连接稳定性。
    - **[新提交]** PR [#61377](https://github.com/NousResearch/hermes-agent/pull/61377) 修复了飞书消息在包含 Markdown 表格时，其他格式（如加粗、链接）被破坏的渲染问题。

- **安全与配置**:
    - **[新提交]** PR [#62321](https://github.com/NousResearch/hermes-agent/pull/62321) 修复了模型探测请求在重定向过程中可能泄露提供商凭据的安全漏洞。
    - **[新提交]** PR [#62326](https://github.com/NousResearch/hermes-agent/pull/62326) 允许用户为特定模型或提供商禁用 `stream=True`，解决了与某些不兼容流式传输的代理服务配合使用时的问题。
    - **[新提交]** PR [#62335](https://github.com/NousResearch/hermes-agent/pull/62335) 为 `hermes doctor` 命令增加了只读的上游健康诊断功能，方便用户排查远端仓库和分支状态。

#### **4. 社区热点**

社区讨论热度极高，多个议题反映了用户的核心诉求：

- **远程访问与多平台需求强烈**:
    - **[Feature, 13评论]** Issue [#10567](https://github.com/NousResearch/hermes-agent/issues/10567) 关于为 Dashboard 添加 `--host` 和自定义 CORS 配置，以便通过 Tailscale/VPN 进行远程访问的需求，获得了13个 👍 支持。这表明 “本地运行、远程访问” 是许多用户和团队的基础需求。
    - **[Feature, 11评论]** Issue [#13484](https://github.com/NousResearch/hermes-agent/issues/13484) 对 Google Cloud Vertex AI 原生支持的呼声极高，11个讨论和14个 👍 证明用户对跨云服务提供商的多样性有强烈需求。
    - **[Bug, 17评论]** Issue [#52914](https://github.com/NousResearch/hermes-agent/issues/52914) QQBot 连接问题的最高评论数（17条），凸显了特定平台（尤其是国内 IM 平台）适配的稳定性对用户来说是巨大的痛点。

- **桌面端体验优化**:
    - **[Bug, 7评论]** Issue [#48098](https://github.com/NousResearch/hermes-agent/issues/48098) 报告桌面端在压缩会话时，状态栏显示“正在总结”未及时更新的问题，反映了用户对 UI 状态反馈及时性的高要求。
    - **[Bug, 5评论]** Issue [#49253](https://github.com/NousResearch/hermes-agent/issues/49253) 指出 iMessage 中 Markdown 粗体会导致 Unicode 字符损坏，这是特定平台（如 Apple 生态）上的边缘情况，说明项目需要关注对非标准消息格式的兼容性。

#### **5. Bug 与稳定性**

项目当日报告了多个 Bug，其中部分已有对应的修复 PR。

| 严重程度 | Bug名称 (链接) | 描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **P1** | [Gateway 消息路由错乱 #54527](https://github.com/NousResearch/hermes-agent/issues/54527) | 桌面端多 TUI 会话并发时，用户输入可能错误路由到其他会话，导致输入丢失。 | 待修复 |
| **P1** | [Bedrock/Claude 运行时认证失败 #28156](https://github.com/NousResearch/hermes-agent/issues/28156) | AWS Bedrock 设置向导接受不完整的 bearer-only 凭证，导致运行时因缺少 IAM 配置而报错。 | 待修复 |
| **P1** | [Codex API 会话重放失败 #27038](https://github.com/NousResearch/hermes-agent/issues/27038) | 恢复 Codex 会话时，因 `id` 字段过长被 Responses API 拒绝，可能导致会话中断。 | 待修复 |
| **P2** | [极长提示词导致模型卡顿 #61265](https://github.com/NousResearch/hermes-agent/issues/61265) | 代理工作流构造了过大的提示词，导致本地模型（如 Open WebUI）出现数分钟停顿，严重影响使用体验。 | 待修复 |
| **P2** | [桌面端状态同步延迟 #48098](https://github.com/NousResearch/hermes-agent/issues/48098) | 会话压缩后，桌面 UI 状态未能及时更新。 | 待修复 |
| **P2** | [向 session owner 错误发送消息 #62330](https://github.com/NousResearch/hermes-agent/pull/62330) | `send_message` 功能在未指定 `chat_id` 时，消息可能被错误发送到全局“家”频道，造成信息泄露。（已有修复PR） | **PR已提交** |
| **P3** | [飞书表格渲染问题 #7675](https://github.com/NousResearch/hermes-agent/issues/7675) | 飞书交互式卡片无法正确识别，按钮点击事件处理异常等问题。 | 待修复 |
| **P3** | [Kanban 死锁自动清理失败 #22926](https://github.com/NousResearch/hermes-agent/issues/22926) | Kanban 工作进程意外死亡后，任务锁定未自动清理，导致任务永久卡死。 | 待修复 |

#### **6. 功能请求与路线图信号**

除 Bug 修复外，社区用户积极提出新功能构想，部分与已存在的 PR 和项目改进方向高度吻合。

- **近期可能纳入的功能**:
    - **[Feature] Dashboard 远程访问** [#10567](https://github.com/NousResearch/hermes-agent/issues/10567): 为解决此问题，PR [#61809](https://github.com/NousResearch/hermes-agent/pull/61809) 已提交，通过增加 session provider 提示 cookie 来改善 Dashboard 的认证刷新路由，这是实现安全远程访问的关键一步。
    - **[Feature] Gemini & Antigravity 集成**: Issue [#13484](https://github.com/NousResearch/hermes-agent/issues/13484) (Vertex AI) 与 [#52657](https://github.com/NousResearch/hermes-agent/issues/52657) (Antigravity) 均涉及 Gemini 的集成。PR [#62332](https://github.com/NousResearch/hermes-agent/pull/62332) 对 Gemini fallback 的修复，暗示项目正在积极改进对 Gemini 的支持，可能是后续版本的一个重点方向。
    - **[Feature] 远程 Agent + 本地工具** [#18715](https://github.com/NousResearch/hermes-agent/issues/18715): 此功能（8评论, 20 👍）允许用户将计算密集型的工具（如代码编译）留在本地执行。该功能需求度极高，但与现有架构改动较大，预计需要更长的开发周期。

- **长期需求信号**:
    - **多平台账户支持**: Issue [#9756](https://github.com/NousResearch/hermes-agent/issues/9756) 建议支持微信多账号绑定，这反映用户希望在一个实例下为家庭或团队提供隔离服务的需求。
    - **可定制化内存路由**: Issue [#31776](https://github.com/NousResearch/hermes-agent/issues/31776) 希望 Hindsight 内存工具支持多 `bank_id` 路由，以便根据不同上下文（如项目、联系人）访问不同的历史记忆仓库。

#### **7. 用户反馈摘要**

从今日的 Issue 评论和 PR 讨论中，可以提炼出以下用户反馈：

- **改善平台适配是当务之急**: 社区对 QQBot、飞书、微信等特定平台的稳定性和功能完整性非常关注。Bug 修复（如飞书表格渲染）和功能请求（如微信多账号）都体现了这点。
- **稳定性高于新功能**: 尽管功能提议活跃，但高 P1/P2 级 Bug（如会话错乱、认证失败）的讨论热度说明，用户的直接痛点是使用过程中的可靠性问题。
- **对远程访问和团队协作有强烈需求**: 无论是 Dashboard 的 CORS 配置，还是“远程 Agent + 本地工具”的构想，都指向了用户希望将 Hermes Agent 从个人本地工具升级为团队协作平台。
- **关注成本和模型选择**: 用户对模型的定价和可用性非常敏感。`deepseek-v4-pro` 定价错误被快速发现和修复，以及用户要求在 Gemini 和 Antigravity 之间进行选择，都反映了这一点。

#### **8. 待处理积压**

以下是一些长期未完全解决或可能被忽视的重要议题，需要维护者进一步关注：

- **长期未解决的平台功能请求**: 如 [#7675](https://github.com/NousResearch/hermes-agent/issues/7675) (飞书卡片交互) 和 [#9756](https://github.com/NousResearch/hermes-agent/issues/9756) (微信多账号)，已存在超过一个月且无明确进展，可能成为社区参与度的瓶颈。
- **定价系统功能未完全实现**: Feature Issue [#9403](https://github.com/NousResearch/hermes-agent/issues/9403) 要求添加定价覆盖、合同定价和同步 CLI，虽已被标记为待实现（Phase 4），但至今未提上日程。随着模型定价复杂度的增加，该功能的优先级可能需要上调。
- **批量未响应的 Sweeper 标签 Issue**: 多个标记为 `sweeper:risk-*`（表示风险，无人认领修复）的 P1/P2 优先级 Bug，如 [#54527](https://github.com/NousResearch/hermes-agent/issues/54527) (消息路由错乱) 和 [#28156](https://github.com/NousResearch/hermes-agent/issues/28156) (Bedrock 认证)，仍无人修复，项目维护者需考虑分配资源或寻求社区贡献者认领。
- **长期搁置的 PR**: PR [#38846](https://github.com/NousResearch/hermes-agent/pull/38846) (桌面端15种语言国际化) 自6月4日提交以来，超过一个月未合并，可能阻碍了桌面应用在全球范围内的推广。
- **Bug 复现困难的高优先级问题**: 如 [#61265](https://github.com/NousResearch/hermes-agent/issues/61265) (极长提示词) 和 [#26489](https://github.com/NousResearch/hermes-agent/issues/26489) (LiteLLM 挂起)，标记为 `needs-repro`，需要维护者或社区用户提供更可靠的复现步骤。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是依据您提供的 OpenHands SDK GitHub 数据生成的 **2026-07-11 项目动态日报**。

---

# OpenHands SDK 项目日报 | 2026-07-11

## 今日速览

今日项目活跃度极高，呈现“高产出、高互动”态势。过去24小时内，Issue 和 PR 的创建与关闭数量持平（均为17条和14条），社区正密集推动从**Bug发现**到**代码合并**的完整闭环。核心贡献者 **@simonrosenberg** 主导的 **Agent Profiles** 相关议题已进入收尾和修复阶段，成为本周的重中之重。同时，v1.35.0 版本的发布也带来了关键的 WebSocket 重连和技能匹配修复，进一步夯实了 SDK 的稳定性和用户体验基础。整体来看，项目健康度良好，开发节奏稳健，社区参与活跃。

## 版本发布

### v1.35.0 发布

**概要：** 该版本聚焦于修复关键 Bug 和优化 CI 流程。

-   **Bug 修复：**
    -   **Skills**: 修复了 `match keyword triggers on whole words only` 的问题（感谢 @VascoSch92），避免关键词触发器的部分匹配，提升了技能触发准确性。
    -   **SDK**: 修复了远程会话 WebSocket 重连机制（感谢 @bozhnyukAlex），增强了 SDK 在网络不稳定下的鲁棒性。
    -   **CI**: 包含了版本号更新相关的 CI 调整。

-   **破坏性变更：** 无。
-   **迁移注意事项：** 建议所有使用远程交互功能或技能关键词匹配功能的用户升级至此版本。

## 项目进展

过去24小时内，项目完成了一系列旨在提升**系统稳定性**、**可观测性**和**功能完整性**的重要合并。

1.  **核心修复与优化：**
    -   **Pr#4070** - **Release v1.35.0**: 标志着新版本发布的里程碑。
    -   **Pr#4081** - **CI**: 将 QA 工作流切换到专用的评估 LLM 代理，避免影响团队 API 预算。
    -   **Pr#4074** - **Test**: 修复了对话树 Fork/Navigate 测试的并发问题，提升测试可靠性。
    -   **Pr#4071** - **Infra**: 推迟了 `browser_use` 日志清理的技术债务截止日期到 v2.0.0，为开发争取了时间。

2.  **功能增强：**
    -   **Pr#4075** - **Feature**: 新增 `commit-history API`，支持列出提交记录和查看差异，对 Code Review 和版本管理场景非常有价值。
    -   **Pr#4076** - **Feature**: `agent-server` 现在能够接收最终快照的 trace 元数据，增强了可观测性。
    -   **Pr#3932** - **Feature**: 为工作区存档暴露仓库元数据（仓库名、分支、commit），极大方便了后续的离线评估和审计工作。

3.  **功能兼容与修复：**
    -   **Pr#4056** - **Fix**: 完成了对 **GPT-5.6** 在 Codex ACP 验证下的支持。
    -   **Pr#3505** - **Fix**: 修复了 Claude Sonnet 模型从默认测试矩阵中消失的回归问题。

**总结：** 项目在修复回归、提升 CI 稳定性以及完善代码分析、可观测性等高级特性方面取得了扎实进展。

## 社区热点

本周的讨论热度高度集中在 **Agent Profiles** 功能的设计、实现和 Bug 修复上，主要贡献者 **@simonrosenberg** 扮演了核心驱动角色。

-   **最热讨论集（Agent Profiles 生态）：**
    -   **#3710、#3979、#4017、#3728、#3959**: 这一系列由 @simonrosenberg 提出的 Issue 共同描绘了从**设计**、**缺陷**到**统一解决方案**的完整路径。社区围绕技能模型、配置继承、ACA 认证、UI 设计等关键点展开了激烈但富有成效的讨论。这体现了社区对 Agent Profiles 这一“一劳永逸”式配置管理功能的强烈需求和深度参与。
    -   **诉求分析：** 核心诉求是**解决 Agent Profiles 在实际使用中出现的各种不一致和缺陷**（如技能作用域、流式传输丢失、配置覆盖问题），并最终**统一并简化**技能模型（从嵌入式和引用式两套到单一服务端目录），这是一个典型的从“可用”向“好用”演进的过程。

-   **高关注度 Bug 报告：**
    -   **#4080** - **One unregistered event kind fails the entire conversation load**: @smolpaws 报告一个严重问题：单个事件反序列化失败会导致整个对话无法加载。该 Issue 虽新开但已有 1 条评论，引起了社区对边缘错误处理机制的关注。

## Bug 与稳定性

今日报告了若干关键 Bug，显示出系统在**事件处理**、**性能限制**和**配置持久化**方面的压力点。

-   **严重性: 高**
    -   **#4080** - **Conversation 完全不可加载**: 单个未注册的事件类型导致整个对话加载失败，这是非常严重的“一刀切”错误处理问题。**目前尚无 PR**。
    -   **#4063** - **max_concurrent_runs 限制失效**: @neubig 指出该配置并未限制原生异步对话，可能导致资源耗尽。**目前尚无 PR**。

-   **严重性: 中**
    -   **#4077** - **Streaming 管道存在正确性与资源安全 Bug**: @VascoSch92 审计发现流式传输管道存在多个 Bug，虽然持久化记录正确，但实时推送可能有损。**目前尚无 PR**。
    -   **#4032** - **LLM Profile Timeout 重启后重置**: @kripper 报告 LLM 超时设置无法在 `agent-server` 重启后保持。**已有 PR #4028 尝试修复**。

-   **严重性: 低**
    -   **#4072** - **browser_use 日志修补**: 一个已知的日志污染问题，已通过 #4071 将清理计划推迟到 v2.0.0。

## 功能请求与路线图信号

新提出的功能请求主要聚焦于**增强系统灵活性和可观测性**，其中一些与已有 PR 高度相关，极有可能被采纳。

-   **高优先级/极可能合并:**
    -   **#4064** - **Request-Scoped LLM 额外头部**: 提出支持在运行时动态注入 LLM 请求元数据。这是一个合理的需求，且实现机制不会破坏现有架构。
    -   **#4062** - **Expose ACP 会话配置选项**: 提出通用化 ACP 会话配置的暴露，以增强对不同 ACP 后端的兼容性。这与 **PR #3996** 中修复 ACP 参数顺序的思路一致，表明社区在积极推动 ACP 功能的完善。
    -   **#4067** - **Split ACP 提供者镜像**: 提出将默认镜像与 ACP 提供程序解耦以减小镜像体积。这是一个显著的 DevOps 优化，很可能被纳入下一个版本的路线图。

-   **信号:**
    -   围绕 Agent Profiles 的 **增强请求（#4029）** 和 **Epic（#3713）** 虽然尚未关闭，但其讨论热度意味着这些是下一阶段开发的核心。

## 用户反馈摘要

从 Issues 的讨论中可提炼出以下用户痛点与诉求：

-   **配置持久化痛点：** 用户 @kripper 明确指出 **LLM Profile 的 Timeout 设定在 Agent Server 重启后会丢失**。这表明在部署环境中，配置的持久化和热加载功能对用户而言至关重要，当前机制存在缺陷。
-   **工作流完整性诉求**： 用户 @smolpaws 报告的事件加载失败问题，反映出用户期望系统具备“部分失败、整体可用”的韧性，而非因单点错误导致全盘皆输。
-   **技术债务清理意识：** 从 @VascoSch92 推迟 `browser_use` 日志修补的 Issue #4072 可以看出，开发者自身对技术债务有清晰的认识，并制定了明确的清理计划（v2.0.0），这是一种健康的项目管理态度。

## 待处理积压

以下为长期未关闭、仍可能对项目产生影响的 PR：

-   **Pr#2911** - `feat(security): add ToolShieldLLMSecurityAnalyzer`（创建于 2026-04-21，已近3个月）
    -   **链接:** https://github.com/OpenHands/software-agent-sdk/pull/2911
    -   **分析:** 这是一项重要的安全特性，可能涉及复杂实现或较大的架构讨论。长时间的开放状态可能意味着功能尚不成熟或正等待关键资源的整合。维护者应关注其进展，避免阻塞路线图。

-   **Pr#3894** - `feat(mcp): subscribe to tools/list_changed for progressive-disclosure servers`（创建于 2026-06-26，已有约2周）
    -   **链接:** https://github.com/OpenHands/software-agent-sdk/pull/3894
    -   **分析:** 该 PR 旨在支持 MCP 协议的渐进式工具暴露，对兼容复杂 MCP 服务器（如 Datadog）非常关键。其标记为 **review-this**，但长时间未合并。维护者应评估其风险并加速审查，以确保 MCP 功能的领先性。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 Pi 项目动态日报。

---

### Pi 项目动态日报 | 2026-07-11

#### 1. 今日速览

今日项目活跃度极高，社区与开发双轮驱动效应显著。过去24小时内，共有57条Issue更新和15条PR提交，显示项目仍处于高速迭代期。**v0.80.6版本正式发布**，引入了全新的“max”思考级别，紧跟GPT-5.6和Claude系列前沿模型。同时，围绕GPT-5.6系列模型的全面支持成为今日社区与开发协作的绝对焦点，系列相关Issue和PR的密集涌现，标志着Pi正在迅速适配最新的AI模型生态。

#### 2. 版本发布

- **v0.80.6** ([查看详情](https://github.com/earendil-works/pi/releases/tag/v0.80.6))
  - **新增功能**:
    - **`max` 思考级别**: 引入了全新的 `max` 思考级别，级别在 `xhigh` 之上。该功能为可选启用，原生支持 GPT-5.6 和自适应的 Claude 模型。用户可通过 CLI (`--thinking max`)、SDK、RPC 及模型选择器使用此功能。同时也支持通过自定义主题 (`thinkingMax`) 进行配置。
  - **迁移与注意事项**: 本次版本新增了一个高阶思考级别，主要用于解锁更强模型的推理能力。对于默认模型的用户，预计无影响。使用自定义模型或主题的用户，建议检查配置是否需要更新以适配新的思考级别。

#### 3. 项目进展

今日项目在“稳健前行”和“拥抱前沿”两个方向同步推进，共合并/关闭了13个PR。

- **核心架构与兼容性修复**:
  - **库嵌入支持**: PR [#6501](https://github.com/earendil-works/pi/pull/6501) 修复了将 Pi 作为嵌入式库使用时，跨会话主题初始化和扩展运行时复用的问题，提升了库模式的稳定性。
  - **OpenRouter 兼容性**: PR [#6496](https://github.com/earendil-works/pi/pull/6496) 修复了 OpenRouter 提供商未能正确发送会话ID (`session_id`) 的问题，解决了 #6366 Issue，改善了该平台用户的体验。
  - **Bun 运行时更新**: PR [#6503](https://github.com/earendil-works/pi/pull/6503) 将 Bun 运行时版本更新至 1.3.14，以支持通过环境变量配置 HTTP 空闲超时，回应了用户关于自托管超时的反馈。

- **模型生态与目录扩展**:
  - **GPT-5.6 模型支持**: 社区贡献者积极更新模型目录，确保 Pi 能识别最新模型。PR [#6471](https://github.com/earendil-works/pi/pull/6471) 修正了 GPT-5.6 代码模型的上下文窗口大小（从 272k 更新至 372k）。PR [#6490](https://github.com/earendil-works/pi/pull/6490) 为多个 Fable-5 供应商添加了 `xhigh` 和 `max` 思考级别。
  - **消息锚定工具加载**: PR [#6474](https://github.com/earendil-works/pi/pull/6474) 合并，支持在对话中途动态引入工具，无需在初始请求中声明所有工具，提升了工具使用的灵活性。
  - **新扩展示例**: PR [#6505](https://github.com/earendil-works/pi/pull/6505) 添加了 `/goal` 扩展示例，展示了如何构建多轮自主任务执行功能，为开发者提供了新的开发范式参考。

#### 4. 社区热点

今日社区讨论焦点主要集中在**模型适配**和**功能增强**方面。

1.  **约束采样 (Constrained Sampling)**:
    - **Issue [#6306](https://github.com/earendil-works/pi/issues/6306)**: 关于支持“Strict Tools / Grammar”的深度讨论持续升温，已积累22条评论，是目前最热的讨论贴。海内外开发者对让AI严格遵循输出格式和工具定义表现出强烈兴趣。 关联的PR [#6341](https://github.com/earendil-works/pi/pull/6341) 也处于开放状态，表明这是一个正在积极开发的核心功能。

2.  **GPT-5.6 模型全面接入**:
    - **Issue [#6475](https://github.com/earendil-works/pi/issues/6475)**: 请求为 GitHub Copilot 提供商添加 GPT-5.6 模型，获得了6个赞，社区对该系列模型的接入呼声很高。
    - **Issue [#6097](https://github.com/earendil-works/pi/issues/6097)**: 关于添加 `max` 思考级别的原始请求，获得17个赞，显示用户对更高阶推理能力的期待已久。此需求已在 v0.80.6 中得到实现。

3.  **Windows 终端兼容性**:
    - **Issue [#6300](https://github.com/earendil-works/pi/issues/6300)**: 关于 Windows 下输入行重绘导致每个字符都在新行的 Bug 持续被讨论，反映了Windows用户对良好体验的迫切需求。

#### 5. Bug 与稳定性

今日报告的 Bug 中，有部分已识别或正在修复，以下按严重程度排序：

1.  **【高】** **回归问题**: Issue [#6476](https://github.com/earendil-works/pi/issues/6476) 报告了 `httpIdleTimeoutMs` 设置在 v0.80.6 版本中失效的问题，导致自托管 OpenAI 兼容服务超时。该问题已部分被 PR [#6503](https://github.com/earendil-works/pi/pull/6503) (更新 Bun 版本) 解决。
2.  **【中】** **会话ID丢失**: Issue [#6477](https://github.com/earendil-works/pi/issues/6477) 指出 compaction 请求因未包含会话ID，导致在部分 OpenAI-Codex 模型上失败，影响了模型的内存管理。目前为开放状态。
3.  **【中】** **重试机制异常**: Issue [#6303](https://github.com/earendil-works/pi/issues/6303) 指出指数退避没有上限，可能导致极长的等待时间，影响重试策略的可用性。
4.  **【低】** **配置绕过**: Issue [#6472](https://github.com/earendil-works/pi/issues/6472) 指出设置 `compaction.enabled=false` 后，溢出恢复路径仍可能触发自动压缩，导致用户配置不完全生效。

#### 6. 功能请求与路线图信号

今日用户提出的功能请求透露出项目未来可能的发展方向。

1.  **约束采样 (Constrained Sampling)**: 从 Issue [#6306](https://github.com/earendil-works/pi/issues/6306) 的热度及关联的开放 PR [#6341](https://github.com/earendil-works/pi/pull/6341) 来看，**约束采样**极有可能成为近期下个版本的核心功能之一。它将允许开发者为工具调用定义严格的输入约束，极大提升 Pi 在结构化任务中的可靠性。

2.  **多轮自主代理**: PR [#6505](https://github.com/earendil-works/pi/pull/6505) 合并的 `/goal` 扩展示例，以及 Issue [#6509](https://github.com/earendil-works/pi/issues/6509) 提出的 `setUsage` 接口，暗示了项目正在为构建更复杂的**自治多轮子代理 (Subagent)** 能力铺垫基础设施。

3.  **更多模型与提供商**: 用户持续要求添加新的模型 (如 Issue [#6475](https://github.com/earendil-works/pi/issues/6475)) 和新的提供商 (如 PR [#6216](https://github.com/earendil-works/pi/pull/6216) 仍在开放的 Amazon Bedrock Mantle 新提供商)，表明项目将长期致力于成为更广泛的AI模型接入层。

#### 7. 用户反馈摘要

- **痛点**: Windows 终端体验不佳 (Issue [#6300](https://github.com/earendil-works/pi/issues/6300))、自托管服务的超时问题 (Issue [#6476](https://github.com/earendil-works/pi/issues/6476))、自定义键绑定在启动时失效 (Issue [#6459](https://github.com/earendil-works/pi/issues/6459))，这些是用户日常使用中遇到的直接障碍。
- **兼容性**: OpenRouter 提供商身份认证 (Issue [#6366](https://github.com/earendil-works/pi/issues/6366)) 和 Copilot 特定模型端点 (Issue [#6510](https://github.com/earendil-works/pi/issues/6510)) 的不兼容问题，凸显了用户对多提供商、多模型生态支持的期望。
- **开发者体验**: 用户尝试编写扩展时遇到 `typebox` 模块加载失败 (Issue [#6512](https://github.com/earendil-works/pi/issues/6512)) 以及 `/reload` 不能更新 `.mjs`/.cjs` 依赖的问题 (Issue [#6000](https://github.com/earendil-works/pi/issues/6000))，表明扩展开发过程中仍存在一些障碍需要改善。
- **正向反馈**: 用户对项目本身表达了感谢（在Issue [#6300](https://github.com/earendil-works/pi/issues/6300) 中提到），同时对新增的 `max` 思考级别和 GPT-5.6 模型支持展现了极高的期待。

#### 8. 待处理积压

- **长期开放的重要 Issue**:
    - **[#6306](https://github.com/earendil-works/pi/issues/6306)**: “支持 Strict Tools / Grammar” 已开放一周，讨论深入，关联的 PR [#6341](https://github.com/earendil-works/pi/pull/6341) 也在进行中，是功能演进的重要信号。
    - **[#6206](https://github.com/earendil-works/pi/issues/6206)**: “context window clamping”问题讨论较多，但尚无直接的修复PR，需要维护者跟进评估。
    - **[#6210](https://github.com/earendil-works/pi/issues/6210)**: “斜杠命令无法选择含括号的模型ID” 问题已开放超过一周，属于可用性问题。
- **待处理的开放 PR**:
    - **[#6216](https://github.com/earendil-works/pi/pull/6216)**: 新增 “Amazon Bedrock Mantle” 提供商的PR已搁置数日，尚未有维护者反馈，需要关注。

---
**综合评价**：项目整体健康状况非常良好，社区贡献活跃，开发响应迅速。当前的核心议题集中在模型适配与核心功能（如约束采样）的探索上。维护者应重点关注Windows终端的兼容性回归问题和自建服务的超时投诉，确保核心稳定性的同时，平稳推进新功能落地。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 | 2026-07-11

---

## 1. 今日速览

过去 24 小时，LiteLLM 项目保持**极高活跃度**：共处理 78 条 Issue（新开/活跃 49 条，已关闭 29 条）和 244 条 PR（待合并 148 条，已合并/关闭 96 条）。发布了一个开发版 v1.93.0-dev.3。社区讨论集中在 **流式响应成本丢失、Rust 迁移、Anthropic 兼容性、以及代理层稳定性** 等方面。整体项目健康度良好，但部分长期 Bug 仍需关注。

---

## 2. 版本发布

### v1.93.0-dev.3

- 类型：开发版（Dev Release）
- 核心变更说明：
  - 此版本暂无详细 changelog，主要附带 **Docker 镜像签名** 验证相关说明。所有 LiteLLM Docker 镜像已使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 进行签名，可通过指定 commit `0112e53` 的公钥验证镜像完整性。
- ⚠️ 迁移注意事项：
  - 此为开发版，可能包含未完全测试的特性，不建议生产环境直接升级。
  - 如果使用 Docker 部署，建议在拉取镜像后执行 `cosign verify` 以确认签名。

---

## 3. 项目进展

以下为本日已合并/关闭的重要 PR，标志着多项关键改进已落地：

| PR | 标题 | 说明 |
|----|------|------|
| [#32793](https://github.com/BerriAI/litellm/pull/32793) | refactor(ui): full-height sidebar shell with content-scoped top bar | 重构 UI 布局，侧边栏全高、顶部栏内容范围限定 |
| [#32635](https://github.com/BerriAI/litellm/pull/32635) | fix(proxy): build redis usage cache from REDIS_* env when cache backend is not Redis | 修复代理层 Redis 缓存构建逻辑，允许从 `REDIS_*` 环境变量读取独立于后端缓存的 Redis 配置 |

此外，尚有多个重要 PR 处于开放待合并状态，预计近期会落地（见第 6 节）。

---

## 4. 社区热点

以下为本日讨论最活跃、反应最强烈的 Issue/PR（按评论数排序，并附链接）：

| 标题 | 类型 | 评论数 | 核心诉求 |
|------|------|--------|----------|
| [#16021](https://github.com/BerriAI/litellm/issues/16021) OpenRouter 流式响应成本丢失 | Bug | 15 | 流式模式下 `usage.cost` 字段未被保留，非流式正常，严重影响计费准确性 |
| [#8244](https://github.com/BerriAI/litellm/issues/8244) 精确 token 计数（vLLM 托管模型） | Feature | 8 (已关闭) | 希望 LiteLLM 原生查询 vLLM 的 tokenizer 而非默认使用 tiktoken，已关闭表明可能已实现 |
| [#18058](https://github.com/BerriAI/litellm/issues/18058) ElevenLabs 模型成本计算异常 | Bug | 8 | 代理层对 ElevenLabs 模型不计算成本，给出最小复现配置 |
| [#14635](https://github.com/BerriAI/litellm/issues/14635) 超时错误显示 None 秒 | Bug | 7 | `litellm.Timeout` 错误消息中 seconds 字段为 `None`，属于明显的显示 Bug |
| [#31263](https://github.com/BerriAI/litellm/issues/31263) LiteLLM Rust 迁移 | 公告 | 7 | 官方宣布启动 Rust 重写，目标达到 sub-1ms 的网关开销，社区关注度极高 |
| [#25390](https://github.com/BerriAI/litellm/issues/25390) Anthropic 流式丢失 tool_use.input | Bug | 6 | 使用 Anthropic 兼容接口 + Gemini/Gemma 模型时，流式模式工具调用字段丢失 |
| [#24123](https://github.com/BerriAI/litellm/issues/24123) 支持 Langfuse SDK v4 | Feature | 4 | 当前锁定 `langfuse ^2.45.0`，用户希望升级以使用 v4 新特性 |
| [#32787](https://github.com/BerriAI/litellm/issues/32787) 模型成本值类型问题 | Bug | 1 (新) | 模型信息通过数据库往返后成本字段变为字符串导致计算错误 |

**分析**：社区关注的焦点集中于 **成本统计准确性**（#16021、#18058、#14635、#32787）和 **流式传输中功能完整性**（#25390）。Rust 迁移（#31263）则吸引了大量讨论和点赞，可能成为项目未来主要演进方向。

---

## 5. Bug 与稳定性

按严重程度排列本日上报的 Bug（含已确认和新出现）：

| 严重程度 | Issue / PR | 问题描述 | 是否有修复 PR |
|----------|------------|----------|--------------|
| **严重** | [#16021](https://github.com/BerriAI/litellm/issues/16021) | OpenRouter 流式成本信息丢失，影响计费准确性 | 无 |
| **严重** | [#25390](https://github.com/BerriAI/litellm/issues/25390) | Anthropic /v1/messages 流式模式下 tool_use.input 字段丢失，导致工具调用失败 | 无 |
| **严重** | [#18667](https://github.com/BerriAI/litellm/issues/18667) | AWS Bedrock 模型生成畸形的 JSON 工具参数后，后续包含历史上下文的请求全部失败（500） | 此 Issue 已关闭，可能已修复 |
| **中** | [#14635](https://github.com/BerriAI/litellm/issues/14635) | 超时错误消息显示 `None seconds`，是简单的显示逻辑 Bug | 无 |
| **中** | [#18058](https://github.com/BerriAI/litellm/issues/18058) | ElevenLabs 模型在代理中不记录成本 | 无 |
| **中** | [#32787](https://github.com/BerriAI/litellm/issues/32787) | 模型成本字段从数据库读出后类型为字符串，导致 float 运算错误 | 无 |
| **低** | [#32775](https://github.com/BerriAI/litellm/issues/32775) | 无法从非 GitHub 源添加技能（Claude Code 插件市场） | 无 |
| **低** | [#32778](https://github.com/BerriAI/litellm/issues/32778) | 工具权限护栏日志级别过高，预期事件也输出 WARNING | 无 |

---

## 6. 功能请求与路线图信号

- **已确认在进行中的方向**：
  - **Rust 迁移**（#31263）：项目已公开启动 Rust 重写，目标是成为最轻量的 AI 网关（sub-1ms 开销），目前可申请早期 Beta 测试。
  - **MCP/DCB Bridge 支持**：多个 PR（#32794、#32828、#32824、#32804）正在构建 "dcr_bridge" 相关的信封（envelope）生产/消费逻辑，预计将用于客户端转发 MCP 认证模式。
  - **独立 Redis 配置**：PR #32661（已合并）允许独立于缓存后端配置协调 Redis；PR #32635 是相关修复。
  - **代理无授权请求成本追踪**：PR #32410 跟踪未认证透传请求的消费日志。

- **社区强烈需求但尚无实现**：
  - [支持 Langfuse Python SDK v4](https://github.com/BerriAI/litellm/issues/24123)（👍 6）
  - [心跳间隔选项](https://github.com/BerriAI/litellm/issues/14953)（👍 2）
  - [按 sessionId 过滤日志](https://github.com/BerriAI/litellm/issues/22973)（👍 3，已关闭，可能已实现）
  - [自定义 tokenizer + 聊天模板](https://github.com/BerriAI/litellm/issues/19332)（已关闭）
  - [从外部路径加载模型成本映射](https://github.com/BerriAI/litellm/issues/25062)（已关闭）

- **可能纳入下一版本**：考虑到近期的 PR 密度，以下方向概率较高：
  - 流式推理 token 保存（#32837）
  - 流式错误事件重新抛出（#32835）
  - Gemini 图片生成模型不标记支持推理（#32836）
  - Anthropic 请求超时参数传递（#32827）
  - Auto-router 统一复杂度与语义选项（#32829）

---

## 7. 用户反馈摘要

从本日 Issue 评论中提取的真实用户声音：

- **#16021（OpenRouter 流式成本）**：“Non-streaming works correctly. In streaming, cost fields are lost.” → 用户明确强调了非流式和流式的行为不一致，影响了计费系统的数据整合。
- **#14635（超时错误显示 None seconds）**：“There is obviously a bug in how the timeout gets measured... always shows 'None seconds'” → 用户不仅报告问题，还指出了根本原因（超时时间传递为 None）。
- **#25390（Anthropic 流式 tool_use）**：“With the exact same request payload: non-streaming returns correct tool block, streaming fails.” → 用户使用 Gemma 4 模型，发现流式与非流式结果不一致，且工具调用字段丢失。
- **#18667（Bedrock 畸形的 JSON 工具参数导致后续请求失败）**：“subsequent requests that include conversation history fail with 500” → 用户指出了单次故障对后续请求的连锁影响，属于严重的可用性问题。
- **#32787（成本字段类型问题）**：“cost values become strings... some YAML parsers... parse 1e-05 as integer” → 用户深入分析了序列化/反序列化导致的数据类型丢失问题，并提出了修正建议。
- **#18058（ElevenLabs 成本不计算）**：“Cost not calculated, even though model is in config.” → 用户提供了最小复现配置，期望成本透明化。

用户普遍期待 **流式与异步场景下的功能完整性** 和 **成本计算的准确性**。

---

## 8. 待处理积压

以下为长期未响应或已标记 `stale` 但仍值得关注的重要议题：

| Issue | 创建时间 | 标签 | 简述 | 最后回复 |
|-------|----------|------|------|----------|
| [#8244](https://github.com/BerriAI/litellm/issues/8244) | 2025-02-04 | stale, enhancement | 精确 token 计数（vLLM） | 2026-07-10（已关闭） |
| [#14953](https://github.com/BerriAI/litellm/issues/14953) | 2025-09-26 | stale, enhancement | 流式心跳间隔 | 2026-07-10（已关闭） |
| [#15063](https://github.com/BerriAI/litellm/issues/15063) | 2025-09-30 | stale, enhancement | 自定义 token 定价比例计算 | 2026-07-10（已关闭） |
| [#15360](https://github.com/BerriAI/litellm/issues/15360) | 2025-10-09 | stale, bug | PostgreSQL 批量插入 spend logs 导致重复执行计划 | 2026-07-10（仍 OPEN） |
| [#14635](https://github.com/BerriAI/litellm/issues/14635) | 2025-09-17 | stale, bug | 超时显示 None seconds | 2026-07-10（仍 OPEN） |
| [#16021](https://github.com/BerriAI/litellm/issues/16021) | 2025-10-28 | bug | OpenRouter 流式成本丢失 | 2026-07-10（仍 OPEN） |

**提醒**：虽然部分议题最近被更新（自动标注？），但 `stale` 标记意味着维护者可能长时间未介入。其中 **#15360**（PostgreSQL 性能问题）和 **#14635**（超时显示 Bug）自创建超过 9 个月仍处于开放状态，建议优先审视。

---

*本日报基于 [LiteLLM GitHub 仓库](https://github.com/BerriAI/litellm) 2026-07-10 的公开数据生成。*

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-07-11

## 今日速览

过去 24 小时内，Temporal 核心仓库保持着较高的开发活跃度：**提交 / 合并了 47 条 Pull Request**（其中 19 条已合并或关闭），**仅 1 个 Issue 被关闭**（安全依赖升级），无新版本发布。项目团队正集中推进 **CHASM 过渡选项、独立活动控制 API、工作流暂停增强、Nexus 租户速率限制**等多项重要特性，同时修复了多个边缘案例和性能问题。整体来看项目处于 **积极迭代、稳定性与功能并重** 的阶段。

## 版本发布

无新版本发布。

## 项目进展

今日合并 / 关闭的 PR 中，以下几项对项目里程碑有显著推动：

- **准备 v1.32.0 发布分支** ([#11015](https://github.com/temporalio/temporal/pull/11015))：由 CI 机器人自动创建，覆盖治理文件并更新依赖，预示新版本即将到来。
- **API 升级到 v1.63.3** ([#11011](https://github.com/temporalio/temporal/pull/11011))：同步上游 API 定义，确保兼容性与功能对齐。
- **工作流任务完成分页（服务器端）** ([#10880](https://github.com/temporalio/temporal/pull/10880))：添加了 `RespondWorkflowTaskCompleted` 请求的分页支持，由动态配置控制（默认关闭），为大规模工作流任务处理做准备。
- **默认重试策略行为修正** ([#11010](https://github.com/temporalio/temporal/pull/11010))：当 `UpdateActivityExecutionOptions` 中设置 `nil retry_policy` 时，现在会使用默认重试策略（与 `StartActivityExecution` 行为一致），同时将默认策略的获取改为按 namespace 名称而非 ID。
- **修复取消暂停时清除待处理工作流任务** ([#10980](https://github.com/temporalio/temporal/pull/10980))：确保取消暂停操作能正确触发新的工作流任务，避免状态不一致。

这些合并意味着 **独立活动操作命令**（#10106）的系列 PR 正在逐步合入主干，CHASM 相关特性也向前迈进。

## 社区热点

今日没有出现评论特别活跃的 Issue 或 PR（评论数均为 undefined），但以下条目因涉及面广或与安全/新功能密切相关，值得关注：

- **安全依赖升级**：Issue [#10676](https://github.com/temporalio/temporal/issues/10676) 报告了 `pgx v5.9.2` 的认证降级漏洞（CWE-306），已关闭（预期升级到 v5.10.0）。虽然无讨论，但供应链安全是社区敏感点。
- **独立活动操作命令**：[#10106](https://github.com/temporalio/temporal/pull/10106) 是一个超大型 PR（自 4 月 28 日开放），实现了 Pause/Unpause/Reset/UpdateOptions 等服务器端控制 API，吸引了后续多个修复性 PR（如 #11013, #11016, #10980），表明该功能是当前开发焦点。
- **内存诊断改进**：[#10742](https://github.com/temporalio/temporal/pull/10742) 旨在 CI 中捕获 OOM 时的 pprof 数据，对测试稳定性有直接影响，可能吸引关注。

## Bug 与稳定性

以下为今日修复或报告的问题，按严重程度排列：

1. **依赖安全漏洞（严重）**：`pgx v5.9.2` 认证降级漏洞，Issue [#10676](https://github.com/temporalio/temporal/issues/10676) 已关闭，fix 预计随依赖升级进入下一版本。
2. **独立活动选项更新导致重试延迟异常（功能缺陷）**：PR [#11016](https://github.com/temporalio/temporal/pull/11016) 修复了当 worker 提供的 `NextRetryDelay` 恰好等于旧重试策略间隔时，待处理重试被意外延迟的问题。已合并。
3. **独立活动还原原始选项时崩溃风险（稳定性）**：PR [#11013](https://github.com/temporalio/temporal/pull/11013) 增加了对 `restore_original=true` 请求的守卫，防止当 `OriginalOptions` 为 nil 时引发错误。已合并。
4. **集群移除验证边缘案例**：PR [#10997](https://github.com/temporalio/temporal/pull/10997) 修复了当 namespace 仅引用其他集群时，移除校验仍可能误拒绝的问题。已合并。
5. **工作流暂停/取消暂停状态不一致**：PR [#10980](https://github.com/temporalio/temporal/pull/10980) 修复了取消暂停时未清除待处理工作流任务导致无法触发新任务的问题。已合并。

所有 fix 均已合入，无未修复的严重 Bug。

## 功能请求与路线图信号

今日活跃 PR 揭示了以下可能纳入下一版本的功能方向：

- **CHASM 过渡选项** ([#10957](https://github.com/temporalio/temporal/pull/10957))：新增 `RefConsistencyLevel` 过渡选项，控制执行陈旧性检查的版本化过渡级别，属于 CHASM 核心机制。
- **Nexus 租户速率限制接口** ([#11012](https://github.com/temporalio/temporal/pull/11012))：提供 OSS 扩展点，允许实现按租户的速率限制，并附带默认 no-op 实现。
- **独立活动执行时间可见性** ([#11017](https://github.com/temporalio/temporal/pull/11017))：将独立活动的执行时间（schedule time + start delay）暴露到 visibility 字段，支持查询。
- **被动集群任务再生** ([#11005](https://github.com/temporalio/temporal/pull/11005))：当时间跳跃被复制到 passive 集群时，重新生成 CHASM 任务，支持多活场景。
- **结构化事件框架** ([#10890](https://github.com/temporalio/temporal/pull/10890))：新增可插拔的事件系统，支持 namespace 与复制生命周期事件的类型化编码和日志输出，为可观测性铺路。
- **工作流暂停支持开始延迟** ([#10975](https://github.com/temporalio/temporal/pull/10975))：允许在第一个工作流任务被派发前（即 `start_delay` 期间）暂停工作流，扩展了暂停功能的使用场景。

这些特征表明 Temporal 正在强化 **独立活动管理、多集群复制、可观测性、安全控制** 等企业级能力。

## 用户反馈摘要

今日无新增 Issue 评论，用户反馈主要隐含在 PR 描述中：

- **独立活动操作** 相关 PR（#10106 及其子 PR）解决了一个明确的用户痛点：用户需要在不修改工作流代码的情况下，通过服务器命令暂停、重置或修改独立活动的选项。修复的延迟问题、还原选项等问题反映了早期用户测试中遇到的边缘案例。
- **集群移除验证** 的修复 (#10997) 回应了运维人员在实际集群管理时遇到的错误阻拦。
- **默认重试策略行为** 的修正 (#11010) 表明此前设置 `nil` 策略时行为不一致，可能导致预期外的无限重试，该修复提升了 API 的直观性。

整体上，用户反馈主要集中在 **独立活动的控制力、配置的一致性、运维操作的可靠性** 上。

## 待处理积压

以下开放 PR 持续时间较长，可能影响功能交付或社区信心，建议维护者重点关注：

1. **[#10106](https://github.com/temporalio/temporal/pull/10106) – Implement Pause/Unpause/Reset/UpdateOptions for standalone activities**  
  开放 74 天，是独立活动控制功能的核心 PR，依赖多次迭代。目前已有多个修复性 PR 合入，此主 PR 应尽快收尾合并。
2. **[#10742](https://github.com/temporalio/temporal/pull/10742) – Improve memory diagnostics for test jobs**  
  开放 25 天，对 CI 稳定性有直接帮助，可减少偶发 OOM 的排查成本。
3. **[#10890](https://github.com/temporalio/temporal/pull/10890) – feat(events): structured event framework**  
  开放 11 天，作为可观测性基础设施，需要与团队对齐接口设计后推动合并。
4. **[#10975](https://github.com/temporalio/temporal/pull/10975) – wf-pause: allow pausing a workflow before the first workflow task**  
  开放 3 天，与 #10106 系列相关，合并优先级较高。

此外，仓库中存在 28 个 **待合并** 的开放 PR，建议团队安排评审资源，减少积压。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*