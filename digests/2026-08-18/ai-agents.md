# OpenClaw 生态日报 2026-08-18

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-17 22:35 UTC

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

# OpenHands SDK 项目动态日报 — 2026-08-18

## 1. 今日速览

- 项目保持高活跃度：过去24小时 5 条 Issue 更新，19 条 PR 更新，其中 14 条待合并、5 条已合并/关闭，无新版本发布。核心维护者与外部贡献者并行的开发节奏稳定，多集中在 LLM 集成（subscription 认证、缓存命中、模型选择器）与工作区后端扩展（Kubernetes）两条主线上。
- 值得关注的是两个标记 `priority:high`、`release-note-required` 的 Bug（#4515、#4514）均在同日获得了对应修复/测试 PR（#4517、#4513），问题响应速度很快。
- 功能请求与 PR 的高度配对（如 #4519→#4516、#4452→#4496）说明路线图上的功能正在被快速落地，而非停留在讨论阶段。
- 依赖维护（Pillow、MCP SDK bump）和安全修复（API key 脱敏）也在持续推进，总体项目健康度良好。

## 2. 版本发布

过去24小时无新版本发布。项目当前处于功能迭代叠加期，下一次版本发布可能会包含下列已合并/关闭的 PR 中的内容。

## 3. 项目进展

过去24小时有 5 条 PR 已合并/关闭，其中值得关注的有：

- **[#4440] fix(agent-server): base_state.json 作为 agent 唯一状态来源（消除 meta.json 重复）** — 由 @enyst 提交。这是 agent-server 持久化层的一次根因级修复：此前 `base_state.json` 与 `meta.json` 同时保存对话状态，存在"双源真相"导致的状态漂移风险。该修复将状态收敛到单一文件，是稳定性方向的架构改进。
  https://github.com/OpenHands/software-agent-sdk/pull/4440

- **[#3503] feat: 为 AgentSettingsBase 添加公开的 from_persisted() 入口点** — 由 @mvanhorn 提交。该 PR 为各 settings 变体增加统一的反序列化入口，并已针对 legacy v0/v1/v2 载荷完成测试。对依赖持久化设置的迁移路径和向后兼容有直接帮助。
  https://github.com/OpenHands/software-agent-sdk/pull/3503

- **[#4465] fix: 将任务结果（task outcome）附加到 finish tool** — 由 @malhotra5 提交，并带 `run-eval-50` 标签（意味着该修复经过了 50 次评估回归验证）。修复了 finish tool 缺少任务最终结果的问题，对下游评估和可观测性有实际价值。
  https://github.com/OpenHands/software-agent-sdk/pull/4465

- **[#4506] fix: 从 validate_profile 错误响应和日志中脱敏 API Key** — 由 @all-hands-bot 提交。这是一个安全修复：API key 可能出现在 `validate_profile` 的报错信息中，现已被脱敏，防止凭据泄漏到日志或终端。
  https://github.com/OpenHands/software-agent-sdk/pull/4506

另有依赖升级 PR（#4347，MCP SDK 1.26.0→1.28.1）在列。总体而言，今日合并项以内部稳定性和安全加固为主，没有引入新的破坏性变更。

## 4. 社区热点

今日讨论最活跃的是以下 Issue：

- **[#4452] Agent Plugins: client extension namespace mapping**（2 条评论，👍 0）— 关于如何将 OpenHands 的 Claude-Code-origin 概念（`commands/`、`agents/`、`hooks/hooks.json`、`entry_command`）映射到自有反域名客户端扩展命名空间下（spec §8）。讨论核心是命名空间到底用 `io.openhands` 还是 `dev.openhands`，目前被 #4405 的 Open Question #2 阻塞。该讨论决定了插件生态的"地址体系"，对后续开发者接入方式影响深远。
  https://github.com/OpenHands/software-agent-sdk/issues/4452

- **[#4515] Condenser disabled for subscription LLMs**（1 条评论）— 这个高优 bug 引起了较多关注，因为它影响的是使用 ChatGPT/Codes subscription 认证的真实用户：上下文超限后压缩逻辑不触发，导致对话直接失败。已有一个修复 PR #4517 带着根因分析（`completion()` 调用使用了错误的 API 端点）提交，讨论热度可能推动其快速合入。
  https://github.com/OpenHands/software-agent-sdk/issues/4515

- **[#4519] Kubernetes-backed workspace**（1 条评论）— 社区对 K8s 后端的诉求清晰：已在 K8s 上运行团队不想被迫引入 Docker 或托管运行时。该需求与 PR #4516 配对，说明维护者已认可方向。
  https://github.com/OpenHands/software-agent-sdk/issues/4519

## 5. Bug 与稳定性

按严重程度排列：

**高优先级（有对应修复 PR，但尚未合入）**

- **[#4515] Condenser disabled for subscription LLMs — context compression never fires**（`priority:high, release-note-required`）— subscription 认证下上下文压缩永不触发，最终导致 `ContextWindowExceededError`。根因是 condenser 调用了错误的 API 端点（`completion()` 而非 subscription 兼容端点）。修复 PR：#4517（@neubig）通过统一 `complete()` 分发解决。
  https://github.com/OpenHands/software-agent-sdk/issues/4515
  https://github.com/OpenHands/software-agent-sdk/pull/4517

- **[#4514] Lifecycle lock deadlock: thread-pool exhaustion blocks all event loading**（`priority:high, release-note-required`）— `_get_or_load_event_service` 在 `lifecycle_lock` 内调用 `asyncio.to_thread()`，默认线程池耗尽后会无限排队，进而阻塞所有事件加载。这是一个严重的并发缺陷，可能导致 Conversation 服务整体不可用。已有一份带复现的测试 PR：#4513（@neubig），第二 commit 包含修复。
  https://github.com/OpenHands/software-agent-sdk/issues/4514
  https://github.com/OpenHands/software-agent-sdk/pull/4513

**低优先级**

- **[#4520] `parse_extension_source` 在 GitHub shorthand 中重复追加 `.git` 后缀**（`priority:low`）— 当用户输入已经带 `.git` 后缀的 `github:owner/repo.git` 时，解析结果变为 `owner/repo.git.git`。这是一个确定性小 bug，社区已有回应，暂无单独修复 PR（可能作为 quick fix 合入）。
  https://github.com/OpenHands/software-agent-sdk/issues/4520

## 6. 功能请求与路线图信号

- **Kubernetes 工作区后端的落地** — Issue #4519（Kubernetes-backed workspace using kubernetes-sigs/agent-sandbox）与 PR #4516（`AgentSandboxWorkspace`，已在 kind 和 GKE 上端到端验证）配对出现。PR 显示已与 agent-sandbox 维护者沟通过，较大概率进入下个版本，将成为既 Docker、hosted runtime API、OpenHands Cloud、Apptainer 之后的第五种工作区后端。
  https://github.com/OpenHands/software-agent-sdk/issues/4519
  https://github.com/OpenHands/software-agent-sdk/pull/4516

- **插件客户端扩展命名空间确定** — #4452 是未来插件生态的基础设计决策，目前有对应 PR #4496（dev.openhands 命名空间映射）。虽然 issue 还处于设计讨论阶段（被 #4405 阻塞），但从 PR 已提交来看，`dev.openhands` 方向大概率被采纳。这将是 SDK 插件系统正式对外 API 的一部分。
  https://github.com/OpenHands/software-agent-sdk/issues/4452
  https://github.com/OpenHands/software-agent-sdk/pull/4496

- **LLM 连接方式的补充** — 两条独立 PR 指向同一方向：让 LLM 配置更灵活。PR #4492（@juanmichelini）添加 "read-at-use" LLM provider connections（刻意保持轻量、向后兼容）；PR #4510（@georgeglarson）为 task tool 增加 per-call `llm_profile` override，解决"主 agent 用 GPT 规划、子 agent 用 DeepSeek 执行"的混合模型工作流。这两项若合入，将显著增强多模型编排能力。
  https://github.com/OpenHands/software-agent-sdk/pull/4492
  https://github.com/OpenHands/software-agent-sdk/pull/4510

## 7. 用户反馈摘要

从今日 Issue 和 PR 的讨论中可提炼出以下真实用户声音：

- **订阅制 LLM 用户的挫败感（#4515）**：使用 ChatGPT subscription（如 `openai/gpt-5.6-sol`）的用户在长对话中遭遇上下文超限后直接报错，而不是自动压缩。这说明 SDK 对"非 API-key 认证"这类新型 LLM 接入方式支持不完整，且失败模式对最终用户不友好（不是降级而是硬失败）。
  https://github.com/OpenHands/software-agent-sdk/issues/4515

- **K8s 用户的部署偏好（#4519）**："Teams that already operate k8s" 不希望在容器运行时上被锁定，工作区应该与既有基础设施对齐。这与企业采用 Agent 平台时的"基础设施一致性"诉求一致。
  https://github.com/OpenHands/software-agent-sdk/issues/4519

- **Windows 端浏览器发现的现实问题（#4502）**：Windows 上浏览器后端发现失败被复现并修复（Playwright Chromium 优先 + 回退逻辑）。这是跨平台使用中典型的本地环境问题，社区用户主动完成了从调查、修复到验证的完整链路。
  https://github.com/OpenHands/software-agent-sdk/pull/4502

- **混合模型工作流被误切换（#4510）**：用户想用"GPT-5.6 规划、DeepSeek V4 Pro 执行"的编排，但因为 `enable_switch_llm_tool` 等默认设置，主 agent 把自己切换到了第二个模型而不是派生子 agent 执行。这类问题是多模型编排真实用户场景的典型痛点。
  https://github.com/OpenHands/software-agent-sdk/pull/4510

## 8. 待处理积压

- **[#3673] feat(sdk): add ask_oracle tool**（创建于 2026-06-11，已超过两个月，`integration-test, review-this` 标签）— 该 PR 为 agent 增加"遇到困难时咨询更强模型"的 capability（second opinion），在 LLM 分工日益复杂的当下有较强的实际价值。持续有更新（8月17日仍在活跃），但作为跨月 PR 建议维护者明确下一步：是补齐 integration test 还是准备合入。
  https://github.com/OpenHands/software-agent-sdk/pull/3673

- **[#4437] fix(acp): add claude-fable-5 to Claude Code model picker options**（创建于 2026-08-09，待合并中）— 修复 Claude Code 的 ACP 模型选择器缺少 `claude-fable-5` 选项的问题。PR 本身简单且已本地验证，优先级低但合入成本小，长期挂着容易积累技术债。
  https://github.com/OpenHands/software-agent-sdk/pull/4437

- 提醒关注 **

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 开源项目日报 2026-08-18

## 1. 今日速览

Temporal 项目今日保持高活跃度：24 小时内 3 个 issue 更新（全部处于开放状态），40 个 PR 更新（31 个待合并，9 个已合并/关闭），无新版本发布。项目重点集中在 reliability-2026 分支的稳定性修复与测试基础设施优化。最值得关注的是，团队针对 PostgreSQL visibility 升级性能问题（[#11594](https://github.com/temporalio/temporal/issues/11594)）在 24 小时内提交并关闭了修复 PR [#11599](https://github.com/temporalio/temporal/pull/11599)，展现了高效的 issue 响应能力。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日共有 9 个 PR 被合并/关闭，以下为关键条目：

- **[#11599 (closed): Optimize Visibility PostgreSQL upgrade schema v1.14](https://github.com/temporalio/temporal/pull/11599)** — 将 [#10371](https://github.com/temporalio/temporal/pull/10371) 的优化方案应用到 v1.14 版本升级脚本中，显著减少升级时的 rewrite 次数，直接修复 [#11594](https://github.com/temporalio/temporal/issues/11594) 报告的性能问题。
- **[#11581 (closed): Enable HTTP/2 keepalive on nexus and callback transports](https://github.com/temporalio/temporal/pull/11581)** — 为 outbound Nexus 操作和 callback 请求启用 HTTP/2 健康检查，避免静默连接断裂导致的请求失败，提升自愈能力。
- **[#11575 (closed): Release removed shared cluster test references](https://github.com/temporalio/temporal/pull/11575)** — 修复共享集群测试中 backing array 保留已完成测试状态导致的内存泄漏，提升

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*