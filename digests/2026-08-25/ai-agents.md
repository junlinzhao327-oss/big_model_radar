# OpenClaw 生态日报 2026-08-25

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-24 22:47 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-25

## 1. 今日速览

过去 24 小时项目处于高压运转状态：**500 条 Issue 更新（473 活跃 / 27 关闭）与 500 条 PR 更新（425 待合并 / 75 合并或关闭）**，活跃度极高。新版本 **v2026.8.1-beta.3** 发布，带来了 GPT-5.6 全系推理支持与 Control UI 首次运行引导改进。但从 Issue 结构看，**P1 级可靠性缺陷密集浮现**——消息丢失、会话状态损坏、进程泄漏、数据覆盖等问题占主导，且多数集中在 Telegram/Feishu 渠道投递与多智能体会话管理上。社区讨论热度最高的议题集中在 **Windows 测试基础设施问题**、**子代理完成消息投递可靠性**、**上下文压缩自主触发**以及**动态模型目录**。整体判断：功能迭代速度很快，但稳定性修复是当前最突出的短板。

---

## 2. 版本发布

### v2026.8.1-beta.3
> 发布时间：2026-08-24（数据源截取自 GitHub Releases）

**新增内容：**
- **GPT-5.6 Sol / Terra / Luna / Ultra 推理支持**：覆盖 OpenClaw 主运行时与 Codex runtime，模型能力矩阵进一步扩展。
- **Control UI 首次运行设置增强**：verified model setup 现在可延续至 Custodian 与可选渠道设置，降低新用户配置门槛。
- **Puppeteer 兼容 CDP relay 支持**：允许配对 Chrome 会话通过 CD

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026‑08‑25

> 数据窗口：过去 24 小时 | 数据来源：GitHub Issues / PR / Releases

---

## 1. 今日速览

- 过去 24 小时 **500 条 Issue 更新**（新开/活跃 314，已关闭 186，关闭率 37.2%）与 **500 条 PR 更新**（待合并 403，已合并/关闭 97，合并率 19.4%），项目整体处于**高活跃度**状态。
- **今日无新版本发布**，但社区讨论中用户已在使用 v0.20.x 系列（v0.20.0 / v0.20.5），说明更新通道存在版本追赶需求。
- 讨论热度最高的议题集中在：技能索引自动化退化（#66616，90 评论）、插件生命周期规范化（#64231）、自动化集成阻塞（#88584）、以及两类大型 bug 集群——**超时/挂起** 与 **fleet 更新可靠性**。
- 今日可见的 PR 中暂无重要合入（唯一条已关闭 PR #94263 为垃圾测试 PR），但多个 P1/P2

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-25

## 1. 今日速览

过去 24 小时项目保持高活跃度：**65 条 Issue 更新**（新开/活跃 10 条，关闭 55 条）与 **21 条 PR 更新**（9 条待合并，12 条已合并/关闭）。**v0.84.3 发布**，带来 PowerShell 工具与更安全的托管更新机制，直接回应了 Windows 用户的长期痛点。今日共关闭 55 条 Issue，合并/关闭 12 条 PR，bug 修复效率较高——其中包括修复 OpenAI 流 abort 信号、llama.cpp 预置模型不可见、xAI 类型构建错误等多个社区高频反馈的问题。整体来看，项目在 **Windows 支持、本地模型生态、AI provider 兼容性** 三条主线上均有实质推进；但同时存在 auto-compaction（#6879）等长期未决的高赞 bug 以及 Windows 相关的新增回归报告，值得持续关注。

## 2. 版本发布

### v0.84.3
> 链接：https://github.com/earendil-works/pi/releases/tag/v0.84.3

**新增功能**

- **PowerShell 工具**：Windows 上可选的原生 PowerShell 命令执行支持。文档见 [PowerShell Tool](https://github.com/earendil-works/pi/blob/v0.84.3/packages/coding-agent/docs/windows.md#powershell-tool)。这是对 Windows 用户长期抱怨 git bash 路径处理问题的直接回应（见 PR #8512，@mitsuhiko 表示"基本放弃 git bash in Windows"）。
- **更安全的托管更新**：更新流程改为分阶段执行 — stage（暂存）、verify（验证）、atomically activate（原子生效），降低更新失败导致服务不可用的风险。

**潜在注意点**

- 发布后已有用户反馈 #8582：内置 PowerShell 工具在交互模式使用 Windows PowerShell 5.1，而 `-p` 打印模式使用 pwsh，两者行为不一致。如依赖 PowerShell 7 特性需留意。
- 托管更新机制改动较大，建议升级前备份配置和 session 数据。

## 3. 项目进展

今日合并/关闭的 12 条 PR 覆盖多个方面，按主题归类：

**AI Provider 兼容性与修复**

- [#8585 fix(ai): abort OpenAI streams immediately when signal fires](https://github.com/earendil-works/pi/pull/8585) — 修复 OpenAI Responses/Completions 流在 abort 信号触发时未立即终止的问题，与 #8409 回归问题直接相关。**已合并**
- [#8578 fix(ai): pin createProvider TApi for xAI Responses provider](https://github.com/earendil-works/pi/pull/8578) — 修复 #8124 后 xAI provider 类型错误导致的构建失败。**已合并**
- [#8570 fix(ai): preserve Codex thread affinity headers](https://github.com/earendil-works/pi/pull/8570) — 为 OpenAI Codex Responses 请求补充 `thread-id` 亲和性 header，与已有的 `session-id`、`x-client-request-id` 对齐上游行为。**已合并**
- [#8302 feat(ai): amazon bedrock mantle](https://github.com/earendil-works/pi/pull/8302) — 新增 Amazon Bedrock Mantle API 支持，但该 PR 被关闭，由新的 #8572/#8573 接续推进。**已关闭**

**llama.cpp 本地模型支持**

- [#8479 fix: expose unloaded llama.cpp presets](https://github.com/earendil-works/pi/pull/8479) — 修复配置了 `--models-preset` 的 llama-server 预置模型不可选的问题。**已合并**
- [#8558 feat: show llama presets if autoload enabled](https://github.com/earendil-works/pi/pull/8558) — 在 autoload 启用时显示 `source: "preset"` 的模型。**已合并**。两条 PR 共同解决了 #8167 报告的 llama.cpp 模型无法选择的问题。

**TUI / 前端体验**

- [#8580 feat(coding-agent): drop extra vertical padding on tool rows](https://github.com/earendil-works/pi/pull/8580) — 减少工具调用行的垂直空白，提升 transcript 信息密度。**已合并**
- [#5268 fix(tui): render the hardware cursor by default so the prompt cursor hollows on blur](https://github.com/earendil-works/pi/pull/5268) — 修复终端失焦时 prompt 光标仍是实心方块的问题。**已合并**

**数据完整性与稳定性**

- [#8575 fix(coding-agent): surface + bound the torn-append replay loss in session JSONL files](https://github.com/earendil-works/pi/pull/8575) — 修复 session JSONL 文件中 torn append 导致静默丢失两条回放条目的问题。**已合并**

**新功能**

- [#8512 feat(coding-agent): add optional PowerShell tool](https://github.com/earendil-works/pi/pull/8512) — 新增 PowerShell 工具，正是 v0.84.3 发布内容。**已合并**

整体来看，今日合并的 PR 质量较高，修复了多个用户高频反馈的问题，特别是 OpenAI 流 abort、llama.cpp 模型选择、Codex 兼容性三个方向。

## 4. 社区热点

| Issue/PR | 评论数 | 👍 | 状态 | 核心诉求 |
|---|---|---|---|---|
| [#7547 [Windows] How do you use Pi on windows?](https://github.com/earendil-works/pi/issues/7547) | 44 | 2 | OPEN | 系统性收集 Windows 用户的使用方式与问题，为后续优化提供依据 |
| [#6879 auto-compaction never triggers after context grows past 100%](https://github.com/earendil-works/pi/issues/6879) | 22 | 19 | OPEN | 自动压缩机制失效，上下文超限后仍不触发，直到 API 拒绝请求 |
| [#6922 Default model cannot be a llama.cpp model](https://github.com/earendil-works/pi/issues/6922) | 11 | 14 | CLOSED | 默认模型无法配置为 llama.cpp 本地模型 |
| [#8167 Cannot pick a model with built-in llama.cpp support](https://github.com/earendil-works/pi/issues/8167) | 11 | 0 | CLOSED | llama-server 路由模式下的模型不在模型列表中显示 |
| [#8157 Migrate grok-mermaid -> lovely-mermaid](https://github.com/earendil-works/pi/issues/8157) | 10 | 1 | OPEN | 将 grok-mermaid 渲染器迁移至 lovely-mermaid，解决原有边界情况问题 |

**分析与洞察**

- **Windows 支持是当前社区最高热度话题**。#7547 已持续讨论 3 周，44 条评论收集了大量 Windows 用户的不同使用方式（WSL、原生、Git Bash、PowerShell 等）。v0.84.3 的 PowerShell 工具正是对这类反馈的回应，但 #8582 表明工具本身的细节仍需打磨。
- **auto-compaction 失效（#6879）是社区情绪最强烈的 bug**：19 个 👍 说明大量用户受到影响，且问题涉及 token 超额费用风险。该问题自 7 月 20 日提出后已活跃一个月，目前仍无明确修复方案。
- **llama.cpp 本地模型支持的需求已获解决**：#6922 和 #8167 均在今日关闭，配合 #8479 和 #8558 两条 PR

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-25

## 1. 今日速览

过去 24 小时 LiteLLM 项目保持高强度迭代：Issues 侧新增/活跃 58 条、关闭 31 条，PR 侧新增/活跃 151 条、合并/关闭 86 条，社区讨论重点集中在**稳定性提升**（官方冲刺路线图 #30484 获 26 条评论）、**预算/用量计费准确性**（#27735）和 **MCP 工具自动执行对 agentic 客户端的破坏性问题**（#37031）。PR 侧主要火力集中在流式回退、HTTP 连接池泄漏、供应商适配器修复等稳定性硬骨头，且多个 PR 直接针对近期回归或已知 Bug，说明项目正处于以稳定性和兼容性为核心的密集修复周期。当日无新版本发布。


## 3. 项目进展

由于昨日合并/关闭的 86 个 PR 具体清单未在数据中展开，以下基于当前待合并（OPEN）状态的高价值 PR 评估项目推进方向。这些 PR 均于 2026-08-24 提交/更新，正处于审查或待合并阶段：

**稳定性/基础设施加固**
- [fix(http_handler): dispose aiohttp session when AsyncHTTPHandler is finalized without a running loop (#36670)](https://github.com/BerriAI/litellm/pull/36670) — 修复 AsyncHTTPHandler 在无事件循环环境下终结时 aiohttp 会话未释放的问题，是此前回收修复（#33428/#32003）的补完，防止连接池泄漏。
- [fix(proxy): recover Prisma after initial startup failure (#38152)](https://github.com/BerriAI/litellm/pull/38152) — 解决 Prisma 首次启动失败后代理永久断连、数据库操作无法恢复的问题，直接对应已关闭的 Issue #34236（非 root 镜像迁移失败）。
- [fix(llms): accept the context manager arguments in __exit__ and __aexit__ (#38146)](https://github.com/BerriAI/litellm/pull/38146) — 修复 `async with AsyncHTTPHandler()` 退出时抛 TypeError 且连接池泄漏的问题。

**路由与转换修复**
- [fix(router): support mid-stream fallback for anthropic_messages route type (#38153)](https://github.com/BerriAI/litellm/pull/38153) — 让 `/v1/messages` 路由在流式中途出错时触发路由器 fallback，避免客户端裸接 `overloaded_error`。
- [fix(anthropic): close abandoned streaming responses (#38082)](https://github.com/BerriAI/litellm/pull/38082) — 关闭被丢弃的 Anthropic 流，防止上游 HTTP 连接耗尽。
- [fix(responses): preserve reasoning_effort=max through Responses API conversion (#38151)](https://github.com/BerriAI/litellm/pull/38151) — 修复 `reasoning_effort="max"` 在 Responses API 转换中被丢弃的问题。
- [fix(responses): let cache-control injection reach the system prompt from instructions (#38120)](https://github.com/BerriAI/litellm/pull/38120) — 修复 Responses API 上 cache-control 自动注入失效、无法享受提示缓存折扣的问题。

**新功能集成**
- [feat(guardrails): add ConductGuard integration (#38143)](https://github.com/BerriAI/litellm/pull/38143) — 新增 ConductGuard 作为一等公民 guardrail，可在请求发往上游前执行策略检查。
- [feat(complexity_router): bound the classifier context block, not each turn in it (#38145)](https://github.com/BerriAI/litellm/pull/38145) — 优化复杂性路由器的上下文截断策略，避免正常对话被过度截断。
- [feat(spend): report prompt caching savings as total and gateway-attributed (#38134)](https://github.com/BerriAI/litellm/pull/38134) — 改进提示缓存节省的计费归因报告，区分网关贡献与供应商侧缓存。

总体来看，项目正在**系统性解决流式传输、连接生命周期、预算准确性、多提供商适配**四类问题，且修复大多带有针对性回归测试，项目健康度良好。


## 4. 社区热点

**#30484 — LiteLLM Stability Sprint Roadmap（官方）**
[链接](https://github.com/BerriAI/litellm/issues/30484)｜26 评论 ｜ 6 👍 ｜ 创建于 2026-06-15，更新于 2026-08-23

官方稳定性冲刺路线图，列出 `/v1/model/info` 响应一致性等计划修复项，并邀请社区反馈想优先修复的 Bug。该 Issue 持续获得高关注，说明社区对稳定性诉求强烈，也是观察官方优先级的重要窗口。

**#25219 — Pods 持续内存增长导致 OOM Killed（已关闭）**
[链接](https://github.com/BerriAI/litellm/issues/25219)｜14 评论 ｜ 6 👍

用户在升级到 `main-v1.82.0-stable` 镜像后频繁遭遇 OOM。该 Issue 已关闭，结合近期的连接池/会话释放修复 PR，可推断内存泄漏问题已取得进展，社区对这一类问题的敏感度很高。

**#27735 — 虚拟 key 预算超支误判（BudgetExceededError）**
[链接](https://github.com/BerriAI/litellm/issues/27735)｜11 评论

团队级虚拟 key 在 spend 低于 max_budget 时仍被拒绝请求，疑似预算缓存/计数不同步。该问题直接关联 [#37171 PR（更新 VerificationToken.spend）](https://github.com/BerriAI/litellm/pull/37171)，修复正在推进。

**#37031 — MCP 自动执行劫持代理性客户端的所有工具调用**
[链接](https://github.com/BerriAI/litellm/issues/37031)｜6 评论 ｜ 创建于 2026-08-15

配置 `require_approval: "never"` 的 MCP 工具在代理端自动执行后，会劫持 Claude Code 等 agentic 客户端自行发送的 Read/Bash/Edit 等工具，导致全部非 MCP 工具报 “Error executing tool”。这是 MCP 自动执行机制与 agentic 客户端共存时的严重设计冲突，值得优先关注。


## 5. Bug 与稳定性

以下按严重程度排列：

**严重（阻断核心功能/数据正确性）**

- **[MCP 自动执行劫持客户端工具调用（#37031）](https://github.com/BerriAI/litellm/issues/37031)** — 仍开放，暂无 fix PR。`require_approval: "never"` 的 MCP 工具会抢占代理性客户端自身的工具调用，破坏所有非 MCP 工具。影响所有使用 Claude Code/类似 agent 且配置了自动执行 MCP 的用户。
- **[虚拟 key 预算超支误判（#27735）](https://github.com/BerriAI/litellm/issues/27735)** — 仍开放，[#37171 PR](https://github.com/BerriAI/litellm/pull/37171) 正在修复，但尚未合并。spend 计数与预算检查不一致导致合法请求被 429。

**高（影响部署/特定提供商）**

- **[litellm-non_root 镜像 Prisma 迁移失败（#34236，已关闭）](https://github.com/BerriAI/litellm/issues/34236)** — 官方镜像 1.84.0 → 1.92.1 升级后，非 root 镜像因 `@prisma/engines` 不可写导致迁移失败。已有关联修复 PR [#38152](https://github.com/BerriAI/litellm/pull/38152)。
- **[bedrock_mantle /invoke 透传报 “Provider not found”（#38054）](https://github.com/BerriAI/litellm/issues/38054)** — 新增 Bug，2026-08-24 创建，暂无 fix PR。native Bedrock passthrough 对 `bedrock_mantle/` 模型不可用。

**中（功能缺损）**

- **[Bedrock rerank 忽略 return_documents（#38006）](https://github.com/BerriAI/litellm/issues/38006)** — `litellm.rerank()` 返回结果永远不带 `document.text`，即使 `return_documents=True` 是默认值。
- **[reasoning_effort=max 在 Responses API 转换中丢失（PR #38151）](https://github.com/BerriAI/litellm/pull/38151)** — `_map_reasoning_effort` 缺少 `max` 分支导致回退为 `None`，已有修复 PR。
- **[SAP 路由丢弃 cache_control 断点（PR #38150）](https://github.com/BerriAI/litellm/pull/38150)** — 提示缓存永不激活，缓存 token 计数为 0，已有修复 PR。
- **[Tencent chat 的 thinking 参数未正确透传（PR #38100）](https://github.com/BerriAI/litellm/pull/38100)** — 腾讯云 chat 调用中思考内容未走 `extra_body`，已有修复 PR。

**低（资源泄漏/清理类）**

- **[AsyncHTTPHandler 上下文管理器 TypeError 且连接池泄漏（#38146）](https://github.com/BerriAI/litellm/pull/38146)** — `__aexit__` 未接收标准参数导致退出时报错，已有修复 PR。
- **[aiohttp 会话在无事件循环终结时未释放（#36670）](https://github.com/BerriAI/litellm/pull/36670)** — 连接池泄漏隐患，已有修复 PR。
- **[Anthropic 被遗弃流未关闭（#38082）](https://github.com/BerriAI/litellm/pull/38082)** — 客户端断连后上游 HTTP 响应未释放，已有修复 PR。


## 6. 功能请求与路线图信号

- **[#30484 稳定性冲刺路线图（官方）](https://github.com/BerriAI/litellm/issues/30484)** — 官方明确将稳定性视为一等公民，社区可在此 Issue 下反馈优先修复项，是观察短期路线图的最佳入口。
- **[#31606 分时/峰谷定价支持](https://github.com/BerriAI/litellm/issues/31606)**（4 评论 ｜ 7 👍）— DeepSeek 等厂商按时间段区分价格，用户希望模型成本计算支持 peak/off-peak 不同费率。有实际付费诉求，可能纳入后续模型成本管理迭代。
- **[#28607 Anthropic Workload Identity Federation 支持](https://github.com/BerriAI/litellm/issues/28607)**（4 评论 ｜ 3 👍）— 企业用户希望支持 OIDC JWT-bearer token exchange 替代静态 API key，属于企业级认证能力。
- **[#35272 健康感知的多后端路由（Anthropic 模型）](https://github.com/BerriAI/litellm/issues/35272)** — 多后端（直连/Bedrock/Vertex）场景下缺少自动故障转移机制，与 #38153 的流式 fallback 修复方向一致，未来可能扩展为更通用的健康路由。
- **[PR #38143 ConductGuard guardrail 集成](https://github.com/BerriAI/litellm/pull/38143)** — 新增策略检查 guardrail，表明安全/合规方向仍在持续投入。
- **[PR #38134 提示缓存节省归因报告](https://github.com/BerriAI/litellm/pull/38134)** — 改进计费可观测性，区分网关侧与供应商侧缓存贡献，回应了用户对成本透明化的诉求。


## 7. 用户反馈摘要

- **对稳定性问题高度敏感**：#25219（OOM）和 #34236（Prisma 迁移失败）均获得较多评论，且都发生在镜像升级后，用户对“升级引入回归”的不满和警惕明显。这两起问题一关一修，社区对修复速度有期待。
- **预算/计费准确性是核心痛点**：#27735 中用户明确描述“管理 API 显示 spend 低于预算但请求被拒绝”的矛盾现象，且与 #27639 疑似同源。成本类问题直接关系用户信任，需尽快合并 #37171 修复。
- **MCP 自动执行的设计冲突引发新担忧**：#37031 暴露了代理

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-25

数据来源: github.com/temporalio/temporal | 数据窗口: 2026-08-24 ~ 2026-08-25

---

## 1. 今日速览

过去 24 小时 Temporal 核心仓库整体活跃度处于**中高水平**。Issue 侧表现平静（仅 1 条新开），但 PR 侧非常活跃，共 59 条更新，其中 18 条已合并/关闭（合并/关闭率约 31%）。当前开发主线集中在 **Worker Callbacks 特性栈**（多 PR 堆叠合并到 `feature/worker-callbacks`）、**Nexus 可观测性与稳定性加固**、**CHASM 调度器 V2 迁移落地**三大方向。没有新版本发布，但社区对 PostgreSQL 分页/游标性能优化提出了具体诉求（#11743），值得后续关注。

---

## 2. 版本发布

**无新版本发布**（latest release 无更新）。

---

## 3. 项目进展

今日合并/关闭的重要 PR **共 18 条**（占比 30%+），重点推进了以下方向：

| 方向 | 关键 PR | 状态 | 说明 |
|---|---|---|---|
| **架构重构** | [#11697 Move CHASM Link and Callback validators into common](https://github.com/temporalio/temporal/pull/11697) | ✅ 已关闭/合并 | 将 `activity.linkValidator` 和 `callback.Validator` 统一迁移至 `common/links` 与 `common/callbacks`，为 Worker Callbacks 特性栈的跨模块复用铺路，也标志着该特性从原型走向工程化。 |
| **Nexus 可观测性** | [#11757 Tag Nexus-owned loggers by component](https://github.com/temporalio/temporal/pull/11757) | 🆕 新开 | 为 Nexus 日志添加 `component=nexus-*` 标签，支持 `{component=~"nexus-.*"}` 查询，显著提升请求级联排障能力。 |
| **Nexus 稳定性** | [#11764 Enforce target namespace blob size limit on Nexus failure/cancel completions](https://github.com/temporalio/temporal/pull/11764) | 🆕 新开 | 修复完成后端未校验目标 namespace 的 `BlobSizeLimitError` 的漏洞，覆盖 HSM 和 CHASM 两条路径，属安全/资源防护类修复。 |
| **批量操作修复** | [#11725 Fix batch activity unpause visibility query scope](https://github.com/temporalio/temporal/pull/11725) | ⏳ 待合并 | 修复按类型批量恢复 activity 时覆盖调用方可见性查询的问题，属于明确的功能缺陷修复。 |
| **测试基础设施** | [#11748 Add log capture to TestLogger](https://github.com/temporalio/temporal/pull/11748) | 🆕 新开 | 引入测试日志捕获能力，为后续验证日志可观测性提供基础设施。 |

> 注：今日大量活跃 PR 属于 Worker Callbacks 特性栈（#11566、#11380、#11520、#11567、#11589、#11735 等），均标注"stacked PR set，不会直接合入 main"，需待整体特性代码完成后统一合入，**短期内不会进入主线版本**。

---

## 4. 社区热点

今日讨论热度最高的条目如下（注：展示的 PR 评论数均为 undefined/0，以下按影响力与关注度筛选）：

- **[#11743 [OPEN] Optimization: Convert remaining PostgreSQL queries to tuple cursors](https://github.com/temporalio/temporal/issues/11743)** — 唯一的新 Issue，作者 @Lakshaymiddha 提出目前仍有两条 PostgreSQL 分页查询使用基于 OR 的复合游标，阻止查询计划器利用复合索引边界，导致深分页时线性退化。社区诉求是让 PostgreSQL 也能获得与 Cassandra/MySQL 一致的游标性能。

- **[#11589 [OPEN] Support Worker-variant callbacks](https://github.com/temporalio/temporal/pull/11589)** — 作者 @chrsmith 标注 *"THIS IS IT! The actual PR that implements Worker callbacks!"*，是整个特性栈的核心实现 PR，包含 Worker 侧 Callback 变体的完整实现。虽然评论数少，但属于项目路线图上的关键节点，社区关注度高。

- **[#11566 Make supported callback kinds configurable](https://github.com/temporalio/temporal/pull/11566)** — Worker Callbacks 特性栈的入口 PR，定义可配置的回调类型集合，决定了该特性对自托管用户的开放面。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | 条目 | 状态 | 说明 |
|---|---|---|---|
| **中** | [#11764 Enforce target namespace blob size limit on Nexus failure/cancel completions](https://github.com/temporalio/temporal/pull/11764) | 🆕 有待合并 PR | **潜在资源滥用/稳定性问题**：失败/取消 completion 的 failure payload 未经目标命名空间 BlobSizeLimit 校验即可进入 History，可能导致过大消息写存储。已有修复 PR，覆盖 HSM 与 CHASM 双路径。 |
| **低** | [#11725 Fix batch activity unpause visibility query scope](https://github.com/temporalio/temporal/pull/11725) | 🆕 有待合并 PR | **功能缺陷**：批量恢复 activity 时，服务端用 activity-type 谓词替换了调用方的可见性查询，导致按类型恢复时可能操作了非目标工作流。已有修复 PR。 |
| **低** | [#11631 Align CHASM ALLOW_ALL lifecycle with V1](https://github.com/temporalio/temporal/pull/11631) | 🆕 待合并 | **行为一致性**：CHASM 调度器在 ALLOW_ALL 重叠策略下附加 completion 回调，与 V1 行为不一致，可能导致重复执行或状态残留。 |

未发现高严重度崩溃/回归类 Bug。整体稳定性良好，当前问题集中在边界条件校验与行为一致性上。

---

## 6. 功能请求与路线图信号

- **PostgreSQL 深度分页性能优化（明确请求）**：Issue [#11743](https://github.com/temporalio/temporal/issues/11743) 请求将剩余两条 PostgreSQL 分页查询从 OR-based 复合游标迁移至 tuple cursors，直接提升深分页场景的查询效率。这条反馈有明确的实现路径（同仓库已有其他查询完成过类似迁移），**有较大概率被纳入后续版本**。目前暂无关联 PR。

- **Worker Callbacks 特性栈（代码已基本完成）**：从 #11589 "THIS IS IT!" 的措辞及整个特性栈（#11566、#11380、#11520、#11567、#11735 等）最后一公里的收尾状态来看，该特性 **可能进入下一版本**（或随 feature branch 的后续发布窗口推出）。该特性将带来新的 `commonpb.Callback` 变体并支持 Worker 侧回调，是当前路线图最清晰的新功能。

- **CHASM 调度器批量迁移（运营工具）**：PR [#11758 Add durable batch schedule migration](https://github.com/temporalio/temporal/pull/11758) 为 `tdbg` 增加持久化批量调度迁移能力，支持运维人员将全部可见性选中的 schedule 从 V1（workflow-backed）迁往 V2（CHASM-backed），并可回滚。结合 [#11462](https://github.com/temporalio/temporal/pull/11462) 的迁移资格修复，CHASM 迁移工具链正在完善，**该能力可能随 CHASM 正式 GA 一并推出**。

- **联邦/可靠性改进（持续）**：多 PR 标记 `[reliability-2026]`（#11697、#11700、#11725、#11462），表明今年有专门的可靠性改进 track，涉及日志可观测性验证、测试辅助设施、调度器迁移等。

---

## 7. 用户反馈摘要

今日社区用户反馈较少（仅 1 条新 Issue），但背后有明确的真实痛点：

- **PostgreSQL 用户的分页性能痛点**（来源：[#11743](https://github.com/temporalio/temporal/issues/11743)）：用户服务端在分页查询时，由于 OR-based 复合游标导致查询计划器无法使用复合索引边界，游标位置越深，页面加载越慢（线性退化）。这说明：
  - Temporal 的 PostgreSQL 支持在**深分页场景**下仍有性能短板，对大规模部署的自托管用户影响明显；
  - 用户社区对 **数据库后端行为一致性** 有期待——不同存储后端（Cassandra/MySQL/PostgreSQL）应有同等的访问路径性能。

---

## 8. 待处理积压

| 条目 | 类型 | 创建时间 | 最近更新 | 积压天数 | 备注 |
|---|---|---|---|---|---|
| [#10781 Richer await timeout diagnostics](https://github.com/temporalio/temporal/pull/10781) | PR (OPEN) | 2026-06-19 | 2026-08-24 | **67 天** | 增强 await 超时诊断信息，依赖 #10417。长周期未合入，可能受阻塞依赖影响。 |
| [#10934 add time skipping to chasm framework](https://github.com/temporalio/temporal/pull/10934) | PR (OPEN) | 2026-07-06 | 2026-08-24 | **50 天** | CHASM 框架时间跳跃支持，PR 1/2（后续 #11761），长期开放于 feature 分支。 |
| [#11462 fix: [Scheduler] V1->V2 migration-eligibility fix and migrated-start ID](https://github.com/temporalio/temporal/pull/11462) | PR (OPEN) | 2026-08-10 | 2026-08-24 | **15 天** | 合并了两个版本导出问题（#11134 + #11427），需单次版本号变更部署，等待排期。 |

**给维护者的提示**：
- #10781 连续一个月以上无实质进展，建议确认是否被 #10417 阻塞、是否需要 reviewer 介入。
- #10934 (CHASM time skipping) 作为 2-PR 栈的首个 PR，若该特性仍在路线图内，建议明确时间线。
- 唯一 Issue #11743 虽新开仅 1 天，但已获得 1 条评论，属于低成本高收益的优化项，建议规划进 PostgreSQL 后端优化 backlog。

---

*报告完*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*