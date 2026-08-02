# OpenClaw 生态日报 2026-08-03

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-02 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-03

## 1. 今日速览

过去 24 小时项目活跃度极高：Issues 更新 500 条（活跃/新开 459，关闭 41），PR 更新 500 条（待合并 389，合并/关闭 111），并发布 1 个新版本 `v2026.7.2-beta.7`。新版本重点强化**状态安全与崩溃恢复**能力，包括隔离存储、崩溃可恢复 SQLite 快照、模式升级数据丢失拒绝等守护机制。然而社区关注度最高的热点集中在稳定性领域——消息丢失、会话状态失控、内存泄漏、崩溃循环等 P0/P1 问题持续获得大量讨论，大量 issue 带有 `clawsweeper:no-new-fix-pr` 与 `needs-maintainer-review` 标签，提示维护者审查积压可能正在扩大。

---

## 2. 版本发布

### v2026.7.2-beta.7
**发布时间**：2026-08-02（过去 24 小时内）

**核心更新 — 状态安全与恢复（State safety and recovery）**，具体包括：

- **隔离存储（Quarantine store）**：主数据库损坏时，持久化数据可被隔离保存而非直接丢失；
- **崩溃可恢复 SQLite 快照（Crash-recoverable SQLite snapshots）**：写入崩溃后仍可恢复快照状态；
- **崩溃持久的文件系统发布（Crash-durable filesystem publication）**：文件系统发布操作具备崩溃持久性；
- **Schema 升级数据丢失拒绝（Schema-upgrade data-loss rejection）**：当升级会导致数据丢失时，系统会**拒绝**升级操作，而非静默破坏数据；
- **回滚写入器快照恢复（Rollback-writer snapshot recovery）**：支持从回滚写入场景中恢复快照。

**破坏性变更**：无明确列出的破坏性变更，但需注意：

- Schema 升级拒绝机制意味着旧版本构建**无法直接打开**已被新版本升级的数据库文件——如在升级前未备份 `state/openclaw.sqlite`，降级将导致数据不可访问；
- 建议用户升级前备份整个状态目录（尤其跨大版本升级场景，参考 issue [#115421](https://github.com/openclaw/openclaw/issues/115421) 中出现的 schema v1/v6 数据丢失问题）。

**链接**：[v2026.7.2-beta.7 Release](https://github.com/openclaw/openclaw/releases)

---

## 3. 项目进展

过去 24 小时累计合并/关闭 111 个 PR，项目在多条战线上推进：

### 已合并的重要修复

- **[#117843](https://github.com/openclaw/openclaw/pull/117843) fix(agents): verify delegated writes before reporting success** — 合入后，共享 `write` 工具在返回成功回执前会进行字节级文件校验，修复了 [#67136](https://github.com/openclaw/openclaw/issues/67136) 中委托写入可能虚报成功的问题；同时超时/中断恢复路径也复用该校验机制。
- **[#117562](https://github.com/openclaw/openclaw/pull/117562) fix(ci): repair plugin prerelease validation** — 修复了插件预发布验证在 loader 移动后失败的问题，并为浏览器模式扩展测试共享生产状态 schema。

### 值得关注的大规模重构（开放中，待审查）

维护者 @steipete 今日提交了一批大规模重构 PR，方向高度一致——**收敛重复实现、统一核心语义**：

- [#118262](https://github.com/openclaw/openclaw/pull/118262) refactor: canonicalize cache mechanics（XL，缓存机制统一）
- [#118252](https://github.com/openclaw/openclaw/pull/118252) fix: bound pending approvals and preserve delivery order（XL，审批生命周期与投递顺序修复）
- [#118254](https://github.com/openclaw/openclaw/pull/118254) refactor(agents): centralize terminal lifecycle outcomes（L，终端生命周期统一分类）
- [#118235](https://github.com/openclaw/openclaw/pull/118235) refactor: adopt canonical async serialization（M，异步序列化收敛）
- [#118205](https://github.com/openclaw/openclaw/pull/118205) fix(auth): retain the selected account when migrating Codex sessions（XL，修复多 OAuth 账号迁移选错账号问题）

这批 PR 如果顺利合入，将显著降低代码库重复度，但此类大规模重构存在兼容性风险（多个 PR 标记 `merge-risk: 🚨 compatibility` / `🚨 session-state`），需要谨慎审查。

**链接**：[全部开放 PR](https://github.com/openclaw/openclaw/pulls)

---

## 4. 社区热点

### 今日讨论热度最高的问题

**🔥 #116277 — DeepSeek v4 Flash 静默回复失败（87 条评论）**  
[链接](https://github.com/openclaw/openclaw/issues/116277)  
模型 `deepseek/deepseek-v4-flash` 静默无法生成回复，Telegram 群组中用户仅收到 "No reply was generated for this message" 的通用回退。该问题被评为 **🦞 diamond lobster** 级别（最高影响评级），涉及消息丢失与 UX 摩擦双重影响。87 条评论说明大量用户可能受影响或参与了复现。当前无 fix PR。

**🔥 #116201 — 实时语音会话状态无界增长（49 条评论）**  
[链接](https://github.com/openclaw/openclaw/issues/116201)  
Realtime voice 会话的资源限制以条目计数或取消信号表达，而非硬性所有权边界，导致在慢速/突发供应商行为下可无限保留 superseded consult 工作、大帧、预就绪音频等。这属于会话状态管理的深层次架构问题。

**🔥 #115326 — 崩溃循环抑制器永久屏蔽 Discord/WhatsApp（25 条评论）**  
[链接](https://github.com/openclaw/openclaw/issues/115326)  
回归问题：Gateway 启动成功后，崩溃循环抑制器仍然生效，永久抑制 Discord 和 WhatsApp 通道；文档中的恢复路径 `channels.start` 失败并报 WebSocket 1006。属于 P1 + diamond lobster 级别。

### 分析

社区热点集中在**三个核心诉求**：

1. **可靠的消息投递** — "静默失败" 与 "消息丢失" 是用户最痛的点（#116277、#115326）；
2. **可预测的资源占用**

---

## 横向生态对比

# 个人 AI 助手/自主智能体开源生态横向对比分析报告

**日期：2026-08-03**


## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态正处于**从"功能竞赛"转向"可靠性竞赛"**的关键阶段。三个活跃项目（OpenClaw、OpenHands SDK、Pi）的社区讨论高度集中于同一组主题：消息丢失、会话状态失控、崩溃恢复、本地模型兼容性与安全边界。头部项目如 OpenClaw 凭借庞大的社区基数和每天数百条 issue/PR 的吞吐量，实质性地承担着"事实标准"的角色；新兴项目则以更快的迭代节奏和更高的治理效率在细分场景中建立优势。整体来看，**稳定性已成为用户第一诉求，AI 智能体的执行可审计性与状态持久化正在成为刚需**。

## 2. 各项目活跃度对比

| 维度 | OpenClaw | OpenHands SDK | Pi |
|---|---|---|---|
| Issues 更新 | 500 条（活跃/新开 459，关闭 41） | 30 条（新开/活跃 30，关闭 0） | 32 条（关闭 28，关闭率 87.5%） |
| PR 更新 | 500 条（待合并 389，合并/关闭 111） | 10 条（待合并 9，合并 1） | 19 条（合并/关闭 14，合并率 73.7%） |
| 新版本发布 | ✅ v2026.7.2-beta.7（状态安全与恢复） | ❌ 无 | ❌ 无 |
| 核心关注点 | 消息丢失、崩溃恢复、会话状态管理、审批生命周期 | 本地模型兼容性，安全审计（凭据泄露、未验证出口），ACP 兼容性 | 上下文压缩（compaction）可靠性、WezTerm/IME 终端体验、Provider 容错 |
| 健康度评估 | ⚠️ 高活跃但维护压力大（大量 `needs-maintainer-review` 标签积压，大规模重构 PR 等待审查） | ⚠️ 处理速度滞后（2/3 issue 待 triage，单日仅 1 个 PR 合入），安全类 issue 积压 | ✅ 治理高效（高关闭率/高合并率，维护者响应迅速），但存在终端渲染回归问题 |

## 3. OpenClaw 在生态中的定位

**OpenClaw 是当前生态中社区规模最大、迭代速度最快的"全能型个人 AI 助手"核心参照项目**，与同类项目存在清晰的定位差异：

- **社区规模对比**：单日 500 条 Issue + 500 条 PR 更新，远超 OpenHands SDK（40 条）与 Pi（51 条）的合计。diamond lobster 级 issue 可吸引 87+ 条评论，生态影响力无出其右。
- **技术路线差异**：OpenClaw 走**单体化个人助手平台**路线，强调跨渠道（Telegram/WhatsApp/Discord）、多模态（实时语音）、以及状态安全等内建平台级能力；Pi 走**终端优先的编码 Agent** 路线，强调 CLI 体验与轻量架构；OpenHands SDK 则定位为 **Agent 开发基础设施**，提供可嵌入的 SDK 与协议层（ACP）。
- **差异化优势**：OpenClaw 的 v2026.7.2-beta.7 引入的隔离存储、崩溃可恢复 SQLite 快照与 Schema 升级数据丢失拒绝机制，在**状态安全与崩溃恢复**维度上领先于 Pi 的 pre-dispatch durability barrier（仅覆盖特定场景）和 OpenHands 的 secrets 持久化修复。该版本标志着 OpenClaw 正在将智能体运行时向**数据库级持久化保证**方向推进。

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **上下文/会话状态管理** | OpenClaw、Pi、OpenHands SDK | OpenClaw #116201 实时语音会话无界增长；Pi #6879 auto-compaction 超过 100% 仍不触发、#7020 压缩后会话中断；OpenHands #4296 上下文压缩 PR、#4080 单事件反序列化失败导致整个会话加载失败 |
| **状态持久化与崩溃恢复** | OpenClaw、Pi、OpenHands SDK | OpenClaw v2026.7.2 隔离存储 + 崩溃可恢复快照，升级数据丢失拒绝；Pi #7466 pre-dispatch durability barrier（区分"未调用"与"已调用但输出丢失"）；OpenHands #4166 secrets 持久化修复 |
| **本地/第三方 LLM 兼容性** | OpenHands SDK、Pi | OpenHands #4248 `execute_bash` 缺少 security_risk 参数、#3992 弱模型被异常终止；Pi #7062 非标准流式响应（缺失 finish_reason）兼容。用户对 Ollama/LM Studio/Databricks 等本地/非旗舰模型适配需求集中爆发 |
| **消息/回复可靠性** | OpenClaw、OpenHands SDK、Pi | OpenClaw #116277 模型静默回复失败（87 条评论）、#115326 崩溃循环抑制器永久屏蔽通道；OpenHands #4260 自动化 PR review 间歇性失效；Pi #7315 Fireworks 请求偶发立即超时 |
| **安全与凭据治理** | OpenHands SDK、OpenClaw | OpenHands fork 审计发现 RemoteWorkspace 出口绕过（#4261）、LLM 初始化未验证 HTTP 请求（#4263）、GitHub 凭据未脱敏（#4271）、模型自评风险绕过人工确认（#4157）；OpenClaw 状态升级数据丢失拒绝机制亦属数据安全范畴 |

## 5. 差异化定位分析

| 维度 | OpenClaw | OpenHands SDK | Pi |
|---|---|---|---|
| **功能侧重** | 全渠道个人助手（Telegram/WhatsApp/Discord/实时语音），强调消息可靠性、状态安全、审批生命周期 | Agent 开发 SDK 与协议层，强调 LLM 调用上下文、持久化事件、ACP 兼容性、安全审计 | 终端 CLI 编码 Agent，强调 TUI 体验（WezTerm/IME/内联图片）、上下文压缩、多 Provider 适配 |
| **目标用户** | 个人用户/重度助手使用者，追求开箱即用的多平台个人 AI | Agent 应用开发者/企业内部工具链，追求可嵌入、可审计的 Agent 基础设施 | 开发者/技术用户，偏好终端工作流与编码 Agent 的深度集成 |
| **技术架构** | 单体平台 + 插件系统，SQLite 状态存储，共享 write 工具字节级校验，大规模集中式重构 | SDK 库 + 事件溯源，LiteLLM 代理层接入，ACP 协议兼容，安全分析器 | 模块化 CLI，异步 provider 适配器层，jiti 扩展加载，实验性命令行组合架构 |
| **当前最大短板** | 海量 issue 堆积，维护者审查积压可能扩大；大规模重构（5 个 XL/L 级 PR）存在兼容性风险 | 维护吞吐不足（合并率 10%）；弱/本地模型兼容性差；安全问题集中 | 上下文压缩机制可靠性不足；终端渲染回归（已回滚可切换渲染器）；非拉丁文输入体验待完善 |

## 6. 社区热度与成熟度

**第一梯队（平台级，快速迭代 + 大规模治理挑战）**：**OpenClaw**。单日 500 条 Issue/PR 级别的吞吐使其处于生态最活跃位置，但大量待审查标签与 XL 级重构 PR 并存，社区处于**功能快速推进与稳定化拉锯**阶段，适合有资源投入的开发者或需要完整功能的个人用户。

**第二梯队（工具级，高速治理）**：**Pi**。87.5% 的 issue 关闭率与 73.7% 的 PR 合并率表明其维护者治理节奏高效，项目处于**密集迭代期**且社区反馈闭环良好。适合终端重度用户和希望跟随快速演进的开发者。

**第三梯队（基础设施级，质量巩固 + 待清理积压）**：**OpenHands SDK**。单日合并率仅 10%，2/3 issue 待 triage，叠加多个长期未修复的关键 bug（#4248、#3992 已持续数月），项目处于**质量巩固期但维护带宽明显不足**，安全审计类 issue 的上升值得团队警惕。

## 7. 值得关注的趋势信号

1. **"静默失败"已成社区最不可容忍的问题类别**：OpenClaw 的"No reply was generated"、OpenHands 的间歇性 PR review 失效、Pi 的 Fireworks 瞬时超时，本质上同属"无报错但无结果"。用户不再接受通用回退消息，**可诊断、可解释的执行失败是下一代 Agent 的入场券**。

2. **Agent 执行状态正从"尽力而为"走向"事务性保证"**：OpenClaw 的崩溃可恢复快照 + Schema 升级拒绝、Pi 的 pre-dispatch 持久化屏障、OpenHands 的按事件跳过降级策略，共同指向一个趋势——**Agent 运行时需要像数据库一样提供持久化、原子性与可恢复性**。对开发者而言，这意味着选择框架时需要优先评估其状态管理层的事务能力。

3. **本地/非旗舰 LLM 兼容性从"Nice-to-have"变为"核心需求"**：三个项目均出现大量关于 Ollama、LM Studio、DeepSeek-Reasoner、Databricks Qwen3 等模型的适配问题。**"弱模型/异构模型下行为一致性"正在成为 Agent 框架的关键竞争力指标**。

4. **安全审计进入常态化阶段**：OpenHands SDK 的 fork 审计报告（未验证出口、凭据未脱敏、模型自评风险）暴露了 AI Agent 特有的攻击面。随着 Agent 权限边界扩大，**针对 Agent 的供应链安全与访问控制审计将成为企业选型的硬性门槛**。

5. **技能与工具生态互操作开始形成**：Pi 兼容 Claude Code 的 SKILL.md frontmatter、OpenHands 围绕 ACP 协议讨论版本兼容、OpenClaw 的技能系统持续演进，三者共同指向**跨框架技能可移植**的方向。统一的技能交换格式可能在不远的将来成为生态分化的分水岭。

6. **维护者治理能力成为项目健康度的决定性变量**：Pi 以高关闭率/高合并率在社区中建立了强信任；OpenHands 的处理滞后直接反映在用户对"本地模型支持"的负面反馈上；OpenClaw 则面临"规模诅咒"——海量 issue 与重构 PR 叠加发出的审查积压信号。**对技术决策者而言，社区治理效率与代码提交频率同样值得关注**。

---

*报告生成时间：2026-08-03。数据来源：OpenClaw、OpenHands SDK、Pi 项目官方 GitHub 动态。*

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-08-03

## 1. 今日速览

过去 24 小时项目活跃度处于**高位**，共产生 30 条 Issue 更新与 10 条 PR 更新，但**无新版本发布**。Issue 侧全部为“新开/活跃”状态、零关闭，且其中约 2/3 带有 `needs-triage` 标签，说明维护者分类压力较大、处理速度未跟上反馈节奏。PR 侧 9 条待合并、1 条已合并，合并吞吐量偏低。值得关注的是，社区讨论集中在安全（凭据泄露、未验证出口）、ACP 兼容性与本地模型/工具链集成三大主题，安全类审计 Issue 数量明显上升，需引起维护团队重视。

---

## 2. 版本发布

**无新版本发布**（过去 24 小时 Releases 数为 0）。当前无版本更新、破坏性变更或迁移注意事项可报告。

---

## 3. 项目进展

过去 24 小时仅 **1 条 PR 被合并**，另有 9 条处于待合并状态：

### 已合并 PR
- **[#4167] fix(llm): resolve chat-option capabilities from the canonical model name**（作者 @JiataiWang，2026-07-21 创建，08-02 合并）
  修复了代理（proxied）思考模型在能力检测时忽略 `model_canonical_name`、导致 temperature/top_p 未正确剥离、thinking 模式未被开启的问题。该修复对使用 LiteLLM 代理层接入思考模型的用户有直接收益。合并后回归测试已覆盖。
  https://github.com/OpenHands/software-agent-sdk/pull/4167

### 待合并 PR（方向性信号）
- **#4328** `chore(sdk): deprecate AgentBase.model_dump_succint` — 响应 #4224 清理议题，采用废弃而非直接删除，兼顾公共 API 兼容性。https://github.com/OpenHands/software-agent-sdk/pull/4328
- **#4166** `fix(conversation): persist secrets added via update_secrets` — 修复 secrets 未持久化、重启后丢失的问题，已附测试。https://github.com/OpenHands/software-agent-sdk/pull/4166
- **#4164** `fix(grep): honor brace alternation in the include filter` — 修复 `*.{ts,tsx}` 类 brace 模式匹配失效，涉及 ripgrep 与 Python 双后端。https://github.com/OpenHands/software-agent-sdk/pull/4164
- **#4159** `refactor(sdk): centralize LLM call context` — LLM 调用上下文集中化重构，降低重复代码。https://github.com/OpenHands/software-agent-sdk/pull/4159

整体来看，项目今日在**合并进度上推进有限**，但待合并队列中包含了 secrets 持久化修复、grep 功能修复、API 清理等多个务实改进，若能及时合入将对 SDK 稳定性与可维护性有明显提升。

---

## 4. 社区热点

以下 Issues/PRs 在过去 24 小时获得最多评论，反映了社区的集中关切：

- **[#4019] ACP profiles inject workspace project skills that duplicate what the ACP CLI already ingests (AGENTS.md)** — 15 条评论
  讨论围绕 PR #4018 引入的 `load_project_skills=True` 与 ACP CLI 自身 AGENTS.md 注入产生的技能重复问题。用户关心的是 ACP 会话中上下文是否被无效重复内容污染。https://github.com/OpenHands/software-agent-sdk/issues/4019

- **[#4248] Missing required parameters for function 'execute_bash': {'security_risk'}** — 13 条评论
  使用 DeepSeek-Reasoner 等模型时出现 `execute_bash` 缺少 `security_risk` 参数的错误。该问题已持续数月，评论活跃度高，显示本地/非主流模型与安全分析器的兼容性仍是主要痛点。https://github.com/OpenHands/software-agent-sdk/issues/4248

- **[#3992] Asymmetric handling of content-without-tool-call responses terminates agents driven by weaker/local models** — 12 条评论
  `ResponseDispatchMixin` 对“有内容但无工具调用”响应的不对称处理导致弱模型/本地模型驱动的 agent 被终止。此议题与 #4248 同属“本地/弱模型兼容性”大类，说明 OpenHands 对非旗舰模型的适配还不够健壮。https://github.com/OpenHands/software-agent-sdk/issues/3992

- **[#4063] max_concurrent_runs does not limit native async conversations** — 12 条评论
  `max_concurrent_runs` 配置仅约束同步 `ThreadPoolExecutor`，对原生异步 `EventService.run()` 不生效，可能导致资源超限。属于架构层行为不一致问题。https://github.com/OpenHands/software-agent-sdk/issues/4063

- **[#4080] One unregistered event kind fails the entire conversation load** — 11 条评论
  单个持久化事件反序列化失败会导致整个会话加载失败并 404，社区期望降级为按事件跳过。https://github.com/OpenHands/software-agent-sdk/issues/4080

**社区诉求总结**：最集中的两点是 — (1) **本地模型/第三方 LLM 的兼容性**（#4248、#3992、#4255、#4250），(2) **系统在边缘场景下的韧性**（#4080、#4063、#4329），即单个失败不应拖垮整个会话或并发控制。

---

## 5. Bug 与稳定性

按严重程度排列（高 → 低）：

### 严重/安全相关
- **[#4261] CRITICAL: RemoteWorkspace host validation gap enables unvalidated egress**（fork 审计发现，2026-07-05 创建）
  `RemoteWorkspaceMixin` 缺少主机校验，可绕过 air-gap 策略形成出口漏洞。https://github.com/OpenHands/software-agent-sdk/issues/4261
- **[#4263] HIGH: `get_litellm_model_info` makes unvalidated httpx.get call at LLM init**（fork 审计发现）
  LLM 初始化时发起未验证的 HTTP 请求，存在策略绕过风险。https://github.com/OpenHands/software-agent-sdk/issues/4263
- **[#4157] LLMSecurityAnalyzer trusts model self-assessed risk level**（2026-07-16）
  `confirmation_mode: true` 下模型可自行将高风险动作标记为 LOW 从而绕过人工确认，属于安全设计缺陷。https://github.com/OpenHands/software-agent-sdk/issues/4157
- **[#4271] GitHub credentials in git remote URLs not redacted**（2026-07-21）
  终端输出泄露 GitHub 凭据。https://github.com/OpenHands/software-agent-sdk/issues/4271
- **[#4282] Security: Unvalidated Workspace Directory in VSCode URL Endpoint**（PR，安全修复）
  修复 `/vscode/url` 端点未验证 `workspace_dir` 参数的问题。https://github.com/OpenHands/software-agent-sdk/pull/4282

### 功能/稳定性 Bug
- **[#4329] ACPAgent.close() races with agent.step()**（2026-08-02 创建，最新）
  并发关闭导致 `AttributeError`/`RuntimeError`，`Conversation.run()` 可能卡死。尚未有 fix PR。https://github.com/OpenHands/software-agent-sdk/issues/4329
- **[#4248] `execute_bash` 缺少 `security_risk` 参数**（2026-04-25 创建）
  影响 DeepSeek-Reasoner 等模型，尚无 fix PR。https://github.com/OpenHands/software-agent-sdk/issues/4248
- **[#3992] 弱模型因“有内容无工具调用”而被终止**（2026-07-04 创建）
  非对称分发逻辑问题，无 fix PR。https://github.com/OpenHands/software-agent-sdk/issues/3992
- **[#4063] `max_concurrent_runs` 不限制 async 会话**（2026-07-10 创建）
  并发控制失效。https://github.com/OpenHands/software-agent-sdk/issues/4063
- **[#4080] 单个事件反序列化失败导致整个会话加载失败**（2026-07-10 创建）
  应降级为按事件跳过。https://github.com/OpenHands/software-agent-sdk/issues/4080
- **[#4245] Agent-Server Webhook 连接失败导致容器崩溃**（2026-01-28 创建）
  老问题仍在活跃讨论中。https://github.com/OpenHands/software-agent-sdk/issues/4245
- **[#4256] browser-use 在 Docker 中因缺少 `--no-sandbox` 无法启动 Chromium**（2026-06-12 创建）
  影响浏览器自动化功能。https://github.com/OpenHands/software-agent-sdk/issues/4256
- **[#4270] GUI 保存 LLM Profile API Key 加密后 Sub-Agent 认证失败**（2026-07-21 创建）
  加密存储与子代理调用链路脱节。https://github.com/OpenHands/software-agent-sdk/issues/4270

---

## 6. 功能请求与路线图信号

- **[#3442] [Feature]: Intelligent Model Selection**（👍 1，9 条评论，2026-05-29 创建）
  用户希望系统自动为每项任务路由到最佳模型，免去手动记忆模型成本/性能/优势的负担。“Decide for Me”动态选择器是该请求的核心。目前无对应 PR，但结合 LLM Profile 体系存在，有被纳入下一版本规划的可能。https://github.com/OpenHands/software-agent-sdk/issues/3442

- **[#4224] [enhancement, architecture] Cleanup: remove dead code, dedup shared logic, trim line count**（2026-07-27 创建，3 条评论）
  提出多处死代码、重复逻辑与行数精简建议，并已由**#4328**（deprecate `model_dump_succint`）响应部分内容。该议题体现了项目进入“技术债务清理”阶段，维护者可能推动更多此类清理。https://github.com/OpenHands/software-agent-sdk/issues/4224

- **#4296 `feat:上下文压缩模块+task list`**（PR，2026-07-29 创建，待合并）
  该 PR 引入上下文压缩与任务列表功能。若合入，将直接提升长会话下 LLM 上下文管理能力，是“功能请求转化为实现”的信号。https://github.com/OpenHands/software-agent-sdk/pull/4296

- **#3503 `feat: add public from_persisted() entry point to AgentSettingsBase`**（PR，2026-06-04 创建，待合并）
  为持久化设置迁移提供公共入口，长期在队列中。https://github.com/OpenHands/software-agent-sdk/pull/3503

- **#4151 `Trace LLM endpoint alongside model`**（PR，2026-07-18 创建，待合并）
  在追踪中记录 LiteLLM endpoint 而不暴露 API key，可观测性改进。https://github.com/OpenHands/software-agent-sdk/pull/4151

---

## 7. 用户反馈摘要

- **本地 LLM 支持仍是最大痛点**：#4255（Ollama 任务超过 5 分钟被杀死）、#4247（LM Studio 未提供 LLM Provider）、#4250（Workers AI 模型上下文窗口不足）等 Issue 表明，用户对“OpenHands + 本地模型”组合的体验有较高期待，但当前实现存在超时配置不生效、provider 识别失败、上下文窗口校验过严等问题。这些反馈指向一个共同诉求：**本地模型使用需要更健壮的配置与降级策略**。https://github.com/OpenHands/software-agent-sdk/issues/4255 | https://github.com/OpenHands/software-agent-sdk/issues/4247 | https://github.com/OpenHands/software-agent-sdk/issues/4250

- **Web 浏览器功能差评集中**：#4253 “Webbrowser inside of OpenHands is broken”（用户无法正常测试自己开发的应用）、#4257 “Cannot create preview links or open browser tabs in sandbox” 显示浏览器集成是 Web 应用开发场景的核心短板，用户希望 OpenHands 能真正替代浏览器调试工具。https://github.com/OpenHands/software-agent-sdk/issues/4253 | https://github.com/OpenHands/software-agent-sdk/issues/4257

- **自动化流程可靠性不足**：#4260 “Cloud Automation PR reviewer intermittently posts no review” 指出自动化 PR 审查会随机失败（webhook 序列化错误 + 600s 上限杀死挂起 agent），影响 CI 集成信任度；#4267 “No response from ACP server” 反映本地 ACP 自动化配置易卡死。https://github.com/OpenHands/software-agent-sdk/issues/4260 | https://github.com/OpenHands/software-agent-sdk/issues/4267

- **ACP 生态兼容性焦虑**：#4093（ACP 0.11 移除 `models` 字段导致 Gemini CLI 报错）、#4158（`switch_profile` 半应用状态不一致）、#4019（技能注入重复）表明用户对 ACP 协议版本变动和会话切换的状态一致性敏感，期望 SDK 在上游版本升级时

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-03

## 1. 今日速览

过去24小时Pi项目保持高度活跃：共32条Issue更新（其中28条已关闭，关闭率87.5%），19条PR活动（14条已合并/关闭，合并率73.7%），无新版本发布。项目处于密集的Bug修复与功能迭代阶段，维护团队响应速度极快，大量用户报告的Issue在当天即被关闭。社区讨论焦点集中在**上下文压缩（compaction）可靠性**、**终端兼容性**（WezTerm/IME/多行粘贴）以及**扩展系统体验优化**三个方向。整体项目健康度良好，从Issue关闭率和PR合并率来看，维护者治理节奏稳定高效。


## 2. 版本发布

过去24小时内无新版本发布。


## 3. 项目进展

今日合并/关闭了14个PR，覆盖CLI架构、AI适配器、终端渲染、扩展系统等多个方面：

### 关键合并/关闭PR

**AI适配器层加固**
- [#7471 fix(ai): retry transient provider errors in Google adapters](https://github.com/earendil-works/pi/pull/7471) — Google Vertex/Gemini适配器在429/5xx瞬时错误时直接终止agent线程，此PR为Google适配器增加了与其他provider（Anthropic/OpenAI/Azure）一致的重试机制，修复AgentHarness用户在高负载下的稳定性问题。
- [#7467 feat(ai): add MiniMax video generation](https://github.com/earendil-works/pi/pull/7467) — 新增MiniMax视频生成支持（全球版+中国版），包含v1/v2端点、任务创建/查询/下载的完整处理链路 —— 视频生成能力正在逐步补齐。
- [#7435 fix(coding-agent): increase connection attempt timeout](https://github.com/earendil-works/pi/pull/7435) — 将Undici连接器地址族尝试超时从Node默认的250ms提升至2秒，修复高延迟路由下Fireworks请求被误判超时的问题（关联Issue #7315）。

**编码能力与技能生态**
- [#7468 feat(agent,coding-agent): accept Claude Code skill frontmatter](https://github.com/earendil-works/pi/pull/7468) — 两个技能加载器（agent + coding-agent）均兼容Claude Code的SKILL.md frontmatter规范，意味着社区大量Claude Code技能可直接在Pi中使用，大幅扩展技能生态。
- [#7466 feat(coding-agent): opt-in pre-dispatch durability barrier](https://github.com/earendil-works/pi/pull/7466) — 新增可选预派发持久化屏障：在provider请求发出前即持久化会话，避免崩溃时无法区分"未调用provider"与"已调用且可能计费但输出丢失"的模糊状态，对需要at-most-once语义的嵌入式场景至关重要。

**CLI与存储架构重构**
- [#7459 feat(coding-agent): compose experimental CLI commands](https://github.com/earendil-works/pi/pull/7459) — 将实验性CLI命令与现有CLI解析器组合，拒绝不支持的旧版选项，并添加类型化分发；#7455、#7478（session storage向repository模式演进，合并/关闭）共同推动存储层向更清晰的资源所有权模型演进。

**终端渲染回退**
- [#7473 Revert "feat(tui): add switchable terminal renderers"](https://github.com/earendil-works/pi/pull/7473) — 回滚了#7440的可切换终端渲染器功能。推测#7440引入了回归，badlogic决定暂缓，这解释了今天#7482等终端渲染修复的紧迫性。
- [#7482 fix(tui): prefer iTerm2 inline images over kitty on WezTerm](https://github.com/earendil-works/pi/pull/7482) — 修复WezTerm下kitty内联图片在滚动转录中逐渐被擦除的bug（#7481），改为优先使用iTerm2协议。

**其他**
- [#7488 fix(coding-agent): respect shellPath in minimal mode example](https://github.com/earendil-works/pi/pull/7488) — 修复minimal-mode示例忽略settings.json中shellPath的问题。
- [#7480 feat(ai): add LLM Gateway provider](https://github.com/earendil-works/pi/pull/7480) — 新增LLM Gateway（OpenRouter风格路由器）为内置openai-completions provider，但此PR已关闭。


## 4. 社区热点

**#6879 — auto-compaction触发机制缺陷（10条评论，10个👍，最受关注）**
https://github.com/earendil-works/pi/issues/6879

用户 @alexanderkreidich 报告在GPT-5.6-sol长会话中，context window已超100%但auto-compaction始终未触发，直到API在373k tokens处拒绝请求。用户建议在每次agent操作后检查context阈值。该Issue已开放近两周且有10个👍，是当前社区最关心的稳定性问题之一。相关PR #7498（defer idle compaction until next prompt）明确提及关联此Issue。

**#7020 — 压缩后Pi有时不继续（7条评论）**
https://github.com/earendil-works/pi/issues/7020

长时间运行的"协调者"类型会话在compaction后偶发中断，用户推测是compaction流程中某些边界条件处理不当。该Issue已标记为`inprogress`，与#6879共同指向compaction机制的深层次问题——**未来版本需要系统性重构compaction触发与恢复逻辑**。

**#7062 — openai-completions适配器处理数组内容和缺失finish_reason（6条评论）**
https://github.com/earendil-works/pi/issues/7062

某些Databricks模型（Qwen3、gpt-oss reasoning）在工具调用时返回`typed array`格式的content以及缺少`finish_reason`，导致Pi解析异常。这是一条典型的**非标准流式响应兼容性**问题，说明Pi的provider适配层需要更宽容的响应容错。

**社区诉求归纳**：当前社区最关心的不是新功能，而是**长会话场景下的稳定性**（compaction可靠性、provider容错）和**终端体验一致性**（WezTerm/IME、多行粘贴）。这两个方向也是Issue数量和讨论热度最集中的领域。


## 5. Bug 与稳定性

### 严重级别：高（影响核心使用流程）

- **[#6879] auto-compaction在context超过100%后仍不触发，直至provider溢出**（OPEN，10评论）
  https://github.com/earendil-works/pi/issues/6879
  影响所有使用长上下文模型的用户，导致token浪费和会话中断。相关PR #7498 已提出在下一个prompt时延迟空闲压缩的修复方向。

- **[#7020] 压缩后Pi有时不继续**（OPEN，inprogress，7评论）
  https://github.com/earendil-works/pi/issues/7020
  长时间运行会话在compaction后偶发中断，影响会话连续性。已标记inprogress，暂无对应PR。

- **[#7413] GitHub Copilot GHE.com企业账户compaction失败 — "unknown stamp"错误**（CLOSED，3评论）
  https://github.com/earendil-works/pi/issues/7413
  GHE.com企业账户的`/compact`命令在summarization阶段返回400认证错误，正常聊天不受影响 —— 表明compaction使用的认证路径与普通请求不同。

### 严重级别：中（影响特定环境或模型）

- **[#7315] Fireworks请求偶尔立即失败"Request timed out"**（CLOSED，4评论）
  https://github.com/earendil-works/pi/issues/7315
  失败时内容为空且token使用量为零，说明在发送前即超时。已由[#7435](https://github.com/earendil-works/pi/pull/7435)修复（地址族尝试超时250ms→2s）。

- **[#7323] `pi update --models`因瞬时目录请求停滞而整个刷新失败**（CLOSED，3评论）
  https://github.com/earendil-works/pi/issues/7323
  网络偶发HTTPS请求停滞时整个模型目录刷新失败，缺少重试机制。

- **[#7499] auth.json含UTF-8 BOM时所有凭据被静默忽略**（CLOSED，1评论）
  https://github.com/earendil-works/pi/issues/7499
  Windows用户使用记事本保存auth.json时可能无意加入BOM，导致所有provider报"No API key found"。这与#7323一起构成**Windows平台可靠性的隐患**。

- **[#7491] qwen-token-plan-cn目录匹配Team Plan白名单，Personal用户9/15模型被拒**（CLOSED，1评论）
  https://github.com/earendil-works/pi/issues/7491
  模型目录与产品版本不匹配，导致个人版订阅用户在多数模型上遇到AccessDenied。

### 严重级别：低（UI/交互局部问题）

- **[#7402] 粘贴孟加拉语后按空格导致行重复 — 宽度过度计算使差分渲染器失步**（CLOSED，6评论）
  https://github.com/earendil-works/pi/issues/7402
  宽字符宽度计算与终端物理光标不同步，影响非拉丁文用户。

- **[#7486] WezTerm启用硬件光标后光标在"Working..."状态跳动**（CLOSED，3评论）
  https://github.com/earendil-works/pi/issues/7486
  showHardwareCursor修复了IME候选窗口位置，但引入了新的光标跳动问题。

- **[#7490] WezTerm输入中文时IME候选窗口闪烁/跳跃/重影**（CLOSED，2评论）
  https://github.com/earendil-works/pi/issues/7490
  在WezTerm中pi agent的IME表现劣于codex CLI，且该Issue与#7486互为关联，说明**WezTerm+IME的组合仍缺乏系统性测试**。

- **[#7481] WezTerm内联kitty图片在滚动转录中退化为单行细条**（CLOSED，2评论）
  https://github.com/earendil-works/pi/issues/7481
  已由[#7482](https://github.com/earendil-works/pi/pull/7482)修复（优先iTerm2内联图片）。

- **[#7464] WebSocket错误后结构化关闭元数据丢失**（CLOSED，2评论）
  https://github.com/earendil-works/pi/issues/7464
  33个provider传输失败中29个仅剩"WebSocket error"通用信息，缺少可诊断的结构化数据。

- **[#7497] 会话发现静默忽略全局会话目录下的符号链接目录**（CLOSED，2评论）
  https://github.com/earendil-works/pi/issues/7497
  listSessions使用readdir未跟随符号链接，导致pi-web等工具无法看到符号链接目录中的会话。

- **[#7489] minimal-mode示例忽略配置的shellPath，在Windows上默认运行WSL**（CLOSED，1评论）
  https://github.com/earendil-works/pi/issues/7489
  已由[#7488](https://github.com/earendil-works/pi/pull/7488)修复。

- **[#7479] Tab补全斜杠命令后参数补全永不出现**（CLOSED，1评论）
  https://github.com/earendil-works/pi/issues/7479
  Tab补全命令名后插入尾随空格并关闭自动补全列表，且不会重新查询参数。

### 严重级别：性能/优化

- **[#7483] 扩展加载器为每个扩展创建jiti实例并串行加载**（CLOSED，1评论）
  https://github.com/earendil-works/pi/issues/7483
  启动性能优化空间明显：复用jiti实例+并行加载可显著缩短启动时间。

- **[#7485] 工具schema每个请求序列化两次（文本片段+JSON tools参数）**（CLOSED，1评论）
  https://github.com/earendil-works/pi/issues/7485
  无原生工具调用模型的请求中工具定义被重复发送，既浪费token也无从选择退出。


## 6. 功能请求与路线图信号

### 高潜力纳入下一版本（已有对应PR或维护者认可）

- **模型目录与版本匹配校验**（#7491）— 用户因目录与白名单不匹配被拒。建议在目录发布流程中增加产品版本验证。短时间内再次出现，值得优先处理。
- **--exclude-extensions / -xe 每运行排除扩展**（[#7475](https://github.com/earendil-works/pi/issues/7475)，CLOSED）— 用户希望按次运行排除重扩展包，避免临时卸载。属于小改动高收益的CLI优化，可能被快速采纳。
- **MCP/扩展工具返回图片自动resize**（[#7330](https://github.com/earendil-works/pi/pull/7330)，OPEN）— 工具返回的图片以全分辨率进入会话历史，浪费context。虽然PR待合并时间较长（8/30至今），但方向明确。
- **/scoped-models中允许选择思考级别**（[#7487](https://github.com/earendil-works/pi/issues/7487)，CLOSED）— 用户要求支持`provider/id:level`格式，绑定alt+left/right快捷键。设置层已支持该格式，只缺UI。

### 信号较弱的长期诉求

- **滚动锁定/阅读模式**（[#4679](https://github.com/earendil-works/pi/issues/4679)，CLOSED，5/18创建，3评论）— 终端输出时滚动阅读会跳回底部；与之相关的[#7495](https://github.com/earendil-works/pi/issues/7495 "Keep the editor visible and stop the view from jumping...") 也是同一类诉求。该Issue已悬置近3个月，说明**滚动行为优化不在当前优先级**，但用户持续提出，可能在后续UI迭代中纳入。
- **单行状态页脚布局**（[#7477](https://github.com/earendil-works/pi/issues/7477)，CLOSED）— UI精简建议。
- **MRU模型切换**（[#6982](https://github.com/earendil-works/pi/issues/6982)，CLOSED，7/22创建，1评论）— 按最近使用顺序快速切换模型的效率建议。已标记`no-action`，说明当前架构中优先级不高。
- **会话存储/持久化架构优化系列**（[#7455](https://github.com/earendil-works/pi/pull/7455)、[

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*