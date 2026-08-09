# AI CLI 工具社区动态日报 2026-08-10

> 生成时间: 2026-08-09 22:36 UTC | 覆盖工具: 7 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比



---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告
**数据范围：** github.com/anthropics/skills | **截止：** 2026-08-10

---

## 一、热门 Skills 排行（按评论数，Top 8）

---

# Claude Code 社区动态日报（2026-08-10）

## 今日速览

今日无新版本发布，社区讨论集中在两个新开放的 Bug：工具调用解析器静默数据丢失（#84362）与 Plan 模式非预期退出（#85095）。与此同时，安全策略误报（ClAudit / cyber / AUP 系列）仍是最大争议点，开发者集中反馈合法云 IAM 管理任务被误拦截。PR 方面共有 3 条更新，其中 plugin-dev 的 YAML 块标量解析修复值得关注。

---

## 社区热点 Issues

以下 10 个 Issue 综合了开放状态、评论热度与影响面，最值得开发者关注：

### 1. Tag-grammar 解析器静默吞掉参数块 —— 数据完整性风险
**#84362** [OPEN] · 评论 4 · 👍 0  
当模型输出不匹配的闭合标签时，解析器会把后续参数块吸收进前面的字符串字段，导致调用“成功”但参数静默丢失，测量到 **6.2% 的字段丢失率**。这是对已关闭 Issue #44826 的重新提交。涉及 MCP 调用数据可靠性，建议关注。  
🔗 https://github.com/anthropics/claude-code/issues/84362

### 2. Plan 模式静默退出并误处理 ExitPlanMode
**#85095** [OPEN] · 评论 4 · 👍 0  
新提交的 Bug：Plan 模式在会话中非预期退出，Agent 将构造出的 ExitPlanMode 当作正常信号处理，可能绕过用户的计划审批意图。影响工作流安全性。  
🔗 https://github.com/anthropics/claude-code/issues/85095

### 3. 网络安全护栏误报——常规系统管理命令被阻断
**#61185** [CLOSED] · 评论 17 · 👍 7  
社区讨论热度最高。常规 sysadmin 审计命令和纯写报告被安全机制误拦，且误报导致上下文污染，破坏会话恢复。该 Issue 同时涉及安全策略精度与会话健壮性，是当日最受关注的话题。  
🔗 https://github.com/anthropics/claude-code/issues/61185

### 4. 服务器端流式字节延迟与 180s 超时中断
**#66095** [CLOSED] · 评论 6 · 👍 2  
在 2.1.157 / Opus 4.8 环境下，请求被接受后迟迟不返回字节（慢首字节数十至数百秒），触达客户端 watchdog 导致死循环。涉及核心网络性能，不少用户可能遇到。  
🔗 https://github.com/anthropics/claude-code/issues/66095

### 5. Telegram 插件：入站 MCP 通知未注入对话
**#42138** [CLOSED] · 评论 8 · 👍 1  
通过 Telegram 插件接收到的 `notifications/claude/channel` 消息不会出现在对话上下文中，影响远程协同场景。社区持续关注插件生态成熟度。  
🔗 https://github.com/anthropics/claude-code/issues/42138

### 6. Agent Teams：长会话后 lead 的 active agent 指针错乱
**#64550** [CLOSED] · 评论 5 · 👍 0  
会话压缩后，team-lead 的 “current agent” 指针停留在某个 teammate 上，导致 lead 以 teammate 身份路由，且 Agent 生成报错 “Teammates cannot spawn other teammates”。影响 Agent Teams 在长任务中的可用性。  
🔗 https://github.com/anthropics/claude-code/issues/64550

### 7. Workflow 并发缺少内存感知调节
**#69033** [CLOSED] · 评论 3 · 👍 1  
大量 fan-out 场景（如 deep-research 并发 84–92 个子代理）导致宿主机 OOM、终端崩溃。当前并发上限仅按 CPU 核数计算（`min(16, cores-2)`），未考虑内存水位，建议按内存动态调节。  
🔗 https://github.com/anthropics/claude-code/issues/69033

### 8. --resume 报 “No conversation found”
**#69952** [CLOSED] · 评论 3 · 👍 0  
macOS 上重置账户权限后 `--resume` 失败，但本地会话文件仍完好，说明恢复逻辑与权限状态耦合。对习惯多会话切换的开发者有影响。  
🔗 https://github.com/anthropics/claude-code/issues/69952

### 9. ClAudit 自动模式分类器拒绝授权工作
**#70773** [CLOSED] · 评论 5 · 👍 0  
harness 的 auto-mode 分类器把合法操作判定为高风险并拉起长时守护进程，报告大量“false positive”。该系列误报已成为社区反馈最集中的领域之一。  
🔗 https://github.com/anthropics/claude-code/issues/70773

### 10. 自持云租户 IAM 策略审查被误报为 AUP 违规
**#70808** [CLOSED] · 评论 3 · 👍 1  
对自有云租户做常规 IAM 角色/策略加固被 AUP 拦截，返回通用策略违规。开发者普遍认为安全过滤器基于术语模式匹配，缺乏对授权上下文的判断。  
🔗 https://github.com/anthropics/claude-code/issues/70808

---

## 重要 PR 进展

过去 24 小时共 3 条 PR 更新，集中在插件与技能开发体验的修复：

### 1. fix(plugin-dev)：解析块标量 agent 描述
**#85323** [OPEN] · 创建 2026-08-09  
修复 #83803 遗留的 YAML 块标量解析问题：`validate-agent.sh` 现在能正确度量 `description: |` / `description: >` 的多行缩进内容，而非把标量标记当作完整描述。提升插件元数据校验准确性。  
🔗 https://github.com/anthropics/claude-code/pull/85323

### 2. fix(skills)：插件技能名使用符合规范的形式
**#85243** [OPEN] · 创建 2026-08-09  
8 个内置技能使用了含空格且标题大写的 `name` 字段（如 “Writing Hookify Rules”、“Agent Development”），不符合规范命名。该 PR 统一为 spec 兼容格式，避免解析与引用歧义。  
🔗 https://github.com/anthropics/claude-code/pull/85243

### 3. [Plugin] 新增 agent-session-commit 插件
**#17395** [CLOSED] · 创建 2026-01-10 · 8 月 9 日更新  
以 `AGENTS.md` 为权威指令文件，`CLAUDE.md` 改为指向它的最小入口；通过 `/session-commit` 命令或 Stop hook 自动提示，在会话结束时增量沉淀项目知识。适合团队长期维护上下文。  
🔗 https://github.com/anthropics/claude-code/pull/17395

---

## 功能需求趋势

- **更精准的安全策略引擎**：大量 cyber / AUP / harness 误报反馈表明，社区迫切需要区分“合法管理操作”与“恶意行为”的上下文感知过滤，而非术语模式匹配。
- **Agent 与子代理的资源治理**：从内存感知并发节流到 Agent Teams 长会话状态恢复，开发者希望系统能在高并发、长时间运行下保持稳定。
- **插件 / MCP 生态成熟化**：包括 Telegram 插件通知注入、plugin-dev 工具链的 YAML 解析与命名规范，都是生态从“可用”走向“规范”的信号。
- **核心解析器健壮性**：Tag-grammar 参数静默丢失与 Plan 模式误退出，揭示了内部解析与状态机在边界条件下的缺陷，触发对数据完整性的担忧。

---

## 开发者关注点

- **安全误报是最大痛点**：尤其是 cloud IAM、防御性加固等合法任务被反复误拦，部分用户需要提交大量申诉（如 @sworrl 连发的二十余条 ClAudit 误报），已实质性影响正常开发与运维效率。
- **数据完整性焦虑**：6.2% 的静默参数丢失会让自动化链路在“无报错”情况下产出错误结果，这类缺陷比显式报错更难排查。
- **长会话稳定性不足**：#61185 的上下文中毒、#64550 的 Agent 指针错乱、#69952 的 resume 失败

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-10

## 今日速览

过去 24 小时没有新的版本发布，社区焦点集中在 **Linux 桌面应用长期缺位**（945 👍 排第一）和 **Windows 平台多项严重 bug**（闪烁、Computer Use 失败、远程控制缺失）。底层基础设施的可靠性问题（Crashpad 无限膨胀、SQLite 空间永不回收、会话存储可达数百 GiB）持续引发开发者对长时运行稳定性的担忧。

---

## 社区热点 Issues（Top 10）

### 1. 🔥 Linux 桌面应用请求 — 已获 945 👍 / 205 💬
**#11023** [enhancement, app]  
[Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)

> 作者 @Suhainator 表示，Codex 桌面应用在 macOS 上因上游 bug（#10432）几乎不可用，希望能在 Linux 桌面使用。该 Issue 已持续半年，获得近千点赞，是当前社区最强烈的产品方向诉求。

**值得关注**：Linux 开发者用户体验长期被忽视，这条 Issue 的热度表明官方桌面应用的跨平台支持已是刚需。

---

### 2. ⭐ 可定制状态栏（TUI）— 150 👍 / 39 💬
**#17827** [enhancement, TUI, config]  
[Customizable status line](https://github.com/openai/codex/issues/17827)

> 借鉴 Claude Code 的终端底部状态栏设计，用户希望在 TUI 中通过 shell 脚本自定义展示实时信息（token 用量、模型名、速率限制、上下文窗口、git 分支等）。

**值得关注**：这是 TUI 用户最集中的功能痛点之一，39 条评论中大量用户提供了具体的状态栏配置案例。

---

### 3. ⚠️ Crashpad 转储无限膨胀 — 16 💬
**#25921** [bug, app, performance]  
[Codex Desktop continuously generates Crashpad pending dumps, growing without any limit: +5GB per day](https://github.com/openai/codex/issues/25921)

> `~/Library/Application Support/com.openai.codex/web/Crashpad/pending` 目录一天内增长到 4.9GB / 54,504 个文件，持续占用磁盘。

**值得关注**：属于长时间使用场景下的“隐性磁盘杀手”，对本地 SSD 容量是严重威胁。

---

### 4. 🖥️ Windows Computer Use：窗口发现失败 — 10 💬
**#37383** [bug, windows-os, app, computer-use]  
[Computer Use on Windows fails during app/window discovery with 0x80070003](https://github.com/openai/codex/issues/37383)

> Windows 11 Pro 25H2 上，Computer Use 功能在应用/窗口发现阶段直接报 `0x80070003`（路径不存在）。用户为 Pro x5 订阅用户，说明付费用户已开始在日常环境重度依赖该功能。

**值得关注**：Computer Use 是 Codex 2026 年的重点能力，Windows 端的可用性仍不稳定。

---

### 5. 📱 iOS 无法显示 SSH 远程项目 — 13 💬 / 19 👍
**#23527** [bug, iOS, app, app-server, remote]  
[Codex mobile does not show SSH remote projects from connected Mac host](https://github.com/openai/codex/issues/23527)

> Mac 桌面端已连接 SSH 远程项目，但 ChatGPT 移动端在项目选择器中看不到这些项目。三端（Mac↔SSH↔Mobile）链路在“展示层”断裂。

**值得关注**：远程控制是多端协作的核心场景，该问题阻塞了移动端“随时随地继续工作”的价值主张。

---

### 6. ⏳ 打开聊天固定等待 5 秒 — 6 💬 / 6 👍
**#37398** [bug, app, session, performance]  
[Codex Desktop: opening any unloaded local chat waits ~5 seconds on owner discovery timeout](https://github.com/openai/codex/issues/37398)

> 聊天转录实际恢复仅需 <200ms，但固定的 owner-discovery 超时让每次打开都阻塞 5 秒。

**值得关注**：典型的“非功能性问题但极其影响感知性能”的案例，每次点击聊天都要干等。

---

### 7. 💫 Windows 桌面版持续闪烁 — 5 💬
**#34299** [bug, windows-os, app]  
[Windows Desktop 26.715.31925 continuously flickers on Work page after update](https://github.com/openai/codex/issues/34299)

> 更新到 26.715.31925 后，ChatGPT Desktop 在 Work 页面持续闪烁。另有多条类似报告（#34351，4💬），均来自 Windows 11 用户。

**值得关注**：多个 Windows 版本出现渲染层闪烁问题，疑似 Electron/Chromium 升级引入的回归，影响面较大。

---

### 8. 🔁 macOS 远程控制线程恢复回归 — 4 💬 / 4 👍
**#37403** [bug, app, app-server, remote]  
[[macOS][regression] Desktop cannot resume Remote Control / CLI thread: `already has an active writer`](https://github.com/openai/codex/issues/37403)

> 8 月 7 日更新后，移动端 Remote Control 启动的 CLI 线程无法在桌面端恢复，报错 `already has an active writer`。用户原本的“夜间手机发起 / 白天桌面继续”工作流被打断。

**值得关注**：Regression 出现在核心的远程续跑场景中，直接破坏既有用户工作流。

---

### 9. 📦 SQLite 空间永不回收 — 3 💬
**#35823** [bug, windows-os, app, performance]  
[logs_2.sqlite never reclaims freed pages: auto_vacuum=INCREMENTAL is set but never run](https://github.com/openai/codex/issues/35823)

> 10 天保留策略正常运作，但 `auto_vacuum=INCREMENTAL` 从未触发，导致 `logs_2.sqlite` 文件单调增长，磁盘空间持续被“已删除的数据”占据。

**值得关注**：此问题与 #25921（Crashpad）、#34337（会话存储）叠加，构成桌面端“存储失控三重奏”。

---

### 10. 🔄 自动上下文压缩后陷入恢复循环 — 3 💬 / 2 👍
**#34322** [bug, model-behavior, context, app]  
[Serious auto-compact bug: agent repeatedly enters a resume loop after conversation optimization](https://github.com/openai/codex/issues/34322)

> 自动压缩（conversation optimization）后，Agent 反复进入“恢复”循环，无法稳定继续任务。这对长会话用户是致命的——压缩本身是为了继续，结果反而让会话报废。

**值得关注**：语境管理是 Agent 类产品的核心体验，该 bug 直接影响长任务的可靠性。

---

## 重要 PR 进展（全部 7 条）

### #31817 — models.json 自动更新
[Update models.json](https://github.com/openai/codex/pull/31817) · 由 GitHub Actions 自动更新

> 例行更新模型列表，反映最新的可用模型与路由信息。

---

### #37723 — 会话配置导入失败，报告 I/O 子类型
[Report I/O subtypes for session config import failures](https://github.com/openai/codex/pull/37723) · 已 Closed

> 为 `failed_to_load_session_config` 追加稳定的 `std::io::ErrorKind` 分类（`invalid_data` / `not_found` / `permission_denied`），让配置加载失败更易诊断。

**亮点**：直接从“难排查”到“看一眼就知道原因”，提升了遥测数据的可操作性。

---

### #37709 — 修复 TUI 组合器空白换行问题
[Keep wrapped composer whitespace with following text](https://github.com/openai/codex/pull/37709) · 已 Closed

> 修复 TUI 组合器中溢出的空白字符被单独拆到下一行的问题。使用 grapheme-safe 的换行策略，让断行的 Unicode 空白跟随其后的文本。

**亮点**：小但影响日常输入体验的细节修复，对非英文输入尤其友好。

---

### #37654 — exec-server 广播环境配置读取能力
[Advertise environment config read support](https://github.com/openai/codex/pull/37654) · 已 Closed

> 为 exec-server 增加 `environmentConfigRead` 能力声明，本地执行器默认开启；旧执行器反序列化时回退为 `false`。

**亮点**：能力协商机制的补全，为后续环境配置相关功能铺路，且保持了向后兼容。

---

### #37645 — 插件安装失败分析优化
[Improve plugin install failure analytics](https://github.com/openai/codex/pull/37645) · 已 Closed

> 为远程目录、变更、bundle 下载等失败场景新增 HTTP 状态子类型，用稳定的低基数维度替代原始错误消息，便于归因。

**亮点**：在插件生态扩展期，这一步对识别“网络问题 vs. 目录问题 vs. 包问题”至关重要。

---

### #37644 — Hook 处理器执行泛化
[Generalize hook handler execution](https://github.com/openai/codex/pull/37644) · 已 Closed

> 重构为按 handler 类型路由执行，保留原命令 hook 行为；同时拒绝 MCP 工具输入中无法用 TOML 表达的值（如 `null`）参与信任哈希。

**亮点**：为 hook 体系扩展新 handler 类型铺路，同时堵住了信任哈希的一个边角漏洞。

---

### #37641 — 命令审批前缀规则改用步骤上下文
[Use the step context for command approval prefix rules](https://github.com/openai/codex/pull/37641) · 已 Closed

> 选择 exec 策略时，改从当前活动步骤上下文中读取 `allow_prefix_rules`，使审批前缀规则绑定到正确的执行上下文。

**亮点**：修复了多步骤/并行场景下审批规则可能“张冠李戴”的隐患。

---

## 功能需求趋势

从全部 Issues 中提炼，社区关注的功能方向按热度排序：

1. **Linux 桌面应用**（#11023，945 👍）— 一骑绝尘，桌面端的跨平台支持是最大缺口。
2. **TUI 可定制性**（#17827、#10562、#13466、#36711）— 状态栏自定义、禁用幽灵建议、占位符可配置、嵌入 micro 编辑器，终端用户体验精细化是持续的诉求。
3. **多端远程协作**（#23527、#30899、#30372、#37403）— Mac/Windows/移动三端的配对与项目同步仍有多处断裂，Windows 端配对入口缺失尤为突出。
4. **自动化任务可靠性**（#24327）— 用户要求离线期间错过的自动化任务支持补跑（catch-up），这是自动化从“玩具”走向“生产力”的关键。
5. **专属 AI 角色体系**（#37736）— 社区开始提出“My AI Team”这类持久化命名角色的概念，表明用户不满足于通用 Agent，希望有可复用的角色化工作流。

---

## 开发者关注点

**1. Windows 平台是重灾区**
- 桌面应用闪烁（#34299、#34351、#35101 同样波及 macOS）
- Computer Use 窗口控制失败（#37383、#37281）
- 远程控制无法启动（#30372）
- `/agent` 命令导致终端冻结（#36505）

Windows 上的高频 bug 报告已明显超过 macOS，建议官方加大对 Win11 的 CI 覆盖。

**2. 长时间运行后存储失控**
- Crashpad 转储 +5GB/天（#25921）
- SQLite 文件永不回收（#35823）
- 会话 rollout 存储可达数百 GiB（#34337）

这类问题短时间不易暴露，但一旦触达磁盘上限就会“突然致命”。开发者呼吁引入存储上限和主动清理策略。

**3. Hook 与审批机制存在信任漏洞**
- 忽略 git worktree 中的项目级 hooks.json（#27133）
- PreToolUse deny 不生效，写入照样执行（#27833）

钩子机制是安全边界的基石，这两条 Issue 若属实，意味着安全策略可以被静默绕过，需要高优先级处理。

**4. 自动压缩（Compact）的可靠性**
- 压缩后 Agent 陷入恢复循环（#34322），让长会话直接“报废”

这属于所有长任务用户都会遇到的问题，压缩本是续命机制，现在反而成了“死亡开关”。

---

*数据截至 2026-08-09 · 来源：[github.com/openai/codex](https://github.com/openai/codex) | 本日报由 AI 自动生成，仅供参考*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

## GitHub Copilot CLI 社区动态日报（2026-08-10）

### 1. 今日速览

今日虽无新版本发布与 PR 合入，但 Issue 区异常活跃，近 24 小时集中涌现了十几条新反馈。**MCP 集成稳定性**成为当前最突出痛点（超时无重试、临时策略误杀用户配置、OAuth 认证失败）；同时 **Claude 模型在企业账号下突然全部不可用**、**并行任务触发限流**、**CPU 占用 100%** 等问题也引发开发者集中关注。

### 2. 版本发布

无新版本 Release。

### 3. 社区热点 Issues

以下为近期最值得关注的 10 个 Issue（含讨论热度、影响面与社区反应）：

1. **允许取消或删除已排队的消息**  
   [#1857](https://github.com/github/copilot-cli/issues/1857) · 👍 26 · 💬 9  
   用户希望能在 agent 忙碌或 `/compact` 期间取消已通过 `Ctrl+Q`/`Ctrl+Enter` 排队的消息。这是目前互动设计上呼声最高的改进项，点赞与评论数均居前列。

2. **`/remote` 在组织仓库上报 `could not resolve repository`**  
   [#2751](https://github.com/github/copilot-cli/issues/2751) · 👍 13 · 💬 8  
   v1.0.28 中针对 GitHub 组织仓库的远程会话无法解析仓库。影响企业用户使用远程开发能力，讨论热度持续上升。

3. **`sessionStart` Hook 不触发**  
   [#1730](https://github.com/github/copilot-cli/issues/1730) · 💬 7  
   在 v0.0.420（Windows 11/PowerShell 7）下 `.github/hooks/*.json` 定义的 `sessionStart` 钩子不执行，影响插件生态的可靠性。该问题已存在数月，开发者期待官方修复。

4. **MCP 初始化握手固定 60 秒超时且无重试**  
   [#4421](https://github.com/github/c

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 | 2026-08-10

## 今日速览

今日无新版本发布，社区动态集中在两个方向：一条持续近半年的 **Memory System（跨会话持久上下文）功能需求**（#1283）仍为讨论热点；另一条新提交的 **ACP 流式响应静默挂死 bug**（#2598）以详尽的技术分析引发对协议健壮性与数据落盘完整性的关注。PR 方面，仅一条来自社区的 Google GenAI/MCP 工具参数兼容性修复（#739）在等待审查。

## 社区热点 Issues

> 数据源在过去 24 小时内更新有限，以下为当前最值得关注的 2 条。

- **#1283 [enhancement] Memory System：跨会话持久上下文**  
  作者 @CatKang | 评论 27 | 创建于 2026-02-27，最近更新 2026-08-09  
  **为什么重要**：该 issue 提出为 Kimi Code CLI 构建一套完整的记忆系统，包括 AI 自动管理的“笔记”与用户手动定义的指令，使工具能在不同会话间记住项目模式与用户偏好。虽然点赞数为 0，但评论数达 27 条，讨论持续约半年，是社区对“长会话持久化”需求最集中的表达，直接关系到 CLI 在多轮真实工作流中的可用性。  
  **链接**：https://github.com/MoonshotAI/kimi-cli/issues/1283

- **#2598 [BUG] ACP/print 流式响应静默挂死：无空闲超时、被顶替轮 partial 不落 wire（0.31.1 只覆盖 Esc 场景）**  
  作者 @ai-agent-workbench | 评论 0 | 创建 2026-08-09，最近更新 2026-08-09  
  **为什么重要**：该 issue 对 kimi CLI 0.34.0 版本（ACP 模式）中的严重可靠性问题做了清晰复盘：流式对话中内容 delta 全部到达后，连接仍挂死，无 `[DONE]`/finish 帧、无超时机制；用户发送下一条消息时，挂死轮被静默顶替，且已流式答复**从未写入 wire.jsonl**（缺少 `content.part` 与 `usage.record`）。这直接影响无人值守/自动化场景的数据可信度，也暴露了 CLI 在优雅退出、空闲超时与协议状态机上的缺口，值得官方优先调查。  
  **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2598

## 重要 PR 进展

> 数据源在过去 24 小时内更新有限，以下为当前最值得关注的 1 条。

- **#739 fix(kosong)：从 Google GenAI 工具参数中剥离 JSON Schema 元数据**  
  作者 @xiaoju111a | 创建于 2026-01-28，最近更新 2026-08-09  
  **功能/修复内容**：修复 Google GenAI provider 与 MCP 工具之间的兼容性问题。当 MCP 工具（如 Exa MCP）带有标准 JSON Schema 元数据字段时，Google GenAI 会报验证错误。该 PR 通过剥离或转换这些元数据，使工具箱能正常接入 Google GenAI 后端。  
  **链接**：https://github.com/MoonshotAI/kimi-cli/pull/739

## 功能需求趋势

基于近期 issue 更新，社区最关注的功能方向包括：

1. **跨会话记忆 / 上下文持久化**（#1283）——期望 CLI 能自动记录或由用户维护长期上下文，避免每次会话“从零开始”。
2. **ACP/print 流式协议健壮性**（#2598）——对流式请求的最终完成帧、空闲超时、错误恢复与 wire.jsonl 落盘语义有更高要求，尤其是面向工作流自动化的场景。
3. **多提供商工具兼容性**（PR #739）——MCP 工具生态与 Google GenAI 等不同 provider 的参数格式适配，是社区持续关注的操作层痛点。

## 开发者关注点

从近期反馈中提炼出的高频痛点：

- **流式请求无超时保护**：`config.toml` 中缺少流式空闲超时可配置项，导致断连或服务端不发送终止帧时无限阻塞。
- **数据可追溯性不足**：被顶替轮次的已生成内容不落 wire.jsonl，给调试、审计与计费追溯带来困难。
- **跨会话上下文割裂**：用户希望对项目约定、常用参数等进行长期记忆，减少重复输入。
- **MCP 工具接入门槛**：不同模型后端对 JSON Schema 的兼容性差异，导致同一个 MCP 工具在不同 provider 下出现验证错误。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-08-10）

## 今日速览

今日社区围绕 **多智能体协调**、**会话架构统一** 与 **MCP 集成稳定性** 展开深度讨论：两个重量级 RFC 分别提出独立会话原生协调机制和 Turn-based SessionRuntime 统一方案；MCP Streamable HTTP 的兼容性 Bug 引发关注。同时，CI/E2E 测试稳定性问题依然突出，多个自动生成的失败 Issue 持续占据榜单，项目维护者正在通过引入 watchdog 与微 diff 超时机制来缓解 sandbox 挂起和自动修复效率问题。

---

## 社区热点 Issues（10 条）

### 1. RFC: Native coordination for independent Qwen sessions
**#8718** | P2 · 多智能体 · 讨论中 | 8 条评论

由 @yiliang114 提出的实验性多会话协调方案：允许一个 leader 会话在保持交互的同时，派发 2-3 个独立 worker，并能观察任务运行时状态、收集结构化结果。这是 Qwen Code 在多智能体协作方向上的重要架构探索，社区讨论热度较高。

🔗 https://github.com/QwenLM/qwen-code/issues/8718

### 2. Streamable HTTP: optional GET/SSE stream rejected with 404 kills the whole MCP connection
**#8784** | P2 · MCP · 新增 | 5 条评论

严重的 MCP 兼容性缺陷：Qwen Code 客户端在完成 POST 握手后，会额外探测可选的服务端推送流（GET + SSE）。若服务端按 MCP 规范返回 404，整个 MCP 连接反而被终止。对广泛使用的 Streamable HTTP 传输方式构成实际风险，社区反馈积极。

🔗 https://github.com/QwenLM/qwen-code/issues/8784

### 3. fix(serve): Preserve the current session when a large restore times out
**#8678** | P1 · 会话管理 · 讨论中 | 2 条评论

大型会话恢复超时时，当前会话可能被意外丢弃。P1 优先级的核心 Bug，PR1（#8691）已合并实现了超时契约与可观测性，本 Issue 持续跟踪剩余修复。对大规模开发者工作流影响显著，建议关注后续进展。

🔗 https://github.com/QwenLM/qwen-code/issues/8678

### 4. Proposal: rebuild /review Step 3–5 orchestration on the workflow engine
**#8769** | P2 · 工作流引擎 · 讨论中 | 4 条评论

@wenshao 提议将 `/review` 技能的智能体扇出、验证、反向审计从模型驱动改为工作流引擎驱动，使编排逻辑变为确定性代码。延续近期对 Workflow 编排层（#8690）的关注，体现了社区对「可预期、可调试」流程的强烈需求。

🔗 https://github.com/QwenLM/qwen-code/issues/8769

### 5. Proposal: unify the session reasoning loops on a Turn-based SessionRuntime
**#8775** | P2 · 核心架构 · 讨论中 | 2 条评论

直击架构重复痛点：TUI、headless、ACP Session、serve 分发、AgentCore 各自独立实现了「发送提示 → 流事件 → 工具分发 → 循环」的推理循环。提议统一为 Turn-based SessionRuntime，是当前最具影响力的架构重构方向之一。

🔗 https://github.com/QwenLM/qwen-code/issues/8775

### 6. Windows standalone installer fails when powershell.exe cannot resolve Get-FileHash
**#7118** | P2 · Windows 安装 · 需 triage | 6 条评论 · 👍 3

Windows 独立安装包在校验 SHA-256 时失败，原因与 PowerShell 环境相关。该问题持续近一个月仍未解决，今日更新显示获得 3 个 👍，是 Windows 用户最关心的安装阻塞问题之一。

🔗 https://github.com/QwenLM/qwen-code/issues/7118

### 7. bug(sdk): hidden unrecognized diagnostics mutate and evict transcript state
**#8823** | P2 · SDK/daemon · 新增 | 3 条评论

未识别的 daemon 事件在内部被规范化为调试事件，可能被 Web Shell 渲染器隐藏，但在隐藏前它们会先经过共享 transcript reducer（`appendStatusBlock()`），导致两个用户可见的会话状态问题。SDK 层数据一致性的典型缺陷，对构建上层工具的开发者影响较大。

🔗 https://github.com/QwenLM/qwen-code/issues/8823

### 8. npm test doesn't run due to unkown flag
**#8721** | P2 · 构建系统 · 讨论中 | 5 条评论

本地执行 `make test` 时 npm 因未知标志直接报错（`EUNKNOWN`），阻塞社区贡献者运行测试。对于开源项目的开发者体验是明显的减分项，维护者需尽快修复 npm scripts 配置。

🔗 https://github.com/QwenLM/qwen-code/issues/8721

### 9. proposal: Add a direct external context provider profile
**#7585** | P3 · 集成/MCP · 讨论中 | 12 条评论

提议为 Qwen Code 增加「直接外部上下文提供者」配置：通过私有 monorepo 集成，支持互斥的按需与自动召回两种配置，让单个交互式 CLI 进程从管理员绑定的外部源检索仓库共享上下文。评论数高（12 条），是企业级上下文/内存管理方向的重要参考。

🔗 https://github.com/QwenLM/qwen-code/issues/7585

### 10. security: read-only git sub-commands can execute programs configured in .git/config
**#8575** | P2 · 安全 · 已关闭 | 2 条评论

只读命令分类器（`isShellCommandReadOnlyAST`）仅分析命令文本，但白名单中的 git 子命令可执行 `.git/config` 中配置的外部程序（`diff.external`、`core.fsmonitor`）。这是与命令注入不同的新型绕过向量，已关闭但安全影响深远，值得持续关注。

🔗 https://github.com/QwenLM/qwen-code/issues/8575

---

## 重要 PR 进展（10 条）

### 1. fix(workflows): make replay journal durable
**#8735** | 工作流引擎 · @qqqys

将工作流回放状态升级为持久化的版本化检查点：通过 per-run 队列串行化日志写入，暂停/终止状态需等待持久化完成，恢复时校验精确的日志前缀。是对 Workflow 引擎可靠性的关键补强。

🔗 https://github.com/QwenLM/qwen-code/pull/8735

### 2. feat(cli): adopt Goal v3 in ACP sessions
**#8732** | CLI/ACP · @qqqys

将 ACP/Web Shell 会话中 `/goal` 的旧 Stop-hook 实现替换为 CLI 已使用的 Goal v3 运行时，支持创建、状态、编辑、暂停、恢复、替换、清除等完整操作，并通过统一状态机持久化。

🔗 https://github.com/QwenLM/qwen-code/pull/8732

### 3. fix(ci): watchdog silent sandbox hangs and reap the containers they leak
**#8816** | CI 基建 · @wenshao

针对自动修复流程中「静默 2 小时 sandbox 挂起」问题的双重缓解：在 `run-agent.mjs` 中引入空闲 watchdog（默认 20 分钟无输出即判定挂起并终止），同时补充容器清理机制，避免泄漏。对提升 autofix 效率至关重要。

🔗 https://github.com/QwenLM/qwen-code/pull/8816

### 4. fix(web-shell): stop rendering unrecognized daemon events in transcripts
**#8812** | Web Shell · @wenshao

修复 #8823 的前端部分：daemon UI 规范化器为每个调试事件盖上结构化 `debugReason` 标记，Web Shell 据此停止将「无法识别框架」的调试投影渲染为对话内容。

🔗 https://github.com/QwenLM/qwen-code/pull/8812

### 5. fix(web-shell): reconcile mid-turn messages with daemon state
**#8798** | Web Shell · @ytahdn

让 daemon 成为已接受 mid-turn 消息的唯一权威：Web Shell 按稳定消息 ID 调和共享会话队列，刷新/切换会话后可恢复排队消息，避免回合空闲时重复提交 daemon 已拥有的消息。针对 Web Shell 数据一致性的重要修复。

🔗 https://github.com/QwenLM/qwen-code/pull/8798

### 6. feat(cli): add /advisor command for second-opinion conversation review
**#7567** | CLI 功能 · @yiliang114

新增手动 `/advisor [focus]` 斜杠命令：以只读 fork 侧查询方式，让评审模型对当前对话给出独立第二意见（复用 `/btw` 的 forked agent 缓存机制）。对代码审查与决策辅助是实用增强。

🔗 https://github.com/QwenLM/qwen-code/pull/7567

### 7. fix(core): catch content-only thinking-tag leaks on all OpenAI-compatible providers
**#8818** | 模型兼容 · @yiliang114

针对 #6666 的全面修复：将「content-only thinking-tag 泄漏」的防御扩展至所有 OpenAI 兼容

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*