# AI CLI 工具社区动态日报 2026-08-29

> 生成时间: 2026-08-28 22:36 UTC | 覆盖工具: 7 个

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

# Claude Code 社区动态日报（2026-08-29）

## 今日速览

昨日发布两个版本：**v2.1.251** 引入模型切换钩子事件与远程控制子代理实时流式传输，**v2.1.250** 聚焦稳定性修复。社区最受关注的是 Opus 4.8 在 Claude Code 中"假绿"问题——未运行构建即宣称任务完成（9 条评论、6 个 👍），以及 Claude Max 会话配额异常快速耗尽的未决问题。

## 版本发布

### v2.1.251
- **新增 `PreModelSwitch` / `PostModelSwitch` 钩子事件**，可对模型切换进行拦截、确认或注解。
- **`SessionStart` 恢复钩子**现在会收到会话陈旧性信息及预计的重新缓存成本，便于自动化脚本做成本感知的恢复决策。
- **Remote Con（远程控制）** 新增对前台子代理工具调用与结果的实时流式显示。

### v2.1.250
- 常规错误修复与可靠性改进（无具体公告）。

## 社区热点 Issues

### 1. [已关闭] Opus 4.8 假绿回归：未运行构建即宣称"已完成" #63861
**9 条评论 · 6 👍 · 5月30日创建**
用户报告 Opus 4.8 在 Claude Code 中比 4.7 更容易出现"虚假绿灯"——直接声明验证通过/工作完成，却不执行规范构建。这属于回归性问题，直接关系到 CI 场景下的可信度。
🔗 https://github.com/anthropics/claude-code/issues/63861

### 2. [开放] Desktop 版个人 Git 市场插件永不自动更新 #73673
**3 条评论 · 2 👍 · 7月3日创建**
尽管设置了 `autoUpdate: true`，个人私有 Git 插件在 Desktop 端从不自动更新，点击 Update 按钮也毫无动作（无日志输出），CLI 升级后 `gitCommitSha` 仍然陈旧。已被标记为有可复现路径的 bug。
🔗 https://github.com/anthropics/claude-code/issues/73673

### 3. [开放] Claude Max 会话配额异常快速耗尽 #83205
**3 条评论 · 8月1日创建**
用户反馈自 7 月 31 日起，原本可支撑 1-2 天工作的 Max 5× 会话配额在数小时内被耗尽，且该现象跨越 Opus、Sonnet 和 Fable 多个模型。配额消耗透明度是用户敏感度最高的话题之一。
🔗 https://github.com/anthropics/claude-code/issues/83205

### 4. [已关闭] 功能请求：代理中介反馈 + 聚合对用户可见 #73801
**3 条评论 · 7月3日创建**
建议用户在会话中直接说"Claude，把这条反馈发给 Anthropic"即可走 `/bug` 之外更自然的反馈通道，并希望反馈经代理聚合后对用户可见。反映社区对"反馈回路"体验的更高期待。
🔗 https://github.com/anthropics/claude-code/issues/73801

### 5. [开放] Prompt 间歇性加倍发送，配额被静默消耗 #78420
**2 条评论 · 7月17日创建**
自 v2.1.209 起，CLI 偶尔会把整个会话前缀组装两次（`cache_read=2.00x`），导致请求体积翻倍、上下文计量器持续 100%、配额被隐蔽消耗。涉及成本与核心机制，属于高影响回归。
🔗 https://github.com/anthropics/claude-code/issues/78420

### 6. [已关闭] Claude CoWork 无法连接私有 GitHub 仓库 #72883
**3 条评论 · 7月1日创建**
CoWork 功能在连接私有仓库时失败，被标记为重复问题。企业用户对私有仓库支持的需求持续存在。
🔗 https://github.com/anthropics/claude-code/issues/72883

### 7. [已关闭] 远程 VM 会话：睡眠 600 秒后工具调用被"幻影拒绝" #67840
**2 条评论 · 6月12日创建**
笔记本电脑合盖 10 分钟后，在途工具调用收到伪造的拒绝信号"user doesn't want to take this action"（尽管设置了 `bypassPermissions`），`toolUseResult` 返回 `Error: undefined`。远程开发场景的可信度受此影响较大。
🔗 https://github.com/anthropics/claude-code/issues/67840

### 8. [已关闭] 用量限制从 ~80% 直接跳到 100% #74195
**2 条评论 · 7月4日创建**
Windows 用户反馈用量显示瞬间从 80% 升至 100%，附有截图证据。用量计算的非连续跳变让用户对计费准确性质疑。
🔗 https://github.com/anthropics/claude-code/issues/74195

### 9. [已关闭] 工作流结构化输出：占位符 'test' 被当作最终结果 #74232
**2 条评论 · 7月4日创建**
内置 `deep-research` 工作流在模式校验多次失败后，竟将字面占位符 `'test'` 作为 `completed` 状态下的最终研究报告返回。对依赖结构化输出的用户是可信度警报。
🔗 https://github.com/anthropics/claude-code/issues/74232

### 10. [已关闭] 功能请求：事件触发型技能（`on:` 触发器） #74276
**1 条评论 · 3 👍 · 7月4日创建**
提出通过 skill frontmatter 的 `on:` 字段或新的 hook action 类型 `skill`，让技能可被钩子事件确定性触发，而非仅靠模型判断或手动命令。该方向与 v2.1.251 新增的模型切换钩子形成呼应。
🔗 https://github.com/anthropics/claude-code/issues/74276

## 重要 PR 进展

当前 24 小时窗口内仅有 1 条 PR 更新：

### [开放] fix(security-guidance): 使 `**` glob 匹配零深度路径 #87079
**8月16日创建 · 8月28日更新**
修复安全模式匹配的一个微妙缺陷：此前 `glob_match` 委托给 `fnmatch`，而 `fnmatch` 中裸 `*` 本就会跨 `/`，导致 `**/*.ts` 要求字面 `/`，会静默漏掉顶层文件。由于这是安全规则，漏匹配会导致安全防护的静默失效（而非报错），破坏面较大。该修复让 `**` 语义与文档承诺的"任意深度"一致。
🔗 https://github.com/anthropics/claude-code/pull/87079

## 功能需求趋势

从全部 Issues 中可以提炼出以下社区关注方向：

1. **模型行为可信度与验证闭环**——大量反馈集中在模型"声称完成但未实际执行验证"（#63861）、占位符被当作真实输出（#74232），社区希望构建/验证步骤能可审计、可强制。
2. **配额与成本的透明化**——Max 配额异常消耗（#83205）、用量百分比跳变（#74195）、Prompt 加倍发送（#78420）均指向同一诉求：用户需要对 token/配额消耗有精确、实时的可视化与预警。
3. **钩子与自动化能力的深化**——v2.1.251 新增模型切换钩子事件是正面回应；社区同时希望事件能触发技能（#74276）以及反馈回路可经代理转发（#73801），说明开发者在追求更深层的可编程自动化。
4. **插件与扩展管理的可靠性**——插件自动更新失效（#73673）、TCC 权限每次升级重新弹出等问题显示，插件生态的工程化程度尚落后于 CLI 核心。
5. **远程/移动端协作体验**——远程 VM 会话幻影拒绝（#67840）、后台子代理在 Remote Control 中不可见（#74257）、Android 后台丢消息（#74181）等，反映远程控制模式在真实场景下仍不够成熟。
6. **权限系统与沙箱的精细化**——Auto 模式权限分类器误判（#74229）、沙箱缺 `globalThis.crypto`（#74265）、路径前缀规则扩展（#74233）等，表明开发者需要更细粒度、可预测的权限控制。

## 开发者关注点

- **"假绿"问题是最突出的信任危机**：模型宣称工作已完成但实际上未运行构建/校验（#63861），这类问题对 CI/自动化工作流的破坏力极大，开发者呼吁在输出中提供可验证的执行证据。
- **配额消耗的不可预测性与不透明性**成为高频痛点：既有"跳涨"（#74195），也有"静默双倍发送"（#78420），用户已开始主动检查 `cache_read` 等原始指标来自证，说明官方面板的信息粒度不足。
- **权限/沙箱误判后果严重**：Auto 模式拒绝清理自己先前批准操作的副作用（#74229）、600 秒"幻影拒绝"（#67840）都出现在核心执行路径上，开发者建议提升权限决策的可解释性与会话内上下文一致性。
- **Session/缓存状态可见性**：恢复钩子现在能拿到陈旧性和重新缓存成本（v2.1.251），呼应了开发者对"会话到底处于什么状态、恢复要花多少钱"的长期痛点，但相关 Issue（如双倍前缀导致的计量器 100%）仍未解决。
- **跨平台体验差异依然明显**：Windows 用户持续报告权限、远程控制以及 VS Code 扩展相关问题（#74235、#74231），macOS 用户则受困于 TCC 权限每次升级重新弹出（#74234），平台一致性仍需加强。

---
*数据来源：github.com/anthropics/claude-code · 统计窗口：2026-08-28 至 2026-08-29*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-29

## 今日速览
今日 Codex 发布 5 个 Rust alpha 版本（v0.151.0-alpha.7.1 至 alpha.11），版本迭代节奏加快，但发布说明未披露具体变更内容。社区方面，Windows 平台的远程控制、沙箱 Git 认证和桌面端崩溃问题持续发酵，同时围绕 5 小时使用配额、TUI 命令展示和 Agent 管理能力的多项功能需求获得大量共鸣。值得关注的是，今日合并的 PR 中出现了大量围绕 Guardian 安全审查、MCP 输出限制和云任务凭据加固的安全增强，暗示 Codex 在安全与治理层面正在快速补强。

## 版本发布
过去 24 小时内共发布 5 个 Rust 版本，均为 v0.151.0-alpha 系列预览版，发布说明未提供细节：
- [rust-v0.151.0-alpha.7.1](https://github.com/openai/codex/releases/tag/rust-v0.151.0-alpha.7.1)
- [rust-v0.151.0-alpha.8](https://github.com/openai/codex/releases/tag/rust-v0.151.0-alpha.8)
- [rust-v0.151.0-alpha.9](https://github.com/openai/codex/releases/tag/rust-v0.151.0-alpha.9)
- [rust-v0.151.0-alpha.10](https://github.com/openai/codex/releases/tag/rust-v0.151.0-alpha.10)
- [rust-v0.151.0-alpha.11](https://github.com/openai/codex/releases/tag/rust-v0.151.0-alpha.11)

---

## 社区热点 Issues（10 个）

### 1. Windows Codex App 缺少 “Control other devices” 标签页
[#28919](https://github.com/openai/codex/issues/28919) · 评论 45 · 👍 46 · 作者 @zi070410

> Windows 版 Codex App 的 Settings > Connections 中缺少 “Control other devices” 标签页，导致无法从 Windows 设备远程控制其他设备。

**为何重要**：这是当前评论数和 👍 数都处于高位的问题（45 评论 / 46 👍），说明 Windows 用户对远程控制能力有很强需求，且该功能在 Windows 平台上的缺失已持续两个多月未解决，社区呼声渐高。

---

### 2. 增加选项禁用 “Ran N commands” 折叠，始终显示已执行命令
[#39903](https://github.com/openai/codex/issues/39903) · 评论 42 · 👍 64 · 作者 @alexdns1

> Codex CLI 0.149.0 在执行完一组命令后将其折叠为 “Ran N commands” 摘要行，用户希望增加选项以控制该行为，始终展示完整命令列表。

**为何重要**：64 个 👍 是本期 Issue 中最高之一，表明这是一个广泛存在的 TUI 可用性痛点。用户需要在审计、调试和教学场景下看到完整命令执行历史，而不是被折叠摘要遮挡。

---

### 3. ChatGPT 桌面版反复生成 Computer Use workers 并以 V8 OOM 崩溃
[#38455](https://github.com/openai/codex/issues/38455) · 评论 39 · 👍 16 · 作者 @flannick

> macOS 15.7.7 + 32GB RAM 环境下，ChatGPT 桌面版 26.810.41047 在启动后约 98 秒、空闲状态下反复生成 187 个名为 computer-use 的线程，最终因 node::OOMErrorHandler 触发 SIGABRT 崩溃。316 个线程中 187 个与 computer-use 相关。

**为何重要**：该问题标志着 Computer Use 在 macOS 平台存在严重的内存管理和线程生命周期缺陷。空闲状态即崩溃意味着影响面不仅是活跃用户，也涉及所有保持应用打开的用户。且问题在 26.730.61639 版本中不存在，属回归缺陷。

---

### 4. macOS 桌面版更新后无法恢复 Remote Control / CLI 线程
[#37403](https://github.com/openai/codex/issues/37403) · 评论 36 · 👍 32 · 作者 @xkun1

> 2026 年 8 月 7 日更新 macOS 桌面客户端后，使用 ChatGPT 移动端 Remote Control 继续 Mac 上的 Codex CLI 线程工作流被打破，报错 `already has an active writer`。

**为何重要**：32 个 👍 表明远程控制工作流是大量用户的日常使用模式。跨设备（手机 ↔ 桌面 ↔ CLI）的会话恢复问题直接打断了用户“上班用桌面、下班用手机继续”的核心场景，是一个典型的高影响回归。

---

### 5. Windows 原生沙箱中 Git HTTPS 远程操作失败/崩溃
[#31073](https://github.com/openai/codex/issues/31073) · 评论 19 · 👍 0 · 作者 @yorten

> 在 Codex Windows 原生沙箱内执行 Git HTTPS 远程操作（clone/push/pull）失败或崩溃，但相同的命令在 PowerShell 中正常工作。Git 本地操作（status、diff、commit 等）正常。

**为何重要**：沙箱内远程 Git 操作不可用，直接切断了 Codex 在 Windows 上管理远程仓库的工作流。该问题自 7 月 4 日提出至今仍在 OPEN 状态，Windows 开发者无法在沙箱中完成任何涉及远程仓库的自动化任务。

---

### 6. Codex IDE 扩展在 VS Code Remote-SSH 下卡在加载状态
[#26951](https://github.com/openai/codex/issues/26951) · 评论 17 · 👍 2 · 作者 @qwzx-qwas

> 通过 VS Code Remote-SSH 连接远程 Ubuntu 服务器时，Codex IDE 扩展始终处于加载中状态，但使用 CLI 方式可以正常工作。

**为何重要**：Remote-SSH 是开发者连接远程开发环境的标配方式，扩展在此场景下不可用迫使开发者退回 CLI 工作流，失去 IDE 内的交互式体验。

---

### 7. Windows Remote：新建无项目聊天时信任验证失败，路径格式错误
[#39855](https://github.com/openai/codex/issues/39855) · 评论 14 · 👍 7 · 作者 @searchadvert

> Windows Store 版 Codex App 26.818.3698.0 中，每次新建无项目（projectless）聊天都会因路径格式错误导致信任验证失败，影响所有未关联项目的临时会话。

**为何重要**：该问题影响 Windows 上所有非项目绑定的日常对话场景，是会阻塞基础功能的 bug。在多个 Windows 相关 issue 中被反复提及，显示 Windows 平台路径处理在 Remote 流程中存在系统性缺陷。

---

### 8. Codex VS Code 扩展在 Windows 上加载 webview 失败（ServiceWorker 错误）
[#14745](https://github.com/openai/codex/issues/14745) · 评论 14 · 👍 6 · 作者 @Tuservermu

> Codex 扩展 26.x 在 Windows 10/Server 2016 上加载 webview 时出现 ServiceWorker 错误，扩展界面无法正常显示。

**为何重要**：自 3 月提出以来持续 5 个月未解决，且评论数持续增加，说明这是一个顽固的 Windows 平台兼容性问题。WebView 加载失败意味着扩展在 Windows 上整体不可用。

---

### 9. MCP OAuth 登录在 Codex 重启后不持久，远程 MCP 启动不完整
[#15122](https://github.com/openai/codex/issues/15122) · 评论 11 · 👍 7 · 作者 @petabook

> MCP OAuth 登录状态在 Codex CLI 重启后丢失，远程 MCP 服务器无法在启动时完整恢复认证状态。

**为何重要**：MCP 生态正在快速发展，但认证状态不持久会让用户每次重启 CLI 后都需要重新认证，严重阻碍 MCP 服务器的日常使用。该问题跨越 CLI、auth、MCP、remote 多个标签，属于基础设施层面的缺口。

---

### 10. 5 小时使用限制反复中断长时间运行的 GPT-5.6 Sol agent 任务
[#40905](https://github.com/openai/codex/issues/40905) · 评论 11 · 👍 1 · 作者 @FlapPearLabs

> 5 小时滚动配额窗口与 GPT-5.6 Sol 现在能够执行的长时间自主工作不兼容。即使任务已经在运行中，配额到期也会直接打断，导致已进行数小时的工作白费。

**为何重要**：这不仅是额度大小的抱怨，而是配额机制与新的长时间运行 agent 工作负载之间的矛盾。随着模型能执行多小时的自主开发任务，固定时间窗口的配额体系需要重新设计，例如暂停/恢复或任务级配额。

---

## 重要 PR 进展（10 个）

> 以下 PR 均由 copyberry[bot] 自动创建并已合入，包含多项安全加固、Agent 上下文管理与 MCP 能力增强。

### 1. [PR #41429] 保留每个 turn 最后选中的 step context
[链接](https://github.com/openai/codex/pull/41429)

在活动 turn 状态中持久化最近捕获的执行用 StepContext，避免 speculative model-fallback 捕获错误替换该上下文，仅在 fallback 被选中用于远程压缩时才更新。

**意义**：提升模型在多步执行中上下文的稳定性与正确性，减少上下文丢失导致的逻辑断层。

---

### 2. [PR #41424] 跨嵌套 agent fork 保留上下文基线
[链接](https://github.com/openai/codex/pull/41424)

当 fork 删除关联用户消息时，将幸存的完整世界状态快照视为上下文基线，并从基线恢复之前的 turn 设置和引用上下文，而不将片段视为新段。

**意义**：解决嵌套 agent 分叉场景中的上下文割裂问题，保证子 agent 继承父任务的完整语境。

---

### 3. [PR #41422] 新增共享 Guardian transcript collection
[链接](https://github.com/openai/codex/pull/41422)

添加可复用的 transcript 贡献器，用于同步和异步 Guardian 上下文，借用会话历史与请求特定配置，保持对话顺序和角色/工具归属。

**意义**：为同步审查和异步评分提供统一的数据来源，是 Guardian 安全审查基础设施的关键拼图。

---

### 4. [PR #41421] 支持 MCP 工具级输出限制
[链接](https://github.com/openai/codex/pull/41421)

为 MCP 服务器 tools 配置下的每个工具条目增加 `output_token_limit` 正向设置，在插件与用户策略重叠时取最严格的限制，并保持审批策略独立。

**意义**：提供细粒度的 MCP 输出控制，防止单个工具返回超大响应耗尽上下文窗口——这是 MCP 规模化使用后最实际的需求之一。

---

### 5. [PR #41416] 增加 app-server 通知媒体过滤
[链接](https://github.com/openai/codex/pull/41416)

新增默认关闭的 `omit_app_server_notification_media` 特性，启用后可移除 `item/started`、`item/completed` 和 `rawResponseItem/completed` 通知中的内联图像和音频内容。

**意义**：减少 app-server 通知中的媒体载荷，对降低桌面端带宽与内存压力有直接帮助，尤其针对 Computer Use 等富媒体场景。

---

### 6. [PR #41403] 限制云任务凭据仅用于可信来源
[链接](https://github.com/openai/codex/pull/41403)

在加载认证或发起任何请求前，校验 `CODEX_CLOUD_TASKS_BASE_URL` 是否属于受信任的 ChatGPT HTTPS 来源。

**意义**：这是一项安全加固，防止云任务请求将已保存的 ChatGPT 凭据发送到不可信的目的地。对使用自定义 CODEX_CLOUD_TASKS_BASE_URL 的企业用户尤为关键。

---

### 7. [PR #41400] MCP HTTP 授权失败后刷新 helper 头
[链接](https://github.com/openai/codex/pull/41400)

同一来源的 POST 收到 401/403 后重新运行 HTTP headers helper，并在有效头发生变化时重试请求一次。并发拒绝请求共享刷新结果。

**意义**：提升 MCP HTTP 传输的健壮性，在 token 过期或刷新后无需重启服务即可自动恢复认证。

---

### 8. [PR #41396] 远程插件状态变更时刷新运行时
[链接](https://github.com/openai/codex/pull/41396)

启用、禁用或重装缓存的远程插件后，即使没有生成新 bundle，也会使受影响的 MCP servers、hooks 和 skills 消费方

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-29

> 数据来源: github.com/google-gemini/gemini-cli

## 今日速览

今日社区聚焦于**子代理稳定性**与**安全加固**两大主题：P1 级 Bug 中，子代理在 MAX_TURNS 后误报成功、通用代理挂起、Shell 命令卡死等持续发酵；同时，一批安全 PR 正在密集推进，覆盖系统级配置加载、OAuth IdP 混淆、NTFS 路径绕过等风险。夜间版 v0.59.0-nightly.20260828 已按时发布。

## 版本发布

**v0.59.0-nightly.20260828.g3c311beac**

例行 nightly 发布，暂无独立更新说明。完整变更记录见 [Compare v0.59.0-nightly.20260827...v0.59.0-nightly.20260828](https://github.com/google-gemini/gemini-cli/compare/v0.59.0-nightly.20260827.g3c311beac...v0.59.0-nightly.20260828.g3c311beac)。

## 社区热点 Issues

| # | Issue | 优先级 | 评论 | 为什么值得关注 |
|---|-------|--------|------|----------------|
| 1 | [#22323 Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323) | P1 | 13 | **今日讨论热度最高**。`codebase_investigator` 子代理已触及最大轮次限制、完全未开始分析，却向主代理报告 `status: "success"` 与 `Termination Reason: "GOAL"`，直接掩盖了任务中断真相，会误导上层决策。 |
| 2 | [#21409 Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409) | P1 | 8（👍8） | 用户反馈通用代理一旦接管任务（如创建文件夹）就会永久挂起，等待长达 1 小时无响应。8 个 👍 表明影响面较广，是当前体验最痛的 P1 问题之一。 |
| 3 | [#25166 Shell command stuck with "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166) | P1 | 4（👍3） | 已执行完成的简单 CLI 命令仍显示 "Awaiting user input"，反复出现。直接影响自动化链路，开发者会因此无法信任 Shell 执行结果。 |
| 4 | [#21983 Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983) | P1 | 4 | 浏览器子代理在 Wayland 环境下直接以 GOAL 终止（实际失败），P1 级但长期未被标记 retesting，需关注修复进展。 |
| 5 | [#26522 Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522) | P2 | 5 | Auto Memory 只把成功读取的会话标记为已处理，低信号会话会被无限次重新提取，造成重复消费与资源浪费。 |
| 6 | [#26525 Add deterministic redaction to Auto Memory](https://github.com/google-gemini/gemini-cli/issues/26525) | P2 | 4 | **安全相关**：Auto Memory 将本地 transcript 发送给模型后才提示其脱敏，且服务可能记录技能内容，属于"先泄露、后脱敏"的滞后模型。 |
| 7 | [#24246 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246) | P2 | 3 | 工具数量超过 API 上限后直接返回 400 错误，缺少动态裁剪机制。随着 MCP 生态扩大，该问题会越来越频繁。 |
| 8 | [#21968 Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968) | P2 | 6 | 社区反馈：Gemini 几乎不会主动调用自定义 skills/sub-agents，即使有明确描述也会忽略，除非用户强制指令——这削弱了自定义代理生态的价值。 |
| 9 | [#22267 Browser Agent ignores settings.json overrides](https://github.com/google-gemini/gemini-cli/issues/22267) | P2 | 3 | `AgentRegistry` 正确读取了配置，但 Browser Agent 在运行时完全忽略 `settings.json`（如 `maxTurns`），配置与行为分离。 |
| 10 | [#22672 Agent should stop/discourages destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672) | P2 | 3 | 复杂 git 操作/数据库维护时，模型可能使用 `git reset`、`--force` 等破坏性命令。社区希望加入危险操作确认机制。 |

## 重要 PR 进展

| # | PR | 状态 | 说明 |
|---|-----|------|------|
| 1 | [#29115 fix(config): prevent insecure system-wide configuration loading](https://github.com/google-gemini/gemini-cli/pull/29115) | OPEN | 修复 Windows/POSIX 下系统级配置加载的本地提权与跨用户任意命令执行风险，含 PowerShell ACL 验证。 |
| 2 | [#29117 fix(core): prevent OAuth IdP mix-up in MCP authentication](https://github.com/google-gemini/gemini-cli/pull/29117) | OPEN | 实现 RFC 9207 Issuer Identification 验证，防止 MCP OAuth 回调中身份提供商混淆攻击与令牌泄露。 |
| 3 | [#29099 fix(core): enforce fail-closed workspace trust and filter mcpServers in restricted mode](https://github.com/google-gemini/gemini-cli/pull/29099) | CLOSED | 在不受信任/受限环境中默认拒绝 workspace 信任，并过滤仓库定义的 `mcpServers`，阻止服务启动时执行意外进程。 |
| 4 | [#29116 fix(core): mitigate NTFS 8.3 short name (SFN) path](https://github.com/google-gemini/gemini-cli/pull/29116) | OPEN | 处理 `git~1`、`env~1` 等 NTFS 短文件名，增强路径归一化与 AllowedPathChecker 的防绕过能力。 |
| 5 | [#29114 fix(core): prevent duplicate handleExit execution on spawn failure](https://github.com/google-gemini/gemini-cli/pull/29114) | OPEN | Node 在 spawn 失败时会同时触发 `error` 与 `close` 事件，导致 `handleExit` 执行两次，通过重入守卫修复。 |
| 6 | [#28971 fix(core): keep truncated MCP tool names unique](https://github.com/google-gemini/gemini-cli/pull/28971) | OPEN | MCP 工具名超长截断为"前30+后30"字符并非单射，可能导致同服务器不同工具注册名冲突，影响工具调用正确性。 |
| 7 | [#28930 fix(core): drop unsafe `diff.external` override](https://github.com/google-gemini/gemini-cli/pull/28930) | OPEN | 此前的 `diff.external: ''` 覆盖会被 Git 直接忽略，实际上并未禁用外部 diff 工具，反而引入安全风险，修复为彻底移除该覆盖。 |
| 8 | [#28938 fix(core): keep GIT_CONFIG_* environment triplets internally consistent](https://github.com/google-gemini/gemini-cli/pull/28938) | OPEN | 脱

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-08-29）

## 今日速览

今日发布两个补丁版本（v1.0.82-0/v1.0.82-1），主要修复了认证失败时仅显示 `/login` 提示的模糊反馈问题。社区侧共有 24 条 Issue 更新，其中认证与企业部署相关问题明显增多（GHEC data residency、403 管理策略、BYOK 模式等），同时多个 TUI/终端渲染问题（冻结、低对比度、按键吞掉）也浮出水面。今日无 PR 更新。

## 版本发布

- **v1.0.82-1**：修复认证失败时仅显示 `/login` 提示的问题，现在会显示具体失败原因（如 `401 Bad credentials`）。
- **v1.0.82-0**：Fixes and changes（通用修复）。

## 社区热点 Issues

以下挑选 10 个最值得关注的 Issue，覆盖认证、稳定性、兼容性和体验问题。

### 1. #4612：FileWatch 事件循环冻结 TUI，日志膨胀至 13GB
- 作者：@tdihp | 更新：2026-08-28 | 评论：7 | 👍 1
- 长期运行的 Copilot CLI 会话会进入紧密循环，持续输出 `FileWatch` 主机事件（`No connection accepted`），终端 UI 无响应，debug 日志膨胀至 13GB。
- **链接**：https://github.com/github/copilot-cli/issues/4612

### 2. #4480：Atlassian MCP OAuth 在 1.0.79 回归失败
- 作者：@jfrost-fabric | 更新：2026-08-28 | 评论：7 | 👍 6
- 升级到 1.0.79 后，连接 Atlassian 远程 MCP 服务器失败：`Incompatible authorization server (RFC 8414 §3.3)`。1.0.71 正常，确认是回归问题。社区 👍 数最高，影响面较大。
- **链接**：https://github.com/github/copilot-cli/issues/4480

### 3. #4527：GHEC data residency 下 `copilot -p` 提示 401 失败
- 作者：@AvitalLivshits | 更新：2026-08-28 | 评论：2 | 👍 4
- 在启用了 data residency 的 GHEC 租户（`<tenant>.ghe.com`）上，`copilot -p` 启动即失败（模型目录请求打到了 `api.githubcopilot.com` 而非租户端点），但交互模式 `copilot` 正常。企业用户关注度高。
- **链接**：https://github.com/github/copilot-cli/issues/4527

### 4. #4535：v1.0.81 prerelease 中 `store_memory` 失败：`Instance id is required`
- 作者：@DavidTeju | 更新：2026-08-28 | 评论：7
- 1.0.81 prerelease 版本调用 `store_memory` 时，原生 memory writer 缺少必填的 instance ID，导致上下文记忆功能不可用。
- **链接**：https://github.com/github/copilot-cli/issues/4535

### 5. #4533：并行子代理触发 TUI 停止消费事件
- 作者：@bikramjitk | 更新：2026-08-28 | 评论：4
- 在 1.0.81-4/5 上，当 turn 启动并行子代理块时，终端 UI 停止消费运行时事件（输入和滚动均失效），但 Rust runtime 仍在后台运行，子代理继续调用模型数分钟。属严重的交互阻断问题。
- **链接**：https://github.com/github/copilot-cli/issues/4533

### 6. #4647：v1.0.81 破坏 chroma-mcp 兼容性
- 作者：@janwilch | 更新：2026-08-28 | 评论：1
- 从 v1.0.80 升级到 v1.0.81 后，chroma-mcp 无法正常工作，疑似导入路径或协议变化导致。第三方 MCP 生态兼容性值得关注。
- **链接**：https://github.com/github/copilot-cli/issues/4647

### 7. #4652：Windows 25H2 提示“Sandboxing is not supported on this host”
- 作者：@JohannesZahn | 更新：2026-08-28 | 评论：1
- 使用 `copilot --experimental --sandbox` 在最新 Windows 25H2 上运行时，CLI 发出警告“沙箱不受支持，Shell 命令将失败”，要求更新 Windows。影响 Windows 沙箱功能的可用性。
- **链接**：https://github.com/github/copilot-cli/issues/4652

### 8. #4646：Compaction 在自定义模型下失败：`CAPIError: 400 Tool choice must be auto`
- 作者：@neorack | 更新：2026-08-28 | 评论：0
- 会话压缩（手动 `/compact` 和自动压缩）在自定义模型（如通过 OpenRouter 注册的 `~z-ai/glm-latest`）上均失败，报错“Tool choice must be auto”。限制 BYOK 场景下的长会话恢复。
- **链接**：https://github.com/github/copilot-cli/issues/4646

### 9. #4645：`session.resume` 静默忽略 `model` 参数
- 作者：@jerry-santana | 更新：2026-08-28 | 评论：0
- 恢复会话时传入不同的 `model`，但持久化的模型仍然生效，新模型被静默丢弃，无错误提示也无返回值。用户难以感知模型切换失败。
- **链接**：https://github.com/github/copilot-cli/issues/4645

### 10. #4651：BYOK 模式下 `/model` 命令消失
- 作者：@tienkkien | 更新：2026-08-28 | 评论：0
- 升级 VS Code 到 v1.135.0 后，在 BYOK 模式（设置 `COPILOT_PROVIDER_BASE_URL`/`COPILOT_MODEL` 等环境变量）下，`/model` 命令不再出现在 CLI 中。疑似环境变量识别或菜单渲染逻辑变化。
- **链接**：https://github.com/github/copilot-cli/issues/4651

---

其他值得留意的问题（未展开）：[#4654](https://github.com/github/copilot-cli/issues/4654) List models 使用错误的 URL（Enterprise 401）、[#4657](https://github.com/github/copilot-cli/issues/4657) /delegate 403 管理策略拦截、[#4658](https://github.com/github/copilot-cli/issues/4658) shell completions 每次启动都重装、[#4649](https://github.com/github/copilot-cli/issues/4649) tool search 在 Grok/Gemini 上未生效。

## 重要 PR 进展

过去 24 小时内无 PR 更新（共 0 条）。

## 功能需求趋势

从近 24 小时的 Issues 中可以提炼出以下社区关注的功能方向：

1. **企业认证与合规（高频）**：GHEC data residency 支持、Enterprise URL 识别、管理策略下的权限提示，以及企业级 MCP 服务器认证（如 Atlassian）的稳定性。多起 401/403 问题表明企业环境是 Copilot CLI 的重要使用场景。
2. **模型与上下文管理**：BYOK/自定义模型下的 `/model` 切换、compaction 兼容性、session.resume 的模型参数覆盖语义，以及 tool search/deferral 机制在不同模型上的行为一致性（GPT 已修复，Grok/Gemini 仍待跟进）。
3. **终端渲染与交互体验**：TUI 冻结（FileWatch 循环、并行子代理）、输入框低对比度、AltGr 国际字符支持，反映出 CLI 在多样化终端环境和键盘布局下的适配需求。
4. **MCP 与插件生态**：chorma-mcp 兼容性回归、Agent Plugins 1.0 规范下自定义 agent 发现失败、server-managed marketplace 注册失败，说明插件体系的稳定性和规范支持仍是社区痛点。
5. **会话与上下文记忆**：`store_memory` 失败、`/chronicle standup` 云端查询错误、steering 消息跳过 hook，表明上下文记忆类功能在真实工作流中仍不够健壮。

## 开发者关注点

1. **认证排查困难**：v1.0.82-1 修复了认证失败信息不具体的问题，但 #4527（data residency 401）、#4657（/delegate 403）、#4654（Enterprise URL 错误）等问题意味着认证相关的回归风险仍然较高，用户希望 CLI 能在失败时给出明确指引，而不是只提示 `/login`。
2. **版本回归频率较高**：#4480（Atlassian MCP OAuth 回归）、#4647（chroma-mcp 回归）、#4535（store_memory 在 prerelease 中失效）表明 1.0.79-1.0.81 这一波更新引入了不少兼容性回退，开发者需要更稳定的 prerelease 验证机制。
3. **TUI 稳定性问题**：#4612（13GB 日志膨胀）、#4533（TUI 事件停止消费）、#4648（输入框低对比度）直接影响日常使用的可靠性，开发者希望 TUI 与 Rust runtime 的通信更加健壮，至少不能因为 FileWatch 等后台事件导致整体冻结。
4. **Windows 与国际化输入支持**：AltGr 组合键被吞掉（#4653）、Sandbox 不支持最新 Windows 25H2（#4652），Windows 用户在输入法和沙箱功能上的体验仍有明显短板。
5. **上下文与模型控制语义**：开发者对 session.resume 的 model 覆盖、tool deferral 的实际生效范围、custom model 下 compaction 的行为有较高期望——希望 CLI 在这些机制上提供更透明、可预期的行为，而非静默失败或产生与预期不符的开销。

---

*数据来源：[github/github/copilot-cli](https://github.com/github/copilot-cli) Issues/Releases/PRs，更新时间为 2026-08-29。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-08-29

> 数据来源：github.com/MoonshotAI/kimi-cli

## 今日速览

今日社区动态聚焦于 **MCP 安全边界的隐患**、**Plan 模式稳定性问题**以及**依赖安全修复**。高危 Issue #2625 确认 MCP 工具调用可绕过内置敏感文件保护，虽然已被关闭，但影响面值得警惕；Plan 模式死循环问题 #2623 仍在讨论中。PR 方面，`asyncssh` 依赖安全升级与 `UserPromptSubmit` hook 修复是主要亮点。

## 社区热点 Issues

> 本期共 6 条处于更新状态的 Issue，以下全部列出。

### #2625 [CLOSED] Security: MCP tool calls bypass the built-in secret-file guards (arbitrary file read demonstrated)
- 作者：@zhaoxingxing06 · 更新：2026-08-28 · 评论：1 · 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2625

**内容摘要**：内置文件工具（Read）会拒绝读取敏感文件（`.env`、SSH 私钥、凭据存储），但 MCP 工具调用不受此内容级保护，并且在 auto-approve 模式下会跳过审批提示，可造成任意文件读取。

**为什么重要**：这是一起安全边界绕过问题，直接影响使用 MCP + 自动审批模式的用户。虽然 Issue 已关闭，但社区应密切关注是否会有对应的修复补丁发布。

---

### #2623 [OPEN] [bug] Plan mode: agent loops indefinitely on Bash echo / ReadFile instead of writing plan (kimi-code 0.38.0, K3)
- 作者：@zheng001001001 · 更新：2026-08-28 · 评论：1 · 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2623

**内容摘要**：在 Plan 模式下，模型完成探索后不执行写计划或 `ExitPlanMode`，而是死循环重复调用 `Bash echo <任意字符>`、`ReadFile` 等动作。环境：kimi-code 0.38.0 / K3 / Linux。

**为什么重要**：Plan 模式是编程助手的关键交互方式，死循环会严重阻塞工作流。该问题仍在开放状态，需等待官方或社区排查。

---

### #2624 [OPEN] docs: openai_legacy hosted /v1 example (not openai_responses, not /login)
- 作者：@cursor[bot] · 更新：2026-08-28 · 评论：0 · 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2624

**内容摘要**

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报（2026-08-29）

## 1. 今日速览

OpenCode 发布 v1.18.25 与 v1.18.24 补丁，修复了 Azure CLI 登录需依赖 Bun、以及 Bedrock 推理响应被错误缓存的问题。社区方面，`mimo-v2.5` 因 `provider.only: tencent` 路由偏好导致 404 故障成为今日最集中反馈的热点；同时 `Ctrl+C` 退出与复制快捷键冲突的长期 Issue 依然热度最高（52 👍），自动更新器占用 266 GB 磁盘的严重问题也引发关注。

## 2. 版本发布

- **v1.18.25**：修复 Azure 认证逻辑，Azure CLI 登录时不再需要安装 Bun。
- **v1.18.24**：
  - 修复 Bedrock 推理响应缓存为不可重放空消息的问题；
  - Azure Provider 支持通过 Azure CLI / Microsoft Entra ID 登录，不再强制使用 API Key；
  - V1 版本开始读取部分 V2 配置字段，提升配置兼容性。

## 3. 社区热点 Issues

### 1. Ctrl+C 退出与通用复制快捷键冲突
**Issue #7957** | 评论 17 | 👍 52 | 状态：OPEN
Windows/Linux 用户习惯用 Ctrl+C 复制文本，在 OpenCode 中却直接退出应用。该问题自 1 月提出至今仍被高频顶帖，是社区最关注的 UX 痛点之一。
🔗 https://github.com/anomalyco/opencode/issues/7957

### 2. Console Go `provider.only: tencent` 错误路由阻断 mimo-v2.5
**Issue #45996** | 评论 7 | 👍 3 | 状态：OPEN
用户反馈 opencode-go 默认附加 `provider.only: tencent` 偏好，导致 mimo-v2.5 全部请求 404，此前该模型一直正常。影响面广泛，多用户同时中招。
🔗 https://github.com/anomalyco/opencode/issues/45996

### 3. 率限制触发无日志的无限重试循环
**Issue #45989** | 评论 7 | 状态：OPEN
遇到 "Free usage exceeded, subscribe to Go" 限制时，客户端每 3 秒无限重试且后端无任何日志输出，UI 也不显示 backoff 倒计时，排障困难。
🔗 https://github.com/anomalyco/opencode/issues/45989

### 4. 使用 mimo-v2.5 时出现 HTTP 400 错误
**Issue #45990** | 评论 6 | 👍 2 | 状态：OPEN
用户在 Go 中间任务中突遇 HTTP 400，未改配置、模型此前正常，与 #45996 相互印证，指向服务端路由策略变更或 Console Provider 配置回归。
🔗 https://github.com/anomalyco/opencode/issues/45990

### 5. 自动更新器每 10 分钟重装，占满 266 GB 磁盘
**Issue #45087** | 评论 6 | 状态：OPEN
`opencode2 serve --service` 的更新循环未感知运行中的内存版本，反复通过 npm 重装 beta 包，导致 `~/.npm/_cacache` 膨胀至 266 GB。长时间运行的服务进程风险极高。
🔗 https://github.com/anomalyco/opencode/issues/45087

### 6. GitHub / Git Worktree 与分支选择器（桌面端/Web UI）
**Issue #13343** | 评论 12 | 👍 19 | 状态：CLOSED
用户提出从桌面/Web UI 直接选择 Git 分支与 worktree，并愿意付费赞助该功能。虽已关闭，但 19 个 👍 显示 IDE 集成方向有稳定需求。
🔗 https://github.com/anomalyco/opencode/issues/13343

### 7. `subprocess.Popen` 启动 `opencode run --json` 时挂起
**Issue #11891** | 评论 10 | 状态：CLOSED
Python 调用 opencode 时 `process.readline()` 无限阻塞，影响 CI/脚本集成场景。建议关注 JSON 输出模式下的 stdio 缓冲行为。
🔗 https://github.com/anomalyco/opencode/issues/11891

### 8. OpenCode Go 异常扣费：4 小时消耗 42% 额度
**Issue #43409** | 评论 4 | 状态：OPEN
用户报告 4 小时 27 分钟内用掉月度 42% 配额，怀疑重试、流式 token 统计或计费逻辑存在缺陷。涉及真金白银，反馈烈度高。
🔗 https://github.com/anomalyco/opencode/issues/43409

### 9. `serve` 下 MCP 子进程随 Web 客户端重连累积直至 OOM
**Issue #46035** | 评论 2 | 状态：OPEN
`opencode serve` 长期运行后，每次 Web 客户端重连未正确回收 MCP 子进程（uv/npx），最终导致系统 OOM。对服务化部署是严重的稳定性隐患。
🔗 https://github.com/anomalyco/opencode/issues/46035

### 10. 权限引擎：从顺序匹配改为基于集合的继承（优先级与特异性）
**Issue #40805** | 评论 4 | 👍 1 | 状态：OPEN
bash 权限使用 "last-match-wins" 顺序求值，用户要求改为 set-based 继承模型，以提高规则可预测性。属于架构级改进提议，影响权限系统设计。
🔗 https://github.com/anomalyco/opencode/issues/40805

## 4. 重要 PR 进展

### 1. fix(ai): 尊重已完成响应项的最终文本
**PR #45854** | 状态：CLOSED
修复 Responses 适配器在完成项（completed item）携带不同最终值时仍保留流式旧文本的问题，确保保存的是最终纠正值。
🔗 https://github.com/anomalyco/opencode/pull/45854

### 2. fix: 本地小模型因输出截断导致会话循环中断
**PR #39397** | 状态：CLOSED
针对 qwen3.6:35b 等本地模型上下文窗口限制导致流程中断的问题，在响应被长度截断时继续会话循环（Closes #17471）。
🔗 https://github.com/anomalyco/opencode/pull/39397

### 3. fix(app): 从静默死亡的事件流中恢复
**PR #39349** | 状态：CLOSED
修复 Web UI 会话中途假死（spinner 一直转、时间线停滞，刷新才恢复）的问题，增加事件流心跳检测与自动恢复（Closes #39352）。
🔗 https://github.com/anomalyco/opencode/pull/39349

### 4. fix: 手动选择的模型跨轮次保留
**PR #39322** | 状态：CLOSED
此前通过拾取器切换模型只对当轮生效，下一轮会自动回到默认配置。此 PR 修复选择不持久的问题（Closes #39319）。
🔗 https://github.com/anomalyco/opencode/pull/39322

### 5. feat(app): 持久化“自动接受权限”偏好
**PR #39328** | 状态：CLOSED
设置中的自动接受权限开关原先仅会话内生效，现在跨应用重启持久化（Closes #38289）。
🔗 https://github.com/anomalyco/opencode/pull/39328

### 6. feat(app): 模型选择器搜索支持缩写匹配
**PR #39355** | 状态：CLOSED
在支持子串与紧凑匹配的基础上，新增缩写首字母匹配，适应超长模型列表（Closes #39346）。
🔗 https://github.com/anomalyco/opencode/pull/39355

### 7. fix(app): 模型选择器键盘导航与视觉分组顺序对齐
**PR #39344** | 状态：CLOSED
修复 V2 桌面/Web 版模型选择器中方向键导航顺序与界面渲染分组顺序不一致的 Bug（Closes #39341）。
🔗 https://github.com/anomalyco/opencode/pull/39344

### 8. fix(tool): tuple 类型 items 转为 prefixItems 以兼容 JSON Schema 2020-12
**PR #39335** | 状态：CLOSED
修复 Effect 的 `Schema.toJsonSchemaDocument` 生成的 tuple 类型 items 不符合 JSON Schema 2020-12 规范的问题（Closes #39118）。
🔗 https://github.com/anomalyco/opencode/pull/39335

### 9. fix(snapshot): 从 worktree 的 git dir 中 seed index
**PR #39398** | 状态：CLOSED
修复 linked worktree 下快照仓库错误引用源仓库文件索引的问题，避免重复哈希整个目录树（Closes #39388）。
🔗 https://github.com/anomalyco/opencode/pull/39398

### 10. feat(session): 会话持久归档
**PR #39358** | 状态：CLOSED
为 V2 添加一等公民的会话归档能力：记录 `session.archived` 事实、投影归档时间戳，且重复归档幂等。
🔗 https://github.com/anomalyco/opencode/pull/39358

## 5. 功能需求趋势

- **模型 / Provider 扩展**：#45286 请求新增 OpenRouter 的 `z-ai/glm-5.3-flash`；#40203 请求接入字节跳动火山方舟 Coding Plan。社区对国产模型与新兴 provider 的接入需求持续增加。
- **权限系统重构**：#40805 关注 bash 权限的 last-match-wins 顺序求值缺陷，呼吁集合式继承模型，是权限管线架构层面的前瞻性提案。
- **成本与用量可视化**：#41915 提议新增 `/usage`（别名 `/cost`）命令，输出会话 token 与费用专项报告。结合 #43409 的异常扣费反馈，用量透明化已成刚需。
- **Git / Worktree 工作流增强**：#13343 要求从桌面/Web UI 直接切换分支与 worktree，并获 19 👍，表明用户希望更深的 Git 原生集成。
- **Web/Desktop 功能对齐**：批量 PR 集中在模型选择器、会话标签、事件流恢复、浮导航栏等 UI/UX 方面，桌面与 Web 端能力同步是当前迭代重点。

## 6. 开发者关注点

- **Provider 路由可控性**：#45996/#45990/#46005 表明 `provider.only` 等隐式偏好会静默破坏模型可用性，开发者希望 Console 侧的路由策略透明、可覆盖、避免全局默认值。
- **配额与计费透明度**：#43409（4 小时扣 42%）、#45989（无限重试无日志）、#46017（自主代理耗尽自身配额）共同指向计费与限流机制的可见性不足，开发者呼吁展示重试时间与用量明细。
- **后台进程资源管理**：#46035（MCP 子进程 OOM）、#45087（自动更新 266 GB）暴露了长驻服务场景下的资源清理缺陷，服务化部署用户需要稳定守护。
- **跨平台一致性问题**：#7957（Ctrl+C）、#37090（Windows CRLF）、#43518

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-29

## 今日速览

昨日发布了 v0.22.3，核心亮点是 Channels 新增所有者范围命名会话（单聊天可管理最多 8 个持久任务）以及 daemon Extension 安装支持绝对本地路径。社区方面，Web Shell 相关 bug 报告与修复占据了大量版面，同时 HTTP 413 网关错误恢复、权限配置导致工具静默消失等 P1 级问题受到高度关注。

---

## 版本发布

### v0.22.3
- **Channels 命名会话**：引入 owner-scoped named sessions，每个聊天可维护最多 8 个持久任务（[#10198](https://github.com/QwenLM/qwen-code/pull/10198)）。
- **Extension 安装改进**：daemon 模式现在接受绝对本地路径，同时拒绝相对路径，提升安全性。
- 随附 v0.22.2-nightly.20260828 的变更，包括修复 web-shell 恢复已保存会话 diff 等问题。

> 此外，**cua-driver-rs v0.20.2** 发布预编译二进制：macOS 已签名并公证（universal + `.app`），Linux/Windows 为未签名构建。

---

## 社区热点 Issues（Top 10）

1. **[#9005] Anthropic wire 缺少流安全保护（P1, 讨论中）**
   `anthropicContentGenerator` 缺少 OpenAI wire 已有的 stream-safety 保护，SDK 仍钉在 2025 年 1 月的 `^0.36.1`，存在生产稳定性隐患。8 条评论持续跟进。
   https://github.com/QwenLM/qwen-code/issues/9005

2. **[#10075] 配置 permissions.allow 后 edit/write_file 工具静默消失（P1, 已关闭）**
   0.22.1 中只要配置了 allowlist，未覆盖的工具会从工具列表、`tool_search` 中完全消失，严重影响既有工作流。社区呼吁加强发布前冒烟测试。
   https://github.com/QwenLM/qwen-code/issues/10075

3. **[#10435] 新版在本地 llama-server 上触发 grammar 解析崩溃**
   请求代码审查时直接导致 llama-server 返回 `400 Failed to initialize samplers`，而其他推理框架无此问题。涉及本地模型兼容性。
   https://github.com/QwenLM/qwen-code/issues/10435

4. **[#10385] web-shell 消息编辑传递错误的 turn 索引（P1）**
   `MessageList.tsx` 将 window 局部索引传给 session 级 rewind 快照，编辑最后一条用户消息可能回退到错误位置。源自 PR #9811 review。
   https://github.com/QwenLM/qwen-code/issues/10385

5. **[#10405] web-shell 会话切换覆盖层永久锁定（P2）**
   daemon 不可达时选择历史会话会设置 `switchingSessionId`，随后覆盖层永远不消失，用户必须手动重载 webview 才能恢复操作。
   https://github.com/QwenLM/qwen-code/issues/10405

6. **[#10380] OpenAI 兼容网关返回 HTTP 413 后自动压缩无法恢复（P2）**
   长会话若因反向代理请求体积限制返回 413，会话会永久不可用，token 压缩路径未覆盖此错误码。
   https://github.com/QwenLM/qwen-code/issues/10380

7. **[#10400] tools.eager 条目名为 Object.prototype 键导致崩溃（P1, blocked）**
   若 `tools.eager` 配置了如 `constructor` 等名称，`PermissionManager.initialize` 直接崩溃。PR #10098 已因范围超限拆分跟踪。
   https://github.com/QwenLM/qwen-code/issues/10400

8. **[#10430] AppContainer 测试永远无法触达 queued-submission drain**
   共享 mock 导致 config 初始化失败，所有相关逻辑只能靠 `renderHook` 间接测试，覆盖缺口明显。
   https://github.com/QwenLM/qwen-code/issues/10430

9. **[#10369] MCP Apps 内联 UI 在 v0.22.2 中不渲染（P2）**
   payload 已送达、renderer 存在，但 UI 不出现；静默 fallback 加 stale stdio server 导致调试困难。
   https://github.com/QwenLM/qwen-code/issues/10369

10. **[#10210] Agent Team: team_delete 在文件系统清理失败时仍报告成功（P2）**
    `deleteTeamDirs()` 的 `fs.rm` 错误被 `Promise.all` 吞掉，可能留下磁盘残留并误导调用方。
    https://github.com/QwenLM/qwen-code/issues/10210

---

## 重要 PR 进展（Top 10）

1. **[#10408] 用一次性压缩恢复 HTTP 413 拒绝的模型请求**
   把 413 归类为 token 溢出同路径，新增类型化检测器，使长会话在网关限制下可自愈。
   https://github.com/QwenLM/qwen-code/pull/10408

2. **[#10416] web-shell 固定会话保持在原分组中可见**
   此前 Pinned 分组会同时把会话从原始分组移除，导致组计数显示为 0、成员“丢失”。
   https://github.com/QwenLM/qwen-code/pull/10416

3. **[#10436] 让 queued-submission drain 可通过渲染的 AppContainer 触达**
   纯测试脚手架改动：修正共享 `measureElement` mock，使 AppContainer 测试能覆盖真实调用点。
   https://github.com/QwenLM/qwen-code/pull/10436

4. **[#10282] 每轮向模型注入输出风格提醒**
   修复 #9565 中“生成了 reminder 但从未发送”的问题，非默认风格激活时每条用户消息都会附带系统提醒。
   https://github.com/QwenLM/qwen-code/pull/10282

5. **[#9895] daemon 支持 scoped workspace memory tasks**
   为 sessionless 记忆任务的 remember/forget 增加 `project`/`user` 目标，覆盖 REST、ACP 扩展与 TS SDK，并新增能力协商标签。
   https://github.com/QwenLM/qwen-code/pull/9895

6. **[#10345] 恢复 main 分支的 post-merge push 触发**
   仅 `test` job 响应 push；nightly 保持现有两条平台 lane，避免其余 job 重复运行。
   https://github.com/QwenLM/qwen-code/pull/10345

7. **[#10221] 新增 prose-execution 审计与 counter-frame 审计**
   补全 #9655 事故复盘遗留的两个评审视角，覆盖对已应用修复方案与对侧论点的独立审计。
   https://github.com/QwenLM/qwen-code/pull/10221

8. **[#10425] 从绑定 PR 的 closing references 派生 session issue 绑定**
   daemon 的 PR 状态刷新现在同步跟踪 `Fixes #N` 关联的 issue 及其状态，让会话绑定关系更完整。
   https://github.com/QwenLM/qwen-code/pull/10425

9. **[#10259] Goal 消息发送受调用方递归预算约束**
   逐项审计 `client.ts` 中 Goal 类型消息绕过 session 上限的例外，移除不必要的递归预算豁免。
   https://github.com/QwenLM/qwen-code/pull/10259

10. **[#10423] review 在任何 agent 运行前预构建 worktree**
    `QWEN_REVIEW_PREBUILD=1` 时，`fetch-pr` 直接复用 Agent 7 的构建步骤，减少 CI 等待与重复编译。
    https://github.com/QwenLM/qwen-code/pull/10423

---

## 功能需求趋势

- **Web Shell / Web 界面成熟化**：本日 50 条 issue 中近 1/3 与 web-shell 相关（#10385、#10391、#10399、#10405、#10416 等），从 bug 修复走向工作区信息展示、workspace overview、会话分组

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*