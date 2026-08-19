# AI CLI 工具社区动态日报 2026-08-20

> 生成时间: 2026-08-19 22:36 UTC | 覆盖工具: 7 个

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



---

# Claude Code 社区动态日报 — 2026-08-20

## 今日速览

昨日发布 v2.1.236 版本，新增 `ANTHROPIC_DEFAULT_MODEL` 环境变量（可设置新会话默认模型）与 `notify_when_idle` 跨会话通知能力，进一步完善了多会话协作场景。社区 Issue 方面，跨平台（Windows/WSL2/macOS）的稳定性问题依然是主要反馈热点，特别是代理后台进程、跨会话消息持久化以及 MCP 相关缺陷，建议开发者在 Windows 与桌面端场景中留意升级后的行为变化。

## 版本发布

### v2.1.236
- **`ANTHROPIC_DEFAULT_MODEL` 环境变量**：设置新会话启动时的默认模型。与 `ANTHROPIC_MODEL` 不同，用户仍可通过 `/model` 切换模型，且选择会持久化到后续会话（重启后仍保留），属于对现有模型的配置时机和持久性策略的修正。
- **`notify_when_idle`（跨会话 SendMessage）**：允许一个 Claude Code 会话在空闲时向另一个会话发送消息，进一步完善了多会话/代理间协作的基础能力。

来源：https://github.com/anthropics/claude-code/releases

## 社区热点 Issues

以下按社区关注度与影响范围挑选 10 个值得关注的 Issue（数据来源为过去 24 小时有更新的条目）：

### 1. 跨会话消息在 Windows 桌面端“幽灵投递”
- **#87509** [CLOSED] [Windows/桌面/代理]
- 跨会话 `send_message` 在 Windows Desktop 上报告成功，消息也会渲染在目标 UI，但从未写入真实转录（.jsonl），重启后即丢失。
- 为何重要：直接影响多会话协作可靠性，UI 表现与持久化结果不一致，排查成本高。
- 社区反应：作者明确描述了 UI“假成功”的完整复现路径，已关闭（或已定位修复）。
- https://github.com/anthropics/claude-code/issues/87509

### 2. 韩文文本在 UI 卡片中乱码
- **#80415** [OPEN] [IDE/VS Code 扩展]
- 韩文（Hangul）文本在 `AskUserQuestion` 与 `TodoWrite` 卡片 UI 中显示乱码，影响非英语用户的核心交互。
- 为何重要：国际化（i18n）显示缺陷，直接损伤东亚用户群的使用体验，且位于高频 UI 组件。
- 社区反应：6 条评论，2 个 👍，属于近期讨论热度较高的 bug。
- https://github.com/anthropics/claude-code/issues/80415

### 3. Bash 工具在 Auto 模式下被滥用做读写编辑
- **#87971** [OPEN] [Windows/VS Code/工具]
- Claude 在 Auto 模式下倾向用 Bash 工具执行读写与编辑，而非使用专门的读写工具，可能导致权限绕过或操作非预期文件。
- 为何重要：涉及 Auto 模式与工具选择策略，关系到安全与用户预期的一致性。
- 社区反应：新上报（8 月 19 日创建），已有 3 个 👍，用户关注度高。
- https://github.com/anthropics/claude-code/issues/87971

### 4. 仓库级插件配置在云沙盒中失效
- **#78119** [OPEN] [claude.ai/code/插件]
- 仓库提交的 `extraKnownMarketplaces` 与 `enabledPlugins` 在 claude.ai/code 云端沙盒环境中从未被处理，而 hooks 可以正常读取同一份 settings.json。
- 为何重要：云沙盒与实际环境行为不一致，影响插件开发者的测试与分发链路。
- 社区反应：5 个 👍，是近期标记数较高的功能类缺陷，评论区关联了三条相近的历史 Issue。
- https://github.com/anthropics/claude-code/issues/78119

### 5. 桌面端“按 PR 状态分组”功能被移除
- **#78115** [OPEN] [macOS 桌面端/回归]
- 新版桌面应用 Code 选项卡侧边栏的 “Group by PR status” 选项被移除，仅剩 “State”。
- 为何重要：功能无预警下线（疑似回归），影响既有用户工作流。
- 社区反应：有 2 个 👍，用户对 UI 功能回退敏感度较高。
- https://github.com/anthropics/claude-code/issues/78115

### 6. 交互式流式渲染在 Windows 上不增量绘制
- **#80364** [OPEN] [TUI/Windows/WSL2]
- 交互式文本流在 Windows 上从不增量刷新输出，且可在全新的 WSL2/Debian + xterm 环境复现，说明问题不在终端模拟器本身。
- 为何重要：影响 Windows 与 WSL2 用户最基础的阅读体验，且已排除终端差异因素，指向 CLI 内部逻辑。
- 社区反应：独立复现路径清晰，作者提供了平台外复现说明。
- https://github.com/anthropics/claude-code/issues/80364

### 7. WSL2 下 managed-settings.json 破坏 Bash 沙盒
- **#80284** [OPEN] [WSL2/核心]
- WSL2 下 `managed-settings.json` 会导致沙盒构建出带空用户名的 Windows 侧路径（`/mnt/c/Users/.claude`），使所有命令无法执行。
- 为何重要：企业托管配置场景下，单份配置即可瘫痪全部命令，属于高破坏性缺陷。
- 社区反应：复现条件明确（WSL2 + 托管设置）。
- https://github.com/anthropics/claude-code/issues/80284

### 8. 桌面端 MCP 环境变量不展开
- **#80197** [OPEN] [MCP/Windows 桌面端]
- Windows 桌面应用静默地不展开用户级 `mcpServers` env 中的 `${VAR}`，而 CLI 端行为正确。
- 为何重要：桌面端与 CLI 行为不一致会导致 MCP 服务器配置“看起来没问题但连不上”，隐蔽性强。
- 社区反应：处于还原最小复现阶段，暂无大量评论但属于典型平台一致性缺陷。
- https://github.com/anthropics/claude-code/issues/80197

### 9. 中断回合会静默杀死后台子代理
- **#78151** [OPEN] [macOS/代理/数据丢失]
- 用户中断一个回合时，正在运行的后台子代理会被静默终止，无通知、无失败状态标记。
- 为何重要：中断是高频操作，后台任务被静默杀死会造成工作结果丢失，且用户完全无感知。
- 社区反应：作者搜索了“interrupt kills background agents”等关键词，确认此为孤立问题。
- https://github.com/anthropics/claude-code/issues/78151

### 10. 转录文件在会话启动后间歇性无法解析
- **#78135** [OPEN] [macOS/代理/数据丢失]
- 会话/代理转录在启动后立即出现 “not found in project directory” 的间歇性错误，导致后台代理无法恢复，且崩溃会话的转录永久丢失。
- 为何重要：直接涉及会话数据可靠性，与 #87509、#80320 共同指向对话持久化链路的多点问题。
- 社区反应：作者明确标注了版本 2.1.198 与时间线，提供了完整环境信息。
- https://github.com/anthropics/claude-code/issues/78135

## 最新 PR 说明

过去 24 小时 PR 活动较少，仅 1 条公开 PR 有更新。考虑到日报覆盖面，我们将其列出，同时归纳了近期 PR 的活跃趋势。

### 1. 文档：补充 marketplace 的 skipLfs 配置说明
- **#77977** [OPEN] [文档]
- 为插件开发文档补充 `github` 与 `git` marketplace 源对象的 `skipLfs` 选项，并添加 GitHub shorthand 与通用 Git URL 跳过 Git LFS 下载的示例，回应 #63035。
- 影响：帮助插件开发者在大仓库场景下避免 LFS 下载开销，纯文档变更。
- https://github.com/anthropics/claude-code/pull/77977

> **PR 趋势补充**：尽管当日 PR 仅 1 条，但结合近期合并流，社区 PR 集中在文档补齐（如 #77977）和小范围修 Bug。核心功能开发仍以官方闭源发布为主，建议关注 Release 说明以获取更完整的演进信息。

## 功能需求趋势

从近 24 小时活跃的 50 条 Issue 中可提炼出几个社区关注度最高的功能方向：

### IDE 与桌面端集成
- **VS Code 扩展**：国际化显示（#80415）、网络驱动器场景下 Session 丢失（#80228）、Auto 模式下工具选择策略（#87971）。
- **桌面应用**：侧边栏 Session 丢失（#78130）、配置 symlink 被覆盖（#80276）、UI 功能静默移除（#78115）。
- 趋势：桌面端正逐渐成为独立于 CLI 的重要入口，用户对一致性和数据持久性的要求明显提升。

### 多会话 / Agent 协作
- 跨会话 `send_message` 持久化失败（#87509）、Cowork 会话跨设备同步（#80329）与转录未持久化（#80320）、iTerm2 命令截断（#80302）。
- 趋势：v2.1.236 引入 `notify_when_idle` 表明官方正在推进跨会话通信，而社区侧则已在真实场景中暴露出持久化与渲染不一致的落地问题。

### Windows / WSL2 平台支持
- 流式渲染不刷新（#80364）、Bash 工具 stdout 尾部丢失（#80317）、managed-settings 路径错误（#80284）、MCP env 不展开（#80197）。
- 趋势：Windows 平台已成为除 macOS 外的第二大使用场景，平台一致性是社区最集中的痛点。

### MCP 生态稳定性
- MCP 工具发现失败（#78150）、环境变量展开不一致（#80197）、iOS 端审批提示被静默丢弃（#80295）。
- 趋势：MCP 的采用率在上升，但“CLI 正常、桌面端/iOS 异常”的跨端行为差异引发大量问题。

### 代理 / 后台任务可靠性
- 中断杀死后台子代理（#78151）、托管代理因图片尺寸问题终止（#78127）、后台服务不可达（#80093）。
- 趋势：Agent 相关功能处于快速迭代期，用户关注“可恢复性”胜过“功能丰富度”——宁可失败也不希望静默中断。

## 开发者关注点

**1. 数据持久化一致性成为首要痛点**
- 多条 Issue 指向同一类问题：UI 显示成功，但转录文件未写入（#87509、#80320）；或者转录文件存在但 UI 读不到（#78135）。核心诉求是：**会话状态必须以磁盘转录为唯一事实来源，UI 应与之一致**，且不能因崩溃或中断丢失。

**2. Windows 平台行为与 macOS 差异过大**
- 流式输出、Bash 工具输出完整性、路径处理（#80284）在 Windows/WSL2 上与 macOS 存在明显差距。开发者期望在 Windows 下获得与 macOS 同等的体验，而非“能跑但残废”。

**3. 静默失败比报错更令人困扰**
- #87509 的“幽灵投递”、#78151 的“静默杀死子代理”、#80197 的“MCP env 静默不展开”共同指向一个开发体验原则：**宁可明确报错，也不能表面成功实际失效**。这已成为用户投诉中最常见的情绪主线。

**4. MCP 跨端一致性需求上升**
- 随着 MCP 服务器的普及，开发者期望 CLI、桌面端、云端沙盒（#78119）行为一致。配置在 A 端有效、B 端无效，会导致难以排查的配置漂移问题。

**5. Auto 模式下的工具选择策略受关注**
- #87971（Bash 滥用）与 #80242（Edit 审批无法被 allow 规则豁免）表明了社区对 Auto 模式的两个核心诉求：**正确选择专用工具**、**让显式授权规则真正生效**。

---

**总结**：v2.1.236 的 `notify_when_idle` 和 `ANTHROPIC_DEFAULT_MODEL` 释放了多会话协作与模型配置的积极信号；但社区反馈显示，桌端与跨平台一致性问题已成为当前用户满意度的最大短板，建议优先关注 #87509、#80364、#78119 三个方向的进展——它们分别代表了数据持久化、平台一致性、云沙盒功能对齐三类核心诉求。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 · 2026-08-20

## 1. 今日速览

昨日 Codex 发布了 `rust-v0.149.0-alpha.1` Alpha 预发布版本；社区热度集中在 Windows 桌面端：内置浏览器插件初始化失败（#39136）以 77 条评论成为焦点，同时 Windows 下会话归档失败、认证丢失、更新机制故障等多条 Issue 持续发酵。PR 侧则以安全加固为主，包括停止将 Git 命令视为固有安全、隔离插件 Git 操作等。

## 2. 版本发布

### rust-v0.149.0-alpha.1

- **版本号：** 0.149.0-alpha.1
- **链接：** https://github.com/openai/codex/releases

本次为 Alpha 预发布版本，官方 Release 页面未附带详细变更日志，需关注后续 Beta/稳定版发布说明。

## 3. 社区热点 Issues（Top 10）

### ① Windows 内置浏览器插件初始化失败：Trusted RPC 依赖不在可信代码路径内
- **Issue #39136** | 评论 77 | 👍 41
- **链接：** https://github.com/openai/codex/issues/39136
- **要点：** Windows 版 Codex 桌面应用打开内置浏览器 UI 时，因 Trusted RPC 依赖未被识别为可信路径导致初始化失败。这是目前评论数和点赞数双高的热点问题，影响 Plus 用户。

### ② GPT Sol/Terra 线程无法生成 Luna 子代理：版本不兼容
- **Issue #34301** | 评论 10 | 👍 34
- **链接：** https://github.com/openai/codex/issues/34301
- **要点：** Windows 下 `gpt-5.6-sol` 模型线程无法调用 Luna 多智能体子代理，社区反应强烈（34👍）。涉及 CLI 0.144.6 与子代理版本匹配问题。

### ③ macOS 桌面端反复生成 Computer Use 工作进程并触发 V8 OOM 崩溃
- **Issue #38455** | 评论 30 | 👍 12
- **链接：** https://github.com/openai/codex/issues/38455
- **要点：** App 26.810.41047 在空闲状态下约 98 秒后崩溃，崩溃时存在 187 个 `computer-use` 线程，最终因 `node::OOMErrorHandler` 中止。此前版本正常，疑似回归。

### ④ “不再询问”权限记忆功能失效
- **Issue #11298** | 评论 10 | 👍 18
- **链接：** https://github.com/openai/codex/issues/11298
- **要点：** “Yes, and don't ask again for commands that start with” 功能不生效，沙箱反复请求命令执行权限，长期未修复，Pro 用户受影响。

### ⑤ Windows 原生安装执行 `codex update` 失败
- **Issue #30015** | 评论 8 | 👍 14
- **链接：** https://github.com/openai/codex/issues/30015
- **要点：** Windows 上通过原生安装方式部署的 Codex CLI 调用 `codex update` 无法完成更新，与 #27117、#34030 同属 Windows 更新链路问题。

### ⑥ Windows 独立更新时 PSModulePath 被继承导致 Get-FileHash 失败
- **Issue #27117** | 评论 17 | 👍 13
- **链接：** https://github.com/openai/codex/issues/27117
- **要点：** 从 pwsh 启动的 Codex 在更新时启动 `powershell.exe`，子进程错误继承 PowerShell 7 的 `PSModulePath`，导致 `Get-FileHash` 校验崩溃。

### ⑦ Local Compaction v2 无限保留 input_image 负载，触发反复自动压缩
- **Issue #33493** | 评论 17 | 👍 4
- **链接：** https://github.com/openai/codex/issues/33493
- **要点：** 长会话线程在图片密集场景下，压缩后的 input_image 数据不被清理，导致上下文持续膨胀并反复进入自动压缩循环。

### ⑧ [Windows] 打开旧线程导致个人 Pro 账号被登出
- **Issue #39189** | 评论 9 | 👍 2
- **链接：** https://github.com/openai/codex/issues/39189
- **要点：** 工作区仅设置 401 后，打开已有线程会连带将个人 ChatGPT Pro 账号登出。认证状态管理存在严重缺陷。

### ⑨ Windows 桌面开启 Advanced Account Security 后 15-40 秒内丢失登录态
- **Issue #39170** | 评论 5 | 👍 6
- **链接：** https://github.com/openai/codex/issues/39170
- **要点：** 开启“高级账户安全”后桌面应用快速掉登录，但 CLI 仍保持登录，说明桌面端与 CLI 的凭据刷新机制不一致。

### ⑩ Codex 0.148.0 破坏 `-c` 方式添加的 MCP 服务器（app-server 模式）
- **Issue #39537** | 评论 2 | 👍 0
- **链接：** https://github.com/openai/codex/issues/39537
- **要点：** 新发布的 0.148.0 在 app-server 模式下无法正确加载通过 `-c` 选项配置的 MCP 服务器，属于版本回归，macOS 用户已确认。

## 4. 重要 PR 进展（Top 10）

### ① 停止将 Git 命令视为固有安全（#39524）
- **链接：** https://github.com/openai/codex/pull/39524
- **内容：** 仓库配置可使只读 Git 命令执行辅助程序，仅靠参数无法建立信任。PR 将 Git 命令从 Unix/Windows 已知安全命令分类中移除。属安全加固重要变更。

### ② 隔离自动插件 Git 操作（#39520）
- **链接：** https://github.com/openai/codex/pull/39520
- **内容：** 防止后台市场/插件刷新继承项目级 Git 配置（如远程重定向、自定义 Helper），避免自动操作被仓库配置劫持。

### ③ 为 Bedrock 刷新过期 AWS 凭证（#39410）
- **链接：** https://github.com/openai/codex/pull/39410
- **内容：** 新增 `aws.auth_refresh` 提供方配置，支持通过 `aws` 命令及可配置超时刷新过期凭证，解决 Bedrock 长会话中途凭证失效问题。

### ④ 移除异步用户消息功能门控（#39452）
- **链接：** https://github.com/openai/codex/pull/39452
- **内容：** 当模型支持时，向根代理开放 `send_user_message_async`；保留 `send_async_message` 兼容标志以兼容旧配置。

### ⑤ 在首轮对话前持久化线程节移动（#39523）
- **链接：** https://github.com/openai/codex/pull/39523
- **内容：** 修复新建非临时线程尚未持久化时移动至分区会丢失的问题，在移动前先物化并刷新线程数据。

### ⑥ 整合 Guardian 扩展到 `codex-guardian-v2`（#39474）
- **链接：** https://github.com/openai/codex/pull/39474
- **内容：** 将 Guardian 线程生命周期贡献者与子代理生成上下文统一收敛至 `codex-guardian-v2` 扩展，移除冗余入口点。

### ⑦ 使用 `mem::take` 清理统一执行输出缓冲区（#39515）
- **链接：** https://github.com/openai/codex/pull/39515
- **内容：** 用 `std::mem::take` 替代自定义 `HeadTailBuffer::drain`，在取出缓冲数据的同时重置共享缓冲区状态，减少出错面。

### ⑧ 将 HeadTailBuffer 容量改为 const 泛型（#39493）
- **链接：** https://github.com/openai/codex/pull/39493
- **内容：** 通过 const 泛型参数化 `MAX_BYTES`，生产环境默认使用 `UNIFIED_EXEC_OUTPUT_MAX_BYTES` 容量，并更新测试覆盖。

### ⑨ 支持旧版系统 Bubblewrap 的 FD 挂载（#39404）
- **链接：** https://github.com/openai/codex/pull/39404
- **内容：** 探测系统 Bubblewrap 是否支持 `--ro-bind-fd`，旧版本自动回退到兼容模式，提升 Linux 沙箱可移植性。

### ⑩ 为内置控制工具调用添加分析埋点（#39510）
- **链接：** https://github.com/openai/codex/pull/39510
- **

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-20

## 今日速览

昨日 Gemini CLI 发布两个稳定/预览版本（v0.56.0 与 v0.57.0-preview.0），重点修复 OAuth 代理与 IDE 连接问题。社区讨论热度集中在 Subagent 状态误报与 Agent 挂起等稳定性问题上；PR 方面涌现多个针对 Whisper 语音模块的可靠性修复与新模型（3.7 Flash）支持。

---

## 版本发布

### v0.57.0-preview.0
- **动态解析 Cloud Workstations 代理重定向 URI**，修复 OAuth 流程中代理场景下无法完成认证的问题（[#28688](https://github.com/google-gemini/gemini-cli/pull/28688)）
- **修复 IDE 连接中的目录不匹配问题**，避免错误上下文导致的操作偏差（[PR #28688](https://github.com/google-gemini/gemini-cli/pull/28688)）

### v0.56.0
- 正式版本发布，完整变更记录见 [Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.55.1...v0.56.0)

### v0.56.0-nightly.20260819
- SSR Agent：为 Vertex AI locations 补充文档链接（[#28865](https://github.com/google-gemini/gemini-cli/pull/28865)）
- SSR Agent：修复 agents 模式禁用时 Subagent 仍被触发的问题

---

## 社区热点 Issues（Top 10）

### 1. Subagent 超限后误报“成功”（#22323）
**优先级 P1，12 条评论，持续发酵中**
`codebase_investigator` 子代理在达到 MAX_TURNS 后返回 `status: "success"` 与 `Termination Reason: "GOAL"`，掩盖了实际被中断的事实。社区认为这是 Agent 可观测性的严重缺口，会导致错误信任自动结论。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22323)

### 2. Generalist Agent 无限挂起（#21409）
**优先级 P1，8 条评论，👍 8**
简单操作（如创建文件夹）在委托给 generalist agent 后永久挂起，用户最长等待 1 小时无响应。作者已提供 workaround（禁用 subagent 委托），但此问题严重影响基础可用性，社区关注度高。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21409)

### 3. Shell 命令完成后卡在“Waiting input”（#25166）
**优先级 P1，4 条评论，👍 3**
简单的 CLI 命令执行完成后，界面仍显示命令运行中并等待输入。涉及终端状态机核心逻辑，是当前最影响日常体验的 bug 之一。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/25166)

### 4. Browser Subagent 在 Wayland 下失败（#21983）
**优先级 P1，4 条评论**
浏览器子代理在 Wayland 环境中直接失败，限制 Linux 用户使用浏览器自动化能力，属于平台兼容性关键问题。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21983)

### 5. get-shit-done 输出钩子导致崩溃（#22186）
**优先级 P1，3 条评论**
GSD 输出接近完成时触发崩溃（containers 启动后打印摘要阶段），疑似与输出处理钩子的边界条件有关。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22186)

### 6. 零依赖 OS 沙箱化：利用模型 bash 亲和性（#19873）
**优先级 P2，8 条评论**
提议利用 Gemini 3 模型原生擅长 POSIX 工具的特点，通过零依赖沙箱在执行后做“意图路由”，在安全性与充分发挥模型能力之间取得平衡。社区讨论热烈，被视为下一代工具设计方向。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/19873)

### 7. 组件级评估基础设施（#24353）
**优先级 P1，7 条评论**
已有 76 个行为评估测试覆盖 6 个 Gemini 模型，但缺少组件级评估框架来更精细地验证每个 Agent 组件的表现。这是提升整体质量的关键基础设施。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/24353)

### 8. AST 感知的文件读取与代码库映射评估（#22745）
**优先级 P2，7 条评论**
探索利用 AST 感知工具精确定位方法边界、减少 token 噪声并优化代码库导航，为未来的上下文压缩与检索策略提供依据。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22745)

### 9. Auto Memory 对低信号会话的无限重试（#26522）
**优先级 P2，5 条评论**
Auto Memory 服务只将成功 `read_file` 的会话标记为已处理，低信号会话会反复出现在候选池中，造成重复计算。社区建议引入“跳过即记录”机制。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/26522)

### 10. 超过 128 个工具时出现 400 错误（#24246）
**优先级 P2，3 条评论**
当启用工具超过 128 个时触发 API 400 错误。开发者期望 Agent 能够根据上下文动态裁剪工具列表，而不是全量携带。与未来大规模工具生态的发展直接相关。
[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/24246)

---

## 重要 PR 进展（Top 10）

### 1. GCS 轨迹日志与产物保留（#28922）
为生产环境与评估运行实现 GCS 轨迹记录和调试产物存储，便于事后排查 agent 执行过程。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28922)

### 2. 子进程执行安全加固（#28898）
防止敏感认证令牌泄漏到不受信任的工具执行环境中，并增强 GitHub API 交互安全性。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28898)

### 3. 符号链接一致性处理（#28915）
修复 `.geminiignore`/`.gitignore` 对符号链接路径的评估不一致问题，消除工具行为偏差。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28915)

### 4. 扩展环境变量需用户同意（#28863）
扩展更新不再能静默注入环境变量到 MCP Server 进程，所有变更需重新获得用户许可。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28863)

### 5. Whisper 转录 stdout 行缓冲（#28916）
修复本地语音模式下转录文本跨 chunk 被丢弃的问题，通过按行缓冲组装完整输出。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28916)

### 6. Whisper 模型下载原子化（#28917）
下载过程改为临时文件 + 原子重命名，避免中断或失败留下损坏模型文件。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28917)

### 7. 重试 nudge 注入保留前缀缓存（#28914）
将重试提示从 systemInstruction 移到 contents 末尾，既触发恢复又保留静态前缀缓存，优化性能。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28914)

### 8. 新增 Gemini 3.7 Flash / 3.6 Flash 模型支持（#28910）
在 core 与 cli 中配置新模型定义与选择逻辑，跟进最新模型发布。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28910)

### 9. 恢复 stdin 暂停状态（#28889）
修复终端能力检测后 stdin 未恢复暂停模式的问题，避免输入流异常。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28889)

### 10. 支持聊天会话重命名（#28907）
新增 `/chat rename` 与 `/resume rename` 命令，通过现有存储链路保存自定义标题。
[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28907)

---

## 功能需求趋势

1. **Agent 可观测性**：Subagent 轨迹共享（#22598）、bugreport 包含子代理上下文（#21763）等需求频出，社区对“发生什么、为什么”的透明度要求显著提升。
2. **AST/结构化代码理解**：#22745 与 #22746 形成组合拳，期望通过 AST 感知工具实现精确读码、精准搜索与高效映射，降低 token 消耗。
3. **安全与权限治理**：要求 agent 主动避免破坏性操作（#22672）、沙箱环境变量规范化（#28911/#28904）、扩展环境变量同意机制（#28863），安全红线成为社区共识。
4. **终端体验与稳定性**：resize 闪烁（#21924）、ctrl+o 展开抖动（#28921）、stdin 恢复（#28889）等 UI/终端细节问题关注度上升。
5. **模型动态适配**：新模型快速接入（#28910）与工具数量超限问题（#24246）并存，社区期望更智能的工具裁剪与模型路由策略。

---

## 开发者关注点

- **高发稳定性 bug 影响信任**：Shell 卡住、Agent 挂起、GSD 崩溃等 P1 问题反复出现，开发者普遍反馈“简单操作也会卡死”，对 CLI 作为日常工具的信心造成冲击。
- **Auto Memory 系统引发隐私担忧**：#26525 指出转录内容先进入模型上下文再做脱敏，开发者认为应在发送前进行确定性脱敏，并减少日志输出。
- **配置覆盖失效**：#22267 指出 Browser Agent 忽略 `settings.json` 的 maxTurns 等配置，覆盖机制的有效性是高频痛点。
- **Agent 对自身能力“不自知”**：#21968、#21432 表明模型不会主动使用 skills/subagents，也不了解自己的 CLI 参数与快捷键，影响自动化深度。
- **对修复速度的期待**：多个 P1 issue 长期处于 need-retesting 状态，社区希望官方加快验证节奏并同步进展。

---

*本日报由 AI 自动生成，数据截止 2026-08-19 24:00 UTC。*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-08-20

## 今日速览
过去 24 小时，Copilot CLI 连续发布 1.0.81-2/3/4 三个修补版本，稳定性修复节奏加快。社区焦点集中在 **Sandbox 强制启用**与 **MCP OAuth 兼容性**两大方向：多条 issue 指出新版 Sandbox 行为与用户显式配置冲突，Atlassian MCP 连接在 1.0.79/1.0.80 中连续回归。此外，非交互模式绕过企业权限策略的问题引发安全关注。

## 版本发布
| 版本 | 说明 |
|---|---|
| [v1.0.81-4](https://github.com/github/copilot-cli/releases) | Fixes and changes |
| [v1.0.81-3](https://github.com/github/copilot-cli/releases) | Fixes and changes |
| [v1.0.81-2](https://github.com/github/copilot-cli/releases) | Fixes and changes |

官方未提供详细变更日志。结合同日 issue 活跃度推测，本轮修复可能涉及 Sandbox 策略、MCP 初始化流程及权限控制等近期热点问题。

## 社区热点 Issues

**1. Linux 终端 ctrl+shift+c 复制快捷键回归** — #2082  
[链接](https://github.com/github/copilot-cli/issues/2082)  
自 v1.0.4 起，Ubuntu 24.04 终端中 `ctrl+shift+c` 复制所选文本的功能失效，用户不得不改用 `ctrl+c` 或右键菜单。该问题持续数月仍未被修复，热度高（👍 12，评论 24），是终端体验中最受关注的老 bug。

**2. Atlassian MCP OAuth 失败（RFC 8414 §3.3）** — #4480

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-08-20）

## 今日速览

今日无新版本发布、无新 Pull Request 动态。过去 24 小时唯一的 Issue 更新是 **#2609**，该问题报告了 ACP（Agent Client Protocol）模式下内置 Grep/Glob 工具不可用、Bash 能力受限的缺陷，目前已关闭。该 Issue 集中体现了社区对 **ACP/IDE 集成完整性** 与 **工具调用兼容性** 的关注。

## 版本发布

过去 24 小时内无新版本 Release，当前仓库最新版本仍为 v0.37.x。

## 社区热点 Issues

> 数据说明：过去 24 小时内有更新的 Issue 仅 1 条，无足够样本支撑“10 个挑选项”，故聚焦分析该唯一动态。

### [#2609 [ACP] Grep/Glob blocked: "ACP runtime only supports interactive Bash tool processes"; Bash intermittently reports "ACP terminal capability is unavailable"](https://github.com/MoonshotAI/kimi-cli/issues/2609)

- **作者**：@SolomonFang | **创建**：2026-08-19 | **更新时间**：2026-08-19 | **状态**：Closed
- **评论数**：0 | **浏览量点赞**：0 👍
- **环境**：kimi-code CLI 0.37.1 / macOS / ACP 客户端为 Zed（通过 `kimi acp` 连接）

**现象**：在 ACP 会话中，内置 `Grep` 与 `Glob` 工具必定失败，并报错 `ACP runtime only supports interactive Bash tool processes`。`Read` 工具工作正常，但 `Bash` 工具偶发 `ACP terminal capability is unavailable` 错误。

**为何值得关注**：
- ACP 是 Kimi Code CLI 与 Zed 等编辑器深度集成的关键通道，Grep/Glob 在 AI 编程中的使用频率非常高，直接阻塞会显著影响编辑器内编码体验；
- 错误信息对用户不透明——“only supports interactive Bash” 并未解释为何 Grep/Glob 被禁用，也没有给出替代方案；
- 该问题创建当日即被关闭，社区尚未来得及展开讨论，但缺少 Issue 闭环说明，用户可能在其他 ACP 客户端中继续踩坑。

**社区反应**：当前为 0 评论、0 点赞，讨论热度较低，可理解为问题被快速修复或绕过，但也可能意味着 ACP 模式尚处于早期验证阶段，使用人群有限。

## 重要 PR 进展

过去 24 小时内，仓库没有新的 Pull Request 创建或合并动态，因此今日无重要 PR 可汇报。

## 功能需求趋势

> 基于今日唯一 Issue #2609，以及 Kimi Code CLI 的产品定位，提炼以下趋势（样本有限，仅作方向性参考）：

1. **ACP/编辑器集成**：用户越来越倾向于在 Zed、VS Code、Neovim 等编辑器中直接调用 Kimi Code CLI，将其作为 AI 编程后端。ACP 模式下内置工具链是否完整，将直接影响这一类工作流的成败。
2. **工具调用统一性**：Grep/Glob/Read/Bash 等工具在普通 TUI 会话与 ACP 会话之间的行为应尽量保持一致，而不是因协议限制引入不预期差异。
3. **错误信息可读性**：技术型用户也能够接受合理的限制，但需要清晰的错误提示、文档说明或可配置的降级策略，而不是一条含义模糊的字符串。

## 开发者关注点

- **ACP 模式工具支持范围**：开发者期望官方明确列出哪些内置工具在 ACP 下可用、哪些不可用，以及对应的替代路径。
- **Bash 进程管理策略**：当前仅支持 “interactive Bash” 似乎是为了维护 session 状态，但这会阻塞非交互式的 grep/glob 任务，希望后续版本能提供更灵活的策略（如仅读命令自动批准）。
- **故障排查体验**：多个错误信息同时出现（Grep/Glob 失败 + Bash 偶发能力不足），会让开发者难以判断问题是出在 CLI 侧、ACP 协议侧还是 Zed 客户端侧。建议补齐 ACP session 的日志导出与诊断建议。

---
*报告基于 2026-08-20 GitHub 公开数据生成，数据范围有限，内容仅供参考。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报（2026-08-20）

## 今日速览

今日社区最集中的声音指向 **Go 订阅计费不透明与配额异常消耗**——多条高赞 Issue 报告本地用量统计与云端实际扣费严重不符，缓存读取计费规则不明；与此同时，**Provider 流中断被静默记录为正常结束**的 bug（#37852）获得了 56 个 👍，成为近期开发者痛点最强烈的技术问题。代码贡献方面，TUI 交互增强与多个 AI 适配修复正在推进。

## 版本发布

过去 24 小时内无新版本发布。

## 社区热点 Issues

1. **[#37852] Aborted provider stream recorded as clean stop (finish=unknown, zero usage, no text)**  
   Provider 流中途终止时，opencode 错误地将其记录为正常完成（finish=unknown、零 tokens、无文本），agent 循环静默退出且无任何错误上报，导致 subagent 返回空结果。  
   评论 19 | 👍 56 | [链接](https://github.com/anomalyco/opencode/issues/37852)

2. **[#4877] Emacs keybindings frustratingly inconsistent**  
   用户反馈 Ctrl-A/Ctrl-K 等 Emacs 肌肉记忆键位在 TUI 中行为不一致：Ctrl-A 跳到整个文本窗口开头而非行首，Ctrl-K 随之失效。  
   评论 26 | 👍 2 | [链接](https://github.com/anomalyco/opencode/issues/4877)

3. **[#43463] Complaint — Zen 订阅购买后无法生成代码**  
   用户购买 Zen 套餐两天后即报错：`invalid_encrypted_content`，加密内容无法被解析，无法生成任何代码。  
   评论 8 | [链接](https://github.com/anomalyco/opencode/issues/43463)

4. **[#43364] luna session isn't working in opencode go**  
   Go 订阅用户在终端使用 GPT-5.6 Luna 时突然报 `invalid_encrypted_content`，新建会话也无法恢复。  
   评论 7 | 👍 3 | [链接](https://github.com/anomalyco/opencode/issues/43364)

5. **[#41976] Go plan: $60/month quota exhausted in 6 days while the client recorded only $14.80**  
   付费用户 6 天内 $60 配额耗尽，但本地客户端仅记录了 $14.80 用量——cache-read 计费对用户不可见且无文档，本地计量器误导用户。  
   评论 4 | [链接](https://github.com/anomalyco/opencode/issues/41976)

6. **[#25848] [FEATURE]: add session renaming**  
   用户请求支持手动为 session 重命名（如 `/rename` 命令或 CLI 参数），方便多项目会话管理。  
   评论 13 | 👍 1 | [链接](https://github.com/anomalyco/opencode/issues/25848)

7. **[#9296] Experimental plan mode handover -> build uses plan agent's model**  
   用户配置 plan 使用 GPT-5.2、build 使用 opus-4.5，但 plan 模式切换至 build 时仍使用 plan 的模型，导致构建阶段报错。  
   评论 8 | 👍 11 | [链接](https://github.com/anomalyco/opencode/issues/9296)

8. **[#37047] Compaction hallucinating project details after update**  
   升级至 1.18.0 后，会话压缩（compaction）生成的摘要与原始会话完全无关，产生大量幻觉内容。  
   评论 4 | [链接](https://github.com/anomalyco/opencode/issues/37047)

9. **[#43387] OpenCode Go 5-hour limit shows ~50% consumed after only ~$1.80 of usage**  
   5 小时内的用量限额显示已消耗约 50%（约 $6/$12），但实际用量仅约 $1.80，请求在达到美元限额前即被限流。  
   评论 2 | [链接](https://github.com/anomalyco/opencode/issues/43387)

10. **[#39876] [2.0] tui: libopentui temporary copies consume 207 GiB**  
    OpenCode 2.0 在 $TMPDIR 中遗留了约 58,935 份 `libopentui.dylib` 临时文件，共占用 207.4 GiB，几乎塞满磁盘。  
    评论 3 | 👍 1 | [链接](https://github.com/anomalyco/opencode/issues/39876)

## 重要 PR 进展

1. **[#43520] feat(client): optimistic prompt admission with client-minted IDs**  
   数据层新增 client-minted ID，prompt 发送即时渲染，并通过幂等机制保证与服务器回包对账一致，大幅提升输入响应速度。  
   [链接](https://github.com/anomalyco/opencode/pull/43520)

2. **[#43528] fix(tui): render commands as attachments**  
   将斜杠命令渲染为“命令附件”，模型不再看到模板展开后的过程文本，只接收最终结果，提升 TUI 展示一致性。  
   [链接](https://github.com/anomalyco/opencode/pull/43528)

3. **[#43479] fix(ai): isolate Gemini function-response turns**  
   修复 Gemini 将 system updates 合并进包含 function response 的 user turn 的问题，符合 Gemini 对 function-response 的格式要求。  
   [链接](https://github.com/anomalyco/opencode/pull/43479)

4. **[#43498] fix(ai): preserve Vertex Anthropic tool continuations**  
   解决 Vertex 在 Claude 工具调用以本地 system message 结尾时返回 HTTP 404 的问题，保留工具续接上下文。  
   [链接](https://github.com/anomalyco/opencode/pull/43498)

5. **[#43522] fix: eliminate flaky CI races**  
   修复过去两天 V2 测试中持续出现的 CI 竞态问题（TUI 插件重复激活、CLI 子进程测试受真实环境干扰等），提升 CI 稳定性。  
   [链接](https://github.com/anomalyco/opencode/pull/43522)

6. **[#43526] fix(tui): handle form clipboard shortcut**  
   TUI 表单支持 Ctrl+V 粘贴；当焦点在配置选项上时，粘贴会自动打开自定义输入并填入文本。  
   [链接](https://github.com/anomalyco/opencode/pull/43526)

7. **[#37813] refactor(opencode): coalesce code mode progress updates**  
   将 Code Mode 的累计子调用元数据改为 100ms 间隔合并发布，避免每个事件触发一次持久化。  
   [链接](https://github.com/anomalyco/opencode/pull/37813)

8. **[#37810] fix(github): wait for browser callback before polling install status**  
   修复 `opencode github install` 在 Linux 上无限挂起、macOS/Windows 上静默超时的问题，等待浏览器回调后再开始轮询。  
   [链接](https://github.com/anomalyco/opencode/pull/37810)

9. **[#37809] fix(console): prevent open redirect in /auth/authorize continue parameter**  
   修复控制台 `/auth/authorize` 路由的开放重定向漏洞（CWE-601），阻止恶意构造的 continue 参数跳转。  
   [链接](https://github.com/anomalyco/opencode/pull/37809)

10. **[#37768] fix(desktop): to restore provider catalog**  
    改用桌面兼容路径读取 ModelsDev 快照，恢复桌面端设置中的内置 provider 目录，并保留模型元数据与定价信息。  
    [链接](https://github.com/anomalyco/opencode/pull/37768)

## 功能需求趋势

- **会话管理增强**：手动重命名 session（#25848）、崩溃后自动恢复会话（#43488）是高频诉求，说明用户对多会话组织和数据持久性的要求正在提升。
- **配额/计费透明化**：Go 订阅用户集中反馈缓存读取计费不可见、本地计量与真实扣费不一致（#41976、#43387、#43409、#43416、#43424），要求明确 cache-read 计费规则并修复本地用量统计。
- **桌面端交互补全**：TUI 已有的快捷键切换 agent（Tab/Shift+Tab）需同步到桌面 App（#41742）；用户请求在 agent 需要审批时发出声音/通知（#43493）；Review 模式快捷键冲突需修复（#43408）。
- **新模型/新 Provider 稳定性**：Luna（#43364）、Muse（#43477）、DeepSeek V4 Flash（#40253）接入后出现加密内容校验失败、端点不可用等问题，模型接入的兼容性测试需要加强。
- **TUI 打磨**：Emacs 键位一致性（#4877）、Windows 下回车失效（#23219）、detach/reattach 后 pending 提示丢失（#36604）、临时文件占用 207 GiB（#39876）——TUI 仍是核心使用场景，但交互细节和资源管理问题突出。

## 开发者关注点

- **计费不透明是当前最大信任危机**：多条高赞 Issue 反映 Go 订阅的缓存读取计费机制未被文档化、本地用量仪表与实际扣费偏差大，5 小时窗口与 30 天配额双重限制导致“提前限流”的感知非常强烈。
- **Provider 流中断被误判为正常结束**：`finish=unknown` 且零 usage、零文本却算作完整一轮，直接导致 subagent 返回空结果——这类“静默失败”在自动化和 agent 工作流中损害尤其严重。
- **模型切换与配置作用域 bug**：plan 模式切换到 build 时错误沿用 plan 的模型（#9296），提示用户配置的 agent.model 作用域逻辑仍有漏洞。
- **加密内容校验错误成为新痛点**：多个订阅用户在同一时间段内遇到 `invalid_encrypted_content` 错误，猜测与 Console/Go 服务端变更相关，需要官方尽快介入排查。
- **升级后稳定性回退**：Compaction 产生幻觉（#37047）和桌面端 provider 目录丢失（#37768 对应 issue）均为升级后出现，提示版本发布前对会话压缩和桌面离线 catalog 的回归测试需要补充。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

## 今日速览

- 昨日发布 v0.21.14 正式版，核心是新增 `qwen sessions ps` 命令与 live-session registry，支持以 JSON 输出列出并管理运行中的交互式会话（[#8969](https://github.com/QwenLM/qwen-code/pull/8969)）。
- 社区焦点集中在会话与 Token 管理的可靠性上：多个 P1/P2 Bug 涉及模型切换后 Token 计数错乱、`/effort max` 导致会话不可用、压缩后上下文丢失等问题。
- 多代理（Agent Team）相关误报问题引发讨论，`run_in_background` 失效、`task_list` 循环误判等反馈集中；同时 `/review` 工具链与 daemon 资源治理的 PR 持续推进。

---

## 版本发布

### v0.21.14（正式版）
- 新增 `qwen sessions ps` 命令与 live-session registry，可列出并管理运行中的交互式会话，支持 JSON 输出，便于脚本化和自动化运维场景（[#8969](https://github.com/QwenLM

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*