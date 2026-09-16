# AI CLI 工具社区动态日报 2026-09-16

> 生成时间: 2026-09-16 00:30 UTC | 覆盖工具: 7 个

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

> 说明：PR 评论数字段在数据中为 `undefined`，无法严格按评论数排序；以下按关联 Issue 热度、更新活跃度与影响面综合判断。截至 2026-09-16，所列 PR 均为 **OPEN**，未见 merged/draft。

## 1. 热门 Skills 排行

1. **skill-creator 触发评测修复**  
   - PR：[#1298](https://github.com/anthropics/skills/pull/1298)、[#1769](https://github.com/anthropics/skills/pull/1769)、[#539](https://github.com/anthropics/skills/pull/539)  
   - 功能：Skill 创建与触发评测，是 Skills 生态的“元技能”。  
   - 热点：触发评测误报/漏报、`precision=100% recall=0%`、Windows 子进程兼容、YAML 特殊字符导致 description 解析失败。  
   - 状态：OPEN，且与高热度 Issue #556、#1721 直接相关，优先级很高。

2. **mcp-builder 兼容性与评测修复**  
   - PR：[#1742](https://github.com/anthropics/skills/pull/1742)、[#1724](https://github.com/anthropics/skills/pull/1724)、[#1602](https://github.com/anthropics/skills/pull/1602)  
   - 功能：构建、连接和评测 MCP Server。  
   - 热点：`mcp>=2.0.0` 中 `streamablehttp_client` 重命名、自定义 headers、TextContent 序列化失败、默认模型过旧。  
   - 状态：OPEN，关联 #1668、#1390、#1602，属于生态基础设施型修复。

3. **claude-api 模型与上下文维护**  
   - PR：[#1607](https://github.com/anthropics/skills/pull/1607)  
   - 功能：Claude API 使用指南与模型列表维护。  
   - 热点：退休模型 ID 未标记；Issue #1487 指出该 Skill 曾一次注入约 156k tokens，严重挤压上下文窗口。  
   - 状态：OPEN，修复明确但影响面大。

4. **md2video-audio：Markdown 转视频**  
   - PR：[#1703](https://github.com/anthropics/skills/pull/1703)  
   - 功能：将 Markdown 经 Marp 转为演示文稿，再编译为带真人感配音的 MP4。  
   - 热点：零成本、文档到视频自动化、多模态内容生成。  
   - 状态：OPEN，更新于 2026-09-15，活跃度较高。

5. **document-typography：文档排版质量控制**  
   - PR：[#514](https://github.com/anthropics/skills/pull/514)  
   -

---

# Claude Code 社区动态日报
**日期：2026-09-16** · 数据源：github.com/anthropics/claude-code

---

## 一、今日速览

1. **v2.1.273 面向企业网关开放可观测性**：新增一组可选请求头（请求类别、Agent 类型、上一轮工具耗时、上下文压缩状态），网关侧可据此做路由与配额治理，通过 `CLAUDE_CODE_GATEWAY_HINT_HEADERS=1` 显式开启。
2. **Windows 平台稳定性问题集中爆发**：Desktop 重启死锁（189 条评论）、Cowork Plan9 挂载失败（117 条评论）、设备桥接失效等多条高热度 Issue 同日更新，Windows 已成为当前最大的稳定性短板。
3. **可扩展性与模型路由是社区两大诉求**：Mods/函数钩子路线图讨论（182 评论 / 113 赞）与 `fableplan` 别名请求（57 赞）构成本日最高声量。

---

## 二、版本发布

### v2.1.273（过去 24h）

- **新增 LLM 网关请求头**（需 `CLAUDE_CODE_GATEWAY_HINT_HEADERS=1` 显式开启）：
  - `x-claude-code-request-class` — 请求类别
  - `x-claude-code-agent-type` — Agent 类型
  - `x-claude-code-prev-tool-durations` — 上一轮工具调用耗时
  - `x-claude-code-compaction` / `x-claude-code-context-compacted` — 上下文压缩状态
- 新增一类通知能力（Release Notes 原文在此处被截断）。
- 意义：Claude Code 正把运行时遥测能力下沉到网关层，方便企业自建 LLM Gateway 做按 Agent/请求类的路由、限流与成本归因，与 #84532（Gateway 使用容器服务账号凭据）等企业需求方向一致。

### v2.1.272（过去 24h）

- 仅标注 "Bug fixes and reliability improvements"，无功能性变更。

---

## 三、社区热点 Issues（Top 10）

### 1. [#42776](https://github.com/anthropics/claude-code/issues/42776) — Desktop 在 Windows 上因孤儿进程文件锁无法重启 🔥
- **状态**：OPEN（标记 `invalid`）｜189 评论｜89 👍｜创建于 2026-04-02
- **为什么重要**：这是当前评论数最高的 Issue，且已持续 5 个多月未解决。文件锁导致应用无法重新启动，属于"卡死级"体验破坏。
- **社区反应**：89 个赞说明受影响面广；被标记为 `invalid` 却仍有 189 条讨论，反映标签判定与用户实际感受之间存在落差。

### 2. [#91870](https://github.com/anthropics/claude-code/issues/91870) — Mods：让 Claude 的可扩展性提升 10 倍
- **状态**：OPEN（`enhancement, area:hooks, area:plugins`）｜182 评论｜113 👍｜创建于 2026-09-03
- **为什么重要**：**全站点赞数最高的 Issue**。官方在讨论中给出 "Community Update: Sep 9, 2026"，承诺"function hooks 将在数周内而非数天内发布"，明确了一条产品路线图。
- **社区反应**：作者 @poteat 同时提交了相关 mod PR（见第四节），讨论已从"要不要做"进入"怎么做"的阶段。

### 3. [#92984](https://github.com/anthropics/claude-code/issues/92984) — Cowork（Windows）：Windows 更新 KB5124008 后所有 Plan9 共享挂载失败
- **状态**：OPEN（`bug, has repro, platform:windows, area:cowork`）｜117 评论｜58 👍
- **为什么重要**：有明确复现路径与临时解法——**卸载该 KB 即可恢复**，属于典型的平台侧回归问题，会直接影响 Cowork 在 Windows 上可不可用。
- **社区反应**：117 条评论显示大量用户在交叉验证 KB 版本与现象。

### 4. [#66903](https://github.com/anthropics/claude-code/issues/66903) — 新增 `fableplan` 别名（对标 `opusplan`）
- **状态**：OPEN（`enhancement, area:model`）｜5 评论｜**57 👍**
- **为什么重要**：评论不多但点赞极高，说明这是一个"共识型"需求——用户希望在新模型上复用 `opusplan` 的规划/执行分层工作流。反映社区对新模型接入与别名体系的持续关注。

### 5. [#93683](https://github.com/anthropics/claude-code/issues/93683) — 每条工具结果中被注入的指令会覆盖用户显式指令，且无法关闭
- **状态**：OPEN（`bug, has repro, platform:macos, area:core`）
- **为什么重要**：这是一个**信任与可控性**问题。用户在工具结果中发现系统附加的 `type=attachment` 指令，且没有任何 opt-out 开关，导致模型行为偏离用户意图。
- **社区反应**：虽评论数仅 5，但问题性质敏感，属于"高信号"反馈。

### 6. [#94620](https://github.com/anthropics/claude-code/issues/94620) — 请求内置的跨平台"列出运行中的 Claude Code 会话及状态"能力
- **状态**：OPEN（`enhancement, platform:linux, area:hooks, area:cli`）｜创建于 2026-09-16
- **为什么重要**：当天新开的需求。外部进程目前无法获知"哪些会话在跑、是空闲还是等我确认"，这对多会话编排、IDE 集成、自动化调度都是基础能力缺失。

### 7. [#92710](https://github.com/anthropics/claude-code/issues/92710) — Cowork（macOS）：新项目自 9/6 起只能绑定单个文件夹，多文件夹工作流被静默破坏
- **状态**：OPEN（`duplicate, platform:macos, area:cowork, area:desktop`）｜4 评论｜5 👍
- **为什么重要**：典型"静默回归 + 文档不同步"问题——行为已变更（"Use a folder" 单文件夹、Context 仅接受

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-09-16）

## 一、今日速览

- **0.155.0 进入高频 alpha 迭代**：过去 24 小时内连续发布 `rust-v0.155.0-alpha.5` 至 `alpha.8` 共 4 个版本，但 Release Note 均为空，推测为内部快速修复与 CI 验证。
- **TUI 可定制化与 Windows 平台问题主导社区讨论**：状态栏定制需求（#17827）以 182 👍 居首；Windows 插件不可用、沙箱失败等问题在 Issue 榜中占据多个席位。
- **内部自动化工作流集中落地修复**：一批由 `copyberry[bot]` 提交的 PR 在 24 小时内关闭，覆盖 WSL 启动检测、Windows 沙箱策略、Analytics 面板与 MCP UI 元数据等方向。

---

## 二、版本发布

过去 24 小时共发布 4 个 Rust 版本，均为 0.155.0 的 alpha 补丁：

| 版本 | 说明 |
|---|---|
| [rust-v0.155.0-alpha.8](https://github.com/openai/codex/releases) | Release 0.155.0-alpha.8 |
| [rust-v0.155.0-alpha.7](https://github.com/openai/codex/releases) | Release 0.155.0-alpha.7 |
| [rust-v0.155.0-alpha.6](https://github.com/openai/codex/releases) | Release 0.155.0-alpha.6 |
| [rust-v0.155.0-alpha.5](https://github.com/openai/codex/releases) | Release 0.155.0-alpha.5 |

**观察**：4 个版本均未附带变更日志，说明 0.155.0 仍处于不稳定的密集迭代阶段，不建议生产环境跟随 alpha 通道。

---

## 三、社区热点 Issues（10 个）

1. **[#17827] Customizable status line（TUI 可定制状态栏）** — 46 评论 / 182 👍
   社区呼声最高的功能需求。用户希望像 Claude Code 那样，通过 shell 脚本在 TUI 底部展示 token 用量、模型名、限流状态、上下文窗口、git 分支等信息。
   https://github.com/openai/codex/issues/17827

2. **[#25220] Windows 捆绑插件全部不可用（EFS 加密导致 copyfile 失败）** — 38 评论
   Microsoft Store 版 Codex 的 Computer Use、Browser、Chrome、LaTeX 插件在 EFS 加密的 WindowsApps 目录下无法复制文件，属于 Windows 分发的系统级阻塞问题。
   https://github.com/openai/codex/issues/25220

3. **[#13852] Supabase MCP 反复要求重新认证** — 20 评论
   `initialize` 阶段 OAuth token 刷新失败，导致 MCP 集成在生产工作流中不可用。反映出 MCP 认证生命周期管理仍是薄弱环节。
   https://github.com/openai/codex/issues/13852

4. **[#34268] 多智能体 V2 全历史 fork 导致会话存储突破 100 GiB** — 16 评论 / 已关闭
   长会话使用 Ultra reasoning 与多智能体 V2 时，压缩快照和内联图片被重复复制，存储呈乘数级增长。该问题已关闭，但暴露出会话存储缺乏上限与清理机制。
   https://github.com/openai/codex/issues/34268

5. **[#43237] GPT-6 Astra 对 `hi` 返回 invalid_prompt** — 16 评论
   在 Linux/macOS 上以最小后端复现，CLI 与最小后端均拒绝最基础输入。作为新模型的行为异常，开发者关注度较高。
   https://github.com/openai/codex/issues/43237

6. **[#17642] ChatGPT 账号无法使用 gpt-5.3-codex-spark** — 15 评论
   返回 400 错误：“该模型在 Codex 配合 ChatGPT 账号使用时不受支持”。账号类型与模型权限的映射不透明，导致 Pro 用户也无法调用。
   https://github.com/openai/codex/issues/17642

7. **[#26338] Codex App 支持包含多个 Git 仓库的父工作区** — 14 评论 / 36 👍
   用户希望在一个父目录下管理多个独立仓库，而不是为每个

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报
**日期：2026-09-16** ｜ 数据来源：github.com/google-gemini/gemini-cli

---

## 1. 今日速览

今日社区焦点集中在 **Agent/Subagent 的可靠性**：多条 P1 级 Issue（通用 Agent 挂起、MAX_TURNS 被误报为成功、Shell 执行卡在 "Waiting input"）同日被更新，且大多带有 `workstream-rollup` 与 `maintainer only` 标签，说明官方正在集中收口。同时 v0.60.0 正式版发布，带来 Web Fetch 目标校验与 MCP OAuth（RFC 9207）安全修复，OAuth refresh token 丢失问题也有对应 PR 提交。

---

## 2. 版本发布

| 版本 | 类型 | 要点 |
|---|---|---|
| **v0.60.0** | 正式版 | `fix(core)`: 改进 web fetch 工具的目标地址校验与连接路由；`fix(core)`: 在 MCP OAuth 流程中强制 RFC 9207 issuer 识别 |
| **v0.61.0-preview.0** | 预览版 | 包含 v0.60.0-preview.0 / v0.59 的 Changelog 汇总，版本号从 nightly 20260908 递增 |
| **v0.61.0-nightly.20260915.g9c1b0a610** | Nightly | 常规每日构建，无额外说明 |

> 观察：v0.60.0 的两项修复都指向**安全边界**（URL 校验、OAuth issuer 识别），与今日多个安全类 Issue 形成呼应。

---

## 3. 社区热点 Issues（10 条）

1. **[#22323] Subagent 达到 MAX_TURNS 后仍上报 GOAL success**（P1 / bug / 13 评论 / 👍2）
   子 Agent 在未做任何分析、仅因触达最大轮次而中断时，仍返回 `status: "success"` 与 `Termination Reason: "GOAL"`，掩盖了真实中断。这是**可观测性失真**的典型问题，会直接误导上层编排与用户判断，是今日评论数最高的 Issue。
   https://github.com/google-gemini/gemini-cli/issues/22323

2. **[#21409] Generalist Agent 无限挂起**（P1 / bug / 8 评论 / 👍8）
   一旦 CLI 委派给通用 Agent，即使是"创建文件夹"这类简单操作也会永久卡死（用户等待一小时）。禁止使用 sub agent 可规避，说明委派链路存在阻塞。👍 数最高，社区共鸣强烈。
   https://github.com/google-gemini/gemini-cli/issues/21409

3. **[#19873] 通过零依赖 OS 沙箱释放模型的 bash 亲和性**（P2 / enhancement / 9 评论）
   提案认为 Gemini 3 模型原生擅长链式调用 `grep`/`cat`/`sed`/`awk`，希望在**不牺牲安全与 UX** 的前提下让模型走原生 bash 路径，并配合"执行后意图路由"。这是架构级方向性讨论。
   https://github.com/google-gemini/gemini-cli/issues/19873

4. **[#25166] Shell 命令执行完成后仍卡在 "Waiting input"**（P1 / core / 4 评论 / 👍3）
   简单 CLI 命令已结束，但 UI 仍显示 Shell 活跃并"等待用户输入"。属于**会话状态机与 PTY 生命周期**问题，与今日 PR #29340 的 PTY 清理改动高度相关。
   https://github.com/google-gemini/gemini-cli/issues/25166

5. **[#22745] 评估 AST-aware 文件读取、搜索与代码库映射**（P2 / EPIC / 7 评论）
   探索用 AST 感知工具精确读取方法边界、减少错位读取与 token 噪声。这是**上下文效率**方向的长期 EPIC，配套还有 #22746（用 AST 感知 CLI 工具映射代码库）。
   https://github.com/google-gemini/gemini-cli/issues/22745

6. **[#21968] Gemini 很少主动使用 skills 与 sub-agents**（P2 / bug / 6 评论）
   用户反馈：除非显式指令，模型几乎不会自主调用自定义 skill（如 gradle、git）。这削弱了扩展机制的实用价值，属于**工具调度策略**问题。
   https://github.com/google-gemini/gemini-cli/issues/21968

7. **[#26525] Auto Memory 需要确定性脱敏并降低日志量**（P2 / security / 5 评论）
   Auto Memory 会读取本地 transcript 并发送给后台抽取 Agent，脱敏发生在内容**已进入模型上下文之后**，且服务可能记录既有 skill 信息。属于隐私与数据流安全的关键缺陷。
   https://github.com/google-gemini/gemini-cli/issues/26525

8. **[#21983] browser subagent 在 Wayland 下失败**（P1 / agent/browser / 4 评论）
   浏览器子 Agent 在 Wayland 环境直接失败。Linux 桌面兼容性是实际使用率的硬门槛，与 #22232（浏览器 profile 锁恢复）构成同一主题簇。
   https://github.com/google-gemini/gemini-cli/issues/21983

9. **[#24246] 工具数超过 128 个时触发 400 错误**（P2 / bug / 3 评论）
   工具规模膨胀导致请求被拒。随着 MCP server 与 skill 生态扩张，**工具注册与作用域裁剪**将成为架构瓶颈。
   https://github.com/google-gemini/gemini-cli/issues/24246

10. **[#21335] `/compress` 结果不跨会话持久化**（P2 / bug / 👍2）
    压缩后的摘要只更新内存历史，未写回 session 文件，退出再恢复即失效。直接影响长会话的 token 成本控制。
    https://github.com/google-gemini/gemini-cli/issues/21335

> 补充值得留意：
> - **[#22672] Agent 应停止/劝阻破坏性行为**（`git reset --force` 等）— 安全护栏类需求 https://github.com/google-gemini/gemini-cli/issues/22672
> - **[#26522] / [#26523] Auto Memory 低信号会话无限重试、无效 patch 静默跳过** — 记忆系统质量系列 https://github.com/google-gemini/gemini-cli/issues/26522
> - **[#21763] `/bug` 报告不包含 subagent 上下文** — 与 #22323 同属可观测性缺口 https://github.com/google-gemini/gemini-cli/issues/21763

---

## 4. 重要 PR 进展（10 条）

1. **[#29339] 修复 OAuth refresh token 在刷新时丢失**（P1 / core / OPEN）
   解决 GH-21691：刷新凭据时 `refresh_token` 被覆盖，导致用户陷入重复认证错误循环；同时让凭据删除具备幂等性。**今日最高优先级修复之一**。
   https://github.com/google-gemini/gemini-cli/pull/29339

2. **[#29347] 修复 UI 负布局尺寸导致的渲染崩溃**（P1 / ui / maintainer only）
   为 `renderBorder` 与字符串重复逻辑加防御，避免 `RangeError: Invalid count value: -1`，并在多个 UI 组件中统一做 `Math.max(0, ...)` 夹取。
   https://github.com/google-gemini/gemini-cli/pull/29347

3. **[#29343] 抑制请求取消时未捕获的 AbortError 日志**（size/m / OPEN）
   修复 Node 23+ 下用户取消查询/流时 `AbortError` 从 EventTarget 监听器冒泡导致的硬崩溃。
   https://github.com/google-gemini/gemini-cli/pull/29343

4. **[#29340] 改进 PTY 文件描述符清理与执行生命周期管理**（core / OPEN）
   在 POSIX 平台确保 PTY slave 描述符与后台 shell 执行结束后完整释放资源——与 #25166 的"卡住"现象可能同源。
   https://github.com/google-gemini/gemini-cli/pull/29340

5. **[#29341] 将 MCP 工具调用标题格式化为结构化签名**（P1 / core,acp / CLOSED）
   统一 ACP 载荷与核心工具接口中 MCP/发现型工具的展示格式，把"说明文本"与"结构化签名"分离，改善非交互式场景可读性。
   https://github.com/google-gemini/gemini-cli/pull/29341

6. **[#29335] 保证 AgentLoopContext 属性在对象展开时不丢失**（P1 / core）
   `Config` 类原本用原型 getter 实现 `AgentLoopContext`，在 spread 后属性丢失；改为可保留的形式，避免 Agent 循环上下文残缺。
   https://github.com/google-gemini/gemini-cli/pull/29335

7. **[#29333] 校验"约定发现"的策略目录权限**（P2 / enterprise / OPEN）
   此前只校验系统策略目录；用户级与工作区级策略目录由约定发现，其权限是唯一凭证，现一并纳入 `isDirectorySecure` 检查。企业安全重要补丁。
   https://github.com/google-gemini/gemini-cli/pull/29333

8. **[#29342] 避免输入历史状态嵌套更新**（P2 / core / OPEN）
   重构 `useInputHistoryStore`，消除 React StrictMode 下的嵌套 setState 双调用问题，保留原有顺序与去重行为。Closes #29313。
   https://github.com/google-gemini/gemini-cli/pull/29342

9. **[#29304] 截断时不再切断 UTF-16 代理对**（cli / OPEN）
   `sanitizeForDisplay` 在表情符号中间截断会产生孤立代理项导致渲染丢字符，现修复分割边界。细节体验类修复。
   https://github.com/google-gemini/gemini-cli/pull/29304

10. **[#29242] 修复 `isAuthenticationError` 把 401 当子串匹配**（P2 / core / OPEN）
    `message.includes('401')` 会误命中端口号 4012、ID、行号等，触发错误的重新认证/登出流程。改为更精确判定。
    https://github.com/google-gemini/gemini-cli/pull/29242

> 其他：**[#29137]** 由 Dependabot 提交的 npm 依赖组更新（77 项，含 `simple-git` 3.28→3.36、`@modelcontextprotocol/sdk`），是一个体量较大的依赖维护 PR。https://github.com/google-gemini/gemini-cli/pull/29137

---

## 5. 功能需求趋势

从近 24 小时更新的 50 条 Issue 中，可提炼出以下方向：

- **Subagent 体系成熟化（最热）**：可观测性（轨迹共享 `/chat share`、bug 报告含子 Agent 上下文）、终止原因语义正确性、配置覆盖（`settings.json` 的 `maxTurns` 被忽略）、浏览器子 Agent 的容错与平台兼容。
- **安全与沙箱边界**：零依赖 OS 沙箱释放 bash 亲和性、策略目录权限校验、Auto Memory 确定性脱敏、破坏性命令（`git reset --force`）防护。
- **上下文与记忆效率**：AST-aware 读取/搜索/代码库映射、Tactful Extraction 外科式读取、Auto Memory 质量与重试策略、`/compress` 持久化、用持久化文件任务追踪替代 `WriteToDo`（#18836）。
- **工具生态与规模管理**：工具数 >128 报 400、MCP 工具签名标准化、工具作用域智能裁剪。
- **终端与跨平台体验**：Wayland 支持、终端 resize 高性能无闪烁渲染（#21924）、输入历史状态、UTF-16 截断、临时脚本乱落盘（#23571）。
- **认证与凭据健壮性**：OAuth refresh token 保留、401 误判、凭据删除幂等。

---

## 6. 开发者关注点（痛点总结）

1. **Agent 会"卡死"也会"假装成功"** —— #21409（永久挂起）、#22323（MAX_TURNS 误报 GOAL success）、#25166（命令结束仍等待输入）、#22186（输出 hook 崩溃）共同指向**执行状态机的可信度**问题。开发者既拿不到正确结果，也无法从状态中判断发生了什么。

2. **交互式命令与子进程管理是企业级阻塞点** —— `vite create` 卡在交互提示（#22465）、Shell "Waiting input" 假死、PTY 资源未释放，直接影响日常开发流程可用性。

3. **配置不生效削弱可预期性** —— Browser Agent 忽略 `settings.json` 覆盖（#22267）、`~/.gemini/agents/` 下的符号链接不被识别（#20079），让用户的定制化投入落空。

4. **模型不主动使用扩展能力** ——

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 · 2026-09-16

## 1. 今日速览

今天 Copilot CLI 连发 **v1.0.84-8 / v1.0.84-9** 两个补丁版本，重点在上下文管理开关、转录视图精简化和 Agent Factory 运行控制，同时优化了大历史会话的元数据扫描性能。社区侧最突出的信号仍是**内存/会话稳定性问题**：多个 OOM、compaction 死循环、会话锁残留 Issue 在过去 24 小时内持续活跃，涉及 Linux、macOS 与长会话恢复场景。此外，长达近一年的 #13（vim 输入模式）与 #54（VS Code Copilot Chat 能力整合）两个高赞需求在同日关闭，成为今日社区焦点。

---

## 2. 版本发布

### v1.0.84-9
- **新增**：在 `/settings` 中提供开关，可选择为 agent 和 subagent 启用上下文管理工具（context management tools）。
- **改进**：大幅缩短大型本地会话历史的元数据扫描时间，代价是线程与内存占用上升。
- **修复**：`End` 与 `Ctrl+E` 现在会把光标移动到软换行行的真实末尾，修复了输入截断/定位错误的问题。

### v1.0.84-8
- **新增**：`transcriptView` 支持 `"concise"` 模式，把工具调用活动聚合为可展开的“工作摘要”，显著降低长会话的视觉噪音。
- **改进**：可在 `/factories` 对话框中暂停（pause）与恢复（resume）Agent Factory 运行。
- **修复**：登录、切换账号、登出后，模型列表现在会正确刷新。

> 观察：两个版本一条主线是“降低长会话的信息与性能负担”（concise transcript、上下文管理开关、元数据扫描优化），另一条是“让用户对环境有更多显式控制权”（settings 开关、Factory 暂停）。这与社区中大量关于长会话 OOM 的反馈方向一致，但目前尚未触及 OOM 根因。

---

## 3. 社区热点 Issues（按重要性精选 10 条）

### 1）[#13](https://github.com/github/copilot-cli/issues/13) — CLI 输入应支持 vi/vim 模式（CLOSED）
- 作者 @RyanHecht｜13 评论｜**76 👍（今日最高赞）**
- 为习惯模态编辑器的用户提供键盘驱动的交互输入。历经近一年讨论后关闭，是社区呼声最高的交互体验需求，也暗示 CLI 输入层将向可插拔/可配置编辑模式演进。

### 2）[#54](https://github.com/github/copilot-cli/issues/54) — Copilot CLI 应完整复用 VS Code Copilot Chat 的能力与配置（CLOSED）
- 作者 @bartlettroscoe｜13 评论｜20 👍
- 主张 CLI 应作为已配置好的 VS Code Copilot Chat 的 CLI/批处理前端，而非另一套独立设置。该议题关闭对“IDE 与 CLI 配置一体化”方向具有标志性意义，直接影响企业用户的配置治理成本。

### 3）[#4664](https://github.com/github/copilot-cli/issues/4664) — 恢复长会话时 JS heap OOM 崩溃（OPEN）
- @shrijitnair｜8 评论｜2 👍｜标签：area:sessions, area:context-memory
- 恢复大型历史会话时，Node 进程在加载阶段即触及约 4GB 堆上限并崩溃，**用户无法进入会话**。这是今日评论数最多的未关闭 Issue，与新版“元数据扫描优化”直接相关，但显然未能覆盖该场景。

### 4）[#1148](https://github.com/github/copilot-cli/issues/1148) — Windows 下所有被编辑文件被强制改为 CRLF（OPEN）
- @BillyONeal｜7 评论｜8 👍｜标签：area:platform-windows, area:tools
- 原本 LF 的文件被 Copilot 编辑后变成 CRLF，会污染 diff、破坏跨平台仓库。属于“静默破坏用户代码库”的高危问题，长期存在且影响面广（vcpkg 维护者报告）。

### 5）[#4438](https://github.com/github/copilot-cli/issues/4438) — `disable-model-invocation: true` 导致技能完全不可达（OPEN）
- @grammy-jiang｜6 评论｜7 👍｜标签：area:agents
- 该字段本意是“禁止模型自动调用、仅允许手动调用”，实际却让技能在 CLI 中彻底不可用（`Skill not found`）。属于语义实现错误，直接影响 skill/agent 生态的可控性设计。

### 6）[#4725](https://github.com/github/copilot-cli/issues/4725) — Linux 上频繁 JavaScript heap out of memory（OPEN）
- @jbulow｜6 评论｜1 👍｜标签：area:platform-linux
- 每隔几分钟即因 Mark-Compact / allocation failure 崩溃，日志显示堆稳定在约 3.9GB。这是**平台维度的稳定性问题**，说明 OOM 不是单一会话过大导致，而可能存在泄漏或回收策略缺陷。

### 7）[#4849](https://github.com/github/copilot-cli/issues/4849) — 降低 subagent 工作流的延迟与评审循环开销（OPEN）
- @tjgreen42｜5 评论｜标签：triage
- 指出 agent 启动、任务交接与“评审→修复→再评审”往返常常每轮耗时数分钟。直接命中多 agent 编排的实用性瓶颈，是当前 agent 化落地的核心效率痛点。

### 8）[#4699](https://github.com/github/copilot-cli/issues/4699) — 长 `--resume` 会话 OOM，且崩溃转储被写入用户 cwd（OPEN）
- @pedoch｜4 评论｜5 👍｜标签：area:sessions, area:context-memory
- 14 小时内崩溃 3 次，且 Node 诊断报告直接落在当前工作目录，污染用户项目。**稳定性问题叠加“污染工作区”的次生伤害**，是 OOM 类问题中最易被诟病的一条。

### 9）[#2734](https://github.com/github/copilot-cli/issues/2734) — 插件自动更新（全部或按插件）（OPEN）
- @msosav｜3 评论｜**13 👍**
- 目前插件市场更新需用户手动检查与安装，导致用户长期停留在含缺陷版本。高赞表明插件生态成熟后，**分发与版本管理**已成为刚需。

### 10）[#3954](https://github.com/github/copilot-cli/issues/3954) — `explore` 工具硬编码 `gpt-5.4-mini`，忽略自定义/DeepSeek 配置（OPEN）
- @Aferrara3｜4 评论｜3 👍｜标签：area:agents, area:models
- 用户配置的自定义模型端点被内置工具绕过，导致请求失败或行为不一致。关系到**自定义模型/多模型供应商支持**的可信度，是 agent 与模型配置解耦的关键缺口。

> 其他值得留意的今日新增/更新：[#4807](https://github.com/github/copilot-cli/issues/4807) 空闲进程 FileWatch 事件风暴、221% CPU、33GB 日志；[#4780](https://github.com/github/copilot-cli/issues/4780) compaction 触发后进入不可恢复崩溃循环；[#4805](https://github.com/github/copilot-cli/issues/4805) 崩溃残留 `inuse.<pid>.lock` 导致会话无法重开。

---

## 4. 重要 PR 进展

过去 24 小时内 **没有更新的 Pull Request（共 0 条）**，本期无 PR 内容可汇总。

从 Issue 的时间戳分布看，社区反馈量（43 条更新）与合并节奏之间存在明显落差，尤其是 OOM 与沙箱策略类问题已连续多日活跃但缺少可追踪的修复 PR，建议后续关注维护者是否会在 1.0.85 前后批量回应。

---

## 5. 功能需求趋势

从本次全部 Issues 中可提炼出五个主要方向：

1. **会话生命周期与内存治理（最热）**
   OOM、heap 上限、compaction 死循环、会话锁残留、事件存储耗尽重试风暴——相关 Issue 占比最高（#4664、#4725、#4699、#4639、#4780、#4506、#4251、#4807、#4805）。这是当前**唯一可能阻断用户日常使用**的问题族。

2. **Agent / Subagent 编排的可用性与效率**
   需求集中在降低 subagent 往返延迟（#4849）、修复后台 subagent 卡死（#4850）、技能调用语义正确性（#4438）、工具与模型配置解耦（#3954）。社区已从“能不能跑 agent”转向“跑得稳不稳、快不快”。

3. **配置与策略的统一治理**
   `extraKnownMarketplaces` 未注册（#4556）、托管设置自动刷新破坏 IDE MCP 重载与 `/allow-all`（#4847）、企业级 CLI 沙箱/ yolo 策略（#4783）、沙箱策略被部分命令绕过（#4846、#4854）。企业用户在推动**策略真正生效**而非仅被展示。

4. **IDE 与外部生态集成**
   #54 关闭标志着 CLI↔VS Code 一体化诉求进入执行阶段；MCP 侧则出现 CIMD OAuth 回调端口不匹配（#4800、#4793）与 MCP 不可用时误报“waiting on ide”并挂起（#4552）等问题。

5. **终端交互与可访问性细节**
   vim 模式（#13）、Warp 主题色不跟随终端（#4843）、macOS Terminal 无键盘输入（#4855）、Ctrl-D 在表单中误触发退出（#4866）、SIGINT 后模型仍在运行并上报成功（#4863）、表单向/聊天式澄清问题（#4865）。终端体验正成为差异化竞争点。

---

## 6. 开发者关注点

- **稳定性优先级高于新功能**：OOM 相关 Issue 在评论数、跨平台覆盖（Linux/macOS/Windows）上全面领先，且多数以“崩溃导致无法恢复会话”收尾。开发者希望看到的是**根因修复与内存上限可配置**，而非仅做扫描提速。
- **“静默破坏”最不可接受**：CRLF 改写（#1148）、崩溃转储写入 cwd（#4699）、33GB 日志刷盘（#4807），这类问题会污染用户的代码库与磁盘，信任成本远高于功能缺失。
- **配置必须被尊重**：自定义模型被硬编码覆盖（#3954）、沙箱策略显示已允许但实际拦截（#4854）、服务端下发的 marketplace 未注册（#4556），开发者反复强调“设置面板里写了就要生效”。
- **多 Agent 工作流的实际效率**：subagent 启动慢、评审循环冗长、后台任务卡在 running 状态不返回结果，这些直接决定 agent 化工作流能否进入日常生产使用。
- **平台一致性与终端适配**：Windows 行尾、Linux 内存、Warp/macOS Terminal 的输入与配色差异，说明跨平台质量仍是短板。
- **生态运维能力缺口**：插件自动更新（#2734，13 👍）反映出插件体系已进入“需要版本治理”的阶段，缺少更新通道会成为生态扩张的阻力。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报
**日期：2026-09-16** ｜ 数据源：github.com/MoonshotAI/kimi-cli

> **数据说明**：过去 24 小时内该仓库**无新版本发布、无 PR 更新**，仅 4 条 Issue 有活动（2 OPEN / 2 CLOSED）。因此本期"热点 Issue"按实际数据全部列出，不做凑数；PR 部分无内容可报。样本量小，趋势判断仅供参考。

---

## 1. 今日速览

今日社区活动集中在**计费透明度**与**跨平台体验**两条线索上：一条付费用户提交的缓存计费异常（cache_read 重复计费、cache_creation 恒为 0，导致配额消耗放大约 10 倍）持续发酵，是当前风险等级最高的 OPEN Issue；同时两条积压近半年的老 Issue（macOS Cmd+V 粘贴图片、PicoClaw 第三方 Agent 接入）在今日被集中关闭，显示维护者正在清理历史积压。此外，新增一条关于 Kimi Work 会话标题日期前缀的功能建议，暴露出 Kimi Work/Desktop 缺少独立公开 issue tracker 的治理问题。

---

## 2. 版本发布

过去 24 小时无新 Release。

---

## 3. 社区热点 Issues

### 🔴 高优先级

**#2626 [OPEN] 配额异常消耗：cache_read 每轮计费且 cache_creation 恒为 0（放大 >10 倍）**
- 作者：@ahmadyaseen35-coder ｜ 创建：2026-08-29 ｜ 更新：2026-09-15 ｜ 评论：2 ｜ 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2626
- **为什么重要**：这是一条来自**年付订阅付费用户**的计费异常报告。用户反馈 2026-08-28 晚间在轻度使用的情况下，5 小时配额窗口在几分钟内掉掉约 40%；并附上 CLI 侧的日志证据表明 `cache_read` 在**每一轮对话**都被计费，而 `cache_creation` 始终为 0。如果属实，这意味着 prompt cache 的计费口径存在系统性偏差，会造成远超实际用量的配额扣减（作者估计 >10 倍放大）。
- **社区反应**：目前 2 条评论、0 点赞，讨论声量不大，但**影响面与严重度远高于热度本身**——它直接关系到付费用户的成本与服务可信度。已开放 18 天仍未关闭，建议维护方尽快给出计费口径说明或复现结论。

**#2646 [OPEN] 功能建议：Kimi Work 会话标题自动加创建日期前缀（YYYYMMDD）**
- 作者：@GH-Mason ｜ 创建：2026-09-15 ｜ 更新：2026-09-15 ｜ 评论：0 ｜ 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2646
- **为什么重要**：需求本身不复杂（会话标题前缀日期，便于按时间线检索），但**这条 Issue 的真正价值在于"Routing note"**：作者明确表示找不到 Kimi Work / Kimi Desktop 的公开 issue tracker，只能参照 #2143 的先例提交到 kimi-cli 仓库，并请求转交给桌面端团队。这是一个仓库治理与用户反馈通路问题，会持续制造噪声 Issue。
- **社区反应**：新提交，暂无评论。建议维护者在 README/模板中明确各产品线的反馈入口。

### 🟢 已关闭 / 已解决

**#1433 [CLOSED] [bug] 剪贴板图片处理只考虑 Ctrl+V，忽略 macOS 的 Cmd+V**
- 作者：@ringotypowriter ｜ 创建：2026-03-13 ｜ 更新：2026-09-15 ｜ 评论：2 ｜ 👍：1
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1433
- **为什么重要**：典型的**平台差异型 bug**。环境为 Darwin 25.3.0 arm64，CLI 版本 1.22.0，模型 kimi-for-coding，订阅 Kimi Coding Plan。在 macOS 上 CLI 内粘贴图片只绑定 Ctrl+V，未处理 Cmd+V，导致 Mac 用户粘贴图片功能实际不可用。
- **社区反应**：积压约 6 个月后今日关闭，是今日唯一获得点赞（👍1）的 Issue。与 #1435 同日关闭，可视为维护者在做一轮老旧 Issue 清理。

**#1435 [CLOSED] [enhancement] 为 Kimi For Coding API 增加 PicoClaw 支持**
- 作者：@clawaizhang ｜ 创建：2026-03-14 ｜ 更新：2026-09-15 ｜ 评论：0 ｜ 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1435
- **为什么重要**：请求将 **Kimi For Coding 订阅接入第三方开源 AI Agent 项目 PicoClaw**（sipeed/picoclaw）。作者指出当前 API 对第三方客户端存在访问限制，导致无法在自己的订阅下使用外部 Agent。这触及"**订阅能力是否开放给第三方工具链**"这一生态策略问题。
- **社区反应**：0 评论、0 点赞，且以关闭收场——在无维护者公开说明的情况下，尚不清楚是已支持、转为其他渠道跟进，还是被判定为超出仓库范围。**建议关注是否有配套的官方说明**，否则同类请求会反复出现。

---

## 4. 重要 PR 进展

过去 24 小时内**无 Pull Request 更新**，本期无内容可报。

对于一个日活量不低的 CLI 工具而言，PR 流转为 0 值得留意：结合 Issue 端"老 Issue 集中关闭、新功能需求缺少 PR 承接"的现状，可能反映当前处于**发版间隙或合并冻结期**。

---

## 5. 功能需求趋势

从本期仅有的 4 条 Issue 中，可提炼出以下方向：

| 方向 | 代表 Issue | 说明 |
|---|---|---|
| **计费与配额透明度** | #2626 | 用户有能力、也愿意从 CLI 侧取证（日志、计费字段）来质疑用量统计。cache 计费口径的可见性与准确性正成为付费用户关注焦点。 |
| **macOS / 原生平台体验** | #1433 | 快捷键、剪贴板、路径等平台差异仍是 bug 主要来源，跨平台等价性是长期欠账。 |
| **第三方 Agent 与工具链集成** | #1435 | 社区希望把 Kimi For Coding 订阅带入 PicoClaw 等外部 Agent 生态，API 开放边界是核心争议点。 |
| **桌面端产品线治理** | #2646 | Kimi Work / Kimi Desktop 缺少独立公开跟踪渠道，需求被迫"借道"提交。 |
| **会话组织与检索** | #2646 | 会话标题结构化（如日期前缀）反映用户会话量增长后对归档、检索的实际需求。 |

---

## 6. 开发者关注点

1. **缓存计费是否可信，是当前最大的信任风险点。** cache_read 逐轮计费 + cache_creation 恒为 0 的组合，若确为计费缺陷，会直接放大所有重度用户的成本。开发者需要的不只是修复，还有**可自查的用量明细**（每轮 token / cache 命中与写入的账单可见性）。
2. **长尾平台差异 bug 的修复周期偏长。** #1433 从 3 月拖到 9 月才关闭，对 macOS 主力开发者群体而言，日常操作级功能（粘贴图片）不可用半年，体验损耗明显。
3. **反馈通路不清晰，正在产生"错位提交"。** #2646 的 Routing note 是明确信号：用户不知道 Kimi Work/Desktop 的问题该提到哪里。建议提供统一入口或多仓库跳转指引。
4. **第三方集成诉求缺少官方明确答复。** #1435 在 0 评论状态下关闭，用户无法判断这是"能力已开放"还是"策略不允许"。**策略类 Issue 关闭时应附一句结论**，可显著降低重复提问。
5. **本期无 PR 活动。** 若为非合并窗口属正常；若持续多日，则意味着社区贡献与维护吞吐之间的落差在扩大，值得关注后续 Release 节奏。

---

*本期数据量有限，趋势结论基于 4 条 Issue 样本，请结合后续日报连续观察。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 · 2026-09-16

> 数据来源：github.com/anomalyco/opencode

---

## 1. 今日速览

今天没有新版本发布，社区焦点集中在 **1.18.30 的严重回归崩溃**：`SystemPrompt.environment` 抛出的 `TypeError: undefined is not an object (evaluating 'a.name')` 已由至少 3 个独立 Issue 报告，累计 60+ 评论、55+ 👍，属于阻塞级问题。与此同时，V2 新 UI 的「强制单会话 + 强制水平标签页」激起了较大反弹（#36942 / #48888），支付与配额相关的投诉也占据热榜前列。PR 侧则以前后端协议对齐、数据库迁移保护和 AI 配额错误分类为主，修复节奏明显加快。

---

## 2. 版本发布

过去 24 小时无新 Release。

---

## 3. 社区热点 Issues

### 🔴 阻塞级 Bug

**1. 1.18.30 全量 prompt 崩溃（同一根因的三个 Issue）**
- [#48645](https://github.com/anomalyco/opencode/issues/48645) — 9 评论 / 15 👍，pacman 升级到 1.18.30 后每条 prompt 立即报 `Unexpected server error`，1.18.18 正常
- [#48372](https://github.com/anomalyco/opencode/issues/48372) — 6 评论 / 23 👍，`opencode run` 与 TUI 双双崩溃
- [#49158](https://github.com/anomalyco/opencode/issues/49158) — 6 评论 / 17 👍，附完整堆栈 `SystemPrompt.environment (chunk-y88jw4qv.js:50:13096)`

**为什么重要**：这是当前最高优先级的可用性事故，任何一次 prompt 都必然失败，等于让 1.18.30 版本完全不可用。三个 Issue 完全同源，说明影响面广且复现成本极低，社区情绪明显焦虑。

### 🟠 产品体验争议

**2. [#36942](https://github.com/anomalyco/opencode/issues/36942) — [FEATURE] 垂直标签页（20 评论 / 38 👍）**
新 UI 强制水平标签页，超过 5 个会话标题就无法同时查看。这是过去 24 小时评论数最高的 Issue，反映出重度多会话用户对新 UI 布局的强烈不满。

**3. [#48888](https://github.com/anomalyco/opencode/issues/48888) — 原有布局被强制替换为单会话界面（11 评论 / 4 👍）**
用户被强制切换到「只有一个会话面板」的窗口，多项目、多会话场景必须频繁点击 Home 或按 Ctrl+B。语气激烈，与 #36942 形成同一诉求的合流。

### 🟡 商业化与计费

**4. [#45278](https://github.com/anomalyco/opencode/issues/45278) — 用了 3 个月的信用卡突然被拒付（19 评论）**
同一张卡、同一银行，银行确认无异常，但订阅续费持续被拒。评论数第二高，说明并非个例，支付链路可能存在服务端问题。

**5. [#48330](https://github.com/anomalyco/opencode/issues/48330) — [2.0] Copilot Legacy 单次 prompt 耗尽全部配额（8 评论）**
Legacy Copilot 订阅（1500 请求/月）在 opencode2 中被一次会话全部消耗并触发 429，opencode 1 无此问题。属于 V2 费用模型的严重回归。

**6. [#45989](https://github.com/anomalyco/opencode/issues/45989) — 限流后无限重试且无日志（9 评论）**
遇到 rate limit 后每 3 秒无限重试，既不显示 backoff/重置时间，后端也无任何错误或网络事件记录。用户既看不到真实原因，也无法自助排查。

### 🟢 能力与安全

**7. [#1168](https://github.com/anomalyco/opencode/issues/1168) — 让链接可点击（Ctrl+左键打开浏览器）（12 评论 / 133 👍）**
全榜 👍 数最高的 Issue，从 2025 年 7 月一直活到今天仍处于 OPEN。属于低成本、高共识的体验改进，长期未落地是社区摩擦点。

**8. [#42263](https://github.com/anomalyco/opencode/issues/42263) — PDF 附件无大小限制且每轮重复 base64 编码导致 OOM（4 评论）**
整个 PDF 被无上限 base64 编码进内存，且每一轮对话都重新编码。对处理长文档的开发者是硬伤。

**9. [#49222](https://github.com/anomalyco/opencode/issues/49222) — TUI 启动无条件占用 6.5–7GB RSS（2 评论）**
全新空目录、无插件、无内容、无历史，仍然吃掉近 7GB 内存。与 #42263 一起指向内存管理这一系统性问题。

**10. [#36682](https://github.com/anomalyco/opencode/issues/36682) — [SECURITY] 压缩摘要注入可执行指令（5 评论）**
自动压缩生成的摘要若包含「Next Move」行动计划，模型会当作用户输入直接执行，无需用户确认。这是一条明确 Prompt Injection 向量，值得安全团队优先评估。

---

## 4. 重要 PR 进展

**1. [#49225](https://github.com/anomalyco/opencode/pull/49225) — fix(core): DB schema 领先运行时时应快速失败**
一次性关闭 #49177、#38471、#35403。桌面端、CLI 和插件共用同一个 `opencode.db`，谁先打开谁就可能推进 schema，导致落后运行时出现 `no such column: replacement_seq`。这是今天最有价值的健壮性修复。

**2. [#49195](https://github.com/anomalyco/opencode/pull/49195) — fix(ai): 将网关账户限额归类为 quota，4xx 不再重试**
把 HTTP 402 归类为 `QuotaExceeded`，将 OpenCode Zen 的 `GoUsageLimitError` / `FreeUsageLimitError` / `CreditLimitExceeded` 纳入 `QUOTA_CODES`。直接对应 #45989 一类的无限重试问题。

**3. [#49241](https://github.com/anomalyco/opencode/pull/49241) — fix(core): 保持配置的 MCP URL 作为 OAuth resource**
关闭 #46316。交互式登录与连接刷新此前发送了不同的 RFC 8707 `resource`，被严格授权服务器以 `invalid_target` 拒绝。影响远程 MCP 接入的可靠性。

**4. [#49235](https://github.com/anomalyco/opencode/pull/49235) — feat(core): 向 code mode 脚本暴露 fetch**
`execute` 工具运行的脚本现在可以直接调用 `fetch`，基于 #49196 的 host function 机制实现，不引入新运行时类型。显著扩展了 code mode 的表达能力。

**5. [#49249](https://github.com/anomalyco/opencode/pull/49249) — fix(codemode): 将 `tools.search` 视为内置 search**
弱模型常写成 `tools.search({query})`，此前会报 `Unknown tool 'search'`——从模型视角看这是「我刚做的动作失败了」。属于高性价比的模型兼容性修补。

**6. [#49250](https://github.com/anomalyco/opencode/pull/49250) / [#49163](https://github.com/anomalyco/opencode/pull/49163) — fix(tui): 合并 thinking 与 patch 的进度行**
当 thinking 块打开且 patch 工具同时运行时，时间线会画两条 spinner 行。修复后合并展示，TUI 视觉噪声下降。

**7. [#49223](https://github.com/anomalyco/opencode/pull/49223) — fix(session): 会话标题生成增加重试与模型回退**
关闭 #42287、#30662。标题生成只跑一次小模型，失败后会话永久停留在 `New session - ...`。现在会重试并回退到会话模型。

**8. [#49245](https://github.com/anomalyco/opencode/pull/49245) — feat(session): 新增 `auto` 推理强度变体**
当模型暴露多个 reasoning effort 时，额外提供 `auto` 选项，由系统在会话内自动选择。降低了用户手动调参的负担（该 PR 已 CLOSED，可能被后续实现替代）。

**9. [#49236](https://github.com/anomalyco/opencode/pull/49236) — test(desktop): 删除 395 个测试文件中的 335 个（85%）**
保留全部 benchmark、时间线稳定性检查和 profiling 工具，仅保留模型选择与签名相关测试。这是一个信号强烈的工程取舍，值得关注它是否会影响桌面端回归防护能力。

**10. [#49071](https://github.com/anomalyco/opencode/pull/49071) — fix(ai): 对 OpenAI prompt cache key 改用白名单**
`lowerOptions` 此前无条件把 `promptCacheKey` 降级为 `prompt_cache_key`，改为白名单后可避免不兼容供应商收到意外字段。

> 另有一批协议/测试对齐类 PR 集中合入：[#49251](https://github.com/anomalyco/opencode/pull/49251)（ACP fixture 契约）、[#49246](https://github.com/anomalyco/opencode/pull/49246) 与 [#49248](https://github.com/anomalyco/opencode/pull/49248)（`session.form.list` 断言修正）、[#49243](https://github.com/anomalyco/opencode/pull/49243)（plugin host fixture）。这些都是在为「interactive resources 迁移到 Session API」的重构收尾，说明 V2 协议层仍在快速演进。

---

## 5. 功能需求趋势

从本期全部 Issues 中可以提炼出六条主线：

| 方向 | 代表 Issue | 社区信号 |
|---|---|---|
| **UI / 布局可配置性** | [#36942](https://github.com/anomalyco/opencode/issues/36942)、[#48888](https://github.com/anomalyco/opencode/issues/48888) | 最强反弹。用户要求垂直标签、多会话面板回归，反对单会话强制布局 |
| **超长上下文与输出管理** | [#17471](https://github.com/anomalyco/opencode/issues/17471)、[#42263](https://github.com/anomalyco/opencode/issues/42263) | 1M 上下文时代，输出触顶后自动续写、附件内存上限成为刚需 |
| **模型/供应商兼容性** | [#48069](https://github.com/anomalyco/opencode/issues/48069)、[#49028](

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-09-16）

## 1. 今日速览

过去 24 小时，`cua-driver-rs v0.20.9` 发布，提供 macOS 签名公证、Linux/Windows 预构建二进制。社区侧，TUI 静默退出问题 #11500 仍是最高热度 P1；同时 ACP 权限审批、OpenAI 兼容网关参数序列化、VS Code Remote-SSH 等集成问题集中出现。修复侧，MiniMax 空 `parameters`、review worktree 路径、NTFS bigint 文件 ID、`settings.json` BOM 等 PR 正在推进。

---

## 2. 版本发布

### cua-driver-rs v0.20.9

过去 24 小时发布 Qwen CUA Driver 预构建二进制，vendored 在 `packages/cua-driver` 下。

- **macOS**：codesigned + notarized universal binary + `QwenCuaDriver.app`
- **Linux**：unsigned，x86_64 + arm64，glibc 2.31 floor
- **Windows**：unsigned UIAccess worker + native SDK payload，x86_64 + arm64

链接：https://github.com/QwenLM/qwen-code/releases

---

## 3. 社区热点 Issues

### #11500 [OPEN][P1] TUI 在多个后台代理完成时静默退出（React #185）

作者 @zaalipro，15 条评论，1 个 👍。多个后台 subagent 连续完成时，交互式 TUI 因未捕获的 `Minified React error #185`（Maximum update depth exceeded）直接掉回 shell，恢复后 CLI 还报告 “Previous session appears...”。这是当前最热的 P1 稳定性问题，指向 Ink `useBoxMetrics` 布局监听器 setState 循环。  
链接：https://github.com/QwenLM/qwen-code/issues/11500

### #2382 [CLOSED] VS Code Companion 扩展再次无法工作

作者 @AndyInjiner，9 条评论。用户反馈 0.12.2 可用、0.12.3 不可用，并尝试降级 VS Code 版本仍无效。该问题从 2026-03 持续到近期关闭，说明 VS Code 扩展兼容性是长期高关注区。  
链接：https://github.com/QwenLM/qwen-code/issues/2382

### #11834 [CLOSED][P1] API 400：`function parameters is empty (2013)`

作者 @wangvhero，7 条评论。用户发送“你好”即触发 `400 invalid params, function parameters is empty`，同时 `/update` 显示 Qwen Code 0.23.3 已是最新。该问题直指无参数工具在 OpenAI 兼容链路上的参数序列化，后续 PR #11842 已尝试在 MiniMax 路径修复。  
链接：https://github.com/QwenLM/qwen-code/issues/11834

### #11556 [CLOSED][P1] vscode-ide-companion 0.23.1 在 Remote-SSH 下卡在 webview loading

作者 @max-xue，7 条评论。环境为 VSCode 1.133.0 客户端 + 1.137.0 Remote-SSH Server（linux-arm64），扩展 0.23.1 无法在远程工作区正常加载。Remote-SSH 是专业开发者高频场景，该问题影响 IDE 集成可用性。  
链接：https://github.com/QwenLM/qwen-code/issues/11556

### #11574 [CLOSED][P2] VS Code 扩展更新后隐藏所有旧会话历史

作者 @Luolingli，7 条评论。VS Code 扩展 0.23.1 的会话历史对话框硬编码 `sourceType` 过滤，只显示 `"vscode"` 来源，而 0.23.x 之前由 VS Code 扩展或终端 CLI 持久化的会话缺少该元数据，导致历史全部不可见。该问题涉及升级兼容与会话迁移。  
链接：https://github.com/QwenLM/qwen-code/issues

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*