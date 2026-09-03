# AI CLI 工具社区动态日报 2026-09-04

> 生成时间: 2026-09-03 22:36 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-09-04）

> 数据来自 2026-09-04 各官方 GitHub 动态。GitHub Copilot CLI、Kimi Code CLI、Qwen Code CLI 当日未提供有效动态数据，以下对比仅基于已有材料，并在相应位置标注“无数据”。

---

## 1. 生态全景

AI CLI 工具正在从“能写代码”的辅助角色，演进为涉及模型路由、沙箱安全、上下文压缩、MCP 协议、会话生命周期管理的系统级 Agent 平台。当日动态中，OpenAI Codex 以密集发版和 GPT-6-Astra 预热领跑迭代节奏；Claude Code 无新 Release，社区集中于 Windows 桌面体验与 stale issue 清理；OpenCode 在多 Provider 接入、模型目录同步、性能回归之间承压；Gemini CLI 则明显处于 Agent 可靠性与安全边界攻坚期。整体看，社区的关注重心已从“模型生成能力”转向“长期运行后的稳定性、可控性与安全治理”。

---

## 2. 各工具活跃度对比

| 工具 | Issues 更新 | PR 更新 | Release / 版本 |
|---|---|---|---|
| Claude Code | 50 条 | 5 条（

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---

# Claude Code 社区动态日报 — 2026-09-04

## 今日速览

过去 24 小时无新版本发布，社区讨论热度集中在 Windows 平台体验问题上——尤其是 Claude Desktop 窗口置顶 Bug（#85891，74 条评论、166 👍），该 Issue 仍是当前最受关注的未解决问题。此外，大量 7 月提交的中低热度 Issue 在昨日被批量标记 `stale` 并关闭，仅 2 个 Issue 保持 OPEN 状态；PR 侧有 5 条更新，其中 2 条直指 plugin-dev validator 脚本同一处 `set -e` 缺陷。

## 社区热点 Issues

过去 24 小时共更新 50 条 Issue，以下为最受关注或最具代表性的 10 条。

**1. Windows 11：Claude Desktop 主窗口始终置顶且无法关闭**
[#85891](https://github.com/anthropics/claude-code/issues/85891) | OPEN | 评论 74 | 👍 166
Claude Desktop 在 Windows 11 上表现为 topmost 窗口，即使用户切换到其他应用，主窗口仍绘制在最上层，且无设置项可关闭。此为 macOS 对应问题 #66516 的 Windows 版本。74 条评论与 166 个赞表明该问题影响面广泛，是当前社区呼声最高的未解决 Bug。

**2. 功能请求：git worktree 池应改为 opt-out——每个会话一个 worktree，归档时才释放**
[#91472](https://github.com/anthropics/claude-code/issues/91472) | OPEN | 评论 1 | 👍 1
提出者为避免并行会话共享 worktree 导致的混乱，建议将当前 worktree 复用/池化策略改为默认一个会话独占一个 worktree、会话归档后才释放。这是 9 月 2 日新提交的 feature request，仍处于讨论早期。

**3. Intel Mac + AMD dGPU 重度并行使用 Claude Code CLI 导致内核崩溃**
[#74805](https://github.com/anthropics/claude-code/issues/74805) | CLOSED（stale）| 评论 4
16 英寸 MacBook Pro 2019（i9-9980HK + Radeon Pro 5500M）在重度并行 CLI 使用时触发 WindowServer watchdog 超时并内核崩溃。属于系统级稳定性问题，虽然已被 stale 机器人关闭，但值得 Intel Mac 用户留意。

**4. Opus 4.8（1M 上下文）反复产生不可用的助手输出**
[#68352](https://github.com/anthropics/claude-code/issues/68352) | CLOSED（stale）| 评论 3
单次 Claude Code 会话中每次失败的 turn 都输出扩展格式异常内容。1M 上下文模型的质量问题反馈较少见，可能与超长上下文的处理缺陷有关。

**5. Remote Control 环境生命周期缺陷：过期环境无法区分/无法移除**
[#76811](https://github.com/anthropics/claude-code/issues/76811) | CLOSED（stale）| 评论 3 | 👍 2
每次启动 `claude remote-control` 服务器都会注册新环境，旧环境堆积后无法清理且与活跃环境无法区分，影响 claude.ai/code 及 Android App 端的环境选择器体验。

**6. Windows 下 MCP stdio 服务启动时闪现控制台窗口**
[#79219](https://github.com/anthropics/claude-code/issues/79219) | CLOSED（stale）| 评论 3
Windows 平台上以 `node` 启动的 stdio MCP server 每次（重）启动都会闪现 conhost.exe 控制台窗口，疑似子进程 spawn 未设置 `windowsHide`。影响所有基于 Node 的 MCP 服务使用者。

**7. Sidebar：归档会话无法拖入分组，快捷键加速键无效**
[#79519](https://github.com/anthropics/claude-code/issues/79519) | CLOSED（stale）| 评论 2
桌面端 sidebar 中，已归档的会话无法通过拖拽归入自定义分组；右键菜单的键盘加速键也不生效，批量整理会话时非常痛苦。

**8. `disable-model-invocation` skills 在 GrowthBook 开关关闭时完全不可见**
[#77740](https://github.com/anthropics/claude-code/issues/77740) | CLOSED（stale）| 评论 2 | 👍 2
SKILL.md 中声明 `disable-model-invocation: true` 的用户级技能本应只是禁止模型自动调用，实际却从模型可见的所有列表中被彻底移除。当 skills-dashboard 的 GrowthBook flag 关闭时，即使用户手动调用也找不到这些技能。

**9. MCP Streamable HTTP 的 `tools/list_changed` 通知在 2.1.211 中被忽略**
[#78208](https://github.com/anthropics/claude-code/issues/78208) | CLOSED（stale）| 评论 2
2.1.211 版本回归：MCP server 通过 Streamable HTTP 发送 `notifications/tools/list_changed` 后，CLI 不刷新工具列表，而 2.1.210 工作正常。工具变更在长会话中不会被感知。

**10. Windows：每次 Bash/PowerShell 工具调用都弹出控制台窗口并抢占焦点**
[#73901](https://github.com/anthropics/claude-code/issues/73901) | CLOSED（stale）| 评论 2 | 👍 1
即使是由后台计划任务触发的工具调用，也会弹出可见的 `powershell.exe` 窗口并抢夺当前焦点，对日常使用干扰很大。与 #79219 同属 Windows 子进程窗口可见性问题。

> **说明**：上述 Issue 多数虽已因长期无响应被标记 `stale` 关闭，但问题本身并未解决。社区可考虑为主观上仍然存在的 Issue 补充新信息以触发重新开启（如 #85891）。

## 重要 PR 进展

过去 24 小时共更新 5 条 PR（1 条已关闭，4 条开放），以下全部列出：

**1. [CLOSED] 更新 /frontend-design SKILL.md**
[#91894](https://github.com/anthropics/claude-code/pull/91894) | @ant-kurt | 已关闭
对 frontend-design 技能的文档性更新，已于 9 月 3 日关闭，无实质性代码变更。

**2. [OPEN] docs：将 code-review README 与当前基于校验的命令对齐**
[#79150](https://github.com/anthropics/claude-code/pull/79150) | @Codeturion
该 PR 修复文档与技术现状脱节的问题：README 中描述的 git blame/history 流程、0–100 置信度评分及 80 分阈值在实际命令中已不存在，且指导用户编辑的 "Filter out any issues with a score less than 80." 配置行根本不存在，需要修正以免误导。

**3. [OPEN] fix(security-guidance)：使 ** glob 模式可匹配零深度路径**
[#87079](https://github.com/anthropics/claude-code/pull/87079) | @anishsamant
安全相关的关键修复：`glob_match` 委托给 `fnmatch` 后，裸 `*` 已可跨 `/` 匹配，导致 `**/*.ts` 需要一个字面 `/`，从而使 security-patterns.json 规则静默漏掉顶层文件。由于这是安全规则，漏检是静默的，风险更高。

**4. [OPEN] validate-agent.sh：不要在第一个警告时中止（set -e 交互 + 计数器），并停止误报合法 agent**
[#89404](https://github.com/anthropics/claude-code/pull/89404) | @bcherny
修复公开 issue #83803。plugin-dev 的 `validate-agent.sh` 在自己的示例 agent 文件上验证失败，根因是 `set -euo pipefail` 下 `((warning_count++))` 在值为 0 时求值返回非零退出码，导致脚本在第一个警告处即中止。另修复了对合法 agent 文件的误报问题。

**5. [OPEN] fix(plugin-dev)：validator 脚本因

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-09-04

## 今日速览

今日核心动态围绕 **GPT-6-Astra 模型的预热布局**展开——0.153.1 补丁通过 API 方式隐藏接入该模型，且同日合并了内置目录、Amazon Bedrock 目录等多条相关 PR，暗示新一代模型即将正式铺开。修复层面，Vim 模式在 0.153.0 中获得了撤销/重做支持，同时社区对 **桌面端磁盘占用失控（~165 GiB）** 与 **Windows 桌面宠物交互穿透**仍保持高热度关注。

## 版本发布

### rust-v0.153.1
**核心变更**：新增 GPT-6-Astra 模型目录支持，可通过 API 配置而不更改默认模型或出现在模型选择器中（#42605 回传）。

### rust-v0.153.0
**核心变更**：
- Vim 模式支持 `u` 撤销、`Ctrl+R` 重做，保留完整草稿内容（含粘贴内容和附件）
- 插件 CLI 支持列出、安装和移除操作

另有 0.154.0-alpha.1 / alpha.2 和 0.153.0-alpha.5.1 预发布版本产出。

## 社区热点 Issues（10 条）

### 1. 子代理磁盘占用失控
**#34061** [bug, CLI, subagent, performance] — [链接](https://github.com/openai/codex/issues/34061)  
作者 @jezell 报告 Codex CLI 中子代理产生异常磁盘占用，24 条评论成为今日最热 issue。Pro 用户 + macOS 环境下问题尤为突出，社区对该问题的复现和规避策略讨论积极。👍 5

### 2. 截图在每次压缩后重复持久化，会话目录高达 ~165 GiB
**#35458** [bug, context, app, subagent, session] — [链接](https://github.com/openai/codex/issues/35458)  
Desktop 版在每次上下文压缩时将全量截图（base64 图像）重新落盘，且子代理 fork 会继承这些数据，导致 `~/.codex/sessions` 积累至 165 GiB（95% 为图片）。这是磁盘问题的深层根因之一。👍 0（较新）

### 3. Esc-Esc 回溯无法找到已选提示词
**#37421** [bug, TUI, CLI] — [链接](https://github.com/openai/codex/issues/37421)  
CLI 0.147.0 中 Esc-Esc 回溯在持久化线程中找不到已选提示词，影响 TUI 核心交互。以 **44 个 👍** 成为本期社区呼声最高的问题，目前已标记 Closed，修复方向值得追踪。

### 4. 无法切换模型与推理强度
**#17318** [bug, app] — [链接](https://github.com/openai/codex/issues/17318)  
长期未关闭的高赞问题（👍 30），macOS 桌面版在部分会话中无法切换模型与 reasoning efforts，影响实际工作流，社区持续关注。

### 5. Windows Desktop Pet 点击穿透
**#41513** [bug, windows-os, app, pets] — [链接](https://github.com/openai/codex/issues/41513)  
Windows 桌面宠物（内置 Codey 和自定义 Remiel）变成点击穿透状态，无法拖拽。21 条评论中含多个复现确认，是一个高可见度的 Windows 桌面体验问题。👍 8

### 6. 服务端删除的对话在 Recents 中"复活"
**#40219** [bug, app, session] — [链接](https://github.com/openai/codex/issues/40219)  
macOS 上服务器端删除的会话不断重新出现在"最近"列表中，且无法移除。这触及会话同步一致性问题，18 条评论表明相当一部分用户受到影响。👍 15

### 7. app-server 每次 thread/list 全量加载会话文件
**#22411** [enhancement, app-server, performance] — [链接](https://github.com/openai/codex/issues/22411)  
每次 `thread/list` 调用都反序列化全部会话文件，数月后性能灾难性下降，且在后台无感消耗 API tokens。这一性能隐患与 #34061/#35458 的磁盘问题叠加，指向 app-server 架构性瓶颈。

### 8. codex exec 在外部只读沙箱内因 installation_id 写权限失败
**#42398** [bug, sandbox, exec, CLI] — [链接](https://github.com/openai/codex/issues/42398)  
codex exec 置身于只读 sandbox 时，即使 Codex 自身的沙箱已启用，installation_id 解析器仍要求写访问权限从而导致启动失败。影响容器化/CI 只读环境中的嵌入场景。

### 9. 取消的 Code Mode 嵌套工具调用导致 PreToolUse 钩子永久"Running"
**#42511** [bug, TUI, CLI, tool-calls, hooks] — [链接](https://github.com/openai/codex/issues/42511)  
取消 Code Mode 中嵌套工具调用后，PreToolUse 钩子在 TUI 中永久显示"Running"，影响后续交互和钩子执行流。

### 10. Codex 未遵循 MCP tools/list 的 nextCursor 分页
**#28858** [bug, mcp, CLI] — [链接](https://github.com/openai/codex/issues/28858)  
MCP 服务器若通过 `nextCursor` 分页返回工具列表，Codex 只读取第一页，导致工具不完整。对使用大规模 MCP 工具集的用户影响明显。👍 6

## 重要 PR 进展（10 条）

### 1. GPT-6-Astra 模型目录完成多路分发
- **#42607** [内置目录] — [链接](https://github.com/openai/codex/pull/42607)：在 bundled catalog 中添加隐藏的 `gpt-6-astra` 模型定义，含推理级别、工具能力、上下文限制、agent 指令和 review 策略，并重新排序现有模型优先级。
- **#42605** [回传 0.153] — [链接](https://github.com/openai/codex/pull/42605)：为 0.153.1 热修复回传目录更新，确保发布线一致。
- **#42619** [Amazon Bedrock] — [链接](https://github.com/openai/codex/pull/42619)：同步将 `openai.gpt-6-astra` 加入 Bedrock 目录，并包含全球/US 跨区域变体。

三条 PR 联动表明 GPT-6-Astra 正在多个渠道同步铺开，且当前被设计为"隐藏可配置但不出现在选择器中"的灰度策略。

### 2. 强化 macOS 沙箱防终端输入注入
**#42590** — [链接](https://github.com/openai/codex/pull/42590)  
沙箱子进程继承了用户控制终端，恶意子进程可利用 `TIOCSTI` 向 Codex 退出后恢复的非沙箱 shell 注入输入。PR 追加 `file-ioctl` 限制以封堵该攻击面，属于安全加固类更新。

### 3. 修复 Vim 模式在旧终端中的 Esc 输入竞争
**#42584** — [链接](https://github.com/openai/codex/pull/42584)  
旧终端将 `Alt+字符` 与 `Esc 后跟字符` 编码为相同序列，导致 Vim 插入/替换模式下按 Esc 后立即输入命令时 composer 状态错乱。通过恢复算法判断意图（与 0.153.0 的撤销/重做互补，完善 Vim 体验）。

### 4. MCP 服务器状态增加工具发现错误上报
**#42598** — [链接](https://github.com/openai/codex/pull/42598)  
空的工具映射无法区分"正常返回空目录"与"服务启动/发现失败"。新增可空 `toolsError` 字段，使 `mcpServerStatus/list` 能明确暴露失败状态，提升 MCP 排障能力。

### 5. 保留 MCP 工具调用的认证挑战
**#42552** — [链接](https://github.com/openai/codex/pull/42552)  
静默 OAuth 刷新失败后，调用方需要原始认证挑战来发起交互式登录，且禁止在刷新失败后自动重放被拒绝的调用。修复 MCP 工具调用在认证过期场景下的死循环和静默失败问题。

### 6. 记录 Windows 沙箱私有桌面使用指标
**#42596** — [链接](https://github.com/openai/codex/pull/42596)  
为 Windows restricted-token 沙箱执行新增 `private_desktop` 计数器，按是否启用私有桌面隔离打标签——为 Windows 沙箱行为分析提供可观测性基础。

### 7. 本地插件安装后自动重载用户配置
**#42593** — [链接](https://github.com/openai/codex/pull/42593)  
此前安装本地插件后，已加载线程保留旧配置，导致插件自带的 MCP 服务器与待生效的用户配置更改无法在当前会话中启用。此 PR 在插件安装后即时重载用户配置。

### 8. 压缩 TUI 启动警告输出
**#42609** — [链接](https://github.com/openai/codex/pull/42609)  
将配置、技能、沙箱和 MCP 等启动诊断合并为会话头部下方单条摘要（包含 MCP/登录计数），完整文本保留在 transcript 中。改善启动信息过载。

### 9. 通过 app-server API 暴露线程发起者
**#42458** — [链接](https://github.com/openai/codex/pull/42458)  
在线程响应和 `thread/started` 通知中新增创建时的 `originator` 字段，持久化至线程元数据并在 list/read/resume/rollout/SQLite 全链路保留首次记录值，为多端协作提供来源追溯。

### 10. 以 exec server 初始化超时约束 Noise 握手
**#42623** — [链接](https://github.com/openai/codex/pull/42623)  
将鉴权 Noise 握手纳入 exec server 初始化超时窗口管理，先完成握手再发送 JSON-RPC `initialize`，共享超时配置。防止握手阶段无限阻塞，健壮性修复。

## 功能需求趋势

从近 24 小时更新的 Issues（共 50 条）可提炼出以下社区关注方向：

1. **新模型支持与模型灵活度**：GPT-6-Astra 的灰度接入 + 用户对模型版本回退/切换能力的持续诉求（#17318、#25917 "Bring back model 5.3"）表明，在模型快速迭代中社区对**可控性和可选择性**的需求在上升。

2. **上下文压缩/持久化的正确性**：压缩后截图重新落盘（#35458）、压缩后线程内部校验错误（#41922）等，直指 compaction 管线的稳定性；配套 PR（#42588、#42579）也体现了对该链路的系统性加固。

3. **MCP 生态深化**：从工具分页（#28858）、认证挑战保留（#18527、#30460、#42552）到发现错误上报（#42598），MCP 已从"能不能连"进入"大规模、复杂认证下可不可靠"的阶段。

4. **沙箱与安全加固**：macOS 终端注入封堵、只读沙箱兼容性（#42398）、Windows 沙箱可观测性——同时覆盖安全攻防与 CI 嵌入场景的适配。

5. **Vim 模式的体验补全**：0.153.0 带来 undo/redo，配套的 Esc 输入修复（#42584）说明 TUI 编辑体验仍在精耕细作。

## 开发者关注点

- **磁盘与性能痛点集中爆发**：#34061（子代理磁盘占用）+#35458（165 GiB 截图会话数据）+#22411（list 全量加载）形成"性能三重奏"。开发者对桌面/CLI 长期使用后的资源积累表达了明显不满，这可能是未来几个版本优化的重要方向。

- **窗口/桌面交互可靠性在 Windows 端欠佳**：桌面宠物穿透、远程 SSH 审批按钮无响应（#34652）、paginated 会话重复序号（#41566）、长会话崩溃（#41581），Windows 平台存在一批联动性 UI 缺陷。

- **会话一致性和数据所有权**：服务端已删对话在本地 Recents 中"复活"（#40219，👍 15）引发较多共鸣；上下文压缩后内部验证错误导致聊天不可用（#41922）也被多次点名。

- **自主行为可控性引发讨论**：#36596（模型无视续跑指令主动终止）与 #42017（tool 执行后被替换的 prose 降低可读性）反映出开发者希望更精准地控制 agent 的"何时停、何时说"。

- **钩子与守卫机制进入深水区**：#42511（取消操作导致钩子永久挂起）、Guardian 相关多 PR（#42529、#42579、#42588）表明审查/授权基础设施正快速演进，但带来的边缘情况也需要社区持续反馈打磨。

---

*本日报数据来源：[github.com/openai/codex](https://github.com/openai/codex)，统计窗口为 2026-09-03 至 2026-09-04。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-09-04

> 数据来源：github.com/google-gemini/gemini-cli

## 1. 今日速览

过去 24 小时无新版本 Release，社区焦点集中在 **Agent 可靠性**与**安全边界**上。一方面，多个 P1 级 Bug 仍在持续发酵：generalist agent 挂起、Shell 命令完成后卡死、子代理在 MAX_TURNS 后被误报为“GOAL 成功”；另一方面，一批安全修复 PR 密集推进，包括 checkpoint 路径穿越、Windows 下 git 参数绕过沙箱、硬编码 API Key 清理等。整体来看，项目正处在一轮“查漏补缺”的安全加固与代理稳定性攻坚期。

## 2. 版本发布

过去 24 小时无新版本 Release。

## 3. 社区热点 Issues（10 条）

1. **[P1] Subagent recovery after MAX_TURNS is reported as GOAL success, hiding interruption**
   - [google-gemini/gemini-cli#22323](https://github.com/google-gemini/gemini-cli/issues/22323)
   - 重要原因：`codebase_investigator` 等子代理明明因 MAX_TURNS 被中断，却向主会话上报 `status: "success"` / `Termination Reason: "GOAL"`。这类误导性成功会让用户对任务完成情况产生错误判断，是目前 Agent 可靠性投诉中最具代表性的问题。
   - 社区反应：13 条评论，热度和关注度很高。

2. **[P1] Generalist agent hangs**
   - [google-gemini/gemini-cli#21409](https://github.com/google-gemini/gemini-cli/issues/21409)
   - 重要原因：一旦主代理决定交由 generalist agent 处理，任务就会无限期挂起，用户反馈“等了一个小时”也没有结果。即使是创建文件夹这种简单操作也会触发。社区发现一个 Workaround：在 prompt 中明确禁止使用子代理即可规避。
   - 社区反应：8 条评论、8 个 👍，是近期开发者痛点最集中的 Issue 之一。

3. **[P1] Shell command execution gets stuck with "Waiting input" after command completes**
   - [google-gemini/gemini-cli#25166](https://github.com/google-gemini/gemini-cli/issues/25166)
   - 重要原因：极端简单的 CLI 命令执行完成后，UI 仍显示命令处于活动状态并等待输入。说明伪终端/输入流管理存在缺陷，会显著降低自动化任务的可靠性。
   - 社区反应：4 条评论、3 个 👍，属于高频复现类问题。

4. **[P2] Gemini does not use skills and sub-agents enough**
   - [google-gemini/gemini-cli#21968](https://github.com/google-gemini/gemini-cli/issues/21968)
   - 重要原因：用户自建了 gradle、git 等自定义 skill，期待模型在相关场景自动调用，但实际只有在用户明确指令时才会使用。这反映 Agent 在工具/技能编排上的主动性不足，直接影响 CLI 作为“智能代理”的使用价值。
   - 社区反应：6 条评论，虽无高赞，但共鸣度高。

5. **[P2] Assess the impact of AST-aware file reads, search, and mapping（EPIC）**
   - [google-gemini/gemini-cli#22745](https://github

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>



</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-09-04

## 今日速览

OpenCode 今日无新版本发布，但社区围绕 **Muse Spark 1.3 免费模型在 1.18.27 中集体不可用** 爆发了多起 issue，Zen 模型列表与 CLI 实际返回不一致成为当日最热话题；同时 **CPU 高占用** 的长期 issue 仍在持续发酵（49 条评论），客服与计费相关反馈也十分密集。PR 侧核心维护者正在推进 Snowflake Cortex 原生认证、Copilot 路由修复和 compaction 请求重试等底层完善工作。

## 社区热点 Issues

共 50 条活跃 issue，以下按关注度与影响面精选 10 条：

1. **#30086 新版本 OpenCode CPU 占用率飙升**
   - **评论**: 49 | **👍**: 26 | 状态: OPEN
   - 摘要: 约 7 天前更新后，CPU 占用率大幅上升。过去可同时运行 10 个会话，现在 3 个会话就导致鼠标延迟卡顿。这是当前社区反馈最强烈的性能回归问题。
   - 链接: https://github.com/anomalyco/opencode/issues/30086

2. **#12393 [web] 如何在 opencode-desktop 中取消归档会话**
   - **评论**: 20 | **👍**: 34 | 状态: CLOSED
   - 摘要: 用户在桌面端 v1.1.53 误点了会话归档，找不到恢复入口。虽然是已关闭问题，但 34 个 👍 说明该交互缺失痛点极高。
   - 链接: https://github.com/anomalyco/opencode/issues/12393

3. **#47047 SSE 错误与 #44944 相关——出现死循环**
   - **评论**: 9 | **👍**: 0 | 状态: OPEN
   - 摘要: Big Pickle 模型在生成代码时陷入循环，AI 停顿思考时跳出循环导致编辑错乱，影响 1.18.27 及 1.18.26 两个版本。属于当天新报告的严重模型行为异常。
   - 链接: https://github.com/anomalyco/opencode/issues/47047

4. **#38255 不同用量看板数据严重不一致**
   - **评论**: 11 | **👍**: 0 | 状态: OPEN
   - 摘要: 用户称月度限制看板显示 100% 用量，但细粒度看板显示同期仅消耗约 10 美元，导致所有模型在午夜被错误停用。计费数据可信度问题直接影响用户信任。
   - 链接: https://github.com/anomalyco/opencode/issues/38255

5. **#45278 持续 3 个月的支付卡突然被拒**
   - **评论**: 9 | **👍**: 2 | 状态: OPEN
   - 摘要: 用户使用同一张卡成功支付 3 个月后突然被拒，银行确认卡无问题。续费流程的稳定性疑似存在服务端故障。
   - 链接: https://github.com/anomalyco/opencode/issues/45278

6. **#36280 Worker 子进程因 SIGILL 崩溃导致系统冻结**
   - **评论**: 5 | **👍**: 0 | 状态: OPEN
   - 摘要: 在 Intel i5-7200U (Kaby Lake) 上，Worker 子进程触发 SIGILL 非法指令崩溃，随后递归崩溃处理（systemd-coredump → drkonqi → apport）尝试分配约 28 GB 内存，最终导致系统冻结。硬件兼容性存在严重缺陷。
   - 链接: https://github.com/anomalyco/opencode/issues/36280

7. **#47120 Zen 列出 muse-spark-1.3-contributor-free 但 CLI 无法调用**
   - **评论**: 3 | **👍**: 0 | 状态: OPEN
   - 摘要: OpenCode Zen 在模型端点中广告了 `muse-spark-1.3-contributor-free`，但 1.18.27 CLI 未列出该模型，直接调用返回 UnknownError，关联 #40 系列 provider-catalog 工作。这是 9 月 3 日集中爆发的 Muse Spark 模型问题之一。
   - 链接: https://github.com/anomalyco/opencode/issues/47120

8. **#46932 添加认证元数据后 Muse Spark 1.3 消失**
   - **评论**: 3 | **👍**: 3 | 状态: CLOSED
   - 摘要: 用户配置 meta api-key 后，Muse Spark 1.3 模型不再出现。多个用户（#47075、#47157）报告类似现象，指向模型发现逻辑存在通用缺陷。
   - 链接: https://github.com/anomalyco/opencode/issues/46932

9. **#47034 Gemini 3.8 Flash 返回 400 "model turn" 错误**
   - **评论**: 3 | **👍**: 0 | 状态: OPEN
   - 摘要: Gemini 3.8 Flash 在模型回合后流式请求失败，报错 `Requests ending with a model turn are not supported`，影响通过 Gemini API 使用该模型的用户。
   - 链接: https://github.com/anomalyco/opencode/issues/47034

10. **#47096 桌面端自动接受权限开关无效**
    - **评论**: 2 | **👍**: 0 | 状态: OPEN
    - 摘要: 设置中 "Auto-accept permissions" 开关显示为 ON，但实际工具调用仍会弹出权限提示，开关未真正驱动运行时行为。
    - 链接: https://github.com/anomalyco/opencode/issues/47096

**其他值得关注**: #47157 (Synara + Muse Spark 1.3 报递归 JSON schema 错误)、#47072 (支付成功但工作区余额未同步)、#47097 (本地 serve 可能加载托管 UI 而非本地构建)。

## 重要 PR 进展

过去 24 小时共 50 条活跃 PR，精选如下：

1. **#47156 feat(core): 支持 Snowflake Cortex 原生认证**
   - 超集并合并了 #47135、#47139、#47151 三个独立 PR。改用原生 AI 包、加入浏览器 OAuth (含 PKCE)、移除 AI SDK wrapper。对 Snowflake 插件使用者是重要基础设施升级。
   - 链接: https://github.com/anomalyco/opencode/pull/47156

2. **#47160 fix(core): 在所有路由上分类 GitHub Copilot 请求**
   - 此前 Copilot 插件的 `X-Interaction-Type` 头只在原生 Claude 路由上生效，AI SDK 路由（GPT、其他 Copilot 模型）完全绕过。修复后能正确标记标题生成与压缩请求。
   - 链接: https://github.com/anomalyco/opencode/pull/47160

3. **#47159 fix(core): 重试被中断的压缩请求**
   - 压缩过程遇瞬时错误会失败，且可能接受被截断的摘要。本次复用现有 session 重试机制，提升长会话压缩可靠性。
   - 链接: https://github.com/anomalyco/opencode/pull/47159

4. **#47155 fix(app): 创建 worktree 时保留斜杠命令**
   - 修复首条消息创建新 worktree 时 `/review ...` 被当作纯文本发送的问题，行为与 TUI 保持一致，无需 Core 改动。
   - 链接: https://github.com/anomalyco/opencode/pull/47155

5. **#47102 [contributor] fix(desktop): 先渲染界面再初始化遥测**
   - 之前生产环境会先等待 Sentry SDK 动态 imports 完成才挂载 UI，导致启动变慢。本次将遥测改为异步非阻塞启动，并补充回归测试。
   - 链接: https://github.com/anomalyco/opencode/pull/47102

6. **#46973 [contributor] feat(app): 为实验性设置创建独立设置页**
   - 将此前散落的 Tabs / Show project names 等实验选项移动到新设立的 Experimental 页面，回应社区对设置页组织方式的需求。
   - 链接: https://github.com/anomalyco/opencode/pull/46973

7. **#45782 [contributor] feat(app): 新增“关于”设置页**
   - 应用版本号、GitHub 贡献者数量、致谢与法律信息等集中展示，附带动态版本渲染。持续完善桌面端 V2 设置体验。
   - 链接: https://github.com/anomalyco/opencode/pull/45782

8. **#45156 fix(desktop): 打磨 V2 会话并避免 store 竞争**
   - 统一 V2 控件的焦点、Hover、边框和间距，修复会话与 composer 交互不一致问题（关闭 #45154）。桌面端体验连续优化中。
   - 链接: https://github.com/anomalyco/opencode/pull/45156

9. **#46266 fix(tui): 显示思考快捷方式**
   - 当当前模型支持思考变体时，TUI 输入框将展示 `variant.cycle` 快捷键，解决 #46265 中“功能存在但无提示”的问题。
   - 链接: https://github.com/anomalyco/opencode/pull/46266

10. **#40268 fix(session): 重试顶层流请求超时**
    - 针对部分 OpenAI Responses 兼容提供商在 HTTP 200 后发出错误 SSE 事件导致会话中断的问题，加入重试机制（Closes #39221）。
    - 链接: https://github.com/anomalyco/opencode/pull/40268

**其他值得关注**: #40310 (新增 llmgateway-providers provider，LLM Gateway 集成)、#40289 (TUI 显示当前 Git 分支)。

## 功能需求趋势

从 Issues 和 PRs 中可以提炼出以下功能方向趋势：

- **Muse Spark / 模型发现一致性**：Muse Spark 1.3 Contributor Free 在 Zen 与 CLI 之间发现不一致的问题在 9 月 3 日集中爆发（#47120、#46932、#47075、#47157），且与 #40524 中“利用 `/models` 端点调和模型目录”的 V2 工作直接相关，是当前模型支持方向的核心矛盾。
- **性能回归跟踪**：CPU 高占用 (#30086) 与 SIGILL 崩溃 (#36280) 均是在近期版本中出现的回归或兼容性退化，开发者对启动后资源占用极其敏感。
- **系统提示词可配置化**：#15457（Default/Light 模式切换，#15457，5 评论 / 7 👍）反映用户希望系统提示词能适配小型/非前沿模型，而非一刀切重度优化。
- **MCP 生态完善**：#25961 要求支持 Client ID Metadata Document (CIMD)，配合 #25861 系列可以看到 OAuth 授权服务器集成是 MCP 方向的重要需求。
- **计费与用量透明化**：#38255、#45278、#47072 三个并发 issue 指向计费面板数据一致性、支付流程稳定性问题，直接影响用户信任与留存。

## 开发者关注点

开发者反馈主要集中在以下高频痛点：

- **模型可见性与可用性**：以 Muse Spark 1.3 系列为代表，大量“Zen 显示有模型，但 CLI 调不到/不显示”的反馈，说明模型目录实时同步缺口已经严重影响使用体验。
- **流式与错误恢复**：#47047（SSE 死循环）、#47034（Gemini 400）、#47153（上游 90 秒无数据）反映出流式请求异常处理仍不稳健，缺乏分类与重试策略。
- **桌面端与 TUI 细节缺失**：归档会话无法恢复（#12393）、TUI skills 列表未实现（#47067/#47068）、自动接受权限开关无效（#47096）等高频交互问题虽不致命，但累积消耗用户信任。
- **网络与代理兼容性**：#47041 指出编译后的 Bun 二进制会忽略 `NODE_OPTIONS` 中的 DNS 设置且时常绕过 `NO_PROXY`，将 loopback 流量错误地送入 HTTP 代理，对使用代理的开发环境是关键阻塞。
- **错误信息可操作性不足**：#47039 指出 Provider HTTP 失败（401/429/5xx）被压缩成 `UnknownError`，插件无法据此实现 fallback——开发者对错误可编程性提出了更高要求。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*