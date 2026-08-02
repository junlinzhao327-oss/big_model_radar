# OpenClaw 生态日报 2026-08-03

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-02 23:16 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-03

## 1. 今日速览

过去 24 小时项目活跃度极高：**500 条 Issue 更新**（新开/活跃 457，关闭 43）与 **500 条 PR 更新**（待合并 367，已合并/关闭 133），并发布 1 个新版本 `v2026.7.2-beta.7`。版本重点转向**状态安全与恢复**（SQLite 快照、隔离存储、schema 降级保护），但社区侧仍被多个长期未决的 P0/P1 稳定性问题困扰——特别是网关内存泄漏（#91588）、DeepSeek v4 Flash 静默回复失败（#116277，87 条评论）和崩溃循环断路器无法恢复（#115326）。维护者 `@steipete` 今日提交了密集的测试重构与生命周期修复系列 PR，表明项目正在系统性地清理技术债与跨模块一致性问题，但**高热度 bug 的修复 PR 覆盖率仍然偏低**，是当前健康度的主要短板。

## 2. 版本发布

### v2026.7.2-beta.7
- 链接：https://github.com/openclaw/openclaw/releases/tag/v2026.7.2-beta.7
- 核心主题：**State safety and recovery（状态安全与恢复）**
- 亮点内容（来自 release notes）：
  - **隔离存储（Quarantine Store）**：在主数据库损坏时保护持久化数据，避免故障扩散
  - **崩溃可恢复 SQLite 快照**：快照机制具备崩溃恢复能力，降低意外中断导致的数据损坏风险
  - **崩溃持久的文件系统发布**：文件系统发布操作具备崩溃持久性
  - **Schema 升级数据丢失拒绝**：拒绝可能导致数据丢失的 schema 升级路径
  - **回滚写入者快照恢复**：支持回滚场景下的写入者快照恢复

⚠️ **迁移注意事项**：该版本涉及 schema 升级防护逻辑，配合今日 Issue #115421（“Schema 降级恢复不得 quarantine/wipe 状态 DB”）可见，**旧版本打开新 schema 状态目录时存在数据被隔离/清空的风险**。升级前建议手动备份 `state/openclaw.sqlite`，并避免在升级后回退到旧版本运行。

## 3. 项目进展

今日关闭/合并的 PR 中，以下对项目实际推进最为关键：

| PR | 说明 | 意义 |
|---|---|---|
| [#118205 fix(auth): retain the selected account when migrating Codex sessions](https://github.com/openclaw/openclaw/pull/118205) | 修复多 ChatGPT OAuth 账户迁移时会话被静默切换到错误账户的问题（关闭 #58498） | 修复了一个影响账户隔离与使用量统计正确性的兼容性 bug |
| [#118251 fix(channels): recorded lifecycle facts outrank derived signals at the consumer boundary](https://github.com/openclaw/openclaw/pull/118251) | 在 gateway/consumer 边界让“已记录的生命周期事实”优先于“派生的弱信号” | 消除 Discord 等渠道在 blocked/stopped 等状态上的误判，是生命周期一致性系列的关键一步 |
| [#118280 fix(cron): normalize rounded schedule duration boundaries](https://github.com/openclaw/openclaw/pull/118280) | 修复 cron 列表/详情中出现 `in 60m`、`24h ago` 等不可能的相对时间 | 改善自动化运维体验 |
| [#118207 perf(gateway): reduce sessions.list read amplification under streaming load](https://github.com/openclaw/openclaw/pull/118207) | 将 `sessions.list` 在 8 并发流式场景下的延迟从 ~9.1s 降下来（针对 #118027） | 解决高并发下的读放大瓶颈，直接影响多用户网关体验 |
| [#118232 refactor(gateway): table-drive lazy method registration](https://github.com/openclaw/openclaw/pull/118232) | 将 gateway 方法策略与懒加载派发表驱动化 | 消除多文件同步维护导致的“有广告无路由”问题 |
| [#118256 chore(lint): resolve the 40 reserved baseline findings to zero-noise lint:all](https://github.com/openclaw/openclaw/pull/118256) | `pnpm lint:all` 达到零告警 | 提升代码库可维护性与 CI 信号质量 |

此外还有一批维护性重构（#118295、#118264、#118223、#118220、#118239、#114411、#118273、#118283、#118235），主要围绕**测试夹具去重**和**异步序列化规范化**。这批改动不直接改变用户行为，但显著降低了后续修复的回归风险与审查成本。总体而言，项目今日在“基础设施/内部一致性”上迈进了扎实的一步，但在用户可见的稳定性修复上进展有限。

## 4. 社区热点

今日讨论热度最高的 Issues 集中在**消息可靠性**与**资源管理**两个主题：

- **[#116277 DeepSeek v4 Flash silent reply failure（87 条评论）](https://github.com/openclaw/openclaw/issues/116277)** — P1，带 `diamond lobster` 最高热度评级，标签含 `impact:message-loss`。DeepSeek v4 Flash 在 Telegram 群聊中静默失败并回退为通用占位消息。87 条评论说明大量用户可能受此影响。当前**无新 fix PR**，需产品决策。
- **[#116201 Realtime voice work can retain unbounded provider and consult state（49 条评论）](https://github.com/openclaw/openclaw/issues/116201)** — 实时语音会话在慢/突发 provider 行为下无界保留 superseded consult 工作、provider 帧、pre-ready 音频等状态。目前 `needs-info`，等待更多信息。
- **[#115326 Crash-loop breaker suppresses Discord/WhatsApp permanently（25 条评论）](https://github.com/openclaw/openclaw/issues/115326)** — 崩溃循环断路器激活后永久抑制 Discord/WhatsApp

---

## 横向生态对比

# AI 智能体开源生态横向对比分析报告（2026-08-03）

## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态整体处于**从"功能扩张"转向"可靠性建设"的关键阶段**：各项目不约而同将状态持久化、崩溃恢复、流式传输稳定性与模型兼容性列为优先方向，OpenClaw 发布以"状态安全与恢复"为核心的 beta 版本，Pi 引入 pre-d

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报（2026-08-03）

## 1. 今日速览

过去 24 小时 OpenHands SDK 仓库保持高活跃度：30 条 Issue 更新（全部处于开放或活跃状态，无关闭），11 条 PR 更新（9 条待合并，2 条已关闭/合并），无新版本发布。社区讨论集中在 ACP 集成、LLM 初始化安全、以及并发/可靠性问题上。值得关注的是，安全审计类 Issue 占比较高（如 CRITICAL 级 egress 风险、凭据泄漏等），但对应 fix PR 尚不多见。整体而言，项目功能迭代仍在推进，但 Bug 积压与安全加固压力明显，维护者需要优先处理高风险项。

## 3. 项目进展

过去 24 小时有 2 个 PR 被关闭/合并，另有 9 个 PR 处于待合并状态，显示核心逻辑修复与代码清理工作仍在持续。

**已关闭/合并：**

- [PR #4167 fix(llm): resolve chat-option capabilities from the canonical model name](https://github.com/OpenHands/software-agent-sdk/pull/4167)  
  修复了代理模型无法正确启用 thinking、错误保留 temperature 的问题。该 PR 已关闭，说明 LLM 能力检测逻辑得到了一次关键修正。
- [PR #4330 Feat/task scope conflict preflight](https://github.com/OpenHands/software-agent-sdk/pull/4330)  
  该 PR 本身为 draft 状态，现已关闭，可能暂未进入实施阶段。

**值得关注的待合并 PR：**

- [PR #4282 Security: Unvalidated Workspace Directory in VSCode URL Endpoint](https://github.com/OpenHands/software-agent-sdk/pull/4282) —— 修复 `/vscode/url` 端点未校验 `workspace_dir` 的安全问题，属于中危安全修复。
- [PR #4166 fix(conversation): persist secrets added via update_secrets](https://github.com/OpenHands/software-agent-sdk/pull/4166) —— 修复 secrets 更新后未持久化、重启丢失的问题。
- [PR #4164 fix(grep): honor brace alternation in the include filter](https://github.com/OpenHands/software-agent-sdk/pull/4164) —— 修复 `grep` include 过滤器中 `*.{ts,tsx}` 这类 brace 模式失效的问题。
- [PR #4159 refactor(sdk): centralize LLM call context](https://github.com/OpenHands/software-agent-sdk/pull/4159) —— 集中化 LLM 调用上下文，属于架构级重构。
- [PR #4328 chore(sdk): deprecate AgentBase.model_dump_succint](https://github.com/OpenHands/software-agent-sdk/pull/4328) —— 配合 #4224 清理工作，将 `model_dump_succint` 标记为弃用而非直接删除，兼顾 API 兼容性。

这些 PR 主要集中在稳定性修复、安全加固与内部代码整理，尚未看到大型新功能合并。

## 4. 社区热点

过去 24 小时评论最活跃的 Issue 反映了社区对 ACP 协议兼容性、模型兼容性和并发控制的关注：

- [#4019 [bug] ACP profiles inject workspace project skills that duplicate what the ACP CLI already ingests (AGENTS.md)](https://github.com/OpenHands/software-agent-sdk/issues/4019) — 15 条评论  
  讨论 ACP profile 与 ACP CLI 重复注入 AGENTS.md 技能的问题。用户担心技能重复加载可能导致上下文混乱和 token 浪费，属于集成设计层面的争议。

- [#4248 [bug] Missing required parameters for function 'execute_bash': {'security_risk'}](https://github.com/OpenHands/software-agent-sdk/issues/4248) — 13 条评论  
  使用 `deepseek-reasoner` 模型时报错缺少 `security_risk` 参数。说明部分模型不会按预期输出额外字段，SDK 的鲁棒性需要改进。

- [#3992 [bug] Asymmetric handling of content-without-tool-call responses terminates agents driven by weaker/local models](https://github.com/OpenHands/software-agent-sdk/issues/3992) — 12 条评论  
  指出 `ResponseDispatchMixin` 对“无工具调用的纯内容响应”处理不对称，容易导致本地小模型驱动 Agent 时提前终止。本地模型用户对此敏感。

- [#4063 [bug] max_concurrent_runs does not limit native async conversations](https://github.com/OpenHands/software-agent-sdk/issues/4063) — 12 条评论  
  `max_concurrent_runs` 配置只对同步线程池生效，原生异步路径不受控。这触及部署容量管理，运维侧关注度较高。

- [#4080 [bug] One unregistered event kind fails the entire conversation load](https://github.com/OpenHands/software-agent-sdk/issues/4080) — 11 条评论  
  单个事件反序列化失败会导致整个会话无法加载，用户认为应当降级跳过而不是整体失败。社区普遍支持 per-event 容错。

这些热点 Issue 的共同诉求是：**增强对非主流模型、异常数据和异步场景的容错能力**。

## 5. Bug 与稳定性

按严重程度列出今日活跃的 Bug（含安全审计类）：

**CRITICAL**

- [#4261 OpenHands Fork Audit - CRITICAL: RemoteWorkspace host validation gap enables unvalidated egress](https://github.com/OpenHands/software-agent-sdk/issues/4261)  
  远程工作区未校验目标主机，可能导致绕开隔离策略的任意 egress。暂无对应 fix PR。

**HIGH**

- [#4263 OpenHands Fork Audit - HIGH: get_litellm_model_info makes unvalidated httpx.get call at LLM init](https://github.com/OpenHands/software-agent-sdk/issues/4263)  
  LLM 初始化时发起未经验证的 HTTP 请求，存在潜在数据外泄风险。暂无 fix PR。
- [#4157 [security] LLMSecurityAnalyzer trusts

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-03

## 今日速览
过去 24 小时项目活跃度较高：共产生 32 条 Issue 更新（其中 28 条关闭）与 19 条 PR 更新（14 条合并/关闭），无新版本发布。社区关注焦点集中在 compaction 机制的可靠性上（#6879、#7020 等），多位用户反馈上下文超限、compaction 触发不及时等问题，并有对应 PR #7498 尝试修复。此外，今日合并了 MiniMax 视频生成、Claude Code 技能兼容等多项新功能，同时出现了 TUI 渲染器切换 PR 被合并后又快速回滚的反复，反映项目处于快速迭代中。

- 活跃度评估：**高**（大量 Issue 关闭 + 功能 PR 合并，但存在回滚争议）
- 风险提示：compaction 相关 Bug 连续多日占据社区热点，且尚未有合入修复

---

## 版本发布
无新版本发布（最新 Releases 为空）。

---

## 项目进展
今日（截至 2026-08-02 数据）共有 14 条 PR 被合并或关闭，以下为重要变更：

### ✨ 新功能
- **feat(ai): add MiniMax video generation**（#7467，已合并）— 新增 MiniMax 视频生成支持，包含 v1/v2 端点、任务查询与下载处理。扩展了 Pi 在多模态内容生成方面的能力。
- **feat(ai): add LLM Gateway provider with API key and OAuth login**（#7480，已合并）— 新增 LLM Gateway（OpenRouter 风格路由器）作为内置 openai-completions 提供方，包含约 151 个模型的目录拉取能力。
- **feat(agent,coding-agent): accept Claude Code skill frontmatter**（#7468，已合并）— 使两个 skill 加载器兼容 Claude Code 的 SKILL.md frontmatter 格式，提升生态互操作性。
- **feat(coding-agent): opt-in pre-dispatch durability barrier**（#7466，已合并）— 为 embedder 提供可选的一致性保障，解决"provider 调用前崩溃导致无法区分是否已计费"的问题。
- **feat(agent): compose session storage through repositories**（#7478）与 **feat(agent): simplify session storage composition**（#7455）— 对会话存储层进行抽象简化，为后续 server 会话持久化铺路。
- **feat(coding-agent): add server session backend**（#7396，待合并）— 为 PiServer 增加 JSONL 持久化会话后端（含跨进程锁、崩溃恢复）。

### 🐛 修复
- **fix(coding-agent): increase connection attempt timeout**（#7435，已合并）— 将 Undici 连接超时从 250ms 提升至 2s，修复 Fireworks 在高延迟路由上快速失败的问题。
- **fix(coding-agent): respect shellPath in minimal mode example**（#7488，已合并）— 修复 minimal-mode 扩展示例忽略 settings.json 中 shellPath 的问题（对应 Issue #7489）。
- **fix(ai): retry transient provider errors in Google adapters**（#7471，已合并）— Google Vertex/Gemini 适配器在拿到首 token 前遇到 429/5xx 时将不再直接终止 agent 线程。

### ⚠️ 异常信号
- **feat(tui): add switchable terminal renderers**（#7440）当日合并后被 **Revert**（#7473，已合并）撤销 — 该 PR 本意是支持运行时切换 TUI 渲染器，但因稳定性风险被回滚。项目在"推进新渲染架构"与"保持稳定"之间做出了保守选择。

**整体评估**：项目在 AI 供应商接入（MiniMax、LLM Gateway）、Google 适配器稳定性、会话存储重构方面有实质推进；compaction 问题尚未有合入修复，但 #7498 的 PR 已被提出，正处于讨论期。

---

## 社区热点
### 1. [Bug] auto-compaction never triggers after context grows past 100%（#6879，OPEN）
- **热度**：10 条评论 / 10 👍（同期最高）
- **诉求**：用户在一个 2 小时+ 的 agent 回合中，上下文占用超过 100% 后 compaction 仍未触发，直到 API 在 373k tokens 时拒绝请求才被迫触发。用户希望"在每次 agent 操作后都应检查上下文用量"。
- **链接**：https://github.com/earendil-works/pi/issues/6879

### 2. [Bug] Sometimes Pi doesn't continue after compaction（#7020，OPEN）
- **热度**：7 条评论
- **诉求**：对长时间运行的协调型（coordinator）会话，compaction 后 Pi 有时无法继续执行，疑似 compaction 边界条件的缺陷。该问题与 #6879 同属"compaction 可靠性"主题。
- **链接**：https://github.com/earendil-works/pi/issues/7020

### 3. [PR] fix(coding-agent): defer idle compaction until next prompt（#7498，OPEN）
- **热度**：围绕 #6879 提出的修复方案 — 将"空闲压缩"推迟到下次用户提示之后，避免不必要的 token 消耗与上下文边界副作用。作者自称"非修复但相关"。
- **链接**：https://github.com/earendil-works/pi/pull/7498

**趋势判断**：compaction 在当前 agent 工作流中承担关键角色，但行为不够可预测，已经连续造成多起用户困扰（#6879、#7020、#7492、#7413）。社区正在积极探索修复方向，但尚未形成定论。

---

## Bug 与稳定性
按严重程度排列：

| 严重度 | Issue | 描述 | Fix PR |
|--------|-------|------|--------|
| 🔴 高 | #6879 | compaction 在上下文超限（>100%）后不触发，直到 provider 拒绝请求；造成 token 浪费与任务中断 | #7498（开放） |
| 🔴 高 | #7020 | compaction 完成后有时不继续后续执行，长会话高发 | 无 |
| 🟠 中 | #7062 | OpenAI Completions 适配器不支持数组格式的 delta.content 及缺失 finish_reason 的响应（影响 Databricks 部分模型） | 无 |
| 🟠 中 | #7486 | WezTerm 下开启硬件光标后，光标在 "Working..." 状态跳动（由 #5200 的 workaround 引入） | 无 |
| 🟠 中 | #7490 | WezTerm 中中文 IME 候选窗闪烁/跳动/残影（codex 正常） | 无 |
| 🟠 中 | #7323 | `pi update --models` 单次瞬时网络故障导致整个目录刷新失败（无重试） | 无 |
| 🟡 低 | #7497 | sessions 目录下的符号链接目录被 listSessions 静默忽略，pi-web 看不到对应会话 | 无 |
| 🟡 低 | #7499 | auth.json 若含 UTF-8 BOM，所有凭据被静默忽略且无法保存新 key | 无 |
| 🟡 低 | #7402 / #7481 / #7484 / #7479 | 差分渲染器宽度计数问题导致孟加拉文粘贴后行重复；WezTerm 中 kitty 图片在滚动后被逐步擦除（#7481 已有 fix PR #7482，已合并）；扩展发送的斜杠命令被当作文本消息；Tab 补全斜杠命令后参数补全失效 | #7482 ✅ |

**亮点**：今日有 2 个修复已合入（#7435 Fireworks 超时、#7488 shellPath、#7482 WezTerm 图片问题、#7471 Google 重试），整体 Bug 修复速度较快；但 compaction 相关的高严重度问题仍需关注。

---

## 功能请求与路线图信号
以下信号结合 Issue 讨论与 PR 状态，推测可能进入下一版本：

| 功能请求 | 相关 Issue/PR | 状态判断 |
|----------|---------------|----------|
| **MiniMax 视频生成**（text-to-video） | PR #7467（已合并） | ✅ 已进入主线 |
| **LLM Gateway provider**（OpenRouter 风格） | PR #7480（已合并） | ✅ 已进入主线 |
| **Claude Code 技能兼容**（SKILL.md frontmatter） | PR #7468（已合并） | ✅ 已进入主线 |
| **askWithFrozenContext()** — 插件/扩展可在冻结当前上下文基础上发起额外 LLM 调用（如 review-with-variants） | Issue #7500 | 设计提案，社区有共鸣，存在短期实现可能 |
| **/scoped-models 中支持 thinking level 选择** | Issue #7487 | 功能明确且改动不大，可能进入后续小版本 |
| **--exclude-extensions / -xe** 按需跳过扩展加载 | Issue #7475 | 用户明确愿意贡献代码，维护者回应后有望快速落地 |
| **AI_AGENT=pi 环境变量**（子进程身份标识，解决 #7132） | PR #7493（开放） | 已获得 lgtm，等待合入 |
| **调度/压缩语义改进** — compaction 取消原因透出（#7492）、空闲压缩延迟（PR #7498） | #7492 / #7498 | 正在讨论核心机制，是当前最大路线图信号 |

---

## 用户反馈摘要
从今日 Issue 评论中可提炼以下真实用户视角：

- **长会话用户对 compaction 的可靠性已产生不信任**："我的会话是协调型长跑，不是单问题聚焦型——这种场景下 compaction 的瑕疵暴露得更多"（来自 #7020）。说明当前 compaction 逻辑更适合短会话模式，对持续型 agent 工作负载支撑不足。
- **Windows 用户的编辑器/终端兼容性困扰集中爆发**：auth.json 的 BOM 问题（#7499）、minimal-mode 忽略 shellPath 回退到 WSL（#7489）、WezTerm 的 IME/光标/图片渲染问题（#7486、#7490、#7481）均来自 Windows 使用者，暗示该平台测试覆盖仍需加强。
- **用户开始对比同类工具**："codex 在同样的 WezTerm 环境下完全正常"（#7490）——这种对比对 Pi 的终端体验口碑有直接影响。
- **对"模型目录更新"这类基础体验也有抱怨**：`pi update --models` 遇到一次瞬时网络故障就整体失败，用户希望有重试机制（#7323）。
- **扩展开发者的反馈**：扩展加载时每个扩展单独创建 jiti 实例且串行加载带来启动性能开销（#7483）；工具 schema 在同一请求中被序列化两次且无法关闭（#7485）——这些反馈指向扩展生态基础设施的优化空间。

---

## 待处理积压
以下为长时间未关闭/未响应的重要 Issue 与 PR，建议维护者关注：

| 项目 | 创建时间 | 天数 | 说明 |
|------|----------|------|------|
| #6879 [OPEN] compaction 触发机制缺陷 | 2026-07-20 | 14 天 | 最热 Issue（10👍），仍无合入修复，仅 #7498 在讨论中 |
| #7020 [OPEN] compaction 后不继续执行 | 2026-07-23 | 11 天 | 高严重度，无修复 PR |
| #7062 [OPEN] Databricks 非标准流式响应兼容 | 2026-07-24 | 10 天 | 影响 Qwen3 / gpt-oss 用户，有待分类/认领 |
| #7321 [OPEN] Termux 多行粘贴被回车拆散 | 2026-07-30 | 4 天 | 终端兼容性 Bug，面向移动端用户 |
| PR #7330 [OPEN] 工具返回图片未统一走 processImage 路径 | 2026-07-30 | 4 天 | 修复方案已就绪，等待 review |
| PR #7396 [OPEN] server 会话后端 | 2026-07-31 | 3 天 | 功能完整，涉及面大，需重点 review |
| PR #7498 [OPEN] 延迟空闲压缩 | 2026-08-02 | 1 天 | 针对 #6879，需要维护者给出明确态度 |

**提醒**：#6879 已持续两周且社区呼声最高，建议优先推动相关修复（#7498 或替代方案）进入主线，以缓解用户对 compaction 机制的信任危机。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-03

## 1. 今日速览

过去 24 小时内，LiteLLM 项目保持了极高的社区活跃度：**64 条 Issue 更新**（新开/活跃 49 条，关闭 15 条）与 **137 条 PR 更新**（待合并 104 条，合并/关闭 33 条）双双处于高位。无新版本发布。值得关注的是，**104 条待合并 PR 是合并队列的 3 倍以上**，维护者合并速度可能成为项目迭代的瓶颈。今日新增 Bug 聚焦于流式传输兼容性（Amazon Nova zstd 解码失败、Bedrock Converse 参数静默丢弃）与预算/路由正确性问题；同时，长期悬置的 UI 深色模式需求（#10177）依旧以 61 条评论、69 个 👍 稳居社区热度榜首。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日共有 **33 个 PR 被合并/关闭**，结合待合并队列的构成，可看出项目目前在以下几个方向持续迈进：

- **Provider 生态扩展**：[#35613](https://github.com/BerriAI/litellm/pull/35613) 为 Azure AI Foundry 上的 Fireworks 模型（`azure_ai/FW-*`）补齐价格映射，修复了这些模型花费追踪为 0 或错误的问题（关联 issue #26618）；[#35610](https://github.com/BerriAI/litellm/pull/35610) 新增 AvalAI 作为 JSON 配置的 OpenAI 兼容 provider，继续拓宽网关覆盖范围。
- **Realtime API 完善**：[#35600](https://github.com/BerriAI/litellm/pull/35600) 将实时翻译端点提升为一等公民，新增 WebSocket 与 WebRTC 代理路径，并集成 OpenAI SDK 2.52 以支持最新转录模型，同时修补了 WebRTC 直连绕过花费追踪与预算执行的漏洞。
- **流式传输稳定性修复**：[#35601](https://github.com/BerriAI/litellm/pull/35601) 从默认 `Accept-Encoding` 头中移除 `zstd`，直击 `amazon_nova` 流式调用 100% 失败的问题（见 Bug 章节 #35589）。
- **权限与安全修复**：[#35132](https://github.com/BerriAI/litellm/pull/35132) 允许非管理员在安全预设前提下更新 key 类型（修复 #34975），将管理性操作与普通 key 编辑解耦。
- **RAG 与 MCP 能力补强**：[#35607](https://github.com/BerriAI/litellm/pull/35607) 修复 `/v1/rag/query` 中 vector_store_registry 凭证解析问题；[#33444](https://github.com/BerriAI/litellm/pull/33444) 为 `mcp_tool_search` 引入可配置默认 `top_k`，含 DB 迁移支持。
- **长期挂起 PR 有进展**：OIDC 客户端元数据宣告提交（[#35234](https://github.com/BerriAI/litellm/pull/35234)）、Grok 对话缓存头支持（[#34706](https://github.com/BerriAI/litellm/pull/34706)）、Exa `outputSchema` 透传（[#35032](https://github.com/BerriAI/litellm/pull/35032)）等均在持续更新中。

## 4. 社区热点

- **[#10177 [Feature]: Dark Mode](https://github.com/BerriAI/litellm/issues/10177)** — ⭐ 今日最热 Issue，累计 61 条评论、69 个 👍，创建于 2025 年 4 月至今仍被持续讨论。用户以 "I'm going blind" 直白表达了对深色主题的迫切需求，核心诉求围绕管理面板（Admin UI）的可用性与视觉健康。该需求长期无官方回应，社区关注度持续积累。
- **[#35589 amazon_nova streaming fails 100%](https://github.com/BerriAI/litellm/issues/35589)** — 新提交的严重 Bug，3 条评论，直指 Amazon Nova 流式调用 100% 失败，根因定位到 httpx zstd decoder 对多帧 SSE 复用已结束的 decompressobj。已有对应修复 PR（[#35601](https://github.com/BerriAI/litellm/pull/35601)），值得称赞的是从问题报告到修复 PR 的响应速度极快。
- **[#33984 LiteLLM Cloudflare adapter 不翻译 OpenAI content-part 消息](https://github.com/BerriAI/litellm/issues/33984)** — 5 条评论。Cloudflare Workers AI 适配器未将 OpenAI 格式的 content-part 消息正确翻译为 Cloudflare 期望格式，影响以 LiteLLM 作为网关接入 Cloudflare 的用户。
- **[#34105 Bedrock Converse 静默丢弃 reasoning_effort](https://github.com/BerriAI/litellm/issues/34105)** — 4 条评论。当对非 Anthropic/Nova2/GPT-OSS 的 Bedrock 模型（如 Qwen3）传入 `reasoning_effort` 参数时被静默丢弃，无任何报错提示，属于不易察觉的"静默错误"类型。

## 5. Bug 与稳定性

**高严重度**

- **[#35589 Amazon Nova 流式调用 100% 失败](https://github.com/BerriAI/litellm/issues/35589)** — `amazon_nova` 全量流式请求失败，非流式正常。根因是 `httpx.DecodingError: cannot use a decompressobj multiple times`，由 zstd 多帧 SSE 解码冲突导致。**已有修复 PR：** [#35601](https://github.com/BerriAI/litellm/pull/35601)（停止默认声明 zstd 支持）。
- **[#35577 新 DB 部署在 Router upsert 时被丢弃](https://github.com/BerriAI/litellm/issues/35577)** — 通过 `Router.upsert_deployment()` 首次加载的 DB 后端部署会从代理的内存路由中消失，可能导致新配置的模型无法被路由到。
- **[#35524 预算预留被跳过](https://github.com/BerriAI/litellm/issues/35524)** — 当请求成本无法预估正向最大值时，乐观预算预留逻辑直接返回且不预留任何额度，使并发超支风险暴露在成本无法预估的路由/模型上。

**中严重度**

- **[#27038 disable_end_user_cost_tracking 未生效](https://github.com/BerriAI/litellm/issues/27038)** — 配置 `disable_end_user_cost_tracking: true` 后，`SpendLogs.end_user` 仍被写入、`DailyEndUserSpend` 仍更新，成本追踪开关形同虚设。
- **[#34105 Bedrock reasoning_effort 静默丢弃](https://github.com/BerriAI/litellm/issues/34105)** — 非 Anthropic/Nova2/GPT-OSS 模型（如 Qwen3）上传入 `reasoning_effort` 被无提示丢弃。
- **[#35460 MCPServerManager 重复探测](https://github.com/BerriAI/litellm/issues/35460)** — 对不支持 `list_prompts`/`list_resources` 的 MCP 服务器，每次聚合 `/mcp` 请求都会重复探测，产生无谓开销与日志噪音。
- **[#35582 aresponses 静默丢弃 stop 参数](https://github.com/BerriAI/litellm/issues/35582)**（已关闭）— `stop` 参数在 `aresponses` 中被静默过滤，不报错也不警告，容易误导调用方。
- **[#26547 post_call guardrail 丢弃流式纯文本响应](https://github.com/BerriAI/litellm/issues/26547)**（已关闭）— `tool_permission` 守卫的 `post_call` 模式在流式请求下会静默丢弃纯文本响应。

**低严重度 / 体验类**

- [#34105](https://github.com/BerriAI/litellm/issues/34105) 以外，[#35177](https://github.com/BerriAI/litellm/issues/35177) 报告 `user_url_allowed_hosts` 在 `general_settings` 下生效但 `litellm_settings` 下不生效的配置行为不一致问题。
- [#35543](https://github.com/BerriAI/litellm/issues/35543) 报告 `async_pre_call_hook` 返回 `str` 的文档承诺在 `/v1/chat/completions` 上不可达（call_type 为 `acompletion`），文档与实现存在偏差。

## 6. 功能请求与路线图信号

- **Dark Mode（[#10177](https://github.com/BerriAI/litellm/issues/10177)）**：69 👍 的强需求信号，横跨 15 个月仍在发酵。考虑到该项目已有一个活跃的 UI 团队（今日多条 UI 修复 PR），这一需求有望被纳入后续 UI 改版计划。
- **OpenAI 最新音频模型支持（[#35600](https://github.com/BerriAI/litellm/pull/35600)）**：PR 已就绪，说明项目正在紧跟 OpenAI Realtime API 演进，将 translation 端点与新的转录模型纳入一等支持。
- **原生 OIDC 客户端元数据宣告（[#35234](https://github.com/BerriAI/litellm/pull/35234)）**：为 headless 机器上的 `lite login` 提供设备码登录路径，并让 IdP 会话对 LiteLLM 可见，属于企业级 SSO 体验的补全。
- **Grok 对话缓存（[#34706](https://github.com/BerriAI/litellm/pull/34706)）**：为 xAI 模型增加 `x_grok_conv_id` 参数与 HTTP 头映射，满足需要显式控制对话亲和性的用户。
- **模型目录更新**：[#26765](https://github.com/BerriAI/litellm/issues/26765) 请求新增 `azure_ai/gpt-image-2` 定价条目；[#27094](https://github.com/BerriAI/litellm/issues/27094) 指出 AI21 模型列表过时，仅剩 `jamba-large-1.7` 与 `jamba-mini-2` 两个模型，建议及时清理价格清单。
- **新 Provider 信号**：[#35610](https://github.com/BerriAI/litellm

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-03

## 1. 今日速览

过去24小时 Temporal 项目保持中高活跃度：无新 Issue 产生，但 PR 活动密集（共 15 条），其中 5 条已合并/关闭、10 条仍在开放待审。活动集中于 **SAA（Sync Activity）功能完善**、**1.32.0 发布准备**、以及多个**可靠性修复**（retry jitter 失效、heartbeat checkpoint 丢失、logger tags 丢失、连接池缺失）。值得注意，SAA 相关的 PR 出现多次迭代（#11379 → #11396 为同一功能的修正版本；#11391 → #11393 为 API 变更的替代版本），说明该功能正处于快速打磨阶段。无新版本发布，但 1.32.0 发布分支已开始准备。

- 活跃度评估：⭐⭐⭐⭐（PR 密集，Issue 侧平静）
- 核心主题：SAA 功能迭代、发布准备、bug 修复


## 2. 版本发布

**无正式版本发布。**

但 [#11395 [CLOSED] 1.32.0: Prepare release branch](https://github.com/temporalio/temporal/pull/11395) 已合并/关闭，意味着 **v1.32.0 的发布流程已正式启动**。该 PR 主要负责覆盖 governance 文件与更新依赖，通常标志着发布前期的准备阶段。预期未来 1–2 周内会有正式 RC 或 release 版本出炉。

## 3. 项目进展

今日共 5 条 PR 被合并/关闭，按重要性排序：

| PR | 说明 | 意义 |
|---|---|---|
| [#11395 Prepare 1.32.0 release branch](https://github.com/temporalio/temporal/pull/11395) | 发布分支准备 | 1.32.0 版本进入发布倒计时 |
| [#11379 Record SAA task schedule-to-start latency](https://github.com/temporalio/temporal/pull/11379) | 为 SAA 任务增加 schedule-to-start 延迟指标 | SAA 可观测性补全第一步（后由 #11396 修正替代） |
| [#11375 Port SAA/WFA CompleteById tests to declarative framework](https://github.com/temporalio/temporal/pull/11375) | 将 CompleteById 测试迁移至声明式框架 | 测试体系现代化，减少 225 行代码并增强断言能力 |
| [#11391 Drop reset_attempts/reset_heartbeat from UnpauseActivityExecution](https://github.com/temporalio/temporal/pull/11391) | API 字段移除 | 对应 temporalio/api#846 的 API 变更（已被 #11393 新版本替代） |
| [#11349 11321 suggestion](https://github.com/temporalio/temporal/pull/11349) | 未注明内容 | 已关闭，未见具体说明 |

**整体推进方向**：SAA 是可观测性指标与测试基础设施的完善（#11375/#11379）；API 在向更精简的方向演进（#11391）；发布流程开始运转（#11395）。

## 4. 社区热点

今日数据中无新增 Issue，因此活跃焦点完全集中在 PR 展开的领域上。最值得关注的讨论群组是 **SAA（Sync Activity）相关的一系列 PR**，由 @dandavison 主导发起：

- [#11396 Record SAA task schedule-to-start latency（开放）](https://github.com/temporalio/temporal/pull/11396)
- [#11363 Persist heartbeat checkpoint data on failure（开放）](https://github.com/temporalio/temporal/pull/11363)
- [#11375 Port CompleteById tests（已关闭）](https://github.com/temporalio/temporal/pull/11375)

**诉求分析**：SAA 是 Temporal 近期重点推进的新功能，社区/维护团队正在快速补齐它的可观测性（latency 指标）、数据可靠性（heartbeat 持久化）和测试覆盖。三日内同一作者连续提交 6 条 SAA 相关 PR 且反复迭代（#11379 → #11396），说明该功能仍在快速演进、尚未对外完全稳定。

## 5. Bug 与稳定性

今日无新 Bug Issue 报告，但多个开放 PR 揭示了现存缺陷，按严重程度排列：

| 严重度 | 问题 | 对应 PR | 状态 |
|---|---|---|---|
| 高 | **Retry jitter 完全失效**：`addJitter` 因整数运算截断，导致 `WithJitter(0.1)` 下 2s 的退避永远是 2.000s，无法分散 | [#11397 Fix constant/error-dependent retry jitter](https://github.com/temporalio/temporal/pull/11397) | ✅ 已有 fix PR |
| 高 | **SAA 活动失败时 heartbeat checkpoint 数据未持久化**，导致重试时最新进度丢失 | [#11363 Persist heartbeat checkpoint data on failure](https://github.com/temporalio/temporal/pull/11363) | ✅ 已有 fix PR |
| 中 | **SAA 缺少 schedule-to-start 延迟指标**，无法与 WFA 对比观察 backlog 积压情况 | [#11396 Record SAA task schedule-to-start latency](https://github.com/temporalio/temporal/pull/11396) | ✅ 已有 fix PR（前版本 #11379 已关闭） |
| 中 | **Throttled logger 的 tags 在 `Skip()` 后丢失**，影响日志关联性 | [#11355 Preserve logger tags across Skip()](https://github.com/temporalio/temporal/pull/11355) | ✅ 已有 fix PR |
| 中 | **ActivityExecutionInfo 未填充 LastDeploymentVersion**，导致 Describe 返回信息不完整 | [#11386 Include LastDeploymentVersion in buildActivityExecutionInfo](https://github.com/temporalio/temporal/pull/11386) | ✅ 已有 fix PR |
| 低 | **frontend gRPC 连接每次调用重新 dial**，存在性能浪费 | [#11296 Cache frontend gRPC connections](https://github.com/temporalio/temporal/pull/11296) | ✅ 已有 fix PR（修复 #11289） |

**总体判断**：无致命回归，但固定缺陷数量不少，尤其 retry jitter 失效属于影响线上行为的问题（退避分散失效可能导致惊群效应）。

## 6. 功能请求与路线图信号

虽然今日无新 Issue 提出功能请求，但 PR 侧呈现了清晰的路线图信号：

| 信号 | 来源 PR | 判断 |
|---|---|---|
| **SAA 功能进入成熟期**：指标、持久化、测试三路并进 | #11396 / #11363 / #11375 | 很可能进入 1.32.0 正式版本 |
| **API 简化**：UnpauseActivityExecution 移除 `reset_attempts` 与 `reset_heartbeat` 字段 | [#11393 Drop reset_attempts](https://github.com/temporalio/temporal/pull/11393) | 配合 temporalio/api#846，API 语义收敛 |
| **UpdateOptions 语义收紧**：不允许在 `CANCEL_REQUESTED` 或 `RESET_REQUESTED` 状态下携带 | [#11394 Do not permit UpdateOptions](https://github.com/temporalio/temporal/pull/11394) | 明确状态机边界，提升 API 确定性 |
| **性能优化**：frontend gRPC 连接复用 | [#11296 Cache gRPC connections](https://github.com/temporalio/temporal/pull/11296) | 针对高频调用场景的优化，或回应 issues #11289 |
| **v1.32.0 发布窗口开启** | #11395 | 上述多项修复/功能大概率随新版发布 |

## 7. 用户反馈摘要

由于今日无新 Issue 且现有 PR 评论区数据为空，以下反馈信号从 PR 描述中间接提炼：

- **Retry jitter 不被遵守的真实场景**（#11397）：用户设置 `WithJitter(0.1)` 和 2s 基准，实际每次重试均为精确 2.000s。在分布式系统中这种"伪随机"退避会导致客户端同步重试，放大下游压力。
- **SAA 活动重试丢失进度**（#11363）：当活动 attempt 失败时，调用方随失败消息发送的 checkpoint 数据没有持久化为 last heartbeat details，导致下次 attempt 无法恢复最新进度。作者在描述中直接引用"a relatively bad bug"。
- **Describe 信息不完整**（#11386）：当 poller 报告了 deployment version 后，`DescribeActivity` 返回的 `LastDeploymentVersion` 始终为空，影响部署追踪和发布回滚判断。

这些反馈集中于"配置不生效"和"数据可见性缺失"两类问题，反映了用户对 Temporal 可靠性机制的可预期性和可观测性有较高要求。

## 8. 待处理积压

以下为长期未合并且值得关注的 PR，提醒维护者审查或决定去留：

| PR | 状态 | 停滞时长 | 备注 |
|---|---|---|---|
| [#9796 Handle duplicate err in apply snapshot](https://github.com/temporalio/temporal/pull/9796) | OPEN 且已标记 **[stale]** | 自 2026-04-02 至今 **约 4 个月** | 处理 apply snapshot 中重复错误需要 reload 重试的逻辑，属于核心数据路径。已被标记 stale，建议维护者明确关闭或安排评审 |
| [#11155 Log NotFound errors when adding speculative WFT](https://github.com/temporalio/temporal/pull/11155) | OPEN | 自 2026-07-20 至今 **2 周** | 低风险打日志改动，与现有 `pushWorkflowTask` 行为对齐。作者 @RajeshRajendiran 今日同时提交了 #11296，属于同一活跃贡献者，值得尽快过审 |

**项目健康度综合评估**：Temporal 项目当前处于 SAA 功能攻坚与 v1.32.0 发布筹备的双线并行状态。活跃贡献者多、修复节奏快（多数 bug 在 PR 阶段即被解决），但 Issue 侧数据为零说明公开用户反馈渠道热度一般——也可能是大规模功能改动期间社区讨论集中于 Slack/论坛等其他渠道。核心风险项是 #9796 这类长时间 stale 的存储层修复，建议维护团队在本周内给出明确方向。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*