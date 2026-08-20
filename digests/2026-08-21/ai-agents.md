# OpenClaw 生态日报 2026-08-21

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-20 22:49 UTC

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

# AI 智能体与个人 AI 助手开源生态横向对比报告（2026-08-21）

> 说明：本次动态快照中，**OpenClaw** 与 **LiteLLM** 未提供具体数据（LiteLLM 仅有标题），因此本报告以 **Hermes Agent、OpenHands SDK、Pi、Temporal** 四个项目的实际数据为主进行量化分析，其余两个项目仅作生态定位说明。所有 Issue/PR 数字均为过去 24 小时更新事件数，非存量。

---

## 1. 生态全景

个人 AI 助手与自主智能体生态正处于**高活跃、强迭代、稳定性与安全加固并重**的阶段。头部项目如 Hermes Agent、Temporal 保持极高 PR 流量，但普遍存在“合并率低于新增率”的积压压力。今日共性问题是：**LLM Provider 兼容性修复、Windows 桌面链路稳定性、技能/记忆/上下文生命周期管理、以及安全策略精细化**成为多项目共同主战场。生态整体正在从“功能快速堆叠”转向“可信赖、可观测、可自托管”的成熟化阶段。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | Release | 健康度评估 |
|---|---:|---:|---|---|
| **OpenClaw** | 未提供 | 未提供 | — | 本次无数据，无法量化评估 |
| **Hermes Agent** | 419（新开/活跃 336，关闭 83） | 500（待合并 415，合并/关闭 85） | 无新版本 | 活跃度极高，但合并率约 17%，积压压力持续上升；有 P0 级 PR 待处理，需关注 |
| **OpenHands SDK** | 11（新开 10，关闭 1） | 14（待合并 11，合并/关闭 3） | 无新版本；v1.43.0 准备中 | 社区响应闭环良好，多个新 Issue 数小时内获 PR 跟进；高优安全 Bug 尚无修复，需排期 |
| **Pi** | 50（关闭 43，活跃 7） | 16（合并/关闭 11，待合并 5） | 无新版本 | 集中 Triage 清理，长期 PR 落地，TUI 稳定性修复密集；健康度良好 |
| **Temporal** | 4（含 2 个新 Bug） | 67（合并/关闭 28，待合并 39） | 无新版本 | 高频迭代与稳定性加固并行，但 2 个高严重度 Bug 暂无修复，需警惕 |
| **LiteLLM** | 未提供 | 未提供 | — | 本次无数据，无法量化评估 |

---

## 3. OpenClaw 在生态中的定位

由于今日快照未包含 OpenClaw 的 Issue/PR/Release 数据，**无法对其社区规模、活跃度、技术路线差异进行量化对比**。仅从生态位置看，OpenClaw 作为核心参照项目，大概率扮演“个人 AI 助手/自主智能体开源基线”的角色，与 Hermes Agent、Pi 处于同类赛道。后续若能补全其仓库动态，建议从以下角度对比：

- 与 Hermes Agent：功能广度、桌面端支持、Provider 兼容性；
- 与 Pi：终端体验、轻量化程度、交互范式；
- 与 OpenHands SDK：开发者嵌入能力、Agent Server / API 成熟度。

在数据缺失前，本报告不强行对其下结论。

---

## 4. 共同关注的技术方向

### 4.1 LLM Provider 兼容性与错误可观测性
- **Hermes Agent**：修复 Gemini emoji 400 错误、OpenRouter/Kimi 空消息问题；
- **OpenHands SDK**：Synthetic Provider 工具调用语法异常、Qwen3 `<think>` 块泄漏、Nebius 404 错误传播；
- **Pi**：Kimi thinking base64url 规范化、严格模式 provider 下消息插入顺序。

> 诉求：第三方/本地/合成模型的兼容性修补仍是日常高频工作，且失败时必须有明确错误而非泛化提示。

### 4.2 本地/自托管部署与 Windows 支持
- **Hermes Agent**：Windows 桌面应用更新后应用被删除、蓝屏等破坏性 Bug 集群，正在推进事务化重建；
- **Pi**：Windows 使用情况征集为今日最热 Issue（34 条评论）；
- **OpenHands SDK**：局域网纯 HTTP 下 Cookie 被拒导致 401，涉及安全策略与自托管可用性平衡。

### 4.3 技能/记忆/上下文生命周期管理
- **Hermes Agent**：技能索引过期（29.8h 未更新，限制 26h）；
- **OpenHands SDK**：Condensation 后技能与路径规则静默失效、全局 `load_memory` 偏好被忽略；
- **Pi**：auto-compaction 触发失败（17 👍）。

> 诉求：配置“静默失效”是用户信任杀手，上下文压缩后的行为一致性成为核心痛点。

### 4.4 安全加固向 MCP/子代理/配置文件扩展
- **Hermes Agent**：MCP 目录环境变量写入白名单限制；
- **OpenHands SDK**：加密 LLM 配置解密链路不完整、子代理 deny-list 功能；
- **Pi**：安全审计后补充 security.md manifest。

### 4.5 大规模与极端场景稳定性
- **Hermes Agent**：prompt_caching 负切片溢出（P0 内存 Bug）；
- **Pi**：14.5MB 大 diff 导致调用栈溢出崩溃；
- **Temporal**：SQL 连接池不可恢复关闭、批量操作无限挂起。

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构特征 |
|---|---|---|---|
| **OpenClaw** | 核心参照，定位个人 AI 助手基线 | 待补充 | 待补充 |
| **Hermes Agent** | 通用 AI 助手/桌面端 + 多 Provider + MCP | 终端用户、桌面应用开发者 | 大而全的 Agent 框架，功能密度高，社区量大 |
| **OpenHands SDK** | 可嵌入的 Agent Server / SDK，强调会话、记忆、工具、沙箱 | 软件开发者、需要自动化编码助手的团队 | 模块化 SDK，支持 AgentSandboxWorkspace 与 Kubernetes 后端，API 契约清晰 |
| **Pi** | 终端原生个人 AI 助手，TUI 优先 | 开发者、终端重度用户 | 轻量、交互体验优先，注重 TUI 渲染细节与命令流 |
| **Temporal** | 分布式工作流/持久执行编排 | 平台工程师、后端架构师 | Go 服务端，确定性工作流引擎，Nexus 作为 Agent

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，这是 2026-08-21 的 Hermes Agent 项目动态日报。

---

# Hermes Agent 项目动态日报 — 2026-08-21

## 1. 今日速览

项目在过去 24 小时保持**极高活跃度**：共发生 419 条 Issue 更新（新开/活跃 336 条，关闭 83 条）与 500 条 PR 更新（待合并 415 条，合并/关闭 85 条）。尽管无新版本发布，但合并/关闭率（Issue 约 19.8%，PR 约 17%）略低于新增速率，**积压压力仍在上升**。今日最突出的信号是 **Windows 桌面应用更新链路出现破坏性 Bug 集群**（更新后应用被删除、更新失败导致蓝屏等），同时出现 1 个 **P0 级 PR（#90972）** 修复 prompt_caching 的严重内存切片问题。社区讨论热度集中在技能索引失效（65 评论）、通用 ACP 客户端（24 评论 / 23 👍）与 Webhook 修复 meta-issue（21 评论）上。

## 2. 版本发布

今日无新版本发布（Releases: 0）。

## 3. 项目进展

今日共有 85 条 PR 被合并或关闭。在待合并的 415 条中，有一批高质量修复与新功能值得关注：

- **P0 紧急修复：prompt_caching 负切片溢出**（[PR #90972](https://github.com/NousResearch/hermes-agent/pull/90972)）— 修复 Anthropic provider 中 `non_sys[-0:]` 在 Python 中解析为整个切片、导致缓存标记错误的问题。这是今日最高优先级 PR，需尽快评审合并。
- **Windows 桌面包重建事务化**（[PR #91079](https://github.com/NousResearch/hermes-agent/pull/91079)）— 针对 #44225 与 #86443 的破坏性更新问题，使重建变为生成绑定事务，并防止 Node 运行时版本不匹配。另一个长期开放的相关 PR [#44234](https://github.com/NousResearch/hermes-agent/pull/44234)（6 月 11 日提交）也在等待中。
- **Gemini emoji 400 错误修复**（[PR #91101](https://github.com/NousResearch/hermes-agent/pull/91101)）— 根因是 httpx 以 `ensure_ascii=True` 序列化 JSON，改为原始 UTF-8 后修复。
- **ACP set_model 解析修复**（[PR #91100](https://github.com/NousResearch/hermes-agent/pull/91100)）— 解决「已配置但提示 No LLM provider configured」的问题，异常不再被吞掉。
- **空 final assistant 消息清理**（[PR #91094](https://github.com/NousResearch/hermes-agent/pull/91094)）— 修复 OpenRouter/Kimi 等 provider 在 replay 时产生空消息的问题。
- **桌面回复保留与频道刷新**（[PR #91141](https://github.com/NousResearch/hermes-agent/pull/91141)）— 防止 stale refresh 在 `sessions.changed` 时覆盖刚完成的回复。
- **Discord 纯文本模式**（[PR #91140](https://github.com/NousResearch/hermes-agent/pull/91140)）— 新增 `discord.voice_enabled` 开关，默认 `true` 保持现状，为不需要语音的部署提供选项。
- **MCP 目录环境变量写入限制**（[PR #91139](https://github.com/NousResearch/hermes-agent/pull/91139)）— 安全加固：只允许写入目录条目声明的环境变量，拦截运行时与审批控制变量。
- **Kanban 本地模型 worker 支持**（[PR #91142](https://github.com/NousResearch/hermes-agent/pull/91142)）— 为小参数本地模型提供可选的 `kanban.worker_tools` 白名单，降低 lifecycle schema 复杂度。

项目整体在 **稳定性修复（Windows 链路、provider 兼容、会话状态）** 与 **安全加固（MCP、文件操作）** 两个方向均有实质推进。

## 4. 社区热点

- **[#66616 [skills-index-watchdog] 技能索引过期](https://github.com/NousResearch/hermes-agent/issues/66616)**（65 评论）— 自动化探针报告索引已 29.8h 未更新（限制 26h）。评论

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-08-21

## 1. 今日速览

过去24小时项目活跃度极高：共产生 11 条 Issue 更新（10 条活跃/新增，1 条关闭）和 14 条 PR 更新（11 条待合并，3 条合并/关闭），无新版本发布。值得关注的是，今日 Bug 报告集中在安全（LLM 配置解密、会话 Cookie 拒绝）、记忆持久化和 LLM 工具调用正确性三个方向，且三个高优先级（priority:high）Bug 已全部进入 ready-for-dev 状态或已有对应 fix PR。项目整体处于密集修复与功能并进的阶段，社区反馈与开发响应形成良好闭环——多个今日新开 Issue 在数小时内即获得 PR 跟进。


## 2. 版本发布

过去 24 小时无新版本发布。但 [#4553](https://github.com/OpenHands/software-agent-sdk/pull/4553) 正在准备 Release **v1.43.0**，已通过集成测试、行为测试和安全扫描，预计即将发布。当前最新 release 为 v1.42.1（Agent Server）。


## 3. 项目进展

今日有 3 个 PR 被合并/关闭，体现了三个方向的实际推进：

- **[#4539](https://github.com/OpenHands/software-agent-sdk/pull/4539) fix(agent-server): backfill redacted LLM api_key on agent_settings launch** — 修复了通过原始 settings payload 启动会话时 API key 被掩码为星号导致鉴权失败的问题（解决 #4533）。这是一个影响所有通过 API 直接启动会话用户的实用修复。
- **[#4535](https://github.com/OpenHands/software-agent-sdk/pull/4535) fix(agent-server): propagate out-of-band run failures as ConversationErrorEvent** — 解决了 LLM 调用失败（如 Nebius + 不存在的模型返回 404）时 UI 只显示泛化错误的问题，现在会以 ConversationErrorEvent 形式正确传达失败原因（关联 OpenHands/OpenHands#16686）。
- **[#4560](https://github.com/OpenHands/software-agent-sdk/pull/4560) feat(tools): add structured task outcome preset（closed）** — 与 [#4479](https://github.com/OpenHands/software-agent-sdk/pull/4479) 同标题，疑似重复 PR 被关闭，结构化 `TaskOutcome` 预设仍由 #4479 推进中。

此外，**11 个 PR 正待合并**，其中值得关注的新增项：

- [#4552](https://github.com/OpenHands/software-agent-sdk/pull/4552) 修复 condensation 后触发技能失效（对应 #4544）
- [#4557](https://github.com/OpenHands/software-agent-sdk/pull/4557) 实现子代理 deny-list 功能（对应 #4556）
- [#4534](https://github.com/OpenHands/software-agent-sdk/pull/4534) 去除 LLM 生成标题中的思考块泄漏（对应 #4541）


## 4. 社区热点

今日讨论最活跃的议题集中在 **LLM 工具调用的正确性**与**记忆/上下文管理**两个主题上：

1. **[#4540: 合成 Provider 下工具调用返回怪异语法](https://github.com/OpenHands/software-agent-sdk/issues/4540)**（6 条评论）
   用户报告在 Docker 安装的 Agent Canvas 1.14.0 上，Synthetic provider 的模型在工具调用时偶尔返回原始/奇怪的语法，影响正常工具执行。这是今日评论最多的 Issue，反映出第三方/合成 LLM Provider 的兼容性问题是用户实际使用中的高频痛点。

2. **[#4544: Condensation 后触发技能与路径规则静默失效](https://github.com/OpenHands/software-agent-sdk/issues/4544)**（4 条评论）
   关键词触发的技能和路径触发的规则在对话压缩（condensation）后被"遗忘"，导致后续对话中这些自动化行为静默消失。该问题已有 3 名用户确认复现，表明这是一个影响面较广的回归类问题。目前已由 [#4552](https://github.com/OpenHands/software-agent-sdk/pull/4552) 提交修复。

3. **[#4542: 全局 load_memory 偏好被静默忽略](https://github.com/OpenHands/software-agent-sdk/issues/4542)**（4 条评论）
   用户配置的全局 `agent_context.load_memory` 偏好仅在通过 agent profile 启动对话时生效，直接指定 agent 时会静默丢失。后台社区对"配置设置失效"类问题尤为敏感，因为此类问题难以排查。


## 5. Bug 与稳定性

今日共报告 8 个 Bug，按严重程度排列如下：

### 高优先级（High）

- **[#4542](https://github.com/OpenHands/software-agent-sdk/issues/4542) 全局 load_memory 偏好被忽略** — `agent_context.load_memory` 仅在通过 `agent_profile_id` 启动会话时生效，直接使用 `agent` 或 `agent_settings` 启动时设置静默丢失，导致持久记忆不加载。**暂无对应修复 PR**。标记 `release-note-required`。

- **[#4558](https://github.com/OpenHands/software-agent-sdk/issues/4558) 加密 LLM 配置仅在会话路径解密** — `LLMProfileStore.load()` 的 `cipher` 参数只有会话启动路径传入，FallbackStrategy 和子代理加载配置时以 `cipher=None` 调用，在加密配置的服务器上会导致回退策略/子代理无法使用加密的 LLM 配置。标记 `ready-for-dev`，有安全影响。**暂无对应修复 PR**。

### 中优先级（Medium）

- **[#4555](https://github.com/OpenHands/software-agent-sdk/pull/4555) Agent Server 事件端点无限挂起** — LocalConversation 清理阻塞时，既有会话的事件端点会无限期挂起，UI 表现为"转圈"。标记 `duplicate-candidate`，**暂无对应修复 PR**。

- **[#4562](https://github.com/OpenHands/software-agent-sdk/issues/4562) 局域网 HTTP 下 workspace 文件返回 401** — workspace-session 端点发出 `SameSite=None` 但不带 `Secure` 的 Cookie，导致通过非 loopback 的纯 HTTP 访问时 Cookie 被浏览器拒绝，返回 401。标记 `release-note-required` 和 `ready-for-dev`。**已有对应 PR [#4563](https://github.com/OpenHands/software-agent-sdk/pull/4563)**。

- **[#4540](https://github.com/OpenHands/software-agent-sdk/issues/4540) Synthetic Provider 工具调用返回错误语法** — 模型返回工具调用为原始字符串格式，导致工具无法正确解析执行。**暂无对应修复 PR**。

- **[#4541](https://github.com/OpenHands/software-agent-sdk/issues/4541) Qwen3-32B 的 `<think>` 行为异常** — 思考块泄漏到会话自动生成标题中，可能导致标题污染和上下文混乱。**已有对应 PR [#4534](https://github.com/OpenHands/software-agent-sdk/pull/4534)**。

- **[#4554](https://github.com/OpenHands/software-agent-sdk/issues/4554) CriticMixin 始终以 git_patch=None 调用 evaluate()** — 导致 critic 评估的是对话记录而非代码 diff，影响评估质量。**暂无对应修复 PR**。

- **[#4544](https://github.com/OpenHands/software-agent-sdk/issues/4544) Condensation 后触发技能/路径规则静默失效** — 已在社区热点中详述。**已有对应 PR [#4552](https://github.com/OpenHands/software-agent-sdk/pull/4552)**。

> **健康度评估**：今日高优 Bug 集中在安全与记忆两个核心领域，且 #4558 和 #4542 都暂无修复 PR，建议维护者优先分配资源。中等优先级 Bug 中约 1/3 已有对应 fix PR，响应速度良好。


## 6. 功能请求与路线图信号

今日有 4 个功能请求/增强，显示出明确的路线图方向：

1. **[#4556](https://github.com/OpenHands/software-agent-sdk/issues/4556) 子代理 deny-list（disabled_agents）** — Skills 已有 `AgentContext.disabled_skills`，用户希望为子代理提供类似的每会话禁用列表，在生成时强制校验。**已有对应 PR [#4557](https://github.com/OpenHands/software-agent-sdk/pull/4557)**，较大概率进入下一版本。

2. **[#4561](https://github.com/OpenHands/software-agent-sdk/issues/4561) 允许通过 ConversationConfig 自定义标题生成提示词** — 目前 `generate_title_with_llm()` 的提示词硬编码，用户希望可配置以适配不同场景（如隐私过滤、命名风格）。标记 `release-note-required`，属于易实现的小增强，可能被纳入近期版本。

3. **[#4479（PR）](https://github.com/OpenHands/software-agent-sdk/pull/4479) 结构化任务结果预设** — 在 `openhands.tools.preset` 下新增 `TaskOutcome` 等结构化模型，使 `FinishTool` 返回结构化结果。虽非今日新开，但仍在持续活跃中，代表了工具调用从自由文本向结构化演进的趋势。

4. **[#4130（已关闭）](https://github.com/OpenHands/software-agent-sdk/issues/4130) search_tool 功能请求关闭**（标记为 duplicate）— 该请求探讨了当工具数量增长（尤其通过 MCP）时，如何避免全部放入系统提示词导致性能下降。关闭为 duplicate 暗示已有其他 Issue 或内部方案在跟踪此需求。这是路线图上的重要信号：**工具检索/动态工具加载**可能已在规划中。


## 7. 用户反馈摘要

从今日 Issue 评论和描述中提炼的真实用户反馈：

- **配置"静默失效"是信任杀手**：多位用户（#4542、#4544）遇到的问题都是"我配置了但没生效，而且没有任何提示"，这类问题排查成本极高，用户反馈中表现出明显的沮丧感。SDK 应在配置被忽略时给出警告日志或显式错误。

- **第三方/合成 LLM Provider 兼容性焦虑**：#4540 和 #4541 分别报告了 Synthetic provider 和 Qwen3 的异常行为。结合 #4535 的修复（LLM 调用失败的错误传播），社区对 LLM Provider 生态的广度支持有较高期待，且希望失败时有明确的错误信息而非泛化提示。

- **安全与部署场景的摩擦**：#4562 反映了自托管用户在纯 HTTP 局域网环境中的实际困难——Cookie 安全策略过于激进导致功能不可用，用户需要的是在安全与可用性之间更细致的平衡策略。

- **API 直接调用者的工具链缺口**：#4539 的修复（API key 掩码回填）解决了一个典型问题——前端发送掩码后的 payload 给后端，后端拿掩码值去鉴权显然会失败。这类"前后端契约"问题在 SDK 使用场景中影响面较大，社区希望能够系统性规避。


## 8. 待处理积压

以下为值得维护者关注的长周期未响应/未解决项：

1. **[PR #4287: Pareto prompt meta-profile routing](https://github.com/OpenHands/software-agent-sdk/pull/4287)**（已开放 24 天，最后更新 2026-08-20）
   引入来自 OpenHands/research#76 的 Pareto 路由器提示词，作为元配置档路由策略。作者明确标注 draft 状态等待路由策略就绪，但持续有更新，建议维护者给出明确评审意见。

2. **[PR #4479: 结构化任务结果预设](https://github.com/OpenHands/software-agent-sdk/pull/4479)**（已开放 9 天）
   实验性结构化 `TaskOutcome` 模型。虽非紧急，但属于工具系统演进方向，建议维护者早期介入设计评审，避免后续返工。

3. **[PR #4516: AgentSandboxWorkspace（Kubernetes 后端）](https://github.com/OpenHands/software-agent-sdk/pull/4516)**（已开放 4 天，最后更新 2026-08-20）
   增加 Kubernetes 作为沙箱运行后端，已在 kind 和 GKE 上验证。对于已有 k8s 集群的团队是有价值的部署选项，建议维护者关注其与现有 workspace 抽象的一致性设计。

4. **[Issue #4542: 全局 load_memory 偏好被忽略](https://github.com/OpenHands/software-agent-sdk/issues/4542)**（high，暂无修复）
   虽为新 Issue，但因其高优先级且暂无对应 PR，在此特别提示——这类"静默吞配置"的问题对用户信任伤害较大，建议优先排期。


*本日报数据来源：OpenHands/software-agent-sdk GitHub 仓库，统计周期为 2026-08-20 至 2026-08-21（过去 24 小时）。*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-21

> 数据窗口：过去 24 小时 | 数据来源：earendil-works/pi GitHub

---

## 1. 今日速览

过去 24 小时项目活跃度较高：**50 条 Issue 更新（43 条关闭 / 7 条活跃）**，**16 条 PR 更新（11 条合并或关闭 / 5 条待合并）**，无新版本发布。Issue 关闭率高达 86%，其中大部分为长期积压的重复请求（尤其是 `/exit` 别名系列）和 `no-action`/`untriaged` 标记的三方提交，说明维护者今日进行了一轮集中的 Triage 与清理。项目核心健康度良好：多个长期挂起的 PR 今日被合并（含 5 月 15 日提交的 `/exit` 别名 PR），TUI 稳定性修复密集落地。社区关注焦点集中在 **Windows 支持**（34 条评论）和 **auto-compaction 触发失败**（17 👍）两个方向。

---

## 2. 版本发布

今日无新版本 Release。

---

## 3. 项目进展（今日合并/关闭的 PR）

今日合并/关闭 11 个 PR，覆盖 TUI 渲染、AI 提供商兼容性、退出命令体验三大方向，整体推进明显：

### 🎨 TUI / 终端体验
| PR | 内容 | 意义 |
|---|---|---|
| [#8407](https://github.com/earendil-works/pi/pull/8407) | 修复鼠标选中软换行文本复制时被硬拼接为换行的问题 | 提升全屏模式下复制代码/URL 的准确性 |
| [#8363](https://github.com/earendil-works/pi/pull/8363) | 修复表格链接颜色泄漏到 padding/边框（fixes #8335） | TUI 渲染细节修复，附测试 |
| [#5268](https://github.com/earendil-works/pi/pull/5268) | 默认渲染硬件光标，窗口失焦后提示符光标空心化（fixes #3896） | 从 6 月 1 日挂起至今的长期 PR，今日合并 |
| [#8395](https://github.com/earendil-works/pi/pull/8395) | 避免 `lines.push(...contentLines)` 在 ~14.5MB 大 diff 时触发 V8 调用栈溢出崩溃（fixes #8036） | 修复渲染超大 diff 时的 TUI 崩溃 |

### 🔌 AI 提供商兼容性
| PR | 内容 | 意义 |
|---|---|---|
| [#8405](https://github.com/earendil-works/pi/pull/8405) | 将 `kimi-coding` thinking 签名字段规范化为 base64url | 修复 Kimi 多轮 reasoning 对话 400 错误 |
| [#8416](https://github.com/earendil-works/pi/pull/8416) | `triggerTurn: false` 的自定义消息延迟到工具批次结束后发送 | 避免消息插入 `toolCall`/`toolResult` 之间被严格模式 provider 拒绝 |
| [#8384](https://github.com/earendil-works/pi/pull/8384) | 安全审计后补充 security.md manifest | 供应链安全维护 |

### ⚙️ 命令与设置
| PR | 内容 | 意义 |
|---|---|---|
| [#4537](https://github.com/earendil-works/pi/pull/4537) + [#5160](https://github.com/earendil-works/pi/pull/5160) | 为 `/quit` 增加 `/exit`（及 `/bye`）别名 | 终结了自 5 月 15 日以来 6 个重复 issue 的诉求 |
| [#8399](https://github.com/earendil-works/pi/pull/8399) | `/model` `/thinking` 选择器显示并支持搜索 "default" | 配合 Ctrl+S 持久化设置，减少歧义 |

**总体判断**：项目今日完成了约 11 项合并，其中 TUI 修复占比最高（4/11），且覆盖了从复制、光标、颜色到崩溃的多个纬度；`/exit` 别名从 5 月拖到 8 月终于落地，是用户呼声最高的诉求之一。项目整体呈现"稳定迭代 + 社区驱动"的节奏。

---

## 4. 社区热点

### 🔥 最热 Issue：#7547 — Windows 使用情况大规模征集
- 链接：https://github.com/earendil-works/pi/issues/7547
- 状态：OPEN | 评论 **34** | 更新于 2026-08

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-21

## 今日速览

Temporal 核心库今日整体活跃度**较高**：过去 24 小时内 PR 更新达 67 条，其中 28 条已合并/关闭、39 条处于待合并状态，代码评审与合入节奏密集；Issue 侧有 4 条更新，包含 2 个新报告的潜在严重 Bug（SQL 连接池不可恢复关闭、批量操作无限挂起），需关注后续响应。无新版本发布。当前开发重点集中在 **reliability-2026 可靠性专题、Nexus 功能扩展及 Worker callbacks 特性分支**上，尤其在复制任务优先级、调度器迁移、Nexus 拦截器重构等方向有实质性推进。项目整体处于“高频迭代、稳定性加固并行”的健康状态。

---

## 版本发布

今日无新版本发布。

---

## 项目进展

过去 24 小时共有 28 个 PR 被合并/关闭，其中较有代表性的合入包括：

- **Nexus：支持 Query-backed Nexus 操作（#11274）**  
  PR 合入意味着 Nexus 操作现在可以由 Workflow Query 提供支持，进一步将 Temporal 原语（查询）暴露为 Nexus 操作，是 Nexus 功能拼图的重要一块。  
  https://github.com/temporalio/temporal/pull/11274

- **复制应用生命周期事件改进（#11645）**  
  改进复制应用到生命周期事件：捕获 post-transaction 可变状态、将成功的 verify history 修复报告为 `outcome=backfilled`、在 verify applied 事件中包含修复范围与 `new_run_id`，并新增 zombie 相关回归测试。该 PR 对多集群复制、故障恢复场景的可观测性和正确性有直接提升。  
  https://github.com/temporalio/temporal/pull/11645

- **自适应测试超时：通过 Await 扩展测试上下文（#10417，reliability-2026）**  
  合入后，长耗时 Await 调用可以请求额外的测试作用域上下文时间，避免 CI 超时误报，有助于减少因测试基础设施不稳定导致的失败噪音。  
  https://github.com/temporalio/temporal/pull/10417

此外，还有 25 个其余 PR 已合并/关闭（未完整展示）。整体来看，项目在**复制可靠性、Nexus 能力完善、测试基础设施**三条线均有实质推进。

---

## 社区热点

- **Worker Deployments 版本 GC 缺陷（#10737）**  
  这是当前社区讨论最持久、反馈最具体的问题之一：在频繁部署的控制器场景下，旧版本不被回收，最终顶到 `matching.maxVersionsInDeployment` 上限，导致 rollout 被卡死。该 Issue 创建于 6 月 16 日，截至今日已有 5 条评论，且在 8 月 20 日仍有更新，说明用户受影响时间长、诉求强烈。  
  https://github.com/temporalio/temporal/issues/10737

- **Cassandra 压缩策略迁移请求（#11314）**  
  用户建议将 schema.cql 中默认的 LeveledCompactionStrategy（LCS）替换为 Cassandra 5.x 的 UnifiedCompactionStrategy（UCS），认为 LCS 并非适合所有工作负载的通用默认值。该请求获得 3 条评论，反映出 Cassandra 运维侧用户对存储引擎最佳实践升级的关注。  
  https://github.com/temporalio/temporal/issues/11314

---

## Bug 与稳定性

按严重程度排序：

| 严重度 | Issue/PR | 描述 | 状态 |
|---|---|---|---|
| 🔴 高 | #11691 | **SQL session 刷新可不可逆地关闭连接池（“sql: database is closed”）**，随后 membership heartbeat 静默失败，集群呈现“僵尸”状态但仍报告 SERVING，无法 dispatch 任何任务。这对 SQL 存储用户是潜在的生产事故级问题。 | 新报告（8-20），暂无评论，无 fix PR |
| 🔴 高 | #10737 | **Worker Deployment 版本 GC 无法在达到 `maxVersionsInDeployment` 时回收满足条件的已排空版本**，使得 rollout 被卡住。影响高频发布用户，已持续 2 个月。 | OPEN，5 条评论，暂无 fix PR |
| 🟠 中 | #11683 | **批量操作（Batch Operations）可能无限期卡在 RUNNING**，底层 Visibility 持续超时并无限重试，无进展也无明确失败。 | 新报告（8-20），暂无评论，无 fix PR |

链接：  
https://github.com/temporalio/temporal/issues/11691  
https://github.com/temporalio/temporal/issues/10737  
https://github.com/temporalio/temporal/issues/11683

---

## 功能请求与路线图信号

- **Cassandra UCS 迁移（#11314）**：用户请求将默认压缩策略从 LCS 改为 Cassandra 5.x 的 UCS，预期性能更好、IO 更平滑。该请求与 Cassandra 5.x 普及时间线相关，具备纳入后续版本的合理性。  
  https://github.com/temporalio/temporal/issues/11314

- **Worker 可观测性增强（PR #11348）**：为 workflow/activity 任务完成类指标添加 `worker_deployment_name` 和 `worker_build_id` 标签。与 Worker Versioning 功能配套，利于按部署版本监控，目前仍 OPEN。  
  https://github.com/temporalio/temporal/pull/11348

- **Nexus 路线图持续落地**：今日有 Query-backed Nexus 操作合入（#11274），另有 Nexus 前端拦截器重构（#11464）和 CHASM Nexus 取消语义修正（#11312）仍在推进，表明 Nexus 仍是近期功能开发核心方向。  
  https://github.com/temporalio/temporal/pull/11464  
  https://github.com/temporalio/temporal/pull/11312

- **复制可靠性专题（reliability-2026）**：多个相关 PR 处于活跃状态（如 #11692 强制复制任务低优先级、#11462 Scheduler 迁移修复、#11556 ALLOW_ALL 调度完成状态隔离），说明这一内部可靠性专项在持续推进。

---

## 用户反馈摘要

- **高频发布用户的痛点（#10737）**：用户使用控制器频繁部署 Worker，每次部署都注册新的 Worker Deployment Version，但旧版本无法被自动回收，最终顶到上限阻断发布。用户预期“已排空版本应被自动 reclaim”，实际行为与其部署模型不匹配，说明 **Worker Versioning 的 GC 策略需要从“上限保护”向“自动清理”演进**。  
  https://github.com/temporalio/temporal/issues/10737

- **Cassandra 运维视角（#11314）**：反馈者指出当前 LCS 对所有表“一刀切”并非最优，UCS 在多数场景下表现更好。该诉求带有明显的“默认配置应更贴近最佳实践”的期望，说明用户在存储层有主动调优意识，也暗示官方默认 schema 需要跟随上游 Cassandra 演进。  
  https://github.com/temporalio/temporal/issues/11314

- **SQL 存储用户的信任危机（#11691）**：连接池一旦关闭便不可恢复、集群却仍自报 SERVING，这种“静默僵尸”行为会让用户对故障切换和自动恢复机制产生不信任，属于对系统自愈能力的强烈不满。

---

## 待处理积压

- **#10737 Worker Deployment 版本 GC 缺陷** — 自 2026-06-16 创建至今已超 2 个月，5 条评论，无 fix PR，持续影响高频部署用户且阻塞 rollout。建议维护者优先评估 GC 回收逻辑或调整 `maxVersionsInDeployment` 的语义。  
  https://github.com/temporalio/temporal/issues/10737

- **#11314 Cassandra 压缩策略迁移** — 自 2026-07-27 创建，3 条评论，无相关 PR。建议在 Cassandra 5.x 支持矩阵稳定后评估是否纳入 schema 默认值更新。  
  https://github.com/temporalio/temporal/issues/11314

- **PR #11464 Nexus 前端拦截器重构** — 自 2026-08-11 开启，已近 10 天仍未合入，属于 Nexus 路线图依赖项，需关注是否被阻塞。  
  https://github.com/temporalio/t

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*