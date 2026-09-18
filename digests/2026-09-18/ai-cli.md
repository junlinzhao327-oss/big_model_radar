# AI CLI 工具社区动态日报 2026-09-18

> 生成时间: 2026-09-18 00:28 UTC | 覆盖工具: 7 个

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

# Claude Code Skills 社区热点报告
**数据截止：2026-09-18**  
注：样本中 PR 评论数字段为 `undefined`，因此“热门 PR”按展示顺序、更新活跃度及关联 Issue 影响综合判断；Issues 评论数用于提炼需求趋势。以下 PR 状态均为 `OPEN`。

---

## 1. 热门 Skills 排行（PR）

1. **#1298 fix(skill-creator): isolate trigger evals and handle Windows and runtime failures**  
   功能：修复 `skill-creator` 触发评估中的假阴性、Windows 下 `select()` 失败、运行时错误被误判为未触发等问题。  
   讨论热点：触发评估隔离、跨平台兼容、负例误通过导致优化失真。  
   状态：OPEN｜更新：2026-09-16  
   https://github.com/anthropics/skills/pull/1298

2. **#1769 Fix skill-creator trigger detection reporting 0% recall**  
   功能：修复 `skill-creator` 触发检测始终报告 `precision=100% recall=0%` 的严重问题。  
   讨论热点：关联 Issue #1721，描述优化基于错误证据，影响所有 Skill 的触发质量。  
   状态：OPEN｜更新：2026-09-15  
   https://github.com/anthropics/skills/pull/1769

3. **#1742 fix(mcp-builder): support mcp>=2 streamable_http_client import and custom headers**  
   功能：适配 `mcp>=2.0.0` 的导入重命名，并支持通过 `create_mcp_http_client` 配置自定义 Header。  
   讨论热点：修复 Issue #1668，MCP 生态升级后的连接兼容性。  
   状态：OPEN｜更新：2026-09-17  
   https://github.com/anthropics/skills/pull/1742

4. **#1703 Add md2video-audio skill**  
   功能：将 Markdown 文档编译为带拟真语音的专业 MP4 视频，号称零成本工作流。  
   讨论热点：Markdown → Marp → 视频/语音的自动化生产链路。  
   状态：OPEN｜更新：2026-09-15  
   https://github.com/anthropics

---

# Claude Code 社区动态日报
**日期：2026-09-18** ｜ 数据源：github.com/anthropics/claude-code

---

## 1. 今日速览

今天社区热度继续集中在 **可扩展性（Mods / Function Hooks）** 上，Issue #91870 以 195 条评论、120 个 👍 稳居榜首，官方已明确"数周内"交付 function hooks。同时，**VS Code 扩展**相关的老问题集中回流（焦点抢占、拖拽失效、权限设置不生效），加上新出现的 **Remote Control 会话离线** 反馈，IDE/桌面端体验成为当日最密集的痛点区。版本侧发布 v2.1.275，新增网关登录账号确认与"立即发送"快捷键。

---

## 2. 版本发布

### v2.1.275
- **网关登录身份确认**：登录 Claude apps gateway 时，若网关返回账号名，用户需先确认后才会保存凭证；`/status` 中可查看当前账号。
- **新增"立即发送"按键**：`Ctrl+Enter`（或 `Ctrl+X Ctrl+S`）可中断当前回合，并把队列中所有待发消息一次性发出——对长任务中插队输入的场景较为实用。

> 链接：https://github.com/anthropics/claude-code/releases

---

## 3. 社区热点 Issues（Top 10）

**1. #91870 Mods — make Claude 10x more extensible** ｜195 评论 ｜👍120
社区当前最高热度议题。作者 @poteat 在 9 月 9 日的社区更新中表示反馈"高信噪比、实质性影响了设计"，并承诺 **function hooks 将在数周内（而非数天）交付**。这是整个 Mods / 插件生态的路线图级讨论，值得所有插件开发者跟踪。
https://github.com/anthropics/claude-code/issues/91870

**2. #53247 Windows 桌面端无法启动（Silo / Job Object 残留，HRESULT 0x80070020）** ｜93 评论 ｜👍33
应用崩溃后残留孤儿进程对象，**只能注销或重启系统才能恢复**，已在 AppModel-Runtime EventID 215/208 中留下痕迹。4 月至今未解，属于严重的平台可靠性问题。
https://github.com/anthropics/claude-code/issues/53247

**3. #11455 Session Handoff / Continuity Support** ｜36 评论 ｜👍25
提出一年之久的会话交接/连续性需求：CLI 会话无法在机器或上下文之间平滑延续。对多机、长周期项目的开发者影响很大，评论区持续有用户补充场景。
https://github.com/anthropics/claude-code/issues/11455

**4. #25128 VS Code 扩展聊天面板拖拽失效** ｜33 评论 ｜👍48
终端 CLI 拖拽正常，**VS Code 扩展面板完全不可用**，自 v2.1.6 起回归且至今未修。👍 数偏高，说明受影响面广。
https://github.com/anthropics/claude-code/issues/25128

**5. #15921 VS Code 扩展不遵守 `.claude/settings.local.json` 权限** ｜31 评论 ｜👍32
即便开启 `bypassPermissions`，Bash/Write/Edit 操作仍未按配置生效——涉及权限模型的正确性，属于安全敏感级别的问题。
https://github.com/anthropics/claude-code/issues/15921

**6. #32726 VS Code 扩展：面板抢焦点** ｜19 评论 ｜👍57
Claude 有输出时面板自动展开并抢走编辑器焦点，打断输入。👍 数在榜单中最高之一，典型的高频体验损耗。
https://github.com/anthropics/claude-code/issues/32726

**7. #94225 macOS：直连 ISP 路径 TLS 1.3 握手被重置（ECONNRESET）** ｜2 评论
Anthropic 入口在携带 **X25519MLKEM768** 密钥共享时重置握手；改用经典 key share 或 VPN 后 12/12 成功。技术含量高，是 #74767 的重新开启，涉及后量子加密兼容性。
https://github.com/anthropics/claude-code/issues/94225

**8. #93438 Agent 使用 `isolation:"worktree"` 时 cwd 状态污染父会话** ｜1 评论
并行派发多个 implementer agent（Conductor 模式）时，worktree 会话状态会渗回调度方会话，直接影响多 Agent 编排的正确性。
https://github.com/anthropics/claude-code/issues/93438

**9. #81081 会话启动时的 skill 列表按体积预算静默截断描述** ｜11 评论
skill 描述在启动时被静默裁剪，用户难以察觉能力缺失；官方文档与实际行为不一致，已被标记 reproduced。
https://github.com/anthropics/claude-code/issues/81081

**10. #93156 浏览器面板无法授予持久站点权限** ｜6 评论
每个动作都弹权限框，且只有"拒绝 / 允许一次"，没有"始终允许"，`launchPreviewAllowedOrigins`、工具白名单、`bypassPermissions` 均无效。
https://github.com/anthropics/claude-code/issues/93156

**其他值得留意（当日新建/更新）**：
- #95254 Remote Control 会话在手机上显示"offline"，却仍能接收并处理其他会话消息，无法输入。
  https://github.com/anthropics/claude-code/issues/95254
- #95231 Remote Control 会话被当作 `entrypoint=sdk-cli` 过滤，本地 `/resume` 选择器中不可见。
  https://github.com/anthropics/claude-code/issues/95231

---

## 4. 重要 PR 进展

> 过去 24 小时内更新的 PR 仅 3 条，以下全部列出（本期 PR 侧整体较为平静）。

**#95198 mods/diff: 将 openPane 返回值类型放宽为 `unknown`**
让 diff mod 的宿主契约能同时兼容当前与下一版引擎类型定义（`$.ui.open` 即将返回结果对象），无调用方读取该值，行为不变。属于 Mods 生态的前瞻性类型适配。
https://github.com/anthropics/claude-code/pull/95198

**#94847 diff: 仅在确实有文件可列时才打开面板**
修复 diff 面板在会话首次 Edit/Write/NotebookEdit 时"先开面板后拉取"导致的空面板问题——写入仓库外、被忽略文件或不同 worktree 时会显示空白的 "No tracked changes"。
https://github.com/anthropics/claude-code/pull/94847

**#87077 fix(pr-review-toolkit): 修复所有 agent 的非法 YAML frontmatter**
各 agent 的 description 是包含 `Daisy: "..."` 这类对话行的未加引号标量，被 YAML 解析为嵌套映射，导致 agent 以空 frontmatter（name/description/model 全空）加载。
https://github.com/anthropics/claude-code/pull/87077

---

## 5. 功能需求趋势

从本期 50 条 Issues 中可提炼出六条主线：

| 方向 | 代表 Issue | 趋势判断 |
|---|---|---|
| **可扩展性 / Mods / Hooks** | #91870、PR #95198/#94847 | 官方已给出交付时间表，是当前最强投入方向 |
| **IDE 集成体验** | #25128、#32726、#15921、#77004、#79436 | VS Code 扩展是投诉最密集的模块，涵盖焦点、拖拽、权限、渲染 |
| **上下文 / Token 效率** | #92255、#83363、#85169、#81081 | MCP schema 与 deferred tools 在禁用后仍消耗 token（#83363 约 20k/会话），社区要求可调优的上下文保留策略 |
| **权限与安全护栏** | #15921、#93156、#79399 | 权限配置不被尊重、缺少"持久授权"、Agent 批量创建 91 个 PR 被仓库封禁 |
| **跨平台桌面可靠性** | #53247、#92472、#88632、#88640、#79296 | Windows 启动/重启、Cowork 本地项目挂载、Arch Linux 支持均长期未解 |
| **会话连续性与远程控制** | #11455、#95254、#95231 | Handoff、Remote Control 的可见性与连通性是新出现的热点 |

---

## 6. 开发者关注点（痛点与高频反馈）

1. **权限系统"说了不算"**：`settings.local.json`、`bypassPermissions`、`launchPreviewAllowedOrigins` 在 VS Code 扩展和桌面端多处失效，既影响效率也影响信任（#15921、#93156）。
2. **编辑器焦点与交互细节被反复强调**：面板抢焦点（👍57）、拖拽失效（👍48）、长消息 "Show less" 被挤出屏幕（#77004），说明 VS Code 扩展需要一次系统性 UX 修整。
3. **上下文与成本的可控性**：MCP schema 与 deferred tools 在关闭后仍在计费式占用 token，另有用户报告会话级模型切换导致全程按 Fable 高端费率计费且无提示（#79478）。
4. **多 Agent 编排的隔离性不足**：worktree 隔离出现 cwd 状态回渗（#93438），叠加 Agent 缺乏批量操作护栏（#79399），并行任务的安全边界尚未闭环。
5. **平台一致性与历史欠账**：Windows 桌面端崩溃后必须重启、Cowork 的 Project 记忆在 Local 与 Cloud 会话间行为不一致、Arch Linux 无官方桌面版——多个 4 月～7 月的老 Issue 至今 OPEN。
6. **大量 issue 被 `stale` 关闭引发摩擦**：本期列表中 #79399、#79436、#79453、#79486、#79296、#79304、#79311、#79330 等均以 `stale` 标签关闭，其中不乏 👍 较高的合理请求，社区对自动清理机制的观感值得官方关注。

---

*本日报基于 GitHub 公开数据自动整理，评论数与 👍 数反映截至 2026-09-18 的社区反馈热度。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报
**日期：2026-09-18** | 数据来源：github.com/openai/codex

---

## 一、今日速览

今日 Codex 发布 **rust-v0.155.0 稳定版**，带来实验性语音对话（`/voice`）与 TUI 推理摘要展示，同时推进至 **v0.156.0-alpha.1**。社区侧，**模型容量/限流问题（#28507、#43375）持续发酵**，累计评论超 80 条；**MCP 与第三方模型兼容性（#26234、#28858）** 和 **macOS Intel x64 版 Computer Use 缺失（#24437 等）** 成为开发者集中吐槽的两大痛点。PR 方面，Bot 集中合并了 OAuth 网关凭证管理、环境网络策略校验、插件缓存保留等一批基础设施改进。

---

## 二、版本发布

### rust-v0.155.0（稳定版）
- **实验性 `/voice` 语音对话**：支持实时转录与麦克风控制，需通过 `/experimental` 开启（#43581、#43651、#44331）
- **TUI 体验增强**：状态栏实时显示推理摘要（reasoning summaries），每轮成功完成后展示完成时间戳

### rust-v0.156.0-alpha.1
- 新 alpha 周期开启，具体变更未在 release note 中展开

### 其他 alpha 迭代
- rust-v0.155.0-alpha.15 ~ alpha.18 连续发布，为 0.155 稳定版做最后打磨

> 链接：https://github.com/openai/codex/releases

---

## 三、社区热点 Issues（Top 10）

| # | Issue | 热度 | 要点 |
|---|-------|------|------|
| 1 | **[#28507](https://github.com/openai/codex/issues/28507)** 模型容量不足（"Selected model is at capacity"） | 💬56 👍52 | 横跨 6 月至 9 月的长尾问题，Windows/Pro 5x 用户反复遭遇，至今 OPEN，是社区情绪最集中的一条 |
| 2 | **[#26234](https://github.com/openai/codex/issues/26234)** 为非 OpenAI Responses API 提供商扁平化 MCP namespace 工具 | 💬35 👍48 | Ollama / LM Studio / OpenRouter / Bedrock 用户下 MCP 工具完全不可调用，因 Codex 使用私有 `{"type":"namespace"}` 序列化格式，阻碍本地化/多厂商部署 |
| 3 | **[#24287](https://github.com/openai/codex/issues/24287)** Desktop 接受输入但 UI 卡在 Thinking，Stop 失效 | 💬31 👍14 | macOS 上会话状态机缺陷，重启后 turn 甚至不可见，属高严重度 UI/状态一致性问题 |
| 4 | **[#43375](https://github.com/openai/codex/issues/43375)** 多个 GPT-5 / GPT-6 模型返回容量错误 | 💬28 👍15 | 与 #28507 同源但覆盖面更广，跨模型切换仍失败，说明是服务端调度层而非单模型问题 |
| 5 | **[#31878](https://github.com/openai/codex/issues/31878)** ChatGPT/Codex 合并后 Projects 从桌面侧边栏消失 | 💬17 👍18 | ChatGPT 桌面端与 Codex 合并的回归问题，macOS 26.707 上 Projects 仅在网页端可见 |
| 6 | **[#40905](https://github.com/openai/codex/issues/40905)** 5 小时用量窗口打断长时 GPT-5.6 Sol Agent 任务 | 💬15 👍4 | 提出的是结构性矛盾：滚动窗口与当前自主长任务能力不匹配，属于产品策略级反馈 |
| 7 | **[#32188](https://github.com/openai/codex/issues/32188)** 后台 exec 会话完成时的事件驱动唤醒 | 💬10 👍13 | 社区呼声很高的 CLI 增强：用事件唤醒替代 `write_stdin` 轮询，可显著节省 model turn |
| 8 | **[#44848](https://github.com/openai/codex/issues/44848)** Daybreak 安全校验误报，导致活跃 goal 被标记为 stalled | 💬8 | Codex App 上的 safety-check / subagent 误判，影响 goal 状态可信度 |
| 9 | **[#45302](https://github.com/openai/codex/issues/45302)** Windows 提权沙箱失败：deny_read_acl_state.json 无效 | 💬8 | `helper_unknown_error: apply deny-read ACLs`，文件为 22 字节 NUL，与 #42958、#44034、#46114 构成同一类 Windows 沙箱故障群 |
| 10 | **[#

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报（2026-09-18）

## 1. 今日速览

今日 Gemini CLI 发布 `v0.62.0-nightly.20260917` 夜间版本。社区讨论高度集中在 **Subagent 生命周期与终止语义**（假 GOAL 成功、Generalist agent 挂起）以及 **Shell/PTY 执行稳定性**（Windows ConPTY、Wayland、命令完成后卡在 "Waiting input"）。PR 侧迎来一波 P1 修复：从 subagent 恢复语义、会话恢复工具响应重放，到 OAuth token 刷新、VS Code 终端焦点保持均有推进。

---

## 2. 版本发布

**v0.62.0-nightly.20260917.g6a466a7e2**
- 夜间构建版本，无详细变更说明。
- Full Changelog: https://github.com/google-gemini/gemini-cli/compare/v0.62.0-nightly.20260916.g6a466a7e2...v0.62.0-nightly.20260917.g6a466a7e2

---

## 3. 社区热点 Issues（Top 10）

1. **[#22323] Subagent 达到 MAX_TURNS 后仍被报告为 GOAL success，掩盖了中断事实**
   `priority/p1` · 13 评论 · 2 👍
   `codebase_investigator` subagent 在未完成分析、触发最大轮次限制时，仍返回 `status: "success"` 与 `Termination Reason: "GOAL"`，导致上层无法感知任务实际失败。这是当前社区最关注的可靠性问题，已有对应修复 PR。
   https://github.com/google-gemini/gemini-cli/issues/22323

2. **[#21409] Generalist agent 无限挂起**
   `priority/p1` · 8 评论 · 8 👍（本批最高赞）
   user 反馈每当 CLI 委派给 generalist agent 就会永久卡住，简单如创建文件夹也需等待一小时。禁用 subagent 委派可规避。高 👍 数说明该问题影响面广。
   https://github.com/google-gemini/gemini-cli/issues/21409

3. **[#25166] Shell 命令执行完成后卡在 "Waiting input"**
   `priority/p1` · 4 评论 · 3 👍
   简单 CLI 命令已执行结束，但 UI 仍显示 shell 命令活跃并等待用户输入。属于核心交互阻塞类 bug。
   https://github.com/google-gemini/gemini-cli/issues/25166

4. **[#19873] 利用模型的 bash 亲和力：零依赖 OS 沙箱 + 执行后意图路由**
   `priority/p2` · 9 评论
   提案让 Gemini 3 以原生 bash 用户方式（grep/cat/sed/awk）探索与编辑代码，同时通过零依赖沙箱保障安全。属于架构级方向讨论。
   https://github.com/google-gemini/gemini-cli/issues/19873

5. **[#22745] 评估 AST 感知的文件读取、搜索与代码库映射的影响**
   `priority/p2` · 7 评论 · EPIC
   探索 AST 感知工具能否减少无效读取轮次与 token 噪声，是提升代码理解效率的关键研究方向。
   https://github.com/google-gemini/gemini-cli/issues/22745

6. **[#21968] Gemini 不够主动使用 skills 与 sub-agents**
   `priority/p2` · 6 评论
   用户反馈除非显式指令，模型几乎不会自主调用自定义 skill 或 subagent，影响扩展能力发挥。
   https://github.com/google-gemini/gemini-cli/issues/21968

7. **[#26525] Auto Memory 需要确定性脱敏并减少日志**
   `priority/p2, area/security` · 5 评论
   当前 Auto Memory 在内容进入模型上下文**之后**才依赖提示词脱敏，存在密钥先入模型的风险；服务端还会记录已有 skill 信息。安全敏感度高。
   https://github.com/google-gemini/gemini-cli/issues/26525

8. **[#26522] Auto Memory 不应无限重试低信号会话**
   `priority/p2` · 4 评论
   低信号会话若未被 `read_file` 读取，就不会被标记为已处理，从而反复出现在索引中，造成重复开销。
   https://github.com/google-gemini/gemini-cli/issues/26522

9. **[#21983] Browser subagent 在 Wayland 下失败**
   `priority/p1, agent/browser` · 4 评论
   浏览器子代理在 Wayland 环境直接失败并报告终止原因 GOAL，Linux 桌面兼容性问题。
   https://github.com/google-gemini/gemini-cli/issues/21983

10. **[#24246] 工具数 > 128 时触发 400 错误**
    `priority/p2` · 3 评论
    当可用工具超过阈值时 CLI 遭遇 400，期望 agent 能更智能地限定工具范围。与工具生态扩张直接相关。
    https://github.com/google-gemini/gemini-cli/issues/24246

---

## 4. 重要 PR 进展（Top 10）

1. **[#29367] fix(agents): 保留 subagent 恢复时的原始终止原因，防止假 GOAL 成功**
   `priority/p1, area/agent` — 直接修复 #22323。根因是 `LocalAgentExecutor` 恢复路径无条件覆盖 `terminateReason`。
   https://github.com/google-gemini/gemini-cli/pull/29367

2. **[#29379] fix(core): 同步 ConPTY 进程退出生命周期并加固 PTY 输出终结**
   `priority/p1, area/core` — 提升 Windows ConPTY 下 `ShellExecutionService` 的进程生命周期确定性与流完成一致性。
   https://github.com/google-gemini/gemini-cli/pull/29379

3. **[#29366] fix(core): 停止会话恢复时重复回放工具响应**
   `priority/p1, area/core` — 使用 `-r` 恢复会话时每个工具结果被发送两次，导致 functionCall/functionResponse 配对校验失败。影响所有会话恢复路径。
   https://github.com/google-gemini/gemini-cli/pull/29366

4. **[#29368] fix(acp): 即使无可恢复内容也按 ID 解析 session/load**
   `priority/p1, area/non-interactive` — 修复 #29288，会话文件存在且 sessionId 完全匹配时仍加载失败的问题。
   https://github.com/google-gemini/gemini-cli/pull/29368

5. **[#29339] fix(core): 刷新时保留 OAuth refresh token，凭证删除幂等（已关闭）**
   `priority/p1, area/core` — 修复 GH-21691：刷新后 `refresh_token` 丢失导致用户陷入重复认证错误循环。
   https://github.com/google-gemini/gemini-cli/pull/29339

6. **[#29378] fix(vscode-ide-companion): 关闭 diff 标签时保留终端焦点**
   `priority/p1, area/extensions` — 向 `tabGroups.close` 传入 `preserveFocus=true`，避免编辑器抢走集成终端焦点，改善多文件编辑体验。
   https://github.com/google-gemini/gemini-cli/pull/29378

7. **[#29343] fix(cli): 抑制请求取消期间未捕获的 AbortError 日志**
   `size/m` — 解决 Node 23+ 下用户取消查询时 `node-fetch` 事件监听器内同步抛出的 `AbortError` 导致硬崩溃。
   https://github.com/google-gemini/gemini-cli/pull/29343

8. **[#

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报
**日期：2026-09-18**

## 1. 今日速览

过去 24 小时，Copilot CLI 发布 `v1.0.86` 与 `v1.0.86-2`，重点增强自定义 agents 对仓库指令文件的接入，并包含修复性变更。社区讨论仍高度集中在 **MCP 生命周期与兼容性、插件/Agents 发现、Windows 插件更新文件锁、Auto 模型回归** 等方向。过去 24 小时无 PR 更新，代码合入动态暂缺。

---

## 2.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-09-18** ｜ 数据来源：github.com/MoonshotAI/kimi-cli

> 说明：过去 24 小时窗口内，仓库仅产生 3 条 Issue 更新与 1 条 PR 更新，数量不足以支撑"各选 10 条"的筛选。以下按实际数据全量呈现，并附重要性评估。

---

## 一、今日速览

过去 24 小时无新版本发布，社区活动集中在**运行时稳定性**与**客户端配置一致性**两个方向：一是 Kimi Desktop 的「chat 记忆 / 梦境记忆」开关疑似被服务端功能门控拦截，配置未落盘；二是 subagent 启动时对 `auth.kimi.ai` 的 OAuth 拉取存在间歇性超时，导致整个子代理派生流程失败。同时，一条针对重复 tool-call 死循环的修复 PR 已提交待审。

---

## 二、版本发布

过去 24 小时无新 Release。

---

## 三、社区热点 Issues（本窗口共 3 条，全量列出）

### 1. #2649 [OPEN] Kimi Desktop「梦境记忆」开关不写入配置，疑似服务端门控未放行
- 作者：@GH-Mason ｜ 创建/更新：2026-09-17 ｜ 评论：2 ｜ 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2649
- **内容**：环境为 Kimi Desktop 3.2.9（macOS / Electron 43.6.0），账号为 Vivace 会员。设置 → chat 记忆 →「梦境记忆」开关可正常拨动，但拨动后本地 `daimon/config.json` 中的 `features.memory`、`features.memory.dream`、`runtime.dream.autoTrigger...` 等字段均未更新。
- **为什么重要**：这是一个典型的"UI 状态与持久化状态不一致"问题。用户是付费会员且开关可操作，说明前端未做禁用处理，但配置不落盘意味着功能实质上不可用；报告者推测是服务端功能门控（feature gate）未对该账号放行。这类问题会直接损害付费用户对"记忆"这一核心卖点的信任，且排查路径横跨客户端与服务端，优先级应较高。
- **社区反应**：已有 2 条评论，处于初步定位阶段。

### 2. #2650 [OPEN] subagent 启动间歇性失败：OAuth token 拉取 `auth.kimi.ai` 超时
- 作者：@genhoi ｜ 创建/更新：2026-09-17 ｜ 评论：0 ｜ 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2650
- **内容**：在用户已完整认证、主会话工作正常的前提下，启动 subagent 会间歇性地因连接 `auth.kimi.ai` 超时而失败；重试同样的启动操作最终能够成功。当前实现中，一次瞬时的认证端点抖动会导致整个 subagent 派生流程失败。
- **为什么重要**：这是**错误处理策略缺陷**而非单纯的网络问题。认证端点抖动属于不可避免的瞬时故障，但当前实现没有退避重试或降级路径，属于典型的"单点抖动放大为整体失败"。Subagent 是多任务/并行编排的关键能力，失败率哪怕只有个位数也会显著影响批量场景体验。建议引入带抖动的指数退避 + 可配置超时。
- **社区反应**：暂无评论，属于新提交的独立报告。

### 3. #1276 [CLOSED] `@` 文件自动补全缺漏文件
- 作者：@hongquan ｜ 创建：2026-02-27 ｜ 更新并关闭：2026-09-17 ｜ 评论：2 ｜ 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1276
- **内容**：Kimi Code CLI 1.16.0，Moonshot AI 开放平台，模型 `kimi-k2.5`，Linux 6.17.0-14-generic x86_64。`@` 触发的文件自动补全列表中缺失部分文件。
- **为什么重要**：`@` 文件引用是 CLI 中出现频率最高的交互之一，补全缺漏会直接打断心流，用户不得不手打路径。该 Issue 从 2 月挂到 9 月才关闭，生命周期长达近 7 个月，侧面反映了补全索引逻辑（很可能是 gitignore / 隐藏目录 / 符号链接的处理边界）的排查难度。
- **社区反应**：2 条评论后关闭，建议关注关闭原因（已修复 or 失效关闭），并在后续版本中回归验证。

---

## 四、重要 PR 进展（本窗口共 1 条，全量列出）

### #2651 [OPEN] fix: stop repeated tool-call loops
- 作者：@Oxygen56 ｜ 创建/更新：2026-09-17 ｜ 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/pull/2651
- 关联 Issue：#2637
- **内容**：把"重复相同 tool-call"的防护逻辑从**软停止改为硬停止**。此前的行为是：运行时在达到重复上限时设置了停止标志，但**仍然会执行那最后一次重复调用**，之后才真正停下。本 PR 改为在达到重复上限后、执行下一次重复调用之前即硬性中断。
- **为什么重要**：这类 off-by-one 的边界缺陷会造成实际损害——多出来的一次重复调用既浪费 token 与配额，也可能产生真实的副作用（如重复写入文件、重复执行命令）。修复方向明确、改动面小，属于低风险高收益的稳定性补丁，建议优先评审合入，并补充针对"恰好达到上限"这一边界条件的单元测试。

---

## 五、功能需求趋势

基于本窗口全部 Issue 提炼，社区关注方向集中在以下几点：

1. **记忆 / 上下文持久化（Memory & Dream Memory）**
   #2649 显示用户对"跨会话记忆"期望很高，且已进入付费会员的使用路径。当前痛点是功能可用性与会员权益的联动校验不透明——用户无法判断"开关无效"是自己配置问题、客户端 Bug 还是账号未放行。

2. **多代理编排的健壮性（Subagent / Orchestration）**
   #2650 指向 subagent 生命周期的容错短板。随着并行/多代理工作流成为主流用法，认证、派生、回收各环节都需要独立的重试与降级策略，而非让单次网络抖动终止整个流程。

3. **CLI 交互体验与补全准确性**
   #1276 虽已关闭，但 `@` 文件补全的完整性、索引范围（.gitignore、隐藏文件、monorepo 子目录）仍是高频体验点，长期未解说明该模块的边界条件较为复杂。

4. **运行时循环防护与配额保护**
   #2651 表明"工具调用死循环"是真实发生过的场景。除了事后中断，社区可能还会期待**可配置的重复上限**、循环检测的可观测性输出（日志/警告）以及 token 消耗的显式提示。

5. **网络与认证层可观测性**
   #2650 中用户无法自行区分是端点故障还是本地网络问题。分层错误信息（DNS / TLS / 超时 / 401）与 `--verbose` 诊断输出会显著降低此类 Issue 的往返成本。

---

## 六、开发者关注点

综合本窗口反馈，开发者侧的痛点可归纳为：

- **配置写入与 UI 状态脱节**（#2649）：开关 UI 与 `daimon/config.json` 不同步，且无任何错误提示，用户只能靠手动检查配置文件才发现问题。建议：写配置失败时在 UI 层显式报错，并在功能门控未放行时直接禁用开关并说明原因。
- **瞬时网络故障缺乏重试语义**（#2650）：OAuth 拉取超时直接终止 subagent 派生，缺少退避重试、独立超时配置和失败降级。这是"可用性由最脆弱一环决定"的典型案例。
- **重复调用防护存在边界漏洞**（#2651 / #2637）：上限触发后仍会多执行一次，说明停止条件的判定时机需要更严格的测试覆盖。
- **长尾体验问题修复周期偏长**（#1276，约 7 个月）：补全类问题虽然不阻塞核心流程，但高频触及，建议纳入常规回归测试集。
- **M 端（Desktop）与 CLI 的问题边界模糊**：#2649 是 Desktop 端问题，却提交在 CLI 仓库，说明用户在"功能归属哪个仓库"上存在困惑，可能需要在模板或文档中明确分流规则。

---

*本日报基于过去 24 小时 GitHub 公开数据自动汇总。如需持续跟踪，建议订阅 #2649 与 #2651 的后续进展。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 (2026-09-18)

## 今日速览
今日无新版本发布。社区最热点是免费层错误“OpenCode's free tier can only be used from within OpenCode”集中爆发，影响官方桌面端与 CLI 用户，多个重复 Issue 被创建。同时，Muse Spark 1.3 会话恢复错误和 DeepSeek V4 Flash 中国托管政策持续引发讨论，计费透明度与版本回归问题也备受关注。

## 版本发布
无。

## 社区热点 Issues

1. **#49433 [OPEN] Error from provider (Console): OpenCode's free tier can only be used from within OpenCode**  
   - 链接：https://github.com/anomalyco/opencode/issues/49433  
   - 重要性：免费层用户无法使用，错误信息自相矛盾（在 OpenCode 内却提示只能在 OpenCode 内使用），影响范围广。  
   - 社区反应：27 条评论，4 👍，大量用户报告相同问题并创建重复 Issue。

2. **#39845 [OPEN] DeepSeek V4 Flash on suddenly requires "Enable models hosted in China" for OpenCode Go subscription**  
   - 链接：https://github.com/anomalyco/opencode/issues/39845  
   - 重要性：模型托管政策变更导致会话中断，需显式 opt-in 中国托管，影响付费 Go 订阅用户。  
   - 社区反应：24 条评论，30 👍，高赞表明广泛共鸣。

3. **#48645 [OPEN] Regression in 1.18.30: every prompt crashes with TypeError in SystemPrompt.environment ("a.name") — 1.18.18 works fine**  
   - 链接：https://github.com/anomalyco/opencode/issues/48645  
   - 重要性：版本回归导致所有提示立即崩溃，严重影响可用性。  
   - 社区反应：10 条评论，17 👍，用户报告回滚到 1.18.18 可解决。

4. **#489

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报
**日期：2026-09-18** | 数据来源：[github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)

---

## 一、今日速览

桌面端 **Qwen Code Desktop v0.24.0** 正式发布，同日夜间构建同步推进 ACP 边界验收与 CLI 权限队列修复。社区方面，**上下文/Token 管理**成为最密集的话题簇（#12028 系列拆分出 5+ 个独立 Issue），同时 **React #185 崩溃**（#11732、#11783）在 Linux/Windows TUI 与后台任务场景持续发酵。CI 可靠性、权限规则安全性与会话完整性也是今日高频讨论方向。

---

## 二、版本发布

### 🚀 desktop-v0.24.0（Qwen Code Desktop v0.24.0）
- `fix(cli): scope the ACP permission queue to the session`（[#11802](https://github.com/QwenLM/qwen-code/pull/11802) by @chiga0）——将 ACP 权限队列作用域收窄至会话级别，避免跨会话串扰。
- `feat(channels): add shared output modes`——通道层新增共享输出模式。

### 🌙 v0.24.0-nightly.20260917.f822124af5
- `docs(serve): record merged ACP boundary acceptance`（[#12024](https://github.com/QwenLM/qwen-code/pull/12024) by @wenshao）——记录 ACP 边界验收结果。
- `fix(ci): wait for the published export re...`——CI 中等待发布导出的修复。

---

## 三、社区热点 Issues

1. **[#9278](https://github.com/QwenLM/qwen-code/issues/9278) `/review` 发布时收敛建议设计（OPEN · P2 · 10 评论）**
   记录 `/review` 的 publish-time convergence advisory 完整设计与实测数据。指出评审回路增益 > 1 时仅靠 AGENTS.md 中 "约 5 轮后只处理 Critical" 的 prose 阻尼，在评论最多、上下文最满时最容易失效。属于自动化评审系统的方法论级讨论，是今日评论数最高的 Issue。

2. **[#11732](https://github.com/QwenLM/qwen-code/issues/11732) 0.23.3 React #185 崩溃（CLOSED · P1 · 8 评论）**
   Linux 上长任务运行中 TUI 因无捕获的 React 错误 #185 崩溃，而原生 monitor 任务仍在后台继续。两个独立会话复现，已被关闭，但其姊妹问题 #11783 仍开放，说明修复可能尚未完全覆盖。

3. **[#12061](https://github.com/QwenLM/qwen-code/issues/12061) 回调身份变化替换活跃工具调度器（OPEN · P2 · 8 评论）**
   `useReactToolScheduler` 在 caller callback 身份变化时重建 `CoreToolScheduler`，导致仍在持有活跃 batch 的调度器被替换。典型的 React hooks 与命令式调度器混用缺陷，影响工具执行的正确性。

4. **[#8138](https://github.com/QwenLM/qwen-code/issues/8138) worktree 下 settings.json 写入项目根（OPEN · P2 · 7 评论）**
   在 git worktree 中保存设置时写入的是 **project-root** 的 `.qwen/settings.json` 而非 worktree 自身的 `.qwen/`。自 7 月底创建至今仍在更新，属于长期悬而未决的多 worktree 隔离问题。

5. **[#12053](https://github.com/QwenLM/qwen-code/issues/12053) 精简 Goal runtime：基于当轮证据判断完成（OPEN · P2 · 7 评论）**
   实测两次 `/goal-draft` 会话均在单个 Goal turn 内（约 100 次工具调用）完成全部目标，随后的 evidence catalog 与 checkpoint 机制变成纯开销。社区倾向删除这些冗余抽象——对应 PR #12120 已提交。

6. **[#11956](https://github.com/QwenLM/qwen-code/issues/11956) 无参工具的 `parameters` 被序列化为 null（OPEN · P2 · 6 评论）**
   0.23.4 会把无参工具的 `parameters` 字段序列化为 `null`，导致严格的 OpenAI 兼容网关拒绝整个请求（期望 `{}` 或省略）。影响第三方兼容层接入，属于协议层兼容性 bug。

7. **[#10689](https://github.com/QwenLM/qwen-code/issues/10689) kimi-k3 经 OpenAI 兼容代理反复报错 tool call（OPEN · P1 · 6 评论）**
   长会话（transcript ~1.6 MB）下 `qwen serve` 反复出现 `Model response contained a malformed tool call`，5 次重试耗尽。P1 级核心缺陷，涉及大 transcript 场景下的流式解析健壮性。

8. **[#12072](https://github.com/QwenLM/qwen-code/issues/12072) OpenRouter preset 发送了错误的自定义头（OPEN · P3 · 6 评论）**
   内置 OpenRouter preset 发送 `X-OpenRouter-Title`，但 OpenRouter 实际只识别 `X-Title` 做应用归因。小问题但影响 provider preset 的准确性与可观测性。

9. **[#12091](https://github.com/QwenLM/qwen-code/issues/12091) `sessions/delete` 删除活跃会话 transcript 致永久损坏（OPEN · P1 · 4 评论）**
   删除仍被运行时 attach 的会话时，writer 不会停止，而是重建 file head-less 并继续追加，首条记录 `parentUuid` 悬空，导致 `degraded_history`、自动续聊失效。会话管理路线图上的严重数据完整性问题。

10. **[#10887](https://github.com/QwenLM/qwen-code/issues/10887) 重复工具错误无提前终止，会话烧掉 5–14M token（OPEN · P1 · 4 评论）**
    生产会话在 0.20.1–0.21.0 上出现死循环探索：工具反复返回同一错误但无终止机制，单会话消耗 5–14M token。与 #12028 上下文预算簇呼应，是成本与稳定性的双重痛点。

---

## 四、重要 PR 进展

1. **[#12115](https://github.com/QwenLM/qwen-code/pull/12115) `fix(installer)`：为 Linux 归档预检 glibc（OPEN）**
   在 CentOS 7 等旧发行版上，独立安装器会安装自带 Node.js 22 的官方归档，但运行时会因缺少 `GLIBC_*` 符号启动失败。本 PR 在安装前预检 glibc，把事后崩溃变为事前提示。

2. **[#12131](https://github.com/QwenLM/qwen-code/pull/12131) `fix(core)`：在 transcript 中保留 MCP App HTML 以便回放渲染（CLOSED）**
   MCP App 工具结果现在会保留 `html` 与 `toolResult`（在保留显示预算内），使已保存会话能重放 App 的沙箱 iframe。直接回应 #10369 的 MCP Apps 渲染可见性问题。

3. **[#11242](https://github.com/QwenLM/qwen-code/pull/11242) `feat(browser-use)`：新增 Chrome Native Messaging 中继（OPEN）**
   通过本地 Native Messaging host 与 Qwen Chrome 扩展，把 Browser SDK

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*