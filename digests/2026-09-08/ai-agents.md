# OpenClaw 生态日报 2026-09-08

> Issues: 480 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-07 22:35 UTC

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

## OpenHands SDK 项目动态日报 — 2026-09-08

---

### 1. 今日速览

过去 24 小时项目活跃度极高：共有 13 条 Issue 更新（新增/活跃 12 条，关闭 1 条）和 48 条 PR 更新（其中 44 条待合并），并发布了 v1.45.0 新版本，标志着 TypeScript 客户端正式并入 monorepo，是 SDK 工程整合的重要里程碑。然而，发布管道存在隐患——v1.45.0 因签发 token 限制导致 TypeScript 与 PyPI 发布器均被跳过（见 Issue #4887），发布健康度受损。Bug 修复类 PR 占比很高，覆盖流式响应、文件编辑、并发与 MCP 重连等稳定性关键领域，但大量 PR 长期处于待审查状态（最早的 #3811 已挂载近 3 个月），评审积压是当前核心工程风险。社区侧，ACP 0.11 破坏性变更与第三方运行时依赖安全是讨论热度最高的两个话题。

---

### 2. 版本发布

**v1.45.0** ([链接](https://github.com/OpenHands/software-agent-sdk/releases))

主要变更：
- **feat: move TypeScript client into monorepo**（#4702）— TypeScript 客户端从独立仓库迁入本仓库统一管理，是工程整合的关键一步
- **feat(agent-server): add INSTALL_CAPABILITIES build arg**（#4698）— 为 agent-server 增加构建时可配置的能力安装选项
- **docs: refresh AGENTS.md** — 维护者指南更新

⚠️ **破坏性/关注事项**：本次发布触发了发布管道的疑似缺陷。据 Issue [#4887](https://github.com/OpenHands/software-agent-sdk/issues/4887) 报告：使用 `GITHUB_TOKEN` 创建的 Release **不会触发** 以下游 `release: published` 为监听事件的 workflow，导致 v1.45.0 的 TypeScript registry 发布器（两个）与 PyPI 发布器全部被跳过。目前发布流程中显式手动 dispatch 与监听器两种模式混用，需尽快统一。

---

### 3. 项目进展

**纯机器人 PR 动向：**
- #4707 (fix/glob): Python fallback 以 `root_dir` 限定搜索范围，替代进程级 `os.chdir`，修复并发场景下相对路径解析错乱问题 — [PR #4707](https://github.com/OpenHands/software-agent-sdk/pull/4707)
- #4772 (fix/sdk): 修复流式 wrapper 用过期 completion 覆盖新 yield 的 `ResponseCompletedEvent` 的缺陷（针对 #4679）— [PR #4772](https://github.com/OpenHands/software-agent-sdk/pull/4772)
- #4704 (fix/sdk): 异步 completions 改经 `RouterLLM.select_llm` 路由，修复异步场景模型选择不一致问题（修复 #4660）— [PR #4704](https://github.com/OpenHands/software-agent-sdk/pull/4704)
- #4799 (fix/events): WebSocket 客户端改为优先使用 Node 22 全局 `WebSocket`，移除 `ws` 依赖（对应 Issue #4846）— [PR #4799](https://github.com/OpenHands/software-agent-sdk/pull/4799)
- 另有 v1.45.0 发布相关的 #4702（TypeScript 客户端入 monorepo）与 #4698（agent-server 构建参数）已合并

**今日关闭的 Issue：**
- #4452（Agent Plugins 扩展命名空间映射）标记关闭（原设计需重新讨论方案） — [Issue #4452](https://github.com/OpenHands/software-agent-sdk/issues/4452)

整体而言，项目正式迈入 TS/Python 双端统一管理的新阶段，同时在流式事件模型、异步路由正确性上持续修补，稳定性和一致性方向推进明显。

---

### 4. 社区热点

**最热议题 Top 3：**

1. **[#4093] ACP 0.11 从 NewSessionResponse 移除 Gemini 模型状态字段**（评论 14）— [链接](https://github.com/OpenHands/software-agent-sdk/issues/4093)
   自 7 月 12 日创建以来讨论持续升温，至今仍未解决。核心冲突是：SDK 对 `agent-client-protocol` 只设下限无上限，而 ACP 0.11.0 移除了 `models` 不稳定字段，导致 Gemini CLI 0.46 的模型状态上报机制失效。这是典型的**上游依赖演进破坏兼容性**问题，至今未修复值得关注。社区诉求方向：要么锁定 ACP 版本上限，要么跟进新协议字段传递方式。

2. **[#4850] OpenCode 要求 LiteLLM 3 日内发送 x-opencode-session 头**（评论 5）— [链接](https://github.com/OpenHands/software-agent-sdk/issues/4850)
   第三方工具（OpenCode）对 LLM 网关提出专属 header 要求，而 OpenHands 通过 LiteLLM 间接依赖该通道、无对应 provider 配置。这实际是**供应链控制力问题**，与 #4880 同源：SDK 的能力正被第三方的临时性决定所绑架。

3. **[#4887] 发布 dispatch 流程待统一**（评论 3，今日创建）— [链接](https://github.com/OpenHands/software-agent-sdk/issues/4887)
   发布 v1.45.0 即暴露流程缺陷，引发生态工具链（PyPI/TypeScript registry）同步失败，社区关注度高，已获得 `priority:medium` 标记。

---

### 5. Bug 与稳定性

| 严重度 | Issue | 说明 | Fix PR 状态 |
|---|---|---|---|
| 🔴 高 | [#4887](https://github.com/OpenHands/software-agent-sdk/issues/4887) | 发布管道缺陷：GITHUB_TOKEN 释放不触发下游 workflow，v1.45.0 的 TS/PyPI 发布全部跳过 | 无 |
| 🔴 高 | [#4891](https://github.com/OpenHands/software-agent-sdk/issues/4891) |（今日新增）MCP server 不可达时 `create_mcp_tools()` 抛错阻断 `send_message`，LLM 未被调用对话即死 | 无 |
| 🟠 中 | [#4769](https://github.com/OpenHands/software-agent-sdk/issues/4769) | Responses 流式中，wrapper 的 stale 状态覆盖覆盖合法 `ResponseCompletedEvent` | ✅ [#4772](https://github.com/OpenHands/software-agent-sdk/pull/4772) |
| 🟠 中 | [#4837](https://github.com/OpenHands/software-agent-sdk/issues/4837) | 瞬时 HTTP 错误后 MCP 重建连接仍失败（nesting 计数器未归零） | 无 |
| 🟠 中 | [#4847](https://github.com/OpenHands/software-agent-sdk/issues/4847) | `RemoteConversation.fork()` 静默丢弃服务端返回的 title；测试 mock 的响应结构错误 | 无 |
| 🟠 中 | [#4668](https://github.com/OpenHands/software-agent-sdk/issues/4668) | 规划文件编辑器丢弃观察结果中的继承差异数据（仅复制 4/7 字段） | 无 |
| 🟠 中 | [#4664](https://github.com/OpenHands/software-agent-sdk/issues/4664) | OpenHandsCloudWorkspace resume 后仍在使用旧连接数据（key/URL 更新不生效） | 无 |
| 🟡 低 | [#4846](https://github.com/OpenHands/software-agent-sdk/issues/4846) | WebSocket 客户端在 Node ESM 环境忽略全局 WebSocket | ✅ [#4799](https://github.com/OpenHands/software-agent-sdk/pull/4799) |

---

### 6. 功能请求与路线图信号

- **[#4781] 服务端子对话工具**（`ready-for-dev`）— 将 Agent Canvas 的 `launch_child_conversation` 由客户端工具改为服务端实现，使同一后端的多客户端不再依赖浏览器副作用 — [链接](https://github.com/OpenHands/software-agent-sdk/issues/4781)。目前社区已有配套 PR #4822（StreamContext 流身份）与 #4700（StreamingDeltaEvent 去 Event 化），显示流式架构重构逐步推进
- **[#4850] 支持 OpenCode 等第三方 provider 的专属 header 透传** — 用户在 Issue 区讨论是否需要类似 `x-opencode-session` 的透传机制 — [链接](https://github.com/OpenHands/software-agent-sdk/issues/4850)
- **[#4880] 模型能力数据源收归自有**（`ready-for-dev`）— 将模型能力/价格表从 LiteLLM main 分支运行时拉取改为 SDK 内确定性维护 — [链接](https://github.com/OpenHands/software-agent-sdk/issues/4880)
- **[#4874] Cursor 作为内建 ACP provider**（PR，提交于 9 月 6 日）— 注册 Cursor CLI 的 ACP 协议支持。这是一项新工具集成，规格小巧、不膨胀镜像 — [PR #4874](https://github.com/OpenHands/software-agent-sdk/pull/4874)
- **[#4452] Agent Plugins 扩展命名空间映射**——已关闭但为“需要进一步设计”，恢复后需要继续推动 spec §8 的落地

---

### 7. 用户反馈摘要

- **MCP 故障时直接阻断对话是最伤体验的问题**：Issue #4891 用户报告“MCP server unreachable 导致 send_message 直接失败、LLM 从未被调用，会话相当于死亡”。用户预期：可选工具源不可用不应阻断主对话，需要优雅降级 — [链接](https://github.com/OpenHands/software-agent-sdk/issues/4891)
- **流式 API 的完成事件被丢弃是隐晦的数据一致性问题**：Issue #4769 描述了合法 completion 被 wrapper 的过期状态覆盖，该问题会影响依赖该事件的自动评估/工具循环。有 PR 修复但仍在栈中 9 天 — 用户希望类似数据丢失类 bug 优先合入
- **开发者认可好的小修**：PR #4875 作者在自托管部署中遇到了后台取消不掉的问题，二次确认修复有效才提交；#4406 作者则以“本地验证后送出 upstream”证明了 SDK 在 mcp 2.x 环境下的兼容缺口 — 开发者普遍以实际部署中复现的 bug 为驱动提交修复，问题可信、真实感强
- **版本发布工程质量正被社区密切观察**：v1.45.0 发布后立即有人跟进文档/发布器同时缺失的问题——用户对“发布即坏”的容忍度极低，这提醒项目维护者应尽快系统性修复触发式发布机制

---

### 8. 待处理积压

> ⚠️ 以下条目长期未获维护者响应或处于长时间待审查状态，建议优先安排 triage 与 review 资源。

**PR 积压（按等待时长排序）：**
| PR | 主题 | 创建 | 等待天数 |
|---|---|---|---|
| [#3811](https://github.com/OpenHands/software-agent-sdk/pull/3811) | fix(workspace): 为 `__del__` 方法增加部分构造实例保护 | 2026-06-20 | 80 天 |
| [#4135](https://github.com/OpenHands/software-agent-sdk/pull/4135) | 支持注入 WebSocketCallbackClient 工厂（可测试性改进） | 2026-07-17 | 53 天 |
| [#4183](https://github.com/OpenHands/software-agent-sdk/pull/4183) | fix: 子代理加载加密 LLM profile 时缺少服务端 cipher | 2026-07-22 | 48 天 |
| [#4322](https://github.com/OpenHands/software-agent-sdk/pull/4322) | fix(sdk): anyOf 非 null 类型选择时排除布尔 false | 2026-07-31 | 39 天 |
| [#4406](https://github.com/OpenHands/software-agent-sdk/pull/4406) | fix(tools): 在 MCP 2.x 下补 mcp 1.x Server 装饰器 shim | 2026-08-07 | 32 天 |

**Issue 积压：**
- [#4093](https://github.com/OpenHands/software-agent-sdk/issues/4093) ACP 0.11 兼容性破坏：7 月 12 日报告，14 条评论，已近 2 个月无修复抵达。在缺少版本上限控制的情况下，上游再次发版将扩大影响面
- [#4664](https://github.com/OpenHands/software-agent-sdk/issues/4664)、[#4668](https://github.com/OpenHands/software-agent-sdk/issues/4668)：8 月 27 日进入 `priority:medium` 但至今还未见到直接的 fix PR，两条bug都涉及数据字段保留问题，容易在工具链下层形成隐蔽的数据丢失

**质量观察**：44 个 PR 待合并，其中大量 PR 已标记 "ready-for-review" 并附带完整的手工验证描述——这将严重影响新特性的落地节奏，并可能打击外部贡献者提交高质量代码的意愿。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

## Pi 项目日报 — 2026-09-08

### 1. 今日速览

Pi 项目在过去 24 小时保持高活跃度：共 62 条 Issue 更新（新开/活跃 13 条，关闭 49 条）、26 条 PR 更新（待合并 10 条，关闭 16 条），无新版本发布。Issue 关闭率接近 79%，显示维护者清理积压效率良好，但仍有 #4945（openai-codex 连接可靠性，开放超 3 个月）这类长期问题悬而未决。社区热点集中在编码智能体稳定性（#4945/#5886）、Windows 平台支持（#7547）以及与 OpenCode Go 生态的兼容性修复（x-opencode-session 系列）。

---

### 2. 版本发布

过去 24 小时无新版本发布。

---

### 3. 项目进展

今日关闭的 16 条 PR 中，以下变更对项目推进较为关键：

- **Copilot GPT 模型路由修复** — [PR #9253](https://github.com/earendil-works/pi/pull/9253) 将 GitHub Copilot 的 GPT 系列模型从 `/chat/completions` 切换到 Responses API，修复了 `gpt-6-astra` 的 400 错误（issue #9209），并向未来兼容性迈出一步。
- **编码智能体手动重试 API** — [PR #9292](https://github.com/earendil-works/pi/pull/9292) 为 `coding-agent` 新增手动重试命令/API，弥补自动重试无法覆盖所有故障场景的缺口。
- **扩展流式支持** — [PR #9272](https://github.com/earendil-works/pi/pull/9272) 开放 `stream(...)` 与 `streamSimple(...)`，允许扩展从自定义 provider 流式调用（修复 #8964）。
- **Agent 循环错误传播修复** — [PR #9269](https://github.com/earendil-works/pi/pull/9269) 修复 `agentLoop()` 中未处理 Promise rejection 的问题，避免 OAuth 刷新失败等场景下静默异常。
- **交错用户内容修复** — [PR #8615](https://github.com/earendil-works/pi/pull/8615) 保留 `sendUserMessage()` 中原始文本/图片块顺序，覆盖消息从传达到流式处理全过程。
- **文档与质量基建** — [PR #9077](https://github.com/earendil-works/pi/pull/9077) 在 Containerization 文档新增 Docker Sandboxes 章节（对应 #8788）；[PR #9280](https://github.com/earendil-works/pi/pull/9280) 引入实现驱动的文档评估机制。
- **其他合并/关闭** — [PR #9278](https://github.com/earendil-works/pi/pull/9278) 更新仓库链接引用；[PR #5732](https://github.com/earendil-works/pi/pull/5732) 增加 `allowCommands` 扩展选项；[PR #256](https://github.com/earendil-works/pi/pull/256)（XDG Base Directory）和 [PR #9](https://github.com/earendil-works/pi/pull/9)（AGENTS.md 支持）等历史 PR 在今日关闭，推测已完成合并或归档。

整体来看，项目在响应 provider 生态变化（Copilot、OpenCode Go）上速度较快，同时对 `coding-agent` 的错误处理和扩展 API 有持续打磨。

---

### 4. 社区热点

- **[#4945 — openai-codex Connection Reliability Issues](https://github.com/earendil-works/pi/issues/4945)**（77 评论 · 33 👍 · OPEN）  
  自 5 月创建以来持续活跃，用户报告 `openai-codex`/`gpt-5.5` 会话反复卡在 `Working...` 状态，无文本、无工具调用、无报错，只能按 Esc 中断。积累的 33 个 👍 反映出影响的用户面较广。该问题不仅是稳定性 bug，也触及 TUI 交互层在流式场景下的反馈缺失，社区诉求强烈。

- **[#7547 — How do you use Pi on windows?](https://github.com/earendil-works/pi/issues/7547)**（61 评论 · 2 👍 · OPEN）  
  Windows 开发者的集中反馈帖，讨论 Pi 在 Windows 上的多种运行方式（原生、WSL、容器等）以及由此产生的碎片化体验。该贴由维护者 @petrroll 发起，本质上是一次公开的用户调研，目的是确定核心支持范围与文档优先级。

- **[OpenCode Go `x-opencode-session` 系列 Issues](https://github.com/earendil-works/pi/issues/9230)**（#9230 · #9290 · #9237 等，均在 24 小时内关闭）  
  OpenCode Go 从 2026-09-06 起强制要求请求携带 `x-opencode-session` header，导致 Pi 核心及社区扩展（如 pi-opencode-bridge）的请求失败。该类问题引发了 3–5 条相关 Issue，并催生了 [PR #9272](https://github.com/earendil-works/pi/pull/9272) 等修复。这反映了平台依赖外部服务时，上游 API 变更对下游项目的冲击速度之快。

- **[#6996 — Gemini 3.x thought_signature 失败](https://github.com/earendil-works/pi/issues/6996)**（9 评论 · CLOSED）  
  Gemini 3.x 模型在工具调用历史中缺少 `thought_signature` 导致请求失败，24 小时内关闭，属于外部 API 行为变化驱动的兼容性修复。

---

### 5. Bug 与稳定性

以下按严重程度排列（🔥 = 高优先级，⚠️ = 中优先级，💡 = 低优先级）：

| 严重级别 | Issue / PR | 描述 | 状态 |
|---|---|---|---|
| 🔥 | [#4945](https://github.com/earendil-works/pi/issues/4945) | openai-codex 连接反复卡死，无错误可恢复路径，持续超 3 个月 | OPEN，无 fix PR |
| 🔥 | [#9294](https://github.com/earendil-works/pi/issues/9294) | `claude-fable-5` 内置 `allowedFallbackModels` 包含已废弃的 `claude-opus-4-8`，导致 400 错误 | CLOSED，[PR #9297](https://github.com/earendil-works/pi/pull/9297) 已提出修复 |
| 🔥 | [#9276](https://github.com/earendil-works/pi/issues/9276) | `grep` 工具在 context > 0 时读取整个文件，导致 headless SDK 进程 OOM | CLOSED（待查证修复归属） |
| 🔥 | [#9298](https://github.com/earendil-works/pi/issues/9298)

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目日报 — 2026-09-08

## 1. 今日速览

过去 24 小时 Temporal Server 仓库活跃度处于中等偏上水平：3 条 Issue 更新、15 条 PR 更新，其中 13 条仍待合并、2 条已关闭。值得关注的是，Schedules 超过 2100 年限制问题（#9383）在沉寂数月后重新活跃，配套 PR #9396 也在推进中；Nexus/CHASM 与 SQL 存储后端相关 PR 占据当前开发量的较大比重。仓库正在为 1.32.0 准备 release branch（#11947），整体处于「版本发布前准备 + 功能迭代 + 稳定性加固」并行阶段。

## 2. 版本发布

过去 24 小时无正式版本发布。

需要注意：#11947（1.32.0: Prepare release branch）已关闭，说明 1.32.0 发布分支流程已经启动，正式版本可能即将进入 RC/GA 阶段。建议关注后续 changelog 中的破坏性变更与迁移说明。

## 3. 项目进展

### 今日关闭的 PR

- [**#11947**](https://github.com/temporalio/temporal/pull/11947) — `1.32.0: Prepare release branch`（@temporal-cicd[bot]）：覆盖 governance 文件并更新依赖，标记 1.32.0 发布流程正式启动。
- [**#11347**](https://github.com/temporalio/temporal/pull/11347) — `Allow registering new task queue types at the family limit`（@Shivs11）：修正任务队列 family 到达 `MaxTaskQueues` 上限时无法注册新 task queue type 的边界

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*