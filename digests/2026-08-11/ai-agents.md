# OpenClaw 生态日报 2026-08-11

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-10 22:36 UTC

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

# 个人 AI 助手 / 自主智能体开源生态横向对比分析报告
**日期：2026-08-11**

---

## 1. 生态全景

当前个人 AI 助手与自主智能体生态正处于**从单点工具向标准化基础设施演进**的关键阶段。多项目不约而同地围绕 **Agent Plugins 可移植包格式**（agent-plugins.org v1.0.0 WD）进行架构适配，OpenHands 已拆解 4 个落地设计子 Issue，Pi 亦被社区要求原生支持该规范。与此同时，**AI 网关/代理层**（LiteLLM、Pi AI Gateway）正在成为企业落地的核心基础设施，预算执行、PII 脱敏、多模型路由等治理能力需求密集涌现。资源生命周期管理（连接泄漏、GC 阻塞）在 Temporal、OpenHands 中形成系统性修复浪潮，标志着生态正从"功能扩张期"进入"稳定性巩固期"。值得注意的是，**MCP 生态的高可用性预期**正在成为新共识——单个 MCP server 的故障不应导致整个会话终止。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | 新开/活跃 | 关闭 | 待合并 | 合并/关闭 | Release | 健康度评估 |
|---|---|---|---|---|---|---|---|---|
| **OpenClaw** | 无数据 | 无数据 | — | — | — | — | 无 | ⚪ 数据缺失（核心参照项目，但本期无动态可追踪） |
| **Hermes Agent** | 无数据 | 无数据 | — | — | — | — | 无 | ⚪ 数据缺失 |
| **OpenHands SDK** | 14 | 31 | — | — | 21 | 10 | 无 | 🟢 高 — 稳定性修复与架构前瞻并行，GC wedge 高危问题已闭环 |
| **Pi** | 138 | 19 | 28 | 110 | 9 | 10 | 无 | 🟢 高 — 维护响应极快（80% Issue 关闭率），但 `[no-action]` 批量关闭需留意误判风险 |
| **LiteLLM** | 64 | 201 | 56 | 8 | 152 | 49 | **v1.96.0**（cosign 签名） | 🟡 中上 — 功能迭代极快（49 PR/日），但 Issue 积压压力大，2 个资金/安全级 Bug 拖期 3.5 个月 |
| **Temporal** | 4 | 31 | 2 | 2 | 23 | 8 | 无 | 🟢 高 — 资源泄漏系统性治理取得实质进展，当天报告的 SDK 泄漏即获 PR 跟进 |

> 注：OpenClaw、Hermes Agent 无本日报数据，无法量化评估。若其保持"核心参照"定位，建议补齐追踪源后再行判断。

---

## 3. OpenClaw 在生态中的定位

由于本期缺少 OpenClaw 的可量化动态，以下评估基于其**"核心参照"定位**及生态内其他项目的间接信号：

- **生态位判断**：OpenClaw 在生态中扮演**智能体运行时与插件标准的定义者**角色，类比 Kubernetes 之于容器生态。其他项目的适配行为（OpenHands 的 PluginFormat 策略重构、Pi 社区的 plugin.json 诉求）均指向 OpenClaw 所推动的 **agent-plugins.org** 标准正在成为跨厂商互操作的事实基线。
- **技术路线差异**：与 LiteLLM（网关治理）和 Pi（终端原生体验）不同，OpenClaw 聚焦**智能体可移植性**——即"一次编写，多智能体运行"的插件封装规范。这与 OpenHands 的 SDK 化路线形成互补而非竞争。
- **社区规模与影响力**：agent-plugins.org 的 TSC 成员覆盖 Amazon、Cursor、Microsoft 等头部厂商，表明 OpenClaw 主导的标准已具备**跨生态杠杆**。其对标的是"智能体领域的 npm/Homebrew"。
- **风险提示**：核心参照项目一旦更新节奏放缓（本期无动态），可能影响下游生态对新标准的跟进信心。建议关注其未来两周是否有 Release 或 Roadmap 更新。

---

## 4. 共同关注的技术方向

| 方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **Agent Plugins 可移植包格式** | OpenHands（#4405 + 4 子 Issue）、Pi（#7776） | 支持 agent-plugins.org 的 plugin.json 清单、MCP 配置打包、安全边界（路径强制+窄失败）；OpenHands 已重构 PluginFormat 策略模式为其铺路 |
| **MCP / 外部服务容错降级** | OpenHands（#4454）、Pi（#7882、#7899） | 单个 MCP server 不可达时降级为"不带该工具继续运行"而非 500；Pi 对 Bedrock 空 key 工具调用、TTY 输入时序异常做防御性处理 |
| **多模型路由与网关扩展** | LiteLLM（#31876、PR #36459）、Pi（#7901） | per-deployment 失败策略差异化、tag 维度限流；Pi 新增 Cloudflare Workers AI Gateway 传输层，实现 Worker 内运行 |
| **资源泄漏与运行时稳定性** | Temporal（#11296/#11437/#11460）、OpenHands（#4416/#4417） | 消除 gRPC 连接泄漏、GC 全停（wedge）、SDK 客户端释放顺序错误——两个项目不约而同进入"深度资源治理"阶段 |
| **可观测性与成本治理** | LiteLLM（流式 usage 少计 #36114、SpendLogs 批量更新）、OpenHands（遥测区分自动化会话 #4425）、Temporal（指标基数无界 #9945） | 计费数据准确性、遥测语义化、监控指标生命周期管理成为规模化部署刚需 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键特征 |
|---|---|---|---|
| **OpenClaw** | 智能体插件标准与运行时（参照实现） | 智能体开发者、插件作者、厂商 | 以 agent-plugins.org 规范为核心，跨智能体互操作；定义 plugin.json/mcp.json 加载与安全边界 |
| **OpenHands SDK** | 软件代理可嵌入 SDK（agent-as-a-service） | 将 Agent 能力嵌入自有产品的开发者 | Pydantic 领域模型 + asyncio 事件循环 + 插件策略模式；SDK 形态便于二次开发 |
| **Pi** | 终端原生 AI 编码助手（TUI-first） | 追求极致终端体验的开发者、多 Provider 用户 | Rust 风格终端交互 + 多 Provider（Copilot/Bedrock/llama.cpp/Cloudflare）聚合；批量关闭积压 Issue 显示维护纪律严格 |
| **LiteLLM** | AI 网关/代理基础设施（Proxy Layer） | 平台工程团队、企业 AI 基础设施管理者 | 高吞吐请求路由 + 预算/限流/计费 + 多 Provider 适配；201 条 PR/日，迭代速度生态第一 |
| **Temporal** | 分布式工作流编排（Agent 基础设施底座） | 构建复杂 Agent 工作流的后端工程师 | 持久化执行 + 故障恢复 + 复制/重试基础设施；本期无用户侧新功能，专注资源治理与 CGS Foundation 复制改进 |

**关键区分**：LiteLLM 管"模型接入与钱"，Temporal 管"流程可靠执行"，Pi 管"终端人机交互"，OpenHands 管"Agent 能力嵌入"，OpenClaw 管"智能体互操作标准"。

---

## 6. 社区热度与成熟度

**🟢 第一梯队：快速迭代期（功能扩张与标准卡位）**
- **LiteLLM**：PR 更新 201 条/日，49 条合并，发布 v1.96.0 安全增强版。处于"功能吞吐"峰值，但 Issue 积压与 Bug 拖期（预算绕过 3.5 个月未修）提示需警惕质量债。
- **Pi**：Issue 日更新 138 条，但关闭 110 条（关闭率 80%），维护节奏"高进高出"。自动压缩失效（#6879，3 周无 fix）与 WSL 登录挂起（#6187，40+ 天开放）是其主要短板。

**🟢 第二梯队：质量巩固期（深度治理与架构前瞻）**
- **Temporal**：Issue 量少（4 条）但 PR 流水线密集（31 条，23 条待合并），集中在资源泄漏、复制可靠性、CHASM 加固——典型的基础设施成熟期特征。
- **OpenHands SDK**：Issue/PR 均衡（14/31），以稳定修复（GC wedge）+ 架构重构（PluginFormat 策略化）双线推进，方向明确但合并管线积压 21 条，需要关注交付节奏。

**⚪ 第三梯队：数据缺失**
- **OpenClaw、Hermes Agent**：本期无动态，无法判定热度。建议补充追踪源后再评估。

---

## 7. 值得关注的趋势信号

1. **智能体可移植性标准化进入落地前夜**：agent-plugins.org 从"规范讨论"进入"设计拆解"（OpenHands #4450-#4453），且 Pi 社区同步提出兼容诉求——**跨智能体插件标准即将迎来首个实现浪潮**。对开发者：现在为插件编写 plugin.json 清单，未来可同时触达多个智能体生态，建议尽早布局。

2. **AI 网关的"计费准确性"成为企业采用硬门槛**：LiteLLM 流式 usage 少计（#36114）、SpendLogs end_user 固定错误（#31441）、预算绕过（#26672）三个问题叠加，表明**企业级落地对资金可审计性的敏感度远超想象**。若你的 Agent 产品有付费场景，gateway 层的 usage 聚合准确性应作为 P0 级技术债处理。

3. **MCP 生态进入"韧性"阶段**：OpenHands #4454（MCP 故障应降级而非中断）不是孤例——Pi 对 Bedrock 空 key 的防御性清洗、Temporal 对重试抖动的修复，共同指向**外部依赖的异常数据与故障行为正在成为主

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目日报 — 2026-08-11

## 1. 今日速览

项目整体活跃度**高**：过去24小时产生 14 条 Issue 更新和 31 条 PR 更新（其中 10 条已合并/关闭），且核心维护者与外部贡献者并行推进多条功能线。**最具信号意义的事件是 Agent Plugins（#4405）从规范讨论进入落地设计阶段**——昨日（8/10）一口气新增了 4 个分解子 Issue（#4450-#4453），说明该项目未来数周可能进入实现周期。稳定性方面，高优先级 GC 阻塞问题（#4416）已被 PR #4417 修复并关闭，另有 2 个中优先级 Bug（#4382、#4443）已分别有对应 fix PR（#4444、#4445）在审。值得关注的是，**暂无新版本发布**，且待合并 PR 达 21 条，合并管线存在一定积压。LLM 路由元数据、MCP 容错、插件安全边界是当前社区讨论最集中的方向。

---

## 2. 版本发布

今日无新版本发布。上一次发布可能早于 8/10（#4443 中提及 PyInstaller bundle 属于 1.41.0，当前正在修复其打包遗漏问题）。

---

## 3. 项目进展

今日关闭的 PR 主要贡献在稳定性修复、插件架构重构、可观测性与文档四个方面：

| PR | 状态 | 关联 Issue | 意义 |
|---|---|---|---|
| [#4417](https://github.com/OpenHands/software-agent-sdk/pull/4417) fix(agent-server): compose ConversationInfo off the event loop | **已合并** | 修复 #4416 | 根除了 `GET /api/conversations/search` 引发的周期性 GC 全停（"wedge"）问题，将大对象组合移出 asyncio 事件循环线程。这是近期最影响用户体验的高危稳定性修复 |
| [#4420](https://github.com/OpenHands/software-agent-sdk/pull/4420) refactor(plugin): extract PluginFormat strategy | **已合并** | 为 #4405 铺路 | 将插件处理逻辑抽取为策略模式，为支持 Agent Plugins 多格式生态做架构准备。后续可直接添加策略类来支持新格式 |
| [#4425](https://github.com/OpenHands/software-agent-sdk/pull/4425) feat(telemetry): identify local automation conversations | **已合并** | — | 遥测数据将可区分自动化创建的会话与本地 Agent Canvas 会话，同时保持总会话数统计不变，利于运营分析 |
| [#4449](https://github.com/OpenHands/software-agent-sdk/pull/4449) docs: refresh AGENTS.md guidance | **已合并** | — | 更新了 AGENTS.md 指导文档，降低贡献者参与门槛 |

**整体评价**：项目今日在"稳定性"和"架构前瞻"两个维度上都有实质推进。GC wedge 修复是本日最重要的健康度提升；PluginFormat 策略化重构则展示了项目在为 Agent Plugins 生态做准备时的架构纪律。

---

## 4. 社区热点

今日讨论最活跃的 Issues/PRs：

- **[#2935 [Refactor] Introduce deep_copy() and replace() methods for Agent and LLM](https://github.com/OpenHands/software-agent-sdk/issues/2935)** — 6 条评论（4月创建，今日仍有更新）
  - 诉求：目前 Agent/LLM 拷贝与更新散落各处，使用 Pydantic 原生产品（`model_copy`、`model_dump`/`model_validate`）导致模式不一致。社区希望引入统一的 `deep_copy()` 和 `replace()` 方法。这是对代码可维护性的长期诉求，值得维护层关注。

- **[#3746 max_input_tokens in agent_settings.json does not take effect](https://github.com/OpenHands/software-agent-sdk/issues/3746)** — 5 条评论（已关闭）
  - 诉求：用户在 headless CLI 模式下配置 `llm.max_input_tokens` 不生效。这是配置生效链路的问题，关闭原因未明示，但用户侧反馈强烈。

- **[#4405 Spec: Support the Agent Plugins portable package format](https://github.com/OpenHands/software-agent-sdk/issues/4405)** — 4 条评论
  - 诉求：支持 [agent-plugins.org](https://agent-plugins.org)（v1.0.0 Working Draft）开放标准。该标准 TSC 成员来自 Amazon、Cursor、Microsoft 等，社区对此跨厂商标准在本项目落地呼声较高。昨日新增的 4 个子 Issue 表明维护者正在将其拆解并进入设计阶段。

- **[#4454 MCP server connection failure at startup aborts the whole conversation](https://github.com/OpenHands/software-agent-sdk/issues/4454)** — 2 条评论（新开）
  - 诉求：单个 MCP server 不可达即导致整个会话 500 失败，用户明确要求**降级而非中断**。这反映了 MCP 生态下的高可用性预期。

更多评论数可见于 #3524（3 条）、#4382（2 条）和 #3804（2 条）。

---

## 5. Bug 与稳定性

按严重程度排列：

### 🔴 高危
- **[#4416 agent-server: periodic multi-second GC pauses during conversation search](https://github.com/OpenHands/software-agent-sdk/issues/4416)** — **已关闭**
  - 影响：`GET /api/conversations/search` 在事件循环上同步构建复杂 Pydantic 对象，导致每请求数秒级全阻塞，表现为"整个服务卡死直至重启"。
  - 修复：✅ 已由 [#4417](https://github.com/OpenHands/software-agent-sdk/pull/4417) 合并修复。

### 🟡 中危
- **[#4454 MCP server connection failure aborts conversation with 500](https://github.com/OpenHands/software-agent-sdk/issues/4454)** — 新开，无 fix PR
  - 影响：MCP server 不可达时整个会话创建失败，用户期望降级为"不带该工具继续运行"。
  - 状态：⚠️ 待认领。

- **[#4382 ACP derived cost ignores cache/thought buckets, zeroes unknown models](https://github.com/OpenHands/software-agent-sdk/issues/4382)** — 待合并 PR [#4444](https://github.com/OpenHands/software-agent-sdk/pull/4444)
  - 影响：ACP 会话计费缺失缓存/思考 token 定价；未知模型成本被静默清零；`UsageUpdate.cost` 停更时派生成本会持续累加。
  - 状态：✅ fix PR 已提交（#4444），待评审。

- **[#4443 agent-server 1.41.0 PyInstaller bundle omits browser_use/js (rrweb recording)](https://github.com/OpenHands/software-agent-sdk/issues/4443)** — 待合并 PR [#4445](https://github.com/OpenHands/software-agent-sdk/pull/4445)
  - 影响：冻结打包的 agent-server 执行浏览器录制时报 `wait-for-rrweb.js` 文件缺失。
  - 状态：✅ fix PR 已提交（#4445），待评审。

### 🟢 低位
- **[#3746 max_input_tokens in agent_settings.json does not take effect in headless CLI mode](https://github.com/OpenHands/software-agent-sdk/issues/3746)** — 已关闭（关闭原因未注明）

---

## 6. 功能请求与路线图信号

### 强信号（已有对应 PR 或在设计阶段）

- **Agent Plugins 标准化支持**（[#4405](https://github.com/OpenHands/software-agent-sdk/issues/4405)）
  - 8/10 新增 4 个分解子 Issue，表明进入设计/实现阶段：
    - [#4450](https://github.com/OpenHands/software-agent-sdk/issues/4450) manifest loader（plugin.json 闭合 schema）
    - [#4451](https://github.com/OpenHands/software-agent-sdk/issues/4451) mcp.json loader + PLUGIN_ROOT/PLUGIN_DATA 展开
    - [#4452](https://github.com/OpenHands/software-agent-sdk/issues/4452) 客户端扩展命名空间映射（`io.openhands` vs `dev.openhands` 待定）
    - [#4453](https://github.com/OpenHands/software-agent-sdk/issues/4453) 路径包含强制 + 窄失败边界（安全层）
  - 同时 [#4420](https://github.com/OpenHands/software-agent-sdk/pull/4420) 已合并的策略模式重构为其铺路。

- **路由模型运行时元数据解析**（[#4421](

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-11

## 1. 今日速览

过去24小时项目整体活跃度处于**高位**。Issues 更新 138 条，其中新开/活跃 28 条，关闭 110 条，关闭数远高于新开数，说明维护团队在批量处理积压问题上投入了大量精力；PR 更新 19 条，其中 9 条待合并、10 条已合并/关闭，代码推进节奏正常。值得注意的是，本期有大量标记为 `[no-action]` 的 issue 被直接关闭（如 #7855、#7850、#7886、#7876 等），表明维护者正在快速筛选并论断非问题报告，这有助于控制 issue 积压规模，但也需留意是否存在误关风险。版本发布方面今日无新 Release。

- **Issue 关闭率**：110/138 ≈ 80%，维护响应高效
- **PR 合并率**：10/19 ≈ 53%，接近半数 PR 今日已落地
- **高热度 issue**：Windows 使用问题收集帖（24 评论）、WSL 登录挂起（21 评论）、自动压缩失效（16 评论、16 👍）

---

## 2. 版本发布

**无新版本发布。**

上一次版本为 0.84.1（仍有用户报告该版本存在问题，见下文 Bug 与稳定性章节）。预计下一版本将包含今日合并/关闭的多项修复和新功能。

---

## 3. 项目进展

今日合并/关闭的 PR 中，有几个值得关注的实质推进：

**会话与上下文**

- [#7872 feat(coding-agent): expose context files at session start](https://github.com/earendil-works/pi/pull/7872)：`session_start` 事件现在会携带加载的 AGENTS/CLAUDE 上下文文件列表，帮助扩展开发者理解会话的上下文来源。已关闭。
- [#7881 fix(ai): reject item_* content IDs in message-level input[].id fields](https://github.com/earendil-works/pi/pull/7881)：修复 Responses API 中 `item_*` 与 `msg_*` 两个 ID 命名空间的混用问题，避免流式响应 ID 污染消息历史。已关闭。

**工具调用可靠性**

- [#7882 fix(ai): sanitize empty Bedrock tool argument keys](https://github.com/earendil-works/pi/pull/7882)：修复 Bedrock 生成的包含空 key（`""`）的工具调用导致整个 session 不可用的问题。修复方式为在重放时递归移除空属性名，但不修改已持久化的会话数据。关闭 #7782。已关闭。
- [#7904 fix(edit): normalize single-object edits argument to array](https://github.com/earendil-works/pi/pull/7904)：让 `edit` 工具兼容模型以单个对象而非数组形式传入 `edits` 参数的情况，降低对模型输出格式的敏感度。已关闭。

**交互与终端体验**

- [#7879 Make the interactive footer responsive in narrow panes](https://github.com/earendil-works/pi/pull/7879)：让 TUI 底部状态栏在窄窗口下优先保留上下文窗口信息，将次要的用量统计折行展示。已关闭。
- [#7887 fix: add trailing newline after current working directory](https://github.com/earendil-works/pi/pull/7887)：修复系统提示词中当前工作目录后缺少换行，导致首条用户消息与目录拼接在一起的问题。已关闭。
- [#7873 skip global aliases](https://github.com/earendil-works/pi/pull/7873)：bash 工具调用时跳过 `alias -g` 全局别名（如 `G='| grep'`），避免命令解析出错。已关闭。

**其他**

- [#7905 fix(config): refine pnpm detection...](https://github.com/earendil-works/pi/pull/7905)：优化包管理器检测逻辑，避免将 `$PNPM_HOME` 下非 pnpm 实际管理的包误判为 pnpm 安装。已关闭。
- [#7906 feat(coding-agent): add fullscreen fixed top bar](https://github.com/earendil-works/pi/pull/7906)：新增全屏模式固定顶栏，左侧显示缩写 cwd 和 git 分支，右侧显示上下文用量和自动压缩状态。已关闭。
- [#7877 feat(subagent): add Muse Spark via Muse Code](https://github.com/earendil-works/pi/pull/7877)：新增 Meta/Muse Code 作为 subagent 的备选运行时，支持目录驱动发现和显式路由。已关闭。

**待合并 PR（摘要）**

- [#7913 feat(tui): add fullscreen transcript search](https://github.com/earendil-works/pi/pull/7913)：全屏模式下的会话内容搜索（`Ctrl+Shift+f`）
- [#7910 feat(coding-agent): add canonical message identity to markdown transformer context](https://github.com/earendil-works/pi/pull/7910)：为 markdown transformer 增加消息级身份信息，关闭 #7828
- [#7903 feat(tui): add unbound single-line transcript scrolling actions](https://github.com/earendil-works/pi/pull/7903)：新增单行滚动操作（默认未绑定按键），关闭 #7830
- [#7901 feat(ai): AI Gateway transport over Cloudflare AI binding](https://github.com/earendil-works/pi/pull/7901)：新增 Cloudflare Workers AI Gateway 传输层支持，对应 #7838
- [#7899 fix(tui): prevent split Alt+Enter from interrupting](https://github.com/earendil-works/pi/pull/7899)：修复 Alt+Enter 被拆分为 ESC+CR 导致误触发中断的问题，对应 #7876

整体来看，项目今日在**AI 网关接入、TUI 交互细节、工具调用健壮性、subagent 生态**四个方向均有实质推进。

---

## 4. 社区热点

### 🔥 [#7547 [Windows] How do you use Pi on windows? What issues are you seeing?](https://github.com/earendil-works/pi/issues/7547) — 24 条评论

由维护者 @petrroll 发起的 Windows 使用情况收集帖。核心诉求是摸清 Windows 用户基数与痛点分布——Pi 在 Windows 上的运行方式过于碎片化（WSL、原生、Cygwin 等），团队难以确定该把精力投向何处。这是项目方面向社区的一次**主动调研**，建议关注该帖结论对 Windows 支持路线图的影响。

### 🔥 [#6187 Pi login hangs in WSL after browser-based GitHub Copilot device authorization](https://github.com/earendil-works/pi/issues/6187) — 21 条评论

WSL 环境下完成 GitHub Copilot 设备授权后，Pi 客户端无法感知授权完成而一直挂起。WSL 是 Windows 用户使用 Pi 的主要途径之一，这个问题影响面不小。目前已开放超过 40 天，仍无修复 PR，值得关注。

### 🔥 [#6879 auto-compaction never triggers after context grows past 100% until provider overflow](https://github.com/earendil-works/pi/issues/6879) — 16 条评论，16 👍

自动压缩机制的核心缺陷：上下文超过阈值后不会触发压缩，直到 API 在 373k tokens 处拒绝请求才介入。这个 issue 获得 16 个 👍，侧面反映不少用户遭遇过同样问题。issue 创建于 7 月 20 日，已超 3 周未见 fix PR，是最受社区关注的技术债之一。

### 🔥 [#6922 Default model cannot be a llama.cpp model: startup shows "No models available"](https://github.com/earendil-works/pi/issues/6922) — 10 条评论，14 👍

当 `defaultProvider` 设为 `"llama.cpp"` 时，Pi 启动报 "No models available" 并退出。该 issue 已关闭，但 14 个 👍 说明本地模型用户对 llama.cpp 支持有较高期待，需要确认修复是否在下个版本中生效。

---

## 5. Bug 与稳定性

按严重程度排列：

### 严重（核心功能受损或会话数据丢失）

| Issue | 描述 | 状态 | Fix PR |
|---|---|---|---|
| [#6879](https://github.com/earendil-works/pi/issues/6879) | 自动压缩在上下文超过 100% 后不触发，直到 API 拒绝请求（373k tokens 才被动介入） | OPEN | 无 |
| [#6187](https://github.com/earendil-works/pi/issues/6187) | WSL 中 Copilot 设备授权完成后 Pi 登录挂起 | OPEN | 无 |
| [#7730](https://github.com/earendil-works/pi/issues/7730) | Mac OS 长时间会话 CPU 占用 50-110%，内存 600-800MB | OPEN | 无 |

### 中等（功能异常/损坏但可绕行）

| Issue | 描述 | 状态 | Fix PR |
|---|---|---|---|
| [#7782](https://github.com/earendil-works/pi/issues/7782) | Bedrock 返回含空 key 的工具调用，Pi 持久化后每轮重放导致会话永久失效 | CLOSED | ✅ [#7882](https://github.com/earendil-works/pi/pull/7882) 已合并 |
| [#7876](https://github.com/earendil-works/pi/issues/7876) | Alt+Enter 在 10ms ESC 超时下被拆分为 ESC+CR，表现为间歇性中断正在运行的任务 | CLOSED | ✅ [#7899](https://github.com/earendil-works/pi/pull/7899) 待合并 |
| [#7855](https://github.com/earendil-works/pi/issues/7855) | "Response was truncated before completion" 随机出现，需手动提示继续 | CLOSED (no-action) | 无 |
| [#7850](https://github.com/earendil-works/pi/issues/7850) | Copilot 登录在组织有 20+ 模型时因 429 限流失败 | CLOSED (no-action) | 无 |
| [#7771](https://github.com/earendil-works/pi/issues/7771) | 0.84.1 无法启动：`zlib.createZstdDecompress is not a function`（Node 23） | CLOSED (no-action) | 无 |

### 低（体验问题）

| Issue | 描述 | 状态 | Fix PR |
|---|---|---|---|
| [#7806](https://github.com/earendil-works/pi/issues/7806) | macOS 终端流式输出时使用滚轮查看历史，会被自动拉回顶部 | CLOSED (no-action) | 无 |
| [#7832](https://github.com/earendil-works/pi/issues/7832) | Mermaid 流程图含 `:::className` 语法时渲染失败 | CLOSED (no-action) | 无 |

**值得警惕的信号**：今日有 7 个 bug 类 issue 被标记为 `[no-action]` 直接关闭，包括 #7855（响应随机截断）和 #7771（无法启动）这类看起来影响较大的问题。虽然 `no-action` 可能意味着维护者定位到用户侧原因（如 Node 版本、配置问题），但建议关注关闭评论中的具体说明，避免真实 bug 被误判。

**稳定性趋势判断**：工具参数校验（#7882）、TTY 输入时序（#7899）、ID 命名空间隔离（#7881）这三类修复表明，**Pi 当前的主要稳定性风险集中在 AI 提供方返回的异常数据和大户环境下的输入竞争条件**上。

---

## 6. 功能请求与路线图信号

### 已进入 PR 阶段（大概率纳入下一版本）

| 功能需求 | Issue | PR | 信号 |
|---|---|---|---|
| 全屏模式下会话内容搜索 | —（直接提交 PR） | [#7913](https://github.com/earendil-works/pi/pull/7913) | 由 @mitsuhiko（核心维护者）提交，**落地概率极高** |
| Cloudflare Workers AI Gateway 传输层 | [#7838](https://github.com/earendil-works/pi/issues/7838) | [#7901](https://github.com/earendil-works/pi/pull/7901) | 满足在 Cloudflare Worker 内运行 Pi 的应用场景 |
| Markdown transformer 增加消息身份（messageId/timestamp） | [#7828](https://github.com/earendil-works/pi/issues/7828) | [#7910](https://github.com/earendil-works/pi/pull/7910) | 扩展开发者按消息维度装饰内容的前置能力 |
| 全屏 TUI 单行滚动 | [#7830](https://github.com/earendil-works/pi/issues/7830) | [#7903](https://github.com/earendil-works/pi/pull/7903) | 细化长输出阅读体验 |

### 需求明确但尚未进入实施

- [#7776 Agent Plugins 规范支持](https://github.com/earendil-works/pi/issues/7776)：让 Pi 原生识别 agent-plugins.org 的 plugin.json 清单，与 Codex 等跨 agent 共享插件。已关闭（no-action），但属生态位布局型需求，值得持续关注。
- [#7802 可选的 sticky header 显示最后发送的 prompt](https://github.com/earendil-works/pi/issues/7802)：TUI 会话长时快速回顾当前任务的轻量增强。已关闭。
- [#7444 WebSocket 重试仅处理两种错误码](https://

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-11

## 1. 今日速览

过去24小时项目活跃度极高：Issues 侧共64条更新（新开/活跃56条、关闭8条），PR 侧达到201条更新（待合并152条、已合并/关闭49条），并发布了 v1.96.0 安全增强版本。当前 PR 合并速度（49条/日）显著高于 Issue 关闭速度（8条/日），说明维护团队正在集中处理功能开发与代码合入，但 Issue 积压仍面临一定压力。社区讨论焦点集中在预算执行可靠性、OpenWebUI 集成、PII 脱敏配置，以及多副本部署下的告警重复等长期痛点；同时有多项性能优化（Rate Limiter Redis 写入、SpendLogs 批量更新）正处于活跃开发中。整体项目健康度良好，但部分资金/安全相关的 Bug 已存在较长时间，建议优先关注。

---

## 2. 版本发布

### v1.96.0 — Docker 镜像签名验证增强

**发布内容：** 该版本的核心变更为所有 LiteLLM Docker 镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 进行签名，且所有 release 使用相同的签名密钥（引入于 [commit `0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0)），提供了镜像完整性验证能力。

**影响与迁移注意事项：**
- 对使用官方 Docker 镜像的用户，建议在 CI/CD 流水线中增加 cosign 签名验证步骤，确保部署的镜像未被篡改；
- 尚不确定 v1.96.0 是否包含其他功能性变更，建议查看完整 [Release Notes](https://github.com/BerriAI/litellm/releases) 以确认升级范围；
- 对于从旧版本升级的用户，此安全增强无破坏性变更，但若您的环境使用私有化镜像仓库镜像同步，需确保同步工具兼容 cosign 签名元数据。

---

## 3. 项目进展

今日共有 49 条 PR 被合并或关闭，以下为其中最值得关注的功能推进：

### 3.1 向量存储（Vector Store）管理闭环
- **[PR #36289]** 新增 `GET /v1/indexes` 管理端点，用于列出所有已注册的虚拟索引（已关闭/合并）。解决了 `POST /v1/indexes` 创建索引后无法查看的问题，并修复了两个 lazy OpenAPI snapshot 生成器缺陷。
- **[PR #36306]** 在 Admin UI 的 Vector Stores 页面新增代理管理员专属的 Indexes 标签页（已关闭/合并），显示索引名称、后端向量库、Provider 索引及创建时间。以上两个 PR 形成了向量索引从创建到可视化的完整管理闭环。

### 3.2 OpenRouter 价格数据库大范围修正
- **[PR #34986]** 同步了过期/错误的 `openrouter/*` 模型定价（已关闭/合并）。修复了部分模型计费偏差高达 30 倍的问题，例如 `openrouter/mistralai/mistral-large` 原计费 $8/$24 修正为实际 $2/$6；`openrouter/gryphe/mythomax-l2-13b` 原 $1.875 修正为 $0.06；同时为 31 个支持搜索的模型补全了 web-search 定价。

### 3.3 Router 冷却策略差异化
- **[PR #31876]** 为 Router 增加 per-deployment `allowed_fails_policy` 配置，使不同可靠性的部署（如实验模型 vs 生产模型）可以设置独立的失败容忍阈值（已关闭）。同时修正了 DualCache TTL 计算问题。该改动提升了多模型路由场景下的灵活性和稳定性。

### 3.4 测试基础设施迁移
- **[PR #36465]**（开放中）将 compat-matrix 定时发布任务从旧的 `tests/claude_code` 套件迁移到 `tests/e2e/claude_code`，以覆盖 GPT 列测试，属于测试基建的长期改进。

---

## 4. 社区热点

### 4.1 Budget 执行绕过问题 — 讨论最激烈
- **[Issue #26672]**「Budget enforcement bypassed in v1.82.3」（15条评论，4👍）仍处于打开状态。用户反馈在 v1.82.3 上 key/user 的 `max_budget` 完全不生效，即使 spend 已超限仍可继续调用。该 Issue 自 2026-04-28 创建以来已持续 3.5 个月，且被标记为 `bug` 和 `proxy` 标签，反映了社区对计费核心功能稳定性的高度关注。

### 4.2 OpenWebUI 集成文档与实现不一致
- **[Issue #14667]**「user_header_mappings does not work with OpenWebUI」（12条评论，1👍）。创建于 2025-09-18，距今已近一年。用户根据官方文档配置 `x-openwebui-user-email` 和 `x-openwebui-user-id` 追踪用量失败，最终发现是 LiteLLM 未正确读取该 header。该问题长期存在，已标记 `stale`，但社区仍在持续顶帖。

### 4.3 PII 脱敏配置无效
- **[Issue #14516]**「Setting output_parse_pii has no effect」（11条评论，2👍）。创建于 2025-09-12，同样接近一年。用户尝试通过 UI、config.yml 和请求体三种方式设置 `output_parse_pii: True`（配 Presidio），响应仍然被脱敏，说明配置完全未生效。

### 4.4 Rate Limiter 性能优化提案
- **[Issue #31880]**「skip post-call Redis writes for keys with no rate limits configured」（10条评论）。由核心贡献者 @deepanshululla 提出：当前每次 LLM 调用后即使 key/user/team 未配置任何速率限制，也会无条件向 Redis 写入计数器，属于无效写入。该 Issue 直接导向 PR，社区关注度高（6👍），体现了用户对高吞吐场景下性能浪费的认可。

---

## 5. Bug 与稳定性

按严重程度排列（低 → 高）：

### 🟡 中等级 — 功能异常/兼容性

- **[#36366]** Azure Responses 转发空 namespace 描述：`additional_tools` 未规范化嵌套 namespace 工具，Codex CLI 0.147.0 默认配置会触发该问题（2026-08-09 创建，仍有待修复）。
- **[#32218]** Z.AI Coding Plan 文档中 `glm-5.2[1m]` 变体在 LiteLLM Proxy 请求时返回 `Unknown Model`，但 `glm-5.2` 正常（6条评论）。
- **[#25748]** Vertex AI Anthropic 流式请求在提供自定义 `api_base` 时返回 404（已被标记 `stale`，但更新日期为 2026-08-10，表明仍有关注）。

### 🟠 高等级 — 数据准确性/并发正确性

- **[#36114]** 流式 usage 严重少计（provider-independent）：在链式代理（Front-Proxy → Upstream-Proxy → Bedrock）场景下，流式响应的最终 usage 远低于非流式请求。作者指出根因在流聚合层而非 provider 转换（2026-08-06 创建，已有6条评论）。
- **[#31441]** `end_user` 在 SpendLogs 中被固定为第一个请求的 `user`：共享虚拟 key 上的后续请求即使携带不同的 `user` 字段，`end_user` 列仍然不变（v1.87.0 回归）。
- **[#27955]** `max_parallel_requests` 计数器在流式中途取消时单调递增（Redis），最终导致所有请求被拒绝（Anthropic `/v1/messages` 路径）。

### 🔴 严重级 — 资金/安全

- **[#26672]** 预算执行绕过（v1.82.3）：key/user `max_budget` 完全不生效，存在资金超支风险。无 fix PR 关联，且已持续 3.5 个月。
- **[#35664]** UI Cookie JWT 包含可重用的 API key 材料（`key` claim），复制后可在其他浏览器/会话中冒充身份，属于凭据泄露风险（v1.94.0，2026-08-03 报告）。
- **[#35665]** 登出/修改密码不撤销已签发的 UI 会话，已泄露的会话凭据可持续使用（v1.94.0）。

---

## 6. 功能请求与路线图信号

### 6.1 性能与可扩展性优化（有明确 PR 支撑）
- **Rate Limiter 后置写入跳过**（[#31880](https://github.com/BerriAI/litellm/issues/31880)）：为未配置速率限制的 key 跳过 Redis 计数器写入，减少无效 I/O。
- **Spend 更新可配置化**（[#31866](https://github.com/BerriAI/litellm/issues/31866)）：新增 `disable_entity_spend_updates` 标志，在高请求量场景下保留 SpendLogs 原始记录但跳过实体计数器的 UPDATE 操作。
- **Tag 维度速率限制**（[PR #36459](https://github.com/BerriAI/litellm/pull/36459)，开放中）：按 tag 进行 token/request/dollar/concurrency 多维度限流，支持滚动窗口，弥补当前仅支持按调度重置的 tag 美元预算的不足。

### 6.2 细粒度控制增强
- **Per-Key Prompt Caching 开关**（[PR #36466](https://github.com/BerriAI/litellm/pull/36466)，开放中）：新增 `enable_prompt_caching` 字段，允许管理员为单个虚拟 key 开启或关闭缓存注入，替代当前 gateway 全量开关的粗暴模式。
- **Router per-deployment 失败策略**（[#31876](https://github.com/BerriAI/litellm/issues/31876)）：已合并，允许按部署独立配置 `allowed_fails`。

### 6.3 可观测性与生命周期管理
- **模型 deprecation_date 补全**（[PR #36080](https://github.com/BerriAI/litellm/pull/36080)，开放中）：为 65 个模型补充 Azure/Vertex/Gemini/xAI 的退役日期元数据，此前 `text-embedding-004` 误用了 Gemini API 日期而非 Vertex 的。
- **Healthcheck 日志开关**（[#17235](https://github.com/BerriAI/litellm/issues/17235)，5条评论，6👍）：用户希望有独立 flag 关闭健康检查日志，仅保留错误日志，以降低日志量。

### 6.4 SDK 健壮性
- **[#27581](https://github.com/BerriAI/litellm/issues/27581)**：请求 `cost_per_token()`/`completion_cost

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 开源项目动态日报
**日期：2026-08-11**

---

## 今日速览

过去24小时内，Temporal 项目保持高度活跃：共产生 4 条 Issue 更新（2 新开/活跃、2 关闭）和 31 条 PR 更新（23 待合并、8 已合并/关闭）。今日的核心主题围绕 **资源泄漏系统性修复** 展开——多起连接泄漏、对象泄漏问题已有对应修复并完成合并。此外，复制任务改进、CHASM 组件加固、Worker 回调新功能等多个方向均有 PR 在推进中，但多数仍处于待合并状态，尚未形成大规模合入浪潮。项目整体健康度良好，维护者对可靠性类问题响应积极，尤其体现在新的 SDK 客户端关闭泄漏 Issue（#11460）在当天即获得了关联修复 PR（#11438）的跟进。

---

## 版本发布

今日无新版本发布。

---

## 项目进展

今日共 8 个 PR 完成合并/关闭，主要为 **资源生命周期管理** 的可靠性修复和测试基础设施改进。值得关注的是，这些合并的 PR 围绕同一主题形成合力——**系统性消除集群关闭时的对象与连接泄漏**，这意味着项目正经历一轮深度的资源管理治理。

### 重点合并/关闭 PR

1. **减少集群关闭对象泄漏**（#11310，merged）— @stephanos
   - **内容**：释放测试集群关闭后的引用、将认证回调状态与已停止的服务器图分离、移除宽泛的主机级泄漏豁免，并将测试基座的宽泛豁免替换为有文档记录的进程生命周期路径。
   - **意义**：此项为 goleak 测试框架的精确化铺平道路，使未来资源泄漏检测更精准。合并 #11310 之后，#11296、#11437、#11438 等修复才能安全落地。

2. **缓存本地/远程 frontend gRPC 连接**（#11296，merged）— @RajeshRajendiran
   - **内容**：`RPCFactory` 的 `CreateLocalFrontendGRPCConnection` 和 `CreateRemoteFrontendGRPCConnection` 改为缓存 `grpc.ClientConn` 而非每次调用新建。本地连接通过 `sync.OnceValue` 记忆化。
   - **意义**：**直接修复 #11289**（Frontend/Admin 的 SearchAttributes 和 AddOrUpdateRemoteCluster 处理器每次调用泄漏一个 gRPC 连接的问题），消除了未绑定的 goroutine 和内存增长源头。

3. **关闭版本检查响应的所有路径**（#11437，merged）— @prathyushpv
   - **内容**：`versioninfo.Caller.Call` 中的 `defer` 原本位于状态检查之下，非 200 响应会带着未关闭的 body 返回。修复后将 body 关闭移到所有返回路径上。
   - **意义**：测试中报告的 2 个 goroutine 泄漏即由此产生，现已解决。

4. **为混合脑开发服务器启用独立活动**（#11457，merged）— @fretz12
   - **内容**：在混合脑测试的 release server 上启用 `activity.enableStandalone` 动态配置。
   - **原因**：`throughput_stress` 在 namespace 报告支持时会自动启用独立活动负载；当前测试服务器（1.32）默认开启该功能，导致测试与服务器行为不一致。

> **整体评价**：今日合并的 PR 虽然数量不多，但共同完成了 **集群关闭路径上资源泄漏问题的系统性收敛**。与此配套的 #11438（RPCFactory 持有并关闭 gRPC 连接）、#11436（停止 SDK workers/clients）已在待合并队列中，预计近期将进一步巩固这一主题的成果。

---

## 社区热点

今日讨论最活跃的 Issue 集中在 **大规模生产环境下的存储与可观测性问题**，背后反映了用户对运行稳定性和运维成本的诉求。

1. **PostgreSQL 高吞吐量下索引膨胀问题**（#10145，Closed，7 条评论，👍 2）
   - 作者 @oznu 报告：在每小时数十万工作流的高负载下，PostgreSQL 数据库大小持续增加，不受保留期设置约束——表本身仅 46 左右规模，但数据库整体持续膨胀。
   - 该 Issue 虽已关闭，但 7 条评论表明社区对存储效率问题有较高关注。数据大小与保留期设置不匹配的问题可能指向索引清理或 vacuum 策略的深层次问题。

2. **Matching 服务 Prometheus 指标基数无界增长**（#9945，Open，3 条评论）
   - @Sanil2108 指出 `PhysicalTaskQueueManager` 卸载或 task queue 空闲后，matching 服务的 Prometheus 指标基数 **不会随之回收**，长期运行可能导致监控数据量失控。
   - 该 Issue 自 2026-04-14 创建至今已近 4 个月未关闭，是长期受关注但尚未解决的稳定性问题。

3. **新 Issue：SDK 客户端在集群关闭时未正确关闭**（#11460，Open，0 评论）
   - @prathyushpv 报告：`sdk.clientFactory.Close` 会在关闭共享系统客户端前释放由 `NewClient` 派生的客户端。由于 SDK 只有在每个派生客户端都关闭后才关闭底层 gRPC 连接，导致系统客户端被提前释放。作者在当天内即提交了修复 PR #11438，响应速度非常快。

**分析**：社区热点集中在 **连接/资源泄漏** 和 **高负载下的稳定性** 两个维度。值得肯定的是，Temporal 团队对当天报告的泄漏问题即出现关联修复 PR（#11460 → #11438），响应迅速；但长期存在的指标基数问题（#9945）仍待专项解决。

---

## Bug 与稳定性

今日 Bug 报告按严重程度排序如下：

### 高严重度

1. **SDK 客户端与底层 gRPC 连接在集群关闭时释放顺序错误**（#11460 — OPEN）
   - **影响**：集群关闭路径上，派生 SDK 客户端可能带着未关闭的 gRPC 连接被释放，影响正常集群关闭的干净性。
   - **修复状态**：✅ 已有修复 PR #11438（RPCFactory 持有并关闭 gRPC 连接；SDK 客户端工厂关闭其管理的客户端），待合并。
   - **关联 PR**：#11436 也涉及停止 SDK workers/clients，形成互补。

2. **Frontend/Admin RPC 处理器每次调用泄漏未缓存的 `grpc.ClientConn`**（#11289 — CLOSED）
   - **影响**：反复调用 `{Add,Remove,List/Get}SearchAttributes` 或 `AddOrUpdateRemoteCluster` 会导致 goroutine 和内存无界增长。
   - **状态**：✅ 已由 PR #11296 修复并合并，作为今日新增的已修复项。

### 中严重度

3. **复制流发送器遇到不可构建任务时阻塞流**（#11422 — PR OPEN）
   - **影响**：当复制流发送器无法构建（转换）任务时，重试预算耗尽后会将整个流阻塞。
   - **修复**：建议跳过不可构建任务并记录日志，新增 `ReplicationTaskSendSkipped` 指标。待合并。

4. **重试抖动逻辑被截断为无效操作**（#11397 — PR OPEN）
   - **影响**：`addJitter` 函数始终未生效——2 秒基础延迟配合 `WithJitter(0.1)` 时，所有延迟精确返回 2.000 秒，而非预期的 `[2.0s, 2.2s)` 区间。
   - **修复**：已重写为正确的随机抖动计算，避免重试风暴效应。待合并。

### 低严重度

5. **PostgreSQL 索引膨胀（高吞吐场景）**（#10145 — CLOSED）
   - 虽已关闭，但 root cause 是否解决未从今日数据中确认，建议关注关闭原因。

6. **Matching 服务 Prometheus 指标基数无界增长**（#9945 — OPEN）
   - 已有讨论但长期未解决，当前无对应修复 PR。

---

## 功能请求与路线图信号

今日没有新的用户侧功能请求，但多个待合并 PR 透露出明确的路线图方向：

### 1. Worker 回调变体支持
- **#11380**（OPEN）：识别新的 `commonpb` Worker 回调变体，是 stacked PR 集的一部分，目标合入 `feature/worker-callbacks` 分支。
- **#11456**（OPEN）：CHASM `Callback` 组件支持新的 Worker 变体——区别于 Nexus 回调的 HTTP POST 方式，Worker 回调用于在另一个 namespace 中调用 Nexus。
- **信号**：Worker 回调是一项完整的新功能，预计将丰富跨 namespace 的工作流交互模式。

### 2. 复制任务可靠性增强（CGS Foundation 方向）
团队在 `team/cgs-foundation` 分支下密集布局复制路径改进：
- **#11401**：发出 handover 水位线和分片就绪事件，推进 namespace handover 完成判定。
- **#11411**：删除工作流复制任务携带 failover version，避免乱序删除导致数据不一致。
- **#11356**：为复制流增加客户端最大生命周期（带抖动），周期性优雅重建流，防止长期运行的流因未知状态卡死。
- **#11459**：在 `sent` 生命周期事件上记录复制任务实际携带的内容，因为 `LastUpdateVersionedTransition` 时间戳会被后续转换覆盖，事后无法恢复任务内容。

### 3. SQLite 数据库所有权租约
- **#11458**（OPEN）：为 SQL 插件添加可选的数据库租约能力，当 wrapper 和租约计数归零时关闭并移除 SQLite 连接池条目，跨 server 和 persistence 测试集群生命周期持有租约。
- **信号**：这是 SQLite 在 Temporal 中作为嵌入式数据库的基础设施完善，可能服务于单机部署和测试场景的稳定性提升。

### 4. CHASM 组件加固
- **#11432**（OPEN）：新增 `chasmtest.FirePureTasksStrict` 测试工具，强制验证“纯任务执行后必须失效”的框架假设——任务执行后立即重跑验证器，不合格的任务会被判定违规。
- **#10502**（OPEN）：若纯任务在有效执行后仍保持有效，则将其移入 DLQ 并抛出新任务错误，避免执行卡死。同时为测试框架增加单元测试验证。

---

## 用户反馈摘要

从今日 Issue 讨论中可以提炼以下来自真实用户的反馈：

**🗣️ 痛点一：高吞吐量下的 PostgreSQL 存储成本失控**
> “在每小时数十万工作流的场景下，数据库大小持续增加，无论如何设置保留期都无法阻止增长——表体量只有 46 左右，但整个数据库的体积远超比例。”

@oznu 在 #10145 中描述的场景揭示了存储回收机制在高负载下的失效，对依赖 PostgreSQL 的生产用户造成了实际的运维成本压力。该问题获得了 2 个 👍 和 7 条评论（Issue 已关闭）。

**🗣️ 痛点二：长期运行的监控指标膨胀**
> “matching 服务在 task queue 变为空闲或 `PhysicalTaskQueueManager` 卸载后，Prometheus 指标基数不回收。”

@Sanil2108 在 #9945 的反馈反映了长时间运行集群中监控体系逐渐被无效数据淹没的问题，这对大规模部署的可观测性构成持续威胁。

**🗣️ 满意点：泄漏修复响应迅速**
今日 #11460 的作者 @prathyushpv 在提交 Issue 当天即关联了修复 PR #11438，说明项目维护者（或贡献者）对资源泄漏类问题具有较高优先级意识。这种 “问题当天报告、当天即有修复” 的节奏对社区信心有积极影响。

---

## 待处理积压

### 长期未解决 Issue

1. **Matching 服务 Prometheus 指标基数无界增长**（#9945 — OPEN，202

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*