# AI CLI 工具社区动态日报 2026-08-04

> 生成时间: 2026-08-03 22:35 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-08-04）

## 1. 生态全景

当前 AI CLI 工具已从“单点代码生成”快速演进为**具备 Agent 调度、MCP 集成、多模型切换、桌面化形态的完整开发前端**。OpenAI Codex、Gemini CLI、GitHub Copilot CLI、Qwen Code 均在 24 小时内保持高频发布与社区反馈闭环，其中 MCP 生态和 Agent 子代理可靠性成为共同攻坚方向。Windows/WSL 跨平台兼容问题在多个工具中集中爆发，反映出开发环境异构性已成为规模化采用的主要摩擦点。整体而言，工具链正在从“能用”向“稳定、可控、可治理”过渡，但成熟度分化明显。

## 2. 各工具活跃度对比

> 注：Claude Code、Kimi Code CLI、OpenCode 在 2026-08-04 未提供社区动态摘要，以下为“—”。

| 工具 | 热点 Issues 数 | PR 数（列出的） | Release 情况 |
|---|---|---|---|
| OpenAI Codex | 10 | 6（另有 20+ 内部自动化 PR 合并） | 2 个 Rust alpha 预发布 |
| Gemini CLI | 10 | 10 | 1 个 nightly |
| GitHub Copilot CLI | 10 | 0（24h 内无新 PR） | v1.0.78-3 正式补丁 |
| Qwen Code | 10（另有 1 个发布阻塞 Issue） | 10 | v0.21.4 正式版 + 1 个 nightly |
| Claude Code | — | — | — |
| Kimi Code CLI | — | — | — |
| OpenCode | — | — | — |

## 3. 共同关注的功能方向

### 3.1 MCP 生态的稳定性与安全管控
- **OpenAI Codex**：新增 Agent Plugins MCP 配置解析、MCP 工具按 surface 暴露控制、stdio helper 进程清理。
- **Gemini CLI**：修复 MCP OAuth token 刷新、完善 MCP 同意书展示（env/cwd/headers）、加固 stdio 环境变量传递。
- **Copilot CLI**：企业托管策略枚举校验失败导致 MCP 服务器被阻断；Actions 中 GITHUB_TOKEN 获取 MCP 策略返回 403。
- **Qwen Code**：SDK-Embedded MCP 工具在恢复会话后失效；重复 provider tool call ID 报错；MCP 热重载残留问题。

**结论**：MCP 已从“接入能力”进入“生产级治理”阶段，认证、策略、生命周期管理是各工具重点补课区域。

### 3.2 Agent 子代理的可信度与资源回收
- **OpenAI Codex**：Subagent 泄漏 stdio MCP helper 进程树。
- **Gemini CLI**：Subagent 将 MAX_TURNS 中断误报为成功；generalist agent 无限挂起；shell 命令卡死。
- **Qwen Code**：Fork agents 继承兄弟 fork 指令导致上下文污染。

**结论**：子代理的“误报成功/挂起/泄漏”会系统性破坏自动化可信度，已成为 agent 工程质量的核心矛盾。

### 3.3 多模型与 BYOK 灵活性
- **Copilot CLI**：`/model` 无法切换本地 BYOK 模型；单环境变量绑定单模型。
- **OpenAI Codex**：用户对 Sol 模型上下文缩水高度敏感（Pro 订阅用户）。
- **Qwen Code**：Bailian Token Plan 模型列表不同步。

**结论**：用户不再接受“单模型锁定”，模型可切换、透明规格、动态配置是增强粘性的关键。

### 3.4 跨平台（Windows / WSL）兼容性
- **OpenAI Codex**：WSL 仓库误判为非 Git；OneDrive 断流；WSL 下 Node REPL 路径不匹配。
- **Copilot CLI**：WSL2 下 Ctrl+H 被误判为 Ctrl+Backspace；原生 Windows 终端序列混入。
- **Qwen Code**：Windows 桌面版会话静默删除（ACP workspace cwd 不匹配）。

**结论**：Windows/WSL2 混合环境仍是稳定性短板，多个工具在此出现 P1/P2 级回归。

### 3.5 上下文管理与缓存优化
- **Gemini CLI**：工具执行中断导致上下文损坏；Auto Memory 对低信号会话无限重试。
- **OpenAI Codex**：线程导航因元数据无界膨胀变慢。
- **Qwen Code**：Size-triggered 微压缩反复失效提示缓存。

**结论**：上下文管理不再是“省钱”问题，而是直接影响正确性和响应速度的基础设施缺陷。

## 4. 差异化定位分析

| 工具 | 功能侧重 | 目标用户 | 技术路线特征 |
|---|---|---|---|
| **OpenAI Codex** | MCP 接入、Git 进程治理、桌面/云同步边界 | 重度使用 GPT 模型的开发者、远程办公团队 | 高频内部自动化重构（copyberry[bot] 批量合入 PR）、Rust 重写推进、预发布验证型迭代 |
| **Gemini CLI** | Agent 子代理可靠性、安全加固（OAuth/脱敏）、AST 感知代码理解 | 对 Agent 自主性和可观测性要求高的团队 | 问题驱动+防御性编程（大量针对边界条件的修复）、EPIC 探索 AST 导航 |
| **GitHub Copilot CLI** | 多模型/BYOK、插件作用域管理、企业策略适配 | GitHub 生态用户、企业级托管环境 | 跟随 GitHub 官方模型与政策演进、以补丁形式快速修复、重视 TUI 交互细节 |
| **Qwen Code** | Web Shell 桌面化、渠道集成（GitHub/Email/音频）、可信运行时 | 中文用户、阿里云 Bailian 生态、多模态场景 | 正式版+nightly 双轨，功能迭代快；强调确定性工具执行和外部工具守卫，向可信 Agent 运行时演进 |

## 5. 社区热度与成熟度

- **OpenAI Codex**：社区活跃度高，自动化 PR 合入量大，但发布均为 alpha 预发布，处于快速迭代和稳定性加固并行阶段。Issue 集中于 Windows/WSL 和模型透明度，用户基数大。
- **Gemini CLI**：P1 级问题密集，社区对 Agent 信任度高度敏感，PR 覆盖安全、上下文、MCP 等核心链路，属于“边跑边修”的快速成长期。
- **GitHub Copilot CLI**：发布节奏稳定（补丁版本），社区讨论聚焦模型策略和插件能力，但 24h 无新 PR，进入相对平稳的功能打磨期。
- **Qwen Code**：正式版发布后 bug 集中暴露（桌面端、MCP、缓存），同时新功能（渠道集成、守卫 Provider）持续推进，处于功能扩张与稳定性博弈期。
- **Claude Code / Kimi Code / OpenCode**：当日无公开动态，无法评估，但这也提示其在社区开放透明度上可能弱于上述四家。

## 6. 值得关注的趋势信号

1. **MCP 进入治理时代**：单纯“能连”已不够，OAuth 刷新、策略校验、进程回收、surface 级权限控制成为标配。开发者选择工具时，应重点考察其对 MCP server 生命周期的管控能力。

2. **Agent 可信度是下一场战役**：子代理误报成功、静默失败、上下文污染等问题的讨论密度，预示着“结果可验证”将成为 AI CLI 的核心竞争力。企业采用前需评估工具的审计与确认机制。

3. **BYOK 和多模型切换从“可选”变为“刚需”**：用户希望在同一会话内灵活切换 cloud/本地/不同厂商模型。无法提供这一能力的工具将在模型多元化趋势中流失用户。

4. **Windows/WSL 适配决定开发者的日常幸福感**：多个 P1/P2 问题集中在文件系统（OneDrive、ext4）、终端按键、路径映射。面向企业推广时，跨平台稳定性是前提条件。

5. **确定性工具执行成为新范式**：Qwen Code 的“外部工具守卫”和“确定性工具执行边界”提案，体现了将 LLM 置于信任边界之外、通过运行时约束动作的思路。这可能是下一阶段 AI CLI 的安全架构方向。

6. **上下文管理进入精细化阶段**：提示缓存被无效压缩、线程元数据膨胀、Auto Memory 低效重试等细节问题，直接影响成本和延迟。工具的内存策略设计将逐步从“启发式”走向“可解释、可干预”。

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

# OpenAI Codex 社区动态日报（2026-08-04）

## 1. 今日速览

昨日社区热度集中在 **Windows/WSL 集成稳定性** 与 **模型配置/配额** 两大方向，OneDrive 断流（#35420）与 GPT-5.6 Sol 上下文缩水（#31860）成为讨论焦点。工程侧则以 `copyberry[bot]` 自动提交的 20+ 个 PR 为主，覆盖 **MCP 工具管控、Git 进程清理、模型指令整合** 等内部重构，可见官方正在密集推进稳定性修复。两个 Rust alpha 版本（`v0.147.0-alpha.6`、`v0.147.0-alpha.1.2`）已发布，均未附带详细变更日志。

## 2. 版本发布

| 版本 | 说明 |
|---|---|
| [rust-v0.147.0-alpha.6](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.6) | 预发布，无详细变更日志。 |
| [rust-v0.147.0-alpha.1.2](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.1.2) | 预发布，无详细变更日志。 |

两个版本接近同期发布，结合昨日大量内部 PR 合并，推测 `0.147.0` 主线包含 MCP 配置解析、权限注入优化等行为变更，但尚未在 changelog 中公开，建议关注后续稳定版发布说明。

## 3. 社区热点 Issues

### #35420｜OneDrive 工作区导致 Codex 流式响应反复断连
👀 30 条评论 ｜ 🔗 [Issue 链接](https://github.com/openai/codex/issues/35420)

Windows 上 OneDrive 托管的 workspace 在 OneDrive 降级时，流式请求反复报 `stream disconnected before completion`，生成多个 request ID。**代表了一类"文件系统/云同步层异常导致 Codex 会话中断"的系统性问题**，在远程办公场景中影响极大。

### #31860｜GPT-5.6 Sol 上下文被限制在 372K，远低于 1.05M 模型规格
👀 14 条评论 ｜ 👍 26 ｜ 🔗 [Issue 链接](https://github.com/openai/codex/issues/31860)

用户实测 Codex App 中 Sol 模型的上下文被 catalog 截断至 372K（实际可用 353.4K），与官方规格不符。**高赞说明用户对模型能力透明性高度敏感**，尤其是 Pro 订阅用户。

### #28919｜Windows 版缺少 "Control other devices" 选项卡
👀 26 条评论 ｜ 👍 30 ｜ 🔗 [Issue 链接](https://github.com/openai/codex/issues/28919)

Windows 桌面版 Settings > Connections 中缺失远程设备管理入口，而其他平台可用。**当前社区最高赞 Issue，功能缺失类问题通常影响范围广、修复优先级高**。

### #19504｜阿拉伯语/希伯来语用户需要完整 RTL 文本支持
👀 24 条评论 ｜ 👍 19 ｜ 🔗 [Issue 链接](https://github.com/openai/codex/issues/19504)

Codex 与 Chat 面板中的阿拉伯语渲染存在对齐、标点错乱。属于明确的**本地化缺口**，已被官方列入 "Papercuts 2026" 看板。

### #21211｜线程导航/加载因元数据无界膨胀而变慢
👀 23 条评论 ｜ 🔗 [Issue 链接](https://github.com/openai/codex/issues/21211)

`threads.title` 被撑满为完整首条消息，SQLite 线程导航路径元数据无界增长，导致历史会话加载性能持续恶化。**社区反馈定位到了具体根因，属于典型的技术债清理目标**。

### #35119｜最新版将 WSL 有效仓库误判为 "非 Git 仓库"
👀 14 条评论 ｜ 👍 13 ｜ 🔗 [Issue 链接](https://github.com/openai/codex/issues/35119)

`26.721.3404` 在 Windows + WSL2 下将 ext4 上的仓库标记为 non-Git，并提示 "Git is unavailable"。**影响所有 WSL 开发者的基础操作，是 Windows 侧的严重回归**。

### #17574｜Subagent 泄漏 stdio MCP helper 进程树
👀 15 条评论 ｜ 🔗 [Issue 链接](https://github.com/openai/codex/issues/17574)

`xcodebuildmcp` 与 `chrome-devtools-mcp` 等 stdio helper 在 App 中反复累积，进程树未随 subagent 结束而清理。**涉及资源回收，长期运行易导致系统卡顿**。

### #29639｜WSL 工作区下 Browser Use / Node REPL 无法工作
👀 14 条评论 ｜ 👍 3 ｜ 🔗 [Issue 链接](https://github.com/openai/codex/issues/29639)

桌面版自动生成 Windows 版 `node_repl.exe`，但工具调用传入的是 Linux/WSL 路径，`sandboxCwd` 不匹配导致失败。**是 Windows + WSL 混合环境的典型边界问题**。

### #29908｜apply_patch 与沙箱在 Ubuntu 24.04 上因 Bubblewrap 报错失败
👀 13 条评论 ｜ 🔗 [Issue 链接](https://github.com/openai/codex/issues/29908)

Bubblewrap 0.9.0 在 Ubuntu 24.04 + Kernel 6.17 下出现 loopback/userns 错误，`apply_patch` 完全不可用。直接影响 Linux 上最常用的文件编辑工具。

### #15477｜Codex Cloud 自动代码审查静默失败，配额显示不一致
👀 11 条评论 ｜ 👍 6 ｜ 🔗 [Issue 链接](https://github.com/openai/codex/issues/15477)

GitHub 自动 code review 三合一 bug：静默失败、dashboard 显示有配额但实际提示限额、存在陈旧 GitHub 连接状态。**静默失败比显式报错更危险，用户无法感知任务是否已终止**。

## 4. 重要 PR 进展

> 注：昨日 PR 均由 `copyberry[bot]` 提交，已全部关闭（大概率已合并）。内部自动化程度极高，每日合入量可观。

### #36796｜新增 Agent Plugins MCP 配置解析
🔗 [PR 链接](https://github.com/openai/codex/pull/36796)

将 Agent Plugins v1 的 `mcp.json` 翻译为 Codex MCP 配置，支持 `PLUGIN_ROOT`/`PLUGIN_DATA` 变量展开。**打通插件生态与 Codex MCP 的关键桥接层**。

### #36793｜终止超时 Git 进程树
🔗 [PR 链接](https://github.com/openai/codex/pull/36793)

Git 元数据命令超时后，不再残留 helper 子进程：Unix 下引入独立 process group，Windows 下使用 Job Object 清理。**直接针对 Windows 上 git.exe 反复创建导致内核 Token 增长的问题**（对应 Issue #30926）。

### #36781｜MCP 工具支持按 surface 控制暴露范围
🔗 [PR 链接](https://github.com/openai/codex/pull/36781)

新增 `omit_tools_from` 配置，允许 server 指定工具是否出现在直接调用（direct）、工具搜索（search）、Code Mode 三个 surface 中。**解决"一次禁用全局失效"的粗粒度问题**。

### #36772｜提升 host-owned Codex Apps 目录上限
🔗 [PR 链接](https://github.com/openai/codex/pull/36772)

将 `codex_apps` 注册的工具目录上限从 2,048 提升至 8,192，同时保留标准 MCP 的 2,048 限制。**适配工具目录快速增长，避免大目录被截断**。

### #36771｜加固 Linux 受管代理 helper 生命周期
🔗 [PR 链接](https://github.com/openai/codex/pull/36771)

修复托管代理 helper 在沙箱命令退出后仍持有标准流、继承已关闭 fd 导致 proxy 就绪失败、僵尸进程残留 socket 目录等问题。**属于 Linux 自托管环境的稳定性深水区修复**。

### #36745｜整合 apply_patch 运行时执行

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报（2026-08-04）

## 今日速览

昨日更新集中在 **Agent 子代理稳定性** 与 **安全加固** 两大方向：多个 P1/P2 级问题直指 Subagent 误报成功、挂起及 shell 命令卡死等可靠性缺陷；同时社区提交了大量防御性修复 PR，覆盖 MCP OAuth 刷新、扩展下载原子性及上下文损坏防护。夜间版 v0.55.0-nightly 照常发布。

## 版本发布

- **v0.55.0-nightly.20260803.gf47d6c6f7**（2026-08-03 发布）  
  常规 nightly 迭代，无独立变更说明。完整改动对比见：  
  [v0.55.0-nightly.20260802...v0.55.0-nightly.20260803](https://github.com/google-gemini/gemini-cli/compare/v0.55.0-nightly.20260802.gf47d6c6f7...v0.55.0-nightly.20260803.gf47d6c6f7)

## 社区热点 Issues

**1. Subagent 将 MAX_TURNS 中断误报为 GOAL 成功** | [issue #22323](https://github.com/google-gemini/gemini-cli/issues/22323)  
P1 · 12 评论 · 2 👍  
`codebase_investigator` 子代理在达到最大轮次、实际未做任何分析时，仍向上报告 `status: "success"` / `Termination Reason: "GOAL"`。社区认为这会系统性掩盖 agent 中断，导致错误归因，是 evaluate 类任务的可信度危机。

**2. Generalist agent 无限挂起** | [issue #21409](https://github.com/google-gemini/gemini-cli/issues/21409)  
P1 · 8 评论 · 8 👍  
用户反馈任何触发 generalist 子代理的任务（如创建文件夹）都会永久挂起，最长等待 1 小时无响应。手动禁止子代理后问题消失，社区要求明确该代理的激活条件与超时机制。

**3. Shell 命令执行完成后卡死于 “Waiting input”** | [issue #25166](https://github.com/google-gemini/gemini-cli/issues/25166)  
P1 · 4 评论 · 3 👍  
极简命令（不会等待输入的命令）执行完成后，UI 仍显示命令活动并等待用户输入。此问题高频触发于常规 CLI 工作流，严重影响自动化脚本。

**4. Auto Memory 对低信号会话无限重试** | [issue #26522](https://github.com/google-gemini/gemini-cli/issues/26522)  
P2 · 5 评论  
后台提取代理判断某个会话为低信号而跳过时，该会话未被标记为已处理，导致同一候选会话被反复提取，浪费 token 且延迟真正的高价值记忆入库。

**5. Auto Memory 缺少确定性脱敏，且日志过度** | [issue #26525](https://github.com/google-gemini/gemini-cli/issues/26525)  
P2 · 安全 · 4 评论  
本地 transcript 的明文内容在交给提取模型前，仅依赖 prompt 指令脱敏——敏感数据在进入上下文后才执行编辑，且现有 skill 内容可能被写入日志。社区呼吁构建“发送前确定性 redaction”机制。

**6. Browser subagent 在 Wayland 下失败** | [issue #21983](https://github.com/google-gemini/gemini-cli/issues/21983)  
P1 · 4 评论 · 1 👍  
浏览器子代理在 Wayland 会话中直接终止（`Termination Reason: GOAL` 但实际未完成任务）。Wayland 已成为主流 Linux 显示服务，此兼容性缺口影响面较广。

**7. AST-aware 文件读取/搜索/代码库映射价值评估** | [issue #22745](https://github.com/google-gemini/gemini-cli/issues/22745)  
P2 · EPIC · 7 评论 · 1 👍  
EPIC 跟踪一系列调查：用 AST 感知工具精确读取方法边界、减少误导性读取造成的轮次浪费、压缩 token 噪声，并探索基于 AST 的代码库导航。反映社区对“深度代码理解”的持续诉求。

**8. Gemini 几乎不主动使用 skills 与 sub-agents** | [issue #21968](https://github.com/google-gemini/gemini-cli/issues/21968)  
P2 · 6 评论  
用户提供 gradle/git 等自定义 skill 后，模型仅在显式指令下才会调用，即使任务高度相关也不主动触发。社区要求提升工具选择的“意图匹配率”。

**9. 利用模型 bash 原生能力：零依赖 OS 沙箱 + 执行后意图路由** | [issue #19873](https://github.com/google-gemini/gemini-cli/issues/19873)  
P2 · 8 评论 · 1 👍  
提案称 Gemini 3 原生就是“bash 用户”，擅长串联 POSIX 工具。建议引入零依赖 OS 沙箱，既保留模型偏好的原生工具链，又保证安全与 UX，并执行“post-execution intent routing”以理解命令的真实意图。

**10. Agent 应主动阻止/劝阻破坏性操作** | [issue #22672](https://github.com/google-gemini/gemini-cli/issues/22672)  
P2 · 3 评论 · 1 👍  
在某些复杂 git 操作、分支管理、数据库维护中，模型会使用 `git reset`、`--force` 等危险命令，而实际上存在更安全的替代路径。社区要求 agent 对破坏性命令实施“安全替代优先 + 显式确认”策略。

## 重要 PR 进展

**1. 修复上下文损坏与配额错误回退** | [PR #28671](https://github.com/google-gemini/gemini-cli/pull/28671)  
core/cli · 新增  
针对工具执行被中断（配额回退、用户 ESC 查询）时出现的上下文损坏与“自动补全式”前缀延续问题，增加最后一公里防御性历史加固。

**2. GCA agent 模式容量错误回退** | [PR #28670](https://github.com/google-gemini/gemini-cli/pull/28670)  
core · 新增  
修复 Gemini Code Assist (GCA) 后端 `MODEL_CAPACITY_EXHAUSTED` / HTTP 429 时在同一失败模型上无限重试的问题，改为正确回退至其他可用模型（如 Flash）。

**3. 使用存储的 client ID 刷新 MCP OAuth token** | [PR #28481](https://github.com/google-gemini/gemini-cli/pull/28481)  
security/core · P1  
修复通过 OAuth discovery + 动态客户端注册接入的 MCP 服务器无法刷新 token 的问题。此前刷新在本地即失败并删除凭证，强制用户频繁重新认证。

**4. VS Code 扩展 Disposable 泄漏修复** | [PR #28665](https://github.com/google-gemini/gemini-cli/pull/28665)  
vscode-ide-companion · P2  
`activate()` 中两个 `context.subscriptions.push(...)` 参数对被意外转换为逗号表达式，导致每个表达式仅保留最后一个值，泄漏两个 Disposable。现恢复为独立 push。

**5. GlobTool 工作区目录验证不一致** | [PR #28666](https://github.com/google-gemini/gemini-cli/pull/28666)  
core · P2  
`validateToolParamValues()` 只校验 `config.getTargetDir()`，而 `execute()` 实际搜索完整工作区目录集，造成校验与执行范围不一致。此修复让二者对齐，避免越权文件访问。

**6. MCP 同意书展示完整配置 + stdio env 加固** | [PR #28664](https://github.com/google-gemini/gemini-cli/pull/28664)  
mcp · 新增  
扩展更新的同意书此前仅展示命令/参数/URL，遗漏 `env`、`cwd`、`headers` 等执行影响字段；更新时也不会对比这些字段决定是否重新征询。此 PR 补齐展示并硬化 stdio 环境变量传递。

**7. fetchJson 抗畸形 JSON 与流失败** | [PR #28663](https://github.com/google-gemini/gemini-cli/pull/28663)  
extensions · 新增  
`packages/cli/src/config/extensions/github_fetch.ts` 中 `JSON.parse` 在异步 `end` 回调内执行，且无错误处理，畸形响应或流中断会泄漏未捕获异常并崩溃扩展。现改为拒绝 Promise 并统一处理。

**8. 保留 thoughtSignature 以修复并行工具调用 400 错误** | [PR #28586](https://github.com/google-gemini/gemini-cli/pull/28586)  
agent/core · P2  
v0.53.0 回归：并行工具调用时 `thoughtSignature` 被意外剥离，导致 API 返回 400。该 PR 在 functionCall 部件中保留签名字段。

**9. formatTruncatedToolOutput 负数/零长度守卫** | [PR #28639](https://github.com/google-gemini/gemini-cli/pull/28639)  
core · P1  
`maxChars <= 0` 时，`String.prototype.slice` 的负索引行为会把输出膨胀约 2 倍。修复为直接原样返回内容，并补充 `maxChars = 0` 与负值回归测试。

**10. 会话保留机制防碰撞保护** | [PR #28653](https://github.com/google-gemini/gemini-cli/pull/28653)  
cli · 新增  
此前清理逻辑会把一个过期会话扩展到所有共享相同 8 字符短文件名后缀的会话文件上，可能删除无关会话。该 PR 改为“碰撞安全”的保留清理路径。

## 功能需求趋势

从

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-08-04）

## 1. 今日速览

今日发布补丁版本 v1.0.78-3，新增实验性 `/new-worktree` 命令并改进登录与交互式快捷方式。社区讨论焦点集中在 **BYOK 多模型切换**（#3709、#3282）与 **插件作用域/开关管理**（#1665、#2714）上，同时出现了多起关于 MCP 策略获取失败（#4346、#4349）和 `gpt-5.6-luna` 模型不可用（#4337）的新报告。

## 2. 版本发布

**v1.0.78-3** — [Release 链接](https://github.com/github/copilot-cli/releases/tag/v1.0.78-3)

- **新增**：实验性 `/new-worktree` 命令，可创建新 worktree 并在其中开启新对话。
- **改进**：交互式 shell 快捷键现在通过 Enter 启动，并在 "$" 武装状态下显示内联提示。
- **修复**：本地桌面环境下，`copilot login` 默认改为浏览器授权流程。

## 3. 社区热点 Issues（10 个）

### #3709 允许 `/model` 在同一会话内切换多个模型（含 BYOK / 本地 provider）
**状态**：OPEN | **标签**：`models` | 👍 20 · 💬 3  
BYOK 模式下会话被 `COPILOT_MODEL` 锁定，`/model` 选择器仅列出 GitHub 托管模型，无法切换到本地 provider 提供的模型，用户被迫重启会话。是“多模型工作流”诉求的典型代表。  
🔗 https://github.com/github/copilot-cli/issues/3709

### #3282 在 copilot CLI 中添加多 BYOK 模型能力
**状态**：OPEN | **标签**：`models`、`configuration` | 👍 20 · 💬 7  
当前 BYOK 仅支持通过单个环境变量配置一个模型，无法在 TUI 内实时切换，需终止会话重设变量。社区希望支持多模型 BYOK 配置与动态选择。  
🔗 https://github.com/github/copilot-cli/issues/3282

### #1665 支持将 Copilot CLI 插件作用域限定到项目或仓库
**状态**：CLOSED | **标签**：`plugins`、`configuration` | 👍 18 · 💬 14（已关闭）  
现有插件全局安装、全局加载，难以按仓库/项目启用针对性插件。该 issue 已被关闭，但获得大量关注，暗示官方可能已有内部方案或另开跟踪。  
🔗 https://github.com/github/copilot-cli/issues/1665

### #2714 功能请求：支持快速启用/禁用插件
**状态**：OPEN | **标签**：`plugins` | 👍 11 · 💬 2  
`copilot plugin` 仅支持安装、列表、卸载、更新，缺少 toggle 能力。用户对比 Gemini CLI、Claude Code 均已支持该功能，期望补齐。  
🔗 https://github.com/github/copilot-cli/issues/2714

### #4337 `gpt-5.6-luna` 在 /models 中可见但 `/chat/completions` 不可用
**状态**：CLOSED | 👍 0 · 💬 2  
模型在 Copilot Models API 中展示，但只能通过 `/responses` 访问，标准 OpenAI 兼容的 `/chat/completions` 接口返回失败，破坏了依赖 chat completions 的 MoA / 聚合类工具。对 API 兼容性有较高参考价值。  
🔗 https://github.com/github/copilot-cli/issues/4337

### #4349 托管设置策略校验失败，阻塞所有本地/自定义 MCP 服务器
**状态**：OPEN | **标签**：`triage`  
企业 GHE 返回 `permissions.disableBypassPermissionsMode` 的合法枚举值 `"enable"`，但 CLI 校验器只接受 `"disable"`，导致策略获取失败、全部 MCP 服务器被阻断。企业环境中影响面大。  
🔗 https://github.com/github/copilot-cli/issues/4349

### #4346 MCP 注册表策略获取返回 403，CI 中非默认 MCP 服务器全部被阻断
**状态**：OPEN | **标签**：`triage`  
在 GitHub Actions 中使用内置 `GITHUB_TOKEN` 认证时（`copilot-requests: write`），MCP 注册表策略接口返回 403，导致非默认 MCP 服务器全部不可用。直接影响 CI 自动化场景。  
🔗 https://github.com/github/copilot-cli/issues/4346

### #4078 计划提示词（`/every`、`/after`）触发后杀掉现有提示队列
**状态**：CLOSED | **标签**：`sessions` | 💬 5  
调度提示词触发后，队列中剩余 N 个提示不再继续弹出，自动化流程被意外中断。虽已关闭，但暴露了会话队列设计上的一个边界问题。  
🔗 https://github.com/github/copilot-cli/issues/4078

### #4328 WSL2 下 `Ctrl+H`（删除前一字符）被误判为 `Ctrl+Backspace`（删除整词）
**状态**：OPEN | **标签**：`input-keyboard`、`platform-windows` | 💬 2  
Windows Terminal 的 `WT_SESSION` 环境变量泄漏进 WSL2，使 `Ctrl+H` 行为异常。属于常见跨平台终端兼容性问题，影响 WSL2 用户日常输入效率。  
🔗 https://github.com/github/copilot-cli/issues/4328

### #4351 会话成本总览在首次上下文压缩后静默丢失固定金额
**状态**：OPEN | **标签**：`triage`  
Copilot CLI v1.0.77（macOS）首次上下文压缩成功时，会话累计成本会静默少计一块固定开销。对依赖成本追踪的用户有一定影响。  
🔗 https://github.com/github/copilot-cli/issues/4351

## 4. 重要 PR 进展

过去 24 小时内无新的 Pull Request，暂无 PR 动态可汇报。

## 5. 功能需求趋势

从近 30 条 Issues 中可提炼出以下五个需求方向：

- **模型灵活性与 BYOK 扩展**：多 BYOK 模型支持（#3282）、`/model` 可切换本地模型（#3709）、恢复会话时的模型/推理参数记忆（#4340）——社区明显希望摆脱“单模型锁定”限制。
- **插件系统成熟化**：项目级/仓库级插件作用域（#1665）、插件开关（#2714）、Windows 下符号链接支持（#2286）——插件正在成为核心工作流的一部分。
- **终端渲染与交互优化**：自定义颜色主题（#2830）、表格渲染质量（#2412）、对话历史滚动（#4313）、OSC 9;4 进度条开关（#4352）、流式长链接导致的表格抖动（#4347）——终端 UI 体验仍是高频痛点。
- **企业 / 托管环境适配**：托管设置策略的枚举兼容（#4349）、Actions 中 `GITHUB_TOKEN` 的 MCP 策略访问（#4346）——企业级部署存在现实障碍。
- **会话与输入状态管理**：计划提示词与队列交互（#4078）、存储提示（`Ctrl+S`）在切换会话后丢失（#4334）、取消的输入仍被送入 Agent（#4336）——用户对输入和会话状态的一致性有较高要求。

## 6. 开发者关注点

- **MCP 与 CI 集成存在认证/策略阻断**：GITHUB_TOKEN 下 403、托管设置策略枚举误判，直接破坏 CI 自动化和企业部署。
- **模型切换成本高**：BYOK 单模型绑定、`/model` 不包含本地模型，被迫反复重启会话，影响开发流连续性。
- **输入处理存在反直觉行为**：取消后的输入仍会被 Agent 正常处理（#4336），存储的提示在会话切换后无法恢复（#4334），暴露出输入状态机问题。
- **跨平台终端兼容性**：WSL2 按键误判（#4328）、原生 Windows zellij 的 DA1 序列混入输入框（#4267）等，在 Windows/WSL2 用户群中出现频率较高。
- **终端渲染细节影响体验**：表格错位、流式重排、进度条序列不可关闭等，虽然不影响核心功能，但显著降低长时间使用时的舒适度。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>



</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-08-04）

## 1. 今日速览

**v0.21.4 正式发布**，Web Shell 升级为发布就绪的桌面应用，补齐了生命周期管理、单实例与自动更新能力。社区侧出现一批高优先级 bug 报告，涵盖 MCP 工具在恢复会话中失效（#8433）、桌面版会话静默自动删除（#8400）以及提示缓存被微压缩反复失效（#8452）等关键问题。此外，**v0.21.5 发布流程在 CI 质量检查阶段失败**（#8476），发布进度受阻。

## 2. 版本发布

### v0.21.4（Release）
- **Web Shell 桌面化**：成为发布就绪的桌面应用，支持原生生命周期管理、单实例行为与自动更新。[#8132](https://github.com/QwenLM/qwen-code/pull/8132)
- **历史分页优化**：Web Shell 历史分页可优雅处理超大轮次的数据展示。

### v0.21.3-nightly.20260803.e1e5b42ce
- **文档补全**：完善 TUI 键盘快捷键参考文档。[#8327](https://github.com/QwenLM/qwen-code/pull/8327)
- **Bug 修复**：解除 history pagination 在特定场景下的阻塞问题。

## 3. 社区热点 Issues（Top 10）

### 🔴 高优先级
- **[P1] 桌面版会话在应用重启后静默自动删除**（#8400）  
  Windows 桌面版 v0.0.5 在 ACP session/load 失败（workspace cwd 不匹配）时，自动删除本地会话镜像，用户数据无提示丢失。  
  👥 3 评论 | 更新于 08-03  
  [查看详情](https://github.com/QwenLM/qwen-code/issues/8400)

- **[P2] SDK-Embedded MCP Server 工具在恢复会话后失效**（#8433）  
  使用 `createSdkMcpServer` 嵌入的 MCP 工具在首个查询正常，但恢复会话后直接调用总失败，影响 SDK 集成稳定性。  
  👥 3 评论 | 更新于 08-03  
  [查看详情](https://github.com/QwenLM/qwen-code/issues/8433)

- **[P2] Size-triggered 微压缩反复失效提示缓存**（#8452）  
  默认 500,000 字符阈值触发微压缩，在连续 ToolResult 轮次中反复重写已缓存的对话前缀，导致缓存命中率下降。  
  👥 3 评论 | 更新于 08-03  
  [查看详情](https://github.com/QwenLM/qwen-code/issues/8452)

- **[P2] `isAbortError` 未识别 OpenAI SDK 的 `APIUserAbortError`**（#8398）  
  在 `auth_type=openai` 路径下用户取消请求被误分类，影响取消后的错误处理与状态恢复。  
  👥 3 评论 | 更新于 08-03  
  [查看详情](https://github.com/QwenLM/qwen-code/issues/8398)

- **[P2] Duplicate provider tool call id**（#8382）  
  工具调用报错“Duplicate provider tool call id”且未被记录，导致后续环境异常。  
  👥 6 评论 | 更新于 08-03  
  [查看详情](https://github.com/QwenLM/qwen-code/issues/8382)

### 🟡 功能与体验
- **[P3] 确定性工具执行边界提案**（#8102）  
  核心方向：将 LLM 置于信任边界之外，使运行时能确定性约束、授权、观察和评估模型产生的动作，构建可信 Agent 运行时。  
  👥 13 评论 | 更新于 08-03 | 社区讨论热度最高  
  [查看详情](https://github.com/QwenLM/qwen-code/issues/8102)

- **[P2] Bailian Token Plan 模型列表不同步**（#8432）  
  `/auth` 内置模型列表与 Bailian 控制台实际模型列表不同步，且图片/视频生成失败。  
  👥 4 评论 | 更新于 08-03  
  [查看详情](https://github.com/QwenLM/qwen-code/issues/8432)

- **[P2] 取消 Prompt 后内容未恢复**（#8316）  
  Ctrl+C 取消 agent 思考后，已输入内容丢失，无法从输入框找回修改。  
  👥 7 评论 | 更新于 08-03  
  [查看详情](https://github.com/QwenLM/qwen-code/issues/8316)

- **[P3] Fork agents 继承兄弟 fork 指令，引发上下文污染**（#8326）  
  并行 fork 子代理继承了包含所有兄弟 functionCall 的父级最后消息，泄露上下文信息。  
  👥 4 评论 | 更新于 08-03 | 👍 1  
  [查看详情](https://github.com/QwenLM/qwen-code/issues/8326)

- **[P2] 模型名过长导致选择困难**（#8470）  
  使用 Alibaba token plan 时，"[Modelstuidio token plan]"前缀过长，在 Paseo 移动端模型列表中被截断。  
  👥 5 评论 | 更新于 08-03  
  [查看详情](https://github.com/QwenLM/qwen-code/issues/8470)

> 另请注意：[#8476](https://github.com/QwenLM/qwen-code/issues/8476) **v0.21.5 发布流程在 quality 检查阶段失败**（3 评论），已标记 `ready-for-agent` 待处理。

## 4. 重要 PR 进展（Top 10）

- **[feat] 成本账本：从磁盘记录构建 review 成本明细**（#8471）  
  针对“0.21.3 正常，0.21.4 变慢”的回归问题，通过回放 review 记录实现成本归因，无需手工聚合遥测数据。  
  [查看详情](https://github.com/QwenLM/qwen-code/pull/8471)

- **[fix] 启动时清理过期 worktree 项目快照**（#7925）  
  修复 #7906：worktree 会话注册的项目快照此前从未被清理，崩溃/强杀路径下残留。  
  [查看详情](https://github.com/QwenLM/qwen-code/pull/7925)

- **[fix] 保持 Web Shell 中 pending 后台 Agent 活跃**（#8413）  
  后台 subagent 未完成时，保持 turn 展开状态，避免过早折叠导致信息丢失。  
  [查看详情](https://github.com/QwenLM/qwen-code/pull/8413)

- **[feat] GitHub Channels 支持本地 gh 认证**（#8461）  
  复用宿主机的 `gh auth login` 凭据作为显式 PAT 之外的备选认证方式，Web Shell 提供 `useLocalGh` 开关。  
  [查看详情](https://github.com/QwenLM/qwen-code/pull/8461)

- **[feat] 将 Plan 审批绑定到具体 Todo 修订版**（#8393）  
  `exit_plan_mode` 审批请求携带 Todo plan ID 与 source tool-call ID，WebShell 需双重匹配才可解析审批 DAG，防止审批漂移。  
  [查看详情](https://github.com/QwenLM/qwen-code/pull/8393)

- **[feat] Autofix 要求隔离的定向 E2E 证明**（#8318）  
  为 Autofix 问题增加 fail-closed 验证链：传输不可变失败元数据、绑定维护者审批到精确标题与正文，验证候选提交身份。  
  [查看详情](https://github.com/QwenLM/qwen-code/pull/8318)

- **[fix] 模型切换保持会话级作用域**（#6579）  
  普通 `/model` 命令仅更新活跃会话；持久化为默认模型需显式使用 `/model --default`，避免模型切换泄漏到其他会话。  
  [查看详情](https://github.com/QwenLM/qwen-code/pull/6579)

- **[feat] 外部工具守卫 Provider**（#8125）  
  为托管 `qwen serve` ACP 部署提供可选的进程启动前策略 Provider，默认关闭；设为 `required` 时需完成带版本握手。  
  [查看详情](https://github.com/QwenLM/qwen-code/pull/8125)

- **[fix] 加固 Qwen 3.8 reasoning effort wire shape**（#8488）  
  针对 #8472 的 review 反馈修复 DashScope 请求格式：当 effort 层级以 `reasoning_effort` 发送时，丢弃冲突的 `enable_thinking` 和 `thinking_budget` 参数。  
  [查看详情](https://github.com/QwenLM/qwen-code/pull/8488)

- **[feat] 附件音频桥接**（#8332）  
  主模型不支持音频时，通过批处理语音模型将 `@` 附件及 ACP 音频提示转写为文本，并标记为“非可信机器转写”。  
  [查看详情](https://github.com/QwenLM/qwen-code/pull/8332)

## 5. 功能需求趋势

从近 24 小时 Issue 与 PR 中提炼出以下社区关注方向：

| 方向 | 代表性 Issue/PR | 热度 |
|------|----------------|------|
| **可信 Agent 运行时** | #8102 确定性工具执行边界；#8125 外部工具守卫 | 高（深度讨论中） |
| **MCP 生态完善** | #8433 SDK-Embedded MCP 失效；#8492 MCP 热重载残留；#8382 重复 tool call ID | 高（多项 bug 集中爆发） |
| **Web Shell / 桌面体验** | #8413 后台 Agent 保持活跃；#8445 会话刷新认证；#8494 双 workspace artifact 误操作 | 中（活跃迭代中） |
| **渠道集成（Channel）** | #8281 Email (IMAP/SMTP)；#8461 本地 gh 认证 | 中（新方向） |
| **多媒体（Omni + 音频）** | #8183 视频端到端 S1 通路；#8332 音频桥接；#8350 可信私有 ASR 地址 |

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*