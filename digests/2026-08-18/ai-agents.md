# OpenClaw 生态日报 2026-08-18

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-17 22:44 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-18

## 今日速览

过去24小时内，OpenClaw 仓库保持极高活跃度：**500条 Issue 更新**（其中新开/活跃 489 条，关闭 11 条）和 **500条 PR 更新**（待合并 406 条，合并/关闭 94 条）。Issue 与 PR 更新量双双触顶榜单上限，说明项目正经历大规模的社区反馈与贡献涌入。然而，**0 个新版本发布**，且大量高优 Issue 仍处于 `needs-maintainer-review` 状态，提示维护团队可能面临显著的审查积压压力。整体来看，项目处于**高活跃度与高积压并存**的状态——社区热情高涨，但核心维护者的处理速度或成瓶颈。

---

## 版本发布

今日无新版本发布（最新 Releases 为空）。

---

## 项目进展

尽管无新版本发布，但今日有 **94 个 PR 被合并或关闭**，以下为值得关注的已完成工作：

### 已合并/关闭

1. **[#120900 feat(ui): review install policy warnings](https://github.com/openclaw/openclaw/pull/120900)** —（已关闭，CLOSED）为 Control UI 增加安装策略警告的审查与确认能力。管理员可在界面中查看插件安装的安全警告并主动确认继续。与已关闭的 [#116489](https://github.com/openclaw/openclaw/pull/116489) 配套，后者实现了同一功能的 CLI 路径。两者合并意味着**安全的插件安装流程在 CLI 与 UI 两端均已落地**，这是对供应链安全的重要加固。

### 仍开放但取得阶段性进展

2. **[#125302 fix(agents): stop silent compaction failures](https://github.com/openclaw/openclaw/pull/125302)** — 修复自动会话压缩静默失败的问题。此前会话压缩失败时不记录任何原因，导致会话无限增长直至硬性上下文溢出。当前处于 `⏳ waiting on author` 状态。

3. **[#125435 fix(agents): preserve configured workspaces after setup migration](https://github.com/openclaw/openclaw/pull/125435)** — 修复从旧版升级时，Doctor 的 JSON-to-SQLite 迁移后自定义工作区被误判为丢失的问题。

4. **[#125384 refactor(workers): make worker turns node-only](https://github.com/openclaw/openclaw/pull/125384)** — 移除 worker 执行模式中已废弃的 SSH 租约路径，仅保留 node 传输方式，简化了 worker-provider 合约。

5. **[#120900 feat(ui): review install policy warnings](https://github.com/openclaw/openclaw/pull/120900)**（已关闭）、**[#116489 feat(security): require acknowledgement for install policy warnings](https://github.com/openclaw/openclaw/pull/116489)**（已关闭）——两者构成完整的"安装策略警告确认"功能闭环，涉及 CLI、UI、Gateway 三层，属于安全加固的实质性推进。

> **项目健康度观察**：今日合并/关闭的 PR 数量尚可（94），但核心修复类 PR（如 #125302、#125435）尚未合并，且大量 PR 处于 `waiting on author` 或 `needs proof` 状态，合并节奏有待提升。

---

## 社区热点

### 讨论最活跃的 Issues

1. **[#77598 [maintainer, P2] Track live dev agent behavior and trajectory](https://github.com/openclaw/openclaw/issues/77598)** — **23 条评论**。这是一个持续追踪开发者（Pash）dev agent 行为的运行笔记式 issue，观察从 2026-05-04 开始至今已超过 3 个月。社区对此高度关注，反映了用户对**代理行为可观测性**的强烈兴趣。

2. **[#91009 [P1] Codex PreToolUse native hook relay spawns CPU-bound openclaw-hooks processes and stalls gateway RPC](https://github.com/openclaw/openclaw/issues/91009)** — **20 条评论**。Codex 集成导致的 CPU 100% 占用问题，严重影响 Gateway 性能。属于发布阻断类缺陷。

3. **[#68596 [P2] Feature Request: Configurable streaming watchdog timeout threshold](https://github.com/openclaw/openclaw/issues/68596)** — **15 条评论，👍 8 次**。用户对长时间思考模型（如 DeepSeek-R1）频繁触发流式看门狗警告表示不满，要求可配置超时阈值。这一需求在长推理模型流行的背景下颇具代表性。

4. **[#62505 [P1] Coding Agent never completes anything](https://github.com/openclaw/openclaw/issues/62505)** — **15 条评论**。高优回归问题：编码 Agent 从 2026.4.2 版本后完全失效。直接打击核心使用场景。

5. **[#38327 [P1] "Cannot convert undefined or null to object" with google-vertex/gemini-3.1-pro-preview](https://github.com/openclaw/openclaw/issues/38327)** — **14 条评论，👍 3 次**。知名模型供应商集成回归，影响面较大。

### 讨论最活跃的 PRs

PR 列表显示评论数均为 `undefined`（数据未展示），但以下 PR 因标签密度高（`maintainer`、`P0/P1`、`merge-risk` 等）值得关注：

- **[#125412 [P0] fix(gateway): restore external Tailscale Serve and Funnel proxies](https://github.com/openclaw/openclaw/pull/125412)** — P0 级别的安全/兼容性修复，恢复外部 Tailscale 代理支持。
- **[#125256 [P2] fix(cli): let nested agent exec --timeout override the parent flag](https://github.com/openclaw/openclaw/pull/125256)** — 修复嵌套 agent exec 超时参数继承问题。
- **[#123356 [P2] improve(control-ui): stage slash command arguments in the composer](https://github.com/openclaw/openclaw/pull/123356)** — UI 体验改进，支持在 composer 中暂存斜杠命令参数。

### 背后的诉求

- **稳定性焦虑**：多个高评论 Issue 指向核心功能不可用（编码 Agent 挂起、gemini 报错、Codex CPU 风暴），用户对回归问题高度敏感。
- **长上下文/长思考模型适配**：流式超时、上下文膨胀、静默压缩失败等问题的讨论背后，是对新一代长推理模型支持的迫切需求。
- **可观测性被高频提及**：从 dev agent 行为追踪（#77598）到插件 hooks 缺少 trace 上下文（#50291），再到任务状态持久化（#52640），社区明显希望 OpenClaw 提供更完善的可观测性能力。

---

## Bug 与稳定性

> 标签说明：`🐚 platinum hermit` 最高严重度，依次为 `🦞 diamond lobster`、`🦐 gold shrimp`、`🦪 silver shellfish`、`🌊 off-meta tidepool`、`🧂 unranked krab`。

### 🔴 严重问题（P0/P1 + 高影响）

1. **[#70903 [P0] Persistent file-based provider cooldown blocks user for hours after billing recovery](https://github.com/openclaw/openclaw/issues/70903)** — 严重 UX 缺陷：402 账单错误后，冷却时间戳持久化到文件，用户充值后仍被长时间封锁。**无 fix PR**。

2. **[#91009 [P1] Codex PreToolUse hook relay spawns CPU-bound processes, stalls Gateway RPC](https://github.com/openclaw/openclaw/issues/91009)** — Codex 钩子进程 CPU 占用 100% 以上，建议排查 hook 执行机制。**无 fix PR**。

3. **[#62505 [P1] Coding Agent never completes anything](https://github.com/openclaw/openclaw/issues/62505)** — 核心编码场景回归，自 2026.4.2 起失效。**无 fix PR**，需优先定位。

4. **[#38327 [P1] "Cannot convert undefined or null to object" with Gemini 3.1 Pro Preview](https://github.com/openclaw/openclaw/issues/38327)** — 13 天未解决的高优回归。**无 fix PR**。

5. **[#96834 [P1] WhatsApp 1:1 inbound image wedges main lane ~3min](https://github.com/openclaw/openclaw/issues/96834)** — 多模态消息阻塞会话主通道，已被标签 `clawsweeper-recovery-stuck` 标记。**无 fix PR**。

6. **[#78493 [P1] sudo openclaw update can create mixed ownership, then doctor overwrites config](https://github.com/openclaw/openclaw/issues/78493)** — macOS 权限混乱导致配置被覆盖，存在数据损坏风险。**无 fix PR**。

### 🟠 中等问题（P1/P2）

7. **[#97616 [P1] OpenClaw leaks unreaped hook/tool child processes](https://github.com/openclaw/openclaw/issues/97616)** — 僵尸进程累积导致运行时性能退化。**无 fix PR**。

8. **[#53408 [P1] Write/exec tool parameters silently dropped after long conversations](https://github.com/openclaw/openclaw/issues/53408)** — 长对话后工具参数丢失，破坏核心工具调用链路。**无 fix PR**。

9. **[#53540 [P1] "Network connection lost" when tool call params are large](https://github.com/openclaw/openclaw/issues/53540)** — 工具参数生成延迟超过请求超时，误报断网。**无 fix PR**。

10. **[#71689 [P1] Tasks registry restore fails on malformed SQLite image](https://github.com/openclaw/openclaw/issues/71689)** — SQLite 损坏导致 Gateway 启动失败。**无 fix PR**。

11. **[#45224 [P1] Playwright assertion error crashes Gateway](https://github.com/openclaw/openclaw/issues/45224)** — 未捕获的断言异常导致整个进程退出。

### 已有修复 PR 的问题（亮点）

- **[#125302 fix(agents): stop silent compaction failures](https://github.com/openclaw/openclaw/pull/125302)** — 对应静默压缩失败问题（community 关注点）。
- **[#123228 fix(ai): keep sessions usable with malformed reasoning history](https://github.com/openclaw/openclaw/pull/123228)** — 修复持久化 reasoning 历史损坏导致后续 turn 全部失败的问题。
- **[#125432 fix(matrix): keep user ID authorization case-sensitive](https://github.com/openclaw/openclaw/pull/125432)** — 修复 Matrix 用户 ID 大小写折叠导致的越权风险（安全相关）。
- **[#64546 fix: Mattermost interaction token forgeable via hardcoded HMAC](https://github.com/openclaw/openclaw/pull/64546)** — 修复 Mattermost 扩展中硬编码 HMAC 密钥导致 token 可伪造的安全漏洞。
- **[#120900 / #116489 feat(security): install policy warning acknowledgement（已关闭）](https://github.com/openclaw/openclaw/pull/120900)** — 安装策略警告确认，安全加固闭环。

> **稳定性总结**：今日无新增 P0 级问题，但大量 P1 问题仍处于待修状态，特别是 **#70903（provider 冷却机制）** 和 **#91009（Codex CPU 风暴）** 两个高影响问题均无对应 fix PR。值得肯定的是，security 方向的修复/加固（Matrix 大小写、Mattermost 硬编码、安装策略确认）正在稳步推进。

---

## 功能请求与路线图信号

### 高潜力功能请求（来自 Issues）

1. **[#60572 Multi-Slot Memory Architecture](https://github.com/openclaw/openclaw/issues/60572)**（👍 3，P2）— 将单一 memory 槽位拆分为多用途记忆槽，支持不同记忆层使用不同 provider。有相关 PR 链接（`linked-pr-open`），**可能已进入开发阶段**。

2. **[#63990 Multi-index embedding memory with model-aware failover](https://github.com/openclaw/openclaw/issues/63990)**（P3）— 多索引嵌入记忆 + 模型感知故障切换，解决混合向量空间问题的生产级方案。

3. **[#71058 Support multiple Azure/Teams bots on a single Gateway](https://github.com/openclaw/openclaw/issues/71058)**（P2）— 多 Teams 机器人支持，面向企业客户的多租户需求。

4. **[#67413 Per-agent dreaming configuration](https://github.com/openclaw/openclaw/issues/67413)**（👍 5，P2）— 按 agent 配置记忆"做梦"（dreaming）频率/开关，解决多 workspace 同时运行时内存峰值问题。

5. **[#56781 Fallback model chain for compaction and LCM summaryModel](https://github.com/openclaw/openclaw/issues/56781)**（P2）— 为压缩和 LCM 摘要模型增加 fallback 链，避免单模型限流时静默失败。

6. **[#42840 MathJax/LaTeX support in Control UI](https://github.com/openclaw/openclaw/issues/42840)**（👍 10，P3）— 呼声极高的 UI 功能，虽为 P3 但点赞数最高。

7. **[#45758 Support YAML as config file format](https://github.com/openclaw/openclaw/issues/45758)**（👍 2，P3）— YAML 配置支持，提升可读性与运维友好度。

### 已有 PR 对应信号

- **[#123356 improve(control-ui): stage slash command arguments in the composer](https://github.com/openclaw/openclaw/pull/123356)** — 对应 UI 改进方向仍在作者手中（`waiting on author`）。
- **[#125395 fix(ui): make Guardian review activity subtle](https://github.com/openclaw/openclaw/pull/125395)** — UI 噪音优化，降低 Guardian 审查横幅的干扰性。

---

## 用户反馈摘要

### 真实痛点

1. **中文用户表达强烈不满（#51429）**：
   > "看起来有人把工作路径 hardcode 进代码里而且居然被合并发布了……这位 wangtao 是谁？"
   
   反映开发流程中缺少基本的代码审查，用户体验严重受损。

2. **长时间等待与删除重装无果（#75782）**：
   > "Auth stage 无论 OAuth 状态如何同步阻塞 10–15 秒……删除所有 OAuth 配置后依然如此"

---

## 横向生态对比

# OpenClaw / Hermes / OpenHands SDK / Pi / LiteLLM 横向对比分析报告（2026-08-18）

> 说明：Temporal 数据未提供，本次不纳入对比；LiteLLM 为 AI 网关/代理层，非终端智能体，作为生态基础设施一并参考。

## 1. 生态全景

个人 AI 助手/自主智能体开源生态正处于**高活跃、高积压、高期待**的快速演进期。头部项目（OpenClaw、Hermes、LiteLLM）单日 Issue + PR 更新总量均达数百条级别，社区参与热情极高，但大量 P0/P1 级缺陷长期无人认领、数百条 PR 等待合并，核心维护者的审查吞吐能力已成为生态瓶颈。与此同时，长上下文/长思考模型的普及正系统性冲击现有架构——多个项目同时暴露压缩失效、流式超时、内存泄漏等问题，说明基础设施尚未完全适配新一代模型。安全加固和可观测性建设需求在多项目中同步涌现，成为下一阶段竞争的关键分水岭。整体态势可概括为：**社区先行、维护滞后、架构承压、安全与可观测性正在补课**。

## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | Release | 合并/关闭 PR | 健康度评估 |
|---|---|---|---|---|---|
| **OpenClaw** | 500（489 新开/活跃，11 关闭） | 500（406 待合并，94 合并/关闭） | 无 | 94 | 🟡 **高活跃 + 高积压**：社区热度爆表，但维护瓶颈显著，大量核心修复（压缩、Provider 冷却、Codex CPU）尚无对应 fix PR |
| **Hermes Agent** | 500（396 新开/活跃，104 关闭） | 500（404 待合并，96 合并/关闭） | v0.20.3 补丁版 | 96 | 🟡 **快速迭代 + 大量 bug 存量**：发布节奏稳定，桌面端/Bot 功能迭代积极，但 Debian 安装失败、Windows 更新锁死、secrets 泄漏等 P1 问题仍待解 |
| **OpenHands SDK** | 5（全部开放） | 19（14 待合并，5 合并） | 无 | 5 | 🟢 **小体量 + 高响应**：2 个 high bug 当日修复，核心架构修复（状态一致性）已合入，项目健康度良好 |
| **Pi** | 143（20 新开，123 关闭） | 34（9 待合并，25 合并） | 无 | 25 | 🟢 **小步快跑 + 消化良好**：今日关闭 rate 约 86%，合并集中在 AI 兼容性、扩展系统、TUI 稳定性，属于精干型维护节奏 |
| **LiteLLM** | 104（77 新开/活跃，27 关闭） | 297（223 待合并，74 合并） | 无 | 74 | 🟡 **功能迭代与深水区修复并存**：批量管理与计费修复持续推进，但预算绕过（#26672）、OOM（#25219）等 3 个月以上未解决的严重问题形成风险 |

## 3. OpenClaw 在生态中的定位

OpenClaw 是当前生态中**社区规模最大、功能覆盖面最广**的通用个人 AI 助手平台。与同类相比：

- **优势**：单日 500 Issue / 500 PR 的活跃度遥遥领先，是 Hermes（同为全功能助手）的约 2 倍体量。覆盖多平台渠道（Matrix、WhatsApp、Teams、Mattermost、Codex 集成）及 CLI/UI/Gateway 三层架构，生态广度无出其右。安全加固推进扎实（安装策略确认闭环、Mattermost HMAC 修复、Matrix 越权修复），显示对供应链安全的重视程度。
- **技术路线差异**：走**全平台 + 插件化**的综合路线，强调多渠道接入（聊天、IDE、CLI）和代理行为可观测性（dev agent 行为追踪、Provider 冷却、GPU/worker 管理）。相比 Hermes 的重桌面端 Bot UX、Pi 的终端优先体验、OpenHands SDK 的开发者组件定位，OpenClaw 更接近"个人 AI 的操作系统"。
- **社区规模对比**：Issue/PR 讨论深度和标签密度（P0/P1/maintainer/merge-risk 多标签叠加）显著高于其他项目，但这也意味着更重的维护负担——0 新版本发布、大量 P1 无 fix PR，是其当前最大隐忧。

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **长上下文压缩与流式超时** | OpenClaw（#125302 静默压缩失败、#68596 流式看门狗）、Pi（#6879 压缩阈值越过 100% 窗口）、OpenHands（#4515 订阅 LLM 冷凝器失效）、Hermes（#83390 DeepSeek 标题生成 400） | 新一代长推理模型（GPT-5.x、DeepSeek、Gemini 3.x）正在击穿现有压缩/超时机制，需系统级重构而非打补丁 |
| **可观测性与追踪** | OpenClaw（#77598 dev agent 行为追踪、#91009 CPU 风暴排查）、Hermes（Skills 索引告警）、Pi（新增 `session_compact_failed` 事件）、LiteLLM（用量/成本追踪） | 社区对"代理在做什么、卡在哪、为什么失败"的可见性需求已成为刚需 |
| **安全与密钥隔离** | OpenClaw（安装策略确认、Mattermost 硬编码、Matrix 大小写）、Hermes（#82936 secrets 跨 Profile 泄漏）、OpenHands（#4506 API Key 脱敏） | 多渠道/多 Profile 场景下的密钥管理、越权防护、供应链安全正在成为共同底线 |
| **模型路由与混合编排** | Pi（Anthropic refusal 回退、thinking budget 泛化）、OpenHands（#3673 ask_oracle、#4492 read-at-use provider）、LiteLLM（复杂度路由、fallback 语义）、OpenClaw（#56781 fallback 模型链） | 多模型协同、故障切换、成本感知路由开始从"增强功能"变为"基础能力" |
| **插件/扩展系统** | OpenHands（#4452 插件命名空间）、Pi（嵌套 skill 修复、扩展生命周期事件）、OpenClaw（安装策略确认）、Hermes（Skills 索引降级） | 插件生态的标准化、生命周期管理、安全审查成为各项目竞争的新前线 |
| **企业级部署** | OpenHands（#4519 Kubernetes 原生 workspace）、OpenClaw（#71058 多 Teams bot）、LiteLLM（K8s OOM、Azure、Bedrock）、Hermes（可插拔 SessionDB） | 从个人开发者走向企业内部基础设施是多项目共有的演进方向 |

## 5. 差异化定位分析

| 项目 | 定位 | 目标用户 | 核心架构特征 |
|---|---|---|---|
| **OpenClaw** | 全功能个人 AI 助手平台 | 个人/专业用户、多平台使用者 | 三层架构（CLI/UI/Gateway）+ 插件系统，强调多平台接入与生态广度 |
| **Hermes Agent** | 桌面端优先的 AI 助手 | 桌面重度用户、Bot Chat 场景 | Electron 客户端 + Profile 体系 + Bot 会话管理；桌面端体验打磨最深入 |
| **OpenHands SDK** | 智能体开发框架 | 开发者、AI 应用团队 | 以 SDK 为核心，提供 workspace、事件系统、插件机制；刚从 agent-server 中独立出来，架构最现代 |
| **Pi** | 终端优先的极简智能体 | 高级用户、TUI/CLI 爱好者 | 单文件 Go 二进制 + 终端渲染 + 深度 AI 提供商兼容；追求极简与性能（Pi 是这些项目里唯一一个轻量级的） |
| **LiteLLM** | AI 网关/接入层 | 平台团队、后端工程师 | 代理层架构，300+ provider 兼容、预算控制、guardrails、成本核算；是上述助手类项目的"基础设施" |

## 6. 社区热度与成熟度

**第一梯队：超级活跃 + 维护承压**（OpenClaw、Hermes）

两项目均达到 GitHub 单日更新量上限（500/500），但都没能完全消化涌入的贡献。两者都处于"快速迭代 vs 稳定性欠账"的矛盾期：OpenClaw 大量 P1 无 fix PR、Hermes 有平台兼容性反复，**质量巩固阶段尚未到来**。

**第二梯队：稳健迭代 + 突出重点**（LiteLLM）

日更新量虽不及头部但体量可观（297 PR），功能推进（批次管理、FLUX 3、复杂度路由）与历史 bug 修复并行。问题是预算绕过、OOM 等严重问题悬置过久，影响生产信任度。

**第三梯队：精干健康 / 快速成长**（Pi、OpenHands）

Pi 呈"小步快跑 + 精准补漏"节奏，合并率高、关闭率高，项目健康度最好；OpenHands SDK 体量虽小但**典型的高质量维护范式**——两个 high bug 当天修复、架构级修复（#4440 状态一致性）快速合入，属于从 0 到 1 阶段但工程纪律极佳的项目。

**成熟度结论**：OpenClaw 和 Hermes 社区规模遥遥领先，但**成熟度反而不及 Pi 和 OpenHands**——后者在响应速度、合并效率、质量把控上表现更优，说明"社区规模大"与"项目健康"并非线性关系。

## 7. 值得关注的趋势信号

**① 长上下文模型正在引发系统级架构重构**
压缩失效、流式超时、上下文膨胀在 OpenClaw、Pi、OpenHands 中同时爆发，这不是单个 bug 而是架构与新一代模型不匹配的系统性信号。对开发者的参考价值：**在设计新智能体时，应将上下文压缩/摘要作为一等公民考虑**，而非后期补救；可借鉴 Pi 的 append compaction、OpenHands 的 Condenser 模型等探索。

**② 可观测性成为智能体开发的基础设施**
从 OpenClaw 的 dev agent 行为追踪、Hermes 的 Skills 索引告警到 Pi 的 `session_compact_failed` 事件，社区对运行时透明度的需求已经非常明确。参考价值：**智能体产品应当内置轨迹回放、事件流、性能仪表盘**，否则面对长会话和复杂行动链时用户将"盲人摸象"。

**③ 安全加固从"加分项"变为"入场券"**
Hermes 的 secrets 跨 Profile 泄漏、OpenClaw 的 Matrix 越权、LiteLLM 的健康检查端点泄露密钥、OpenHands 的 API Key 脱敏——安全问题正从单点出现变为普遍挑战。参考价值：**多 Profile/多租户/多渠道场景下的密钥隔离和权限边界是必须提前设计的架构决策**，而非事后修复。

**④ 前端（智能体）与基础设施（网关）分工清晰化**
OpenClaw、Hermes、Pi、OpenHands 在上层竞争智能体体验，LiteLLM 在下游默默承担模型路由、

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-18

## 1. 今日速览

过去 24 小时项目保持高活跃度：共更新 500 条 Issue（新开/活跃 396，关闭 104）和 500 条 PR（待合并 404，合并/关闭 96），并发布了 v0.20.3（v2026.8.16.2）补丁版本（汇总 v0.20.2 后约 125 个 PR）。今日社区热度集中于安装/更新流程回归（Debian 安装失败、Windows 更新锁死）、桌面端 CPU 空转与 Bot Chat 会话管理问题，以及 Skills 索引持续降级的自动化告警。安全相关 Issue（跨 Profile 密钥泄漏）和大量 P1 级 Bug 的出现表明项目在快速迭代中对平台兼容性与隔离性仍存在压力。整体来看，项目迭代节奏快、社区参与积极，但待合并 PR 积压超 400 条，合并吞吐需要关注。

## 2. 版本发布

**v2026.8.16.2 / Hermes Agent v0.20.3**（2026-08-16 发布）

- **性质**：Patch 补丁版，将 v0.20.2 之后约 125 个 PR 打包为稳定 tag，面向下游 Docker 镜像、托管部署与新安装用户。
- **内容**：未提供逐条 changelog，主要包含 bugfix 与稳定性收编。
- **破坏性变更**：Patch 版本，预计无破坏性变更。
- **迁移注意**：保持常规升级路径即可；若为 Docker 或托管部署，建议跟踪镜像标签更新。[Release 链接](https://github.com/NousResearch/hermes-agent/releases)

## 3. 项目进展

今日合并/关闭的 PR 集中在桌面端、Bot 模式、Session 状态一致性及文档方向：

- **桌面端 Bot 面板全面修复**（闭环了此前多个反复）：[#88690](https://github.com/NousResearch/hermes-agent/pull/88690) 合并，点击 Bot 始终打开固定的 canonical Bot Chat，pin 不再因瞬时失败丢失；此前 [#88148](https://github.com/NousResearch/hermes-agent/pull/88148)、[#88292](https://github.com/NousResearch/hermes-agent/pull/88292) 分别修复 intro 失败后 pin 被清除、roster 预览与实际打开会话不一致的问题。
- **跨机器 Bot DM 打通**： [#88678](https://github.com/NousResearch/hermes-agent/pull/88678) 合并，远程 @mention 能进入接收方固定的 canonical Bot Chat，并支持回复中继，补齐了上一步仅完成投递的短板。
- **Profile 切换期间 404 不再误删会话**： [#88699](https://github.com/NousResearch/hermes-agent/pull/88699) 合并，中间态 404 会等待切换完成而非跳转空白聊天。
- **评估能力建设**：[#88663](https://github.com/NousResearch/hermes-agent/pull/88663) 将 PR #81958 的 Browser Use 204 次 A/B benchmark 转为可复跑的 `evals/browser_use/`。
- **文档**：[#88708](https://github.com/NousResearch/hermes-agent/pull/88708) 补充 `profiles.list` 的 `preferred_session_ids` 用法（随 #88690 上线）。

这些改动集中打磨桌面端与会话归属一致性，说明 Bot Mode 正在被积极推向稳定。

## 4. 社区热点

| 排名 | Issue/PR | 评论数 | 核心诉求 |
|---|---|---|---|
| 1 | [#66616 Skills 索引过期/降级](https://github.com/NousResearch/hermes-agent/issues/66616) | 47 | 自动化探针 24h 超时阈值触发告警，索引 29.8h 未更新，docs 站点依赖该索引 |
| 2 | [#84834 Webhook Feature Package 修复元问题](https://github.com/NousResearch/hermes-agent/issues/84834) | 17 | 社区发起的 5×2×3 全链路 webhook 修复追踪 |
| 3 | [#23717 可插拔 SessionDB Provider RFC](https://github.com/NousResearch/hermes-agent/issues/23717) | 17 (👍7) | SQLite 共享导致 `git pull` 与运行中 Agent 互锁，呼吁 PostgreSQL/MySQL 支持 |
| 4 | [#73082 桌面端 Renderer 空转 100% CPU](https://github.com/NousResearch/hermes-agent/issues/73082) | 14 | Electron 空闲时持续 50–90% CPU，macOS 报告最高能耗 |
| 5 | [#83390 DeepSeek 标题生成 HTTP 400](https://github.com/NousResearch/hermes-agent/issues/83390) | 13 | DeepSeek 不支持 `response_format`，`auxiliary.title_generation` 直接失败 |
| 6 | [#82936 多 Profile 下 secrets 泄漏到子进程](https://github.com/NousResearch/hermes-agent/issues/82936) | 13 | `multiplex_profiles` 开启时，默认 Profile 的 secrets 被二级 Profile 的 terminal/kanban 看到 |

**分析**：讨论热度最高的两类诉求分别是“基础设施可靠性”（索引、SessionDB、Webhook）和“资源占用/隔离安全”。其中 #23717 的 7 个 👍 表明社区对 SQLite 单文件方案的扩展性不满已久，是潜在架构级改进方向。

## 5

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目日报 — 2026-08-18

## 1. 今日速览

过去24小时项目处于**高活跃度**状态：5条新 Issue 全部为开放状态，其中2条为 `priority:high` 的 Bug（生命周期锁死锁、订阅LLM冷凝器失效），且均已迅速获得对应修复 PR（#4513、#4517），说明维护团队响应及时。PR 方面共19条动态，其中14条仍在待合并状态，5条已合并/关闭，覆盖持久化状态修复、API密钥脱敏、依赖更新等多个方向。值得注意的是，今日新增的 Kubernetes workspace 功能（Issue #4519 + PR #4516）和插件命名空间映射（Issue #4452 + PR #4496）均形成了完整的"问题→实现"闭环，显示项目路线图执行力度较强。无新版本发布。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日有5个 PR 合并/关闭，其中3个为功能性合并，2个为依赖/维护更新：

| PR | 内容 | 影响 |
|---|---|---|
| [#4440](https://github.com/OpenHands/software-agent-sdk/pull/4440) [Merged] | 将 `base_state.json` 设为 agent 状态的唯一事实源，消除 `meta.json` 双写不一致问题 | **核心架构修复**。SDK 与 agent-server 之间长期存在的状态同步隐患得到根治，降低了崩溃后恢复时状态错乱的风险 |
| [#3503](https://github.com/OpenHands/software-agent-sdk/pull/3503) [Merged] | 为 `AgentSettingsBase` 添加公共 `from_persisted()` 入口，支持各设置变体从历史数据加载 | 解决了持久化设置迁移中"旧 v0/v1/v2 载荷无法还原具体类型"的问题，对长期运行或升级场景友好 |
| [#4465](https://github.com/OpenHands/software-agent-sdk/pull/4465) [Merged] | 让 `finish` 工具携带任务结果信息 | 改进 agent 完成任务的闭环，便于上层应用感知最终状态 |
| [#4506](https://github.com/OpenHands/software-agent-sdk/pull/4506) [Merged] | 从 `validate_profile` 错误响应和日志中脱敏 API Key | 安全加固，防止密钥在错误消息中泄露 |
| [#4347](https://github.com/OpenHands/software-agent-sdk/pull/4347) [Merged] | 依赖更新：`mcp` 1.26.0 → 1.28.1 | 例行依赖维护，获得上游修复与弃用告警 |

整体来看，项目在**数据一致性**（#4440）、**安全加固**（#4506）、**可扩展性**（#3503）三个维度上均有推进，健康度良好。

---

## 4. 社区热点

今日讨论最活跃/值得关注的 Issue：

- **[#4452](https://github.com/OpenHands/software-agent-sdk/issues/4452) — Agent Plugins: client extension namespace mapping**  
  评论数：2 | 状态：Needs Design  
  这是通往 #4405 的架构级设计讨论。核心争议点在于命名空间选择（`io.openhands` vs `dev.openhands`），目前已出现对应 PR [#4496](https://github.com/OpenHands/software-agent-sdk/pull/4496) 使用 `dev.openhands` 命名空间实现。该讨论持续一周（创建于8/10，更新于8/17），说明社区对插件扩展机制的重视程度高，且涉及兼容性决策，需要充分论证。

- **[#4515](https://github.com/OpenHands/software-agent-sdk/issues/4515) — Condenser disabled for subscription LLMs**  
  评论数：1 | 状态：ready-for-dev  
  直指订阅制 ChatGPT LLM（如 `openai/gpt-5.6-sol`）在 `ContextWindowExceededError` 之前从不触发上下文压缩的问题，严重影响长对话场景的生产使用。该 Issue 发布后**当天即被修复**（见 PR #4517），体现了项目对高优 bug 的快速响应。

其余 Issue 评论数均为1，整体讨论热度集中在上述两个话题。

---

## 5. Bug 与稳定性

今日报告了3个 Bug（按严重程度降序排列）：

| 严重程度 | Issue | 描述 | 修复状态 |
|---|---|---|---|
| 🔴 High | [#4514](https://github.com/OpenHands/software-agent-sdk/issues/4514) — Lifecycle lock deadlock: thread-pool exhaustion blocks all event loading | `_get_or_load_event_service` 持锁后调用 `asyncio.to_thread`，当默认线程池耗尽（大量 worker 卡在慢 I/O 上）时，事件加载会无限期阻塞——**生产环境级故障**，可导致会话完全不可恢复 | 已有测试 + 修复 PR [#4513](https://github.com/OpenHands/software-agent-sdk/pull/4513)（test + fix 同 PR） |
| 🔴 High | [#4515](https://github.com/OpenHands/software-agent-sdk/issues/4515) — Condenser disabled for subscription LLMs | 订阅制 LLM 的冷凝/压缩逻辑调用错误的 API endpoint，导致上下文窗口超限后直接 `ContextWindowExceededError` 失败，而非自动压缩 | 已修复：[#4517](https://github.com/OpenHands/software-agent-sdk/pull/4517) 统一 `complete()` 分发路径 |
| 🟢 Low | [#4520](https://github.com/OpenHands/software-agent-sdk/issues/4520) — `parse_extension_source` duplicates `.git` suffix in GitHub shorthand | `github:owner/repository` 缩写扩展时无条件追加 `.git`，若仓库名本身已带 `.git`（如 `github:owner/repo.git`）会得到 `repo.git.git` | 暂无修复 PR，待 `ready-for-dev` |

另外，PR 中还有一个稳定性相关修复：#4512 阻止 `cache_control` 在缓存被禁用时仍被发射（[#4512](https://github.com/OpenHands/software-agent-sdk/pull/4512)，open）。

---

## 6. 功能请求与路线图信号

今日有2个新功能请求，且均已出现或已有对应实现：

1. **Kubernetes 后端 Workspace** — Issue [#4519](https://github.com/OpenHands/software-agent-sdk/issues/4519)  
   用户 @aleks-stefanovic 提出为已在 k8s 上运行团队提供原生工作区方案，避免依赖 Docker 或托管运行时。**同日 PR [#4516](https://github.com/OpenHands/software-agent-sdk/pull/4516) 即提交了 `AgentSandboxWorkspace` 实现（基于 `kubernetes-sigs/agent-sandbox`）**，并经 kind + GKE 验证。这表明 Kubernetes 支持是即将引入的重量级能力，值得关注其 review 进度。

2. **Agent Plugins 客户端扩展命名空间映射** — Issue [#4452](https://github.com/OpenHands/software-agent-sdk/issues/4452)  
   为 OpenHands 的 Claude-Code-origin 概念（`commands/`、`hooks/` 等）建立自有反域名命名空间，属于插件生态的重要架构决策。PR [#4496](https://github.com/OpenHands/software-agent-sdk/pull/4496) 已实现 `dev.openhands` 命名空间下的映射。

此外，两个体现了路线图趋势的既有 PR 值得关注：
- **[#3673](https://github.com/OpenHands/software-agent-sdk/pull/3673) — `ask_oracle` 工具**（6/11 提交，持续更新中）：让 agent 在遇到困难时向更强大的 LLM 求助，已有人工验证，等合入。
- **[#4492](https://github.com/OpenHands/software-agent-sdk/pull/4492) — read-at-use LLM provider connections**：为模型路由提供轻量级、向后兼容的 provider 连接方案。

以上共同指向的方向：**混合模型编排、插件化扩展、Kubernetes 部署支持**将成为接下来 SDK 的三大关键词。

---

## 7. 用户反馈摘要

- **长对话场景痛点**（[#4515](https://github.com/OpenHands/software-agent-sdk/issues/4515)）：用户 @neubig 报告使用 ChatGPT 订阅模型（Codex auth）进行长对话时，语境压缩从未触发，最终必然撞上上下文窗口上限而失败。反馈关键词：**"never trigger context compression"**。这暴露了订阅模型与传统 API 在端点/认证流程上的差异未在 condenser 中得到映射。

- **生产稳定性担忧**（[#4514](https://github.com/OpenHands/software-agent-sdk/issues/4514)）：同一用户提供的死锁复现场景展示了线程池耗尽时整个会话事件加载被阻塞的"全站不可用"风险。用户明确指出问题发生在 `asyncio.to_thread` 排队且无法取消的场景，属于真实生产环境的高危隐患。

- **企业级部署需求**（[#4519](https://github.com/OpenHands/software-agent-sdk/issues/4519)）：用户 @aleks-stefanovic 表示团队已运行 k8s，希望 agent sandbox 能原生跑在 k8s 上而不是绕道 Docker/托管运行时。这是一个明确的"开源项目被企业内部基础设施接纳"的信号，说明 SDK 正在获得 B 端用户。

- **小瑕疵反馈**（[#4520](https://github.com/OpenHands/software-agent-sdk/issues/4520)）：用户 @yifanxiong272 报告 GitHub shorthand 展开时的 `.git` 重复问题，虽为 low 级，但属于日常使用中容易踩到的小坑，建议尽快打补丁。

---

## 8. 待处理积压

以下为值得维护者关注的长期未合并/未响应条目：

| 条目 | 状态 | 时长 | 建议 |
|---|---|---|---|
| [#3673](https://github.com/OpenHands/software-agent-sdk/pull/3673) — `ask_oracle` 工具 | OPEN，`review-this` 标记 | **自 6/11 起至今超过2个月** | 功能已完成并有人工验证，建议安排 reviewer 优先审阅，否则功能价值随 LLM 能力迭代递减 |
| [#4437](https://github.com/OpenHands/software-agent-sdk/pull/4437) — 添加 `claude-fable-5` 模型 | OPEN，8/9 创建 | 约9天 | 模型选择器缺失新模型会影响 ACP 用户的使用体验，建议快速合入 |
| [#4497](https://github.com/OpenHands/software-agent-sdk/pull/4497) — workspace 默认 LLM 从活跃 profile 解析 | OPEN | 4天 | 修复静默模型/凭据漂移，属质量问题，建议排期合入 |
| [#4488](https://github.com/OpenHands/software-agent-sdk/pull/4488) — crash recovery 中断分支修复 | OPEN | 4天 | 已带无 mock 的测试用例，可考虑在下一迭代优先合并 |

---

**总结**：OpenHands SDK 在过去24小时展现出良好的项目健康度——两个 high 级 bug 均当天修复、架构级功能（Kubernetes workspace、插件命名空间）快速推进到实现阶段、安全加固随手合入。需要关注的是 #3673 等 PR 的积压时间过长，以及 #4520 `.git` 重复这类小 bug 的清理节奏。整体评级：**活跃且健康** 🟢

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-18

> 数据窗口：2026-08-17（过去 24 小时） | 数据来源：github.com/earendil-works/pi

---

## 1. 今日速览

项目保持高强度迭代节奏：过去 24 小时产生 143 条 Issue 更新（其中 123 条关闭、20 条新开活跃）和 34 条 PR 更新（25 条合并/关闭、9 条待合并）。Issue 关闭/更新比例约 86%，说明维护者响应迅速、积压消化良好。本期无新版本发布，但 PR 合并集中在 AI 提供商兼容性、扩展系统生命周期事件、TUI 渲染稳定性三大方向，且多为对已有高优 Bug 的定向修复（如 #8017、#6479、#7994），整体呈"小步快跑 + 精准补漏"状态。

---

## 3. 项目进展

### 3.1 AI 提供商与模型目录（合并 5 项 PR）

| PR | 内容 | 关联 Issue |
|---|---|---|
| [#8258](https://github.com/earendil-works/pi/pull/8258) | **Anthropic refusal 回退支持**：当 API 返回 `stop_reason: "refusal"` 且伴随思维提取时，自动使用 `allowed_fallback_models` 元数据回退，修复压缩失败 | #8017 |
| [#8246](https://github.com/earendil-works/pi/pull/8246) | **openai-completions reasoning details 完整回传**：保留带签名的 `reasoning.text`/`reasoning.summary`，修复下次请求丢失推理详情的问题 | #7994 |
| [#8240](https://github.com/earendil-works/pi/pull/8240) | **Qwen Token Plan 目录统一**：`qwen-token-plan` 与 `qwen-token-plan-cn` 共用同一八模型文本目录（含 deepseek-v4-pro / v4-flash 新模型），独立版维持七模型 | #8194 |
| [#8275](https://github.com/earendil-works/pi/pull/8275) | **thinking token budget 字段泛化**：将 vLLM 的 `thinking_token_budget` 扩展至 SGLang（`thinking_budget`）与 llama.cpp（`thinking_budget_tokens`） | #7638 后续 |
| [#7173](https://github.com/earendil-works/pi/pull/7173) | 显示名重命名：`OpenCode Zen Go` → `OpenCode Go`，使 `pi --list-models` 与 provider 名一致 | #7157 |

### 3.2 扩展系统与生命周期（合并 3 项 PR）

- [#8255](https://github.com/earendil-works/pi/pull/8255)：修复 `~/.agents/skills/` 下嵌套的独立 Markdown skill（如 `third-party/child-skill.md`）被静默忽略的问题 — 修复 #6479
- [#8241](https://github.com/earendil-works/pi/pull/8241)：新增扩展可见的 `session_compact_failed` 事件，压缩失败不再只有内部 `compaction_end errors` — 修复 #8175
- [#8242](https://github.com/earendil-works/pi/pull/8242)：扩展示例从 `agent_end` 改用 `agent_settled`，避免在重试/压缩/follow-up 仍在进行时过早触发"done"状态 — 修复 #7350

### 3.3 TUI 与渲染稳定性（合并 2 项 PR）

- [#8253](https://github.com/earendil-works/pi/pull/8253)：当视口上方的工具结果更新时，不再整屏清空重绘，消除 10k+ 行长对话中的可见闪烁
- [#8249](https://github.com/earendil-works/pi/pull/8249，待合并)：主题切换后重算 Markdown 缓存前缀、启动头部与警告文本的 ANSI 颜色

### 3.4 实验性功能

- [#8120](https://github.com/earendil-works/pi/pull/8120)：新增**追加式压缩（append compaction）**，以 `PI_EXPERIMENTAL=1` 启用。复用活跃 system prompt、工具、上下文与路由会话，使压缩前缀能复用供应商 prompt 缓存；独立压缩仍为默认

---

## 4. 社区热点

### 🔥 最热 Issue：自动压缩失效（#6879，18 评论 / 17 👍）
[#6879](https://github.com/earendil-works/pi/issues/6879) 仍为打开状态，是当前社区关注度最高的单一问题。用户报告在 GPT-5.6-sol 上单个 agentic turn 运行超过 2 小时，footer 已越过压缩阈值并持续增长至超过 100% 上下文窗口，最终在 373k tokens 时被 API 拒绝才触发压缩。这暴露了压缩检查机制的可靠性缺陷，并直接推高使用成本，后续发出大量要求"每一步 agent 动作后都检查"的声音。建议优先排期。

### 👍 最多点赞：Linux XDG 规范（#534，39 👍 / 15 评论）
[#534](https://github.com/earendil-works/pi/issues/534)（config 目录位置不符合 XDG 规范）今日关闭。三个月来收获 39 个 👍，说明 Linux 用户对"配置落 `$HOME` 根目录"的强烈不满。关闭本身

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-18

## 1. 今日速览

过去24小时LiteLLM项目保持高活跃度：共更新104条Issue（新开/活跃77条，关闭27条）和297条PR（待合并223条，已合并/关闭74条），无新版本发布。开发侧以修复为主，集中在批次管理API（/v1/batches）、定价数据修正、流式成本核算等方面，同时有多个新功能PR（FLUX 3视频生成、自定义复杂度路由分层）进入待合并队列。社区讨论焦点集中在**预算控制绕过**（#26672）、**OOM内存泄漏**（#25219）和**GPT-5.4响应兼容性**（#25429）三个生产环境严重问题上，其中预算绕过和OOM问题已开放超过3个月未闭环，暴露了稳定性方面的隐忧。项目整体处于"功能迭代与深水区修复并行"的状态。

## 2. 版本发布

过去24小时无新版本发布。

## 3. 项目进展

今日无新版本产出，但合并/关闭的74条PR持续推动代码质量与功能修复，以下是值得关注的关键合并：

**API 正确性与兼容性**
- [fix(proxy): return 404 instead of 500 for unresolvable batch and file ids on /v1/batches](https://github.com/BerriAI/litellm/pull/37201)：将未知batch/file id的报错从500改为404，并修复了隐式openai fallback导致的误导性报错信息，改善了API语义。
- [fix: stop rust flag from leaking into upstream provider request bodies](https://github.com/BerriAI/litellm/pull/37218)：修复`rust: true`配置导致的400错误——该标志不再作为body字段发送给上游provider。
- [fix(streaming): track provider-reported cost when caller omits include_usage](https://github.com/BerriAI/litellm/pull/35013)：OpenRouter等流式请求在调用方未要求`include_usage`时，现在仍会保留usage-only chunk用于成本核算，修复了spend log显示$0的问题。

**成本与计费修复**
- [[MLI-8301] Fix Gemini 3.6 Flash promotional pricing](https://github.com/BerriAI/litellm/pull/37193)：修正Gemini 3.6 Flash宣传期定价过高的问题，应用Google当前introductory定价。
- [fix(pricing): add the azure gpt-realtime-2 family](https://github.com/BerriAI/litellm/pull/31565)：为Azure实时语音模型补充缺失的成本映射，实时图片输入将按独立费率计费。

**性能优化**
- [perf(guardrails): stop sending the conversation twice in the noma v2 payload](https://github.com/BerriAI/litellm/pull/36764)：Noma v2 guardrail扫描请求体不再重复发送整个会话，图像密集型请求减少约95%冗余字节。

**其他**
- [feat(shadow-eval): name the shadowed key in job responses and the UI headline](https://github.com/BerriAI/litellm/pull/37221)：shadow-eval功能现在会在UI和job响应中显示被采样的具体key名称。
- [revert: don't fix mcp scope authorization server issuer](https://github.com/BerriAI/litellm/pull/37220)：撤销了一个MCP授权server issuer的改动，保留原实现。

整体来看，项目在**批次管理、计费准确性和流式数据处理**三个方向上有实质性推进，同时修复了多个影响生产环境的参数泄漏和错误状态码问题。

## 4. 社区热点

过去24小时讨论最热烈的Issue集中在以下三个方向：

**① 生产事故与可靠性（评论最多）**
- [\[Bug]: chatgpt/gpt-5.4 returns empty final Responses output](https://github.com/BerriAI/litellm/issues/25429)（19条评论，4👍）：GPT-5.4配合ChatGPT订阅认证时，`responses()`输出为空，`completion()`桥接报"Unknown items"错误。该Issue来自4月，至今未解决，评论仍在更新。
- [\[Bug]: Budget enforcement bypassed in v1.82.3](https://github.com/BerriAI/litellm/issues/26672)（17条评论，4👍）：预算超限但未被拦截，直接影响成本控制，生产环境高风险。4月底上报，目前仍为OPEN状态。
- [\[Bug]: Pods get OOM Killed due to continous increase in memory](https://github.com/BerriAI/litellm/issues/25219)（14条评论，6👍）：升级到v1.82.0后持续内存增长导致OOM Kill，4月上报至今未关闭。

**② LLM Translation 兼容性**
- [\[Bug]: AnthropicException 400 - vector_store_ids: Extra inputs are not permitted](https://github.com/BerriAI/litellm/issues/23741)（13条评论，12👍）：通过LiteLLM转发到Anthropic时，`vector_store_ids`字段被Anthropic API拒绝。该Issue获得12个👍，是社区关注度最高的兼容性问题之一。

**③ 可观测性集成需求**
- [\[Feature]: Support Langfuse Python SDK v4](https://github.com/BerriAI/litellm/issues/24123)（9条评论，12👍）：用户要求解锁Langfuse v4 SDK，当前被`pyproject.toml`锁在v2。Langfuse官方人员也在相关Issue #33383中留言，说明两个SDK的升级需求已进入上游厂商视野。

**分析**：预算和内存问题是社区最关心的生产稳定性痛点，且长期未解决可能导致用户流失。LLM Translation层的字段透传错误和Langfuse集成滞后则反映了用户对**生态兼容性**的持续要求。

## 5. Bug 与稳定性

按严重程度排列（🔴=严重/影响生产，🟡=中等，🟢=低）：

**🔴 严重**
- [\[Bug]: Budget enforcement bypassed for key/user max_budget despite spend exceeding max_budget](https://github.com/BerriAI/litellm/issues/26672) — v1.82.3中新部署环境预算限制完全不生效。存在两个相关Issue（#27381、#34101），说明预算体系存在系统性缺陷。**无对应fix PR**。
- [\[Bug]: Pods get OOM Killed due to continuous increase in memory](https://github.com/BerriAI/litellm/issues/25219) — main-v1.82.0-stable镜像持续内存增长导致OOM。4月上报仍未解决。**无对应fix PR**。
- [\[Bug]: gammavariate: alpha and beta must be > 0.0 — adaptive_router 永久500](https://github.com/BerriAI/litellm/issues/35590) — 一个persisted的alpha/beta=0单元导致整个router永久500，不重启不恢复。**无对应fix PR**。

**🟡 中等**
- [\[Bug]: GET /health returns extra_headers and aws_session_token in plaintext](https://github.com/BerriAI/litellm/issues/36898) — 健康检查端点泄露敏感配置信息（extra_headers、aws_session_token），属于安全隐患。**无对应fix PR**。
- [\[Bug]: Bedrock CountTokens unsupported for Claude Opus 5/Sonnet 5 → token counts understated](https://github.com/BerriAI/litellm/issues/37102) — 不支持的模型静默返回低估的token数，影响计费准确性。**无对应fix PR**。
- [\[Bug]: Mid-stream fallback request includes assistant prefill block, breaks for fallback targets](https://github.com/BerriAI/litellm/issues/27967) — 流式中断后的fallback请求携带`prefix=True`的assistant预填充块，部分不支持`prefix=True`的目标模型会失败。**无对应fix PR**。

**🟢 较低（已有fix或近期修复）**
- [\[Bug]: Docs mention litellm.turn_on_message_logging, which doesn't exist](https://github.com/BerriAI/litellm/issues/37143) — 文档引用了不存在的API，低风险。**无对应fix PR**。
- [Fix "azure/gpt-audio-mini-2025-10-06" pricing entry](https://github.com/BerriAI/litellm/issues/37170) / [Fix "azure/gpt-audio-1.5-2026-02-23"](https://github.com/BerriAI/litellm/issues/37169) — 定价表条目错误，已有PR #31565围绕realtime家族定价处理中，可能覆盖部分问题。
- [\[Bug\]: service_tier=priority silently billed at default rate](https://github.com/BerriAI/litellm/issues/37046) — 已关闭，说明已有处理。

**今日修复的Bug（参考"项目进展"部分）**：batch/file 500错误（#37201）、rust flag泄漏（#37218）、OpenRouter流式成本丢失（#35013）。

## 6. 功能请求与路线图信号

**有明确PR支撑、可能进入下一版本的功能：**
- [feat(complexity_router): operator-defined tier sets for the LLM classifier](https://github.com/BerriAI/litellm/pull/37226) — 允许运维自定义复杂度路由的tier分层（不再硬编码SIMPLE/MEDIUM/COMPLEX/REASONING），方向性强，与现有自适应路由体系一脉相承。
- [feat(black_forest_labs): add FLUX 3 video generation](https://github.com/BerriAI/litellm/pull/37224) — 新增FLUX 3视频生成支持，补齐BFL在视频模态的空白。
- [feat(guardrails): track bedrock guardrail usage units per invocation](https://github.com/BerriAI/litellm/pull/37225) — 将Bedrock guardrail用量记入spend log，满足AWS成本审计需求。

**社区呼声高、值得关注的路线图信号：**
- [Support Langfuse Python SDK v4](https://github.com/BerriAI/litellm/issues/24123)（12👍）与[Upgrade Langfuse integration to v4 and v4 OTel ingestion](https://github.com/BerriAI/litellm/issues/33383)（6👍）：Langfuse官方人员已参与讨论，升级SDK是双向诉求，预计会进入近期迭代。
- [Support Azure AI Foundry Agents v2 (Responses API with agent_reference)](https://github.com/BerriAI/litellm/issues/25372)：来自微软生态用户，Responses API + agent_reference是Agent服务新范式。
- [Support time-based / peak-offpeak pricing](https://github.com/BerriAI/litellm/issues/31606)（5👍）：DeepSeek等厂商的分时段计费需求，对成本准确核算有明确价值。
- [Feature: Add provider Sglang](https://github.com/BerriAI/litellm/issues/13681)（15👍，已关闭）：该功能已关闭，可能已实现或转向其他方案。
- [Adaptive similarity threshold for valkey-semantic cache](https://github.com/BerriAI/litellm/issues/36124)：语义缓存的自适应阈值优化，属于基础设施体验改进。

## 7. 用户反馈摘要

**主要痛点（来自Issue评论）：**
- **预算控制失效是最大不满**：#26672、#27381等Issue反映，用户升级到新版本后预算防护如同虚设，可能导致不可控的云成本支出。有用户评论表示"部署到生产环境后才发现，需要立即回滚"。
- **升级引发内存问题**：#25219显示v1.82.x版本升级后出现持续内存增长，用户反馈"升级后Pod反复OOM，监控曲线呈持续上升趋势"，严重影响稳定性。
- **新模型支持滞后**：#25429（GPT-5.4）、#37102（Claude Opus 5/Sonnet 5）等Issue表明，用户对前沿模型的支持速度期待很高，但目前仍有响应格式和token计数等兼容性问题。
- **配置项失效/文档误导**：#37143反映文档中不存在的API配置，#16623反映config.yaml在OpenAPI spec中消失。用户需要花费大量时间排查文档与实现不一致的问题。
- **LLM translation字段透传不稳定**：#23741、#23841等Issue指出Anthropic/OpenAI之间的字段转换存在多个边界case。

**使用场景观察：**
- 不少用户使用LiteLLM作为**多provider网关**，尤其同时接入OpenAI、Anthropic、Azure、Bedrock等，对字段透传和计费准确性要求极高。
- 有用户（如#19769）在Kubernetes环境中通过

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*