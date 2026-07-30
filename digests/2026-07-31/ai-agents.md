# OpenClaw 生态日报 2026-07-31

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-30 23:28 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，以下是针对 OpenClaw 项目生成的 2026-07-31 项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-07-31

## 1. 今日速览

OpenClaw 项目在 2026年7月30日表现出极高的社区参与度和开发活跃度。过去 24 小时内，项目新增和活跃的 Issue 数量高达 488 条，同时有 425 个 Pull Request 处于待合并状态，表明社区贡献热情高涨，但也给维护团队带来了巨大的审查和合并压力。虽然今日无正式版本发布，但 PR 合并/关闭量达到 75 个，显示项目修复和功能推进工作仍在有序进行。当前社区焦点主要集中在 **消息丢失、会话状态异常、安全边界、以及 Crash-Loop 稳定性** 等核心痛点之上。项目健康度整体积极，但 **维护者审查和产品决策的瓶颈问题愈发突出**，大量 P1 和 P2 级别的高优问题长期等待定论。

## 2. 版本发布

**无**。过去 24 小时内未有新版本发布。

## 3. 项目进展

尽管合并效率受限于积压，但今日仍有 75 个 PR 被合并或关闭，在多个关键领域取得了实质性进展：

- **核心稳定性修复**：
    - `#115286`：修复了配置中 `agents.defaults.mediaLocalRoots` 无法被识别的问题，保障了运维人员可以通过该配置授权从受信任目录发送本地文件。
    - `#114633`：修复了系统代理在浏览器或 macOS 界面中给出“退出 OpenClaw 并运行终端命令”这种不可操作指导的问题。
- **关键通道与 UI 修复**：
    - `#116405`：修复了 Matrix 通道中 Agent 回复按钮无法到达聊天室的问题，保证了交互式组件的可用性。
    - `#116579`：修复了在 Tailscale Serve 后面运行 Gateway 时出现的假端口占用报告，改善了网络环境下的用户体检。
- **安全性与兼容性提升**：
    - `#115323`：新增了只读的 `memory.list` RPC 方法，允许管理类客户端枚举 Agent 的记忆内容，增强了监控和管理能力。
    - `#105335`：修复了模型选择被锁定的会话中，代码路径可能拒绝并重置模型覆盖的问题，保证了对 Claude Code 等第三方集成的兼容性。
- **自动化流程优化**：
    - `#116580` ：调整了 CI 中 OpenAI 实时测试配置的启动预算，以解决测试因超时而失败的问题，提升了发布验证的可靠性。
    - `#116567`：由 Bot 自动发起并更新了原生应用的本地化文件，保持了多语言支持的同步。

**项目整体推进了** 对核心 BUG 的修复、渠道客户端的体验优化以及 CI/CD 流程的稳健性。

## 4. 社区热点

今日讨论最为热烈的议题反映了用户在 **消息传递可靠性** 和 **平台生态扩展** 上的深度关切：

- **`#115326` (20条评论)**：[Crash-loop breaker 导致 Discord/WhatsApp 永久沉默](https://github.com/openclaw/openclaw/issues/115326)
    - **用户诉求**：这是一个回归 Bug，用户报告在 Gateway 启动后，Crash-loop 断路器机制错误地永久抑制了 Discord 和 WhatsApp 的消息收发，且文档中提供的恢复路径 (`channels.start`) 因 WebSocket 1006 错误而失效。社区成员对“消息传递完全静默”这一严重问题表达了强烈的担忧和挫折感，迫切需要一个可靠的修复方案。

- **`#50090` (15条评论)**：[社区技能开发与 ClawHub 生态](https://github.com/openclaw/openclaw/issues/50090)
    - **用户诉求**：这是对 ClawHub 技能市场的长期讨论。用户肯定了 `SKILL.md` 带来的生态潜力，但直言当前“承诺与实践之间存在巨大鸿沟”。社区反馈的核心痛点在于技能安装、配置和使用体验不佳（如 `$XDG_CONFIG_HOME` 不解析），希望项目能优先解决基础设施的一致性和易用性问题，让第三方技能能够真正“即装即用”。

- **`#99551` (16条评论)**：[Codex 工作器失控硬化跟踪](https://github.com/openclaw/openclaw/issues/99551) & **`#48003` (15条评论)**：[Steer 模式无法在中途注入消息](https://github.com/openclaw/openclaw/issues/48003)
    - **技术深度讨论**：这两条 Issue 代表了社区对特定功能缺陷的深度分析和跟踪。前者是围绕“Codex 工作器失控”事件的系统性硬化方案，涉及安全性和会话状态；后者则深入分析了 `messages.queue.mode: "steer"` 功能失效的根本原因（`KeyedAsyncQueue` 引入的回归）。这些讨论体现了高级用户对内部机制的理解和对关键功能的依赖。

## 5. Bug 与稳定性

今日报告的 Bug 主要集中在稳定性、消息丢失和安全相关领域，按严重程度排列如下：

**P0 (灾难性)**
- `#48920` [**O**]：Live 文档超前于 Release 版本，大量新配置项无法在现有版本使用。
    - 已有 Fix PR? 否。

**P1 (高优先级)**
- `#115326` [**O**]： **(消息丢失/Crash-Loop)** Crash-loop breaker 永久抑制 Discord/WhatsApp ，且恢复路径失效。社区反馈最热烈。
    - 已有 Fix PR? 否。
- `#49876` [**O**]： **(安全/幻觉)** Cron 会话在工具调用失败时，会生成幻觉输出并发送给用户，造成信任与安全问题。
    - 已有 Fix PR? 否。
- `#57326` [**O**]： **(会话状态/安全)** CLI 后端辅助路径仍绕过 CLI 调度，存在安全风险。
    - 已有 Fix PR? 否。
- `#74586` [**O**]： **(会话状态)** AM 嵌入式运行中止 `memory_search` 工具调用，并误判为超时。
    - 已有 Fix PR? 否。
- `#51396` [**O**]： **(回归/安全)** `clearUnboundScopes` 无条件剥离非本地 Token 认证客户端的操作员权限。
    - 已有 Fix PR? 否（但有 `linked-pr-open` 标签）。
- `#53540` [**O**]： **(消息丢失)** 嵌入式运行器因 LLM 生成大参数工具时延超过底层请求超时而报错失败。
    - 已有 Fix PR? 否。
- `#115909` [**O**]： **(安全/可用性)** 捆绑的浏览器 Copilot 客户端因 WebSocket 认证逻辑问题，永远无法完成配对连接。
    - 已有 Fix PR? 否。

**P2 (中等优先级)**
- `#115001` [**O**]： **(行为错误)** Hybrid 记忆搜索因 FTS LIKE 兜底逻辑返回虚假的高相似度分数。
    - 已有 Fix PR? 否。
- `#53408` [**O**]： **(行为错误)** `write/exec` 工具参数在长对话后会被静默丢弃，导致工具调用失败。
    - 已有 Fix PR? 否。
- `#52186` [**O**]： **(行为错误)** ElevenLabs TTS 成功生成音频，但客户端仍播放 OpenAI 语音。
    - 已有 Fix PR? 否。

## 6. 功能请求与路线图信号

今日涌现的功能请求主要集中在 **会话管理、渠道能力增强和系统可观察性** 上，部分已有关联 PR，可能被纳入下一阶段规划：

- **多会话架构 (RFC)** (`#48874`)：提出了“共享 LLM + 隔离会话 + 公共知识库”的架构，旨在节省资源并实现会话间隔离。该方案若被采纳，将是一个重大的架构演进信号。
- **持久化任务状态界面** (`#52640`)：为长时间运行的频道任务（如 Discord）提供一个权威的、持久的进度 / 状态展示。此功能与 Agent 的实用性和透明性密切相关，用户呼声较高。
- **会话标签/昵称功能** (`#55249`)：希望为晦涩的会话 key 添加用户友好的别名，以提升 Dashboard 的管理效率。这是一个典型的 UX 优化需求，实施难度较低。
- **Discord 编辑/删除事件支持** (`#53654`)：允许用户通过编辑消息来重新触发 Agent 处理，通过删除消息来取消处理。这是一个与主流聊天机器人平台（如 Discord 自身）对齐的功能，对交互体验提升显著。
- **Agent 间可见消息传递 (ACP)** (`#50798`)：允许协调 Agent 向子会话的 Discord 线程发送可见消息，而不创建污染路由的“主会话”。这表明社区对复杂的多 Agent 协作场景有更深层的需求。
- **保留最后 N 条原始消息** (`#58818`)：提出在上下文压缩和会话重置后，仍保证 Agent 能看到最近的原始消息。这是对当前“上下文窗口”管理机制的补充，有助于 Agent 更好地理解对话上下文。
    - 已有 Fix PR? 关联网址内无，但此需求与 compaction 行为高度相关。

## 7. 用户反馈摘要

从今日的 Issue 评论中可以提炼出以下真实用户痛点：

- **“硬编码路径”引发的信任危机**：`#51429` 的用户愤怒地指出，代码中硬编码了某位开发者 (`wangtao`) 的工作路径，导致新安装的 OpenClaw 在用户系统上错误地创建了不期望的目录。这不仅是一个 Bug，更严重损害了开源社区的信任感。
- **模型过度安全限制的挫败感**：`#48104` 的用户反馈，模型的内置安全/道德边界会阻止其执行管理员明确授权的运维任务（如 SSH 诊断）。用户认为，在 Operator 工作流中，模型不应越俎代庖进行价值判断。
- **iOS/WebChat 沉默的困惑**：`#97983` 的用户报告，官方 iOS 应用和 WebChat 的消息能加入本地 transcript，但无法可靠地触发 Agent 回复。用户尝试各种方法未果，体现了官方客户端核心功能缺失带来的困扰。
- **对于“承诺 vs. 现实”的期待**：正如 `#50090` 所讨论的，社区对 OpenClaw 的“技能市场”前景充满期待，但当前复杂的配置和安装体验让用户感到失望。用户希望项目能优先打磨好基础体验，再谈生态壮大。

## 8. 待处理积压

以下为长期未响应的高优问题，已严重影响用户体验，需维护者优先介入审查与决策：

- **`#99551`** (P1，创建于 2026-07-03)：[Codex 工作器失控硬化跟踪](https://github.com/openclaw/openclaw/issues/99551)。虽然维护者已参与，但涉及的多项子 Issue 及其复杂的安全设计决策，需要尽快获得产品层面的认可与释放。
- **`#48003`** (P1，创建于 2026-03-16)：[Steer 模式无法在中途注入消息](https://github.com/openclaw/openclaw/issues/48003)。一个被分析了根本原因的回归 Bug，但仍因 `needs-product-decision` 标签而停滞。
- **`#31331`** (P1，创建于 2026-03-02)：[Docker + Sandbox 无法访问工作空间](https://github.com/openclaw/openclaw/issues/31331)。一个存在近五个月的高优问题，对使用 Docker 部署的用户是严重阻碍。即便有 Fix PR 链接，但标签仍为 `needs-product-decision`。
- **`#47910`** (P1，创建于 2026-03-16)：[按失败类别进行提供商故障转移](https://github.com/openclaw/openclaw/issues/47910)。一个能显著提升系统可用性的成熟方案，但因对架构有影响而停留在决策阶段，迟迟未能落地。
- **`#50291`** (P2，创建于 2026-03-19)：[插件 Hook 缺乏追踪上下文](https://github.com/openclaw/openclaw/issues/50291)。对于依赖可观测性进行故障排查的运维人员是持续痛点，但至今仍缺乏产品层面的优先级认可。

---

## 横向生态对比

# AI 智能体与个人 AI 助手开源生态横向对比分析报告 | 2026-07-31

---

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态整体呈现 **“高贡献涌入与维护瓶颈并存”** 的态势。头部项目（OpenClaw、Hermes Agent）日增 Issue/PR 均超 400 条，但合并率普遍低于 15%，核心维护团队面临严峻的审查积压压力。安全加固与稳定性修复成为各项目共识：OpenClaw 修复了消息丢失与凭证泄露，OpenHands SDK 紧急发布 v1.39.1 安全补丁，LiteLLM 修复了护栏旁路和预算控制缺陷。与此同时，社区对 **企业级治理（审计、预算、访问控制）、多平台兼容性（Windows/Wayland）、开发者体验（暗黑模式、TUI 性能）** 的需求显著上升，表明生态正从“能用”向“好用、可管”过渡。

---

## 2. 各项目活跃度对比

| 项目 | 新增/活跃 Issues | 待合并 PR | 合并/关闭 PR | 版本发布 | 健康度评估 |
|------|-----------------|-----------|-------------|---------|-----------|
| **OpenClaw** | 488 | 425 | 75 | 无 | **高活跃但维护瓶颈严重**，P1/P2 问题堆积 |
| **Hermes Agent** | 471（新开+活跃） | 450 | 50 | 无 | **极高涌入、合并率仅 5-10%**，严重 Bug 长期未修 |
| **OpenHands SDK** | 46（更新） | 47 | 5+8=13 | v1.39.1（安全补丁） | **中等活跃、响应及时**，安全修复优先 |
| **Pi** | 91（处理） | 32 | 24（PR） | 无 | **高效维护**，合并率 75%，架构稳步推进 |
| **LiteLLM** | 57（新开+活跃） | 151 | 80 | v1.95.0-rc.1 | **重度积压但核心功能迭代快**，运维方向修复多 |
| **Temporal** | 隐私数据* | 38 | 7 | 无 | **中等活跃、合并速度慢**，发现严重数据竞争 Bug |

> *Temporal 未提供 Issues 总数，仅 45 条 PR 活动，7 条合并。  
> 极端活跃阈值：OpenClaw、Hermes Agent 日增 Issue/PR 均超 400，接近社区“洪峰”状态。

---

## 3. OpenClaw 在生态中的定位

**核心优势**：
- **社区规模与贡献量领先**：日增 Issues 488 条，PR 425 条，远超其他项目，表明开发者生态最强。
- **功能纵深最强**：修复了消息丢失、会话状态、Crash-Loop 等核心稳定性问题，同时推进 ClawHub 技能市场、多 Agent 协作（ACP）等高级功能。
- **用户痛点明确**：社区反馈极具代表性，涵盖嵌入式运行、安全边界的深度技术讨论，反映其被用于高复杂度场景。

**技术路线差异**：
- 采用 **Agent 间可见消息传递（ACP）** 和 **技能插件体系（SKILL.md）**，架构上强调模块化和生态扩展。
- 与 LiteLLM 的轻量代理定位不同，OpenClaw 是一个包含运行时、网关、UI 的完整平台；与 Pi 的终端优先设计不同，OpenClaw 侧重多渠道（Discord、WhatsApp、WebChat）统一体验。

**社区规模对比**：
- 日活 Issue/PR 数量约为 Pi 的 5-10 倍，Hermes Agent 的 1.1 倍，OpenHands SDK 的 10 倍。但合并效率仅为 Pi 的 30%，瓶颈问题最为突出。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|----------|----------|----------|
| **安全边界与审计** | OpenClaw、OpenHands SDK、LiteLLM、Temporal | 凭证泄露防护（OpenClaw #115286、OpenHands #3990）、护栏扫描（LiteLLM #35257）、记忆投毒防御（OpenHands #4251）、数据竞争（Temporal #11352） |
| **预算/成本控制** | OpenClaw、OpenHands SDK、LiteLLM | 临时预算提升、多窗口预算（LiteLLM #35265）、成本门控（OpenHands #4273）、防止模型幻觉造成浪费 |
| **多平台兼容性** | Hermes Agent、Pi、LiteLLM | Windows Terminal 滚动失效（Pi #6502）、Wayland 剪贴板（Pi #7248）、桌面 CPU 满载（Hermes #73082）、暗黑模式（LiteLLM #10177） |
| **流式传输与工具调用完整性** | LiteLLM、OpenClaw | stream_chunk_builder 损坏 Gemini 工具调用（LiteLLM #25869）、流式护栏跳过 |
| **远程/多会话架构** | Pi、OpenClaw、Temporal | 远程会话协议（Pi #7344）、Nexus 操作（Temporal #11274）、共享会话 UID 信封（Hermes #69961） |

---

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent | OpenHands SDK | Pi | LiteLLM | Temporal |
|------|----------|--------------|---------------|----|---------|----------|
| **功能侧重** | 全功能 Agent 平台（多渠道 + 技能市场） | 桌面优先、语音交互、MCP 集成 | SDK/框架，侧重安全与企业治理 | 终端 TUI + 扩展协议，极简设计 | LLM 代理网关，成本与路由控制 | 工作流引擎，时间跳跃与持久协调 |
| **目标用户** | 高级开发者、社区贡献者 | 桌面用户、语音交互爱好者 | 企业开发者、DevOps | 开发者、远程沙箱用户 | 平台运维、成本管控团队 | 后端工程师、微服务协调者 |
| **技术架构** | 单体 + 网关 + 插件生态 | 模块化 + 桌面端 + ACP | 可插拔 SDK + 安全层 | 终端应用 + 远程协议 | 轻量代理 + 多供应商路由 | 分布式事务工作流 |
| **当前阶段** | 快速迭代但维护承压 | 高产但合并能力落后 | 安全加固期 | 架构重构期（远程协议） | 稳定迭代 + 极限修复 | 功能延展期（Nexus） |

---

## 6. 社区热度与成熟度分层

**第一梯队（极高热度，快速迭代阶段）**：
- **OpenClaw**、**Hermes Agent**：日新增 Issue/PR 均超 400，社区贡献爆炸，但维护响应严重滞后，Bug 修复周期长。适合愿意参与早期贡献、容忍不稳定的开发者。

**第二梯队（较高热度，质量巩固阶段）**：
- **LiteLLM**：PR 积压 151 条，但合并率 35% 左右，且持续发布 RC 版和补丁，运维方向修复密集。适合生产环境对成本和合规要求高的用户。
- **Pi**：合并率高达 75%，架构进展迅速，社区反馈正向。适合追求稳定、轻量终端体验的开发者。

**第三梯队（中等热度，安全与企业化阶段）**：
- **OpenHands SDK**：活跃度适中，发布安全补丁及时，功能请求偏向企业治理。适合企业级安全集成场景。
- **Temporal**：专注工作流引擎，社区讨论偏向技术深度，迭代节奏稳定。适合有复杂状态管理需求的团队。

---

## 7. 值得关注的趋势信号

1. **安全已成第一优先级**：OpenHands 停止记录运行时信息、LiteLLM 修复护栏旁路、OpenClaw 解决凭证泄漏——各项目不约而同将安全修复放在合并队列前端。**开发者应主动升级至最新安全补丁，并在集成时启用审计日志。**

2. **远程/多会话架构成为主流**：Pi 合并远程会话协议和客户端库，Temporal 推进查询驱动的 Nexus 操作，Hermes 探索共享网关会话 UID。这意味着 AI Agent 正从单机脚本向分布式可协调服务演进。**架构师可提前规划会话亲和性与跨进程通信方案。**

3. **企业治理需求从软需求变硬需求**：预算控制、证据门控、访问控制（OpenHands #4273、LiteLLM #35265）、文件访问白名单——社区明确要求 Agent 行为可审计、可限制。**企业部署需考虑引入治理层插件或自定义 Hook。**

4. **流式+工具调用完整性是普遍挑战**：LiteLLM 的 stream_chunk_builder 损坏 Gemini 工具调用，Hermes MCP keepalive 超时，OpenClaw 的嵌入式运行器因超时报错。**任何涉及流式输出的 Agent 框架都需要对工具调用切片和组装进行严苛测试。**

5. **多平台/多终端体验差距拉大**：Pi 收到大量 Windows Terminal 滚动、Wayland 剪贴板反馈；Hermes 桌面客户端 CPU 满载；LiteLLM 暗黑模式呼声极高。**非 macOS/Linux 用户对桌面体验的不满正在积累，项目方若忽视将丢失大量用户基础。**

---

*报告基于 2026-07-31 各项目 GitHub 公开数据生成，旨在为技术决策者提供横向参考。*

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目日报 — 2026-07-31

---

## 1. 今日速览

过去 24 小时项目收到 **500 条 Issue 更新**（新开/活跃 471，关闭 29）和 **500 条 PR 更新**（待合并 450，合并/关闭 50），无新版本发布。整体活跃度极高，社区提交和讨论溢出，但合并/关闭率仅约 5%–10%，维护者处理积压的速度跟不上新涌入的速度。已知严重 Bug（如桌面客户端 CPU 满载、更新流程损坏、MCP 连接超时等）持续堆积，多项长期功能请求（RAG、多角色路由）仍未落地。项目处于“高产但追赶”状态，可能需要决策者加速关键 PR 的合并或分流。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日合并/关闭的 PR 共 50 条，以下为评论数较高或影响较大的 2 条已关闭 PR：

- **#74887 [CLOSED]** `feat(desktop): route wake voice turns to existing sessions`  
  在桌面端为唤醒词后的语音轮次增加确定性会话路由，支持自然语言指令（如“Hey Hermes — send to the resume session”），解析后自动匹配非存档会话。  
  👉 [https://github.com/NousResearch/hermes-agent/pull/74887](https://github.com/NousResearch/hermes-agent/pull/74887)

- **#75076 [CLOSED]** `fix(mem0): make self-hosted HTTP timeout configurable`  
  将自托管 Mem0 后端的硬编码 30 秒超时改为可通过配置或环境变量调整，解决大记忆批次写入时因超时导致失败的问题。  
  👉 [https://github.com/NousResearch/hermes-agent/pull/75076](https://github.com/NousResearch/hermes-agent/pull/75076)

此外，大量开放 PR 处于待合并状态（450 条），其中包含多个关键 Bugfix（如网关 Footer 重复、WebGL 渲染、OAuth 令牌持久化等）和功能特性（原生语音流、桌面发布火车），但尚未被合并，积压风险上升。

---

## 4. 社区热点

讨论最活跃的 Issues（评论数 8–9 条，👍 较多）：

- **#64231** — [需求裁决] `chore(plugins): lifecycle-event catalog, hook taxonomy, and batch disposition of pending hook PRs`  
  计划将大量零散的 `VALID_HOOKS` 补丁统一整理为生命周期事件目录和钩子分类标准。社区强烈希望清理挂起的钩子 PR。  
  👉 [https://github.com/NousResearch/hermes-agent/issues/64231](https://github.com/NousResearch/hermes-agent/issues/64231)

- **#844** — [Feature] `Knowledgebase RAG System — User-Configured Document Directory...`  
  创建于 3 月 10 日，获 4 个 👍，要求让用户指定文档目录并自动索引/嵌入/检索，被视为工作区概念的一部分。至今未实现，社区持续关注。  
  👉 [https://github.com/NousResearch/hermes-agent/issues/844](https://github.com/NousResearch/hermes-agent/issues/844)

- **#5143** — [Feature] `Multi-Role Auto-Routing via Gateway Hooks`  
  获 15 个 👍，提出通过上下文分类器实现多角色自动路由，并处理路由错误恢复。社区期待度高，已有多轮修订。  
  👉 [https://github.com/NousResearch/hermes-agent/issues/5143](https://github.com/NousResearch/hermes-agent/issues/5143)

- **#73082** — [Bug] `Desktop client renderer/GPU processes spin at 100%+ CPU at idle`  
  P2 级 Bug，导致 macOS 上电池消耗最高、机身发热，严重影响用户体验。评论 7 条。  
  👉 [https://github.com/NousResearch/hermes-agent/issues/73082](https://github.com/NousResearch/hermes-agent/issues/73082)

**诉求分析**：用户对三大方向呼声最高：① 清理钩子系统（#64231）；② 知识库 RAG 功能（#844）；③ 多角色/多平台路由（#5143）。同时，桌面端性能问题和更新流程故障是当前最主要的体验痛点。

---

## 5. Bug 与稳定性

以下为今日活跃的 Bug（按严重程度排列），已附对应的修复 PR（如有）：

### P2 级别（严重）

| Bug 标题 | 创建日期 | 简要描述 | 是否有 fix PR |
|----------|----------|----------|---------------|
| **#73082** —— Desktop CPU 100% idle | 07-28 | Electron 渲染进程/GPU 空闲时占用 50-90% CPU，导致发热和高能耗 | 无 |
| **#73237** —— 401 不重试直接降级 | 07-28 | 静态 API key 的 provider 收到 401 后不重试，立即切换到后备 provider，浪费配置 | 无 |
| **#74805** —— Windows 更新竞争 | 07-30 | 桌面底部栏更新按钮第一次执行时因“另一进程占用”失败，不会自动重试 | 无 |
| **#74973** —— macOS 更新静默跳过网关重启 | 07-30 | `hermes update` 完成后网关已停止并从 launchd 卸载，但显示成功 | 无 |
| **#69178** —— Discord /model 和 /profile 忽略多路复用路由 | 07-22 | 原生斜杠命令不携带足够元数据，导致多配置文件路由失效 | 无 |
| **#53676** —— MCP HTTP 传输初始化失败 | 06-27 | WigAI 服务器正常，但 Hermes 收到 400 导致 0 个活跃 MCP 服务器 | 无 |
| **#62548** —— ACP 背景完成通知丢失 | 07-11 | 使用 ACP 适配器时，`terminal(background=true, notify_on_complete=true)` 的完成通知无法送达客户端 | 无 |
| **#65787** —— MCP keepalive 超时 + 重连循环 | 07-16 | keepalive 使用 `list_tools()` 导致 O(工具数量) 开销，大服务器必超时 | 无 |
| **#67453** —— `key_env` 仅对首个会话生效 | 07-19 | 自定义 provider 的 `key_env` 在网关重启后只能解析一次，后续会话全部 401/403 | 无 |
| **#69398** —— 配对存储路径变更导致审批失效 | 07-22 | 升级后配对审批文件路径改变，旧审批不再被读取，需重新审批 | 无 |

### P3 级别（一般）

- **#74973**（已列）、#62170（TUI 会话切换后内容陈旧）、#71995（绝对路径绕过硬编码安全底线）、#74313（无效输出中 usage 不计入计费）、#58576（Web 事件循环因 GIL 阻塞 51s）、#19337（MiniMax OAuth 跳转到已删除页面）、#38161（update 中断后报成功，无完整性检查）、#29023（WhatsApp 回复检测因设备后缀不匹配失败）等。

**一部分 Bug 已有修复 PR 在排队**：如 #75081（修复 FTS 转录重复写入）、#75079（修复 runtime footer 遗漏）、#75080（修复 no-sandbox 启动标志）、#75078（修复 Discord 语音首帧 STT 垃圾）、#75077（修复 Codex 应用服务器路径下重复回复）、#75075（Buzz 适配器强化）等。但这些 PR 本身也处于“开放待合并”状态，并未进入主线。

---

## 6. 功能请求与路线图信号

### 高热度、可能纳入下一版本的功能

- **#844** — 知识库 RAG 系统（用户指定文档目录、嵌入、混合搜索、自动检索）  
  被标记为 P3，但社区持续要求，若负责人加快决策可能会进入 v0.19 路线图。

- **#5143** — 多角色自动路由（通过网关钩子实现上下文分类器和误路由恢复）  
  已有详细 v2 方案，PR 待定，可能适配 v0.14 后的新架构。

- **#64231** — 插件生命周期事件目录和钩子分类标准  
  旨在一次性清理所有挂起的 `VALID_HOOKS` 补丁，项目维护者 @teknium1 已在参与讨论。

- **#62595** — 主题感知压缩（topic-aware compaction）  
  解决多主题短消息会话（如 Feishu/WeChat）上下文压缩时产生混合错误摘要的问题。

- **#54204** — 允许已有会话从一个 workspace 移动到另一个  
  桌面端 UI 需求，对项目管理很重要。

- **#56865** — 添加本地终端子进程内存保护  
  防止重型任务（构建、测试）导致整个网关 OOM。

- **#69961** — 共享网关会话的受信任发送者 UID 信封  
  为 Slack/Discord/Telegram 共享线程提供平台验证的发送者身份。

### 已有关联 PR 的信号

- **#35040** — 原生语音轮次流式端点（SSE），可能引入 `POST /api/voice/turns/stream`。  
- **#67809** — 添加已验证的桌面发布火车（本地、闭环）。  
- **#67822** — 修复桌面端围栏文件列表渲染为代码块。  
- **#46682** — 使网关审批信息更可读（摘要式分类）。  

这些 PR 表明项目正在向**桌面端体验优化、语音交互标准化、安全审计增强**方向演进。

---

## 7. 用户反馈摘要

从 Issues 评论中提炼的真实用户声音：

- **“桌面客户端发热、风扇狂转”** ：多次提及 macOS 上高 CPU 占用和电池消耗问题，严重影响日常使用，用户希望尽快修复（#73082）。
- **“TUI 会话切换后显示的是旧内容”** ：使用 v0.18.1 Docker 版本的用户反映，切换到另一个 session 后，界面停留在上一个 session 的缓存，需手动刷新（#62170）。
- **“Windows 更新总是第一次失败”** ：点击桌面底部栏的更新按钮，首次尝试因文件占用失败，第二次才能成功；用户担心更新可能不完整（#74805）。
- **“macOS 更新后网关直接挂了，没有任何提示”** ：执行 `hermes update` 显示成功，但网关已被卸载，消息通道中断，用户不得不手动修复（#74973）。
- **“自定义 provider 的 API key 环境变量只被读取一次”** ：配置了 `key_env` 后，网关启动后的第一个会话正常，后续所有会话都返回 401/403，用户需要每次重启网关（#67453）。
- **“Discord 原生斜杠命令不遵守多配置文件路由”** ：已设置 `multiplex_profiles: true` 和 `profile_routes`，但普通消息正常路由，斜杠命令却被忽略（#69178）。
- **“MCP 服务器超时频繁，keepalive 反而造成更大负载”** ：大 MCP 服务器的 `list_tools` 响应慢，导致 keepalive 超时并反复重连循环（#65787）。
- **“升级后配对审批莫名其妙的消失了”** ：从 0.18.x 升级后，原有的 Telegram 配对审批因路径变化而失效，用户需要重新审批（#69398）。

这些反馈集中反映了**更新可靠性、多平台一致性、性能稳定性**是当前用户最不满意的三个维度。

---

## 8. 待处理积压

以下为创建超过一个月且仍有社区关注的未关闭重要 Issue/PR，建议维护者尽快评估或分配资源：

| 编号 | 标题 | 创建日期 | 标签 | 建议 | 链接 |
|------|------|----------|------|------|------|
| #844 | Knowledgebase RAG System | 2026-03-10 | feature, P3 | 社区等待 4 个月，建议明确是否进入路线图，或标记为未来规划 | [Issue](https://github.com/NousResearch/hermes-agent/issues/844) |
| #5143 | Multi-Role Auto-Routing via Gateway Hooks | 2026-04-04 | feature, P3 | 已有 v2 方案，15 个 👍，决策为何停滞？ | [Issue](https://github.com/NousResearch/hermes-agent/issues/5143) |
| #35763 | Hindsight memory provider 反复初始化，计数器重置 | 2026-05-31 | bug, P3 | 影响 `retain_every_n_turns` 功能，但无人认领 | [Issue](https://github.com/NousResearch/hermes-agent/issues/35763) |
| #19337 | MiniMax OAuth 指向已删除页面 | 2026-05-03 | bug, P2 | MiniMax 用户无法完成 OAuth 授权，急需修复 | [Issue](https://github.com/NousResearch/hermes-agent/issues/19337) |
| #29023 | WhatsApp 回复检测失败（设备后缀不匹配） | 2026-05

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，这是根据您提供的 OpenHands SDK 数据生成的 2026-07-31 项目动态日报。

---

# OpenHands SDK 项目动态日报 | 2026-07-31

## 1. 今日速览

今日项目处于高度活跃状态，社区贡献与讨论力度均处高位。过去 24 小时内，有 **46 条 Issue** 和 **47 条 PR** 被更新，虽然合并/关闭数量较少（分别为 5 和 8），但大量 PR 处于“待合并”状态，表明项目正在进行密集的代码审查与功能整合。同时，项目发布了 **v1.39.1** 安全补丁，并有多项围绕**安全增强**与**企业级治理**的深层讨论，反映出项目在追求功能丰富的同时，正将稳定性和安全性置于优先位置。

## 2. 版本发布

**v1.39.1 (Patch Release)**
- **主要更新：**
    - `fix(security)`: **停止记录运行时信息**，这是一项重要的安全修复，旨在防止敏感信息在日志中泄露。
    - `fix(ci)`: 修复了发布版本时，Smoke Test 容器的端口绑定问题。
    - `chore(release)`: 移除了发布流程清单中的一项检查项，简化了发布步骤。
- **破坏性变更：** 无
- **迁移注意事项：** 无特殊迁移步骤，建议用户更新到此版本以获得最新的安全修复。
- **链接：** https://github.com/OpenHands/software-agent-sdk/releases/tag/v1.39.1

## 3. 项目进展

今日合并或关闭的 PR 推动了以下方向，项目在**安全加固、API 清理** 和 **基础设施优化** 上稳步前进：

- **安全修复 (已合并):**
    - **PR #3990**: 修复了 `FileSecretsStore` 将明文 `secrets.json` 写入工作区目录的问题，确保密钥文件不会被错误地持久化到工作区中。
    - **PR #4175**: 修复了 `git remote -v` 命令输出中暴露的 GitHub 证书 (Token) 问题，新 PR 将对终端输出进行智能检测与红action。
    - **PR #3584**: 修复了向 `agent-server` 发送 POST 请求时 `X-Session-API-Key` 头信息缺失的问题，确保了会话认证的完整性。
- **API 与工作流清理 (已合并):**
    - **PR #4004**: 标记了已废弃的兼容性别名和遗留的 MCP 字段，并发出弃用警告，为未来的 API 清理做准备。
    - **PR #4299**: 移除了与当前工作流冲突的自动化 QA 工作流，简化了 CI 流程。
- **依赖更新 (已合并):**
    - **PR #4306**: 将 `joserfc` 库从 1.6.4 升级至 1.6.8，这是一个关键的安全依赖，修复了包括拒绝空 OctKey 在内的安全问题。

**项目进展总结：** 核心工作集中在解决关键安全漏洞和清理遗留代码，这为后续新功能的引入奠定了更稳固的基础。

## 4. 社区热点

今日社区讨论最为热烈的话题，主要集中在 **AI Agent 的安全边界** 与 **企业级部署** 两大领域。

- **热点 Issue #1: 内存投毒防御**
    - **#4251**: [Security: OWASP Agent Memory Guard integration for memory poisoning defense](https://github.com/OpenHands/software-agent-sdk/issues/4251)
    - **评论数: 21**
    - **核心诉求：** 用户提出了对 Agent 长期记忆被恶意污染的担忧，并请求集成 OWASP Memory Guard 等防护机制。这反映了社区对 Agent 在长时间、高自主性操作下安全性的普遍关切。

- **热点 Issue #2: PR 中的截图支持**
    - **#4235**: [Add support for including screenshots in PRs](https://github.com/OpenHands/software-agent-sdk/issues/4235)
    - **评论数: 18**
    - **核心诉求：** 用户希望 Agent 在创建 PR 时，能自动将生成的 Web 页面截图作为可视化证据附加到 PR 描述中。诉求背后是提升代码审查的效率与体验，让审查者能快速直观地看到变更效果。

## 5. Bug 与稳定性

今日报告了多个影响系统稳定性和可用性的 Bug，按严重程度排列如下：

- **高严重性：**
    - **[Bug]: Missing required parameters: ‘security_risk’** ([#4248](https://github.com/OpenHands/software-agent-sdk/issues/4248)): 使用 DeepSeek 模型时，`execute_bash` 函数缺少 `security_risk` 参数，导致功能不可用。
    - **[Bug]: Agent-Server Webhook 连接失败导致容器崩溃** ([#4245](https://github.com/OpenHands/software-agent-sdk/issues/4245)): Webhook 连接问题会引发容器崩溃和沙箱连接错误，严重影响后端稳定性。
    - **[Bug]: 使用 Ollama 时出现 5 分钟超时** ([#4255](https://github.com/OpenHands/software-agent-sdk/issues/4255)): 用户在 UI 或配置文件中设置的超时时间无效，任务超过 300 秒即被强制终止。

- **中严重性：**
    - **[Bug]: LM Studio 无法提供 LLM Provider** ([#4247](https://github.com/OpenHands/software-agent-sdk/issues/4247)): 用户无法在 LM Studio 环境中设置 LLM Provider，导致无法启动本地模型。
    - **[Bug]: 全局技能无法加载** ([#4252](https://github.com/OpenHands/software-agent-sdk/issues/4252)): 新添加的全局技能（Global Skills）在 CLI 和 WebUI 中均无法加载和使用。
    - **[Bug]: 浏览器功能在容器内损坏** ([#4256](https://github.com/OpenHands/software-agent-sdk/issues/4256)): Agent-server Docker 镜像中的 `browser-use` 启动 Chromium 时缺少 `--no-sandbox` 参数，导致浏览器功能完全不可用。

- **已有修复 PR 的 Bug：**
    - **[Bug]: GitHub credentials in git remote URLs are not redacted** ([#4271](与 PR #4175 相关)): 与 PR #4175 同时修复，该 PR 今日已合并。

## 6. 功能请求与路线图信号

今日多个功能请求从基础功能完善向**企业级治理**和**高级安全模型**演进，显示出社区对 OpenHands 更深层次应用场景的期待：

- **潜在下一版本功能：**
    - **[Enhancement]: 凭证存储集成** ([#4241](https://github.com/OpenHands/software-agent-sdk/issues/4241)): 允许 Agent 在运行时自动登录私有资源，是解决私有仓库、数据库等场景的关键。
    - **[Enhancement]: 可插拔的持久化执行后端** ([#4254](https://github.com/OpenHands/software-agent-sdk/issues/4254)): 用于处理超长任务的 Agent 会话，提升任务完成的可靠性。
    - **[Enhancement]: 证据门控** ([#4259](https://github.com/OpenHands/software-agent-sdk/issues/4259)): 允许审核者在 Agent 执行关键操作（如代码修改、文件删除）前进行审查和放行。

- **路线图信号：**
    - **[Feature]: 治理层** ([#4273](https://github.com/OpenHands/software-agent-sdk/issues/4273)): 提出的“文件访问控制、命令白名单、成本预算”等功能，是确保 OpenHands 能在受监管的企业环境中部署的关键路线图信号。
    - **[PRD]: 重新思考技能管理** ([#4243](https://github.com/OpenHands/software-agent-sdk/issues/4243)): 当前的“微代理管理”界面已落后于 Agent 技能体系的发展，社区呼吁对 Agent 技能进行全面的重新设计。

## 7. 用户反馈摘要

从 Issue 和 PR 评论中可以提炼出以下关键用户反馈：

- **痛点与不满：**
    - **用户体验受阻：** 许多用户反映，在与本地 LLM（如 Ollama, LM Studio）集成时，面临着超时不可配置、Provider 无法识别等基础性问题，严重阻碍了本地部署的尝试。
    - **功能不稳定：** 浏览器沙箱、全局技能等核心功能的频繁报错（如 `#4252`, `#4256`），降低了用户对 SDK 稳定性的信心。
    - **调试成本高：** 社区反馈中频繁出现“无视觉反馈”、“无错误通知”（如 `#4246`），用户在遇到 Agent 挂起或超时等问题时，缺乏清晰的诊断信息。

- **满意与期望：**
    - **对安全改进的积极回应：** 用户对直接关闭和修复凭证泄露等严重安全问题（`#3989`, `#4271`）的 PR 反应积极，这表明用户高度认可项目对安全性的重视。
    - **期待更高阶的功能：** 用户需求已从“能运行”转向“能管理”。企业级用户明确表示了对 Agent 行为有审计、控制和预算管理的需求（`#4259`, `#4273`）。

## 8. 待处理积压

以下关键议题需要引起维护者的关注，它们开放时间长、社区有较高期待或与项目核心方向紧密相关：

- **高影响力待合并 PR:**
    - **PR #3939**: [ci: adopt release-actions (release-please) for automated releases](https://github.com/OpenHands/software-agent-sdk/pull/3939) - **自 7 月 1 日起已开放近一个月，至今为 Draft 状态。** 此 PR 旨在实现自动化的版本发布流程，对于项目维护意义重大，建议尽快审视并推进。
    - **PR #3563**: [feat(security): supply-chain typosquat analyzer on shared shell parser](https://github.com/OpenHands/software-agent-sdk/pull/3563) - **自 6 月 8 日起开放，已有人类测试通过。** 该 PR 为 shell 命令解析器添加供应链攻击检测能力，是重要的安全特性，应考虑合并。

- **长期未响应但高需求的功能请求:**
    - **Issue #4235**: [Add support for including screenshots in PRs](https://github.com/OpenHands/software-agent-sdk/issues/4235) - **自 2025 年 8 月起开放，已获 2 个 👍，评论 18 条。** 社区对此提升代码审查体验的功能呼声很高。
    - **Issue #4242**: [Frontmatter field for multiple repos](https://github.com/OpenHands/software-agent-sdk/issues/4242) - **自 2025 年 12 月起开放，评论 15 条。** 允许在文档头部指定多个仓库进行克隆，是提升多仓库项目处理能力的基础需求。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，这是根据您提供的 Pi 项目 GitHub 数据生成的 2026-07-31 项目动态日报。

---

## Pi 项目动态日报 | 2026-07-31

### 今日速览

今日项目整体活跃度极高，社区贡献与核心维护均表现强劲。过去24小时内，项目共处理了 91 条 Issue 和 32 个 PR，其中关闭/合并了 74 个 Issue 和 24 个 PR，展现了高效的维护响应能力。虽然无新版本发布，但多个重量级 PR 的合并（如远程会话协议 `pi-protocol` 和 Markdown 渲染 API）标志着项目在架构和 API 层面取得了重要进展。与此同时，社区反馈集中在 TUI 性能优化、跨平台兼容性（特别是 Windows 和 Wayland）以及对 Anthropic/Gemini 等提供商的支持改进上。

### 版本发布

无。

### 项目进展

今日核心进展体现在架构重构和关键功能落地上，多个重要 PR 已合并，项目整体向前迈出一大步。

- **远程会话协议与客户端库**：多个关联 PR 已合并，标志着 `pi` 从单进程应用向远程、多会话架构演进。
    - PR [#7344](https://github.com/earendil-works/pi/pull/7344) 新增了 `@earendil-works/pi-protocol` 包，定义了传输无关的远程会话命令、事件和快照协议。
    - PR [#7348](https://github.com/earendil-works/pi/pull/7348) 新增了 `@earendil-works/pi-client` 包，提供了一个运行时中立的会话客户端，用于与远程 Pi 服务器交互。
    - PR [#7346](https://github.com/earendil-works/pi/pull/7346) 在 `pi-ai` 和 `pi-protocol` 之间共享运行时模式，统一了技术栈。
    - PR [#7343](https://github.com/earendil-works/pi/pull/7343) 为 `AgentHarness` 添加了优雅关闭的生命周期管理。

- **Markdown 渲染 API 落地**：PR [#7231](https://github.com/earendil-works/pi/pull/7231) 合入，关闭了 [#6747](https://github.com/earendil-works/pi/issues/6747)。该 API 允许扩展在不修改发送给 LLM 的内容的前提下，改变 Agent 消息的 Markdown 渲染效果（例如用于实现公式渲染器）。

- **关键 Bug 修复**：
    - **Wayland 剪贴板支持**：PR [#7261](https://github.com/earendil-works/pi/pull/7261) 合入，修复了 Wayland 环境下 `Ctrl+V` 粘贴失效的问题，现已优先使用 `wl-paste`。
    - **RPC 服务器崩溃修复**：PR [#7309](https://github.com/earendil-works/pi/pull/7309) 合入，为 RPC 标准输出处理器的 `JSON.parse` 添加了 try/catch，防止子进程非 JSON 日志导致主进程崩溃。
    - **终端兼容性修复**：PR [#7340](https://github.com/earendil-works/pi/pull/7340) 修复了在浅色终端背景下，粗体 Markdown 文字因显示为白色而不可见的问题。
    - **SDK 示例更新**：PR [#7306](https://github.com/earendil-works/pi/pull/7306) 合入，更新了自定义模型 SDK 示例，推荐使用 `ModelRuntime` 替代已废弃的 `getModel` API。

- **功能增强**：
    - **实验性 Loadout 管理**：PR [#7148](https://github.com/earendil-works/pi/pull/7148) 开启，允许用户在会话中动态启用或禁用扩展。
    - **搜索索引 (SQLite)**：PR [#7163](https://github.com/earendil-works/pi/pull/7163) 开启，为 `SessionRepo` 增加 `search()` 方法，并使用 FTS5 来提升 SQLite 后端搜索效率。

### 社区热点

今日社区讨论热度较高，主要围绕渲染性能、跨平台特性和 API 设计展开。

- **渲染性能与兼容性**：多个 Issue 聚焦于 TUI 在不同环境下的渲染问题。
    - [#7194](https://github.com/earendil-works/pi/issues/7194) “Pi does a full re-render every 1s” 获得了 7 条评论和 1 个赞，用户报告在远程沙箱环境下，当工具卡片滚动到视口外时，Pi 会每隔 1 秒进行全量重绘，导致严重性能问题。
    - [#5990](https://github.com/earendil-works/pi/issues/5990) “TUI flickers when confirm/select dialog content is taller” 有 6 条评论和 3 个赞，用户发现对话框内容高于终端高度时会导致持续闪烁。
    - [#6502](https://github.com/earendil-works/pi/issues/6502) “Windows Terminal scrolls to the top” 有 5 条评论和 5 个赞（今日最高赞），问题指出 `ESC[3J` 转义序列会清空滚动缓冲区，导致终端反复滚动到顶部。

- **特性请求与 API 讨论**：
    - [#6747](https://github.com/earendil-works/pi/issues/6747) “An API for enhancing agent message markdown” 有 12 条评论，是今日评论最多的 Issue。用户社区对扩展 Markdown 渲染能力有强烈诉求，该请求已通过 PR [#7231](https://github.com/earendil-works/pi/pull/7231) 解决。
    - [#7267](https://github.com/earendil-works/pi/issues/7267) “Discrepancy between custom provider documentation and registerProvider implementation” 收到 5 条评论，社区用户发现自定义提供商文档与 `registerProvider` 接口的实际实现存在差异，引发了对文档准确性的关注。

- **多提供商功能对齐**：
    - [#7161](https://github.com/earendil-works/pi/issues/7161) “anthropic-messages never sends x-client-request-id” 指出相比 OpenAI，Anthropic 路径未发送请求 ID，导致网关无法实现会话亲和性，影响多账户轮询场景。
    - [#7047](https://github.com/earendil-works/pi/issues/7047) “Gemini 3.x tool-call IDs stripped” 报告 Gemini 3.x 模型工具调用的 ID 被丢弃，导致多轮对话中断。

### Bug 与稳定性

今日报告的 Bug 主要集中在 TUI 渲染、跨平台兼容性和协议实现上，多数已有关联的修复 PR。

| 严重程度 | Issue | 问题描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **严重** | [#7194](https://github.com/earendil-works/pi/issues/7194) | 工具卡片移出视口后每 1 秒全量重绘，导致性能瘫痪。 | OPEN |
| **严重** | [#6819](https://github.com/earendil-works/pi/issues/6819) | 提供商未返回 `usage` 数据时，整个会话因 `undefined` 错误永久崩溃。 | CLOSED (标记为no-action) |
| **严重** | [#7007](https://github.com/earendil-works/pi/issues/7007) | 并发 inline UI 对话框导致 Promise 永远不 resolve，造成死锁。 | CLOSED (标记为no-action) |
| **严重** | [#7267](https://github.com/earendil-works/pi/issues/7267) | 自定义提供商文档与 `registerProvider` 实现不一致，导致用户集成失败。 | OPEN (inprogress) |
| **高** | [#7248](https://github.com/earendil-works/pi/issues/7248) | Wayland 下 `Ctrl+V` 粘贴文本静默失败。 | 已修复：PR [#7261](https://github.com/earendil-works/pi/pull/7261) 已合入。 |
| **高** | [#7047](https://github.com/earendil-works/pi/issues/7047) | Gemini 3.x 模型工具调用 ID 被剥离，导致多轮工具调用失败。 | OPEN |
| **高** | [#7304](https://github.com/earendil-works/pi/issues/7304) | Windows Terminal 下，流式输出时，滚动到上方的视图因上方行重排而自动跳回。 | CLOSED |
| **中** | [#7187](https://github.com/earendil-works/pi/issues/7187) | 第三方扩展包清单错误导致核心包解析静默崩溃，永久阻塞用户会话。 | CLOSED |
| **中** | [#7179](https://github.com/earendil-works/pi/issues/7179) | `autocompleteMaxVisible` 设置重启后重置为默认值。 | CLOSED |
| **中** | [#7157](https://github.com/earendil-works/pi/issues/7157) | OpenCode Go 提供商显示名称错误显示为 “OpenCode Zen Go”。 | CLOSED |
| **低** | [#7128](https://github.com/earendil-works/pi/issues/7128) | 系统提示语中新加入的 `PI_*` 环境变量检查规则，导致 Agent 频繁执行不必要的 bash 命令。 | CLOSED (标记为no-action) |

### 功能请求与路线图信号

- **API 扩展与集成**：
    - [#7299](https://github.com/earendil-works/pi/issues/7299) “Expose the existing shouldStopAfterTurn callback through AgentOptions” 请求将底层循环的 `shouldStopAfterTurn` 钩子暴露在 `AgentOptions` 中。这可能是未来增强 Agent 循环控制的一个信号。
    - [#7244](https://github.com/earendil-works/pi/issues/7244) “Enhance `version` to show runtime (bun|node|deno ...)” 请求在 `version` 命令中显示运行环境。这是一个低成本的易用性改进，有助于诊断环境相关的问题。

- **新功能探索**：
    - PR [#7148](https://github.com/earendil-works/pi/pull/7148) “Experimental loadout management” 开启的实验性 Loadout 管理，允许动态开关扩展。若稳定，极有可能纳入下一版本。
    - PR [#7339](https://github.com/earendil-works/pi/pull/7339) “DRAFT: add openai background mode responses” 是对 OpenAI Background Mode Responses API 的初步实现尝试，体现了项目紧跟上游 API 发展的意图。
    - PR [#6534](https://github.com/earendil-works/pi/pull/6534) “feat(ai): add developer message role” 新增开发者消息角色，这是对 RFC 54 的跟进，可能涉及更复杂的人物设定和系统提示迭代。

- **长期呼声**：
    - [#5064](https://github.com/earendil-works/pi/issues/5064) “Add Context Windows option” (4 条评论) 和 [#4174](https://github.com/earendil-works/pi/issues/4174) “Add a Python SDK for pi-agent-core and pi-ai” (4 条评论，4 个赞) 是两个长期存在的功能请求，虽未直接进展，但社区仍有关注。

### 用户反馈摘要

- **正面反馈**：用户 `@polemotionkor-arch` 在报告 Windows 输入问题时，首先表达了“Thank you for this great project”。用户 `@armgabrielyan` 在请求 Python SDK 时表示“I have been using `pi` coding agent and am really fascinated by it. I really like its minimalistic design”。这表明核心用户群体对项目价值和设计理念高度认可。

- **痛点与使用场景**：
    - **远程/沙箱环境**：用户 `@slim-bean` 报告在远程沙箱中使用 Pi 时，因全量重绘导致性能问题，表明有用户深度集成了 Pi 到远程开发环境。
    - **多平台兼容性**：Wayland 和 Windows Terminal 用户报告了显示和交互问题，这表明跨平台支持，特别是非 macOS/Linux 的桌面体验，是用户非常关心的痛点。
    - **提供商网络**：用户 `@mteam88` 报告 Anthropic 缺少 `x-client-request-id` 导致无法使用代理网关，`@mcowger` 报告 Gemini 工具调用 ID 问题，说明企业级用户对模型提供的稳定性、集成度和标准性有较高要求。
    - **技能系统**：用户 `@johnstegeman` 报告引用技能时，Pi 会将技能的安装目录误认为用户项目目录，影响用户对技能系统的信任。

### 待处理积压

以下为长期未响应或需要额外关注的重要 Issue/PR：

- **功能请求**：
    - [#5064](https://github.com/earendil-works/pi/issues/5064) “Add Context Windows option” - 自5月27日开启，虽有4条评论，但无实质性进展。作为对标 Copilot CLI 的关键功能，值得重新审视。
    - [#4174](https://github.com/earendil-works/pi/issues/4174) “Add a Python SDK” - 自5月4日开启，被标记为因大重构而关闭（closed-because-bigrefactor），但社区仍对其有期待。随着项目架构的稳定，是否重新评估此需求？

- **长期 Bug**：
    - [#6300](https://github.com/earendil-works/pi/issues/6300) “[bug] Windows: Input line is redrawn on every keystroke” - 自7月4日开启，评论中有用户提出，但至今未有修复 PR 关联。该 bug 严重影响 Windows 用户体验，应优先处理。
    - [#7153](https://github.com/earendil-works/pi/issues/7153) “`/scoped-models` appears to do nothing for ~5 minutes” - 自7月26日开启，涉及等待模型目录刷新的 5 分钟阻塞问题，严重影响高阶功能的可用性。

- **待审查 PR**：
    - [#7161](https://github.com/earendil-works/pi/issues/7161) “anthropic-messages never sends x-client-request-id” (6条评论)，虽然无关联 PR，但该问题对使用 Anthropic 网关的企业用户影响较大，且实现成本可能不高，可考虑优先修复。
    - [#7121](https://github.com/earendil-works/pi/issues/7121) “fix(tools): byte count in write, false limit warning in find” (3条评论)，

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目日报 2026-07-31

---

## 1. 今日速览

过去24小时项目保持极高活跃度：共处理69条Issue（新开/活跃57条，关闭12条），231条PR（待合并151条，合并/关闭80条），并发布了1个候选版本（v1.95.0-rc.1）。社区对UI暗黑模式、预算控制行为、流式输出保护等话题讨论火热，多个长期Bug（如Redis SSL、Prisma死锁）仍在等待修复。项目整体进入快速迭代节奏，但需注意大量PR积压（151条待合并）和部分核心问题的持续暴露。

---

## 2. 版本发布

- **v1.95.0-rc.1** 🚀  
  [查看发布详情](https://github.com/BerriAI/litellm/releases/tag/v1.95.0-rc.1)  
  本版本为候选发布，主要变更来自Docker镜像签名机制的统一验证。所有LiteLLM Docker镜像已启用cosign签名，每次发布均使用与commit `0112e53` 关联的相同密钥进行签名，提升供应链安全。建议使用Docker部署的用户在拉取镜像前验证签名。  
  **注意**：此版本为RC，尚未标记稳定，生产环境建议等待正式版。

---

## 3. 项目进展

今日合并/关闭的重要PR展示了多个方向的实质性推进：

| PR | 摘要 | 状态 |
|----|------|------|
| [#35267 feat(db): opt-in REPLICA IDENTITY FULL](https://github.com/BerriAI/litellm/pull/35267) | 新增环境变量 `LITELLM_SET_REPLICA_IDENTITY_FULL`，允许PostgreSQL逻辑复制消费者自动设置表级 `REPLICA IDENTITY FULL`，无需手动维护。 | 已合并 |
| [#35274 fix(proxy): only enforce budgets on routes that can spend](https://github.com/BerriAI/litellm/pull/35274) | 修复预算超限用户被锁定全部Admin UI的问题；预算检查现在仅作用于消费类路由（如推理接口），非消费路由（如UI页面、管理API）不再被预算阻断。 | 已合并 |
| [#35268 fix(ui): stop clamping the budgets Budget ID column at 15 characters](https://github.com/BerriAI/litellm/pull/35268) | 修复管理面板中预算ID列被硬编码截断为15字符的问题，现根据内容自适应显示。 | 已合并 |
| [#35277 chore(release): backport #35271 to stable/1.94.x and cut 1.94.1](https://github.com/BerriAI/litellm/pull/35277) | 将#35271（回退 #32005 对团队密钥个人预算强制的变更）反向移植至1.94.x稳定分支，并发布1.94.1补丁版本，修复1.94.0中团队密钥被所有者个人预算误拦截的回归。 | 已合并 |
| [#35263 fix(policy_engine): preserve config-defined policies across DB sync](https://github.com/BerriAI/litellm/pull/35263) | 确保YAML配置中定义的策略和策略附件在数据库连接后仍被强制执行，并暴露于列表API和UI中。 | 已合并 |
| [#35260 fix(proxy): run post_call guardrails on /v1/messages streaming](https://github.com/BerriAI/litellm/pull/35260) | 修复 Anthropic Messages API（`/v1/messages`）流式响应中 `post_call` 护栏被静默跳过的问题，现在会对流式输出进行安全扫描。 | 已合并 |
| [#35265 fix(proxy): apply temp_budget_increase to multi-window budget_limits](https://github.com/BerriAI/litellm/pull/35265) | 修复 `temp_budget_increase` 对多窗口预算（`budget_limits`）完全无效的问题，现在临时预算提升可正确应用于多时间窗口的预算限制。 | 已合并 |

**整体进度**：今日修复集中于预算控制（团队密钥、多窗口预算、非消费路由放行）、数据库复制支持、护栏扫描覆盖、配置策略持久化等运维关键环节。项目在稳定性和合规性上迈出重要一步。

---

## 4. 社区热点

以下议题在过去24小时内获得最多评论和互动，反映了社区的强烈诉求：

| Issue | 标题 | 评论数 | 👍 | 状态 |
|-------|------|--------|----|------|
| [#10177](https://github.com/BerriAI/litellm/issues/10177) | **[Feature]: Dark Mode**（UI暗黑模式） | 59 | 69 | OPEN |
| [#31555](https://github.com/BerriAI/litellm/issues/31555) | **[Feature]: Optional Markov-Based Routing Strategy**（基于马尔可夫的智能路由） | 9 | 0 | OPEN |
| [#25869](https://github.com/BerriAI/litellm/issues/25869) | **[Bug]: `stream_chunk_builder` corrupts Gemini tool calls**（流式拼接破坏Gemini工具调用） | 8 | 0 | OPEN |
| [#35076](https://github.com/BerriAI/litellm/issues/35076) | **[Bug]: skip_user_budget_on_team_key: true does not work**（团队密钥预算跳过失效） | 7 | 2 | CLOSED |
| [#16587](https://github.com/BerriAI/litellm/issues/16587) | **[Bug]: Redis: ssl=False forces SSLConnection**（Redis SSL配置反直觉） | 6 | 0 | OPEN |

**分析**：
- **暗黑模式**（#10177）以69个👍成为最受欢迎的功能请求，用户直言“going blind”，侧面反映当前UI对长时间运维人员的视觉负担。
- **智能路由**（#31555）提出马尔可夫决策过程的动态供应商选择，表明社区对成本优化和实时指标路由有更高阶需求。
- **流式兼容性**（#25869）暴露了Gemini模型在使用流式+工具调用时的严重数据损坏问题，直接影响生产使用。
- **预算行为**（#35076）虽然已关闭，但讨论显示用户对1.94.0版本变更感到困惑，且当时缺少迁移指南。

---

## 5. Bug 与稳定性

### 严重级别排列（P0为最严重）

| 严重度 | Issue | 摘要 | 状态 | 相关Fix PR |
|--------|-------|------|------|------------|
| **P0** | [#35255](https://github.com/BerriAI/litellm/issues/35255) | 配置定义策略在数据库连接后停止强制，且列表API不显示，管理面板完全不可见 | OPEN | [#35263](https://github.com/BerriAI/litellm/pull/35263) 已合并 |
| **P0** | [#35257](https://github.com/BerriAI/litellm/issues/35257) | `/v1/messages` 流式响应中 `post_call` 护栏被静默跳过，危险内容直通客户端，审计日志显示“success” | OPEN | [#35260](https://github.com/BerriAI/litellm/pull/35260) 已合并 |
| **P1** | [#33167](https://github.com/BerriAI/litellm/issues/33167) | v1.92.0起每次启动下载Prisma二进制，企业内网无互联网时启动失败，7个👍 | OPEN | 暂无 |
| **P1** | [#26192](https://github.com/BerriAI/litellm/issues/26192) | RDS IAM token刷新时 `PrismaWrapper.__getattr__` 同步阻塞30秒，导致Liveness探针失败 | OPEN | 暂无 |
| **P2** | [#16587](https://github.com/BerriAI/litellm/issues/16587) | `ssl=False` 被错误处理为强制SSL连接，破坏非TLS Redis配置 | OPEN | 暂无 |
| **P2** | [#35011](https://github.com/BerriAI/litellm/issues/35011) | 价格配置文件中 `claude-fable-5` 缓存最小token数与直接条目冲突，且499个模型缺少最小值 | OPEN | 暂无 |

**重点提醒**：  
- **护栏旁路**（#35257）属于安全类Bug，被合并的PR #35260已修复，建议升级至包含该修复的版本。  
- **Prisma二进制下载**（#33167）在离线环境/严格网络策略下是阻断性缺陷，项目组应优先处理。  
- **Redis SSL**（#16587）自2025年11月报告以来已8个月未修复，影响大量非TLS Redis用户。

---

## 6. 功能请求与路线图信号

### 高热度/可能纳入下个版本的功能

| Issue | 描述 | 社区热度 | 可能的PR/路线图 |
|-------|------|----------|-----------------|
| [#10177](https://github.com/BerriAI/litellm/issues/10177) | **暗黑模式** – UI增加深色主题 | 59评论，69👍 | 无对应PR，但人气极高，可能近期安排 |
| [#31555](https://github.com/BerriAI/litellm/issues/31555) | **马尔可夫路由策略** – 基于实时指标的供应商选择 | 9评论 | 暂无PR，属于高级路由功能 |
| [#33921](https://github.com/BerriAI/litellm/issues/33921) | **新增Kimi K3、Inkling、Tinker平台原生支持** | 3评论 | 暂无PR |
| [#35250](https://github.com/BerriAI/litellm/issues/35250) | **添加Gemini Robotics ER 2 Preview & ER 1.6 Preview 定价** | 1评论 | [#35287](https://github.com/BerriAI/litellm/pull/35287) 已合并 |
| [#34076](https://github.com/BerriAI/litellm/issues/34076) | **自定义UI登录认证函数 `custom_ui_auth`** | 2评论 | 无对应PR |
| [#35097](https://github.com/BerriAI/litellm/issues/35097) | **标签路由支持AND语义（`&tag`前缀）** | 3评论 | 无对应PR |
| [#35233](https://github.com/BerriAI/litellm/issues/35233) | **Claude Code marketplace端点增加严格鉴权** | 1评论 | 无对应PR |

**路线图判断**：  
- 此次发布版本重点在数据库运维、护栏扫描、预算控制等稳定性方向，未包含新功能。  
- 暗黑模式（#10177）用户呼声极大，但未见具体开发计划，建议项目组在下一个功能版本优先考虑。  
- 新模型支持（Gemini Robotics）已通过PR快速响应，体现了LiteLLM对大模型生态的跟进速度。

---

## 7. 用户反馈摘要

从今日活跃的Issues评论中提炼真实用户声音：

| 用户痛点 | 引用/场景 | 对应Issue |
|----------|-----------|-----------|
| **UI视觉疲劳** | “I'm going blind.” —— 长时间使用亮色背景管理面板的运维人员 | #10177 |
| **企业网络限制** | “In many corporate networks, egress is locked down.” —— 无法从互联网下载Prisma二进制，导致v1.92.0起无法启动 | #33167 |
| **预算配置困惑** | “The release notes say ‘set `general_settings.skip_user_budget_on_team_key: true`’ but it doesn't work.” —— 文档与行为不一致 | #35076 |
| **流式工具调用损坏** | “Follow-up turns fail with 400 Bad Request: 'Corrupted tool call context'.” —— Gemini流式模式下游任务中断 | #25869 |
| **缓存成本失真** | “OpenAI models do not price the cache-write portion of the request.” —— 缓存写入token未被计入成本，造成预算控制失效 | #33772 |
| **SSO用户管理混乱** | “SSO users cannot login because -7 (minus seven) spots are available.” —— SSO用户计数异常导致登录拒绝 | #31734 |
| **S3回调失效** | “Service must be in list - S3 callback does not work.” —— 标准配置下S3回调始终不工作 | #26770 |

**满意方面**：用户对社区响应速度（如暗黑模式高赞、Gemini Robotics模型价格快速添加）表示认可；部分已修复的Bug（如团队密钥预算问题）得到了积极反馈。但离离线环境支持、流式完整性等根本性痛点仍有距离。

---

## 8. 待处理积压

以下Issue/PR长时间未获维护者响应或进展缓慢，需重点关注：

| 编号 | 标题 | 创建日期 | 最后更新 | 备注 |
|------|------|----------|----------|------|
| [#16587](https://github.com/BerriAI/litellm/issues/16587) | Redis: ssl=False forces SSLConnection | 2025-11-13 | 2026-07-30 | 8个月未修复，严重影响非TLS Redis用户 |
| [#25869](https://github.com/BerriAI/litellm/issues/25869) | stream_chunk_builder corrupts Gemini tool calls | 2026-04-16 | 2026-07-30 | 流式工具调用数据损坏，无PR对应 |
| [#21023](https://github.com/BerriAI/litellm/issues/21023) | Inconsistent spend logging for custom model pricing | 2026-02-12 | 2026-07-30 | 自定义模型成本记录不一致，无PR对应 |
| [#16773](https://github.com/BerriAI/litellm/issues/16773) | Incorrect label count in increment_deployment_cooled_down | 2025-11-18 | 2026-07-30 | Prometheus监控指标无法工作，无PR对应 |
| [#26192](https://github.com/BerriAI/litellm/issues/26192) | PrismaWrapper.__getattr__ deadlocks event loop | 2026-04-21 | 2026-07-30 | RDS IAM认证用户生产环境风险 |
| [#33167](https://github.com/BerriAI/litellm/issues/33167) | v1.92.0 downloads Prisma Binaries at startup | 2026-07-14 | 2026-07-30 | 7个👍，企业用户阻塞性缺陷 |

**建议**：以上Issue均涉及核心功能或关键运维场景，建议项目维护者在下一迭代周期

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是为 Temporal 项目生成的 2026-07-31 项目动态日报。

---

### Temporal 项目动态日报 | 2026年07月31日

---

### 1. 今日速览

今日项目整体活跃度 **非常高**。过去24小时内，共有 **45 条 Pull Request** 在活动，其中 7 条被合并或关闭，显示出核心团队在持续推进多项功能和修复。然而，仍有 **38 条 PR 等待合并**，合并瓶颈较为显著。在稳定性方面，发现了一个关于 **数据竞争（Data Race）** 的严重 Bug (#11352)，目前尚无修复 PR 关联，需重点关注。此外，Nexus 操作和活动执行引擎（SAA）相关的多项 PR 更新频繁，表明这些是当前开发的重心。

### 2. 版本发布

无

### 3. 项目进展

今日没有大型版本发布，但 7 条合并/关闭的 PR 推进了多项关键改进：

- **依赖与基础设施更新**：`#11265` 已关闭，该 PR 更新了 `ringpop-go` 和 `tchannel-go` 依赖，修复了成员管理相关 Bug 并提升了 Go 版本兼容性。这是保障集群稳定性的重要维护工作。
- **调度器（Scheduler）修复**：`#11162` 已关闭，修复了在回填（backfill）操作中因容量限制导致跳过部分时间范围的问题，提升了调度器的可靠性。
- **代码清理与文档**：`#11340` 已关闭，修正了调度器取消/终止重试逻辑中的误导性注释，提高了代码的可读性和可维护性。

### 4. 社区热点

以下 PR 在过去 24 小时内获得了较多关注和评论，是社区讨论的热点：

- **`#11274 [Query-backed Nexus Operations]`**：该 PR 旨在支持以工作流查询（Query）作为 Nexus 操作的实现方式，是扩展 Nexus 功能集的关键步骤。讨论集中在该方案的设计和测试方法上。 (https://github.com/temporalio/temporal/pull/11274)
- **`#11276 [修复 UpdateSchedule 的 nil 指针解引用]`**：该 PR 修复了一个可能导致服务 Panic 但被错误恢复的 Bug。社区的讨论聚焦于该 Bug 对用户的实际影响以及修复的及时性。 (https://github.com/temporalio/temporal/pull/11276)
- **`#11345 [迁移 PollerPQ 到侵入式链表]`**：这是一个性能优化 PR，由于原优先级队列并未被充分利用，团队决定将其替换为更轻量的数据结构。讨论围绕该优化的性能基准测试结果展开。 (https://github.com/temporalio/temporal/pull/11345)

### 5. Bug 与稳定性

今日报告了一个关键稳定性问题，按严重程度排列如下：

- **严重**
  - **`#11352` （数据竞争）**：`ReaderImpl.AppendSlices` 方法存在未同步的 `r.slices.Back()` 读取操作，导致并发数据竞争。该问题可能引发数据损坏或不可预测的行为。**暂无关联的 Fix PR**，需要开发团队紧急评估。
    (https://github.com/temporalio/temporal/issues/11352)
- **高**
  - **`#11249` （nil Failure 处理不当）**：`RespondActivityTaskFailed` 请求中遗漏 `Failure` 时，SAA（Sync Activity，同步活动）错误地将其判定为不可重试。该 PR 已提出修复，旨在与 WFA（Workflow Activity，工作流活动）行为对齐。
    (https://github.com/temporalio/temporal/pull/11249)

### 6. 功能请求与路线图信号

- **CI/CD 平台扩展（`#6104`）**：用户请求将 CI 测试扩展到 Linux ARM、macOS 和 Windows 平台。这反映了社区对多平台支持的需求日益增长。虽然创建已有一段时间，但鉴于稳定性问题频发，扩大测试矩阵以覆盖更多架构是合理的下一步。
- **查询驱动的 Nexus 操作（`#11274`）**：该 PR 表明 Temporal 团队正致力于将所有 Temporal 原语（Primitives）作为 Nexus 操作暴露，这是其服务互联愿景的重要一步，预计会被纳入未来版本。
- **Worker 回调功能（`#11338` 和 `#11361`）**：多个 PR 指向一个名为 `feature/worker-callbacks` 的长期功能分支。该功能旨在实现工作流完成后回调外部系统（CHASM 和 SANO），是增强系统集成能力的关键信号。

### 7. 用户反馈摘要

尽管今日无大量用户评论，但从 Issue 和 PR 的描述中可提炼出以下用户反馈信号：

- **对多平台支持的需求**：`#6104` 表明用户希望在非 Linux x64 平台上也能获得官方测试保障，这关系到开发者在本地 macOS 或 Windows 环境下的开发体验。
- **对行为一致性的关注**：`#11249` 的修复反映了开发者对 SAA 和 WFA 两种活动执行模式行为一致性的高要求，任何细微差异都可能成为用户的痛点。
- **对时间跳过功能稳定性的期望**：`#11220` 和 `#11259` 致力于增强时间跳跃（Time-Skipping）功能的可控性和可观测性。用户通过描述引入“最大跳过次数”等配置，表达了避免因无限重试导致测试时间过长的强烈需求。

### 8. 待处理积压

- **`#6104`（CI 平台扩展）**：创建于 2024 年 6 月，至今已超过两年。尽管只有 1 条评论，但这是一个涉及开发者体验和项目长期健康的持续需求，建议维护者考虑排期。
    (https://github.com/temporalio/temporal/issues/6104)
- **长期未合并的 PR**：如 `#11169`（7月21日创建）、`#11220`（7月22日创建）等多条 PR 已超一周未合并，考虑到项目目前有 38 条待合并 PR，可能存在 Code Review 或 CI 资源瓶颈。维护者应关注此类 PR 的积压情况。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*