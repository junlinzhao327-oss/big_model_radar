# OpenClaw 生态日报 2026-08-29

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-29 03:44 UTC

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

# Hermes Agent 项目日报 — 2026-08-29

## 1. 今日速览

过去 24 小时项目活动量维持高位：共 384 条 Issue 更新（新开/活跃 327 条，关闭 57 条）和 500 条 PR 更新（待合并 450 条，已合并/关闭 50 条），社区提交和讨论均处于活跃状态。无新版本发布。今日热点集中在**桌面端稳定性**（启动超时、后端 READY 信号丢失、Wayland 白屏、进程被过早杀死）、**会话状态持久化与恢复**（远程网关会话无法恢复、多 profile 存储隔离失效、压缩后重复召回）以及**自动化基础设施**（技能索引过期、cron 合并冲突、curator 终端归档绕过）三大方向，其中多个 P0/P1 级问题已有对应修复 PR 在途。整体项目健康度：提交节奏快、问题响应及时，但桌面端与会话状态的系统性缺陷仍积压较多。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日无明确标记 "已合并" 的 PR 细目（50 条已合并/关闭 PR 未在 Top 20 列表中逐一标注），但从已关闭 Issue 可反推以下关键工作已完成：

- **Debian 安装问题修复**（[#87093](https://github.com/NousResearch/hermes-agent/issues/87093)，P0，已关闭）：`uv.lock` 与 `npm install` 失败导致的安装链路断裂已解决，安装脚本的锁文件同步逻辑得到修正。
- **桌面端持久多网关连接战役收官**（[#94724](https://github.com/NousResearch/hermes-agent/issues/94724)，已关闭）：官方标注 "CAMPAIGN COMPLETE"，共合并 29 个 PR，2 个同日回归已修复，15 个被保留的修复集群全部发布。
- **桌面端启动超时问题**（[#96282](https://github.com/NousResearch/hermes-agent/issues/96282)，P1，已关闭）：`HERMES_BACKEND_READY` sentinel 被误写到 stderr 导致 Electron 启动失败的问题已修复。
- **xAI grok-4.5 会话被 400 永久卡死**（[#69078](https://github.com/NousResearch/hermes-agent/issues/69078)，P2，已关闭）：图像恢复匹配器漏掉的边界情况得到处理，会话不再因历史中的非法 PNG 被永久中断。

此外，以下 PR 处于开放待合并状态，值得关注：

- **上下文硬上限**（[#92905](https://github.com/NousResearch/hermes-agent/pull/92905)，P2）：为 profile 增加 `model.max_context_length` 硬性上限，统一截断所有入口的上下文窗口。
- **工具输出按引用复用**（[#78090](https://github.com/NousResearch/hermes-agent/pull/78090)，P3）：结构化工具结果按调用 ID 保留，后续工具可通过 `{{tool_result:<call_id>.<field>}}` 引用，减少重复调用。
- **终端归档绕过修复**（[#97609](https://github.com/NousResearch/hermes-agent/pull/97609)，P1）：阻止 curator 直接移动文件到 `.archive/`，强制走受控的 `skill_manage(delete)` 路径，避免 cron 引用迁移被跳过。
- **update 命令重构**（[#97634](https://github.com/NousResearch/hermes-agent/pull/97634)，P3）：10,211 行 `update_cmd.py` 按职责拆分为模块，保留兼容门面，是提升可维护性的机械重构。

## 4. 社区热点

- **[#66616 Skills index is stale or degraded](https://github.com/NousResearch/hermes-agent/issues/66616)**（114 条评论，最热）：自动化探针报告技能索引比 26 小时限制慢了 29.8 小时，状态 `degraded`，自 7 月 18 日创建至今已活跃超一个月，持续吸引大量维护者讨论，反映了社区对文档与技能发现机制可靠性的高度关注。

- **[#88584 Automated Nous integration is blocked](https://github.com/NousResearch/hermes-agent/issues/88584)**（38 条评论）：定时 Nous-to-Enterkey 合并流程因 `cron/jobs.py` 冲突被阻断，属于跨仓库自动化管道的稳定性问题。

- **[#84834 Webhook Feature Package — graph-gated repair (meta-issue)](https://github.com/NousResearch/hermes-agent/issues/84834)**（24 条评论）：覆盖整个 webhook 表面（ingress、execution、delivery、配置、管理 UI、部署、文档）的 5×2×3 修复 Feature Package 追踪器，说明 webhook 相关缺陷已形成一个系统性的待修整面。

- **[#87093 Debian installation broken](https://github.com/NousResearch/hermes-agent/issues/87093)**（23 条评论，4 👍）：安装脚本在 Debian 13.6 上因 `uv.lock` 与 `npm install` 失败而中断，是今日最影响新用户入门的问题，现已关闭。

## 5. Bug 与稳定性

按严重程度排列（P0 → P3）：

| 严重度 | Issue | 描述 | 有无 fix PR |
|---|---|---|---|
| P0 | [#87093](https://github.com/NousResearch/hermes-agent/issues/87093) | Debian 13.6 安装失败：`uv.lock` 需更新 + `npm install` 失败 | 已关闭（修复完成） |
| P1 | [#96266](https://github.com/NousResearch/hermes-agent/issues/96266) | Linux 桌面端强制本地 backend 在 `HERMES_BACKEND_READY` 约 10 秒后被杀死，"Hermes couldn't start"，重试/修复均失败 | 无 |
| P1 | [#97609](https://github.com/NousResearch/hermes-agent/pull/97609) | curator 可通过直接文件移动绕过受控的归档路径，造成 cron 技能引用迁移失效 | 有 PR（开放中） |
| P1 | [#96282](https://github.com/NousResearch/hermes-agent/issues/96282) | Electron 桌面启动超时：`HERMES_BACKEND_READY` 被打印到 stderr 而非 stdout | 已关闭（修复完成） |
| P1 | [#93888](https://github.com/NousResearch/hermes-agent/issues/93888) | 桌面端向远程网关发送本地运行时 ID，导致已存会话永久 "Restore failed — Session not found" | 无 |
| P1 | [#94248](https://github.com/NousResearch/hermes-agent/issues/94248) | macOS arm64 网关上 delegate 超时后 17–72 ms 内 SIGSEGV（12 份崩溃报告），与 Codex SSL 读相关 | 无 |
| P1 | [#90837](https://github.com/NousResearch/hermes-agent/issues/90837) | state.db 在网关只写模式下反复损坏：8/2–8/20 共 11 次，已用小时级哨兵冻结现场但其间外部因素全部排除 | 无 |
| P1 | [#94058](https://github.com/NousResearch/hermes-agent/issues/94058) | Linux 桌面 .desktop 入口的 Exec 行解析 venv symlink 到裸解释器，升级后从启动器启动即崩溃 | 无 |
| P1 | [#86366](https://github.com/NousResearch/hermes-agent/issues/86366) | `archive_and_compact` 将保留尾部也标记 `compacted=1`，导致每次压缩后尾部重复并被召回两次 | 无 |
| P2 | [#88275](https://github.com/NousResearch/hermes-agent/issues/88275) | 桌面渲染进程空闲时占 CPU 40–73%，Intel Mac 上热降频，禁用 GPU 仅部分缓解 | 无 |
| P2 | [#38193](https://github.com/NousResearch/hermes-agent/issues/38193) | OAuth 背书的 MCP 服务器在 keepalive 重连后永久死锁（auth-flow 生成器的锁跨任务释放） | 已关闭 |
| P3 | [#69672](https://github.com/NousResearch/hermes-agent/issues/69672) | `messages_fts_trigram` 索引了 NUL JSON 哨兵，使 state.db FTS 完整性依赖 SQLite 版本，并造成 DB 膨胀 | 无 |
| P3 | [#71998](https://github.com/NousResearch/hermes-agent/issues/71998) | `pre_llm_call` 插件在多模态图像轮次丢 context 返回值 | 无 |

## 6. 功能请求与路线图信号

今日出现的功能需求与在途 PR 表明以下方向可能进入下一版本：

- **统一 slash 命令注册表**（[#96692](https://github.com/NousResearch/hermes-agent/issues/96692)）：一个版本化的命令目录 + 解析器 + 调用/结果契约，覆盖 CLI、TUI、gateway、桌面端与插件。如果被采纳，将是跨端一致性的基础设施级改动。

- **上下文硬上限**（[#92905 PR](https://github.com/NousResearch/hermes-agent/pull/92905)）：为 profile 配置强制 `model.max_context_length`，与现有的压缩系统互补，社区已有明确 PR。

- **工具输出按引用复用**（[#78090 PR](https://github.com/NousResearch/hermes-agent/pull/78090)）：允许后续工具直接引用前序工具输出，减少重复调用、降低 token 消耗。

- **跨平台会话上下文共享**（[#4335](https://github.com/NousResearch/hermes-agent/issues/4335)，3 👍，16 条评论）：CLI ↔ Telegram 等平台间共享会话上下文，避免"渠道孤岛"。`needs-decision` 标签仍在，说明尚未进入实施阶段。

- **RealtimeVoiceProvider ABC**（[#77111](https://github.com/NousResearch/hermes-agent/issues/77111)）：四个竞争的双工语音 PR 需要先定接口。参照 Footprint Ladder 规则，3+ 同类 PR 时先设计 ABC + orchestrator，以现有内建实现为首个 provider。这强烈暗示语音能力将在后续版本集中整合。

- **Mistral 作为 LLM 提供商**（[#20859](https://github.com/NousResearch/hermes-agent/issues/20859)，27 👍）：虽被标记 `wontfix`，但获得了今日数据中最高的社区点赞数，呼声明显，值得维护团队重新审视。

## 7. 用户反馈摘要

从今日活跃 Issue 的评论中可提炼以下真实用户痛点：

- **安装即失败是最大的新用户流失点**：Debian 13.6 用户反馈"只有 Yum 额外装了，curl | bash 就跑不动"，锁文件与 npm 步骤双双失败，对新手极不友好（[#87093](https://github.com/NousResearch/hermes-agent/issues/87093)）。
- **macOS 桌面的启动等待机制不可靠**：同一份日志里 backend 已宣告端口，但桌面端还是等到 90 秒超时（[#60323](https://github.com/NousResearch/hermes-agent/issues/60323)）；升级一个 commit 后启动直接 fail（[#96282](https://github.com/NousResearch/hermes-agent/issues/96282)）。Intel Mac 用户还面临渲染进程 40–70% 的 CPU 占用与热降频（[#88275](https://github.com/NousResearch/hermes-agent/issues/88275)）。
- **远程网关会话恢复反复踩坑**：

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-08-29

## 1. 今日速览

过去24小时内，OpenHands SDK 项目保持高活跃度：**26 条 Issue 更新**（新增/活跃 16 条，关闭 10 条）、**33 条 PR 更新**（待合并 30 条，已合并/关闭 3 条），并发布 **v1.44.1** 补丁版本。社区焦点集中在**流式传输架构重构**（#4671 系列）上：多个相关 Bug 被报告并快速关闭，显示维护者正在密集推进这一领域的整改。与此同时，**安全与稳定性议题**占据重要位置，包括 webhook 信息泄露（#4672）和 telemetry 计数失真（#4673）等高风险问题均已在本周内闭环。整体来看，项目正处于**活跃迭代期**，架构层面的重构（流式、事件日志、OpenAI 网关）与用户侧功能请求（内存防护、镜像瘦身）并行推进，社区参与度和维护响应速度均处于健康水平。

## 2. 版本发布

**v1.44.1**（补丁版本，链接：[Release 页面](https://github.com/OpenHands/software-agent-sdk/releases)）

**更新内容：**
- `feat(agent-server)`: 新增 `INSTALL_ACP_PROVIDERS` 构建参数（PR [#4687](https://github.com/OpenHands/software-agent-sdk/pull/4687)，允许在构建 agent-server 镜像时有选择地安装 ACP providers）。
- `chore(deps)`: 将 lmnr 依赖升级至 0.7.60（PR [#4688](https://github.com/OpenHands/software-agent-sdk/pull/4688)）。
- 验证并支持 DeepSeek v4 Flash 模型。

**破坏性变更与迁移注意：**
- 本次为补丁版本，**无明确破坏性变更**。
- 新增构建参数 `INSTALL_ACP_PROVIDERS` 为可选配置项，默认行为与先前版本一致；自定义 Docker 构建的用户无需额外操作。
- 依赖升级（lmnr）属于常规版本更新，未发现 API 变更。

## 3. 项目进展

今日虽无重大功能合入（过去24小时内合并/关闭 3 条 PR，但具体列表未公布），但值得注意的是，**多个重要 Issue 被关闭**，且其中不少是架构问题的修复结果：

- **流式传输架构整改推进**：经 #4689（PR）实现 streaming-delta 的 opt-in 机制后，关闭了 [#4672（webhook 被每个 token delta 轰炸）](https://github.com/OpenHands/software-agent-sdk/issues/4672) 和 [#4673（telemetry event_count 失真）](https://github.com/OpenHands/software-agent-sdk/issues/4673)。这标志着 `#4671 [Epic] Streaming: 分离线格式与持久事件记录` 的第一步已落地，为后续 Delta 事件独立化（#4696）铺平了道路。
- **项目技能加载修复**：关闭了 [#4019（ACP profiles 重复注入项目技能）](https://github.com/OpenHands/software-agent-sdk/issues/4019)。此前 PR #4018 引入的 `AgentContext(load_project_skills=True)` 行为已被确认并保留，修复了项目技能无法到达 profile 的问题。
- **性能优化**：关闭了 [#3906（EventLog.append 的 O(N²) 性能问题）](https://github.com/OpenHands/software-agent-sdk/issues/3906)。该问题为 #3263 的后续，随着新的性能 PR（如 [#4697](https://github.com/OpenHands/software-agent-sdk/pull/4697)）提交，旧问题被解决并关闭。
- **其他关闭项**：LLM profile 超时重置（#4032）、browser-use iframe 崩溃（#3753）、run-scoped LLM headers（#4064）、prompt caching TTL（#4292）、Grok OAuth（#4269）等。

**整体判断**：项目正在系统性地清理技术债务，并围绕“流式传输”这一核心架构问题进行分步重构。每一步都有明确的后续计划（#4696），显示出清晰的技术路线图。

## 4. 社区热点

今日讨论最活跃的话题围绕 **流式传输架构重构**（#4671 系列），该问题及其子 Issue 成为社区关注的核心：

- **[#4672 webhook 被 token 轰炸（已关闭，High priority）](https://github.com/OpenHands/software-agent-sdk/issues/4672)**：3条评论，但标签含 `priority:high, security-related, hooks, security`，是今日最值得关注的 Bug。用户 @VascoSch92 发现每生成一个 token delta 就会向配置的 webhook 发起一次 POST，存在信息泄露和资源消耗风险。该问题由 #4689 的 opt-in 机制修复，讨论中 @enyst 提出了关键疑问“deltas 不应该是 Events”，直接催生了后续 #4696 的架构调整。
- **[#4671 [Epic] 流式传输：分离线格式与持久事件记录](https://github.com/OpenHands/software-agent-sdk/issues/4671)**：作为该系列的总追踪 Issue，它揭示了当前架构中 Token delta 通过两条互不相知的通道（持久事件 vs. PubSub）传输的根本性问题，反映了社区对**可观测性和数据一致性**的强烈诉求。
- **[#4696 StreamingDeltaEvent 独立化](https://github.com/OpenHands/software-agent-sdk/issues/4696)**：作为 #4671 的下一步，由 @VascoSch92 与维护者 @enyst 的讨论直接催生，展示了社区协作推动架构演进的良好氛围。
- **其他活跃讨论**：[#4251（OWASP Agent Memory Guard 内存防护）](https://github.com/OpenHands/software-agent-sdk/issues/4251) 和 [#4259（reviewer-facing 证据门）](https://github.com/OpenHands/software-agent-sdk/issues/4259) 虽历史较长，但近期仍在积累评论（15条和11条），说明** agent 安全性和可审计性**是社区持续关注的热点。

## 5. Bug 与稳定性

按严重程度排列：

**高优先级（已修复/关闭）：**

- **[#4672 webhook 将每个 token delta POST 到网络钩子（已关闭，priority:high, security）](https://github.com/OpenHands/software-agent-sdk/issues/4672)**：配置 webhook 的对话在流式输出时，每个 token 增量都会被无条件 POST，属于**信息泄露 + 资源滥用**风险。修复方案已通过 #4689 的 opt-in 机制（`Subscriber.receives_streaming_deltas`）合入。⚠️ **关注点**：该修复默认仅 `_WebSocketSubscriber` 选择接收，其他订阅者（如 `_EventSubscriber`）不感知，需注意升级后的行为变化。

**中优先级（已修复/关闭）：**

- **[#4673 telemetry event_count 包含 token delta，导致跨会话不可比（已关闭）](https://github.com/OpenHands/software-agent-sdk/issues/4673)**：事件计数在 match 之前无条件累加，使指标失真。已随 #4672 一并修复。
- **[#4032 LLM profile 超时在 agent-server 重启后丢失（已关闭）](https://github.com/OpenHands/software-agent-sdk/issues/4032)**：重启后超时配置被重置为默认值。该问题已被修复（相关修复 PR 未列出，但关闭状态显示已解决）。
- **[#3753 browser-use 0.11.9 的 iframe detach 导致 DOM 提取失败（已关闭）](https://github.com/OpenHands/software-agent-sdk/issues/3753)**：网页中的广告/插件 iframe 会导致整个 DOM 提取崩溃，影响浏览器工具的可用性。

**新增未修复 Bug：**

- **[#4695 token delta 不再重置运行时空闲计时器，导致长时间流式传输时 pod 被回收（新开，无修复）](https://github.com/OpenHands/software-agent-sdk/issues/4695)**：这是 #4689 引入的回归——由于 `_EventSubscriber` 未 opt-in 接收 streaming deltas，长流式任务中空闲计时器被持续触发，可能造成 pod 中途被回收。**该 Bug 会对生产环境造成实际影响，需尽快制定修复方案**（或在 #4696 中一并解决）。

**修复 PR 已提交：**
- [#4697 使 EventLog.append 成本变为常数级](https://github.com/OpenHands/software-agent-sdk/pull/4697)，修复 #3906 的 O(N²) 性能问题。
- [#4582 修复文件编辑器在无尾部换行的文件末尾插入时错误拼接](https://github.com/OpenHands/software-agent-sdk/pull/4582)。

## 6. 功能请求与路线图信号

今日新增/活跃的功能请求主要集中在以下方向：

- **[#4696 StreamingDeltaEvent 不再继承 Event，拥有独立扇出（新开，ready-for-dev）](https://github.com/OpenHands/software-agent-sdk/issues/4696)**：这是 #4671 Epic 的下一步，旨在彻底将 token delta 从 Event 体系中剥离。**预计将在近期进入开发**，相关 PR 可能很快提交。
- **[#4645 将 OpenVSCode Server、Chromium 和桌面环境设为可选（ready-for-dev）](https://github.com/OpenHands/software-agent-sdk/issues/4645)**：这三项占 agent-server 镜像的 34.5%（564.9 MB），社区要求将其改为可选组件以精简镜像。**已标记 ready-for-dev**，可能是下一版本的候选特性。
- **[#4254 可插拔的持久化后端（durable execution backend）](https://github.com/OpenHands/software-agent-sdk/issues/4254)**：用户需要支持超长任务（超过 sandbox 会话窗口）。目前为开放性讨论，尚未进入开发路线图。
- **[#4251 OWASP Agent Memory Guard 集成（内存投毒防御）](https://github.com/OpenHands/software-agent-sdk/issues/4251)**：获得 15 条评论，反映社区对 agent 内存安全的重视。由于涉及范围大，短期内可能不会实施，但可视为长期安全路线图的一部分。
- **[#3598/#3599/#3600/#3601/#3602 OpenAI 网关增强系列](https://github.com/OpenHands/software-agent-sdk/issues/3598)**：这组由维护者 @enyst 提出的 roadmap 议题，包括 conversation 复用、操作 polish、final-answer streaming、Responses API、tool-call streaming。其中 **final-answer streaming** 可能在当前流式重构落地后推进。

## 7. 用户反馈摘要

从今日活跃的 Issues 评论和 PR 描述中，可以提取以下真实用户声音：

- **对流式传输架构现状的不满（@VascoSch92，来自 #4671/#4672/#4695）**：“Streamed text leaves the agent on two channels that know nothing about each other, and only one of them is tracked.” 用户指出当前 Streaming 存在双通道割裂问题，且 #4695 直接导致 pod 回收，**对生产稳定性构成威胁**。诉求是希望有一个统一的、可观测的流式架构。
- **对 webhook 滥用的担忧（#4672）**：用户发现“every token delta is POSTed to that webhook”，这不仅是性能问题，更可能是**安全事件**。Webhook 端点可能因高频请求被限流或误判为攻击。
- **对镜像体积膨胀的抱怨（#4645，由维护者 @simonrosenberg 提出）**：OpenVSCode、Chromium、桌面环境无条件打包，占镜像 34.5%——这对云上部署和带宽敏感场景是沉重的负担，用户希望获得裁剪选项。
- **对超时配置丢失的困惑（#4032）**：用户 @kripper 明确描述了“当 agent-server 重启时，配置的 LLM timeout 未保留，系统重置为默认值”。这说明**配置持久化**在重启用例中存在缺陷。
- **对深度性能问题的反馈（#3906）**：`EventLog.append` 在每次写入时进行全目录 listdir，导致 O(N²) 复杂度。用户 @tomsen02 的底层的技术剖析显示，在长会话中该问题会显著影响写入延迟。
- **功能性需求（#4269 Grok OAuth）**：用户希望新增 Grok 0auth 选项，但该 Issue 已被关闭，说明**该功能可能已实现、被拒绝或近期无计划**，需留意用户是否会有后续反馈。

## 8. 待处理积压

以下为长期未关闭且仍有价值的重要 Issue 或 PR，需引起维护者关注：

**长期开放的 Epic：**

- **[#2053 Skills

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-29

## 1. 今日速览

今日项目活跃度极高，PR 更新达到 229 条（其中 99 条已合并/关闭），Issue 更新 57 条（15 条已关闭，42 条活跃），另有 1 个 dev 版本发布。项目团队正在多点发力：企业级预算控制（#38647）、MCP Gateway 安全加固（#38724/#38726/#38728）、Bedrock/SageMaker 凭证链修复（#38727）、以及 OTel 可观测性补全（#38716）均有实质性推进。结合大量携带 stale 标签的旧 issue 被批量关闭，项目处于"快速迭代 + 积压清理"双轨运行状态，整体健康度良好。

---

## 2. 版本发布

### v1.100.0-dev.2（预发布版）
- **发布说明核心内容**：该版本为 dev 预发布版，重点在于验证 Docker 镜像签名机制——所有 LiteLLM Docker 镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 签名，每次发布使用同一签名密钥（源自 commit `0112e53`）。
- **破坏性变更**：未提及明确的破坏性变更。
- **迁移注意事项**：无特殊迁移要求。
- **数据观察**：版本号已达 v1.100，说明项目已进入百级版本迭代周期；dev 版发布频率（每日 1-2 个）表明团队保持持续集成节奏。

🔗 [查看 Release](https://github.com/BerriAI/litellm/releases)

---

## 3. 项目进展

今日合并/关闭的 PR 中有以下值得关注：

| PR | 内容 | 影响 |
|---|---|---|
| [#23971](https://github.com/BerriAI/litellm/pull/23971) | 修复 Bedrock Invoke API 对 Claude 4.6 的 `output_config.effort` 参数剥离问题 | 修复了 Claude 4.6 在 Bedrock 上无法使用 adaptive thinking 的问题，属于已存在较久的功能缺失补全 |
| [#34396](https://github.com/BerriAI/litellm/issues/34396) | 修复 Lakera v2 guardrail 忽略 `skip_system_message_in_guardrail` / `skip_tool_message_in_guardrail` 配置 | 让通用 guardrail 配置选项在 Lakera v2 上保持一致行为 |
| [#38715](https://github.com/BerriAI/litellm/pull/38715) | 将 RestrictedPython 依赖下限从 8.1 提升至 8.5 | 保障自定义代码 guardrail 沙箱的安全性，防止绕过 protected-name 检查 |

此外，以下新提交的 PR 值得关注（虽尚未合并但方向明确）：
- **#38727**：修复 Bedrock embeddings 和 SageMaker 在 credential loading 时丢失 `aws_external_id` 的问题——弥补了 Bedrock chat 路径已支持而其他路径缺失的不一致。
- **#38721**：修复 policy engine 中 `post_call` guardrail pipeline 解析了但不执行的问题，并修正了 `/policies/test-pipeline` 测试端点。

**整体评估**：项目今日并未推出突破性大功能，但修复了多个"看似可用实则存在隐藏缺陷"的路径，属于稳定性/一致性驱动的一天。对生产用户来说，这些修复的累积价值很高。

---

## 4. 社区热点

今日最受关注的 Issue/PR 如下：

### 🔥 #11929 — Usage Dashboard 支出报告与失败请求归因两个 Bug（15 条评论，已关闭）
- **链接**：https://github.com/BerriAI/litellm/issues/11929
- **讨论热点**：前端分页导致总支出被严重低估（跨页数据未正确汇总）；后端失败请求的 provider 归因显示为 0。
- **分析**：这是企业用户最痛的点——**计费数据不准确直接影响信任度**。该 issue 维护了 14 个月才关闭，也从侧面反映 dashboard 计费相关的改动在 LiteLLM 中优先级不够高。建议团队对 spend reporting 模块做一次系统性回归测试。

### 🔥 #33221 — OpenAI gpt-5.6 系列模型 tool calls 报 reasoning_effort 错误（12 条评论，已关闭）
- **链接**：https://github.com/BerriAI/litellm/issues/33221
- **讨论热点**：自托管 proxy 上，gpt-5.6-sol/luna/terra 等模型只要带 function tools 调用 `/chat/completions` 就会报 `reasoning_effort` 相关错误。
- **分析**：OpenAI 新一代模型的参数校验更严格，LiteLLM 在参数透传层需要不断适配。值得注意的是 #34301（temperature 校验）和 #33171（Azure gpt-5.5/5.6 拒绝非默认 temperature）也是同类问题，说明 **OpenAI 5.6 系列模型参数适配是近期社区的集中痛点**。

### 🔥 #24530 — /metrics 端点默认无认证暴露多租户 PII（8 条评论，未关闭）
- **链接**：https://github.com/BerriAI/litellm/issues/24530
- **讨论热点**：Prometheus `/metrics` 端点默认无需认证，在 production 部署中会暴露敏感的多租户数据。虽有 opt-in 配置 `require_auth_for_metrics_endpoint: true`，但默认不安全仍是风险。
- **分析**：这是一个**安全隐患+默认值设计**的讨论。社区用户对 LiteLLM 将"不安全"作为默认值表达了不满，后续版本中应关注默认值策略的调整。

---

## 5. Bug 与稳定性

按严重程度排列今日值得关注的 Bug：

### 🔴 严重（影响生产可用性）

| Issue | 描述 | 状态 |
|---|---|---|
| [#38629](https://github.com/BerriAI/litellm/issues/38629) | Team model access 在请求时执行但在 `/key/generate` 时未执行，且 `/key/update` 校验的是更新前的 model 列表——两种路径不一致，容易踩坑难排查 | 🆕 新开，无 fix PR |
| [#37988](https://github.com/BerriAI/litellm/issues/37988) | GCP Terraform 模块已配置 Redis，但 proxy 报告无 coordination Redis——基础设施与运行时状态不一致 | 🆕 新开（8/23），无 fix PR |

### 🟡 中等

| Issue | 描述 | 状态 |
|---|---|---|
| [#38060](https://github.com/BerriAI/litellm/issues/38060) | Dashboard Logs 视图分页按 message 计数而非按 session 分组计数，导致分页数与显示组数不匹配 | 🆕 新开（8/24），3 条评论，无 fix PR |
| [#29342](https://github.com/BerriAI/litellm/issues/29342) | `LiteLLM_SpendLogToolIndex` 只有插入没有清理，spend log 保留策略删除旧数据后该索引成孤儿，无限增长 | 长期未修复（5/30 创建），仅 1 条评论 |
| [#29348](https://github.com/BerriAI/litellm/issues/29348) | Helm chart 默认 image tag 为 `main-<appVersion>`，但 ghcr 上稳定版不存在该 tag，导致 `ImagePullBackOff` | 长期未修复（5/30 创建），仅 1 条评论 |
| [#36401](https://github.com/BerriAI/litellm/issues/36401) | Gemini `thinkingConfig.includeThoughts` 被硬编码为 True，`reasoning_effort` 设置时无法关闭 thought summaries | 未关闭，2 条评论，👍1 |

### 🟢 轻微

| Issue | 描述 | 状态 |
|---|---|---|
| [#28880](https://github.com/BerriAI/litellm/issues/28880) | 用户邮箱创建时未 trim 前导空格，导致后续登录/密码重置失败 | 2 条评论，未修复 |

---

## 6. 功能请求与路线图信号

今日最值得关注的功能需求及其路线图信号：

### 高概率纳入近期版本

| 需求 | 信号 |
|---|---|
| **MCP Gateway 支持非对称签名（RS256）**（PR [#38728](https://github.com/BerriAI/litellm/pull/38728)）| devin-ai-integration[bot] 提交，方向明确，属于 MCP 安全体系补全 |
| **MCP Gateway 支持 RFC 7662 OAuth introspection**（PR [#38726](https://github.com/BerriAI/litellm/pull/38726)）| 同属 MCP 安全系列，与外部 gateway 集成相关 |
| **Per-user MCP OAuth 凭证绑定到认证调用者**（PR [#38724](https://github.com/BerriAI/litellm/pull/38724)）| 修复了"任意授权 grant 落入任意用户凭证槽"的身份隔离问题 |
| **AI Power Grid 新 provider 接入**（PR [#38725](https://github.com/BerriAI/litellm/pull/38725)）| 新 OpenAI-compatible provider 注册，含定价元数据 |

### 社区呼声较高

| 需求 | 信号 |
|---|---|
| **Anthropic Workload Identity Federation（OIDC JWT-bearer）**（[#28607](https://github.com/BerriAI/litellm/issues/28607)）| 5 条评论，👍3，属于云原生场景下的企业认证需求，但暂无对应 PR |
| **强制安全标识符（immutable user_id）**（[#14505](https://github.com/BerriAI/litellm/issues/14505)）| 企业级安全需求，P1 标签，2025-09 提出至今未落地，已有 5 条讨论 |
| **Usage dashboard 支持单用户多 key 的日用量对比**（[#28234](https://github.com/BerriAI/litellm/issues/28234)）| 用户体验类需求，暂无 PR |

---

## 7. 用户反馈摘要

从今日 Issues/PR 评论中提炼的真实声音：

**"计费数据不可信"是最痛的反馈**
> [#11929](https://github.com/BerriAI/litellm/issues/11929) 用户描述了两个具体 bug："总支出在跨页时严重少报"、"失败请求的 provider 归因全显示 0"。这直接冲击了用户对 dashboard 的信心。

**对 OpenAI 新模型适配速度的关注**
> [#33221](https://github.com/BerriAI/litellm/issues/33221) 和 [#34301](https://github.com/BerriAI/litellm/issues/34301) 中，用户对 gpt-5.6 系列的参数校验问题表达了困惑，尤其是 `drop_params` 不能生效的场景（#33171），因为"param-dropping layer 只移除它认识的参数"。

**对默认安全性的不满**
> [#24530](https://github.com/BerriAI/litellm/issues/24530) 用户明确指出：`/metrics` 默认无认证是"广泛存在的真实风险"。虽然已有 opt-in 配置，但用户期望的是 secure-by-default。

**对 Terraform 模块配置与运行时不一致的困惑**
> [#37988](https://github.com/BerriAI/litellm/issues/37988)：Terraform 配了 Redis 但 proxy 说没有，这类"基础设施说一套、运行时做另一套"的问题极大增加排障成本。

**对长期未修 Bug 的无奈**
> [#29342](https://github.com/BerriAI/litellm/issues/29342)（SpendLogToolIndex 无限增长）、[#29348](https://github.com/BerriAI/litellm/issues/29348)（Helm 默认镜像 tag 拉不下来）都已搁置 3 个月以上，社区用户的隐含诉求是"请维护者至少标记计划修复的版本"。

---

## 8. 待处理积压

以下问题长期未得到有效响应或修复，建议维护者优先关注：

| 项目 | 关键信息 | 搁置时长 |
|---|---|---|
| [#14505](https://github.com/BerriAI/litellm/issues/14505) [P1] 强制 safety identifiers | 企业级安全需求，P1 优先级但近一年未推进 | 2025-09 创建，近 12 个月 |
| [#29348](https://github.com/BerriAI/litellm/issues/29348) Helm chart 默认镜像 tag 不存在 | 直接导致用户安装失败（ImagePullBackOff），影响面大 | 2026-05-30，3 个月 |
| [#29342](https://github.com/BerriAI/litellm/issues/29342) SpendLogToolIndex 无清理机制 | 数据库无限增长风险，且与 retention 策略矛盾 | 2026-05-30，3 个月 |
| [#24530](https://github.com/BerriAI/litellm/issues/24530) /metrics 默认无认证 | 安全隐患，讨论热度高（8 条评论）但仍未修复 | 2026-03-24，5 个月 |
| [#28607](https://github.com/BerriAI/litellm/issues/28607) Anthropic WIF 支持 | 👍3，企业级认证需求，暂无对应 PR | 2026-05-22，3 个月 |
| PR [#33010](https://github.com/BerriAI/litellm/pull/33010) v3 rate limiter 跳过未配置 key 的 Redis 写入 | 修复了 issue #31880，已有测试，但 48 天未合并 | 2026-07-12

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-29

## 今日速览

过去24小时项目活跃度较高：PR 更新 55 条，其中 14 条已合并/关闭，41 条待合并，显示核心功能开发进入密集提交期；Issue 侧更新仅 3 条，其中 2 个已关闭（均为 enhancement 类），1 个严重 Bug 被报告。今日无新版本发布，但 PR 池中涉及 worker callbacks、Nexus、Scheduler v2、reliability-2026 等多项重点方向的推进，项目处于功能迭代与稳定性加固并行的阶段。

## 项目进展

今日合并/关闭的 PR 集中在以下方向：

**Scheduler 修复** — [#11630](https://github.com/temporalio/temporal/pull/11630) 修复了 `ExecuteTask` 中 terminate、cancel、start 三个阶段分别独立消耗 action 预算的问题，改为共享同一预算，防止单次执行超限。

**Worker Commands 文档化** — [#11648](https://github.com/temporalio/temporal/pull/11648) 为 worker command 控制队列补充了 `TASK_QUEUE_KIND_WORKER_COMMANDS` 的说明文档，提升可观测性。

**复制路径健壮性** — [#11052](https://github.com/temporalio/temporal/pull/11052) 在处理被动复制路径上的僵尸/孤儿工作流时，若 `currentRunID == ""`，调用 `CreateWorkflowModeBypassCurrent` 保留持久化状态，修复了可能的数据丢失风险。

**附加进展（仍开放但高度活跃）**：worker shutdown poll 注册竞态修复（[#11841](https://github.com/temporalio/temporal/pull/11841)）、perNamespaceWorker 初始化数据竞争修复（[#11825](https://github.com/temporalio/temporal/pull/11825)）均已完成实现并进入审查阶段，属于 reliability-2026 方向的稳定性推进。

## 社区热点

今日讨论热度最高的 Issue 是 **[#11842](https://github.com/temporalio/temporal/issues/11842)**—“Worker Deployment routingConfigUpdateState stays IN_PROGRESS forever”，由 @pnoker 于 8月28日 报告，虽然暂无评论，但标题直接点出该问题可阻塞所有 worker deployment 的 rollout，严重性极高，预计将吸引大量关注。

PR 侧评论数据未返回（均为 `undefined`），但 [#11589](https://github.com/temporalio/temporal/pull/11589) “Support Worker-variant callbacks” 作为 worker callbacks 功能堆栈中最核心的实现 PR，以及 [#10128](https://github.com/temporalio/temporal/pull/10128) CLI 版本提升 PR（标记为 stale 但仍在更新），均是值得关注的活跃讨论对象。

## Bug 与稳定性

按严重程度排序：

**🔴 严重（阻塞发布）**
- **[#11842](https://github.com/temporalio/temporal/issues/11842)** — `routingConfigUpdateState` 永久停留在 `IN_PROGRESS`，导致 workflow+activity 任务队列永远无法被提升为 current，阻碍所有 worker deployment 滚动更新。目前无评论、无关联 fix PR，处于“刚报告待确认”状态。

**🟠 中等（数据竞争/竞态）**
- worker shutdown poll 注册竞态（[#11841](https://github.com/temporalio/temporal/pull/11841)）— 已有修复 PR，等待审查合入。
- perNamespaceWorker 初始化数据竞争（[#11825](https://github.com/temporalio/temporal/pull/11825)）— 已有修复 PR，并附带动态配置回调注册的锁顺序修复。

**🟡 较低（可靠性加固）**
- History 服务被重复失败的 Task Queue 注册请求打爆的风险（[#11858](https://github.com/temporalio/temporal/pull/11858)）— 通过缓存 WD Client 中的 Deployment 限制和未知错误来缓解，PR 已提交。
- worker command 轮询超时导致的 goroutine 阻塞（[#11851](https://github.com/temporalio/temporal/pull/11851)）— 停止对 `UpstreamTimeout` 重试，PR 已提交。

## 功能请求与路线图信号

**新功能请求**：
- **[#11844](https://github.com/temporalio/temporal/issues/11844) — Rust SDK 支持**（已关闭）：用户明确希望 Temporal 提供 Rust SDK。虽然该 Issue 被关闭，但结合近期社区对 Rust 生态的关注，这可能是 Temporal 未来语言扩展方向的潜在信号。
- **[#11718](https://github.com/temporalio/temporal/issues/11718) — release archive 中包含开发 CLI**（已关闭）：用户希望发布归档中直接附带 `temporal` 开发 CLI，便于通过工具链管理依赖。该请求已获 2 条评论，说明有讨论价值。

**从 PR 推断的路线图信号**：
- **Worker callbacks 功能堆栈**（[#11589](https://github.com/temporalio/temporal/pull/11589)、[#11566](https://github.com/temporalio/temporal/pull/11566)、[#11520](https://github.com/temporalio/temporal/pull/11520)）仍在持续推进中，其中 [#11520](https://github.com/temporalio/temporal/pull/11520) 将补充 `CallbackInfo.outcome` 字段，属于功能完整性的重要补齐。
- **Scheduler V2 版本控制**（[#11831](https://github.com/temporalio/temporal/pull/11831)、[#11856](https://github.com/temporalio/temporal/pull/11856)）正在构建 per-iteration 版本天花板评估和命名空间级 promotion 控制，为渐进式推动 V2 调度器铺路。

## 用户反馈摘要

从 Issue 评论中提炼的用户声音：

- **Mise 用户的部署诉求**（[#11718](https://github.com/temporalio/temporal/issues/11718)）：用户使用 [Mise](https://github.com/jdx/mise) 管理项目依赖，其机制仅能安装 release archive 中打包的二进制文件，因此希望 Temporal 将开发 CLI 也放入发布归档。这表明部分用户越来越依赖于工具链自动化的部署方式，希望避免手动下载。
- **Rust 社区声音**（[#11844](https://github.com/temporalio/temporal/issues/11844)）：用户以简洁的请求表达了对 Rust SDK 的期待，反映出部分开发者生态中存在对 Rust 客户端的需求，但在当前 SDKS（Go/Java/TypeScript/Python/.NET）外，Rust 尚未进入官方路线图。

## 待处理积压

整体 backlog 健康度良好，绝大多数 PR 和 Issue 在过去 24-48 小时内有更新。以下项目值得关注：

- **[#10128](https://github.com/temporalio/temporal/pull/10128)**：标记为 `[stale]`，但仍在持续更新（最后更新于 8月29日），涉及 CLI 版本从 1.6.1 → 1.7.0 的默认设定，属于低风险依赖升级，建议尽快合入。
- **[#11463](https://github.com/temporalio/temporal/pull/11463) “Schedule v2 replay fidelity”**：创建于 8月10日，仍在积极更新（最后更新于 8月28日），属于 Scheduler V2 正确性验证的重要工作，体量较大，需持续跟踪。
- **[#11757](https://github.com/temporalio/temporal/pull/11757) “Tag Nexus logs by lifecycle stage”**：8月24日创建，更新至 8月28日，Nexus 可观测性改进，等待审查。

---

*本日报基于 2026-08-29 的 GitHub 公开数据自动生成，仅供项目健康度参考。*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*