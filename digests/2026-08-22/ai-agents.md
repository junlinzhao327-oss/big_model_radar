# OpenClaw 生态日报 2026-08-22

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-21 22:45 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-22

## 1. 今日速览

过去 24 小时内，OpenClaw 项目保持高度活跃：共产生 500 条 Issue 更新（新开/活跃 490 条，关闭 10 条）和 500 条 PR 更新（待合并 389 条，合并/关闭 111 条）。无新版本发布，项目处于密集开发迭代期。值得关注的是，今日更新中出现 1 个 P0 级数据安全 Bug（文件工具剥离 `@` 路径前缀）以及多个 P1 级消息丢失/会话状态问题，但绝大多数 Bug 已有对应的修复 PR 在推进中。整体来看，项目社区参与度高、自动化维护流程（clawsweeper）运转成熟，但部分功能请求与长期积压的 PR 仍需维护者给予决策关注。

---

## 2. 版本发布

过去 24 小时内无新版本发布。

---

## 3. 项目进展

今日关闭/合并的 PR 主要覆盖网关稳定性、macOS 应用、Web UI 和工具链优化：

**网关架构与稳定性**
- [fix(gateway): keep conversation delivery within agent bindings (#126424)](https://github.com/openclaw/openclaw/pull/126424) — 修复多代理场景下会话工具将消息投递到未绑定会话的问题，避免路由污染和跨代理串话。
- [fix(status): surface an invalid config instead of reporting a healthy system (#127402)](https://github.com/openclaw/openclaw/pull/127402) — `openclaw status` 此前在配置文件校验失败时仍以退出码 0 报告健康状态，本次修复为静默配置错误增加了显式提示。

**平台与运维**
- [fix(macos): preserve remote tunnels when switching connection modes (#127665)](https://github.com/openclaw/openclaw/pull/127665) — 修复 macOS 用户在本地/远程 Gateway 切换时，本地端口清理任务误杀新建 SSH 隧道的问题。
- [refactor(tooling): centralize managed child process cleanup (#127480)](https://github.com/openclaw/openclaw/pull/127480) — 将仓库工具链中独立实现的进程组信号、存活轮询、Windows 进程树终止逻辑统一收口，降低维护成本。

**Web UI 与性能**
- [fix(ui): keep run history dropdown text consistent across devices (#127443)](https://github.com/openclaw/openclaw/pull/127443) — 修复移动端 Automations 运行历史排序下拉框字体与相邻控件不一致的问题。
- [perf(discord): avoid redundant outbound payload cleanup (#127422)](https://github.com/openclaw/openclaw/pull/127422) — 消除 Discord 消息发送路径中的重复顶层字段清理，减少每次发送的分配开销。

**测试与质量控制**
- [improve: speed up browser extension security test suites (#127471)](https://github.com/openclaw/openclaw/pull/127471) — 将浏览器扩展安全测试中默认的 50ms 观察间隔改为异步确认完成后立即推进，显著压缩测试墙钟时间。

---

## 4. 社区热点

今日讨论最活跃的 Issue 集中在渠道适配、环境变量处理与跨平台稳定性：

**[#48788] feat: centralized filename encoding utility for multi-encoding Content-Disposition handling（19 条评论，👍 1）**
https://github.com/openclaw/openclaw/issues/48788

> 讨论核心：PR #48578 已修复飞书中文文件名被误读为 Latin-1 的最常见场景，但社区认为需要从架构层面建立统一的文件名编码工具，覆盖 Shift-JIS、EUC-KR、GB18030 等更多编码。这一诉求反映出用户对多渠道、多语言环境下文件传输可靠性的普遍关注。

**[#53628] [Bug]: ${XDG_CONFIG_HOME} is not process when installing a skill（14 条评论，👍 1）**
https://github.com/openclaw/openclaw/issues/53628

> Docker 安装场景下，`XDG_CONFIG_HOME` 环境变量在 clawhub 技能安装时未被解析展开。该问题从 3 月持续至今仍无修复 PR，引发用户对配置一致性的讨论。

**[#119796] [Bug]: Windows: vitest teardown fails with EBUSY unlink on agent state DB（14 条评论）**
https://github.com/openclaw/openclaw/issues/119796

> Windows 平台下，`extensions/zalo` 的轮询测试套件在 teardown 阶段因 `openclaw-agent.sqlite` 句柄未释放而报 `EBUSY`，导致测试失败。该问题被标记为 `clawsweeper:linked-pr-open`，已有修复 PR 在跟进。

**[#87561] Define durable final fallback delivery semantics across channels（10 条评论，👍 1）**
https://github.com/openclaw/openclaw/issues/87561

> 围绕“代理回合以内部回退/错误消息结束时，用户却因渠道投递层抑制或丢弃最终负载而看到沉默”的核心矛盾，社区在讨论跨渠道统一的持久化投递语义，其中引用了 #845 的 WhatsApp 报告作为案例。

---

## 5. Bug 与稳定性

今日报告的 Bug 按严重程度排列如下（🩺 = 已有 fix PR 在推进，🔴 = 尚无修复 PR）：

**P0（数据丢失风险）**
- [🔴🩺 #119270] [Bug]: file tools strip a leading @ from destination paths（8 月 4 日创建，仍打开）
  https://github.com/openclaw/openclaw/issues/119270
  `write`/`edit`/`apply_patch` 在解析目标路径前剥离开头的 `@` 符号，导致写入/改写/删除错误文件。这是当前最严重的数据安全问题。

**P1（消息丢失 / 会话状态损坏）**
- [🔴 #87561] Define durable final fallback delivery semantics across channels
  https://github.com/openclaw/openclaw/issues/87561

- [🔴 #97616] OpenClaw leaks unreaped hook/tool child processes（僵尸进程累积，运行时退化）
  https://github.com/openclaw/openclaw/issues/97616

- [🔴 #49381] Feishu: duplicate final replies can occur after model failover from rate-limited primary
  https://github.com/openclaw/openclaw/issues/49381

- [🔴 #86612] Docker gateway container restart loop when `OPENCLAW_SANDBOX=1` and `OPENCLAW_HOME=/mnt/...`
  https://github.com/openclaw/openclaw/issues/86612

- [🔴 #83598] anthropic:claude-cli OAuth refresh still dead-ends main lane in 2026.5.12（所有代理流量 failover）
  https://github.com/openclaw/openclaw/issues/83598

- [🔴 #108215] Context usage drops from 57% to 13% without compaction after large tool output（无压缩的上下文丢失）
  https://github.com/openclaw/openclaw/issues/108215

- [🩺 #84486] Text before tool calls is lost in Feishu streaming card reply mode（`clawsweeper:fix-shape-clear`）
  https://github.com/openclaw/openclaw/issues/84486

- [🩺 #86050] Gateway buffers claude-cli stream events; surfaces only see final message（`clawsweeper:linked-pr-open`）
  https://github.com/openclaw/openclaw/issues/86050

- [🩺 #42803] Feishu text commands (/stop, /new, /status) no longer bypass queue during active agent run（回归）
  https://github.com/openclaw/openclaw/issues/42803

**P2（功能性缺陷 / 平台兼容性）**
- [🩺 #119796] Windows vitest teardown `EBUSY` on agent state DB → [PR #127646 等] 相关修复在途
  https://github.com/openclaw/openclaw/issues/119796

- [🩺 #120735] Telegram inbound stickers arrive as raw file refs with no description and are not staged to disk
  https://github.com/openclaw/openclaw/issues/120735

- [🩺 #50611] Memory flush never triggers when `reserveTokensFloor` equals `contextWindow`
  https://github.com/openclaw/openclaw/issues/50611

- [🩺 #43797] Sandbox prune does not clean up workspace directory（磁盘空间泄漏）
  https://github.com/openclaw/openclaw/issues/43797

- [🩺 #50490] Feishu 群聊中 activation 模式切换无效（回归）
  https://github.com/openclaw/openclaw/issues/50490

- [🩺 #124751] iOS app duplicates assistant replies at the bottom and does not auto-scroll to

---

## 横向生态对比

说明：本次快照中 **Hermes Agent、LiteLLM、Temporal** 未提供社区动态数据，故横向对比聚焦于有完整数据的 **OpenClaw、OpenHands SDK、Pi** 三个项目。

---

## 1. 生态全景

个人 AI 助手与自主智能体开源生态已从“演示可行性”进入“工程可靠性”阶段。当前格局呈分层协同：OpenClaw 代表全渠道个人助手运行时，OpenHands SDK 代表可嵌入的 Agent 构建组件，Pi 代表垂直编码场景的交互式代理。三者不约而同将重心转向数据安全、会话一致性、长上下文管理与多模型兼容性。社区活跃度分化明显，头部项目日更新量级达数百，但普遍存在 PR 积压与 P0/P1 缺陷并存的情况。

---

## 2.

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目日报 — 2026-08-22

## 1. 今日速览

过去24小时项目保持高度活跃：共产生 **29 条 Issue 更新**（新开/活跃 17，关闭 12）与 **21 条 PR 更新**（待合并 12，已合并/关闭 9），并连续发布 **v1.43.0 与 v1.43.1 两个版本**。项目重点关注 **agent 会话生命周期锁优化、内存加载偏好修复、子代理并发性能、以及多模型提供商兼容性**。值得关注的是，两条高优先级性能 Bug（#4537、#4569）均有对应的修复 PR 在途；同时社区合作类 PR（如 AIML API 的 RevShare 集成、自托管 GitLab token 克隆修复）显示出 SDK 生态的外联扩展态势。项目整体健康度良好，并发与可靠性议题是当前主旋律。


## 2. 版本发布

### v1.43.1（8月21日）
🔗 [Release v1.43.1](https://github.com/OpenHands/software-agent-sdk/releases/tag/v1.43.1) | [发布 PR #4572](https://github.com/OpenHands/software-agent-sdk/pull/4572)

**主要更新内容：**
- **chore(deps)**：gitpython 依赖从 3.1.50 升级至 3.1.58（[PR #4545](https://github.com/OpenHands/software-agent-sdk/pull/4545)），包含安全修复
- **feat(prompt)**：默认 agent prompt 新增本地会话历史存储路径说明，帮助 agent 定位之前的本地对话记录（[PR #4527](https://github.com/OpenHands/software-agent-sdk/pull/4527)）
- **fix(sdk)**：resolve workspace 相关修复

### v1.43.0（8月20日）
🔗 [Release v1.43.0](https://github.com/OpenHands/software-agent-sdk/releases/tag/v1.43.0) | [发布 PR #4553](https://github.com/OpenHands/software-agent-sdk/pull/4553)

**主要更新内容：**
- **feat(plugin)**：新增 Agent Plugins manifest 加载器（root plugin.json + 封闭 schema），为插件生态奠定基础（[PR #4474](https://github.com/OpenHands/software-agent-sdk/pull/4474)）
- **fix(security-scan)**：改进 release security scan 评论输出

**破坏性变更与迁移注意事项：** 两个版本均未标注破坏性变更。v1.43.0 引入的插件 manifest 加载器属于新增能力，不影响现有 API。


## 3. 项目进展

重点合并/关闭 PR 汇总：

| 领域 | PR | 说明 |
|------|-----|------|
| **Prompt/记忆** | [PR #4527](https://github.com/OpenHands/software-agent-sdk/pull/4527) | 已合并。默认 prompt 告知 agent 本地会话历史位置，配合已关闭的 [Issue #4528](https://github.com/OpenHands/software-agent-sdk/issues/4528) |
| **Workspace/LLM** | [PR #4497](https://github.com/OpenHands/software-agent-sdk/pull/4497) | 已合并。修复 workspace 默认 LLM 忽略 active profile 的问题（[Issue #4494](https://github.com/OpenHands/software-agent-sdk/issues/4494)） |
| **SDK 工具** | [PR #4471](https://github.com/OpenHands/software-agent-sdk/pull/4471) | 已合并。修复 `normalize_tool_call` 重复添加 `git` 命令前缀的问题（[Issue #4468](https://github.com/OpenHands/software-agent-sdk/issues/4468)） |
| **LLM 兼容** | [PR #4567](https://github.com/OpenHands/software-agent-sdk/pull/4567) | 已合并。修复 Kimi K3 视觉元数据归一化问题 |
| **工具能力** | [PR #4479](https://github.com/OpenHands/software-agent-sdk/pull/4479) | 已合并。为 `FinishTool` 添加结构化任务结果预设（呼应 [Issue #4106](https://github.com/OpenHands/software-agent-sdk/issues/4106)） |
| **评估/路由** | [PR #3636](https://github.com/OpenHands/software-agent-sdk/pull/3636) | 已合并。新增 `router-classified-3tier` 模型条目并附加递归 preflight 检查 |
| **依赖安全** | [PR #4545](https://github.com/OpenHands/software-agent-sdk/pull/4545) | 已合并。GitPython 3.1.50 → 3.1.58 安全升级 |

**关键进展评估：** 今日合并的 PR 集中解决了三类问题——**用户可感知的 prompt/记忆缺陷**、**LLM 配置漂移**和**工具调用的畸形行为**。特别是 #4471 和 #4497 的修复，前者消除了工具调用层面的静默错误，后者堵住了 keyless 模型被意外启动的隐患。此外，#4479 的完成标志着 agent 任务结果表达从自由文本走向结构化，为任务可观测性铺路。


## 4. 社区热点

### 🔥 讨论热度最高

| 排名 | Issue/PR | 评论数 | 主题 |
|------|----------|--------|------|
| 1 | [#2510 Investigate Dependabot support for uv workspaces](https://github.com/OpenHands/software-agent-sdk/issues/2510) | 22 | 已关闭。长期探讨 uv monorepo 下的 Dependabot 支持方案 |
| 2 | [#2697 [Feature]: QuestionTool -- mid-task structured questions](https://github.com/OpenHands/software-agent-sdk/issues/2697) | 8 | agent 在任务中途遇到歧义时无结构化方式向用户提问 |
| 3 | [#3560 Supply-chain typosquat detection analyzer](https://github.com/OpenHands/software-agent-sdk/issues/3560) | 8 | 供应链投毒检测：需要能识别相似包名的确定性分析器 |
| 4 | [#4542 Global agent_context.load_memory preference ignored](https://github.com/OpenHands/software-agent-sdk/issues/4542) | 5 | 高优先级 Bug：全局内存加载偏好仅在一个路径生效 |

### 需求背后的深层信号

- **#2697 的 QuestionTool 诉求**反映出 agent 在真实任务中频繁遭遇"歧义-猜测-返工"的低效循环。社区希望在 agent 工具集中加入**结构化提问机制**，而非依赖自由文本输出。该需求与 #4106（任务不可行声明）在本质上同源——都在要求**更丰富的 agent-用户通信原语**。
- **#3560 的 typosquat 检测需求**体现了安全维度从"命令形态分析"向"供应链依赖分析"的扩展。开发者希望 `PatternSecurityAnalyzer` 之外，还有能力识别 `openai` vs `openai-py` 这类混淆包名攻击。
- **#2510 虽然已关闭**，但长达 22 条评论、跨 5 个月的讨论说明 uv workspace 用户对 Dependabot 支持的长期痛点。关闭可能意味着暂时搁置或以文档形式承接（见 8 月 PR #4144）。


## 5. Bug 与稳定性

### 高优先级（priority:high）

- **[#4542] `agent_context.load_memory` 全局偏好被忽略**（8月19日创建，8月21日更新，5 评论）
  🔗 https://github.com/OpenHands/software-agent-sdk/issues/4542
  **现象：** 全局用户偏好仅在通过 `agent_profile_id` 启动会话时生效，直接传 `agent` 或 `agent_settings` 的会话会丢失内存加载设置。
  **Fix PR：** ✅ 已有 [PR #4566](https://github.com/OpenHands/software-agent-sdk/pull/4566)（8月21日提交，待合并）

- **[#4569] 全局 `_lifecycle_lock` 导致跨会话阻塞**（8月21日创建，2 评论）
  🔗 https://github.com/OpenHands/software-agent-sdk/issues/4569
  **现象：** `ConversationService` 用单一全局 `asyncio.Lock` 保护所有会话生命周期操作，其中磁盘 I/O 和子进程启动在锁内执行会阻塞无关会话。
  **Fix PR：** ✅ 已有 [PR #4570](https://github.com/OpenHands/software-agent-sdk/pull/4570) + [PR #4513](https://github.com/OpenHands/software-agent-sdk/pull/4513)（含复现测试）

- **[#4537] TaskToolSet 委托持有父会话锁导致 UI 冻结**（8月18日创建，2 评论，👍 1）
  🔗 https://github.com/OpenHands/software-agent-sdk/issues/4537
  **现象：** 子代理运行时持有父会话的 `ConversationState` 锁，耗尽执行线程池并冻结 Agent Canvas 会话列表渲染。
  **Fix PR：** ❌ 暂无直接 fix PR，但 #4570 的 per-conversation lock 改造可部分缓解。

### 中等优先级（priority:medium）

- **[#4544] Condensation 后触发式技能和路径规则静默失效**（8月19日创建，5 评论）
  🔗 https://github.com/OpenHands/software-agent-sdk/issues/4544
  关键字触发的技能注入事件被 condensation 遗忘，导致后续技能/规则不再应用。
  **Fix PR：** ❌ 暂无。

- **[#4541] Qwen3-32B 异常 `<think>` 行为**（8月18日创建，4 评论）
  🔗 https://github.com/OpenHands/software-agent-sdk/issues/4541
  `<think>` 标签出现在标题生成、思想流等多个位置，行为异常。
  **Fix PR：** ❌ 暂无。

- **[#4540] Synthetic Provider 工具调用返回异常语法**（8月19日创建，4 评论）
  🔗 https://github.com/OpenHands/software-agent-sdk/issues/4540
  **Fix PR：** ❌ 暂无。

- **[#4543] 自托管 GitLab 克隆时 token 被忽略**（8月19日创建，3 评论）
  🔗 https://github.com/OpenHands/software-agent-sdk/issues/4543
  **Fix PR：** ✅ 已有 [PR #4571](https://github.com/OpenHands/software-agent-sdk/pull/4571)（8月21日提交，待合并）

- **[#4500] 增量视图缓存跳过 `enforce_properties`，遗留孤儿 action/obs 对**（已关闭）
  🔗 https://github.com/OpenHands/software-agent-sdk/issues/4500

### 其他

- **[#4575] Agent 终端命令继承服务器进程优先级**（8月21日创建）
  🔗 https://github.com/OpenHands/software-agent-sdk/issues/4575
  **Fix PR：** ✅ [PR #4573](https://github.com/OpenHands/software-agent-sdk/pull/4573)（draft，降低 agent 进程优先级）

### 已关闭 Bug（回归验证）

- [#3645] DeepSeek custom base_url 不再剥离 provider 前缀 ✅
- [#4107] TaskToolSet 未向子代理传播父中断 ✅
- [#4468] `normalize_tool_call` 重复添加 git 前缀 ✅（PR #4471 已合并）
- [#4156] Windows 下 uvx 启动 agent-server ModuleNotFoundError ✅
- [#4494] workspace 默认 LLM 忽略 active profile ✅（PR #4497 已合并）


## 6. 功能请求与路线图信号

| 功能请求 | Issue | 状态/关联 PR | 纳入下版可能性 |
|----------|-------|-------------|----------------|
| **50/50 RevShare 集成：OpenHands & AIML API** | [#4574](https://github.com/OpenHands/software-agent-sdk/issues/4574) | [PR #4576](https://github.com/OpenHands/software-agent-sdk/pull/4576) 已提交 | ⭐ 高——合作方已完成技术工作，属于生态扩展 |
| **QuestionTool：任务中结构化提问** | [#2697](https://github.com/OpenHands/software-agent-sdk/issues/2697) | 无关联 PR | 中——累积 8 评论，需求明确，需设计 |
| **供应链 typosquat 检测分析器** | [#3560](https://github.com/OpenHands/software-agent-sdk/issues/3560) | 无关联 PR | 中——安全团队可能接盘 |
| **非阻塞后台子代理执行** | [#2047](https://github.com/OpenHands/software-agent-sdk/issues/2047) | 无关联 PR | 中——与 #4537 的性能问题相关，可能借机推进 |
| **OS keyring 密钥存储** | [#3988](https://github.com/OpenHands/software-agent-sdk/issues/3988) | 无关联 PR，但已有设计文档链接 | 低-中——已有架构设计比较，可能进入规划 |
| **结构化任务不可行声明** | [#4106](https://github.com/Open

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-22

## 今日速览

过去 24 小时项目活跃度中等偏高：Issues 更新 53 条，其中新开/活跃仅 10 条、关闭 43 条，关闭数为新开数的 4 倍以上，说明维护者正在高效清理积压；PR 方面 7 条中 5 条已合并/关闭，2 条待合并，均来自外部贡献者。无新版本发布，项目处于稳定迭代期。社区讨论焦点集中在 Windows 平台体验、自动压缩（auto-compaction）触发机制以及键盘兼容性问题，其中压缩相关 Issue 获得 17 个 👍，反映出用户对长会话稳定性的强烈需求。

---

## 项目进展

今日共合并/关闭 5 个 PR，其中 4 个为功能性修复/增强，1 个为长期悬置的功能实现：

- **#4537 feat: Exit alias**（合并）— 为 `/quit` 增加 `/exit` 别名，与 Codex、Claude、OpenCode 等主流编码代理保持一致。该 PR 自 5 月 15 日创建，今日终于合并，解决了一批用户的长期小困扰。🔗 [PR #4537](https://github.com/earendil-works/pi/pull/4537)

- **#8459 fix(tui): 全屏模式下双击选择保留 `/` 和 `-` 边界**（合并）— 修复 #7746：全屏 TUI 双击路径时按 `Intl.Segmenter` 分词，导致路径被拆成多段。此修复让双击可选中完整路径，显著提升全屏模式下的文本操作体验。🔗 [PR #8459](https://github.com/earendil-works/pi/pull/8459) / [Issue #7746](https://github.com/earendil-works/pi/issues/7746)

- **#8428 fix(coding-agent): 会话上下文重建时重新配对工具结果**（合并）— 修复 #8166 中描述的会话损坏 bug：在恢复、压缩、分支导航等重建路径中，工具结果现在会与发起工具调用的 assistant 消息正确配对，孤立结果会被丢弃。这是对会话稳定性的重要底层修复。🔗 [PR #8428](https://github.com/earendil-works/pi/pull/8428)

- **#8433 feat(coding-agent): 添加 --exclude-extensions 以跳过指定扩展**（合并）— 扩展加载从"全有或全无"变为可精细排除。用户现在可以表达"我的常规扩展集，减去这几个"，对第三方扩展管理很有价值。🔗 [PR #8433](https://github.com/earendil-works/pi/pull/8433)

- **#8443 feat(interactive-mode): 实验性 flag 下通过 Radius artifacts 分享**（合并）— `/share` 命令在实验模式下改用 Radius artifacts 替代 gist，未登录时自动触发认证流程。🔗 [PR #8443](https://github.com/earendil-works/pi/pull/8443)

整体来看，项目在 TUI 交互、会话稳定性和扩展管理三个方向上均有实质推进。

---

## 社区热点

### 最热 Issue：#7547 — Windows 使用方式调研（36 评论）
作者 @petrroll 发起了一项 Windows 使用方式调研，收集用户在 Windows 上的运行方式（WSL、原生、MSYS2 等）以及遇到的问题，以便项目决定优化方向（修复 bug、完善文档 vs 将某些路径外包给扩展）。36 条评论说明 Windows 用户基数可观且诉求多样。🔗 [Issue #7547](https://github.com/earendil-works/pi/issues/7547)

此 Issue 与今日关闭的 #2733（Windows Terminal 退格/删除键问题，11 评论）和 #7130（Kitty 终端退格删除 2 字符，9 评论）形成呼应，共同指向**键盘输入兼容性问题在非标准终端环境中集中爆发**。

### 最高赞 Issue：#6879 — auto-compaction 永不触发（17 👍 / 19 评论）
用户 @alexanderkreidich 报告：在 GPT-5.6-sol 的 agentic 会话中，一次工具调用运行超 2 小时，footer 已显示超过压缩阈值、context 使用超过 100%，但自动压缩始终不触发，直到 API 在 373k tokens 处拒绝请求才被迫压缩。作者建议在每次 agent 步骤后都检查压缩条件。17 个 👍 表明大量用户遭遇过类似长会话失控问题。🔗 [Issue #6879](https://github.com/earendil-works/pi/issues/6879)

### 值得关注：#7995 — OpenRouter responses API 缺少 Anthropic 缓存支持（7 评论）
由 OpenRouter 员工代提交的性能基准报告：870 次试验显示，`openai-responses` 实现因不发送 Anthropic 风格 `cache_control`，导致 Claude 通过 OpenRouter 使用时成本增加 2.5 倍。这是一个直接影响用户账单的性能问题。🔗 [Issue #7995](https://github.com/earendil-works/pi/issues/7995)

---

## Bug 与稳定性

### 严重等级：高

- **#6879 auto-compaction 永不触发，直至 provider 溢出** — 当上下文超过 100% 时压缩不启动，直到 API 拒绝请求（373k tokens）才强制触发。影响所有长会话用户，浪费 tokens 且可能中断会话。已有明确修复建议（每次 agent 步骤后检查），但暂无关联 PR。17 👍 为今日最高。🔗 [Issue #6879](https://github.com/earendil-works/pi/issues/6879)

- **#8134 通过正向代理访问纯 HTTP provider 时，首次工具调用后 agent 停止** — 0.84.0 回归：当 `baseUrl` 为 `http://` 且设置 `HTTP_PROXY` 时，首次模型调用成功、工具执行成功，但后续请求永不返回。阻断使用自建 HTTP 服务的用户。暂无 PR。🔗 [Issue #8134](https://github.com/earendil-works/pi/issues/8134)

- **#2644 长会话崩溃：`FATAL ERROR: JavaScript heap out of memory` (SIGABRT)** — 运行 30+ 分钟且工具使用频繁后 Node.js OOM 崩溃。属于老旧问题（3 月创建），今日有评论更新但未关闭。🔗 [Issue #2644](https://github.com/earendil-works/pi/issues/2644)

### 严重等级：中

- **#7130 Kitty 终端中退格键删除 2 个字符** — Kitty 键盘协议释放事件未被过滤，导致退格行为异常。与 #2733（Windows Terminal 退格问题）同源，均为键盘协议适配回归。🔗 [Issue #7130](https://github.com/earendil-works/pi/issues/7130)

- **#8442 herdr pane 内退格键被忽略（KKP 协议下 legacy 0x7f 冲突）** — 在 herdr pane 中普通退格无效，Ctrl+退格可删除。根因是 Kitty 键盘协议激活后，host 发送 legacy `0x7f` 与协议冲突。🔗 [Issue #8442](https://github.com/earendil-works/pi/issues/8442)

- **#8425 自定义 `app.models.save` 绑定被 `/model` 和 `/thinking` 忽略** — 用户重绑定保存快捷键后，selectors 仍直接匹配 ctrl+s 并显示错误的按键提示。功能正确性受影响，但范围有限。🔗 [Issue #8425](https://github.com/earendil-works/pi/issues/8425)

### 严重等级：低

- **#8456 Gemini 3.7 Flash 拒绝 /tree 分支摘要（MINIMAL thinking 不受支持）** — 内置摘要请求未包含 reasoning 参数，在要求 MINIMAL thinking 的模型上失败。🔗 [Issue #8456](https://github.com/earendil-works/pi/issues/8456)

- **#8417 后台 git 包更新检查在 TUI 上弹出 SSH 密码提示** — SSH 密钥加密且无 agent 时，后台检查会阻塞 UI 并直接打印提示。🔗 [Issue #8417](https://github.com/earendil-works/pi/issues/8417)

---

## 功能请求与路线图信号

### 今日新提需求（均当日关闭 — 进入 triage backlog）

- **#8454 OpenRouter reasoning-mandatory 模型适配** — 后台调用（如会话标题生成）会显式发送 `reasoning:{effort:"none"}`，被要求强制推理的端点（如 `stealth/ox-alpha`）拒绝（HTTP 400）。需适配层在该类模型上自动省略 reasoning 字段。🔗 [Issue #8454](https://github.com/earendil-works/pi/issues/8454)

- **#8453 显式手动全跨度压缩模式** — 提议新增 `/compact --all [instructions]`，压缩整个活跃分支并仅保留最小结构化延续边界。与 #8452（改进压缩提示词状态保真）出自同一作者，显示用户在探索更可控的压缩语义。🔗 [Issue #8453](https://github.com/earendil-works/pi/issues/8453) / [Issue #8452](https://github.com/earendil-works/pi/issues/8452)

- **#8451 RPC 模式增加 provider 登录操作** — 当前 `/login` 仅限交互模式，RPC 客户端需手动编辑 auth.json 重启。提议将 ModelRuntime.login() 暴露为 RPC 操作。🔗 [Issue #8451](https://github.com/earendil-works/pi/issues/8451)

- **#8450 添加 Parasail.io 提供商** — Parasail 员工请求将其平台作为内置 provider（OpenAI 兼容 API，提供 Kimi K3、GLM5.2、DeepSeek V4 Pro/Flash 等模型）。🔗 [Issue #8450](https://github.com/earendil-works/pi/issues/8450)

### 较长期需求（已开放，部分 in-progress）

- **#7553 可配置压缩的思考级别/模型**（inprogress）— 让压缩（自动/手动）使用独立的 thinking level，而不是沿用会话当前级别。对使用推理模型的用户显著影响压缩成本和质量。🔗 [Issue #7553](https://github.com/earendil-works/pi/issues/7553)

- **#8133 按模型配置压缩设置**（inprogress / 3 👍）— 通过 `compaction.profiles` map 为不同模型设置不同的 reserveTokens 等参数。与 #7553 互补，显示压缩机制正在经历系统性升级。🔗 [Issue #8133](https://github.com/earendil-works/pi/issues/8133)

- **#7995 OpenRouter responses API 缓存支持** — 性能/成本关键需求，有可量化的 2.5 倍成本差异。OpenRouter 合作方已介入，预计进入路线图的概率较高。🔗 [Issue #7995](https://github.com/earendil-works/pi/issues/7995)

- **#8140 长行保护机制的参考实现** — 作者明确表示主要作为维护者的背景数据而非期望合并。这类"研究型"Issue 通常用于指引未来方向。🔗 [Issue #8140](https://github.com/earendil-works/pi/issues/8140)

### 已有关联 PR 的功能

- **#8422 fix(ai): xAI Grok Build 省略 reasoning effort**（待合并）— 针对 xAI 拒绝包含 `reasoning.effort` 的请求。与 #8454 是同一类问题：**不同 provider 对 reasoning 字段的接受度差异需要更细粒度适配**。🔗 [PR #8422](https://

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*