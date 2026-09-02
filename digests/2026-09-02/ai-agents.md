# OpenClaw 生态日报 2026-09-02

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-02 00:19 UTC

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

# Hermes Agent 项目动态日报 — 2026-09-02

## 今日速览
项目在过去24小时内保持极高活跃度：**461 条 Issues 更新**（新开/活跃 364 条，关闭 97 条）与 **500 条 PR 更新**（待合并 399 条，合并/关闭 101 条）均创近期高位，显示社区贡献与维护者响应均处于满负荷状态。无新版本发布，但 P1 级 Bug 的修复与关闭速度同步加快；会话状态持久化、上下文压缩管道、Windows 平台兼容性仍是最集中的攻坚方向。社区围绕 Claude 订阅 OAuth、Bot Group Chats 跨端可用性、持久化记忆等议题形成了明显共识性诉求。

---

## 项目进展

今日共合并/关闭 **101 条 PR**（占 PR 更新总量 20.2%），虽无版本发布，但从活跃 PR 队列可清晰看到以下方向正在推进：

**网关与会话基础设施**
- [fix(api_server): use the shared SessionDB registry](https://github.com/NousResearch/hermes-agent/pull/100767) — 移除 API server 私有的 SessionDB 写入器，改用进程级共享注册表，消除多写者导致的 state.db 竞争风险。直接呼应 #90837 的库损坏问题。
- [fix(gateway): suppress repeated backend-unavailable notices](https://github.com/NousResearch/hermes-agent/pull/100769) — 后端宕机时不再逐条暴露内部异常细节，改为在投递边界做信号抑制。
- [fix(gateway): arm loop-tick witness only on POSIX](https://github.com/NousResearch/hermes-agent/pull/96989) — 修复 Windows 上因 `asyncio.start_unix_server` 不存在导致网关启动即抛 AttributeError 的问题，推动 #96956 关闭。

**桌面端稳定性**
- [fix(desktop): bound orphan-reap sweep so slow probes cannot stall boot](https://github.com/NousResearch/hermes-agent/pull/100774) — 为 Windows 孤儿进程清扫增加 5s 超时上限，避免 PowerShell 探测阻塞启动。
- [feat(desktop): add WS disconnect diagnostics for 3-minute drop investigation](https://github.com/NousResearch/hermes-agent/pull/100779) — 为 Windows 上间歇性 3 分钟断连问题补充客户端/服务端双向探针。

**工具链与兼容性**
- [fix(search): handle unprefixed ripgrep I/O diagnostics](https://github.com/NousResearch/hermes-agent/pull/99985) — 修复 ripgrep 0.10.0 无 `rg:` 前缀错误被误判为工具输出损坏的问题。
- [fix(tools): cleanup daemons idle on an Event](https://github.com/NousResearch/hermes-agent/pull/100784) — 避免 terminal/browser 工具后台守护线程被 `time.sleep` patch 后变成忙循环，解决测试串扰。
- [Background PTY sessions no longer hang on terminal probes](https://github.com/NousResearch/hermes-agent/pull/100775) — 引入有界应答机制，修复子进程探测终端状态时后台 PTY 会话挂起。

**代码架构重构**
- [refactor(gateway): extract slash-command handlers into package](https://github.com/NousResearch/hermes-agent/pull/99999) — 将 75 个方法的网关 slash-command 巨类拆分为独立包，延续 god-file 治理策略。
- [feat(runtime): add provider-neutral AgentRuntime plugin API](https://github.com/NousResearch/hermes-agent/pull/99474) — 新增 profile-scoped 运行时注册接口，为第三方整轮运行时提供标准接入缝。

---

## 社区热点

### 1. Skills index 持续降级，自动巡检发现 29.8h 未重建
[#66616](https://github.com/NousResearch/hermes-agent/issues/66616) — **137 条评论**，自动化探针报告 `/docs/api/skills-index.json` 已过期 29.8 小时（限时 26h）。该问题由 bot 持续跟踪，长时间未关闭，说明索引构建工作流的可靠性需要人工介入。

### 2. 外部自动化集成被 cron 冲突阻塞
[#88584](https://github.com/NousResearch/hermes-agent/issues/88584) — **52 条评论**，Nous-to-Enterkey 定时合并因 `cron/jobs.py` 冲突持续失败，dashboard 更新器停留在旧版本。该 issue 被打上 `invalid` 标签但仍有大量讨论，反映跨仓库协作流程的摩擦。

### 3. 持久化会话记忆（跨会话搜索 + 自动压缩）成为最长寿功能请求
[#8457](https://github.com/NousResearch/hermes-agent/issues/8457) — **19 条评论**，自 4 月提出至今持续获得关注。用户核心痛点是会话结束后上下文完全丢失、`MemoryManager` 缺乏跨 gateway 重启的持久化机制。该请求与 #97948、#97963 等压缩管道 Bug 形成呼应：**先有可靠的持久化/压缩，才能谈记忆**。

### 4. Claude 订阅用户拒绝“双重付费”
[#25267](https://github.com/NousResearch/hermes-agent/issues/25267) — **53 👍 / 18 条评论**，是当前获赞最多的功能请求。用户希望用 Claude Pro/Max 订阅通过 OAuth 直接接入 Hermes，而非额外支付 per-token API 费用。相关 bug [#65365](https://github.com/NousResearch/hermes-agent/issues/65365) 显示即使使用 OAuth，暴露 `memory`/`session_search` 工具也会被 Anthropic 拒绝并要求“添加额外用量”——这进一步放大了订阅用户的挫败感。

### 5. Desktop 远程会话恢复失败（已修复，讨论热度仍高）
[#93888](https://github.com/NousResearch/hermes-agent/issues/93888) — **18 条评论**，桌面端向远程 Gateway 发送本地 8 位运行时 ID 导致“Session not found”无法恢复。该 P1 已关闭，但讨论量大，说明远程桌面场景用户基数可观。

### 6. Bot Group Chats 脱离桌面运行成为一致诉求
[#97681](https://github.com/NousResearch/hermes-agent/issues/97681)（16 评论）、[#89995](https://github.com/NousResearch/hermes-agent/issues/89995)（16 评论）、[#95163](https://github.com/NousResearch/hermes-agent/issues/95163)（11 评论）三案相互关联：用户要求 Bot 群聊在桌面关闭后继续运行、在 Web dashboard 中可访问、并转为 gateway 权威的后端托管模式。这已成为 Bot 功能走向生产化的明确路线图信号。

---

## Bug 与稳定性

### P1 · 仍开放

- [**state.db 反复损坏 — 11 次事故，已排除所有外部因素**](https://github.com/NousResearch/hermes-agent/issues/90837)
  生产网关在 8/02–8/20 间 11 次损坏 state.db，团队已建立小时级冻结哨兵（DB+WAL/SHM+lsof+进程表），所有外部原因均被现场排除。这是目前最严重的稳定性

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-09-02

## 1. 今日速览

过去24小时内，项目保持高活跃度：共产生 25 条 Issue 更新（其中 15 条新开/活跃、10 条关闭）及 50 条 PR 更新（43 条待合并、7 条已合并/关闭）。**各项指标整体健康**：Issue 关闭率为 40%，PR 进入合并流程的比例较高；安全与稳定性类 Issue 占比显著（多起安全漏洞与高优 Bug 已进入开发或修复阶段），功能开发与社区反馈双线并行。今日无新版本发布，项目处于**密集迭代期**，大量修复正在从 Issue 走向 PR 合并阶段。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日虽未有 PR 被合并的详细信息，但从关闭的 10 个 Issue 可窥见项目关键进展，尤其在**安全加固、架构整理与稳定性**方向：

- **[#4794](https://github.com/OpenHands/software-agent-sdk/issues/4794)（已关闭）**：`check_deprecations.py` 增强——新增对 Pydantic Field 级过期字段的检查能力，保证框架升级过程安全可控。
- **安全类里程碑关闭**：
  - **[#4677](https://github.com/OpenHands/software-agent-sdk/issues/4677)（已关闭）**：Secret masking 覆盖范围不足的问题——此前 13 个工具仅 1 个参与脱敏，现已关闭，说明该安全缺口已被修复或被更高优先级的方案吸收；
  - **[#4802](https://github.com/OpenHands/software-agent-sdk/issues/4802)（已关闭）**：`sanitized_env()` 泄漏 `OH_SECRET_KEY` 与 V1 session-key 至子进程的问题已修复，这是高优安全缺陷。
- **[#4695](https://github.com/OpenHands/software-agent-sdk/issues/4695)（已关闭）**：token deltas 不再重置空闲计时器导致长流式任务被回收的问题已修复，对长时间运行的 agent 任务至关重要。
- **[#4243](https://github.com/OpenHands/software-agent-sdk/issues/4243)（已关闭）**：Skills Management 的产品需求文档已敲定并关闭，意味着技能管理相关开发即将进入实施阶段。
- **[#4273](https://github.com/OpenHands/software-agent-sdk/issues/4273)（已关闭）**：企业级治理层（文件访问控制、命令白名单、成本预算、审计证据）的 Feature 请求。

整体来看，项目正在**从功能验证走向安全加固与架构整理**，在企业级部署、安全合规方向有明确的收敛动作。

---

## 4. 社区热点

### 讨论最活跃的 Issues（按评论数排序）

| Issue | 标题 | 评论数 | 👍 | 状态 |
|-------|------|--------|-----|------|
| [#4235](https://github.com/OpenHands/software-agent-sdk/issues/4235) | Add support for including screenshots in PRs | 19 | 2 | OPEN |
| [#4242](https://github.com/OpenHands/software-agent-sdk/issues/4242) | Frontmatter field for multiple repos | 16 | 0 | OPEN |
| [#4243](https://github.com/OpenHands/software-agent-sdk/issues/4243) | [PRD] Re-thinking Skills Management | 16 | 0 | CLOSED |
| [#4273](https://github.com/OpenHands/software-agent-sdk/issues/4273) | Governance layer for agent actions | 13 | 0 | CLOSED |
| [#3442](https://github.com/OpenHands/software-agent-sdk/issues/3442) | Intelligent Model Selection | 12 | 1 | OPEN |
| [#4241](https://github.com/OpenHands/software-agent-sdk/issues/4241) | Credential store integration | 10 | 0 | CLOSED |

### 热点分析

1. **#4235 [PR 截图支持]**（19 评论）——用户最强烈的诉求集中在**代码评审体验**：当 agent 生成 HTML/Web 内容后，PR 描述中没有可视化预览，评审者难以直观了解变更效果。这是开发体验类需求中呼声最高的一条，👍 数也最高，说明这是**高频痛点**。
2. **#4242 [多仓库支持]**（16 评论）——开发者希望在一个 task 中方便地指定多个仓库进行克隆，前端字段设计是讨论核心。该需求源自 OpenHands 主仓库 issue 拆分，说明多仓库工作流是真实场景。
3. **#3442 [智能模型选择]**（12 评论）——用户希望能自动为每个任务选择最合适的模型，而不必手动记忆各模型的价格与性能差异，属于**智能化/自动化方向**的典型需求。

### 讨论最活跃的 PRs

- **[#4815](https://github.com/OpenHands/software-agent-sdk/pull/4815)**（新增）：为 Claude Code 模型选择器添加 fable 模型选项，直接回应用户的 Issue。
- **[#4406](https://github.com/OpenHands/software-agent-sdk/pull/4406)**：MCP 1.x/2.x 兼容性 shim，解决依赖升级后浏览器工具无法构建的问题，说明用户环境中存在真实的依赖生态迁移压力。
- **[#4697](https://github.com/OpenHands/software-agent-sdk/pull/4697)**：EventLog 性能优化——使 append 操作耗时不再随会话长度线性增长。

---

## 5. Bug 与稳定性

### 高优先级（High）

| Issue | 标题 | 状态 | 已有修复 PR |
|-------|------|------|------------|
| [#4542](https://github.com/OpenHands/software-agent-sdk/issues/4542) | 全局 `agent_context.load_memory` 偏好仅在通过 agent_profile 启动对话时生效 | OPEN / ready-for-dev | 无 |
| [#4802](https://github.com/OpenHands/software-agent-sdk/issues/4802) | `sanitized_env()` 泄漏 `OH_SECRET_KEY` 和 V1 session-key 至 agent 子进程 | CLOSED | 已关闭（已修复） |
| [#4677](https://github.com/OpenHands/software-agent-sdk/issues/4677) | Secret masking 仅覆盖 13 个工具中的 1 个——模型可通过 file_editor、grep、glob 等读取原始密钥 | CLOSED | 已关闭（已修复或已吸收） |

> **#4677 特别说明**：即使已关闭，该 Issue 的描述本身就揭示了严重的安全隐患——模型可通过多种工具绕过脱敏读取明文密钥，建议关注后续是否有回归测试覆盖。

### 中优先级（Medium）

| Issue | 标题 | 状态 | 已有修复 PR |
|-------|------|------|------------|
| [#4810](https://github.com/OpenHands/software-agent-sdk/issues/4810) | `set_confirmation_policy`、`set_security_analyzer`、`update_secrets` 变更未持久化到 `meta.json` | OPEN / ready-for-dev | **[#4813](https://github.com/OpenHands/software-agent-sdk/pull/4813)** 已提交 |
| [#4811](https://github.com/OpenHands/software-agent-sdk/issues/4811) | fork 时通过向 `tags` 注入 title，导致数据混乱 | OPEN / ready-for-dev | **[#4814](https://github.com/OpenHands/software-agent-sdk/pull/4814)** 已提交 |
| [#4709](https://github.com/OpenHands/software-agent-sdk/issues/4709) | `AgentContext.current_datetime` 持久化在 settings.json，导致 prompt 中 `CURRENT_DATETIME` 过期 | OPEN / ready-for-dev | 无 |
| [#4695](https://github.com/OpenHands/software-agent-sdk/issues/4695) | token deltas 不再重置空闲计时器，长流式任务容器可能被回收 | CLOSED | 已修复 |

### 分析

- **高优 bug 有明显收敛**：#4677、#4802 均属安全高危，已在今日关闭，说明修复或重构已完成。
- **记忆系统不稳定**：#4542 与 #4709 分别指出**全局记忆偏好被忽略**和**时间戳过期**问题，表明对话持久化与记忆功能的实现仍有细节缺陷。
- **数据一致性问题**：#4810 与 #4811 均指向 `ConversationState` 与 `StoredConversation` 之间的同步缺陷，两个修复 PR 均已在今天提交（#4813、#4814），是另一个反映会话状态管理需要重构的信号。

---

## 6. 功能请求与路线图信号

### 短期可能落地的功能（已有实现 PR 或 ready-for-dev 标记）

| Issue | 功能 | 配套 PR | 状态说明 |
|-------|------|---------|---------|
| [#4812](https://github.com/OpenHands/software-agent-sdk/issues/4812) | ACP：Claude Code 模型选择器缺少 `claude-fable-5` | **[#4815](https://github.com/OpenHands/software-agent-sdk/pull/4815)** | PR 已提交，验证通过 |
| [#4235](https://github.com/OpenHands/software-agent-sdk/issues/4235) | PR 中支持截图预览 | 无 | backlog，社区呼声最高（👍2 / 评论19），但暂无实现 |
| [#4781](https://github.com/OpenHands/software-agent-sdk/issues/4781) | 服务端同后端子对话工具（不再依赖浏览器） | 无 | ready-for-dev |
| [#4643](https://github.com/OpenHands/software-agent-sdk/issues/4643) | agent-server 镜像可选能力集，参数化 provider 配置 | 无 | 步骤 0-2 已完成，持续进行中 |

### 中期路线图信号（roadmap 标签）

- **Skills 体系升级**：仍然是最活跃的路线图方向。涵盖[执行隔离与模型路由 Epic #2053](https://github.com/OpenHands/software-agent-sdk/issues/2053)、[Skills 管理 PRD #4243](https://github.com/OpenHands/software-agent-sdk/issues/4243)（今日关闭）等，预计后续大版本将重点发力。
- **对话克隆**：[#4244](https://github.com/OpenHands/software-agent-sdk/issues/4244) 提出克隆对话轨迹和工作区到新对话，已出 PRD。
- **镜像体积治理**：[#4643](https://github.com/OpenHands/software-agent-sdk/issues/4643) 指出 agent-server 镜像高达 1.64 GB，大部分能力部署时用不到，计划将镜像内容构建为可选的“契约”。

### 长期方向

- **智能模型选择**（[#3442](https://github.com/OpenHands/software-agent-sdk/issues/3442)，12 评论）：自动将每个任务路由到最合适的模型。
- **治理与合规层**（[#4273](https://github.com/OpenHands/software-agent-sdk/issues/4273)，已关闭）：文件访问控制、命令白名单、成本预算、审计证据等企业级需求已进入产品讨论流程。
- **凭据库集成**（[#4241](https://github.com/OpenHands/software-agent-sdk/issues/4241)，已关闭）：运行时自动登录私有资源。

---

## 7. 用户反馈摘要

### 高频痛点

1. **代码评审体验不足**（#4235）：“当 OpenHands 生成 HTML 或 Web 内容并创建 PR 时，PR 描述中无法包含运行应用的视觉表示，评审者难以快速了解变更内容。” —— 社区期待**可视化结果嵌入 PR** 的提升。
2. **技能/微代理管理界面落后**（#4243）：“OpenHands GUI 提供的‘微代理管理’界面无法胜任工作，严重落后于 AGENTS.md、Agent Skills 等新特性。” —— 用户对现有管理界面的**不满情绪明显**。
3. **安全与合规意识增强**（#4273、#4677）：企业级用户明确提出需要**治理层功能**，且对密钥管理漏洞给出了非常具体的技术细节，说明用户已开始在受监管环境中使用 OpenHands。

### 典型用户场景

- **多仓库任务处理**（#4242）：用户希望一次性指定多个代码库进行协作开发，现有 frontmatter 仅支持单个仓库。
- **派生对话**（#4244）：“我可能在某件事上工作过，但想基于之前的工作开启一个新的衍生对话”—— 用户在长任务迭代时**需要保留上下文的能力**。
- **私域资源访问**（#4241）：OpenHands 有时需要访问非公开资源，用户希望实现运行时自动登录，减少人工介入。

### 满意的地方

- 今日多个安全 Bug 关闭速度较快（#4677、#4802），说明团队**对安全问题响应及时**。
- 社区贡献热情高：大量 PR 来自外部贡献者（如 #4582、#4784、#4815 等），项目生态建设得到社区认可。

---

## 8. 待

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-09-02

## 今日速览

过去24小时项目整体活跃度极高：共 252 条 Issue 更新（其中 213 条关闭，关闭率达 84.5%），23 条 PR 更新（18 条已合并/关闭）。社区反馈处理效率显著，但同时也出现了多起 0.84.3/0.84.4 的回归问题，集中在 TUI 渲染、扩展加载和内存占用方面。修复 PR 跟进迅速，已有多个针对性的 fix 被合并，特别是围绕 Agent 生命周期和工具执行正确性的多项修复已进入主分支。项目健康度整体良好，维护者响应积极。

---

## 版本发布

过去24小时内无新版本发布。当前版本为 0.84.4，但有多个针对 0.84.3/0.84.4 回归的修复已通过 PR 合入主分支，预计将随下一版本发布。

---

## 项目进展

今日合并/关闭了多项重要 PR，核心聚焦于 Agent 生命周期正确性、TUI 行为修复和工具执行可靠性：

- **[#8937 fix(coding-agent): settle active turn before in-memory fork](https://github.com/earendil-works/pi/pull/8937)** — 修复内存 fork 时活动工具回合未结算导致 toolResult 落入错误会话、资源被错误清理的问题。这是对 #5886 类生命周期 bug 的进一步巩固。
- **[#8936 fix(agent): stop prepared tools after preflight abort](https://github.com/earendil-works/pi/pull/8936)** — 预检中止后不再启动已准备的并行工具调用，并补充了回归测试。
- **[#8957 Fix/wrap UI prompt context lose prototypes](https://github.com/earendil-works/pi/pull/8957)** — 对应 #8829，修复 `wrapUIPromptContext` 展开拷贝丢失原型方法的问题，保证类实例 UI 的兼容性。
- **[#8950 feat(coding-agent): keep theme markers visible](https://github.com/earendil-works/pi/pull/8950)** — 主题标记在 TUI 选择中保持可见，是 #8900 的后续补丁。
- **[#8966 fix(coding-agent): --provider without --model selects that provider's default; auth failures name the failing provider](https://github.com/earendil-works/pi/pull/8966)** — 修复 `--provider` 在未指定 `--model` 时被静默忽略的问题，并改进认证失败的错误信息。

此外，[#8946](https://github.com/earendil-works/pi/pull/8946) 修复了会话语境切换时扩展信任运行时可能被错误服务的问题；[#8627](https://github.com/earendil-works/pi/pull/8627) 让所有 cwd 敏感工具使用 `ctx.cwd`；[#8737](https://github.com/earendil-works/pi/pull/8737) 完善了 `NO_PROXY` 对子域名和 IPv6 的匹配。

---

## 社区热点

### 讨论热度最高

- **[#8584 TUI row corruption during streaming: assistant text rendered one word per line after long tool output](https://github.com/earendil-works/pi/issues/8584)**（26 条评论，👍 9，已关闭）
  用户报告流式输出时文本被错误地逐词换行，该问题在长工具输出后频繁出现，影响阅读体验。由于该 issue 已关闭，推测已有对应修复方案。

- **[#2870 [bug] Follow XDG Base Directory](https://github.com/earendil-works/pi/issues/2870)**（21 条评论，👍 54，已关闭）
  Linux 用户强烈要求遵循 XDG 目录规范，将配置/状态文件从 `$HOME` 移出。54 个 👍 表明这是社区最广泛认可的规范性问题之一，现已关闭。

- **[#7730 [bug] High CPU usage on Mac OS with long session](https://github.com/earendil-works/pi/issues/7730)**（14 条评论，👍 10，打开中）
  macOS 上长会话导致 CPU 占用 50–110%、内存 600–800MB，用户推测与会话长度/上下文大小相关，目前仍开放。

**诉求分析**：社区热点集中在两类——一是 TUI 渲染体验问题（换行、复制粘贴等），二是系统集成层面的规范性问题（XDG、资源占用）。高 👍 数的 issue 多为长期影响日常使用的质量缺陷，而非新功能需求。

---

## Bug 与稳定性

今日报告的 Bug 按严重程度排列：

### 🔴 严重（崩溃/数据损坏/进程终止）

- **[#8746 0.84.3 keeps reasoning in every message, sessions OOM at 20GB+ with subagents](https://github.com/earendil-works/pi/issues/8746)**（已关闭）
  0.84.3 下内核 OOM killer 两天内杀掉 5 个 21–27GB RSS 的进程，用户称 0.84.2 上 10 天无此问题。疑似回归，需重点排查。

- **[#8620 0.84.3 bundled CLI: every global extension fails with "Cannot find module"](https://github.com/earendil-works/pi/issues/8620)**（打开中）
  0.84.3 升级后，所有全局扩展因无法解析 `@earendil-works/pi-*` 包而加载失败，阻断依赖自定义扩展的用户。

- **[#8852 JSONL session opened twice in one process writes duplicate seq and corrupts the file](https://github.com/earendil-works/pi/issues/8852)**（已关闭）
  同一进程内打开同一会话文件两次时，两个实例共享相同 `nextSequence` 导致重复 seq，文件静默损坏。

### 🟠 中等（功能异常/回归）

- **[#7730 High CPU usage on Mac OS with long session](https://github.com/earendil-works/pi/issues/7730)**（打开中）
  长会话下 CPU 和内存持续高占用，影响 macOS 用户长时间使用。

- **[#8753 0.84.3 regression: reasoning_details echo deterministically degenerates Venice GLM reasoning](https://github.com/earendil-works/pi/issues/8753)**（已关闭）
  0.84.3 引入 `reasoning_details` 回显导致 Venice GLM 模型推理质量确定性退化，属模型兼容性回归。

- **[#6996 Gemini 3.x models fail during tool use due to missing thought_signature](https://github.com/earendil-works/pi/issues/6996)**（打开中）
  Gemini 3.x 工具调用缺少 `thought_signature` 导致请求失败，阻塞 Gemini 用户使用工具功能。

- **[#8134 Agent stops after first tool call when plain-HTTP provider reached through forward proxy](https://github.com/earendil-works/pi/issues/8134)**（打开中）
  0.84.0 起，通过正向代理访问 HTTP 提供商时，工具调用后挂起，影响特定网络环境的用户。

### 🟢 轻度（体验问题）

- **[#8806 TUI crashes on narrow terminals (80-88 cols)](https://github.com/earendil-works/pi/issues/8806)**（已关闭）
  窄终端启动时硬崩溃，渲染行超出宽度。已有修复 PR [#8898](https://github.com/earendil-works/pi/pull/8898)（SIGWINCH 自信号包装）合入。

- **[#8894 CLI value options consume the following flag when their value is missing](https://github.com/earendil-works/pi/issues/8894)**（已关闭）
  CLI 参数值缺失时误吞下一个 flag，已有对应修复 PR [#8966](https://github.com/earendil-works/pi/pull/8966)。

- **[#8673 TUI: soft line breaks render as hard breaks](https://github.com/earendil-works/pi/issues/8673)**（已关闭）
  Markdown 段落中单个 `\n` 被错误渲染为硬换行，已有对应修复 PR [#8950](https://github.com/earendil-works/pi/pull/8950) 及 [#8751](https://github.com/earendil-works/pi/issues/8751)。

**修复跟进情况**：上述 Bug 大多已有对应修复合入，包括 #8936、#8937、#8898、#8966 等，展示了团队快速响应能力。重点关注 #8746（OOM）和 #8620（扩展加载失败）两个仍待验证的回归问题，建议维护者优先确认修复版本。

---

## 功能请求与路线图信号

今日提交的功能请求中，以下方向值得关注：

- **[#8969 feat(coding-agent): add model and thinking overrides to subagent tool](https://github.com/earendil-works/pi/pull/8969)**（已关闭）
  允许调用者在派发子代理时指定模型和思考级别，支持“快速侦察模型 + 重量规划模型”的工作流组合。

- **[#8951 feat(coding-agent): hide headless sessions from the resume picker by default](https://github.com/earendil-works/pi/pull/8951)**（已关闭）
  RPC 模式、子代理等自动生成的会话不再污染 `/resume` 列表，改善交互体验。

- **[#8869 SDK: allow configuring the bash full-output directory](https://github.com/earendil-works/pi/issues/8869)**（已关闭）
  为 SDK 嵌入者提供 `fullOutputDirectory` 配置项，控制 bash 截断输出的落地位置，默认保持 `os.tmpdir()`。

- **[#8885 Ingest external entries in SessionManager](https://github.com/earendil-works/pi/issues/8885)**（已关闭）
  新增 `SessionManager.fromEntries()` 工厂方法，支持将已摄取条目注入 SessionManager，服务化/嵌入场景需要。

- **[#8834 Opt-in package namespace (pi.namespace) for skills and prompt templates](https://github.com/earendil-works/pi/issues/8834)**（已关闭）
  通过 `pi.namespace` 统一技能/提示模板的命名前缀，便于生态包避免命名冲突。

- **[#8665 Escape hatch to force OSC 8 hyperlinks on](https://github.com/earendil-works/pi/issues/8665)**（已关闭）
  提供 `PI_HYPERLINKS=1|0|auto` 环境变量，绕过终端能力检测失败的限制。

以上请求集中在**扩展生态**（命名空间、SDK 目录配置）、**服务化部署**（SessionManager 外部条目）和**可定制性**（子代理模型覆盖、超链接强制开启）三个方向，预计下个版本可能涵盖多数轻量级功能。

---

## 用户反馈摘要

从今日 Issue 评论中提炼的典型用户反馈：

- **对 0.84.3 回归不满**：多名用户明确表示升级后出现严重问题（OOM、扩展失效、推理退化），并强调“0.84.2 运行 10 天无任何问题”。这提示版本发布前应增加回归测试覆盖，特别是对长会话、扩展加载和模型兼容性的验证。
- **XDG 规范呼声高涨**（[#2870](https://github.com/earendil-works/pi/issues/2870)，54 👍）：Linux 用户很在意应用对系统目录规范的遵循，这反映了开发者用户群体对整洁、标准化的强烈偏好。
- **TUI 渲染细节影响阅读**（[#8584](https://github.com/earendil-works/pi/issues/8584)、[#8673](https://github.com/earendil-works/pi/issues/8673)）：终端用户对输出格式的敏感度很高，逐词换行、软换行被硬渲染等问题直接拉低使用体验。
- **授权与网络环境兼容性**（[#8468](https://github.com/earendil-works/pi/issues/8468)、[#8134](https://github.com/earendil-works/pi/issues/8134)）：部分用户通过代理或特殊网络环境使用，这类问题优先级虽不高但影响特定人群的可用性。
- **积极信号**：SDK 嵌入者（如 [@gabriel-imascono](https://github.com/gabriel-imascono)、[@y-nk](https://github.com/y-nk)）主动提出完善方案并愿意实现，说明 Pi 作为嵌入式 agent 引擎的开发者生态正在建立。

---

## 待处理积压

以下问题长期开放或等待维护者关注：

- **[#7730 High CPU usage on Mac OS with long session](https://github.com/earendil-works/pi/issues/7730)**（2026-08-06 创建，打开中，14 评论）
  macOS 高 CPU 问题已开放近一个月，影响面广，需持续跟进。

- **[#5886 AgentSession settlement/continuation and assistant-tail lifecycle bugs](https://github.com/earendil-works/pi/issues/5886)**（2026-06-18 创建，打开中，10 评论）
  会话结算与续接生命周期类 bug 的 meta issue，今日 #8937 的修复是该方向的补强，但 issue 本身仍未关闭，建议评估是否还有遗留子项。

- **[#6996 Gemini 3.x models fail during tool use due to missing thought_signature](https://github.com/earendil-works/pi/issues/6996)**（2026-07-23 创建，打开中）
  Gemini 3.x 工具调用问题，等待模型 API 适配。

- **[#8620 global extension fails with "Cannot find module @earendil-works/pi-coding-agent"](https://github.com/earendil-works/pi/issues/8620)**（2026-08-25 创建，打开中，8 评论）
  影响所有使用全局扩展的用户，建议优先处理。

- **[#8158 feat(coding-agent): upgrade Mermaid terminal rendering](https://github.com/earendil-works/pi/pull/8158)**（2026-08-15 创建，打开中）
  距离发起已两周，仍处于开放状态，需维护者评估合并意向。

---

> **总结**：Pi 项目处于高速迭代阶段，社区反馈活跃、修复效率高，但 0.84.3 回归教训提醒需加强版本发布前的回归测试，尤其是长会话稳定性、扩展加载和模型兼容性三个高风险区域。SDK/嵌入能力的需求正在上升，建议路线图向生态建设倾斜。整体健康度：**良好**，建议关注 OOM 与扩展加载两个待验证回归。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目日报（2026-09-02）

## 今日速览

过去 24 小时项目活跃度较高：共产生 **3 条 Issue 更新** 和 **54 条 PR 更新**，其中 14 条已合并/关闭，40 条仍处于待合并状态。原因为当前正处于 **reliability-2026** 与 **oss-foundations** 两大主题的密集迭代期，多个可靠性修复与基础设施 PR 被批量合入。Nexus 回调机制与批量状态重建（RebuildMutableState）成为近期开发焦点，同时一个涉及 SQL 连接池的严重稳定性 Issue（#11691）值得关注。整体来看，项目保持健康的推进节奏，但尚未发布新版本。

---

## 项目进展

今日有 **14 条 PR 被合并/关闭**，集中在以下方向：

### 已合入的修复
- **[PR #11839]** `[reliability-2026, release/1.32.0]` 修复 `FirstWorkflowTaskBackoff` 在 ContinueAsNew 后累积的问题：当工作流在 executionTime 前执行 ContinueAsNew，计算 lifetime 为负导致 backoff 不断累积。该修复阻止了这一异常叠加。
  https://github.com/temporalio/temporal/pull/11839
- **[PR #11800]** `[release/1.31.3, release/1.30.7, release/1.32.0]` 捕获 Visibility query converter 中的 panic，将其转为错误返回，避免 converter 内部的假设不成立时导致服务崩溃。该修复已同步到三个维护分支。
  https://github.com/temporalio/temporal/pull/11800
- **[PR #11564]** `[release/1.31.3, release/1.30.7, release/1.32.0]` 修复 Elasticsearch Visibility 分页过滤中的日期格式比较问题：datetime 序列化现在始终包含纳秒分量，同时补充了 ES 集成测试。
  https://github.com/temporalio/temporal/pull/11564
- **[PR #11409]** `[release/1.31.3, release/1.30.7]` 将 sqlparser 依赖从 commit 引用更新到 v0.1.0 tagged 版本（同 commit 无功能变更）。
  https://github.com/temporalio/temporal/pull/11409

### 新增基础设施
- **[PR #11887]** `[team/cgs-foundation, reliability-2026]` 新增**单集群被动复制测试框架**：将 active 工作流变更通过 versioned-transition 复制链路分流，仅持久化被动结果，并与 active 执行对比 task payload 与 trace。
  https://github.com/temporalio/temporal/pull/11887
- **[PR #11863]** `[reliability-2026]` 将 worker 命令的 `DispatchTimeout` 与 `MaxTaskAttempts` 从编译期常量改为动态配置项（`WorkerCommandsDispatchTimeout` / `WorkerCommandsMaxAttempts`），默认值不变（10s / 3 次），使这些参数可运行时调整而无需重新部署。
  https://github.com/temporalio/temporal/pull/11863

---

## 社区热点

今日讨论热度最高的条目为 **Issue #11691**，这是一条关于 SQL 会话刷新引发集群级故障的严重问题。虽然创建于 8 月 20 日，但 9 月 1 日仍在活跃讨论中（1 条评论）：

> **Issue #11691** — SQL session refresh 可能不可恢复地关闭连接池（`"sql: database is closed"`），导致 membership heartbeat 永久静默失败，集群表现为僵尸状态（表面 SERVING 但无法派发任务）。
> https://github.com/temporalio/temporal/issues/11691

**诉求分析**：用户期望 SQL 会话刷新机制要么能从自身引发的所有错误状态中恢复，要么在持续失败的 heartbeat 时主动升级（重建连接或终止进程交由 supervisor 重启）。当前该问题会导致集群"看起来健康，实际瘫痪"，对生产环境威胁较大。目前尚未看到关联的 fix PR。

另外，Nexus 相关话题占据大量 PR/Issue 篇幅（#11891、#11889、#11380、#11770、#11851），表明 **Nexus worker callbacks 功能正在进行系统性推进**，从协议识别、链路关联到超时容错均有覆盖。

---

## Bug 与稳定性

按严重程度排序：

| 严重程度 | 编号 | 描述 | 状态 |
|---------|------|------|------|
| **P0 严重** | [#11691](https://github.com/temporalio/temporal/issues/11691) | SQL 会话刷新导致连接池永久关闭，集群僵尸化（表面 SERVING 但无法调度任何任务），heartbeat 静默失败 | 无 fix PR，持续 12 天 |
| **P1 中等** | [#11841](https://github.com/temporalio/temporal/pull/11841) | 关闭期间存在竞态条件：poller 正在启动但尚未注册，导致 shutdown 请求漏掉该 poller，goroutine 无法被取消 | 有修复 PR（开放中），通过在检查 shutdown cache 前先注册 poll 解决 |
| **P1 中等** | [#11839](https://github.com/temporalio/temporal/pull/11839) | ContinueAsNew 导致 FirstWorkflowTaskBackoff 异常累积（若工作流在 executionTime 前继续执行，lifetime 为负） | ✅ 已合入 release/1.32.0 |
| **P2 一般** | [#11800](https://github.com/temporalio/temporal/pull/11800) | Visibility query converter 可能因 store 实现 bug 触发 panic | ✅ 已合入三个维护分支（1.31.3/1.30.7/1.32.0） |
| **P2 一般** | [#11564](https://github.com/temporalio/temporal/pull/11564) | Elasticsearch 分页过滤对不完整 datetime 比较结果不可预期（精度缺失导致漏查/错查） | ✅ 已合入 |
| **P2 一般** | [#11801](https://github.com/temporalio/temporal/pull/11801) | Visibility SQL 查询转换器多个解析缺陷：`ExecutionStatus IN (...)` 元组解析失败、负 double 比较报错（如 `CustomDouble > -1.5`）、非 bool 与 boolean 比较未报错 | 有修复 PR（开放中），未合入 |

### 值得注意的修复模式

多个 Bug 修复（#11800、#11564、#11409）同时标记了 `release/1.31.3`、`release/1.30.7`、`release/1.32.0` 三个维护分支，说明团队正在通过**批量热修复**方式维护旧版本线。这可能是为了配合下一轮 patch release。

---

## 功能请求与路线图信号

### 新提出的功能（Issue）

1. **[Issue #11891]** 将 `NexusHandler` 变体回调标记为 system payload（避免编码/解码问题）。这是 Nexus 回调功能链上的配套改动。
   https://github.com/temporalio/temporal/issues/11891

2. **[Issue #11889]** 为 NexusHandler 回调添加**双向链接**（backlinks），在回调派发时，在源操作的 callback 与 Nexus 操作派生的资源之间建立关联。
   https://github.com/temporalio/temporal/issues/11889

### 路线图信号

- **Nexus worker callbacks 功能链已成形**：#11380（识别 `commonpb.NexusHandler` 回调变体，feature/worker-callbacks 分支）+ #11891（system payload 标记）+ #11889（backlinks）+ #11770（Nexus 遥测关联）+ #11851（Nexus 派发超时容错）。该功能涉及协议层、可观测性、容错三方面，预计会随完整功能合入 main 分支。
- **reliability-2026 持续推进**：今日大量 PR 带有该标签，覆盖 replication 测试（#11887）、任务队列保护（#11858）、metrics 完善（#11885、#11840、#11884）等。
- **观察型指标增强**：#11885 新增 `task_alertable_attempt` metric 区分系统导致的重试循环 vs 用户导致的重试；#11884 新增 namespace 复制结果与端到端延迟指标。这些表明项目在**可观测性方面持续投入**。

---

## 用户反馈摘要

**来自 Issue #11691 的用户反馈（生产痛点）**：

> 用户 @enasikbst 报告的场景是：SQL session refresh 引发连接池关闭后，集群 membership heartbeat 静默失败，但集群对外仍报告 SERVING。这意味着**所有任务派发实际已不可用，但监控系统无法感知**。用户明确提出了两条期望：一是 SQL 会话刷新应能从自身引发的所有错误中恢复；二是若 heartbeat 持续失败应主动升级处理（重建连接或结束进程交由 supervisor 重启）。这是一个典型的"沉默故障"案例，对生产可靠性影响极大。

**间接反馈（从 PR 摘要推断）**：

- [#11851](https://github.com/temporalio/temporal/pull/11851) 的用户场景：当 worker 消失后，每次 `DispatchNexusTask` 尝试会阻塞 goroutine 长达 10s 超时，导致资源浪费。用户需要系统停止对 poller timeout（UpstreamTimeout）的重试，而保留对传输层错误的重试。
- [#11858](https://github.com/temporalio/temporal/pull/11858) 的场景：重复失败的 Task Queue 注册请求可能压垮 History 服务，需要一个带 TTL 的缓存来限制"too-many-deployments"错误的重复上报。

---

## 待处理积压

### 值得关注的长时未响应问题

| 编号 | 创建时间 | 持续天数 | 说明 |
|------|---------|---------|------|
| [#11691](https://github.com/temporalio/temporal/issues/11691) | 2026-08-20 | **13 天** | SQL 会话刷新导致集群僵尸化，P0 级稳定性问题，**暂无 fix PR 关联** |
| [#10095](https://github.com/temporalio/temporal/pull/10095) | 2026-04-28 | **127 天** | Mutation testing tool [WiP]，仍然开放但长期无实质性更新，最后一次更新为 9 月 1 日（可能仍在进行） |
| [#11380](https://github.com/temporalio/temporal/pull/11380) | 2026-07-31 | **33 天** | 识别 `NexusHandler` 回调变体，等待 feature/worker-callbacks 功能链整体完成后合入 main，属于预期内的等待 |

### 风险提示

> **长期无人响应的 PR**：#10095（mutation testing tool）从 4 月 28 日创建至今已超过 4 个月，虽然 9 月 1 日有更新活动，但整体进度缓慢。如果该工具是团队内部规划的一部分，建议明确里程碑；如果是社区贡献，则需要维护者回应是否考虑合入，避免社区贡献者长期悬空。

---

## 项目健康度总结

| 指标 | 数值 | 评估 |
|------|------|------|
| 24h Issue 处理量 | 3 条（0 关闭） | ⚠️ 偏少，且 1 条 P0 级 Issue 无处理进展 |
| 24h PR 处理量 | 54 条（14 关闭/合并） | ✅ 非常活跃 |
| 新版本发布 | 0 个 | 正常（可能在下周发布 patch release） |
| 维护分支覆盖 | 3 条（1.31.3/1.30.7/1.32.0） | ✅ 热修复覆盖面广 |
| 长期未响应 | 1 个 P0 Issue 持续 13 天 | ⚠️ 需要关注 |

**核心关注点**：`#11691` 作为 P0 级集群稳定性问题已存在 13 天且无 fix PR，建议维护者尽快确认是否为已知问题、是否有内部修复计划。其余方向（Nexus callbacks、reliability-2026、可观测性）均处于良性推进状态。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*