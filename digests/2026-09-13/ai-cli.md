# AI CLI 工具社区动态日报 2026-09-13

> 生成时间: 2026-09-12 22:35 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-09-13）

## 1. 生态全景

当前 AI CLI 工具已从“能否生成代码”进入“长会话、自主代理、多模型编排是否可控”的阶段。社区焦点高度集中在稳定性、成本可观测性、MCP 生态、权限安全与跨平台一致性上。官方工具（Claude Code、Gemini CLI、Copilot CLI）与开源/社区工具（OpenCode、Qwen Code、Kimi Code CLI）并行演进，但痛点趋同：prompt cache、子代理可靠性、终端/剪贴板、沙箱与配额。与此同时，插件与执行环境抽象开始成为下一代架构竞争点。

## 2. 各工具活跃度对比

| 工具 | Release | Issues（日报披露/24h窗口） | PR（日报披露/24h窗口） | 今日社区信号 |
|---|---|---|---|---|
| **Claude Code** | v2.1.270 热修 | 热点 ≥18：10 条热点 + 8 条 ClAudit 批量关闭补充

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---

# Claude Code 社区动态日报 · 2026-09-13

数据来源：[github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)

---

## 一、今日速览

1. **热修复发布**：v2.1.270 紧急修复了 2.1.269 引入的回归——长时间运行的会话中，只读 git 命令会意外弹出权限确认。
2. **社区焦点仍在稳定性与成本**：Windows 桌面端 GPU 进程崩溃（111 条评论）仍是讨论量最高的议题；Prompt Cache 反复失效导致约 74% 缓存写入浪费的 issue 持续发酵。
3. **大批 issue 被批量标记 stale 并关闭**，覆盖 MCP、statusline、成本配额、安全审查过滤等方向——其中不少是有复现步骤、有明确影响的报告，引发对 triage 节奏的隐性担忧。

---

## 二、版本发布

### v2.1.270

> 修复：会话运行一段时间后，Bash 中的只读 git 命令会意外请求权限（2.1.269 引入的回归）

- 属于典型的"上一个版本引入 → 下一个版本回滚"的快速响应，说明 2.1.269 的权限判定逻辑改动影响面较广，触达了所有高频使用 git 的 CLI 用户。
- 建议仍停留在 2.1.269 的用户尽快升级。

---

## 三、社区热点 Issues

> 选取标准：评论量、影响范围（崩溃/数据丢失/安全/成本）、是否为可复现的回归。

### 1. Windows 桌面端 GPU 进程致命崩溃，MSIX 包进入不可启动状态
[#80444](https://github.com/anthropics/claude-code/issues/80444) · `OPEN` · 111 评论 · 👍17
- **为何重要**：通过应用内 Browser 标签触发 `0x060C201E` GPU 进程崩溃后，整个 MSIX 包变为不可启动（`appxState=2`），必须走"修复"流程才能恢复。这是**应用级不可用**，而非单次会话失败。
- **社区反应**：跨两个 NVIDIA 驱动版本均可复现，评论数远超其他 issue（111 vs 次高 12），是当前最热的稳定性问题。

### 2. Prompt Cache 多轮并行工具调用后整体重建，约 74% 缓存写入被浪费
[#63930](https://github.com/anthropics/claude-code/issues/63930) · `CLOSED (stale)` · 12 评论 · 👍7
- **为何重要**：自 ~v2.1.154（与 Opus 4.7 → 4.8 切换同期）起，会话中途 prompt cache 被反复失效，`cache_read` 塌陷到 system+tools 下限，直接转化为真金白银的成本。
- **社区反应**：报告者提供了四个会话的 token 统计作为证据，标签含 `area:cost`、`has repro`，但最终以 stale 关闭，未见到公开的修复说明。

### 3. Cowork 云会话无法访问任何 GitHub 仓库，git 代理引导调用不存在的 `add_repo` 工具
[#84581](https://github.com/anthropics/claude-code/issues/84581) · `OPEN` · 8 评论 · 👍5
- **为何重要**：云会话（Cowork）是 Claude Code 的重要增量场景，而 GitHub 访问是其核心依赖。代理提示中引用了不存在的工具名，说明服务端与客户端能力描述已脱节。
- **社区反应**：仍处于 OPEN，是今日列表中少数未被 stale 关闭的活跃问题。

### 4. 共享 claude daemon 把首个会话的 `ANTHROPIC_AUTH_TOKEN` 泄漏到机器上所有后续会话
[#79427](https://github.com/anthropics/claude-code/issues/79427) · `CLOSED` · 2 评论 · 标签 `area:security` `high-priority`
- **为何重要**：典型的"静默错误账号计费/鉴权"问题——后续所有 daemon 派生的会话都继承了首个会话的环境变量。兼具**安全**与**计费**双重风险。
- **社区反应**：被标记 high-priority 且带复现，但评论数不高，可能因为触发条件（共享 daemon + 多个 token）较窄。

### 5. Claude in Chrome 在 WSL 会话中完全不可用，桌面应用强制为 WSL 项目启用 WSL 运行时
[#93124](https://github.com/anthropics/claude-code/issues/93124) · `OPEN` · 1 评论
- **为何重要**：Windows + WSL2 是开发者的主流组合之一。桌面端一旦检测到 WSL 路径就切到 WSL 运行时，随后 CLI 因检测到 WSL 而禁用 Chrome 工具，形成**无解死锁**。
- **社区反应**：9 月 9 日新建，是较新的问题；与之呼应的还有 [#79655](https://github.com/anthropics/claude-code/issues/79655)（请求支持 WSL 下的 Claude in Chrome，👍2），说明该平台组合需求真实存在。

### 6. 全部 Cowork 项目丢失 + `cleanupPeriodDays=30` 默认值静默删除会话记录
[#86280](https://github.com/anthropics/claude-code/issues/86280) · `CLOSED (stale)` · 标签 `data-loss`
- **为何重要**：macOS 更新/重启后 `local-agent-mode-sessions` 被重建为空；更关键的是 30 天会话记录清理默认值在用户无感知的情况下执行删除。**数据保留策略的默认值需要显式告知**。
- **社区反应**：带 `data-loss` 标签却以 stale 关闭，是本次批量关闭中最值得追问的一类。

### 7. 后台任务通知被误吞入斜杠命令的 `$ARGUMENTS`，污染 prompt 并暴露内部标签
[#86651](https://github.com/anthropics/claude-code/issues/86651) · `CLOSED (stale)` · 标签 `area:core`
- **为何重要**：当后台任务通知与斜杠命令派发同时发生时，通知文本被当作该命令的参数载荷投递。这既是**数据一致性问题**，也会把内部 `<command-args>` 原始标签暴露给模型。
- **社区反应**：Windows 平台报告，含明确复现路径。

### 8. Statusline 的 OSC 8 超链接不再可点击（2.1.181 回归）
[#70161](https://github.com/anthropics/claude-code/issues/70161) · `CLOSED (stale)` · 标签 `area:tui` `regression` `reproduced`
- **为何重要**：TUI 渲染层的回归，直接影响自定义 statusline 生态（大量第三方脚本依赖 OSC 8 输出可点击链接）。带 `reproduced` 标签说明已被社区复现。
- **社区反应**：评论 5 条，👍3，属于"小但确定"的问题，长期未修复后关闭。

### 9. 用量限制提示的重置时间比实际恢复时间晚 3.5–4 小时
[#77469](https://github.com/anthropics/claude-code/issues/77469)（Windows）与 [#74165](https://github.com/anthropics/claude-code/issues/74165)（macOS）· 均已 `CLOSED (stale)`
- **为何重要**：报告者因信任错误的"重置时间"而停止工作、白白损失工时；#74165 更指出 `/usage` 显示约 3% 就已开始拒绝请求。属于**配额可观测性**问题。
- **社区反应**：两个平台独立报告同一现象，形成跨平台一致性证据链。

### 10. MCP stdio server 中途退出后：懒重连只成功一次，随后工具被错误注销且重生进程泄漏
[#74329](https://github.com/anthropics/claude-code/issues/74329) · `CLOSED (stale)` · 标签 `area:mcp` `reproduced`
- **为何重要**：MCP 工具链的可靠性直接影响 agent 能力边界。"调用成功一次 → 工具全被注销 + 僵尸进程泄漏"是难以诊断的复合故障。
- **社区反应**：由知名开发者报告（@jph00），标签含 `reproduced`，仍未获得修复说明即关闭。

**补充观察**：用户 @sworrl 单日有 **7+ 条 ClAudit 安全/AUP 误判**报告被批量 stale 关闭（[#85369](https://github.com/anthropics/claude-code/issues/85369)、[#85354](https://github.com/anthropics/claude-code/issues/85354)、[#85385](https://github.com/anthropics/claude-code/issues/85385)、[#85365](https://github.com/anthropics/claude-code/issues/85365)、[#85381](https://github.com/anthropics/claude-code/issues/85381)、[#85352](https://github.com/anthropics/claude-code/issues/85352)、[#85348](https://github.com/anthropics/claude-code/issues/85348)、[#85346](https://github.com/anthropics/claude-code/issues/85346)），均带 Request ID、可服务端复现、严重级别为 `session-halted`。这组数据值得单独关注。

---

## 四、重要 PR 进展

> 说明：过去 24 小时内仓库仅更新 **3 条 PR**，无法凑满 10 条。以下为全部条目的解读，其余内容以前述 Issue 为主。

### 1. `mods/diff`：对齐内置 `/diff` 面板表现
[#93452](https://github.com/anthropics/claude-code/pull/93452) · `CLOSED` · @poteat
- 让 `/diff` mod 的面板与内置 diff 面板一致：hunk 通过引擎的 code element 绘制、复用内置的关闭 ✕、行间距与空状态位置、窄终端下的 resize 提示行，并限制同一时间只有一个仓库探测在途。
- **信号**：`mods/` 目录的存在表明官方正在构建**可插拔 mod 体系**，且强调与内置 UI 的视觉/行为一致性。

### 2. `mods`：为 diff、sec-default、telemetry 补充单元测试，并按插件声明做类型校验
[#93912](https://github.com/anthropics/claude-code/pull/93912) · `CLOSED` · @poteat
- 测试运行在与 mod 相同的运行时环境中：每个测试拿到引擎自己的 `$` 和 hooks 模块同样的 `on`，在自身之下注册 `mock.clock` / `mock.store` / `mock.env` 或普通 hooks，并通过 `$` 驱动 mod。新增 `claude plugin test <dir>` 命令运行测试。
- **信号**：**插件测试基础设施**落地（`claude plugin test`），配套类型定义同步收紧。若你计划开发或维护 mod，这是最值得关注的变更。

### 3. `[docs]` 补充"由上下文溢出导致的假用量限制"故障排查文档
[#61716](https://github.com/anthropics/claude-code/pull/61716) · `OPEN` · @giruuuuj
- 文档化「`usage limit reached` 误报」的真实根因：上下文溢出被错误映射为用量限制，因为 `/compact` 会以 `Extra usage required for 1M context` 失败，而该错误被映射到了错误的消息上。Closes [#50321](https://github.com/anthropics/claude-code/issues/50321)。
- **临时方案**：切换到 1M 上下文模型。
- **信号**：与 Issue #77469 / #74165 属于同一类"配额可观测性"问题，从文档侧先行缓解。

---

## 五、功能需求趋势

从今日全部 Issues 中可提炼出以下方向：

| 方向 | 代表性 Issue | 社区诉求 |
|---|---|---|
| **成本与配额可观测性** | #63930、#77469、#74165、#84750、#61716 | Prompt Cache 失效原因不可见、用量限制提示与实际恢复时间不符、token 异常消耗 |
| **跨平台一致性（WSL / Windows）** | #93124、#79655、#78189、#86651 | WSL 下 Chrome 工具完全不可用、Windows 控制台窗口闪烁、平台特有的数据解析错误 |
| **云会话 / Cowork 基础设施** | #84581、#86828、#86280 | GitHub 访问被代理策略覆盖、网络策略失效、云会话数据持久性 |
| **Agent 会话生命周期管理** | #83996、#80119、#82192、#86864、#83013 | 后台 agent 被误杀/误标完成、worktree 会话无法退出、pinned 会话不可达、FleetView 分组诉求 |
| **安全与权限** | #79427、#86857、#80444 | daemon 凭证泄漏、workspace trust 对话框不弹出导致安全门失效、桌面端崩溃后包状态不可恢复 |
| **安全审查误判（ClAudit）** | #85346–#85385 系列 | 多条授权工作

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-09-13** | 数据来源：[google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli) | 统计窗口：过去 24 小时

---

## 一、今日速览

今日 nightly 发布聚焦**安全加固**：修复了通过构建文件修改与不可信 flag 触发的间接提示注入，并强化了沙箱文件系统边界。Issue 侧，**Agent 可靠性**（子代理 MAX_TURNS 误报成功、generalist agent 挂起）与**安全/记忆系统**（Auto Memory 脱敏、MCP 策略执行）是讨论最密集的两条主线。PR 侧则集中涌现一批稳定性与安全边界修复，包括终端闪烁、checkpoint 校验、shell wrapper 剥离与模型选择被静默改写等问题。

---

## 二、版本发布

### v0.61.0-nightly.20260912.g9c1b0a610

本轮 nightly 的安全属性明显增强，已披露的变更包括：

- **fix(core)**：阻止通过构建文件修改（build file modifications）与不可信 flags 实现间接提示注入（Indirect Prompt Injection）。[PR #29250](https://github.com/google-gemini/gemini-cli/pull/29250)
- **fix(sandbox)**：加固沙箱文件系统边界，将沙箱运行时状态与宿主配置目录隔离，用净化后的配置文件替代宿主目录挂载，并统一路径敏感性检查中的 realpath 解析。[PR #29214](https://github.com/google-gemini/gemini-cli/pull/29214)（已关闭/合入）

对应的版本号 bump PR 为 [#29291](https://github.com/google-gemini/gemini-cli/pull/29291)（`gemini-cli-robot` 自动生成）。Release notes 在数据源中部分截断，完整变更请以官方 Release 页面为准。

---

## 三、社区热点 Issues（10 条）

### 1. 子代理 MAX_TURNS 被误报为 GOAL 成功，掩盖中断 [#22323](https://github.com/google-gemini/gemini-cli/issues/22323)
`priority/p1` · 13 条评论 · 👍2 · 创建于 2026-03-13，长期未闭环
`codebase_investigator` 子代理在达到最大轮次限制、未做任何分析的情况下，仍返回 `status: "success"` 与 `Termination Reason: "GOAL"`。**重要性**：终止原因语义错误会让上层 Agent 和用户误判任务真实状态，是 Agent 编排可信度的基础性问题。13 条评论说明维护者与社区反复复现、定位。

### 2. 零依赖 OS 沙箱 + 执行后意图路由，释放模型 bash 原生能力 [#19873](https://github.com/google-gemini/gemini-cli/issues/19873)
`priority/p2` · 9 条评论 · 👍1
提案指出 Gemini 3 系列模型本质上是“原生 bash 用户”，习惯用 `grep`/`sed`/`awk` 链式探索代码库。方案希望在**不牺牲安全与 UX** 的前提下，通过零依赖 OS 沙箱与执行后意图路由来适配这种能力。**重要性**：这是少见的架构级提案，直接影响工具设计范式。

### 3. Generalist agent 永久挂起 [#21409](https://github.com/google-gemini/gemini-cli/issues/21409)
`priority/p1` · 8 条评论 · 👍8（本批 Issue 中最高）
只要 Gemini CLI 委派给 generalist agent，任务就会永久挂起，连创建文件夹这类简单操作也不例外；用户等待最长一小时。禁用子代理委派可绕过。**重要性**：高赞说明影响面广，属于阻塞级体验问题。

### 4. AST 感知的文件读取、搜索与代码库映射评估 [#22745](https://github.com/google-gemini/gemini-cli/issues/22745)
`priority/p2` · 7 条评论 · 👍1
EPIC 级议题，评估 AST 感知能力能否：更精确地读取方法边界、减少错位读取带来的轮次浪费与 token 噪声、支撑代码库映射。**重要性**：指向“降低上下文成本 + 提升定位精度”的中长期方向，是多个 token 优化议题的上游。

### 5. Gemini 不主动使用 skills 与子代理 [#21968](https://github.com/google-gemini/gemini-cli/issues/21968)
`priority/p2` · 6 条评论
用户反馈：除非显式指令，Gemini 几乎不会主动调用自定义 skills 或子代理，即使当前任务高度相关（如已配置 gradle、git skill）。**重要性**：这关系到 Agent 扩展机制能否真正被“自发使用”，是 skills 生态能否成立的关键。

### 6. Auto Memory 需要确定性脱敏并减少日志量 [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)
`area/security` · 5 条评论
Auto Memory 会把本地 transcript 内容发送给后台抽取代理，当前仅在 prompt 层要求模型脱敏——**内容已进入模型上下文之后**才发生。**重要性**：典型的“先泄露、后补救”风险，涉及本地隐私数据出域。

### 7. Auto Memory 对低信号会话无限重试 [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)
`priority/p2` · 4 条评论
会话只有在抽取代理成功 `read_file` 后才被标记为已处理；若代理判断为低信号而跳过读取，该会话会一直被反复捞出。**重要性**：资源浪费与潜在的重复模型调用，属于记忆子系统状态机设计缺陷。

### 8. shell 命令执行完成后卡在 “Waiting input” [#25166](https://github.com/google-gemini/gemini-cli/issues/25166)
`priority/p1` · 4 条评论 · 👍3
命令早已结束，界面仍显示 shell 命令处于活跃状态并“等待用户输入”，且发生在完全不需要交互的简单命令上。**重要性**：高频交互路径上的状态同步 bug，直接影响可用性。

### 9. browser subagent 在 Wayland 下失败 [#21983](https://github.com/google-gemini/gemini-cli/issues/21983)
`priority/p1` · `agent/browser` · 4 条评论 · 👍1
Wayland 环境下浏览器子代理直接失败，终止原因显示 GOAL。**重要性**：Linux 桌面用户（尤其较新发行版）的主路径阻塞，且与 #22323 同属“终止原因语义不可信”问题。

### 10. Browser Agent 忽略 settings.json 覆盖（如 maxTurns）[#22267](https://github.com/google-gemini/gemini-cli/issues/22267)
`priority/p2` · 3 条评论
`AgentRegistry` 初始化时能正确合并配置，但 Browser Agent 实际运行时完全忽略全局/项目级 `settings.json` 覆盖。**重要性**：配置不生效会破坏用户对 CLI 的信任，且难以自行排查。

> 其他值得跟踪：`>128 tools 触发 400 错误` [#24246](https://github.com/google-gemini/gemini-cli/issues/24246)、`Agent 应阻止破坏性行为（git reset --force）` [#22672](https://github.com/google-gemini/gemini-cli/issues/22672)、`/compress 不跨会话持久化` [#21335](https://github.com/google-gemini/gemini-cli/issues/21335)。

---

## 四、重要 PR 进展（10 条）

### 1. checkpoint 加载校验 history 必须为数组 [#29292](https://github.com/google-gemini/gemini-cli/pull/29292)（OPEN）
修复 #29194：`/resume` 加载的 checkpoint JSON 若语法合法但 `history` 非数组（如 `null`、`123`，常见于写入中断或文件损坏），此前会被当作合法对象接受，导致后续操作崩溃。本 PR 增加类型校验。

### 2. 修复 stdout 竞争与光标焦点导致的终端闪烁 [#29294](https://github.com/google-gemini/gemini-cli/pull/29294)（OPEN）
针对后台命令执行时输入、或快速输入引起的终端闪烁与撕裂，定位到 `ink` reconciler 周期中的两个并发渲染瓶颈并修复。Closes #29295。

### 3. 不再改写用户显式选择的 gemini-2.5-flash [#29217](https://github.com/google-gemini/gemini-cli/pull/29217)（OPEN）
`isFlashModel()` 使用过宽的 `endsWith('flash')` 匹配，导致 3.5 Flash GA 后 `--model gemini-2.5-flash` 被静默升级为 `gemini-3.5-flash`。**重要性**：显式模型选择被偷偷替换，会直接影响成本与可复现性。

### 4. 保留已批准的 shell 命令，避免确认重试循环 [#29201](https://github.com/google-gemini/gemini-cli/pull/29201)（OPEN）
修复 #29197：TOML 自定义命令包含多个 `!{...}` shell 注入且都需要确认时，CLI 会在命令间循环、永远无法收敛，即使用户每次都选 “always allow”。

### 5. 剥离携带额外 flags 的 shell wrapper [#29203](https://github.com/google-gemini/gemini-cli/pull/29203)（OPEN，安全）
原 `stripShellWrapper` 仅识别裸 `bash -c` / `powershell [-NoProfile] -Command`，任何额外 wrapper flag 都会让输入保持原样，而策略引擎只在剥离发生变化时才复查内层命令——形成策略绕过面。新正则容忍短 flag 簇。

### 6. MCP 策略在运行时一致强制执行 [#29200](https://github.com/google-gemini/gemini-cli/pull/29200)（OPEN，企业/非交互）
对齐 MCP 运行时策略检查与 CLI 的大小写不敏感、去空白服务器名匹配；将**显式空**的 `mcp.allowed` 列表视为 fail-closed，而非放行所有已配置

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报
**日期：2026-09-13** ｜ 数据来源：github.com/github/copilot-cli

---

## 一、今日速览

今日仓库无新版本发布，社区讨论集中在**运行稳定性与资源消耗**上：Linux 平台的内存溢出崩溃（#4725）和子代理长工具链导致的 prompt cache 失效（#4829）是当前最突出的两个性能问题。同时，供应链安全治理继续推进——GitHub 安全机器人提交的 Actions SHA 固定 PR 已合并关闭，Dependabot 则提出了两项大版本依赖升级。功能侧，MCP 取消请求、目录权限回收、多模型可观测性等议题反映出 CLI 正从"能用"走向"可控、可观测"。

---

## 二、版本发布

今日（2026-09-13 过去 24 小时）**无新 Release 发布**。

> 注：Issues 中有用户反馈运行于 `v1.0.83`（见 #4829），可作为当前主线版本参考。

---

## 三、社区热点 Issues

过去 24 小时内共有 7 条 Issue 更新。以下为全部条目及其关注价值：

### 1. #4725 🔴 Linux 平台频繁 JavaScript 堆内存溢出崩溃
- **状态**：OPEN ｜ 作者 @jbulow ｜ 创建 09-04，更新 09-12 ｜ 评论 4 ｜ 👍 1
- **要点**：CLI 每隔几分钟即以 `Mark-Compact ... allocation failure` 崩溃，堆内存已逼近 4GB 上限（4098MB），GC 无法回收。
- **为何重要**：这是本批次中**持续时间最长、讨论最活跃**的问题，属于阻塞性缺陷。当 4GB 堆被耗尽时 CLI 直接终止，对长时间会话用户是致命影响。
- 🔗 https://github.com/github/copilot-cli/issues/4725

### 2. #4829 ⚠️ 子代理单轮长工具调用序列击穿 prompt caching，token 消耗成倍放大
- **状态**：OPEN ｜ 作者 @gcapnias ｜ 更新 09-12 ｜ 评论 0
- **要点**：自定义子代理（通过 `task` 工具）在单轮内可执行数百次工具调用，导致 prompt cache 失效、token 消耗复利式增长。环境为 v1.0.83 / Windows 11 / Gemini 3.8 Flash。
- **为何重要**：直接关系到**自主代理场景的成本可控性**，是企业用户最敏感的指标之一。
- 🔗 https://github.com/github/copilot-cli/issues/4829

### 3. #4831 🖼️ 粘贴一张图后，claude-opus-5 拒绝查看任何后续图片
- **状态**：OPEN ｜ 作者 @incrediblecrab ｜ 更新 09-12 ｜ 评论 0
- **要点**：粘贴截图后，所有 `view` 调用均返回 `You've reached the maximum number of images you can view (1)`，会话内的图像配额被一次消耗殆尽。
- **为何重要**：**多模态能力在会话状态管理上的明显缺陷**，涉及新模型（claude-opus-5）适配问题，影响面广。
- 🔗 https://github.com/github/copilot-cli/issues/4831

### 4. #4759 ✅ [已关闭] MCP 取消请求未被发送
- **状态**：CLOSED ｜ 作者 @rroesch1 ｜ 更新 09-12 ｜ 评论 1
- **要点**：当工具调用等待 URL 模式 elicitation（如浏览器认证）时，用户取消操作不会向 MCP 服务端发送 cancellation 请求，造成悬挂调用。
- **为何重要**：**MCP 协议合规性问题**，今日已关闭，说明维护者已介入处理，是积极信号。
- 🔗 https://github.com/github/copilot-cli/issues/4759

### 5. #4830 📁 新增 `/remove-dir` 命令以回收目录访问权限
- **状态**：OPEN ｜ 作者 @ashutoshkbharti ｜ 更新 09-12 ｜ 评论 0
- **要点**：现有 `/add-dir` 与 `/list-dirs` 缺少对应的撤销命令，用户必须重启会话才能缩减目录访问范围。
- **为何重要**：**权限最小化**的合理诉求，与终端 AI 工具的安全审计需求高度契合，实现成本低、收益明确。
- 🔗 https://github.com/github/copilot-cli/issues/4830

### 6. #4825 📊 HydraFusion 阶段级模型/判定/额度指标接入 OpenTelemetry
- **状态**：OPEN ｜ 作者 @samueltauil ｜ 更新 09-12 ｜ 评论 0
- **要点**：一个 HydraFusion 轮次可能调用多个模型，但外部仅能看到单一答案与单一额度数字。路由决策已写入 `~/.copilot/session-state/<id>/events.jsonl`，但未暴露给 OpenTelemetry。
- **为何重要**：**可观测性是企业落地的门槛**，多模型路由的透明度直接影响成本核算与质量归因。
- 🔗 https://github.com/github/copilot-cli/issues/4825

### 7. #4824 ⌨️ `ctrl-t` 入队提示词不执行
- **状态**：OPEN ｜ 作者 @mziller ｜ 更新 09-12 ｜ 评论 1
- **要点**：`ctrl-t` 可将提示词入队，但前一个提示完成后队列不自动执行，UI 永久停留在 "Working" 状态。
- **为何重要**：典型**交互体验回归**，用户期望自动串行执行或可视化调度，属于高频使用路径。
- 🔗 https://github.com/github/copilot-cli/issues/4824

> 说明：过去 24 小时窗口内仅捕获到上述 7 条 Issue 更新，故未凑足 10 条，其余条目为历史 Issue。

---

## 四、重要 PR 进展

过去 24 小时内共有 3 条 PR 更新，全部与**供应链安全与 CI 治理**相关：

### 1. #4808 ✅ [已关闭] 将 GitHub Actions 固定到 commit SHA
- **作者**：@github-security-bot ｜ 创建 09-10，更新 09-12
- **内容**：将 4 个文件中扫描到的 3 处 `uses:` 引用全部固定为不可变 commit SHA；跳过 0、警告 0、错误 0。
- **意义**：防范 Actions 上游被劫持导致的供应链攻击，是 GitHub 官方推行的安全最佳实践，已合并落地。
- 🔗 https://github.com/github/copilot-cli/pull/4808

### 2. #4828 ⬆️ 升级 `actions/github-script` 7.1.0 → 9.0.0
- **作者**：@dependabot[bot] ｜ 更新 09-12
- **内容**：跨两个大版本升级（含 breaking changes），用于执行 GitHub API 脚本的官方 Action。
- **风险提示**：v9 为主版本跃迁，需关注 Node 运行时与 API 行为变更对现有工作流的影响。
- 🔗 https://github.com/github/copilot-cli/pull/4828

### 3. #4827 ⬆️ 升级 `actions/stale` 9.1.0 → 11.0.0
- **作者**：@dependabot[bot] ｜ 更新 09-12
- **内容**：仓库的 Issue/PR 自动标记陈旧（stale）策略依赖升级，v11 带来增强能力。
- **意义**：直接影响社区 Issue 治理效率——考虑到当前 Issue 数量与 triage 压力，该升级值得关注。
- 🔗 https://github.com/github/copilot-cli/pull/4827

> 说明：过去 24 小时窗口内仅捕获到 3 条 PR 更新，故未凑足 10 条。

---

## 五、功能需求趋势

从本批次 Issues 中可提炼出以下六大方向：

| 方向 | 代表 Issue | 社区诉求 |
|---|---|---|
| **性能与资源管理** | #4725、#4829 | 内存占用治理、prompt cache 有效性、长会话与自主代理的成本控制 |
| **MCP 协议合规** | #4759 | 完整的取消/中断语义，避免悬挂调用，保障与第三方 MCP 服务的互操作性 |
| **多模态会话状态** | #4831 | 图像配额在会话内的正确管理与跨轮次持久化 |
| **安全与权限最小化** | #4830、#4808 | 目录访问可回收、CI 引用可固化，逐步构建可审计的权限模型 |
| **可观测性 / 成本透明** | #4825 | 多模型路由的过程数据（模型、判定、额度）输出至 OpenTelemetry |
| **交互体验与多任务** | #4824 | 提示词队列的自动调度与状态可视化 |

**趋势判断**：社区关注点已从"功能是否存在"转向**"在长时、自主、多模型场景下是否可控且可解释"**。性能与可观测性两条线索交织出现，预示企业级使用场景正在成为反馈主力。

---

## 六、开发者关注点

1. **稳定性优先于新功能**
   Linux 平台的内存崩溃（#4725）持续 8 天未解、4 条评论讨论，反映出跨平台健壮性仍是短板；用户实际部署场景（长时间运行会话）与测试场景存在差距。

2. **自主代理的 token 成本失控**
   #4829 揭示了一个结构性风险：当子代理被允许在单轮内执行数百次工具调用时，缓存失效会带来数量级的成本增长。开发者需要**细粒度的执行边界控制**或**缓存友好的调用策略**。

3. **会话状态管理的一致性缺口**
   图像配额（#4831）、目录权限（#4830）、提示队列（#4824）三个问题指向同一根因：**会话内的可变状态缺少统一的读写与重置接口**，用户被迫通过重启来"恢复出厂设置"。

4. **多模型路由的透明度诉求**
   HydraFusion 的多模型编排能力已具备，但缺乏对外可观测的输出（#4825）。开发者不仅想知道答案，还想知道"是哪个模型、依据什么、花了多少额度"。

5. **供应链安全治理进入常态化**
   两个大版本依赖升级 + 一次 Actions SHA 固定合并，表明仓库已建立自动化的依赖与安全巡检机制。建议关注 v9/v11 主版本升级对既有工作流的兼容性验证。

---

*本日报基于 GitHub 公开数据自动汇总，Issue/PR 数量以过去 24 小时更新窗口为准。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-09-13）

数据来源：github.com/MoonshotAI/kimi-cli  
统计窗口：过去 24 小时  
今日数据概况：Releases 0；Issues 更新 3 条（OPEN 1 / CLOSED 2）；Pull Requests 更新 0 条。

> 说明：过去 24 小时 Issue 更新量仅 3 条，PR 为 0，因此无法按常规要求筛选出 10 个 Issue / 10 个 PR。以下为全部可用动态，不编造条目。

---

## 1. 今日速览

过去 24 小时 Kimi Code CLI 无新版本、无 PR 更新，社区动态主要集中在 Issue 区。唯一仍处于 OPEN 状态的是一条 Web UI 增强需求：希望在队列面板中加入 Steer（⚡）按钮，让用户能在 AI 运行时实时引导任务，而不是只能排队等待。另有两條历史 Bug（Web 模式刷新/端口异常、Agent 鲁莽行为）在今日窗口内显示为已关闭，但均无评论说明处理结论。

---

## 2. 版本发布

过去 24 小时无新 Release。

---

## 3. 社区热点 Issues

受数据限制，过去 24 小时仅有 3 条 Issue 更新，以下为全部条目。

### 1. #2370 [OPEN][enhancement] Web UI 队列面板增加 Steer（⚡）按钮
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2370
- 作者：@2986787982dsx-ui
- 创建：2026-05-26 / 更新：2026-09-12
- 状态：OPEN
- 社区反应：评论 1，👍 2
- 摘要：在 Windows PowerShell 通过 `kimi web` 启动的 Kimi Code Web UI 中，当 AI 正在运行时按 `Enter` 发送跟进消息，消息会进入队列。用户希望增加 Steer（⚡）按钮，以便对运行中的任务进行实时引导。
- 为什么重要：这是今日唯一 OPEN 的增强需求，指向 Web UI 的核心交互升级——从“排队等待”走向“运行中干预”。2 个 👍 表明已有初步社区认同。
- 关注点：Web UI 的任务队列控制、实时 steer 能力、运行中消息注入体验。

### 2. #1409 [CLOSED][bug] kimi cli web mode 持续刷新并连接不同端口
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1409
- 作者：@LSTM-Kirigaya
- 创建：2026-03-11 / 更新：2026-09-12
- 状态：CLOSED
- 社区反应：评论 0，👍 0
- 环境：v1.20.0，Kimi Code，kimi-for-coding，Darwin 25.2.0 arm64
- 摘要：在 coding 过程中使用 `/web` 时，网页持续刷新并连接不同端口。
- 为什么重要：Web 模式是 Kimi Code CLI 的重要入口，端口漂移和反复刷新会直接影响会话稳定性、调试连续性和可用性。该 Issue 已关闭，但无评论说明修复方式或关闭原因。
- 关注点：Web UI 连接稳定性、端口分配机制、macOS arm64 环境兼容性。

### 3. #1404 [CLOSED][bug] Reckless behaviour（鲁莽行为）
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1404
- 作者：@acorello
- 创建：2026-03-11 / 更新：2026-09-12
- 状态：CLOSED
- 社区反应：评论 0，👍 0
- 环境：v1.19.0，kimi.ai，kimi-for-coding，Darwin 25.3.0 arm64
- 摘要：用户要求 kimi 制定计划并展示，摘要在此处截断；标题指向 Agent 出现鲁莽/未受控行为。
- 为什么重要：涉及 Coding Agent 的安全边界、计划确认机制和执行可控性，是开发者信任 Agent 的关键问题。该 Issue 已关闭，但缺少评论说明，处理透明度不足。
- 关注点：Agent 行为安全、计划呈现、执行前确认、中断与回滚机制。

---

## 4. 重要 PR 进展

过去 24 小时无 Pull Request 更新，因此无重要 PR 进展可列。

---

## 5. 功能需求趋势

从当前 3 条 Issue 中可提炼出以下方向：

1. **Web UI 实时控制与任务引导**  
   #2370 明确提出 Steer（⚡）按钮，说明用户希望 AI 运行时可以实时干预、调整方向，而不是只能把消息排入队列。

2. **Web 模式稳定性与连接可靠性**

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 · 2026-09-13

> 数据来源：github.com/anomalyco/opencode

---

## 1. 今日速览

今日无新版本发布。社区注意力高度集中在**剪贴板复制/粘贴链路失效**这一跨平台顽疾上——TUI、VS Code 扩展、Web 终端（code-server / Codespaces）、Windows 终端、GNU Screen 均有人反馈"提示已复制但实际未复制"，相关 Issue 合计占据今日评论量前四名。PR 侧则以一批 2026-08-12 遗留 PR 的自动化清理（`automated-pr-cleanup`）为主，实质性的新合并进展有限。

---

## 2. 版本发布

过去 24 小时内无新 Release。

---

## 3. 社区热点 Issues

### 剪贴板问题集群（今日绝对主线）

**1. #4283 — Copy To Clipboard is not working** ⭐ 最高热度
131 条评论、123 个 👍，是今日社区声量最大的 Issue，且自 2025-11 创建至今仍未解决。用户选中模型响应文本后，界面提示复制成功但剪贴板为空。
🔗 https://github.com/anomalyco/opencode/issues/4283

**2. #13984 — can not copy and paste in opencode CLI**
57 条评论、32 个 👍。与 #4283 症状一致但出现在 CLI 场景：右上角显示"copied to clipboard"，Ctrl+V 却粘贴不出任何内容。说明问题并非单一前端渲染路径导致。
🔗 https://github.com/anomalyco/opencode/issues/13984

**3. #41470 — "Copied to clipboard" doesn't work（VSCode Server / Docker）**
22 条评论。在 Docker 内的 VS Code Server 中运行 OpenCode 时，文本无法进入系统剪贴板，属于典型的远程容器剪贴板桥接缺失。
🔗 https://github.com/anomalyco/opencode/issues/41470

**4. #26459 — Clipboard copy fails in web-based VSCode terminals**
14 条评论。覆盖 code-server、GitHub Codespaces、Remote SSH、Gitpod 等浏览器侧环境，同样表现为"UI 提示成功、实际未复制"。
🔗 https://github.com/anomalyco/opencode/issues/26459

**5. #32985 — GNU Screen 下无真彩色、复制粘贴损坏、无鼠标支持**
5 条评论、3 个 👍。Ubuntu 24.04 + Screen 4.09 场景下的终端能力协商问题，进一步说明剪贴板/终端集成缺少统一抽象层。
🔗 https://github.com/anomalyco/opencode/issues/32985

**6. #35258 / #39588 — Windows 终端与 Mac VS Code 扩展的粘贴失效**
分别覆盖 Windows（右键与 Ctrl+V 均无效）与 macOS 上的 OpenCode Beta 扩展（0.1.1 版本，右键/⌘V/菜单均不可用），显示问题跨 OS 与跨宿主形态普遍存在。
🔗 https://github.com/anomalyco/opencode/issues/35258
🔗 https://github.com/anomalyco/opencode/issues/39588

### 运行时与 2.0 架构问题

**7. #26602 — Desktop 在慢速本地 Provider 上触发 5 分钟 Headers Timeout**
12 条评论。即使配置了 `"timeout": false` 或更大超时值，OpenCode Desktop 仍会在恰好 5 分钟后中断本地 OpenAI 兼容 Provider 请求，说明超时配置未贯通到实际 HTTP 层。
🔗 https://github.com/anomalyco/opencode/issues/26602

**8. #36761 — [bug, core, 2.0] 向模型暴露合法的 subagent ID**
7 条评论。V2 的 `subagent` 工具未把已配置的 subagent ID 暴露给模型，也没有发现（discovery）操作，导致模型只能猜测 ID，委派任务在运行期失败。这是 2.0 核心可用性问题。
🔗 https://github.com/anomalyco/opencode/issues/36761

**9. #48675 — `opencode run` 零分块流停滞：无超时、无重试、无退出**
3 个并行 headless worker 在 17 秒内相继卡死在流开启状态，进程既不超时也不退出，对 CI/自动化场景是致命的静默失败。
🔗 https://github.com/anomalyco/opencode/issues/48675

**10. #48715 — Desktop server sidecar 反复崩溃（0xC0000409）+ 图像数量错误**
Windows 11 桌面端在内存压力下 sidecar 崩溃；同时"Too many images in request"错误会让会话永久不可用，附带多份 debug bundle。
🔗 https://github.com/anomalyco/opencode/issues/48715

**其他值得留意**：#31087（SSE 事件流无界内存增长，已 CLOSED）、#47258（标签页后台恢复后 SSE 不重连，需手动刷新）、#39628（从手机/第二设备远程审批权限请求）、#48721（模型键含斜杠时 `ProviderModelNotFoundError` 报错信息自相矛盾）。

---

## 4. 重要 PR 进展

> 说明：今日 PR 列表绝大部分为 `[automated-pr-cleanup]` 标记的 2026-08-12 遗留 PR 批量关闭，属仓库清理动作而非新功能推进。以下按技术价值排序。

**1. #48722 [OPEN] docs(ecosystem): add lintlang plugin**
今日唯一新开 PR，向生态插件表新增 lintlang 集成，纯文档变更。
🔗 https://github.com/anomalyco/opencode/pull/48722

**2. #42158 fix(opencode): 将 question 工具桥接到 ACP elicitation**
修复 `question` 工具在 ACP 模式下的无限阻塞——根因是 `question.asked` 事件携带的 QuestionV2 请求 ID 未回传给 `sdk.question.reply/reject`。
🔗 https://github.com/anomalyco/opencode/pull/42158

**3. #42150 fix(opencode): 文本/推理增量累积从 O(N²) 优化为 O(N)**
长会话下 delta 拼接的二次复杂度问题，直接关系长上下文性能。
🔗 https://github.com/anomalyco/opencode/pull/42150

**4. #42102 fix(llm): 保留嵌套的 OpenAI 流式错误**
将此前只合并到 `v2` 分支的嵌套 Responses SSE 错误处理回补到 `dev`，避免错误信息丢失。
🔗 https://github.com/anomalyco/opencode/pull/42102

**5. #42101 fix(console): 为 Zen 响应添加 CORS 头**
此前只在 OPTIONS 预检响应中带 CORS，实际模型列表响应缺失，导致浏览器侧调用失败。
🔗 https://github.com/anomalyco/opencode/pull/42101

**6. #42095 fix(desktop): 退出前先停止 sidecar**
修复 Linux 上关闭桌面端时 Electron NodeService 被 SIGABRT 终止、服务端清理未完成的问题——与今日 #48715 的 sidecar 崩溃现象互为印证。
🔗 https://github.com/anomalyco/opencode/pull/42095

**7. #42022 fix(opencode): 校验 upgrade 请求**
要求 `POST /global/upgrade` 携带 `application/json`（强制走 CORS 预检），并拒绝非合法语义版本的升级目标，属安全加固。
🔗 https://github.com/anomalyco/opencode/pull/42022

**8. #42087 fix(desktop): 限制应用启动范围**
只允许 "Open in" 菜单中暴露的应用穿越桌面 IPC 边界，Windows 可执行路径在主进程校验后解析，属 IPC 攻击面收敛。
🔗 https://github.com/anomalyco/opencode/pull/42087

**9. #42084 fix: 保留 apply_patch 的尾部空行**
修复文件以 `\n\n` 结尾时，补丁未触碰该处却被静默删除最后一行空行的问题。
🔗 https://github.com/anomalyco/opencode/pull/42084

**10. #42020 fix(mcp): 本地 MCP Server 瞬时启动失败时重试**
MCP 并行 spawn（`concurrency: "unbounded"`）下的竞态失败重试，与 #43845（V2 service 每个项目目录各 spawn 一对 MCP）共同指向 MCP 生命周期管理的薄弱环节。
🔗 https://github.com/anomalyco/opencode/pull/42020

**另可关注**：#42063（拒绝空压缩摘要，避免静默丢上下文）、#42056（会话选择器中的目录过滤快捷键失效）、#42052（多行显示 `&&` 链式 shell 命令）、#42112（TUI 显示 tok/s 吞吐）。

---

## 5. 功能需求趋势

| 方向 | 代表 Issue | 趋势判断 |
|---|---|---|
| **终端/剪贴板集成可靠性** | #4283、#13984、#41470、#26459、#32985、#35258、#39588、#47165、#44056 | 今日最集中的方向。需求本质是从"渲染层复制"走向"逻辑文本 + 宿主剪贴板 API"的统一抽象，覆盖 SSH、容器、Web IDE、Screen、Windows 终端等全部宿主形态 |
| **2.0 / v2 架构完善** | #36761、#47258、#43845、#48636、#48720、#48718 | subagent ID 暴露、SSE 重连、service 进程模型、TUI 草稿保护、slash 技能参数丢失——均为 v2 落地期的能力缺口 |
| **健壮性与错误可观测性** | #48675、#38866、#26602、#48721 | 社区不再只关注功能，而是要求"失败必须可见"：流停滞要超时/重试/退出，子代理错误不能被伪装成空成功结果 |
| **性能与资源占用** | #31087、#42150、#43845、#26602 | 无界内存增长、O(N²) 累积、进程膨胀，指向长会话与多项目场景 |
| **权限与远程协作** | #39628、#48651 | 移动端/第二设备审批、Plan Mode 被绕过，反映长任务无人值守场景的真实需求 |
| **模型与配额支持** | #48687、#48721、#48681 | DeepSeek 4.1 Flash 周限额计算异常、含斜杠的自定义模型键、订阅后仍提示超限 |
| **桌面端体验细节** | #48661、#48656、#48715 | 面板最大化/恢复、默认主题对比度过低、sidecar 稳定性 |

---

## 6. 开发者关注点

1. **剪贴板是最高优先级、最长寿的痛点。** #4283 自 2025-11 挂起近 10 个月，累积 131 条评论与 123 个 👍，说明这不是边缘场景，而是核心交互路径缺失。多宿主（TUI / 扩展 / Web IDE / 容器 / Screen）共享同一根因，需要一次性架构性解决，而非逐个打补丁。

2. **超时与重试语义不一致，配置不生效。** `"timeout": false` 被 5 分钟硬超时覆盖（#26602）；零分块流停滞既无超时也无重试也无退出（#48675）。开发者期待的是可预测、可配置的失败边界。

3. **错误被静默吞掉，破坏自动化信任。** 子代理流错误最终以空 `<task_result></task_result>` 返回（#38866），headless worker 静默卡死（#48675），`ProviderModelNotFoundError` 建议的模型串就是报错的同一个串（#48721）。对 CI/Agent 编排场景，静默失败比报错更危险。

4. **进程与内存生命周期需系统性收敛。** SSE 无界内存增长（#31087）、V

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 · 2026-09-13

> 数据源：github.com/QwenLM/qwen-code

---

## 一、今日速览

今天社区最核心的矛盾集中在**TUI 稳定性**上：Ink `useBoxMetrics` 引发的 React #185 崩溃已从一个边缘场景扩散为可复现的高优先级问题，并直接催生了对应的补丁 PR。与此同时，**执行环境可分离化**（沙箱 / 容器 / 远程执行）成为核心架构讨论主线，Issue #11695 与 PR #11711、#11746 构成一条完整的技术演进链。Web Shell / daemon 侧则继续高频迭代，PWA、上下文可视化、模型配置等能力同步推进。

---

## 二、版本发布

**v0.23.3-nightly.20260912.54aa66834b**（nightly）

- `refactor(dingtalk)`: 移除已废弃的后台响应聚合逻辑（@qqqys, #11570）
- `feat(channels)!`: 含破坏性变更的 channels 相关调整（提交标题在数据源中被截断，具体影响范围需查阅 PR 正文）

> 提示：该 nightly 为常规构建，未包含针对当前 P1 崩溃（React #185）的修复。

---

## 三、社区热点 Issues（Top 10）

1. **#11500 [P1][OPEN] TUI 在多个后台 agent 完成时静默退出（React #185）** — 今日讨论度最高（10 条评论）。根因定位到 Ink `useBoxMetrics` 的 layout-listener → setState 循环，会话恢复时 CLI 还会误报"上次会话异常"。这是当前最影响可用性的缺陷。https://github.com/QwenLM/qwen-code/issues/11500

2. **#11732 [P1][OPEN] 0.23.3 原生 monitor 长任务运行时崩溃** — 与 #11500 同一失败模式的两个独立会话复现，说明该崩溃已从"后台 agent"扩展到"长任务监控"场景，影响面扩大。https://github.com/QwenLM/qwen-code/issues/11732

3. **#11695 [P2][OPEN] tracking(core): 将 agent harness 与执行环境解耦** — 由 @wenshao 提出的伞形方向，主张工具执行位置应成为运行时可寻址、可替换的一部分，而非进程属性。这是本轮架构演进的总纲，直接牵引下面的 #11711 / #11746。https://github.com/QwenLM/qwen-code/issues/11695

4. **#11704 [P3][OPEN] 提案：官方 Android 伴生客户端（基于 ACP 连接 qwen serve）** — 作者愿意自行实现 MVP 并长期维护，定位为瘦客户端而非在手机上跑完整运行时。反映了移动端接入的明确社区诉求。https://github.com/QwenLM/qwen-code/issues/11704

5. **#11198 [P1][OPEN] 遥测默认上传未脱敏的工具错误文本（含 shell 命令行）** — 隐私风险面比 #10916 更广，属于存量问题。安全类 P1 长期挂起，值得维护者优先处理。https://github.com/QwenLM/qwen-code/issues/11198

6. **#11666 [P2][CLOSED] telemetry：`logPrompts=false` 时仍导出 API 请求内容** — 与上条构成同一族隐私问题，已关闭，说明该类问题正在被收敛，但 #11198 仍需跟进。https://github.com/QwenLM/qwen-code/issues/11666

7. **#10834 [P2][OPEN] MCP 工具返回的图片绕过 read_file 图像预算，全分辨率进入上下文** — 与 `read_file` 的 1568px 缩放策略不一致，是上下文膨胀与成本失控的隐性来源，已 ready-for-agent。https://github.com/QwenLM/qwen-code/issues/10834

8. **#11499 [P2][OPEN] `.mcp.json` 中的 `${VAR}` 占位符未展开** — 导致 `Authorization: Bearer ${MY_TOKEN}` 被字面发送，MCP 配置中无法安全使用环境变量，是接入体验上的硬伤。https://github.com/QwenLM/qwen-code/issues/11499

9. **#11610 [P1][OPEN] hooks：与 Claude Code 契约对齐（stdout、stop_hook_active、超时单位、matchers 等）** — 引擎结构已基本对等，剩余差异集中在契约细节。对齐后可显著降低用户迁移成本，需要讨论。https://github.com/QwenLM/qwen-code/issues/11610

10. **#11657 [P1][CLOSED] Fireworks：Qwen3 工具调用续写因镜像 `messages[].reasoning` 返回 400** — 真实的第三方 provider 兼容性缺陷，首次响应可正常返回 reasoning + tool call，续写即失败，已修复关闭。https://github.com/QwenLM/qwen-code/issues/11657

**其他值得留意**：#11724（Windows 下 7GB 内存占用并中断会话）、#11710（Virtual Viewport 退出后终端状态残留，`nano` 报 `[ Unknown sequence ]`）、#11718（Desktop AppImage 的 `PYTHONHOME`/`PYTHONPATH` 泄漏导致 stdio MCP 的 Python 解释器崩溃）、#11577 / #10953（Goal 与 Todo 状态一致性问题，均已有对应修复）。

---

## 四、重要 PR 进展（Top 10）

1. **#11711 [OPEN] feat(core): 为 subagent 增加容器化执行环境** — #11695 的落地实现：通过 `QWEN_AGENT_EXECUTION_BACKEND` 启用 Docker/Podman，Agent 工具可选 `execution_backend: "container"` 并搭配 worktree 隔离。是沙箱化多智能体的关键一步。https://github.com/QwenLM/qwen-code/pull/11711

2. **#11565 [OPEN] fix(cli): 打断 Ink useBoxMetrics 的 commit 阶段 setState 循环（React #185）** — 通过扩展 `patches/ink+7.0.3.patch` 直接修复 #11500 的崩溃根因，是今天最值得跟进合并的补丁。https://github.com/QwenLM/qwen-code/pull/11565

3. **#11700 [OPEN] feat(web-shell): 改进上下文概览并支持手动压缩** — composer tooltip 显示精确剩余容量，上下文卡片展示 used/total、剩余空间与分类明细，历史卡片标记为快照。直接回应长会话的上下文管理痛点。https://github.com/QwenLM/qwen-code/pull/11700

4. **#11538 [OPEN] feat: 按模型选择 OpenAI API（chat-completions / responses）** — 为 OpenAI 兼容 provider 增加模型级 `api` 字段，解决不同端点能力差异带来的适配问题。https://github.com/QwenLM/qwen-code/pull/11538

5. **#11342 [OPEN] feat(web-shell): 模型角色与上下文窗口配置** — Advisor、图像、语音模型分别使用端点感知选择器，自定义配置区分对话、图像生成、语音转写用途。Web Shell 可配置性的一次系统性提升。https://github.com/QwenLM/qwen-code/pull/11342

6. **#11692 [OPEN] feat(core): web_search 预算可配置并限制提取器回退** — 新增 `tools.webSearch.timeoutMs`（默认由 60s 提升至 120s，支持 `WEB_SEARCH_TIMEOUT_MS`），并约束超时后交给模型的内容量。https://github.com/QwenLM/qwen-code/pull/11692

7. **#10183 [OPEN] feat(memory): 结构化按需召回** — 将扁平、正文臃肿的记忆提示演进为 push/pull 两级 ref/title 树 + 专用检索工具，长期记忆质量的关键改进。https://github.com/QwenLM/qwen-code/pull/10183

8. **#11291 [OPEN] fix(core): 对无状态码的上游错误重试而非终止回合** — 处理网关在已返回 200 的 SSE 流中推送错误对象的情况，避免一轮对话因瞬时故障直接失败。https://github.com/QwenLM/qwen-code/pull/11291

9. **#11727 [OPEN] fix(core): 由生产者自身预算决定 shell 输出大小** — 解决工具截断与调度器截断两套策略互相冲突的问题（工具保留尾部以保住退出码/信号/错误摘要）。https://github.com/QwenLM/qwen-code/pull/11727

10. **#11722 [OPEN] feat(web-shell): 增加可安装 PWA 支持** — 安装后启动直达 server 根路径，不内嵌凭据或会话地址；含 service worker 与离线失败处理，配合 #11704 的移动端诉求。https://github.com/QwenLM/qwen-code/pull/11722

**其他值得关注**：#11606（DashScope metadata 仅对 qwen 家族发送）、#11690（Goal 停顿检查点分批重跑，已关闭）、#10906（Web Shell 展示 Shell/Monitor 任务输出）、#11635（会话侧边栏展示定时任务）、#11163（Web Shell 管理 git remotes）、#9305（VP 模式短内容底部对齐）、#10455（输出语言文件不可写时不再崩溃启动）。

---

## 五、功能需求趋势

- **执行环境抽象与沙箱化（最强主线）**：#11695（harness/executor 分离）→ #11711（容器后端）→ #11746（SSH 远程 worker，当前 blocked）→ #11704（Android 瘦客户端）。社区正在把"agent 在哪里跑工具"提升为一等公民概念。
- **Web Shell / daemon 能力扩张**：PWA 安装、模型角色与上下文窗口配置、上下文可视化与手动压缩、git remotes 管理、定时任务与任务输出面板——Web 端已从预览界面演化为完整的交互入口。
- **多智能体与任务编排**：subagent 容器执行、Todo/Goal 状态一致性（#10953、#11577、#11689）、Goal 检查点分批重试，围绕长任务可靠性持续补齐。
- **MCP 生态质量**：环境变量展开（#11499）、图像预算（#10834）、AppImage 环境变量泄漏（#11718）——从"能连上"走向"连得干净、安全、可预测"。
- **Provider 兼容性**：OpenAI responses API 选择（#11538）、DashScope metadata 条件化（#11606）、Fireworks reasoning 镜像（#11657），第三方模型接入成为常态化维护面。
- **安全与隐私默认值**：遥测脱敏（#11198、#11666）、凭据安全、shell 数据隐私，安全类 Issue 标签密度明显上升。
- **跨平台细节**：Windows 内存（#11724）、Linux 打包

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*