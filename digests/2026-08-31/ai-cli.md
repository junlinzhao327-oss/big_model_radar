# AI CLI 工具社区动态日报 2026-08-31

> 生成时间: 2026-08-31 00:40 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-08-31）

## 1. 生态全景

当前 AI CLI 工具已从"功能竞赛"进入**稳定性与信任建设**阶段。今日各社区动态显示，Windows 平台基础体验、远程控制能力、安全策略透明度、Agent 行为可靠性成为跨工具的共性痛点，而新功能需求相对退居其次。Claude Code 与 OpenAI Codex 凭借庞大用户基数承担了最多"踩坑"反馈；Gemini CLI 与 Qwen Code 正处于快速修复与治理收敛期；Kimi Code 与 OpenCode 则表现出差异化路径（前者聚焦模型工具调用准确性，后者深耕开源插件生态与计费体验）。整体来看，用户对"更新引入回归"的容忍度持续降低，对官方响应时效与兼容性测试的期待显著上升。

## 2. 各工具活跃度对比

| 工具 | 热点 Issues | PR 动态 | Release 情况 | 社区热度信号 |
|------|------------|---------|-------------|-------------|
| **Claude Code** | 10 个（最高 84 评论/98 👍） | 1 个（已关闭） | 无 | 最热 issue 评论数全场最高，"窗口置顶"获 98 👍 |
| **OpenAI Codex** | 10 个（最高 37 评论/34 👍） | 10 个（全部合并） | 发布 `rust-v0.152.0-alpha.4` | 10 项 PR 密集合入，迭代节奏快，安全策略变更引发争议 |
| **Gemini CLI** | 11 个（最高 13 评论，3 个 p1） | 10 个（8 开放/2 关闭） | 发布 1 个 nightly | 维护者对 p1 bug 集中 retest，Dependabot 大 PR（77 包）引关注 |
| **GitHub Copilot CLI** | 无数据 | 无数据 | 无数据 | — |
| **Kimi Code CLI** | 2 个（均为全新） | 无 | 无 | 社区规模最小，但工具调用行为不一致问题直指核心可靠性 |
| **OpenCode** | 10 个（最高 25 评论） | 10 个（8 修复/2 功能） | 无 | 数据库膨胀（13GB+）与计费一致性成社区焦点 |
| **Qwen Code** | 10 个（含 1 个 P1 安全） | 9 个（全部开放中） | nightly 发布失败 | 安全评审（P1）受关注，"跨会话通信"有 12 条讨论 |

> 注：以上为各工具日报中精选并详细列出的数量，非当日全部 Issue/PR 总数；GitHub Copilot CLI 日报数据缺失。

## 3. 共同关注的功能方向

| 方向 | 涉及工具 | 具体诉求 |
|------|---------|---------|
| **Windows 稳定性** | Claude Code（GPU 崩溃 #80444、窗口置顶 #85891、启动失败 #53247）、OpenAI Codex（DWM 句柄泄漏 #33192、WSL 项目操作失败 #41290）、Qwen Code（Computer Use 驱动每次运行 panic #10538） | 三大工具在 Windows 上均有长期未闭环的高热度 bug，涉及桌面版/终端/驱动多个层面，用户要求官方优先补齐基础体验 |
| **远程控制（Remote Control）** | Claude Code（默认开启引发隐私担忧 #88094）、OpenAI Codex（无法附加到进行中会话 #37967，17 👍）、Kimi Code（iPadOS 16.6 Safari/微信登录失败 #2627） | 远程控制功能被多个工具视为核心卖点，但"授权模型、会话附加能力、跨端兼容性"均未达预期 |
| **安全策略透明度** | Claude Code（21 个 AUP/Cyber 误报，输入主观表达触发会话中断）、OpenAI Codex（`approval_policy="untrusted"` 被无弃用移除，34 👍）、Gemini CLI（Auto Memory 脱敏时点在提取模型之后 #26525）、Qwen Code（git 配置键可触发任意命令执行 #10561，P1） | 用户不反对安全机制，但要求"策略变更可见、误报有解释、敏感处理有明确时序" |
| **Agent 行为可靠性** | Gemini CLI（Subagent 达到 MAX_TURNS 仍误报 GOAL 成功 #22323、Generalist Agent 无限挂起 #21409）、Kimi Code（UI 显示 Write 实际发送 Read #2628）、OpenCode（会话永久卡死 #43277）、Claude Code（计划任务被按交互式权限执行 #89632） | "日志/状态与实际行为不一致"是多工具共性问题，直接影响用户对自动化的信任 |
| **插件/生态兼容** | Claude Code（插件 marketplace 不同步 #86428、shebang 可移植性 #35350）、Gemini CLI（hooks 迁移超时单位/键名错误 #29125/#29124）、OpenCode（旧插件加载器把辅助函数混入 hooks #42451、typed RPC 演进 #46105） | 插件系统的"协议规范化"与"迁移兼容性"是共同演进方向 |
| **订阅/计费体验** | Claude Code（Max 5x→20x 支付失败 #56281，官方支持无响应）、OpenCode（扣款成功却显示余额不足 #37790、连续扣款 3 月后突然被拒 #45278、无法删除账户仍持续扣费 #18016） | 付费链路故障正从"偶发"变成"系统性问题"，直接影响产品商业化根基 |

## 4. 差异化定位分析

| 工具 | 功能侧重 | 目标用户 | 技术路线特征 | 当前主要矛盾 |
|------|---------|---------|-------------|-------------|
| **Claude Code** | 桌面应用 + TUI 双形态，插件生态完善，长会话管理 | 从个人开发者到企业的广泛群体；订阅用户占比高 | Electron 桌面版 + CLI 扩展机制，依赖注入式 hooks | 功能最多但 Windows 基础体验拖后腿，AUP 误报损害信任 |
| **OpenAI Codex** | 深度集成模型能力（Computer Use、浏览器操作）、Rust 原生 CLI | 技术敏感型开发者，偏好可定制的本地工具链 | Rust 工具链 + 频繁预发布（alpha），Guardian 授权机制 | 安全策略变更沟通不足，Windows 各子功能（DWM/远程/更新链）故障分散 |
| **Gemini CLI** | Agent 多子代理协作（Subagent、browser_agent）、skills 体系 | 偏好自动化与多代理工作流的开发者 | Google 生态（Gemini 模型 + Antigravity 集成），nightly 高频迭代 | Agent 状态不可信（误报成功/挂起），依赖更新量大需谨慎 |
| **Kimi Code CLI** | 订阅 + OAuth 托管模式，Remote Control 远程控制 | Moonshot 生态用户，移动/远程办公场景 | 官方托管服务，轻量客户端，依赖 Web 控制台 | 社区体量小，工具调用链可观测性不足；跨端兼容刚起步 |
| **OpenCode** | 开源可自托管，插件体系开放式演进，多 provider 接入 | 企业自部署用户、对数据主权敏感的开源社区 | TypeScript 全栈，强调插件契约与进程生命周期治理 | 数据存储无上限策略、计费状态一致性；协议兼容性（variants 字段丢失等） |
| **Qwen Code** | 安全治理导向，Web Shell / VS Code 深度集成，worktree 与沙箱 | 企业用户 + 中文开发者社区贡献者 | 安全审查管线前置（P1 评审），nightly 自动化发布，多平台（Linux/Wayland）适配 | 安全漏洞面收敛与 Web Shell 功能完善并行，nightly 稳定性待提升 |

## 5. 社区热度与成熟度

- **最成熟、社区最大**：Claude Code 以「84 条评论 + 98 👍」的单一 issue 热度断层领先，且 21 个同类 AUP 误报 issue 说明其用户基数足以暴露系统性问题的全貌；但侧面上也反映其更新质量管控压力巨大。
- **高活跃、迭代快**：OpenAI Codex 与 Gemini CLI 均维持高频发布节奏（Codex 单日 10 项 PR 合入 + 1 个 alpha；Gemini 每夜出包），Codex 显示"企业级治理"特征（bot 作者集中），Gemini 显示"社区协作修复"特征（独立贡献者密集提交微补丁，多条 PR 被要求先关联 issue）。
- **快速追赶、治理转向**：OpenCode 与 Qwen Code 从"铺功能"转向"清系统性技术债"——OpenCode 修复一个 bash 挂起连带关闭 7 个相关 issue；Qwen Code 引入安全评审并标记 P1 类问题，社区中英文/西语反馈并存。
- **早期、尚需培育**：Kimi Code 单日仅 2 个新 issue、无 PR 合入，社区规模与生态成熟度均处起步阶段，但首个 issue 即直击工具调用核心正确性，说明早期用户质量较高。

## 6. 值得关注的趋势信号

1. **"状态与行为一致性"成为信任分水岭**：从 Gemini 的 Subagent 误报成功、Kimi 的日志显示 Write 实际发 Read，到 OpenCode 的"扣款成功但显示欠费"——**"系统汇报的状态 ≠ 实际执行的结果"** 正成为跨工具最危险的信任杀手。开发者在评估新工具时，建议优先验证其审计日志与实际行为是否一致，而非只关注 demo 效果。

2. **Windows 不再是"二等公民"而是"一等缺陷源"**：Claude Code GPU 崩溃、Codex DWM 句柄泄漏、Qwen Computer Use 每次 panic——三大工具同一天在 Windows 上出现高热度故障，说明 AI CLI 的桌面客户端架构（Electron/系统级 API 调用）在 Windows 下尚未成熟。**对 Windows 重度用户而言，短期内建议锁定稳定版本、避免追新**。

3. **远程控制从"功能"走向"工作流基础设施"**：三个工具同时出现远程控制相关 issue，且诉求各不相同——Claude Code 要默认关闭、Codex 要支持附加进行中会话、Kimi 要兼容 iPadOS。远程能力正在从"锦上添花"变为"移动办公刚需"，但**授权模型与跨端兼容性未跟上**，先发者未必占优。

4. **安全机制的最大风险是"不可解释"**：AUP 误报、approval_policy 静默移除、脱敏时机不明、git 配置键漏洞——本质都是"安全系统在用户不可见的地方做了影响结果的决策"。**具备安全审计能力、支持策略回滚/干跑的工具将在企业采购中胜出**。

5. **插件生态进入"协议规范化"赛点**：OpenCode 推出 typed RPC、Gemini 修复 hooks 迁移单位/键名、Claude Code 解决 marketplace 同步——各工具都在为"可移植插件"打地基。**接口契约的标准化程度将决定开发者资产的可迁移性**，值得关注是否存在跨工具的统一标准苗头。

6. **计费/订阅故障开始反噬产品口碑**：Claude Code 支付失败无响应、OpenCode 扣款不认账与删除账户困难，已从个例演变为批量反馈。**商业化闭环的可靠性正成为用户留存的新变量**，评估工具时需纳入厂商支持响应时效作为权重。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告
（数据来源: github.com/anthropics/skills · 截至 2026-08-31）

> 数据说明: 快照中 PR 评论数字段未完整捕获，本报告按源数据排序（即评论数降序）推断热度，并结合 Issues 评论/点赞数交叉验证。

---

## 1. 热门 Skills 排行（Top 7）

### 🥇 #1298 skill-creator 评估链路修复 —— 热度最高
- **功能**：修复 `run_eval.py` 恒报 `recall=0%` 的关键缺陷（安装 eval artifact 为真实 skill，并修复 Windows 流读取、触发检测与并行 worker 问题）。
- **讨论热点**：与 Issue #556 直接联动，已有 10+ 独立复现；`run_loop.py`、`improve_description.py` 均消费该信号，意味着 **description 优化循环一直在"对着噪声优化"**。
- **状态**：OPEN（2026-06 创建，6-23 仍有更新）
- 链接: https://github.com/anthropics/skills/pull/1298

### 🥈 #514 document-typography —— 文档排版质检
- **功能**：检测 AI 生成文档的三大高频排版问题——孤行（1–6 词溢出到下一行）、孤寡段落（标题滞留页底）及编号错位。
- **讨论热点**：直击 "AI 生成文档排版劣化" 的普适痛点，被评价为影响每一份 Claude 生成文档的隐形问题。
- **状态**：OPEN（已活跃 5 个多月）
- 链接

---

## Claude Code 社区动态日报（2026-08-31）

### 今日速览

今日无新版本发布。Windows 平台稳定性问题持续占据社区焦点：#80444（GPU 崩溃导致应用不可启动）已达 84 条评论，仍是当前最热 issue；#85891（窗口置顶）虽评论数较少，但以 98 个 👍 成为呼声最高的需求。值得注意的新动向是 macOS 桌面版会话管理问题浮出水面（#90798），以及大量 AUP/Cyber 安全误报系列 issue 被统一标记为 stale。

---

### 社区热点 Issues（10个）

**1. Windows 桌面版 GPU 崩溃，MSIX 包损坏无法启动** — #80444
评论 84 · 👍 14 · [链接](https://github.com/anthropics/claude-code/issues/80444)
Electron 42.7.0 / Chrome 148 环境下，通过应用内浏览器标签页触发的致命 GPU 进程崩溃（0x060C201E）会导致 MSIX 包进入不可启动状态（appxState=2），用户必须执行 Repair 才能恢复。已确认在多个显卡驱动版本上复现，是目前社区讨论最激烈的问题。

**2. Windows 桌面版窗口始终置顶，无设置可关闭** — #85891
评论 44 · 👍 98 · [链接](https://github.com/anthropics/claude-code/issues/85891)
Windows 11 上 Claude Desktop 窗口始终绘制在其他应用之上，即使用户切换焦点也无法被覆盖。这是 #66516（macOS 版相同问题）的 Windows 对应问题，98 个 👍 表明该问题影响面极广，社区强烈要求提供开关。

**3. Windows 启动失败：孤立 Silo / Job Object 致需注销或重启** — #53247
评论 36 · 👍 20 · [链接](https://github.com/anthropics/claude-code/issues/53247)
应用崩溃后遗留的孤立 Job Object 导致后续启动持续失败（HRESULT 0x80070020），只有注销或重启才能恢复。AppModel-Runtime 事件 ID 215/208 与 shell infrastructure 相关，已持续 4 个月仍未能关闭。

**4. 无法从 Max 5x 升级到 Max 20x，支付持续失败** — #56281
评论 21 · 👍 8 · [链接](https://github.com/anthropics/claude-code/issues/56281)
用户多次尝试升级付费套餐时支付环节全部失败，且官方支持渠道无响应。该问题直接影响付费用户的权益，社区关注度高。

**5. macOS 桌面版会话切换产生大量无用会话** — #90798
评论 1 · 👍 0 · [链接](https://github.com/anthropics/claude-code/issues/90798)
新提交的 issue，反映桌面端在并行会话间切换时，`WarmLifecycle` 预暖机制每次都会生成一个永不被使用的 CLI 会话。4 周内累积 950 个无用会话，不仅污染 `claude_code.session.count` 指标，还在 `~/.claude/projects` 下产生大量垃圾文件。数据很惊人，说明桌面版会话架构存在系统性缺陷。

**6. 远程控制（Remote Control）被默认开启** — #88094
评论 7 · 👍 9 · [链接](https://github.com/anthropics/claude-code/issues/88094)
Windows TUI 中远程控制功能在没有用户授权的情况下默认打开，引发隐私与安全担忧。社区认为该功能应默认为关闭状态。

**7. 计划任务被错误地按交互式权限执行** — #89632
评论 5 · 👍 0 · [链接](https://github.com/anthropics/claude-code/issues/89632)
本地计划任务机制明明以“无人值守”为前提（harness 会注入 `<scheduled-task>` 包装器），却依然走 ask-every-tool 交互式权限流程，与任务的非交互定位直接矛盾，需要修复。

**8. WezTerm 下 shift+/ 输入错误（2.1.247 回归）** — #90067
评论 3 · 👍 5 · [链接](https://github.com/anthropics/claude-code/issues/90067)
自 2.1.247 起，WezTerm 中按下 `shift+/` 输出 `/` 而非 `?`。开发者定位到 2.1.247 开始请求 kitty keyboard flags 5（此前为 1），flag 4 可能开启了某些增强模式，导致修饰键事件处理异常。同样的回归还存在于其他终端场景。

**9. 桌面版斜杠命令菜单回归** — #89771
评论 2 · 👍 1 · [链接](https://github.com/anthropics/claude-code/issues/89771)
在桌面应用中，`/` 现在只能作为输入的首字符才能触发斜杠命令菜单，在长句中间输入 `/` 不再弹出 skills/命令建议。`@` 提及功能未受影响，但仍是一个明显的交互回归。

**10. 插件安装后“Failed to update marketplace”** — #86428
评论 3 · 👍 0 · [链接](https://github.com/anthropics/claude-code/issues/86428)
macOS 桌面版通过远程/账户级路径安装的插件，在刷新时因 CLI 缺少本地 marketplace 记录而失败。桌面版与 CLI 之间的插件状态不同步问题，影响插件生态的可用性。

---

### 重要 PR 进展

**#35350：插件脚本使用可移植 shebang**（已关闭）
作者 @letanure · 更新于 2026-08-30 · [链接](https://github.com/anthropics/claude-code/pull/35350)

该 PR 将 11 个插件 shell 脚本中的 `#!/bin/bash` 改为 `#!/usr/bin/env bash`，以兼容 bash 不在 `/bin/bash` 的系统（如 NixOS）。此前已有部分脚本使用了可移植写法，本次是对剩余脚本的统一修复。PR 目前已关闭（可能被合并或 superseded），但它所指向的问题——插件钩子在非标准 bash 路径下失败——仍然是 NixOS 等用户实际会遇到的痛点，之前 #11029 中已经部分修复过。

---

### 功能需求趋势

| 方向 | 关注度 | 代表性 Issue |
|------|--------|-------------|
| **Windows 桌面版稳定性修复** | 极高 | #80444（GPU 崩溃）、#53247（启动失败）、#85891（窗口置顶） |
| **安全过滤器误报率** | 高 | 21 个 #744xx 系列 AUP/Cyber 误报（已标记 stale，但暴露了误报导致会话中断的严重问题） |
| **终端兼容性** | 中高 | #90067（WezTerm 回归）、#79025（Windows 终端渲染腐蚀） |
| **会话/生命周期管理** | 中 | #90798（无用会话膨胀）、#89632（计划任务权限模型缺陷） |
| **插件系统完善** | 中 | #86428（插件 marketplace 不同步）、#35350（shebang 可移植性） |
| **账号与令牌可观测性** | 低 | #90298（无法验证 setup-token 作用域） |
| **升级/支付流程** | 中 | #56281（Max 升级支付失败） |

社区最集中的诉求是 **Windows 平台的基础体验修复**。相比之下，新功能请求较少，当前阶段用户更希望官方优先填补稳定性和兼容性缺口。

---

### 开发者关注点

- **Windows 问题集中爆发：** 从 GPU 崩溃到窗口置顶，再到启动失败和渲染腐蚀，Windows 平台已出现多个长期未解决的高热度 bug，成为社区最主要的负面声音来源。
- **安全误报的最大痛点是“主观表达被误判”：** #744xx 系列中，用户在输入“frustrated exclamation”（如一句抱怨）后被安全过滤器中断正常的授权任务。虽然这些 issue 已被标记为 stale/closed，但 21 个同类 issue 说明误报不是偶发，而是系统性缺陷。
- **回归问题频发：** 2.1.247 引入 WezTerm 键盘输入回归；桌面版斜杠命令菜单也出现行为回归。开发者对每次更新都引入新 bug 感到疲惫，呼吁建立更完善的回归测试。
- **支付与升级链路体验差：** Max 5x → Max 20x 升级支付持续失败且支持无响应，直接影响付费用户，长期不解决将损害产品口碑。
- **会话与权限模型的隐形成本：** macOS 桌面版 4 周产生 950 个无用会话、计划任务按交互式权限执行，都是架构层面的设计问题，短期内可能不会被普通用户感知，但会造成数据污染和资源浪费。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-31

## 今日速览

昨日社区讨论热度集中于 **Windows 平台稳定性**与**远程控制/沙箱安全边界**两大主题：多个 Windows 专属 bug（DWM 性能、WSL 项目失败、握手崩溃）持续发酵，同时 `approval_policy` 移除引发的安全讨论获得 34 个 👍。PR 侧则密集合并了 **MCP 名称规范、Vim 键位增强、Guardian 授权持久化**等 10 项改进，并发布了 `rust-v0.152.0-alpha.4` 预发布版本。

---

## 版本发布

### rust-v0.152.0-alpha.4
- **发布内容**：`0.152.0-alpha.4` 预发布版本（发布说明仅标注版本号，无详细变更日志）。
- **建议**：关注 Rust 工具链的开发者可升级测试，但建议等待正式版说明或 changelog 补充后再用于生产环境。

---

## 社区热点 Issues（最值得关注的 10 个）

### 1. code-mode 主机握手失败，5.6 模型无法正常工作
- **Issue**: [#41049](https://github.com/openai/codex/issues/41049)
- **作者**: @yanweichao123 | ⭐ 1 | 💬 37
- **摘要**: Windows 10 上 Codex App（26.820.71523）本地命令执行通道握手阶段异常退出（code-mode host exited during handshake），导致目录无法自动读取，5.6 模型交互故障。
- **重要性**: 影响核心模型可用性，评论数高居榜首，属阻断性 bug。

---

### 2. Windows 独立更新继承 PSModulePath 导致 Get-FileHash 失败
- **Issue**: [#27117](https://github.com/openai/codex/issues/27117)
- **作者**: @BlueOcean223 | ⭐ 18 | 💬 25
- **摘要**: CLI 从 pwsh 启动时更新动作错误地启动 powershell.exe，子进程继承 pwsh 的 PSModulePath，导致 Get-FileHash 执行失败。
- **重要性**: 高赞（18 👍）的更新管道缺陷，影响 Windows 用户升级体验。

---

### 3. Windows Computer Use 在 EnumWindows 处失败（0x80070003）
- **Issue**: [#37043](https://github.com/openai/codex/issues/37043)
- **作者**: @Moonst | ⭐ 4 | 💬 19
- **摘要**: 内置 Computer Use 辅助程序启动成功，但 `sky.list_apps()` 和 `sky.list_windows()` 立即报 "路径不存在"（0x80070003），重启无效。
- **重要性**: Computer Use 功能在 Windows 上完全不可用，涉及系统 API 调用路径问题。

---

### 4. approval_policy="untrusted" 被无弃用移除，削弱执行审批边界
- **Issue**: [#39973](https://github.com/openai/codex/issues/39973)
- **作者**: @eambrosyupgrade | ⭐ 34 | 💬 12
- **摘要**: 0.149.0 起直接拒绝包含 `approval_policy = "untrusted"` 的配置，用户被要求移除该设置，但移除后无法保留原有的无审批执行策略。
- **重要性**: **今日最高赞 Issue（34 👍）**，社区对安全策略变更的透明度与兼容性强烈不满。

---

### 5. 远程控制无法附加到工作站进行中的 CLI 会话
- **Issue**: [#37967](https://github.com/openai/codex/issues/37967)
- **作者**: @VIKI623 | ⭐ 17 | 💬 12
- **摘要**: 已完成的线程可查看，但在进行中的 CLI 任务无法通过手机端 Remote Control 附加。用户期望"工作站主导 + 手机监控/审批"的正常工作流。
- **重要性**: 高赞（17 👍）功能缺口，Remote Control 在真实工作场景中的核心交互方式未被支持。

---

### 6. Windows 10 DWM Composition 句柄在 Codex 工具调用后累积
- **Issue**: [#33192](https://github.com/openai/codex/issues/33192)
- **作者**: @J-ShuJie | ⭐ 10 | 💬 17
- **摘要**: 终端工具调用场景下 DWM 的 Composition 句柄数增长（5 次调用 +22），无工具任务无增长，疑似句柄泄漏。
- **重要性**: 高赞（10 👍）性能问题，可能引发系统级图形资源耗尽。

---

### 7. Windows 远程：每个新无项目聊天都因路径格式错误无法通过信任验证
- **Issue**: [#39855](https://github.com/openai/codex/issues/39855)
- **作者**: @searchadvert | ⭐ 9 | 💬 18
- **摘要**: Windows Store 版 Codex（26.818.3698.0）发起的新无项目聊天全部失败，报 malformed path，无法完成 trust verification。
- **重要性**: 远程功能在 Windows 上完全不可用，影响所有无项目远程用户。

---

### 8. [Windows][WSL] 切换 Agent 环境到 WSL 后项目创建和删除失败
- **Issue**: [#41290](https://github.com/openai/codex/issues/41290)
- **作者**: @W4yneChen | ⭐ 6 | 💬 16
- **摘要**: Codex App 26.825.31414 在切换 Agent Environment 为 WSL 后，项目创建/移除操作全部失败。
- **重要性**: WSL 集成出现回归，Windows 开发者核心工作流受影响。

---

### 9. 请求增加 PreSkillUse / PostSkillUse 钩子
- **Issue**: [#17132](https://github.com/openai/codex/issues/17132)
- **作者**: @blairhudson | ⭐ 11 | 💬 4
- **摘要**: 建议为显式/隐式的技能调用增加生命周期钩子，便于外部系统感知和干预技能执行。
- **重要性**: 高赞（11 👍）功能增强提案，反映社区对技能系统的可扩展性需求。

---

### 10. Chrome 插件/浏览器/Computer Use 拒绝与某些站点交互
- **Issue**: [#29343](https://github.com/openai/codex/issues/29343)
- **作者**: @joshp123 | ⭐ 5 | 💬 19
- **摘要**: Codex 通过 Chrome 插件访问某些网站时被静默拒绝，没有给出原因，也无替代方案。
- **重要性**: 安全策略执行的可见性问题，用户无法区分"功能限制"与"错误"。

---

## 重要 PR 进展（10 项）

### 1. 在 Turn 元数据中标记历史记录摄取请求
- **PR**: [#41743](https://github.com/openai/codex/pull/41743)
- **状态**: 已关闭 | 作者: @copyberry[bot]
- **内容**: 启用 history-notes token-budget 扩展时，在 Responses turn 元数据中标记 `history_ingest_requested=true`，并保留核心元数据键防止调用方覆盖。
- **影响**: 增强历史记录注入的可观测性与安全性。

---

### 2. 在 TUI 中显示可操作的速率限制横幅
- **PR**: [#41742](https://github.com/openai/codex/pull/41742)
- **状态**: 已关闭 | 作者: @copyberry[bot]
- **内容**: 通过 `account/rateLimits/read` 传递后端横幅与账户身份数据，并过滤非当前认证账户的消息，在 composer 上方渲染速率限制通知。
- **影响**: 改善用户在限流时的知情度和操作指引。

---

### 3. 支持包样式的 MCP 服务器名称
- **PR**: [#41700](https://github.com/openai/codex/pull/41700)
- **状态**: 已关闭 | 作者: @copyberry[bot]
- **内容**: 允许 MCP 服务器名称包含 `:`、`@`、`/`、`.` 等字符，支持类似 `npm:@modelcontextprotocol/server-sequential.thinking` 的命名。
- **影响**: 扩展 MCP 生态兼容性，对齐 npm 等包管理器的命名规范。

---

### 4. 为环境型 MCP 测试设置工作目录
- **PR**: [#41683](https://github.com/openai/codex/pull/41683)
- **状态**: 已关闭 | 作者: @copyberry[bot]
- **内容**: 环境型 stdio MCP server 没有 host-local 工作目录回退机制，测试 fixture 需显式提供 workspace 作为 `cwd`。
- **影响**: 修复环境型 MCP server 的测试可靠性。

---

### 5. 修复旧版 JediTerm 终端的光标样式渲染
- **PR**: [#41673](https://github.com/openai/codex/pull/41673)
- **状态**: 已关闭 | 作者: @copyberry[bot]
- **内容**: 旧版 JediTerm 可能在 `DECSCUSR` 中打印空格中间字符，覆盖光标样式命令下方的字形。改为在终端拥有的可修复字形上应用光标样式并重绘。
- **影响**: 提升旧版终端模拟器下的显示兼容性。

---

### 6. 首个 Node REPL 执行无需等待 Guardian 即可批准
- **PR**: [#41666](https://github.com/openai/codex/pull/41666)
- **状态**: 已关闭 | 作者: @copyberry[bot]
- **内容**: Node REPL 服务器的首次 `js` 执行在异步 Guardian 分类仍在进行时即可快速批准。
- **影响**: 降低 Node REPL 交互延迟，同时保持异步安全审查。

---

### 7. 跨历史压缩保留 Guardian 授权
- **PR**: [#41660](https://github.com/openai/codex/pull/41660)
- **状态**: 已关闭 | 作者: @copyberry[bot]
- **内容**: 历史压缩和 host 注入上下文会重写用户已授权的对话内容，但不应视为授权变更，避免 Guardian 要求重新审查。
- **影响**: 修复长会话压缩后 Guard 误判授权失效的问题。

---

### 8. 更新默认启用 update_plan 的测试
- **PR**: [#41630](https://github.com/openai/codex/pull/41630)
- **状态**: 已关闭 | 作者: @copyberry[bot]
- **内容**: 覆盖 `tools.update_plan.enabled` 的默认、显式启用、显式禁用三种状态，并验证自定义 base/developer 指令下的 prompt 工具列表一致性。
- **影响**: 为 update_plan 默认启用行为提供测试保障。

---

### 9. 将 Vim 历史测试移入历史搜索模块
- **PR**: [#41613](https://github.com/openai/codex/pull/41613)
- **状态**: 已关闭 | 作者: @copyberry[bot]
- **内容**: 将 Vim 历史导航测试与历史搜索实现放在一起，复用人类打字风格的测试辅助函数。
- **影响**: 代码结构整理，提升可维护性。

---

### 10. 为 composer 添加 Vim 搜索动作
- **PR**: [#41586](https://github.com/openai/codex/pull/41586)
- **状态**: 已关闭 | 作者: @copyberry[bot]
- **内容**: 在 draft 本地支持 `/` 和 `?` 正向/反向字面搜索，支持 `n`/`N` 循环跳转，并支持在 delete/change/yank 操作符后使用搜索动作。
- **影响**: 完善 Vim 模式体验，向完整 Vim 键位集迈进。

---

## 功能需求趋势

从本期 50 条活跃 Issue 中提炼出的社区核心诉求：

| 方向

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期**: 2026-08-31  
**数据来源**: [github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)


## 1. 今日速览

今日社区讨论焦点集中在 **Agent 稳定性与可靠性** 上：Subagent 在达到 MAX_TURNS 后误报 GOAL 成功（#22323）及通用 Agent 无故挂起（#21409）位居讨论热度前列，且均已进入 maintainer 的 retesting 流程。社区贡献活跃，多个高质量 PR 围绕核心体验修复（stdin 恢复、CRLF 行尾处理、认证流程改进）推进中；同时 Dependabot 提交了包含 77 个依赖包的大规模更新，值得关注。

## 2. 版本发布

**v0.59.0-nightly.20260830.g0bd1d4397** — 最新 nightly 版本，包含自上一个 nightly 以来的常规更新，具体变更内容可查看 [Full Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.59.0-nightly.20260829.g0bd1d4397...v0.59.0-nightly.20260830.g0bd1d4397)。

## 3. 社区热点 Issues

### #22323 Subagent 达到 MAX_TURNS 后误报 GOAL 成功（最热，13 条评论）
**优先级 p1 ｜ Bug ｜ 需重新测试**
`codebase_investigator` 子代理实际已触发最大轮次限制，但报告状态为 `success`、终止原因为 `GOAL`，导致主会话对中断情况浑然不知。社区已积累大量关注，维护者已标记为 need-retesting。
🔗 https://github.com/google-gemini/gemini-cli/issues/22323

### #21409 通用 Agent 无限挂起（8 条评论）
**优先级 p1 ｜ Bug**
当 Gemini CLI 将任务委派给 generalist agent 时，连简单操作（如创建文件夹）也会永久挂起，最长等待 1 小时后被用户手动取消。显式指示模型不要使用子代理可绕过此问题。
🔗 https://github.com/google-gemini/gemini-cli/issues/21409

### #19873 利用模型 bash 亲和性：零依赖 OS 沙箱与意图路由（8 条评论）
**优先级 p2 ｜ Enhancement ｜ 大工作量**
提出让 Gemini 3 模型以原生 bash 用户方式工作（grep/cat/sed/awk），通过零依赖沙箱与执行后意图路由，兼顾模型能力与用户安全。
🔗 https://github.com/google-gemini/gemini-cli/issues/19873

### #22745 AST 感知的文件读取/搜索/代码库映射评估（7 条评论）
**优先级 p2 ｜ Feature ｜ 用户问题**
EPIC 级 Issue，跟踪一系列调查以评估 AST 感知工具的价值——可精确定位方法边界、减少 token 噪声、提升代码导航效率。这是 #22746 的上游关联 Issue。
🔗 https://github.com/google-gemini/gemini-cli/issues/22745

### #21968 Gemini 不会主动使用 skills 和 sub-agents（6 条评论）
**优先级 p2 ｜ Bug**
用户反馈 Gemini CLI 几乎从不主动使用自定义 skills 和子代理，即使已有 "gradle" 和 "git" 等带明确描述的 skill，仍需手动显式指示。
🔗 https://github.com/google-gemini/gemini-cli/issues/21968

### #25166 Shell 命令执行完毕但卡在 “Waiting input”（4 条评论）
**优先级 p1 ｜ Bug ｜ 中等工作量**
极简单的 CLI 命令执行完成后，Gemini CLI 仍显示命令为 active 状态并卡在 "Awaiting user input"。与终端交互机制相关的核心稳定性问题。
🔗 https://github.com/google-gemini/gemini-cli/issues/25166

### #26525 确定性脱敏与 Auto Memory 日志量削减（5 条评论）
**优先级 p2 ｜ Security ｜ Bug**
Auto Memory 在将转录内容送入后台提取模型之后才执行脱敏提示词，存在敏感信息暴露窗口；且服务会记录已有技能内容等日志，存在安全隐患。
🔗 https://github.com/google-gemini/gemini-cli/issues/26525

### #22232 browser_agent 韧性增强：自动会话接管与锁恢复（4 条评论）
**优先级 p3 ｜ Feature ｜ 用户问题**
`BrowserManager.ts` 当前采用 "fail-fast" 策略，遇到浏览器 profile 被锁（如 persistent 模式下的孤儿进程）时直接失败，期望实现自动恢复机制。
🔗 https://github.com/google-gemini/gemini-cli/issues/22232

### #21983 Wayland 环境下 browser 子代理失败（4 条评论）
**优先级 p1 ｜ Bug ｜ 需重新测试**
Browser Agent 在 Wayland 显示服务器下无法正常工作，终止原因显示为 GOAL。桌面端用户（尤其是 Linux）受影响面较广。
🔗 https://github.com/google-gemini/gemini-cli/issues/21983

### #22672 Agent 应主动阻止/劝阻破坏性行为（3 条评论）
**优先级 p2 ｜ Feature ｜ 用户问题**
模型在复杂 git 操作、数据库维护等场景下可能使用 `git reset`、`--force` 等破坏性命令，社区建议 Agent 应具备危险操作识别与劝阻能力。
🔗 https://github.com/google-gemini/gemini-cli/issues/22672

### 补充关注：#24246 超过 400 个工具导致 400 错误（3 条评论）
**优先级 p2 ｜ Bug**
当可用工具超过 400 个时 Gemini CLI 直接报 400 错误，社区期望 Agent 能更智能地按需裁剪工具范围。
🔗 https://github.com/google-gemini/gemini-cli/issues/24246

## 4. 重要 PR 进展

### #29137 Dependabot 批量升级：77 个 npm 依赖包（XL，Open）
包含 simple-git（3.28.0 → 3.36.0）、@modelcontextprotocol/sdk 等 76 项更新，一次性大版本刷进，合并前需重点关注 breaking changes。
🔗 https://github.com/google-gemini/gemini-cli/pull/29137

### #28889 修复：能力检测后恢复暂停的 stdin（p1, M, Open）
`sylvesterkaczmarek` 修复 `detectCapabilities()` 临时挂载 data listener 后未恢复 stdin 流状态的问题，并为两种流状态补充了回归测试。解决 #28799。
🔗 https://github.com/google-gemini/gemini-cli/pull/28889

### #29132 修复：diff 上下文片段的行尾规范化（Core, S, Open）
针对 CRLF/CR 文件导致 diff 上下文把整个文件灌回模型上下文的问题，新增回归测试覆盖单行变更的 CRLF 文件场景。修复 #29130。
🔗 https://github.com/google-gemini/gemini-cli/pull/29132

### #29110 修复：read_file 内容路由到 FileSystemService（Agent, M/L, Open）
`Abdullah-Builds` 发现 `read_file` 绕过注入的 `FileSystemService` 直接读本地磁盘，与 `write_file`/`replace` 的行为不一致。修复后 ACP 客户端可正确拦截读取操作。
🔗 https://github.com/google-gemini/gemini-cli/pull/29110

### #28960 修复：移除 Antigravity URL 末尾句点（p1, M, Open）
认证流程中展示的 Antigravity URL 因带尾随句点导致用户复制后访问失败，`jeelsoni01` 提交修复。
🔗 https://github.com/google-gemini/gemini-cli/pull/28960

### #28967 修复：静态刷新时清除终端回滚缓冲区（p2, S, Open）
在非 alternate buffer 模式下，`refreshStatic()` 调用 `clearTerminal` 导致 Linux 终端（GNOME Terminal、Alacritty、Konsole 等）的回滚历史被异常清空。修复 #28954。
🔗 https://github.com/google-gemini/gemini-cli/pull/28967

### #29125 修复：hooks 迁移中超时单位换算错误（p2, S, Open）
Claude Code 的 hook 超时以秒为单位（默认 60），Gemini CLI 按毫秒解释，迁移时原样复制导致超时设置失效。修复 #29122。
🔗 https://github.com/google-gemini/gemini-cli/pull/29125

### #29124 修复：SubagentStop 事件键拼写错误（p2, XS, Open）
Claude Code 的 hook 事件拼写为 `SubagentStop`（小写 a），迁移映射表中误写为 `SubAgentStop`，导致该 hook 迁移时被静默丢弃。修复 #29123。
🔗 https://github.com/google-gemini/gemini-cli/pull/29124

### #28827 修复：避免 401 子字符串被误判为认证失败（p2, S, Closed）
某些场景下端口号、退出码等包含 "401" 的内容被 `isAuthenticationError` 误判为认证错误。修复 #28203 并补充了拒绝端口/退出码等场景的回归测试。
🔗 https://github.com/google-gemini/gemini-cli/pull/28827

### #28828 修复：预览模型被静默替换时给出警告（p1/p2, M, Closed）
当请求的预览模型（如 gemini-3.1-pro-preview）无 entitlements 时，Config 会静默回退到 `auto-gemini-2.5` 且无任何提示。该 PR 增加警告机制。修复 #28825。
🔗 https://github.com/google-gemini/gemini-cli/pull/28828

## 5. 功能需求趋势

从今日 Issues 与 PR 中提炼出四个最受关注的方向：

1. **Agent 可靠性与稳定性（最核心）**：Subagent 误报成功、Generalist Agent 挂起、Shell 命令卡死、browser 在 Wayland 下失败——这些问题占据了 p1/p2 优先级的大头，说明社区的当务之急是让 Agent **先稳定起来**。
2. **安全机制强化**：Auto Memory 的脱敏时点（#26525）、工作区信任与 mcpServers 进程执行限制（#29099）、破坏性命令劝阻（#22672），安全场景从“功能需求”上升为“用户痛点”，尤其是企业环境。
3. **上下文效率优化**：AST 感知工具（#22745）、Tactful Extraction 策略（#19561）、默认 36.6k tokens 的上下文基线控制，社区持续探索**更少 Token、更多有效信息**的文件读取方式。
4. **工具生态与迁移兼容性**：hooks 迁移的单位/键名修正（#29125、#29124）、模型超过 400 个工具时的降级策略（#24246），反映出用户将 Gemini CLI 接入现有工作流中的真实接入摩擦。

## 6. 开发者关注点

### 高频痛点

- **子代理行为不可控**：达到轮次上限却报告成功、挂起无响应、不主动使用 skills——模型委派机制的透明度和健壮性不足，开发者无法信任后台任务结果。
- **终端交互状态丢失**：命令卡在 “Waiting input”、stdin 流状态未恢复、终端回滚被意外清除——这些交互层 Bug 直接破坏日常使用体验，且复现率较高。
- **环境适配参差**：Wayland 下的 browser agent、Cloud Workstations 中的 OAuth 回环、Windows/CRLF 行尾处理——跨平台与远程开发场景的适配仍是短板。

### 社区贡献方向

今日有价值的社区 PR 集中在 **核心体验微修复**（stdin、diff、URL 显示），由独立贡献者密集提交，同时有三条 PR 被直接关闭并标记 `status/need-issue`——建议贡献者在提交前务必先关联 Issue，提高合并效率。

### 维护者动态

多个 p1/p2 bug 已标记 `status/need-retesting`（#22323、#21409、#21983、#22267），说明维护者正在集中收敛 Agent 稳定性问题；同时 `workstream-rollup` 标签持续聚合长线工作，建议关注这些 Issue 的后续 retest 结果。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-08-31）

## 1. 今日速览

过去 24 小时内，Kimi Code CLI 无新版本发布，也无 PR 合并或更新。社区动态集中在两个新报告的 Issue 上：一是 `k3-256k` 模型在 0.39.1 中出现工具调用类型错乱（文本显示 Write，实际发送 Read）；二是 Remote Control 功能在 iPadOS 16.6 的 Safari/微信中无法正常启动登录。两者分别指向当前版本中**模型工具调用可靠性**与**远程控制跨端兼容性**两个核心问题。

## 2. 版本发布

无新版本发布。

## 3. 社区热点 Issues

> 过去 24 小时内仅更新 2 个 Issue，且均为新创建、暂无评论。以下全部列出。

### #2628 Model emits Read tool calls instead of Write/Edit — text says 'calling Write', wire shows Read (0.39.1, k3-256k)

- **作者**: @776138506
- **状态**: Open
- **评论/点赞**: 0 / 0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2628
- **为什么重要**: 该问题直指模型代码编辑场景下的工具调用准确性。用户使用 `kimi-code/k3-256k` 模型时，UI 日志显示“调用 Write”，但实际网络请求中发送的却是 `Read` 工具。这种文本行为与实际行为不一致会严重干扰开发者对自动化的信任，可能导致误判文件内容、执行错误操作。
- **社区反应**: 暂无评论，但属于工具调用核心正确性问题，预计会引发较高关注。

### #2627 [Bug] Remote Control login fails to start on iPadOS 16.6 (Safari/WeChat) — “无法开始登录” at code-rc.kimi.com

- **作者**: @VBS-you
- **状态**: Open
- **评论/点赞**: 0 / 0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2627
- **为什么重要**: Remote Control 是 Kimi Code CLI 的远程控制特性，该问题表明其在 iOS 生态中存在兼容性缺陷。用户环境为 Debian 12 服务器 + 0.39.1 客户端，通过 iPadOS 16.6 访问 `code-rc.kimi.com` 登录时失败。涉及浏览器兼容性（Safari / 微信内置浏览器），会影响移动端远程办公场景。
- **社区反应**: 暂无评论，但该问题涉及具体平台版本，属于典型的兼容性反馈。

## 4. 重要 PR 进展

过去 24 小时内无 PR 创建或更新。

## 5. 功能需求趋势

结合当前可见的有限 Issue，社区关注点主要集中在以下方向：

- **工具调用行为一致性**：模型在代码编辑任务中必须正确区分 Read / Write / Edit 等工具，不能仅靠日志文本。用户对实际 wire 层行为保持高度敏感。
- **远程控制的跨端支持**：除桌面浏览器外，开发者希望 Remote Control 在 iPadOS、移动端 H5 等环境同样可用。
- **老版本系统兼容性**：iPadOS 16.6 仍有一定用户基础，要求 CLI 的 Web 控制台具备更宽容的前端兼容策略。

## 6. 开发者关注点

- **工具调用的真实性与可观测性**：开发者不仅关注模型生成结果，还关注 CLI 实际下发的工具指令链。当 UI 文案与实际 wire 数据不一致时，会直接动摇对 CLI 自动化流程的信任。
- **远程控制登录失败阻塞工作流**：Remote Control 登录失败是硬阻塞，用户无法进入远程操作界面。尤其在使用非最新系统或特定浏览器时，缺少降级或明确错误提示。
- **OAuth 订阅模式下的稳定体验**：两个 Issue 均来自使用 Kimi Code 订阅 + OAuth 登录的用户，反映出官方托管供应商模式下，用户对故障的容忍度较低，期望快速修复。

---

*数据来源：github.com/MoonshotAI/kimi-cli（更新于 2026-08-30）*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报（2026-08-31）

## 今日速览

昨日社区讨论热度集中在**数据库无界增长**（#33356，opencode.db 达 13GB+）与**订阅计费状态不一致**（#37790，Go 订阅扣款成功但显示余额不足）两大问题上，均获得大量开发者共鸣。此外，插件系统 API 演进（typed RPC、原生权限审批）与 shell 进程生命周期修复成为 PR 侧最活跃的方向。

## 版本发布

过去 24 小时无新版本发布。

## 社区热点 Issues

### 1. event 表无界增长，opencode.db 达 13GB+（#33356）
数据库在长期运行实例上无任何保留/压缩策略，`message.updated.1` 快照占满磁盘（22GB 卷标满至 97-99%）。25 条评论、8 个 👍，是当前社区最关注的存储/性能问题。多条评论补充了各自实例的膨胀数据，社区希望官方提供清理策略或自动压缩工具。  
🔗 https://github.com/anomalyco/opencode/issues/33356

### 2. Go 订阅扣款成功但工作区显示 “Insufficient balance”（#37790）
Stripe 扣款成功，但 OpenCode Go 工作区仍报余额不足，用户无法使用已购服务。17 条评论，属于高频计费类故障。评论显示这不是孤例，部分用户通过等待同步或重新登录临时恢复，但根因未明。  
🔗 https://github.com/anomalyco/opencode/issues/37790

### 3. 连续正常扣款 3 个月后支付突然被拒（#45278）
同张卡正常支付三个月，突然被拒；银行确认卡片无问题。8 条评论，1 个 👍。评论区多位用户反馈相似经历，猜测与订阅续期策略或 Stripe 元数据异常有关。  
🔗 https://github.com/anomalyco/opencode/issues/45278

### 4. 无法删除 Zen 账户（#18016）
用户反馈 Zen 账户无法自助删除，且会持续扣费、邮件联系无回应。7 条评论、7 个 👍（👍/评论比最高），属于影响信任度的严重问题。评论区推测是 Zen 侧账户系统缺少删除入口，希望 OpenCode 提供代删通道。  
🔗 https://github.com/anomalyco/opencode/issues/18016

### 5. 自定义模型连接持续报 ECONNRESET（#46088）
新会话能启动，但读取几个文件后必现 ECONNRESET；上下文配置 200K tokens，实际读取远未达上限。7 条评论，0 👍。从描述看问题与文件读取触发的并发或流式中断有关，可能涉及自定义 provider 的 HTTP 连接池管理。  
🔗 https://github.com/anomalyco/opencode/issues/46088

### 6. mimo-v2.5 请求报 HTTP 400（#45990）
用户使用 OpenCode Go 搭配 Hermes 中途无配置变更，突然出现 HTTP 400。7 条评论、3 个 👍。评论中有人怀疑是新模型变体参数与 Anthropic 协议不兼容所致（与 #46314 的 effort 字段丢失可能同源）。  
🔗 https://github.com/anomalyco/opencode/issues/45990

### 7. 会话永久卡死、重启无法恢复（#43277）
多个会话在使用中永久卡死，拒绝新消息，重启服务和系统均无法恢复。6 条评论，0 👍。评论区建议检查 event 表损坏或会话状态机死锁，有开发者已开始自建脚本清理卡死会话。  
🔗 https://github.com/anomalyco/opencode/issues/43277

### 8. 旧版插件加载器将非 Hooks 返回值混入 hooks 数组（#42451）
1.16.2 的 `getLegacyPlugins` 会调用插件模块导出的每个函数，并把返回值无验证地 push 进 hooks 数组。若插件导出辅助函数（非 Hooks 对象），启动即崩溃。6 条评论、0 👍，是插件生态兼容性的重要隐患。  
🔗 https://github.com/anomalyco/opencode/issues/42451

### 9. task 工具报 “no such column: replacement_seq”（#35403）
CLI 已应用 38 个迁移，而 `__drizzle_migrations` 表只追踪了 21 个，导致 sub-agent 崩溃。5 条评论、3 个 👍，是当前数据库迁移不一致类问题的代表案例，社区呼吁提供一键迁移修复命令。  
🔗 https://github.com/anomalyco/opencode/issues/35403

### 10. Go 用量 100% 后不启用 Zen 余额兜底（#42938）
Go 月度用量打满后阻塞 “Big Pickle” 12 小时；控制台已开启 “Use balance”，Zen 余额 $39.89 却始终不被使用。5 条评论、0 👍。与 #37790 同属计费/配额一致性问题，影响订阅用户体验。  
🔗 https://github.com/anomalyco/opencode/issues/42938

## 重要 PR 进展

### 1. fix(core): 修复 bash 在进程退出后挂起（#42756）
一次关闭 7 个相关 issue（#20902、#25038、#28697、#36342、#37838、#42044、#42524）。修复 process `exit` 后 bash 未正常结束的问题，是 shell 稳定性关键补丁。  
🔗 https://github.com/anomalyco/opencode/pull/42756

### 2. feat(plugin): 增加 typed RPC 和自定义事件（#46105）
为插件系统引入执行无关的 RPC 契约：类型化输入输出、声明式错误和自定义事件。Promise 和 Effect 插件均可使用。这是插件系统向正式协议演进的重要一步。  
🔗 https://github.com/anomalyco/opencode/pull/46105

### 3. fix(shell): 限制 Windows 进程退出后的管道排空（#46085）
解决 Windows 下 `bunx agent-browser`、`dotnet build/test` 等长生命周期子进程退出后 stdout/stderr 句柄未关闭导致 shell 无法完成的问题。  
🔗 https://github.com/anomalyco/opencode/pull/46085

### 4. fix(core): 限制会话 shell 输出为 50 KiB 预览（#45136）
会话内 shell 命令输出与常规 shell 一样仅保留 50 KiB 预览，大输出改为文件存储，防止 TUI 卡顿/内存膨胀。  
🔗 https://github.com/anomalyco/opencode/pull/45136

### 5. fix(opencode): 终止本地 MCP 进程树（#46312）
修复本地 stdio MCP 启动器在断开或替换后遗留后代进程的问题，关闭 #46253，关联 #46035。对长时间运行 OpenCode 的用户是重要修复。  
🔗 https://github.com/anomalyco/opencode/pull/46312

### 6. feat(app): “Open in” 菜单增加 VS Code Insiders 和 Antigravity（#40872）
在会话头部 “Open in” 下拉菜单中补充两个常用的外部编辑器选项，属于低风险 QoL 改进。  
🔗 https://github.com/anomalyco/opencode/pull/40872

### 7. fix(opencode): debug info 中 file:// 插件路径只显示 basename（#40301）
`opencode debug info` 将本地自动发现插件从完整 `file:///C:/Users/...` 改为文件名，提升可读性；关闭 #40300。  
🔗 https://github.com/anomalyco/opencode/pull/40301

### 8. fix(app): 修复无项目打开时 New Session 和项目选择器不可用（#39732）
两个小修复使 `opencode web` 在从未打开过项目的浏览器配置文件中也能正常工作；关闭 #37606、#37611。  
🔗 https://github.com/anomalyco/opencode/pull/39732

### 9. feat(tui): Ctrl+L 直接打开会话列表（#39698）
为 V2 TUI 增加 `Ctrl+L` 直接打开会话列表，原有的 `<leader>l` 仍保留作为备用绑定。社区反馈积极的体验优化。  
🔗 https://github.com/anomalyco/opencode/pull/39698

### 10. fix(plugin): 准确报告进程内 serverUrl（#39717）
默认 TUI 走进程内传输，不绑定 HTTP 监听器，但 `PluginInput.serverUrl` 此前回退到 `http://...` 造成误导；现改为准确反映进程内 server。关闭 #39561。  
🔗 https://github.com/anomalyco/opencode/pull/39717

## 功能需求趋势

- **存储与性能治理**：`event` 表无界增长（#33356）、磁盘持续扫描 80MB/s（#46256）、会话输出无上限（#45136）等表明，存储管理和资源使用上限已成为社区最关心的稳定性方向。
- **订阅/计费一致性**：多条 issue（#37790、#45278、#42938、#46252、#46255）集中在“付费后无法使用”“免费限制误报”“余额兜底不生效”上，说明计费系统体验是当前用户满意度瓶颈。
- **插件系统能力扩展**：typed RPC/自定义事件（#46105）、工具执行前请求原生权限审批（#37164）、TUI 插件插槽（#20504）显示出用户对插件生态深度的期待。
- **会话与进程生命周期**：会话永久卡死（#43277）、bash 挂起（#42756）、MCP 进程树回收（#46312）、Windows 管道排空（#46085）等指向进程/会话生命周期管理的系统性改进。
- **模型与协议兼容性**：variants 字段丢失（#42876、#46314）、mimo-v2.5 HTTP 400（#45990）、ECONNRESET（#46088）说明多 provider 协议兼容性仍是企业自部署用户的痛点。
- **Web/桌面 UI 完善**：Web UI 忽略 `default_agent`（#45873）、桌面端内联 LaTeX 不渲染（#39170）、端口占用提示含糊（#46263）、界面现代化提议（#46280）显示 UI 细节打磨需求持续存在。

## 开发者关注点

1. **数据安全与磁盘膨胀**：多用户反馈 opencode.db 在无长期维护下可达 10GB+ 且无清理入口（#33356、#35403），亟需官方提供压缩/迁移工具。
2. **付费与配额体验割裂**：“扣款了不认账”（#37790）、“免费额度误报”（#46252）、“Go 打满不自动切 Zen 余额”（#42938）等削弱用户信任。
3. **会话/进程状态不可恢复**：会话卡死且重启无效（#43277）、自定义模型 ECONNRESET 必现（#46088）是调用链上的高影响问题。
4. **模型参数静默丢失**：variants 中 body 级字段（#42876）和 reasoning effort（#46314）被计算、显示但不上送，给调试和精细化控制带来困扰。
5. **中文/西语等多语言用户反馈增加**：多条中文、西班牙语 issue（#46257、#46258、#46299）多为低质量/重复报告，但也提示非英语用户占比在上升，官方可以考虑 i18n 支持和垃圾 issue 过滤。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-31

## 今日速览

今日社区动态集中在 **Web Shell / IDE 集成** 与 **安全治理** 两大方向：安全评审暴露了命令执行配置键的开放入口风险（P1），多个 Web Shell 相关 bug（隐藏错误、diff 审批锁定）受到关注。功能需求方面，跨会话通信、Bubblewrap 沙箱、配置热加载等呼声较高。另外，昨夜 v0.22.3-nightly 发布失败，社区已自动跟踪。

---

## 社区热点 Issues

### 1. 安全：命令执行配置键是开放入口集（P1）
**#10561** — `review: command-execution config keys are an open entrance set — fsmonitor, hooks, and the user's global config`
- **重要性**：评审发现审查管线中多个 git 配置键可导致任意命令执行，属于安全类 P1 问题。攻击者可通过构造配置键，让 `git` 调用触发恶意命令。
- **社区反应**：2 条评论，评审者 `@wenshao` 将 R2-2/R2-3 合并为一条 class 级问题，认为仅新增调用点无法关闭漏洞。
- 链接：https://github.com/QwenLM/qwen-code/issues/10561

### 2. Windows 崩溃：Computer Use 驱动 0.20.0 每次运行都 panic
**#10538** — `Computer Use: driver portable 0.20.0 panics on every embedded runtime creation (Windows x64)`
- **重要性**：Windows x64 + Node v24 环境下，`@qwen-code/cua-sdk@0.20.0` 创建嵌入式运行时必现 panic，直接影响 Windows 用户使用 Computer Use 能力。
- **社区反应**：3 条评论，状态为 `need-retesting`，已附完整环境信息和本地路径。
- 链接：https://github.com/QwenLM/qwen-code/issues/10538

### 3. 功能：跨会话消息传递（in-progress）
**#8724** — `Cross-session messaging: let Qwen Code sessions on the same machine message each other`
- **重要性**：规划在 roadmap 多智能体路径上，允许同机会话间通过 `list_agents` / `send_message` 交互，状态已标为 `in-progress`，是社区关注的多智能体协作基础能力。
- **社区反应**：12 条评论，讨论含接收端 fail-closed 门控设计。
- 链接：https://github.com/QwenLM/qwen-code/issues/8724

### 4. 功能：`.worktreeinclude` 支持复制 gitignored 文件
**#10584** — `feat: Support .worktreeinclude for copying gitignored files into worktrees`
- **重要性**：来自 `@Krzysztof318`，希望在创建 Qwen Code worktree 时可自动复制 `.gitignore` 中排除的配置文件（如 `.env`、本地证书）。继承自 #4056 的 Phase D 计划。
- **社区反应**：2 条评论，当前处于开放讨论。
- 链接：https://github.com/QwenLM/qwen-code/issues/10584

### 5. 功能：Linux 原生 Bubblewrap 沙箱后端
**#10583** — `feat(sandbox): add lightweight Bubblewrap backend for Linux`
- **重要性**：为 Linux 用户提供不依赖 Docker/Podman 的轻量 OS 级隔离，降低沙箱使用门槛，安全性与易用性的平衡是社区持续关注点。
- **社区反应**：2 条评论，标注 `need-discussion`。
- 链接：https://github.com/QwenLM/qwen-code/issues/10583

### 6. 功能：模型配置热加载
**#10568** — `功能请求：模型配置热加载，无需重启 CLI`
- **重要性**：用户编辑 `settings.json` 添加新模型后需完全重启 CLI 才能生效。请求支持文件监听、`/reload-config` 命令或懒加载，并指出竞品 Qoder CLI 已支持热加载。
- **社区反应**：2 条评论，需求描述具体、可执行性强。
- 链接：https://github.com/QwenLM/qwen-code/issues/10568

### 7. Bug：Web Shell 隐藏真实错误
**#10564** — `bug(serve): Web Shell shows generic "Internal error" for failed turns, hiding the provider's actual error message`
- **重要性**：`qwen serve` 的 Web Shell 在模型提供商拒绝请求时只显示 `Internal error`，导致用户无法获知根本原因，直接影响本地调试效率。
- **社区反应**：2 条评论。
- 链接：https://github.com/QwenLM/qwen-code/issues/10564

### 8. Bug：vscode 中关闭 diff 标签导致审批行锁定
**#10557** — `vscode: closing a web-shell permission diff tab leaves the approval row locked without a re-open path`
- **重要性**：关闭只读权限 diff 标签后，审批行永久锁定且无重新打开入口，属于 WebShell 切换后的流程缺陷，影响编辑权限审批。
- **社区反应**：2 条评论，源自 PR #10534 的机器人审查线程。
- 链接：https://github.com/QwenLM/qwen-code/issues/10557

### 9. Bug：Termius 输入损坏
**#10562** — `Termius input corruption from physical cursor positioning`
- **重要性**：IME 支持引入的物理光标定位在 Termius 中导致输入行错乱（macOS 本地与 SSH 均触发），影响使用 Termius 的远程开发用户。
- **社区反应**：2 条评论。
- 链接：https://github.com/QwenLM/qwen-code/issues/10562

### 10. 运维：夜间版发布失败
**#10535** — `Release Failed for v0.22.3-nightly.20260830.413b6d15d3 on 2026-08-30`
- **重要性**：夜间版发布工作流在 `integration_none` job 失败，可能阻塞社区获取最新 nightly 功能。由 GitHub Actions 自动创建。
- **社区反应**：2 条评论，状态为 `ready-for-agent`。
- 链接：https://github.com/QwenLM/qwen-code/issues/10535

---

## 重要 PR 进展

### 1. 修复 VS Code 原生 diff 审批流程
**#10534** — `fix(vscode): restore native diff approval after WebShell cutover`
- **内容**：恢复 WebShell 工具权限切换后的 VS Code 原生 Diff 审批，Accept/Reject 命令现在能正确解析 WebShell 权限。
- **状态**：开放中，与多个后续 issue（#10557、#10585）关联。
- 链接：https://github.com/QwenLM/qwen-code/pull/10534

### 2. 修复内联 thinking 块处理
**#9607** — `fix(core): demote balanced inline thinking blocks instead of failing the turn`
- **内容**：OpenAI 兼容端点在 `content` 中发送的合法内联 thinking 块不再导致回合失败，改为降级处理。
- **状态**：开放中，已拆分出 #10559 跟踪后续。
- 链接：https://github.com/QwenLM/qwen-code/pull/9607

### 3. 网络错误自动重试
**#10347** — `feat(core): auto-retry transient network errors (EOF) where Ctrl+Y is unavailable`
- **内容**：将 4xx 包裹的底层网络失败（EOF）重分类为可重试传输错误，应用已有有界自动重试，改善无 Ctrl+Y 场景的健壮性。
- **状态**：开放中，`review/self-reported`。
- 链接：https://github.com/QwenLM/qwen-code/pull/10347

### 4. Web Shell 侧边栏工作区概览
**#10407** — `feat(web-shell): show workspace overview and a workspace menu in the sidebar`
- **内容**：工作区行显示会话统计、完整路径 tooltip，并支持展开状态下从行内管理工作区。
- **状态**：开放中。
- 链接：https://github.com/QwenLM/qwen-code/pull/10407

### 5. `/commit` 命令：AI 草拟提交信息
**#10586** — `feat(cli): add /commit slash command with AI-drafted commit messages`
- **内容**：通过 `SubmitPromptActionReturn` 注入 prompt，让模型自主收集 diff、生成提交信息并执行提交，取代原先薄封装 shell 命令的方案（对应 #4000）。
- **状态**：开放中。
- 链接：https://github.com/QwenLM/qwen-code/pull/10586

### 6. WebShell 推理偏好持久化
**#10489** — `fix(web-shell): persist model reasoning preferences`
- **内容**：复用 `model.reasoningEffort` 设置，持久化 WebShell 模型推理偏好，使 daemon 会话间保持配置。
- **状态**：开放中，`autofix/takeover`。
- 链接：https://github.com/QwenLM/qwen-code/pull/10489

### 7. Bash 权限规则保留环境前缀
**#10212** — `fix(core): preserve environment prefixes in Bash permission rules`
- **内容**：修复 `NODE_OPTIONS=... npm --version` 绕过权限匹配的问题，环境赋值前缀现成为权限身份的一部分。
- **状态**：开放中，安全相关改进。
- 链接：https://github.com/QwenLM/qwen-code/pull/10212

### 8. WebShell 脏工作树 git 更新
**#10390** — `feat(web-shell): unblock git update on dirty working tree`
- **内容**：工作区更新遇到未提交改动时，提供解析面板而非单行错误，支持 stash 或强制拉取。
- **状态**：开放中，`autofix/takeover, autofix/needs-human`。
- 链接：https://github.com/QwenLM/qwen-code/pull/10390

### 9. 输出样式选择
**#10283** — `feat(cli): select an output style via general.outputStyle or --output-style`
- **内容**：为 #9565 的输出样式增加 `general.outputStyle` 配置与 `--output-style` 标志，支持大小写不敏感解析。
- **状态**：

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*