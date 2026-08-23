# OpenClaw 生态日报 2026-08-24

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-23 22:36 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-24

## 1. 今日速览

过去24小时项目活跃度极高：共产生500条Issue更新（450条新开/活跃、50条关闭）和500条PR更新（391条待合并、109条已合并/关闭），但无新版本发布。当前处于 **v2026.8.1-beta.2 → beta.3 的发布验证窗口**，社区讨论焦点集中在发布验证流程（#125626，18条评论）与若干P1消息丢失/会话状态类回归（#127710、#126246、#126707等）。值得警惕的是一个 **P0级SQLite损坏复发问题**（#126821，5天内5次事件），项目整体处于“高吞吐、重稳定性验证”的阶段，维护者审核资源明显承压——大量PR长期处于`waiting on author`或`needs proof`状态。

---

## 2. 版本发布

**无新版本发布。** 最新版本仍为 v2026.8.1-beta.2，正在推进 beta.3 的发布验证。当前发布阻塞点集中在：
- #125626 发布验证清单尚未完成
- PR #128391 / #128371 试图解决 beta.3 发布流程中“规范发布者只接受完整验证清单”的自动化阻塞，后者被前者替代后已关闭

---

## 3. 项目进展

今日共有109条PR合并/关闭，以下为关键进展：

### 已合并/已关闭的重要PR

- **[安全] 安装策略警告确认机制落地（#116489 已关闭 / #120900 已关闭）**
  `external security.installPolicy` 现在支持返回 `warn`，CLI 与 Control UI 均支持操作者审阅后确认继续安装。这是安全边界的重要增强：管理员不再被迫在“全盘拒绝”和“盲目放行”之间二选一。
  https://github.com/openclaw/openclaw/pull/116489
  https://github.com/openclaw/openclaw/pull/120900

- **[修复] 保持 Claude CLI OAuth 在 Control UI 中的可用性（#125471 已关闭）**
  修复了 Gateway 重启后遗留的 `auth.profiles["anthropic:claude-cli"]` 条目导致 OAuth 刷新所有权丢失、Control UI 中 Claude CLI 模型不可用的问题。
  https://github.com/openclaw/openclaw/pull/125471

- **[修复] 会话投递严格限定在 Agent 绑定范围内（#126424 已关闭）**
  阻止多 Agent 场景下 conversation 工具将消息投递到其他 Agent 的绑定频道之外，是一个重要的消息投递隔离修复。
  https://github.com/openclaw/openclaw/pull/126424

- **[发布流程] beta 验证证据授权（#128371 已关闭）**
  解决了 beta.3 发布阻塞：规范发布者原本只接受全量验证清单，但冻结候选仅改动 Slack 测试且历史失败已重跑成功。被 #128391 替代，后者在主分支注册了 focused beta evidence workflow。
  https://github.com/openclaw/openclaw/pull/128371
  https://github.com/openclaw/openclaw/pull/128391

### 已确认修复的Issue（close: already-fixed）

- **#112246** — Codex app-server 稳定 session-key 绑定无 TTL 永久墓碑问题（已修复）
  https://github.com/openclaw/openclaw/issues/112246
- **#111745** — safe-package-install 全量安装6个平台二进制包（~2.0GB）问题（已修复）
  https://github.com/openclaw/openclaw/issues/111745
- **#111969** — 前台回复栅栏无界等待问题（已修复）
  https://github.com/openclaw/openclaw/issues/111969

整体判断：项目在安全策略确认、OAuth 状态保持、消息投递隔离三个方向有明显推进，且已有多个历史 P1 问题被确认修复，说明 2026.8.1 系列 beta 的稳定性工作在持续收敛。

---

## 4. 社区热点

### 最热 Issue TOP 5（按评论数）

| Issue | 评论数 | 核心诉求 |
|---|---|---|
| [#125626] Release validation: v2026.8.1-beta.2 | 18 | 社区测试者协作完成 beta.2 发布验证，关注发布质量门槛 |
| [#119796] Windows: vitest teardown EBUSY on agent state DB | 15 | Windows 平台测试基础设施稳定性，sqlite 句柄释放问题导致测试套件无法收尾 |
| [#121953] Cron agent stall on DeepSeek（`[cron:` 前缀被降优先级） | 13 | DeepSeek API 对 `[cron:` 开头消息走低优先级队列，导致定时任务卡顿数十秒至分钟级 |
| [#39476] A2A sessions_send

---

## 横向生态对比

# 个人 AI 助手与自主智能体开源生态横向对比分析报告

**分析日期：2026-08-24**

---

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态正处于**高吞吐迭代与稳定性验证并行的关键阶段**：OpenClaw 与 Hermes Agent 两日新增 Issue/PR 更新均以数百计，但同时无任何项目发布正式新版本，说明社区集体进入功能密集合并后的质量收敛期。生态共同面临的短板高度一致——**更新流程可靠性、多端会话状态同步、Windows 平台兼容性**三大问题在多个项目中反复出现，已构成影响用户信任的共性瓶颈。与此同时，**协议互操作性开始从口号走向代码落地**（OpenHands SDK 的 A2A 服务端实现），外部贡献者主动提交修复 PR 的案例增加，生态正在从"核心团队驱动"向"社区协作驱动"过渡。

---

## 2. 各项目活跃度对比

| 项目 | Issue 更新（新开/关闭） | PR 更新（合并/关闭） | Release 状态 | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 500（450/50） | 500（391 待合并、109 已合并/关闭） | v2026.8.1-beta.2 → beta.3 验证窗口 | ⚠️ 高吞吐但维护者承压；P0 SQLite 损坏复发（5 天 5 次），发布验证流程阻塞，大量 PR 长期处于 waiting-on-author |
| **Hermes Agent** | 406（349/57） | 500（428 待合并、72 已合并/关闭） | v0.20.5，无新版本 | ⚠️ 高强度迭代修复期；大量 P1 bug 集中在更新流程与状态同步，桌面端体验逐步修复，但待合并 PR 积压严重 |
| **OpenHands SDK** | 17（13/4） | 25（4 已合并/关闭） | 无新版本 | ✅ 双线推进中；并发/死锁类 bug 集中爆发但响应快（#4597→#4599 同日出现），A2A 功能落地带来积极信号 |
| **Pi** | 48（46 关闭） | 16（13 合并/关闭） | 无新版本 | ✅ 整体健康；Issue 关闭率 95.8%，维护者响应极快，几乎无积压，修复方向精准（模型兼容、流式错误透传） |
| **LiteLLM** | 数据缺失（日报未提供） | 数据缺失（日报未提供） | — | — |
| **Temporal** | 1（新增 bug 报告） | 28（9 合并/关闭） | 1.32.0 发布分支已准备 | ✅ 健康稳定；worker callbacks 功能系列集中推进，新 bug 报告与修复 PR 同日出现（#11733→#11734），响应迅速 |

---

## 3. OpenClaw 在生态中的定位

OpenClaw 是目前生态中**社区吞吐量最大、治理流程最规范**的自主智能体平台。

- **核心优势**：在同等规模项目中率先建立了**发布验证清单机制**——beta.3 因"规范发布者只接受完整验证清单"而阻塞自动化发布，虽拖延了版本节奏，但体现了对质量门槛的坚持。安全策略方向也已超出多数同类项目：`installPolicy` 支持三道态度（允许/警告/拒绝），CLI 与 Control UI 双端都支持操作者审阅确认，解决了"全盘拒绝/盲目放行"的二元困境。多 Agent 消息投递隔离（#126424）则是对多智能体协作安全边界的实质性补强。

- **与 Hermes Agent 对比**：Hermes 功能面更广（桌面端 Bot Mode、Kanban、Fleet 更新跟踪），但稳定性问题也更分散；OpenClaw 则集中火力在消息可靠性与会话状态保持上，技术路线更聚焦。两者社区规模相当（均约 500 条 PR 日更新），但 OpenClaw 的 P0（SQLite 损坏复发）更需警惕。

- **社区信任度**：从讨论焦点看，用户对 OpenClaw 的发布质量有较高期待（#125626 有 18 条协作验证评论），说明社区愿意参与质量共治，但也反映出维护者审核资源确实吃紧——大量 PR 长时间停留在 `waiting on author` 状态。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **更新/安装流程可靠性** | Hermes、Pi | Hermes 在 Debian/Fedora/macOS 上多次报告安装失败与更新 split-brain；Pi 作者坦言放弃 Windows 上折腾 git bash，转向原生 PowerShell 工具。跨发行版、跨平台更新链路是目前用户信任的最大缺口 |
| **多端会话/状态同步** | Hermes、OpenClaw、Pi | Hermes 桌面端更新后会话不加载（#89675）、Telegram 更新后桌面端不刷新（#42962）；OpenClaw 有 OAuth 所有权丢失和会话投递越界问题（均已修复）；Pi 有 Abort 后工具结果错配到已中止会话（#8525）。会话状态的一致性仍是普遍难点 |
| **长会话/上下文压缩稳定性** | Hermes、Pi | Hermes 遭遇 DeepSeek 500k tokens 上下文压缩后会话永久卡死（#78981）；Pi 需规范化历史消息顺序以避免 Kimi 等严格校验提供商报 400（#8536）。长会话在不同模型间的可移植性是真实痛点 |
| **异步取消与并发死锁** | OpenHands SDK、Temporal | OpenHands 的 AsyncExecutor.close() 永久挂起、EventBus 超时僵尸线程（#4597/#4598）；Temporal 的 ambiguous History timeout 导致 task start 未送达（#11733）。两项目均在处理"同步阻塞代码无法被异步取消中断"这一架构性难题 |
| **协议互操作与扩展消息平台** | OpenHands、Hermes、Pi | OpenHands 的 A2A 服务端 PR（#4590）使 agent 可被发现并互操作；Hermes 推进 Buzz 消息平台接入（#93265）；Pi 覆盖多模型供应商的 finish reason 透传。生态正从单机工具走向网状协作 |
| **第三方模型（DeepSeek/Kimi 等）兼容性** | Hermes、Pi | DeepSeek 在 Hermes 中触发 `title_generation` 失败和压缩卡死；Pi 针对 Kimi 的严格消息顺序做了针对性规范化。国产模型的协议差异正在消耗大量修复精力 |
| **Windows 平台体验** | OpenClaw、Hermes、Pi | OpenClaw 的 vitest EBUSY（#119796）、Hermes 的 kanban.db-wal 反复删除与更新死循环、Pi 的路径自动完成与 PowerShell 工具——Windows 已成为不可忽视的第二平台 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|---|---|---|---|
| **OpenClaw** | 自主智能体核心基础设施：消息投递、多 Agent 隔离、安全策略、会话恢复 | 自部署 Agent 平台运营者、多 Agent 场景开发者 | 强发布验证流程 + 安全策略三道态度；架构上强调 Agent 绑定频道隔离、规范化的安装策略确认机制 |
| **Hermes Agent** | 全功能个人 AI 助手：桌面应用 + 多消息平台接入 + Fleet 管理 | 桌面端重度用户、多设备个人用户 | 双层架构（桌面端 + Gateway）；功能面广度优先，近期集中修补 Bot Mode 与 Kanban 等具体体验；Fleet 更新可靠性已升级为跟踪 Epic（#91277） |
| **OpenHands SDK** | Agent 开发框架/SDK：API 稳定性、工具调用链、Agent Server | 构建自定义 Agent 应用的开发者 | 仓库边界明确（SDK + Agent Server + 规范 API）；强调崩溃恢复容错（孤儿工具结果容忍）、并发模型（per-conversation lock）；即将具备 A2A 服务端能力 |
| **Pi** | 终端/编辑器优先的 Agent 工具：TUI、本地模型（llama.cpp）、扩展 API | CLI/TUI 深度用户、扩展开发者 | 轻量级、单仓库、迭代极快；架构偏向可嵌入式（扩展事件、ctx API）；对 OpenAI 兼容层做严格的互操作对齐 |
| **Temporal** | 分布式工作流引擎（非 Agent 项目，但常被用于 Agent 任务编排） | 生产级后端工程师 | 强一致性的任务队列与历史存储；当前正补齐 worker callbacks 全套能力与 OTEL 可观测性 |

---

## 6. 社区热度与成熟度

**第一梯队：高吞吐、快速迭代（日更新数百条）**
- **OpenClaw** 与 **Hermes Agent** 体量相当，均处于"功能密集合并 + 稳定性瓶颈凸显"的阶段。OpenClaw 更偏质量巩固（发布验证阻塞、P0 跟踪），Hermes 更偏功能打磨（桌面端密集修复）。

**第二梯队：中活跃、极速收敛（数十条量级）**
- **Pi** 表现最健康：Issue 关闭率 95.8%、PR 多数当日合并、无积压，属于"小步快跑"模式。**OpenHands SDK** 处于转型期：在修复并发问题的同时推进 A2A 战略功能，社区贡献者活跃度高。

**第三梯队：基础设施型（Issue 少、PR 持续）**
- **Temporal** 作为工作流引擎，Issue 提交天然少于 Agent 项目，但 PR

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-24

---

## 1. 今日速览

过去24小时内，Hermes Agent 仓库保持了极高的社区活跃度：**406 条 Issue 更新**（新开/活跃 349 条，关闭 57 条）与 **500 条 PR 更新**（待合并 428 条，已合并/关闭 72 条），其中桌面端（Desktop）、网关（Gateway）与安装更新（Install/Update）为最集中的讨论领域。当前项目处于**高强度迭代修复期**，虽无新版本发布，但 `main` 分支上持续有修复 PR 合入（如 Bot Mode 桌面端交互修复、Kanban 数据库连接修复），同时大量 P1 级 Bug 仍处于开放状态且集中在**更新流程可靠性**与**跨配置文件/跨网关状态同步**两大主题上。值得注意的信号是：社区开始主动提交针对 issue 的修复 PR（如 Telegram User-Agent fallback、SSRF-safe client 默认 UA），表明外部贡献者参与度呈上升趋势。

---

## 2. 版本发布

过去24小时内无新版本发布。项目当前最新版本停留在 **v0.20.5**（`b2c4f1f376`），该版本被 #91675 引用为复现环境版本。

---

## 3. 项目进展

过去24小时共有 **72 个 PR 被合并或关闭**。从展示的已合并/关闭 PR 来看，主要进展集中在 **桌面端 Bot Mode 体验修复** 与 **后端稳定性修补** 两个方向，具体包括：

- **Bot Mode 桌面端交互修复**（密集合入，共 4 个 PR）：
  - [#93025](https://github.com/NousResearch/hermes-agent/pull/93025) — 修复 Bots 主视图持续闪烁（strobing）的问题，通过约束 re-front 行为解决渲染抖动。
  - [#93013](https://github.com/NousResearch/hermes-agent/pull/93013) — 修复 Bots 面板中 Cronjob 行点击无响应的问题，现在点击可打开任务详情。
  - [#93065](https://github.com/NousResearch/hermes-agent/pull/93065) — 使应用内浏览器在 Bot Mode 中可用，点击链接不再像 no-op。

- **Kanban 看板稳定性**：
  - [#93236](https://github.com/NousResearch/hermes-agent/pull/93236) — 复用事件流数据库连接，避免 Windows 上因每 300ms 开关 WAL 连接导致 `kanban.db-wal` 被反复删除、看板卡顿的问题。

- **工具调用循环防护**：
  - [#60087](https://github.com/NousResearch/hermes-agent/pull/60087) — 为 `ToolCallGuardrailController` 增加"内容不变但参数变化"的重复工具结果检测，弥补了原有基于签名的循环检测盲区。

这些修复表明项目正在**逐个击破 Bot Mode 的桌面端体验问题**，同时 Kanban 看板在 Windows 上的性能问题得到针对性解决。整体来看，项目在"打磨既有功能稳定性"上向前推进了明显一步。

---

## 4. 社区热点

今日讨论最集中的议题呈现出"**维护者自驱动治理**"与"**用户真实痛点**"两大类别：

- **#66616 [skills-index-watchdog] Skills index is stale or degraded**（83 条评论，[链接](https://github.com/NousResearch/hermes-agent/issues/66616)）
  由 @nousbot-eng 发起，是自动化探针报告：Skills Hub 的索引文件已 29.8h 未刷新（阈值 26h）。虽然这是一条机器人维护的 issue，但 83 条评论说明该问题已引发大量关注，且有关于 watchdogs 策略的详细讨论。这反映了项目**自动化运维体系正在运作但存在缺口**。

- **#88584 [Automated Nous integration is blocked]**（23 条评论，[链接](https://github.com/NousResearch/hermes-agent/issues/88584)）
  用户 @echokos 报告 cron 作业自动合入流程被 `cron/jobs.py` 的冲突阻断，导致 Enterkey 上游更新停滞。

- **#84834 [Webhook Feature Package — graph-gated repair]**（23 条评论，[链接](https://github.com/NousResearch/hermes-agent/issues/84834)）
  Webhook 全链路修复的 meta-issue，涉及入口、执行、投递、配置、管理 UI、部署和文档，说明 Webhook 功能面存在系统性问题，社区正在组织系统性修复。

- **#89675 [Desktop: no sessions load after update]**（21 条评论，👍 2，[链接](https://github.com/NousResearch/hermes-agent/issues/89675)）
  高影响力 Bug：macOS 桌面端更新后，所有 agent profile 的会话均无法加载。2 个 👍 表明受影响用户较多。

- **#18715 [Support remote Hermes agent with local tool execution]**（16 条评论，👍 26，[链接](https://github.com/NousResearch/hermes-agent/issues/18715)）
  从 5 月一直活跃至今的功能请求，获得 **26 个 👍**，是社区呼声最高的功能之一。用户希望将模型推理与工具执行分离在不同机器上。

- **#68871 [Add messaging support for Buzz]**（19 条评论，👍 16，[链接](https://github.com/NousResearch/hermes-agent/issues/68871)）
  已有对应 PR **#93265**（open，[链接](https://github.com/NousResearch/hermes-agent/pull/93265)）正在推进 Buzz 适配，包含线程隔离与被动上下文保留。

---

## 5. Bug 与稳定性

过去24小时新增/活跃的 Bug 类 Issue 数量多且覆盖面广，按严重程度排列如下：

### P1 级（严重，影响核心使用）

- **#91675 [Windows: gateway start prints ✓ then dies after 6s liveness poll]**（[链接](https://github.com/NousResearch/hermes-agent/issues/91675)）
  已复现于 v0.20.5。`schtasks /run` 路径下 gateway 启动后崩溃，且冷启动仅恢复当前 profile。是此前修复 #84185 的后续跟踪问题，暂无 fix PR。

- **#78981 [Session permanently dies after DeepSeek context-compression hangs]**（[链接](https://github.com/NousResearch/hermes-agent/issues/78981)）
  长会话（500k tokens）在上下文压缩时流式响应永久停滞，600s 上限后整个会话无法恢复，后续消息无法启动新回合。严重损害长会话可靠性。

- **#84220 [Desktop Home → new chat binds files pane to previous project]**（[链接](https://github.com/NousResearch/hermes-agent/issues/84220)）
  桌面端从命名项目切回 Home 后，文件面板仍绑定旧项目的 cwd。

- **#87093 [Debian installation broken; uv.lock & npm install failed]**（👍 4，[链接](https://github.com/NousResearch/hermes-agent/issues/87093)）
  用户反馈 Debian 13.6 上安装脚本执行失败，涉及 `uv.lock` 与 `npm install`。

- **#71047 [config set duplicates top-level key + Telegram streaming duplicates message]**（[链接](https://github.com/NousResearch/hermes-agent/issues/71047)）
  两个独立问题合报：配置写入产生重复键、Telegram 流式回复导致消息重复投递。

### P2 级（中等，影响特定场景）

- **#88275 [Desktop renderer burns 40-70% CPU at idle]**（[链接](https://github.com/NousResearch/hermes-agent/issues/88275)）
  macOS Intel 设备上桌面端渲染进程持续高 CPU 占用，导致热降频。禁用 GPU 可部分缓解。

- **#93063 [Fedora 44 installation failed]**（8 条评论，[链接](https://github.com/NousResearch/hermes-agent/issues/93063)）
  与 #87093 同类的安装问题，说明跨发行版安装脚本兼容性是当前高频痛点。

- **#67605 [Profile switch is partial — MCP tools and secrets from wrong profile]**（[链接](https://github.com/NousResearch/hermes-agent/issues/67605)）
  桌面端/dashboard 切换 profile 时，MCP 工具未加载，secrets 仍解析自启动 profile。

- **#77277 [Desktop in-app update loops forever on Windows]**（[链接](https://github.com/NousResearch/hermes-agent/issues/77277)）
  更新程序将自身 respawn 的后台进程识别为"另一 Hermes 进程"，导致更新永远失败。

- **#42962 [Desktop active session doesn't refresh after Telegram update]**（[链接](https://github.com/NousResearch/hermes-agent/issues/42962)）
  多端会话同步问题，已开放 2 个多月。

### 已有修复 PR 的 Bug

- **Telegram send_image fallback 缺少 User-Agent** → PR **#89262**（open，[链接](https://github.com/NousResearch/hermes-agent/pull/89262)）已提交修复。
- **SSRF-safe client 默认 UA 缺失** → PR **#93259**（open，[链接](https://github.com/NousResearch/hermes-agent/pull/93259)）已提交修复。
- **Bot Mode 桌面端交互问题**（闪烁、Cronjob 行不可点、浏览器不显示）→ PR **#93025/#93013/#93065**（均已合并）。
- **Matrix E2EE 密钥投递不稳定** → PR **#93256**（open，[链接](https://github.com/NousResearch/hermes-agent/pull/93256)）已提交修复，涉及刷新设备列表、重新分享 Megolm 会话等。

---

## 6. 功能请求与路线图信号

值得关注的开放功能请求及对应的 PR 进展：

### 高热度功能请求

- **#18715 [Remote agent + local tool execution]**（👍 26，[链接](https://github.com/NousResearch/hermes-agent/issues/18715)）
  社区呼声最高的功能请求，覆盖远程模型推理与本地工具运行的分离场景。目前尚无对应 PR，但已置为 P2 并进入 needs-decision，说明维护者已关注。

- **#68871 [Buzz messaging support]**（👍 16，[链接](https://github.com/NousResearch/hermes-agent/issues/68871)）
  对应 PR **#93265**（[链接](https://github.com/NousResearch/hermes-agent/pull/93265)）已完成线程隔离与上下文保留设计，并支持 opt-in 的被动上下文。若合入，Buzz 将成为继 Discord/Telegram/Matrix 后的新消息平台。

### 正在推进中的 Feature PR

- **#92893 [pre_llm_call runtime_override]**（[链接](https://github.com/NousResearch/hermes-agent/pull/92893)）
  允许插件在 `pre_llm_call` 钩子中直接修改实际 LLM 调用的 API kwargs，避免 monkey-patch 内部方法。这将提升插件生态的可扩展性。

- **#87983 [social-har-api-connectivity skill]**（[链接](https://github.com/NousResearch/hermes-agent/pull/87983)）
  通过 CDP 驱动 Chrome 捕获登录流量，以授权方式获取社交平台 API 凭据。涉及安全敏感性，需要关注权限边界。

- **#90022 [skills_guard 扩展威胁模式]**（[链接](https://github.com/NousResearch/hermes-agent/pull/90022)）
  增加 SQL 注入、XSS、VBA、Unicode 混淆、供应链等 14 种新检测模式。

- **#93257 [hermes-kame-api-rotation 入插件索引]**（[链接](https://github.com/NousResearch/hermes-agent/pull/93257)）
  第三方 API 密钥轮换插件提交到官方插件索引。

### 路线图信号

- **#91277 [Fleet update reliability tracking]**（[链接](https://github.com/NousResearch/hermes-agent/issues/91277)）
  由 @teknium1 发起，系统性跟踪"本地/多 profile/远程/image-managed"四类部署方式的更新可靠性问题，关联 15+ PR。可视为**下一阶段更新系统的重构路线图**。

- **#93091 [Bot Mode reliability program]**（[链接](https://github.com/NousResearch/hermes-agent/issues/93091)）
  提出 bot 失败原因类型化、消息 TTL、注意力徽章、leader 路由、重试策略等完整改进方案。

- **#83565 [Child-process credential-inheritance closure]**（[链接](https://github.com/NousResearch/hermes-agent/issues/83565)）
  作为 campaign epic，系统性跟踪"子进程凭据继承"类安全问题，涵盖多个 PR 和 Issue。

---

## 7. 用户反馈摘要

从今日活跃的 Issues 中可提炼出以下真实用户痛点与场景反馈：

**痛点一：更新/安装流程不可靠**
- 多用户在 Debian（#87093[←链接](https://github.com/NousResearch/hermes-agent/issues/87093)）、Fedora 44（#93063[←链接](https://github.com/NousResearch/hermes-agent/issues/93063)）上安装失败，错误集中在 `uv.lock` 和 `npm install`。安装在非主流发行版上的兼容性是重大短板。
- macOS 桌面端在终端执行 `hermes update` 后，应用可被重建但 `/Applications/Hermes.app` 保持旧版，形成 split-brain（#52339[←链接](https://github.com/NousResearch/hermes-agent/issues/52339)）。
- 非默认 profile 在更新后可能残留旧运行时，导致 ImportError（#56717[←链接](https://github.com/NousResearch/hermes-agent/issues/56717)）。
- macOS 上每次更新后，由于 ad-hoc 重新签名导致 keychain ACL 失配，每次启动都重新弹窗（#91115[←链接](https://github.com/NousResearch/hermes-agent/issues/91115)）。

**痛点二：多端会话/状态不同步**
- 桌面端更新后 session 完全不加载（#89675[←链接](https://github.com/NousResearch/hermes-agent/issues/89675)）。
- 从 Telegram 更新同一会话后，桌面端视图不刷新（#42962[←链接](https://github.com/NousResearch/hermes-agent/issues/42962)）。
- 长任务后 Enter 提交的消息不在 UI 中显示，文本仍留在输入框（#68927[←链接](https://github.com/NousResearch/hermes-agent/issues/68927)）。

**痛点三：特定模型/平台的兼容性**
- DeepSeek 上 `title_generation` 因 `response_format` 不支持而失败（#83390[←链接](https://github.com/NousResearch/hermes-agent/issues/83390)）。
- DeepSeek 长会话上下文压缩后永久卡死（#78981[←链接](https://github.com/NousResearch/hermes-agent/issues/78981)）。
- Ollama 本地模型被客户端约 1.5s 主动取消

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-08-24

## 今日速览

过去 24 小时项目活跃度维持高位：共有 17 条 Issue 更新（其中 13 条新开或活跃、4 条关闭）和 25 条 PR 更新（其中 4 条已合并/关闭），无新版本发布。**值得注意的高优先级 bug 集中爆发**——围绕异步取消机制在同步阻塞代码上失效的问题出现了多个关联 Issue（#4597、#4598）以及配套的复现测试 PR #4599，表明社区正在系统性排查并发/死锁类稳定性问题。与此同时，A2A 协议支持（#1060）终于迎来 PR #4590，意味着这一长期搁置的功能请求可能在近期落地。整体来看，项目正处于**高强度修复并发稳定性问题 + 推进战略性协议能力**的双线推进阶段。

---

## 项目进展

今日合并/关闭的 PR 与 Issue 主要聚焦于崩溃恢复容错与项目治理边界：

- **合并/关闭 PR**
  - **fix(sdk): tolerate orphaned tool results in view indices**（[#4594](https://github.com/OpenHands/software-agent-sdk/pull/4594)）— 已关闭。修复 agent-server 重启后崩溃恢复可能保留"孤儿"工具结果，导致 view 索引重建时崩溃的问题。对应的 Issue #4591 同步关闭，这意味着 `ToolCallMatchingProperty` 的 KeyError 问题已有一致性的修复方案兜底。
  - **docs: document SDK repository boundaries**（[#4587](https://github.com/OpenHands/software-agent-sdk/pull/4587)）— 已关闭。官方正式落定 SDK 仓库的边界定位：**本仓库负责 Python SDK、Agent Server、规范 API 与 Agent 行为**，理清了与 Agent Canvas、TypeScript 客户端和自动化服务的边界（对应 Issue #4586 关闭）。

- **对应关闭的 Issue**
  - [#4569](https://github.com/OpenHands/software-agent-sdk/issues/4569) 全局生命周期锁导致的跨会话 wedge 问题被关闭，per-conversation locks 方案已落地（配套优化 PR #4596 今日仍开放中）。
  - [#4543](https://github.com/OpenHands/software-agent-sdk/issues/4543) 自托管 GitLab 无法使用 token 克隆的问题已关闭。
  - [#2044](https://github.com/OpenHands/software-agent-sdk/issues/2044) skills 支持按 skill 覆盖 LLM Profile 的 enhancement 被关闭（具体实现需进一步追踪合并历史）。

---

## 社区热点

| 热点 | 类型 | 讨论热度 | 核心诉求 |
|------|------|----------|----------|
| [**#1060 Google A2A 支持**](https://github.com/OpenHands/software-agent-sdk/issues/1060) | Enhancement | 20 评论 / 26 👍 | 让 OpenHands agent 通过 Google 的 Agent-to-Agent 协议与其他 agent 互操作。该 Issue 自 2025 年 4 月提出至今已横跨一年，社区关注度持续累积 |
| [**#4537 TaskToolSet 子代理调用冻结 Canvas UI**](https://github.com/OpenHands/software-agent-sdk/issues/4537) | Bug (high) | 5 评论 | 子代理运行期间持有父会话锁，导致 Agent Canvas 会话列表停止渲染——直接影响日常使用体验 |
| [**#4543 自托管 GitLab token 无效**](https://github.com/OpenHands/software-agent-sdk/issues/4543) | Bug (medium) | 5 评论 | 非 gitlab.com 实例的 token 被忽略，阻断私有仓库克隆场景（今日已关闭） |
| [**#2044 按 skill 覆盖 LLM Profile**](https://github.com/OpenHands/software-agent-sdk/issues/2044) | Enhancement | 5 评论 | 简单 skill 任务也应使用低成本模型，避免不必要的开销（今日已关闭） |

**分析**：A2A 支持是当前社区**呼声最集中**的协议级能力诉求，且恰逢 Google A2A 生态窗口期。值得关注的是，社区成员 @lukegalea 在今日提交了 PR [#4590](https://github.com/OpenHands/software-agent-sdk/pull/4590)（支持 Agent Card + JSON-RPC/SSE 的 A2A 服务端实现），为该 Issue 带来了实质性的落地希望，预计将成为下一版本的重要特性之一。

---

## Bug 与稳定性

> 按严重程度从高到低排列。`状态`说明：✅ 已有修复 PR / 🔄 修复进行中 / ❌ 暂无修复。

### 🔴 高优先级（Priority: High）

| Issue | 问题描述 | 状态 |
|-------|----------|------|
| [#4537](https://github.com/OpenHands/software-agent-sdk/issues/4537) | **TaskToolSet 子代理调用期间持有父会话的全局锁**，导致 agent canvas 会话列表冻结、executor 池饱和 | ❌ 暂无修复 PR，但 #4569 的 per-conversation lock 改造可能部分缓解 |
| [#4597](https://github.com/OpenHands/software-agent-sdk/issues/4597) | **`AsyncExecutor.close()` 永久挂起**：当任务阻塞在同步代码（忽略取消的 worker 线程）时，close 无法退出 | ✅ PR [#4599](https://github.com/OpenHands/software-agent-sdk/pull/4599) 添加了 2 个失败测试作为复现，修复尚未出现（预期方向是允许线程泄漏但确保进程退出） |
| [#4598](https://github.com/OpenHands/software-agent-sdk/issues/4598) | **bubus EventBus 处理器超时后留下僵尸线程**：`asyncio.wait_for` 无法中断底层同步阻塞调用，超时后线程继续存活 | ✅ PR [#4599](https://github.com/OpenHands/software-agent-sdk/pull/4599) 属同一根因，测试先行 |
| [#4601](https://github.com/OpenHands/software-agent-sdk/issues/4601) | **浏览器工具只检查 Chromium 二进制存在，不验证能否真正启动**，缺少共享库、损坏二进制、display/headless 等导致的伪可用状态 | ✅ PR [#4602](https://github.com/OpenHands/software-agent-sdk/pull/4602) 已提交，作 pre-flight 启动验证 |

### 🟡 中优先级（Priority: Medium）

| Issue | 问题描述 | 状态 |
|-------|----------|------|
| [#4578](https://github.com/OpenHands/software-agent-sdk/issues/4578) | 会话历史包含冒号分隔的 tool-call ID 时，从 Kimi K3 切换到 GPT-5.6 失败 | ❌ 暂无修复 |
| [#4583](https://github.com/OpenHands/software-agent-sdk/issues/4583) | 文件编辑器 insert 在文件无尾随换行时拼接到最后一行而非新起一行 | ❌ 暂无修复 |
| [#4575](https://github.com/OpenHands/software-agent-sdk/issues/4575) | agent 终端命令继承 agent-server 进程优先级，影响资源调度 | ❌ 暂无修复 |
| [#4591](https://github.com/OpenHands/software-agent-sdk/issues/4591) | 崩溃恢复后出现孤儿 observation 导致 `manipulation_indices` 崩溃，对话被永久卡住 | ✅ PR [#4592](https://github.com/OpenHands/software-agent-sdk/pull/4592)、[#4594](https://github.com/OpenHands/software-agent-sdk/pull/4594) 已提交 |

### 稳定性总结

今日暴露的 bug 呈现出清晰的模式：**async 取消机制无法中断 C 级同步阻塞操作**（#4597、#4598、#4601 均与此相关）。这属于 asyncio 的已知限制，需要架构层面的隔离策略（如 thread pool + 超时强制丢弃），而非简单取消。PR #4599 通过测试先行的方式将此问题固化为回归用例，方向正确；但修复的最终形态仍待讨论。

---

## 功能请求与路线图信号

| 功能请求 | 关联 PR | 路线图判断 |
|----------|---------|------------|
| [**A2A 协议支持**（#1060）](https://github.com/OpenHands/software-agent-sdk/issues/1060) — 成为 A2A mesh 中的可发现节点 | ✅ [#4590](https://github.com/OpenHands/software-agent-sdk/pull/4590) 已提交，实现 Agent Card + JSON-RPC/SSE | **高概率进入下一版本**。这是今日最重磅的路线图信号 |
| [**按 skill 覆盖 LLM Profile**（#2044）](https://github.com/OpenHands/software-agent-sdk/issues/2044) | 已关闭（未展示对应合并 PR，但实现应该已合入 main） | 已完成 |
| [**per-key tag 端点**（#4577）](https://github.com/OpenHands/software-agent-sdk/issues/4577) — 避免 PATCH /api/conversations/{id} 的 read-modify-write 竞争 | 无 | 已标 ready-for-dev，属于 API 体验优化，预计中短期可排入 |
| [**HOL Guard 安全分析器示例**（#4593）](https://github.com/OpenHands/software-agent-sdk/issues/4593) — 在 SecurityAnalyzerBase 中接入本地安全层 | ✅ [#4600](https://github.com/OpenHands/software-agent-sdk/pull/4600) 已提交（draft） | 社区驱动 + 安全增强，可能以独立 example 形式合入 |
| [**按操作计时插桩**（#4589）](https://github.com/OpenHands/software-agent-sdk/issues/4589) — 为历史上慢/死锁操作加自动化耗时信号 | 无 | 与 #4588 共同构成"可观测性 + 质量门禁"建设方向，反映项目开始系统性治理稳定性问题 |
| [**预发布负载测试门禁**（#4588）](https://github.com/OpenHands/software-agent-sdk/issues/4588) — 阻塞合并的回归保护 | ✅ [#4595](https://github.com/OpenHands/software-agent-sdk/pull/4595) 已提交（CI 阻塞发布流程的 stress 回归） | 若合入将显著提升发布质量基线 |

---

## 用户反馈摘要

- **UI 冻结影响日常使用**（来自 #4537）：用户 @quickbearattack 描述了 TaskToolSet 子代理调用期间，"Agent Canvas 会话列表停止渲染，整个 duration 都不动"。这类问题直接削弱了多任务并行场景的可用性，是最直接影响日常生产力的一类反馈。

- **API 设计细节引发调用方困惑**（来自 #4577）：用户 @BSmick6 指出 `UpdateConversationRequest.tags` 的"替换整个 tag map"语义在当前文档中虽有说明，但"任何希望只更新单个 key 的客户端都得先读后写"，在并发场景下有竞争风险。这是在 API 使用层面的真实摩擦点，解决方案（per-key 端点）简单明确。

- **模型切换遇到历史兼容性壁垒**（来自 #4578）：用户 @rajshah4 报告从 Kimi K3 切换到 GPT-5.6 时，因历史中的 MCP 并行 tool-call 的 ID 中包含冒号而失败。这暴露了**持久化格式与跨模型兼容性**之间的问题——用户期望无缝切换模型，却被存量数据格式约束。

- **安全细节需要更精细的控制**（来自 #4543、#4575）：自托管 GitLab 的 token 被忽略（已修复）、终端命令继承服务器进程优先级，这两个问题的共同点是用户对**私有化部署 / 细粒度资源控制**有明确预期。

- **积极信号——社区主动贡献**：HOL Guard 示例（#4593/#4600）由外部用户 @kantorcodes 主动提出并附带了 PR；A2A 也是由社区成员 @lukegalea 以"我自己想从编排栈通过 A2A 调用 OpenHands agents"为动机直接提交了实现。这表明 SDK 具备良好的可扩展性，社区对协议互操作和安全性扩展有热情。

---

## 待处理积压

### ⚠️ 长期未合并的 PR

| PR | 创建时间 | 已等待 | 说明 |
|----|----------|--------|------|
| [#4044](https://github.com/OpenHands/software-agent-sdk/pull/4044) chore(deps): bump lewagon/wait-on-check-action 1.7.0 → 1.8.1 | 2026-07-09 | **45 天** |

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 2026-08-24

## 今日速览

过去24小时Pi项目共产生48条Issue更新和16条PR更新，整体活跃度健康。**Issue关闭率高达95.8%（46/48）**，绝大多数为新提交的untriaged条目被快速处理或关闭；PR方面同样以合并/关闭为主（13/16），**无新版本发布**。今日工作重心明显偏向稳定性和兼容性修复，包括llama.cpp模型列表暴露、Kimi/OpenAI严格消息顺序规范化、流式错误透传、Windows平台体验等，共完成约13项合并/关闭的PR，项目整体处于高频迭代、快速收敛的维护阶段。值得关注的是，今日开放中Issue仅2条（#7724、#5932），说明维护者响应效率极高。

## 项目进展

今日虽无新版本发布，但合并/关闭的13个PR在多个方向上有实质推进：

**模型与兼容性**
- [#8535](https://github.com/earendil-works/pi/pull/8535) 让**llama.cpp未加载的模型**出现在 `/model` 列表中，后端会自动按需加载，省去手动 `/llama` 操作。该PR与 [#8479](https://github.com/earendil-works/pi/pull/8479) 配合，解决了 #8167 报告的模型列表缺失问题。
- [#8536](https://github.com/earendil-works/pi/pull/8536) **规范化会话历史中的tool-result消息顺序**，修复向严格校验的OpenAI兼容提供商（如Kimi kimi-k2/k3）回放历史时出现的400错误。
- [#8487](https://github.com/earendil-works/pi/pull/8487) 在coding-agent中暴露**finish reason兼容性覆盖**的类型定义（此前仅在API中隐含支持）。
- [#8509](https://github.com/earendil-works/pi/pull/8509) 将OpenRouter等提供商返回的 `network_error` finish reason正确透出为错误，避免静默中断；同时支持无工具模型（toolless models）。

**稳定性与可靠性**
- [#8532](https://github.com/earendil-works/pi/pull/8532) 为grep/find工具的stdout读取**增加单行长度上限**，防止超长行触发V8 RangeError导致父进程崩溃。
- [#8524](https://github.com/earendil-works/pi/pull/8524) 让 `Working...` 状态指示器**保持到 `agent_settled` 回调完成之后再清除**，避免外部观察者误判回合结束。
- [#8513](https://github.com/earendil-works/pi/pull/8513) 修复edit工具中**未转义原始控制字符**（真实换行/制表符）导致的JSON.parse失败，是对 #3370 修复的补充。
- [#8424](https://github.com/earendil-works/pi/pull/8424) 扩展工厂加载失败时**丢弃暂存状态并清理事件监听器**，防止半初始化状态残留。
- [#8505](https://github.com/earendil-works/pi/pull/8505) 为agent重试循环增加 **`maxAgentDelayMs` 上限**（默认30秒），避免退避无限增长。
- [#8500](https://github.com/earendil-works/pi/pull/8500) 修复plan-mode中bash守护的两个误报类别（路径包含"code"被误拦截、计划提取被演示文本干扰）。

**文档与体验**
- [#8482](https://github.com/earendil-works/pi/pull/8482) 修正自定义footer文档，指向 `ctx.getContextUsage()` 这一正确API。

**开放中值得关注的PR**
- [#8032](https://github.com/earendil-works/pi/pull/8032) 为TUI组件增加鼠标事件接收能力（对应issue #7683已关闭，等待合并）。
- [#8512](https://github.com/earendil-works/pi/pull/8512) 新增**可选的PowerShell工具**，改善Windows原生环境体验（作者mitsuhiko坦言放弃在Windows上折腾git bash）。
- [#7952](https://github.com/earendil-works/pi/pull/7952) 为markdown transformer context添加 `messageId` 和 `timestamp`。

## 社区热点

今日讨论最集中的Issues（按评论数排序）：

1. **[#7683 [已关闭] pi-tui组件接收其自身行上的鼠标事件](https://github.com/earendil-works/pi/issues/7683)**（评论11）
   提出为组件增加 `Component.onMouse(event)` 钩子，让组件可自行命中测试其 `LayoutBox` 区域内的鼠标事件。这是TUI交互模型的重要扩展，对应PR #8032尚在开放中，社区讨论持续。

2. **[#8167 [已关闭] 无法选择内置llama.cpp支持的模型](https://github.com/earendil-works/pi/issues/8167)**（评论10）
   用户报告llama-server router模式下的模型不出现在模型列表中，即使 `/llama` 可以正常加载。该问题已被 #8479 和 #8535 两个PR联合修复，社区反馈活跃，是今日模型兼容性的核心议题。

3. **[#7885 [已关闭] npm search不索引新发布的pi-packages](https://github.com/earendil-works/pi/issues/7885)**（评论7）
   用户发布的 `pi-affix-prompt` 包在 `npm search` 中无法被找到，导致无法出现在 pi.dev/packages 画廊。反映**包发现链路**存在问题，影响社区生态的可见性。

4. **[#5932 [开放中] 将ctx.navigateTree()暴露给agent](https://github.com/earendil-works/pi/issues/5932)**（评论7，👍2）
   用户希望 `navigateTree()` 不仅存在于ExtensionCommandContext，也应在普通ExtensionContext中可用，以便自定义 `/goal` 实现。该议题从6月21日讨论至今仍开放，是Extensions API设计的一个重要信号。

5. **[#8183 [已关闭] 文档记录Windows Terminal的Ctrl+Shift+F冲突](https://github.com/earendil-works/pi/issues/8183)**（评论6）
   全屏转录搜索的默认键绑定与Windows Terminal自身查找快捷键冲突，用户建议文档中提供重绑指导。

**社区诉求分析**：今日热点集中在 (a) TUI组件交互能力的边界扩展；(b) 本地模型（llama.cpp）的无缝集成；(c) 包生态的可发现性。社区对窗口期短、响应迅速的修复表示认可，同时也期待更细粒度的扩展API（如鼠标事件、navigateTree）。

## Bug 与稳定性

今日报告的Bug按严重程度排列：

**严重（可能导致数据错乱/会话挂起）**
- [#8531 [已关闭] 连续"Request timed out"后自动重试静默停滞，会话无限期挂起](https://github.com/earendil-works/pi/issues/8531) — RPC模式下重试逻辑的空白等待问题，无PR但已关闭。
- [#8525 [已关闭] Abort导致SessionManager叶子状态stale，工具结果被错配到已中止的assistant](https://github.com/earendil-works/pi/issues/8525) — 中止后的工具结果parentId指向错误节点，恢复时会因无匹配tool use而报错。
- [#8537 [已关闭] Kimi (moonshotai-cn) 处理重放历史时出现400错误：孤儿tool消息、交错user消息、重复tool_call_id](https://github.com/earendil-works/pi/issues/8537) — **已有修复PR #8536**。
- [#8504 [已关闭] OpenAI兼容提供商在tool_call deltas上回显空 `custom: {}` 导致函数调用参数被丢弃](https://github.com/earendil-works/pi/issues/8504) — 普通function工具调用被误路由到custom-tool路径。

**中等问题**
- [#8526 [已关闭] Vertex AI数组包装的错误体被丢弃，导致"(no body)"文本触发错误的上下文溢出压缩](https://github.com/earendil-works/pi/issues/8526) — 错误解析的可观测性缺陷，可能引发误压缩。
- [#8527 [已关闭] openai-responses的 `function_call_arguments.done` 事件中arguments可能为undefined触发TypeError](https://github.com/earendil-works/pi/issues/8527)。
- [#8521 [已关闭] edit工具：包含原始控制字符的字符串化edits仍验证失败](https://github.com/earendil-works/pi/issues/8521) — **已有修复PR #8513**。
- [#8541 [已关闭] OpenAI兼容的429错误被表面为通用"ERROR"，无原始信息](https://github.com/earendil-works/pi/issues/8541) — 错误透传链路不够详尽。
- [#8529 [已关闭] todo工具的toggle操作非幂等，重复调用会静默取消已完成项](https://github.com/earendil-works/pi/issues/8529) — 缺少"complete/uncomplete"幂等操作。

**轻微/体验问题**
- [#8528 [已关闭] 复制agent输出时尾随空格被保留](https://github.com/earendil-works/pi/issues/8528)，源于Markdown渲染会padding每行至终端宽度。
- [#8523 [已关闭] Windows上带盘符的绝对路径 `@` 自动完成无建议](https://github.com/earendil-works/pi/issues/8523)。
- [#8534 [已关闭] TUI中highlight.js的 `symbol` 语法域未着色，Elixir原子显示为纯文本](https://github.com/earendil-works/pi/issues/8534)。

今日没有发现崩溃级别的回归，但#8525的abort状态管理问题值得后续关注（关联#7724冷恢复问题）。

## 功能请求与路线图信号

今日收到的功能请求信号：

**有明确实现路径 / 即将纳入**
- [#7683](https://github.com/earendil-works/pi/issues/7683) 组件鼠标事件 → **PR #8032已实现，等待合并**（TUI交互增强）。
- [#8539](https://github.com/earendil-works/pi/issues/8539) 在 `/model` 列表中显示llama.cpp未加载的模型 → **PR #8535已合并**。
- [#8533](https://github.com/earendil-works/pi/issues/8533) 为扩展提供窄范围的Skill可见性API（deny-only） → 需要维护者评估扩展生态的方向。
- [#8457](https://github.com/earendil-works/pi/issues/8457)（👍2）允许技能像prompt模板一样在句中调用（`/name args` 出现在首行之后） → 编辑器体验的重要增强。

**处于设计讨论阶段**
- [#5932](https://github.com/earendil-works/pi/issues/5932)（开放中）暴露 `ctx.navigateTree()` 给普通ExtensionContext → 已有2个👍，从6月讨论至今。
- [#8344](https://github.com/earendil-works/pi/issues/8344)（no-action）全屏TUI中按工具输出块独立展开/折叠 → 维护者标记不采取行动，但社区有需求声。
- [#8452](https://github.com/earendil-works/pi/issues/8452) 改进默认压缩提示词，使摘要merge/deduplicate并保留continuation状态 → 涉及核心上下文管理策略，值得跟进。
- [#8530](https://github.com/earendil-works/pi/issues/8530) 新增 `user_bash_complete` 扩展事件 → 对自动化工作流有用。

**开发者体验**
- [#8512](https://github.com/earendil-works/pi/pull/8512) 可选的PowerShell工具（开放中）→ Windows原生用户呼声高，作者已有初步实现。
- [#8529](https://github.com/earendil-works/pi/issues/8529) todo工具幂等complete/uncomplete → 小而优的API改进。
- [#8372](https://github.com/earendil-works/pi/issues/8372) Windows（WSL/原生）键位冲突问题系统性梳理。

## 用户反馈摘要

**满意与正面反馈**
- llama.cpp模型的列表问题获得快速响应（#8167被两个PR联合修复，且同时覆盖了 `--models-dir` 和 `--models-preset` 两种用法），用户对修复方向表示认可。
- 对OpenAI兼容提供商的行为对齐（#8536、#8509）被认为是走向"严格模式互操作"的重要一步。

**真实痛点**
- **Windows平台仍是短板**：多起Windows相关Issue（键位冲突 #8183/#8372、路径自动完成 #8523、PowerShell支持 #8512）。用户反映Windows Terminal的快捷键冲突频繁，且文件路径处理体验与Unix差异较大，powershell工具PR的评论中作者mitsuhiko直言"正在放弃让git bash在Windows上正常工作"。
- **错误

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 开源项目动态日报 — 2026-08-24

## 今日速览

过去 24 小时 Temporal 项目整体活跃度较高，主要精力集中在 **worker callbacks 大型功能系列 PR** 的持续推进上（8 个相关 PR 同日更新），同时完成了 **1.32.0 发布分支的准备工作**。Issue 侧相对平静，仅新增 1 条关于 "ambiguous History timeout 导致 task start 未能送达" 的 bug 报告；PR 侧流量较大，共 28 条更新，其中 9 条已合并/关闭。值得注意的是，新 issue #11733 与该 bug 对应的修复 PR #11734 在同日出现，修复响应速度较快，项目整体健康度良好。

---

## 项目进展

今日无正式版本发布，但 **1.32.0 发布分支已准备完成**（`#11737` 已关闭），说明新版本开发周期已进入收尾阶段，通常意味着收集社区反馈、修复稳定性的窗口正在打开。

合并/关闭的 PR 中值得关注的有：

| PR | 说明 | 状态 |
|---|---|---|
| [#11737](https://github.com/temporalio/temporal/pull/11737) | 1.32.0 发布分支准备：覆盖 governance 文件 + 更新依赖 | ✅ 已关闭 |
| [#10290](https://github.com/temporalio/temporal/pull/10290) | 为 Nexus HTTP endpoints 添加 OTEL instrumentation（从 5 月持续至今，约 3 个月合并） | ✅ 已关闭 |
| [#10192](https://github.com/temporalio/temporal/pull/10192) | 支持 standalone callbacks（worker callbacks 功能的前置基础） | ✅ 已关闭 |
| [#11726](https://github.com/temporalio/temporal/pull/11726) | 测试分片 salt 自动更新（CI 基础设施维护） | ✅ 已关闭 |

特别是 **#10290 和 #10192 的合并**，标志着很早启动的 OTEL 可观测性增强和 standalone callbacks 基础能力正式落地，为后续 worker callbacks 全套功能的合入扫清了前置依赖。

---

## 社区热点

### 1. Worker Callbacks 功能系列（当前最大开发主线）

由 `@chrsmith` 主导的 **worker callbacks** 功能栈今日有 7-8 个 PR 密集更新，包括 [#11589（核心实现）](https://github.com/temporalio/temporal/pull/11589)、[#11566（callback 类型可配置化）](https://github.com/temporalio/temporal/pull/11566)、[#11567（SANOs 完成回调）](https://github.com/temporalio/temporal/pull/11567)、[#11520（CallbackInfo.outcome 填充）](https://github.com/temporalio/temporal/pull/11520)、[#11735（standalone Nexus operators 上的 Links 支持）](https://github.com/temporalio/temporal/pull/11735) 等。这些 PR 均为 stacked 模式，统一合入 `feature/worker-callbacks` 分支后再进 main，表明 **Temporal 正在为 worker 回调构建一套完整的、覆盖 workflow/activity/Nexus 多场景的能力体系**。生态影响面广，社区关注度高。

### 2. Schedule 时间跳跃（Time Skipping）双 PR 并行

`@feiyang3cat` 在 chasm framework 的 time skipping（[#10934](https://github.com/temporalio/temporal/pull/10934)）基础上，今日新增了 **[#11741]（schedules 场景的 time skipping 实现）**（https://github.com/temporalio/temporal/pull/11741），依赖 api repo 的 [PR #856](https://github.com/temporalio/api/pull/856) 变更。这延续了 Temporal 在 **测试时跳过实际等待时间** 方向上的能力铺设，对改善开发体验有直接价值。

### 3. 运维能力增强

`@verma-divyanshu-git` 提交的 [#11659](https://github.com/temporalio/temporal/pull/11659) 为 **MySQL 增加多主机和 DNS SRV 连接支持**，解决集群环境中多 MySQL 实例的 failover 和只读路由问题。该 PR 自 8-19 创建以来持续更新，是基础设施方向一个值得关注的增强。

---

## Bug 与稳定性

### 严重程度：高

**#11733 Task start can remain undelivered after an ambiguous History timeout**（[Issue 链接](https://github.com/temporalio/temporal/issues/11733)）  
- **报告时间**：2026-08-23，作者 `@ali-khokhar-nvidia`  
- **问题描述**：当 History 已提交 workflow/activity task start，而原始 worker poll 仍处于活跃状态时，一个 per-attempt 的 RPC deadline 会让 task 在 History 中已启动但从未送达 worker，Matching 应该通过 same-request-ID 合约恢复已提交的响应，但当前行为可能导致任务永远丢失。这属于 **任务一致性问题，直接影响工作流可靠性**。  
- **修复状态**：作者同日提交了 **修复 PR #11734**（[链接](https://github.com/temporalio/temporal/pull/11734)），方案是：在原始 poll 活跃期间，跨 attempt-local deadline 保留同一个 `RecordWorkflowTaskStarted`/`RecordActivityTaskStarted` request ID；当 deadline 导致结果歧义时，在同一个 attempt 内保留后续的 `BusyWorkflow`。**响应迅速，值得关注合入进度**。

### 严重程度：中

**#11397 Fix constant/error-dependent retry jitter being truncated to a no-op**（[PR 链接](https://github.com/temporalio/temporal/pull/11397)）  
- `common/backoff/retrypolicy.go` 中 `addJitter` 的实现由于类型运算问题，在 2s 基础时长下 `WithJitter(0.1)` 只能返回精确的 2.000s，jitter 完全未生效。影响所有依赖 retry policy 的调用方。  
- PR 已在 8-23 更新，等待合入。

### 严重程度：低

**#11355 Preserve logger tags across Skip()**（[PR 链接](https://github.com/temporalio/temporal/pull/11355)）  
- `zapLogger.Skip()` 克隆 logger 时未携带 `tags`，导致 throttle logger 包装后丢失已有标签。已附带测试修复，8-23 有更新。

---

## 功能请求与路线图信号

| 功能方向 | 相关 PR / Issue | 当前状态 | 判断 |
|---|---|---|---|
| **Worker Callbacks**（完整闭环） | #11589、#11566、#11567、#11520、#11735、#11380 + 已合并的 #10192 | feature 分支持续推进，多 PR stacked | 明确进入下一版本路线图 |
| **Chasm + Schedules Time Skipping** | #10934、#11741 | 两个 PR 并行推进 | 持续开发中，可能进入后续版本 |
| **MySQL 多主机 / SRV 连接** | #11659 | 持续更新中 | 有明确运维场景需求，合入概率较高 |
| **独立 history scanner 流控** | #11738（新增 `worker.historyScannerRPS` 动态配置） | 新 PR，待 review | 小改动，属于易采纳的优化型功能 |
| **Parent Close Policy 测试补齐** | #11739（7 个新测试用例） | 新 PR | 质量改进为主，合入难度低 |

---

## 用户反馈摘要

由于过去 24 小时 Issue 仅 1 条且无评论数据，用户反馈主要从 Issue #11733 的描述中提炼：

**核心用户诉求 —— 强调系统一致性语义**：报告者在 Expected Behavior 中明确表达了期望——"相同 request-ID 合约下，Matching 应能从 History 恢复已提交的响应"。这表明用户对 Temporal 的 **at-least-once 语义和 request-ID 去重机制有较强信任和依赖**，遇到超时截断引入的语义缺口时，期望系统能自愈而非丢失任务。这类反馈反映了生产用户对分布式系统一致性的敏感度，值得维护团队重视。

另有部分 PR 属于外部贡献者提交（如 `@verma-divyanshu-git` 的 MySQL SRV 支持、`@geraldw-ai` 的 jitter/logger 修复），说明社区对运维化、可观测性方向的改进有持续兴趣。

---

## 待处理积压

以下 PR / Issue 持续未合并或未解决，建议维护者关注：

| 项目 | 创建时间 | 已等待 | 备注 |
|---|---|---|---|
| [#10934](https://github.com/temporalio/temporal/pull/10934) add time skipping to chasm framework | 2026-07-06 | **约 7 周** | 已有后续 PR #11741，但本 PR 仍未合入；有测试覆盖，建议加速 review |
| [#11397](https://github.com/temporalio/temporal/pull/11397) retry jitter 修复 | 2026-08-02 | 3 周 | Bug 明确且修复简单，长期未合入可能影响所有 retry 调用方 |
| [#11355](https://github.com/temporalio/temporal/pull/11355) logger tags 修复 | 2026-07-30 | 3.5 周 | 小修复但长时间待 review |
| [#11380](https://github.com

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*