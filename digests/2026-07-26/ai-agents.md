# OpenClaw 生态日报 2026-07-26

> Issues: 321 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-25 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

## OpenClaw 项目日报 — 2026-07-26

### 1. 今日速览

过去 24 小时，OpenClaw 项目保持极高活跃度：共处理 **321 条 Issue 更新**（新开/活跃 226，关闭 95）和 **500 条 PR 更新**（待合并 296，已合并/关闭 204）。社区提交密度仍处高位，但 **P0/P1 级 Bug 和回归问题占比上升**，尤其在网关启动、内存管理和渠道交付方面。无新版本发布，但有多项大型重构 PR 进入审查阶段，项目健康度总体稳定，维护者需紧急关注若干阻塞性 Bug。

---

### 2. 版本发布

（无新版本发布，本日从略）

---

### 3. 项目进展

过去 24 小时合并/关闭的重要 PR 包括：

- **[#113889] refactor(agents): finish exec pipeline split**（已合并）  
  完成 `bash-tools.exec.ts` 拆分，将主执行管线模块从 740 行降至合规尺寸，不改变审批或执行行为。  
  https://github.com/openclaw/openclaw/pull/113889

- **[#113874] fix(qa): prevent live transport cleanup races**（开放中，但已通过审查）  
  修复 QA 场景下并发清理导致信道驱动重复停止的竞态问题。  
  https://github.com/openclaw/openclaw/pull/113874

- **[#113894] fix(ui): restore automatic agent fast-mode settings**（开放中）  
  修复 Control UI 中无法选择 `auto` 快速模式策略的回归，表单字段从开关恢复为三值选择。  
  https://github.com/openclaw/openclaw/pull/113894

此外，多个大型重构 PR 进入维护者审查阶段，包括 `feat(plugins): add external verification approvals`（#113517）、`refactor(daemon): split Windows task scheduler integration`（#113783）、`refactor(agents): split direct compaction pipeline`（#113880）。这些 PR 旨在降低单体模块复杂度，提升可维护性，**表明项目正从功能添加期转向架构治理期**。

---

### 4. 社区热点

今日讨论最活跃的 Issues/PRs：

| 编号 | 标题 | 评论数 | 关注点 |
|------|------|--------|--------|
| [#7707] | Feature Request: Memory Trust Tagging by Source | 21 | 用户提议按来源（用户指令、网页抓取、第三方技能）标记内存信任等级，防范内存投毒攻击。获得 diamond lobster 最高隐患评级。 |
| [#78308] | Channel-mediated approval for MCP tool calls (consent envelope) | 15 | 要求 MCP 工具调用复用已有渠道审批机制，解决外部状态变更的安全管控缺失。 |
| [#86996] | Active Memory + Codex app-server path 导致延迟、超时、启动中止 | 14 | 组合使用 active-memory、honcho、lossless-claw 和 OpenAI Codex 时，简单 Telegram 指令响应极慢，已引发多名用户共鸣。 |
| [#113306] | SQLite snapshot restore lacks end-to-end crash and identity guarantees | 13 | 快照创建/恢复可能在不牢固的目录链接下报告成功，存在数据丢失风险。 |
| [#108435] | update to openclaw 2026.7.1: gateway fails to start | 11 | **P0 回归**：升级后 gateway 无法启动，systemd、ollama、手动启动均失败。 |

社区普遍诉求集中在 **安全加固（内存标签、工具审批、文件沙箱）** 和 **稳定性修复（网关启动、内存泄漏、上下文膨胀）**。此外 Telegram、Discord、WhatsApp 等渠道的交付丢失问题也反复出现。

---

### 5. Bug 与稳定性

按严重程度排列（P0 > P1 > P2），标注是否已有修复 PR：

| 严重度 | Issue | 摘要 | 修复状态 |
|--------|-------|------|----------|
| **P0** | [#108435] gateway 启动失败（2026.7.1 回归，systemd/ollama/手动均失败） | [OPEN] 无关联 PR |
| **P0** | [#107220] gateway crash-loop：遗留 memory sidecar `meta`/`chunks` 冲突致命 | [CLOSED] 已修复 |
| **P0** | [#95515] 升级 6.8→6.9 损坏 email 频道配置（写入非法 groupAllowFrom） | [OPEN] 有 linked PR |
| **P1** | [#86996] Active Memory + Codex 导致严重延迟/超时/启动中止 | [OPEN] 无 fix PR |
| **P1** | [#113306] SQLite 快照恢复缺乏崩溃与身份保证 | [OPEN] 无 fix PR |
| **P1** | [#7710] 子代理列表在 v2026.4.29 仍为空 | [CLOSED] 已关闭（但用户反馈修复不完整） |
| **P1** | [#113315] Telegram 更新永久丢失（已持久化 offset 但无 ingress） | [OPEN] 无 fix PR |
| **P1** | [#112423] 大型 SQLite 记录清理阻塞事件循环 | [OPEN] 无 fix PR |
| **P1** | [#94251] Ollama 远程 provider 流式未消费（chat 会话卡住） | [OPEN] 无 fix PR |
| **P2** | [#43747] 内存管理混乱（不同实例表现不同） | [OPEN] 无 fix PR |
| **P2** | [#87299] Telegram 大型会话出现 “Something went wrong” 和 Codex 失败 | [CLOSED] 已关闭但用户报告复现 |

**今日最紧急 Bug**：`#108435` 为 P0 回归，影响所有升级至 2026.7.1 的用户，需优先排查。

---

### 6. 功能请求与路线图信号

| 功能请求 | 链接 | 用户场景 | 潜在纳入版本 |
|----------|------|----------|--------------|
| 内存信任标签（按来源标记可信度） | [#7707] | 防止网页、第三方技能隐藏恶意指令投毒记忆 | 需安全审查 + 产品决策，路线图可能 Q3 |
| 渠道审批信封（MCP 工具调用） | [#78308] | 外部状态变更（发送邮件、写入 vault）需用户显式同意 | 已有对应 PR 概念验证 |
| 文件系统沙箱配置 | [#7722] | 限制 agent 可读写路径，防御任意文件访问 | 安全增强，可能纳入 2026.8 |
| 动态模型发现（OpenRouter 等） | [#10687] | 提供商模型目录频繁更新，需自动拉取而非静态列表 | 已有 `models.generated` 改进讨论 |
| 子 agent 工具限制（per-spawn） | [#15032] | 创建隔离网络搜索 agent 防止提示注入 | 安全架构重要补充，已有详细设计 |
| 上下文溢出时触发模型回退 | [#9986] | 主模型超限时自动 fallback 到更大模型 | 功能增强，已有配置占位但未实现 |
| 预压缩 agent 通知与结构化窗口 | [#38520] | 长工作流 agent 需要提前收到压缩通知以保存状态 | 大状态工作流稳定性需求 |
| 外部验证审批插件 | [#113517] | 插件拥有外部验证审批合约 | **已有完整 PR，可能进入下一版本** |

以上 `#113517`（外部验证审批）已进入审查，是当前最接近合并的功能性 PR。

---

### 7. 用户反馈摘要

从 Issues 评论中提炼的真实用户痛点：

- **“升级后配置丢失或损坏”**（#54634、#95515、#103162）：多用户在升级过程中遇到 `openclaw.json` 被静默修改或 schema 校验失败，导致服务中断。用户期望升级过程更透明、提供回滚机制。
- **“文档与发布版本脱节”**（#48920、#103162）：文档中记录的配置项（如 `IsolatedSessions`、`streaming.preview.toolProgress`）在最新版本中不存在或 schema 拒绝，用户必须查阅社区帖子才能找到有效配置。
- **“内存/上下文管理混乱”**（#43747、#67419）：不同用户或同一用户的不同实例内存存储方式不一致（SQLite  vs 文件），且 bootstrap 文件每轮重复注入浪费 20-30% token，用户希望统一策略并优化上下文开销。
- **“渠道消息交付不可靠”**（#92186、#91564、#113315）：WhatsApp 群组回复只送达最后一个 @mention；Telegram 特定线程变成永久黑洞；消息被 ack 但从未进入 agent。用户强调这是生产环境的严重阻碍。
- **“网关稳定性欠佳”**（#108435、#87109、#107220）：升级后启动失败、空闲内存泄漏至 1GB+、crash-loop 需手动重启。运维成本高，用户期望更健壮的 self-health 和恢复机制。

总体满意点：社区活跃、迭代快、功能丰富；不满意点：升级兼容性、核心稳定性、渠道交付可靠性。

---

### 8. 待处理积压

以下为长期未响应或未解决的重要 Issue/PR，提醒维护者关注：

| 编号 | 标题 | 创建时间 | 最后更新 | 原因 |
|------|------|----------|----------|------|
| [#48920] | Live Docs are ahead of release | 2026-03-17 | 2026-07-24 | 文档与实际版本配置差异，已超 4 个月无实质推进 |
| [#11955] | Memory/Context Improvements（指标+全局语义搜索+对话链式） | 2026-02-08 | 2026-07-25 | 涉及多个核心改进，虽有讨论但无统一设计 |
| [#38520] | Pre-compaction agent notification | 2026-03-07 | 2026-07-25 | 安全/协作功能，持续有 +1 但未进入优先队列 |
| [#15032] | Per-spawn tool restrictions for sub-agents | 2026-02-12 | 2026-07-25 | 安全增强，已多次被提及但无具体实现 |
| [#10944] | Add parseMode config for Telegram | 2026-02-07 | 2026-07-25 | 简单配置项，长期未进入计划 |
| [#9637] | Disable emojis/unicode in TUI for accessibility | 2026-02-05 | 2026-07-25 | 影响残障用户，无维护者响应 |
| [#9409] | Improve context overflow error message | 2026-02-05 | 2026-07-25 | 用户体验改进，低优先级但长期未处理 |

**特别提示**：`#48920`（文档超前发布）和 `#103162`（文档配置被 schema 拒绝）属于**用户信任问题**，建议优先修复，避免用户因文档误导而配置失败。

---

*报告基于 github.com/openclaw/openclaw 截至 2026-07-25 的数据生成，覆盖过去 24 小时动态。所有链接可点击跳转至对应 Issue/PR。*

---

## 横向生态对比

# 个人 AI 智能体开源生态横向对比分析报告（2026-07-26）

## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态正处于 **“功能爆发期”向“质量巩固期”过渡**的关键阶段。各项目社区活跃度持续高位运行，单日 Issue/PR 总量超过 1000 条，反映出开发者参与热情极高。然而，随着功能快速堆叠，**安全加固、稳定性修复和架构治理**成为多项目共同的主旋律——OpenClaw 开始大型重构降复杂、Hermes Agent 密集修复会话状态崩溃、LiteLLM 修复凭证泄漏、Pi 优化 TUI 性能和 compaction 可靠性。同时，**新模型支持（Claude Opus 5、DeepSeek V4）和平台适配（Buzz、飞书、Azure AD）**仍是吸引用户的关键卖点。总体来看，生态正从“能用”迈向“可靠”，用户对生产环境下的升级兼容、消息交付一致性提出了更高要求。

## 2. 各项目活跃度对比

| 项目 | Issues 更新数 | PR 更新数 | 版本发布 | 健康度评估 |
|------|---------------|-----------|----------|------------|
| **OpenClaw** | 321（新开/活跃 226，关闭 95） | 500（待合并 296，合并/关闭 204） | 无 | 总体稳定，但 P0/P1 Bug 占比上升，需紧急关注 |
| **Hermes Agent** | 500（总更新数）* | 500（总更新数）* | 无 | 中等偏上，PR 积压严重，会话稳定性问题突出 |
| **Pi** | 56（关闭 45） | 19（合并/关闭 11） | **v0.82.1** | 良好，Compaction 和 TUI 性能问题待改善 |
| **LiteLLM** | 76（新开/活跃 57，关闭 19） | 199（待合并 117，合并/关闭 82） | 无 | 高活跃度，长期社区 Issue 积压需关注 |
| **Temporal** | 0（无新增/关闭） | 29（待合并 23，合并/关闭 6） | 无（1.32.0 分支准备中） | 良好（内部活跃，外部冷却），CHASM 调度器密集修复 |
| **OpenHands SDK** | 数据不可用 | 数据不可用 | — | 摘要生成失败，无法评估 |

*Hermes Agent 日报原文给出 500 条 Issue 和 500 条 PR 更新，但后续细节显示实际合并数有限，此处按报告数据列出总更新量；具体 Issus/PR 的详细分类可能存在重叠统计。

## 3. OpenClaw 在生态中的定位

- **社区规模最大**：单日 321 条 Issue 和 500 条 PR 更新，远超其他项目，用户基数与贡献者网络处于生态领先位置。
- **功能覆盖面最全**：涵盖 agent 执行管线、多渠道交付（Telegram、WhatsApp、Discord）、内存管理、文件沙箱等，定位为“全能型个人 AI 助手框架”。
- **技术路线差异**：相比 Hermes Agent 侧重前端/桌面体验、Pi 侧重终端 TUI、LiteLLM 专注 API 网关，OpenClaw 更像“一体化操作系统”——拥有自己的配置文件规范、插件系统、渠道审批机制。当前正从功能添加转向架构治理（详见多大型重构 PR），表明项目在技术债务管理上更为主动。
- **痛点同样突出**：升级兼容性（gateway 启动失败）、渠道交付可靠性（消息丢失）和内存管理混乱等稳定性问题在同类中最为高频，社区呼声也最高。

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|----------|----------|----------|
| **安全加固** | OpenClaw、Hermes Agent、LiteLLM、Pi | 内存信任标签（OpenClaw #7707）、MCP 工具调用审批（OpenClaw #78308，LiteLLM #34340 凭证泄漏修复）、凭证代理守护进程（Hermes Agent #4656）、文件系统沙箱（Pi #7722 / OpenClaw #7722） |
| **会话/上下文稳定性** | OpenClaw、Hermes Agent、Pi、LiteLLM | 会话状态损坏/恢复（Hermes Agent #64934、#69078）、Compaction 后停滞（Pi #7020）、SQLite 快照缺乏保证（OpenClaw #113306）、上下文溢出回退（OpenClaw #9986） |
| **新模型与提供商集成** | Pi、LiteLLM、Hermes Agent | Claude Opus 5（Pi）、MachGen 图像生成（LiteLLM #34651）、Ollama 原生 API（Hermes Agent #4505）、DeepSeek V4 多轮失败（LiteLLM #26395） |
| **可观测性与运维** | LiteLLM、Temporal | Prometheus 指标通配符（LiteLLM #34622）、工作流运行时状态暴露（Temporal #11259）、shard backlog 年龄指标（Temporal #11255） |
| **跨平台/渠道适配** | OpenClaw、Hermes Agent、Pi | 消息交付可靠性（OpenClaw Telegram/WhatsApp）、飞书 Markdown（Hermes Agent #46470）、Buzz 平台集成（Hermes Agent #68871）、OpenRouter 手动回调（Pi #7078） |

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent | Pi | LiteLLM | Temporal |
|------|----------|--------------|----|---------|----------|
| **功能侧重** | 全能型个人助手框架（Agent 执行、渠道、内存、审批） | 多平台适配器 + 桌面端体验 | 终端 TUI 交互 + 模型广泛支持 | LLM API 网关（路由、安全、成本控制） | 分布式工作流引擎（调度、编排、复制） |
| **目标用户** | 个人开发者、自部署社群 | 个人用户、跨平台消息集成者 | 终端爱好者、技术极客 | 企业运维/工程团队 | 微服务/后台开发者 |
| **技术架构特点** | 单体+大型重构降复杂，插件系统，渠道审批 | 前端（桌面/APP）+ 后端 SDK 分离，快速迭代 | 轻量级 Node.js 应用，TUI 第一，模型集成层 | 代理层（Proxy）+ 大量集成适配器，企业 SSO | 服务端（Go）+ 数据库（Cassandra/SQL），高可用复制 |
| **当前阶段** | 架构治理期（大型重构 PR） | 功能叠加期（大量 PR 涌入） | 快速迭代期（频繁版本发布） | 混合期（新功能+长期 Bug 积压） | 质量巩固期（CHASM 密集修复） |

## 6. 社区热度与成熟度分层

| 分层 | 项目 | 特征 |
|------|------|------|
| **🔥 极度活跃（快速迭代）** | Hermes Agent、Pi | 单日 PR/Issue 总量≥500，频繁版本发布（Pi 昨天发版），社区评论活跃，新功能涌入快，但稳定性短板明显。 |
| **🔥 高度活跃（质量巩固）** | OpenClaw、LiteLLM | 单日 PR/Issue 数百起，大型重构或长期 Bug 修复并行，社区规模大，但用户对稳定性的不满比例上升。 |
| **🌡️ 中等活跃（内部密集）** | Temporal | 公开 Issue 少，核心团队 PR 密集（29 个 PR 几乎全来自维护者），外部贡献热度低，但内部开发节奏快，适合后台稳定演进。 |
| **⬇️ 数据缺失** | OpenHands SDK | 无法评估 |

## 7. 值得关注的趋势信号

1. **安全从“可选项”变为“必须项”**  
   多项目用户不约而同提出内存投毒防御（OpenClaw #7707）、工具调用审批（#78308）、凭证防泄漏（LiteLLM #34340），反映出智能体执行权限扩大后，社区对安全架构的敏感度急剧上升。**开发者应考虑在三层（内存→工具→网络）上建立信任链**。

2. **消息交付一致性成为生产瓶颈**  
   OpenClaw 的 Telegram 消息丢失、Hermes Agent 的会话状态损坏、Pi 的 compaction 后停滞——这些看似不同的 Bug 背后是 **“状态持久化+异步通信”的可靠性坑**。未来 AI 代理若想进入生产任务，必须解决幂等、死信恢复和可观测性。

3. **模型支持“组件化”趋势明显**  
   Pi 和 LiteLLM 都在快速增加新模型提供商（MachGen、OpenInfer），同时 Heremes Agent 在讨论 Ollama 原生 API。**“模型切换”不再是硬编码而是可插拔插件**，项目边界正在从“绑定特定模型”转向“统一网关+适配器”模式。

4. **终端交互体验开始被单独优化**  
   Pi 投入大量精力修复 TUI CPU 占用、滚动闪烁、补全空格等细节；Hermes Agent 修复桌面端工作目录和认证循环。这表明 **AI 智能体正在从“API 服务”向“用户客户端产品”进化**，交互流畅度将影响流失率。

5. **架构治理成为规模瓶颈**  
   OpenClaw 是最典型代表：通过拆解 700+ 行单体模块（#113889）、分离任务调度（#113880）来提升可维护性。LiteLLM 也在优化 CI 范围（#34600）。**当功能积累到一定程度，“拆分”比“新增”更重要**——这是所有快速增长项目不久将面临的挑战。

---

*报告基于 2026-07-26 各项目 GitHub 动态生成，数据源截至当日数据。OpenHands SDK 因摘要生成失败未纳入详细分析。*

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，这是根据您提供的 Hermes Agent 项目数据生成的 2026-07-26 项目动态日报。

***

# Hermes Agent 项目动态日报 | 2026-07-26

## 1. 今日速览

项目今日极度活跃，24小时内产生了500条Issue和500条PR更新，但大量PR处于待合并状态，表明社区贡献热情高涨，但核心维护团队的审查和合并能力面临压力。今日没有新版本发布，但大量关键Bug修复（如会话状态损坏、首条消息丢失）和长期悬而未决的功能请求（如插件接口扩展、Ollama优化）有了实质性进展。总体来看，项目正处于功能快速迭代与稳定性攻坚并行的阶段，健康度中等偏上，但需要警惕积压问题。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日共有95个PR被合并/关闭，51个Issue被关闭，显示了高效的清理工作。关键进展包括：

-   **核心会话稳定性修复**：多个影响会话状态的严重 Bug 得到解决，包括 `$64934`（双轮并发导致会话永久性损坏）、`$64789`（桌面端提交目标错误）和 `$65384`（远程后端非默认配置文件创建新会话），这些修复将极大提升用户体验。
-   **桌面端问题收敛**：`$38855`（工作目录设置被遗忘）和 `$63679`（消息重复渲染）等桌面端用户体验 Bug 被关闭，表明桌面应用稳定性正在改善。
-   **平台适配器推进**：`$46470`（飞书平台 Markdown 渲染问题）被修复，`PR #71610`（Buzz/Nostr 平台适配器）被提交，显示了项目在跨平台支持方面的持续投入。
-   **文档完善**：`PR #71615`（Memory vs. Skills 决策框架）被合并，有助于降低新用户的学习成本，提升社区自服务能力。

## 4. 社区热点

今日社区最活跃的讨论集中在以下几个话题：

-   **插件接口扩展 (Issue #64182)**：以16条评论成为最热门Issue。该项目旨在为长期等待的PR提供稳定的发布通道，反映了社区对扩展Hermes核心功能的强烈渴望，尤其是围绕插件生命周期的管理。
-   **Ollama 集成优化 (Issue #4505)**：获得14条评论和2个👍。社区对于使用Ollama原生 `/api/chat` 端点替换OpenAI兼容端点的方案讨论热烈，核心诉求是获得更好的流式传输体验和更少的工具调用问题，这反映出用户对本地部署和性能优化的重视。
-   **Buzz (Block开源项目) 集成 (Issue #68871， PR #71610)**：此功能获得了10个👍，一经提出就迅速有对应的PR提交。这显示出社区对“AI Agent与人混合协作”场景的兴奋，以及项目对新平台的快速响应能力。
-   **凭证代理守护进程 (Issue #4656)**：13条评论，关注安全性的高级功能。社区深入探讨了在已有PID命名空间隔离基础上，如何进一步消除凭据泄露风险，表明高级用户对生产环境下的安全架构有较高要求。

## 5. Bug 与稳定性

今日报告的 Bug 数量众多，按严重程度排列如下：

-   **严重 (P0/P1)**：
    -   无 P0 级别 Bug 报告。P1 级别 Bug `$38855`（工作目录设置问题）和 `$63078`（首条消息导致空白会话）已被关闭，但后者在修复前影响极大。
-   **高 (P2)**：
    -   [**Bug**] **xAI `grok-4.5` 图像处理错误导致会话永久性损坏** (`$69078`): 一个无效的PNG图像会永久“砖化”整个会话，无法通过任何方式恢复，影响严重。
    -   [**Bug**] **`keepalive_expiry=20s` 导致 Cloudflare/OpenRouter 流式传输中断** (`$67012`): 影响使用特定代理服务的用户。
    -   [**Bug**] **桌面端云/远程网关认证循环** (`$71514`): 桌面端在连接有认证需求的远程后端时陷入无限401重试循环，无法加载UI。
    -   [**Bug**] **`providers` vs `custom_providers` 存储不一致** (`$71298`): 导致CLI和GUI对模型的配置存在分歧，用户体验较差。
-   **中 (P3)**：
    -   今日大量报告的 `sweeper:risk-session-state` 类Bug，如 `$66875`（浏览插件标签页后会话切换问题）、`$67600`（桌面端默认配置文件会话侧边栏空白），均与前端会话状态管理有关，虽然优先级P2/P3，但反映出桌面端会话状态管理模块存在系统性脆性。

**批量修复情况**：今日有多个 PR（如 `#71605`， `#71611`， `#71612`）直接针对 `sweeper:risk-session-state` 标签下的问题进行修复，表明团队已注意到此系统性问题并开始批量处理。

## 6. 功能请求与路线图信号

-   **高可能性纳入下一版本**：
    -   **Buzz 平台适配器** (`PR #71610`): 已有完整实现 PR，作为社区呼声极高的功能，很可能被快速合并。
    -   **MCP 智能加载** (`Issue #66473`): 虽然PR已关闭，但其讨论的“懒加载”、“按会话范围分配工具”等概念是解决资源占用和性能瓶颈的关键，很可能成为即将到来的插件/工具框架重构的一部分。
-   **中期路线图信号**：
    -   **插件接口扩展** (`Issue #64182`): 作为跟踪问题，它本身就是一个路线图信号，表明项目将正式化、标准化插件生态，为第三方开发者扫清障碍。
    -   **Ollama 原生 API 集成** (`Issue #4505`): 社区对此有强烈的共识，代表了从“兼容层”转向“原生集成”的架构思路，可能会在未来版本中作为一个默认选项或配置项落地。

## 7. 用户反馈摘要

-   **痛点明确**：
    -   **会话状态不稳定是最大痛点**：用户普遍反映在多种场景下（切换标签页、使用非默认配置、远程连接等）会遇到会话丢失、消息错乱等问题，严重影响日常使用。
    -   **桌面端配置体验不佳**：工作目录、远程认证、配置文件不一致等问题让桌面端的上手和配置过程充满了“意外”。
-   **高度期待**：
    -   **Ollama 用户对原生API呼声极高**：他们希望获得更流畅、更本地的体验，而不是通过“翻译层”与Ollama交互。
    -   **社区对“Agent to Human”通信场景充满兴趣**：对于像 Buzz 这样的新平台，用户不仅仅把它看作又一个消息通道，而是将其视为实现“人类与Agent协同工作”的重要基础设施。
-   **学习成本**：社区成员对 `Memory` 和 `Skills` 的概念区分仍有困惑，用户对 `PR #71615` 合并的文档表示了积极关注。

## 8. 待处理积压

-   **长期未响应的核心性能与兼容性 Issue**：
    -   **`#4505`[OPEN] - Ollama 原生API集成**：从4月1日提交至今，讨论热烈（14条评论），但为期近4个月仍为“待决策”状态。考虑到社区呼声和明确的性能优势，建议维护者尽快做出决策。
    -   **`#55293`[OPEN] - 文件搜索工具不包含空目录**：PR于6月30日提交，至今仍未合并。这是一个违反直观预期的行为，可能影响依赖文件树结构的用户。
-   **等待反馈的 PR**：
    -   **`#55297`[OPEN] - WhatsApp 适配器aiohttp依赖缺失修复**：同样于6月30日提交，至今仍是开放且未合并状态。对于计划使用WhatsApp作为平台的新用户，这是个阻碍性问题。
    -   **`#58458`[OPEN] - Windows平台Matrix后端刷新失败**：该问题严重阻碍了Windows用户的更新流程，可能表明测试覆盖或对Windows平台的支持存在短板，需要维护者关注。

---
**分析师总结**：Hermes Agent 项目展现出强大的社区活力和快速迭代能力，尤其是在应对高频Bug和回应社区新平台需求方面表现突出。然而，庞大的PR积压、关键功能决策的长期搁置（如Ollama）以及部分P2级Bug的持续存在，是项目当前的主要风险点。建议核心团队在未来一段时间内，优先进行一轮“Bug清理”和“积压PR合并”，以稳定根基，再迈向更宏大的功能扩展。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

⚠️ 摘要生成失败。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目日报 — 2026-07-26

## 1. 今日速览
过去 24 小时，Pi 项目保持高活跃度：共处理 **56 条 Issue**（关闭 45 条）、**19 个 PR**（合并/关闭 11 个），并发布了 **v0.82.1** 版本。核心进展包括：Claude Opus 5 模型支持、多个 TUI 稳定性修复（CPU 高占用、滚动条清空、冻结等），以及 compaction 和会话切换的改进。社区讨论集中在大模型集成体验与长会话资源消耗上，整体项目健康度良好。

## 2. 版本发布：v0.82.1
- **新功能**
  - **Claude Opus 5** — 在 Anthropic 和 Amazon Bedrock 上可用，支持自适应思维（含 `xhigh`）、推理配置（inference profiles）和提示缓存。
- **影响与迁移**
  无破坏性变更，用户可立即更新到 v0.82.1 并配置 Claude Opus 5。相关文档已更新：[Providers](https://github.com/earendil-works/pi/blob/v0.82.1/packages/coding-agent/docs/providers.md#api-keys)。

## 3. 项目进展
### 已合并/关闭的显著 PR
| PR | 描述 | 影响 |
|---|---|---|
| [#7116](https://github.com/earendil-works/pi/pull/7116) | fix(tui): 截断超宽行而非崩溃 | 解决因权限系统长 JSON 导致会话崩溃的严重问题 |
| [#7111](https://github.com/earendil-works/pi/pull/7111) | feat: 支持持久化外部工具结果 | 允许会话主机在进程外等待工具结果，提升扩展性 |
| [#7091](https://github.com/earendil-works/pi/pull/7091) | fix(coding-agent): 拒绝重叠的用户 bash 命令 | 防止用户在 RPC 会话中同时运行多个 bash 导致混乱 |
| [#7085](https://github.com/earendil-works/pi/pull/7085) | feat: 添加 vitest eval 测试框架 | 为 Pi 的 AI 评估能力提供标准测试环境，便于后续质量保障 |
| [#7081](https://github.com/earendil-works/pi/pull/7081) | feat(ai): 在 Bedrock 上支持 Claude Opus 5 | 随新版发布一同落地 |
| [#7072](https://github.com/earendil-works/pi/pull/7072) | fix(coding-agent): 缓存 llama.cpp 模型目录 | 解决 `defaultProvider`/`defaultModel` 启动时因异步刷新失效的问题 |
| [#7061](https://github.com/earendil-works/pi/pull/7061) | fix: 处理 OpenAI 兼容流中的数组内容与缺失 finish_reason | 修复 Databricks 等非标准提供商的中文乱码与推理内容问题 |
| [#7032](https://github.com/earendil-works/pi/pull/7032) | fix(coding-agent): 暴露不可用的 scoped 模型 | 使用户能看到并删除不可用的自定义模型 |

### 待合并的 PR（共 8 个）
值得关注的有：
- [#7110](https://github.com/earendil-works/pi/pull/7110) fix: 防止启动后会话切换导致重复消息
- [#7114](https://github.com/earendil-works/pi/pull/7114) feat: 为 OpenRouter OAuth 登录添加手动回调粘贴（适配 SSH 场景）
- [#6654](https://github.com/earendil-works/pi/pull/6654) feat: 增加 `promptCacheKey` 流选项（已开放 12 天，待整合）
- [#7117](https://github.com/earendil-works/pi/pull/7117) feat: 扩展创建评估（新开放的扩展能力测试）

## 4. 社区热点
| 议题 | 评论数 | 👍 | 链接 | 核心诉求 |
|---|---|---|---|---|
| TUI 全屏重绘清除终端滚动条 | 15 | 0 | [#6050](https://github.com/earendil-works/pi/issues/6050) | 交互模式下滚动条跳跃，根因在核心渲染器，已被关闭（标记为“no-action”） |
| Copilot Enterprise 无法完成 compaction | 13 | 11 | [#6768](https://github.com/earendil-works/pi/issues/6768) | 使用 Copilot Enterprise 许可证时 Compaction 失败，返回 421/400 错误，11 个赞表明广泛受影响 |
| TUI 在流式时占用完整 CPU 核心 | 7 | 0 | [#6665](https://github.com/earendil-works/pi/issues/6665) | 长会话中 TUI 占用 100% CPU，原因是 `Intl.Segmenter` 未缓存且逐 chunk 重建 Markdown，已有 inprogress 标签 |
| 确认对话框内空滚动闪烁 | 5 | 3 | [#5990](https://github.com/earendil-works/pi/issues/5990) | 当对话框内容高于终端时连续重绘，zoom out 后消失，inprogress |
| Tab 补全后多出空格阻止参数触发 | 5 | 0 | [#5593](https://github.com/earendil-works/pi/issues/5593) | `/sb-l<Tab>` 产生 `/sb-list ` 导致后续空格无法激活参数补全，inprogress |

分析：**Compaction 相关的 Bug 是社区最痛的点**（#6768 点赞数最高），其次为 TUI 性能与交互流畅度。这些议题均已有关注，部分已进入 inprogress 状态。

## 5. Bug 与稳定性
按严重程度排列，标注是否已有 fix PR：

| 严重度 | Issue | 表现 | 修复状态 |
|---|---|---|---|
| 🔴 严重 | [#6665](https://github.com/earendil-works/pi/issues/6665) | TUI 在模型流式时 100% 占用单核 | inprogress（7月15日开启，无外部 PR） |
| 🔴 严重 | [#7020](https://github.com/earendil-works/pi/issues/7020) | Compaction 后 Pi 不继续响应（协调者会话场景） | inprogress，尚无 PR |
| 🟠 中 | [#7067](https://github.com/earendil-works/pi/issues/7067) | 模型切换导致 GPT 返回 HTML 错误、Qwen enable_thinking 400 | 已关闭（no-action），但问题仍在 |
| 🟠 中 | [#7048](https://github.com/earendil-works/pi/issues/7048) | Compaction 总结因 token 达到上限而被截断，但未检测 `stopReason:'length'` | 开放，尚无 PR |
| 🟠 中 | [#7064](https://github.com/earendil-works/pi/issues/7064) | WSL 下绝对 Windows 路径处理错误，工具调用失败 | 开放，尚无 PR |
| 🟠 中 | [#7113](https://github.com/earendil-works/pi/issues/7113) | 当 pi.dev 目录不可达时，`/login` 输入 API key 后 TUI 永久冻结 | 已关闭（untriaged），紧急修复未安排 |
| 🟡 低 | [#7069](https://github.com/earendil-works/pi/issues/7069) | 升级到 v0.82.0 后 `bash` 工具持续报验证错误 | 已关闭（no-action），可能由 #7056 的 PR 间接修复 |
| 🟡 低 | [#7077](https://github.com/earendil-works/pi/issues/7077) | 任务完成后状态仍显示“Working...” | 已关闭（no-action），需 UX 改进 |

## 6. 功能请求与路线图信号
- **OpenRouter 手动回调粘贴**（#7078 → PR #7114 待合并）：支持 SSH/远程环境下的 OAuth 登录流程。
- **Session-affinity 头转发**（#7107, #7108, #7104 等多条重复 Issue）：让自定义提供商获得会话亲和性，本周现大量用户请求，有可能纳入 v0.83。
- **RPC 调用 `refreshModels`**（#7087）：允许程序化强制刷新模型列表，当前已关闭（no-action），但社区有明确需求。
- **扩展创建评估框架**（PR #7117）：正扩展 eval 能力，为即将到来的 Pi 扩展生态做准备。
- **工具输出截断限制可配置**（#7066）：本地模型用户请求更细粒度控制，尚未有 PR，但属于合理路线图项。
- **提示缓存键覆盖**（PR #6654）：`promptCacheKey` 选项，等待合并，将提升高级用户对缓存的控制。

## 7. 用户反馈摘要
- **正面反馈**：多位用户对新模型支持（Claude Opus 5）表示欢迎（#7076 有 +1），OpenRouter 登录功能让 SSH 用户惊喜（#7078）。
- **负面痛点**：
  - “Compaction 后在长协调者会话中 Pi 停滞不前” —— @dpetrou-continua (#7020)
  - “Copilot Enterprise 的 Compaction 完全无法使用” —— @MojangPlsFix（11 赞，#6768）
  - “每次升级后都害怕 bash 工具验证失败” —— @kexul (#7069)
  - “WSL 下路径处理太脆弱，经常被迫用命令行手动修复” —— @lionkor (#7064)
  - “模型切换几乎没有校验，用完 token 才发现” —— @dust617 (#7067, #7065)
- **使用场景**：用户倾向于将 Pi 用作长期“协调器”会话，而非单一任务，这对 compaction、上下文管理提出更高要求。

## 8. 待处理积压
以下 Issue/PR 长期未得到维护者响应或进展缓慢，需社区关注：

| 类型 | 编号 | 创建日期 | 状态 | 说明 |
|---|---|---|---|---|
| Issue | [#5593](https://github.com/earendil-works/pi/issues/5593) | 2026-06-10 | inprogress | Tab 补全空格问题，已 47 天未推进 |
| Issue | [#5990](https://github.com/earendil-works/pi/issues/5990) | 2026-06-23 | inprogress | 对话框闪烁，已 33 天 |
| Issue | [#6665](https://github.com/earendil-works/pi/issues/6665) | 2026-07-15 | inprogress | CPU 100% 核心问题，已 11 天 |
| Issue | [#6768](https://github.com/earendil-works/pi/issues/6768) | 2026-07-17 | open | Compaction on Copilot Enterprise，10 赞，急于解决 |
| Issue | [#7048](https://github.com/earendil-works/pi/issues/7048) | 2026-07-24 | open | Compaction 摘要截断，最近但无响应 |
| PR | [#6654](https://github.com/earendil-works/pi/pull/6654) | 2026-07-14 | open | promptCacheKey 选项，12 天未合并 |
| PR | [#7031](https://github.com/earendil-works/pi/pull/7031) | 2026-07-23 | open | 测试默认离线运行，3 天未审阅 |

---

**总结**：Pi 项目在 v0.82.1 中引入期待已久的 Claude Opus 5，并修复了一批影响日常使用的 Bug。社区最关心的 Compaction 稳定性、TUI 性能问题仍在持续改进中，WSL/跨平台兼容性也是近期短板。建议维护者优先跟进 #6768、#6665 和 #7020 等高频影响问题，同时加速 #6654 和 #7114 等高质量 PR 的合并，以回应用户对扩展性和远程环境支持的需求。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-07-26

## 1. 今日速览

过去24小时项目保持**高活跃度**：共处理 **76 条 Issue**（新开/活跃 57，关闭 19）和 **199 条 PR**（待合并 117，已合并/关闭 82）。无新版本发布，但大量 PR 正在推进，涵盖 MCP 安全、Azure 认证、守卫规则修复、UI 优化等多个方向。社区参与积极，累计 **95 个讨论热度（👍）** 体现用户对稳定性和功能扩展的迫切需求。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日合并/关闭了 **82 个 PR**，其中多项关键修复已落地，显著提升了项目的安全性与稳定性：

### 🔒 已合并/关闭的重要 PR
- **#34340** `fix(mcp): stop leaking upstream server credentials in tool-call 403` — 修复了通过工具调用泄露上游 MCP 服务凭证的安全漏洞，现在未授权用户只能看到模糊的错误信息。
- **#34600** `fix(ci): scope UI lint to the files a PR actually changed` — CI 改进，避免因无关文件改动导致 UI lint 失败，提升开发效率。
- **#34656** `fix(proxy): stop litellm/proxy from shadowing installed packages on sys.path` — 解决了代理脚本运行时 `litellm/proxy/a2a` 目录遮蔽已安装 `a2a` SDK 的问题，使 A2A 代理调用正常工作。
- **#34598** `fix(cost-optimization): swap methodology Collapse for a shadcn HoverCard` — 成本优化页面 UI 改进，将“节省计算方式”说明从笨重的折叠组件改为悬浮提示，提升用户体验。

### 🚀 今日新提出的重要开放 PR
- **#34664** `fix(e2e)` — 防止单个 e2e 测试破坏共享代理环境，解决因测试导致 Redis 中断、Bedrock 守卫规则污染等问题。
- **#34663** `fix(proxy): restore provider pass-through routes under SERVER_ROOT_PATH` — 修复了在 `SERVER_ROOT_PATH` 下所有提供商的透传路由返回 404 的严重问题。
- **#34658 / #34655** `fix/feat(azure/realtime)` — 支持 Azure AD（Entra ID）身份认证连接实时 WebSocket，替代仅支持 api-key 的旧方案。
- **#34651** `feat(machgen): add MachGen image generation provider` — 新增 MachGen 图像生成提供商支持。
- **#34622** `feat(prometheus): support wildcard metric name` — Prometheus 指标配置支持通配符，方便批量过滤标签。

项目整体在**安全性、兼容性、可观测性**三个维度稳步推进，尤其针对 MCP 和代理路由的修复值得关注。

## 4. 社区热点

评论数最高的 Issue 揭示了用户最关心的三大痛点：

| 排名 | Issue | 评论数 | 👍 | 核心诉求 |
|------|-------|--------|-----|----------|
| 🥇 | [#26395](https://github.com/BerriAI/litellm/issues/26395) [CLOSED] | 22 | 25 | DeepSeek V4 Pro 多轮对话失败：首轮成功，后续轮次因 `reasoning_content` 剥离导致 400 错误。该 Issue 已关闭，可能已通过内部 PR 修复。 |
| 🥈 | [#16021](https://github.com/BerriAI/litellm/issues/16021) [OPEN] | 16 | 3 | OpenRouter 流式响应丢失成本信息（`usage.cost`），非流式正常。持续 9 个月未解决，社区呼声较高。 |
| 🥉 | [#25762](https://github.com/BerriAI/litellm/issues/25762) [OPEN] | 15 | 14 | 标准版 SSO 用户 5 人限制 —— 用户希望取消限制，以满足企业级部署需求。 |

其他高评论 Issue 包括：
- **#14052**（9 评论）：`x-litellm-tags` 标签路由不按预期 fallback，影响请求可靠性，已标识为 P0 阻塞用例。
- **#20078**（6 评论）：`/v1/audio/speech` 端点对 Qwen3-TTS 模型强制要求 `voice` 参数，且剥离自定义参数，导致 TTS 服务不可用。

## 5. Bug 与稳定性

今日报告的 Bug 按严重程度排列如下：

### 🔴 严重（影响核心功能/安全）
- **#26395** ([CLOSED] DeepSeek V4 多轮对话失败) — 已关闭，推测已修复。
- **#16021** ([OPEN] OpenRouter 流式成本丢失) — 长期未修复，影响计费准确性。
- **#14052** ([OPEN] P0/阻塞) `x-litellm-tags` 路由不 fallback — 导致关键业务请求不可用。
- **#33820** ([OPEN] aiohttp 3.14.x 连接池污染) — 导致跨提供商“连接超时”偶发失败，影响范围广。

### 🟡 中等（影响特定场景）
- **#20078** ([OPEN] Qwen3-TTS voice 参数必填) — 音频服务不可用。
- **#24152** ([OPEN] 密钥级模型速率限制不触发 fallback) — 资源管理缺陷。
- **#26398** ([OPEN] MCP 工具调用时字符串长度限制错误) — Claude Code 集成故障。
- **#26413** ([OPEN] `"think": false` 被忽略) — 推理模型仍返回思考内容。
- **#34636** ([OPEN] Redis 缓存测试使用 `url` 字段失败) — 新报告，UI 配置路径问题。
- **#22747** ([OPEN] Azure Responses API 超时问题) — GPT-5-PRO 长时间推理时 Socket 断开。
- **#32903** ([OPEN] `GET /v1/models` 所有模型显示 `owned_by: "openai"`) — 信息误导。

### 🟢 低影响（性能/体验）
- **#24398** ([CLOSED] 导入 litellm 时 RAM 尖峰) — 已关闭，可能已优化。
- **#26192** ([OPEN] RDS IAM token 过期导致事件循环死锁) — 影响健康检查。
- **#33817** ([OPEN] 守卫监控显示 "Flagged" 而非 "Blocked") — UI 标签错误。
- **#29652** ([CLOSED] 模型级守卫不执行) — 已关闭，推测修复。

### 🔧 已有对应修复 PR 的 Bug
- **#34663** PR 修复 `SERVER_ROOT_PATH` 下透传路由 404。
- **#34658 / #34655** PR 修复 Azure WebSocket 认证。
- **#34656** PR 修复 `sys.path` 阴影问题。
- **#34340** PR 修复 MCP 凭证泄漏（已合并）。

## 6. 功能请求与路线图信号

以下新功能需求社区关注度高，且有迹象表明可能被纳入下一版本：

| Issue | 功能 | 可行性判断 |
|-------|------|-----------|
| [#25762](https://github.com/BerriAI/litellm/issues/25762) | 取消标准版 SSO 5 用户限制 | 15 评论 + 14 👍，企业用户强需求，可能与商业计划调整相关 |
| [#33960](https://github.com/BerriAI/litellm/issues/33960) | 路由组支持 per-group `allowed_fails / cooldown_time` | 与现有路由能力互补，已有详细设计 |
| [#34357](https://github.com/BerriAI/litellm/issues/34357) | 添加 OpenInfer 提供商 | 提供商原生集成请求，社区贡献意愿明确 |
| [#34662](https://github.com/BerriAI/litellm/issues/34662) | 提供商凭据的周期性可用性计划 | 新提出，暂无 PR，但与现有 `credential_info` 结构一致 |
| [#34566](https://github.com/BerriAI/litellm/issues/34566) | 发布完整的 MCP DCR 桥接流程 | 已关联 v1.93.0，请求文档补全 |
| [#34651](https://github.com/BerriAI/litellm/pull/34651) | 新增 MachGen 图像生成提供商 | **已有 PR**，几乎确定纳入下个版本 |

此外，今日有 **5 个新增提供商/集成相关的 PR**（MachGen, OpenInfer, Azure AD, Prometheus 通配符），表明项目在**生态扩展**和**可观测性**上持续加码。

## 7. 用户反馈摘要

从 Issues 和 PR 评论中提炼用户真实反馈：

- **DeepSeek V4 Pro 多轮失败**：用户 `@anjun` 反馈“首轮成功，后续轮次全部失败”，涉及 `reasoning_content` 剥离，影响多轮对话任务。社区 25 个 👍 表明影响面广。
- **OpenRouter 流式成本信息丢失**：用户 `@bbarwik` 表示“非流式工作正常，流式模式下 `usage.cost` 丢失”，导致无法准确计费。该 Issue 已存在 9 个月，用户耐心接近极限。
- **标签路由 fallback 缺失**：用户 `@TeddyAmkie` 写道“期望如果 x-litellm-tags 提供的标签失败，请求应 fallback 到相似标签”，但实际无任何 fallback，导致业务中断。被标记为 P0/阻塞。
- **音频端点不灵活**：用户 `@miesgre` 反馈 Qwen3-TTS 强制要求 `voice` 参数，且自定义参数被剥离，导致无法使用特定模型特性。
- **推理模型 `think` 参数被忽略**：用户 `@slavb18` 设置 `"think": false` 后仍收到推理内容，认为这是关键配置漏洞。
- **aiohttp 连接池污染**：用户 `@deepanshululla` 报告升级到 v1.91.0 后偶发跨提供商超时，“问题难以复现但严重影响生产环境”。
- **Redis 缓存测试报错**：用户 `@mikew` 表示“UI 提示输入 `redis://` URL，但测试连接失败”——期望 UI 能正确处理 URL 格式。
- **用户对 PR 改进表示认可**：如 #34340 修复凭证泄漏后，社区反应积极；#34600 提升 CI 体验也被认为是“早该做的”。

## 8. 待处理积压

以下 Issue 和 PR 长期未获得回复或更新，需维护者关注：

### 📌 长期未响应的严重 Issue
| Issue | 创建时间 | 最后更新 | 问题 |
|-------|----------|----------|------|
| [#16021](https://github.com/BerriAI/litellm/issues/16021) | 2025-10-28 | 2026-07-25 | OpenRouter 流式成本丢失，已标记 `stale`，但用户持续关注 |
| [#14052](https://github.com/BerriAI/litellm/issues/14052) | 2025-08-29 | 2026-07-25 | 路由标签不 fallback，P0 阻塞，被标记 `stale` |
| [#20078](https://github.com/BerriAI/litellm/issues/20078) | 2026-01-30 | 2026-07-25 | TTS voice 参数问题，标记 `stale` |
| [#22747](https://github.com/BerriAI/litellm/issues/22747) | 2026-03-04 | 2026-07-25 | Azure Responses API 超时，标记 `stale` |
| [#24152](https://github.com/BerriAI/litellm/issues/24152) | 2026-03-19 | 2026-07-25 | 密钥级速率限制不触发 fallback，无 fix PR |

### 📌 长期未合并的 PR
| PR | 创建时间 | 最后更新 | 状态 |
|----|----------|----------|------|
| [#30873](https://github.com/BerriAI/litellm/pull/30873) | 2026-06-20 | 2026-07-25 | OpenOTel v2 追踪目的地，仍为 OPEN，可能需要评审 |
| [#32958](https://github.com/BerriAI/litellm/pull/32958) | 2026-07-11 | 2026-07-25 | 团队批量更新成员，仍为 OPEN |
| [#34192](https://github.com/BerriAI/litellm/pull/34192) | 2026-07-21 | 2026-07-25 | 批量任务分页游标修复，仍为 OPEN |
| [#33665](https://github.com/BerriAI/litellm/pull/33665) | 2026-07-17 | 2026-07-25 | MCP 工具路由通过 server_id，仍为 OPEN |

> 建议维护者优先评估 **#16021**（流式成本）和 **#14052**（路由标签）这两个长期阻塞用户的 Issue，并加快 **#33665**（MCP 工具路由）等安全相关 PR 的合并步伐。

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

好的，以下是基于您提供的 GitHub 数据生成的 Temporal 项目日报。

---

# Temporal 开源项目日报 - 2026-07-26

**数据来源:** github.com/temporalio/temporal
**数据日期:** 2026-07-25 至 2026-07-26
**分析师:** AI 智能体与个人 AI 助手领域开源项目分析师

---

### 1. 今日速览

- **Issues 活跃度低迷，核心开发聚焦 PR:** 过去 24 小时内无新增或关闭的 Issue，社区反馈和bug报告活动暂时停滞。然而，PR 活动非常活跃，共有 29 条 PR 更新，其中 23 条处于待合并状态，6 条已合并或关闭，表明项目核心开发团队正在进行密集的代码提交和修复工作。
- **CHASM 调度器成为开发焦点:** 今日 PR 内容高度集中，由 `@davidporter-id-au` 提交的一系列 PR 几乎全部聚焦于 CHASM (新的调度器后端) 的稳定性、边界处理和性能优化。这标志着项目正**从功能开发阶段向稳定性和健壮性打磨阶段过渡**。
- **项目健康度评估: 良好（内部活跃，外部冷却）。** 虽然社区反馈和外部贡献者活动较少，但核心团队的开发节奏非常强劲，尤其是在修复复杂模块（如 CHASM）的内部缺陷和提升工程韧性方面。项目功能演进和 Bug 修复的推进速度很快。

### 2. 版本发布

*（无）*

### 3. 项目进展

过去 24 小时，项目在 **CHASM 调度器**和**版本发布准备**方面取得了明确进展。以下是已合并/关闭的重要 PR：

- **发布分支准备 (`#11287`，已合并):** 自动化机器人 `temporal-cicd[bot]` 完成了 1.32.0 版本发布分支的准备工作，包括覆盖治理文件和更新依赖项。这表明 **Temporal 1.32.0 正式版本已接近就绪**。
    - [https://github.com/temporalio/temporal/pull/11287](https://github.com/temporalio/temporal/pull/11287)
- **CHASM Nexus 回调时间戳修复 (`#10915`，已合并):** 一个重要的修复，确保 CHASM Nexus 操作完成事件的时间戳使用的是异步回调中报告的实际关闭时间，而非服务器处理时间。这显著提高了审计和计费场景中时间戳的准确性。
    - [https://github.com/temporalio/temporal/pull/10915](https://github.com/temporalio/temporal/pull/10915)
- **CHASM 调度器请求去重 (`#11284`，已合并):** 修复了 CHASM 调度器未根据请求 ID 对 `PatchSchedule` 和 `UpdateSchedule` 进行去重的问题。这避免了因客户端重试导致的重复操作，提升了系统的幂等性保证。
    - [https://github.com/temporalio/temporal/pull/11284](https://github.com/temporalio/temporal/pull/11284)
- **测试与导入修复 (`#11285`，已合并， `#11286`，已合并):** 修复了匹配分区管理器测试中的动态配置导入问题，并通过自动化流程更新了测试分片盐值，以优化测试均衡性和效率。

此外，还有 23 个待合并的 PR，绝大部分是来自 `@davidporter-id-au` 对 CHASM 调度器的一系列修复，这些修复一旦合并，将极大提升该新后端的健壮性。

### 4. 社区热点

今日社区讨论的热点集中在 **PR `#11259`**，该 PR 持续受到关注。

- **PR `#11259`: VTS (Versioning Transition State) 的优化** - 作者: `@feiyang3cat`
    这是今日最受关注的 PR，虽然其评论和反应数未提供，但其内容涉及**在 `DescribeWorkflowExecution` 中增加运行时字段**，允许用户检查时间跳过的运行时状态。这直接关系到**版本控制**和**工作流调试**的易用性。背后的核心诉求是**增加用户对工作流运行时内部状态的可观测性**，特别是当涉及到复杂的版本迁移和时间跳过逻辑时。
    - [https://github.com/temporalio/temporal/pull/11259](https://github.com/temporalio/temporal/pull/11259)

其他由 `@davidporter-id-au` 提交的大量 PR 也构成了今日的讨论热点，但这些更多是代码审查行为，而非公开社区讨论。焦点集中于对 CHASM 调度器各种边缘情况的系统性修复。

### 5. Bug 与稳定性

今日 PR 日志暴露了多个关键的 Bug 和稳定性问题，主要集中在 CHASM 调度器模块，这些问题均已创建修复 PR。

**严重 Bug (已修复/有修复PR):**

1.  **空指针解引用 (`#11276`，修复中):** `WorkflowHandler.UpdateSchedule` 在处理 `nil` 请求时会 panic。这是一个严重的运行时崩溃问题，尽管有全局恢复机制，但仍会导致客户端得到非预期的错误响应。
    - [https://github.com/temporalio/temporal/pull/11276](https://github.com/temporalio/temporal/pull/11276)
2.  **输入校验缺失 (`#11275`，修复中):** `PatchSchedule` 接口在处理 `nil patch` 时也会 panic。与上一条类似，是另一个可能导致服务异常的入口点。
    - [https://github.com/temporalio/temporal/pull/11275](https://github.com/temporalio/temporal/pull/11275)
3.  **状态不一致问题 (`#11278`，修复中):** 使用 `InitialPatch.Pause` 创建的 CHASM 调度器启动时未正确应用暂停状态，可能导致立即产生不期望的执行动作。
    - [https://github.com/temporalio/temporal/pull/11278](https://github.com/temporalio/temporal/pull/11278)
4.  **逻辑错误导致死锁/乱序 (`#11280`，修复中):** 修复了 `InvokerMaxStartAttempts` 配置的边界计算错误，该错误可能导致工作流启动尝试次数超过预期。
    - [https://github.com/temporalio/temporal/pull/11280](https://github.com/temporalio/temporal/pull/11280)
5.  **数据竞争/脏写 (`#11288`，修复中):** 这是 CHASM 测试引擎中的两个 Bug，直接导致了 VT (版本转换) 不匹配，进而可能导致逻辑任务无法生成。这影响了测试的可信度。
    - [https://github.com/temporalio/temporal/pull/11288](https://github.com/temporalio/temporal/pull/11288)
6.  **时间边界错误 (`#11281`，修复中):** 自动启动的重试逻辑中，对“追赶截止时间”的判断错误，可能导致本应跳过的过期任务被重新执行。
    - [https://github.com/temporalio/temporal/pull/11281](https://github.com/temporalio/temporal/pull/11281)

**中等严重性 Bug (有修复PR):**

- 协议缓冲区格式校验缺失 (`#11282`，修复中): 允许了格式错误的 `Duration` 输入，可能造成不可预期的行为。
- V2-to-V1 调度器迁移时，起始边界设置错误 (`#11277`，修复中)。

**总结：** 今日发现并修复了大量直接影响稳定性的 Bug，表明项目正在进行深入的质量内审，对系统的健壮性要求很高。

### 6. 功能请求与路线图信号

- **增强可观测性 (`#11259`):** 在 `DescribeWorkflowExecution` 中暴露版本和时间跳过状态，这是一个明确的功能增强信号。表明项目正在关注用户对于**运行时内部状态可见性**的需求，很可能被纳入下一个或后续版本。
- **监控指标增强 (`#11255`，待合并):** 新增 `shardinfo_immediate_queue_backlog_age` 指标，允许用户监控**即时任务队列的“老化”情况**，而不仅仅是大小（`lag`）。这反映了对**运维监控精细化**的追求。
    - [https://github.com/temporalio/temporal/pull/11255](https://github.com/temporalio/temporal/pull/11255)
- **复制与数据一致性增强 (`#11257`，待合并):** 当复制任务应用于“当前执行记录”丢失的工作流时，自动重建该记录。这是一个重要的**数据自修复**能力，提升了多集群部署场景下的韧性，是生产环境高可用性的关键功能。
    - [https://github.com/temporalio/temporal/pull/11257](https://github.com/temporalio/temporal/pull/11257)

### 7. 用户反馈摘要

由于今日无公开Issue，用户直接反馈较少。但我们可以从 PR 的上下文推断用户痛点：

- **用户痛点：崩溃与非预期行为。** 多项修复（如 `#11276`， `#11278`）针对的是操作调度器时可能遇到的崩溃 (`nil request`) 或逻辑错误（暂停状态未生效）。这些错误在特定操作流程下可能导致终端用户困惑或服务中断。
- **监测与调试的痛点。** `#11255` 和 `#11259` 两个 PR 分别从监控和可观测性角度切入，反映了用户在运营和开发过程中对**更精细的监控指标**和**更强大的调试能力**的持续需求。

### 8. 待处理积压

仓库健康度良好，暂无长期未被响应的关键 Issue。但以下是值得关注的待合并 PR，它们属于功能增强或修复，若长期积压可能影响项目演进：

1.  **`#11155`: Log NotFound errors when adding speculative WFT to matching**
    - 作者: `@RajeshRajendiran` | 创建: 2026-07-20
    - 这是一个重要的稳定性改进，确保在面对特定类型的错误时能正确记录日志。已待合并6天，建议关注其合并进度。
    - [https://github.com/temporalio/temporal/pull/11155](https://github.com/temporalio/temporal/pull/11155)

2.  **`#11257`: Reconstruct missing current execution record on replication apply**
    - 作者: `@jiechenz` | 创建: 2026-07-24
    - 如前所述，这是一个增强复制场景下数据一致性的关键功能。该功能涉及核心持久化和复制逻辑，需要细致的审查。
    - [https://github.com/temporalio/temporal/pull/11257](https://github.com/temporalio/temporal/pull/11257)

**总结:** 目前积压的 PR 更新普遍较新（1天以内），没有发现因长期无人问津而成为“老赖”的 Issue 或 PR。项目维护者响应速度快，项目总体迭代健康。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*