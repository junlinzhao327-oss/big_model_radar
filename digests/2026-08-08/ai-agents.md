# OpenClaw 生态日报 2026-08-08

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-07 22:59 UTC

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

# Hermes Agent 项目动态日报 — 2026-08-08

## 1. 今日速览

过去24小时内，Hermes Agent 项目保持极高的社区活跃度：**352条 Issue 更新**（新开/活跃301条，关闭51条）、**500条 PR 更新**（待合并358条，合并/关闭142条），日均吞吐量处于本项目历史高位。无新版本发布，项目处于密集开发迭代期。社区讨论集中在三大主题：**“god-file分解”架构治理史诗**（#78647，59条评论）、**插件接口扩展**（#64182，29条评论）与**桌面端稳定性问题**（#63047、#79407等）。从数据看，桌面端（Desktop）质量问题占据大量 Issue/PR，是当前反馈最集中、修复最活跃的区域；同时多个 P1 级核心 Agent 稳定性 Bug 仍在推进中，项目健康度整体良好但存在明显的“质量债”压力。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日有 **142 条 PR 合并/关闭**（数据源未逐条列出），从可见的关闭记录与代码状态看，项目在以下方向有实质推进：

- **会话路由 Bug 修复已合入主分支**：[#68358](https://github.com/NousResearch/hermes-agent/issues/68358)（桌面端新会话消息被路由到旧 TUI 会话）已关闭，标记 `sweeper:implemented-on-main`，修复已随主分支发布。
- **Matrix 定时任务投递失败修复**：[#61495](https://github.com/NousResearch/hermes-agent/issues/61495)（“Timeout context manager should be used inside a task”）已关闭，解决了 Matrix 网关手动 cron 投递时的异步上下文错误。
- **Gateway 澄清死锁修复**：[#71997](https://github.com/NousResearch/hermes-agent/pull/71997)（`fix(gateway): release rejected native clarifies before steering`）已关闭，修复了 #71946 中严格选项校验导致的原生选择澄清死锁，同时避免将非匹配文本当作选项。
- **安全审计清理推进中**：[#79618](https://github.com/NousResearch/hermes-agent/pull/79618)（`fix(sec): clear uv audit findings`）旨在修复 `uv audit` 报告的 13 项安全公告，并封堵 `tools/lazy_deps.py` 与 `pyproject.toml` 重复依赖导致的回归路径，尚未合并。
- **桌面端自包含安装器**：[#79599](https://github.com/NousResearch/hermes-agent/pull/79599) 将桌面应用构建为单文件自包含安装器（内置 agent 源码、uv、CPython、wheelhouse 等），首次启动不再需要下载和 npm 构建，处于待合并状态。
- **Agent 流式传输稳定性修复**：[#80122](https://github.com/NousResearch/hermes-agent/pull/80122)（`fix(agent): handle auxiliary stream stalls and prevent turn ghosting`）修复 #78981 “Permanent Session Death”，定位到辅助流进度上报与压缩调用点的三个相互交织的缺陷，尚未合并。

## 4. 社区热点

| 议题 | 评论数 | 热度分析 |
|---|---|---|
| [#78647](https://github.com/NousResearch/hermes-agent/issues/78647) Epic: Shard all 20 god files — repo-wide god-file decomposition | 59 | 社区对**架构治理**有极强共识：将

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

好的，作为一名专注开源项目分析的技术编辑，我将根据您提供的 GitHub 数据，为您生成了 2026 年 8 月 8 日的 OpenHands SDK 项目动态日报。

---

# OpenHands SDK 项目动态日报 | 2026-08-08

## 1. 今日速览

今日 OpenHands SDK 项目活跃度**高**，核心维护者与社区贡献者双轨并行。过去 24 小时内，Issue 和 PR 更新总量达 42 条，其中有 16 个 PR 正在等待合并，表明项目正处于**密集开发与合并周期**。值得关注的是，今日工作重心明显向 **ACP (Agent Client Protocol) 稳定性**、**Windows 平台支持**以及**安全/凭证治理**倾斜，多项高优先级修复与重构已经落地或进入最后审查阶段。虽然今日无新版本发布，但根据 Issue #3691 的追踪信息，包含重大 SDK 变更的 **v1.29.0** 预计将在近期发布，项目整体处于迈向下一里程碑的冲刺期。

## 2. 版本发布

**无**

*注意：尽管今日无新 Release，但 Issue #3691 提及当前最新 tag 为 `v1.28.1`，且一个关键的 `feat`（开启 Agent Canvas 从 ACPAgent 源码服务的支持）已合并至 `main`，预计作为 **v1.29.0** 发布。*

## 3. 项目进展

今日有 7 个 PR 被合并或关闭，主要推进了以下关键领域：

- **ACP 可靠性与可观测性（核心维护者推动）**：
    - **[#4415] fix(observability): record non-executed tool results**：修复了 Laminar 数据完整性问题。现在当工具校验失败或被识别为未知工具时，系统会立即记录一个包含原始 `tool_call_id` 的 TOOL 结果 span，解决了此前验证失败和未知工具调用在追踪数据中“凭空消失”的问题。这显著提升了调试复杂 Agent 工作流的可观测性。
    - **[#4404] fix(sdk): make ACP auth failures self-diagnosing**：改善了 Codex ACP 认证失败时的错误日志，使其能够更清晰地指示问题根源，减少用户在配置 ACP 时的困惑。
    - **[#4403] fix(acp): recover credential monitor after transient errors**：修复了 Codex 凭证监视器在遇到瞬时 `CredentialSyncError` 后永久停止的问题，增强了 ACP 凭证同步的韧性。
- **开发者体验与配置管理**：
    - **[#4327] feat(hooks): discover hooks.json in .agents/ as well as .openhands/**：项目级配置文件现在统一支持 `.agents/` 目录（如 Skills、Plugins 等），Hooks 配置不再局限于 `.openhands/`，使项目配置更加一致和直观。
- **运行时增强**：
    - **[#4414] feat: derive automation conversation tags in base RemoteWorkspace**：为远程工作空间的基础逻辑添加了自动化对话标签的派生能力，为后续的自动化运维和分类管理打基础。
    - **[#4127] feat(browser): record visible sessions as WebM**：为浏览器会话增加了 WebM 格式的屏幕录制能力，这对于改进 E2E 测试体验和用户操作回溯非常有价值。

## 4. 社区热点

今日讨论焦点呈现“**安全/凭证治理**”与“**插件系统演进**”双峰格局：

- **Issue [#1440] Plugin 1.0 Definition (评论: 25)**：这是目前项目内讨论度最高的话题。该 Issue 旨在定义 SDK 插件（Plugin）的基本规范，并明确将 MCP 配置和运行时配置的整合排除在初始范围之外。围绕“插件是 SDK 概念还是 OpenHands 概念”的核心问题，社区展开了长线深入讨论。这反映了社区对**标准化、可移植的插件体系**的强烈渴望。
    - 链接: https://github.com/OpenHands/software-agent-sdk/issues/1440
- **安全/凭证泄露问题群组（评论数合计约 20+）**：围绕 GitHub 凭证在终端输出中泄露 ([#4271])、Codex 凭证在 ACP 会话间/并发下的同步问题 ([#4170], [#4171], [#4177])，社区与维护者进行了密集互动。这些问题被拆分为多阶段（Phase 1/2）处理，并涉及Agent Canvas、OpenHands SaaS 等多种拓扑，显示出这些问题在真实的生产环境中具有广泛影响。
    - 链接: https://github.com/OpenHands/software-agent-sdk/issues/4271
    - 链接: https://github.com/OpenHands/software-agent-sdk/issues/4170
- **新标准引入讨论 (评论: 1)**：**[Issue #4405]** 提出支持 [agent-plugins.org](http://agent-plugins.org) 的便携式插件包格式，这是 Amazon、Cursor、Microsoft 等巨头支持的新兴开放标准。虽然刚提出，但迅速获得了维护者的关注 (Needs Design 标签)，并已有一个配套的重构 PR [#4420] 提交，预示着该提案可能被快速采纳。

## 5. Bug 与稳定性

今日报告和修复的 Bug 主要集中在**安全**、**性能**和**平台兼容性**方面，按严重程度排列如下：

- **严重（高优先级，导致服务不可用）**：
    - **[Issue #4416] agent-server: periodic multi-second GC pauses ... cause total request stall ('wedge')** (priority: high)：一个导致所有请求停滞数秒的严重性能问题。`GET /api/conversations/search` 接口在事件循环线程上执行了沉重的并发安全 GC 停顿，造成服务“卡死”。
        - **已有修复 PR**: [#4417] fix(agent-server): compose ConversationInfo off the event loop to avoid GC wedge。通过将重负载 Pydantic 模型组装操作移出事件循环来规避此问题。
        - 链接: https://github.com/OpenHands/software-agent-sdk/issues/4416
- **高（安全问题，需紧急关注）**：
    - **[Issue #4271] GitHub credentials in git remote URLs are not redacted from terminal output**：用户的 GitHub 凭证（token）通过 `git remote` URL 被明文打印在终端中，存在敏感信息泄露风险。
        - **已有修复 PR**: [#4175] fix(security): redact git remote URL credentials in terminal output，目前仍在开放状态等待审查。
        - 链接: https://github.com/OpenHands/software-agent-sdk/issues/4271
    - **[Issue #4190] SecretRegistry fails to mask registered secrets in terminal output unless the command referenced the secret name**：这是一个更隐蔽的 API 密钥泄露漏洞。当命令输出中包含密钥值但未提及密钥名时，SecretRegistry 不会对其进行脱敏处理。
        - 链接: https://github.com/OpenHands/software-agent-sdk/issues/4190
    - **[Issue #4411] LLM auth-error text (with partial API key) persisted verbatim into ConversationErrorEvent**：将 LLM 的认证错误信息（其中包含部分 API key）完整存入事件流，造成了额外的密钥片段泄露。
        - 链接: https://github.com/OpenHands/software-agent-sdk/issues/4411
- **中（功能缺陷）**：
    - **[PR #4406] fix(tools): shim mcp 1.x Server decorators so browser_use constructs under mcp 2.x**：在 mcp 2.x 环境下，browser 工具无法构建（`AttributeError`），该 PR 提供了一个兼容垫片来解决此问题。
        - 链接: https://github.com/OpenHands/software-agent-sdk/pull/4406
- **低（稳定性/兼容性）**：
    - **[Issue #3746] max_input_tokens in agent_settings.json does not take effect in headless CLI mode**：`max_input_tokens` 设置在无头 CLI 模式下不生效，导致配置无效。
        - 链接: https://github.com/OpenHands/software-agent-sdk/issues/3746

## 6. 功能请求与路线图信号

结合今日的 Issue 和 PR，以下功能信号值得关注，并可能被纳入下一版本（如 v1.29.0 或后续版本）：

- **插件系统 2.0（信号极强）**：
    - **[Issue #1440] Plugin 1.0 Definition** 仍在演进中。
    - **[Issue #4405] 支持 agent-plugins.org 标准**：社区希望拥抱开放的插件包标准。
    - **配套 PR [#4420] refactor(plugin): extract PluginFormat strategy**：该重构将代码基础准备好，以便支持多种插件格式。这些迹象表明，一个功能更强大的插件系统正在积极设计中。
- **Pi 作为 ACP Provider（信号强）**：
    - **[PR #4419] feat(sdk): register Pi as a built-in ACP provider**：SDK 希望将 Pi 作为一等公民 ACP 提供者，并在 Docker 镜像中预装 `pi-acp`，以丰富用户可选的 ACP 后端。
- **LLM 动态请求级元数据（信号中）**：
    - **[Issue #4421] feat(llm): resolve provider-specific runtime metadata for routed models**：针对 OpenRouter 等路由提供商，需要实现动态的上下文窗口/限额检测，以取代静态的模型元数据。
- **运行时可靠性增强（信号中）**：
    - **[PR #4402] feat(mcp): refresh tools for active conversations**：允许在不重启会话的情况下，为进行中的对话刷新 MCP 工具列表，避免因后端更新导致的功能不一致。

## 7. 用户反馈摘要

从今日的 Issue 和 PR 中，可以提炼出以下真实的用户声音：

- **真实痛点：Windows 平台支持仍待完善**：社区用户 @Telov 提交了 3 个 PR（[#4410] acp_command 存储方式、[#4408] Windows PATH 查找机制、[#4409] 子进程树回收），目标都是修复在 Windows 上安装和使用 OpenHands 遇到的障碍。这印证了 **Windows 平台的体验是当前社区用户的一大痛点**，也体现了社区的积极自救和共建。
- **真实痛点：配置项不生效导致挫败感**：用户 @xiaolei373 在 Issue #3746 中报告了 `max_input_tokens` 配置在 CLI 模式下被忽略的问题，这直接影响了用户对模型输入长度的控制，可能导致任务因截断而失败。
- **真实痛点：晦涩难懂的环境配置错误**：用户 @santosh-kulkarni-25 在 Issue #4407 中报告了一个与 OpenHands 无关的 WordPress 主题错误，这属于无效报告。但这类“误报”也侧面反映出**用户对项目的环境依赖和配置门槛存在困惑**，尤其是对于非 Python 技术栈的用户。
- **来自 PR 的声音：贡献者表达清晰**：从 PR #4406 的 HUMAN 备注 "We run the SDK in an environment where mcp 2.x is installed; there the browser tool cannot be constructed at all..." 可以看出，下游开发者对依赖冲突的困扰，并愿意将手动补丁上游化，体现了社区对项目健康度的贡献意愿。

## 8. 待处理积压

以下是对项目发展有潜在影响的长期未决或关键事项，建议维护者重点关注：

- **[Issue #1440] Plugin 1.0 Definition** (评论: 25)：项目的“基石性”议题，讨论周期长（自 2025 年 12 月）。虽然讨论富有成效，但亟需收敛为具体的设计文档和实施计划，以推动插件系统的落地。
    - 链接: https://github.com/OpenHands/software-agent-sdk/issues/1440
- **[Issue #3746] max_input_tokens 在 CLI 模式无效** (更新于 2026-06-16)：已被报告近两个月，仍处于开放状态，无对应修复 PR。对于 CLI 重度用户而言，这是一个关键配置，长期未修复会消耗用户信任。
    - 链接: https://github.com/OpenHands/software-agent-sdk/issues/3746
- **[PR #4420] refactor(plugin): extract PluginFormat strategy (prep for Agent Plugins support)**：这是支撑 [agent-plugins.org](http://agent-plugins.org) 标准的基础重构，虽然刚刚提交，但其审查和合并进度会直接影响后续插件生态的功能开发。
    - 链接: https://github.com/OpenHands/software-agent-sdk/pull/4420
- **[PR #4175] fix(security): redact git remote URL credentials in terminal output**：这是一个直接修复敏感凭证泄露的安全补丁，已开放超过半月，需要优先推动合并。
    - 链接: https://github.com/OpenHands/software-agent-sdk/pull/4175

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-08

## 1. 今日速览

过去24小时 Pi 项目保持高度活跃：Issues 更新 62 条（其中 53 条已关闭，关闭率 85%），PR 更新 26 条（17 条已合并/关闭），并发布了 v0.84.1 新版本。社区讨论焦点集中在 Windows 使用体验、上下文自动压缩（auto-compaction）失效以及系统提示词对 Agent 行为的过度引导。整体来看，维护者响应迅速，Bug 修复与功能迭代并行推进，项目处于健康且稳定的迭代节奏中。

## 2. 版本发布

### [v0.84.1](https://github.com/earendil-works/pi/releases/tag/v0.84.1)

- **Qwen Token Plan Individual**：内置 provider 现已支持面向 Individual 订阅的模型文档（详见 [providers.md](https://github.com/earendil-works/pi/blob/v0.84.1/packages/coding-agent/docs/providers.md#api-keys)）。
- **Authentication readiness checks**：新增 `pi auth` 相关就绪检查能力（描述截断，完整信息以 release notes 为准）。

**注意事项**：本版本有用户报告在 Node 23 环境下启动失败（`zlib.createZstdDecompress is not a function`，#7771），该 issue 目前标记为已关闭。若你的运行环境为 Node 23，建议升级时注意验证，或暂时固定在上一版本。

## 3. 项目进展

今日合并/关闭的 PR 中，以下几项值得关注：

| PR | 类型 | 说明 |
|---|---|---|
| [#7710](https://github.com/earendil-works/pi/pull/7710) | feat(agent) | 实现 harness v2 计划中的 R3 目标：恢复挂起的 harness 操作（restore suspended operations）。这是 agent 运行时可靠性的重要一步。 |
| [#7749](https://github.com/earendil-works/pi/pull/7749) | fix(coding-agent) | 修复 `/reload` 后自定义工具渲染器丢失的问题（对应 issue #7740），提升扩展机制一致性。 |
| [#7780](https://github.com/earendil-works/pi/pull/7780) | perf(TUI) | 通过增量解析 Markdown 和懒渲染失效优化 TUI 性能，改善长会话下的交互流畅度。 |
| [#7795](https://github.com/earendil-works/pi/pull/7795) | fix(coding-agent) | 使用 `command -v` 替代 `which` 验证 `wl-copy`，修复在沙箱等精简环境下的兼容性。 |
| [#7792](https://github.com/earendil-works/pi/pull/7792) | feat(coding-agent) | 新增隐藏的内置 `cursor-agent` 扩展，桥接已认证的本地 Cursor CLI 会话，无需额外 API Key。 |
| [#7766](https://github.com/earendil-works/pi/pull/7766) | feat(ai) | 保留 Codex `end_turn` 信息，便于调试（关联 issue #7689）。 |

此外，以下开放 PR 值得关注：

- [#7801](https://github.com/earendil-works/pi/pull/7801)（feat: lazily load uncommon syntax grammars）：实验性重构，按需加载不常用语法高亮，降低启动开销。
- [#6216](https://github.com/earendil-works/pi/pull/6216)（feat: Amazon Bedrock Mantle provider）：新增 AWS Bedrock Mantle OpenAI Responses 兼容 provider，已开放超一个月，等待评审。
- [#7762](https://github.com/earendil-works/pi/pull/7762)（feat(provider): LM Studio provider）：新增本地 LM Studio provider，对应 issue #7668。

今日的 PR 活动横跨 agent 运行时稳定性、TUI 性能、provider 生态和扩展机制修复，项目在多个维度同步推进。

## 4. 社区热点

1. **[#7547 [Windows] 使用体验讨论（23 条评论）](https://github.com/earendil-works/pi/issues/7547)**：这是目前社区最活跃的讨论帖。Windows 开发者数量庞大，但 Pi 在 Windows 上有多种运行方式且缺乏清晰的指引，社区呼吁官方聚焦核心场景并明确支持范围，以便集中修复文档和 bug。

2. **[#6879 auto-compaction 失效（13 条评论，👍 15）](https://github.com/earendil-works/pi/issues/6879)**：用户反映在 gpt-5.6-sol 长会话中，context 超过 100% 后自动压缩并不触发，直到 API 在 373k tokens 处拒绝请求才干预。该问题获得了大量高赞，说明长会话可靠性是用户的实质性痛点。评论中社区认为应该在每次 agent step 之后立即检查上下文阈值。

3. **[#7128 系统提示词过度鼓励 bash 调用（11 条评论，👍 7）](https://github.com/earendil-works/pi/issues/7128)**：默认系统提示词新增的 “Inspect PI_* environment variables” 指令导致 Agent 无必要地频繁执行环境检查命令。用户希望系统提示词更加保守，避免诱导无关的 shell 调用。

## 5. Bug 与稳定性

| 严重度 | Issue | 描述 | 是否已有 Fix PR |
|---|---|---|---|
| 🔴 高 | [#7771](https://github.com/earendil-works/pi/issues/7771) | v0.84.1 在 Node 23 下启动崩溃（zlib.createZstdDecompress 不可用） | 已关闭（状态为 CLOSED，需确认修复方式） |
| 🔴 高 | [#6879](https://github.com/earendil-works/pi/issues/6879) | auto-compaction 在整个 agentic turn 内不触发，直到 provider 拒绝请求 | 无，仍在讨论中 |
| 🟡 中 | [#7703](https://github.com/earendil-works/pi/issues/7703) | Agent.reset() 在 prompt() 活跃时调用会留下仅含 assistant 消息的 transcript | 无 |
| 🟡 中 | [#7709](https://github.com/earendil-works/pi/issues/7709) | OpenAI Responses 延迟 function_call 往返时丢失 namespace，导致下一轮报错 | 无 |
| 🟡 中 | [#7726](https://github.com/earendil-works/pi/issues/7726) | baseten provider 将 DeepSeek-V4-Flash-0731 的 maxTokens 设为 1M，超出 API 384K 限制 | 无 |
| 🟡 中 | [#7736](https://github.com/earendil-works/pi/issues/7736) | TUI 渲染行超过终端宽度时触发 uncaughtException 崩溃 | 无 |
| 🟢 低 | [#7053](https://github.com/earendil-works/pi/issues/7053) | 并行 tool batch 中某个工具卡住时，已完成工具的结果会丢失（提示 "No result provided"） | 无 |
| 🟢 低 | [#7740](https://github.com/earendil-works/pi/issues/7740) | `/reload` 后 custom tool 的 renderCall/renderResult 不生效（session_start 中注册的工具） | [✅ #7749](https://github.com/earendil-works/pi/pull/7749) 已合并 |

另外，[#7702](https://github.com/earendil-works/pi/issues/7702)（DeepSeek 经 opencode zen gateway 多轮工具调用报 400）和 [#7783](https://github.com/earendil-works/pi/issues/7783)（extension 的 `triggerTurn:false` 仍触发新 turn）也已关闭，预计修复已合入。整体来看，今日关闭的 53 条 issue 中有相当比例为 bug 确认与修复，项目在稳定性方面的响应较为及时。

## 6. 功能请求与路线图信号

- **[Agent Plugins 规范支持（#7776）](https://github.com/earendil-works/pi/issues/7776)**：社区建议识别根目录 `plugin.json` 并加载 `skills/` 目录，实现跨 Pi、Codex 等 Agent 的可移植插件。这可能是生态战略上值得关注的方向。
- **[LM Studio Provider PR（#7762）](https://github.com/earendil-works/pi/pull/7762)**：本地模型运行需求持续增长，该 PR 已提交并说明“所有 AI

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-08

## 今日速览

过去24小时项目保持高活跃度：65条Issue更新（新开/活跃36条，关闭29条），210条PR更新（待合并130条，合并/关闭80条），并发布1个开发版。今日动态主线集中在**成本计算准确性**与**依赖安全问题**两大方向——多条针对缓存token计费、Azure价格回归的修复PR已合并，同时多个CVE相关依赖固定问题获得解决。社区对依赖精确固定策略（`python-dotenv`、`uvicorn`等）仍存在显著不满情绪，相关Issue获得高赞。整体来看，项目在计费精度、安全修复和类型系统清理上稳步推进，但若干成本回归类Bug（如GPT-5.6成本少报5倍）需尽快响应。

---

## 版本发布

### v1.97.0-dev.2

- **链接**: https://github.com/BerriAI/litellm/releases
- **类型**: 开发预览版

**主要内容**：该版本重点说明所有Docker镜像均通过 [cosign](https://docs.sigstore.dev/cosign/overview/) 进行签名，并公布了签名公钥对应的提交引用（[`0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0)）。用户可通过cosign验证镜像完整性，适合在CI/CD流水线中增加供应链安全校验。

**破坏性变更**：无显著说明。此为dev预发布版，建议生产环境等待stable版本再升级。

---

## 项目进展

今日合并/关闭80条PR，重点推进了以下方向：

**1. 成本计算与缓存token修复（重要）**

- [#32445 fix(anthropic): map responses cached tokens to cache reads](https://github.com/BerriAI/litellm/pull/32445) — 修复 `/v1/messages`（Anthropic格式）桥接到OpenAI Responses模型时 `cache_read_input_tokens` 始终为0的问题（对应Issue #28354）。
- [#33071 fix(responses): map cache_write_tokens to cache_creation_input_tokens](https://github.com/BerriAI/litellm/pull/33071) — 补齐Responses路径 `cache_write_tokens` 到 `cache_creation_input_tokens` 的映射，完善GPT-5.6缓存计费链路。
- [#26893 fix: apply cache-read pricing in custom cost path](https://github.com/BerriAI/litellm/pull/26893) — 自定义计价路径下现在正确应用 `cache_read_input_token_cost`，修复 #26807。

**2. 安全与依赖**

- [#36227 build(deps): bump nanoid to 3.3.17](https://github.com/BerriAI/litellm/pull/36227) — 修复dashboard锁文件中CVSS 8.2的nanoid安全公告。
- [#36213 ci: always run the UI API types sync check](https://github.com/BerriAI/litellm/pull/36213) — 让类型同步检查可在每个PR上运行，防止回归。
- 多个依赖CVE相关Issue（python-dotenv #26333、python-multipart #27472）已关闭。

**3. UI与体验改进**

- [#36232 feat(ui): show user email or alias in usage data export](https://github.com/BerriAI/litellm/pull/36232) — Usage导出现在显示用户邮箱或别名，不再只有原始ID。

**4. 类型系统与代码健康**

- [#36217 fix(a2a): align agent list annotation](https://github.com/BerriAI/litellm/pull/36217) — 修复PR合并冲突导致的CI红。
- [#36189 chore(typing): clear basedpyright Any errors](https://github.com/BerriAI/litellm/pull/36189) — 在a2a、rag ingestion、memory端点用真实类型替换Any，lint预算减451个错误。

---

## 社区热点

**1. 依赖固定策略引发最强反弹**

- [#25280 [CLOSED] Dependency pinning in commit #5f63873 — intentional change?](https://github.com/BerriAI/litellm/issues/25280) — 15条评论、13👍，是今日讨论度最高的Issue。用户对 `python-dotenv` 精确固定到 `==1.0.1` 表示质疑。
- 姊妹Issue [#25210 python-dotenv pinned to ==1.0.1](https://github.com/BerriAI/litellm/issues/25210) 获得11👍。社区核心诉求：**库消费者需要宽松的依赖范围**，精确固定导致CVE无法修复、与其他包冲突。

**2. 日志无法关闭的长期痛点**

- [#10788 [OPEN] INFO logging of incoming requests cannot be switched off](https://github.com/BerriAI/litellm/issues/10788) — 12条评论，`LITELLM_LOG=ERROR` 不生效，代理服务器日志被INFO刷屏。该问题自2025年5月持续至今，仍在开放状态。

**3. 成本回归引发关注**

- [#36192 Azure GPT-5.6 terra/luna cost-map rows carry OpenAI's prices](https://github.com/BerriAI/litellm/issues/36192) — 新建当日即获2条评论。社区快速发现Azure模型价格错误套用了OpenAI直连价。

---

## Bug 与稳定性

按严重程度排序：

### 🔴 高严重度（成本/计费）

| Issue | 描述 | 状态 |
|-------|------|------|
| [#36094](https://github.com/BerriAI/litellm/issues/36094) | `azure/gpt-5.6-luna` 成本少报5倍（v1.95.0后回归，main分支） | OPEN，无fix PR |
| [#36192](https://github.com/BerriAI/litellm/issues/36192) | Azure GPT-5.6 terra/luna价格沿用OpenAI直连价，未应用Azure官方价目 | OPEN，无fix PR |
| [#32496](https://github.com/BerriAI/litellm/issues/32496) | fireworks_ai成本计算器忽略cached_tokens，100%全价计费 | OPEN，无fix PR |
| [#26893](https://github.com/BerriAI/litellm/pull/26893) | 自定义计价路径cache-read定价（已修复） | ✅ 已合并 |

### 🟠 中严重度（功能回归/错误）

| Issue | 描述 | 状态 |
|-------|------|------|
| [#22997](https://github.com/BerriAI/litellm/issues/22997) | v1.81.14在thinking+tool calling场景失败（Claude Code + Kimi K2.5），4👍 | OPEN，无fix PR |
| [#27469](https://github.com/BerriAI/litellm/issues/27469) | v1.83.7回归：OpenAI→Anthropic转换丢失 `tool_call.function.arguments` | OPEN，无fix PR |
| [#35359](https://github.com/BerriAI/litellm/issues/35359) | `batches.create` fallback到其他模型组后返回错误provider的报错信息 | OPEN，无fix PR |
| [#36119](https://github.com/BerriAI/litellm/pull/36119) | Bedrock ApplyGuardrail超大请求失败（有修复PR） | 🟡 fix PR待合并 |

### 🟡 低严重度（体验/安全/长期）

| Issue | 描述 | 状态 |
|-------|------|------|
| [#10788](https://github.com/BerriAI/litellm/issues/10788) | INFO日志无法关闭，`LITELLM_LOG=ERROR`无效 | OPEN（stale） |
| [#21026](https://github.com/BerriAI/litellm/issues/21026) | Team List / User List API频繁随机报错 | OPEN（stale） |
| [#34396](https://github.com/BerriAI/litellm/issues/34396) | Lakera v2 guardrail忽略 `skip_system_message_in_guardrail` / `skip_tool_message_in_guardrail` 配置 | OPEN |
| [#23345](https://github.com/BerriAI/litellm/issues/23345) | Model Info手动添加字段不持久化 | OPEN |
| [#33116](https://github.com/BerriAI/litellm/issues/33116) | Python 3.14安装失败（litellm-rust / PyO3 0.23.5） | CLOSED |

---

## 功能请求与路线图信号

今日有多个新功能PR提交，部分已具备较完整实现：

**1. 路由标签增强（下版本可能纳入）**

- [#36193 feat(router): add required-AND (&) tag prefix and allow_fail_open flag](https://github

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-08

## 今日速览

过去 24 小时项目保持高活跃度：共发生 29 条 PR 更新（待合并 15 条 / 已合并或关闭 14 条），Issue 更新 1 条（无新增关闭），暂无新版本发布。值得注意的是，**1.32.0 发布分支的两条准备 PR（#11448、#11444）同日提交并被合并**，表明版本发布流程已进入准备阶段。开发主力集中在 CHASM 纯任务状态机（#11433、#11432）、调度器迁移与版本控制（#11427、#11134）、以及可靠性工程（reliability-2026）系列改进上，社区侧唯一的活跃 issue 是已持续一年多的 Elastic 客户端替换请求（#7930）。

- 整体活跃度：**高**（29 条 PR 更新为近期高位）
- 重要里程碑信号：1.32.0 发布分支创建工作已启动
- 健康度：**良好**；无严重回归报告，修复类 PR 占比较高


## 版本发布

今日无正式版本发布。但需关注以下发布准备动态：

| PR | 说明 | 状态 |
|----|------|------|
| [#11448](https://github.com/temporalio/temporal/pull/11448) | **1.32.0: Prepare release branch** — 覆盖治理文件并更新依赖 | 已合并 |
| [#11444](https://github.com/temporalio/temporal/pull/11444) | **1.32.0: Prepare release branch**（并行准备分支） | 已合并 |
| [#11445](https://github.com/temporalio/temporal/pull/11445) | **Update to API v1.63.5** — 将 go.temporal.io/api 从伪版本升级到正式 tag（v1.63.5），符合 Cloud 发布要求 | 已合并 |

**迁移提示**：API 升级为 tag 版本对应，无破坏性变更说明；但 1.32.0 中包含的调度器行为变更（见下文）建议用户关注升级文档。


## 项目进展

今日合并/关闭的 14 条 PR 主要覆盖以下主题，从多个维度推动了项目进展：

**1. 可靠性工程（reliability-2026）系列持续推进**
- [#11255](https://github.com/temporalio/temporal/pull/11255) 新增 `shardinfo_immediate_queue_backlog_age` 指标，补齐了即时队列缺少时间维度积压观测的空白，是队列健康可观测性的重要补充。
- [#11311](https://github.com/temporalio/temporal/pull/11311) Backfiller 任务围栏机制改为使用持久化的任务序列值，替代此前基于任务执行时间与 HWM 的比较；并兼容旧二进制生成的无编号任务，增强了迁移过程中的稳定性。
- [#11308](https://github.com/temporalio/temporal/pull/11308) 在 legacy 与 CHASM 两类调度器中统一将 `VersioningOverride` 从 schedule actions 透传到 workflow start 请求，并在持久化前拒绝结构无效的覆盖配置，修复了调度器绕过版本控制的问题。

**2. 调度器（Scheduler）迁移与稳定性**
- [#11142](https://github.com/temporalio/temporal/pull/11142) 为调度器已知问题补充回归测试，为后续修复建立防护网。
- [#11427](https://github.com/temporalio/temporal/pull/11427)（待合并）为 V1 调度器 workflow 引入版本 13，迁移后的 CHASM buffered starts 优先保留已有 workflow/request ID，避免 ID 变更引发的下游问题。

**3. 复制与数据一致性**
- [#11424](https://github.com/temporalio/temporal/pull/11424) 待机子工作流完成验证时，将父工作流的跨集群重发改为**异步执行**，避免同步重发带来的长耗时阻塞，改善了 standby 场景的性能表现。

**4. 测试基础设施**
- [#11441](https://github.com/temporalio/temporal/pull/11441) 将 137 个根功能测试迁移到可导入的注册表，支持按名称、正则和谓词筛选，并使功能测试可被外部 runner 使用。这是测试基础设施开放化的重要一步。

**5. 发布流程**
- 1.32.0 分支准备 PR 已合并（见上文版本发布板块）。

整体来看，项目在可靠性可观测性、调度器一致性、复制链路健壮性和测试基础设施四个方向同时取得了实质性进展，且 14 条合并/关闭 PR 中大多数为功能改进而非琐碎维护。


## 社区热点

今日社区讨论聚焦点仍是长期未关闭的 issue：

**[#7930 Replace "github.com/olivere/elastic/v7" with the official client "github.com/elastic/go-elasticsearch"](https://github.com/temporalio/temporal/issues/7930)**

- 作者：@jmbarzee
- 创建：2025-06-18（持续超过 14 个月）
- 更新：2026-08-07
- 评论：17 条 | 👍 0

**背景与诉求**：`olivere/elastic` 已被官方标记为弃用（deprecated），用户希望 Temporal 跟进迁移到 Elastic 官方 Go 客户端。该 issue 自 2025 年 6 月提出后一直处于 open 状态，昨日有新的动态更新，说明社区仍在关注。0 👍 但 17 条评论表明虽然广泛讨论但投票热度不高——可能因为这是一个技术债清理型任务，对最终用户的功能影响有限，所以优先级一直被排在后面。但这确实是项目长期健康度的一个隐患。

此外，今日活跃的 PR #11433（CHASM 纯任务失效断言）和 #11432（纯任务失效不变性守卫）在技术社区内关注度较高，属于对 CHASM 框架核心不变量（纯任务执行后必须失效）的强化，体现了项目对新架构严谨性的重视。


## Bug 与稳定性

今日合并/关闭的 PR 中包含以下稳定性修复（按潜在影响排序）：

| 严重程度 | 问题 | 修复 PR | 说明 |
|---------|------|---------|------|
| 中 | 跨集群重发父工作流可能长时间阻塞 | [#11424](https://github.com/temporalio/temporal/pull/11424) | 待机子工作流完成验证期间，若超过阈值需要重发父工作流，原本是同步执行（涉及跨集群状态同步 + 分页历史回填），现改为异步，消除了潜在的长时阻塞 |
| 中 | 源集群删除工作流时，在途的 SYNC_VERSIONED_TRANSITION 任务在目标端应用失败后，清理逻辑构造的删除任务执行返回 NotFound 且被错误 DLQ | [#11440](https://github.com/temporalio/temporal/pull/11440)（待合并） | 修复清理路径上任务被误判为 DLQ 场景 |
| 低 | 子工作流在 ChildWorkflowExecutionStarted 后 NotFound，但无对账指标 | [#11447](https://github.com/temporalio/temporal/pull/11447)（待合并） | 新增 `child_execution_not_found` 计数器和 Error 日志，便于观测，不改变行为 |
| 低 | CLI 全局 flag（如 -c）放置在子命令之后时报错信息无引导 | [#10227](https://github.com/temporalio/temporal/pull/10227)（待合并） | 改善用户提示，说明全局 flag 应置于子命令之前；已持续开放近 3 个月 |

**未发现** P0/P1 级别的严重 Bug、崩溃或数据损坏类问题。


## 功能请求与路线图信号

**1. Elastic 官方客户端替换（#7930）**

请求将已弃用的 `github.com/olivere/elastic/v7` 替换为官方 `github.com/elastic/go-elasticsearch`。结合 Temporal 近期对依赖治理的重视（如 #11445 将 API 依赖升级到正式 tag），该项目有可能在后续版本（1.32.0 或之后）被纳入技术债清理范围。但考虑到该 issue 搁置时间超过一年，短期内被处理的概率仍偏低。

**2. 功能测试外部化（#11441）**

将功能测试注册表开放给外部 runner —— 这是 Temporal 生态开放性增强的一个信号，未来第三方项目可能可以直接复用 Temporal 的功能测试框架，对生态发展有积极意义。

**3. 调度器迁移增强（#11427、#11134）**

两个 PR 合力完善 V1↔V2 调度器之间的迁移安全性（保留 ID、避免 3rd party SDK 崩溃），反映 Temporal 团队正在为调度器迁移场景做深度加固。


## 用户反馈摘要

基于 issue #7930 的评论内容（共 17 条），用户侧反馈要点：

- **技术债关注**：有用户指出 `olivere/elastic` 已停止维护，继续依赖存在安全和兼容性风险，尤其对使用 Elasticsearch 高级特性（如自定义查询）的部署场景影响明显。
- **使用场景**：Temporal 使用 Elasticsearch 作为 Visibility 存储，该问题影响的是**生产环境依赖 Elasticsearch Visibility 的用户**；不使用 ES Visibility 的用户基本无感知。
- **社区态度**：整体倾向于"应该做、但优先级不高"的共识，未见到强烈催促或 workaround 需求，反映了该请求属于"重要不紧急"类型。

其他 PR 讨论中未见明显负面反馈；CHASM 相关 PR 的技术评论区相对安静，说明设计文档和实现基本获得了 reviewer 认可。


## 待处理积压

| 项目 | 类型 | 已开放时间 | 详情 |
|------|------|-----------|------|
| [#7930](https://github.com/temporalio/temporal/issues/7930) Elastic 客户端替换 | Issue（enhancement） | 2025-06-18 至今（**14+ 个月**） | 替换已弃用的 olivere/elastic，昨日有更新，但无明确处理计划 |
| [#10227](https://github.com/temporalio/temporal/pull/10227) CLI 全局 flag 提示改进 | PR（待合并） | 2026-05-12 至今（**近 3 个月**） | 修复 `temporal-server start -c` 报错无提示的问题，修复内容简单明确（Fixes #6226），但一直未获 review/merge，建议维护者优先关注 |
| [#11257](https://github.com/temporalio/temporal/pull/11257) 复制应用时重建缺失的当前执行记录 | PR（待合并） | 2026-07-24 至今（**2 周+**） | 涉及复制一致性的重要修复，已进入 review 尾声 |

**维护者提醒**：#10227 是一个解决真实用户痛点的小改动（PR 描述中明确复现了 `temporal-server start -c /etc/temporal` 的报错场景），却搁置了近三个月。建议在下一个 triage 会议中确认其状态。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*