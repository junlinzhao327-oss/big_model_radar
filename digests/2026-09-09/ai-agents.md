# OpenClaw 生态日报 2026-09-09

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-08 22:35 UTC

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

# OpenHands SDK 项目动态日报 — 2026-09-09

## 1. 今日速览

过去 24 小时项目活跃度维持高位：29 条 Issue 更新（19 条新开/活跃、10 条关闭），50 条 PR 更新（47 条待合并、3 条已合并/关闭）。值得注意的是，9 月 8 日集中涌现了大量由 AI 代理（OpenHands）代用户创建的高质量 Issue，涵盖动态属性访问清理（#4902–#4905）、ACP 子进程孤儿（#4910/#4901）、MCP 断连处理（#4891）等，说明项目正在被“自举”使用且反馈链路畅通。另有 Release v1.46.0 的发布 PR（#4908）正在准备中，但尚无正式版本发布。

- **活跃度**：高。Issue + PR 合计 79 条更新，远超日常均值。
- **健康度信号**：安全/稳定性类 Issue 占比偏高（容器崩溃、API key 丢失、进程孤儿等），但多数已被标记 ready-for-dev 或有对应修复 PR，响应速度良性。
- **隐患**：多个 1–4 月创建的老 Issue（#4245、#4246、#4247、#4250 等）仍处于 needs-triage/开放状态，积压清理节奏待加快。

## 2. 版本发布

**无正式 Release**。但 [PR #4908: Release v1.46.0](https://github.com/OpenHands/software-agent-sdk/pull/4908) 已进入发布流程，版本号已设为 1.46.0，集成测试、行为测试、安全扫描等检查项均已勾选，由 @juanmichelini 启动、@all-hands-bot 执行发布。若该 PR 合入，v1.46.0 将成为下一个公开版本。

## 3. 项目进展

数据中未单独列出“已合并 PR”明细（仅给出总数 3），但通过今日关闭的 10 条 Issue 可以确认以下修复已落地或合入主分支：

| 关闭 Issue | 关联修复 | 意义 |
|---|---|---|
| [#4896](https://github.com/OpenHands/software-agent-sdk/issues/4896)：ChatGPT 订阅 profile 预检失败（high priority） | 修复已完成 | 恢复 ChatGPT OAuth 订阅用户在预检保存 LLM profile 时的正确鉴权 |
| [#4817](https://github.com/OpenHands/software-agent-sdk/issues/4817)：LLM span 成本忽略 prompt-cache tokens | 修复已完成（含 #4816） | LLM 可观测性成本核算与 provider 实际账单对齐 |
| [#4816](https://github.com/OpenHands/software-agent-sdk/issues/4816)：自定义 `litellm_proxy/*` 模型成本记录为 $0 | 修复已完成 | 统一 native/ACP 两条路径的模型成本估算 |
| [#4255](https://github.com/OpenHands/software-agent-sdk/issues/4255)、[#4256](https://github.com/OpenHands/software-agent-sdk/issues/4256)、[#4257](https://github.com/OpenHands/software-agent-sdk/issues/4257) | 老 Bug 清理关闭 | Ollama 超时、Chromium sandbox、沙箱预览链接等历史问题收尾 |
| [#4261](https://github.com/OpenHands/software-agent-sdk/issues/4261)：RemoteWorkspace host 校验缺失（CRITICAL 安全审计） | 审计后关闭 | Fork 审计中发现的 egress 风险已完成评估处理 |
| [#3992](https://github.com/OpenHands/software-agent-sdk/issues/3992)：弱模型因非对称响应分发被终止 | 关闭 | 弱模型/本地模型兼容性讨论收敛 |

此外，当前有 47 条 PR 待合并，其中多条的修复范围对项目路线图有实质意义：代理云运行时请求（#4878）、云沙箱 resume 后客户端重定向（#4770）、StreamingDeltaEvent 解耦重构（#4700）、DeepSeek prompt-cache 遥测（#4490）等。

## 4. 社区热点

| Issue | 评论数 | 主题 |
|---|---|---|
| [#4248](https://github.com/OpenHands/software-agent-sdk/issues/4248) | 15 | `execute_bash` 报 “Missing required parameters: security_risk”，发生在 deepseek-reasoner 上 |
| [#3992](https://github.com/OpenHands/software-agent-sdk/issues/3992) | 14 | 无 tool-call 的内容响应处理不对称导致弱模型 agent 被终止 |
| [#4245](https://github.com/OpenHands/software-agent-sdk/issues/4245) | 12 | agent-server Webhook 连接失败导致容器崩溃和沙箱连接错误 |
| [#4246](https://github.com/OpenHands/software-agent-sdk/issues/4246) | 12 | MCP 工具初始化超时且界面无任何反馈，agent 空转 |
| [#4255](https://github.com/OpenHands/software-agent-sdk/issues/4255) | 10 | Ollama 场景超过 300 秒任务被强杀，UI/settings.json 修改无效 |

**热点评论的动态分析**：本次评论前五的 Issue 存在一个共同特征——均由第三方模型或自托管生态用户触发，反馈集中在两类诉求：

1. **本地模型兼容性**（#4248、#3992）：主流 LLM API 行为差异（如 deepseek-reasoner 缺少 security_risk 参数、弱模型不输出 tool_calls）正在让 SDK 的假设面临挑战，用户期待更宽容的模型适配层。
2. **自托管稳定性**（#4245、#4246）：Webhook 断连与 MCP 超时都表现为“进程崩溃 / 无感知静默失败”，暴露出错误上报和可恢复性设计的不足。

## 5. Bug 与稳定性

按严重程度排序：

### 🔴 严重 — 安全 / 数据风险

| Issue | 标题 |

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，这是 2026-09-09 的 Pi 项目动态日报。

---

## Pi 项目动态日报 (2026-09-09)

### 1. 今日速览

Pi 项目在过去 24 小时处于高活跃度状态。Issue 处理效率极高，关闭了 61 个问题，同时新增/活跃 11 个，总量达 72 条；PR 方面也有 14 个被合并/关闭，4 个待处理。虽然今日没有新版本发布，但从合并的 PR 与关闭的 Issue 来看，项目在 bug 修复、依赖更新、终端兼容性等方面均取得实质进展，呈现出健康、维护者响应迅速的良好态势。众多高讨论度的 bug 在社区反馈后很快被处理（如 #8919、#8717），体现了高效的社区协作。值得注意的是，围绕 `opencode-go` 新安全头（x-opencode-session）引发的连锁问题（#9230, #9290, #9302）是当前影响第三方集成稳定性的集中点。

### 2. 版本发布

无。

### 3. 项目进展

今日合并/关闭的 PR 展示了项目在多方面的快速迭代：

- **运行时依赖与安全更新**：PR #9341 更新了多项运行时依赖（包含 `minimatch`），并保留关键依赖版本，确保依赖安全与稳定。([#9341](https://github.com/earendil-works/pi/pull/9341))
- **稳定性修复（Compaction 与上下文显示）**：PR #9337 修复了三个已在下游 fork 中验证的 bug：Case 3 compaction 触发评估错误、`getContextUsage` 在失败/中止回合中的显示、以及相关边界情况。该 PR 将这些修复统合移植回主线，避免其随 fork 更新而被丢弃。([#9337](https://github.com/earendil-works/pi/pull/9337))
- **多项 UI 问题快速修复**：PR #9316 合并了三个独立修复：
  - 修复全屏模式下自定义 footer 占位空行的问题（closes #8919）。
  - 修复扩展提供的 header/footer 组件无法折叠的问题（#8717）。
  - 修复另一个相关 UI 组件尺寸说明问题（#8720）。([#9316](https://github.com/earendil-works/pi/pull/9316))
- **用户体验改进**：
  - PR #9303 修复了通过会话选择器恢复会话时没有用户反馈的问题。该选择器现在会在会话实际恢复完成后再关闭，避免用户误以为操作失败。([#9303](https://github.com/earendil-works/pi/pull/9303))
  - PR #9310 修复了全屏模式下切换会话后，先前文本选择残留到新会话的错误。([#9310](https://github.com/earendil-works/pi/pull/9310))
- **第三方工具生态适配**：PR #8627 让 read、write、edit、grep 等所有与 cwd 相关的内置工具支持使用扩展上下文中的真实会话 cwd (`ctx.cwd`) 进行路径解析，使扩展工具的行为与内置工具保持一致。([#8627](https://github.com/earendil-works/pi/pull/8627))
- **终端兼容性增强**：多个 PR 针对新出现的 Orca 终端进行了适配，包括支持 Kitty 图片协议（#9329）和 OSC 8 超链接（#9307）。两个 PR 目前仍处于开放状态。([#9329](https://github.com/earendil-works/pi/pull/9329)) ([#9307](https://github.com/earendil-works/pi/pull/9307))
- **Bug 修复**：PR #9319 修复了在自定义组件缺失 `invalidate` 方法时，主题变化可能引发崩溃的问题。([#9319](https://github.com/earendil-works/pi/pull/9319))

### 4. 社区热点

今日讨论热度最高的 Issues 揭示了 Pi 用户群的多方面诉求：

- **#5363：对更多模型提供商支持的需求**（19条评论，15 👍）：要求新增 `amazon-bedrock-mantle` provider。作者基于使用经验，指出现有 bedrock provider 基于 Converse API，无法用于模型 Mantle 的 OpenAI 兼容 Responses API。该问题自 6 月提出且持续获得关注，目前标记为 `[inprogress]`，说明开发者重视对主流云服务商新型 API 的适配。([Issues #5363](https://github.com/earendil-works/pi/issues/5363))
- **#7444：关键基础设施稳定性问题**（10条评论）：WebSocket 重试机制仅针对 2 个错误码实现，其他瞬时 `response.failed` 错误会直接使一轮操作硬停止。这会导致在不可靠网络下，用户经常性遇到任务中断，是影响 agent 核心体验稳定性的潜在 bug。([Issues #7444](https://github.com/earendil-works/pi/issues/7444))
- **#8823：用户界面的响应性问题**（10条评论）：用户汇报按 Esc 键取消流式输出时经常失灵，请求会持续到 Provider 自行结束。这违背了用户预期，被认为是交互控制不畅的严重问题。([Issues #8823](https://github.com/earendil-works/pi/issues/8823))
- **#9052：界面模式偏好与微调诉求**（7条评论，3 👍）：社区成员对全屏模式固定输入框表示认可，但介意滚动速度慢，希望滚动效率能向普通模式看齐。此类问题虽不关乎核心功能，却深刻影响用户体验的满意度。([Issues #9052](https://github.com/earendil-works/pi/issues/9052))
- **#7010：开发者生态的标准规范性**（7条评论）：请求将 OpenAI 兼容的 chat-completions providers 的可选对象 tool schemas 进行规范化。这属于第三方开发工具链的细节问题，但常给使用结构化输出的开发者带来困扰。([Issues #7010](https://github.com/earendil-works/pi/issues/7010))

### 5. Bug 与稳定性

今日报告的 Bug 按严重程度排列如下：

- **严重（崩溃/数据损坏）**：
  - **#9276：grep 工具在上下文行数开启时可致 OOM**：当 `grep` 工具匹配到大量日志文件时，进程会因堆内存溢出而崩溃。问题已确认并标记为 Bug，目前无相关 PR。([Issues #9276](https://github.com/earendil-works/pi/issues/9276))
  - **#8667：Stale compaction 条目导致会话永久损坏**：一次在工具调用执行期间触发的自动 compaction 事件会将会话树永久置于不合法状态，导致后续任何调用都报 Anthropic 400 错误。该问题最终被标记为 `[closed]` 处理，但文档应记录该风险。([Issues #8667](https://github.com/earendil-works/pi/issues/8667))
  - **#9340：`AgentSession.abort()` 不能阻止其后自动 compaction**：外部宿主在 abort 后报告的进程回收仍可能触发自动压缩，这可能引入意外状态。([Issues #9340](https://github.com/earendil-works/pi/issues/9340))

- **高（核心功能失效）**：
  - **#9212：Sonnet-5 经网关 13% 的编辑工具调用被截断**：工具参数在验证时解析显示为截断的空数组，如 `edits:[{}]`。这意味着模型输出触发生成过程，但在解析时被错误处理。这将直接导致大量模型调用失败。([Issues #9212](https://github.com/earendil-works/pi/issues/9212))
  - **#8706：Z.AI GLM 模型“强制思考”逻辑泄漏推理内容**：即使关闭思维链，强制思考模型仍会在输出结构中传入开关，导致输出包含不应有的推理内容，影响正常功能。该 Issue 已关闭，但需注意模型兼容逻辑。([Issues #8706](https://github.com/earendil-works/pi/issues/8706))
  - **#7444：WebSocket 重试机制覆盖不足**：见上文社区热点，该问题对网络波动环境下的可靠性有显著影响。([Issues #7444](https://github.com/earendil-works/pi/issues/7444))

- **中（体验减退/功能异常）**：
  - **#8823：Esc 无法可靠取消流式请求**：看似低优先级，实则会重度降低用户对主动权的掌控感。([Issues #8823](https://github.com/earendil-works/pi/issues/8823))
  - **#9339：全屏编辑器硬件光标错位闪烁**：在特定的 IME 配置及渲染器下，硬件光标无法定位到假光标位置，破坏输入体验。([Issues #9339](https://github.com/earendil-works/pi/issues/9339))
  - **#7445：`openai-responses` 中 Developer Role 的启用逻辑错误**：系统提示词的角色选择应仅取决于 provider 功能，而非由模型 `reasoning` 参数间接决定。([Issues #7445](https://github.com/earendil-works/pi/issues/7445))

- **低（扩展/API 失衡）**：
  - **#9290 / #9230：`opencode-go` 模型缺少新的 x-opencode-session 头**：导致所有第三方扩展与主项目发往 opencode-go 的请求在 2026-09-06 之后失败。相关补丁在社区有更高的应用优先级。([Issues #9290](https://github.com/earendil-works/pi/issues/9290)) ([Issues #9230](https://github.com/earendil-works/pi/issues/9230))
  - **#9302：out-of-loop 摘要过程无法获取必要的 provider 头**：这直接导致在 opencode 系列模型上，分支摘要与上下文压缩操作全部失败，无可用变通方案。([Issues #9302](https://github.com/earendil-works/pi/issues/9302))

**已有对应 fix PR 的 Bug**：
- **#8919** 已由 PR #9316 修复。
- **#8717** 已由 PR #9316 修复。
- **#8720** 已由 PR #9316 修复。
- **#8409** 相关修复在开放中的 PR #8635 中实现，主要针对暂停中的 tool 执行结束后的中断传递问题。

### 6. 功能请求与路线图信号

- **新 Provider 适配（基于 #5363）**：存在对 Bedrock Mantle 此类更贴近未来模型服务的 OpenAI 兼容终端的支持需求。该 PR 已提出一段时间，并标记为进行中，说明维护方判断其有纳入下一步路线图的价值。([Issues #5363](https://github.com/earendil-works/pi/issues/5363))
- **Provider 反馈的“标准化”趋势（PR #9345）**：新增抽象层让 providers 提供用量报告。首个实现是 Anthropic OAuth 适配器。这是一个能提升 Pi 费用透明度的前瞻性功能，有望被纳入后续版本。([PR #9345](https://github.com/earendil-works/pi/pull/9345))
- **成本核算优化（PR #6881）**：允许在响应头已包含成本的场景直接采用 Provider 报告的价格，避免依赖本地静态价格表判断。该 PR 目前开放且标记为 `[inprogress]`——印证了成本结构化、可靠化是项目的一个明确方向。([PR #6881](https://github.com/earendil-works/pi/pull/6881))
- **针对扩展 API 的更细粒度控制**：用户不只满足于“运行”。#9236 建议为扩展层增加“消息送达确认与幂等队列”，这属于消息可靠性的高级特征。这指示了一种倾向：Pi 可能在向平台级 agent 运行时的方向演进。([Issues #9236](https://github.com/earendil-works/pi/issues/9236))
- **非功能性性能优化建议**：
  - **#9267** 通过 `String.indexOf()` 降低模糊搜索的资源消耗。属于微小优化。([Issues #9267](https://github.com/earendil-works/pi/issues/9267))
  - **#7739** 建立早期启动延迟预算，目标是给使用者更接近于普通命令的“瞬间”体验。([Issues #7739](https://github.com/earendil-works/pi/issues/7739))
- **新协议支持预研（#9338）**：有提议让内置的 `kimi-coding` provider 尝试启用其新支持的、尚属半公开状态的 OpenAI 兼容 Responses API。这项如果实施，能扩大对一个活跃模型的适用性。([Issues #9338](https://github.com/earendil-works/pi/issues/9338))

### 7. 用户反馈摘要

从今日的评论中提炼出的真实用户痛点和场景如下：

- **“全屏模式下的滚动速度只有

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 开源项目日报 — 2026-09-09

## 1. 今日速览

过去 24 小时 Temporal 核心仓库整体处于**高度活跃**状态：PR 更新达到 45 条（待合并 28，已合并/关闭 17），主要集中在可靠性修复、worker callbacks 功能开发及 CI 基础设施改进；Issue 侧活跃度偏低（2 条），但其中 #11691 暴露出一个可导致集群永久丧失任务分发能力的严重 SQL 持久化缺陷，需高度关注。无新版本发布，项目重点在稳定性加固和内部架构演进。

---

## 2. 版本发布

**无新版本发布。**

---

## 3. 项目进展

今日无大型 feature 合入主线，但多笔修复与基础设施 PR 已关闭/合并，属于典型的“内部加固 + 问题修复”节奏：

- **#11955 [CLOSED]** — `[reliability-2026] fix: Don't block schedule rollback on a closed dummy sentinel` — 修复 schedulev2→v1 回滚时未正确依据 sentinel/15 分钟状态判断、导致回滚被阻塞的问题。该 PR 与下方 #11964 构成 V2-to-V1 迁移的完整修复链。
- **#11964 [CLOSED]** — `Simplify non-occupying workflow handling in schedule migration` — 将 schedule 迁移中 not-found 与 non-running 两种状态合并为单一非占用分支，简化回滚路径逻辑，作为对 #11955 review 意见的跟进。
- **#11929 [CLOSED]** — `Update to Go 1.27.0` — 工具链升级至 Go 1.27.0，完成编译链的现代化。
- **#8783 [CLOSED]** — `Revert "fix: make release dep check job always run on PRs"` — 撤回前序 CI 改动，因已验证可通过无需额外规则的方式确保 release 分支状态检查，属于 CI 策略简化。

整体而言，今日项目进展集中于 **schedule 迁移稳定性修复**与**工具链升级**，未引入新破坏性变更。

此外，若干值得关注的在途 PR 正待合并：

| PR | 方向 |
|---|---|
| #11971 | Cloud/v1.32.0 分支 cherry-pick（涵盖上述两项 schedule 迁移修复） |
| #11968 | 修复 SignalWithStart 在执行关闭后的 request ID 去重逻辑 |
| #11963 | 引入 chasm 流控库，推进 flow control 基础建设 |
| #11966 | 用原子 deadline 替换 per-limiter 刷新 timer，优化热点路径性能 |

---

## 4. 社区热点

今日 Issue/PR 评论区活跃度均较低（评论数普遍为 0-3），并未出现单点高热度的公开讨论。相对而言关注度最集中的为以下两个条目：

- **#11691**（👍 2, 评论 3）— [SQL session refresh can close the connection pool irrecoverably](https://github.com/temporalio/temporal/issues/11691)
  该 Issue 虽创建于 8 月 20 日，但过去 24 小时仍持续获得更新，是当前社区对可靠性缺陷关注度最高的条目。其影响面从 SQL 连接池管理延伸到“僵尸集群”判定问题，触及用户对分布式系统自愈能力的信任根基。

- **#11958**（评论 1）— [Fix ambiguities related to `chasmcallbackpb.CallbackState::request_id`](https://github.com/temporalio/temporal/issues/11958)
  虽为新开 Issue，但直接指向 CHASM Callback 协议中 request_id 字段的语义歧义，与当前 worker-callbacks 系列的 PR 工作直接相关，提请设计层面消除误用风险。

值得留意的还有多笔 worker callbacks 功能栈 PR（#11566、#11520、#11380），皆明确标注合入 feature 分支，显示出团队在该特性上正进行大规模、长期的栈式协作开发。

---

## 5. Bug 与稳定性

### 🔴 严重

- **#11691** — [SQL session refresh can close the connection pool irrecoverably](https://github.com/temporalio/temporal/issues/11691)
  现象：SQL session refresh 可能因 “sql: database is closed” 不可逆关闭连接池，随后 membership heartbeat 永久静默失败，集群对外误报 SERVING 但实际无法分发任何任务，形成 “zombie cluster”。
  影响：任何使用 SQL 持久化（如 MySQL/PostgreSQL）的 Temporal 部署，在网络抖动或存储重启后均可能触发；用户侧只能通过人工介入恢复。
  状态：未关闭，**尚无关联 fix PR**。Issue 摘要明确诉求：要么 session refresh 自愈全部自造错误状态，要么持续失败的 heartbeat 应 escalates（重建连接或终止进程交由 supervisor 重启），可视为对系统韧性设计的直接挑战。

### 🟡 中等

- **#11955 / #11964** — schedule V2→V1 回滚可能被 closed dummy sentinel 状态阻塞，导致快速回滚失败。已通过上述两 PR 修复，属于“reliability-2026”计划一部分，关闭即代表已修复。

### 🟢 低风险

- **#11968** — SignalWithStart 在原 workflow 关闭后重试，可能错误地重新启动新 run 或发送重复 signal。已有 [fix 等待审查](https://github.com/temporalio/temporal/pull/11968)，影响限于边界时序场景。

---

## 6. 功能请求与路线图信号

- **#11969 [OPEN][DRAFT]** — [Adds a feature to track and skip bad ES hostname IPs](https://github.com/temporalio/temporal/pull/11969)
  引入自定义 dial context + TTL 缓存，跳过不可达的 Elasticsearch IP，帮助 Temporal 从 AZ 分区故障中恢复。若合入，将显著提升 ES 后端的可用性韧性，适合纳入下一版本规划。

- **#11961 [OPEN]** — [Persistence fault injection](https://github.com/temporalio/temporal/pull/11961)
  在持久化层加入故障注入能力，与已有的 gRPC/HTTP 请求注入能力对齐。属于质量保障基础设施，便于上游开发者在测试中验证磁盘/数据库故障场景——这对 #11691 这类问题的提前发现与回归测试有直接价值。

- **#11965 [OPEN]** — [Make Nexus callback source header opt-in](https://github.com/temporalio/temporal/pull/11965)
  改变 callback URL 语义并允许配置 `callback.inspectSourceHeader`，该行为变更可能进入下一个 minor 版本，部署时需要关注配置项默认值变更。

- **#9948 [OPEN]** — [Add command to dump dynamic configuration values](https://github.com/temporalio/temporal/pull/9948)
  新增 `tdbg` 命令以转储动态配置值，用于调试与可观测性。虽搁置时间较长，但近期仍有更新，保持合入可能。

---

## 7. 用户反馈摘要

基于现有 Issue 评论，提炼如下真实用户痛点与诉求：

- **对故障自愈能力的强烈诉求（#11691）**：用户明确要求系统“要么恢复自身创建的错误状态，要么显式失敗（escalates）”。案例中集群表面上健康（SERVING）却无法处理任务对比鲜明，说明用户对健康检查有效性有较高期待，且对无告警的长期静默故障容忍度很低。该场景通常发生在 SQL 存储故障后的恢复窗口内，用户群体偏向自运维的中大型部署。

- **对协议字段语义精确性的持续关注（#11958）**：社区开发者（如 @chrsmith）在 CHASM Callback 设计中主动发起对 `request_id` 语义歧义（“foot gun”）的修正确认，说明参与贡献的开发者正积极推动设计质量，避免未来兼容性问题积压。

- **合并节奏相对审慎**：大部分发布时间较长的高价值 PR（#11380、#11520、#11566）仍滞留在功能分支等待整体代码完成，用户若希望尽早使用相关能力，需关注 worker-callbacks 特性主线的整体进度，而非个别 PR。

---

## 8. 待处理积压

以下高价值条目长期未获合入/响应，建议维护者优先审视：

- **#11691**（8 月 20 日创建，已 20 天）— SQL session refresh 导致集群性故障，至今无 fix PR 或官方回应，这是当前对生产环境危害最大的积压问题。
- **#9948**（4 月 14 日创建，近 5 个月）— tdbg 动态配置转储命令，长期功能缺失且实现已就绪，合入阻碍不明。
- **#11380**（7 月 31 日创建）— 新增 `commonpb.NexusHandler` callback 变体识别，作为 worker-callbacks 关键依赖，长期处于栈式等待状态。
- **#11492**（8 月 12 日创建）— “gradual connect shedding” 复制流量渐降能力，直接提升全球命名空间扩缩容体验，需明确推进计划。

---

**总体健康度评估**：Temporal 当前开发活跃度和工程纪律均处于良好状态，可靠性专项（reliability-2026）持续产出修复；主要风险面集中在 SQL 后端深层次故障自愈能力缺失（#11691）及一批高价值功能 PR 的长期滞留。建议关注未来 48–72 小时是否出现 #11691 关联修复 PR，以及 worker-callbacks 特性分支的合并窗口。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*