# AI CLI 工具社区动态日报 2026-09-08

> 生成时间: 2026-09-08 00:30 UTC | 覆盖工具: 7 个

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



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-09-08）

## 今日速览

- 仓库发布 `rust-v0.154.0-alpha.6` 新

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-09-08

## 1. 今日速览

昨日发布 v0.60.0-nightly.20260907 版本；社区对**模型静默降级**（#28859，任意 `gemini-<X.Y>-flash` 被静默替换为 gemini-3.5-flash）反响强烈，成为当前最受关注的正确性问题。在 PR 侧，**Sandbox 安全加固**（#29214、#29216）与**扩展更新回滚修复**（#29166）是今日最值得关注的两条主线，前者旨在收敛容器内凭据泄露风险，后者直接修复了社区报告的 "回滚=空目录" 问题。

---

## 2. 版本发布

### v0.60.0-nightly.20260907.g85aca163f
- 常规 nightly 自动版本更新，无独立变更说明。
- 🔗 [查看完整 Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.60.0-nightly.20260906.g85aca163f...v0.60.0-nightly.20260907.g85aca163f)

---

## 3. 社区热点 Issues（10 个）

**1. ⚠️ 用户指定的 flash 模型被静默替换为 gemini-3.5-flash（P1，👍 14，8 评论）** — [#28859](https://github.com/google-gemini/gemini-cli/issues/28859)
请求任意 `--model gemini-<X.Y>-flash`（包括**不存在的版本号**）都会由 `gemini-3.5-flash` 成功响应，无报错、无警告，唯一线索是 JSON 输出中的 `stats.models`。这是严重的「静默错误」——用户以为在跑指定模型，实际上被悄悄降级。社区共 14 人点赞，是目前舆论压力最高的问题。

**2. 🔒 403 "The caller does not have permission"（已关闭，33 评论，👍 12）** — [#25306](https://github.com/google-gemini/gemini-cli/issues/25306)
安全/权限类告警，API 返回 403 权限不足错误。该问题积压了近 5 个月，累计 33 条评论，是社区参与度最高的话题之一，已被标记 need-triage / possible-duplicate 并关闭。

**3. Subagent 在 MAX_TURNS 后上报 "GOAL success"，掩盖真实中断（P1，13 评论）** — [#22323](https://github.com/google-gemini/gemini-cli/issues/22323)
`codebase_investigator` 子代理在自身结果已写明「达到最大轮次、未做任何分析」的情况下，仍上报 `status: "success"` / `Termination Reason: "GOAL"`。**假成功比真失败更有害**——会让上层误判任务已完成。该 P1 bug 已进入 need-retesting 阶段。

**4. Generalist 子代理永久挂起（P1，8 评论，👍 8）** — [#21409](https://github.com/google-gemini/gemini-cli/issues/21409)
一旦 Gemini CLI 委派任务给 generalist agent 就无限挂起，连「创建文件夹」这种简单操作也能卡住一小时。社区给出的 workaround 是**在提示词里明确禁止使用子代理**——侧面说明该问题对日常使用影响较大。

**5. 简单 Shell 命令执行完成后卡在 "Waiting input"（P1，4 评论，👍 3）** — [#25166](https://github.com/google-gemini/gemini-cli/issues/25166)
执行极简单的 CLI 命令后，命令已结束但终端仍显示该命令处于活动状态并「等待输入」。问题可稳定复现，属于终端/会话状态机类 bug，影响自动化流程的连续性。

**6. 扩展更新回滚把空目录当备份（P2，5 评论）** — [#29033](https://github.com/google-gemini/gemini-cli/issues/29033)
`update.ts` 声称「回滚」时把临时目录拷回扩展目录，但该临时目录**自始至终是空的**——回滚实际恢复了 0 个文件，唯一可观测效果是让情况更糟。社区已确认这是扩展更新失败的直接原因。今日已有对应修复 PR（见下文 #29166）。

**7. Auto Memory 在内容入库后才做脱敏，存在泄密风险（P2，5 评论）** — [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)
Auto Memory 会将本地 transcript 发给后台提取模型的上下文后才提示其脱敏，且服务会记录已存在的 skill 内容。社区要求实现**确定性脱敏**并减少 Auto Memory 的日志量，属于安全/隐私类改进需求。

**8. 利用模型原生 bash 能力：零依赖沙箱 + 执行后意图路由（P2，enhancement，9 评论）** — [#19873](https://github.com/google-gemini/gemini-cli/issues/19873)
Gemini 3 模型的训练范式高度贴合原生 bash 工具链（grep/cat/sed/awk）。该提案主张通过零依赖 OS 沙箱和安全的后置意图路由，让模型充分发挥 bash 天赋，同时不牺牲安全与 UX。方向与今日多个沙箱加固 PR 形成呼应。

**9. EPIC：评估 AST 感知的文件读取/搜索/代码库映射价值（P2，7 评论）** — [#22745](https://github.com/google-gemini/gemini-cli/issues/22745)
探索用 AST 感知工具精确定位方法边界、减少因错位读取导致的多次往返与 token 浪费，并改进代码库导航。对应子 issue #22746 建议从 tilth/glyph 等现

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-09-08

## 今日速览

今日无新版本 Release，但 Issue 和 PR 活跃度有明显上升。社区反馈焦点集中在 **Windows 桌面应用 1.1.15 的 Local session 创建限制**、**CLI 1.0.83 引入的 MCP 连接超时/CPU 占用回归**，以及**远程 MCP 服务器的 OAuth 认证流程缺陷**。较早提出的"项目级插件作用域"（#1665）在今日被关闭，但获得了 18 个 👍，仍是社区关注度最高的功能需求之一。

## 社区热点 Issues（10 个）

**1. 支持项目/仓库级插件作用域（#1665，已关闭）**
- 作者希望插件既能全局安装，也能按项目/仓库隔离加载，解决团队协作时插件配置互相干扰的问题。Issue 获得 18 👍，是近半年社区呼声最高的功能请求之一。
- https://github.com/github/copilot-cli/issues/1665

**2. `disable-model-invocation: true` 使 Skill 完全不可达（#4438，Open）**
- 用户发现标记为"仅手动调用"的 skill 在显式请求时返回 `Skill not found`，CLI 根本无法手动调用它，与 frontmatter 语义相矛盾。6 👍 + 4 评论，涉及 agents 与 skill 路由逻辑的设计缺陷。
- https://github.com/github/copilot-cli/issues/4438

**3. Windows 桌面 App 要求必须先归档 idle session 才能新建 Local session（#4756，Open）**
- 今日新增、9 👍 的高热度 Bug：Windows 版 Copilot App 1.1.15 在项目已有 idle session 时无法创建新 Local session，报 `invalid argument`。影响大量 Windows 用户的多会话并行工作流。
- https://github.com/github/copilot-cli/issues/4756

**4. 桌面 App 无法在运行中的 Local session 旁创建第二个会话（#4742，Open）**
- 与 #4756 同源，自动更新到 1.1.15 后触发：同一项目只要有一个活跃 CLI 进程，新建 Local session 即失败。社区评论中已有 7 条补充信息，属于高频复现问题。
- https://github.com/github/copilot-cli/issues/4742

**5. 非第一方 HTTP MCP 服务器的 OAuth 流程完全失效（#4017，Triaged）**
- 远程 MCP 服务器（Atlassian、incident.io 等）配置 `"type": "http"` 后，host-token 被取消但浏览器弹窗从不出现，无报错无输出。已持续 2 个月仍在 triage 阶段，社区已出现 3 条补充评论。
- https://github.com/github/copilot-cli/issues/4017

**6. 会话恢复时将 MCP 初始化连接的超时从 ~16s 降到 ~1s（#4753，Open）**
- CLI 1.0.83 恢复会话时，如果 stdio MCP 服务器还在初始化就会被立刻取消，导致该服务器在会话期间静默不可用。属于明显的版本回归 Bug。
- https://github.com/github/copilot-cli/issues/4753

**7. `--yolo` / `--allow-all` 因 fail-closed 策略被整场会话禁用（#4757，Open）**
- 用户的托管策略解析结果为"无策略"，但 CLI 仍应用 fail-closed 姿态，永久禁止 bypass-permissions 模式。安全策略判定逻辑出现误伤。
- https://github.com/github/copilot-cli/issues/4757

**8. 会话在 turn 结束时永久卡死（#4755，Open）**
- 队列消息落在 turn 结束边界时，会话进入"非 idle 非 running"的楔死状态，无法接受输入、进程不崩溃、queue 永不清空。Claude Code 迁移用户 NSTA1 提交的 bug 已获 1 条评论确认，尚无 workaround。
- https://github.com/github/copilot-cli/issues/4755

**9. Copilot TUI 持续占用 CPU（#4750，Open）**
- CLI 1.0.83 用户报告 TUI 空闲时占用 6-7% CPU（16 core 机器），执行一次 prompt 后甚至涨到 2-4 个核心的占用。直接影响开发者笔记本续航与风扇噪音，亟待修复。
- https://github.com/github/copilot-cli/issues/4750

**10. `/refine` 发送不兼容的 `reasoning_effort` 参数导致 400 错误（#4747，Open）**
- `/refine` 内部调用 `gpt-4o-mini` 时发送 `reasoning_effort: "medium"`，而该模型不支持此参数。开发者已通过 Session Diagnosis 定位到根因，是模型路由层缺少参数兼容性检查。
- https://github.com/github/copilot-cli/issues/4747

## 重要 PR 进展（2 个）

**#4748 Add joke cli（Open）**
- 作者提交了一个名为 "joke cli" 的 PR，暂无描述信息，可能为实验性或娱乐性功能，社区尚未开始讨论。
- https://github.com/github/copilot-cli/pull/4748

**#4746 Add experimental next-action extension prototype（Open）**
- 微软员工提交的实验性 SDK 扩展示例：基于模型推断"下一步操作"（next-best-action）。代码位于 `examples/next-best-action/`，通过 `joinSession()` 复用前台 session，不参与自动发现，也不修改已安装 CLI。对希望探索扩展 API 的开发者有参考价值。
- https://github.com/github/copilot-cli/pull/4746

## 功能需求趋势

从今日全部数据看，社区最关注的四个功能方向为：

1. **插件的项目/仓库级作用域（#1665）**：已关闭但获得 18 👍，说明按团队/项目隔离插件配置的需求仍然强烈，未来可能以其他形式回归。
2. **Session 的过滤、分组与可管理性（#4693）**：用户希望在 tab 与 `/resume` 列表中按仓库/solution 过滤 session，当前 `open-sessions-state.json` 仅存 `openedAt` 等基础字段，缺少 repo 维度。
3. **非交互/自动化场景的会话状态可观测性（#4743、#4760）**：ACP 场景中 `end_turn` 之后后台 shell 仍会触发自主工具调用与文本输出，缺少"会话进入 idle"的明确信号，对上层 agent 编排造成困扰。
4. **MCP 协议完整性**：多项 issue 指向 MCP OAuth 的 User-Agent 传递缺失（#4681）、缺少 cancellation 请求（#4759）、初始化超时策略不合理（#4753），说明社区正用真实的 MCP 服务器生态拷打 CLI 的协议实现。

## 开发者关注点

- **Windows 桌面 App 的 session 创建限制是本日最高频痛点。** #4756（9 👍）与 #4742 触及同一问题：App 1.1.15 强制用户在新建 Local session 前必须归档/关闭已有 session，破坏了并行多工作区的基本工作流。这可能是 1.1.15 的回归，预期官方会尽快响应。

- **1.0.83 版本出现成规模的稳定性回退。** 涉及 MCP 初始化超时从 16s 缩短为 1s（#4753）、TUI 空闲时 CPU 占用激增（#4750）、后台 subagent 事件延迟 14 分钟才送达（#4760）、Azure MCP `learn=true` 调用 180s 超时（#4749）。多个 issue 发生在 2026-09-07 同一天被提交，提示 1.0.83 发布后存在集中性的兼容性问题。若你正在使用 1.0.83，建议关注后续 Patch 版本。

- **MCP OAuth 与模型参数兼容性问题显示生态位差异在扩大。** 远程 MCP 服务器在绕过 Copilot Desktop 的 OAuth 流程时直接卡死（#4017），`/refine` 对 `gpt-4o-mini` 发送 `reasoning_effort` 这种参数级"幻觉"，说明 CLI 在实际工作中已深度接触多样化的第三方模型与 MCP Server，需要更健壮的错误处理和协议适配。

- **session 状态管理与数据丢失风险持续发酵。** Session 永久卡死（#4755）、删除被驱逐 session 无效且 `ON DELETE CASCADE` 不触发（#4754）、表单输入回车误提交且草稿不可恢复（#4738）——这些 issue 的共同点是用户"写了或做了一半的东西"可能瞬间丢失，建议尽快为 elicitation form 加入草稿保护机制。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-09-08

## 今日速览

过去 24 小时内，Kimi Code CLI 没有发布新版本。社区讨论主要集中在 Windows 平台输入法字符重复、Agent 陷入重复读取工具循环，以及两个长期功能诉求（Plan 模式、MCP 配置无缝迁移）的重新回温。PR 方面，有两个提交正在推进，分别涉及“手机远程配对/旁观控制”和 `get_share_dir` 路径缓存优化。

## 版本发布

过去 24 小时未有新版本或预发布版本发布。

## 社区热点 Issues

> 说明：过去 24 小时更新/创建的 Issue 共 4 条，以下完整列出。

### 1. [#2584] Bug：Windows 上（及部分 IME）输入泰文等字符时出现重复
- **状态**：Open
- **作者**：@mgprona
- **时间**：2026-08-04 创建 / 2026-09-07 更新
- **评论 / 点赞**：1 / 1
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2584

**摘要**：在 Windows 11 环境下运行 Kimi Code CLI 0.31.1，使用默认订阅与默认模型时，用户使用泰文或其他 IME 输入法在 prompt 中输入文本会出现字符重复问题。

**关注原因**：这是典型的本地化输入缺陷，会直接影响泰国、日本、中文等依赖 IME/组合字符输入的用户。该问题从 8 月 4 日创建至今仍未关闭，说明可能涉及终端输入底层处理，值得 Windows 用户重点关注。

---

### 2. [#2637] Bug：Agent 陷入重复 Read-tool 循环，无法输出 Edit 调用
- **状态**：Open
- **作者**：@devalirzayev
- **时间**：2026-09-07 创建 / 更新
- **评论 / 点赞**：0 / 0
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2637

**摘要**：在 0.41.0 版本中，Agent 反复调用 Read 工具，陷入死循环，始终无法进入实际编辑文件的阶段。

**关注原因**：这是直接阻塞核心编码流程的稳定性缺陷。如果用户正在使用 Agentic 模式自动修改代码，这类工具循环会导致任务长时间无进展，并大量消耗上下文窗口和 token。虽然刚创建且暂无评论，但问题复现路径明确，建议后续跟进。

---

### 3. [#1354] [增强] Plan（计划）模式
- **状态**：Closed
- **作者**：@panzhiyi87-droid
- **时间**：2026-03-06 创建 / 2026-09-07 更新
- **评论 / 点赞**：1 / 7
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/1354

**摘要**：用户希望 Kimi Code CLI 提供内置 Plan 模式。曾尝试通过自定义 skill 实现，但 Kimi Code 经常在规划讨论完成前就自主开始执行代码操作。

**关注原因**：该 Issue 是当前数据中点赞数最高的（7 👍），说明社区对其有明确需求。虽然 Issue 状态为“已关闭”，但 9 月 7 日仍有更新活动，可能意味着官方已部分实现、或用户在跟进新的讨论。Plan 模式是 Agent 类 CLI 产品中最核心的执行控制机制之一，能防止 Agent“抢跑”。

---

### 4. [#1356] [增强] 无缝迁移其他主流 Agent CLI 的 MCP Skill 配置
- **状态**：Closed
- **作者**：@deshes
- **时间**：2026-03-06 创建 / 2026-09-07 更新
- **评论 / 点赞**：0 / 0
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/1356

**摘要**：Kimi Code CLI 用户同时也在使用 Claude Code、Cursor、Windsurf、Continue 等工具。这些工具都支持 MCP（Model Context Protocol）服务或技能配置，但各家存储格式不同，导致用户难以平滑迁移到 Kimi CLI。

**关注原因**：MCP 配置的“碎片化”是当前 AI 编程工具生态的真实痛点。若 Kimi CLI 能兼容、导入其他 CLI 的 MCP/Skill 配置，将显著降低用户从其他工具切换的迁移成本，是拉新和留存的有效手段。该 Issue 同样在 9 月 7 日被更新，暗示了社区延续关注度。

---

## 重要 PR 进展

> 说明：过去 24 小时更新的 PR 共 2 条，以下完整列出。

### 1. [#2616] 支持通过 Build Remote Agent 进行手机配对（

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-09-08

## 今日速览

Issue 侧最鲜明的信号是编辑器集成需求持续高热：VS Code 官方扩展请求（#11176）以 148 👍 和 29 条评论稳居榜首，且已跨越半年仍未关闭。与此同时，会话卡死类问题呈现集中爆发态势：至少 4 个独立 Issue（#43277、#44747、#37580、#45011）分别描述会话永久卡死、子代理权限请求丢失、SSE 静默断流以及 Web 端会话不可见，稳定性成为当前社区共识性痛点。PR 方面，Moonshot provider 的加入（#47851）和桌面端更新机制改进（#47858）是近期合并/活跃度较高的功能型改动。

## 版本发布

过去 24 小时内无新版本发布。

## 社区热点 Issues

### 1. VS Code 官方扩展 [#11176]
OpenCode 官方 VS Code 扩展的呼声已持续半年以上。29 条评论、148 个 👍，是当前社区关注度最高的 Request。摘要指出希望以原生扩展形态在 VS Code 内运行，而非通过 TUI/终端间接使用。
🔗 https://github.com/anomalyco/opencode/issues/11176

### 2. 会话在正常使用中永久卡死，重启无法恢复 [#43277]
设计核心的 session 层缺陷：多个会话在正常使用时进入"永久卡死"状态，拒绝新消息，重启系统和服务均无法恢复。虽只有 1 个 👍，但严重性被 8 条评论反复印证。
🔗 https://github.com/anomalyco/opencode/issues/43277

### 3. Mistral 托管 GLM-5.2 工具调用失败 [#43199]
Mistral 开始托管第三方开源模型（GLM-5.2）。用户手动添加该模型后文本响应正常，但一旦调用工具即报错。反映 provider 兼容层对新兴模型/托管模式支持不足，评论 9 条。
🔗 https://github.com/anomalyco/opencode/issues/43199

### 4. VS Code Copilot BYOK 语言模型 provider 扩展 [#27303]
VSCode Copilot 已支持 BYOK（Bring Your Own Key）和外部语言模型 provider 扩展，用户期待 OpenCode 提供官方 Go/Zen BYOK 扩展接入 Copilot。虽仅有 6 条评论，但与 #11176 呼应，标明 IDE 集成方向的重要性。
🔗 https://github.com/anomalyco/opencode/issues/27303

### 5. Go 订阅额度耗尽后 Zen 余额未被使用 [#42938]
用户订阅 Go 套餐达到月度 100% 用量后被阻塞 12 小时。尽管已开启 "Use balance" 且 Zen 余额有 $39.89，但按文档应回退到 Zen 余额的逻辑并未生效。涉及计费/订阅系统的预期管理，评论 6 条。
🔗 https://github.com/anomalyco/opencode/issues/42938

### 6. gpt-5.6-sol-fast/high 推理中断：rs_*:0 not found [#36241]
macOS 上使用 OpenAI Codex OAuth 并在高推理强度下，流式输出反复中断，报 `reasoning part rs_<redacted>:0 not found`。指向特定模型+推理变体组合的兼容问题，6 条评论。
🔗 https://github.com/anomalyco/opencode/issues/36241

### 7. CLI/TUI 创建的会话在 Web Home 不可见 [#45011]
来自 CLI/TUI/`opencode run` 创建的会话永远不会出现在 Web UI 首页——项目注册表仅存在于浏览器端（client-side only），显示为空列表。项目切换/找回成本很高，评论 6 条。
🔗 https://github.com/anomalyco/opencode/issues/45011

### 8. commentary 通道未实现导致模型对话中途结束 [#47168]
gpt.txt 系统提示要求模型通过 `commentary` 通道发送进度更新，但代码中根本没有实现该通道。在 chat-completions 模型上，每条这样的消息都会意外终止 turn。文档 — 实现不一致的典型案例，5 条评论。
🔗 https://github.com/anomalyco/opencode/issues/47168

### 9. SSE 流静默中断导致会话和子代理永久挂起 [#37580]
ChatGPT 订阅（openai provider, codex auth）下的子代理在运行中冻结、永不恢复。父会话永远 busy，且 `chunkTimeout` 在 openai 路径上无默认值。稳定性关键缺陷，4 条评论、3 👍。
🔗 https://github.com/anomalyco/opencode/issues/37580

### 10. 插拔式"数据流面板"需求 [#46156]
用户希望 TUI/桌面端在会话窗口预留专用的插件数据流侧栏/面板，让插件可以实时展示结构化日志、指标和上下文仪表板，避免污染聊天流。生态建设向可观测性延伸的信号，4 条评论。
🔗 https://github.com/anomalyco/opencode/issues/46156

### 备选关注
- **Auto Router 错误信息改进**（#47794，4 评论）：当前仅显示 `rate_limit_exceeded`，无法辨识 Auto Router 尝试连接的具体模型，排障困难。
- **OpenCode Desktop 更新打断未完成任务**（#47850，2 评论）：点击更新后桌面应用直接退出，正在执行的 prompt 被强杀，无等待/确认机制。

## 重要 PR 进展

### 1. feat(ai): 新增 Moonshot provider [#47851]
新增 Moonshot 门面，默认走 Chat Completions，并提供显式的 `.chat`、`.messages`、`.responses` 选择器；提供方模块仅 145 行，复用共享协议实现。该 PR 仍在开放状态。
🔗 https://github.com/anomalyco/opencode/pull/47851

### 2. feat(tui): 浏览 projects、directories 与 worktrees [#45029]
新增 TUI 项目打开对话框，支持列出 Git worktree、嵌套项目目录以及非 Git 目录（与既有会话关联），避免必须先打开错误项目再切换的窘境。仍在开放中。
🔗 https://github.com/anomalyco/opencode/pull/45029

### 3. fix(session): 清除归档时间戳而不是静默忽略 [#47848]
修复会话取消归档后时间戳未被重置的问题；同时处理了后端一半的 #24153，web UI 部分由 #43919 跟进。
🔗 https://github.com/anomalyco/opencode/pull/47848

### 4. fix(snapshot): 限定回滚补丁范围并保护删除操作 [#47861]
关键 bug 修复：快照存储是 worktree 全局的（`snapshot/<project>/<worktree-hash>`），但补丁文件列表写的是项目绝对路径——回滚补丁时可能误伤同项目中其他 worktree 的文件；本次会限定作用域且保护删除操作。关闭 #40736、#33940、#46783。
🔗 https://github.com/anomalyco/opencode/pull/47861

### 5. feat(app): 会话消息时间线导航条 [#41135]
长会话导航困难，PR 实现了一种紧凑的 DeepSeek-web 风格的"序列圆点导航条"（替代完整侧边栏），支持消息维度快速跳转。
🔗 https://github.com/anomalyco/opencode/pull/41135

### 6. fix(provider): 转发 config 自定义模型的 agent 温度 [#41016]
`opencode.json` 中以 `provider.<id>.models` 定义的自定义模型默认无 temperature 能力，导致 agent 级温度被静默丢弃。此 PR 修复了该问题（关闭 #34554）。
🔗 https://github.com/anomalyco/opencode/pull/41016

### 7. fix(console): 保留 Anthropic 工具名称 [#41130]
修复 Anthropic `/messages` → OpenAI 兼容 `/chat/completions` 转换中工具定义被错误改名问题（修复 #41120），保证 tool calling 跨协议稳定。
🔗 https://github.com/anomalyco/opencode/pull/41130

### 8. fix(app): tab 挂起时始终保持进度可见 [#47835]
去除 `revealProjectOnHover` 及 hover-only 头像包裹/分组样式。session 处于 busy 状态时进度指示器常驻可见，不再需要 hover 才能查看。
🔗 https://github.com/anomalyco/opencode/pull/47835

### 9. feat(updates): 在 opencode.ai/update 路径下提供更新服务 [#47858]
将既有 update Worker 挂载到 `opencode.ai/update` 并保留原有 hostname；同时为 AUR 本地制品发布作准备。影响桌面端/CLI 更新链路。
🔗 https://github.com/anomalyco/opencode/pull/47858

### 10. fix(acp): 为 todos 发送 plan 类更新消息 [#41132]
将 OpenCode 的 `todo.updated` 事件映射为 ACP `session/update` 消息（`sessionUpdate: "plan"`），使 ACP 客户端能像 plan 模式一样实时看到 todo 变化（关闭 #40745）。
🔗 https://github.com/anomalyco/opencode/pull/41132

### 备选关注
- **fix(session-ui): 对齐 retry 图标与文本**（#47859）：删除 spinner 遗留的偏移，为对齐新增几何回归组件测试。
- **fix(console): 标准化工具根级合成 schema**（#41128）：补全 OpenAI-compatible 工具 Schema `oneOf/anyOf/allOf` 根级归一化。
- **内置 schema 根对象直接暴露**（#41127）：生成的公共配置 schema 不再包一层空壳。
- **LSP 静态工作区诊断支持**（#41122）：`workspacePullState()` 根据语言服务器声明能力正确拉取静态诊断。

## 功能需求趋势

1. **官方 IDE 扩展与编辑器生态集成**（最强烈）
   #11176（VS Code Extension）持续高热；#27303 要求 BYOK provider 扩展接入 Copilot；#47842 及 #47820 等 Issue 表明用户正在尝试将 OpenCode 嵌入 Cursor、Tencent WorkBuddy/CodeBuddy 等第三方编辑器，兼容性失败会立即被报告。官方 SDK/本地 Server 的 OpenAI 兼容端点需求（#31724）也与此同源。

2. **新增模型/Provider 支持持续高频**
   新增提供商支持（#47851 Moonshot PR）、新托管模型适配（#43199 GLM-5.2）、OpenAI 最新模型推理路径兼容等问题集中出现（#36241），反映社区对"开箱即跑新模型"的强烈预期。

3. **Web/Desktop UI 与 CLI/TUI 跨端一致性**
   多个 Issue 指向不同前端会话列表/项目注册表数据不一致的问题（#45011、#46444、#47834）。多端会话同步成为桌面客户端/Web 用户的核心诉求。

4. **会话稳定性/可恢复性**
   半数高热度 Issue 指向同一类问题：会话永久 stuck（#43277）、子代理权限请求被吞导致父会话死等（#44747）、SSE 流中断后无超时兜底（#37580）。这一方向的 PR/修复优先级预计会提高。

5. **插件系统与可观测性扩展**
   #46156 提议在会话页为插件保留专属数据面板——将插件能力从"干预编辑/文件操作"扩展至"实时指标和仪表板"，是插件生态成熟的信号。

## 开发者关注点

- **账户/余额回退逻辑透明化**：Go 订阅额度耗尽后 Zen 余额未能自动兜底（#42938），用户需要更清晰、可预期的扣费/回退策略。
- **配置路径和权限预期管理**：更新工具总是把新版本写入 APPDATA 而非用户指定安装路径（#17044）；自动模式（Auto mode）下重复误报权限请求（#47545）；Auto Router 错误无法识别实际尝试的模型（#47794）。
- **AI 内置警告频发**：OpenCode 本身正在用 AI 自动生成的 Issue/PR 若清理不及时（如大量 automated

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*