# OpenClaw 生态日报 2026-08-01

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-31 23:26 UTC

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

# OpenHands SDK 项目动态日报 — 2026-08-01

## 1. 今日速览

过去 24 小时项目活跃度处于高位：共 38 条 Issue 更新（新开/活跃 31 条，关闭 7 条）和 50 条 PR 更新（待合并 47 条，合并/关闭 3 条），表明社区讨论和开发提交均十分密集；无新版本发布。讨论热点集中在函数调用参数错误、异步并发控制缺失、ACP 协议兼容性等问题上，体现出用户对本地模型支持和系统稳定性有较高期待。今日合并了 3 个 PR，包括对话错误分类、LLM 提供者抽象重构和发布分支命名修复，项目在架构治理和可观测性方面稳步推进。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日有 3 个 PR 被关闭/合并，虽然数量不多，但包含一个重要的架构级重构：

- **PR #4316**（合并）：[feat(sdk): classify conversation errors](https://github.com/OpenHands/software-agent-sdk/pull/4316) — 为对话和 Agent 错误事件引入向后兼容的结构化分类，将运行限制、Provider 异常和未识别异常统一处理，使 SDK 消费者的错误处理更一致、可操作。
- **PR #2363**（关闭）：[refactor(llm): add LiteLLM-backed provider abstraction](https://github.com/OpenHands/software-agent-sdk/pull/2363) — 将原先混合的 "provider/model" 字符串抽象为独立的 Provider 层，为后续多 Provider 管理、模型路由和配置简化奠定基础；该 PR 由 @enyst 提交并经过人工测试，是 LLM 子系统的一项长期基础设施改进。
- **PR #4073**（合并）：[Use the right branch name in release branches](https://github.com/OpenHands/software-agent-sdk/pull/4073) — 修复发布分支命名模式（采用 `rel-*`），与当前实际使用的分支策略对齐，减少发布流程的混乱。

此外，今日新提交的 PR 中也出现了若干值得关注的方向：**PR #4319**（[修复 PATCH /api/settings 激活 profile 时加载对应 LLM](https://github.com/OpenHands/software-agent-sdk/pull/4319)）、**PR #4323**（[限制 Webhook 投递内存](https://github.com/OpenHands/software-agent-sdk/pull/4323)）、**PR #4311**（[在自动化回调中报告累计 LLM 成本](https://github.com/OpenHands/software-agent-sdk/pull/4311)），分别涉及配置管理、稳定性防护和可观测性增强。

## 4. 社区热点

- **[Issue #3540](https://github.com/OpenHands/software-agent-sdk/issues/3540)**（24 条评论，已关闭）：提议为 agent-server 增加 OpenAI 兼容的 `/v1/chat/completions` 网关，使任何 OpenAI 协议客户端都能直接与 OpenHands Agent 对话。这是社区呼声很高的互操作性需求，24 条评论说明讨论相当深入，虽已关闭但思路可能已进入其他实现路径。
- **[Issue #4019](https://github.com/OpenHands/software-agent-sdk/issues/4019)**（14 条评论）：ACP profile 注入的 workspace 技能与 ACP CLI 自身依据 AGENTS.md 摄入的技能重复，导致冲突或冗余加载，用户对技能加载机制的精确性有较高要求。
- **[Issue #4248](https://github.com/OpenHands/software-agent-sdk/issues/4248)**（12 条评论）：`execute_bash` 缺少必填参数 `security_risk`，DeepSeek-reasoner 等模型调用时直接报错。反映当前工具调用对模型输出的 schema 兼容性要求较严格，对非 GPT 类模型存在摩擦。
- **[Issue #3992](https://github.com/OpenHands/software-agent-sdk/issues/3992)** 与 **[Issue #4063](https://github.com/OpenHands/software-agent-sdk/issues/4063)**（各 11 条评论）：前者讨论内容型响应（无工具调用）被不对称处理导致弱模型/本地模型 Agent 直接终止；后者指出 `max_concurrent_runs` 没有限制原生异步对话，并发控制行为与文档不符。

**分析**：社区热点集中在协议兼容性、本地/弱模型适配以及并发控制这三条主线上，说明 OpenHands SDK 的用户群体正从 GPT 模型主导向更多样化的模型和部署场景扩展，项目需要在抽象层和容错机制上做出相应调整。

## 5. Bug 与稳定性

按严重程度排列：

**高严重度（安全/凭据）**

- **[Issue #4271](https://github.com/OpenHands/software-agent-sdk/issues/4271)** — GitHub 凭据在 git remote URL 中未脱敏，直接暴露在终端输出中，存在凭据泄露风险；尚无关联修复 PR。
- **[Issue #4157](https://github.com/OpenHands/software-agent-sdk/issues/4157)** — `LLMSecurityAnalyzer` 直接信任模型自我评估的风险等级，`confirmation_mode` 下 LOW 风险动作自动执行，可能绕过人工确认机制。
- **[Issue #4263](https://github.com/OpenHands/software-agent-sdk/issues/4263)** — `get_litellm_model_info` 在未经验证的情况下发起 `httpx.get` 请求，被第三方审计标记为潜在出口漏洞（HIGHLY，P2）。

**中高严重度（核心功能破坏）**

- **[Issue #4248](https://github.com/OpenHands/software-agent-sdk/issues/4248)** — `execute_bash` 缺失 `security_risk` 参数导致 DeepSeek 等模型工具调用失败。
- **[Issue #4063](https://github.com/OpenHands/software-agent-sdk/issues/4063)** — `max_concurrent_runs` 配置不生效，原生异步对话可以绕过并发限制，可能引发资源耗尽。
- **[Issue #4080](https://github.com/OpenHands/software-agent-sdk/issues/4080)** — 单个事件反序列化失败会导致整个会话加载失败，且在 Agent-Server 端被静默丢弃、404 不可见。
- **[Issue #3992](https://github.com/OpenHands/software-agent-sdk/issues/3992)** — 内容型响应被当作异常终止处理，对较弱/本地模型极不友好。
- **[Issue #4256](https://github.com/OpenHands/software-agent-sdk/issues/4256)** — Docker 镜像内 browser-use 启动 Chromium 时未带 `--no-sandbox`，导致 `BrowserLaunchEvent` 超时和 CDP 初始化失败。

**中低严重度（体验/配置）**

- **[Issue #4245](https://github.com/OpenHands/software-agent-sdk/issues/4245)** — Webhook 连接失败导致容器崩溃和 Sandbox 连接错误。
- **[Issue #4255](https://github.com/OpenHands/software-agent-sdk/issues/4255)** — Ollama 模型任务超过 300 秒被强制终止，UI 内调整超时无效。
- **[Issue #4252](https://github.com/OpenHands/software-agent-sdk/issues/4252)** — 新增的 Global Skills 在 CLI 安装和 WebUI 中均无法加载。

**已有修复 PR 的 Bug**：`max_concurrent_runs`（#4063）与 `_build_acp_settings` 技能重复（#4018/#4019）相关修复正在推进中；`switch_profile` 半应用问题（#4158）在 **PR #4221**（[base_state 在恢复时作为权威依据](https://github.com/OpenHands/software-agent-sdk/pull/4221)）中尝试从根因上解决，该 PR 涵盖 LLM/profile 切换、超时恢复等多个关联问题。

## 6. 功能请求与路线图信号

- **OpenAI 兼容网关**（[Issue #3540](https://github.com/OpenHands/software-agent-sdk/issues/3540)）：虽已关闭，但这是将 OpenHands Agent 接入更广泛生态的关键接口，很可能以其他形式落地。
- **/goal 持久目标命令**（[Issue #3569](https://github.com/OpenHands/software-agent-sdk/issues/3569)）：借鉴 Codex CLI 的 `/goal` 功能设计，用户需求明确，评论区有积极讨论，可能与未来的任务自动化能力结合。
- **标题生成 LLM 偏好**（[Issue #4199](https://github.com/OpenHands/software-agent-sdk/issues/4199)）：SDK 已支持 `title_llm_profile` 持久化，但 Canvas 和 OpenHands 应用层缺少暴露入口，属于体验补全型需求，落地难度较低。
- **PR #4113**（[物化非内联多部分内容到工作区](https://github.com/OpenHands/software-agent-sdk/pull/4113)）：将图片等多部分附件写入沙箱文件系统，解决 Agent 无法读取内联内容的问题，是重要的能力补充。
- **PR #4101**（[发布 python-lite 镜像](https://github.com/OpenHands/software-agent-sdk/pull/4101)）：通过跳过预装 ACP Provider 减小镜像体积，面向 docker 部署的轻量化需求。
- **PR #4311**（[自动化完成回调报告 LLM 成本](https://github.com/OpenHands/software-agent-sdk/pull/4311)）：为自动化任务增加成本可观测性，符合平台化运营的趋势。
- **PR #4134**（[重试空聊天流](https://github.com/OpenHands/software-agent-sdk/pull/4134)）：修复流式响应为空时不重试导致的任务失败，属于稳定性优化。

综合来看，下一版本可能纳入的方向包括：ACP/OpenAI 协议兼容性增强、本地模型容错改进、多部分内容处理、资源使用可观测性以及部署轻量化。

## 7. 用户反馈摘要

- **本地模型支持是核心痛点**：多个 Issue（#4247、#4248、#4250、#4255）反映出用户对 DeepSeek、Ollama、LM Studio、Workers AI 等本地/替代模型的支持存在明显摩擦。典型反馈包括："DeepSeek-reasoner 调用 `execute_bash` 直接报

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-01

## 1. 今日速览

过去 24 小时内，LiteLLM 仓库迎来中高强度活跃：共 52 条 Issue 更新（39 条新开或活跃，13 条关闭）与 246 条 PR 更新（180 条待合并，66 条已合并/关闭）。版本节奏上，v1.96.0-dev 系列连续发布两个开发版、v1.95.0-rc.2 进入候选阶段，说明项目正处于 v1.95.0 收尾与 v1.96.0 新功能开发并行的快节奏周期。开发重点集中在 PTU（预置吞吐量）计费功能、UI/UX 增强、Responses API 桥接修复以及 Azure Entra ID 认证支持等方面，同时社区反馈了大量与流式响应、速率限制、Redis 连接相关的真实生产问题，项目整体活跃度与响应速度呈现健康态势。

## 2. 版本发布

今日发布 3 个新版本，均为预发布版本：

- **v1.96.0-dev.2** — https://github.com/BerriAI/litellm/releases/tag/v1.96.0-dev.2
- **v1.95.0-rc.2** — https://github.com/BerriAI/litellm/releases/tag/v1.95.0-rc.2
- **v1.96.0-dev.1** — https://github.com/BerriAI/litellm/releases/tag/v1.96.0-dev.1

三个版本的发布说明内容一致，均为模板化的 Docker 镜像签名验证说明：LiteLLM 所有 Docker 镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 签名，每个 release 使用与 [commit `0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0) 相同的密钥。**无破坏性变更与迁移注意事项**。值得关注的是 v1.95.0-rc.2 的发布，说明 v1.95.0 进入候选阶段，预计正式版即将推出。

## 3. 项目进展

过去 24 小时 66 条 PR 已合并/关闭（约占 PR 总数的 27%），展示了持续较高的代码吞吐量。以下几项值得关注：

**已合并/关闭的 PR：**

- **fix(type-discipline): exempt values frozen in place by tuple/frozenset/MappingProxyType from LIT002** ([#35325](https://github.com/BerriAI/litellm/pull/35325)) — 修复 LIT002 静态检查器对已由不可变类型包装的字典/集合/列表字面量的误报，提升代码质量工具链的准确性。
- **fix(ui): search request logs by request_id server-side** ([#32134](https://github.com/BerriAI/litellm/pull/32134)) — 将 UI 顶部的"通过 Request ID 搜索"字段接入已有的 `/spend/logs/ui?request_id=` 后端过滤接口，移除仅搜寻当前页的客户端过滤，修复 #32047。这是用户可感知的 UI 修复。

**关键功能 PR 管线（当前 OPEN，代表路线图信号）：**

- **PTU（Provisioned Throughput）计费功能系列**：今日出现 4 个相互关联的 PR，构成一个完整的功能模块——[#35341](https://github.com/BerriAI/litellm/pull/35341) 在模型部署上增加配置 PTU 计费字段的能力；[#35343](https://github.com/BerriAI/litellm/pull/35343) 实现按活跃小时写入每日 PTU 计费 rollup；[#35391](https://github.com/BerriAI/litellm/pull/35391) 将 PTU 费率暴露于日常活动读取路径；[#35393](https://github.com/BerriAI/litellm/pull/35393) 在 UI 模型表单和 Usage 页面加入 PTU 输入和展示。说明 LiteLLM 正在补齐预置吞吐量的端到端成本计量能力。

## 4. 社区热点

今日讨论最活跃的 Issue 集中在流式处理、Redis 连接、OpenRouter 模型选择等真实生产场景问题：

- **[#25869] Gemini 流式工具调用损坏（8 评论）** — [链接](https://github.com/BerriAI/litellm/issues/25869)
  用户 @jph00 报告 `stream_chunk_builder` 会破坏 Gemini 的 `server_side_tool_invocations` 和 `thought_signatures`，导致多轮对话中后续请求出现 `400 Bad Request: "Corrupted tool call context"`。这是流式场景下较为隐蔽的数据完整性问题，8 条评论的讨论热度也说明影响面较广。

- **[#16587] Redis ssl=False 强制使用 SSLConnection（7 评论）** — [链接](https://github.com/BerriAI/litellm/issues/16587)
  报告指出 `ssl=False` 的配置会被"配置项存在即启用"的逻辑误判为需要 SSL，导致 GCP Memorystore 非 TLS 实例连接失败。用户提供了详细环境参数（LiteLLM 1.79.1, redis-py 5.2.1, Redis 4.0.14, Kubernetes），属于配置语义实现的边界问题。

- **[#24795] OpenRouter 模型 Test Connect 失败（7 评论，7 👍）** — [链接](https://github.com/BerriAI/litellm/issues/24795)
  从 Admin UI 下拉列表选择 `openrouter/google/gemini-2.5-flash` 后点击 Test Connect 报 `"is not a valid model ID"`。这个 issue 获得了 7 个 👍，说明许多用户在使用 OpenRouter 模型时遇到了类似的模型 ID 校验问题。

- **[#19086] 错误登录重定向（6 评论，2 👍，已关闭）** — [链接](https://github.com/BerriAI/litellm/issues/19086)
  `/fallback/login` 登录后跳转到不存在的 URL，用户需要手动进入 `/ui`。部分同事反馈更新后"登录机制完全损坏"，说明该问题在特定配置下影响较大。已关闭，但需关注修复是否进入正式版本。

## 5. Bug 与稳定性

今日新增 Bug 按严重程度排列：

**高严重度：**

- **[#35411] AttributeError: `LiteLLMCompletionStreamingIterator` 缺少 `completed_response` 属性（Anthropic 经 Responses API 中途报错）** — [链接](https://github.com/BerriAI/litellm/issues/35411)
  流式中途发生 provider 错误时，迭代器对象上没有已完成的响应属性，导致 AttributeError 掩盖真实错误，并绕过重试和 fallback 机制。**已有修复 PR：[#35413](https://github.com/BerriAI/litellm/pull/35413) 已创建**。

- **[#35357] 单个 batch 报错导致整个 CheckBatchCost 轮询周期中止** — [链接](https://github.com/BerriAI/litellm/issues/35357)
  成本计算轮询缺乏 per-job 错误隔离，一个批次的成本计算异常会让所有其他批次陷入停滞。

**中严重度：**

- **[#35358] CheckBatchCost 完成 reconciliation 但不写 spend 行** — [链接](https://github.com/BerriAI/litellm/issues/35358)
  托管批次成功标记为 `batch_processed=true`，但计费明细静默丢失，无任何错误提示。对账单准确性有直接影响。

- **[#35362] `client.files.list()` 在托管文件代理上报 "api_key client option must be set"** — [链接](https://github.com/BerriAI/litellm/issues/35362)
  普通 OpenAI SDK 调用在启用托管文件功能时返回 500，影响文件管理 API 的可用性。

- **[#25869] Gemini 流式工具调用上下文损坏（见上文）** — [链接](https://github.com/BerriAI/litellm/issues/25869)
  会导致多轮工具调用对话完全不可用。

**低严重度/配置类：**

- **[#16587] Redis ssl=False 配置被误判为启用 SSL** — [链接](https://github.com/BerriAI/litellm/issues/16587)
  属于配置存在性检查的逻辑缺陷，影响非 TLS Redis 用户。

## 6. 功能请求与路线图信号

今日社区提出多个新功能需求，结合已有 PR 判断路线图方向：

- **新模型/平台支持（强信号）**：
  - [#33921](https://github.com/BerriAI/litellm/issues/33921) 请求原生支持 Kimi K3（Moonshot AI）、Inkling（Thinking Machines Lab）和 Tinker 平台。
  - [#35410](https://github.com/BerriAI/litellm/issues/35410) 请求支持 kimi k3、glm 5.2 等 Morph 平台模型。
  - [#24229](https://github.com/BerriAI/litellm/issues/24229) 请求将 `venice/grok-code-fast-1` 加入模型定价文件。
  新模型接入持续是社区最集中的需求方向。

- **认证方式扩展**：[#31649](https://github.com/BerriAI/litellm/issues/31649)（已关闭）请求支持 OpenAI Workload Identity Federation（OIDC token exchange）。配合今日 [#35415](https://github.com/BerriAI/litellm/pull/35415) PR 为所有 Azure AI Foundry 路由新增 Entra ID/OAuth 认证，说明企业级认证能力正在被积极补齐。

- **用户身份映射（6 👍）**：[#21927](https://github.com/BerriAI/litellm/issues/21927) 请求将请求头映射的用户 ID 改为映射用户 Email，典型使用场景为 OpenWebUI 的对接。

- **自助密码找回（已进入开发）**：PR [#35083](https://github.com/BerriAI/litellm/pull/35083) 为内部用户实现自助忘记密码流程，回应了非 SSO 用户无法自行找回访问权限的长期痛点。

- **可观测性增强（PR 信号）**：[#34201](https://github.com/BerriAI/litellm/pull/34201) 为 Prometheus 增加全局 `exclude_metrics` 和 `exclude_labels` 配置项，满足指标定制需求。

## 7. 用户反馈摘要

- **流式功能的可靠性是核心痛点**：#25869 用户详细定位了 `stream_chunk_builder` 对 Gemini 工具调用上下文的破坏路径，并指出这会导致多轮对话彻底不可用。

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*