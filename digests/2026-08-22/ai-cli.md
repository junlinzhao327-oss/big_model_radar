# AI CLI 工具社区动态日报 2026-08-22

> 生成时间: 2026-08-21 22:35 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-08-22）

## 一、生态全景

当前 AI CLI 工具已从单轮对话式补全，快速转向**多代理并行执行 + 长周期会话管理 + 插件生态扩展**的“Agent 工作台”形态，竞争焦点从模型能力外包转移至**工程可靠性、成本透明度和平台兼容性**。各主流工具均在快速迭代，但普遍出现子代理生命周期失控、会话状态回归、MCP 集成摩擦等“成长的阵痛”。同时，同一批高频需求（多模型/BYOK、成本可视化、沙箱可配置性）几乎横跨所有工具社区，说明市场已进入**功能趋同、体验与治理决定胜负**的阶段。值得注意的是，多工具集中出现认证失效、静默降级、资源泄漏等稳定性问题，可靠性成为当前最大的行业痛点。

---

## 二、各工具活跃度对比（2026-08-22）

> 数据基于各仓库社区日报公开信息，范围以 24 小时动态为主。

| 工具 | Issues 活跃度 | PR 活跃度 | Release 情况 | 阶段特征 |
|------|-------------|----------|-------------|---------|
| **OpenAI Codex** | 9 个热点议题；单 issue 最高 35 评论 / 22 👍 | 密集合入（Guardian、Browser/Computer Use、Bedrock） | 5 个 Rust alpha（v0.149~v0.150） | 高频迭代，范围快速扩张，但回归较多 |
| **GitHub Copilot CLI** | 10 个热点议题；Top 合计获 50+ 👍 | 0 个新 PR | v1.0.81-7 正式发布 | 版本节奏稳健，进入功能深化期 |
| **Gemini CLI** | 聚焦子代理可靠性（多个 P1 级 Bug） | 10+ 个 PR（贡献者 joneba-google 主导） | v0.56.0-nightly | 早期成长阶段，核心机制待夯实 |
| **Kimi Code CLI** | 1 个新 Bug（#2615） | 1 个 PR（插件安全文档） | 无新版本 | 短期低活动，但问题指向深水区 |
| **OpenCode** | 10 个热点议题；单 issue 最高 31 评论 / 38 👍 | 6+ 个 core 修复 PR（kitlangton） | v1.18.21 / v1.18.20 连续补丁 | 社区驱动、响应迅速的补丁期 |

**注**：Claude Code、Qwen Code 当日无公开摘要数据，未纳入对比。

---

## 三、共同关注的功能方向

### 1. 子代理生命周期治理（最集中痛点）
- **Kimi**（#2615）：子代理在 `killed/timed_out` 后仍持续调用 LLM，配额失控且不可拦截。
- **Codex**（#35259）：等待/轮询期间模型被反复调用，token 开销占 19.8%。
- **Gemini**：P1 级 Bug 暴露代理误报成功、无响应挂起。
- **Copilot**（#4533）：并行子代理启动导致终端 UI 完全卡死。

**结论**：对子代理的强制终止语义、资源配额可见性、任务状态真实性，已从优化项上升为基础设施级要求。

### 2. 成本透明化
- **Open

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截止 2026-08-22）

## 一、热门 Skills 排行

1. **skill-creator 评估链路修复**（#1298，OPEN）— 热度最高的 PR。修复 `run_eval.py` 对所有描述一律报告 `recall=0%` 的致命缺陷（#556 有 10+ 独立复现），并顺带修复 Windows 流读取、触发检测与并行 worker 问题。社区讨论热点：skill-creator 工具链在 Windows 上近乎不可用，已阻碍描述优化闭环。
   https://github.com/anthropics/skills/pull/1298

2. **document-typography 排版质检 Skill**（#514，OPEN）— 新增 AI 生成文档的排版质量控制：孤儿行（1-6 词溢出到下一行）、寡妇标题（节标题滞留页底）、编号错位。讨论热点：这些问题是 Claude 生成文档的普遍痛点，用户很少主动要求排版，但影响体验极深。
   https://github.com/anthropics/skills/pull/514

3. **PDF Skill 大小写路径修复**（#538，OPEN）— 修复 `SKILL.md` 中 8 处与文件名不匹配的引用（`REFERENCE.md`→`reference.md`、`FORMS.md`→`forms.md`），在大小写敏感文件系统上会导致 skill 加载失败。
   https://github.com/anthropics/skills/pull/538

4. **ODT 文档 Skill**（#486，OPEN）— 新增 OpenDocument 格式（.odt/.ods）的创建、模板填充及 ODT→HTML 转换能力，触发词覆盖 ODT/ODS/ODF/Libre

---



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-08-22）

## 今日速览

过去 24 小时，Codex 社区的核心话题集中在 **Windows/Remote 稳定性** 与 **认证失效** 问题上，尤其是 26.818 系列更新后 Windows 主机与 Android/iOS 远程控制大面积异常。PR 侧则密集合入了 **Guardian 安全审查、Browser/Computer Use 配置** 及 **Amazon Bedrock 原生接入** 相关改动，同时发布了 5 个 Rust alpha 版本。

---

## 版本发布

过去 24 小时共发布 5 个 Rust 工具链 alpha 版本，均未附带详细变更说明：

- [rust-v0.150.0-alpha.5](https://github.com/openai/codex/releases)
- [rust-v0.150.0-alpha.3](https://github.com/openai/codex/releases)
- [rust-v0.150.0-alpha.2](https://github.com/openai/codex/releases)
- [rust-v0.149.0-alpha.7.1](https://github.com/openai/codex/releases)
- [rust-v0.149.0-alpha.4.1](https://github.com/openai/codex/releases)

---

## 社区热点 Issues

### 1. macOS 桌面端反复生成 Computer Use Worker 并崩溃（V8 OOM）  
[#38455](https://github.com/openai/codex/issues/38455) · 评论 35 · 👍 15  
Codex Desktop 26.810.41047 在空闲状态下于启动后 98 秒内触发 `node::OOMErrorHandler`，崩溃时 316 个线程中 187 个名为 `computer-use`，且应用空闲时也在生成 Worker。上一版本 26.730.61639 正常，属明显回归，影响面较广。

### 2. 打开历史会话导致 ChatGPT 认证失效、跳转登录页  
[#39162](https://github.com/openai/codex/issues/39162) · 评论 31 · 👍 22  
macOS 26.814.41407 版本中，打开既有会话会使认证状态失效并跳转至登录页。用户明确给出已知可用版本（26.810.52044），是典型的客户端认证状态回归，社区讨论热度高。

### 3. Windows 下所有内置插件不可用（Computer Use、Browser、Chrome、LaTeX）  
[#25220](https://github.com/openai/codex/issues/25220) · 评论 27 · 👍 4  
Microsoft Store 安装的 Codex 在 Windows 11 China 上插件全部不可用，根因指向 EFS 加密的 WindowsApps 文件导致 `copyfile` 失败。该问题已持续近三个月仍未解决，Windows 沙箱/插件平台的稳定性是当前最大痛点之一。

### 4. 桌面自动化静默回退到 workspace-write 沙箱  
[#15310](https://github.com/openai/codex/issues/15310) · 评论 21 · 👍 16  
计划任务/定时自动化在配置了 `danger-full-access` 时仍以 `workspace-write` 启动线程，且仅在用户手动进入聊天 UI 后才纠正。静默降级对自动化工作流有实际破坏性，社区关注度高。

### 5. Codex Desktop 在等待/轮询期间反复调用模型，消耗大量配额  
[#35259](https://github.com/openai/codex/issues/35259) · 评论 15 · 👍 8  
多代理/Ultra 模式下，仅执行 `wait/status polling` 的模型调用占原始本地 token 量的 19.8%。开发者对其配额消耗的透明度提出质疑。

### 6. Bedrock 原生 Codex 缺少显式缓存控制，缓存写入成本高  
[#37674](https://github.com/openai/codex/issues/37674) · 评论 12 · 👍 12 · 已关闭  
Codex CLI 请求 Bedrock Mantle 时无法为 GPT-5.6 Sol 开启显式提示缓存，Agentic 工作负载产生大量 cache-write token。与 #35300 相关，代表自定义 Provider 场景的深度需求。

### 7. ChatGPT Pro（20x）账户实际获得 Pro 5x 的 Codex 用量额度  
[#38157](https://github.com/openai/codex/issues/38157) · 评论 7 · 👍 5  
多账户订阅信息仍显示 Pro（20x），官方用量 API 也返回 `plan_type: "pro"`，但实际用量额度按 Pro 5x 档位计算。配额计费不一致对重度用户影响显著。

### 8. Codex App 阻止 API Key 用户使用本地/私有插件市场  
[#20621](https://github.com/openai/codex/issues/20621) · 评论 4 · 👍 28 · 已关闭  
Enterprise/API Key 认证用户无法管理与使用本地或私有插件市场。虽然已关闭，但 👍 28 显示社区对该功能限制仍有强烈诉求。

### 9. Android Remote 在 Windows 主机上不可用：显示已断开、长任务无法打开  
[#39947](

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-22

## 今日速览

今日社区讨论重心集中在**子代理（Subagent）可靠性与状态真实性**问题上，多个 P1 级 Bug 暴露了"代理误报成功"和"无响应挂起"等影响日常使用的缺陷。与此同时，**PR 生成与评测流水线**成为最活跃的开发方向，`joneba-google` 主导提交了 10+ 个相关 PR。官方发布 v0.56.0-nightly，包含 symlink 忽略路径修复与 shell 执行服务重构两项核心变更。

---

## 版本发布

### v0.56.0-nightly.20260821.g30573d2e4

- **fix(core)**：修复忽略路径处理中 symlink 求值不一致的问题（@luisfelipe-alt，[PR #28915](https://github.com/google

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

## GitHub Copilot CLI 社区动态日报 — 2026-08-22

### 今日速览

v1.0.81-7 发布，新增崩溃/重启后自动恢复会话的能力，并优化了模型信息展示。社区对多模型切换与 BYOK（自带密钥）支持的需求持续高涨（#3282、#3709 合计获得 50+ 👍 ️）。此外，MCP 可靠性、ACP 协议一致性和 Windows 平台体验是今日新问题的高发区。

---

### 版本发布

**v1.0.81-7**

- **会话恢复**：CLI 启动时会主动提供恢复此前仍处于打开状态的会话，崩溃或机器重启后无需手动逐个终端重新打开。
- **模型信息增强**：`models.list` 现在包含服务端发布的 `infoMessages` 和 `warningMessages` 字段，便于用户了解每个模型的当前状态与限制。
- **新命令**：新增 `copilot app`，用于打开 GitHub Copilot 应用入口（原描述被截断）。

---

### 社区热点 Issues（Top 10）

**1. [#3709 允许 /model 在单个会话中切换多个模型，包括 BYOK/本地提供商](https://github.com/github/copilot-cli/issues/3709)**
👍 27 | 💬 4 | 更新于 08-21
当前 BYOK 模式通过 `COPILOT_MODEL` 将会话固定为单一模型，`/model` 选择器仅列出 GitHub 托管模型，无法选择本地 BYOK 提供商提供的模型。用户希望在一个会话内自由切换模型。该问题与 #3282 并列，是社区呼声最高的功能方向。

**2. [#3282 在 Copilot CLI 中增加多个 BYOK 模型能力](https://github.com/github/copilot-cli/issues/3282)**
👍 26 | 💬 8 | 更新于 08-21
用户希望在 TUI 中直接切换多个 BYOK 模型，而不是每次换模型都要终止会话并重新设置环境变量。评论中讨论了扩展 `/model` 选择器以显示所有已配置模型（包括 BYOK）的可行方案。

**3. [#1313 会话分支（Session Branching）](https://github.com/github/copilot-cli/issues/1313)**
👍 13 | 💬 7 | 更新于 08-21
允许用户从当前会话的任意位置分支出一个新会话，新会话继承完整对话历史，同时保留原会话的完整性。这一功能将极大提升探索性任务和多方案对比的工作效率，属中长线功能需求。

**4. [#4345 模型 'claude-haiku-4.5' 不支持推理强度 'medium'](https://github.com/github/copilot-cli/issues/4345)**
👍 4 | 💬 8 | 更新于 08-21
在同时启用 `copilot_cli_opus_medium_effort_default` 和 `copilot_cli_gpt_5_4_mini_for_explore` 两个服务端功能开关时，子代理执行反复报错 `Reasoning effort 'medium' is not supported`。反映服务器端功能开关与模型能力矩阵之间的冲突。

**5. [#4211 Copilot CLI 无法处理结构化 MCP 响应中的 BigInt](https://github.com/github/copilot-cli/issues/4211)**
👍 3 | 💬 5 | 更新于 08-21
当 MCP 服务器返回大整数时，CLI 抛错 `TypeError: Do not know how to serialize a BigInt`，导致任务全部中止。该问题会阻断所有依赖大整数数据（如时间戳、ID、加密货币数值）的 MCP 集成。

**6. [#4535 `store_memory` 在 v1.0.81 预发布版中失败：`Instance id is required`](https://github.com/github/copilot-cli/issues/4535)**
👍 0 | 💬 4 | 更新于 08-21
由 GPT-5.6 Sol 代理自动提交。`store_memory` 在 1.0.81 预发布版中一致失败，原生内存写入器被调用时缺少必需的实例 ID。这会导致上下文记忆功能在最新预发布版中不可用，对依赖长期记忆的用户影响较大。

**7. [#4521 沙箱无法禁用](https://github.com/github/copilot-cli/issues/4521)**
👍 4 | 💬 3 | 更新于 08-21
配置文件中显示沙箱已禁用，但运行状态仍显示沙箱已启用，且命令执行依然走沙箱。这是一个配置与运行时状态不一致的严重问题，会阻止用户通过本地工具链完成需要完整系统权限的任务。

**8. [#4533 并行子代理启动时终端 UI 停止消费事件（输入+滚动全部失效）](https://github.com/github/copilot-cli/issues/4533)**
👍 0 | 💬 1 | 更新于 08-21
在预发布版（1.0.81-4/5）中，当一次 turn 启动并行子代理块时，终端 UI 完全停止响应滚动和输入，但 Rust 运行时仍在后台持续运行。属于严重的 UI 阻塞问题，影响复杂任务的可观测性和可操作性。

**9. [#4485 主题一夜之间自动变亮](https://github.com/github/copilot-cli/issues/4485)**
👍 2 | 💬 2 | 更新于 08-21
用户报告早上打开时主题为深色，但隔夜休眠唤醒后主题变为浅色。CLI 可能错误地跟随了 macOS 系统的颜色模式变化，而非保持用户显式选择。

**10. [#4511 会话 AIC 显示不可靠](https://github.com/github/copilot-cli/issues/4511)**
👍 0 | 💬 2 | 更新于 08-21
在 Kimi K3 的长时间会话中，AIC（AI 使用成本）统计严重低估实际消耗。这类计量不准确会影响企业用户对成本的控制和预算规划。

---

### 重要 PR 进展

过去 24 小时内无 PR 更新（共 0 条）。当前社区讨论集中在 issues 层面，暂无新的代码补丁进入审查阶段。建议关注上方热点 issue 的修复进度，尤其是 #4345（推理强度冲突）和 #4535（store_memory 失败）等回归性问题。

---

### 功能需求趋势

从今日 issue 中提炼的社区最关注功能方向：

- **多模型与 BYOK 深度集成**（#3282、#3709、#4560）：不再是单纯“能否接入多个模型”，而是“能否在会话中自由切换模型、是否支持本地推理提供商、以及 `auto` 模式能否正确传递推理强度配置”。这是当前第一大功能需求阵营。
- **会话管理增强**（#1313、#4535、#4554）：包括会话分支、会话恢复/持久化、`/resume` 范围切换等。用户正在将 CLI 会话视为可长期工作的“工作区”，而非一次性任务。
- **MCP 生态成熟度**（#4211、#4542、#4552、#4562）：MCP 服务器的发现（发现但未连接）、配置重载（沿用旧配置而不是重新读取）、结构化响应类型兼容（BigInt）以及不可用状态展示，都是第三方工具链接入时的关键阻力。
- **ACP 协议一致性**（#4555、#4561）：`session/prompt` 和 `session/cancel` 的行为与 ACP 规范存在偏差，导致客户端集成方无法正确区分“正常结束”与“用户取消”，会破坏上层 UI 的状态机。
- **计划评审交互**（#4563）：在生成计划上直接添加内联注释，而不是在聊天中用文字描述修改意见。这标志着用户希望将代码评审模式迁移到规划阶段。

---

### 开发者关注点

- **第三方 MCP 集成可靠性是最大痛点**：从 BigInt 序列化错误、MCP 服务器不可用卡死、到 `.mcp.json` 配置被缓存，MCP 相关问题的报告密度今日最高，直接影响 Copilot CLI 作为“Agent 中枢”的可信度。
- **沙箱与权限控制的“玄学”问题**（#4521）：配置禁用但实际仍启用，这类状态不一致问题会让开发者对 CLI 的执行环境失去信任，尤其是在需要系统级操作的场景。
- **Windows 平台体验欠佳**：#4549 中每个 shell 命令都会闪现一个新的 PowerShell 窗口并抢占焦点；#4540 中 `wta.exe` 因路径引用错误无法启动。Windows 用户的终端自动化体验仍与 macOS/Linux 存在明显差距。
- **成本可见性受关注**：AIC 显示不准确（#4511）会直接影响企业用户评估 Copilot CLI 的实际 ROI，尤其是在使用第三方模型供应商（如 Kimi）时。
- **预发布版回归频繁**：#4533（UI 卡死）、#4535（store_memory 失败）均出现在 1.0.81 预发布版中，建议生产环境用户暂时停留在 1.0.80 稳定版，等待上述回归修复后再升级。

---

> 报告生成时间：2026-08-22 | 数据来源：[github.com/github/copilot-cli](https://github.com/github/copilot-cli) | 本文由 AI 辅助编译，仅供参考。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-08-22

## 今日速览

过去 24 小时内，Kimi Code CLI 仓库没有发布新版本，公开动态以两条 "Open" 状态更新为主：一条是关于**后台子代理在任务终止后仍持续调用大模型**的 Bug Issue（#2615），另一条是**完善插件安全与持久化数据文档**的 PR（#2614）。虽然今日动态不多，但两个条目分别指向「资源生命周期可控性」与「插件安全边界」两个关键方向，值得开发者关注。

## 版本发布

过去 24 小时内没有新的 Release 发布，此部分省略。

## 社区热点 Issues

过去 24 小时内共有 1 个 Issue 更新，暂不足以列出 10 条。以下是当前最值得关注的 Issue：

### #2615 [Bug] 后台子代理在 TaskStop/超时标记为终止后仍持续调用 LLM - **重点关注**

- **作者**: @pc9527zxx
- **创建**: 2026-08-21
- **更新**: 2026-08-21
- **评论**: 0 ｜ **👍**: 0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2615

**摘要**: 一个后台子代理在任务及其元数据已被标记为 `timed_out` 或 `killed` 后，依然会继续发出 LLM 请求。该任务会从活动任务跟踪中消失，导致消耗的 token 配额不可见，且 `TaskStop` 无法再停止该子代理；用户只能通过终止整个进程来阻止它。

**为什么重要**：

- 涉及**资源泄漏与配额失控**：任务已终止但 LLM 调用仍在产生费用，且不可观测。
- 暴露任务状态机的**缺陷**：`timed_out` / `killed` 状态未真正终止底层子代理进程。
- `TaskStop` 对已标记终态的任务失效，用户失去控制手段。

**社区反应**: 暂无评论，但该问题的严重性较高，预计会引发关于任务调度与后台进程生命周期的讨论。

## 重要 PR 进展

过去 24 小时内共有 1 个 PR 更新，以下是当前进展：

### #2614 [OPEN] docs(plugins): document security and persistent data - **待合并**

- **作者**: @QIANLING-0831
- **创建**: 2026-08-20
- **更新**: 2026-08-21
- **链接**: https://github.com/MoonshotAI/kimi-cli/pull/2614

**摘要**: 该 PR 补充了插件相关的关键安全文档，内容包括：

- 明确说明插件工具以**本地子进程**方式运行，并拥有当前用户的文件与网络访问权限。
- 记录 `inject` 机制下的凭证处理方式，并警告用户避免将注入值打印到日志或提交到代码仓库。
- 说明重新安装插件会替换其安装目录，建议用户注意自定义配置和数据的持久化问题。

**意义**: 这是对插件系统安全边界的一次重要补充，有助于减少凭据泄露风险与误操作，符合当前 AI 编码工具安全实践的主流方向。

## 功能需求趋势

由于今日公开数据仅涵盖 1 个 Issue 与 1 个 PR，无法进行高置信度的趋势分析。基于现有信息的初步观察如下：

- **可观测性**：社区开始关注 AI 子代理调用行为的透明度，比如任务终止后的资源消耗不可见（#2615）。
- **安全与权限边界**：插件的本地权限、凭据处理与数据持久化正在成为文档与体验的一部分（#2614）。
- **生命周期管理**：如何让 `TaskStop`、超时机制真实地终止底层子代理进程，是预期会持续发酵的议题。

## 开发者关注点

基于今日两个条目的初步分析：

- **痛点：后台任务资源失控**。开发者反映子代理在超时或被杀后仍继续发出 LLM 请求，导致配额消耗不可追踪且无法干预（#2615）。
- **痛点：插件权限与凭据安全**。PR #2614 的背景说明开发者对插件子进程的文件/网络访问范围、注入凭证的日志泄漏风险存在担忧。
- 另有一个值得关注的高频需求方向：**任务终止的可靠性**。当前实现对子代理进程的终止不够彻底，用户希望获得强制的、可验证的终止语义。

---

*以上内容仅基于 2026-08-21 至 2026-08-22 期间 GitHub 公开数据生成，数据样本有限，部分结论为方向性判断。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报

**日期：2026-08-22 | 数据来源：github.com/anomalyco/opencode**

---

## 📌 今日速览

过去 24 小时内，OpenCode 发布 **v1.18.21** 与 **v1.18.20** 两个补丁版本，核心聚焦响应中断恢复与网络错误重试机制，桌面端也修复了文件搜索体验问题。社区侧，**流式模式禁用请求**（#785）持续发酵，以 38 👍 / 31 评论稳居热度榜首；模型/Provider 兼容性问题（DeepSeek 免费模型缺失、ChatGPT OAuth 失败、textVerbosity 误注入）成为新晋高频反馈。核心贡献者 @kitlangton 提交了 6 个 core 修复 PR，围绕 fork 继承、shell 生命周期与 provider 故障恢复，值得关注。

---

## 🚀 版本发布

### v1.18.21
**Core**
- 当模型报告未知 `finish reason` 时继续响应，而非提前停止
- Vertex AI `eu` / `us` 多区域 Gemini 请求路由至 REP 端点

**Desktop**
- 文件搜索加载期间保持搜索结果可见

### v1.18.20
**Core**
- 展示失败的 subagent 工具调用，并附带可恢复的 `task_id`
- 对 `finish_reason: network_error` 的 Provider 响应自动重试
- 重试更多网络错误变体（`network-error`、`network_error` 等）
- 以可恢复形式呈现 subagent 失败，而非直接返回空结果

---

## 🔥 社区热点 Issues

### 1. 如何禁用流式模式？ — 热度最高
[#785](https://github.com/anomalyco/opencode/issues/785) · 31 评论 · 38 👍 · 开放中
> 用户 @SimonWai 使用的代理 Provider（Credal OpenAI Proxy）不支持流式，请求是否需要非流式模式。评论区持续活跃近一年，说明大量用户受限于代理/网关的流式兼容性，官方尚未给出明确方案。

### 2. 会话在空 LLM 响应时静默终止（finish: unknown, 0 tokens）
[#41469](https://github.com/anomalyco/opencode/issues/41469) · 10 评论 · 开放中
> 当模型返回空 completion（0 tokens、无输出、finish reason 为 `unknown`）时，OpenCode 将其视为正常结束，会话循环静默退出。**v1.18.21 的修复正是针对此问题**，但该 issue 仍开放，建议关注是否彻底解决。

### 3. 归档会话的恢复/取消归档能力
[#24153](https://github.com/anomalyco/opencode/issues/24153) · 9 评论 · 11 👍 · 开放中
> 归档会话目前是单向操作，用户无法从侧边栏恢复。需求明确、投票数高，社区呼声集中于会话管理的基础体验完善。

### 4. 在模型选择器中显示模型成本
[#14524](https://github.com/anomalyco/opencode/issues/14524) · 5 评论 · 10 👍 · 开放中
> TUI 选择模型时无成本指示，用户难以预估 token 开销。与 #12377 成本追踪架构形成呼应，反映社区对成本透明化的强烈需求。

### 5. [RFC] 成本追踪架构：Subagent 聚合 + 多模型正确性
[#12377](https://github.com/anomalyco/opencode/issues/12377) · 10 评论 · 已关闭
> 系统性梳理了成本追踪的多个缺陷：parent session 未包含子 session 成本、多模型工作流下成本显示不准确等。虽是 RFC，但其架构讨论为后续成本功能奠定方向。

### 6. DeepSeek-v4-flash-free 模型缺失（双报）
[#43829](https://github.com/anomalyco/opencode/issues/43829) · 5 评论 · 开放中
[#43805](https://github.com/anomalyco/opencode/issues/43805) · 4 评论 · 开放中
> 同一问题被两位用户分别上报：模型存在于 `/zen/v1/models` API 中，但 TUI/Web 的模型下拉列表不显示，免费用户无法使用。涉及 Zen 网关与模型列表同步逻辑。

### 7. OpenCode 随机停止响应
[#34473](https://github.com/anomalyco/opencode/issues/34473) · 5 评论 · 3 👍 · 开放中
> v1.17.11 桌面版，使用 "big pickle" 模型时响应随机中断，无报错、直接播放完成音效。与 #41469 属同类稳定性问题，用户体感明显。

### 8. Desktop v1.16.0 Windows 大文件 diff 计算时 UI 冻结
[#30906](https://github.com/anomalyco/opencode/issues/30906) · 7 评论 · 已关闭
> Electron 渲染进程在处理大文件 diff 时完全无响应，v1.15.13 无此问题，确认是回归。已关闭，但 Windows 桌面端性能仍是敏感区域。

### 9. MCP 工具定义懒加载以减少 token 开销
[#35376](https://github.com/anomalyco/opencode/issues/35376) · 5 评论 · 开放中
> 多 MCP 服务器场景下，所有工具定义被注入每个会话的 system prompt，9 个 MCP server 时 token 消耗显著。社区对 MCP 工具按需加载的诉求明确。

### 10. 权限对话框不渲染：应用假死
[#41847](https://github.com/anomalyco/opencode/issues/41847) · 4 评论 · 开放中
> 后端生成了 3270 个权限提示但界面从未渲染，用户看不见对话框，应用被阻塞至 "假死"。属于严重 UX 缺陷，对自动化工作流影响较大。

---

## 🔧 重要 PR 进展

### 1. [contributor] fix(tui): 折叠 MCP 侧边栏错误
[#44003](https://github.com/anomalyco/opencode/pull/44003) · 开放中
> @kitlangton 改进 MCP 故障展示：服务器名称截断、状态右对齐，避免完整错误串（如 HTML）破坏侧边栏布局。

### 2. [contributor] fix(core): 目录重建后位置服务自动恢复
[#44005](https://github.com/anomalyco/opencode/pull/44005) · 开放中
> 会话引用的 worktree 目录被删除后重建时，立即恢复位置服务，无需重启会话。

### 3. feat(desktop): MCP 服务器配置与连接测试
[#43719](https://github.com

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*