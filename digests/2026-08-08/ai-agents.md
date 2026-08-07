# OpenClaw 生态日报 2026-08-08

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-07 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-08

## 1. 今日速览

过去24小时项目保持**极高活跃度**：共更新500条Issue（新开/活跃465条，关闭35条）和500条PR（待合并381条，合并/关闭119条），但**没有新版本发布**。社区提交与讨论热情高涨，但维持者审查速度明显落后（PR合并率仅约24%），大量P0/P1级Bug和等待验证的PR持续积压。值得警惕的是，今日出现了4个P0级问题（数据库迁移失败致网关无法启动、totalTokens膨胀导致过早压缩丢数据、iOS更新破坏Talk Mode、CLI预检损坏实时状态库），且均有实际的用户数据丢失/服务中断报告，项目健康度处于“**高活跃、高积压、高风险**”状态。

---

## 2. 版本发布

**无新版本发布。**

上一个已知版本仍为 `2026.7.2` 系列。多个已报告问题（如数据库迁移失败 #119263、iOS 应用兼容性 #108520、网关冷启动回归 #119087）仍待修复并合入下一个版本，暂无候选版本的发布时间线可参考。

---

## 3. 项目进展

今日共有 **119 个 PR 被合并或关闭**。根据可获取数据，以下为值得关注的重要进展：

### 已合并/关闭

- **[#111528] fix(agents): prevent false mid-turn overflow recovery**（已关闭，proof: sufficient，P1）— 修复了启用 opt-in 中轮预检时，工具结果密集的长轮次被误判为上下文溢出、导致先前工具结果被持久截断的问题。合并后消除了误报溢出恢复对会话状态的破坏风险。
  链接：https://github.com/openclaw/openclaw/pull/111528

- **[#110171] feat(talk/realtime): voice chat should behave identically to text chat**（Issue 已关闭，P1）— 语音对话与文本对话的上下文对等问题获得解决（linked PR 已合入），iOS Talk 场景下长期记忆与对话历史将保持一致。
  链接：https://github.com/openclaw/openclaw/issues/110171

- **[#92884] config validate rejects plugin-owned channel schema extensions**（Issue 已关闭，P2，fix-shape-clear, queueable-fix）— 此前 `config validate` 会在插件元数据扩展内置 channel schema 之前拒绝插件拥有的配置扩展，现已修复（对应 fix PR 已合入），扫清了 Slack 等插件引入 schema-backed 配置的障碍。
  链接：https://github.com/openclaw/openclaw/issues/92884

### 合并方向信号

- **Code Mode 12层修复栈**（#120361 Layer 12/12 + #120360 Layer 11/12 + #119892 等依赖链）正在持续推进，覆盖 exec 目标投影、因果修复、trace 投影等核心能力。虽然尚未合入，但栈式提交方式表明这是近期重点工程的收尾阶段。
  链接：https://github.com/openclaw/openclaw/pull/120361

- **macOS 实时语音（Talk）功能** 的两个PR（#118499 Gateway-relay Talk 支持、#118505 Talk 设置界面）仍在等待更充分的视频/截图验证（needs proof），但功能已进入可验证阶段。
  链接：https://github.com/openclaw/openclaw/pull/118499 、 https://github.com/openclaw/openclaw/pull/118505

总体而言，今日合并集中在 **会话状态保护、配置校验、语音上下文对等** 三个方向，属于稳定性修复而非新功能铺开。大量功能型PR（Telegram Business Connect、macOS Talk、Code Mode 栈）仍卡在“等待验证”或“等待作者”状态，短期合入压力较大。

---

## 4. 社区热点

### 🔥 最热 Issue：#116277 — DeepSeek v4 Flash 静默回复失败（125条评论）

- **摘要**：DeepSeek v4 Flash 模型在 Telegram 群消息中静默无法生成回复，OpenClaw 仅发布通用 fallback 消息 *“No reply was generated for this message”*，无实际回复内容。
- **标签**：P1, impact:message-loss, issue-rating: 🦞 diamond lobster, source-repro, linked-pr-open
- **链接**：https://github.com/openclaw/openclaw/issues/116277

**诉求分析**：这是今日讨论量最高的Issue，125条评论显示大量用户遭遇了同样的静默失败。核心不满点有两个：一是模型静默失败后没有自动重试或降级到其他模型，而是直接发布无意义的占位消息；二是 fallback 机制完全不透明，用户无法得知失败原因。关联的 PR 已打开但尚无新 fix PR，社区对模型层容错能力有强烈期待。

### 💬 高讨论量 Issue

| Issue | 标题 | 评论数 | 核心诉求 |
|---|---|---|---|
| [#45608](https://github.com/openclaw/openclaw/issues/45608) | 预重置 agentic 内存刷新（/new 和 daily reset 应获得与 compaction 相同的内存刷新机制） | 11（4👍） | 防止 /new 和每日重置销毁会话前丢失重要记忆 |
| [#86684](https://github.com/openclaw/openclaw/issues/86684) | sessions_yield 子代理唤醒可在低上下文时压缩父分支（回归） | 10（1👍） | 子代理完成时父会话被错误压缩，上下文仅65k/1.05M |
| [#85030](https://github.com/openclaw/openclaw/issues/85030) | MCP 工具未注入子代理会话（bundle-mcp + 允许列表全部被忽略） | 10（6👍） | 多配置方式全部失效，子代理只能使用内建工具 |
| [#53408](https://github.com/openclaw/openclaw/issues/53408) | 长对话后 write/exec 工具参数静默丢失 | 10（2👍） | 工具调用参数在15+轮后变为空对象，工作流断裂 |
| [#45494](https://github.com/openclaw/openclaw/issues/45494) | Cron 任务在 LLM API 持续中断时静默超时而非快速失败 | 9 | 每次重试耗尽180s，无法及时感知故障 |

### 社区情绪观察

- **“静默失败”成为众矢之的**：多个高讨论Issue（#116

---

## 横向生态对比

# 个人 AI 助手与自主智能体开源生态横向对比报告

**数据窗口：2026-08-07 ~ 2026-08-08** | **覆盖项目：OpenClaw / Hermes Agent / Pi / LiteLLM / Temporal**（OpenHands SDK 今日无数据）


## 1. 生态全景

当前生态呈现"智能体应用层 + 基础设施层"双轨分化：OpenClaw、Hermes Agent、Pi 等智能体项目聚焦会话记忆、多端体验与开发效率，LiteLLM、Temporal 则分别承担模型网关与工作流编排底座。整体活跃度极高但健康度两极分化——头部项目（OpenClaw、Hermes）社区提交量远超维护者审查能力，处于"高活跃、高积压"状态，单日出现多个 P0 数据丢失级问题；中小型项目（Pi、LiteLLM、Temporal）则保持稳健合并节奏。贯穿所有项目的共同痛点是**长会话上下文管理的可靠性**（压缩不触发、误触发、压缩后不继续）与**静默失败对用户信任的消耗**。生态正从"功能铺开期"全面转入"稳定性与工程治理期"。

## 2. 各项目活跃度对比

| 项目 | Issues | PRs | 合并/关闭率 | Release | 健康度评估 |
|---|---|---|---|---|---|
| **OpenClaw** | 500（新/活跃 465，关闭 35） | 500（待合并 381，合并/关闭 119） | 23.8% | 无 | 🔴 高活跃/高积压/高风险：4 个 P0 含数据丢失 |
| **Hermes Agent** | 362（新/活跃 311，关闭 51） | 500（待合并 350，合并/关闭 150） | 30% | 无 | 🟠 高吞吐重构 + 密集修复，桌面端 P1 积压 |
| **OpenHands SDK** | — | — | — | — | ⚪

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-08

> 数据来源：github.com/NousResearch/hermes-agent | 数据窗口：过去 24 小时（截至 2026-08-07 更新）


## 1. 今日速览

过去 24 小时项目活跃度处于 **高位**：共产生 362 条 Issue 更新（新开/活跃 311，关闭 51）与 500 条 PR 更新（待合并 350，合并/关闭 150），无新版本发布。当前主线是 **repo 级 god-file 分解重构**（Epic #78647，59 评论），由 @andrexibiza 持续推动，已拆分为 `context_compressor.py`、`auth.py`、`kanban_db.py`、`auxiliary_client.py` 等多个子任务。稳定性层面，**桌面端（macOS/Windows）与会话状态管理** 是 Bug 高发区，今日出现多个 P1/P2 级别问题；同时 @thatssoheil 今日集中提交了 5 个修复 PR（#81343–#81348），覆盖 delegate 会话隔离、进程组回收、配置解析陷阱等方向。整体而言，项目处于 **高吞吐重构 + 密集修复** 的双轨状态，社区参与度强，但桌面端与平台网关（Feishu/Telegram/Matrix/WhatsApp）的稳定性仍需重点关注。


## 2. 版本发布

**无新版本发布。**

过去 24 小时内 Hermes Agent 未发布任何新 Release。上一个已知版本为 0.20.0（存在桌面端底部面板缺失的回归报告，见 #79407）；另有 0.19.0 的 Windows 更新失败反馈（#73381）仍在跟踪。


## 3. 项目进展

过去 24 小时合计 **150 条 PR 被合并或关闭**，以下为可见的代表性合入/关闭项：

- **[#21683] fix: guard BlueBubbles sends with contact book**（已关闭）
  安全加固：BlueBubbles 发送目标必须通过联系人簿精确解析（ID/显示名/别名），直发短信须匹配唯一已认证的 allow_outbound DM handle，减少消息投递到错误联系人的风险。
  https://github.com/NousResearch/hermes-agent/pull/21683

- **[#73249] fix(auth): preserve explicit credential status resets**（已关闭）
  修复凭据池状态重置被 on-disk 合并逻辑吞掉的问题——显式清除的凭据状态现在可以正确持久化，同时保留陈旧写入保护。
  https://github.com/NousResearch/hermes-agent/pull/73249

- **[#80718] Show earlier messages no longer hides most of a session**（已关闭）
  桌面端修复："Show earlier messages" 按钮此前因 DOM 预算与权重函数混用，出现在会话底部两三轮之外，导致大部分会话被隐藏；现已修正预算核算逻辑。
  https://github.com/NousResearch/hermes-agent/pull/80718

- **[#68358]（Issue 关闭，sweeper:implemented-on-main）** 新桌面会话消息被错误路由到陈旧 TUI 会话的问题已标记为合入 main。
  https://github.com/NousResearch/hermes-agent/issues/68358

- **[#61495]（Issue 关闭）** Matrix 手动 cron 投递报错 "Timeout context manager should be used inside a task" 已关闭，表明修复已落地。
  https://github.com/NousResearch/hermes-agent/issues/61495

**整体判断**：项目的 god-file 分解重构持续推进（多个 shard 子任务获得更新），同时安全/认证/消息路由类修复保持合入节奏，代码质量治理处于活跃期。


## 4. 社区热点

以下为过去 24 小时讨论最活跃的 Issues/PRs（按评论数排序）：

- **[#78647] Epic: Shard all 20 god files — repo-wide god-file decomposition** — 59 评论
  社区对 repo 级重构方向讨论极为热烈。该 Epic 确立"god files 一律拆分、不允许回退"的仓库政策，代表项目正在经历一次大型架构治理。问题在于 god-file 文件体量巨大（如 `kanban_db.py` 10,275 行、`auxiliary_client.py` 9,924 行），拆分难度和工作量都值得关注。
  https://github.com/NousResearch/hermes-agent/issues/78647

- **[#64182] Tracking: Plugin Interface Expansion — community ideas, July 2026** — 29 评论
  插件接口扩展的汇总跟踪 Issue，源自 Discord 社区讨论。目标是让长期排队的 PR 能基于稳定的公共接口合并，社区对插件生态的扩展诉求强烈。
  https://github.com/NousResearch/hermes-agent/issues/64182

- **[#78645] Shard agent/context_compressor.py (god-file decomposition)** — 25 评论
  `context_compressor.py`（6,789 行）拆分专项。作为 god-file 分解的具体执行项，评论热度高说明社区既关心重构进度，也关注拆分过程中是否会引入行为变化或回归。
  https://github.com/NousResearch/hermes-agent/issues/78645

- **[#63047] [Bug]: Desktop app becomes completely unresponsive after ~5 messages on macOS 27 beta** — 13 评论
  桌面端 P1 级 Bug 引发持续关注。用户报告约 5 轮对话后整个 UI 冻结（含设置面板），且存在与 #40692 类似的卡顿问题。社区对 macOS 27 beta 下的桌面端稳定性表达了较高关注。
  https://github.com/NousResearch/hermes-agent/issues/63047

- **[#4335] Feature Request: Cross-platform session context sharing (CLI ↔ Telegram)** — 12 评论
  跨平台（CLI/Telegram/Discord）会话上下文共享的功能请求，获得 3 个 👍，长期讨论热度稳定。用户期望不同网关间的会话状态能互通，而非各自隔离。
  https://github.com/NousResearch/hermes-agent/issues/4335

另外，今天出现一批编号密集（#81342–#81349）的新 PR，由多位作者提交，显示社区贡献者活跃度处于高位。


## 5. Bug 与稳定性

按严重程度排列（P1 优先），标注是否已有对应修复 PR：

### P1 — 严重

- **[#63047] macOS 27 beta 桌面端约 5 条消息后完全无响应（含设置）**
  影响：UI 全冻结，仅能等待或强制退出。目前**未见对应 fix PR**。已有 13 条评论，属于高危未决问题。
  https://github.com/NousResearch/hermes-agent/issues/63047

- **[#79278] 上下文压缩可能丢弃进行中的工具链——副作用已完成但结果丢失，agent 重放执行**
  影响：非幂等操作可能被重复执行，存在安全风险。**未见 fix PR**，但有 @zakhounet 提供的详细复现路径。
  https://github.com/NousResearch/hermes-agent/issues/79278

- **[#72924] `hermes update` 运行时重建静默丢弃声明的 extras 依赖（Telegram/voice/test）**
  影响：更新看似成功，实际关键依赖缺失，导致 Telegram、语音等功能不可用。**未见 fix PR**。
  https://github.com/NousResearch/hermes-agent/issues/72924

- **[#81267] Cron 委托子代理持有已关闭的 SessionDB，导致 flush 崩溃** — **已有 fix PR #81343**（今日提交）
  https://github.com/NousResearch/hermes-agent/issues/81267
  https://github.com/NousResearch/hermes-agent/pull/81343

### P2 — 中等

- **[#73381] Windows Desktop 更新失败**——venv 缺少 cryptography + Windows 文件锁导致 `uv pip install -e .` 退出码 2。**未见 fix PR。**
  https://github.com/NousResearch/hermes-agent/issues/73381

- **[#79407] [0.20.0 回归] 桌面端底部操作面板完全消失，应用退化为 viewer-only**。**未见 fix PR。**
  https://github.com/NousResearch/hermes-agent/issues/79407

- **[#75269] SessionDB 保留已结束工作线程的 WAL 读取连接，耗尽 RLIMIT_NOFILE**。**未见 fix PR。**
  https://github.com/NousResearch/hermes-agent/issues/75269

- **[#75801] OpenCode Go gpt-5.6-luna 无 finish_reason → 4 次假"网络中断"续传；桌面端丢弃流式答案**。**未见 fix PR。**
  https://github.com/NousResearch/hermes-agent/issues/75801

- **[#71941] 委托子上下文通过共享终端快照持久残留（HERMES_DELEGATED_CHILD_CONTEXT）**。**未见 fix PR。**
  https://github.com/NousResearch/hermes-agent/issues/71941

- **[#62823] 桌面端 Session Zombie 队列锁与 UI 状态泄漏（并发会话切换时）**。**未见 fix PR。**
  https://github.com/NousResearch/hermes-agent/issues/62823

- **[#80308] read_file 将合法 UTF-8 CJK 文件误判为二进制；search_files 对所有查询返回 0 结果**。**未见 fix PR。**
  https://github.com/NousResearch/hermes-agent/issues/80308

- **[#69163] 导入 coder profile 后 gateway 未注册，`coder gateway start` 报错**。**未见 fix PR。**
  https://github.com/NousResearch/hermes-agent/issues/69163

### P3 — 较低

- **[#10251] Feishu 命令审批卡片按钮点击报错 200340**（9 评论）。**未见 fix PR。**
  https://github.com/NousResearch/hermes-agent/issues/10251

- **[#7675] Feishu 三合一问题：卡片交互被当成 `/card` 命令、审批按钮无效、流式卡片回复缺失**。**未见 fix PR。**
  https://github.com/NousResearch/hermes-agent/issues/7675

- **[#51327] Linux .desktop 启动器下 Electron chrome-sandbox 缺少 setuid 导致静默失败**。**未见 fix PR。**
  https://github.com/NousResearch/hermes-agent/issues/51327

- **[#80308 关联] Windows 平台文件工具问题持续积累**，见上。

### 其他值得注意

- **[#81347] fix(terminal): keep mid-command backgrounded compounds valid shell**（今日提交）——修复 `A && B & C` 被错误改写为 `A && {

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

## Pi 项目动态日报 — 2026-08-08

### 1. 今日速览

过去 24 小时项目处于高活跃状态：共更新 Issues 63 条（其中 54 条关闭，9 条新开/活跃），PR 更新 26 条（17 条已合并/关闭），并发布了 v0.84.1。社区讨论焦点集中在 Windows 使用体验（#7547，23 评论）、上下文压缩阈值不触发（#6879，15 👍）及系统提示词对工具调用的过度引导（#7128）。整体来看，项目在 Bug 修复与功能迭代上并行推进，Issue 关闭率较高，项目健康度良好。

---

### 2. 版本发布：v0.84.1

**https://github.com/earendil-works/pi/releases**

本次发布包含两项新功能：

- **Qwen Token Plan Individual** — 内置了面向个人订阅计划的模型提供商，详情见 [API Keys 文档](https://github.com/earendil-works/pi/blob/v0.84.1/packages/coding-agent/docs/providers.md#api-keys)。
- **认证就绪检查** — 新增 `pi auth` 相关认证状态检查能力（发布说明被截断，完整变更待查）。

⚠️ 迁移注意事项：目前未在发布说明中提及明确的破坏性变更，但注意有用户报告 #7771 在升级到 0.84.1 后出现启动失败（Node 23 环境下 `zlib.createZstdDecompress is not a function`），建议 Node 版本非 LTS 的用户留意。

---

### 3. 项目进展

今日合并/关闭了 17 条 PR，其中有几个值得关注：

- **#7710 feat(agent): restore suspended harness operations.**（[链接](https://github.com/earendil-works/pi/pull/7710)）实现了 harness v2 计划中的 R3 恢复机制，允许从会话记录中重建 `AgentHarness`，是 Agent 状态管理的一大步。
- **#7792 feat(coding-agent): bridge Cursor CLI auth via local agent session**（[链接](https://github.com/earendil-works/pi/pull/7792)）新增隐藏的 `cursor-agent` 扩展，可复用现有 Cursor CLI 登录态，并暴露 `pi cursor status` 健康检查命令。
- **#7780 TUI performance improvement**（[链接](https://github.com/earendil-works/pi/pull/7780)）通过增量解析 Markdown 和惰性渲染失效优化 TUI 性能。
- **#7749 fix(coding-agent): preserve custom tool renderers after reload**（[链接](https://github.com/earendil-works/pi/pull/7749)）修复了 `/reload` 后 `session_start` 注册的自定义工具渲染器丢失的问题。
- **#7795 fix(coding-agent): use `command -v` to verify wl-copy exists**（[链接](https://github.com/earendil-works/pi/pull/7795)）将外部二进制 `which` 替换为 shell 内建 `command -v`，增强沙箱环境兼容性。
- **#7788 fix(example): render tool errors via `context.isError` in built-in-tool-renderer**（[链接](https://github.com/earendil-works/pi/pull/7788)）修复示例中错误检测依赖字符串匹配的不稳定问题。
- **#7758 feat(coding-agent): add exit foreground task and `ctx.version`**（[链接](https://github.com/earendil-works/pi/pull/7758)）允许扩展在 Pi 退出后将控制权移交给前台长驻进程，同时暴露版本信息。

此外，**#7759 Feat/matvenus agent**（[链接](https://github.com/earendil-works/pi/pull/7759)）也已关闭，属于新 agent 接入。

---

### 4. 社区热点

- **[#7547 [Windows] How do you use Pi on windows? What issues are you seeing?](https://github.com/earendil-works/pi/issues/7547)** — 23 条评论，1 👍。作者发起调研，指出 Windows 上运行 Pi 的方式太多，难以确定核心团队应聚焦的方向。这是一次社区摸底，背后的诉求是希望官方明确 Windows 支持策略与最佳实践。
- **[#6879 auto-compaction never triggers after context grows past 100% until provider overflow](https://github.com/earendil-works/pi/issues/6879)** — 13 条评论，15 👍。用户在一次 2 小时以上的 agentic turn 中，上下文超过压缩阈值后继续增长，直到 API 在 373k tokens 才拒绝。社区普遍关注上下文压缩可靠性问题。
- **[#7128 New default `PI_*` guideline in system prompt over-encourages unnecessary bash calls](https://github.com/earendil-works/pi/issues/7128)** — 11 条评论，7 👍。最近系统提示词中新增的"检查 PI_* 环境变量"指导让 agent 频繁执行不必要的 env 检查命令，引发 token 浪费讨论。
- **[#7020 Sometimes Pi doesn't continue after compaction](https://github.com/earendil-works/pi/issues/7020)** — 10 条评论。用户反馈长时 coordinator 类会话在压缩后偶发不继续的情况，与 #6879 共同指向压缩机制的稳定性。

---

### 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue | 描述 | 状态 |
|--------|-------|------|------|
| 🔴 高 | [#7771](https://github.com/earendil-works/pi/issues/7771) | 0.84.1 启动失败：`zlib.createZstdDecompress is not a function`（Node 23） | 已关闭，未有对应 fix PR，疑似环境问题 |
| 🔴 高 | [#6879](https://github.com/earendil-works/pi/issues/6879) | 自动压缩在上下文超过 100% 后不触发，直到 provider 溢出拒绝 | 开放中，15 👍，需尽快修复 |
| 🟠 中 | [#7730](https://github.com/earendil-works/pi/issues/7730) | Mac OS 长会话出现 50–110% 高 CPU，内存 600–800MB | 开放中，5 👍，该问题与上下文大小相关 |
| 🟠 中 | [#7736](https://github.com/earendil-works/pi/issues/7736) | 终端宽度不足时未捕获异常导致崩溃（`Rendered line 409 exceeds terminal width`） | 已关闭 |
| 🟠 中 | [#7702](https://github.com/earendil-works/pi/issues/7702) | DeepSeek 模型经 opencode zen 网关在 tool-call 多轮对话中需回传 `reasoning_content` | 已关闭 |
| 🟠 中 | [#7709](https://github.com/earendil-works/pi/issues/7709) | openai-responses 延迟 `function_call` 往返时丢失 `namespace`，导致下轮失败 | 已关闭 |
| 🟡 低 | [#7726](https://github.com/earendil-w

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 | 2026-08-08

> 数据来源：github.com/BerriAI/litellm | 统计周期：2026-08-07 ~ 2026-08-08

## 1. 今日速览

过去 24 小时 LiteLLM 项目保持高活跃度：**65 条 Issues 更新**（新开/活跃 36 条、已关闭 29 条），**213 条 PR 更新**（待合并 135 条、已合并/关闭 78 条），并发布了 1 个开发版（v1.97.0-dev.2）。社区讨论热度集中于**依赖固定策略的争议**（#25280，15 评论 / 13👍）和 **Azure GPT-5.6 成本计算回归**（#36094），反映出用户对库依赖兼容性与计费准确性的高度敏感。在研发侧，**成本/计费准确性**是一条清晰的主线：3 个缓存 token 定价相关 PR 被合并（#26893、#32445、#33071），另有多个价格相关修复在途。项目整体健康度良好，但长期积压的日志开关、限速绕过等老问题仍需维护者关注。

## 2. 版本发布

### v1.97.0-dev.2（开发预览版）
- **发布内容**：该版本重点附带 **Docker 镜像签名验证说明**。所有 LiteLLM Docker 镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 签名，每次发布使用同一密钥（见 [commit `0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0)），用户可据此验证镜像完整性。
- **破坏性变更**：无明确破坏性变更披露。
- **迁移注意事项

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报（2026-08-08）

## 1. 今日速览
过去 24 小时 Temporal 保持中等偏上的活跃度：共 1 条 Issue 更新，27 条 PR 更新，其中 13 条已合并/关闭，14 条仍在待合并状态，合并率约 48%。开发重心集中在 CHASM 纯任务执行不变式、`reliability-2026` 框架下的复制/队列可靠性改进，以及 1.32.0 发布分支准备。今日无新版本发布。社区侧，一个提出替换已废弃 Elastic 客户端依赖的长期 Issue 仍持续收到讨论，值得关注。

## 2. 版本发布
今日无新版本发布。

## 3. 项目进展
今日合并/关闭的 PR 主要围绕可靠性增强、测试基础设施改进与发布准备：

- **[#11441] Make functional tests available to external runners**（@tdeebswihart）：将 137 个根功能测试体迁移到可导入的外部测试注册表，并引入 runner-scoped 集群路由、逻辑测试名和清理机制。这显著降低了外部贡献者编写和运行功能测试的门槛，是项目可测试性的重要提升。  
  https://github.com/temporalio/temporal/pull/11441

- **[#11424] Resend parent workflow asynchronously during standby child completion verification**（@michaely520）：将 standby 子工作流完成验证中的父工作流重发操作改为异步执行，避免跨集群状态同步和历史回填长时间阻塞关键路径。  
  https://github.com/temporalio/temporal/pull/11424

- **[#11311] Fence Backfiller tasks by generation**（@chaptersix）：用持久化的任务序列值替代任务执行时间与 backfill HWM 比较，避免因时钟漂移或任务重放导致 backfill 越界，并兼容旧二进制创建的无编号任务。  
  https://github.com/temporalio/temporal/pull/11311

- **[#11345] Migrate PollerPQ to an intrusive linked list**（@moody-temporal）：将 PollerPQ 的优先级堆迁移为侵入式链表，简化实现并降低维护成本，同时保持所需语义。  
  https://github.com/temporalio/temporal/pull/11345

- **[#11308] Forward schedule versioning overrides**（@chaptersix）：使 legacy 与 CHASM 调度器都能正确将 `VersioningOverride` 传递给工作流启动请求，并在持久化前进行结构校验。  
  https://github.com/temporalio/temporal/pull/11308

- **[#11434] partition scaler: 检查所有可能的队列 backlog**（@carlydf）：修复 `AllActive` 漏检未加载分区/版本队列 backlog 的问题，同时避免 scaler 描述调用加载未加载分区，提升分区伸缩判断的准确性。  
  https://github.com/temporalio/temporal/pull/11434

- **[#11445] Update to API v1.63.5**（@lilydoar）：将 `go.temporal.io/api` 从伪版本升级到正式 tag v1.63.5，满足云发布对 tag 版本的要求。  
  https://github.com/temporalio/temporal/pull/11445

此外，两条 `1.32.0: Prepare release branch` PR（[#11448](https://github.com/temporalio/temporal/pull/11448)、[#11444](https://github.com/temporalio/temporal/pull/11444)）已关闭，说明 1.32.0 发布分支治理文件与依赖已就绪，版本发布流程正在推进。

## 4. 社区热点
- **[#7930] 替换废弃的 Elastic 客户端依赖**（@jmbarzee）  
  这是今日唯一的高热度 Issue，累计 17 条评论，更新于 2026-08-07。核心诉求是使用官方 `github.com/elastic/go-elasticsearch` 替换已废弃的 `github.com/olivere/elastic/v7`。该 Issue 已开放超过一年，仍无实质进展，社区讨论反映出用户对项目长期维护性和依赖卫生的关注。  
  https://github.com/temporalio/temporal/issues/7930

## 5. Bug 与稳定性
今日没有新增的 Bug Issue，但多条已合并 PR 针对稳定性问题：

- **[#11440] Don't DLQ sync versioned transition task when cleanup finds nothing to delete**（@jiechenz）  
  修复了一个边界场景：当源集群工作流已删除，而目标集群应用同步任务时 NotFound，清理逻辑构造的删除任务执行结果为空，此前会错误地将任务送入 DLQ。该修复避免无效 DLQ 积压。  
  https://github.com/temporalio/temporal/pull/11440

- **[#11447] Monitor child execution NotFound after ChildWorkflowExecutionStarted**（@simvlad）  
  在 `createFirstWorkflowTask` 中新增 `child_execution_not_found` 计数器和 Error 日志，用于观测子工作流启动后立刻缺失的异常情况，属于可观测性增强，辅助快速定位跨工作流问题。  
  https://github.com/temporalio/temporal/pull/11447

- **[#11424] standby child completion 验证异步化**（@michaely520）  
  将可能导致长时间阻塞的“重发父工作流”操作移出同步路径，降低 standby 集群处理完成事件时的延迟风险。  
  https://github.com/temporalio/temporal/pull/11424

这些修复多围绕复制路径边界条件和队列伸缩准确性，显示项目在主动加固高可用场景下的稳定性。

## 6. 功能请求与路线图信号
- **依赖替换请求**：Issue #7930 仍开放，用户明确要求替换废弃的 Elastic 客户端。虽然该 Issue 尚未被标记为 accepted，但长期讨论可能促使维护者排期处理。  
  https://github.com/temporalio/temporal/issues/7930

- **CHASM 持续深入**：多条待合并 PR（[#11433](https://github.com/temporalio/temporal/pull/11433)、[#11432](https://github.com/temporalio/temporal/pull/11432)、[#11446](https://github.com/temporalio/temporal/pull/11446)）围绕 CHASM 纯任务失效不变式、严格测试工具及代码库重组展开，表明 CHASM 引擎已进入实现攻坚期，是当前明确的路线图重点。

- **reliability-2026 标签成为主线**：大量 PR 携带 `reliability-2026` 标签，涉及复制任务版本化、队列 backlog 监控、分区伸缩等。可判断 2026 年可靠性工程仍是该项目最重要的投资方向之一。

## 7. 用户反馈摘要
- 在 Issue #7930 的讨论中，用户 @jmbarzee 明确表达了对依赖维护的担忧：`olivere/elastic` 已弃用，继续使用会带来安全与兼容性风险，希望项目采用官方客户端。该反馈具有一定代表性，说明社区用户对 Temporal 底层依赖的现代化程度有较高期望。  
  https://github.com/temporalio/temporal/issues/7930

## 8. 待处理积压
- **[#7930] 替换 Elastic 客户端**：Issue 创建于 2025-06-18，至今已超一年，仍 open 且评论数最高。建议维护者给出明确态度或计划。  
  https://github.com/temporalio/temporal/issues/7930

- **[#10227] CLI 全局标志位置提示**：PR 于 2026-05-12 由 @1fanwang 提交，修复 `temporal-server start -c` 因全局标志位置错误而给出无提示报错的问题。当前仍 open，更新于 2026-08-07，已等待近三个月，亟需维护者 review。  
  https://github.com/temporalio/temporal/pull/10227

- **[#11255] 即时队列 backlog 年龄指标**：PR 于 2026-07-23 提交，为 `shardinfo` 增加 `shardinfo_immediate_queue_backlog_age` 指标，当前仍 open。该功能对排队延迟观测有直接帮助，建议优先合入。  
  https://github.com/temporalio/temporal/pull/11255

---

**总结**：Temporal 项目今日整体健康度良好，PR 合并节奏稳定，可靠性改进和测试基建是当前主要推进方向；无新版本发布，但 1.32.0 发布分支已准备完毕。需留意长期未响应的依赖替换 Issue 和等待较久的 CLI 修复 PR，避免社区贡献者积极性受挫。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*