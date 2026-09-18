# OpenClaw 生态日报 2026-09-19

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-18 22:35 UTC

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

# Pi 项目动态日报 · 2026-09-19

> 数据窗口：2026-09-18 ~ 2026-09-19 ｜ 数据来源：github.com/earendil-works/pi

---

## 1. 今日速览

Pi 今日处于**高强度维护活跃期**：24 小时内 70 条 Issue 更新（关闭 48 条，关闭率约 69%）、20 条 PR 更新（合并/关闭 13 条），但**无新版本发布**。合并侧重心集中在 retry 语义修正、会话/进程身份正确性、TUI 崩溃防护与 AI Provider 推理调度上，属于"稳定性回补日"而非功能扩张日。活跃讨论仍由 **Windows 平台支持路径混乱（#7547，64 评论）**、**macOS 长会话 CPU 占用（#7730）** 与**新 Claude 模型编辑工具失败率（#6278）** 三大老问题主导，这三者共同构成当前用户体感最强的负面信号。同时，今日关闭/合并了大量"模型目录过期""no-action 回归"类 Issue，说明维护者正在快速清理噪音，但**7 个 PR 滞留待合并（部分已开放 5 周以上）**，审查带宽可能成为下一阶段瓶颈。

---

## 2. 版本发布

**今日无新版本发布。** 最近一次可观测版本仍为 `0.85.1`（多份 Issue 以其为复现基线，如 #9725、#9737）。考虑今日已合并 13 条修复类 PR（含 retry 语义、流截断重试、溢出重试消息刷新等），预计近期将滚动出一个补丁版本。

---

## 3. 项目进展

### 3.1 今日合并/关闭的关键 PR（13 条）

**可靠性/重试语义修正（本日最集中的一条主线）**

| PR | 内容 | 价值 |
|---|---|---|
| [#9724](https://github.com/earendil-works/pi/pull/9724) | malformed `Retry-After` HTTP-date 回退到指数退避，并拒绝非有限延迟 | 修复 #9571 的 429 紧循环重试 |
| [#9736](https://github.com/earendil-works/pi/pull/9736) | 流在终止事件前被截断时，不再依赖错误措辞即触发重试 | 修复 #9735，兼容 OpenAI 兼容层/代理场景 |
| [#9722](https://github.com/earendil-works/pi/pull/9722) | 无诊断 body 的裸 4xx 纳入重试模式 | 网关类故障不再 fail-fast |

**会话与进程身份正确性**

- [#9754](https://github.com/earendil-works/pi/pull/9754)：将同一仓库的不同 git worktree 视为同一项目，并解析 session-dir 符号链接 — 修复 #9753，避免"跨项目 fork 提示"误报。
- [#9734](https://github.com/earendil-works/pi/pull/9734)：拒绝歧义的 `--session`/`--fork` ID 前缀并列出候选。此前静默选中最近会话，会把历史**追加写入错误的 session 文件**，属数据正确性问题，修复价值高。
- [#9738](https://github.com/earendil-works/pi/pull/9738)：溢出重试前先 flush 延迟的自定义消息，避免 `willRetry` 分支丢弃 provider 可见状态。

**TUI / 交互体验**

- [#9762](https://github.com/earendil-works/pi/pull/9762)：防护扩展工具返回非规范结果（缺少 `content` 数组）导致的 TUI 未捕获 `TypeError` 崩溃 — 修复 #9761，**崩溃会导致整个进程退出**，属高优先级防护。
- [#9744](https://github.com/earendil-works/pi/pull/9744)：新增 `/retry` 命令，用于连接重试失败后恢复被放弃的 turn。直接来自本地 LLM（llama-server）用户场景。
- [#9742](https://github.com/earendil-works/pi/pull/9742)：shell 耗时展示支持小时/分钟/秒 — 修复 #9628。
- [#9745](https://github.com/earendil-works/pi/pull/9745)：澄清 `app.message.copy` 快捷键描述，对齐 selection-first 行为 — 修复 #9660。

**AI Provider 层**

- [#9720](https://github.com/earendil-works/pi/pull/9720)：以 `thinkingLevelMap` 替代 id allowlist 驱动 Mistral 推理调度，并新增 `zai-glm-5-3`。
- [#9739](https://github.com/earendil-works/pi/pull/9739)：补充 qwen token plan / glm-5.3 / deepseek-v4.1-flash 测试覆盖。
- [#9749](https://github.com/earendil-works/pi/pull/9749)：SDK 调用方可注入 `formatResumeCommand`，便于嵌入式场景（如 Patooie）展示真实恢复命令。

### 3.2 推进程度评估

按覆盖面计，本日 **13 条 PR 关闭、48 条 Issue 关闭**，触及 retry、流解析、会话身份、TUI 崩溃、Provider 推理、CLI 参数校验等 6 个子系统，属于**健康的高吞吐清理日**。但需注意：关闭的 Issue 中有相当比例标记为 `no-action` 或属于"模型目录过期"类数据更新（#9485、#9616、#9737、#9725），真实代码变更的"含金量"低于关闭数量所暗示的水平。

---

## 4. 社区热点

### 🔥 #7547 [OPEN] [Windows] [sink-thread] How do you use Pi on Windows? What issues are you seeing?
[链接](https://github.com/earendil-works/pi/issues/7547) ｜ 64 评论 ｜ 👍2 ｜ 开放 47 天

本日讨论量断层第一。作者 @petrroll 提出的核心问题不是某个具体 Bug，而是**战略级困惑**：Pi 在 Windows 上存在"gazillion"种运行方式（原生、WSL、Git Bash、扩展注入……），维护者难以判断应把精力投入到"修 Bug / 做文档 / 开箱即用"哪一端，还是把部分路径下放给扩展生态。这条 thread 实际是**平台支持矩阵的定义性讨论**，与今日多条 Windows 具体 Bug（#9361、#9129、#9549）形成印证。建议维护者给出官方支持等级（Tier 1/2/3）以收束讨论。

### #6278 [CLOSED] [bug] New Claude models work poorly with the current Pi's edit tool
[链接](https://github.com/earendil-works/pi/issues/6278) ｜ 25 评论 ｜ 👍10 ｜ 已关闭

👍 数最高（10）之一。核心问题：新版 Claude 会在 `edit` 工具参数中"发明"额外字段（`new_text_x`、`type`、`in_file`、`closeenough` 等），触发 `must not have additional properties` 校验失败，**某些会话失败率约 20%**。这是典型的"模型行为变化 × 严格 schema 校验"冲突。已关闭说明已有应对（宽松化或过滤），但值得关注其具体方案是否会削弱校验强度。

### #7730 [OPEN] [bug] High CPU usage on Mac OS with long session
[链接](https://github.com/earendil-works/pi/issues/7730) ｜ 16 评论 ｜ 👍10 ｜ 开放 44 天

CPU 在 50%~110% 之间摆动，内存 600–800MB，疑似与上下文长度/会话时长正相关。👍 数同样为 10，情绪强烈。**至今无关联 fix PR**，且与 #9549（全屏大 transcript 每帧重渲染）指向同一类渲染/状态管理病灶，建议合并排查。

### 其他高互动

| Issue | 评论 | 要点 |
|---|---|---|
| [#8928](https://github.com/earendil-works/pi/issues/8928) | 11 | 并行启动时，auth.json 中他方 provider 的过期 OAuth 凭证会导致"No API key found" **持续约 48 秒**；有确定性复现与计时数据，生产环境踩坑 3 小时 |
| [#8684](https://github.com/earendil-works/pi/issues/8684) |

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 · 2026-09-19

> 数据来源：[github.com/BerriAI/litellm](https://github.com/BerriAI/litellm)
> 统计窗口：过去 24 小时（截至 2026-09-19）

---

## 一、今日速览

1. **活跃度处于高位**：过去 24 小时 Issues 更新 78 条（新开/活跃 51、关闭 27），PR 更新 372 条（待合并 195、已合并/关闭 177），单日 PR 吞吐量接近 400 条，属于典型的"高频迭代 + 大量机器人贡献"运行状态。
2. **发布节奏持续推进**：发布 1 个新版本 `v1.103.0-dev.2`，为 1.103 系列的开发预览版，Release Notes 仅涉及 Docker 镜像 cosign 签名验证说明，未披露面向用户的变更。
3. **今日合并/关闭集中在低讨论量 PR**：本次抓取的头部 PR 中仅 1 条为已关闭（[#41888](https://github.com/BerriAI/litellm/pull/41888)），其余 19 条仍处于 OPEN 评审状态，待合并队列（195 条）明显偏长。
4. **安全/权限类 Issue 集中浮现**：虚拟键模型白名单绕过（[#41810](https://github.com/BerriAI/litellm/issues/41810)）、流式 Guardrails 分块逃逸（[#41611](https://github.com/BerriAI/litellm/issues/41611)）、按客户 RPM 限制缓存后失效（[#39713](https://github.com/BerriAI/litellm/issues/39713)）三条同时处于活跃状态，是今日最需要关注的稳定性信号。
5. **积压清理见效**：今日关闭的 27 条 Issue 中，至少 10 条带有 `stale` 标签（如 [#16073](https://github.com/BerriAI/litellm/issues/16073)、[#30135](https://github.com/BerriAI/litellm/issues/30135)、[#30836](https://github.com/BerriAI/litellm/issues/30836)），其中包含创建于 2025-10-29、存续近一年的 fal.ai 模型支持请求。

**综合健康度评估**：提交动能强、社区参与度高，但 *PR 待合并队列 / 已关闭* 比例约为 1.1:1，评审带宽已成为瓶颈；同时 AI 机器人账号（`devin-ai-integration[bot]`）贡献了头部 PR 的绝大多数，需要在质量把关上投入额外注意力。

---

## 二、版本发布

### v1.103.0-dev.2（开发预览版）

- **链接**：[Release v1.103.0-dev.2](https://github.com/BerriAI/litellm/releases)
- **发布内容**：Release Notes 全文围绕 Docker 镜像签名验证展开——所有 LiteLLM Docker 镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 签名，签名密钥与 commit [`0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0) 引入的密钥一致。

**分析：**

| 维度 | 结论 |
|---|---|
| 破坏性变更 | Release Notes 中**未披露**任何破坏性变更 |
| 迁移注意事项 | 无需迁移；因是 `-dev.2` 后缀的开发构建，**不建议生产环境使用** |
| 实质更新 | 本次公告偏向供应链安全（签名验证）合规说明，而非功能变更 |

> ⚠️ 提示：由于该版本为 dev 预发布，且 Notes 未列出代码级变更列表，建议关注后续 `v1.103.0` 正式版的完整 CHANGELOG。若运维侧有镜像校验需求，可现在就按 cosign 流程接入签名验证。

---

## 三、项目进展

由于本次抓取的 PR 评论区数据缺失（评论数显示为 `undefined`），以下基于 PR 标题、摘要与状态进行主题聚合。

### 3.1 已合并 / 已关闭

- **[#41888](https://github.com/BerriAI/litellm/pull/41888) [CLOSED] `feat(ui): link MCP Servers page to the user's connected MCP servers`**
  - 解决：`/ui/connect`（用户已连接的 MCP 服务器页面，含 Disconnect 功能）此前在 Dashboard 中**没有任何入口**，用户必须手动记住 URL；`/ui/mcp-servers` 页面上也无任何指向。
  - 推进：打通 MCP 服务器管理与用户连接视图之间的导航断点，属于 MCP 控制台体验的补完。

> 说明：今日另有约 176 条 PR 被合并/关闭，但均未进入头部讨论列表，无公开摘要可供分析。

### 3.2 正在评审的重点 PR（按主题聚类）

**A. 预算与配额治理（成本控制主线）**

| PR |

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报
**报告日期：2026-09-19　｜　数据窗口：过去 24 小时　｜　仓库：github.com/temporalio/temporal**

---

## 1. 今日速览

Temporal 今日维持**高强度活跃状态**：Issues 更新 17 条（新开/活跃 2，关闭 15）、PR 更新 58 条（待合并 43，合并/关闭 15），并同步发布 2 个补丁版本（v1.30.7、v1.31.3），呈现"稳定分支维护 + 主干架构演进"双线并行的典型节奏。

今日最显著的特征是**问题积压批量清理**：15 条关闭 Issue 中绝大多数是 2022–2024 年提出的 enhancement，一次性收口；同时两个新问题指向真实生产风险（MySQL 连接池无界增长、Schedule 版本覆盖未生效）。

主干侧由 **CHASM / namespace replication 七连 PR 栈**、**Dynamic Partitioning 配置化**、**SQL 持久化性能优化**三条主线推动，工程投入明显集中在架构迁移与可扩展性上。

整体健康度评估：**良好偏积极**。发布节奏稳定、架构演进路线清晰；主要风险点是 43 条待合并 PR 形成的评审队列压力，以及部分长周期 PR 栈的合并复杂度。

---

## 2. 版本发布

今日发布两个补丁版本，均为 **Cherry-pick 性质的稳定分支维护**，无破坏性变更、无迁移要求。

### v1.30.7（v1.30.x 维护线）
链接：https://github.com/temporalio/temporal/releases

| 变更 | PR | 说明 |
|---|---|---|
| 引入最新 manual docker build action | [#10976](https://github.com/temporalio/temporal/pull/10976) | CI/发布基础设施修复 |
| 同步更新 `docker-bake.hcl` | [#10977](https://github.com/temporalio/temporal/pull/10977) | 与上条配套，保证镜像构建一致 |
| Cherry-pick #11090：为 matching handler API 增加 panic handler | — | **可靠性修复**，防止匹配服务处理器 panic 导致进程级故障 |

### v1.31.3（v1.31.x 维护线）
链接：https://github.com/temporalio/temporal/releases

| 变更 | PR | 说明 |
|---|---|---|
| Cherry-pick #11090：matching handler API panic handler | [#11106](https://github.com/temporalio/temporal/pull/11106) | 与 v1.30.7 同源的稳定性修复 |
| 新增 Nexus callback source header 检查开关 | [#11982](https://github.com/temporalio/temporal/pull/11982) | **安全相关**：为 Nexus 回调来源头提供可配置的校验开关（toggle），由 @bergundy 提交 |
| 升级 `go.temporal.io/...` 依赖 | — | 常规依赖升级（日志中被截断） |

**注意事项**：建议 v1.30.x / v1.31.x 用户升级以获得 matching 服务的 panic 防护；Nexus callback source header toggle 为可选配置项（默认行为需参考对应 PR 说明），启用前请确认回调链路兼容性。

---

## 3. 项目进展

今日合并/关闭 15 条 PR，主要推进方向如下：

### 3.1 CHASM 组件化行为建模（已关闭）
- **[#12044](https://github.com/temporalio/temporal/pull/12044) — CHASM Activity 组件行为模型/规范**（@dandavison，已关闭）
  为 Activity 的 CHASM 组件引入**可执行模型（executable model / specification）**，并将集成测试接入该模型，使每一个事件/状态转换都被规范校验。这是 CHASM 迁移从"实现"走向"可验证正确性"的关键一步。

### 3.2 版本化状态转换任务优化（已关闭）
- **[#12139](https://github.com/temporalio/temporal/pull/12139) — 避免 verify transition 任务加载 mutable state**（@xwduan，已关闭）
  在创建 `SyncVersionedTransitionTask` 时仅捕获当前 version-history items（不含 cluster-local branch token），并在获取 workflow 锁与加载 mutable state **之前**生成待发送的 verify 任务。直接收益是减少热路径上的状态加载与锁竞争。

### 3.3 Dynamic Partitioning 落地（已关闭 1 条 + 2 条在审）
- **[#12144](https://github.com/temporalio/temporal/pull/12144) — poll cancellation fan-out 使用动态分区数**（@rkannan82，已关闭）
  解析 `TODO(dynamic partitioning)`，`CancelOutstandingWorkerPolls` 扇出时改用 `PartitionScale()` 的真实读分区数，回退到动态配置值。修复了分区扩容后取消广播不完整的问题。

### 3.4 名称空间复制向 CHASM 迁移（七连栈，进行中）
由 @qyc5937 提交的 PR 栈（PR0→PR3）正在分阶段推进，是当前**最大的架构演进工程**：
- [#12112](https://github.com/temporalio/temporal/pull/12112) PR0：抽取共享复制 helpers 到 `common/namespace/nsreplication`
- [#12135](https://github.com/temporalio/temporal/pull/12135) PR1a：新增 namespace-mutation protobuf 契约与 `ApplyNamespaceMutation` 接收端
- [#12113](https://github.com/temporalio/temporal/pull/12113) PR1b：实现 inert CHASM 库与生命周期状态机
- [#12115](https://github.com/temporalio/temporal/pull/12115) PR2：接入 shadow 传输模式（`legacy` / `shadow` / `chasm` 动态配置，默认 legacy）
- [#12125](https://github.com/temporalio/temporal/pull/12125) PR3：启用 authoritative CHASM 传输

**推进程度评估**：今日项目中约 1/3 的待合并 PR 集中在这条栈上，属于"高投入、长周期、低风险发布"的迁移模式（shadow → authoritative 渐进切换），设计上对现网是安全的。

---

## 4. 社区热点

> 注：本次数据快照未返回评论计数字段（`undefined`），以下按议题影响面、讨论时长与业务关联度排序。

| 排名 | 议题 | 状态 | 热度依据 |
|---|---|---|---|
| 1 | [#9747](https://github.com/temporalio/temporal/issues/9747) MySQL Connector 在 DB 持续不可用期间创建无界 `sql.DB` 连接池 | OPEN | 7 条评论（本批次最多）、开放近 6 个月、涉及生产级连接耗尽 |
| 2 | [#12162](https://github.com/temporalio/temporal/issues/12162) 在 child workflow options 中暴露 start delay | CLOSED | 👍 5，客户端/子工作流功能对齐诉求 |
| 3 | [#1203](https://github.com/temporalio/temporal/issues/1203) 新增 `SignalWithReset` | CLOSED | 👍 6（本批次最高），2021 年提出，社区期待度长期存在 |
| 4 | [#12153](https://github.com/temporalio/temporal/issues/12153) SDK 应提供原生查询构造器 | CLOSED | 4 条评论，Go SDK visibility 查询字符串拼接易错 |
| 5 | [#12172](https://github.com/temporalio/temporal/issues/12172) UI 中带 source mapping 的堆栈追踪 | CLOSED | 2 条评论，调试体验类高价值诉求 |

**背后诉求分析**：
- **#9747 是今日唯一具备"生产事故潜力"的热点**。核心矛盾在于 `DatabaseHandle.reconnect()` 未遵守 maxConns 约束，导致连接总数随重连次数线性膨胀，在 DB 抖动场景下可能引发级联故障。7 条评论说明社区已在做深入复现与方案讨论，但**至今未见对应 fix PR**（详见第 5 节）。
- **#1203 / #12162** 反映的是"客户端能力已存在、服务端/SDK 未对齐"的**功能对等性缺口**（client-only 能力缺失在 child workflow、signal 语义上的映射）。
- **#12153 / #12172 / #12168** 构成一组"开发者体验"信号：查询构造、堆栈可读性、replay 结果可校验——都是用户在**大规模运维与调试阶段**才会强烈感知的痛点，说明 Temporal 用户群正从"接入期"走向"规模化运营期"。

---

## 5. Bug 与稳定性

### 🔴 高严重度

| 议题 | 类型 | 摘要 | Fix PR |
|---|---|---|---|
| [#9747](https://github.com/temporalio/temporal/issues/9747) | potential-bug | MySQL Connector 在 DB 持续不可用期间创建**无界 `sql.DB` 连接池**；期望重连时遵守 maxConns，实际总连接数可能超过 `pods × pools × maxConns`。可导致 DB 恢复后连接风暴、服务不可用 | ❌ 未发现 |
| [#12148](https://github.com/temporalio/temporal/issues/12148) | functional bug（新报） | V1 scheduler 中 `ScheduleWorkflowAction.VersioningOverride` **被持久化但从未应用到启动的 workflow**；固定 Worker Deployment Version 的 Schedule 实际未生效，影响灰度/固定版本发布场景 | ❌ 未发现 |

**说明**：
- #9747 自 2026-03-30 创建至今已近半年仍为 OPEN，且属于"数据库不可用"这一最需要弹性的场景，**建议提升优先级并指派 owner**。
- #12148 是今日新报（2026-09-18），描述规范、附带预期行为对比，属于**静默失效类 bug**（不报错但语义不正确），排查成本高，建议尽快确认 V1/V2 scheduler 的覆盖范围。

### 🟡 中低严重度（已关闭，视为已修复/已收敛）

| 议题 | 摘要 | 状态 |
|---|---|---|
| [#11709](https://github.com/temporalio/temporal/issues/11709) | PostgreSQL history 分页在复合游标前**重复扫描行**，页查询成本随前置行数增长 | CLOSED（已有对应 SQL 优化 PR，见下） |

**关联修复 PR（在审/已合）**——今日 SQL 持久化性能修复较为集中，疑似为 #11709 / #11710 / #11711 系列：
- [#12098](https://github.com/temporalio/temporal/pull/12098)（OPEN）重写 PostgreSQL workflow 与 CHASM current-execution 加锁逻辑：先在子查询中锁定当前行，再用完整主键 join 锁定执行记录，避免扫描历史 run。
- [#11714](https://github.com/temporalio/temporal/pull/11714)（OPEN，fixes #11711）SQL

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*