# OpenClaw 生态日报 2026-08-11

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-10 23:00 UTC

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

**报告日期：** 2026-08-11  
**数据来源：** 各项目 GitHub 社区动态摘要  
**说明：** OpenClaw、OpenHands SDK、Pi 三个项目在本次摘要中未提供动态数据，相关对比基于其余已披露项目展开。

---

## 1. 生态全景

当前个人 AI 助手与自主智能体生态呈现出 **“应用层快速迭代、基础设施层强化治理、稳定性与合规性成为共同瓶颈”** 的态势。Hermes Agent 单日 500 条 PR 更新、LiteLLM 发布 v1.96.0 并处理预算绕过与安全漏洞，说明项目仍处于高强度的功能扩张与修补期；而 Temporal 则聚焦资源泄漏与可靠性整改，代表底层执行引擎正在走向成熟。社区对**预算控制、多租户隔离、数据脱敏、可观测性**的诉求日益强烈，意味着生态正从“可用”迈向“企业级生产可用”。同时，上游模型/平台（xAI、Bedrock、OpenWebUI）的兼容性问题频繁暴露，多源集成适配仍是普遍痛点。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新（新开/活跃 / 关闭） | PR 更新（待合并 / 已合并关闭） | Release | 健康度评估 |
|---|---|---|---|---|
| **Hermes Agent** | 368（331 / 37） | 500（399 / 101） | 无 | 高活跃，但 P1 缺陷积压、合并管线有压力 |
| **LiteLLM** | 64（56 / 8） | 206（153 / 53） | v1.96.0 | 高活跃，需警惕核心计费/安全回归 |
| **Temporal** | 4（2 / 2） | 35（26 / 9） | 无 | 良好，可靠性工程系统性推进 |
| **OpenClaw** | 未提供 | 未提供 | 未提供 | 无法评估 |
| **OpenHands SDK** | 未提供 | 未提供 | 未提供 | 无法评估 |
| **Pi** | 未提供 | 未提供 | 未提供 | 无法评估 |

> Hermes Agent 的 PR 数量显著高于其他项目，但 399 条待合并 PR 也暗示审查/合并吞吐可能成为下一阶段瓶颈。LiteLLM 更新节奏适中，版本迭代较快。Temporal 活动量最低，符合其作为成熟基础设施的稳定演进特征。

---

## 3. OpenClaw 在生态中的定位

本次动态摘要中 **OpenClaw 没有任何数据**，因此无法基于实际社区动态评估其优势、技术路线差异或社区规模。作为“核心参照”项目，它的缺席可能意味着当日无高优先级更新，或数据采集遗漏。

从生态整体推断：若 OpenClaw 定位于个人 AI 助手网关/代理，则需要与 Hermes Agent（桌面端+消息平台集成）形成差异化；若定位于执行层，则需与 Temporal（持久工作流）对标。在缺少可靠数据前，本报告不做进一步猜测。建议补充后续动态后再进行准确定位分析。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目及具体诉求 |
|---|---|
| **资源泄漏与句柄治理** | **Hermes Agent**：SessionDB 描述符泄漏、gateway 句柄治理；**Temporal**：gRPC 连接泄漏、version check 响应体关闭。二者都在主动修复长期运行的资源消耗问题。 |
| **多租户与企业级隔离** | **Hermes Agent**：多租户内存隔离触发架构决策；**LiteLLM**：tag 级限流、per-key prompt caching、共享 key 下 end_user 固定归属问题。均指向生产环境的多租户精细控制需求。 |
| **预算控制与成本可观测** | **LiteLLM**：预算强制执行绕过、流式 usage 严重少计、批量任务成本归属；**Temporal**：匹配服务指标基数无限增长。成本与用量准确性是共同焦点。 |
| **上游模型/平台兼容性** | **LiteLLM**：Bedrock 误报支持 web_search、Z.AI 模型名解析失败；**Hermes Agent**：xAI OAuth 档位限制、Teams devtunnel 协议文档修正。多供应商适配的脆弱性普遍存在。 |
| **安全与合规** | **LiteLLM**：PII 脱敏无效、UI 会话安全漏洞、MCP 日志脱敏；**Hermes Agent**：Honcho 写路径静默写入修复。数据合规正成为硬性要求。 |
| **桌面端稳定性** | **Hermes Agent**：macOS 桌面冻结、GPU 空闲满载、Full Disk Access 被撤销。目前其他项目未直接涉及，但可能预示客户端类智能体助手的普遍短板。 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|---|---|---|---|
| **Hermes Agent** | 个人 AI 助手客户端 + 网关，覆盖桌面 UI、消息平台（Slack/Teams）、多代理交互 | 极客、桌面端用户、企业个人助理场景 | 桌面客户端 + agent 网关 + SessionDB，强调交互与插件生态，面临 Electron 级稳定性问题 |
| **LiteLLM** | 统一的 LLM 代理/网关，提供 100+ provider 接入、预算、限流、日志、UI 管理 | 开发者、平台团队、企业 AI 基础设施运维 | 服务端 proxy（Python），典型企业网关架构，侧重治理与集成，无客户端 |
| **Temporal** | 持久执行工作流引擎，管理长时间运行的分布式任务 | 后端开发、平台工程师、任务编排需求方 | Go 服务端 + gRPC + SQLite/PostgreSQL，核心是可靠性和可恢复性，与 AI 生态通过 Nexus/sdk 结合 |
| **OpenHands SDK** | 未提供 | — | — |
| **Pi** | 未提供 | — | — |

---

## 6. 社区热度与成熟度

- **快速迭代阶段：Hermes Agent、LiteLLM**  
  两者日均 PR 达百条以上（Hermes 500、LiteLLM 206），新功能与修复并进，但伴随较多开放性缺陷。Hermes 的 P1 问题（桌面冻结、overlay 失效）持续 20-30 天无修复，显示快速增长下稳定性欠债；LiteLLM 则出现预算绕过、安全漏洞等生产红线问题，但响应速度较 Hermes 更快。

- **质量巩固阶段：Temporal**  
  日 PR 仅 35 条，但集中在资源泄漏修复、连接复用和 worker-callbacks 新特性上，说明基础功能已稳定，当前以内部可靠性治理和定向扩展为主。

- **数据不足：OpenClaw、OpenHands SDK、Pi**  
  无法判断活跃度与成熟度，需后续数据补充。

---

## 7. 值得关注的趋势信号

1. **智能体应用的“桌面端稳定性”仍是硬伤**  
   Hermes 桌面在 macOS 上 5 条消息即冻结、30 天未修复，且多个 P2 渲染问题堆积。对计划将 AI 助手嵌入桌面的开发者，Electron/客户端生命周期管理需提前投入。

2. **预算控制是企业采纳的“红线”**  
   LiteLLM 预算绕过和流式 usage 少计虽已持续数月，但社区关注度极高（多条 issue 评论 10+）。未来所有面向企业的 AI 基础设施，必须把成本计量做成“硬防火墙”而非事后统计。

3. **多租户隔离成为主流诉求**  
   Hermes 的 `needs-decision` 与 LiteLLM 的 tag 级限流、per-key 缓存表明：单用户原型已不再满足生产需求，租户级资源隔离与配额管理是下一阶段竞争力核心。

4. **上游服务变更未同步，引发集成层连锁问题**  
   xAI OAuth 只放行 Heavy 档位、Bedrock 误报支持 web_search 等事件，凸显依赖单一模型/云厂商的风险。智能体项目需要建立更主动的适配层测试与上游变更监控机制。

5. **AI 辅助开发已进入开源维护日常**  
   Temporal 出现“标准化 Claude review comments”的 PR，说明 AI 代码审查正在融入维护工作流。对开源项目而言，这可能提升审查效率，但也需关注风格统一问题。

6. **可观测性指标的无界增长被忽视**  
   Temporal 的 matching 服务指标基数无限增长、LiteLLM 的 usage 失真，都指向长期运行系统的可观测性成本。设计指标时需考虑基数约束与聚合准确性，否则大规模部署将带来监控系统自身崩溃。

---

**报告结束**  
建议：下一次分析时补充 OpenClaw/OpenHands SDK/Pi 的社区数据，以完善生态全景与定位对比。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-11

---

## 今日速览

过去 24 小时项目活动量处于高位：**368 条 Issues 更新**（新开/活跃 331，关闭 37）与 **500 条 PR 更新**（待合并 399，已合并/关闭 101）表明社区提交与维护者响应均十分积极。值得关注的是，**P1 级 Bug 新增/活跃明显**（桌面冻结、SessionDB 描述符耗尽、TUI overlay 失效等），稳定性问题仍是当前主要矛盾；但大量修复 PR 已同步提交（如句柄泄漏、Slack/Maatrix 消息重放、Honcho 写路径），说明项目正处在快速修补周期。无新版本发布，合并管线存在一定积压（399 条待合并 PR）。

---

## 版本发布

今日无新版本 Release。

---

## 项目进展

今日共 **101 条 PR 被合并/关闭**，体现在以下关键方向上：

**已合并/关闭（可见样本）**

- **docs(teams): correct devtunnel webhook protocol** ([#83464](https://github.com/NousResearch/hermes-agent/pull/83464)) — 修正 Microsoft Teams devtunnel 示例中本地 webhook 的协议描述（HTTP vs HTTPS），避免集成方配置错误。
- **docs(kanban): document workflow configuration preflight** ([#83483](https://github.com/NousResearch/hermes-agent/pull/83483)) — 补充 workflow_configuration 预检、路由优先级与依赖规则的文档。

**新提交的高价值 PR（待合并）**

- **SQLite 描述符泄漏修复** — [#83397](https://github.com/NousResearch/hermes-agent/pull/83397) 与 [#83490](https://github.com/NousResearch/hermes-agent/pull/83490) 从不同角度解决 SessionDB 连接未关闭的问题（前者针对异常路径，后者引入固定四连接租用池替代每线程缓存），直接对应 #75269 等 P1 issue。
- **网关句柄治理** — [#83502](https://github.com/NousResearch/hermes-agent/pull/83502) 关闭 session-search SQLite 句柄、绑定 gateway 数据库/输出句柄，并硬阻断 computer-use 对 Terminal 的变更，降低描述符耗尽风险。
- **Slack 消息重放修复** — [#73450](https://github.com/NousResearch/hermes-agent/pull/73450) 与 [#83501](https://github.com/NousResearch/hermes-agent/pull/83501) 解决 thread 父消息编辑/元数据变更被误判为新输入的问题。
- **Honcho 写路径修复** — [#83500](https://github.com/NousResearch/hermes-agent/pull/83500) 使 `saveMessages: false` 真正生效，并尊重 `writeFrequency`，修复静默写入的合规性风险。
- **Desktop 稳定性** — [#83492](https://github.com/NousResearch/hermes-agent/pull/83492) 修复 malformed grid layout 导致的 RangeError 挂起；[#82942](https://github.com/NousResearch/hermes-agent/pull/82942) 为自动上下文压缩增加护栏；[#80342](https://github.com/NousResearch/hermes-agent/pull/80342) 引入智能轮询与 SWR 缓存。
- **功能扩展** — [#83495](https://github.com/NousResearch/hermes-agent/pull/83495) 为 CompanyIntel 增加持久化执行与 SSE replay；[#83498](https://github.com/NousResearch/hermes-agent/pull/83498) 新增 Camofox 浏览器执行后端。

整体来看，项目正集中精力处理 **文件描述符/句柄泄漏** 与 **平台消息重放** 两类系统性缺陷，同时持续向桌面端与插件生态投入。

---

## 社区热点

**1. xAI OAuth 403 — 标准 SuperGrok 订阅被拒**（[#26847](https://github.com/NousResearch/hermes-agent/issues/26847)，31 评论，已关闭，👍2）

- 用户持有 $30/月的 SuperGrok 订阅，OAuth 流程与 token 存储均正常，但 xAI 后端仅对 Heavy 档位放行，与官方文档宣称的“所有订阅档位可用”相矛盾。该 issue 已关闭，但 31 条评论表明社区对 xAI 集成策略（尤其是文档承诺与实际策略的落差）存在明显不满。这是“集成方后端限制”而非 Hermes 本身缺陷，但暴露了 Hermes 对上游服务变更的响应速度问题。

**2. 桌面端 5 条消息后完全冻结（macOS 27 beta）**（[#63047](https://github.com/NousResearch/hermes-agent/issues/63047)，27 评论，打开，P1）

- 用户报告 Hermes Desktop 在单会话约 5 条消息后 UI 完全冻结，连 Settings 也无法打开，只能强制退出。该 issue 从 7 月 12 日持续至今接近一个月仍为打开状态，且无对应 fix PR，是当前最热的 P1 稳定性问题之一。评论区有大量 macOS 用户补充复现环境，诉求是优先修复而非仅定位到“beta 系统兼容”。

**3. 多租户 Hermes 内存隔离问题**（[#34352](https://github.com/NousResearch/hermes-agent/issues/34352)，20 评论，打开，needs-decision）

- 贡献者 @NimbleCoAI 声称已在生产环境运行数月多租户修复，核心问题是 memory 操作绕过 hook 系统导致租户隔离不可能。该 issue 被维护者标记为 `needs-decision`，且社区对“是否将修复合入核心”讨论激烈——体现了企业级多租户部署的强烈需求与核心架构保守之间的张力。

---

## Bug 与稳定性

按严重程度排列：

**P1 — 高影响 / 需优先关注**

| Issue | 描述 | 状态 |
|---|---|---|
| [#63047](https://github.com/NousResearch/hermes-agent/issues/63047) | macOS 27 beta 桌面端约 5 条消息后完全冻结，Settings 不可用 | 打开 30 天，**无 fix PR** |
| [#69592](https://github.com/NousResearch/hermes-agent/issues/69592) | ambient widget dock 加载后 /sessions 与 /models overlay 不可见，无法恢复会话/切换模型 | 打开 20 天，**无 fix PR** |
| [#75269](https://github.com/NousResearch/hermes-agent/issues/75269) | SessionDB 每个 worker 线程缓存一个 WAL 只读连接，短生命周期线程退出后不释放，耗尽 RLIMIT_NOFILE | 打开 11 天，**已有 fix PR**（[#83397](https://github.com/NousResearch/hermes-agent/pull/83397)、[#83490](https://github.com/NousResearch/hermes-agent/pull/83490)） |

**P2 — 中影响 / 多数已有修复方向**

- **search_files Windows 绝对路径失败**（[#63177](https://github.com/NousResearch/hermes-agent/issues/63177), [#67629](https://github.com/NousResearch/hermes-agent/issues/67629)）：`_bash_safe_path` 将 `D:\` 重写为 `/d/`，native rg 无法识别。已标记为 duplicate 关系，但 #63177 说明其并非 #61915 的回归。暂无 fix PR。
- **Desktop GPU/渲染进程空闲时 100%+ CPU**（[#73082](https://github.com/NousResearch/hermes-agent/issues/73082)）：Electron 渲染器与 GPU helper 在 idle 时满载，macOS 报告为最大耗电应用。暂无 fix PR。
- **桌面更新后 Full Disk Access 被撤销**（[#52010](https://github.com/NousResearch/hermes-agent/issues/52010)）：每次更新需重新授权，与 Accessibility/Microphone 问题独立。打开 48 天，无 fix PR。
- **MoA quiet 模式丢失 tool_calls**（[#58437](https://github.com/NousResearch/hermes-agent/issues/58437)）：已关闭，推测已修复。
- **lifecycle_guard 空字节崩溃**（[#77780](https://github.com/NousResearch/hermes-agent/issues/77780)）：已关闭（17 评论），修复已合入。

**P3 — 低影响 / 平台兼容类**

- **Python 3.14 DaemonThreadPoolExecutor 崩溃**（[#58596](https://github.com/NousResearch/hermes-agent/issues/58596)）— `_initializer` 属性被移除，影响 async delegation、skills hub fan-out。暂无修复。
- **Electron chrome-sandbox 缺少 setuid 导致 .desktop 启动静默失败**（[#51327](https://github.com/NousResearch/hermes-agent/issues/51327)）。

---

## 功能请求与路线图信号

**多租户内存隔离**（[#34352](https://github.com/NousResearch/hermes-agent/issues/34352)）

- 社区已有生产级修复方案，且被标记为 `needs-decision`。若维护者决定吸收，将直接解锁企业级多租户部署场景，是近期最重要的路线图决策点。

**持久会话记忆与跨会话搜索**（[#8457](https://github

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-11

## 1. 今日速览

过去 24 小时项目活跃度极高：共产生 64 条 Issue 更新（新开/活跃 56 条，关闭 8 条）和 206 条 PR 更新（待合并 153 条，已合并/关闭 53 条），并发布了 v1.96.0 新版本。从数据看，项目处于高强度的开发迭代节奏中：一方面有大量新功能 PR 涌入（如 tag 级限流、MCP 日志脱敏、UI 角色权限治理），另一方面也暴露出多个严重稳定性问题——包括预算执行绕过、流式 usage 统计严重失真、UI 会话安全漏洞等。值得关注的是，今日关闭的 PR 中有多项是针对具体 Bug 的修复（Bedrock web_search 误报、SAML SSO 检测等），且与同日新开的 Issue/PR 形成完整的问题发现-修复链路，整体健康度为“高活跃、需警惕核心领域回归”。

## 2. 版本发布

**v1.96.0**（2026-08-10 发布）

本次版本的主要公开信息集中在 Docker 镜像签名的验证说明上。所有 LiteLLM Docker 镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 进行签名，每次发布使用同一把密钥（引入于 [commit `0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0)）。管理员在拉取 v1.96.0 及后续版本镜像时，可通过 cosign 验证镜像完整性与发布方身份。

**⚠️ 注意**：由于官方 Release Notes 未在数据中提供完整更新日志，建议升级前查看 GitHub Releases 页面确认变更详情。结合当前 PR 合并情况推测，本版本可能包含 UI 角色权限修复（如 #36475、#36469）、Arize MCP 追踪崩溃修复（#36453）等近期合并的改动，但需以官方发布说明为准。

## 3. 项目进展

今日关闭/合并的 PR 共 53 条，其中对项目有实质推进的包括：

**核心功能修复**
- [fix(bedrock): reject Anthropic server-side web_search tool with actionable error (#36473)](https://github.com/BerriAI/litellm/pull/36473) — 在调用 Bedrock 前显式拒绝 Anthropic web_search 工具，将原先晦涩的 400 错误替换为包含工具名、模型名和文档链接的可操作错误信息。
- [fix(bedrock): stop claiming native web_search support on Bedrock (#36442)](https://github.com/BerriAI/litellm/pull/36442) — 修正 Bedrock 配置中错误声明支持 web_search 的问题，避免网关错误拦截并向上游透传该工具。
- [fix(proxy): treat SAML as configured in UI SSO detection (#36196)](https://github.com/BerriAI/litellm/pull/36196) — 修复仅配置 SAML（未配置 OAuth）时，UI 登录页不显示 SSO 入口的问题。该 PR 使用 Grok 4.5 辅助发现与修复，已通过验证。
- [fix: replace mutable default arguments with None (#25555)](https://github.com/BerriAI/litellm/pull/25555) — 修复多处可变默认参数（`= []`、`= {}`）潜在的状态共享问题，属 Python 最佳实践修正。

**问题修复闭环**：今日关闭的 Issue 还包括 Bedrock 结构化输出（#35655）、batches.create 回退错误（#35359）、whisper-1 模型调用（#27083）、路由 cooldown 策略（#31876）、日志跟踪 ID 关联（#31873）等，这些均已在近期版本中得到修复。

整体来看，项目今日的推进集中在三个方向：**Bedrock/Anthropic 适配层的正确性修正**、**UI 与权限系统的加固**（多团队、角色可访问性）、**开发体验与代码质量提升**（类型标注、默认参数）。

## 4. 社区热点

今日讨论最热烈的 Issue 集中在以下几项：

- [【Bug】Budget enforcement bypassed in v1.82.3 for key/user max_budget despite spend exceeding max_budget (#26672)](https://github.com/BerriAI/litellm/issues/26672) — 评论 15 条，👍 4 次。用户报告在 v1.82.3 中新部署的代理上，`max_budget` 完全不生效，即使消费已超额仍未触发限制。该问题已持续近 4 个月，社区持续关注，说明**预算强制执行是用户最敏感的能力之一**，绕过后可能直接造成财务损失。

- [【Bug】user_header_mappings does not work with OpenWebUI (#14667)](https://github.com/BerriAI/litellm/issues/14667) — 评论 12 条。OpenWebUI 用户无法正确通过 header 映射关联用户身份，影响用量追踪与多租户场景。该 Issue 已存在近一年，用户“desperately trying”的措辞反映出较高的挫败感。

- [【Bug】Setting "output_parse_pii" has no effect (#14516)](https://github.com/BerriAI/litellm/issues/14516) — 评论 11 条，👍 2 次。配置 PII 脱敏后响应仍以明文返回，涉及合规敏感场景，用户通过 UI、config、请求体三种方式尝试均无效。

- [【性能】fix(rate-limiter): skip post-call Redis writes for keys with no rate limits configured (#31880)](https://github.com/BerriAI/litellm/issues/31880) — 评论 10 条。尽管标题是 “fix”，实际是 GitHub Issue 中描述的性能优化方案：无速率限制的请求仍写入 Redis 计数器，造成大量无意义 I/O。该方案由 @deepanshululla 提出，**体现社区开始关注大规模部署下的性能损耗**。

**热点分析**：当前社区最关注的三大主题为：**预算/计费准确性、第三方生态集成（OpenWebUI）、数据脱敏合规**。这些问题直接关系到生产环境的成本控制、用户可观测性和数据安全，建议维护者优先响应。

## 5. Bug 与稳定性

今日报告的 Bug 按严重程度排列如下：

| 严重程度 | Issue/PR | 描述 | 状态/修复 |
|---------|---------|------|-----------|
| 🔴 严重 | [#26672](https://github.com/BerriAI/litellm/issues/26672) | 预算强制执行绕过，key/user 超支仍可继续调用 | 待修复 (OPEN) |
| 🔴 严重 | [#36114](https://github.com/BerriAI/litellm/issues/36114) | 流式 usage 严重少计（跨多个 provider），根因在流聚合层而非 provider 转换 | 待修复 (OPEN)，作者已定位根因 |
| 🔴 安全 | [#35665](https://github.com/BerriAI/litellm/issues/35665) & [#35664](https://github.com/BerriAI/litellm/issues/35664) | UI 注销/改密后 session 仍有效；UI 的 JWT cookie 包含可复用的 API key 材料 | 待修复 (OPEN)，v1.94.0 受影响 |
| 🟠 高 | [#32218](https://github.com/BerriAI/litellm/issues/32218) | Z.AI 文档宣传的 `glm-5.2[1m]` 模型在代理上返回 Unknown Model | 待修复 (OPEN) |
| 🟠 高 | [#31441](https://github.com/BerriAI/litellm/issues/31441) | 共享虚拟 key 下 `end_user` 被固定为首个请求的 user（v1.87.0 回归） | 待修复 (OPEN) |
| 🟠 高 | [#31880](https://github.com/BerriAI/litellm/issues/31880) | 未配置限流时仍写 Redis 计数器，造成高并发下性能浪费 | 方案已提出，关联 PR 尚未合并 |
| 🟡 中 | [#35775](https://github.com/BerriAI/litellm/issues/35775) | 与 VSCode 原生 Model-Provider (BYOK) 不兼容 | 待修复 (OPEN) |
| 🟡 中 | [#36366](https://github.com/BerriAI/litellm/issues/36366) | Azure Responses 透传空 namespace 描述，导致 Codex CLI 崩溃 | 待修复 (OPEN) |
| 🟡 中 | [#27955](https://github.com/BerriAI/litellm/issues/27955) | 流式中断时 `max_parallel_requests` 计数单调递增，最终拒绝所有请求 | 待修复 (OPEN) |
| 🟢 低 | [#20494](https://github.com/BerriAI/litellm/issues/20494) | 使用相同 secret key 重复生成虚拟 key 未报错 | 待修复 (OPEN) |

**重点关注**：预算绕过（#26672）和流式 usage 少计（#36114）直接影响计费可信度，是生产环境的“红线问题”。安全类问题（#35665/#35664）涉及管理端凭证泄露风险，建议提高处理优先级。

## 6. 功能请求与路线图信号

今日提交的新 PR 释放了明确的功能规划信号：

- [feat(rate-limiting): tag-scoped token/request/dollar/concurrency rate limits (#36459)](https://github.com/BerriAI/litellm/pull/36459) — 新增按任意 tag 维度（非 key）进行令牌/请求/金额/并发限流，支持滚动窗口。**这是对用户在多租户场景下精细化限流诉求的积极回应，可能进入下一版本。**

- [feat(proxy): per-key prompt caching toggle via enable_prompt_caching (#36466)](https://github.com/BerriAI/litellm/pull/36466) — 将 prompt caching 从全局开关细化为单 key 可控，避免“一刀切”策略干扰特定客户。

- [feat(proxy): proactive model deprecation alerts and /model/deprecations endpoint (#26900)](https://github.com/BerriAI/litellm/pull/26900) — 提前暴露模型弃用日期，帮助运维人员在 provider 下线前完成迁移，属于主动运维能力的补强。

- [fix(batches): attribute Anthropic passthrough batch cost to the creating key, team and tags (#36468)](https://github.com/BerriAI/litellm/pull/36468) — 修复批量任务的成本归属缺失，确保 key 预算和 tag 消耗被正确统计。

- [fix(redaction): redact MCP tool arguments and results (#36474)](https://github.com/BerriAI/litellm/pull/36474) — 对 MCP 工具调用参数与结果进行脱敏，补足日志安全盲区。

**路线图信号**：上述 PR 覆盖了**配额精细化、缓存策略个性化、日志安全、成本可归因性**四大方向，加上此前社区反复提出的 [Rust pip binary (#31261)](https://github.com/BerriAI/litellm/issues/31261) 计划，可以看出项目正逐步从“功能覆盖”转向“企业级精细治理”。

## 7. 用户反馈摘要

从今日活跃的 Issue 评论中，可以提炼出以下真实用户痛点：

- **预算失控焦虑**（#26672）：一位用户在 v1.82.3 上发现预算不生效后，持续追问；评论中有其他用户表示遇到类似问题。**核心诉求是“预算必须作为硬性防火墙”**，而非事后账单统计。

- **集成生态的挫败感**（#14667）：OpenWebUI 是自托管用户广泛使用的聊天前端，header 映射失效导致 per-user 用量无法拆分。用户在数月等待后仍未获解决，已在评论中表达失望情绪。

- **合规压力**（#14516）：PII 脱敏无效涉及企业使用 LiteLLM 的合规底线，用户同时尝试三种配置方式（UI、config、请求体）均失败，说明文档与实现可能存在偏差。

- **日志噪音影响排障**（#17235）：用户希望至少能关闭 healthcheck 日志，只保留 ERROR 级别输出，当前 `LITELLM_LOG=ERROR` 未生效。这在高 QPS 场景下增加了日志存储成本与排障难度。

- **多副本部署的重复副作用**（#14809）：K8s 多副本下，Slack 告

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-11

> 数据来源：github.com/temporalio/temporal | 统计窗口：2026-08-10 ~ 2026-08-11

---

## 1. 今日速览

过去 24 小时 Temporal 仓库保持**高活跃度**：共 35 条 PR 更新（26 条待合并、9 条已合并/关闭），4 条 Issue 更新（2 条新开/活跃、2 条关闭），无新版本发布。当前开发重心明显集中在 **reliability-2026 可靠性整治**（gRPC/SDK 资源泄漏修复、replication 流健壮性）与 **worker-callbacks 新特性**两条主线上。两个困扰用户数月的 Bug（#10145 PostgreSQL 索引膨胀、#11289 gRPC 连接泄漏）均于今日关闭，其中 #11289 已由对应修复 PR #11296 合入。整体项目健康度良好，社区反馈的稳定性问题正在被系统性消化。

---

## 2. 版本发布

无新版本发布（过去 24 小时 Releases 为 0）。

---

## 3. 项目进展

今日关闭的 PR 多属于可靠性工程范畴，核心进展如下：

- **【已合并】前端 gRPC 连接缓存落地（#11296）** — 由 @RajeshRajendiran 提交，`RPCFactory.CreateLocalFrontendGRPCConnection` 与 `CreateRemoteFrontendGRPCConnection` 改为基于 `sync.OnceValue` 缓存连接，彻底修复 #11289 中每次 RPC 调用都新建 `grpc.ClientConn` 导致的 goroutine/内存泄漏问题。这是对长期运营集群的重要稳定性改进。
  https://github.com/temporalio/temporal/pull/11296

- **【已合并】version check 响应体全部路径关闭（#11437）** — @prathyushpv 修复了 `versioninfo.Caller.Call` 中 `defer` 位于状态码检查之下、导致非 200 响应泄漏 body 的问题。该泄漏此前会造成 goleak 测试报错。
  https://github.com/temporalio/temporal/pull/11437

- **【已合并】混合脑开发服务器启用 standalone activities（#11457）** — @fretz12 在 mixed-brain 测试的 release server 上启用 `activity.enableStandalone` 动态配置，避免新旧服务器行为不一致导致吞吐测试（`throughput_stress`）发送 standalone activity 调用失败。
  https://github.com/temporalio/temporal/pull/11457

- **【已关闭，未合并】资源泄漏清理探索（#11309）** — @stephanos 的「Do not merge」清理 PR 今日关闭，其内容（关闭 frontend gRPC 连接、SDK worker 停止、取消 version-check HTTP 请求等）已被拆分为 #11438、#11436 等更细粒度的 PR 继续推进，说明团队正在有步骤地消化关闭路径上的资源泄漏问题。
  https://github.com/temporalio/temporal/pull/11309

综合来看，项目今日在「**关闭路径资源释放**」和「**连接复用**」两个方向上有实质代码落地，多个长期存在的泄漏隐患得到修复。

---

## 4. 社区热点

- **PostgreSQL 索引膨胀讨论（#10145，7 条评论，2 👍，已关闭）** — 这是过去 24 小时讨论最密集的 Issue。用户 @oznu 报告在每小时数十万工作流的高吞吐场景下，PG 数据库体积无视 retention period 持续膨胀，表本身仅 46MB 而整体库远大于此。该 Issue 自 5 月创建、历时 3 个月后于今日关闭，虽然关闭原因未标注，但引发了社区对 Temporal 默认 PG schema 在高写入下索引维护策略的广泛讨论。
  https://github.com/temporalio/temporal/issues/10145

- **Matching 服务指标基数无限增长（#9945，3 条评论）** — 用户 @Sanil2108 指出 matching 服务的 Prometheus 指标基数未被 `PhysicalTaskQueueManager` 卸载/空闲队列回收所约束，otel gauges 导致基数无界增长。该 Issue 已开放近 4 个月，反映运营大规模集群的用户对可观测性成本的真实担忧。
  https://github.com/temporalio/temporal/issues/9945

- **PR #11461 "Standardize Claude review comments"** — 一条略显特殊的 PR，由 @stephanos 提交，内容为标准化 AI 代码审查（Claude）的评论格式，表明 Temporal 维护团队已将 AI 辅助审查纳入日常工作流，属于开发流程层面的有趣信号。
  https://github.com/temporalio/temporal/pull/11461

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue/PR | 状态 | 说明 |
|---|---|---|---|
| **高** | #11460 — SDK 客户端在集群关闭时未被正确释放 | OPEN（0 评论） | 新报告：`sdk.clientFactory.Close` 释放派生客户端先于共享系统客户端，导致关闭路径上 gRPC 连接悬挂。已有关联 PR #11438/#11436 正在处理同一批资源释放逻辑。 |
| **中高** | #9945 — Matching 服务 Prometheus 指标基数无界增长 | OPEN（3 评论） | otel gauges 未随任务队列卸载而回收，长期运行可能导致监控系统内存/存储压力。暂无对应 fix PR。 |
| **中** | #11289 — 前端 SearchAttributes/RemoteCluster 处理器每次调用泄漏 grpc.ClientConn | **已关闭** | ✅ 已由 #11296 修复（连接缓存 + 复用）。 |
| **中** | #10145 — PostgreSQL 索引膨胀 | **已关闭** | 行为确认存在，但关闭原因不明确（可能转由文档或配置指引处理）。 |
| **低** | #11437 — version check 响应体泄漏 | **已合并** | ✅ 已修复。 |

此外，今日活跃的可靠性修复 PR 还包括：
- **#11438** — `RPCFactory` 持有并关闭其拨号的 gRPC 连接；`CreateLocalFrontendGRPCConnection` 改为单例记忆化连接（OPEN）
  https://github.com/temporalio/temporal/pull/11438
- **#11436** — 停止 worker service 启动的 SDK workers 与 clients（parentclosepolicy、scanner、batch activity）（OPEN）
  https://github.com/temporalio/temporal/pull/11436

---

## 6. 功能请求与路线图信号

- **Worker 变体回调（Worker-variant callbacks）**：今日两条相关 PR（#11456 支持 worker-variant callbacks、#11380 识别新的 `commonpb` Worker callback 变体）活跃更新。该功能允许 CHASM 回调直接调用同一 namespace 内的 Nexus worker，而非仅发送 HTTP POST 到外部端点。这是 **Nexus 生态向 worker 内建回调扩展**的重要信号，可能进入下一版本。
  https://github.com/temporalio/temporal/pull/11456
  https://github.com/temporalio/temporal/pull/11380

- **SQLite 数据库所有权租约（#11458）**：@stephanos 新增 SQL plugin 的可选数据库租约（lease）能力，支持 wrapper/lease 计数归零时关闭并移除 SQLite 池条目。这为**嵌入式 SQLite 模式的多进程/生命周期管理**铺路，可能服务于本地开发或边缘部署场景。
  https://github.com/temporalio/temporal/pull/11458

- **SDK 认证 Token 注入（#10721）**：为 `SdkClientFactoryProvider` 增加可选 `auth.TokenProvider` 支持，使集群可使用动态 token 认证。该

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*