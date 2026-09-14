# OpenClaw 生态日报 2026-09-15

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-14 22:36 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 · 2026-09-15

---

## 1. 今日速览

OpenClaw 今日维持**极高活跃度**：过去 24 小时 Issues 更新 500 条（新开/活跃 309、关闭 191），PR 更新 500 条（待合并 293、已合并/关闭 207），但**无新版本发布**。社区讨论集中在**更新/升级可靠性**（多条 P0/P1）、**会话状态与消息丢失**以及**Gateway 事件循环阻塞/崩溃循环**三大主题。维护者 @steipete 主导了大量性能与 SQLite worker 迁移类 PR，其中多项标注为 stacked/待前序合入，说明进行中的架构性重构规模较大。整体健康度：**讨论与修复吞吐强劲，但待合并 PR 积压至 293 条，且多条 P0 级更新故障仍未闭环，稳定性压力偏高**。

---

## 2. 版本发布

无新版本发布（0 个）。最新 Releases 列表为空，当前可观测的最新版本仍为 **2026.9.4**（见 Issue #144809、#145510 中提及）。

---

## 3. 项目进展

今日共 **207 条 PR 已合并/关闭**、**191 条 Issues 关闭**。从可见样本看，推进方向主要分为三类：

**架构性能重构（维护者主导）**
- [#148442 [CLOSED] refactor: replace duplicated filesystem helpers with fs-safe](https://github.com/openclaw/openclaw/pull/148442) — 已关闭，采用 `fs-safe 0.11.0` 消除重复文件系统代码，保留路径策略与恢复行为。
- [#148560 refactor(skills): move library resource metadata reads off the Gateway thread](https://github.com/openclaw/openclaw/pull/148560) — 将技能库元数据读取移出 Gateway 主线程。
- [#148574 refactor(tasks): prepare cold task and flow reads asynchronously](https://github.com/openclaw/openclaw/pull/148574)、[#148576 refactor(tasks): load fresh owner projections asynchronously](https://github.com/openclaw/openclaw/pull/148576) — 将冷任务/流程读取异步化，与 #144592 关联。
- [#146557 feat: offload data-only keyed plugin state operations](https://github.com/openclaw/openclaw/pull/146557) — 将 10 类纯数据键控操作下移到共享状态 worker，保留值/错误/过期/容量/顺序语义。
- [#147971 perf: compile measured nested tool validation](https://github.com/openclaw/openclaw/pull/147971) — 仅对嵌套工具活动校验做按需编译，避免全量 schema 编译的首用开销。

**关键修复**
- [#148256 [P0] fix(ui): recover repository sessions without workers](https://github.com/openclaw/openclaw/pull/148256) — 修复 Control UI 中仓库会话在 worker 缺失/本地不可用时无法继续的问题，关闭 #147495。
- [#146913 [P1] fix(gateway): isolate deferred config reload context](https://github.com/openclaw/openclaw/pull/146913) — 隔离延迟配置重载的异步上下文，避免继承请求的 turn-scoped 状态，关联 #118839。
- [#147661 [P1] fix: restore context reads for the installed official Teams plugin](https://github.com/openclaw/openclaw/pull/147661) — 恢复官方 Teams 插件上下文读取，基于已合入的 #143341 前置。
- [#148214 [P2] fix(worker): restore shell analysis in node sessions](https://github.com/openclaw/openclaw/pull/148214) — 修复配对节点会话中 WASM 缺失导致 shell 分析不完整。
- [#146503 [P2] fix(codex): heartbeat response tool unavailable during scheduled checks](https://github.com/openclaw/openclaw/pull/146503) — 修复 Codex 定时心跳无法调用 `heartbeat_respond`。
- [#148537 [P2] fix(ui): preserve client attribution in unloaded replies](https://github.com/openclaw/openclaw/pull/148537) — 保留历史回复中 `via CLI` / `via RPC` 来源标签。

**整体推进评估**：项目正处于一次**横向的 Gateway 阻塞消除 + SQLite worker 化重构**周期中，大量 PR 以 stacked 方式推进，单日合并/关闭 207 条显示合并管线通畅；但重构类 PR 多为 XL/L 尺寸且相互依赖，短期仍会占用维护者审查带宽。

---

## 4. 社区热点

今日评论最活跃的讨论：

| 排名 | 条目 | 评论 | 状态 | 链接 |
|---|---|---|---|---|
| 1 | Text between tool calls leaks to messaging channels（P1，安全/会话状态） | 40 | OPEN | [#25592](https://github.com/openclaw/openclaw/issues/25592) |
| 2 | OpenClaw leaks unreaped hook/tool child processes → zombie 累积、运行时退化（P1，崩溃循环） | 31 | OPEN | [#97616](https://github.com/openclaw/openclaw/issues/97616) |
| 3 | 2026.5.27 Codex app-server 轮次完成停滞回归（P1） | 22 | CLOSED | [#88312](https://github.com/openclaw/openclaw/issues/88312) |
| 4 | 同步 agent 持久化与 transcript 维护阻塞 Gateway 事件循环（P1） | 20 | OPEN | [#119720](https://github.com/openclaw/openclaw/issues/119720) |
| 5 | 集中化文件名编码工具（多编码 Content-Disposition，P3） | 20 | OPEN | [#48788](https://github.com/openclaw/openclaw/issues/48788) |
| 6 | 嵌入式 prompt 缓存跨 room-event/policy/Responses 边界失效（P2，安全） | 19 | OPEN | [#102175](https://github.com/openclaw/openclaw/issues/102175) |
| 7 | MCP server init 超时崩溃 Gateway（未处理 rejection，P1） | 16 | OPEN | [#144911](https://github.com/openclaw/openclaw/issues/144911) |
| 8 | 更新至 2026.7.1 后 Gateway 无法启动（P0） | 15 | CLOSED | [#108435](https://github.com/openclaw/openclaw/issues/108435) |

**背后诉求分析**：
- **#25592 与 #102175、#77292、#77121** 共同指向**隔离与安全性**——工具调用中间文本泄漏到 Slack/iMessage、子/父 agent 投递上下文跨用户泄漏、prompt 缓存跨授权边界失效。用户对“内部处理输出不应可见”和“多租户/多用户边界不应穿透”的要求非常强烈。
- **#97616、#119720、#76038、#77584** 等构成**运行时韧性**主线：僵尸进程、事件循环阻塞、会话卡死恢复失效，属于长稳运行场景下的系统性问题。
- **#88312、#108435 已关闭**，说明历史回归在持续清理，但**更新/升级路径**今日又有新的 P0 报告（见下节），是当前最热的未解痛点。

---

## 5. Bug 与稳定性

按严重程度排列（标注是否已有 fix PR / linked PR）：

### P0 — 更新/启动/崩溃
| Issue | 摘要 | 状态 | Fix PR |
|---|---|---|---|
| [#146860](https://github.com/openclaw/openclaw/issues/146860) | Windows：Scheduled Task 使用 `LogonType: InteractiveToken` 时托管更新交接无法取得进程启动标识，卡在 `activating` 后 `abandoned` | OPEN | 未见 |
| [#145510](https://github.com/openclaw/openclaw/issues/145510) | 2026.9.3 → 2026.9.4 更新 `runtime-verification-failed`（win32/x64） | OPEN | 未见 |
| [#145252](https://github.com/openclaw/openclaw/issues/145252) | [Tracking] 2026.9.3 / 2026.9.4 更新、升级与恢复可靠性 | OPEN | 协调索引 |
| [#108435](https://github.com/openclaw/openclaw/issues/108435) | 更新至 2026.7.1 后 Gateway 无法启动（systemd/ollama/manual 均失败） | CLOSED | 已关闭 |
| [#123326](https://github.com/openclaw/openclaw/issues/123326) | 显式多 agent Codex 迁移导致 Gateway 启动 crash-loop | OPEN | `linked-pr-open` |

### P1 — 崩溃/消息丢失/会话状态
| Issue | 摘要 | 状态 | Fix PR |
|---|---|---|---|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | 工具调用之间的文本泄漏到消息渠道（impact: security） | OPEN | `linked-pr-open`，待产品决策 |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | hook/tool 子进程未回收，僵尸累积、运行时退化 | OPEN | 未见 |
| [#119720](https://github.com/openclaw/openclaw/issues/119720) | 同步持久化与 transcript 维护阻塞 Gateway 事件循环 | OPEN | 部分修复已落地（#140231、#138984） |
| [#144911](https://github.com/openclaw/openclaw/issues/144911) | stdio MCP server init 30s 超时 → 未处理 rejection 拖垮整个 Gateway | OPEN | `queueable-fix`，fix-shape-clear |
| [#125570](https://github.com/openclaw/openclaw/issues/125570) | Skill Workshop update 覆盖 live skill `description`，静默破坏技能路由（data-loss） | OPEN | `no-new-fix-pr` |
| [#145152](https://github.com/openclaw/openclaw/issues/145152) | 卡住会话恢复把 force-clear 报为 abort，无 run/owner 标识 | OPEN | `queueable-fix` |
| [#144809](https://github.com/openclaw/openclaw/issues/144809) | claude-cli：超过 `RUN_STALE_TAKEOVER_MS` 的 turn 丢失整个回复（`no active tool authority snapshot`） | OPEN | `no-new-fix-pr`，需信息 |
| [#125764](https://github.com/openclaw/openclaw/issues/125764) | Telegram 出站网络失败仅一次尝试即 dead-letter，announce/完成回复静默丢失 | OPEN | `no-new-fix-pr` |
| [#142336](https://github.com/openclaw/openclaw/issues/142336) | 2026.9.2+ 核心 `/dashboard` 与 Telegram Mini App 启动器冲突 | OPEN | `linked-pr-open` |
| [#134993](https://github.com/openclaw/openclaw/issues/134993) | 2026.8.1 升级后 Gateway 单核满载（文件系统发现忙循环） | OPEN | `needs-info` |

### P2 — 行为/回归
- [#102175](https://github.com/openclaw/openclaw/issues/102175) 嵌入式 prompt 缓存跨边界失效，需产品决策与安全审查。
- [#139710](https://github.com/openclaw/openclaw/issues/139710) 轮次中途插件生成取代同时杀死

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报
**日期：2026-09-15** | 数据来源：github.com/NousResearch/hermes-agent

---

## 一、今日速览

过去 24 小时项目维持**极高活跃度**：Issues 与 PR 各更新 500 条，其中 PR 端待合并量高达 429 条，显示维护者积压压力显著。v2026.9.14（v0.21.3）补丁版正式发布，将自 v0.21.2 以来约 **338 个 PR** 打包为稳定标签，供 Docker / Hermes Cloud / 托管部署消费。今日最显著的健康信号是 **state.db WAL 损坏问题群出现收敛**——多个 P0/P1 相关 Issue（#109687、#109728、#109727、#103339）于今日关闭，但仍有一批同类 P1 问题（#100896、#71335、#107402）悬而未决。社区侧，Intel Mac 构建请求系列（#42199/#40456/#42928）全部关闭，标志着桌面端 arm64-only 争议告一段落。

**健康度评估：活跃度极高，稳定性处于"收敛中"状态，但 PR 积压（429 待合并）与 WAL/多写入者风险类别仍是主要隐患。**

---

## 二、版本发布

### v2026.9.14 — Hermes Agent v0.21.3（补丁版）

- **发布日期：** 2026 年 9 月 14 日
- **性质：** 补丁发布（Patch Release）
- **核心内容：** 将自 v0.21.2 以来合并的 **约 338 个 PR** 汇总为一个稳定的、可供下游消费者使用的标记版本，面向 Docker 镜像、Hermes Cloud 及托管部署。
- **关键修复：** 远程网关（remote-gateway）登录修复是本次打包发布的直接动因；Release 说明明确表示该标签"存在是为了"让这些修复能够被下游稳定获取。
- **破坏性变更：** 未在提供的数据中提及。
- **迁移注意事项：** 作为补丁版承接 338 个 PR，建议下游（Docker/Cloud/托管）消费者从 v0.21.2 升级前，先阅读中间合并 PR 的 release notes 以确认行为变化；建议先在 staging 环境验证网关登录流程。

🔗 链接：https://github.com/NousResearch/hermes-agent/releases

> ⚠️ 数据中该 Release 说明被截断，完整破坏性变更清单需查阅 GitHub Release 原文。

---

## 三、项目进展

今日未见已合并 PR 明细列表（500 条 PR 中 71 条已合并/关闭），但从**已关闭 Issue** 与**待合并修复 PR** 可清晰看到几条重要推进线：

### 1. state.db / WAL 多写入者损坏治理（最大进展）
今日多个高严重度 Issue 关闭，说明治理链条正在收敛：
- [#109687](https://github.com/NousResearch/hermes-agent/issues/109687) **[CLOSED] [P0]**：单一普通 CLI 调用使网关 state.db WAL 代际成孤儿，网关静默丢弃会话写入。
- [#109728](https://github.com/NousResearch/hermes-agent/issues/109728) **[CLOSED] [P0]**：#109509 权限加固丢掉 SQLite 锁，导致 WAL 代际被删与会话中断。
- [#109727](https://github.com/NousResearch/hermes-agent/issues/109727) **[CLOSED] [P1]**：第二个 Hermes 进程 unlink 活跃的 state.db-wal/-shm。
- [#103339](https://github.com/NousResearch/hermes-agent/issues/103339) **[CLOSED] [P1]**：`doctor --fix` / `repair_state_db_schema` 等第二写入者损坏活跃 WAL，提议 lazy flock 单写入者门禁。

→ 该批关闭与 v0.21.3 打包修复呼应，是本周期**稳定性推进的核心胜利**。

### 2. Intel Mac 桌面支持争议终结
- [#42199](https://github.com/NousResearch/hermes-agent/issues/42199) [CLOSED]、[#40456](https://github.com/NousResearch/hermes-agent/issues/40456) [CLOSED]、[#42928](https://github.com/NousResearch/hermes-agent/issues/42928) [CLOSED] 全部关闭，桌面 DMG arm64-only 问题完成闭环。

### 3. 安全扫描器误报治理（PR 侧推进）
- [#111255](https://github.com/NousResearch/hermes-agent/pull/111255)：内容扫描器不再拦截对 `~/.ssh` 的只读提及，写入仍拦截（salvage #89249）。
- [#111257](https://github.com/NousResearch/hermes-agent/pull/111257)：技能/插件扫描器不再把 `self.profile` 属性访问误判为 shell-rc 编辑。
- [#111265](https://github.com/NousResearch/hermes-agent/pull/111265)：技能扫描器不再因"命名了它拒绝读取的密钥"而隔离技能（#92478 / salvage #92632）。
- [#85124](https://github.com/NousResearch/hermes-agent/pull/85124)：停止过度拒绝安全的插件脱敏模式。

→ 一线维护者 @teknium1 亲自 salvage 多个社区 PR，说明**减少误报、改善安全与可用性平衡**是当前明确方向。

### 4. 网关消息投递与中继修复
- [#111263](https://github.com/NousResearch/hermes-agent/pull/111263)：修复实时投递意图被清扫、owner settled 后被丢弃（Closes #111261）。
- [#111264](https://github.com/NousResearch/hermes-agent/pull/111264)：修复对端数<2 时 relay roster 未清理残留网关（Closes #111262）。
- [#111266](https://github.com/NousResearch/hermes-agent/pull/111266)：处理媒体 SendResult 返回失败但未抛异常的情况。
- [#99941](https://github.com/NousResearch/hermes-agent/pull/99941)：阻止进程通知产生重复回复。

**整体推进度：** 稳定性和安全边界治理显著前进；网关消息投递一致性有系统性修复；桌面 UI 与 i18n 属于并行推进线。

---

## 四、社区热点

按讨论热度排序：

| 排名 | 议题 | 状态 | 评论 | 诉求分析 |
|---|---|---|---|---|
| 1 | [#88584](https://github.com/NousResearch/hermes-agent/issues/88584) 自动化 Nous 集成被阻断 | OPEN [P3] | **100** | 评论数远超其他议题（是第二名的 3.5 倍），但标签为 `invalid`+`P3`。`cron/jobs.py` 合并冲突导致 Nous→Enterkey 定时同步失败，dashboard updater 停留在旧 Enterkey 版本。诉求背后是**跨组织自动化流水线的可靠性**。 |
| 2 | [#97681](https://github.com/NousResearch/hermes-agent/issues/97681) 桌面关闭后 Bot 群聊应继续工作 | OPEN [P2] | 28 | 跨网关 Bot 在 Desktop 关闭后仍应能协作、被另一设备接管。涉及 `risk-session-state` + `risk-message-delivery` 双重风险标签，是**"无头/多设备持续运行"**的核心诉求。 |
| 3 | [#107402](https://github.com/NousResearch/hermes-agent/issues/107402) `hermes update` 留下永久警告 | OPEN [P1] | 18 | `hermes update` 在网关自身进程树内调用时，重启被延迟但验证立即执行，留下 `fleet_restart` 永久 stale 警告。**升级体验与状态一致性**痛点。 |
| 4 | [#58576](https://github.com/NousResearch/hermes-agent/issues/58576) web_server 事件循环卡顿最长 51s | OPEN [P1] | 14 | GIL 压力下桌面 UI 冻结近一分钟。**性能与响应性**经典问题。 |
| 5 | [#38007](https://github.com/NousResearch/hermes-agent/issues/38007) 系统托盘后台运行支持 | OPEN [P2] | 11 / **👍19** | 点赞数全场最高。Windows/Linux 关闭窗口即退出，冷启动慢。**桌面常驻体验**是社区强需求。 |
| 6 | [#110591](https://github.com/NousResearch/hermes-agent/issues/110591) Discord 表格/状态字段 Markdown 渲染 | OPEN [P3] | 13 | 新开即高讨论，Discord 不渲染 GFM 表格，现有转换为 bullet 丢失列对齐。**平台原生体验**诉求。 |

**背后共性诉求：** ① 多设备/无头持续可用性；② 升级与状态一致性；③ 桌面端性能与常驻体验；④ 平台原生渲染质量。

---

## 五、Bug 与稳定性

按严重程度排列（标注是否有 fix PR）：

### 🔴 P0 — 严重
| Issue | 描述 | 状态 | Fix |
|---|---|---|---|
| [#109687](https://github.com/NousResearch/hermes-agent/issues/109687) | CLI 调用使网关 state.db WAL 成孤儿，网关静默丢会话写入 | **已关闭** | v0.21.3 打包修复 |
| [#109728](https://github.com/NousResearch/hermes-agent/issues/109728) | #109509 权限加固丢 SQLite 锁，导致已删 WAL 代际与会话中断 | **已关闭** | 已修复 |

### 🟠 P1 — 高
| Issue | 描述

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目日报 — 2026-09-15

---

## 1. 今日速览

- 项目保持**极高活跃度**：过去 24 小时共 80 条协作更新（Issues 30 条、PR 50 条），其中新开/活跃 Issue 26 条，处于近期高位。
- **PR 吞吐存在结构性压力**：44 条 PR 待合并，仅 6 条合并/关闭，待审队列持续累积，review 带宽可能成为瓶颈。
- **安全与密钥治理成为主线**：Agent Profile 的 secret 作用域（#5030、#5014）、LookupSecret 死锁（#5025）、私下安全披露渠道请求（#5034）同日集中出现。
- **高优先级稳定性问题未清**：ChatGPT 订阅 LLM 调用挂起（#4997）与 LookupSecret 事件循环死锁（#5025）均标 `priority:high` 且 `ready-for-dev`，但尚未见对应 fix PR。
- 无新版本发布，今日关闭 4 条 Issue，其中 #4818（MCP OAuth 授权失败）为高优先级修复闭环。

---

## 2. 版本发布

无新版本发布，本节省略。

---

## 3. 项目进展

> 注：本次数据仅提供「6 条 PR 已合并/

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 · 2026-09-15

> 数据窗口：2026-09-14（过去 24 小时）｜来源：github.com/earendil-works/pi
> 说明：PR 数据未提供评论数，社区热度以 Issues 评论数、👍 数为主要依据。

---

## 1. 今日速览

Pi 今日处于**高吞吐维护状态**：Issues 更新 73 条，关闭 54 条（关闭率 74%），清理力度显著，新开/活跃仅 19 条，积压未失控。PR 侧则呈"漏斗收窄"形态——31 条更新中 22 条待合并、仅 9 条合并/关闭（29%），**评审带宽已成为主要瓶颈**。讨论焦点高度集中在 provider 适配层与成本计费准确性：Bedrock/Anthropic 缓存计费、`PI_OFFLINE` 语义、Grok 错误归类三组问题占据评论榜前列。架构层面，@mitsuhiko 的 PR #9548（会话中途系统消息）与 PR #6534（developer role）提示项目正在向"可审计的 transcript"方向演进，但仍处于 OPEN 状态。无新版本发布。

---

## 2. 版本发布

今日无新 Release，本节省略。

---

## 3. 项目进展

今日共有 **9 条 PR 合并/关闭**、**54 条 Issue 关闭**，推进方向集中在启动性能、Provider 覆盖与配置卫生三块。

| PR | 状态 | 推进内容 |
|---|---|---|
| [#8474](https://github.com/earendil-works/pi/pull/8474) `feat(coding-agent): bundle Node runtime` | 已关闭 | 重构打包方式，显著减少加载文件数，直指**慢 IO 环境启动问题**，尤其 Windows Defender 扫描导致的启动延迟。作者 @mitsuhiko |
| [#9594](https://github.com/earendil-works/pi/pull/9594) `feat(ai): add Gemini-only Antigravity provider` | 已关闭 | 新增 Google Antigravity 一等 OAuth provider，**恢复订阅制 Gemini 访问**（此前上游实现被移除后失效） |
| [#8732](https://github.com/earendil-works/pi/pull/8732) `fix(ai): preserve reasoning_content on cross-model replay` | 已关闭 | 修复 DeepSeek 系 thinking 端点在跨模型重放时因缺失 `reasoning_content` 被拒的问题 |
| [#9589](https://github.com/earendil-works/pi/pull/9589) `fix(ai): type user input items in Responses API` | 已关闭 | 修复严格 Responses 端点因 input item 缺 `type` 报 400 |
| [#9584](https://github.com/earendil-works/pi/pull/9584) / [#9582](https://github.com/earendil-works/pi/pull/9582) `fix: select sole scoped model when cycling` | 已关闭 | 修复 `Ctrl+P` 在 scope 内仅一个且与当前模型不同时误报 "Only one model in scope" |
| [#9581](https://github.com/earendil-works/pi/pull/9581) `fix: warn when prompt template frontmatter fails to parse` | 已关闭 | 对应 Issue #9354，让 prompt 模板 YAML 解析失败不再静默丢弃，复用 TUI 既有告警通道 |
| [#9591](https://github.com/earendil-works/pi/pull/9591) `feat: export image bytes MIME detector` | 已关闭 | 导出 `detectSupportedImageMimeType`，解除沙箱化扩展读取图片的能力限制 |
| [#4318](https://github.com/earendil-works/pi/pull/4318) `Moves changelog ack state out of settings.json` | 已关闭 | 新增 `~/.pi/agent/state.json` + StateManager，使 `settings.json` 保持用户可管理、可 dotfiles 分发 |

**整体评估**：功能面推进扎实（新 provider + 3 个兼容性修复 + 启动性能重构），但架构级变更（#9548、#6534、#9434）尚无一条落地，项目处于"底层修复快、上层演进慢"的节奏。

---

## 4. 社区热点

### Issues 评论榜 Top 5

1. **[#8684](https://github.com/earendil-works/pi/issues/8684)（OPEN，8 评论）`PI_OFFLINE` 静默禁用全部 provider 模型发现**
   文档声明其仅关闭启动期网络运维（更新检查、遥测），实际却在整个 session 内禁用所有 provider model-catalog 网络发现。属**文档与行为严重不符**，8 条评论显示社区在争论"是改文档还是改行为"。
2. **[#9298](https://github.com/earendil-works/pi/issues/9298)（CLOSED，7 评论）Grok 403 被标注为 "OpenAI API error"**
   Grok 余额/订阅错误经 OpenAI-compatible Responses 通道后被包装成 OpenAI 计费错误，用户被误导到错误的服务商去排查。已关闭。
3. **[#8752](https://github.com/earendil-works/pi/issues/8752)（OPEN，6 评论，👍5）Bedrock `usage.input` 跨模型族未规范化**
   Anthropic 族上报净值、OpenAI 族上报含 cacheRead/cacheWrite 的毛值，直接导致**虚假 cache-miss 提示与输入成本翻倍**。这是今日 👍 最高的问题。
4. **[#9381](https://github.com/earendil-works/pi/issues/9381)（CLOSED，6 评论）Package Report: pi-safe-compact**
   社区上报第三方包 `pi-safe-compact` 0.6.3 存在可疑/不安全行为（涉及用户账号不可用）。已关闭，但暴露了**第三方包审核链路**的诉求。
5. **[#8720](https://github.com/earendil-works/pi/issues/8720)（OPEN，6 评论）空白 tool result 永久 brick 掉会话**
   工具返回纯空白（Windows bash 的 `"\r\n"`）时被原样发给 OpenAI-compatible provider，触发 HTTP 400，且坏消息滞留历史，此后**每个请求都失败**。

### PR 关注点

- **[#9548](https://github.com/earendil-works/pi/pull/9548) Mid conversation system messages**（@mitsuhiko，OPEN）：把系统提示文本与工具变更写入 transcript 而非静默改写起始条件，支持恢复/分支后还原状态并保留缓存前缀。属**核心数据模型变更**，影响面大。
- **[#6534](https://github.com/earendil-works/pi/pull/6534) feat(ai): add developer message role**（@mitsuhiko，OPEN，自 07-11 起）：experimental，关联 RFC 54。
- **[#9601](https://github.com/earendil-works/pi/pull/9601) fix: avoid transcript scans for exact session IDs**：直接回应 #9440 的性能痛点。

**诉求解读**：社区当前最关心的不是"能不能用"，而是**"花钱对不对、错误归因准不准、坏消息能不能自愈"**。三组高赞/高评论问题全部指向 provider 适配层的语义保真度，而非 UI 或功能缺失。

---

## 5. Bug 与稳定性

按严重程度排列（🔴 阻断 / 🟠 高 / 🟡 中）：

### 🔴 会话级阻断

| Issue | 现象 | Fix PR |
|---|---|---|
| [#8720](https://github.com/earendil-works/pi/issues/8720) | 空白 tool result 触发 HTTP 400 且污染历史，**会话永久不可用** | ❌ 未见 |
| [#9306](https://github.com/earendil-works/pi/issues/9306) `[inprogress]` | turn 以 `error`/`aborted` 结束但已流出 `toolCall` 块，留下未匹配调用，下次 `runAgentLoopContinue` 被 provider 拒绝 | ❌ 未见 |
| [#9599](https://github.com/earendil-works/pi/issues/9599) | `tool_execution_end` 监听器抛错导致已完成工具的 toolResult 未写入 `agent.state.messages`，历史中出现孤立 tool call | ✅ 已 CLOSED |
| [#9596](https://github.com/earendil-works/pi/issues/9596) | 同目录并发两个 `pi -c` 写入同一 session 文件，**无锁无告警**，两条对话交错、产生非预期分支 | ✅ 已 CLOSED（当日） |

### 🟠 成本与正确性

| Issue | 现象 | 标记 |
|---|---|---|
| [#8752](https://github.com/earendil-works/pi/issues/8752) | Bedrock `usage.input` 未按模型族规范化 → 虚假 cache-miss、输入成本翻倍 | 👍5，OPEN |
| [#9457](https://github.com/earendil-works/pi/issues/9457) | `bedrock-converse-stream` 从不设置 `cacheWrite1h`，1h 缓存写入按 5m 费率计费 | 👍4，OPEN |
| [#9210](https://github.com/earendil-works/pi/issues/9210) | 经 Vercel AI Gateway 的 Anthropic Messages，`cacheWrite1h` 恒为 0，1h 写入按 5m 计费 | OPEN |
| [#9391](https://github.com/earendil-works/pi/issues/9391) | 压缩后 stale signed thinking blocks 每轮重放，Anthropic 每请求丢弃 15 个块（`prefix_binding_mismatch`） | OPEN |
| [#9602](https://github.com/earendil-works/pi/issues/9602) | 压缩时纳入被先前模型请求省略的 thinking 消息，导致**溢出** | ✅ 已 CLOSED |

> 注：#

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*