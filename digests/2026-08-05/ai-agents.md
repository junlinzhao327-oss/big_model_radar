# OpenClaw 生态日报 2026-08-05

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-04 23:28 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

## 1. 今日速览

OpenClaw 项目在过去 24 小时内保持极高活跃度：Issue 更新 500+ 条（新开/活跃 442 条，关闭 58 条），PR 更新 500+ 条（待合并 384 条，已合并/关闭 116 条），并发布了 2 个补丁版本。社区热度集中在 DeepSeek v4 Flash 静默失败（104 条评论，已关闭）、Realtime voice 状态无界增长（58 条评论，仍开放）等稳定性问题上。值得注意的是，多个 P1/diamond-lobster 级问题已有对应修复 PR 进入审查流程，显示维护团队响应及时；但 Subagent 完成静默丢失（#44925）、多智能体编排不稳定（#43367）等 3 月开启的长期问题仍悬挂，是当前健康度的主要扣分项。

## 2. 版本发布

过去 24 小时发布了 2 个补丁版本，均为 Bug 修复，未发现破坏性变更或迁移注意事项。

**v2026.7.1-2**
- **npm 插件元数据兼容性**：接受新版 npm

---

## 横向生态对比

# 横向对比分析报告：AI 智能体与个人 AI 助手开源生态（2026-08-05）

---

## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态正处于 **“高活跃、强分化、重稳定”** 的阶段：头部项目（OpenClaw、Hermes Agent）单日 Issue/PR 更新均破 500，社区参与度极高；与此同时，可观测性、流式数据完整性、插件接口稳定性、多智能体编排可靠性等问题在多个项目中集中爆发，说明生态正从“功能搭建”转向“生产级打磨”。企业级诉求（多租户、预算管控、企业版兼容）明显升温，而底层基础设施（Temporal）也在同步推进复制架构与调度可靠性，暗示整个生态开始为大规模、高可靠部署做铺垫。整体而言，生态依然高速演进，但稳定性和信任建设已成为下一阶段竞争焦点。

---

## 2. 各项目活跃度对比

| 项目 | Issue 更新量（新开/活跃 / 关闭） | PR 更新量（待合并 / 合并关闭） | Release | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 500+（442 / 58） | 500+（384 / 116） | 2 个补丁版本 | 极高活跃，响应及时；但 Subagent 丢失、多智能体编排等长期问题仍悬挂，健康度“活跃但承压” |
| **Hermes Agent** | 500+（446 / 54） | 500+（413 / 87） | 无 | 功能拓展与稳定性加固并行，87 个 PR 合并/关闭，健康度“良好” |
| **OpenHands SDK** | 19（16 / 3） | 50（45 / 5） | 无 | 高强度功能开发 + 稳定性修复并行，但 45 个待合并 PR 对 review 带宽构成压力，健康度“较好但有瓶颈” |
| **Pi** | 60（11 / 49） | 31（8 / 23） | 无 | 关闭率约 82%，维护响应迅速，健康度“优秀” |
| **LiteLLM** | 83（52 / 31） | 242（161 / 81） | 无 | 快速迭代，但多个跨版本 bug 复活、流式丢块未解决，健康度“活跃但风险累积” |
| **Temporal** | 2（新开 1 / 关闭 1） | 38（23 / 15） | 无 | 架构演进期，合并率较高；但 #10737 严重 issue 50 天无修复，健康度“稳健但有阻塞项” |

> 注：OpenClaw 与 Hermes 的更新量达到数据展示上限，实际可能更高；Pi 的 Issue 关闭率显著领先，体现高处理效率。

---

## 3. OpenClaw 在生态中的定位

OpenClaw 目前是个人 AI 智能体生态中的 **“核心参照”项目**，其定位可从三个维度理解：

- **社区规模与活跃度领跑**：单日 Issue/PR 更新量双双触达 500+ 上限，远超 Pi、OpenHands SDK 等同类，与 Hermes Agent 并列第一梯队；同时连续发布 2 个补丁版本，说明维护团队不仅跟进速度快，还保持高频发版节奏。
- **技术路线侧重多智能体协同与实时交互**：从今日热点问题可看出，OpenClaw 的核心场景包括 **Subagent 任务编排**、**多智能体协同**、**Realtime voice 状态管理**，明显聚焦于“多个智能体协同完成复杂任务”，而非单会话对话。
- **优势与隐忧并存**：优势在于社区反馈极多、P1 问题多能快速获得修复 PR，问题响应闭环能力强；隐忧在于 3 月开启的 Subagent 结果静默丢失、多智能体编排不稳定等长期问题仍未解决，这会导致依赖其编排能力的高阶用户信任度受损。

与 Hermes 相比，Hermes 更突出插件接口扩展、多租户架构和桌面端体验；与 Pi 相比，Pi 走轻量终端交互路线，更强调跨提供商兼容与本地效率。OpenClaw 则以“多智能体编排 + 大规模社区驱动”形成差异，是生态中观察智能体协作复杂度的最佳样本。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **可观测性与追踪完整性** | OpenHands SDK、LiteLLM、OpenClaw | 子 agent 共享 trace_id 但产生交错 span；MCP 工具调用被拆分为多个 trace；ACP 会话完全不可见；DeepSeek 静默失败无法察觉。均要求完善 trace 传播与 span 标记，确保训练和排障数据可信。 |
| **流式响应与数据完整性** | LiteLLM、Pi、OpenClaw | Anthropic 兼容端点 thinking 块后丢失首个 text_delta；Bedrock 推理模型同样丢块；重试成功后界面残留错误提示。流式场景的**确定性**成为用户体验核心痛点。 |
| **插件/扩展接口稳定性** | Hermes Agent、OpenHands SDK、Pi | 插件作者等待接口稳定以便发布；Canvas Extensions 需要 manifest、REST API 等完整规划；发布二进制缺少 `node:sqlite` 导致插件崩溃。接口的一致性和运行时依赖管理是共性瓶颈。 |
| **多智能体/子代理可靠性** | OpenClaw、OpenHands SDK、Temporal | Subagent 结果静默丢失；子 agent 会话与父 trace 关系混乱；跨集群 failover 后子工作流丢失需恢复机制。多级任务编排的**状态一致性和故障恢复**成为刚需。 |
| **企业级与多租户能力** | Hermes、LiteLLM、Pi、Temporal | 多租户架构、per-model 预算、key 权限过滤、Copilot Enterprise/GHE.com 兼容、Worker Deployment 版本 GC 等。企业采购和规模化部署正在倒逼项目补齐管理、安全、合规能力。 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|---|---|---|---|
| **OpenClaw** | 多智能体编排、实时语音交互、Subagent 任务分发 | 追求复杂任务自动化的开发者/研究团队 | 强调子代理和实时会话状态管理，社区驱动，迭代速度快 |
| **Hermes Agent** | 通用个人 AI 助手，桌面端体验、插件系统、多租户 | 桌面端重度用户、企业团队 | 提供 TUI/桌面端，支持 MEMORY.md/USER.md CRUD，关注工作区隔离（X-Hermes-Workspace） |
| **OpenHands SDK** | 软件工程 Agent SDK，面向代码开发场景 | 构建代码智能体的开发者 | 提供 REST API 与 MCP 集成，强调可观测性（trace/span）与工具动态协调，正推进 Canvas Extensions |
| **Pi** | 终端原生 AI 助手，多 AI 提供商接入，RPC 控制 | CLI 用户、Windows 用户、嵌入式 UI 场景 | 轻量级、基于 Bun/Node，支持 Unix Socket/TCP RPC，内置多种提供商（Cortecs、LLM Gateway） |
| **LiteLLM** | AI 网关/代理，统一 LLM API，成本与预算管理 | 企业平台团队、API 管理者 | 代理层架构，聚焦路由、限流、预算、可观测性，支持 100+ 提供商 |
| **Temporal** | 分布式工作流引擎（非 AI 原生，但支撑 Agent 编排） | 后端工程师、平台团队 | 提供持久化执行、故障恢复、复制/搬迁，CHASM 调度器与 Worker Versioning 是当前重点 |

简言之：**OpenClaw / Hermes / Pi** 面向终端用户，竞争点为交互体验和智能体能力；**OpenHands SDK** 面向软件 Agent 开发，强调代码场景和可观测性；**LiteLLM** 是通用 LLM 基础设施，解决接入和管理问题；**Temporal** 则是更底层的可靠性底座，为任意 Agent 工作流提供事务性保证。

---

## 6. 社区热度与成熟度

| 梯队 | 项目 | 特征 |
|---|---|---|
| **第一梯队：超高频迭代** | OpenClaw、Hermes Agent、LiteLLM | 单日 PR 更新均超 200，合并/关闭量大，功能高速推进；同时稳定性欠账较多（OpenClaw 长期 issue、LiteLLM 跨版本 bug），属于“跑得快，也摔得多”的阶段。 |
| **第二梯队：均衡发展** | Pi、OpenHands SDK | 活跃度中高，但 Issue 关闭率、PR 合并效率高，维护者对反馈响应及时。Pi 的 Issue 关闭

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目日报 — 2026-08-05

## 今日速览

过去 24 小时项目活跃度极高：**500 条 Issue 更新**（新开/活跃 446 条，关闭 54 条）与 **500 条 PR 更新**（待合并 413 条，合并/关闭 87 条）均达到数据展示上限，实际吞吐量可能更高。无新版本 Release 发布，但 87 个 PR 完成合并/关闭，集成节奏稳定。当前社区讨论焦点集中在**插件接口扩展**（#64182，19 评论）与**多租户架构能力**（#34352，13 评论）两大方向，同时 P1 级稳定性 bug（终端守卫崩溃、Discord 网关重连循环）已出现对应修复 PR，项目处于**功能拓展与稳定性加固并行**的健康状态。

## 版本发布

今日无新版本发布。上一个已知版本为受回归问题影响的 **0.19.1**（见 #76886）。

## 项目进展

过去 24 小时 **87 个 PR 被合并/关闭**。展示的 20 条高热度 PR 均处于待合并状态，但两个高影响 Issue 已关闭，表明对应修复已合入主干：

- **[已关闭] #38855（P1）** 桌面端工作目录设置不覆盖旧的已记住 workspace cwd — `Settings -> Workspace -> Working Directory` 配置在 `~/.hermes/config.yaml` 中正确设置后，新会话仍可能打开到旧的 localStorage 目录。该问题已关闭，直接影响桌面端多工作区用户。 https://github.com/NousResearch/hermes-agent/issues/38855

- **[已关闭] #75959（P2）** 桌面端 Skills/Toolsets 面板加载失败 — `GET /api/tools/toolsets` 因重复执行 Nous 订阅检查耗时 ~19 秒，超过 15 秒 IPC 超时阈值。性能问题已解决。 https://github.com/NousResearch/hermes-agent/issues/75959

待合并 PR 中，以下修复值得关注（对应已报告的 bug 或能力补全）：

| PR | 修复/新增内容 | 关联 Issue |
|---|---|---|
| [#78945](https://github.com/NousResearch/hermes-agent/pull/78945) | `lifecycle_guard.py` 捕获 `ValueError: embedded null byte`，修复终端命令因二进制路径崩溃 | #77780, #77703（均为 P1） |
| [#78947](https://github.com/NousResearch/hermes-agent/pull/78947) | TUI 网关恢复会话时，若持久化的 provider 已从配置中删除，回退到配置默认值 | #75128 |
| [#78917](https://github.com/NousResearch/hermes-agent/pull/78917) | 从子进程环境变量中选择性剥离 Hermes-venv 的 `PYTHONPATH`，防止污染 terminal/`execute_code`/cron 子进程 | #74817 |
| [#57887](https://github.com/NousResearch/hermes-agent/pull/57887) | 错误分类器识别 OpenRouter/Groq/Together/Fireworks 聚合器包装的上游 403 错误 | — |
| [#76750](https://github.com/NousResearch/hermes-agent/pull/76750) | 新增 `hermes memory add/replace/remove` 内置 MEMORY.md/USER.md CRUD CLI 命令 | #10771（部分） |
| [#78923](https://github.com/NousResearch/hermes-agent/pull/78923) | API 层增加 `X-Hermes-Workspace` 请求头，按 API 会话绑定工作区，支持上下文发现与任务隔离 | — |

## 社区热点

**最热 Issue 前三名均聚焦基础设施能力：**

1. **[#64182] 插件接口扩展追踪（19 评论）** — 7 月社区 Discord 讨论的沉淀，目标是让长期排队 PR 能稳定发布。评论热度反映了插件作者对接口稳定性的迫切需求。 https://github.com/NousResearch/hermes-agent/issues/64182

2

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-08-05

## 1. 今日速览

过去 24 小时项目活跃度极高：**19 条 Issue 更新**（新开/活跃 16 条，关闭 3 条）、**50 条 PR 更新**（待合并 45 条，已合并/关闭 5 条），无新版本发布。**Canvas Extensions** 成为今日绝对主线——维护者 @VascoSch92 一次性提交了约 10 个相互关联的 issue（#4348–#4357），构成从 manifest 模型、REST API、安全护栏到测试矩阵的完整功能规划，标志着该功能正从讨论走向工程落地。与此同时，可观测性领域出现系列 bug 报告与修复（#4358、#4360、#4359），由 @simonrosenberg 主导推进。整体来看，项目处于**高强度功能开发 + 稳定性修复并行的健康状态**，但 45 条待合并 PR 对 review 带宽构成压力。

## 2. 版本发布

过去 24 小时无新版本发布。

## 3. 项目进展

今日有 5 个 PR 合并/关闭，主要集中在可观测性修复与 MCP 能力补全：

| PR | 标题 | 状态 | 意义 |
|---|---|---|---|
| [#4367](https://github.com/OpenHands/software-agent-sdk/pull/4367) | fix(mcp): reconcile live agent tool snapshots | CLOSED | 支持运行时动态更新 agent 工具列表，对齐 OpenCode 已有行为，是 MCP 集成能力的关键补强 |
| [#4360](https://github.com/OpenHands/software-agent-sdk/pull/4360) | refactor(observability): stop depending on lmnr to propagate trace context into tool workers | CLOSED | 显式传播并行工具调用的 trace context，修复可观测性数据损坏问题（对应 #4358） |
| [#4359](https://github.com/OpenHands/software-agent-sdk/pull/4359) | fix(observability): mark utility LLM spans (title generation, ask_agent) | CLOSED | 为工具性 LLM 调用（generate_title/ask_agent）添加元数据标记，使训练轨迹可被正确识别（对应 #4358） |
| [#4366](https://github.com/OpenHands/software-agent-sdk/pull/4366) | Set AI_AGENT for SDK subprocesses | CLOSED | 为 SDK 子进程设置 `AI_AGENT` 环境变量，与行业趋势对齐，简化 AI agent 的识别 |
| [#4312](https://github.com/OpenHands/software-agent-sdk/pull/4312) | chore(deps): bump aiohttp from 3.13.4 to 3.14.3 | CLOSED | 依赖安全更新，消除已知漏洞风险 |

**重大进展信号**：可观测性领域 #4358 报告的「轨迹损坏/不完整且无任何报错」问题已通过 #4360/#4359 快速闭环（issue 与 PR 同日关闭），体现了项目对数据质量问题的响应速度。MCP 工具动态协调能力落地则直接扩展了 SDK 在复杂工具生态中的实用性。

## 4. 社区热点

今日讨论最活跃的 Issue 集中在两处：

- **[#1317 Consider different default prompts for interactive vs non-interactive agents](https://github.com/OpenHands/software-agent-sdk/issues/1317)**（6 条评论，CLOSED）：由 @neubig 提出，讨论 CLI 用户与云端用户在等待 agent 完成任务时的体验差异——CLI 用户希望更简洁、少啰嗦，云端用户则能接受更详尽的输出。该 issue 创建于 2025-12-04，今日仍被关注，说明**交互模式适配**是社区长期关心的体验议题。

- **[#4267 agent-server (No response from ACP server) when setting up automation using Local ACP, opencode, ollama](https://github.com/OpenHands/software-agent-sdk/issues/4267)**（5 条评论，OPEN）：用户 @azcoffeehabit 报告在配置 GitHub 仓库监控等自动化场景时，agent-server 对 ACP server 无响应。这是一个**影响实际自动化工作流集成的阻塞性 bug**，评论区持续有讨论，当前无明确 fix PR。

**趋势分析**：今日社区热点从「讨论型」（prompt 设计）转向「工程型」（ACP 集成、自动化配置），反映出 SDK 正被更多真实业务场景采用，用户对集成稳定性提出更高要求。Canvas Extensions 系列 issue 虽评论数不多，但体量庞大且由核心维护者系统性提出，是值得密切关注的战略方向。

## 5. Bug 与稳定性

按严重程度排列：

**🔴 高优先级**

- **[#4368 ACP conversations are invisible to Laminar: no LLM spans, no TOOL spans, no token/cost attributes](https://github.com/OpenHands/software-agent-sdk/issues/4368)**（priority:high，无 fix PR）：ACP 会话在 Laminar 中完全不可见——无 LLM span、无 TOOL span、无 token/成本属性，导致 ACP 会话与「agent 从未运行」的会话在结构上无法区分，**直接破坏可观测性**。

- **[#4350 Canvas Extensions: installation persistence — fix disabled-by-default and self-heal auto-enable](https://github.com/OpenHands/software-agent-sdk/issues/4350)**（priority:high，security）：扩展安装存在「默认禁用失效」和「自愈自动启用」两个已确认问题，涉及安全边界。

**🟡 中优先级**

- **[#4358 TOOL span loses parent under parallel tool execution; utility LLM calls leak into the trace](https://github.com/OpenHands/software-agent-sdk/issues/4358)**（已关闭）：两个可观测性 bug 导致导出的训练轨迹损坏/不完整且无报错。**已有 fix PR**（#4360、#4359），已闭环。

- **[#4365 Sub-agent (task) conversations share the parent's trace_id but carry their own session_id](https://github.com/OpenHands/software-agent-sdk/issues/4365)**（priority:medium）：子 agent 会话与父会话共享 trace_id 但携带独立 session_id，导致同一 trace 包含两个 session 的 span 且交错排列。无 fix PR。

- **[#4363 InstallationManager.update() silently drops pinned refs](https://github.com/OpenHands/software-agent-sdk/issues/4363)**（priority:medium）：强制 `ref=None` 导致固定版本引用被静默丢弃，应改为协调而非强制覆盖。

- **[#3759 is_git_url() does not recognize the ssh:// scheme](https://github.com/OpenHands/software-agent-sdk/issues/3759)**（STALE，1 条评论）：`ssh://git@bitbucket.example.com:7999/team/repo.git` 形式的 plugin source 解析失败，错误信息误导性强。创建于 6 月中旬，至今未修复。

**🟢 低优先级 / 待确认**

- **[#4267 agent-server (No response from ACP server)](https://github.com/OpenHands/software-agent-sdk/issues/4267)**：持续活跃但无明确 fix PR，已影响

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，这是 2026-08-05 的 Pi 项目动态日报。

---

# Pi 项目动态日报 | 2026-08-05

## 1. 今日速览

过去24小时，Pi 项目保持高活跃度与高处理效率：共更新 60 条 Issues（其中 49 条已关闭，关闭率约 82%）和 31 条 PR（其中 23 条已合并/关闭）。核心开发集中在 **v2 harness 的 SQLite 会话存储后端**、**RPC 协议增强**、**新增 AI 提供商**以及 **Copilot 企业版兼容性修复**。社区反馈的热点集中在 Copilot Enterprise 压缩（Compaction）失败、Windows 平台体验及终端 UI 的稳定性问题。项目整体健康度良好，维护者响应迅速。

## 2. 版本发布

- **无新版本发布。** （当前最新版本线索：Issue #7603 提及 `0.83.0`）

## 3. 项目进展

今日合并/关闭的 PR 展示了项目在架构演进和功能扩展上的持续推进：

- **架构演进（v2 Harness）**：
  - [#7396 `feat(coding-agent): add server session backend`](https://github.com/earendil-works/pi/pull/7396) **[MERGED]**：为 `PiServer` 添加了持久的会话后端，基于 JSONL 存储，支持跨进程锁与崩溃恢复，是 v2 harness 的关键基础设施。
  - [#7614 `feat: remove legacy server implementation`](https://github.com/earendil-works/pi/pull/7614) **[MERGED]**：移除了实验性的遗留子进程服务器实现。与 #7396 配合，标志服务器架构向新方案完成切换。
  - [#7591 `refactor: update sqlite for lanes`](https://github.com/earendil-works/pi/pull/7591) **[MERGED]**：为 v2 harness 更新 SQLite 会话存储，增加 lane 支持、分支缓存表等。
  - [#7626 `fix(agent): own SQLite backend tests in storage package`](https://github.com/earendil-works/pi/pull/7626) **[MERGED]**：将 SQLite 后端测试移至独立的 `packages/storage/sqlite-node` 包，优化测试结构。

- **RPC 与集成能力**：
  - [#7621 `feat(rpc): expose argument completions via get_argument_completions`](https://github.com/earendil-works/pi/pull/7621) **[MERGED]**：新增 RPC 命令 `get_argument_completions`，允许嵌入式客户端（如 Web UI）获取斜杠命令的参数补全。
  - [#7599 `rpc over sockets`](https://github.com/earendil-works/pi/pull/7599) **[MERGED]**：新增 `--listen` 选项，支持通过 Unix Socket 或 TCP 进行 RPC 通信。

- **提供商支持**：
  - [#7571 `feat(ai): add built-in Cortecs provider support`](https://github.com/earendil-works/pi/pull/7571) **[MERGED]**：新增欧洲 AI 提供商/路由器 **Cortecs** 的内置支持。
  - [#7610 `feat(ai): add LLM Gateway and LLM Gateway DevPass providers`](https://github.com/earendil-works/pi/pull/7610) **[OPEN]**：新增 OpenRouter 风格路由器 **LLM Gateway** 作为内置提供商。

- **修复与优化**：
  - [#7624 `feat(coding-agent): render Mermaid diagrams`](https://github.com/earendil-works/pi/pull/7624) **[OPEN]**：实现 Markdown 中 Mermaid 图表渲染。
  - [#7602 `feat(coding-agent): configurable summarization models`](https://github.com/earendil-works/pi/pull/7602) **[OPEN]**：支持为压缩和分支摘要配置独立的模型与思考级别（Closes #7553）。
  - [#7604 `fix(ai): keep $defs in non-strict Anthropic tool schemas`](https://github.com/earendil-works/pi/pull/7604) **[MERGED]**：修复 Anthropic 工具 schema 中 `$defs` 被丢弃导致引用悬空的问题。
  - [#7605 `fix(ai): keep response bodies out of OAuth error messages`](https://github.com/earendil-works/pi/pull/7605) **[MERGED]**：修复 OAuth 错误信息泄露敏感响应体的问题（安全修复）。
  - [#7606 `fix(ai): let an explicit chatgpt-account-id header override JWT extraction for Codex`](https://github.com/earendil-works/pi/pull/7606) **[MERGED]**：修复部分 ChatGPT 令牌缺少账号声明导致请求失败的问题。
  - [#7598 `fix(examples): accept array-form tools in the subagent example`](https://github.com/earendil-works/pi/pull/7598) **[MERGED]**：修复示例代码中 frontmatter 解析数组失败的问题。

## 4. 社区热点

今日讨论最热烈的话题集中在 Copilot 企业版用户遇到的严重问题，以及 Windows 平台体验的征集。

1.  **[#6768 `[bug] Compaction using Copilot Enterprise not possible`](https://github.com/earendil-works/pi/issues/6768) [CLOSED] | 评论: 19 | 👍: 18**
   - 这是今日社区最关注的议题。使用 GitHub Copilot Enterprise 许可证时，上下文压缩（Compaction）功能完全不可用，OpenAI 路径报 `421 Misdirected Request` 错误，Anthropic 模型同样失败。该问题有 19 条评论和 18 个赞，说明受影响的用户面很广。该 Issue 今日已关闭，同时出现了多个相关的新 Issue（见下文 Bug 部分），可能已找到根因并分流处理。

2.  **[#7547 `[Windows] [sink-thread] How do you use Pi on windows? What issues are you seeing?`](https://github.com/earendil-works/pi/issues/7547) [OPEN] | 评论: 11**
   - 项目方主动发起的 Windows 用户体验征集帖。帖子指出有大量 Windows 开发者使用 Pi，但因其使用方式多样，项目方难以确定优化重点。这是项目维护者主动收集反馈、规划路线图的信号，值得关注和参与。

3.  **[#7161 `anthropic-messages never sends x-client-request-id, unlike all OpenAI paths`](https://github.com/earendil-works/pi/issues/7161) [CLOSED] | 评论: 10**
   - 一个 API 兼容性问题，`anthropic-messages` 路径不发送 `x-client-request-id` 头，导致基于该头进行会话粘滞的网关（如 CliProxyAPI）无法为 Anthropic 会话分组。这反映了用户对多账户/网关等高级用法的需求。

4.  **[#5023 `[bug] terminal scrolls to beginning without reason`](https://github.com/earendil-works/pi/issues/5023) [CLOSED] | 评论: 11**
   - 一个长期存在的终端 UI 问题，终端会无缘无故跳转到会话开头。该问题创建于 5 月 26 日，今日关闭，可能已修复。

## 5. Bug 与稳定性

今日报告的 Bug 中，Copilot 企业版压缩失败是核心痛点，此外还存在数项影响稳定的问题。

**严重（核心功能不可用）**
- [#7594 `node:sqlite missing in release binary causing plugin breakage`](https://github.com/earendil-works/pi/issues/7594) [CLOSED]：发布版二进制缺少 `node:sqlite` 模块，导致依赖此模块的插件（如 `pi-total-recall`）无法加载。
- [#7579 `[bug] Compaction fails with 421 on Copilot enterprise seats`](https://github.com/earendil-works/pi/issues/7579) [CLOSED]：与 #6768 同源，正常对话正常，但压缩失败。分析指出压缩路径未像正常请求一样重写 baseUrl。
- [#7413 `Compaction fails on GitHub Copilot GHE.com enterprise accounts — "unknown stamp" error`](https://github.com/earendil-works/pi/issues/7413) [OPEN]：GHE.com 企业账户压缩失败，报 `unknown stamp` 错误。显示企业版压缩问题有多种表现。

**中等（稳定性与体验）**
- [#7528 `TUI crashes the whole process when a custom dialog line exceeds terminal width`](https://github.com/earendil-works/pi/issues/7528) [CLOSED]：自定义对话框中的行超过终端宽度时，会导致整个进程崩溃（未捕获异常）。
- [#7574 `Fullscreen mode: Home/End/PageUp/PageDown are consumed by the transcript viewport`](https://github.com/earendil-works/pi/issues/7574) [CLOSED]：全屏模式下，编辑器按键被视图抢占，导致光标移动快捷键失效。
- [#7508 `GitHub Copilot OAuth refresh has no request timeout`](https://github.com/earendil-works/pi/issues/7508) [CLOSED]：OAuth 令牌刷新没有超时机制，网络问题可能导致会话冻结约5分钟。
- [#7613 `Successful retries leave permanent red error lines`](https://github.com/earendil-works/pi/issues/7613) [CLOSED]：请求重试成功后，界面仍保留红色的 `Error: fetch failed` 提示，造成误导。
- [#7565 `tui: Terminal progress indicator is never cleared`](https://github.com/earendil-works/pi/issues/7565) [CLOSED]：终端进度指示器显示后无法清除（OSC 语法错误）。

**较低（功能异常）**
- [#7603 `unknown role: developer`](https://github.com/earendil-works/pi/issues/7603) [CLOSED]：使用 Deepseek 时，因消息角色 `developer` 不被支持而报 422 错误。
- [#7572 `Project retry.provider settings replace global provider retry settings`](https://github.com/earendil-works/pi/issues/7572) [CLOSED]：项目级配置中的 `retry.provider` 覆盖了全局配置，不符合文档所述的递归合并预期。
- [#7328 `validateToolArguments() coerces values that already match a nullable union`](https://github.com/earendil-works/pi/issues/7328) [CLOSED]：工具参数校验将合法的 `null` 强转为其他类型（如 `0`），导致依赖 `null` 表示“未设置”的工具出错。

## 6. 功能请求与路线图信号

今日的功能请求显示出社区对**可定制性**和**平台完备性**的强需求。

- **Mermaid 图表渲染**：Issue [#7623](https://github.com/earendil-works/pi/issues/7623) 请求渲染 Mermaid 图表，已被 PR [#7624](https://github.com/earendil-works/pi/pull/7624) 实现，属于用户呼声高、落地快的功能。
- **可配置的压缩模型**：Issue [#7553](https://github.com/earendil-works/pi/issues/7553) 请求为压缩功能单独配置思考级别/模型，已由 PR [#7602](https://github.com/earendil-works/pi/pull/7602) 解决。
- **iTerm2 图片尺寸参数**：Issue [#7465](https://github.com/earendil-works/pi/issues/7465) 请求在 iTerm2 内联图片中添加 `size` 参数以兼容 xterm.js，已有 PR [#7612](https://github.com/earendil-works/pi/pull/7612) 提出修复。
- **RPC 模式暴露认证**：Issue [#7590](https://github.com/earendil-works/pi/issues/7590) 请求在 RPC 协议中暴露提供商的身份验证（登录/登出等），这符合项目增强嵌入式客户端能力的路线。
- **Qwen Token Plan Individual 提供商**：Issue [#7631](https://github.com/earendil-works/pi/issues/7631) 请求为 Qwen 的 Individual 订阅套餐添加明确的提供商支持。
- **优化 `version` 命令**：Issue [#7244](https://github.com/earendil-works/pi/issues/7244) 请求在 `version` 命令中显示运行时信息（bun/node/deno），以便更好地诊断问题。
- **Add Context Windows option**：Issue [#5064](https://github.com/earendil-works/pi/issues/5064) 请求添加上下文窗口大小选项。该问题已创建超两个月，今日关闭但未合并到 PR，可能已进入内部路线图。

## 7. 用户反馈摘要

- **Copilot 企业版用户受阻**：多个 Issue（#6768, #7579, #7413）表明 Copilot Enterprise/GHE.com 用户无法使用核心的压缩功能，这直接影响了他们的日常工作流。用户 "MojangPlsFix" 在 #6768 中详细描述了错误信息，体现了尝试解决问题的耐心。
- **Windows 用户处于“可用但不够好”状态**：Issue #7547 的讨论表明，Windows 上虽有用户成功运行 Pi，但存在多种可能导致困惑的运行方式。Windows 用户也遇到了一些特定问题，如 [#7427](https://github.com/earendil-works/pi/issues/7427)（加载技能崩溃）和 [#6817](https://github.com/earendil-works/pi/issues/6817)（`find` 工具路径模式无效）。
- **网络不稳定环境下的体验问题**：Issue #7508 指出在弱网环境下，令牌刷新问题会导致会话长时间无响应，这对于移动办公或网络受限的用户是严重的体验障碍

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-05

## 1. 今日速览

过去24小时内，LiteLLM 项目保持高强度迭代：共产生 **83 条 Issue 更新**（新开/活跃 52 条，关闭 31 条）和 **242 条 PR 更新**（待合并 161 条，合并/关闭 81 条），无新版本发布。PR 活跃度远高于 Issue 处理量，说明核心团队正集中推进功能开发和缺陷修复。值得关注的是，多个跨版本遗留 Bug（如 #24677 TPM 限流、#22998 数据库迁移问题）在今日重新活跃，反映出用户对稳定性的诉求持续累积；同时社区对 UI/UX 改进（#24037）和云端成本计算准确性（#35841、#35481）表现出较高关注度。整体来看，项目处在功能快速迭代期，但稳定性议题占比偏高，建议维护者平衡新功能开发与存量缺陷修复的节奏。

---

## 2. 版本发布

今日无新版本发布（最新 Releases 为空）。上一个稳定版停留在 v1.95.0 附近（基于 Issue #35763 的引用），用户正在等待包含近期大量 PR 修复的下一个版本。

---

## 3. 项目进展

今日共合并/关闭 81 条 PR，以下为关键推进项：

### 已合并的重要 PR

| PR | 内容 | 影响 |
|---|---|---|
| [#35834](https://github.com/BerriAI/litellm/pull/35834) | **fix(proxy): enforce per-model budgets against resolved cursor model variants** | 修复 Cursor 变体别名绕过按模型预算的问题，预算检查现在基于实际计费的 base model，对使用 Cursor 集成的企业用户是重要修正 |
| [#35746](https://github.com/BerriAI/litellm/pull/35746) | **feat(ui): reorder Add Auto Router into name + template, with a collapsible detailed config** | 重构 Auto Router 创建流程，让用户可以先通过模板快速创建，再展开详细配置，降低使用门槛 |
| [#35840](https://github.com/BerriAI/litellm/pull/35840) | **fix(proxy): apply key_alias/key_hash filters to all /key/list visibility branches** | 修复 team admin 视角下 key_alias 过滤器失效的问题，现在所有可见性分支统一应用过滤条件 |
| [#35806](https://github.com/BerriAI/litellm/pull/35806) | **fix(azure_storage): honor AZURE_STORAGE_ENDPOINT_SUFFIX for sovereign clouds** | 新增 `AZURE_STORAGE_ENDPOINT_SUFFIX` 环境变量，支持 Azure Government 等主权云存储，对政企客户是刚需 |
| [#34627](https://github.com/BerriAI/litellm/pull/34627) | **fix(router): eagerly fetch Vertex AI deferred stream to surface HTTP errors in _acompletion fallback path** | 修复 Vertex AI/Bedrock 延迟流式响应的 HTTP 错误无法触发 fallback 的问题，减少流式中断导致的内容丢失 |
| [#34528](https://github.com/BerriAI/litellm/pull/34528) | **fix(otel): keep MCP tool calls in one trace when the client sends no trace context** | 修复 MCP 工具调用在无 traceparent 时被拆分为两个 trace 的问题，确保可观测性数据完整性 |

### 待合并的关键 PR（当前开放中）

- [#35839](https://github.com/BerriAI/litellm/pull/35839) — **feat(spend): add a per-session auto-router benchmarks rollup**：为 auto-router 基准测试提供专门的汇总数据后端，避免扫描全量 SpendLogs（最宽表），是重要的性能优化方向
- [#35843](https://github.com/BerriAI/litellm/pull/35843) — **fix(router): redact fallback tracebacks at the call site and cover the sync deferred stream**：修复 fallback 失败日志泄露 provider key 的安全问题，同时补上同步 deferred stream 的 fallback 路径
- [#35717](https://github.com/BerriAI/litellm/pull/35717) — **feat(sgr): make the gateway middleware the source of truth for successful requests**：统一 SGR 成功请求的统计口径，从 SpendLogs 改为 gateway middleware 计数

**总评**：项目在预算控制、key 权限过滤、云存储兼容性、OTEL 可观测性等多个维度都有实际改进，企业级功能完善度在持续上升。

---

## 4. 社区热点

### 最热 Issue：#24677 [Bug]: Incorrect TPM limiting for virtual keys

- 链接：https://github.com/BerriAI/litellm/issues/24677
- 活跃度：16 条评论，4 👍 | 状态：OPEN
- 作者 @yuri-alias 明确指出该问题曾在 #18953 被标记为已解决，但在 v1.82.3 仍然存在。实际速率限制与预期不符，用户已经跨多个版本验证，说明修复并未真正生效。

### 最高赞 Issue：#24037 /ui/chat returns 404 — Next.js static export missing index.html

- 链接：https://github.com/BerriAI/litellm/issues/24037
- 活跃度：6 条评论，**26 👍**（今日 Issue 中最高） | 状态：OPEN
- UI 子路由（`/ui/chat`、`/ui/logs` 等）直接访问返回 404，需要从 `/ui/` 入口导航。虽然不算核心功能，但 26 个 👍 表明大量用户遇到此问题。

### 高频反馈：#30765 /v1/messages streaming drops first text_delta after thinking block

- 链接：https://github.com/BerriAI/litellm/issues/30765
- 活跃度：7 条评论，1 👍 | 状态：OPEN
- Claude Code 用户在使用 LiteLLM 的 Anthropic 兼容端点时，thinking 块结束后首个 text_delta 被吞掉。与 #25214（Bedrock 推理模型同样丢块）疑似同源问题。

**诉求分析**：社区当前最关心的是 (a) 速率限制的准确性（涉及成本控制），(b) Anthropic 兼容端点的流式完整性（直接关系到 Claude Code 用户体验），以及 (c) UI 路由基础体验。三者都直接影响生产环境可用性。

---

## 5. Bug 与稳定性

按严重程度排列：

### 🔴 严重 — 阻塞部署/启动

| Issue | 描述 | 状态 |
|---|---|---|
| [#35763](https://github.com/BerriAI/litellm/issues/35763) | **ImportError: cannot import name 'get_flat_dependant' from 'fastapi.dependencies.utils'** — 当 FastAPI ≥0.141.0 时 LiteLLM proxy 完全无法启动（包括 `--version`） | 今日新建，暂无 fix PR。影响所有升级 FastAPI 的用户，需紧急处理 |
| [#34236](https://github.com/BerriAI/litellm/issues/34236) | **litellm-non_root 镜像无法运行 Prisma 迁移** — @prisma/engines 目录不可写，升级 1.84.0→1.92.1 时迁移失败 | 5 条评论，5 👍，OPEN，无 fix PR |

### 🟠 高 — 功能异常/数据不一致

| Issue | 描述 | 状态 |
|---|---|---|
| [#22998](https://github.com/BerriAI/litellm/issues/22998) | **litellm_proxy_extras 迁移记录但列未创建** — 升级至 v1.81.14 后 `/v2/login` 返回 500，MCP 接口静默返回空数组 | 已关闭，但 4 👍 说明影响面广，建议确认修复方案已发布 |
| [#24677](https://github.com/BerriAI/litellm/issues/24677) | **虚拟 key 的 TPM 限流不生效** — 用户确认跨多个版本（v1.80.0→v1.82.3）仍然存在 | OPEN，无 fix PR |
| [#30765](https://github.com/BerriAI/litellm/issues/30765) | **/v1/messages 流式响应丢失 thinking→text 过渡后的首个 text_delta** | OPEN，无 fix PR |
| [#25214](https://github.com/BerriAI/litellm/issues/25214) | **Bedrock 推理模型同样存在流式丢块问题** | OPEN，7 👍，无 fix PR |

### 🟡 中 — 配置/兼容性问题

| Issue | 描述 | 状态 |
|---|---|---|
| [#24037](https://github.com/BerriAI/litellm/issues/24037) | UI 子路由直接访问返回 404 | OPEN，26 👍，无 fix PR |
| [#27183](https://github.com/BerriAI/litellm/issues/27183) | Ollama Vision VLM 调用因缺少 pillow 失败 | OPEN，5 👍，无 fix PR |
| [#18060](https://github.com/BerriAI/litellm/issues/18060) | 未授权/错误请求导致死循环重试 | OPEN（2025-12 创建），无 fix PR |
| [#35775](https://github.com/BerriAI/litellm/issues/35775) | 与 VSCode 原生 Model-Provider 不兼容 | 今日新建，OPEN |

**稳定性趋势判断**：今日无新版本发布，但新增了 1 个阻塞性 Bug（#35763 FastAPI 兼容性），同时多个 long-standing 流式丢块问题仍未解决。建议下个版本优先覆盖这些已知问题的修复。

---

## 6. 功能请求与路线图信号

### 用户明确提出的新需求

| Issue | 需求 | 热度 | 分析 |
|---|---|---|---|
| [#35745](https://github.com/BerriAI/litellm/issues/35745) | Invite User 弹窗增加 Microsoft Graph 目录搜索（通过 Entra ID 搜索用户） | 今日新建 | 企业管理员场景的合理补充，与已有的 SSO/团队管理功能形成闭环 |
| [#23388](https://github.com/BerriAI/litellm/issues/23388) | 为 gemini-2.5-flash 和 flash-lite 增加 priority/flex paygo 定价支持 | 2 条评论，1 👍 | Vertex AI 已支持，属于补齐模型覆盖范围 |
| [#23700](https://github.com/BerriAI/litellm/issues/23700) | MCP OAuth 端点不支持 refresh_token grant type | 2 条评论，2 👍 | 元数据已声明支持 refresh_token，但实际端点未实现，是功能缺口 |

### 结合 PR 的路线图信号

- **#30873 [OPEN] feat(otel/v2)!: admin-owned, identity-scoped trace destinations** — 允许不同团队将 trace 路由到不同后端，解决多租户可观测性隔离问题。这是一个 breaking change PR，自 6/20 创建至今仍未合并，可能在下个大版本中落地。
- **#35839 [OPEN] feat(spend): per-session auto-router benchmarks rollup** — 为 auto-router 的 benchmark 引入专用汇总表，避免扫描全量 SpendLogs。说明团队在性能优化方向持续投入。
- **#35746（已合并）Add Auto Router UI 重构** — 降低 Auto Router 配置门槛，这是推动复杂路由功能采用率的重要一步。

**预判**：下一版本可能重点包含 (a) OTEL v2 多租户 trace 隔离，(b) spend 数据查询性能优化，(c) 更多模型的成本计算修正（Azure 定价调整 #35841、#35481 待合并）。

---

## 7. 用户反馈摘要

### 正面反馈

- **Auto Router 功能值得期待**：PR #35746 的 UI 改进说明团队在响应 #35199（模板下拉）等社区反馈，降低配置复杂度
- **安全敏感度高**：PR #35843 主动修复 fallback 日志泄露 provider key 的问题，说明维护者对安全问题响应积极
- **主流云支持持续扩展**：PR #35806 对 Azure 主权云的支持展示了企业级合规能力

### 负面反馈（按频次）

- **"说修好了但没修好"**：Issue #24677 明确指出 #18953 标记 solved 后问题仍然存在，用户 @yuri-alias 跨版本验证发现 v1.82.3 依旧是旧行为。信任受损是这类反馈的最大风险。
- **流式响应丢失影响 Claude Code 体验**：#30765 和 #25214 两个 issue 都指向同一类问题——thinking 块后丢首个 text，直接导致 Claude Code 回答不完整。7 👍 和 4 👍 的活跃度说明这不是个例。
- **UI 体验粗糙**：26 个 👍 的 #24037（UI 子路由 404）说明即便是轻度使用的用户也会撞上这个问题。
- **数据库迁移是升级最大痛点**：#22998（迁移记录与实际列不一致）和 #34236（Prisma 目录不可写）双双活跃，用户对升级的恐惧感可能因此增加。

### 用户使用场景提炼

- **Claude Code + LiteLLM 代理**是当前最热的用法，但 Anthropic 兼容端点的流式处理和 MCP 工具调用体验是一大短板
- **企业多团队场景**（team admin、key alias、per-model budget）的权限过滤和预算管理逻辑需要更精细
- **容器化部署用户**对镜像的可写性和权限配置有更高要求

---

## 8. 待处理积压

### 长期未响应的关键 Issue

| Issue | 创建时间 | 最后更新 | 延迟 | 重要性 |
|---|---|---|---|---|
| [#18060](https://github.com/BerriAI/litellm/issues/18060) Infinite loops on unauthorized requests | 2025-12-16 | 2026-08-04 | **233 天** | 🔴 可能导致资源耗尽和费用失控 |
| [#23700](https://github.com/BerriAI/litellm/issues/23700) MCP OAuth 缺少 refresh_token | 2026-03-15 | 2026-08-04 | 142 天 | 🟠 功能缺失，2 👍 |
| [#23388](https://github.com/BerriAI/litellm/issues/23388) Gemini flex/paygo 定价支持 | 2026-03-11 | 2026-08-04 | 146 天 | 🟡 增强需求，1 👍 |
| [#32357](https://github.com/BerriAI/litellm/issues/32357) /v

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-05

---

## 1. 今日速览

过去 24 小时 Temporal 主仓库保持 **高度活跃**：共 38 条 PR 更新，其中 15 条已合并或关闭，23 条待合并；Issue 层面新开 1 条、关闭 1 条。无新版本发布。核心精力集中在 **CHASM 调度器可靠性修复**（多个 PR 围绕初始暂停状态、catch-up 截止时间、迁移标识展开）、**复制（replication）架构演进**（read-through buffer、当前执行记录重建、孤儿子工作流恢复）以及 **Activity 可靠性对齐**（LastDeploymentVersion 传递、重试失败截断）。最值得关注的是新提交的 Issue #10737：Worker Deployment 版本 GC 在达到 `maxVersionsInDeployment` 上限时无法回收已排空版本，可能导致持续部署的 rollouts 被卡死，需要尽快跟进。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

过去 24 小时关闭的 PR 中，以下 6 条值得注意（按主题归类）：

### 3.1 CHASM 调度器持续加固

- **#11368 [CLOSED]** — 修复 CHASM 初始调度暂停状态。原来通过 `InitialPatch.Pause` 创建的调度器会以未暂停状态启动，可能立即生成并执行动作；现在改为在生成器和 backfiller 武装之前就应用初始暂停/取消暂停状态，并补充了 CHASM 测试引擎覆盖。  
  https://github.com/temporalio/temporal/pull/11368

- **#11278 [CLOSED]** — 在创建 CHASM 调度器时正确应用 `InitialPatch` 的暂停/取消暂停指令。此前 `NewScheduler` 只将初始 patch 路由到 `handlePatch`，而该函数只处理立即触发和 backfill，忽略了 pause/unpause 字段。  
  https://github.com/temporalio/temporal/pull/11278

- **#11282 [CLOSED]** — 在调度器创建/更新入口拒绝畸形 的 interval 和 phase duration protobuf，返回 4XX 错误，并带有 killswitch 以防意外行为变化。  
  https://github.com/temporalio/temporal/pull/11282

### 3.2 复制（Replication）可靠性与可观测性

- **#9434 [CLOSED]** — 对重复重定向请求发出指标。这是 3 月 3 日创建的长期 PR，今日关闭，其目的与同日新增的 #11418（添加重复请求转发指标）一致，疑似由 #11418 取代收尾。  
  https://github.com/temporalio/temporal/pull/9434

### 3.3 系统可观测性与测试修复

- **#8319 [CLOSED]** — 记录系统 worker 致命错误日志，改善调试体验。该 PR 自 2025-09-12 起积压近一年，今日终于关闭（被标为 stale）。  
  https://github.com/temporalio/temporal/pull/8319

- **#11416 [CLOSED]** — 移除过时的 SAA 延迟恢复取消功能测试，补上聚焦的单元测试，验证 `TransitionCancelRequested` 会清除 `ResetRestoreOptions`。  
  https://github.com/temporalio/temporal/pull/11416

**总结**：项目在调度器正确性（CHASM 初始化路径）和复制可观测性上有了明确进展，但真正的架构型 PR（如 #11263 复制流读取缓冲、#11388 孤儿子工作流恢复、#11257 当前执行记录重建）仍处于开放待合并状态，尚未落地主线。

---

## 4. 社区热点

当前讨论热度最高的条目是 **Issue #10737**（4 条评论，已持续开放超过 6 周）：

> **Worker Deployment 版本 GC 不回收已排空版本，导致 rollouts 被卡住**  
> 用户 @noamyehudai 使用 Worker Versioning + 频繁部署的控制器，每部署一次注册新版本。期望旧版本排空后被自动回收以不超过 `matching.maxVersionsInDeployment` 上限，但实际 GC 未生效。  
> https://github.com/temporalio/temporal/issues/10737

**诉求分析**：这是 Worker Versioning 真实生产环境中的瓶颈问题。用户以 controller 方式高频发布，触及版本数量上限后 rollout 被阻断。该 issue 已存在超 6 周且带 `[OPEN]` 状态，社区有持续讨论但尚无 fix PR 关联，需要维护者介入。此外，PR #11386（在 `ActivityExecutionInfo` 中补充 `LastDeploymentVersion`）正是为了修复 Worker Versioning 中 `DescribeActivity` 不返回部署版本的问题，说明该主题仍是社区关注重点。

---

## 5. Bug 与稳定性

按严重程度排序：

### 🔴 严重 — Worker Versioning 版本回收失效（功能阻塞）

- **#10737 [OPEN]**：Worker Deployment 的 GC 在达到 `maxVersionsInDeployment` 时无法回收已排空的旧版本，导致后续部署被阻断。影响持续部署/频繁发布的工作流。目前 **无关联 fix PR**，且 issue 已开放 6+ 周。  
  https://github.com/temporalio/temporal/issues/10737

### 🟠 中等 — 数据竞争（已有关闭记录）

- **#11352 [CLOSED]**：`ReaderImpl.AppendSlices` 中 `r.slices.Back()` 在无锁保护下被读取，与 `MergeSlices` 等其他方法并发调用时产生 data race。该 issue 今日关闭，但数据未显示修复 PR 编号，建议确认是否已合入。  
  https://github.com/temporalio/temporal/issues/11352

### 🟡 关注中 — Activity 可靠性对齐修复（已有 PR，未合并）

- **PR #11386 [OPEN]** — `buildActivityExecutionInfo` 未返回 `LastDeploymentVersion`，导致 `DescribeActivity` 丢失部署版本信息。已有修复 PR。  
  https://github.com/temporalio/temporal/pull/11386

- **PR #11385 [OPEN]** — 独立 Activity（CHASM）重试时保留的 `LastFailureDetails` 未截断，与工作流 Activity 行为不一致，可能造成状态存储膨胀。已有修复 PR。  
  https://github.com/temporalio/temporal/pull/11385

### 🟢 已修复/已关闭

- **#11416 [CLOSED]** — 修正 SAA 延迟恢复取消的测试覆盖（本身为测试修复，不涉及产品逻辑）。

---

## 6. 功能请求与路线图信号

从今日活跃 PR 中可以观察到以下功能方向，部分将重塑复制与调度架构：

| 方向 | PR | 状态 | 信号解读 |
|------|-----|------|---------|
| **复制流命名空间隔离** | #11263 — 为复制流队列扫描添加 read-through buffer，「5-PR 系列」第一步 | OPEN | 大型架构调整正在进行，后续包括 reader group、lane protocol、isolation manager、sender isolation。 |
| **孤儿子工作流恢复** | #11388 — force failover 后允许父工作流将丢失的子工作流标记为 zombie 并原子替换 | OPEN | 提升跨集群故障场景下的数据自愈能力。 |
| **缺失当前执行记录重建** | #11257 — 复制应用时若发现 `currentRunID == ""`，区分“用户删除”和“记录缺失”，后者尝试重建 | OPEN | 消除复制任务执行中的不确定性。 |
| **工作线程回调持久化** | #11413 / #11415 — 持久化 CHASM Callback 的 terminal failure，并为其添加 completion callbacks | OPEN（stacked PR） | 工作线程回调功能的容错与可观测性补强。 |
| **连接缓存恢复** | #11268 — 恢复共享 internode 连接缓存，增加关闭保护与定期清理 | OPEN | 权衡连接重用与优雅关闭的正确性。 |
| **SAA/WFA 行为对齐** | #11417 — SAA 默认不再重置 heartbeat，并尊重 `reset_heartbeat` 标志 | OPEN | 消除 Activity 重试语义中 SAA 与 WFA 的不一致。 |

**路线图判断**：`reliability-2026` 和 `team/cgs-foundation` 两个标签下的 PR 占据今日活跃清单的半数以上，说明 Temporal 正在系统性推进 **复制架构重构** 与 **核心可靠性修复**。CHASM 调度器的问题也在一波波修补（初始暂停、catch-up 截止、迁移标识、非法 protobuf 拒绝），表明其正在走向生产就绪。Worker callbacks 持久化是较新的功能方向，处于较早期阶段。

---

## 7. 用户反馈摘要

数据中可提取的用户反馈主要来自 Issue #10737 的讨论串（共 4 条评论，内容未提供，但可从问题描述推断）：

- **Worker Versioning 的 GC 行为与用户预期不符**：用户以代码控制器方式高频部署 Worker Deployment 版本，期望旧版本排空后自动回收，避免触碰 `maxVersionsInDeployment`。实际 GC 未回收已排空的版本，导致 rollout 进程被卡死。这反映了 **Worker Versioning 在生产环境高频发布场景下尚不够成熟**，GC 策略需要更积极地回收 drained 版本，或提供手动强制清理的途径。

- **部署频率是核心使用场景**：用户明确表示“每次部署注册新版本”，说明 Worker Deployments 被当作 CI/CD 流程的一等公民使用，而不是低频手动操作。这为设计版本配额和回收策略提供了重要输入。

其余 issue/PR 评论均未展示详细内容，暂无更广泛的用户声音可供提取。

---

## 8. 待处理积压

以下为需维护者关注、但长期处于未合并/未响应状态的条目：

| 条目 | 类型 | 创建时间 | 持续时间 | 说明 |
|------|------|---------|---------|------|
| **#10737** Worker Deployment GC 不回收 drained 版本 | Issue | 2026-06-16 | **50 天** | 严重功能缺陷，无关联 PR，持续影响用户 rollout。 |
| **#11166** 迁移时同期 pending starts 赋予唯一标识 | PR | 2026-07-21 | 15 天 | CHASM 调度迁移正确性修复，仍在 review，未见冲突或阻塞说明。 |
| **#11281** 重试自动启动前重新检查 catch-up 截止时间 | PR | 2026-07-25 | 11 天 | 与 #11166 同属 CHASM 迁移可靠性系列，均未合并。 |
| **#11257** 复制应用时重建缺失的当前执行记录 | PR | 2026-07-24 | 12 天 | `team/cgs-foundation` 核心修复，review 周期偏长。 |
| **#9434** 重复重定向请求指标 | PR | 2026-03-03 | **5 个月** | 今日刚关闭，但历史积压反映了指标类 PR 长时间未被响应；新 PR #11418 已接力提出同类指标。 |

> ⚠️ 特别提醒：**#10737** 已持续 50 天未分配修复，且直接阻塞高频部署用户的正常迭代，建议维护者优先标记并安排处理。

---

*本报告基于 Temporal GitHub 数据自动生成，覆盖 2026-08-04 至 2026-08-05 时间段。*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*