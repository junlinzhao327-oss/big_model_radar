# AI CLI 工具社区动态日报 2026-08-21

> 生成时间: 2026-08-20 22:49 UTC | 覆盖工具: 7 个

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

# Claude Code Skills 社区热点报告（截至 2026-08-21）

> 说明：PR 评论数在数据中显示为 `undefined`，本报告排序参考仓库 PR 列表“按评论数排序”结果，并综合 Issue 讨论热度、更新时间判断社区关注度。所有 PR 当前状态均为 **Open**。

## 1. 热门 Skills 排行

以下 8 个 PR 位于热门列表前列，代表社区当前最关注的 Skill 功能方向：

- **document-typography（#514）** — Open  
  功能：为 AI 生成的文档提供排版质量控制，重点解决孤行（1–6 个词溢出到下一行）、寡行段落（标题被留在页底）、编号错位等常见问题。  
  社区热点：这些排版问题几乎影响所有 Claude 生成的文档，用户普遍认为这是长期被忽视的“最后一公里”质量缺口。  
  [GitHub PR #514](https://github.com/anthropics/skills/pull/514)

- **ODT Skill（#486）** — Open  
  功能：支持创建、填充、读取 OpenDocument 格式文件（.odt/.ods），并能将 ODT 转换为 HTML；覆盖 LibreOffice 及 ISO 标准文档处理。  
  社区热点：企业和公共部门对开放格式的刚需，模板填充和 ODT→HTML 转换被反复提及。  
  [GitHub PR #486](https://github.com/anthropics/skills/pull/486)

- **skill-quality-analyzer & skill-security-analyzer（#83）** — Open  
  功能：两个元技能。前者从结构文档化、示例完整性等五个维度评估 Skill 质量；后者对 Skill 进行安全审查。  
  社区热点：呼应了“社区 Skill 质量参差不齐”和“安全信任边界”两大担忧，社区期待官方提供可复用的质量/安全校验工具。  
  [GitHub PR #83](https://github.com/anthropics/skills/pull/83)

- **frontend-design 改进（#210）** — Open  
  功能：修订既有 frontend-design Skill，目标是提升指令的可操作性和内部一致性，确保 Claude 能在单次会话中实际遵循每条指引。  
  社区热点：讨论焦点是 Skill 描述过于抽象、Claude 难以落地，需要更具体的行为引导。  
  [GitHub PR #210](https://github.com/anthropics/skills

---



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-21

## 1. 今日速览

昨日正式发布 `rust-v0.149.0`，新增交互式 `codex agents` 仪表板及 TUI 工作目录管理命令；社区端“恢复 /undo 功能”的呼声达到 394 👍，成为当前最强需求信号。与此同时，桌面端（macOS/Windows）的崩溃、认证失效与归档失败问题成为今日高频反馈焦点，官方已通过多轮 PR 在稳定性、MCP 与安全签名验证方面密集推进修复。

## 2. 版本发布

### rust-v0.149.0（正式版）
- 新增交互式 `codex agents` 仪表板，支持搜索、启动、打开、重命名、停止任务，并可配置快捷键（#39094 等）。
- 新增 `/cd`、`/pwd`、`/cwd` 命令，用于在 TUI 会话中管理工作目录（#38894）。

另有 `0.150.0-alpha.1`、`0.149.0-alpha.7` 等预发布版本迭代，无公开详情。

## 3. 社区热点 Issues（10 条）

### 1. 请求恢复 /undo 功能
- **#9203** | [链接](https://github.com/openai/codex/issues/9203)
- **👍 394 · 💬 71** · 开放中
- **为何重要**：/undo 被移除后，用户面临未跟踪文件被误删、未提交修改被覆盖时无法回退的问题。原 Issue 来自 1 月，至今仍是社区最高赞需求，说明该功能对日常安全操作不可缺失。

### 2. macOS 桌面版崩溃：Computer Use 反复生成进程并触发 V8 OOM
- **#38455** | [链接](https://github.com/openai/codex/issues/38455)
- **👍 13 · 💬 33** · 开放中
- **为何重要**：26.810.41047 版本在空闲状态下反复生成 187 个 computer-use 线程，最终因 Node.js OOM 崩溃（316 线程），严重影响 macOS 用户。

### 3. macOS：打开已有对话使 ChatGPT 认证失效并跳转登录
- **#39162** | [链接](https://github.com/openai/codex/issues/39162)
- **👍 21 · 💬 28** · 开放中
- **为何重要**：26.814.41407 版本打开历史会话即触发认证失效，导致用户被迫重新登录，属于阻断级回归。

### 4. 定时任务在成功运行后自动禁用
- **#38350** | [链接](https://github.com/openai/codex/issues/38350)
- **👍 0 · 💬 25** · 开放中
- **为何重要**：Web 端定时任务未经用户授权即在成功运行后自动切换为 paused，多个无关任务同时出现，自动化可靠性存疑。

### 5. 子代理导致异常磁盘占用
- **#34061** | [链接](https://github.com/openai/codex/issues/34061)
- **👍 2 · 💬 20** · 开放中
- **为何重要**：CLI 0.144.6 + gpt-5.6 下子代理产生大量磁盘写入，影响长期任务运行与磁盘寿命。

### 6. 分页历史记录丢失有效数据并复用序号
- **#35746** | [链接](https://github.com/openai/codex/issues/35746)
- **👍 0 · 💬 16** · 开放中
- **为何重要**：分页 Rollout 历史解码存在 Ordinal 复用与数据丢失，影响会话审计与恢复。

### 7. 中文界面将 xhigh / ultra 推理力度均渲染为“极高”
- **#31963** | [链接](https://github.com/openai/codex/issues/31963)
- **👍 5 · 💬 15** · 开放中
- **为何重要**：zh-CN 本地化错误导致用户无法区分高端推理档位，实测影响 GPT-5.6 Sol 模型选项选择。

### 8. Windows：子代理面板永久显示已完成代理为 Active
- **#38364** | [链接](https://github.com/openai/codex/issues/38364)
- **👍 0 · 💬 10** · 开放中
- **为何重要**：26.803.10989.0 中子代理执行完毕后 UI 状态不刷新，造成误判和无效等待。

### 9. Windows：无法归档对话
- **#39161** | [链接](https://github.com/openai/codex/issues/39161)
- **👍 13 · 💬 9** · 开放中
- **为何重要**：26.814.5167.0 中归档功能失效，且存在 app-server 相关复现路径，影响会话组织与清理。

### 10. MCP OAuth 生命周期与企业 SSO 不可靠
- **#35006** | [链接](https://github.com/openai/codex/issues/35006)
- **👍 0 · 💬 9** · 开放中
- **为何重要**：作为 MCP OAuth 生命周期管理跟踪 Issue，覆盖凭据存储与重认证等问题，是 Enterprise 用户在真实业务中接入 MCP 的关键阻碍。

## 4. 重要 PR 进展（10 条）

### 1. 为 Amazon Bedrock 模型启用多智能体 V1
- **#39804** | [链接](https://github.com/openai/codex/pull/39804)
- 因 Bedrock 不支持 multi-agent V2 所需 response items，统一将 Bedrock 目录归一化为 `MultiAgentVersion::V1`，覆盖远程目录与静态 Runtime 目录。

### 2. 刷新内置模型定义，新增 Daybreak Blue / Red
- **#39770** | [链接](https://github.com/openai/codex/pull/39770)
- 加入隐藏模型 Daybreak Blue 和 Daybreak Red；同步刷新能力、指令、plan 可用性和服务层元数据，并调整 auto-review 模型。

### 3. 升级 rmcp 至 3.1.3
- **#39798** | [链接](https://github.com/openai/codex/pull/39798)
- 升级 `rmcp`/`rmcp-macros`，保留 MCP 发现回退时的认证与重试语义，并修复无关错误误触发 legacy fallback 的问题。

### 4. TUI 状态栏可配置主机名
- **#39795** | [链接](https://github.com/openai/codex/pull/39795)
- 新增 `hostname` 状态栏项，不触发 DNS 解析，并在无可用主机名时自动省略。

### 5. 支持宿主接受的 exec-server WebSockets
- **#39786** | [链接](https://github.com/openai/codex/pull/39786)
- 新增 `from_accepted_websocket` / `replace_accepted_websocket`，便于宿主以已认证的 Axum WebSocket 构建远程环境。

### 6. 独立工具输出视为外部上下文并污染记忆
- **#39791** | [链接](https://github.com/openai/codex/pull/39791)
- 无 `call_id` 的 `function_call_output` 被视为外部上下文，且当 `memories.disable_on_external_context` 开启时标记记忆模式为 polluted。

### 7. 拒绝父拥有子代理的设置更新
- **#39792** | [链接](https://github.com/openai/codex/pull/39792)
- 将现有直接输入限制扩展至 `thread/settings/update`，防止父拥有的 Multi-Agent V2 子代理越权修改设置。

### 8. 支持自定义模型提供商的轮次成本遥测
- **#39785** | [链接](https://github.com/openai/codex/pull/39785)
- 非 OpenAI 提供商的 turn-cost 查询走各自 endpoint 与认证，保留原 OpenAI API-key 路径并排除 Bedrock。

### 9. 启动/安装前校验 Codex 应用签名
- **#39776** | [链接](https://github.com/openai/codex/pull/39776

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 2026-08-21

## 今日速览

今日最值得关注的是两个高优先级核心 Bug 修复 PR：`GIT_CONFIG_*` 环境变量错误导致所有 git 命令失败，以及中断响应占位符被持久化污染上下文的修复。社区侧，子代理状态误报问题持续发酵（#22323，共 12 条评论），多个关于子代理挂起、浏览器代理 Wayland 兼容性、命令卡死的问题仍在开放状态等待处理。新版本方面，今日发布了 v0.56.0-nightly.20260820 更新。

## 版本发布

**v0.56.0-nightly.20260820.ge90c63fa1** [查看详情](https://github.com/google-gemini/gemini-cli/releases/tag/v0.56.0-nightly.20260820.ge90c63fa1)

- 修复(core)：保留带有工具或媒体的空文本轮次（感谢 @DavidAPierce，[PR #28892](https://github.com/google-gemini/gemini-cli/pull/28892)）
- 更新 v0.57.0-preview.0 的 Changelog

## 社区热点 Issues（10 条精选）

### 1. Subagent 达到 MAX_TURNS 后被误报为 GOAL 成功（#22323）
**高赞/热议** | P1 | 评论 12 | 👍 2
`codebase_investigator` 子代理实际已触发最大轮次限制，却报告 `status: "success"` 和 `Termination Reason: "GOAL"`，掩盖了真实的中断原因。这直接影响用户对子代理执行结果的信任。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/issues/22323)

### 2. 通用代理（Generalist agent）挂起永不返回（#21409）
**高赞/热议** | P1 | 评论 8 | 👍 8
当 Gemini CLI 委派给通用代理时，任务会无限期挂起，简单的文件夹创建操作也要等待一小时。通过指示模型不使用子代理可以绕过，说明问题出在子代理调度或执行链路。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/issues/21409)

### 3. 零依赖 OS 沙箱与执行后意图路由（#19873）
P2 | 评论 8 | 大型改进
提案建议利用 Gemini 3 模型原生 bash 操作能力，通过零依赖 OS 沙箱实现安全的命令执行，并在执行后做意图路由，兼顾模型偏好与用户安全。属于架构级改进方向。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/issues/19873)

### 4. Gemini 不主动使用 skills 和子代理（#21968）
P2 | 评论 6
社区反馈 Gemini 几乎不会自主调用自定义 skills 和子代理，即使有明确的描述匹配也不主动使用，降低了高级功能的实际价值。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/issues/21968)

### 5. Shell 命令执行完成后卡在 "Waiting input"（#25166）
**高赞** | P1 | 评论 4 | 👍 3
执行简单的 CLI 命令后，Gemini 持续显示命令处于活动状态并等待用户输入，即使命令早已完成。该问题可稳定复现，影响日常交互效率。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/issues/25166)

### 6. 超过 128 个工具时遭遇 400 错误（#24246）
P2 | 评论 3
当可用工具超过 128 个（实际触发于 400 个），Gemini CLI 会报 400 错误。期望能智能限制工具范围，而非简单报错。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/issues/24246)

### 7. Browser 子代理在 Wayland 环境下失败（#21983）
P1 | 评论 4 | 👍 1
浏览器子代理在 Wayland（Linux）环境启动失败，影响 Linux 桌面用户使用浏览器自动化能力。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/issues/21983)

### 8. get-shit-done 输出钩子导致崩溃（#22186）
P1 | 评论 3
当 get-shit-done 输出接近完成（打印用户摘要）时，会反复导致 Gemini CLI 崩溃，属于高影响稳定性问题。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/issues/22186)

### 9. Auto Memory 对低信号会话无限重试（#26522）
P2 | 评论 5
Auto Memory 将未读的低信号会话反复标记为未处理，导致后台提取代理对同一批会话无限重试，浪费资源。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/issues/26522)

### 10. 子代理轨迹应可通过 `/chat share` 可见（#22598）
P3 | 评论 2 | 👍 1
子代理轨迹已由聊天记录服务保存，但没有便捷的查看和分享方式。社区建议通过 `/chat share` 暴露子代理执行轨迹，便于审查和评估。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/issues/22598)

## 重要 PR 进展（10 条精选）

### 1. 修复 `GIT_CONFIG_*` 环境变量不一致（#28938）
**P1 | 核心 | 大型**
`sanitizeEnvironment()` 可能生成 git 无法解析的 `GIT_CONFIG_*` 环境变量，导致所有 git 命令直接失败（已在 git 2.50.1 复现）。属于影响面广泛的严重修复。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/pull/28938)

### 2. 修复中断响应占位符被持久化的问题（#28939）
**核心 | 大型**
中断的工具响应轮次后，Gemini CLI 会在历史中插入 `[The previous response was interrupted before it completed.]` 文本，该文本被当作模型消息持久化并在后续请求中重复发送，污染上下文。此 PR 修复该问题（Fixes #28927）。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/pull/28939)

### 3. 历史回滚与重试提示优化（#28934）
**大型**
优化工具调用取消和重试提示逻辑，避免上下文窗口膨胀，减少 API 请求量，并通过前缀缓存最大化重试效率。做法是取消时回滚合成文本而非追加。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/pull/28934)

### 4. macOS Seatbelt 沙箱隔离容器运行时（#28935）
**大型 | 安全**
在 macOS Seatbelt 沙箱配置中显式拒绝 Docker/容器运行时的 UNIX 套接字、CLI 二进制、Mach/XPC 服务查找和 POSIX 共享内存访问，防止通过 VirtioFS 等容器超管文件系统挂载实现沙箱逃逸。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/pull/28935)

### 5. 移除不安全的 `diff.external` 覆盖（#28930）
**P1 | 核心 | 安全**
PR #28792 添加了 `['diff.external', '']` 以禁用外部 diff 工具，但 git 不将空值视为“未设置”，而是报错。此 PR 移除该不安全覆盖（Fixes #28928）。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/pull/28930)

### 6. 新增 Gemini 3.7 Flash / 3.6 Flash 模型支持（#28910）
**P2 | 核心/CLI | 超大型**
为 `packages/core` 和 `packages/cli` 添加 Gemini 3.7 Flash、3.6 Flash 和 3.5 Flash-Lite 的完整模型解析与选择配置。注意：该 PR 已被关闭，可能因需要返工或已合入其他分支。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/pull/28910)

### 7. 预览模型静默替换时发出警告（#28828）
**P1/P2 | 代理**
当用户请求预览模型（如 `gemini-3.1-pro-preview`）但账户无对应权限时，`Config` 会静默降级为 `auto-gemini-2.5` 且无任何提示。此 PR 增加显式警告（Fixes #28825）。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/pull/28828)

### 8. 扩展程序环境变更需用户同意并清理环境变量（#28863）
**中等 | 安全**
修复扩展更新可能绕过用户同意、向 MCP 服务注入未经授权环境变量的问题。将 MCP 服务器环境配置纳入同意字符串，并清理可改变运行时行为的自定义环境变量。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/pull/28863)

### 9. 禁止在 agents mode 禁用时运行子代理（#28867）
**P2 | 代理 | 回归修复**
修复 v0.33.0 引入的回归：即使用户在配置中禁用了 agents mode，子代理（如通用代理）仍会被初始化和运行。此 PR 修复 #22093。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/pull/28867)

### 10. Whisper 模型原子下载与失败清理（#28917）
**核心 | 稳定**
`WhisperModelManager.downloadModel()` 改为写入临时文件（`.downloading`），处理后端压力和流错误，校验下载长度，失败自动清理，最后原子重命名，避免下载中断留下损坏文件。
[GitHub 链接](https://github.com/google-gemini/gemini-cli/pull/28917)

## 功能需求趋势

从今日活跃的 Issues 和 PR 中，社区最关注的方向集中在：

| 方向 | 关注点 | 代表 Issue/PR |
|------|--------|--------------|
| **子代理可靠性** | 状态误报、挂起、不主动调用 | #22323、#21409、#21968 |
| **安全性增强** | 沙箱隔离、环境变量清理、拒绝危险命令 | PR #28935、#28863、#28930、Issue #22672 |
| **记忆系统完善** | Auto Memory 质量、重试策略、信息脱敏 | #26522、#26525、#26516 |
| **文件处理智能化** | AST 感知读取/搜索/映射，减少 token 消耗 | #22745、#22746、#19561 |
| **配置灵活性与一致性** | symlink 识别、settings.json 覆盖、路径规范化 | #20079、#22267、PR #28915 |
| **上下文窗口优化** | 重试时避免膨胀、前缀缓存、取消回滚 | PR #28934、#28939、#19561 |

## 开发者关注点

社区高频痛点和核心诉求主要集中在以下几个层面：

1. **子代理状态报告不可信**：#22323 中“达到 MAX_TURNS 被误报为 GOAL 成功”的问题，加上 #21409 的挂起问题，说明子代理生命周期管理和状态传递仍存在系统性缺陷，开发者据此难以判断任务真实执行情况。

2. **环境变量处理引发连锁故障**：PR #28938 和 #28930 都指向环境变量清理逻辑的不完善——前者导致 `GIT_CONFIG_*` 畸形而使所有 git 命令失败，后者暴露空值覆盖 `diff.external` 导致的报错。这两处问题对日常开发流程影响极大。

3. **命令执行卡死**：#25166 中命令完成后仍显示“等待输入”，以及 #22465 中交互式提示（如 `vite` 创建）卡住，表明 CLI 对子进程交互的边界处理不够健壮。

4. **配置/文件系统边界情况支持不足**：`settings.json` 覆盖被忽略（#22267）、symlink 不被识别（#20079)、ignore 路径处理不一致（PR #28915）等，属于高频率边界场景问题。

5. **上下文管理与 token 经济性**：#19561 提出的“Tactful Extraction”方案和 PR #28934 的优化方向表明，开发者对上下文膨胀、前缀缓存效率和 token 消耗持续关注。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-08-21）

## 今日速览

今日发布 v1.0.81-6 和 v1.0.81-5 两个版本，主要新增默认启动模式/权限配置和 `--with-token` 登录方式，并修复了 pending 状态残留问题。社区方面，MCP 服务器连接与认证问题、沙箱权限限制、会话状态丢失仍是讨论焦点；此外出现了一个值得警惕的 PR：试图将 CLI 文档从 README 中完全移除。

## 版本发布

### v1.0.81-6
- **新增**：`defaultMode` 与 `defaultPermissionMode` 设置，可在新交互会话中预设启动模式和审批行为；`copilot login` 新增 `--with-token`，支持从 stdin 读取认证 token。
- **改进**：ACP 客户端现在可获得 subagent ID、raw 事件订阅及实时标题/模型信息。

### v1.0.81-5
- **修复**：agent 工作期间发送新的 prompt 后，不再在 transcript 底部残留一份卡在 `(pending)` 状态的重复副本。

发布链接：https://github.com/github/copilot-cli/releases

## 社区热点 Issues

以下为过去 24 小时内最值得关注的 10 个 Issue（按评论数/影响力排序）：

### 1. [#1481 SHIFT+ENTER 应当换行，却触发了执行（28 评论 / 17 👍）](https://github.com/github/copilot-cli/issues/1481)
绝大多数聊天应用使用 SHIFT+ENTER 换行，而 Copilot CLI 将其绑定为执行 prompt，反向使用 CTRL+ENTER 换行，用户体验与直觉相悖。该 issue 已关闭，社区普遍认为是高优先级交互缺陷。

### 2. [#4390 组织启用的模型缺失（Claude Sonnet 5/Opus 5、Kimi K3）（15 评论 / 7 👍）](https://github.com/github/copilot-cli/issues/4390)
Copilot Business 组织已显式启用的 Anthropic 模型在 CLI 中不可用，选择 `claude-sonnet-5` 会提示 "disabled by your organization"。这属于企业模型目录同步问题，影响面较大。

### 3. [#3162 1.0.42 将 registry 中已列出的 MCP 服务器误报为策略拦截（7 评论）](https://github.com/github/copilot-cli/issues/3162)
自定义 MCP 服务器已在官方 registry 中登记，但 CLI 仍判定为 "blocked by policy"。疑似 registry 校验/匹配逻辑存在误报。

### 4. [#4096 第三方 MCP 在 App 中显示 Connected，但工具未同步到 CLI 会话（6 评论 / 2 👍）](https://github.com/github/copilot-cli/issues/4096)
通过 App UI 登录 Atlassian Remote MCP 后，会话中工具始终不可用，提示与 OAuth token 未桥接到 CLI 会话有关。MCP 生态的连通性仍是高频痛点。

### 5. [#4503 SDK server 未认证便报告就绪，Slack 会话创建泛化失败（5 评论）](https://github.com/github/copilot-cli/issues/4503)
SDK 服务器启动时环境缺少 `COPILOT_SDK_AUTH_TOKEN`，但自检报 ready，导致后续 Slack 会话创建失败。属于早期错误检测缺位问题。

### 6. [#4439 1.0.79 拒绝 GitLab MCP OAuth 元数据（RFC 8414 issuer mismatch）（5 评论 / 3 👍）](https://github.com/github/copilot-cli/issues/4439)
GitLab Self-Managed MCP 使用 OAuth 2.0 动态注册时，CLI 因 issuer 校验不匹配而拒绝认证。影响自托管 GitLab 用户接入 MCP。

### 7. [#4206 环境 footer 永远卡在 "Loading:"（4 评论 / 3 👍）](https://github.com/github/copilot-cli/issues/4206)
状态栏显示 "◎ Loading: 1 instruction, 40 skills, ..." 永不结束，但 `/env` 实际已加载完成。属于状态同步问题，易误导用户。

### 8. [#4038 非交互模式：MCP 服务器晚到注入空用户消息（3 评论）](https://github.com/github/copilot-cli/issues/4038)
`copilot -p` 在 MCP 服务器暴露 7+ 工具时，会在真实 prompt 后附加一条空用户消息，模型转而回复空消息，甚至回显系统 prompt。非交互管道受影响严重。

### 9. [#4524 沙箱禁止 Copilot 使用 git（3 评论）](https://github.com/github/copilot-cli/issues/4524)
在强制沙箱最新版中，即使用户放行了整个工作目录，git 命令仍无法执行。反映沙箱策略限制过度、配置复杂。

### 10. [#4535 store_memory 在 v1.0.81 预发布版中报 "Instance id is required"（3 评论）](https://github.com/github/copilot-cli/issues/4535)
原生内存写入器被调用时缺少实例 ID，`store_memory` 功能在新版本预发布中完全不可用。涉及隐私/状态持久化能力，值得跟进。

## 重要 PR 进展

过去 24 小时内仅有 1 条 PR 更新：

### [#4510 [OPEN] Remove GitHub Copilot CLI documentation from README](https://github.com/github/copilot-cli/pull/4510)
作者：@prioritizedprotection086 | 创建：2026-08-17 | 更新：2026-08-20

该 PR 将 README 中关于 Copilot CLI 的安装说明、使用指南等详细信息全部删除。这是一个非常不寻常的变更——移除项目的核心文档入口通常属于恶意行为或内部策略调整。鉴于该 PR 仍处于开放状态，建议社区密切关注其动机与后续讨论，谨慎合并。

## 功能需求趋势

从今日的 Issues 中可以提炼出以下社区最关注的功能方向：

1. **MCP 生态成熟度**（#3162、#4096、#4439、#4542、#4038）
   MCP 连接、OAuth 认证、工具可见性、策略校验等方面暴露大量问题，社区对 MCP 的稳定性预期远高于当前实现。

2. **权限与沙箱精细化**（#4524、#4546、#4528、#4349）
   多个 issue 指向沙箱过于严格或行为异常，而企业 managed settings 的 `disableBypassPermissionsMode` 在非交互模式下可被绕过，权限模型需要更一致的设计。

3. **会话持久化与跨环境恢复**（#4529、#4539、#4543）
   WSL2、Remote-SSH、Ctrl+Z 重启等场景下会话状态丢失或双数据库分裂，开发者希望会话能跨主机/终端环境无缝恢复。

4. **终端交互体验优化**（#1481、#4447、#4532、#4544）
   快捷键语义、按词删除、pending 行重复、图片粘贴等细节问题频发，说明终端 UI 的打磨仍需加强。

5. **企业策略兼容性**（#4390、#4349、#4528）
   企业用户在启用托管策略后遭遇模型不可见、策略校验失败、非交互绕过等矛盾行为，企业特性与本地配置的协调机制需改进。

## 开发者关注点

- **快捷键与通用习惯严重偏离**：SHIFT+ENTER 无法换行、Backspace 整词删除，基本输入体验仍不符合用户预期。
- **MCP 认证与连通性是最大痛点**：无论是 GitLab 自托管 OAuth 还是 Atlassian 远程 MCP，OAuth token 在 App/CLI 间的桥接反复出问题。
- **沙箱启用后功能不可用**：git、VS Code remote、wslpath 等常见工具在沙箱中失效，用户配置成本高且缺少明确报错指引。
- **非交互模式（-p/--prompt）在特定条件下被污染**：MCP 晚连接注入空消息、权限绕过企业设置，自动化管道受影响严重。
- **会话状态可靠性不足**：从 WSL/Remote-SSH 断开恢复到内存 store_memory 失败，会话数据的持久化与同步机制亟需加固。
- **Windows 系问题集中**：wta.exe 启动路径引号错误、WebView2 渲染器崩溃、Git 配置块破坏 VS Code 发现，Windows/WSL 环境需要专项适配。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-08-21

## 今日速览

过去 24 小时无新版本发布，社区活跃度集中在插件生态的基础能力建设上：一个围绕「工作区级长期记忆」的功能提案（#2613）与一份插件安全/数据持久化文档 PR（#2614）同步出现，暗示插件机制进入深化阶段。目前 Issue 与 PR 数量均以 1 条新增为主，整体社区讨论处于平稳蓄力期。

---

## 版本发布

过去 24 小时无新的 Release。

---

## 社区热点 Issues

> 过去 24 小时内更新共 1 条 Issue，已全部列出。

### 1. Kimi Memory Plus — 工作区范围的长期记忆插件提案
**#2613 | [OPEN] | [enhancement] | 作者: @QIANLING-0831 | 👍 0**

**地址**: https://github.com/MoonshotAI/kimi-cli/issues/2613

**核心内容**：提出一种名为「Kimi Memory Plus」的插件方案，为工作区提供长期记忆能力。

**为什么值得关注**：
- 这是当前唯一处于活跃讨论中的功能提案，反映了开发者对“跨会话上下文保持”的明显需求。
- 提案中特别提到一个**兼容性发现**：当前 Kimi Code CLI 已能将显式记忆工具注册为 stdio MCP 服务器，但**尚未识别该仓库中的实验性实现**——这意味着插件/MCP 基础设施本身已具备基本条件，但官方侧的识别与接入仍缺一环。
- 作者在原提案基础上于 2026-08-21 做了「Compatibility update」，说明提案正在持续迭代，并非一次性抛出。

**社区反应**：暂无评论，处于早期讨论阶段，有待官方或社区贡献者给出可执行性评估。

---

## 重要 PR 进展

> 过去 24 小时内更新共 1 条 PR，已全部列出。

### 1. docs(plugins): 补充插件安全性与持久化数据文档
**#2614 | [OPEN] | 作者: @QIANLING-0831 | 链接**: https://github.com/MoonshotAI/kimi-cli/pull/2614

**Summary 解读**：
- 明确插件工具以**本地子进程**形式运行，并拥有当前用户级别的文件与网络访问权限（对安全边界做了透明化说明）。
- 在文档中补充 `inject` 凭据处理的说明，并明确提出**警告**：不应将注入值写入日志或提交到版本库。
- 澄清重新安装插件会**覆盖其已安装目录**，防止使用者误以为会增量合并。
- 推荐采用独立目录等方式隔离插件持久化数据（其余内容涉及相关最佳实践）。

**影响评估**：这是一份偏工程化、安全规约性质的文档 PR，填补了插件机制在“权限模型”“凭据管理”“状态持久化”三个方向上的空白。

---

## 功能需求趋势

基于当前全部活跃 Issues（#2613 等），可提炼出以下趋势信号：

| 趋势方向 | 说明 |
|---|---|
| **工作区级长期记忆** | 社区希望 CLI 具备跨会话、持久化的上下文能力，而不仅限于单次对话窗口。 |
| **MCP 生态适配** | 显式记忆工具通过 stdio MCP 服务注册已可行，但官方对实验性实现尚未识别，说明 MCP 是当前扩展能力的重要载体。 |
| **插件安全与数据管理** | 围绕插件运行权限、凭据安全、重装行为、数据持久化的讨论 / 文档需求正在上升，体现出社区开始关注插件机制的工程化质量。 |

---

## 开发者关注点

根据现有 Issue / PR 反馈，开发者主要关注：

1. **上下文连续性缺失**：工作区级记忆缺失是目前最突出的功能痛点，开发者期望 CLI 能记住项目维度的“历史背景”，而非仅依赖每次会话的短时上下文。
2. **插件能力接入一致性**：MCP 服务虽可注册，但官方对实验性插件的识别存在“断层”，希望官方尽快补齐对社区实验性扩展的正式支持。
3. **安全边界清晰化**：开发者对插件子进程权限范围（文件/网络）、注入凭据保护、重装覆盖等行为存在不确定性，需要官方文档提供明确约定。

---

*数据来源: [github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli) | 统计周期: 2026-08-20 ~ 2026-08-21*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

## OpenCode 社区动态日报（2026-08-21）

> 数据来源：github.com/anomalyco/opencode

## 📌 今日速览

- v1.18.19 发布，带来 Cloudflare AI Gateway 模型的原生 OpenAI/Anthropic 透传支持，并进一步对齐 Codex 速率限制与 ChatGPT 订阅限制。
- 社区关注焦点集中在 **2.0 版本 subagent 会话阻断问题**（#43619）和 **Web UI 终端按钮消失**（#30158）两大顽固缺陷上，多条相关 Issue 讨论热度持续攀升。
- 内存泄漏（#35107、#34574）与 TUI 渲染/性能问题（#20458、#42657）仍是开发者高频反馈的稳定性痛点。

---

## 🚀 版本发布

### v1.18.19

**核心改进**
- **Cloudflare AI Gateway 原生透传**：新增对 OpenAI 和 Anthropic 模型的原生透传支持，提升网关场景下的兼容性与稳定性。
- **Codex 速率限制更贴近 ChatGPT 订阅限制**：感谢 @GameOn223 的贡献，费率控制策略现在与订阅模型对齐，避免误判。

**Bug 修复**
- 移除内置的 Qwen 采样默认值，该配置此前可能向模型发送不支持的自定义采样参数。
- 另有部分修复描述未完整披露，详细内容请见仓库 Release 页面。

---

## 🔥 社区热点 Issues

### 1. Web UI 终端按钮神秘消失（#30158）
- **状态**：OPEN | **评论**：12 | **👍**：14
- `v1.15.12` 起，Web UI 右上角终端按钮及若干其他图标消失，降级到 `v1.15.11` 即恢复。作为影响范围广泛且持续数月未解决的 UI 回归，社区关注度极高。
- https://github.com/anomalyco/opencode/issues/30158

### 2. [2.0] subagent 工具强制要求 sessionID，阻断首个子会话创建（#43619）
- **状态**：OPEN | **评论**：9 | **👍**：0
- 2.0 的 `subagent` 工具文档要求省略 `sessionID` 以创建新会话，但实际暴露的 schema 却强制要求该字段。这直接阻断所有需要委派首个 child agent 的编码工作流，属于 2.0 关键阻断性缺陷。
- https://github.com/anomalyco/opencode/issues/43619

### 3. TypeError: Failed to fetch（#27474）
- **状态**：OPEN | **评论**：10 | **👍**：0
- 点击 "explore" 或智能体入口时，若未能正确跳转到子 agent，控制台即抛出 `TypeError: Failed to fetch`。该问题在中文用户中引发大量反馈。

- https://github.com/anomalyco/opencode/issues/27474

### 4. 安装脚本忽略 OPENCODE_INSTALL_DIR 环境变量（#7675）
- **状态**：CLOSED | **评论**：10 |

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*