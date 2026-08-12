# OpenClaw 生态日报 2026-08-13

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-12 23:05 UTC

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

# 个人 AI 智能体开源生态横向对比分析报告

**日期：2026-08-13**


## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态正处于 **“基础能力补课 + 生态化扩展”** 双线并进的阶段。从今日各项目动态来看，工程化能力的巩固（并发回归修复、配置管理、安全漏洞响应）仍是各项目投入最多的方向，而可观测性、成本治理与可扩展插件体系正在成为新一代智能体平台的竞争焦点。与此同时，社区对企业级部署场景（私有技能、资源复用、安全合规）的诉求显著增强，推动项目从“能跑通 demo”向“能在企业环境落地”演进。整体判断：生态已越过原型期，进入工程成熟度与平台化能力的角力阶段。


## 2. 各项目活跃度对比

| 项目 | Issues（24h） | PRs（24h） | Release | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 无数据 | 无数据 | 无数据 | 数据缺失，无法评估 |
| **Hermes Agent** | 无数据 | 无数据 | 无数据 | 数据缺失，无法评估 |
| **OpenHands SDK** | 9（新开/活跃 4，关闭 5） | 30（待合并 20，合并/关闭 10） | **v1.42.1** | ★★★★★ 优秀：并发回归 24h 内修复并发布，bug 上报到修复 PR 当天即开，发布纪律极佳 |
| **LiteLLM** | 73（新开/活跃 54，关闭 19） | 273（待合并 161，合并/关闭 112） | 无 | ★★★★☆ 健康：合并率约 41%，推进节奏好；但 stale 积压较多，高影响 bug 无 fix PR 的情况值得关注 |
| **Pi** | 无数据 | 无数据 | 无数据 | 数据缺失，无法评估 |
| **Temporal** | 3（新开，0 关闭） | 62（待合并 44，合并/关闭 18） | 无 | ★★★★☆ 稳健：PR 栈推进有序，但今日 main 分支合并少，2 条高危安全漏洞待响应拉低评分 |

> 注：OpenClaw、Hermes Agent、Pi 三个项目本期无社区动态数据，不纳入量化对比，仅在定性层面讨论。


## 3. OpenClaw 在生态中的定位

> ⚠️ **数据说明**：OpenClaw 本期摘要为空，以下分析基于生态逻辑推断，非当日数据支撑。

若 OpenClaw 作为“核心参照”项目确实承载个人 AI 助手入口的角色，其生态定位可从两个维度理解：

- **与 OpenHands SDK 对比**：OpenHands 走的是“开发者优先”路线——提供 SDK、插件 manifest、API 契约，让开发者构建自己的 agent；如果 OpenClaw 的定位是“终端用户直接使用的个人 AI 助手”，则两者形成“最终产品 vs 开发框架”的互补而非直接竞争。核心差异化将是**开箱即用的体验完整度**与**底层可编程性的深度**之争。

- **与 LiteLLM 对比**：LiteLLM 位于智能体技术栈的更底层——模型路由、网关、成本控制。如果 OpenClaw 定位为个人助手本体，LiteLLM 更像是其可选的模型基础设施层。两者可以共存，但 OpenClaw 若自建模型路由能力则存在功能重叠的可能。

- **社区规模推断**：考虑到 OpenHands 单日 30 条 PR、LiteLLM 单日 273 条 PR 更新量级，一个健康的一线开源 AI 助手项目通常应有至少两位数日 PR 活跃度。OpenClaw 若活跃度显著低于此水平，则其“核心参照”地位可能更多来自产品定义或社区影响力，而非代码迭代速度。


## 4. 共同关注的技术方向

**① 配置管理的可靠性（LiteLLM + Temporal）**
- LiteLLM [#12875](https://github.com/BerriAI/litellm/issues/12875)：DB 中旧配置静默覆盖新部署配置，导致变更不生效
- Temporal [#2341](https://github.com/temporalio/temporal/issues/2341)：配置加载缺少严格校验，错误 key 无提示，部署排障耗时一整天
- **共同诉求**：配置系统需要有明确的优先级规则、严格的校验机制与可诊断的错误信息

**② 安全漏洞的快速响应（OpenHands + Temporal）**
- OpenHands：git remote URL 中令牌泄露的安全修复当日合并（[#4175](https://github.com/OpenHands/software-agent-sdk/pull/4175)）
- Temporal：同日上报 2 条高危安全漏洞（Go 工具链 CVE-2026-42507、容器镜像高危/严重漏洞）
- **共同信号**：安全扫描工具正在成为社区发现漏洞的主流渠道，项目维护者的响应速度将直接影响企业用户的信任度

**③ 成本治理与计费准确性（OpenHands + LiteLLM）**
- OpenHands [#2044](https://github.com/OpenHands/software-agent-sdk/issues/2044)：希望 per-skill 覆盖 LLM 模型配置，简单任务不强行走昂贵模型
- LiteLLM [#36192](https://github.com/BerriAI/litellm/issues/36192)：Azure 模型价格映射错误，直接影响成本报表准确性
- **共同信号**：随着 agent 从 demo 走向生产，成本已从“无关紧要”变为“核心关切”，精细化的成本分配与准确的计量是刚需

**④ 企业级私有化部署（OpenHands + LiteLLM）**
- OpenHands [#4476](https://github.com/OpenHands/software-agent-sdk/pull/4476)：企业临时沙箱场景的持久化目录支持
- LiteLLM [#36676](https://github.com/BerriAI/litellm/pull/36676)：Terraform 模块支持复用现有 AWS 资源，降低锁定账户部署门槛
- **共同信号**：两者不约而同地在为企业环境中的部署灵活性与资源复用提供支持

**⑤ 扩展能力的生态化（OpenHands + LiteLLM）**
- OpenHands：Agent Plugins manifest loader 落地（[#4474](https://github.com/OpenHands/software-agent-sdk/pull/4474)）
- LiteLLM：Skills 自服务化提交 + 管理员审核机制（[#36677](https://github.com/BerriAI/litellm/pull/36677)），私有技能添加认证（[#26071](https://github.com/BerriAI/litellm/issues/26071)，👍 13 为当日最高热度）
- **共同信号**：插件/技能体系正在从“官方维护”走向“社区自服务 + 审核治理”的模式


## 5. 差异化定位分析

| 维度 | **OpenHands SDK** | **LiteLLM** | **Temporal** |
|---|---|---|---|
| **功能侧重** | 软件 agent 开发框架（SDK + 工具链） | LLM 网关/代理（路由、计费、可观测性） | 分布式工作流编排引擎 |
| **目标用户** | 构建定制化 agent 的开发者 | 管理多模型接入的平台/ infra 团队 | 需要可靠任务编排的后端工程师 |
| **技术架构** | Agent 运行时 + 插件系统 + REST API | 代理层（Proxy）+ 管理 UI + 多 Provider 适配 | 持久化工作流引擎 + 测试运行器 + Worker Callbacks |
| **当前阶段** | 快速迭代期（日 PR 30 条） | 高强度迭代期（日 PR 273 条） | 基础重构与新功能并行期 |
| **核心挑战** | 在灵活性与稳定性之间平衡（并发回归就是教训） | 规模化管理：大量 Provider 适配 + 配置/计费复杂度 | 安全性响应与长期技术债（4 年未关的 config 严格模式诉求） |
| **生态角色** | agent 应用层的“乐高积木” | 模型与 agent 之间的“路由器/收银台” | agent 后端的“可靠性底座” |


## 6. 社区热度与成熟度分层

**第一梯队：高强度迭代层（日 PR > 100）**
- **LiteLLM**：日 PR 更新 273 条，新开/活跃 Issue 54 条。正处于功能快速扩张期，但合并率 41% 与 stale 积压表明社区贡献量大、维护者筛选负担也在加重。属于“跑得快、也要留意脚下”的阶段。

**第二梯队：稳健推进层（日 PR 30–100）**
- **OpenHands SDK**：日 PR 30 条，迭代节奏可控且质量高（bug 当日修复、patch 当日发布）。项目处于“功能扩展 + 质量巩固”的均衡状态，工程纪律优秀。
- **Temporal**：日 PR 62 条但 main 分支合并少，核心贡献集中在少数维护者的 PR 栈上。属于深度重构期的典型特征——表面活跃度高，但面向用户的可见进展相对滞后。

**第三梯队：数据缺失层**
- **OpenClaw / Hermes Agent / Pi**：本期无社区动态数据。需要连续观察才能判断它们是处于静默期还是维护降速。


## 7. 值得关注的趋势信号

**① 安全合规已成为开源 AI 项目的“入场券”而非“加分项”**
Temporal 单日收到 2 条安全扫描上报（CVE、AWS Inspector），OpenHands 修复了 git 令牌泄露问题。对 AI 智能体开发者而言：**在功能规划中预留安全响应通道**（安全 PR 优先合并、定期依赖扫描、容器镜像基线维护）应是默认配置，而非事后补救。

**② 精细成本治理是 agent 规模化的前提**
从 OpenHands 的 per-skill 模型覆盖到 LiteLLM 的 Azure 计价修正，社区在用脚投票：**当 agent 从玩具走向生产力工具，每个 token 的成本都必须可解释、可分配、可控制**。智能体开发者应尽早将成本计量与路由策略纳入架构设计，而非事后打补丁。

**③ 模型配置的“接口化”成为分层趋势**
LiteLLM 在模型路由层抽象配置，OpenHands 在 skill 层抽象模型选择，Temporal 在配置加载层强调校验——三层同时出现对“配置”的重新思考。这暗示智能体技术栈正在固化出清晰的**分层契约**：模型层、Agent 逻辑层、工作流编排层各自管理自己的配置域，减少跨层耦合。

**④ 插件生态正在从“官方应用商店”走向“社区自服务 + 治理”**
LiteLLM 的 Skills 自服务提交 + 管理员审核 PR、OpenHands 的 Agent Plugins manifest loader，共同指向一个趋势：**平台的价值越来越取决于第三方扩展的丰富度，而治理机制（manifest、审核流、版本管理）是扩展生态能否健康生长的关键基础设施**。

**⑤ 流式交互的稳定性是尚未被充分解决的问题**
LiteLLM 的 [#27955](https://github.com/BerriAI/litellm/issues/27955)（流式请求取消后限流计数泄漏导致全局限流）暴露了一个深层次问题——流式请求的生命周期管理在代理层仍未完全成熟。随着 streaming agent 交互成为主流，这类“边角问题”将越来越多地成为生产环境事故的根源。

---

*本报告基于 2026-08-13 GitHub 公开数据生成，部分项目数据缺失，结论以现有数据为限。*

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报

**日期：2026-08-13 | 数据窗口：过去 24 小时**

---

## 1. 今日速览

OpenHands SDK 过去 24 小时保持高强度迭代：共更新 9 条 Issue（新开/活跃 4 条，关闭 5 条）和 30 条 PR（待合并 20 条，已合并/关闭 10 条），并正式发布 **v1.42.1**。本日核心看点是**并发回归的快速修复与发布**：此前 LLM 调用被全局配置串行化的问题（#4380 / #4473）已在 v1.42.1 中修复并确认并行恢复；同时两个新上报的 bug（git 前缀重复、str_replace 上下文窗口偏移）均已由社区开发者第一时间提交修复 PR，响应速度极快。版本发布与插件体系（Agent Plugins manifest loader）的落地标志着 SDK 在稳定性和架构扩展上双线推进，整体项目健康度**优秀**。

---

## 2. 版本发布：v1.42.1

🔗 [Release v1.42.1](https://github.com/OpenHands/software-agent-sdk/pull/4475)（发布 PR #4475）

**更新内容：**

| 变更 | 说明 | 关联 PR |
|---|---|---|
| 🐛 fix(goal) | 修复 goal 循环在 STUCK 运行中被错误标记为 "interrupted" 而中止的问题，不再需要手动点击 resume | [#4381](https://github.com/OpenHands/software-agent-sdk/pull/4381) |
| ✨ feat(hooks) | 实现基于 LLM 的 HookType.PROMPT 评估机制 | [#4160](https://github.com/OpenHands/software-agent-sdk/pull/4160) |
| 🐛 fix(llm) | 停止通过全局配置序列化 LLM 调用，恢复并行执行能力 | [#4473](https://github.com/OpenHands/software-agent-sdk/pull/4473) |

**破坏性变更：** 无。

**迁移注意：**
- HookType.PROMPT 为新增能力，现有 hook 配置不受影响。
- LLM 串行化修复改变了调用执行模型（恢复并行），依赖串行顺序的极端场景需关注。

---

## 3. 项目进展

**已合并 / 关闭的关键 PR（共 10 条），按影响面排序：**

- 🔧 **fix(llm): stop serializing calls through global config** — [#4473](https://github.com/OpenHands/software-agent-sdk/pull/4473)（@neubig）  
  修复了导致 agent server 在 LLM 调用较慢时退化为单线程的**严重并发回归**，作者确认修复后调用恢复并行。直接关闭 Issue #4380 并触发新 Issue #4477（补并发负载测试）。

- 🔌 **feat(plugin): add Agent Plugins manifest loader** — [#4474](https://github.com/OpenHands/software-agent-sdk/pull/4474)（@VascoSch92）  
  实现根级 `plugin.json` 解析器（closed schema，永不走网络获取），关闭 Issue #4450，是 Agent Plugins 体系（#4405）的关键基础组件。

- 🛡️ **fix(security): redact git remote URL credentials** — [#4175](https://github.com/OpenHands/software-agent-sdk/pull/4175)（@Solaris-star）  
  安全修复：`git remote -v` 输出中会泄露 `ghu_...@github.com` 形式的用户令牌，现已脱敏（对应 OpenHands#15338）。

- ⚙️ **fix: PATCH /api/settings loads the profile's LLM when setting active_profile** — [#4319](https://github.com/OpenHands/software-agent-sdk/pull/4319)（@emmanuel-adu）  
  修复切换 active_profile 时 LLM 配置未正确加载的问题。

- 📦 **Release v1.42.1** — [#4475](https://github.com/OpenHands/software-agent-sdk/pull/4475)（@all-hands-bot）

- 🔍 **fix(security-scan): improve release security scan comment** — [#4397](https://github.com/OpenHands/software-agent-sdk/pull/4397)

**同步关闭的 Issue（5 条）：** #2755（HookType.PROMPT 实现）、#3790（fork PR 的 REST API 契约摘要）、#3799（Laminar 追踪元数据）、#4450（插件 manifest loader）、#4380（goal loop 中断 bug）。

> **整体推进评估：** 一个 patch 版本发布 + 并发回归修复 + 插件架构落地 + 2 项安全修复合并，项目净前进约 2-3 个里程碑点；v1.42.1 的快速发布（从修复到发版不足 24 小时）体现了良好的发布纪律。

---

## 4. 社区热点

**🔥 最长寿讨论：LLM Profile per-skill override（4 评论）**  
[#2044: feat(skills): LLM Profile override per skill](https://github.com/OpenHands/software-agent-sdk/issues/2044)  
已存在 6 个月（2026-02-13 创建）并被打上 Stale 标签，但今日仍有更新。诉求：当前所有 skill 共用父 agent 的模型配置，简单任务也被迫使用昂贵/慢速模型，希望在 skill frontmatter 中增加 `model`/`profile` 字段。这反映了**成本治理**的普遍需求，在 v1.42.1 引入 LLM 并行修复后，按 skill 分配模型的呼声可能进一步上升。

**📌 高关注新 bug 讨论（各 1 条评论，均速配修复 PR）：**
- [#4468](https://github.com/OpenHands/software-agent-sdk/issues/4468) — `normalize_tool_call` 重复添加 git 前缀（priority: medium，release-note-required）→ 修复 PR [#4471](https://github.com/OpenHands/software-agent-sdk/pull/4471) 当天即开
- [#4469](https://github.com/OpenHands/software-agent-sdk/issues/4469) — `FileEditor.str_replace` 验证片段少了一行前导上下文（priority: low）→ 修复 PR [#4472](https://github.com/OpenHands/software-agent-sdk/pull/4472)

**🧵 PR 侧讨论焦点：**  
- [#4476](https://github.com/OpenHands/software-agent-sdk/pull/4476)（OH_PERSISTENCE_DIR 支持）HUMAN 部分明确请求 review 关注企业临时沙箱场景
- [#4473](https://github.com/OpenHands/software-agent-sdk/pull/4473) 附带了并行修复前后的实测截图，社区确认有效

---

## 5. Bug 与稳定性

按严重程度排序：

| 严重度 | Bug | 状态 | 修复 PR |
|---|---|---|---|
|

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目日报 — 2026-08-13

## 1. 今日速览

过去24小时 LiteLLM 项目保持高强度迭代：共产生 73 条 Issue 更新（新开/活跃 54 条，已关闭 19 条）和 273 条 PR 更新（待合并 161 条，已合并/关闭 112 条），合并/关闭率约 41%，项目推进节奏健康。今日无新版本发布，当前开发重心集中在代理稳定性修复、可观测性（OpenTelemetry/Langfuse）完善、UI 组件重构及新模型/Provider 适配四个方向。长期遗留问题中仍有不少标记为 `stale` 的 Bug 未获处理，但核心路由与计费问题修复活跃。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

过去 24 小时合并/关闭的 112 个 PR 中，以下已合入的变更值得关注：

- **UI 层改进**：[#36495](https://github.com/BerriAI/litellm/pull/36495) 在 Admin UI 中增加 Redis 未配置警告横幅，帮助多 worker 部署场景下及时发现问题；[#28518](https://github.com/BerriAI/litellm/pull/28518) 新增管理员可配置的仪表盘横幅，支持发布状态、消息文本和提示样式。
- **基础设施/部署**：[#36676](https://github.com/BerriAI/litellm/pull/36676) 让 Terraform AWS 模块的 VPC、Aurora、Redis 变为可选，支持复用现有资源，降低在锁定账户中的部署门槛。
- **Bug 修复**：Issue [#12875](https://github.com/BerriAI/litellm/issues/12875)（LiteLLM_Config 表覆盖新部署配置）与 [#33168](https://github.com/BerriAI/litellm/issues/33168)（DB 存储的 auto-router/complexity-router 模型从 `/v1/models` 消失）均已在今日关闭，此前阻塞用户的核心问题得到解决。

综合来看，项目在 UI 可用性、部署灵活性和配置管理三方面均有实质推进。

## 4. 社区热点

- [**#26071**](https://github.com/BerriAI/litellm/issues/26071)：私有仓库技能添加与认证支持（8 评论，👍 13）— 用户希望 LiteLLM 支持通过 SSH 密钥（本地）或 GitHub Access Token（远程/私有）添加 Claude skills 及类似 AI 技能插件。该需求热度最高，反映出企业用户对私有 AI 技能集成的强烈诉求。
- [**#12875**](https://github.com/BerriAI/litellm/issues/12875)：LiteLLM_Config 表覆盖新部署配置（11 评论，已关闭）— 用户发现 `_update_config_fields` 从数据库表拉取旧值覆盖新配置，引发社区广泛讨论，现已关闭，表明已修复或提供解决方案。
- [**#36192**](https://github.com/BerriAI/litellm/issues/36192)：Azure GPT-5.6 terra/luna 成本映射错误（5 评论）— Azure 未跟随 OpenAI 的降价，但 LiteLLM 的价格表错误地将 OpenAI 直连价格套用到 Azure 模型上，直接影响用户计费准确性。
- [**#24513**](https://github.com/BerriAI/litellm/issues/24513)：Usage AI Chat 在代理别名/模型组场景下失败（5 评论）— 使用 `mylitellmmodel` 这类代理模型组名称时，Usage 看板的 Ask AI 功能不可用，暴露了 UI 层对代理路由模型的适配缺口。

## 5. Bug 与稳定性

**严重（计费/可用性）**：
- [#36192](https://github.com/BerriAI/litellm/issues/36192)：Azure GPT-5.6 terra/luna 价格行错误地沿用 OpenAI 直连价格，Azure 未经历 7 月 30 日的降价。影响成本核算准确性。**无对应 fix PR**。
- [#27955](https://github.com/BerriAI/litellm/issues/27955)：`max_parallel_requests` 计数在客户端取消流式 `/v1/messages` 请求时单调递增，最终导致所有请求被限流。**无对应 fix PR**。

**中等（功能异常）**：
- [#31553](https://github.com/BerriAI/litellm/issues/31553)：工具调用后出现意外空白 assistant 消息，影响 Deepseek 后端对话体验。**无对应 fix PR**。
- [#36566](https://github.com/BerriAI/litellm/issues/36566)：`litellm_content_filter` 评估结果未出现在请求日志和 Guardrails Monitor 中。**无对应 fix PR**。
- [#36524](https://github.com/BerriAI/litellm/issues/36524)：pre_call guardrail 在 Anthropic `/v1/messages` 路由上将 `document` 内容块错误转换为 `image`，导致 PDF 请求 400。**无对应 fix PR**。

**已修复/关闭**：
- [#36553](https://github.com/BerriAI/litellm/issues/36553)：`_should_start_new_content_block` 在空 `choices` 分块上崩溃，已关闭。
- [#36526](https://github.com/BerriAI/litellm/issues/36526)：litellm 1.96.1 缺少 Python 3.13 wheel/sdist，已关闭。
- [#27105](https://github.com/BerriAI/litellm/issues/27105)：mcp_semantic_tool_filter 生成无效 OpenAI 工具 schema，已关闭。
- [#27173](https://github.com/BerriAI/litellm/issues/27173)：Helm chart 1.1.0 standalone DB secret 漂移导致 CrashLoop，已关闭。

## 6. 功能请求与路线图信号

- **私有化技能（Skills）生态**：[#26071](https://github.com/BerriAI/litellm/issues/26071) 要求支持私有仓库技能的认证添加（👍 13，最高热度）；而 PR [#36677](https://github.com/BerriAI/litellm/pull/36677)（feat(skills): self-service skill submission with admin review）已经提出非管理员可提交技能、管理员审核后发布的功能，两者结合表明 Skills 正在从管理员特权向自服务化演进。
- **OpenRouter 动态成本对账**：[#27588](https://github.com/BerriAI/litellm/issues/27588) 提出支持 Service Tiers 和实时价格同步，属于计费精确性增强，目前无对应 PR。
- **新 Provider 接入**：[#36624](https://github.com/BerriAI/litellm/pull/36624) 新增 Gandr TTS provider；[#36704](https://github.com/BerriAI/litellm/pull/36704) 为 Parallel AI 增加 chat + responses 端点支持并完善搜索参数。两者均处于待合并状态，预计后续版本纳入。
- **MCP 工具搜索配置化**：[#33444](https://github.com/BerriAI/litellm/pull/33444) 为 `mcp_tool_search` 增加全局默认 `top_k` 和 per-key 覆盖，已在 PR 阶段并附带 DB migration。

## 7. 用户反馈摘要

- **配置管理困扰**：用户在 [#12875](https://github.com/BerriAI/litellm/issues/12875) 中反映数据库中的旧配置会静默覆盖新部署的 `general_settings`，导致配置变更不生效，排查过程费时费力。该问题已关闭。
- **代理模型组在 UI 中的体验缺陷**：[#24513](https://github.com/BerriAI/litellm/issues/24513) 表明正常的代理模型组名称（`mylitellmmodel`）在 Usage AI Chat 中不工作，普通代理请求正常但 UI 功能失败，反映出 UI 层与路由层对模型标识处理不一致。
- **计费准确性焦虑**：[#36192](https://github.com/BerriAI/litellm/issues/36192) 用户指出 Azure 模型价格未跟随 Azure 官方定价，担心成本报表失真，且涉及 terra/luna 大幅降价差异。
- **流式取消的副作用**：[#27955](https://github.com/BerriAI/litellm/issues/27955) 描述客户端中断流式请求后限流计数无法释放，最终整个代理不可用，属于对稳定性影响较大的痛点。
- **认证错误码不合理**：PR [#35480](https://github.com/BerriAI/litellm/pull/35480) 指出 master-key-only 模式下认证失败返回 500 而非 401，增加了客户端错误处理的复杂度。

## 8. 待处理积压

以下为创建时间较早、仍处于开放状态且被标记 `stale` 的 Issue/PR，建议维护者优先审视：

| 编号 | 创建时间 | 标题 | 标签 |
|------|----------|------|------|
| [#20867](https://github.com/BerriAI/litellm/issues/20867) | 2026-02-10 | 限流错误报告为 "No deployments available" 且打印堆栈 | bug, llm translation, stale |
| [#21036](https://github.com/BerriAI/litellm/issues/21036) | 2026-02-12 | Vertex AI 在使用全局 API endpoint/token 时仍强制要求凭据 | bug, llm translation, stale, SDK |
| [#24513](https://github.com/BerriAI/litellm/issues/24513) | 2026-03-24 | Usage AI Chat 在使用代理模型组名时失败 | llm translation, stale |
| [#27168](https://github.com/BerriAI/litellm/issues/27168) | 2026-05-05 | Anthropic 转换器对所有 claude 模型强制设置 effort 为 xhigh，导致 400（👍 3） | bug, proxy, llm translation, stale, claude code |
| [#27362](https://github.com/BerriAI/litellm/issues/27362) | 2026-05-07 | cooldown_handlers.py 硬编码 APIConnectionError，阻止故障转移 | bug, proxy, llm translation, stale |
| [#27363](https://github.com/BerriAI/litellm/issues/27363) | 2026-05-07 | aembedding 缺少 num_retries kwarg，导致 embedding 无重试无故障转移 | bug, proxy, llm translation, stale |
| PR [#33444](https://github.com/BerriAI/litellm/pull/33444) | 2026-07-15 | mcp_tool_search 可配置默认 top_k | mcp, enhancement（已有一个月未合并） |

这些积压项集中在 Anthropic/Vertex 适配、重试/故障转移可靠性和 UI 模型兼容性三个方面，均有真实用户场景支撑，建议在新版本规划中予以排期。

---

*本日报基于 GitHub 公开数据自动生成，链接和引用均指向原始 Issue/PR。*

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-13

## 1. 今日速览

过去 24 小时 Temporal 项目保持高度活跃：共产生 62 条 PR 更新，其中 18 条已合并或关闭、44 条仍在待合并状态；新开/活跃 Issue 3 条，但无 Issue 关闭记录，亦无新版本发布。当前开发焦点集中在两大方向：一是以 @stephanos 为代表的测试运行器（test runner）基础设施大规模重构（涉及约 11 个 PR 的 PR 栈），二是以 @chrsmith 为代表的 worker callbacks（CHASM）功能开发。整体来看，项目代码活动频繁、工程推进有序，但安全类 Issue（Go 工具链漏洞、容器镜像漏洞）的涌入需要维护者优先评估。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日明确关闭的 PR 仅 1 条：

- **[#11415 [CLOSED] Add completion callbacks to SANOs](https://github.com/temporalio/temporal/pull/11415)** — 该 PR 属于 worker callbacks 功能栈的一部分（合入 `chrsmith/wc-persist-callback-terminal-failures` 特性分支），为 SANOs（Serverless Application Notification Objects）添加 completion callbacks API 表面，并附带测试基础设施的清理与合并。

虽然该 PR 不会直接进入 `main` 分支，但它标志着 worker callbacks 功能正在从设计走向代码落地的阶段。

此外，今日有大量 PR 处于活跃更新状态，虽未合并但代表明确的项目推进方向：

- **测试运行器（Test Runner）重构**（@stephanos）：包括 [记录 canonical Go test 尝试结果 #11487](https://github.com/temporalio/temporal/pull/11487)、[驱逐 retries 至 attempt results #11488](https://github.com/temporalio/temporal/pull/11488)、[共享 JUnit 模块加固 #11513](https://github.com/temporalio/temporal/pull/11513)、[移除 legacy JUnit merger #11516](https://github.com/temporalio/temporal/pull/11516)、[持久化 canonical 尝试历史 #11515](https://github.com/temporalio/temporal/pull/11515) 等近 10 个 PR 组成的栈。该系列重构将测试执行的核心逻辑迁移到 canonical attempt results 上，为后续更可靠的测试报告、重试策略和时间处理铺路。
- **Worker Callbacks 功能**（@chrsmith）：[支持 worker-variant callbacks #11456](https://github.com/temporalio/temporal/pull/11456) 和 [Populate CallbackInfo.outcome #11520](https://github.com/temporalio/temporal/pull/11520) 持续推进，后者是嵌套 PR 栈的一部分，用于持久化 CHASM Callback 组件的终态失败。

> 综合来看，项目整体处于"基础设施重构 + 新功能并行开发"的活跃阶段，虽然今日没有直接进入 `main` 的合并，但多条 PR 栈的更新频率表明相关功能离主线合入越来越近。

## 4. 社区热点

今日评论数最多的条目是 2022 年创建的配置解析增强请求：

- **[#2341 [OPEN] config: strict mode for configuration parsing](https://github.com/temporalio/temporal/issues/2341)** — 评论 5 条，👍 1。该 Issue 由 @danielhochman 于 2022 年 1 月提出，至今仍未关闭。用户在摘要中描述了团队因配置缺少 key 却无错误提示，花费一整天排查部署问题的经历，呼吁引入配置解析的 strict mode（严格模式）。

诉求分析：这是一个长期悬而未决的"开发者体验"类需求。核心痛点是 Temporal 的 bootstrap 配置加载缺乏验证与错误信息，导致配置错误在生产部署中难以快速定位。该需求虽未进入当前开发主序列，但评论在 2026 年 8 月仍有更新，说明社区对该问题的关注持续存在。

## 5. Bug 与稳定性

今日报告了 2 条与安全相关的 Issue，按照严重程度排列：

**高危：Go 工具链漏洞**

- **[#11495 [OPEN] Bump Go toolchain to 1.26.4 to resolve net/textproto vuln (CVE-2026-42507 / GO-2026-5039)](https://github.com/temporalio/temporal/issues/11495)** — go.mod 当前声明 go 1.26.3，受标准库 `net/textproto` 包中 CVE-2026-42507（GO-2026-5039）影响。使用 Go 1.26.0–1.26.3 构建的二进制文件包含漏洞代码。尚无对应的 fix PR。

**高危：容器镜像安全漏洞**

- **[#11497 [OPEN] Request Patch Release - For High & Critical Vulnerabilities in latest images - AWS Inspector Report](https://github.com/temporalio/temporal/issues/11497)** — 用户使用 AWS Inspector 对最新 Temporal 镜像进行扫描，报告存在高危和严重漏洞，请求发布补丁版本。Issue 创建于 2026-08-12，目前无评论、无对应 fix PR。

两条漏洞的共性在于：均涉及"最新版本/镜像"受已知高危漏洞影响，且均由外部安全扫描触发。从社区行为来看，用户对 Temporal 镜像的安全响应速度有较高期待，建议维护者优先确认受影响版本并规划补丁发布。

## 6. 功能请求与路线图信号

**配置 strict mode（长期待认领）**

- [#2341](https://github.com/temporalio/temporal/issues/2341) 已标记 `enhancement` 和 `up-for-grabs`，表明这是一个适合社区贡献者接手、但尚未排入当前路线图的功能。鉴于该 Issue 已存在 4 年以上，如果项目团队近期有配置系统的重构计划，建议一并考虑。

**Worker callbacks 功能（开发中）**

- [#11415](https://github.com/temporalio/temporal/pull/11415)（SANOs completion callbacks）、[#11456](https://github.com/temporalio/temporal/pull/11456)（worker-variant callbacks）等一组 PR 正在活跃开发中，说明 worker callbacks（CHASM）是明确的路线上功能，API 正在逐步成形。

**测试框架增强（开发中）**

- @stephanos 的 Await 2.0（[#10377](https://github.com/temporalio/temporal/pull/10377)）、[自适应测试超时 #10417](https://github.com/temporalio/temporal/pull/10417)、[await 超时诊断增强 #10781](https://github.com/temporalio/temporal/pull/10781) 以及 [降低功能测试 scheduler worker 数量 #11474](https://github.com/temporalio/temporal/pull/11474)（标记 `reliability-2026`）共同指向测试可靠性与开发者体验的持续改进，这一系列 PR 极有可能进入 2026 下半年的版本。

## 7. 用户反馈摘要

今日 Issue/PR 评论区中反映出的真实用户反馈主要集中在一个长期痛点上：

- **配置错误的可诊断性不足**（来自 [#2341](https://github.com/temporalio/temporal/issues/2341)）：
  > "我们团队最近部署了一个新的 Temporal 环境，由于缺少配置 key，且 bootstrap 代码没有错误提示和校验，我们花了整整一天时间调试。"

  这反映出用户在真实的部署场景中，对配置加载的友好性有明确诉求——不仅需要启动失败，还需要清晰的错误定位信息。该反馈自 2022 年提出，至今仍无实质变化，可视为一项长期未解决的开发者体验债务。

其余新 Issue（#11497 与 #11495）均为安全扫描工具自动生成的报告型 Issue，暂时未出现用户的进一步反馈或评论。

## 8. 待处理积压

以下为需要维护者关注的长期未响应/未解决条目：

**长期开放 Issue**

- **[#2341 配置解析 strict mode（`up-for-grabs`）](https://github.com/temporalio/temporal/issues/2341)** — 创建于 2022-01-04，至今已超过 4 年。评论数 5，说明社区持续关注但无人认领。作为 `up-for-grabs` 条目，建议维护者补充更详细的实现指引（如

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*