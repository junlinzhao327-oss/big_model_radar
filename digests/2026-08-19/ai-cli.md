# AI CLI 工具社区动态日报 2026-08-19

> 生成时间: 2026-08-18 22:36 UTC | 覆盖工具: 7 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比



---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---

# Claude Code 社区动态日报 — 2026-08-19

## 今日速览

- **v2.1.235 发布**：新增可选拼写检查功能，并修复了语言服务器断开/重连导致整轮 prompt cache 失效的问题。
- **两条高热度 Issue 持续发酵**：关于上下文压缩后记忆丢失的讨论（89 评论）与 GitHub 连接器未被 CLI 识别（88 评论、139 👍），成为社区最集中反馈的两大痛点。
- **Windows 桌面端回归问题集中浮现**：跨会话消息被静默丢弃、`send_message` 假成功等近期回归引发关注，多条均在近一周内报告。

## 版本发布

### v2.1.235
- **新增 `spellcheck` 设置**：在 prompt 输入框输入时，调用系统已安装的 `aspell` / `hunspell` / `ispell` 为拼写错误的单词加下划线。
- **修复**：语言服务器在会话中断开或重连时，导致整轮 prompt cache 被无效化的问题。
- **修复**：嵌套 m…（Changelog 截断，建议到 Release 页面查看完整条目）。

---

## 社区热点 Issues（Top 10）

### 1. 跨上下文压缩的持久记忆 — Feature Request / 自建方案
- **Issue**: [#34556](https://github.com/anthropics/claude-code/issues/34556)（CLOSED · 89 评论 · 👎 6? — 实际 👍 6）
- 作者记录了 **26 天内经历的 59 次压缩**，由于 Claude Code 在每次上下文压缩后丢失未外部保存的一切内容，作者干脆自己构建了一套完整的记忆持久化系统。这条 Issue 侧面反映了**长期会话工作流在无持久记忆下的极高摩擦**，评论区也成为了自建方案的交流现场。

### 2. GitHub Connector 在 Claude Desktop 已连接，但 CLI 不识别
- **Issue**: [#32479](https://github.com/anthropics/claude-code/issues/32479)（OPEN · 88 评论 · 139 👍）
- 用户在 Desktop 端已成功连接 GitHub，但 Claude Code CLI 完全感知不到该集成。这是当前获得 👍 最多的 Issue，说明**桌面端与 CLI 的集成状态不同步**影响面很大，且距创建已 5 个多月仍未解决。

### 3. API Error: Connection closed mid-response — 频繁到无法使用
- **Issue**: [#69415](https://github.com/anthropics/claude-code/issues/69415)（OPEN · 53 评论 · 81 👍）
- 在 VS Code + WSL 环境下，API 连接在响应中途反复关闭，频率高到让 Claude Code 无法完成任何任务。53 条评论说明这不是个例，**网络层稳定性**已经成为阻塞性痛点。

### 4. Windows 桌面端跨会话消息被静默丢弃
- **Issue**: [#86298](https://github.com/anthropics/claude-code/issues/86298)（OPEN · 19 评论 · 1 👍）
- 回归自桌面端 1.28929.0：跨会话消息会进入一个 UI 永远不会展示的审批等待状态，约 5 分钟后过期；**而发送方完全无感知**。对消息可靠性的打击极大，且提交于 8 月 13 日，是近期快速升温的新回归。

### 5. Cowork VM 连接超时（Intel Mac 回归）
- **Issue**: [#87503](https://github.com/anthropics/claude-code/issues/87503)（CLOSED · 8 评论 · 0 👍）
- 升级至 1.32352.0 后，Intel Mac 上 Cowork VM 连接超时，guest 永远连不上。已关闭，但符合“**新版本在特定平台引入即回归**”的模式，需要留意修复验证。

### 6. `getCurrentOutputStyleName is not defined` — 核心回归
- **Issue**: [#71980](https://github.com/anthropics/claude-code/issues/71980)（CLOSED · 7 评论 · 1 👍）
- 从 2.1.193 开始，启动/恢复会话直接崩溃，报 `ReferenceError: getCurrentOutputStyleName is not defined`，2.1.191 不受影响。属于**核心启动路径回归**，跨越多个版本仍存在，说明发布前回归测试存在盲区。

### 7. Opus 4.8 严重多症状退化（桌面端）
- **Issue**: [#66539](https://github.com/anthropics/claude-code/issues/66539)（CLOSED · 7 评论 · 2 👍）
- 自 6 月 8 日起，桌面端 Opus 4.8 出现多症状退化：忽略 CLAUDE.md、绕过权限确认、幻觉、拒绝可执行任务、未经提示直接写文件。虽然标签带 `stale` 且已关闭，但**模型行为可靠性与权限边界的讨论价值仍然很高**。

### 8. `send_message` 在原生 Windows 上假成功
- **Issue**: [#86603](https://github.com/anthropics/claude-code/issues/86603)（OPEN · 6 评论 · 0 👍）
- 在原生 Windows 上，跨会话消息并未真正提供，但 `send_message` 仍然返回成功：没有 inbox socket 绑定、没有任何投递，调用方无法区分成功与否。注意 payload 还是**明文存储**的，涉及安全问题。

### 9. Bash 工具描述内嵌会话 URL，导致每次 `/resume` 整轮 prompt cache 失效
- **Issue**: [#87137](https://github.com/anthropics/claude-code/issues/87137)（OPEN · 1 评论 · 0 👍）
- 一个非常漂亮的成本/性能洞察：`Bash` 工具描述里带着每个会话唯一的 console URL，而工具定义排在 system prompt 最前面，URL 一变，整个缓存前缀就失效了。**每次恢复会话都要全量重读**，对长会话用户意味着显著的成本浪费。

### 10. Claude Code 声称工作完成但从不验证，WebGL 项目浪费数小时
- **Issue**: [#66054](https://github.com/anthropics/claude-code/issues/66054)（CLOSED · 5 评论 · 0 👍）
- 用户要求 WebGL 星云背景，Claude Code 连续写出含类型错误的 GLSL shader、部署了完全不生效的方案，却反复声称已完成。**“假装完成”的可靠性问题**会极大消耗开发者对工具的信任，与 #66539 模型退化不无关联。

---

## 重要 PR 进展

过去 24 小时内 PR 活动较少，仅 2 条更新，全部列出：

### 1. add the missing source to claude code
- **PR**: [#41611](https://github.com/anthropics/claude-code/pull/41611)（OPEN · 作者 @tornikeo）
- 一个来源不明的外部 PR，标题内容模糊（"add missing source"），创建于 3 月 31 日，但直到 8 月 18 日仍有更新。建议先阅读 diff 再决定是否合入。

### 2. ralph-wiggum: use disable-model-invocation so the model can't self-invoke /ralph-loop
- **PR**: [#87395](https://github.com/anthropics/claude-code/pull/87395)（CLOSED · 作者 @bcherny）
- 修复 ralph-wiggum 插件的漏洞：此前用 `hide-from-slash-command-tool: "true"` 来隐藏 `/ralph-loop`，但该 frontmatter 字段根本不受支持，Claude 可以自行调用 `/ralph-loop` 陷入循环。改为使用 `disable-model-invocation` 后，模型无法再自我触发。**对插件开发者是很好的 fetch，能让插件更安全地限制模型访问权限。**

---

## 功能需求趋势

综合全部 Issue 更新，社区最关注的功能方向有五个：

1. **长期记忆 / 状态持久化**
   - 代表 Issue: [#34556](

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-19

## 今日速览

今日最重要的动态集中在三个方面：**Codex CLI 0.148.0 正式发布**，带来了 TUI 对话导出、会话 fork 与归档等增强；**Windows 平台成为 bug 重灾区**，多个归档失败、浏览器插件初始化失败问题集中爆发；同时社区对 **token 消耗过快（#14593）** 的讨论热度持续攀升，累计 630 条评论，成为当前最受关注的问题。

---

## 版本发布

### rust-v0.148.0（正式版）
🔗 https://github.com/openai/codex/releases/tag/rust-v0.148.0

**新功能：**
- **TUI 对话导出**：使用 `/export` 可将完整 TUI 对话导出为 Markdown，支持复制到剪贴板或保存为新文件（#37358）
- **会话 Fork/归档**：`codex exec fork` 支持 fork 会话；TUI 恢复选择器中可直接归档或恢复会话（#37367, #37369, #37371）
- **启动效率**：TUI 初始化期间即可起草提示（#37375）

另外，`rust-v0.148.0-alpha.22` 和 `rust-v0.148.0-alpha.23` 两个预发布版本也已推送，为正式版提供增量修复。

---

## 社区热点 Issues（Top 10）

### 🔥 1. #14593 — Token 消耗速度异常快
- **链接**: https://github.com/openai/codex/issues/14593
- **热度**: 630 评论 | 285 👍 | 状态: OPEN
- **为什么重要**: 社区中持续最久、讨论最激烈的问题之一，大量用户反馈在 VS Code 扩展（Business 订阅）下 token 被异常快速消耗，直接影响使用成本。已持续 5 个月仍未解决，说明根因复杂。

### 2. #20500 — 支持每个应用/连接器多个命名账户
- **链接**: https://github.com/openai/codex/issues/20500
- **热度**: 28 评论 | 107 👍 | 状态: OPEN
- **为什么重要**: 功能需求类 issue 中获赞最高，开发者希望在同一 Codex 会话中连接多个独立授权的账户（如同一连接器的多个 GitHub 账号），并需要明确的账户选择和隐私边界。

### 3. #39136 — Windows 内置浏览器插件初始化失败：Trusted RPC 依赖不在可信代码路径中
- **链接**: https://github.com/openai/codex/issues/39136
- **热度**: 59 评论 | 17 👍 | 状态: OPEN
- **为什么重要**: 影响 ChatGPT Plus 用户在 Windows 上使用 Codex App 内置浏览器功能，是当日新增 issue 中评论增速最快的。

### 4. #37380 — 0.147.0 回归：Azure Responses 拒绝空函数命名空间描述
- **链接**: https://github.com/openai/codex/issues/37380
- **热度**: 18 评论 | 40 👍 | 状态: OPEN
- **为什么重要**: 自定义 Azure OpenAI 提供商在升级到 0.147.0 后完全不可用，`gpt-5.6-sol` 模型的工具调用被拒绝。40 个 👍 说明大量 Azure 企业用户受影响。

### 5. #30408 — MCP 服务器进程泄漏：每个线程的进程从未清理（RSS 超 9GB）
- **链接**: https://github.com/openai/codex/issues/30408
- **热度**: 29 评论 | 8 👍 | 状态: OPEN
- **为什么重要**: app-server 为每个新线程生成一套全局 MCP 进程，但在线程归档/关闭后从不终止，导致内存无界累积。这是长期运行用户的重大稳定性隐患。

### 6. #38455 — macOS 上 Computer Use worker 反复生成并崩溃（V8 OOM）
- **链接**: https://github.com/openai/codex/issues/38455
- **热度**: 26 评论 | 12 👍 | 状态: OPEN
- **为什么重要**: 26.810.41047 版本在空闲 98 秒后崩溃，崩毁时 316 个线程中有 187 个名为 computer-use。旧版 26.730.61639 正常，确认是回归。

### 7. #37403 — [macOS] 回归：桌面端无法恢复 Remote Control / CLI 线程 `already has an active writer`
- **链接**: https://github.com/openai/codex/issues/37403
- **热度**: 25 评论 | 18 👍 | 状态: OPEN
- **为什么重要**: 影响 Remote Control 工作流——用户在移动端遥控 Mac 上的 CLI 线程后，桌面端无法再打开同一线程，对远程协作场景造成严重阻断。

### 8. #31864 — GPT-5.6 Sol 所有 turn 失败：MultiAgentV2 使用保留的 collaboration.spawn_agent
- **链接**: https://github.com/openai/codex/issues/31864
- **热度**: 7 评论 | 17 👍 | 状态: OPEN
- **为什么重要**: 系统性故障——所有涉及 GPT-5.6 Sol 的会话在模型处理提示前即报错，错误信息显示 `collaboration.spawn_agent` 被保留但配置不匹配。

### 9. #39269 — Windows: Voice Chat Fork 丢失父项目上下文、模型选择和 AGENTS 启动行为
- **链接**: https://github.com/openai/codex/issues/39269
- **热度**: 6 评论 | 0 👍 | 状态: OPEN
- **为什么重要**: 当日新增，Windows 桌面端从新任务发起 Voice Chat 时，fork 出的子会话未能继承父任务的模型配置（GPT-5.6 Terra）和项目上下文。

### 10. #23186 — 自定义提供商下 MCP 工具被包装为 type:"namespace"，严格 schema 后端无法解包
- **链接**: https://github.com/openai/codex/issues/23186
- **热度**: 5 评论 | 18 👍 | 状态: OPEN
- **为什么重要**: 自定义 Responses API 提供商（如 llama.cpp）无法使用 MCP 工具，因为 Codex 将 MCP 工具包裹在 `type:"namespace"` 扩展中，而多数后端只认 `type:"function"`。18 👍 显示在本地模型用户中关注度极高。

---

## 重要 PR 进展（Top 10）

### 1. #39296 — 在 Codex 会话中启用 MCP 工具钩子
🔗 https://github.com/openai/codex/pull/39296
通过会话的共享 MCP 运行时执行 `mcp_tool` 钩子，仅允许已连接、已编目且策略允许的工具，不可用的服务器立即失败。

### 2. #39299 — 将 agent 角色限制为有界配置覆盖
🔗 https://github.com/openai/codex/pull/39299
子 agent 只能通过角色覆盖模型行为和开发者配置，不能扩大权限或更改继承自父会话的提供商配置，安全性提升。

### 3. #39301 — 防止 Node REPL 认证令牌到达子进程
🔗 https://github.com/openai/codex/pull/39301
将 `NODE_REPL_AUTH_TOKEN` 加入模型可达子进程不可继承的环境变量列表，并支持大小写不敏感的移除，关键安全修复。

### 4. #39285 — 在 TUI 变更审批中显示文件目标
🔗 https://github.com/openai/codex/pull/39285
每个文件变更批准现在显示描述和受影响的目标路径，移动操作同时显示源路径和目标路径，跨平台格式化路径，不可用时显示 unavailable。直接回应 #36637。

### 5. #39290 — 为 `codex doctor` 添加 Windows 沙箱诊断
🔗 https://github.com/openai/codex/pull/39290
报告配置的 Windows 沙箱后端及 denied-read 限制是否生效，诊断不兼容的代理策略、不完整/失败的沙箱配置等。

### 6. #39294 — 增加 SQLite 日志接收器批处理
🔗 https://github.com/openai/codex/pull/39294
默认有界日志队列容量从 512 提升至 2,048，插入批大小从 128 提升至 512，刷新间隔从 2 秒延长至 10 秒，减少 I/O 压力。

### 7. #39284 — 报告审批期间的网络断开
🔗 https://github.com/openai/codex/pull/39284
当本地代理请求在审批完成前断开时，为所属工具调用生成模型可见的断开说明，避免工具调用悬空。

### 8. #39298 — 允许覆盖 Codex 包版本
🔗 https://github.com/openai/codex/pull/39298
新增 `--package-version` 参数设置写入 `codex-package.json` 的版本，并拒绝不兼容的语义版本值（如溢出数字组件）。

### 9. #39277 — 声明实验性 Amazon Bedrock 设置 API
🔗 https://github.com/openai/codex/pull/39277
新增实验性 `account/bedrock/discover` 和 `account/bedrock/setup` 请求，定义 AWS profile 与环境凭据的发现结果及设置输入，AWS 集成方向的重要铺垫。

### 10. #39303 — 记录 Guardian v2 分类 token 使用
🔗 https://github.com/openai/codex/pull/39303
将会话归属的扩展指标传递给 Guardian v2 采样器，记录分类 token 使用直方图（总量、输入、缓存输入、输出等），提升可观测性。

---

## 功能需求趋势

从过去 24 小时的 Issues 中，社区最关注的五个功能方向为：

1. **多账户/多身份支持（#20500, 107👍）**：同一 Codex 会话连接多个独立授权账户，是当前最高优的功能请求，说明企业用户对隔离和切换有强烈需求。
2. **跨提供商会话交接（#38365, #23186, #36942）**：用户在 GPT 会话与自定义模型（llama.cpp、MiniMax 等）之间切换时，希望保留工作上下文并实现功能对等——特别是 MCP 工具在自定义提供商下的可用性。
3. **Windows 平台完善（#39136, #39209, #39236, #39239, #39269）**：归档失败（`\\?\` 路径问题）、浏览器插件修复流程失效、Voice Chat fork 上下文丢失——Windows 已成为缺口最明显的平台。
4. **输入/输出限制与用量透明化（#14593, #39167, #39260）**：用户强烈要求更透明的 token 消耗、限额计算和用量记录。信用账本冻结、限额跳变等数据异常加剧了不信任感。
5. **性能与稳定性（#30408, #38455, #38939, #38787, #38565）**：MCP 进程泄漏、Computer Use 线程失控导致 OOM、线程恢复二次复杂度等问题说明 Codex 在长期运行/大线程场景下的资源管理仍需加强。

---

## 开发者关注点

- **🔥 高频痛点：token 消耗过快且账单不透明** — #14593 累计 630 条评论仍在增长；#39167 报告 Pro 20x 周限额在零活动的一夜之间从 88% 跳到 100%；#39260 显示信用使用账本自 8 月 8 日起完全冻结。这三个 issue 共同指向一个核心问题：**用户无法信任用量计量，也无法有效控制成本**。
- **Windows 归档功能连环失效** — #39209、#39239 均报告 `thread/archive` 在 rollout 路径使用 `\\?\` 前缀时失败（os error 2）；#39269 报告 Voice Chat fork 丢失上下文；#39236 报告 Chrome 修复流程无法重建 RPC 配置。Windows 用户的基础操作可靠性明显落后于 macOS。
- **自定义模型/本地模型生态受阻** — #23186（18👍）、#31354、#26977 三连 issue 均指向同一个问题：MCP 工具在自定义 Responses API 提供商下返回 `unsupported call` 或无法解包 `type:"namespace"`。社区已提出增加扁平化工具选项的功能请求（#36942），但官方尚未回应。
- **MCP 资源泄漏** — #30408 的 9GB+ RSS 泄漏获得 29 条评论，开发者普遍认为 app-server 在线程生命周期管理上存在根本缺陷，需要立即修复。
- **macOS 稳定性回归** — #38455、#38939 两个 issue 都描述 Computer Use 在 macOS 上失控产生大量 worker 线程并最终 V8 OOM 崩溃，且崩溃后无法正常使用 App。开发者建议回滚至 26.730.61639 作为临时规避。

---

*本日报基于 GitHub 公开数据生成，数据抓取时间：2026-08-19。Issues 与 PR 按评论数/关注度综合排序，完整列表请见 https://github.com/openai/codex/issues 与 https://github.com/openai/codex/pulls。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**2026-08-19** | 数据来源: [github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)


## 今日速览

昨夜发布的 v0.56.0-nightly 主要围绕 SSR Agent 的修复，同时社区对子代理可靠性的讨论热度最高：Subagent 在达到 MAX_TURNS 后被误报为成功（#22323）以及 Generalist agent 无限挂起（#21409）是两个最受关注的问题。此外，官方 SSR Agent 今天集中提交了一批安全相关修复，覆盖 OAuth 超时、Cloud Shell 404 及子进程安全加固等。

## 版本发布

### v0.56.0-nightly.20260818.g194edea47
- **[SSR Agent]** 澄清隐私通知措辞与选择选项（[#28820](https://github.com/google-gemini/gemini-cli/pull/28820)）
- **[SSR Agent]** 修复集成测试中的 TypeScript strict-null 错误（[#28820](https://github.com/google-gemini/gemini-cli/pull/28820) 关联）

## 社区热点 Issues

本周精选 10 个值得关注的问题，覆盖 P1/P2 高优先级缺陷与重大功能方向：

### 1. Subagent 达到 MAX_TURNS 后被误报为成功
**#22323** | [priority/p1, kind/bug] | 12 评论 | 2 👍
[链接](https://github.com/google-gemini/gemini-cli/issues/22323)
`codebase_investigator` 子代理在自身结果明确显示"达到最大轮次、未做任何分析"的情况下，仍报告 `status: "success"` 和 `Termination Reason: "GOAL"`，严重误导用户判断任务真实状态。

### 2. Generalist agent 无限挂起
**#21409** | [priority/p1, kind/bug] | 8 评论 | 8 👍
[链接](https://github.com/google-gemini/gemini-cli/issues/21409)
当 Gemini CLI 委派任务给 generalist agent 时，即使简单操作（如创建文件夹）也会永久挂起，用户等待长达一小时。社区临时解决办法是显式指示模型不要使用子代理。

### 3. Shell 命令执行完成后卡在"等待输入"
**#25166** | [priority/p1, kind/bug] | 4 评论 | 3 👍
[链接](https://github.com/google-gemini/gemini-cli/issues/25166)
极简单的 CLI 命令执行完毕后，Gemini 仍显示"Awaiting user input"并挂起，即命令实际已完成但界面状态未更新，影响日常自动化流程。

### 4. Browser 子代理在 Wayland 下失败
**#21983** | [priority/p1, kind/bug] | 4 评论 | 1 👍
[链接](https://github.com/google-gemini/gemini-cli/issues/21983)
浏览器子代理在 Wayland 会话中无法正常工作，报错后以 `Termination Reason: GOAL` 结束，但实际任务未完成，与 #22323 的问题表现相似。

### 5. get-shit-done 输出钩子导致崩溃
**#22186** | [priority/p1, kind/bug] | 3 评论
[链接](https://github.com/google-gemini/gemini-cli/issues/22186)
当 get-shit-done 输出接近完成（即将打印用户摘要）时，Gemini CLI 频繁崩溃，疑似输出钩子存在边界条件缺陷。

### 6. 零依赖 OS 沙箱与执行后意图路由
**#19873** | [priority/p2, kind/enhancement, effort/large] | 8 评论 | 1 👍
[链接](https://github.com/google-gemini/gemini-cli/issues/19873)
利用 Gemini 3 模型原生 bash 操作能力，提出通过零依赖 OS 沙箱 + 执行后意图路由，在保证安全的前提下充分发挥模型的命令行工具链偏好。

### 7. 组件级评估体系（EPIC）
**#24353** | [priority/p1] | 7 评论
[链接](https://github.com/google-gemini/gemini-cli/issues/24353)
现有 76 个行为评估测试仅覆盖 6 个 Gemini 模型，此 EPIC 旨在建立更健壮的组件级评估设施，解决 eval 覆盖不足和基础设施欠缺的问题。

### 8. AST 感知的文件读取、搜索与映射（EPIC）
**#22745** | [priority/p2, kind/feature] | 7 评论 | 1 👍
[链接](https://github.com/google-gemini/gemini-cli/issues/22745)
系统评估 AST 感知工具的价值：更精确读取方法边界、减少因读取错位导致的多次调用和 token 浪费，并改善代码库导航（[关联 #22746](https://github.com/google-gemini/gemini-cli/issues/22746)）。

### 9. Gemini 不会主动使用 skills 和子代理
**#21968** | [priority/p2, kind/bug] | 6 评论
[链接](https://github.com/google-gemini/gemini-cli/issues/21968)
社区反馈：Gemini 基本不会自主调用用户自定义的 skills 和子代理，即使任务高度相关（如 gradle/git skill），只有显式指示才会使用，导致自定义工作流形同虚设。

### 10. Auto Memory 对低信号会话无限重试
**#26522** | [priority/p2, kind/bug] | 5 评论
[链接](https://github.com/google-gemini/gemini-cli/issues/26522)
Auto Memory 后台提取代理仅将成功 `read_file` 的会话标记为已处理，低信号会话会被无限次重新暴露给提取代理，造成资源浪费。关联问题还包括[无效补丁静默跳过 #26523](https://github.com/google-gemini/gemini-cli/issues/26523) 和[日志安全改进 #26525](https://github.com/google-gemini/gemini-cli/issues/26525)。

## 重要 PR 进展

今日合并/提交的 PR 以 SSR Agent 批量修复为主，另有若干核心稳定性改进：

### 1. 加固子进程执行安全、配置摄入与 GitHub API 交互
**#28898** | OPEN | [size/m]
[链接](https://github.com/google-gemini/gemini-cli/pull/28898)
防止敏感认证令牌泄漏到不可信工具执行环境，提升核心编排子进程的可靠性与安全性。

### 2. 支持 symlink 的 Agent Markdown 文件
**#28883** | CLOSED | fixes #20079 | [priority/p2, size/m]
[链接](https://github.com/google-gemini/gemini-cli/pull/28883)
修复 `~/.gemini/agents/` 下符号链接文件无法被识别为子代理的问题，方便用户通过链接管理代理配置。

### 3. 修复流式内容导致的循环检测误报
**#28877** | CLOSED | fixes #18551 | [priority/p2, size/s]
[链接](https://github.com/google-gemini/gemini-cli/pull/28877)
流式响应包含连续空格等均匀填充字符时，循环检测服务会误判为死循环；此修复在提交 prompt 后立即出现的均匀内容场景下跳过误报。

### 4. 处理 Cloud Shell 默认项目 404 错误
**#28876** | CLOSED | fixes #18062 | [priority/p2, size/s]
[链接](https://github.com/google-gemini/gemini-cli/pull/28876)
Cloud Shell + Google Cloud Lab 场景下默认项目 `cloudshell-gca` 不存在时返回 404，此修复让 CLI 优雅降级而不是直接失败。

### 5. 修复 OAuth 回调超时导致未处理的 Promise 拒绝
**#28873** | CLOSED | fixes #28512 | [priority/p1, size/s]
[链接](https://github.com/google-gemini/gemini-cli/pull/28873)
认证流程中 OAuth 回调服务器 5 分钟超时后，未捕获的 promise 拒绝会导致进程崩溃，现已在超时路径中正确接住错误。

### 6. ACP 模式：补发 pending 工具调用更新
**#28870** | CLOSED | fixes #21783 | [priority/p1, size/s]
[链接](https://github.com/google-gemini/gemini-cli/pull/28870)
在 ACP 模式下请求用户确认工具权限前，先发送 `tool_call` 会话更新（status 为 `pending`），避免违反协议顺序导致客户端状态错乱。

### 7. 保留显式 Flash 模型 ID
**#28893** | OPEN | fixes #28859 | [priority/p1, size/m]
[链接](https://github.com/google-gemini/gemini-cli/pull/28893)
将 Gemini 3.5 Flash 的滚动重写仅限制在通用 `flash` 别名和已知 rollout ID，保留 `gemini-3.6-flash` 等显式模型 ID，失效 ID 交由 API 返回错误而非静默改写。

### 8. 扩展环境变更需确认并净化运行环境变量
**#28863** | OPEN | [size/m]
[链接](https://github.com/google-gemini/gemini-cli/pull/28863)
修复扩展更新可绕过用户同意、向 MCP 服务器进程注入未授权环境变量的问题——将 MCP 服务器环境配置纳入同意字符串，并净化自定义环境变量。

### 9. Eval 重试逻辑补上 429 限流错误处理
**#28891** | OPEN | fixes #28696 | [priority/p3, size/xl]
[链接](https://github.com/google-gemini/gemini-cli/pull/28891)
`withEvalRetries` 原先对 `RESOURCE_EXHAUSTED`（429）静默穿透，导致评估因限流而非断言失败；现将其纳入重试覆盖范围。

### 10. 修复窄宽度下幽灵文本无限循环
**#28641** | CLOSED

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-08-19

## 今日速览

昨日发布 **v1.0.81-1**，新增 Gemini 3.7 Flash 模型支持和沙箱配置快捷编辑能力，但随之而来的是多起沙箱无法禁用/策略未决时被强制启用的反馈（#4521、#4522）。此外，MCP 相关 Issues 持续霸榜，OAuth 认证回归、进程泄漏等问题仍在发酵，社区对**沙箱控制权**和 **MCP 稳定性**的关注度达到近期高点。

---

## 版本发布

### v1.0.81-1

**新增**
- 支持 Gemini 3.7 Flash 模型
- 在 `/sandbox` 中新增 `Ctrl+E` 快捷键，可直接在编辑器中打开 `settings.json`
- `--usage-output-file` 的 JSON 输出新增 per-agent 使用量指标

**改进**
- 在 Schedule Manager 中，使用 `x` 键移除已排定的 `/every` 和 `/after` 提示

**修复**
- 修复 `allow-all` 关闭时的若干问题
- 其他稳定性修复

发布链接：https://github.com/github/copilot-cli/releases

---

## 社区热点 Issues

以下为过去 24 小时内更新最活跃、社区反响最强烈的 10 个 Issue：

### 1. 组织已启用模型从目录中缺失（Claude Sonnet 5/Opus 5 与 Kimi K3）
**#4390** | 10 评论 | 👍 7 | [链接](https://github.com/github/copilot-cli/issues/4390)

企业用户反馈：组织已在 Copilot Business 中显式启用的 Anthropic 模型（claude-sonnet-5 等）在 CLI 中不可用，选择时报 `This model is disabled by your organization`。**影响面大**，涉及三家主流模型供应商，评论区持续活跃。

### 2. 新版本强制启用沙箱，覆盖用户显式 `sandbox.enabled=false`
**#4522** | 1 评论 | 👍 1 | [链接](https://github.com/github/copilot-cli/issues/4522)

1.0.81-1 中当服务端托管策略暂时未决时，CLI 强制启用本地沙箱——即使用户在配置中显式设置了 `"sandbox": { "enabled": false }`，且设备 MDM 与文件策略中均无沙箱设置。**这是今日最新的高优先级问题**，直接关系到用户对环境控制权的信任。

### 3. 沙箱无法被禁用
**#4521** | 1 评论 | 👍 2 | [链接](https://github.com/github/copilot-cli/issues/4521)

配置显示沙箱已禁用，但运行状态仍显示启用，且执行时实际尝试使用沙箱。与 #4522 相互印证，指向 1.0.81-1 中沙箱策略判断逻辑存在回归。

### 4. Copilot CLI 1.0.42 误报注册表 MCP 服务器被策略阻止
**#3162** | 7 评论 | 👍 1 | [链接](https://github.com/github/copilot-cli/issues/3162)

自定义 MCP 服务器已在官方注册表中且应被允许，但 CLI 仍将其标记为 *blocked by policy*。该问题已存在三个月，尽管状态为 CLOSED，但仍在持续收到开发者讨论，反映 MCP 策略校验逻辑的脆弱。

### 5. 自定义 Agent YAML Frontmatter 应支持推理力度（Reasoning Effort）配置
**#2904** | 7 评论 | 👍 20 | [链接](https://github.com/github/copilot-cli/issues/2904)

当前 `.agent.md` 自定义 Agent 仅能通过 `model` 字段固定模型，无法单独设置推理力度。社区要求为每个 Agent 提供独立的 `--effort` 控制。**获得 20 个 👍，为今日需求类 Issue 中最受关注的一条**。

### 6. 第三方 MCP OAuth Token 未桥接到 CLI 会话
**#4096** | 6 评论 | 👍 2 | [链接](https://github.com/github/copilot-cli/issues/4096)

在 Copilot App 中通过 OAuth 连接 Atlassian Remote MCP 后显示"Connected"，但 CLI 会话中该服务器的工具始终不可用。直指**跨应用认证状态同步**的核心缺陷，已在 1.0.42 之后多个版本中复现。

### 7. Atlassian MCP OAuth 在 1.0.80 中回归
**#4490** | 3 评论 | 👍 0 | [链接](https://github.com/github/copilot-cli/issues/4490)

1.0.80 引入 RFC 8414 §3.3 的 issuer 校验后，Atlassian MCP 认证失败。1.0.78 正常，属于**明确的行为回归**。认证类问题高频出现，社区已表现出一定的疲劳感。

### 8. MCP 服务器连接泄漏：stdio 子进程无限累积
**#3698** | 0 评论 | 👍 3 | [链接](https://github.com/github/copilot-cli/issues/3698)

当 stdio MCP 服务器响应慢或上游不可达时，CLI 生成的子进程既不回收也不终止，重启/重连时重复生成，直至 CPU 占满、系统卡顿。已存在两个多月，与 #4392（认证后重建 MCP 客户端导致孤儿进程）相互关联，**是高频 MCP 痛点背后的根源问题之一**。

### 9. 支持按模式配置默认模型（plan mode vs. autopilot）
**#2958** | 4 评论 | 👍 16 | [链接](https://github.com/github/copilot-cli/issues/2958)

用户希望针对 plan 模式和 autopilot 模式分别配置默认模型。**获得 16 个 👍**，为需求类第二高。在很多工作流中计划与执行使用不同模型的诉求很强烈。

### 10. 支持刷新生效 BYOK Provider 凭据，无需重启 CLI
**#3682** | 2 评论 | 👍 6 | [链接](https://github.com/github/copilot-cli/issues/3682)

BYOK 场景下，CLI 仅在进程启动时读取一次 `COPILOT_PROVIDER_API_KEY` 与自定义 headers。短时凭据（Entra ID、AWS STS、OIDC JWT）过期后必须重启 CLI，生产环境不可接受。企业用户（含微软内部）持续反馈。

---

## 重要 PR 进展

过去 24 小时内仅 1 条 PR 更新：

### #3163 ViewSonic monitor（非功能性 PR）
[链接](https://github.com/github/copilot-cli/pull/3163)

标题与摘要内容均为无关内容（"ViewSonic monitor"），疑似垃圾/误提 PR，创建于三个月前，今日被触碰更新。无实质代码变更，建议社区忽略。

> ⚠️ 说明：Copilot CLI 是 GitHub 官方产品，社区贡献 PR 一直较少，近 24 小时窗口内未出现功能性 PR。上述项目当前节奏以官方闭源迭代为主，外部 PR 的参与度非常有限。

---

## 功能需求趋势

综合当前全部 Issues，社区最关注的五大方向：

### 1. MCP 生态成熟度（占比最高）
- 策略误报（#3162）、OAuth 兼容性（#4490）、进程泄漏（#3698、#4392）、BigInt 序列化（#4211）、`content` 与 `structuredContent` 重复暴露（#4515）等多点开花
- **信号**：MCP 已从"能不能连"进入"连得好不好、稳不稳定、安不安全"阶段

### 2. 沙箱控制权与策略透明度（新增热点）
- 1.0.81-1 的强制启用问题（#4521、#4522）与 JVM 子进程不受 RW 路径授权约束（#4516）表明沙箱功能正在快速迭代，但策略判断与用户显式配置之间的优先级关系需要更清晰

### 3. 新模型支持与模型选择灵活性
- Gemini 3.7 Flash 已随 v1.0.81-1 落地
- 组织级模型不可用（#4390）、按模式配置模型（#2958）、自定义 Agent 推理力度（#2904）等需求热度持续上升
- 用户希望：**谁能用什么模型、什么模式下用什么模型、每个 Agent 用什么力度**，都能自主控制

### 4. Agent / Skill 可配置性
- `disable-model-invocation: true` 导致 skill 完全不可达（#4438）
- 内置 Agent 不继承自定义指令（#1990）
- 独立 hook 文件不被发现（#4520）
- 需求本质：**用户需要完整的、分层的可配置能力**，而不只是配置文件解析

### 5. 会话生命周期管理
- 历史会话滚动浏览（#4313）
- `/rename` 被自动命名覆盖（#2622）
- 会话 AIC 用量显示不准确（#4511）
- 属于日常体验类需求，虽不如前四类热门，但长期存在、反馈稳定

---

## 开发者关注点

**高频痛点与共性诉求：**

| 痛点/需求 | 相关 Issue | 说明 |
|---|---|---|
| **沙箱强制执行引发反弹** | #4521、#4522、#4516 | 1.0.81-1 中用户显式禁用被服务器策略覆盖，JVM 子进程路径授权失效。开发者对"我的配置我说了不算"的反馈十分强烈 |
| **MCP 进程泄漏与孤儿进程** | #3698、#4392 | 长时间使用后系统资源被耗尽，已有开发者报告 CPU 100% 的问题，是当前最严重稳定性问题之一 |
| **认证状态同步与回归** | #4490、#4096 | OAuth 在 App 与 CLI 之间的状态桥接不可靠，且版本间行为不稳定（1.0.78 正常、1.0.80 回归） |
| **组织模型策略不可见** | #4390 | 企业管理员已配置的模型策略未正确映射到 CLI，且错误信息具有误导性（报告"disabled by organization"） |
| **配置生命周期管理** | #3682、#812、#4482 | 凭据/AGENTS.md/permissions-config.json 均存在启动后不重载、不生效的问题，开发者需要完整的配置热更新能力 |
| **使用量计量不透明** | #4511 | Kimi K3 等模型会话语义消耗显示严重低估，影响企业成本追踪 |

**一句话总结：** 社区当前最集中的情绪是——Copilot CLI 的功能迭代速度很快（新模型、新 UI、新沙箱），但稳定性、配置控制权和 MCP 基础设施的可靠性没有跟上，尤其是**沙箱强开**和**MCP 进程泄漏**这两件事，已经成为 1.0.81 系列最受关注的风险点。

---

*日报生成时间：2026-08-19 · 数据来源：[github/github/copilot-cli](https://github.com/github/copilot-cli)*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-08-19）

> 数据来源：github.com/MoonshotAI/kimi-cli  
> 说明：过去 24 小时无新 Release；有 2 个 Issue 和 2 个 PR 更新，以下全部收录分析。

## 今日速览

今日最值得关注的是：社区量化交易博主开源了 **K3 + Kimi Code 的样本外策略生成基准测试报告**（#2608），为 CLI 在专业领域的实战表现提供了外部验证；同时 Web UI 被报告在标签切换/重载后对非 Kimi（OpenAI 兼容）

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-19

## 今日速览

今日社区最集中的动态是 **OpenCode Go 配额/计费不一致** 问题的集中爆发：至少 5 个 Issue 报告配额消耗与账单金额严重不符，且集中在 `deepseek-v4-flash` 模型上。与此同时，**Linear Agent 集成**（👍 34）与 **/resume、/pause 命令**（👍 28）等高赞功能请求持续引发讨论。底层架构方面，`message.updated.1` 序列化开销、消息 ID 回绕等性能与数据一致性问题也受到开发者高度关注。

## 社区热点 Issues

以下是近 24 小时内评论数最多、最受关注的 10 个 Issue：

### 1. Linear Agent 集成（👍 34 / 💬 17）
**#3787** — 社区呼声最高的功能请求之一，参考 Linear 官方 Agents 能力，希望能将 Linear issue 直接分配给 OpenCode Agent 处理，实现从任务追踪到代码执行的闭环。
🔗 https://github.com/anomalyco/opencode/issues/3787

### 2. OpenCode Go 配额消耗异常偏高（👍 7 / 💬 15）
**#42985** — 用户反馈 Go 配额消耗约为 usage 图表显示的 DeepSeek V4 Flash 成本的 **4 倍**。同一天显示消费 $3.31，但配额扣除额远超此数，引发对计量准确性的质疑。
🔗 https://github.com/anomalyco/opencode/issues/42985

### 3. 新增 /resume 与 /pause 命令（👍 28 / 💬 8）
**#7226** — 希望提供显式的暂停/恢复命令，避免目前只能通过 Esc 中断、再手动输入冗长提示词恢复上下文的低效流程。
🔗 https://github.com/anomalyco/opencode/issues/7226

### 4. 阻止 TUI 自动向下滚动（👍 18 / 💬 11）
**#7648** — Agent 流式生成新消息时，TUI 持续滚动导致用户无法阅读当前内容。该议题讨论了较长时间后于近期关闭

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-19

## 今日速览

今日发布 v0.21.11-nightly 版本，新增 live-session registry 及 `qwen sessions ps` 实时会话管理命令，daemon 侧同步推进 skill 切换能力。多智能体协作方向成为社区最热议题，24 小时内新增 3 个相关 bug 报告（#9430、#9431、#9428），且 PR #9433 已快速跟进修复。此外，SWE-bench Verified 与 Terminal-Bench 2.0 端到端基准测试部分结果被 QUARANTINED，质量门禁持续收紧。

## 版本发布

### v0.21.11-nightly.20260818.259951c53e
- **新功能**：新增 live-session registry 及 `qwen sessions ps` 命令，支持查询实时会话列表（PR #8969）
- **daemon 改进**：附加 skill-toggling 能力（详情待完整 changelog）

### 基准验证 Releases（dsw-eas-*）
- `dsw-eas-full-20260818-r3`：全量端到端验证（SWE-bench Verified 500 + Terminal-Bench 2.0 89），结果已回写，状态 **QUARANTINED**
- `dsw-eas-full-20260818-r2`：同上，状态 **QUARANTINED**
- `dsw-eas-tb-smoke-20260818-r2`：凭证刷新端到端冒烟（1 SWE-bench + 1 Terminal-Bench），状态 **SUCCEEDED**（1/1 解决）
- `dsw-eas-tb-smoke-20260818-r1`：临时沙箱恢复冒烟验证

## 社区热点 Issues（10 个）

### 1. [P1] API Error 400 持续 12-16 小时未恢复
**#656** | 更新于 2026-08-18 | 评论 11 | [链接](https://github.com/QwenLM/qwen-code/issues/656)

用户报告所有消息均返回 `InternalError.Algo.InvalidParameter`，持续 12-16 小时，无任何配置变更。作为 P1 级核心 bug，该问题严重影响使用，虽创建时间较早但仍在活跃更新中，说明排查可能涉及服务端算法参数。

### 2. [P2] RFC：独立 Qwen 会话的原生协调机制（已关闭）
**#8718** | 更新于 2026-08-18 | 评论 10 | [链接](https://github.com/QwenLM/qwen-code/issues/8718)

提出 leader 调度多个 worker 会话并采集结构化结果的设计，推动多会话协同从手动方式走向原生支持。虽已关闭，但 10 条评论显示讨论深入，为后续多智能体功能奠基。

### 3. [P2] 可靠的自动记忆召回 — 时机、质量与遥测
**#7040** | 更新于 2026-08-18 | 评论 10 | [链接](https://github.com/QwenLM/qwen-code/issues/7040)

记忆召回功能持续迭代中，已有 1 个 PR 合并（#7393）、2 个在审（#8716）。该 issue 同时跟踪召回精度和多语言评测，是社区对上下文性能关注的核心载体。

### 4. [P2] 团队成员无法向 leader 发送普通消息
**#9276** | 更新于 2026-08-18 | 评论 7 | [链接](https://github.com/QwenLM/qwen-code/issues/9276)

团队成员发送状态消息被误判为 shutdown 请求，报错 `Only the team leader can request shutdowns`。多智能体通信语义存在严重缺陷，直接影响团队协作模式的可用性。

### 5. [P1] Windows 桌面版会话静默自动删除
**#8400** | 更新于 2026-08-18 | 评论 4 | [链接](https://github.com/QwenLM/qwen-code/issues/8400)

Desktop 0.0.5 在 ACP session 加载失败时，因 workspace cwd 不匹配导致消息加载为 0，进而静默删除本地会话镜像。涉及数据丢失，属高危问题。

### 6. [P2] 不支持的图片 MIME 可中断 Responses 兼容会话
**#9291** | 更新于 2026-08-18 | 评论 4 | [链接](https://github.com/QwenLM/qwen-code/issues/9291)

真实 `.heic` 图片被作为 `image/heic` data URI 转发后遭端点拒绝，导致整个会话中止。暴露了附件 MIME 校验缺失，属于输入验证盲区。

### 7. [P3] 命名队友静默忽略 run_in_background: false
**#9430** | 创建于 2026-08-18 | 评论 3 | [链接](https://github.com/QwenLM/qwen-code/issues/9430)

Agent Team 的命名队友接受 `run_in_background: false` 但无效，仍被并发启动且工具立即返回。后台执行语义不透明，易引发资源竞争，该 issue 发布当天即有对应 PR #9433 跟进。

### 8. [P2] /review 发布时收敛建议设计（中文）
**#9278** | 更新于 2026-08-18 | 评论 5 | [链接](https://github.com/QwenLM/qwen-code/issues/9278)

详细记录了 `/review` 命令发布时收敛控制的设计与实测，针对评审-修复失控回路提出遥测、诊断与操作者发布面方案。反映 CI 自动化复杂度的持续攀升。

### 9. 跨会话消息传递：同机 Qwen Code 会话互发消息
**#8724** | 更新于 2026-08-18 | 评论 6 | [链接](https://github.com/QwenLM/qwen-code/issues/8724)

提出用 `list_agents` 发现、`send_message` 定向发送的跨会话通信方案，并要求接收端有 fail-closed 门控。该能力是构建本地多智能体协作网络的基础，社区讨论热度高。

### 10. [P2] 取消 prompt 后内容未恢复到输入框
**#8316** | 更新于 2026-08-18 | 评论 10 | [链接](https://github.com/QwenLM/qwen-code/issues/8316)

Ctrl+C 取消 prompt 后文本丢失，用户需重新输入。交互细节上的高频痛点，10 条评论说明影响面较大，涉及输入状态管理。

## 重要 PR 进展（10 个）

### 1. 修复 output.format "stream-json" 配置 schema 不匹配
**#8966** | [链接](https://github.com/QwenLM/qwen-code/pull/8966)

使配置文件 schema 接受 `stream-json` 格式，与 CLI 运行时行为保持一致。修复配置声明与解析不一致带来的告警或启动失败。

### 2. MAX_TOKENS 输出恢复后记录合并轮次
**#8980** | [链接](https://github.com/QwenLM/qwen-code/pull/8980)

模型输出因 MAX_TOKENS 截断后，恢复

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*