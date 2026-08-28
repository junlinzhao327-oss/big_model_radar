# OpenClaw 生态日报 2026-08-28

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-28 06:10 UTC

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

# AI 智能体与个人助手开源生态横向对比 — 2026-08-28

## 1. 生态全景

个人 AI 助手/自主智能体生态正从"模型能力展示"快速转向"生产级基础设施"建设。LiteLLM 以**日均 300+ PR 更新**的高频迭代打磨 AI 网关，Rust 迁移计划与计费/路由优化揭示基础设施层竞争已进入"性能+成本"深水区。Temporal 则代表工作流引擎在 AI 代理场景的纵深整合，尤其是 CHASM/System Nexus 与 Worker Deployment 相关修复，表明长时运行任务对状态可靠性的要求正从"可用"升级为"可审计、可恢复"。二者分别从**南北向流量**与**东西向状态**两个维度，为上层 OpenClaw、Hermes Agent、OpenHands SDK、Pi 等应用/框架层智能体提供支撑，生态分工日趋清晰。

## 2. 各项目活跃度对比

| 项目 | Issues（24h更新） | PRs（24h更新） | Release | 健康度评估 |
|------|-------------------|----------------|---------|------------|
| **LiteLLM** | 79 条（58 活跃 / 21 关闭） | 324 条（184 待合并 / 140 合并关闭） | v1.100.0-dev.2 | 🟢 **极高活跃**，快速迭代期，Bug 修复响应快（Bedrock 认证问题当天有 fix） |
| **Temporal** | 2 条（均新开） | 81 条（33 合并/关闭 / 48 待合并） | 无（1.32.0 收尾中） | 🟢 **高活跃**，可靠性专项加固阶段，P0 部署阻断问题待解决 |
| **OpenClaw** | 本期无数据 | 本期无数据 | 本期无数据 | ⚪ 待数据补齐 |
| **Hermes Agent** | 本期无数据 | 本期无数据 | 本期无数据 | ⚪ 待数据补齐 |
| **OpenHands SDK** | 本期无数据 | 本期无数据 | 本期无数据 | ⚪ 待数据补齐 |
| **Pi** | 本期无数据 | 本期无数据 | 本期无数据 | ⚪ 待数据补齐 |

> ⚠️ **数据说明**：OpenClaw、Hermes Agent、OpenHands SDK、Pi 四个仓库本期未采集到社区动态，下表定位与趋势分析将结合项目公开背景进行定性推断，不涉及

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-28

## 1. 今日速览

过去24小时LiteLLM项目保持极高的开发活跃度：共产生79条Issue更新（新开/活跃58条，关闭21条）和324条PR更新（待合并184条，合并/关闭140条）。值得注意的是，今日有多个高价值PR被合并，包括Anthropic reasoning_effort参数修复、complexity router路由优化、以及management API新增用户PATCH端点；同时发布了1个新的开发版本v1.100.0-dev.2。社区层面，Rust迁移计划（#31263）仍是讨论最热烈的话题，反映了用户对网关性能的持续关注；新提交的Bedrock bearer-token认证耗时问题（#38549）已获得快速响应并出现对应修复PR，体现了项目维护的高效闭环。

- **Issue 活跃度**：极高（79条/24h，其中58条处于活跃状态）
- **PR 活跃度**：极高（324条/24h，含184条待合并）
- **核心主题**：Rust迁移、Bedrock稳定性、计费正确性、UI/UX改进

## 2. 版本发布

### v1.100.0-dev.2（开发版）

- **发布时间**：2026-08-28
- **说明**：这是v1.100.0系列的第二个开发版本。该版本发布说明未包含功能变更日志，仅强调所有Docker镜像均使用[cosign](https://docs.sigstore.dev/cosign/overview/)进行签名验证。每次发布使用同一签名密钥（见commit [`0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0)）。
- **注意事项**：作为dev版本，不建议在生产环境直接升级；生产用户应等待稳定版发布。建议验证镜像签名后再部署。

## 3. 项目进展

今日合并/关闭了多个高价值PR，显著推进了以下方向：

### 3.1 核心路由与代理逻辑

- **[fix(anthropic): handle per-level reasoning_effort flags without supports_reasoning](https://github.com/BerriAI/litellm/pull/38618)** — 已合并。修复了 `gpt-5-search-api` 等模型因缺少 `supports_reasoning` 标志导致 `minimal` 请求降级到 `low` 的问题。此前解析器仅检查 `supports_reasoning` 标志，忽略 `supports_minimal_reasoning_effort` 等分级别支持。此修复对使用 Anthropic 模型且依赖分级推理能力（minimal/low/medium/high）的用户至关重要。

- **[fix(complexity_router): route client housekeeping calls to the cheapest tier](https://github.com/BerriAI/litellm/pull/38598)** — 已关闭。修复了编码代理的会话标题生成（housekeeping）请求被错误分类为COMPLEX并路由到顶级模型的问题。真实流量数据显示，一天17次标题生成调用中有11次被误判。现在分类器将识别客户端自身维护性提示词，并将其路由到最低成本层级。

- **[fix(router): drop a tier param the routed target cannot take](https://github.com/BerriAI/litellm/pull/38622)** — 已关闭。修复了自动路由器在目标部署不支持某tier参数时整个tier返回400错误的问题。现在过滤器会检查分组部署声明的能力，在请求离开代理前剔除目标不支持的参数。此修复涉及kimi-k3的Lite预设的四个后端。

### 3.2 Management API 与 UI

- **[feat(management-v1): add PATCH /management/v1/users/{user_id} so user settings can be cleared](https://github.com/BerriAI/litellm/pull/38599)** — 已关闭。新增 `PATCH /management/v1/users/{user_id}` 端点，支持合并补丁语义。解决此前 `/user/update` 静默丢弃null值、无法清除用户设置的长期问题（此前仅 `max_budget` 可通过一次性补丁清除）。这补全了用户管理的关键能力。

- **[feat(ui): edit the auto-router tier set with custom classifier-defined tiers](https://github.com/BerriAI/litellm/pull/38603)** — 待合并。新的自动路由器表单不再固定为四个复杂度层级，提供 "Edit tiers" 按钮可将层级列表转为编辑器，支持自定义名称和分类器描述。需要 SECURITY_REVIEW 等自定义层级的运维人员无需再手写原始配置。

### 3.3 其他重要合并/关闭

- **[chore(ci): promote internal staging to main](https://github.com/BerriAI/litellm/pull/38616)** — 已关闭。内部staging分支合并至main。
- **[fix(proxy): admit litellm_proxy/hosted_vllm in provider-endpoint discovery](https://github.com/BerriAI/litellm/pull/38617)** — 待合并。修复 `GET /v1/models` 返回字面量 `litellm_proxy/*` 而非上游模型列表的问题。
- **[fix(searxng): preserve upstream HTTP errors instead of returning empty results](https://github.com/BerriAI/litellm/pull/38630)** — 待合并。修复SearXNG搜索适配器未检查HTTP状态码、在429/503时返回空结果的问题，对应 #38628。
- **[fix(shadow_eval): measure both arms' cost so a job reports what the router would have saved](https://github.com/BerriAI/litellm/pull/38631)** — 待合并。阴影评估现在同时报告影子臂成本，包括此前缺失的分类器调用成本。

## 4. 社区热点

### 今日最热讨论

1. **[#31263 LiteLLM Rust Migration - the fastest and litest AI Gateway](https://github.com/BerriAI/litellm/issues/31263)** — 21条评论，17个👍
   作为Rust迁移的父ticket，持续获得社区高度关注。目标是在sub 1ms开销内实现最快的AI网关。该项目开启了Beta测试者申请表格，并将Rust版本定位为"lite"实现（重量更轻、资源占用更少）。社区反馈表明用户对网关性能极致化有强烈需求，尤其是对延迟敏感的应用场景。此迁移可能对项目的长期架构产生根本性影响。

2. **[#26886 [Bug]: Prisma reconnection failed](https://github.com/BerriAI/litellm/issues/26886)** — 16条评论，11个👍
   LiteLLM Proxy Pod周期性不稳定的问题。用户反馈Prisma查询引擎进程频繁崩溃，且未提供有效恢复机制。该Issue已持续4个月未解决，影响面较大（11人点赞），反映了生产环境稳定性的核心诉求。

3. **[#24530 [Security]: /metrics endpoint default-unauthenticated exposes multi-tenant PII](https://github.com/BerriAI/litellm/issues/24530)** — 8条评论
   安全漏洞报告：Prometheus的`/metrics`端点默认无认证，在多租户生产部署中暴露敏感数据。虽然存在`require_auth_for_metrics_endpoint: true`的显式配置，但默认不安全的设置导致广泛风险。这是企业级部署中的显著安全隐患，已有第三方（Aitema-gmbh）专门跟进。

4. **[#33383 Upgrade Langfuse integration to Python SDK v4 and v4 OTel ingestion](https://github.com/BerriAI/litellm/issues/33383)** — 8条评论，9个👍
   Langfuse团队成员直接提出的需求，希望LiteLLM升级Langfuse SDK至v4.7.0+或兼容v4 OTel span。Langfuse Cloud的Fast Preview已采用新观测优先的摄取路径，当前集成若不加紧跟进将影响LiteLLM用户在Langfuse上的实时数据体验。这条Issue体现了两大开源项目之间的生态协作。

5. **[#30762 [Bug/Docs]: Snowflake provider streaming tool-calls dropped](https://github.com/BerriAI/litellm/issues/30762)** — 8条评论
   Snowflake Cortex的使用者报告了多个关联问题：流式工具调用被丢弃、端点文档有误导性、OpenAI-/Anthropic兼容Cortex端点的SDK使用存在缺口。涉及`/snowflake/`提供商代码和文档两个层面。

### 分析

社区热点集中在三类诉求：**性能**（Rust迁移）、**稳定性**（Prisma崩溃）、**安全**（metrics未认证暴露）。这三者恰好对应LLM网关在生产环境中的核心关切：低延迟、高可靠、强安全。这些热点议题将持续影响项目的Roadmap优先级。

## 5. Bug 与稳定性

### 高严重度（已有修复或有明确影响）

1. **[#38549 [Bug]: Bedrock bearer-token auth resolves and discards AWS credentials](https://github.com/BerriAI/litellm/issues/38549)** — 新报，有fix
   当使用bearer token认证时，LiteLLM仍会尝试解析AWS SigV4凭据并丢弃结果，在无EC2实例元数据服务的环境中每次请求都会消耗约2秒IMDS超时。这是一个性能放大Bug，对AWS外部署Bedrock的用户影响严重。**已有修复PR：[#38619](https://github.com/BerriAI/litellm/pull/38619)**。

2. **[#38610 [Bug]: /v1/messages stream answers 200 with message_start then SSE error on fallback failure](https://github.com/BerriAI/litellm/issues/38610)** — 新报，有fix
   当流式`/v1/messages`请求在内容到达前失败并触发fallback时，fallback流被转发，但若fallback也失败，客户端会先收到200 + `message_start`，随后才收到SSE错误块。这是协议语义错误，导致客户端难以正确处理。**已有修复PR：[#38623](https://github.com/BerriAI/litellm/pull/38623)** — 缓冲Anthropic fallback生命周期帧，仅在真实内容到达后转发，fallback失败时传播原始错误。

3. **[#38357 [Bug]: Bedrock handler never reads httpx.Response.headers — x-amzn-RequestId missing](https://github.com/BerriAI/litellm/issues/38357)** — 3天前报告，仍活跃
   Bedrock Converse/流式路径的`response._hidden_params["additional_headers"]`始终为空dict，导致AWS请求ID等原始响应头丢失。影响可观测性和调试能力，对需要审计AWS请求的用户尤为不便。

4. **[#38546 [Bug]: ocr_cost() does not account for annotation_cost_per_page](https://github.com/BerriAI/litellm/issues/38546)** — 新报
   `ocr_cost()` 只计算 `ocr_cost_per_page * pages_processed`，忽略了 `annotation_cost_per_page` 和 `pages_processed_annotation`。使用 `document_annotation_format` 调用OCR端点时（如Microsoft等供应商），成本计算不准确。

5. **[#38515 [Bug]: Zero-cost models are blocked once user's max_budget is exhausted](https://github.com/BerriAI/litellm/issues/38515)** — 新报
   定价为0成本的模型本应在用户预算耗尽后继续可用，但认证层在预算检查后直接拦截所有请求。对于使用免费模型作为fallback或用于系统维护请求的部署，这是一个需要关注的行为。

### 中低严重度

6. **[#38360 [Bug]: Model Settings update failed](https://github.com/BerriAI/litellm/issues/38360)** — 2天前报告
   修改"Model Name"并保存后显示成功消息，但刷新后更改不持久。

7. **[#38401 [Bug]: Bedrock Realtime acknowledges sessions before provider readiness](https://github.com/BerriAI/litellm/issues/38401)** — 新报
   Bedrock Nova Sonnet的`InvokeModelWithBidirectionalStream`在`/v1/realtime`路径上存在会话确认过早的问题，且对终态流失败缺乏处理。已被标记为潜在重复。

8. **[#38511 [Bug]: Responses streaming error handler crashes with AttributeError on completion-bridge iterator](https://github.com/BerriAI/litellm/issues/38511)** — 新报
   流式`/v1/responses`请求失败时，错误处理器本身崩溃（`'LiteLLMCompletionStreamingIterator' object has no attribute 'completed_response'`），导致客户端只看到处理器的AttributeError而看不到原始错误。

### 今日已关闭的 Bug（部分）

- [#15519 DB exception in update_spend job](https://github.com/BerriAI/litellm/issues/15519) — 已关闭
- [#32484 Unexpected log messages about unresolved cost with Docker 1.90.0](https://github.com/BerriAI/litellm/issues/32484) — 已关闭
- [#27671 Responses API streaming bridge multi-step tool calls text-delta ID issue](https://github.com/BerriAI/litellm/issues/27671) — 已关闭
- [#28530 Ollama Gemma 4 Infinite Tool Loop](https://github.com/BerriAI/litellm/issues/28530) — 已关闭
- [#28527 BYOK for non-OpenAPI spec MCP missing in UI](https://github.com/BerriAI/litellm/issues/28527) — 已关闭

## 6. 功能请求与路线图信号

### 可能被纳入下一版本的功能（已有对应PR）

1. **GLM-5.3-Flash 模型定价**（[#38608](https://github.com/BerriAI/litellm/issues/38608) → [#38627](https://github.com/BerriAI/litellm/pull/38627)）
   用户请求在`model_prices_and_context_window.json`中添加`zai/glm-5.3-flash`定价。PR已提交，定价为Input $0.15/1M、Output $0.50/1M、缓存Input $0.03/1M。快速响应体现了社区驱动的模型支持机制运行良好。

2. **Volcengine Seed 2.1 旗舰模型支持**（[#38516](https://github.com/BerriAI/litellm/pull/38516)）
   添加`volcengine/doubao-seed-2-1-pro-260628`和`volcengine/doubao-seed-2-1-turbo-260628`两个新模型到成本映射表。

3. **Auto-router自定义层级**（[#38603](https://github.com/BerriAI/litellm/pull/38603)）
   自动路由器UI

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 · 2026-08-28

---

## 1. 今日速览

Temporal 核心仓库今日处于**高活跃度**状态：过去 24 小时内 Pull Request 更新达 81 条，其中 33 条已合并/关闭，48 条仍在待合并队列中，显示出密集的工程交付节奏。Issue 侧新增 2 条（均为 OPEN），暂无版本发布。今日合入内容集中在 **CHASM/System Nexus 可靠性修复**与**测试基建复位**方面；新提交的 PR 则覆盖了**工作流调度器关键路径上的数据竞争与 backoff 累积 Bug**、**cron 参数校验前移**以及**慢请求日志可观测性增强**。值得关注的是，新 Issue #11842 报告的 Worker Deployment 路由配置状态卡死问题直接触及部署安全边界，建议高优先级跟踪。

---

## 2. 版本发布

**无新版本 Release。**

（注：PR #11801 以 `release/1.32.0` 为基干分支，提示 1.32.0 仍在积极收尾中，相关修复可能随该版本发布。）

---

## 3. 项目进展

过去 24 小时内合并/关闭的 33 条 PR 中，以下合入内容对项目推进有明显价值：

| PR | 标题 | 关注点 |
|----|------|--------|
| [#11820](https://github.com/temporalio/temporal/pull/11820) | [reliability-2026] Fix Nexus start-operation retry classification for wrapped service errors | 修复 Nexus 操作启动时对包装服务错误的错误分类，防止重试策略失效 |
| [#11818](https://github.com/temporalio/temporal/pull/11818) | Re-enable BUFFER_ONE backfill test; drop unsupported memo-only test | 测试框架恢复：重新启用 BUFFER_ONE 回填测试并清理不支持的无意义测试用例 |

同时，**48 条待合并 PR** 中有多条具备高落地价值，只要完成 review 即可显著提升系统健壮性：

- **#11843** —— 将 cron 校验从 frontend handler 前移到共享 `RequestValidator`，为 CHASM/System Nexus 提供校验能力，直接修复 #11822。
- **#11839** —— 修复 ContinueAsNew 时 `FirstWorkflowTaskBackoff` 持续累积的问题，该 Bug 会导致工作流在特定时序下不断推迟调度。
- **#11841** —— 修复 worker 关闭竞态：轮询注册与关闭检查的顺序问题，正确实现为“先注册再检查关闭标志”，防止关闭请求错过正在启动的 poll。
- **#11825** —— 修复 `perNamespaceWorker` 初始化阶段的 data race，动态配置回调可能在 `ns` 字段初始化前触发造成 nil 解引用。
- **#11801** —— 修复 Visibility SQL 查询转换器的三个解析问题（枚举元组、负数值、布尔类型误比较），属于查询兼容性修复。

项目整体处于**可靠性加固阶段**：以 `reliability-2026` 为标签的修复持续批量涌入，覆盖复制路径、任务队列、Nexus 执行器、指标埋点与查询层，工程质量信号积极。

---

## 4. 社区热点

今日 Issue 与 PR 评论数整体偏低（多数为 0 或未统计），但以下条目存在明显的诉求信号：

- **[#11842 Worker Deployment routingConfigUpdateState 永久 IN_PROGRESS](https://github.com/temporalio/temporal/issues/11842)**（新开，0 评论）  
  这是今日最值得关注的稳定性报告：用户 `@pnoker` 在将版本提升为 `current` 后，`routingConfigUpdateState` 始终无法从 `IN_PROGRESS` 转为 `COMPLETED`，导致任何 Worker 都无法确认路由，**每次发布（rollout）都被卡死**。该描述直指 Worker Deployment 特性在真实环境中的可用性缺口，虽刚创建尚无讨论，但严重性决定了其极可能获得高赞和快速响应。

- **[#11822 SignalWithStart 缺少 cron 校验](https://github.com/temporalio/temporal/issues/11822)**（新开，0 评论）  
  问题指出 SDK 内部通过 System Nexus 调用 `SignalWithStartWorkflowExecution` 时绕过了 Frontend 常规校验路径，导致非法 cron 表达式可被提交。**该 Issue 发布后 24 小时内即出现修复 PR #11843**，体现 Temporal 团队对 SDK 侧反馈的快速响应能力。

- **#11828 慢请求日志缺失 namespace 标签**（由 `claude[bot]` 提交，Slack 链路可见）  
  PR 来自 `@Yimin Chen` 的请求，指出慢请求 warning 日志中无法定位所属 namespace，显著增加线上排障成本。该诉求代表**可观测性精细化**的普遍需求，反映了大型部署环境下日志必须带上下文标签的强诉求。

---

## 5. Bug 与稳定性

按严重程度排序，过去 24 小时内暴露的 Bug 如下：

| 严重度 | Issue/PR | 说明 | 状态 |
|--------|----------|------|------|
| **P0（阻断发布）** | [#11842](https://github.com/temporalio/temporal/issues/11842) | Worker Deployment 路由配置更新永久卡在 IN_PROGRESS，导致所有 rollout 无法切换 current 版本 | 无 fix PR，新开待诊断 |
| **P1（高）** | [#11839](https://github.com/temporalio/temporal/pull/11839) | ContinueAsNew 叠加 executionTime 时 FirstWorkflowTaskBackoff 负向累积，引发调度周期无限推迟 | 已有 fix PR |
| **P1（高）** | [#11841](https://github.com/temporalio/temporal/pull/11841) | Worker 关闭流程竞态：poll 注册晚于 shutdown 缓存填充，极端情况下 poll 被遗漏，任务悬挂 | 已有 fix PR |
| **P1（高）** | [#11822](https://github.com/temporalio/temporal/issues/11822) | SignalWithStart（经 System Nexus）未校验 cron 表达式，非法字符串可直接被纳入调度 | 已有 fix PR #11843 |
| **P2（中）** | [#11825](https://github.com/temporalio/temporal/pull/11825) | perNamespaceWorker 初始化 data race，动态配置回调可能在字段初始化前触发 nil 访问 | 已有 fix PR |
| **P2（中）** | [#11801](https://github.com/temporalio/temporal/pull/11801) | Visibility SQL 查询转换器：IN 元组解析错误、负 double 解析失败、布尔比较误判 | 已有 fix PR（目标 1.32.0） |
| **P2（中）** | [#11774](https://github.com/temporalio/temporal/pull/11774) | SignalWithStart 在 Cassandra 遗留的孤立 current pointer 上挂起，超过 35 天仍未合并（issue #10841） | fix PR 于 8/25 提交，待 review |

**健康度评估**：核心调度路径今日集中暴露了数个并发/时序 Bug（#11839、#11841、#11825），且均已有修复 PR，反映团队在可靠性专项（reliability-2026）下主动挖掘深水区问题；但 #11842 作为新出现的 P0 级部署阻断问题，若无快速介入，将对 Worker Deployment 特性的生产可用性造成持续负面影响。

---

## 6. 功能请求与路线图信号

| 功能点 | 关联 PR/Issue | 说明 |
|--------|---------------|------|
| **Namespace 软删除** | [#10118](https://github.com/temporal

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*