# OpenClaw 生态日报 2026-09-04

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-03 22:36 UTC

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



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报（2026-09-04）

## 1. 今日速览

过去24小时项目保持高度活跃：17条Issue更新（新开/活跃14条，关闭3条）与42条PR更新（32条待合并），显示社区贡献意愿强烈。无新版本发布，仍处在密集开发迭代周期。当前开发重心集中在三大方向：一是LLM成本核算准确性与prompt-cache token计数修正（#4817/#4836）；二是会话状态持久化一致性重构，涉及confirmation_policy与secrets的存储位置迁移（#4810/#4813/#4814/#4849/#4847）；三是流式传输架构Epic持续推进，围绕WebSocket envelope格式与连接生命周期管理展开（#4671/#4681/#4763/#4822/#4844）。ACP provider生态扩展（Kimi、OpenCode）亦在并行推进。

---

## 2. 版本发布

过去24小时无新版本发布。

---

## 3. 项目进展

过去24小时有10条PR合并/关闭，另有3条Issue关闭，反映出以下实质进展：

**ACP Provider 生态扩展收尾**
- [PR #4714](https://github.com/OpenHands/software-agent-sdk/pull/4714)（合并）将 Kimi Code 注册为内置 ACP provider，关闭 [Issue #4716](https://github.com/OpenHands/software-agent-sdk/issues/4716)。PR 在原作者端到端验证（kimi acp 0.39.1）基础上，由维护者 rebase 至 #4832 的安装目录（install catalog）之上，成为后续 provider 接入的参考范式。
- [PR #4419](https://github.com/OpenHands/software-agent-sdk/pull/4419)（合并）完成 Pi 作为内置 ACP provider 的注册，采用双包（adapter+engine）pin 结构与 file-secret 规范，同样基于 #4832 安装目录集成。
- [PR #4827](https://github.com/OpenHands/software-agent-sdk/pull/4827) 正在推进 OpenCode 的内置 provider 支持，所有注册字段来自对真实 `opencode acp` 服务的验证，暂不纳入默认镜像。

**TypeScript Client CI 加固**
- [PR #4844](https://github.com/OpenHands/software-agent-sdk/pull/4844)（合并）使 TypeScript client 的集成测试改对当前分支构建的 agent-server 运行，修复此前集成测试一直隐式依赖远端固定版本、无法捕获分支内破坏性变更的问题。

**WebSocket 兼容性修复推进**
- [Issue #4764](https://github.com/OpenHands/software-agent-sdk/issues/4764) 关闭，但同日 [Issue #4846](https://github.com/OpenHands/software-agent-sdk/issues/4846) 被重新提交（标记 duplicate-candidate），[PR #4799](https://github.com/OpenHands/software-agent-sdk/pull/4799) 提供了修复实现并等待合并。

**其他关闭的PR/Issue**
- [PR #4114](https://github.com/OpenHands/software-agent-sdk/pull/4114)（关闭/合并）修复存储事件反序列化失败时逐条降级（degrade per event）的问题。
- [PR #4043](https://github.com/OpenHands/software-agent-sdk/pull/4043)（关闭）因过期标记为 Stale，但其核心诉求（claude-sonnet-5 应列入 `PROMPT_CACHE_MODELS`）仍具参考价值，Contributor 报告 cache_read 始终为 0、费用与 Opus 持平。

---

## 4. 社区热点

**[Issue #4817 — LLM span 成本忽略 prompt-cache tokens（5条评论）](https://github.com/OpenHands/software-agent-sdk/issues/4817)**
成本核算准确性是目前社区关注度最高的技术债。该 Issue 指出现有原生路径下 LLM span 成本计算未纳入 prompt-cache tokens，与 provider/proxy 实际账单存在偏差；同时是 #4382（ACP 路径）的对应问题，延续自 #4816 的最小修复。社区围绕修复方案产生了讨论（Option A 方案在 [PR #4848](https://github.com/OpenHands/software-agent-sdk/pull/4848) 中提交为 draft 测试 PR 进行端到端验证）。

**[Issue #4850 — Anomalyco/OpenCode 要求 LiteLLM 在3天内携带 x-opencode-session 头（4条评论）](https://github.com/OpenHands/software-agent-sdk/issues/4850)**
外部上游（BerriAI/litellm#39503）的强制变更引发社区关注。核心矛盾：OpenHands/OpenCode 在 LiteLLM/OpenHands 中并无对应 provider 注册，该会话头要求给框架集成方造成时间压力。

**[Issue #4810 — confirmation_policy、security_analyzer、secrets 变更未持久化至 meta.json（4条评论）](https://github.com/OpenHands/software-agent-sdk/issues/4810)**
状态管理持久化一致性的高频痛点。API 调用已成功写入 `base_state.json`，但 `StoredConversation`/`meta.json` 未同步，导致重启后所有变更丢失。社区正在围绕“统一由 ConversationState 作为唯一权威来源”的方向讨论架构性修复策略。

**[Issue #4708 — 请求为 RemoteConversation 提供可注入的 WebSocket 客户端工厂（3条评论）](https://github.com/OpenHands/software-agent-sdk/issues/4708)**
测试可扩展性与可观测性的功能提案。`RemoteConversation` 在 `__init__` 中硬编码 `WebSocketCallbackClient`，用户无法注入 mock 或自定义实现，限制了 SDK 在测试与监控场景下的灵活性。

---

## 5. Bug 与稳定性

按严重程度排序：

**高 — 状态持久化丢失**
- [Issue #4810](https://github.com/OpenHands/software-agent-sdk/issues/4810)：`set_confirmation_policy`、`set_security_analyzer`、`update_secrets` 的变更在重启后全部丢失。根因在于双存储（`base_state.json` vs `meta.json`）未同步。已有 [PR #4813](https://github.com/OpenHands/software-agent-sdk/pull/4813) 提出将字段移至 ConversationState 单源存储的修复方案。

**高 — RemoteConversation.fork() 静默丢弃 fork 标题**
- [Issue #4847](https://github.com/OpenHands/software-agent-sdk/issues/4847)：fork 接口返回的 `ConversationInfo` 包含 title/tags，但客户端实现丢弃了 title。此外，测试 mock 的 server 响应结构与实际接口不符，导致缺陷未被捕获。与 [PR #4814](https://github.com/OpenHands/software-agent-sdk/pull/4814)（从 fork 移除 title，改由 StoredConversation 管理）直接相关。

**高 — LLM span 成本计算错误（双重缺陷）**
- [Issue #4817](https://github.com/OpenHands/software-agent-sdk/issues/4817)：原生路径忽略 prompt-cache tokens，成本与账单偏差。分支 PR [PR #4848](https://github.com/OpenHands/software-agent-sdk/pull/4848) 正在进行实况验证；配套修复 PR [PR #4836](https://github.com/OpenHands/software-agent-sdk/pull/4836)（解决 `litellm_proxy/*` 自定义模型成本记录为 $0 的别名定价注册问题）亦在队列中。

**中 — 测试稳定性问题**
- [Issue #4840](https://github.com/OpenHands/software-agent-sdk/issues/4840)：`test_acp_agent.py` 在 7 次完整运行中 4 次失败（约57%），根因是 `TestACPAgentCleanup` 误计其他 agent 的 `_finalize` 调用——测试间隔离性不足。

**中 — WebSocket 客户端与 Node ESM 兼容性**
- [Issue #4846](https://github.com/OpenHands/software-agent-sdk/issues/4846)：`conversation` 与 `bash` 事件客户端仅检查 `window.WebSocket`，在 Node ESM 环境下因 `require` 不可用而失败。已有 [PR #4799](https://github.com/OpenHands/software-agent-sdk/pull/4799) 修复（改用 global WebSocket 并移除 ws 依赖）。与已关闭的 Issue #4764 高度重复。

**中 — MCP 重连在瞬时 HTTP 错误后失效**
- [Issue #4837](https://github.com/OpenHands/software-agent-sdk/issues/4837)：FastMCP 在瞬态 HTTP 错误后终断会话任务但嵌套计数器未归零，导致 SDK 后续重连失败——会话状态机的一致性缺陷。

---

## 6. 功能请求与路线图信号

**流式传输架构（Streaming Epic）进入第五步**
- [Issue #4671](https://github.com/OpenHands/software-agent-sdk/issues/4671)（Epic）+ [Issue #4681](https://github.com/OpenHands/software-agent-sdk/issues/4681)（步骤3+4，已关闭）。服务器端 endpoint（#4807，已合并）已落地，[PR #4822](https://github.com/OpenHands/software-agent-sdk/pull/4822) 推进至“StreamContext 铸造流身份并关闭每个流”，[Issue #4763](https://github.com/OpenHands/software-agent-sdk/issues/4763) 则等待针对 pinned agent-server release 的客户端适配。预计下一版本将显著强化双通道（durable events vs PubSub token deltas）的统一。

**可注入 WebSocket 客户端工厂**
- [Issue #4708](https://github.com/OpenHands/software-agent-sdk/issues/4708)（截至今日已开放约7天）：允许外部注入自定义 WebSocket 客户端工厂，提升 `RemoteConversation` 的可测试性。小而清晰，低侵入，属社区欢迎的 DX 改善类型，提议者 @p1c2u 已给出初步设计。

**ConversationInfo 数据模型收敛**
- [Issue #4849](https://github.com/OpenHands/software-agent-sdk/issues/4849)：提议从 `ConversationState`/`StoredConversation` 动态派生 `ConversationInfo`，而非重新声明约20个冗余字段。与前述持久化 Issue #4810/#4847 同源同向——均指向“单一事实来源”的模型重构主线。

**ACP 云支持范围显式声明**
- [Issue #4841](https://github.com/OpenHands/software-agent-sdk/issues/4841)：区分 “Registered / Preinstalled / Cloud-supported” 三层支持语义，要求显式声明哪些 ACP harness 在云端环境被支持。

**ACP 下游 CI 对齐**
- [Issue #4833](https://github.com/OpenHands/software-agent-sdk/issues/4833)：所有消费 SDK 的仓库需对 `ACP_PROVIDERS`/`ACP_INSTALL_CATALOG` 注册变更设置 CI 断言，避免各自维护的 provider 知识副本过期。

两项目前均标记 `ready-for-dev`，是下一阶段集成/发布的重要候选功能，同时也验证着 #4820（新增4个ACP provider的per provider定制）是否真正可复用。

**processs 改进**
- [Issue #4605](https://github.com/OpenHands/software-agent-sdk/issues/4605)：将 `ready-for-dev` 流程与 OpenHands 主库对齐，新增 SDK 特定的复现门槛（python/pytest/uv/pip 标准），从流程上保证提交质量。

---

## 7. 用户反馈摘要

**关于 WebSocket 兼容性问题：用户对回归持敏感态度**
报告者 @georgeglarson（[Issue #4846](https://github.com/OpenHands/software-agent-sdk/issues/4846)）指出：其 ESM 包中无法 use `require('ws')`，导致 bash 和 conversation 客户端完全不可用。此问题曾被维护者以某种原因关闭（#4764），但用户重新提起并非常细致地在描述中说明“这不是重复”的理由与适用环境（Node 22 global WebSocket）；同时也自行提交了修复 PR #4799，是典型的“发现问题 → 自己修复”路径，说明 SDK 的技术门槛在社区接受度较好。

**关于 LLM 成本可观测性：用户对费用透明化有明确期待**
[Issue #4817](https://github.com/OpenHands/software-agent-sdk/issues/4817) 的报障用户可以精确地指出成本核算与账单差异的路径差异（原生路径 vs ACP 路径，缓存 token 不参与计费的问题），并明确说明这是对 #4382 缺失一半的补全，体现了高质量工程用户对 SDK 成本可观测性诉求的强烈关注。

**关于 upstream 变更的被动响应**
[Issue #4850](https://github.com/OpenHands/software-agent-sdk/issues/4850) 的提问者表达了对不受自身控制的上游变化（LiteLLM 强制要求增加 x-opencode-session 头）的紧迫感，因其在 OpenHands（

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目日报 — 2026-09-04

> 数据源：github.com/temporalio/temporal | 统计时段：过去 24 小时

## 1. 今日速览

- 过去 24 小时项目整体活跃度较高：共 68 条 PR 被更新，其中 19 条已合并/关闭，49 条仍处于开放/待合并状态。
- Issues 侧很平静，仅新增 1 条 enhancement；今日无新版本发布。
- 已关闭/合并的 PR 主要集中在历史分页校验、Worker Deployment 清理、shutdown poll 竞态修复等稳定性与可靠性方向。
- 仍在迭代的开放 PR 则集中在动态分区、poller 自动扩缩容信号、CHASM/Nexus 可观测性等中长期能力建设。
- 总体来看，项目状态健康：PR 流动量大，缺陷修复节奏快，Issue 新增压力低；但 49 条待合并 PR 中不乏已持续数周的复杂改动，需要关注评审与合并效率。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*