# AI CLI 工具社区动态日报 2026-08-26

> 生成时间: 2026-08-25 22:49 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告

**日期：2026-08-26｜数据来源：各工具 GitHub 仓库社区动态**

---

## 1. 生态全景

当前 AI CLI 工具正处于「功能竞赛」与「信任危机」并存的窗口期。各主流工具均在快速迭代，但社区反馈的重心已从「能否完成任务」转向「执行结果是否可信、过程是否可控，以及失败时能否给出清晰的诊断路径」。具体表现为三类共性信号：一是**稳定性问题集中爆发**，卡死、挂起、静默失败、会话失联在各工具中高频出现；二是**安全加固成为当前 PR 主线**，凭据泄露、OAuth 鉴权、SSRF 防护等议题在多个仓库同步推进；三是**上下文管理与模型策略透明度**开始成为影响用户决策的关键竞争力——长上下文、自动压缩、权限控制等能力正在从「加分项」变为「基本盘」。

---

## 2. 各工具活跃度对比

| 工具 | 版本发布 | 活跃 Issues 数* | PR 动向 | 今日最强信号 |
|---|---|---|---|---|
| **Claude Code** | 2 个补丁版（v2.1.245/246） | 10+ 个热点 | 1 个社区 PR（脚本修复） | Remote Control 空闲断连（83👍，持续近半年） |
| **OpenAI Codex** | 3 个 alpha 版（v0.150.0-a.9/10/11） | 10+ 个热点 | **12+ 个 PR 合并**（并发密集） | Linux 桌面支持（953👍，已关闭） |
| **Gemini CLI** | 4 个版本（含 2 个正式版） | 10 个 P1/P2 | 10 个 PR（**3 个安全修复**） | 子代理 MAX_TURNS 误报为成功（P1） |
| **GitHub Copilot CLI** | 1 个正式版（v1.0.81-10） | 6 个热点 | 无 | vi/vim 输入模式（74👍，跨 11 个月） |
| **Kimi Code CLI** | 无 | 2 个活跃 | 无 | Edit/Write 假成功但不写盘（P0 回归） |
| **OpenCode** | 1 个补丁版（v1.18.23） | 10+ 个热点 | 10+ 个 PR（功能与修复并重） | Ox Alpha Free 工具调用全线故障 |
| **Qwen Code** | 无数据 | 无数据 | 无数据 | —（当日无社区动态） |

> *注：各仓库维护节奏与 issue 关闭策略不同，活跃数只反映当日报告覆盖范围，横向对比需结合上下文解读。若仅以「合并 PR 数量」衡量迭代速度，OpenAI Codex 与 Gemini CLI 在 24 小时内完成的安全修复与功能合入展示出极高的工程吞吐。

---

## 3. 共同关注的功能方向

以下诉求在多个工具社区中形成共振，按覆盖广度排序：

### 3.1 执行结果的可信度与「假成功」问题
- **Gemini CLI**：子代理达到 MAX_TURNS 被误报为 GOAL 成功（P1）
- **Kimi Code**：Edit/Write 返回成功但磁盘无变化（P0）
- **Claude Code**：上下文压缩静默不触发，会话无限挂起
- **OpenCode**：TUI 多问题工具调用无响应，不发送任何事件

> **共同本质**：工具调用的返回状态与真实执行结果不一致，导致自动化流程误判、用户信任受损。

### 3.2 上下文管理与长会话控制
- **Claude Code**：autocompact 惰性触发、覆盖变量被忽略、1M 上下文百分比计算错误
- **Kimi Code**：压缩后重新打开已删除任务
- **Gemini CLI**：Auto Memory 无限重试低信号会话
- **OpenCode**：用户要求删除/编辑上下文中的无效消息

> 各工具在压缩策略、生命周期管理、token 可见性上均处于「有功能但不可控」的状态。

### 3.3 MCP 生态的可靠性与安全性
- **Claude Code**：.mcpb 扩展权限回归
- **OpenAI Codex**：MCP 传输配置崩溃
- **Gemini CLI**：MCP OAuth SSRF 修复（已完成）、扩展环境变量注入防护
- **Copilot CLI**：MCP workspace 配置检测与连接状态不一致

> MCP 正在成为标准扩展协议，但连接可靠性、OAuth 标准化与权限模型仍处于「补课」阶段。

### 3.4 IDE/桌面端集成深度
- **Claude Code**：VS Code 扩展缺少 statusLine 与模型展示
- **OpenAI Codex**：Linux 桌面客户端需求（953👍，全社区最高）
- **Gemini CLI**：IDE stop() 阻塞导致扩展无法卸载
- **OpenCode**：桌面端会话搜索、MCP 管理 UI

> 终端 CLI 不再是唯一入口，「在 IDE 中获得与 CLI 同等能力」的诉求在各用户群中同步增长。

### 3.5 Windows 平台稳定性
- **Claude Code**：窗口置顶、MSIX 卡死、访问冲突崩溃
- **OpenAI Codex**：昨日 6+ 个 Windows 专属新 Bug（认证循环、沙箱崩溃、MCP 失效）
- **OpenCode**：Windows 控制台窗口闪烁

### 3.6 模型策略与自定义模型支持
- **Claude Code**：Usage Policy 误报、豁免表单无效
- **OpenAI Codex**：非 OpenAI 提供商下子代理编排不可用
- **Gemini CLI**：自定义 skills/agents 不被主动调用

---

## 4. 差异化定位分析

| 工具 | 核心定位 | 技术路线特征 | 当前的「短板」 |
|---|---|---|---|
| **Claude Code** | 企业级 Agent 工作台 | 强调 Remote/Cowork 协作、Agent SDK、细粒度权限模型 | 模型策略「一刀切」引发信任危机；上下文管理链路缺乏系统测试 |
| **OpenAI Codex** | OpenAI 生态的深度集成者 | 高频率迭代；同时推进会话总结、遥测、托管 worktree 等工程基建 | Windows 桌面端存在系统性回归；对非 OpenAI 自定义提供商支持不足 |
| **Gemini CLI** | 安全敏感的自动化 Agent | 安全加固力度最大（OAuth/SSRF/凭据清理）；A2A 协议探索 | Agent 可靠性（挂起、误报）拖累整体体验 |
| **Copilot CLI** | GitHub/Copilot 工作流的延伸 | 在 MCP 与插件管理上跟进，形成与 GitHub 平台的闭环 | 功能演进节奏偏慢；社区诉求（vi/vim）长年未解决 |
| **Kimi Code CLI** | 轻量高效的代工助手（中文社区） | 社区规模较小，功能聚焦核心编码场景 | P0 级假成功 Bug 未响应，影响基础信任 |
| **OpenCode** | 开放可扩展的多模型网关 | 插件驱动、社区活跃、对多 provider 兼容激进（Cloudflare/Vertex/Zen） | 免费模型（Ox Alpha Free）故障波及面广；桌面端稳定性有缺口 |

---

## 5. 社区热度与成熟度

**高成熟度 / 慢节奏**
- **GitHub Copilot CLI**：依赖 GitHub 既有生态，功能迭代相对克制，社区长期诉求堆积（vi/vim 模式 74👍 悬置近一年）。

**高成熟度 / 快节奏**
- **Claude Code**：社区规模大且问题讨论深度高，但版本节奏更偏「稳定补丁」，日更量小、PR 侧冷清——呈现成熟产品在稳定期的典型特征。
- **OpenAI Codex**：PR 合并与版本发布密度居首，伴随大量新功能合入，但 Windows 端问题的密集爆发说明测试覆盖尚未跟上迭代速度。

**快速上升期**
- **Gemini CLI**：版本更新频繁（正式版+preview+nightly 四发），安全投入明显，但 P1 级 Agent 稳定性问题仍带「先上线后补稳」的早期特征。
- **OpenCode**：开源社区活跃度极高，Issue 与 PR 双向繁荣，功能创新激进（如持久化终端、1800x 性能优化），处于典型的快速成长期。

**早期 / 低活跃度**
- **Kimi Code CLI**：日活数据极少，社区规模有限，但 P0 Bug 暴露出的可靠性问题若不快速修复，将直接影响早期用户留存。
- **Qwen Code**：当日无社区数据，处于静默期或数据采集盲区。

---

## 6. 值得关注的趋势信号

对技术决策者和开发者而言，以下五个信号最具参考价值：

**① 「假成功」比失败更可怕——可信代理成为硬性要求**
Kimi、Gemini、Claude Code 同日出现「状态误报」「假成功」「静默挂起」类问题，这不是巧合。当 Agent 从「建议者」变为「执行者」，工具调用返回状态与磁盘/系统真实状态的一致性就是底线。在选择工具时，应优先评估其 **错误诊断路径（日志、

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---

# Claude Code 社区动态日报 — 2026-08-26

## 今日速览

昨日发布两个补丁版本（v2.1.245/v2.1.246），重点修复 Linux glibc 2.44 启动崩溃，并新增 Bash 权限规则通配符警告与 `/permissions` Auto 模式管理页。社区层面，**Remote Control 会话空闲断连**（83 👍）持续保持最高关注度，另有新上报的 **Usage Policy 误报**（#89354）与 **Cowork 遥测缺用户身份**（#89483）值得留意。PR 侧相对冷清，仅 1 个脚本修复合入候选。

---

## 版本发布

### v2.1.246
- 新增**启动警告**：当 Bash 允许规则在子命令前使用通配符（如 `Bash(git * main)`）时提示风险——此类规则可能匹配到子命令前插入的选项。
- 在 `/permissions` 中新增 **Auto 模式标签页**，支持查看和编辑自动模式分类器规则。

### v2.1.245
- 修复 Linux 发行版（Arch Linux、CachyOS、Fedora Rawhide 等）携带 **glibc 2.44** 时的启动崩溃问题。

---

## 社区热点 Issues

### 1. Remote Control 会话空闲约 20 分钟后静默死亡 — #32982 ⭐ 83 👍
**标签**: bug / macOS / Linux / networking  
**链接**: https://github.com/anthropics/claude-code/issues/32982  
交互式 CLI、`remoteControlAtStartup` 及 `--agent` 会话均在空闲 5–30 分钟后被服务端 TTL 杀死，keepalive 无效。这是当前社区**获赞最高**的 issue，已持续近半年，覆盖多种触发路径，对远程/无人值守工作流影响严重。

### 2. Claude Desktop (Windows 11) 窗口永远置顶 — #85891 💬 24
**标签**: bug / Windows  
**链接**: https://github.com/anthropics/claude-code/issues/85891  
主窗口始终悬浮于其他应用之上且无设置项可关闭，被视为 Windows 端 counterpart of #66516。35 👍 说明受影响用户面广，评论区讨论热烈。

### 3. MCPB 扩展 Calendar/Reminders 写入权限回归 — #58239 💬 10
**标签**: bug / macOS / MCP  
**链接**: https://github.com/anthropics/claude-code/issues/58239  
Claude Desktop 1.6608.2 破坏 `.mcpb` 扩展对 EventKit（日历+提醒）的写入访问，早前版本可正常工作。虽已被标记 invalid/stale 关闭，但涉及 MCP 扩展生态权限模型，值得跟进。

### 4. VS Code 扩展无法查看当前激活模型 — #74349
**标签**: enhancement / IDE / statusline  
**链接**: https://github.com/anthropics/claude-code/issues/74349  
终端 CLI 有 `statusLine`/`/status` 可持续显示模型，但 VS Code 原生扩展缺少对应 UI 展示（Sonnet/Opus/Haiku 等）。反映 IDE 侧功能 parity 的持续诉求。

### 5. Autocompact 在上下文边缘从不主动触发 — #77509
**标签**: bug / Windows / agents / Agent SDK  
**链接**: https://github.com/anthropics/claude-code/issues/77509  
达到上下文边缘时，autocompact 只在下一条用户消息到来时**惰性触发**；若后续无输入（headless/Agent SDK 场景），会话将无限期挂起。与 #63186、#73710 共同指向**上下文管理链路**的系统性问题。

### 6. `CLAUDE_AUTOCOMPACT_PCT_OVERRIDE` 被静默忽略 — #63186
**标签**: bug / Linux / core  
**链接**: https://github.com/anthropics/claude-code/issues/63186  
`settings.json` 的 `env` 块中配置该变量对 autocompact 阈值无效（子进程可见但应用自身不读取），配置项形同虚设，影响用户对压缩时机的精细控制。

### 7. 模型安全护栏过严，豁免表单无效 — #72852
**标签**: bug / model / security  
**链接**: https://github.com/anthropics/claude-code/issues/72852  
用户反馈新安全机制对合理用例误杀严重，且 typeform 豁免流程无法生效。与 #89354、#73771 等形成同一情绪集群——**模型策略的透明度和申诉路径**是社区核心不满点。

### 8. Cowork VM 服务空闲反复拆除、恢复极慢 — #81874
**标签**: bug / Desktop  
**链接**: https://github.com/anthropics/claude-code/issues/81874  
`CoworkVMService`（Hyper-V 虚拟机）在空闲时反复 teardown，恢复需冷启动；服务 DACL 还阻止外部干预。Cowork 作为远程协作新功能，稳定性问题开始集中暴露。

### 9. [新] Usage Policy 误报：农业公共生物安全数据被拦截 — #89354
**标签**: bug / macOS / model / API  
**链接**: https://github.com/anthropics/claude-code/issues/89354  
8 月 24 日新提交：公共农业生物安全数据在单会话中触发 12 次误报，提供 request IDs。此类误报正在侵蚀用户对模型策略的信任，建议关注官方后续说明。

### 10. `/usage` 叠加层 Escape 键行为回归 — #86491
**标签**: bug / Linux / TUI / regression  
**链接**: https://github.com/anthropics/claude-code/issues/86491  
打开 `/usage` 时首次 Escape 会穿透叠加层、误拒绝底层 pending 工具调用，第二次才关闭面板。交互细节回归，已标记 `reproduced`，修复预期较快。

---

## 重要 PR 进展

过去 24 小时仅有 1 个 PR 更新，属社区贡献脚本修复：

### #89404 — validate-agent.sh：修复 `set -e` 误中止与误报
**作者**: @bcherny | **状态**: OPEN  
**链接**: https://github.com/anthropics/claude-code/pull/89404  
修复公开 issue #83803（plugin-dev 自身 agent 文件校验失败），根因有三：
1. `((warning_count++))` 在 `set -euo pipefail` 下首个警告即中止整个脚本；
2. 算术表达式的退出码问题导致合法 agent 被误判；
3. 通配符/模式匹配逻辑存在非预期行为。

对插件开发者而言，此修复直接影响 `validate-agent.sh` 的可用性，值得关注合入进度。

---

## 功能需求趋势

综合全部 Issues，社区最关注的功能方向如下：

| 方向 | 代表 Issue | 诉求要点 |
|---|---|---|
| **IDE 集成深度** | #74349、#77829 | VS Code 扩展补齐 statusLine 渲染、当前模型展示、spinnerVerbs 等 CLI 既有能力 |
| **上下文管理精细化** | #77509、#63186、#73710 | autocompact 主动触发、覆盖变量生效、1M 上下文下百分比按正确分母计算 |
| **Remote/Cowork 稳定性** | #32982、#81874、#84581 | 会话保活、VM 生命周期可控、远程会话 GitHub 仓库访问打通 |
| **模型策略透明度** | #72852、#89354、#73771 | 豁免流程可用、误报申诉渠道、按身份/用途白名单制 |
| **MCP 插件生态增强** | #73792 | Slack 插件补 `conversations.mark` 等常用 API 能力 |

---

## 开发者关注点

- **Remote Control 闲置断连是持续最久的痛点**（#32982，83 👍）：服务端 TTL 无视 keepalive，直接打击远程协作与无人值守 agent 场景，社区期待 Anthropic 正面回应。
- **模型安全策略「一刀切」引发信任危机**：从严肃的误报申诉（#89354）到近乎情绪化的反馈（#73771「I am tired of this」），用户普遍希望有可用的申诉/豁免机制，而非表单空转。
- **上下文管理链路存在多处失效**：覆盖变量被忽略、主动压缩不触发、百分比显示错误（#63186/#77509/#73710），三案并发表明该模块缺少系统性回归测试。
- **Windows 平台稳定性仍是短板**：窗口置顶（#85891）、MSIX event-loop 卡死（#73491）、WMI 过载（#73785）、访问冲突崩溃（#73780）等多案并存，覆盖面广。
- **IDE 侧形态正在成为「一等公民」**：多起 issue 要求 VS Code 扩展与 CLI 能力对齐，而非仅作为终端包装器。

---

*数据范围：anthropics/claude-code 仓库 2026-08-25 至 08-26 更新内容。部分 issue 因标记 stale/closed，实际活跃度需结合官方响应判断。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-26

## 今日速览

过去 24 小时内，Codex 连续发布了 3 个 Rust 0.150.0 系列 alpha 版本（alpha.9/10/11），迭代节奏明显加快。社区方面，Windows 桌面端成为问题重灾区：认证循环、沙箱恢复失败、MCP 传输配置崩溃等新 Issue 集中出现，且多集中在昨日发布的版本 26.820/26.818 上。功能需求层面，Linux 桌面应用支持（953👍）与「删除会话线程」等长期诉求保持高热。

---

## 版本发布

过去 24 小时发布了 3 个版本，均属 `rust-v0.150.0-alpha` 系列预发布版本，仓库仅提供了基础 Release 说明（无额外变更日志）：

- **rust-v0.150.0-alpha.9** — 0.150.0-alpha.9
- **rust-v0.150.0-alpha.11** — 0.150.0-alpha.11
- **rust-v0.150.0-alpha.10** — 0.150.0-alpha.10

> 说明：三个版本标注为预发布（alpha），推测为同一开发主线上的连续构建，具体变更内容未随 Release 说明披露，建议关注后续正式 Release Notes。

---

## 社区热点 Issues

#### 1. Codex 桌面应用不支持 Linux（已关闭，209 评论 / 953👍）
> 社区长期最高赞需求。用户希望能在 Linux 桌面使用 Codex 应用，此前因 macOS 上的电源消耗问题几乎无法使用。该 Issue 已关闭，但关闭原因未注明，可能是已进入路线图或转移至其他跟踪渠道。

🔗 https://github.com/openai/codex/issues/11023

#### 2. 定时任务运行成功后自动禁用自身（40 评论）
> 多个 ChatGPT Work 中的周期性定时任务在成功执行后，从 enabled 状态自动变为 paused，且没有任何用户操作。涉及 4 个不相关任务同时出现该问题，疑似自动化调度层的状态管理 Bug，对依赖自动化的团队影响较大。

🔗 https://github.com/openai/codex/issues/38350

#### 3. 允许删除会话线程而非仅归档（29 评论 / 105👍）
> macOS 应用目前只能归档线程，用户需要手动进入 `~/.codex/archived_sessions/` 操作文件。这是一个长期存在且呼声很高的产品功能缺失。

🔗 https://github.com/openai/codex/issues/13018

#### 4. 增加选项禁用「已运行 N 条命令」折叠（25 评论 / 43👍）
> CLI/TUI 用户希望始终展开显示已执行的命令，而不是被折叠成一行摘要。对于需要审计终端输出的场景（如 screen/tmux 录制）尤为关键。

🔗 https://github.com/openai/codex/issues/39903

#### 5. Windows 独立更新时 PSModulePath 继承导致 Get-FileHash 失败（22 评论）
> 从 PowerShell 7 启动 Codex 后，更新流程会拉起 Windows PowerShell（powershell.exe），子进程继承了 PS7 的 PSModulePath，导致模块加载冲突。Windows 更新链路的一个典型环境继承 Bug。

🔗 https://github.com/openai/codex/issues/27117

#### 6. 原生子代理编排不兼容非 OpenAI 自定义提供商（14 评论）
> 使用自定义模型提供商（非 OpenAI）时，原生 subagent 编排无法正常工作。限制了大量依赖第三方模型网关（如 Azure OpenAI、本地代理）的企业用户。

🔗 https://github.com/openai/codex/issues/17598

#### 7. Windows 稳定版 ChatGPT 26.820 报「invalid transport in mcp_servers.codex_app」（11 评论）
> 最新稳定版应用在读取 MCP 配置时报传输协议无效，而 Beta 版 26.727 可正常工作。属于典型的版本回退/兼容性破坏问题，影响所有使用 MCP 的 Windows 用户。

🔗 https://github.com/openai/codex/issues/40715

#### 8. 应用内浏览器初始化失败：node_repl 拒绝 node:process 导入（10 评论）
> 内置 Browser 插件在初始化阶段即崩溃，无法发现或控制浏览器标签页。影响 macOS 上使用桌面应用浏览器能力的用户。

🔗 https://github.com/openai/codex/issues/35224

#### 9. 支持 GPT-5.6 可选 1M 上下文（8 评论 / 22👍）
> 延续 #19464 的请求，希望 Codex 全客户端（App/CLI/IDE）支持 GPT-5.6 的 1M 上下文窗口。对于大型代码库分析场景有实际需求。

🔗 https://github.com/openai/codex/issues/31868

#### 10. git worktree 下项目级 hooks.json 被静默忽略（9 评论）
> 在 git worktree 中运行 Codex 时，项目根目录的 `.codex/hooks.json` 不会生效，且无任何警告。对使用 worktree 做多任务并行开发的团队是个隐蔽的坑。

🔗 https://github.com/openai/codex/issues/27133

---

## 重要 PR 进展

所有列出的 PR 均在 8 月 25 日合并/关闭（作者为 copyberry[bot]），且包含详细变更摘要：

#### 1. 生成自动和手动会话总结（#40705）
> 为不活跃/失焦会话自动生成短摘要并附加到会话记录中，同时新增 `/recap` 命令支持手动触发。对多会话开发者是实用改进。

🔗 https://github.com/openai/codex/pull/40705

#### 2. 清理 Git 远程元数据中的凭据（#40713）
> Git 远程 URL 可能内嵌用户名、密码或 token，此前会随轮次元数据和持久化线程元数据传递。现新增 `SanitizedGitUrl` 在进入存储路径前剥离凭据。安全修复。

🔗 https://github.com/openai/codex/pull/40713

#### 3. 调试输出中脱敏 Bedrock API Key（#40706）
> 派生 Debug 格式化实现会暴露托管 Amazon Bedrock API Key，现改为自定义 Debug 实现，输出 `<redacted>` 保留区域信息，并附带回归测试。

🔗 https://github.com/openai/codex/pull/40706

#### 4. 为 MCP OAuth 添加企业 ID-JAG 交换（#40722）
> 新增非交互式两步交换流程：从企业身份提供商获取 ID-JAG，再交换资源绑定的 MCP Bearer token，并校验端点 URL、请求输入和 ID-JAG 声明。

🔗 https://github.com/openai/codex/pull/40722

#### 5. 保留组合器超链接跨行完整性（#40720）
> 修复 TUI 组合器（composer）内 URL 在换行时被截断的问题，通过 OSC 8 完整目标附加到每个包裹片段，并缓存超链接元数据。

🔗 https://github.com/openai/codex/pull/40720

#### 6. 加固 MCP OAuth 回调处理（#40691）
> 解决多个 MCP 服务器共享回调 URL 时授权响应可能被关联到错误服务器的问题。启用元数据广告稳定回调，并校验 issuer。

🔗 https://github.com/openai/codex/pull/40691

#### 7. 保留保留工具模式中的参数边界（#40719）
> 保留工具参数约束（`minimum`/`maximum`/`maxLength`）在 schema 解析后不丢失，确保模型收到声明限值。对依赖工具参数校验的 Agent 场景关键。

🔗 https://github.com/openai/codex/pull/40719

#### 8. 追踪图像生成请求 ID 到分析（#40714）
> 从图像生成和编辑响应中读取 `x-codex-imagegen-request-id`，并传播到 `codex_image_generation_event` 分析中（仅进程内保留，不参与持久化）。

🔗 https://github.com/openai/codex/pull/40714

#### 9. 添加插件归属的技能遥测（#40724）
> 为 `codex.skill.injected` 添加 `plugin_id`、`model_slug`、`reasoning_effort` 维度，支持从编排器技能元数据中传播插件 ID。便于追踪技能调用的插件来源。

🔗 https://github.com/openai/codex/pull/40724

#### 10. 为托管工作树添加线程所有权元数据（#40716）
> 新增 `WorktreeManager` API，将托管 linked worktree 绑定到线程并记录所有者。使用带版本号的 `codex-thread.json` 以原子、无覆盖写入方式存储在 Git 元数据中。

🔗 https://github.com/openai/codex/pull/40716

#### 11. 为 SQLite 日志持久化添加遥测（#40726）
> 新增对批处理大小、写入延迟、失败次数和写入前丢弃条目的可观测性，并确保导出器诊断不会反馈回 SQLite 日志 sink。

🔗 https://github.com/openai/codex/pull/40726

#### 12. 移除 code-mode host 的 WebSocket 传输（#40692）
> app server 的 `--code-mode-host` 仅接受 HTTP/HTTPS gRPC 端点；独立 code-mode host 限制为 stdio 和 gRPC 监听器；移除 WebSocket 会话提供程序及双重 WebSocket 协商逻辑。

🔗 https://github.com/openai/codex/pull/40692

> 其他已关闭 PR：#40697（准备自动 TUI 会话总结生成）、#40696（TUI 会话总结 UI 准备）、#40709（重命名用户指令负载为 `Instructions`）、#40710（远程执行器连接刷新）、#40712（relay 助手迁移至 exec-server 测试支持）、#40717（沙箱 exec-server 测试环境）、#40718（为固定 Codex 版本添加 Bazel 仓库）、#40723（更新生物学 Trusted Access 链接）等。

---

## 功能需求趋势

从当前活跃 Issues 中可提炼出以下社区高关注方向：

| 方向 | 代表 Issue | 热度信号 |
|------|-----------|---------|
| **Linux 桌面客户端** | #11023 | 953👍，已关闭但需求量大 |
| **会话管理增强**（删除线程、项目绑定、恢复） | #13018、#40219 | 105👍，多平台反馈 |
| **TUI/CLI 可用性优化**（命令可见性、就地编辑、超链接） | #39903、#35005、#40720 | 43👍，集中在 CLI 工作流 |
| **长上下文支持**（1M Context） | #31868 | 22👍，针对 GPT-5.6 |
| **自定义模型提供商兼容性** | #17598 | 14 评论，企业用户受阻 |
| **Windows 平台稳定性** | #40715、#40700、#40698 等 | 昨日新增 6+ 条 Windows 专属 Bug |
| **定时任务/自动化可靠性** | #38350 | 40 评论，状态管理异常 |

**趋势解读**：
- **长上下文** 和 **自定义提供商** 是企业在规模化落地时的两大瓶颈，预计官方将继续加码；
- **TUI 可配置性**（折叠行为、编辑模式）正在取代单纯「加功能」的诉求，社区开始要求「可控性」；
- **Windows 桌面端稳定性** 是目前最集中的短期痛点，昨日密集出现了 6 个以上与版本 26.818/26.820 相关的启动/认证/沙箱崩溃报告。

---

## 开发者关注点

**1. Windows 桌面端成重灾区**
- 认证循环（#40699）、应用启动失败（#40700）、沙箱恢复崩溃 0xc0000142（#39251）、浏览器进程反复崩溃（#40711）、MCP 传输失效（#40715）、权限状态静默降级（#40698）、会话中途 exit 0（#40630）——过去 24 小时内密集出现，且集中在最新稳定版，提示该版本可能存在系统性回归。

**2. TUI 折叠命令摘要引发审计需求**
- 用户希望在 `screen`/`tmux` 等场景下完整保留命令输出，折叠功能对自动化记录和远程协作造成了信息丢失。该 Issue 短期内从 0 增长到 25 评论，说明触达了真实痛点。

**3. 异常 token 消耗问题持续发酵**
- 多起报告（#33196、#39854）显示并行 subagent 导致 token 消耗异常放大（单次任务消耗 ~678M token），且伴随 `wait_agent` 轮询和 `fork_turns="all"` 配置。这与多代理编排机制的设计权衡直接相关，已引发用户对成本控制的担忧。

**4. 自定义模型生态的「二等公民」焦虑**
- 原生 subagent 编排对非 OpenAI 提供商不生效（#17598），叠加 MCP OAuth 鉴权复杂化（#40715、#40691），使用第三方/自建网关的开发者面临集成壁垒。

**5. 数据安全与凭据泄露防护成为 PR 主线**
- 昨日合并的 PR 中有多项涉及凭据清理（Git 远程 URL、Bedrock API Key）与 OAuth 加固，说明官方正在审计敏感信息在元数据链中的传递路径。

**6. 定时任务可靠性**
- 自动化任务成功运行后自动禁用（#38350）在论坛引发讨论，普遍认为这是调度状态机的问题而非用户操作，对依赖无人值守自动化的

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-26

## 今日速览

今日发布了 4 个版本（含 2 个正式版），核心修复集中在 OAuth 流程、IDE 连接稳定性与符号链接处理。社区讨论热度集中在 **Agent 挂起/卡死**（#21409、#25166）与 **子代理错误报告不准确**（#22323）两大 P1 级 Bug 上；安全类 PR 数量明显上升，涵盖 MCP OAuth SSRF 防护、扩展环境变量注入防护及 A2A 服务器凭据清理。

---

## 版本发布

| 版本 | 类型 | 核心内容 |
|------|------|----------|
| **v0.58.0-preview.0** | Preview | 修复 ignore 路径处理中符号链接求值不一致的问题；core 重构 |
| **v0.57.0** | 正式版 | 支持 Cloud Workstations 动态解析代理重定向 URI（OAuth 流程）；修复 IDE 连接中目录不匹配被吞掉的问题 |
| **v0.57.0-preview.1** | Preview | Cherry-pick 修复到 v0.57.0-preview.0 并生成补丁版本 |
| **v0.56.0-nightly.20260825** | Nightly | a2a-server 清除新消息轮次中的过期取消错误；core 在写策略配置中声明顶层安全检查器 |

> 完整变更日志：[v0.57.0 对比](https://github.com/google-gemini/gemini-cli/compare/v0.56.0...v0.57.0)

---

## 社区热点 Issues（Top 10）

### 1. Subagent 达到 MAX_TURNS 被误报为 GOAL 成功 🔥 P1
[#22323](https://github.com/google-gemini/gemini-cli/issues/22323)

`codebase_investigator` 子代理在未执行任何分析就触及最大轮次限制时，仍上报 `status: "success"` 和 `Termination Reason: "GOAL"`，**掩盖了中断事实**。当前 13 条评论，社区质疑错误报告会导致自动化流程误判任务完成。更新于 8 月 25 日，标记为 `need-retesting`。

### 2. Generalist agent 无限挂起 🔥 P1
[#21409](https://github.com/google-gemini/gemini-cli/issues/21409)

只要 Gemini CLI 委派给 generalist agent（如创建文件夹这类简单操作），就会永远挂起，用户最长等待 1 小时后取消。社区给出临时绕过方案：**在提示词中显式禁止委派子代理**。获得 8 👍，是当前社区反馈最强烈的 Agent 稳定性问题。

### 3. Shell 命令执行卡在 "Waiting input" P1
[#25166](https://github.com/google-gemini/gemini-cli/issues/25166)

简单 CLI 命令执行完成后，终端仍显示命令活跃并等待用户输入，但进程实际已结束。该问题**高频复现**，影响面广，3 👍。属于 core 领域，标记 `effort/medium`。

### 4. Browser 子代理在 Wayland 下失败 P1
[#21983](https://github.com/google-gemini/gemini-cli/issues/21983)

Browser Agent 在 Wayland 会话中直接失败，Termination Reason 显示为 GOAL 但实际未完成目标。对 Linux 桌面用户影响较大，1 👍。

### 5. Auto Memory 无限重试低信号会话 P2
[#26522](https://github.com/google-gemini/gemini-cli/issues/26522)

Auto Memory 仅在提取代理成功读取 transcript 后才将会话标记为已处理；若代理因低信号跳过读取，该会话会**反复出现在索引中并被无限重试**，浪费 token 和算力。5 条评论，反应了用户对后台资源消耗的关注。

### 6. 超过 128 个工具时遭遇 400 错误 P2
[#24246](https://github.com/google-gemini/gemini-cli/issues/24246)

工具数量超过约 400 个时 API 返回 400。用户期望 Agent 能**智能收窄工具范围**而非全量暴露。属于 core 限制，影响重度扩展用户。

### 7. Gemini 不主动使用 skills 和 sub-agents P2
[#21968](https://github.com/google-gemini/gemini-cli/issues/21968)

用户配置了 Gradle、Git 等自定义 skills，但 Gemini 在被明确指示之前**几乎从不主动调用**，即使任务高度相关。社区认为这削弱了自定义扩展的价值。

### 8. AST 感知文件读取价值评估 P2（Feature）
[#22745](https://github.com/google-gemini/gemini-cli/issues/22745)

EPIC 级特性：用 AST 感知工具实现精准读取方法边界、减少轮次和 token 噪声。评论中建议以 `tilth` 或 `glyph` 为起点做代码库映射。代表社区对 **token 效率**的持续追求。

### 9. Agent 应阻止/劝阻破坏性行为 P2
[#22672](https://github.com/google-gemini/gemini-cli/issues/22672)

在复杂 git 操作、分支管理、数据库维护等场景中，模型会使用 `git reset`、`--force` 等命令，即便存在更安全的替代方案。社区期望 Agent 具备**危险操作识别与劝阻**能力。

### 10. `~/.gemini/agents/` 下符号链接不被识别 P2
[#20079](https://github.com/google-gemini/gemini-cli/issues/20079)

`filename.md` 符号链接不会被识别为有效 Agent，而真实文件可以。该问题与今日 v0.58.0-preview.0 的符号链接修复相呼应，用户希望 Home 目录下的 Agent 配置支持符号链接。

---

## 重要 PR 进展（Top 10）

### 1. [安全] 修复 MCP OAuth 元数据发现 SSRF 🛡️
[#29081](https://github.com/google-gemini/gemini-cli/pull/29081)

强制遵循 RFC 9728 §7.7 与 RFC 8414 安全约束：远程 OAuth 端点强制 HTTPS（仅 loopback 允许 HTTP）、验证资源标识符的 origin 匹配。这是对 MCP 生态安全性的重要补强。

### 2. [安全] 扩展环境变更需用户同意 + 环境变量清洗 🛡️
[#28863](https://github.com/google-gemini/gemini-cli/pull/28863)

扩展更新此前可**绕过用户同意检查**，且未授权环境变量可能被注入 MCP Server 进程。此 PR 将环境配置纳入同意字符串生成，并清洗自定义环境变量。

### 3. [稳定性] 修复 vscode-ide-companion 的 stop() 挂起 🔧
[#29088](https://github.com/google-gemini/gemini-cli/pull/29088)

`IdeServer.stop()` 等待所有连接排空，但 MCP 传输在 `GET /mcp` 上持有长连接流式响应，导致 **stop() 永不 resolve**，扩展 deactivate 被阻塞。修复后 VS Code 扩展可正常卸载。

### 4. [稳定性] 修复 CLI 扩展并发安装竞态 🔧
[#29087](https://github.com/google-gemini/gemini-cli/pull/29087)

两个 Gemini CLI 进程同时安装/更新同一扩展时，会交错执行文件拷贝和元数据写入。通过 `proper-lockfile` 增加文件锁，防止数据损坏。

### 5. [稳定性] abortSignal 正确传递到 retryWithBackoff 🔧
[#29089](https://github.com/google-gemini/gemini-cli/pull/29089)

`BaseLlmClient`（供会话摘要、压缩、分类器等使用）虽接受 `abortSignal` 但未传给重试逻辑，导致取消操作后仍可能发起重试。当前评论数不多，但属基础设施修复。

### 6. [安全] 移除 A2A Server 误导性安全方案与硬编码凭据 🛡️
[#29067](https://github.com/google-gemini/gemini-cli/pull/29067)

`coderAgentCard` 中移除了误导性的 `securitySchemes` 声明，并从 `customUserBuilder` 中删除不安全的硬编码凭据。该 PR 在 #29018 基础上重启，可见维护者对安全修复的审慎。

### 7. [安全] 丢弃不安全的 `diff.external` 覆盖 🛡️
[#28930](https://github.com/google-gemini/gemini-cli/pull/28930)

此前通过 `['diff.external', '']` 禁用外部 diff 工具，但 Git 将空值解释为"使用内置 diff"，与预期相悖。修复后改用正确方式，**避免意外触发外部工具**。

### 8. [正确性] 混合行尾检测：单条 CRLF 不再误判整个文件
[#28983](https://github.com/google-gemini/gemini-cli/pull/28983)

`detectLineEnding()` 原先只要文件中出现一个 `\r\n` 就将整个文件判定为 CRLF，与周围大量 LF 行相矛盾。修复为混合行尾检测，提升跨平台编辑体验。

### 9. [依赖] npm 依赖批量升级（76 项更新）📦
[#28984](https://github.com/google-gemini/gemini-cli/pull/28984)

涉及 `simple-git`（3.28→3.36）、`@modelcontextprotocol/sdk` 等 76 个包。属于常规依赖维护，但属于 `size/xl` 变更，建议关注是否引入行为变化。

### 10. [文档] Windows longpaths 配置说明
[#28926](https://github.com/google-gemini/gemini-cli/pull/28926)

在 `CONTRIBUTING.md` 中增加 Windows `core.longpaths=true` 配置指南。因深层嵌套快照路径超过 `MAX_PATH`（260 字符），Windows 克隆会产生约 3000 个脏暂存文件，严重影响 Windows 贡献者体验。

---

## 功能需求趋势

综合全部 50 条 Issues，社区关注度最高的功能方向集中在五个维度：

1. **Agent 行为可靠性**（约 40%）：子代理状态误报、generalist 挂起、执行完不退出等问题占据主导，社区已从追求功能丰富转向追求**结果可信任**。
2. **安全加固**（约 20%）：MCP OAuth SSRF、扩展注入、A2A 硬编码凭据、`diff.external` 滥用等，安全 PR 数量创近期新高，说明官方正在系统性收紧边界。
3. **Token 效率与上下文管理**：AST 感知文件读取（#22745）、Tactful Extraction（#19561）、Auto Memory 重试控制（#26522、#26523），社区持续关注上下文膨胀问题。
4. **IDE 集成体验**：vscode-ide-companion 的 stop() 挂起被连续两个 PR 修复（#28789 关闭、#29088 新开），IDE 连接稳定性是当前短板。
5. **终端体验与跨平台**：resize 闪烁（#21924）、Windows longpaths 说明、Wayland 浏览器失败，跨平台问题持续被报告。

---

## 开发者关注点（痛点总结）

- **"看起来成功实则失败"的误导性上报**：MAX_TURNS 被报为 GOAL、浏览器 Agent 未完成目标却返回成功，这类问题对自动化流程伤害极大，开发者多次建议区分"正常完成"与"被中断"的终止原因。
- **卡死/悬停类问题优先级最高**：generalist 挂起、shell 等待输入不退出、IDE stop() 阻塞——三个独立问题指向同一核心诉求：**任何操作都应可取消、可超时、可诊断**。
- **安全边界与便捷性的平衡**：社区一方面感谢扩展环境变量注入修复，另一方面在 #19873 中希望通过零依赖 OS 沙箱释放模型的 bash 原生能力，在安全前提下提升性能。
- **配置灵活性不足**：symlink 不被识别、browser_agent 忽略 `settings.json` 覆盖——开发者希望在配置层获得一致的语义化行为。

---

*本日报由 AI 自动整理自 GitHub 公开数据，日期为 2026-08-26。数据范围：过去 24

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-26**

## 今日速览
今日发布 v1.0.81-10，插件仪表板（Plugins Dashboard）正式向所有用户开放，并统一了 `x` 删除键交互。社区讨论热点集中在 MCP 配置可靠性问题（workspace 配置未实际连接、1.0.81-10 令牌注入回归）以及长期悬而未决的 vi/vim 输入模式请求（👍 74）。

## 版本发布

### v1.0.81-10

**新功能**
- 插件仪表板向所有用户开放：运行 `/plugin`、`/mcp` 或 `/skills` 即可访问。
- 设置 `PLUGINS_DASHBOARD=false` 可退出该仪表板及 `copilot plugins` 命令。

**改进**
- `x` 键现在在所有场景中统一作为删除键：包括 `/sandbox config`、`/settings`、`/mcp`、会话对话框及 diff 视图。

## 社区热点 Issues

### 1. vi/vim 输入模式
[#13](https://github.com/github/copilot-cli/issues/13)（👍 74，💬 8）
作者 @RyanHecht 于 2025 年 9 月提出，至今仍是评论区活跃度最高的功能请求。用户希望在 CLI 交互界面中使用模态编辑器风格的键盘驱动导航和编辑。高赞数表明键盘优先的工作流在 CLI 深度用户中占显著比例。

### 2. 1.0.81-10 MCP 令牌注入回归
[#4604](https://github.com/github/copilot-cli/issues/4604)（新增，💬 0）
升级到 1.0.81-10 后，用户配置的 `api.githubcopilot.com/mcp/` 服务器不再收到自动注入的 Copilot 令牌，且 OAuth 方式因远端不支持动态客户端注册而无法救回。新版本引入的认证回归，需优先关注。

### 3. store_memory 失败与 MCP 服务器被剥离
[#4602](https://github.com/github/copilot-cli/issues/4602)（新增，💬 0）
`store_memory` 工具导致整个会话失败，所有 MCP 服务器被剥离，根因指向 `managedSettings` 在 `serverFetchFailed` 时 fail-closed。报告者指出该机制与多个既有 issue 共享同一根因，需要统一处理。

### 4. Auto 模型强制禁用推理努力
[#4560](https://github.com/github/copilot-cli/issues/4560)（💬 1）
当模型设置为 `auto` 时，`reasoningEffort` 始终为 `null`，且拒绝任何手动配置。依赖 `auto` 路由策略的用户无法对推理强度进行控制，属于模型配置层面的功能缺口。

### 5. 新模型被企业策略禁用且无法开启
[#4272](https://github.com/github/copilot-cli/issues/4272)（👍 3，💬 1）
企业用户看到大量新模型提示“被组织策略禁用”，但管理页面并没有对应开关，管理员也无从下手。涉及企业策略与模型可用性的联动问题。

### 6. Workspace .mcp.json 检测与连接不一致
[#4542](https://github.com/github/copilot-cli/issues/4542)（👍 1，💬 2）
`mcp list` 显示 workspace `.mcp.json` 的服务器为“已启用”，但实际 agent 会话中并未真正连接。“检测

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-08-26）

数据源：github.com/MoonshotAI/kimi-cli

## 1. 今日速览

过去24小时（2026-08-25 ~ 2026-08-26），Kimi Code CLI 仓库无新版本发布、无新增或更新的 Pull Request，活跃 Issue 有 2 条。最值得关注的是 macOS 平台上的一个高危回归 Bug（#2617）：0.38.0 版本的 `Edit` 和 `Write` 工具返回“成功”提示却未写入磁盘，极易误导开发者。另一条是存在一个多月的上下文压缩 Bug（#2523）昨日有用户继续反馈，该问题会导致已删除任务被错误重新打开。

## 2. 版本发布

过去24小时内无新版本发布。

## 3. 社区热点 Issues

过去24小时共有 2 条活跃更新，全部列出如下：

### #2617 Edit/Write 工具报告成功但从未写入磁盘（0.38.0, macOS）

- **作者**：@tizerluo
- **创建**：2026-08-25 | **更新**：2026-08-25 | **评论**：2 | **状态**：Open
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2617
- **摘要**：自 2026-08-25 ~17:00 UTC 起，`Edit` 和 `Write` 工具在会话中静默失败：返回“文件已更新/文件创建成功”但磁盘上无任何改动，报告者称 100% 可复现。
- **重要性**：**P0 级回归 Bug**。AI 编程助手的核心价值就是可信地修改代码，虚假成功会导致用户盲目信任结果，最终保存/构建时才发现文件不一致，严重影响开发流程。
- **社区反应**：已有 2 条评论讨论排查方向（疑为该时间段的一次热更新引入），官方尚未回复。

### #2523 上下文压缩 Bug——重新打开已完成并删除的任务（v0.6.3, Windows）

- **作者**：@Frogzter
- **创建**：2026-07-20 | **更新**：2026-08-25 | **评论**：1 | **状态**：Open
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2523
- **摘要**：在 v0.6.3、Windows 环境下，触发上下文压缩后，CLI 会重新打开一个已经完成并删除的任务，导致会话列表混乱。模型为 K2.7 coding，用户附带了 PDF 过程记录。
- **重要性**：上下文压缩是长会话的核心场景，该 Bug 导致任务生命周期管理失效，影响多任务连续执行的可靠性。
- **社区反应**：Issue 已存在近一个月，昨日仍有新回复，说明问题在现版本仍可复现，用户希望提供任务状态重置/清理方案。

> 数据有限，当前仅 2 个活跃 Issue，暂无法列出“挑选 10 个热门”的清单。

## 4. 重要 PR 进展

过去24小时内无新增或更新的 Pull Request。

## 5. 功能需求趋势

从当前活跃 Issue 中可提炼出两个社区核心关注方向：

| 方向 | 具体诉求 | 关联 Issue |
| --- | --- | --- |
| **文件系统可靠性** | `Edit`/`Write` 等工具调用的返回值必须与磁盘真实状态一致，失败时应立即报错而非静默吞掉 | #2617 |
| **上下文/会话管理** | 上下文压缩不应复活已删除任务；需要显式的任务清理与恢复命令 | #2523 |

## 6. 开发者关注点

- **假成功的危害**：#2617 最被诟病的不是“写入失败”，而是“报告成功”。开发者期望工具调用在异常时抛错，并附带详细的写入路径/日志，便于快速定位。
- **跨平台一致性问题**：#2523 暴露 Windows 平台下任务状态恢复机制与 macOS/Linux 的差异，用户建议增加 `session list` / `task cleanup` 之类的管理命令。
- **快速修复的诉求**：两个 Issue 都是高影响稳定性问题，开发者关注官方是否会在未来 24 小时内发布 hotfix 或给出临时规避方案。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-26

## 1. 今日速览

OpenCode 发布 v1.18.23 补丁版本，修复了 Cloudflare AI Gateway 对第三方提供方（含 Anthropic 模型）的路由问题。社区方面，Ox Alpha Free 模型在工具调用时集体报错 "Endpoint is unavailable" 成为今日最集中的故障反馈（多个 Issue 同时活跃）；此外，桌面端搜索、会话管理等长期功能需求持续获得高赞。

## 2. 版本发布

**v1.18.23**（核心修复）

- 修复 Cloudflare AI Gateway 对第三方提供方的路由问题，使非 Workers 模型可通过网关 REST API 正常工作。
- 修复通过 Cloudflare AI Gateway 使用 Anthropic 模型时的模型 ID 转换问题（如 `claude-haiku-4.5` 这类带点的 ID 正确转为虚线格式）。

https://github.com/anomalyco/opencode/releases/tag/v1.18.23

## 3. 社区热点 Issues（Top 10）

### 3.1 Ox Alpha Free 工具调用全链路故障（今日最高频）

| Issue | 标题 | 状态 | 评论/👍 | 摘要 |
|---|---|---|---|---|
| [#44300](https://github.com/anomalyco/opencode/issues/44300) | Zen API: x-preview-f-free / ox-alpha-free fails with "Endpoint is unavailable" for any request containing tools | OPEN | 13 / 5 | 自 08-23 起，任何包含 `tools` 数组的请求在 Zen Console 和 Go 两条路由上均稳定失败，影响所有使用工具调用的开发者 |
| [#44850](https://github.com/anomalyco/opencode/issues/44850) | Ox Alpha Free fails with "Endpoint is unavailable" when OpenCode uses tools | OPEN | 7 / 2 | 独立确认同一问题：普通对话正常，一旦 OpenCode 启用工具即报错，导致 NVGT 等项目无法工作 |
| [#45020](https://github.com/anomalyco/opencode/issues/45020) | Error from provider (Console Go): Upstream request failed: Endpoint is unavailab... | CLOSED | 2 / 0 | 同一错误的重复报告 |
| [#45084](https://github.com/anomalyco/opencode/issues/45084) | [needs:compliance] Error from provider (Console): Upstream request failed: Endpoint is unavailable. | CLOSED | 1 / 0 | 用户明确表达"这个错误太烦人且反复出现，请修复" |

**重要性**：这是当前影响面最广的线上故障，涉及免费模型的核心可用性。多人在不同 Issue 中重复报告，且带有截图证据，说明问题确实在服务端，而非个别用户配置。

### 3.2 macOS 启动崩溃（高评论）

- **[#8345](https://github.com/anomalyco/opencode/issues/8345)** — `zsh: illegal hardware instruction opencode`（OPEN，23 评论，7 👍）
  用户在 Terminal 中启动 opencode 即崩溃，发生在 Intel x64 macOS（darwin-x64）上，安装包为 dmg 版本。已持续数月仍开放，社区关注度高。

### 3.3 会话管理与数据控制（高赞功能诉求）

- **[#7712](https://github.com/anomalyco/opencode/issues/7712)** — 编辑上下文删除消息（CLOSED，4 评论，**12 👍**）
  用户希望能在上下文中删除消息以避免死胡同，该请求获得大量认可，但 Issue 已被关闭，社区仍有呼声。

- **[#43277](https://github.com/anomalyco/opencode/issues/43277)** — 会话永久卡死，重启无法恢复（OPEN，5 评论）
  多个会话在正常使用中卡死，状态持久化到磁盘，重启后依然拒绝新消息，且无法通过任何方式恢复。属严重数据可用性问题。

### 3.4 桌面端 & TUI 稳定性

- **[#35434](https://github.com/anomalyco/opencode/issues/35434)** — 多问题工具调用在 TUI 中静默失败（CLOSED，7 评论）
  v1.17.13 回归：`question` 工具含 ≥2 个问题时，TUI 渲染表单但回车无响应，不发送任何事件。单问题调用正常，指向明确的回归源 #34116。

- **[#35494](https://github.com/anomalyco/opencode/issues/35494)** — TUI 在 Debian 13 / XFCE / X11 上白屏冻结（OPEN，3 评论）
  TUI 完全白屏，只有 `kill -9` 能结束，涉及 Linux 桌面环境兼容问题。

### 3.5 连接与网络问题

- **[#12405](https://github.com/anomalyco/opencode/issues/12405)** — 连接被服务器重置（CLOSED，19 评论）
  Windows 10 环境下使用代理连接智谱 GLM4.7 时，执行 init 命令即报错，是环境兼容性的高频案例。

### 3.6 2.0 自动更新器异常（惊人类 Bug）

- **[#45087](https://github.com/anomalyco/opencode/issues/45087)** — 自动更新器重新安装 OpenCode 占用 **266 GB**（OPEN，3 评论）
  `opencode2 serve --service` 每 10 分钟执行一次更新循环，不断向 `~/.npm/_cacache` 写入 beta 包，直至磁盘被填满。已超出普通 bug 范畴，属资源耗尽级事故。

## 4. 重要 PR 进展（Top 10）

### 4.1 核心稳定性修复

- **[#43498](https://github.com/anomalyco/opencode/pull/43498)** — fix(ai): preserve Vertex Anthropic tool continuations（CLOSED）
  修复 Vertex Anthropic 工具连续调用结束时以系统消息结尾导致 HTTP 404 的问题。对 Vertex AI 用户是实际阻塞项。

- **[#45002](https://github.com/anomalyco/opencode/pull/45002)** — feat(core): repair malformed tool arguments before validation（OPEN）
  注册内部插件，在 schema 校验前修复工具参数的小毛病（如移除 null、强转数值/布尔字符串、解析字符串化容器），降低模型输出 JSON 不规范的失败率。

- **[#44895](https://github.com/anomalyco/opencode/pull/44895)** — fix(opencode): deterministic plugin load order and hook error isolation（OPEN）
  修复插件加载顺序不确定的问题，并隔离 hook 错误防止单点失败。是大型重构 #44242 的一部分。

### 4.2 模型兼容性增强

- **[#45088](https://github.com/anomalyco/opencode/pull/45088)** — fix(ai): enable Vertex Anthropic prompt caching（CLOSED）
  为 Vertex Anthropic 增加自动缓存断点，覆盖工具、系统指令和会话消息，显著降低成本和延迟。

- **[#45085](https://github.com/anomalyco/opencode/pull/45085)** — fix(ai): send responses instructions at top level（CLOSED）
  将 Responses API 的初始指令从合成系统消息改到标准顶层 `instructions` 字段，统一 `request.system` 为唯一来源。

- **[#45081](https://github.com/anomalyco/opencode/pull/45081)** — fix(ai): accept responses calls without item ids（CLOSED）
  接受缺少可选 provider item ID 但包含 `call_id` 的 Responses function_call，提升对多样 provider 实现的兼容性。

- **[#45075](https://github.com/anomalyco/opencode/pull/45075)** — fix(ai): require reasoning fields for deepseek assistants（CLOSED）
  为 DeepSeek 推理模型增加 `requireReasoning` 选项，根据模型 ID/provider/端点智能推断是否必须发送 reasoning 字段。

### 4.3 新功能与体验优化

- **[#44971](https://github.com/anomalyco/opencode/pull/44971)** — feat(tui): add persistent session terminals（OPEN）
  TUI 新增持久化会话终端：左侧会话 + 右侧选定终端的固定双栏布局，终端成员关系和选择状态按会话管理，无递归窗格树。

- **[#45086](https://github.com/anomalyco/opencode/pull/45086)** — feat(core): support Azure CLI authentication（OPEN，bot 提交）
  为 V2 Azure provider 增加通过现有 Azure CLI 会话的 Microsoft Entra ID 认证，同时保留 API key 流程。与 #45079 为双版本提交（V2/当前）。

- **[#44898](https://github.com/anomalyco/opencode/pull/44898)** — fix(opencode): honest context arithmetic for small and unreported model limits（OPEN）
  修复小上下文或未上报上下文限制模型的 token 计算不准确问题（#41372 系列的第二部分）。

- **[#38880](https://github.com/anomalyco/opencode/pull/38880)** — fix(tui): ~1800x image pasting performance improvement（CLOSED）
  TUI 图片粘贴性能提升约 1800 倍，移除旧的 osascript/PowerShell 外部进程方案。虽为老 PR（7 月），但性能提升显著，值得关注。

## 5. 功能需求趋势

从过去 24 小时的活跃 Issue 中可以看到社区聚焦的功能方向：

### 5.1 桌面端体验深化
- **会话内搜索**（[#19143](https://github.com/anomalyco/opencode/issues/19143)，9 评论/8 👍）：在桌面应用中实现 Cmd+F / Ctrl+F 搜索会话消息，定位长对话中的关键信息。
- **MCP 服务器桌面管理**（[#40335](https://github.com/anomalyco/opencode/issues/40335)，3 评论/2 👍）：在桌面端直接添加/编辑/测试 MCP 服务器，目前仍依赖 CLI 和手工改配置。
- **Windows 控制台窗口闪烁**（[#42440](https://github.com/anomalyco/opencode/issues/42440)）：每次执行子进程命令时弹出黑色控制台窗口，影响 Windows 11 用户。

### 5.2 会话生命周期管理
- **删除/编辑上下文消息**（[#7712](https://github.com/anomalyco/opencode/issues/7712)，12 👍）：允许用户删除无用中间步骤，减少上下文污染。
- **删除项目和会话**（[#37280](https://github.com/anomalyco/opencode/issues/37280)，2 👍）：支持从 OpenCode 中移除不再需要的项目，连带清理会话数据。

### 5.3 本地化与输入法支持
- **希伯来语 locale**（[#42447](https://github.com/anomalyco/opencode/issues/42447)）：请求新增 he 语言完整翻译。
- **IME 输入法兼容**（[#39632](https://github.com/anomalyco/opencode/issues/39632)，2 👍）：v2 输入框中 IME 首字直接上屏而非保持组词状态，中日韩用户输入会有明显挫败感。

## 6. 开发者关注点

### 6.1 Ox Alpha Free 故障持续发酵
"Endpoint is unavailable" 在 24 小时内被至少 4 个 Issue 独立报告，且带 [needs:compliance] 标签。这是当前开发者最痛的线上问题——免费模型在工具调用场景完全不可

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*