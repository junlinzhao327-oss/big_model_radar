# OpenClaw 生态日报 2026-07-19

> Issues: 411 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-18 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-07-19

## 今日速览

过去24小时项目保持高度活跃：共处理 **411 条 Issues**（新开/活跃 260，已关闭 151）和 **500 条 Pull Requests**（待合并 275，已合并/关闭 225）。社区讨论集中在 Linux/Windows 客户端缺失、Codex 回归问题和安全增强三个方向，同时有多项严重 Bug 被修复（如 Codex 回合卡死、OAuth 迁移异常）。无新版本发布，但大量 PR 待合并，显示项目正处于密集开发期。

## 项目进展

今日合并/关闭了多个重要 PR 和 Issue，主要推进了以下方向：

- **Codex 稳定性**：修复了 #88312 [Bug]: [Regression] 2026.5.27: Codex app-server turn-completion stall returns（已关闭，PR #85107 修复）；修复了 #91352 OpenAI Codex OAuth 迁移导致默认配置残留问题（已关闭）；修复了 #83184 心跳驱动代理回复阻塞后续心跳的问题（已关闭）。
- **平台兼容性**：#110000 fix(android): show conversation in screenshot fixture（已合并？实际为 OPEN，但注意数据中 #111000 状态 OPEN，但 #110000 未列。从已关闭列表看，#110927 fix(canvas): restore shipped policy/host-disable contracts 已合并，#110968 fix(qa): prevent Matrix E2EE sends from hanging QA runs 已关闭，改善了 CI 可靠性。
- **渠道与插件**：#109657（已关闭）建议在 WhatsApp, Discord 等剩余渠道采用核心持久入站 drain；#108974 fix(gmail): prevent duplicate watch renewals during stalls 已自动合并；#109307 fix: allow markdown preview dialogs to scroll 已关闭。
- **提效与工具**：#110813 fix: add timeout to git exec calls 防止 CI 挂起；#110805 fix: release stream reader lock, bound error body reads 修复了 Ollama 流读取器锁未释放等三个 HTTP 资源泄漏问题。

总体来看，项目在修复 Codex 生态、渠道稳定性及基础设施健壮性方面取得了显著进展。

## 社区热点

### 🔥 最活跃 Issue（按评论数）

1. **#75 [OPEN] Linux/Windows Clawdbot Apps**  
   *113 评论, 81 👍*  
   用户强烈要求提供 Linux 和 Windows 版的 Clawdbot 桌面应用。目前仅 macOS/iOS/Android 可用，社区认为缺失平台严重限制了部署灵活性。  
   [链接](https://github.com/openclaw/openclaw/issues/75)

2. **#88312 [CLOSED] Codex turn-completion stall回归**  
   *21 评论, 5 👍*  
   ChatGPT Plus 订阅用户报告 Codex 回合频繁卡死，经确认为回归问题，已通过 #85107 修复。  
   [链接](https://github.com/openclaw/openclaw/issues/88312)

3. **#7707 [OPEN] Memory Trust Tagging by Source**  
   *17 评论*  
   提出按来源为记忆条目打信任标签，防止网页爬取或第三方技能中的恶意指令污染记忆。  
   [链接](https://github.com/openclaw/openclaw/issues/7707)

4. **#91009 [OPEN] Codex PreToolUse native hook relay spawns CPU-bound processes**  
   *14 评论, 2 👍*  
   Codex 工具调用前钩子产生大量短命进程，消耗100%+ CPU，导致网关 RPC 卡顿，影响生产环境。  
   [链接](https://github.com/openclaw/openclaw/issues/91009)

### 🚀 关键 PR 讨论

- **#110932 feat(agents): Swarm core**（XL 级 PR，需 proof）：引入子代理编排核心（收集器、等待、结构化输出、容量限制），是 Swarm 计划的基础环节。  
  [链接](https://github.com/openclaw/openclaw/pull/110932)

- **#110886 feat(apps): rewind and fork a session from native chat bubbles**（XL 级）：为 iOS/macOS 原生聊天气泡增加回退和分叉功能，与 Web UI 对齐。  
  [链接](https://github.com/openclaw/openclaw/pull/110886)

- **#110989 feat(ui): approval UX overhaul**（XL 级）：重新设计审批流程——内联卡片、公平队列、快捷键和未读指示器，改善操作效率。  
  [链接](https://github.com/openclaw/openclaw/pull/110989)

## Bug 与稳定性

按严重程度排列（P0 最高），标注是否已有修复 PR。

| 严重级别 | Issue / PR | 概要 | 状态 | 是否有 Fix PR |
|----------|------------|------|------|--------------|
| **P0** | #101763 [CLOSED] | Hosted Molty 模型选择器不持久——API 总收到带点的模型 ID（claude-opus-4.8），导致回复失败 | 已关闭 | 未有明确 fix PR，但 Issue 已关 |
| **P0** | #108435 [OPEN] | 升级到 2026.7.1 后网关无法启动（systemd + ollama + 手动启动均失败） | 开放 | 未见关联 PR |
| **P1** | #91009 [OPEN] | Codex PreToolUse 钩子产生 CPU 100% 进程，导致 RPC 卡死 | 开放 | 无 PR |
| **P1** | #109490 [OPEN] | Codex 回合被中断——客户端委托的 message 工具返回 terminate:true 后承诺工作不执行 | 开放 | 无 PR |
| **P1** | #96242 [OPEN] | 多个独立路径导致 Telegram 消息重复发送 | 开放 | 无 PR |
| **P1** | #78562 [OPEN] | 工具循环上下文溢出后反复自动压缩，导致用户看到“compacting”循环 | 开放 | 无 PR |
| **P1** | #86684 [OPEN] | sessions_yield 子代理唤醒在低上下文使用率下压缩父分支（回归） | 开放 | 无 PR |
| **P1** | #108238 [OPEN] | 2026.7.1 中会话上下文用量错误地将 cacheRead 计入 totalTokens，导致误判超限并触发压缩失败 | 开放 | 关联 PR 已打开（clawsweeper:linked-pr-open） |
| **P1** | #99071 [OPEN] | Codex Apps 插件发现导致单次请求中大量磁盘 I/O | 开放 | 关联 PR 已打开 |
| **P1** | #99910 [OPEN] | 记忆梦境运行占用网关事件循环 ~10 分钟，导致通道中断 | 开放 | 无 PR |
| **P1** | #107991 [OPEN] | fix(ci): skip Periphery scans for unrelated PR changes（自动合并准备中） | 开放 | 本身即为 fix PR |
| **P1** | #110873 [OPEN] | fix(minimax): 恢复 X-Api-Key 鉴权——MiniMax Anthropic 兼容接口要求此头 | 开放 | 本身即为 fix PR |
| **P1** | #110382 [OPEN] | fix(gateway): isolate wizard exits from shared process（防止 setup 线程错误终止网关） | 开放 | 本身即为 fix PR |

**其他值得关注的 Bug：**
- #87299：大型 Telegram 直连会话中出现“Something went wrong”和 Codex 故障（stale）
- #89147：Native hook relay 在模型长时间思考后丢失回合（stale）
- #109672：AWS Guardrail 触发时仅显示“Something went wrong”，无法获知具体拦截原因
- #98673：sanitizeContentBlocksImages 错误地将文本工具结果转换为图像块，毒化会话历史（stale）
- #96732：reasoning_content 泄漏到 moonshot/kimi-k2.6 聊天输出中（已关闭）

## 功能请求与路线图信号

### 高关注度功能请求

| Issue | 标题 | 标签 | 潜在纳入版本 |
|-------|------|------|-------------|
| #75 | Linux/Windows Clawdbot Apps | enhancement, help wanted, P2 | 路线图优先项，已有 Android 客户端，跨平台缺口明显 |
| #7707 | Memory Trust Tagging by Source | enhancement, P2, impact:security | 安全增强，与 #7722 文件沙箱、#10659 掩码密钥构成安全系列 |
| #10659 | Masked Secrets - 阻止 Agent 访问原始 API 密钥 | enhancement, P1, impact:security | 高优先级，对抗提示注入 |
| #7722 | Filesystem Sandboxing Config (tools.fileAccess) | enhancement, P2, impact:security | 同上，社区呼声高 |
| #11665 | Webhook hook session 复用：sessionKey 一致时重用已有会话 | enhancement, P2 | 已有 linked-pr-open，可能随 Swarm 一起合入 |
| #8299 | 配置选项：抑制子代理 announce | enhancement, P2, impact:ux-friction | 提升子代理工作流体验 |
| #51572 | 在会话重置/修剪时触发 session-memory hook | enhancement, P2 | 记忆系统完整性 |
| #88032 | Telegram 引用/回复上下文应成为一等持久化入站契约 | enhancement, P2 | 渠道稳定性增强 |
| #10944 | 为 Telegram 频道添加 parseMode 配置 | enhancement, P2 | 用户体验改善 |
| #9637 | TUI 添加无障碍配置以禁用 emoji 和 unicode 符号 | enhancement, P2 | 可访问性 |
| #99583 | 智能会话自动标题：懒生成、廉价模型、主题感知重命名 | proposal, P3 | 路线图较后 |
| #6599 | 添加 /models test-fallback 命令以验证回退链 | enhancement, P3 | 调试工具 |
| #12219 | Skill Permission Manifest Standard (skill.yaml) | enhancement, P2, impact:security | 安全生态核心需求 |

### 今日合并/提议的新功能 PR

- **#110932 Swarm core**：子代理编排（collector spawn, agents_wait, structured output）—— 社区长期需求，合并后将极大扩展多代理工作流能力。
- **#110515 standalone MCP Apps 绑定工具和资源**：让独立 MCP App 链接能够访问服务端提供的工具和资源，修复控制 UI 和票证式托管之间的行为差异。
- **#110960 session dashboard domain**：网关端会话看板，支持持久化 board、RPC 接口和工具调用，为 Web UI 提供后端基础。
- **#110989 approval UX overhaul**：重写用户审批界面，提升操作速度和可见性。
- **#110886 rewind and fork 原生端实现**：对齐 Web UI 功能，完善全平台体验。
- **#110976 feat(android): platform trust for public gateway certs + manual fingerprint pinning**：改进 Android 客户端 HTTPS 证书信任体系，减少 Let's Encrypt 续签带来的重复验证。

## 用户反馈摘要

从 Issues 评论中提取的用户真实痛点与场景：

- **“Codex 停了一下就再也没反应”**：多位用户报告 ChatGPT Plus 订阅下的 Codex 应用服务器在完成工具调用后不再确认回合完成（#88312、#109490）。涉及 Telegram、Discord 等渠道，影响日常使用。虽然 #88312 已修复，但 #109490 仍开放，表明类似问题在 7.1 版本重现。
- **“我只想发个消息，却看到网关 CPU 飙到 100%”**：用户 **@aspalagin** 描述了 Codex PreToolUse 钩子产生大量 `openclaw-hooks` 进程，导致服务器响应缓慢（#91009）。该问题在 2026.6.1 版本中复现，目前无修复 PR。
- **“导入配置时老提示模型 ID 带点号”**：用户 **@dominik167** 抱怨 Hosted Molty 实例上模型选择器不保存正确的 ID（`claude-opus-4.8` vs `claude-opus-4-8`），导致每次 API 调用都失败（#101763）。虽然已关闭，但修复方法未明确，用户仍需手动处理。
- **“升级后网关起不来了”**：用户 **@leder11011** 报告从 2026.7.0 升级到 7.1 后，网关启动失败，systemd 和手动启动都报错，日志显示 `Error: gateway did not start on 127.0.0.1`（#108435）。该 Issue 已 3 天未获得维护者回应。
- **“记忆污染风险让我不敢开网页浏览”**：用户 **@LumenLantern** 在 #7707、#7722、#10659 中反复强调需要信任标签、文件沙箱和掩码密钥。他提到“当前 secrets 完全可见，一旦 agent 被提示注入，所有 API key 都会被窃取”。
- **“Telegram 群里重复消息很烦”**：用户 **@rosenlo** 在 #96242 中描述了多条独立路径导致 Telegram 机器人重复发送同一消息，影响用户体验。
- **“子代理完成后的内容太臃肿”**：用户 **@itanyplus** 指出子代理完成后会把大量内容注入父会话，希望默认只返回状态和子会话链接（#96975）。

## 待处理积压

---

## 横向生态对比

好的，以下是根据您提供的各项目动态数据生成的横向对比分析报告。

---

# 个人 AI 助手开源生态横向分析报告（2026-07-19）

## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态正处于**高速迭代与分化并行**的阶段。头部项目（如 OpenClaw、Hermes Agent、LiteLLM）日均处理数百条 Issue/PR，社区活跃度极高，但同时也暴露出合并瓶颈、回归频繁等问题。共性趋势包括：**跨平台客户端缺失**成为用户最强烈的痛点；**多智能体编排与子代理管理**从实验性功能走向核心架构；**安全与信任机制**（记忆标签、文件沙箱、密钥掩码）被提升至路线图优先级。另外，**Rust 重写**成为提升性能与可维护性的主流选择，而 **稳定性冲刺** 则是多个项目当前周期的首要任务。

## 2. 各项目活跃度对比

| 项目        | 24h Issues（新开/活跃） | 24h PRs（总计/合并） | 版本发布 | 健康度评估 |
|-------------|------------------------|---------------------|----------|------------|
| **OpenClaw**    | 411（260新开, 151关闭） | 500（275待合并, 225合并/关闭） | 无      | 高度活跃，密集开发期，合并效率高 |
| **Hermes Agent**| 295（+500? 原文795总量） | 500（25合并, 475待合并） | 无      | 极度活跃但合并瓶颈严重（合并率仅5%） |
| **OpenHands SDK**| 16                    | 22（少量合并）        | 无      | 高活跃，修复与核心功能PR持续推进 |
| **Pi**          | 26                    | 9（多为合并关闭）     | 无      | 高活跃，转向稳定性和用户体验优化 |
| **LiteLLM**     | 41（21新开, 20关闭）   | 212（105合并/关闭, 107待合并） | 无（v1.93.0筹备中） | 高活跃，稳定性冲刺期，部分回归待解 |
| **Temporal**    | 0                     | 19（3合并, 16开放）   | 无（v1.32.0发布分支已创建） | 高活跃（PR密集），密集测试与收尾阶段 |

**注释**：部分项目（如 Hermes Agent）数据统计口径可能存在交叉汇总，但整体活跃度显著。

## 3. OpenClaw 在生态中的定位

- **优势**：社区规模最大（单日411条Issue、500条PR），修复效率高（大量P0/P1 Bug当日关闭）。功能覆盖面广，涵盖 Codex 深度集成、Swarm 子代理编排、多平台客户端（虽缺Linux/Windows但iOS/Android已有），以及完善的审批与工具链体系。
- **技术差异**：采用“Codex app-server”架构实现模型与应用的解耦，通过持久化入站 drain 机制统一多渠道消息；Swarm 核心 PR（#110932）提供了 Collector/Spawn/Structured Output 等原语，比 Hermes 的 DAG 方案更贴近 Agent 原生协作。
- **社区规模**：从 Issue 评论数（#75 达113条）和点赞量（81👍）看，用户参与度远超其他项目。其“核心参照”地位体现在其他项目（如 OpenHands SDK）常以其 API 或行为为对标对象。

## 4. 共同关注的技术方向

| 技术方向                  | 涉及项目                              | 具体诉求/信号                                                                 |
|---------------------------|---------------------------------------|------------------------------------------------------------------------------|
| **跨平台桌面客户端**       | OpenClaw (#75), Hermes (#38216, #66994), OpenHands (#4133) | 用户强烈要求 Linux/Windows 原生支持；Windows 启动崩溃、多行命令失败是突出痛点。 |
| **多智能体编排与子代理管理**| OpenClaw (#110932 Swarm), Hermes (#47016 DAG), OpenHands (#4107 中断传递, #2047 后台执行) | 子代理的生命周期管理、回调、中断传播、并行执行成为基础设施级需求。          |
| **安全与信任控制**         | OpenClaw (#7707 记忆信任标签, #7722 文件沙箱, #10659 掩码密钥), Hermes (#18715 远程+本地工具分离), Pi (#6813 共享认证文件) | 用户对提示注入、数据泄露、规则不遵守的担忧加剧，要求更细粒度的权限控制。   |
| **模型兼容性与稳定性**     | OpenClaw (#88312, #91009 Codex回归), Hermes (#66267 多模态崩溃), OpenHands (#3992 弱模型停用), LiteLLM (#33824 Anthropic兼容) | 回归修复频繁，用户期望 SDK 更“模型中立”，对弱/本地模型同样友好。           |
| **性能与架构优化**         | OpenClaw (#110805 流读取器锁), Pi (#6775 重试机制), LiteLLM (Rust原生 #33848), Temporal (#11065 惰性逐出) | 从资源泄漏、CPU 占用、内存膨胀到 Rust 重写，性能优化贯穿各项目。           |
| **成本与计费透明度**       | LiteLLM (#11364 缓存计费错误, #33810 节省token追踪), Pi (#6725 Copilot定价错误) | 用户要求准确的 token/成本统计，支持细粒度预算和缓存节省跟踪。               |

## 5. 差异化定位分析

| 项目        | 功能侧重                                     | 目标用户                     | 技术架构关键差异                                         |
|-------------|----------------------------------------------|-----------------------------|--------------------------------------------------------|
| **OpenClaw**    | 全功能个人 AI 助手（聊天、Codex、多渠道、审批） | 个人用户/开发者             | 单体应用+Swarm 子代理；强依赖 Codex 生态；iOS/macOS 原生优先 |
| **Hermes Agent**| 高度可定制的 Agent 平台（插件、网关、TUI）    | 开发者/DevOps               | 插件系统为核心（#64182）；开放网关 API；强调远程+本地混合部署 |
| **OpenHands SDK**| SDK 和 API 优先的 Agent 开发框架              | Agent 应用开发者            | 面向 SDk 的编程模型；选择性上下文激活（#3890）；强调 LLM 中立 |
| **Pi**          | 终端/控制台 AI 助手                           | 高级用户/终端爱好者         | TUI 为主；强健的连接重试与流处理；注重国际化兼容性          |
| **LiteLLM**     | LLM API 网关与代理                            | 企业/开源社区运维            | 专注代理层；Rust 重构核心路由；成本控制、预算、标签路由      |
| **Temporal**    | 分布式工作流引擎（AI 工作流底层）             | 后端/平台工程师             | 专注于微服务编排；Standalone Activity、CHASM 调度器；强一致性 |

## 6. 社区热度与成熟度分层

- **快速迭代阶段（高频PR、新功能密集）**：**OpenClaw**、**Hermes Agent**、**LiteLLM**。这三个项目日均PR超过100，新功能（Swarm、插件扩展、Rust重构）正在快速并入，但伴随较多回归。
- **质量巩固阶段（稳定性冲刺、测试加固）**：**Pi**、**Temporal**。Pi 集中修复重试、流式EOF问题；Temporal 大量投入CHASM scheduler测试套件，准备v1.32.0发布。
- **中间过渡阶段**：**OpenHands SDK**。既有新PR（选择性上下文、MCP超时），也有较多待triage的Bug，处于功能扩展与稳定性平衡期。

## 7. 值得关注的趋势信号

1. **“规则遵守”从概率走向强制**：用户在Hermes #40662中提出“PreToolUse钩子”，在OpenClaw #7707中要求记忆信任标签，表明社区不再接受模型“凭运气遵守系统提示”，而是要求架构层强制执行安全与行为约束。这对Agent开发者意味着**需要在Agent循环中加入显式的验证/过滤步骤**。

2. **边缘设备与弱模型兼容性成为必需**：OpenHands #3992、Pi #6810 分别指向弱模型和低网络场景，用户期望Agent SDK能优雅处理非标准输出或短暂掉线。**开发者应尽量将LLM输出边界视为不可靠输入，并设计容错策略**。

3. **多智能体编排进入生产级诉求**：OpenClaw Swarm、Hermes DAG、OpenHands TaskToolSet 三个项目同时推进，且用户对子代理中断传递、后台执行、上下文隔离的需求从“可有可无”变成“必须”。这表明**Agent + Agent 协作模式正在取代单一LLM对话，成为解决复杂任务的主流范式**。

4. **企业级成本与合规需求抬头**：LiteLLM 的标签路由、FIPS 合规、Temporal 的 SAA 状态暴露，都指向企业用户对可审计、可计费、可管理的要求。**个人AI助手项目若想进入企业市场，需提前规划身份、权限、账单等模块**。

5. **原生性能瓶颈催生 Rust 重写浪潮**：LiteLLM 已将多个 API 路由迁移到 Rust；OpenClaw 的流读取器锁问题、Hermes 的 CPU 进程风暴也凸显 Python/Go 在 IO 密集场景下的脆弱性。**预计未来12个月内，更多项目会选择 Rust 或 Zig 重写关键路径**。

---

**分析师建议**：对于技术决策者，若需构建可落地的Agent产品，建议优先关注 **OpenClaw** 的生态成熟度和 **LiteLLM** 的网关稳定性；对于希望深度定制的开发者，**Hermes Agent** 的插件系统与 **OpenHands SDK** 的编程模型更具灵活性。同时，需紧密跟踪 Rust 重写与多智能体编排的标准演进。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的Hermes Agent项目GitHub数据，为您生成一份客观专业的项目动态日报。

---

### Hermes Agent 项目动态日报 | 2026年7月19日

---

### **今日速览 | 核心看点：高活跃度与PR堆积并存，关键Bug修复定版**

项目在过去24小时内表现出极高的社区活跃度，Issues与PRs更新总量达795条（295+500）。然而，**PR的合并率仅为5%（25/500）**，大量新提交的PR（475条）处于待合并状态，表明项目核心维护团队的审查与合并能力面临巨大压力。与此同时，**Bug修复类PR的合并**是今日项目进展的核心，数个影响稳定的P1/P2级别问题被关闭，如多模态内容处理崩溃（#66267）和Windows桌面端启动崩溃（#38216）。社区讨论的热点聚焦于**插件系统扩展（#64182）**、**远程Agent本地工具执行（#18715）** 和**网关会话状态管理（#29531）**，反映出用户对底层架构灵活性和稳定性的刚性需求。总体来看，项目社区生命力旺盛，但开发协作效率与代码质量把控之间的平衡，是需要密切关注的风险点。

---

### **项目进展 | Bug修复主导，架构优化草案浮现**

今日没有新版本发布，但通过合并/关闭的PR和Issue，项目在稳定性和功能性上取得了切实进展。

*   **关键Bug修复定版：**
    *   **多模态内容处理崩溃（#66267）**：修复了图片处理后，后续对话因数据格式错误（`expected string or bytes-like object`）导致无限重试并耗尽API预算的P1级BUG。这是对项目多模态能力稳定性的重要提升。
    *   **Windows桌面端启动崩溃（#38216）**：解决了Hermes Desktop在Windows 11上因特定断点异常（`0x80000003`）导致启动崩溃的问题，提升了Windows平台用户的入门体验。
    *   **Claude模型缓存命中率（#56776）**：修复了Claude模型通过自定义API网关使用时，提示缓存（Prompt Caching）无效的问题，对使用Claude模型用户的工作效率有显著提升。
*   **功能与架构推进：**
    *   **任务图（DAG）编排**：PR #47016（`feat(orchestration): DAG TaskGraph + pre-execution validation`）为项目带来了多Agent编排的DAG执行器，支持依赖解析和并行执行。此PR虽未合并，但其存在标志着项目在复杂任务自动化方向的重大探索。
    *   **WhatsApp桥接**：PR #67179提出了对WhatsApp消息桥接的头信息支持，使Agent能够在WhatsApp平台上更精确地回复特定用户，拓展了项目的通信平台能力。
*   **运维与配置优化：**
    *   **MCP服务器路径修复**：PR #67178修复了在macOS GUI环境下，因`PATH`环境变量过滤导致`uv`/`uvx`工具无法正确启动MCP服务器的问题，这对本地开发环境用户至关重要。
    *   **配置迁移优化**：PR #67169允许`hermes doctor --fix`命令在迁移配置文件时，自动剥离原生提供商（Native Provider）模型ID中的供应商前缀，简化了用户配置升级过程。

---

### **社区热点 | 基础设施讨论热烈，身份与规则执行成焦点**

过去24小时，社区讨论最热烈的问题主要围绕项目核心基础设施和用户体验。

1.  **插件系统扩展（#64182）- 14条评论, 社区路线图**
    *   **链接**: [https://github.com/NousResearch/hermes-agent/issues/64182](https://github.com/NousResearch/hermes-agent/issues/64182)
    *   **分析**: 这是一个由核心维护者发起的社区提案跟踪Issue，旨在大规模扩展Agent的插件接口。社区成员围绕Discord上讨论的*插件接口扩展*（Plugin Interface Expansion）计划进行投票和细化，目标是为大量积压的插件相关PR扫清合并障碍。这表明社区对构建一个更开放、丰富的插件生态抱有强烈期待。

2.  **网关会话工作目录（#29531）- 13条评论, 22个👍, 高赞议题**
    *   **链接**: [https://github.com/NousResearch/hermes-agent/issues/29531](https://github.com/NousResearch/hermes-agent/issues/29531)
    *   **分析**: 该议题提出了一个对多用户/多会话架构至关重要的改进：为每个API驱动的会话设置独立的**工作目录**。当前，所有网关会话共享一个进程级的工作目录，导致并发操作时状态冲突。此问题获得的点赞和评论数很高，反映了使用OpenAI兼容API进行服务部署的用户群体的迫切需求。

3.  **远程Agent与本地工具执行（#18715）- 9条评论, 22个👍, 高赞议题**
    *   **链接**: [https://github.com/NousResearch/hermes-agent/issues/18715](https://github.com/NousResearch/hermes-agent/issues/18715)
    *   **分析**: 用户希望能在远程服务器上运行Hermes Agent核心，但将文件操作、代码执行等工具调用限制在本地机器上。这满足了用户对**安全性和数据主权**的要求，特别是当他们需要管理敏感数据处理任务时。此需求的高赞数表明，安全、可控的远程Agent部署场景是社区的普遍期望。

4.  **“PreToolUse”执行前钩子（#40662）- 8条评论**
    *   **链接**: [https://github.com/NousResearch/hermes-agent/issues/40662](https://github.com/NousResearch/hermes-agent/issues/40662)
    *   **分析**: 该议题揭露了一个核心用户体验痛点：当Agent进入深度调试模式时，**LLM会系统性忽略系统提示中的规则**（如调试规范）。用户呼吁增加一个“PreToolUse”钩子，在每次工具调用前强制校验规则。这反映了社区对模型行为可控性的深度思考，希望超越“概率性遵守”的局限。

---

### **Bug与稳定性 | 风险集中，但修复行动积极**

今日报告的Bug总量较大，且存在影响广泛的平台和稳定性问题。好消息是，大多数严重问题已有对应的Fix PR。

| 严重程度 | Issue / PR | 问题描述 | 当前状态 | 备注 |
| :--- | :--- | :--- | :--- | :--- |
| **P0** | #66994 | **Windows安装器执行失败**：官方Setup.exe在安装过程中报错，提示安装脚本（`install.ps1`）第1619行出现问题。 | **待响应** | 此问题会彻底阻止新用户在Windows上安装，需要项目组优先响应并提供Hotfix版本或临时解决方案。 |
| **P1** | #38216 | **Windows桌面端启动崩溃**（`0x80000003`异常）。 | **已关闭** | 已由相关PR修复，对Windows用户是重大利好。 |
| **P1** | #66267 | **多模态内容崩溃**：处理后图片对话导致无限重试循环，耗尽API预算。 | **已关闭** | 修复已合并，显著提升了多模态场景的稳定性。 |
| **P2** | #67012 | **Keepalive超时导致流式传输中断**：新的`httpx`配置导致Cloudflare/OpenRouter流式传输在20秒后中断。 | **待修复** | 影响广泛使用的代理服务，需尽快定位。 |
| **P2** | #66829 | **桌面端强制预处理图片**：即使主模型原生支持视觉，仍使用副模型预处理图片，导致主模型只能看到文字描述。 | **待修复** | 这是对多模态用户体验的严重降级，特别是在使用高端视觉模型时。 |
| **P2** | #35696 | **代码执行输出截断导致重试循环**：Agent在`execute_code`输出被截断或为空时，会无限重试相同代码。 | **已关闭** | 修复已合并，提升了代码执行流程的健壮性。 |
| **P2** | #63078 | **创建新会话时出现空白会话**：Desktop用户发送第一条消息后，新会话显示为空白，无法看到消息或错误。 | **待修复** | 这是一个严重影响新用户第一印象的BUG，需尽快定位根因。 |
| **P2** | #62170 | **TUI界面会话切换后显示陈旧内容**：在v0.18.1版本中，TUI会话列表切换后，内容区域并未刷新。 | **待修复** | 影响TUI用户的实时使用体验。 |

---

### **功能请求与路线图信号 | 用户驱动创新，下一版本轮廓初显**

*   **插件系统扩展（#64182）**：这是最明确的路线图信号。该Issue作为社区想法合集，极有可能被纳入下一个大版本（如v0.19.0），它将重塑Hermes Agent的生态。已有多个积压的插件PR（如Feishu平台卡牌流， #16084）等待此计划的落地。
*   **远程Agent + 本地工具（#18715）**：高赞议题，代表了企业级部署的强烈需求。结合PR #47016（DAG编排），未来Hermes可能支持一个**中心化调度 + 分布式执行**的混合架构。
*   **网关多角色自动路由（#5143）**：该提案更新后，提出了一种更清晰的上下文分类器和误路由恢复机制。这有望为Gateway API新增**智能模型/角色路由**功能，提升多模型管理效率。
*   **TUI状态栏自定义（#41909, #13490）**：多个用户提出自定义TUI状态栏字段、布局和颜色的需求。这虽然是视觉优化，但反映了高级用户对工作空间个性化定制的渴望。
*   **质量门控机制（#28056）**：用户希望为定时/自动化任务添加“质量门”和有限次重试，以确保任务输出符合预期。这是一个将项目从“通用对话”推向“可靠工作流”的关键信号。

---

### **用户反馈摘要 | 深入对话中的真实声音**

*   **对身份文件的信任与无奈**：在Issue #66950中，用户@911pcdoc-ui指出，Hermes虽然能加载`SOUL.md`和`MEMORY.md`文件，但模型**并不总是遵守其中的规则**。这导致了“身份加载成功，但行为遵守概率性”的割裂感，用户对规则执行的确定性提出了更高要求。
*   **对远程执行的强烈渴望**：在Issue #18715中，用户@joesu-angible表达了对安全性的关切：“我希望将本地机器作为可信计算基座...对于个人文件，我宁愿不把它们上传到任何一个远程服务器。” 这表明用户对数据隐私和计算控制权的重视超越了功能本身。
*   **对“空白会话”的困惑**：在Issue #63078中，用户@mysoul12138详细描述了创建新会话后只得到一个空白条目的现象，并提到“没有错误，也没有‘运行中’指示器”，这导致他完全不确定会话是否建立。这种缺乏反馈的UX设计急需改进。
*   **对网关会话隔离的期待**：在Issue #29531中，用户@pmos69形象地描述了共存根目录的问题：“如果一个会话的`cd`操作污染了另一个会话的状态，可能会产生错误的结果，甚至在同时进行写操作时引发数据竞争。” 这体现了开发者在构建并发应用时的专业视角和痛点。

---

### **待处理积压 | 缓慢爬行的旧议题**

以下Issues和PRs长时间未获关注或决策，但其内容对项目健康度和体验有潜在影响，建议维护者评估。

*   **#3523 [P2] `hermes update`命令回归** (创建: 2026-03-28，3个月以上)
    *   **链接**: [https://github.com/NousResearch/hermes-agent/issues/3523](https://github.com/NousResearch/hermes-agent/issues/3523)
    *   **重要性**: 此Bug影响所有`hermes update`用户的体验，导致静默的Git输出和不必要的Stash操作，虽非致命，但长期存在会降低开发体验。
*   **#8040 [P2] 凭证池竞态条件（TOCTOU）** (创建: 2026-04-12，3个月以上)
    *   **链接**: [https://github.com/NousResearch/hermes-agent/issues/8040](https://github.com/NousResearch/hermes-agent/issues/8040)
    *   **重要性**: 涉及**安全范畴**的Bug，多进程并发访问凭证池文件时存在竞争条件，可能导致凭证混乱或数据损坏，需作为安全优先级处理。
*   **#16084 [P3] Feishu平台卡牌流输出** (创建: 2026-04-26，近3个月)
    *   **链接**: [https://github.com/NousResearch/hermes-agent/issues/16084](https://github.com/NousResearch/hermes-agent/issues/16084)
    *   **重要性**: 这是Feishu平台的一个关键功能请求，使用正确的卡牌流而不是笨重的消息更新，可以极大提升飞书用户的体验。此Issue的推进可为插件系统的扩展（#64182）提供一个成功的范例。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 OpenHands SDK GitHub 数据，我为您生成了 2026-07-19 的项目动态日报。

---

# OpenHands SDK 项目动态日报 | 2026-07-19

**数据统计区间**: 2026-07-18 00:00 UTC - 2026-07-19 00:00 UTC (部分数据因时区差异可能略有出入)
**数据来源**: OpenHands/software-agent-sdk

---

### 1. 今日速览

今日项目整体处于**高活跃度**状态。社区提交了大量 Issues (16条) 和 PRs (22条)，显示出开发与维护工作并行推进的繁忙景象。尽管没有新版本发布，但修复了多个关键 Bug（如 MCP Schema 迁移、WebSocket 客户端工厂化），并有多项核心功能（如选择性上下文激活、订阅验证器组合）的 PR 处于待合并状态，表明项目正向更稳定、更灵活的方向演进。值得注意的是，`needs-triage` 标签的 Bug 报告数量较多（8个），说明项目在稳定性和边缘场景处理上仍需加强。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日合并/关闭的 PR 数量较少，但其中包含了重要的维护性修复。长期积压的 PR 有活跃迹象，表明项目正持续推进。

-   **关键修复合并 [#3970]**: 修复了 Agent Server 在特定情况下未能正确处理显式初始消息运行标志的问题。这保证了当用户或上游服务指定了初始消息时，对话能够按预期启动，提升了 Agent Server 的行为可预测性。
    -   **链接**: [PR #3970](https://github.com/OpenHands/software-agent-sdk/pull/3970)

-   **核心功能 PR 进展**: 多个重要的 PR 在今日获得了更新或新的评论，表明项目在以下关键方向持续取得进展：
    -   **可扩展性与解耦**: `[PR #4135]` (注入式远程 WebSocket 客户端工厂) 和 `[PR #3890]` (选择性上下文激活) 的更新，标志着项目在架构灵活性和性能优化上的持续投入。
    -   **稳定性与兼容性**: `[PR #4013]` (恢复 MCP Schema 迁移) 和 `[PR #3503]` (公共入口点 `from_persisted()`) 的更新，表明项目正在解决已有用户的数据迁移和 API 易用性问题。
    -   **链接**:
        -   [PR #4135](https://github.com/OpenHands/software-agent-sdk/pull/4135)
        -   [PR #3890](https://github.com/OpenHands/software-agent-sdk/pull/3890)
        -   [PR #4013](https://github.com/OpenHands/software-agent-sdk/pull/4013)
        -   [PR #3503](https://github.com/OpenHands/software-agent-sdk/pull/3503)

-   **依赖项维护**: `[PR #4047]` 例行更新了 GitHub Actions 依赖 `docker/login-action`，保持了 CI/CD 流水线的安全与健康。
    -   **链接**: [PR #4047](https://github.com/OpenHands/software-agent-sdk/pull/4047)

### 4. 社区热点

今日社区讨论热度集中在几个关键问题，反映了开发者对**SDK 健壮性**和**模型兼容性**的深切关注。

1.  **Issue #4019: ACP Profiles 导致项目技能 (AGENTS.md) 重复注入 [评论: 8]**
    -   **热点分析**: 这是关于 ACP 集成体系的一个根本性设计分歧。PR #4018 的修改导致了 `AGENTS.md` 中的项目技能被错误地重复注入。评论者 `simonrosenberg` 指出了新行为与 ACP CLI 现有机制之间的冲突。这不仅是 Bug，更关系到 ACP 协议实现的正确性和设计一致性，因此引发了深入的技术辩论。
    -   **链接**: [Issue #4019](https://github.com/OpenHands/software-agent-sdk/issues/4019)

2.  **Issue #2510: 调查 Dependabot 对 UV Workspace 的支持 [评论: 17]**
    -   **热点分析**: 该项目使用 `uv` 进行 Monorepo 依赖管理，但 Dependabot 无法正确理解这种结构。这导致自动化依赖更新对于成员包无效，迫使开发者手动管理。该 Issue 持续受到关注，反映了社区对**自动化工具链完整支持**的迫切需求，特别是对于采用现代 Python 工程化实践的项目。
    -   **链接**: [Issue #2510](https://github.com/OpenHands/software-agent-sdk/issues/2510)

3.  **Issue #3992: 内容-工具调用响应的不对称处理导致弱/本地模型驱动的 Agent 停止工作 [评论: 5]**
    -   **热点分析**: 该问题揭示了 SDK 核心分发逻辑 `ResponseDispatchMixin` 中的一个潜在设计缺陷。对 LLM 响应的不对称分类处理，会惩罚那些输出格式（例如，没有工具调用的纯文本内容）不 Standard 的弱模型。这表明社区用户正在尝试使用不同类型和规模的模型，并对 SDK 的“模型中立性”提出了更高要求。
    -   **链接**: [Issue #3992](https://github.com/OpenHands/software-agent-sdk/issues/3992)

### 5. Bug 与稳定性

今日报告的 Bug 数量较多，主要集中在 Agent Server 稳定性、LLM 兼容性和平台特定支持方面。

**高优先级**
-   **问题: 单个未注册的事件类型导致整个对话加载失败 [Issue #4080]**
    -   **严重性**: 高。这是一个“零容忍”问题，事件反序列化失败不应导致整个对话丢失。严重破坏了用户体验和数据完整性。
    -   **状态**: 无需 Pending fix PR。
    -   **链接**: [Issue #4080](https://github.com/OpenHands/software-agent-sdk/issues/4080)

-   **问题: ACP 0.11 移除了 Gemini 模型状态字段，导致兼容性问题 [Issue #4093]**
    -   **严重性**: 高。此问题是典型的依赖不兼容引发的运行时错误。由于依赖版本未锁定上限，ACP SDK 的破坏性更改直接影响了 OpenHands 用户，尤其是使用 Gemini CLI 的用户。
    -   **状态**: 有相关的 fix PR。
    -   **链接**: [Issue #4093](https://github.com/OpenHands/software-agent-sdk/issues/4093)

**中优先级**
-   **问题: `max_concurrent_runs` 配置项不限制原生异步对话 [Issue #4063]**
    -   **严重性**: 中。配置项失效导致并发控制机制无效，可能引发非预期的资源消耗和集群负载。
    -   **状态**: 无需 Pending fix PR。
    -   **链接**: [Issue #4063](https://github.com/OpenHands/software-agent-sdk/issues/4063)

-   **问题: `TaskToolSet` 在父级被中断时不向活跃子 Agent 传递中断信号 [Issue #4107]**
    -   **严重性**: 中。这是多 Agent 协调中的一个 Bug，中断行为不一致可能导致子 Agent 无法及时清理、产生孤立进程或丢失上下文。
    -   **状态**: 无需 Pending fix PR。
    -   **链接**: [Issue #4107](https://github.com/OpenHands/software-agent-sdk/issues/4107)

-   **问题: WindowsTerminal 无法提交多行 PowerShell 命令 [Issue #4133]**
    -   **严重性**: 中。此 Bug 严重限制了 Windows 平台用户的 Agent 能力，尤其是在执行如 PS1 脚本等复杂命令时。
    -   **状态**: 新增 Bug，需尽快确认和分配。
    -   **链接**: [Issue #4133](https://github.com/OpenHands/software-agent-sdk/issues/4133)

-   **问题: 未认证的模型信息查找导致无意义的 API 请求 [Issue #4098]**
    -   **严重性**: 中。虽不直接影响功能，但造成了不必要的网络请求和潜在的性能开销，属于代码健壮性问题。
    -   **状态**: 无需 Pending fix PR。
    -   **链接**: [Issue #4098](https://github.com/OpenHands/software-agent-sdk/issues/4098)

**低优先级**
-   **问题: 无效或过期的 LLM API Key 导致无业务可操作的错误 [Issue #3411]**
    -   **严重性**: 低（已关闭，但问题本身具有代表性）。虽然已关闭，但该问题反映了用户配置错误时的不佳体验，提示项目在错误信息传达方面有改进空间。修复方案可能是提供更清晰、可操作的错误提示。
    -   **状态**: 已关闭。
    -   **链接**: [Issue #3411](https://github.com/OpenHands/software-agent-sdk/issues/3411)

### 6. 功能请求与路线图信号

今日活跃的功能请求反映了向**更健壮、更灵活、更易扩展**方向发展的需求。

-   **选择性上下文激活 ([PR #3890](https://github.com/OpenHands/software-agent-sdk/pull/3890))**: 该 PR 旨在消解 `AGENTS.md` 中的上下文膨胀，允许为不同子 Agent 加载相关信息。这是一个重要的架构优化，暗示项目正从单体 Agent 向更复杂的多 Agent、微服务化组织演进。很可能成为下一个大版本的核心特性。

-   **非阻塞后台子 Agent 执行 ([Issue #2047](https://github.com/OpenHands/software-agent-sdk/issues/2047))**: 尽管已关闭，但其 “支持后台任务” 的思想与 “选择性上下文激活” 一脉相承，都是关于 Agent 执行模式的进化。这可能是项目未来提升并发能力的方向。

-   **MCP 超时传播 ([PR #3254](https://github.com/OpenHands/software-agent-sdk/pull/3254))**: 该提出的功能允许用户在 MCP 服务器配置中定义工具超时，并自动应用到执行器。这为 MCP 集成提供了更精细的控制能力，是提升 SDK 可配置性和健壮性的重要一步。

-   **Kimi Code 会员集成 ([PR #4150](https://github.com/OpenHands/software-agent-sdk/pull/4150))**: 新增对 Moonshot 的 Kimi Code 编程模型的支持。这表明项目正在积极扩展其 LLM 兼容列表，拥抱中国市场/模型的开发者，具有明确的路线图信号。

### 7. 用户反馈摘要

-   **用户痛点 - Windows 平台体验差**: `[Issue #4133]` 报告了 WindowsTerminal 无法处理多行 PowerShell 命令的问题。这表明 Windows 用户体验是当前的一个薄弱环节，对于想要在 Windows 环境下运行的 Agent 构成了严重障碍。

-   **用户痛点 - 依赖管理自动化失效**: `[Issue #2510]` 的高评论数表明，依赖自动化（Dependabot）在 `uv workspace` 上的失效问题持续困扰团队，迫使他们回到手动管理的老路上，增加了维护负担。

-   **用户痛点 - 恢复机制脆弱**: `[Issue #4080]` 和 `[Issue #3411]` 从不同角度反映了恢复/加载机制的问题。前者是灾难性的整个对话丢失，后者是配置错误导致“假死”。用户期望有更强的容错能力和更清晰的错误信息。

-   **用户诉求 - 更好的 LLM 兼容性**: `[Issue #3992]` 和 `[Issue #4093]` 表明社区正在使用各种 LLM（包括弱/本地模型和特定厂商的 CLI），并遇到了 SDK 核心逻辑对他们的不兼容。用户希望 SDK 更加“模型中立”和“向前兼容”。

### 8. 待处理积压

以下 Issue 或 PR 已存在较长时间但仍未获得足够关注或解决，提醒维护者关注。

-   **重大功能 PR 长期搁置**:
    -   `[PR #3890]` (选择性上下文激活): 创建近一个月，是潜在的颠覆性功能，可能会有较大的 API 或行为变更。
    -   `[PR #3254]` (MCP 超时传播): 创建两个多月，涉及跨组件协作，可能需要在多个层面进行协调。
    -   `[PR #3336]` (读写安装元数据编码问题): 存在超过一个月的 Bug fix，虽然简单但涉及平台兼容性（Windows），应优先合并。

-   **高价值功能请求待评估**:
    -   `[Issue #2047]` (非阻塞后台子 Agent): 尽管已标记为 `Stale` 并关闭，但该特性与当前的热点方向（多 Agent、上下文管理）高度相关，建议重新评估其可行性，或考虑将其纳入后续版本规划。

-   **用户修复的 Bug 等待合并**:
    - `[Issue #3411]` (无效 API Key 错误难以调试): 已关闭，但用户提出的根本体验问题（提供可操作的错误信息）仍未在社区中得到广泛解决。如果已有解决思路，应该创建新的 Issue 来跟进。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，作为专注于 AI 智能体与个人 AI 助手领域的开源项目分析师，我已根据您提供的 2026-07-19 的 GitHub 数据，为您生成了 Pi 项目的动态日报。

---

### 📈 Pi 项目动态日报 | 2026-07-19

---

#### 1. 今日速览

项目今日活跃度极高，在过去24小时内共处理了 **26 条 Issues** 和 **9 个 PR**，显示出强大的社区参与度和维护团队的高效响应。大部分 Issues 集中在 Bug 修复和用户体验优化上，而 PR 侧重点在于增强系统稳定性和修复关键功能缺陷（如重试机制、连接处理）。尤其值得肯定的是，针对「压缩」和「OpenAI Responses」等核心流程的稳定性 Rusty 补丁正在合并，标志着项目正从功能快速迭代阶段，转向更注重健壮性和性能优化的成熟期。

---

#### 2. 版本发布
无。

---

#### 3. 项目进展

今日有多项重要改进被合并或关闭，项目在稳定性和用户体验方面迈出了坚实一步。

- **核心流程健壮性增强：**
    - **[PR #6775] (OPEN -> 待合并)** 为「压缩」和「分支摘要」功能引入了失败重试机制。这直接修复了 `#6647` 中单次临时性流中断导致整个压缩过程失败的问题，是提升后台任务可靠性的关键补丁。[查看详情](https://github.com/earendil-works/pi/pull/6775)
    - **[PR #6807] (CLOSED)** 修复了 OpenAI Responses API 流式处理中的“僵尸连接”问题。现在，当收到 `response.completed` 事件后，系统会立即停止读取流，避免无谓地等待直到网络 EOF，从而提升了响应速度和资源利用率。[查看详情](https://github.com/earendil-works/pi/pull/6807)
    - **[PR #6804] (CLOSED)** 修复了当提供者被注销后，其对应的作用域模型无法从 `enabledModels` 列表中移除的 UI Bug，解决了 `#6806` 中用户必须手动修改配置文件的痛点。[查看详情](https://github.com/earendil-works/pi/pull/6804)

- **用户体验优化：**
    - **[PR #6802] (CLOSED)** 修正了页脚扩展上下文指示器硬编码为 `[1M]` 的问题。现在它会准确显示模型实际的 `extendedContextWindow` 值，为用户提供了更精确的信息反馈。[查看详情](https://github.com/earendil-works/pi/pull/6802)
    - **[PR #6812] (CLOSED)** 修复了 `pi-ai` 二进制路径声明不一致导致的 `package-lock.json` 文件冲突问题，解决了依赖管理中的一个恼人痛点。[查看详情](https://github.com/earendil-works/pi/pull/6812)

---

#### 4. 社区热点

今日社区讨论最热烈的两个议题反映了用户对**系统行为透明度和控制力**的深层次需求。

-   **#6303: 指数退避重试无限增长问题**（**8条评论，1个👍**）
    - **链接**: [https://github.com/earendil-works/pi/issues/6303](https://github.com/earendil-works/pi/issues/6303)
    - **分析**: 此 Issue 揭示了 `getRetrySettings()` 未返回 `maxDelayMs` 参数，导致指数退避策略在极端情况下（如重试7次）产生长达数分钟的等待。用户普遍认为即使存在 `maxRetryDelayMs` 配置项，代码也未正确遵守。背后是对“系统行为需有边界和可控性”的诉求，即使是为了重试的可靠性，也不应以无限等待为代价。该 Issue **今日刚被标记为已关闭**，表明团队已快速响应并修复了此问题。

-   **#3790: 为思维层级循环增加反向快捷键**（**6条评论**）
    - **链接**: [https://github.com/earendil-works/pi/issues/3790](https://github.com/earendil-works/pi/issues/3790)
    - **分析**: 这是一个典型的用户体验优化提案。在具有5-6个思维层级的系统中，用户很容易“过头”。提案要求增加反向循环快捷键，而不是被迫正向循环所有级别。这反映了社区在工具使用中追求“效率”和“控制感”的普遍心态。该 Issue 维护了三个月后于今日关闭，表明团队可能已找到一种合理的方式将其纳入未来更新。

---

#### 5. Bug 与稳定性

今日报告的 Bug 涉及计费、兼容性、性能等多个维度，按严重程度排列如下：

-     **(严重) #6725 [OPEN] Copilot 的 GPT-5.6 模型定价错误**
    - **链接**: [https://github.com/earendil-works/pi/issues/6725](https://github.com/earendil-works/pi/issues/6725)
    - **分析**: 报告指出 Copilot 服务的 OpenAI 模型未将 `cacheWrite` 成本计入总费用。这直接关乎用户实际账单与 Pi 显示费用的不一致，属于财务记账层面的严重 Bug。目前标记为 `inprogress`。

-   **(严重) #6784 [CLOSED] iTerm2 与 Pi.dev 的兼容性问题**
    - **链接**: [https://github.com/earendil-works/pi/issues/6784](https://github.com/earendil-works/pi/issues/6784)
    - **分析**: 报告称 Pi.dev 在 iTerm2 上“几乎不可用”，出现画面跳闪、背景颜色异常。鉴于 iTerm2 是 macOS 下流行的终端模拟器，此问题影响面较大，所幸今日已被关闭。

-   **(中) #6794 [CLOSED] 因模型目录刷新导致启动超级慢**
    - **链接**: [https://github.com/earendil-works/pi/issues/6794](https://github.com/earendil-works/pi/issues/6794)
    - **分析**: 用户报告 Pi 启动“永远”没反应，原因是启动时获取最新模型目录（model catalogue）的操作卡住了。这属于冷启动性能问题，已关闭，但应关注其背后的优化或限时策略。

-   **(中) #6675 [OPEN] `pi update --self` 在连接中断后无重试**
    - **链接**: [https://github.com/earendil-works/pi/issues/6675](https://github.com/earendil-works/pi/issues/6675)
    - **分析**: 自更新操作过于脆弱，一次临时的网络故障就会导致更新失败并退出，没有自动重试机制。这降低了用户的更新成功率，尤其是在网络不稳定的环境中。

-   **(低) #6782 [CLOSED] 天城文（印地语）导致编辑器重绘损坏**
    - **链接**: [https://github.com/earendil-works/pi/issues/6782](https://github.com/earendil-works/pi/issues/6782)
    - **分析**: 属于输入法/字符集兼容性问题。粘贴非拉丁字符导致编辑器每敲一次键盘就重复输出若干行。已关闭，可能是通过添加输入过滤或修复渲染引擎处理。

**已有 Fix PR 的 Bug**：
- `#6647` (压缩失败) -> `#6775` (已 PR，待合并)
- `#6806` (无法移除作用域模型) -> `#6804` (已合并修复)
- `#6808` (流式处理等待 EOF) -> `#6807` (已合并修复)
- `#6811` (lockfile 文件冲突) -> `#6812` (已合并修复)

---

#### 6. 功能请求与路线图信号

-   **高潜力：手动重试命令 `/retry`** (`#6810`)
    - **链接**: [https://github.com/earendil-works/pi/issues/6810](https://github.com/earendil-works/pi/issues/6810)
    - **信号**: 此功能简单直观，用户在弱网环境下有强烈需求。它提供了一个当自动重试耗尽后的手动“救场”方式，API 描述中提到的“Exactly like today‘s automatic retry”也降低了实现复杂度。极有可能被纳入下一版本的改进中。

-   **中期规划：隐藏/禁用 Provider 的能力** (`#6803`)
    - **链接**: [https://github.com/earendil-works/pi/issues/6803](https://github.com/earendil-works/pi/issues/6803)
    - **信号**: 社区对 `models.json` 的管理精细化诉求。用户希望在不删除配置的情况下，能按需启用/停用某些 Provider，以便在 `/model` 列表和管理界面中减少干扰。此需求反映了用户对“可配置性”和“信息洁净度”的更高要求。

-   **长期考量：共享认证文件支持** (`#6813`)
    - **链接**: [https://github.com/earendil-works/pi/pull/6813](https://github.com/earendil-works/pi/pull/6813)
    - **信号**: 通过环境变量独立于 Pi agent 配置目录的认证文件路径，这将利好于团队协作、CI/CD、或需要更严格权限管理的部署场景。该 PR 为代码代理引入此功能，预示着项目正在向更企业级、更可编程的方向演进。

---

#### 7. 用户反馈摘要

-   **正面反馈**: 用户在 `#6303` 中明确指出 **“虽然存在 `maxRetryDelayMs` 配置项，但代码并未使用它”**，这表明用户对 Pi 的配置体系有深入了解并提出了合理质疑。而 Issue 关闭后，维护者应已确认并修复了此不一致性，提升了产品透明度。
-   **痛点反馈**: 低移动网络覆盖成为终端用户的核心痛点（`#6810`），自动重试穷尽很快，且无手动干预手段。这提示项目应考虑构建**更智能、可交互**的网络恢复策略。
-   **体验反馈**: 用户对 `iTerm2` (`#6784`) 和 `Devanagari` (`#6782`) 的兼容性问题抱怨强烈，说明**跨平台和国际化**的测试仍有待加强。同时，`Ctrl+G` 编辑器打开慢 (`#6774`) 和启动加载卡死 (`#6794`) 等性能问题，是影响用户第一印象的关键因素。
-   **贡献者行为**: `#6811` 的作者在发现自己的 PR 不符合贡献规范（未获得 `lgtm`）后，礼貌地在 PR 描述中道歉并承认错误，社区氛围积极健康。

---

#### 8. 待处理积压

-   **[OPEN] Issue #6303 / PR #6775: 指数退避 & 压缩重试**
    - **链接**: [https://github.com/earendil-works/pi/pull/6775](https://github.com/earendil-works/pi/pull/6775)
    - **分析**: 虽然关联的 `#6303` 已关闭，但其核心修复——为压缩功能添加重试——的 PR `#6775` 仍处于 **OPEN** 状态，等待 maintainer 审阅和合并。这同样是提升核心流程稳定性的关键一环，值得优先关注，避免“结论已出，修复未到”的情况。

-   **[OPEN] PR #5262: 为 Anthropic Vertex AI 提供商增加支持**
    - **链接**: [https://github.com/earendil-works/pi/pull/5262](https://github.com/earendil-works/pi/pull/5262)
    - **分析**: 这是一个来自外部贡献者、功能完整的 PR，旨在添加 GCP Vertex AI 上的 Claude 模型支持。该 PR 自 **2026-05-31** 起已处于 OPEN 状态近50天。虽然更新日期显示有新的提交，但该 PR 代表了一项重要的平台集成，长期未合并可能会导致社区贡献者的积极性下降，是项目路线图上需要决策的信号。

---
**报告结束。**

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据 2026-07-18 全天（覆盖至 2026-07-19 日报生成时间点）的 GitHub 数据，以下是 LiteLLM 项目动态日报。

---

## LiteLLM 项目动态日报 | 2026-07-19

### 1. 今日速览

过去 24 小时，LiteLLM 项目保持 **高活跃度**：共处理 41 条 Issue（新开/活跃 21 条，关闭 20 条），并提交了 212 个 PR（待合并 107 个，已合并/关闭 105 个）。社区围绕 **稳定性冲刺** 和 **v1.93.0 版本发布** 展开密集协作，大量回归问题被确认并快速提交修复。**Rust 重构** 工作持续推进，多个核心 API 的 Rust 端口正在开发中，同时官方也在积极解决因依赖和 Docker 镜像引起的部署中断问题。整体项目 **健康度良好**，但短期稳定性仍需关注。

### 2. 版本发布

**无新版本发布。** 目前团队正积极准备 v1.93.0 稳定版，已通过 PR #33847 和 #33869 将多个 staging 修复 backport 至 `patch-1.93.0rc2` 分支，预计在下一日完成正式发布。

### 3. 项目进展

今天共有 **105 个 PR 被合并/关闭**，涵盖功能开发、稳定性修复和基础设施升级。以下为重点进展：

- **v1.93.0 稳定版筹备**：PR #33847 和 #33869 完成了共 13 个 staging 修复的 backport，包括 Docker 镜像启动修复（#33853）、路由器 `/v1/models` 端点性能回归修复（#33864）等。
- **Rust 原生重构推进**：
  - PR #33848：实现 `LITELLM_RUST` 环境变量控制，将原生 Anthropic `/messages` 路由到 Rust 后端。
  - PR #33849：1:1 移植 OpenAI Responses API WebSocket 到 `litellm-rust`。
  - PR #33836：重构代码结构，将 Rust 库统一放入顶层 `src/` 目录。
  - PR #33865 / #33867：新增 Rust 提供者抽象标准和官方 Rust 风格指南文档。
- **新 Provider 支持**：
  - PR #33862：阿里云 DashScope 新增 `qwen-image-edit-plus` 图像编辑和 `qwen3-tts-vc` 语音合成支持。
  - PR #33866：字节跳动 `BytePlus` 新增 `Seedream` 图像生成模型支持。
- **功能优化**：
  - PR #33810：在每日花费聚合中跟踪 prompt 压缩节省的 tokens。
  - PR #33856：修复 Azure AI Foundry 模型的 Responses API 路由到原生端点。
  - PR #33832：新增端到端测试，验证多预算窗口的正确行为。
- **依赖与构建修复**：
  - PR #33822：将 `aiohttp` 上限锁定在 3.14 以下，避免连接池超时回归。
  - PR #33857：为 rc 版本重建 Admin UI 前端 bundle。

### 4. 社区热点

| Issue / PR | 类型 | 评论数 | 核心诉求 |
|---|---|---|---|
| [#30484](https://github.com/BerriAI/litellm/issues/30484) – LiteLLM Stability Sprint Roadmap | Issue (开放性) | 24 | **稳定性冲刺路线图**。作者 @ishaan-berri 将稳定性提升为一等公民，列出本周 bug 修复计划，并邀请社区投票。用户积极参与，列出希望优先处理的 bug（如 `/v1/model/info` 不一致响应）。 |
| [#11364](https://github.com/BerriAI/litellm/issues/11364) – Anthropic cached tokens 成本计算错误 | Issue (已关闭) | 14 | 使用 Anthropic 模型时，缓存 token 成本被当成普通输入计算，导致费用统计错误。该 Issue 持续一年多后今日由用户 @regismesquita 回复确认，已关闭（可能已修复）。 |
| [#14052](https://github.com/BerriAI/litellm/issues/14052) – x-litellm-tags 未正确路由请求 | Issue (开放性) | 7 | 标记为 **P0** 和 **blocking use cases**，影响使用标签路由的企业用户。期望当目标标签失效时，应回退到类似标签或 fallback 模型。目前仍开放，社区要求更高优先级处理。 |

**分析**：社区最关注的是 **稳定性**（路线图）和 **成本准确性**（Anthropic 缓存计费）。标签路由问题被标记为最高优先级，但尚未分配 PR，需持续关注。

### 5. Bug 与稳定性

今日报告了多个回归或阻碍性 Bug，按严重程度排列：

| 严重等级 | Issue | 问题 | 状态 |
|---|---|---|---|
| **P0 – 阻断部署** | [#33650](https://github.com/BerriAI/litellm/issues/33650) | v1.90.0+ 的 Docker 镜像因 `libatomic.so.1` 缺失导致新部署数据库迁移静默失败（与 #24554 同根因）。 | 已关闭（在今天 backport 的 #33853 修复） |
| **高 – 性能/可用性** | [#33636](https://github.com/BerriAI/litellm/issues/33636) | v1.92.0 中 `GET /v1/models` 在每个模型上执行未缓存的 `get_model_group_info`，导致 CPU 飙升数分钟，健康检查失败。 | 已关闭（#33864 修复） |
| **中 – 功能异常** | [#33824](https://github.com/BerriAI/litellm/issues/33824) | v1.92.0+ 中 Anthropic `/v1/messages` 代理与 Zhipu 模型不兼容，Claude CLI 集成失败。 | 开放，暂无对应 PR |
| **中 – UI 崩溃** | [#33381](https://github.com/BerriAI/litellm/issues/33381) | Usage 页面在数据集较大时客户端崩溃（`Cannot read properties of undefined (reading 'spend')`）。 | 开放 |
| **低 – 翻译错误** | [#33281](https://github.com/BerriAI/litellm/issues/33281) | Bedrock 开启 `guardrailConfig` 后，尾部用户消息的 `cache_control` 被静默丢弃。 | 开放 |
| **低 – 流式数据** | [#33764](https://github.com/BerriAI/litellm/issues/33764) | 使用 `response_format=json` 转录时 Pydantic 校验失败。 | 开放 |

此外，以下回归问题今日已有对应的 fix PR：
- #33859 – 修复 Anthropic 流式响应中重复的 `message_start` 事件。
- #33860 – 修复 `responses` 到 `chat completions` 转换中空 `tools` 数组问题。
- #33861 – 修复 `token_counter` 遇到 Anthropic 图像内容块时抛异常的问题。
- #33864 – 修复路由器 `/v1/models` 中 malformed token 限制导致类型错误。

### 6. 功能请求与路线图信号

- **稳定性冲刺（#30484）**：官方公开路线图，计划修复一系列 bug，社区评论表明最期望解决的是 **模型信息接口不一致**、**慢查询** 和 **标签路由**。
- **FIPS 合规（#25861，3 个👍）**：用户要求 LiteLLM Proxy 符合 FIPS 标准，该请求曾因长期未更新被关闭，现已重新开放，并附有详细需求描述（加密模块、TLS 等）。
- **Anthropic `task_budget` 参数支持（#25971）**：用户希望 SDK 支持 Claude Opus 4.7 的 `task_budget` 参数，属于新模型特性适配。
- **Rust 原生路由**：PR #33848 和 #33849 表明官方正在将 Anthropic Messages 和 OpenAI Responses WebSocket 等核心 API 迁移至 Rust 实现，预计将在未来版本中通过环境变量切换。
- **预算/配额增强**：PR #33832 的测试表明团队在完善多 budget window 的正确性；PR #33810 在花费日志中记录 prompt 压缩节省 tokens，为更细粒度计费做准备。

### 7. 用户反馈摘要

从今日 Issues 评论中提炼出以下用户声音：

- **“Docker 镜像挂了很久”**：多位用户反映 v1.90.0 至 v1.92.0 期间新部署完全无法启动（#33650 评论区），导致无法升级，强烈要求尽快修复。该问题已在今日 backport 中解决。
- **“标签路由不可靠”**：企业用户 @TeddyAmkie 在 #14052 中描述 `x-litellm-tags` 在目标模型失败时不回退，导致生产流量中断。用户希望提供明确回退优先级。
- **“成本统计误差影响预算”**：#11364 的 Anthropic 缓存成本问题持续一年，用户 @regismesquita 指出这导致实际花费与报告不符，影响企业成本管控。虽已关闭，但用户仍希望官方进行回归测试。
- **“Admin UI 崩溃”**：#33381 的用户抱怨在使用多页数据时页面完全无法加载，影响监控体验。
- **“导入包导致内存激增”**：#24398 的用户发现在 FastAPI 应用中导入 `litellm` 导致 RAM 从 130MB 飙升至 1.3GB，对资源敏感部署构成挑战。

### 8. 待处理积压

以下为开放时间较长（超过一周）或标记为高优先级但暂无对应 PR 的关键 Issue：

| Issue | 创建日期 | 标签 | 说明 |
|---|---|---|---|
| [#14052](https://github.com/BerriAI/litellm/issues/14052) – 标签路由问题 | 2025-08-29 | `P0`, `blocking use cases`, `enterprise` | 仍是开放性最高优先级的 bug，无 assignee，需优先分配。 |
| [#18685](https://github.com/BerriAI/litellm/issues/18685) – `ensure_alternating_roles` 对 tool calls 失效 | 2026-01-06 | `bug`, `proxy`, `llm translation`, `SDK` | 影响 Devstral 2 等模型，5 条评论，无进展。 |
| [#24398](https://github.com/BerriAI/litellm/issues/24398) – 导入时 RAM 飙升 | 2026-03-23 | `llm translation`, `stale` | 已标记 stale，但未关闭，用户仍受此问题困扰。 |
| [#25628](https://github.com/BerriAI/litellm/issues/25628) – langfuse_otel 记录原始模型名而非别名 | 2026-04-13 | `bug`, `proxy`, `llm translation` | 影响可观测性场景，3 条评论，无 PR。 |
| [#25861](https://github.com/BerriAI/litellm/issues/25861) – FIPS 合规 | 2026-04-16 | `enhancement`, `proxy` | 企业安全刚需，3 个👍，仍需设计/实现。 |
| [#26019](https://github.com/BerriAI/litellm/issues/26019) – 悬空请求告警：600s+ 但在 spend logs 中无记录 | 2026-04-18 | `proxy`, `llm translation`, `stale` | 监控告警与数据不一致，2 条评论，无处理。 |

---

**总结**：今日 LiteLLM 项目主要围绕 **v1.93.0 稳定性版本** 和 **Rust 重构** 两大主线运转。社区对 Docker 部署破坏性回归和标签路由问题反应强烈。建议维护者在明日发布稳定版本后，优先解决 #14052 等 P0 积压问题，并考虑对 #24398 的 RAM 问题进行性能优化。

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 Temporal 项目 GitHub 数据，为您生成 2026年7月19日的项目动态日报。

---

### **Temporal 项目动态日报 | 2026-07-19**

#### **1. 今日速览**

过去24小时内，Temporal 项目没有报告新问题，Issues 更新量为 0，但 Pull Requests (PR) 动态非常活跃，共更新了 19 条。这主要源于多项新功能（如 Standalone Activity 和 CHASM）的并行开发与测试加固。虽然今日无新版本发布，但涉及 **1.32.0 版本发布分支准备** 的 PR 已被合并，表明下一个正式版本的发布流程已启动。整体来看，项目处于**密集开发与新功能收尾阶段**，核心团队通过持续提交测试用例和修复来确保新特性的稳定性，项目健康度良好，活跃度评估为**高**。

#### **2. 版本发布**

无新版本发布。

#### **3. 项目进展**

今日有 3 个 PR 被成功合并或关闭，标志着重要模块的推进：

- **准备 v1.32.0 发布分支**： [#11136](https://github.com/temporalio/temporal/pull/11136) 已合并。这是一个计划中的维护操作，用于创建一个新版本分支，通常意味着近期会有新版本发布。此 PR 更新了依赖并覆盖了 governance 文件。
- **性能与代码清理**：
    - [#11065](https://github.com/temporalio/temporal/pull/11065) 已合并。这是一个显著的性能优化，将 `MapRequestRateLimiterImpl` 的清理逻辑从独立的 goroutine 改为惰性（lazy）逐出模式，减少了因定时清理带来的资源开销和内务管理复杂性。
- **新功能默认启用**：
    - [#11122](https://github.com/temporalio/temporal/pull/11122) 已合并。此 PR 将 `Standalone Activity` 的启动延迟功能默认开启，并增加了命名空间级别的能力控制。这是 `Standalone Activity` 能力走向成熟并逐步开放给所有用户的关键一步。

这些合并推进了**性能优化**和**核心功能灰度**的进程，项目整体向着更稳定、更高效的 v1.32.0 版本迈进了一大步。

#### **4. 社区热点**

尽管今日没有产生大量评论和反应的 Issue/PR，但以下 PR 代表了社区和开发者最关注的领域，其背后的诉求非常明确：

- **Scheduler 系统全面加固**： 以 @davidporter-id-au 为代表，提交了一系列关于 **CHASM Scheduler** 的测试框架 PR，包括**生命周期驱动测试** ([#10726](https://github.com/temporalio/temporal/pull/10726))、**确定性属性测试** ([#10727](https://github.com/temporalio/temporal/pull/10727))、**随机序列的快速属性测试** ([#10728](https://github.com/temporalio/temporal/pull/10728)) 以及 **V2->V1->V2 迁移的往返测试** ([#10729](https://github.com/temporalio/temporal/pull/10729))。这表明开发团队正在对核心的 **Scheduler 模块进行大规模、高密度的测试覆盖**，目标是确保迁移和运行时的绝对稳定，这是支撑生产环境信赖的基础。

- **Standalone Activity (SAA) 功能集大成**： 多个与 SAA 相关的 PR 在今日活跃，包括**超时类型修复** ([#11137](https://github.com/temporalio/temporal/pull/11137))、**状态暴露** ([#11130](https://github.com/temporalio/temporal/pull/11130))、**元数据追踪** ([#11049](https://github.com/temporalio/temporal/pull/11049)) 和**可见性支持** ([#11017](https://github.com/temporalio/temporal/pull/11017))。这揭示了社区对 `Standalone Activity` 功能的强烈期待，用户迫切需要**更精细的控制**（如暂停、恢复）、**更准确的监控**（如正确报告超时、执行时间）和**更高的调试透明度**。

#### **5. Bug 与稳定性**

今日无新增 Issues 报告严重 Bug，但以下 PR 直接解决了已存在的问题和潜在风险：

- **严重级 - 功能逻辑错误**：
    - **[#11134](https://github.com/temporalio/temporal/pull/11134)**: 修复了 Scheduler 从 v1 迁移到 v2 时可能导致的第三方 SDK 崩溃问题。通过引入迁移保护，只对可能出错的缓存条目进行迁移，而非全量。这是一个影响面广的回归性修复。
- **中等级 - 行为不符合预期**：
    - **[#11137](https://github.com/temporalio/temporal/pull/11137)**: 修复了 `Standalone Activity` 在达到 `ScheduleToClose` 截止时间时，错误报告超时类型的问题。现在会正确报告为 `SCHEDULE_TO_CLOSE`，提升了错误诊断的准确性。
    - **[#11028](https://github.com/temporalio/temporal/pull/11028)**: 修复了 CHASM 模式下 `Nexus` 操作在 `workflow reset` 后无法完成的问题，通过添加 run fallback 逻辑，使其与 HSM 模式行为一致，保证了数据一致性。

#### **6. 功能请求与路线图信号**

结合今日活跃的 PR，可以清晰看到项目下一阶段的路线图重点：

- **Standalone Activity (SAA) 功能集**： [#10106](https://github.com/temporalio/temporal/pull/10106) （Pause/Unpause/Reset/UpdateOptions）虽然创建较早今日未有活跃更新，但其他配套 PR 的活跃表明该大型功能正处于集成和打磨阶段。可以预见，**完整的 SAA 控制面**将是下一个版本的重要卖点。
- **CHASM 模块的完善**： [#11080](https://github.com/temporalio/temporal/pull/11080) 为 CHASM 库增加了系统搜索属性注册选项，这是完善 CHASM 作为全新底层架构能力的重要一环，预示着未来可能有更多基于 CHASM 的特性发布。
- **代码清晰度与维护性提升**： [#11133](https://github.com/temporalio/temporal/pull/11133) 计划移除已默认开启的 `matching.enableMigration` 动态配置，这表明团队正在清理已稳定功能的遗留配置，减少维护负担。而 [#11132](https://github.com/temporalio/temporal/pull/11132) 对匹配客户端的重构，则体现了对代码可读性和性能一致的追求，是项目长期健康的信号。

#### **7. 用户反馈摘要**

由于 24 小时内无新的 Issues 讨论，根据 PR 的“Why”部分可以间接捕捉到用户反馈和痛点：

- **痛点：监控数据不准确**。 用户在查询 Standalone Activity 状态时发现 `PAUSED` 状态的 Activity 被显示为 `Running` ([#11130](https://github.com/temporalio/temporal/pull/11130))，导致无法基于状态进行有效过滤和查询。这凸显了用户对**精确且颗粒度小的状态可见性**的需求。
- **需求：更强大的控制能力**。 来自 [#10106](https://github.com/temporalio/temporal/pull/10106) 等 PR 的长期存在，说明用户一直在积极推动对 `Standalone Activity` 更丰富的运维操作（暂停、恢复、重置等），以满足动态流程管理和故障恢复的场景。

#### **8. 待处理积压**

以下为开放时间较长且今日有更新的重要 PR，提醒维护者关注其推进和测试情况：

- **[#10726 - #10729] Scheduler 测试套件系列**： 这 4 个 PR 自 2026-06-16 起开放，由 @davidporter-id-au 提交。它们为 CHASM Scheduler 构建了完整的测试基础设施。虽然存在时间较长，但今日有更新，表明仍在活跃开发中。考虑到其庞大和重要性，可能需要更多审查时间。维护者应重点确保这些测试能尽快合并，以保障 Scheduler 功能的稳定性。

---

**分析师总结**：Temporal 项目今日在**核心功能（Standalone Activity 和 CHASM Scheduler）的测试和稳定性修复**上投入了大量精力。虽然没有新版本发布，但 v1.32.0 发布分支的创建和多项性能/代码优化 PR 的合并，都预示着即将迎来一个重要的功能发布。项目健康状态良好，代码质量与测试文化持续巩固。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*