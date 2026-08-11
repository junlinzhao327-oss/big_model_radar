# OpenClaw 生态日报 2026-08-12

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-11 23:07 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-12

---

## 1. 今日速览

过去 24 小时 OpenClaw 仓库保持高强度运转：**500 条 Issue 更新**（新开/活跃 395，关闭 105）、**500 条 PR 更新**（已合并/关闭 207，待合并 293），均接近 GitHub 单仓库单日活动上限，社区贡献与维护者响应均处于极活跃水平。**今日无新版本发布**，项目处于两次正式发布之间的密集修复与合入窗口。值得警惕的是，多个 P1 级可靠性问题（静默回复失败、消息截断/丢失、工具参数静默清空）仍处于“被反复报告—修复—复发”的循环中，其中 [#121058](https://github.com/openclaw/openclaw/issues/121058) 以 60 条评论成为社区关注度最高的 Issue，反映出用户对“已关闭但实际未修复”问题的不满情绪正在累积。同时，渠道适配器（飞书、Discord、QQ、Mattermost 等）的配置 schema 缺陷修复在本日 PR 中占比最高，表明项目正通过社区驱动的方式系统性收敛多平台兼容性问题。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日共 207 个 PR 被合并或关闭，合并率约 41%，处于健康水平。从高讨论度 PR 来看，项目推进集中在以下方向：

### 3.1 渠道适配器修复（密集合入）
多款渠道的配置 schema 与运行时行为不一致问题正在被集中修复。已关闭的 PR 包括：

- **[#119357](https://github.com/openclaw/openclaw/pull/119357) fix(qqbot): honor the configured upgradeUrl in /bot-upgrade** — 修复 QQ 机器人 `upgradeUrl` 配置被文档化但运行时被忽略的问题。已关闭。
- **[#120198](https://github.com/openclaw/openclaw/pull/120198) fix(context-engine): warn when legacy host-param default withholds params** — 为未声明 `acceptedHostParams` 的 context engine 增加一次性警告，避免 `undefined` 参数静默失败。已关闭。

**仍开放但已具备高合并就绪度的 PR：**

- **[#117287](https://github.com/openclaw/openclaw/pull/117287)** — 修复飞书与 Mattermost 的 config schema 拒绝 `contextVisibility` 键（运行时实际读取该键）的问题，涉及配置校验与运行时逻辑不一致。
- **[#118157](https://github.com/openclaw/openclaw/pull/118157)** — 修复 11 个 bundled channel（buzz、clickclack、mattermost、nostr、tlon、twitch 等）拒绝文档化的 `mediaMaxMb` 覆盖键。
- **[#121991](https://github.com/openclaw/openclaw/pull/121991)** — 修复 Discord 扩展未处理 MCP 字符串化 `components` 导致组件在三条发送路径上丢失的问题。

### 3.2 核心运行时可靠性
- **[#120491](https://github.com/openclaw/openclaw/pull/120491) feat(tools): per-turn per-target send budget guard for message tools** — 为 `message` 与 `conversations_send` 工具增加每轮每目标发送预算守卫，防止模型在同一轮内重复发布雷同回复（duplicate-answer storms）。这是对 [#96827](https://github.com/openclaw/openclaw/issues/96827)（message_tool_only 模式级联自回复）等问题的系统性回应。
- **[#122176](https://github.com/openclaw/openclaw/pull/122176) refactor(state): retire commitments schema** — 在 [#121479](https://github.com/openclaw/openclaw/pull/121479) 移除 commitments 功能后，清理遗留的共享数据表与 5 个索引，完成架构清理。
- **[#122309](https://github.com/openclaw/openclaw/pull/122309) fix(update): prevent stale post-core state reuse** — 修复更新后复用陈旧 post-core 状态的问题（对应 Issue [#94559](https://github.com/openclaw/openclaw/issues/94559)）。

### 3.3 安全与边界加固
- **[#119847](https://github.com/openclaw/openclaw/pull/119847)** — 修复 `sessions_spawn` 附加文件时，工作区控制的符号链接可将目标重定向到子工作区之外的漏洞，已改用既有文件系统安全能力。
- **[#118579](https://github.com/openclaw/openclaw/pull/118579)** — 修复 Discord 语音转录捕获可能被模型提供的 bot 账户劫持，在多账户环境下导致跨账户路由的问题。
- **[#119341](https://github.com/openclaw/openclaw/pull/119341) feat(gateway): define system-agent QR contract** — 为 gateway 系统代理之间的 QR 码传输建立统一的 PNG 协议边界（base64、签名、解码大小上限），消除 WhatsApp/Zalo/设备配对等多模块间的实现漂移。

---

## 4. 社区热点

### 🔥 [#121058](https://github.com/openclaw/openclaw/issues/121058) — Silent reply failures still recurring（60 条评论）
**现象：** 用户 @sloptop-the-terrible 报告静默回复失败在 #116277 被关闭后仍然持续出现，监控 cron 在新 Issue 创建当天（2026-08-09）仍记录到新发生事件，且失败时完全没有 queued reply payload。
**背后诉求：** 这是典型的“fix 未覆盖全路径”案例。社区不满的核心不在于 bug 本身，而在于**关闭 Issue 时缺乏充分的回归验证**；用户被要求反复上报同类问题，信任成本在上升。
**当前状态：** Open，无关联 fix PR。

### 💬 [#7707](https://github.com/openclaw/openclaw/issues/7707) — Memory Trust Tagging by Source（37 条评论）
**现象：** 从 2026-02-03 创建至今持续讨论中，用户建议为记忆条目按来源打上信任等级（用户命令 / 网页抓取 / 第三方技能），防止恶意指令通过网页或第三方内容投毒记忆，进而影响后续行为。
**背后诉求：** 该项目是安全方向呼声最高的功能请求，已挂上 `needs-security-review` 标签，但 6 个月来无实质进展。社区认为这是 **AI 代理长期记忆安全的根基性设计**，而非可选项。

### 📊 [#92201](https://github.com/openclaw/openclaw/issues/92201) — Anthropic thinking 签名重放失效（22 条评论，已关闭）
P1 级 bug，涉及嵌入式 runner（Slack 插件）持久化 Anthropic thinking block 后签名失效，恢复包装器因错误文本被泛化而永远无法触发。**该 Issue 已关闭**，说明已在 main 分支修复，但社区在 [#121058](https://github.com/openclaw/openclaw/issues/121058) 中提出了类似质疑：修复是否真正覆盖了所有触发路径。

### 💰 [#42475](https://github.com/openclaw/openclaw/issues/42475) — Per-agent cost budget enforcement（20 条评论）
请求在 gateway 层增加按 agent 的每日/每月成本上限。用户 @hkochar 明确提出了实现参考（`session-cost-usage.ts`），说明其已阅读源码，是**深度用户的需求驱动**，反映出多 agent 生产部署正在成为真实使用场景。

---

## 5. Bug 与稳定性

> 严重度排序：P0 > P1 > P2。标记 “✅ 有修复 PR” 或 “❌ 无修复 PR”。

### 🔴 P0 — 已关闭
- **[#121675](https://github.com/openclaw/openclaw/issues/121675)** — `2026.8.1-beta.1` 发布时未同步发布配套 `@openclaw/*` 插件，叠加新的启动收敛守卫导致不可恢复的启动死循环。**已关闭**（今日），属于发布流程事故，后续需关注发布流水线是否已增加插件联动检查。

### 🟠 P1 — 高影响，多数尚无修复 PR

| Issue | 问题描述 | 影响面 | 修复状态 |
|---|---|---|---|
| [#121058](https://github.com

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，这是基于您提供的 GitHub 数据生成的 **Hermes Agent 项目动态日报**（2026-08-12）。

---

# Hermes Agent 项目动态日报 | 2026-08-12

## 1. 今日速览

项目活跃度极高，过去 24 小时内 Issue 和 PR 更新量分别达到 **353** 与 **500** 条，显示出强劲的开发动能与社区参与度。然而，**Issue 关闭率（6.5%）与 PR 合并率（10.8%）偏低**，导致积压工作增长迅速，这可能是项目健康度的潜在隐患。无新版本发布，工作重点集中在大型功能开发、跨切面 Bug 修复以及持续进行的 God-file 架构重构上。

- **活跃度：** 极高
- **项目健康度：** 关注积压增长，但核心机制（如 Session 状态管理、安全边界）的 PR 推进紧锣密鼓。
- **核心主题：** 架构重构（God-file sharding / 跨进程会话）、安全边界增强、多租户/多配置文件隔离。

## 3. 项目进展

今日合并/关闭的 PR 数量有限（54 条），但质量较高，主要解决了一些长期存在的顽疾。同时，多个高价值 PR 被提交，有望极大提升系统稳定性与架构清晰度。

**已合并/关闭 PR (部分):**

- **[#62332] fix: guard Gemini fallback and gate Honcho context injection** - 修复 Gemini 原生回退机制与 Honcho 记忆上下文注入的可靠性问题，防止工具调用因缺乏 Gemini“思考签名”而失败，显著提升模型回退与记忆功能的稳定性。
- **[#41087] fix: fail closed on Telegram voice cache timeouts** - 修复 Telegram 语音消息缓存超时后错误地派发空 Agent 回合的问题，现在会通过有界重试与“失败关闭”策略，直接向用户回复错误报告，避免了无效的任务跟进。
- **[#84143] fix(browser): isolate Browser Use Python environment** - 修复桌面端因继承 Hermes Python 运行时导致 Browser Use CLI `ModuleNotFoundError` 的问题，通过隔离环境避免了 ABI 混用，提升了浏览器自动化功能的可靠性。
- **[#75269 (Issue 关闭)] SessionDB retains WAL readers** - 修复了长生命周期 SessionDB 因缓存 WAL 连接导致文件描述符耗尽的 Bug。

**关键新提交 (OPEN PR):**
- **[#84145] feat(state): DB storage layer for the cross-process turn lease (#67442)** - 为跨进程会话序列化提供了数据库级存储层（`turn_leases` 表），是解决 CLI 连续性会话并发问题的关键基础设施，虽未接线但意义重大。
- **[#84148] refactor(mcp_tool): extract schema-helpers slice R4-2** - 继续推进史诗级 God-file 分片任务，从 7731 行的 `mcp_tool.py` 中提取出独立的 schema 辅助模块，保持了项目的架构整洁度。

## 4. 社区热点

今日讨论热度集中在架构演进与深水区技术挑战上，社区表现出极高的参与度。

- **[#78647] Epic: Shard all 20 god files — repo-wide god-file decomposition** *(评论: 67)*
  这是目前绝对的热点，详细规划了将仓库中 20 个巨型文件（God files）拆分为模块的计划。社区对其中涉及的接口设计和重构边界讨论热烈。这表明支持者认可当前“重构优于复制”的长期策略。
  链接: https://github.com/NousResearch/hermes-agent/issues/78647

- **[#34352] Solving the Multi-Tenant Hermes Problem** *(评论: 24)*
  高赞问题（👍 3），核心矛盾是 Memory 操作绕过了 Hook 机制，导致多租户隔离无法实现，只能通过 Fork 核心来解决。这反映了企业级用户在隔离性和安全性方面的强烈需求。
  链接: https://github.com/NousResearch/hermes-agent/issues/34352

- **[#67442] Cross-process turn serialization: CLI-continuity sessions need a DB-level lease** *(评论: 14)*
  讨论限定在 CLI 连接已存在会话时，跨进程并发写入导致的状态损坏问题。社区聚焦于如何通过 DB 级租约优雅地解决，而非暴力加锁。
  链接: https://github.com/NousResearch/hermes-agent/issues/67442

## 5. Bug 与稳定性

今日 Bug 修复覆盖了从 Windows 平台问题到服务进程崩溃的多个方面，其中有 High 优先级问题亟待处理。

**严重程度: P1 (High)**
- **[#83683] Desktop restart reaps the live gateway but never relaunches it (WeChat/QQ go silent)** *(已开)*
  回归问题，Windows 下桌面应用重启会强制关闭网关且不自动拉起，导致消息服务中断，影响严重。尚无对应修复 PR。
  链接: https://github.com/NousResearch/hermes-agent/issues/83683

- **[#54189] state.db unbounded growth: no session lifecycle/cleanup mechanism** *(已开，👍2)*
  长期存在的顽疾：`state.db` 在正常使用下可两周内涨至 659MB。目前仅有与之相关的存储层 PR (#84145)，但缺少完整的 Session 生命周期管理和清理机制。
  链接: https://github.com/NousResearch/hermes-agent/issues/54189

**严重程度: P2 (Medium)**
- **[#83714] patch tool truncates new_string content with literal '...[truncated]' text** *(已开, 8-11新增)*
  数据损坏级 Bug，`patch` 工具会向文件中写入字面量 `...[truncated]`，直接破坏代码。尚未看到 fix PR。
  链接: https://github.com/NousResearch/hermes-agent/issues/83714

- **[#71242] Anthropic auxiliary usage shim drops cache tokens — MoA aggregator cost under-reported ~7x** *(已开)*
  成本控制相关，会导致 MoA 聚合器严重低估成本（约 7 倍）。尚未看到 fix PR。
  链接: https://github.com/NousResearch/hermes-agent/issues/71242

- **[#63177] search_files silently returns 0 results on Windows when passed an absolute path** *(已开)*
  Windows 平台的老牌问题，涉及 ripgrep 与 MSYS_NO_PATHCONV 冲突，严重影响用户体验。
  链接: https://github.com/NousResearch/hermes-agent/issues/63177

**其他值得关注的 P2 优先级 Bug：** [桌面端 CPU 100%](https://github.com/NousResearch/hermes-agent/issues/73082)、[`hermes update` 误删 agent-browser](https://github.com/NousResearch/hermes-agent/issues/43564)、[Secret 泄漏至次要 Profile（安全边界）](https://github.com/NousResearch/hermes-agent/issues/82936)、[Gmail MCP 网关注册失败](https://github.com/NousResearch/hermes-agent/issues/78190)、[Dashboard 卡在重连](https://github.com/NousResearch/hermes-agent/issues/71349)。

## 6. 功能请求与路线图信号

- **多租户/多 Profile 隔离增强：** 社区对 **#34352** 的强烈诉求表明，多租户是继多 Profile 之后的必然演进方向。目前已有 **#84097 fix(auth)** 的 PR 尝试添加 `inherit_global: false` 边界，**#66887** 也关注了存储隔离，但在 Memory 层面的彻底净化仍需探索。
- **跨进程会话状态持久化：** 需求 **#67442** 已有明显进展——**PR #84145** 已提交存储层实现。另一条 **PR #84142** 试图在网关重启后维持消息连续性，两者的组合将极大改善 CLI 和网关的稳定性可靠性，预计会是下一阶段的重点。
- **桌面端功能优化：** 桌面端工作区热度提升，出现了 **关闭到托盘** (#78343)、**Tab 关闭控制** (#83051)、**本地 Token/成本分析面板** (#77221) 等新功能 PR/Issue，说明桌面端开始从“可用”走向“好用”。
- **MCP 生态扩展：** 新增 **iCloud MCP** (#84144) 与 **Gmail MCP** 修复 (#78190) 表明，项目在持续丰富 MCP 集成，但 **Gmail** 的问题显示网关进程的 OAuth 流程与 CLI 可能存在差异，需统一处理。
- **插件 API 标准化：** **#17540 / #17542 / #17543** 三个重复的 Issue 同时指向“官方 TUI 状态栏插件 API”的缺失，即使状态为 duplicate，也说明用户对稳定的插件扩展点有着渴望。

## 7. 用户反馈摘要

- **多租户用户的痛点**：开发者 [#34352](https://github.com/NousResearch/hermes-agent/issues/34352) 明确指出，由于内存操作绕过 Hook，他们只能长期维护一个 Fork 版本来支撑生产环境，这极大增加了升级成本——核心诉求是“官方支持标准 Hook 化隔离”。
- **对 Windows 平台的失望**：#63177 的提交者 @ElvisTR 在问题中详细复现了 `search_files` 在 Windows 下因为环境变量冲突导致的静默失败，并强调了自己已排除重复可能，反映出用户对平台差异问题的严谨态度。
- **对“更新即破坏”的抱怨**：#43564 反馈的用户表示，“更新成功”后被 `hermes doctor` 告知依赖缺失，这种不一致的更新体验令用户困惑。
- **技能污染现象**：用户 @sunyang-lab 在 #17345 中描述了一个诡异场景——Hermes 能看到并详细描述另一个无关项目（OpenClaw）的 Skills 内容，这引发了对本地存储隔离性的信任危机。
- **对新架构重构的支持**：#78647 评论区围绕“God-file 拆分”的讨论非常热烈，虽然参与门槛较高，但参与者普遍认可此项技术债清理的必要性，并愿意协助讨论拆分边界。

## 8. 待处理积压

以下高价值/高优先级讨论长期处于未响应或未解决状态，建议维护者重点关注：

- **[#34352] Solving the Multi-Tenant Hermes Problem** *(2026-05-29 创建, 24条评论)*
  影响范围大，涉及核心架构（内存操作 Hook）。长期 `needs-decision` 标签未去掉。请关注链接: https://github.com/NousResearch/hermes-agent/issues/34352

- **[#54189] state.db unbounded growth: no session lifecycle/cleanup mechanism** *(P1, 2026-06-28 创建, 7条评论)*
  这是资源耗尽类问题，直接影响长时间运行用户的稳定性。请关注链接: https://github.com/NousResearch/hermes-agent/issues/54189

- **[#17345] hermes 的 skills 仓库与 openclaw 的 skills 仓库存在污染行为** *(2026-04-29 创建, 6条评论)*
  不仅是隔离问题，还涉及信息安全（用户本地路径/文件被发现）。提交者用中文描述，可能需要本地化支持或视觉扫描。请关注链接: https://github.com/NousResearch/hermes-agent/issues/17345

- **[#2975] WhatsApp bridge only checks  on PATH and misses usable macOS runtimes** *(2026-03-25 创建, P3, 9条评论)*
  长期未修复的平台兼容性问题，且已经跨平台（macOS），会降低新用户的初次接入体验。请关注链接: https://github.com/NousResearch/hermes-agent/issues/2975

- **PR 积压风险：** 当前有 **446 个 PR 待合并**，其中部分来自新授权的开发者（如 @ThomasCrouzet），是否有足够的人力完成 Review 与合并将是未来一周的观察点。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报（2026-08-12）

## 1. 今日速览

过去 24 小时项目保持高度活跃：共产生 10 条 Issue 更新（7 条活跃 / 3 条关闭）、20 条 PR 更新（16 条待审 / 4 条合并或关闭），并正式发布 v1.42.0。核心看点集中在三方面：一是 v1.42.0 发布，带来 ACP provider 版本升级与可观测性增强；二是 issue #4388（bash 事件分页缺陷）与 #4463（工作流门禁移植）均已在同日获得对应 PR，反应迅速；三是安全相关讨论（#2721、#2708）持续活跃，社区对底层安全架构的技术债关注度较高。整体来看，项目维护节奏健康，修复与功能开发双线同步推进。

## 2. 版本发布

**v1.42.0** 已于 2026-08-11 发布（[发布 PR #4466](https://github.com/OpenHands/software-agent-sdk/pull/4466)），主要变化：

- **chore(acp)**：将 pinned 的 `claude-agent-acp` 升级至 0.63.0、`codex-acp` 升级至 1.1.7（[#4391](https://github.com/OpenHands/software-agent-sdk/pull/4391)）。
- **feat(observability)**：为 ACP 回合新增 LLM 与 TOOL 类型的 span 埋点，提升链路观测能力（[#4391](https://github.com/OpenHands/software-agent-sdk/pull/4391)）。

**变更影响与迁移注意**：本次未发现明确的破坏性变更。但 ACP provider 依赖版本有跳跃，使用自

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-12

## 1. 今日速览

过去 24 小时 Pi 项目整体活跃度较高：共产生 74 条 Issue 更新、44 条 PR 更新，其中 Issue 关闭率达 81%（60/74），PR 合并/关闭率达 70%（31/44），说明维护者响应迅速、清理积压效率明显。无新版本发布，但出现了多个值得关注的回归与稳定性报告（bun 运行时崩溃、OpenAI 兼容 SSE 流挂起、TUI 渲染回归），其中部分已对应修复 PR 或正在审查中。社区侧，Windows 支持方式（#7547）和 Mac 高 CPU（#7730）是讨论最热烈的两个话题；功能请求方面，子代理配置继承、主题覆盖、流式事件携带 usage 等 PR 均指向明确的用户诉求。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日合并/关闭的 PR 中以修复类和能力增强为主，主要推进了以下方向：

- **子代理配置继承**（[#7897](https://github.com/earendil-works/pi/pull/7897)）：子代理默认继承当前会话的 model/thinking 配置，修复了多会话场景下子代理跟随“任意会话最后一个设置”的混乱行为。
- **Cloudflare AI Gateway 传输**（[#7901](https://github.com/earendil-works/pi/pull/7901)）：新增通过 Cloudflare Workers AI binding 作为 AI Gateway 传输层的能力，对应 issue #7838。
- **编辑工具容错与模糊匹配增强**（[#7978](https://github.com/earendil-works/pi/pull/7978) / [#7962](https://github.com/earendil-works/pi/pull/7962)）：修复了 `edits` 参数为单对象时工具抛错的问题，并在模糊匹配中折叠空白符差异，使小模型对“内容一致但空格不同”的编辑请求能正确匹配。
- **OpenAI 兼容 SSE 流中断修复**（[#7959](https://github.com/earendil-works/pi/pull/7959)）：为 openai-completions 路径增加了“响应中途停滞”超时机制，修复了服务端发送完整内容后不关闭连接导致会话永久挂起的问题（对应 #7954）。
- **TUI 剪贴板与键盘协议修复**（[#7972](https://github.com/earendil-works/pi/pull/7972) / [#7899](https://github.com/earendil-works/pi/pull/7899)）：OSC 52 剪贴板写入失败时不再盲目提示“Copied!”；Kitty 键盘协议缺失时 Alt+Enter 的 ESC+CR 拆分不再导致误触发 `app.interrupt`。
- **示例扩展能力补齐**（[#7967](https://github.com/earendil-works/pi/pull/7967)）：`notify` 示例扩展新增 VS Code 集成终端支持（OSC 99 → 桌面通知）。
- **文档完善**（[#7965](https://github.com/earendil-works/pi/pull/7965)）：补充 iTerm2 / Ghostty 下 fullscreen 鼠标行为差异的文档说明。

此外，有两个新能力 PR 处于开放状态，值得关注：

- [#7982](https://github.com/earendil-works/pi/pull/7982)：在 JSON/RPC 的 `message_update` 事件中恢复携带 cumulative `usage`（修复 #7911），保持流大小线性。
- [#7953](https://github.com/earendil-works/pi/pull/7953)：在 `toolcall_start` 事件中增加常量大小的 `id` 与 `toolName` 字段，便于消费方在流开始阶段即可识别工具。

---

## 4. 社区热点

今日讨论最集中的几个 Issue 反映了当前用户的核心关注点：

- **[#7547 — How do you use Pi on Windows? What issues are you seeing?](https://github.com/earendil-works/pi/issues/7547)**（25 评论，1 👍）  
  开放式征集 Windows 用户的使用方式与痛点。评论数高说明 Windows 支持是当前社区最关心的话题之一——用户对“在 Windows 上到底应该怎么跑 Pi”感到困惑，维护者也借此收集信息以决定投入方向。

- **[#6187 — Pi login hangs in WSL after GitHub Copilot device authorization](https://github.com/earendil-works/pi/issues/6187)**（25 评论，已关闭）  
  WSL 环境下浏览器设备授权完成后客户端仍卡在登录态。该问题自 6 月 30 日创建、今日仍被更新，说明 WSL 用户群体不小且对登录体验敏感。

- **[#7730 — High CPU usage on Mac OS with long session](https://github.com/earendil-works/pi/issues/7730)**（10 评论，8 👍）  
  Mac 上长时间会话导致 CPU 占用 50%–100%+、内存 600–800MB。虽然没有崩溃那么严重，但 8 个 👍 表明很多 Mac 用户正在被此问题困扰。

- **[#7846 — Unable to start 0.84.0, 0.84.1 with bun runtime](https://github.com/earendil-works/pi/issues/7846)**（10 评论，1 👍）  
  bun 运行时下 `zlib.createZstdDecompress is not a function` 崩溃，阻断了一部分 bun 用户使用最新版本。

核心诉求分析：社区当前最在意的是 **跨平台（Windows/WSL/Mac）稳定性** 和 **运行时兼容性（bun）**。同时，围绕 Copilot 登录 429 的两条 issue（[#7850](https://github.com/earendil-works/pi/issues/7850)、[#7428](https://github.com/earendil-works/pi/issues/7428)）合计 12 个 👍，反映了使用 GitHub Copilot 企业/组织账户的用户对大模型列表规模带来的限流问题有强烈痛感。

---

## 5. Bug 与稳定性

按严重程度排列今日活跃的 Bug 类条目：

**严重阻断**

- **[#7846 — bun 运行时无法启动 0.84.0 / 0.84.1](https://github.com/earendil-works/pi/issues/7846)**：`zlib.createZstdDecompress is not a function` 导致运行时崩溃。影响所有 bun 用户升级到最新版。暂无对应 fix PR。
- **[#6187 — WSL 下 Copilot 设备授权后登录挂起](https://github.com/earendil-works/pi/issues/6187)**（已关闭）：浏览器侧授权完成后客户端检测不到，永久等待。该问题最终被关闭，但未在数据中看到对应修复说明，建议确认修复归属。

**高影响**

- **[#7954 — OpenAI 兼容 SSE 流永不结束导致会话永久挂起](https://github.com/earendil-works/pi/issues/7954)**：内容已完整返回，但连接不关闭，进程一直存活。✅ 已有修复 PR [#7959](https://github.com/earendil-works/pi/pull/7959)（已合并）。
- **[#7850 / #7428 — GitHub Copilot 登录 429（组织账户 20+ 模型时必现）](https://github.com/earendil-works/pi/issues/7850)**：已关闭，标记为 no-action；属于服务端限流，客户端暂时无法规避。
- **[#5291 — Anthropic 订阅用户会话经常卡在 “Working...”](https://github.com/earendil-works/pi/issues/5291)**：6 月 1 日创建，今日仍有更新，长期未解决，9 条评论、3 👍。

**中低影响 / 回归**

- **[#7979 — 回归：fallback 工具结果渲染器忽略 expanded 标志（v0.62.0+）](https://github.com/earendil-works/pi/issues/7979)**：`Ctrl+O` 对未自带 renderResult 的扩展工具（web_search、MCP bridge）无效，输出始终全文渲染。暂无 fix PR。
- **[#7911 — 0.84.0 起 wire 协议上 `message_update` 丢失 `usage` 字段](https://github.com/earendil-works/pi/issues/7911)**：修复 #7290 时顺带删掉了 `usage`，导致 JSON/RPC 消费方在流结束前拿不到 usage。✅ 已有修复 PR [#7982](https://github.com/earendil-works/pi/pull/7982)（开放中）。
- **[#7836 / #7835 — edit 工具模糊匹配与参数形态问题](https://github.com/earendil-works/pi/issues/7836)**：空白符差异导致模糊匹配失败；单对象 `edits` 参数被工具直接拒绝。✅ 对应修复 PR [#7978](https://github.com/earendil-works/pi/pull/7978) 与 [#7962](https://github.com/earendil-works/pi/pull/7962) 已合并。
- **[#7444 — WebSocket 重试仅处理两种错误码，其他 transient 错误直接中断回合](https://github.com/earendil-works/pi/issues/7444)**：`response.failed` 非 `previous_response_not_found` / `websocket_connection

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*