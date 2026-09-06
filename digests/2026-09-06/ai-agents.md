# OpenClaw 生态日报 2026-09-06

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-05 23:59 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-09-06

## 今日速览

过去24小时 OpenClaw 仓库保持极高的社区活跃度：共产生 **500 条 Issue 更新**（新开/活跃 438 条，关闭 62 条）与 **500 条 PR 更新**（待合并 285 条，已合并/关闭 215 条），并发布了 **v2026.9.2** 新版本。值得关注的是，Issue 中大量高优（P1）问题集中在**会话状态破坏与消息丢失**两大核心可靠性领域，且多条问题带有 `clawsweeper:no-new-fix-pr` 标签，说明维护者尚未找到明确修复路径；与此同时，以 @steipete 为代表的贡献者正密集提交测试修复与性能优化 PR，项目整体处在**功能迭代加快、稳定性修复压力增大**的阶段。

---

## 版本发布

### v2026.9.2 (openclaw 2026.9.2)
🔗 [查看 Release](https://github.com/openclaw/openclaw/releases)

**核心亮点：**
- **更快、更灵敏的聊天体验**：处理长对话记录和磁盘占用时保持聊天、仪表盘和会话交互的流畅响应
- **仪表盘直接查找**：减少冷加载工作
- **Gateway 事件循环外的持久化历史读取**：避免大会话造成的事件循环阻塞

**破坏性变更：** Release 说明文本截断，未展示完整的破坏性变更内容。从关联的 Issue #119720（同步持久化阻塞 Gateway 事件循环）来看，本次架构调整直指该问题，建议升级用户关注 **Gateway 事件循环外读取** 是否影响现有持久化插件（如 memory-core）的行为。

---

## 项目进展

### 今日合并/关闭的关键 PR

| PR | 标题 | 状态 | 意义 |
|---|---|---|---|
| [#139519](https://github.com/openclaw/openclaw/pull/139519) | fix(test): unblock CI after storage-failure regression assertion | ✅ 已合并 | 修复 #139409 合并导致的 CI 主分支失败，解除所有 PR 继承的阻断问题 |
| [#139466](https://github.com/openclaw/openclaw/pull/139466) | feat(browser): set up the Chrome extension from this Mac | ✅ 已合并 | 为 macOS 应用增加 Chrome 扩展本地设置流程（关闭 #139448） |
| [#139459](https://github.com/openclaw/openclaw/pull/139459) | feat: enable CLI agents by default | ✅ 已合并 | 默认启用 `gateway.cliAgents`，简化 Control UI 新会话页面流程 |

### 项目整体推进方向

- **性能优化集中提交**：@steipete 今日提交了约 15 个 PR，集中在 **Gateway 生命周期管理**（#139500 防悬挂关停）、**会话存储性能**（#139528 避免大存储中的慢速 incognito key 检查）、**浏览器快照分配优化**（#139532、#139502）等方向，可见项目当前正在经历一轮规模化性能调优。
- **测试基础设施修复**：多个 PR（#139519、#139524、#139531）专门修复主分支 CI 失败，表明项目正从 #139409 合并造成的回归中恢复。
- **UI/UX 改进密集**：Control UI 骨架屏加载（#139525）、会话重置通知修复（#137917）、Android/ iOS 设置页迁移到 Dashboard（#137494、#139514）等，显示桌面端与移动端体验正在同步打磨。

---

## 社区热点

### 今日讨论度最高的 Issues

| Issue | 标题 | 严重度 | 评论数 | 核心诉求 |
|---|---|---|---|---|
| [#69208](https://github.com/openclaw/openclaw/issues/69208) | Umbrella: duplicate transcript, replay, and context assembly across channels | P1 | 14 | 跨渠道（MSTeams、webchat、Telegram、followup queue、delivery-mirror）的重复录制/回放/上下文组装问题汇总，影响会话状态与消息丢失 |
| [#132762](https://github.com/openclaw/openclaw/issues/132762) | overflow retry can end successfully on a tool result without final delivery | P1 | 13 | overflow-retry 后重试以 toolResult 结尾而缺少最终助手回复，尽管标记成功 |
| [#53763](https://github.com/openclaw/openclaw/issues/53763) | Built-in headless browser for reliable web access without external dependencies | P3 | 12 | 希望内嵌 headless Chromium，不依赖用户 Chrome 或第三方 API |
| [#39476](https://github.com/openclaw/openclaw/issues/39476) | A2A sessions_send: target agent can call sessions_send back, causing duplicate messages | P1 | 12 | Agent A→B 的 A2A 消息如果 B 回调则导致 A 侧重复消息 |
| [#96975](https://github.com/openclaw/openclaw/issues/96975) | Isolate subagent completion from parent context | P2 | 12 | 希望默认只注入子代理状态+链接，不注入完整内容 |

**点评：** 高热度讨论集中在 **消息传递可靠性与去重** 这一核心体验问题上。多个看似独立的 issue（#69208、#132762、#39476）实则可追溯到会话上下文组装与重试机制的共同缺陷，用户端的直接感受是"机器人回复重复"或"消息丢失"，这类问题已被多个 issue 标记为 P1，说明对用户信任度伤害极大。

---

## Bug 与稳定性

### P0 级别

| Issue | 标题 | 状态 |
|---|---|---|
| [#91931](https://github.com/openclaw/openclaw/issues/91931) | Preseeded SOUL.md/IDENTITY.md/USER.md 使 OpenClaw 自动完成引导并**删除用户提供的 BOOTSTRAP.md** | 🔴 开放，已有 Linked PR |

### P1 级别（按风险类型分类）

| Issue | 标题 | 影响类型 | 是否有 Fix PR |
|---|---|---|---|
| [#136183](https://github.com/openclaw/openclaw/issues/136183) | Command executor 挂起：ssh 在等待 server banner 时被 SIGTERM（2026.8.1 回归，8.2 仍存在） | 功能回归 | ❌ 无 |
| [#135111](https://github.com/openclaw/openclaw/issues/135111) | 间歇性 "Provider completed tool call with malformed JSON arguments"（claude-sonnet-5，8.1 开始） | 功能回归 | ❌ 无 |
| [#132765](https://github.com/openclaw/openclaw/issues/132765) | agents_wait 忽略 timeoutSeconds——约 60 秒后作为工具错误死亡 | 超时控制 | ❌ 无 |
| [#119720](https://github.com/openclaw/openclaw/issues/119720) | 同步 agent 持久化和 transcript 维护在大规模下阻塞 Gateway 事件循环 | 性能/可用性 | ⚠️ v2026.9.2 已针对性优化 |
| [#112259](https://github.com/openclaw/openclaw/issues/112259) | 零载荷分派无重试/死信/用户可见失败，入站消息被静默丢弃 | 消息丢失 | ❌ 无 |
| [#110190](https://github.com/openclaw/openclaw/issues/110190) | 运行时上下文载体放置在用户消息之后导致模型严重混淆 | 上下文组装 | ❌ 无 |
| [#102534](https://github.com/openclaw/openclaw/issues/102534) | Cron 调度器定时器在重度超时后永久停止触发 | 定时任务 | ❌ 无 |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | OpenClaw 泄漏未收割的 hook/tool 子进程，导致僵尸进程堆积 | 资源泄漏 | ❌ 无 |
| [#54488](https://github.com/openclaw/openclaw/issues/54488) | followup drain 独占会话 lane，阻塞入站分派 20-30 分钟 | 消息延迟 | ❌ 无 |
| [#137332](https://github.com/openclaw/openclaw/issues/137332) | 混合 terminal requester-settle 批在所有权检查后永远重试（2026.9 回归） | 消息丢失 | ⚠️ `fix-shape-clear` 标签 |
| [#132720](https://github.com/openclaw/openclaw/issues/132720) | claude-cli 410 session_expired（2026.9.1-beta.1，有效 paste-token） | 认证问题 | ❌ 无 |
| [#132762](https://github.com/openclaw/openclaw/issues/132762) | overflow retry 以 toolResult 成功结束但无最终交付 | 消息丢失 | ❌ 无 |

### 稳定性观察

今日新出现的高关注回归有 **#137332**（2026.9 期间引入）和 **#136183**（8.1 引入，8.2 仍存在），说明近版本在会话归属与命令执行模块引入的回归仍在消化中。此外 **macOS Gateway 更新后不可恢复** 的问题（#85027）仍然开放，对桌面用户影响较大。

---

## 功能请求与路线图信号

| Issue | 标题 | 评论数 | 纳入可能性 |
|---|---|---|---|
| [#53763](https://github.com/openclaw/openclaw/issues/53763) | 内置 headless 浏览器，不依赖外部依赖 | 12 | 中——用户诉求强，但涉及依赖体积与安全审查 |
| [#14785](https://github.com/openclaw/openclaw/issues/14785) | 降低 tool schema token 开销（每会话约 3,500 tokens） | 10 | **高**——与当前性能优化主题高度一致，token 成本直接影响用户账单 |
| [#99583](https://github.com/openclaw/openclaw/issues/99583) | 智能会话自动命名（懒生成/廉价模型/主题感知） | 8 | 高——已有 LLM slug generator 在代码库中，推进成本低 |
| [#71452](https://github.com/openclaw/openclaw/issues/71452) | 消息列表分页替代硬编码 25 条限制 | 6 | 中——需要消息格式化模块改造 |
| [#6599](https://github.com/openclaw/openclaw/issues/6599) | /models 测试命令验证 fallback 链 | 11 | 中——提升运维可观测性 |
| [#54373](https://github.com/openclaw/openclaw/issues/54373) | 为注入的上下文段添加来源/易变性元数据 | 6 | 低——涉及系统提示词格式深层变化 |
| [#63990](https://github.com/openclaw/openclaw/issues/63990) | 多索引 embedding 记忆，模型感知故障转移 | 6 | 低——需架构级设计 |

**路线图判断：** 当前优化重点在**减少 token 开销**（#14785）和**沉浸式体验改进**（Control UI 骨架屏、TUI 滚动行为 #44130），预计下一版本将优先纳入**会话自动命名**与**tool schema 压缩**两类 Feature。

---

## 用户反馈摘要

### 高频痛点

1. **消息重复/丢失**：评论中多次出现"同一用户消息得到两条最终回复"（如 Feishu #49381 通道在模型 fallback 后重复；Telegram DM 路由到主会话 #41165），用户对消息可靠性感知最强。

2. **回复延迟/机器人无响应**：#53008 提到内存压缩阻塞主处理 lane 达 10+ 分钟，期间所有 Telegram 入站消息排队不处理；#54488 的 followup 队列独占问题导致 20-30 分钟延迟。有用户（#72015）指出在 multi-agent gateway 上启用 active-memory 后"正常回复变慢或不可靠"。

3. **升级带来的回归**：两周内多个用户报告升级到 2026.8.x 后出现全新的间歇性故障（malformed JSON #135111、ssh 挂起 #136183、Windows 上 exec/read 返回空结果 #105528），升级谨慎情绪在评论中上升。

4. **状态/用量展示不透明**：#111630 中 MiniMax-M3 的状态显示 `Context: ?/1.0m`，#101929 中上下文预估比实际收费高 2.3-2.6 倍，用户对成本"不可见"和"预估偏差过大"均表达了不满。

### 用户积极反馈

- Control UI 加载体验改进（骨架屏 #139525）获得社区好评
- 新版本在**长对话中保持聊天响应流畅**的核心改进获得关注（v2026.9.2 Release 说明）
- 移动端 Dashboard 设置整合（#139514/#139492）被看作改善跨端体验的积极信号

---

##

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目日报 — 2026-09-06

## 1. 今日速览

过去 24 小时项目整体处于 **中等偏高活跃度**：共产生 7 条 Issue 更新（6 条新开/活跃、1 条关闭）和 47 条 PR 更新（43 条待合并、4 条已合并/关闭），无新版本发布。活动重心明显集中在 **ACP（Agent Client Protocol）相关能力补齐** 上：Hermes 内置 Provider 的 PR #4864 正式落地，ACP 系列话题（标题生成凭据、harness parity、epic 跟踪）持续产生讨论。与此同时，Release v1.45.0 的发布 PR #4869 已启动，说明项目正处在 **下一版本发布前夕的功能收敛与质量加固阶段**。值得关注的是，Issue 侧评论量整体偏低（多数为 1–2 条），讨论深度仍有提升空间。

---

## 2. 版本发布

过去 24 小时 **无新版本发布（0 个 Releases）**。

但一个重要的版本信号已经出现：**Release v1.45.0 发布准备 PR #4869** 已由 @all-hands-bot 创建， checklist 显示版本号已设置为 1.45.0，集成测试与行为测试待全部通过后即可发版。建议社区用户留意该 PR 的最终合并时间，以规划升级窗口。

---

## 3. 项目进展

过去 24 小时共有 **4 条 PR 被合并或关闭**，但具体条目未包含在评论数最多的前 20 列表中，因此无法从当前数据中精确追踪其内容。从仍在活跃推进的开放 PR 来看，以下几项工作有明显进展信号：

- **Hermes ACP Provider 从 issue 走向实现**：PR #4864 提交了将 Hermes 作为内置 ACP Provider 的实现。值得关注的是，作者明确指出原定 `uvx --from git+…` 安装方案不可行（Hermes 有意阻止 wheel 构建），因此改为 shallow git checkout 机制。该 PR 是 Hermes 进军内置 ACP 阵营的关键一步，也牵动着 #4634 和 #4820 两个跟踪 issue 的进度。
- **Release v1.45.0 发布流程启动**：PR #4869 进入集成测试与行为测试阶段，仓库正为下一个小版本做准备。
- **流式事件重构持续深化**：PR #4822 与 #4700 均在 9 月 5 日有更新，两条都属于 streaming epic 的一部分。前者为 stream 引入身份标识，使客户端可按 ID 关闭任意流；后者将 `StreamingDeltaEvent` 从 Event 继承体系中解耦，属于破坏性重构。两者叠加表明流式传输架构正在向更独立的身份/分发模型演进。
- **一批 SDK 稳定性修复等待合入**：如 API Key 脱敏规则增强（#4771）、stream completion 保留逻辑修复（#4772）、hook 非字符串决策处理（#4773）、critic 接收 workspace git patch（#4585）、mcp 1.x Server decorator 兼容 shim（#4406）等，说明维护者近期在集中处理一批边界条件问题。

---

## 4. 社区热点

根据 Issue 评论数与 PR 讨论密度，今日热点集中在 **ACP 模式与 Agent Canvas 云端行为**：

- **#4867 — ACP 模式下对话标题生成因缺少凭据而失败**（评论 2 条｜👍 0）  
  Issue 指出 ACP 模式下对话由外部子进程驱动，LLM 设置实际是"惰性"（inert）的，但标题生成功能仍会发起真实 LLM 调用，并且解析到文档中标注为"不应被直接调用"的 ACP sentinel LLM，从而报错。该问题暴露出 **ACP 模式与内部 LLM 调用逻辑之间的边界模糊**，用户被迫面对与自身场景无关的凭据报错，属于典型的设计契约缺口。

- **#4820 — [Epic] Built-in ACP harness parity**（评论 2 条）  
  Epic 目标是将 Kimi、OpenCode、Pi、Hermes 和 Antigravity 做成与 claude-code、codex、gemini-cli 同级的内置 ACP Provider。9 月 4 日状态更新为 "2 of 4 landed"（Kimi #4714 和 Pi #4419），Hermes 的实现 PR #4864 已在昨日提交，说明 **ACP harness 覆盖范围正在快速扩大**，但达到完整 parity 仍有距离。

- **#4634 — 通过既有 ACP 路径添加 Hermes**（评论 2 条）  
  Hermes 是 #4627 harness comparison 套装中的最后一个。该 Issue 明确约束：**不得增加 agent-server 镜像体积**。PR #4864 的 git checkout 安装方式正是为此约束设计的，说明实现与约束之间已形成呼应。

- **PR #4864 — Hermes provider 机制讨论**  
  作者主动请求 reviewer "先审机制、而非只看 diff"，并解释了 Hermes 有意阻止 wheel 构建这一技术限制。这种"请重点审方案"的请求姿态，加上 ACP 是当前主线方向，预计会成为近期 review 讨论的焦点。

**热点诉求归纳**：社区当前最强信号是希望 **ACP 生态尽快达到 harness 全面 parity**，让更多外部 Coding Agent 能通过"标准路径"获得 SDK 同等能力（Canvas 可用 + evaluation harness 可用）。其次是希望 **ACP 模式下不再触发与宿主 LLM 配置无关的内部调用**。

---

## 5. Bug 与稳定性

按严重程度排序如下：

### 高

- **#4854 — Agent Canvas 云端确认操作返回 HTTP 405（Method Not Allowed）**  
  创建于 2026-09-03，昨日仍有更新。用户在 staging/prod 云端模式下点击高风险操作的 **Cancel** 或 **Continue** 均得到 `405 Method Not Allowed`，而 localhost/本地模式同一流程正常，可稳定复现。该 Bug 会直接阻断云端用户执行危险操作时的确认/取消决策，影响面较大。  
  **目前未见对应 fix PR。**

### 中

- **#4867 — ACP 模式标题生成使用 sentinel LLM 且缺少凭据时报错**

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-09-06

## 1. 今日速览

过去 24 小时 Pi 项目保持高度活跃：Issues 侧共更新 54 条（新开/活跃 8 条，关闭 46 条），PR 侧更新 18 条（待合并 8 条，已合并/关闭 10 条），并发布了一个新补丁版本 v0.85.1。值得关注的是，#9132（0.85.0 发布包缺失 `pi-server` 运行时依赖）这一严重的打包事故已在当日通过 #9170/#9172 合并修复并随 v0.85.1 发布，展现了较快的响应速度。社区热点集中在 Windows 支持（#7547，52 评论）、终端滚动异常（#5023，19 评论）以及新 provider 集成（#5363，18 评论/15 👍），说明用户对跨平台体验和多模型接入有持续且强烈的需求。整体项目健康度良好，维护者关闭了大量已解决或过时的 issue，保持仓库整洁。

---

## 2. 版本发布

### v0.85.1

**核心更新：GPT-6 Astra 接入**

- 通过 OpenAI API keys 和 OpenAI Codex 订阅两种方式提供 GPT-6 Astra 模型支持。
- 相关文档已更新：[API Keys](https://github.com/earendil-works/pi/blob/v0.85.1/packages/coding-agent/docs/providers.md#api-keys) 与 [OpenAI Codex](https://github.com/earendil-works/pi/blob/v0.85.1/packages/cod...) 说明。

**背后动因**

v0.85.1 的发布直接修复了 0.85.0 中一个严重打包缺陷（[#9132](https://github.com/earendil-works/pi/issues/9132)）：`@earendil-works/pi-coding-agent@0.85.0` 的 `dist/cli.js` 静态导入了未声明的运行时依赖 `@earendil-works/pi-server`，导致用户全新安装后无法正常导入或启动 CLI。该问题已在 #9170（声明运行时依赖）与 #9172（防止同类问题再次发布）中修复。

**破坏性变更/迁移注意事项**：无明确破坏性变更报告。

---

## 3. 项目进展

当日共合并/关闭 10 个 PR，重点进展如下：

**核心修复 — 0.85.0 打包事故**

- [#9170 fix(coding-agent): declare pi-server runtime dependency](https://github.com/earendil-works/pi/pull/9170) — 声明 `@earendil-works/pi-server` 运行时依赖，解决 `dist/index.js` 静态导入缺失导致的崩溃问题。
- [#9172 fix(coding-agent): prevent broken package root publication](https://github.com/earendil-works/pi/pull/9172) — 增加发布前防护机制，避免同类打包缺陷再次流入 npm。

**功能增强**

- [#9214 Invoke skills and prompt templates mid-sentence](https://github.com/earendil-works/pi/pull/9214) — 允许 skills 和 prompt templates 在输入行中句（非仅在首行）展开，直接回应 #8457 的需求。
- [#7970 feat(coding-agent): Show when the fullscreen transcript is scrolled up](https://github.com/earendil-works/pi/pull/7970) — 全屏 transcript 模式增加 `↓` 指示器，当用户回滚浏览历史时在状态栏显示，滚回底部自动消失。
- [#9163 feat(tui): Simplify clipboard handling](https://github.com/earendil-works/pi/pull/9163) — 简化剪贴板处理层，为 NixOS 等平台构建铺路。
- [#9166 feat(tui): accelerate Alt-modified wheel scrolling](https://github.com/earendil-works/pi/pull/9166) — Alt+滚轮加速 5 倍滚动，提升长会话浏览效率。
- [#9182 fix(coding-agent): skip session events on invalidated extension runners](https://github.com/earendil-works/pi/pull/9182) — 修复 `/new` 或 Ctrl+C 退出竞态下扩展运行时非法化导致的悬挂/崩溃。

**细节修复**

- [#9215 fix(tui): allow zero-row custom footers](https://github.com/earendil-works/pi/pull/9215) — 修复自定义 footer 在无内容时仍占用一空行的问题。
- [#9204 / #9208 fix(coding-agent): use --no-extensions flag in RPC extension UI example](https://github.com/earendil-works/pi/pull/9204) — 修正示例代码中的错误 CLI flag（`--no-extension` → `--no-extensions`）。

**待合并重要 PR（部分）**

- [#9116 / #9117](https://github.com/earendil-works/pi/pull/9116)：引入 mid-conversation system messages 及 system message deltas，是 #8998 的分层拆分，将重构系统提示的动态更新机制。
- [#9096 feat(ai,coding-agent): add Meta provider with Muse subscription OAuth](https://github.com/earendil-works/pi/pull/9096)：新增 Meta Muse 订阅模型。
- [#9137 feat(coding-agent): add Nix flake](https://github.com/earendil-works/pi/pull/9137)（WIP）。
- [#9179 fix(coding-agent): reject tree navigation during compaction](https://github.com/earendil-works/pi/pull/9179) — 修复 compaction 与 tree navigation 并发竞态。

---

## 4. 社区热点

**🔥 Windows 使用体验 — Issues [#7547](https://github.com/earendil-works/pi/issues/7547)（52 评论 / 2 👍 / 开放中）**

作者 @petrroll 提出 Windows 用户数量庞大但 Pi 的运行方式碎片化——有多重运行环境，难以确定核心团队应在何处集中投入（修 bug、完善文档、开箱即用体验），哪些场景应交给外部扩展支持。该帖已成为 Windows 用户的聚合反馈帖，评论区有大量用户汇报具体问题（如 #6300 输入重绘错乱、#5200 IME 候选框定位错误等）。这是 Pi 跨平台战略的关键信号：Windows 支持是社区最强烈的呼声之一。

**终端异常滚动 — Issues [#5023](https://github.com/earendil-works/pi/issues/5023)（19 评论 / 3 👍 / 已关闭）**

用户报告终端在模型输出过程中会随机跳转到会话开头又迅速滚动到底部。该 issue 被标记为 closed（可能在同一轮更新中因重复/已修复而关闭），但其高评论量说明终端渲染稳定性是 TUI 类 AI 工具的核心体验问题。

**Amazon Bedrock Mantle Provider — Issues [#5363](https://github.com/earendil-works/pi/issues/5363)（18 评论 / 15 👍 / 开放中）**

用户希望为 `packages/ai` 增加 `amazon-bedrock-mantle` provider——Bedrock Mantle 模型使用 OpenAI 兼容 API 端点，与现有 `amazon-bedrock` 的 Converse API 不兼容。15 个 👍 表明企业级 AWS 用户对 Bedrock 生态内 OpenAI 兼容模型的需求非常明确且强烈。

---

## 5. Bug 与稳定性

### 严重（已修复 / 有对应 fix PR）

| Issue/PR | 描述 | 状态 |
|---|---|---|
| [#9132](https://github.com/earendil-works/pi/issues/9132) | `0.85.0` 发布包 `cli.js` 静态导入未声明的 `@earendil-works/pi-server`，全新安装即崩溃 | ✅ #9170 + #9172 已合并，v0.85.1 已发布 |
| [#9036](https://github.com/earendil-works/pi/issues/9036) | `openai-codex` SSE 解析器将整个响应缓冲为一个字符串，导致致命 V8 堆 OOM | 已关闭，待确认修复版本 |
| [#9181 → #9182](https://github.com/earendil-works/pi/pull/9182) | session 替换期间扩展 runner 失效导致 teardown 悬挂 | ✅ #9182 已合并 |

### 中等问题

| Issue | 描述 | 状态 |
|---|---|---|
| [#9212](https://github.com/earendil-works/pi/issues/9212) | 经网关使用 `claude-sonnet-5` 时，13% 的 edit 工具调用被截断为 `edits:[{}]`（共 134 次调用中 18 次失败） | 已关闭（untriaged） |
| [#9210](https://github.com/earendil-works/pi/issues/9210) | 经网关使用 Anthropic Messages 时 `cacheWrite1h` 永远为 0，导致 1h 缓存写入按 5m 费率计费，成本虚高 | 已关闭（untriaged） |
| [#9216](https://github.com/earendil-works/pi/issues/9216) | Ollama `qwen3.8:27b` 从 0.84.x 升级到 0.85.x 后出现 stream `terminated` 回归 + auto-compaction 停止重触发 | 已关闭（untriaged） |
| [#9211](https://github.com/earendil-works/pi/issues/9211) | `vercelGatewayRouting` 配置在 `vercel-ai-gateway` provider 上不生效——所有模型仍走 `anthropic-messages` | 已关闭（untriaged） |
| [#8684](https://github.com/earendil-works/pi/issues/8684) | `PI_OFFLINE` 环境变量实际禁用了所有 provider model discovery，行为与文档描述不符 | 开放中 |
| [#9169](https://github.com/earendil-works/pi/issues/9169) | Windows 11 + WezTerm 全屏 TUI 模式下图片渲染异常（非全屏模式正常） | 已关闭（untriaged） |
| [#9180](https://github.com/earendil-works/pi/issues/9180) | 后台 catalog 刷新后 `/model` 选择器的 `scoped` 视图不更新（如新增的 `gpt-6-astra` 不可见） | 已关闭（untriaged） |
| [#9073](https://github.com/earendil-works/pi/issues/9073) | `JsonlSessionRepo` 的 cwd-scoped session ID 因目录编码碰撞（如 `tenant-a/project` vs `tenant/a-project`）而冲突 | 开放中 |

### 体验问题

- [#9209](https://github.com/earendil-works/pi/issues/9209)：GitHub Copilot 的 `gpt-6-astra` 被错误路由到不支持的 Chat Completions 端点。
- [#9199](https://github.com/earendil-works/pi/issues/9199)：TUI 不同菜单的键位交互不一致（`/` 菜单用 tab 补全、`@` 菜单用 select confirm）。

---

## 6. 功能请求与路线图信号

**高潜力（社区强烈需求，已有相关 PR 或讨论）**

- [#5363](https://github.com/earendil-works/pi/issues/5363) **Amazon Bedrock Mantle provider**（15 👍）— 企业 AWS/OpenAI 兼容模型接入，尚无对应 PR。
- [#9113](https://github.com/earendil-works/pi/issues/9113) **OpenAI async tool calling** — 支持 GPT-6 Astra 及后续模型的异步工具调用，工具执行时模型可继续工作。v0.85.1 已引入 GPT-6 Astra，该能力有望成为下一步关注点。
- [#8791](https://github.com/earendil-works/pi/issues/8791) **向扩展暴露 `ModelRuntime`**（4 👍）— 扩展需要创建隔离的进程内 agent 会话。已关闭（no-action），但方向与 agent harness 演进一致。

**已有 PR 推进中的功能**

- **Mid-conversation system messages / system message deltas**（[#9116](https://github.com/earendil-works/pi/pull/9116) + [#9117](https://github.com/earendil-works/pi/pull/9117)）— 重构运行时提示词和工具变化的传递机制，属于架构级改进，值得关注合并时间。
- **Meta / Muse provider**（[#9096](https://github.com/earendil-works/pi/pull/9096)）— 新增 Meta 模型供应商，含其特殊的每日 token 重铸机制。
- **LLM Gateway providers**（[#7610](https://github.com/earendil-works/pi/pull/7610)）— 接入 OpenRouter 风格路由服务 LLM Gateway。
- **Nix flake**（[#9137](https://github.com/earendil-works/pi/pull/9137)）— 官方 Nix 打包支持（WIP）。
- **Mermaid 终端渲染升级**（[#8158](https://github.com/earendil-works/pi/pull/8158)）。

**路线图信号**

- v0.85.1 新增 GPT-6 Astra，说明 Pi 紧跟最新模型。多个 provider 相关 PR（[#8734](https://github.com/earendil-works/pi/pull/8734) 支持 top-level instructions、#7610 LLM Gateway）也表明 Pi 正在持续扩充模型生态接入的广度与灵活性。
- #8457（/skill 和 /template 中句调用，4 👍）已由 #9214 合入，说明社区呼声能快速落地。

---

## 7. 用户反馈摘要

**Windows 支持的迫切需求**（[#7547](https://github.com/earendil-works/pi/issues/7547)）

> “There are gazzilion developers on windows... there are too many ways pi can be run on windows and as such it is hard to know where to focus energy”

用户希望核心团队明确 Windows 的推荐运行方式，并集中修复 Windows 特有的 TUI 问题。附带反馈包括 Windows 下输入行重绘错乱（[#6300](https://github.com/earendil-works/pi/issues/6300)）、IME 候选框定位错误（[#5200](https://github.com/earendil-works/pi/issues/5200)）、以及全屏 TUI 图片渲染问题（[#9169](https://github.com/earendil-works/pi/issues/9169)）。

**对发布质量的关注**（[#9132](https://github.com/earendil-works/pi/issues/9132)，5 👍）

打包事故引发了用户对 npm 发布质量的质疑。好在当天即完成修复并发布 v0.85.1，团队响应速度值得肯定。用户 @any-victor 还贡献了 #9172 防止同类问题复发，体现了社区对工程质量的高要求。

**成本透明与 Provider 行为一致性**（[#9210](https://github.com/earendil-works/pi/issues/9210)）

> “every assistant message records `cacheWrite1h: 0` even though the gateway honors the 1h TTL. `calculateCost` then bills all cache writes

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 开源项目动态日报 — 2026-09-06

## 今日速览

过去 24 小时项目活跃度中等偏上：2 条新 Issue、13 条 PR 更新（其中 4 条合并/关闭、9 条待合并），无正式版本发布。多条与 **reliability-2026** 计划相关的稳定性 PR 持续推进并落地，同时 **Nexus 协议兼容性**与 **SignalWithStart 行为对齐**成为当前修复热点。值得关注的是，**1.32.0 发布分支已准备就绪**（#11945），预示下一个 minor 版本即将进入发布流程。整体而言，项目在稳定性加固与协议合规两条线上均保持稳定推进，社区讨论集中在 Nexus `request-timeout` 格式缺陷上，对应的修复 PR 已在同一天提交，响应迅速。

## 版本发布

**无新版本发布。**

> 📌 信号：`temporal-cicd[bot]` 已提交 **1.32.0 发布分支准备** PR（#11945），包括覆盖 governance 文件与依赖更新。这通常意味着 1.32.0 的功能冻结与 RC 构建已进入倒计时，预计不久将有正式版本发布。

## 项目进展

过去 24 小时共有 4 条 PR 被合并/关闭，分别对应 **poller 扩缩容策略修正**、**子工作流异常可观测性**、**版本删除流程的 NDE 修复回退**以及**版本分支基建**：

- **[[reliability-2026] Fix poller scaling decisions for backlog tasks and rate-limited queues（#11618）— 已合并**  
  修复了任务队列 poller 扩缩容的两个错误信号：当任务来自 DB 积压时不发送缩容信号，队列被限流时不发送扩容信号。此前积压任务的等待时间会误导系统做出相反的扩缩容决策。该修复对任务队列的资源效率与稳定性有直接帮助。
  https://github.com/temporalio/temporal/pull/11618

- **[[reliability-2026, oss-foundations] Monitor child execution NotFound after ChildWorkflowExecutionStarted（#11447）— 已合并**  
  当 `ScheduleWorkflowTask` 对子工作流返回 NotFound 时，现在会发出 `child_execution_not_found` 计数器和 Error 日志，便于运维人员发现子工作流在启动后被移除的异常场景。不改变原有行为，纯可观测性增强。
  https://github.com/temporalio/temporal/pull/11447

- **[Log context for version delete propagation failures（#11941）— 已合并**  
  回退了 #11698 引入的一个变更——该变更在特定版本工作流场景下会导致计数器未递减，进而影响版本工作流的 CAN'ing 速率控制（命名空间版本删除传播的限速机制）。修复恢复了正确的 counter 递减行为并保留日志上下文。
  https://github.com/temporalio/temporal/pull/11941

- **[[自动] 1.32.0: Prepare release branch（#11945）— 已合并/关闭**  
  版本发布分支基建，通常由 CI 自动完成，不代表功能变更。
  https://github.com/temporalio/temporal/pull/11945

**此外，以下高价值 PR 正在排队等待合入：**

- **#11944 — fix: format Nexus request-timeout with FormatDuration**（新开，直接修复 #11569），将 Nexus `request-timeout` 的格式化从 `time.Duration.String()` 切换为 `commonnexus.FormatDuration`，确保符合 Nexus 协议语法。这是对当日最热 Issue 的即时响应。
  https://github.com/temporalio/temporal/pull/11944

- **#11397 — Fix constant/error-dependent retry jitter being truncated to a no-op** 修复了 `common/backoff/retrypolicy.go` 中 `addJitter` 因整数截断导致的抖动失效问题，已在队列中等待约一个月。
  https://github.com/temporalio/temporal/pull/11397

- **#11810 — [reliability-2026] Fix SignalWithStart bypassing continue-as-new backoff** 修复 `SignalWithStart` 绕过 workflow-initiated continue-as-new 的 backoff 问题，属于工作流语义一致性的重要修正。
  https://github.com/temporalio/temporal/pull/11810

## 社区热点

今日讨论最集中的是 **#11569 — Nexus 服务器可能发送畸形 `request-timeout` 头**，累计 3 条评论，是过去 24 小时社区互动最多的条目，且由核心维护者 @mjameswh 提交：

> **#11569** [OPEN] Nexus: server may send malformed `request-timeout` header (negative values and units outside the Nexus grammar)  
> 作者指出服务器在计算剩余超时时间时可能产生**负值**或超出 Nexus 词法单元的 `µs/ns` 等单位，违反 Nexus 协议规范中对 duration 格式的定义（仅允许 `ms`、`s`、`m`，不允许符号）。
> https://github.com/temporalio/temporal/issues/11569

**诉求分析**：这反映出社区对 **Nexus 协议合规性** 的重视——尤其是当 Temporal 作为 Nexus 服务端时，HTTP 头部必须严格遵循 Nexus 规范，否则下游 SDK/客户端可能解析失败。该 Issue 在当天即获得修复 PR（#11944），体现了维护团队对协议边界问题的高优先级响应。

另一条新 Issue **#11943（Version check HTTP request has no timeout or cancellation）** 目前尚无评论，但触及生产环境常见的稳定性隐患（HTTP 请求悬挂），预计会引发后续讨论。

## Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue/PR | 描述 | 状态 |
|---------|----------|------|------|
| 🟠 中高 | [#11943](https://github.com/temporalio/temporal/issues/11943) | **版本检查 HTTP 请求无超时/取消**：`VersionChecker` 可因 version-info 请求悬挂而无限阻塞，Stop 时无法取消已发出的请求，后台 goroutine 无法退出，可能导致 goroutine 泄漏。 | 新开，无修复 PR |
| 🟡 中 | [#11569](https://github.com/temporalio/temporal/issues/11569) | **Nexus 服务器发送畸形 `request-timeout` 头**：可能出现负值以及 `µs`/`ns` 等 Nexus 语法不允许的时间单位，导致下游解析失败。 | 已有修复 PR：[#11944](https://github.com/temporalio/temporal/pull/11944) |
| 🟢 低 | [#11397](https://github.com/temporalio/temporal/pull/11397) | **重试抖动失效**：`addJitter` 因整数截断始终不生效，所有重试延迟固定为基准值而非预期的 `[base, base+jitter)` 区间。 | 修复 PR 待合并，已积压约 35 天 |

**健康度评估**：近期合并的 #11941 表明项目对命名空间版本删除这类易引发级联故障的路径保持了审慎态度，发现 NDE 后很快回退并修正。整体 bug 响应速度良好，Bug → Fix PR 的间隔在当天级别。

## 功能请求与路线图信号

暂无全新的用户功能请求，但以下待合并 PR 传递了明确的路线图信号：

- **Nexus 可观测性增强（#11927）** — 为 `callback_outbound_requests` 和 `callback_outbound_latency` 指标新增 `nexus_completion_source` 标签，便于按回调来源区分监控。结合 #11569 与 #11944，Nexus 相关能力正在经历一轮"合规性 + 可观测性"的系统性打磨。
  https://github.com/temporalio/temporal/pull/11927

- **通用分页错误语义（#11940）** — 将分支不匹配错误从 `CurrentBranchChanged` 改为通用 `ErrInvalidNextPageToken`，避免将内部实现细节泄露给客户端。可视为 API 错误语义清理的一部分。
  https://github.com/temporalio/temporal/pull/11940

- **Standby 任务验证容错（#11939）** — 子工作流处于陈旧分支时不再返回错误，使 standby 验证标记任务完成并避免无限重试。属于多集群/standby 场景的稳定性优化。
  https://github.com/temporalio/temporal/pull/11939

- **Eager dispatch 匹配 API（#11872）** — 新增 `GrantEagerDispatch` 匹配服务 RPC，配套生成 clients/mocks/metrics/retry 全链路。这是 **eager workflow/activity dispatch** 方向的底层能力铺垫，值得关注其在未来版本中的落地。
  https://github.com/temporalio/temporal/pull/11872

- **活动失败信息总大小限制（#11644）** — 引入新的动态配置 `limit.mutableStateActivityFailureTotalSize.error`，将 mutable state 中所有 pending activity 的 `RetryLastFailure` 总量限制为 6MB（默认），防止累积的失败详情撑爆 mutable state 上限（8MB）。属于面向超大规模工作流的防御性改进。
  https://github.com/temporalio/temporal/pull/11644

## 用户反馈摘要

过去 24 小时社区直接反馈集中在 #11569 的技术细节讨论中，核心观点为：

- **痛点**：Nexus `request-timeout` 头的格式必须严格匹配协议语法。`time.Duration.String()` 可能产生 `-3.5s`、`1500µ

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*