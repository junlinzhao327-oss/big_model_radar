# OpenClaw 生态日报 2026-09-03

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-03 00:21 UTC

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



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-09-03

## 今日速览

过去 24 小时 LiteLLM 项目保持高强度迭代：共产生 84 条 Issue 更新（53 条活跃 / 31 条关闭）和 392 条 PR 更新（162 条已合并或关闭），并发布 2 个 Docker-only 版本。值得关注的是，v1.99.1 与 v1.97.1 均仅提供容器镜像而无 PyPI 包，提示发布流程可能正在围绕 Rust 重写进行重构。Rust 迁移母题（#31263）已持续近三个月并仍在活跃讨论，说明这是项目当前最重要的战略方向。同时，MCP 生态、Claude Code 集成、GPT-5.4/ChatGPT 订阅兼容性是社区反馈最集中的三个热点领域。整体判断：项目处于活跃演进期，但需警惕 PR 待合并队列长达 230 条带来的合流压力。

---

## 版本发布

### v1.99.1 — Docker-only release
- **发布时间**：2026-09-03（Git tag 与 Release 用于镜像到精确 commit 的可追溯性）
- **核心变更**：容器镜像专属版本，**无 PyPI 包**
- **迁移注意**：`pip install litellm==1.99.1` 不会解析成功，PyPI 用户应继续停留在 v1.99.0；需要使用新镜像的用户直接从容器仓库拉取对应 tag

### v1.97.1 — Docker-only release
- **发布时间**：2026-09-03（同样的 Docker-only 发布模式）
- **核心变更**：容器镜像专属版本，**无 PyPI 包**
- **迁移注意**：PyPI 用户应停留 v1.97.0；如需新镜像请直接拉取容器 tag

> ⚠️ **分析师注**：连续两个补丁版本均跳过 PyPI、仅发布 Docker 镜像，推测与 1.99.0-rc2 UI bug 批次（#39436）的验证节奏或 Rust 网关的镜像分发策略相关。建议关注 PyPI 通道何时恢复。</br> 链接：[v1.99.1](https://github.com/BerriAI/litellm/releases/tag/v1.99.1) · [v1.97.1](https://github.com/BerriAI/litellm/releases/tag/v1.97.1)

---

## 项目进展

本周合并/关闭的 162 条 PR 中有 31 条 Issue 被关闭（其中不少是带 `stale` 标签的老问题），维护者正在系统性地清理历史积压。从今日活跃的 PR 内容可以看出项目正沿以下方向推进：

### 1. Rust 迁移开始补测试基建
PR [#39440](https://github.com/BerriAI/litellm/pull/39440) 为网关新增了 `gateway_trace` 测试，与 litellm-rust crates 形成 1:1 映射。这说明 Rust 网关不仅在做功能迁移，测试对齐也在同步推进，是衡量迁移进度的关键信号。

### 2. xAI 计费逻辑修正
PR [#39441](https://github.com/BerriAI/litellm/pull/39441) 改为直接采用 xAI 上报的账单金额，而非 LiteLLM 根据 token 自行重算——特别针对服务端工具调用（server-side tools）等问题场景。这是对社区长期反馈的响应式修复。

### 3. MCP 功能与安全修复批量合入
- [#39446](https://github.com/BerriAI/litellm/pull/39446) 修复 MCP token exchange / ID-JAG 流程中误将 LiteLLM 虚拟密钥作为上游 subject token 外发的安全隐患；
- [#39234](https://github.com/BerriAI/litellm/pull/39234) 修复 agent-bound key 访问 MCP 服务器时静默返回空工具列表（HTTP 200 无报错）的问题，并在 Admin UI 中补全 agent MCP 授权管理；
- [#35142](https://github.com/BerriAI/litellm/pull/35142) 让 `pre_mcp_call` guardrail 真正扫描 MCP 工具参数。

### 4. 稳定性修复
- [#39443](https://github.com/BerriAI/litellm/pull/39443) 修复 `force_ipv4: true` 时忽略 `HTTP(S)_PROXY` / `NO_PROXY` 环境变量的问题；
- [#39411](https://github.com/BerriAI/litellm/pull/39411) 修复 Bearer-token 配置下 Bedrock 仍需走 SigV4 凭证链导致 500 报错的问题；
- [#39436](https://github.com/BerriAI/litellm/pull/39436) 集中修复 1.99.0-rc2 的 UI bug（空 org 导致 key 创建 500、会话分页错误、access group 重命名/删除问题等）；
- [#39366](https://github.com/BerriAI/litellm/pull/39366)（已关闭）修复 guardrail 在后端 `namespace` 工具时将其扁平化为 `ns__member` 导致 Codex 调用失败的问题。

### 5. 可观测性增强
PR [#39402](https://github.com/BerriAI/litellm/pull/39402) 为 Datadog LLM Obs 添加了成本标签维度、路由决策字段（auto-router 决策在 Datadog 中可见）、reasoning token 指标和脱敏门控，补全了企业级观测能力。

---

## 社区热点

### #31263 — LiteLLM Rust Migration（🔥 24 条评论 · 19 👍）
> Rust 迁移母题。用户持续就 sub-1ms 开销、迁移进展、Beta 测试提问。该 Issue 自 2026-06-25 创建至今已近三个月，仍保持社区关注度第一，且 PR [#39440](https://github.com/BerriAI/litellm/pull/39440) 表明迁移仍在稳步推进。
> 链接：https://github.com/BerriAI/litellm/issues/31263

### #25429 — GPT-5.4 空输出问题（💬 21 条评论 · 5 👍）
> 使用 ChatGPT 订阅账号通过 `litellm.responses()` 调用 `chatgpt/gpt-5.4` 时返回空 output 且 completion bridge 报错。从评论数量看影响面较大，且与 #26179 很可能同源（同为 gpt-5.4 经 litellm.responses 返回空 output）。表明 ChatGPT 订阅渠道的兼容性问题仍未彻底解决。
> 链接：https://github.com/BerriAI/litellm/issues/25429

### #37031 — MCP auto-execute 劫持 Claude Code 工具调用（💬 11 条评论）
> 新近出现且讨论快速升温的问题：MCP 工具配置 `require_approval: "never"` 后，代理端 auto-execute 逻辑会“劫持”Claude Code 等 agentic 客户端自带工具（Read/Bash/Edit），最终导致非 MCP 工具全部报 `Error executing tool`。这表明 MCP 自动执行与客户端原生工具之间的优先级规则存在设计缺陷。
> 链接：https://github.com/BerriAI/litellm/issues/37031

### #20495 — MCP OAuth 流程缺陷（💬 10 条评论 · stale 标签）
> 2 月创建的老问题，临时 OAuth server 未继承 MCP 服务器的 `authorization_url` 和 `token_url` 配置。评论数不少但长期未修复且已被标记 stale——社区多次遇到此问题但缺少维护者确认。
> 链接：https://github.com/BerriAI/litellm/issues/20495

### #23156 — GPT-5.4 工具调用 + reasoning_effort 失败（4 条评论 · 8 👍）
> 高赞低评论，说明很多人遇到了同样的问题但不想重复补充细节。openai-agents SDK + GPT-5.4 + `reasoning_effort` 的组合在工具调用时崩溃。
> 链接：https://github.com/BerriAI/litellm/issues/23156

---

## Bug 与稳定性

### 🔴 高危

| 严重度 | Issue/PR | 描述 | 状态 |
|--------|----------|------|------|
| **安全** | [#39446](https://github.com/BerriAI/litellm/pull/39446) | MCP token exchange 流程将 LiteLLM 虚拟密钥作为上游 subject token 外发至客户 IdP | ✅ 已有修复 PR（open） |
| **安全** | [#37031](https://github.com/BerriAI/litellm/issues/37031) | MCP auto-execute 劫持客户端工具导致 Claude Code 工具链断裂 | ⚠️ 尚无修复 PR |
| **兼容性** | [#38202](https://github.com/BerriAI/litellm/issues/38202) | LiteLLM 与 Python 3.10 不兼容（多个问题叠加），社区已有详细汇总 | ⚠️ 尚无修复 PR |
| **功能性** | [#38689](https://github.com/BerriAI/litellm/issues/38689) | Anthropic /v1/messages 流式请求出现间歇性 ~16

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-09-03

## 1. 今日速览

过去 24 小时 Temporal 核心仓库呈现典型的“高代码产出、低用户互动”状态：PR 更新量达 72 条，其中合并/关闭 27 条、待合并 45 条，分布在 `reliability-2026`、`team/cgs-foundation`、`oss-foundations` 及 `worker-callbacks` 功能分支等多条线上；相比之下 Issue 侧仅 2 条更新且均未关闭。最值得关注的是一个会导致 Worker Deployment 路由配置永久卡在 `IN_PROGRESS`、阻断所有 rollout 的严重问题（#11842），目前正在讨论中但尚无对应 fix PR。总体而言项目在复制一致性、子工作流恢复、可观测性与 Worker 回调功能上的推进力度显著，核心服务稳定性仍是关注重点，维护者响应速度较快。

## 2. 版本发布

过去 24 小时内无新版本 Release。

## 3. 项目进展

今日合并/关闭的 PR 主要集中在子工作流一致性、可见性存储优化和复制正确性修复方向。值得注意的合并项包括：

- **子工作流孤儿替换机制落地**（[#11815](https://github.com/temporalio/temporal/pull/11815)，已合并）：强化了 force failover 后无 worker 推进的孤儿子工作流处理，通过请求级 `OrphanedChildReplacementInfo` 携带父分支版本历史作为证据，允许在冲突时原子性地终止孤儿运行并创建替代，属于 CGS（Cross-cluster/Global replication 相关）基础能力的关键拼图。
- **修复晚到复制后子工作流完成恢复**（[#11868](https://github.com/temporalio/temporal/pull/11868)，已合并）：当活动父流程从延迟复制中重新生成 `StartChildExecution` 任务时，若发现子流程已关闭，现在会通过 Workflow ID 解析子流程当前运行并校验其属于预期的执行链，修复了父流程无法正确恢复完成状态的路径。
- **PostgreSQL 可见性 schema v1.14 升级脚本优化**（[#11599](https://github.com/temporalio/temporal/pull/11599)，已合并）：将此前合并的优化（#10371）同步应用到 v1.14 升级路径，降低升级耗时，已同步至 `release/1.31.3` 与 `release/1.32.0`。 
- **Visibility 分页查询日期时间格式统一**（[#11619](https://github.com/temporalio/temporal/pull/11619)，已合并至 `cloud/v1.32.0-161`）：Elasticsearch 分页过滤器中的 datetime 格式固定为包含纳秒分量，避免因精度差异导致的漏数据或重复数据。

这些合并共同推进了复制流隔离、子工作流生命周期一致性与可见性存储稳定性；与此同时，Worker-variant callbacks 系列 PR（见下）仍在功能分支中活跃迭代，并未直接合入 main，说明该功能仍处于早期整合阶段。

## 4. 社区热点

24 小时内 Issue 侧活跃度较低的背景下，热点主要围绕具体故障讨论与长期搁置需求的重启：

- **Worker Deployment routing config 永久卡死**（[#11842](https://github.com/temporalio/temporal/issues/11842)，作者 @pnoker）：该 issue 虽然是 8 月 28 日创建，但过去 24 小时仍有 2 条新评论，是最受关注的讨论。用户报告当 workflow 与 activity task queue 无法成为 current 时，每一次 rollout 都会卡死。由于评论内容未公开，无法得知 maintainer 的具体回应，但从开放状态和无关联 fix PR 来看，该问题仍在定位中。
- **Elastic Serverless 支持请求被重新激活**（[#6253](https://github.com/temporalio/temporal/issues/6253)，作者 @thegedge）：这条 2024 年 7 月的功能请求在昨日获得了一条新评论（评论内容未披露）。该请求讨论的是将 Elastic Serverless 用于 Visibility store，需要支持 `Authorization` 头的自定义配置。此类长期积压的请求被"顶起"，通常意味着有更多用户遇到了相同痛点，值得维护者重新评估优先级。
- **高讨论度 PR 背后是功能方向性选择**：在 PR 侧，@chrsmith 的 worker-callbacks 系列（[#11589](https://github.com/temporalio/temporal/pull/11589)、[#11520](https://github.com/temporalio/temporal/pull/11520)、[#11380](https://github.com/temporalio/temporal/pull/11380) 等 6 条）是最大的 PR 簇，虽然评论数未在元数据中体现，但其"stacked PR set"的规模表明该特性正处于攻坚阶段。此外 [#11909](https://github.com/temporalio/temporal/pull/11909)（改进 poller 伸缩信号，目前为 WIP）展示了社区通过动态配置优化资源利用率的关注。

今日社区诉求的共性是：**用户在意的不是新功能的数量，而是 rollout 能否顺利推行、以及基础设施能否适配云厂商的托管服务形态（如 Elastic Serverless）**。

## 5. Bug 与稳定性

按严重程度排列：

- **Critical — Worker Deployment 路由配置永久 `IN_PROGRESS`**（[#11842](https://github.com/temporalio/temporal/issues/11842)）：受影响环境无法将任何新 build 提升为 current，且 `DescribeWorkerDeployment.routingConfigUpdateState` 永远无法达到 `COMPLETED`。该问题会"wedging every rollout"，即阻断所有部署发布。目前无对应 fix PR，修复进展待关注。
- **Major — workflow update 复制时 UpdateCount 被额外自增**（[PR #11911](https://github.com/temporalio/temporal/pull/11911)，作者 @xwduan）：当复制插入 `UpdateInfo` 条目到 mutable state 时，UpdateCount 被多加了一次，导致源/目标计数不一致。修复 PR 已提交并扩展了 mutation/snapshot 复制测试，属数据一致性 bug，风险等级高，合并优先级应靠前。
- **Major — SignalWithStart 在孤儿 current-execution 指针上挂起**（[#11774](https://github.com/temporalio/temporal/pull/11774)，Fixes [#10841](https://github.com/temporalio/temporal/issues/10841)）：Cassandra 可能残留 current_executions 指针指向已完成的 workflow，新 SignalWithStart 请求遇到该指针时会 hang。PR 提出的修复方案为在 BrandNew 冲突且当前行是 completed 状态时以 `UpdateCurrent` 行为覆盖，与 StartWorkflow 的既有恢复逻辑对齐。该 PR 自 8 月 25 日起仍开放待合并。
- **Minor — SignalWithStart 未在请求校验阶段验证 cron 表达式**（[#11843](https://github.com/temporalio/temporal/pull/11843)，Fixes [#11822](https://github.com/temporalio/temporal/issues/11822)）：该校验目前在 frontend handler 中执行，PR 将其移至共享的 `RequestValidator.ValidateSignalWithStartRequest`，使 System Nexus/CHASM 也能够获得校验能力。属修复型增强，风险低。
- **Minor — "system payload" 判定有误**（[#11906](https://github.com/temporalio/temporal/pull/11906)，作者 @chrsmith）：作者本人对修复方向表示不确定，需要领域专家仔细 review。该 PR 牵涉 System Nexus Endpoint 对 system payload 的当前需求定义，若不修正可能产生误报。

## 6. 功能请求与路线图信号

- **Worker-variant callbacks（功能系列）**：从 [#11589](https://github.com/temporalio/temporal/pull/11589)（Worker callbacks 总实现）到 [#11520](https://github.com/temporalio/temporal/pull/11520)（填充 CallbackInfo.outcome）、[#11566](https://github.com/temporalio/temporal/pull/11566)（将支持的 callback 类型做成可配置）、[#11567](https://github.com/temporalio/temporal/pull/11567)（SANOs 支持完成回调）以及 [#11380](https://github.com/temporalio/temporal/pull/11380)（识别 `commonpb.NexusHandler` callback 变体），这是一个完整的跨版本功能形态。当前全部停留在 `feature/worker-callbacks` 分支，短期内不会进入 main，但其架构方向清晰——callback 机制将兼容 Nexus 与 worker 执行两种变体，且支持按部署配置开关。
- **复制流 namespace 隔离（5-PR 系列）**：[#11304](https://github.com/temporalio/temporal/pull/11304)（isolation manager）为该系列的 Part 4，其前置 Part 3（#11303 lane protocol）已合入 main。该 PR 从 7 月 27 日开放至今已超过一个月仍未合入，可能受 Part 5（sender isolation）依赖影响。整体方向是让复制流具备更细粒度的 namespace 级隔离能力。
- **改进 poller 伸缩信号（动态配置）**：[#11909](https://github.com/temporalio/temporal/pull/11909)（WIP）在 @kannanjgithub 原始提交基础上由 @veeral-patel 清理后重新提交。该功能将改善 task queue 的 poller 弹性伸缩，对高负载场景的资源利用率有实际意义。
- **Elastic Serverless 作为 Visibility store**（[#6253](https://github.com/temporalio/temporal/issues/6253)）：仍无对应实现 PR。鉴于 Elastic Serverless 形态已推出两年有余，且新评论再次出现，该功能于下一版本纳入的可能性在上升。

## 7. 用户反馈摘要

基于 Issues 及 PR 描述中的可读信息，今日主要用户声音如下：

- **Rollout 流程的脆弱性是最大痛点**（来自 [#11842](https://github.com/temporalio/temporal/issues/11842)）：用户 @pnoker 汇报的场景描述了从 `SetWorkerDeploymentCurrentVersion` 到 routingConfigUpdateState 完成之间的链路会无限期卡死。深层诉求是：**Worker Deployment 的当前版本提升应是一个可以在秒级完成、且结果可预期（COMPLETED/FAILED）的操作**。若中间态永远无法收敛，任何自动化发布系统都无法可靠工作。该用户的环境里 workflow 与 activity task queue 同时受影响，说明不是某一个队列的偶发问题，而可能是全局状态机缺陷。
- **云厂商托管服务适配需求浮现**（来自 [#6253](https://github.com/temporalio/temporal/issues/6253)）：Temporal 用户希望把 Visibility 存储在 Elastic Serverless 上，以降低自管理 Elasticsearch 的运维成本。目前的阻碍是不能为 search attributes 客户端设置 `Authorization` 头。这是"Temporal 部署上云"趋势下的普遍诉求——用户期望存储层可以无缝对接各大云厂商的 serverless 产品。
- **开发者自查反馈建设性意见**（来自 [#11906](https://github.com/temporalio/temporal/pull/11906)）：PR 作者 @chrsmith 在描述中敞明自己对该领域不熟悉，请求审阅者严格把关，并对自己提出的修复方向表示不确定、甚至提出"或者我们只需放宽 system payload 约束即可"的替代方案。这种诚实标注"请帮助我确认"的协作风格有助于提升 code review 质量。

## 8. 待处理积压

- **Elastic Serverless 支持（Issue #6253）积压已超两年**：自 2024 年 7 月 8 日创建至今仍未关闭，且在 2026-09-02 才再度获得评论。考虑到 Elastic 官方已将 Serverless 作为主推形态，建议维护者确认此请求是否仍在路线图中——若否，应明确关闭并给出替代方案（如使用 Elastic Cloud 传统部署 + VPC 私网连接）。
- **复制隔离系列 Part 4（PR #11304）在 main 上停留时间过长**：已开放 38 天。前置依赖（#11303）已于更早时间合并，该 PR 目前为独立状态仍无法合入，需维护者跟进 Part 5 的进度或对 Part 4 进行单独 review/merge，避免大 diff 累积导致合并成本越来越高。
- **SignalWithStart 孤儿指针修复（PR #11774）处于待合并状态达 9 天**：它修复的是一个会导致 API 永久 hang 的 Cassandra 遗留问题（#10841），但至今未合入。若有明确关联版本计划（如排队等 1.33 窗口），建议在 PR 中注明目标版本，否则建议优先合入，以免真实用户在生产环境继续触发该问题。
- **@chrsmith 的六个 worker-callbacks PR 中，最老的（#11380）从 7 月 31 日起已开放 34 天**，尽管它们明确声明将合入功能分支而非 main，仍建议维护者关注整个 PR set 的进度，避免长期挂起导致 rebase 负担越来越重，且阻塞后续依赖该功能的用户侧开发计划。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*