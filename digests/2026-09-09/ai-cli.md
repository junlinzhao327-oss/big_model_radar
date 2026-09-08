# AI CLI 工具社区动态日报 2026-09-09

> 生成时间: 2026-09-08 22:35 UTC | 覆盖工具: 7 个

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

# Claude Code 社区动态日报
**2026-09-09** | 数据来源：github.com/anthropics/claude-code

---

## 1. 今日速览

- 发布 v2.1.265，新增遥测字段与 `--plugin-dir` 指向插件目录的支持，补全应用网关侧的用户属性传递。
- 最热 Issue 聚焦 macOS Claude Desktop 与 CLI 子代理会话的兼容性回归，20 条评论，仍在排查中。
- 上次批量清理后，大量陈旧 Issue 于昨日被关闭，但 #92016（CLI/Desktop 会话集成）等新活跃问题仍被持续追踪。

---

## 2. 版本发布

**v2.1.265**（[Release 链接](https://github.com/anthropics/claude-code/releases)）

主要变更：

- 遥测增强：新增 `user.email` 和 `user.groups` 字段，由 Claude Desktop/Cowork 通过 Claude apps 网关发送，与终端会话行为对齐。
- 插件加载优化：`--plugin-dir` 现可指向包含多个插件的文件夹，每个含 manifest 的子文件夹会被加载，并支持运行时动态增删。

> 解读：前者服务于企业级用量归因与团队管理，后者简化了多插件项目的组织与分发。

---

## 3. 社区热点 Issues（Top 10）

### 1. Claude Desktop（Code 标签页）自动拒绝 CLI 原生 SendMessage，破坏子代理恢复
- [#92016](https://github.com/anthropics/claude-code/issues/92016) | **状态：OPEN** | 评论 20 | 👍 7
- 作者：@DennisPh1977｜更新：09-08
- **为何重要**：macOS Desktop 1.46388.1 在 Code 标签页中对 CLI-native `SendMessage` 工具一律自动拒绝，导致依赖子代理续跑的会话在桌面端无法恢复；当前 Desktop 的“会话替换”仅覆盖 session-to-session 场景。属平台回归，社区讨论热度最高。

### 2. Harness 发出的 `<system-reminder>` 措辞与提示注入无法区分
- [#46465](https://github.com/anthropics/claude-code/issues/46465) | **状态：CLOSED** | 评论 15
- 作者：@Studnicky｜更新：09-08
- **为何重要**：系统注入的工具结果中包含 “NEVER mention this reminder to the user” 字样，恰是提示注入攻击的典型口吻，存在被模型/上层应用误判的风险。该安全透明度问题虽被标记 stale 关闭，但值得持续关注。

### 3. Fable 5：含工具调用的响应中，文本内容不显示
- [#81853](https://github.com/anthropics/claude-code/issues/81853) | **状态：CLOSED** | 评论 7 | 👍 3
- 作者：@rhv-resideo｜更新：09-08
- **为何重要**：使用 `claude-fable-5` 时，凡同时包含文本与工具调用的响应，终端主界面只渲染工具调用部分（文本仅在 Ctrl+O 详细记录可见）。同配置下 Opus 4.8 正常——模型行为差异导致的可用性缺陷。

### 4. JetBrains 重做终端重复鼠标事件：链接被打开两次
- [#68568](https://github.com/anthropics/claude-code/issues/68568) | **状态：CLOSED** | 评论 7 | 👍 6
- 作者：@valzf｜更新：09-08
- **为何重要**：JetBrains 新版终端将单击事件投递两次（滚动已去重而点击未去重），导致 URL/文件路径会打开两个标签页/文件。凡是点击驱动的操作均受影响，IDE 集成体验打折。

### 5. Windows Desktop MSIX：退出时更新器强制注册到活动容器，应用不可启动
- [#89687](https://github.com/anthropics/claude-code/issues/89687) | **状态：OPEN** | 评论 6
- 作者：@daringo42-creator｜更新：09-08
- **为何重要**：退出时自动更新将 AppX 包注册到仍在运行的容器中，报错 `0x80070020`，应用需注销/重新登录方可恢复。问题涉及桌面端更新器生命周期，影响面较广。

### 6. Desktop 会话记录静默永久不可用（数据丢失）
- [#92825](https://github.com/anthropics/claude-code/issues/92825) | **状态：OPEN** | 评论 2
- 作者：@mmalc｜创建/更新：09-08
- **为何重要**：macOS 上 Desktop 的 `cliSessionId` 被置空后，历史会话记录永久无法访问且无本地恢复路径。作为 #79044 的后续，数据丢失类问题属于最高优先级缺陷，即使评论数尚少也应重点关注。

### 7. 功能请求：多账号配额池化 + 共享会话上下文
- [#92517](https://github.com/anthropics/claude-code/issues/92517) | **状态：OPEN** | 评论 2
- 作者：@chrisfore｜更新：09-08
- **为何重要**：小型团队希望将多个订阅配额汇聚到项目共享池，并跨账号共享会话上下文以协作同一工程。**这是少有的面向团队协作的功能需求**，而非 bug 报告——隐含需求为“组织级配额管理”。

### 8. 无法更新支付方式：真实账号为 Max 5x，客服系统却显示 Free
- [#80973](https://github.com/anthropics/claude-code/issues/80973) | **状态：CLOSED** | 评论 6 | 👍 1
- 作者：@itsrayforreal｜更新：09-08
- **为何重要**：支付链路报“连接被关闭”，且 Anthropic 支持端（Fin）将 Max 5x 账号误判为 Free 套餐，导致用户既无法自助更新支付方式、也无法走客服解决。账号状态不一致问题直指计费系统数据源。

### 9. Desktop 会话上下文引用 ~/.claude.json 中的过期身份
- [#78838](https://github.com/anthropics/claude-code/issues/78838) | **状态：CLOSED** | 评论 5
- 作者：@m-hoss｜更新：09-08
- **为何重要**：桌面端会话上下文被错误关联到旧账号身份，与当前实际付费账号不符，存在误计费/权限归属风险。作者同日自行更正了最初报告方向，社区已确认问题产生于本地缓存而非服务端计费。

### 10. 无任何活跃聊天却快速耗尽 100% Token 配额
- [#82478](https://github.com/anthropics/claude-code/issues/82478) | **状态：CLOSED** | 评论 5
- 作者：@Fraitz｜更新：09-08
- **为何重要**：用户反馈无明显对话的情况下，账号在一天内消耗至 100% 配额。属于成本超支恐慌的高敏问题，社区对“静默 token 消耗”的担忧集中在此。

---

## 4. 重要 PR 进展

过去 24 小时内**仅 1 条 PR 更新**：

### 延长 issue 生命周期：stale/autoclose 超时从 14 天调整为 90 天
- [#63686](https://github.com/anthropics/claude-code/pull/63686) | **状态：CLOSED**
- 作者：@caseyWebb｜更新：09-08
- **内容**：修改 `scripts/issue-lifecycle.ts` 中的 stale/autoclose 阈值——从 14 天放宽至 90 天，影响“标记 stale 的静默期”与“关闭前宽限”。
- **意义**：结合昨日 50 条内容更新中约 80% 被 stale 关闭的现状，该 PR 将有效减少“社区还在讨论、机器人已锁帖”的现象，提升长尾问题的可见度。

---

## 5. 功能需求趋势

从全部 Issues 的标题与话题标签中，提炼出以下社区最集中的功能方向：

| 趋势方向 | 代表 Issue | 说明 |
| --- | --- | --- |
| **团队/多账号协作** | [#92517](https://github.com/anthropics/claude-code/issues/92517) | 将个人订阅转化为项目级配额池、共享会话上下文，满足小团队协作诉求 |
| **桌面端与 CLI 会话无缝互通** | [#92016](https://github.com/anthropics/claude-code/issues/92016)、[#92825](https://github.com/anthropics/claude-code/issues/92825) | 要求 Desktop Code 标签页完全代理 CLI 原生工具，杜绝数据/会话孤岛 |
| **自动化生命周期更温和** | [#63686](https://github.com/anthropics/claude-code/pull/63686) | 社区希望减少“被机器人抢答式关闭”，给真实讨论留出更长窗口 |
| **账号/账单数据一致性** | [#80973](https://github.com/anthropics/claude-code/issues/80973)、[#78838](https://github.com/anthropics/claude-code/issues/78838) | 套餐状态、身份归属应在本地缓存与服务端严格对齐 |
| **模型层新特性支持** | [#81853](https://github.com/anthropics/claude-code/issues/81853)、[#85932](https://github.com/anthropics/claude-code/issues/85932) | Fable 5 等多模型并存下的行为差异化适配，以及模型无关的 UI 功能统一 |

---

## 6. 开发者关注点

**高频痛点总结：**

- **静默会话/数据不可达**：#92825 与 #81662 暴露一致痛点——后台会话/桌面恢复失败时，**原 transcript 可能变得不可追溯**，开发者希望有更强的本地持久化保障与恢复路径。
- **账号身份与 Token 消耗不透明**：#82478（无聊天却耗 token）、#78838（身份读取错误）共同指向**用量归因不可信**的问题，影响用户对成本的信任。
- **安全机制误伤与不可辨识**：#46465 指系统自身措辞像注入攻击；#85929、#85541 等多起“安全过滤器误杀良性代码”报告，说明 **cyber 安全分类器的误报率让开发者不满**。
- **多终端/IDE 适配质量问题**：#68568（JetBrains 重复点击）、#77967（Windows Terminal 滚动卡输入框）、#78444（后台会话不走代理）显示桌面与 IDE 环境下的**工具交互细节仍不完善**。
- **TUI 与子代理隔离策略僵硬**：#85931（worktree 中无 IO 的循环也报“too complex”）反映出**安全校验语焉不详**，在无逃逸风险时仍拒绝执行，徒增摩擦。

---
> 本日报由公开 GitHub 数据自动生成，仅供参考。所有链接均指向原始讨论，可点击跳转参与交流。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

## Gemini CLI 社区动态日报
**日期：2026-09-09** | 数据源：github.com/google-gemini/gemini-cli

---

### 一、今日速览

今日社区围绕**子代理稳定性**与**安全加固**展开密集讨论：多个高优先级 Issue 将子代理超时误报、挂死、Wayland 环境下 Browser Agent 失败列为 P1 bug，且在持续数月的等待后仍处于 "need-retesting"，社区耐心正在被消耗；PR 方面则集中出现一批针对**路径穿越、提示注入、敏感凭证隔离**等安全修复（至少 6 个），显示官方正对沙箱边界与文件系统防护做系统性加固。此外，**Auto Memory 系列问题**和 **Windows 路径兼容性**也是社区高频关注点。

---

### 二、版本发布

过去 24 小时内发布了 3 个版本：

- **[v0.60.0-preview.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.60.0-preview.0)** — 主要包含两项修复：
  - `fix(core)`: 改进 Web fetch 工具中的目标验证与连接路由
  - `fix(core)`: 在 MCP OAuth 流程中强制实施 RFC 9207 签发者识别（可防范 OAuth 重定向劫持类攻击）
- **[v0.60.0-nightly.20260908.g85aca163f](https://github.com/google-gemini/gemini-cli/releases/tag/v0.60.0-nightly.20260908.g85aca163f)** — 常规每日构建，无显著变更
- **[v0.59.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.59.0)** — 正式版本发布（此前已进入 preview/RC 阶段），包含面向 0.59.0-nightly 系列的变更集合与发布说明

---

### 三、社区热点 Issues（10 个）

##### 1. Subagent recovery after MAX_TURNS 误报为成功 🔥 最热
- **编号**: [#22323](https://github.com/google-gemini/gemini-cli/issues/22323) | P1, bug | 评论 13 | 👍 2
- **核心问题**: `codebase_investigator` 子代理在**尚未执行任何分析、仅在命中 MAX_TURNS 上限**的情况下，仍以 `status: "success"` + `Termination Reason: "GOAL"` 上报，对外隐藏了"中断"这一真实状态，误导主代理与用户。
- **社区看法**: 这是"伪装成功"类 bug，影响面大且难排查，与子代理工作流密切相关。6 月创建至今，状态已进入 need-retesting，但长时间无实质性更新让社区不满。

##### 2. Generalist agent 挂死，等待最长达 1 小时
- **编号**: [#21409](https://github.com/google-gemini/gemini-cli/issues/21409) | P1, bug | 评论 8 | 👍 8
- **核心问题**: Gemini CLI 一旦将任务委托给 generalist agent（如创建文件夹等简单操作）就会**无限期挂起**；用户反复测试，等待 1 小时仍未返回。显式指示模型不要使用子代理后可绕开。
- **社区看法**: 点赞数最高之一，属于高复现率的基础体验问题，严重削弱了对 Agent 能力的信任。

##### 3. 零依赖 OS 沙箱 + 指令意图路由（长期提议）
- **编号**: [#19873](https://github.com/google-gemini/gemini-cli/issues/19873) | P2, enhancement | 评论 9 | 👍 1
- **核心内容**: 提议利用 Gemini 3 模型天然熟悉 POSIX shell 的特性，通过**零依赖 OS 级沙箱** + 命令执行后的"意图路由"（Intent Routing）机制，让模型自由使用 `grep/sed/awk` 等原生工具链，同时不牺牲用户安全性。
- **社区看法**: 已存活 6 个多月，社区认为这是从"限制模型能力"向"在沙箱内最大化能力"演进的关键方向。

##### 4. Windows 路径大小写敏感比较致 ACP/IDE 路由失效
- **编号**: [#24246](https://github.com/google-gemini/gemini-cli/issues/24246) | P2, bug | 评论 3 | 👍 0
- **核心问题**: Gemini CLI 在工具数量超过 128 个（有用户实测 400+ 个）时触发 400 错误。用户期望动态裁剪工具范围、按需注入，而不是一次性堆给模型。
- **社区看法**: 涉及 MCP 生态扩展后的可扩展性问题，对重度使用多 MCP server 的用户是一个不可忽视的瓶颈。

##### 5. Gemini 不会主动使用 skills 与 sub-agents
- **编号**: [#21968](https://github.com/google-gemini/gemini-cli/issues/21968) | P2, bug | 评论 6 | 👍 0
- **核心问题**: 用户为 "gradle"、"git" 配置了自定义 skills，但当任务高度相关时 Gemini **几乎从不主动调用**，只有显式指示才生效。这让用户精心维护的技能库形同虚设。
- **社区看法**: 如果模型不主动使用扩展能力，skills/sub-agent 生态的价值将大打折扣。此问题与上方的 Agent 挂死问题共同指向 Agent 编排层的不足。

##### 6. 浏览器子代理 Wayland 环境下失败
- **编号**: [#21983](https://github.com/google-gemini/gemini-cli/issues/21983) | P1, bug, browser | 评论 4 | 👍 1
- **核心问题**: Browser Agent 在 Wayland 显示服务器下直接失败，无法启动浏览器会话。
- **社区看法**: Linux 用户（特别是较新发行版默认 Wayland）受影响较大。P1 级别但自 3 月以来仍未解决，待复测状态已久。

##### 7. Shell 命令完成后卡"Waiting input"
- **编号**: [#25166](https://github.com/google-gemini/gemini-cli/issues/25166) | P1, core, bug | 评论 4 | 👍 3
- **核心问题**: 简单 CLI 命令已执行完毕，但 Gemini CLI 仍显示命令在运行并卡在"Awaiting user input"，极简命令也会触发。
- **社区看法**: 高频、高干扰的 bug（4 月创建至今无修复），导致自动化流程不可靠。

##### 8. Browser Agent 忽略 settings.json 中 maxTurns 等覆盖配置
- **编号**: [#22267](https://github.com/google-gemini/gemini-cli/issues/22267) | P2, bug | 评论 3 | 👍 0
- **核心问题**: AgentRegistry 启动时虽正确读取了全局/项目级 `settings.json`，但 Browser Agent 实际运行时**完全忽略其中的配置覆盖**。
- **社区看法**: 配置不生效类 bug 后果隐蔽——用户以为设了限制，实际子代理可能无限制运行。

##### 9. Auto Memory：低信号会话无限重试
- **编号**: [#26522](https://github.com/google-gemini/gemini-cli/issues/26522) | P2, bug | 评论 4 | 👍 0
- **核心问题**: Auto Memory 后台提取代理仅当 `read_file` 成功后才会将会话标记为"已处理"。若某条会话被判定为低信号而跳过，则该会话**永远不会被标记**，会在后续索引中反复出现并触发重试。
- **社区看法**: 与 #26525（确定性脱敏）、#26523（无效补丁隔离）、#26516（质检汇总）组成 Auto Memory 质量问题矩阵，说明该功能在数据面存在系统性的工程欠账。

##### 10. 沙箱中挂载宿主机 ~/.gemini 凭据泄露风险
- **编号**: [#29216](https://github.com/google-gemini/gemini-cli/pull/29216)（对应修复 PR）| 4 章中相关 Issue #26525 亦涉及 | 评论 5 | 👍 0
- **关联 Issue**: [#26525](https://github.com/google-gemini/gemini-cli/issues/26525) | P2, security, bug | 评论 5
- **核心问题**: Auto Memory 将本地 transcript 原文发送至后台提取模型，脱敏在**内容已进入上下文之后**才执行；相关服务还可能记录已存在技能的提示词。社区要求实现**确定性脱敏**并减少 Auto Memory 的日志量。

---

### 四、重要 PR 进展（10 个）

##### 1. 原子化文件写入，修复同路径并发编辑静默丢失
- **PR**: [#29244](https://github.com/google-gemini/gemini-cli/pull/29244) | P1, core | 新增 | Open
- **内容**: 并行工具执行下，两个 `replace` 调用可同时作用于同一文件——都读到原始内容、后者覆盖前者，且**双双向上报告成功**。该 PR 引入原子写入并对同路径写操作加锁串行化，防止静默丢编辑。

##### 2. 关闭 `get_internal_docs` 路径守卫的兄弟前缀绕过
- **PR**: [#29249](https://github.com/google-gemini/gemini-cli/pull/29249) | P1, core, security | 新增 | Open
- **内容**: 路径守卫用字符串前缀比较做合法性判断，缺少路径分量边界——任何名称以 docs 目录名开头的兄弟目录（如 `docs-evil/`）都可绕过，将任意文件内容读给模型。修复改用**逐路径分量**比较。

##### 3. 防止间接提示注入（构建文件 + 不受信任 flags）
- **PR**: [#29250](https://github.com/google-gemini/gemini-cli/pull/29250) | size/xl | 新增 | Open
- **内容**: 针对"构建文件被篡改注入恶意指令"和"不受信任的 shell 参数/标志"两类向量，在 restricted 模式下加固 `shell`、`edit` 等内置工具的关键执行路径，规避间接提示注入攻击。

##### 4. 保留显式版本的 Flash 模型 ID
- **PR**: [#29252](https://github.com/google-gemini/gemini-cli/pull/29252) | P1, agent | 新增 | Open
- **内容**: 用户显式传入版本化 Flash 模型 ID（如 `--model flash-2.5-xxx`）时，不再静默映射到 3.5 Flash 默认版，保证 `--model` 精确定位；无效 ID 交给 API 返回明确错误。

##### 5. Windows 下路径比较改为大小写不敏感
- **PR**: [#29247](https://github.com/google-gemini/gemini-cli/pull/29247) | core | 新增 | Open
- **内容**: 修复 `isWithinRoot()` 用 `===`/`startsWith` 比较路径导致的 Windows 问题——`c:\` 与 `C:\` 大小写不同即被误判为越界，破坏 ACP/IDE 文件路由与 ignore-path 规范化。

##### 6. 隔离沙箱运行时，修复宿主机配置目录暴露
- **PR**: [#29214](https://github.com/google-gemini/gemini-cli/pull/29214) | size/l→xl | 更新 | Open
- **内容**: 加固沙箱文件系统边界：将沙箱运行时状态与宿主机配置目录分离、以"清洗后的配置文件"替代宿主机目录挂载、路径越界检查改用 realpath 解析（兼容不存在路径）。

##### 7. 修复确认后历史与遥测重复记录
- **PR**: [#29248](https://github.com/google-gemini/gemini-cli/pull/29248) | cli | 新增 | Open
- **内容**: 当用户在确认弹窗期间又发送新消息时，确认后的 `/resume save <tag>` 等命令会产生重复历史与遥测记录。该 PR 在确认流程中抑制重复插入。

##### 8. A2A Server 缺少 express.json() 中间件导致 JSON-RPC 解析失败
- **PR**: [#29126](https://github.com/google-gemini/gemini-cli/pull/29126) | a2a-server | 更新 | Open（修复 #29073）
- **内容**: `express.json()` 挂载于 `appBuilder.setupRoutes()` **之后**，导致 A2A SDK 路由（如 `POST /`）收到的 `req.body` 为 `undefined`，JSON-RPC 解析完全不可用。调整中间件顺序即可。

##### 9. 对不受信任的工具输出强制信封元数据来源
- **PR**: [#29215](https://github.com/google-gemini/gemini-cli/pull/29215) | core | 已合并 | Closed
- **内容**: 更新系统提示词，要求模型在处理外部工具/MCP server 输出时，仅信任**验证过的顶层 envelope 属性**来推导作者身份与操作状态，防止被工具输出中的脏数据欺骗。

##### 10. 缓解 NTFS 8.3 短文件名（SFN）路径绕过
- **PR**: [#29116](https://github.com/google-gemini/gemini-cli/pull/29116) | core | 更新 | Closed
- **内容**: Windows 上 `git~1`、`env~1`、`node_m~1` 等 NTFS 短名可绕过路径规范化与 AllowedPathChecker。通过增强路径规范化逻辑处理短名展开，封堵路径穿越与黑名单绕过。

---

### 五、功能需求趋势

从全部 50 条活跃 Issue 中提炼出的社区关注方向：

| 方向 | 热度 | 代表性 Issue/PR |
|---|---|---|
| **子代理稳定性与编排** | 🔥🔥🔥 极高 | MAX_TURNS 误报 (#22323)、generalist 挂死 (#21409)、技能/子代理不被主动使用 (#21968) |
| **安全与沙箱加固** | 🔥🔥🔥 高（且集中爆发） | 间接提示注入 (#29250)、信封元数据来源 (#29215)、NTFS 短名绕过 (#29116)、路径守卫修复 (#29249)、宿主配置隔离 |
| **Auto Memory 系统质量** | 🔥🔥 中高 | 确定性脱敏 (#26525)、无限重试 (#26522)、无效补丁

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-09-09

## 今日速览
v1.0.84-2 正式向所有用户开放 Vim 模态编辑模式，此前呼声最高的 #13 也已随之关闭。但社区对「会话恢复稳定性」的抱怨正在集中爆发：长时间会话出现 OOM 崩溃、13GB 调试日志撑爆磁盘、恢复时 MCP 连接被过早取消等 7 个相关 Issue 在过去 24 小时内均有新进展。与此同时，Windows 桌面端 1.1.15 的本地多会话限制引发强烈不满（单 Issue 收获 19👍），成为新的舆论焦点。

## 版本发布
**v1.0.84-2** — 主要更新：
- **Vim 模式全面开放**：无需再等待灰度，在 composer 中输入 `/vim` 或设置 `editorMode: vim` 即可使用模态编辑，输入时实时显示当前模式。
- **Windows 沙箱改进**：在支持的 Windows 沙盒策略下，交互式 shell 命令现在会记录被阻止的访问行为。

## 社区热点 Issues（10 个）
1. **#13 CLI 输入应有 vi/vim 模式（已解决）**
   👍 76 | 评论 11 | 更新于 09-08
   年度最热功能请求终于落地。该 Issue 自 2025-09-25 起持续 11 个月，社区共给出 76 个赞，最终在 v1.0.84-2 中实现并关闭。
   https://github.com/github/copilot-cli/issues/13

2. **#4756 Windows 要求先归档空闲会话才能新建 Local 会话**
   👍 19 | 评论 5 | 更新于 09-08
   桌面应用 1.1.15 回归：同一项目只要存在一个带活动 CLI 进程的 Local 会话，新建第二个会话即报 `invalid argument`。用户被迫频繁归档/恢复，正常多任务工作流被打破。
   https://github.com/github/copilot-cli/issues/4756

3. **#2943 OpenRouter 集成**
   👍 14 | 评论 3 | 更新于 09-08
   用户希望配置 OpenRouter API Key 以调用其模型市场。作者表示 Copilot Chat 已支持相关路由，但 CLI 尚缺此能力——新模型支持呼声持续走高。
   https://github.com/github/copilot-cli/issues/2943

4. **#1724 在界面中展示当前 TODO 清单**
   👍 11 | 评论 1 | 更新于 09-08
   建议仿照 opencode 将 agent 内部维护的 TODO 列表放到侧边栏 TUI 展示，帮助用户实时了解任务进度与下一步计划。
   https://github.com/github/copilot-cli/issues/1724

5. **#4742 桌面应用 1.1.15：活动 Local 会话阻塞第二个 Local 会话**
   评论 10 | 更新于 09-08
   与 #4756 同源问题（不同用户从不同角度报告）。自动更新到 1.1.15 后，只要某项目有一个 Live CLI 进程，就无法在同项目创建新的 Local 分支会话。社区认为该限制与桌面应用对「workspace 锁」的处理过于激进有关。
   https://github.com/github/copilot-cli/issues/4742

6. **#4612 疯狂 FileWatch 事件循环冻结 TUI，调试日志疯长至 13GB**
   评论 9 | 更新于 09-08
   长时间会话恢复后，`rust:copilot_runtime` 进入死循环喷射 `No connection accepted a host event {"kind":"FileWatch"}`，导致 UI 卡死并将磁盘日志撑到 13GB。属于资源耗尽级别的严重稳定性缺陷。
   https://github.com/github/copilot-cli/issues/4612

7. **#4664 恢复长期会话时 JavaScript 堆内存耗尽崩溃**
   评论 7 | 更新于 09-08
   加载/恢复大型历史会话期间 Node.js 进程达到约 4GB V8 堆上限后直接 fatal。长时间跨周会话的用户几乎必然命中的问题，目前无规避手段（连 `/fork` 都无法执行）。
   https://github.com/github/copilot-cli/issues/4664

8. **#2861 压缩失败：模型返回空响应（连续 3 次重试均失败）**
   评论 6 | 更新于 09-08
   在 <30 轮短会话上对 Claude Opus 4.6 执行 `/compact` 仍稳定复现 `received empty response from model`，三连败后会话无法压缩。空响应重试机制疑似对特定模型存在兼容缺陷。
   https://github.com/github/copilot-cli/issues/2861

9. **#4438 `disable-model-invocation: true` 让技能完全不可达而非「仅手动」**
   评论 4 | 更新于 09-07
   按文档将技能设为「禁止模型自动调用」后，该技能反而从模型侧彻底消失：`copilot skill list` 能看到，但模型调用 `skill()` 返回 `Skill not found`。语义与实现不一致。
   https://github.com/github/copilot-cli/issues/4438

10. **#4753 v1.0.83 回归：会话恢复将 MCP 连接超时从 ~16s 砍到 ~1s**
    评论 3 | 更新于 09-08
    恢复会话（前台 handover）时，尚未

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>



</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-09-09

## 今日速览

昨日社区动态主要集中在三个方面：一是 `v0.23.2-preview.0` 与 `v0.23.1` 相继发布，其中 `v0.23.1` 正式移除了 `@qwen-code/webui` 包；二是 Windows 平台 `conhost.exe` 进程泄漏问题（#11303）持续发酵，已被拆分为独立 issue #11352 跟踪；三是权限 deny 规则误伤（#11405）引发讨论，社区已提交对应修复 PR（#11411）。

## 版本发布

**v0.23.2-preview.0**
- 仅包含一项 CI 修复：隔离子进程密集型 E2E 测试，降低 fork 压力（PR #11388）
- 完整变更：[Changelog](https://github.com/QwenLM/qwen-code/releases/tag/v0.23.2-preview.0)

**v0.23.1**
- Breaking Change：正式退役 `@qwen-code/webui` 包（PR #9812）
- 功能更新：Web Shell 可视化与动态管理增强（详情见完整 changelog）
- 完整变更：[Changelog](https://github.com/QwenLM/qwen-code/releases/tag/v0.23.1)

**sdk-typescript-v0.1.9 / v0.1.10**
- 两个 SDK 版本相继发布，捆绑 CLI 版本分别为 0.23.0 与 0.23.1
- 包含 #11022 中请求的两项修复：`enableManagedAutoMemory` 设置生效、prompt-cache 相关修复
- 详见：[SDK Releases](https://github.com/QwenLM/qwen-code/releases)

## 社区热点 Issues

**1. [P1] [Windows] qwen-cli 泄漏 headless conhost.exe 进程 — 347 个进程 / 约 2.8GB 内存**
- 作者：@Andrea-Bruno | 评论 10 | 创建 09-07
- 在 Windows 上，VS Code Companion 内嵌的 qwen-cli 会持续泄漏 ConPTY 进程（12 小时内累计 347 个、占用约 2.8GB 内存）且从不释放。这是近期最受关注的 Windows 稳定性问题之一。
- 链接：https://github.com/QwenLM/qwen-code/issues/11303

**2. [P1] [Windows] node-pty 在 shell 自然退出时泄漏 ConPTY host（conhost.exe）**
- 作者：@yiliang114 | 评论 3 | 创建 09-08
- 从 #11303 拆分出的不可修复部分：baton 在 onExit 前被清除，导致 JS 侧无法调用 ClosePseudoConsole，为上游依赖缺陷。
- 链接：https://github.com/QwenLM/qwen-code/issues/11352

**3. [P2] Deny 规则按 pattern 拒绝工具后，模型被误导为该工具完全不可用**
- 作者：@nihil-pro | 评论 3 | 创建 09-08
- 当 `Bash(npm view *)` 这类 pattern 级 deny 规则触发时，错误信息过于笼统，模型会认为整个工具被禁用而非仅该调用被拒。社区已提交 PR #11411 修复提示信息。
- 链接：https://github.com/QwenLM/qwen-code/issues/11405

**4. [P2] sdk-typescript Docker 测试共享同一 QWEN_HOME，memory prefetch 干扰 fake-server 响应**
- 作者：@yiliang114 | 评论 3 | 创建 09-08
- `release-sdk.yml` 的 docker 场景下，`permission-control.test.ts` 15/20 测试确定性失败，疑似测试隔离问题，影响 SDK 发布质量。
- 链接：https://github.com/QwenLM/qwen-code/issues/11394

**5. [P2] 请求发布包含 managed-memory 与 prompt-cache 修复的新版 @qwen-code/sdk（已关闭）**
- 作者：@qoggy | 评论 3 | 创建 09-04 | 关闭 09-08
- 社区明确提出需要新 SDK 发布以包含 #6941 与 #8464 两项已合入 main 的修复；SDK v0.1.9 / v0.1.10 已响应此需求。
- 链接：https://github.com/QwenLM/qwen-code/issues/11022

**6. [P2] daemon 扩展：将注册与活动实例解耦，引入 LRU live set 以突破 25 工作区上限**
- 作者：@doudouOUC | 评论 3 | 更新 09-08（含容量测量数据）
- 作者实测更新指出：1/25/256 容量基线中闲置成本并不足以支持完整 LRU 作为硬前置条件，建议先做注册/运行时解耦。涉及 daemon 架构设计方向。
- 链接：https://github.com/QwenLM/qwen-code/issues/11386

**7. [P2] Channel service pidfile 误判 recycler PID 为存活服务**
- 作者：@BenGuanRan | 评论 3 | 更新 09-08
- `readServiceInfo()` 只验证 JSON 结构和 `process.kill(pid, 0)`，无法证明该 PID 属于原进程，存在被系统回收的 PID"顶替"的风险。
- 链接：https://github.com/QwenLM/qwen-code/issues/10685

**8. [P3] Web Shell：turn navigation rail 出现后，消息列与 composer 水平错位**
- 作者：@qqqys | 评论 4 | 创建 09-08
- 完成至少一轮对话后，左侧 turn-navigation rail 出现，导致 transcript 列不再与下方 composer 对齐，属 UI 细节回归。
- 链接：https://github.com/QwenLM/qwen-code/issues/11335

**9. [P2] 无状态 SSE 限流错误跳过了 rate-limit 重试**
- 作者：@DragonnZhang | 评论 2 | 关闭 09-08
- Anthropic 兼容端点可在 HTTP 200 流中发送无状态码/status 的临时限流错误，Qwen Code 未将其识别为可重试错误，导致对话中断。已有对应 PR #11291 修复。
- 链接：https://github.com/QwenLM/qwen-code/issues/11215

**10. [P2] ACP/Zed 中 AskUserQuestion 显示为 "Raw Input"**
- 作者：@randmaru | 评论 2 | 创建 09-08
- Zed IDE 中多选提问界面未正常渲染，而是显示原始输入模式，影响 ACP 交互体验。
- 链接：https://github.com/QwenLM/qwen-code/issues/11361

另有多个 CI 失败自动跟踪 issue（#11343、#11364、#11367、#11373、#11377、#11389）显示 main 分支 E2E 及 Lint 工作流近期处于不稳定状态，值得注意。

## 重要 PR 进展

**1. fix(permissions): 复合与虚拟操作 shell 拒绝时引用匹配的 deny 规则**
- 作者：@yiliang114 | 更新 09-08
- 直接修复 #11405：当命令被 pattern 级权限规则拒绝（如 `Bash(npm view *)`），提示信息现在会引用匹配规则，并将拒绝描述为"调用级"而非"工具级"，避免模型误解。
- 链接：https://github.com/QwenLM/qwen-code/pull/11411

**2. fix(web-shell): 在空闲时保留 daemon 拒绝的轮转中消息**
- 作者：@wenshao | 更新 09-08
- 当轮转进行中发送的消息因会话已空闲而被拒时，daemon 会明确说明原因，浏览器会将其作为普通 prompt 重新发送，而非提示发送失败。
- 链接：https://github.com/QwenLM/qwen-code/pull/11289

**3. fix(core): 重试无状态上游错误而非结束对话**
- 作者：@wenshao | 更新 09-08
- 对应 #11215：当网关在已返回 200 的 SSE 流中推送错误对象时（无 HTTP status），OpenAI SDK 层现将其识别为可重试错误，进入 bounded backoff 而非直接中断。
- 链接：https://github.com/QwenLM/qwen-code/pull/11291

**4. fix(core): 在 checkout hooks 失败时保留分支提交**
- 作者：@gauravyad86 | 更新 09-08
- 分支创建失败时不再删除 checkout hooks 或并发写入者产生的历史记录；仅在确实切换了分支时才执行恢复。
- 链接：https://github.com/QwenLM/qwen-code/pull/11258

**5. feat(web-shell): 暴露 assistant turn 结算生命周期**
- 作者：@yiliang114 | 更新 09-08
- 为宿主应用新增可选回调：报告 daemon 权威的 assistant turn 结算结果（完成/取消/失败、stop reason、错误详情、最终消息），在 terminal state 后投递。
- 链接：https://github.com/QwenLM/qwen-code/pull/11251

**6. feat(core): ModelStudio Standard/Token Plan 默认启用内置 web_search**
- 作者：@qqqys | 更新 09-08
- 当正在运行的模型可支持搜索请求时，内置 `web_search` 工具自动启用，无需三项独立设置；Alibaba ModelStudio presets 声明 DashScope 服务端搜索工具支持。
- 链接：https://github.com/QwenLM/qwen-code/pull/11348

**7. feat(core): 扩展 Kimi、Qwen、DeepSeek reasoning presets**
- 作者：@callmeYe | 更新 09-08
- Moonshot K3 支持 low/high/max，K2.7 Code 保持 thinking-only，K2.6 暴露原生 thinking toggle；Qwen 3.8 支持 low/medium/xhigh；DeepSeek V4 Pro 与 Flash 也有更新。
- 链接：https://github.com/QwenLM/qwen-code/pull/11349

**8. feat(serve): 将扩展作用域限定到 workspace runtimes**
- 作者：@ytahdn | 更新 09-08
- 将全局扩展目录通过各 workspace 选定的 runtime 暴露；将扩展状态协调到活跃 workspace runtime，并提供 workspace 限定的 daemon/SDK 访问。
- 链接：https://github.com/QwenLM/qwen-code/pull/11086

**9. fix(ci): 将 serve route E2E 与 fork 压力隔离（#11389）**
- 作者：@qwen-code-dev-bot | 更新 09-08
- 在 Linux E2E 批次（docker 与 sandbox:none）完成后，将 `qwen serve` route 套件单独跑在单个 Vitest fork 中，规避 fork 压力引发的 flaky。
- 链接：https://github.com/QwenLM/qwen-code/pull/11391

**10. feat(web-shell): 改善 session overview 导航与会话详情**
- 作者：@wenshao | 更新 09-08
- 每个会话在标题下方展示 workspace、branch 和 PR；为 approval、question、running、idle 状态增加视觉区分，并加入状态过滤与 branch/PR 搜索。另有 follow-up issue #11390 记录后续收尾。
- 链接：https://github.com/QwenLM/qwen-code/pull/11238

**其他值得关注的 PR：**
- **feat(core): 为延迟工具保留 prompt cache** — 稳定两步桥接：`tool_search` 查看 schema、`tool_call` 执行调用（PR #10410）
- **fix(web-shell): 修复本地文件桥接的 trust-gate 与 bystander 缺口**（PR #11169）
- **refactor(channels): 移除废弃的 block streaming**（PR #11381）
- **fix(web-shell): 替换 split rerender 测试中的 undefined mock**（PR #11406，修复 #11404）

## 功能需求趋势

1. **工具权限控制的精细化与可解释性**
   - 社区希望 deny 规则的错误信息能精确定位到具体调用与匹配规则（#11405），而非让模型误判工具整体不可用。对应 PR 已第一时间提出，反映了开发者对权限可诊断性的高要求。

2. **Web Shell 可嵌入、可定制、可白标**
   - 多个 issue 集中于将 `qwen serve` 的 Web Shell

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*