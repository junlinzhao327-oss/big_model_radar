# OpenClaw 生态日报 2026-08-09

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-08 22:51 UTC

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

# AI Agent 开源生态横向对比分析报告

**报告日期：2026-08-09**


## 1. 生态全景

个人 AI 助手 / 自主智能体开源生态已形成清晰的**分层格局**：终端交互层（Pi）、嵌入 SDK 层（OpenHands SDK）、LLM 网关层（LiteLLM）与工作流编排层（Temporal）各司其职，且层间耦合正在加深。跨项目的共同信号是：**LLM 配置的健壮性与连接可靠性已取代基础功能开发，成为社区最集中的痛点**（Pi 的 provider 连接问题、OpenHands 的配置预验证、LiteLLM 的日志/回归报告）。与此同时，**插件生态标准化**（OpenHands 的 agent-plugins.org 支持）与**可观测性/多租户能力**（LiteLLM 的 OTEL 出口系列、OpenHands 的密钥泄露修复）正成为下一阶段竞争焦点。整体而言，生态正从"能用"迈向"好用且可信"，迭代节奏快但质量治理压力同步上升。


## 2. 各项目活跃度对比

| 项目 | Issue 动态 | PR 动态 | Release | 健康度评估 |
|------|-----------|---------|---------|-----------|
| **OpenClaw** | 数据缺失 | 数据缺失 | 数据缺失 | ⚠️ 无法评估（本日无数据） |
| **Hermes Agent** | 数据缺失 | 数据缺失 | 数据缺失 | ⚠️ 无法评估（本日无数据） |
| **OpenHands SDK** | 11 条更新（全部活跃，0 关闭） | 17 条 PR 更新（0 合并/关闭，17 待合并） | 无 | 🟡 活跃开发但 **PR 积压严重**，合并流程是瓶颈 |
| **Pi** | 34 条更新（32 关闭 / 2 活跃） | 12 条 PR 更新（7 合并/关闭 / 5 待合并） | 无 | 🟢 **高频迭代 + 快速响应**，社区驱动明显 |
| **LiteLLM** | 22 条更新（19 活跃 / 3 关闭） | 153 条 PR 更新（47 合并 / 106 待合并） | **v1.94.2**（cosign 镜像签名） | 🟢 迭代速度最快，但**回归风险与长期积压并存** |
| **Temporal** | 0 新增/关闭 | 6 条 PR 更新（2 关闭 / 4 待合并） | 无（1.32.0 发布分支已准备） | 🟢 稳定推进，企业级节奏，社区互动低 |


## 3. OpenClaw 在生态中的定位

> ⚠️ 本日未提供 OpenClaw 的项目动态数据，以下分析基于其在报告框架中的"核心参照"角色，结合生态整体格局进行逻辑推断，不涉及其具体指标。

**生态角色独特且承上启下**：如果说 Pi 是"终端体验型"、OpenHands SDK 是"能力嵌入型"、LiteLLM 是"基础设施型"，那么 OpenClaw 的定位更接近 **"全栈个人 AI 助手参考实现"**——覆盖从模型接入、工具调用到交互界面的完整闭环。这种"横向整合"路线与其余项目的"纵向深耕"形成互补，使其天然适合作为生态的**集成基准**：LiteLLM 为它提供网关能力，OpenHands SDK 可为它补充可嵌入的 agent 运行时，Pi 为它提供交互范式参照。

**优势**：全栈整合带来的开箱即用体验，能够直接对标商用个人 AI 助手，是生态中少数可以直接面向终端用户的完整方案。

**技术路线差异**：不追求单一环节的最优，而是强调各层之间的**默认配置可用性**与**端到端一致性**——这与 Pi 的终端优先、LiteLLM 的网关纵深形成鲜明对比。

**社区规模**：无法基于本日数据量化，但其"核心参照"地位本身说明受到了生态内外的广泛关注。


## 4. 共同关注的技术方向

### 4.1 LLM 连接可靠性与配置健壮性（涉及：Pi、OpenHands、LiteLLM）
- **Pi**：`#4945` openai-codex 连接可靠性问题（76 评论 / 31👍，积压 3 个月），`#7820` 约 30% 长流式请求因 WebSocket 断开且无重试。
- **OpenHands**：LLM 配置预验证 endpoint（#4422）、路由模型运行时元数据（#4423）、`max_input_tokens` 不生效修复（#4435）。
- **LiteLLM**：`#10788` 日志级别无法关闭（从 2025 年 5 月持续，12+ 评论），responses API 空输出回归（#36275）。

**共识**：模型接入的**可诊断性**与**失败恢复**已取代功能堆叠，成为用户体验的第一决定因素。

### 4.2 插件生态标准化（涉及：OpenHands）
- `#4405` 提议支持 agent-plugins.org 开放打包标准（v1.0.0 WD，TSC 含 Amazon/Cursor/Microsoft 核心维护者）；`#4420` 正向多插件格式做前置重构。
- 这是本日最明确的**战略性**信号：插件生态正从"各自为政"走向"跨平台兼容"。

### 4.3 可观测性与安全加固（涉及：OpenHands、LiteLLM、Pi）
- **OpenHands**：修复生产 Datadog 日志中 API 密钥明文泄露（#4424，高优）。
- **LiteLLM**：OTEL 多租户出口系列（#35513–#35517）、cosign 镜像签名（v1.94.2）。
- **Pi**：为 telemetry 添加 StreamAssistant 支持（#7713）、恶意 npm 包报告（#7825）。

### 4.4 长上下文与上下文压缩管理（涉及：Pi、OpenHands）
- **Pi**：`#6879` auto-compaction 在长 agent turn 中不触发，直到 provider 溢出（373k token）；衍生 Issue #7821。
- **OpenHands**：condenser `max_tokens` 继承修复（#4435）。

### 4.5 企业级/多租户能力下沉（涉及：LiteLLM、Pi、OpenHands）
- **LiteLLM**：按团队/组织解析 OTEL 出口、预算重置 leader election（#36287）、PTU 计费闭环。
- **Pi**：单 Provider 多账号登录请求（#7814）、并行进程会话隔离（#7812）。
- **OpenHands**：遥测区分自动化会话（#4425）。


## 5. 差异化定位分析

| 项目 | 核心定位 | 目标用户 | 关键架构特征 | 突出优势 | 主要短板 |
|------|---------|---------|-------------|---------|---------|
| **OpenHands SDK** | 可嵌入 Agent 运行时 SDK | 应用开发者 | 库式嵌入，LLM 调用上下文集中，配置/插件抽象层 | 灵活集成、配置体系完善 | PR 积压拖慢迭代；插件标准未定 |
| **Pi** | 终端优先的个人 AI Agent | 终端用户/技术爱好者 | 全屏 TUI + CLI，多 provider 直连 | 交互体验打磨深、社区响应快 | provider 长流可靠性存疑；上下文管理被动 |
| **LiteLLM** | LLM 网关/代理层 | 企业平台团队 | 代理式统一入口，路由/计费/可观测 | 企业级功能密度最高（多租户、成本归因） | 回归风险与长期 Issue 积压；上手复杂度高 |
| **Temporal** | 持久化工作流引擎 | 后端/基础设施开发者 | 确定性执行 + 回调/事件驱动 | 可靠性治理体系化（reliability-2026） | 社区互动低；功能演进由内部主导 |

**一句话总结**：OpenHands 做"嵌入"，Pi 做"体验"，LiteLLM 做"管道"，Temporal 做"底座"——四者互补大于竞争，OpenClaw 则可能扮演"集大成者"的整合角色。


## 6. 社区热度与成熟度

### 🟢 快速迭代期（功能高频上线，社区反馈驱动）
- **LiteLLM**：单日 47 个 PR 合并、153 条 PR 更新、发布 v1.94.2，功能管线密集。处于"功能军备竞赛"阶段，但需要防范回归质量。
- **Pi**：单日 32 个 Issue 关闭，PR 合并率高（7/12），修复响应快。典型的社区驱动、小步快跑节奏。

### 🟡 架构重构期（活跃但合入受阻）
- **OpenHands SDK**：核心维护者密集提交 8 个关联 PR，但 17 个 PR 全部待合并（最长等待 20 天）。正处于架构重构的"

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报

**日期：2026-08-09**
**数据来源：** github.com/OpenHands/software-agent-sdk


## 1. 今日速览

过去 24 小时项目保持**高活跃度**：共有 11 条 Issue 更新与 17 条 PR 更新，其中 17 个 PR 均处于待合并状态，暂无新合并或关闭的 PR。Issue 侧全部为活跃状态（11 个待处理，0 个关闭）。值得关注的是，核心维护者 @neubig 密集提交了 8 个关联 Issue-PR 对（涵盖 LLM 路由元数据、配置迁移修复、CI 调整等），显示 SDK 正在进行一轮以 **LLM 配置健壮性** 和 **架构重构** 为核心的集中迭代。此外，Plugin 相关讨论在沉寂多时后重新升温（#1440 + #4405），是值得关注的路线图信号。整体评估：**项目处于活跃开发期，PR 积压待审是当前主要瓶颈。**


## 2. 版本发布

**过去 24 小时内无新版本发布。**


## 3. 项目进展

过去 24 小时 **没有 PR 被合并或关闭**，17 个 PR 全部处于待合并状态。尽管没有代码合入主分支，但这些待合并 PR 清晰展示了项目当前推进的技术方向：

**架构重构**
- **Centralize LLM call context** ([#4159](https://github.com/OpenHands/software-agent-sdk/pull/4159))：将 LLM 调用上下文集中在 SDK 层，属于基础架构级重构，影响面较大，已持续等待近三周，建议维护者重点关注。

**LLM 配置与可观测性**
- **Pre-flight LLM validation endpoint** ([#4422](https://github.com/OpenHands/software-agent-sdk/pull/4422))：新增 `POST /api/profiles/{name}/validate` 接口，在保存配置前用最小 token 请求验证 LLM 配置正确性，直击 PostHog 中数千条错误配置问题的痛点。
- **Provider-specific runtime metadata for routed models** ([#4423](https://github.com/OpenHands/software-agent-sdk/pull/4423) / [#4421](https://github.com/OpenHands/software-agent-sdk/issues/4421))：解决 OpenRouter 等路由提供商的实际模型限制与静态目录不一致的问题。
- **Inherit condenser max_tokens** ([#4435](https://github.com/OpenHands/software-agent-sdk/pull/4435))：修复 headless CLI 模式下 `max_input_tokens` 不生效的问题，社区贡献者 @vnktadithya 已定位根因并提交修复。

**Plugin 生态**
- **Extract PluginFormat strategy** ([#4420](https://github.com/OpenHands/software-agent-sdk/pull/4420))：为支持多插件格式（如 agent-plugins.org 标准）做的前置重构，表明项目正在为插件生态的扩展铺路。

**稳定性与安全**
- **Fix MCP fetch server runtime dependencies** ([#4303](https://github.com/OpenHands/software-agent-sdk/pull/4303))：修复上游 `mcp` 2.0.0 中 `McpError` 重命名导致的兼容性问题。
- **Redact URL query parameters containing secrets** ([#4424](https://github.com/OpenHands/software-agent-sdk/pull/4424))：解决 Datadog 日志中 32+ 条 API 密钥明文泄露问题，属安全修复，建议优先合并。
- **Repair v1 skills migration** ([#4320](https://github.com/OpenHands/software-agent-sdk/pull/4320))：修复升级后遗留的 `default` agent profile 不可编辑问题。\


## 4. 社区热点

**🔥 最热 Issue：[#1440 Plugin 1.0 Definition](https://github.com/OpenHands/software-agent-sdk/issues/1440)**
- 作者：@jpelletier1 | 评论：**26 条** | 创建于 2025-12-18，更新于 2026-08-08
- 该 Issue 是项目中最老的开放 Issue，讨论 Plugin 1.0 的定义范围，明确将 MCP config 和 runtime config 的纳入列为 Out of Scope。尽管已经持续 8 个月，仍在持续获得更新，说明是社区长期关注的核心议题。

**📈 新热点：[#4405 Spec: Support the Agent Plugins portable package format](https://github.com/OpenHands/software-agent-sdk/issues/4405)**
- 作者：@VascoSch92 | 评论：1 条 | 创建于 2026-08-06
- 提议支持 [agent-plugins.org](https://agent-plugins.org) 的开放、厂商中立插件打包标准（v1.0.0 Working Draft），其 TSC 包含 Amazon、Cursor、Microsoft 的核心维护者。结合 PR #4420 的 PluginFormat 策略重构，**OpenHands 正在为插件的跨平台兼容做准备**。

**💬 社区反馈最具体：[#3746 max_input_tokens 配置不生效](https://github.com/OpenHands/software-agent-sdk/issues/3746)**
- 作者：@xiaolei373 | 评论：4 条
- 用户提供了脱敏后的完整 JSON 配置，反馈 `agent_settings.json` 中的 `llm.max_input_tokens` 在 headless CLI 模式下不生效。该问题今日已被 PR #4435 锁定并修复，展现了社区驱动的良性循环。

两个热点背后共同的诉求是：**用户希望 OpenHands 的配置体系更透明、更可靠，同时生态能拥抱行业标准以减少锁定**。


## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue | 描述 | Fix PR |
|---------|-------|------|--------|
| 🔴 高（安全问题） | — | 运行时日志中 URL 查询参数里的 API 密钥明文泄露（生产 Datadog 中发现 32+ 条记录） | [#4424](https://github.com/OpenHands/software-agent-sdk/pull/4424) 待合并 |
| 🟠 中 | [#3746](https://github.com/OpenHands/software-agent-sdk/issues/3746) | `max_input_tokens` 在 headless CLI 模式下不生效 | [#4435](https://github.com/OpenHands/software-agent-sdk/pull/4435) 待合并 |
| 🟠 中 | [#4431](https://github.com/OpenHands/software-agent-sdk/issues/4431) | 升级后遗留的 `default` agent profile 不可编辑（v1 skills 迁移 bug） | [#4320](https://github.com/OpenHands/software-agent-sdk/pull/4320) 待合并 |
| 🟡 低 | [#4432](https://github.com/OpenHands/software-agent-sdk/issues/4432) | MCP fetch server 运行时依赖未固定，上游 `mcp` 2.0.0 致 API 变更 | [#4303](https://github.com/OpenHands/software-agent-sdk/pull/4303) 待合并 |

所有今日上报的 Bug 均已有对应的修复 PR，且处于待合并状态，说明核心维护者响应及时、修复链路完整。


## 6. 功能请求与路线图信号

**近期可能被纳入的功能（已有 PR 支撑）：**

1. **LLM 配置预验证**（[#4429](https://github.com/OpenHands/software-agent-sdk/issues/4429) → PR [#4422](https://github.com/OpenHands/software-agent-sdk/pull/4422)）：保存 LLM profile 前先做最小请求验证，直接改善用户体验，减少配置错误。另由 companion PR OpenHands/OpenHands#16417 联动。

2. **路由模型运行时元数据解析**（[#4428](https://github.com/OpenHands/software-agent-sdk/issues/4428) → PR [#4423](https://github.com/OpenHands/software-agent-sdk/pull/4423)）：解决 OpenRouter 等路由提供商的模型限制准确性问题。

3. **Agent Plugins 标准支持**（[#4405](https://github.com/OpenHands/software-agent-sdk/issues/4405)）：仍处于 Needs Design 阶段，是战略性路线图信号，与 PR [#4420](https://github.com/OpenHands/software-agent-sdk/pull/4420) 的 PluginFormat 策略提取相呼应。

4. **遥测区分自动化会话**（[#4427](https://github.com/OpenHands/software-agent-sdk/issues/4427) → PR [#4425](https://github.com/OpenHands/software-agent-sdk/pull/4425)）：为 Local Agent Canvas 部署增加 `is_automation` 标记，提升遥测数据可分析性。

5. **可选择的 Laminar 观测工具**（PR [#4434](https://github.com/OpenHands/software-agent-sdk/pull/4434)）：允许仅启用 LiteLLM instrumentation，将 init 延迟从 5.971s 降至 0.370s（E2B 环境下），对性能敏感场景有显著价值。

6. **MCP 工具热刷新**（PR [#4402](https://github.com/OpenHands/software-agent-sdk/pull/4402)）：支持活动会话中刷新后端拥有的 MCP 工具，增强 E2B 部署场景的灵活性。\


## 7. 用户反馈摘要

> 基于今日活跃 Issues 及 PR 中用户的直接评论。

- **配置不生效是用户的核心痛点**（[#3746](https://github.com/OpenHands/software-agent-sdk/issues/3746)）：用户 @xiaolei373 提供了完整的 JSON 配置样例，期望 `max_input_tokens` 在 headless 模式下生效。该问题最终被社区贡献者定位根因（`build_condenser()` 中参数丢失），体现了**用户真实场景驱动社区修复**的良性循环。

- **Windows 安装/使用困难**（PR [#4408](https://github.com/OpenHands/software-agent-sdk/pull/4408)）：贡献者 @Telov 提到 "Had issues installing OpenHands on windows. Putting up some PRs to help the community"，修复 ACP 在 Windows 上无法启动的问题（`CreateProcess` 不追加 `.exe`）。

- **生产环境日志泄露密钥的担忧**（PR [#4424](https://github.com/OpenHands/software-agent-sdk/pull/4424)）：用户（通过 bot 提交）报告 Datadog 日志中发现 API 密钥明文出现在 URL 查询参数中，是由 httpx/httpcore 的错误日志引起的，安全问题已触发修复。

- **E2B 部署用户对性能高度敏感**（PR [#4434](https://github.com/OpenHands/software-agent-sdk/pull/4434) 和 [#4426](https://github.com/OpenHands/software-agent-sdk/pull/4426)）：用户提交数据显示，限制 Laminar 初始化范围可将 init 延迟降低 94%（5.971s → 0.370s），说明**部署场景下的冷启动性能**是部分用户的核心诉求。

- **文档与示例不完整**（PR [#4418](https://github.com/OpenHands/software-agent-sdk/pull/4418)）：贡献者 @luciobaiocchi 指出 #4207 引入 `response_schema` 但没有附带可运行示例，主动补充了结构化输出的示例代码，反映**用户对开箱即用示例的高需求**。

- **Plugin 讨论长线持续**（[#1440](https://github.com/OpenHands/software-agent-sdk/issues/1440)）：该 Issue 自 2025-12-18 开启至今仍在更新（26条评论），社区对 Plugin 的边界定义（哪些属于 SDK 概念、哪些属于 OpenHands 概念）持续关注。

- **奇怪的 LLM 噪音**（PR [#4153](https://github.com/OpenHands/software-agent-sdk/pull/4153)）：用户运行 Agent Canvas 时遇到 LLM 产生 "奇怪的噪音"，期望在 `finish` 这类只读工具上允许 `security_risk` 参数以抑制。


## 8. 待处理积压

**⚠️ 长期未合并的重要 PR：**

| PR | 主题 | 等待时间 | 备注 |
|----|------|---------|------|
| [#4159](https://github.com/OpenHands/software-agent-sdk/pull/4159) | refactor(sdk): centralize LLM call context | **20 天**（07-20 创建） | 核心架构重构，关联 Issue #4433，影响面大，需评审 |
| [#4153](https://github.com/OpenHands/software-agent-sdk/pull/4153) | fix(llm): allow security_risk param on read-only tools | **21 天**（07-19 创建） | 保持 draft 状态，已等待约 3 周 |
| [#4303](https://github.com/OpenHands/software-agent-sdk/pull/4303) | fix(mcp): pin fetch server runtime dependencies | **11 天**（07-29 创建） | 阻塞依赖上游 `mcp` 2.0.0 兼容性问题 |
| [#4320](https://github.com/OpenHands/software-agent-sdk/pull/4320) | fix(profiles): repair v1 skills migration | **9 天**（07-31 创建） | 影响升级用户的 profile 可编辑性 |
| [#4325](https://github.com/OpenHands/software-agent-sdk/pull/4325) | ci: remove release security scan | **8 天**（08-01 创建） | 涉及 CI 安全策略变更，需明确决策 |

**⚠️ 长期未关闭的 Issue：**
- **[#1440 Plugin 1.0 Definition](https://github.com/OpenHands/software-agent-sdk/issues/1440)**：已开放近 8 个月，仍在活跃讨论中。随着 #4405（Agent Plugins 标准支持）的提出，建议维护者评估是否将 #1440 的结论沉淀为正式设计文档，并明确与 #4405 的关系，避免两条线并行造成社区困惑。

---

*本日报由 AI 分析师自动生成，数据截止 2026-08-09。所有链接均指向 GitHub 原始内容。*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-09

## 今日速览

过去24小时项目维护活跃：共处理34条Issue更新（关闭32条、新开/活跃2条）、12条PR更新（7条合并/关闭、5条待合并），无新版本发布。当前社区关注焦点集中在 **openai-codex 连接可靠性**（#4945，76条评论、31个👍，持续近三个月尚未关闭）与 **auto-compaction 触发时机缺陷**（#6879、#7821 等多个关联Issue）两大稳定性问题上。今日关闭的PR以针对性Bug修复为主（并发compaction崩溃、DeepSeek参数透传、TUI复制换行等），整体看项目处于高频迭代、快速响应社区反馈的健康节奏。

---

## 版本发布

无新版本发布。

---

## 项目进展

今日合并/关闭的7个PR均为针对性修复，展现了项目在**运行时诊断、稳定性、生态兼容**三个维度推进：

- **#7834 — `--version` 标注运行时信息**：`pi --version` 现在会输出 `0.84.1 (node/bun/deno)`，便于问题报告和自动化诊断区分运行环境。关闭 #7244。
- **#7833 — notify 扩展示例改用 `agent_settled`**：修复了通知在自动重试、compaction 重试完成前就误触发的逻辑缺陷。
- **#7811 — 修复原生 DeepSeek 模型的 `max_tokens`**：此前向 DeepSeek 发送 `max_completion_tokens` 会被静默忽略，参数约束失效。
- **#7817 — 将 `incomplete reason='length'` 视为正常截断**：兼容火山方舟等 OpenAI 兼容提供方的响应格式，避免误判为错误。
- **#7810 — 禁止并发 compaction 调用**：修复快速连按 `/compact` 或快捷键导致 TUI 崩溃（Reading `'signal'` of undefined）的问题。
- **#7721 — 修复全屏 TUI 复制文本时多余换行**：鼠标选择跨行文本不会再把视觉换行混入复制内容。
- **#7823 — 从 oh-my-pi 移植 A 级 agent 能力**：包括流式规则（stream rules）、subagent 工具、advisor、跨会话记忆四项功能，按功能拆分提交。

待合并的5个PR中，值得关注的有：
- **#7801 — 语法高亮懒加载**（@mitsuhiko）：实验性重构，减少启动时加载不常用语法带来的开销。
- **#7807 — 为 DeepSeek V4 Flash 暴露 `low` reasoning effort**：此前会被错误提升为 `high`。
- **#7784 — 重构 recovery 状态派生逻辑**：移除专用查询 API，改用有界 `findRecords()` 统一派生。
- **#7610 — 新增 LLM Gateway 与 DevPass providers**：OpenRouter 风格路由服务，由 LLM Gateway 团队贡献。
- **#7713 — 为 telemetry 添加 StreamAssistant 支持**：harness v2 的遥测基础能力。

---

## 社区热点

- **#4945 — openai-codex Connection Reliability Issues**（[链接](https://github.com/earendil-works/pi/issues/4945)）
  76条评论 | 31👍 | 创建于2026-05-24，持续活跃中。用户报告 `gpt-5.5` 在长思考场景下TUI卡在 `Working...`，无流式文本、无工具调用、无错误提示，只能按 Escape 中止。该Issue已积压近三个月，是当前社区最大的不满集中点。

- **#6879 — auto-compaction never triggers after context grows past 100%**（[链接](https://github.com/earendil-works/pi/issues/6879)）
  15条评论 | 15👍。单次 agentic turn 运行超过2小时，上下文超过压缩阈值后继续增长至373k token，直到 API 拒绝请求才触发 compaction。用户建议在每个 agent 步骤之后检查，而非等整个循环结束。

- **#7820 — openai-codex 流式请求无 retryProviderRequest 包装**（[链接](https://github.com/earendil-works/pi/issues/7820)）
  与 #4945 同源问题，实测约30%的长流式请求因 WebSocket 断开（1006）死亡，且无重试机制。

- **#7823 — oh-my-pi A级能力移植 PR**（[链接](https://github.com/earendil-works/pi/pull/7823)）
  该 PR 将社区插件集 oh-my-pi 的核心能力移植进 pi 主线，涉及流式规则（可在输出流中被中止、丢弃残缺部分并重试）、subagent 工具等，反映社区对核心 agent 循环能力增强的强烈需求。

---

## Bug 与稳定性

按严重程度排列：

**🔴 严重（会话中断/数据完整性）**

- **#6879 — compaction 不触发直到 provider 溢出**（[链接](https://github.com/earendil-works/pi/issues/6879)）— 长agent turn 可打爆上下文窗口。**相关PR**: #7810 仅修复了并发触发崩溃，根因尚未修复；#7821 是同一根因的后续报告。
- **#7782 — Bedrock 非法工具调用毒化会话**（[链接](https://github.com/earendil-works/pi/issues/7782)）— 含空键的工具参数被执行并持久化，导致每个后续 turn 重放且被 Bedrock 拒绝，会话永久损坏。需要参数校验/消毒机制。
- **#7825 — 恶意包报告：`@baylarsadigov/omp-undo-redo`**（[链接](https://github.com/earendil-works/pi/issues/7825)）— 用户报告该包导致消息发送延迟2~5秒，卸载后立即恢复。供应链安全需关注。

**🟠 中等**

- **#7820 — openai-codex 流式中断无重试**（[链接](https://github.com/earendil-works/pi/issues/7820)）— 约30%长流式请求因传输错误死亡，无 retryProviderRequest 包装。
- **#7821 — compaction 等待 agent_end**（[链接](https://github.com/earendil-works/pi/issues/7821)）— 长工具循环期间超阈值后继续发请求。
- **#7734 — print 模式 + 子代理 + 扩展同时存在时挂起**（[链接](https://github.com/earendil-works/pi/issues/7734)）— 0.84.0/0.83.0 重现，任务完成后进程不退出，0% CPU。
- **#7836 — 编辑模糊匹配对空白长度差异敏感**（[链接](https://github.com/earendil-works/pi/issues/7836)）— `normalizeForFuzzyMatch` 未折叠空白，小模型在编辑时易失败。
- **#7816 — Reload 时 in-flight 命令报错 stale context**（[链接](https://github.com/earendil-works/pi/issues/7816)）。

**🟡 轻微/体验问题**

- **#7837 — 全屏 TUI 鼠标选择静默覆盖系统剪贴板**（[链接](https://github.com/earendil-works/pi/issues/7837)）— 无修饰键、无设置项可关闭 OSC 52 写入。
- **#7829 — Windows 无效 settings.json 报误导性错误**（[链接](https://github.com/earendil-works/pi/issues/7829)）— 反斜杠未转义导致 JSON 解析失败，却提示 `bash not found`。
- **#7832 — Mermaid `:::className` 语法渲染失败**（[链接](https://github.com/earendil-works/pi/issues/7832)）。
- **#7831 — RPC 会话替换导致扩展重复绑定**（[链接](https://github.com/earendil-works/pi/issues/7831)）— `session_start` 与资源事件触发两次。
- **#7806 — macOS 终端滚动 Bug**（[链接](https://github.com/earendil-works/pi/issues/7806)）— 流式输出时滚轮自动跳到顶部，无法留在历史查看位置。

---

## 功能请求与路线图信号

- **Meta Model API 接入**（[#7543](https://github.com/earendil-works/pi/issues/7543)）— 请求支持 Meta 的 Muse Spark，按现有 provider 模式即可实现，难度低、社区有需求。
- **多配置 Profile 支持**（[#7813](https://github.com/earendil-works/pi/issues/7813)）— 按 CLI 参数/环境变量区分多套 settings，被关闭但代表明确需求。
- **单 Provider 多账号登录**（[#7814](https://github.com/earendil-works/pi/issues/7814)）— 两个 ChatGPT Plus 订阅同时使用，避免自建 provider 扩展。
- **扩展侧终止 turn 的能力**（[#7824](https://github.com/earendil-works/pi/issues/7824)）— 让扩展能主动结束 agent run，以及调用方控制 RpcClient 超时/关闭。
- **消息身份暴露给 Markdown 转换器**（[#7828](https://github.com/earendil-works/pi/issues/7828)）— 添加 `messageId` 到 transformer context，按消息做装饰。
- **删除当前激活会话并返回主页**（[#7818](https://github.com/earendil-works/pi/issues/7818)）— 当前 active session 被禁止删除，只能从 resume 选择器删。
- **UI/交互类**：全屏 TUI 逐行滚动（[#7830](https://github.com/earendil-works/pi/issues/7830)）、滚轮步长可配置（[#7765](https://github.com/earendil-works/pi/issues/7765)）、描述过长时弹出横向滚动（[#7827](https://github.com/earendil-works/pi/issues/7827)）、删除当前 session（[#7818](https://github.com/earendil-works/pi/issues/7818)）、输入后立即显示用户消息（[#7819](https://github.com/earendil-works/pi/issues/7819)）。
- **并行 Pi 进程会话隔离**（[#7812](https://github.com/earendil-works/pi/issues/7812)）— 文档化或强制要求传 session 目录/ID。

---

## 用户反馈摘要

- **对 openai-codex 连接体验失望**：多个用户独立报告同一类问题（卡 `Working...`、WebSocket 1006 断开、无重试），说明该 provider 路径在长流式场景下尚未达到生产可用标准，社区期待优先修复。
- **对上下文压缩机制有较高期待**：#6879 的 15👍 与 #7821 的出现，说明用户对超过100%上下文窗口后系统不主动介入的现象敏感，期望更积极的资源保护策略。
- **对扩展机制的灵活性需求增强**：#7824、#7828、#7816 指向同一个方向 — 扩展开发者在更细粒度上干预和控制 Pi 行为的诉求正在增加。
- **用户体验细节受关注**：从复制粘贴的换行（#7721 已修复）、滚动行为（#7806、#7830）、剪贴板覆盖（#7837）到 Cmd+V 粘贴图片（#4332），用户对终端 UI 细节打磨有明显期待。

---

## 待处理积压

- **#4945 — openai-codex 连接可靠性问题**（[链接](https://github.com/earendil-works/pi/issues/4945)）— ⚠️ **最高优先级关注**。创建于3个月前，76条评论、31个👍，至今仍未解决。关联 #7820、#7821 等新报告进一步佐证问题广泛存在，建议维护者优先排查。
- **#6879 — compaction 触发机制缺陷**（[链接](https://github.com/earendil-works/pi/issues/6879)）— 自7月20日报告至今近3周无 fix PR，已产生衍生 Issue #7821。
- **#7543 — Meta Model API 请求**（[链接](https://github.com/earendil-works/pi/issues/7543)）— 社区贡献了清晰的接入路径，但被以 `no-action` 关闭，建议维护者回复说明是否暂不支持第三方新增 provider 或计划在其他版本纳入。
- **#4332 — Cmd+V 粘贴图片**（[链接](https://github.com/earendil-works/pi/issues/4332)）— 5月报告至今被标记 `closed-because-weekend`，但该交互缺陷在 macOS 用户中依然存在。
- **待合并 PR 提示**：#7801（语法懒加载）和 #7784（recovery 重构）已分别等待2天，建议尽快 review，减少分支漂移成本。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报（2026-08-09）

## 1. 今日速览

过去 24 小时 LiteLLM 项目继续保持高活跃度：共 22 条 Issue 更新（19 条活跃 / 3 条关闭），153 条 PR 更新（106 条待合并 / 47 条已合并或关闭），并发布 1 个新版本 v1.94.2。开发重心集中在三个方向：**可观测性与 OTEL 多租户出口**、**自适应路由/自动路由质量评估**、**批处理成本归因与预算作业稳定性**。Issue 侧则有多个值得警惕的回归报告（如 #36275 的 responses API 空输出），同时一条从 2025 年 5 月持续至今的日志控制 Issue（#10788）评论数仍在增长，显示用户对基础体验问题耐心正在消耗。整体判断：项目迭代速度快、功能管线丰富，但需要加强对回归的快速响应与长期积压问题的治理。

---

## 2. 版本发布

### v1.94.2
- **发布时间**：2026-08-08
- **核心内容**：本次发布聚焦供应链安全，补充了 **Docker 镜像签名验证（cosign）** 的正式说明。所有 LiteLLM Docker 镜像均使用 cosign 签名，每次发布使用统一密钥（引入于 commit `0112e53`），用户可按文档验证镜像完整性。
- **破坏性变更**：无（描述中未提及）。
- **迁移注意事项**：升级无特殊操作；建议在生产环境引入镜像签名校验，确保部署物与官方 release 一致。

> 说明：release 注释本身较短，未包含功能变更明细；功能变更请结合下方 PR 管线观察。

---

## 3. 项目进展

过去 24 小时有 **47 个 PR 被合并/关闭**、**3 个 Issue 被关闭**。从可观察到的 PR 列表看，当前主线进展如下：

**已关闭的重要 Issue（代表问题解决）**
- [#35530 [Security] 原始 provider 文件 ID 绕过托管文件所有权检查](https://github.com/BerriAI/litellm/issues/35530) — 安全问题关闭，涉及文件检索/内容/删除端点的租户所有权校验修复，值得确认补丁覆盖范围。
- [#35133 Vertex batch 创建返回不透明 HTTP 500（list index out of range）](https://github.com/BerriAI/litellm/issues/35133) — 批处理错误传播修复已关闭。
- [#31966 /v1/models 不解析实体 Access Groups](https://github.com/BerriAI/litellm/issues/31966) — 权限模型相关缺陷修复。

**进行中的高价值 PR（反映开发方向）**
- **OTEL 可观测性重构系列**（[#35513](https://github.com/BerriAI/litellm/pull/35513)、[#35514](https://github.com/BerriAI/litellm/pull/35514)、[#35515](https://github.com/BerriAI/litellm/pull/35515)、[#35516](https://github.com/BerriAI/litellm/pull/35516)、[#35517](https://github.com/BerriAI/litellm/pull/35517)）：管理员级日志目标（destination）凭证、按团队/组织解析 trace 出口、在 `/team/info` 与 `/organization/info` 中披露解析结果、UI 管理入口——这一系列将把现有"代理级全局 OTEL 单出口"升级为"多租户可配置导出"。
- **自适应/自动路由**：shadow eval 预评估（[#36250](https://github.com/BerriAI/litellm/pull/36250)）、升级/弃用质量信号（[#36255](https://github.com/BerriAI/litellm/pull/36255)）、效率后验（EURo 参考设计移植，[#36199](https://github.com/BerriAI/litellm/pull/36199)）、分档基准图表（[#36291](https://github.com/BerriAI/litellm/pull/36291)）——路由从"省钱"向"省钱且保质"演进。
- **PTU 计费**：每日按活跃小时写入 flat cost（[#35343](https://github.com/BerriAI/litellm/pull/35343)）、模型表单与 Usage 页 UI（[#35393](https://github.com/BerriAI/litellm/pull/35393)）、opt-in 环境变量门控（[#36138](https://github.com/BerriAI/litellm/pull/36138)）——为 Provisioned Throughput 场景补齐成本核算闭环。
- **批处理成本归因**：[#34456](https://github.com/BerriAI/litellm/pull/34456) 修复 Vertex 批处理成本无法归属到 key/team/tags 的问题。
- **预算重置作业**：[#36287](https://github.com/BerriAI/litellm/pull/36287) 引入原子预算级联、leader election 与分块扫描，解决 Postgres 超时导致重置中断、多 pod 并发冲突。

**结论**：项目正向"企业级网关"方向稳步推进，尤其是计费、可观测性、路由质量三块基础设施，整体前进约 2-3 个功能里程碑。

---

## 4. 社区热点

| 条目 | 类型 | 评论数 | 核心诉求 |
|---|---|---|---|
| [#10788 代理服务器 INFO 日志无法关闭](https://github.com/BerriAI/litellm/issues/10788) | Issue | 12 | `LITELLM_LOG=ERROR` 不生效，每条请求的 INFO 日志刷屏，需要可靠的日志级别

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报（2026-08-09）

## 1. 今日速览

过去 24 小时内 Temporal 核心仓库活跃度中等偏上：无新增或关闭的 Issue，PR 侧共有 6 条更新，其中 2 条已关闭（含发布分支准备与可靠性验证器应用）、4 条待合并。开发重点集中在 **CHASM Callback 功能栈**（回调完成回调、终态失败持久化）与 **reliability-2026** 可靠性加固两项主线上。值得注意的是，1.32.0 发布分支准备 PR 已关闭，暗示新版本发布流程可能已启动或临近。

## 2. 版本发布

今日无新版本发布。

但需关注 [#11449](https://github.com/temporalio/temporal/pull/11449)（已关闭）：该 PR 为 `1.32.0` 准备发布分支，包含覆盖治理文件与更新依赖。若该 PR 已被合并，则 1.32.0 的版本发布可能即将进入流程，建议社区用户留意后续 Release Notes，特别是依赖更新可能带来的兼容性影响。

## 3. 项目进展

今日关闭的两个 PR 是主要进展：

- **[#11449: Prepare release branch for 1.32.0](https://github.com/temporalio/temporal/pull/11449)**（关闭）  
  由 CI 机器人创建，为 1.32.0 版本初始化发布分支，更新了仓库治理文件和依赖版本。这是版本发布流程的关键前置步骤，标志着 1.32.0 已进入发布前准备阶段。

- **[#11442: Apply Callback Validator to Workflow Update Callbacks](https://github.com/temporalio/temporal/pull/11442)**（关闭）  
  `reliability-2026` 系列的一部分，将 Callback Validator 一致性地应用于 Workflow Update Callbacks。新增了单元测试与功能测试，修复了验证逻辑覆盖不完全的问题，提升了回调路径的可靠性。

另有 4 个待合并 PR 持续推进：

- **CHASM Callback 功能栈**（并非直接进入 main，而是合入特性分支）：  
  - [#11415: Add completion callbacks to SANOs](https://github.com/temporalio/temporal/pull/11415) 扩展 worker callbacks 的 API surface，新增 `completion_callbacks` 字段。  
  - [#11413: Persist Callback terminal failures](https://github.com/temporalio/temporal/pull/11413) 为 CHASM Callback 组件新增持久化终态失败字段，使回调失败状态可被记录和恢复。  
  这两项合在一起，正在为 Callback 功能补齐“执行完成后通知”和“终态失败持久化”的能力。

- **可靠性加固**：  
  - [#11433: Assert that an executed CHASM pure task has become invalid](https://github.com/temporalio/temporal/pull/11433) 实现了 `Node.EachPureTask` 中遗留的 TODO——纯任务执行后重新校验有效性，若仍有效则通过 softassert 返回内部错误，加强对异常状态的检测力度。

整体来看，项目正在从“Callback 功能开发”和“系统可靠性体系化加固”两个方向稳步前进，同时 1.32.0 的发布准备工作也已在推进中。

## 4. 社区热点

今日 Issues 与 PR 均无评论、无点赞，外部社区互动几乎为零。全部 6 条 PR 均为内部开发或机器人自动化操作，暂无值得关注的高热度讨论。从近期 PR 密集度看，CHASM Callback 与可靠性主题是当前内部最关注的方向，但尚未形成外部社区热议。

## 5. Bug 与稳定性

今日无新 Bug Issue 上报，无崩溃或回归类报告。以下更新与稳定性相关，但不属于线上缺陷：

- **[#11443: Fixing test task manager for new matchers](https://github.com/temporalio/temporal/pull/11443)**（开放）  
  修复测试任务管理器以适配新的 matcher 机制。属于测试基础设施的兼容性修复，可视为内部工程质量优化。PR 描述未填写具体变更内容与测试方式，模板完成度较低。

- **[#11433: Assert that an executed CHASM pure task has become invalid](https://github.com/temporalio/temporal/pull/11433)**（开放）  
  属于主动防御型增强，在纯任务执行后增加二次校验，防止因任务状态未正确失效而导致的潜在错误。该 PR 包含 softassert 机制，可在非严重故障时捕获不一致状态。

未发现需要紧急处理的高严重度 Bug。

## 6. 功能请求与路线图信号

今日无新 Issue 级别的功能请求。但在 PR 中可以看到明确的路线图信号：

- **Worker Callbacks 功能持续演进**：`#11415` 与 `#11413` 属于一个 stacked PR 系列，最终目标是为主流程加入完整的回调完成与失败持久化能力。结合此前 `reliability-2026` 系列对 Callback Validator 的强化，可以判断 **回调机制是近期版本的核心特性之一**，预计将在后续版本（可能包含 1.32.0 或其后版本）中提供更完善的公开 API。

- **reliability-2026 加固持续落地**：`#11442` 与 `#11433` 均属该计划，重点在于对 CHASM 相关任务执行状态进行更严格的验证。这意味着项目在功能开发之外，正同步提升内部一致性保障机制，降低长尾故障风险。

## 7. 用户反馈摘要

今日无任何 Issue 评论或用户反馈数据。所有 PR 均无评论互动，暂无外部使用者的满意度、痛点或场景信息可供提炼。建议关注后续发布版本后用户的反馈，特别是 Callback 功能上线后可能的使用体验反馈。

## 8. 待处理积压

当前有 4 个开放 PR 需要关注：

| PR | 说明 | 状态 |
|---|---|---|
| [#11415: Add completion callbacks to SANOs](https://github.com/temporalio/temporal/pull/11415) | Callback 新功能开发，属于 stacked PR，暂不直接进入 main，等待整体功能完成 | 开放 |
| [#11413: Persist Callback terminal failures](https://github.com/temporalio/temporal/pull/11413) | Callback 持久化功能开发，同上属于 stacked PR | 开放 |
| [#11443: Fixing test task manager for new matchers](https://github.com/temporalio/temporal/pull/11443) | 测试基础设施修复，PR 描述未完成，需补充变更说明 | 开放 |
| [#11433: Assert that an executed CHASM pure task has become invalid](https://github.com/temporalio/temporal/pull/11433) | 可靠性增强，已有明确实现方案与测试 | 开放 |

其中 `#11443` 的 PR 描述模板未填写，长期未更新的话可能被遗忘，建议维护者跟进确认是否为 WIP。`#11415` 与 `#11413` 依赖特性分支整体完成，需要跟踪上游分支合并计划。`#11433` 属于可靠性计划的一部分，应优先评审以便尽早合入主线。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*