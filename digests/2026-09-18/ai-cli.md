# AI CLI 工具社区动态日报 2026-09-18

> 生成时间: 2026-09-17 22:35 UTC | 覆盖工具: 7 个

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
**日期：2026-09-18** · 数据来源：github.com/anthropics/claude-code

---

## 一、今日速览

今日最重磅的动态是 Issue #91870（Mods 可扩展性提案）持续发酵，已累积 **194 条评论、120 个 👍**，官方在其中发布社区更新，承诺"数周内"交付 function hooks。与此同时，仓库进行了一轮大规模的 **stale 清理**，过去 24 小时更新的 50 条 Issue 中绝大多数被标记 `stale` 并关闭。发布层面，v2.1.275 与 v2.1.274 连续落地，聚焦网关登录确认、消息队列发送快捷键与内存告警。

---

## 二、版本发布

### v2.1.275
- **网关登录确认**：登录账号信息被纳入 Claude apps gateway 的登录流程，网关声明账号后需用户确认才保存凭据，`/status` 中可查看该账号。
- **新增"立即发送"快捷键**：`ctrl+enter`（或 `ctrl+x ctrl+s`）可中断当前回合，并一次性发送队列中所有待发消息。

### v2.1.274
- **内存告警**：内存占用进入临界状态时显示可见警告，并给出释放内存或安全重启的操作步骤。
- **MCP 启动等待可控**：新增环境变量 `CLAUDE_CODE_MCP_STARTUP_WAIT_MS`，用于限定首个非交互回合等待 MCP 服务器连接的最长时间（`0` 表示不等待）。
- 另有一条关于 `effort` 属性的变更因摘要截断无法确认细节（疑与 `cl` 开头的配置或命令相关）。

---

## 三、社区热点 Issues

> 说明：过去 24 小时更新的 50 条 Issue 中，仅 #91870 处于 OPEN 状态，其余展示条目均为 CLOSED + `stale`。以下按重要性排序。

**1. [#91870](https://github.com/anthropics/claude-code/issues/91870) — Mods：让 Claude 的可扩展性提升 10 倍** `OPEN`
今日唯一的活跃议题，也是最热的议题。作者 @poteat，194 评论 / 120 👍。官方更新明确表示"数周内交付 function hooks"，并感谢社区高信号反馈"实质性影响了设计"。这是判断 Claude Code 扩展生态走向的关键风向标。

**2. [#79399](https://github.com/anthropics/claude-code/issues/79399) — Agent 批量创建 PR 缺乏保护机制** `CLOSED · stale`
在真实外部仓库自动创建 91 个 PR，全部被自动关闭，仓库将用户锁定。这是一个典型的 **agent 破坏性自动化**案例，暴露出缺少批量操作预检与限流护栏。虽被 stale 关闭，但其风险模型值得持续关注。

**3. [#79440](https://github.com/anthropics/claude-code/issues/79440) — Bash 工具启用 `expand_aliases`，别名可在 Hook 批准后改写命令** `CLOSED · stale`
非交互 shell 仍开启别名展开，导致 alias/function 可在 `PreToolUse` hook 审批通过**之后**静默替换实际执行命令。这是一个绕过安全审查链的隐患，属于权限模型层面的严重问题。

**4. [#79478](https://github.com/anthropics/claude-code/issues/79478) — 会话级模型切换按高价计费，无任何提示** `CLOSED · stale`
用户意图仅对少数任务级/agent 级调用启用高价模型，结果整个交互会话跑在高价模型上。核心诉求是**成本可见性与作用域隔离**。

**5. [#79436](https://github.com/anthropics/claude-code/issues/79436) — VS Code 扩展内联渲染图片** `CLOSED · stale`
当前聊天面板仅显示 `[Image]` 占位符。这是 IDE 集成体验中最直观的体验缺口之一。

**6. [#79542](https://github.com/anthropics/claude-code/issues/79542) — 内置"朗读回复"（TTS）模式** `CLOSED · stale`
用户已用 `Stop` hook 自建本地 TTS 方案（读取 transcript、剥离 markdown 后朗读），建议官方做成 opt-in 内置能力。属于无障碍（a11y）方向的实用提案。

**7. [#79381](https://github.com/anthropics/claude-code/issues/79381) — `/nudge`：发送不写入会话上下文的一次性指令** `CLOSED · stale`
6 👍。解决会话中途临时纠偏却污染上下文的问题，是上下文管理的常见痛点。

**8. [#79296](https://github.com/anthropics/claude-code/issues/79296) — Claude Desktop 官方支持 Arch Linux 及衍生发行版** `CLOSED · stale`
8 👍，为列表内点赞最高之一，反映 Linux 桌面用户群体的明确缺口。

**9. [#79311](https://github.com/anthropics/claude-code/issues/79311) — VS Code 扩展渲染 MCP `claude/channel` 推送通知** `CLOSED · stale`
要求 VS Code 原生面板与终端 TUI 功能对齐。IDE 与终端的能力割裂是反复出现的主题。

**10. [#79468](https://github.com/anthropics/claude-code/issues/79468) — Keybindings 支持直接切换模型与调整 effort** `CLOSED · stale`
当前 `keybindings.json` 只能打开选择器，无法一键切到指定模型或直接调 effort，键盘流用户的操作效率受限。

**其他值得一提**：[#79534](https://github.com/anthropics/claude-code/issues/79534)（虚构生物题材游戏代码被内容策略误拒）、[#79401](https://github.com/anthropics/claude-code/issues/79401)（`VirtualMessageList: itemKeys/messages length desync` 遥测错误）、[#79304](https://github.com/anthropics/claude-code/issues/79304)（要求恢复已下线的 Fable 模型支持）。

---

## 四、重要 PR 进展

> 过去 24 小时更新的 PR 共 **3 条**，全部列出。

**1. [#95198](https://github.com/anthropics/claude-code/pull/95198) — `mods/diff`：将 `openPane` 返回值类型放宽为 `unknown`** `OPEN` · @poteat
diff mod 的主机契约声明 `openPane` 返回 `Promise<void>`，而 `$.ui.open` 即将返回一个结果对象。改为 `Promise<unknown>` 后可同时兼容当前与下一版引擎类型定义。无调用方读取该值，行为无变化——属于面向 Mods 平台演进的类型兼容准备。

**2. [#94847](https://github.com/anthropics/claude-code/pull/94847) — `diff`：首次编辑仅在确有文件可列时才打开面板** `OPEN` · @bcherny
修复原逻辑在会话首次 Edit/Write/NotebookEdit **之前**就自动打开 diff 面板的问题。当写入发生在仓库外、被忽略的文件或不同 worktree 时，会出现空的"No tracked changes"面板。现在改为先 fetch 再决定是否开面板。

**3. [#87077](https://github.com/anthropics/claude-code/pull/87077) — `fix(pr-review-toolkit)`：修复所有 agent 中无效的 YAML frontmatter** `OPEN` · @anishsamant
各 agent 的 `description` 是未加引号的标量，内含 `Daisy: "..."` 这类对话行，在 YAML 中会被解析为嵌套映射，导致 frontmatter 解析失败、`name/description/model` 全部为空。属于影响 agent 加载的实质性修复。

---

## 五、功能需求趋势

综合本次数据，社区关注方向集中在以下几类：

| 方向 | 代表 Issue | 诉求要点 |
|---|---|---|
| **扩展性平台（Mods / Hooks / Plugins）** | #91870、#95198 | 从"配置式扩展"走向函数级 hook，官方已承诺近期交付 |
| **IDE 集成（VS Code / Desktop）** | #79436、#79311、#79394、#79361 | 内联图片渲染、MCP 推送通知、会话历史配置——与终端 TUI 能力对齐 |
| **安全与权限护栏** | #79399、#79440、#79411、#79809、#79330 | 批量操作保护、hook 审批后命令不可被改写、按 tab 撤销访问权、权限对话框可重绑定 |
| **成本与模型管理** | #79478、#79479、#79468、#79304 | 计费可见性、模型作用域隔离、按任务复杂度主动建议升级、直接绑定模型切换键 |
| **TUI / 交互细节** | #79453、#79451、#79443、#79456、#79466、#79520 | 退出行为一致性（Ctrl+D）、picker 支持子串匹配、可交互删除会话、按时间排序文件建议、URL fragment 深链 |
| **上下文与会话管理** | #79381、#79391、#79435 | 一次性不持久指令、HTML 会话导出、`cleanupPeriodDays` 初始化引导 |
| **平台覆盖与国际化** | #79296、#79720 | Arch Linux 官方支持、斜杠命令描述多语言（i18n） |

---

## 六、开发者关注点

1. **Stale 清理引发反馈闭环担忧**：本轮 50 条更新 Issue 中仅 1 条 OPEN，其余大量以 `stale` 关闭。部分被关闭条目（如 #79440 的 hook 安全绕过、#79399 的批量 PR 事故）并非无价值问题，社区可能对"以 stale 关闭代替修复"产生抵触情绪。**建议官方对高价值 stale 项给出明确状态说明。**

2. **安全审批链的完整性**：`expand_aliases` 案例说明，`PreToolUse` hook 看到的内容与 shell 实际执行的内容可能不一致——这类"审批后变更"是权限模型中最需要封堵的一类漏洞。

3. **Agent 自主性的边界**：91 个 PR 的失控事件表明，当 agent 具备对外部系统的写权限时，缺少预检、限流与人工确认的护栏会带来真实损害。

4. **成本透明度**：高价模型的会话级作用域"静默生效"是最易产生账单冲击的体验问题，开发者希望有明确的确认提示与作用域区分。

5. **IDE 与终端的能力落差**：多条 Issue（图片渲染、MCP 推送、会话历史）指向同一诉求——VS Code / Desktop 应当与终端 TUI 保持功能对等，而非二等公民。

6. **键盘流与效率细节**：Ctrl+D 行为一致性、picker 子串匹配、keybindings 直连模型切换等"小改动高频次"需求密集出现，表明重度用户对操作肌肉记忆的一致性极为敏感。

---

*本日报基于 GitHub 公开数据自动整理，Issue/PR 状态与评论数随时间变化。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-09-18）

数据来源：github.com/openai/codex

---

## 1. 今日速览

- **发布侧**：0.155.0 的 alpha 通道在 24 小时内连续推进 4 个版本（alpha.14 → alpha.17），但仍为无说明的滚动构建，稳定版用户暂无可感知变更。
- **社区侧**：Windows/WSL 环境切换导致项目创建/删除失败（#41290，76 条评论、54 赞）持续占据热度榜首；模型容量限制（#28507）与桌面端会话卡死（#24287）紧随其后，三大痛点均为长期未闭环问题。
- **PR 侧**：过去 24 小时大量 PR 被批量关闭（多由 `copyberry[bot]` 提交），主线围绕**沙箱权限抽象（EnvironmentAccess）**、**网络策略按执行器 OS 校验**、**OAuth 诊断安全**与**发布上传限流**展开，属于底层架构与安全加固型迭代。

---

## 2. 版本发布

过去 24 小时共 4 个发布，均为 Rust 侧预发布标签，**无 changelog 内容**：

| 版本 | 说明 |
|---|---|
| rust-v0.155.0-alpha.17 | Release 0.155.0-alpha.17 |
| rust-v0.155.0-alpha.16 | Release 0.155.0-alpha.16 |
| rust-v0.155.0-alpha.15 | Release 0.155.0-alpha.15 |
| rust-v0.155.0-alpha.14 | Release 0.155.0-alpha.14 |

**解读**：alpha 号在 24 小时内连跳 4 次，说明 0.155.0 分支正处于高频合入期，但缺少 release note 会让下游（尤其是基于 bundled codex-cli 的桌面端）难以判断哪些问题已修复。结合 #46298 中用户报告 "bundled codex-cli 0.155.0-alpha.2.6"，可推测桌面端与 Rust CLI 的版本耦合仍是排障难点。

---

## 3. 社区热点 Issues（Top 10）

1. **[#41290](https://github.com/openai/codex/issues/41290) Windows/WSL 切换 Agent Environment 后项目创建与删除失败**
   `bug, windows-os, app` | 76 评论 | 👍 54
   Codex App 26.825.31414 在将 Agent Environment 切到 WSL 后，项目无法创建或移除。这是当前热度最高、持续时间最长（8 月底创建）的问题，54 个赞说明影响面集中在 Windows + WSL 这一主流开发组合上。

2. **[#28507](https://github.com/openai/codex/issues/28507) "Selected model is at capacity" 持续报错**
   `bug, rate-limits, app` | 56 评论 | 👍 52
   自 6 月起持续跟踪，Pro 5x 用户仍频繁撞上容量限制。评论数与点赞数双高，反映的已不只是单点 bug，而是**模型供给与限流策略**层面的信任问题。

3. **[#24287](https://github.com/openai/codex/issues/24287) 桌面端接受 prompt 后 UI 卡在 Thinking，Stop 失效且重启后 turn 不可见**
   `bug, app, session, app-server` | 30 评论 | 👍 14
   典型的会话状态机缺陷：请求已发出但 UI 无终态、中断无效、turn 丢失。对日常使用者属于"阻断级"体验问题，长期未闭合。

4. **[#31878](https://github.com/openai/codex/issues/31878) ChatGPT/Codex 合并后 Projects 在桌面侧边栏消失**
   `bug, app` | 17 评论 | 👍 18
   网页端存在但 macOS 桌面端不显示，是产品合并后的数据同步/归属回归，直接影响用户在桌面端的工作区组织方式。

5. **[#42739](https://github.com/openai/codex/issues/42739) Windows 桌面更新后本地项目从侧边栏消失**
   `bug, windows-os, app, session` | 14 评论
   与 #31878 同类但平台为 Windows：Projects 显示 "No projects"，而 Recents 与磁盘目录都正常。两地并发报告提示是**项目索引/元数据迁移**问题而非单一平台 bug。

6. **[#41779](https://github.com/openai/codex/issues/41779) Windows 本地 API 启动被 "blocked by policy" 拒绝**
   `bug, windows-os, sandbox, tool-calls, app` | 13 评论
   `exec_command` 在 PowerShell 命令执行前即被策略拦截，且不产生 stdout/stderr 日志。与 #42688（飞书 CLI 凭据在沙箱内不可用）、#46252（app-server 忽略 default_permissions）共同构成**沙箱/权限模型**这一类高频噪音。

7. **[#32188](https://github.com/openai/codex/issues/32188) 后台 exec 会话完成时需要事件驱动的唤醒机制**
   `enhancement, CLI, tool-calls` | 10 评论 | 👍 13
   当前长命令只能靠模型轮询 `write_stdin` 或委派子智能体，造成额外 turn 消耗。这是一个高质量的功能提案，指向 agent 编排的**效率与 token 成本**优化。

8. **[#33171](https://github.com/openai/codex/issues/33171) 远程压缩（remote-compaction）容量错误导致长期目标被终结**
   `bug, context, app, connectivity, app-server` | 9 评论
   长时 `/goal` 任务反复触及远程压缩容量上限后整体失败，而其他任务健康。涉及**上下文管理与长任务可靠性**，是 agent 长跑场景的关键缺陷。

9. **[#46304](https://github.com/openai/codex/issues/46304) ChatGPT Pro 账号下 GPT-5.6 Sol 与 GPT-6 Astra 被拒**
   `bug, auth, app` | 4 评论 | 9-17 新建
   报错为"该模型在使用 ChatGPT 账号时不受支持"，而 GPT-5.6 Terra 正常。这是**新模型接入与账号权限映射**的最新信号，值得优先跟踪。

10. **[#40124](https://github.com/openai/codex/issues/40124) CLI / Web / 移动端之间的无缝会话交接**
    `enhancement, CLI, session, remote` | 6 评论
    希望在终端发起的会话能在手机或网页上原样继续。与 #19893（[Azure Auth 支持](https://github.com/openai/codex/issues/19893)）共同代表**企业化与多端化**的诉求方向。

---

## 4. 重要 PR 进展

> 说明：过去 24 小时 PR 几乎全部处于 CLOSED 状态且无评论数据，多由 `copyberry[bot]` 提交，可视为一批已处理完毕的基础设施改动。

**权限与沙箱（本日最大主题）**

1. **[#46271](https://github.com/openai/codex/pull/46271) 通过 Windows 沙箱配置启用 MXC 选择**
   接受 `windows.sandbox = "mxc"`，并在环境配置、命令执行、patch 写入与沙箱元数据中全程保留所选后端，TUI 侧同步展示沙箱状态。

2. **[#46302](https://github.com/openai/codex/pull/46302) 按执行器 OS 校验网络 socket 策略**
   修复控制器与执行器跨 OS 场景（如 Linux 控制器 + Windows 执行器）下，合法的绝对路径被错误拒绝的问题——直接对应 Windows 路径类 issue 的根因之一。

3. **[#46293](https://github.com/openai/codex/pull/46293) 技能发现与加载统一走 `EnvironmentAccess`**
   将技能发现、环境技能加载、插件命名空间解析从直接调用 `ExecutorFileSystem` 改为经 `EnvironmentAccess`，消除隐式沙箱参数。

4. **[#46268](https://github.com/openai/codex/pull/46268) 新增绑定环境权限的文件系统访问器**
   引入 `EnvironmentAccess` 与 `FileSystemEnvironmentAccessor`，对外只暴露受控操作，禁止消费者提取底层文件系统或切换沙箱。

**安全与认证**

5. **[#46300](https://github.com/openai/codex/pull/46300) 集中化 OAuth 登录与刷新，收紧诊断信息**
   合并两套 OAuth 请求/错误处理路径，避免 token endpoint 错误回显凭据、JSON 解码失败泄露 token 值。

6. **[#46297](https://github.com/openai/codex/pull/46297) 为全部多智能体 V2 工具支持目录化描述**
   将模型目录描述覆盖从 `spawn_agent` 扩展到 `send_message`、`followup` 等工具，提升多 agent 场景下模型选择工具的准确性。

**性能与状态管理**

7. **[#46305](https://github.com/openai/codex/pull/46305) 避免为 app-server 活跃 turn 查询克隆 turn items**
   暴露 `ThreadState::active_turn_id()`，中断校验等只需 ID 的调用不再生成完整 turn 快照。

8. **[#46294](https://github.com/openai/codex/pull/46294) 将线程启动元数据与重放历史分离**
   `CodexThread` 不再持有完整 `SessionConfiguredEvent`（含初始重放消息），减少内存与克隆开销。

9. **[#46292](https://github.com/openai/codex/pull/46292) 同步 Guardian 评审保留所选推理强度**
   在启用 `reasoning_effort_override` 且父历史含强度更新时，保证同步 Guardian 评审仍使用请求级选择的 reasoning effort。

**TUI / 渲染与工程化**

10. **[#46266](https://github.com/openai/codex/pull/46266) 扩展 Unicode 数学渲染（重音、符号、分隔符）**
    支持 `\hat`、`\bar`、`\vec`、`\dot` 等作用于单个可见字素，并保留上下标能力，同时补充物理、集合、逻辑、箭头类符号。同类还有 **[#26476](https://github.com/openai/codex/pull/26476)** 在 iTerm2 标签页显示实时活动详情（限制输出量、避免高频 OSC 写入）。

11. **发布工程**：**[#46303](https://github.com/openai/codex/pull/46303)** 将 release 资产改为串行上传并升级 `softprops/action-gh-release` 至 v3.0.3；**[#46278](https://github.com/openai/codex/pull/46278)** 降低 R2 上传并发并启用标准重试——两者均针对 GitHub/R2 的**二级限流**问题。

---

## 5. 功能需求趋势

从过去 24 小时更新的 50 条 Issue 中可提炼出以下方向：

| 方向 | 代表 Issue | 说明 |
|---|---|---|
| **沙箱与权限透明度** | #41779、#42688、#46252、#46210 | 权限被拒时缺少诊断、`default_permissions` 被静默忽略、hook 信任路径无文档，是当前最密集的一类诉求 |
| **多端会话与工作区同步** | #31878、#42739、#40124 | Projects 索引在不同端/不同版本间丢失，以及 CLI→Web→移动端的会话交接 |
| **限流与模型可用性** | #28507、#22073、#46298、#40082 | 容量错误、启动即消耗额度、用量不显示、第三方模型被隐藏 |
| **上下文与长任务可靠性** | #33171、#32188 | 远程压缩失败会终结整个目标；后台任务缺少事件驱动唤醒 |
| **IDE / 编辑器体验** | #15684、#11846 | 主题回归（已修复）、macOS 原生拼写检查缺失 |
| **企业级认证** | #19893、#46304 | Azure 认证支持、ChatGPT 账号与特定模型的权限映射 |
| **Windows 平台专项** | #41290、#42739、#41779、#10347、#43498 | UNC 路径规范化、CUA surface 被错误裁剪、WSL 环境切换等 |
| **macOS 稳定性** | #43089、#45449、#45435 | CrBrowserMain SIGTRAP 崩溃、Chrome 扩展 native messaging 清单缺失 |

---

## 6. 开发者关注点

1. **"静默失败"是最被反感的

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报｜2026-09-18

> 数据来源：[github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)  
> 统计窗口：过去 24 小时（截至 2026-09-17 更新）

---

## 1. 今日速览

今日社区焦点集中在 **子代理生命周期可靠性** 与 **终端/Shell 执行稳定性** 两条主线。最受关注的是 `#22323` 子代理达到 `MAX_TURNS` 后仍被报告为 `GOAL success` 的问题，已有对应修复 PR `#29367` 提交。此外，VS Code 扩展的焦点保持、ConPTY 进程退出同步、会话恢复时工具响应重复回放等多项 P1 修复正在推进。

---

## 2. 版本发布

过去 24 小时发布 1 个 nightly 版本：

- **v0.62.0-nightly.20260917.g6a466a7e2**  
  该版本为每日构建，未附带详细变更说明。  
  链接：[Release](https://github.com/google-gemini/gemini-cli/compare/v0.62.0-nightly.20260916.g6a466a7e2...v0.62.0-nightly.20260917.g6a466a7e2)

---

## 3. 社区热点 Issues（精选 10 条）

### ① #22323 子代理 MAX_TURNS 恢复被误报为 GOAL 成功
- **状态**：OPEN｜priority/p1｜评论 13｜👍 2
- **要点**：`codebase_investigator` 子代理在达到最大轮次限制、尚未完成分析的情况下，仍返回 `status: "success"` 和 `Termination Reason: "GOAL"`，掩盖了中断事实。
- **为什么重要**：这是当前评论数最高的 Issue，直接关系到用户能否信任子代理的执行结果；错误成功信号会误导后续自动化流程。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/22323

### ② #21409 Generalist agent 无限挂起
- **状态**：OPEN｜priority/p1｜评论 8｜👍 8
- **要点**：一旦 Gemini CLI 委派给 generalist agent，即使是创建文件夹这类简单操作也会永久挂起，用户等待长达一小时仍未恢复；禁用子代理委派可规避。
- **为什么重要**：👍 数最高的 P1 问题，说明大量用户受到实际阻塞，是当前最影响可用性的缺陷之一。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/21409

### ③ #25166 Shell 命令执行完成后仍卡在 “Waiting input”
- **状态**：OPEN｜priority/p1｜评论 4｜👍 3
- **要点**：简单 CLI 命令已结束，但界面仍显示 shell 命令处于活动状态并等待用户输入。
- **为什么重要**：这是高频交互路径上的卡死问题，直接影响日常 shell 工作流。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/25166

### ④ #19873 零依赖 OS 沙箱 + 执行后意图路由
- **状态**：OPEN｜priority/p2｜评论 9｜👍 1
- **要点**：利用 Gemini 3 模型原生 bash 亲和性，通过零依赖 OS 级沙箱和事后意图路由，在不牺牲安全性的前提下释放模型使用 POSIX 工具链的能力。
- **为什么重要**：属于架构级增强提案，代表 “模型原生能力最大化” 与 “安全边界” 之间的平衡方向。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/19873

### ⑤ #22745 AST 感知文件读取、搜索与代码库映射评估
- **状态**：OPEN｜priority/p2｜评论 7｜👍 1
- **要点**：评估 AST 感知工具能否更精确地读取方法边界、减少误读轮次、降低 token 噪声，并改善代码库导航。
- **为什么重要**：如果落地，将显著提升大型代码库场景下的上下文效率。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/22745

### ⑥ #21968 Gemini 不主动使用 skills 和 sub-agents
- **状态**：OPEN｜priority/p2｜评论 6
- **要点**：用户反馈即使存在高度相关的自定义 skill（如 gradle、git），模型也不会主动调用，除非显式指令。
- **为什么重要**：这削弱了 skills/sub-agents 体系的价值，是功能采纳率的核心障碍。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/21968

### ⑦ #26525 Auto Memory 需要确定性脱敏并减少日志
- **状态**：OPEN｜priority/p2｜area/security｜评论 5
- **要点**：Auto Memory 会把本地 transcript 内容发送给后台提取代理，虽然提示词要求模型脱敏，但敏感内容已先进入模型上下文；服务端还会记录 existing skill 等日志。
- **为什么重要**：涉及隐私与密钥泄露风险，是安全方向的重点跟踪项。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/26525

### ⑧ #21983 browser subagent 在 Wayland 下失败
- **状态**：OPEN｜priority/p1｜评论 4｜👍 1
- **要点**：Wayland 环境下 browser subagent 失败，尽管终止原因显示为 GOAL。
- **为什么重要**：Linux 桌面用户的关键路径兼容问题，且同样存在终止原因误报。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/21983

### ⑨ #24246 工具数超过 128 个时触发 400 错误
- **状态**：OPEN｜priority/p2｜评论 3
- **要点**：启用工具较多时 Gemini CLI 返回 400 错误，期望 agent 能更智能地限制工具范围。
- **为什么重要**：随着 MCP 和扩展生态增长，工具数量膨胀是必然趋势，需要系统级治理。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/24246

### ⑩ #21335 `/compress` 在会话恢复后不持久
- **状态**：OPEN｜priority/p2｜评论 2｜👍 2
- **要点**：`/compress` 仅在内存中替换历史，未写回磁盘 session 文件，恢复会话后摘要丢失。
- **为什么重要**：直接影响 token 节省效果与长会话体验，是用户可感知的上下文管理缺陷。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/21335

---

## 4. 重要 PR 进展（精选 10 条）

### ① #29367 保留子代理恢复时的原始终止原因，防止假 GOAL 成功
- **状态**：OPEN｜priority/p1｜area/agent
- **内容**：修复 `LocalAgentExecutor` 恢复路径无条件覆盖 `terminateReason` 的问题，直接回应 `#22323`。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/29367

### ② #29366 会话恢复时不再重复回放工具响应
- **状态**：OPEN｜priority/p1｜area/core
- **内容**：使用 `-r`、会话浏览器或 ACP 恢复会话时，每个工具结果会被发送两次，导致首个请求在检查 functionCall/functionResponse 配对的后端上失败；同时修复重复写入 recording 的问题。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/29366

### ③ #29378 关闭 diff 标签时保留终端焦点（VS Code Companion）
- **状态**：OPEN｜priority/p1｜area/extensions
- **内容**：调用 `tabGroups.close` 时传入 `preserveFocus`，避免关闭 diff 预览后焦点被编辑器组抢走，提升多文件编辑流畅度。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/29378

### ④ #29379 同步 ConPTY 进程退出生命周期并加固 PTY 输出收尾
- **状态**：OPEN｜priority/p1｜area/core
- **内容**：改善 Windows ConPTY 环境下 `ShellExecutionService` 的进程生命周期确定性与流完成一致性。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/29379

### ⑤ #29368 即使无可恢复内容也按 ID 解析 `session/load`
- **状态**：OPEN｜priority/p1｜area/non-interactive
- **内容**：修复 ACP 会话加载路径，解决 `#29288` 中会话文件存在但加载失败的问题。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/29368

### ⑥ #29343 抑制请求取消时的未捕获 AbortError
- **状态**：OPEN｜size/m｜size/l
- **内容**：修复 Node 23+ 下用户取消查询/流时，EventTarget 监听器中同步抛出的 `AbortError` 导致硬崩溃的问题。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/29343

### ⑦ #29380 改进终端缓冲区内存管理与 Windows 诊断路径格式
- **状态**：OPEN｜size/l
- **内容**：优化 PTY shell 执行与 headless 终端缓冲区序列化的内存占用，并改进 `/bug`、`/bug-memory` 中 Windows 路径的 Markdown 格式。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/29380

### ⑧ #29339 刷新时保留 OAuth refresh token，并使凭证删除幂等
- **状态**：CLOSED｜priority/p1｜area/core
- **内容**：修复 Google OAuth 凭证刷新后丢失 `refresh_token`、导致用户陷入重复认证错误循环的问题（GH-21691）。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/29339

### ⑨ #29304 截断时避免拆分 UTF-16 代理对
- **状态**：OPEN｜area/core
- **内容**：修复 `sanitizeForDisplay` 在截断边界落在 emoji 中间时产生孤立代理项、导致 emoji 静默丢失的问题。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/29304

### ⑩ #29377 更新认证错误文档链接并增加 fallback
- **状态**：OPEN｜priority/p1｜area/core
- **内容**：将 GCP 认证错误文档链接指向正确的 `#set-gcp` 锚点，并保留向后兼容 fallback。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/29377

> 另有若干文档修正 PR 同日更新，包括 `#29374`（extensions 设置类别）、`#29373`（HookDecision 的 ask/approve 值）、`#29372`（环境变量脱敏键名）、`#29371`（ACP flag 参考），显示社区正在集中清理文档与 schema 不一致问题。

---

## 5. 功能需求趋势

从过去 24 小时更新的 Issues 与 PR 中，可以提炼出以下社区关注方向：

1. **子代理与 Agent 可靠性**  
   挂起、误报成功、终止原因不透明、浏览器代理配置失效等问题密集出现，说明 agent 编排层是当前最大的稳定性瓶颈。

2. **终端与 Shell 执行体验**  
   PTY/ConPTY 生命周期、交互式提示卡死、终端 resize 闪烁、等待输入误判等，是跨平台高频问题。

3. **上下文与 Token 效率**  
   AST 感知读取、Tactful Extraction、`/compress` 持久化、工具数量上限治理等需求，反映大代码库场景下的成本与上下文压力。

4. **安全与沙箱**  
   零依赖 OS 沙箱、Auto Memory 确定性脱敏、破坏性命令防护、After-execution 意图路由，安全正从“提示词约束”走向“机制约束”。

5. **IDE / 编辑器集成**

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-09-18）

数据来源：github.com/MoonshotAI/kimi-cli  
统计范围：过去 24 小时内更新内容  
**数据边界说明**：过去 24 小时无新 Releases；仅 3 条 Issue 更新、1 条 PR 更新。因此无法按常规数量挑选 10 条 Issue/PR，以下为全部可分析条目。

---

## 1. 今日速览

过去 24 小时 Kimi Code CLI 无新版本发布。社区动态集中在两处：Kimi Desktop「梦境记忆」开关不写入本地配置，疑似服务端功能门控未放行；子代理启动因 OAuth token 获取超时出现间歇性失败。另有一项长期 `@` 自动补全缺失文件 Issue 关闭，以及一条阻止重复工具调用循环的 PR 提交。

---

## 2. 版本发布

过去 24 小时无新 Releases。

---

## 3. 社区热点 Issues

> 过去 24 小时内仅 3 条 Issue 更新，以下为全部条目。

### 1. #2649 [OPEN] [Bug][Kimi Desktop] “chat 记忆 / 梦境记忆”开关拨动后不写入配置；疑似服务端功能门控未放行
- **作者**：@GH-Mason  
- **创建/更新**：2026-09-17  
- **评论**：2 | 👍：0  
- **为什么重要**：Kimi Desktop 3.2.9 中「梦境记忆」开关可正常拨动，但本地 `daimon/config.json` 未写入 `features.memory`、`features.memory.dream`、`runtime.dream.autoTrigger` 等配置。用户设置无法持久化，且疑似服务端功能门控未放行，直接影响会员功能体验与桌面端记忆能力。
- **社区反应**：已有 2 条评论，讨论可能集中在复现路径与服务端门控排查。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2649

### 2. #2650 [OPEN] [Bug] Intermittent subagent launch failure: OAuth token fetch to auth.kimi.ai times out
- **作者**：@genhoi  
- **创建/更新**：2026-09-17  
- **评论**：0 | 👍：0  
- **为什么重要**：子代理启动间歇性失败，原因是向 `auth.kimi.ai` 获取 OAuth token 超时；主会话正常且用户已认证，重试后可能成功。该问题说明认证端点瞬时抖动会直接中断子代理 spawn，影响多代理/子任务工作流稳定性。
- **社区反应**：暂无评论，但属于高优先级运行时稳定性问题。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2650

### 3. #1276 [CLOSED] [bug] `@` is missing files in autocomplete
- **作者**：@hongquan  
- **创建**：2026-02-27 | **更新**：2026-09-17  
- **评论**：2 | 👍：0  
- **为什么重要**：Kimi Code CLI 1.16.0 在 Linux 上使用 `@` 自动补全时缺失文件，环境为 kimi-k2.5。该问题从 2 月持续至 9 月后关闭，可能已修复或确认重复。文件引用是 CLI 高频操作，补全缺失会显著影响日常开发体验。
- **社区反应**：2 条评论，无点赞，属于长期遗留问题关闭。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/1276

---

## 4. 重要 PR 进展

> 过去 24 小时内仅 1 条 PR 更新，以下为全部条目。

### 1. #2651 [OPEN] fix: stop repeated tool-call loops
- **作者**：@Oxygen56  
- **创建/更新**：2026-09-17  
- **相关内容**：关联 Issue #2637  
- **功能/修复内容**：将重复相同工具调用的守卫改为“硬停止”。达到重复上限后，不再执行最后一次重复调用。此前运行时虽在达到上限时设置停止标志，但仍会执行该次重复调用，之后才停止。该修复可避免工具调用循环浪费 token、时间与执行资源。
- **为什么重要**：直接改善 Agent 工具调用稳定性，减少无限循环和重复执行，属于运行时核心可靠性修复。
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2651

---

## 5. 功能需求趋势

基于本期全部 Issue 更新，可提炼出以下方向：

1. **桌面端记忆功能与配置持久化**  
   「梦境记忆」开关需要可靠写入本地配置，并保持与服务端功能门控一致。

2. **子代理与多代理稳定性**  
   OAuth token 获取超时不应直接导致子代理启动失败，社区期望重试、超时预算或降级机制。

3. **CLI 文件引用与自动补全体验**  
   `@` 自动补全缺失文件问题长期存在后关闭，说明文件选择、路径补全仍是 CLI 高频体验关注点。

4. **工具调用循环防护与 Agent 执行可靠性**  
   PR #2651 针对重复工具调用循环进行硬停止，反映社区对 Agent 执行安全性和资源消耗的高度关注。

---

## 6. 开发者关注点

- **配置不落盘 / 功能门控不一致**：UI 开关与服务端门控、本地配置不同步，导致用户误以为设置已生效。
- **认证端点瞬态故障**：`auth.kimi.ai` 超时导致子代理启动失败，需要更健壮的重试与容错策略。
- **工具调用去重与循环终止**：达到重复上限后应立即停止，而不是多执行一次重复调用。
- **长期 Bug 的修复周期**：`@` 自动补全缺失文件问题持续数月后关闭，说明部分平台/版本兼容问题修复周期较长。
- **数据量限制下的趋势判断**：本期可分析样本较少，以上趋势需结合后续 Issue/PR 持续观察。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报（2026-09-18）

数据来源：[github.com/anomalyco/opencode](https://github.com/anomalyco/opencode)

## 1. 今日速览

过去 24 小时无新 Release，社区焦点集中在**免费层鉴权/配额故障**：大量用户报告使用官方 Desktop、macOS App 或第三方前端时，免费模型被错误拒绝，提示 “OpenCode's free tier can only be used from within OpenCode”。同时，Muse Spark 1.3 免费模型的 `encrypted_content` 报错、自动压缩失败、1.18.30 回归崩溃、Windows ARM64 TUI 初始化失败等问题仍在持续发酵。PR 侧以自动化清理和功能合并为主，插件生态、notebook memory、i18n、MCP structured content、无认证 serve 等方向有进展。

## 2. 版本发布

过去 24 小时无新 Releases。

## 3. 社区热点 Issues

1. **[#35149] “Insufficient Balance” error when executing free models (opencode/big-pickle) on OpenCode Zen**  
   状态：CLOSED｜44 评论｜20 👍  
   链接：https://github.com/anomalyco/opencode/issues/35149  
   重要性：免费模型被 CLI 硬阻断，涉及 OpenCode Zen 上游 token 路由管线，属于核心可用性问题。社区讨论极热烈，高赞说明影响面广。

2. **[#49580] Free tier (Muse Spark 1.3 Free) fails with 'can only be used from within OpenCode' when using MonoCode frontend with OpenCode backend**  
   状态：OPEN｜27 评论｜1 👍  
   链接：https://github.com/anomalyco/opencode/issues/49580  
   重要性：第三方前端 MonoCode 搭配 OpenCode 后端时，免费层被误判为“不在 OpenCode 内”。这直接影响生态集成和开放后端定位。

3. **[#49433] Error from provider (Console): OpenCode's free tier can only be used from within OpenCode**  
   状态：OPEN｜25 评论｜4 👍  
   链接：https://github.com/anomalyco/opencode/issues/49433  
   重要性：任意模型均触发该错误，说明不是单模型问题，而是免费层来源校验或 Console provider 鉴权逻辑出现系统性故障。

4. **[#19130] Windows ARM64 native: OpenTUI fails to initialize with bun:ffi dlopen TinyCC error**  
   状态：OPEN｜25 评论｜13 👍  
   链接：https://github.com/anomalyco/opencode/issues/19130  
   重要性：Windows 11 ARM64 原生二进制可运行非交互命令，但 TUI 无法初始化。平台原生支持是长期痛点，13 👍 表明 ARM64 用户关注度高。

5. **[#39845] DeepSeek V4 Flash suddenly requires "Enable models hosted in China" for OpenCode Go subscription**  
   状态：OPEN｜24 评论｜30 👍  
   链接：https://github.com/anomalyco/opencode/issues/39845  
   重要性：会话中途突然要求中国托管模型 opt-in，涉及区域合规、订阅可用性和模型路由策略。30 👍 为今日最高，说明该问题争议或影响很大。

6. **[#48645] Regression in 1.18.30: every prompt crashes with TypeError in SystemPrompt.environment ("a.name") — 1.18.18 works fine**  
   状态：OPEN｜10 评论｜17 👍  
   链接：https://github.com/anomalyco/opencode/issues/48645  
   重要性：新版本导致每个 prompt 立即失败，属于严重回归。高赞说明用户强烈希望尽快修复或回滚。

7. **[#49587] Auto-compaction fails with "OpenCode's free tier can only be used from within OpenCode" on OpenCode Zen**  
   状态：

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 · 2026-09-18

## 今日速览

Qwen Code Desktop v0.24.0 正式发布，nightly 版本继续迭代，ACP 权限队列与 channels 输出模式是本次交付重点。社区侧，React 渲染崩溃（error #185）和工具调度器被意外替换等 P1/P2 级稳定性问题集中爆发，同时围绕上下文预算、会话生命周期与沙箱执行的讨论持续升温。PR 侧则聚焦于 Linux bwrap 沙箱基础、子代理容器执行、MCP 内容保留等底层能力建设，以及大量 CI 稳定性补丁。

---

## 版本发布

### desktop-v0.24.0（正式版）
- `fix(cli): scope the ACP permission queue to the session` — ACP 权限队列按会话隔离，避免跨会话串扰（#11802）
- `feat(channels): add shared output modes` — 新增共享输出模式，统一多通道输出行为

### v0.24.0-nightly.20260917.f822124af5（nightly）
- `docs(serve): record merged ACP boundary acceptance`（#12024）
- `fix(ci): wait for the published export re...` — 发布导出重试相关 CI 修复

---

## 社区热点 Issues

1. **#9278 [OPEN] `/review` 发布时收敛建议设计（10 评论，最热）**
   完整记录 `/review` 的"失控回路"问题：push → 评审 → 修复 → diff 变大 → 更多 finding，回路增益 > 1，唯一阻尼只是 AGENTS.md 里一句 prose。这是评审机制自我膨胀的根因设计讨论，值得关注其后续 telemetry 与 operator 侧投放面设计。
   https://github.com/QwenLM/qwen-code/issues/9278

2. **#11732 [CLOSED] 0.23.3 长任务运行时崩溃 React error #185（P1，8 评论）**
   native monitor 长时间任务的场景下出现未捕获的 React 错误，两次独立会话复现同一失败模式。已关闭，但同类问题 #11783 仍在追踪，说明渲染层稳定性仍是焦点。
   https://github.com/QwenLM/qwen-code/issues/11732

3. **#12061 [OPEN] 回调标识变化替换活跃 tool scheduler（P2，8 评论）**
   `useReactToolScheduler` 在调用方回调标识变化时会重建 `CoreToolScheduler`，导致仍持有 active batch 的调度器被替换，工具状态更新可能丢失。这是当日新报的核心并发/渲染交织 bug。
   https://github.com/QwenLM/qwen-code/issues/12061

4. **#8138 [OPEN] worktree 场景 settings.json 写入错误位置（P2，7 评论）**
   在 git worktree 内保存设置时，写到了全局/项目根的 `.qwen/settings.json`，而非 worktree 自身的 `.qwen/`。长期未决的配置隔离问题，影响多 worktree 并行开发体验。
   https://github.com/QwenLM/qwen-code/issues/8138

5. **#12053 [OPEN] 精简 Goal runtime：用当前轮证据判定完成（7 评论）**
   实测两个 `/goal-draft` 会话各在约 100 次工具调用的单个 Goal 轮次内完成目标，随后的 evidence catalog 与 checkpoints 成为多余开销。属上下文性能路线（#12028）的一部分。
   https://github.com/QwenLM/qwen-code/issues/12053

6. **#11956 [OPEN] 无参数工具 `parameters` 被序列化为 null，严格网关拒绝请求（6 评论）**
   参数为空的工具其 `parameters` 字段被判为 `null`，严格 OpenAI 兼容网关因此拒绝整个请求。典型的协议兼容性问题，影响自建代理用户。
   https://github.com/QwenLM/qwen-code/issues/11956

7. **#10689 [OPEN] kimi-k3 经 OpenAI 兼容代理反复 malformed tool call（P1，6 评论）**
   长会话（transcript ~1.6 MB）下 prompt 轮次稳定失败："Model response contained a malformed tool call"，5 次重试耗尽。涉及第三方厂商模型接入与长上下文稳定性。
   https://github.com/QwenLM/qwen-code/issues/10689

8. **#8622 [CLOSED] 0.21.6 回归：多数 hooks 事件不再分发（P1，6 评论）**
   `PreToolUse`/`PostToolUse`/`PreCompact`/`SessionStart` 均不触发，仅 `UserPromptSubmit` 和 `Stop` 生效，而 0.21.5 正常。影响 hooks 生态与自动化扩展，已关闭但影响面广。
   https://github.com/QwenLM/qwen-code/issues/8622

9. **#12113 [OPEN] ACP 在 finish_reason=length 后仍上报 end_turn（P2，5 评论）**
   使用官方 npm 包 0.24.0，`qwen --acp` 客户端即使响应因输出 token 限制被截断，仍收到 `stopReason: "end_turn"`，且无模型/IDE 也能复现。直接影响 IDE 集成的截断处理正确性。
   https://github.com/QwenLM/qwen-code/issues/12113

10. **#12091 [OPEN] 删除活跃会话会 unlink transcript，写者重建导致会话永久损坏（P1，4 评论）**
    `sessions/delete` 对仍在运行的会话删除 `chats/<id>.jsonl`，附着的 writer 继续重建并追加，首条记录 `parentUuid` 指向不存在的父节点，导致 degraded_history 且自动续跑被禁用。会话管理路线上的高风险缺陷。
    https://github.com/QwenLM/qwen-code/issues/12091

> 其他值得留意：#11851（`isAsyncOperator` 安全边界，P1）、#10887（重复工具错误无早期终止，5–14M token 燃烧）、#11783（TUI React #185）、#11817（Windows 下 loop-guard 测试确定性失败）、#12072（OpenRouter 预设头名错误）、#12048/#12029/#12030/#12033（上下文预算与遥测系列）。

---

## 重要 PR 进展

1. **#12067 [OPEN] `feat(core): Add the bwrap execution foundation`**
   为计划中的工具级 Linux 沙箱打底：结构化 executable/argv/environment 启动、带可信完成证据的 bwrap 适配器、进程监督与受限二进制 worker。沙箱能力的基石 PR。
   https://github.com/QwenLM/qwen-code/pull/12067

2. **#11711 [OPEN] `feat(core): add container execution for subagents`**
   Unix 主机上为普通子代理启用容器执行，操作者可通过 `QWEN_AGENT_EXECUTION_BACKEND=docker|podman` 强制；项目环境文件与设置无法覆盖该操作者级约束。
   https://github.com/QwenLM/qwen-code/pull/11711

3. **#12131 [OPEN] `fix(core): keep MCP App html in recorded transcripts so replay can render`**
   MCP App 工具结果现在保留 `html` 与 `toolResult`（在保留预算内），使保存的会话可回放 App 的沙箱 iframe，终端历史路径仍按原样丢弃。
   https://github.com/QwenLM/qwen-code/pull/12131

4. **#10835 [OPEN] `fix(core): bound oversized images returned by MCP tools`**
   将来自 MCP 工具的图片纳入与磁盘读图相同的视觉预算，截图开销不再因入口不同而不同；已符合预算的图片原样转发。
   https://github.com/QwenLM/qwen-code/pull/10835

5. **#12050 [OPEN] `feat(web-shell): expose slash-command exports as artifacts`**
   使 `/export md|html|json|jsonl` 输出在 Web Shell 中作为 turn artifacts 暴露，带预览与下载控件，且 artifact 引用可跨会话历史回放。
   https://github.com/QwenLM/qwen-code/pull/12050

6. **#12007 [OPEN] `fix(core): stop session recovery from flagging unanswered notifications`**
   修复会话恢复分类器把"已记录但未应答"的后台通知误判为中断轮次的问题，并阻止 daemon 在自动轮次运行时弹出"继续执行"。
   https://github.com/QwenLM/qwen-code/pull/12007

7. **#11988 [OPEN] `fix(core): strip reasoning blocks closed with native think tags in compaction`**
   自动压缩不再因模型用原生 think 标签闭合推理块而丢弃总结，sanitizer 现识别 `think` 等实际标签。
   https://github.com/QwenLM/qwen-code/pull/11988

8. **#11865 [OPEN] `fix(core): treat only space/tab/newline as word separators in isAsyncOperator`**
   修复安全边界类问题：`/\s/` 曾把 `\r`/`\v`/`\f`/`\u00a0` 当作 bash 分隔符，可能让 Bash allow 规则覆盖第二条命令（对应 #11851）。
   https://github.com/QwenLM/qwen-code/pull/11865

9. **#11684 [OPEN] `fix(core): keep reasoning and function_call items adjacent through Responses cleanup`**
   Responses 请求管线在清理历史时，把回放的 reasoning 项与其紧随的并行工具调用组视为一个整体，避免孤立清理破坏上下文。
   https://github.com/QwenLM/qwen-code/pull/11684

10. **#12115 [OPEN] `fix(installer): preflight glibc for standalone Linux archives`**
   在 CentOS 7 等老发行版上，安装前预检 glibc，避免下载安装后因内置 Node.js 22 无法启动而出现 `GLIBC_*` 符号缺失的运行时失败。
    https://github.com/QwenLM/qwen-code/pull/12115

> CI 稳定性补丁密集出现：#12128（E2E artifact 下载单次重试）、#11989（未启动 job 重跑而非逐 commit 建 issue）、#11134（macOS E2E shard 死亡重试）、#11297（E2E checkout 重试）。

---

## 功能需求趋势

- **上下文与性能治理（最密集方向）**：#12028 系列衍生出 #12029（百分比预算随窗口放大失效）、#12030（扩展 context 文件无门控常驻）、#12033（`/context` 分类明细不闭合）、#12048（遥测令牌估算器混用）、#12053（Goal runtime 精简），反映项目正系统性重构长上下文预算与归因。
- **IDE / 协议集成**：ACP 相关讨论活跃（#12113 的 end_turn、#11361 的 AskUserQuestion 在 Zed 显示 Raw Input），VSCode 侧 #12059 继续跟进远程 webview 失败模式，OpenRouter 预设头名 #12072 属第三方路由兼容。
- **沙箱与安全执行**：bwrap 基础（#12067）与子代理容器执行（#11711）并行推进，配合权限解析安全修复 #11851/#11865，显示"可信操作者强制隔离"正成为核心能力。
- **MCP 生态完善**：#10369（MCP Apps 内联 UI 在 Web Shell 不渲染）长期存在，#12131/#10835 从 transcript 保留与图片预算两侧补齐 MCP 内容处理。
- **会话生命周期与恢复**：#12091（删除活跃会话损坏 transcript）、#12007（恢复误判）、`sessions/delete` 语义是近期主线。
- **多模型/网关兼容性**：#11956（null parameters）、

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*