# OpenClaw 生态日报 2026-09-13

> Issues: 498 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-13 00:03 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目日报 · 2026-09-13

> 数据来源：github.com/openclaw/openclaw｜统计窗口：过去 24 小时

---

## 1. 今日速览

- **活跃度极高**：24 小时内 Issues 更新 498 条（新开/活跃 270，关闭 228），PR 更新 500 条（待合并 267，合并/关闭 233），合计约 1000 次协作事件，属于典型的高频维护日。
- **核心矛盾集中在升级链**：围绕 `2026.9.3 → 2026.9.4` 的更新、迁移、回滚问题密集出现，并已出现维护者级 Tracking Issue（#145252），多条 P0 级 release-blocker 仍未闭合。
- **子代理（Subagent）可靠性是第二大主题**：完成事件静默丢失、`sessions_yield` 悬挂、任务行卡在 `running` 等问题跨越 3—8 月多次复发，说明这是结构性缺陷而非单点回归。
- **资源与性能类问题凸显**：僵尸子进程累积（#97616）、cron 同步 `PRAGMA integrity_check` 阻塞事件循环（#142476，已关闭）、大仓库 Git 读取卡顿等，主要影响大规模网关部署。
- **零版本发布**：在大量 P0 修复尚未落地的情况下保持不发布，属于"先稳后发"的克制策略；但积压的 release-blocker 正在威胁 2026.9.x 分支的可用性口碑。

---

## 2. 版本发布

过去 24 小时无新版本发布（Releases 数量为 0）。结合多条 P0 级更新失败与回滚问题，当前主线更可能处于"修复窗口期"而非"发布窗口期"。

---

## 3. 项目进展

今日合并/关闭的 PR 主要集中在**升级可靠性、数据库扫描性能、内部重构**三条线上。

**已落地（合并/关闭）的关键变更：**

| PR | 状态 | 内容 | 价值 |
|---|---|---|---|
| [#146512](https://github.com/openclaw/openclaw/pull/146512) | CLOSED | 避免重复的 agent 数据库完整性扫描 | 直接缓解大库重开时的会话操作卡顿，与 #142476 同类病根 |
| [#146502](https://github.com/openclaw/openclaw/pull/146502) | CLOSED | Web UI 中"编码会话发现"设置更易找到 | 将 Claude Code / Codex / OpenCode / Pi 的发现配置从分散面板收敛 |
| [#146566](https://github.com/openclaw/openclaw/pull/146566) | CLOSED | 集中化"被打断回合"的 transcript 读取 | 纯内部重构，统一恢复replay 的准入边界 |
| [#146462](https://github.com/openclaw/openclaw/pull/146462) | 已合并 | 修复授权指引（repair authorization guidance） | 升级/修复路径的可用性 |
| [#146486](https://github.com/openclaw/openclaw/pull/146486) | 已合并 | 插件导入扫描 | 插件加载可靠性 |
| [#146488](https://github.com/openclaw/openclaw/pull/146488) | 已合并 | 预置 provider 元数据 | 模型/provider 初始化 |
| [#146410](https://github.com/openclaw/openclaw/pull/146410) / [#146538](https://github.com/openclaw/openclaw/pull/146538) | 已合并 | 启动与 CI 库存修复 | 启动稳定性 |

**整体推进评估**：项目在"性能退化"方向上有明确进展——数据库完整性扫描重复执行、Git 大仓库读取、verbose 命令 CPU 开销（[#146406](https://github.com/openclaw/openclaw/pull/146406)）、history 重复计算（[#146574](https://github.com/openclaw/openclaw/pull/146574)）等一批"事件循环阻塞/重复 I/O"类优化正在成体系推进。但**升级链的 P0 尚未收口**，向前迈进的净增量主要体现在稳定性债务的偿还，而非新能力交付。

---

## 4. 社区热点

按评论数排序的讨论焦点：

**① [#97616](https://github.com/openclaw/openclaw/issues/97616) — 僵尸子进程累积（28 评论，OPEN，P1，🦪 silver shellfish）**
hook/tool 执行泄漏未回收的子进程（`openclaw-hooks`、`bash`、`codex`），长期累积为僵尸并导致运行时退化。诉求：子进程生命周期管理与回收保障。

**② [#44925](https://github.com/openclaw/openclaw/issues/44925) — Subagent 完成静默丢失（27 评论，OPEN，P1，🦞 diamond lobster）**
无重试、无通知、无超时自动重启。创建于 3 月，跨越半年仍开放，且已带 `needs-product-decision` 标签。诉求：subagent 编排需要"可观测 + 可恢复"的语义保证。

**③ [#142585](https://github.com/openclaw/openclaw/issues/142585) — Doctor 拒绝合法 legacy workspace（17 评论，OPEN，P0，🦐 gold shrimp）**
`2026.7.1-2 → 2026.9.3` 升级时，Doctor 识别出合法 legacy 状态却拒绝迁移。诉求：迁移器应接受"规范行缺失"这一合法历史形态。

**④ [#67777](https://github.com/openclaw/openclaw/issues/67777) — subagent 完成投递在 timeout/drain/orphan 下丢失（16 评论，已关闭，🦞 diamond lobster）**
与 #44925 同源问题的收敛项，今日关闭，是可喜信号。

**⑤ [#78308](https://github.com/openclaw/openclaw/issues/78308) — MCP 工具调用的通道级审批（16 评论，OPEN，P2，🦞 diamond lobster）**
让 MCP server 通过 `tools/call` 返回标准 envelope，接入已有的 `/approve <id>` 审批管线。诉求：**安全治理**——MCP 能改外部状态（发邮件、写 vault）却没有与 shell-exec 同级的同意机制。

**⑥ [#144502](https://github.com/openclaw/openclaw/issues/144502) — WhatsApp 无法播放 TTS 语音（12 评论，P1，🐚 platinum hermit）**
48 kHz + Lavf vendor tag 导致"audio unavailable"、下载失败。诉求：音频编码需适配 WhatsApp 移动端解码器。

**⑦ [#142476](https://github.com/openclaw/openclaw/issues/142476) — cron reaper 同步完整性检查阻塞事件循环 14–76 秒（12 评论，已关闭，🦞 diamond lobster）**
632-agent 网关场景下的严重性能回归，今日关闭。

**⑧ [#136183](https://github.com/openclaw/openclaw/issues/136183) — ssh 命令执行挂起（12 评论，OPEN，P1）**
SIGTERM 在等待 server banner 阶段被打出，2026.8.1 引入、8.2 持续。

**背后趋势**：社区讨论热度高度集中在**"静默失败"**（完成丢失、消息丢弃、任务悬挂）与**"大规模部署退化"**（632-agent 网关、共享工作区）两类。用户对"没有报错但结果不见了"的容忍度极低，这是当前最大信任风险。

---

## 5. Bug 与稳定性

### P0 / Release Blocker（最高优先级）

| Issue | 问题 | 状态 | Fix PR |
|---|---|---|---|
| [#145252](https://github.com/openclaw/openclaw/issues/145252) | [Tracking] 2026.9.3/9.4 更新、升级、恢复可靠性总索引 | OPEN | 协调中 |
| [#144739](https://github.com/openclaw/openclaw/issues/144739) | 2026.9.3→9.4 用 9.3 运行 schema-17 候选状态 | OPEN | 未见 |
| [#145192](https://github.com/openclaw/openclaw/issues/145192) | 9.2→9.4 在候选 Doctor 处失败后回滚到已迁移状态 | OPEN | 未见 |
| [#145510](https://github.com/openclaw/openclaw/issues/145510) | 更新失败于 runtime-verification-failed（Windows） | OPEN | 未见 |
| [#145929](https://github.com/openclaw/openclaw/issues/145929) | auth profile logout/写入因 lock-may-be-busy 永久失败 | OPEN | 未见 |
| [#142585](https://github.com/openclaw/openclaw/issues/142585) | Doctor 拒绝合法 legacy workspace 与 attestation 导入 | OPEN | 未见 |
| [#112475](https://github.com/openclaw/openclaw/issues/112475) | 设备配对移除后无法恢复（Gateway 2026.7.1） | OPEN | 未见 |
| [#145782](https://github.com/openclaw/openclaw/issues/145782) | 更新失败：repairing 阶段（darwin/arm64） | **CLOSED** | 已处理 |
| [#140620](https://github.com/openclaw/openclaw/issues/140620) | session transcript 迁移 27/~1500 后停滞 | **CLOSED** | 已处理 |

### P1

| Issue | 问题 | 状态 | Fix PR |
|---|---|---|---|
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | 僵尸子进程累积导致运行时退化 | OPEN | 未见 |
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | subagent 完成静默丢失 | OPEN | 待产品决策 |
| [#144502](https://github.com/openclaw/openclaw/issues/144502) | WhatsApp TTS 语音不可播放 | OPEN

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目日报 · 2026-09-13

> 数据窗口：2026-09-12 ~ 2026-09-13（过去 24 小时）
> 仓库：github.com/NousResearch/hermes-agent
> 说明：本日 PR 数据中评论数字段缺失（`undefined`），PR 部分热点按更新时间、标签与关联 Issue 推断；Issues 部分按评论数排序展示 Top 30。

---

## 1. 今日速览

1. **高吞吐维护窗口**：24 小时内 Issues 更新 500 条（新开/活跃 340、关闭 160，关闭率约 32%），PR 更新 500 条（待合并 362、已合并/关闭 138），**无新版本发布**，属于"高强度流转、低发布节奏"的一天。
2. **Issue 侧流动性尚可，PR 侧积压明显**：362 条待合并 vs 138 条已合并/关闭，待合并占比约 **72%**，审阅带宽是当前最紧的资源。
3. **故障焦点高度集中在 cron 调度子系统**：今日 Top 30 中有 6 条直接指向 `comp/cron`（#100401、#109243、#88584、#2788、#39609、#94139 相关路径），叠加多个 `sweeper:risk-session-state` / `risk-message-delivery` 风险标签，说明**持久化会话状态与任务投递的可靠性**是本周期主线。
4. **安全类问题持续暴露**：审批层绕过（#74078、#59293）与"破坏性命令未确认"（#10199）构成一条清晰的安全加固需求线。
5. **整体健康度评估：中性偏紧**。有明确的修复 PR 跟进（#109252、#109253、#109255、#109259、#109477），但多个 P1 长期未闭合（#39609 已挂 100 天、#62774 已挂 64 天），需关注维护者注意力分配。

---

## 2. 版本发布

本日**无新版本发布**（0 个），最新 Releases 为空。无破坏性变更与迁移事项需要通报。

---

## 3. 项目进展

今日共有 138 条 PR 被合并/关闭、160 条 Issue 关闭。以下为可辨识的重要推进：

### 已关闭的关键 Issue（问题侧推进）

| Issue | 级别 | 影响 | 状态 |
|---|---|---|---|
| [#100401](https://github.com/NousResearch/hermes-agent/issues/100401) cron fire-claim 心跳与自身 fence 死锁，导致所有 >60s 任务被误记为 "Interrupted by shutdown" | **P1** | 直接影响所有长耗时定时任务的正确性 | 已关闭 |
| [#94139](https://github.com/NousResearch/hermes-agent/issues/94139) `codex_responses` 迭代上限摘要路径携带 `tool_choice` 但无 `tools`，xAI 等严格 Provider 返回 400 且进程仍 exit 0 | **P1** | 静默失败，CI/自动化场景危害大 | 已关闭 |
| [#2384](https://github.com/NousResearch/hermes-agent/issues/2384) Anthropic fallback 继承 Codex `model.base_url`，把 Claude 请求发往 chatgpt.com/backend-api/codex | P2 | 跨 Provider 配置污染 | 已关闭 |
| [#4379](https://github.com/NousResearch/hermes-agent/issues/4379) Token 开销分析：每次 API 调用 73% 为固定开销（~13.9K tokens） | P2 / needs-decision | 成本核心议题，21 条评论 | 已关闭 |
| [#4505](https://github.com/NousResearch/hermes-agent/issues/4505) Ollama 集成改用原生 `/api/chat` | P2 / 5 👍 | Provider 质量优化 | 已关闭 |
| [#11113](https://github.com/NousResearch/hermes-agent/issues/11113) MCP 熔断器把工具级错误（DNS/4xx/5xx）计为服务级失败 | P2 / 4 👍 | 误熔断，影响可用性 | 已关闭 |
| [#5472](https://github.com/NousResearch/hermes-agent/issues/5472) Discord 会话内 `send_message` 无法投递到当前频道 | P2 | 多消息批量投递阻碍 | 已关闭 |
| [#86146](https://github.com/NousResearch/hermes-agent/issues/86146) profile 切换模型列表串用主 profile | P2 | 多 profile 用户体验 | 已关闭 |
| [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) Skills 索引 watchdog 报告 degraded（索引 29.8h > 26h 上限） | P3 自动化 | 自动化噪声，202 条评论 | 已关闭 |

### 已合并/关闭的 PR

- [#109379](https://github.com/NousResearch/hermes-agent/pull/109379) `fix(agent): fall back to /props when /v1/props lacks n_ctx and guard json`（修复 #108638）——**已关闭**，修复 llama.cpp `/v1/props` → `/props` 回退被 HTTP 状态码错误门控、以及 JSON 解析未防护三重叠加缺陷，属于压缩/上下文元数据路径的实质修复。
- 其余 137 条合并/关闭 PR 未在 Top 20 评论区展示，无法逐条确认。

### 整体前进步长评估

本日**问题侧推进强、合并侧推进中等**：cron 死锁（P1）、codex_responses 静默失败（P1）、Anthropic base_url 污染三个高价值缺陷被关闭，是明确的稳定性收益；但 PR 侧由于 362 条积压，功能类 PR（如 #104567、#98470）推进缓慢。

---

## 4. 社区热点

按评论数排序的讨论焦点：

| 排名 | 条目 | 评论 | 状态 | 焦点 |
|---|---|---|---|---|
| 1 | [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) Skills index stale/degraded | 202 | CLOSED | 自动化 watchdog 与索引新鲜度告警 |
| 2 | [#88584](https://github.com/NousResearch/hermes-agent/issues/88584) Automated Nous integration is blocked | 93 | OPEN / `invalid` | 定时 Nous→Enterkey 合并在 `cron/jobs.py` 冲突，发布分支未变更，仪表盘停留在旧版 |
| 3 | [#2825](https://github.com/NousResearch/hermes-agent/issues/2825) Termux/proot Ubuntu 安装失败 | 37 | CLOSED | 移动端 Linux 环境安装路径 |
| 4 | [#97681](https://github.com/NousResearch/hermes-agent/issues/97681) Desktop 关闭后 Bot 群聊应继续工作 | 28 / 1 👍 | OPEN | 跨网关多 Bot 协作、跨设备续接 |
| 5 | [#100401](https://github.com/NousResearch/hermes-agent/issues/100401) cron fire-claim 死锁 | 22 | CLOSED | P1 调度器正确性 |
| 6 | [#4379](https://github.com/NousResearch/hermes-agent/issues/4379) Token 固定开销 73% | 21 | CLOSED | 成本与性能优化 |
| 7 | [#109243](https://github.com/NousResearch/hermes-agent/issues/109243) cron 外部 worker 5s ack 窗口 vs 12s 冷启动 | 17 | OPEN | 同一天开单、同一天有修复 PR |

### 背后诉求分析

- **调度器是当前最大痛点域**：#100401（死锁）、#109243（握手超时）、#2788（cron 无有效日志）、#39609（kanban 状态自动越过人工闸门）四条独立线索指向同一结论——**cron/任务编排的时序假设（心跳、ack 窗口、状态迁移）与实际运行时延不匹配**。#109243 报告当日即出现修复 PR（#109252），响应速度值得肯定。
- **自动化与人工关注的争夺**：#66616（202 条）与 #88584（93 条）合计 295 条评论，绝大多数来自机器人/自动化流水线，而非人类用户。这类"高频低信息量"条目正在挤占维护者的 issue triage 带宽，建议对 watchdog 类告警做抑制/聚合。
- **跨设备与多 Bot 协作是明确的产品诉求**：#97681 希望 Bot 群聊在 Desktop 关闭后仍能运行、可换设备接管、可交换文件与指令，这已经超出 bug 范畴，指向"headless 常驻网关 + 授权协作"的能力边界。

---

## 5. Bug 与稳定性

按严重程度排列（标注是否已有 fix PR）：

### P1 — 严重

| Issue | 描述 | 状态 | Fix PR |
|---|---|---|---|
| [#105104](https://github.com/NousResearch/hermes-agent/issues/105104) | Desktop Bot Mode 侧边栏点击 Bot 间歇性无响应，受影响 Bot 不确定，失败时后端零活动（Linux desktop，v0.21.0） | OPEN，2026-09-07 起 | 未见对应 PR |
| [#39609](https://github.com/NousResearch/hermes-agent/issues/39609) | `--initial-status blocked` 创建的任务约 1 秒后被无 actor 自动提升为 ready，**绕过人工审批闸门** | OPEN，2026-06-05

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报
**日期：2026-09-13** ｜ 数据源：github.com/OpenHands/software-agent-sdk

---

## 1. 今日速览

- **活跃度处于高位，但合并吞吐严重滞后**：过去 24 小时 29 条 Issue 更新、50 条 PR 更新，然而仅 1 条 PR 被合并/关闭，49 条仍在待合并状态，Issue 关闭率约 7%（2/29）。项目处于"输入远大于消化"的状态，Review 带宽已成为主要瓶颈。
- **两条主线并行推进**：一是**类型系统治理**（以 #4902 为父任务的 `getattr`/`setattr` 清理，衍生出 #4903–#4905 及 #4973–#4979 共 10+ 个子任务）；二是**运行时/控制面安全架构**（#5004、#5007、#5009、#5012、#5014 一组 Docker 与 Canvas 传输层议题）。
- **1 个高优先级 Bug 待处置**：#4997 —— ChatGPT 订阅（OAuth）配置下 LLM 调用挂起会导致会话永久卡在 `RUNNING`，目前**尚无对应修复 PR**。
- **无新版本发布**，且今日无 PR 进入发布通道，短期内不宜期待版本迭代。
- 值得注意的是，今日绝大多数 Issue 由 @neubig 提交并标注 "created by an AI agent (OpenHands)"，说明维护者正在用自有 Agent 批量生成路线图任务——这既是项目特色，也放大了待处理队列。

---

## 2. 版本发布

今日无新版本发布（0 个 Release），无破坏性变更或迁移事项需要说明。

---

## 3. 项目进展

今日合并/关闭量极低（PR 1 条、Issue 2 条），从可见数据看，实质推进集中在**问题闭环**而非代码落地：

| 事项 | 状态 | 说明 |
|---|---|---|
| [#4902](https://github.com/OpenHands/software-agent-sdk/issues/4902) 禁止动态 `getattr`/`setattr` | ✅ 已关闭 | 父任务宣告目标达成（lint 规则 + 首轮清理），但 #4903/#4904/#4905 及其子任务仍全部开启，后续切片工作量巨大 |
| [#4986](https://github.com/OpenHands/software-agent-sdk/issues/4986) 标题生成 Prompt 拼接错误 | ✅ 已关闭 | 同日开启的 [#4987](https://github.com/OpenHands/software-agent-sdk/issues/4987) 为同一问题的重复项且带 `release-note-required`，对应的修复 PR [#4985](https://github.com/OpenHands/software-agent-sdk/pull/4985) 已提交，形成"关旧开新 + 修复在途"的闭环 |
| PR 合并 | ⚠️ 仅 1 条 | 该 PR 未出现在评论数 Top-20 列表中，具体内容无法从本次数据确认 |

**整体推进评估**：今日项目在"代码合入"维度几乎停滞，但在"问题定义与任务拆解"维度进展显著——大量 `ready-for-dev` 标记的 Issue 已就绪，一旦 Review 带宽释放，具备集中落地的潜力。

---

## 4. 社区热点

按评论数排序，今日讨论最集中的 Issue 是：

1. **[#4658](https://github.com/OpenHands/software-agent-sdk/issues/4658)｜3 评论｜延迟初始化失败留下半初始化 runtime**
   `InitService` 在初始化异常后回到 `dormant`，但不回滚已变更的环境、配置、遥测与模块级 conversation-service 状态。这是典型的**状态机原子性缺陷**，牵涉架构层，属于"不炸但难查"的长期隐患。

2. **[#4671](https://github.com/OpenHands/software-agent-sdk/issues/4671)｜3 评论｜Epic：流式传输——将 wire format 与持久化事件记录解耦**
   痛点是流式文本走了**两条互不知晓的通道**：durable events 经回调链落盘，token deltas 则由生产线程直接投递给 `PubSub`，二者无排序保证。这是流式体验一致性的架构级根因。

3. **Docker/安全三连**：#5014（2 评论）、#5012（2 评论）、#5004（2 评论）——分别涉及 profile 密钥在 Docker 运行时物化前强制执行、Canvas WebSocket 传输下沉到 TypeScript SDK、以及**不删除审计历史的前提下释放 Docker runtime**。三者共同指向"多租户/自动化编排场景下的控制面治理"。

**背后诉求解读**：
- 社区对**正确性边界**（初始化原子性、事件排序）的诉求高于对新功能的诉求；
- 自动化编排方（scheduled factory、trusted orchestrator）正成为核心用户画像，他们要求**可释放、可审计、可最小授权的 runtime 生命周期**；
- 传输层实现重复（Canvas 自带一套 WebSocket 逻辑）被明确视为技术债，希望统一到 SDK 内。

---

## 5. Bug 与稳定性

按严重程度排列：

### 🔴 高优先级
| Issue | 问题 | 修复 PR |
|---|---|---|
| [#4997](https://github.com/OpenHands/software-agent-sdk/issues/4997) | **ChatGPT 订阅（OAuth）profile 下 LLM 调用挂起**，会话进入永久停滞：`execution_status` 恒为 `RUNNING` 但不再产生事件。标签含 `security`，且缺乏超时/心跳兜底 | ❌ 无 |

### 🟠 中优先级
| Issue | 问题 | 修复 PR |
|---|---|---|
| [#4990](https://github.com/OpenHands/software-agent-sdk/issues/4990) | `POST /pause` 立即把状态置为 `paused`，但

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报
**报告日期：2026-09-13**

---

## 1. 今日速览

- **PR 吞吐量处于高位**：过去 24 小时共 243 条 PR 更新，其中 132 条已合并/关闭、111 条待合并，关闭率约 54%，代码侧消化能力强于新增积压。
- **Issue 侧呈净流入**：34 条 Issue 更新中 25 条为新开/活跃、仅 9 条关闭，未决问题总量小幅上升，需关注维护带宽分配。
- **今日无新版本发布**，项目仍处于持续迭代（非发版）窗口，改动以修复、计费准确性、安全加固为主。
- **计费与翻译桥（Responses↔Chat/Anthropic）是今日两大主题**：多条高优 Bug 与修复 PR 集中在这两个子模块。
- **社区热度最高的问题 #23741 已持续挂起近半年**（14 评论、13 👍），是本日最值得介入的长期痛点。

---

## 2. 版本发布

无新版本发布，本节略。

---

## 3. 项目进展

今日合并/关闭 132 条 PR，以下为可追溯的重点进展：

| PR | 内容 | 意义 |
|---|---|---|
| [#40907](https://github.com/BerriAI/litellm/pull/40907) | fix(proxy): 允许非管理员在 `/key/list` 上按 `key_alias` 子串匹配 | 修复 Team Admin / Member 搜索团队 Key 返回空列表的体验缺陷，恢复 v1.100.x 前的行为 |
| [#40898](https://github.com/BerriAI/litellm/pull/40898) | chore(prices): 同步 5 家供应商 276 个模型（48 个新增） | 价格目录与供应商定价对齐 |
| [#40897](https://github.com/BerriAI/litellm/pull/40897) | chore(prices): 同步 277 个模型（33 个新增），覆盖 Anthropic/Fireworks/OpenAI/Together/Vertex | 同上，含 Anthropic 13 个模型修正 |
| [#29892](https://github.com/BerriAI/litellm/pull/29892) | test: 为 `safe_json_loads` 补充单元测试 | 小范围测试覆盖补齐，纯测试、无生产代码变更 |

Issue 侧同步关闭的修复类问题包括 Vertex AI 健康状态误报（[#28206](https://github.com/BerriAI/litellm/issues/28206)）、Bedrock 工具配置校验失败（[#19384](https://github.com/BerriAI/litellm/issues/19384)）、月度重置后 `max_budget` 失效（[#27300](https://github.com/BerriAI/litellm/issues/27300)）、`ResetBudgetJob` 全局崩溃（[#27171](https://github.com/BerriAI/litellm/issues/27171)）、OCR 自定义定价被忽略（[#36608](https://github.com/BerriAI/litellm/issues/36608)）等，说明预算/计费子系统的历史欠账正在被系统性清理。

**整体推进评估**：本日项目在「计费准确性」与「预算系统稳定性」两个方向上有实质收敛，同时价格目录保持自动同步。但新开 Issue 明显多于关闭，功能请求侧积压未见缓解。

---

## 4. 社区热点

### 🔥 #23741 — Anthropic 400：`vector_store_ids` 不被允许（14 评论 / 13 👍 / 仍 OPEN）
- 链接：https://github.com/BerriAI/litellm/issues/23741
- 创建于 2026-03-16，今日仍有更新，是当之无愧的社区焦点。
- **诉求**：通过 LiteLLM 转发到 Anthropic 时，请求体携带 `vector_store_ids` / `vector_store` 会被 Anthropic 直接拒绝并返回 400。用户希望 LiteLLM 在翻译层做好参数剥离或映射，而非原样透传非法字段。
- **分析**：13 个 👍 说明这是跨用户的高频阻塞问题。该 Issue 已关联多个修复 PR（#23742 / #30086）但均未彻底解决，且今日新开 [#40908](https://github.com/BerriAI/litellm/issues/40908) 指出 `enable_anthropic_prompt_caching` 会“饿死”vector-store 预调用钩子——说明该链路存在结构性设计与功能开关互斥的问题，建议维护者作为本 Sprint 的一号议题。

### #28206 — Vertex AI 模型健康状态误报（13 评论，今日 CLOSED）
- 链接：https://github.com/BerriAI/litellm/issues/28206
- 自 v1.84.0 起模型健康看板将 Vertex AI 全部标记为 Unhealthy，影响运维告警可信度。已关闭，社区痛点解除。

### #19384 — Bedrock / Cursor 集成报 toolConfig 校验错误（9 评论，今日 CLOSED）
- 链接：https://github.com/BerriAI/litellm/issues/19384
- Cursor + LiteLLM + Bedrock 组合在 `toolConfig` 上产生 11 项校验错误，属于典型 IDE 生态联动问题，关闭对 Cursor 用户群体意义较大。

### #22984 — VLLM `cached_tokens` 成本计算缺失（5 评论 / 5 👍 / OPEN）
- 链接：https://github.com/BerriAI/litellm/issues/22984
- 自托管 VLLM 用户的计费准确性诉求，开放近 6 个月仍未闭环。

---

## 5. Bug 与稳定性

### 🔴 严重（影响计费正确性或安全边界）

| 问题 | 状态 | 说明 |
|---|---|---|
| [#23741](https://github.com/BerriAI/litellm/issues/23741) Anthropic `vector_store_ids` 400 | OPEN，14 评论 | 阻断性错误，无法通过配置绕过 |
| [#40649](https://github.com/BerriAI/litellm/issues/40649) Admin UI 编辑模型持久化派生定价，Azure 花费记为 $0 | OPEN | 直接导致计费失真，附带自定义定价丢失 |
| [#31260](https://github.com/BerriAI/litellm/issues/31260) Router 同步 `_embedding` 绕过团队/访问组作用域 | OPEN | **潜在越权**：同步调用可访问未授权模型 |
| [#40736](https://github.com/BerriAI/litellm/issues/40736) 流式用量合并器在显式归零后仍保留过期 cache-write tokens | OPEN | 计费偏高，与 [#40627](https://github.com/BerriAI/litellm/pull/40627)（缓存实时音频计费修复）同域 |
| [#36608](https://github.com/BerriAI/litellm/issues/36608) OCR 成本忽略部署自定义定价 | CLOSED | 未命中价格表即 $0 计费，今日已关闭 |

### 🟠 中等（功能回归/体验受损）

- [#40887](https://github.com/BerriAI/litellm/issues/40887) Responses→Chat 流式丢失 reasoning 进度与缓存推理状态（3 评论，今日活跃）
- [#40654](https://github.com/BerriAI/litellm/issues/40654) 同上桥接在流式/非流式结果中丢弃 `reasoning_text`
- [#40851](https://github.com/BerriAI/litellm/issues/40851) `LiteLLM_SpendLogs.session_id` 不反映 `litellm_session_id`，会话分组失效
- [#40780](https://github.com/BerriAI/litellm/issues/40780) `openai/` 前缀自托管模型把 `/v1/messages` 路由到 Responses API，静默破坏多模态
- [#40628](https://github.com/BerriAI/litellm/issues/40628) OpenAI 图像生成把 `extra_headers` 误放入 JSON body

### 🟡 稳定性/运维

- [#30061](https://github.com/BerriAI/litellm/issues/30061) 启用 OTEL 回调后容器持续崩溃（NoneType），开放逾 3 个月
- [#40651](https://github.com/BerriAI/litellm/issues/40651) `lite codex` 在子命令后传 `-c` 时静默绕过代理
- [#40822](https://github.com/BerriAI/litellm/issues/40822) Helm chart 的 `podSecurityContext` / `securityContext` 为空，Pod 默认以 root 运行（**安全加固缺失**）
- [#40890](https://github.com/BerriAI/litellm/issues/40890) `/v1/messages` 原生透传丢弃 adaptive thinking 与 effort

**Fix PR 关联情况**：今日有修复动作的 PR 集中在计费与日志域（[#40627](https://github.com/BerriAI/litellm/pull/40627) 缓存

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*