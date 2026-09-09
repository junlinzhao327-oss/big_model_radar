# AI CLI 工具社区动态日报 2026-09-10

> 生成时间: 2026-09-09 22:35 UTC | 覆盖工具: 7 个

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



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-09-10

## 今日速览

Codex 发布 v0.154.0，正式引入 GPT-6-Astra 模型支持，并带来实验性 worktree 会话隔离功能。社区层面，Windows 平台的稳定性与功能缺陷（尤其 Computer Use、性能卡顿）仍是讨论焦点，同时大量 Pull Request 集中修复沙箱逃逸、Guardian 审查预算与托管守护进程恢复机制，安全加固与可靠性提升成为当前主线。

---

## 版本发布

过去 24 小时共发布 1 个正式版本及 4 个 alpha 版本：

### rust-v0.154.0（正式版）
- **GPT-6-Astra 模型支持**：已可在模型选择器（Model Picker）及 Amazon Bedrock 目录中使用。（[#42879](https://github.com/openai/codex/issues/42879)、[#42619](https://github.com/openai/codex/issues/42619)）
- **实验性 worktree 支持**：可通过 `--worktree` 或 `/worktree` 为新建或 fork 的会话创建独立代码检出，并支持浏览与恢复。（[#42652](https://github.com/openai/codex/issues/42652)、[#43069](https://github.com/openai/codex/issues/43069)、[#43120](https://github.com/openai/codex/issues/43120)）

### 预发布版容器
- `rust-v0.154.0-alpha.6.1` / `alpha.8` / `alpha.10.2` / `alpha.11`（均为 Release 容器，未附带独立变更说明）

---

## 社区热点 Issues

### 1. Windows Codex App 频繁冻结/卡顿
**#20214** | 👍 87 | 💬 111 | [GitHub](https://github.com/openai/codex/issues/20214)
Windows 11 Pro 用户报告 Codex App 在系统资源充足的情况下依然频繁卡顿、UI 无响应。该问题自 4 月创建以来持续数月未关闭，评论数过百，是当前 Windows 平台最受关注的稳定性缺陷之一。

### 2. 后台进程轮询浪费 Token：每次 write_stdin 轮询都触发完整 API 回合
**#13733** | 👍 40 | 💬 40 | [GitHub](https://github.com/openai/codex/issues/13733)
当 `cargo build` 等后台进程运行时，Codex 进入轮询循环，**每次状态检查都携带完整对话历史进行 API 往返**，导致 Token 消耗随历史长度与轮询次数乘积级放大。社区强烈期待轮询逻辑优化。

### 3. Windows Computer Use 截图失败：SetIsBorderRequired 接口不支持
**#25178** | 👍 23 | 💬 53 | [GitHub](https://github.com/openai/codex/issues/25178)
Windows 10 22H2 上 Computer Use 可枚举窗口、发送键盘输入，但 `get_window_state` 请求截图时在捕获前即失败，报错 `SetIsBorderRequired failed: 不支持此接口 (0x80004002)`，严重限制桌面自动化能力。

### 4. Codex Desktop 等待/状态轮询期间重复进入模型，消耗大量 Credits
**#35259** | 👍 19 | 💬 22 | [GitHub](https://github.com/openai/codex/issues/35259)
在多代理（Ultra/multi-agent）工作流中，Codex Desktop 仅为了等待代理或轮询终端状态就反复重新进入模型。实测显示仅 wait/status 轮询的模型回合即占本地 Token 总消耗的 **19.8%**，与 #13733 同源。

### 5. Windows/Android 远程项目同步不对称，新项目不出现且触发信任门
**#41470** | 👍 3 | 💬 16 | [GitHub](https://github.com/openai/codex/issues/41470)
早期创建的 Codex 项目可在 Windows 与 Android 间正常同步，但后续在桌面新建的项目无法出现在移动端；由移动端发起的线程反而触发信任确认（trust gate）。远程同步一致性亟待修复。

### 6. Codex CLI/Desktop 会话存储无边界增长，可达数百 GiB
**#34337** | 👍 2 | 💬 11 | [GitHub](https://github.com/openai/codex/issues/34337)
Codex CLI 与 Desktop 共享本地 rollout/session 存储，在长时间正常运行下可从几十 GiB 增长至数百 GiB 甚至 TiB 级，远超单个 zstd 设置可控制的范畴，磁盘空间压力显著。

### 7. Windows 桌面 App：进程启动但窗口永不出现
**#42669** | 👍 0 | 💬 8 | [GitHub](https://github.com/openai/codex/issues/42669)
在 Windows 11 (25H2) 上，Codex Desktop App (26.901.2854.0) 的进程正常运行，但 UI 窗口始终不显示，日志提示 `Artifact Session host Unix-socket transport is not available on Windows`。同一环境中 CLI 0.153.0 可正常使用。

### 8. macOS Remote Control：配对成功但主机保持 Offline，WebSocket 握手 503
**#44316** | 👍 0 | 💬 2 | [GitHub](https://github.com/openai/codex/issues/44316)
最新版 Codex App (26.903.61454) 在 macOS 上可成功完成配对，但主机始终显示离线，WebSocket 握手返回 HTTP 503。影响跨设备远程连接能力。

### 9. 本地会话/跟踪存储增长无边界（跟踪 Issue，由 Codex 自主生成）
**#42648** | 👍 0 | 💬 2 | [GitHub](https://github.com/openai/codex/issues/42648)
由 Codex 全自主研究并起草的跟踪 Issue，汇总了多个交互机制共同导致本地会话存储无边界增长的问题。该 Issue 以 AI 自主操作账户发布，反映 Codex 自身用于工程分析的实践深度。

### 10. VS Code Codex Chat 代码块丢失语法高亮
**#41659** | 👍 5 | 💬 3 | [GitHub](https://github.com/openai/codex/issues/41659)
最新 VS Code + Codex 扩展中，Chat 面板的围栏代码块不再语法高亮，近乎纯灰/白单色渲染，编辑器内正常，问题疑似局限于 Chat Webview。影响日常代码审阅体验。

---

## 重要 PR 进展

> 过去 24 小时内合并/关闭的 PR 均由 `copyberry[bot]` 提交，集中围绕托管守护进程恢复、Guardian 安全预算与沙箱逃逸加固。

### 1. 三次空自动续行后阻塞目标
**#44320** | [GitHub](https://github.com/openai/codex/pull/44320)
自动目标续行若连续三次返回空最终答案且无其他进展，将目标标记为 `blocked`，防止无进展循环消耗资源。

### 2. 受管守护进程重启时恢复已保存线程
**#44314** | [GitHub](https://github.com/openai/codex/pull/44314)
守护进程启动时消费恢复快照，在后台恢复线程，使活动目标无需等待客户端重连即可继续执行。

### 3. 遵循共享 Retry-After 截止时间（远程控制）
**#44311** | [GitHub](https://github.com/openai/codex/pull/44311)
修复远程控制请求可通过配对、认证变更或重连绕过服务器 `Retry-After` 延迟限制的问题；主动令牌刷新在服务器明确延迟时也不再继续使用旧令牌。

### 4. 阻止受限文件系统沙箱中的 WSL 互操作逃逸
**#44286** | [GitHub](https://github.com/openai/codex/pull/44286)
安全加固：网络启用时 WSL interop 可绕过 Linux 文件系统沙箱启动 Windows 进程（甚至通过 `wsl.exe` 以 root 重新进入发行版）。PR 在 bubblewrap 内掩蔽 WSL interop sockets，封堵逃逸路径。

### 5. 记录受管守护进程关闭时的线程恢复候选
**#44299** | [GitHub](https://github.com/openai/codex/pull/44299)
优雅关闭时将已成功持久化的根线程 ID 原子保存至 `loaded-threads.json`，排除临时线程与待卸载线程，并在启动时清理过期恢复数据。

### 6. 强制执行异步 Guardian classifier 的完整输入预算
**#44293** | [GitHub](https://github.com/openai/codex/pull/44293)
异步审查须在发送给 classifier 前计入完整请求上下文，包括父压缩检查点与图像，避免超出模型上下文窗口。

### 7. 为 Guardian 审查强制执行完整请求预算
**#44281** | [GitHub](https://github.com/openai/codex/pull/44281)
审查证据可能本身在限额内，但加入历史、工具、输出格式与提醒后超出reviewer上下文窗口；工具续行也可能使既有审查超限。此 PR 从模型配置解析输入限额并前置拦截。

### 8. 防止命令 Hooks 在阻塞 stdin 时挂起
**#44288** | [GitHub](https://github.com/openai/codex/pull/44288)
修复写入 hook 输入前未排空输出导致的管道缓冲死锁；stdin 写入被移入超时控制内，避免从不读取输入的 hook 无限挂起。

### 9. 为 Guardian 和 Memory 请求设置 turn 触发器
**#44298** | [GitHub](https://github.com/openai/codex/pull/44298)
在请求元数据中为 `guardian_review`、`guardian_classifier`、`memory_consolidation` 等填充 `turn_trigger`，提升遥测可观测性，区分系统触发与用户触发回合。

### 10. 受管守护进程关闭前持久化已加载线程
**#44283** | [GitHub](https://github.com/openai/codex/pull/44283)
通过隐藏的 `--managed-daemon` 标志，在关闭前持久化包括延迟 rollout 的空闲线程；当 rollout I/O 阻塞时仍可强制关闭，兼顾可靠性与可终止性。

---

## 功能需求趋势

综合近期 Issues 与 PR，社区关注的功能方向呈现以下趋势：

| 方向 | 需求/Feature | 典型 Issue/PR |
|---|---|---|
| **新模型支持** | GPT-6-Astra 接入正式发布，进入模型选择器与 Bedrock | [#42879](https://github.com/openai/codex/issues/42879) 等 |
| **国产化会话隔离** | Worktree 隔离检出、自定义 worktree 后端（Jujutsu `jj` 社区呼声较高，👍 27） | [#42652](https://github.com/openai/codex/issues/42652)、[#26648](https://github.com/openai/codex/issues/26648) |
| **Token/费用效率** | 消除 wait/status 轮询导致的重复 API 全景往返；移除 60 秒阻塞等待限制 | [#13733](https://github.com/openai/codex/issues/13733)、[#35259](https://github.com/openai/codex/issues/35259)、[#31935](https://github.com/openai/codex/issues/31935) |
| **Windows 一等公民** | 修复 App 卡顿、Computer Use 截图失败、WSL2 路径迁移、Remote 控制不可用等系统性短板 | [#20214](https://github.com/openai/codex/issues/20214)、[#25178](https://github.com/openai/codex/issues/25178)、[#42984](https://github.com/openai/codex/issues/42984) |
| **沙箱安全加固** | 拦截 WSL interop 逃逸、MXC 卷权限细化、Windows 系统配置命名空间探测 | [#44286](https://github.com/openai/codex/pull/44286)、[#44289](https://github.com/openai/codex/pull/44289)、[#44284](https://github.com/openai/codex/pull/44284) |
| **状态持久化与恢复** | 托管守护进程关闭/重启时线程保存与恢复、rollout 迁移保留历史 | [#44283](https://github.com/openai/codex/pull/44283)、[#44299](https://github.com/openai/codex/pull/44299)、[#44314](https://github.com/openai/codex/pull/44314)、[#38762](https://github.com/openai/codex/issues/

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 2026-09-10

## 今日速览

昨日发布 nightly v0.61.0 版本，主要针对 NTFS 路径兼容性与沙箱配置隔离进行修复。社区讨论集中在 **Agent 工作流可靠性**（MAX_TURNS 误报、Generalist 挂起）与**安全加固**（提示注入防护、沙箱边界）两大方向。目前已有 10 余个高优先级 issue 处于维护者追踪/待回归验证状态，且大量改进围绕 Auto Memory 与子代理行为展开。

## 版本发布

### v0.61.0-nightly.20260909.ged2ac40df
- **fix(core)**：缓解 NTFS 8.3 短文件名（SFN）路径导致的问题
- **fix(cli)**：在沙箱容器中隔离 settings 目录，避免主机配置干扰容器运行

## 社区热点 Issues（Top 10）

### 1. Subagent 达到 MAX_TURNS 被误报为 GOAL 成功
**#22323** | [BUG][P1] | 13 评论 | 👍 2
`codebase_investigator` 子代理在命中最大轮次限制后，自身结果已表明"未做任何分析"，却仍向主会话上报 `status: "success"` 与 `Termination Reason: "GOAL"`，导致中断被隐藏、用户误判任务完成。
🔗 https://github.com/google-gemini/gemini-cli/issues/22323

### 2. Generalist Agent 无限挂起
**#21409** | [BUG][P1] | 8 评论 | 👍 8
多个用户反馈一旦 Gemini CLI 将任务委托给 generalist agent（如简单的创建文件夹操作）便永久挂起，等待超过 1 小时仍无响应。明确指示模型不要使用子代理可绕过该问题。
🔗 https://github.com/google-gemini/gemini-cli/issues/21409

### 3. 利用模型原生的 bash 亲和力，实现零依赖 OS 沙箱
**#19873** | [ENHANCEMENT][P2] | 9 评论 | 👍 1
提议利用 Gemini 3 模型天然擅长链式调用 POSIX 工具的特点，建立更安全的 OS 沙箱与执行后意图路由机制，在不牺牲安全性的前提下释放模型原生能力。
🔗 https://github.com/google-gemini/gemini-cli/issues/19873

### 4. 评估 AST 感知的文件读取/搜索/映射价值
**#22745** | [FEATURE][P2] | 7 评论 | 👍 1
EPIC 追踪一系列调查：AST 感知工具能否通过精确读取方法边界、减少对齐偏差的读取、降低 token 噪声，显著提升代码探索效率。
🔗 https://github.com/google-gemini/gemini-cli/issues/22745

### 5. Gemini 不会主动使用 skills 与 sub-agents
**#21968** | [BUG][P2] | 6 评论
用户反馈（虽为轶事证据）模型几乎不会主动使用自定义 skills 和子代理，即便已有明确描述的 `gradle`/`git` 等技能，仍需显式指令才会调用。
🔗 https://github.com/google-gemini/gemini-cli/issues/21968

### 6. Shell 命令执行完毕后卡在"Waiting input"
**#25166** | [BUG][P1] | 4 评论 | 👍 3
简单 CLI 命令执行完成后，终端仍显示命令激活且"等待用户输入"并挂起。该问题可稳定复现，涉及 shell 执行状态机的缺陷。
🔗 https://github.com/google-gemini/gemini-cli/issues/25166

### 7. Auto Memory 缺少确定性脱敏，且日志过多
**#26525** | [SECURITY][P2] | 5 评论
Auto Memory 在将本地 transcript 送入后台提取模型前，并未先执行确定性机密脱敏——而是在内容已进入模型上下文后才提示模型自行编辑。同时服务日志可能记录现有技能内容，存在泄露风险。
🔗 https://github.com/google-gemini/gemini-cli/issues/26525

### 8. Browser Subagent 在 Wayland 环境下失败
**#21983** | [BUG][P1] | 4 评论 | 👍 1
Browser subagent 在 Wayland 会话中运行失败，`Termination Reason: GOAL` 但实际未完成任务，怀疑与显示服务器/浏览器启动参数兼容性有关。
🔗 https://github.com/google-gemini/gemini-cli/issues/21983

### 9. Auto Memory 对低信号会话无休止重试
**#26522** | [BUG][P2] | 4 评论
只有当后台提取代理成功读取 transcript 后，会话才被标记为已处理。若代理判断某会话低信号而跳过读取，该会话会反复出现在待处理队列中，造成无效重试。
🔗 https://github.com/google-gemini/gemini-cli/issues/26522

### 10. /compress 命令无法跨会话/恢复持久化
**#21335** | [BUG][P2] | 2 评论 | 👍 2
`/compress` 虽能正确压缩当前内存中的对话历史，但压缩结果不会回写到磁盘上的 session 文件，恢复会话时历史仍然完整——压缩形同虚设。
🔗 https://github.com/google-gemini/gemini-cli/issues/21335

## 重要 PR 进展（Top 10）

### 1. 防止通过构建文件与不可信参数进行间接提示注入
**#29250** | [fix/core] | OPEN | size/xl
重构受限工作区模式下的内建执行路径（`shell`、`edit`、`write_file`），加强工作区边界校验——重点覆盖构建配置文件与外部命令参数，阻止间接提示注入。
🔗 https://github.com/google-gemini/gemini-cli/pull/29250

### 2. 加固沙箱文件系统边界并隔离运行时状态
**#29214** | [fix/sandbox] | OPEN | size/l · xl
将沙箱运行时状态与主机配置目录隔离；以"净化后的配置文件"替代主机目录挂载；统一使用 realpath 做路径敏感性检查，并为不存在路径提供兜底。
🔗 https://github.com/google-gemini/gemini-cli/pull/29214

### 3. 修复中断轮次导致的会话上下文污染
**#29265** | [fix/agent] | OPEN | size/m | area/agent
SIGINT、超时或工具执行中止会污染当前聊天会话历史，破坏后续指令执行。此 PR 在中断发生时清理/回滚进行中的 generation 与 tool execution 上下文。
🔗 https://github.com/google-gemini/gemini-cli/pull/29265

### 4. 修复 Git 仓库内 macOS Seatbelt 下启动崩溃（认证流程）
**#29163** | [fix/cli][P1] | OPEN | size/l | area/security
`useGitBranchName` hook 在受限权限环境（macOS Seatbelt / 其他沙箱）读取 `.git` 时导致 CLI 启动崩溃。PR 针对"git 仓库 + 受限权限"场景增加防护。
🔗 https://github.com/google-gemini/gemini-cli/pull/29163

### 5. 不再在 Shell 执行中清空用户 Git 配置
**#29156** | [fix/core] | OPEN |

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-09-10）

## 今日速览
今日发布补丁版本 v1.0.84-3，修复了 `/copy` 遗漏任务完成消息及 OAuth 认证 MCP 服务器的连接可靠性问题。社区热点集中于两个方向：一是 Windows 平台会话创建与终端渲染的持续性问题（#4756、#3700），二是 `400 input item ID does not belong to this connection` 连接错误在多场景下的复发（关联 #2147、#4791）。另有多个新提交的高优先级问题等待 triage，其中 Windows 沙箱路径权限与听写输入异常值得关注。

## 版本发布
**v1.0.84-3** 补丁版本，包含两项修复：

- `/copy` 现在会包含任务完成消息（task completion messages）
- OAuth 认证的 MCP 服务器在会话启动阶段的连接可靠性得到修复

## 社区热点 Issues
### 1. Light theme doesn't work — #135
**评论 12 | 👍 12** | 创建于 2025-09-30，持续未关闭
浅色主题终端下界面仍以深色渲染，影响版本 0.0.330。该问题已持续近一年仍未被解决，且有新提交的同类问题（#3773），社区对主题支持的不满正在累积。
🔗 https://github.com/github/copilot-cli/issues/135

### 2. Windows 上新会话创建前需归档所有空闲项目会话 — #4756
**评论 7 | 👍 19** | 创建于 2026-09-07
Windows 桌面应用在已有会话存在时创建新会话报 `Failed to create session: invalid argument`。19 个 👍 说明影响范围较大，且属于阻塞性功能缺陷而非体验优化。
🔗 https://github.com/github/copilot-cli/issues/4756

### 3. `store_memory` 在 v1.0.81 prerelease 中稳定失败 — #4535
**评论 8** | 版本 v1.0.81 prerelease
原生内存写入器被调用时缺少必需的 instance ID，导致记忆功能不可用。属于核心功能的回归问题。
🔗 https://github.com/github/copilot-cli/issues/4535

### 4. CAIP 400 错误：input item ID does not belong to this connection — #2147
**评论 6** | 已关闭
`gpt-5.4 (xhigh)` 下 websocket 连接抛出 400 错误。虽然该 issue 已关闭，但同类问题仍在新场景中出现（见 #4791），连接上下文管理可能仍存在系统性缺陷。
🔗 https://github.com/github/copilot-cli/issues/2147

### 5. `--yolo` / `--allow-all` 被无策略账户的 fail-closed 限制误伤 — #4757
**评论 3** | 版本 1.1.15（app）/ 1.0.83-5（CLI）
企业托管设置中 fail-closed 策略被解析为 absent，但 bypass-permissions mode 仍在整个会话中被禁止。影响自动化流程的高权限模式使用。
🔗 https://github.com/github/copilot-cli/issues/4757

### 6. WSL2 回归：CLI 主线程空转占 215% CPU — #3700
**评论 3** | 标记 High severity
v1.0.60 在 WSL2 下 TUI 输出冻结，主线程空转占用约 215% CPU，直到重启才能恢复。为 #2208 回归，每次新会话必现。影响 WSL2 用户的日常开发。
🔗 https://github.com/github/copilot-cli/issues/3700

### 7. Ctrl+Backspace 删除整个单词 — #2199
**评论 3 | 👍 7**
编辑器通用快捷键在 CLI 输入中不可用。Windows 用户同样反馈该问题（#3858，👍 6）。小需求，但反映跨平台输入体验的一致性欠缺。
🔗 https://github.com/github/copilot-cli/issues/2199

### 8. 原生 `tgrep` 索引器在大规模 monorepo 上 OOM 杀死宿主机 — #3976
**评论 3**
tgrep 守护进程无内存上限，在大规模代码仓库中启动即可拖垮宿主机。属于实验特性，但会严重影响开启该实验的用户。
🔗 https://github.com/github/copilot-cli/issues/3976

### 9. Mission Control 仪表盘链接 404 — #4775
**评论 3** | 创建于 2026-09-09
Dashboard 渲染远程会话链接指向 `/copilot/tasks/<uuid>`，实际会话存在于 `/agents/tasks/<uuid>`。外部任务管理界面存在错误 URL 路径。
🔗 https://github.com/github/copilot-cli/issues/4775

### 10. 辅助权限模式约 1 小时后自动失效 — #4764
**评论 1** | 版本 1.0.83
权限模式只会自动停止工作，需要重启会话才能恢复。对长会话工作流的自动化有负面影响。
🔗 https://github.com/github/copilot-cli/issues/4764

## 重要 PR 进展
过去 24 小时仅有 2 个 PR 更新，均为文档变更，无代码功能合入：

### 1. Revise notice regarding third-party services — #4786
修订第三方服务相关声明，明确访问要求与条款。
🔗 https://github.com/github/copilot-cli/pull/4786

### 2. Document the WebSocket responses opt-out — #4770
为支持 WebSocket responses 的模型新增传输层退出机制文档。当 WebSocket 被网络阻断或遭遇 `400 input item ID does not belong to this connection` 错误时，提供可用的备选方案。社区中存在多个由同一错误引发的 issue（#2147、#4791），此文档可帮助开发者自我排查。
🔗 https://github.com/github/copilot-cli/pull/4770

## 功能需求趋势
以下方向频繁出现在近期 issue 中：

- **终端交互一致性**：Ctrl+Backspace 跨平台支持（#2199、#3858），但该快捷键在 Windows 上仍不可用；macOS 下 Ctrl+C 复制文本与取消对话框的冲突（#4789）
- **主题与可访问性**：浅色主题失效（#135、#3773），以及固定浅色/深色主题的开关功能（#4620）——部分用户希望将 GitHub 主题固定为深色，不随系统外观变化
- **MCP 生态完善**：带认证信息的 MCP registry 读取，适应企业安全要求（#3772）；OAuth 服务器重定向场景的兼容（#4769）；MCP 工具发现的准确性问题（#4773）
- **多账户支持**：在多个 GitHub 账户（个人、企业）之间快速切换（#367）
- **插件依赖管理**：市场插件需要跨/内部依赖声明与自动安装机制（#4487）
- **会话与上下文恢复**：开发者在系统重启之后难以快速恢复最近的会话，期望 CLI 默认回到上次会话或主动询问（#1467）

## 开发者关注点
- **连接错误反复出现且恢复手段有限**：`input item ID does not belong to this connection` 错误在不同场景下持续出现。核心问题表现为：因误用错误用户账户切换导致的不可恢复错误提示，重启会话仍不能解决（#4791）。该问题在 gpt-5.4 等模型下影响严重。
- **权限模式稳定性不足**：辅助权限模式在会话运行约 1 小时后自动失效、无日志提示（#4764），一局长时间开发会话往往需要手动重启服务；fail-closed 策略误判同样会引起高权限模式被限制（#4757）。
- **平台特定问题积聚**：Windows 相关的会话创建失败、任务栏状态卡死（#4771）、通知角标不清空（#4381）、WSL2 CPU 空转（#3700）等多类问题仍然活跃，且部分已标记为高危、等待修复。
- **MCP 配置与读取鲁棒性**：在非仓库根目录下运行 CLI 时配置读取失效（#4765），MCP 服务器发现机制反复报告 0 个工具（#4773），以及 OAuth 服务器重定向导致的认证失败（#4769）等问题严重影响 MCP 生态的集成体验。
- **体验细节问题**：远程 SSH 会话中复制命令报告成功但剪贴板为空（#4551）、听写模式下内容被周期性删除（#4787）等输入输出异常干扰日常工作流。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-09-10

## 1. 今日速览

过去 24 小时未发布新版本，社区活跃度主要集中在 4 个 Issue 与 1 个 PR 的更新上。值得关注的是：macOS 端 `/login` 设备认证流程出现 HTTP 500 问题，另有 Windows 终端下阿拉伯语（RTL）文本反转显示的 bug 报告；同时一项针对 FetchURL 重复提取文本的修复 PR 已关闭。此外，VSCode 扩展的 @ 文件上下文选择优化和 Web 端"引用与回复"功能需求仍在持续发酵。

---

## 2. 版本发布

过去 24 小时内无新版本 Release。

---

## 3. 社区热点 Issues

过去 24 小时内有更新的 Issue 共 4 条，以下全部列出。由于单日增量较少，暂不涉及 10 条筛选。

### #2638 ｜ `/login` 设备认证在浏览器批准后返回 HTTP 500（CLI v0.42.0, macOS）
- **状态**: OPEN ｜ **更新**: 2026-09-09 ｜ **评论**: 0
- **影响**: 登录流程中断，用户在浏览器中批准设备码后 CLI 仍报错；该问题同时影响 CLI 与 VS Code 扩展，且发生在 Free 计划账号（Adagio）上——影响面较大。
- **摘要**: 执行 `/login` → 浏览器打开设备码页 → 用户批准 → CLI/VS Code 侧返回 HTTP 500。问题可稳定复现。
- **为什么重要**: 认证是使用所有功能的前置条件，macOS + VS Code 双重命中意味着这不是孤立环境问题。
- [GitHub 链接](https://github.com/MoonshotAI/kimi-cli/issues/2638)

### #2639 ｜ Windows 终端下阿拉伯语（RTL）文本字符级反转显示
- **状态**: OPEN ｜ **更新**: 2026-09-09 ｜ **评论**: 0
- **影响**: 在交互式 `kimi` 提示框中直接输入阿拉伯语，回声以「每个字符逐字反转」顺序呈现；当 AI 回复中包含阿拉伯语与拉丁文/数字混排时也出现同样反转。
- **摘要**: RTL 语言用户的基本输入/输出显示受损，属于终端渲染层可能未正确应用双向文本算法（bidi）的问题。
- **为什么重要**: 该问题直接阻碍阿拉伯语用户使用 CLI，属于国际化与可访问性缺口；修复范围可能涉及终端 UI 库或输出编码层。
- [GitHub 链接](https://github.com/MoonshotAI/kimi-cli/issues/2639)

### #1270 ｜ [增强] VSCode 扩展：敲入 `@` 后应优先显示已打开的文件
- **状态**: CLOSED ｜ **创建**: 2026-02-27 ｜ **更新**: 2026-09-09 ｜ **评论**: 1
- **背景**: 版本 v0.4.3。用户在对话框输入 `@` 时，备选文件列表应优先展示 VSCode 当前已打开的文件，因为大概率意图是对这些文件进行分析和操作。
- **为什么重要**: 虽然该 Issue 在几个月前被关闭，但更新于 9 月 9 日（可能是关联 PR 或评论触发的重新讨论），反映出**上下文感知的文件选择**仍是 IDE 集成的高频诉求。
- [GitHub 链接](https://github.com/MoonshotAI/kimi-cli/issues/1270)

### #2601 ｜ [功能请求] 引用与回复：可对 AI 回复中任意选区进行评论
- **状态**: CLOSED ｜ **创建**: 2026-08-11 ｜ **更新**: 2026-09-09 ｜ **评论**: 0
- **内容**: 希望 Kimi Web 支持引用回复——用户可选中 AI 回复中的任意文本片段（段落/代码块/计划步骤/diff 行），针对该精确选区附加评论或追问，让 agent 基于选区继续工作。
- **为什么重要**: 该请求虽然针对 Kimi Web，但「精细位置引用」的交互模式也可能影响 CLI/编辑器端用户在对话中对代码片段进行锚定评论的预期；其被关闭可能意味着已被内部路线图吸收或存在替代方案。
- [GitHub 链接](https://github.com/MoonshotAI/kimi-cli/issues/2601)

---

## 4. 重要 PR 进展

过去 24 小时内更新的 PR 仅 1 条。

### #1863 ｜ fix(fetch): 抑制重复的摘录评论文本
- **状态**: CLOSED ｜ **创建**: 2026-04-13 ｜ **更新**: 2026-09-09 ｜ 点赞: 0
- **问题根因**: HTML 提取路径中，Trafilatura 同时提取正文（main text）与评论（comments）；当前逻辑未做去重，当评论规范化后与正文内容相同，搜索结果被去重，但提取（fetch）输出中出现重复文本。
- **修复内容**:
  - 切换 `FetchURL` 的 HTML 提取路径，使其分别检查 Trafilatura 的正文与评论；
  - 当评论规范化后与正文一致时抑制重复评论；
  - 为 GitHub Issue 提取输出重复问题添加回归测试。
- **意义**: 当你让 CLI 抓取一个 GitHub Issue/讨论页时，返回的摘要将更干净，不再出现大段重复文本——对使用 fetch 功能做代码审查/资料汇总的用户是直接体验优化。
- [GitHub 链接](https://github.com/MoonshotAI/kimi-cli/pull/1863)

---

## 5. 功能需求趋势

基于近期 Issues 的整体走向（包括今日 4 条，并参考社区积累的历史需求），可以观察到以下方向：

- **认证与账号体验**：设备授权流程的可靠性。`/login` 的 HTTP 500 并非孤例，CLI 认证（device code flow）的端到端稳定性是高频关注点，尤其是浏览器与终端交互的部分。
- **IDE 集成深化**：VSCode 扩展需要更强的上下文推断，如 `@` 触发时需要按「当前打开文件 > 工作区文件 > 历史文件」的优先级排序，而非通用列表。
- **精细化对话交互**：用户期望能对 AI 输出中的任意片段进行「选区级」引用与追问，该模式在 Web 端、CLI 端与编辑器端均有适用空间（diff 行、代码块、计划步骤等均为锚点场景）。
- **国际化 / 本地化**：非拉丁文字系统（从 RTL 文本到 CJK）在终端 UI 中的渲染正确率成为新痛点，说明用户群正在明显扩展至非英语地区。

---

## 6. 开发者关注点

- **登录链路脆弱性**：多个环境（macOS + VS Code + Free 计划）下均出现批准后 HTTP 500，开发者会质疑该错误是否因服务端状态码处理不当或设备码轮询逻辑缺陷导致；同时希望错误信息能更加友好，而不是单纯抛出一个 500。
- **多语言文本渲染质量**：Windows Terminal 下的 RTL 反转问题提示 CLI 所依赖的终端 UI 或输出缓冲对 Unicode 双向算法的支持不足；类似问题未来也可能出现在其他复杂文本（如 emoji 变体、组合字符）场景。
- **抓取结果的去重与准确性**：#1863 的修复源自 GitHub Issue 页面提取出现重复内容，说明开发者信息检索流程中对「无噪声」的需求正在上升——他们希望 fetch 工具能像人一样区分正文与评论，而不是一股脑拼在一起。
- **高频需求未被有效回应（潜在不满）**：#1270 中「@ 优先展示打开文件」与 #2601 的「选区引用」提出了数月至半年，但至今陆续以 CLOSED 状态收尾——社区可能期待官方对其落地路线或替代方案（如通过 `.kimircc`、API 或快捷命令模拟）给出更明确的指引。

---

以上为 2026-09-10 日报全量内容，过去 24 小时动态条目较少，无新增版本、Issue 与 PR 均非首次创建而是有更新进展。如需追踪明日增量，建议重点关注 #2638（认证 500）是否会快速获得服务端修复，以及 #2639（RTL）是否进入 triage 阶段。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-09-10

## 1. 今日速览

OpenCode 发布 v1.18.30，修复 Bedrock DeepSeek 模型 ID 解析并更新 Azure/OpenAI provider SDK。社区端，配置热重载（#8751）与 `@` 文件索引滞后（#32747）仍是讨论热度最高的两大议题；PR 侧则集中于桌面端会话加载性能、TUI 启动竞态与 ACP 会话边界修复。

## 2. 版本发布

### v1.18.30
- **Core 改进**：为 GPT-6 模型新增 Astra system prompt。
- **Bugfixes**：
  - 保留 Bedrock DeepSeek 模型 ID（含 ARN 格式），确保正确解析（@YeEmrick）。
  - 更新 Azure provider SDK，修复兼容性问题。
  - 更新 OpenAI provider SDK，同步上游修复。

## 3. 社区热点 Issues（10 个）

1. **[#8751 Hot-reload agents, skills and commands](https://github.com/anomalyco/opencode/issues/8751)** — 社区呼声最高的功能请求（👍 96，评论 23）。用户希望在 OpenCode 运行中动态加载配置、新建 agent/skill 而无需重启。长时间未关闭说明需求持续性强。

2. **[#32747 @ 文件提示不包含启动后新建文件](https://github.com/anomalyco/opencode/issues/32747)** — 这是一个影响日常开发效率的 bug：启动后新建的文件无法通过 `@` 检索到，重启后恢复正常。评论 16，开发者普遍认为 TUI 的搜索状态存在陈旧缓存。

3. **[#18654 OpenCode Zen 无法修改/删除邮箱](https://github.com/anomalyco/opencode/issues/18654)** — 账户管理缺陷：更换 GitHub 邮箱后出现重复用户。评论 7，涉及账户体系完整性问题，值得官方重视。

4. **[#39491 Plan 模式可通过 bash 绕过限制写文件](https://github.com/anomalyco/opencode/issues/39491)** — Claude Sonnet 4.6 在 plan 模式下忘记约束，改用 `cat > file` 直接写 SKILL.md。反映模式约束在模型调用层存在绕过路径，属于安全边界问题。

5. **[#47034 Gemini 3.8 Flash 报错 “Requests ending with a model turn are not supported”](https://github.com/anomalyco/opencode/issues/47034)** — Gemini 3.8 Flash 在新版本 API 下出现 400 错误，与消息轮次格式有关，影响 Google 新模型接入。

6. **[#48237 Settings 中 auto-accept 开关在无 session 时置灰](https://github.com/anomalyco/opencode/issues/48237)** — 用户提交了包含根因分析和修复设计的完整报告（涉及 `createPermissionScopeController`），并关联了 #37617 / #45159 / #31137 同类问题。质量较高，便于维护者直接跟进。

7. **[#42238 `opencode run --format json` 将自动压缩内部信息混入普通文本事件](https://github.com/anomalyco/opencode/issues/42238)** — JSONL 消费者无法区分 compaction 摘要与真实用户/助手消息，破坏自动化流程的数据解析。属于可观测性与输出规范问题。

8. **[#41571 Kimi K3-256K 自 v1

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-09-10）

## 今日速览

Qwen Code 今日发布稳定版 **v0.23.2**，主要改进 Web Shell 分屏会话导航体验；终端 / 守护进程侧稳定性问题则成为社区讨论焦点，其中 Windows 下 `conhost.exe` 泄漏问题（#11303）与 VS Code 扩展升级后丢失会话历史（#11489）最受关注。版本节奏方面，官方同时推进 SDK TypeScript v0.1.11 和 cua-driver-rs v0.20.5 发布，持续补齐工具链与跨平台支撑。

## 版本发布

过去 24 小时共发布 4 个版本/制品：

- **Qwen Code v0.23.2**（最新稳定版）：主要包含 Web Shell 分屏会话导航改进（[#11250](https://github.com/QwenLM/qwen-code/pull/11250)）；无已知 Breaking Changes。
- **v0.23.2-nightly.20260909.2e212144d3**：针对 goal 机制修复——当 checkpoint 超出预算时执行重试，不再 stal（[#11365](https://github.com/QwenLM/qwen-code/pull/11365)）。
- **sdk-typescript-v0.1.11**：捆绑 CLI 0.23.2 构建版本。
- **cua-driver-rs v0.20.5**：Qwen CUA Driver 预编译跨平台二进制，macOS 版完成签名与公证，Windows 版含 UIAccess worker。

## 社区热点 Issues

过去 24 小时有 50 条 Issue 更新，以下为最受关注的 10 条：

1. **[[P1] Windows 下 qwen-cli 泄漏 conhost.exe 进程：347 个进程 / 约 2.8 GB 内存](https://github.com/QwenLM/qwen-code/issues/11303)**
   VS Code Companion 内嵌的 qwen-cli 运行 12 小时后产生大量 ConPTY 子进程且不释放，评论数 12 条，是目前社区反馈最强烈的 Windows 性能问题。

2. **[[P1] 扩展更新丢失全部会话历史（v0.21.x → v0.23.x）](https://github.com/QwenLM/qwen-code/issues/11489)**
   用户升级 VS Code 扩展后发现侧边栏历史会话全部消失，`state.vscdb` 仍在但新版不再读取。涉及数据可访问性，社区反应迅速。

3. **[[P1] TUI 静默退出：多个后台 agent 完成时触发 React #185](https://github.com/QwenLM/qwen-code/issues/11500)**
   多个后台子代理短时间内相继完成时，`useBoxMetrics` 布局监听触发 setState 死循环，CLI 直接退出到 shell，影响无人值守场景。

4. **[[P1] node-pty 自然退出时泄漏 ConPTY host](https://github.com/QwenLM/qwen-code/issues/11352)**
   从 #11303 中拆分出的另一独立缺陷：baton 在 `onExit` 前被清除，导致 `ClosePseudoConsole` 无法从 JS 层调用，受限于上游依赖。

5. **[[P1] 会话运行时回收时后台 shell 输出与唤醒通知丢失](https://github.com/QwenLM/qwen-code/issues/11119)**
   `qwen serve` 的 Web Shell 会话中，后台轮询任务在 turn 结束后继续运行，但输出和通知被静默丢弃，最终导致会话卡死。

6. **[[P2] 预中止的工具请求可能排在无关活动批次之后](https://github.com/QwenLM/qwen-code/issues/11146)**
   `CoreToolScheduler.schedule()` 在批次未结束时将已取消请求加入队列；取消信号不会重放给后注册的监听器，导致请求无效等待。

7. **[[P2] .mcp.json 中 `${VAR}` 未被展开，密钥被字面发送](https://github.com/QwenLM/qwen-code/issues/11499)**
   用户在 `.mcp.json` 中使用 `Bearer ${MY_TOKEN}` 形式配置认证头，实际请求把 `${MY_TOKEN}` 原文发给了服务端，存在安全隐患。

8. **[[P2] 守护进程守卫拒绝工作区自身仓库：`.git` 为 junction/symlink 时连只读 git 命令也被拦截](https://github.com/QwenLM/qwen-code/issues/11503)**
   Windows 上将 meta 目录放在其他卷的 junction 时，`git status / log / diff` 全部被 guard 拒绝，影响合法本地开发流程。

9. **[[P3] 讨论：是否引入 SQLite 支撑 Session/Prompt 索引](https://github.com/QwenLM/qwen-code/issues/11433)**
   针对长会话、大量 session、精确 Prompt 查询与重连/附加等场景，社区发起设计讨论，建议用嵌入式 SQLite 改善历史检索性能。

10. **[[P3] feat(serve)：支持远程文件夹 —— 客户端连接远程 daemon](https://github.com/QwenLM/qwen-code/issues/11475)**
    基于现有远程 Web Shell 与 multi-workspace API，提出交互端在本地、daemon 和工作区在远程的开发工作流支持。

## 重要 PR 进展

过去 24 小时更新的 PR 共 50 条，以下为 10 个值得关注的变化：

1. **[fix(review): 将宿主可信状态移出容器的可写层](https://github.com/QwenLM/qwen-code/pull/9983)**
   把工作区 lease 文件从 `.qwen/tmp`（容器可写挂载）迁出，避免宿主侧 git 通过容器内指针解析，加固 review 沙箱隔离。

2. **[perf(export): 将 transcript 渲染器的内嵌 CSS 拆为独立版本化资源](https://github.com/QwenLM/qwen-code/pull/11485)**
   导出文档改为并行加载带版本号与 SRI 保护的 `export-transcript-document.css`，减小主文档体积。

3. **[fix(web-shell): 避免重复冷会话恢复](https://github.com/QwenLM/qwen-code/pull/11413)**
   打开既有会话时先完成工作区发现再恢复 transcript，Discard 的 StrictMode effect 会提前退出，防止重复初始化。

4. **[feat(serve): 将扩展作用域限定到 workspace 运行时](https://github.com/QwenLM/qwen-code/pull/11086)**
   全局扩展目录按工作区运行时隔离，统一 daemon/SDK 访问，并同步更新扩展管理、composer 添加菜单和 `@` 引用。

5. **[fix(cli): 加载项目 .mcp.json 时展开 `${VAR}` 占位符](https://github.com/Q

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*