# AI CLI 工具社区动态日报 2026-08-23

> 生成时间: 2026-08-22 22:42 UTC | 覆盖工具: 7 个

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

# Claude Code 社区动态日报 — 2026-08-23

## 今日速览

- **Anthropic 发布 v2.1.240**，内容为 bug 修复与可靠性改进，无新功能声明。
- **社区最高热度的 #27302（同一 Connector 多账户支持）已悬挂 6 个月**，获 357 👍、234 评论，是目前最强烈的功能需求信号。
- **Hook 系统可靠性成为今日关键词**：Windows 上 PreToolUse 完全不触发（#88896）、子代理 Hook 静默跳过（#69260）、禁用插件 Hook 仍在执行（#85893）等问题密集出现；同时约 20 条 7 月初创建的旧 Issue 被统一标记为 `stale` 关闭。

## 版本发布

**v2.1.240**
- 仅包含 "Bug fixes and reliability improvements"，未说明具体修复项，建议关注 Hook、会话持久化相关问题的修复验证。

## 社区热点 Issues

### 🔥 开放中

1. **[#27302] 支持同一 Connector 的多个账户（Claude Code Web / claude.ai）** — `enhancement` / `area:auth`
   - 状态：OPEN ｜ 234 评论 ｜ 357 👍（全场最高）
   - 意义：涉及多账户（相同 Connector、不同账号）在 Claude 与 Claude Code Web 端的切换需求，自 2 月提出至今仍未落地，是社区呼声最大的认证类功能缺口。
   - 链接：https://github.com/anthropics/claude-code/issues/27302

2. **[#75037] 后台代理会话故障：快速终止、attach 时 worker 崩溃循环、丢失后台任务完成记录** — `bug` / `platform:macos` / `area:agent-view`
   - 状态：OPEN ｜ 9 评论
   - 意义：影响 `claude --bg` / `/bg` 派发长任务后再 attach 的核心工作流，三个独立故障（快速终止、崩溃循环、完成记录缺失）直接影响自动化可靠性，后台代理用户应重点关注。
   - 链接：https://github.com/anthropics/claude-code/issues/75037

3. **[#88896] Windows 上 PreToolUse Hook 完全不触发（v2.1.240）** — `bug` / `platform:windows` / `area:hooks`
   - 状态：OPEN（昨日新建）｜ 1 评论
   - 意义：最新版中 Windows 平台所有工具调用的 `PreToolUse` 静默失效，而 `SessionStart`/`Stop` 等 Hook 正常。安全审计类 Hook 失效意味着**防护链路断档**，是 Windows 用户当前最紧急的 bug。
   - 链接：https://github.com/anthropics/claude-code/issues/88896

4. **[#88383] 2.1.238 回归：交互式 CLI 会话把 thinking 存为签名空壳（thinking: ""）** — `bug` / `regression` / `area:core`
   - 状态：OPEN ｜ 3 评论 ｜ 1 👍
   - 意义：2.1.238 起，`entrypoint: "cli"` 的交互会话在 JSONL 中只落盘 `{"type":"thinking","thinking":"","signature":"<sig>"}` 空壳，与 #87947 中 print 模式问题同形。影响会话回放、记忆提取与工具链兼容性，且为版本回归。
   - 链接：https://github.com/anthropics/claude-code/issues/88383

### ✅ 今日关闭（含 stale 清理）

5. **[#69260] PreToolUse Hook 对子代理（Agent 工具）静默跳过** — `bug` / `area:hooks` / `area:agents`
   - 状态：CLOSED（需更多信息）｜ 6 评论 ｜ 2 👍
   - 意义：主代理 Hook 正常、子代理全部绕过，导致命令改写/安全检查只覆盖部分工具调用。与 #86405 重复，#86405 同样被关闭，说明 Anthropic 已了解该路径问题。
   - 链接：https://github.com/anthropics/claude-code

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-23

## 今日速览

macOS 与 Windows 客户端的会话/认证稳定性问题集中爆发，多条高赞 Issue 指向“打开旧会话导致重新登录”和系统级性能失控（`syspolicyd`/`trustd` CPU 飙升）。与此同时，GPT-5.6 显式 prompt 缓存与远程控制等新能力成为社区呼唤的焦点。MCP 相关内部 PR 密集合并，反映出运行时连接治理正在加速演进。

## 版本发布

过去 24 小时发布了两个预发布版本（来自 GitHub Releases）：

- **[rust-v0.150.0-alpha.7](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.7)** — 0.150.0-alpha.7
- **[rust-v0.149.0-alpha.7.2](https://github.com/openai/codex/releases/tag/rust-v0.149.0-alpha.7.2)** — 0.149.0-alpha.7.2

均为 patch 级预发布，未附带详细变更说明。

## 社区热点 Issues

以下 10 条 Issue 按社区关注度、影响面与时效性综合选取：

1. **[Codex Desktop for macOS 反复触发 `syspolicyd`/`trustd` CPU 与内存失控](https://github.com/openai/codex/issues/25719)** 👎 394 👍 85 条评论
   持续近 3 个月的最热 Issue。Codex Desktop 在运行期间反复唤醒 macOS 安全组件导致 CPU/内存占用异常，迄今未关闭。影响 Plus 用户、Apple Silicon 平台，是当前 macOS 端最严重的性能问题。

2. **[macOS 打开已有会话会使 ChatGPT 认证失效并跳转登录](https://github.com/openai/codex/issues/39162)** 👍 26 · 37 条评论
   8 月 18 日新建，迅速升温。用户在 26.814.41407 上打开历史会话时被强制登出，上一个正常版本 26.810.52044 无此问题，疑似新引入的认证回归。

3. **[ChatGPT Desktop 反复生成 Computer Use worker 并以 V8 OOM 崩溃](https://github.com/openai/codex/issues/38455)** 👍 15 · 36 条评论
   空闲状态下启动 98 秒后即崩溃，崩溃时 316 个线程中 187 个与 computer-use 相关。32GB 内存的 Apple Silicon 设备可复现，旧版本 26.730.61639 正常，属于明显的版本回归。

4. **[Native Bedrock GPT-5.6 Sol 缺少显式缓存控制，产生高额 cache-write 支出](https://github.com/openai/codex/issues/37674)** 👍 12 · 13 条评论（已关闭）
   使用 Bedrock Mantle 接入 GPT-5.6 Sol 时无法开启显式 prompt 缓存，导致 agentic 编码任务产生大量 cache-write token，成本显著上升。与 #35300 同源，但提供了独立生产环境证据。

5. **[Claude Code 式远程控制功能请求](https://github.com/openai/codex/issues/27565)** 👍 15 · 12 条评论
   社区希望 Codex CLI 能像 Claude Code 的 `/remote-control` 一样，让手机 App 直接接管 CLI 会话，免去 SSH 隧道与消息同步的复杂度。该诉求已持续两个月，反应了跨端协作的真实需求。

6. **[WSL 环境自定义 Pets 因路径归一化无法加载](https://github.com/openai/codex/issues/20730)** 👍 28 · 23 条评论
   Windows + WSL 环境下自定义 Pets 目录因路径归一化失效。Pets 是 Codex 桌面端的个性化功能，该问题在 5 月提出后仍开放，说明跨平台路径兼容性尚未解决。

7. **[Windows 打开已有线程会将个人 Pro 账户登出](https://github.com/openai/codex/issues/39189)** 👍 4 · 17 条评论
   与 #39162 极为相似，但发生在 Windows 端。工作区权限 401 后，个人 Pro 账户被意外登出。桌面客户端 26.814.41407、Codex core 0.148.0 可复现，认证边界处理存在缺陷。

8. **[Codex 无法生成 `prompt_cache_breakpoint`，GPT-5.6 稳定前缀无法复用](https://github.com/openai/codex/issues/35300)** 👍 4 · 6 条评论
   GPT-5.6 支持显式 prompt 缓存断点，但 Codex 自身生成的内容块不支持该字段，导致稳定启动前缀无法复用。Codex 仓库自带的迁移指南已描述此问题，属于“自己已知但未修复”的典型。

9. **[`apply_patch` 可绕过批准修改可写根目录之外的文件](https://github.com/openai/codex/issues/31434)** 👍 0 · 3 条评论
   安全相关。在 WSL 环境中，`apply_patch` 可以修改可写根之外的文件且不触发审批。虽然关注度不高，但属于沙箱逃逸类风险，值得安全团队优先评估。

10. **[CLI 0.149.0 认证头未发送，ChatGPT 登录模式返回 401](https://github.com/openai/codex/issues/39883)** 👍 0 · 2 条评论
   0.149.0 引入的认证回归：ChatGPT 登录模式下请求不再携带认证头，0.148.0 正常。虽评论不多，但直接影响所有 CLI 登录用户，是新版本常见事故类型。

## 重要 PR 进展

过去 24 小时共合并 4 个 PR，均为 `copyberry[bot]` 提交并已关闭，聚焦 MCP 运行时治理与会话生命周期：

1. **[Use thread source metadata for Guardian classifiers](https://github.com/openai/codex/pull/40150)**
   为 Guardian 分类器请求添加 `thread_source` 元数据，移除分类器专用的 `request_kind`/`is_guardian_mode` 字段，同步更新 sampler 与扩展测试。属于可观测性/审计层面的基础设施改进。

2. **[Report runtime MCP connection status](https://github.com/openai/codex/pull/40068)**
   在 `mcpServerStatus/list` 中新增可空 `runtimeStatus` 字段，用于反映线程实时连接状态，解决 MCP 清单缓存与真实连接状态脱节的问题。

3. **[Add unfinished root turn suspension](https://github.com/openai/codex/pull/40038)**
   新增 `CodexThread::suspend_turn_and_shutdown` 与 `SuspendTurnOutcome`，使活跃根 turn 可在不标记完成/中止的情况下被挂起，为其他运行时恢复同一 turn ID 创造前提。

4. **[Preserve strict MCP auto-review outcomes](https://github.com/openai/codex/pull/40031)**
   严格模式下 MCP 自动审查的拒绝、超时、中止响应将被透传，保留审查者的理由与元数据，不再替换为通用拒绝。默认仍保持 fail-closed 行为。

## 功能需求趋势

从近 24 小时 Issues 与 PR 中可提炼出以下社区最关注的功能方向：

- **远程控制与会话转移**：`#27565`（Claude Code 式远程控制）与 `#40055`（CLI ↔ Desktop 会话转移）表明用户希望打破终端与桌面端、移动端的会话边界，实现无缝接力。
- **新模型能力适配**：围绕 GPT-5.6 Sol 的 prompt 缓存问题（`#35300`、`#37674`）热度上升，用户需要 Codex 原生支持显式缓存断点与 Bedrock 缓存控制，以降低 agentic 工作负载成本。
- **MCP 连接状态可观测性**：4 个合并 PR 中有 3 个直接涉及 MCP 运行时治理（连接状态上报、严格审查结果保留、Guardian 元数据），说明 MCP 生态正从“能用”迈向“可管”。
- **Pets 与 Skills 个性化体验**：自定义 Pets 在 WSL 下失效（`#20730`）、Windows 宠物点击热区漂移（`#34227`）、系统 Skills 目录被误删（`#19265`），个性化功能在跨平台场景下仍不成熟。
- **会话恢复容错**：渲染器重载导致状态不同步（`#24263`）、恢复长线程时空白终端（`#34724`）、Windows 恢复时缺失 transcript（`#40151`），会话恢复健壮性已成为高频诉求。

## 开发者关注点

- **macOS 性能失控**：`#25719` 以 394 👍 成为绝对热点，Codex Desktop 触发 `syspolicyd`/`trustd` 的 CPU/内存异常仍未解决，这已是阻碍 macOS 用户日常使用的首要痛点。
- **认证与会话稳定性**：macOS（`#39162`）与 Windows（`#39189`）同时出现“打开旧会话即登出”，加上 `#39803`、`#39883` 等重复登录/401 问题，认证状态的保持与恢复是当前最集中的回归热点。
- **WebSearch 被 Cloudflare 拦截**：`#29197` 与 `#18456` 都指出客户端 HTTP 请求因 User-Agent 缺失/不合规被边缘节点 403，Windows 用户受影响明显。
- **崩溃类问题高频出现**：V8 OOM（`#38455`）、缺少工具调用结果导致整体崩溃（`#32653`）、进程启动失败（`#34928`）等多条 Issue 并存，反映桌面端稳定性依旧是短板。
- **长期线程恢复体验差**：多个 Issue 指向“长会话恢复”时的空白、卡顿或状态缺失，TUI/CLI 与桌面端均有涉及，提示会话持久化的工程难度被低估。

---
*本日报基于 GitHub 公开数据自动生成，供技术开发者快速了解社区动态。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报（2026-08-23）

## 今日速览

昨日发布 v0.56.0-nightly 版本，重点修复 macOS 沙箱中 Docker/容器运行时套接字与二进制的隔离漏洞。社区讨论集中于 Subagent 可靠性问题——`MAX_TURNS` 误报成功（#22323）与通用代理挂起（#21409）持续引发关注；此外，多核安全类 PR（变量展开绕过修复、excludeTools 文档纠正）进入活跃评审期。

## 版本发布

**v0.56.0-nightly.20260822.g5411f113c**（8月22日）
- 修复 macOS Seatbelt 沙箱：隔离 Docker 与容器运行时套接字、CLI 二进制及 Mach/XPC 服务，防止通过 VirtioFS 等容器 Hypervisor 文件系统挂载实现沙箱逃逸。贡献者：@josebalius（首次贡献）
- 发布链接：https://github.com/google-gemini/gemini-cli/releases

## 社区热点 Issues

1. **Subagent 在 MAX_TURNS 后误报 GOAL success**（#22323，13 评论）
   `codebase_investigator` 子代理在达到最大轮次后仍返回 `status: "success"`/`Termination Reason: "GOAL"`，实际未做任何分析。中断被隐藏为成功，极易误导上层决策。
   https://github.com/google-gemini/gemini-cli/issues/22323

2. **Generalist agent 无限挂起**（#21409，8 评论，8 👍）
   简单操作（如创建文件夹）在委托给通用代理后永久挂起，最长等待 1 小时无响应。用户通过明确禁止委托子代理可规避此问题。
   https://github.com/google-gemini/gemini-cli/issues/21409

3. **零依赖 OS 沙箱与执行后意图路由**（#19873，8 评论）
   增强提案：利用 Gemini 3 模型的 bash 原生能力（grep/cat/sed/awk 链式调用），在不牺牲安全性的前提下通过 OS 级沙箱和意图路由释放模型潜力。
   https://github.com/google-gemini/gemini-cli/issues/19873

4. **AST 感知文件读取/搜索/代码库映射评估**（#22745，7 评论）
   EPIC 追踪：探索 AST 感知工具在一次调用中精确读取方法边界、降低 token 噪声、减少 misaligned reads 带来的轮次消耗。
   https://github.com/google-gemini/gemini-cli/issues/22745

5. **Gemini 不会主动使用 skills 和 sub-agents**（#21968，6 评论）
   即使用户已配置 gradle/git 等 skills（含明确描述），模型在相关场景下仍不调用，必须显式指示才使用。
   https://github.com/google-gemini/gemini-cli/issues/21968

6. **Auto Memory 对低信号会话无限重试**（#26522，5 评论）
   当提取代理判断会话为低信号而不读取时，该会话永远留在待处理队列，会被反复呈现，造成资源和 token 浪费。
   https://github.com/google-gemini/gemini-cli/issues/26522

7. **Auto Memory 缺少确定性脱敏且日志过多**（#26525，4 评论）
   敏感内容在进入模型上下文后才由 prompt 指令脱敏，且服务会记录已存在的 skill 内容，存在隐私泄露风险。
   https://github.com/google-gemini/gemini-cli/issues/26525

8. **Shell 命令执行后卡在 "Waiting input"**（#25166，4 评论，3 👍）
   极简 CLI 命令完成后，界面仍显示命令活跃并等待输入，需频繁手动中断。属于高频复现的终端交互阻塞问题。
   https://github.com/google-gemini/gemini-cli/issues/25166

9. **Browser agent 会话接管与锁恢复**（#22232，4 评论）
   `BrowserManager.ts` 目前采用 fail-fast 策略，遇到持久化会话配置下的 profile 锁（含孤儿进程）即失败，缺少自动接管与锁恢复机制。
   https://github.com/google-gemini/gemini-cli/issues/22232

10. **Browser subagent 在 Wayland 下失败**（#21983，4 评论）
    浏览器子代理在 Wayland 环境中无法正常工作，终止原因显示为 GOAL 但实际未完成任务。
    https://github.com/google-gemini/gemini-cli/issues/21983

## 重要 PR 进展

1. **fix(sandbox): 隔离 macOS Seatbelt 中的 Docker/容器运行时**（#28935，已合入）
   PR #28935 的修复已进入 nightly 版本。详细拒绝 UNIX socket、CLI 二进制、Mach/XPC 服务查找与 POSIX 共享内存，防止沙箱逃逸。
   https://github.com/google-gemini/gemini-cli/pull/28935

2. **fix(core): 阻塞 $VAR/${VAR} 变量展开绕过（GHSA-wpqr-6v78-jr5g）**（#28902）
   修复 `detectBashSubstitution()`/`detectPowerShellSubstitution()` 中不完整的检查，并加强自动化去重工作流的安全防护。
   https://github.com/google-gemini/gemini-cli/pull/28902

3. **fix(cli): 防止静态刷新时清空终端滚动缓冲**（#28967）
   修复 `refreshStatic()` 在非 alternate buffer 模式下调用 `clearTerminal` 导致 Linux/Unix 终端模拟器滚动历史被清空的问题。
   https://github.com/google-gemini/gemini-cli/pull/28967

4. **docs(extensions): 纠正 excludeTools 示例永不匹配的问题**（#28966）
   文档中 `run_shell_command(rm -rf *)` 形式的示例实际上因精确名称匹配而从未生效，改为裸工具名，并指向策略引擎处理命令级阻止。
   https://github.com/google-gemini/gemini-cli/pull/28966
   （另有维护者提交的相同主题 PR #28963：https://github.com/google-gemini/gemini-cli/pull/28963）

5. **fix(core): write 策略配置中声明顶层安全检查器**（#28961）
   将 `write.toml` 中的安全检查器定义对齐为标准顶层 `[[safety_checker]]` 表数组，确保 `AllowedPathChecker` 在 `write_file`/`replace` 工具中正确注册。
   https://github.com/google-gemini/gemini-cli/pull/28961

6. **fix(cli): 保留执行中的 subagent 工具调用 UI 展示**（#27862）
   修复子代理工具调用在执行时从界面消失的问题，更新 `useToolScheduler` hook，保持活动状态持续可见。
   https://github.com/google-gemini/gemini-cli/pull/27862

7. **fix(core): 工具调用的结构化显示标题优先级**（#27863）
   `getDisplayTitle()` 现在优先使用 `_toolDisplayName`，其次是 `_toolName`，确保结构化展示标题不被错误覆盖。
   https://github.com/google-gemini/gemini-cli/pull/27863

8. **fix(extensions): 环境变更需同意并消毒运行时变量**（#28863）
   将 MCP 服务器环境配置纳入 consent 字符串生成，并过滤可能改变运行时行为的环境变量，防止扩展更新绕过用户同意注入恶意配置。
   https://github.com/google-gemini/gemini-cli/pull/28863

9. **fix(a2a-server): 新消息轮次时清除过期取消错误**（#28940）
   修复请求中止/取消后，后续用户 prompt 立即崩溃 `Execution aborted` 的状态损坏问题，解决 GCA 执行停止问题。
   https://github.com/google-gemini/gemini-cli/pull/28940

10. **fix(core): 避免将 401 子串误判为认证错误**（#28827）
    修复 `isAuthenticationError` 对包含 `401` 的无关值（如端口号、退出码）产生误报的问题，并增加回归覆盖。
    https://github.com/google-gemini/gemini-cli/pull/28827

## 功能需求趋势

- **Subagent 能力深化与可视化**：社区强烈要求子代理状态汇报准确（区分 GOAL 与 MAX_TURNS）、运行轨迹可通过 `/chat share` 分享，以及 AST 感知的文件读取策略来降低 token 消耗。
- **安全与沙箱强化**：从 macOS Seatbelt 隔离、变量展开绕过修复，到 Auto Memory 的确定性脱敏，安全类需求贯穿沙箱、策略引擎和记忆服务。
- **终端交互体验优化**：高频出现 shell 命令执行后悬挂、终端缩放闪烁、滚动缓冲被误清等终端渲染与状态管理问题。
- **记忆系统可靠性**：Auto Memory 的低信号会话无限重试、无效 patch 隔离、脱敏与日志控制成为记忆功能的主要改进方向。
- **浏览器自动化韧性**：Wayland 支持、持久化 profile 锁恢复、settings.json 覆盖生效是 browser agent 的核心诉求。

## 开发者关注点

- **状态汇报失真**：子代理将中断误报为成功（#22323）、bugreport 缺少子代理上下文（#21763），导致开发者对代理执行结果难以信任。
- **执行挂起高频**：generalist agent 无限挂起（#21409）与 shell 命令完成后卡在 "Waiting input"（#25166）严重阻塞日常工作流。
- **安全疑虑集中**：变量展开绕过（#28902）、Auto Memory 在脱敏前将原始内容送入模型上下文（#26525），引发对敏感数据暴露的担忧。
- **自定义代理/技能发现缺陷**：`~/.gemini/agents/` 下 symlink 文件不被识别（#20079），且模型不会主动使用已配置的 skills（#21968）。
- **扩展性限制**：启用超过 128 个工具时遭遇 400 错误（#24246），模型被限制在 shell 执行后会在随机目录散落临时脚本（#23571）。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-08-23）

## 今日速览

过去 24 小时 GitHub Copilot CLI 仓库无新版本发布、无 PR 更新，共有 11 个 Issue 产生更新。社区讨论热点集中在 **多 BYOK 模型切换**（#3282、#3709）、**MCP 初始化兼容性**（#4370）以及 **`--cloud` 远端任务稳定性**（#4568）。新提交的 Issue 中，Agent 只确认不执行工具、Windows 自动更新后进程残留 CPU 100% 等问题也值得关注。

## 版本发布

过去 24 小时无新版本发布。

## 社区热点 Issues

### 1. 允许 `/model` 在一个会话内切换多个模型，包括 BYOK/本地 Provider
**#3709** · `area:models` · 👍 27 · 💬 5  
当前 BYOK 模式会把会话锁定到 `COPILOT_MODEL` 指定的单一模型，而 `/model` 选择器只列出 GitHub 托管模型，看不到本地 BYOK Provider。开发者希望能在会话内随时切换到本地模型，这是目前模型生态最集中的诉求。  
🔗 https://github.com/github/copilot-cli/issues/3709

### 2. 支持在 Copilot CLI 中配置多个 BYOK 模型
**#3282** · `area:models`, `area:configuration` · 👍 26 · 💬 9  
该 Issue 提出在环境变量中配置多个 BYOK 模型，并能在 TUI 中直接切换，而不是每次都要终止会话、重新设置环境变量。它与 #3709 互相补充，共同指向“灵活、多模型、无需重启”的核心需求。  
🔗 https://github.com/github/copilot-cli/issues/3282

### 3. `--cloud` owner picker 挂起、重连崩溃、任务轮询 429
**#4568** · `triage` · 新 Issue  
无仓库上下文时，CLI 会一直卡在 `Loading available owners...`；有仓库上下文时，云任务停留在 `session.requested` 直到超时，且轮询接口出现 429。多个症状叠加，说明 `--cloud` 远端任务链路目前还不够稳定。  
🔗 https://github.com/github/copilot-cli/issues/4568

### 4. Agent 反复确认“已收到”却不执行任何工具动作
**#4566** · `triage` · 新 Issue  
在 1.0.80 版本 + `gpt-5.3-codex` 下，Agent 会一直输出确认信息，但不会实际调用工具。这类“假执行”问题会严重破坏自动化工作流，需要尽快定位是模型行为还是 CLI 工具调度问题。  
🔗 https://github.com/github/copilot-cli/issues/4566

### 5. MCP 初始化失败：FastMCP 返回 `-32602` 导致连接中断
**#4370** · `area:mcp` · 👍 1 · 💬 2  
CLI 在 MCP 初始化阶段会请求 `server/discover`，而 FastMCP 未实现该接口并返回 `-32602 Invalid request parameters`。Copilot CLI 把这个响应视为致命错误，导致无法连接 FastMCP 构建的 MCP Server。MCP 生态兼容性仍需加强。  
🔗 https://github.com/github/copilot-cli/issues/4370

### 6. 间歇性报错：需要启用 Enterprise/Organization Policy
**#2306** · `area:authentication`, `area:enterprise` · 👍 3 · 💬 7  
开发者每周会随机遇到 2-3 次 “You are not authorized to use this Copilot feature” 错误，随后又自行恢复。该问题影响企业用户信任度，需要排查服务端策略同步或鉴权缓存逻辑。  
🔗 https://github.com/github/copilot-cli/issues/2306

### 7. 无法在本地恢复远端会话
**#4514** · `area:sessions` · 👍 1 · 💬 1  
通过 `/resume` 选择远端会话后无法正常恢复，导致跨设备继续工作的场景受阻。远端/云会话的持久化和恢复能力还需要完善。  
🔗 https://github.com/github/copilot-cli/issues/4514

### 8. Windows 自动更新后，旧进程从 `copilot.exe.old` 继续运行并占满 CPU
**#4111** · `area:sessions`, `area:platform-windows`, `area:installation`  
长时间运行的交互式或 `--plan` 会话在 Windows 原地自动更新后，进程不会退出，而是从被重命名的 `copilot.exe.old` 继续执行，部分孤儿进程会有一个线程 100% 占用 CPU。对 Windows 重度用户影响明显。  
🔗 https://github.com/github/copilot-cli/issues/4111

### 9. 希望显式信任不安全的 HTTP OTLP Exporter 端点
**#4567** · `triage` · 新 Issue  
开发者希望像 VS Code / Copilot 默认 OTLP 端点一样，允许用户显式信任 `http://localhost:4318` 之类的本地 OTLP Collector，而不是静默禁用 telemetry export。这会方便本地可观测性调试。  
🔗 https://github.com/github/copilot-cli/issues/4567

### 10. 已触发的 pending prompt 仍残留在屏幕上
**#4564** · `triage`  
当 Agent 运行期间输入新 prompt，它会以 `(pending · ctrl+c to cancel)` 形式排队；但 prompt 被注入执行后，pending 状态没有正确清除，残留的 UI 提示会影响交互体验。  
🔗 https://github.com/github/copilot-cli/issues/4564

## 重要 PR 进展

过去 24 小时无 PR 新增或更新，暂无条目可列。建议关注上述 Issue 中 MCP 初始化、企业策略鉴权、`--cloud` 稳定性等问题的后续修复是否进入新版本。

## 功能需求趋势

- **多模型 / BYOK 切换**：社区最强烈的呼声。开发者不满足于通过环境变量固定单个模型，希望在 TUI 或 `/model` 中直接切换 GitHub 托管模型、BYOK 模型和本地 Provider 模型。
- **远端会话与 Cloud 任务稳定性**：多个 Issue 涉及远端会话恢复、云任务创建和轮询失败，说明 Copilot CLI 的云端工作流正在被更多用户使用，但稳定性仍需补齐。
- **MCP 生态兼容性**：MCP 已逐渐成为 Copilot CLI 的重要扩展方式，但当前初始化协议过于严格，对 FastMCP 等常见实现不够友好。
- **企业策略与鉴权可靠性**：企业用户间歇性遇到 policy 未启用错误，需要更透明的错误上下文和更稳定的鉴权状态。
- **可观测性与本地调试**：出现希望信任本地 OTLP HTTP 端点的需求，开发者希望在不关闭 telemetry 的情况下接入本地监控。

## 开发者关注点

- **BYOK 使用体验割裂**：切换模型必须先退出会话并修改环境变量，无法在会话内动态选择，影响长任务效率。
- **“幽灵进程”问题**：Windows 自动更新后残留 `copilot.exe.old` 进程并持续占用 CPU，升级机制需要处理运行中会话。
- **云任务失败链路不透明**：owner picker 挂起、任务卡在 `session.requested`、轮询 429，缺少清晰错误提示和自动恢复机制。
- **Agent 不执行工具**：新版本 1.0.80 下出现 Agent 只确认不调用工具的行为，对自动化使用场景是重大阻碍。
- **MCP Server 接入门槛高**：对未实现 `server/discover` 的 Server 直接判死，兼容性策略需要调整。
- **UI 细节仍需打磨**：pending prompt 残留显示虽小，但会干扰高频交互用户的操作判断。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>



</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-23

## 今日速览
今日无新版本发布，社区讨论集中在**沙箱/权限控制**与**会话稳定性**两大主题。`#2242`（Agent 沙箱）持续高热（83 评论 / 71 👍），`#7101`（自定义系统提示）以 127 👍 成为最受期待的功能请求。与此同时，多个严重 Bug 被报告：桌面版启动失败（`#40516`）、会话永久卡死（`#43277`）、托管网关流式中断（`#44044`）均影响用户日常使用。

## 社区热点 Issues
精选 10 个最受关注或风险最高的 Issue：

1. **[#2242] Is there a way to sandbox

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-23

## 今日速览

v0.22.0 正式发布，重点强化 Web Shell 稳定性（防 OOM 崩溃）与 Review 循环诊断能力。值得关注的是，Review 工作流在执行被评审仓库自身命令时正推进容器化隔离（#9723），安全边界讨论升温；同时社区反馈聚焦于会话恢复失败、循环检测误报等稳定性问题，以及 VS Code 集成体验优化。

## 版本发布

### v0.22.0（正式版）
- **Web Shell 防崩溃**：通过限制 transcript 保留量并裁剪超长 replay，避免因内存溢出导致崩溃（[#9303](https://github.com/QwenLM/qwen-code/pull/9303)）
- **Review 循环稳定性**：Review 循环现可引用具体文件及反复出现的 finding，向作者解释循环无法收敛的原因，提升诊断透明度
- 另有 nightly 版本 `v0.21.14-nightly.20260822.7a4566cb3b`，包含 review 功能改进与 CI 修复

> 注：v0.22.0 release notes 正文暂未填充，以上 Highlights 内容来自官方发布说明。

## 社区热点 Issues（10 个）

| Issue | 标题 | 热度 | 重要性 |
|-------|------|------|--------|
| [#8102](https://github.com/QwenLM/qwen-code/issues/8102) | proposal(core): deterministic tool-execution boundaries for a trustworthy agent runtime | 17 评论 | 提出将语言模型置于信任边界之外，确定性约束/审计模型行为。安全架构方向性讨论，社区关注度高 |
| [#9278](https://github.com/QwenLM/qwen-code/issues/9278) | Design: /review publish-time convergence advisory — telemetry, diagnosis, and operator-owned posting surfaces | 9 评论 | Review 循环失控问题（推送触发评审→修复→diff 变大→更多 finding），完整设计方案与实测记录，需求迫切 |
| [#9556](https://github.com/QwenLM/qwen-code/issues/9556) | review: decide whether the pipeline should keep granting code execution as the invoking user | 8 评论 | 安全关键问题：Review 以调用者身份执行代码的权限模型是否需要重构，直接推动了 PR #9723 的容器化方案 |
| [#9002](https://github.com/QwenLM/qwen-code/issues/9002) | SDK Python rejects permission_mode="auto" although the CLI supports it | 6 评论 | CLI 与 SDK 行为不一致，客户端校验阻塞合法配置，影响自动化用户 |
| [#9198](https://github.com/QwenLM/qwen-code/issues/9198) | qwen 跑出来oom 问题 | 5 评论 | 用户运行一周后 OOM，1T 内存服务器仍被耗尽，且 tmux 终端交互异常。严重稳定性 bug |
| [#9733](https://github.com/QwenLM/qwen-code/issues/9733) | bug(core): loop detection false-positives on verification cycles and kills unattended turns unrecoverably | 4 评论 | 循环检测误杀合法的"写脚本→运行→编辑→重跑"验证序列，且终端无法自动恢复，严重影响无人值守自动化 |
| [#9699](https://github.com/QwenLM/qwen-code/issues/9699) | ci: Dependency CVE audit fails on every PR as of 2026-08-21 | 4 评论 | 8 个依赖漏洞（1 high）导致所有 PR 的 CVE 审计失败，阻塞 CI 流程 |
| [#9706](https://github.com/QwenLM/qwen-code/issues/9706) | Auto session title can echo the TITLE_SYSTEM_PROMPT example verbatim | 4 评论 | 自动会话标题直接输出系统提示词示例文本，影响多会话管理体验 |
| [#9573](https://github.com/QwenLM/qwen-code/issues/9573) | bug(core): resumed sessions show 'Tool result missing from saved history' for tool calls that completed normally | 4 评论 | 会话恢复后 tool 调用的正常结果被替换为"缺失"占位符，阻断后续流程 |
| [#9695](https://github.com/QwenLM/qwen-code/issues/9695) | Deferred review findings from PR #9655 | 4 评论 | 自动评审循环积累的待处理 finding，维护者可转为独立 issue/PR，需人工关注 |

**其他值得关注**：[#9246](https://github.com/QwenLM/qwen-code/pull/9246)（Web Shell 侧边栏固定卡顿）、[#9333](https://github.com/QwenLM/qwen-code/issues/9333)（Node REPL MCP 交付形态变更）、[#9725](https://github.com/QwenLM/qwen-code/issues/9725)（VS Code transcript 需要真实运行时验收）。

## 重要 PR 进展（10 个）

| PR | 标题 | 核心内容 |
|----|------|----------|
| [#9719](https://github.com/QwenLM/qwen-code/pull/9719) | feat(vscode-ide-companion): adopt WebShell transcript as the default timeline | VS Code 插件采用 WebShell transcript 作为默认会话时间线，通过 ACP adapter 接入 SDK reducer，让聊天记录在 IDE 中获得一致的渲染体验 |
| [#9723](https://github.com/QwenLM/qwen-code/pull/9723) | feat(review): run the reviewed repository's own commands behind a container (#9556) | **重点安全改进**：将被评审仓库自身的命令执行放入容器边界，权限模型由"环境属性"变为"操作者策略"，是 #9556 的核心落地 |
| [#9744](https://github.com/QwenLM/qwen-code/pull/9744) | fix(review): count a fix-induced re-report as first-time work | 修复评审首次计数逻辑：携带前一轮 id 的修复引发评论应视为新工作，纠正收敛判断 |
| [#9627](https://github.com/QwenLM/qwen-code/pull/9627) | feat(review): back comment-status and presubmit for Aone Code targets | 为 Aone Code MR 补全评论状态检查与 presubmit 流程，此前两个流程被跳过 |
| [#9748](https://github.com/QwenLM/qwen-code/pull/9748) | fix(review): repair permissions before giving up on worktree cleanup | Review 清理 worktree 失败时先修复权限（恢复写位）再放弃，减少残留文件 |
| [#9582](https://github.com/QwenLM/qwen-code/pull/9582) | fix(telemetry): roll back replayed usage when a session swap fails | 会话切换失败时回放遥测数据回滚，避免用量计数失真 |
| [#9340](https://github.com/QwenLM/qwen-code/pull/9340) | feat(review): say when the approach, not the patch, is the open question | Review 多轮且 diff 大幅增长后，明确提示"问题在方案而非当前补丁"，抑制无意义迭代 |
| [#9602](https://github.com/QwenLM/qwen-code/pull/9602) | fix(core): clear tool display list before awaiting completion callback | 修复 tool 显示列表在回调完成后才清除的时序问题，附带回归测试 |
| [#9607](https://github.com/QwenLM/qwen-code/pull/9607) | fix(core): demote balanced inline thinking blocks instead of failing the turn | OpenAI 兼容端点上混合思考模型输出双阶段思考块时，降级处理而非直接终止回合 |
| [#9737](https://github.com/QwenLM/qwen-code/pull/9737) | refactor(cli): enforce utils leaf-layer dependency direction (#9146) | CLI `utils/` 目录机械性强制为叶子层，消除反向依赖（config/ui/i18n 等），提升可维护性 |

## 功能需求趋势

1. **Review 系统智能化与收敛控制**
   社区对 `/review` 的期望从"找问题"转向"能收敛"。多个 issue/PR 围绕：指出方案性问题（#9340）、解释循环不稳定原因（#9278）、修复计数逻辑（#9744）、发布时收敛建议（#9526）。核心诉求是让 Review 循环可诊断、可终止。

2. **安全边界与容器化**
   #8102（确定性工具执行边界）、#9556（评审代码执行权限）、#9723（容器化执行）共同指向一个方向：将模型行为约束在可审计的沙箱内，不让被评审代码以调用者身份直接运行。

3. **VS Code 集成深化**
   多个 issue 围绕 VS Code 插件体验：#8617（选择框遮挡内容）、#9725（transcript 需要真实 VS Code 运行时验收）、#9726（块标识稳定性）、#9727（artifact blob CSP）、#9743（拖拽文件支持）。WebShell transcript 正向 VS Code 迁移（#9719）。

4. **会话生命周期管理**
   会话恢复失败（#9573）、自动标题异常（#9706）、OOM 导致会话崩溃（#9198）、循环检测误杀（#9733）、会话固定卡顿（#9465）——会话的持久性、可恢复性和资源占用是热门方向。

5. **渠道集成扩展**
   DingTalk Workspace 渠道（#9394）、Aone Code 评审支持（#9627）、MindsHub 网关文档（#9746）表明社区正拓展多平台接入能力。

6. **AI 自动化辅助开发**
   Computer Use Skill（#9335）、会话级持久化 Node REPL（#9333，现改为 MCP server 形态交付）等探索方向，反映社区对"模型编写并调用工具完成复杂任务"的期待。

## 开发者关注点

- **稳定性是最大痛点**：OOM 崩溃（#9198）、会话恢复后 tool 结果丢失（#9573）、循环检测误杀无人值守任务（#9733）直接影响日常使用，反馈最为强烈。
- **评审循环需要"刹车机制"**：多位用户的 issue 指向 Review 陷入"修复→引入新缺陷→更多 finding"的失控回路，要求有明确的收敛退出策略。
- **CLI 与 SDK 行为一致性**：Python SDK 拒绝 CLI 支持的配置（#9002）等不一致问题，增加自动化集成的适配成本。
- **安全权限默认原则**：社区对"以用户身份执行代码"的默认行为开始质疑，期待更保守的默认配置和显式策略控制。
- **CI 可靠性**：依赖 CVE 审计全面失败（#9699）暴露供应链风险，社区希望安全扫描不因基础设施问题阻塞日常开发。
- **CI 基础设施的自动化维护**：#7167 Fleet Shepherd Dashboard 持续自动跟踪 PR 状态（idle 检测、自动调度），但需人工介入处理的 PR 仍积累较多，自动化与人工协作的边界值得关注。

---
*数据窗口：2026-08-22 ~ 2026-08-23 | 来源：[github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*