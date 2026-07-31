# OpenClaw 生态日报 2026-08-01

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-31 22:36 UTC

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

好的，作为一名 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 Hermes Agent GitHub 数据，为您生成一份结构清晰、数据驱动的项目动态日报。

---

# Hermes Agent 项目动态日报 — 2026-08-01

## 1. 今日速览

Hermes Agent 项目今日社区活跃度极高，过去 24 小时内共有 1000 条 Issue/PR 更新，其中新开/活跃 Issue 442 条，待合并 PR 高达 417 条，显示出强劲的开发与讨论势头。昨日发布的 v0.19.1 (v2026.7.30) 补丁版本整合了自 v0.19.0 以来的 1000+ PR，为下游用户提供了稳定基线。当前社区关注焦点集中在**网关权限模型（RBAC）**、**Token 开销优化**、**会话持久记忆**以及 **macOS 桌面端更新器故障**等关键问题上。整体项目健康度良好，但 PR 积压数量较多，需关注合并效率。

## 2. 版本发布

**v2026.7.30 (v0.19.1)** 于 7 月 30 日发布。

- **更新内容**：这是一个补丁版本，主要将自 v0.19.0 以来合并的 1000+ 个 PR 集中打包为一个稳定标签，供下游消费者（Docker 镜像、托管部署、全新安装）使用。该版本本身不包含新的功能特性，旨在提供更稳定的分发基线。
- **破坏性变更**：未明确说明，但作为大型补丁汇总，建议用户查看自 v0.19.0 以来的 CHANGELOG 以确认是否存在配置文件或 API 行为变更。
- **迁移注意事项**：建议下游用户将该版本之前的非稳定构建（如通过 `main` 分支安装）升级至此标签，以确保环境一致性。

## 3. 项目进展

由于数据集中未单独列出“今日已合并/关闭的 PR”详细内容，我们无法提供具体合并 PR 的功能描述。但从今日更新的 83 条已合并/关闭 PR 及最新发布版本信息来看，项目正处于高频迭代后的稳定化阶段。

- **版本基线与后续开发**：v0.19.1 的成功发布意味着过去两周的高频 PR 合并已经过整合测试，项目主线已具备良好的稳定性。
- **今日新增 PR 聚焦点**：今日新提交的大量 PR（如 #75700 #75701 #75703 #75704 等）集中在 **WhatsApp 桥接加固**、**Copilot 路由安全**、**Windows Git 路径修复**、**Teams 流媒体体验优化**等方向，表明社区已开始在稳定基线上进行新一轮的功能迭代与稳定性修补。

## 4. 社区热点

过去 24 小时内，下述 Issue 引发了最广泛的讨论，反映了社区的核心诉求：

- **网关权限分级 (RBAC)** — **[#527](https://github.com/NousResearch/hermes-agent/issues/527)** (评论: 18, 👍: 11)
  当前门控平台采用“全有或全无”的二元授权模式，社区强烈希望引入 Owner/Admin/User/Guest 等角色，实现对命令、工具和终端访问的细粒度控制。这是今日关注度最高的功能需求，直接影响企业级用户的多租户部署。

- **Token 开销分析** — **[#4379](https://github.com/NousResearch/hermes-agent/issues/4379)** (评论: 18)
  用户通过自建监控面板发现 **73% 的 API 调用是固定开销 (约 13.9K tokens)**。这不仅是成本问题，更反映了默认系统提示词或上下文构建策略存在巨大优化空间。社区对此类数据驱动的问题反馈非常积极。

- **持久会话记忆** — **[#8457](https://github.com/NousResearch/hermes-agent/issues/8457)** (评论: 16)
  用户希望会话记忆能够在网关重启或会话结束后持久化，并支持跨会话搜索。该问题与 #27013 "Agents lose project context across session restarts" 高度相关，说明“记忆连续性”是当前用户体验的一大痛点。

- **Dashboard 粘贴功能缺陷** — **[#24860](https://github.com/NousResearch/hermes-agent/issues/24860)** (评论: 14, 👍: 5)
  这是一个影响日常使用体验的 bug：Web Dashboard 的聊天框不支持 Ctrl+V 粘贴文本和图片。该问题虽小，但因频繁触发而获得大量共鸣。

## 5. Bug 与稳定性

今日报告的 Bug 覆盖范围广泛，以下按严重程度排列：

**P1 (严重)**
- **macOS 应用内更新器长期损坏** — **[#74836](https://github.com/NousResearch/hermes-agent/issues/74836)**、**[#74531](https://github.com/NousResearch/hermes-agent/issues/74531)**、**[#74942](https://github.com/NousResearch/hermes-agent/issues/74942)**。
  这是今日最集中的 Bug 集群。**过期的 `hermes-setup` 二进制文件**、**更新器进程未完全退出导致误判**以及 **PID 误检**均会导致 macOS 桌面端更新永远失败。相关修复 PR 尚未出现，但在 PR #75706 与 #75703 中已有针对 Windows 和 CLI 更新逻辑的修复尝试，macOS 问题亟待专门处理。

- **SQLite 连接追踪逻辑缺陷** — **[#75699](https://github.com/NousResearch/hermes-agent/pull/75699)** (已有 Fix PR)
  连接在 `close()` 成功前就从注册表中移除，若 close 失败（如跨线程错误）会导致文件描述符泄漏，且后续操作判定连接已关闭。PR #75709 也针对该问题提出了修复。这两份 PR 表明该问题已引起维护者注意。

**P2 (中等)**
- **xAI 图像错误导致的会话永久损坏** — **[#69078](https://github.com/NousResearch/hermes-agent/issues/69078)**
  一次无效的 PNG 错误 (400) 会“永久性损坏”整个会话，重启网关也无法恢复，**即使后续请求是纯文本也会失败**。这是一个极其严重的会话状态管理问题，且规避了所有图像恢复机制。

- **Codex 适配器流式迭代错误** — **[#74532](https://github.com/NousResearch/hermes-agent/issues/74532)**
  部分符合 Codex 兼容性的端点会返回已完成的响应对象，而非 SSE 流，导致解析失败。

- **自定义 Provider 的 `max_output_tokens` 被静默丢弃** — **[#21498](https://github.com/NousResearch/hermes-agent/issues/21498)**
  配置在规范化时被删除，导致 API 请求发送错误的参数并使用模型默认的最小值（2048 tokens），影响长文本生成。

- **`no_agent=True` Cron 任务忽略远程终端配置** — **[#29849](https://github.com/NousResearch/hermes-agent/issues/29849)**
  脚本始终在调度器本地执行，而非遵循 `terminal.backend` 的配置（如 SSH），可能导致脚本在错误环境运行。

**P3 (较低)**
- **Dashboard 渲染问题** — [#51769](https://github.com/NousResearch/hermes-agent/issues/51769)、**Desktop 侧边栏问题** — [#67368](https://github.com/NousResearch/hermes-agent/issues/67368)、**macOS 唤醒抢焦点** — [#67001](https://github.com/NousResearch/hermes-agent/issues/67001)、**Photon 附件读取失败** — [#75673](https://github.com/NousResearch/hermes-agent/pull/75673) 等。

## 6. 功能请求与路线图信号

今日最突出的功能请求集中在 **权限与多租户** 与 **会话与记忆** 两大方向，预计将影响后续版本规划。

- **网关权限层级 (RBAC)** — **[#527](https://github.com/NousResearch/hermes-agent/issues/527)** (👍 11)
  这是当前呼声最高的新功能，可能成为 v0.20 或下一阶段的核心特性。

- **多角色自动路由** — **[#5143](https://github.com/NousResearch/hermes-agent/issues/5143)** (👍 16)
  与 #527 互补，通过 Hook 实现基于上下文的角色路由，属于高级工作流功能。

- **多后端终端** — **[#1855](https://github.com/NousResearch/hermes-agent/issues/1855)** (👍 11)
  用户希望突破单一全局远程终端的限制，能够同时连接本地及多个命名远程环境。

- **持久会话记忆** — **[#8457](https://github.com/NousResearch/hermes-agent/issues/8457)**、**[#27013](https://github.com/NousResearch/hermes-agent/issues/27013)**
  这是解决用户体验碎片化的关键，尽管实现复杂，但其相关的 PR 和讨论较活跃，未来有望落地。

- **明确的路线图信号**：
  今日 PR 列表中出现了 **Unified PID/TID UTC logging** ([#75691](https://github.com/NousResearch/hermes-agent/pull/75691)) 和 **API Server 平台的属性支持** — [#75526](https://github.com/NousResearch/hermes-agent/pull/75526)，表明项目在可观测性和平台一致性方面有持续投入。

## 7. 用户反馈摘要

- **成本敏感度极高**：用户 (Bichev) 通过 [#4379](https://github.com/NousResearch/hermes-agent/issues/4379) 指出约 73% 的 API 调用是固定开销。这直接影响了用户的续费意愿和使用频次，**优化提示词和上下文管理应作为最高优先级之一**。

- **记忆断层导致信任危机**：在 [#27013](https://github.com/NousResearch/hermes-agent/issues/27013) 中，用户反馈代理在会话重启后会“幻觉”错误的项目身份，严重干扰了实际工作流，降低了用户对 agent 长期可靠性的信任。

- **配置被“静默”篡改引发困惑**：多个问题（如 [#21498](https://github.com/NousResearch/hermes-agent/issues/21498) 自定义参数被丢弃、[#25859](https://github.com/NousResearch/hermes-agent/issues/25859) 两个超时配置键冲突、[#58546](https://github.com/NousResearch/hermes-agent/issues/58546) OAuth 凭证优先于环境变量）都指向同一个痛点：**系统在不告知用户的情况下，以不透明的方式更改了配置行为**。

- **高风险的安全边界反馈**：用户 (luizfneves404) 在 [#58546](https://github.com/NousResearch/hermes-agent/issues/58546) 中强调，自动发现的 Claude Code OAuth 凭证优先级高于显式配置的 API 密钥，可能导致**意外的身份或计费归属**，这是一个极具价值的安全反馈。

## 8. 待处理积压 (维护者关注提醒)

以下 Issue/PR 长期存在且讨论度高，但尚未看到明确的处理结论或修复 PR，建议维护者优先关注：

- **[#4379](https://github.com/NousResearch/hermes-agent/issues/4379) Token 开销分析 (4月1日创建)**：虽然讨论热烈，但尚未看到官方的性能优化专项或回应方案。建议评估是否存在短期可执行的优化项。

- **[#527](https://github.com/NousResearch/hermes-agent/issues/527) 网关权限分级 (3月6日创建)**：已获得 18 条评论和 11 个 👍，但状态仍为 `needs-decision`。该决策对社区贡献方向影响较大，建议尽快明确是否纳入路线图。

- **[#8457](https://github.com/NousResearch/hermes-agent/issues/8457) 持久会话记忆 (4月12日创建)**：该功能与多个后续 issue 和 PR 相关联，属于社区长期呼唤的“缺失拼图”，但当前仍未进入 `Accepted` 状态。

- **[#29849](https://github.com/NousResearch/hermes-agent/issues/29849) Cron 任务忽略远程后端 (5月21日创建)**：这是一个隐蔽的逻辑错误，可能导致用户在不知情的情况下于错误环境中执行脚本，风险较高，需尽快确认。

---
**数据截止时间**：2026-08-01 00:00 UTC。本报告基于公开 GitHub 数据生成，供项目健康度参考。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-08-01

## 今日速览

过去 24 小时项目保持高活跃度：共产生 39 条 Issue 更新（32 条新开/活跃，7 条关闭）和 50 条 PR 更新（47 条待合并，3 条已合并/关闭），无新版本发布。当前 Issue 池中约 70% 为标记 `needs-triage` 的 Bug 报告，安全相关讨论（凭据泄露、安全分析器信任模型、未验证 HTTP 调用）明显升温，显示社区对生产环境稳定性和安全性的关注度正在上升。合并/关闭的 3 个 PR 集中在错误分类标准化、LiteLLM Provider 抽象和发布分支命名修正，表明项目正推进内部架构重构与可观测性改进。整体健康度良好，但待合并 PR 积压（47 条）值得关注。

---

## 项目进展

今日无代码合并（merge）事件，关闭/合并的 3 个 PR 主要为架构重构与流程修正：

- **[#4316 [CLOSED] feat(sdk): classify conversation errors**](https://github.com/OpenHands/software-agent-sdk/pull/4316)
  为对话与 Agent 错误事件引入向后兼容的结构化分类（运行限制、Provider 结果、未知异常），使 SDK 消费者无需解析错误详情即可获得可操作的错误信息。这是提升 SDK 可观测性的重要一步。

- **[#2363 [CLOSED] refactor(llm): add LiteLLM-backed provider abstraction**](https://github.com/OpenHands/software-agent-sdk/pull/2363)
  将混合的 “provider/model” 字符串抽象为独立的 Provider 层，历时近 5 个月后关闭。该重构为后续多 Provider 差异化配置与认证管理奠定基础。

- **[#4073 [CLOSED] Use the right branch name in release branches**](https://github.com/OpenHands/software-agent-sdk/pull/4073)
  修正发布分支命名规范为 `rel-*/`，与现有模式对齐，属于发布流程的工程化收尾。

**整体评估**：今日虽是架构与流程的重构日而非功能推进日，但错误分类标准化 + Provider 抽象落地意味着 SDK 正在为了更稳定的多 LLM 支持和可诊断性“打地基”。

---

## 社区热点

### 🔥 讨论热度最高

- **[#3540 [CLOSED] feat: OpenAI-compatible /v1/chat/completions gateway for the agent-server](https://github.com/OpenHands/software-agent-sdk/issues/3540)** — 24 条评论
  由 @smolpaws（代理）代 @enyst 发布的提案：为 agent-server 增加 OpenAI 兼容的 `/v1/chat/completions` 端点，让任何支持 OpenAI 协议的客户端都能直接驱动 OpenHands Agent。该提案已被标记 Stale 并关闭，但评论数稳居第一，说明社区对“标准协议接入”有强烈意愿，未来可能以其他形式重启。

- **[#4019 [OPEN] ACP profiles inject workspace project skills that duplicate what the ACP CLI already ingests (AGENTS.md)](https://github.com/OpenHands/software-agent-sdk/issues/4019)** — 14 条评论
  围绕 PR #4018 引入的回归展开：ACP 配置文件总是以 `load_project_skills=True` 构造 AgentContext，导致工作区项目技能与 ACP CLI 自身注入的 skills 重复。讨论反映了 ACP 集成路径中职责边界不清的问题。

### 📈 高共鸣 Issue（10+ 评论）

| Issue | 标题 | 评论数 | 状态 |
|-------|------|--------|------|
| [#4248](https://github.com/OpenHands/software-agent-sdk/issues/4248) | Missing required parameters for 'execute_bash': {'security_risk'} | 12 | OPEN |
| [#3992](https://github.com/OpenHands/software-agent-sdk/issues/3992) | Asymmetric handling of content-without-tool-call responses | 11 | OPEN |
| [#4063](https://github.com/OpenHands/software-agent-sdk/issues/4063) | max_concurrent_runs does not limit native async conversations | 11 | OPEN |
| [#4080](https://github.com/OpenHands/software-agent-sdk/issues/4080) | One unregistered event kind fails the entire conversation load | 10 | OPEN |
| [#3005](https://github.com/OpenHands/software-agent-sdk/issues/3005) | All verified models are also OpenHands verified models | 10 | OPEN |

**共性诉求**：高热度问题集中在三类——(1) 本地/弱模型兼容性不足（#4248、#3992）；(2) 并发与异步行为不符合文档预期（#4063）；(3) 单点故障导致整体功能失效（#4080）。这些指向用户对 SDK 在非理想环境下的鲁棒性要求。

---

## Bug 与稳定性

> **严重程度**：🔴 严重（阻断/安全）| 🟠 中等（功能失效）| 🟡 轻微（体验/边界）

### 🔴 安全相关

- **[#4271 [OPEN] GitHub credentials in git remote URLs are not redacted from terminal output](https://github.com/OpenHands/software-agent-sdk/issues/4271)**（5 评论）
  OpenHands Cloud 用户的 GitHub 凭据经 git remote URL 暴露在终端输出中。凭据泄露属高危，**暂无 fix PR**，需尽快处理。

- **[#4157 [OPEN] LLMSecurityAnalyzer trusts model self-assessed risk level](https://github.com/OpenHands/software-agent-sdk/issues/4157)**（5 评论）
  当 `security_analyzer: llm` + `confirmation_mode: true` 时，任何被 LLM 自评为 LOW 的操作都自动执行，无需人工确认。等于让模型自己给自己放行，风险极高。**暂无 fix PR**。

- **[#4263 [OPEN] get_litellm_model_info makes unvalidated httpx.get call at LLM init](https://github.com/OpenHands/software-agent-sdk/issues/4263)**（3 评论）
  Fork 审计发现：`model_info.py:31` 在 LLM 初始化时发起未经验证的 `httpx.get` 请求，可能造成策略绕过（egress hole）。**暂无 fix PR**。

- **[#4098 [OPEN] Avoid unauthenticated model-info lookup for managed OpenHands models](https://github.com/OpenHands/software-agent-sdk/issues/4098)**（9 评论）
  即使无 API key，`openhands/*` 模型的 LLM 初始化仍会同步请求外部 `/v1/model/info` 接口，造成不必要的外部依赖调用。**暂无 fix PR**。

### 🟠 功能阻断

- **[#4248 [OPEN] execute_bash 缺少必填参数 security_risk](https://github.com/OpenHands/software-agent-sdk/issues/4248)**（12 评论）
  使用 deepseek-reasoner 时，`execute_bash` 报缺少 `security_risk` 参数，Agent 直接崩溃。由 #4157 安全设计引入，影响特定模型的工具调用链。**暂无 fix PR**。

- **[#4063 [OPEN] max_concurrent_runs 不限制原生异步会话](https://github.com/OpenHands/software-agent-sdk/issues/4063)**（11 评论）
  文档声明该配置用于限制并发 Agent 步数，但实际仅作用于同步 `ThreadPoolExecutor`；`EventService.run()` 绕过限制，可能导致资源耗尽。**暂无 fix PR**。

- **[#4080 [OPEN] 单个未注册事件类型导致整个对话加载失败](https://github.com/OpenHands/software-agent-sdk/issues/4080)**（10 评论）
  一个事件反序列化失败（如自定义 `observation.kind`），整个会话 404，且从服务器列表静默消失。应降级为单事件跳过而非整体失败。**暂无 fix PR**。

- **[#4245 [OPEN] Webhook 连接失败导致容器崩溃](https://github.com/OpenHands/software-agent-sdk/issues/4245)**（9 评论，创建于 1 月）
  agent-server 容器无法连接 webhook 端点时引发级联崩溃和 Sandbox 连接错误。已有 [#4323 Webhook 投递内存 bound](https://github.com/OpenHands/software-agent-sdk/pull/4323) 和 [#4136 状态更新发布 bound](https://github.com/OpenHands/software-agent-sdk/pull/4136) 两 PR 在途，但尚未合入。

- **[#4246 [OPEN] MCP 工具初始化超时导致 Agent 无响应](https://github.com/OpenHands/software-agent-sdk/issues/4246)**（9 评论）
  超时错误后 Agent 保持空闲，UI 无任何视觉反馈。**暂无 fix PR**。

### 🟡 体验/兼容性

- **Ollama 5 分钟超时**（[#4255](https://github.com/OpenHands/software-agent-sdk/issues/4255)，7 评论）：UI 和 settings.json 均无法覆盖默认 300 秒超时。
- **ACP 0.11 移除 Gemini 模型状态字段**（[#4093](https://github.com/OpenHands/software-agent-sdk/issues/4093)，9 评论）：`agent-client-protocol` 无上限约束，0.11.0 导致 Pydantic 校验失败。
- **Chromium 缺 `--no-sandbox`**（[#4256](https://github.com/OpenHands/software-agent-sdk/issues/4256)，6 评论）：agent-server Docker 镜像内 browser-use 启动失败。
- **Global Skills 不加载**（[#4252](https://github.com/OpenHands/software-agent-sdk/issues/4252)，6 评论）：CLI 安装后新增 Global Skills 无法注入。
- **ACP switch_profile 半应用**（[#4158](https://github.com/OpenHands/software-agent-sdk/issues/4158)，4 评论）：状态文件更新但 live session 仍用旧 agent。
- **Web 浏览器功能不稳定**（[#4253](https://github.com/OpenHands/software-agent-sdk/issues/4253)，4 评论）：

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-01

## 1. 今日速览

LiteLLM 近期保持极高的社区活跃度和迭代速率：过去 24 小时内有 **248 条 PR 更新**（其中 69 条已合并/关闭）和 **56 条 Issue 更新**（其中 15 条已关闭），项目吞吐和问题解决效率处于健康水平。当前的开发重点明显向**成本核算与计费可视化（PTU/自动路由节省）**倾斜，同时伴随着对 Azure AI 认证、Claude Code 集成以及 Responses API 桥接层的密集修复。今日发布了 3 个 Pre-release 版本（v1.95.0-rc.2 与 v1.96.0-dev.x），但均以 Docker 签名维护为主，无破坏性变更提示。

---

## 2. 版本发布

今日发布 3 个版本，均为预发布/开发版：

- **v1.96.0-dev.2** [查看](https://github.com/BerriAI/litellm/releases)
- **v1.95.0-rc.2** [查看](https://github.com/BerriAI/litellm/releases)
- **v1.96.0-dev.1** [查看](https://github.com/BerriAI/litellm/releases)

**更新内容与备注**：三个版本的 Release Notes 均仅强调所有 LiteLLM Docker 镜像已使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 进行签名，且所有版本均使用同一密钥（见 [commit `0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0)）。**未提及任何面向用户的功能变更、破坏性变更或迁移注意事项**，推测是针对 `main` 分支的同步或 CI 构建验证。

---

## 3. 项目进展

今日合并/关闭的 PR 主要集中于 UI 修复与依赖维护，而多个高价值功能 PR 仍在开放中，表明项目正在跨越关键里程碑：

- **UI 体验修复（已合并）**：
  - `#32134` [fix(ui): search request logs by request_id server-side](https://github.com/BerriAI/litellm/pull/32134)：修复请求日志搜索仅限客户端过滤的问题，改为服务端按 `request_id` 查询。
  - `#35322` [fix(ui): nest source object in Claude Code marketplace settings snippet](https://github.com/BerriAI/litellm/pull/35322)：修复 Claude Code 技能设置中

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-01

## 今日速览

过去 24 小时项目整体活跃度 **较高**：PR 更新达 63 条（其中 40 条待合并、23 条已合并/关闭），表明核心开发迭代节奏快；Issue 侧相对平静，仅 3 条新开/活跃，无新增闭合问题。无新版本发布。从 PR 内容看，**Standalone Activity（SAA）** 与 **CHASM 调度器** 是两个明显的高频开发方向，此外 S3 可见性查询、Nexus 操作支持等亦有多项推进。社区侧，关于 **DST（夏令时）调度处理** 的讨论热度最高，但整体反馈量有限。

---

## 项目进展

今日合并/关闭的 PR 主要集中在以下三个方面，标志项目在稳定性与功能完整性上又前进了一步：

- **[PR #11377] WCP 7/X: Change failure cause and expose workflow task completion size limit**（已关闭）
  - 当工作流任务完成缓冲区溢出时，失败原因由 `PAYLOADS_TOO_LARGE` 改为 `WORKFLOW_TASK_FAILED_CAUSE_REQUEST_TOO_LARGE`；同时 `DescribeNamespace` 新增 `workflow_task_completion_size_limit_error` 字段。属于可观测性与错误语义的收尾改进。
  - https://github.com/temporalio/temporal/pull/11377

- **[PR #11271] scheduler: treat non-positive catchup window as unset (CHASM)**（已关闭）
  - CHASM V2 调度器中，非正 catchup window 现在按“未设置”处理并返回默认值，而不是钳制到最小值。修复了边界行为，并为后续 `DescribeSchedule` 的改进打好基础。
  - https://github.com/temporalio/temporal/pull/11271

- **[PR #11325] Bug fix: SAA: chain the underlying failure cause on terminal timeouts**（已关闭）
  - SAA 终态超时失败现在会链式保留前序 attempt 的原始失败原因，避免 SDK 用户只能看到超时错误而丢失业务异常细节。这是对 SAA 可观测性的实质修复。
  - https://github.com/temporalio/temporal/pull/11325

此外，以下开放 PR 虽尚未合并，但已进入评审或接近完成，值得关注：

- **[PR #11378] Enable standalone activity start delay by default** —— 拟将 SAA 独立 Activity 的启动延迟能力默认开启，推进 SAA 功能 GA。
- **[PR #11383] Accept WorkflowType in S3 visibility queries** —— 让 S3 可见性归档查询支持 `WorkflowType` 字段，并保留 `WorkflowTypeName` 为兼容别名。
- **[PR #11382] Scheduler (CHASM): resolve catchup window in describe** —— 完善 `DescribeSchedule` 对 catchup window 的展示语义。

---

## 社区热点

- **[Issue #8205] Improve DST handling in schedules**（5 条评论，4 👍）
  - 是过去 24 小时讨论量最高、反应最多的问题。该 Issue 早在 2025-08-18 提出，用户引用官方文档说明：当 Cron 配置为本地时间戳时，跨 DST 切换日可能执行 0 次、1 次或多次。该问题涉及许多用户的真实业务场景，至今未闭环。
  - https://github.com/temporalio/temporal/issues/8205

该问题的长期讨论热度反映了 **Temporal Cron 调度在真实世界时区场景下的行为不确定性** 是用户普遍关注的痛点，社区希望得到更清晰、可预期的语义（例如跳过或补偿执行策略）。

---

## Bug 与稳定性

按影响面与严重程度排序：

1. **Nexus reapply 无法区分“CHASM 拥有该操作”与“无树拥有该操作”**
   - 状态：OPEN，已有修复 PR [#11381]
   - 该问题是 Reset/复制事件重放中的正确性缺陷：HSM 状态机未找到操作时，现在会回退到 CHASM 树，导致不可预期，且与 #10986 之前的路径有回归关系。这属于数据面正确性问题，修复（[PR #11381]）已将 `ErrStateMachineNotFound` 重新视为可跳过，等待评审合并。
   - https://github.com/temporalio/temporal/issues/11384
   - https://github.com/temporalio/temporal/pull/11381

2. **Workflow List 在热存储与归档存储查询方式不一致**
   - 状态：OPEN，暂无关联 fix PR
   - 用户 `temporal workflow list -q 'WorkflowType = "..."'` 在热工作流上有效，但增加 `--archived` 后预期同样方式，显然行为不一致。这是一个命令语义一致性问题，影响日常运维体验。
   - https://github.com/temporalio/temporal/issues/7821

3. **SAA：pending reset 期间允许 update/unpause 等操作（潜在状态错误）**
   - 状态：OPEN，已有修复 PR [#11360] 和 [#11358]
   - 修复方向为：reset 挂起拒绝更新选项、非暂停状态拒绝 unpause 等，防止无效状态转换被记录。
   - https://github.com/temporalio/temporal/pull/11360
   - https://github.com/temporalio/temporal/pull/11358

---

## 功能请求与路线图信号

- **[Issue #8205] 改进调度的 DST 处理**（功能增强）
  - 虽然 Issue 已持续近一年，但至今仍有用户关注。随着未来调度语义迭代，这一问题可能会进入正式路线图。相关讨论可视为路线图信号。
  - https://github.com/temporalio/temporal/issues/8205

- **[PR #11378] Standalone Activity 启动延迟默认开启**
  - 方向很明确：SAA 的 `start delay` 能力将随此变更进入 GA 默认启用。这是 SAA 功能走向成熟的重要信号。
  - https://github.com/temporalio/temporal/pull/11378

- **[PR #11383] S3 可见性查询支持 WorkflowType**
  - 持续补齐归档可见性查询能力，保持与热存储查询的字段一致性。
  - https://github.com/temporalio/temporal/pull/11383

- **[PR #11274] 支持 Query-backed Nexus Operations**
  - 旨在将 Workflow Query 作为 Nexus 操作对外暴露，是“所有 Temporal 原语均可作为 Nexus 操作”路线的一部分。
  - https://github.com/temporalio/temporal/pull/11274

---

## 用户反馈摘要

- **对于 #7821**：用户 kkcmadhu-IBM 期望能以统一的查询语句同时访问热工作流与归档工作流。当前需要为归档单独调整查询方式，使用体验割裂。这代表用户对一致操作接口的明确期待。
  - https://github.com/temporalio/temporal/issues/7821

- **对于 #8205**：用户从 Slack 转来疑问——当 Cron 配置为本地时间且跨 DST 切换时，执行次数存在不确定性。这说明用户不仅关心“什么时候跑”，还关心“为什么没跑”。他们希望文档给出的行为描述能转变为实际系统中可预测、可控的语义。
  - https://github.com/temporalio/temporal/issues/8205

---

## 待处理积压

以下 Issue 长期开放且仍未得到解决，提醒维护者关注：

- **[Issue #7821] Workflow list 热/归档查询不一致**
  - 创建于 2025-05-28，已开放超过一年，仅 2 条评论。问题明确但关注度低，容易持续被埋没。
  - https://github.com/temporalio/temporal/issues/7821

- **[Issue #8205] 改进调度的 DST 处理**
  - 创建于 2025-08-18，已开放近一年，5 条评论 4 个 👍。长时间未解决，属于社区呼声较高但实施复杂度可能较高的改进。
  - https://github.com/temporalio/temporal/issues/8205

---

*本日报由 AI 基于 GitHub 数据自动生成，仅供参考。*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*