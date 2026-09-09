# AI CLI 工具社区动态日报 2026-09-09

> 生成时间: 2026-09-09 00:21 UTC | 覆盖工具: 7 个

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

数据来源：github.com/anthropics/skills | 分析截止：2026-09-09

> 说明：本报告基于仓库 Issues 与 PR 的标题、摘要、关联讨论及生命周期状态。PR 列表中评论数字段未开放，关注度采用间接信号判断（Issue 讨论密度、复现数量、时间跨度、更新频率等）。

---

## 一、热门 Skills 排行

以下为当前社区关注度最高的 8 个 PR：

### 1. skill-creator：评估体系可信度修复（最热）
- **PR**: [#1298 fix(skill-creator): run_eval.py always reports 0% recall](https://github.com/anthropics/skills/pull/1298)
- **状态**: Open，2026-06 创建，持续更新
- **功能**: 修复 `run_eval.py` 在所有环境下报告 `recall=0%` 的严重问题——即 skill 描述优化循环实际在“对着噪声做优化”。修复点包括：将 eval artifact 安装为真实 skill、Windows 流读取、触发检测、并行 worker。
- **讨论热点**: 对应 Issue #556，已有 10+ 独立复现。skill 描述优化是 skill-creator 的核心闭环，该问题直接导致官方自动优化能力失效，是工具链领域影响面最大的单点故障。

### 2

---



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-09-09

## 1. 今日速览

- **v1.0.84-2 发布**，Vim 模式正式向所有用户开放，可直接通过 `/vim` 或 `editorMode` 配置开启。
- **Issue #13 圆满关闭**，社区呼声最高的 Vim 输入模式经过近一年的迭代终于落地，标志着 CLI 编辑器体验的重大完善。
- **会话（Session）问题持续高发**，Windows Local session 创建失败、会话恢复后 MCP 连接断开、内存泄漏刷爆 13GB 日志等多个问题正在被社区集中讨论和追踪。

## 2. 版本发布

### v1.0.84-2
> 链接: [GitHub Releases](https://github.com/github/copilot-cli/releases)

**新增功能**
- Vim 模式已全面开放：在 Composer 中可通过 `/vim` 命令或配置 `editorMode` 为 `vim` 开启模态编辑，输入时会实时显示当前模式。

**改进**
- 在支持的 Windows 沙箱策略下，交互式 shell 命令现在会记录被阻止的访问行为。

## 3. 社区热点 Issues（Top 10）

截至本日报统计时，仓库共有 44 条最近更新的 Issue，以下为最受关注的 10 条：

### ① #13 CLI input should have a vi/vim input mode（已关闭）
- **作者**: @RyanHecht | 💬 11 | 👍 76
- **链接**: https://github.com/github/copilot-cli/issues/13
- **为何重要**: 这是 Vim 模式的原始功能请求，获得 76 个赞，是社区最渴望的功能之一。今日随 v1.0.84-2 发布而告一段落，标志着该需求正式得到满足。

### ② #4756 Windows app requires archiving every idle project session before creating a new Local session
- **作者**: @TomHarveyBCM | 创建: 2026-09-07 | 更新: 2026-09-09 | 💬 6 | 👍 19
- **链接**: https://github.com/github/copilot-cli/issues/4756
- **为何重要**: 高赞（19👍），Windows 桌面板 1.1.15 的回归问题：一个项目只要有存活会话，就无法新建同项目的 Local 分支会话，严重阻塞多任务开发者。

### ③ #4742 Desktop app 1.1.15: cannot create a second Local (branch) session while one is running
- **作者**: @DannyBe99 | 创建: 2026-09-06 | 💬 10 | 👍 5
- **链接**: https://github.com/github/copilot-cli/issues/4742
- **为何重要**: 与 #4756 几乎同一问题，10 条评论显示影响面广。自动升级至 1.1.15 后触发回归，两个线程正在并行调查此缺陷。

### ④ #4612 Runaway FileWatch host-event loop freezes TUI and grows debug log to 13 GB
- **作者**: @tdihp | 创建: 2026-08-26 | 💬 9 | 👍 1
- **链接**: https://github.com/github/copilot-cli/issues/4612
- **为何重要**: FileWatch 事件陷入死循环，导致 TUI 卡死且 debug 日志膨胀至 13GB，属于严重的稳定性问题，正在 triage 流程中。

### ⑤ #4664 Copilot CLI crashes with JavaScript heap out of memory when resuming a long-standing session
- **作者**: @shrijitnair | 创建: 2026-08-30 | 💬 7 | 👍 2
- **链接**: https://github.com/github/copilot-cli/issues/4664
- **为何重要**: 恢复长期会话时 Node.js V8 堆内存溢出直接崩溃。对深度使用 CLI 的开发者影响较大，需要官方首先关注会话的持久化与恢复性能。

### ⑥ #2861 Compaction failed: received empty response from model (3x retry, manual /compact on Opus 4.6)
- **作者**: @ronkeele | 创建: 2026-04-20 | 💬 6 | 👍 4
- **链接**: https://github.com/github/copilot-cli/issues/2861
- **为何重要**: 老 issue 再次被更新提及。Opus 4.6 模型下 `/compact` 连续重试三次仍失败，暴露出模型空响应时的错误恢复逻辑缺陷。

### ⑦ #2943 openrouter integration
- **作者**: @asule90 | 创建: 2026-04-24 | 💬 3 | 👍 14
- **链接**: https://github.com/github/copilot-cli/issues/2943
- **为何重要**: 14 个 👍 表明仍然存在强烈兴趣：社区希望将 OpenRouter 集成到 copilot-cli 中，让它能够接入更多模型进行切换和选择。

### ⑧ #4753 v1.0.83: session resume cancels in-flight stdio MCP server connections (~1s timeout, was ~16s in v1.0.82)
- **作者**: @indeherb | 创建: 2026-09-07 | 💬 3 | 👍 1
- **链接**: https://github.com/github/copilot-cli/issues/4753
- **为何重要**: 会话恢复的超时时间从 v1.0.82 的 16s 骤降到 v1.0.83 的 1s，导致正在初始化的 stdio MCP 服务器被中断，加剧了会话恢复后的 MCP 工具不可用问题。

### ⑨ #4505 Resumed session retains stale connection item IDs after interrupted response
- **作者**: @Adamkadaban | 创建: 2026-08-16 | 💬 3 | 👍 3
- **链接**: https://github.com/github/copilot-cli/issues/4505
- **为何重要**: 恢复会话后每次 prompt 都报 “input item ID does not belong to this connection” 错误，且 `/fork` 无法解决，严重影响会话的可恢复性。

### ⑩ #4757 `--yolo` / `--allow-all` blocked for the whole session by a fail-closed bypass restriction applied on an account with NO managed policy
- **作者**: @jordanms | 创建: 2026-09-07 | 💬 3 | 👍 0
- **链接**: https://github.com/github/copilot-cli/issues/4757
- **为何重要**: 没有配置托管策略的账号也被错误地应用了 fail-closed 限制策略，导致整场会话都无法进入 `--yolo` 模式，属于策略解析的矛盾性问题，对企业用户与自动化场景影响尤甚。

## 4. 重要 PR 进展

过去 24 小时内共新增/更新 4 个 PR（未达到 10 条，全部列出），其中两条为重要修复，两条因重复或含垃圾提交而已关闭。

### ① #4770 [OPEN] Document the WebSocket responses opt-out
- **作者**: @1fanwang | 创建: 2026-09-08
- **链接**: https://github.com/github/copilot-cli/pull/4770
- **内容**: 文档型 PR，旨在说明当 WebSocket responses transport 不可用（例如网络屏蔽或出现 `400 input item ID does not belong to this connection`）时，如何通过选项关闭该功能进行逃生。

### ② #4762 [CLOSED] install: report unsupported operating systems
- **作者**: @devm33 | 创建: 2026-09-08
- **链接**: https://github.com/github/copilot-cli/pull/4762
- **内容**: 修复 `install.sh` 在 FreeBSD 下的误报逻辑。此前会在非 macOS/Linux 平台错误提示 “Windows detected but winget not found”，现改为正常报告“系统不受支持”。

### ③ #4761 [CLOSED] install: report unsupported operating systems
- **作者**: @1fanwang | 创建: 2026-09-08
- **链接**: https://github.com/github/copilot-cli/pull/4761
- **内容**: 与 #4762 实现相同功能，极可能是作者未发现此前已存在 PR 而创建的重复提交，已关闭。（已合并至 #4762 为优）

### ④ #4100 [CLOSED] shangti0168
- **作者**: @huangyoufeng76-debug | 创建: 2026-07-12 | 更新: 2026-09-08
- **链接**: https://github.com/github/copilot-cli/pull/4100
- **内容**: 垃圾/噪音 PR（描述仅“安全性”），今日关闭。建议忽略。

## 5. 功能需求趋势

综合今日所有 Issues 与 PR 内容，社区最关注的方向如下：

- **Vim 风格模态编辑**：Issue #13 持续近一年，💬 11、👍 76，现已随 v1.0.84-2 落地。用户对键盘流效率的追求是强需求。
- **MCP 扩展与连接可靠性**：
  - #4753：会话恢复与 MCP 连接初始化冲突；
  - #4759：要求 CLI 在取消工具调用时向 MCP server 发送 cancellation 请求；
  - #4773/#4772：MCP 工具被误报为 0 个、/clear 与 /restart 破坏 MCP 集成。
  - 说明 MCP 已经从“能否接入”进入“接入后是否健壮可用”的深水区。
- **第三方模型接入（OpenRouter）**：#2943 再次活跃，14 👍，用户希望接入更多模型并为不同场景选择模型。
- **会话（Session）可持续性**：
  - #4664 内存溢出、#4505 旧连接 ID 残留、#2836 孤儿会话状态文件夹、#4755 会话永久卡死。
  - 用户对“暂停 → 恢复 → 继续”这条核心路径的稳定性期待越来越高。
- **Windows 平台体验**：#4742、#4756 都指向 Local session 创建被阻塞；#4531 Git 配置丢失导致 VS Code 启动后 Git 发现失败。Windows 已成为本轮回归更新的重灾区。
- **授权与安全策略可预期性**：#4757 显示无策略账号被误拦截、#4759 则要求按规范发送 MCP cancellation、#4696 Allow-all 权限闲置后自动丢失——都在诉求“权限规则应当透明、一致”。

## 6. 开发者关注点（痛点 / 高频词）

高频痛点集中在以下几类：

- **会话恢复稳定性是最大痛点**：#4505、#4664、#4755 #4753 形成了一条“恢复会话 → MCP 连不上 → 内存爆掉 → 永久卡死”的链路，把“恢复”这件事从边缘业务变成了主路径质量瓶颈。
- **版本回归让人疲惫**：#4742 与 #4756 同为 1.1.15 桌面板上的 Local session 回归；#4505 则从 v1.0.83 起开始出现。开发者对标“天天向上”的版本演进抱有较高的防回归期待。
- **MCP 配置与生命周期管理混乱**：恢复、`/clear`、`/restart` 或重复扫描（#4773）都可能造成 MCP 服务静默失效，用户被迫一次次重启进程或执行 `/mcp reload`。相关 issue 数量显著增加。
- **调试与排障成本过高**：Debug 日志涨到 13GB（#4612）、macOS 上的 MallocStackLogging 噪音（#4614）都让用户难以自行定位崩溃。
- **工作区适配仍不成熟**：#4765 指出“工作目录不是 git 仓库根”时，`.mcp.json` 和 hook 配置无法被正确读取——恰好点出 monorepo/多仓库 workspace 的开发场景需求。

---

*本日报由 AI 辅助整理，数据截止 2026-09-09。所有条目均附有 GitHub 原始链接，可点击查看详情。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>



</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报

**日期：2026-09-09**  
**数据来源：github.com/anomalyco/opencode**

---

## 1. 今日速览

过去 24 小时内 OpenCode **无新版本发布**，社区讨论热度集中在**性能退化（高 CPU、无限循环）、桌面端架构重构**以及**模型配置/会话管理**等方向。值得关注的是，开发团队提交了多个“桌面功能扩展化”重构 PR，正在将终端、浏览器、代码审查等内置模块逐步拆分为可插拔扩展，为未来生态插件化铺路。与此同时，多条与高内存/CPU 占用、AI 循环失控相关的老 Issue 被重新顶起，说明稳定性仍是用户核心诉求。

---

## 2. 版本发布

（无）

---

## 3. 社区热点 Issues

挑选了 10 条最值得关注的 Issue，涵盖性能、稳定性、功能需求与配置缺陷。

### 3.1 [CLOSED] Memory Megathread
- **作者**: @thdxr | **评论**: 144 | **👍**: 110  
- **编号**: [#20695](https://github.com/anomalyco/opencode/issues/20695)  
- **为什么重要**: 这是内存问题的总集帖，收集了大量散落的内存泄漏报告，并引导用户提交堆快照。虽然已关闭，但社区参与度极高，是当前性能问题的“风向标”。

### 3.2 [OPEN] High CPU usage in newer versions of OpenCode
- **作者**: @DenisSilent | **创建**: 2026-05-31 | **评论**: 51 | **👍**: 27  
- **编号**: [#30086](https://github.com/anomalyco/opencode/issues/30086)  
- **为什么重要**: 近 7 天 CPU 飙升，从可同时开 10 个会话降到 3 个就卡顿，甚至影响鼠标响应。评论数高，说明受影响用户面广，与下述 #42306 可归为同类根因。

### 3.3 [OPEN] [FEATURE] : keep legacy layout option
- **作者**: @darkine24th | **评论**: 43 | **👍**: 47  
- **编号**: [#37012](https://github.com/anomalyco/opencode/issues/37012)  
- **为什么重要**: 社区对新版 UI 布局不满，认为旧版主窗口可直接访问所有功能，而新版需要多次导航。👍 数在 Issue 中最高，代表着一股明确的 UX 回归诉求。

### 3.4 [OPEN] Bug: OpenCode enters infinite loop after tool calls complete
- **作者**: @Dvalin21 | **评论**: 11 | **👍**: 4  
- **编号**: [#26220](https://github.com/anomalyco/opencode/issues/26220)  
- **为什么重要**: 工具调用结束后进程陷入死循环，不响应输入且不退出。直接击中使用可靠性的核心，且与 2.0 的 #45442 呼应，属于长期未解决的“AI 失控”类关键缺陷。

### 3.5 [OPEN] [FEATURE]: Add unarchive/restore for archived sessions
- **作者**: @alohaninja | **评论**: 10 | **👍**: 11  
- **编号**: [#24153](https://github.com/anomalyco/opencode/issues/24153)  
- **为什么重要**: 归档会话目前是“单向操作”，归档后只能变暗显示，无法恢复或搜索。这是一个高赞、低评论数的典型“小而痛”功能，对长期用户的工作流影响明显。

### 3.6 [OPEN] [2.0] subagent: infinite loop of identical tool calls for ~50min with no loop protection, uncontrollable token burn
- **作者**: @wujiachen0727 | **创建**: 2026-08-27 | **评论**: 4 | **👍**: 1  
- **编号**: [#45442](https://github.com/anomalyco/opencode/issues/45442)  
- **为什么重要**: 2.0 中一个后台 subagent 在约 50 分钟内连续发出 364 次相同的 grep 调用，没有任何循环防护，token 消耗失控。2.0 刚起步就出现此类问题，用户信任度影响很大。

### 3.7 [OPEN] TUI: main thread burns ~100% CPU continuously redrawing a spinner (~15fps writev to tty) with no active output
- **作者**: @pudy | **评论**: 3 | **👍**: 0  
- **编号**: [#42306](https://github.com/anomalyco/opencode/issues/42306)  
- **为什么重要**: 通过 strace 证实 TUI 主线程在无输出时仍以 ~100% CPU 循环刷新 spinner。这是 #30086 之外的又一条高 CPU 根因证据，后端与前端线程都存在问题。

### 3.8 [OPEN] Missing Content-Type bypasses model response body timeout and leaves sessions busy indefinitely
- **作者**: @totalolage | **评论**: 2 | **👍**: 0  
- **编号**: [#47605](https://github.com/anomalyco/opencode/issues/47605)  
- **为什么重要**: 当模型返回的 HTTP 200 缺少 `Content-Type` 时，客户端超时形同虚设，会话永远处于 busy 状态。这暴露了流式响应处理对“畸形响应头”的健壮性不足。

### 3.9 [OPEN] Desktop sidecar repeatedly crashes with V8 out-of-memory, causing local server red and Failed to fetch
- **作者**: @caser9257 | **评论**: 3 | **👍**: 0  
- **编号**: [#41964](https://github.com/anomalyco/opencode/issues/41964)  
- **为什么重要**: 桌面端 sidecar 进程反复因 V8 OOM 崩溃，导致界面提示 `Failed to fetch`。用户并发会话达到一定数量后，桌面端稳定性明显劣化，属于架构级限制。

### 3.10 [OPEN] Mid-session model resolution silently falls back to global config.model, ignoring the TUI-selected model
- **作者**: @a-d-gordienko | **创建**: 2026-09-08 | **评论**: 2 | **👍**: 0  
- **编号**: [#47968](https://github.com/anomalyco/opencode/issues/47968)  
- **为什么重要**: 用户在 TUI 中选择模型后，实际流量却被静默路由到全局 `config.model`，所选模型收到 0 请求。虽然新提交，但影响模型计费、归属和可靠性判断，值得追踪。

---

## 4. 重要 PR 进展

以下 PR 分为两大类：Hona 主导的“桌面扩展化”大型重构，以及若干关键的 Bug 修复与清理。

### 4.1 桌面端扩展化重构（架构级）

这一系列 PR 将桌面应用的内置功能逐步提取为 `@opencode/plugin-*` 独立包，并引入公共扩展 Manager。

- **feat(plugin): explore desktop extensions and manager**  
  **作者**: @Hona | [#47935](https://github.com/anomalyco/opencode/pull/47935)  
  **内容**: 新增桌面扩展 SDK 和管理器，提供渲染端/主进程入口、TUI slot 解析器、宿主面板/原生 surface 能力以及 Settings → Extensions 页面。这是整个插件化架构的地基。

- **refactor(desktop): extract the browser extension package**  
  **作者**: @Hona | [#47936](https://github.com/anomalyco/opencode/pull/47936)  
  **内容**: 将浏览器渲染器和原生实现迁入 `@opencode/plugin-browser-desktop`，且除公共 API 外不依赖 App/Desktop/Core。

- **refactor(app): extract review and file viewer extension**  
  **作者**: @Hona | [#47947](https://github.com/anomalyco/opencode/pull/47947)  
  **内容**: 将 Git 审查、文件树、文件预览、Diff 查看、行内评论和 “Open in” 等整体迁入 `@opencode/plugin-review-desktop`，宿主仍负责面板布局与焦点管理。

- **refactor(app): extract context usage extension**  
  **作者**: @Hona | [#47948](https://github.com/anomalyco/opencode/pull/47948)  
  **内容**: 将上下文用量按钮、统计、系统提示词显示、原始消息及导出功能提取为 `@opencode/plugin-context-desktop`。

- **refactor(app): extract terminal desktop extension**  
  **作者**: @Hona | [#48045](https://github.com/anomalyco/opencode/pull/48045)  
  **内容**: 将 Ghostty 渲染、PTY 连接、终端标签/标题/焦点/序列化全部移入 `@opencode/plugin-terminal-desktop`，并使副停靠栏通过公共 slots 参与布局。

### 4.2 关键修复与清理

- **refactor(session): remove message content mutation API**  
  **作者**: @rekram1-node | [#48043](https://github.com/anomalyco/opencode/pull/48043)  
  **内容**: 移除由 #45015 引入、为 #44984 准备的“已完成的 assistant 消息内容修改”API，包括 `PATCH message`、`session.messageUpdate` 及配套错误类型。属于收敛 1.x 协议面。

- **fix(server): reject malformed

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*