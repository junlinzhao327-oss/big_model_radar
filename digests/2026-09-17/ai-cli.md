# AI CLI 工具社区动态日报 2026-09-17

> 生成时间: 2026-09-16 22:35 UTC | 覆盖工具: 7 个

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

# AI CLI 工具社区动态横向对比分析报告  
**日期：2026-09-17**  
**数据口径说明**：各日报统计口径不同，有的为“过去 24 小时更新 Issue 总数”，有的为“热点 Issue/PR 列表”。下表尽量还原原文数据，未披露项标注为“未披露/无数据”，因此横向比较需谨慎。

---

## 1. 生态全景

当前 AI CLI 工具已从“单轮代码补全/问答”进入**多代理编排、MCP 集成、上下文治理与企业级权限**的深水区。社区最强烈的痛点不再是“能不能写代码”，而是**子代理是否可靠、配额是否可控、配置是否真的生效、会话是否能接入 CI/CD**。同时，多个工具出现“高频发版但缺少说明”“stale/自动化关闭压过真实需求”“强制 UI 迁移引发反弹”等治理型问题。整体看，生态竞争焦点正在从模型能力转向**工程可靠性、成本透明度和可编程性**。

---

## 2. 各工具活跃度对比

| 工具 | Issues 动态 | PR 动态 | Release 情况 | 活跃度判断 |
|---|---|---|---|---|
| **Claude Code** | 过去 24h 更新 30 条热门 Issue，28 条带 `stale` 被关闭；唯一高热 OPEN：#26073 Windows MSIX MCP 配置错误 | 3 条更新，全部围绕 `mods/diff`；1 OPEN / 2 CLOSED | 无新 Release | 存量清理型，新增代码少，社区历史需求被 stale 吞没 |
| **OpenAI Codex** | 热点 Issue 至少列示 6 条；#41220 配额异常 45 评论，#44781 消息队列 41 评论/50 👍 | 批量关闭 PR，由 `copyberry[bot]` 集中推进，覆盖 rollout 压缩、MCP 只读、Windows 沙箱、无障碍；具体数量未披露 | 8 个标签，含 `rusty-v8-v152.2.0` 与多个 `rust-v0.155.0-alpha.*`；均无 Release Notes | 高频 alpha 发版，Issue 热度高，但透明度和说明不足 |
| **Gemini CLI** | 过去 24h 更新约 50 条 Issue；热点 Top10 中多个 P1，子代理/Shell 执行问题突出 | 29 条更新，安全与正确性修复密集 | 1 个 nightly：`v0.62.0-nightly.20260916.g6a466a7e2` | 高活跃，修复密集，多代理可靠性是主战场 |
| **GitHub Copilot CLI** | 本期约 50 条 Issue；热点 10 条，MCP/OAuth/Worktrees/中文输入法受关注 | 0 条 PR 更新 | 发布 `v1.0.86-1`、`v1.0.86-0`；前日 `v1.0.85` 引入 Vim 模式 | Release 驱动，Issue 量大，PR 通道当日停滞 |
| **Kimi Code CLI** | 1 条 Issue：#2647 配额耗尽后主/子 agent 失控重试 14h+ | 1 条 PR：#2648 增加 `PreToolUse` HOL Guard 示例 | 无新 Release | 低活跃，早期项目，但问题严重性高 |
| **OpenCode** | 热点 10 条 + 其他；UI 迁移、Provider tools 失败、Agent 循环不终止 | 20 条 PR 全部 CLOSED，统一 `automated-pr-cleanup`，创建于 2026-08-16 | 无新 Release | 社区情绪高，代码合入停滞；历史 PR 被批量清理 |
| **Qwen Code** | 摘要未提供 | 摘要未提供 | 摘要未提供 | 无数据，无法评估 |

---

## 3. 共同关注的功能方向

| 功能方向 | 涉及工具 | 具体诉求 |
|---|---|---|
| **多代理/子代理编排可靠性** | Claude Code、Codex、Gemini CLI、Copilot CLI、Kimi CLI、OpenCode | 子代理终止语义、失败可见性、父子会话

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---

# Claude Code 社区动态日报 · 2026-09-17

数据来源：github.com/anthropics/claude-code

---

## 1. 今日速览

今日无新版本发布，社区动态以 **Issue 存量清理**为主：过去 24 小时更新的 30 条热门 Issue 中有 28 条带 `stale` 标签被自动关闭，绝大多数是 7 月底集中提交的 UI／体验类功能请求。唯一保持高热的是 **#26073 Windows MSIX 版 MCP 配置读取错误**（23 条评论、33 👍），仍是当前最受关注的未解决 Bug。PR 侧仅 3 条更新，且全部集中在 `mods/diff` 差异面板的打开时机与类型安全上。

---

## 2. 版本发布

过去 24 小时无新 Release（含预发布）。

---

## 3. 社区热点 Issues

> 说明：今日 Issue 流几乎被 stale 自动关闭占据。以下按"仍在讨论的价值"而非"是否仍 OPEN"排序，并标注状态。

| # | 状态 | 标题要点 | 为什么值得关注 | 社区反应 |
|---|---|---|---|---|
| 1 | **OPEN** | [#26073](https://github.com/anthropics/claude-code/issues/26073) Windows MSIX：「Edit Config」打开了错误的 `claude_desktop_config.json`，MCP Server 静默加载失败 | 当前**唯一高热未解决 Bug**。MSIX 打包应用的配置文件重定向导致用户编辑了无效路径，且失败无任何报错，属"静默失效"类最危险的问题 | 23 评论 / 33 👍，跨 7 个月仍在更新 |
| 2 | **OPEN** | [#89783](https://github.com/anthropics/claude-code/issues/89783) 支持程序化创建多个命名子会话并自动启动（免手动点击） | 直指 subagent 编排的关键缺口：批量化 fan-out 目前必须人工点击 chip，无法脚本化 | 3 评论 / 2 👍，新提交且已被维护者关注 |
| 3 | CLOSED | [#81946](https://github.com/anthropics/claude-code/issues/81946) session transcript／memory 应可随项目移植，scratch 文件保持本地 | 触及 `~/.claude/projects/<sanitized-path>` 按绝对路径索引的架构问题，影响多机协作与项目迁移 | 4 评论，为本批关闭项中讨论最多的一条 |
| 4 | CLOSED | [#82203](https://github.com/anthropics/claude-code/issues/82203) Threads：可导航的会话内子对话（fork + 多 agent UI + 合并回主流） | 与 #89783 同源需求——社区希望会话具备**分叉与合并**能力，而非线性历史 | 2 评论 |
| 5 | CLOSED | [#82114](https://github.com/anthropics/claude-code/issues/82114) 按模型设置默认 effort level | 当前 `effortLevel` 为全局单值，但 `/model` 可自由切换，导致"大模型省钱、小模型拉满"的组合无法持久化 | 1 评论 / 1 👍 |
| 6 | CLOSED | [#82581](https://github.com/anthropics/claude-code/issues/82581) Session pinning 在 CLI 中完全不可见，应暴露到 `agents --json` 与 `--help` | GUI（`Ctrl+T`／桌面端）已有能力，CLI 却无法发现、查询或非交互式设置，属典型的**能力不对等** | 1 评论 / 1 👍 |
| 7 | CLOSED | [#81943](https://github.com/anthropics/claude-code/issues/81943) 提供不写入上下文的 Bash 模式（如 `!!`） | `!` 前缀会无条件把命令与输出灌入上下文，`pwd`／`ls`／`git status` 这类高频命令持续污染窗口 | 1 评论，需求描述具体、可落地性强 |
| 8 | CLOSED | [#81892](https://github.com/anthropics/claude-code/issues/81892) 将 Project Instructions 视为一个"始终激活的 Skill" | 统一 instructions 与 skills 两套机制，可能简化上下文加载与优先级模型 | 1 评论 / 3 👍（关闭项中点赞较高） |
| 9 | CLOSED | [#82095](https://github.com/anthropics/claude-code/issues/82095) 可信设备支持同时注册多个 FIDO2 认证器（当前仅单注册、替换式） | 企业安全场景刚需：单认证器丢失即需走找回流程；作者指出 7 月时支持文档中尚无 passkey 条目 | 3 评论 / 5 👍 |
| 10 | CLOSED | [#81897](https://github.com/anthropics/claude-code/issues/81897) 流式输出时实时显示 tokens-per-second | 用户无法区分"模型慢／网络慢／被限流"，也无法横向比较模型速度；上一轮同类请求 #58248 曾被 stale 关闭 | 1 评论 |

**其他值得留意**：[#81901](https://github.com/anthropics/claude-code/issues/81901) AskUserQuestion 工具 pageSize 可配置、[#81959](https://github.com/anthropics/claude-code/issues/81958) 桌面端退出入口可发现性、[#81877](https://github.com/anthropics/claude-code/issues/81877) SendUserFile 的 Office 文件内联预览、[#82033](https://github.com/anthropics/claude-code/issues/82033) 无障碍 answer-first 输出风格、[#82146](https://github.com/anthropics/claude-code/issues/82146) 为消息边界与 Stop-hook 结果发出语义标记。

---

## 4. 重要 PR 进展

过去 24 小时仅 **3 条 PR** 更新，全部围绕 `mods/diff` 差异面板，主题高度一致：**修正面板打开条件与类型契约**。

1. **[#94847 [OPEN]](https://github.com/anthropics/claude-code/pull/94847)** — `diff: the first edit opens the pane only when it has a file to list`
   修复 diff 面板在会话首次成功 Edit／Write／NotebookEdit 时**无条件抢先打开**的问题：此前即便写入仓库外文件、被 ignore 的文件，或写入了与会话不同的 worktree，也会先开面板再拉取，结果呈现空面板「No tracked changes」。改为先确认有可列出的文件再打开。**本批唯一仍处于 OPEN 状态的 PR。**

2. **[#94843 [CLOSED]](https://github.com/anthropics/claude-code/pull/94843)** — `diff: the prompt hint reads the viewport's layout through a type that may lack it`
   类型安全修复。`mods/diff` 的 prompt hint hook 读取 `viewport.isFullscreen`，但部分引擎的 `RenderViewport` 尚未声明该字段，导致类型检查失败——尽管运行时行为本就正确。改为通过可选读取方式访问，消除编译期假阳性。

3. **[#94653 [CLOSED]](https://github.com/anthropics/claude-code/pull/94653)** — `diff: the first edit opens the pane only where the layout docks it`
   收敛上一条的触发条件：此前只要终端宽度 ≥144 列就自动开面板，未考虑布局是否能停靠。在主屏模式（`CLAUDE_CODE_NO_FLICKER=0`）下并无停靠区，面板会以内置对话框形态内联挤在 prompt 上方，宽终端下体验尤其突兀。

> 注：今日 PR 数量不足以支撑 10 条清单，以上为全部 3 条；三条实为同一处逻辑的连续迭代（#94653 → #94843 → #94847）。

---

## 5. 功能需求趋势

从本批 Issue（含被关闭项）可提炼出五条主线：

1. **Agent／会话编排（最集中）**
   [#89783](https://github.com/anthropics/claude-code/issues/89783) 程序化命名子会话、[#82203](https://github.com/anthropics/claude-code/issues/82203) Threads 分叉合并、[#82066](https://github.com/anthropics/claude-code/issues/82066) workflow 逻辑失败标记、[#81963](https://github.com/anthropics/claude-code/issues/81963) VSCode 中标注子 agent 工具调用、[#81928](https://github.com/anthropics/claude-code/issues/81928) 将 routine 运行结果移入 sessions 列表。社区已把 Claude Code 当作**多 agent 调度平台**使用，现有 UI 与 CLI 原语明显不足。

2. **上下文与内存治理**
   [#81943](https://github.com/anthropics/claude-code/issues/81943) 不污染上下文的 Bash 模式、[#81946](https://github.com/anthropics/claude-code/issues/81946) transcript 项目可移植、[#82146](https://github.com/anthropics/claude-code/issues/82146) 折叠被取代草稿、[#81892](https://github.com/anthropics/claude-code/issues/81892) instructions-as-skill。核心诉求是把"什么进入上下文、存放于何处"变成可控项。

3. **TUI／桌面端可定制性**
   [#81883](https://github.com/anthropics/claude-code/issues/81883) 内边距与密度、[#81889](https://github.com/anthropics/claude-code/issues/81889) 隐藏 diff／内容预览、[#81856](https://github.com/anthropics/claude-code/issues/81856) 退出组织级自定义 spinner 文案、[#81897](https://github.com/anthropics/claude-code/issues/81897) TPS 显示、[#82065](https://github.com/anthropics/claude-code/issues/82065) 关闭 prompt 建议、[#82128](https://github.com/anthropics/claude-code/issues/82128) 过滤。信号明确：**默认信息密度偏高，且缺少关闭开关**。

4. **CLI 与 GUI 能力对齐**
   [#82581](https://github.com/anthropics/claude-code/issues/82581) pinning 不可见于 CLI、[#82103](https://github.com/anthropics/claude-code/issues/82103) 将 `/btw` 侧聊带到 Chat／Cowork、[#81837](https://github.com/anthropics/claude-code/issues/81837) Windows 搜索键映射。终端优先用户要求获得与图形端对等的可发现性和可脚本化能力。

5. **模型与配置粒度**
   [#82114](https://github.com/anthropics/claude-code/issues/82114) per-model effort level、[#82207](https://github.com/anthropics/claude-code/issues/82207) 云环境配置增加 instructions 字段、[#81871](https://github.com/anthropics/claude-code/issues/81871) 计费／许可信息应答一致性。

此外，**IDE 集成**（[#81895](https://github.com/anthropics/claude-code/issues/81895) 多文件多行选择高亮，作者明确对比 Cursor 与 Codex 扩展）与**无障碍**（[#82033](https://github.com/anthropics/claude-code/issues/82033) answer-first 完整句输出）虽条目较少，但属长期未被满足的细分诉求。

---

## 6. 开发者关注点

- **静默失败比报错更危险**：#26073 是本日最高热度问题，配置被写到错误路径 + MCP 静默加载失败 + 无提示，三重叠加。用户对"看得见的失败"容忍度远高于"看起来正常但其实没生效"。
- **上下文预算焦虑**：大量请求围绕"别把东西塞进上下文"（[#81943](https://github.com/anthropics/claude-code/issues/81943)、[#82146](https://github.com/anthropics/claude-code/issues/82146)、[#81889](https://github.com/anthropics/claude-code/issues/81889)）。开发者把 context window 视为稀缺资源，希望按命令／工具粒度精细控制。
- **stale 机器人正在吞掉有效需求**：本批 30 条中 28 条被 stale 关闭，其中多条（[#81897](https://github.com/anthropics/claude-code/issues/81897) 明确引用了上一轮同样因 stale 关闭的 #58248、[#81892](https://github.com/anthropics/claude-code/issues/81892) 获 3 👍）在关闭时已获一定认同。同一个需求被反复提交又被反复关闭，本身就是值得维护者关注的信号。
- **可编程性缺口阻碍自动化**：需要程序化创建子会话（[#89783](https://github.com/anthropics/claude-code/issues/89783)）、非交互式 pin 会话（[#82581](https://github.com/anthropics/claude-code/issues/82581)）、以逻辑结果而非运行时异常标记 agent 失败（[#82066](https://github.com/anthropics/claude-code/issues/82066)）。开发者要把 Claude Code 接入 CI／批处理流水线，但现有原语偏交互式设计。
- **企业安全与合规待补**：多 FIDO2 认证器（[#82095](https://github.com/anthropics/claude-code/issues/82095)）、组织级配置与个人偏好冲突时的退出机制（[#81856](https://github.com/anthropics/claude-code/issues/81856) 要求个人可退出组织定制的 spinner 文案），反映组织部署场景正在增加。

---

*本日报基于 GitHub 公开数据自动整理，Issue 状态与评论数会随时间变化

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-09-17）

---

## 一、今日速览

过去 24 小时，Codex 仓库进入 **0.155.0-alpha 密集迭代期**，一口气合并/发布了 8 个版本标签（含 rusty-v8 依赖升级），但几乎全部为无说明的滚动构建。社区侧最热话题仍集中在 **用量/配额核算不透明**（#41220 累计 45 条评论）和 **Codex Desktop 消息队列失效**（#44781 / #45019 / #45626 系列，合计点赞超 100）。批量关闭的 PR 由 `copyberry[bot]` 集中推进，覆盖 rollout 压缩、MCP 只读策略、Windows 沙箱修复与无障碍支持四个方向。

---

## 二、版本发布

过去 24 小时共 8 个标签，**均无实质性 Release Notes**：

| 标签 | 说明 |
|---|---|
| `rusty-v8-v152.2.0` | V8 运行时依赖版本升级 |
| `rust-v0.155.0-alpha.9` | 0.155.0 alpha 线 |
| `rust-v0.155.0-alpha.2.5` / `.2.6` | 0.155.0 alpha 线分支 |
| `rust-v0.155.0-alpha.10 / .11 / .12 / .13` | 0.155.0 alpha 线连续推进 |

**解读**：同一小版本内出现 alpha.10→.13 的连续发布，且与 alpha.2.5、alpha.9 并行存在，说明主干正在高频发版验证。`rusty-v8` 独立发版通常与 CLI 冷启动性能或沙箱内 JS 执行有关。由于官方未附 changelog，具体行为变化需自行 diff 提交。

---

## 三、社区热点 Issues（Top 10）

### 1. [#41220](https://github.com/openai/codex/issues/41220) — 配额异常消耗元追踪（45 评论 / 👍17）
**最重磅的 issue**。作为跨报告聚合追踪器，它汇总了大量"配额/积分消耗速度远超历史基线"的反馈，涵盖订阅额度与购买积分。45 条评论说明这不是个例，而是系统性的用量核算问题。**为什么重要**：直接关系计费信任，是当前社区情绪最集中的爆发点。

### 2. [#44781](https://github.com/openai/codex/issues/44781) — Desktop 编辑重发排队消息报错（41 评论 / 👍50）
Windows Codex Desktop，对排队中的消息执行编辑并重发时触发 `App-server queued follow-up no longer exists`。**为什么重要**：50 个 👍 是本次数据中最高互动量之一，说明命中大量 Windows 用户的日常操作路径。

### 3. [#45019](https://github.com/openai/codex/issues/45019) — App-server 排队 follow-up 丢失（19 评论 / 👍48）
与 #44781 同源问题，macOS + X20 PRO 环境复现。**一个 bug 分裂成两个高赞 issue**，反映 app-server 队列状态机存在跨平台一致性问题。

### 4. [#35259](https://github.com/openai/codex/issues/35259) — 等待轮询导致模型重复入场消耗积分（26 评论 / 👍22）
Codex Desktop 在 Ultra/多智能体场景下，仅为"等待 agent 或轮询终端状态"就反复调用模型。作者实测：**纯 wait/status 轮询占本地 token 量的 19.8%**。这是 #41220 配额问题的技术根因之一。

### 5. [#45085](https://github.com/openai/codex/issues/45085) — GPT-6 Astra 单任务吃掉 86% 周配额（7 评论）
一次多智能体 Work 任务约 4.5 小时内消耗 ~1.98 亿 token（97.4% 命中缓存），占 Prolite 周配额 86%。**极端的量化案例**，为配额争议提供了可复现的数据样本。

### 6. [#18115](https://github.com/openai/codex/issues/18115) — 仓库级插件市场与配置（15 评论 / 👍66）

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-09-17** | 数据来源：[github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)

---

## 一、今日速览

今日社区焦点集中在 **Agent 可靠性** 与 **子代理（Subagent）行为异常** 上：多个 P1 级 Issue（如子代理达到最大轮次后误报成功、generalist agent 无限挂起、shell 命令执行卡死）持续被更新和重测，反映出多代理编排的稳定性仍是最大痛点。与此同时，PR 侧出现了大量安全与正确性修复，包括路径遍历绕过、原子文件写入、凭证泄露防护等，显示维护者正在加固核心执行链路。

---

## 二、版本发布

### v0.62.0-nightly.20260916.g6a466a7e2

过去 24 小时发布 1 个 nightly 版本，包含两项修复：

- **fix(core)**：确保 `AgentLoopContext` 属性在对象展开（object spread）过程中被正确保留 —— PR [#29335](https://github.com/google-gemini/gemini-cli/pull/29335)，作者 @diegogodinezr。这类问题可能导致 Agent 循环上下文状态丢失，属于底层正确性修复。
- **fix(a2a-server)**：在 tasks metadata endpoint 中针对不支持的 store 增加提前返回 —— 避免无效请求导致的异常路径。

该版本为夜间构建，主要服务于持续集成与早期验证。

---

## 三、社区热点 Issues

### 1. 子代理达到 MAX_TURNS 后误报为 GOAL 成功（P1）
[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) · 评论 13 · 👍 2

`codebase_investigator` 子代理在尚未执行任何分析前就达到最大轮次限制，却仍返回 `status: "success"` 和 `Termination Reason: "GOAL"`。这会**掩盖真实的中断原因**，让上层 Agent 误以为任务已完成，是本周期评论数最高的 Issue，也是最典型的"静默失败"问题。

### 2. Generalist Agent 无限挂起（P1）
[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) · 评论 8 · 👍 8

用户反馈一旦请求被转交给 generalist agent，即便是创建文件夹这类简单操作也会永久挂起，最长等待达 1 小时；明确指示模型不要使用子代理则可规避。**8 个 👍 表明这是高共鸣问题**，直指子代理委派机制的可靠性缺陷。

### 3. Shell 命令执行完成后卡在 "Waiting input"（P1）
[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) · 评论 4 · 👍 3

简单 CLI 命令执行完毕后，界面仍显示 shell 处于活动状态并"等待用户输入"。这是终端交互层与执行生命周期不同步的典型症状，严重影响日常使用流畅度。

### 4. 零依赖 OS 沙箱 + 执行后意图路由（P2）
[#19873](https://github.com/google-gemini/gemini-cli/issues/19873) · 评论 9

提案指出 Gemini 3 系列模型本质上被训练为"原生 bash 用户"，倾向于串联 `grep`/`cat`/`sed`/`awk` 等 POSIX 工具探索代码库。该 Issue 探索如何在不牺牲安全与体验的前提下释放这种能力，是**架构层面的重要讨论**。

### 5. AST 感知的文件读取、搜索与代码库映射评估（P2）
[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) · 评论 7

EPIC 级追踪议题，评估 AST 感知工具能否减少因读取边界不精确带来的多余轮次与 token 噪声。配套平台侧议题见 [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)，推荐以 tilth 或 glyph 为起点。

### 6. Gemini 不主动使用 skills 与子代理（P2）
[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) · 评论 6

用户反馈即使拥有描述清晰的 `gradle`、`git` 等自定义 skill，模型在高度相关的任务中也不会主动调用，必须显式指令。这直接影响扩展机制的实际价值，涉及**工具选择的策略与提示工程**。

### 7. Auto Memory 需要确定性脱敏（P2）
[#26525](https://github.com/google-gemini/gemini-cli/issues/26525) · 评论 5

Auto Memory 会读取本地会话记录并发送给后台提取代理，但脱敏只在内容进入模型上下文**之后**才由提示词完成。存在敏感信息先行暴露的风险，需要改为确定性（deterministic）前置脱敏。相关议题还包括 [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)、[#26523](https://github.com/google-gemini/gemini-cli/issues/26523)、[#26516](https://github.com/google-gemini/gemini-cli/issues/26516)。

### 8. Browser 子代理在 Wayland 下失败（P1）
[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) · 评论 4

Linux Wayland 环境下浏览器子代理启动即终止，并同样报告 `Termination Reason: GOAL`。与 #22323 形成同一类"终止原因误报"问题的两个表现面。

### 9. 输出 hook 导致 CLI 崩溃（P1）
[#22186](https://github.com/google-gemini/gemini-cli/issues/22186) · 评论 3

当 `get-shit-done` 输出接近完成、正在打印用户摘要时，Gemini 反复崩溃。属于 hook 机制与输出渲染交互的稳定性缺陷。

### 10. `/compress` 在会话恢复后失效（P2）
[#21335](https://github.com/google-gemini/gemini-cli/issues/21335) · 评论 2 · 👍 2

`/compress` 能在内存中正确用摘要替换历史，但**不会写回磁盘会话文件**，导致退出后恢复会话时压缩效果丢失。对长会话 token 成本控制影响显著。

> 其他值得留意的 Issue：Agent 破坏性行为约束 [#22672](https://github.com/google-gemini/gemini-cli/issues/22672)、超过 128 个工具触发 400 错误 [#24246](https://github.com/google-gemini/gemini-cli/issues/24246)、模型在随机位置创建临时脚本 [#23571](https://github.com/google-gemini/gemini-cli/issues/23571)、Browser Agent 忽略 settings.json 覆盖 [#22267](https://github.com/google-gemini/gemini-cli/issues/22267)、用持久化文件任务跟踪替代 WriteToDo [#18836](https://github.com/google-gemini/gemini-cli/issues/18836)。

---

## 四、重要 PR 进展

### 1. 修复 `get_internal_docs` 路径守卫的兄弟前缀绕过（P1，安全）
[#29249](https://github.com/google-gemini/gemini-cli/pull/29249)

原守卫使用字符串前缀比较，缺少路径分量边界判断，导致任何**名字以文档目录名开头**的兄弟目录都会被接受，工具可将该文件内容返回给模型。这是路径遍历类安全问题，优先级最高。

### 2. 工具文件写入原子化并对同路径写入串行化（P1）
[#29244](https://github.com/google-gemini/gemini-cli/pull/29244)

并行工具执行时，两个针对同一文件的 `replace` 调用会各自读取原始内容，后写者静默丢弃前者的修改，而**两个调用都向模型报告成功**。该 PR 修复这一隐蔽的数据丢失问题。

### 3. 修复 Git 仓库中认证阶段崩溃（P1，安全，已关闭）
[#29163](https://github.com/google-gemini/gemini-cli/pull/29163)

在 macOS Seatbelt 等受限权限环境下，启动时挂载的 `useGitBranchName` hook 因无法读取 `.git` 目录导致崩溃。已合并关闭。

### 4. web_fetch 保留表格行与列结构
[#29359](https://github.com/google-gemini/gemini-cli/pull/29359)

`web_fetch` 会丢失页面中的全部表格 —— `html-to-text` 在未指定 `table` 选择器时将 `<table>` 渲染为普通块，子元素直接拼接，三列价格表最终变成 `PlanPriceSeatsStarter9 EUR3Pro29...` 这样的乱码串。

### 5. 改进 PTY 文件描述符清理与执行生命周期管理
[#29340](https://github.com/google-gemini/gemini-cli/pull/29340)

跨 POSIX 平台完善 `ShellExecutionService` 与 `ExecutionLifecycleService` 的资源释放，确保 PTY 会话与后台 shell 执行结束时完整回收句柄。与 #25166 的卡死问题方向相关。

### 6. 不再在 shell 执行中清空用户 Git 配置（已关闭）
[#29156](https://github.com/google-gemini/gemini-cli/pull/29156)

`prepareExecution` 曾将 `GIT_CONFIG_GLOBAL`/`GIT_CONFIG_SYSTEM` 指向 `/dev/null`，使所有 shell 工具命令看不到用户的全局/系统 Git 配置，`user.name`、`user.email` 等失效。该行为已回退。

### 7. 修复 skill 优先级与激活状态的的大小写敏感性（已关闭）
[#29151](https://github.com/google-gemini/gemini-cli/pull/29151)

`SkillManager` 中工作区 skill 覆盖内置/扩展 skill 的优先级映射以及激活状态跟踪，在名称大小写不一致时失效。改为大小写不敏感匹配。

### 8. 正确解码 BOM 编码内容（已关闭）
[#29155](https://github.com/google-gemini/gemini-cli/pull/29155)

`isEmpty()` 检测到 BOM 后仍以 UTF-8 解码，导致 UTF-16/UTF-32 编码的纯空白 plan 文件被解码为 NUL 字符，`trim()` 判定为非空，从而绕过 `validatePlanContent` 校验。

### 9. 修复 CLI 截断时拆散 surrogate pair
[#29304](https://github.com/google-gemini/gemini-cli/pull/29304)

`sanitizeForDisplay` 截断边界落在 emoji 中间时会产出未配对代理项，渲染时静默丢字。属于终端显示层的基础正确性修复。

### 10. Windows 下 `isWithinRoot` 改为大小写不敏感
[#29247](https://github.com/google-gemini/gemini-cli/pull/29247)

原实现用大小写敏感的 `===`/`startsWith` 比较路径，在 Windows 上会拒绝盘符或目录大小写不同的合法根内路径，破坏 ACP/IDE 文件系统路由与忽略路径归一化。

> 其他 PR：无根 podman 沙箱使用 `--userns=keep-id` [#29354](https://github.com/google-gemini/gemini-cli/pull/29354)、修正环境变量脱敏文档 [#29353](https://github.com/google-gemini/gemini-cli/pull/29353)、补全 hook 决策值文档 [#29352](https://github.com/google-gemini/gemini-cli/pull/29352)、避免确认后重复历史与遥测 [#29248](https://github.com/google-gemini/gemini-cli/pull/29248)、反向搜索高亮对齐原文 [#29358](https://github.com/google-gemini/gemini-cli/pull/29358)。

---

## 五、功能需求趋势

从过去 24 小时更新的 50 条 Issue 与 29 条 PR 中，可提炼出以下社区关注方向：

| 方向 | 代表 Issue / PR | 说明 |
|---|---|---|
| **多代理编排与子代理可靠性** | #22323、#21409、#21968、#20195 | 数量最多、优先级最高的一类，涵盖委派、恢复、终止语义、轨迹可见性 |
| **执行生命周期与终端交互稳定性** | #25166、#22186、#21924、#22465 | shell 卡死、hook 崩溃、resize 闪烁、交互式提示阻塞 |
| **安全沙箱与权限边界** | #19873、#29249、#29163、#26525 | OS 沙箱、路径遍历、认证崩溃、确定性脱敏 |
| **代码理解

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-09-17** | 数据来源：[github.com/github/copilot-cli](https://github.com/github/copilot-cli)

---

## 一、今日速览

过去 24 小时 Copilot CLI 连续发布 v1.0.86-1、v1.0.86-0 两个补丁版本，并延续 v1.0.85 的 Vim 模式与上下文管理能力，重点修复了会话恢复的健壮性与 Autopilot 行为。社区侧，Issue 清理节奏明显加快：多个长期高赞需求（自定义 Agent 推理强度、子 Agent 工具调用可见性）被关闭，但 MCP 配置不生效、OAuth 认证链路不可达等配置/网络类问题仍在持续发酵。此外，Worktrees 默认行为、Windows/macOS 平台兼容性、中文输入法等开发者体验问题保持较高关注度。

---

## 二、版本发布

### v1.0.86-1
- **新增**：自定义 Agent 现在可通过 frontmatter 中的 `include-custom-instructions: true` 主动选择加入仓库级指令文件（`AGENTS.md`、`copilot-instructions.md`、`CLAUDE.md`），使 Agent 的上下文注入更可控。
- **修复**：在未指定 plugin-directory、discovery 或 working-directory 覆盖参数时恢复活跃会话，行为更加稳定。

### v1.0.86-0
- **修复**：即使 transcript 文件存在可恢复的损坏，也仍可恢复会话。
- **修复**：compact timeline 中展开的推理文本不再被置灰，可读性与时间线其余部分保持一致。
- **修复**：Autopilot 在任务被接受完成后即停止，不再意外继续执行。

### v1.0.85（2026-09-16）
- **Vim 模式全面开放**：通过 `/vim` 或设置 `editorMode: vim` 启用模态编辑，输入时实时显示当前模式。
- **新增 `/settings` 选项**：可选择性为 Agent 和子 Agent 启用上下文管理工具。
- 新增 `transcriptView` 相关设置（内容在数据中被截断，建议查看 Release 页面）。

> 发布页：https://github.com/github/copilot-cli/releases

---

## 三、社区热点 Issues

以下为过去 24 小时内更新、最值得关注的 10 个 Issue：

1. **[#2904 [CLOSED] 自定义 Agent YAML Frontmatter 应支持 reasoning effort](https://github.com/github/copilot-cli/issues/2904)**
   - 9 条评论 · 23 👍
   - 当前 reasoning effort 只能通过全局 CLI 参数 `--effort` 配置，无法按 Agent 粒度区分。该需求触及多 Agent 协作场景的核心——不同任务需要不同推理深度。高赞且已关闭，说明官方已响应。

2. **[#1322 [CLOSED] 展示子 Agent 工具调用详情](https://github.com/github/copilot-cli/issues/1322)**
   - 7 条评论 · 25 👍
   - 目前子 Agent 只显示状态和耗时，无法像 VS Code Copilot Chat 那样下钻查看工具调用。这是可观测性的关键缺口，25 个赞反映了开发者对调试能力的强烈诉求。

3. **[#2243 [OPEN] Worktrees 是灾难，应默认禁用](https://github.com/github/copilot-cli/issues/2243)**
   - 3 条评论 · 16 👍
   - 用户反馈 CLI 自动创建的 worktree 导致大量代码难以合回主分支。涉及默认安全策略与 Git 工作流侵入性，仍是开放状态，值得持续跟踪。

4. **[#2050 [CLOSED] Claude Sonnet 4.6 执行失败：HTTP/2 GOAWAY 连接中断](https://github.com/github/copilot-cli/issues/2050)**
   - 9 条评论 · 4 👍
   - 在大文件（8KB YAML）任务中重试 5 次仍失败，而 Gemini 3 Pro 无此问题。指向特定模型 + 网络层的稳定性问题，已关闭但影响面较大。

5. **[#4542 [OPEN] Workspace `.mcp.json` 被 `mcp list` 识别却未在实际会话中连接](https://github.com/github/copilot-cli/issues/4542)**
   - 3 条评论 · 1 👍
   - `copilot mcp list` 显示 `Status: Enabled`，但交互式/`-i`/`-p` 会话中均不可用。配置检测与运行时加载脱节，是 MCP 生态信任度的典型问题。

6. **[#3100 [OPEN] 带 Bearer Token 的 HTTP MCP Server 走 OAuth 发现而非回退到 Header 认证](https://github.com/github/copilot-cli/issues/3100)**
   - 1 条评论 · 10 👍
   - 明明配置了 `Authorization: Bearer`，CLI 却尝试 `/.well-known/oauth-authorization-server` 并失败。10 个赞说明大量企业用户受此困扰。

7. **[#4855 [CLOSED] macOS Terminal 中 1.0.84-8 无法接受交互键盘输入](https://github.com/github/copilot-cli/issues/4855)**
   - 3 条评论
   - 界面正常加载但键盘无响应，非交互模式正常。此类"完全不可用"级 Bug 对 macOS 用户影响直接，需确认新版本是否已修复。

8. **[#3009 [OPEN] 远程容器 / Codespaces 中 MCP OAuth 回调不可达，且无手动粘贴 Token 兜底](https://github.com/github/copilot-cli/issues/3009)**
   - 2 条评论 · 1 👍
   - OAuth 重定向到 `localhost` 回调地址，在容器/远程开发环境中浏览器无法访问，也没有手动粘贴授权码的降级路径。远程开发场景的阻塞性缺陷。

9. **[#3170 [CLOSED] 中文输入光标位置错误](https://github.com/github/copilot-cli/issues/3170)**
   - 2 条评论 · 2 👍
   - 涉及 CJK 输入法的终端渲染与光标定位，对中文开发者日常体验影响明显，已关闭。

10. **[#4854 [CLOSED] 本地沙箱"Allow local network"设置不生效](https://github.com/github/copilot-cli/issues/4854) / [#4867 [OPEN] `/sandbox policy` 命令存在 Bug](https://github.com/github/copilot-cli/issues/4867)**
    - 3 条评论 / 1 条评论
    - 无论开关如何，`/sandbox policy` 均显示网络被阻止；官方回应"会修"。沙箱策略的"显示与行为不一致"会严重削弱用户对安全边界的信任。

---

## 四、重要 PR 进展

过去 24 小时内，仓库 **无新增或更新的 Pull Request（共 0 条）**。

本日代码变更主要通过 Release 通道交付（见"版本发布"部分），其中 v1.0.86 系列涉及的会话恢复健壮性、推理文本可读性、Autopilot 终止逻辑，以及 v1.0.86-1 的自定义指令文件选择加入机制，可视为对应 PR 已合并后的产物。建议关注后续 PR 恢复更新后再做跟踪。

> PR 列表：https://github.com/github/copilot-cli/pulls

---

## 五、功能需求趋势

从本期 50 条 Issue 中可提炼出以下六大方向：

1. **Agent 细粒度控制**：按 Agent 配置 reasoning effort（#2904）、自定义指令文件的选择加入（v1.0.86-1）、plugin skills 注入 `available_skills`（#2753）。社区希望 Agent 从"全局配置"走向"按任务定制"。

2. **可观测性与调试透明化**：子 Agent 工具调用详情（#1322）、推理文本不再置灰（v1.0.86-0）、`/skills` UI 支持文本复制（#3741）。开发者需要看清 Agent 在做什么。

3. **MCP 配置与认证的可靠性**：workspace

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-09-17）

## 今日速览
过去 24 小时无新 Release；社区仅有 1 条 Issue 和 1 条 PR 更新。最值得关注的是 #2647：会话触发 5 小时用量限制 403 后，主 agent 持续重试 14+ 小时，子 agent 还生成脱离式重试循环并整夜调用 Kimi CLI，暴露出配额耗尽后的失控重试与子 agent 生命周期管理问题。另一条 #2648 则提供了 `PreToolUse` 安全门示例，用 HOL Guard 在执行 Shell 命令前做分类拦截。

---

## 版本发布
本日无新版本发布。

---

## 社区热点 Issues
> 说明：过去 24 小时内仅 1 条 Issue 更新，无法挑选 10 条；以下为全量列出。

### 1. #2647 [OPEN] Session keeps burning quota after terminal 403 "5-hour usage limit": subagent spawns detached retry-loop calling kimi CLI overnight, main agent retries for 14h
- 作者：@gleb7499
- 创建/更新：2026-09-16
- 评论：0｜👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2647
- 摘要：会话命中终止性 `403 provider.auth_error: 5-hour usage limit` 后，出现三类问题：主 agent 未中止会话，而是持续重试失败的 LLM 请求 14+ 小时；一个模型访问被拒的 subagent 写入并启动了 detached 任务；标题显示该 subagent 生成脱离式重试循环，整夜调用 Kimi CLI。
- 为什么重要：这不是普通报错，而是配额耗尽后的“重试风暴”和子 agent 资源泄漏问题，可能导致额度持续燃烧、后台进程失控、无人值守场景下成本不可控。
- 社区反应：暂无评论和点赞，但问题严重性高，涉及核心错误恢复与进程生命周期机制。

---

## 重要 PR 进展
> 说明：过去 24 小时内仅 1 条 PR 更新，无法挑选 10 条；以下为全量列出。

### 1. #2648 [OPEN] examples: add HOL Guard PreToolUse gate
- 作者：@kantorcodes
- 创建/更新：2026-09-16
- 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/pull/2648
- 内容：新增一个聚焦 `PreToolUse` 的示例，将 Kimi CLI 的 `Shell` 命令在执行前发送给 HOL Guard。该 hook 会调用 `hol-guard command test <command> --json`，仅当 `classification.explicitly_benign` 为 `true` 且 `minimum_action` 为 `allow` 时继续执行，否则以退出码 2 处理。
- 价值：展示如何在工具执行前加入命令安全分类与策略门禁，有助于防止危险 Shell 命令被 agent 直接执行。

---

## 功能需求趋势
> 注：过去 24 小时样本仅 2 条，趋势判断代表性有限。

- **配额与限流错误处理**：社区关注 terminal 错误触发后的熔断、退避和会话终止机制，避免无限重试。来源：https://github.com/MoonshotAI/kimi-cli/issues/2647
- **子 agent 生命周期与资源隔离**：需要限制 subagent 生成 detached 进程、递归调用 CLI 或脱离主会话继续运行。来源：https://github.com/MoonshotAI/kimi-cli/issues/2647
- **执行前安全门禁**：通过 `PreToolUse` 或类似 hook 对 Shell 命令做分类、白名单和策略判断。来源：https://github.com/MoonshotAI/kimi-cli/pull/2648
- **可观测性与终止控制**：开发者需要更清晰的会话状态、重试次数、子进程跟踪，以及一键中止残留任务的能力。

---

## 开发者关注点
- **配额成本失控**：403 用量限制后仍持续重试，可能整夜消耗额度，是当前最突出的痛点。
- **错误恢复策略不足**：终止性认证/限流错误应直接中止或进入可控退避，而不是让主 agent 重试 14+ 小时。
- **subagent 与 detached 进程风险**：子 agent 被拒后仍生成脱离式循环，说明需要更严格的进程边界和父子会话终止传播。
- **Shell 命令安全执行**：`PreToolUse` + HOL Guard 示例说明社区正在探索执行前安全审核，降低危险命令执行风险。

---

数据来源：github.com/MoonshotAI/kimi-cli。以上内容仅基于过去 24 小时内更新的 Issue/PR，不代表项目全量社区动态。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 · 2026-09-17

> 数据来源：github.com/anomalyco/opencode

---

## 一、今日速览

过去 24 小时**无新版本发布**，社区讨论高度集中在**新版 UI 的强制性迁移**上——恢复旧版布局/持久左侧边栏的相关 Issue 占据热榜前五中的四席，累计 👍 超过 80。与此同时，Provider 侧的**工具调用（tools）失败**与**reasoning/encrypted_content 报错**成为新增 bug 的主要来源。PR 方面当日无任何推进：展示的 20 个 PR **全部处于 CLOSED 状态且统一带有 `automated-pr-cleanup` 标签**，均创建于 2026-08-16，属于历史积压 PR 的批量清理。

---

## 二、社区热点 Issues

### 1. 恢复旧版 UI：持久左侧边栏（#48882）🔥 最高热度
23 条评论、27 👍，是当日讨论最激烈的议题。作者指出 #20242 的侧边栏重构将经典双栏布局（持久左侧栏 + 会话面板）替换为顶部标签式布局，请求以可选开关的形式恢复旧版。
🔗 https://github.com/anomalyco/opencode/issues/48882

### 2. Web 端无法回退新布局，且新布局缺失 Workspaces（#37546）
24 👍，热度仅次于 #48882。核心诉求：升级到 `v1.17.19` 之后新布局自动启用且**没有 UI 入口切回**，同时新布局**完全未实现 workspaces（git worktree）**，导致依赖工作区的 Web 用户无法降级。
🔗 https://github.com/anomalyco/opencode/issues/37546

### 3. 强制 V2 界面摧毁多项目/多 Agent 工作流（#48837）
17 👍。作者管理 20+ 会话，指出切换回旧 GUI 的选项已被完全移除（界面提示"先前的版面已无法使用"），对多项目并行场景造成实质性效率损失。这是产品决策层面的强反馈，不只是 UI 偏好。
🔗 https://github.com/anomalyco/opencode/issues/48837

### 4. 新 UI 增加"持久左侧边栏"布局选项（#48956）
12 👍，与 #48882、#49021、#49005 形成同一诉求的集群（分别为：恢复旧布局、恢复旧布局、增加 escape hatch）。社区用多个 Issue 反复表达同一需求，说明官方尚未给出明确回应。
🔗 https://github.com/anomalyco/opencode/issues/48956

### 5. Zen API 免费模型带 tools 请求全部失败（#44300，已关闭）
15 条评论，是技术类 Issue 中讨论最深入的。`x-preview-f-free` 与 `ox-alpha-free` 自 2026-08-23 起，任何包含 `tools` 数组的请求在两个入口均返回 `Endpoint is unavailable`。该问题已关闭，但其症状在今日新 Issue 中**仍以变体形式复现**（见 #49413）。
🔗 https://github.com/anomalyco/opencode/issues/44300

### 6. 支持 `$skill-name` 行内技能调用（#15617）
25 👍，是热榜中点赞最高的**功能请求**。目前技能只能在 prompt 起始位置调用，社区希望在任意位置使用 `$skill-name` 语法，让技能组合更接近"斜杠命令 + 自然语言"的混合工作流。
🔗 https://github.com/anomalyco/opencode/issues/15617

### 7. Agent 步骤循环在 `unknown` finish reason 下永不终止（#49414，今日新增）
高价值技术报告。当 provider 返回的 finish reason 无法映射到 opencode 内部枚举（`stop`/`length`/`tool-calls`/`content-filter`/`error`）而落到 `unknown`、且本轮无工具调用时，`SessionPrompt.run` 的循环不退出，形成**无界请求风暴**。属于可能造成账号额度被烧的高危缺陷。
🔗 https://github.com/anomalyco/opencode/issues/49414

### 8. 会话标题由注入的记忆/系统上下文生成（#23114）
当 memory MCP 服务向系统提示或合成消息注入历史摘要时，自动标题生成会把完整渲染后的消息历史传给标题模型，导致标题反映的是记忆内容而非用户真实输入。属于 MCP 生态普及后的典型上下文污染问题。
🔗 https://github.com/anomalyco/opencode/issues/23114

### 9. 长会话中途冻结/无响应（#34214）
多次工具调用往返后助手突然停止响应，UI 冻结、工具不再执行，必须强制关闭终端。该 Issue 自 6 月创建至今仍为 OPEN，是**长会话稳定性**长尾问题的代表。
🔗 https://github.com/anomalyco/opencode/issues/34214

### 10. OpenAI 兼容 provider 的 `reasoning` 字段被丢弃（#35283）
当 provider 把思维链放在 `reasoning` delta 字段（而非 `reasoning_content`）时，opencode 直接丢弃，推理内容完全不显示。问题定位在 `packages/llm/src/protocols/openai` 的 delta schema，影响所有走 OpenAI 兼容协议的第三方推理模型。
🔗 https://github.com/anomalyco/opencode/issues/35283

### 其他值得留意
- **#49413** `union-alpha` 带工具调用稳定 503（今日新增，与 #44300 同源）。
- **#49188 / #49173** `muse-spark-1.3-contributor-free` 报 `encrypted_content was not issued to this caller`，新会话 2–3 条消息即触发。
- **#49416** 用户质疑"为免费模型付费"，暴露出免费额度的错误提示指向第三方计费页面，体验割裂。
- **#49401** 新 UI 下项目侧边栏不显示任何会话（Web + Desktop 均复现）。

---

## 三、重要 PR 进展

> ⚠️ **重要前提**：过去 24 小时内更新的 20 个 PR **全部为 CLOSED**，且统一带有 `[automated-pr-cleanup]` 标签，创建时间均为 2026-08-16。也就是说，这些是**被自动化流程批量关闭的历史积压 PR**，而非当日合入的新功能。以下按内容价值排列，供了解被搁置/关闭的工作方向。

| # | PR | 内容 |
|---|---|---|
| 1 | #42872 | **Desktop MOD 加载器 Beta**：加载前校验 MOD manifest 与权限申请，并上报贡献配置。若后续重新推进，将是桌面端扩展性的关键基础设施。 |
| 2 | #42904 | **Server 项目元数据 API**：新增 `PATCH /api/project/:projectID`，可更新项目名称、图标与启动命令，空字段保留原值。 |
| 3 | #42927 | **TUI 显示上下文窗口上限**：输入栏原本只显示 `30.0K (15%)`，改为展示上限值，同时关联 #13003。 |
| 4 | #42939 | **TUI 默认隐藏 tab 快捷数字**，新增 `tabs.numbers` 配置项并在设置面板中暴露。 |
| 5 | #42885 | **TUI worker RPC 失败不再白屏挂起**，改为显式暴露错误（关闭 #34981，关联 #41284/#35494）。 |
| 6 | #42854 | **Windows 工具命令非交互执行**：修复 `npm exec` 之类提示 stdin 时挂起的问题，保持子进程 stdin 关闭。 |
| 7 | #42894 | **避免无 model 的 prompt 覆盖用户手动切换的模型**（修复插件 completion-reminder 场景）。 |
| 8 | #42937 / #42936 | **新增 Taplo（TOML）与 Marksman（Markdown）LSP 支持**，扩充编辑器语言能力。 |
| 9 | #42902 / #42901 | **新增 Odin 语法高亮**（V2 TUI，注册 Tree-sitter WASM）与 **PureScript `purs-tidy` 格式化支持**。 |
| 10 | #42840 | **CLI 暴露持久化事件**：将 `OPENCODE_EVENTS_PERSIST=1` 映射到既有的 `ServerOptions.events.persist`。 |

**解读**：当日 PR 队列呈现"只出不进"状态。语言支持、LSP 扩展、桌面扩展机制等社区贡献均被自动关闭，短期内外部署贡献者的合入预期需要下调。

---

## 四、功能需求趋势

1. **UI 布局可配置化（绝对主导）**
   恢复旧版布局、持久左侧边栏、布局 toggle 转正、Web 端补回切换入口——相关 Issue 至少 7 个（#48882、#49021、#37546、#38230、#48837、#48956、#49005），点赞合计逾 80。核心诉求从"审美偏好"升级为"是否需要 escape hatch"的产品治理问题。

2. **多项目 / 多工作区（workspace / git worktree）能力回归**
   #37546、#37508、#48837 反复指向同一件事：新布局没有实现 workspaces，而这是多项目并行用户的核心工作流。

3. **可扩展性与技能系统**
   `$skill-name` 行内调用（#15617，25 👍）、Desktop MOD 加载器（#42872）显示社区希望把 OpenCode 当作可编程平台而非固定形态工具。

4. **Provider 兼容性与协议健壮性**
   集中在 `tools` 数组导致的 503（#44300、#49413）、`reasoning` 字段解析（#35283）、`encrypted_content` 校验（#49188、#49173）三类，均属 OpenAI 兼容层的边界处理缺失。

5. **平台覆盖扩展**
   #49316 请求官方 Android APK，反映移动端/远程开发场景的需求苗头。

---

## 五、开发者关注点

- **强制迁移缺乏退路，是最强烈的情绪点**。多份 Issue 明确指出"切换回旧版面的选项已完全消失"，并认为这是产品决策而非缺陷——一旦 `oldInterfaceSunset` 日期生效，桌面端用户将无法保留原布局。
- **新 UI 存在功能性回归**：workspaces 缺失（#37546、#37508）、侧边栏不显示会话（#49401）、TUI 侧边栏消失后 Toggle 无效（#28971）。这不只是外观变化，而是能力净损失。
- **Provider 网关在带工具调用时不稳定**是当前最高频的运行时报错，且呈现"修复一个、复现一个"的模式（#44300 关闭后 #49413 立即出现），建议官方从网关侧统一排查而非逐模型修补。
- **长会话可靠性仍是长尾痛点**：中途冻结（#34214）、Agent 循环不终止（#49414）、`opencode2` 卡在 "Starting background server..."（#41746）均指向会话生命周期管理。
- **错误信息误导**：免费模型额度耗尽后返回指向第三方计费页的 `insufficient_user_quota` 提示（#49416），对"免费模型"用户造成认知冲突。
- **平台细节问题被长期搁置**：Neovim 内嵌终端粘贴重复（#34078）、Windows 上启动后 `Failed to fetch`（#46651）、TUI 中 Markdown 链接渲染为 `label (url)` 而非 OSC 8 纯标签（#45001）。

---

*本日报由 AI 开发工具技术分析自动生成，数据截至 2026-09-17。*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*