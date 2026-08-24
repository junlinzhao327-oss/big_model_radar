# OpenClaw 生态日报 2026-08-25

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-24 22:36 UTC

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

**报告日期：** 2026-08-25  
**数据快照区间：** 2026-08-23 ~ 2026-08-24（各项目 GitHub API）  
**说明：** OpenClaw、Pi、Temporal 三个项目本次数据快照为空，仅作项目占位与生态定位说明，不进行量化对比。

---

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态呈现**高活跃度与生产化转型并行的态势**。以 Hermes Agent、OpenHands SDK、LiteLLM 为代表的项目在 24 小时内合计产生超 600 条 Issue 与 760 条 PR 更新，但**无一发布新版本**，说明行业正处于密集修复合璧、功能快速沉淀的"冲刺前夜"。社区诉求高度趋同：**MCP 工具生态的易用性、会话/状态持久化的可靠性、多提供方兼容层的稳健性、以及生产环境的安全与成本控制**是跨项目共通的四大焦点。与此同时，高 PR 待合并积压（如 Hermes 403 条、LiteLLM 145 条）暴露了社区规模扩大后的审查瓶颈，流程治理将成为下一阶段项目健康度的关键变量。

---

## 2. 各项目活跃度对比

| 项目 | Issue 更新（新开/活跃 / 关闭） | PR 更新（待合并 / 合并或关闭） | Release | 合并率 | 健康度评估 |
|------|------|------|---------|--------|-----------|
| **Hermes Agent** | 500（313 / 187，关闭率 37.4%） | 500（403 / 97，合并率 19.4%） | 无 | 19.4% | 🟡 **高活跃但有瓶颈**：P1/P2 Bug 密集，修复 PR 集中，但 403 条 PR 待合并积压严重 |
| **OpenHands SDK** | 23（13 / 10） | 37（21 / 16，合并率 43.2%） | 无 | 43.2% | 🟢 **健康迭代**：高优 Bug 24h 内响应，闭环效率高，社区讨论有深度 |
| **LiteLLM** | 89（58 / 31） | 231（145 / 86，合并率 37.2%） | 无 | 37.2% | 🟢 **冲刺攻坚**：稳定性 Sprint 聚焦明确，安全/可靠性修复优先，合并节奏正常 |
| **OpenClaw** | 数据快照为空 | 数据快照为空 | — | — | ⚪ 无法评估 |
| **Pi** | 数据快照为空 | 数据快照为空 | — | — | ⚪ 无法评估 |
| **Temporal** | 数据快照为空 | 数据快照为空 | — | — | ⚪ 无法评估 |

> 注：合并率按"已合并/关闭 PR ÷ PR 更新总数"估算，各项目 PR 状态口径可能不同，仅作相对参考。

---

## 3. OpenClaw 在生态中的定位

OpenClaw 被列为本报告的核心参照项目，但本次 GitHub 数据快照为空，无法进行同口径量化对比。从生态格局推断：

- **功能坐标**：从命名和"个人 AI 助手"定位看，OpenClaw 大概率与 Hermes Agent、OpenHands SDK 处于同一赛道（Agent 运行时/编排层），但可能更侧重于**本地优先、个人化部署与多设备协同**，以区别于 Hermes 的桌面重客户端路线和 OpenHands 的开发者 SDK 路线。
- **生态位缺口**：当前三个有数据项目各自占据"桌面端 Agent 运行时"（Hermes）、"多智能体开发 SDK"（OpenHands）、"LLM 网关/可观测性"（LiteLLM）三个生态位。OpenClaw 作为"核心参照"被提出，推测其可能是**个人 AI 助手的统一入口/编排框架**，填补端侧到服务端之间的空白。
- **待验证项**：其社区规模、技术栈（是否基于 MCP）、与 LiteLLM 等网关的集成关系，需后续补充数据再评估。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求/案例 |
|---------|---------|-------------|
| **安全与密钥管理** | OpenHands、LiteLLM、Hermes | OpenHands [#4609](https://github.com/OpenHands/software-agent-sdk/issues/4609) 密钥明文持久化；LiteLLM [#38114](https://github.com/BerriAI/litellm/pull/38114) Vertex 透传泄露调用方认证头；Hermes [#94244](https://github.com/NousResearch/hermes-agent/pull/94244) 认证边界修复 |
| **MCP 生态治理** | Hermes、OpenHands、LiteLLM | Hermes [#51587](https://github.com/NousResearch/hermes-agent/issues/51587) MCP 工具无法进入会话工具集；OpenHands 希望 `.mcp.json` 自动发现与选择性注册（[#2754](https://github.com/OpenHands/software-agent-sdk/issues/2754)、[#376](https://github.com/OpenHands/software-agent-sdk/issues/376)）；LiteLLM 遭遇 MCP 工具调用劫持（[#37031](https://github.com/BerriAI/litellm/issues/370

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-25

> 数据区间：2026-08-23 ~ 2026-08-24（GitHub API 快照）  
> 数据来源：github.com/NousResearch/hermes-agent Issues / PRs / Releases

---

## 1. 今日速览

过去 24 小时项目**高度活跃**：500 条 Issue 更新（新开/活跃 313、关闭 187，关闭率 37.4%），500 条 PR 更新（待合并 403、已合并/关闭 97，合并率 19.4%）。无新版本发布。值得注意的信号：**P1/P2 级 Bug 密集出现在 Desktop、Session 状态、安装/更新链路**，同时一批针对性修复 PR 已在 24 小时内集中提交，显示维护团队正在围绕 "session-state" 与 "fleet update reliability" 两个方向进行系统性攻坚。PR 待合并队列高达 403 条，审查积压是当前流程健康度的主要短板。

---

## 3. 项目进展

> 说明：今日无新版本 Release。数据快照未单独列出已合并 PR 明细，以下通过已关闭 Issue 与新增 fix PR 推断项目实际推进方向。

### 3.1 已关闭 Issue 反映的修复落地

- **Desktop GUI 缩放设置回退**（[#60693](https://github.com/NousResearch/hermes-agent/issues/60693)）：110% 缩放间歇性重置为 100%，已关闭，推测对应修复已合入。
- **MCP 工具无法进入会话工具集**（[#51587](https://github.com/NousResearch/hermes-agent/issues/51587)，P1）：stdio MCP 连接成功但工具不显示，已关闭，阻塞性 Bug 解决。
- **terminal 工具 embedded null 崩溃**（[#82887](https://github.com/NousResearch/hermes-agent/issues/82887)）：路径含二进制可执行文件时 `ValueError`，根因定位在 `_read_script_in_env`，已关闭。
- **Playwright Chromium 安装挂起**（[#76312](https://github.com/NousResearch/hermes-agent/issues/76312)）与 **Fedora 44 安装失败**（[#93063](https://github.com/NousResearch/hermes-agent/issues/93063)）：均为安装链路 Bug，已关闭，安装器稳定性有实质改进。
- **Desktop 编辑早期消息失败**（[#75756](https://github.com/NousResearch/hermes-agent/issues/75756)）：`Edit failed / session not found`，已关闭。
- **Per-subagent 模型覆盖请求**（[#58731](https://github.com/NousResearch/hermes-agent/issues/58731)）：标记 `sweeper:not-planned` 关闭，明确暂不纳入路线图。

### 3.2 新提交 fix/feat PR 方向

今日集中提交的 PR 呈现明确的攻坚主题（均为 OPEN 状态，待合并）：

| 方向 | PR | 解决的问题 |
|---|---|---|
| Desktop 多连接路由 | [#94147](https://github.com/NousResearch/hermes-agent/pull/94147) | Remote New Bot 保留 profile origin、路由到 owner、首轮前 preflight provider |
| Desktop 重连会话恢复 | [#92733](https://github.com/NousResearch/hermes-agent/pull/92733) | 重连 attach 后 hydrate transcript，收敛 durable transcript 与最新 live turn |
| Bot Mode 会话同步 | [#94255](https://github.com/NousResearch/hermes-agent/pull/94255) | workspace-tile 在 `sessions.changed` 时 reconcile，修复后台投递不刷新 |
| 认证边界 | [#94244](https://github.com/NousResearch/hermes-agent/pull/94244) | 修复 gated 模式下 loopback `?token=` WS 认证被拒绝（#93981

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-08-25

## 1. 今日速览

过去24小时内，OpenHands SDK 项目保持**高度活跃**：共更新 23 条 Issue（新开/活跃 13 条，关闭 10 条）和 37 条 PR（待合并 21 条，合并/关闭 16 条），无新版本发布。项目当前重点集中在**稳定性修复**（线程池死锁、异步挂起、浏览器工具冲突）、**安全性增强**（密钥明文存储、MCP OAuth 测试隔离）以及**API 体验优化**（标签端点、工具调用解析）上。社区讨论热度集中在长期未决的 A2A 协议支持与 MCP 工具管理两个方向，整体项目健康度良好，维护者响应迅速。

📊 **活跃度评估**：高。大量 `priority:high` 的 bug 在 24 小时内被关闭或进入修复流程，说明问题追踪与修复闭环效率较高。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日合并/关闭的 PR 主要聚焦于测试基础设施、依赖安全和 bug 修复，具体进展如下：

### 🔧 修复与改进
- **[#4616 `Fix: incorrectly removes action event`](https://github.com/OpenHands/software-agent-sdk/pull/4616) [OPEN]**：修复了持久化确认恢复流程中误删 action 事件的问题，与 [#4532](https://github.com/OpenHands/software-agent-sdk/issues/4532) 相关，解决了恢复会话时丢失 tool_use 消息的缺陷。
- **[#4610 `fix: normalize tool call ids before persisting events`](https://github.com/OpenHands/software-agent-sdk/pull/4610) [OPEN]**：修复并行 MCP 工具调用 ID 含有 `:` 等特殊字符导致的事件持久化关联问题。
- **[#4521 `test(agent-server): isolate MCP OAuth settings persistence via OH_PERSISTENCE_DIR`](https://github.com/OpenHands/software-agent-sdk/pull/4521) [CLOSED]**：修复 MCP OAuth 设置存储测试可能污染开发者/CI 默认持久化目录的问题，对应 Issue [#4604](https://github.com/OpenHands/software-agent-sdk/issues/4604)。

### 📦 依赖安全更新
- **[#4620 `chore(deps): bump httplib2 from 0.31.0 to 0.32.0`](https://github.com/OpenHands/software-agent-sdk/pull/4620) [CLOSED]**：依赖安全/兼容性升级。
- **[#4619 `chore(deps): bump pyasn1 from 0.6.3 to 0.6.4`](https://github.com/OpenHands/software-agent-sdk/pull/4619) [CLOSED]**：**安全发布**，修复 CVE 漏洞。

### 🏗️ 新功能
- **[#4622 `feat(tools): add factory_spawn server tool + attach client tools to resolved agents`](https://github.com/OpenHands/software-agent-sdk/pull/4622) [CLOSED]**：新增 `factory_spawn` 服务端工具，为多智能体场景提供新的工具扩展机制。

> 💡 **整体判断**：项目在稳定性（死锁、销毁挂起）、安全（CVE 修复、密钥处理）和测试质量方面均有推进，虽无重大功能落地，但为下一版本铺平了基础。

---

## 4. 社区热点

### 🥇 最热 Issue
- **[#1787 `Proposal: Fork conversation when tools change`](https://github.com/OpenHands/software-agent-sdk/issues/1787)【23 条评论】**：已关闭。讨论如何在对话中途增删工具时保持事件日志不可变——通过 fork 对话而非修改系统提示词。虽然已 stale，但体现了社区对工具动态管理的深层需求。

### 🥈 高关注度讨论
- **[#1060 `Google a2a support`](https://github.com/OpenHands/software-agent-sdk/issues/1060)【20 条评论，👍 26】OPEN**：自 2025 年 4 月以来持续活跃，社区对 A2A（Agent-to-Agent）协议互操作的需求强烈，目前仍在等待 `ready-for-dev`。
- **[#2754 `Auto-discover project-scoped .mcp.json`](https://github.com/OpenHands/software-agent-sdk/issues/2754)【12 条评论】CLOSED**：用户希望 MCP 服务器配置能通过项目级 `.mcp.json` 自动发现，减少手动传入 `Agent(mcp_config=...)` 的负担。已关闭，但相关诉求影响了后续 MCP 工具管理方向的讨论。
- **[#4540 `Tool calls return incorrect/weird syntax with Synthetic Provider`](https://github.com/OpenHands/software-agent-sdk/issues/4540)【7 条评论】OPEN**：用户报告在 Agent Canvas 1.14.0 中使用 Synthetic provider 时，工具调用返回异常原始语法，直接影响开发体验，已标记 `ready-for-dev`。

> 💡 **诉求分析**：社区热点集中在两个方向：一是 **MCP 工具生态的易用性**（自动发现、选择性注册、解析兼容），二是 **模型/API 兼容层稳定性**（Synthetic provider、Qwen3、OpenAI prefix），表明用户在真实项目中广泛集成外部模型与工具服务，对适配层质量要求很高。

---

## 5. Bug 与稳定性

### 🔴 高优先级（priority: high）
| Issue | 问题描述 | 状态 | 对应修复 PR |
|-------|---------|------|------------|
| [#4597](https://github.com/OpenHands/software-agent-sdk/issues/4597) | `AsyncExecutor.close()` 在同步代码阻塞时永久挂起 | 已关闭（24h 内） | 由 [#4546](https://github.com/OpenHands/software-agent-sdk/issues/4546) 同类问题驱动，已修复 |
| [#4514](https://github.com/OpenHands/software-agent-sdk/issues/4514) | 生命周期锁 + 线程池耗尽导致所有事件加载阻塞 | 已关闭（24h 内） | 已修复，相关修复涉及锁范围优化 |
| [#4532](https://github.com/OpenHands/software-agent-sdk/issues/4532) | 恢复确认暂停的对话时丢失 assistant `tool_use` 消息，导致 LLM 请求被拒绝 | OPEN | [#4616](https://github.com/OpenHands/software-agent-sdk/pull/4616) OPEN |
| [#4601](https://github.com/OpenHands/software-agent-sdk/issues/4601) | 浏览器工具共享 `user_data_dir`，导致 SingletonLock 冲突和僵尸线程 | 已关闭 || 

### 🟡 中优先级（priority: medium）
| Issue | 问题描述 | 状态 | 对应修复 PR |
|-------|---------|------|------------|
| [#4541](https://github.com/OpenHands/software-agent-sdk/issues/4541) | Qwen3-32B 的 `<think>` 标签出现异常行为（标题污染、思维块丢失） | 已关闭 | 已处理 |
| [#4540](https://github.com/OpenHands/software-agent-sdk/issues/4540) | Synthetic Provider 工具调用返回异常语法 | OPEN `ready-for-dev` | — |
| [#4613](https://github.com/OpenHands/software-agent-sdk/issues/4613) | OpenAI provider 对命名空间模型 ID 前缀重复剥离 | OPEN `ready-for-dev` | [#4438](https://github.com/OpenHands/software-agent-sdk/pull/4438) OPEN |
| [#4604](https://github.com/OpenHands/software-agent-sdk/issues/4604) | MCP OAuth 设置存储测试污染默认持久化目录 | OPEN | [#4521](https://github.com/OpenHands/software-agent-sdk/pull/4521) CLOSED |

> ⚠️ **观察**：高优先级 bug 主要集中在**并发/生命周期管理**（线程池、锁、异步关闭）和**持久化恢复**的边界场景，这些都是生产环境高负载下容易暴露的问题。好消息是多数已快速关闭或已有对应 PR，项目响应速度和修复质量均在线。

---

## 6. 功能请求与路线图信号

| Issue/PR | 需求 | 状态 | 纳入下一版本的可能性 |
|---------|------|------|---------------------|
| [#4624](https://github.com/OpenHands/software-agent-sdk/issues/4624) | 将 ACP provider 从被废弃的 Gemini CLI 迁移至 Antigravity CLI（agy） | OPEN | **高**。Google 已官方停服 Gemini CLI，属外部依赖强迁移，预计近期会进开发计划。 |
| [#4577](https://github.com/OpenHands/software-agent-sdk/issues/4577) | 为标签增加 per-key 端点，避免 PATCH 接口的读改写开销 | OPEN | **高**。[#4617](https://github.com/OpenHands/software-agent-sdk/pull/4617) 已提交实现，可能进入下一版本。 |
| [#4589](https://github.com/OpenHands/software-agent-sdk/issues/4589) | 为历史上慢/死锁操作增加 per-operation 计时埋点 | OPEN `ready-for-dev` | **中高**。属于运维可观测性改进，与近期稳定性修复一脉相承。 |
| [#4609](https://github.com/OpenHands/software-agent-sdk/issues/4609) | `OH_SECRET_KEY` 未设置时拒绝明文持久化密钥 | OPEN `ready-for-dev` | **高**。[#4618](https://github.com/OpenHands/software-agent-sdk/pull/4618) 已实现（require_secret_key），安全向改动，合入概率大。 |
| [#4605](https://github.com/OpenHands/software-agent-sdk/issues/4605) | 增加并强制 `ready-for-dev` Issue/PR 就绪门禁 | OPEN | 中。属于流程改进，短期可能先落地为 CI 检查。 |
| [#4621](https://github.com/OpenHands/software-agent-sdk/issues/4621) | 清理失效/重复的 PR 自动化标签（review-this、oh-docstring 等） | OPEN | 中。仓库卫生类需求，影响面小。 |

> 📌 **路线图判断**：下一版本可能聚焦三大主题：**ACP/Gemini CLI 迁移**、**密钥/安全增强**、**标签 API 便捷化**。同时 MCP 工具过滤（[#376](https://github.com/OpenHands/software-agent-sdk/issues/376)）、Tool search（[#4083](https://github.com/OpenHands/software-agent-sdk/issues/4083)）等中期课题仍值得关注。

---

## 7. 用户反馈摘要

根据今日活跃的 Issue 评论，提炼用户真实反馈：

- **🧩 持久化恢复的信任危机**（[#4532](https://github.com/OpenHands/software-agent-sdk/issues/4532)）：用户指出暂停确认的对话在恢复后，LLM 请求缺少 assistant `tool_use` 消息却仍带 `tool_result`，导致 Bedrock 等供应商直接拒绝请求。**痛点**：确认流程是生产环境常用特性，该缺陷导致对话无法继续，影响严重。

- **🔐 安全焦虑**（[#4609](https://github.com/OpenHands/software-agent-sdk/issues/4609)）：用户反馈当 `OH_SECRET_KEY` 未设置时，密钥以明文持久化。**诉求**：期望系统在存在密钥时强制要求设置 `OH_SECRET_KEY`，或至少提供显式拒绝选项，避免敏感信息裸奔。

- **⚡ API 效率抱怨**（[#4577](https://github.com/OpenHands/software-agent-sdk/issues/4577)）：开发者和集成方反映 `PATCH /api/conversations/{id}` 更新标签时替换整个 map 的设计，在客户端场景下容易产生竞态，且效率低下。**诉求**：提供 per-key 的增删端点（[#4617](https://github.com/OpenHands/software-agent-sdk/pull/4617) 已响应）。

- **🧠 模型兼容性困惑**（[#4541](https://github.com/OpenHands/software-agent-sdk/issues/4541)、[#4613](https://github.com/OpenHands/software-agent-sdk/issues/4613)）：Qwen3 的 `<think>` 处理、OpenAI 命名空间模型 ID 的 prefix 剥离问题，让用户对 Agent Canvas 的模型无关性承诺产生疑虑。**期望**：SDK 在适配层更透明、更健壮，或至少将 provider 侧的解析责任清晰文档化（[#4614](https://github.com/OpenHands/software-agent-sdk/pull/4614) 已在此方向推进）。

---

## 8. 待处理积压

以下为长期未决、但有一定重要性的 Issue/PR，建议维护者优先关注：

| 编号 | 类型 | 标题 | 创建时间 | 最后更新 | 备注 |
|------|------|------|---------|---------|------|
| [#1060](https://github.com/OpenHands/software-agent-sdk/issues/1060) | Issue | Google a2a support | 2025-04-21 | 2026-08-24 | 已活跃超 16 个月，👍 26，处于 `ready-for-dev` 但始终未开工 |
| [#376](https://github.com/OpenHands/software-agent-sdk/issues/376) | Issue | MCP Tool Integration: Selective tool registration and filtering | 2025-09-20 | 2026-08-24 | 近 1 年未动，MCP 工具权重问题持续存在 |
| [#3673](https://github.com/OpenHands/software-agent-sdk/pull/3673) | PR | feat(sdk): add ask_oracle tool | 2026-06-11 | 2026-08-24 | `review-this` 标记至今未被合并，功能对复杂任务有帮助 |
| [#3958](https://github.com/OpenHands/software-agent-sdk/pull/3958) | PR | chore(deps): bump docker/build-push-action | 2026-07-02 | 2026-08-24 | 依赖长期未合并，存在潜在兼容性风险 |
| [#4083](https://github.com/OpenHands/software-agent-sdk/issues/4083) | Issue | Investig

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-25

## 1. 今日速览

过去 24 小时 LiteLLM 项目活跃度处于高位：共产生 89 条 Issue 更新（新开/活跃 58、关闭 31）和 231 条 PR 更新（待合并 145、已合并/关闭 86），无新版本发布。开发重心明显聚焦于**稳定性冲刺（Stability Sprint）**，围绕预算计费一致性（如 #27735）、MCP 工具调用劫持（#37031）、流式响应回归（#36767）等方向密集提交修复；同时新增 ConductGuard 集成（#38143）、vLLM-Omni 视频 API（#38148）等功能性 PR，释放出"存量问题修复与增量功能扩展并行"的信号。社区侧讨论热度最高的议题集中在稳定性路线图、OOM 内存泄漏与 Copilot 超额费用，说明生产环境可靠性是用户当前的核心诉求。

---

## 2. 版本发布

**无新版本发布。** 当前最新版本仍为 v1.94.x 系列（参考 #36767 回归描述）。建议关注 `staging` 分支中密集合并的修复 PR（如 #38114、#38141），预计近期将有一个以稳定性修复为主的 patch/minor 版本发布。

---

## 3. 项目进展

今日合并/关闭的关键 PR 表明项目在**安全加固、配置可靠性、路由稳定性**三个方向取得实质推进：

- **[已关闭] fix(passthrough): 修复 Vertex 透传泄露调用方虚拟密钥（#38114）** — 修复无凭证 Vertex 透传时，将 `Authorization`、`x-litellm-api-key`、`x-goog-api-key` 等调用方认证头转发至 Google 的安全漏洞。这是高危修复，影响所有使用 Vertex 透传的代理用户。[PR #38114](https://github.com/BerriAI/litellm/pull/38114)
- **[已合并] feat(complexity_router): 为分类器上下文设置边界而非限制单轮长度（#38141）** — 被 #38145 明确标注"已合并"，修正了复杂度路由分类器将每轮对话独立截断至 200 字符、导致普通对话在进入分类器前被切碎的问题。[PR #38145](https://github.com/BerriAI/litellm/pull/38145)
- **[已关闭] feat(models): 审计注册表元数据并修正 Databricks 缓存定价（#37902）** — 重新对照官方文档校验模型注册表元数据，将 Databricks 缓存 token 从全价修正为缓存价，并清理了退役路由的不完整元数据。[PR #37902](https://github.com/BerriAI/litellm/pull/37902)
- **ci 门禁强化：禁止 Prisma 迁移中包含行级重写 DML（#37899）** — 新增代码质量门禁，拒绝迁移文件中出现 `UPDATE`/`DELETE`/`MERGE` 等未分批的行重写操作，避免代理启动时迁移导致停机。此前已发生一次需回滚的未分批 `UPDATE` 事故。[PR #37899](https://github.com/BerriAI/litellm/pull/37899)

另有 86 条 PR 已合并/关闭，整体呈现"安全漏洞优先修复 + 核心链路可靠性加固 + 新集成快速落地"的推进节奏。

---

## 4. 社区热点

- **LiteLLM 稳定性冲刺路线图（#30484，26 评论，👍6）** — 官方发布的稳定性 Sprint Roadmap，列出 `/v1/model/info` 响应不一致、OOM、预算计算等已知问题的修复计划，并征集用户反馈。该 issue 已成为社区集中反馈生产稳定性问题的汇聚点，评论数断层领先。[Issue #30484](https://github.com/BerriAI/litellm/issues/30484)
- **Pod 因内存持续增长被 OOM Kill（#25219，14 评论，👍6，已关闭）** — 用户升级至 `main-v1.82.0-stable` 镜像后频繁出现 OOM。评论中多名用户反馈复现路径，最终关闭，是全社区最关注的内存问题之一。[Issue #25219](https://github.com/BerriAI/litellm/issues/25219)
- **虚拟密钥预算达到上限却拒绝请求，/key/info 显示花费未超限（#27735，11 评论）** — 团队作用域虚拟密钥请求被 `BudgetExceededError` 拒绝，但管理 API 显示 spend 低于 max_budget。该 issue 指向预算计数器陈旧/不同步问题，影响实际业务可用性，评论中已有多个用户确认遇到同类现象。[Issue #27735](https://github.com/BerriAI/litellm/issues/27735)
- **GitHub Copilot 提供方产生超额 Premium 请求（#18155，6 评论，👍10）** — 在长时多轮 agentic 流程中（Plan mode、子代理流、工具调用），LiteLLM 代理导致 Copilot 产生大量额外 premium 请求，用户直接感受到成本上涨。👍 数为全榜最高，反映生产用户对成本的敏感关注。[Issue #18155](https://github.com/BerriAI/litellm/issues/18155)

**诉求分析：** 社区当前最强烈的三个诉求分别是——① 生产环境内存/稳定性问题（OOM、预算不一致）；② 成本可预测性（Copilot 超额请求、缓存定价准确性）；③ 对官方路线图的参与感（Stability Sprint 征集意见

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*