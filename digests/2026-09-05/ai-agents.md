# OpenClaw 生态日报 2026-09-05

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-05 00:11 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-09-05

## 今日速览

过去24小时内 OpenClaw 仓库继续保持极高的社区活跃度：新增/活跃 Issue 439 条、PR 更新 500 条，评论密集集中于 P1 级 Bug（会话状态丢失、消息静默丢弃、多代理编排不稳）与长期悬而未决的产品决策议题。虽然今日无新版本发布，但维护者提交了近 20 个高优先级修复 PR（涉及 Codex 推理恢复、会话 yield 历史保留、SQLite 事务优化等），整体呈现“高活跃度、高积压、快修复”并行的态势——Issue 中大量存在 `no-new-fix-pr` + `needs-maintainer-review` 标签的积压问题，同时新一轮 PR 链正在快速形成闭环。核心关键词：**稳定性修复密集推进，版本节奏暂缓，社区对数据丢失/消息丢失类 Bug 关注度极高**。

---

## 项目进展

今日无新版本发布（0 个 Releases），合并/关闭 PR 152 个。以下聚焦接近合并或已完成维护者审查的高价值 PR：

- **[#138372 [CLOSED] chore(i18n): refresh native locales](https://github.com/openclaw/openclaw/pull/138372)** — 机器人 PR，刷新 21 种原生应用语言（Android phone/Wear、iOS/watchOS、macOS），覆盖 47 个新增字符串。唯一已合并的 PR。
- **[#138697 fix: recover stale Windows owners when exited PIDs return EPERM](https://github.com/openclaw/openclaw/pull/138697)**（P2, proof: sufficient, ready for maintainer look）— 修复 Windows 上已退出进程 PID 仍返回 EPERM 导致陈旧锁/数据库租约无法恢复的问题。来自真实 Gateway 恢复事故。
- **[#138334 fix(sessions): keep custom session icon across /reset](https://github.com/openclaw/openclaw/pull/138334)**（P2, proof: sufficient, proof: telegram-e2e, ready for maintainer look）— 修复 `/reset` 后自定义会话图标丢失，保留操作者自定义外观。
- **[#138710 fix(sqlite): avoid writes when reacquiring data-free coordinators](https://github.com/openclaw/openclaw/pull/138710)**（P2, ready for maintainer look）— 避免空协调器锁获取时产生无谓 SQLite journal 写放大。
- **[#138655 improve(gateway): reduce work for oversized chat history updates](https://github.com/openclaw/openclaw/pull/138655)**（P3, proof: sufficient, ready for maintainer look）— 针对超大聊天历史追更进行 CPU/临时内存优化。

另有大量 P1/P2 PR 处于 `📣 needs proof` 状态，集中在 Codex 推理恢复（[#138595](https://github.com/openclaw/openclaw/pull/138595)）、全权限任务重启后丢工具（[#138701](https://github.com/openclaw/openclaw/pull/138701)）、递归子代理会话（[#138059](https://github.com/openclaw/openclaw/pull/138059)）等方向。整体来看，**项目正密集修复 2026.7.x ~ 2026.9.x 线路上积累的会话状态与消息投递质量问题。**

---

## 社区热点

今日讨论最热的 5 条 Issue（按评论数排序），深层共同指向 **“会话状态可靠性与信令完整性”**：

- **[#44925 [P1, diamond lobster] Subagent completion silently lost — no retry, no notification, no auto-restart on timeout](https://github.com/openclaw/openclaw/issues/44925)**（评论 26，👍 2）— 子代理任务在 E31/E42/E45 等多种失败模式下结果静默丢失，无重试、无通知、无自动重启。**诉求：为子代理完成通知建立端到端确认与恢复机制。** 已打 `needs-product-decision` 标签，无 fix PR。
- **[#22438 [P2] feat: Tiered bootstrap file loading for progressive context control](https://github.com/openclaw/openclaw/issues/22438)**（评论 18）— 大型工作区用户请求分级加载 bootstrap 文件以节省上下文窗口。**诉求：对 token 成本敏感的生产用户群体日益庞大。** 已打 `linked-pr-open`，说明已有实现进行中。
- **[#38327 [P1, diamond lobster] "Cannot convert undefined or null to object" in 2026.3.2 with google-vertex/gemini-3.1-pro-preview](https://github.com/openclaw/openclaw/issues/38327)**（评论 16，👍 3）— 升级后 Gemini 3.1 pro preview 用户完全不可用。**诉求：尽快定位回归源并发布 hotfix，已持续 6 个月仍无 fix PR。**
- **[#43367 [P1, gold shrimp] Multi-agent orchestration is unstable](https://github.com/openclaw/openclaw/issues/43367)**（评论 15）— 并发 `agents add` 配置互相覆盖、session-lock 失败、子任务游离。**诉求：并发安全的多代理 API。** 已有 `linked-pr-open` 但需 info。
- **[#53628 [P3, diamond lobster] ${XDG_CONFIG_HOME} not processed when installing a skill](https://github.com/openclaw/openclaw/issues/53628)**（评论 15）— Docker 场景下安装 skill 时 XDG_CONFIG_HOME 环境变量未被解析。**诉求：容器部署已成为重要使用场景，相关体验问题应优先修复。**

PR 侧评论区热度较低，但 [#137381 fix: sessions_yield keeps long transcript history available](https://github.com/openclaw/openclaw/pull/137381)（P1，等待作者）、[#138199 chore(deps): refresh seven-day-cooled dependencies](https://github.com/openclaw/openclaw/pull/138199)、[#138713 fix(ui): open Dashboard directly and simplify panel controls](https://github.com/openclaw/openclaw/pull/138713) 值得关注（关联 UI 体验与长会话可用性）。

---

## Bug 与稳定性

按严重程度排列今日最值得关注的 Bug：

**🔴 P0 — 文档与版本脱节**
- **[#48920 [P0, platinum hermit] Live Docs are ahead of release](https://github.com/openclaw/openclaw/issues/48920)** — `IsolatedSessions` 已在 docs 中但 2026.3.13 尚未支持，用户按文档配置即失败。更新于 2026-09-04，无 fix PR。**文档发布流程需要与版本发布流程绑定。**

**🟠 P1 — 消息丢失 / 静默失败（高危）**
- **[#92241 [P1, diamond lobster] Gateway holds stale module import paths after update/rollback — inbound messages silently dropped (ERR_MODULE_NOT_FOUND)](https://github.com/openclaw/openclaw/issues/92241)** — 回滚后进程仍持有旧模块路径，systemd 显示 active 但消息全部静默丢弃。**已有 `linked-pr-open`，这是生产环境最危险的状态之一。**
- **[#44925 [P1] Subagent completion silently lost](https://github.com/openclaw/openclaw/issues/44925)** — 见上文社区热点。
- **[#119992 [P1] Per-turn send budget for the message tool](https://github.com/openclaw/openclaw/issues/119992)** — 单轮内消息工具调用无预算限制，agent 可重复发送改写答案，导致重复消息风暴。已有 `linked-pr-open`。
- **[#135111 [P1] Intermittent "Provider completed tool call with malformed JSON arguments" on v2026.8.1](https://github.com/openclaw/openclaw/issues/135111)**（claude-sonnet-5，回归）— 升级后间歇性失败约 6 次，无具体文件/工具关联，定位困难。

**🟠 P1 — 会话状态 / 崩溃循环**
- **[#71689 [P1, diamond lobster] Tasks registry restore fails on malformed SQLite image](https://github.com/openclaw/openclaw/issues/71689)** — SQLite 损坏导致 Gateway 启动反复失败。
- **[#114234 [P1] Usage-cost refresh lock is never releasable after restart that reuses owner PID (containers)](https://github.com/openclaw/openclaw/issues/114234)** — PID 复用导致锁永久冻结。
- **[#119720 [P1] Synchronous SQLite agent.write transactions block gateway event loop at scale](https://github.com/openclaw/openclaw/issues/119720)** — 同步写阻塞事件循环，ANALYZE 从未运行，复现数据：36.7s → 809ms。
- **[#97616 [P1] Leaks unreaped hook/tool child processes (zombies)](https://github.com/openclaw/openclaw/issues/97616)** — 僵尸进程累积导致运行时性能退化。

**🟡 P2 — 功能回归 / 兼容性**
- **[#107814 [CLOSED] gpt-5.3-codex-spark emits empty arguments for required tool calls](https://github.com/openclaw/openclaw/issues/107814)** — 已关闭，原始 issue 于 7/14 创建，今日关闭。修复方向见 [#138714 fix(openai): honor disabled reasoning effort for mapped models](https://github.com/openclaw/openclaw/pull/138714) 与 [#138682 fix(exec): keep gateway exec open for legacy GitHub profile ids](https://github.com/openclaw/openclaw/pull/138682)。
- **[#120162 [P1] qualityGuard audit retry shares timeout budget and is killed by same abort signal](https://github.com/openclaw/openclaw/issues/120162)** — 慢速模型下保护性压缩的审计重试被同一 abort 信号杀死，整个压缩失败。

**值得注意的趋势**：今日大量 P1/P2 Issue 同时带有 `needs-maintainer-review` + `needs-product-decision` 标签且更新日期停留在 2026-09-04，说明维护者已开始集中审视但尚未给出明确结论，可能进入批量产品决策阶段。

---

## 功能请求与路线图信号

- **上下文 / Token 优化三连**：
  - [#14785 Reduce tool schema token overhead (~3,500 tok/session)](https://github.com/openclaw/openclaw/issues/14785)（P2，needs-maintainer-review）
  - [#22438 Tiered bootstrap file loading](https://github.com/openclaw/openclaw/issues/22438)（已有 linked PR）
  - [#38568 Inject context window % into system prompt runtime section](https://github.com/openclaw/openclaw/issues/38568)
  
  三者共同指向 **token 经济性**——随着生产环境大规模使用，用户开始精细化管理上下文窗口的每一部分。
- **Agent 自治能力演进：**
  - [#6757 Agent-triggered context compaction (self-compact tool)](https://github.com/openclaw/openclaw/issues/6757)（创建于 2026-02-02，已积压 7 个月，评论 8 条）
  - [#33975 Fallback approval mode + model attribution in messages](https://github.com/openclaw/openclaw/issues/33975)——主模型故障时静默 fallback 需要用户可见性与审批控制。
  - [#45390 Session TTL / max lifetime for automatic rotation](https://github.com/openclaw/openclaw/issues/45390)——6+ 天不轮换导致 171k/200k token 和 71 次超时。
  - [#13219 Per-model usage logging for cost tracking](https://github.com/openclaw/openclaw/issues/13219)——需要原生按模型用量统计。
- **合规 / 安全边界：**
  - [#44289 Generate secretref reference docs from secret target registry metadata](https://github.com/openclaw/openclaw/issues/44289)——安全文档自动化。
  - [#134898 [PR] feat(plugin-sdk): expose the external verification approvals surface](https://github.com/openclaw/openclaw/pull/134898)——插件外部验证审批面，已在 RFC 阶段。

**路线图信号最强的 PR**：`#138059 feat(agents): allow bounded recursive session spawning by default`（P2）将子代理递归深度默认设为 5，配合 `#130741 fix(agents): reconcile subagents through scoped session owner`，表明 **子代理体系正在从“能跑”走向“可管、可控、可恢复”**。

---

## 用户反馈摘要

- **最强烈的负面情绪集中在“静默丢失”类问题**。#44925 的原帖作者详细列举了三种失败模式（完成通知失败、超时、交付镜像消费失败），并称“结果是静默丢失”，评论区大量用户附议生产事故。#92241 描述回滚后消息被静默丢弃但进程“看起来健康”，这种状态让运营者最不放心。
- **对“文档领先于版本”表达了明确不满**。#48920 用户直接指出“Live docs are ahead of release”，认为 docs 应该严格对应可安装版本，否则缺乏可信度（👍 4，为今日最高）。这对发布流程提出了脚本化校验的诉求。
- **本地化/国产模型用户反馈积极**：#88079 指出 Kimi Code 与 DeepSeek Reasoner 的推理内容在 WebChat 不渲染（仅 MiniMax 可工作），说明国产模型集成是增长点但工程质量仍不稳定；#42591 是一份用中文提交的 install.sh 可维护性优化建议（79KB/2498 行单体需拆分），开发者群体开始关注工程可维护性。
- **多代理场景的可靠性被反复提及**：#43367 描述并行 `agents add` 会覆盖配置、session-lock 失败，说明用户正在尝试将 OpenClaw 真正用于并行任务编排，但当前 API 的并发安全性尚未达到生产预期。
- 正面反馈：暂无直接表扬类 Issue，但 #88079 中用户特别标注“MiniMax works”，间接认可了部分模型适配的完成度。

---

## 待处理积压

以下为长期未响应/未修复且影响重大的项目，提醒维护者优先处理：

- **[#38327 [P1] google-vertex/gemini-3.1-pro-preview "Cannot convert undefined or null to object"（2026-03-06 创建，持续 6 个月，👍 3）](https://github.com/openclaw/openclaw/issues/38327)** — 无任何 fix PR，打满 `diamond lobster` + regression + auth-provider 标签。
- **[#6767 [P2] Agent-triggered self-compact tool（2026-02-02 创建，7 个月）](https://github.com/openclaw/openclaw/issues/6757)** — 评论 8 条，早期路线图信号，后来没有下文。
- **[#6757 [P2] Feature

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-09-05

## 今日速览

过去 24 小时项目处于**高活跃、零发布**状态：Issues 更新 73 条（新开/活跃 44 条，关闭 29 条），PR 更新 283 条（待合并 180 条，已合并/关闭 103 条）。仓库正在经历一轮明显的**积压清理**——多个

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*