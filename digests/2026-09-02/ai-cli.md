# AI CLI 工具社区动态日报 2026-09-02

> 生成时间: 2026-09-01 22:35 UTC | 覆盖工具: 7 个

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

# Claude Code 社区动态日报

**日期：2026-09-02** | 数据来源：github.com/anthropics/claude-code


## 今日速览

昨日连续发布两个补丁版本：**v2.1.257** 引入新模型 Claude Fable 5.1 并新增时间显示设置，**v2.1.258** 紧急修复了 macOS 12 启动回归。社区方面，一个 Windows 上 Claude Desktop 窗口始终置顶的老 Issue 热度持续攀升（125 👍 / 57 评论），同时新报告了 v2.1.257 在 macOS 12 上因 dyld 符号缺失直接无法启动的回归。过去 24 小时 Issue 更新活跃（50 条），但 PR 仅有 1 条合并。


## 版本发布

### v2.1.258（补丁修复）
- **修复**：macOS 12 (Monterey) 启动失败 —— 这是 2.1.255 引入的回归，本次专门修复
- **修复**：远程/计划会话在权限审批重发后报错 `"user messages must have non-empty content"` 的问题

### v2.1.257（功能新增）
- **新增模型**：Claude Fable 5.1（`claude-fable-5-1`），现为默认 Fable 模型。具备 **1M 上下文窗口**，定价 $10/$50 per Mtok，缓存读取 $0.25/Mtok
- **新增设置**：`timeFormat`（12/24 小时制、24 小时 UTC 或自定义 strftime 模板）与 `timeZone`，用于控制回合结束时钟与转录显示


## 社区热点 Issues（Top 10）

### 🔥 1. Claude Desktop (Windows)：主窗口始终置顶，无设置可关闭
**#85891** | 开放中 | 作者 @kylealty-boop | 👍 125 | 💬 57

Windows 11 上桌面版窗口表现为 topmost，即使焦点切换到其他应用也始终绘制在最上层，且应用内没有关闭开关。这是 macOS 端 #66516 的 Windows 对应问题。**这是当前社区关注度最高的 Issue**——125 个 👍 遥遥领先，Windows 用户对此体验问题反馈强烈，但官方至今未给出解决方案或时间表。

[查看 Issue](https://github.com/anthropics/claude-code/issues/85891)

### 🔥 2. v2.1.257 在 macOS 12 启动即崩溃（dyld: _DNSServiceGetAddrInfoEx）
**#91309** | 开放中 | 作者 @adamjali | 👍 1 | 💬 1

**与最新版本直接相关的高优先级回归**。自动更新器将 v2.1.257 安装到 macOS 12 后，应用因缺少 `_DNSServiceGetAddrInfoEx` 符号启动即 abort，且更新器会一直安装这个不可用版本。虽然 v2.1.258 已修复此问题，但已安装 v2.1.257 的用户更新路径是否顺畅仍需验证。

[查看 Issue](https://github.com/anthropics/claude-code/issues/91309)

### 🔥 3. 桌面版持续弹出无标签横幅："This tab shows a single file and can't follow links"
**#91332** | 开放中 | 作者 @khal1234 | 💬 3

桌面应用（非 CLI/VS Code）在使用中反复弹出无标题横幅，提示"此标签页显示单个文件，无法点击链接"，但没有提供任何关闭/忽略选项。桌面端 UI 细节问题，虽然评论不多，但属于高频出现的干扰性体验 bug，且缺少明确的触发场景说明。

[查看 Issue](https://github.com/anthropics/claude-code/issues/91332)

### 🔥 4. modelPicker 跳过 `opusplan` 行，但选择器中却不显示 Opus Plan Mode
**#89690** | 开放中 | 作者 @urda | 💬 2 | 含复现步骤

`modelPicker` 中 `model` 为 `opusplan` 的配置行永远不会出现在 `/model` 选择器里——系统认为它已被内置 lineup 覆盖，但实际上普通会话的 lineup 中**根本没有** Opus Plan Mode 这一行。`opusplan` 是模式（mode）而非模型，导致该配置完全不可达。

[查看 Issue](https://github.com/anthropics/claude-code/issues/89690)

### 🔥 5. 子代理与父会话同进程运行：无隔离、无环境区分标记
**#74417** | 已关闭（stale） | 作者 @malformed-c | 💬 3

Task/Agent 工具派生的子代理与父会话运行在**完全相同的 OS 进程**中，环境变量完全一致，无法通过 `CLAUDE_CODE_CHILD_SESSION` 等标记区分"我是子代理"还是"我是顶层会话"。对需要进程级隔离的权限控制、资源限制和调试场景有重大影响，是 Agent 架构演进中的核心欠账。

[查看 Issue](https://github.com/anthropics/claude-code/issues/74417)

### 🔥 6. 会话内 `/logout` 静默终止所有持久化，12 小时对话记录丢失
**#76267** | 已关闭（stale） | 作者 @alexgetu | 👍 1 | 💬 2

运行 `/logout` 再重新认证后，会话进入"无持久化"状态：对话仍可正常继续，但从那一刻起所有新消息都不再写入 transcript、历史记录和注册表，最终导致 **12 小时的对话记录全部丢失**。数据可靠性问题，用户毫无感知地丢失会话记录，影响严重。

[查看 Issue](https://github.com/anthropics/claude-code/issues/76267)

### 🔥 7. LSP 插件找不到用户 PATH 中的语言服务器（Windows）
**#75612** | 已关闭（stale） | 作者 @r3bb1t | 💬 7

`rust-analyzer`、`clangd` 等语言服务器若安装在**用户级 PATH**（而非系统级 PATH），LSP 插件启动时报 `Command 'X' not found or is in an unsafe location`。Windows 平台 PATH 作用域差异问题，影响大量使用 Scoop/用户级安装的开发者。

[查看 Issue](https://github.com/anthropics/claude-code/issues/75612)

### 🔥 8. bypassPermissions 模式在 UNC 路径下仍弹 Edit/Write 确认
**#41914** | 已关闭（stale） | 作者 @mklod | 👍 8 | 💬 5

`bypassPermissions` 模式下，当工作目录或文件路径为 Windows UNC 路径（`\server\share\...`）时，Edit/Write 工具仍会强制弹出"是否进行此编辑"的确认框。权限绕过模式在 UNC 环境下失效，4 个月未修复，Windows 企业网络用户影响面持续存在。

[查看 Issue](https://github.com/anthropics/claude-code/issues/41914)

### 🔥 9. run_in_background 任务完成通知被路由到错误的会话
**#76174** | 已关闭（stale） | 作者 @YayoRazo | 💬 4

Bash 工具 `run_in_background: true` 启动的后台任务，完成后的 `<task-notification>` 有时不会发送给发起会话，而是被投递到另一个无关会话——恰好是列表中的另一个活跃会话。多会话并行场景下通知串线会导致用户错过关键任务结果。

[查看 Issue](https://github.com/anthropics/claude-code/issues/76174)

### 🔥 10. MCP 工具响应在并发子代理负载下返回其他调用数据
**#76198** | 已关闭（stale） | 作者 @cameron-bales-telus-health | 💬 1

**并发场景下的数据串线问题**。多个子代理并行执行时，MCP 工具调用偶发返回**另一个并发工具调用**的数据，而非自身请求的结果。对于依赖 MCP 做数据读取/写入的 Agent 工作流，这种串线可能导致脏写或错误的业务决策，属于典型的并发竞态 bug。

[查看 Issue](https://github.com/anthropics/claude-code/issues/76198)


## 重要 PR 进展

> ⚠️ 过去 24 小时仅 **1** 条 PR 更新，以下为完整收录。

### #78371 Harden ralph-wiggum 插件：边界迭代 + 推送/发布守卫 + stop-hook 修复
**状态**：已关闭 | 作者 @kazukinakai | 更新于 2026-09-01

对 `ralph-wiggum` 插件（无限循环执行的工具）进行安全加固：
- **有界迭代**：限制循环最大执行次数，避免失控
- **push/publish 守卫**：阻止无人值守的循环在迭代中途执行 git push、merge、publish、deploy 等危险操作
- **stop-hook 修复**：修正在特定流程下停止钩子不生效的问题

**意义**：虽然仅为社区插件，但反映出"Agent 安全边界"已成为社区自发关注的重点方向——防止自主循环造成不可逆的外发操作是当前 Agent 工程化的核心议题之一。

[查看 PR](https://github.com/anthropics/claude-code/pull/78371)


## 功能需求趋势

从昨日活跃的 50 条 Issue 中提炼出社区最关注的五大方向：

1. **Agent/子代理架构演进**（#74417、#75904、#69022、#76204、#76198）
   - 进程隔离、独立环境标记、并发数据隔离成为核心诉求
   - 用户已在小规模（3-5 workers）与大规模（20-30 workers）两种模式下使用 agent teams，迫切需求**按需启动/按团队配置 MCP 作用域**与**精简引导模式**

2. **Windows 平台体验一致性**（#85891、#75612、#41914、#76174）
   - 窗口行为、PATH 解析、UNC 路径权限、后台通知路由等问题密集出现
   - 多条老 Issue 在 8/31-9/1 被批量标记 stale 关闭，社区对此类"静默关闭"存在不满

3. **模型与模式选择器的可配置性**（#89690）
   - 新模式（如 Opus Plan Mode）无法通过 modelPicker 正确暴露，配置系统与模型线之间出现"覆盖盲区"
   - v2.1.257 新增 Fable 5.1 后，模型配置灵活性成为新热点

4. **会话持久化与数据可靠性**（#76267、#75924、#76206）
   - `/logout` 静默停写、压缩后历史"看得见但模型摸不着"、远程会话命名丢失——用户对会话数据的**完整性和可恢复性**要求明确上升

5. **MCP 生态的稳定性**（#74913、#76198）
   - 从系统代理（PAC）干扰到并发响应串线，MCP 在复杂网络与并发场景下暴露的稳定性问题开始被系统性报告


## 开发者关注点

1. **macOS 12 用户安全感

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-09-02

## 今日速览

Codex 于昨日发布 rust-v0.152.0 与 v0.152.1 两个正式版本，带来 Vim 模式搜索、速率限制横幅操作等新功能，并修复了 Guardian 审批中的 Node REPL 策略问题。社区方面，多消息对话回复错乱（#8648，已获 83 条评论）与语音转录功能（#3000，获 218 👍）成为讨论最热烈的话题，Windows/WSL 兼容问题也出现了多个新报告。

## 版本发布

**发布版本：rust-v0.152.1（Bug Fix）**
- 修复 Guardian approval review 未遵循模型元数据中 Node REPL 策略的问题。
- 完整变更：https://github.com/openai/codex/compare/rust-v0.152.0...rust-v0.152.1

**发布版本：rust-v0.152.0（新功能）**
- Vim 模式新增 `/` 和 `?` 搜索、高亮匹配以及 `n`/`N` 重复导航（#41586）。
- 速率限制横幅现在提供查看用量、管理额度、重置限制、管理套餐等操作入口（#41742）。
- 终端 UI 与 `codex exec` 也有功能更新。
- 另发布了 0.153.0 系列三个 alpha 版本（alpha.1/alpha.2/alpha.4），未注明具体变更内容。

## 社区热点 Issues

1. **Codex 回复旧消息而非最新消息**（#8648，评论 83，👍 62） 
   - 多轮对话中 Codex 偶尔会错误地回复较早的消息而不是最新消息，GPT-5.2-xhigh 上出现，社区大量用户推测与上下文排序或 compaction 有关。
   - https://github.com/openai/codex/issues/8648

2. **IDE 扩展的语音转录功能**（#3000，评论 36，👍 218）
   - 社区希望在 Codex 面板中加入 push-to-talk 麦克风按钮，直接语音输入 prompt 和后续修改。已持续近一年，是目前 👍 最多的需求之一。
   - https://github.com/openai/codex/issues/3000

3. **TUI 的语音转录支持**（#14630，评论 22，👍 58）
   - CLI 用户希望复用 Codex App 的语音转录模型，替代目前系统级听写，提升语音输入质量。
   - https://github.com/openai/codex/issues/14630

4. **审批模式只读选项**（#11915，评论 20，👍 41）
   - 用户希望增加 "read-only" approval 模式，让 Codex 可读文件但不允许任何写操作，用于涉密或生产环境代码审查。
   - https://github.com/openai/codex/issues/11915

5. **Windows 桌面版 Browser Use / Node REPL 在 WSL 工作区失败**（#29639，评论 18）
   - 桌面应用生成 Windows 版 node_repl.exe，却收到 Linux/WSL 路径的 sandboxCwd，导致 MCP 工具调用映射失败，WSL 用户受影响。
   - https://github.com/openai/codex/issues/29639

6. **macOS 更新后全局 UI 文字变细且模糊**（#40782，评论 12）
   - 26.820.60940 版本后中文界面（简中）下文字渲染异常发虚，疑似字体平滑或缩放 regression，影响日常阅读。
   - https://github.com/openai/codex/issues/40782

7. **Codex 作用域内存管理**（#18343，评论 12，👍 11）
   - 提议支持 global / project / hybrid / per-thread 四层 memory scope，避免全局记忆环境污染特定项目。
   - https://github.com/openai/codex/issues/18343

8. **Windows 桌面版更新后本地执行失败**（#41088，评论 11）
   - 26.820.7780.0 更新后 Codex Desktop 在 Windows 上无法启动本地执行，可能与环境变量或权限迁移有关。
   - https://github.com/openai/codex/issues/41088

9. **WSL2 下 codex-code-mode-host 0.147.0 每次 shell exec 崩溃**（#38417，评论 11）
   - SIGTRAP 固定在偏移 0x982442 处触发，0.146.1 正常，属于明确的 0.147.0 regression，影响所有 WSL2 用户。
   - https://github.com/openai/codex/issues/38417

10. **Windows 桌面版更新后历史本地项目消失**（#39121，评论 11）
    - 26.810.7004.0 更新后历史项目列表丢失，任务保留、新项目正常，疑似本地索引或会话存储 schema 迁移 bug。
    - https://github.com/openai/codex/issues/39121

## 重要 PR 进展

1. **Full Access 下跳过 Guardian 审查**（#42147）
   - 当 `approvalPolicy: "never"` 且权限不受限时，确认类操作不再触发模型审查，减少不必要的 Guardian 开销。
   - https://github.com/openai/codex/pull/42147

2. **在 executor 上下文中解析权限请求**（#42146）
   - `request_permissions` 的路径和授权将基于选定的 executor 环境（路径规范、家目录、工作区根目录、临时目录）进行解析，修复跨平台路径误判。
   - https://github.com/openai/codex/pull/42146

3. **新增 Guardian V2 分析事件**（#42144）
   - 新增 `codex_guardian_v2_classification` 和 `codex_guardian_v2_fast_decision` 埋点，可观测风险等级、耗时、模型和线程归属。
   - https://github.com/openai/codex/pull/42144

4. **Plus/Team 计划早期速率限制警告**（#42142）
   - Plus 和 Team 用户在约 5 小时用量窗口剩余不足 50% 时提前警告，其他计划保持原有 75%/90%/95% 阈值。
   - https://github.com/openai/codex/pull/42142

5. **Vim composer 历史支持 redo**（#42140）
   - 新增有界 redo 栈，`Ctrl+R` 在 Vim normal 模式下可重做撤销的完整草稿（含粘贴内容和图片附件），并支持 `vim_no_redo` 配置。
   - https://github.com/openai/codex/pull/42140

6. **为符合条件的轮次预热 shell 快照**（#42137）
   - 在 turn hooks 接受轮次后异步捕获登录 shell 环境，避免 Shell Snapshot V2 在命令启动时阻塞命令路径。
   - https://github.com/openai/codex/pull/42137

7. **支持符号链接会话根目录的线程 fork**（#42135）
   - 修复 `sessions` 目录为符号链接时 fork 分页恢复线程失败的 bug，统一使用规范化路径校验 rollout lineage。
   - https://github.com/openai/codex/pull/42135

8. **MCP 审批请求携带应用链接元数据**（#42134 + #42133）
   - 在 MCP 工具审批中保留 `link_id`，并按 app account link 作用域化审批记忆，避免不同账号间审批错误复用。
   - https://github.com/openai/codex/pull/42134
   - https://github.com/openai/codex/pull/42133

9. **限制 Git 根目录发现的阻塞**（#42132）
   - 为 Git root 发现增加共享并发限制，避免文件系统探测耗尽 Tokio blocking pool 或延迟运行时关闭。
   - https://github.com/openai/codex/pull/42132

10. **修复 macOS 相对路径 MCP 服务器启动**（#42117）
    - Rust 在 macOS 上相对可执行路径 + 工作目录组合会回退到 `fork`（历史 `posix_spawnp` 问题），现改为更可靠的方式启动。
    - https://github.com/openai/codex/pull/42117

## 功能需求趋势

- **语音交互大热**：TUI 与 IDE 扩展的语音转录是两个独立但高赞的 issue（合计 276 👍），语音 prompt 已成为社区最期待的功能方向。
- **更细粒度的安全策略**：包括只读审批模式（#11915）、Full Access 下的删除操作硬确认（#33624），社区对沙箱权限的精细化控制需求显著上升。
- **作用域化记忆/状态管理**：#18343 要求 memory 支持 project/per-thread 作用域，#20958 提出 `/goal` 的意图校准与 side-thread 容忍，长任务状态管理开始受到关注。
- **跨平台稳定性**：Windows 桌面版、WSL2、macOS 的多个 bug 显示跨平台执行环境（特别是 WSL 路径映射）是当前主要的稳定性短板。
- **Agent 行为可靠性**：#42115、#40646、#37278 等新 issue 集中在 agent 丢失任务焦点、违反约束、误报执行状态等问题，模型行为可控性成为高优先级话题。
- **安全护栏（Guardian）演进**：多个 PR 围绕 Guardian V2 的跳过逻辑、分析事件、权限上下文解析展开，表明安全审查系统正在快速迭代。

## 开发者关注点

- **对话上下文管理问题突出**：#8648（回复错乱）、#36642（auto-compaction 静默丢弃历史）、#31659（compaction 丢失 goal）共同指向长对话上下文维护是目前最影响日常使用的问题。
- **自动压缩（Auto-compaction）不可靠**：#36642 报告 0.145.0 后压缩会静默丢弃所有历史，且无法感知；#31659 显示压缩后目标丢失、回到追踪近期 prompt 的状态。
- **Windows/WSL 兼容性问题集中爆发**：当天 50 条 issue 中约 8 条与 Windows 相关，涉及桌面版更新故障、WSL 路径映射、pet overlay 交互失效、本地执行启动失败等，Windows 用户的更新体验和 WSL 支持是明显的痛点。
- **更新引入回归**：多个 issue（#41088、#39121、#40782）直接指向桌面版更新后的功能回退或 UI 异常，开发者在版本更新上存在"不敢升级"的情绪。
- **安全与权限控制呼声增强**：除只读模式外，社区对 Full Access 下危险操作缺乏硬确认（#33624）、agent 修改项目级 config 无需授权（#15680）等问题反馈集中，安全机制需要更主动的防护。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-09-02

## 1. 今日速览

昨日 v0.58.0 正式版发布，包含 symlink 路径处理修复及多项 core 重构。社区讨论集中在子代理可靠性问题（假成功、挂起）与安全加固——一个涉及硬编码 Google API Key 的 PR 和 macOS 下认证挂起的新 Issue 尤为值得关注。同时，多起针对符号链接、NTFS 短路径名、BOM 编码等文件系统兼容性问题的修复正密集推进。

## 2. 版本发布

过去 24 小时共发布 3 个版本：

- **v0.58.0（正式版）**：修复了 ignore 路径处理中的 symlink 一致性求值问题，并包含 core 重构。同步更新了变更日志。
  https://github.com/google-gemini/gemini-cli/releases/tag/v0.58.0
- **v0.59.0-preview.0（预览版）**：包含 core 修复（防止…），为下个主版本的功能预览。
  https://github.com/google-gemini/gemini-cli/releases/tag/v0.59.0-preview.0
- **v0.59.0-nightly.20260901.g0bd1d4397（夜间版）**：常规每日构建。
  https://github.com/google-gemini/gemini-cli/releases/tag/v0.59.0-nightly.20260901.g0bd1d4397

## 3. 社区热点 Issues

挑选了 10 个讨论度最高或影响面最大的 Issue：

| Issue | 标题 | 评论 | 优先级 | 看点 |
|---|---|---|---|---|
| [#22323](https://github.com/google-gemini/gemini-cli/issues/22323) | Subagent recovery after MAX_TURNS is reported as GOAL success | 13 | P1 | 子代理在触发最大轮次限制后被错误报告为“成功”，会**掩盖真实的中断原因**，是目前最热门的 bug |
| [#19873](https://github.com/google-gemini/gemini-cli/issues/19873) | Zero-Dependency OS Sandboxing & Post-Execution Intent Routing | 9 | P2 | 提出利用模型原生的 bash 能力，通过**零依赖沙箱**保障安全，是一个方向性的增强提案 |
| [#21409](https://github.com/google-gemini/gemini-cli/issues/21409) | Generalist agent hangs | 8 | P1 | 一旦交给 generalist agent 执行任务（如创建文件夹）就会**永久挂起**，用户只能手动取消，影响大 |
| [#22745](https://github.com/google-gemini/gemini-cli/issues/22745) | Assess the impact of AST-aware file reads, search, and mapping | 7 | P2 | 探索 **AST 感知**的文件读取与搜索能力，有望减少 token 消耗和轮次浪费 |
| [#21968](https://github.com/google-gemini/gemini-cli/issues/21968) | Gemini does not use skills and sub-agents enough | 6 | P2 | 用户反馈 Gemini **几乎不会主动使用**自定义 skills 和子代理，需要显式指令才生效 |
| [#26525](https://github.com/google-gemini/gemini-cli/issues/26525) | Add deterministic redaction and reduce Auto Memory logging | 5 | P2 | 安全相关：Auto Memory 将明文内容先送入模型上下文再“指示”其脱敏，流程设计存在**确定性隐患** |
| [#25166](https://github.com/google-gemini/gemini-cli/issues/25166) | Shell command execution gets stuck with "Waiting input" | 4 | P1 | Shell 命令执行完毕后界面仍显示“等待输入”，简单命令也会触发，高频复现 |
| [#29153](https://github.com/google-gemini/gemini-cli/issues/29153) | v0.57.0 hangs on "Waiting for authentication..." in subdirectories on macOS | 2 | P1 | **当天提交的新 Issue**：在 macOS 子目录下启动 v0.57.0 卡死在认证界面，属于回归问题 |
| [#20079](https://github.com/google-gemini/gemini-cli/issues/20079) | ~/.gemini/agents/filename.md symlink is not recognized as agent | 4 | P2 | 符号链接形式的 agent 文件无法被识别，影响使用 dotfiles 管理配置的用户 |
| [#22672](https://github.com/google-gemini/gemini-cli/issues/22672) | Agent should stop/discourage destructive behavior | 3 | P2 | 模型在复杂 git 操作中倾向使用 `git reset`、`--force` 等**危险命令**，社区呼吁加入安全护栏 |

## 4. 重要 PR 进展

以下 10 个 PR 反映了当前社区的主要修复方向：

| PR | 标题 | 状态 | 看点 |
|---|---|---|---|
| [#29163](https://github.com/google-gemini/gemini-cli/pull/29163) | fix(cli): prevent crash during authentication in git repositories | OPEN | 修复 macOS Seatbelt 或受限权限环境下在 Git 仓库内启动崩溃的**认证回归问题**（对应 Issue #29153） |
| [#29158](https://github.com/google-gemini/gemini-cli/pull/29158) | fix(core): sanitize and remove hardcoded Google CrUX API key | OPEN | 移除编译产物中**硬编码的 Google API Key**，避免凭据泄露到发布的 npm 包中，安全修复 |
| [#29156](https://github.com/google-gemini/gemini-cli/pull/29156) | fix(core): stop nullifying user git config in shell executions | OPEN | 此前的改动将 `GIT_CONFIG_GLOBAL` 指向 `/dev/null`，导致用户的 `user.name` 等配置丢失，本 PR 修复该回归 |
| [#29155](https://github.com/google-gemini/gemini-cli/pull/29155) | fix(core): decode BOM-encoded content correctly in isEmpty | OPEN | 修复 UTF-16/UTF-32 编码的 BOM 文件被误判为非空的问题，影响计划文件校验 |
| [#29151](https://github.com/google-gemini/gemini-cli/pull/29151) | fix(core): handle skill precedence and active state case-insensitively | OPEN | 修复 Skill 优先级覆盖因**大小写不匹配**失效的问题（如 `MySkill` 与 `myskill`） |
| [#29117](https://github.com/google-gemini/gemini-cli/pull/29117) | fix(core): enforce RFC 9207 issuer identification in MCP OAuth flow | OPEN | 在 MCP OAuth 流程中实施 **RFC 9207 issuer 验证**，防止 token 被路由到恶意端点 |
| [#29116](https://github.com/google-gemini/gemini-cli/pull/29116) | fix(core): mitigate NTFS 8.3 short name (SFN) path | OPEN | 处理 Windows NTFS 短文件名（如 `git~1`）导致的**路径穿越与黑名单绕过**问题 |
| [#28975](https://github.com/google-gemini/gemini-cli/pull/28975) | fix(core): keep glob results for symlinked workspace roots | OPEN | 修复工作区根目录通过符号链接访问时 glob 返回“No files found”的问题（macOS `/tmp` 场景） |
| [#29106](https://github.com/google-gemini/gemini-cli/pull/29106) | fix(core): flush final SSE event on EOF without trailing blank line | OPEN | 修复 SSE 流在无尾随空行结束时**丢失 final event**（如 `finishReason`）的问题 |
| [#29115](https://github.com/google-gemini/gemini-cli/pull/29115) | fix(config): enforce strict permission and ownership checks on system-wide config | OPEN | 对 Windows/POSIX 的系统级配置文件实施**所有权与 ACL 校验**后再加载，防止本地提权攻击 |

## 5. 功能需求趋势

从近期的 Issue 与 PR 中可以提炼出社区关注的四个核心方向：

1. **Agent/子代理可靠性与可观测性**（约 50% 的热门 Issue）
   - 子代理的失败被误报为成功、generalist 挂起、不主动使用 skills/sub-agents、trajectory 无法通过 `/chat share` 分享等——社区对 agent 运行状态的透明度和可控性需求极高。
   - [Issue #22323](https://github.com/google-gemini/gemini-cli/issues/22323)、[#22598](https://github.com/google-gemini/gemini-cli/issues/22598)

2. **安全加固**
   - 涉及 API Key 硬编码、OAuth issuer 校验、Auto Memory 脱敏逻辑、配置文件权限验证等多个方面。安全左移的趋势明显。
   - [PR #29158](https://github.com/google-gemini/gemini-cli/pull/29158)、[#26525](https://github.com/google-gemini/gemini-cli/issues/26525)

3. **文件系统兼容性修补**
   - 符号链接（symlink）、NTFS 8.3 短文件名、BOM 编码、Windows junction 等边缘场景密集出现。开发者使用的文件系统多样性远超预期。
   - [PR #29116](https://github.com/google-gemini/gemini-cli/pull/29116)、[#28975](https://github.com/google-gemini/gemini-cli/pull/28975)

4. **模型行为引导与约束**
   - 社区希望模型能：自动正确使用 skills/sub-agents、避免破坏性 git 命令、不在随机位置创建临时脚本、不创建交互式任务（如 vite）。本质上是对 **agent 行为边界的精细化控制** 诉求。
   - [Issue #22672](https://github.com/google-gemini/gemini-cli/issues/22672)、[#23571](https://github.com/google-gemini/gemini-cli/issues/23571)

## 6. 开发者关注点

从近期反馈中归纳出的高频痛点和需求：

- **子代理“假成功”是信任杀手**：`codebase_investigator` 触达 MAX_TURNS 后仍报告 `GOAL` 成功，用户无法区分真实完成与中断。这类问题会严重削弱对 agent 自动化的信任。
- **认证与 Shell 执行的稳定性问题**：macOS 认证挂起（#29153）、Shell 执行后卡在 “Waiting input”（#25166）都是 P1 级别的日常开发阻塞问题，且反馈集中。
- **安全合规成为阻塞项**：硬编码 API key 的移除和配置文件的权限检查表明，企业用户在尝试落地 Gemini CLI 时对安全审查十分敏感。
- **配置与环境的“隐藏行为”引发困惑**：例如 Shell 执行时静默置空 `GIT_CONFIG_GLOBAL` 导致用户 git 身份丢失。开发者希望 CLI 的执行环境与本地环境保持一致，不做隐式修改。

---

*数据时间范围：2026-08-31 至 2026-09-02（GitHub

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-09-02）

## 今日速览

今日发布了 **v1.0.83-1**，主要带来 split Sessions 侧边栏排序记忆与企业级登录固定组织能力。Issue 方面，**会话恢复时的内存溢出（OOM）** 和 **MCP 协议兼容问题** 成为社区讨论焦点；BYOK（自带密钥）相关回归（`/model` 命令失效、模型 ID 发送错误）也受到较多关注。过去 24 小时无 Pull Request 更新。

---

## 版本发布

### v1.0.83-1
- **新增**：split Sessions 侧边栏支持按 Recent、Created、Name 及经典 None 排序，选定顺序会在重启后保留；企业管理员可通过 `forceLoginOrgs` 托管设置将登录固定到已批准的 GitHub 组织。
- **改进**：优化 `/mcp config` 以及 MCP 服务器添加/编辑流程。

---

## 社区热点 Issues（Top 10）

### 1. [#13 CLI input should have a vi/vim input mode](https://github.com/github/copilot-cli/issues/13)
- **热度**：👍 75，评论 9，状态 Closed（更新时间 2026-09-01）
- **要点**：用户强烈需求在 Copilot CLI 交互界面中支持 vi/vim 风格键盘操作。虽然该 Issue 已关闭，但 75 个赞表明终端模态编辑仍是社区呼声最高的体验改进之一。

### 2. [#4664 Copilot CLI crashes with JavaScript heap out of memory when resuming a long-standing session](https://github.com/github/copilot-cli/issues/4664)
- **热度**：评论 5，状态 Open
- **要点**：恢复长时间运行的大会话时 Node.js 堆内存溢出，导致崩溃。这直接影响到重度用户的日常使用，社区希望官方能优化会话序列化/加载机制或提供分页加载。

### 3. [#4525 1.0.81-1 sends legacy `initialize` after successful modern `server/discover`, causing -32022](https://github.com/github/copilot-cli/issues/4525)
- **热度**：评论 4，状态 Open
- **要点**：与 Python MCP SDK 2.0.0 双时代运行器存在协议兼容问题：CLI 先发送现代 `server/discover` 探测，随后又发送旧版 `initialize`，导致 MCP 初始化失败。该问题影响大量 MCP 服务器整合场景。

### 4. [#3688 Repository-level custom agents resolved relative to git root, but skills and .mcp.json relative to cwd](https://github.com/github/copilot-cli/issues/3688)
- **热度**：评论 3，👍 3，状态 Open
- **要点**：仓库级自定义代理、技能和 `.mcp.json` 的解析基准目录不一致，导致同一仓库内不同目录下行为不同。社区认为这是配置发现机制的设计缺陷。

### 5. [#4438 disable-model-invocation: true makes a skill unreachable, not manual-only](https://github.com/github/copilot-cli/issues/4438)
- **热度**：评论 3，👍 5，状态 Open
- **要点**：技能声明 `disable-model-invocation: true` 后，用户无法通过显式调用触发该技能，`skill()` 工具返回 "Skill not found"。社区希望该配置只阻止模型自动调用，而非完全禁用手动调用。

### 6. [#4680 CLI sends wrong model ID to custom OpenAI-compatible endpoint, killing the session](https://github.com/github/copilot-cli/issues/4680)
- **热度**：评论 2，状态 Open
- **要点**：使用自定义 OpenAI 兼容端点时，CLI 将请求体中的模型名硬编码为 `gpt-5.4-nano`，忽略配置的 `mimo-v2.5`，导致会话直接失效。BYOK 用户受影响严重。

### 7. [#4672 1.0.82 Regression: Unknown command: /model with BYOK](https://github.com/github/copilot-cli/issues/4672)
- **热度**：评论 2，👍 1，状态 Open
- **要点**：1.0.81/82 回归：通过环境变量配置 BYOK 模型后，`/model` 命令不再可用。对于托管多种模型的 Azure AI Foundry 用户，这是阻断性问题。

### 8. [#4686 Node.js OOM crash after ~37 min — 31,965 leaked async libuv handles (SEA ignores NODE_OPTIONS)](https://github.com/github/copilot-cli/issues/4686)
- **热度**：评论 1，状态 Open
- **要点**：运行约 37 分钟后因泄漏 31,965 个异步 libuv 句柄触发 OOM，且 SEA（单文件可执行文件）模式忽略 `NODE_OPTIONS`，用户无法通过环境变量调优。这提示底层运行时存在长期资源泄漏。

### 9. [#4674 Resuming a session does not restore the custom agent (regression of #917)](https://github.com/github/copilot-cli/issues/4674)
- **热度**：评论 0，状态 Open
- **要点**：恢复会话时未恢复自定义代理，其 `mcp-servers` 与 `tools` 白名单全部丢失，会话静默退化为无代理状态。这是对旧问题 #917 的回归，影响依赖自定义代理的团队。

### 10. [#4678 ACP: session/new blocks for 192s on a single unresponsive MCP server (no bounded MCP startup budget)](https://github.com/github/copilot-cli/issues/4678)
- **热度**：评论 0，状态 Open
- **要点**：ACP 模式下 `session/new` 会等待所有 MCP 服务器连接完成，单个无响应 HTTP MCP 服务导致会话创建延迟高达 192 秒。社区希望引入 MCP 启动超时或并行预算控制。

---

## 重要 PR 进展

过去 24 小时内**无 Pull Request 更新**（0 条）。

---

## 功能需求趋势

从近期 Issues 中提炼的社区核心功能诉求包括：

- **终端编辑体验**：vi/vim 模态输入模式（#13）仍是最受关注的交互改进方向。
- **会话/上下文管理**：需要更健全的会话恢复机制——既要避免 OOM（#4664、#4686），也要保证恢复后自定义代理、指令文件等上下文不丢失（#4674、#4687）。
- **MCP 生态兼容**：重视与不同 MCP SDK 的协议握手、OAuth 认证细节、启动超时控制，以及服务器连接失败时的优雅降级（#4525、#4681、#4678）。
- **BYOK/自定义模型支持**：修复模型 ID 透传、`/model` 命令回归、`session.resume` 忽略新模型参数等问题（#4680、#4672、#4645）。
- **配置路径一致性**：要求自定义代理、技能和 `.mcp.json` 的解析基准目录统一（#3688）。
- **精细化权限控制**：希望支持路径级别的持久写入审批（#4682），而非全有或全无。
- **资源调度优化**：子代理并发限制应感知系统负载，避免拖垮宿主机和 CLI 自身 UI（#4688

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-09-02

## 今日速览

- Kimi Code CLI 发布 **v1.50.0**，修复了 kosong 协议层误发 `anthropic-beta` 头的问题，并落地了 deprecation-aware 更新流程（含一键迁移至 Kimi Code）。
- 近期更新的 2 个 Issue 均已关闭：一个涉及「连续任务无法预写提示词」的需求，另一个是「Task 子任务偶发卡死」的 bug（反馈版本 v1.16.0）。
- PR 侧呈现出一个明显信号：项目正围绕**「向 Kimi Code 迁移」**做基础设施改造，同时补齐插件系统的安全与持久化数据文档。

## 版本发布

**v1.50.0**（发布于 2026-09-01）

本版本聚焦稳定性与升级体验：

- `fix(kosong)`：未声明任何 beta 特性时，不再发送空的 `anthropic-beta` 请求头，避免对上游网关产生干扰（[#2580](https://github.com/MoonshotAI/kimi-cli/pull/2580)）。
- `chore(release)`：将 kosong 子包升级至 v0.56.0（[#2581](https://github.com/MoonshotAI/kimi-cli/pull/2581)）。
- `feat(shell)`：新增 deprecation-aware 更新流程——当 CDN 发布迁移公告时，CLI 会将当前 Python 发行版标记为 deprecated，并引导用户一键迁移至 Kimi Code（[#2630](https://github.com/MoonshotAI/kimi-cli/pull/2630)）。

## 社区热点 Issues

> 过去 24 小时内共 2 条 Issue 更新，均已关闭。全部列出如下：

### 1. [#1287] [增强] 执行当前任务时，无法为下一个任务编写提示词
- **作者**：@XiaoPengYouCode
- **状态**：已关闭
- **背景**：执行一个长耗时任务时，下一任务的 Prompt 输入框仍处于锁定状态，用户无法提前准备下一个指令，影响连续任务的流水线效率。
- **社区反应**：1 条评论。该需求本质上是**任务队列/预输入**能力，对批量脚本型用户较为关键。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/1287

### 2. [#1292] [缺陷] 调用 Task 时有时会卡住
- **作者**：@Wolido
- **状态**：已关闭
- **版本**：kimi v1.16.0 / Darwin 25.3.0 arm64
- **梗概**：多个 Task 子任务并发执行时，某几个子任务会无响应卡死。
- **社区反应**：暂无评论。该 bug 直击多任务可靠性，可能涉及任务调度或模型响应处理。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/1292

## 重要 PR 进展

> 过去 24 小时内共 4 条 PR 更新，按影响面排序全部列出：

### 1. [#2630] [已关闭] feat(shell): deprecation-aware 更新流程与一键迁移 Kimi Code
- **作者**：@jackfish212
- **内容**：读取 CDN 上的迁移公告（`kimi_cli/migration.json`），当新版发布时，CLI 自动感知废弃状态，并在升级过程中提供一键迁移至 Kimi Code 的交互。
- **意义**：属于 kimi-cli 向 Kimi Code 收敛的战略性改动，直接影响所有 Python 发行版用户的升级路径。
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2630

### 2. [#2614] [开启] docs(plugins): 补充插件安全与持久化数据文档
- **作者**：@QIANLING-0831
- **内容**：纯文档改动，明确插件合约边界：`plugin.json`、基于命令的工具、`inject` 机制以及 `~/.kimi/plugins/` 安装目录；并说明插件持久化数据与安全模型。
- **意义**：为第三方插件开发者提供了可依据的规范，降低误用风险。
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2614

### 3. [#2632] [已关闭] chore(release): bump kimi-cli 至 1.50.0
- **作者**：@sailist
- **内容**：发布流程 PR，同步 `packages/kimi-code` 的 wrapper 版本与 `kimi-cli==1.50.0` 依赖锁定，并移动 release notes。
- **意义**：保证 pip 包与仓库 tag 版本一致，属于例行发布同步。
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2632

### 4. [#742] [已关闭] 添加 `$ list` skills（如 codex）
- **作者**：@ZacharyZhang-NY
- **内容**：提议新增 `$ list` 命令，用以展示可用 skills，对齐 codex CLI 的交互方式。
- **状态说明**：已于今日被关闭，但未在 PR 描述中找到明确的关闭原因；推测为**超出当前里程碑范围**或已迁移至 Kimi Code 方向。建议关注后续的 skills 可发现性功能是否以新形态出现。
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/742

## 功能需求趋势

从近期活动的 Issue 与 PR 来看，社区关注度集中在以下四个方向：

1. **任务编排与预输入**：用户希望在任务执行期间提前编写下一个 Prompt，以减少等待、提升批处理效率（[#1287](https://github.com/MoonshotAI/kimi-cli/issues/1287)）。
2. **CLI 可扩展性与技能发现**：参考 codex 实现方式，新增 `$ list skills` 命令，增强技能的可探索性（[#742](https://github.com/MoonshotAI/kimi-cli/pull/742)）。
3. **迁移与废弃流程**：官方主动推动从 kimi-cli 到 Kimi Code 的平滑迁移，社区对这一路径的透明度与自动化接受度较高（[#2630](https://github.com/MoonshotAI/kimi-cli/pull/2630)）。
4. **插件生态规范化**：文档层面对齐插件的安全边界和数据持久化规则，为后续插件生态扩张打好基础（[#2614](https://github.com/MoonshotAI/kimi-cli/pull/2614)）。

## 开发者关注点

- **并发任务卡死是当前最尖锐的稳定性问题**：多个 Task 子任务并发时可能无响应（反馈于 v1.16.0）。虽然 Issue 已关闭，但**尚未看到公开的修复说明**，建议在 v1.50.0 中主动做回归验证。
- **连续任务的交互阻塞**：执行当前任务时无法预写下一任务 Prompt，影响自动化和 Composer 式工作流，已有用户明确提出改进需求。
- **升级路径的确定性**：从「deprecation-aware 更新流程」的合并可以看出，开发者对**废弃提示 + 一键迁移**的体验诉求强烈；期待 Kimi Code 迁移期间，旧版本能保留足够长的过渡期，并保持数据/配置兼容。
- **文档先行**：插件安全与持久化数据的文档化，反映出插件开发者对**明确规范**的渴求，侧面说明社区第三方插件已有一定规模。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-09-02

## 今日速览

OpenCode 发布 v1.18.26 补丁版本，集中修复了 Claude 5 会话、Bedrock GPT-5.6 推理参数等稳定性问题。社区方面，**模型自动发现**（#6231）以 225 👍 成为最受关注的功能请求；**剪贴板复制失效**（#4283）已积累 128 条评论，成为持续最久的未解决痛点。此外，多条自动化 PR 进入清理合并阶段，涉及权限提示、Provider 解析、MCP 重连等多个核心模块。

## 版本发布

### v1.18.26

**核心 Bug 修复：**
- **Claude 5 会话**：容忍提示或工具变更后残留的 stale thinking blocks，不再导致会话失败
- **Bedrock GPT-5.6**：`none` reasoning effort 现在可被正确接受
- **Bedrock reasoning 与 replay** 处理可靠性提升（贡献者：[@pengzh1](https://github.com/pengzh1)）
- **工具调用计时** 在特定场景下保持精确

---

## 社区热点 Issues

### 1. Copy To Clipboard is not working — 用户耐心逼近极限
**Issue [#4283](https://github.com/anomalyco/opencode/issues/4283)** · 评论 128 · 👍 119 · 开放中

> 从 2025 年 11 月报告至今仍未修复，用户用 1.0.62 旧版本复现，选择响应文本无法复制到剪贴板。超长生命周期 + 高评论数说明该问题影响面广且复现稳定。

### 2. Auto-discover models from OpenAI-compatible provider endpoints — 社区最强呼声
**Issue [#6231](https://github.com/anomalyco/opencode/issues/6231)** · 评论 47 · 👍 225 · 开放中

> 针对 LM Studio、Ollama、llama.cpp 等本地 Provider，用户希望自动发现 `/v1/models` 中的模型，而不是手动在 `opencode.json` 中逐一列举。225 个 👍 表明这是本地模型工作流中迫切的基础能力。

### 3. System Theme no longer works after v1.0.0
**Issue [#3688](https://github.com/anomalyco/opencode/issues/3688)** · 评论 38 · 👍 20 · 已关闭

> v1.0.0 后 `System` 主题选项消失，配置 `system` 也不生效。38 条评论说明回归影响范围不小，虽已关闭但值得关注后续是否真正修复。

### 4. Add config option to disable copy-on-select behavior — 与 #4283 呼应的次生需求
**Issue [#10490](https://github.com/anomalyco/opencode/issues/10490)** · 评论 18 · 👍 32 · 开放中

> 用户希望增加 `opencode.json` 配置项，关闭"选中即复制"的类 XTerm 行为。此需求与 #4283 的剪贴板问题叠加，说明 OpenCode 在剪贴板交互设计上存在系统性缺陷。

### 5. opencode is using CPU for doing nothing! — 空闲状态吃 CPU
**Issue [#19466](https://github.com/anomalyco/opencode/issues/19466)** · 评论 16 · 👍 16 · 开放中

> API 限流重试等待期间（`retrying in 18m 12s`），i9-14900 单核占用 ~50%。长时间等待 + 高 CPU 消耗，对开发者笔记本续航和风扇噪音都是明显干扰。

### 6. `permission.ask` plugin hook is defined but not triggered
**Issue [#7006](https://github.com/anomalyco/opencode/issues/7006)** · 评论 14 · 👍 24 · 开放中

> 插件中定义的 `permission.ask` hook 不触发，导致自定义自动批准逻辑完全失效。这直接打击了插件的可编程性，是权限系统（PermissionV2）的重要缺陷。

### 7. cli tab completions for bash, fish, and zsh — 长期搁置的基础体验
**Issue [#1515](https://github.com/anomalyco/opencode/issues/1515)** · 评论 11 · 👍 33 · 已关闭

> 请求通过 `source <(opencode completions $SHELL)` 提供 shell 补全。虽然已关闭，但 33 👍 说明该功能仍是高频需求，关闭原因待查（可能已实现或排期）。

### 8. Support Multiple Skills in a Single Prompt — 多框架工作流受阻
**Issue [#25570](https://github.com/anomalyco/opencode/issues/25570)** · 评论 8 · 👍 22 · 开放中

> 当前无法在单次 prompt 中指定多个 skills，多框架项目需要反复切换上下文。这是 Skills 生态从"单点能力"走向"工作流编排"的关键一步。

### 9. LM Studio shows only 3/9 models — 自动发现确实坏了
**Issue [#18011](https://github.com/anomalyco/opencode/issues/18011)** · 评论 7 · 👍 5 · 开放中

> LM Studio 0.4.6 `/v1/models` 返回 9 个模型，OpenCode 只显示 3 个。这为 #6231 提供了实证：自动发现不仅缺失，现有发现逻辑还有 bug。

### 10. Unlimited usage Exploit on opencode models — 安全漏洞报告
**Issue [#34344](https://github.com/anomalyco/opencode/issues/34344)** · 评论 7 · 👍 0 · 开放中

> 免费模型的速率限制绑定 IP，VPN 轮换即可绕过限制无限使用。虽然 👍 为 0，但这是一个真实的服务滥用漏洞，涉及 DeepSeek v4 Flash 和 mimo v2.5 等免费模型。

---

## 重要 PR 进展

### 1. fix(app): show review diffs for non-git VCS backends
**PR [#46684](https://github.com/anomalyco/opencode/pull/46684)** · 开放中 · 2026-09-01

> 修复会话审查面板对非 git VCS（Mercurial 或插件注册的其他后端）的 diff 展示问题，`normalize...` 逻辑扩展。

### 2. fix(core): materialize pending state incrementally
**PR [#46631](https://github.com/anomalyco/opencode/pull/46631)** · 开放中 · 2026-09-01

> 插件启动期间 OAuth 方法已注册但不可读，导致过期的 saved credential 刷新失败、Console 请求失败、账号模型缺失。增量物化 pending state 解决启动竞态。

### 3. fix(console): order Go usage chart by request count
**PR [#40103](https://github.com/anomalyco/opencode/pull/40103)** · 已关闭 · 2026-09-01 更新

> 修复 Go 用量图表排序：Kimi K3 应排在 Grok 4.5 之上，按每五小时请求数正确排序。

### 4. fix(opencode): clear stale permission prompts
**PR [#40100](https://github.com/anomalyco/opencode/pull/40100)** · 已关闭 · 2026-09-01 更新

> 被中断或销毁的权限请求从服务端移除时未发布 `permission.replied`，导致 Web/Desktop 客户端界面卡死。关闭 #29422。

### 5. fix(opencode): finish prompt loop by parent link
**PR [#40099](https://github.com/anomalyco/opencode/pull/40099)** · 已关闭 · 2026-09-01 更新

> 通过 `parentID` 而非消息 ID 比较来完成 assistant turn 到 user message 的链接，避免客户端/服务端时钟不一致导致的循环无法结束。

### 6. refactor(opencode): propagate typed Skill.NotFoundError instead of defect
**PR [#40092](https://github.com/anomalyco/opencode/pull/40092)** · 已关闭 · 2026-09-01 更新

> 按照 `ERR-4` 规范，将 `Effect.die(...)` 调用改为类型化的 `Skill.NotFoundError`，提升 Skills 错误可恢复性。

### 7. fix(core): expand AWS_REGION in Bedrock Mantle base URL
**PR [#40076](https://github.com/anomalyco/opencode/pull/40076)** · 已关闭 · 2026-09-01 更新

> 目录中 Mantle 端点模板 `https://bedrock-mantle.${AWS_REGION}.api.aws/openai/v1` 未正确替换 `AWS_REGION` 环境变量，v1 地址被字面使用导致请求失败。

### 8. fix(provider): parse URL-based provider IDs

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*