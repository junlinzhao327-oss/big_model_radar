# AI CLI 工具社区动态日报 2026-09-01

> 生成时间: 2026-09-01 01:19 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-09-01）

> 说明：本报告基于各项目 2026-09-01 社区日报摘要；其中 OpenAI Codex 板块本次摘要为空，无法参与横向对比。

---

## 1. 生态全景

AI CLI 工具已进入 **“高频发布 + 真实环境大规模验证”** 阶段，社区反馈不再只是功能请求，而是集中在稳定性、安全边界和跨平台兼容性上。Claude Code、Gemini CLI、OpenCode 等均保持日级、夜间版迭代节奏，但 Windows 端问题、Agent 假成功、会话恢复失败等成为跨项目共性问题。与此同时，模型路由/BYOK、MCP 工具链、子代理编排正成为下一代竞争焦点。整体看，工具从“能用”向“可靠、可信、可治理”过渡。

---

## 2. 各工具活跃度对比

| 工具 | Release | 热点 Issues | PR 动态 |
|---|---|---:|---|
| Claude Code | v2.1.252（3 项修复） | 10 组热点，最高评论 88（Windows GPU 崩溃）；安全策略误报 30+ 条成系统性反馈 | 本期摘要未披露独立 PR |
| OpenAI Codex | 本期无动态摘要 | — | — |
| Gemini CLI | v0.59.0-nightly.20260831 | 5 个热点，含 4 个 P1；累计评论约 34 | 安全加固、gemini-2.5-flash-lite fallback 链 PR（无编号） |
| GitHub Copilot CLI | v1.0.83-0（mTLS 支持等） | 2 个热点：企业 Agent 不显示、BYOK 下 /model 回归 | Release 内含修复，无独立 PR 汇总 |
| Kimi Code CLI | 无 | 1 个阻断级 GBK 编码崩溃，0 评论 | 2 个 PR：StrReplaceFile 空字符串校验、迁移到 Kimi Code 流程 |
| OpenCode | 无 | 10 个热点，最高 126 评论（剪贴板失效） | 10 个 PR：桌面浏览器、Firecrawl 搜索、工具命名空间等 |
| Qwen Code | v0.22.3-nightly（含 git 状态提示等） | 10 个热点，聚焦会话管理、多智能体误报 | Release 含 PR #10397；未单独披露 PR 汇总 |

---

## 3. 共同关注的功能方向

### 3.1 Windows 与非 UTF-8 环境兼容性
- **Claude Code**：Windows 桌面版 GPU 崩溃、窗口置顶、Git Bash 反斜杠被剥离。
- **Kimi Code**：中文 Windows 下 GBK 编码崩溃。
- **OpenCode**：2.0 升级后 Windows 本地插件静默加载失败。
- **信号**：Windows 已成为 AI CLI 规模化落地的关键瓶颈。

### 3.2 Agent 执行可靠性与“假成功”
- **Gemini CLI**：Subagent 到达 MAX_TURNS 后误报 GOAL 成功；Generalist Agent 挂起。
- **Qwen Code**：多智能体 `task_list` 相同参数被误判为死循环。
- **OpenCode**：模型响应随机中断、无报错；`opencode run` 高概率挂起。
- **信号**：Agent 的“假成功”比显式失败更危险，直接影响自动化信任度。

### 3.3 会话恢复与长会话治理
- **Qwen Code**：`--resume` 可复现已修复的悬空 thought 风险；HTTP 413 后长会话不可恢复；归档会话与活跃会话冲突。
- **Claude Code**：Remote Control 会话卡顿。
- **Copilot CLI**：会话恢复导致崩溃。
- **OpenCode**：会话级实例选择器、等待审批超时后 spinner 丢失。
- **信号**：会话的持久化、恢复、压缩、归档是当前工程化短板。

### 3.4 安全边界与信任模型
- **Claude Code**：服务端安全过滤器大量误报，影响合法逆向/取证/调试。
- **Kimi Code**：StrReplaceFile 空字符串可被静默插入内容，缺输入校验。
- **Q

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---

# Claude Code 社区动态日报 — 2026-09-01

## 今日速览

📦 昨日发布 **v2.1.252**，修复了 Mac 上 Bash 命令 "task output swap refused" 报错、项目级 "always allow" 设置未持久化以及 Remote Control 会话卡顿三个问题。社区方面，**Windows 桌面端的两个问题（GPU 崩溃、窗口置顶）讨论热度最高**，分别达到 88 条和 51 条评论；此外，一位用户集中提交的 30+ 条安全策略误报问题已经形成系统性的反馈现象，值得 Anthropic 重视。

---

## 版本发布

### v2.1.252
🔗 https://github.com/anthropics/claude-code/releases/tag/v2.1.252

- 🐛 **修复**: Bash 命令在部分 Mac 上报错 "task output swap refused (tasks dir moved or linked)" 的问题
- 🐛 **修复**: 在尚无 `.claude/settings.local.json` 的项目中，"always allow" 设置无法保存的问题
- 🐛 **修复**: 由 Claude Desktop 或 VS Code 托管的 Remote Control 会话卡顿长达一分钟的问题

---

## 社区热点 Issues（10 个）

### 1. 💥 Windows 桌面版 GPU 崩溃，修复前应用无法启动
**#80444** | 评论 88 | 👍 15 | [链接](https://github.com/anthropics/claude-code/issues/80444)

Claude Desktop 1.24012.1 在 Windows 11 上通过应用内浏览器标签页触发致命 GPU 进程崩溃（错误码 0x060C201E），导致 MSIX 包进入不可启动状态（appxState=2），只能通过"修复"操作恢复。已确认在 NVIDIA RTX 2080 的两个驱动版本上均可复现。该问题影响面广，评论区讨论激烈。

**关注理由**: 严重阻塞桌面端用户体验，涉及 Electron/GPU 底层，修复难度高。

---

### 2. ⚠️ Windows 桌面窗口始终置顶，无关闭选项
**#85891** | 评论 51 | 👍 117 | [链接](https://github.com/anthropics/claude-code/issues/85891)

Claude Desktop 在 Windows 11 上表现为 topmost 窗口，即使切换到其他应用也始终置顶显示，且应用内没有提供禁用该行为的设置。👍 117 是本期 Issues 中最高的，说明大量 Windows 用户深受困扰。该问题与 #66516（macOS 端同样问题）形成呼应。

**关注理由**: 高赞 + 跨平台同类问题，直接影响用户日常使用。

---

### 3. 📋 数月日常使用错误记录——来自深度用户的系统性反馈
**#69044** | 评论 31 | 👍 0 | [链接](https://github.com/anthropics/claude-code/issues/69044)

一位每日使用 Claude Code 的用户用德语系统性地记录了数月来反复出现的错误模式，并非一次性抱怨，而是结构化的反馈文档。虽然 👍 不多，但 31 条评论说明社区在围绕这些模式进行深入讨论。

**关注理由**: 来自长期重度用户的场景化反馈，对产品改进有重要参考价值。

---

### 4. 🎯 VS Code 扩展缺批量 diff 审查模式
**#31888** | 评论 18 | 👍 50 | [链接](https://github.com/anthropics/claude-code/issues/31888)

用户请求在 Claude Code VS Code 扩展中加入类似 Cursor 原生 Agent 的批量 diff 审查模式：在批准前一次性展示所有变更，而非逐个文件审查。👍 50 反映该需求在 IDE 用户中相当普遍。

**关注理由**: 高赞功能请求，直接对标竞品体验，是 IDE 集成方向的重要信号。

---

### 5. 📎 Gmail MCP Connector 缺少附件支持
**#28575** | 评论 11 | 👍 33 | [链接](https://github.com/anthropics/claude-code/issues/28575)

请求为 Gmail MCP 的 `gmail_create_draft` 增加文件附件支持，并新增 `gmail_send_draft` 工具。

**关注理由**: MCP 生态扩展的代表性需求，反映用户对 MCP 工具完成度的要求正在提高。

---

### 6. 🔒 安全过滤器误报——30+ 条同类问题集中提交
**#75536、#75519、#75506、#75503、#75504、#75491、#75110、#75108、#75109、#75076 等** | 每条约 3 条评论 | [示例链接](https://github.com/anthropics/claude-code/issues/75536)

用户 @sworrl 集中提交了 30+ 条安全策略误报问题，覆盖 "cyber" 和 "aup" 两类误拦截：合法的固件逆向分析、内存取证、无人机协议分析、个人设备调试、甚至打开空目录都会被服务端安全过滤器拦截。大量 issue 被标记为 duplicate 且已关闭，但这种"批量上报"的方式本身就是对误报率升高的强烈反馈。

**关注理由**: 安全过滤器的误报已系统性地影响合法开发工作，是当前最突出的信任危机信号。

---

### 7. 🐛 Windows/Git Bash 下反斜杠被静默剥离
**#89392** | 评论 2 | [链接](https://github.com/anthropics/claude-code/issues/89392)

Bash 工具在 Windows/Git Bash 环境下将命令字符串中的 `\\` 静默折叠为 `\`，导致需要双反斜杠的路径或转义场景下命令被破坏。已提供复现步骤（has repro）。

**关注理由**: Windows 平台命令执行的隐蔽 bug，可能导致用户误判为自身脚本问题，排查成本高。

---

### 8. 💬 聊天面板发送消息后自动滚动到底部，丢失阅读位置
**#76350** | 评论 2 | 👍 2 | [链接](https://github.com/anthropics/claude-code/issues/76350)

VS Code/Cursor 扩展中，向上滚动阅读历史消息时，发送新消息会强制将视图拉回底部，导致阅读位置丢失。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-09-01**

---

## 1. 今日速览

今日社区动态集中在 **Agent 稳定性与安全加固** 两大方向：多个 P1 级 Bug 持续发酵，包括 Subagent 在达到 MAX_TURNS 后被误报为"成功"、Generalist Agent 无响应挂起，以及 Shell 命令执行卡在 "Waiting input" 状态。PR 侧则以安全修复和体验优化为主，涉及移除硬编码凭据、防止后台 git 操作劫持 stdin、增强配置文件路径权限验证等。值得关注的是，模型 fallback 链中加入 `gemini-2.5-flash-lite` 的 PR 今日更新，利好免费额度用户。

---

## 2. 版本发布

- **[v0.59.0-nightly.20260831.g0bd1d4397](https://github.com/google-gemini/gemini-cli/releases/tag/v0.59.0-nightly.20260831.g0bd1d4397)** — Nightly 版本，主要包含近期 master 分支的累积修复与改进，具体变更请查看 [Full Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.59.0-nightly.20260830.g0bd1d4397...v0.59.0-nightly.20260831.g0bd1d4397)。

---

## 3. 社区热点 Issues

### [1. Subagent 到达 MAX_TURNS 后恢复被误报为 GOAL 成功](https://github.com/google-gemini/gemini-cli/issues/22323)
**优先级 P1 | 评论 13 | 更新于 2026-09-01**
`codebase_investigator` 子代理在命中最大轮次限制、尚未执行任何分析时，却返回 `status: "success"` 与 `Termination Reason: "GOAL"`，掩盖了真实的中断原因。该问题直接影响 Agent 的可靠性判断，是社区最关注的 Bug 之一。

### [2. Generalist Agent 无响应挂起](https://github.com/google-gemini/gemini-cli/issues/21409)
**优先级 P1 | 评论 8 | 👍 8 | 更新于 2026-09-01**
当 CLI 将任务交给 generalist agent 时，即使是创建文件夹这类简单操作也会永久挂起，有用户等待长达一小时无果。变通方案是显式指示模型不要使用子代理。

### [3. Shell 命令执行完成但卡在 "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)
**优先级 P1 | 评论 4 | 👍 3 | 更新于 2026-09-01**
简单 CLI 命令执行完毕后，界面仍显示命令活动并进入"等待用户输入"状态，即使是不会请求输入的命令也能复现。此问题严重影响自动化流程与日常使用体验。

### [4. Browser Subagent 在 Wayland 下失败](https://github.com/google-gemini/gemini-cli/issues/21983)
**优先级 P1 | 评论 4 | 👍 1 | 更新于 2026-09-01**
浏览器子代理在 Wayland 环境下无法正常工作，中止时给出 `Termination Reason: GOAL`，但并未实际完成任务。涉及图形环境兼容性问题。

### [5. Auto Memory 的确定化脱敏与日志缩减](https://github.com/google-gemini/gemini-cli/issues/26525)
**优先级 P2 | 评论 5 | 更新于 2026-09-01**
指出 Auto

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-09-01）

> 数据来源：github.com/github/copilot-cli | 统计周期：2026-08-31 ~ 2026-09-01

## 今日速览

今日发布 v1.0.83-0，重点新增代理环境下的 mTLS 客户端证书支持，并修复 herdr 终端复用器兼容性问题。社区侧，1.0.81/82 的多个回归问题（BYOK 的 /model 命令失效、TLS 代理下 OAuth 登录失败）成为讨论焦点；与此同时，会话恢复导致的崩溃、延迟执行等稳定性缺陷也在密集反馈中，值得团队优先排查。

## 版本发布

### v1.0.83-0

- **新增**：自动为模型与 Web 请求提供 HTTPS 代理 mTLS 客户端证书支持。
- **修复**：正确识别 herdr 终端复用器，不再误判为 tmux；herdr 窗格中 Kitty 键盘协议、配色方案跟随、终端进度、`/copy` 与通知功能恢复正常。

🔗 https://github.com/github/copilot-cli/releases/tag/v1.0.83-0

## 社区热点 Issues（Top 10）

### 1. 组织级 Agent 不显示（#1285）
- **作者**：@SAhmeti ｜ **评论 8** ｜ **👍 9** ｜ **状态：Open**
- **摘要**：用户在企业组织下创建 `.github-private` 仓库并配置 Agents，但 CLI 与 VS Code 中均无法看到。采用标准模板且命名空间正确，仍然不显示。
- **关注点**：企业级 Agent 分发核心路径疑似受阻，影响组织级规模化使用。

🔗 https://github.com/github/copilot-cli/issues/1285

### 2. 1.0.82 回归：BYOK 下 /model 命令失效（#4672）
- **作者**：@extedosse ｜ **评论 1** ｜ **状态：Open**
- **摘要**：1.0.81/82 版本中，当通过环境变量配置 BYOK 模型时，`/model`

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-09-01

## 1. 今日速览

今日社区动态集中在**稳定性修复**与**项目迁移**两大主题。新提交的 PR 针对 `StrReplaceFile` 工具的空字符串处理缺陷提出了修复方案，同时另一 PR 正积极推动从 kimi-cli 向 Kimi Code 的弃用感知迁移流程。此外，一个 Windows 平台下的 GBK 编码报错 Issue 浮出水面，反映了工具链在非 Unicode 环境下的兼容性问题。

---

## 2. 版本发布

过去 24 小时内无新的 Release 发布。

---

## 3. 社区热点 Issues

以下为过去 24 小时内更新且值得关注的 Issue：

### #2629 `UnicodeEncodeError: 'gbk' codec can't encode character '\u0133'`
- **作者**: @tuies
- **状态**: OPEN / 0 评论 / 0 👍
- **链接**: [查看 Issue](https://github.com/MoonshotAI/kimi-cli/issues/2629)
- **详请**: 在 Windows (NT 10.0.19045) 平台上使用 Kimi Code CLI 1.49.0 与 K2.7 Code 模型时，工具在输出包含特殊字符 `\u0133`（ĳ，荷兰语 ij 连字）的内容时触发了 Python 的 GBK 编解码错误，导致 CLI 在运行过程中直接崩溃。错误信息显示位置在 position 1559。

**为什么值得关注**：这是目前唯一一个在 Windows 环境下报告的编码崩溃问题。GBK 是 Windows 简体中文系统的默认编码，与 UTF-8 相比对 Unicode 字符支持不足。

**社区反应与分析**：虽然评论数为 0，但该问题直接指向核心的跨平台兼容性缺陷。对于依赖中文 Windows 环境的开发者来说，这是一个阻断级 Bug。需要排查的方向包括：终端输出流的编码设置（是否可强制 UTF-8）、日志记录模块的编码处理等。按当前活跃度，建议优先修复。

---

## 4. 重要 PR 进展

以下为过去 24 小时内更新的重要 Pull Request：

### #2631 `fix(file): reject empty old string in StrReplaceFile`
- **作者**: @rootkiller6788
- **状态**: OPEN / 0 👍
- **链接**: [查看 PR](https://github.com/MoonshotAI/kimi-cli/pull/2631)
- **内容摘要**: 作者在测试 `StrReplaceFile` 工具时发现了极端输入场景下的隐患。当 agent 传入一个空的 `old` 字符串时，Python 的 `str.replace()` 不会匹配任何内容，而是会将 `new` 字符串插入到开头（或启用 `replace_all=True` 时插入到每个字符之间），且工具会报告操作成功。这种"静默的破坏"会悄无声息地篡改文件内容。

**为何重要**：这是一个非常漂亮且危险的边界条件。空字符串作为"查找目标"在编辑器 UI 上几乎无法被误触发，但在 agent 工具调用时，模型可能会因为逻辑错误或 token 截断而生成空参数。该 PR 直接堵住了这个可能导致源码文件被批量插入无效字符串的隐患。若合并，将显著提升 `StrReplaceFile` 的健壮性。

### #2630 `feat(shell): deprecation-aware update flow with one-key migration to Kimi Code`
- **作者**: @jackfish212
- **状态**: OPEN / 0 👍
- **链接**: [查看 PR](https://github.com/MoonshotAI/kimi-cli/pull/2630)
- **内容摘要**: 该 PR 是 kimi-cli → Kimi Code 迁移大动作的一部分。当 CDN 发布迁移公告（`https://cdn.kimi.com/kimi-code-tips/kimi_cli/migration.json`）时，CLI 会将 Python 版本标记为"已弃用"，并引导用户完成一键迁移至新的 Kimi Code 工具。

**为何重要**：这是一个信号——MoonshotAI 正在明确规划 kimi-cli 的淘汰路径。当前仓库的 README 和 UI 已经抹去了 CLI 的字样，这个 PR 的落地将把 Python 版本的用户无缝转移到新工具上。对于仍在使用 kimi-cli 的开发者来说，这代表着未来会有合并/更名的重大变动。

---

## 5. 功能需求趋势

基于今日更新的 Issue 与 PR 数据，结合项目整体迁移背景，社区关注的功能需求方向呈现以下趋势:

1. **编码与字符集兼容性**：Windows 平台下的 GBK 编码报错表明，CLI 在输出侧对 Unicode 字符的处理仍不够健壮。**支持强制 UTF-8 输出**或**自动检测终端字符集**成为刚需。

2. **工具安全性（Agent 工具边界）**：`StrReplaceFile` 的空字符串问题揭示了一个更大命题——**如何对 Agent 工具入参进行运行时校验**。社区对"工具操作透明且可回滚"的期望在升温。

3. **平滑迁移与向后兼容**：PR #2630 的迁移流程设计，体现了对存量 kimi-cli 用户（尤其是通过 pip 安装的 Python 生态用户）的重视。**一键迁移**、**配置保留**和**废弃通知机制**将决定迁移工具链的完成度。

4. **新模型支持**：Issue #2629 使用了 K2.7 Code 模型，虽未直接提及新模型需求，但该模型的引入间接表明用户对最新 Code 模型的采纳速度极快。未来社区大概率会持续要求**对最新 K 系列模型（如 K2.5++、K3）的即时支持**。

5. **跨平台体验一致性**：Issues 中反复出现的 Windows 环境异常，说明开发者的主力环境已从 macOS/Linux 扩展到 Windows，**对 PowerShell 原生支持**、**Windows 终端渲染兼容性**的诉求逐步增强。

---

## 6. 开发者关注点

结合上述动态，开发者反馈中的痛点主要集中在以下方面：

- **Windows 中文本地化下的稳定性**：GBK 编码崩溃是典型的中文 Windows 用户才会遭遇的问题。这暗示了 CLI 在读取系统区域设置和终端编码时存在假设偏差（默认假设 UTF-8）。开发者需要确保代码正确处理 `PYTHONIOENCODING` 和 `stdout` 的编码回退策略。

- **Agent 工具误操作的可察觉性**：`StrReplaceFile` 的空 `old` 字符串问题，暴露了模型驱动的文件编辑工具在"零输入"场景下可能造成的无感知文件破坏。**在应用文件修改前打印 diff 摘要**，是一个高频呼声。

- **迁移成本与实际体验**：目前从 kimi-cli 到 Kimi Code 的迁移意图已通过 PR #2630 明确化。开发者关心的核心痛点将是：**迁移后自定义脚本/配置是否保留**、**Python 版能否继续获得安全更新**，以及**迁移失败时的回滚方案**。

- **Issue 响应速度与透明化**：今日唯一的 Issue 评论数为 0，这可能让反馈者感到缺乏支持。社区期望对严重 Bug（如编码崩溃）有更快的响应确认机制——例如打上 `triaged` 标签或给出初步排查指引。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-09-01

## 今日速览

昨日无新版本发布，社区讨论集中于三个方向：**剪贴板复制失效**（#4283，126条评论）、**2.0 迁移引发的一系列兼容性与稳定性问题**，以及**订阅计费/免费额度争议**。PR 侧以核心可靠性修复为主，并出现了实验性桌面浏览器和 Firecrawl 开发者搜索提供器等新功能。

---

## 社区热点 Issues

### 1. 复制到剪贴板功能失效
- **#4283**：复制响应文本到剪贴板无效，在 OpenCode 1.0.62 上复现。已积累 **126 条评论** 和 **117 👍**，是目前社区反馈最集中的问题，影响范围极广。
- 链接：https://github.com/anomalyco/opencode/issues/4283

### 2. 使用量仪表盘数据不一致，触发限额误判
- **#38255**：免费额度在午夜被判定为“每周超限”，但粒度使用仪表盘显示同期仅消耗约 10 美元额度。计费数据口径不统一直接导致用户无法使用服务。
- 链接：https://github.com/anomalyco/opencode/issues/38255

### 3. 请求接入 GitHub Copilot 自动模型路由 API
- **#20235**：建议 OpenCode 接入 Copilot 的 `/models/session` 自动路由端点，使模型选择更智能。获得 **29 👍**，是近期最受关注的新模型接入方向。
- 链接：https://github.com/anomalyco/opencode/issues/20235

### 4. Zen 账户无法删除，持续扣费且无客服响应
- **#18016**：用户反馈无法删除 Zen 账户，退款无门、邮件无回复。属于严重的计费/合规问题，已获 8 条评论。
- 链接：https://github.com/anomalyco/opencode/issues/18016

### 5. 可配置的“运行中提示”投递模式（队列 vs 引导）
- **#32157**：希望为 2.0 增加 `queue`、`steer`、`break` 三种运行中提示投递语义，并支持压缩感知的引导行为。获 **78 👍**，社区对交互控制精细化的需求强烈。
- 链接：https://github.com/anomalyco/opencode/issues/32157

### 6. 模型响应随机中断，无任何报错
- **#34473**：桌面版 v1.17.11 在使用 Big Pickle 模型时随机停止响应，无错误抛出，仅播放完成音。影响稳定性的核心痛点。
- 链接：https://github.com/anomalyco/opencode/issues/34473

### 7. 新布局下 “Auto-accept permissions” 按钮被禁用
- **#31137**：启用“新布局与设计”后，权限自动接受按钮置灰；经典布局下正常。2.0 UI 回归性问题。
- 链接：https://github.com/anomalyco/opencode/issues/31137

### 8. 免费模型无限使用漏洞（VPN 轮换绕过限流）
- **#34344**：限流仅绑定 IP，切换 VPN 即可重置额度。社区已确认可用 VPN 轮换自动化持续调用 DeepSeek v4 Flash 与 mimo v2.5。涉及资源滥用风险。
- 链接：https://github.com/anomalyco/opencode/issues/34344

### 9. `opencode run` 偶发挂起，无法创建会话（约 56% 失败率）
- **#38723**：`opencode run` 在 init 阶段挂起，零输出、零报错，只能超时退出。间歇性高概率失败，严重影响脚本/CI 使用。
- 链接：https://github.com/anomalyco/opencode/issues/38723

### 10. 2.0 升级后 Windows 本地插件静默加载失败
- **#46408**：beta-18721 升级后，`cli.json` 中 `file://` 插件目录配置失效，侧边栏无插件渲染，日志仅静默丢失。2.0 配置迁移的回归问题。
- 链接：https://github.com/anomalyco/opencode/issues/46408

---

## 重要 PR 进展

### 1. 实验性桌面浏览器
- **#44838**：在桌面会话旁新增浏览器面板，支持地址栏、前进/后退、刷新与停止控制，代理可打开页面与截图。属于 2.0 重大新功能。
- 链接：https://github.com/anomalyco/opencode/pull/44838

### 2. Firecrawl 开发者搜索提供器
- **#46512**：新增 `firecrawl-developer` Web 搜索提供器，针对 GitHub Issues、PR、README 与文档构建的开发者索引优化搜索。已有 #41042 的后续扩展。
- 链接：https://github.com/anomalyco/opencode/pull/46512

### 3. 核心：注册工具命名空间
- **#46487**：为工具增加命名空间元数据注册机制，保持 `namespace` 字符串兼容，支持命名空间定义在重放、优先级、重载与销毁中一致保留，并按命名空间分组工具。
- 链接：https://github.com/anomalyco/opencode/pull/46487

### 4. SDK：配置会话级实例选择器
- **#46496**：允许嵌入式应用配置 Core 的会话感知实例选择器，解决多线程同目录下插件栈隔离与后置注册时机过晚的问题。
- 链接：https://github.com/anomalyco/opencode/pull/46496

### 5. 拒绝重复补丁目标（对齐 Codex 行为）
- **#46477**：对同一源路径的多个文件操作（如两次 update 或 update-then-delete）在写入前直接拒绝，防止并发写入冲突。
- 链接：https://github.com/anomalyco/opencode/pull/46477

### 6. Bedrock 推理参数 Normalize
- **#46501**：统一 GPT-5 Bedrock Converse 推理映射，将 effort 与 summary 作为 `additionalModelRequestFields.reasoning` 传递，并保留用户配置的 SDK 风格选项。
- 链接：https://github.com/anomalyco/opencode/pull/46501

### 7. 修复排队控件的提示提升
- **#46443**：解决取消排队提示时可能误消费后续 move/compaction 的问题，避免会话位置漂移或异常。
- 链接：https://github.com/anomalyco/opencode/pull/46443

### 8. 跨 Location 清理保留审批
- **#46509**：修复会话等待审批超 1 小时后回到会话出现无审批的活跃 spinner 问题，保证权限服务在位置清理后仍可响应。
- 链接：https://github.com/anomalyco/opencode/pull/46509

### 9. 面板可见性按标签页隔离
- **#46508**：终端与审查面板的可见性改为按桌面标签页持久化，高度、PTY 会话等全局范围保持不变，标签页关闭时清除面板状态。
- 链接：https://github.com/anomalyco/opencode/pull/46508

### 10. 按调用 ID 协调最终响应
- **#46084**：修复部分兼容 OpenAI 的提供器不发送 `output_item.done` 时，通过响应完成事件按 `call_id` 匹配待处理函数调用参数的问题。
- 链接：https://github.com/anomalyco/opencode/pull/46084

---

## 功能需求趋势

| 方向 | 代表 Issues | 热度 |
|------|-----------|------|
| **2.0 配置热重载与 SDK 触发** | #43698、#42478、#42898 | 中高，正在活跃开发 |
| **MCP 工具链深入** | #40335（桌面端 MCP 管理）、#46512（Firecrawl） | 中高，持续增长 |
| **模型路由与网关** | #20235（Copilot 路由）、#44910（Zen Go 网关 500） | 高，影响日常使用 |
| **订阅/计费透明度** | #38255、#18016、#46511、#46460 | 高，投诉密集 |
|

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-09-01

## 今日速览

昨晚发布 nightly v0.22.3，主要新增了 Web Shell 的 git 状态提示与 review 流程改进。社区讨论热点集中在会话管理（resume/归档/压缩）的可靠性问题，以及多智能体任务协作中 `task_list` 的重复调用误报。此外，多个关于 CLI 可发现性、安全信任边界的 Issue 和 PR 正在快速推进中。

## 版本发布

**v0.22.3-nightly.20260831.3a0c4c6108**（2026-08-31）
- `feat(web-shell): show git state hints beside branch picker actions` — 在分支选择器操作旁展示 git 状态提示（PR #10397）
- `feat(review): emit the St…`（release notes 原文截断，完整内容请查阅 GitHub Releases 页面）

## 社区热点 Issues

本月社区围绕会话管理、多智能体协作与配置隔离展开了密集反馈，以下 10 条最值得关注：

1. **🔴 认证模型列表不同步** — [#8432](https://github.com/QwenLM/qwen-code/issues/8432)
   「阿里云百炼个人 Token 计划」内置模型列表与控制台实际列表不同步，导致图像/视频生成失败。7 条评论，是当前最热 bug，直接影响国内用户的生产使用。

2. **🔴 多智能体 `task_list` 误报死循环** — [#9450](https://github.com/QwenLM/qwen-code/issues/9450)
   Agent Team 协作中，队友反复读取共享任务状态时，因工具参数相同被误判为"duplicate tool-call loop"。`task_list` 相同参数并不代表相同结果，社区呼吁引入团队状态感知。

3. **🟠 CLI `--help` 缺失已注册参数** — [#8897](https://github.com/QwenLM/qwen-code/issues/8897)
   `--approval-mode` 与 `--auth-type` 可实际使用但不出现在 `qwen --help` 中，降低功能可发现性，6 条评论确认该问题在 0.21.9 上存在。

4. **🟠 worktree 配置写入错误位置** — [#8138](https://github.com/QwenLM/qwen-code/issues/8138)
   在 git worktree 中保存设置会写入全局/项目根目录的 `settings.json`，而非 worktree 自己的 `.qwen/`，导致多工作区配置互相污染。

5. **🟠 `--resume` 可复现已修复的悬空 thought 风险** — [#8535](https://github.com/QwenLM/qwen-code/issues/8535)
   实时会话路径中 PR #8260 已修复的"unsigned trailing thought + tool_use"隐患，在 `--resume`/`--continue` 路径上仍可被重建，历史会话恢复存在安全风险。

6. **🟠 自动压缩无法从 HTTP 413 中恢复** — [#10380](https://github.com/QwenLM/qwen-code/issues/10380)
   OpenAI 兼容网关返回 413（请求体过大）后，长会话永久不可用。自动压缩机制未针对 413 做降级/重试，是长会话可靠性的明显短板。

7. **🟠 归档活动会话引发 active/archived 冲突** — [#9688](https://github.com/QwenLM/qwen-code/issues/9688)
   归档操作成功后，正在运行的 writer 仍会以同一 session ID 重建 `chats/<id>.jsonl`，导致活跃与归档副本同时存在，Web UI 状态混乱。

8. **🟡 「Press ctrl+s」提示误导** — [#10640](https://github.com/QwenLM/qwen-code/issues/10640)
   代理回复末尾总是显示"还有更多行需要按 ctrl+s 展开"，但实际每次检查都没有更多内容。低优先级 UI bug，但影响日常使用观感。

9. **🟡 Skill 重装原子性缺陷** — [#10187](https://github.com/QwenLM/qwen-code/issues/10187)（已合并至 #10652 跟进）
   `installSkillFromUrl()` 在最终 rename 失败前会先删除现有 Skill 目录，导致更新失败时旧版本也被清空。6 轮 review 后仍遗留若干健壮性问题待解决。

10. **🟡 review CI gate 信任锚点风险** — [#10654](https://github.com/QwenLM/qwen-code/issues/10654)
    `qwen review run` 将计划、缓存账本、stop sidecar 等信任工件都写入模型会话的写面，安全设计上存在信任锚点越权的讨论空间。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*