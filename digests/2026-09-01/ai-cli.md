# AI CLI 工具社区动态日报 2026-09-01

> 生成时间: 2026-08-31 22:35 UTC | 覆盖工具: 7 个

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

> ⚠️ **数据范围说明**：本次动态摘要仅覆盖 **OpenAI Codex** 与 **Qwen Code** 两个工具，其余 5 个工具（Claude Code、Gemini CLI、GitHub Copilot CLI、Kimi Code CLI、OpenCode）未提供社区数据。以下分析基于可用数据，并已标注数据缺口，避免误导性推断。

---

## 1. 生态全景

AI CLI 工具正从"对话式编码助手"加速演变为"自主执行平台"。OpenAI Codex 在 24 小时内密集发布 3 个 alpha 版本（`v0.152.0-alpha.5~7`），Qwen Code 保持 nightly 节奏，双方均处于高频迭代期。共同主线有三：一是从"对话生成代码"走向"无人值守执行"（定时任务、语音助手、自动 review）；二是 MCP 集成越过"能否连接"阶段，进入"可靠性和生命周期管理"攻坚期；三是会话存储膨胀、Windows 稳定性、安全信任边界等"大规模使用后遗症"集中浮现，说明行业竞争已从功能密度转向可靠性深度。

---

## 2. 各工具活跃度对比

| 工具 | Releases（24h） | 关键 PR 动态 | Top 10 Issue 活跃度 | 最高 👍 |
|---|---|---|---|---|
| **OpenAI Codex** | 3（rust-v0.152.0-alpha.5 / .6 / .7） | 10 个关键 PR：9 个已关闭/合并，1 个开启（架构重构） | 合计 ~303 条评论；单 issue

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-09-01

## 今日速览

过去 24 小时，OpenAI Codex 密集发布了 `0.152.0-alpha.5` 至 `alpha.7` 三个预览版本，核心工作集中在 TUI 会话稳定性与 MCP 事件流架构。社区讨论热度最高的是三个方向：定时任务未经授权被自动禁用（63 条评论）、TUI 命令折叠行为引发强烈反对（73 👍）、Windows 桌面端多项阻断性问题（启动失败、ACL 拒绝等）。PR 侧，`copyberry[bot]` 批量贡献了 TUI 重连、MCP 订阅保持、voice host 生命周期等基础设施改进。

## 版本发布

**rust-v0.152.0-alpha.7 / alpha.6 / alpha.5**

过去 24 小时连续发布三个 alpha 版本。官方 Release 说明仅有版本号，未附带详细变更日志。结合同期合并的 PR 推断，这三个版本大概率包含 TUI 自动重连、命令展示优化、MCP 事件流管理等近期合入的新特性。建议关注后续稳定版发布说明。

## 社区热点 Issues

以下为过去 24 小时更新最活跃或影响力最大的 10 个 Issue：

1. **[Recurring scheduled tasks disable themselves after successful runs without user authorization](https://github.com/openai/codex/issues/38350)**
   - 63 条评论 | 高活跃度
   - 周期性定时任务在成功运行后未经用户同意自动从 "enabled" 变为 "paused"，一次事故中 4 个不相关任务同时被禁用。自动化可靠性和用户授权问题，值得高度关注。

2. **[add an option to disable “Ran N commands” collapsing and always show executed commands](https://github.com/openai/codex/issues/39903)**
   - 54 条评论 | 73 👍
   - 用户强烈要求 TUI 增加选项关闭 "Ran N commands" 折叠行为。73 个 👍 表明这是社区广泛认可的体验问题，PR #41893 已在尝试解决。

3. **[Windows 26.820 Codex Desktop cannot start: bundled codex.exe relocation from WindowsApps fails](https://github.com/openai/codex/issues/40700)**
   - 39 条评论
   - Windows 桌面版因 WindowsApps 目录重定位失败导致完全无法启动，属于阻断性 bug，影响 ChatGPT Plus 订阅用户。

4. **[Windows Computer Use screenshot fails on Windows 10 22H2 when SetIsBorderRequired is called](https://github.com/openai/codex/issues/25178)**
   - 35 条评论 | 17 👍
   - Windows 上 Computer Use 的 `get_window_state` 截图功能因 `SetIsBorderRequired` 接口不支持（0x80004002）而失败，影响 Win10 22H2 用户，长期未解决。

5. **["Bad request" error](https://github.com/openai/codex/issues/10571)**
   - 26 条评论
   - 从 0.94.0 版本起就存在的 "Bad request" 错误，至今仍被频繁提及，且横跨 macOS/Linux 多个平台，疑似后端协议层面的兼容性问题。

6. **[Dynamically loading nested AGENTS.md](https://github.com/openai/codex/issues/12115)**
   - 24 条评论 | 109 👍
   - 社区强烈要求 Codex 支持嵌套 AGENTS.md 的动态加载和覆盖语义，已有 Wix 等大客户反馈。109 👍 是本期所有 Issue 中最高，说明上下文配置管理是核心痛点。

7. **[Input message disappears while Codex CLI is responding](https://github.com/openai/codex/issues/5538)**
   - 20 条评论
   - 老 issue（2025-10-22），CLI 响应期间用户输入的部分消息会消失，影响长输入场景，至今未关闭。

8. **[Subagents leak stdio MCP helper trees in Codex App; xcodebuildmcp and chrome-devtools-mcp accumulate indefinitely](https://github.com/openai/codex/issues/17574)**
   - 16 条评论
   - 子代理在使用 stdio MCP 时泄漏辅助进程树，`xcodebuildmcp` 和 `chrome-devtools-mcp` 无限累积，最终可能耗尽系统资源。

9. **[Android Remote became unusable: Windows host appears disconnected and long tasks do not open](https://github.com/openai/codex/issues/39947)**
   - 14 条评论 | 6 👍
   - Android 端远程连接 Windows 主机时显示已断开、长任务无法打开。跨端远程一致性问题，移动端用户体验受损。

10. **[Windows floating pet remains click-through and cannot be dragged](https://github.com/openai/codex/issues/41465)**
    - 12 条评论 | 9 👍
    - Windows 桌面悬浮宠物无法接收鼠标输入、不能拖拽。UI 交互 bug，虽非核心功能但反映了桌面端细节完成度不足。

## 重要 PR 进展

以下为过去 24 小时更新/合并的 10 个关键 PR：

1. **[Show successful TUI commands individually](https://github.com/openai/codex/pull/41893)**（已关闭）
   - 直接回应 Issue #39903：每个完成的命令单独显示为一个 history cell，不再折叠为 "Ran N commands"，但保留文件读取/搜索的 "Explored" 分组。

2. **[Persist response token usage in rollout history](https://github.com/openai/codex/pull/41912)**（已关闭）
   - 在 rollout 中新增持久化的 `TokenUsageRecord`，使恢复的线程无需回扫压缩检查点即可正确累计 token 用量。

3. **[Reconnect TUI app-server sessions automatically](https://github.com/openai/codex/pull/41916)**（已关闭）
   - app-server 传输断开后 TUI 自动重连，重建客户端并恢复活动线程，保留缓存转录、草稿和实时通知。

4. **[Add a manager for MCP event streams](https://github.com/openai/codex/pull/41906)**（已关闭）
   - 新增 `McpEventStreamManager`，按线程和订阅管理事件流 worker，激活确认后才完成启动，事件流与来源 runtime 生命周期解耦。

5. **[Keep MCP event subscriptions alive after task unloading](https://github.com/openai/codex/pull/41899)**（已关闭）
   - 新增 `McpEventStreamOpener`，使 MCP 事件订阅可超越关联任务的 MCP runtime 存活。

6. **[Allow per-call sideband endpoints for existing realtime calls](https://github.com/openai/codex/pull/41923)**（已关闭）
   - 为 `ConversationStartTransport::ExistingCall` 增加进程内 `sideband_base_url` 覆盖，per-call 端点优先。

7. **[Add installed voice host lifecycle support](https://github.com/openai/codex/pull/41902)**（已关闭）
   - 新增 `VoiceHost`，负责解析打包的语音助手、执行协议握手和强制关闭与进程清理，为桌面语音功能打基础。

8. **[Make permission transforms aware of executor path context](https://github.com/openai/codex/pull/41909)**（已关闭）
   - 权限转换逻辑现在感知执行器路径上下文，可正确解析项目根、home-relative deny globs、临时目录等，增强沙箱安全。

9. **[Avoid scanning archived rollouts when archiving threads](https://github.com/openai/codex/pull/41908)**（已关闭）
   - 归档线程时使用 `RolloutReferenceIndex::scan_unarchived` 只扫描未移动文件，避免无谓地读取整个归档，优化性能。

10. **[Extract apps cache logic into ConnectorRuntimeManager](https://github.com/openai/codex/pull/31471)**（开启）
    - 由 `@mzeng-openai` 提交的架构重构 PR（faster-connectors 系列 1/4），将 Codex Apps 工具缓存抽取为 `ConnectorRuntimeManager`，并按账户/用户/工作区维度隔离 runtime 上下文。

## 功能需求趋势

综合过去 24 小时 Issue 与 PR 讨论，社区关注度最高的功能方向为：

- **TUI/CLI 交互精细化**：要求命令展示可控（#39903）、输入不丢失（#5538）、断开自动重连（#41916），社区对终端体验的细节要求越来越高。
- **Windows 平台稳定性攻坚**：Issue 中 Windows 独占问题占比极高——启动失败（#40700）、Computer Use 截图失败（#25178）、ACL 拒绝（#40047）、进程反复生成（#26812）、UI 卡顿（#38793）。Windows 已是 Codex 桌面端最薄弱的环节。
- **上下文管理与 AGENTS.md 动态加载**：嵌套 AGENTS.md 动态加载获 109 👍（#12115），context_compaction 错误虽已关闭（#27511/#27555/#27269），但用户对透明、可控的上下文压缩仍有强烈诉求。
- **本地存储与会话生命周期治理**：会话 rollout 膨胀至 TiB 级（#34337）、陈旧 session_index 指向缺失文件（#31074）、ghost 线程无法归档（#39567），本地数据治理问题被反复提及。
- **MCP 生态成熟化**：子代理 MCP 进程泄漏（#17574）、事件订阅生命周期管理（#41899/#41906），说明 MCP 集成正从"能用"走向"可靠"。

## 开发者关注点

- **自动化任务可靠性**：定时任务成功后自动禁用（#38350）引发对"无人值守自动化"信任感的担忧。若该问题不解决，用户将不敢依赖 Codex 执行计划任务。
- **Windows 桌面版是重灾区**：从启动失败、文件 ACL 拒绝、UI 卡顿到浮动宠物无法拖拽，Windows 端的体验明显落后于 macOS。多位用户在多个 Windows 版本（10/11、26200 等）上均复现了问题。
- **本地存储无上限增长**：会话存储从几十 GiB 膨胀到 TiB 级（#34337），且删除/归档/清理的 UX 不明确（#28187）。开发者希望 Codex 提供清晰的存储管理和自动清理机制。
- **Agent 行为可控性不足**：模型在明确指示继续工作后仍自行终止任务（#36596）、子代理忽略显式 model_provider 配置（#40858），开发者需要更强的 agent 行为约束能力。
- **老问题悬而未决**：#10571（Bad request）从 2 月持续至今、#5538（输入消失）从去年 10 月至今仍未关闭，社区对长期未修复问题的耐心正在消耗。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>



</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-09-01

## 今日速览

- 发布 `v0.22.3-nightly.20260831`，带来 Web Shell 的 git 状态提示与 review 流程改进。
- Bailian Token Plan 认证与模型列表不同步问题（#8432）持续发酵，成为社区讨论热度最高的话题。
- 会话管理（归档、恢复、resume）与安全信任边界成为今日 issue 与 PR 的共同主线。

## 版本发布

### v0.22.3-nightly.20260831.3a0c4c6108

- feat(web-shell): 分支选择器操作旁展示 git 状态提示（PR #10397）
- feat(review): 相关改动进行中（截断，详见 PR）
- 发布链接: https://github.com/QwenLM/qwen-code/releases

## 社区热点 Issues（Top 10）

### 1. Bailian Token Plan 模型列表不同步，图片/视频生成失败 — #8432
- 热度: 7 评论 | 1 👍 | 创建于 2026-08-03 | 状态: OPEN
- `/auth` 内置模型列表与阿里云百炼 Token Plan 个人版实际模型列表不同步，导致部分模型无法使用、图片/视频生成失败。
- 该 issue 同时牵出文档缺失问题（#10620），社区对 Token Plan 的完整支持呼声较高。
- 链接: https://github.com/QwenLM/qwen-code/issues/8432

### 2. `--approval-mode` / `--auth-type` 已注册但未出现在 `qwen --help` — #8897
- 热度: 6 评论 | 状态: CLOSED
- CLI 已接受并校验这两个参数，但 help 输出缺失，CLI 可发现性差。
- 链接: https://github.com/QwenLM/qwen-code/issues/8897

### 3. `task_list` 将空白可选过滤器视为活跃过滤器 — #9281
- 热度: 5 评论 | 状态: CLOSED
- `owner` / `blockedBy` 字段序列化为空字符串时，工具显示文本与 store 过滤逻辑不一致，返回 "No tasks found."。
- 链接: https://github.com/QwenLM/qwen-code/issues/9281

### 4. PR #10532 延迟审查发现 — #10547
- 热度: 5 评论 | 状态: OPEN | Bot 创建
- 自动化审查发现的、超出原 PR 范围的问题，等待维护者跟进处理。
- 链接: https://github.com/QwenLM/qwen-code/issues/10547

### 5. worktree 的 settings.json 写入项目根目录而非 worktree 自身 — #8138
- 热度: 5 评论 | 状态: OPEN | welcome-pr
- worktree 隔离场景下，修改设置会写到全局/项目根目录，而非 worktree 的 `.qwen/settings.json`，配置隔离失效。
- 链接: https://github.com/QwenLM/qwen-code/issues/8138

### 6. 主分支 E2E CI 失败（自动跟踪）— #10356
- 热度: 5 评论 | 状态: CLOSED | Bot 创建
- 测试结果上报前 CI 已失败，按 commit 跟踪。此类 CI 失败 issue 今日有 7 例，为自动化流程的一部分。
- 链接: https://github.com/QwenLM/qwen-code/issues/10356

### 7. “Press ctrl+s to show more lines” 提示多余显示 — #10640
- 热度: 4 评论 | 状态: OPEN | P3/UI
- 实际没有更多内容时，agent 响应末尾仍频繁显示该提示，造成误导。
- 链接: https://github.com/QwenLM/qwen-code/issues/10640

### 8. `--resume` 可重建悬空无符号思考风险（PR #8260 修复被绕过）— #8535
- 热度: 4 评论 | 状态: OPEN | need-discussion
- `--resume` / `--continue` 可绕过 live session 路径的 `dropDanglingUnsignedTrailingThought` 修复，重建安全问题。
- 链接: https://github.com/QwenLM/qwen-code/issues/8535

### 9. 会话归档后可同时存在 active + archived 副本 — #9688
- 热度: 3 评论 | 状态: OPEN | P2/daemon
- 归档成功后，仍在运行的 writer 会用同一 session ID 重建 `chats/<session-id>.jsonl`，Web UI 出现活动与归档副本冲突。
- 链接: https://github.com/QwenLM/qwen-code/issues/9688

### 10. 长期运行工具期间 live session 恢复触发 30s drain 超时 — #9773
- 热度: 3 评论 | 状态: OPEN | P3/daemon
- #9705 修复了错误的占位符移除逻辑，但 live session 恢复路径的 UX 缺口仍然存在，需要专项设计。
- 链接: https://github.com/QwenLM/qwen-code/issues/9773

## 重要 PR 进展（Top 10）

### 1. feat(ipc): 跨会话 inbox 连接支持 per-session token 认证 — #10636
- 为实验性跨会话消息 inbox 增加连接级认证，每个 session 生成随机 token 并以 0600 权限发布在 registry 记录中。
- 链接: https://github.com/QwenLM/qwen-code/pull/10636

### 2. fix(web-shell): 保持手动会话名跨 `/clear` — #9260
- `/clear` 后 successor session 在首次 prompt 前持久化手动会话名，避免自动标题覆盖用户标签。
- 链接: https://github.com/QwenLM/qwen-code/pull/9260

### 3. feat(cli): `/cd` 后重新加载项目运行时 — #10263
- 事务性切换 settings 和文件监听，刷新 context files、权限、tools、hooks、skills、subagents、MCP servers 等运行时状态。
- 链接: https://github.com/QwenLM/qwen-code/pull/10263

### 4. feat(web-shell): 解除 dirty working tree 上 git 更新阻塞 — #10390
- pull 被未提交更改阻塞时，分支选择器提供两种解决路径，不再以一行错误告终。
- 链接: https://github.com/QwenLM/qwen-code/pull/10390

### 5. feat(web-shell): 从绑定 PR 的 closing references 派生 session issue bindings — #10425
- daemon 的 PR-state 刷新逻辑现在会跟踪 PR 的 `Fixes #N` 引用，并同步 issue 状态。
- 链接: https://github.com/QwenLM/qwen-code/pull/10425

### 6. fix(hooks): 关闭 hook 执行的四个信任边界漏洞 — #10427
- HTTP hooks 不跟随重定向、仓库控制的配置不再可触发任意的网络出口/代码执行等，为单 commit reopen。
- 链接: https://github.com/QwenLM/qwen-code/pull/10427

### 7. fix(cli): 输出语言文件不可写时不再启动崩溃 — #10455
- 全局配置目录不可创建（只读 home 或 root 残留）时，无保护的写入会抛出异常，现在优雅降级。
- 链接: https://github.com/QwenLM/qwen-code/pull/10455

### 8. feat(review): 多轮 review 以 fix-audit 形状运行 — #10136
- 可预测地进入 critical-only 发布姿态时，re-review 改为窄范围的 fix-audit，而非完整的第一轮形状。
- 链接: https://github.com/QwenLM/qwen-code/pull/10136

### 9. feat(review): 新增 prose-execution 审计与 counter-frame 审计 — #10221
- 补齐 #9655 事后分析中的最后两个审计视角，替换 #9717。
- 链接: https://github.com/QwenLM/qwen-code/pull/10221

### 10. feat(core): 对无 Ctrl+Y 场景自动重试瞬时网络错误（EOF）— #10347
- 将包装为 4xx 的低层网络错误（如 `400 network error ... EOF`）归类为可重试传输错误，适用既有有界自动重试。
- 链接: https://github.com/QwenLM/qwen-code/pull/10347

## 功能需求趋势

1. **更健壮的会话管理 / 恢复语义**：归档与活跃会话冲突（#9688）、恢复期间超时（#9773）、`--resume` 安全风险（#8535）、replay 收尾逻辑（#9953）——社区对会话生命周期的一致性和可预测性要求显著提升。
2. **Token Plan 认证与文档完善**：除 bug 报告 #8432 外，#10620 明确要求补齐 Token Plan 的端到端配置文档，涵盖 endpoint、region、env key 与 settings.json 示例。
3. **Web Shell / UI 体验打磨**：Home/End 键不生效（#10642）、多余提示信息（#10640）、会话 artifact 快照暴露（#10638）等小问题密集出现，反映 Web Shell 使用面扩大后对细节品质的要求。
4. **安全与信任边界**：review run 的信任锚点位于模型会话写面内（#10654）、hook 信任边界（PR #10427）、IPC 跨会话认证（PR #10636）——安全相关提案持续增多。
5. **自动清理与配置隔离**：`.qwen` 文件夹自动清理（#10641）与 worktree settings 写入隔离（#8138）体现出用户在长时间使用后对配置管理和存储卫生的关注。

## 开发者关注点

- **认证配置依然是最痛点**：Token Plan 模型列表不同步+文档缺失的组合，让付费用户难以放心切换认证方案；`--approval-mode` 等参数不出现在 help 中则进一步降低 CLI 可发现性。
- **会话状态不一致反复出现**：归档冲突、resume 安全风险、恢复超时等问题横跨 daemon、CLI、Web UI 三层，说明会话状态机的边界条件尚未收敛。
- **review 自动化强度较高但噪音需控制**：大量 autofix/skip、autofix/in-progress 的 CI 失败自动跟踪 issue 和 deferred review findings 产生了一定的信息噪音，社区希望聚焦 critical 修复、减少重复报告。
- **配置写入路径的隔离性**：worktree 场景下设置写入位置错误、输出语言文件不可写导致崩溃——小场景的边界处理问题虽不频繁，但一旦触发影响明显。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*