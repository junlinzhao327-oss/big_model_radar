# OpenClaw 生态日报 2026-08-30

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-29 22:36 UTC

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

# OpenHands SDK 项目动态日报（2026-08-30）

## 1. 今日速览

过去 24 小时项目保持中等偏高的活跃度：5 条 Issue 更新（全部新增/活跃，无关闭），29 条 PR 更新（全部停留在待合并状态，无合并、无关闭），无新版本发布。值得关注的是，**今日合并/关闭数为零** —— 大量 PR 已进入待合并队列（含 6 月、7 月提交的老 PR），但合并流程未见推进，这是当前项目健康度的主要风险点。Issue 侧反馈集中在并发安全（glob fallback 修改进程 cwd）、运行时资源回收（空闲计时器失效导致 pod 被回收）、MCP 输入校验等基础设施问题上，且已有对应修复 PR 提交，说明社区响应及时，但合并瓶颈日益突出。

---

## 2. 版本发布

**无新版本发布。** 最近一次 Release 日期早于本统计窗口，当前代码库处于大量 PR 待合并、版本发版停滞的状态。

---

## 3. 项目进展

**今日无 PR 被合并或关闭。** 这是一个需要警惕的信号——29 条 PR 全部处于 open 状态，说明大量已完成开发、等待审查的代码未能流入主干。不过这 29 条待合并 PR 本身勾勒出了项目正在推进的方向：

| 方向 | 代表性 PR | 说明 |
|---|---|---|
| **并发安全修复** | [#4707](https://github.com/OpenHands/software-agent-sdk/pull/4707) | 修复 glob 工具的 Python fallback 用 `os.chdir` 修改进程级 cwd 的竞态问题，改用 `root_dir` 参数化实现 |
| **可扩展性与依赖注入** | [#4135](https://github.com/OpenHands/software-agent-sdk/pull/4135) | 为 `RemoteConversation` 增加可注入的 WebSocket client 工厂，解除模块级单例硬编码 |
| **成本与可观测性** | [#4490](https://github.com/OpenHands/software-agent-sdk/pull/4490)、[#4703](https://github.com/OpenHands/software-agent-sdk/pull/4703) | DeepSeek prompt cache 命中计入 telemetry；LLM 生成对话标题时去除 inline reasoning 块 |
| **性能优化** | [#4697](https://github.com/OpenHands/software-agent-sdk/pull/4697) | 将 `EventLog.append` 从 O(conversation length) 降为 O(1)，避免长对话场景下每次追加全量扫描 |
| **平台适配** | [#4502](https://github.com/OpenHands/software-agent-sdk/pull/4502)、[#4550](https://github.com/OpenHands/software-agent-sdk/pull/4550) | Windows 上优先使用 Playwright 自管 Chromium；Azure OpenAI API 版本更新至 2025-03-01 |
| **数据模型完善** | [#4470](https://github.com/OpenHands/software-agent-sdk/pull/4470)、[#4566](https://github.com/OpenHands/software-agent-sdk/pull/4566) | TaskTracker 引入稳定任务 ID 并持久化；`load_memory` 偏好传播到所有启动路径 |

项目整体处于"功能开发快、合并上版慢"的错位状态。27 个待合并 PR 背后是大量已完成验证的代码，但项目主干实际推进幅度有限。

---

## 4. 社区热点

### 最受关注 Issue：#4663 — glob fallback 修改进程级 cwd（3 条评论）

[#4663 [Bug]: Python glob fallback mutates the process-wide working directory](https://github.com/OpenHands/software-agent-sdk/issues/4663)

该 Issue 由 `@enyst` 提交，指出 `glob` 工具的 Python fallback 实现（`impl.py:185-231`）通过 `os.chdir(search_path)` 实现相对路径匹配，这在并发执行器场景下会与无关线程产生竞态。3 条评论是今日全项目最高讨论量，说明**全局状态污染**问题在 SDK 用户中引起了共鸣——涉及 `cwd` 的修改不仅影响当前工具调用，还会波及进程内所有并发任务。该问题已由 PR #4707 提出修复，且修复方案（改用 `root_dir` 参数而非恢复 `cwd`）在思路上比原实现更彻底——它从根上消除了对全局状态的修改，而非"改完再改回来"。

### 值得关注的联动讨论：#4708 ↔ #4135

[#4708 [Feature]: Injectable WebSocket client factory for RemoteConversation](https://github.com/OpenHands/software-agent-sdk/issues/4708) 与对应的 [PR #4135](https://github.com/OpenHands/software-agent-sdk/pull/4135) 已经共存超过一个月（PR 创建于 2026-07-17）。Issue 提出 `RemoteConversation` 在 `__init__` 中直接构造 `WebSocketCallbackClient`，用户无法注入自定义 transport 实现。PR 已附带完整测试证据并标注"ready for review"，但至今未合并。这反映出社区对**可扩展性**的诉求与维护者合并节奏之间存在张力。

---

## 5. Bug 与稳定性

今日 5 条 Issue 中有 4 条为 Bug 报告，1 条为功能请求。按严重程度排列如下：

### 高风险：运行时资源回收缺陷

**[#4695] token deltas 不再重置运行时空闲计时器，长流式任务可能造成 pod 被回收**
[链接](https://github.com/OpenHands/software-agent-sdk/issues/4695) | 作者: @VascoSch92 | 优先级: medium

PR #4689 将流式 delta 投递改为 opt-in 后，`_EventSubscriber` 未订阅 streaming deltas，导致**长流式任务中持续产生的 token delta 不会重置运行时空闲计时器**，部署平台可能误判会话空闲而回收 pod。这是典型的"重构引入的回归"——功能正确但生命周期信号丢失。目前没有对应的修复 PR。

### 高风险：并发安全 — 进程级全局状态污染

**[#4663] glob fallback 修改进程级 cwd**
[链接](https://github.com/OpenHands/software-agent-sdk/issues/4663) | 作者: @enyst | 评论: 3

`os.chdir` 是进程级操作，对它的修改在并发 executor 下会干扰所有共享该进程的代码。**修复 PR #4707 已提交，正处于待合并状态**。该修复采用了比原实现更稳健的方案——彻底移除对 `cwd` 的读写，而非依赖事后恢复。

### 中风险：状态持久化导致语义过期

**[#4709] AgentContext.current_datetime 序列化到 settings.json，导致提示词中 CURRENT_DATETIME 过期**
[链接](https://github.com/OpenHands/software-agent-sdk/issues/4709) | 作者: @RobG-git

`current_datetime` 默认值为 `datetime.now().astimezone()`，但该值被持久化到 settings.json 后，后续加载会使用旧时间戳，导致 prompt 中的 `CURRENT_DATETIME` 严重过期。这是**状态持久化边界设计问题**——动态计算值不应与用户配置混存。目前无对应修复 PR。

### 中风险：MCP 集成校验错误

**[#4705] GitHub MCP 工具缺少 inputSchema，导致任务列表与自动化页面状态不一致**
[链接](https://github.com/OpenHands/software-agent-sdk/issues/4705) | 作者: @S-zhi

Agent Canvas 自动化中使用 GitHub MCP 工具时，日志视图报 44 条验证错误——所有 GitHub MCP 工具均缺少 `inputSchema`。问题同时影响任务列表和自动化页面的展示一致性和执行状态。目前无对应修复 PR。

---

## 6. 功能请求与路线图信号

今日唯一明确的功能请求：

**[#4708] 可注入的 WebSocket client 工厂**
[链接](https://github.com/OpenHands/software-agent-sdk/issues/4708) | 作者: @p1c2u | 标签: enhancement, ready-for-dev

`RemoteConversation` 硬编码构造 `WebSocketCallbackClient` 限制了自定义 transport 的接入。对应 PR #4135 已完成并待合并（已等待 44 天），**该功能被纳入下一版本的概率很高**，前提是维护者推进合并。

结合待合并 PR 的完整列表，以下方向有可能进入下一版本：

- **自定义标题生成提示词**（[#4564](https://github.com/OpenHands/software-agent-sdk/pull/4564)）：允许用户自定义 LLM 标题生成的 prompt；
- **稳定任务标识符**（[#4470](https://github.com/OpenHands/software-agent-sdk/pull/4470)）：TaskTracker 持久化稳定 task ID，兼容旧版无 ID 的 TASKS.json；
- **dev.openhands 扩展命名空间**（[#4496](https://github.com/OpenHands/software-agent-sdk/pull/4496)）：将 client 扩展 map 到统一命名空间下，并清理重复代码；
- **仓库访问预检**（[#4504](https://github.com/OpenHand

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-30

> 数据口径：2026-08-29 00:00 UTC 至 2026-08-30 00:00 UTC（GitHub API 快照）

---

## 1. 今日速览

过去 24 小时 LiteLLM 项目保持**极高活跃度**：Issues 更新 50 条（新开/活跃 35、关闭 15），PR 更新 232 条（待合并 140、已合并/关闭 92），合并/关闭率达 40%，表明核心团队与外部贡献者均在高频推进代码合入。今日无新版本 Release，但 PR 流中出现了多处涉及 1.99.0 rc 的修复回移，暗示 1.99.0 正式版发布前的收敛工作正在进行。值得关注的是，dashboard 计费显示、MCP 工具自动执行、Gemini 3 参数兼容等问题仍在社区中引发持续讨论，其中部分老 issue（如 #11929）在关闭后仍保持高评论热度。

---

## 2. 版本发布

**无新版本发布。**

当前可见的预发布收敛信号：
- PR #38821 将 13 个 shadcn 迁移回归修复回移到 **rc/1.99.0** 分支，说明 1.99.0 RC 阶段存在已知 UI 回归（暗色模式不可读、下拉/弹出框行为异常），正式版预计将包含这批修复。
- PR #38805 正在将内部 staging 分支提升至 main，属于常规发布前同步。

如你是 1.99.0 rc 用户，建议关注上述两个 PR 的合并状态后再决定是否升级。

---

## 3. 项目进展

今日 PR 总数 232 条，其中 92 条已合并或关闭。受数据展示限制，以下基于可见的 20 条高评论 PR 样本概括进展方向：

**已关闭/合并的值得注意 PR：**

- [#38807 fix(cost): treat a zero rate as a price when selecting a cost metric](https://github.com/BerriAI/litellm/pull/38807) — 修复 `select_cost_metric_for_model` 按真值判断导致**零费率被跳过**的问题。对使用 `input_cost_per_character: 0` 这类显式零定价的模型（常见于部分 embedding 或促销模型）成本计算会恢复正确。

- [#38013 feat(anthropic): workload identity federation, pluggable identity sources, and provider-level setup](https://github.com/BerriAI/litellm/pull/38013) — 虽最终关闭，但其内容已在 [#38818](https://github.com/BerriAI/litellm/pull/38818)（内部副本，仍 OPEN）中延续，目标是为 Anthropic 直连增加 Workload Identity Federation（WIF）支持，摆脱长期静态 `sk-ant` 密钥。这是企业级认证能力的重要补齐，与 Vertex/Azure 已有的联合身份体系拉齐。

**主要进行中的功能推进（OPEN PR）：**

| 方向 | PR | 说明 |
|---|---|---|
| **可观测性** | [#38822](https://github.com/BerriAI/litellm/pull/38822) | UI Logging & Alerts 页面展示运行时回调（runtime callback），运行时注册的回调以只读方式合并展示 |
| **路由与治理** | [#38784](https://github.com/BerriAI/litellm/pull/38784) | 模型访问组（model access group）级别共享预算，无需逐个 key 手动输入 |
| **安全策略** | [#38788](https://github.com/BerriAI/litellm/pull/38788) | 流式响应也执行 post_call guardrail 管道，此前流式请求一律被 400 拒绝 |
| **流式体验** | [#38787](https://github.com/BerriAI/litellm/pull/38787) | 原生流式响应增加上游计时 HTTP 头；此前 Gemini native stream 在 header 发出前即返回 |
| **模型兼容性** | [#38792](https://github.com/BerriAI/litellm/pull/38792) | OpenAI Responses API 工具 schema 顶层 anyOf/oneOf/allOf 扁平化，修复 Codex MCP 工具 400 |
| **成本准确性** | [#38820](https://github.com/BerriAI/litellm/pull/38820) | 修复 Together AI 服务端同步把 `context_length` 误写为 `max_output_tokens`（28 个模型虚标 1M 级输出上限） |
| **稳定性** | [#38819](https://github.com/BerriAI/litellm/pull/38819) | Gemini TTS 不再把 `response_format` 当 chat 参数透传（此前必现 500） |

**整体判断**：LiteLLM 正处于 "功能面拓宽 + 兼容性修补 + 1.99.0 发布前收尾" 三线并行的状态。Anthropic WIF、共享预算、流式 guardrail 均是面向企业客户的关键能力，预计会随 1.99.x 或 2.0 进入正式版本。

---

## 4. 社区热点

今日讨论热度集中在以下 issue：

**TOP 1： [#11929 Usage Dashboard: Two Issues with Spend Reporting and Failed Request Attribution](https://github.com/BerriAI/litellm/issues/11929)**（15 条评论，已关闭）
- 前端分页导致总花费严重低估；后端失败请求显示 0 归属错误。
- 该 issue 已标记 stale 并关闭，但 15 条评论的高热度说明财务数据准确性是用户最敏感的痛点。关闭可能意味着修复已合入，但社区仍在观望验证。

**TOP 2： [#37031 MCP auto-execute (require_approval "never") hijacks client-side tool_use from agentic clients like Claude Code](https://github.com/BerriAI/litellm/issues/37031)**（7 条评论，OPEN）
- 配置了 `require_approval: "never"` 的 MCP 工具会劫持 Claude Code 客户端自身的工具调用（Read/Bash/Edit），导致所有非 MCP 工具报 "Error executing tool"。
- 这是 MCP Gateway 能力与 agentic 客户端共存的架构性冲突，涉及执行语义的边界划分，短期内需要明确的设计决策。

**TOP 3： [#27944 Anthropic batch costs always 0 — transform_file_content_request routes msgbatch_* IDs to wrong endpoint](https://github.com/BerriAI/litellm/issues/27944)**（6 条评论，已关闭）
- `CheckBatchCost` 对已完成 Anthropic batch 始终记录 0 token / $0 成本，原因是 `msgbatch_*` ID 被路由到错误 endpoint。
- 与 [#30635](https://github.com/BerriAI/litellm/issues/30635)（batch 成本 403 无法追踪）共同指向 **batch API 成本追踪**是长期被诟病的薄弱环节。

共性洞察：社区最关注的是 **"钱算得准不准"** 和 **"agentic 工具链能不能无缝工作"** 两件事，前者关乎信任，后者关乎生态兼容。

---

## 5. Bug 与稳定性

按严重程度排列：

### 高严重度

- **[#38731 litellm stops forwarding model requests](https://github.com/BerriAI/litellm/issues/38731)**（OPEN，8/29 新建）
  - 现象：1.97.0 容器化部署中，通过 mgmt API 自动创建/删除 ephemeral key 后，litellm 停止转发所有模型请求。
  - 影响面：生产级阻塞问题，尚无可用的 workaround，急需维护者确认是否为 1.97.0 回归。
  - **无关联 fix PR**。

- **[#38732 delete key confirmation dialog should ignore surrounding whitespace](https://github.com/BerriAI/litellm/issues/38732)**（OPEN，8/29 新建）
  - 现象：key 名不允许前后空格，但删除确认对话框要求输入 key 名时未忽略空格，导致用户无法输入匹配文本、无法删除 key。
  - 影响面：UI 操作阻塞，但目前仅 1 条评论，尚未大面积反馈。
  - **低风险修复，无关联 PR**。

### 中高严重度

- **[#38663 fix(gemini): do not inject temperature for Gemini 3 models when omitted](https://github.com/BerriAI/litellm/issues/38663)**（OPEN，8/28 新建，2 评论）
  - `VertexGeminiConfig.map_openai_params` 对 Gemini 3.x 在调用方未传 temperature 时强制注入 `1.0`，与 Google 新行为冲突（Gemini 3 可能默认应为 `0` 或采用模型默认），影响 Google AI Studio 与 Vertex 两条路径。
  - 已有明确修复方向，**尚无关联 PR**。

- **[#36168 streaming drops upstream usage when the final chunk has a non-empty choices array](https://github.com/BerriAI/litellm/issues/36168)**（OPEN，8/7 创建，2 评论）
  - 流式响应末 chunk 同时含 `choices` 与 `usage` 时 usage 被丢弃，导致 `cached_tokens` 丢失、成本按全量输入计费。
  - 这是 #28735 的镜像问题（入口 vs 出口），说明 streaming 场景下 usage 处理存在系统性缺陷，涉及计费准确性。
  - **无关联 fix PR**。

### 中严重度

- **[#11929 Usage Dashboard spend/page bug](https://github.com/BerriAI/litellm/issues/11929)**（CLOSED）— dashboard 分页少报花费 + 失败请求归属为 0。已关闭但建议维护者在 release notes 中明确说明修复版本。
- **[#36548 LoggingWorker strands task when event loop changes](https://github.com/BerriAI/litellm/issues/36548)**（OPEN，8/11 创建）— 多事件循环环境中 `LoggingWorker._ensure_queue` 不取消旧任务即丢弃队列，可导致日志丢失或任务泄漏。多线程部署下必现。
- **[#37622 Least busy routing not balanced](https://github.com/BerriAI/litellm/issues/37622)**（OPEN，8

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 开源项目日报 — 2026-08-30

## 今日速览

过去 24 小时，Temporal 项目活跃度保持高位：共 18 条 PR 更新（其中 1 条关闭），1 条 Issue 更新（已关闭），无新版本发布。开发焦点集中在测试基础设施（stephanos 系列 PR）、worker 命令调度可配置性（#11863、#11851）以及 PostgreSQL 可见性过滤 bug 修复（#11860）。项目已启动 1.32.0 版本发布准备工作（#11861），但正式版本尚未发布。整体来看，项目处于活跃开发与发布过渡期，稳定性与开发者体验并进。

## 项目进展

今日唯一合并/关闭的 PR 为 **#11861 [CLOSED] 1.32.0: Prepare release branch**，由 CI 机器人创建，内容为覆盖治理文件和更新依赖。该 PR 关闭标志着 1.32.0 发布分支已准备就绪，后续将进入版本发布周期。其余 17 条 PR 仍处于开放状态，多为正在 review 或测试中的改进，尚未提交合并，项目核心功能推进主要依靠新 PR 的持续提交。

## 社区热点

- **Issue #11718 [CLOSED] [enhancement] Provide the temporal development cli in the release archive** — 评论数 3，是今日唯一有明确评论量的条目。用户 @sinux-l5d 提出希望 release archive 中包含 `temporal development cli`，以便通过 Mise 等工具直接管理依赖。该 Issue 已于 24 小时内关闭，推测可能被纳入版本发布计划或得到替代方案。其背后反映了开发者对开箱即用、与本地工具链无缝集成的强烈需求。  
  [链接](https://github.com/temporalio/temporal/issues/11718)

- **PR #11863 与 #11851**：围绕 worker 命令调度的超时与重试机制，属于运维可调性改进，虽无评论数据，但讨论热度可能较高，因直接影响集群故障恢复效率。  
  [#11863](https://github.com/temporalio/temporal/pull/11863) | [#11851](https://github.com/temporalio/temporal/pull/11851)

## Bug 与稳定性

1. **[高] PostgreSQL 可见性过滤器 bug** — **#11860**：当过滤值含问号（如 `WorkflowId = 'foo?-value'`）时，PostgreSQL 查询失败并报 `could not determine data type of parameter $1 (42P18)`。该 PR 定位到 visibility converter 的 SQL 参数处理问题，可视为重要功能修复。  
   [链接](https://github.com/temporalio/temporal/pull/11860)

2. **[中] worker 命令调度延迟** — **#11851**：当 worker 不存在时，每次 `DispatchNexusTask` 会阻塞 goroutine 10 秒。该 PR 停止对 poller timeout 的重试，仅重试传输层错误，显著缩短故障检测时间。  
   [链接](https://github.com/temporalio/temporal/pull/11851)

3. **[中] worker 命令超时/重试不可配置** — **#11863**：将 `DispatchTimeout` 与 `MaxTaskAttempts` 从常量改为动态配置，默认值由 10s/3 次调整为 5s/30 次，提升高并发下的韧性。  
   [链接](https://github.com/temporalio/temporal/pull/11863)

4. **[低] pending trigger 排序不确定性问题** — **#11859**：修复 `convertBackfillersCHASMToLegacy` 中 map 遍历顺序导致的不确定性，改为基于 ID 的稳定排序，避免因随机迭代而产生非确定性行为。  
   [链接](https://github.com/temporalio/temporal/pull/11859)

5. **测试稳定性改进系列**：stephanos 提交了多个 PR（#11826、#11865、#10781、#11766、#11864、#11830），优化 Await 轮询、超时诊断和测试上下文缓存，虽非生产 bug，但有助于减少 flaky 测试和提升 CI 可靠性。

## 功能请求与路线图信号

- **#11347**：允许任务队列达到 `MaxTaskQueues` 限制时，为已有 TaskQueue 注册新的任务队列类型，同时保留真正新家族的限制错误。该功能增强了动态配置弹性，可能被纳入后续核心调度能力。  
  [链接](https://github.com/temporalio/temporal/pull/11347)

- **#11855**：允许将用户批处理操作委托给 admin batch（通过 tdbg 在 temporal-system 命名空间中执行），特定场景下帮助用户在命名空间受限时取消工作流等操作。  
  [链接](https://github.com/temporalio/temporal/pull/11855)

- **#11566** / **#11520**：关于 worker callback 功能增强（可配置 callback 种类、填充 `CallbackInfo.outcome`），属于长线特性，目标合并到 `feature/worker-callbacks` 分支。  
  [#11566](https://github.com/temporalio/temporal/pull/11566) | [#11520](https://github.com/temporalio/temporal/pull/11520)

- **#10227**：改进 CLI 全局参数位置错误时的提示信息，降低新手使用门槛，开发体验友好。  
  [链接](https://github.com/temporalio/temporal/pull/10227)

## 用户反馈摘要

- 来自 **#11718** 的用户反馈：用户使用 Mise 管理项目依赖，期望直接从 release archive 安装 temporal development CLI，无需额外构建步骤。该需求透露出用户对标准化、可脚本化的开发环境搭建的渴望，也反映了当前分发包在可迁移性上的差距。  
  [链接](https://github.com/temporalio/temporal/issues/11718)

## 待处理积压

以下 PR 长期未合并，需维护者关注：

- **#10128 [stale] Bump defaultCliVersion to 1.7.0**：自 2026-04-29 创建，已标记为 stale，目标是将 CLI 版本从 1.6.1 提升至 1.7.0。该更新可能因时间推移已过期，需要重新评估或关闭。  
  [链接](https://github.com/temporalio/temporal/pull/10128)

- **#10227**：CLI 全局参数提示改进，已存在 3 个月以上，原因为“等待 review”。建议维护者确认优先级。  
  [链接](https://github.com/temporalio/temporal/pull/10227)

- **#10781**：Timeout diagnostics 系列 PR 之一，自 2026-06-19 开放，已进入堆叠依赖状态，需关注其前置依赖合并情况。  
  [链接](https://github.com/temporalio/temporal/pull/10781)

- **#11520**：CallbackInfo.outcome 填充功能，已开放近 3 周，且为堆叠 PR，需持续跟踪其基线分支 `chrsmith/wc-add-worker-cb-variant` 的进度。  
  [链接](https://github.com/temporalio/temporal/pull/11520)

---

**项目健康度评估**：活跃度优秀，社区贡献持续输入，版本流程启动；需关注长期未合并 PR 的积压风险，以及测试改进系列与发布计划的协调。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*