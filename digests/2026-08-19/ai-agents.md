# OpenClaw 生态日报 2026-08-19

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-18 22:36 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-19

> 数据来源：github.com/openclaw/openclaw | 统计窗口：过去 24 小时


## 1. 今日速览

过去 24 小时内，OpenClaw 仓库保持着高强度的社区活跃度：累计 **500 条 Issue 更新**（新开/活跃 461 条，关闭 39 条）与 **500 条 PR 更新**（待合并 337 条，已合并/关闭 163 条），合并/关闭率达 32.6%。值得关注的是，今日有 **8 个新 PR 集中提交**（#126017、#126013、#126043、#126048、#126052、#126051、#126030、#126054），涵盖 Heap OOM 崩溃修复、Web UI 模型发现、会话目录去重/精简、控制台国际化等方向；同时 **#126055（发布验证流程精简）与 #126043（命名 CLI 会话侧边栏可见性）已直接合并**，表明维护者正在同时推进稳定性修复与 UI/发布体验优化，并保持快速响应。此外，一批长期积压的 P1/diamond-lobster 级 Bug（如 #62505、#83959、#94939、#91144 等）仍处于待审状态，修复积压是当前项目健康度的主要短板。

**活跃度评级：高** —— 24 小时内 1000 条 Issue/PR 更新、8 个新 PR、2 个快速合并，社区讨论与提交均十分活跃。


## 2. 版本发布

过去 24 小时内无新版本发布（最新 Releases：无）。

当前处于 **2026.8.1-beta.2 之后的 beta 周期**，从今日 PR 可观察到维护者正在为下一版本做稳定性收敛：包括 #126055「release: streamline validation setup」（已合并，加速 beta/gateway 发布验证）、#126053「refactor: consolidate meeting and media provider families」、#126030「refactor(canvas): make the panel a widget presenter」（大规模重构，涉及 android/ios/macos/linux/web-ui 全端）等合并候选。此外 #125424（隐藏 OpenClaw 托管的 provider 会话）、#125983（从 session rows 移除客户端可见的 activeRunIds）等 XL 级重构 PR 均处于待审/待作者更新状态，预计将随下一个 beta 版本发布。

**发布前瞻**：当前没有已发布的版本，但 8 个新 PR + 3 个重构/清理类 XL PR 正在排队，下一个 beta 版本可能包含媒体策略安全修复（#125950）、Base64 附件 OOM 修复（#126017）、动态模型发现修复（#126013）等关键补丁。


## 3. 项目进展

今日有 **163 个 PR 被合并/关闭**。以下为其中值得关注的重要 PR（含今日新合并）：

### ✅ 已合并（直接推进项目）

| PR | 标题/内容 | 状态 | 说明 |
|---|---|---|---|
| [#126055](https://github.com/openclaw/openclaw/pull/126055) | fix(release): streamline validation setup | ✅ 已合并 | 维护者直接请求合并。加速 beta/gateway 发现流程、改进本地 worksheet 可用性、增加可见的进度指示与测试人员引导——**提升未来所有版本的发布效率** |
| [#126043](https://github.com/openclaw/openclaw/pull/126043) | fix: show named CLI sessions in the sidebar | ✅ 已合并 | 修复 `openclaw agent --session-key <key>` 创建的命名 CLI 会话不出现在 Control UI 侧边栏的问题。改善 CLI 与 Web UI 的会话可见性一致性 |
| [#120900](https://github.com/openclaw/openclaw/pull/120900) | feat(ui): review install policy warnings | ✅ 已关闭 | 允许管理员在 Control UI 中查看安装策略警告并决定是否继续安装插件。与 #116489 配套，构成完整的安全安装审查链路 |
| [#116489](https://github.com/openclaw/openclaw/pull/116489) | feat(security): require acknowledgement for install policy warnings | ✅ 已关闭 | 安全策略安装警告确认机制——外部 `security.installPolicy` 命令可返回 `warn`，交互式 CLI 安装时要求操作者输入确切的插件名确认，防止误装可疑插件 |

### 🚧 关键待合并 PR（方向性信号）

| PR | 标题/内容 | 状态 | 影响 |
|---|---|---|---|
| [#125707](https://github.com/openclaw/openclaw/pull/125707) | fix(codex): report native thread reasoning effort | 👀 待维护者查看（P1） | Codex 线程推理力度（reasoning effort）的持久化与通知捕获 |
| [#125950](https://github.com/openclaw/openclaw/pull/125950) | fix(media): honor sender tool policy for outbound file reads | ⏳ 等待作者（P1） | 安全边界修复——`toolsBySender` deny 规则未覆盖模型所选本地文件附件 |
| [#126017](https://github.com/openclaw/openclaw/pull/126017) | fix: large base64 attachments on /v1/responses crash the gateway with heap OOM | 👀 待维护者查看（P1） | 修复客户端发送大型 base64 附件导致网关进程堆内存溢出崩溃（FATAL ERROR） |
| [#126013](https://github.com/openclaw/openclaw/pull/126013) | fix(ui): New Session misses dynamically discovered models | 📣 需要 proof（P2） | Web UI「新会话」无法显示动态发现的模型——与 #10687 动态模型发现路线直接相关 |
| [#125983](https://github.com/openclaw/openclaw/pull/125983) | refactor(sessions): drop client-visible activeRunIds from session rows | ⏳ 等待作者（P1，XL） | 协议精简：session rows 中移除从未被客户端使用、可能不一致的 activeRunIds 字段 |

**整体判断**：项目在三个方向上稳步推进——① 发布工程/工具链效率（#126055）；② 安全边界加固（#116489、#120900、#125950、#123848）；③ 会话系统架构清理（#125424、#125983、#126043）。这些改动体现了从「功能扩张」到「稳定性与安全收敛」的阶段性侧重。


## 4. 社区热点

今日讨论最活跃的 Issues 主要集中在 **会话状态/消息丢失** 与 **回归类 Bug** 两大主题。以下按评论数和社区关注度排序：

### 🥇 热门 Issue 榜

| Issue | 标题 | 评论 | 热度分析 |
|---|---|---|---|
| [#80319](https://github.com/openclaw/openclaw/issues/80319) | QA tool-defaults suite conflates Codex-native tools with OpenClaw dynamic tool parity | 17 | 评论数最高。QA 测试套件将 Codex 原生工具与 OpenClaw 动态工具混为一谈，原报告夸大问题但纠正后属于测试框架问题。反映出社区对 **Codex 工具兼容性** 的高度关注 |
| [#112423](https://github.com/openclaw/openclaw/issues/112423) | Large SQLite transcript cleanup blocks the gateway event loop | 15 | 大型 SQLite 转录清理阻塞网关事件循环——**性能类 Bug 引发广泛共鸣**，升级后 SQLite 仓储的规模化问题正在显现 |
| [#62505](https://github.com/openclaw/openclaw/issues/62505) | Coding Agent never completes anything (worked in 2026.4.2 and earlier) | 15 | **严重回归**：编码 Agent 完全不工作，且被标记为 `clawsweeper-recovery-stuck`（恢复卡死）。发布 4 个多月仍未修复，社区用户持续跟进 |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | "Cannot convert undefined or null to object" in 2026.3.2 with google-vertex/gemini-3.1-pro-preview | 14 | 老问题但仍有高热度（👍3），google-vertex 认证提供者的兼容性问题长期未解决 |
| [#79902](https://github.com/openclaw/openclaw/issues/79902) | Add companion-friendly SQLite transcript/session seams on top of database-first runtime | 14 | 特性讨论 + 数据库优先架构下的扩展性诉求，与 #112423 的 SQLite 性能问题形成呼应 |

### 🔥 社区诉求背后的信号

1. **SQLite 迁移阵痛**：#112423、#79902、#94939、#90378 等 Issue 显示，2026.5→6.x 的 SQLite 迁移虽然方向正确，但 **性能（事件循环阻塞）、数据兼容性（0 字节 store）、配置迁移（cron 默认值）** 问题集中爆发。社区对 database-first 架构的方向认同，但对迁移的平滑度和运行时稳定性明显不满。

2. **Coding Agent 可靠性**：#62505（15 评论）与 #84516（13 评论）表明，**Codex/编码 Agent 核心场景的可靠性** 是社区最敏感的痛点——「worked before, now fails」的回归最容易引发长期持续关注。

3. **P1 + diamond lobster 组合的 High-Severity 问题**：当前共有约 10+ 个同时标注 `P1` + `🦞 diamond lobster`（最高严重度）的 Issue 处于 OPEN 状态（#62505、#40001、#83959、#94939、#91144、#90098、#90378、#117609、#88032、#88079、#62328、#91941 等），这些是社区最希望维护者优先处理的「硬骨头」。


## 5. Bug 与稳定性

过去 24 小时内报告的 Bug 与稳定性问题中，以下按严重程度排列（P1 = 高，P2 = 中，P3 = 低）：

### 🔴 P1 — 高严重度

| Issue | 标题 | 状态 | Fix PR |
|---|---|---|---|
| [#124788](https://github.com/openclaw/openclaw/issues/124788) | beta.2 gateway: event loop blocks ~100s every ~10 min | 🆕 新报告（8/16创建，6评论） | 无 — 锚定定时器 + 字符串构建 + fs 扫描；禁用所有 memory 插件仍复现 |
| [#40001](https://github.com/openclaw/openclaw/issues/40001) | Write tool lacks append mode — isolated cron sessions destroy shared files | OPEN（diamond lobster，12评论） | 无 — 需要产品决策；数据丢失风险高 |
| [#62505](https://github.com/openclaw/openclaw/issues/62505) | Coding Agent never completes anything (regression) | OPEN（diamond lobster，15评论，stuck） | 无 — 自 4 月提出至今未修复 |
| [#83959](https://github.com/openclaw/openclaw/issues/83959) | Codex app-server startup retries can exhaust before replacement server ready | OPEN（diamond lobster，11评论，stuck） | 有 linked PR 但未合入 |
| [#94939](https://github.com/openclaw/openclaw/issues/94939) | 6.x state migration leaves channel conversation-store SQLite empty (0 bytes) | OPEN（diamond lobster，8评论，stuck） | 有 linked PR 但未合入 — MS Teams 主动消息（proactive）发送中断 |
| [#91144](https://github.com/openclaw/openclaw/issues/91144) | Windows native CLI gateway Scheduled Task does not stay running | OPEN（diamond lobster，8评论，stuck） | 有 linked PR 但未合入 |
| [#90098](https://github.com/openclaw/openclaw/issues/90098) | Stack-safe large attachment handling for Control UI and gateway | OPEN（diamond lobster，8评论，stuck） | 有 linked PR 但未合入 — 大 PDF 导致 RangeError 栈溢出 |
| [#90378](https://github.com/openclaw/openclaw/issues/90378) | 5.28 → 6.1 cron store migrated to SQLite silently; new jobs default to delivery.mode=announce | OPEN（diamond lobster，8评论，stuck） | 有 linked PR 但未合入 |
| [#117609](https://github.com/openclaw/openclaw/issues/117609) | Transient LLM/socket errors not retried at embedded-assistant stage (long turns die whole) | OPEN（diamond lobster，8评论） | 有 linked PR 但未合入 |
| [#103231](https://github.com/openclaw/openclaw/issues/103231) | claude-cli backend: ownsNativeCompaction assumption is false — sessions grow past 200% context | ✅ 已关闭 | 已解决 — 社区确认修复 |

### 🟡 P2 — 中严重度（节选）

| Issue | 标题 | 状态 | Fix PR |
|---|---|---|---|
| [#88657](https://github.com/openclaw/openclaw/issues/88657) | DeepSeek V4 Flash incomplete turn (payloads=0, tools=2) in 2026.5.27/28 | OPEN（11评论） | 无 |
| [#84516](https://github.com/openclaw/openclaw/issues/84516) | Codex app-server: long agent replies silently truncated at ~1000-1100 chars | OPEN（13评论） | 无 |
| [#112423](https://github.com/openclaw/openclaw/issues/112423) | Large SQLite transcript cleanup blocks the gateway event loop | OPEN（15评论） | 无 |
| [#88079](https://github.com/openclaw/openclaw/issues/88079) | WebChat: reasoning_content not streamed for Kimi Code & DeepSeek Reasoner | OPEN（7评论） | 有 linked PR 但未合入 |
| [#92186](https://github.com/openclaw/openclaw/issues/92186) | Foreground reply fence cancels delivery of completed replies to earlier concurrent group messages | OPEN（6评论） | 无 — `not-repro-on-main` |
| [#91892](https://github.com/openclaw/openclaw/issues/91892) | Cron jobs stall during AI model calls (model_call:stream_progress never completes) | OPEN（7评论，stuck） | 无 |
| [#102534](https://github.com/openclaw/openclaw/issues/102534) | Cron scheduler timer permanently stops firing after heavy timeouts | OPEN（6评论，stuck） | 无 |
| [#125679](https://github.com/openclaw/openclaw/issues/125679) | Matrix channel never completes initial sync — infinite restart loop（已 bisect 到 #125302） | 🆕 新报告（8/18） | ✅ [#123931](https://github.com/openclaw/openclaw/pull/123931) — fix(matrix): recognize room version 12 room IDs（已提交，等待作者） |

### 🟢 今日新引入 Bug 摘要

- **#125679（Matrix 无限重启循环）**：8/18 当天新报告，已精确 bisect 到 #125302 的回归，且已有对应修复 PR #123931——**这是今日唯一有完整「报告→定位→修复」链路的新 Bug**。
- **#124788（beta.2 事件循环阻塞 100 秒/10 分钟）**：8/16 报告的 beta 回归，6 评论跟进中，暂无 fix PR，属于最新版本（2026.8.1-beta.2）特有的高风险问题。

**稳定性总结**：今日无新崩溃级 Bug（除 #126017 修复的 OOM 问题恰好是昨天报告的 #126015）。但 **P1 级修复积压严重**——至少 9 个 diamond-lobster 级 P1 Issue 仍无 fix PR 合入，且多个被标记为 `clawsweeper-recovery-stuck`（恢复机制本身卡死）。好消息是 #103231（claude-cli 压缩路径假阳性）今日已关闭，说明攻坚型修复仍在推进。


## 6. 功能请求与路线图信号

### 今日新增功能请求

| Issue | 标题 | 可能纳入下一版本？ | 理由 |
|---|---|---|---|
| [#125679](https://github.com/openclaw/openclaw/issues/125679) | Matrix room version 12 兼容 | ⭐ 几乎确定 | 已有对应 fix PR #123931（`fix(matrix): recognize room version 12 room IDs`），且 P1 优先级 |
| [#126013](https://github.com/openclaw/openclaw/pull/126013) | New Session 支持动态发现的模型 | ⭐ 很可能 | 直接对接 #10687 动态模型发现路线，已有对应 PR 提交 |
| [#125424](https://github.com/openclaw/openclaw/pull/125424) | 隐藏 OpenClaw 托管的 provider 会话 | ⭐ 很可能 | 会话目录架构清理的一部分，P2 + XL 规模 |
| [#125983](https://github.com/openclaw/openclaw/pull/125983) | 移除 session rows 中的 activeRunIds | ⭐ 很可能 | 协议精简，避免不一致状态，P1 优先级 |

### 中长期路线图信号（来自既有活跃 Issue）

1. **动态模型发现（#10687）**：持续获得关注（👍3、9 评论），且今日 #126013 PR 直接推进了 Web UI 侧的动态模型支持。**这是明确的路线图方向**，OpenRouter 等快速更迭的模型目录已让静态 catalog 模式不可持续。

2. **SQLite transcript/session 可组合性（#79902）**：社区希望在 database-first runtime 之上提供规范的 SQLite 访问层，而非「爬取不透明 blob」。与 #112423（SQLite 清理性能）形成「功能需求 + 性能缺陷」的组合，**下一版本大概率会对 SQLite 层做重构或性能优化**。

3. **记忆系统去重（#95724）**：多个 Agent 共享同一

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-19

> 数据窗口：2026-08-18 至 2026-08-19 | 数据来源：github.com/NousResearch/hermes-agent

---

## 1. 今日速览

项目处于**极高度活跃**状态：过去 24 小时共有 419 条 Issue 更新（其中 361 条新开/活跃、58 条关闭）和 500 条 PR 更新（其中 119 条已合并/关闭、381 条待合并

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

### OpenHands SDK 项目动态日报 — 2026-08-19

---

#### 1. 今日速览

过去24小时项目保持高度活跃：Issue 与 PR 更新合计达 39 条，其中 PR 更新 27 条（含 6 条合并/关闭），显示出持续的迭代节奏。当前开发重心明显偏向 **LLM 交互正确性**（消息序列化、推理内容泄漏、会话恢复丢消息）、**基础设施与隐私合规**（部署标识、持久化路径）、以及 **账号/凭据管理架构**（provider 连接存储）。此外，测试体系建设（边界测试、无用测试清理）与自动化运维（依赖更新）也有不少投入。今日无新版本发布，但多项修复与功能 PR 合并，整体健康度良好，技术债清理与功能推进并进。

---

#### 2. 版本发布

今日无新版本发布。

---

#### 3. 项目进展

今日共合并/关闭 6 个 PR，其中多个是关键修复或功能奠基：

- **`#4455` [CLOSED] Backend: Model providers — provider store + nested models + named-secret key** — 这是 provider 架构的基础 PR，为"一次连接、多次使用"的 provider 模型铺路，并作为其他相关 PR 的阻塞项，合入后有望推动 provider 管理功能落地。链接: https://github.com/OpenHands/software-agent-sdk/pull/4455

- **`#4507` [CLOSED] fix(agent-server): invalidate cached ConversationInfo on metadata-only updates after idle eviction** — 修复了空闲驱逐后元数据更新导致缓存不一致的问题，提升 agent-server 的会话管理稳定性。链接: https://github.com/OpenHands/software-agent-sdk/pull/4507

- **`#4522` [CLOSED] feat: Add deployment kind to agent-server telemetry** — 为 telemetry 添加部署类型标签，是 issue `#4523` 的配套实现，支持区分远程托管与本地自托管。链接: https://github.com/OpenHands/software-agent-sdk/pull/4522

- **`#4344` [CLOSED] feat(sdk): add cleanup LLM profile for outward agent text** — 增加清理用 LLM profile，用于修正对外消息（Slack/GitHub）的乱码或风格问题，是对社区需求的直接回应。链接: https://github.com/OpenHands/software-agent-sdk/pull/4344

- **`#4435` [CLOSED] fix(settings): inherit condenser max_tokens from LLM effective_max_input_tokens** — 修复了 condenser 的 max_tokens 未继承模型限制的 bug，解决了 issue `#3746`。链接: https://github.com/OpenHands/software-agent-sdk/pull/4435

- **`#4518` [CLOSED] chore(deps-dev): bump pillow from 12.2.0 to 12.3.0** — 例行依赖更新，保持生态安全与兼容。链接: https://github.com/OpenHands/software-agent-sdk/pull/4518

> **整体判断**：今日合并内容覆盖架构、bug 修复、telemetry 与依赖管理，项目在多条线上稳步推进。

---

#### 4. 社区热点

以下 Issue/PR 在今日讨论最活跃，反映了社区关注焦点：

- **`#4511` [Bug] `Message.to_chat_dict` emits `cache_control` when caching is disabled** — 3 条评论，是今日评论最多的 Issue，已有对应修复 PR `#4512`。链接: https://github.com/OpenHands/software-agent-sdk/issues/4511

- **`#4530` [Bug] LLM-generated conversation titles leak raw `<think>` reasoning blocks** — 2 条评论，讨论推理模型返回原始思考块导致标题泄漏的问题，已有关联修复 PR `#4534`。链接: https://github.com/OpenHands/software-agent-sdk/issues/4530

- **`#4532` [Bug] Reopening a confirmation-paused conversation drops the assistant tool_use message** — 高优先级 bug，涉及会话恢复后 LLM 请求缺失 tool_use 消息，被提供商拒绝。链接: https://github.com/OpenHands/software-agent-sdk/issues/4532

- **`#4533` [Bug] Conversation launch drops LLM api_key when the seeded `default` agent profile is active** — 自托管用户反馈的认证错误，凸显本地部署的易用性问题。链接: https://github.com/OpenHands/software-agent-sdk/issues/4533

- **`#4528` [Enhancement] Tell agents where to find previous local conversations** — 社区希望 agent 的默认提示词能指引本地历史会话存储位置，已由 PR `#4527` 实现并合入。链接: https://github.com/OpenHands/software-agent-sdk/issues/4528

**分析**：今日热点集中在 **LLM 输出可靠性**（缓存标记、思考块泄漏）和 **会话生命周期完整性**（恢复时消息丢失、凭据丢失），这反映出随着 agent 越来越依赖上下文与多轮交互，开发者对"无意外"的 LLM 交互链路有强烈需求。

---

#### 5. Bug 与稳定性

今日报告的 Bug 按严重程度排序如下：

| 严重程度 | Issue | 描述 | 状态 |
|---------|-------|------|------|
| 🔴 高 | [#4532](https://github.com/OpenHands/software-agent-sdk/issues/4532) | 恢复暂停的会话后，下一次请求缺少 assistant `tool_use` 消息，但保留了 `tool_result`，导致提供商（如 Bedrock）拒绝请求 | 待修复，暂无 PR |
| 🟠 中 | [#4533](https://github.com/OpenHands/software-agent-sdk/issues/4533) | 使用默认 `default` agent profile 启动会话时，LLM `api_key` 丢失，导致 LiteLLM `AuthenticationError`（自托管场景） | 待修复，尚无对应 PR |
| 🟠 中 | [#4511](https://github.com/OpenHands/software-agent-sdk/issues/4511) | `Message.to_chat_dict` 在 `cache_enabled=False` 时仍输出 `cache_control` 标记 | 已有修复 PR: [#4512](https://github.com/OpenHands/software-agent-sdk/pull/4512) |
| 🟠 中 | [#4530](https://github.com/OpenHands/software-agent-sdk/issues/4530) | LLM 生成的会话标题泄漏原始 `<think>` 推理块（如 Qwen3 在 Nebius 上未拆分 `reasoning_content`） | 已有修复 PR: [#4534](https://github.com/OpenHands/software-agent-sdk/pull/4534) |
| 🟠 中 | [#4525](https://github.com/OpenHands/software-agent-sdk/issues/4525) | `events_to_messages` 缺少边界测试，补测试时发现并行调用批次中 `responses_reasoning_item` 被丢弃 | 已有测试/修复 PR: [#4526](https://github.com/OpenHands/software-agent-sdk/pull/4526) |
| 🟢 低 | [#4520](https://github.com/OpenHands/software-agent-sdk/issues/4520) | `parse_extension_source` 在处理 `github:owner/repo` 简写时重复添加 `.git` 后缀 | 待修复，暂无对应 PR |

**稳定性趋势**：今日 bug 多数围绕 **LLM 消息转换/序列化** 和 **会话状态恢复**。好在大部分已有及时修复 PR，反映项目对问题响应迅速。

---

#### 6. 功能请求与路线图信号

- **`#4531` [Feature] Add provider-connection store: share one credential across multiple LLM profiles** — 请求将 provider 凭据与 profile 解耦，实现一凭据多用。配套 PR `#4492`（Add read-at-use LLM provider connections）已在开发，且 `#4455` 已合入基础架构，**预计进入下一版本**。链接: https://github.com/OpenHands/software-agent-sdk/issues/4531

- **`#4528` [Enhancement] Tell agents where to find previous local conversations** — 要求提示词中说明本地历史会话位置，PR `#4527` 已实现，**大概率随下版本发布**。链接: https://github.com/OpenHands/software-agent-sdk/issues/4528

- **`#4529` [PR] feat(telemetry): identify automation conversations** — 对应 issue `#4427`，为 telemetry 添加 `is_automation` 标记，区分用户/自动化发起的会话，已开 PR，可能进入后续版本。链接: https://github.com/OpenHands/software-agent-sdk/pull/4529

- **`#4476` [PR] fix: respect OH_PERSISTENCE_DIR for all ~/.openhands paths** — 针对企业临时沙箱环境的状态持久化问题，处于开放状态，未合并。这是企业部署的关键能力，值得关注。链接: https://github.com/OpenHands/software-agent-sdk/pull/4476

**路线图信号**：`provider-connection store`、自动化会话标识、持久化目录可配是当前社区呼声较高的方向，极有可能在后续版本中优先落地。

---

#### 7. 用户反馈摘要

从今日 Issues 评论中可提炼出以下用户声音：

- **自托管用户的痛点**（来自 `#4533`）：一位基于 OpenHands 的 agent 在自托管 agent-server + agent-canvas 时，因 seeded `default` agent profile 导致 API key 丢失，引发认证失败。用户明确描述了复现路径，显示出 **自托管场景下默认配置的可靠性** 对社区用户至关重要。

- **推理模型的使用摩擦**（来自 `#4530`）：社区用户面对 Qwen3 等未按标准输出 `reasoning_content` 的模型时，遇到标题泄漏 `<think>` 块的问题。这反映出 **多 provider 兼容层的不完善** 是真实阻碍。

- **开发者对测试完备性的主动关注**（来自 `#4525`）：Contributor 在补全 `events_to_messages` 边界测试的同时，主动暴露了 `responses_reasoning_item` 批次丢失的深层 bug。这说明社区维护者 **对测试质量的自我要求较高**，也侧面体现代码库复杂度。

- **企业级持久化需求**（来自 `#4476` PR 描述）：企业临时沙箱在恢复时丢失 `~/.openhands`，需要将用户状态重定向到持久卷。这是 **企业落地的关键需求**，但被讨论热度相对较低，值得维护者留意。

---

#### 8. 待处理积压

以下 Issue/PR 长期未获得关注或响应，建议维护者审阅：

- **`#4130` [Feature] search_tool** — 创建于 2026-07-16，已超过一个月，标记为 `duplicate-candidate`，有 2 条评论。Issue 指出工具数量增长导致系统提示词膨胀，影响性能与缓存，诉求是提供动态工具发现/搜索机制。建议尽快确认 duplicates 状态，或给出是否采纳的方向性答复。链接: https://github.com/OpenHands/software-agent-sdk/issues/4130

- **`#4427` [Enhancement] feat(telemetry): identify local automation conversations** — 创建于 2026-08-08，10 天无评论，但已有对应 PR `#4529` 合并，**应尽快关闭** 或更新状态。链接: https://github.com/OpenHands/software-agent-sdk/issues/4427

- **`#3673` [PR] feat(sdk): add ask_oracle tool** — 自 2026-06-11 起一直处于开放状态，已有集成测试标记，是较长期的功能 PR。建议明确其下一步计划（合入、打回或需要更多评审）。链接: https://github.com/OpenHands/software-agent-sdk/pull/3673

- **`#4484` [PR] Weekly test sweep: remove low-value tests + simplify** — 已开放数周，目标是清理低价值测试，维护者若不及时处理，类似清理工作可能堆积。链接: https://github.com/OpenHands/software-agent-sdk/pull/4484

---

*数据来源：GitHub OpenHands/software-agent-sdk 仓库，统计时间窗口 2026-08-18 至 2026-08-19。*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-19

## 1. 今日速览

过去 24 小时 Pi 项目保持高活跃度：共 74 条 Issue 更新（新增/活跃 12 条，关闭 62 条）和 27 条 PR 更新（待合并 13 条，合并/关闭 14 条），关闭率显著高于新增率，显示维护团队处理效率良好。核心工作集中在 GitHub Copilot 登录限流修复、Anthropic 用量计费回退修正、以及 TUI 渲染性能优化上。多方用户报告的 Copilot 429 问题已有对应修复 PR（#8254）进入待合并队列；两个开放式功能请求（Bedrock Mantle provider、缓存友好压缩）均有活跃 PR 推进。整体项目健康度良好，未出现新版本发布，但社区讨论热度与代码维护节奏均处于较高水平。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日合并/关闭的 PR 中，以下几项对项目功能完善和稳定性提升有直接贡献：

- **Copilot 策略登录限流修复（#8254，OPEN）**：fetch 账户模型目录后再更新策略，仅更新已知、支持工具且未配置的模型，并为限流请求增加有界重试。该 PR 直接针对 #7850（组织 Copilot 登录 429 问题）与 #8251（GHEC 登录并发策略请求导致 429），有望解决近期社区反馈最集中的 Copilot 登录难题。
- **Anthropic 服务端回退用量修正（#8308 已关闭 → #8319 重新实现，OPEN）**：#8308 修复了 Anthropic 服务端回退（如返回 `claude-opus-4-8`）时仍按请求模型计费的问题，但随后被 #8313 回退，同日 #8319 以“正确方式”重新实现——线程化传递 usage 成本而非错误使用模型目录。显示该修复经过了一次实现质量评审，最终方案值得期待。
- **Bedrock redacted reasoning 往返修复（#8314，CLOSED）**：修复 Bedrock Converse API 将加密推理内容作为 `redactedContent` 不透明成员返回时的处理逻辑，确保推理内容在往返过程中不丢失或损坏。
- **工具结果图片折叠修复（#8303，CLOSED）**：修复了折叠工具输出时，即使设置了 `showImages` 也错误挂载 Kitty/iTerm 图片子组件导致布局错乱的问题，修复 #8304。
- **openai-completions 推理 token 预算字段泛化（#8275，CLOSED）**：继 #7638 之后，将 `thinking_token_budget` 的支持扩展到 Qwen/SGLang 的 `thinking_budget` 与 llama.cpp 的 `thinking_budget_tokens`，并补充了兼容性文档。
- **TUI 长 Markdown 渲染让出事件循环（#8327，CLOSED）**：为长 Markdown 渲染增加基于单调时钟的 deadline 与回调机制，修复大文档渲染时终端无响应的问题。

此外，`disabledCommands` 设置（#8326）已合并，允许用户和团队禁用具体内置斜杠命令（如 `/share`、`/export`），对数据安全有积极意义；`agent_recovery_exhausted` 扩展钩子 PR（#8316）虽已关闭，但从 Issue #8317 来看需求本身已被提出，可能后续重新纳入。

## 4. 社区热点

- **[#7547 [Windows] [sink-thread] How do you use Pi on windows? What issues are you seeing?](https://github.com/earendil-works/pi/issues/7547)**（评论 28，👍 1）  
  Windows 用户体验征集帖，创建两周仍保持最高讨论热度。项目方主动收集 Windows 用户的使用方式和痛点，意在确定支持精力分配方向（核心修复 vs 文档 vs 开箱即用），是社区驱动的路线图调研型 Issue。

- **[#2870 [bug] Follow XDG Base Directory（CLOSED）](https://github.com/earendil-works/pi/issues/2870)**（评论 19，👍 50）  
  Linux 用户要求遵循 XDG 规范，将配置文件从 `$HOME` 移至 `$XDG_CONFIG_HOME`。50 👍 反映该诉求在社区有广泛共鸣；关联的早期 Issue #534（16 评论，46 👍）也在今日更新后关闭，说明这一长期痛点已获解决。

- **[#5363 Add amazon-bedrock-mantle provider（OPEN，inprogress）](https://github.com/earendil-works/pi/issues/5363)**（评论 16，👍 15）  
  请求新增 Bedrock Mantle OpenAI 兼容 provider，因为 Mantle 模型（如 GPT-5.x 系列）不走 Converse API。已有 PR #6216 与 #8302 两个实现，其中 #8302 今日更新为 WIP（等待 API key 权限做端到端测试），社区关注度与实现进度双高。

- **[#534 config folder is out of place on Linux（CLOSED）](https://github.com/earendil-works/pi/issues/534)**（评论 16，👍 46）  
  与 #2870 同源的 XDG 目录历史 Issue，今日关闭确认了该问题的最终修复。

- **[#7850 GitHub Copilot login fails with 429（CLOSED，no-action）](https://github.com/earendil-works/pi/issues/7850)**（评论 13，👍 7）  
  因组织有 20+ 可用模型导致 Copilot 登录限流，虽然标为 no-action，但同场景的 #8251 与 #8121 仍在出现。PR #8254 即为修复此问题而开。

**诉求分析**：社区当前最集中的诉求有三类——① Windows 与 Linux 下的本地体验打磨（XDG 规范、find 卡死、终端尺寸变化崩溃）；② Copilot/企业级登录的稳定性和限流处理；③ 新模型 API 的接入速度（Bedrock Mantle 是典型代表）。

## 5. Bug 与稳定性

按严重程度排列今日报告的 Bug（含昨日报告但今日仍活跃/更新者）：

| 严重度 | Issue | 描述 | 状态/Fix PR |
|---|---|---|---|
| **严重** | [#8166](https://github.com/earendil-works/pi/issues/8166) | 自定义消息在工具批处理中途注入，破坏 tool_calls→tool 邻接关系，导致 DeepSeek 每次后续轮次都返回 400 错误，会话不可用 | Open，暂无 PR |
| **严重** | [#8036](https://github.com/earendil-works/pi/issues/8036) | `edit` 工具渲染 ~14.5MB 大 diff 时导致 TUI 崩溃，resume 会话时也会复现 | Open，暂无 PR |
| **严重** | [#8237](https://github.com/earendil-works/pi/issues/8237) | pi-coding-agent 嵌入 Node SEA 可执行文件时，jiti alias 解析失败导致扩展永不加载 | Closed (no-action)，但影响嵌入场景用户 |
| **中等** | [#8252](https://github.com/earendil-works/pi/issues/8252) | tmux 窗口宽度变为 1 列时，spinner 触发的宽度检查让 pi 以 exit code 1 崩溃（数日反复出现） | Closed，但未说明修复版本 |
| **中等** | [#8282](https://github.com/earendil-works/pi/issues/8282) | Windows 下 `find` 扫描大量文件目录（如 C:\Windows）时进程卡死，占用高 CPU，只能手动结束 | Closed (no-action)，建议改用 fd |
| **中等** | [#8134](https://github.com/earendil-works/pi/issues/8134) | 通过正向代理访问纯 HTTP provider 时，首次工具调用后的后续模型请求挂起（0.84.0 回归） | Open，暂无 PR |
| **中等** | [#8286](https://github.com/earendil-works/pi/issues/8286) | openai-completions 走真实网络时静默失败（空输出或幻觉响应），仅 127.0.0.1 回环地址正常 | Closed (no-action) |
| **较低** | [#8281](https://github.com/earendil-works/pi/issues/8281) | 长会话（~10k+ 行）中，视口上方内容变化导致全屏闪烁重绘 | Closed (no-action) |
| **较低** | [#8309](https://github.com/earendil-works/pi/issues/8309) | 长对话时每次执行新命令界面先跳到顶部再跳回，macOS 和 Windows 均有 | Closed (no-action) |
| **较低** | [#8323](https://github.com/earendil-works/pi/issues/8323) | OpenAI 客户端创建时未设置 timeout，使用 SDK 默认 600s，本地模型思考超过 10 分钟会被切断 | Closed (untriaged) |
| **较低** | [#8245](https://github.com/earendil-works/pi/issues/8245) | `after_provider_response` 扩展钩子在 Google Generative AI provider 上从不触发 | Closed (no-action) |

今日共关闭 62 条 Issue，其中相当比例为 no-action 或 untriaged 关闭，说明团队对 issue 分类与过滤的效率较高，但部分 Bug（如 #8282、#8286）虽被关闭，用户的实际问题并未得到代码层面的修复，存在“关闭但不解决”的风险。

## 6. 功能请求与路线图信号

- **Amazon Bedrock Mantle provider（#5363）**：已有 PR #6216（OpenAI Bedrock provider 路线）与 #8302（WIP，等待权限测试）双线推进，是当前路线图上最明确的下一版本功能之一。来自 [#6216 PR](https://github.com/earendil-works/pi/pull/6216) 的描述表明 Mantle 是 Amazon 新推出的 API 表面，若不支持则相关 GPT 模型完全不可用。
- **缓存友好压缩（Cache-friendly compaction，PR #8307）**：将压缩请求追加到主会话以复用已有缓存，避免独立请求的高成本。仅启用自动压缩场景，属于性能优化类新功能，随 PR 合并可能进入 0.85。
- **`agent_recovery_exhausted` 扩展钩子（#8317 + PR #8316）**：允许扩展在原生重试与溢出压缩均耗尽后进行模型切换并继续会话。PR #8316 虽已关闭，但 Issue #8317 本身是今日新开且关闭的，双关闭表明该功能可能在内部重新设计；若纳入，将极大增强扩展对恢复流程的控制力。
- **`disabledCommands` 设置（#8326，已合并）**：用户/组织可禁用内置斜杠命令，回应了对 `/share`、`/export` 等隐私敏感命令的管控需求，属安全/治理类功能。
- **OpenAI 兼容 provider 加入 `/login` 流程（#8320/#8324）**：两个相同主题的 PR 均于今日关闭，核心需求为通过登录向导直接配置 OpenAI-compatible 自定义 endpoint（含 base URL、模型名、API key、默认 128k 上下文），降低自建网关/本地模型的使用门槛。
- **RPC 与 CLI 功能对齐（#885）**：1 月提出的 RPC 全 parity 请求今日有新评论（3 条），该需求长期存在但推进缓慢，可能因 CLI 本身功能演进过快导致 parity 目标不断移动。
- **AgentHarness 持久化前置消息替换钩子（#8292）**：请求在消息持久化前可替换最终消息（用于注入结构化内容块），今日新开即被关闭，但使用场景明确（扩展开发），后续有重启可能。

## 7. 用户反馈摘要

从今日活跃 Issue 与评论中可提炼出以下真实用户声音：

- **Windows 支持呼声高，但体验碎片化**（#7547）：用户对 pi 在 Windows 上的运行方式感到困惑，方式过多导致不知何处集中修复。部分问题（如 #8282 的 find 卡死）让用户只能自行 workaround（改用 fd）。
- **XDG 长期痛点确认解决**：在 #2870/#534 关闭之际，用户对项目最终遵循 Linux 标准表示认可，两个 Issue 合计 96 个 👍 表明这一修复的社区价值极高。
- **Copilot 429 问题令人沮丧**（#8121）：用户明确说“虽然释放说明声称修复了，但 0.84.2 仍然报错”，并自行用了 workaround 才恢复。说明修复覆盖面不全（企业版 GHEC 场景未覆盖，见 #8251）。
- **压缩/恢复流程有隐蔽回归**：多个 Issue（#5463、#6339、#7724、#8283）从不同角度触及恢复流程的问题——编译后继续失败、压缩阈值在 agentic run 中不触发、恢复后重放截断消息。PR #8283 今日仍在修复“重试和压缩后恢复 continuation”的边界场景，说明该区域较脆弱。
- **长会话 TUI 体验仍是痛点**（#8281、#8309、#8212）：跳顶/闪烁/主题残留等视觉问题在长对话中反复出现，虽都被标记 no-action 或 closed，但用户表达“被困扰很久”，UI 层仍需系统性的渲染性能与增量更新优化。
- **集成开发者希望更多扩展钩子**（#8317、#8292、#8245）：扩展机制（预持久化消息钩子、恢复耗尽钩子、after_provider_response 在所有 provider 上可靠触发）是第三方集成者最关心的基础设施能力。

## 8. 待处理积压

以下为值得维护者关注的长期未响应或推进缓慢的重要条目：

| 条目 | 创建时间 | 类型 | 积压原因/状态 |
|---|---|---|---|
| [#6216 Amazon Bedrock Mantle OpenAI Responses provider](https://github.com/earendil-works/pi/pull/6216) | 2026-07-01 | PR | 近 7 周仍在 open，但 #5363 需求明确、 #8302 也在推进，建议明确维护归属或闭合并指向 #8302 |
| [#885 RPC parity with CLI](https://github.com/earendil-works/pi/issues/885) | 2026-01-21 | Issue | 半年以上未实质推进，近期有评论提及，可能需要路线图决策（接受部分 parity 或安排专项） |
| [#

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-19

## 1. 今日速览

过去24小时项目保持**极高活跃度**：累计产生 92 条 Issue 更新（净新增/活跃 66 条）与 290 条 PR 更新（待合并 177 条、已合并/关闭 113 条），PR 吞吐量达到近期峰值。虽然今日无新版本发布，但大量针对 GPT-5.6 模型系列、Bedrock 成本核算、OTel 可观测性、UI 的 PR 密集推进。社区讨论热度集中在 Responses API 兼容性、预算/配额误判、流式 SSE 协议正确性三个方面；值得警惕的是已有多个高赞 Issue 处于长期未关闭状态（最早可追溯至 2025 年 7 月），积压问题开始侵蚀用户信任。


## 2. 版本发布

今日无新版本发布。


## 3. 项目进展

今日合并/关闭了 113 条 PR，其中多个直接解决下游用户可感知的问题，整体呈现 "修复与基建并重" 的态势：

- **成本核算补全**：`fix(cost_calculator): recognize the ultrafast service tier` (#37355，已关闭) 修复了 `service_tier: "ultrafast"` 被静默按标准费率计费的问题，并避免 `*_ultrafast` 定价键导致请求失败；`feat(guardrails): count bedrock guardrail cost against spend and budgets` (#37362，已关闭) 将 Bedrock Guardrail 调用纳入费用与预算体系，是成本可观测性的重要补全。
- **UI 现代化持续产出**：三条 tremor→shadcn 重构 PR（#37323 已关闭、#37315/#37308 开放中）覆盖缓存设置、Playground 模型选择器、Admin/SSO/SCIM/Alerting 表单及模型信息视图，为设计系统统一扫清障碍。
- **新模型与路由能力**：`feat(openai): add gpt-5.6 model family to registry` (#37371) 补齐 GPT-5.6 Sol/Terra/Luna 的成本与 `tool_choice` 支持；`feat(proxy): add project-level ITPM and OTPM quotas` (#35110) 则回应了输出型任务饿死输入型任务的配额治理需求。

**值得关注**：177 条 PR 等待合并形成了可观的 backlog，如果 Maintainer 吞吐不能跟上，社区贡献者的耐心可能成为下一个瓶颈。


## 4. 社区热点

| Issue/PR | 标题 | 评论量 | 反应 |
|---|---|---|---|
| [#25429](https://github.com/BerriAI/litellm/issues/25429) | gpt-5.4 经 chatgpt/ Responses API 返回空内容、completion() 桥接报错 | 20 | 👍 4 |
| [#23741](https://github.com/BerriAI/litellm/issues/23741) | AnthropicException 400: `vector_store_ids: Extra inputs are not permitted` | 13 | 👍 12 |
| [#14667](https://github.com/BerriAI/litellm/issues/14667) | `user_header_mappings` 与 OpenWebUI 不兼容（closed） | 12 | 👍 1 |
| [#14516](https://github.com/BerriAI/litellm/issues/14516) | `output_parse_pii` 设置不生效（closed） | 11 | 👍 2 |
| [#12448](https://github.com/BerriAI/litellm/issues/12448) | 支持 salt_key 轮换 | 10 | 👍 3 |

**热点分析**：三大未被关闭的热门 issue 集中在**兼容层质量**上——#25429 直指 `responses()` 与 `completion()` 两条 API 路径在 OpenAI 新模型上行为不一致；#23741 暴露了 LiteLLM 将 `vector_store_ids` 透传给 Anthropic 导致 400，说明参数白名单/黑名单机制存在漏洞；#12448 则代表了生产环境对安全运维能力（salt_key 轮换）的强诉求。这些都是用户在实际业务中直接遇到的阻断性问题，高 👍 数印证了痛点普遍性。


## 5. Bug 与稳定性

按严重程度排列：

**🔴 严重（影响生产可用性 / 资金）**

- **[#37273](https://github.com/BerriAI/litellm/issues/37273) [新] `/v1/messages` 流式响应重复发送 `content_block_stop`，导致工具被执行两次** — Anthropic 流式协议的关键正确性问题，会造成真实业务副作用（写操作重复执行），尚无 fix PR。
- **[#35590](https://github.com/BerriAI/litellm/issues/35590) adaptive_router 一个持久化的 alpha/beta=0 单元永久 500 错误** — `gammavariate: alpha and beta must be > 0.0`，重启也无法恢复。路由核心组件一旦故障即为全阻。无关联 fix PR。
- **[#36898](https://github.com/BerriAI/litellm/issues/36898) `GET /health` 明文泄露 `extra_headers` 与 `aws_session_token`** — 安全敏感，作者明确指出 `/model/info` 已修复但 `/health` 漏掉，属于同类漏洞的未修复变体。无 fix PR。

**🟠 主要（功能受损 / 重要请求异常）**

- **[#27735](https://github.com/BerriAI/litellm/issues/27735) 虚拟密钥 `BudgetExceededError` 使用了过期 spend 数据** — 用户往返 /key/info 显示额度未超限但请求被拒，疑似预算检查与计数路径存在竞态。关联 #27639（未关闭）。
- **[#37261](https://github.com/BerriAI/litellm/issues/37261) [新] 无 Redis 时 `provider_budget_config` 计算 `budget_reset_at` 漂移到 57 年后** — 导致月度预算永不重置。
- **[#37268](https://github.com/BerriAI/litellm/issues/37268) [新] `azure/gpt-5.6-sol` 在 `model_prices_and_context_window.json` 中条目错误** — 影响成本估算与准入控制。

**🟡 次要（边界场景 / 配置误导）**

- **[#37102](https://github.com/BerriAI/litellm/issues/37102) Bedrock CountTokens 不支持时**静默返回低估的 token 数，影响用量审计。
- **[#27492](https://github.com/BerriAI/litellm/issues/27492) `use_chat_completions_api: true` 丢弃 `reasoning_content`** — 推理模型经转换后内容丢失。


## 6. 功能请求与路线图信号

- **Amazon Bedrock AgentCore 搜索将成为一等公民**：Issue [#31819](https://github.com/BerriAI/litellm/issues/31819) 请求将 Bedrock AgentCore Web Search 作为原生 `search()` 提供方，PR [#36331](https://github.com/BerriAI/litellm/pull/36331)（开放中）已落地实现，大概率进入下一版本。
- **项目级 ITPM/OTPM 配额**：PR #35110 引入独立的输入/输出 token 限额，回应了输出密集型任务饿死输入任务的问题，契合 Mantle 风格配额需求。该 PR 已开放 20 天，合入后可缓解此前只能合并 TPM 的限制。
- **salt_key 轮换**：#12448 已提出 1 年仍未实现。生产环境调试日志可能泄露 `master_key`/`salt_key`，期望参照 master_key 轮换机制，目前没有对应 PR，路线图优先级不明。
- **Adaptive Router 自定义分类器 UI**：PR #37374 新增 config 声明的自定义分类器 registry，解决 dashboard 无法编辑自定义 auto-router 的问题。

**判断**：AgentCore 搜索与项目级配额是 "已上车" 的需求；salt 轮换与预算竞态修复则是明显的呼声高但响应慢的领域，建议 Maintainer 明确表态。


## 7. 用户反馈摘要

- **"文档说支持，实际不工作"类反馈集中**：#14667（OpenWebUI user_header_mappings，closed）、#14516（output_parse_pii，closed）均为用户严格按文档操作却失效，最终以 stale 关闭。#22173（Helm chart 指向不存在的镜像）已有 5 个 👍，用户按官方文档部署即失败，对信任伤害较大。**诉求是提升文档与配置校验的一致性**。
- **对"静默丢弃/静默出错"强烈不满**：#33184 指出 `store`/`prompt_cache_key` 被接受但不转发；#27967 指出 mid-stream fallback 把 `prefix=True` 的 assistant 预填充块发给不支持的模型导致 fallback 失败。用户期待的是**显式报错而非静默降级**。
- **成本数据缺失影响财务对账**：#31194（Databricks 价格过时）、#37371（GPT-5.6 成本为 $0）等说明用户对价格表的实时性很敏感，特别是新模型发布后。
- **正面反馈**：#37370/#37372 等 UI PR 持续解决下拉框 label、CI 超时等细节体验问题；#37368（为 Assistants/A2A 流加 SSE keepalive）体现了对网络代理环境下长连接稳定性的主动修复，这类"防患于未然"的 PR 社区评价通常较好。


## 8. 待处理积压

以下 Issue 长期存在但一直未关闭，建议维护者优先关注：

- **[#12448](https://github.com/BerriAI/litellm/issues/12448) salt_key 轮换支持** — 开放超 13 个月，10 条评论，安全相关，无 PR。
- **[#22878](https://github.com/BerriAI/litellm/issues/22878) Claude Code 2.1.69 + GitHub Copilot 代理时 `OpenAIError: Bad Request`** — 开放 5 个月，影响 Claude Code 用户接入 Copilot 模型的场景。
- **[#21312](https://github.com/BerriAI/litellm/issues/21312) 失败的请求不计入 RPM 限额** — 开放 6 个月，会导致限流机制被绕过，对配额治理是实际漏洞。
- **[#19499](https://github.com/BerriAI/litellm/issues/19499) Prompt Injection 检测阻塞事件循环导致 Pod 重启** — 开放 7 个月，属于安全功能带来的稳定性问题，且与 K8s 部署强相关。
- **[#22173](https://github.com/BerriAI/litellm/issues/22173) Helm chart 指向不存在的镜像** — 开放近 6 个月，直接阻断新用户部署，5 个 👍，建议尽快修复文档/Chart。
- **[#27518](https://github.com/BerriAI/litellm/issues/27518) 代理级 `async_pre_call_hook` 在 `/v1/messages` 上被绕过** — 已关闭，但作为安全/合规钩子被绕过的事件，建议在 Changelog 中明确说明修复版本，避免用户误用旧版。

---

**健康度总评**：项目当前处于高频迭代期，社区贡献活跃（外部 PR 占比可观），但存在两点隐忧：一是长期未关闭的高赞 Issue 积压（最早可追溯至 2025 年 7 月）削弱了用户对维护响应速度的信心；二是安全/资金相关的 Bug（#36898、#27735、#35590）虽有报告但尚无 fix PR，需防备信任透支。建议 Maintainer 优先分配资源到安全类与预算准确性相关的修复上，并对 1 年未动的 #12448 给出明确路线图表态。

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-19

## 今日速览

过去24小时项目整体活跃度较高：共更新 Issue 3 条（2 条开放中、1 条已关闭），PR 更新 61 条（45 条待合并、16 条已合并/关闭），无新版本发布。开发重心明显集中在 **reliability-2026 专项**，涉及 Scheduler V1→V2 迁移修复、CHASM（Callback/HSM）Nexus 操作稳定性、OTEL/gRPC 全局注册资源释放、Nexus 请求链路追踪等，反映了项目当前正系统性地治理历史遗留可靠性问题与观测盲区。社区侧讨论热度一般，最受关注的是 Worker Deployment Version 清理失败问题（#11539），属于用户实际运维中遇到的阻塞性问题。

## 项目进展

今日合并/关闭的 PR 共 16 条，其中可确认的合入内容包括：

- **[reliability-2026] 修复 approximateSize 在 activity 启动与心跳路径上的少计问题（#11486）**：修复了 `AddActivityTaskStartedEvent` 与心跳处理中对 `ActivityInfo` 变更未计入 mutable state 大小计数器的问题，避免大规模状态下内存估算偏差。https://github.com/temporalio/temporal/pull/11486
- **[reliability-2026] 统一验证 callback 链接的有效性（#11610）**：确保 callback 上的链接在各请求路径上被一致校验，避免不一致的校验逻辑导致潜在安全问题。https://github.com/temporalio/temporal/pull/11610
- **仅重建实际截止时间发生变动的 activity 定时器（#11613，cherry-pick #11565）**：避免重复创建定时器任务，降低 hot shard 风险。https://github.com/temporalio/temporal/pull/11613
- **[reliability-2026] [Elasticsearch] datetime 格式始终包含纳秒分量（#11619，cherry-pick #11564）**：提升时间戳精度与排序一致性。https://github.com/temporalio/temporal/pull/11619

此外还有一条 **revert PR（#11616）**，撤销了此前"跳过整个 mutable state 事务"的优化——该提交会在特定复制场景下导致执行卡死，需要回退。https://github.com/temporalio/temporal/pull/11616

整体来看，项目在可靠性改进（状态统计准确性、定时器重复触发、时间格式一致性）、可观测性增强（Nexus/Worker span 注解）与关键回滚三个方向同步推进，体现了"修补与加固并行"的版本策略。


## 社区热点

- **#11539 DeleteWorkerDeploymentVersion 永久失败（2 条评论，评论区持续活跃）**：这是过去 24 小时内讨论度最高、且仍在持续发酵的 Issue。用户报告当某个版本的 summary 数据仍然存在但其 workflow 已经不复存在时，删除操作会永久性失败，进而阻塞新版本的注册——在 `matching.maxVersionsInDeployment` 配额约束下，这会导致 Deployment 无法滚动更新。评论者主要围绕版本清理机制与生命周期管理展开讨论。https://github.com/temporalio/temporal/issues/11539

该问题触及了 Worker Deployment 版本管理在生命周期边界场景下的设计缺口，涉及"summary 生命周期 vs workflow 生命周期"的错配，值得项目维护者优先关注。


## Bug 与稳定性

按严重程度排序：

1. **DeleteWorkerDeploymentVersion 永久失败（#11539）**：会导致 Worker Deployment 版本无法清理、新版本无法注册，影响生产环境的版本滚动能力。目前尚待修复 PR。https://github.com/temporalio/temporal/issues/11539
2. **`computeFutureActionTimes` 在 `RemainingActions` 为负数时 panic（#11620）**：由损坏/非法的调度状态触发，导致 panic。已提交修复 PR，将 `count` 约束为不小于 0。https://github.com/temporalio/temporal/pull/11620
3. **复制执行卡死问题（#11616 revert）**：`#10539` 引入的"chasm 事务被跳过时跳过整个 mutable state 事务"在特定复制场景下导致执行卡住。已通过 revert PR 修复。https://github.com/temporalio/temporal/pull/11616
4. **CHASM Generator 缓冲区容量误算（#11621）**：完成操作的历史记录被计入 `MaxBufferSize`，导致缓冲区过早耗尽。已提交修复 PR，将 retained completion history 从容量检查中排除。https://github.com/temporalio/temporal/pull/11621
5. **Nexus 操作中 `httpCaller` 绑定顺序问题（#11605）**：在 clusterID 未设置时可能出现非空 httpCaller 搭配空 receiver 的异常状态。已提交修复 PR。https://github.com/temporalio/temporal/pull/11605


## 功能请求与路线图信号

- **内置 Kubernetes Service Account ClaimMapper（#11607）**：自托管 Kubernetes 场景下，用户希望直接通过投影的 Service Account Token 映射 Temporal 命名空间角色，而不必维护自定义 ClaimMapper 和自定义服务端二进制。这是一个高频运维需求，如果被采纳将大幅降低 K8s 自托管用户的接入成本。目前暂无对应 PR，但对产品路线图有明确信号意义。https://github.com/temporalio/temporal/issues/11607

结合已有 PR 判断，**Scheduler V1→V2 迁移（#11462）** 是明确进入下一版本/近期版本的功能项，该 PR 合并了两个需版本号提升的迁移修复，同时优化了迁移后的 start ID 处理，可能伴随一次版本升级部署。https://github.com/temporalio/temporal/pull/11462

此外，**CHASM（Callback/HSM）Nexus 能力**正在密集收尾（#11605、#11621、#11404），多个 PR 集中修复 Nexus 操作的边界情况与时间跳过机制，说明该特性正在接近成熟。


## 用户反馈摘要

- **版本清理的"卡死"体验（#11539）**：用户的核心痛点是——当一个版本 summary 比其 workflow 存活更久时，删除操作会永久性失败，且没有清晰的恢复路径。这导致版本配额被耗尽，新版本无法注册。从评论讨论中可以看出，用户期望 Temporal 在版本生命周期管理上有更健壮的兜底机制（例如自动清理孤儿 summary）。https://github.com/temporalio/temporal/issues/11539
- **K8s 自托管者的"定制化负担"（#11607）**：该用户明确表达了"不想为每个 K8s 部署重建自定义服务端二进制"的诉求。这反映了自托管用户群体中一个未被满足的共性需求：即开箱即用的云原生身份映射能力。

整体来看，用户对 Temporal 的功能深度持认可态度，目前提到的痛点主要集中在运维便利性与极端边界场景的健壮性上。


## 待处理积压

- **#10739 Annotate worker task spans（2026-06-16 创建，持续 2 个月）**：该 PR 为 workflow/activity/Nexus worker task 添加 span 注解，是提升可观测性的重要工作，依赖 #11561。长时间未合并，建议关注依赖链的阻塞状态。https://github.com/temporalio/temporal/pull/10739
- **#11404 improvements on time-skipping task regeneration（2026-08-03 创建）**：包含性能优化与两个功能测试，已开放超过两周。涉及时间跳过机制的行为变更，需要仔细评审。https://github.com/temporalio/temporal/pull/11404
- **#11462 Scheduler V1→V2 migration-eligibility fix（2026-08-10 创建，仍在开放中）**：这是 Scheduler 迁移的关键修复，合并了两个独立修复并需要版本号提升。建议持续跟踪其评审进展，避免影响后续版本发布节奏。https://github.com/temporalio/temporal/pull/11462


**总体评估**：项目处于活跃开发期，可靠性专项推进节奏良好。当前最需要关注的是 #11539 的修复方案落地，以及 #11620/#11621 等已提交修复的 review 合并进度。功能请求侧，Kubernetes 原生集成能力（#11607）是一个明确的产品机会信号。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*