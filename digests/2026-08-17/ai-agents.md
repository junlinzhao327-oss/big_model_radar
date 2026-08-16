# OpenClaw 生态日报 2026-08-17

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-16 22:35 UTC

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

# AI 智能体开源生态横向对比报告（2026-08-17）

> 声明：本报告基于采集到的 LiteLLM 与 Temporal 两项目完整动态数据；OpenClaw、Hermes Agent、OpenHands SDK、Pi 四项目本日摘要为空，相关分析将予以明确标注。

---

## 1. 生态全景

当前个人 AI 助手与自主智能体生态呈现明显的 **"基础设施热、应用层静"** 两极化态势。当日绝大多数的社区活力集中在 LLM 网关（LiteLLM：149 条 PR 更新、2 个版本发布）与工作流编排（Temporal：1.32.0 发布分支就绪）等支撑层；而面向终端用户与智能体应用的四个项目（OpenClaw、Hermes Agent、OpenHands SDK、Pi）均未捕获到可观测动态。热点流向集中在实时通信能力（WebSocket 透传、流式 TTS）、计费/成本核算准确性、云厂商生态适配（Azure Foundry、OpenAI Skills）与 Kubernetes 原生运维体验四大方向，表明行业正从"能不能接"转向"接得好不好、算得准不准、运维稳不稳"的深水区。

---

## 2. 各项目活跃度对比

| 项目 | Issues（新增/活跃） | PR 动态 | Release | 健康度评估 |
|------|-------|---------|---------|-----------|
| **LiteLLM** | 23 新增/活跃，7 关闭 | 149 条更新（112 待合并 / 37 合并或关闭） | v1.97.0 稳定版 + v1.98.0-rc.1 | 🟡 高速迭代但合并积压扩大（112 条待合并），存在效率瓶颈 |
| **Temporal** | 1 新增 | 5 条更新（2 关闭） | 无新版本（1.32.0 发布分支就绪） | 🟢 版本发布前质量巩固期，节奏平稳 |
| **OpenClaw** | 无数据捕获 | 无数据捕获 | 无数据捕获 | ⚪ 建议核查数据采集链路是否正常 |
| **Hermes Agent** | 无数据捕获 | 无数据捕获 | 无数据捕获 | ⚪ 同上 |
| **OpenHands SDK** | 无数据捕获 | 无数据捕获 | 无数据捕获 | ⚪ 同上 |
| **Pi** | 无数据捕获 | 无数据捕获 | 无数据捕获 | ⚪ 同上 |

**数据可信度说明**：LiteLLM 与 Temporal 为本日数据的可信主体；其余四项目要么处于低活跃期，要么存在"监测盲区"——建议后续增加对这几个仓库的 watch 配置校验。

---

## 3. OpenClaw 在生态中的定位

*（注：本日 OpenClaw 无动态数据，以下定位分析基于其作为生态核心参照的既定角色及同类项目格局推演。）*

**生态位置**：OpenClaw 处于竞争最激烈的个人 AI 助手/自主智能体框架赛道，但本日零动态使其对标者（Hermes Agent、OpenHands SDK、Pi）同期也处于静默状态，说明该赛道当前缺少"每日高吞吐"的催化剂。

**相对优势**：相比 Hermes Agent 的 NousResearch 研究血统、OpenHands SDK 聚焦软件工程垂直场景、Pi 的极简实验风格，OpenClaw 作为核心参照项目，其差异化本应体现在对**个人 AI 助手端到端闭环**的覆盖——即从模型调用、工具调用到长期记忆、多端接入的一体化设计，而非单一环节。

**技术路线差异**：
- **OpenClaw / Pi**：面向通用个人助手，侧重易用性与部署形态；
- **Hermes Agent**：研究与前沿对齐，强调模型原生 agent 能力；
- **OpenHands SDK**：垂直深耕软件工程任务（编码、调试、PR），工程化属性强。

**社区规模判断**：本日数据无法量化比较社区规模，但参照同类项目规律，Personal Agent 赛道通常"Star 多、Daily Issue/PR 稀"，与基础设施项目（LiteLLM/Temporal）的高持续活跃形成常态反差。

---

## 4. 共同关注的技术方向

基于可信数据（LiteLLM + Temporal），本日跨项目涌现的需求集中在：

| 方向 | 涉及项目 | 具体诉求 |
|------|---------|---------|
| **实时通信与流式协议** | LiteLLM | WebSocket 透传路由（#36151）、ElevenLabs 流式 TTS（#37084）、实时会话定价（#36958） |
| **计费与成本核算准确性** | LiteLLM | 批量任务计费丢失（#37077）、Gemini grounding 重复计费（#36397）、deployment 定价覆盖（#36958） |
| **认证/授权语义一致性** | LiteLLM | MCP 路由 500 而非 401（#37080）、Admin 路由 401 vs 403（#37108）、模型列表越权（#26420） |
| **云厂商生态适配** | LiteLLM | Azure AI Foundry Agents v2（#25372）、OpenAI/Azure Skills 原生路由（#37074）、Fireworks AI on Foundry（#26618） |
| **Kubernetes 原生运维** | LiteLLM | Helm 依赖仓库切换（#19769）、K8s Operator/GitOps CRD 驱动（#18428） |
| **升级路径与性能优化** | Temporal | PostgreSQL visibility schema v1.14 升级未复用重写优化（#11594） |

其中"实时/流式能力"和"成本可观测性"是当日最强烈的信号——两者共同指向一个趋势：**智能体应用正从离线任务式转向实时交互式，而商业化落地倒逼计费精确化**。

---

## 5. 差异化定位分析

| 项目 | 核心定位 | 目标用户 | 技术架构关键特征 | 竞争锚点 |
|------|---------|---------|----------------|---------|
| **LiteLLM** | 多模型网关/代理层 | AI 应用开发者、平台工程团队 | 统一 API 面 + 100+ Provider 适配 + 代理/成本管理 | 云厂商无关的中间层 |
| **OpenClaw** | 个人 AI 助手框架 | 个人用户、轻量开发者 | 端到端 agent 闭环（模型+工具+记忆） | 开箱即用的个人助手 |
| **Hermes Agent** | 研究型自主智能体 | AI 研究者、前沿开发者 | 依托 NousResearch 模型能力，追求 agent 自主性上限 | 模型-智能体深度协同 |
| **OpenHands SDK** | 软件工程 agent 开发套件 | 开发者工具链团队 | 面向编码任务的工作流抽象、环境沙箱集成 | 垂直深耕代码智能体 |
| **Pi** | 极简/实验性 agent 引擎 | 探索型开发者 | 轻量、最小化依赖，偏向原语级抽象 | 架构简洁性 |
| **Temporal** | 分布式工作流编排 | 后端/平台工程师 | 持久化执行、确定性重放、可视性 | 可靠性优先的任务编排 |

本质区别：**基础设施层（LiteLLM/Temporal）卖确定性，应用层（OpenClaw/Hermes/OpenHands/Pi）卖智能性**。前者本日获得社区密集投票，后者处于观望趋势。

---

## 6. 社区热度与成熟度

**按活跃度分层：**

| 层次 | 项目 | 阶段特征 |
|------|------|---------|
| **快速迭代层** | LiteLLM | 日 PR 149 条、双版本发布，社区贡献者密集修补计费与实时协议细节；但 112 条待合并 PR 显示合并管线已成为瓶颈 |
| **质量巩固层** | Temporal | 1.32.0 发布分支持续准备，测试 shard 优化、无新功能合并；社区关注点聚焦升级路径细节，属成熟项目典型节奏 |
| **静默/盲区层** | OpenClaw / Hermes Agent / OpenHands SDK / Pi | 本日零捕获动态；需区分"低活跃"与"数据采集缺失"，不排除项目处于设计/重构间歇期 |

**趋势解读**：LiteLLM 的 PR 合并积压（112 条）与 Temporal 的"发布分支准备"形成对照——一个在扩张中承受效率压力，一个在收敛中稳扎稳打。这反映开源项目生命周期中"快速扩张→整合巩固"的典型交替。

---

## 7. 值得关注的趋势信号

1. **实时交互成为智能体基础能力**：LiteLLM 集中为 WebSocket 透传、流式 TTS、realtime sessions 打补丁，说明智能体应用正从"请求-响应"范式转向"持久连接+流式多模态"范式。对开发者而言，网关层对 WebSocket 协议的支持度应纳入选型指标。

2. **计费精确性成为生产化门槛**：本日至少 4 个计费类 PR/Issue（#37077、#36958、#36397 等），覆盖批量任务、实时会话、grounding 搜索等新场景。若网关计费不可信，多 agent 商业化就无从谈起——这可能是比功能数量更优先的评估维度。

3. **鉴权语义错误正在积累技术债**：500 vs 401、401 vs 403 等 HTTP 语义错误被密集报告且无修复 PR，反映高速迭代中对安全边界的打磨滞后。AI 网关已成为基础设施，其鉴权一致性应等同传统 API 网关对待。

4. **云厂商生态适配是最大外部驱动力**：Azure Foundry Agents v2、OpenAI Skills、Fireworks AI on Foundry 等请求均指向"跟随微软/OpenAI 平台演进"的社区焦虑。多模型网关的生命力正取决于对云生态迁移节奏的响应速度。

5. **K8s 原生运维从"可选"变"必备"**：Helm 依赖治理（#19769）与 Operator/GitOps CRD 化（#18428）获得数月持续关注，说明企业级部署需求已从单机 Docker 转向多租户 K8s 集群。若 OpenClaw 等应用层项目未来有企业化计划，应提前布局 Helm Chart 与 Operator 支持。

6. **升级路径的"公平性"影响用户信任**：Temporal 的 schema 升级优化遗漏（#11594）虽是细节，却暴露大版本快速迭代中对历史路径的覆盖不足。对所有平台型项目：**版本升级体验与新增功能同等重要**，应纳入发布验收清单。

---

*报告完，数据截止 2026-08-17 社区动态摘要。*

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

# LiteLLM 项目动态日报 — 2026-08-17

## 今日速览

LiteLLM 过去 24 小时保持高活跃度：新增/活跃 Issue 23 条、关闭 7 条；PR 更新 149 条（其中 112 条待合并，37 条已完成合并或关闭），并发布 1 个 Release 候选版（v1.98.0-rc.1）和 1 个稳定版（v1.97.0）。值得关注的是，今日新提交的 PR 在实时通信（WebSocket 透传、ElevenLabs 流式 TTS）、新 Provider 集成（OpenCode 双变体、Levo AI Guardrail、Azure Skills）以及计费/成本核算修复上均有明显发力。虽然 PR 提交量大，但待合并 PR 池仍在扩大（112 条），合并效率或成项目短期瓶颈。与此同时，多个涉及认证/授权语义（401 vs 403）与计费准确性的 Bug 被集中报告，值得维护团队优先关注。

---

## 版本发布

两个新版本均只附带了 Docker 镜像签名验证说明，未在 release notes 中提供详细变更日志，建议前往 [GitHub Releases 页面](https://github.com/BerriAI/litellm/releases) 获取完整信息。

### v1.97.0（稳定版）
- 链接：https://github.com/BerriAI/litellm/releases/tag/v1.97.0
- 当前 release 说明仅包含 cosign 镜像签名验证指引，未提供功能变更明细。
- 建议用户关注此版本对应的 commit 历史以评估升级影响。

### v1.98.0-rc.1（候选版）
- 链接：https://github.com/BerriAI/litellm/releases/tag/v1.98.0-rc.1
- 与 v1.97.0 的 release 说明格式一致，未列出新功能或破坏性变更。

**迁移注意事项**：在官方变更日志补充之前，生产环境升级建议先以 v1.97.0 为准进行回归测试，暂缓采用 rc.1。

---

## 项目进展

今日没有明确标注为 "MERGED" 的 PR 出现在数据前 20 条中，但以下 PR 被标记为 **CLOSED**（状态需结合具体关闭原因判断）：

- **#33938 fix: content_block_delta type mismatch when reasoning and content arrive in one chunk** — 修复 Anthropic 流式响应中 reasoning 与 content 同 chunk 到达时 `content_block_delta` 类型不匹配的问题。作者在 checklist 中未勾选 CI 通过项，关闭原因可能是 CI 或测试未通过。[PR 链接](https://github.com/BerriAI/litellm/pull/33938)
- **#33860 fix: omit empty tools array in responses to chat completion transformation** — 修复 Responses API 转换为 Chat Completions 时携带空 `tools` 数组的问题。同样未勾选 CI 通过项。[PR 链接](https://github.com/BerriAI/litellm/pull/33860)
- **#37120 fix(proxy): register WebSocket passthrough for OpenAI prefixes (CI mirror of #36151)** — 这是一个 CI 辅助镜像 PR，不是功能 PR。它为了让 #36151（WebSocket 透传）能触发 GitHub Actions 检查而创建，完成后会关闭，不应合并或审查。[PR 链接](https://github.com/BerriAI/litellm/pull/37120)

在**待合并**队列中，以下 PR 展示了项目正在推进的增量改进：

- **WebSocket 能力扩展**：#36151 为 /openai 和 /openai_passthrough 前缀注册 WebSocket 透传路由，解决 `client.realtime.connect()` 和 `client.responses.connect()` 无法通过代理的问题；#37084 为 ElevenLabs 新增 WebSocket 流式输入 TTS 端点，开发者无需再缓冲完整文本再合成，可降低首字延迟数百毫秒。
- **计费与成本核算修正**：#37077 修复批量任务检索时丢失模型身份导致计费为 $0 的问题，改为按 deployment 自身模型与费率定价；#36958 使实时会话（realtime sessions）尊重 deployment 的 `model_info` 定价覆盖；#36397 修复 Gemini 3 grounding 按 web search query 计费时对深度多轮搜索的重复计费问题。
- **Bedrock 批量任务增强**：#34087 为 Bedrock 托管批量任务增加取消能力（调用 `StopModelInvocationJob`）；#36392 修复托管批量上传返回 `bytes: 0` 的问题。
- **基础设施/可观测性**：#37123 与 #37122 分别修复 Uvicorn 默认 JSON 日志中的 secret 泄露和 `%s://%s:%d` 占位符未被替换的问题（后者直接修复 #37121）。

整体来看，项目在维持高迭代速度的同时，社区贡献者开始密集修补计费准确性和流式/实时场景的协议细节。

---

## 社区热点

基于评论数和 👍 数，以下议题是社区关注焦点：

- **#19769 Helm Chart 依赖仓库切换建议（8 评论 / 5 👍）** — 受 Bitnami 目录政策变化影响，社区建议将 PostgreSQL 和 Redis 依赖切换到 Cloudpirates 等维护更稳定的仓库。这是一个影响所有 Helm 部署用户的基础设施决策，讨论热度贯穿数月，但仍处于 open 状态。https://github.com/BerriAI/litellm/issues/19769

- **#25372 支持 Azure AI Foundry Agents v2（5 评论 / 4 👍）** — 用户希望 LiteLLM 支持微软新的 Foundry Agents v2 体验（Responses API + `agent_reference`），该 API 已弃用旧的 Assistant API。此为微软生态迁移的风向标，相关功能请求与今日新增的 #37074（OpenAI/Azure Skills 原生路由）形成呼应。https://github.com/BerriAI/litellm/issues/25372

- **#27460 Payload tags 不再被识别（7 评论）** — 用户报告 v1.83.9-nightly 之后 `metadata.tags` 中的标签不再生效，且未报错。由于涉及可观测性数据链路，有 7 条跟进评论，说明影响面较广。https://github.com/BerriAI/litellm/issues/27460

- **#18428 Kubernetes Operator / GitOps 深度集成（5 评论 / 5 👍）** — 来自 2025 年 12 月的长期功能请求，希望引入 CRD 驱动的动态配置（LLMModel、MCPServer、LLMGuardrails），支持 namespace 级多租户与自助服务。这是社区对运维现代化最集中的诉求之一。https://github.com/BerriAI/litellm/issues/18428

- **#26618 支持 Azure Foundry 上的 Fireworks AI 模型（5 评论）** — 已标记为 CLOSED，但其中提到的模型阵容（DeepSeek V3.2、gpt-oss-120b、Kimi K2.5、MiniMax M2.5）与 Azure Foundry 多模型生态布局一致。https://github.com/BerriAI/litellm/issues/26618

**分析**：社区热度最高的议题集中在三类诉求——① 云厂商生态适配（Azure Foundry / OpenAI Skills / Agents v2）；② Kubernetes 原生运维体验（Helm 依赖、Operator、GitOps）；③ 可观测性与计费准确性回归。这与项目近期发布节奏中成本核算修复 PR 较多的事实相互印证。

---

## Bug 与稳定性

按严重程度排列：

### 高严重度（鉴权/安全语义错误）

- **#37080 MCP 路由返回 HTTP 500 而非 401** — 任何 MCP 网关路由在缺少或携带无效 `Authorization` 时返回 500 `{"error":"MCP request failed"}`，ProxyException 泄漏到通用异常处理器。认证失败被伪装成服务器内部错误，影响客户端重试逻辑和排障。暂无 fix PR。[Issue](https://github.com/BerriAI/litellm/issues/37080)
- **#37108 Admin-only 路由拒绝返回 401 而非 403，且 Prometheus 记录 `exception_status="None"`** — 非管理员调用管理路由被拒绝时状态码语义错误、指标元数据缺失，可能导致监控告警失准。暂无 fix PR。[Issue](https://github.com/BerriAI/litellm/issues/37108)
- **#26420 GET /v1/models 忽略 `user.models` 限制** — 用户被限制在某个 access group 内时，仍可看到全量代理模型列表（虽然调用受限模型会被 401），存在模型列表信息泄露风险。暂无 fix PR。[Issue](https://github.com/BerriAI/litellm/issues/26420)

### 中高严重度（功能回归/错误路由）

- **#28561 Bedrock rerank 升级后完全不可用** — 从 v1.83.14 升级到 v1.85.0 后 `Unable to map Bedrock request to provider`，用户已定位疑似根因（changelog 相关改动），尚在等待官方确认或修复。暂无 fix PR。[Issue](https://github.com/BerriAI/litellm/issues/28561)
- **#36928 `interactions.create()` 静默丢失 `response_format`（Gemini）** — 进程级设置 `USE_LITELLM_PROXY=true` 后，Gemini 模型的 `response_format` 被静默丢弃，影响结构化输出场景。暂无 fix PR。[Issue](https://github.com/BerriAI/litellm/issues/36928)
- **#37088 `/v1/messages` 将 openai/ 自定义 api_base 模型错误路由到 Responses API** — 当上游仅

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报（2026-08-17）

## 1. 今日速览

过去24小时内，Temporal 项目保持中等活跃度：新增1个Issue、5个PR有更新，其中2个PR被关闭（包含1.32.0发布分支准备）。目前未发布新版本，但1.32.0的发布分支已准备就绪，暗示版本发布临近。社区关注点集中在PostgreSQL visibility schema v1.14升级路径未应用查询优化这一潜在性能问题上（#11594），该项目为PR #10371在后续版本中的遗漏。整体来看，项目临近版本发布期，稳定性与性能优化的讨论热度处于正常水平。

---

## 2. 版本发布

**无新版本发布。**

> 注：今日有 PR #11593（[链接](https://github.com/temporalio/temporal/pull/11593)）完成 1.32.0 发布分支的准备，该 PR 已关闭，通常意味着版本发布流程已启动，预计 1.32.0 版本将在近期正式发布。

---

## 3. 项目进展

今日无重大功能合并，但以下 PR 值得关注：

- **[#11593] 1.32.0: Prepare release branch**（[链接](https://github.com/temporalio/temporal/pull/11593)）— 已关闭，完成 1.32.0 发布分支的准备，包括覆盖治理文件和更新依赖。该动作标志着 1.32.0 已进入发布倒计时阶段。
- **[#11590] Update test shard salt**（[链接](https://github.com/temporalio/temporal/pull/11590)）— 已关闭，由优化测试分片工作流自动生成，用于改善测试并行分片的稳定性，属于持续性的工程质量维护。

这两个 PR 表明项目正处于「发布准备 → 质量保障」的过渡期，没有引入新功能，但为版本发布铺平了道路。

---

## 4. 社区热点

今日社区讨论的焦点集中在唯一新开的 Issue 上：

- **[#11594] PostgreSQL visibility v1.14 schema upgrade misses the v1.10–v1.13 rewrite optimization**（[链接](https://github.com/temporalio/temporal/issues/11594)）— 作者 @tsurdilo 指出，PR #10371 对 PostgreSQL visibility 升级在 schema 版本 v1.10–v1.13 段做了性能优化，但 v1.14 的迁移未包含该优化。这意味着从 1.29 升级到 1.31 的用户，在升级到 v1.14 schema 时仍需执行一次额外的重写操作（如组合重写），导致升级时间变长。

**诉求分析**：该 issue 反映了用户对升级路径性能的关注，尤其是大型部署中对迁移耗时的敏感度。提交者 @tsurdilo 是 Temporal 社区的活跃成员，推测其代表了一批在生产环境中使用 PostgreSQL visibility 存储的大型用户。该问题不涉及数据损坏，但会显著影响升级效率。

---

## 5. Bug 与稳定性

今日仅报告1个Bug，按严重程度评估如下：

| 严重程度 | Issue/PR | 描述 | 状态 |
|---------|----------|------|------|
| 🟡 中等（性能/升级效率） | [#11594](https://github.com/temporalio/temporal/issues/11594) | PostgreSQL visibility v1.14 schema升级未应用v1.10–v1.13的查询重写优化，导致升级路径非最优 | 未关闭，无评论，尚无关联修复PR |

**分析**：该问题非功能性bug，不影响运行稳定性，但会延长特定版本路径下的升级时间。由于它是 PR #10371 的遗漏，修复难度预计不大（将 v1.14 的迁移逻辑对齐到优化模式即可）。考虑到 1.32.0 发布分支已准备好，此问题有可能在 1.32.0 中修复，或作为已知限制在 release notes 中说明。

---

## 6. 功能请求与路线图信号

今日无新增功能请求（Feature Request）。但以下 PR 提供了路线图信号：

- **[#11578] Fix execution last running clock on start**（[链接](https://github.com/temporalio/temporal/pull/11578)，仍 OPEN）— 修复执行记录在启动时的 last running clock 问题，属于数据一致性的修补方向，已提交 2 天但暂无评论和 reviewer 指派，可能需要维护者关注。
- **[#9980] WIP: Add HostHealthAggregator**（[链接](https://github.com/temporalio/temporal/pull/9980)，仍 OPEN 且标记为 stale）— 用于聚合 Temporal 组件的健康状态并通过 DeepHealthCheck 输出，属于系统级可观测性方向。该 PR 已存在 4 个月且被标记为 stale，但今日有更新（更新时间 2026-08-16），可能意味着作者重新开始推进。

**路线图推断**：通过 DeepHealthCheck 暴露更细粒度健康状态（#9980）可能是长期规划的一部分；短期版本 1.32.0 大概率以稳定性修复和内部优化为主，不包含重大新功能。

---

## 7. 用户反馈摘要

今日 Issue 评论区无直接用户反馈，但可从 #11594 的描述中提炼用户痛点：

- **升级时长痛点**：用户 @tsurdilo 明确描述了从 1.29 升级到 1.31 时需执行额外重写操作的场景。在大型数据库中，schema 升级意味着数小时甚至更长时间的维护窗口。用户期望所有 schema 版本升级段都享有同等的优化待遇，这反映了生产环境用户对「升级开销可预期、可最小化」的强烈需求。

---

## 8. 待处理积压

以下 Issue/PR 需要维护者特别关注：

- **[#9980] WIP: Add HostHealthAggregator**（[链接](https://github.com/temporalio/temporal/pull/9980)）— 打开已 4 个月，标记为 stale，但今日有动态更新。建议维护者确认是否纳入近期路线图，或引导作者关闭/拆分。
- **[#11578] Fix execution last running clock on start**（[链接](https://github.com/temporalio/temporal/pull/11578)）— 已打开 3 天，无评论、无 reviewer。此修复涉及执行数据一致性，建议指定 reviewer 尽快审查，避免随版本发布窗口被遗漏。
- **[#11594] PostgreSQL visibility v1.14 schema 升级优化遗漏**（[链接](https://github.com/temporalio/temporal/issues/11594)）— 新开问题但零讨论。鉴于其影响版本升级效率且修复路径清晰，建议维护者优先确认该问题是否会影响正在准备的 1.32.0 版本。

---

## 项目健康度总结

Temporal 当前处于「版本发布前期」的健康状态：开发焦点从新功能转向发布准备（#11593）与测试基础设施维护（#11590/#11592）。社区反馈活跃度中等，新 Issue 聚焦于升级路径的细节优化。建议维护者在 1.32.0 发布前重点确认 #11594 是否需在版本中处理，并推动 #11578 的审查进度。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*