# AI CLI 工具社区动态日报 2026-08-14

> 生成时间: 2026-08-13 22:36 UTC | 覆盖工具: 7 个

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

# AI CLI 工具生态横向对比分析报告（2026-08-14）

## 1. 生态全景

2026年AI CLI赛道已进入“功能基建完成、可靠性攻坚”的阶段：头部玩家（Claude Code、Codex）放慢功能迭代，转向文档清理与安全加固；中坚力量（Gemini CLI、OpenCode）加速补位，密集发版并扩张模型生态。跨工具的高频反馈集中在三大共性痛点——生成失控/指令遵循、挂起/静默失败、MCP远程连接工程化。与此同时，跨会话记忆（Kimi #1283、OpenCode #42425）和多模型聚合（Gemini定义Claude模型、OpenCode兼容Kimi/DeepSeek）正成为新一轮差异化竞争的前沿。

---

## 2. 各工具活跃度对比

> 注：GitHub Copilot CLI 与 Qwen Code 本日无公开数据（可能静默期或数据源未收录），不计入对比。

| 工具 | 版本发布 | Issues（24h内） | PR（24h内） | 最热Issue热度 |
|------|---------|----------------|------------|--------------|
| **Claude Code** | 1个正式版（v2.1.231） | 约50条活跃，10条精选（9条文档） | 1条（CI安全加固） | #65961：110👍 |
| **OpenAI Codex** | 2个alpha预发布（rust-v0.148.0-a.11/a.12） | 约10条代表性（macOS回归/Windows兼容） | 10条（context/安全/恢复） | #34700：36👍 |
| **Gemini CLI** | 1个nightly（v0.56.0-nightly） | 约10条代表性（5条P1 bug） | 至少4条（含模型定义/重试） | #21409：8👍 |
| **Kimi Code CLI** | 无 | 3条 | 0条 | #1283：38评论 |
| **OpenCode** | 1个补丁（v1.18.18） | 约10条代表性 | 10条 | #6719：77👍 |

**活跃度画像：**
- **Codex / OpenCode**：PR最活跃（各10条），功能迭代和修复节奏最好
- **Gemini CLI**：Issue 密集且 P1 bug 占半数，处于“高速开发+稳定性欠债”状态
- **Claude Code**：PR 仅1条，Issue 以文档关闭为主，处于“消化存量”阶段
- **Kimi Code**：社区规模小，Issue 数量少但讨论质量高（#2598 有详尽复现步骤）

---

## 3. 共同关注的功能方向

### 3.1 模型输出控制与生成可靠性
| 工具 | 代表Issue | 诉求 |
|------|----------|------|
| Claude Code | #65961（110👍） | 要求忽略“不要写注释”指令，输出冗长 |
| Kimi Code | #2597 | 单步生成88k tokens乱码，需熔断机制 |
| Gemini CLI | #22323 / #25166 | Subagent超时误报成功、Shell卡死 |

**共识**：社区对“生成护栏”的诉求已超越功能层面——不仅要输出好，更要**可预期、可终止、可追责**。

### 3.2 MCP 从协议走向工程化
| 工具 | 动态 | 关注点 |
|------|------|--------|
| Claude Code | v2.1.231 修复 OAuth redirect；6条MCP相关文档 | 认证、环境变量展开、header动态化 |
| Codex | #15643 要求按RFC正确解析scopes | 企业级Remote MCP接入规范 |
| OpenCode | #42431 MCP重试；#42429 WSL命令包装 | 连接稳定性、跨环境兼容 |

**结论**：MCP的接入门槛正在从“能否连上”转向“企业级可用”（OAuth、重试、安全边界）。

### 3.3 跨会话记忆与上下文持久化
| 工具 | 动态 | 信号 |
|------|------|------|
| Kimi Code | #1283 跨会话记忆（38评论，2月至今未断） | 最强烈的长期呼声 |
| OpenCode | PR #42425 新增 agent_memory 表 | 已将记忆系统落地为DB级功能 |
| Codex | #38365 跨模型会话切换；#38445 保留client指令跨压缩 | 上下文连续性 |

**判断**：记忆/上下文持久化正从“锦上添花”变为“核心竞争点”，OpenCode 已率先动手。

### 3.4 配置体验
| 工具 | 动态 | 痛点 |
|------|------|------|
| OpenCode | #6719 请求/reload命令（77👍） | 改配置需重启 |
| Codex | #19909 会话目录不可配置（35👍） | 数据被iCloud同步 |
| Claude Code | 9条文档issue全部关于配置路径/认证 | settings.json与~/.claude.json混用 |

**趋势**：配置的“可发现性 + 热更新 + 路径稳定”是开发者留存的基础项。

### 3.5 Windows/桌面兼容性
Codex 占据了绝大部分Windows问题（#35871 MSIX pwsh、#37029 Computer Use、#35210浏览器崩溃、#33074鼠标卡顿），OpenCode 的 #42429 也在补 WSL 场景。Windows 沙箱和桌面端仍是全行业短板。

---

## 4. 差异化定位分析

| 维度 | Claude Code | OpenAI Codex | Gemini CLI | Kimi Code | OpenCode |
|------|-------------|--------------|------------|-----------|----------|
| **技术路线** | TypeScript / 内置插件市场 | Rust重写 / 双端（CLI+Desktop） | 未提及（Google生态） | 未明确 | TypeScript / 开放插件API |
| **核心优势** | MCP生态最完善、文档管理规范 | 安全治理（Guardian V2）、Rust性能 | Eval评估体系（工具调用格式化/失败摘要）、多模型定义（已加Claude模型） | 轻量、聚焦核心 | 插件模型最活跃（社区PR驱动）、聚合多提供商（Kimi/DeepSeek/xAI） |
| **主要短板** | 模型输出控制差（110👍证言）；迭代节奏放缓 | Windows兼容性大幅拖累体验；Desktop回归频发 | Agent稳定性堪忧（5个P1 bug）；社区声量相对低 | 无发布节奏；长任务缺少保护；社区规模最小 | V2迁移期破坏性变更多；远程开发（VSCode/Docker/WSL）不完善 |
| **目标用户** | 企业级/规范流程团队 | 开发者个体+安全敏感企业 | 深度Agent工作流用户 | 轻量任务/个人用户 | 插件生态爱好者/多模型用户 |

**解读**：五个工具已分化为三条路线——
- **平台路线**（Claude Code / Codex）：构建完整IDE/桌面生态，拼企业级能力
- **Agent路线**（Gemini CLI）：押注多代理协作，但目前稳定性未跟上愿景
- **社区/聚合路线**（OpenCode / Kimi）：靠插件和低门槛聚合模型，走开源社区驱动

---

## 5

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---

## Claude Code 社区动态日报 — 2026-08-14

---

### 1. 今日速览

- 官方发布 **v2.1.231**，针对 MCP OAuth 登录时 redirect URI 不匹配（尤其是 Slack 等预注册客户端）进行了修复。
- 社区最热 Issue 集中在 **模型默认输出冗长代码注释** 的问题上，获得 110 个 👍，开发者普遍反馈指令遵循仍需改善。
- PR 队列相对安静，近 24 小时仅更新 1 个 CI 安全加固 PR（SHA-pinning），同时大量文档相关 Issues 被批量关闭，暗示官方在集中清理文档积压。

---

### 2. 版本发布

**v2.1.231** 已发布。更新内容：

- 修复 MCP OAuth 登录失败：对于使用预注册 OAuth 客户端（如 Slack）的服务器，此前存在 redirect URI mismatch 问题，现已解决。

---

### 3. 社区热点 Issues

以下为过去 24 小时更新最活跃、评论数最多的 Issue（筛选 10 条最具代表性）：

**1. [模型行为] Claude 默认生成冗长代码注释，忽略停止指令**  
[#65961](https://github.com/anthropics/claude-code/issues/65961)  
作者：@bhuvarloka | 状态：OPEN | 👍 110 | 评论 11  
**为什么重要**：该 Issue 是当前社区声量最高的问题，开发者反馈 Claude 即使被明确要求也不要写注释，仍会默认产出大量冗余注释，直接影响代码生成质量。高赞数表明这不是个例，而是模型输出偏好与用户控制之间的核心矛盾。已打上 `model` 标签，预计官方会针对性调整 prompt 或模型行为。

**2. [文档] Settings 文档仍将 `/config` 配置写在 `~/.claude.json`，而非 `~/.claude/settings.json`**  
[#52601](https://github.com/anthropics/claude-code/issues/52601)  
作者：@coygeek | 状态：CLOSED | 评论 7  
**为什么重要**：全局配置路径是开发者环境搭建的基础信息，文档错误会直接导致配置不生效。该 Issue 已关闭，说明修复已合入官方文档。

**3. [文档] Worktree 文档缺失 `/tui` 与 `/update` 的会话中途行为说明**  
[#51376](https://github.com/anthropics/claude-code/issues/51376)  
作者：@coygeek | 状态：CLOSED | 评论 6  
**为什么重要**：Git worktree 并行会话是 Claude Code 多任务场景的常用能力，官方文档缺失关键时刻的行为预期，曾导致用户误操作。现已关闭并补齐。

**4. [文档] 认证文档未说明设置 `CLAUDE_CODE_OAUTH_TOKEN` 时 `/login` 的行为**  
[#52203](https://github.com/anthropics/claude-code/issues/52203)  
作者：@coygeek | 状态：CLOSED | 评论 5  
**为什么重要**：认证优先级与 token 配置是 CI/CD 集成的关键路径，文档盲区会造成自动化流程中断。

**5. [文档] 托管插件市场的 `blockedMarketplaces` 限制未记录**  
[#52611](https://github.com/anthropics/claude-code/issues/52611)  
作者：@coygeek | 状态：CLOSED | 评论 5  
**为什么重要**：企业级用户需要黑白名单能力来控制插件来源，此文档补齐对企业安全治理有直接价值。

**6. [文档] MCP 文档未覆盖 SSE/WebSocket 远程 header 的 env-var 展开**  
[#52619](https://github.com/anthropics/claude-code/issues/52619)  
作者：@coygeek | 状态：CLOSED | 评论 5  
**为什么重要**：动态 header + 环境变量展开是 MCP 远程认证的常见需求，文档缺失导致团队排查成本上升。

**7. [文档] 插件市场文档缺未经识别 source 格式的错误处理说明**  
[#53076](https://github.com/anthropics/claude-code/issues/53076)  
作者：@coygeek | 状态：CLOSED | 评论 5  
**为什么重要**：插件源格式错误时的行为不确定性会阻碍插件生态的故障排查，文档补全后有助于标准化安装反馈。

**8. [文档] 交互模式文档缺失溢出对话框的滚动控制**  
[#54162](https://github.com/anthropics/claude-code/issues/54162)  
作者：@coygeek | 状态：CLOSED | 评论 5  
**为什么重要**：交互模式的键盘导航是终端用户体验核心，溢出场景属于隐藏阻力点，官方文档现已覆盖。

**9. [文档] VS Code `/context` 命令缺失原生 token 用量弹窗行为说明**  
[#54174](https://github.com/anthropics/claude-code/issues/54174)  
作者：@coygeek | 状态：CLOSED | 评论 5  
**为什么重要**：VS Code 插件是重度用户的主要入口，`/context` 命令展示 token 用量的行为直接影响上下文管理策略。

**10. [文档] OpenTelemetry 监控文档未说明 `api_request` / `api_error` 数值型属性的类型**  
[#54471](https://github.com/anthropics/claude-code/issues/54471)  
作者：@coygeek | 状态：CLOSED | 评论 5  
**为什么重要**：OTel 属性类型（string/number）决定监控仪表盘的数据处理逻辑，类型标注缺失会造成异常埋点解析错误。现已被修正。

> 补充：这 10 个 Issue 中 9 个均为同一作者 @coygeek 提交的系统性文档勘误，标记为 `stale` 后近期被集中关闭，说明官方刚完成一批文档同步清理。社区实际功能请求声量集中在 #65961。

---

### 4. 重要 PR 进展

过去 24 小时 PR 队列仅更新 1 条，暂无新合并的功能性 PR：

**#60280 [CLOSED] CI：SHA-pin 剩余 actions/checkout 与 actions/github-script**  
[查看 PR](https://github.com/anthropics/claude-code/pull/60280)  
作者：@arpitjain099  
- **内容**：基于 #56784 的后续改进，将 6 个 worklow（`auto-close-duplicates`、`backfill-duplicate-comments`、`claude-dedupe-issues`、`claude-issue-triage` 等）中的 `actions/checkout@v4` 固定到 SHA `34e114876b0b11c390a56381ad16ebd13914f8d5`（对应 v4.3.1），并对 `actions/github-script` 做同样处理。
- **意义**：这是供应链安全加固，避免第三方 action 被篡改的风险，属于可靠性基础设施调整，对用户侧无感知但长期提升仓库安全性。

> 说明：24 小时窗口内未出现新功能或修复类 PR，核心功能改动仍以版本 v2.1.231 的 MCP OAuth 修复为主。

---

### 5. 功能需求趋势

从 50 条 Issues 中挖掘的主题分布如下：

- **文档准确性与完整性（占比最高）**：约 30+ 条 Issue 指向官方文档滞后或缺失，集中在配置路径（`settings.json` vs `~/.claude.json`）、认证流程、MCP 远程服务器、插件市场限制、worktree 行为等。这反映出 Claude Code 迭代速度较快，文档维护已成为社区痛点。
- **MCP 工程化**：除文档外，MCP 相关的认证、header 展开、重连流程被反复提及。结合最新版本对 OAuth redirect 的修复，官方正在加速 MCP 远程服务器的稳定性。
- **模型输出控制**：#65961 以 110 个 👍 成为最高关注 Issue，社区强烈希望在提示词层面能更严格地约束代码风格（尤其是注释密度）。
- **观测性与可运维性**：OpenTelemetry 监控指标、analytics 遥测披露、`cleanupPeriodDays` 保留策略等，说明企业级开发者在将 Claude Code 纳入正式研发流程时，需要更强的可观测性保障。
- **交互体验细化**：交互模式溢出对话框、Vim 模式 Esc 中断、`/color` 远程同步等 UI/UX 类问题，体现用户对终端交互细节的要求在上升。

---

### 6. 开发者关注点

- **指令遵循仍是核心痛点**：#65961 的广泛共鸣（110 👍）说明开发者希望 Claude 在“不要写注释”这类明确指令上更可靠，而不是每次都需要反复纠正。
- **配置路径混乱影响上手**：`~/.claude.json` 与 `~/.claude/settings.json` 的持久化位置不明确，导致用户配置不生效或丢失，属于高频踩坑点。
- **MCP OAuth 兼容性**：v2.1.231 修复的 redirect URI 问题证明 Slack 等预注册 OAuth 客户端的接入成本依然存在，社区期待 MCP 认证更加“开箱即用”。
- **文档同步滞后**：大量 `stale` 文档 Issue 被关闭表明问题已被解决，但在本轮集中清理前，用户至少经历了 3-4 个月的文档空白期，社区希望官方能缩短文档发布与代码发布之间的时间差。
- **供应链安全关注**：PR #60280 的 SHA-pinning 虽为底层维护，但反映出社区有开发者（@arpitjain099）在主动推动仓库安全标准，这与企业用户在 CI 中使用 Claude Code 的安全合规诉求一致。

---

**一句话总结**：本日动态以 MCP OAuth 修复和一批文档清理为主，而社区最强烈的真实呼声是——**“请让 Claude 别再说废话”**。#65961 的 110 个 👍 值得官方后续重点关注。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-08-14）

## 1. 今日速览

昨日共发布 2 个 CLI 预发布版本（rust-v0.148.0-alpha.12 / alpha.11），主要围绕 Rust 与安全加固。社区热度最高的问题集中在 macOS 桌面端「远程控制无法恢复」回归（#37403）、 `gpt-5.6-luna` 在 Windows 上无法作为 subagent 被 `spawn_agent` 调用（#34700），以及 Windows sandbox 与 MSIX PowerShell 的兼容性失败（#35871）。另有一大批 PR 集中处理 context 管理、Guardian 安全策略与 app-server 恢复逻辑。

## 2. 版本发布

| 版本 | 说明 |
|---|---|
| [rust-v0.148.0-alpha.12](https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.12) | 0.148.0-alpha.12 |
| [rust-v0.148.0-alpha.11](https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.11) | 0.148.0-alpha.11 |

两个 alpha 均为 Rust 工具链的预发布版本，Release 描述未附带详细变更日志。

## 3. 社区热点 Issues

**1. [macOS 桌面端 Remote Control / CLI 线程回归：“already has an active writer”](https://github.com/openai/codex/issues/37403)**（18 评论 / 11 👍）
8 月 7 日更新后，macOS 用户无法通过手机远程恢复 Codex CLI 线程。涉及 app-server 与 remote 双端竞态，是目前评论最集中的回归问题。

**2. [请求将 App 的 “Chats” 项目目录改为可配置](https://github.com/openai/codex/issues/19909)**（17 评论 / 35 👍）
`~/Documents/Codex` 被 iCloud Drive 同步，不适合存放编码会话。这是社区呼声最高的长期功能需求之一。

**3. [Windows App/CLI：multi_agent_v2 下 spawn_agent 拒绝 gpt-5.6-luna](https://github.com/openai/codex/issues/34700)**（15 评论 / 36 👍）
用户显式配置了 Luna 模型，但 multi-agent 流程不予识别，Windows 端常见。与 #37910、#38344 同为模型识别域问题。

**4. [Windows sandbox：MSIX 版 pwsh 导致 CreateProcessAsUserW 报错 5](https://github.com/openai/codex/issues/35871)**（13 评论）
Microsoft Store 安装的 PowerShell 7 在受限 token 下无法启动，sandbox 整体不可用。属于 Windows 平台的高频阻塞问题。

**5. [Windows Desktop IAB：browser.tabs.finalize() 会直接终止整个应用](https://github.com/openai/codex/issues/35210)**（12 评论）
内嵌浏览器插件在调用 tab 关闭接口时，进程被静默终止，无错误提示。影响自动化浏览器操作场景。

**6. [Windows 26.730.7989.0：Computer Use 在应用选择前即报 EPERM lstat](https://github.com/openai/codex/issues/37029)**（12 评论）
Computer Use 流程在 Windows 上无法启动，涉及 sandbox 与运行时文件访问权限，目前无绕过方案。

**7. [Codex Desktop 重启后错误的将已关闭 subagent 恢复为 Working](https://github.com/openai/codex/issues/37563)**（12 评论 / 4 👍）
已完成或中止的子代理在重启桌面后重新显示为工作状态，导致会话状态混乱。与 #37042 属同族问题。

**8. [Windows 持久化插件缓存 hash 路径导致旧线程丢失 skills](https://github.com/openai/codex/issues/25285)**（10 评论）
插件目录名称不稳定，缓存更新后旧会话无法解析 `SKILL.md` 绝对路径，技能加载持续失败。

**9. [Remote MCP：scopes_supported 应从 resource metadata 文档提取](https://github.com/openai/codex/issues/15643)**（7 评论 / 14 👍）
当前以 `.well-known/oauth-protected-resource` 等方式获取 scope 不符合规范，企业级 Remote MCP 集成受阻。

**10. [Windows Codex 启动/任务切换时鼠标卡顿](https://github.com/openai/codex/issues/33074)**（7 评论 / 9 👍）
CPU/磁盘未饱和但物理鼠标操作受影响，重装系统后仍复现，疑似渲染线程或输入处理优先级问题。

> 备注：#36523 （[macOS 启动时 OOM：external-agent-import 解析 1.73 GB Claude 数据](https://github.com/openai/codex/issues/36523)）被标记为 P0 回归，虽本周评论较少，但影响严重，上线前应重点验证。

## 4. 重要 PR 进展

**1. [Refresh current-time reminders for full-history subagents](https://github.com/openai/codex/pull/38446)**
防止父会话的当前时间提醒被复制到全历史子代理中，避免继承提醒累积，保留子代理新生成的提醒。

**2. [Retain client developer messages across context compaction](https://github.com/openai/codex/pull/38445)**
上下文压缩后，保留客户端开发者编写的指令（当启用 `retain_client_developer_messages` 时）。解决长期会话指令丢失问题。

**3. [Tag current time reminders in model context](https://github.com/openai/codex/pull/38443)**
将注入的当前时间提醒包装为 `<current_time_reminder>` 标签，同时保持 `clock.curr_time` 工具输出为明文，提升模型对系统注入信息的可辨识度。

**4. [Give Guardian V2 full tool action context](https://github.com/openai/codex/pull/38441)**
将原始 `ToolPayload`（含工具调用参数与对话上下文）暴露给工具生命周期 hook，使 Guardian 能更准确判断风险。

**5. [Add app-server support for reverting paginated threads](https://github.com/openai/codex/pull/38440)**
实验性 `thread/revert` 请求：将分页线程回退到指定 `beforeTurnId` 前缀，同时保留线程 ID，并中断正在执行的 turn。

**6. [Resolve local MCP refs in Code Mode tool schemas](https://github.com/openai/codex/pull/31901)**
Code Mode 渲染 TypeScript 工具声明时，支持解析 JSON Pointer `$ref`（含 `#/$defs/...`、`#/definitions/...`，支持 RFC 6901 转义）。

**7. [Preserve approval policies for auto-reviewed models](https://github.com/openai/codex/pull/38439)**
当模型命中 `auto_review.required_on_models` 且选择自动评审器时，保留用户配置的 `approvalPolicy`，不再降级为 workspace-write。

**8. [exec-server: start managed network proxy on executor](https://github.com/openai/codex/pull/31453)**
将脱敏后的受管网络策略发送至远程 exec-server 进程，并在执行端启动 HTTP/SOCKS 代理；在 MITM、凭据注入到达边界前 fail-closed。

**9. [Add rustls fallback for local MCP HTTP requests](https://github.com/openai/codex/pull/38436)**
本地 MCP 请求在平台 TLS 后端协商失败后，自动使用 rustls 重试一次，修复部分 HTTPS 端点的连接问题。

**10. [Gate Node REPL Guardian guidance on model metadata](https://github.com/openai/codex/pull/38432)**
仅当父 turn 模型声明 `node_repl_auto_review_required` 时才使用专门的 Node REPL 审批提示，避免对普通 JS 执行过度安全提示。

## 5. 功能需求趋势

- **Vim 模式体验补全**（#21850、#32745、#33296）：社区连续提交多个增强请求，覆盖默认 Insert 模式、`c*` change 操作、基础按键缺失等问题。Vim 模式当前可用性不足以作为日常编辑方式，是 CLI 用户高频反馈区。
- **会话/文件目录可配置**（#19909）：默认 `~/Documents/Codex` 路径与 iCloud 同步冲突，社区期望将 Chats 目录纳入配置项。
- **会话跨模型/跨提供商切换**（#38365）：用户希望将长会话从 GPT 延续到自定义模型供应商时，工具历史能被规范化并可靠传输。
- **`gpt-5.6-luna` 的 subagent 支持**（#34700、#37910、#38344）：多个平台（Windows/macOS）出现同一模型在主线程可用、在 subagent 启动时被拒的问题，属于当前模型矩阵与 multi-agent 集成的前沿缺口。
- **GitHub review connector 配额错误信息改进**（#38405）：安全评审配额耗尽时仅显示“try again later”，用户期待明确的重试时间和具体配额策略。

## 6. 开发者关注点

- **远程恢复与断线恢复**：#37403、#37719 显示 CLI/Desktop 的线程恢复机制在版本迭代中不稳定，“active writer”竞态与持久化失败是高发根因。
- **Subagent 状态不一致**：#37563、#37042 表明页面重载后子代理状态还原逻辑不可靠，影响多代理任务追踪与回溯。
- **Windows sandbox 兼容性**：#35871、#37029、#19599 覆盖 MSIX pwsh、Computer Use、映射网络驱动器三类场景，Windows 沙箱成熟度仍是平台短板。
- **插件/技能数据持久化**：#25285 暴露插件缓存 hash 不稳定导致技能丢失；#38342 报告启用技能后 MCP 工具缺失，插件状态一致性有待验证。
- **安全策略与审批流**：多个人工智能自动审批、Guardian 上下文增强、filesystem 权限修复的 PR 密集合入，说明服务端在安全评估与权限收敛上正快速迭代，但用户侧仍会先经历一段行为变化期。

---

**数据来源**：GitHub `openai/codex` 仓库（采集时间：2026-08-14）。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-14

## 今日速览

昨日发布 v0.56.0-nightly 版本，主要聚焦 eval 评估体系增强（新增工具调用格式化与失败摘要集成）。社区端围绕 Agent 稳定性问题讨论热烈：多个 P1 级 bug 仍在发酵，包括 Subagent 超时误报成功、通用 Agent 挂起、Shell 命令执行后卡死等高频痛点。PR 方面亮点不少：新增 Claude Sonnet 4.5 / Opus 4.8 模型定义，以及容量错误重试、取消回滚、A2A 安全加固等关键修复。

---

## 版本发布

**v0.56.0-nightly.20260813.g1ac337739**（2026-08-13）

主要变更：
- `feat/evals`: 新增工具调用格式化器，并集成失败摘要（#28344）
- `feat(evals)`: 添加工具调用格式化器并整合失败摘要（#28305）
- 同步 v0.55.1 变更日志

🔗 [查看 Release 详情](https://github.com/google-gemini/gemini-cli/releases)

---

## 社区热点 Issues（10 条精选）

### 1. Subagent 超时后误报为 GOAL 成功 — 隐藏真实中断
**#22323** | [P1/bug](https://github.com/google-gemini/gemini-cli/issues/22323) | 评论 12 | 👍 2

`codebase_investigator` 子代理在达到最大轮次限制后，仍报告 `status: "success"` 且终止原因为 `GOAL`，但实际上并未执行任何分析。该问题会直接误导用户对任务结果判断，评论中最集中的讨论点在于「如何区分正常终止与强制中断」。

---

### 2. Generalist Agent 无限期挂起
**#21409** | [P1/bug](https://github.com/google-gemini/gemini-cli/issues/21409) | 评论 8 | 👍 8

用户反馈一旦 CLI 将任务委托给 generalist agent，就会无限期挂起（等过 1 小时无响应）。简单的文件夹创建操作也会触发。社区共鸣强烈（8 个 👍），临时规避方案是显式指示模型不要使用子代理。

---

### 3. Shell 命令执行完仍卡在 "Waiting input"
**#25166** | [P1/bug](https://github.com/google-gemini/gemini-cli/issues/25166) | 评论 4 | 👍 3

执行极简单的 CLI 命令后，终端仍显示命令活跃并等待输入，实际命令早已完成。涉及核心 shell 执行的可靠性，是开发者日常使用中非常恼人的卡顿点。

---

### 4. get-shit-done 输出钩子在打印摘要时崩溃
**#22186** | [P1/bug](https://github.com/google-gemini/gemini-cli/issues/22186) | 评论 3

当 get-shit-done 任务接近完成、打印用户摘要阶段时，CLI 反复崩溃。该问题影响长任务收尾阶段的可靠性，暂未见官方回应。

---

### 5. Browser Subagent 在 Wayland 环境下失败
**#21983** | [P1/bug](https://github.com/google-gemini/gemini-cli/issues/21983) | 评论 4 | 👍 1

浏览器子代理在 Wayland 显示服务器下无法正常工作，涉及 Linux 桌面用户的浏览器自动化场景。

---

### 6. Subagent 未经许可自动运行（v0.33.0 回归）
**#22093** | [P2/bug](https://github.com/google-gemini/gemini-cli/issues/22093) | 评论 3

配置中已禁用 Agents 模式和子代理，更新到 v0.33.0 后 subagent 仍被自动调用（如 generalist）。用户明确表示只期望 MCP 功能，但子代理绕过配置执行。

---

### 7. Auto Memory 安全：缺少确定性脱敏且日志过多
**#26525** | [P2/security](https://github.com/google-gemini/gemini-cli/issues/26525) | 评论 4

Auto Memory 读取本地转录并发送给后台提取模型时，提示词要求脱敏发生在内容进入模型上下文之后，且服务会记录现有技能信息。属于「先发送后脱敏」的安全时序问题，社区关注点集中在数据隐私。同一系列的 #26522（低信号会话无限重试）、#26523（无效补丁静默跳过）、#26516（汇总）也值得关注。

---

### 8. 超过 128/400 个工具时报 400 错误
**#24246** | [P2/bug](https://github.com/google-gemini/gemini-cli/issues/24246) | 评论 3

当可用工具数量超过一定阈值（用户报告 400+）时，Gemini CLI 返回 400 错误。社区期望 Agent 能更智能地按需裁剪工具范围，而非全量加载。

---

### 9. AST 感知文件读取、搜索与代码库映射探索
**#22745** | [P2/EPIC](https://github.com/google-gemini/gemini-cli/issues/22745) | 评论 7

EPIC 型 issue，系统评估 AST 感知工具对代码读取、搜索和 mapping 的价值。潜在收益包括：单次调用精确读取方法边界、减少 token 噪音、提升导航准确性。多个子任务追踪中。

---

### 10. `~/.gemini/agents/` 中的 symlink 不被识别为 Agent
**#20079** | [P2/bug](https://github.com/google-gemini/gemini-cli/issues/20079) | 评论 4

用户将 Agent 定义文件以符号链接形式放入 `~/.gemini/agents/` 时不被识别。影响使用 dotfiles 或多目录管理 Agent 的高级用户。

---

## 重要 PR 进展（10 条精选）

### 1. 新增 Claude Sonnet 4.5 与 Opus 4.8 模型定义
**#28803** | [已合并](https://github.com/google-gemini/gemini-cli/pull/28803) | size/xl

新增 `claude-sonnet-4-5` 和 `claude-opus-4-8` 模型常量、别名解析及策略链回退，同步更新 `DEFAULT_MODEL_CONFIGS`。对多模型用户是实质性扩展。

---

### 2. 容量错误支持上下文感知静默重试
**#28790** | [已合并](https://github.com/google-gemini/gemini-cli/pull/28790) | P1, size/l

修复 #28761 容量耗尽重试回归。非交互式运行遇到容量错误时自动退避重试，最多增加 2 次静默重试，显著提升无人值守场景的稳健性。

---

### 3. 取消/中止时回滚整个多轮请求
**#28801** | [已合并](https://github.com/google-gemini/gemini-cli/pull/28801) | size/m

解决取消多轮带工具调用的请求后，聊天历史残留在未响应状态的问题。新请求会基于完整历史执行，避免上下文错乱。

---

### 4. 规范化 Git 环境，解决工作区状态不一致
**#28792** | [已合并](https://github.com/google-gemini/gemini-cli/pull/28792) | size/l

统一 Git 子进程的环境配置，修复工作区信任评估的初始化问题。确保内部 Git 工具在仓库间可预测、非

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-08-14

## 今日速览
过去24小时，Kimi Code CLI 无新版本发布，也无新增或合并的 PR 动态，社区热度集中在三个悬而未决的 Issue 上：呼声已久的跨会话记忆系统（#1283）仍在持续升温；ACP/print 流式响应“静默挂死”问题（#2598）引发对生产稳定性的讨论；另一起单步生成 88k tokens 乱码的失控事件（#2597）则暴露了长任务下缺少保护机制的风险。整体来看，开发者的反馈集中在**可靠性、可观测性与持久上下文**三大方向。

## 版本发布
过去24小时无新版本发布。

## 社区热点 Issues
过去24小时内有更新的 Issue 共 3 条，均已纳入分析。

### 1. #1283 [增强] 记忆系统——跨会话上下文持久化（社区最热）
- 作者：@CatKang | 创建：2026-02-27 | 更新：2026-08-13 | 评论：38 | 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1283
- 为什么重要：这是仓库中讨论时间最久、评论最多的长期功能请求之一。用户希望 CLI 具备真正的“记忆”，能跨会话记住项目模式、用户偏好和上下文，让 Kimi Code CLI 像资深协作者一样“越用越懂你”。38 条持续评论表明社区对这一能力的诉求非常强烈。
- 社区反应：Issue 自今年二月创建至今讨论未断，属于典型的“高频呼唤但尚未落地”的核心功能，对产品方向判断很有参考价值。

### 2. #2598 [Bug] ACP/print 流式响应静默挂死：无空闲超时，被顶替轮 partial 不落 wire
- 作者：@ai-agent-workbench | 创建：2026-08-09 | 更新：2026-08-13 | 评论：1 | 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2598
- 为什么重要：直接影响 ACP 模式下的自动化体验。现象是内容 delta 已全部到达，但 `[DONE]`/finish 帧始终不来，CLI 无限等待；用户发下一条消息时，挂死轮被静默顶替，且已流式内容**未写入 wire.jsonl**。更关键的是，用户明确指出 0.31.1 的修复只覆盖了 Esc 场景，本次报告的场景仍然存在。
- 社区反应：该 Issue 提供了非常详尽的现象描述、版本信息，并引用官方 config.toml 文档确认“无空闲超时配置项”，对维护者复现有很高价值。

### 3. #2597 [Bug] 失控乱码生成——单次 LLM 步骤产出 88k tokens
- 作者：@kdp123 | 创建：2026-08-08 | 更新：2026-08-13 | 评论：1 | 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2597
- 为什么重要：一次普通交互会话中，单个 LLM 步骤运行了 **3214 秒（约 53 分钟）**，输出 **88,114 个 token** 的重复乱码，包含多语言碎片、损坏的 Markdown 和无限重复。这不仅是模型行为异常，更意味着持续的 API 费用消耗和终端资源占用，对生产环境工具是不可接受的。
- 社区反应：评论数虽少，但问题严重度高，开发者普遍关心是否已有“生成熔断”或“token 上限”保护机制。

## 重要 PR 进展
过去24小时内无 PR 更新（0 条）。结合 Issue 区动态，社区正在期待以下方向出现修复 PR：

- 针对 **#2598** 的 ACP/print 流式挂死修复（尤其是空闲超时与 wire.jsonl 写入）
- 针对 **#2597** 的输出 token 上限与异常生成熔断机制
- 针对 **#1283** 记忆系统的落地实现

我们将在后续日报中持续追踪对应 PR 进展。

## 功能需求趋势
从当前全部更新中的 Issue 来看，社区最关注的功能方向可提炼为三点：

1. **跨会话记忆与上下文持久化（#1283）**  
   用户不满足于单次会话内的上下文，希望 CLI 能自动沉淀项目结构、编码规范和个人偏好，形成可持续积累的长期记忆。这是当前呼声最高、讨论最深的功能诉求。

2. **流式连接健壮性与可配置超时（#2598）**  
   开发者在自动化场景中对“无限等待”零容忍。需求集中在：空闲超时配置项、心跳/keep-alive 机制、以及挂死后的自动重连或降级策略。

3. **生成安全护栏（#2597）**  
   用户希望为模型输出设置硬性上限（如 max_tokens）、异常重复检测与自动终止机制，避免单次失控生成拖垮整个会话。

## 开发者关注点
来自 Issue 反馈中的高频痛点与诉求：

- **可靠性已成为首要关注点**：多个问题都指向“静默失败”——无报错、无超时、无日志落盘，导致排障无从下手。开发者认为这是阻碍 CLI 进入生产流程的关键障碍。
- **可观测性亟需增强**：#2598 中提到的 wire.jsonl 缺失 `content.part` 与 `usage.record`，让用户无法追溯被顶替轮次的完整数据，这类透明度的缺失严重削弱信任感。
- **长任务需要资源保护**：#2597 的单次 53 分钟、88k tokens 的失控生成，让开发者警惕 API 成本失控风险，呼吁加入硬性上限与熔断机制。
- **补丁覆盖范围受关注**：有用户明确指出 0.31.1 对挂死场景的修复并不完整（仅覆盖 Esc 场景），反映出社区对“修复是否彻底”和回归风险的高要求。

---
*数据来源：[github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)，统计窗口：2026-08-14 日报。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-14

## 1. 今日速览

昨日发布补丁版本 v1.18.18，修复了 Kimi 系统提示词选择错误及 xAI 模型 reasoning effort 设置问题。社区方面，围绕新布局去留、插件系统回归、V2 版本数据兼容性等话题讨论激烈，同时一批由 @herjarsa 提交的高质量 PR 覆盖了 MCP 重试、技能发现、模型回退链等多项稳定性改进。

## 2. 版本发布

### v1.18.18
**核心 Bug 修复**：
- 为官方 Moonshot 和 Kimi 提供商正确选择 Kimi 系统提示词
- 修复 xAI 模型的 xhigh reasoning effort 设置问题

🔗 https://github.com/anomalyco/opencode/releases/tag/v1.18.18

## 3. 社区热点 Issues（10 条）

### 3.1 旧布局去留之争 — #37012
**作者**: @darkine24th | **评论**: 37 | **👍**: 41 | **状态**: OPEN

用户强烈要求保留旧版布局，指出旧版可从主窗口直达几乎所有功能，且支持工作区。该 issue 已持续一个月，获得大量 👍 支持，是社区对 UI 改版最集中的反馈。

🔗 https://github.com/anomalyco/opencode/issues/37012

### 3.2 VSCode Server 环境剪贴板失效 — #41470
**作者**: @WqxLoveCoding | **评论**: 15 | **👍**: 1 | **状态**: OPEN

在 Docker 环境的 VSCode Server 中使用 OpenCode 时，"Copied to clipboard" 提示出现但剪贴板实际未写入。影响远程开发场景的用户。

🔗 https://github.com/anomalyco/opencode/issues/41470

### 3.3 插件 provider.models() 钩子回归 — #25630
**作者**: @ErcinDedeoglu | **评论**: 15 | **👍**: 6 | **状态**: OPEN

PR #25167 合并后，插件 `provider.models()` 钩子无法再为自定义提供商填充模型。影响深度依赖插件扩展模型生态的用户，属于插件 API 的回归性问题。

🔗 https://github.com/anomalyco/opencode/issues/25630

### 3.4 请求新增 /reload 命令 — #6719
**作者**: @wojons | **评论**: 15 | **👍**: 77 | **状态**: OPEN

社区强烈希望添加一个 `/reload` 斜杠命令，用于重载全局和项目级 `opencode.jsonc` 配置及 `.opencode/` 目录。77 个 👍 表明这是最高频的效率需求之一。

🔗 https://github.com/anomalyco/opencode/issues/6719

### 3.5 DeepSeek V4 Flash Free 鉴权失败 — #42293
**作者**: @cbrunschen | **评论**: 12 | **👍**: 0 | **状态**: CLOSED

OpenCode Zen 上的 DeepSeek V4 Flash Free 请求大部分失败，报 `invalid_bearer_credential` 错误。用户反馈 1.18.3 升级至 1.18.18 后问题依旧。已关闭但值得关注。

🔗 https://github.com/anomalyco/opencode/issues/42293

### 3.6 官方宣传"100% 免费"与实际订阅矛盾 — #42143
**作者**: @mahmoud-Web-Developer | **评论**: 8 | **👍**: 1 | **状态**: OPEN

用户质疑官网标注"100% 免费"但实际要求订阅。属于文档/定价信息与产品行为不一致的反馈。

🔗 https://github.com/anomalyco/opencode/issues/42143

### 3.7 TypeScript LSP 无法识别子目录 package.json — #18694
**作者**: @x1unix | **评论**: 7 | **👍**: 13 | **状态**: OPEN

当 `package.json` 和 `node_modules` 位于仓库子目录（如 Go+React 项目）时，以仓库根目录运行 opencode 无法使用 TypeScript LSP。影响多语言项目开发者。

🔗 https://github.com/anomalyco/opencode/issues/18694

### 3.8 GitHub Copilot 提供商模型为空 — #42083
**作者**: @Keylessboi | **评论**: 5 | **👍**: 1 | **状态**: OPEN

1.18.15 中 `github-copilot` 提供商登录成功但模型列表中不显示任何模型，`opencode models` 返回 "Provider not found"。

🔗 https://github.com/anomalyco/opencode/issues/42083

### 3.9 无限重试循环 — #29143
**作者**: @niStee | **评论**: 4 | **👍**: 0 | **状态**: CLOSED

当提供商持续失败时，回退系统会陷入无限重试循环，应限制重试次数（如 5 次）以便切换到下一个配置的模型。

🔗 https://github.com/anomalyco/opencode/issues/29143

### 3.10 会话标题被注入内容污染 — #23114
**作者**: @marcusyoung | **评论**: 4 | **👍**: 1 | **状态**: OPEN

会话标题生成时使用了注入到系统提示词中的记忆/上下文数据，而非实际用户消息，导致标题生成不准确。

🔗 https://github.com/anomalyco/opencode/issues/23114

## 4. 重要 PR 进展（10 个）

### 4.1 新增 agent_memory 表与记忆工具插件 — #42425
**作者**: @herjarsa | **状态**: OPEN

新增 `agent_memory` 数据库表和 `memory-tools` 插件，支持通过 Supabase 进行 OpenCode AgentMemory 的云端备份/恢复。对应 issue #41998。

🔗 https://github.com/anomalyco/opencode/pull/42425

### 4.2 插件自动更新失败修复与临时残留清理 — #42427
**作者**: @herjarsa | **状态**: OPEN

修复 `@latest` 插件自动更新卡住的问题，并添加 npm install 后的临时残留清理。绕过本地缓存直接从 registry.npmjs.org 获取 `dist-tags.latest`。

🔗 https://github.com/anomalyco/opencode/pull/42427

### 4.3 实验性性能改进（v2） — #40427
**作者**: @Hona | **状态**: OPEN

针对 v2 的缩减版性能优化系列，涵盖会话路由加载等关键路径。表格显示会话页面加载等指标在 PR 行为下有显著提升。

🔗 https://github.com/anomalyco/opencode/pull/40427

### 4.4 模型回退链 — #42424
**作者**: @herjarsa | **状态**: OPEN

当主模型所有重试耗尽后，自动按配置的 `fallback` 链切换到备用模型。对应 issue #10287。

🔗 https://github.com/anomalyco/opencode/pull/42424

### 4.5 新布局工作区流程 — #38790
**作者**: @Hona | **状态**: OPEN

为新布局添加工作区选择流程：可在本地仓库、隔离的新工作区、或现有工作区之间选择开始会话；composer 位置选择器显示分支上下文。

🔗 https://github.com/anomalyco/opencode/pull/38790

### 4.6 MCP 连接重试机制 — #42431
**作者**: @herjarsa | **状态**: OPEN

修复并发启动 MCP 服务器时的 "Connection closed" 间歇性错误。对应 issue #41996。

🔗 https://github.com/anomalyco/opencode/pull/42431

### 4.7 技能发现前确保插件配置钩子已运行 — #42430
**作者**: @herjarsa | **状态**: OPEN

确保插件的 `config()` 钩子在技能发现前执行，使 superpowers 等插件通过 `config.skills.paths` 注册的技能目录能被正确识别。

🔗 https://github.com/anomalyco/opencode/pull/42430

### 4.8 WSL 模式下 MCP 命令包装 — #42429
**作者**: @herjarsa | **状态**: OPEN

桌面应用在 Windows + WSL 模式下，MCP 本地配置的 Linux 可执行文件无法在 Windows 环境中运行，现自动用 `wsl.exe` 包装。

🔗 https://github.com/anomalyco/opencode/pull/42429

### 4.9 Kimi K2.6 自定义处理器 — #42428
**作者**: @herjarsa | **状态**: OPEN

为 `kimi-for-coding` 提供商添加自定义处理器并修复 k2p6（Kimi K2.6）的模型检测问题。对应 issue #23933。

🔗 https://github.com/anomalyco/opencode/pull/42428

### 4.10 TUI 任务状态颜色规范与图标 — #42426
**作者**: @herjarsa | **状态**: OPEN

为 TUI 添加统一的任务状态颜色约定和图标：成功为绿色、错误为红色等。对应 issue #24404。

🔗 https://github.com/anomalyco/opencode/pull/42426

## 5. 功能需求趋势

从本期 Issues 中可提炼出以下社区重点关注方向：

| 方向 | 代表 Issues | 热度信号 |
|------|------------|---------|
| **UI/布局** | #37012 保留旧布局、#42369 TUI 右侧活动面板 | 37 条评论、41 👍 |
| **插件系统完善** | #25630 provider.models() 回归、#30526 插件依赖漂移、#18544 手动插件更新命令 | 多渠道反馈 |
| **新模型/提供商支持** | #42428 Kimi K2.6、#42293 DeepSeek V4 Flash Free、#42083 GitHub Copilot | 模型生态活跃 |
| **配置热重载** | #6719 `/reload` 命令 | 77 👍 的高赞需求 |
| **稳定性与重试机制** | #29143 无限重试循环、#42424 模型回退链 | 用户对可靠性诉求强 |
| **V2 兼容性** | #42421 TODO 工具缺失、#42260 数据库迁移破坏 V1 | 新版本迁移阵痛 |
| **隐私与安全** | #39931 bash 权限绕过、#34344 免费模型滥用、#42288 联网行为控制 | 安全治理关注 |

## 6. 开发者关注点

**高频痛点**：

1. **插件生态兼容性** — `provider.models()` 钩子回归导致自定义提供商不可用（#25630），插件安装后依赖残留与启动变慢（#30526），提示社区对插件系统的稳定性极为敏感。

2. **远程开发支持不足** — VSCode Server/Docker 下剪贴板失效（#41470）、WSL 下 MCP 命令无法执行（#42429），远程开发场景是当前明显的体验短板。

3. **新旧版本过渡摩擦** — V2 删除了 TODO 工具（#42421）、共享数据库导致 V1 被迁移破坏（#42260），用户对升级犹豫，社区要求保留旧布局的呼声强烈（#37012）。

4. **配置与工作流效率** — 缺少 `/reload` 命令需手动重启（#6719）、TypeScript 多目录项目 LSP 无法识别（#18694），开发者期待更顺畅的配置与多语言项目体验。

5. **免费模型可靠性质疑** — DeepSeek V4 Flash Free 鉴权失败（#42293）、mimo v2.5 响应极慢（#42382）、免费模型被 VPN 绕过滥用（#34344），免费层级的 SLA 与公平性问题需要关注。

6. **会话数据完整性问题** — 标题生成被注入内容污染（#23114、#42386）、AI SDK 丢弃 modelId（#42420），会话元数据的准确性影响用户的搜索与回溯体验。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*