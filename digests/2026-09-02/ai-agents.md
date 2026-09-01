# OpenClaw 生态日报 2026-09-02

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-01 22:35 UTC

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

# 个人 AI 助手/自主智能体开源生态横向分析报告（2026-09-02）


## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态正处于**从功能堆叠转向基础设施稳健性建设**的关键阶段。今日各头部项目的高频议题高度一致：会话状态持久化、秘密治理、上下文计量准确性、计费数据一致性——这些都是规模化落地前必须解决的工程化问题。与此同时，多项目不约而同地出现“技能管理重构”与“多智能体/回调架构”的讨论，昭示着生态正在从单次任务执行迈向持续运行的自治系统。整体呈现“高活跃、强分化、基础加固”的态势。


## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | 合并/关闭 | Release | 健康度评估 |
|------|------------|---------|-----------|---------|-----------|
| **Hermes Agent** | 458（新开/活跃 360，关闭 98） | 500（待合并 401，合并/关闭 99） | 99 | 无 | 高活跃、响应快；CI 基础设施反复回滚，略有隐忧 |
| **OpenHands SDK** | 26（新开/活跃 16，关闭 10） | 50（待合并 43，合并/关闭 7） | 7 | 无 | 活跃但合并率偏低（14%），审查积压需关注 |
| **LiteLLM** | 87 | 349（待合并 192，合并/关闭 157） | 157 | 2 个（v1.101.0-dev.1、v1.99.0） | 极高迭代速度，合并效率 45%；但发布流程存在供应链隐患 |
| **Temporal** | 2（均活跃） | 56（待合并 44，合并/关闭 12） | 12 | 无 | 稳定推进，聚焦可靠性修复；合并速度放缓但仍健康 |
| **OpenClaw** | 无数据 | 无数据 | — | — | 核心参照，今日无动态数据可评估 |
| **Pi** | 无数据 | 无数据 | — | — | 无动态数据可评估 |

> 注：OpenClaw 今日无可用数据，建议补充抓取源。


## 3. OpenClaw 在生态中的定位

作为核心参照项目，OpenClaw 今日无社区动态数据纳入报告，无法直接量化其活跃度。但从生态整体格局推断：同类项目 Hermes Agent 日均 500 条 PR 更新、80+ 条 Issue 活跃，表明个人 AI 助手赛道已进入**白热化竞争期**。若 OpenClaw 有意维持生态位，需关注以下竞品动向：社区对会话持久化的强烈需求（Hermes 多线程讨论、OpenHands 连续 4 个相关 Bug）、订阅 OAuth 接入情绪（Hermes #25267，👍 53）、以及技能管理架构的集体反思（OpenHands #4243）。建议后续补齐 OpenClaw 的 Issues/PR/Release 数据，以便完成与其他项目的精准对标分析。


## 4. 共同关注的技术方向

| 方向 | 涉及项目 | 具体诉求 |
|------|---------|---------|
| **会话状态持久化** | Hermes Agent、OpenHands SDK | Hermes 关注群聊在桌面关闭后持续运行及后端权威托管（#89995、#97681）；OpenHands 连续暴露 meta.json 持久化缺陷（#4810、#4811、#4813、#4814） |
| **秘密治理与安全** | OpenHands SDK、Hermes Agent、LiteLLM | OpenHands 高优关闭“秘密掩码仅覆盖 1/13 工具”（#4677）与“env 泄露密钥”（#4802）；Hermes 合入注册表驱动脱敏（#97383）；LiteLLM 将安全隔离列为主要讨论方向 |
| **技能/工具管理重构** | OpenHands SDK、Hermes Agent | OpenHands 发起“Re-thinking Skills Management”PRD（#4243），指出现有 Microagent 管理界面落后于 AGENTS.md 等新能力；Hermes 的 Skills 索引持续退化（#66616，🔥137 条评论） |
| **成本/计量准确性** | Hermes Agent、LiteLLM | Hermes 修复上下文计量器“虚高”问题（#100621）；LiteLLM 流式计费数据丢失（#14457）仍在发酵 |
| **模型路由智能化** | OpenHands SDK、LiteLLM | OpenHands 社区呼吁“自动为我决定”的智能模型路由（#3442）；LiteLLM 核心方向即路由策略优化 |
| **回调/多智能体编排** | Temporal、Hermes Agent | Temporal 大批量推进 Worker callbacks（5+ stacked PR）；Hermes 群聊架构讨论从“前端渲染器驱动”走向后端权威托管 |
| **可观测性** | Temporal、Hermes Agent | Temporal 为命名空间复制添加结果/延迟指标（#11884）；Hermes 合入 Telemetry Phase 2 指标发送器（#95278） |


## 5. 差异化定位分析

| 维度 | Hermes Agent | OpenHands SDK | LiteLLM | Temporal |
|------|-------------|---------------|---------|----------|
| **功能侧重** | 端侧会话 Agent（桌面/CLI 优先） | 通用智能体应用 SDK | LLM 网关/代理层 | 工作流/编排引擎 |
| **目标用户** | 个人用户、订阅制用户 | 开发者、企业智能体构建者 | 平台工程师、B 端计费方 | SRE、后端架构师 |
| **技术架构** | 单体 Agent + 前端渲染器驱动群聊（向服务端权威迁移） | 模块化 SDK，ConversationService 为核心 | 代理路由 + 计费 + 安全边界 | 持久化工作流引擎 + 强一致状态 |
| **当前核心矛盾** | 桌面端跨平台稳定性、订阅计费双重付费 | PR 合并审查积压、持久化一致性问题 | 计费准确性、发布供应链安全 | SQL 连接池故障“假活”、回调功能落地 |
| **商业化信号** | Claude 订阅 OAuth 直连呼声强烈 | 企业治理层需求明确（文件控制/审计） | 计费准确性和成本控制是核心卖点 | 可靠性是最大卖点，回调功能预示新场景 |

**核心差异总结**：Hermes 打“个人体验牌”，OpenHands 打“开发者平台牌”，LiteLLM 打“基础设施牌”，Temporal 打“可靠性牌”。四者恰好构成智能体生态从应用到基础设施的完整链路。


## 6. 社区热度与成熟度

**快速迭代阶段（高频发布/大量 PR 流动）**
- **LiteLLM** — 日 PR 349 条、双版本发布、合并效率 45%，处于功能密集输出期。但 v1.99.0 发布暴露供应链构建脆弱性（Wolfi python3.14 导致 uvloop 失败），提示速度之下工程韧性需加固。
- **Hermes Agent** — 日 PR 500 条、社区互动极强（458 条 Issue 更新），创新与回滚并行。Desktop E2E 测试反复禁用/启用说明 CI 基础设施尚未稳固，属于“高速扩张、基建追赶”阶段。

**质量巩固阶段（中低更新量、聚焦稳定性）**
- **Temporal** — 更新量中等，但 PR 集中于可靠性修复（worker 超时可配置、ContinueAsNew backoff 累积、竞态修复），并有 5+ 个 stacked PR 推进 Worker callbacks 特性。处于“稳中求进”状态。
- **OpenHands SDK** — 更新量偏低，但讨论高度集中（企业治理、技能管理 PRD），合并率仅 14% 且多个安全相关 PR 等待超 1.5 个月，提示审查带宽已成为发展瓶颈。处于“设计驱动、落地乏力”的风险窗口。

**数据缺失**
- **OpenClaw、Pi** — 今日无数据，无法评级。


## 7. 值得关注的趋势信号

**① 订阅 OAuth 直连将成为 Agent 商业化必答题**
Hermes 社区对 Claude Pro/Max 订阅直连的呼声以 👍 53 高居功能请求榜首，直接指向“双重付费”痛点。Agent 开发者应尽早规划 BYO-Subscription 模式，否则将被竞品以“零边际成本”策略收割用户。

**② 上下文计量与成本透明度将从“功能”变为“信任门槛”**
Hermes 修复上下文计量器虚高（850K→600K 的误读）、LiteLLM 流式计费数据丢失长期未决，两个方向本质同一：用户对不可解释的资源消耗正丧失耐心。提供精确、可审计的 Agent 成本/状态可视化，是建立用户信任的基础设施级要求。

**③ “持续性”成为 Agent 架构分水岭**
群聊在桌面关闭后停摆（Hermes）、fork 标题与 tags 语义混乱（OpenHands）、SQL 连接池故障导致集群“假活”（Temporal）——三个案例共同指向一个问题：智能体/工作流必须能在创建者离线、底层故障时依然正确运行。服务端权威状态 + 可恢复性是下一代架构的底线要求，而非可选项。

**④ 技能管理正站在结构性重构前夜**
OpenHands 发起的 Skills Management PRD 重思 + Hermes 的 Skills 索引自动监控报警，显示现有 Microagent 管理方式已落后于 AGENTS.md、Agent Skills 等新标准。谁先定义“下一代技能管理范式”，谁就掌握了智能体生态的事实标准权。

**⑤ 企业治理需求从“可选”走向“入场券”**
OpenHands #4273（治理层：文件控制/命令白名单/成本预算/审计证据）获得 13 条讨论，与秘密掩码缺失（1/13 工具）、密钥泄露等问题叠加，表明企业采购方对 Agent 的审计能力已设定最低门槛。面向 B 端的 Agent 项目应将治理内建于架构，而非事后补丁。

---

*报告基于 2026-09-02 GitHub 公开数据，部分项目数据截断导致覆盖不完整，仅供参考。*

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，这是 2026 年 9 月 2 日的 Hermes Agent 项目动态日报。

---

# Hermes Agent 项目动态日报 — 2026-09-02

## 1. 今日速览

过去 24 小时项目活跃度极高：共产生 458 条 Issue 更新（新开/活跃 360，关闭 98）和 500 条 PR 更新（待合并 401，已合并/关闭 99），无新版本发布。社区讨论焦点集中在**会话状态持久化与群聊架构**（#8457、#89995、#97681）、**订阅 OAuth 集成**（#25267，👍 53）以及**多个 P1 级稳定性问题**（#90837、#97948、#97963）。值得肯定的是，针对昨日出现的压缩/上下文计量回归（#97963、#97948），社区在 24 小时内即提交了对应修复 PR（#100633、#100621），响应速度很快。但需注意，今日有 3 个 PR 是围绕“重新禁用 Desktop E2E 测试”（#100722、#100720）的反复操作，CI 基础设施稳定性仍待加强。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日虽无 Release，但合并/关闭了多个关键 PR 和 Issue，主要推动了以下方向：

**核心稳定性修复（已合并/关闭）**
- **CLI 上下文计量器重大修复**：[#100621](https://github.com/NousResearch/hermes-agent/pull/100621) 修复了推理模型在 turn 边界处上下文计量器“虚高”问题。此前“850K → 600K”的陡然下降会被用户误读为压缩故障，现已改为显示持久化后的真实对话记录大小。
- **Desktop E2E 测试回滚**：[#100722](https://github.com/NousResearch/hermes-agent/pull/100722) 与 [#100720](https://github.com/NousResearch/hermes-agent/pull/100720) 将 #100453 重新启用的 Desktop E2E 车道再次禁用。该车道在 main 分支上 4/5 运行失败且不稳定，阻塞了所有 PR 合并。
- **多项历史顽固 Bug 关闭**：包括 Remote Gateway 会话恢复失败（[#93888](https://github.com/NousResearch/hermes-agent/issues/93888)）、macOS 下 Electron sandbox 导致桌面端静默崩溃（[#51327](https://github.com/NousResearch/hermes-agent/issues/51327)）、Windows 文件大小写冲突导致 git 状态永久脏（[#88168](https://github.com/NousResearch/hermes-agent/issues/88168)）、以及多个 Windows 更新失败问题（[#63717](https://github.com/NousResearch/hermes-agent/issues/63717)），说明维护者对 Desktop 跨平台问题做了一轮集中清理。

**新功能 / 架构推进（已合并/关闭）**
- **可选共享指标导出器（Telemetry Phase 2）**：[#95278](https://github.com/NousResearch/hermes-agent/pull/95278) 合入，为 Phase-1 遥测服务增加了 agent 端发送器，向 `telemetry.nousresearch.com` 发送每日指标包。
- **注册表驱动脱敏能力**：[#97383](https://github.com/NousResearch/hermes-agent/pull/97383) 合入，允许用户通过 JSON 模式文件注册自定义的敏感值/键格式，在现有脱敏边界生效。

整体来看，项目今日在“修复 + 回滚”上用力较多，新功能推进（遥测、脱敏）属于对既有架构的补全，没有出现跨里程碑级别的大特性合入。


## 4. 社区热点

- **Skills 索引持续退化警报（🔥 137 条评论）**：[#66616](https://github.com/NousResearch/hermes-agent/issues/66616) — `[skills-index-watchdog]` 机器人自动报告 Skills Hub 依赖的索引文件已 29.8 小时未更新（超过 26 小时限制），状态 `degraded`。高评论数说明社区对文档/索引自动化管道的健康度很关注，且在积极排查是 cron 定时任务、部署工作流还是存储问题。

- **自动化集成长期被阻塞（52 条评论）**：[#88584](https://github.com/NousResearch/hermes-agent/issues/88584) — `cron/jobs.py` 的合并冲突导致 Nous-to-Enterkey 的自动化集成停滞，dashboard 更新器停留在旧版本。这是一个跨仓库协作的阻塞性问题，持续两周未解决，社区讨论热烈。

- **Claude 订阅 OAuth 集成呼声最高（👍 53）**：[#25267](https://github.com/NousResearch/hermes-agent/issues/25267) — 用户希望用 Claude Pro/Max 订阅直接作为模型后端，而不是额外支付 API 费用。该需求在功能请求中情绪最强烈，且与另一个已关闭的 OAuth 计费坑（[#65365](https://github.com/NousResearch/hermes-agent/issues/65365)）直接相关，说明订阅用户对“双重付费”问题高度不满。

- **Bot 群聊能力讨论集中爆发**：多 Issue 指向同一课题——群聊目前是桌面端独有的、由前端渲染器驱动，且桌面关闭后群聊即停摆（[#89995](https://github.com/NousResearch/hermes-agent/issues/89995)、[#97681](https://github.com/NousResearch/hermes-agent/issues/97681)、[#95163](https://github.com/NousResearch/hermes-agent/issues/95163)）。三者从“Web 端暴露”“桌面关闭后持续运行”“后端权威托管”三个角度切入，说明这是一个社区关注度持续升温的架构级功能方向。


## 5. Bug 与稳定性

按严重程度排列：

**🔴 P1 — 严重 / 数据损坏风险（有修复 PR 或已关闭）**

- **state.db 反复损坏（11 次/18 天）**：[#90837](https://github.com/NousResearch/hermes-agent/issues/90837) — 仍 OPEN。生产网关 state.db 在 8 月 2 日至 20 日间损坏 11 次

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-09-02

## 1. 今日速览

过去 24 小时项目保持高热度的社区活跃度：**26 条 Issue 更新**（新开/活跃 16 条，关闭 10 条）与 **50 条 PR 更新**（待合并 43 条，合并/关闭 7 条），无新版本发布。安全与持久化类 Bug 成为今日焦点：**#4677 秘密掩码只覆盖 1/13 工具**与 **#4802 环境变量泄露**均涉及 secrets 治理且已在高优先级下关闭或修复推进；同时 **会话状态持久化** 成为新的反复主题（#4810、#4811、#4813、#4814），多个修复 PR 已就绪。整体项目健康度良好——PR 提交活跃度高但合并率偏低（7/50），提示审查积压需关注。

## 2. 版本发布

无。

## 3. 项目进展

今日共 7 条 PR 合并/关闭，虽未逐一披露合并明细，但从关联 Issue 的关闭状态及开启的修复 PR 可窥项目前进方向：

- **安全治理强化**：Issue #4802（`sanitized_env()` 泄露 OH_SECRET_KEY）与 #4677（秘密掩码缺失于 12/13 工具）均已关闭，配合 PR #4715（在工具咽喉点统一遮蔽已注册秘密）在推进，安全内核正在加固。
- **会话持久化修复**：PR #4813（`confirmation_policy`、`security_analyzer`、`secrets` 状态归属修正，针对 #4810）与 PR #4814（fork 标题改为存储于 `StoredConversation`，针对 #4811）已提交，直接回应昨日新报的 meta.json 持久化缺陷。
- **性能优化**：PR #4697 使 `EventLog.append` 成本与对话长度解耦（常数级），对长会话场景的高频写入是实质性改进。
- **模型兼容与工具链**：PR #4183 修复合加密 LLM 配置在子代理中未解密的问题；PR #4406 为 mcp 2.x 添加 Server 装饰器 shim，保障 browser_use 可构造。

项目在**安全、持久化、性能**三条主线同步推进，方向明确且修复及时。

## 4. 社区热点

| 排名 | 条目 | 评论数 | 类型 | 核心诉求 |
|------|------|--------|------|----------|
| 1 | [#4235 Add support for including screenshots in PRs](https://github.com/OpenHands/software-agent-sdk/issues/4235) | 19 | 功能增强 | 希望 OpenHands 在生成 PR 时能自动附带应用截图，便于审查者直观理解变更效果 |
| 2 | [#4242 Frontmatter field for multiple repos](https://github.com/OpenHands/software-agent-sdk/issues/4242) | 16 | 路线图 | 需要一种简便的方式在 frontmatter 中指定多个仓库并克隆 |
| 3 | [#4243 Re-thinking Skills Management](https://github.com/OpenHands/software-agent-sdk/issues/4243) | 16 | PRD 讨论 | 现有 Microagent 管理界面远落后于 AGENTS.md / Agent Skills 等新能力，需重新设计 |
| 3 | [#4273 Governance layer for agent actions](https://github.com/OpenHands/software-agent-sdk/issues/4273) | 13 | 功能增强 | 企业级文件访问控制、命令白名单、成本预算与审计证据需求 |
| 5 | [#3442 Intelligent Model Selection](https://github.com/OpenHands/software-agent-sdk/issues/3442) | 12 | 功能增强 | 期望“自动为我决定”的智能模型路由，免去用户记忆不同模型的成本与效果差异 |

**分析**：社区讨论集中在**企业级治理**（#4273）、**模型智能路由**（#3442）与**多模态支持**（#4235）三个方向。其中 #4235 与 #4242 均有 PR 关联（#4235 对应图片支持方向的多项 PR），表明讨论热度与代码进度同步；#4243 的 PRD 重思提示技能管理即将迎来结构性变更，值得关注后续设计文档。

## 5. Bug 与稳定性

| 严重度 | Issue | 状态 | 是否有修复 PR |
|--------|-------|------|---------------|
| 🔴 High | [#4677 Secret masking covers only 1 of 13 tools](https://github.com/OpenHands/software-agent-sdk/issues/4677) — 模型可通过 file_editor、grep 等 12 个工具读取明文密钥 | 已关闭 | ✅ #4715 |
| 🔴 High | [#4542 Global agent_context.load_memory ignored unless launched from agent profile](https://github.com/OpenHands/software-agent-sdk/issues/4542) — 全局偏好静默丢失，导致持久记忆不生效 | 开放 | ❌ 无 |
| 🔴 High | [#4802 sanitized_env() leaks OH_SECRET_KEY to subprocesses](https://github.com/OpenHands/software-agent-sdk/issues/4802) | 已关闭 | ✅（已关闭，修复可能已合入） |
| 🟡 Medium | [#4810 confirmation_policy / security_analyzer / secrets 变更未持久化到 meta.json](https://github.com/OpenHands/software-agent-sdk/issues/4810) — 重启后丢失 | 开放 | ✅ #4813 |
| 🟡 Medium | [#4709 current_datetime 持久化进 settings.json，导致 prompt 中时间戳陈旧](https://github.com/OpenHands/software-agent-sdk/issues/4709) | 开放 | ❌ 无 |
| 🟡 Medium | [#4811 fork 将标题注入 tags 而非专用字段](https://github.com/OpenHands/software-agent-sdk/issues/4811) | 开放 | ✅ #4814 |
| 🟢 Low | [#4800 In-memory mutation without rollback on save_meta() failure](https://github.com/OpenHands/software-agent-sdk/issues/4800) — 内存与磁盘状态不一致 | 开放 | ❌ 无 |

**今日 Bug 趋势**：`ConversationService` / `StoredConversation` 层的**持久化一致性**问题是今日新暴露的薄弱环节，三个独立 Bug（#4810、#4811、#4800）指向同一模块，好在其中两个已有修复 PR 待合入。安全类两个高优 Bug 均已关闭，但 #4542（记忆偏好静默丢失）仍无修复方案，涉及产品设计层面，建议维护者评估优先级。

## 6. 功能请求与路线图信号

今日新增/活跃的功能请求显示以下方向可能进入下一版本：

- **ACP 模型列表补全**（#4812，claude-fable-5 缺失）→ 已有对应 PR [#4815](https://github.com/OpenHands/software-agent-sdk/pull/4815)，大概率随下一个 minor 版本合入。
- **子对话服务端工具**（#4781，服务端启动同后端 child conversation）→ “ready-for-dev”标记，且超过 1 个开发者讨论，架构方向已明确。
- **Agent 镜像可裁剪化**（#4643，可选能力、参数化 provider、共享 eval 层）→ 步骤 0-2 已完成，是长期优化项。
- **Screenshots in PR**（#4235，有 19 条评论）→ 与 #4236（Better support for images）方向协同，多模态能力是社区长期高频诉求。
- **智能模型选择**（#3442）→ 若 #4704（路由异步补全走 RouterLLM）合入，将是该方向的基础设施铺垫。

## 7. 用户反馈摘要

从今日 Issue 与 PR 的人类作者（HUMAN）注释中提炼：

- **CLI 体验痛点**：#4237 指出 CLI 运行时（CLIRuntime）不支持浏览器功能，但 agent 仍会尝试浏览器动作，导致图片解析失败，浪费 token 且流程断裂。用户期望 CLI 专属 prompt 能剔除浏览器动作空间。
- **配置管理摩擦**：#4238 请求支持“禁用但保留”单个 secret，现有能力只有“全删或全留”，在轮换密钥场景下不够灵活。
- **默认值隐式修改的困扰**：PR #4372 的作者反馈“default agent profile 一直指向已切换走的 LLM profile，且没有任何提示”，希望系统只在用户未显式绑定时才同步默认值。
- **编码 heuristic 误判**：PR #4784 的作者建议优先尝试严格 UTF-8 解码，启发式检测仅在失败时回退，因为现有逻辑“偶尔产生乱码但对于大多数文本文件而言是不必要的冒险”。
- **fork 功能语义混乱**：#4811 指出 fork 时“标题被塞进 tags 字典”，用户侧看到的行为是标题与自定义标签混淆，且更新时需处理同步问题。

## 8. 待处理积压

| 条目 | 创建时间 | 备注 |
|------|----------|------|
| [#4235 支持 PR 附带截图](https://github.com/OpenHands/software-agent-sdk/issues/4235) | 2025-07-18 | 讨论已跨越 13 个月，19 条评论，无 assignee，仍是 highest-comment 功能请求 |
| [#4242 多仓库 frontmatter](https://github.com/OpenHands/software-agent-sdk/issues/4242) | 2025-12-07 | 9 个月未闭环，虽在 roadmap 但无具体时间表 |
| [#2053 Skills Epic（子代理执行/模型路由）](https://github.com/OpenHands/software-agent-sdk/issues/2053) | 2026-02-13 | Epic 级，追踪多个子任务，需要专人持续跟进 |
| PR [#3811 防御 __del__ 部分构造实例](https://github.com/OpenHands/software-agent-sdk/pull/3811) | 2026-06-20 | 等待时长超过 2 个月，修复一个真实的异常抑制场景，建议尽快 review |
| PR [#4183 子代理解密 LLM 配置](https://github.com/OpenHands/software-agent-sdk/pull/4183) | 2026-07-22 | 安全相关修复，已等待 1.5 个月，Fernet 密文被误用为 API key 问题值得优先处理 |
| PR [#4406 mcp 2.x Server shim](https://github.com/OpenHands/software-agent-sdk/pull/4406) | 2026-08-07 | 环境兼容性阻塞（browser_use 无法构建），上游建议尽快合入或给出替代方案 |

---

**项目健康度总结**：整体呈“高活跃、快响应、稳推进”状态，安全与持久化两条关键链路的问题被及时发现并有修复 PR 跟进；PR 合并率（14%）略低，且部分 PR 等待超两个月，审查带宽需补充。功能方向聚焦于企业治理、多模态与模型路由，与路线图信号一致。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-09-02

## 1. 今日速览

LiteLLM 项目今日活跃度处于**极高**水平：24 小时内共发生 87 条 Issue 更新与 349 条 PR 更新，并有 2 个新版本发布。其中 157 条 PR 被合并或关闭，处理效率较高，但仍有 192 条 PR 待合并，存在一定的积压压力。社区讨论焦点集中在**路由策略优化、计费数据准确性、安全隔离**三大方向，多个长期未修复的严重 Bug（如流式计费数据丢失 #14457）仍在持续发酵。整体来看，项目迭代速度快、社区参与度高，但部分关键稳定性问题的修复周期偏长，值得关注。

## 2. 版本发布

今日发布了两个版本：

| 版本 | 类型 | 说明 |
|------|------|------|
| [v1.101.0-dev.1](https://github.com/BerriAI/litellm/releases/tag/v1.101.0-dev.1) | 开发版 | 发布说明主要提及 Docker 镜像签名验证（cosign） |
| [v1.99.0](https://github.com/BerriAI/litellm/releases/tag/v1.99.0) | 正式版 | 发布说明同样以 Docker 镜像签名验证为主 |

**注意事项：** 两个版本的 Release Notes 均仅包含 cosign 镜像签名验证说明，未提供详细的功能变更列表。值得注意的是，PR [#39212](https://github.com/BerriAI/litellm/pull/39212) 中提到 v1.99.0 发布过程中曾因 Wolfi 仓库将 `python3` 解析为 3.14 导致 `uvloop 0.21.0` 构建失败，进而拖垮了 Docker 镜像构建流程。该问题已在 `stable/1.97.x` 分支通过固定 Python 版本修复（cherry-pick #38917），用户若在 1.99.0

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报（2026-09-02）

数据统计截至 2026-09-01 24:00（UTC），基于 GitHub 公开仓库 temporalio/temporal。

## 今日速览

过去 24 小时，Temporal 项目保持高活跃度：ISSUE 侧有 2 条更新（均为活跃状态，无关闭），PR 侧有 56 条更新，其中 12 条已合并/关闭，44 条待合并。更新集中于 **可靠性（reliability-2026）** 、**Worker/Nexus 回调** 及 **命名空间复制（CGS Foundation）** 等方向。无新版本发布。整体来看，项目正处于 **稳定性修复与中型功能开发并行** 的阶段，大量 PR 仍在评审或迭代中，合并速度略有放缓，但开发节奏稳定。

## 项目进展

今日有 12 个 PR 被合并/关闭，在可见数据中以下 4 个 PR 为 **CLOSED** 状态，代表了近期的落地成果：

- [#11863 [reliability-2026] Make worker commands timeout and max attempts configurable](https://github.com/temporalio/temporal/pull/11863)  
  将 `DispatchTimeout` 和 `MaxTaskAttempts` 从编译期常量改为动态配置（`WorkerCommandsDispatchTimeout` / `WorkerCommandsMaxAttempts`），让 Worker 命令超时与重试次数可在运行时调整，无需重新部署。默认值保持不变，便于后续按需调优。

- [#11839 [reliability-2026, release/1.32.0] Fix FirstWorkflowTaskBackoff Accumulation upon ContinueAsNew](https://github.com/temporalio/temporal/pull/11839)  
  修复了在 `ContinueAsNew` 时 `FirstWorkflowTaskBackoff` 不断累积的问题。此前若 workflow 在执行时间前继续 as-new，会导致计算出的生命周期为负，从而造成 backoff 无限增长。该修复已经合入 release/1.32.0 分支，对稳定性有实际意义。

- [#11852 Refactor Nexus dispatch result classification](https://github.com/temporalio/temporal/pull/11852)  
  重构前端 Nexus 代码中 `DispatchNexusTaskResponse` 的分类逻辑，提取可复用的 `DispatchNexusTaskResponse` 分类器，降低后续维护成本，并减少重复代码。

- [#11847 [reliability-2026] Restore linting for legacy HSM packages](https://github.com/temporalio/temporal/pull/11847)  
  移除了对 legacy HSM 包的临时 golangci-lint 排除规则，恢复标准 lint 检查，保证包移动后的代码质量门槛。

此外，部分开放 PR 也在今日获得更新，说明正在积极推进，例如：

- [#11884 Add namespace replication outcome metrics](https://github.com/temporalio/temporal/pull/11884)  
  为 legacy 命名空间元数据复制添加最终结果和端到端延迟指标，覆盖 `applied`、`no_change`、`not_admitted`、`terminal_failure` 等分类，便于观测复制链路的健康度。
- [#11887 Add single-cluster passive replication test harness](https://github.com/temporalio/temporal/pull/11887)  
  新增单集群被动复制测试框架，用于验证 active/passive 状态转移期间的任务负载一致性，属于可靠性测试基础设施的补充。

## 社区热点

由于数据中未提供 PR 的具体评论数，以下基于功能影响力和讨论热度判断：

- [#11691 SQL session refresh can close the connection pool irrecoverably ...](https://github.com/temporalio/temporal/issues/11691)  
  这是一个被标记为 OPEN 的严重 Bug 报告，描述了 SQL 会话刷新失败导致连接池不可恢复关闭，集群虽报告 SERVING 但实际无法调度任务。该 issue 有 1 条评论，且更新时间就在 9 月 1 日，反映出社区对数据面可用性的持续关注。

- Worker callbacks 系列 PR（如 [#11589](https://github.com/temporalio/temporal/pull/11589)、[#11567](https://github.com/temporalio/temporal/pull/11567)、[#11566](https://github.com/temporalio/temporal/pull/11566) 等）均为 stacked PR，目标合并到 `feature/worker-callbacks` 分支。虽然尚未进入 main，但这是一个较大的功能特性，社区对 callback 支持（尤其是 Worker 变体）的期待度较高，讨论分散在多个关联 PR 中。

- [#11851 Stop retrying timeout error when dispatching worker command](https://github.com/temporalio/temporal/pull/11851)  
  关注 Worker 命令调度在 poller 超时下不必要重试的问题。该 PR 指出当前 `DispatchNexusTask` 在 worker 消失时每次尝试会阻塞 goroutine 长达 10 秒，属于性能与资源浪费问题，容易在故障场景中被放大。

## Bug 与稳定性

按严重程度排列：

1. **严重：SQL 连接池不可恢复关闭，导致集群“假活”**  
   [#11691](https://github.com/temporalio/temporal/issues/11691)  
   现象：`sql: database is closed` 后，membership heartbeat 静默失败，集群无法派发任务但仍报告 SERVING。  
   影响：集群实际不可用，但监控无法感知，运维难以介入。  
   该问题仍在开放状态，目前没有对应的 fix PR，用户建议要么让 session refresh 恢复连接，要么让心跳失败升级为进程重启。

2. **中等：Worker 命令调度超时导致 goroutine 泄漏/阻塞**  
   [#11851](https://github.com/temporalio/temporal/pull/11851)  
   当 poller 超时（`UpstreamTimeout`）时不停止重试，导致每个 dispatch 调用阻塞 10 秒。PR 已提出停止重试该错误类型，传输错误仍按原逻辑重试，目前处于 OPEN 状态。

3. **中等：shutdown 期间 poll 未被取消的竞态问题**  
   [#11841 (Fix a race condition that can leave a poll to not get cancelled during shutdown)](https://github.com/temporalio/temporal/pull/11841)  
   修复了 shutdown cache 与 worker poll 注册之间的竞态，避免 poll 已启动但尚未注册时 shutdown 错过取消。该 PR 仍开放，但修复思路清晰。

4. **一般：Visibility SQL 查询转换器解析错误**  
   [#11801 (Fixes to Visibility SQL query converter)](https://github.com/temporalio/temporal/pull/11801)  
   修复 `ExecutionStatus IN (...)` 元组解析、负 double 值比较（如 `CustomDouble > -1.5`）、以及类型不匹配时未返回错误的问题。该 PR 仍开放，预计将提升 SQL 查询兼容性。

5. **一般：ContinueAsNew 导致 FirstWorkflowTaskBackoff 无限累积**  
   [#11839](https://github.com/temporalio/temporal/pull/11839)  
   已在今日合并至 release/1.32.0，属于已修复的回归问题。

## 功能请求与路线图信号

- **NexusHandler 回调反向链接（backlinks）**  
  [#11889 Support backlinks for NexusHandler callbacks](https://github.com/temporalio/temporal/issues/11889)  
  这是一个新提交的跟踪 issue，请求在 NexusHandler 变体回调派发时，为源操作的回调与 Nexus 操作产生的资源之间建立双向链接。目前尚未实现，但说明回调功能的可观测性/可追踪性已被提上议程。

- **Worker callbacks 功能的大规模上线准备**  
  多个 PR（[#11380](https://github.com/temporalio/temporal/pull/11380)、[#11520](https://github.com/temporalio/temporal/pull/11520)、[#11566](https://github.com/temporalio/temporal/pull/11566)、[#11567](https://github.com/temporalio/temporal/pull/11567)、[#11589](https://github.com/temporalio/temporal/pull/11589)）组成 stacked PR 集，正逐步汇聚到 `feature/worker-callbacks` 分支。这些改动涉及 `commonpb.Callback` 新变种、可配置回调类型、CallbackInfo.outcome 填充等。从 PR 描述看，该功能已进入代码完成阶段，可能成为下一个大版本的重要能力。

- **调度器 V1 版本上限动态评估**  
  [#11831 (feat: [Scheduler] re-evaluate V1 version ceiling per iteration)](https://github.com/temporalio/temporal/pull/11831)  
  当前调度器 workflow 使用静态的 `CurrentTweakablePolicies.Version`，该 PR 计划在每次迭代重新评估 V1 版本上限，使调度策略可以随动态配置调整。这是一个面向灵活性的改进，仍处于开放状态。

- **命名空间复制可观测性与被动复制测试**  
  [#11884](https://github.com/temporalio/temporal/pull/11884) 和 [#11887](https://github.com/temporalio/temporal/pull/11887) 分别从“生产指标”和“测试框架”两个维度支撑复制链路的可靠性，反映 Temporal 对跨集群运维场景的重视。

## 用户反馈摘要

- **SQL 连接池问题的用户痛点**（来自 [#11691](https://github.com/temporalio/temporal/issues/11691)）  
  用户明确指出：集群在无法派发任何任务时仍对外报告 `SERVING`，这意味着监控体系会产生“绿码”假象，故障被长期掩盖。用户期望的恢复方式是“要么会话刷新能自愈，要么心跳失败时主动杀进程让 supervisor 拉起”。这体现了对 **故障透明度和可恢复性** 的强烈需求。

- **对 Worker 命令超时重试的抱怨**（来自 [#11851](https://github.com/temporalio/temporal/pull/11851) 的 PR 描述）  
  开发者指出：当 worker 已不存在时，`DispatchNexusTask` 每次尝试都会阻塞 10 秒，导致 goroutine 堆积。这属于“失败场景下的资源浪费”，虽然不直接影响正确性，但在大规模 worker 波动时会影响前端稳定性。

- **回调功能的开发者期待**（来自多个 stacked PR 描述）  
  社区正在推进 Worker-variant callbacks，开发者对回调类型可配置、回调结果可查询（CallbackInfo.outcome）有明确需求，这些 PR 的密集出现说明该功能已从“实验性”走向“产品化”。

## 待处理积压

以下长期未合并或未关闭的 PR/Issue 值得维护者关注：

- **Worker callbacks 系列 PR（自 2026-07-31 起）**  
  包括 [#11380](https://github.com/temporalio/temporal/pull/11380)、[#11520](https://github.com/temporalio/temporal/pull/11520)、[#

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*