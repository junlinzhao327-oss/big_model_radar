# OpenClaw 生态日报 2026-08-26

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-25 22:49 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-26

## 今日速览

过去 24 小时项目活跃度极高：**500 条 Issue 更新**（新开/活跃 435 条，关闭 65 条）与 **500 条 PR 更新**（待合并 301 条，已合并/关闭 199 条，合并率约 39.8%），社区反馈量与开发迭代速度均处于峰值。当前无新版本发布，项目仍处于 `v2026.8.1-beta.3` 验证期，但 `beta.7` 的现场可靠性报告（[#128067](https://github.com/openclaw/openclaw/issues/128067)）已浮现多类消息丢失与重启恢复缺陷，可靠性问题成为社区最集中的关注点。值得注意的是，大量高优 Issue 标有 `clawsweeper:needs-maintainer-review` 与 `needs-product-decision`，表明自动化分类已就绪、但维护者带宽承压，项目处于高反馈、高迭代的 beta 攻坚阶段。

---

## 版本发布

过去 24 小时无新版本发布（最新仍为 [v2026.8.1-beta.3](https://github.com/openclaw/openclaw/releases/tag/v2026.8.1-beta.3)）。

---

## 项目进展

今日关闭/合并的 PR 主要集中于**安全治理、可访问性与构建工具链**三个方向：

- **安全：安装策略警告确认机制落地（双 PR 合围）**
  - [#116489 feat(security): require acknowledgement for install policy warnings](https://github.com/openclaw/openclaw/pull/116489)（XL，已关闭）：为 `security.installPolicy` 增加 `warn` 返回状态，CLI 交互式安装时要求操作者输入确切目标名以确认继续。
  - [#120900 feat(ui): review install policy warnings](https://github.com/openclaw/openclaw/pull/120900)（XL，已关闭）：配套 Control UI 功能，管理员可在界面审查安装策略警告并主动确认插件安装，补齐了操作闭环。

- **可访问性：会话进度卡片显示最后活动

---

## 横向生态对比

## 横向对比分析报告（2026-08-26）

### 1. 生态全景

当前个人 AI 助手/自主智能体开源生态处于**高活跃、高迭代、高反馈**的攻坚阶段。多项目同时面临社区贡献激增与维护者带宽承压的矛盾，合并/关闭速度显著低于流入速度。稳定性问题成为最集中的社区关注点：更新后服务异常、会话持久化失败、跨 provider 兼容性缺陷频繁出现。与此同时，安全治理、可访问性、跨平台支持等工程化议题开始进入核心开发视野，表明生态正从“功能扩展”逐步转向“可靠性加固”。

---

### 2. 各项目活跃度对比

| 项目 | Issue 更新（新开/活跃） | PR 更新（待合并/合并关闭） | 合并率 | Release | 健康度评估 |
|---|---|---|---|---|---|
| **OpenClaw** | 500（435 / 65） | 500（301 / 199） | 39.8% | 无（v2026.8.1-beta.3） | 高活跃但维护者带宽承压，可靠性问题待解 |
| **Hermes Agent** | 388（332 / 56） | 500（425 / 75） | 15.0% | 无 | 贡献意愿强，合并吞吐低，积压风险高 |
| **Pi** | 227（17 / 210） | 33（8 / 25） | 76.0% | 无 | 响应高效，合并率高，处于质量巩固阶段 |
| **LiteLLM** | 94（62 / 32） | 264（172 / 92） | 34.8% | 无 | 活跃稳定，功能开发与 Bug 修复并重 |
| **OpenHands SDK** | 数据未提供 | 数据未提供 | — | — | 无法评估 |
| **Temporal** | 数据未提供 | 数据未提供 | — | — | 无法评估 |

---

### 3. OpenClaw 在生态中的定位

OpenClaw 在提供数据的项目中**社区规模最大**：Issue / PR 更新量均达到 500，与 Hermes 的 PR 量持平但 Issue 量更高；合并率 39.8% 明显高于 Hermes 的 15%，说明维护者响应相对更快。技术路线上，OpenClaw 今日合并的 PR 集中在**安全治理（安装策略警告确认）、可访问性（会话进度卡片）和构建工具链**，结合其 beta 阶段暴露的消息丢失、重启恢复缺陷，可判断项目正从功能爆发转向**平台级工程化加固**。相较之下，Hermes 聚焦多网关/多 Profile 桌面端状态隔离，Pi 聚焦终端轻量体验，LiteLLM 聚焦 API 网关；OpenClaw 更接近面向最终用户与管理员的**全功能助手平台**，在生态中处于核心参照位置。

---

### 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **更新/升级可靠性** | OpenClaw、Hermes | OpenClaw 存在重启恢复缺陷；Hermes 出现 update 后服务停留在陈旧代码、macOS launchd 网关更新后 exit 75 等问题。“更新即坏”严重影响信任。 |
| **跨平台/Windows 支持** | Hermes、Pi | Hermes 有 Windows 大小写碰撞、更新器误杀实例、MCP stdio 崩溃；Pi 社区有大量 Windows 使用问题讨论。 |
| **多 provider/模型兼容性** | Hermes、Pi、LiteLLM | Hermes 遇到 xAI 保留函数名、Gemini JSON 拼接；Pi 遇到 Gemini thought_signature 缺失、OpenRouter reasoning 控制、Bedrock 图片处理；LiteLLM 本身即为多 provider 网关。 |
| **会话持久化与上下文管理** | OpenClaw、Hermes、Pi | OpenClaw 消息丢失；Hermes 的 Pluggable SessionDB 呼声高、SQLite 并发问题导致子代理死亡；Pi 的 auto-compaction 不触发直到上下文溢出。 |
| **工具调用健壮性** | Hermes、Pi、LiteLLM | Hermes MCP stdio 全面快速失败；Pi Claude edit 工具约 20% 失败；LiteLLM 涉及 Claude 消息处理。 |
| **安全与治理** | OpenClaw、LiteLLM | OpenClaw 安装策略警告需确认；LiteLLM 持续推进 Guardrails 安全层。 |

---

### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|---|---|---|---|
| **OpenClaw** | 完整助手生命周期：安装、UI、安全策略、可访问性 | 普通用户 / 管理员 | CLI + Control UI，集中式平台，当前 beta 重点在可靠性 |
| **Hermes Agent** | 多网关/多 Profile 桌面端、消息通道集成（Telegram/WeCom/微信/QQ） | 重度自

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

## Hermes Agent 项目动态日报 — 2026-08-26

### 1. 今日速览
过去 24 小时项目活跃度处于**高位**：共产生 388 条 Issue 更新与 500 条 PR 更新，其中新开/活跃 Issue 332 条、待合并 PR 425 条，显示社区贡献意愿强烈。然而**新版本发布为 0**，且 24 小时内关闭 Issue 仅 56 条（占 14%），合并/关闭 PR 仅 75 条（占 15%），合并吞吐量明显低于提交速度，维护者审阅带宽可能成为瓶颈。值得关注的是，一批来自 @teknium1 的「multi-gateway」系列 fix PR 集中提交，围绕桌面端多网关状态串扰问题展开系统性修复；同时多个 P1 级 Bug（MCP stdio 崩溃、子代理会话静默死亡、xAI 保留函数名冲突）在近两日集中爆发，需要项目维护团队优先响应。

### 2. 版本发布
过去 24 小时内无新版本发布（Releases: 0 个）。

### 3. 项目进展
今日无已合并 PR 的详细记录（最新 PR 列表中全部为 Open 或 Closed 未合并状态），但从 PR 提交趋势可看出项目正在以下方向快速推进：

- **多网关/多 Profile 桌面端状态隔离**：@teknium1 今日密集提交了至少 6 个相关 PR（[#95080](https://github.com/NousResearch/hermes-agent/pull/95080)、[#95081](https://github.com/NousResearch/hermes-agent/pull/95081)、[#95082](https://github.com/NousResearch/hermes-agent/pull/95082)、[#95085](https://github.com/NousResearch/hermes-agent/pull/95085)、[#95087](https://github.com/NousResearch/hermes-agent/pull/95087)），分别修复网关切换时的路由身份泄漏、存储资源在错误网关上执行、二级网关发布虚假 socket、认证信封跨连接串扰等问题。这一系列 PR 指向一个统一的追踪 Issue（#94724），是当前桌面端最系统的架构修补。
- **安装/更新可靠性专项修复**：@teknium1 还提交了 macOS TCC 权限跨更新保留（[#95091](https://github.com/NousResearch/hermes-agent/pull/95091)）和 Windows 更新器误杀其他安装实例（[#95086](https://github.com/NousResearch/hermes-agent/pull/95086)）两个修复，分别salvage自 #77189 与 #92246，说明旧问题正在被重新激活处理。
- **配置系统补全**：[#95095](https://github.com/NousResearch/hermes-agent/pull/95095) 修复 `agent.reasoning_effort` 虽被运行时消费但未列入 `DEFAULT_CONFIG` 导致校验失败的问题；[#95092](https://github.com/NousResearch/hermes-agent/pull/95092) 修复从命名 profile 启动的 dashboard 无法被 `--status`/`--stop` 检测的问题。
- **新平台适配持续进行**：[#84202](https://github.com/NousResearch/hermes-agent/pull/84202)（OneBot 11 QQ 适配器）与 [#65982](https://github.com/NousResearch/hermes-agent/pull/65982)（claude-agent-sdk provider）仍保持更新，虽非今日新开，但持续活跃。

整体而言，项目正处在**桌面端多网关架构加固**与**跨平台更新链路修复**的关键阶段，这些工作直接回应了近期密集出现的 update/restart/session 类 Bug。

### 4. 社区热点
- **[#66616 Skills index is stale or degraded](https://github.com/NousResearch/hermes-agent/issues/66616)（96 条评论）**
  自动化巡检探针报告 Skills Hub 索引已 29.8 小时未刷新（限制 26 小时），状态为 `degraded`。该 Issue 由机器人创建（@nousbot-eng），评论数极高说明团队在索引构建工作流（skills-index.yml cron 调度）问题上进行了大量调试讨论。这属于**基础设施健康度**问题，虽非用户直接可见，但会阻塞技能文档与工具调用的同步。

- **[#88584 Automated Nous integration is blocked](https://github.com/NousResearch/hermes-agent/issues/88584)（30 条评论）**
  自动化的 Nous-to-Enterkey 合并流程在 `cron/jobs.py` 产生冲突，导致 dashboard updater 停留在此前测试版本上。**上游集成管道阻塞**已持续 8 天，评论活跃但未关闭，需要维护者手动介入解决合并冲突。

- **[#13834 Hermes openai-codex fails while official Codex CLI works](https://github.com/NousResearch/hermes-agent/issues/13834)（21 条评论，👍 4）**
  同一台 macOS 机器、同一网络下，官方 `codex` CLI 可以正常完成 ChatGPT 登录与模型响应，但 Hermes 配置 `openai-codex` 后反复失败。该问题自 4 月持续至今仍为 Open，评论数持续增长但无修复 PR 关联，是 **provider 兼容性的长期痛点**。

- **[#23717 RFC: Pluggable SessionDB Provider](https://github.com/NousResearch/hermes-agent/issues/23717)（19 条评论，👍 8）**
  要求将 session 存储从 SQLite 扩展为可插拔的 PostgreSQL/MySQL 等 provider，核心动机是「热更新死亡螺旋」——运行时 `git pull`/`hermes update` 导致共享 SQLite 文件损坏。这是今日评论最多、👍 数最高的功能 RFC，说明**会话存储架构升级**是社区强烈诉求。

- **PR 侧热点**：今日评论数最多的 PR 均显示为 `undefined`（数据缺失），但结合 Issue 热度与 PR 内容判断，[#65982 claude-agent-sdk provider](https://github.com/NousResearch/hermes-agent/pull/65982)（带 7 个 sweeper 风险标签、持续 40 天未合并）仍是最受关注的长期 PR，涉及订阅 OAuth 计费安全边界，维护者显然在谨慎评估。

### 5. Bug 与稳定性
按严重程度排列：

**P1 级（严重）**
- **[#94637 MCP stdio 工具调用全部快速失败](https://github.com/NousResearch/hermes-agent/issues/94637)** — Windows 11 上所有 stdio 传输的 MCP server（ADO、GBrain、chrome-devtools）在 #85125 之后均报 `subprocess has exited`。影响所有依赖 stdio MCP 的 Windows 用户，标记为 duplicate 但仍在接收评论。**已有回归嫌疑**，需排查 #85125 的 subprocess 生命周期改动。
- **[#94736 子代理/Cron 会话静默死亡](https://github.com/NousResearch/hermes-agent/issues/94736)** — `delegate_task` 和 cron 任务间歇性因 `Session DB append_message failed: 'NoneType' object has no attribute 'execute'` 强制结束，即使还有工具调用预算。影响自动化任务可靠性，**与 #23717 的 SQLite 并发问题可能同源**。
- **[#95003 xAI 拒绝 tool_search 函数名](https://github.com/NousResearch/hermes-agent/issues/95003)**（👍 6）— xAI API 将 `tool_search` 视为保留函数名，导致所有启用 Tool Search 的 grok-4.6 请求返回 400。**Hermes 的 Tool Search 功能在 xAI 上完全不可用**，需要为 xAI provider 增加函数名映射/过滤逻辑。
- **[#92145 hermes update 后服务停留在陈旧 sys.modules](https://github.com/NousResearch/hermes-agent/issues/92145)** — 自动重启阶段若抛出 ImportError，更新流程会提前中止，但已在运行的 gateway/serve 进程仍持有旧代码模块，造成运行中服务与磁盘代码不一致。这是 update 可靠性的又一致命缺陷。

**P2 级（中等）**
- **[#93888 Desktop 发送本地 runtime ID 给远程网关导致会话无法恢复](https://github.com/NousResearch/hermes-agent/issues/93888)** — 远程网关会话恢复时收到 8 字符本地临时 session ID，永久卡在 "Restore failed"。
- **[#94540 macOS launchd 网关 update 后 exit 75 且不再重生](https://github.com/NousResearch/hermes-agent/issues/94540)** — 7 个 profile 的网关服务全部退出且 `KeepAlive` 失效。
- **[#72488 Gemini 3.5 Flash 将多个 JSON 对象拼接为单个 tool_call](https://github.com/NousResearch/hermes-agent/issues/72488)** — 模型有时在单个 tool_call 的 arguments 中塞入 N 个 JSON 对象，需要解析层做容错。
- **[#87697 Hermes 客户端约 1.5s 后取消本地 LLM 流](https://github.com/NousResearch/hermes-agent/issues/87697)** — 触发 `<unused49>` token 循环，影响 Ollama 后端用户。
- **[#94146 微信 live 回复在限流后静默丢弃](https://github.com/NousResearch/hermes-agent/issues/94146)** — 即使重新扫码登录、使用最新 main 仍复现，通道变为「只能收不能发」。

**P3 级（低严重度但影响面广）**
- **[#88168 Windows 下 contributors/emails 大小写碰撞导致 git status 永久 dirty](https://github.com/NousResearch/hermes-agent/issues/88168)**（👍 2）— 经典 Windows 大小写不敏感文件系统问题，需仓库层面重命名文件。
- **[#72716 optimize-storage 在中断的 demote 后写入空 FTS 索引](https://github.com/NousResearch/hermes-agent/issues/72716)** — 导致历史消息全文搜索永久丢失。
- **[#62169 Terminal 沙箱删除 CWD 后所有命令 exit 126](https://github.com/NousResearch/hermes-agent/issues/62169)** — 会话 CWD 被外部删除后无法恢复。

**今日 fix PR 覆盖情况**：上述 P1 级 Bug 尚未看到一对一 fix PR；@teknium1 的 multi-gateway 系列主要指向桌面端会话/网关串扰类问题，[#95093](https://github.com/NousResearch/hermes-agent/pull/95093) 修复 terminal 工具嵌套进程的 `TERMINAL_CWD` 陈旧问题，[#95083](https://github.com/NousResearch/hermes-agent/pull/95083) 修复 secondary profile 首次 adapter 连接失败后不再重连的问题。

### 6. 功能请求与路线图信号
- **Pluggable SessionDB（[#23717](https://github.com/NousResearch/hermes-agent/issues/23717)）** — 评论 19 条、👍 8，是当前呼声最高的架构级 RFC。`#94736` 的会话静默死亡和 `#93888` 的会话恢复失败都指向 SQLite 共享状态的问题，**PostgreSQL/MySQL provider 很可能进入下个里程碑**。
- **Bot Mode 群聊接入 Web Dashboard（[#89995](https://github.com/NousResearch/hermes-agent/issues/89995)）** — 目前 Bot Mode 群聊仅限 Electron 桌面端，web dashboard 只有 1:1 聊天。结合 [#91911](https://github.com/NousResearch/hermes-agent/issues/91911)（Bot Mode 控制平面架构）可看出社区希望将 Bot 能力从桌面端解放到 Web/网关层。
- **Voice mode 网页端 WebRTC 音频采集（[#20765](https://github.com/NousResearch/hermes-agent/issues/20765)）**（👍 6）— 远程 SSH/PTY 场景下无法使用语音功能，适合通过浏览器 WebRTC 解决。
- **Autoresearch skill（[#5114](https://github.com/NousResearch/hermes-agent/issues/5114)）** — 要求代理以 git 实验循环方式做 ML 优化，每次改动记录效果，避免盲目覆写文件。目前仅 8 条评论，但概念新颖，属于「代理自主研究」方向的早期信号。
- **Model pinning（[#95090](https://github.com/NousResearch/hermes-agent/pull/95090)）** — 今日新 PR，将常用 provider/model 钉在桌面端模型菜单顶部。小型 UX 改进，**大概率会合入下个版本**。
- **OneBot 11 QQ 适配器（[#84202](https://github.com/NousResearch/hermes-agent/pull/84202)）** — 持续活跃 14 天，如合入将新增 QQ 个人号接入能力，区别于官方 QQ Bot 平台。目前无评论数据，但功能完整度高，值得关注。

### 7. 用户反馈摘要
- **「更新即坏」成为最大信任危机**：多个 P1 级 Bug（#94637、#94736）与大量 P2 更新链路问题（#94540、#92145、#92095、#74973）表明用户对 `hermes update` 的可靠性已产生明显不满。尤其是 macOS launchd 网关在 update 后 exit 75 且不再重生（#94540），直接导致 Telegram/WeCom 等消息通道完全中断，影响生产可用性。用户在 #92095 中反馈点击桌面图标**静默失败**（`Terminal=false` 隐藏了错误），这种「看似成功实则未运行」的体验会进一步削弱信任。
- **Windows 平台体验持续拖后腿**：大小写碰撞导致 git 状态永久 dirty（#88168）、MCP stdio 全面崩溃（#94637）、uv 安装的 .desktop 指向错误解释器（#92095）、更新器误杀所有 hermes.exe（#95086 修复目标）——Windows 用户在多条 Issue 中表达沮丧情绪，但值得肯定的是今日 #95086 已针对性修复「只杀本安装实例的 exe」。
- **本地模型 / 私有部署用户受影响明显**：Ollama 流式响应被客户端 1.5s 超时取消（#87697）、xAI 保留函数名冲突（#95003）、Bailian/DashScope 无 `/v1/models`（#12220）——非 OpenAI 官方渠道的兼容性问题密集出现，说明 Hermes 用户群体中有大量使用替代/本地模型的开发者，他们对 provider 适配层的容错性有较高期待。
- **正面反馈信号**：官方 codex CLI 正常但 Hermes 的 openai-codex 失败（#13834）虽然是个 Bug，但从侧面说明用户认可 Hermes 作为多 provider 聚合入口的价值——他们期望 Hermes 能做 Codex 能做的事，这种「以 Hermes 为主、官方 CLI 为辅」的使用习惯是项目黏性的体现。

### 8. 待处理积压
- **[#13834 Hermes openai-codex 在官方 CLI 可用的机器上失败](https://github.com/NousResearch/hermes-agent/issues/13834)** — 已开放 126 天，21 条评论，👍 4，无 fix PR。属于核心 agent 功能的 provider 兼容性问题，长期未解决可能流失用户。
- **[#23717 RFC: Pluggable SessionDB（PostgreSQL/MySQL）](https://github.com/NousResearch/hermes-agent/issues/23717)** — 已开放 107 天，19 条评论，👍 8，`needs-decision` 标签打了一个多月。这是架构级决策，长期悬而未决会持续积累「SQLite 不够用」类的重复 Issue（#94736 便是一例）。
- **[#20765 Voice mode 网页端 WebRTC](https://github.com/NousResearch/hermes-agent/issues/20765)** — 已开放 112 天，👍 6，多个相关 Voice PR 仍处于 Open（如 #30702），语音功能从桌面/TUI 走向 Web 的进展缓慢。
- **[#65982 claude-agent-sdk provider PR](https://github.com/NousResearch/hermes-agent/pull/65982)** — 待合并 41 天，带有 `needs-decision` 与 7 个 sweeper 风险标签，是 Anthropic 订阅用户的核心诉求（避免按量计费）。长期不合并会迫使相关用户停留在 fork 或手动 patch。
- **[#5114 Autoresearch skill](https://github.com/NousResearch/hermes-agent/issues/5114)** — 已开放 144 天，仅 8 条评论，无维护者回应。属于「创新性功能」类别，目前看优先级低，但长期无人认领会让提出者失去贡献动力。
- 此外，**[#66616 Skill index 持续 degraded](https://github.com/NousResearch/hermes-agent/issues/66616)** 的 96 条评论足以说明索引构建工作流长期不稳定，这属于项目自营基础设施，维护者应优先修复 cron/构建链路，避免文档与工具索引持续落后。

---
**今日整体判断**：项目社区活跃度高、PR 提交密集，说明贡献者愿意投入；但合并速度（75/500）与 Issue 关闭速度（56/388）远低于流入速度，积压压力正在上升。桌面端 multi-gateway 系列 PR 是今日最大的「系统性修复信号」，值得优先 review；P1 级 Bug 集中在 MCP 回归、会话持久化与 xAI 兼容性，建议维护团队按「影响面 × 用户量」排序，优先处理 #94637 与 #94736。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-26

## 今日速览

过去 24 小时 Pi 项目保持着非常高的活跃度：共产生 **227 条 Issue 更新**（其中新开/活跃 17 条，关闭 210 条，关闭/清理效率极高）与 **33 条 PR 更新**（25 条已合并/关闭，8 条待合并，合并率约 76%）。今日无新版本发布。社区讨论焦点集中在 Windows 平台支持（#7547，49 条评论）、Claude 模型 edit 工具兼容性（#6278）、auto-compaction 触发机制（#6879，19 👍）以及 TUI 渲染稳定性（#8584）等方向。项目整体健康度良好：大量 Issue 被快速关闭验证了维护者对社区反馈的响应能力，但部分核心稳定性问题（如上下文压缩、Gemini 3.x 工具调用）仍处于长期开放状态，需持续关注。

---

## 版本发布

今日无新版本发布。上一个版本仍为 v0.84.x 系列（最新为 v0.84.3，已在多个 Issue 中被引用）。相关功能与修复预计在下一版本中集中释放。

---

## 项目进展

今日合并/关闭的 25 个 PR 中，除 4 个无效/占位 PR（#8634、#8632、#8232、#8608）外，其余均包含实质性的功能推进或缺陷修复：

**新功能 / 能力扩展**
- **eager tool execution（PR #8629）**：新增 opt-in 的「急切工具执行」机制，在 `toolcall_end` 时就启动本地 `read` 调用，正常调度时直接复用结果，可显著降低工具调用延迟。属于对编码代理性能的基础性优化。
- **新增 Opper provider（PR #8639）**：将 Opper 作为内置 OpenAI 兼容 provider 加入（`OPPER_API_KEY`），包含 provider 模块、models.dev 模型目录、默认模型与文档。延续了 Pi 快速跟进新模型服务商的节奏。
- **TUI 鼠标点击移动光标（PR #8547，待合并）**：支持在主提示词输入区点击移动光标，改善鼠标启用的终端下的编辑体验。

**关键修复**
- **OpenRouter reasoning 控制推导（PR #8614）**：修复了 `stealth/ox-alpha` 等 reasoning-mandatory 模型在未传 reasoning 时，adapter 主动发送 `reasoning:{effort:"none"}` 导致 HTTP 400 的问题。对应 Issue #8454。
- **Responses API `tool_choice` 省略（PR #8633、PR #8650）**：当请求中无 tools 时不再发送 `tool_choice`，修复 Grok/OpenAI Responses 在 `/compact` 与 overflow compaction 时的 400 错误。
- **Bedrock 上 OpenAI 模型的工具结果图片处理（PR #8642）**：将嵌套在 `toolResult.content` 中的图片提升为同一条 user message 的兄弟 content block，避免 OpenAI models on Bedrock 拒绝会话。
- **保留 Codex 线程亲和性 headers（PR #8570）**：为 OpenAI Codex Responses 请求补充 `thread-id` 头，与已有的 `session-id`/`prompt_cache_key` 配合，提升多请求间的缓存命中。
- **read 工具行数统计修复（PR #8623）**：去除因 `split("\n")` 产生的幻影末尾元素，修正截断提示、续读提示中的行数偏差（Fixes #7329）。
- **扩展工具使用 `ctx.cwd`（PR #8627）**：`read`/`write`/`edit`/`grep` 等 cwd 敏感的工具在扩展场景下优先使用 ExtensionContext 中的真实会话 cwd。
- **bash 可用时加载 skills（PR #8641）**：即使 `read` 不可用、仅 `bash` 存在时也加载 skills 部分，并调整引导文案（Fixes #8551）。

**今日合并的 PR 数量较大，项目在跨 provider 兼容性、上下文窗口边界处理、工具执行性能与 TUI 体验四个维度均有实质推进。**

---

## 社区热点

**#7547 [Windows] 如何使用 Pi？你遇到了哪些问题？（49 条评论，2 👍）**
https://github.com/earendil-works/pi/issues/7547
由 @petrroll 发起的讨论型 Issue，试图系统性收集 Windows 上运行 Pi 的各种方式与痛点，为官方决定「核心支持 vs 外置扩展」提供输入。49 条评论说明 Windows 开发者群体基数大、反馈强烈，是当前社区最关注的方向。

**#6278 [Claude 新模型 edit 工具 20% 失败率]（24 条评论，10 👍，已关闭）**
https://github.com/earendil-works/pi/issues/6278
Claude 新模型在 `edit` 工具中生成模型幻觉的额外 key（如 `new_text_x`、`type`、`closeenough`），导致约 20% 的编辑操作因 `Validation failed for tool "edit"` 失败。该 Issue 以 10 👍 位居住期高赞列表前列，最终关闭，但摘要中未说明具体处理方式（可能已通过 schema 放宽或模型适配解决）。

**#6879 [auto-compaction 从不触发直到 provider 溢出]（23 条评论，19 👍）**
https://github.com/earendil-works/pi/issues/6879
用户在使用 gpt-5.6-sol 时，单次 agentic turn 运行超 2 小时，footer 越过压缩阈值后继续增长至 >100% 上下文窗口，直到 API 在 373k tokens 时拒绝请求。问题指出：压缩检查应在每个 agentic 子步骤后执行，而非仅在 turn 结束时。19 👍 表明该问题触及大量长会话用户的共同痛点。

**#8584 [TUI 行损坏：长工具输出后助手文本逐词换行]（8 条评论，5 👍，已关闭）**
https://github.com/earendil-works/pi/issues/8584
在 `sed -n 515,545p` 这类输出长行的工具调用后，助手文本流式渲染出现「每行一个单词」的乱序现象，高概率复现。已在新版本中修复关闭，但用户对 TUI 渲染稳定性的关注度较高。

---

## Bug 与稳定性

按严重程度排列（含是否已有修复 PR 标注）：

**P0 / 会话中断或数据风险**

- **[OPEN] #6879 auto-compaction 永不触发直到 provider 溢出**（19 👍，开放超一个月）
  https://github.com/earendil-works/pi/issues/6879
  长时 agentic turn 可耗尽整个上下文窗口并被 API 拒绝。无对应修复 PR，但 #8464 也提出相同的「turn 间压缩检查」诉求，已关闭。

- **[OPEN] #8166 DeepSeek 400：自定义消息打断 tool_calls→tool 邻接**（8 条评论）
  https://github.com/earendil-works/pi/issues/8166
  扩展在工具批次中间调用 `pi.sendMessage({ triggerTurn: false })`，导致后续每一轮都报 `Messages with role 'tool' must be a response to a preceding message with 'tool_calls'`。会话完全不可用。无修复 PR。

- **[OPEN] #6996 Gemini 3.x 工具调用失败：缺失 `thought_signature`**（6 条评论）
  https://github.com/earendil-works/pi/issues/6996
  Gemini 3.x 模型在触发工具调用后，提交 tool result 时因历史中缺少 `thought_signature` 而失败。无修复 PR。

- **[CLOSED] #7855 响应截断：「Response was truncated before completion.」**
  https://github.com/earendil-works/pi/issues/7855
  工作过程中随机出现红色提示「响应在完成前被截断」，需手动 `continue`。在任意 OpenAI-compatible API 上复现。已关闭但未说明修复方案。

**P1 / 功能异常或回归**

- **[CLOSED] #8409 中止的 turn 以 `stopReason: "error"` 而非 `"aborted"` 结束（回归）**
  https://github.com/earendil-works/pi/issues/8409

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目日报 — 2026-08-26

## 今日速览

项目活跃度处于**高位**：24小时内Issue更新94条（新开/活跃62，关闭32），PR更新264条（待合并172，合并/关闭92），代码合入与问题修复节奏均维持高速运转。今日无新版本发布，但大量PR处于待合并状态，暗示v1.99.x后续版本正在密集开发中。社区讨论热度集中于预算误报、Claude模型消息处理、Helm部署体验与身份联邦认证（Workload Identity Federation）等话题。Bug修复与功能开发并重，项目健康度整体良好，但部分长期未关闭的技术债（Redis兼容性、OpenAI流式协议合规）值得关注。

## 版本发布

今日无新版本发布。

## 项目进展

过去24小时内有92条PR被合并/关闭，代码库迭代频繁。从展示的PR样本看，今日合并的关键功能为：

- **Bing Grounding 搜索提供者**（#38119，已合并）：为 Foundry Responses API 新增 `bing_grounding` 搜索提供者，支持 `/v1/search` 与聊天 websearch 拦截，补全了搜索供应商矩阵。[PR链接](https://github.com/BerriAI/litellm/pull/38119)

持续活跃、更新至今日的PR显示项目在**性能优化、可观测性、Guardrails 安全层**三个方向有明确进展：

- **流式性能优化**（#36610）：新增共享 `JSONFragmentAccumulator`，解决 Vertex 和 Anthropic 流

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*