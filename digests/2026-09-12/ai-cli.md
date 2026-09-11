# AI CLI 工具社区动态日报 2026-09-12

> 生成时间: 2026-09-11 22:35 UTC | 覆盖工具: 7 个

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
**日期：2026-09-12** ｜ 数据来源：github.com/anthropics/claude-code

---

## 一、今日速览

- **服务端回归事故**成为今日最高优先级信号：Cowork macOS 沙箱 VM 自 2026-09-10 23:15 UTC 起网络路由全失效、云出口代理对所有域名返回 403（#93507），是唯一带 `regression` 标签的新 Issue。
- **v2.1.269 发布**，带来 `claude plugin eval`（插件评测套件 + JSON/HTML 报告）与 `/output-style [name]` 输出风格切换，插件生态工具链进一步成型。
- **Fable 5 安全护栏误报**集中爆发：过去 24 小时内至少 7 条相关 Issue 被批量 `stale` 关闭，社区对"广义护栏拦截正常编码任务"的不满在累积。

---

## 二、版本发布

### v2.1.269

| 更新项 | 说明 |
|---|---|
| `claude plugin eval` | 对 Claude Code 运行插件自带的 eval 套件，输出**可复现的评分结果**（JSON + HTML 报告），详见 `claude plugin eval --help` |
| `/output-style [name]` | 列出并切换输出风格，支持 **Remote Control 远程控制**、云环境及终端场景 |

**解读**：`plugin eval` 是本版本最有分量的能力——它把插件质量从"能不能用"推进到"可量化、可回归验证"，意味着 Anthropic 正在把 Claude Code 当作一个**可测试的插件运行时平台**来建设。`/output-style` 则是体验层的一致性问题（远程/云/本地统一风格）。

---

## 三、社区热点 Issues（精选 10 条）

> 过去 24 小时共 50 条 Issue 有更新，以下为筛选出的最值得关注项。

### 1. #42776 ｜桌面端 Windows 无法重启：孤儿进程文件锁 🥇
- **状态**：OPEN（标签 `invalid`）｜**177 评论 · 88 👍**
- **看点**：全站互动量断层第一，但被标为 `invalid`。这种"高热度 + 官方判定无效"的组合通常意味着**用户环境问题与产品缺陷边界不清**，或标签判定存在争议。值得持续跟踪官方是否重新定性。
- 🔗 https://github.com/anthropics/claude-code/issues/42776

### 2. #93507 ｜Cowork macOS 沙箱完全无网络出口（回归）🔥
- **状态**：OPEN ｜9 评论 · 1 👍｜标签：`regression` `area:sandbox` `area:networking`
- **看点**：**今日最需立即响应的问题**。VM 仅剩 loopback，即使配置"Allow network egress: All domains"，云出口代理仍对全部域名返回 403。明确锁定为 2026-09-10 23:15 UTC 后的回归，时间点精确、可复现性强。
- 🔗 https://github.com/anthropics/claude-code/issues/93507

### 3. #25947 ｜项目记忆文件应存放在项目本地 `.claude/` 📁
- **状态**：OPEN ｜9 评论 · **39 👍**
- **看点**：跨半年仍在活跃的长线需求。当前 `~/.claude/projects/<encoded-path>/memory/MEMORY.md` 的全局存储方式，导致记忆无法随仓库版本化、无法团队共享。这是**呼声最高、争议最小**的功能请求之一。
- 🔗 https://github.com/anthropics/claude-code/issues/25947

### 4. #84918 ｜会话历史与记忆完全绑定绝对路径，仓库迁移即断档
- **状态**：CLOSED（`stale`）｜4 评论
- **看点**：与 #25947 同源但视角互补——**目录重命名/移动后上下文全失**。两者合并看，社区诉求清晰：会话与记忆需要稳定、可迁移的标识符，而非脆弱的绝对路径。
- 🔗 https://github.com/anthropics/claude-code/issues/84918

### 5. #78431 ｜Agent 未经询问把真实邮箱写入 User-Agent
- **状态**：CLOSED（`stale`）｜7 评论 · 4 👍｜标签：`area:security`
- **看点**：典型的**隐私外泄类**问题，且标题情绪化反映用户强烈不满。尽管已 stale 关闭，但"Agent 自主行为缺乏边界"仍是最敏感的话题类别。
- 🔗 https://github.com/anthropics/claude-code/issues/78431

### 6. #78834 ｜内置 ugrep 在特定正则下分配 4–17 GB 内存 💥
- **状态**：CLOSED（`stale`）｜5 评论｜标签：`perf:memory`
- **看点**：**搜索 64 KB 文件却吃掉数 GB 内存**，当模式含尾部 `.{N}` 有界重复时以 ~230 MB/s 稳定增长。报告含两组实测数据，工程质量很高，却因 stale 而关闭，令人遗憾。
- 🔗 https://github.com/anthropics/claude-code/issues/78834

### 7. #86444 ｜桌面端预览 localhost 卡死 + 卸载重装清空全部会话记录
- **状态**：CLOSED（`stale`）｜4 评论｜标签：`area:desktop` `platform:windows`
- **看点**：叠加两个严重问题——**UI 主线程挂起**与**静默数据丢失**。卸载重装抹掉 transcript 属于高危行为，任何"重装试试"的支持建议都会导致用户永久丢数据。
- 🔗 https://github.com/anthropics/claude-code/issues/86444

### 8. #77310 ｜无上限的每小时 PR 自检任务耗尽用量额度
- **状态**：CLOSED ｜3 评论｜标签：`area:cost` `area:cowork`
- **看点**：harness 的 GitHub 集成系统提示会指示会话订阅 webhook **并**自行每小时定时"check-in"，且每次触发都重新排期——**无循环上限、无成本上限**，4 天耗尽整个会话额度。这是 Agent 自主调度的成本治理缺失问题。
- 🔗 https://github.com/anthropics/claude-code/issues/77310

### 9. #72714 ｜`/worktree` 静默污染主仓库 `.git/config`
- **状态**：CLOSED（`stale`）｜3 评论｜标签：`area:tools`
- **看点**：`/worktree` 会把 `core.hooksPath` 写进**主仓库共享的 `.git/config`**，从而永久禁用全局 git hooks。属于"工具副作用超出作用域"的典型，对 CI/团队工作流影响深远。
- 🔗 https://github.com/anthropics/claude-code/issues/72714

### 10. #93707 ｜远程 SSH 连接失败：TCC 权限剥离导致无本地网络权限
- **状态**：OPEN（新）｜2 评论｜标签：`area:networking` `area:desktop` `platform:macos`
- **看点**：macOS 26 上子进程被 TCC 剥夺 Local Network 权限，导致访问 `192.168.x.x` 报 "No route to host"，而同机 Terminal 下手动 ssh 正常。**平台权限模型与子进程架构的冲突**，是 macOS 新系统下的结构性难题。
- 🔗 https://github.com/anthropics/claude-code/issues/93707

### 补充观察：Fable 5 安全护栏误报集群
#86241、#73870、#86602、#86687、#86680、#86652、#86673 等至少 7 条 Issue 在 24 小时内被批量 `stale` 关闭，共同指向同一问题：**广义安全护栏误伤正常任务（UI 重构、勒索软件分析、issue 管理、flutter 测试）**，并强制降级到 Opus 4.8。另有 #86673 指出安全分类器不可用时**Bash/Skill/Agent/MCP 工具全部被阻断，且无 MCP 绕过路径**——这是可用性层面的硬阻塞，值得官方给出统一的处置说明。

---

## 四、重要 PR 进展

⚠️ **数据说明**：本次采集窗口内**仅 1 条 PR**（且已 CLOSED），无法凑齐 10 条。为保持报告真实性，仅如实呈现该条，不做填充。

### #42205 ｜fix(hookify): 规范化 tool matcher 解析
- **状态**：CLOSED ｜作者 @Balajitechlabs
- **内容**：
  - 修复 hookify 工具匹配器解析：含空格分隔符的 matcher 字符串（如 `Edit or Write`）此前因拆分后未 trim 而匹配失败
  - 变更：求值前先 trim matcher；对每个 OR 段做规范化处理
- **意义**：hooks 是 Claude Code 自动化能力的核心扩展点，matcher 解析错误会导致 hook **静默不触发**——这类"无声失败"最难排查。
- 🔗 https://github.com/anthropics/claude-code/pull/42205

**待观察**：PR 数量极少，可能意味着官方对社区 PR 的接受度有限，或该仓库主要作为 Issue 跟踪用途（Contributions 通过其他渠道流转）。

---

## 五、功能需求趋势

从全部 Issues 中提炼出六条主线：

| 方向 | 代表 Issue | 社区诉求 |
|---|---|---|
| **记忆/会话的本地化与可移植性** | #25947、#84918 | 从全局绝对路径迁至项目内 `.claude/`，支持仓库版本化与目录迁移 |
| **网络、沙箱与代理可靠性** | #93507、#85979、#86023、#86349 | 沙箱网络路由、ECONNRESET、MCP 连接超时、自定义 CA 合并 |
| **Agent 成本与自主行为边界** | #77310、#86677 | 定时自检无成本上限、用量提示与实际额度不一致 |
| **安全护栏精度** | #86241 等 7 条 | 减少误报、保留降级路径、分类器不可用时不阻断工具调用 |
| **隐私与数据安全** | #78431、#86444、#86480 | 隐式上报（User-Agent）、重装丢 transcript、Bash 工具误删项目 |
| **IDE / 多端集成一致性** | #86686、#86621、#79515、#86646 | Android 远程连接强制覆盖模型选择、VS Code / IntelliJ / Desktop 行为差异 |

另有两类值得注意的小众信号：**输出语言/方言不稳定**（#86436 葡语、#86656 阿根廷西语，即便 CLAUDE.md 强制指定也无法遵守），以及 **worktree 与 Git hooks 的作用域污染**（#72714、#79515）。

---

## 六、开发者关注点

1. **`stale` 自动关闭正在掩盖真实缺陷** 🔴
   今日 30 条高互动 Issue 中，**超过 20 条被标记 `stale` 关闭**，其中包含含实测数据的高质量内存缺陷报告（#78834）、隐私泄漏（#78431）、数据丢失（#86444）。这会造成两个后果：一是开发者重复提交，二是社区信任流失。**建议官方复核 stale 策略的适用边界**。

2. **回归问题需要更快的响应通道**
   #93507 这类带精确时间戳的回归报告，说明用户已在自发做二分定位。缺少面向 `regression` 标签的加速处理机制，会让事故窗口被拉长。

3. **安全 ≠ 可用**
   安全分类器不可用时直接阻断全部工具调用（#86673），以及广义护栏对正常任务的误伤，共同指向一个设计原则问题：**降级路径必须存在**。开发者可以接受"被拦截"，但不能接受"无路可走"。

4. **跨平台行为一致性欠佳**
   Windows（#42776、#86444、#85979）、macOS（#93707、#80291）、Android（#86686）、WSL2（#78834）各自暴露平台特异性缺陷，macOS 的 TCC 权限模型尤其容易产生"终端可用、App 不可用"的割裂体验。

5. **Agent 自主度的成本与权限治理仍是空白**
   #77310 的自调度循环与 #78431 的隐式信息上报，本质是同一个问题：**Agent 代表用户自主行动时，缺少可配置的边界与预算**。

---

*报告基于 GitHub 公开数据生成；PR 数据覆盖不足，相关章节已标注。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 · 2026-09-12

数据来源：[github.com/openai/codex](https://github.com/openai/codex)

---

## 一、今日速览

过去 24 小时，Codex 的 `rust-v0.155.0-alpha` 线高频推送了 5 个构建，同时语音会话、worktrees 等此前实验性能力通过 PR 转为默认开启，0.155 主线明显在收拢能力面。社区侧热度仍集中在**资源泄漏与 Windows 桌面稳定性**：MCP 进程泄漏 Issue 以 37 条评论居首，Windows 发送按钮卡死、渲染进程启动崩溃、本地 API 被策略拦截等问题同日集中更新。远程/多端同步与本地会话数据一致性（删除残留、孤立 thread、侧边栏分组重置）构成第二大类长期未决问题。

---

## 二、版本发布

过去 24 小时共 7 个 Release，均为 Rust 侧 alpha 构建，Release note 内容为空（仅版本号），无对外可读的变更说明：

| 版本 | 说明 |
|---|---|
| `rust-v0.155.0-alpha.3.10` / `.3.9` / `.3.8` / `.3.7` / `.3` | 0.155.0 alpha.3 系列同日多次迭代，构建密集 |
| `rust-v0.155.0-alpha.2.3` | 0.155 alpha.2 分支的补丁构建 |
| `rust-v0.154.0-alpha.6.2` | 0.154 维护线仍在出补丁 |

**解读**：同日出现 `.7 → .10` 连续构建，通常意味着 alpha 阶段在快速试错或修复回归。结合今日 PR 中大量"稳定化"改动（语音、worktrees、插件设置），0.155 可能正在为一次较大版本收敛做准备。由于缺少 release note，外部开发者难以判断具体回归点，建议关注后续正式版变更日志。

---

## 三、社区热点 Issues（Top 10）

### 1. [MCP server 进程泄漏：每线程进程永不回收，RSS 已超 9 GB](https://github.com/openai/codex/issues/30408)
`bug / mcp / app-server / performance` · @kkkayye · 评论 37 · 👍 8 · 创建于 2026-06-28

app-server 为每个新线程启动一整套全局 MCP server 进程，但线程归档或关闭后**从不杀死**，孤儿进程无界累积。这是当前评论数最高的 Issue，且已跨两个多月未解决；9 GB RSS 的量化数据说明它已从"体验问题"升级为真实的机器资源事故。

### 2. [Windows 桌面：发送按钮无限转圈，提示词永不提交](https://github.com/openai/codex/issues/40968)
`bug / windows-os / app / session` · @BenzighemHoussam09 · 评论 36 · 👍 6 · 创建于 2026-08-26

Windows 11 上发送后续提示后按钮持续 spinning，会话实际上被卡死。属于**完全阻断使用**的级别，评论数说明受影响面很广，且持续两周多未修复。

### 3. [ChatGPT 端 "hit a snag" 崩溃复现（已关闭）](https://github.com/openai/codex/issues/44720)
`bug / app` · @cch123 · 评论 30 · 👍 5 · 创建于 2026-09-11

新提交即获 30 条讨论并当天关闭，属于典型的"高热度快速收敛"案例，可作为官方响应速度的正面样本。

### 4. [超大本地会话历史导致桌面端全面性能塌陷](https://github.com/openai/codex/issues/18693)
`bug / session / performance` · @twentyOne2x · 评论 20 · 👍 9 · 创建于 2026-04-20

打字、滚动、线程列表、随机退出全部受影响，范围远超"切换线程慢"。创建于 4 月，至今仍 OPEN，是**存在时间最长的性能类问题**之一，9 个 👍 表明长历史重度用户（正是 Codex 典型用户）普遍遇到。

### 5. [Agent 创建的顶层任务在桌面搜索与 Codex Mobile Remote 中不可见](https://github.com/openai/codex/issues/32614)
`bug / subagent / app-server / remote` · @hugo-alves · 评论 11 · 👍 3

子代理生成的任务在桌面搜索和移动端远程都找不到，破坏了"任务可追溯"的基本预期，也让远程接续工作流出现断点。

### 6. [Windows：本地 API 启动被 "blocked by policy" 拒绝](https://github.com/openai/codex/issues/41779)
`bug / windows-os / sandbox / tool-calls` · @JoseLuisMartinezMeza · 评论 10

`exec_command` 在 PowerShell 执行前即被策略拒绝，且不产生任何 stdout/stderr 日志。**静默失败 + 无诊断信息**是这类沙箱策略问题的核心痛点，用户几乎无法自查。

### 7. [已删除的 ChatGPT 会话仍残留在 Codex 侧边栏且无法移除](https://github.com/openai/codex/issues/42236)
`bug / windows-os / app / session` · @hyeo0319-bot · 评论 9

跨产品（ChatGPT ↔ Codex）数据同步不一致，删除操作不收敛。与 #14162（孤立 thread 条目）、#41214（归档任务复活）属同一类"本地状态与服务端真相不一致"问题族。

### 8. [Windows Computer Use 无法访问原生应用：应用清单为空、sky RPC 不可用](https://github.com/openai/codex/issues/43596)
`bug / windows-os / computer-use` · @GarryLyons · 评论 8 · 👍 2

Computer Use 在 Windows 上基本处于不可用状态，说明该能力在 Windows 平台的落地仍不完整。

### 9. [iOS Remote 项目列表与 Codex Desktop 不同步](https://github.com/openai/codex/issues/36454)
`bug / iOS / remote / session` · @yu-chern · 评论 7

桌面端未作为 Project 的 source of truth，移动端看到的是另一份列表。与 #32614、#34028 共同指向**远程控制与多端状态模型尚未统一**。

### 10. [Marketplace 升级暂存泄漏：41 天 4,972 个目录、559 GB](https://github.com/openai/codex/issues/39421)
`bug / CLI / skills` · @numberyy · 评论 5 · 👍 1

`~/.codex/.tmp/marketplaces/.staging/` 无清理机制，已有 curated clone 的清理 janitor 但未覆盖 marketplace。这是继 #29994（277 GB）之后更大的实测数据，属于**磁盘级资源泄漏**，与 #30408 同属"清理生命周期缺失"模式。

> 其他值得留意的条目：[#34028 Windows-to-Windows 远程控制需求](https://github.com/openai/codex/issues/34028)（👍 9）、[#44909 跨 3,808 个会话测量 false goal continuation 成本](https://github.com/openai/codex/issues/44909)、[#44748 Windows 升级后渲染进程启动即崩溃](https://github.com/openai/codex/issues/44748)、[#44908 skill 校验脚本缺 PyYAML](https://github.com/openai/codex/issues/44908)。

---

## 四、重要 PR 进展（Top 10）

> 注：本批 PR 均由 `copyberry[bot]` 提交，状态显示为 CLOSED，形态上更接近内部变更向公开仓库的投影同步，社区侧难以直接参与评审。

### 1. [为内置 GPT-5.4 / GPT-5.5 嵌入固定 friendly instructions](https://github.com/openai/codex/pull/44930)
将可选人格模板替换为固定 friendly 指令，这两个模型在 TUI 中不再支持人格选择。属于**模型行为收敛**，会影响现有依赖人格切换的用户工作流。

### 2. [TUI 语音会话默认开启](https://github.com/openai/codex/pull/44921)
`realtime_conversation` 从实验特性提升为 stable 并默认启用，移除实验性提示。语音交互

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报（2026-09-12）

## 今日速览

过去 24 小时，社区焦点高度集中在 **Agent/Subagent 可靠性**：generalist agent 挂起、subagent 达到 MAX_TURNS 却被误报为 GOAL 成功、browser agent 在 Wayland 下失败等 P1 问题持续发酵。安全侧同样活跃，sandbox 文件系统隔离、prompt injection 防护、checkpoint 路径穿越、Windows git 参数校验等多个 PR 集中推进。版本方面仅发布每日 nightly，无重大功能更新。

---

## 版本发布

- **v0.61.0-nightly.20260911.ged2ac40df**  
  自动 nightly 版本 bump，由机器人 PR #29285 完成，无具体功能变更说明。完整变更对比见：[Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.61.0-nightly.20260910.ged2ac40df...v0.61.0-nightly.20260911.ged2ac40df)

---

## 社区热点 Issues

1. **#22323 [P1] Subagent 达到 MAX_TURNS 却报告 GOAL 成功，掩盖中断**  
   评论数最高（13 条）。`codebase_investigator` subagent 在未完成分析、触达最大轮次限制的情况下，仍返回 `status: "success"` 和 `Termination Reason: "GOAL"`，导致中断被隐藏。该问题直接影响用户对 subagent 结果的信任，是当前 agent 可观测性缺陷的典型案例。  
   https://github.com/google-gemini/gemini-cli/issues/22323

2. **#21409 [P1] Generalist agent 无限挂起**  
   获得 8 个 👍，社区反馈强烈。用户报告每当 CLI 委派给 generalist agent 时就会永久挂起，简单如创建文件夹也会卡住，最长等待一小时；明确禁止使用 subagent 可规避。该问题严重阻塞日常使用。  
   https://github.com/google-gemini/gemini-cli/issues/21409

3. **#25166 [P1] Shell 命令执行完成后卡在 “Waiting input”**  
   shell 命令已结束，但 CLI 仍显示命令活跃并等待用户输入。该问题反复出现于极简命令中，属于核心执行链路的状态同步缺陷，影响所有依赖 shell 的工作流。  
   https://github.com/google-gemini/gemini-cli/issues/25166

4. **#19873 [P2] 利用模型 Bash 亲和性：零依赖 OS 沙箱 + 执行后意图路由**  
   架构级 enhancement，9 条评论。提案认为 Gemini 3 原生擅长链式 POSIX 工具（grep/cat/sed/awk），希望在不牺牲安全与 UX 的前提下释放该能力。该方向可能影响未来工具调用与沙箱设计。  
   https://github.com/google-gemini/gemini-cli/issues/19873

5. **#22745 [P2] 评估 AST-aware 文件读取、搜索与代码库映射**  
   EPIC 级追踪 issue，探讨通过 AST 感知工具精确读取方法边界、减少无效轮次与 token 噪声、提升代码导航效率。与 #22746 共同构成代码理解方向的重要探索。  
   https://github.com/google-gemini/gemini-cli/issues/22745

6. **#21968 [P2] Gemini 不够主动使用 skills 和 sub-agents**  
   用户反馈：除非显式指令，Gemini 几乎不会自主调用自定义 skills 与 sub-agents，即使任务高度相关。这直接影响扩展机制的实际价值，是 agent 编排策略的关键反馈。  
   https://github.com/google-gemini/gemini-cli/issues/21968

7. **#26525 [P2] Auto Memory 增加确定性脱敏并减少日志**  
   安全问题：Auto Memory 会读取本地 transcript 并将内容发送给后台提取模型，虽然 prompt 要求脱敏，但内容已进入模型上下文；服务还可能记录已有 skill 内容。该 issue 涉及

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报
**日期：2026-09-12** ｜ 数据来源：github.com/github/copilot-cli

---

## 一、今日速览

今日社区焦点集中在 **MCP 连接生命周期与会话恢复的稳定性**：多条新 Issue 反映 `/clear`、`--resume` 触发的前台会话交接会掐断 MCP 连接或导致 OOM 崩溃。同时，**Skills / AGENTS.md 指令体系**出现多个语义与发现范围相关的 bug（#4438、#4822、#4637）。版本侧发布 v1.0.84-5，新增 session/memory 导入命令，方向与社区长期呼声 #2436（跨会话上下文查询）一致。

---

## 二、版本发布

### v1.0.84-5

**Added**
- 新增 **session 与 memory 导入命令**，支持语义化 JSONL 交换格式（semantic JSONL interchange format），为跨会话/跨工具迁移上下文打下基础。

**Improved**
- **Shell 补全与解析器共用同一语法定义**：`copilot <TAB>` 现在同时提示根级 flag 与子命令，且每个子命令只提示自身可用选项，补全结果与实际解析行为保持一致。

> 注：原始数据中 "Command" 段落后续内容被截断，可能存在未列出的改进项。

---

## 三、社区热点 Issues（Top 10）

1. **[#4095](https://github.com/github/copilot-cli/issues/4095) Windows 插件更新失败 "Access is denied (os error 5)"** ｜ 👍 21（今日最高）
   VS Code 运行时会持有 `installed-plugins` 的文件监视句柄，导致 `copilot plugin update` 在 Windows 上失败。点赞数远超其他 Issue，说明这是高频阻断性问题，且跨 CLI / 桌面端同时受影响。

2. **[#4438](https://github.com/github/copilot-cli/issues/4438) `disable-model-invocation: true` 使技能彻底不可达** ｜ 👍 7 ｜ 评论 5
   该 flag 本意是"仅手动调用"，实际效果却是模型侧 `skill()` 返回 `Skill not found`，而 `copilot skill list` 又能列出——语义自相矛盾。影响所有依赖该字段做技能权限控制的团队。

3. **[#3700](https://github.com/github/copilot-cli/issues/3700) WSL2 回归：主线程空闲时占用 ~215% CPU，TUI 冻结** ｜ 👍 2 ｜ 高严重度
   自 1.0.60 起在 WSL2 上稳定复现，属于 #2208 的回归。TUI 完全无法刷新直到重启，严重影响 Linux 开发者日常使用。

4. **[#4699](https://github.com/github/copilot-cli/issues/4699) 长 `--resume` 会话 V8 堆 OOM 崩溃，且崩溃转储写入用户 cwd** ｜ 👍 5
   14 小时内崩溃 3 次，均触及 4 GiB 堆上限；额外问题是 Node diagnostic report 被写入当前工作目录，污染用户仓库。长会话可靠性 + 环境整洁双重隐患。

5. **[#4753](https://github.com/github/copilot-cli/issues/4753) v1.0.83 session resume 取消进行中的 stdio MCP 连接（超时从 ~16s 缩至 ~1s）** ｜ 👍 1
   会话恢复的前台交接会取消尚在初始化的 MCP server，导致整个会话期间该 server 静默不可用。与 #4818（HTTP MCP 在 `/clear` 后 stranded 为 failed）共同指向同一类架构缺陷。

6. **[#4795](https://github.com/github/copilot-cli/issues/4795) Atlassian MCP OAuth 回调地址不匹配（随机端口 vs 注册端口 33418）** ｜ 👍 3
   在 1.0.83 / 1.0.84-3 上均失败，WSL Ubuntu 24.04 环境。属于远程 MCP 接入的"第一公里"阻塞，与已关闭的 #4464（Entra OAuth 静默刷新 scope bug）构成远程 MCP 认证的一整片问题区。

7. **[#4809](https://github.com/github/copilot-cli/issues/4809) 原生 MCP 客户端在 `initialize` 前发送非标准 `server/discover`（已关闭）** ｜ 👍 0
   该私有请求违反 MCP 生命周期规范，会导致 spec-compliant server 崩溃。已关闭说明官方已受理，与 #4370（FastMCP 返回 `-32602` 即被判定为致命错误）同源，值得关注修复版本。

8. **[#1168](https://github.com/github/copilot-cli/issues/1168) 授权疲劳：单次高层请求触发十余次授权确认** ｜ 👍 2
   1 月提出、至今仍在更新，是持续时间最长的体验类 Issue。反映权限模型粒度过细且缺少批量/持久化授权策略。

9. **[#4764](https://github.com/github/copilot-cli/issues/4764) Assisted 权限模式约 1 小时后失效，需重开会话** ｜ 👍 0
   与 #1168 形成互补：一个"问得太多"，一个"授权后自己失效"。自动批准的状态机存在疑似时间相关的 bug。

10. **[#4035](https://github.com/github/copilot-cli/issues/4035) / [#4814](https://github.com/github/copilot-cli/issues/4814) Voice 模式安装因私有 Azure Artifacts feed 返回 401**
    语音运行时安装器尝试从私有 feed 拉取 `Microsoft.AI.Foundry.Local.Core 1.2.3`，而该包在 nuget.org 公开可用。今日 #4814 新开，说明问题在两个版本周期后仍未修复，语音功能实际处于不可用状态。

**其他值得留意的今日新 Issue**
- [#4822](https://github.com/github/copilot-cli/issues/4822) AGENTS.md 发现机制解析符号链接并遍历所有祖先目录，不尊重 Git 仓库边界，导致误加载无关仓库指令。
- [#4816](https://github.com/github/copilot-cli/issues/4816) 安装器会破坏长度超过 2047 字符的 PATH 环境变量。
- [#4817](https://github.com/github/copilot-cli/issues/4817) `ask_user` 多选参数泄漏到字符串参数时，选项降级为纯文本 JSON 打印。

---

## 四、重要 PR 进展

过去 24 小时内**无 Pull Request 更新**（0 条），因此本期无法提供 PR 级进展分析。结合 Issue 侧的高热度（33 条更新）与 PR 侧的空窗，可推断当前处于版本发布后的反馈收集窗口期，修复工作尚未以 PR 形式公开体现。

---

## 五、功能需求趋势

从本期全部 Issues 提炼出的社区关注方向：

| 方向 | 代表 Issue | 说明 |
|---|---|---|
| **MCP 生态健壮性** | #4753、#4795、#4809、#4370、#4818、#4636 | 占比最高的主题：生命周期合规、OAuth 回调、会话交接时连接保持、`--additional-mcp-config` 被协调逻辑抹除 |
| **会话与上下文记忆** | #4699、#2436、v1.0.84-5 | 跨会话上下文查询（#2436）是长期呼声，新版 import 命令与 OOM 问题从正反两面同时指向会话持久化 |
| **Skills / 自定义指令体系** | #4438、#4637、#4823、#4822 | 语义一致性、重复查找、输出可读性、发现范围边界，说明该特性已进入规模化使用阶段 |
| **权限与安全策略** | #1168、#4764、#4065、#4652 | 授权疲劳、自动批准失效、外泄保护误拦合法 spec 内容、sandbox 在 Windows 25H2 不受支持 |
| **成本与模型选择** | #4821、#4819 | 请求支持 OpenAI Flex tier（`service_tier: flex`）以降低 50% token 成本；组织策略加载时序导致默认模型选择失败 |
| **可扩展钩子** | #4820、#4813 | 希望增加"会话结束 hook"、桌面端渲染自定义状态行与上下文占用 |

---

## 六、开发者关注点

1. **会话交接是当前最大的脆弱点。** `/clear`、`--resume`、前台会话 handover 会在同一时刻打断 MCP 连接、触发内存问题、导致授权状态失效——#4753、#4818、#4699、#4764 本质上是同一个生命周期的四个切面。建议官方优先重构该路径。

2. **Windows / WSL2 体验明显落后。** 插件更新权限冲突（21 👍）、原生运行时反复崩溃（#4026，自 5 月未解）、sandbox 不支持新系统版本、WSL2 CPU 空转——平台一致性仍是最大的用户流失来源。

3. **MCP 规范符合性引发信任问题。** 客户端私自发送 `server/discover` 并在收到 `-32602` 时直接判定初始化失败，会让任何严格遵循规范的第三方 MCP server 无法接入，这直接影响生态扩展速度。

4. **长会话的资源管理亟待改善。** 4 GiB 堆上限、崩溃转储写入用户 cwd，属于"数据污染"级别的问题，开发者对此容忍度极低。

5. **权限系统两头不讨好。** 既提示过频（#1168），又会在无操作情况下自行失效（#4764）；同时安全侧的误拦（#4065）让用户不得不在"被打扰"和"被阻断"之间反复权衡。

6. **安装器的边界条件处理粗糙。** Voice 运行时拉私有 feed 导致 401（#4035 / #4814）、PATH 超 2047 字符被破坏（#4816），这类一次性但破坏性强的缺陷会严重影响首次上手体验。

---

*本报告基于 GitHub 公开数据自动整理，Issue 状态与评论数随时间变化，请以仓库实时页面为准。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-09-12** ｜ **数据来源：[github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)**

---

## 1. 今日速览

今日仓库整体处于**低活跃状态**：过去 24 小时无新版本发布、无 PR 更新，仅有 2 条 Issue 产生更新。其中，一条关于 **Linux/WSL2 下 0.42.0 随机硬死锁**的新增 Bug 报告值得高度关注——该问题会导致进程无法被 SIGTERM/SIGQUIT 终止，并连带拖垮 SSH 会话，属于影响面较广的稳定性缺陷。另一条为 3 月提交的 CentOS 7.9 MCP 连接失败问题，已于今日关闭。

> ⚠️ 数据说明：由于当日有效样本量极小（Issues 2 条、PR 0 条），本报告无法按常规"各取 10 条"的规模展开，趋势判断仅基于有限信号，建议结合多日数据交叉验证。

---

## 2. 版本发布

过去 24 小时内**无新版本发布**。当前社区反馈中出现的版本号为 `0.42.0`（Issue #2640）与 `1.17.0`（Issue #1388），版本号跨度较大，建议维护者在后续 Release Note 中明确版本对应关系，以免用户混淆。

---

## 3. 社区热点 Issues

今日更新的 Issue 共 2 条，全部列出如下：

### 🔴 #2640 [OPEN] [bug] Linux/WSL2 下 kimi CLI 0.42.0 随机硬死锁，SIGTERM/SIGQUIT 无法终止，并拖死 SSH 会话
- **作者**：@jinruyan02 ｜ 创建/更新：2026-09-11 ｜ 评论：0 ｜ 👍：0
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2640
- **为什么重要**：
  - **影响面大**：Linux/WSL2 是 CLI 工具的核心使用场景，尤其是 WSL2 在 Windows 开发者中普及率极高。
  - **故障性质严重**：长时间运行后 TUI 偶发卡死且无响应，属于"硬死锁"级别的稳定性问题；更关键的是**进程无法通过 SIGTERM/SIGQUIT 正常终止**，意味着常规的守候进程回收手段失效，只能强制 kill -9。
  - **连锁影响**：报告指出该问题还会**拖垮 SSH 会话**，这对远程开发用户而言是致命体验问题——一个 CLI 卡死可能导致整个远程会话不可用。
  - **环境信息明确**：Kimi Code 订阅 + `kimi-for-coding` 模型 + 0.42.0 版本，复现线索较为完整。
- **社区反应**：目前评论数为 0、无点赞，尚未形成讨论，但问题本身的严重性足以支撑其成为今日最值得关注的动态。建议维护团队尽快复现并确认是否为 TUI 事件循环或子进程/PTY 句柄泄漏所致。

### 🟢 #1388 [CLOSED] [bug] kimicode 在 CentOS 7.9 terminal 无法使用，显示 mcp connect failed
- **作者**：@supsmile ｜ 创建：2026-03-10 ｜ 更新/关闭：2026-09-11 ｜ 评论：0 ｜ 👍：0
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/1388
- **为什么重要**：
  - 典型的企业内网/老旧发行版兼容性问题：CentOS 7.9 仍在大量企业内部环境中服役，MCP 服务连接失败会直接阻断功能使用。
  - 该 Issue 从 3 月挂到 9 月才关闭，**生命周期长达半年**，反映出老旧平台兼容问题在排期中的优先级可能偏低。
- **社区反应**：无评论、无点赞，属"沉默关闭"型 Issue。关闭本身是好信号，但缺少公开的解决方案说明，其他遇到同类问题的用户可能仍需自行摸索。

---

## 4. 重要 PR 进展

过去 24 小时内**无 Pull Request 更新**。

值得留意的是，当日既无新 PR 也无 PR 活动，而同时存在一条未解决的严重稳定性 Issue（#2640），社区的修复动作尚未在 PR 层面体现。建议关注未来 24–48 小时内是否出现针对该死锁问题的修复提交。

---

## 5. 功能需求趋势

由于当日样本仅 2 条 Issue，以下趋势为**弱信号推导**，需持续观察：

| 方向 | 信号来源 | 观察 |
| --- | --- | --- |
| **运行稳定性 / 长时任务可靠性** | #2640 | 长时间运行后的死锁与进程不可回收问题，是当日最强信号。CLI 类 AI 编程工具通常需要长时间驻留会话，稳定性优先级应高于新功能。 |
| **跨平台兼容性** | #2640、#1388 | 同时覆盖 Linux/WSL2 与 CentOS 7.9，说明社区用户环境高度分散，兼容性测试矩阵需要扩展。 |
| **MCP 生态连通性** | #1388 | MCP 服务连接失败直接使功能不可用，MCP 集成的健壮性与错误提示友好度仍是关注点。 |
| **远程/SSH 场景支持** | #2640 | 死锁拖垮 SSH 会话，暗示远程开发是实际使用中的重要场景，但当前 TUI 对终端异常状态的容错不足。 |

> 注：当日数据中**未出现**关于 IDE 集成、新模型支持、性能优化等方向的直接issue，故不作展开。

---

## 6. 开发者关注点

综合今日有限的反馈，开发者痛点集中在以下几点：

1. **进程生命周期管理失控**（#2640）：程序卡死后无法响应标准信号终止，是 CLI 工具最不可接受的缺陷之一。核心诉求是"随时可安全中断并清理资源"。
2. **终端环境鲁棒性**：无论是 WSL2 的 PTY 行为差异，还是 CentOS 7.9 的老旧依赖栈，TUI 与 MCP 层都需要更强的环境探测与降级能力。
3. **故障隔离不足**：一个 CLI 进程的异常能波及 SSH 会话，说明资源占用或终端状态恢复机制存在设计缺口，建议引入更严格的句柄/子进程回收与超时熔断。
4. **问题响应透明度**：#1388 静默关闭、#2640 零回复，提示社区希望获得更明确的进展同步（如 issue 标签、复现状态、修复版本）。

---

### 📌 编辑建议

今日仓库活跃度处于低位，日报内容以"稳定性告警"为主线。若明日数据量仍偏少，建议改为**滚动式观察**：跟踪 #2640 是否获得维护者回复或关联 PR，并关注是否出现针对 0.42.0 的热修复版本。

*本日报由 AI 工具链自动生成，数据截取自 2026-09-12 的 GitHub 仓库公开信息。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 · 2026-09-12

数据来源：github.com/anomalyco/opencode

---

## 1. 今日速览

今天没有新版本发布，社区注意力集中在 **v2（beta）/ v1.18.30 的稳定性回归** 上：子代理无保护死循环导致 Token 失控、Copilot Legacy 配额被单条 prompt 打满、TUI 崩溃与会话状态静默失败等问题同日集中出现。与此同时，**计费与配额透明度**（Go 订阅余额、DeepSeek 缓存命中率为 0）成为本周最高热度话题。PR 侧出现一次大规模 **automated-pr-cleanup** 自动关闭浪潮，约 50 个 8 月中旬提交的积压 PR 被清理。

---

## 2. 版本发布

过去 24 小时无新 Release。相关的发布侧动作是 maintainer 的 PR #48564：因 `v2` 分支尚未配置 Azure Trusted Signing，**暂时将 Windows 桌面端产物从 V2 stable release 中移除**。
https://github.com/anomalyco/opencode/pull/48564

---

## 3. 社区热点 Issues（Top 10）

**1. #37790 [BUG] Go 订阅已付款但工作区显示 "Insufficient balance"**（18 评论）
付费成功（Stripe）但服务不可用，属于直接影响收入的计费链路故障，是本日评论数最高的 Issue，且已挂起近两个月仍未解决。
https://github.com/anomalyco/opencode/issues/37790

**2. #27110 [FEATURE] 限制并行子代理数量上限**（31 👍，全场最高）
本地模型受限于上下文与显存，并行子代理会让任务反而变慢。高赞说明这是本地/自托管用户的刚需配置项。
https://github.com/anomalyco/opencode/issues/27110

**3. #45442 [2.0] 子代理死循环：364 次相同 grep 调用、持续约 50 分钟**（8 评论）
无循环保护、Token 不可控消耗，提交者附上了完整的调用记录。这是 v2 子代理编排最严重的可靠性问题之一。
https://github.com/anomalyco/opencode/issues/45442

**4. #10939 [CLOSED] `auth login <url>` 未确认即执行远程下发的 auth.command**（6 👍）
安全类问题：`opencode auth login` 拉取 `.well-known/opencode` 后直接执行远端返回的命令，未做确认与 payload 校验。虽已关闭，但值得确认修复是否覆盖全部路径。
https://github.com/anomalyco/opencode/issues/10939

**5. #40993 [FEATURE] 支持 Agent Plugins 标准（agent-plugins.org）**（12 👍）
厂商中立的 Agent Skills + MCP 打包规范，属于跨厂商生态布局，社区呼声明显。
https://github.com/anomalyco/opencode/issues/40993

**6. #48330 [2.0] 单条 prompt 耗尽 Copilot Legacy 全部请求额度**（6 评论）
1500 请求/月的 legacy 订阅在 opencode2 中被一次性打完并触发 429，opencode 1 无此问题，是典型的 v2 版本线上回归。
https://github.com/anomalyco/opencode/issues/48330

**7. #41125 / #43218 OpenCode Go 端点 DeepSeek 提示缓存始终为 0**（3 + 3 评论）
两个独立报告相互印证：即便重复发送完全相同的 prompt，`prompt_cache_hit_tokens` 仍为 0，用户实测命中率低于 10% 并持续下降。直接推高使用成本。
https://github.com/anomalyco/opencode/issues/41125 · https://github.com/anomalyco/opencode/issues/43218

**8. #36241 [macOS] gpt-5.6-sol-fast/high 反复报 `reasoning part rs_*:0 not found`**（7 评论）
Codex OAuth 下流式 reasoning 中断，属于新模型适配层的解析问题。
https://github.com/anomalyco/opencode/issues/36241

**9. #30308 [FEATURE] 类似 Claude Code 的动态工作流（dynamic workflows）**
请求对齐 Claude Code 的 workflows 能力，反映社区期望 OpenCode 在"可编排的 Agent 工作流"上补齐能力。
https://github.com/anomalyco/opencode/issues/30308

**10. v1.18.30 回归问题集群（同日新增）**
- #48553 Desktop 首启 splash 遮罩不消失（白屏 + 脉冲 logo，底层 UI 实际可用）
- #48543 Compaction 在请求未返回时仍持久化摘要边界（无 parts、error 为 null、token 未填充，失败被静默吞掉）
- #48384 TUI 崩溃 `ENOSPC: no space left on device`（watch 状态目录）
- #48503 提交 prompt 后完全无响应、无错误、无 loading 提示

https://github.com/anomalyco/opencode/issues/48553 · https://github.com/anomalyco/opencode/issues/48543 · https://github.com/anomalyco/opencode/issues/48384 · https://github.com/anomalyco/opencode/issues/48503

> 另：#48530 报告 `session.error` 事件被 global sync reducer 忽略，会话卡在 busy 状态且不显示错误 —— 与上述"静默失败"是同一类根因。

---

## 4. 重要 PR 进展

> ⚠️ 今日 PR 列表的绝大多数被标记为 `[automated-pr-cleanup]` 且状态为 CLOSED —— 这是一次针对 8 月 11 日前后积压 PR 的批量自动清理（30 天无更新）。下列条目仍具参考价值，部分值得作者 rebase 后重开。

**1. #48564 fix(release): 从 V2 stable 中省略 Windows 桌面端**（thdxr）
临时规避 Azure Trusted Signing 未配置的问题，直接影响 v2 Windows 用户的分发。
https://github.com/anomalyco/opencode/pull/48564

**2. #41824 feat: 暴露 Go 与 Zen 用量**（bot）
新增认证 Console 端点 + `GET /api/usage`，返回 Go 配额窗口与 Zen 计费用量，并生成 SDK 客户端方法。直接回应了本日最高热度的计费透明度问题。
https://github.com/anomalyco/opencode/pull/41824

**3. #41748 fix(session): 提交新 prompt 时中断正在运行的 prompt**
修复助手执行长耗时 bash 命令时，用户新输入无法抢占的问题。
https://github.com/anomalyco/opencode/pull/41748

**4. #41842 fix(tui

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-09-12）

> 数据来源：github.com/QwenLM/qwen-code ｜ 统计窗口：过去 24 小时

---

## 一、今日速览

今日仅发布一个 nightly 版本，核心动态集中在**稳定性与安全**两条主线：Windows 平台的 PTY/进程泄漏与 MCP 连接问题持续占据高热度，VS Code 集成（Remote-SSH、会话历史）出现回归；同时社区集中反馈了**遥测与调试日志泄露原始请求内容**、CI 依赖 CVE 审计失败等安全议题，对应修复 PR 已陆续提交。

---

## 二、版本发布

### v0.23.3-nightly.20260911.aaa6a32aae

- `refactor(dingtalk)`：移除废弃的后台响应聚合逻辑（[PR #11570](https://github.com/QwenLM/qwen-code/pull/11570)）
- `feat(channels)!`：移除 `me` 相关通道能力 —— **标注为破坏性变更（breaking change）**，Release notes 中该项内容被截断，建议关注后续正式版迁移说明

---

## 三、社区热点 Issues（10 条）

### 1. [#11500](https://github.com/QwenLM/qwen-code/issues/11500) ⭐ P1｜TUI 在多个后台 Agent 完成时静默退出
未捕获的 React #185（"Maximum update depth exceeded"）导致交互式 TUI 直接崩溃回 shell，无任何错误渲染；恢复会话时 CLI 还会提示 "Previous session appears…"。根因指向 Ink `useBoxMetrics` 的 layout-listener setState 循环。**这是当前最高优先级的前端渲染稳定性缺陷**，6 条评论均为复现与定位讨论。

### 2. [#11352](https://github.com/QwenLM/qwen-code/issues/11352) ⭐ P1｜Windows web-terminal PTY 泄漏 conhost.exe
范围已收窄至 web-terminal PTY：shell-tool 部分已由 #11497 修复（改用自带 ConPTY 后端 `useConptyDll: true`），但 web-terminal 仍会在自然退出时遗留 `conhost.exe --headless

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*