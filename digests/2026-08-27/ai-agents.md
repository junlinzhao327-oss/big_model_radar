# OpenClaw 生态日报 2026-08-27

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-27 03:22 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告



---

## 横向生态对比

# 开源 AI 智能体生态横向对比分析报告（2026-08-27）

> 说明：OpenClaw、Hermes Agent、Pi 今日摘要为空，以下涉及部分仅作生态位定性判断，不作活跃度量化。

---

## 1. 生态全景

当前开源个人 AI 助手/自主智能体生态已从“单点演示”进入 **工程化与平台化并进** 阶段。OpenHands SDK 聚焦 Agent 开发框架与子代理编排，LiteLLM 在模型网关/成本治理侧高速迭代，Temporal 则持续加固工作流可靠性底座。社区关注点正从“能否跑通”转向 **并发能力、成本精确度、安全审计、可观测性和部署模块化**。各项目之间的边界逐渐清晰：应用层、SDK 层、网关层、编排层各有代表，且开始通过 ACP 等协议进行横向互操作与基准对比。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | Release | 健康度评估 |
|---|---|---|---|---|
| **OpenHands SDK** | 28 条（19 新开/活跃、9 关闭） | 21 条（13 待合并、8 合并/关闭） | 无 | 高：架构优化与生态扩展并行；高优 Bug #4537 阻塞 UI 可用性 |
| **LiteLLM** | 96 条（53 新开/活跃、43 关闭） | 402 条（221 待合并、181 合并/关闭） | v1.100.0-dev.1 | 很高：吞吐量大、迭代快；PR 积压明显，存在安全类遗留问题 |
| **Temporal** | 3 条（全部新开） | 68 条（17 合并/关闭、51 待合并） | 无 | 高：以稳定性加固为主，PR 队列活跃且方向集中 |
| **OpenClaw** | 无数据 | 无数据 | 无数据 | 无法评估（今日摘要为空） |
| **Hermes Agent** | 无数据 | 无数据 | 无数据 | 无法评估 |
| **Pi** | 无数据 | 无数据 | 无数据 | 无法评估 |

**小结**：LiteLLM 活跃度最高，OpenHands SDK 次之，Temporal 表现为“低 Issue 噪声、高 PR 质量”的巩固型活跃。

---

## 3. OpenClaw 在生态中的定位

今日没有 OpenClaw 的社区动态数据，无法量化其优势、技术路线领先性或社区规模。从生态位看：

- **OpenClaw** 属于最上层的 **个人 AI 助手/终端用户入口**，理论上整合模型、工具、记忆和自动化流程。
- **OpenHands SDK** 更靠近 **开发者基础设施**，提供子代理委派、Agent Canvas、ACP 评估等能力。
- **LiteLLM** 处于 **模型接入与治理层**，核心是统一网关、成本核算和企业管理。
- **Temporal** 则位于 **工作流可靠性底座**，为需要持久化执行的 Agent 任务提供分布式编排。

如果 OpenClaw 以“个人 AI 助手”为核心定位，其与同类项目的差异将是：**不是面向开发者的 SDK，也不是面向运维的网关，而是直接面向终端用户的自主智能体宿主**。社区规模与竞争力数据需补充后方可评估。

---

## 4. 共同关注的技术方向

| 方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **成本精确性与计费可观测** | LiteLLM、OpenHands SDK | LiteLLM 修复重叠 token 双重计费、Azure 价格错配；OpenHands Harness Watch 将成本/性能纳入多 harness 对比 |
| **并发与状态一致性** | OpenHands SDK、Temporal | OpenHands 子代理委派持锁

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-08-27

## 1. 今日速览

过去 24 小时项目活跃度极高：28 条 Issue 更新（19 新开/活跃、9 关闭）与 21 条 PR 更新（13 待合并、8 已合并/关闭），无新版本发布。核心动态集中在三个方面：一是 **Harness Watch 史诗**（#4627）正式启动，派生 8 个 P0/P1 子任务，目标是将 OpenCode、Pi、Hermes 纳入 ACP 评估体系并实现确定性对比；二是 **agent-server 镜像瘦身与模块化**成为明确方向（#4643、#4645），当前 34.5% 镜像体积来自可选的 VNC/Chromium/OpenVSCode 桌面栈；三是 **高优 Bug #4537（TaskToolSet 持锁导致 UI 冻结）** 仍在讨论中，直接阻塞 Agent Canvas 在委派任务期间的可用性。整体来看，项目处于架构优化与生态扩展并行的高活跃期。

## 2. 版本发布

过去 24 小时无新版本发布。

## 3. 项目进展

今日合并/关闭的关键 PR 主要集中在 **Bug 修复、文档完善与代码清理**，没有引入全新功能，但修复了几个直接影响用户体验的问题：

- **[#4517] fix: enable condenser for subscription LLMs via existing completion dispatch**（合并）— 修复高优 Bug #4515：ChatGPT 订阅类 LLM（如 `openai/gpt-5.6-sol`）因走错 API 端点导致上下文压缩永不触发。修复后订阅用户不再因 `ContextWindowExceededError` 断线。这是一个跨越 9 天的核心修复，对订阅制用户价值明显。链接: https://github.com/OpenHands/software-agent-sdk/pull/4517
- **[#4649] fix(critic): default CriticResult.message to None for exclude_none round-trip**（合并）— `CriticResult.message` 因缺少 `default=None` 被 Pydantic 视为必填字段，导致会话恢复失败（事件持久化时 `exclude_none=True` 丢弃该字段）。这是会话恢复链上的一个隐蔽正确性修复。链接: https://github.com/OpenHands/software-agent-sdk/pull/4649
- **[#4618] fix(agent-server): detect all secret-bearing fields for the plaintext-save warning**（合并）— 修复 #4609：明文保存警告此前只检测 `llm.api_key`，漏掉 `critic_api_key`、MCP secrets 和 `agent_context.secrets`。属于安全收口性修复。链接: https://github.com/OpenHands/software-agent-sdk/pull/4618
- **[#4648] docs: refresh AGENTS.md guidance**（合并）— 由自动化 bot 提交，对齐根目录与子目录 AGENTS.md 的持久化不变量说明。链接: https://github.com/OpenHands/software-agent-sdk/pull/4648
- **[#3673] feat(sdk): add ask_oracle tool**（合并）— 新增 `Oracle` 工具，让 agent 在遇到困难时可以向更强的 LLM 请求二次意见。属于 agent 能力的正向扩展。链接: https://github.com/OpenHands/software-agent-sdk/pull/3673
- **[#4655] docs(examples): align Ask Oracle conventions**（关闭）— 与 #3673 配套的示例文档调整。链接: https://github.com/OpenHands/software-agent-sdk/pull/4655
- **[#4656] docs(agent): add docstrings for image helper functions**（关闭）— 为三个图像相关辅助函数补充文档。链接: https://github.com/OpenHands/software-agent-sdk/pull/4656
- **[#4101] feat(agent-server): publish python-lite image**（关闭）— 该 PR 被 #4643 取代（镜像构建重构方案范围扩大）。链接: https://github.com/OpenHands/software-agent-sdk/pull/4101

此外，还有若干小型 SDK 修复 PR 处于待合并状态，包括 provider-only model ID 校验（#4647）、Gemini API key 优先级修复（#4646）、namespaced model ID 前缀剥离修复（#4438）等。

## 4. 社区热点

今日讨论最活跃的 Issue 呈现一个共同主题：**子代理（subagent）委派机制的智能化与并发化**。

- **[#2186] feat(delegation): Advanced Features for Markdown-based Agents** — 15 条评论，👍 1。追踪基于 Markdown 的 agent 尚缺的高级功能（逐项列表已有部分完成）。这是社区对委派能力深度扩展的长期需求，讨论热度最高。链接: https://github.com/OpenHands/software-agent-sdk/issues/2186
- **[#2047] feat(delegate): Non-blocking background subagent execution** — 7 条评论。反对 `thread.join()` 阻塞父 agent，要求支持后台执行子任务。与 #2186 形成呼应，显示用户对 **父 agent 并行处理能力** 的强烈需求。链接: https://github.com/OpenHands/software-agent-sdk/issues/2047
- **[#4537] TaskToolSet delegation holds parent ConversationState lock** — 5 条评论，👍 1，`priority: high`。用户报告实际的性能灾难：委派子 agent 期间整个会话列表冻结。这条 Issue 将并发需求从"更好"升级为"必须修"。链接: https://github.com/OpenHands/software-agent-sdk/issues/4537
- **[#4624] Add Antigravity CLI as a new ACP provider** — 4 条评论。社区希望新增 ACP provider 的呼声持续，且#4624 描述被重写以反映已验证的发现，说明维护者在认真对待。链接: https://github.com/OpenHands/software-agent-sdk/issues/4624

**分析**：社区关注的焦点已经从"agent 能否委派"转向"委派时的并发/性能/体验"。`#4537` 直接暴露了当前架构在真实并发场景下的短板——它很可能是 #2047 和 #2186 所代表的并发诉求的"引爆点"。修复 #4537 将解锁一大波与子代理编排相关的功能需求。

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue | 描述 | Fix PR 状态 |
|---|---|---|---|
| 🔴 高 | [#4537](https://github.com/OpenHands/software-agent-sdk/issues/4537) | TaskToolSet 持有 ConversationState 锁，导致 executor pool 饱和 + Agent Canvas UI 冻结 | **无**。仍在讨论中，暂无对应 PR |
| 🔴 高 | [#4515](https://github.com/OpenHands/software-agent-sdk/issues/4515)（已关闭） | 订阅 LLM 的 condenser 永不触发，最终 ContextWindowExceededError | ✅ 已由 #4517 修复 |
| 🟠 中 | [#4629](https://github.com/OpenHands/software-agent-sdk/issues/4629) | 已废弃的 gemini-cli OAuth 认证方式优先级高于可用的 API key；Gemini pin 版本过期，且未随 Google 2026-06-18 消费者级 cutoff 更新 | ✅ PR #4646 已提交修复认证优先级 |
| 🟠 中 | [#4653](https://github.com/OpenHands/software-agent-sdk/issues/4653)（新开） | `run-examples` CI 中 `28_ask_agent_example.py` 因"orphaned tool_use without tool_result"收到 Anthropic 400 错误 | **无**。AI bot 报告，刚创建 |
| 🟠 中 | [#4077](https://github.com/OpenHands/software-agent-sdk/issues/4077) | 流式 token/delta 管线存在正确性与资源安全 bug（durable record 正确，但实时路径有缺陷） | **无**。已开放 48 天 |

另有两个已关闭的自动化/清理项：`#4633`（事件触发 issue triage 的自动化测试）和 `#4609`（明文 secret 警告缺失，已由 PR #4618 修复）。

**评估**：#4537 是当前最严重的未修复 Bug，直接影响核心 UI 可用性；#4515 的修复已在今日落地，稳定性的最大胜利。整体 Bug 雷达上有 3 个未修复的中高优问题，值得关注。

## 6. 功能请求与路线图信号

今日新开功能请求/路线图条目，按信号强度排列：

- **Harness Watch 史诗（#4627）及 8 个子任务** — 这是一个完整的路线图信号：自动对比 OpenHands、OpenCode、Pi、Hermes 四个 ACP harness 的性能与成本。P0 子任务包括：#4634（add Hermes）、#4635（add Pi）、#4639（add OpenCode）、#4637（scheduled comparisons）、#4638（capture proxy telemetry）、#4642（deterministic paired reports）；P1 为 #4641（diagnose differences）。链接: https://github.com/OpenHands/software-agent-sdk/issues/4627
- **[#4654] Select an LLM profile for an individual task-tool worker**（新开，ready-for-dev）— 父 agent 无法为单个委派任务选择保存的 LLM profile。已有对应 PR #4510（feat(tools): add per-call llm_profile override），大概率进入下一版本。链接: https://github.com/OpenHands/software-agent-sdk/issues/4654
- **[#4645] Make OpenVSCode Server, Chromium, and the desktop stack optional**（新开，ready-for-dev）— 量化证据：564.9 MB compressed（占镜像 34.5%）的无条件安装。与 #4643 的镜像构建重构形成呼应，是明确的架构优化方向。链接: https://github.com/OpenHands/software-agent-sdk/issues/4645
- **[#4643] Reorganise agent-server image build — selectable capabilities**（新开，ready-for-dev）— 取代 #4067 的更大范围镜像重构方案。链接: https://github.com/OpenHands/software-agent-sdk/issues/4643
- **[#4624] Add Antigravity CLI as a new ACP provider**（已重写）— 社区持续要求扩展 ACP provider 列表。链接: https://github.com/OpenHands/software-agent-sdk/issues/4624
- **[#4239] Multi-repo/Cross-repo Awareness**（已有 👍 2）— 期望 agent 自动感知同一组织内其他依赖仓库。这是深度使用者的典型痛点，尚在 roadmap 阶段。链接: https://github.com/OpenHands/software-agent-sdk/issues/4239

**判断**：ACP 生态扩展（尤其是 OpenCode、Pi、Hermes 的评估纳入）和镜像模块化是当下最明确的路线图方向；LLM profile 级联（#4654/#4510）则是最可能快速合入的功能增强。

## 7. 用户反馈摘要

从今日 Issues 评论中提炼的用户真实反馈：

- **委派期间 UI 冻结是真实痛点**（#4537）："Agent Canvas conversation list stops rendering for the entire duration of the delegated task" —— 用户在多轮委派场景下无法看到新消息，交互被完全阻断。这很可能引发社区对 `#2047`（非阻塞后台执行）的更强烈呼吁。
- **订阅 LLM 用户的上下文压缩失效**（#4515）：用户发现订阅 `gpt-5.6-sol` 的会话会硬生生撞上 ContextWindowExceededError，而不是优雅地压缩继续。这类问题影响的是平台的可靠性信任。
- **OAuth 残留凭据干扰正常工作流**（#4629）：用户从 Gemini CLI 迁移后，`~/.gemini/oauth_creds.json` 中的陈旧 OAuth 凭据优先级压过了可用的 `GEMINI_API_KEY`。"A retired auth method outranks a working one" 的措辞反映出用户对此行为的不解与挫败。
- **镜像体积问题开始被关注**（#4645）：有用户/维护者量化指出 34.5% 的镜像体积来自非必需组件，暗示了对拉取时间、磁盘占用和攻击面的隐忧。
- **维护者对自动化流程的自我验证**（#4633）：事件触发的 issue triage 自动化正在测试中，说明项目在尝试减少人工维护开销，长期看有利于响应速度。

## 8. 待处理积压

以下 Issue/PR 长期未得到解决或响应，值得维护者关注：

- **[#4239] Multi-repo/Cross-repo Awareness** — 创建于 2025-09-23，开放近一年，👍 2。这是来自深度用户的真实需求（前后端仓库依赖场景），但一直停留在 roadmap 层面，至今无 PR 或设计文档。链接: https://github.com/OpenHands/software-agent-sdk/issues/4239
- **[#3557] fix(agent-server): don't bump explicit_interrupt_generation on no-op pause/interrupt**（PR）— 创建于 2026-06-07，旨在修复暂停/中断卡死回归（All-Hands-AI/OpenHands#14698），已开放 81 天且待合并。长时间无进展可能意味着该问题较难验证或优先级被压低。链接: https://github.com/OpenHands/software-agent-sdk/pull/3557
- **[#4419] feat(sdk): register Pi as a built-in ACP provider**（PR）— 创建于 2026-08-07，与今日新开的 #4635（Harness Watch: Add Pi）直接相关。如果 #4635 推进落地，这个 PR 应当同步 revive。链接: https://github.com/OpenHands/software-agent-sdk/pull/4419
- **[#4077] Streaming: correctness & resource-safety bugs in token/delta pipeline** — 开放 48 天，无修复 PR。涉及 `llm.py → on_token → PubSub → WebSocket` 全链路，影响流式实时性，技术排查难度可能较高。链接: https://github.com

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报（2026-08-27）

> 数据来源：GitHub `BerriAI/litellm` 过去 24 小时 Issues / PR / Releases 动态

---

## 1. 今日速览

过去 24 小时项目整体非常活跃：**96 条 Issue 更新**（新开/活跃 53 条，已关闭 43 条），**402 条 PR 更新**（待合并 221 条，已合并/关闭 181 条）。从数据看，Issue 关闭率约 45%，PR 合并/关闭率约 45%，维护团队响应速度处于较高水平，但待合并 PR 数量仍大于已合并数量，存在一定积压。今日发布了 `v1.100.0-dev.1` 开发版，主要附带 Docker 镜像签名验证说明。重点修复方向集中在**成本计算准确性**、**缓存计费**、**Schema 兼容性**和**管理 UI 可用性**，同时社区对 **Rust 迁移**、**Prisma 依赖调整**和 **Dark Mode** 等话题关注度很高。

---

## 2. 版本发布

### v1.100.0-dev.1

- 发布链接：https://github.com/BerriAI/litellm/releases/tag/v1.100.0-dev.1
- 类型：开发版（dev）
- 主要内容：
  - 补充了所有 LiteLLM Docker 镜像的 **cosign 签名校验说明**。
  - 每个发布版本均使用同一签名密钥，密钥引入于 commit `0112e53`。
- 破坏性变更：当前信息中未见明确破坏性变更说明。
- 迁移注意事项：由于是 dev 版本，不建议直接用于生产；若需要验证镜像来源，可参考签名校验文档。

---

## 3. 项目进展

过去 24 小时 PR 活动非常密集，虽然多数 key PR 仍处于待合并状态，但已有若干重要改动被合并/关闭。今日较关键的有：

- **修复重叠缓存/多模态 token 双重计费**
  - [PR #37407 fix(cost): stop double-billing cached tokens that overlap a modality](https://github.com/BerriAI/litellm/pull/37407) — 已关闭
  - [PR #38001 fix(cost): stop double-billing overlapping cached and modality input tokens](https://github.com/BerriAI/litellm/pull/38001) — 已关闭
  - 这两个 PR 解决的是同一类问题：当 provider 返回的 `cached_tokens` 与 image/audio/video 等 modality token 存在重叠时，旧逻辑会重复计费，导致实际账单偏高。例如 xAI grok-4.6 场景下日志计费比官方账单高约 72%。

- **复杂度路由器支持 heuristic-first 分类链**
  - [PR #38428 feat(complexity_router): heuristic-first classifier chaining](https://github.com/BerriAI/litellm/pull/38428) — 已关闭
  - 新增 `classifier_type: heuristic_first`，先本地启发式打分，再决定是否调用 LLM classifier，可显著降低简单请求的 classifier 调用成本。

- **其他正在推进的功能型 PR（待合并）**
  - [PR #38452 fix: keep schema reconciliation from fighting a partitioned LiteLLM_SpendLogs](https://github.com/BerriAI/litellm/pull/38452) — 修复分区 SpendLogs 被 schema reconciliation 干扰的问题。
  - [PR #38438 feat(alerting): slack alerts for per-user daily/monthly spend thresholds and spend anomaly detection](https://github.com/BerriAI/litellm/pull/38438) — 新增用户级花费阈值与异常检测 Slack 告警。
  - [PR #38445 feat(proxy): cyberark conjur secret manager configuration via Admin UI](https://github.com/BerriAI/litellm/pull/38445) — 为 CyberArk Conjur 密钥管理增加 Admin UI 配置入口。
  - [PR #38443 feat(scim): assign SCIM-provisioned teams to organizations from group display name mappings](https://github.com/BerriAI/litellm/pull/38443) — SCIM 团队同步支持自动映射到组织。
  - [PR #38442 / #38432 cache observability in request logs](https://github.com/BerriAI/litellm/pull/38442) — 请求日志增加缓存命中/未命中过滤器与 session 级缓存可观测性。

总体判断：项目正在往**更精确的成本核算、更细粒度的可观测性、更完善的企业管理能力**三个方向稳步前进。

---

## 4. 社区热点

今日最受关注的 Issue/PR 有以下几类：

### 1. 高赞 UI 需求：Dark Mode

- [Issue #10177 [Feature]: Dark Mode](https://github.com/BerriAI/litellm/issues/10177)
- 创建于 2025-04-20，已有 **65 条评论、74 个 👍**，最近仍在讨论。
- 用户原话："Please add a dark theme to the UI panel. I'm going blind."
- 分析：虽然只是一个主题功能，但长期占据高热度，说明 LiteLLM 管理面板的日常使用频率很高，社区对 UI/UX 基础体验有强烈诉求。

### 2. 架构与依赖担忧：Prisma Python client 弃用

- [Issue #9753 Notice: Deprecation of the Prisma Python client](https://github.com/BerriAI/litellm/issues/9753)
- 20 条评论，讨论集中在 LiteLLM 是否计划迁移出 Prisma，因为上游 `prisma-client-py` 可能停止维护。
- 分析与 `#26886 Prisma reconnection failed` 相结合，表明 Prisma 相关稳定性和长期维护风险正在成为社区关注焦点。

### 3. 主打路线图：LiteLLM Rust Migration

- [Issue #31263 LiteLLM Rust Migration - the fastest and litest AI Gateway (sub 1ms overheads)](https://github.com/BerriAI/litellm/issues/31263)
- 20 条评论，17 个 👍，由团队发起，作为 Rust 迁移的总 parent ticket。
- 分析：这是项目的重大技术路线信号，社区参与度高，围绕性能、部署体积和兼容性都有讨论。

### 4. 成本/计费问题引发强烈共鸣

- [Issue #13781 OpenAI GPT-5 Chat model does not support "temperature" parameter](https://github.com/BerriAI/litellm/issues/13781) — 11 条评论、20 个 👍，已关闭。
- [Issue #36192 Azure GPT-5.6 terra/luna cost-map rows carry OpenAI's prices](https://github.com/BerriAI/litellm/issues/36192) — 9 条评论，已关闭。
- 分析：用户对模型参数兼容性和不同 provider 定价差异非常敏感，尤其是 Azure 与 OpenAI 直连价格不一致导致成本统计错误。

---

## 5. Bug 与稳定性

以下按严重程度排列今日值得关注的 Bug/回归问题：

### 🔴 高严重度：安全问题

- **[Issue #24530 /metrics endpoint default-unauthenticated exposes multi-tenant PII in production deployments](https://github.com/BerriAI/litellm/issues/24530)**
  - 状态：OPEN
  - 问题：`/metrics` Prometheus 端点默认无需认证，在多租户生产环境可能泄露敏感数据。
  - 是否已有 fix：目前未见对应修复 PR。

- **[Issue #36898 GET /health returns extra_headers and aws_session_token in plaintext](https://github.com/BerriAI/litellm/issues/36898)**
  - 状态：CLOSED
  - 问题：`/health` 接口会明文返回 `extra_headers` 和 `aws_session_token`。
  - 是否已有 fix：该 issue 已关闭，疑似已修复。

### 🟠 高严重度：成本统计回归

- **[Issue #36094 azure/gpt-5.6-luna under-reports cost by 5x on main (Regression after v1.95.0)](https://github.com/BerriAI/litellm/issues/36094)**
  - 状态：CLOSED
  - 问题：`azure/gpt-5.6-luna` 成本少报 5 倍，属于 v1.95.0 后的回归。
  - 是否已有 fix：已关闭，应已修复。

- **[Issue #36192 Azure GPT-5.6 terra/luna cost-map rows carry OpenAI's prices, not Azure's published meters](https://github.com/BerriAI/litellm/issues/36192)**
  - 状态：CLOSED
  - 问题：Azure 模型价格沿用了 OpenAI 的降价，但 Azure 从未降价。
  - 是否已有 fix：已关闭。

### 🟡 中严重度：稳定性与功能异常

- **[Issue #26886 [Bug]: Prisma reconnection failed](https://github.com/BerriAI/litellm/issues/26886)**
  - 状态：OPEN，15 条评论
  - 问题：LiteLLM Proxy Pod 周期性不稳定，Pr

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-27

## 1. 今日速览

过去24小时内，Temporal 核心仓库保持高活跃度：共产生 3 个新 Issue，全部处于开放状态；PR 活动频繁，累计 68 条更新，其中 17 条已合并/关闭，51 条待合并。值得关注的是，多个 PR 聚焦于可靠性提升（如 ServiceErrorInterceptor 与 Visibility 查询转换器的 panic 捕获）以及多集群复制、Nexus 等基础设施的稳定性增强；同时社区报告的 Ringpop 升级后成员震荡问题持续发酵（9条评论、4个👍）。今日无新版本发布，整体项目健康度良好，维护力量集中在稳定性加固和已知 Bug 修复上。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

过去 24 小时内有 17 条 PR 被合并或关闭，涵盖可靠性、Nexus 协议完善、复制流改进等多个方向。以下为关键变化：

- **Nexus 取消请求增加失败能力**（[#11808](https://github.com/temporalio/temporal/pull/11808)，已关闭）：在 Nexus 取消请求中增加 Temporal failure 响应能力头，并遵循 `nexusoperation.useNewFailureWireFormat` 动态配置。这补齐了 Nexus 开始请求与取消请求之间错误传播能力的对称性，对跨集群 Nexus 操作的可观测性和调试有实际意义。
- **修复 SignalWithStart 绕开 continue-as-new backoff**（[#11810](https://github.com/temporalio/temporal/pull/11810)，开放中）：该 PR 使 SignalWithStart 在 continue-as-new 后等待首个工作流任务 backoff，行为与其他场景保持一致，并附带单元测试。如果合并，将修复一个可能导致工作流任务被立即调度、违反 backoff 语义的隐患。
- **混合脑进程混沌测试报告**（[#11814](https://github.com/temporalio/temporal/pull/11814)，开放中）：新增混合脑（mixed-brain）场景下的进程重启混沌测试报告机制，支持以可配置的一分钟默认周期重启 Omes dev server，并在重启后等待所有成员端口就绪。这有助于完善多集群场景下的故障注入测试覆盖。
- **复制流命名空间隔离 5-PR 系列持续推进**（[#11305](https://github.com/temporalio/temporal/pull/11305)，开放中）：该系列目标是为复制流增加按命名空间隔离的 lane 机制，当前 PR 为第 5 部分，依赖前面的隔离管理器等基础工作。

整体来看，项目在可靠性加固（panic 捕获）、Nexus 协议成熟度、复制隔离性三个方向均有实质推进，且有大量 PR 处于活跃迭代中。

---

## 4. 社区热点

- **[#9987] Ringpop membership churn after upgrade to v1.30.x**（[链接](https://github.com/temporalio/temporal/issues/9987)）— 评论 9 | 👍 4
  这是过去 24 小时讨论热度最高的问题。用户从 v1.29.x 升级到 v1.30.x 后，Ringpop 成员环无法在 Pod 启动后数秒内收敛，导致各服务（frontend、history、matching、worker）看到的可达成员列表不一致，影响服务间 gRPC 调用。该问题已持续数月（4 月创建），至今仍开放且获得较多关注，说明升级路径的稳定性是社区核心诉求之一。

- **[#11794] timer_map collection in executions table can contain 10K's of entries**（[链接](https://github.com/temporalio/temporal/issues/11794)）— 评论 1 | 👍 0
  用户对 executions 表中 `timer_map` 可能包含数万条条目表示担忧，并贴出客户在 ScyllaDB 上的实际案例截图。虽然帖子简短，但直指存储层潜在的低效问题，若属实可能对大规模部署的性能和存储成本产生影响。

---

## 5. Bug 与稳定性

今日报告的 3 个 Issue 全部标记为 `[potential-bug]`，按严重程度排列如下：

- **高：Ringpop 成员震荡（升级回归）**（[#9987](https://github.com/temporalio/temporal/issues/9987)）
  从 v1.29.x 升级至 v1.30.x 后，Ringpop 成员环无法正常收敛，服务间发现异常、gRPC 调用受影响。属于升级回归类问题，影响面较大，且已持续数月无修复 PR 关联，值得维护团队优先排查。

- **中：executions 表 timer_map 条目异常膨胀**（[#11794](https://github.com/temporalio/temporal/issues/11794)）
  客户在 ScyllaDB 上观察到单个 executions 行的 `timer_map` 中出现上万个条目。这可能是写入路径上的 bug，也可能是时序逻辑导致的异常累积。当前无明确 fix PR，需进一步确认是否与 ScyllaDB 存储引擎的特定行为有关。

- **中：Postgres Visibility 列表 API 过滤含问号字符串失败**（[#11797](https://github.com/temporalio/temporal/issues/11797)）
  当字符串过滤值包含问号（`?`）时，Postgres 上的 Visibility 列表 API 过滤失效。这会影响用户对自定义搜索属性的灵活查询。同日有一系列 Visibility SQL 查询转换器修复 PR 在队列中（如 [#11801](https://github.com/temporalio/temporal/pull/11801)），其中包含多项解析修复，是否覆盖该场景值得关注。

此外，多个 `[reliability-2026]` 标签的 PR（如 [#11813](https://github.com/temporalio/temporal/pull/11813)、[#11800](https://github.com/temporalio/temporal/pull/11800)、[#11801](https://github.com/temporalio/temporal/pull/11801)）正在为服务顶层拦截器和 Visibility 查询转换器增加 panic 捕获，这些加固措施能显著降低未处理异常导致服务崩溃的风险。

---

## 6. 功能请求与路线图信号

当前 PR 序列透露了以下路线图信号：

- **可靠性 2026（reliability-2026）**：多个 PR 均带有 `reliability-2026` 标签，包括 panic 捕获（[#11813](https://github.com/temporalio/temporal/pull/11813)、[#11800](https://github.com/temporalio/temporal/pull/11800)）和 Visibility 查询转换器修复（[#11801](https://github.com/temporalio/temporal/pull/11801)）。这说明项目将系统性地提升各层级的容错能力，预计未来版本会持续纳入此类加固。
- **SignalWithStart 语义修正**（[#11810](https://github.com/temporalio/temporal/pull/11810)）：修复 continue-as-new 场景下的 backoff 行为，属于工作流语义的正确性改进，可能进入下一补丁版本。
- **调度器（Schedule）功能增强**：多个相关 PR 在推进中，如 [#11629](https://github.com/temporalio/temporal/pull/11629)（校验调度输入并保留 V2 IDs）和 [#11588](https://github.com/temporalio/temporal/pull/11588)（修复刷新后的调度动作延迟），表明调度工作流的健壮性正在持续完善。
- **复制流命名空间隔离**（[#11305](https://github.com/temporalio/temporal/pull/11305)）：5-PR 系列的目标是实现复制流的按命名空间 lane 隔离，这是一个较大的架构演进，可能影响多集群复制的性能和故障域隔离能力。
- **系统 worker 服务默认启用**（[#11812](https://github.com/temporalio/temporal/pull/11812)）：计划在功能测试集群中默认启用 worker-service 主机进程，并将按命名空间的 SDK worker 数量改为动态配置控制，这可能是生产环境部署系统 worker 的前置步骤。

---

## 7. 用户反馈摘要

- **升级稳定性是第一诉求**（[#9987](https://github.com/temporalio/temporal/issues/9987)）：用户明确描述了从 v1.29.x 升级到 v1.30.x 后的预期行为（Pod 启动后数秒内 Ringpop 收敛）与实际行为（成员环持续震荡）之间的差距。评论数达 9 条，说明该问题受到较多用户关注或受影响，社区期望维护者尽快定位修复。
- **对存储效率的担忧**（[#11794](https://github.com/temporalio/temporal/issues/11794)）：用户以“suboptimal”评价 `timer_map` 出现数万条目的现象，并主动怀疑是否存在潜在 bug，反映出用户对大规模场景下 Temporal 存储占用的敏感度较高。
- **对查询灵活性的期望**（[#11797](https://github.com/temporalio/temporal/issues/11797)）：用户引用官方文档指出，文档未对字符串过滤值做字符限制，因此期望任意字符串都能正常工作。这属于文档与实现不一致的体验问题，需要从 query converter 修复和文档明确两方面入手。

---

## 8. 待处理积压

以下 PR/Issue 长期未关闭，建议维护者关注：

- **[#9076] Programmable grpc fault injection**（[链接](https://github.com/temporalio/temporal/pull/9076)）：创建于 2026-01-19，已开放 7 个月。该 PR 为功能测试增加 gRPC 故障注入能力，对提升测试覆盖有长期价值，但长期处于开放状态，可能需要维护者评估是否继续推进或关闭。
- **[#10095] Mutation testing tool [WiP]**（[链接](https://github.com/temporalio/temporal/pull/10095)）：创建于 2026-04-28，已被标记为 `[stale]`。变异测试工具能有效提升测试质量，但该 PR 长期未实质更新，建议明确其状态（继续开发/关闭/移交）。
- **[#9987] Ringpop membership churn**（[链接](https://github.com/temporalio/temporal/issues/9987)）：4 月创建至今仍开放，已积累 9 条评论和 4 个 👍。该 Issue 涉及升级回归，影响面广，应优先排期排查，避免影响用户升级信心。

---

*本日报由 AI 生成，数据来源于 Temporal GitHub 仓库公开信息，统计窗口为 2026-08-26 至 2026-08-27。*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*