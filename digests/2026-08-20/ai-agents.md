# OpenClaw 生态日报 2026-08-20

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-19 22:45 UTC

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

# 个人 AI 助手/自主智能体开源生态横向对比分析报告

**报告日期：** 2026-08-20
**数据范围：** 2026-08-19 → 2026-08-20（24 小时）
**覆盖项目：** Hermes Agent、LiteLLM、Temporal、OpenClaw


## 1. 生态全景

个人 AI 助手与自主智能体开源生态正处于**高烈度迭代期**，头部项目日 PR 提交量达数百条，但合入门槛与维护者瓶颈开始显现（Hermes 合并率仅 21%）。生态竞争焦点正从基础对话能力转向**工具链可靠性、第三方模型兼容性、生产级可观测性**三大方向，Windows 更新流程、DeepSeek 兼容性、MCP 工具执行安全等具体问题高频出现，说明用户已经从"跑通 Demo"进入"生产可用"阶段。同时，底层基础设施（LiteLLM 网关、Temporal 编排引擎）与终端 Agent（Hermes）之间的分工已清晰形成，上层应用繁荣与底层稳定性加固正在同步进行。

## 2. 各项目活跃度对比

| 项目 | Issues（24h） | PR（24h） | Release | 合并率 | 健康度评估 |
|------|--------------|----------|---------|--------|-----------|
| **Hermes Agent** | 414（关闭 57） | 500（合并/关闭 104） | 无 | ~21% | 活跃度极高，但合并瓶颈明显，大量 PR 长期滞留 |
| **LiteLLM** | 72（关闭 19） | 306（合并/关闭 122） | v1.99.0-dev.1 | ~40% | 活跃且健康，修复响应及时，维护节奏稳定 |
| **Temporal** | 23（关闭 2） | 82（合并/关闭 29） | 无 | ~35% | 高强度稳定迭代，偏重质量巩固，待合并积压中等 |
| **OpenClaw** | 本次报告未提供 | — | — | — | 无法评估（无社区动态数据） |

**整体判断：** 三个有数据的项目均处于高度活跃状态。LiteLLM 的健康度最优（合并率 40%），Hermes 的社区声量最大但维护效率承压，Temporal 呈现典型的"基础设施型"稳健节奏。

## 3. OpenClaw 在生态中的定位

> 说明：本次各项目动态摘要中未包含 OpenClaw 的具体社区数据（Issues/PR/Release 等），无法进行基于当日活跃度的定量对比。以下定位分析基于其他项目的横向参照与生态结构推断，供参考。

- **生态生态位：** OpenClaw（核心参照项目）在生态中扮演的是**终端用户 Agent 框架**角色，与 Hermes Agent 构成直接竞品关系。二者同属"人人可用的个人 AI 助手"赛道，面对的是同一批追求本地部署、多模型接入、工具扩展能力的开发者用户。
- **差异化空间：** Hermes 今日的高频迭代集中在 Desktop Profile 管理、Bot Mode、Windows 更新修复——这些恰是个人 Agent 项目从"开发者玩具"走向"日常工具"的必经关卡。OpenClaw 的**技术路线差异**若体现在更轻量的架构、更强的开箱即用性或更活跃的周边生态，将有机会在 Hermes 被合并瓶颈拖累的窗口期形成差异化优势。
- **社区规模参照：** 从 Hermes 单日 414 条 Issue / 500 条 PR 的体量来看，终端 Agent 赛道的社区参与度极高。LiteLLM 与 Temporal 作为基础设施，社区声量相对较小但更聚焦。OpenClaw 若与 Hermes 处于同一量级，其社区活跃度应属于第一梯队。
- **风险提示：** Hermes 今日暴露的 P1 问题——Windows 更新删除应用、Profile 会话无法加载、DeepSeek 长上下文永久死锁——极有可能同样困扰着所有终端 Agent 项目。这类**跨平台桌面稳定性**问题已成为该赛道的关键竞争壁垒。

## 4. 共同关注的技术方向

### 4.1 第三方模型兼容性（投入最大、用户呼声最高）

| 项目 | 具体表现 |
|------|---------|
| **Hermes Agent** | DeepSeek 400 错误（#83390）、DeepSeek 500k 上下文会话永久死亡（#78981，P1）；PR #90330 修复推理级别词汇表跨模型翻译 |
| **LiteLLM** | DeepSeek V4 Flash 价格表请求（#28309）、GPT-5.4 订阅模型支持（#25954）、Gemini 3.5/3.6 Flash 缓存触发条件修正（#37516）、Anthropic/Bedrock 思考 token 计费修正（#35998） |

**信号：** 生态对"非 Anthropic 模型"的支持已从"能跑就行"升级到"必须行为一致"（推理参数、token 计费、响应格式、缓存语义）。

### 4.2 MCP（Model Context Protocol）工具调用的安全与可靠性

| 项目 | 具体表现 |
|------|---------|
| **LiteLLM** | MCP auto-execute 劫持客户端原生工具（#37031，高严重度）；PUT /v1/mcp/server 静默清空 OAuth 字段（#37258）；MCP 凭据输出脱敏 PR（#84153） |
| **Hermes Agent** | OAuth-backed MCP 服务器 keepalive 重连后永久死锁（#38193）；MCP 工具选择与凭据解析修复（#90317） |
| **Temporal** | 与 MCP 无直接关联，但 CallbackInfo、支持 callback kinds 可配置等 PR 体现了外部系统集成生命周期管理的同一方向 |

**信号：** MCP 从协议概念走向生产实践后，**凭据安全、自动执行边界、重连/死锁、配置持久化** 成为全生态共性痛点。

### 4.3 可观测性与成本核算

| 项目 | 具体表现 |
|------|---------|
| **Temporal** | 集群成员状态 gauges（#11146）、失败请求部署归属（#11520）、Nexus 日志标签增强 |
| **LiteLLM** | 失败请求 spend 日志补全部署归属（#37520）、错误响应透传 model-id（#37533）、Vertex 区域端点成本加价 1.1x 修正（#37543）、缓存命中 token 可观测（#36091） |
| **Hermes Agent** | Skills 索引过期监控告警（#66616，59 评论）、CPU 异常占用（#88275） |

**信号：** 无论是 Agent 框架、网关还是编排引擎，**用户都要求能回答"钱花在哪、请求走哪个部署、工作流为什么慢"**。AI 基础设施的观测体系正从"日志级别"向"成本/归因/健康度"三维度升级。

### 4.4 桌面端与更新流程稳定性

| 项目 | 具体表现 |
|------|---------|
| **Hermes Agent** | 7 个 P1 问题中 4 个与桌面/更新直接相关（#89675 Profile 会话丢失、#83846 ZIP 回退删除应用、#63717 更新失败综合诊断、#83529 彻底破坏本地安装） |
| **LiteLLM** | UI 现代化改造（antd → shadcn），迁移 52 个文件/65 处调用（#37540、#37524） |
| **Temporal** | 无直接桌面相关，但 UI 403 权限问题影响 Web 体验（#11639） |

**信号：** 终端 Agent 的"桌面化"进程正在付出代价——**更新机制本身就是最大的稳定性风险源**。同时，Web UI 的技术栈现代化（antd → shadcn）在各项目间同步发生，表明开发者工具正在追求更统一、更轻量的前端范式。

## 5. 差异化定位分析

| 维度 | Hermes Agent | LiteLLM | Temporal | OpenClaw |
|------|-------------|---------|----------|----------|
| **核心定位** | 终端用户个人 AI 助手（桌面应用 + Agent） | LLM 网关 / 统一 API 代理层 | 持久化工作流编排引擎 | 个人 AI 助手框架（参照基准） |
| **目标用户** | 个人开发者、Bot 运营者、桌面用户 | 企业平台/网关运维、模型供应商 | 平台工程、后端开发者 | 个人开发者、研究者 |
| **技术架构** | 桌面应用（Electron）+ 后端服务 + Profile/多连接架构 | 代理/网关模式，请求路由、成本跟踪、UI 控制台 | 分布式事务队列、调度器、worker 版本管理 | 未提供数据，推测为 Agent 框架 |
| **核心壁垒** | 工具链广度、Bot Mode 生态、桌面端体验 | 模型覆盖矩阵（数百供应商）、成本核算精度、企业级治理 | 持久性保证、分布式一致性、故障恢复 | 待确认 |
| **当前阶段** | 功能高速扩展期，稳定性短板明显 | 功能扩张 + 成本/可观测性精修并行 | 质量巩固期，新功能审慎推进 | 无法评估 |

**关键差异总结：** 三者处于 AI 应用栈的不同层级——Hermes 在上层直接服务终端用户，LiteLLM 在中层做模型接入与治理，Temporal 在底层保证工作流不丢不重。**它们不直接竞争，但共享同一波 AI Agent 生态红利。** Hermes 与 LiteLLM 之间存在隐性的"上游依赖"关系：LiteLLM 的模型兼容性修复、MCP 安全改进，最终会传导为 Hermes 类终端 Agent 的稳定性提升。

## 6. 社区热度与成熟度

| 分层 | 项目 | 特征 | 判断 |
|------|------|------|------|
| **第一梯队：超高活跃、快速迭代** | Hermes Agent（414 Issues / 500 PRs） | 合并率仅 21%，大量 PR 累积，新功能密集（Bot Mode、profile_manage、sync-fork），但 P1 bug 积压 | **功能扩张快于质量巩固**，处于跑马圈地阶段，社区热情高涨但维护者亟需补充 |
| **第二梯队：活跃且健康** | LiteLLM（72 Issues / 306 PRs） | 合并率 40%，有明确迭代主线（成本核算、UI 现代化、复杂性路由），bug 修复响应快 | **攻守兼备**，既推新功能又在系统化解决生产环境问题，处于最健康的迭代节奏 |
| **第三梯队：稳健加固** | Temporal（23 Issues / 82 PRs） | 合并率 35%，重心在事件缓存作用域、队列 GC 竞态、调度边界等深水区问题 | **典型的基础设施成熟期**，社区讨论少而精，大规模生产部署背书 |
| **数据缺失** | OpenClaw | — | 本期无法评估 |

**结论：** 当前生态**没有出现明显的"衰退期"项目**。Hermes 的高活跃低合并率是唯一值得警惕的信号——如果持续数周，可能挫伤贡献者积极性。

## 7. 值得关注的趋势信号

### 信号 1：多模型兼容性正在成为 Agent 框架的生命线
Hermes（DeepSeek 400/死锁）和 LiteLLM（Gemini 缓存阈值、Anthropic 思考 token 计费、GPT-5.4 支持延迟）的社区反馈共同指向：**用户对"绑定单一模型供应商"的容忍度已经降至零**。任何模型适配的瑕疵都会迅速升级为高热度 Issue。对开发者而言，在架构设计之初就将模型层抽象为可插拔接口，并建立持续集成式的模型兼容性测试，已是必需项而非加分项。

### 信号 2：MCP 安全与可靠性是下一个主战场
LiteLLM 的 MCP auto-execute 劫持问题、Hermes 的 MCP OAuth 死锁问题，都发生在过去 30 天内且被标记为高严重度。MCP 生态正在从"能连上"进入"能安全自动执行"的深水区。**智能体工具调用的授权边界、凭据生命周期、自动执行审批策略**将是未来 6-12 个月的工具链创新密集区。

### 信号 3：可观测性需求从"技术指标"升级为"业务成本指标"
LiteLLM 三天内两个 PR 直指"失败请求不知道走了哪个部署"（#37520、#37533）；Temporal 在推进 membership gauges；Hermes 的 Skills 索引过期告警已经挂了 33 天（#66616）无人修复——**基础设施团队正在用云原生时代的标准来要求 AI 基础设施**：每个 token、每次调用、每条工作流都要可追踪、可归因、可计费。

### 信号 4：更新/升级流程正在成为桌面端 Agent 的头号稳定性杀手
Hermes 的 7 个 P1 问题中 4 个与更新相关。用户已经足够信任 Agent 以至于把自动化任务交给它，但 Agent 自己在升级时却把数据搞丢了。**"管家能不能管好自己的升级"** 是对 Agent 项目工程成熟度的最直接考验，也是建立用户信任的关键分水岭。

### 信号 5：高活跃不等于高产出——合并瓶颈成为生态共同挑战
Hermes 396 条 PR 待合并、Temporal 53 条待合并，乃至 LiteLLM 的 184 条，共同揭示了一个结构性矛盾：**社区提交速度已远超维护者 review 能力**。对项目方而言，自动化测试门禁（LiteLLM 已开始推动"仅跑相关测试"以降低 CI 成本）、分层维护者机制、机器人辅助 triage 将成为刚需。对贡献者而言，选择合入门槛低、反馈及时的项目贡献 ROI 更高。

---

**免责声明：** 本报告基于 2026-08-20 指定项目的 GitHub 社区动态摘要。OpenClaw、OpenHands SDK、Pi 项目因本次动态数据未提供而未能纳入定量对比，相关分析仅为基于生态结构的定性推断。数据统计口径以各项目日报为准。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-20

> 数据来源：github.com/NousResearch/hermes-agent  
> 统计周期：过去 24 小时（截至 2026-08-20）

---

## 1. 今日速览

过去 24 小时内，Hermes Agent 项目保持**极高活跃度**：Issues 更新 414 条（新开/活跃 357，关闭 57），PR 更新 500 条（待合并 396，已合并/关闭 104）。社区提交密集，尤其集中在 **Desktop 会话/Profile 状态管理、Windows 更新流程、DeepSeek/第三方模型兼容性、以及工具链安全加固** 四个方向。值得注意的是，尽管 PR 提交量巨大（500 条），合并率仅为约 21%，大量 PR 待维护者 review。过去 24 小时无新版本发布，最新稳定版仍为 v0.20.x 系列。

---

## 2. 版本发布

**无新版本发布。** 当前最新版本仍为 v0.20.4（upstream `c69b6471e6`），上一个发布版本 v0.20.2（2026-08-16）。

---

## 3. 项目进展

过去 24 小时有 **104 条 PR 被合并或关闭**，57 个 Issue 被关闭，整体推进节奏明显。

**关键进展与信号：**

- **Desktop Profile 切换系列 bug 已修复**：三个高优先级 Issue — [#89622 "Profile switching is broken!"](https://github.com/NousResearch/hermes-agent/issues/89622)、[#89586 "Desktop: profile switching hangs silently"](https://github.com/NousResearch/hermes-agent/issues/89586)、[#88251 "Windows get-windows binding never staged"](https://github.com/NousResearch/hermes-agent/issues/88251) — 均在今日标记为 CLOSED，说明会话/Profile 机制的最新回归已得到处理。
- **大量新 PR 集中在“Bot Mode”增强**：包括 [#90331 profile_manage 工具](https://github.com/NousResearch/hermes-agent/pull/90331)（Agent 创建 Bot 的治理化路径）、[#90329 跨连接群组创建](https://github.com/NousResearch/hermes-agent/pull/90329)、[#90328 自定义 default bot handle](https://github.com/NousResearch/hermes-agent/pull/90328)、[#90326 Bot roster 活动信号修复](https://github.com/NousResearch/hermes-agent/pull/90326)。表明 Bot Mode 正在成为桌面端的重点迭代方向。
- **工具层大幅修复**：多个 PR 修复了工具选择与凭据解析问题（[#90317](https://github.com/NousResearch/hermes-agent/pull/90317)）、搜索输出非纯 JSON 问题（[#90325](https://github.com/NousResearch/hermes-agent/pull/90325)）、无凭据时 web_search 不可用问题（[#90313](https://github.com/NousResearch/hermes-agent/pull/90313)），覆盖 `search_files`、`web_search`、`web_extract` 等常用工具。
- **模型兼容性修复**：[#90330 "reasoning effort 'ultra' no longer 400s"](https://github.com/NousResearch/hermes-agent/pull/90330) 将 Hermes 内部推理努力级别词汇表在所有模型线路上进行翻译修正，修复了非 Anthropic 模型（如 DeepSeek/OpenRouter）400 错误的问题，覆盖 #89503 bug 类别。

**积压警示：** 今日 396 条 PR 处于待合并状态，大量 PR 已开放数周（如 #84153、#82775、#77548、#71996），合并瓶颈明显。

---

## 4. 社区热点

### 讨论最热的 Issue/PR TOP 3

| 排名 | 编号 | 标题 | 评论数 | 状态 |
|------|------|------|--------|------|
| 1 | [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) | [skills-index-watchdog] Skills index is stale or degraded | 59 | OPEN |
| 2 | [#84834](https://github.com/NousResearch/hermes-agent/issues/84834) | Webhook Feature Package — graph-gated repair (meta-issue) | 19 | OPEN |
| 3 | [#83390](https://github.com/NousResearch/hermes-agent/issues/83390) | Auxiliary title_generation fails on DeepSeek: HTTP 400 | 17 | OPEN |

**分析：**

- **#66616（59 条评论）** — 这是一个自动化探针持续告警：Skills 索引已过期 29.8 小时（阈值 26 小时）。该 Issue 自 7 月 18 日开放至今已超过一个月仍未被解决，59 条评论说明维护者和社区在反复讨论但未落地修复。**核心诉求：CI/CD 自动化管线的可靠性问题被长期忽视。**

- **#84834（19 条评论）** — Webhook 功能包修复的重度 meta-issue，涵盖 ingress、执行、投递、配置、管理 UI、部署和文档全链路。这是社区驱动的系统性质量问题追踪，体现用户对 Webhook 表面整体质量的关注。

- **#83390（17 条评论，👍 2）** — DeepSeek 的 `title_generation` 辅助任务在 `provider: auto` 路由下返回 HTTP 400 `"This response_format type is unavailable now"`。DeepSeek 兼容性问题连续多日成为社区热点（另有 #78981 DeepSeek 500k 上下文会话永久死亡的 P1 问题），反映第三方模型集成稳定性的用户诉求强烈。

---

## 5. Bug 与稳定性

### P1 严重级别（按影响面排序）

| 编号 | 标题 | 状态 | Fix PR |
|------|------|------|--------|
| [#89675](https://github.com/NousResearch/hermes-agent/issues/89675) | Desktop: 更新后所有 Profile 会话无法加载 — backend 未带 `--profile` 启动 | OPEN（11 评论，👍2） | 无 |
| [#83846](https://github.com/NousResearch/hermes-agent/issues/83846) | Windows: ZIP 回退更新逻辑删除桌面应用且不重建；后续更新报 "Already up to date" | OPEN（11 评论） | 无 |
| [#78981](https://github.com/NousResearch/hermes-agent/issues/78981) | DeepSeek 500k token 会话：压缩挂起后会话永久死亡，后续消息不再触发新一轮 | OPEN（7 评论） | 无 |
| [#63717](https://github.com/NousResearch/hermes-agent/issues/63717) | Windows 桌面更新失败 — 7 个关联根因综合诊断 | OPEN（8 评论） | 无 |
| [#83529](https://github.com/NousResearch/hermes-agent/issues/83529) | `hermes update` 彻底破坏本地安装 | OPEN（6 评论） | 无 |
| [#51327](https://github.com/NousResearch/hermes-agent/issues/51327) | Linux `.desktop` 启动器静默失败：Electron chrome-sandbox 缺 setuid 4755 | OPEN（11 评论，6/23 开放） | 无 |

### P2 中等级别（值得关注）

| 编号 | 标题 | 状态 | Fix PR |
|------|------|------|--------|
| [#88275](https://github.com/NousResearch/hermes-agent/issues/88275) | Desktop Renderer 进程空闲时 CPU 40-70%，macOS Intel 热降频 | OPEN（9 评论） | 无 |
| [#85695](https://github.com/NousResearch/hermes-agent/issues/85695) | 误报 "TERMINAL_CWD deprecated" 警告（来自环境变量非 .env） | OPEN（11 评论，👍3） | ✅ [#90320](https://github.com/NousResearch/hermes-agent/pull/90320) |
| [#43900](https://github.com/NousResearch/hermes-agent/issues/43900) | Ollama 本地模型被静默限制为 4096 token 上下文，导致 `finish_reason=length` | OPEN（11 评论） | 无 |
| [#80989](https://github.com/NousResearch/hermes-agent/issues/80989) | v0.20.0 终端/clarify 工具结果被 content-block 包装，偶尔返回错误文件内容 | OPEN（7 评论） | 无 |
| [#66255](https://github.com/NousResearch/hermes-agent/issues/66255) | Gateway 数据库会话恢复绕过重置策略，会话跨重启“永生” | OPEN（5 评论） | 无 |
| [#38193](https://github.com/NousResearch/hermes-agent/issues/38193) | OAuth-backed MCP 服务器在 keepalive 重连后永久死锁 | OPEN（5 评论，6/3 开放） | 无 |

### 安全类 PR（有 fix 未合并）

| 编号 | 标题 | 状态 | 备注 |
|------|------|------|------|
| [#90324](https://github.com/NousResearch/hermes-agent/pull/90324) | Copilot 需要显式 opt-in 才探测 GitHub token | OPEN | 修复 #35946 |
| [#84577](https://github.com/NousResearch/hermes-agent/pull/84577) | 解包命令包装器后再做危险命令检测 | OPEN | 修复 #84551 绕过 |
| [#71996](https://github.com/NousResearch/hermes-agent/pull/71996) | 阻止绝对路径拼写绕过 hardline floor | OPEN | 修复 #71995 |
| [#84153](https://github.com/NousResearch/hermes-agent/pull/84153) | config get 输出中脱敏 MCP 凭据 | OPEN | — |
| [#82775](https://github.com/NousResearch/hermes-agent/pull/82775) | 插件命令按注册名做 gate | OPEN | Telegram 插件命令绕过 |
| [#84093](https://github.com/NousResearch/hermes-agent/pull/84093) | 限制有漏洞的 pydantic-settings 和 Pygments 版本 | OPEN | 依赖安全 |

---

## 6. 功能请求与路线图信号

### 可能是下一版本的方向（来自今日新 PR）

| PR/Issue | 功能 | 价值判断 |
|----------|------|----------|
| [#90313](https://github.com/NousResearch/hermes-agent/pull/90313) | 全新安装无 API key 时 web_search 默认走 Parallel/Exa 免费匿名端点 | 显著降低新用户上手门槛，与 opencode 对齐，预计会合并 |
| [#90331](https://github.com/NousResearch/hermes-agent/pull/90331) | 新增 opt-in `profile_manage` 工具，允许 Agent 在会话中创建 Hermes Profile/Bot | Bot Mode 生态关键闭环，治理化路径，符合 Bot Mode 迭代主题 |
| [#90328](https://github.com/NousResearch/hermes-agent/pull/90328) | 支持为 default bot 配置自定义公开 mention handle | Bot Mode 用户体验小改进 |
| [#90329](https://github.com/NousResearch/hermes-agent/pull/90329) | 启用跨连接（多 gateway）群组创建 | Bot 多连接群聊场景补全 |
| [#82747](https://github.com/NousResearch/hermes-agent/pull/82747) | 新增 `hermes sync-fork` 子命令，支持带本地提交的 fork 更新上游 | 解决 fork 用户无法 `hermes update` 的长期痛点（8/9 提交，仍待合并） |

### 社区

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-20

## 1. 今日速览

过去 24 小时 LiteLLM 项目继续保持极高活跃度：共产生 72 条 Issue 更新（新开/活跃 53 条，关闭 19 条）和 306 条 PR 更新（待合并 184 条，合并/关闭 122 条），并发布了 1 个开发版 Release（v1.99.0-dev.1）。Issue 关闭率约 26%，PR 合并/关闭率约 40%，维护节奏稳定。从PR内容看，项目正围绕 **复杂性路由（Complexity Router）**、**Vertex AI 成本核算修正**、**批量请求限流**、**UI 组件迁移（antd → shadcn）** 等多个方向同步推进，同时持续修复 Anthropic/Claude Code 翻译层和 MCP 相关的问题。社区反馈集中在模型价格表更新、配置项行为异常和代理层语义一致性等方面。

- 活跃度：**极高**（Issue 72 条 / PR 306 条 / Release 1 个）
- 项目健康度：**良好**，PR 合并/关闭比例较高，Bug 修复响应及时


## 2. 版本发布

### v1.99.0-dev.1（开发版）

> 链接：https://github.com/BerriAI/litellm/releases

本次发布为 **开发版（dev build）**，主要更新内容为 **Docker 镜像签名验证说明**：

- 所有 LiteLLM Docker 镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 进行签名
- 每个 Release 使用同一签名密钥（引入于 commit [`0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0)）
- 用户可通过 cosign 验证镜像的完整性和来源

**破坏性变更**：无

**迁移注意事项**：无特殊操作；建议生产环境用户在部署前验证镜像签名。


## 3. 项目进展

今日合并/关闭的重要 PR 集中在以下几方面：

### 路由与成本优化
- **[feat(complexity-router): 使 reasoning override floor 可配置](https://github.com/BerriAI/litellm/pull/37537)**（已关闭）：此前 `reasoning_override_min_score` 被接受但忽略，现通过统一的 accessor 解析 floor，并支持回到无条件 override 的行为（PR #37500 移除的能力）。
- **[fix(vertex_ai): 将区域端点加价纳入成本跟踪](https://github.com/BerriAI/litellm/pull/37543)**（待合并）：Google 自 2026 年 7 月起对非全球区域端点收取 1.1x 费用，此前 LiteLLM 按全球费率跟踪成本，低估支出 10%。该 PR 在成本映射中新增 `regional_...` 字段。
- **[fix(vertex_ai): 仅在首个并行函数调用时回退到占位 thought 签名](https://github.com/BerriAI/litellm/pull/37541)**（待合并）：Gemini 仅对首个并行函数调用签名，LiteLLM 对后续调用伪造跳过校验的占位符，导致回放历史不匹配。修复后占位符仅应用于首个调用。
- **[fix(model_prices): 为 Gemini 3.5/3.6/3.7 Flash 和 3.1 Pro Preview 设置 prompt_cache_min_tokens=4096](https://github.com/BerriAI/litellm/pull/37516)**（已关闭）：此前默认 1,024 tokens 触发 Vertex 硬性 400 错误，现成本表已修正。

### 代理稳定性与可观测性
- **[fix(proxy): 在失败请求的 spend 日志中填充部署归属信息](https://github.com/BerriAI/litellm/pull/37520)**（待合并）：此前失败请求日志缺失 model id、api base、model group，管理员无法定位故障部署。
- **[fix(proxy): 错误响应保留 x-litellm-model-id](https://github.com/BerriAI/litellm/pull/37533)**（待合并）：解决 /v1/embeddings 的 429 等错误响应中缺少模型 ID 的问题。
- **[fix(proxy): secret manager 在解析 os.environ 配置引用前初始化](https://github.com/BerriAI/litellm/pull/37544)**（待合并）：修复拆分镜像中仅由 secret manager 提供的密钥解析为 None 的问题。

### UI 与开发者体验
- **[refactor(ui): 迁移 antd Modal 到共享 shadcn Dialog](https://github.com/BerriAI/litellm/pull/37540)**（待合并）：迁移 52 个文件/65 处调用，是移除 antd 依赖的最大剩余阻塞项。
- **[refactor(ui): 剩余 dashboard 页面全面迁移出 antd](https://github.com/BerriAI/litellm/pull/37524)**（待合并）：Teams、usage、guardrails、auth 等页面全部转换为 shadcn 组件。
- **[docs: 仅运行覆盖改动的测试，完整套件交由 CI](https://github.com/BerriAI/litellm/pull/37528)**（已关闭）：CONTRIBUTING 和 PR 模板改为要求只运行相关测试文件，将本地全量测试耗时从 1 小时+ 中解放出来。

### 模型/厂商适配
- **[fix(anthropic,bedrock): 上报供应商思考 token 而非归类为文本](https://github.com/BerriAI/litellm/pull/35998)**（已关闭）：自适应思考输出此前按文本计费，`thinking_tokens` 被忽略，Converse 对隐藏思考声称 `reasoning_tokens: 0`，签名式思考在 /v1/responses 中消失。现均从供应商响应中读取真实思考 token。

**整体向前推进**：项目在成本核算准确性（Vertex 区域加价、Gemini 缓存下限）、失败请求可观测性（部署归因、model-id 透传）和 UI 现代化（antd 移除）三条线上均有实质性进展，复杂度路由功能增强了可配置性，Anthropic/Bedrock 思考 token 计费问题得到修正。


## 4. 社区热点

### 评论最多的 Issues

| Issue | 评论数 | 主题 | 状态 |
|-------|--------|------|------|
| [#25954 [Feature]](https://github.com/BerriAI/litellm/issues/25954) | 11 | 为 ChatGPT 订阅新增 GPT-5.4 mini/Fast 系列支持 | OPEN（stale） |
| [#12448 [Feature]](https://github.com/BerriAI/litellm/issues/12448) | 10 | 支持 salt_key 轮换（类似 master_key 轮换） | OPEN（stale） |
| [#16623 [Bug]](https://github.com/BerriAI/litellm/issues/16623) | 6 | OpenAPI spec 中 config.yaml 端点消失 | OPEN（stale） |
| [#25234 [Bug]](https://github.com/BerriAI/litellm/issues/25234) | 6 | Request Logs/实时日志滞后（UTC 时区感知问题） | CLOSED |

### 热点分析

1. **GPT-5.4 订阅模型支持**（#25954）：社区用户迫切需要 LiteLLM 跟进最新模型发布，特别是 ChatGPT 订阅渠道的 GPT-5.4 系列。该 Issue 创建于 4 月，至今仍开放且被标记为 stale，说明模型支持节奏可能滞后于用户预期，同时有 2 个 👍。

2. **salt_key 轮换需求**（#12448）：生产环境用户在排查问题开启 debug 日志时，master_key 和 salt_key 可能泄露，因此需要支持轮换机制。该 Issue 有 3 个 👍，且从 2025 年 7 月至今持续活跃，反映企业级安全运维的切实需求。

3. **配置文档断裂**（#16623）：文档指引用户访问 `/#/config.yaml` 查看配置，但该端点已不存在，影响用户排查配置问题。

4. **日志时间戳问题**（#25234）：UI 的 Request Logs 页面比实际时间滞后数小时，涉及 SpendLogs 的时区感知处理。该问题已被标记为 CLOSED，说明已得到修复。


## 5. Bug 与稳定性

### 严重级别：高

- **[Bug: /v1/messages 流式响应中一个 tool_use 块发射两次 content_block_stop，导致工具执行两次](https://github.com/BerriAI/litellm/issues/37273)**（CLOSED）
  影响 Claude Code 类客户端，工具会被重复执行，可能造成生产事故。已关闭，说明已有修复方案。

- **[Bug: MCP auto-execute（require_approval: "never"）劫持客户端工具调用](https://github.com/BerriAI/litellm/issues/37031)**（OPEN）
  当代理配置了 MCP 工具自动执行时，Claude Code 等代理客户端自带的工具（Read/Bash/Edit）会全部报 "Error executing tool"，所有非 MCP 工具不可用。该问题严重破坏 agentic 工作流，需优先处理。

### 严重级别：中

- **[Bug: provider_budget_config 报告 budget_reset_at 约 57 年后（月预算永不重置）](https://github.com/BerriAI/litellm/issues/37261)**（OPEN）
  无 Redis 时，`GET /provider/budgets` 返回的预算重置时间严重错误，导致月预算形同虚设。

- **[Bug: PUT /v1/mcp/server 静默清空 authorization_url/token_url/oauth2_flow](https://github.com/BerriAI/litellm/issues/37258)**（OPEN）
  当 `delegate_auth_to_upstream=true` 时更新 MCP server 配置会丢字段，属于静默数据丢失类问题。

- **[Bug: disable_global_guardrails 配置无效（单复数键名不匹配）](https://github.com/BerriAI/litellm/issues/25487)**（OPEN）
  代码中检查 `disable_global_guardrail`（单数），但所有生产代码写入的是 `disable_global_guardrails`（复数），导致该配置完全失效。该问题已存在约 4 个月，涉及安全相关配置。

- **[Bug: 部署级 TPM 限制在多副本下失效（tpm_limit × N_replica）](https://github.com/BerriAI/litellm/issues/27736)**（CLOSED）
  多副本部署时 TPM 限制变为每副本独立计算，整体限额放大 N 倍。

### 严重级别：低

- **[Bug: Anthropic → Responses API 桥接不报告 cache_read_input_tokens](https://github.com/BerriAI/litellm/issues/36091)**（OPEN）：缓存命中率无法观测。
- **[Bug: translate_tool_choice_to_responses_api 返回对象而非字符串字面量](https://github.com/BerriAI/litellm/issues/32505)**（OPEN）：导致 vLLM 等上游返回 400/422。
- **[Bug: Router.update_settings() 传入 None 时 TypeError](https://github.com/BerriAI/litellm/issues/28126)**（OPEN）：API 容错性问题。
- **[Bug: Vertex AI 区域端点成本低估 10%](https://github.com/BerriAI/litellm/pull/37543)**：已有 fix PR 待合并。

### Bug 修复 PR 汇总

今日有多个 Bug 修复 PR 提交/合并，最值得关注的是：
- [fix(proxy): 填充失败请求的部署归属](https://github.com/BerriAI/litellm/pull/37520)
- [fix(proxy): 批量输入文件快速失败校验](https://github.com/BerriAI/litellm/pull/37527)
- [fix(proxy): 错误响应保留 x-litellm-model-id](https://github.com/BerriAI/litellm/pull/37533)
- [fix(ui_sso): SSO 登录时移除过期团队关系](https://github.com/BerriAI/litellm/pull/37530)


## 6. 功能请求与路线图信号

### 高价值功能请求（评论多、有 👍）

| Issue | 请求内容 | 信号强度 |
|-------|---------|---------|
| [#25954](https://github.com/BerriAI/litellm/issues/25954) | ChatGPT 订阅（chatgpt/）支持 GPT-5.4 mini/Fast 系列 | 高：11 评论、2 👍 |
| [#12448](https://github.com/BerriAI/litellm/issues/12448) | salt_key 轮换机制 | 高：10 评论、3 👍 |
| [#28307](https://github.com/BerriAI/litellm/issues/28307) | 新增 meta-llama/llama-4-scout 到价格表 | 中：3 评论 |
| [#28309](https://github.com/BerriAI/litellm/issues/28309) | 新增 deepseek/deepseek-v4-flash:free 到价格表 | 中：2 评论 |

### 与现有 PR 关联的路线图信号

- **复杂性路由增强**：#37537（reasoning floor 可配置）+ #37534（business 分类 rubric 预设）表明团队在积极迭代 **Complexity Router** 功能，并扩展现有分类场景（从 chat/agentic coding 扩展到 business/sales 领域）。
- **批量请求

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 开源项目动态日报 — 2026-08-20

## 今日速览

过去 24 小时 Temporal 项目保持高强度迭代：23 条 Issue 更新（其中 2 条关闭），82 条 PR 更新（29 条合并/关闭，53 条待合并），未发布新版本。核心开发重心集中在**可观测性增强**（Nexus 日志标签、membership 指标、circuit breaker 状态日志）和**稳定性修复**（事件缓存作用域、调度器时间处理、队列 GC 竞态）。社区侧，MySQL 多主机连接支持已由 issue 落地为 PR（#11659），有望进入下一版本；安全漏洞报告（Go CVE-2026-42507、AWS Inspector 高危扫描）正在等待维护者响应。整体来看，项目处于功能开发与稳定性加固并行的健康状态，但待合并 PR 数量偏高（53 条），合并队列存在一定积压。

---

## 项目进展

**合并/关闭的重要 PR：**

- [#11389 [CLOSED] matching: resume gc after acks that land during an in-flight gc pass](https://github.com/temporalio/temporal/pull/11389) — 修复 GC 传递期间 ack 到达导致的任务 GC 遗漏问题。作者经深入分析后对逻辑进行了文档化和测试验证，未改动核心算法，降低了该场景下 flaky test 的风险。
- [#11373 [CLOSED] edge case fixes for time skipping propagation and fast-forward completion](https://github.com/temporalio/temporal/pull/11373) — 修复两个边界问题：fast-forward 在事务内完成且时间早于 `ms.Now()` 时时间跳过未禁用的场景；以及时间跳跃传播的边界条件处理。

**已关闭的 Issue：**

- [#11600 [CLOSED] Data race in UpdateWithStart: ExecutionState.Status read after workflow lock release](https://github.com/temporalio/temporal/issues/11600) — 锁释放后读取 mutable state 字段的数据竞争问题，已关闭（疑已修复）。
- [#11586 [CLOSED] tdbg dlq commands reject the archival task category (5)](https://github.com/temporalio/temporal/issues/11586) — 归档 DLQ 任务类别无法通过 tdbg 管理的问题，已解决。

**待合并队列中值得关注的重要 PR：**

- [#11660 Scope events cache entries to the shard context instance](https://github.com/temporalio/temporal/pull/11660) — 通过向 `events.EventKey` 添加 `ShardUUID` 修复写入事务因 range CAS 竞争存活时的事件缓存泄漏问题，属数据一致性关键修复。
- [#11659 Support MySQL multi-host and SRV connections](https://github.com/temporalio/temporal/pull/11659) — 实现 MySQL 多主机连接与 DNS SRV 记录支持，直击 issue #10171 的社区诉求。
- [#11462 [Scheduler] V1→V2 migration-eligibility fix and migrated-start ID](https://github.com/temporalio/temporal/pull/11462) — 合并两个 V1 调度器问题修复，统一版本号避免重复部署迁移。

---

## 社区热点

**讨论最活跃的 Issues（按评论数排序）：**

1. [#11146 Membership: emit per-service reachable/available/draining member gauges](https://github.com/temporalio/temporal/issues/11146)（3 评论）— 在 rolling restart 和 gray-failed 主机场景下，运维无法通过指标感知成员服务状态。与 #11108 形成同一方向（membership 可观测性与控制），反映生产环境对集群成员健康可视化的强烈需求。

2. [#11539 DeleteWorkerDeploymentVersion fails permanently when a version summary outlives its version workflow](https://github.com/temporalio/temporal/issues/11539)（3 评论）— Worker Deployment 版本清理永久失败，导致新版本无法注册。用户尝试通过定期删除 drained versions 维持 `matching.maxVersionsInDeployment` 配额，但遭遇持久性故障，影响版本发布流水线。

3. [#10171 MySQL persistence: support multi-host connectAddr and/or SRV-based endpoint discovery](https://github.com/temporalio/temporal/issues/10171)（2 评论）— 用户从 Helm chart 0.73.1 迁移到 1.x 时遭遇 MySQL HA 场景下无 LB/VIP 的困境，请求支持多主机地址或 SRV 发现。此需求已获得 PR [#11659](https://github.com/temporalio/temporal/pull/11659) 实现。

4. [#11534 Fairsim partial counter configuration resets unspecified defaults](https://github.com/temporalio/temporal/issues/11534)（2 评论）— 部分配置覆盖意外重置其他默认值，影响 local development 工具链的使用体验。

**分析：** 今日社区热点集中于生产环境运维痛点——成员状态不可控（#11108/#11146）、版本管理阻塞（#11539）、基础设施部署灵活性（#10171）。这些议题的共同特征是用户在真实生产环境（Kubernetes、多云、无传统 LB 的网络）中遇到的阻碍，维护者已开始通过 PR 回应其中 MySQL 相关诉求。

---

## Bug 与稳定性

**高风险：**

- [#11539 DeleteWorkerDeploymentVersion fails permanently when a version summary outlives its version workflow](https://github.com/temporalio/temporal/issues/11539) — 版本删除永久失败，阻塞新版本注册。尚无针对性 fix PR，但 [#11520 Populate CallbackInfo.outcome](https://github.com/temporalio/temporal/pull/11520) 和 [#11566 Make supported callback kinds configurable](https://github.com/temporalio/temporal/pull/11566) 均与 worker callback 生命周期相关，值得关注。
- [#11402 A lost RegisterWorkerInVersion task permanently disables activity dispatch for a task queue](https://github.com/temporalio/temporal/issues/11402) — 任务丢失将永久禁用队列的活动分发，属持久性故障。无关联 fix PR。
- [#11547 A brief Unavailable blip resets History queue backoff, causing a sustained retry storm](https://github.com/temporalio/temporal/issues/11547) — 短暂的 `Unavailable` 错误会重置队列退避机制，在高负载下引发重试风暴，可能导致集群级联故障。无关联 fix PR。
- [#11188 Race Condition in Queue Pending Task Mitigation](https://github.com/temporalio/temporal/issues/11188) — 待处理任务数超过阈值时 mitigation 逻辑可能触发 fatal crash。无关联 fix PR。

**中风险：**

- [#11569 Nexus: server may send malformed request-timeout header](https://github.com/temporalio/temporal/issues/11569) — 服务器可能发送负值或非法单位的时间头，违反 Nexus 协议语法。无关联 fix PR。
- [#11571 Persistence rate-limit ResourceExhausted is flattened to Unavailable in ProcessOutgoingSearchAttributes](https://github.com/temporalio/temporal/issues/11571) — 错误类型被错误转换，导致重试策略失效。无关联 fix PR。
- [#11230 Client TLS configs do not pick up refreshed root CAs](https://github.com/temporalio/temporal/issues/11230) — 证书轮换后客户端 TLS 配置不刷新，需进程重启。无关联 fix PR。
- [#11429 Healer 在 Kubernetes pod 重启后仍探测旧 pod IP](https://github.com/temporalio/temporal/issues/11429) — 导致网关日志中出现持续访问旧地址的噪音。无关联 fix PR。
- [#11639 ui-server: ListNamespaces/GetClusterInfo return 403 for namespace-scoped admin tokens](https://github.com/temporalio/temporal/issues/11639) — 命名空间级 admin 权限无法加载 Web UI，需要未文档化的 "temporal-system:" 权限。无关联 fix PR。

**低风险 / 性能：**

- [#11594 PostgreSQL visibility v1.14 schema upgrade misses the v1.10–v1.13 rewrite optimization](https://github.com/temporalio/temporal/issues/11594) — 升级时执行了多余的二次 rewrite，增加迁移耗时。无关联 fix PR。
- [#11534 Fairsim partial counter configuration resets unspecified defaults](https://github.com/temporalio/temporal/issues/11534) — 工具配置合并逻辑缺陷。无关联 fix PR。

**已修复：**

- [#11600 Data race in UpdateWithStart](https://github.com/temporalio/temporal/issues/11600)（已关闭）
- [#11586 tdbg dlq archival task category](https://github.com/temporalio/temporal/issues/11586)（已关闭）

---

## 功能请求与路线图信号

**有望进入下一版本（已有对应 PR）：**

- **MySQL 多主机 + SRV 连接支持**（[#10171](https://github.com/temporalio/temporal/issues/10171)）→ PR [#11659](https://github.com/temporal

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*