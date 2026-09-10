# OpenClaw 生态日报 2026-09-10

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-10 00:19 UTC

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

# OpenHands SDK 项目动态日报 — 2026-09-10

## 1. 今日速览

过去24小时项目活跃度较高：共产生 25 条 Issue 更新（新开/活跃 17 条，关闭 8 条）与 50 条 PR 更新（待合并 44 条，已合并/关闭 6 条），并发布了 v1.46.0 补丁版本。当前开发重点集中在三块：**ACP（Agent Client Protocol）provider 架构合规与安全加固**（#4923、#4841、#4874）、**一批由 @enyst 集中提交的架构级 Bug**（涉及进程全局状态污染、并发竞态、会话隔离等，近10条），以及 **OpenAI gateway/streaming 路线图收尾**（#3598-#3602 系列关闭）。值得关注的是，Issue 侧出现了 `priority:high` 的 ACP 文件密钥泄露问题（#4923）与 CI 路径过滤缺口（#4912），需优先响应。项目健康度总体良好，但 PR 待合并队列积压较重（44 条待合并，部分已悬挂超过6周），维护者需关注。

---

## 2. 版本发布

### v1.46.0（最新）
- **发布时间**：2026-09-09 至 2026-09-10 之间
- **Release Notes 摘要**：
  - `fix(ci)`: 集中发布调度分发（PR #4886， @neubig）
  - `fix(agent-server)`: 在 pre-flight 验证中恢复订阅凭据（PR #4898， @neubig）
- **Release Notes 截断**：官方 Notes 在第三条处被截断（`fix(`），预计包含更多内容，建议维护者补全。
- **破坏性变更 / 迁移注意**：未在已公布 Notes 中提及，暂判为无破坏性变更。但结合 #3598-#3602 等多条 OpenAI gateway 相关 issue 在昨日集中关闭，v1.46.0 可能还包含 gateway 增强。

> 链接：https://github.com/OpenHands/software-agent-sdk/releases

---

## 3. 项目进展

### 3.1 已关闭 Issue 所反映的合并内容

过去24小时关闭了 8 条 Issue，其中 4 条属于 OpenAI gateway 路线图（#3598、#3599、#3600、#3601、#3602 中的4条关闭，对应 Chat Completions gateway 的运营打磨、conversation 复用、final-answer streaming、tool-call streaming 评估），说明 **gateway 相关工作已阶段性落地**：

- **#3599 `feat(agent-server): add operational polish to OpenAI gateway`** [CLOSED] — 关闭时间 2026-09-09。网关的 timeout/cancellation/错误可理解性已完善。
- **#3600 `feat(agent-server): add final-answer streaming to OpenAI chat completions gateway`** [CLOSED] — SSE `chat.completion.chunk` 流式支持已落地。
- **#3598 `feat(agent-server): improve OpenAI gateway conversation reuse ergonomics`** [CLOSED] — conversation id 头机制已明确。
- **#3602 `feat(agent-server): evaluate opt-in tool-call streaming for OpenAI gateway`** [CLOSED] — 评估结论为不做默认支持。

> 链接：https://github.com/OpenHands/software-agent-sdk/issues/3599 | #3600 | #3598 | #3602

另外两条关闭的 Bug：

- **#4662 `[Bug]: Nested Git filtering drops unrelated prefix-sharing paths`** [CLOSED] — `get_git_changes()` 改为基于目录祖先而非字符串前缀匹配，修复了嵌套仓库命名导致误删父仓库变更的问题。对应合并的修复。 → https://github.com/OpenHands/software-agent-sdk/issues/4662
- **#4930 `[Feature]: Restore label-triggered API compliance and condenser test suites`** [CLOSED] → https://github.com/OpenHands/software-agent-sdk/issues/4930
- **#4919 `[Docs]: Remove stale run-eval AGENTS reference`** [CLOSED] → https://github.com/OpenHands/software-agent-sdk/issues/4919

### 3.2 整体判断

从 gateway 路线图系列 issue 的批量关闭、v1.46.0 发布与架构级 Bug 的大量标注（`ready-for-dev`）来看，项目当前处于 **"核心路线图收尾 + 架构加固批量启动"** 阶段，正向更稳定、更安全的 SDK 演进。CI 测试与 release 流程也在持续修补（#4886、#4912、#4930）。

---

## 4. 社区热点

### 4.1 #4841 — ACP harness 声明与云行为解耦设计讨论（5条评论）
- **作者**：@simonrosenberg | 更新：09-09 | [链接](https://github.com/OpenHands/software-agent-sdk/issues/4841)
- **状态**：`[OPEN]` `[enhancement, acp]`，9月4日重写为开放设计问题（选项 A–D）
- **核心诉求**：要求**向 SDK 增加一个 ACP harness 不应改变 Cloud 或 Replicated 的行为**。`ACP_PROVIDERS` 目前只声明了什么"存在"，而未声明某个部署"提供"什么。这是 SDK 作为单一事实源与下游部署之间的架构解耦问题。
- **热度分析**：这是 ACP 架构演进中最核心的设计议题，贯穿 #4923（安全漏洞）、#4833（下游 CI）、#4874（新增 Cursor provider）多条线。

### 4.2 #4667 — Tom 处理历史可检查点从未被索引的事件（4条评论）
- **作者**：@enyst | 更新：09-09 | [链接](https://github.com/OpenHands/software-agent-sdk/issues/4667)
- **状态**：`[bug, priority:medium, tools, ready-for-dev]`
- **技术要点**：Tom candidate 选择读取当前事件计数后，`_save_processing_history()` 重新列出可变事件目录，窗口期间新事件可能被错误纳入检查点。

### 4.3 #4925 — MCP 工具调用在 fastmcp>=4.0 下持续产生弃用警告（5条评论中的最新）
- **作者**：@zohuyhieuzo03（外部用户） | 更新：09-09 | [链接](https://github.com/OpenHands/software-agent-sdk/issues/4925)
- **状态**：`[Bug]`，无优先级标签，无关联 fix PR
- **用户痛点**：每次 MCP 工具调用都打出 `FastMCPDeprecationWarning`，涉及 5 处调用点，影响 fastmcp>=4.0 的升级路径。

> 其余评论数 ≥3 的还包括 #4663（glob 并发修改 cwd，3条）、#3599 关闭（route）、#3601（route）、#4661（subagent注册表，3条）等，技术密度较高，社区讨论整体呈深度技术协作特征。

---

## 5. Bug 与稳定性

### 5.1 高危（priority:high）

| Issue | 标题 | 状态 | 分析 |
|---|---|---|---|
| [#4923](https://github.com/OpenHands/software-agent-sdk/issues/4923) | ACPAgent materialises every provider's file secrets | `[OPEN]` `[priority:high, security]` | `acp_file_secrets` 默认取所有已注册 provider 的联合，注册一个带 `file_secrets` 的 harness 会导致所有其他 provider 行为改变。**属于安全敏感的设计缺陷**，昨天刚开且无 fix PR，需尽快响应。 |
| [#4912](https://github.com/OpenHands/software-agent-sdk/issues/4912) | Path-gated test jobs omit `openhands-sdk/**` | `[OPEN]` `[priority:high, ci]` | CI 路径过滤缺失导致 SDK 变更可破坏下游测试但所有必须检查仍为绿色。**这是 CI 可靠性的严重漏洞**，会让回归溜过检查。@simonrosenberg 9月8日提交，昨有更新。 |

### 5.2 中危（priority:medium）— @enyst 批量的并发/污染类 Bug

@enyst 于 8月27日 集中提交了约 10 条架构级 Bug，多数已标记 `ready-for-dev`，但在过去24小时仅有评论更新，尚未出现对应的 fix PR：

| Issue | 问题简述 |
|---|---|
| [#4663](https://github.com/OpenHands/software-agent-sdk/issues/4663) | Python glob fallback 用 `os.chdir` 修改进程全局 cwd，并发时与其他线程竞态 |
| [#4661](https://github.com/OpenHands/software-agent-sdk/issues/4661) | 进程全局 subagent 注册表为 first-writer-wins，跨对话泄漏定义 |
| [#4664](https://github.com/OpenHands/software-agent-sdk/issues/4664) | CloudWorkspace `resume()` 轮询刷新凭据后未更新活动客户端连接 |
| [#4659](https://github.com/OpenHands/software-agent-sdk/issues/4659) | stdout/stderr 并发读取共用 `output_order` 计数器，可能产生顺序值重复 |
| [#4660](https://github.com/OpenHands/software-agent-sdk/issues/4660) | RouterLLM 只覆盖同步 `completion()`，异步 `acompletion()` 绕过路由选择 |
| [#4658](https://github.com/OpenHands/software-agent-sdk/issues/4658) | 延迟初始化失败后部分变更未回滚，运行时处于半初始化状态 |
| [#4666](https://github.com/OpenHands/software-agent-sdk/issues/4666) | 重复浏览器录制启动会孤立后台 flush 任务 |
| [#4668](https://github.com/OpenHands/software-agent-sdk/issues/4668) | Planning file editor 丢继承的 observation 和 diff 数据 |
| [#4665](https://github.com/OpenHands/software-agent-sdk/issues/4665) | Skills marketplace 在当前 extensions manifest 布局下返回空列表 |
| [#4667](https://github.com/OpenHands/software-agent-sdk/issues/4667) | Tom 处理历史可检查点从未被索引的事件 |

这些 Bug 的共同主题是**进程全局可变状态**与**并发安全**——反映了 SDK 从单会话工具向多会话、多租户 server 架构演进过程中的系统性技术债。已标 `ready-for-dev`，等待社区认领。

### 5.3 低危 / 外部报告

- **#4919** `[Docs]: Remove stale run-eval AGENTS reference` — 已关闭，9月9日创建并同日修复。[链接](https://github.com/OpenHands/software-agent-sdk/issues/4919)

### 5.4 已有修复 PR 的 Bug

- **#4662** Nested Git filtering bug — **已关闭**（对应修复已合入）。
- **#4585**（PR）修复 #4554：critics 未收到 workspace git patch — 仍在待合并状态。

---

## 6. 功能请求与路线图信号

### 6.1 ACP 生态扩展（最密集信号）

- **#4841** ACP harness 声明机制设计（开放中）→ 若落地，将改变 SDK 的 ACP provider 注册 API。
- **#4833** ACP 下游 CI 断言清单（`[enhancement, acp, ready-for-dev]`）→ SDK 已成为 ACP provider 唯一事实源，需要让消费仓库在 registry 变更时自动失败提醒。
- **PR #4874**：新增 **Cursor** 为内置 ACP provider — 作者 @genguzzz 实测 Cursor CLI `2026.09.02` 的 ACP 握手成功。[链接](https://github.com/OpenHands/software-agent-sdk/pull/4874)
- **PR #4437**：新增 claude-fable-5 到 Claude Code 模型选择器。[链接](https://github.com/OpenHands/software-agent-sdk/pull/4437)

### 6.2 新能力提案信号

| 提案 | 类型 | 潜在版本 |
|---|---|---|
| **#4892** DAG 任务执行（`run_dag`）| 新架构能力，DAG-as-plan 原语 | 若合入属较大新功能，v1.47+ |
| **#4287** Pareto prompt meta-profile 路由 | 路由增强 | 已测试 + SaaS

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-09-10

## 今日速览

过去 24 小时 Temporal 核心仓库活跃度处于**中等水平**：无新 Issue 产生，PR 侧保持较密集的更新节奏，共 38 条 PR 处于活跃状态（待合并 24 条，已合并/关闭 14 条）。合入工作主要集中于 Nexus 回调指标增强、版本号提升及 release 分支修复同步。值得关注的是，围绕 **Nexus/worker-callbacks** 功能族的 PR 链条今日仍有多条处于活跃更新中，且有从 `release/v1.30.x` 向主分支反向合入的 cherry-pick 操作，说明团队在推进新功能的同时兼顾维护分支稳定性。另有多条关于 `SignalWithStart` 可靠性与数据竞争修复的 PR 持续更新，显示可靠性治理是当前重点投入方向。

---

## 版本发布

无新版本发布。

---

## 项目进展

过去 24 小时关闭/合入的 14 条 PR 中，以下几条对项目状态有明确推进：

- **Nexus 回调指标维度细化**（[#11927](https://github.com/temporalio/temporal/pull/11927)）— 已关闭。为 `callback_outbound_requests` 和 `callback_outbound_latency` 指标新增 `nexus_completion_source` tag，并改进回调完成日志的附加标签。该改动将提升 Nexus 回调链路的可观测性，便于追踪不同来源的完成回调。

- **版本号提升至 1.33**（[#11978](https://github.com/temporalio/temporal/pull/11978)）— 已关闭。服务端版本号已从 1.32 提升至 1.33，为下一轮 release 做准备。

- **Nexus 回调源请求头检查开关**（[#11982](https://github.com/temporalio/temporal/pull/11982)）— 已关闭并合入 `v1.31` 分支。将旧的 Nexus 回调 source-header 路由置于 `callback.inspectSourceHeader` 配置开关之后，默认启用以兼容 `temporal://system` 迁移期间的行为。该修复基于安全考虑，属于维护分支的补丁合入。

- **Cherry-pick 列表匹配性能优化**（[#11981](https://github.com/temporalio/temporal/pull/11981)）— 待合并。将主分支的 List matching 性能优化（原 PR [#11014](https://github.com/temporalio/temporal/pull/11014)）移植至 `release/v1.30.x`，并针对 Schedules V2 的代码差异做了适配。

整体来看，项目在 Nexus 可观测性增强、多分支维护同步以及版本发布准备三个方向上有明确进展，向前迈进的幅度以增量改进为主。

---

## 社区热点

以下 PR 在过去 24 小时获得最多关注或最新动态更新：

- **[SignalWithStart 请求去重修复 #11968](https://github.com/temporalio/temporal/pull/11968)** — 讨论持续活跃（更新于 09-09）。当原始 workflow 已结束后重试 `SignalWithStart` 时，相同 request ID 现在会返回原 run 而非启动新 run。该修复还新增了 `SignalWithStartWorkflowStartDeduped` 指标。同一作者的另一条 PR [#11810](https://github.com/temporalio/temporal/pull/11810)（修复 SignalWithStart 绕过 continue-as-new backoff）也在持续更新，两者聚焦于同一 API 的语义完善，反映社区对该 API 边界场景的高关注度。

- **[progressive connect 发送端方案 #11984](https://github.com/temporalio/temporal/pull/11984)** — 09-09 新创建，是 [#11492](https://github.com/temporalio/temporal/pull/11492) 的精简替代方案。为 global namespace 添加新目标集群时提供发送端渐进式连接能力，通过 `frontend.enableReplicationGradualConnect` 开关控制。该 PR 尚新，但与其替代的 #11492 共同构成了跨集群复制演进的重要信号。

- **标记为 stale 的 CHASM 分支探索 #10114** — 创建于 4 月，至今仍在持续更新（09-10）。作者明确声明**不会合入 main**，仅为探索 workflow activities 迁移至 CHASM 的实验。说明团队内部仍有针对 CHASM 的技术预研在进行，但短期不会形成面向用户的特性。

- **worker-callbacks 功能族多条 PR**（[#11589](https://github.com/temporalio/temporal/pull/11589)、[#11566](https://github.com/temporalio/temporal/pull/11566)、[#11567](https://github.com/temporalio/temporal/pull/11567)、[#11520](https://github.com/temporalio/temporal/pull/11520)、[#11380](https://github.com/temporalio/temporal/pull/11380)）— 均由 @chrsmith 提交，形成 stacked PR 链，最终汇入 `feature/worker-callbacks` 分支。功能范围涵盖 NexusHandler 变体回调、可配置回调类型、CallbackInfo 字段填充等。这些 PR 短期内不会直接进 main，但揭示了未来回调机制的重要演进方向。

---

## Bug 与稳定性

以下稳定性相关 PR 处于活跃状态：

**高严重度：**

- **重试抖动逻辑失效 Bug**（[#11397](https://github.com/temporalio/temporal/pull/11397)）— `common/backoff/retrypolicy.go` 中的 `addJitter` 从未产生实际抖动效果，导致设置 `WithJitter(0.1)` 后所有延迟仍是固定值而非均匀分布于 `[base, base×1.1)` 区间。该 Bug 影响所有依赖重试策略的服务调用。已有修复 PR，但尚未合入。

- **perNamespaceWorker 初始化数据竞争**（[#11825](https://github.com/temporalio/temporal/pull/11825)）— 修复 `getWorkerByNamespace` 中动态配置回调可能在 `ns`、`count`、`opts` 字段初始化前被触发导致的 nil 指针问题。修复方式为注册回调前先持有 worker 锁。已有修复 PR。

**中严重度：**

- **SignalWithStart 绕过 continue-as-new backoff**（[#11810](https://github.com/temporalio/temporal/pull/11810)）— 当 workflow 通过 continue-as-new 重新开始时，`SignalWithStart` 会绕过首个 workflow task 的 backoff 配置。修复后 signal 立即记录但 workflow task 需等待 backoff 到期后才调度。已有修复 PR。

- **SignalWithStart 去重失效致重复执行**（[#11968](https://github.com/temporalio/temporal/pull/11968)）— 原始 workflow 结束后重试 `SignalWithStart` 会启动新 run 并发送重复 signal。修复后相同 request ID 返回原 run 并新增去重指标。已有修复 PR。

- **历史分页在分支元数据变更后的兼容性**（[#11983](https://github.com/temporalio/temporal/pull/11983)）— 当 page token 指向的 tree 和 branch 元数据已过期（stale）时，使用当前 branch token 以支持分页继续。已有修复 PR 并附带单元测试。

- **Logger tags 在 `Skip()` 后丢失**（[#11355](https://github.com/temporalio/temporal/pull/11355)）— `zapLogger.Skip()` 返回的 clone 未携带原 logger 的 tags，修复后与已转发的 `baseZl` 字段保持一致，并同步更新了 `TestThrottleLogger`。已有修复 PR。

---

## 功能请求与路线图信号

- **Worker Callbacks 大功能**：多条 stacked PR（[#11380](https://github.com/temporalio/temporal/pull/11380)、[#11520](https://github.com/temporalio/temporal/pull/11520)、[#11566](https://github.com/temporalio/temporal/pull/11566)、[#11567](https://github.com/temporalio/temporal/pull/11567)、[#11589](https://github.com/temporalio/temporal/pull/11589)）持续推进，明确指向一个全新的 **`NexusHandler` 回调变体**。该特性将允许从 worker 发起回调，而非仅由 Temporal 服务端发起。其中 #11589 被作者称为"the actual PR"（真正的核心实现），预计该功能完整落地后才可能合入 main，暂不进入下一版本。

- **渐进式复制连接**：两条并行的 PR（[#11492](https://github.com/temporalio/temporal/pull/11492) 原始方案与 [#11984](https://github.com/temporalio/temporal/pull/11984) 精简方案）都致力于在 global namespace 加入新集群时，通过一段渐进式的 ramp-up 阶段逐步将复制流量从 shed 状态恢复至完全连接状态。此特性对跨地域多集群部署有实用价值。

- **Nexus 完成来源可区分性**（[#11927](https://github.com/temporalio/temporal/pull/11927)）已合入— 指标 tag 的加入表明团队正在针对不同来源（如 CHASM 与 legacy）的 Nexus 回调建立更细粒度的可观测性体系。

- **tdbg 动态配置值转储命令**（[#9948](https://github.com/temporalio/temporal/pull/9948)）— 来自外部贡献者，为 CLI 工具 `tdbg` 增加动态配置值转储能力，便于运维排查。PR 自 4 月创建至今已 5 个月未合入，不确定是否会进入后续版本。如您是核心维护者，建议评估可行性后尽快给出结论。

---

## 用户反馈摘要

（注：过去 24 小时无新增 Issue，以下提炼自各活跃 PR 中暴露出的问题，代表开发者和真实用户在实际使用中遇到的场景。）

- **重试抖动失效**（[#11397](https://github.com/temporalio/temporal/pull/11397)）— 当配置了 `WithJitter(0.1)` 后，所有重试延迟完全相同，导致流量洪峰在重试时刻集中打向依赖服务。这是一个从代码逻辑层面能明确感知的运维痛点，影响后端服务的负载均衡。

- **SignalWithStart 重复执行风险**（[#11968](https://github.com/temporalio/temporal/pull/11968)）— 当客户端重试 `SignalWithStart` 时（网络超时等场景），如果原 workflow 恰好已结束，会导致重复启动新 workflow 且重复投递信号。这对依赖 request ID 去重语义的业务方是一项严重的行为违约。

- **continue-as-new 后 SignalWithStart 语义缺陷**（[#11810](https://github.com/temporalio/temporal/pull/11810)）— 使用 continue-as-new 模式的长期运行 workflow，如果其初始 backoff 被 SignalWithStart 绕过，可能导致业务逻辑在新 run 中提前启动，破坏原有的延迟执行设计意图。

- **回调来源难追踪**（[#11927](https://github.com/temporalio/temporal/pull/11927)）— 运维与开发者需要从指标维度区分不同来源的 Nexus 回调请求（CHASM 还是 legacy），以便独立追踪各链路的 latency 与错误率。该请求已通过新增指标 tag 得到满足。

---

## 待处理积压

以下 PR 或 Issue 已存在较长时间且缺乏有效推进，提请维护者关注：

- **[tdbg 动态配置转储命令 #9948](https://github.com/temporalio/temporal/pull/9948)** — 由外部贡献者 @vaibhavyadav-dev 提交，创建于 2026-04-14，已存在近 5 个月，仍在开放状态，近期有更新但尚未合入。外部贡献长时间悬而未决会影响贡献者参与积极性，建议明确反馈。

- **[CHASM workflow activities 实验 PR #10114](https://github.com/temporalio/temporal/pull/10114)** — 创建于 2026-04-29，作者本人标注 "will not merge"，但仍在持续更新。建议核心维护者关注该实验分支的结论是否已沉淀为独立 issue 或设计文档，避免长期以 PR 形式悬挂消耗社区关注度。

- **[Logger tags 修复 #11355](https://github.com/temporalio/temporal/pull/11355)** — 创建于 2026-07-30，已开放超 40 天，为明确的 bug 修复且包含测试更新，但仍未合并，建议加快 review 节奏。

- **[Retry 抖动修复 #11397](https://github.com/temporalio/temporal/pull/11397)** — 创建于 2026-08-02，同样是明确的逻辑 bug（代码行为与配置语义完全不符），至今超过一个月未合入，建议维护者确认阻塞原因并及时推进。

- **[NexusHandler 回调变体系列 PR](https://github.com/temporalio/temporal/pull/11380)** — 这一组 PR 在 7 月底至 8 月中旬间创建，至今仍在排队等待合入 feature 分支（部分 PR 的合入目标 `feature/worker-callbacks` 本身尚未合入 main）。鉴于该功能链条较长且改动跨越 API 定义和服务端实现，建议维护者持续给出阶段性进展说明，以便社区了解整体规划。

---

**日报总结**：Temporal 项目当前处于**平稳演进期**，Nexus/callback 生态的深化是近期最显著的信号，SignalWithStart 的可靠性修复及数据竞争治理体现了团队对系统健壮性的持续投入。多分支 cherry-pick 同步表明项目正朝向 1.33 版本的发布稳步推进。需关注的是多条长时间悬而未决的 bug-fix PR 的合入效率。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*