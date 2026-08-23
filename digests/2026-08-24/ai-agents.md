# OpenClaw 生态日报 2026-08-24

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-23 22:42 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-24

## 今日速览

过去 24 小时项目保持**极高活跃度**：累计 500 条 Issue 更新（451 条新开/活跃、49 条关闭）与 500 条 PR 更新（388 条待合并、112 条已合并/关闭）。暂无新版本 Release，但 PR 侧出现 15+ 个新提交，集中在 Control UI 优化、发布流程修复与 ACPX/MCP 安全边界等领域。值得关注的是，一个 **P0 级 SQLite 数据损坏问题**（#126821）在 beta.2 上复发（5 天内 5 次事件），社区讨论热度与维护者响应均处于高位。整体来看，项目在密集迭代 beta 版本的同时，稳定性问题仍是当前最主要矛盾。

## 版本发布

今日无新版本发布。当前最新版本为 **2026.8.1-beta.2**，发布验证 Issue（#125626）仍在进行中，beta.3 的发布流程与聚焦验证证据相关 PR 正在推进（#128371、#128391）。

## 项目进展

今日共 **112 个 PR 被合并/关闭**，其中值得注意的已合并工作：

- **安全策略确认机制落地**：#116489（`feat(security): require acknowledgement for install policy warnings`）要求外部 `security.installPolicy` 命令返回 `warn` 时，操作者必须显式确认才能继续安装有风险的插件/技能；配套的 UI 层实现 #120900 已合并，管理员可在 Control UI 中审查安装策略警告并选择继续。
- **发布流程修复**：#128371 解决了 beta.3 发布阻塞——当冻结候选仅变更了已审查的 Slack 测试且失败记录已被重跑通过时，发布者仍只接受全量验证清单，该 PR 授权了聚焦式 beta 证据提交。
- **OAuth 保留修复**：#125471 修复 Claude CLI OAuth 在 Gateway 重启后可能丢失刷新所有权的问题，使 Control UI 中保持 Claude CLI OAuth 可用。
- **性能与稳定性小幅优化**：#128392 消除了 Matrix 出站路径上重复的 Markdown→Matrix 文本投影；#123975 为 `tsgo` 编译包装器增加超时看门狗与信号清理，避免卡死的编译器进程树。

此外，两个被标记为 `close:superseded` 的 PR（#111155 背景图像生成保持会话 OAuth、#110529 memory-core 429 率限退避）已被更完善的后续方案取代，说明维护团队在持续收敛旧方案。

## 社区热点

今日评论最活跃的 Issue 集中反映了**数据一致性与消息送达可靠性**两大主题：

- **#125626 Release validation: v2026.8.1-beta.2**（18 评论，[链接](https://github.com/openclaw/openclaw/issues/125626)）——发布验证协同贴，多位测试者通过验证技能提交测试结果，属于例行发布流程热点。
- **#119796 Windows: vitest teardown fails with EBUSY**（15 评论，[链接](https://github.com/openclaw/openclaw/issues/119796)）——Windows 平台上 agent 状态数据库文件句柄未释放导致测试 teardown 失败。该 Issue 已关联修复 PR，揭示了 Windows 平台在文件锁语义上的兼容债。
- **#121953 Cron agent stalls on DeepSeek**（13 评论，[链接](https://github.com/openclaw/openclaw/issues/121953)）——OpenClaw 为 cron 任务消息添加 `[cron:<jobId> <name>]` 前缀，但 DeepSeek API 边缘节点将此前缀的请求从低优先级队列服务，导致数十秒至数分钟的停顿。社区围绕"治理前缀是否应作为用户可见内容"展开讨论。
- **#39476 A2A sessions_send 双向调用产生重复消息**（12 评论，[链接](https://github.com/openclaw/openclaw/issues/39476)）——3 月提出至今仍开放，涉及会话状态与消息去重，属于多代理交互的基础架构问题。

PR 侧今天的社区热点是 **#128380 ACPX 环境变量 SecretRefs 修复**（[链接](https://github.com/openclaw/openclaw/pull/128380)），该 PR 同时被标记为兼容性/安全边界/可用性三重合并风险，反映了 ACPX 作为扩展协议在安全配置上的敏感性。

## Bug 与稳定性

今日 Issue 中 Bug 类占比高。按严重程度排列如下：

**P0 级**

- **#126821 SQLite 损坏在全新重建的数据库上 15–24 小时内复发**（[链接](https://github.com/openclaw/openclaw/issues/126821)）——2026.8.1-beta.2 + WSL2 环境，5 天内 5 次事件，包括 `freelist miscount` 和"瘫痪的网关"模式（拒绝所有服务但进程不退出）。涉及 `data-loss` 与 `crash-loop`，目前无 fix PR，需 maintainer 决策。这是当前最严重的稳定性问题。

**P1 级（已有 fix PR 或已在修复中）**

- **#127710 prepared-model-runtime 因瞬时 generation 变更而永久卡死**（[链接](https://github.com/openclaw/openclaw/issues/127710)）——生产环境多代理网关（25 个 agent）两天内出现两种消息丢失模式，指纹漂移使网关永久故障，owner-commit 竞争导致消息静默丢弃。已有相关修复 PR。
- **#126311 Fallback model 在主模型终端错误后继续运行**（[链接](https://github.com/openclaw/openclaw/issues/126311)）——子代理运行的主模型返回 `server_is_overloaded` 后，fallback 模型

---

## 横向生态对比

# AI 智能体开源生态横向对比分析报告

**分析日期：2026-08-24**
**覆盖项目：OpenClaw、Hermes Agent、OpenHands SDK、Pi、LiteLLM、Temporal**

---

## 1. 生态全景

个人 AI 助手与自主智能体生态正处于**从原型验证向生产级基础设施演进的关键阶段**。OpenClaw 的极高迭代密度（单日 500 条 Issue + 500 条 PR 更新）与 LiteLLM 的双版本发布节奏表明，头部项目正加速冲刺功能完备性；与此同时，SQLite 数据损坏、任务投递一致性、消息重复等基础可靠性问题的集中爆发，揭示行业已越过"能否运行"进入"能否可信运行"的深水区。安全权限治理（安装策略确认、凭据覆盖防护、SecretRefs 修复）在多个项目中同步涌现，显示企业级采纳的压力正在倒逼安全边界补全。整体生态呈现**功能高速迭代、稳定性债待偿、安全治理加速补课**的三线并行态势。

---

## 2. 各项目活跃度对比

| 项目 | Issue 动态 | PR 动态 | Release | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 500 条更新（451 新开/活跃，49 关闭） | 500 条更新（388 待合并，112 合并/关闭） | 无（beta.2 验证中，beta.3 筹备中） | ⚠️ 极高活跃，但 P0 数据损坏问题复发，稳定性承压 |
| **Hermes Agent** | 数据缺失 | 数据缺失 | 数据缺失 | — 无法评估 |
| **OpenHands SDK** | 数据缺失 | 数据缺失 | 数据缺失 | — 无法评估 |
| **Pi** | 48 条更新（46 关闭，仅 2 新增） | 16 条更新（13 合并/关闭，3 待合并） | 无 | ✅ 高活跃，需求响应闭环速度快，积压少 |
| **LiteLLM** | 41 条更新（32 新开/活跃） | 143 条更新（99 待合并，44 合并/关闭） | 2 个（v1.98.0 稳定版 + v1.99.0-rc.1） | ⚠️ 高活跃，安全修复响应快，但长尾 Bug 积压明显 |
| **Temporal** | 1 条新 Issue | 28 条更新（9 合并/关闭，19 待合并） | 无（1.32.0 发布分支已准备） | ✅ 稳健推进，处于功能收尾与质量巩固期 |

> **注**：Hermes Agent 与 OpenHands SDK 未提供今日动态数据，无法纳入对比分析。

---

## 3. OpenClaw 在生态中的定位

### 3.1 核心定位：个人 AI 助手的"运行时底座"

OpenClaw 已从单一助手工具演化为**具备多代理网关能力、插件/技能生态、Control UI 管理面、ACPX/MCP 扩展协议**的综合性智能体平台。其社区规模与技术覆盖面在同赛道中处于明显领先地位——单日 PR 合并量（112 个）即超过 Pi 全月水平（13 个/日）与 LiteLLM（44 个/日）之和的 2 倍以上。

### 3.2 差异化优势

| 维度 | OpenClaw | 可对比项目 |
|---|---|---|
| **定位层级** | 智能体运行时 + 网关 + 生态平台 | Pi（单机 TUI 助手）、LiteLLM（模型网关中间件） |
| **架构复杂度** | 多代理编排、cron 任务、A2A 会话、插件安全策略 | Pi 为单体 TUI 架构，LiteLLM 为无状态代理层 |
| **扩展协议** | ACPX/MCP 双协议支持，安全边界持续加固 | Pi 有插件系统，LiteLLM 有 pass-through 前缀，无独立协议 |
| **管理与可观测性** | Control UI（安装策略审查、OAuth 管理、预算窗口） | LiteLLM 有 UI 与预算功能，Pi 仅 TUI |
| **迭代阶段** | beta 密集迭代，版本验证流程完善 | Pi 已相对稳定，LiteLLM 已进入 v1.98 稳定版序列 |

### 3.3 技术路线差异

OpenClaw 选择**"大而全"的平台化路线**：将模型路由、代理编排、安全策略、UI 管理、发布验证全部纳入核心仓库，以高维护成本换取一体化体验。这与其主要参照系——Pi 的"小而精"终端路线（聚焦单用户、TUI 高效交互、插件机制）形成鲜明对比。两者其实服务不同场景：OpenClaw 定位于"个人 AI 基础设施"，Pi 定位于"极客效率工具"。

---

## 4. 共同关注的技术方向

### 4.1 流式响应处理的健壮性（涉及：OpenClaw、Pi、LiteLLM）

| 具体问题 | 涉及项目 | 诉求 |
|---|---|---|
| 流式事件重复（`message_start` 重复） | LiteLLM #33859 | 协议层去重与容错 |
| 流式错误被静默吞掉 | Pi #8509 | 错误透传与类型保真 |
| 工具调用参数在流式中丢失 | Pi #8504、#8527 | 语义完整性保障 |
| 流式 chunk 缺失字段导致 500 | LiteLLM #34382 | 容忍非标准响应 |

**信号**：随着模型 API 多样化，流式协议已成为系统脆弱性的集中爆发点，各项目均在补强容错能力。

### 4.2 安全与权限边界治理（涉及：OpenClaw、LiteLLM）

- **OpenClaw**：#116489 安装策略警告需显式确认（已合并）；#128380 ACPX 环境变量 SecretRefs 修复（三重风险标记）。
- **LiteLLM**：#38033 非管理员覆盖 config 凭据（已有 fix PR #38034）；#21540 空列表权限语义分歧。

**信号**：从"能跑通"到"能管住"是生态的共性演进方向，权限模型与凭据管理成为企业部署的卡点。

### 4.3 平台兼容性——Windows 支持（涉及：OpenClaw、Pi）

- **OpenClaw** #119796：Windows 文件句柄未释放导致测试失败（EBUSY）。
- **Pi** #8523、#8183、#8372：Windows 盘符路径补全缺口、键位冲突、PowerShell 工具诉求。

**信号**：Windows 用户占比可观，但底层差异（文件锁、按键映射、Shell 语义）导致的兼容性债务正在显性化。

### 4.4 自托管/本地模型生态整合（涉及：Pi、LiteLLM、OpenClaw）

- **Pi**：llama.cpp 未加载模型列表可见性修复（#8535/#8479），本地推理集成加深。
- **LiteLLM**：时间/峰谷定价（#31606/#31725）、Gigachat 供应商支持（#25886）。
- **OpenClaw**：DeepSeek 边缘节点对 cron 前缀消息低优先级处理（#121953）。

**信号**：多模型不再是可选项而是默认态，且从"能用"进化到"精准管控成本与行为"。

### 4.5 可观测性与健康度排障（涉及：Temporal、LiteLLM、OpenClaw）

- **Temporal**：OTEL 遥测合入、historyScannerRPS 独立限流。
- **LiteLLM**：预算窗口用量展示（#37044）、导入性能（#7605）。
- **OpenClaw**：Control UI 优化持续迭代。

**信号**：生产环境下，用户对"黑盒不可接受"的诉求高度一致。

---

## 5. 差异化定位分析

| 维度 | **OpenClaw** | **Pi** | **LiteLLM** | **Temporal** |
|---|---|---|---|---|
| **功能侧重** | 完整智能体生命周期（编排、执行、管理、扩展） | 终端优先的交互式编码/任务助手 | AI 模型网关（路由、预算、安全、管理） | 分布式工作流/任务编排引擎 |
| **目标用户** | 个人 AI 基础设施使用者（Power User/开发者） | 极客开发者、TUI 爱好者、本地模型用户 | 企业平台/Infra 团队、LLM 应用开发者 | 后端工程师、平台团队 |
| **技术架构** | 多代理运行时 + Gateway + UI + 插件生态 | 单体应用 + TUI + 插件/扩展事件模型 | 轻量代理层 + Redis 状态 + UI Dashboard | 有状态分布式系统（Persistence + Frontend/History） |
| **AI 原生程度** | 极高（AI 是核心，一切围绕智能体） | 高（AI 交互是主要入口） | 中（AI 是转发对象，自身核心不依赖 AI） | 低（通用 Durable Execution 引擎，与 AI 无绑定） |
| **当前阶段** | Beta 密集迭代，稳定性是主线矛盾 | 稳定演进，需求闭环效率高 | 稳定版 + RC 并行，长尾 Bug 待清 | 接近 1.32.0 发布，功能收尾 + 质量巩固 |
| **独特标识** | 安全策略确认机制、ACPX/MCP 协议 | 扩展事件模型（user_bash_complete 等）、llama.cpp 深度集成 | 预算/峰谷定价、Provider 兼容适配层 | Worker-variant Callbacks、时间跳过、MySQL SRV 支持 |

---

## 6. 社区热度与成熟度

### 6.1 分层矩阵

| 层级 | 项目 | 判断依据 |
|---|---|---|
| **超高频迭代期** | **OpenClaw** | 日更新量级千级（Issue+PR），beta.2 验证中，P0 复发但社区响应高位，属于功能冲刺 + 稳定性攻坚并行阶段 |
| **高频迭代/生态扩展期** | **LiteLLM** | 双版本发布节奏，PR 池大（99 待合并），版本号已到 v1.98/1.99，说明进入功能井喷期，但长尾问题同步积累 |
| **稳态演进期** | **Pi** | 单日 46 Issue 关闭、13 PR 合入，响应速度快，无明显 P0/P1 积压，处于质量打磨与体验优化阶段 |
| **发布准备期** | **Temporal** | 新 Issue 极少，多个长线 PR 集中关闭（Callbacks、OTEL），发布分支已创建，进入版本冻结前收敛阶段 |

### 6.2 社区响应速度对比

- **最快闭环**：Pi —— llama.cpp 模型列表问题从报告（#8167）到修复合并（#8535/#8479）在当日完成，`ryanabx` 数小时从需求到实现。
- **快速修复**：LiteLLM —— 高危凭据覆盖 Bug（#38033）当日即出现 fix PR（#38034）。
- **响应及时但积压矛盾**：OpenClaw —— 大量 PR 待合并（388 个），发布验证和 P0 修复高度活跃，但合并吞吐仍有瓶颈。
- **深度优化**：Temporal —— 一致性边界问题（#11733）当日即获修复 PR（#11734），长线功能按部就班推进。

---

## 7. 值得关注的趋势信号

### 7.1 可靠性成为生态的"生死线"

OpenClaw 的 SQLite 数据损坏（5 天 5 次）与 Temporal 的任务投递歧义，虽分属不同架构层级，但共同指向**持久化与一致性问题已成为分布式 AI 系统最大风险点**。具有长时间运行、自动重试、异步回调特征的 AI Agent 系统，正在重走分布式系统十年走过的路——对开发者而言，选用具备**事务性、可恢复性**的底层（如 Temporal 的 Event Sourcing，或 OpenClaw 正在完善的 SQLite 修复策略）将成为决策关键。

### 7.2 安全治理从"加分项"变为"准入门槛"

三个独立项目在同一日推进安全相关修复（OpenClaw 安装策略确认、LiteLLM 凭据覆盖防护、ACPX SecretRefs），说明**企业采购/自部署的安全审计需求已传导至开源社区**。AI 智能体的插件安装、凭据管理、工具调用权限，将逐步向

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

# Pi 项目动态日报 — 2026-08-24

## 今日速览

过去24小时内 Pi 项目保持高度活跃：共 48 条 Issue 更新，其中 46 条已关闭、仅 2 条新增开放；PR 侧 16 条更新，13 条已合并/关闭，3 条待合并。值得注意的是，今日提交的 Issue 绝大多数为 `[untriaged]` 标签，且多为 Bug 报告和较小功能请求，反映出社区反馈量较大但项目维护者响应迅速。当前有 3 个 PR 处于开放状态，集中在 TUI 鼠标事件、PowerShell 工具和 markdown transformer 扩展。无新版本发布。

---

## 版本发布

今日无新版本发布。

---

## 项目进展

过去24小时内有 13 个 PR 被合并/关闭，大部分为 bug fix 和小的功能改进，涵盖模型兼容性、工具稳定性、TUI 行为和文档修正。

### 已合并/关闭的重要 PR

| PR | 描述 | 关联 Issue |
|---|---|---|
| [#8536](https://github.com/earendil-works/pi/pull/8536) | **修复严格 OpenAI 兼容提供商的 tool-result 历史规范化**。解决了 Moonshot/Kimi（kimi-k3, kimi-k2）重放会话历史时因消息顺序严格校验而报 400 的问题 | #8537 |
| [#8532](https://github.com/earendil-works/pi/pull/8532) | **修复 grep/find 工具子进程输出导致父进程崩溃**。readline 无行长限制，超长行会抛出 RangeError | — |
| [#8513](https://github.com/earendil-works/pi/pull/8513) | **修复 edit 工具中字符串化参数包含未转义控制字符**的问题（#3370 的后续补漏） | #8521 |
| [#8509](https://github.com/earendil-works/pi/pull/8509) | **修复流式 API 错误被静默吞掉以及不支持工具模型**的异常处理问题 | #8499, #8541 |
| [#8505](https://github.com/earendil-works/pi/pull/8505) | **为 agent 外层重试循环添加可配置的最大退避延迟** `retry.maxAgentDelayMs` | — |
| [#8500](https://github.com/earendil-works/pi/pull/8500) | **plan-mode 扩展中 bash 守卫和计划提取的误报消除** | — |
| [#8487](https://github.com/earendil-works/pi/pull/8487) | **暴露 finish reason 兼容性覆写**，补齐 API 类型定义 | #8460 |
| [#8482](https://github.com/earendil-works/pi/pull/8482) | **修正 custom footer 文档**，指向 `ctx.getContextUsage()` | #8392 |
| [#8535](https://github.com/earendil-works/pi/pull/8535) | **为 llama.cpp 增加未加载模型显示在 `/model` 列表**中的功能 | #8539, #8167 |
| [#8479](https://github.com/earendil-works/pi/pull/8479) | **修复 expose unloaded llama.cpp presets**（相关 PR） | #8167 |
| [#8524](https://github.com/earendil-works/pi/pull/8524) | **修复交互式 "Working..." 指示器在 agent_settled 回调完成前就消失**的问题 | — |
| [#8424](https://github.com/earendil-works/pi/pull/8424) | **修复失败扩展工厂的状态清理**，防止事件总线泄漏 | — |

整体来看，今日合入的 PR 集中在提高稳定性（防止进程崩溃、错误吞没、状态不一致）、兼容性（llama.cpp、严格 OpenAI 提供商、Windows）和开发者体验（退避延迟可配置、文档修正）三个方向。

### 仍开放的 PR（值得关注）

- [#8032](https://github.com/earendil-works/pi/pull/8032) — TUI 组件鼠标事件支持（持续活跃中，对应 #7683）
- [#8512](https://github.com/earendil-works/pi/pull/8512) — 可选的 PowerShell 工具，解决 Windows 路径处理问题
- [#7952](https://github.com/earendil-works/pi/pull/7952) — 为 markdown transformer context 添加 messageId 和 timestamp

---

## 社区热点

### 评论最多的 Issue

| Issue | 评论数 | 状态 | 摘要 |
|---|---|---|---|
| [#7683](https://github.com/earendil-works/pi/issues/7683) | 11 | 已关闭 | 提出让 TUI 组件能接收其自身行上的鼠标事件（已有 PR #8032 闭合并即将合入） |
| [#8167](https://github.com/earendil-works/pi/issues/8167) | 10 | 已关闭 | **bug**——内置 llama.cpp 支持无法在模型列表中看到模型选项（已通过 #8535/#8479 解决） |
| [#7885](https://github.com/earendil-works/pi/issues/7885) | 7 | 已关闭 | npm search 无法索引新发布的 pi-packages，导致包无法出现在 pi.dev/packages 画廊 |
| [#5932](https://github.com/earendil-works/pi/issues/5932) | 7 | **仍开放** | 请求在 ExtensionContext 上暴露 `ctx.navigateTree()`（已获 👍 ×2） |

**热点分析**：今日最热的三条 Issue 均针对**功能落差**——组件鼠标事件（#7683）、llama.cpp 模型可见性（#8167）、npm 生态集成（#7885）。其中 #7683 和 #8167 已经形成完整闭环：Issue 报告 → PR 提交 → 合并。这表明维护者对这些方向的优先级较高。相对而言，#5932 是较长时间未关闭的扩展 API 请求（6月21日创建至今），虽然评论不多但已有 👍，说明扩展开发者对更完整的 ExtensionContext API 有持续诉求。

### 讨论集中点

- **Windows 支持与键位冲突**：多条 Issue 围绕 Windows Terminal 的键位冲突（#8183, #8372），社区对 Windows 平台的优化有明确需求。
- **模型兼容性**：多起报告针对 OpenAI-compatible 提供商的严格校验问题（#8537, #8541, #8504），反映 Pi 用户使用的模型生态远比官方支持列表更广泛。

---

## Bug 与稳定性

今日报告的 Bug 密度较高，但多数为 `[untriaged]`，且有多项已有对应修复 PR。按严重程度排列如下：

### 高严重度

| Issue | 描述 | 状态 |
|---|---|---|
| [#8531](https://github.com/earendil-works/pi/issues/8531) | **自动重试在连续 "Request timed out" 后静默停滞，会话无限挂起**（RPC 模式下） | ❌ 无对应 PR |
| [#8525](https://github.com/earendil-works/pi/issues/8525) | **Abort 导致 SessionManager leaf 状态陈旧，后续工具结果被误配到错误的 parentId**，恢复会话时出现工具结果无对应工具调用的不一致 | ❌ 无对应 PR |
| [#8528](https://github.com/earendil-works/pi/issues/8528) | **agent 输出的尾随空格被复制并保留**（`Markdown.render()` 每行填充到终端宽度导致） | ❌ 无对应 PR |

### 中严重度

| Issue | 描述 | 状态 |
|---|---|---|
| [#8526](https://github.com/earendil-works/pi/issues/8526) | **Vertex AI 数组包裹的错误响应体被丢弃**，导致 "(no body)" 文本错误触发上下文溢出压缩 | ❌ 无对应 PR |
| [#8527](https://github.com/earendil-works/pi/issues/8527) | **`response.function_call_arguments.done` 事件的 `arguments` 可能为 undefined**，引发 TypeError（openai-responses 流式） | ❌ 无对应 PR |
| [#8521](https://github.com/earendil-works/pi/issues/8521) | **edit 工具字符串化 edits 中的原始控制字符仍导致校验失败** | ✅ 已有 PR #8513 合并 |
| [#8504](https://github.com/earendil-works/pi/issues/8504) | **openai-completions 中空 `custom:{}` 导致工具调用被误路由到自定义工具路径**，真实参数被丢弃 | ❌ 无对应 PR |
| [#8537](https://github.com/earendil-works/pi/issues/8537) | **Kimi 重放会话历史时出现孤儿 tool 消息、交错 user 消息、重复 tool_call_id** | ✅ 已有 PR #8536 合并 |

### 低严重度（体验/兼容性）

| Issue | 描述 | 状态 |
|---|---|---|
| [#8523](https://github.com/earendil-works/pi/issues/8523) | **Windows 上 @ 文件自动补全不支持盘符绝对路径**（`@C:/...`） | ❌ 无对应 PR |
| [#8529](https://github.com/earendil-works/pi/issues/8529) | **todo 工具 toggle 非幂等**，重复调用会静默取消已完成状态 | ❌ 无对应 PR |
| [#8541](https://github.com/earendil-works/pi/issues/8541) | **Nous Ox Alpha 的 429 错误被表面为泛化 "ERROR"** | ✅ 已有 PR #8509 修复相关错误处理 |

**趋势判断**：今日 bug 报告集中在流式响应处理（#8504, #8527, #8541）、会话一致性与重放（#8525, #8537）、以及平台兼容性（#8523）三个方面。除少量已有对应修复外，其余尚未被维护者分配或回复，可能存在一定的响应延迟风险。

---

## 功能请求与路线图信号

### 值得关注的新功能请求

| Issue | 内容 | 预计纳入可能性 |
|---|---|---|
| [#8533](https://github.com/earendil-works/pi/issues/8533) | 为扩展提供一个**窄范围的 Skill 可见性 API**（deny-only），允许扩展隐藏被发现的 Skill | 可能性中——API 设计方向与现有扩展体系吻合，但需要进一步设计讨论 |
| [#8457](https://github.com/earendil-works/pi/issues/8457) | **允许 Skill 像 prompt template 一样在句子中间调用**（`/name args` 在第一行之后展开） | 可能性中——与已在 0.84 中实现的 template 内联展开一致，设计意图清晰 |
| [#8530](https://github.com/earendil-works/pi/issues/8530) | 新增 "user_bash_complete" 扩展事件，在 bang 命令完成时通知（成功/失败/取消） | 可能性中——API 可扩展性需求，实现简单 |
| [#8344](https://github.com/earendil-works/pi/issues/8344) | TUI 中每个工具输出块支持**独立的鼠标展开/折叠**（保留 `Ctrl+O` 全局操作） | 已标记 no-action——可能因 #7683 的鼠标事件支持已在路线图中 |
| [#8332](https://github.com/earendil-works/pi/issues/8332) | 暴露 Codex **可选上下文上限**（`maxContextWindow: 872000`）作为信息性元数据 | 已标记 no-action |

### 与现有 PR 相关的功能信号

- **llama.cpp 模型管理**：`/model` 列表显示未加载模型这一功能请求（#8539）已通过 #8535 PR 快速落地，用户 `ryanabx` 从提出到实现仅用数小时，说明社区从需求到代码的闭环效率很高。
- **Windows 生态改善**：PR #8512（PowerShell 工具）表明维护者对 Windows 用户的体验问题在积极尝试解决方案，但作者 `mitsuhiko` 表示"需要更多尝试"，可能不会很快合并。

---

## 用户反馈摘要

### 真实用户痛点

1. **Windows 键位冲突高频出现**（#8183, #8372）：两条独立 Issue 报告了 Windows Terminal 中 `Ctrl+Shift+F` 与全屏转录搜索的冲突，用户 `petrroll` 建议 Pi 为 Windows 平台做特殊键位处理，但理解 Pi 无法针对每个平台特殊化。说明 Windows 仍是 Pi 体验最薄弱的环境。

2. **模型生态兼容性是持续痛点**：多起报告围绕 OpenAI-compatible 提供商在严格消息顺序校验、错误处理、流式响应方面的兼容问题（#8537, #8541, #8504）。用户 `wulong-t` 甚至会针对 Moonshot/Kimi 的特殊行为编写 PR 进行修复，反映出活跃的社区贡献氛围。

3. **扩展 API 不完整**：`@ayushdecoded` 在 #5932 中表示正在开发自定义 `/goal` 实现，但受限于 `navigateTree()` 不在 ExtensionContext 上而受阻。

4. **npm 包发现机制失效**（#7885）：包作者 `hellokidder` 发布 `pi-affix-prompt` 后无法通过 npm search 找到，导致 pi.dev/packages 列表中缺失。此问题影响依赖 npm 搜索索引的包分发生命周期，如果持续存在将打击第三方生态。

### 用户满意点

- 多条先前提出的问题（#7683, #8167, #8539）在短时间内通过 PR 合并得到了解决，体现了较高的需求响应积极性。
- `llama-server` 预设加载机制（#8479）让用户能按需延迟加载模型，替代原先需要手动 `/llama` 加载的繁琐流程。

---

## 待处理积压

### 长期未关闭的 Issue

| Issue | 创建时间 | 更新时间 | 标签/状态 | 备注 |
|---|---|---|---|---|
| [#663](https://github.com/earendil-works/pi/issues/663) | 2026-01-12 | 2026-08-23 | 已关闭但持续 7 个月 | `/share` 继承环境 `GITHUB_TOKEN` 的凭据问题。昨日有评论活跃，最终被关闭但没有看到相关修复 PR——建议维护者确认是否真正解决 |
| [#5932](https://github.com/earendil-works/pi/issues/5932) | 2026-06-21 | 2026-08-23 | `[to-discuss, new-harness]`, 👍 ×2 | 请求扩展 ExtensionContext API，已开放 2 个月，仍在讨论阶段 |
| [#7724](https://github.com/earendil-works/pi/issues/7724) | 202

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 (2026-08-24)

## 1. 今日速览

LiteLLM 项目保持非常活跃的社区迭代节奏。过去 24 小时共有 41 条 Issue 更新和 143 条 PR 更新，新开/活跃 Issue 32 条、待合并 PR 99 条，说明社区贡献者参与度极高。今日发布了 2 个版本（v1.98.0 稳定版与 v1.99.0-rc.1 候选版），但发布说明未披露具体变更内容。值得关注的是，今日有多个涉及安全与权限的 Issue 被提出，且社区已迅速贡献了对应修复 PR，反映出项目的响应速度较快。

## 2. 版本发布

过去 24 小时发布了 2 个新版本：

- **[v1.98.0](https://github.com/BerriAI/litellm/releases/tag/v1.98.0)** — 新稳定版
- **[v1.99.0-rc.1](https://github.com/BerriAI/litellm/releases/tag/v1.99.0-rc.1)** — 新候选发布版

> ⚠️ **注**：两个版本的 Release Notes 仅包含 Docker 镜像 cosign 签名验证说明，未附带代码变更日志。建议关注后续补发的更新内容。

---

## 3. 项目进展

今日共合并/关闭 44 条 PR，以下为实质性变更（按关注度排序）：

- **[fix: duplicate message_start in anthropic responses stream wrapper (#33859)](https://github.com/BerriAI/litellm/pull/33859)** — 修复 Anthropic Responses 流式响应中重复 `message_start` 事件的问题，对依赖事件驱动流式解析的开发者有直接受益
- **[feat: add show budget window usage (#37044)](https://github.com/BerriAI/litellm/pull/37044)** — 为 UI 增加预算窗口用量展示，改善多租户场景下资源可观测性
- **[fix(key_management_endpoints.py): allow team/org admins to update team member keys (#38035)](https://github.com/BerriAI/litellm/pull/38035)** — 修复团队管理员更新成员密钥时被 403 拒绝的问题，**注意**该 PR 已被关闭（可能合并或另有方案）
- **[fix: tolerate stream chunks without a choices key in stream_chunk_builder (#34382)](https://github.com/BerriAI/litellm/pull/34382)** — 增强流式构建容错能力，修复 Responses API 模型经 `/chat/completions` 转发时的 500 崩溃

总体评估，今日合并的 PR 集中在流式处理容错、权限模型完善和 UI 可观测性三个方面，项目在提升生产环境稳定性和企业级权限治理上持续推进。

---

## 4. 社区热点

- **[#7605 [Feature]: Improve import speed（已关闭）](https://github.com/BerriAI/litellm/issues/7605)** — 34 条评论，42 👍
  用户反馈导入 `litellm` 包耗时最长可达 1 秒，提供了 `importtime` 可复现脚本。该 Issue 虽已被标记 stale 并关闭，但引发了社区对依赖加载性能的广泛讨论，且在 2026 年 8 月仍有活跃评论，说明该痛点依然存在，或考虑重新开放/跟踪。

- **[#23451 [Bug]: Can't login despite setting password](https://github.com/BerriAI/litellm/issues/23451)** — 8 条评论
  用户设置了密码环境变量但 UI 仍然无法登录，尝试 `admin`、`sk-1234` 等均无效。该问题从 2026 年 3 月持续至今仍有讨论，且涉及 UI Dashboard 登录关键路径，建议维护者优先排查环境变量加载链路。

- **[#19499 [Bug]: Prompt Injection Detection Issues](https://github.com/BerriAI/litellm/issues/19499)** — 5 条评论
  内置提示注入检测被报告存在两个严重问题：启发式检查阻塞事件循环导致 Kubernetes Pod 重启，直接影响生产稳定性。该 Issue 从 2026 年 1 月报告至今仍有讨论，值得安全团队关注。

**社区诉求分析**：高频反馈集中在"包导入性能"、"UI 登录可靠性"、"安全检测稳定性"三个方向，均为直接影响使用者体验和线上稳定性的实际问题。

---

## 5. Bug 与稳定性

### 高危（建议优先处理）

- **[#38033 非管理员可通过 POST /credentials 覆盖 config.yaml 中定义的凭据](https://github.com/BerriAI/litellm/issues/38033)** — 权限提升风险：具备 `/credentials` 路由权限的用户可重用名称覆盖管理员定义的凭据。**已有对应 fix PR：[#38034](https://github.com/BerriAI/litellm/pull/38034)，返回 409 并处理数据库重复竞态**。

- **[#19499 提示注入检测启发式检查阻塞事件循环，导致 K8s Pod 重启](https://github.com/BerriAI/litellm/issues/19499)** — 影响生产环境的稳定性，长期未修复。

- **[#38028 bedrock_mantle 聊天补全忽略 per-model 静态 AWS 密钥](https://github.com/BerriAI/litellm/issues/38028)** — 部署级凭据未参与签名，可能继承代理主机身份，引发凭据混乱。**已有对应 fix PR：[#38032](https://github.com/BerriAI/litellm/pull/38032)**。

- **[#37925 自定义 pass-through 前缀在非默认 Anthropic 兼容主机下文件上传不可用](https://github.com/BerriAI/litellm/issues/37925)** — 路由优先级与 `custom_llm_provider` 解析矛盾，文件上传功能不可用。

### 中危

- **[#36926 持续负载下误报 BudgetExceededError（自愈约 2 分钟）](https://github.com/BerriAI/litellm/issues/36926)** — 拦截请求但能自恢复，与 Redis 预算计数一致性有关。
- **[#34614 Redis 缓存及预算计数在 v1.93.0 失败（ssl_check_hostname 参数错误）](https://github.com/BerriAI/litellm/issues/34614)** — 升级引入的回归问题。
- **[#37823 Azure GPT-4o 数据区域条目缺少 cache_read_input_token_cost，缓存读取计费为零](https://github.com/BerriAI/litellm/issues/37823)** — 成本核算对不上账。
- **[#21540 空 models 列表授予全部模型访问权限，空 MCP 列表则不授予任何访问权限](https://github.com/BerriAI/litellm/issues/21540)** — 安全风险，默认行为不一致。

### 轻微

- **[#38018 Ollama URL 格式错误（%s://%s:%d）](https://github.com/BerriAI/litellm/issues/38018)**

---

## 6. 功能请求与路线图信号

- **[时间/峰谷定价支持（#31606，6 👍）](https://github.com/BerriAI/litellm/issues/31606)** — 用户要求支持 DeepSeek 等按时间段区分的定价模型。社区已有对应 PR **[#31725](https://github.com/BerriAI/litellm/pull/31725) 实现 `off_peak_pricing` 配置块**，该功能正在开发中，很可能进入下一版本。
- **[模型组组合（"group of groups"）（#28125）](https://github.com/BerriAI/litellm/issues/28125)** — 允许模型组引用其他模型组作为成员，虽已关闭但需求明确，未来可能以其他形式回归。
- **[Gigachat 供应商 passthrough 路由（#25886）](https://github.com/BerriAI/litellm/pull/25886)** — 新增供应商支持，待合并。
- **[Anthropic Workload Identity Federation 支持（#38013）](https://github.com/BerriAI/litellm/pull/38013)** — 新提交的 PR，通过联合身份替代长期静态密钥，提升 Anthropic 直连安全性。

---

## 7. 用户反馈摘要

- **导入速度是持续性痛点**：Issue #7605 虽被标记 stale 关闭，但仍在持续收到反馈（最后评论在 2026-08-23），有用户建议优化依赖延迟加载。42 个 👍 表明该问题影响面较大。
- **登录体验困惑**：用户设置密码后仍无法登录 UI（#23451），且尝试多个常见凭据均失败，" Can't login despite setting password " 的标题直接反映了用户的无奈。
- **安全功能不透明**：Lakera guardrail 中设置 `category_thresholds` 会静默禁用未命名类别的拦截（#30727），这可能让用户误以为已被保护，存在安全隐患。
- **功能可用性落差**：Xinference 图片编辑功能被请求后很快关闭（#20961），说明功能可能已实现，但其他功能如"预算窗口用量展示"直到今日 PR #37044 才被合并，用户对可观测性的需求在持续增长。

---

## 8. 待处理积压

以下为长期未响应或需维护者反馈的重要条目：

- **[#19499 提示注入检测导致 Pod 重启（2026-01 报告，7 个月未关闭）](https://github.com/BerriAI/litellm/issues/19499)** — 安全与稳定性双重影响，优先级应提高。
- **[#23451 UI 登录失败（2026-03 报告，5 个月未关闭）](https://github.com/BerriAI/litellm/issues/23451)** — 影响所有自托管用户的基础功能。
- **[#34614 Redis SSL 参数回归（v1.93.0 引入，至今未修复）](https://github.com/BerriAI/litellm/issues/34614)** — 影响使用 Redis 缓存和预算计数的部署。
- **[#7605 导入速度优化（2025-01 发起，虽关闭但有 42 👍）](https://github.com/BerriAI/litellm/issues/7605)** — 建议维护者重新评估或纳入性能优化路线图。

---

**总结**：LiteLLM 项目今日整体健康度高，社区活跃、响应迅速。安全相关的两个 Bug 已有修复 PR 跟进，值得肯定。但登录问题、导入性能、提示注入检测等长尾问题仍待解决；同时时间峰谷定价、预算窗口可视化和 Workload Identity Federation 等新功能正稳步推进中，未来版本值得期待。

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

好的，作为一名 AI 智能体与个人 AI 助手领域开源项目分析师，我为您梳理了 Temporal 项目在今日（2026-08-24）的 GitHub 项目动态日报。

---

# Temporal 项目动态日报 — 2026-08-24

## 1. 今日速览

过去 24 小时内，Temporal 项目活跃度较高，虽无正式版本发布，但核心功能与基础设施均有显著推进。Issue 侧有 1 条新反馈，聚焦于一个关键的一致性问题（任务投递不确定性），且已出现对应的修复 PR。PR 侧共更新 28 条，其中 9 条已合并/关闭，19 条处于待合并状态，整体代码流动顺畅。项目当前正在为 1.32.0 版本的发布做准备，同时社区高度关注的长周期功能（Worker-variant Callbacks、MySQL 多主机支持）也有了实质进展。

## 2. 版本发布

**无正式新版本发布。** 但值得注意的是，自动化机器人已创建 PR **#11737** 用于准备 `1.32.0` 的发布分支，包括覆盖治理文件和更新依赖。该 PR 已于今日关闭，暗示发布流程已进入预发布阶段，或将于近期有正式 release 产出。
[查看发布分支准备 PR](https://github.com/temporalio/temporal/pull/11737)

## 3. 项目进展

今日虽有 9 条 PR 被关闭，但出于信息完整性考虑，大部分被关闭的 PR 为机器人自动化操作（如测试分片盐值更新）。在核心工程进展方面，以下几条 PR 的推进值得关注：

- **Callback 功能栈收尾**：**#10192** 与 **#10290** 均在今日关闭。前者是 "standalone callbacks" 支持（距今已 3 个月的长线功能），后者为 Nexus HTTP 端点添加 OpenTelemetry (OTEL) 遥测。这标志着 Temporal 的长期 feature 栈正在逐步合入主干。
- **测试稳定性优化**：**#11736** 与 **#11726** 均由自动化工作流生成的测试分片盐值更新，用以优化测试负载均衡，是保障项目健康度的例行工程优化。
- **MySQL 多主机支持**：**#11659** 仍为开放状态，旨在支持逗号分隔的多主机地址和 DNS SRV 记录连接，并为每个新连接解析目标、在不可用/只读主机间进行故障转移。

这些合入和推进表明，项目在持续清理长线技术债务，并为新版本的多数据库支持与可观测性提升打下基础。
[查看 standalone callbacks PR](https://github.com/temporalio/temporal/pull/10192) | [查看 OTEL 仪表化 PR](https://github.com/temporalio/temporal/pull/10290) | [查看 MySQL 多主机 PR](https://github.com/temporalio/temporal/pull/11659)

## 4. 社区热点

- **Issue #11733 + PR #11734（关联热点）**：由 @ali-khokhar-nvidia 提出并修复。该组合揭示了用户在使用过程中发现的一个边界问题：当 History 提交了 task start，但原始 worker poll 仍活跃时，由于 RPC 超时可能导致的“任务已开始但无法恢复/响应”的歧义。该问题直指分布式系统中最敏感的一致性痛点，因此在同日即有了对应的修复 PR。这不仅是热点，也是当前最需要被维护者关注的修复点。
[查看 Issue #11733](https://github.com/temporalio/temporal/issues/11733) | [查看 Fix PR #11734](https://github.com/temporalio/temporal/pull/11734)

- **Worker-variant Callbacks（长期热点）**：今日有 3 条相关 PR（#11566、#11520、#11735）更新，且均由 @chrsmith 提交。这组 PR 在沉寂一段时间后再次活跃，显示该堆栈正在进入紧锣密鼓的集成阶段。虽然评论数未列出，但其持续的更新频率和跳动的 PR 数量（占今日展示 PR 的 1/3 以上）依然构成社区关注焦点。
[查看最新更新 PR #11735](https://github.com/temporalio/temporal/pull/11735)

## 5. Bug 与稳定性

- **[严重] 任务启动无法投递问题（Issue #11733）**：被描述为当 History 提交了 workflow/activity task start，但原始 poll 仍活跃时，如果单次 RPC 超时，会导致 task start 保持在模糊状态。**影响**：可能导致任务在系统中已启动但客户端收不到响应，从而触发不必要的重试或卡死。
  **状态**：已有对应的修复 PR **#11734**，建议维护者优先审阅。
  [查看 Issue](https://github.com/temporalio/temporal/issues/11733) | [查看修复 PR](https://github.com/temporalio/temporal/pull/11734)

- **[一般] 重试抖动被截断为无效 (PR #11397)**：该 PR 修复了 `retrypolicy.go` 中 `addJitter` 计算错误，修复前设定的抖动比例（如 0.1）会导致结果始终为 0，实际等待时间恒等于基础耗时（如 2.000s），而非预期的随机范围。属于逻辑功能性 bug，目前修复 PR 仍在开放状态。
  [查看 PR #11397](https://github.com/temporalio/temporal/pull/11397)

- **[无关紧要] 日志标签丢失 (PR #11355)**：修复 `zapLogger.Skip()` 方法在克隆 logger 时未携带 `tags` 字段的问题，以保持日志上下文一致性。
  [查看 PR #11355](https://github.com/temporalio/temporal/pull/11355)

## 6. 功能请求与路线图信号

- **Worker-variant Callbacks（明确路线图信号）**：如前所述，由 API 变更（temporalio/api#856）驱动，这将是继 Nexus 之后的下一个主要外部可观测性/集成特性。多个 PR 表明开发者已经为这一特性构建了完善的测试和路由逻辑。这**很可能**会被纳入下一个主版本中。
  [查看核心实现 PR #11589](https://github.com/temporalio/temporal/pull/11589)

- **MySQL 多主机与 SRV 支持 (PR #11659)**：社区对自托管 MySQL 的高可用支持需求明确，该 PR 试图解决单机故障和 DNS SRV 记录解析问题，若合入将提升 Temporal 在 MySQL 部署场景下的生产可用性。
  [查看 PR #11659](https://github.com/temporalio/temporal/pull/11659)

- **独立的历史扫描器限流 (PR #11738)**：新增动态配置 `worker.historyScannerRPS`，允许运维人员单独调节 history scavenger 的 RPS，避免后台扫描任务挤占主要业务流量。这是对现有“大而全”配置项的精细化拆分，符合生产环境运维精细化的发展趋势。

- **CHASM 时间跳过（Schedules）功能 (PR #10934, #11741)**：为 Chasm 框架及 Schedules 添加“时间跳跃”能力，以满足测试或仿真场景下对时间流逝速度的自定义控制。

## 7. 用户反馈摘要

在有限的 Issue 评论数据中，以下关键用户反馈较有代表性：

- **痛点：分布式系统的不确定性难以调试与恢复**。Issue #11733 中，用户（@ali-khokhar-nvidia）清晰描述了事务性任务启动在超时情况下的确定性缺失。这说明专业用户在深入使用 Temporal 时，对极端边界的处理有较高要求，期待系统能够在任何微小的时序错乱下依然保证传递一次（Exactly-once）语义。
- **诉求：增强系统可诊断性与可控性**。从新增的 `historyScannerRPS` 配置以及 OTEL（OpenTelemetry）探针的合入可以看出，用户在自建监控或云环境运行 Temporal 时，对性能隔离和可观测性的需求在持续增长。

## 8. 待处理积压

以下 PR 已处于较长待合并期，建议维护者关注：

- **PR #10934**（chasm framework 的时间跳过）：自 2026-07-06 创建，已超过 7 周无显著合并信号。
  [查看 PR #10934](https://github.com/temporalio/temporal/pull/10934)
- **PR #11355 / #11397**（日志标签 / 重试抖动）：均为质量修复类 PR，虽不紧急但影响系统可观测性与重试准确性，已停留近 3-4 周，建议加速审阅合并。
  [查看 PR #11355](https://github.com/temporalio/temporal/pull/11355) | [查看 PR #11397](https://github.com/temporalio/temporal/pull/11397)
- **PR #11411**（删除工作流复制任务版本）：涉及数据复制边界的一致性修复，

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*