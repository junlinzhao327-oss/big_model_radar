# OpenClaw 生态日报 2026-09-15

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-15 00:42 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 · 2026-09-15

> 数据来源：github.com/openclaw/openclaw ｜ 统计窗口：过去 24 小时

---

## 1. 今日速览

- **高活跃、零发布**：24 小时内 Issues 与 PR 各更新 500 条（Issues 新开/活跃 314、关闭 186；PR 待合并 280、已合并/关闭 220），但**无新版本发布**，项目处于 2026.9.3 / 2026.9.4 发布后的密集修复与稳定化阶段。
- **更新/升级可靠性是绝对焦点**：今日 P0 级问题集中在升级链路（Windows 托管更新交接 #146860、runtime-verification 失败 #145510、多智能体 Codex 迁移崩溃循环 #123326），并有一个专门的发布稳定性跟踪帖 #145252。
- **性能与事件循环阻塞形成"规模化"主线**：多个 P1 反馈同步 SQLite/持久化阻塞 Gateway 事件循环（#119720、#97616），对应地，维护者今日集中提交/合并了一批"把工作搬进 shared worker"的重构型 PR（#148290、#148594、#148636、#148213）。
- **安全与消息泄漏类问题升温**：#25592（工具调用间文本泄漏到消息渠道，40 条评论）与 #102175（跨边界 prompt cache 失效）均需产品/安全评审，反映多租户与多渠道场景下的隔离风险。
- **维护者清理痕迹明显**：大量带 `stale` 标签的旧 Issue 今日被关闭，同时仍有一批高评论、长期挂起的 P2/P3 议题未解（详见第 8 节）。

**整体健康度判断**：贡献者与维护者响应速度高、修复密度大，但**升级路径的跨平台可靠性（Windows/macOS/FreeBSD）与事件循环阻塞**是当前拖累稳定性的两大结构性风险。

---

## 2. 版本发布

无新版本发布（最新 Releases 为空）。升级相关的稳定性跟踪见 [Issue #145252 [Tracking] 2026.9.3 / 2026.9.4 update, upgrade and recovery reliability](https://github.com/openclaw/openclaw/issues/145252)。

---

## 3. 项目进展（今日合并/关闭的重要 PR）

今日约 220 条 PR 被合并或关闭，主线可归纳为三类：

**A. 性能/架构：把同步工作移出调用线程（维护者 @steipete 主导）**
- [PR #148290 perf(fleet): run registry operations in SQLite workers](https://github.com/openclaw/openclaw/pull/148290) — 注册表读写、端口预留、租约变更移入 worker。
- [PR #148594 improve(cron): move data-only saves off the caller thread](https://github.com/openclaw/openclaw/pull/148594) — Cron 数据保存不再阻塞调用方。
- [PR #148636 perf(delivery): read failed queue counts in shared worker](https://github.com/openclaw/openclaw/pull/148636) — 出站死信健康统计异步化。
- [PR #148213 refactor(mcp): share scoped worker reads and batch requester status](https://github.com/openclaw/openclaw/pull/148213) — MCP OAuth 检查与 provider 准备工作批量化。

**B. 已合并/关闭的修复型 PR**
- [PR #148442 refactor: replace duplicated filesystem helpers with fs-safe](https://github.com/openclaw/openclaw/pull/148442) — 采用 fs-safe 0.11.0，消除重复文件系统代码。
- [PR #148327 fix(config): preserve whitespace in exec provider arguments](https://github.com/openclaw/openclaw/pull/148327) — 修复 `config set --provider-arg` 静默裁剪空白。
- [PR #148625 fix(doctor): stopped private inputs replay after session repair](https://github.com/openclaw/openclaw/pull/148625) — 防止已停止的私有子输入在 Doctor 迁移后被重放。
- [PR #148615 improve(memory): reduce session discovery work](https://github.com/openclaw/openclaw/pull/148615) — 减少 memory-core 冗余发现查询。
- [PR #148457 fix(test): restore broker routing and plugin test boundaries](https://github.com/openclaw/openclaw/pull/148457) — 恢复被破坏的主干 CI 契约。
- [PR #147634 fix(ui): don't classify attributed user messages as peer while viewer is unknown](https://github.com/openclaw/openclaw/pull/147634) — 修复 Web UI 消息左右跳变。

**C. 渠道稳定性**
- [PR #148638 fix(discord): prevent hangs during voice join cleanup](https://github.com/openclaw/openclaw/pull/148638)（P1，维护者）— 修复 Discord 语音加入清理期间的 Gateway 挂起。
- [PR #147988 fix(update): preserve FreeBSD pkg-owned files during self-update](https://github.com/openclaw/openclaw/pull/147988) — 自更新不再覆盖 `pkg` 管理的文件。

**进展评估**：今日无新

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目日报 — 2026-09-15

> 数据来源：[github.com/NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)｜统计窗口：

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报
**日期：2026-09-15** ｜ 数据源：github.com/OpenHands/software-agent-sdk

---

## 1. 今日速览

- 项目维持**高强度活跃**：24 小时内 31 条 Issue、50 条 PR 发生更新，但**零新版本发布**，处于"高输入、低产出"的密集开发阶段。
- 供需失衡明显：新开/活跃 Issue 27 条 vs 关闭 4 条；待合并 PR 41 条 vs 合并/关闭 9 条，**评审（Review）已是当前最大瓶颈**，而非开发产能。
- 今日关闭了高优先级 Bug **#4818（MCP OAuth 安装失败）**，同时 #2510（uv workspaces 的 Dependabot 支持调研）、#4519（Kubernetes 后端工作区）、#5009（自动化 API 缺口）等长期议题收口，说明设计层面的讨论在向落地转化。
- **安全与 Profile 秘密作用域**成为今日最集中的议题簇（#5025 / #5030 / #5014 / #5034），涉及死锁、密钥越权、Docker 运行时时序与私下披露渠道。
- 存在明显的**积压风险**：至少 7 条 2026-07 至 2026-08 创建的 Issue/PR 仍处于 Stale 状态且今日被"唤醒式"更新，提示社区贡献在等待维护者响应。

**健康度评估：活跃度优秀（A），吞吐能力承压（C+），维护者响应带宽是主要风险点。**

---

## 2. 版本发布

今日**无新版本发布**（Releases 为空），无破坏性变更与迁移事项需公示。

---

## 3. 项目进展

今日可见的合并/关闭动作以**依赖维护与议题收口**为主，功能推进增量有限（9 条 PR 合并/关闭中，展示区内仅见 2 条，均为 Dependabot）。

**已关闭的重要 Issue：**

| Issue | 类型 | 意义 |
|---|---|---|
| [#4818](https://github.com/OpenHands/software-agent-sdk/issues/4818) `priority:high, mcp, release-note-required` | Bug | `_BrowserCoordinatedOAuth.callback_handler` 返回 `tuple` 而 mcp 2.x 期望 `AuthorizationCodeResult`，导致 OAuth 同意后安装失败。关闭意味着 **MCP 2.x 迁移路线上一个高优先级阻断点被清除**，且带 `release-note-required` 标签，预计影响下一版本变更日志。 |
| [#2510](https://github.com/OpenHands/software-agent-sdk/issues/2510) `bug, priority:low` | Bug | 从 2026-03 追踪至今、累计 23 条评论的 uv workspaces × Dependabot 支持调研正式关闭，**monorepo 依赖自动化治理的不确定性消除**。 |
| [#4519](https://github.com/OpenHands/software-agent-sdk/issues/4519) `enhancement, ready-for-dev` | Feature | Kubernetes-backed workspace（基于 `kubernetes-sigs/agent-sandbox`）需求关闭，回应了"已有 K8s 集群的团队"这一空白场景。 |
| [#5009](https://github.com/OpenHands/software-agent-sdk/issues/5009) `enhancement, ready-for-dev` | Feature | 补齐既有 conversation/workspace API 的自动化缺口，验收项已勾选完成，**避免引入并行 AgentServerClient/RuntimeClient 层级**的架构约束被确立。 |

**已合并/关闭的 PR：**

- [#5063](https://github.com/OpenHands/software-agent-sdk/pull/5063) — `@types/node` 26.2.0 → 26.5.1（TS client）
- [#5066](https://github.com/OpenHands/software-agent-sdk/pull/5066) — `uvicorn` 0.37.0 → 0.52.4

**整体推进度判断**：功能性进展 ≈ 10%（4 个议题收口 + 2 个依赖升级），架构与安全方向的**设计共识**推进远快于代码落地。项目当前更像处于"路线图成型期"而非"交付冲刺期"。

---

## 4. 社区热点

**① [#2510 uv workspaces 的 Dependabot 支持调研](https://github.com/OpenHands/software-agent-sdk/issues/2510) — 23 条评论，👍1（今日关闭）**
全项目评论数最高。围绕 monorepo 中 root `pyproject.toml` 定义 `[tool.uv.workspace]` / `[tool.uv.sources]` 与成员包各自 `pyproject.toml` 的依赖解析，讨论持续近半年。背后诉求是**依赖更新自动化在多包仓库中不可靠**，直接影响贡献者体验与安全补丁时效。

**② [#4405 Agent Plugins 可移植包格式规范](https://github.com/OpenHands/software-agent-sdk/issues/4405) — 6 条评论，标签 `Needs Design`**
提议支持 `agent-plugins.org` 这一厂商中立的开放标准（v1.0.0 Working Draft，技术指导委员会含 Amazon、Cursor、Microsoft 等核心维护者）。这是**生态互操作性层面的

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报
**日期：2026-09-15** · 仓库：[earendil-works/pi](https://github.com/earendil-works/pi)

---

## 1. 今日速览

- 项目今日保持**高活跃度**：24 小时内落地 73 条 Issue 更新（关闭 54 / 新开或活跃 19）与 33 条 PR 更新（合并或关闭 11 / 待合并 22），**净关闭远大于净新增**，积压清理力度显著。
- 长期悬置的历史请求集中结清：2 月的 [#1391](https://github.com/earendil-works/pi/issues/1391)（多 OAuth 账户）与 5 月的 [#4423](https://github.com/earendil-works/pi/issues/4423)（切换 cwd 命令 API）均在今日关闭，说明维护者正在系统性收敛早期 RFC。
- Provider 生态继续扩张：GMI Cloud（[#9605](https://github.com/earendil-works/pi/pull/9605)）与 Google Antigravity（[#9594](https://github.com/earendil-works/pi/pull/9594)）两个 provider PR 今日落地，同时核心维护者 mitsuhiko 的 Node 运行时打包 PR（[#8474](https://github.com/earendil-works/pi/pull/8474)）合并，直指 Windows 启动性能。
- 稳定性仍是主要矛盾：**Bedrock/Anthropic 缓存计费失真**、**空白工具结果导致会话永久损坏**、**并发 `-c` 写入同一会话文件**等三类问题同时占据讨论榜前列，且多数尚无 fix PR。
- 今日**无新版本发布**，改动处于累积期，预计下一版本将包含 node 打包、多 provider 新增及一批计费修正。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日合并/关闭的 PR 覆盖了**性能、Provider 扩展、API 兼容性、基础设施**四条主线，整体向前推进明显：

### 性能与启动
- **[#8474](https://github.com/earendil-works/pi/pull/8474)（已合并）`feat(coding-agent): bundle Node runtime`** — 由 mitsuhiko 主导，改变 `pi-coding-agent` 打包方式，大幅减少加载文件数，重点解决 Windows Defender 拖慢 IO 导致的启动问题。这是今日**最高权重的合并**，直接影响所有 Windows 用户的首次交互延迟。
- **[#4318](https://github.com/earendil-works/pi/pull/4318)（已关闭）将 changelog ack 状态移出 `settings.json`** — 新增 `StateManager`（`~/.pi/agent/state.json`，带锁与写队列），使 `settings.json` 回归用户可 dotfiles 管理的纯配置，属于健康的基础设施重构。

### Provider 生态扩展
- **[#9605](https://github.com/earendil-works/pi/pull/9605)（已关闭）新增 GMI Cloud provider** — 复用 `openai-completions` 适配器，无需新 API 实现，接入成本极低。
- **[#9594](https://github.com/earendil-works/pi/pull/9594)（已关闭）新增仅 Gemini 的 Antigravity OAuth provider** — 恢复了此前被上游移除的订阅制 Gemini 访问路径，适配当前 provider 架构。

### API 兼容性修复
- **[#9589](https://github.com/earendil-works/pi/pull/9589)（已关闭）`fix(ai): type user input items in Responses API`** — 修复严格 Responses 端点报 `unsupported input item type: ""` 的 400 错误。
- **[#8732](https://github.com/earendil-works/pi/pull/8732)（已关闭）跨模型重放保留 `reasoning_content`** — 修复 DeepSeek 系 thinking 端点因缺失 reasoning 而拒绝请求的问题。
- **[#9584](https://github.com/earendil-works/pi/pull/9584) / [#9582](https://github.com/earendil-works/pi/pull/9582)（已关闭）** — 修复作用域内仅剩一个模型时 `Ctrl+P` 报 "Only one model in scope" 而不切换的回归。
- **[#9581](https://github.com/earendil-works/pi/pull/9581)（已关闭）提示模板 frontmatter 解析失败告警** — 直接对应 Issue [#9354](https://github.com/earendil-works/pi/issues/9354)，补齐了 skills 已有的诊断路径。
- **[#9604](https://github.com/earendil-works/pi/pull/9604)（已关闭）向调用方报告 shell 的 pid** — 为 headless server / 桌面端进程树管理提供扩展点。

**整体评估**：今日是典型的「高吞吐清理日」——合并的 PR 多为验证成熟的中小改动，无破坏性变更；真正决定下一版本体验的 [#8474](https://github.com/earendil-works/pi/pull/8474) 已落地，而 mitsuhiko 的两项架构级 PR（[#9548](https://github.com/earendil-works/pi/pull/9548) 会话内系统消息、[#6534](https://github.com/earendil-works/pi/pull/6534) developer role）仍在 OPEN，构成后续路线图的主要悬念。

---

## 4. 社区热点

### 讨论热度 Top 5

| 排名 | 条目 | 评论 | 状态 | 核心诉求 |
|---|---|---|---|---|
| 1 | [#8684](https://github.com/earendil-works/pi/issues/8684) `PI_OFFLINE` 静默禁用全部 provider 模型发现 | 8 | OPEN | 文档与行为严重不符 |
| 2 | [#9298](https://github.com/earendil-works/pi/issues/9298) Grok 403 被误标为 "OpenAI API error" | 7 | CLOSED | 错误归因误导排障 |
| 3 | [#8752](https://github.com/earendil-works/pi/issues/8752) Bedrock `usage.input` 未按模型族归一化 | 6 (👍5) | OPEN | 虚假 cache-miss 提示 + 输入成本翻倍 |
| 4 | [#9381](https://github.com/earendil-works/pi/issues/9381) pi-safe-compact 包安全报告 | 6 | CLOSED | 第三方包安全审查 |
| 5 | [#8720](https://github.com/earendil-works/pi/issues/8720) 纯空白工具结果永久损坏会话 | 6 | OPEN | 会话可用性硬伤 |

### 深度分析

**（1）配置语义与文档的信任缺口** — [#8684](https://github.com/earendil-works/pi/issues/8684) 是今日评论数最高的开放 Issue，且创建于 8 月 26 日、已持续近三周。用户 @mxr576 指出 `PI_OFFLINE` 被文档限定为「仅禁用启动期网络操作」，实测却禁用了整个会话的 provider 模型目录发现。这类「静默超范围生效」的配置项对离线/隔离环境用户尤其危险，因为故障表现为功能缺失而非报错。

**（2）成本透明度成为高共鸣话题** — [#8752](https://github.com/earendil-works/pi/issues/8752)（👍5）与 [#9457](https://github.com/earendil-works/pi/issues/9457)（👍4）同属 bedrock-converse 成本计算缺陷，都指向 `cacheWrite1h` 缺失导致按更贵的路径计费。加上 [#9210](https://github.com/earendil-works/pi/issues/9210)（Vercel AI Gateway 下 `cacheWrite1h` 恒为 0），**今日共有 3 条独立 Issue 指向同一类缓存计费失真**，且都来自不同作者的不同网关——这已不是个案，而是缓存写入计费模型在跨 provider 路径上的系统性缺陷，值得维护者作为统一主题处理。

**（3）第三方扩展生态的安全与边界** — [#9381](https://github.com/earendil-works/pi/issues/9381) 提交了对 `pi-safe-compact` 0.6.3 的恶意/不安全行为报告，反映了 Pi 的包生态已发展到需要安全审查流程的阶段。配套的扩展能力请求（[#9071](https://github.com/earendil-works/pi/issues/9071) 扩展工具无法覆盖内置工具、[#9434](https://github.com/earendil-works/pi/pull/9434) 允许扩展追加 system prompt）说明扩展 API 的**优先级与覆盖语义仍不清晰**。

---

## 5. Bug 与稳定性

按严重程度排列（🔴 严重 / 🟠 中等 / 🟡 轻微）：

### 🔴 会话级损坏与不可恢复

**1. [#8720](https://github.com/earendil-works/pi/issues/8720) — 纯空白工具结果永久损坏会话（OPEN，6 评论）**
工具返回仅含空白字符（如 Windows bash

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目日报 · 2026-09-15

> 数据来源：github.com/BerriAI/litellm｜统计窗口：过去 24 小时

---

## 1. 今日速览

- **整体活跃度：极高。** 过去 24 小时 PR 更新 283 条、Issue 更新 61 条，对于单体 LLM 网关项目属于高强度开发节奏，且 0 个新版本发布，说明主要精力集中在主分支合流而非发版。
- **合并效率偏低：** 283 条 PR 中 199 条仍待合并、84 条已合并/关闭，待处理队列约为已完成量的 2.4 倍，review 吞吐可能成为瓶颈。
- **Issue 侧以"未解决的老问题被重新激活"为主**——48 条新开/活跃 vs 13 条关闭，且今日活跃榜前几名多为跨月甚至跨年的长尾 Issue。
- **主题聚焦：** 计费/用量核算准确性（budget、spend、cache token）、Responses↔Chat 桥接转换、限流与路由健康度是今日讨论密度最高的三条主线。
- **健康度提示：** 无新版本、无破坏性变更风险；但存在多个"静默错误计算"类 Bug（spend 归零、限流减半），建议优先处理。

---

## 2. 版本发布

今日无新版本发布，无破坏性变更与迁移事项。

---

## 3. 项目进展

> 说明：本次样本仅展示评论数最多的 20 条 PR，其中绝大多数仍为 OPEN 状态，以下为样本内可见的推进信号。

**已完成/关闭：**

- **[#40702] feat(model_armor): logging_only 模式在流式响应投递后扫描**（已关闭）
  解决了 Model Armor `post_call` 必须缓冲整个流、导致首 token 延迟等于总生成时间的性能问题，并新增 `mode: logging_only` 配置。这是今日样本中唯一明确闭环的功能项。
  https://github.com/BerriAI/litellm/pull/40702

**在途的重要 PR（尚未合并，构成下一版主要增量）：**

| PR | 方向 | 价值 |
|---|---|---|
| [#41155](https://github.com/BerriAI/litellm/pull/41155) | 用量聚合查询按 top key 限制 rollup | 修复大规模部署下 Admin Usage 页 500 + Prisma 引擎 OOM（10k key 场景 30GB RSS） |
| [#40894](https://github.com/BerriAI/litellm/pull/40894) | 网关侧管理员托管的持久化 Memory | 默认关闭，管理员可按用户/全员开启，降低应用侧编排成本 |
| [#41128](https://github.com/BerriAI/litellm/pull/41128) | `llm_as_a_judge` 支持 `pre_call` / `during_call` | 补齐此前只支持 `post_call` 的能力缺口 |
| [#38241](https://github.com/BerriAI/litellm/pull/38241) | Microsoft Agent 365 MCP 工具调用护栏 | 让 MCP 工具调用经 Defender 治理与审计 |
| [#41039](https://github.com/BerriAI/litellm/pull/41039) | 用户/团队成员批量删除 API（≤500 条） | 补齐离职批量清理场景 |
| [#41134](https://github.com/BerriAI/litellm/pull/41134) | 模型弃用前 30/7/0 天邮件通知团队管理员 | 从 Slack 广播升级为定向通知 |
| [#36741](https://github.com/BerriAI/litellm/pull/36741) | Langfuse callback 迁移至 v4 SDK | 修复 `langfuse>=4` 下所有回调失败（**已搁置约 1 个月**） |
| [#41151](https://github.com/BerriAI/litellm/pull/41151) / [#41148](https://github.com/BerriAI/litellm/pull/41148) / [#41154](https://github.com/BerriAI/litellm/pull/41154) | Gemini/Vertex/Fireworks/Nova 定价修正 | 修复 gemini `-latest` 别名仍按旧代价格计费的问题 |

**整体推进评估：** 今日增量以"计费准确性 + 运维规模化 + 护栏能力扩展"三条线并行推进，属于质量巩固型迭代，而非新功能爆点；但由于 199 条 PR 积压，实际落地速度低于开发速度。

---

## 4. 社区热点

按评论数与反应数排序：

1. **[#34281] [Bug] Health Checks 应优雅失败**（13 评论）
   https://github.com/BerriAI/litellm/issues/34281
   HomeLab 用户在主机离线时健康检查硬失败。诉求：探测类请求不应污染正常服务错误面。**这是典型的"小场景、高共鸣"问题，适合低成本修复。**

2. **[#10788] [Bug] LiteLLM Proxy 的 INFO 请求日志无法关闭**（13 评论，1 👍，**创建于 2025-05-13**）
   https://github.com/BerriAI/litellm/issues/10788
   用户期望 `LITELLM_LOG=ERROR` 生效但无效，日志被请求行淹没。**悬置 16 个月仍未解决**，是当前社区情绪的重要来源。

3. **[#27735] [Bug] 虚拟 Key 的 BudgetExceededError 使用过期 spend**（12 评论，1 👍）
   https://github.com/BerriAI/litellm/issues/27735
   管理 API 显示 spend 未超预算，但请求被拒。**计费一致性信任问题**，直接冲击用户对配额体系可靠性的信心。

4. **[#34140] v3 限流器对 team×model 限额双重计数，实际 RPM/TPM 只有配置值的一半**（7 评论）
   https://github.com/BerriAI/litellm/issues/34140
   提交者附了精确复现与根因定位（`model_per_team` 路径）。**这类"静默打折"Bug 在容量规划场景下影响极大。**

5. **[#30301] [Feature] 加固 provider transform，防止 LiteLLM 内部 optional_params 泄漏进请求体**（6 评论）
   https://github.com/BerriAI/litellm/issues/30301
   这是一个**类问题（failure class）总纲式提案**，指出多个字段被转发后被严格 provider 拒绝的共性根因。

6. **[#39057] 缓存命中时 spend 归零但 token 列回放原始用量——报表该以哪个口径聚合？**（6 评论）
   https://github.com/BerriAI/litellm/issues/39057
   属于**语义边界讨论**，来自 agent-telemetry 计费审计场景，反映用户对"可解释计费"的需求上升。

**热点分析：** 今日社区讨论已从"功能要什么"明显转向"账目对不对、限流准不准"。这是项目进入生产深水区的典型信号——用户基数已足够大，**正确性与可观测性的优先级正在超过新能力**。

---

## 5. Bug 与稳定性

按严重程度排列（🔴 严重 / 🟠 中等 / 🟡 轻微）：

### 🔴 计费与配额正确性（静默错误，影响资金口径）

| Issue | 问题 | Fix PR |
|---|---|---|
| [#39370](https://github.com/BerriAI/litellm/issues/39370) | reset-budget 任务无法自愈 `budget_duration=null` 但 `budget_reset_at` 非空的脏行，**每次 tick 静默清零 spend，永久循环** | 未见 |
| [#27735](https://github.com/BerriAI/litellm/issues/27735) | BudgetExceededError 使用过期 spend，与实际不符 | 未见 |
| [#40649](https://github.com/BerriAI/litellm/issues/40649) | Admin UI 编辑模型持久化派生定价后，Azure spend 被记为 $0 | 未见 |
| [#40736](https://github.com/BerriAI/litellm/issues/40736) | 流式 usage 合并器在显式置零后仍保留陈旧的 cache-write token | 未见 |

### 🔴 限流与路由

| Issue | 问题 | Fix PR |
|---|---|---|
| [#34140](https://github.com/BerriAI/litellm/issues/34140) | v3 限流器对 team×model 限额双重计数，有效配额减半 | 未见 |
| [#28216](https://github.com/BerriAI/litellm/issues/28216) | `Router.aresponses` 流式路径绕过 `MidStreamFallbackError`，跨 provider fallback 不触发（生产环境已复现） | 未见 |

### 🟠 转换与协议桥接

| Issue | 问题 | Fix PR |
|---|---|---|
| [#40887](https://github.com/BerriAI/litellm/issues/40887) | Responses→Chat 流式丢失 reasoning 进度与缓存推理状态 | 未见 |
| [#40654](https://github.com/BerriAI/litellm/issues/40654) | 桥接在流式/非流式下丢弃原始 `reasoning_text` | 未见 |
| [#30539](https://github.com/BerriAI/litellm/issues/30539) | 无工具请求被转发 `tools: []`，vLLM 返回 422 | 未见 |

### 🟠 依赖与运行时

- [#29268](https://github.com/BerriAI/litellm/issues/29268) — Docker 镜像仍捆绑 `ddtrace 2.19.0`，在 Python 3.13 + APM 下 `/embeddings` 完全不可用。**该问题在 #8744 被 stale 机器人误关后复发**，存在流程性隐患。

### 🟡 已闭环

- ✅ [#26552](https://github.com/BerriAI/litellm/issues/26552) `/v1/images/edits` + mask 的 streaming 请求内容访问错误（已关闭，5 评论 / 3 👍）
- ✅ [#38401](https://github.com/BerriAI/litellm/issues/38401) Bedrock Realtime 早于 provider 就绪即确认会话（已关闭）
- ✅ [#25940](https://github.com/BerriAI/litellm/issues/25940) Langfuse 回调 `AttributeError`（已关闭）
- ✅ [#41029](https://github.com/BerriAI/litellm/issues/41029) Admin UI 侧边栏导航触发整页重载与 404 预取风暴（当日开、当日关，响应迅速）

### 🟡 其他

- [#40979](https://github.com/BerriAI/litellm/issues/40979) `_get_user_agent_tags` 的 User-Agent 头查找未做大小写归一化
- [#17993](https://github.com/BerriAI/litellm/issues/17993) 大时长值（秒/分/时）因跨日边界导致预算重置时间计算错误
- [#27849](https://github.com/BerriAI/litellm/issues/27849) 批量邀请生成的 access token 缺少 `sk-` 前缀，调用被拒
- [#30008](https://github.com/BerriAI/litellm/issues/30008) 自定义脱敏标签配置在 v1.87.1 不生效

> **稳定性结论：** 今日**没有任何一条严重 Bug 有对应的公开 Fix PR**。计费类静默错误的修复缺口是最需要立即补位的方向。

---

## 6. 功能请求与路线图信号

| 需求 | Issue | 对应在途 PR | 入选下一版可能性 |
|---|---|---|---|
| 上游配额/余额主动探测 SDK 接口 | [#34734](https://github.com/BerriAI/litellm/issues/34734) | 无 | 中 — 需求明确（capability-based），但无实现 |
| Request Log / Usage 按 Project 过滤 | [#40386](https://github.com/BerriAI/litellm/issues/40386) | 无（但 #41155 正在重构同查询） | 中高 — 与用量查询重构同源，可顺势落地 |
| 暴露结构化

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*