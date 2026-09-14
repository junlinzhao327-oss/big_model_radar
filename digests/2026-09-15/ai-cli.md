# AI CLI 工具社区动态日报 2026-09-15

> 生成时间: 2026-09-14 22:36 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告  
**日期：2026-09-15**  
**数据口径**：基于各工具当日社区动态摘要；Issues/PR 数量为“日报可见热点/重要条目”，非仓库全量。Claude Code、GitHub Copilot CLI 本次无数据，暂不纳入横向比较。

---

## 1. 生态全景

当前 AI CLI 工具正从“模型能力比拼”转向“生产可用性竞争”：跨平台稳定性、多 Agent 编排、权限安全、TUI 可观测性成为主战场。OpenAI Codex 与 OpenCode 社区体量最大、Issue/PR 最密集，但 Windows 稳定性与 V2 UI 强制迁移暴露出成熟度短板。Gemini CLI 以安全加固和 Agent 可靠性为主线，Qwen Code 发布正式版并推进 CUA 跨平台二进制，Kimi 则聚焦 CJK 输入与审阅协作。整体呈现“功能迭代快、稳定性债集中偿还、可配置/可观测成刚需”的态势。

---

## 2. 各工具活跃度对比

| 工具 | 日报可见 Issues | 日报可见 PR | Release 情况 | 今日核心信号 |
|---|---:|---:|---|---|
| Claude Code | 无数据 | 无数据 | 无 | 本次摘要未提供 |
| OpenAI Codex | 热点 10 | 重要 10 | `rust-v0.155.0-alpha.4` | Windows 稳定性集中爆发；TUI 状态栏 182👍 |
| Gemini CLI | 热点 10 | 安全类 PR 5+ | `v0.61.0-nightly.20260914` | 安全权限修复；P1 Agent 可靠性问题 |
| GitHub Copilot CLI | 无数据 | 无数据 | 无 | 本次摘要未提供 |
| Kimi Code CLI | 3 条更新（1 closed / 2 open） | 0 | 无 | 多 Agent 配额、IME 误发送、审阅批注 |
| OpenCode | 热点 10（从 50 条提炼） | 重要 10 | `v1.18.31` | V2 布局争议；macOS 崩溃；可观测性 PR |
| Q

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告  
数据截止：2026-09-15  
> 注：PR 评论数字段缺失，以下“热度”综合关联 Issue 评论/点赞、更新时间与影响面判断。展示的热门 PR 均为 OPEN，未出现 merged/draft 状态。

## 1. 热门 Skills 排行

| 排名 | Skill / PR | 功能 | 社区讨论热点 | 状态 |
|---|---|---|---|---|
| 1 | **skill-creator 评测修复** [#1298](https://github.com/anthropics/skills/pull/1298) | 修复 `run_eval.py` 始终报告 `recall=0%`，影响 `run_loop.py`、`improve_description.py` | 关联高讨论 Issue [#556](https://github.com/anthropics/skills/issues/556)（12 评论 / 7 👍）：技能触发率 0%，描述优化在噪声上优化；还涉及 Windows 流读取、触发检测、并行 worker | OPEN |
| 2 | **mcp-builder 兼容 MCP v2** [#1742](https://github.com/anthropics/skills/pull/1742) | 支持 `mcp>=2` 的 `streamable_http_client` 导入与自定义 headers | 修复 [#1668](https://github.com/anthropics/skills/issues/1668)；MCP 版本升级导致连接脚本失效，是工具链兼容性热点 | OPEN |
| 3 | **document-typography** [#514](https://github.com/anthropics/skills/pull/514) | AI 生成文档的排版质量控制：孤词换行、孤行段落、编号错位 | 文档生成是高频场景，社区希望 Skills 不只“生成内容”，还“保证出版级质量” | OPEN |
| 4 | **skill-quality-analyzer + skill-security-analyzer** [#83](https://github.com/anthropics/skills/pull/83) | 元技能：从结构、文档、安全等维度评估 Skill 质量 | 与安全信任、质量治理趋势高度呼应；社区需要官方/半官方的 Skill 审核工具 | OPEN |
| 5 | **Hivemind 多智能体编排** [#1628](https://github.com/anthropics/skills/pull/1628) | Claude Code 作为唯一 planner/reviewer/merger，把机械工作委派给免费 headless opencode worker | 多 Agent、成本控制、上下文节省是明显热点；“昂贵模型管规划，免费模型干机械活” | OPEN |
| 6 | **md2video-audio** [#1703](https://github.com/anthropics/skills/pull/1703) | Markdown → Marp 幻灯片 → MP4，并生成拟真配音 | 零成本多媒体内容自动化；把文档工作流延伸到视频生产 | OPEN |
| 7 | **pyxel 复古游戏开发** [#525](https://github.com/anthropics/skills/pull/525) | 面向 Pyxel / pyxel-mcp 的像素游戏开发 Skill | 由上游作者 @kitao 提交，覆盖 write → run_and_capture → inspect → iterate 工作流 | OPEN |
| 8 | **ODT 文档 Skill** [#486](https://github.com/anthropics/skills/pull/486) | OpenDocument 文本创建、模板填充、ODT 转 HTML | 开源/ISO 办公格式需求，补齐 docx/pdf 之外的文档生态 | OPEN |

## 2. 社区需求趋势

1. **安全与信任边界成为第一痛点**  
   [#492](https://github.com/anthropics/skills/issues/492)（43 评论）指出社区 Skill 被分发在 `anthropic/` namespace 下，可能被误认为官方 Skill，造成权限提升与信任边界滥用。社区需要命名空间隔离、签名、来源标识与权限审计。

2. **组织内共享与分发机制**  
   [#228](https://github.com/anthropics/skills/issues/228)（16 评论 / 8 👍）希望 Claude.ai 支持组织级 Skill 共享库、直接分享链接，而不是让人下载 `.skill` 文件再手动上传。安装重复问题也出现在 [#189](https://github.com/anthropics/skills/issues/189)。

3. **评测、触发与质量验证可靠性**  
   [#556](https://github.com/anthropics/skills/issues/556) 的 0% 触发率、[#1390](https://github.com/anthropics/skills/issues/1390) 的 mcp-builder 评测 0/N、[#1602](https://github.com/anthropics/skills/pull/1602)、[#1724](https://github.com/anthropics/skills/pull/1724) 都指向同一问题：Skill 评测链不稳，优化信号不可信。

4. **上下文效率与权限控制**  
   [#1487](https://github.com/anthropics/skills/issues/1487) 抱怨 `claude-api` Skill 一次注入约 156k tokens；[#1175](https://github.com/anthropics/skills/issues/1175) 关注 SharePoint 文档的权限与上下文窗口。社区期待 Skill 更“懒加载”、更 token-efficient。

5

---



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报

**日期：2026-09-15**
**数据来源：github.com/openai/codex**

---

## 1. 今日速览

过去 24 小时，Codex 社区最突出的信号是 **Windows 平台稳定性问题集中爆发**：Computer Use 截图失败、WSL 项目创建阻塞、沙箱句柄/登录会话泄漏、MCP 子进程不回收等长期 Issue 持续获得高热度讨论。功能侧，**TUI 可定制状态栏**以 182 👍 成为最高赞需求，社区对终端体验定制化的呼声强烈。PR 方面集中合并了一批 app-server、Guardian、MXC 网络与 TUI 渲染相关改进。

---

## 2. 版本发布

### rust-v0.155.0-alpha.4
- 发布版本：`0.155.0-alpha.4`
- 说明：Release 页面未提供详细变更日志，仅版本号更新。
- 链接：https://github.com/openai/codex/releases

---

## 3. 社区热点 Issues

挑选过去 24 小时内更新、评论/点赞/影响面最突出的 10 个 Issue：

### ① #17827 可定制状态栏（TUI）
- **状态**：OPEN | 评论 45 | 👍 182
- **重要性**：社区最高赞功能请求。用户希望像 Claude Code 一样在 TUI 底部显示 token 用量、模型名、速率限制、上下文窗口、Git 分支等实时信息，并通过 shell 脚本配置。
- **社区反应**：高赞表明终端用户对可观测性和个性化界面有强烈需求。
- 链接：https://github.com/openai/codex/issues/17827

### ② #41463 [Windows + WSL] 无法创建项目 – AbsolutePathBuf 缺少 base path
- **状态**：OPEN | 评论 56 | 👍 33
- **重要性**：Windows + WSL2 环境下 Codex Desktop 无法创建项目，属于阻塞性缺陷，影响大量 Windows 开发者。
- **社区反应**：评论数极高，用户持续补充复现信息，说明问题普遍且尚未解决。
- 链接：https://github.com/openai/codex/issues/41463

### ③ #25178 Windows Computer Use 截图失败（SetIsBorderRequired 不支持）
- **状态**：OPEN | 评论 58 | 👍 25
- **重要性**：Windows 10 22H2 上 `get_window_state` 截图失败，报 `0x80004002`，导致 Computer Use 核心能力不可用。
- **社区反应**：评论最多，Windows 桌面端用户受影响严重。
- 链接：https://github.com/openai/codex/issues/25178

### ④ #40060 Windows execpolicy 误报：Start-Process 与 URL 同现
- **状态**：OPEN | 评论 17
- **重要性**：PowerShell 脚本中同时出现 `Start-Process` 和无关 URL 时，execpolicy 分类器误判，影响 CLI 沙箱正常使用。
- **社区反应**：用户已确认 0.146.0、0.149.0 及 main 分支均存在，说明是长期逻辑缺陷。
- 链接：https://github.com/openai/codex/issues/40060

### ⑤ #25826 Windows 桌面：多显示器下最大化窗口溢出到相邻屏幕
- **状态**：OPEN | 评论 16 | 👍 18
- **重要性**：多显示器办公场景常见，窗口管理异常直接影响日常使用体验。
- **社区反应**：点赞和评论表明并非个例。
- 链接：https://github.com/openai/codex/issues/25826

### ⑥ #35347 Windows Codex 桌面应用无法启动，AppX 状态为 Modified / NeedsRemediation
- **状态**：OPEN | 评论 15 | 👍 2
- **重要性**：Microsoft Store 安装的桌面应用完全无法启动，属于安装/更新链路严重问题。
- **社区反应**：Windows 11 25H2 用户反馈，影响面较大。
- 链接：https://github.com/openai/codex/issues/35347

### ⑦ #33356 Windows 沙箱每次执行泄漏 3–5 个 lsass 句柄
- **状态**：OPEN | 评论 13 | 👍 1
- **重要性**：长时间会话下句柄泄漏会拖慢整个 OS，属于性能与系统稳定性隐患。
- **社区反应**：用户实测并量化了泄漏速度，问题真实且持续。
- 链接：https://github.com/openai/codex/issues/33356

### ⑧ #28361 Windows 下 codex mcp-server / app-server 子进程永不回收
- **状态**：OPEN | 评论 11 | 👍 3
- **重要性**：每次请求都会生成新的 app-server 和 MCP 子进程，累积到数百个，导致资源耗尽。
- **社区反应**：与 #33356 类似，反映 Windows 进程生命周期管理存在系统性问题。
- 链接：https://github.com/openai/codex/issues/28361

### ⑨ #45019 App-server 排队跟进请求丢失
- **状态**：OPEN | 评论 5 | 👍 26
- **重要性**：排队中的 follow-up 消息会消失，属于会话状态丢失，影响多轮协作可靠性。
- **社区反应**：点赞数很高，说明较多用户遇到同类问题。
- 链接：https://github.com/openai/codex/issues/45019

### ⑩ #38157 ChatGPT Pro (20x) 账户似乎只获得 Pro 5x 的 Codex 用量
- **状态**：OPEN | 评论 10 | 👍 5
- **重要性**：付费等级与实际用量不符，涉及计费公平性和 API `plan_type` 识别问题。
- **社区反应**：多个 Pro 账户确认，用户对配额透明度不满。
- 链接：https://github.com/openai/codex/issues/38157

---

## 4. 重要 PR 进展

过去 24 小时更新的 PR 多为已关闭的合并项，作者以 `copyberry[bot]` 为主。挑选 10 个重要 PR：

### ① #45529 在 app-server 账户读取中暴露所选工作区路由
- **内容**：新增实验性 `account/read.workspaceRouting` 元数据，包含所选 ChatGPT 工作区 ID、HTTPS 后端源和路由覆盖（`us`、`us_cr`、`NO_CONSTRAINT`）。
- 链接：https://github.com/openai/codex/pull/45529

### ② #45524 在 exec server 中启用 MXC TTY 启动与托管网络
- **内容**：Windows 上报告 `windows_mxc` 原生可用性；允许 MXC TTY 启动和托管网络，使用专用代理监听器，无需共享入口限制 SID。
- 链接：https://github.com/openai/codex/pull/45524

### ③ #45521 将 Guardian reviewer 启动移入池
- **内容**：用启动回调替代 `ReviewerSessionFactory`，通过 `ReviewerPool::new` 安装；审核请求复用上下文，池用回调创建可复用和分叉的 reviewer。
- 链接：https://github.com/openai/codex/pull/45521

### ④ #45519 恢复线程时的协作模式
- **内容**：修复恢复线程时协作模式被初始化为 Default、丢失 Plan 模式及开发者指令的问题；重连客户端也能获得服务端上报的模式。
- 链接：https://github.com/openai/codex/pull/45519

### ⑤ #45513 启动线程时允许设置 daybreakEnabled
- **内容**：新增实验性 `thread/start.daybreakEnabled`，客户端可设置持久线程的初始偏好；临时线程显式设置会被拒绝。
- 链接：https://github.com/openai/codex/pull/45513

### ⑥ #45509 在搜索结果选中前共享 MCP 工具规格
- **内容**：优化 MCP 搜索条目构建，使用 `Arc<ToolSpec>` 共享 handler 规格，避免为未选中的工具急切克隆和规范化 schema。
- 链接：https://github.com/openai/codex/pull/45509

### ⑦ #45506 允许对 steered 用户输入进行后台持久化
- **内容**：新增 `PersistContext::SteeredUserInput`，支持后台持久化的存储可将检查点与推理重叠，避免阻塞下一次模型请求。
- 链接：https://github.com/openai/codex/pull/45506

### ⑧ #45505 为统一 exec 添加生命周期追踪
- **内容**：为一次性/可恢复 `exec_command`、`write_stdin`、会话创建和输出收集添加 span，记录结果和输出收集停止原因，并关联对话、回合和进程。
- 链接：https://github.com/openai/codex/pull/45505

### ⑨ #45503 为 HTTP 客户端添加可撤销网络策略原语
- **内容**：新增 `NetworkPolicyController` 和 `NetworkPolicy` API，用于发布目标策略、检查访问和观察策略变化；

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-09-15** | 数据来源：[google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)

---

## 一、今日速览

1. **安全与权限修复成为今日主线**：核心仓库集中出现了 5 个以上涉及策略目录权限、A2A 凭证日志泄露、沙箱扩展递归限制的安全类 PR，安全加固节奏明显加快。
2. **Agent 可靠性问题持续占据 Issue 热榜**：子代理“MAX_TURNS 被误报为成功”、通用代理挂起、Shell 执行卡在「等待输入」等高优先级 Bug 更新频繁，P1 级问题仍是社区最大痛点。
3. **夜间版本照常发布**：`v0.61.0-nightly.20260914` 已跟进，配套的自动版本 bump PR #29321 同步开启。

---

## 二、版本发布

### v0.61.0-nightly.20260914.g9c1b0a610

- 类型：夜间构建（Nightly）
- 变更范围：仅包含 commit `g9c1b0a610`，未附带额外 release notes
- 对比链接：[Full Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.61.0-nightly.20260913.g9c1b0a610...v0.61.0-nightly.20260914.g9c1b0a610)
- 对应 PR：[#29321 chore/release: bump version](https://github.com/google-gemini/gemini-cli/pull/29321)

> 建议关注 nightly 用户重点验证今日合并的 A2A / 策略目录相关修复是否生效。

---

## 三、社区热点 Issues

### 1. [#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — 子代理 MAX_TURNS 中断被误报为 GOAL 成功（**P1 / 13 评论**）
`codebase_investigator` 子代理在耗尽最大回合数时仍返回 `status: "success"` 和 `Termination Reason: "GOAL"`，导致用户误以为分析已完成。这是**结果可信度问题**，对 CI/自动化调用危害最大，评论数最多，说明影响面广。

### 2. [#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — 通用代理（generalist agent）无限挂起（**P1 / 8 👍**）
一旦请求被转交给通用代理，简单任务（如创建文件夹）也会永久挂起，用户最长等待一小时。**8 个点赞 + 8 条评论**，是当前用户呼声最高的可靠性问题之一。

### 3. [#19873](https://github.com/google-gemini/gemini-cli/issues/19873) — 利用模型原生 bash 能力 + 零依赖 OS 沙箱（**P2 / 9 评论**）
提案主张 Gemini 3 模型天生擅长链式调用 POSIX 工具，应通过零依赖沙箱安全地释放这一能力。**架构级方向提案**，可能影响未来工具执行层设计。

### 4. [#22745](https://github.com/google-gemini/gemini-cli/issues/22745) — 评估 AST 感知的文件读取、搜索与代码映射（**P2 / 7 评论**）
EPIC 级议题，目标是减少无效读取、降低 token 噪声并精准定位方法边界。与 #22746 联动，代表 **context 效率优化** 的长期路线。

### 5. [#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — Gemini 主动使用 skills / sub-agents 的频率过低（**P2 / 6 评论**）
用户反馈即使配置了 gradle、git 等 skill，模型也不会自发调用，必须显式指令。暴露出**代理调度策略**层面的缺口。

### 6. [#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — Shell 命令结束后仍卡在「Waiting input」（**P1 / 3 👍**）
命令实际上已执行完毕，但 UI 仍显示「Awaiting user input」，需手动干预。**高频交互体验痛点**。

### 7. [#26525](https://github.com/google-gemini/gemini-cli/issues/26525) — Auto Memory 增加确定性脱敏、减少日志输出（**P2 / 5 评论**）
当前脱敏依赖模型 prompt 指令，**敏感内容已经进入模型上下文后才被处理**，存在合规风险。属于安全类隐性问题。

### 8. [#22672](https://github.com/google-gemini/gemini-cli/issues/22672) — 代理应停止/劝阻破坏性行为（**P2**）
模型在复杂 git 操作中偶尔使用 `git reset`、`--force` 等危险命令。需要**行为护栏**，与 #19873 沙箱提案方向互补。

### 9. [#24246](https://github.com/google-gemini/gemini-cli/issues/24246) — 工具数量超过 128 时触发 400 错误（**P2**）
大量 skill / MCP 工具启用后直接导致 API 报错，缺乏工具裁剪策略。反映**工具生态扩展后的规模治理问题**。

### 10. [#18836](https://github.com/google-gemini/gemini-cli/issues/18836) — 用持久化文件任务跟踪替换 WriteToDo（**P3**）
指出现有 Todo 依赖上下文内维护，存在「context rot」、token 成本高、跨会话丢失三大问题。属于**任务管理

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-09-15）

> 数据来源：github.com/MoonshotAI/kimi-cli  
> 统计范围：过去 24 小时内更新的 Releases、Issues、Pull Requests

## 1. 今日速览
过去 24 小时无新版本发布、无 PR 更新。社区仅有 3 条 Issue 动态：一条已关闭的多 Agent 并发限制/API rate limit 讨论，以及两条新开需求，分别聚焦 `kimi web` 中文输入法回车误发送、Kimi Work 对 Agent 回复的可视化批注与审阅反馈。整体反馈集中在多 Agent 配额透明度、Web 输入体验和人机协作审阅闭环。

## 2. 版本发布
无新 Release。

## 3. 社区热点 Issues
> 说明：过去 24 小时仅 3 条 Issue 更新，以下为全量列出，非 Top 10。

### #1383 [CLOSED] 多 Agent 并发时出现限制 / API rate limit
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1383
- 状态：已关闭｜作者：@asecret｜评论：6｜👍：0
- 摘要：用户使用 `kimi 1.15.0`、Allegretto 订阅，在 OpenClaw 上调用 API。会员权益称支持多 Agent，但两个“小龙虾”同时思考时出现 API rate limit。
- 为什么重要：涉及订阅权益承诺与多 Agent 并发实际限制的一致性，是付费用户较敏感的问题。该 Issue 已有 6 条评论并关闭，说明社区有一定讨论，可能已有官方回应或处理。

### #2643 [OPEN] kimi web 输入法组合状态下回车被误判为发送
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2643
- 状态：开放｜作者：@wangjin1982｜评论：0｜👍：0
- 摘要：在 `kimi web` 输入框使用中文/日文/韩文 IME 时，组词状态下按 Enter 本应确认拼音/字母上屏，却被误判为「发送消息」，导致未完成内容被直接发出。
- 为什么重要：直接影响 CJK 用户的基础输入体验，属于 Web 端高频交互 Bug。实现上需要正确区分 IME composition 状态与 Enter 发送事件。

### #2642 [OPEN] Kimi Work 会话内支持对 Agent 回复的可视化批注与审阅反馈
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2642
- 状态：开放｜作者：@Zhywleo｜评论：0｜👍：0
- 摘要：希望对 Agent 的任意回复，尤其是计划、报告、方案类长回复，支持逐段可视化批注，并将批注以结构化形式返回给 Agent 用于修订，而不是只能靠用户在输入框里用文字描述修改意见。
- 为什么重要：代表 Kimi Work / Kimi Code 在长内容审阅与人机协作闭环上的产品化需求，可显著降低审阅成本，并提升 Agent 修订效率。

## 4. 重要 PR 进展
过去 24 小时无 Pull Request 更新。

## 5. 功能需求趋势
从本期 Issues 看，社区关注方向集中在：

1. **多 Agent 并发与配额/速率限制透明度**  
   会员权益描述需与实际 API rate limit 对齐，避免用户对“支持多 Agent”的理解产生偏差。

2. **Web 端输入法兼容性**  
   CJK IME 组合输入与回车发送逻辑需要解耦，避免误发未完成内容。

3. **Agent 回复审阅与结构化反馈**  
   社区希望支持逐段可视化批注，并将批注结构化回传给 Agent，用于自动或半自动修订。

4. **跨工作流协作体验**  
   Kimi Work、Kimi Code、`kimi web` 之间的审阅、反馈与修订链路仍有明显产品化空间。

## 6. 开发者关注点
- **付费权益与技术限制不一致**：多 Agent 同时运行触发 rate limit，需要更清晰的配额说明或策略优化。
- **输入法场景边界处理**：Enter 在 IME composition 期间不应触发发送。
- **长回复审阅低效**：文字描述修改意见成本高，期望可视化批注与结构化反馈。
- **本期数据量较少**，但新 Issue 更偏真实使用体验和协作工作流，而非底层崩溃类问题。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 · 2026-09-15

> 数据来源：github.com/anomalyco/opencode

---

## 一、今日速览

今日 OpenCode 发布 `v1.18.31`，重点修复会话恢复/分叉时的 ACP 边界与远程配置认证错误处理。社区讨论热度集中在 **V2 新布局争议**（多篇 Issue 要求恢复旧版持久左侧栏）以及 **macOS 上 `SystemPrompt.environment` 崩溃**、**Zen/Muse Spark 家庭模型故障** 等关键稳定性问题。PR 方面，可观测性（W3C traceparent 透传）、协议重构与 codemode 类型跨边界传递成为主线。

---

## 二、版本发布

### v1.18.31
- **Core（Bugfix）**：恢复 ACP 会话在加载、resume、fork 时的 model、effort、mode 以及 reasoning chunk 边界（@JacobNWolf）。
- **TUI（Bugfix）**：启动阶段现在会显示远程配置认证错误，并以失败状态退出，避免静默启动。
- **Extensions**：Improvement 部分内容本次数据中被截断。

---

## 三、社区热点 Issues（挑选 10 条）

| # | 标题 | 状态 | 热度 | 链接 |
|---|------|------|------|------|
| 1 | **无法复制粘贴（CLI）** | OPEN | 59 评论 / 32 👍 | [#13984](https://github.com/anomalyco/opencode/issues/13984) |
| 2 | **SSE read timed out** | CLOSED | 47 评论 / 37 👍 | [#17318](https://github.com/anomalyco/opencode/issues/17318) |
| 3 | **Zen 上 Muse Spark 系列严重错误**（图片/工具调用触发） | OPEN | 26 评论 | [#48741](https://github.com/anomalyco/opencode/issues/48741) |
| 4 | **恢复旧版持久左侧栏 UI 作为选项** | OPEN | 14 评论 / 18 👍 | [#48882](https://github.com/anomalyco/opencode/issues/48882) |
| 5 | **Desktop 本地 provider 5 分钟 Headers Timeout** | OPEN | 13 评论 | [#26602](https://github.com/anomalyco/opencode/issues/26602) |
| 6 | **每个 provider 支持多个 auth profile** | OPEN | 13 评论 / 41 👍 | [#5391](https://github.com/anomalyco/opencode/issues/5391) |
| 7 | **新增 CommandCode 作为 Provider** | CLOSED | 11 评论 / 43 👍 | [#26338](https://github.com/anomalyco/opencode/issues/26338) |
| 8 | **macOS：每个 prompt 都报 `undefined is not an object (evaluating 'a.name')`** | OPEN | 6 评论 / 29 👍 | [#48811](https://github.com/anomalyco/opencode/issues/48811) |
| 9 | **限流后无限重试且无日志（"Free usage exceeded"）** | OPEN | 8 评论 | [#45989](https://github.com/anomalyco/opencode/issues/45989) |
| 10 | **V2 强制界面破坏多项目/多 agent 工作流（20+ 会话）** | OPEN | 4 评论 / 13 👍 | [#48837](https://github.com/anomalyco/opencode/issues/48837) |

**为什么重要：**
- **#13984** 是长期未决的高热度可用性硬伤（CLI 复制粘贴失效），影响日常开发体验。
- **#48741** 暴露 Zen 网关 reasoning `encrypted_content` 校验缺陷，直接影响 Muse Spark 全系可用性。
- **#48811 / #48372** 属于同一根因（`SystemPrompt.environment` 崩溃），macOS 用户"每次 prompt 必崩"，被评为当前最高优先级稳定性缺陷之一。
- **#48882 / #48837 / #49021 / #49031 / #48953** 构成一股强烈的"布局回退"声浪——新 V2/Tabbed 布局被指破坏多项目并行、旧会话可见性等专业工作流。
- **#5391 / #26338** 反映出社区对多账号、多 provider 的强需求（43👍 的 CommandCode 虽被关闭，但呼声明确）。

---

## 四、重要 PR 进展（挑选 10 条）

| # | 标题 | 状态 | 链接 |
|---|------|------|------|
| 1 | **fix(client): 显式暴露被 contender 重叠掩盖的服务启动失败** | CLOSED | [#49040](https://github.com/anomalyco/opencode/pull/49040) |
| 2 | **refactor(ai): 引入 Protocol.withBody 协议请求体扩展**（迁移 Alibaba / Z.AI） | OPEN | [#49068](https://github.com/anomalyco/opencode/pull/49068) |
| 3 | **feat(codemode): Set/RegExp/URLSearchParams 跨宿主边界传递** | CLOSED | [#49065](https://github.com/anomalyco/opencode/pull/49065) |
| 4 | **fix(observability): 在出站 LLM 请求透传 W3C traceparent** | OPEN | [#49046](https://github.com/anomalyco/opencode/pull/49046) |
| 5 | **feat(app): Agents 舰队视图（token sparkline、阶段芯片、TTFT）** | OPEN | [#49066](https://github.com/anomalyco/opencode/pull/49066) |
| 6 | **fix: 修复 v2 分支 CI 失败（codemode limits 超时）** | CLOSED | [#49048](https://github.com/anomalyco/opencode/pull/49048) |
| 7 | **fix: TUI 黑屏 / provider 列表为空（对 v2 daemon）** | CLOSED | [#42658](https://github.com/anomalyco/opencode/pull/42658) |
| 8 | **refactor(core): 重构模型解析逻辑，修复 variant 缺失** | OPEN | [#48943](https://github.com/anomalyco/opencode/pull/48943) |
| 9 | **feat(config): 为 agent markdown prompt 增加 `{file:...}` 插值** | OPEN | [#49064](https://github.com/anomalyco/opencode/pull/49064) |
| 10 | **fix(llm): 处理被截断的 OpenAI 工具参数** | CLOSED | [#42566](https://github.com/anomalyco/opencode/pull/42566) |

**亮点解读：**
- **#49046** 与 Issue #49038 呼应，令 OTLP 网关可为 LLM 调用建立父级 span，补齐生产可观测性链路。
- **#49065** 修复了 `JSON.stringify` 语义下 Set/Map/RegExp 静默丢失数据的隐性坑。
- **#42658** 是自动化 PR 清理批次的一部分，修复 v2 daemon 下 TUI 完全不可用问题。
- **#49064** 提供了类似 `@file` 的轻量 prompt 组合能力，对多 agent 配置复用很有价值。

---

## 五、功能需求趋势

从 50 条 Issue 中提炼出的社区关注方向：

1. **UI/UX 布局可配置化（最热）** — 大量请求要求恢复旧版持久左侧栏 / 保留 V2 与旧版切换开关。代表：#48882、#48837、#49021、#49031、#38230、#48953。
2. **多 provider / 多账号支持** — 每个 provider 多 auth profile、新增第三方 Provider（CommandCode）。代表：#5391、#26338。
3. **可观测性与追踪** — 出站 LLM 请求透传 W3C traceparent（#49038/#49046）、MCP `tools/call` 的 trace context（#46856）。
4. **超时与网络健壮性** — 本地 provider 5 分钟硬超时不可配（#26602）、SDK `session.prompt` 300s undici 超时不可配（#49044）、SSE read timeout（#17318）。
5. **会话/项目持久化与恢复** — 更新后旧会话与项目丢失（#49029）、自动压缩对大上下文模型失效（#46137）。
6. **模型能力与路由** — 多模型协作（当前模型不支持图片时可切换图片生成模型，#49026）、DeepSeek V4 Flash 路由挂起（#40479、#49041）。
7. **TUI 交互细节** — 标签快捷键（Ctrl+T/W/Tab，#37077）、渲染链接可点击（#42625）。

---

## 六、开发者关注点（痛点与高频诉求）

- **强制迁移引发信任危机**：V2/Tabbed 布局在无回退开关的情况下强推，多项目、20+ 会话的重度用户直言"生产力被摧毁"，并出现"丢失历史会话/项目"的次生问题（#49029、#48837、#49031）。这是今日最强烈的负面情绪来源。
- **跨平台崩溃尚未收敛**：macOS 上 `SystemPrompt.environment` 抛 `TypeError` 导致每个 prompt 失败（#48811、#48372），29👍 显示影响面广。
- **超时机制缺乏可配置性**：多层超时（5 分钟 headers、300s undici、SSE read）均不可调，长任务/慢速本地模型直接被判死，是高频复现的生产阻塞项。
- **错误信息与日志缺口**：限流场景每 3 秒无限重试且无任何后端日志（#45989）、服务启动超时错误缺乏上下文（#49040），显著抬高排障成本。
- **供应链与安全误报**：Windows Defender/杀软将可执行文件标记为木马（#49047），已打上 `needs:compliance` 标签，需签名或上报处理。
- **存储与资源边界问题**：TUI 因 `ENOSPC` 崩溃（#48384）、`session_message.seq` NOT NULL 约束失败（#31204），指向 watch 与 migrations 的健壮性。

---

*如需追踪以上条目的后续进展，建议优先订阅 #48811、#48741、#49038 与 v1.18.x 发布线。*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-09-15）

> 数据来源：github.com/QwenLM/qwen-code

---

## 1. 今日速览

今日正式版 **v0.23.4** 发布，包含一项 channels 消息前缀过滤的破坏性变更；CUA Driver 同步推出 v0.20.8/v0.20.7 预构建二进制。社区侧最突出的信号是 **TUI 静默崩溃（React #185）** 系列问题持续发酵，多个 Issue 交叉印证同一根因；同时 **第三方模型兼容性、ACP 审批安全、Windows 扩展管理** 成为新的讨论焦点。维护者在 PR 侧密集推进修复，覆盖 node-pty 打包、Ink 循环守卫、shell 注释解析与 Linux bwrap 沙箱等方向。

---

## 2. 版本发布

### v0.23.4（正式版）
- **Breaking Change**：移除 channels 中可配置的 message-prefix 过滤机制，符合投递条件的消息现直接遵循标准的 sender / group / mention / pairing 策略，不再需要前缀。([#11571](https://github.com/QwenLM/qwen-code/pull/11571))
- 完整变更列表见 release notes。

### v0.23.4-nightly.20260914.f024b37689
- 夜间构建版本，包含 Windows inode gates 相关测试记录与取消 skip 等改动（PR #11853 等）。

### cua-driver-rs v0.20.8 / v0.20.7
- 发布 Qwen CUA Driver 预构建二进制（内置于 `packages/cua-driver`）：
  - **macOS**：已签名 + 公证的 universal binary，附带 `QwenCuaDriver.app`
  - **Linux**：未签名（x86_64 + arm64，glibc 2.31 为下限）
  - **Windows**：未签名的 UIAccess worker + 原生 SDK 载荷（x86_64 + arm64）

---

## 3. 社区热点 Issues

### 🔴 TUI 稳定性（最高优先级）

**1. [#11500](https://github.com/QwenLM/qwen-code/issues/11500) TUI 在多个后台 agent 连续完成时静默退出（React #185）**
- 标签：`priority/P1` `type/bug` `category/ui` `scope/rendering` | 13 条评论 | 👍 1
- 多个后台 subagent 密集完成时，交互式 TUI 抛出未捕获的 Minified React error #185（Maximum update depth exceeded），进程直接掉回 shell 无任何错误渲染。这是当前评论数最多的 Issue，指向 Ink

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*