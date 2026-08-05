# AI CLI 工具社区动态日报 2026-08-06

> 生成时间: 2026-08-05 23:26 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-08-06）

> 数据来源：各工具 GitHub 社区 Issues/PR/Release 动态。Gemini CLI、GitHub Copilot CLI 当日无数据收录，不作对比分析。

---

## 1. 生态全景

当日 AI CLI 工具整体呈 **"多强并立、迭代加速"** 态势：OpenAI Codex 以 1 个稳定版 + 4 个 alpha 密集推进 0.147 版本；Qwen Code 发布 4 个版本（含桌面版首发里程碑）；OpenCode 在社区高热度需求驱动下发布 v1.18.14 并为 V2 架构大规模重构。与此同时，各工具的社区反馈重心正从"功能缺失"转向 **"稳定性、安全性与跨平台体验"**——Claude Code 批量清理陈旧 Issue、Kimi Code 聚焦长上下文可靠性、Qwen Code 曝出 2 个 P1 级安全问题，均指向同一趋势：AI CLI 正从"能对话"的演示阶段迈向"可依赖"的生产工具阶段。

---

## 2. 各工具活跃度对比

| 工具 | 热点 Issues | PR 进展 | 版本发布 | 当日亮点 |
|------|:---:|:---:|:---:|------|
| Claude Code | 10 | 10（详情 1） | 0 | 无新版本；批量关闭 6 月陈旧 Issue；Cowork 桌面端问题集中 |
| OpenAI Codex | 10 | 10 | 5（1 稳定 + 4 alpha） | 0.147 快速迭代；Windows 相关 Issue 高发 |
| Kimi Code | 5（全量） | 2 | 0 | 无发布；跨会话记忆 + 高上下文可靠性讨论深入 |
| OpenCode | 10 | 10 | 1（v1.18.14） | V2 数据迁移重构；VS Code 扩展需求获 134 👍 |
| Qwen Code | 10 | 10 | 4（含 desktop-v0.1.0） | 发布频率最高；Live Voice 实验性上线；2 个 P1 安全 Issue |
| Gemini CLI | — | — | — | 当日无数据收录 |
| GitHub Copilot CLI | — | — | — | 当日无数据收录 |

**迭代速度排序**：Qwen Code（4 releases）＞ OpenAI Codex（5 releases）＞ OpenCode（1 release）＞ Claude Code = Kimi Code（0）。

---

## 3. 共同关注的功能方向

### ① 多代理/并行会话的可观测性与兼容性
- **OpenAI Codex**：`spawn_agent` 拒绝 `gpt-5.6-luna` 模型（#34700，30 👍，为当日最高赞 Issue）。
- **Claude Code**：FleetView 用"过时文本分类器"将活跃 agent 归入 Completed（#64036）。
- **OpenCode**：提出用 LLM 分类器实现"自动模式"权限审批（#37564）、多代理 UI/UX 可视化需求（#40564）。
- **Qwen Code**：headless Goal 工作流文档补充，长时任务证据 checkpoint 机制

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---

# Claude Code 社区动态日报 — 2026-08-06

## 今日速览

过去 24 小时官方未发布新版本，社区讨论热度集中在 **Cowork 桌面端稳定性**（Intel Mac 崩溃、AskUserQuestion 卡片不渲染）与 **Claude Max 计费/配额异常**（#82506）两大方向。此外，大量 stale 状态 Issue 被批量关闭（多为 6 月提交的 macOS/Windows 平台 bug），暗示官方正在进行一轮问题清理。PR 侧主要由外部开发者贡献，其中 RerankerGuo 提交了 7 个 plugin-dev 脚本健壮性修复，并有针对 Cowork 自签名证书问题的 workaround（#84138）。

---

## 社区热点 Issues（10 个）

### 1. #48827 — Cowork 在 Intel Mac 上错误下载 Linux 二进制导致崩溃（CLOSED）
- 链接: https://github.com/anthropics/claude-code/issues/48827
- 评论: 22 | 👍: 4
- 关键信息: 根因已定位——`claude-code-vm/2.1.92/claude` 下载的是 **ELF 64-bit Linux 可执行文件**而非 macOS 二进制，Intel Mac 上触发 SIGILL（exit code 132）。已关闭，预计修复已合入。

### 2. #82506 — Claude Max 会话额度被“无使用即消耗”（OPEN）
- 链接: https://github.com/anthropics/claude-code/issues/82506
- 评论: 17 | 👍: 7
- 关键信息: 用户反馈 Claude Max 订阅的会话限额在未实际使用的情况下被扣除，已通过 preflight checklist 排除重复报告，属于**高可信付费功能缺陷**，受关注度高，官方尚未给出结论。

### 3. #58750 — Cowork Desktop (macOS)：AskUserQuestion 卡片无法到达渲染进程（OPEN）
- 链接: https://github.com/anthropics/claude-code/issues/58750
- 评论: 11 | 👍: 5
- 关键信息: 黄色角标显示有 pending 请求但 UI 不出现，退出应用时该请求被静默解析为 "Dismissed"——用户交互在无感知时丢失，是典型的桌面端消息通道缺陷。

### 4. #21132 — 功能请求：让 Claude 能够自行清空上下文（CLOSED）
- 链接: https://github.com/anthropics/claude-code/issues/21132
- 评论: 10 | 👍: 15
- 关键信息: 虽然已关闭，但 15 个 👍 是本期最高赞需求。用户希望 Claude 在长会话中具备主动 `clear` 上下文的能力，而非依赖手动干预。属 agent 自主管理方向的早期呼声。

### 5. #61930 — iOS Code 标签页：语音听写后键盘遮挡发送按钮（CLOSED）
- 链接: https://github.com/anthropics/claude-code/issues/61930
- 评论: 8 | 👍: 5
- 关键信息: 远程控制 Claude Code 会话时，语音输入后软键盘无法收起，Send 按钮被完全遮挡，指令无法发送。iOS 端远程控制路径的可用性缺陷。

### 6. #68502 — HTTP 529 被错误渲染为 "Rate limited" 并硬失败（CLOSED）
- 链接: https://github.com/anthropics/claude-code/issues/68502
- 评论: 6
- 关键信息: 并行会话/子代理场景下，服务器过载（HTTP 529）被误报为限流，且**无退避重试、不写入错误日志**。并行执行的可靠性隐患，已关闭。

### 7. #68755 — Inline 渲染器破坏终端 scrollback（CLOSED）
- 链接: https://github.com/anthropics/claude-code/issues/68755
- 评论: 3 | 👍: 4
- 关键信息: Ghostty 终端下默认 inline 渲染器用交错覆盖写方式渲染，导致历史回滚内容损坏。影响 macOS + Ghostty 用户群体，已关闭。

### 8. #64036 — FleetView 按过时分类器将活跃 agent 归入 Completed（OPEN）
- 链接: https://github.com/anthropics/claude-code/issues/64036
- 评论: 3 | 👍: 1
- 关键信息: 后台 agent 列表的“工作/完成”分桶由**过时的文本分类器判定**驱动，而非实时会话状态。活跃任务被错误归入 Completed，影响多 agent 编排的可观测性。

### 9. #80131 — Fullscreen 渲染器在 iTerm2 启动时 SIGTTIN 挂起（OPEN）
- 链接: https://github.com/anthropics/claude-code/issues/80131
- 评论: 1 | 👍: 3
- 关键信息: `CLAUDE_CODE_NO_FLICKER=1` 下，TTY 前台进程组丢失导致 `zsh: suspended (tty input)`，鼠标追踪泄漏到 shell。iTerm2 用户受影响，Ghostty 正常——终端兼容性 bug。

### 10. #84212 — Skill 的 `args` 被替换进 SKILL.md 正文中的 `$0/$1`（OPEN）
- 链接: https://github.com/anthropics/claude-code/issues/84212
- 评论: 1（新提交）
- 关键信息: 调用 Skill 传 `args` 时，SKILL.md 中所有 `$0`、`$1`、`$2` 会被按空格拆分替换，**导致 shell 命令被静默破坏**。磁盘文件不变。这是新发现的模板变量替换越权问题，涉嫌注入类缺陷，值得关注。

---

## 重要 PR 进展（10 个）

### 1. #84138 — 修复 Cowork 中 Bun 运行时自签名证书错误（OPEN）
- 链接: https://github.com/anthropics/claude-code/pull/84138
- 作者: @botbikamordehai2-sketch | 更新: 2026-08-05
- 摘要: 针对

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-06

## 今日速览

今日共发布 1 个稳定版补丁与 4 个 `0.147.0-alpha` 迭代版本，重点修复了安全审查默认参数问题。社区方面，Windows 平台相关问题持续高发（WSL Git 误判、桌面卡顿、子代理兼容性），同时社区对侧聊持久化、按线程 Auto 模式等功能需求呼声较高。开源侧的 PR 更新集中于技能系统重构、MCP 握手超时防护与 Git 状态扫描合并等基础设施优化。

---

## 版本发布

### rust-v0.146.1
- **修复**：为 cyber-capable 模型应用更安全的自动审查默认值，并在终端界面中解释权限变更。[#37057](https://github.com/openai/codex/pull/37057)
- **完整变更**：https://github.com/openai/codex/compare/rust-v0.146.0...rust-v0.146.1

### rust-v0.147.0-alpha.x
- 发布 `0.147.0-alpha.6.5`、`0.147.0-alpha.10`、`0.147.0-alpha.11`、`0.147.0-alpha.12` 四个迭代版本，未附加详细说明（持续向 0.147 稳定版推进）。

---

## 社区热点 Issues（Top 10）

### 1. Windows/WSL 误判 Git 不可用
[#35119](https://github.com/openai/codex/issues/35119) — 16 评论 / 14 👍 / 状态：OPEN  
Windows App `26.721.3404` 将有效的 WSL 仓库误判为非 Git 仓库，并报告 “Git is unavailable”。这是 Windows + WSL 组合的高频回归问题，直接影响开发者在 WSL 侧的正常使用。

### 2. Windows 独立更新时 PowerShell 继承 PSModulePath
[#27117](https://github.com/openai/codex/issues/27117) — 12 评论 / 11 👍 / 状态：OPEN  
即使是 PowerShell 7 启动 Codex，更新逻辑仍会调用 `powershell.exe`，子进程继承 pwsh 的 `PSModulePath` 导致 `Get-FileHash` 失败。Windows 更新链路的不稳定对用户影响较大。

### 3. 大线程全量重放导致系统级卡顿
[#33786](https://github.com/openai/codex/issues/33786) — 11 评论 / 2 👍 / 状态：OPEN  
Windows 桌面版在完成大线程对话后，每隔几秒全量重放整个会话，造成系统级输入卡顿。Electron/Chromium 主进程持续高负载，属于性能类严重问题。

### 4. spawn_agent 拒绝 gpt-5.6-luna
[#34700](https://github.com/openai/codex/issues/34700) — 11 评论 / 30 👍 / 状态：OPEN  
当 `multi_agent_v2` 开启时，Codex App `26.715.9868.0` / CLI `0.145.0` 的 `spawn_agent` 不支持 `gpt-5.6-luna` 模型。目前该项目在热门 Issue 中高居点赞榜首，体现用户对多智能体 + 新模型组合的强烈需求。

### 5. 侧聊持久化
[#26227](https://github.com/openai/codex/issues/26227) — 9 评论 / 21 👍 / 状态：OPEN  
希望侧聊可以作为子线程挂载到主线程，避免会话/应用关闭后有用的侧聊上下文丢失。这是社区呼声最高的功能增强之一。

### 6. 桌面 App 文件引用行号跳转不可靠
[#28643](https://github.com/openai/codex/issues/28643) — 8 评论 / 7 👍 / 状态：OPEN  
点击文件引用（带行号）时经常无法跳转到目标行，反复点击也未必可复现。日常开发中文件引用是高频操作，此问题对体验影响明显。

### 7. 安全过滤误报
[#37161](https://github.com/openai/codex/issues/37161) — 4 评论 / 1 👍 / 状态：OPEN  
代码安全请求过滤对静态分析、模糊测试、漏洞检测等合法工程任务误报率过高。新 Issue，安全过滤的平衡问题引发关注。

### 8. Computer Use 在 Windows 上 EPERM 失败
[#37029](https://github.com/openai/codex/issues/37029) — 4 评论 / 1 👍 / 状态：OPEN  
Windows App `26.730.7989.0` 的 Computer Use 功能在应用选择前即因 `EPERM lstat` 报错。Computer Use 在 Windows 上的稳定性仍待改善。

### 9. macOS 屏幕录制流未释放
[#35659](https://github.com/openai/codex/issues/35659) — 3 评论 / 0 👍 / 状态：OPEN  
macOS 上 Computer Use 结束后面 Codex 仍保留 ScreenCaptureKit 流，以约 55–56 FPS 空转，导致 WindowServer 高 CPU/GPU 占用。

### 10. 移动端 Remote 缺少 SSH 项目
[#37142](https://github.com/openai/codex/issues/37142) — 2 评论 / 0 👍 / 状态：OPEN  
Android/iOS 端 Codex Remote 只显示直接会话，无法看到 Windows App 中活动的 SSH 后台项目。远程场景的可用性缺口显著。

---

## 重要 PR 进展（Top 10）

### 1. 绑定远程 MCP 握手 HTTP 请求
[#37168](https://github.com/openai/codex/pull/37168) — 已关闭  
流式 HTTP MCP 握手中，原始 HTTP 请求可能超时后仍继续运行，阻塞后续串行 executor。此 PR 为握手请求增加截止时间追踪，防止死锁。

### 2. 合并并发 Git status 扫描
[#37151](https://github.com/openai/codex/pull/37151) — 已关闭  
对相同仓库的并发 `git status --porcelain` 请求共享同一个正在执行的扫描，避免重复进程开销；不同仓库保持独立。

### 3. 本地强制执行托管认证要求
[#37132](https://github.com/openai/codex/pull/37132) — 已关闭  
在 bootstrap 阶段、云端认证策略拉取前，通过本地 `requirements.toml` 应用 allowlist 限制，防止未授权凭据在受限环境中被使用。

### 4. Windows 路径 URI 比较改为 ASCII 大小写不敏感
[#37129](https://github.com/openai/codex/pull/37129) — 已关闭  
修复 Windows 下 `PathUri` 的相等性和哈希判断：对推断的 Windows 盘符和 UNC 路径采用 ASCII 大小写不敏感比较，同时保持 POSIX 行为不变。

### 5. 按模型能力门控 Apps 使用说明
[#37145](https://github.com/openai/codex/pull/37145) — 已关闭  
在模型元数据中新增 `include_apps_usage_instructions`（默认 true，保持兼容），当模型不支持 Apps 时不再生成相关使用指引。

### 6. 技能选择逻辑移入 skills crate
[#37177](https://github.com/openai/codex/pull/37177) — 已关闭  
新增 `ExplicitSkillLookup`，将显式提及的技能选择与核心技能加载模型解耦，并导出 `collect_explicit_skill_mentions` 公共接口。

### 7. 集中技能调用辅助函数
[#37174](https://github.com/openai/codex/pull/37174) — 已关闭  
将工具提及解析、技能名称统计、隐式调用检测逻辑统一收归 `codex-skills` crate 公共 API，并解耦隐式调用检测与 `SkillLoadOutcome`。

### 8. 增加 textarea 光标和渲染视口保护
[#37166](https://github.com/openai/codex/pull/37166) — 已关闭  
修复逻辑行恰好填满 textarea 宽度时，光标和续行渲染溢出视口的问题；同时对普通、掩码、占位文本等内容进行裁剪。

### 9. 强化 TUI 导航命名会话查找
[#37157](https://github.com/openai/codex/pull/37157) — 已关闭  
在 `resume` 和 `archive` 命令之间共享精确名称候选查找逻辑，偏好有效 SQLite 名称，并可回退恢复遗留索引名称，同时验证 rollout 身份。

### 10. 分页历史迁移
[#37175](https://github.com/openai/codex/pull/37175) — 已关闭  
为 `LocalThreadStore` 新增 `migrate_rollouts`，将遗留 JSONL 记录规范化迁移到分页历史格式（支持 dry-run、可选线程、吞吐限制与结果记录）。

---

## 功能需求趋势

从近期 Issues 提炼出以下社区最关注的方向：

1. **会话持久化与分支管理** — 侧聊持久化（[#26227](https://github.com/openai/codex/issues/26227)）、从消息分支新对话（[#13087](https://github.com/openai/codex/issues/13087)）均体现用户对长会话组织能力的迫切需求。

2. **模型/速度使用的灵活控制** — 用户期望按线程精细化地指定模型和推理卡度（[#34278](https://github.com/openai/codex/issues/34278)），或在计划生成后、实施开始前切换模型（[#26996](https://github.com/openai/codex/issues/26996)）。

3. **Windows 平台的稳定性修复** — 当前 Issues 中 Windows 相关占比极高，包括 WSL 仓库检测（[#35119](https://github.com/openai/codex/issues/35119)）、更新链路（[#27117](https://github.com/openai/codex/issues/27117)）、卡顿（[#33786](https://github.com/openai/codex/issues/33786)）等，已成为影响最大面用户的问题之一。

4. **Computer Use 的跨平台可靠性** — 多个 Issue 暴露了 macOS 和 Windows 上计算机使用功能的资源泄漏、权限失败与超时问题（[#37029](https://github.com/openai/codex/issues/37029)、[#35659](https://github.com/openai/codex/issues/35659)、[#34419](https://github.com/openai/codex/issues/34419)）。

5. **远程/移动端无缝衔接** — 移动端 Remote 只显示直接会话、遗漏 SSH 项目（[#37142](https://github.com/openai/codex/issues/37142)），以及 Android 语音输入上下文缺失（[#37173](https://github.com/openai/codex/issues/37173)），显示远程工作流仍在早期阶段。

---

## 开发者关注点

- **Windows 生态体验是当前最大痛点**：从 WSL 仓库误判、pwsh 更新失败到 Electron 主进程卡顿和系统级输入延迟，Windows 相关 bug 数量多、影响面大、用户反馈积极，是优先修复的关键区域。

- **新模型与多智能体的兼容性滞后**：`gpt-5.6-luna` 在 `spawn_agent`（[#34700](https://github.com/openai/codex/issues/34700)）和工具路由（[#37113](https://github.com/openai/codex/issues/37113)）中的异常让用户感到新模型未能与现有功能充分对齐。

- **性能资源管理问题反复出现**：除 Windows 卡顿外，macOS 上 ScreenCaptureKit 流未释放（[#35659](https://github.com/openai/codex/issues/35659)）和空转 CPU 循环（[#32516](https://github.com/openai/codex/issues/32516)）表明桌面端资源回收存在系统性问题。

- **安全审查误报开始引发社区讨论**：[#37161](https://github.com/openai/codex/issues/37161) 指出对静态分析、模糊测试等正常安全工程任务的误拦截，开发者期望安全机制更加精准、更好地区分“有防护的测试”与“恶意利用”。

- **认证与连接器的体验断层**：Notion 连接器重连后仍返回 401（[#24848](https://github.com/openai/codex/issues/24848)），UI 对各组件状态展示不明确，影响第三方工具链的正常使用。

---

*数据截至 2026-08-06 上午，来源：[github.com/openai/codex](https://github.com/openai/codex)。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-08-06）

> 数据来源：github.com/MoonshotAI/kimi-cli
> 说明：过去 24 小时无版本发布、Issue 更新 5 条、PR 更新 2 条，以下全量呈现。

## 今日速览

今日无新版本发布。社区聚焦三大话题：**跨会话记忆系统**的长期需求仍在讨论（#1283，18 条评论）；**高上下文填充下的代理可靠性**问题被明确提出（#2586，约 500K token 临界点）；**StrReplaceFile 损坏非 UTF-8 字节**的 bug 引发对文件安全性的关注（#2591）。同时，两个新 PR 分别改善错误提示和补充语音 ACP 客户端文档。

## 社区热点 Issues（共 5 条）

### 1. 内存系统：跨会话持久上下文（#1283）
**长期需求，讨论最热**

- 作者：@CatKang | 创建：2026-02-27 | 更新：2026-08-05 | 评论：18 | 状态：OPEN
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1283
- **摘要**：实现一套综合记忆系统，让 Kimi Code CLI 跨会话记住项目模式、用户偏好与有用上下文，包括 AI 自动管理与用户手动定义两类记忆。
- **社区反应**：6 个月来持续有 18 条评论，说明跨会话上下文是高频且未满足的需求。0 个 👍 可能是入口较深的展示问题，但评论区活跃度证明其价值。

### 2. 高上下文填充时代理可靠性下降（#2586）
**严重的长会话稳定性问题，已关闭**

- 作者：@GrokBuildMJW | 创建：2026-08-05 | 更新：2026-08-05 | 评论：1 | 状态：CLOSED
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2586
- **摘要**：在约 500K token（用户测量值，非官方限制）的上下文填充率下，多步代码变更任务出现**重复动作循环、无升级机制、指令漂移**，可靠性明显下降。
- **为什么重要**：长会话是 agentic 编程的典型场景，此现象直接影响复杂任务完成率。

### 3. StrReplaceFile 损坏编辑区域外的不可解码字节（#2591）
**高风险文件完整性 bug**

- 作者：@shoemoney | 创建：2026-08-05 | 更新：2026-08-05 | 评论：0 | 状态：OPEN
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2591
- **摘要**：StrReplaceFile 使用 `errors="replace"` 整文件解码后写回，导致文件**任何位置**的非 UTF-8 字节被替换成 U+FFFD，可能破坏二进制或混合编码文件。
- **为什么重要**：自动编辑工具必须保证"只改目标区域"，此 bug 可能静默损坏用户数据，优先级应较高。

### 4. 模型未声明 capabilities 时与图片返回 MCP 工具冲突（#2588）
**错误提示不友好且副作用已发生**

- 作者：@tic-top | 创建：2026-08-05 | 更新：2026-08-05 | 评论：0 | 状态：OPEN
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2588
- **摘要**：`config.toml` 中未声明 `capabilities` 的模型，在 MCP 工具返回图片时会中止运行，但此时工具副作用已产生；报错信息未给出修复建议。
- **为什么重要**：既有功能校验缺失，也有错误提示设计问题，会打断流程且误导开发者。

### 5. 正常推进会话时异常退出（#2587）
**Windows 平台稳定性问题**

- 作者：@Sdongmaker | 创建：2026-08-05 | 更新：2026-08-05 | 评论：0 | 状态：OPEN
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2587
- **摘要**：Kimi Code v0.29.2、Windows NT 10.0.26200.0 x64、K3 high 模型、`/login` 模式下，正常推进会话时 CLI 异常退出，附带截图但未提供完整日志。
- **为什么重要**：正常使用中崩溃属于阻断性问题，且涉及 K3 新模型 + Windows 环境，需要官方快速定位。

## 重要 PR 进展（共 2 条）

### 1. fix(soul): 在

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-06

## 今日速览

OpenCode 发布 v1.18.14，优化 xAI 无头环境登录流程并增强错误重试机制；社区方面，VS Code 官方扩展（#11176）以 134 👍 高居需求榜首，Pay Go 加密货币支付（#23153）持续升温。此外，大量重构 PR（清理遗留资源、数据迁移 v1→v2）表明项目正为下一代架构（V2）加速准备。

## 版本发布

**v1.18.14**
- **改进**：简化 xAI 登录为单一 device-code 流程，更好地支持无头（headless）和远程环境。
- **Bug 修复**：保留结构化流式中间错误，兼容提供商可重试失败响应；增加对瞬时提供商和网络错误的重试。

## 社区热点 Issues

**1. [FEATURE] 官方 OpenCode VS Code 扩展** · #11176
作者 @c2b247 | 评论 27 | 👍 134
社区呼声最高的功能请求，希望 OpenCode 以原生 VS Code 扩展形式运行，与 IDE 工作流深度集成。
🔗 https://github.com/anomalyco/opencode/issues/11176

**2. DeepSeek V4 Flash 突然要求启用"中国托管模型"** · #39845
作者 @capi | 评论 17 | 👍 22
OpenCode Go 订阅用户会话中途被中断，提示模型仅限中国托管需手动开启，引发对区域限制策略的讨论。
🔗 https://github.com/anomalyco/opencode/issues/39845

**3. [FEATURE] 使用加密货币支付 OpenCode Go** · #23153
作者 @suse-coder | 评论 16 | 👍 36
开发者希望增加加密货币支付选项，反映社区对支付方式多样化的强烈需求。
🔗 https://github.com/anomalyco/opencode/issues/23153

**4. [FEATURE] 跨项目会话列表/选择器** · #31932
作者 @mskadu | 评论 14 | 👍 6
当前 /sessions 命令仅限当前项目，多仓库开发者需要全局会话视图。
🔗 https://github.com/anomalyco/opencode/issues/31932

**5. [FEATURE] SKILL.md frontmatter 支持 disable-model-invocation** · #34498
作者 @yooo1999 | 评论 13 | 👍 49
要求与 Claude Code 对齐，允许在技能中禁用模型调用，收到大量正面反馈。
🔗 https://github.com/anomalyco/opencode/issues/34498

**6. 旧款 Intel Mac 崩溃（非法指令）** · #24876 / #29039
作者 @marcioganzer 等 | 评论 7+7
两个相关 issue：opencode 二进制在旧 Intel Mac 上因 AVX2/FMA 指令集不兼容而崩溃，影响 Ivy Bridge 等老 CPU 用户。
🔗 https://github.com/anomalyco/opencode/issues/24876
🔗 https://github.com/anomalyco/opencode/issues/29039

**7. [FEATURE] "自动模式" LLM 模型分类器自动审批权限** · #37564
作者 @dylbarne | 评论 6 | 👍 11
提出类似 Cursor 的自动模式——用 LLM 分类器判断哪些权限操作可自动批准，提升代理式编程效率。
🔗 https://github.com/anomalyco/opencode/issues/37564

**8. [FEATURE] 技能调用在提示词中间位置自动补全** · #40689
作者 @ThunderRonin | 创建 2026-08-05 | 评论 3
技能触发目前仅支持行首，用户希望在中段也能通过 tab 补全。
🔗 https://github.com/anomalyco/opencode/issues/40689

**9. PyCharm 2026.2 AI Assistant 启动时产生 15-22 个 opencode.exe 进程** · #40696
作者 @opcwj | 创建 2026-08-05 | 评论 3
IDE 初始化时批量创建会话，导致内存耗尽崩溃，是 ACP 集成的严重稳定性 bug。
🔗 https://github.com/anomalyco/opencode/issues/40696

**10. [FEATURE] OpenCode Desktop 远程 SSH 支持** · #33273
作者 @andrei-brz | 评论 3 | 👍 4
Remote SSH 支持被认为是桌面端远程开发的关键能力。
🔗 https://github.com/anomalyco/opencode/issues/33273

## 重要 PR 进展

**1. fix(mcp): 跨进程 OAuth 刷新竞态** · #40768
修复多个进程共享 MCP 凭据刷新导致 token 旋转互相覆盖的问题，解决 #34520。
🔗 https://github.com/anomalyco/opencode/pull/40768

**2. feat(core): v1 数据迁移至 v2** · #40723
实现 REST 触发的 V1 会话历史迁移，导入 V2 数据和 legacy JSON 凭据，并更新 TUI 迁移流程。
🔗 https://github.com/anomalyco/opencode/pull/40723

**3. refactor(core): 去重 Copilot 端点路由** · #40765
复用 @opencode-ai/ai 的共享 Copilot 路由逻辑，删除 Core 中重复实现。
🔗 https://github.com/anomalyco/opencode/pull/40765

**4. refactor: 移除孤立 sqlite 包** · #40766
清理无引用、无消费者的 @opencode-ai/effect-sqlite-node 工作区包，减小仓库和锁文件体积。
🔗 https://github.com/anomalyco/opencode/pull/40766

**5. fix(tui): 提前加载侧边栏项目名** · #40763
优化 TUI 连接后持久化会话标签的加载时序，消除 300ms 空白等待。
🔗 https://github.com/anomalyco/opencode/pull/40763

**6. feat(app): 可选垂直标签栏** · #38308
新增可选的垂直 tab 布局（设置中切换），支持拖拽调宽和折叠，默认仍为水平布局。
🔗 https://github.com/anomalyco/opencode/pull/38308

**7. refactor(plugin): 拆分会话 HTTP 钩子** · #40724
将会话 HTTP 中间件改为独立的 http.request / http.response 钩子，扩展插件能力。
🔗 https://github.com/anomalyco/opencode/pull/40724

**8. fix(core): 连接自定义提供商** · #40761
使自定义提供商即使未声明环境凭据也能作为集成出现在 /connect 中，并支持手动 API key 认证。
🔗 https://github.com/anomalyco/opencode/pull/40761

**9. feat(acp): 从 todowrite 工具调用发送计划会话更新** · #31834
为 ACP 集成补齐计划渲染事件，使 TodoWrite 能触发 UI 计划展示。
🔗 https://github.com/anomalyco/opencode/pull/31834

**10. fix(core): 同一仓库多个克隆视为同一项目** · #35311
修复同一仓库不同克隆被识别为不同项目的问题，关闭 14 个关联 issue。
🔗 https://github.com/anomalyco/opencode/pull/35311

## 功能需求趋势

- **IDE 集成深化**：VS Code 官方扩展（#11176）居首，加上 PyCharm ACP 问题（#40696），显示 IDE 工作流是核心场景。
- **国际化与合规**：瑞典语翻译贡献（#40716）、DeepSeek 地区限制（#39845）引发关注，全球化和区域策略需兼顾。
- **TUI/UX 增强**：跨项目会话选择（#31932）、提示词中间位置的技能/命令补全（#40689、#40719）表明用户界面的敏捷性越来越重要。
- **多代理可视化**：多代理并行工作流的 UI/UX 可视化（#40564）正在成为新的功能焦点。
- **性能与兼容性**：Intel Mac 崩溃（#24876/#29039）、离线环境 ripgrep 内置（#31734）等基础设施问题仍被高频提及。

## 开发者关注点

- **老硬件兼容性**：Intel Mac（Ivy Bridge 及更早）的 AVX2 依赖导致二进制无法启动——这是发布流程中需要引入分级构建（baseline vs modern）的明确信号。
- **全局规则可靠性**：全局 ~/.config/opencode/AGENTS.md 规则被跨会话遗忘（#40348），影响用户对"规则持久性"的信任。
- **进程资源管理**：PyCharm AI Assistant 启动时生成大量 opencode.exe 进程导致内存耗尽（#40696），急需对 ACP 会话增加并发限制。
- **远程开发能力**：Remote SSH（#33273）与远程服务器路径同步问题（#35240），显示团队协作场景下的远程工作流仍不完善。
- **会话状态管理**：会话没有状态标签（Todo/Done/Backlog），任务进度不更新（#40688），用户需要一个更成熟的会话组织模型。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-06

## 今日速览

今日最值得关注的是 **v0.21.6 正式版发布**，带来了 macOS WebShell 上的实验性 Live Voice 实时语音交互能力；同时 **Qwen Code Desktop v0.1.0** 也已完成首批发布。社区侧，两个安全相关 issue 需要重视：一是 CLI 警告清理逻辑可能泄漏含 `@` 的密码（#8136），二是只读 shell 分类器存在命令注入绕过漏洞（#8582，P1）；此外 CI `/review` 流程的高频超时问题（#8597）以及 tmux 下的 TUI 闪烁问题也引发了较多用户讨论。

---

## 版本发布

### v0.21.6（正式版）
- **实验性功能**：WebShell 在 macOS 上新增原生 Live Voice 支持，可通过全局快捷键进行实时音频交互（[#7859](https://github.com/QwenLM/qwen-code/pull/7859)）
- Web Shell 在后台任务活跃期间保持对话轮次展开，改善流式输出体验
- 链接：[v0.21.6 Release](https://github.com/QwenLM/qwen-code/releases)

### v0.21.6-preview.0
- 浏览器扩展新增 alpha 就绪诊断（browser-ext alpha readiness diagnostics）
- 文档补充 headless Goal 工作流说明
- 链接：[v0.21.6-preview.0 Release](https://github.com/QwenLM/qwen-code/releases)

### v0.21.5-nightly.20260805.32e274157
- 与 preview.0 同步包含浏览器扩展诊断与 headless Goal 文档更新
- 链接：[nightly Release](https://github.com/QwenLM/qwen-code/releases)

### desktop-v0.1.0（桌面版首发里程碑）
- CI 修复：qwen-triage container job 增加默认 bash shell
- Web Shell 多个稳定性修复
- 链接：[desktop-v0.1.0 Release](https://github.com/QwenLM/qwen-code/releases)

---

## 社区热点 Issues（10 个）

### 1. 安全：只读 shell 分类器可被命令替换绕过 — [P1]
[#8582](https://github.com/QwenLM/qwen-code/issues/8582)
AST 分类器与运行时替换检测存在盲区：通过行继续符 `\` 或 `${var@P}` 等技巧可隐藏命令替换，导致只读 shell 自动放行任意代码执行。这是当前最严重的安全问题之一，建议尽快跟进。

### 2. 安全：Provider 警告清理逻辑泄漏密码（含 `@` 时）
[#8136](https://github.com/QwenLM/qwen-code/issues/8136)
`sanitizeProviderWarning` 在截取 userinfo 时对端口与 `@` 的处理有缺陷，可能将完整的密码随 `/status` 负载输出。涉及 CLI 安全边界，8 条评论，社区讨论活跃。

### 3. CI：/review 反向审计启动作业静默挂起，直到超时被杀 — [P1]
[#8597](https://github.com/QwenLM/qwen-code/issues/8597)
8 月 4 日 12 次超时、8 月 5 日 14:50 前再添 9 次，多数占满 360 分钟预算。分析显示 5 次中有 4 次是同一失败模式，CI 基础设施稳定性告急。

### 4. CLI：`qwen mcp list` 在无响应的 SSE 服务器上无限挂起
[#8550](https://github.com/QwenLM/qwen-code/issues/8550)
SSE transport 的 MCP server 若不发送 `endpoint` 事件，`qwen mcp list` 将永久阻塞，无超时机制。影响 MCP 配置排障效率，已标记 `ready-for-agent`。

### 5. VSCode 插件：Edit/Write 文件链接错误解析到工作区根目录
[#8606](https://github.com/QwenLM/qwen-code/issues/8606)
模型使用 `edit_file`/`write_file` 后，结果中的文件链接一律解析为 `<workspace-root>/<basename>`，任何嵌套文件都会报"file not found"。严重影响 VSCode 用户日常使用。

### 6. 桌面版：复制响应按钮无效（Windows）
[#8538](https://github.com/QwenLM/qwen-code/issues/8538)
Windows 10 上 Qwen Code Desktop 0.0.5 的 copy-response 按钮点击无任何效果，已排除重启、重装等常规手段。桌面端基础功能尚不完善。

### 7. Web Shell：带 bearer token 时刷新会话深链返回 401
[#8560](https://github.com/QwenLM/qwen-code/issues/8560)
`qwen serve --token <secret>` 启动后，会话进行中浏览器 URL 变为 `/session/<id>`，刷新该页面会因认证失效返回 401，需要重新登录。属于认证流程缺陷。

### 8. TUI：tmux < 3.5 中持续闪烁
[#8580](https://github.com/QwenLM/qwen-code/issues/8580)
tmux 3.4 环境下 TUI 每秒 2–3 次全屏清空重绘，根因是 Ink renderer 的 overflow 帧行为与 DEC 2026 查询未配合。另一条 [issue #8562](https://github.com/QwenLM/qwen-code/issues/8562) 也报告了类似 tmux 环境下的闪屏问题，社区反馈较多。

### 9. 桌面端架构路线：基于 Web Shell 构建低维护成本桌面应用
[#8092](https://github.com/QwenLM/qwen-code/issues/8092)
社区建议复用 Web Shell 作为桌面应用主体，而非维护独立的 UI 实现。与今日发布的 desktop-v0.1.0 方向一致，且后续 issue [#8596](https://github.com/QwenLM/qwen-code/issues/8596) 进一步提议废弃 Electron 版、将 Tauri shell 更名为 desktop。

### 10. 功能提议：本地控制模式（QR 码配对手机访问）
[#8595](https://github.com/QwenLM/qwen-code/issues/8595)
希望通过桌面应用展示 QR 码，扫码后手机即可接管本地 Qwen Code 会话，零手动配置。反映了开发者对移动端远控的明确需求。

---

## 重要 PR 进展（10 个）

### 1. feat(web-shell): native Live Voice（已合并）
[#7859](https://github.com/QwenLM/qwen-code/pull/7859)
为 WebShell on macOS 带来实验性 Live Voice 支持，含 onboarding 流程与 Codex-parity 实时架构。默认关闭，不影响 CLI/TUI 及其他平台，已随 v0.21.6 发布。

### 2. fix(core): 流式响应总生命周期上限 + 精简 review fan-out 启动
[#8602](https://github.com/QwenLM/qwen-code/pull/8602)
修复 #8597 的静默挂起问题：现有流式 watchdog 仅在 chunk 间无数据时触发，且每收一个 chunk 就重置；本 PR 增加请求级总时长上限，并同步精简 CI review 的并行启动逻辑。

### 3. fix(autofix): review CLI bundle 附带 core 构建产物
[#8612](https://github.com/QwenLM/qwen-code/pull/8612)
将 core 包的构建输出纳入 CLI bundle 产物，并在各分段恢复后校验入口存在性，避免 review 阶段缺依赖。

### 4. fix(review): 停止反向审计循环，留出报告时间
[#8468](https://github.com/QwenLM/qwen-code/pull/8468)
针对 reverse-audit 迭代循环频繁跑满 5 轮上限、耗尽超时预算的问题，调整流程以保留结果上报空间。

### 5. ci(autofix): 重型 autofix 作业迁移到 ECS 自托管池
[#8603](https://github.com/QwenLM/qwen-code/pull/8603)
将 issue-fixing agent、review CLI bundle 构建、review-feedback address agent 三道重型作业从 GitHub-hosted runner 迁移至持久化 ECS 池，降低 CI 波动。

### 6. feat(core): 长时 Goal 证据 checkpoint
[#8465](https://github.com/QwenLM/qwen-code/pull/8465)
在证据目录达到硬限制前，运行时暂停自动续跑，由独立的无工具验证器将累积证据压缩为有界摘要，避免长时任务证据超限。

### 7. feat(cli): VP 模式恢复 Ctrl+click 超链接与右键菜单
[#8439](https://github.com/QwenLM/qwen-code/pull/8439)
Virtual Viewport 模式启用 SGR 鼠标追踪后，终端原生能力（点开链接、右键菜单）被吞掉；本 PR 在保持状态跟踪的同时修复此回归。

### 8. feat: 支持从任意会话消息 fork
[#8274](https://github.com/QwenLM/qwen-code/pull/8274)
此前分支只能基于最新活跃会话状态，无法准确定位到较早的 Assistant 响应；本 PR 将 fork 点扩展到任意可见消息，需处理工具调用、取消、元数据与并发记录等边界。

### 9. feat(cli): 附件音频桥
[#8332](https://github.com/QwenLM/qwen-code/pull/8332)
主模型不支持音频时，通过配置的 batch voice model 转写用户

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*