# OpenClaw 生态日报 2026-08-17

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-16 22:41 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，这是根据 OpenClaw (github.com/openclaw/openclaw) 2026-08-17 的 GitHub 数据生成的项目动态日报。

---

# OpenClaw 项目动态日报 — 2026-08-17

## 1. 今日速览

项目活跃度处于**极高**水平：过去 24 小时 Issue 与 PR 更新均达到 500 条（受 GitHub API 分页上限截断，实际总量可能更高），新开/活跃 Issue 与待合并 PR 数量庞大。社区对 **P1 级“静默失败”与“消息丢失”类问题的关注度持续飙升**（如 #121058 评论数达 97），且多个历史遗留 P1 问题长期未决，维护者审查积压风险加剧。与此同时，团队在**安全加固**（#116489、#124858）、**会话状态持久化**（#124857）与 **UI 性能**（#124868）方面提交了密集的 PR，显示出较高的迭代速度。项目整体处于“高产但伴随着高稳定性欠债”的状态。

## 2. 版本发布

**无功能性版本发布。** 今日唯一 release 为辅助性数据存档：

- **pr-124528-profiles**: [PR #124528 Gateway profile evidence](https://github.com/openclaw/openclaw/releases/tag/pr-124528-profiles)
  - **内容**: 针对 PR #124528 的 CPU profiles 归档，包含修复前与修复后（exact-head）的三节点、12 并发轮次 Gateway 压力测试数据。
  - **解读**: 这是为支撑 PR #124528 性能对比而发布的内部数据包，非用户面向的功能版本。它暗示团队正在针对 **Gateway 事件循环热点**（event-loop hotspot）进行专项优化，与今日活跃的 #115908、#112423 等事件循环阻塞问题形成呼应。

由于无功能更新，**无破坏性变更或迁移注意事项**。

## 3. 项目进展

今日有 **86 条 PR 被合并/关闭**，以下为其中影响面较大的合并项（基于展示列表）：

- **[#116489](https://github.com/openclaw/openclaw/pull/116489) feat(security): require acknowledgement for install policy warnings** — 安全增强，要求操作者对安装策略警告进行显式确认，涉及 CLI、Gateway、macOS 等多个入口，是今日最大的安全合并。
- **[#120900](https://github.com/openclaw/openclaw/pull/120900) feat(ui): review install policy warnings** — 与 #116489 配套的 UI 功能，允许管理员在 Control UI 中审查并确认安装策略警告，打通了安全流程的最后一环。
- **[#124870](https://github.com/openclaw/openclaw/pull/124870) refactor(security): consolidate path containment onto canonical fs-safe guard** — 统一了 agent、gateway、plugin 等各层的路径包含检查逻辑，修复了 `..cache` 等特殊路径被误判为逃逸的问题，是重要的安全与稳定性重构。
- **[#124865](https://github.com/openclaw/openclaw/pull/124865) refactor: replace assertion chains with typed fixture builders (wave 2)** — 测试基建重构，将脆弱的 `as unknown as` 断言链替换为类型安全的 fixture builder，提升测试可维护性。

**整体评估**: 项目在安全边界统一、安装策略可视化、路径校验加固方面有明显推进。但**关键的稳定性修复（如 #121058 静默失败）尚未看到合并的 fix PR**，因此核心痛点并未在今日消除。

## 4. 社区热点

讨论焦点主要集中在长期未决的 P1 问题上，用户诉求高度集中于**消息可靠性与会话一致性**。

- **[#121058](https://github.com/openclaw/openclaw/issues/121058) [CLOSED] [P1] Silent reply failures still recurring after #116277 closed** — 评论 **97** 条，为今日最热 Issue。尽管被标记为 CLOSED，但该问题在 #116277 关闭后仍在监控中持续复发，用户@sloptop-the-terrible 明确指出“cron 日志今天仍在记录新故障”。这是一个典型的“关闭但未修复”的复发型问题，社区不满情绪较高。
- **[#42475](https://github.com/openclaw/openclaw/issues/42475) [OPEN] [P2] Per-agent cost budget enforcement at the gateway level** — 评论 26 条。社区对 **Gateway 级成本管控**（每个 agent 的日/月消费上限）有强烈诉求，希望防止模型调用失控导致高昂账单。
- **[#48003](https://github.com/openclaw/openclaw/issues/48003) [OPEN] [P1] Steer mode does not inject messages mid-turn for main sessions** — 评论 21 条。steer 模式无法在回合中注入消息，直接影响用户对会话的实时干预能力，且已关联 PR，是近期可能取得突破的焦点。

**需求分析**: 用户最关心的不是新功能，而是**“消息不能丢、状态不能错、钱不能失控”**这三大根基性问题。

## 5. Bug 与稳定性

今日报告的 Bug 数量庞大，以下按严重程度排列核心问题，并标注修复状态：

**🔴 危险级（P1 / 数据丢失 / 消息丢失）**

- **[#121058](https://github.com/openclaw/openclaw/issues/121058) 静默回复失败复发** — 高关注（97 评论）。**无直接 fix PR**，且此前同源问题 #116277 已关闭但未彻底修复，风险极高。
- **[#115908](https://github.com/openclaw/openclaw/issues/115908) 会话转录投影活锁导致主线程阻塞** — 有源码级复现（source-repro），**无 fix PR**。持续写入时可能让所有通道停顿数十秒。
- **[#112423](https://github.com/openclaw/openclaw/issues/112423) 大型 SQLite 转录清理阻塞事件循环** — 有 source-repro，**无 fix PR**。与 #115908 同属事件循环健康度问题。
- **[#117609](https://github.com/openclaw/openclaw/issues/117609) 嵌入式助手阶段缺少对临时错误的退避重试** — **有修复方案**（fix-shape-clear, queueable-fix），等待队列化实施。
- **[#97680](https://github.com/openclaw/openclaw/issues/97680) Beta 标签更新后外部插件停留在 latest 版本** — **有修复方案**（queueable-fix），等待队列化实施。
- **[#48003](https://github.com/openclaw/openclaw/issues/48003) Steer 模式不注入消息** — **已有关联 PR**（linked-pr-open），预计近期有修复。
- **[#38327](https://github.com/openclaw/openclaw/issues/38327) Google Vertex/Gemini 回归 “Cannot convert undefined or null to object”** — 无 fix PR，需 live repro，影响

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-17

> 数据窗口：2026-08-16 至 2026-08-17（GitHub `NousResearch/hermes-agent`）｜全部数据来自官方仓库公开信息


## 1. 今日速览

过去 24 小时 Hermes Agent 项目保持**极高活跃度**：Issues 更新 427 条（新开/活跃 283、关闭 144），PR 更新 500 条（待合并 414、合并/关闭 86），并发布 v0.20.2 稳定补丁版本。社区讨论热点集中在**多租户/内存隔离**、**工具 schema token 开销**、**桌面端回归问题**以及**技能索引健康度**几个方向；PR 侧则密集出现安全边界修复（命令审批模式、认证绕过、密钥泄漏）、会话状态修复与桌面端体验改进。整体项目健康度良好，修复与功能开发双线并行推进，但长期未决的 P2 安全类 issue（如审批超时误判、多 profile 密钥泄漏）仍需重点关注。

- 新增 Releases：1 个（v2026.8.16 / v0.20.2，patch 集合版）
- Issues 关闭率：33.7%（144/427）
- PR 合并/关闭率：17.2%（86/500）


## 2. 版本发布

### [Hermes Agent v0.20.2 (v2026.8.16)](https://github.com/NousResearch/hermes-agent/releases)

- **发布日期**：2026-08-16
- **性质**：Patch release
- **内容**：将自 v0.20.1 以来合并的 **~397 个 PR** 汇总为一个稳定的 tagged 版本，供下游消费者（Docker 镜像、托管部署、全新安装）使用。
- **破坏性变更**：发布说明未标注明确破坏性变更。
- **迁移注意**：无特别提示；但今日 issue 中出现 v0.18.2 → v0.20.1 升级时 SQLite FTS5 索引不兼容报告（[#86027](https://github.com/NousResearch/hermes-agent/issues/86027)），建议升级用户注意 `state.db` 的 SQLite 版本兼容情况。


## 3. 项目进展

过去 24 小时有多个重要 PR 进入合入队列或完成关闭，整体项目在**架构重构收尾、安全性加固、桌面端体验修复**三方面取得进展。

### 3.1 大型重构完成

- [#78647 [COMPLETE] Large-file decomposition: 20/20 done](https://github.com/NousResearch/hermes-agent/issues/78647)（79 条评论）已关闭。这是仓库级 god-file 分片 epic，标记“**all god files are sharded, never reverted**”为长期政策，标志着项目代码结构现代化的重要里程碑。

### 3.2 本轮新提交的重点 PR（部分，主要为 OPEN 状态，备选合入）

| PR | 方向 |
|---|---|
| [#87981 feat: raise Codex OAuth context to 350K](https://github.com/NousResearch/hermes-agent/pull/87981) | gpt-5.6/gpt-5.4 Codex OAuth 上下文窗口从 272K 提升到 350K（实测约 371K），减少 ~100K 的广告余量浪费 |
| [#87975 fix(approval): anchor git clean pattern to command position](https://github.com/NousResearch/hermes-agent/pull/87975) | 修复危险命令检测器将引号内的 `git clean -f` 文本误判为危险命令的安全/误报问题 |
| [#87976 fix(gateway): scope /reasoning and /fast to routed profile](https://github.com/NousResearch/hermes-agent/pull/87976) | 多 profile 路由下 `/reasoning` 和 `/fast` 读写错误配置的问题 |
| [#87978 fix(desktop): prefer live context usage during turns](https://github.com/NousResearch/hermes-agent/pull/87978) | 桌面端 context 使用量仪表盘在响应流式传输期间显示过期估算值的问题 |
| [#87974 fix(tools): scope resolved names to active turn](https://github.com/NousResearch/hermes-agent/pull/87974) | 将工具名解析结果从进程级全局状态改为按轮次隔离的 ContextVar |
| [#87977 feat(desktop): expose connection-aware plugin routing](https://github.com/NousResearch/hermes-agent/pull/87977) | 桌面插件可枚举并路由到所有已注册连接上的 profile |
| [#87969 fix(tools): surface plugin-registered STT providers](https://github.com/NousResearch/hermes-agent/pull/87969) | 能力选择器遗漏插件注册的 STT provider 的后端修复 |
| [#87968 fix(gateway): don't feed bare media filename to model](https://github.com/NousResearch/hermes-agent/pull/87968) | Matrix 平台音频/文件消息无 caption 时，将裸文件名作为消息文本喂给模型的问题 |
| [#87967 feat(cron): media-send timeout configurable](https://github.com/NousResearch/hermes-agent/pull/87967) | cron 媒体投递 30 秒硬编码超时改为 `HERMES_CRON_MEDIA_SEND_TIMEOUT` 可配置 |
| [#87980 fix(desktop): guard whole build-critical dep set](https://github.com/NousResearch/hermes-agent/pull/87980) | 桌面构建前置依赖检查仅覆盖 vite 单一包的问题 |

### 3.3 已关闭的较重要 Issue（对应修复已合入）

- [#83683](https://github.com/NousResearch/hermes-agent/issues/83683)（P1，Windows 桌面重启后 gateway 不重启的回归）— 已关闭
- [#82001](https://github.com/NousResearch/hermes-agent/issues/82001)（P1，agent flush 不采纳压缩后 continuation 的会话状态 bug）— 已关闭
- [#68563](https://github.com/NousResearch/hermes-agent/issues/68563)（Gateway durable session 不刷新 SOUL.md 变更后的 system prompt）— 已关闭
- [#50530](https://github.com/NousResearch/hermes-agent/issues/50530)（google-antigravity 遗留 P2 集成问题汇总）— 已关闭

> 综合来看，项目在持续推进“**代码结构现代化**”和“**多 profile/多租户安全隔离**”两条主线；新提交的 PR 也呈现出对**审批安全**、**会话状态正确性**、**配置隔离**的高度关注。


## 4. 社区热点

| 排名 | Issue/PR | 评论数 | 状态 | 核心诉求 |
|---|---|---|---|---|
| 1 | [#78647 Large-file decomposition: 20/20 done](https://github.com/NousResearch/hermes-agent/issues/78647) | 79 | CLOSED | 仓库级 god-file 分片 epic 完结，讨论热度高说明社区对代码可维护性的关注 |
| 2 | [#66616 Skills index is stale or degraded](https://github.com/NousResearch/hermes-agent/issues/66616) | 44 | OPEN | 自动化新鲜度探测失败，`skills-index.json` 已 29.8h 未更新（上限 26h），影响文档站技能中心 |
| 3 | [#6839 Lazy Tool Schema Loading — Two-Pass Tool Injection](https://github.com/NousResearch/hermes-agent/issues/6839) | 40 | OPEN | 每次 API 调用注入全部工具 schema（约 3,500–5,000 tokens），本地模型上开销显著；获 18 👍 |
| 4 | [#34352 Solving the Multi-Tenant Hermes Problem](https://github.com/NousResearch/hermes-agent/issues/34352) | 34 | OPEN | Memory 操作绕过 hook 系统，多租户隔离无法在不 fork 核心的前提下实现；用户已自维护生产修复数月 |
| 5 | [#83683 Desktop restart reaps live gateway but never relaunches](https://github.com/NousResearch/hermes-agent/issues/83683) | 33 | CLOSED | Windows 桌面端重启后微信/QQ/Telegram 网关静默；P1 回归，已修复 |

**简要分析**：

- 围绕 **#6839**（工具 schema 注入开销）与 **#34352**（多租户隔离）的讨论反映出用户对**本地模型成本**和**多租户架构支撑**的强烈诉求——这两者可能共同指向路线图中的“**更轻量、更隔离**”方向。
- **#66616** 是机器人自动上报的基础设施问题，虽不直接影响用户但持续近一个月未闭环（详见“待处理积压”）。
- 已关闭的 **#78647** 有 79 条评论，说明社区对这次大型重构高度关注。


## 5. Bug 与稳定性

按严重程度排列，并标注 fix 状态。

### P1（严重）

| Issue | 描述 | 状态 |
|---|---|---|
| [#83683](https://github.com/NousResearch/hermes-agent/issues/83683) | Windows 桌面端重启后 gateway 被强杀且不重启，微信/QQ/Telegram 全部静默（回归） | ✅ 已关闭（修复完成） |
| [#82001](https://github.com/NousResearch/hermes-agent/issues/82001) | 压缩触发时 agent flush 不采纳续写，用户被误导为“磁盘已满”（实际为 session 身份交接 gap） | ✅ 已关闭（修复完成） |
| [#80439](https://github.com/NousResearch/hermes-agent/issues/80439) | 桌面端自动生成的 `hermes.desktop` Exec 路径错误，KDE 任务栏固定失效 | 🔶 OPEN，未发现对应 fix PR |

### P2（重要）

| Issue | 描述 | 状态 |
|---|---|---|
| [#82936](https://github.com/NousResearch/hermes-agent/issues/82936) | multiplex_profiles 下默认 profile 的 secrets 泄漏进次要 profile 的 terminal 工具与 Kanban worker 子进程（安全边界） | 🔶 OPEN，未见专门 fix PR |
| [#81048](https://github.com/NousResearch/hermes-agent/issues/81048) | **Tier 1 安全关键**：审批超时被误标记为“用户明确拒绝” | 🔶 OPEN，未见 fix PR |
| [#83390](https://github.com/NousResearch/hermes-agent/issues/83390) | DeepSeek 上 auxiliary title_generation 失败：HTTP 400 “response_format types unavailable” | 🔶 OPEN |
| [#82887](https://github.com/NousResearch/hermes-agent/issues/82887) | terminal 工具引用二进制可执行文件时崩溃 “embedded null character in path”（`_read_script_in_env` 根因） | 🔶 OPEN |
| [#85695](https://github.com/NousResearch/hermes-agent/issues/85695) | 每次启动误报 “TERMINAL_CWD deprecated”（用户从未设置，仅注释存在） | 🔶 OPEN |
| [#32528](https://github.com

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-08-17

## 1. 今日速览

过去 24 小时项目活跃度中等偏高：Issue 侧共 3 条更新（2 条新增、1 条关闭），PR 侧共 10 条更新（9 条待合并、1 条关闭）。安全与稳定性方面，high 优先级缺陷「secret 脱敏大小写绕过」已形成完整修复闭环（Issue #4505 → PR #4508），同时新暴露 1 个 medium 级 LLM 消息缓存问题（#4511）。功能开发节奏强劲，`llm_profile` 覆盖、后台任务生命周期、仓库访问预检等 3 个新功能 PR 均在今日保持活跃。需注意两点：9/10 的 PR 仍处于待合并状态，合并吞吐偏低；无新版本发布，功能落地节奏以 PR 合入为准。

## 2. 版本发布

过去 24 小时无新版本发布，本节省略。

## 3. 项目进展

今日仅 1 个 PR 完成合并/关闭，属于安全修复闭环：

- **[#4508] fix: make dict-entry secret redaction case-insensitive** — 已关闭（2026-08-16 创建，同日关闭）
  - 修复 `redact_text_secrets` 对字典式文本中 `API_KEY`、`ApiKey` 等小写/混合大小写密钥名不生效的问题，对应 high 安全 Bug（#4505）同步关闭。
  - 链接：https://github.com/OpenHands/software-agent-sdk/pull/4508

除上述合并外，另有 9 个 PR 处于待合并状态（详见第 6 部分）。整体来看，今日项目在安全加固上取得实质进展，但大量功能与修复积压在待合并队列，合并速度是当前项目推进的主要瓶颈。

## 4. 社区热点

今日 Issue 侧各有 1 条评论，讨论热度相对平均；PR 侧评论数据未记录。值得关注的信号：

- **[#4510] feat(tools): add per-call llm_profile override to the task tool**

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目日报 — 2026-08-17

## 今日速览
过去24小时项目活跃度极高：**42条Issue更新**（34条已关闭）、**8条PR全部合并/关闭**，闭环效率出色。新开/活跃Issue仅8条，显示核心问题正被快速消化。合并的PR集中在**token计量修正、xAI模型路由（默认Grok 4.6）、Kiro OAuth登录、MiniMax文生图**等方向。值得关注的是两条涉及**自定义消息在流式输出期间破坏tool_calls顺序**的严重bug已被定位并提交修复PR（#8209），以及pi.dev目录接口超时问题获得PR修复（#8204）。整体项目健康度良好，维护者响应及时。

---

## 项目进展
今日8条PR全部合并，主要推进方向：

**核心修复**
- [#8218 fix(coding-agent): getStats tokens.total = billable only](https://github.com/earendil-works/pi/pull/8218) — 修正token统计包含缓存token导致总费用高估120倍的问题，避免压缩预算过早触发。
- [#8209 fix(coding-agent): defer non-turn custom messages to end of turn while streaming](https://github.com/earendil-works/pi/pull/8209) — 修复流式期间插入自定义消息破坏tool_calls顺序的严重bug（对应#8166、#8210）。
- [#8204 fix(coding-agent): retry hung pi.dev catalog refreshes](https://github.com/earendil-works/pi/pull/8204) — 为目录刷新增加超时重试，解决`pi update --models`挂起问题（对应#8198）。
- [#8119 fix: track kimi cached tokens](https://github.com/earendil-works/pi/pull/8119) — 正确解析Kimi的`usage.cached_tokens`，将其计入缓存读取而非普通输入（对应#8075）。

**新功能/集成**
- [#8217 feat(auth): add Kiro OAuth device login](https://github.com/earendil-works/pi/pull/8217) — 新增Kiro OAuth设备码登录，含刷新、错误处理与回归测试。
- [#8124 feat(ai): route xAI models through Responses and default to Grok 4.6](https://github.com/earendil-works/pi/pull/8124) — xAI模型默认走Responses API，默认模型从Grok 4.5升至4.6。
- [#8193 feat(ai): add image-to-image generation for MiniMax](https://github.com/earendil-works/pi/pull/8193) — MiniMax文生图新增图生图支持，补齐双区域端点。

**其他**
- [#8076 DRAFT: dev branch with new harness](https://github.com/earendil-works/pi/pull/8076) — 新harness开发分支（DRAFT，已关闭）。

---

## 社区热点
高讨论度Issue反映用户对**终端稳定性、交互体验、性能**的集中诉求：

- **[#5023 terminal scrolls to beginning without reason](https://github.com/earendil-works/pi/issues/5023)**（评论14，👍2，已关闭）— 终端随机跳转到会话开头并快速滚动到底部，在模型输出时偶发。此类问题严重影响日常使用，用户数量多、情绪反馈强烈。
- **[#7683 pi-tui: components receive mouse events on their own rows](https://github.com/earendil-works/pi/issues/7683)**（评论10，已关闭）— 希望TUI组件可选择性接收自身行区域的鼠标事件，用于自定义交互，需在滚动/选择处理前分发。
- **[#8029 Very slow performance on moving in prompt editor](https://github.com/earendil-works/pi/issues/8029)**（评论9，开放，`inprogress`）— 大文本输入时光标移动呈线性延迟，7000行时单次↑按键耗时1650ms，属严重性能缺陷。
- **[#6300 Windows: Input line redrawn on every keystroke](https://github.com/earendil-works/pi/issues/6300)**（评论7，开放）— Windows 10/11 + cmd/Windows Terminal + Node v22，每次按键输入行整体重绘且换行错乱，影响Windows用户体验。
- **[#8157 Migrate grok-mermaid -> lovely-mermaid](https://github.com/earendil-works/pi/issues/8157)**（评论5，开放）— 提议将mermaid渲染从grok-mermaid迁移至lovely-mermaid，后者解析器质量更高且获得更多维护。

---

## Bug 与稳定性

**P0 — 严重（性能/功能不可用）**
- [#8029 大文本prompt编辑器性能](https://github.com/earendil-works/pi/issues/8029)（开放，标记`inprogress`）— 7000行输入时方向键响应高达1650ms，维护者已关注。
- [#7870 远程目录覆盖GLM-5.2 contextWindow为262k（应为1M）](https://github.com/earendil-works/pi/issues/7870)（开放，`inprogress`）— 模型上下文窗口被错误缩小4倍，可能触发不必要的压缩。
- [#8061 Context budget忽略maxTokens输出预留](https://github.com/earendil-works/pi/issues/8061)（开放）— 输入仅占78%窗口时仍被provider拒绝，且自动压缩重试同样失败（👍1）。
- [#8198 pi.dev catalog接口超时](https://github.com/earendil-works/pi/issues/8198)（开放）— 多个网络均超时，curl也收不到响应；**已有PR #8204修复与#8205跟进**。

**P1 — 功能性缺陷**
- [#8166 流式中注入自定义消息破坏tool_calls顺序](https://github.com/earendil-works/pi/issues/8166)（已关闭）— 导致DeepSeek/Moonshot永久400错误；**已有PR #8209修复**，另有#8210确认。
- [#7994 reasoning_details仅支持加密条目往返](https://github.com/earendil-works/pi/issues/7994)（开放）— 非加密推理内容无法回传，影响OpenRouter多API面兼容（870次基准测试发现）。
- [#6300 Windows输入行每次按键重绘](https://github.com/earendil-works/pi/issues/6300)（开放）— 跨cmd/Windows Terminal复现，Windows平台体验受损。

**P2 — 配置/兼容性问题**
- [#8207 pnpm下pi update无法升级到最新版](https://github.com/earendil-works/pi/issues/8207)（已关闭）— pnpm与npm包管理语义差异导致。
- [#8203 llama.cpp无默认模型](https://github.com/earendil-works/pi/issues/8203)（已关闭）— 保存API key后提示无默认模型，/model无可用模型。
- [#8208 openai-responses重放历史产生孤儿reasoning条目](https://github.com/earendil-works/pi/issues/8208)（已关闭）— 长会话下请求被provider拒收。

**今日已修复（合并PR对应的Issue）**
- #8166、#8198、#8075（Kimi token统计）、#8069（GLM 5.2空命令，`no-action`）、#5823（--model provider忽略，`no-action`）。

---

## 功能请求与路线图信号
按讨论热度和PR关联性排序，以下需求可能进入下一版本：

**高可能性（已有PR或标记inprogress）**
- **RPC暴露slash命令参数补全** — [#8214](https://github.com/earendil-works/pi/issues/8214)（get_argument_completions RPC命令，与TUI内部数据同源）。
- **Extension API：让扩展可否决agent_end** — [#8213](https://github.com/earendil-works/pi/issues/8213)（可返回veto阻止settling，重定向agent）。
- **客户端重试pi.dev目录刷新** — [#8205](https://github.com/earendil-works/pi/issues/8205)（PR #8204已合并）。
- **限制subagent示例的嵌套深度** — [#8195](https://github.com/earendil-works/pi/issues/8195)（示例不传`--no-extensions`导致子代理可无限递归）。
- **对齐Qwen Token Plan模型目录** — [#8194](https://github.com/earendil-works/pi/issues/8194)（两个区域变体暴露一致的最新8模型列表）。

**中等可能性（社区有明确诉求，待维护者评估）**
- **TUI组件级鼠标事件** — [#7683](https://github.com/earendil-works/pi/issues/7683)（评论10，设计案已提出：`Component.onMouse` + LayoutBox相对坐标）。
- **mermaid渲染迁移至lovely-mermaid** — [#8157](https://github.com/earendil-works/pi/issues/8157)（替换1:1移植的grok-mermaid，改善解析器边界情况）。

**已落地（今日合并）**
- Kiro OAuth登录、xAI默认走Responses + Grok 4.6、MiniMax图生图、Kimi缓存token统计、token统计计费修正。

---

## 用户反馈摘要
从今日Issue评论提炼的真实声音：

**痛点**
- **终端行为异常**（#5023）：模型工作期间终端突然滚动，用户表示“完全随机、无任何交互发生”，体验割裂。
- **大幅文本操作性能**（#8029）：用户明确量化“7000行→单次↑ 1650ms”，认为性能不可接受。
- **Windows输入体验**（#6300）：用户指出“每个字符都出现在新行上”，基本无法正常输入，且跨终端复现。
- **provider配置陷阱**（#8069）：用户尝试Mistral托管的GLM 5.2，简单问答正常但会执行空命令，导致harness行为异常。
- **目录刷新生效性**（#8198）：用户报告“pi update --models”持续超时，curl也拿不到任何响应体，影响模型列表更新。

**安全关注**
- **#8216 pi-devin-auth 安全报告**（已关闭）：用户举报该包“仓库页为a-wall，信任其处理用户凭据似乎不安全”，引发对第三方包安全审查的讨论。

**改进建议**
- 用户普遍希望**底层数据能力开放**（#8214 RPC补全、#8213 agent_end veto），说明插件生态正从“观察”向“控制”演进。

---

## 待处理积压
以下Issue开放时间较长或关注度较高，需维护者重点关注：

- **[#5581 triggerTurn:true绕过before_agent_start事件](https://github.com/earendil-works/pi/issues/5581)** — 创建于2026-06-10，持续2个月+，今日仍在更新（4条评论，👍1）。`sendMessage()`直接调用`_runAgentPrompt`绕过事件钩子，影响扩展系统的确定性。
- **[#6300 Windows输入行重绘问题](https://github.com/earendil-works/pi/issues/6300)** — 创建于2026-07-04，今日有更新（7条评论），仍无修复PR或进展标记。Windows平台核心体验问题，建议优先排期。
- **[#5823 --model provider/model 忽略显式provider](https://github.com/earendil-works/pi/issues/5823)** — 创建于2026-06-16，今日已关闭但标记为`no-action`（未实际修复）。多provider场景下模型ID冲突时无法指定provider，属配置隐性问题，建议追踪后续的provider解析重构。

---

*数据范围：2026-08-16 至 2026-08-17 · 来源：earendil-works/pi GitHub*

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

好的，作为 LiteLLM 开源项目分析师，我根据您提供的 GitHub 数据，生成了一份 2026 年 8 月 17 日的项目动态日报。

---

### LiteLLM 项目动态日报 (2026-08-17)

#### 1. 今日速览

LiteLLM 项目今日活跃度极高，在过去 24 小时内共有 30 条 Issue 更新和 148 条 PR 更新，并发布了 2 个版本。项目核心关注点集中在 **Claude Code 相关支持（/v1/messages）**、**Bedrock 与 Vertex AI 的稳定性与成本计算**，以及 **Pass-through 与身份认证机制的精细化**。虽然 PR 待合并数量（111）较高，表明维护者与社区贡献者的协作负载较大，但高版本的迭代频率（v1.97.0 与 rc 候选版）显示了项目健康的演进速度。社区中关于 **Bug 修复、成本计费争议和 Kubernetes/Operator 集成**的讨论尤为热烈，是当前用户最主要的痛点与期待。

#### 2. 版本发布

今日发布了两个新版本，均为 Docker 镜像签名验证的配套文档更新，无重大功能性变更或已知破坏性变更。

- **v1.98.0-rc.1** / **v1.97.0**:
  - **内容**：两个版本均未附带独立的 Changelog 说明，Release 页面主体内容是关于如何验证 Docker 镜像签名（使用 cosign）。这表明版本的发布重点可能在于安全加固与供应链安全验证流程的完善。
  - **迁移注意事项**： 无。由于变更内容仅涉及镜像签名验证说明，不影响代码 API 或配置文件的向后兼容性。对于常规用户，升级风险极低；但对于有严格供应链安全要求的团队，建议立即采用新的签名验证流程。
  - **链接**: [v1.98.0-rc.1](https://github.com/BerriAI/litellm/releases/tag/v1.98.0-rc.1) | [v1.97.0](https://github.com/BerriAI/litellm/releases/tag/v1.97.0)

#### 3. 项目进展

今日无突出的大功能合并，但多个关键 Issue 被关闭，推动了项目在稳定性和兼容性方面的进展。重要进展包括：

- **Azure AI Foundry 生态扩展**：关闭了 "[Feature]: Add support for Fireworks AI models in Azure Foundry" (#26618)，意味着 LiteLLM 已支持在 Azure Foundry 中调用 Fireworks AI 的模型（如 DeepSeek V3.2等），扩大了其在 Azure 云平台上的模型覆盖范围。
- **云服务稳定性修复**：关闭了 "[Bug]: `timeout` silently ignored for Bedrock and Vertex AI streaming requests" (#23375)，修复了流式请求中 timeout 参数被忽略的问题，这是生产中常见的隐患。
- **Vertex AI 批处理验证**：解决了 "[Bug]: Vertex batch accepts vertex_location: global, then forwards a request URL that 400s" (#35134)，增强了服务的健壮性，避免了无效请求发送到上游。
- **社区与CI流程优化**：关闭了多个陈旧（stale）Issue，包括 CI 工作流引用错误分支 (#27510) 和指标重置 (#27519)，表明项目在维护自动化和流程规范上有所改进。

#### 4. 社区热点

今日讨论最热门的 Issue 揭示了用户对基础设施和核心功能的强烈关注：

- **Helm Chart 依赖源迁移** ([#19769](https://github.com/BerriAI/litellm/issues/19769))：获得 8 条评论和 5 个赞。用户**@freinold** 提议因 Bitnami 目录变更，将 Helm Chart 的 Postgres 和 Redis 依赖迁移到 Cloudpirates 等更稳定的仓库。这反映了生产用户在供应链安全和部署稳定性上的迫切需求，是云原生环境下常见的痛点。
- **Payload Tags 识别回归** ([#27460](https://github.com/BerriAI/litellm/issues/27460))：获得 7 条评论，用户报告在 v1.83.9-nightly 之后，通过 `metadata.tags` 传递的标签不再被识别。这直接关联到成本审计和用量追踪的核心功能，属于必须修复的高优回归问题，会直接影响用户对消费数据的信任。
- **Azure AI Foundry Agents v2 支持** ([#25372](https://github.com/BerriAI/litellm/issues/25372))：获得 5 条评论和 4 个赞。用户**@bachya** 提议支持新的 Responses API 和 `agent_reference`。这明确指向企业级用户对微软最新 AI 服务的采纳趋势，是重要的投资组合扩展信号。

#### 5. Bug 与稳定性

今日报告的 Bug 集中在认证、路由和计费准确性上，按严重程度排列如下：

**高严重度**
- **认证绕过/错误响应**：
  - `MCP routes return HTTP 500 instead of 401` ([#37080](https://github.com/BerriAI/litellm/issues/37080))：未授权请求返回 500 而非 401，是安全性和 API 合规性问题。目前无固定 PR。
  - `Admin-only route denials return 401 instead of 403` ([#37108](https://github.com/BerriAI/litellm/issues/37108))：同样存在 HTTP 状态码语义错误，会导致客户端重试逻辑混乱。目前无固定 PR。

**中严重度（功能回归/数据准确性）**
- **计费与令牌统计错误**：
  - `Pass-through — upstream-reported cost and tokens are discarded on non-streaming /v1/messages` ([#37105](https://github.com/BerriAI/litellm/issues/37105))：非流式请求丢弃上游上报的开销与令牌，导致成本核算失真。
  - `compression_savings_spend and prompt_caching_savings_spend always $0` ([#37117](https://github.com/BerriAI/litellm/issues/37117))：在成本路由下，节省成本指标恒为$0，影响优化效果评估。
  - `LiteLLM proxy silently returns understated token counts when Bedrock CountTokens is unsupported` ([#37102](https://github.com/BerriAI/litellm/issues/37102))：对于不支持的模型，令牌数被错误计算并静默返回，可能引发配额和费用层面的误解。
- **模型路由错误**：
  - `/v1/messages routes openai/ models with custom api_base to the Responses API` ([#37088](https://github.com/BerriAI/litellm/issues/37088))：自定义 `api_base` 的 OpenAI 模型被错误路由到不支持的 Responses API，功能失效。
  - `Bedrock rerank broken after upgrading from v1.83.14 to v1.85` ([#28561](https://github.com/BerriAI/litellm/issues/28561))：升级后，Bedrock Rerank 接口映射失败，是明显的回归问题。

**低严重度/体验问题**
- **日志与显示**：
  - `help` ([#37121](https://github.com/BerriAI/litellm/issues/37121))：控制台打印字面量 `%s://%s://%s:%d` 而非真实 URL。**已存在修复 PR** ([#37122](https://github.com/BerriAI/litellm/pull/37122))。
  - `guard-main-branch.yml references non-existent litellm_oss_branch` ([#27510](https://github.com/BerriAI/litellm/issues/27510))：CI 指导信息指向无效分支，已关闭。

#### 6. 功能请求与路线图信号

今天的功能请求清晰地指向了 **实时交互**、**新生态集成** 和 **治理能力** 三个方向：

- **实时/流式能力**：
  - `feat(elevenlabs): add WebSocket streaming-input TTS endpoint` ([PR #37084](https://github.com/BerriAI/litellm/pull/37084))：为 ElevenLabs 增加流式 TTS，减少延迟。这是一个完整的 PR，优先度很高。
  - `fix(proxy): register WebSocket passthrough for OpenAI prefixes` ([PR #36151](https://github.com/BerriAI/litellm/pull/36151))：修复 OpenAI 前缀下的 WebSocket 停止转发问题，对接 realtime API。
- **新提供商集成**：
  - `feat(opencode): add opencode_go and opencode_zen first-class providers` ([PR #37103](https://github.com/BerriAI/litellm/pull/37103))：将 OpenCode 作为头等提供商加入。
  - `feat: add Levo AI Gateway guardrail integration` ([PR #37113](https://github.com/BerriAI/litellm/pull/37113))：新增 LLM 网关防护栏集成。
  - `Add native OpenAI and Azure OpenAI Skills provider routing` ([Issue #37074](https://github.com/BerriAI/litellm/issues/37074))：请求支持 Skills API 路由，企业级功能。
- **计费与配置增强**：
  - `feat: email alerts for cost savings report` ([Issue #37076](https://github.com/BerriAI/litellm/issues/37076))：用户希望定期接收成本节约报告邮件，这是从工具到服务的关键一步。
  - `Support model group composition ("group of groups")` ([Issue #28125](https://github.com/BerriAI/litellm/issues/28125))：允许模型组嵌套，提升配置灵活性和可维护性。
  - `Let a pass-through target report which model actually served` ([Issue #37107](https://github.com/BerriAI/litellm/issues/37107))：增强可观测性，让上游能够报告实际服务模型。

这些 PR 和 Issue 表明，项目下一阶段的路线图很可能围绕**实时交互体验（WebSocket）**、**扩展AI生态（OpenCode, Azure Skills）** 以及**计费与可观测性深化**展开。

#### 7. 用户反馈摘要

- **对成本与计费准确性的高度不满**：多个 Issue（如 #37105, #37117, #28561）表明用户对代理上报的令牌数和成本非常敏感，任何静默丢弃或计算错误都会引发严重信任危机。用户期望 LiteLLM 能如实反映上游报告的数据。
- **对 Kubernetes/GitOps 集成的强烈渴望**：Issue #19769 和 #18428（K8s Operator）获得了高赞和讨论，体现了生产用户希望将 LiteLLM 无缝融入其基础设施交付流程的强烈需求。
- **对配置灵活性的要求**：Issue #28125 (模型组嵌套) 和 #26420 (user.models限制) 指出，当前模型定义和权限控制模型不够灵活，无法满足复杂的组织级应用场景。
- **对 Claude Code / Anthropic 接口兼容性的关注**：多个 Issue（如 #37118 丢弃 stop_sequences、#37088 路由错误）专门针对 `/v1/messages` 端点，表明 LlamaIndex/Claude Code 用户群体的活跃度在增加，他们是当前生态中非常挑剔的使用者。

#### 8. 待处理积压

以下 Issue/PR 长期未获响应，建议核心维护者关注：

- **长期开放的 Issue**:
  - `[Feature]: LiteLLM Operator for deeper integration with Kubernetes and GitOps` ([#18428](https://github.com/BerriAI/litellm/issues/18428))：创建于 2025-12-25，获得 5 个赞。这是一个被广泛期待的企业级功能，长期未获官方排期。
  - `Helm Chart: Switch to other repo provider` ([#19769](https://github.com/BerriAI/litellm/issues/19769))：创建于 2026-01-26，仍开放，但标题已标记为 `[stale]`，需要维护者评估是否接受该建议。
  - `GET /v1/models ignores user.models restriction` ([#26420](https://github.com/BerriAI/litellm/issues/26420))：权限控制漏洞，开放近 4 个月，有安全影响，值得优先处理。
- **待合并的 PR**:
  - `fix(pricing): add the azure gpt-realtime-2 family` ([#31565](https://github.com/BerriAI/litellm/pull/31565))：创建于 2026-06-28，已开放一个多月。这是计费准确的必要补充，长时间未合并不禁让人对维护者处理计费相关 PR 的优先级产生疑虑。
  - `fix: count anthropic image content blocks in token_counter instead of raising` ([#33861](https://github.com/BerriAI/litellm/pull/33861)) 与 `fix: duplicate message_start in anthropic responses stream wrapper` ([#33859](https://github.com/BerriAI/litellm/pull/33859))：均由 **@streber42** 提交，创建于 2026-07-18，针对 Anthropic 接口的修复，接近一个月未合并，需要确认是否因测试或设计问题阻塞。

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-17

## 1. 今日速览

过去24小时Temporal项目整体保持常规维护节奏。Issue侧活跃度较低（仅1条新开），但PR侧有5条更新，其中含1条release分支准备和2条自动测试分片调优，说明CI与发布基础设施在持续运转。核心关注点集中在两个方向：一是针对PostgreSQL visibility schema升级流程的新报告bug（#11594），二是针对1.31.0的可靠性与性能修复PR（#11578）仍在推进中。项目整体处于“发布周期启动+常规维护”并行的状态，无明显风险事件。

## 2. 版本发布

过去24小时无新版本发布。

值得留意的是，PR #11593（1.32.0 Prepare release branch）已于昨日关闭，意味着1.32.0版本分支已经就绪，正式进入开发/发布准备周期。预计未来数日至数周内可能出现1.32.0的alpha/beta版本。

## 3. 项目进展

今日合并/关闭的PR共2条，均为自动化流程类操作：

- **[CLOSED] 1.32.0: Prepare release branch（#11593）** — 由temporal-cicd机器人创建并关闭，完成release分支的治理文件覆盖与依赖更新。这标志着1.32.0代码线正式建立，后续feature PR将逐步合入该分支。
  https://github.com/temporalio/temporal/pull/11593

- **[CLOSED] Update test shard salt（#11590）** — 自动优化测试分片均衡度的例行PR，反映CI测试分片系统在持续自动调优，间接说明测试集规模较大且维护者未忽视测试基础设施健康度。
  https://github.com/temporalio/temporal/pull/11590

另有1条值得关注的进行中PR：

- **[OPEN] 修复execution last running clock（#11578）** — 针对1.31.0的reliability修复，解决ID复用场景下新execution成为current时LastRunningClock未被正确更新的问题。该问题可能导致时间相关的追踪状态不准确，修复后能改善执行语义的一致性。目前该PR仍在review阶段。
  https://github.com/temporalio/temporal/pull/11578

整体来看，项目进入1.32.0开发周期，可靠性修复仍在推进，自动化管线运行良好，但功能性用户贡献今日并不多。

## 4. 社区热点

过去24小时内所有Issue和PR的评论数均为0（除PR页面显示undefined外），未出现高讨论热度的线程。

在有限的数据中，最值得关注的是新Issue **#11594**（PostgreSQL visibility v1.14 schema升级未应用优化），虽然尚无评论或表情回应，但它针对的是一个具体的性能回归场景（从1.29升级到1.31时的schema重写成本），这类问题通常能引发用户共鸣，预计后续会有较多讨论。

https://github.com/temporalio/temporal/issues/11594

## 5. Bug 与稳定性

今日报告1条新Bug，无崩溃或严重回归事件。

**中优先级 — PostgreSQL visibility schema升级性能退化**

- **Issue #11594 [OPEN]**：PR #10371优化了PostgreSQL visibility schema从v1.10–v1.13的升级重写逻辑，但v1.14的迁移未包含在该优化中，仍使用旧的重写模式。这导致从1.29升级到1.31的用户在进行组合schema重写（comb rewrite）时会产生不必要的额外开销。该问题影响PostgreSQL用户的升级体验与迁移耗时，但目前尚无对应的fix PR链接。
  https://github.com/temporalio/temporal/issues/11594

**低优先级 — Execution LastRunningClock 语义问题**

- 对应修复PR **#11578** 仍在推进。场景是ID重用且新execution成为current时，LastRunningClock未被更新。虽然该问题被标记在reliability分支上，但其影响范围相对有限（涉及时间相关状态追踪），不构成紧急崩溃风险。
  https://github.com/temporalio/temporal/pull/11578

## 6. 功能请求与路线图信号

今日无新的功能请求Issue。

路线图信号方面存在两个值得关注的点：

1. **#11594暗示PostgreSQL migrations的持续优化方向**：Issue指出优化未覆盖v1.14 schema升级。这提示维护团队在升级流程优化上需保持一致性，修复方案很可能是在v1.14迁移中应用与v1.10–v1.13相同的优化模式。该问题大概率会进入1.32.0或后续patch版本的修复清单。

2. **#9980 HostHealthAggregator（陈旧WIP PR）**：这是一个自2026年4月17日起的WIP PR，旨在聚合Temporal各组件的健康状态并通过DeepHealthCheck对外输出，为健康管理系统的精细化决策提供数据。从时间跨度看，说明维护团队内部对系统级健康监控能力的探索已持续数月，该功能有概率出现在未来版本路线图中，但目前仍处于早期阶段。
   https://github.com/temporalio/temporal/pull/9980

## 7. 用户反馈摘要

今日唯一的Issue即来自用户反馈，可提炼如下：

- **用户痛点的具体场景**：使用PostgreSQL visibility的用户在从Temporal 1.29升级到1.31时，schema升级需要执行两次rewrite操作（一次针对组合schema，一次针对v1.14），而其中的部分rewrite本可通过已有优化避免。对于拥有大量历史数据的生产环境，这种重复rewrite意味着更长的升级停机窗口和潜在的操作风险。

- **用户对优化一致性的期待**：报告者在描述问题时明确对比了“优化已覆盖的版本”与“未覆盖的版本”，说明Temporal用户对升级路径的平滑度有较高期待，并希望官方在性能优化上保持版本间的连贯性。这也间接反映了社区对Temporal升级体验的重视程度。

## 8. 待处理积压

- **PR #9980 [OPEN] — [stale] WIP: Add HostHealthAggregator**：自2026年4月17日创建至今已4个月，已标记为stale。该PR涉及深度健康检查（DeepHealthCheck）能力的扩展，虽为WIP状态，但对理解项目长期监控能力规划有参考价值。建议维护者明确该PR的保留/关闭意图，或补充阶段性进展。
  https://github.com/temporalio/temporal/pull/9980

- **Issue #11594 [OPEN]**（新开，暂无评论）：虽然不属于长期积压，但考虑到升级性能问题对用户的影响，建议维护者尽快确认是否接受为优化项，避免进入长期无响应状态。
  https://github.com/temporalio/temporal/issues/11594

---

**项目健康度评估**：综合来看，Temporal项目在发布准备、CI自动化维护、可靠性修复三条线路上均有常规动作落地；新Bug报告响应窗口尚可（今日新开，等待维护者确认）；社区讨论热度偏低但无负面情绪累积。整体属于稳健、健康的维护状态。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*