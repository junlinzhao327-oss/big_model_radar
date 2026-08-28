# OpenClaw 生态日报 2026-08-28

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-28 04:05 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-28

## 1. 今日速览

过去24小时内，OpenClaw 项目收到 **500 条 Issue 更新**（新开/活跃 398，关闭 102）和 **500 条 PR 更新**（待合并 278，已合并/关闭 222），整体社区活跃度处于**高位**。当前正值 **2026.8.1 版本验证期**，beta 反馈和稳定性修复构成今日主线。值得关注的是，**会话状态一致性**（session-state）、**消息丢失**（message-loss）与**认证（auth-provider）问题**在 Issue 中占据突出比重，多个 P1 级问题持续被社区和 clawsweeper 机器人标记。好消息是约 10 个重要 PR 已进入"ready for maintainer look"或"needs proof"状态，其中包含会话压缩、auth 修复、Slack 与 UI 稳定性等关键改动，项目正在朝 2026.8.1 正式版稳步推进。🚀

---

## 2. 版本发布

**今日无新版本发布。**

当前验证中版本：[v2026.8.1-beta.3](https://github.com/openclaw/openclaw/releases/tag/v2026.8.1-beta.3)（见 issue [#125626](https://github.com/openclaw/openclaw/issues/125626)）。

---

## 3. 项目进展

### 关键 PR 进展汇总

| PR | 说明 | 状态 |
|---|---|---|
| [#131020](https://github.com/openclaw/openclaw/pull/131020) | **UI 修复**：peer-tab 删除后保留聊天可见性；修复 Control UI 多标签页下聊天预加载失效问题 | ✅ 已关闭 |
| [#123535](https://github.com/openclaw/openclaw/pull/123535) | **UI 性能**：避免侧边栏会话目录刷新风暴 | ✅ 已关闭 |
| [#131091](https://github.com/openclaw/openclaw/pull/131091) | **CI 增强**：增加 Crabbox PR 门禁的 admin-only 降级通道 | ✅ 已关闭 |
| [#128371](https://github.com/openclaw/openclaw/pull/128371) | **发布流程**：为 beta.3 聚焦验证证据授权 | ✅ 已关闭 |
| [#126424](https://github.com/openclaw/openclaw/pull/126424) | **消息投递修复**：将对话投递保持在 agent 绑定范围内（多 agent 场景），涉及 Discord/iMessage/Matrix/Slack/Telegram/Feishu 等全部渠道 | ✅ 已关闭 |
| [#123236](https://github.com/openclaw/openclaw/pull/123236) | **安全边界**：在 launch 边界传递已解析的 exec 权限（worker 不再默认以 full/off 重建 exec 工具） | 🟡 待合并 |
| [#130993](https://github.com/openclaw/openclaw/pull/130993) | **会话稳定性**：修复 Responses 会话在达到上下文限制前压缩（6 个同一管线修复，包括 replay 估算翻倍、丢失 coherent context boundary 等问题） | 🟡 待合并 |
| [#130986](https://github.com/openclaw/openclaw/pull/130986) | **会话修复**：修复 Activity 中参与者身份误归属问题 | 🟡 待合并 |
| [#131369](https://github.com/openclaw/openclaw/pull/131369) | **配置修复**：保留索引与整列表 agent 编辑（`config set`/`patch` 对 `agents.list` 生效但未写入 keyed roster） | 🟡 待合并 |
| [#131202](https://github.com/openclaw/openclaw/pull/131202) | **UI 修复**：停止截断侧边栏会话名册 | 🟡 待合并 |

**今日关闭的 3 个 PR 中，两个为 UI 稳定性修复，一个为 CI/发布流程改进；** 今日合并的 PR 大多为 UI 较小修复与流程类改进，核心稳定性 PR 仍处于待合并/待审查状态。

---

## 4. 社区热点

### 🔥 今日讨论最活跃的 Issue

| Issue | 评论数 | 核心诉求 |
|---|---|---|
| [#125626](https://github.com/openclaw/openclaw/issues/125626) — **2026.8.1 beta 反馈帖** | **21** | 测试者集中汇报 beta 问题 |
| [#48788](https://github.com/openclaw/openclaw/issues/48788) — **集中式 filename 编码工具** | **20** | 多编码 Content-Disposition 的架构级解决方案 |
| [#87744](https://github.com/openclaw/openclaw/issues/87744) — **Codex-backed Telegram 超时** | **18** | Telegram 的 Codex 回合永不达 terminal 状态 |
| [#115908](https://github.com/openclaw/openclaw/issues/115908) — **会话投影 livelock** | **14** | 持续写入下主线程被阻塞，所有渠道停摆 |
| [#87561](https://github.com/openclaw/openclaw/issues/87561) — **最终投递语义** | **13** | 定义跨渠道的持久最终回退投递语义 |

### 社区关注焦点分析

- **Beta 验证期集中反馈**：#125626 是该版本的核心反馈通道，社区围绕 2026.8.1-beta.3 的行为差异进行集中报道。
- **渠道投递可靠性与会话正确性持续占据核心讨论**：#87744、#87561、#106760、#131150（Slack DM 在 gateway 重启后被静默丢弃）等投递相关问题热度依旧。
- **架构级改进呼声**：#48788 提出中央化 filename 编码工具，已在 #48578 中解决 UTF-8/Latin-1 常见案例，但社区希望覆盖 Shift-JIS、EUC-KR、GB18030 等多编码场景——这说明项目已进入**多语言、多区域适配的深水区**。

---

## 5. Bug 与稳定性

### P1 级问题（按严重程度排序）

**🔴 会话阻塞 / 崩溃类**

1. **[#115908](https://github.com/openclaw/openclaw/issues/115908)** — 会话投影 reconcile 在持续写入下 livelock，阻塞主线程数秒，**波及所有渠道传输**。影响：session-state / crash-loop。⚠️ 暂无 fix PR。
2. **[#125344](https://github.com/openclaw/openclaw/issues/125344)** — memory-core 本地 embedding workers 与 codex app-servers **无 idle TTL 泄漏**，扼杀 gateway cgroup。⚠️ 暂无 fix PR。
3. **[#53008](https://github.com/openclaw/openclaw/issues/53008)** — 记忆压实阻塞主处理通道，bot 无响应 **10+ 分钟**。⚠️ 暂无 fix PR。

**🟠 消息丢失类**

4. **[#131150](https://github.com/openclaw/openclaw/issues/131150)** — 19 个 Slack 账号的 socket mode 下，**gateway 重启后所有 Slack DM 被静默丢弃**（`prepareSlackMessage` 返回 null）。标记 `clawsweeper:fix-shape-clear` + `queueable-fix`，⚠️ 暂无 fix PR。
5. **[#87744](https://github.com/openclaw/openclaw/issues/87744)** — Codex-backed Telegram 回合反复超时，永不达 `turn/completed`，**用户看不到最终回答**。⚠️ 暂无 fix PR。
6. **[#86215](https://github.com/openclaw/openclaw/issues/86215)** — Codex OAuth 刷新失败可使 agent **卡死数小时**，无警报、无 profile 轮换。⚠️ 暂无 fix PR。

**🟡 状态错误 / 回归类**

7. **[#126906](https://github.com/openclaw/openclaw/issues/126906)** — 拒绝 `write` 工具会**静默禁用记忆持久化**，且 agent 仍报告成功。⚠️ 暂无 fix PR（严重安全隐患）。
8. **[#126360](https://github.com/openclaw/openclaw/issues/126360)** — 显式多 agent 所有权下 `AgentSelectionRequiredError` 日志洪泛。⚠️ 暂无 fix PR。
9. **[#99586](https://github.com/openclaw/openclaw/issues/99586)** — gateway 触碰操作后运行时工具面返回空白 body，**容器重启仅短暂缓解**。⚠️ 暂无 fix PR。
10. **[#53408](https://github.com/openclaw/openclaw/issues/53408)** — 长对话后 `write`/`exec` **参数被静默丢弃**。⚠️ 暂无 fix PR。
11. **[#98435](https://github.com/openclaw/openclaw/issues/98435)** — gateway 重启后 MCP loopback 传输**不自动重握手**，`recovered=1` 具有误导性。⚠️ 暂无 fix PR。
12. **[#98702](https://github.com/openclaw/openclaw/issues/98702)** — 内建 openclaw runtime 继承的 OpenAI OAuth 在 `openai-chatgpt-responses` 传输上被拒绝，main 却成功。⚠️ 暂无 fix PR。

### 已有关联 fix PR 的 Bug

- **[#118489](https://github.com/openclaw/openclaw/issues/118489)**（Failed-tool finalization 被跳过）→ ✅ 已关闭，由 [#118344](https://github.com/openclaw/openclaw/pull/118344) 修复。
- **[#106760](https://github.com/openclaw/openclaw/issues/106760)**（Telegram 多 content block 第一个文本被擦除）→ ✅ 已关闭。
- **[#112248](https://github.com/openclaw/openclaw/issues/112248)**（`@openclaw/codex` 插件注册失败 → 已关闭）。

---

## 6. 功能请求与路线图信号

### 高优先级特性请求

| Issue | 标题 | 社区信号 |
|---|---|---|
| [#60572](https://github.com/openclaw/openclaw/issues/60572) | **多槽记忆架构**（Multi-Slot Memory Architecture） | 9 评论 / 3 👍，已有 linked PR |
| [#42840](https://github.com/openclaw/openclaw/issues/42840) | **Control UI 支持 MathJax/LaTeX** | 10 评论 / **10 👍**，呼声极高 |
| [#71058](https://github.com/openclaw/openclaw/issues/71058) | **单 Gateway 支持多个 Azure/Teams bot** | 9 评论 |
| [#88154](https://github.com/openclaw/openclaw/issues/88154) | **Slack Modal 交互工作流支持** | 8 评论 |
| [#7338](https://github.com/openclaw/openclaw/issues/7338) | **Agent 外部 API 请求的证明头**（Attestation Headers） | 5 评论 / 3 👍，标记 `needs-security-review` |
| [#9912](https://github.com/openclaw/openclaw/issues/9912) | **maxTurns/maxToolCalls 配置项** | 6 评论（KIMI K2 等模型忽略 system prompt 的防护） |
| [#78865](https://github.com/openclaw/openclaw/issues/78865) | **工具调用熔断器**（Tool Call Circuit Breaker） | 6 评论 — "50 分钟看 agent 撞墙"强烈诉求 |
| [#51336](https://github.com/openclaw/openclaw/issues/51336) | **错误消息中显示 API provider 名称** | 6 评论 |

### 路线图信号

- **会话与记忆基础设施处于风口浪尖**：多槽记忆、记忆保留策略（[#114612](https://github.com/openclaw/openclaw/issues/114612)）、记忆压实阻塞（[#53008](https://github.com/openclaw/openclaw/issues/53008)）、memory flush 配置陷阱（[#50611](https://github.com/openclaw/openclaw/issues/50611)）形成组合信号——项目正在**记忆架构重构的关键节点**，下一个 minor 版本极可能包含大的 memory-core 改进。
- **认证体系正在收敛**：#98702、#86215、[#125471](https://github.com/openclaw/openclaw/pull/125471)（Claude CLI OAuth 修复）、[#118823](https://github.com/openclaw/openclaw/pull/118823)（Codex 运行重载持久 OpenAI auth）等多线并进，说明 **OAuth 多 profile 架构正在稳定化**。
- **Sandbox/工作区生命周期治理**开始被系统化解决（[#43797](https://github.com/openclaw/openclaw/issues/43797) sandbox prune 不清理 workspace、[#131409](https://github.com/openclaw/openclaw/pull/131409) 撤回 Daytona 插件）。

---

## 7. 用户反馈摘要

### 典型用户痛点

1. **"Agent 在错误路径上反复横跳，浪费大量时间与 token"**
   - [#78865](https://github.com/openclaw/openclaw/issues/78865)：外部 API 限流后，agent 盲目重试 50 分钟。评论原文："**I just spent 50 minutes watching my agent bash its head against a wall.**"
   - [#53008](https://github.com/openclaw/openclaw/issues/53008)：记忆压实挂起导致 bot 完全无响应 10 分钟，所有消息排队未被处理。

2. **"静默失败是最让人沮丧的"**
   - [#126906](https://github.com/openclaw/openclaw/issues/126906)：**"Denying a tool via `tools.deny` can disable memory persistence, and nothing tells anyone — not the operator at startup, not `doctor`, and not the agent, which then reports success for saves that never happened."** — 工具降级后 agent 仍报告成功，运维完全无感知。
   - [#131150](https://github.com/openclaw/openclaw/issues/131150)：19 个 Slack 账号的 DM 在 gateway 重启后全部静默丢弃，无日志提示。
   - [#53408](https://github.com/openclaw/openclaw/issues/53408)：长对话后 write/exec 参数被静默丢弃，导致输出错误无崩溃。

3. **"多 agent 场景的复杂度逐渐显现"**
   - [#126360](https://github.com/openclaw/openclaw/issues/126360)：显式所有权下系统组件缺少 agentId 目标导致日志洪泛。
   - [#126424](https://github.com/openclaw/openclaw/pull/126424) 的合并说明多 agent 对话工具可绕过 agent bindings 投递消息。

4. **Beta 测试者的整体反馈（来自 [#125626](https://github.com/openclaw/openclaw/issues/125626)）**
   - 社区对 2026.8.1 beta 的验证活动活跃，测试范围涵盖最新 beta.3，反馈集中在投递可靠性、记忆系统稳定性与配置边界。

### 值得关注的用户表达

- [#48788](https://github.com/openclaw/openclaw/issues/48788) 中社区对架构级修复的期望：**"a proper architectural solution should handle multiple encodings across all channel adapters"**——用户已不满足于点状修复，要求全局性方案。
- [#78865](https://github.com/openclaw/openclaw/issues/78865) 作者直言 **"this is a critical missing feature"**——工具调用熔断器被视为基础设施级的缺失。

---

## 8. 待处理积压

### ⚠️ 长期未响应/未修复的重要 Issue

| Issue | 创建时间 | 最新评论 | 积压天数 | 备注 |
|---|---|---|---|---|
| [#41165](https://github.com/openclaw/openclaw/issues/41165) — Telegram DM 仍可落入 main session | 2026-03-09 | 2026-08-28 | **172 天** | P1，diamond lobster，修复 #40519 后仍复现，标记需要产品决策 |
| [#53408](https://github.com/openclaw/openclaw/issues/53408) — 长对话后 write/exec 参数静默丢弃 | 2026-03-24 | 2026-08-28 | **157 天** | P1，silver shellfish，无 fix PR |
| [#53008](https://github.com/openclaw/openclaw/issues/53008) — 记忆压实阻塞主通道 10+ 分钟 | 2026-03-23 | 2026-08-28 | **158 天** | P1，diamond lobster，无 fix PR |
| [#86215](https://github.com/openclaw/openclaw/issues/86215) — Codex OAuth 刷新失败卡死数小时 | 2026-05-24 | 2026-08-28 | **96 天** | P1，diamond lobster，无 fix PR，标记 `needs-product-decision` |
| [#87561](

---

## 横向生态对比

# 开源 AI 智能体生态横向对比分析报告（2026-08-28）

## 1. 生态全景

个人 AI 助手与自主智能体开源生态正处于**高活跃、快迭代**阶段：头部项目单日 PR/Issue 更新可达数百甚至上千条，版本发布与架构级重构并行。生态已明显分化为**终端助手网关（OpenClaw/Hermes）、开发者 SDK（OpenHands）、LLM 基础设施网关（LiteLLM）、工作流编排（Temporal）** 四个层次。稳定性与安全问题成为各项目共同的主战场——消息丢失、会话状态不一致、密钥遮蔽缺失、认证失败卡死等“静默失败”类问题被集中暴露。与此同时，多项目同步向 **A2A/ACP 协议、记忆架构重构、可观测性增强**三大方向投入，生态正从“单点智能”走向“可组合、可治理的智能体基础设施”。

## 2. 各项目活跃度对比

| 项目 | Issue 更新 | PR 更新 | Release | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 500（新开/活跃 398，关闭 102） | 500（待合并 278，合并/关闭 222） | 无（v2026.8.1-beta.3 验证中） | 社区热度最高，beta 反馈密集；P1 bug 积压较多，但修复管线通畅 |
| **Hermes Agent** | 448（新开/活跃 339，关闭 109） | 500（待合并 395，合并/关闭 105） | **v0.20.6（v2026.8.27）** | 极高活跃，3 个大型追踪 Issue 收官；更新链路是主要风险面 |
| **OpenHands SDK** | 33（活跃/新开 32） | 20（合并/关闭 9） | **v1.44.0** | 高活跃，安全缺陷集中暴露，版本节奏稳定 |
| **LiteLLM** | 79（新开/活跃 56，关闭 23） | 326（待合并 189，合并/关闭 137） | 无 | 极高活跃，合并效率高；Rust 迁移与稳定性治理并行 |
| **Temporal** | 1（新增） | 80（待合并 47，合并/关闭 33） | 无 | Issue 讨论少但工程推进扎实，可靠性修复响应快 |
| **Pi** | 暂无数据 | 暂无数据 | 暂无数据 | 当日无动态摘要 |

> 注：Pi 项目在本次数据源中未提供可分析内容，以下对比不包含 Pi。

## 3. OpenClaw 在生态中的定位

**OpenClaw 是目前生态中社区规模最大、渠道覆盖最广的终端助手网关项目**。

- **优势**：单日 500 Issue + 500 PR 的社区活跃度遥遥领先；支持 Discord/iMessage/Matrix/Slack/Telegram/Feishu 等全渠道消息投递，面向“个人 AI 助手”场景的形态最为完整；正处于 2026.8.1 正式版验证期，社区反馈闭环紧密。
- **技术路线差异**：与 Hermes Agent 相比，OpenClaw 聚焦“多渠道个人助手网关”而非桌面端/Fleet 管理；与 LiteLLM 相比，LiteLLM 是模型/成本路由层，OpenClaw 是会话与 Agent 执行层；与 OpenHands SDK 相比，OpenClaw 是完整应用而 OpenHands 是构建此类应用的 SDK；与 Temporal 相比，Temporal 提供通用工作流可靠性底座，OpenClaw 则直接面向终端用户交互。
- **当前短板**：会话状态一致性（session-state/message-loss）和 P1 级阻塞问题积压较多，且多个关键修复 PR 仍在待合并状态。这与其 beta 阶段社区大规模验证有关，也说明**渠道广度领先的同时，核心稳定性还未完全跟上社区期望**。

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **会话状态一致性与消息不丢失** | OpenClaw、Hermes、OpenHands、Temporal | OpenClaw：会话投影 livelock、Slack DM 重启后静默丢弃；Hermes：统一 deadline 层系统性消除 timeout/hang；OpenHands：全局锁串行化、子代理事件不可见；Temporal：SignalWithStart 校验缺失 |
| **认证与密钥安全** | OpenClaw、OpenHands、LiteLLM | OpenClaw：OAuth 刷新失败卡死、多 profile 认证收敛；OpenHands：密钥遮蔽仅覆盖 1/13 工具、模型输出未遮蔽；LiteLLM：Bedrock Bearer 认证路径误解析 AWS 凭证 |
| **记忆与上下文管理** | OpenClaw、Hermes、OpenHands | OpenClaw：多槽记忆架构、记忆压实阻塞主通道 10+ 分钟；Hermes：统一 deadline 解决长任务挂起；OpenHands：`load_memory` 全局偏好被静默忽略 |
| **Agent 间通信协议（A2A/ACP/Nexus）** | LiteLLM、OpenHands、Temporal | LiteLLM：A2A agent 注册表语义搜索；OpenHands：ACP provider 支持、A2A 服务器模式；Temporal：System Nexus 集成 SignalWithStart |
| **可观测性与成本核算** | OpenHands、LiteLLM、Temporal | OpenHands：telemetry 统计 token delta 导致指标不可比；LiteLLM：Responses API usage.cost 永远记 0、Prisma 崩溃无告警；Temporal：慢请求日志增加 namespace 标签 |
| **工具调用防护与熔断** | OpenClaw、LiteLLM | OpenClaw：工具调用熔断器呼声极高（“agent 撞墙 50 分钟”）；LiteLLM：连接拒绝被误映射导致 Router 错误冷却 |
| **更新与部署可靠性** | Hermes、Temporal | Hermes：Windows 更新挂起、systemd 边界问题；Temporal：namespace 软删除长期积压 |

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构特点 |
|---|---|---|---|
| **OpenClaw** | 多渠道个人 AI 助手网关，会话与记忆管理 | 个人用户、自托管社区 | 渠道适配器 + Agent 运行时 + 记忆系统；beta 验证期，社区驱动 |
| **Hermes Agent** | 桌面端 + 网关 + Fleet 多机管理 | 个人/团队重度用户 | 频繁 patch 版本（v0.20.x），强调更新链路与 systemd 集成 |
| **OpenHands SDK** | 软件工程 Agent 的构建 SDK | 开发者、AI Agent 产品团队 | 模块化 SDK，流式架构重构 + ACP/A2A 协议支持，安全遮蔽是短板 |
| **LiteLLM** | LLM 统一网关：路由、预算、fallback、guardrail | 企业平台团队 | Python 网关 + 计划中 Rust 迁移；复杂路由器与 A2A 搜索是近期亮点 |
| **Temporal** | 分布式工作流编排引擎 | 后端/基础设施工程师 | 非 AI 专用，但成为 Agent 任务可靠执行的底层依赖；CHASM/Nexus 集成进行中 |

**关键差异**：OpenClaw 与 Hermes 竞争同一层（终端助手），但 OpenClaw 更重渠道生态、Hermes 更重桌面/Fleet 管理；OpenHands 与 LiteLLM 分别从“Agent 开发框架”和“模型网关”两个入口向中间层靠拢；Temporal 作为通用底座，不直接面向 AI 用户，但为整个生态提供可靠性支撑。

## 6. 社区热度与成熟度

**第一梯队（极高活跃/快速迭代）**：**OpenClaw、Hermes Agent、LiteLLM**。
三者单日 PR 更新均超过 300，社区反馈量大，功能迭代与 bug 修复并行。OpenClaw 处于 beta 验证期，Hermes 刚发布 v0.20.6，LiteLLM 则在 Rust 迁移与功能扩展双线推进。

**第二梯队（高活跃/质量巩固）**：**OpenHands SDK、Temporal**。
OpenHands 单日 PR 仅 20 条，但一次代码审查集中暴露 8 个架构级 bug，说明正在从“功能扩张”转向“质量收紧”；Temporal Issue 侧极冷（仅 1 条新 Issue），但 PR 侧 80 条且多为可靠性修复，属于典型的工程驱动型项目，社区讨论少、代码产出稳。

**成熟度判断**：Temporal 最成熟，稳定性修复体系化；OpenClaw 社区最活跃但尚在 beta 攻坚；Hermes 通过高频 patch 维持可用性；LiteLLM 功能推进极快但 bug 密度同步上升；OpenHands 处于安全加固的关键窗口期。

## 7. 值得关注的趋势信号

1. **“静默失败”成为全生态公敌**：OpenClaw 的 Slack DM 静默丢弃、内存持久化静默禁用、参数静默丢失；OpenHands 的 PR-reviewer 静默不发布结果；LiteLLM 的 usage.cost 静默记 0。用户对“无日志、无警报、无崩溃”的失败模式忍耐度已到极限，**可观测性和明确失败语义将是下一阶段核心竞争力**。

2. **记忆与上下文架构迎来重构窗口**：OpenClaw 的多槽记忆、Hermes 的统一 deadline 层、OpenHands 的记忆偏好一致性，三个项目不约而同触及记忆/上下文基础设施。结合 OpenClaw 记忆压实阻塞主通道等 P1 问题，**“记忆即基础设施”已成为头部项目共识**，未来 1-2 个 minor 版本内可能出现记忆架构的集中升级。

3. **A2A/ACP 协议从概念走向落地**：LiteLLM 实现 A2A agent 语义搜索，OpenHands 引入 ACP provider 构建参数并推进 A2A 服务器模式，Temporal 通过 Nexus 支持 workflow 间调用。**跨 Agent 通信正在成为网关和 SDK 层的默认能力**，生态将从单 Agent 孤岛走向可互操作的 Agent 网格。

4. **成本治理从“记账”走向“精细化控制”**：LiteLLM 的零成本模型被预算阻止、复杂路由器将内务调用误路由到顶级模型、OpenClaw 用户要求 maxTurns/maxToolCalls 硬限制、工具调用熔断器诉求——**用户不再满足于事后账单，而是要求在运行前/运行中阻止浪费**。对 Agent 开发者而言，工具级熔断、预算感知路由、成本可观测性应作为一等公民设计。

5. **OAuth 多 Profile 架构成为终端 Agent 的标配难题**：OpenClaw 的 Codex OAuth 刷新失败、OpenHands 的加密 LLM profile 解密不完整、LiteLLM 的 Bedrock 凭证误解析——多个项目在认证链路上出现类似问题。**认证体系的稳定性和可恢复性将决定 Agent 能否真正“无人值守”**。

6. **更新/部署链路是最后一块短板**：Hermes 的 Windows 更新挂起、systemd 代际边界问题，Temporal 的 namespace 软删除积压 4 个月，OpenClaw 的 sandbox/workspace 生命周期治理刚起步。**Agent 的“自更新”和“生命周期管理”能力尚未成熟**，这将是下一阶段运维侧的核心竞争点。

---

*报告基于 2026-08-28 各项目 GitHub 公开动态生成。Pi 项目当日无数据，未纳入对比。*

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-28

## 1. 今日速览

项目今日活跃度**极高**：过去 24 小时产生 448 条 Issue 更新（其中 339 条新开/活跃、109 条关闭）与 500 条 PR 更新（395 条待合并、105 条已合并/关闭），均处于历史高位。昨日发布 v0.20.6（v2026.8.27）patch 版本，统一收编自 v0.20.5 以来约 525 个 PR。值得关注的是，3 个大型追踪 Issue 在同日关闭标记完成（桌面多网关持久连接、统一超时/挂起架构修复、Fleet 更新可靠性方案），说明项目正从零散补丁转向结构性收尾；但安装/更新类 Bug 持续高发（P0 Debian 安装失败、Windows 更新挂起、systemd 边界问题），仍是当前最明显的短板。整体判断：**功能推进与稳定性修复双线并行，版本健康度良好，更新链路是主要风险面。**

---

## 2. 版本发布

### Hermes Agent v0.20.6（v2026.8.27）

- **发布日期**：2026 年 8 月 27 日
- **类型**：Patch 版本
- **核心内容**：滚动收编 v0.20.5 以来约 **525 个 PR**，面向 Docker 镜像、托管部署与新安装用户提供稳定标签。
- **破坏性变更**：无（Patch 版本，保持 API/配置向后兼容）。
- **迁移注意事项**：
  - 下游 Docker 用户建议升级到 `v2026.8.27` 标签以纳入自 v0.20.5 以来的全部修复；
  - 由于该版本主要面向稳定化，不包含新增配置项，现有 `~/.hermes/` 配置无需调整；
  - 桌面端用户若通过 `hermes update` 更新，请注意 #95589 等 Windows 更新流程已知问题（见 Bug 部分）。

发布链接：https://github.com/NousResearch/hermes-agent/releases/tag/v2026.8.27

---

## 3. 项目进展

今日无大型 feature PR 合并，但多个结构性追踪 Issue 关闭，标志若干长期战役收官：

### 里程碑：3 个大型追踪 Issue 关闭

- **[#94724] Desktop 持久多网关连接 — CAMPAIGN COMPLETE（29 个 PR）**（已关闭）  
  桌面端多网关持久连接战役全部完成：29 个 PR 合并，2 个同日回归已修复，15 个被挽救的遗留问题全部交付。  
  https://github.com/NousResearch/hermes-agent/issues/94724

- **[#91277] Fleet 更新可靠性统一部署方案**（已关闭）  
  针对“更新是最不可靠能力”的追踪 Issue（涉及约 30 个 open issues / 15 个 open PRs），今日关闭意味着方案阶段完成并进入执行。  
  https://github.com/NousResearch/hermes-agent/issues/91277

- **[#85125] 统一 deadline 层 — 4 阶段架构修复**（已关闭）  
  解决超时/挂起积压（400+ 匹配 issue）的架构性方案完成设计阶段，将系统性消除 timeout/hang bug 类。  
  https://github.com/NousResearch/hermes-agent/issues/85125

### 关键新提交 PR

- **[#96851] fix(gateway): 停止阻塞事件循环 — off-loop 热路径 + ASYNC lint 门槛（P1）**  
  针对“事件循环阻塞”bug 类的架构级修复：将 async 函数中的阻塞调用移出 event loop，避免整个 gateway 冻结。这是持续产生 incident 的根因修复。  
  https://github.com/NousResearch/hermes-agent/pull/96851

- **[#96853] fix(update): 强制执行 systemd worker 代际边界**  
  在 in-place 源码变更前建立精确的 Linux user-systemd 清单，用 canary-first 代际边界执行重启，防止更新时服务成员漂移。  
  https://github.com/NousResearch/hermes-agent/pull/96853

- **[#96862]

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目日报 — 2026-08-28

## 1. 今日速览

过去 24 小时项目保持**高活跃度**：共产生 33 条 Issue 更新（其中 32 条活跃/新开）和 20 条 PR 更新（9 条已合并/关闭），并发布 v1.44.0。值得关注的信号是，**安全问题成为当前最集中的开发焦点**——VascoSch92 在 #4671 流式架构重构 Epic 下连续提交了 9 个子任务，其中 3 条标记为 `priority：high` 的安全相关缺陷（#4672/#4677/#4678），直指 token 泄漏与密钥遮蔽覆盖不足两大风险。此外，enyst 在同一天集中提交了 8 个中等优先级 Bug（#4661-#4668），涵盖 git 路径匹配、全局工作目录竞态、进程级注册表泄漏等架构层面问题，呈现出一次系统的代码审查结果。v1.44.1 的发布 PR（#4693）已在当日起步，版本迭代节奏稳定。

---

## 2. 版本发布

### v1.44.0（2026-08-27/28 发布）

**包含的修复：**

- **fix(agent-server)**：在中断(action interruption)分支上保持崩溃恢复结果不丢失（PR #4488，@neubig）
- **fix(workspace)**：注入 git clone token 时显式遵守指定的 provider host（PR #4488 同批次，@rsd-darshan）

**破坏性变更：** 无明确标注。

**迁移注意事项：** 该版本无已知迁移要求。v1.44.1 发布 PR（#4693）已于 8/28 启动，处于 checklist 阶段，预计包含后续 bugfix。

---

## 3. 项目进展

过去 24 小时共合并/关闭 9 个 PR，按影响面排列：

- **#4688 chore(deps)： bump lmnr to 0.7.60**（已合并）— 修复 LiteLLM streaming 推理追踪丢失与 token 计量错误问题，直接影响可观测性数据准确性。链接：https://github.com/OpenHands/software-agent-sdk/pull/4688
- **#4691 fix(sdk)： resolve structured builtin tool specs remotely**（已关闭）— 修复结构化内置工具规格的远程解析逻辑。链接：https://github.com/OpenHands/software-agent-sdk/pull/4691
- **#4690 fix(mcp)： map mcp SDK McpError to connection failure in probe**（已合并）— 将 MCP 连接测试中的 `McpError： Session terminated` 错误映射为清晰可读的连接失败提示，改善 Agent Canvas 生态的 MCP 服务器接入体验。链接：https://github.com/OpenHands/software-agent-sdk/pull/4690
- **#4687 feat(agent-server)： add INSTALL_ACP_PROVIDERS build arg**（已合并）— 为 agent-server 镜像增加可选 ACP provider 构建参数，是 #4643 的第二步，为 ACP 协议支持铺路。链接：https://github.com/OpenHands/software-agent-sdk/pull/4687
- **#4686 Verify DeepSeek v4 Flash model**（已关闭）— 完成 DeepSeek v4 Flash 模型验证。
- **#4685 test(agent-server)： cover conversation reads not serializing behind an unrelated start**（已关闭）— 为 #4675 的全局锁问题添加回归测试。
- **#4684 / #4628 Release v1.44.0 发布流程**（已关闭）— v1.44.0 的正式发布 PR 与重复发布流程。
- **#4651 refactor(agent-server)： share ACP provider payload as parent-independent Docker layer**（已合并）— 重构 Docker 层结构，将 ACP provider payload 提取为独立层，提升镜像层复用效率。

**整体评价：** 项目的重点是依赖与基础设施加固（lmnr 升级、MCP 错误映射、Docker 层重构），同时回归测试的补充（#4685）说明维护者正在有意识地为已知架构问题建立防护网。

---

## 4. 社区热点

| Issue | 标题 | 评论数 | 主题 |
|-------|------|--------|------|
| [#4577](https://github.com/OpenHands/software-agent-sdk/issues/4577) | [Feature]： Add per-key tag endpoints to avoid read-modify-write on PATCH /api/conversations/{id} | 6 | 新端点设计讨论 |
| [#4542](https://github.com/OpenHands/software-agent-sdk/issues/4542) | Global agent_context.load_memory preference is ignored unless conversation launched from agent profile | 6 | 全局偏好语义争议 |
| [#4260](https://github.com/OpenHands/software-agent-sdk/issues/4260) | Cloud Automation PR reviewer intermittently posts no review | 5 | CI/CD 自动化可靠性 |
| [#3907](https://github.com/OpenHands/software-agent-sdk/issues/3907) | feat： forward sub-agent (TaskToolSet) inner events to live conversation stream | 5 | 实时事件流可观测性 |

**分析与诉求：**

1. **#4577 的诉求本质是 API 设计的效率与原子性**。当前 `PATCH /api/conversations/{id}` 的 `tags` 字段采用整替换语义，客户端在并发写入场景需要先读后写（read-modify-write），既低效又存在竞态。该 Issue 已有对应 PR #4617（POST/DELETE 单 key 端点），处于开放状态，预计将作为 API 增强方向继续推进。

2. **#4542 反映的是"全局偏好"语义的一致性缺口**。用户预期 `agent_context.load_memory` 作为全局用户偏好应无条件生效，但实际只在显式指定 `agent_profile_id` 时生效。这属于行为与文档/心智模型不一致的问题。

3. **#4260 指向 CI/CD 自动化链路中的"静默失败"**。PR-reviewer bot 出现"进程评论但最终不发布结果"的间歇故障，叠加 600 秒超时上限导致任务被杀死。这类问题严重削弱用户对 AI 自动化工作流的信任，属于高影响低复现率的"隐形故障"。

4. **#3907 的诉求是子代理可见性**。当 TaskToolSet 派生子代理时，父级实时事件流对子代理内部事件"失明"，限制了上层消费者（如 WebSocket 客户端）对完整执行过程的感知。

---

## 5. Bug 与稳定性

按严重程度从高到低排列（P0→P2）：

### 🔴 高风险（security-related / priority：high）

| Issue | 问题 | 修复 PR | 说明 |
|-------|------|---------|------|
| [#4672](https://github.com/OpenHands/software-agent-sdk/issues/4672) | **每个 token delta 都被 POST 到已配置的 webhook**。`WebhookSubscriber.__call__` 无事件类型过滤，流式输出时每个 token 增量都会触发一次 webhook POST，既造成隐私泄露风险，也可能产生海量请求 | ✅ **#4689（已开放）** 由 VascoSch92 提交，修复方案：停止向所有 subscriber 广播 `StreamingDeltaEvent` | 属于 #4671（流式架构重构）核心问题之一 |
| [#4677](https://github.com/OpenHands/software-agent-sdk/issues/4677) | **密钥遮蔽只覆盖 13 个工具中的 1 个**。仅有 `terminal/impl.py` 调用了 `SecretRegistry.mask_secrets_in_output`，`file_editor`、`grep`、`glob`、`apply_patch`、`browser_use` 等 12 个工具均未遮蔽 | ❌ 尚无 | 安全影响范围最广的问题 |
| [#4678](https://github.com/OpenHands/software-agent-sdk/issues/4678) | **模型输出从未在标准 Agent 路径上遮蔽**。`mask_secrets_in_output` 在 `acp_agent.py` 之外只有 2 个调用点，标准 agent 执行路径完全没有遮蔽 | ❌ 尚无 | 影响所有使用标准 SDK 的客户端 |

### 🟡 中高风险（priority：high）

| Issue | 问题 | 修复 PR |
|-------|------|---------|
| [#4542](https://github.com/OpenHands/software-agent-sdk/issues/4542) | 全局 `load_memory` 偏好被静默忽略 | ❌ 尚无 |
| [#4675](https://github.com/OpenHands/software-agent-sdk/issues/4675) | `_lifecycle_lock` 进程级锁导致所有 conversation-scoped 请求全局串行 | ⚠️ 已有回归测试（#4685），正式修复未出现 |
| [#4558](https://github.com/OpenHands/software-agent-sdk/issues/4558) | 加密 LLM profile 仅在 conversation 路径解密，FallbackStrategy 与 sub-agents 加载时无 cipher | ❌ 尚无 |

### 🟢 中风险（priority：medium）

- **[#4562](https://github.com/OpenHands/software-agent-sdk/issues/4562) workspace 文件在私有局域网 HTTP 访问时返回 401** — `SameSite=None` 但缺 `Secure` 标记，导致 session cookie 被浏览器拒绝
- **[#4692](https://github.com/OpenHands/software-agent-sdk/issues/4692) TaskManager 强制 `stream=False`** — 使用 ChatGPT 订阅时子代理 LLM 流式能力被禁用，破坏兼容性（2026-08-28 新开）
- **[#4673](https://github.com/OpenHands/software-agent-sdk/issues/4673) telemetry event_count_bucket 统计 token deltas** — 使指标跨会话不可比
- **[#4674](https://github.com/OpenHands/software-agent-sdk/issues/4674) ConversationState 单一 FIFOLock 守护六个独立关注点** — 锁竞争导致吞吐受限
- **[#4668](https://github.com/OpenHands/software-agent-sdk/issues/4668) Planning file editor 丢弃继承的 observation 和 diff 数据** — 下游工具功能缺失
- **[#4667](https://github.com/OpenHands/software-agent-sdk/issues/4667) Tom 处理历史可能检查点未索引事件**
- **[#4670](https://github.com/OpenHands/software-agent-sdk/issues/4670) WebSocketCallbackClient.stop() 无法关闭静默连接** — worker 线程泄漏
- **[#4661](https://github.com/OpenHands/software-agent-sdk/issues/4661) 进程级 subagent 注册表跨对话泄漏定义**
- **[#4663](https://github.com/OpenHands/software-agent-sdk/issues/4663) Python glob fallback 修改进程全局 cwd**
- **[#4664](https://github.com/OpenHands/software-agent-sdk/issues/4664) CloudWorkspace resume 使用过期连接数据**（security）
- **[#4665](https://github.com/OpenHands/software-agent-sdk/issues/4665) Skills marketplace 对当前 extensions manifest 布局返回空**
- **[#4666](https://github.com/OpenHands/software-agent-sdk/issues/4666) 重复浏览器录制启动可能孤儿化 flush task**
- **[#4662](https://github.com/OpenHands/software-agent-sdk/issues/4662) 嵌套 Git 过滤使用词法前缀匹配丢弃无关路径**

---

## 6. 功能请求与路线图信号

### 可能纳入下一版本的功能

1. **Per-key tag endpoints（#4577 + PR #4617）** — 方案已明确（POST/DELETE `/api/conversations/{id}/tags/{key}`），PR 已经提交，属于低风险 API 增强。从 Issue 创建到 PR 仅 3 天，说明需求方有强推动力，预计 v1.45.0 可落地。

2. **A2A 协议服务器模式（PR #4590）** — 实现 Agent Card + JSON-RPC/SSE，使 agent-server 成为 A2A 网格中的可发现节点。该 PR 已存在 5 天且标为开放状态，属于长期功能规划方向（对应 #1060），短期内可能停留于 review。

3. **流式架构重构（#4671 Epic）** — 包含 12 个以上的子任务

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-28

## 1. 今日速览

过去24小时 LiteLLM 项目保持**极高活跃度**：合计 79 条 Issue 更新与 326 条 PR 更新，创近期峰值。新开/活跃 Issue 56 条、关闭 23 条，PR 待合并 189 条、合并/关闭 137 条，表明维护团队在快速推进合并工作的同时，社区反馈与功能请求也大量涌入。今日无新版本发布，但 Rust 迁移（#31263）作为 6 月启动的长期主线仍在持续发酵，成为社区讨论的核心焦点。整体来看，项目处于功能迭代与架构升级并行的快节奏阶段，Bug 报告密度较高，稳定性治理是当前的主要矛盾。

---

## 3. 项目进展

今日无新版本发布，PR 合并/关闭 137 条。以下为值得关注的重要 PR（部分为新提交，仍在 Review 阶段）：

- **#38624 fix(exceptions): keep a refused connection an APIConnectionError**（[链接](https://github.com/BerriAI/litellm/pull/38624)）— 修复 #38318 引入的回归：连接拒绝被错误映射为 InternalServerError，导致 Router 冷却了未实际失败的部署。属于稳定性关键修复。
- **#38623 fix(proxy): hold fallback lifecycle frames**（[链接](https://github.com/BerriAI/litellm/pull/38623)）— 修复 `/v1/messages` 流式请求 fallback 失败时提前返回 200 SSE 的问题，对应 Issue #38610。
- **#38618 fix(anthropic): handle per-level reasoning_effort flags without supports_reasoning**（[链接](https://github.com/BerriAI/litellm/pull/38618)）— 修复 GPT-5-search-api 因缺少 `supports_reasoning` 标志导致 reasoning_effort 降级的问题。
- **#38620 / #38619 fix(bedrock): skip AWS credentials for bearer auth**（[链接 1](https://github.com/BerriAI/litellm/pull/38620)、[链接 2](https://github.com/BerriAI/litellm/pull/38619)）— 两个同主题 PR：Bearrer 认证路径下跳过 AWS SigV4 凭证解析，消除 IMDS 不可达时约 2 秒延迟。
- **#38617 fix(proxy): admit litellm_proxy/hosted_vllm in provider-endpoint discovery**（[链接](https://github.com/BerriAI/litellm/pull/38617)）— 修复 GET /v1/models 返回字面 `litellm_proxy/*` 而非真实模型列表的问题。
- **#38609 feat(a2a): semantic search over the agent registry**（[链接](https://github.com/BerriAI/litellm/pull/38609)）— 新增 `GET /v1/agents?query` 语义搜索与 `agent_search` MCP 工具，agent 注册表可搜索性增强。
- **#38598 fix(complexity_router): route client housekeeping calls to the cheapest tier**（[链接](https://github.com/BerriAI/litellm/pull/38598)）— 自动路由器的分类器误将对话标题生成等内务调用标记为 COMPLEX 并路由到顶级，现修正为识别客户端内务提示并路由到最便宜档位。

整体来看，项目在**代理稳定性**（异常映射、fallback 生命周期）、**Bedrock 集成优化**、**复杂路由器精细化**三个方向有明显推进。

---

## 4. 社区热点

### 🔥 #31263 LiteLLM Rust Migration — the fastest and litest AI Gateway (sub 1ms overheads)
- **评论 21 | 👍 17** — [链接](https://github.com/BerriAI/litellm/issues/31263)
- 这是 Rust 迁移的总票务，6 月 25 日创建后持续活跃。社区关注点集中在迁移对现有 Python API 兼容性的影响、Rust 网关的性能收益（sub 1ms 开销）、以及 Beta 测试者计划的参与方式。该 Issue 被置顶为迁移相关的唯一讨论入口，反映用户对架构演进方向的高度关注与期待。

### 🔥 #26886 [Bug]: Prisma reconnection failed
- **评论 16 | 👍 11** — [链接](https://github.com/BerriAI/litellm/issues/26886)
- LiteLLM Proxy Pod 中 Prisma 查询引擎周期性崩溃，导致代理不稳定。该问题自 4 月 30 日报告以来持续活跃，评论数高说明不少用户遭遇类似问题。这是当前最受关注的稳定性 Bug。

### 🔥 #33383 Upgrade Langfuse integration to Python SDK v4 and v4 OTel ingestion
- **评论 8 | 👍 9** — [链接](https://github.com/BerriAI/litellm/issues/33383)
- Langfuse 团队成员主动提出的集成升级请求，属于上游依赖适配。Langfuse Cloud Fast Preview 使用新的 observations-first 摄入路径，需要 LiteLLM 升级 SDK。此类外部维护者直接发起的 Issue 通常会被优先处理。

---

## 5. Bug 与稳定性

今日 Bug 类 Issue 密集，按严重程度排列如下：

### 🔴 高严重度

- **#26886 [Bug]: Prisma reconnection failed**（[链接](https://github.com/BerriAI/litellm/issues/26886)）— Prisma 查询引擎进程崩溃导致代理不稳定，4 月底报告，持续活跃，暂无明确 fix PR。影响面较大。
- **#38515 [Bug]: Zero-cost models are blocked once a user's personal max_budget is exhausted**（[链接](https://github.com/BerriAI/litellm/issues/38515)）— 零成本模型（价格为 0）在用户预算耗尽后仍被阻止，与定价逻辑相悖，属商业逻辑 Bug。
- **#38358 [Bug]: litellm_settings.request_timeout never fires when upstream is silent from the first byte**（[链接](https://github.com/BerriAI/litellm/issues/38358)）— 上游接受 TCP 连接但不发送任何数据时，request_timeout 永不触发，可能导致请求挂起。

### 🟡 中严重度

- **#31441 [Bug]: end_user in SpendLogs pinned to first request's user on shared virtual key**（[链接](https://github.com/BerriAI/litellm/issues/31441)）— v1.87.0 回归：共享虚拟密钥下 `end_user` 列被固定为第一个请求的用户，导致花销归属错误。
- **#38511 [Bug]: Responses streaming error handler crashes with AttributeError**（[链接](https://github.com/BerriAI/litellm/issues/38511)）— 流式响应错误处理器崩溃，掩盖了真正的错误原因，影响可观测性。
- **#38357 [Bug]: Bedrock Converse/InvokeModel handler never reads httpx.Response.headers**（[链接](https://github.com/BerriAI/litellm/issues/38357)）— `x-amzn-RequestId` 等 Bedrock 响应头缺失，影响排查与审计。
- **#38401 [Bug]: Bedrock Realtime acknowledges sessions before provider readiness**（[链接](https://github.com/BerriAI/litellm/issues/38401)）— 会话在 provider 就绪前被确认，且终端流失败被抑制。
- **#21540 Inconsistent default access: empty models list grants all access, empty MCP list grants none**（[链接](https://github.com/BerriAI/litellm/issues/21540)）— 空 models 列表与空 MCP 列表的默认行为相反，构成安全风险。
- **#34492 [Bug]: Applying budget_duration on existing key/user/team doesn't reset carried spend**（[链接](https://github.com/BerriAI/litellm/issues/34492)）— 预算窗口应用到已有密钥时，累计消费未重置，导致新窗口立即触发 429。

### 🟢 低严重度 / 边缘

- **#38510 / #38527 等** — 若干文档问题、模型价格补充请求（如 #38608 请求添加 GLM-5.3-Flash 价格条目）。

**已有对应 fix PR 的：** #38610（fallback 流式错误）→ PR #38623；#38620/#38619 对 Bedrock 凭证问题；#38360（模型设置保存不生效）仍在排查中。

---

## 6. 功能请求与路线图信号

多个 Feature Request 值得关注，其中部分已有对应 PR：

| 功能需求 | Issue 链接 | 对应 PR | 纳入可能性 |
|---------|-----------|---------|-----------|
| **Vertex AI RAG Engine 作为 vector store provider**（#36285） | [链接](https://github.com/BerriAI/litellm/issues/36285) | 无 | 中 — 企业用户常用场景，但实现面较大 |
| **QwenCloud 官方迁移路径**（#36150） | [链接](https://github.com/BerriAI/litellm/issues/36150) | 无 | 中 — 新增 provider 适配属常规需求 |
| **Generic guardrail fail-open 模式**（#19779，已关闭） | [链接](https://github.com/BerriAI/litellm/issues/19779) | 无 | 已关闭但未落地，可关注后续 |
| **自定义分类器 tier 编辑 UI** | PR #38603 | [PR 链接](https://github.com/BerriAI/litellm/pull/38603) | 高 — 已有实现 |
| **自定义 tier 参数过滤** | PR #38622 | [PR 链接](https://github.com/BerriAI/litellm/pull/38622) | 高 — 已有实现 |
| **A2A agent 语义搜索** | PR #38609 | [PR 链接](https://github.com/BerriAI/litellm/pull/38609) | 高 — 已有实现 |
| **模型/项目创建时 rpm/tpm 配额必填开关** | PR #36514 | [PR 链接](https://github.com/BerriAI/litellm/pull/36514) | 中 — 已提交两周，待 Review |
| **Lakera v2 guardrail 增强** | PR #34940 | [PR 链接](https://github.com/BerriAI/litellm/pull/34940) | 中 — 已提交一个月，待合并 |

**路线图信号：** Rust 迁移（#31263）明确是长期主线；复杂路由器（Complexity Router）的持续迭代（#38598、#38603、#38622）表明该功能进入精细化阶段；A2A agent 生态的扩展（#38609）暗示了 agent 间通信的战略方向。

---

## 7. 用户反馈摘要

- **Rust 迁移期待高、疑问也不少**：社区对 sub 1ms 开销的性能目标反应正面（17 👍），但用户更关心 Python API 的兼容性、现有部署的迁移路径、以及 Beta 测试者的申请流程（#31263）。
- **Prisma 崩溃困扰多用户**：4 月底报告的问题至今活跃，16 条评论中多个用户表示遇到类似 Pod 不稳定问题，用户对修复速度有一定不满情绪（#26886）。
- **定价与配额逻辑投诉集中在预算相关**：零成本模型被预算阻止（#38515）、预算窗口重置不生效（#34492）、缓存 token 计费错误（#26807 已关闭但评论仍有效），说明用户对成本核算精确性非常敏感。
- **OpenRouter cost 统计缺口**：PR #38538 指出 Responses API 的 usage.cost 未被读取导致花费永远记为 $0，影响用户成本账单准确性。
- **默认行为不一致引发安全担忧**：#21540 中空 models 列表授予全部权限，而空 MCP 列表授予无权限，用户认为这是安全隐患。

---

## 8. 待处理积压

以下 Issue 长期未获明确回应或进展缓慢，提醒维护者关注：

- **#26886 Prisma reconnection failed**（[链接](https://github.com/BerriAI/litellm/issues/26886)）— 4 月底创建，至今 4 个月，16 条评论、11 👍，仍无 fix 方案。
- **#14505 [P1] [Feature]: Pass immutable safety identifiers (user_ids) by default**（[链接](https://github.com/BerriAI/litellm/issues/14505)）— 2025 年 9 月创建，Enterprise P1 优先级，近一年仍未落地。
- **#22289 PostgreSQL connections silently dropped by RDS**（[链接](https://github.com/BerriAI/litellm/issues/22289)）— 2 月创建，6 个月零回应，RDS 用户可能受影响。
- **#15519 [Bug]: DB exception in update_spend job**（[链接](https://github.com/BerriAI/litellm/issues/15519)）— 2025 年 10 月创建，曾标记 stale 现重新激活，说明问题仍在复现。
- **#26807 Cached prompt tokens billed as regular input**（[链接](https://github.com/BerriAI/litellm/issues/26807)）— 4 月创建，缓存 token 计费错误影响成本核算准确性，已关闭但用户持续评论。

---

*本日报基于 GitHub 公开数据自动生成，数据统计时间为 2026-08-28。*

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-28

## 今日速览

过去24小时内 Temporal 项目保持高度活跃，PR 更新达 80 条（待合并 47 条，已合并/关闭 33 条），显示核心开发节奏紧凑。Issue 侧仅新增 1 条（#11822），为 CHASM/System Nexus 集成中 SignalWithStart 未验证 cron 调度的潜在缺陷。无新版本发布。整体来看，项目当前聚焦于可靠性（reliability-2026）、CHASM 框架集成和稳定性修复三大方向，社区讨论数量较少但工程推进力度较大。

---

## 版本发布

过去 24 小时无新版本发布。

---

## 项目进展

今日合并/关闭 33 条 PR，但列表中的已关闭 PR 均为开发中的合并或撤回，未发现社区大版本发布。以下为今日值得关注的在途 PR 进展：

### 稳定性与可靠性（reliability-2026 系列）
- [#11841 Fix worker shutdown poll registration race](https://github.com/temporalio/temporal/pull/11841) — 修复 worker 关闭过程中 poll 注册的竞态条件，防止关闭请求遗漏仍在启动中的 poll。由 @rkannan82 提交。
- [#11839 Fix FirstWorkflowTaskBackoff Accumulation upon ContinueAsNew](https://github.com/temporalio/temporal/pull/11839) — 修复 ContinueAsNew 后首次工作流任务退避时间累积为负值的问题，此前会导致退避无限累积。由 @yycptt 提交。
- [#11825 Fix data race in perNamespaceWorker initialization](https://github.com/temporalio/temporal/pull/11825) — 修复 perNamespaceWorker 初始化期间的数据竞争，在注册动态配置回调前加锁。由 @rkannan82 提交。
- [#10502 DLQ pure task validation enhancement](https://github.com/temporalio/temporal/pull/10502) — 若纯任务执行后仍有效，则抛出错误并将其移入 DLQ，避免执行卡死；同时为测试框架增加单元测试验证。由 @awln-temporal 提交。
- [#11840 Emit force termination metric](https://github.com/temporalio/temporal/pull/11840) — 发出带 namespace、archetype 和 reason 标签的强制终止指标，仅统计系统/CHASM 框架导致的终止。由 @yycptt 提交。

### CHASM 与 Nexus 集成
- [#11820 Fix Nexus start-operation retry classification](https://github.com/temporalio/temporal/pull/11820) — 修复 `handleStartOperationError` 等函数对包装后 service error 的重试分类，使用 `errors.As` 解包错误类型。已关闭（合并）。由 @tekkaya 提交。
- [#11774 Fix SignalWithStart hang on orphaned current-execution pointer](https://github.com/temporalio/temporal/pull/11774) — 修复 Cassandra 中 current_executions 指针残留导致 SignalWithStart 挂起的问题，通过 UpdateCurrent 覆盖孤儿指针。由 @ryancocuzzo 提交。关联 Issue #10841。

### 可观测性与运维工具
- [#11828 Include namespace tag in slow request log](https://github.com/temporalio/temporal/pull/11828) — 慢请求日志增加 namespace 标签，提升问题定位效率。由 @claude[bot] 代 Yimin Chen 提交（Slack 驱动）。
- [#11722 tdbg dynamic config describe/get/dump](https://github.com/temporalio/temporal/pull/11722) — 为 tdbg CLI 增加动态配置的查看、获取与导出能力，方便运维排查。由 @feiyang3cat 提交。

### 其他功能推进
- [#11807 Dedupe visibility archival](https://github.com/temporalio/temporal/pull/11807) — S3/GCS 可见性归档增加 SHA-256 内容感知去重，减少重复上传。由 @qyc5937 提交。
- [#11818 Re-enable BUFFER_ONE backfill test](https://github.com/temporalio/temporal/pull/11818) — 重新启用此前跳过的 `testBackfillWithBufferOneOverlap` 测试，并删除不再支持的 memo-only 更新测试。由 @chaptersix 提交。
- [#11836/#11837 Legacy HSM 迁移与 lint 修复](https://github.com/temporalio/temporal/pull/11836) — 将旧版 HSM 实现迁移到 history service 下，并修复相关 lint 问题。由 @stephanos 提交。

---

## 社区热点

今日 Issue 和 PR 评论数整体偏低，热度相对集中在以下两条：

### 1. [#11822 SignalWithStart 不验证 cron schedules（新 Issue）](https://github.com/temporalio/temporal/issues/11822)
由 @dplyukhin 报告，指出 SDK 客户端在正常情况下会通过 Frontend 校验 `SignalWithStartWorkflowExecution` 的 cron 表达式，但 SDK 团队正在支持从 workflow 内部通过 System Nexus 发起 SignalWithStart，而这一路径**绕过了已有的校验逻辑**。该 Issue 无评论，但涉及 SDK 与 Server 的协作边界，后续可能会引发技术方案讨论。

### 2. [#11774 Fix SignalWithStart hang on orphaned current-execution pointer](https://github.com/temporalio/temporal/pull/11774)
该 PR 修复 Cassandra 存储层 current_executions 指针残留导致的 SignalWithStart 挂起问题（关联 #10841，该 Issue 目前已关闭）。由于 SignalWithStart 是 Temporal 的高频 API，此修复对使用 Cassandra 的长期运行集群尤为关键，存在较大潜在影响面。

---

## Bug 与稳定性

| 严重程度 | 问题 | 状态 | 修复 PR |
|---------|------|------|---------|
| 高 | SignalWithStart 在 System Nexus 路径下不校验 cron 表达式，可能接受非法调度（#11822） | 待讨论 | 暂无 |
| 高 | Cassandra 中 current_executions 指针残留导致 SignalWithStart 操作挂起（#10841） | Issue 已关闭 | [#11774](https://github.com/temporalio/temporal/pull/11774) 已提交修复 |
| 中 | ContinueAsNew 后 FirstWorkflowTaskBackoff 负值累积，导致退避时间无限增加 | 已定位 | [#11839](https://github.com/temporalio/temporal/pull/11839) |
| 中 | worker 关闭时 poll 注册竞态，可能丢失正在启动的 poll | 已定位 | [#11841](https://github.com/temporalio/temporal/pull/11841) |
| 中 | perNamespaceWorker 初始化数据竞争（动态配置回调在 ns 未初始化时触发） | 已定位 | [#11825](https://github.com/temporalio/temporal/pull/11825) |
| 低 | 可见性归档重复上传 S3/GCS，产生额外成本 | 已定位 | [#11807](https://github.com/temporalio/temporal/pull/11807) 提供 opt-in 去重 |

以上 PR 均已提交修复方案，等待 review 与合并，项目对稳定性问题的响应速度较快，整体健康度良好。

---

## 功能请求与路线图信号

- **可观测性增强**：`tdbg` 动态配置 CLI（#11722）与慢请求日志 namespace 标签（#11828）这两个功能表明项目正在强化运维诊断能力，预计会随下一个 minor 版本发布。
- **可见性归档成本优化**：#11807 的 S3/GCS 去重功能提供了 opt-in 的 SHA-256 内容感知去重，这是对用户存储成本痛点的直接响应，有较高概率被纳入近期版本。
- **Nexus 日志结构化**：[#11757 Tag Nexus logs by lifecycle stage](https://github.com/temporalio/temporal/pull/11757) 为 Nexus 请求日志增加 `nexus-stage` 标签（包括 caller-inbound、handler-queue 等 7 个阶段），有助于复杂链路排障，还在 review 中。
- **测试基础设施改进**：[#11830 Make test contexts safe to cache](https://github.com/temporalio/temporal/pull/11830) 与 [#11826 Use adaptive internal timing for Await](https://github.com/temporalio/temporal/pull/11826) 正在优化测试框架的上下文缓存与时间控制，属于内部工程质量提升。

---

## 用户反馈摘要

今日 Issue 评论较少，目前没有大量来自社区的声音，仅从已有数据中可提炼：

- **@dplyukhin（Temporal 员工）** 在 #11822 中反映 SDK 侧支持 SignalWithStart from workflow 的工作正在推进，但 Server 端校验缺失，暴露了 SDK 与 Server 功能对齐的协作盲区。这提示在跨组件功能开发时需同步更新相应校验逻辑，以避免行为不一致。
- **#11828 的来源为 Slack 请求（Yimin Chen）**，说明内部工程师在排查慢请求时因日志缺少 namespace 标签而效率受限。这一反馈直接转化为了 PR，体现了项目内部反馈闭环的高效。

---

## 待处理积压

| PR/Issue | 创建时间 | 最后更新时间 | 备注 |
|---------|---------|------------|------|
| [#10118 Implement namespace soft deletion](https://github.com/temporalio/temporal/pull/10118) | 2026-04-29 | 2026-08-28 | 已持续 4 个月，实现 namespace 软删除与恢复，涉及状态机变更，需要维持 review 关注 |
| [#10502 DLQ pure task validation](https://github.com/temporalio/temporal/pull/10502) | 2026-06-03 | 2026-08-28 | reliability-2026 关键项，防止任务卡死，建议推进合并 |
| [#11648 Worker command task queue kind 文档](https://github.com/temporalio/temporal/pull/11648) | 2026-08-19 | 2026-08-28 | 文档补充类 PR，等待 review，积压时间 9 天 |
| [#11629 Validate schedule inputs and preserve V2 IDs](https://github.com/temporalio/temporal/pull/11629) | 2026-08-18 | 2026-08-27 | Schedule 输入校验 + V2 ID 保留，涉及调度语义，建议加快 review 周期 |

---

**总结**：Temporal 项目当前处于高强度开发迭代期，PR 活跃度极高，大量可靠性修复与 CHASM 集成工作并行推进。社区 Issue 讨论虽少，但工程侧对稳定性问题的响应速度值得肯定。建议关注 #11822 的后续讨论（SignalWithStart 校验缺失），以及 #11774 的合并进度（Cassandra 用户受影响面较大）。项目整体健康度良好，无重大阻塞性问题。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*