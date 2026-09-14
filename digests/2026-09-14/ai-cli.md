# AI CLI 工具社区动态日报 2026-09-14

> 生成时间: 2026-09-14 00:16 UTC | 覆盖工具: 7 个

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

# Claude Code Skills 社区热点报告（截至 2026-09-14）

> 数据说明：PR 评论数字段为 `undefined`，以下“热门 PR”按仓库给出的评论数排序顺序选取；所列 PR 当前均为 **OPEN**。

## 1. 热门 Skills 排行（PR Top 8）

1. **#1298 fix(skill-creator): run_eval.py 永远报告 0% recall**  
   功能：修复技能评估链路，安装 eval artifact 为真实 skill，并修 Windows 流读取、触发检测、并行 worker。  
   热点：评估循环在噪声上优化，关联 Issue #556 的 10+ 次独立复现。状态：OPEN。  
   https://github.com/anthropics/skills/pull/1298

2. **#1742 fix(mcp-builder): 支持 mcp>=2 的 streamable_http_client 和 custom headers**  
   功能：适配 MCP SDK 2.

---

# Claude Code 社区动态日报
**日期：2026-09-14** ｜ 数据来源：github.com/anthropics/claude-code

---

## 一、今日速览

今日无新版本发布，社区热度集中在**存量长期 Issue 的持续发酵**与**新增平台级 Bug** 上：Windows 桌面端重启动失败的 Issue（#42776）累计 182 条评论，Visual Studio 2026 集成请求（#15942）以 437 👍 保持最高呼声。过去 24 小时共有 50 个 Issue 有更新，新增问题集中在 Skill 变量替换异常、Remote Control 会话生命周期、以及鼠标捕获/配置文件被全局改写等"可控性与可预期性"类痛点上。

---

## 二、版本发布

过去 24 小时无新 Releases。

---

## 三、社区热点 Issues（Top 10）

### 1. Windows 桌面端因孤儿进程文件锁无法重启 ⭐ 评论最多
[#42776](https://github.com/anthropics/claude-code/issues/42776) ｜ OPEN ｜ 182 评论 ｜ 88 👍 ｜ 创建于 2026-04-02
Windows 上 Claude Code Desktop 退出后残留孤儿进程持有文件锁，导致应用无法重新启动。**这是当前社区讨论量最高的活跃 Bug**，且自 4 月创建至今横跨 5 个多月仍未修复，评论持续增长说明影响面广、绕过方案不彻底。

### 2. Visual Studio 2026 集成请求 ⭐ 点赞最高
[#15942](https://github.com/anthropics/claude-code/issues/15942) ｜ OPEN ｜ 152 评论 ｜ 437 👍 ｜ 创建于 2026-01-01
请求为 Visual Studio 2026 提供官方集成。437 个 👍 是全量数据中的最高值，反映出 **IDE 集成广度**仍是社区最强烈的诉求，尤其在 VS Code / JetBrains 之外的 .NET 技术栈。

### 3. VS Code 扩展：关闭"自动附加当前文件/选区"
[#24726](https://github.com/anthropics/claude-code/issues/24726) ｜ OPEN ｜ 73 评论 ｜ 237 👍
侧边栏自动把打开的文件或选中代码附加进上下文，用户无法关闭。高赞 + 高评论表明这不是个例，而是**上下文注入的默认行为与用户预期冲突**的典型问题，与今天新增的 #94052 属同一类。

### 4. Agent 层级可视化面板（TUI + Desktop）
[#24537](https://github.com/anthropics/claude-code/issues/24537) ｜ OPEN ｜ 18 评论 ｜ 19 👍
为多 Agent 工作流提供统一的实时层级视图。随着 Agent 编排能力增强，**"看得见"正在成为与"跑得动"同等重要的需求**，该 Issue 同时打上了 cost / tui / core / ide 多个标签，说明其影响面跨越多个子系统。

### 5. `/model` 与 `/effort` 全局改写 settings.json
[#66402](https://github.com/anthropics/claude-code/issues/66402) ｜ OPEN ｜ 16 评论 ｜ 14 👍
两个命令会立即写入 `~/.claude/settings.json`，导致 `claude agents` 的 fleet 视图无法为不同 Agent 配置独立模型与推理强度。**这是"全局配置 vs 多 Agent 隔离"的结构性冲突**，对生产级多 Agent 使用场景影响很大。

### 6. 桌面端定时任务模型选择端到端失效
[#91884](https://github.com/anthropics/claude-code/issues/91884) ｜ OPEN ｜ 5 评论 ｜ 0 👍
macOS Desktop 的定时任务在 spawn 时忽略用户设置、文档中描述的模型选择器不存在、MCP 工具缺少 model 参数——三处同时断裂。带 `documentation` 与 `has repro` 标签，属**文档与实现不一致**的典型，容易造成用户长时间误配。

### 7. Windows Cowork：device_bash 永久失效
[#93442](https://github.com/anthropics/claude-code/issues/93442) ｜ OPEN ｜ 2 评论 ｜ 1 👍
报错为 "no Plan9 drive shares mounted"，重启应用乃至重启操作系统后依然存在。区别于普通 Bug，它**跨越应用与 OS 重启仍无法恢复**，是环境层级的硬故障。

### 8. Skill 加载时 `$1`–`$19` 被替换为无关对话文本
[#94065](https://github.com/anthropics/claude-code/issues/94065) ｜ OPEN ｜ 1 评论 ｜ 0 👍 ｜ 2026-09-13 新建
Skill Markdown 中的字面量 `$5`、`$19` 会被替换成当前对话中的无关片段，而 CLAUDE.md 不受影响。这是**新发生且可复现**的问题，直接破坏 Skill 中涉及金额、版本号、参数占位的内容可靠性。

### 9. Remote Control：worktree 在会话归档前被删除
[#93345](https://github.com/anthropics/claude-code/issues/93345) ｜ OPEN ｜ 1 评论 ｜ 0 👍
会话子进程一退出即删除隔离 worktree，且 `activeSessionIds` 几乎从不持久化，导致 bridge 进程重启后会话无法恢复。对依赖 Remote Control 做长任务的用户而言，这是**数据丢失级别**的问题。

### 10. Remote Control 默认开启，用户无感知
[#88094](https://github.com/anthropics/claude-code/issues/88094) ｜ OPEN ｜ 10 评论 ｜ 10 👍
Windows 上 Remote Control 被默认打开。与 #92885（Cowork 执行模式应可见、应说明哪些数据离开本机）形成呼应，共同指向**远程执行能力的默认值设定与透明度不足**。

**其他值得一提：** [#94029](https://github.com/anthropics/claude-code/issues/94029) `claude attach` 无视 `CLAUDE_CODE_DISABLE_MOUSE*` 环境变量（回归）；[#91327](https://github.com/anthropics/claude-code/issues/91327) devcontainer 的 `init-firewall.sh` 在两条白名单域名解析到同一 IP 时因 `set -e` + ipset 重复而启动失败；[#94070](https://github.com/anthropics/claude-code/issues/94070) 在事件报告中输入 CVE 编号触发网络安全过滤器误报，导致会话中止。

---

## 四、重要 PR 进展

> 说明：过去 24 小时内仅有 **5 个 PR** 有更新，以下全部列出，未凑数。

1. [#93951](https://github.com/anthropics/claude-code/pull/93951) ｜ OPEN ｜ @poteat
   将 diff、sec-default、telemetry 三个 mod 的行为测试迁移到 `mods/<mod>/tests/` 下，由 `claude plugin test` 执行。**插件系统的测试归属与可移植性**进一步规范化，是插件生态走向成熟的基础设施动作。

2. [#93932](https://github.com/anthropics/claude-code/pull/93932) ｜ CLOSED ｜ @poteat
   修正 telemetry mod 在 `plugin.json` 中 `types` 路径未使用 `./` 相对前缀的问题（manifest schema 拒绝裸相对路径）。一行修复，**统一了 manifest 路径约定**。

3. [#89404](https://github.com/anthropics/claude-code/pull/89404) ｜ OPEN ｜ @bcherny
   修复 `validate-agent.sh` 在 `set -euo pipefail` 下因 `((warning_count++))` 返回非零而提前中止的问题，解决 plugin-dev 自身 agent 文件被误报。对应公共 Issue #83803，**直接改善插件开发者的本地校验体验**。

4. [#79148](https://github.com/anthropics/claude-code/pull/79148) ｜ OPEN ｜ @Codeturion
   为四个示例规则文件补上必需的 `hookify.` 前缀。由于加载器只识别 `.claude/hookify.*.local.md`，现有示例按文档复制后**静默失效**——这是一个典型的"文档正确、示例错误"陷阱。

5. [#41621](https://github.com/anthropics/claude-code/pull/41621) ｜ CLOSED ｜ @code-yeongyu
   补充 CLI 构建基础设施与打包配置，包含从 TypeScript 源码打包为单文件可执行程序的相关文档与 esbuild 配置。虽已关闭，但**构建链路的公开化**对社区二次开发与审计有参考价值。

---

## 五、功能需求趋势

从本期全部 Issue 的标签分布与内容看，社区关注方向可归纳为五条主线：

| 方向 | 代表 Issue | 诉求核心 |
|---|---|---|
| **IDE 集成广度与深度** | [#15942](https://github.com/anthropics/claude-code/issues/15942) VS 2026、[#24726](https://github.com/anthropics/claude-code/issues/24726) 禁用自动附加、[#34196](https://github.com/anthropics/claude-code/issues/34196) 聊天面板字号、[#94052](https://github.com/anthropics/claude-code/issues/94052) 上下文自动附加开关失效 | 不只求"支持"，更求**可配置**（字号、附加行为、开关持久化） |
| **多 Agent 编排与可观测性** | [#24537](https://github.com/anthropics/claude-code/issues/24537) Agent 层级面板、[#66402](https://github.com/anthropics/claude-code/issues/66402) per-agent 模型/effort | 需要**按 Agent 隔离配置** + **实时可视化** |
| **远程/协作执行的透明度** | [#92885](https://github.com/anthropics/claude-code/issues/92885) Cowork 本地/远程模式可见化、[#88094](https://github.com/anthropics/claude-code/issues/88094) Remote Control 默认开启、[#93345](https://github.com/anthropics/claude-code/issues/93345) worktree 生命周期 | 用户希望明确知道**什么数据离开了本机**、会话何时被清理 |
| **沙箱与 Devcontainer 可靠性** | [#91327](https://github.com/anthropics/claude-code/issues/91327)、[#93442](https://github.com/anthropics/claude-code/issues/93442) | 首次启动即失败的环境问题对 CI/团队落地杀伤力最大 |
| **Skill / 插件生态契约** | [#94065](https://github.com/anthropics/claude-code/issues/94065) 变量被替换、[#94067](https://github.com/anthropics/claude-code/issues/94067) executor hand-off 命名、[#89291](https://github.com/anthropics/claude-code/issues/89291) plan 文件命名模板 | 需要**稳定、可预测的文件与变量约定** |

此外，**平台质量分布**值得注意：Windows 相关 Issue 在本期占比显著（#42776、#66402、#88094、#93442、#94052、#94065），已超过 macOS 与 Linux，Windows 正在成为问题密度最高的平台。

---

## 六、开发者关注点

1. **进程与生命周期管理是最大痛点。** 孤儿进程锁文件（#42776）、会话退出即删 worktree 且状态不持久化（#93345）、headless 模式启动挂起（#75613）——三者本质相同：**Claude Code 的后台进程与会话状态缺乏可恢复、可观测的生命周期契约**。

2. **全局副作用与用户预期冲突。** `/model`、`/effort` 直接写全局 `settings.json`（#66402），界面开关不持久化（#94052），自动附加无法关闭（#24726）。开发者反复表达同一个诉求：**"我改的东西应该只影响我想要的范围，并且应该被记住。"**

3. **文档与实现脱节带来隐性成本。** 定时任务文档承诺的选择器不存在（#91884）、hookify 示例缺少必需前缀（#79148）、validate-agent.sh 误报（#89404）。这类问题修复成本低，但对新用户的劝退效应极强。

4. **平台特有质量问题集中在 Windows。** Cowork 的 Plan9 drive share 故障需重启系统仍不恢复（#93442），加上长期悬置的 #42776，说明 Windows 路径尚未达到与其他平台同等的稳定性水位。

5. **安全过滤误报开始阻碍合法工作。** #94070 中，安全研究员在事件报告表单填写 CVE 编号即触发 `cyber` 类别误判，会话被中止（severity: session-halted）。**误报的代价是"合法安全工作者被挡在门外"**，这类反馈值得产品侧优先评估。

6. **更新提示的误报噪音。** Homebrew cask（#86231）与 apt（#87197）安装场景下反复出现"Update available!"，虽已标记 stale，但反映出**多分发渠道版本对齐**仍不完善，属于低严重度高频骚扰型问题。

---

*本期统计：过去 24 小时无 Release，50 个 Issue 有更新（展示评论数 Top 30），5 个 PR 有更新。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 · 2026-09-14

---

## 1. 今日速览

过去 24 小时 Codex 仓库无新版本发布，社区讨论热度几乎全部集中在 Windows 平台。Issue 热榜前 30 条中带 `windows-os` 标签的占了 17 条，其中 #41463（Windows + WSL 无法创建项目）以 54 条评论、33 个赞稳居榜首。PR 侧则由 `copyberry[bot]`

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

⚠️ 摘要生成失败。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-09-14）

> 数据范围：github.com/github/copilot-cli 过去 24 小时更新内容
> 说明：本日社区活跃度较低，过去 24 小时**新增/更新 Issue 仅 4 条、PR 仅 2 条**，因此「社区热点 Issue」「重要 PR」两节按实际数据全量列出，不做凑数。

---

## 1. 今日速览

今日无新版本发布，社区焦点集中在 **Copilot CLI v1.0.83 的稳定性与 Agent 运行时问题**：一是工作区 `.mcp.json` 配置完全未被加载（MCP 集成回归），二是语音模式在 Linux 上触发 ONNX Runtime 断言崩溃；同时子智能体（Subagent）长工具调用链导致 prompt 缓存失效、token 消耗成倍放大的成本问题持续被讨论。PR 侧仅有两条 Dependabot 发起的 GitHub Actions 版本升级，均已关闭合并，无功能性变更。

---

## 2. 版本发布

过去 24 小时无新 Release。

当前社区反馈所指向的版本为 **v1.0.83**，本日多条 Bug 均在该版本复现，建议该版本用户关注下述 MCP 与语音相关问题。

---

## 3. 社区热点 Issues（本日全部 4 条）

**1. [#4832](https://github.com/github/copilot-cli/issues/4832) [triage] Workspace `.mcp.json` 从未被加载，`mcp list` 无 Workspace 分组**
- 作者 @ryan-knopp-elanco｜2026-09-13 创建｜评论 0｜👍 0
- **为何重要**：这不是显示层问题，而是功能性失效——仓库根目录的 `.mcp.json` 被完全忽略，MCP Server 从未启动，会话日志中也没有任何相关记录，`copilot mcp list` 只输出 `User servers:`。对依赖工作区级 MCP 配置做团队协作/项目隔离的用户来说，这是阻断性回归。
- **社区反应**：刚提交、尚无评论，但属于典型的「新版本回归」型高优先级 Bug，预计会快速获得 triage 关注。

**2. [#4833](https://github.com/github/copilot-cli/issues/4833) [triage] 语音模式在 Linux 上因 Nemotron ASR 的 ONNX Runtime 断言崩溃**
- 作者 @r-o-x｜2026-09-13 创建｜评论 0｜👍 0
- **为何重要**：启用语音输入后 CLI 以 `SIGABRT` 中止并 core dump（Linux x64 / Manjaro），崩溃发生在本机 Nemotron 语音模型处理音频阶段。属于进程级崩溃，非优雅降级；也反映出本地推理（ONNX）在非主流 Linux 发行版上的兼容性风险。
- **社区反应**：新提交，暂无讨论；Linux 桌面用户可重点关注。

**3. [#4829](https://github.com/github/copilot-cli/issues/4829) [triage] Subagent 在单轮内执行超长工具调用序列，导致 prompt 缓存失效与 token 消耗成倍增长**
- 作者 @gcapnias｜2026-09-12 创建｜2026-09-13 更新｜评论 1｜👍 0
- **为何重要**：直击 Agent 架构的成本核心。通过 `task` 工具运行自定义子智能体时，单轮内允许数百次工具调用，缓存前缀被反复击穿，token 用量呈复合式增长（v1.0.83 / Windows 11 / Gemini 3.8 Flash）。这是「能力越强、账单越贵」的典型矛盾，对重度编排用户影响直接。
- **社区反应**：已有 1 条评论参与讨论，是本日互动度最高的 Issue。

**4. [#2254](https://github.com/github/copilot-cli/issues/2254) [area:agents] 为后台子智能体增加实时进度流式输出**
- 作者 @Ghislain89｜2026-03-24 创建｜2026-09-13 更新｜评论 1｜👍 0
- **为何重要**：长期未闭环的功能请求（已挂起近半年）。当前 `/tasks` 在运行多阶段编排智能体（plan → implement → deliver → review）时仅展示工具调用计数，缺乏细粒度可观测性，用户无法判断子智能体究竟在做什么、是否卡死。
- **社区反应**：本日仍有更新，说明需求持续存在；与 #4829 同属「Agent 运行时」议题簇，二者叠加形成对 Agent 可观测性与成本控制的双重诉求。

---

## 4. 重要 PR 进展（本日全部 2 条）

**1. [#4827](https://github.com/github/copilot-cli/pull/4827) [CLOSED] build(deps): bump actions/stale from 9.1.0 to 11.0.0**
- 作者 @dependabot[bot]｜2026-09-12 创建｜2026-09-13 更新
- 内容：将 stale 机器人 Action 从 9.1.0 升级至 11.0.0（含多个破坏性变更与增强）。影响仓库层面的 Issue/PR 自动清理策略，对终端用户无直接感知。

**2. [#4828](https://github.com/github/copilot-cli/pull/4828) [CLOSED] build(deps): bump actions/github-script from 7.1.0 to 9.0.0**
- 作者 @dependabot[bot]｜2026-09-12 创建｜2026-09-13 更新
- 内容：`actions/github-script` 从 7.1.0 跨两个大版本升级至 9.0.0，主要用于仓库自动化脚本。同样属于 CI 基础设施维护。

> 小结：本日 PR 通道无任何功能开发或缺陷修复合并，全部为依赖维护，说明核心团队当日未通过公开 PR 推进面向用户的改动。

---

## 5. 功能需求趋势

从本期全部 Issue 中可提炼出四个方向：

1. **Agent 运行时可观测性（最突出）**：后台子智能体的进度流式输出（#2254）与长工具链的行为透明度（#4829）指向同一诉求——多阶段编排已成为主流用法，但用户对「Agent 正在做什么」几乎无感知。
2. **Token 成本与缓存效率**：prompt caching 失效导致的复合型 token 增长，正在成为 Agent 能力扩张后的隐性成本瓶颈，预计会催生对缓存策略、上下文压缩与会话切分机制的需求。
3. **MCP 生态集成质量**：工作区级 `.mcp.json` 的加载回归说明 MCP 已成为核心使用路径，配置发现、层级优先级与 `mcp list` 的可诊断性需要更稳固的保障。
4. **多模态/本地推理的跨平台稳定性**：语音模式依赖本地 Nemotron ASR + ONNX Runtime，在 Linux 桌面环境出现硬崩溃，跨发行版兼容性与失败降级策略是后续关注点。

---

## 6. 开发者关注点（痛点与高频诉求）

- **成本不可控**：子智能体长时间自主运行带来的 token 消耗缺乏上限与预警机制，开发者需要预算护栏与更聪明的缓存复用。
- **可观测性缺口**：仅凭工具调用计数无法判断编排流程健康度，开发者要求实时进度、阶段状态与更细粒度的日志输出。
- **配置回归的信任成本**：`.mcp.json` 静默失效（无报错、无日志）比直接报错更危险，开发者期望配置加载失败时能被显式告知。
- **稳定性与平台覆盖**：Linux（尤其非 Ubuntu 发行版）上的原生崩溃、以及 Windows/PowerShell 环境下的性能问题，显示跨平台测试矩阵仍需补强。
- **版本集中度**：本日 3 条 Issue 明确指向 v1.0.83，建议该版本用户留意 MCP 与语音功能，必要时回退或等待修复版本。

---

*注：本日报基于过去 24 小时公开数据生成；Issue/PR 数量不足 10 条时按实际全量呈现，未做推测性补充。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-09-14** ｜ 数据来源：[github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

---

## ⚠️ 数据说明

今日数据量极小：过去 24 小时内**无新版本发布**、**无 Issue 更新（0 条）**、**仅 1 个 PR 更新**。

因此，日报中「10 个热点 Issue」「10 个重要 PR」的常规编排无法成立——为避免虚构内容，相关部分据实压缩呈现，并以该唯一 PR 为样本做有限度的趋势解读。

---

## 1. 今日速览

今日仓库处于低活跃状态，唯一的社区动态是一份关于 **OpenAI 兼容 Provider 配置文档的澄清 PR（#2641）**。该 PR 聚焦于一个高频困惑点：自定义 OpenAI 兼容服务需要「API 根地址 + 服务方接受的模型 ID」，且环境变量会覆盖配置文件中的同名字段。除此之外，无新版本、无 Issue 变动，项目整体节奏平稳。

---

## 2. 版本发布

无新版本发布。

---

## 3. 社区热点 Issues

**过去 24 小时内无 Issue 更新（共 0 条）。**

- 无可供筛选的议题，本期不列条目。
- 若该状态持续，建议关注仓库 Issues 列表是否有积压：[查看全部 Issues](https://github.com/MoonshotAI/kimi-cli/issues)

---

## 4. 重要 PR 进展

过去 24 小时内共 1 个 PR 更新，即全部动态：

### 📄 #2641 [OPEN] docs(providers): clarify OpenAI-compatible configuration
- **作者**：@QIU-Guanzong
- **创建 / 更新**：2026-09-13
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2641
- **状态**：OPEN，👍 0

**内容摘要（据提供的 PR 描述）：**

1. **明确自定义 OpenAI 兼容 Provider 的配置要求** —— 需要提供 API 根地址（base URL）以及**服务端实际接受的模型 ID**，而非想当然的模型别名。
2. **补充环境变量覆盖规则** —— 非空的 `OPENAI_BASE_URL` 与 `OPENAI_API_KEY` 会**覆盖** provider 配置中的对应字段，且该行为同时作用于 `openai_legacy` 与 `openai_responses` 两种模式。
3. **中英文文档同步维护** —— 保持英文与中文文档一致（原文摘要在该处被截断）。

**为什么值得关注：**

- 这是**纯文档改动但指向真实痛点**：接入第三方 OpenAI 兼容服务（如各类自建网关、兼容层、海外/国产模型供应商）时，「base URL 该填到哪一层」「模型 ID 谁说了算」「配置文件为何被环境变量劫持」是典型的三连坑。
- 涉及 `openai_legacy` 与 `openai_responses` 两条路径的**优先级语义**说明，对排查「配置写了但没生效」类问题有直接帮助。
- 属于典型的**低成本、高收益**贡献：不需要改动运行时逻辑，即可减少后续重复提问与误报 Issue。

**观察建议：** 该 PR 尚无评论与点赞，建议维护者优先确认文档描述是否与实际代码中的覆盖优先级完全一致——文档一旦与实现产生偏差，反而会制造新的排障成本。

---

## 5. 功能需求趋势

**本期数据不足以提炼趋势。** 由于过去 24 小时内 Issues 更新为 0，无法从社区诉求中归纳功能方向。

仅从唯一 PR 的选题可以得出一个**弱信号**：

- **多 Provider / OpenAI 兼容接入的配置体验**仍是社区实际使用中的摩擦点，且矛盾集中在「文档表述」而非「功能缺失」层面——这通常意味着核心能力已具备，问题在于可发现性与可理解性。

后续若出现更多同类议题，可将其归入 **Provider 配置与互操作性** 这一方向持续跟踪。

---

## 6. 开发者关注点

基于现有 1 条 PR 数据，可总结的开发者关注点如下（均为**有限推断**，非高频统计结论）：

| 关注点 | 具体表现 | 关联 |
|---|---|---|
| 配置语义不清 | 自定义 OpenAI 兼容服务的 base URL 层级、模型 ID 来源不明确 | PR #2641 |
| 配置优先级困惑 | 环境变量与配置文件冲突时谁生效，需明确覆盖规则 | PR #2641 |
| 双协议路径差异 | `openai_legacy` 与 `openai_responses` 行为是否一致 | PR #2641 |
| 中英文文档一致性 | 文档需双语同步，避免非英语用户获取信息滞后 | PR #2641 |

**总体判断：** 今日无阻塞性 Bug、无破坏性变更、无版本迭代，属于典型的「静默维护日」。社区在这段时间的需求集中在**降低接入门槛与排障成本**上，而非推动新功能。

---

*本日报基于 GitHub 公开数据自动整理，仅覆盖指定时间窗口内的更新；Issue 更新数为 0 时段落长度受限属正常情况。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 · 2026-09-14

## 今日速览

今日社区焦点集中在 **V2 新界面强制迁移引发的强烈反弹**——旧布局被彻底移除，但新布局尚不支持多工作树、MCP 面板缺失等问题集中爆发。同时 **1.18.30 版本的全局 TypeError 回归**导致大量用户 prompt 直接失败，成为最高优先级的技术问题。此外，Zen/Muse Spark 模型的 `encrypted_content` 报错持续发酵。

---

## 版本发布

过去 24 小时内无新版本发布。

---

## 社区热点 Issues

**1. [#4283 Copy To Clipboard is not working](https://github.com/anomalyco/opencode/issues/4283)**
评论 133、👍 124，是当前社区最长寿且热度最高的 Issue。用户选中响应文本后无法复制，从 v1.0.62 一直延续至今未解决。与 #48839（v2 Web 代码块复制按钮失效）叠加，说明剪贴板功能在多个平台/布局上系统性失效。

**2. [#23153 [FEATURE] Pay Go with crypto](https://github.com/anomalyco/opencode/issues/23153)**
评论 22、👍 51，社区对 OpenCode Go 加密支付需求强烈。反映部分用户受地域支付渠道限制，加密支付已成商业化的高频诉求。

**3. [#48741 [2.0] Opencode Zen critical errors on Muse Spark family](https://github.com/anomalyco/opencode/issues/48741)**
评论 21。Muse Spark 系列在收到图片或执行工具调用时抛出 `reasoning encrypted_content was not issued to this caller`，影响 Zen 上的所有 Muse Spark 模型。与 #48805（同 session 切换模型触发同类错误）构成同一个 provider 层缺陷。

**4. [#43277 Sessions permanently stuck during normal use](https://github.com/anomalyco/opencode/issues/43277)**
评论 14。会话进入"卡死"状态后重启服务、重启系统均无法恢复，属于持久化/状态机层面的严重问题，影响日常使用信心。

**5. [#48645 Regression in 1.18.30: every prompt crashes with TypeError](https://github.com/anomalyco/opencode/issues/48645) / [#48803 v1.18.30: every prompt fails with TypeError](https://github.com/anomalyco/opencode/issues/48803)**
两个独立用户分别报告 v1.18.30 每次 prompt 都失败于 `SystemPrompt.environment` 的 TypeError，回退到 1.18.18 / 1.18.20 即恢复。属于高优先级回归，且二者交叉印证。

**6. [#48837 [UI feedback] Forced V2 interface destroys productivity](https://github.com/anomalyco/opencode/issues/48837)**
评论 2、👍 2。多项目/多代理（20+ session）用户反馈 V2 界面严重降低生产力，与 #39835、#48835 形成对"强制新布局"的集中抗议。

**7. [#48835 旧布局被强制移除，但新布局又不支持多工作树](https://github.com/anomalyco/opencode/issues/48835)**
评论 2、👍 3。9 月 14 日午夜 OpenCode Desktop 突然切换到新布局，设置中"旧版界面已无法使用"，但新布局无法管理多个 worktree，属于功能性倒退。

**8. [#36423 [2.0] subagent: no cancellation support for background subagents](https://github.com/anomalyco/opencode/issues/36423)**
评论 5、👍 4。v2 后台 subagent 返回 `ses_...` 会话 ID 并可恢复，但无法取消运行中的子代理，是 v2 代理编排能力的关键缺口。

**9. [#34442 Windows Desktop installer is broken offline](https://github.com/anomalyco/opencode/issues/34442)**
评论 3、👍 4。离线安装的 Windows Desktop 因未内置 ripgrep，导致 `grep`/`glob`/`skill` 及内置技能全部不可用。对企业内网/离线环境是阻断性问题。

**10. [#46426 MCP toggle is missing in New UI](https://github.com/anomalyco/opencode/issues/46426) / [#48859 (俄语) 新布局中 MCP 开关缺失](https://github.com/anomalyco/opencode/issues/48859)**
新布局缺失 MCP 启用/禁用开关，只能退回旧布局操作。与"强制迁移 V2"叠加，进一步放大用户不满。

> 其他值得留意：#48850（Desktop 随机将运行中 turn 标记为 interrupted）、#48848（git 快照跨进程竞争 + 陈旧 index.lock 永久卡死）、#48868（PDF 工具结果回放触发 422 校验错误）、#48869（AppImage 不显示在应用菜单）。

---

## 重要 PR 进展

**1. [#48877 fix(core): break filesystem/search import cycle](https://github.com/anomalyco/opencode/pull/48877)**
修复 `filesystem.ts` 与 `filesystem/search.ts` 互相 import 并在求值期解引用导致的循环依赖，关闭 #48876。

**2. [#48878 fix(tui): force terminal reset on exit for Windows ConPTY](https://github.com/anomalyco/opencode/pull/48878)**
针对 Windows ConPTY（Alacritty + zellij）退出后终端进入 raw/损坏状态的问题，强制终端重置，关闭 #48776。

**3. [#48871 fix(project): resolve an associated directory to its project instead of global](https://github.com/anomalyco/opencode/pull/48871)**
修复非 git 目录一律被 `Project.resolve` 判为 `ID.global` 的问题，使 `project_directory` 表真正参与解析，关闭 #48870。

**4. [#44264 feat(session): add suffix compaction](https://github.com/anomalyco/opencode/pull/44264)**
新增实验性 `compaction.mode: "suffix"`，为会话上下文压缩提供更优策略，作者标注由 AI 辅助生成。

**5. [#44535 fix(session): stop creating phantom "unknown" tool parts on re-emitted deltas](https://github.com/anomalyco/opencode/pull/44535)**
修复重复增量下发时凭空生成 `unknown` 工具调用（#33618），澄清该幻影调用由 opencode 而非模型产生。

**6. [#48867 [contributor] feat(core): make worktree APIs project-based](https://github.com/anomalyco/opencode/pull/48867)**
将四个 worktree 操作全部改为基于 `projectID`，不再依赖调用方指定路径。这是回应"多工作树支持缺失"的核心基建，值得持续跟踪。

**7. [#45207 fix(tui): show readable Effect errors](https://github.com/anomalyco/opencode/pull/45207)**
Effect `Cause` 不再走通用 `JSON.stringify`，避免向用户暴露内部结构，关闭 #34925。

**8. [#42340 fix(cli): stop `run` from sleeping through an exhausted quota](https://github.com/anomalyco/opencode/pull/42340)**
修复 `opencode run` 在配额耗尽时无输出且永不返回（实际是休眠而非卡死），关闭 #40747。

**9. [#42326 fix(opencode): accumulate step tokens instead of overwriting](https://github.com/anomalyco/opencode/pull/42326)**
多步工具调用中 `processor.ts` 每次 `step-finish` 覆盖 `assistantMessage.tokens`，修复后仅统计最后一步的问题，关闭 #42324。

**10. [#42372 (已关闭) feat(app): show tokens-per-second in context usage indicator](https://github.com/anomalyco/opencode/pull/42372)**
在上下文使用指示器（进度圆环）中展示 tokens/s 速率，改善用户对模型性能的可见性。

> 另有 #47913（印尼语 README）、#42323（意大利语 references 文档）、#42365（Go 平台 Grok 4.5 改用 Responses API）、#42355（配置中缺失 `{file:...}` 变量不再阻断启动）等文档与兼容性修复一并合入/推进。

---

## 功能需求趋势

从今日 50 条 Issue 中可提炼出以下方向：

| 方向 | 代表 Issue | 说明 |
|---|---|---|
| **UI/布局迭代阵痛** | #48837 #48835 #39835 #46426 #48859 | 旧布局被强制下线，新布局缺少多 worktree、MCP 开关等能力，成为最大争议点 |
| **多工作树 / Monorepo 支持** | #36605 #48835 #48867 | v2 monorepo 跨目录 subagent、worktree 项目管理需求集中 |
| **代理编排可控性** | #36423 #47458 | 后台子代理取消、插件工具附件与取消信号传递 |
| **Provider / 模型兼容** | #22212 #42365 #48741 #48805 #48868 | LiteLLM 统一端点、Grok 4.5、Muse Spark 的 encrypted_content 与 PDF 回放问题 |
| **平台可靠性（Windows/离线）** | #34442 #48762 #48850 #48878 | ripgrep 未打包、非 git 路径、随机中断、ConPTY 终端损坏 |
| **商业化与支付** | #23153 | OpenCode Go 加密支付 |
| **剪贴板与复制** | #4283 #48839 | 跨平台跨布局的复制失效，长期未解决 |

---

## 开发者关注点

1. **回归问题处理速度**：1.18.30 的 `SystemPrompt.environment` TypeError 让所有 prompt 不可用（#48645、#48803），开发者希望获得更快的回滚/热修复通道。
2. **状态一致性与可恢复性**：会话永久卡死（#43277）、git 快照竞争与陈旧 `index.lock`（#48848）、

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*