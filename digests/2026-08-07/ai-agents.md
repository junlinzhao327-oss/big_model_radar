# OpenClaw 生态日报 2026-08-07

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-07 01:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告



---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-08-07

## 1. 今日速览

过去 24 小时，OpenHands SDK 处于**高活跃度**状态：15 条 Issue 更新（8 条新开/活跃、7 条关闭），29 条 PR 更新（15 条待合并、14 条已合并/关闭），并正式发布 **v1.41.0**。今日主线是 **Canvas Extensions** 首批安全与持久化基础组件合入 v1.41.0（manifest 校验、entrypoint 包含检查、安装持久化修复等），同时 **ACP 可观测性**（LLM/TOOL spans）与 **Bash 事件分页**等稳定性 bug 也已完成修复并合入。值得关注的是，用户侧仍不断报告新的安全和稳定性问题（secrets 明文写入 `.git/config`、分页游标死循环、事件静默丢失等），但均已有对应 fix PR 跟进，项目修复响应速度较快。

---

## 2. 版本发布

### [v1.41.0](https://github.com/OpenHands/software-agent-sdk/releases)（2026-08-06）

Release PR：[#4393](https://github.com/OpenHands/software-agent-sdk/pull/4393)

已确认的变更内容：

- **feat(agent-server): Canvas Extensions manifest and containment [1/4]**（[#4361](https://github.com/OpenHands/software-agent-sdk/pull/4361)，@VascoSch92）— Canvas Extensions 四步计划的第一步：manifest 模型、校验与 entrypoint 包含检查落地。
- **fix(observability): give delegate conversations their own detached Laminar trace**（@simonrosenberg）— 修复委派会话的 Laminar trace 归属问题。

**破坏性变更**：暂无确认信息。

**迁移注意事项**：尚未获取完整变更日志，若你正在使用 Canvas Extensions 的早期实验接口，建议关注后续 [1/4] 剩余 PR 的合入动态。完整 changelog 请查看 [Release v1.41.0](https://github.com/OpenHands/software-agent-sdk/releases/tag/v1.41.0)。

---

## 3. 项目进展

今日合入/关闭的关键 PR 展示了**安全加固**、**可观测性**与**社区 PR 吸收**三条主线：

### Canvas Extensions 安全基础（首批合入）

围绕 #4348–#4351 四个安全相关 Issue，对应的实现已随 v1.41.0 合入或关闭：

- **[#4348](https://github.com/OpenHands/software-agent-sdk/issues/4348) manifest 模型与 entrypoint 包含检查** — 已关闭，包含路径穿越与 symlink 逃逸的对抗性测试（安全关键）
- **[#4350](https://github.com/OpenHands/software-agent-sdk/issues/4350) 安装持久化：修复 disabled-by-default 与 self-heal auto-enable** — 已关闭（priority: high, security-related）
- **[#4351](https://github.com/OpenHands/software-agent-sdk/issues/4351) staged install + 原子替换 + 两步刷新** — 已关闭（priority: high, security-related）
- **[#4349](https://github.com/OpenHands/software-agent-sdk/issues/4349) 安装记录增加 requested_ref 字段** — 已关闭

### ACP 可观测性补齐

- **[#4376](https://github.com/OpenHands/software-agent-sdk/pull/4376) feat(observability): emit LLM and TOOL spans for ACP turns**（@simonrosenberg）— 已合并，修复 [#4373](https://github.com/OpenHands/software-agent-sdk/issues/4373)（ACP 会话轨迹为空），使 ACP 对话可被 Laminar 等工具完整重建。

### 社区贡献吸收

- **[#4362](https://github.com/OpenHands/software-agent-sdk/pull/4362) 使 conversation worktree root 可配置**（@xmrflipflop，首次贡献者）— 已合入。解决 `/tmp/conversation-worktrees/` 硬编码、`/tmp` 被清理导致工作区丢失的问题。配套讨论见 [#4398](https://github.com/OpenHands/software-agent-sdk/issues/4398)。
- **[#4207](https://github.com/OpenHands/software-agent-sdk/pull/4207) feat: structured output**（@luciobaiocchi）— 已关闭/合并，兑现 [#2566](https://github.com/OpenHands/software-agent-sdk/issues/2566) 关于 first-class structured output 的长期请求。

### 维护与依赖

- **[#4391](https://github.com/OpenHands/software-agent-sdk/pull/4391)** bump claude-agent-acp 至 0.63.0、codex-acp 至 1.1.7
- **[#4346](https://github.com/OpenHands/software-agent-sdk/pull/4346)** json-repair 0.54.2 → 0.60.1

---

## 4. 社区热点

> 注：本次 PR 数据未提供评论数，以下基于 Issue 评论热度分析。

| 热度 | Issue | 状态 | 评论数 | 分析 |
|---|---|---|---|---|
| 🔥 最高 | [#2566 Structured Output 功能请求](https://github.com/OpenHands/software-agent-sdk/issues/2566) | 已关闭 | 16（累计） | 历史最活跃的功能诉求之一，关联 #1566、#4116、#2808 等多条线索。随着 PR [#4207](https://github.com/OpenHands/software-agent-sdk/pull/4207) 合入，该请求正式落地为 first-class 支持。 |
| 中 | [#3746 max_input_tokens 在 headless CLI 模式不生效](https://github.com/OpenHands/software-agent-sdk/issues/3746) | OPEN（stale, priority: low） | 3 | 用户配置了 `llm.max_input_tokens` 但运行时完全无效，属于配置可信度问题。已标记 stale 且低优先级，社区关注度有限。 |
| 中 | [#4288 reference-only credentials 设计文档](https://github.com/OpenHands/software-agent-sdk/issues/4288) | OPEN | 2 | 安全架构设计：凭证仅引用、运行时安全交付。由 @simonrosenberg 发起，正值 Canvas 重构从 enterprise 私有仓库迁回，属于长期安全路线图的一部分。 |
| 低 | [#4399 secrets 明文写入 .git/config](https://github.com/OpenHands/software-agent-sdk/issues/4399) | OPEN（priority: high） | 1 | 新报告的高危安全问题，但已有 fix PR [#4401](https://github.com/OpenHands/software-agent-sdk/pull/4401) 跟进（已关闭/合并）。 |

**核心诉求分析**：社区热度集中在两个方向——（1）**产物可靠性**：结构化输出、可观测性 trace 完整重建；（2）**安全默认值**：secrets 不应被模型诱导写入任何明文位置。两者都获得了快速响应。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue | 描述 | 状态 |
|---|---|---|---|
| 🔴 High | [#4399](https://github.com/OpenHands/software-agent-sdk/issues/4399) | **CustomSecretsSection 诱导模型将 secrets 写入 .git/config 明文** — 系统提示中的 `<CUSTOM_SECRETS>` 块给了模型错误示例 | 已有 fix：[#4401](https://github.com/OpenHands/software-agent-sdk/pull/4401) 已关闭（禁止在 git remote URL 中推荐 secrets） |
| 🟠 Medium | [#4388](https://github.com/OpenHands/software-agent-sdk/issues/4388) | **search_bash_events 分页在 order__gt 过滤下错误** — 先按文件数选页再过滤，导致页面不足、客户端拿到空 next-page 后死循环 | 已有 fix：[#4396](https://github.com/OpenHands/software-agent-sdk/pull/4396) OPEN |
| 🟠 Medium | [#4386](https://github.com/OpenHands/software-agent-sdk/issues/4386) | **_emit_event_from_thread 静默吞掉异常** — run_in_executor 返回的 Future 被丢弃，磁盘满/序列化错误时 LLM 统计与日志事件静默丢失 | 暂无 fix PR |
| 🟠 Medium | [#4387](https://github.com/OpenHands/software-agent-sdk/issues/4387) | **agent-server close() 10s 超时 < wait_for_pending 30s 上限** — 二次取消会中断 finally 块，`_publish_state_update` 永不触发 | 暂无 fix PR |
| 🟡 Low | [#3746](https://github.com/OpenHands/software-agent-sdk/issues/3746) | **max_input_tokens 在 headless CLI 模式不生效**（stale, priority: low） | 无进展 |

**稳定性判断**：今日报告的 bug 集中在 agent-server 的**边界条件**：超时竞态、分页游标、异常静默。分页问题已在修复中（#4396），但 #4386/#4387 尚无对应 PR，建议维护者优先关注。

---

## 6. 功能请求与路线图信号

| 信号 | Issue/PR | 类型 | 判断 |
|---|---|---|---|
| 🧩 **Agent Plugins（agent-plugins.org）便携包格式支持** | [#4405](https://github.com/OpenHands/software-agent-sdk/issues/4405) | 新 Spec（Needs Design） | 由 @VascoSch92 提出，是 Canvas Extensions 生态的重要外部标准化动作。尚处设计阶段，**大概率进入 next milestone**。 |
| 🖥 **Canvas Extensions REST API surface** | [#4352](https://github.com/OpenHands/software-agent-sdk/issues/4352) / PR [#4395](https://github.com/OpenHands/software-agent-sdk/pull/4395) | 功能实现 | PR 已提交（OPEN），install/list/enable/disable/uninstall/bundle API 即将落地。 |
| 🎯 **Structured Output first-class 支持** | [#2566](https://github.com/OpenHands/software-agent-sdk/issues/2566) / PR [#4207](https://github.com/OpenHands/software-agent-sdk/pull/4207) | 功能落地 | **已合入**，下一版本即可使用。 |
| 🔄 **MCP 2.x 兼容 shim** | [#4406](https://github.com/OpenHands/software-agent-sdk/pull/4406) | 兼容性修复 | 用户在 mcp 2.x 环境下 browser tool 完全无法构造，提交了本地验证过的 shim。mcp 依赖已在 [#4347](https://github.com/OpenHands/software-agent-sdk/pull/4347) 中 bump 至 1.28.1，此 PR 是前瞻性修复。 |
| ⚙️ **ACP model/effort 切换** | [#4384](https://github.com/OpenHands/software-agent-sdk/pull/4384) | 功能增强 | 社区用户 @ryanskidmore 已在本地 fork 验证，希望 OpenHands + Claude Code 作为日常驱动。 |
| 🔑 **Reference-only credentials 安全设计** | [#4288](https://github.com/OpenHands/software-agent-sdk/issues/4288) | 架构设计 | 安全路线图标杆，短期内不会落地但值得跟踪。 |

---

## 7. 用户反馈摘要

> 基于 Issue 数据（PR 数据未含评论，以下推断来自 Issue 描述与上下文）。

- **结构化输出是长期痛点**（#2566）：从 2026-03-25 提起，历经 16 条评论、关联 3 个相关 Issue/PR，今日随 #4207 合入获得解决。说明社区对**可重试、可验证的 LLM 输出格式**有强烈且持续的需求。
- **配置不生效伤害信任**（#3746）：headless CLI 下 `llm.max_input_tokens` 静默无效，用户做了完整配置排查（sanitized config）。这类问题容易被标记 stale，但对 CLI 重度用户影响直接。
- **ACP 功能陈旧阻碍日常使用**（#4384）：用户明确表示"希望 OpenHands +

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-07

## 1. 今日速览

过去 24 小时项目保持高强度迭代：共 69 条 Issue 更新（新开/活跃 18 条，关闭 51 条），31 条 PR 更新（合并/关闭 21 条，待合并 10 条），并发布了 v0.84.0。最值得关注的是新版本引入的 Fullscreen TUI 模式，但随之而来两个 TUI 崩溃类 Bug（#7736、#7737）当天即被快速定位并关闭，说明 TUI 相关功能正处于密集打磨期。社区侧，Windows 使用体验（#7547，22 评论）和 auto-compaction 不触发（#6879，15 👍）是最受关注的两个议题。整体项目健康度良好，修复与功能提交均保持较高吞吐。

## 2. 版本发布

**v0.84.0** 于今日发布，核心新特性为：

- **Fullscreen TUI mode** — 支持在常规与全屏模式之间运行时切换，提供 sticky 编辑器和底部栏、可独立滚动的 transcript 区域，以及可拖动的滚动条。详见 [UI & Display 文档](https://github.com/earendil-works/pi/blob/v0.84.0/packages/coding-agent/docs/setting)。

该版本同时包含若干 TUI 相关的修复（如多击文本选择、全屏复制时多余换行等）。目前未见明确的破坏性变更公告，但全屏模式作为新交互形态，建议使用 TUI 的用户关注升级后的键位与鼠标行为变化。

## 3. 项目进展

今日合并/关闭的 PR 覆盖 TUI、Agent 核心、开发者体验三大方向，共 21 条 PR 完成合并或关闭：

**TUI 稳定性与体验**
- [#7733 fix(tui): correct multi-click text selection](https://github.com/earendil-works/pi/pull/7733) — 修复双击选词包含尾随空白等行为问题
- [#7721 fix(tui): avoid unwanted newlines when copying in fullscreen](https://github.com/earendil-works/pi/pull/7721) — 修复全屏模式下复制长行文本时引入多余换行的问题
- [#7718 fix(tui): preserve scrollback on content-driven full redraws](https://github.com/earendil-works/pi/pull/7718) — 修复重绘时丢失终端回滚缓冲的问题

**Agent 核心正确性**
- [#7717 fix(agent): reject reset during active runs](https://github.com/earendil-works/pi/pull/7717) — 修复 `Agent.reset()` 在活动运行中被调用导致 transcript 状态损坏的问题（对应 #7703）
- [#7715 feat(agent): allow blocked tool calls to terminate](https://github.com/earendil-works/pi/pull/7715) — 为被拦截的工具调用增加 `terminate` 提示能力（对应 #5998），扩展可在拦截工具调用时建议 Agent 结束回合

**开发者体验与平台**
- [#7685 fix(coding-agent): disable bunfig autoload in compiled binaries](https://github.com/earendil-works/pi/pull/7685) — 修复编译后的二进制文件意外加载 `bunfig.toml` preload 导致启动崩溃的问题
- [#7681 Support AGENTS.override.md as per-directory context override](https://github.com/earendil-works/pi/pull/7681) — 新增最高优先级的目录级上下文文件支持
- [#7659 feat(ai): add Qwen Token Plan Individual provider](https://github.com/earendil-works/pi/pull/7659) — 新增 Qwen Token Plan 个人版内建 provider
- [#7671 feat(coding-agent): colocate tool prompt contributions with tool definitions](https://github.com/earendil-works/pi/pull/7671) — 将工具的系统提示词与工具定义内聚，便于维护
- [#7686 feat(coding-agent): add configurable Harness factory](https://github.com/earendil-works/pi/pull/7686) — Harness v2 方向的可配置工厂
- [#7729 docs(coding-agent): reconcile keybinding behavior](https://github.com/earendil-works/pi/pull/7729) — 文档与实际键位行为对齐

整体来看，Agent 核心的并发/重置语义正在收紧，TUI 打磨是当前迭代重点，同时外部 provider 生态在持续扩展（Qwen、Ollama Cloud、Bedrock、LLM Gateway 等）。

## 4. 社区热点

**#7547 [Windows] How do you use Pi on windows? What issues are you seeing?** — 22 条评论，1 👍
[链接](https://github.com/earendil-works/pi/issues/7547)
社区主动发起 Windows 使用情况调研，讨论如何聚焦 Windows 支持的能量分配。这是目前社区最热烈的讨论，说明 Windows 用户基数可观且支持方式分散（WSL、原生、远程等），维护者需要明确核心支持路径。

**#7399 truncateToWidth() leaves dangling OSC 8 hyperlink** — 13 条评论
[链接](https://github.com/earendil-works/pi/issues/7399)
终端超链接截断后未闭合 OSC 8 序列，导致终端渲染异常。属于比较底层的 TUI 渲染正确性问题，用户提供了无需扩展即可复现的最小用例。

**#6879 auto-compaction never triggers until provider overflow** — 12 条评论，15 👍
[链接](https://github.com/earendil-works/pi/issues/6879)
用户报告在一次超过 2 小时的 agentic 会话中，上下文使用率超过 100% 持续攀升，compaction 直到 API 在 373k tokens 处拒绝请求才触发。15 个 👍 表明这是大量用户的真实痛点。

**#7128 New default PI_* guideline over-encourages unnecessary bash calls** — 10 条评论，5 👍
[链接](https://github.com/earendil-works/pi/issues/7128)
最新的系统提示词中"检查 PI_* 环境变量"的指导导致了 Agent 频繁执行不必要的 env 检查命令。用户指出这偏离了任务本身，属于提示词工程回归。

## 5. Bug 与稳定性

按严重程度排列：

**严重**
- [#7736 Uncaught exception when exceeded terminal width](https://github.com/earendil-works/pi/issues/7736) — v0.84.0 中渲染行超过终端宽度直接导致进程崩溃（`pi exiting due to uncaughtException`）。已关闭，修复方向为让自定义组件正确 truncate。同日 [#7737](https://github.com/earendil-works/pi/issues/7737) 报告了同根因问题（TUI throws on over-wide lines），也已关闭。
- [#6879 auto-compaction never triggers](https://github.com/earendil-works/pi/issues/6879) — 上下文压缩在超过 100% 后仍不触发，直到 provider 报错。**尚未关闭，15 👍，需重点跟进**。用户建议在每个 agentic 步骤后检查上下文水位。
- [#7702 DeepSeek models 400: reasoning_content must be passed back](https://github.com/earendil-works/pi/issues/7702) — 通过 opencode zen gateway 使用 DeepSeek 模型时，多轮/工具调用会话因未回传 `reasoning_content` 而报 400。**开放中，inprogress**。

**中等**
- [#7600 pi-coding-agent leaks X11 connections](https://github.com/earendil-works/pi/issues/7600) — 长运行进程 8 天内泄漏 182 条 X server 连接，填满 256 客户端表后导致所有新 X 客户端失败。**开放中**，对 Linux 桌面用户影响大。
- [#7321 Multi-line paste broken without bracketed paste (Termux)](https://github.com/earendil-works/pi/issues/7321) — 不支持 bracketed paste 的终端（如 Termux）粘贴多行文本时首个 `\r` 触发 submit。**开放中**。
- [#7399 truncateToWidth() dangling OSC 8 hyperlink](https://github.com/earendil-works/pi/issues/7399) — 截断后留下未闭合的超链接转义序列。已关闭，但未在 PR 列表中看到明确修复，建议确认修复方式与版本。

**轻微（已修复/已关闭）**
- [#7703 Agent.reset() leaves assistant-only transcript](https://github.com/earendil-works/pi/issues/7703) — 已由 #7717 修复。
- [#7413 Compaction fails on GitHub Copilot GHE.com](https://github.com/earendil-works/pi/issues/7413) — GHE.com 企业账号 `/compact` 报 "unknown stamp" 错误，已关闭。
- [#6662 Mouse select+copy scrolls to bottom](https://github.com/earendil-works/pi/issues/6662) — 已关闭。

## 6. 功能请求与路线图信号

**TUI 增强（当前最热门方向）**
- [#7725 Select word with double click in fullscreen TUI mode](https://github.com/earendil-works/pi/issues/7725) — 双击选中整个单词，拖拽扩展选择。与 #7733 修复直接相关，预计继续迭代。
- [#7735 Half-page scroll keybindings for fullscreen transcript](https://github.com/earendil-works/pi/issues/7735) — 半页滚动快捷键（当前是全页滚动），已有关闭记录但未见对应 PR，可能已实现。
- [#7720 Allow disabling select to copy in fullscreen TUI mode](https://github.com/earendil-works/pi/issues/7720) — 增加开关以避免选中即复制造成剪贴板被意外覆盖。

**Provider 生态（对应 PR 已在队列中）**
- [#7742 feat(ai): Ollama Cloud support](https://github.com/earendil-works/pi/pull/7742) — 新增 Ollama Cloud provider，使用 `OLLAMA_API_KEY`，混合本地/云连接。开放中。
- [#7668 Support LM Studio as first-class provider](https://github.com/earendil-works/pi/issues/7668) — 请求通过 `/login` 方式支持 LM Studio，当前 models.json 方式体验不佳。
- [#6216 feat: Add Amazon Bedrock Mantle OpenAI Responses provider](https://github.com/earendil-works/pi/pull/6216) — Bedrock Mantle Responses

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 开源项目动态日报（2026-08-07）

## 今日速览

过去 24 小时 LiteLLM 仓库保持高热度的开发与社区活动：共更新 59 条 Issue（38 条新开/活跃、21 条关闭）与 248 条 PR（163 条待合并、85 条已合并/关闭），但无新版本发布。开发重心集中在代理安全加固（身份断言、登录限速）、路由策略精细化（会话亲和、输出 Token 预估）与多 Provider 适配（Azure 政府云、SCX.ai、OpenAI TTS 流式）。社区关注度最高的议题为限流可靠性、版本回归与 Admin UI 使用体验。整体看，项目迭代节奏密集，维护者对 Issue/PR 有持续响应，但长期积压的 stale 条目与未合并 PR 仍需关注。

---

## 项目进展

今日合并/关闭的 85 条 PR 中，以下几项对项目有实质推进：

- **[#36121]

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-07

## 今日速览

过去 24 小时项目整体活跃度较高，核心开发集中在可靠性专题（reliability-2026）与匹配器（matching）性能优化上。PR 更新 29 条，其中 5 条已合并/关闭，24 条处于待合并状态，代码审查流动顺畅；Issue 侧仅新增 1 条 K8s 环境下的潜在 Bug 报告，且已有对应修复 PR 在同日提交，社区响应迅速。值得关注的是，今日新提交的 PR 中有多条直接针对昨日/近期报告的 Bug 展开修复，呈现出"问题报告→修复提交"的快速闭环。整体来看，项目处于稳健的迭代节奏，可靠性方向的系统性改进仍在持续推进。

- 活跃度评估：高（PR 29 条，其中 5 条合并/关闭）
- Issue 数量：低（1 条新增，无已关闭）
- 新版本发布：0 个


## 项目进展

今日合并/关闭的 5 条 PR 覆盖了命名空间聚合、worker 部署版本管理、时间跳过行为验证三个方向，另有多条处于待合并状态的高价值 PR 正在推进。

### 已合并/关闭

1. **#11189 Add TemporalNamespaceDivision group by column allowlist**（已合并）
   - 为系统工作流引入命名空间划分的 group by 列白名单，支持跨 Archetype 聚合，为后续系统级分析和观测能力奠定基础。
   - https://github.com/temporalio/temporal/pull/11189

2. **#11426 Gate worker deployment version demotion signals**（已合并）
   - 新增全局动态配置 `matching.enableWorkerDeploymentVersionDemotionSignal`，默认关闭信号降级路径，恢复传统 `SyncWorkerDeploymentVersion` 更新路径。这是对 worker 部署版本管理机制的一次兼容性保护，避免旧版本客户端因信号缺失而出现行为差异。
   - https://github.com/temporalio/temporal/pull/11426

3. **#11376 new functional test for time skipping behavior during pause and unpause**（已合并）
   - 新增功能测试，覆盖工作流暂停/恢复期间的时间跳过行为，并验证相关配置在暂停状态下可保存、恢复后时间跳过正常衔接。增强了时间跳过机制在嵌套/暂停场景下的回归保障。
   - https://github.com/temporalio/temporal/pull/11376

### 待合并高价值 PR（节选）

4. **#11114 matching: backlog-aware client poll load balancing**（reliability-2026）
   - 消费服务端下发的 per-partition backlog 计数，让 poller 优先选择积压较多的 partition，避免 poller 被空 partition"困住"而其他 partition 积压。这是匹配器负载均衡的重要改进。
   - https://github.com/temporalio/temporal/pull/11114

5. **#11371 Migrate fairTaskReader outstanding tasks to a CoW btree**
   - 将 fairTaskReader 底层数据结构从 gods treemap 迁移至 tidwall/btree，利用 copy-on-write 机制重构 merge 逻辑，预期降低内存占用与锁竞争。
   - https://github.com/temporalio/temporal/pull/11371

6. **#11441 Make functional tests available to external runners**
   - 将 137 个根功能测试体迁移至可导入的注册表，并新增 runner 级集群路由、逻辑测试名、shard 清单等能力，显著提升测试框架的可扩展性。
   - https://github.com/temporalio/temporal/pull/11441

**整体判断**：项目正处于可靠性专题（reliability-2026）的密集攻坚期，从该系列 PR 的主题分布（backlog 感知、btree 迁移、队列 backlog 指标、复制流生命周期管理、DLQ 任务处理）可以看出，项目在系统性的稳定性加固上投入显著，这些改进将在未来版本中逐步落地。


## 社区热点

今日讨论/交互最为活跃的 PR 集中在匹配器可靠性和 ringpop 修复两个方向：

1. **#11114 matching: backlog-aware client poll load balancing**
   - 创建于 2026-07-16，更新于 2026-08-07（今日有更新活动），是今日最受关注的 PR 之一。该 PR 解决的是 poller 负载不均这一实际生产痛点，涉及客户端与服务端的配合改动，属于可靠性系列的核心改进，社区关注度高。
   - https://github.com/temporalio/temporal/pull/11114

2. **#11431 Fix stale ringpop healer targets**
   - 创建于 2026-08-06，更新于 2026-08-07，直接对应今日新增 Issue #11429 的修复 PR。由于该 PR 触及 K8s 环境下 pod 重启后服务发现失败的常见问题，预期会收到较多社区反馈。
   - https://github.com/temporalio/temporal/pull/11431

3. **#11255 Add immediate queue backlog age metric**
   - 由 @prathyushpv 提交，为 `shardinfo_immediate_queue_lag` 补充时间维度对应指标 `shardinfo_immediate_queue_backlog_age`，并讨论了即时任务键无时间戳带来的实现难点。观测类改进是社区长期关注点。
   - https://github.com/temporalio/temporal/pull/11255

**分析**：社区关注的热点集中在"可观测性"与"负载均衡"两大主题——前者对应运维排障需求，后者对应大规模部署下的性能稳定性诉求，两者都是生产环境用户最直接关心的方向。


## Bug 与稳定性

今日报告 1 条新 Bug，另有若干待合并 PR 也在修复既有稳定性问题。

### 新增 Bug（按严重程度排列）

1. **[高] #11429 K8s pod 重启后 ringpop healer 持续探测旧 pod IP**
   - 现象：`DiscoverProvider: statichosts.New(hostPorts...)` 在 frontend pod 重启后，temporal-worker 仍持续访问旧 pod IP，导致服务发现异常。
   - 影响：K8s 环境下滚动更新或异常重启后，worker 与 frontend 之间的连接可能中断，长期不恢复将影响任务分发。
   - 修复 PR：**#11431 Fix stale ringpop healer targets** 已于 2026-08-06 提交，将静态 bootstrap 主机列表替换为动态发现提供程序，从持久化存储刷新活跃成员地址，并附带单元测试。
   - 状态：已定位，修复 PR 待审查/合并。
   - Issue 链接：https://github.com/temporalio/temporal/issues/11429
   - Fix PR 链接：https://github.com/temporalio/temporal/pull/11431

### 待合并稳定性修复 PR

2. **[中] #11440 Don't DLQ sync versioned transition task when cleanup finds nothing to delete**
   - 源集群删除工作流后，SYNC_VERSIONED_TRANSITION 任务在目标集群触发 NotFound，清理逻辑构建 ExecutableDeleteExecutionTask 后直接调用 `Execute()` 返回原始错误，导致任务被错误地送入 DLQ。
   - 状态：WIP，修复进行中。
   - https://github.com/temporalio/temporal/pull/11440

3. **[中] #11424 Resend parent workflow asynchronously during standby child completion verification**
   - 备集群子工作流完成验证时，向主集群重发父工作流的过程涉及跨集群状态同步和可能的分页历史回填，耗时较长。该 PR 将其改为异步执行，避免阻塞关键路径。
   - https://github.com/temporalio/temporal/pull/11424

4. **[中] #11434 Check unloaded version queue backlog**
   - `AllActive` 仅覆盖已加载队列，导致未加载的 per-version backlog 被遗漏，Scaler 可能误判 partition 已排空。该 PR 修复了未加载 version queue 的 backlog 检查。
   - https://github.com/temporalio/temporal/pull/11434

5. **[低] #11443 Fixing test task manager for new matchers**
   - 适配新 matcher 逻辑的测试任务管理器修复，属于测试基础设施同步更新。
   - https://github.com/temporalio/temporal/pull/11443


## 功能请求与路线图信号

### 明确的路线图信号：reliability-2026 系列继续扩展

从今日活跃 PR 看，reliability-2026 专题仍在持续推进，覆盖以下方向：

- **匹配器负载感知**：#11114 backlog-aware client poll load balancing 让 poller 按 partition 积压⾼低动态加权，配合 #11434 的未加载队列 backlog 检查，构成完整的匹配器负载均衡体系。
- **队列数据结构优化**：#11371 CoW btree 迁移降低 fairTaskReader 的内存与锁开销。
- **复制流管理**：#11356 引入客户端侧复制流最大存活时间（含 jitter 系数），定期优雅重建复制流，避免长期运行的流因状态过期导致故障。
- **DLQ 链路修复**：#10502（纯任务执行后仍有效则入 DLQ）、#11440（清理无删除内容时不入 DLQ）从两个方向完善 DLQ 的边界处理逻辑。
- **可观测性补充**：#11255 新增 immediate queue backlog age 指标，补全队列积压的时间维度视图。

### 可能纳入下一版本的功能方向

- **worker 部署版本管理的兼容性加固**：#11426 已通过动态配置将信号降级路径默认关闭，保护旧客户端。这一配置化思路可能推广到其他兼容性敏感的特性上。
- **大规模部署的运维友好性**：#11401（namespace handover watermark 与 shard readiness 宽事件）、#11424（异步重发父工作流）都在降低运维操作的阻塞与风险。
- **本季度新增的 "K8s 环境动态服务发现"**：#11431 将 ringpop healer 从静态地址改为动态发现，是 K8s 部署场景的重要体验改进，值得关注其合入节奏。


## 用户反馈摘要

当前 Issue 池反馈较少（仅 1 条新增），从可用数据提炼如下：

1. **K8s 滚动重启后的服务发现断裂**（来自 #11429）
   - **场景**：Temporal 部署在 K8s 上，frontend pod 发生重启后，temporal-worker 仍然持续探测旧的 pod IP。
   - **诉求**：期望 ringpop healer 能感知 pod 地址变化并自动刷新成员列表，无需人工干预或手动重启 worker。
   - **满意度**：可看出用户对当前静态发现的体验不满意，但这并非新问题，而是 ringpop 静态配置在 K8s 动态网络环境下的典型局限。社区快速响应修复值得肯定。
   - https://github.com/temporalio/temporal/issues/11429

2. **跨集群数据一致性边缘场景**（来自 #11424、#11440 等 PR 的背景描述）
   - 多个 PR 均在处理跨集群复制场景下的边界条件（主备集群状态不同步、源集群删除后同步任务失败等）。虽然没有直接的 Issue 评论，但这些 PR 的存在说明社区用户在生产环境中遇到了这些场景并反馈到了 Temporal 团队。
   - https://github.com/temporalio/temporal/pull/11424 | https://github.com/temporalio/temporal/pull/11440


## 待处理积压

以下为长期未关闭或近期可能需维护者关注的项目：

1. **#9878 [stale] retry and error parsing**（创建于 2026-04-08，已积压 4 个月）
   - 为 SQL persistence 启动时的版本兼容检查增加自动重试和 error wrapping 修复。已标记为 [stale]，但今日有更新活动，建议维护者确认是否继续推进或关闭。
   - https://github.com/temporalio/temporal/pull/9878

2. **#11232 VLN-1574: remediate checkout-below-v7**（创建于 2026-07-23）
   - 自动化安全活动（camper）创建的 HIGH 严重性安全修复，涉及 checkout-below-v7 规则。安全类 PR 建议优先审查。
   - https://github.com/temporalio/temporal/pull/11232

3. **#11311 Fence Backfiller tasks by generation**（创建于 2026-07-27）
   - 使用持久化的任务序列值替代任务执行时间与 backfill HWM 比较，以正确隔离 Backfiller 任务。技术方案较复杂，需要 maintainer 仔细审查。
   - https://github.com/temporalio/temporal/pull/11311

4. **#11431 Fix stale ringpop healer targets**（创建于 2026-08-06）
   - 作为 #11429 的直接修复，建议尽快安排 review 与合并，以免 K8s 用户持续受影响。
   - https://github.com/temporalio/temporal/pull/11431

5. **#11356 Add client-side max lifetime for replication streams**（创建于 2026-07-30）
   - 复制流的最大存活时间机制，涉及跨集群复制稳定性，属于基础设施关键改动，review 周期可能较长，值得持续关注。
   - https://github.com/temporalio/temporal/pull/11356

---

**总结**：Temporal 项目今日延续了 reliability-2026 专题的密集推进节奏，匹配器负载均衡、队列数据结构优化、复制流管理等多个方向均有实质进展。K8s 环境下的 ringpop 服务发现问题获得了快速响应，修复 PR 已在审查中。整体项目健康度良好，社区反馈与开发迭代形成了正向循环。建议关注 #11431 的合入进度及 #11255 指标设计的最终落地。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*