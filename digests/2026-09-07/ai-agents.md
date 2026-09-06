# OpenClaw 生态日报 2026-09-07

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-06 22:35 UTC

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

# Pi 项目动态日报 — 2026-09-07

## 1. 今日速览

过去 24 小时 Pi 项目活跃度处于健康水平：Issues 处理速度快（38 条更新中 32 条已关闭，关闭率约 84%），PR 流转正常（18 条更新中 12 条进入合并/关闭流程）。今日无新版本发布，项目处于功能迭代与问题修复并行推进阶段。值得注意的是，社区提交的多个 PR 存在内容重复提交现象（如 #9248/#9249/#9251，以及 #9250/#9252），可能反映外部贡献者之间的沟通协作成本偏高。一个已经持续 3 个多月的高热度连接稳定性 Issue（#4945）仍然处于打开状态，是当前项目健康度的主要减分项。

## 2. 版本发布

无新版本发布（最新版本维持在 0.85.1）。相关快照请关注 Releases 页面：[https://github.com/earendil-works/pi/releases](https://github.com/earendil-works/pi/releases)

## 3. 项目进展

今日进入关闭流程的 PR 覆盖了若干值得关注的修复与功能：

- **Copilot GPT 模型路由修复**：[PR #9253](https://github.com/earendil-works/pi/pull/9253) — 将 Copilot GPT 模型统一路由到 Responses 端点，修复 `gpt-6-astra` 等模型无法通过 Chat Completions 访问的问题（对应 Issue #9209）。该 PR 同时移除了对 GitHub 目录中已不存在的 gpt4 模型的依赖，具备前瞻性。
- **DNS 解析修复**：[PR #9250](https://github.com/earendil-works/pi/pull/9250) / [PR #9252](https://github.com/earendil-works/pi/pull/9252，内容相同) — 将 undici 的 DNS 解析固定到 Node 系统 `dns.lookup`，修复 MagicDNS/分域 DNS 环境下 `ENOTFOUND` 报错（对应 Issue #9244）。
- **跨提供商故障转移**：[PR #9248](https://github.com/earendil-works/pi/pull/9248) / [PR #9249](https://github.com/earendil-works/pi/pull/9249) / [PR #9251](https://github.com/earendil-works/pi/pull/9251，内容相同) — 为 coding-agent 新增可选的跨提供商 fallback 能力：主提供商遇到传输/不可达错误时可自动切换至备用提供商，避免会话硬失败（对应 Issue #9242）。
- **认证状态动态解析**：[PR #9233](https://github.com/earendil-works/pi/pull/9233) — 修复模型解析依赖启动快照中认证状态的问题，改为实时解析，消除启动时后台刷新未完成导致的竞态。
- **OpenRouter `:free` 模型 maxTokens 修正**：[PR #9224](https://github.com/earendil-works/pi/pull/9224) — OpenRouter 免费模型在目录中常声明过大的上下文窗口，Pi 按目录值发送 max_tokens 会被上游拒绝；修复为按基础模型限制截断。
- **TUI 交互增强**：[PR #9080](https://github.com/earendil-works/pi/pull/9080) — 为 TUI 增加“跳转到最新消息”控件。
- **工具调用确认扩展**：[PR #9227](https://github.com/earendil-works/pi/pull/9227) — 增加 per-call 工具确认的扩展实现，对应 Issue #9228 的诉求。
- **UI 上下文封装修复**：[PR #9219](https://github.com/earendil-works/pi/pull/9219) — 修复 `wrapUIPromptContext` 使用对象展开导致 embedder 提供的 UI 上下文原型方法丢失的问题。

此外，值得注意 [#9250/#9252 与 #9248/#9249/#9251 两组重复 PR](https://github.com/earendil-works/pi/pulls)——同一位贡献者对同一问题提交了多份完全相同的 PR，建议维护者留意并清理，为后续贡献者保留清晰的 PR 基线。

## 4. 社区热点

- **[#4945 [OPEN] openai-codex Connection Reliability Issues](https://github.com/earendil-works/pi/issues/4945)** — 76 条评论 / 32 👍，是当前社区影响面最大、讨论最激烈的问题。用户连续数日遭遇 `gpt-5.5` 对话时 TUI 卡在 "Working..." 状态、无输出无错误、只能按 Escape 中断的故障。该 Issue 已打开 3 个多月，高点赞数说明大量用户遭遇同样问题。其背后诉求指向两端：一是对上游 OpenAI 连接稳定性的依赖，二是 TUI 对“无响应”状态缺少超时/自恢复机制。

- **[#7547 [OPEN] [Windows] How do you use Pi on windows? What issues are you seeing?](https://github.com/earendil-works/pi/issues/7547)** — 55 条评论。这是一条官方主动发起的 Windows 生态收集帖，用于摸清用户如何在 Windows 上使用 Pi、以便决定核心团队应在哪些方向投入。55 条回复反映出社区对 Windows 支持的高度关注，以及当前使用方式高度碎片化（WSL、原生、容器等）的现状。结合近期多条 Windows 专项 Issue（#9229、#9240 等），Pi 对 Windows 平台的支持可能正在进入系统化梳理与投入阶段。

## 5. Bug 与稳定性

按影响面与严重程度排列：

**高**
- **[#4945](https://github.com/earendil-works/pi/issues/4945)：openai-codex 连接可靠性问题（OPEN，76 评论）** — 用户反复出现 TUI 卡死在 "Working..."、无任何流式输出或错误提示，只能手动 Escape 中断。已持续数日/数月。目前尚无对应 fix PR。

**中**
- **[#9229](https://github.com/earendil-works/pi/issues/9229)：Windows 下 shell_path 配置被忽略（已关闭）** — 即使 WSL 功能已禁用且配置了 `shell_path`，Pi 仍优先使用 WSL bash。影响 Windows 用户的自定义 shell 体验。
- **[#9240](https://github.com/earendil-works/pi/issues/9240)：TUI 视口上方内容变更触发全量重绘导致滚动位置丢失（已关闭）** — 流式输出中如果视口上方的行发生变化（如 markdown 重排、思维块展开、工具调用更新），终端会跳到会话顶部，长时间任务中的阅读位置难以保持。
- **[#9209](https://github.com/earendil-works/pi/issues/9209)：Copilot GPT-6 Astra 被路由到不支持的 Chat Completions 端点（已关闭）** — 已由 [PR #9253](https://github.com/earendil-works/pi/pull/9253) 修复。

**低**
- **[#9245](https://github.com/earendil-works/pi/issues/9245)：`--api-key` 与 auth.json 的解析顺序不符合预期（已关闭）** — 用户使用 1Password CLI 引用作为 key 时，API Key 的解析优先级与直觉不符。
- **[#8306](https://github.com/earendil-works/pi/issues/8306)：全屏 TUI 图片渲染只有首行可见（已关闭）** — 由错误的刷新逻辑导致。
- **[#9165](https://github.com/earendil-works/pi/issues/9165)：Claude Opus 5 经 OpenRouter 时拒绝 per-message output_config（已关闭）** — 仅影响该模型经 OpenRouter 的场景，Anthropic 直连正常。

**其他**
- **[#9244](https://github.com/earendil-works/pi/issues/9244)：MagicDNS 风格域名解析失败（已关闭）** — 已有 [#9250](https://github.com/earendil-works/pi/pull/9250) / [#9252](https://github.com/earendil-works/pi/pull/9252) 修复 PR。

## 6. 功能请求与路线图信号

以下新提交/活跃的功能请求反映了社区对 Pi 平台化能力的持续期待：

- **模型覆盖与兼容性**
  - [Issue #9133](https://github.com/earendil-works/pi/issues/9133)：增加对 `gpt-6-astra` 的支持（其 Copilot 路由问题已由 PR #9253 覆盖）
  - [PR #6881](https://github.com/earendil-works/pi/pull/6881)：使用提供商上报的实际费用替代目录估算（已开放近 2 个月）
  - [PR #9096](https://github.com/earendil-works/pi/pull/9096)：新增 Meta provider 及 Muse 订阅 OAuth 支持（开放中）
  - [PR #7610](https://github.com/earendil-works/pi/pull/7610)：新增 LLM Gateway 及 DevPass 两个内置提供商（开放超 1 个月）

- **会话与可用性**
  - [Issue #9242](https://github.com/earendil-works/pi/issues/9242)：跨提供商故障转移链——已由 PR #9248/#9249/#9251 实现，预计进入下一版本
  - [Issue #8826](https://github.com/earendil-works/pi/issues/8826)：为编码代理的指数退避增加可配置上限，以应对长时间上游故障（OPEN）
  - [Issue #8617](https://github.com/earendil-works/pi/issues/8617)：Codex provider 对图片密集的工具结果使用文件引用而非 base64 回放（OPEN，作者已有原型）

- **扩展与集成能力**
  - [Issue #9236](https://github.com/earendil-works/pi/issues/9236)：提供带确认语义的用户消息投递 API（带幂等与可中断性，已关闭）
  - [Issue #9238](https://github.com/earendil-works/pi/issues/9238)：让扩展可在运行时切换 TUI 模式，并以布局列方式挂载（已关闭）
  - [Issue #9247](https://github.com/earendil-works/pi/issues/9247)：在 JSON/RPC 事件中暴露提供商原生的失败分类（已关闭）
  - [Issue #9254](https://github.com/earendil-works/pi/issues/9254)：让扩展可覆盖内置 UI 文案，以支持国际化（已关闭）

- **工程质量与依赖**
  - [Issue #9225](https://github.com/earendil-works/pi/issues/9225)：将 esbuild 从轻量运行时/上下文链路中解耦，减少 SDK 消费者的安装体积（已关闭）
  - [PR #9137](https://github.com/earendil-works/pi/pull/9137)：添加 Nix flake 支持（WIP）

整体信号：下一版本大概率会包含 Copilot 模型路由修正、跨提供商故障转移

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-09-07

## 1. 今日速览

过去 24 小时 Temporal 核心仓库活跃度中等偏上：无新 Issue 报告、无新版本发布，但 PR 侧保持 10 条更新，其中 9 条仍处于开放状态、1 条关闭。值得关注的是，@temporal-cicd[bot] 提交了 `1.32.0: Prepare release branch` 的 PR 并在同日被关闭，预示 1.32.0 发布流程已正式启动，项目正处在活跃开发与版本收口并行的阶段。当前 PR 积压以性能优化（6 条）为主，另有 CLI 工具增强、存储后端扩展和可观测性改进各 1-2 条，项目在"高性能与可运维性"两条主线上持续投入。

---

## 2. 版本发布

**无新版本发布。**

但有一条重要的版本流程信号：

- [#11946 [CLOSED] 1.32.0: Prepare release branch](https://github.com/temporalio/temporal/pull/11946) — 由 CI 机器人于 2026-09-06 提交的同日合并，内容为覆盖 governance 文件并更新依赖。这表明 **1.32.0 的 release branch 已经创建**，正式版本预计将在近期发布。

---

## 3. 项目进展

今日唯一关闭的 PR 是版本发布准备（见上），标志 1.32.0 进入发布倒计时阶段。其余 9 条 PR 虽未合并，但从近期更新活跃度看，多个核心方向取得实质推进：

- **动态配置调试工具链**（两条独立实现并行推进，功能高度重叠）：
  - [#11722 [OPEN] tdbg dynamic config describe, get, dump](https://github.com/temporalio/temporal/pull/11722) — 新增 `tdbg dc` 三个子命令，用于描述/读取/导出动态配置。
  - [#9948 [OPEN] Add command to dump dynamic configuration values](https://github.com/temporalio/temporal/pull/9948) — 类似功能，自 4 月搁置至今，两条 PR 如何整合需维护者决断。

- **高性能存储与持久化优化**（@mykaul 主导的一系列优化继续活跃更新）：
  - [#11804 Perf/lazy timer map](https://github.com/temporalio/temporal/pull/11804) — 避免每次加载 workflow 时急切反序列化整个 `timer_map`（10k+ 条目时可达 3.5MB、30k 次内存分配），改为延迟加载。对 timer-heavy 工作流的持久化性能影响显著。
  - [#11181 Replace MapScan with typed Scan in ScyllaDB/Cassandra](https://github.com/temporalio/temporal/pull/11181) — 消除逐行 map 分配开销。
  - [#11179 Cache getQueue result in QueueV2 EnqueueMessage path](https://github.com/temporalio/temporal/pull/11179) — 消除每次 EnqueueMessage 的额外 CQL round-trip。

- **Metrics 与 gRPC 路径优化**：
  - [#11301 sync.Map scope cache + sync.Pool metricsContext](https://github.com/temporalio/temporal/pull/11301) — 针对 metrics 路径约 26% CPU（GC）占比的分配压力优化。
  - [#11300 Cache resolved namespace names across interceptor chain](https://github.com/temporalio/temporal/pull/11300) — 消除每次调用 6-7 个拦截器中重复的 namespace 解析。

- **存储后端扩展与可观测性增强**：
  - [#11886 Amazon OpenSearch Serverless (AOSS) 支持](https://github.com/temporalio/temporal/pull/11886) — 使 Elasticsearch visibility store 可用于 AOSS，三项差异适配且默认向后兼容。
  - [#11927 Nexus completion callback 指标透传来源标签](https://github.com/temporalio/temporal/pull/11927) — 为 callback 指标增加 `nexus_completion_source` 标签。

**评估**：项目整体向前迈进主要体现在两处：1.32.0 版本线启动 + 性能优化 PR 群持续迭代更新。特别是 timer_map 延迟加载和 Cassandra Scan 优化若合入，将直接改善大规模工作流场景的稳定性与吞吐。但 PR 合并速度偏慢也是客观事实——多条 PR 打开时间已超过 6 周。

---

## 4. 社区热点

由于今日无 Issue 更新，且各 PR 的评论数未明确展示（均为 0 或未统计），"讨论热度"主要体现在多条 PR 在 09-06 当天仍在持续更新，说明作者与维护者之间有实质性的 review 往返。相对更受关注的方向集中在：

- **tdbg 动态配置命令（#11722 与 #9948）**：两条 PR 来自不同作者、功能高度重叠、且 #9948 比 #11722 早开 4 个月。这种重复 PR 的长期共存本身就反映了一个共同诉求：**运维人员迫切需要命令行工具来检查和调试动态配置**。
  - [#11722](https://github.com/temporalio/temporal/pull/11722)
  - [#9948](https://github.com/temporalio/temporal/pull/9948)

- **Amazon OpenSearch Serverless（AOSS）支持（#11886）**：这是来自外部贡献者 @ofir-blaus 的功能型 PR。AOSS 是 AWS 托管 OpenSearch 的无服务器形态，Temporal 用户中采用 AWS 生态的比例较高，此能力对 visibility 功能在 AOSS 上的落地有关键意义。
  - [#11886](https://github.com/temporalio/temporal/pull/11886)

**分析**：社区当前的隐性热点偏向**降低运维门槛**（动态配置可调试）与**拥抱托管服务生态**（AOSS），而非新功能探索。

---

## 5. Bug 与稳定性

今日无新报告的 Bug、崩溃或回归 Issue。

稳定性相关工作更多体现在 PR 侧：

- 低风险（无破坏性）：#11946 发布分支准备仅更新依赖和 governance 文件。
- 中低风险：AOSS 兼容（#11886）三项适配均默认关闭，不影响现有 Elasticsearch 用户。
- 需要关注但已有修复方向：@mykaul 的系列性能 PR 直指 ScyllaDB/Cassandra 在 timer-heavy、队列密集型场景下的 GC 压力和高延迟问题，虽非"已报 bug"，但属于预防性稳定性加固：
  - [#11804 Lazy timer map](https://github.com/temporalio/temporal/pull/11804)
  - [#11181 Typed Scan 替代 MapScan](https://github.com/temporalio/temporal/pull/11181)
  - [#11179 缓存 getQueue 结果](https://github.com/temporalio/temporal/pull/11179)

---

## 6. 功能请求与路线图信号

今日虽无新 Issue 提出功能请求，但从活跃 PR 可以清晰观察到以下路线图信号：

| 方向 | 信号 PR | 可能的版本归属 |
|---|---|---|
| CLI 工具（tdbg 动态配置操作） | [#11722](https://github.com/temporalio/temporal/pull/11722)、[#9948](https://github.com/temporalio/temporal/pull/9948) | 距离合入仍有整合工作，最早 1.32 或推迟至 1.33 |
| Amazon OpenSearch Serverless 支持 | [#11886](https://github.com/temporalio/temporal/pull/11886) | 若 review 顺利，可能进入 1.32 |
| Nexus callback 可观测性增强 | [#11927](https://github.com/temporalio/temporal/pull/11927) | 1.32（已开 4 天，改动量小，合并概率较高） |
| 性能优化系列 | #11301、#11300、#11804、#11181、#11179 | 系列若能在 1.32 窗口关闭前合入则随 1.32 发布，否则顺延 |

Nexus 相关 PR（#11927）虽然改动较小，但表明 Nexus 功能仍在持续打磨可观测性，说明 Temporal 团队在 Nexus 产品化上仍在持续投入。

---

## 7. 用户反馈摘要

今日无 Issue 讨论，因此没有直接的用户评论可用于提炼。但从 PR 的动机描述中可间接看出使用者的真实痛点：

- **动态配置调试困难**：#9948 的作者（外部贡献者 @vaibhavyadav-dev）明确提出 "make it easier to inspect dynamic config values directly from CLI"，这是运维侧诉求的直接反馈。
- **大规模工作流持久化成本高**：#11804 提到 ScyllaDB 的 `timer_map` 在 timer-heavy 工作流中可膨胀至 10k+ 条目（约 157KB），每次加载即产生 3.5MB 临时对象和 30k 次分配。该 PR 提交者虽为维护者，但这无疑来自真实生产环境观测。
- **EnqueueMessage 吞吐瓶颈**：#11179 暴露了每次 EnqueueMessage 都需要一次额外的 CQL round-trip 验证队列元数据，这种"隐藏的读放大"影响队列写入吞吐。
- **AOSS 用户的 visibility 功能受阻**：#11886 的三项阻塞性差异意味着当前 AOSS 用户无法直接使用 Temporal 的 Elasticsearch visibility 功能，社区存在明确的使用需求。

---

## 8. 待处理积压

以下 PR 长期未合并或未关闭，建议维护者关注：

| PR | 打开时长* | 状态风险 | 说明 |
|---|---|---|---|
| [#9948 tdbg dump dynamic config](https://github.com/temporalio/temporal/pull/9948) | 约 4 个月 24 天 | 🔴 高 | 4 月 14 日创建后长期搁置；与 #11722 功能重复，需要决策合并还是关闭 |
| [#11181 MapScan → typed Scan](https://github.com/temporalio/temporal/pull/11181) | 约 1 个月 17 天 | 🟡 中 | 改动横跨 7 个 Cassandra store 文件，review 成本较高 |
| [#11179 Cache getQueue result](https://github.com/temporalio/temporal/pull/11179) | 约 1 个月 17 天 | 🟡 中 | 涉及缓存一致性，需注意 `RangeDeleteMessages` 更新时的失效逻辑 |
| [#11300 Cache resolved namespace names](https://github.com/temporalio/temporal/pull/11300) | 约 1 个月 11 天 | 🟡 中 | 拦截器链共有 6-7 处重复解析，优化方向明确但需要对所有调用路径做回归验证 |
| [#11301 metrics 分配优化](https://github.com/temporalio/temporal/pull/11301) | 约 1 个月 11 天 | 🟡 中 | 涉及 `sync.Map`、`sync.Pool`，需确认无内存泄漏风险 |
| [#11804 Lazy timer map](https://github.com/temporalio/temporal/pull/11804) | 约 12 天 | 🟢 低 | 较新，等待 review 中，但价值大，建议优先推进 |

*计算基准：2026-09-07，PR 内 "更新" 时间均为 2026-09-06，说明均有活跃迭代。

**总体健康度评估**：项目在 1.32.0 发布前处于开发收口期，过去 24 小时无 Issue 涌入、无功能回归报告，整体稳定；但 PR 合并速度慢于创建速度（9 条待合并 vs 1 条关闭），积压趋势值得关注。若 1.32.0 release branch 已就绪，建议维护者尽快对 #11722 vs #9948 的功能重叠做出合并/关闭决策，并在版本窗口关闭前优先处理 #11927（改动小）和 #11804（价值大）。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*