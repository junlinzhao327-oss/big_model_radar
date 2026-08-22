# OpenClaw 生态日报 2026-08-23

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-22 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-23

## 1. 今日速览

过去24小时项目保持极高活跃度：500条Issue更新（480条新开/活跃，20条关闭）与500条PR更新（427条待合并，73条已合并/关闭），显示社区参与度与维护者响应均处于高位。但需警惕的是，已有多个P0/P1级稳定性问题（如beta.2网关事件循环阻塞、SQLite损坏复发）进入待处理队列，且大量高优先级问题长期积压。无新版本发布，项目当前聚焦于beta.2的发布验证与回归修复。总体上，项目处于高频迭代阶段，但稳定性债务正在累积。

## 3. 项目进展

今日共73个PR被合并/关闭，重点集中在：

- **多通道消息投递**：[#126424](https://github.com/openclaw/openclaw/pull/126424) 确保会话投递严格限定在Agent绑定范围内，影响Discord、iMessage、Matrix、Mattermost、Slack、Telegram、Feishu等全渠道，属于安全边界修复。
- **OAuth/认证稳定性**：[#125471](https://github.com/openclaw/openclaw/pull/125471) 保持Claude CLI OAuth在控制UI中可用，修复Gateway重启后刷新所有权丢失问题。
- **安装策略**：合并[#116489](https://github.com/openclaw/openclaw/pull/116489)（安装策略警告需操作员确认）及[#120900](https://github.com/openclaw/openclaw/pull/120900)（UI支持审查安装策略警告），构筑插件安装安全防线。

另有#118505、#118499等macOS实时语音（Talk）相关PR在等待审查，显示macOS平台功能补全仍是开发方向之一。

## 4. 社区热点

| 排名 | Issue/PR | 评论数 | 核心诉求 |
|-------|----------|--------|----------|
| 1 | [#125626 Release validation: v2026.8.1-beta.2](https://github.com/openclaw/openclaw/issues/125626) | 19 | 社区成员正在按流程对beta.2做发布验证，要求参与者在release-only评论中报告结果 |
| 2 | [#68596 Configurable streaming watchdog timeout](https://github.com/openclaw/openclaw/issues/68596) | 15 | 深度推理模型（如Kimi K2.5、DeepSeek-R1）触发流式看门狗误报，希望支持自定义超时阈值 |
| 3 | [#96834 WhatsApp 1:1 图片导致主消息通道停滞约3分钟](https://github.com/openclaw/openclaw/issues/96834) | 14 | 图片消息注入后多模态处理流程卡死，造成消息丢失，带复现步骤 |
| 4 | [#67777 子代理完成投递在超时/排空/孤儿清理时会丢失](https://github.com/openclaw/openclaw/issues/67777) | 12 | 子代理结果在busy-lane、超时、重启恢复等场景下静默丢失 |
| 5 | [#51429 工作路径被硬编码为 /Users/wangtao 并已发布](https://github.com/openclaw/openclaw/issues/51429) | 12 | 用户对代码中残留个人路径被合并发布表达强烈不满 |

其中，**硬编码路径泄漏**（#51429）是典型的人为流程失误，触发了社区对代码审查流程的质疑；而**流式看门狗超时**（#68596）与**WhatsApp图片处理**（#96834）代表真实用户遭遇的日常使用障碍，诉求明确且可复现，建议优先处理。

## 5. Bug 与稳定性

### P0 级

| Issue | 问题 | 状态 |
|--------|------|------|
| [#124788](https://github.com/openclaw/openclaw/issues/124788) | **beta.2 网关事件循环每约10.9分钟阻塞100–120秒**，导致WebSocket断开、HTTP /ready无响应、cron调度器停滞。已确认即使禁用全部内存插件仍复现 | 无fix PR，待维护者处理 |
| [#126821](https://github.com/openclaw/openclaw/issues/126821) | **SQLite损坏在纯净重建后15–24小时内复发**（WSL2），5天内5次事件，包含"网关瘫痪但进程不退出"模式 | 无fix PR，databaseloss风险 |

### P1 级

| Issue | 问题 | 状态 |
|--------|------|------|
| [#85030](https://github.com/openclaw/openclaw/issues/85030) | MCP工具不注入子代理会话，`bundle-mcp`+白名单全部失效，仅收到内置工具 | 无fix PR |
| [#89278](https://github.com/openclaw/openclaw/issues/89278) | Codex OAuth刷新后cron/heartbeat仍因10秒超时失败 | 有linked PR |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | hook/tool子进程未被回收，僵尸进程累积导致运行退化 | 无fix PR |
| [#113701](https://github.com/openclaw/openclaw/issues/113701) | 大型工具输出导致上下文溢出，压缩无法恢复，会话进入失败循环 | 无fix PR |
| [#78805](https://github.com/openclaw/openclaw/issues/78805) | 同步I/O（execSync/readFileSync）导致事件循环阻塞达4秒 | 有linked PR |

## 6. 功能请求与路线图信号

以下功能请求讨论热度高且有明确需求依据，部分已有对应PR：

- **macOS 实时语音（Talk）支持**：PR [#118505](https://github.com/openclaw/openclaw/pull/118505) 与 [#118499](https://github.com/openclaw/openclaw/pull/118499) 分别推进Talk设置与Gateway中继支持，方向是让macOS端获得完整的实时语音体验。
- **流式看门狗超时可配置**（[#68596](https://github.com/openclaw/openclaw/issues/68596)）：深度推理模型用户群体的强烈诉求，属于低成本高收益的配置增强。
- **优雅网关重启＋会话恢复**（[#57425](https://github.com/openclaw/openclaw/issues/57425)）：解决重启时进行中任务被静默杀死的问题，对生产部署尤为重要，但设计面较大。
- **会话快照保存/加载**（[#13700](https://github.com/openclaw/openclaw/issues/13700)）：支持 `/session save|load` 用于A/B测试、分支对话、回滚操作，是中长期路线图级需求。
- **内置节奏感知速率限制**（[#45771](https://github.com/openclaw/openclaw/issues/45771)）：针对自主循环（子代理、心跳任务）的API限额消耗控制。

社区对功能开发的期待集中在三点：**流式传输稳定性、macOS体验补齐、会话生命周期管理**。

## 7. 用户反馈摘要

- **硬编码路径泄漏引发信任危机**（[#51429](https://github.com/openclaw/openclaw/issues/51429)）：用户"buggiant-coder"措辞激烈，强烈质疑代码审查流程；"似乎是有人把工作路径硬编码进代码而且居然被合并发布了"。
- **配置警告无法消解**（[#60612](https://github.com/openclaw/openclaw/issues/60612)）：doctor提示NVM node问题，但每次重启都会被重新生成，用户无法手动修复，体验较差。
- **重启等待超时**（[#89528](https://github.com/openclaw/openclaw/issues/89528)）：`--safe --skip-deferral` 标志仍无法跳过重启时本身的回复排空等待，说明该标志实装不彻底。
- **同一回复重复发送**（[#49381](https://github.com/openclaw/openclaw/issues/49381)）：Feishu渠道在限流主模型失败切换后，会发送两条最终回复，用户困惑且无法自行规避。
- **cron失败通知轰炸**（[#90595](https://github.com/openclaw/openclaw/issues/90595)）：热重载和重试期间持续发送失败通知，造成告警疲劳，社区用户呼吁按重试状态延迟通知。

## 8. 待处理积压

以下高优先级Issue长期未关闭且无有效fix PR，需维护者关注：

| 时间 | Issue | 优先级 | 备注 |
|------|--------|--------|------|
| 2026-05-21 | [#85030 MCP工具不注入子代理](https://github.com/openclaw/openclaw/issues/85030) | P1 | 已3个月无进展，阻塞subagent场景 |
| 2026-04-16 | [#67777 子代理完成投递丢失](https://github.com/openclaw/openclaw/issues/67777) | P1 | 超过4个月未关闭 |
| 2026-03-13 | [#44502 Discord路由/提及门控问题](https://github.com/openclaw/openclaw/issues/44502) | P2 | 3月创建，至今开放，需live reproduction |
| 2026-04-17 | [#68187 SSE-MCP会话重启后stale](https://github.com/openclaw/openclaw/issues/68187) | P2 | 已4个月无有效回应 |
| 2026-03-13 | [#45224 Playwright断言崩溃网关](https://github.com/openclaw/openclaw/issues/45224) | P1 | 已有fix-shape-clear，但一直未合入 |

> 总体判断：OpenClaw当前处于高活跃度、高问题密度的beta周期，发布验证（#125626）与P0级稳定性问题（#124788、#126821）是当前最需要投入的关键路径。建议优先修复SQLite损坏与事件循环阻塞，再集中处理长期积压的P1级子代理相关问题。

---
*本报告基于OpenClaw GitHub仓库公开数据自动生成，数据覆盖2026-08-22至2026-08-23的更新。*

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报

**日期：** 2026-08-23  
**数据窗口：** 2026-08-22 - 2026-08-23（过去 24 小时）


## 1. 今日速览

过去 24 小时项目处于**高度活跃**状态：共处理 Issues 11 条（新开/活跃 6 条，关闭 5 条），PR 17 条（6 条待合并，11 条已合并/关闭）。虽然无新版本发布，但多条高优先级 Bug（如崩溃恢复导致数据损坏、全局锁引发的并发卡死）已有对应修复 PR，表明维护者对稳定性问题响应迅速。值得关注的是，社区讨论集中在异步锁粒度、子代理事件流、模型兼容性等底层架构议题上，项目正从功能扩展期逐步进入稳定性加固阶段。


## 2. 版本发布

过去 24 小时无新版本发布。


## 3. 项目进展

今日合并/关闭的 PR 覆盖了安全修复、性能优化和工程规范等多个维度，项目在稳定性和开发体验上均有实质推进：

- **[PR #4571] fix(workspace): honor explicit provider host when injecting git clone tokens**（已合并） — 修复了自托管 GitLab 实例的 token 注入问题，解决了企业用户无法使用私有 Git 仓库的阻塞性问题。对应 Issue [#4543](https://github.com/OpenHands/software-agent-sdk/issues/4543) 已关闭。相关开发者已本地运行 61 个测试。  
  https://github.com/OpenHands/software-agent-sdk/pull/4571

- **[PR #4488] fix(agent-server): keep crash recovery result on interrupted action branch**（已合并） — 修复了 agent-server 重启后对话事件分支损坏的严重 Bug（对应 Issue #4487），在真实环境中观察到三个对话受影响，修复采用文件备份租约接管测试，无 mock。  
  https://github.com/OpenHands/software-agent-sdk/pull/4488

- **[PR #2888] fix: sanitize malformed tool call arguments in LLM history**（已合并） — 修复了 LLM 输出畸形 JSON 参数导致历史消息损坏的问题，避免了下一次调用时错误传播。  
  https://github.com/OpenHands/software-agent-sdk/pull/2888

- **[PR #3266] fix(agent-server): evict idle terminal conversations**（已合并） — 为终端会话增加可配置的空闲 TTL 和 GC 间隔，避免内存泄漏，且不丢失持久化数据。  
  https://github.com/OpenHands/software-agent-sdk/pull/3266

- **[PR #3905] Optimize conversation search and count**（已合并） — 优化了对话搜索与计数性能。  
  https://github.com/OpenHands/software-agent-sdk/pull/3905

- **[PR #3800] [automated] Update verified_models.py**（已合并） — 自动化流程更新了通过全部 5 个基准测试的模型列表。  
  https://github.com/OpenHands/software-agent-sdk/pull/3800

- **[PR #3782] chore(examples): move 43_mixed_marketplace_skills to 05_skills_and_plugins**（已合并） — 示例目录结构优化，将资料市场技能示例迁移至专属目录，改善了开发者导航体验。  
  https://github.com/OpenHands/software-agent-sdk/pull/3782

- **[PR #2185] fix: MCP OAuth timeout regression - pin fastmcp <3**（已合并） — 修复了因 fastmcp 自动升级到 v3.0.2 导致的 OAuth MCP 服务器超时回归问题。  
  https://github.com/OpenHands/software-agent-sdk/pull/2185

- **[PR #1457] [plugins] Plugin Marketplace Compatibility: Align with Claude Code & AgentSpec**（已合并） — 达成与 Claude Code Plugins 和 AgentSpec 标准的完全兼容，支持插件市场 monorepo 与 Python 包共享同一插件结构。  
  https://github.com/OpenHands/software-agent-sdk/pull/1457


## 4. 社区热点

**🔥 热度最高 Issue：[#3303] [Feature]: ToolBuild hooks**（11 条评论，已关闭）  
社区用户希望获得工具列表构建前/后的钩子函数，以便在工具发送给 LLM 前进行运行时操作。该需求涉及 Agent 行为的深度自定义，已在 3 个月后标记为 Stale 并关闭。这说明核心团队当前重心不在扩展 Hook 机制上。  
https://github.com/OpenHands/software-agent-sdk/issues/3303

**[#4511] `Message.to_chat_dict` 缓存控制 Bug**（5 条评论，开放中）  
当缓存被禁用时，`Message.to_chat_dict` 仍可能发出 `cache_control` 标记。该问题影响 Anthropic 缓存行为，是典型的配置未生效问题，已标记 `ready-for-dev`。  
https://github.com/OpenHands/software-agent-sdk/issues/4511

**[#4537] 子代理运行导致 UI 冻结**（4 条评论，1 👍，开放中）  
`TaskToolSet` 子代理调用期间持有父级 `ConversationState` 锁，导致 Agent Canvas 对话列表在整个委派任务期间停止渲染。该问题直接冲击用户体验，已被标记为高优先级。  
https://github.com/OpenHands/software-agent-sdk/issues/4537

**分析：** 社区讨论热点集中在 **子代理/委派机制的稳定性** 与 **LLM 交互的配置正确性** 上。用户对多代理并行运行时的性能和 UI 响应有明确期望，同时对底层 LLM 调用参数的准确性有较高敏感度。


## 5. Bug 与稳定性

### 🔴 高优先级

| Issue | 问题描述 | 状态 | 对应修复 PR |
|-------|---------|------|------------|
| [#4537](https://github.com/OpenHands/software-agent-sdk/issues/4537) | `TaskToolSet` 子代理持有父级锁，导致 executor 池饱和和 UI 冻结 | 开放中，4 条评论，1 👍 | 暂无直接 PR |
| [#4569](https://github.com/OpenHands/software-agent-sdk/issues/4569) | 全局 `_lifecycle_lock` 导致跨对话互锁（并发回归） | 开放中，`ready-for-dev` | **[PR #4570](https://github.com/OpenHands/software-agent-sdk/pull/4570)**（开放中） |
| [#4487](https://github.com/OpenHands/software-agent-sdk/issues/4487) | 崩溃恢复孤立了被中断的工具结果，永久破坏后续轮次 | 已关闭 | ✅ **[PR #4488](https://github.com/OpenHands/software-agent-sdk/pull/4488)**（已合并） |

### 🟡 中优先级

| Issue | 问题描述 | 状态 | 对应修复 PR |
|-------|---------|------|------------|
| [#4511](https://github.com/OpenHands/software-agent-sdk/issues/4511) | `Message.to_chat_dict` 在禁用缓存时仍发出 `cache_control` | 开放中，`ready-for-dev` | 暂无 |
| [#4543](https://github.com/OpenHands/software-agent-sdk/issues/4543) | 自托管 GitLab 无法使用 token 克隆仓库 | 已关闭 | ✅ **[PR #4571](https://github.com/OpenHands/software-agent-sdk/pull/4571)**（已合并） |
| [#4554](https://github.com/OpenHands/software-agent-sdk/issues/4554) | `CriticMixin` 始终以 `git_patch=None` 调用 `evaluate()` | 开放中 | 暂无 |

### 🟢 其他

| Issue | 问题描述 | 状态 |
|-------|---------|------|
| [#4578](https://github.com/OpenHands/software-agent-sdk/issues/4578) | 切换到 GPT-5.6 时，历史中含冒号分隔的 tool-call ID 导致失败 | 开放中，`ready-for-dev` |
| [#3940](https://github.com/OpenHands/software-agent-sdk/issues/3940) | `initial_message.run` 在对话启动时被硬编码为 True（已关闭，Stale） | 已关闭 |

**Bug 趋势判断：** 并发锁设计（#4569、#4537）和 LLM 兼容性（#4578、#4511）是当前稳定性短板。值得肯定的是，崩溃恢复问题（#4487）和 GitLab token 问题（#4543）均在 24 小时内完成了修复闭环。


## 6. 功能请求与路线图信号

- **[#3303] ToolBuild hooks**（已关闭/Stale）→ 工具列表运行时操作钩子需求，短期优先级较低。  
  https://github.com/OpenHands/software-agent-sdk/issues/3303

- **[#4577] Add per-key tag endpoints**（开放中，2 条评论）→ 避免 PATCH `/api/conversations/{id}` 的全量标签替换，需要细粒度更新接口。属于 API 体验优化，与现有 `UpdateConversationRequest.tags` 语义冲突，可能被纳入后续 API 改进。  
  https://github.com/OpenHands/software-agent-sdk/issues/4577

- **[#3907] forward sub-agent (TaskToolSet) inner events to the live conversation stream**（已关闭/Stale）→ 子代理内部事件透传到父级实时流，对 WebSocket 实时消费者非常重要，建议在未来版本重新评估。  
  https://github.com/OpenHands/software-agent-sdk/issues/3907

- **[PR #4576] 50/50 RevShare Integration: OpenHands & AIML API**（开放中）→ 外部商业合作伙伴提出的集成方案，AIML API（1000+ 模型聚合平台）希望成为 OpenHands 的验证提供商选项。该 PR 涉及商业条款，需要团队评估。  
  https://github.com/OpenHands/software-agent-sdk/pull/4576

- **[PR #2810] Memory: Research & Implementation Plan for Persistent Auto-Learning**（已合并）→ 持久化自动学习记忆的研究与实现计划，标志记忆功能进入规划阶段，值得关注后续进展。  
  https://github.com/OpenHands/software-agent-sdk/pull/2810


## 7. 用户反馈摘要

- **企业部署者的痛点（Issue #4543）**：自托管 GitLab 用户无法注入 token 克隆仓库，说明企业级用户使用非 SaaS 版本时存在集成障碍。这类问题直接影响私有化部署场景的可用性。  
  https://github.com/OpenHands/software-agent-sdk/issues/4543

- **重度使用者的观察（Issue #4537）**："Agent Canvas conversation list stops rendering for the entire duration of the delegated task" — 子代理执行期间 UI 完全冻结，说明当前锁机制在长时间任务下会严重影响多任务操作体验。背后的现象也提醒了委派场景需要并行支持。  
  https://github.com/OpenHands/software-agent-sdk/issues/4537

- **API 客户端开发者的困扰（Issue #4577）**：标签更新必须整表替换，客户端不得不执行"读取-修改-写入"操作，存在并发覆盖风险和额外的往返延迟，尤其对于需要频繁标记多会话的自动化运维场景比较不便。  
  https://github.com/OpenHands/software-agent-sdk/issues/4577

- **模型切换用户的挫败感（Issue #4578）**：从 Kimi K3 切换到 GPT-5.6 时因历史消息中的 tool_call_id 冒号分隔格式失败，跨模型迁移能力是用户选择开放平台的重要原因，这类问题会削弱多模型战略的价值。  
  https://github.com/OpenHands/software-agent-sdk/issues/4578

- **对文档准确性的认可（Issue #4577 引述）**：用户肯定 `UpdateConversationRequest.tags` 文档说明清晰（"Replaces all existing tags when provided"），说明项目文档质量获得了用户认可，是积极信号。  
  https://github.com/OpenHands/software-agent-sdk/issues/4577


## 8. 待处理积压

- **[PR #4438] fix(sdk): prevent double provider-prefix strip for namespaced model IDs** — 自 2026-08-09 起待合并，处理模型 ID 前缀解析问题，无评论无更新，PR 作者已提交但等待维护者关注。  
  https://github.com/OpenHands/software-agent-sdk/pull/4438

- **[PR #2888] fix: sanitize malformed tool call arguments** — 该 PR 经过长时间停留（4 月创建，8 月 22 日关闭/合并），说明维护队列审阅延迟较明显。  
  https://github.com/OpenHands/software-agent-sdk/pull/2888

- **[PR #1457] Plugin Marketplace Compatibility** — 自 2025 年 12 月开启，历时 8 个月才合并，大型跨标准兼容工作审阅周期较长。  
  https://github.com/OpenHands/software-agent-sdk/pull/1457

- **[PR #4576] AIML API RevShare 集成** — 商业合作类 PR，需要商务与法务评估，预期审阅周期较长。  
  https://github.com/OpenHands/software-agent-sdk/pull/4576


## 项目健康度总结

| 维度 | 状态 | 说明 |
|------|------|------|
| **活跃度** | 🟢 高 | 24h 内 11 Issues + 17 PRs，且新开和合并数量均衡 |
| **响应速度** | 🟢 快 | 高优先级 Bug（#4487、#4543）在 24h 内完成修复闭环 |
| **并发/性能** | 🟡 关注 | 锁粒度和子代理并发问题仍在解决中（#4569、#4537） |
| **社区参与** | 🟢 活跃 | 用户积极报告 Bug 和提出功能需求，外部贡献者持续提交 PR |
| **版本演进** | 🟡 平稳 | 无新版本发布，处于稳定性修复窗口期 |

**结论：** 项目正处于健康的社区驱动开发阶段，核心团队对高优 Bug 响应迅速，但并发架构和模型兼容性仍是当前主要技术债。建议用户关注 [PR #4570](https://github.com/OpenHands/software-agent-sdk/pull/4570)（全局锁替换为 per-conversation 锁）的合入进展，该修复将直接影响多会话并发场景的稳定性。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-23

## 今日速览

过去24小时 Pi 项目 Issue 与 PR 处理量显著放大：共 62 条 Issue 更新（其中 54 条关闭）、11 条 PR 更新（其中 7 条合并/关闭），无新版本发布。项目整体处于高强度维护状态，大量 bug 修复与功能合入已落地，同时社区围绕 Windows 支持、上下文压缩可靠性、终端兼容性等话题展开密集讨论。值得关注的是，多个长期悬置的功能性 PR（如 llama.cpp 集成、ConPTY 渲染修复）已接近完成，预示下一个版本将包含实质性的稳定性提升。

---

## 版本发布

本期无新版本发布。

---

## 项目进展

过去24小时有 7 条 PR 完成合并或关闭，主要集中在以下几个方向：

- **Windows/ConPTY 渲染修复** — `fix(tui): disable autowrap around main-screen renders to prevent ConPTY drift`（[#8485](https://github.com/earendil-works/pi/pull/8485)）修复 Windows Terminal 下编辑器光标丢失/视口滚动错位的问题，配套新增编辑器滚动捕获与验证工具链（[#8486](https://github.com/earendil-works/pi/pull/8486)）。这直接回应了社区中高优先级的 Windows 体验 bug。
- **llama.cpp 集成补全** — `fix: expose unloaded llama.cpp presets`（[#8479](https://github.com/earendil-works/pi/pull/8479)）解决了使用 `--models-preset` 时未加载预设无法在模型列表显示的问题，是 #8167 的修复 PR。
- **Provider 生态扩展** — `feat(ai): add MindsHub provider`（[#8488](https://github.com/earendil-works/pi/pull/8488)）将 MindsHub 加入内置 `pi-ai` 提供商，进一步丰富 OpenAI/Anthropic 兼容网关的接入选项。
- **本地化能力** — `feat(coding-agent,tui): add locale switching via /settings`（[#8295](https://github.com/earendil-works/pi/pull/8295)）支持在 `/settings` 菜单中切换英文与简体中文，并新增 locale 持久化机制。
- **TUI 细节优化** — `fix(tui): keep / and - inside fullscreen double-click word selection`（[#8459](https://github.com/earendil-works/pi/pull/8459)）修复全屏模式下双击选中路径时 `/` 与 `-` 被割裂的问题。

此外，`feat(coding-agent): bundle Node runtime`（[#8474](https://github.com/earendil-works/pi/pull/8474)）正在优化 `pi-coding-agent` 的打包方式，以减少加载文件数量、缓解 Windows Defender 等环境下的启动延迟，虽已关闭但尚需更多测试。

项目整体围绕 **Windows 体验修复、模型提供方接入、TUI 交互细节**三个方向稳步推进，且修复类 PR 与对应 Issue 形成闭环，项目健康度良好。

---

## 社区热点

- **[#7547] [Windows] How do you use Pi on windows? What issues are you seeing?**（[链接](https://github.com/earendil-works/pi/issues/7547)）— 39 条评论，持续发酵中。作者 @petrroll 直接面向 Windows 用户征集使用方式与痛点，意在识别核心投入方向。该帖反映出 Windows 上运行 Pi 的方式碎片化（原生、WSL、MSYS2 等），项目方需要明确优先支持路径。
- **[#6879] auto-compaction never triggers after context grows past 100% until provider overflow**（[链接](https://github.com/earendil-works/pi/issues/6879)）— 20 条评论、18 个 👍，是当前最受关注的功能性 bug。用户报告在一次 2 小时的 agentic turn 中上下文突破 100% 直到 API 拒绝请求（373k tokens），自动压缩未按预期触发。社区共识是需要在每次 agent 步骤后检查压缩阈值。
- **[#7130] Backspace deletes 2 chars in Kitty (Kitty protocol release events not filtered)**（[链接](https://github.com/earendil-works/pi/issues/7130)）— 11 条评论，Kitty 键盘协议下退格键行为异常，已定位到协议事件过滤问题。
- **[#8157] Migrate grok-mermaid -> lovely-mermaid**（[链接](https://github.com/earendil-works/pi/issues/8157)）— 9 条评论，社区中有人提议将 mermaid 渲染迁移到维护更好的 `lovely-mermaid`，需关注是否被纳入路线图。

---

## Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue | 描述 | 状态 |
|---|---|---|---|
| 高 | [#6879](https://github.com/earendil-works/pi/issues/6879) | 自动压缩在上下文超限后仍不触发，直至 provider overflow；存在工作中断与 token 消耗风险 | 开放中，无 fix PR |
| 高 | [#8484](https://github.com/earendil-works/pi/issues/8484) | Windows Terminal 下编辑长文时视口滚动到顶、光标丢失（ConPTY autowrap drift） | **有 fix PR：** [#8485](https://github.com/earendil-works/pi/pull/8485) 已合并/关闭 |
| 中 | [#7130](https://github.com/earendil-works/pi/issues/7130) | Kitty 协议下退格键一次删除两个字符 | 开放中，已定位原因 |
| 中 | [#8442](https://github.com/earendil-works/pi/issues/8442) | herdr pane 内 Backspace 被忽略（legacy `0x7f` 未被 KKP 协议识别），Ctrl+Backspace 正常 | 已关闭，待验证修复方案 |
| 中 | [#8212](https://github.com/earendil-works/pi/issues/8212) | 0.84.2 切换主题后 header、tree 标签等处残留旧主题色 | 开放中 |
| 低 | [#8468](https://github.com/earendil-works/pi/issues/8468) | GitHub Copilot 登录超时，可能与 PR #8254 相关（未进入 release） | 已关闭，需等版本发布验证 |
| 低 | [#7779](https://github.com/earendil-works/pi/issues/7779) | `auth.json` 与 `models-store.json` 权限为 `0600`，多用户共享 `PI_CODING_AGENT_DIR` 受阻 | 已关闭，权限逻辑调整 |

**信号：** 维护者对 bug 响应非常积极，Windows/ConPTY 修复从 Issue 报告到 PR 合入仅一天（#8484 → #8485），是项目健康度的积极指标。但 #6879（自动压缩）由于涉及核心上下文管理逻辑，仍是最关键的未修复稳定性风险。

---

## 功能请求与路线图信号

- **自动压缩与输出继续增强** — [#8464](https://github.com/earendil-works/pi/issues/8464) 提出在模型真正达到输出上限时自动继续运行、并在工具回合间隙检查压缩，与 #6879 高度关联，可能随上下文管理重构一并考虑。
- **模型选择持久化范围配置** — [#8376](https://github.com/earendil-works/pi/issues/8376) 希望 `/model` 选择可配置为 session/directory/global 不同持久化范围，属于低成本高收益的 UX 改进。
- **排除扩展加载** — [#8431](https://github.com/earendil-works/pi/issues/8431) 建议增加 `--exclude-extensions` 参数，与现有 `--exclude-tools` 对齐；目前扩展加载是"全有或全无"，该需求在复杂配置用户中有一定代表性。
- **MindsHub 提供商** — [#8489](https://github.com/earendil-works/pi/issues/8489) 已在 PR #8488 中实现并合并，进入下一版本无悬念。
- **远程会话运行本地 TUI**（[#8481](https://github.com/earendil-works/pi/issues/8481)）— 希望在 Kubernetes devbox 中由客户端渲染 TUI、服务端承载 agent 会话。属于架构级能力，现有 `RemoteSession` 机制可以延伸，但需要明确 RPC 接口设计，短期落地可能性低。
- **记忆扩展方案**（[#8385](https://github.com/earendil-works/pi/issues/8385)）— SQLite 检索式记忆 + 活跃笔记本 + 蒸馏，社区提出的完整记忆机制，与当前上下文压缩问题互补，值得维护者评估是否吸收

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-23

## 1. 今日速览

过去 24 小时 LiteLLM 项目保持高度活跃：共产生 68 条 Issue 更新（新开/活跃 29，已关闭 39）和 314 条 PR 更新（待合并 107，已合并/关闭 207），修复吞吐量显著。今日无新版本发布，但大量修复集中在 Responses API 桥接、成本计费准确性和团队管理并发安全等方向，另有多个长期未决的社区热点（如 Dark Mode #10177）持续获得关注。总体来看，项目维护响应速度较快、问题关闭率高，处于健康且密集的迭代周期中。

## 2. 版本发布

今日无新版本发布。最近可用版本仍为 v1.96.2（有用户反馈该版本在 `uv tool update` 后出现 FastAPI 兼容性问题，见 #36922），建议关注后续补丁版本。

## 3. 项目进展

今日共合并/关闭 207 个 PR，覆盖功能修复、测试加固和基础设施改进。从代表性的合并 PR 中可以看出以下几个清晰的推进方向：

### Responses API 桥接层持续完善
- **#37946 fix(responses): mint Responses API item IDs in the completion bridge**：修复桥接 `/v1/responses` 输出项携带 `chatcmpl-*` ID、流式事件与最终快照 ID 前缀不一致、图片生成项 ID 格式错误等问题，避免原生 OpenAI 拒绝重放历史记录。 https://github.com/BerriAI/litellm/pull/37946
- **#36355 fix(responses-bridge): preserve reasoning input items and signed thinking blocks**：保留 `reasoning` 输入项、防止明文推理变成可见 assistant 文本、让 `encrypted_content` 签名可回传。 https://github.com/BerriAI/litellm/pull/36355

### 代理行为修正
- **#37964 fix(proxy): omit litellm_batch_guardrail when no guardrail acted**：修复所有 `/v1/files` 响应都带 `litellm_batch_guardrail: null` 的字段泄漏问题，恢复与 OpenAI 文件形状的字节一致性。 https://github.com/BerriAI/litellm/pull/37964

### 工程质量与测试
- **#37974 test: add regression coverage for twelve closed issues**：为 12 个已修复但缺乏回归保护的问题补充测试，纯测试改动，防止修复静默回退。 https://github.com/BerriAI/litellm/pull/37974
- **#37957 test(e2e): harden the suite against response-cache cross-talk, slow providers and single upstream blips**：定位了 e2e 构建 43–51 和 PR 门禁 110–114 中所有非确定性失败的三个测试框架弱点并加固。 https://github.com/BerriAI/litellm/pull/37957
- **#37976 chore: rebuild Admin UI bundle**：重新生成 Admin UI 构建产物，修复代理页面落后于 dashboard 源码的问题。 https://github.com/BerriAI/litellm/pull/37976

### 正在推进中的高价值 PR（待合并）
- **#37975 fix(databricks): bill cached tokens at cache rates and add missing Claude pricing**：修复 Databricks 缓存读取按全价计费、注册表缺少缓存读写费率、以及多个 Claude 模型（Opus 4.7/4.8/5、Sonnet 5、Fable 5）未定价的问题。 https://github.com/BerriAI/litellm/pull/37975
- **#37953 fix(anthropic): round-trip thinking blocks to OpenAI backends on /v1/messages**：修复 `/v1/messages` 在 OpenAI 系后端丢失前一轮 thinking 块、以及 Moonshot 模型拒绝回合的问题。 https://github.com/BerriAI/litellm/pull/37953
- **#37899 ci: ban row-rewriting DML from prisma migrations**：在 CI 中禁止 migration 里出现 `UPDATE`/`DELETE`/`MERGE`，防止代理启动时执行行级重写造成停机。 https://github.com/BerriAI/litellm/pull/37899

## 4. 社区热点

### 最热 Issue：Dark Mode 请求（长期高赞）
- **#10177 [Feature]: Dark Mode** — 评论 64，👍 73，自 2025 年 4 月创建至今仍为 OPEN。用户声称“I'm going blind”，反映 Admin UI 可访问性痛点。这是当前社区呼声最高的功能请求，长期未得到官方排期回应。 https://github.com/BerriAI/litellm/issues/10177

### 用量统计看板双 Bug 引发讨论
- **#11929 [Bug]: Usage Dashboard: Two Issues with Spend Reporting and Failed Request Attribution** — 评论 15。涉及前端分页导致总花费严重少报、后端失败请求归属显示为 0 两个独立问题。直接关系到用户对计费数据的信任度，标的为 `mlops user request`。 https://github.com/BerriAI/litellm/issues/11929

### Vertex AI 自定义 api_base 凭证问题
- **#19138 [Bug]: Vertex AI: Custom api_base credential skip logic missing** — 评论 11，已关闭。用户通过自定义代理使用 Vertex AI 模型时，代理本不要求 Google 凭证，但库仍抛出 `DefaultCredentialsError`。该问题标有 `llm translation` 和 `SDK`，关闭说明修复已合入。 https://github.com/BerriAI/litellm/issues/19138

### 登录失效问题
- **#23451 [Bug]: Can't login despite setting password** — 评论 8，OPEN。用户设置了环境变量密码但 UI 无法用任何账号登录，涉及认证阻断，影响面大。 https://github.com/BerriAI/litellm/issues/23451

## 5. Bug 与稳定性

以下按严重程度排列今日活跃的 Bug 报告：

### 🔴 高严重度 — 阻断部署或核心功能
- **#36922 LiteLLM Proxy fails to start after uv tool update**：`uv tool update litellm["proxy"]` 升级到 v1.96.2 后，因 FastAPI `get_flat

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-23

## 今日速览

过去 24 小时内，Temporal 项目保持较高活跃度：共产生 21 条 PR 动态（待合并 19 条、关闭 2 条），新增/活跃 Issue 2 条，无新版本发布。PR 主要集中在 SQL 持久化领域（PostgreSQL 游标分页、并发更新条件、连接池刷新节流）、Worker Callbacks 特性堆叠 PR、以及多集群可靠性改进。值得关注的是今日已关闭 1.32.0 发布分支准备 PR，表明新版本即将进入发布流程。整体来看，项目处于“发布准备期 + 深度功能开发并行”的冲刺阶段，活跃度健康，社区反馈集中在配置行为一致性和本地开发工具链便捷性两方面。

## 版本发布

今日无新版本发布。

不过，PR [#11729](https://github.com/temporalio/temporal/pull/11729)（已关闭）完成了 1.32.0 发布分支的准备工作（覆盖治理文件、更新依赖），这是版本发布前的常规动作，预计 1.32.0 将在近期正式发布。

## 项目进展

虽然今日无功能 PR 被合并，但有两个值得关注的关闭 PR：

- [#11729](https://github.com/temporalio/temporal/pull/11729) **1.32.0 发布分支准备完成** — 说明 1.32.0 已进入发布流程，包含本次发布所需的基础设施调整。
- [#11708](https://github.com/temporalio/temporal/pull/11708) **更新测试分片盐值** — 由 optimize-test-sharding 自动化工作流生成，用于优化 CI 测试分片稳定性。

此外，21 条开放 PR 中有一批高质量代码正在推进，指向项目近期的重点方向：

- **SQL 持久化性能与正确性**（[#11712](https://github.com/temporalio/temporal/pull/11712)、[#11713](https://github.com/temporalio/temporal/pull/11713)、[#11714](https://github.com/temporalio/temporal/pull/11714)）：分别修复 PostgreSQL 分页 OR 表达式性能问题（#11709）、无变更时跳过更新（#11710）、以及并发更新时缺少条件校验（#11711），显著提升 SQL 型后端的稳定性。
- **Worker Callbacks 特性堆叠 PR**（[#11566](https://github.com/temporalio/temporal/pull/11566)、[#11520](https://github.com/temporalio/temporal/pull/11520)、[#11380](https://github.com/temporalio/temporal/pull/11380)）：持续向 `feature/worker-callbacks` 分支累积代码，目前尚未合入 main。
- **父子工作流可观测性**（[#11707](https://github.com/temporalio/temporal/pull/11707)）+ **被动集群子工作流失联恢复**（[#11705](https://github.com/temporalio/temporal/pull/11705)）：为多集群场景补充调试和自愈能力。
- **搜索属性 LIKE 操作**（[#11728](https://github.com/temporalio/temporal/pull/11728)）：为 keyword 类搜索属性引入子串匹配。

总体来看，Temporal 正在为 1.32.0 做最后的冲刺，同时在 SQL 存储选型、worker callbacks 新特性、多集群可靠性三个方向持续沉淀，项目向前推进的速度稳定。

## 社区热点

今日讨论最集中、评论最多的 Issue 是：

- **[#11721](https://github.com/temporalio/temporal/issues/11721) [Bug] MaximumAttempts can't be set to 0 when history.defaultActivityRetryPolicy is set on the server**（评论 3 条）
  - 作者 @M0NsTeRRR 报告：当服务端通过动态配置设置了 `history.defaultActivityRetryPolicy` 时，客户端显式传入 `MaximumAttempts=0`（即无限重试）会被服务端覆盖为默认的 5 次。由于 proto3 int32 无法区分“未设置”和“显式 0”，导致用户无法在实际业务中按需关闭重试限制。
  - 该问题触及服务端动态配置与客户端显式策略的优先级语义，属于影响生产行为的配置兼容性 bug，社区关注度高。

另一个讨论中的请求：

- **[#11718](https://github.com/temporalio/temporal/issues/11718) [enhancement] 在发布归档中包含 temporal development CLI**
  - 用户使用 [Mise](https://github.com/jdx/mise) 管理项目依赖，但 release archive 中不含 CLI 可执行文件。Mise 生态约定直接使用发布包中的二进制，导致自动化安装流程断裂。这类工具链集成诉求在开源社区中较为普遍。

## Bug 与稳定性

| 严重程度 | 问题 | 状态 | 修复 PR |
|---|---|---|---|
| **高** | [#11721](https://github.com/temporalio/temporal/issues/11721) 动态配置 `defaultActivityRetryPolicy` 覆盖用户显式 `MaximumAttempts=0`，导致“无限重试”无法实现 | 开放中，已有 3 条讨论 | 已有 [#11727](https://github.com/temporalio/temporal/pull/11727) 提交修复，保持显式 0 的语义 |
| 中 | [#11730](https://github.com/temporalio/temporal/pull/11730) SQL 连接池刷新节流检查顺序有误——若被节流，连接池被清空但未创建替代池，数据库句柄可能失效 | 修复 PR 开放中 | 该 PR 自身即修复 |
| 中 | [#11714](https://github.com/temporalio/temporal/pull/11714) SQL 执行更新缺少并发条件校验（修复 #11711），可能引发更新覆盖 | 修复 PR 开放中 | 该 PR 自身即修复 |
| 低 | [#11725](https://github.com/temporalio/temporal/pull/11725) 基于类型的批处理活动取消暂停操作会替换调用方可见性查询，导致批量操作范围错误 | 修复 PR 开放中 | 该 PR 自身即修复 |

值得注意的是 [#11714](https://github.com/temporalio/temporal/pull/11714) 对应的底层 Issue #11711 和另外两个 SQL 正确性 Issues（#11709、#11710）虽然未列入今日新报告，但它们对应的修复 PR 今日仍在活跃，说明 SQL 存储选项正在经历一次集中的正确性补强。

## 功能请求与路线图信号

今日新出现的功能请求：

- **[#11718](https://github.com/temporalio/temporal/issues/11718)** 将 development CLI 打包进 release archive。改动工程量不大，但涉及发布流水线调整，可能被纳入近期版本。

结合当前开放 PR，以下方向值得重点关注，将成为未来版本的能力：

- **搜索属性增强**：[#11728](https://github.com/temporalio/temporal/pull/11728) 为 keyword 搜索属性新增 `LIKE/NOT LIKE` 操作符（SQL LIKE 模式与 ES wildcard 映射），可实现子串过滤，补齐当前仅支持精确匹配的短板。
- **Worker Callbacks 新的 callback 变体**：由 [#11380](https://github.com/temporalio/temporal/pull/11380)、[#11520](https://github.com/temporalio/temporal/pull/11520)、[#11566](https://github.com/temporalio/temporal/pull/11566) 等多条堆叠 PR 构成，为 `commonpb.Callback` 增加支持 worker 回调的新变体。该系列已在功能分支上迭代约 3 周，是一条长期的路线图级特性。
- **多集群渐进连接**：[#11492](

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*