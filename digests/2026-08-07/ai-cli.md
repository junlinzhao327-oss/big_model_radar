# AI CLI 工具社区动态日报 2026-08-07

> 生成时间: 2026-08-06 22:35 UTC | 覆盖工具: 7 个

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

**报告日期：2026-08-07 · 数据窗口：过去 24 小时 GitHub 社区动态**

---

## 一、生态全景

AI CLI 工具已全面进入"高迭代、高争议、高风险"的密集竞争期。主流工具在 Agent 自主性上持续加码，但子代理失控、token 消耗不可控、静默失败等可靠性问题成为全行业共性痛点。安全边界（MCP 生命周期、文件信任域、只读命令绕过）与成本治理（配额透明、预算中断）正在取代基础代码生成能力，成为社区最强烈的诉求方向。与此同时，Linux/Windows 桌面端支持缺口和会话持久化能力，构成了下一阶段产品差异化的关键战场。

---

## 二、各工具活跃度对比（今日列出）

| 工具 | Issues 数 | PR 数 | Release 情况 |
|---|---|---|---|
| **Claude Code** | 5 个（#16157 达 1486 评论） | 未单列（v2.1.223 已发布） | ✅ v2.1.223 正式版：Marketplace 通配符管理 |
| **OpenAI Codex** | 10 个（#11023 获 931 👍） | 10 个（MCP/模型切换/插件系统为主） | ✅ rust-v0.147.0-alpha.13 内部迭代 |
| **Gemini CLI** | 10 个（3 个 P1 级） | 6 个（消息融合修复、Gemini 3.6 Flash 支持） | ✅ v0.54.0 稳定版 + v0.55.0-preview.1 + nightly |
| **GitHub Copilot CLI** | 无数据 | 无数据 | 无数据 |
| **Kimi Code** | 3 个（记忆系统 #1283 居首） | 1 个（#2594 数据损坏修复） | 无新版本 |
| **OpenCode** | 10 个（#37852 获 52 👍） | 10 个（Hosted Workspace、会话导入导出） | 无新 Release（CLI v1.18.14 / V2 next） |
| **Qwen Code** | 10 个（#3203 达 151 评论） | 3 个（安全修复为主） | ✅ v0.21.6-nightly + live-host-v0.1.0 |

> 注：以上为各工具今日日报列出的活跃条目数，并非仓库全部积压量。GitHub Copilot CLI 本次未提供有效数据，不参与后续分析。

---

## 三、共同关注的功能方向

### 1. 子代理/后台 Agent 的可靠性与可控性（最广泛）
- **Claude Code**：#65796 workflow 恢复后静默重跑已完成子代理；#72080 子代理陷入 `count <invoke` 无限循环。
- **OpenAI Codex**：#37282 无人值守会话单次消耗 42 亿 tokens，且无中断路径。
- **Gemini CLI**：#22323 子代理达轮次上限却误报成功；#21409 generalist 子代理无限挂起。
- **OpenCode**：#37852 提供者流中断被记录为"干净停止"，子代理静默返回空结果。

**核心诉求**：子代理需要明确的终止条件、成本上限、中途干预能力，以及"失败≠成功"的诚实状态上报。

### 2. 会话持久化与跨会话记忆
- **Kimi Code**：#1283 跨会话 Memory System（20 评论，当前最高讨论量）。
- **OpenAI Codex**：#23999 侧边栏历史丢失；#26227 side chats 持久化为子线程（22 👍）。
- **OpenCode**：#24628 会话取证静默停止落盘；#40914 会话导入/导出 PR 进入评审。
- **Gemini CLI**：#26522 Auto Memory 无限重试低信号会话，浪费上下文。

### 3. MCP 生命周期与资源安全
- **OpenAI Codex**：#30408 每线程产生一套 MCP 进程且从不回收（9+ GB RSS）；PR #37273/#37261 优化 MCP handler 缓存与懒启动。
- **OpenCode**：#26195 MCP OAuth 流程无法打开浏览器；#40125 按 MCP 服务器的信任配置（指纹固定）。
- **Gemini CLI**：PR 侧持续增强 MCP OAuth（#28679 相关）。

### 4. 模型路由与配额透明度
- **OpenCode**：#40409 `deepseek-v4-flash` 实际返回 V3.2；#40928 免费层上下文配额分配不透明。
- **Claude Code**：#16157 Max 订阅瞬间触发周限额（1486 评论、692 👍）。
- **Qwen Code**：#3203 免费额度从 1,000 次/日削减至 100 次的提案引发 151 条评论反对。

### 5. Windows 平台系统性体验问题
- **OpenAI Codex**：#20214 频繁冻结、#34260 taskkill.exe 进程风暴耗尽 WMI、#26613 闪烁 PowerShell 窗口。
- **Qwen Code**：#8615 桌面版启动即崩溃（`EISDIR lstat 'C:'`）。
- 共性：桌面端进程模型、渲染性能、权限隔离均未达到与 macOS 同等的成熟度。

### 6. 安全边界与数据完整性（新兴趋势）
- **Qwen Code**：#8582 只读 shell 分类器可被 `${var@P}` 绕过；#8627 信任目录被祖先覆盖；#8643 从不可信祖先加载 `.env`。
- **Kimi Code**：#2591 `StrReplaceFile` 破坏编辑区域外的非 UTF-8 字节（永久损坏二进制文件）。
- **OpenCode**：#39875 静默移除 Go 服务提供商署名，社区信任情绪累积。

---

## 四、差异化定位分析

| 工具 | 定位 | 目标用户 | 技术路线与侧重点 |
|---|---|---|---|
| **Claude Code** | 企业级深度代理工作流 | 专业开发团队、重度 Claude 订阅用户 | 功能覆盖面最广（marketplace、workflow、skills、slash commands），但计费争议大规模反噬；桌面版与 CLI 功能不对等。 |
| **OpenAI Codex** | 跨平台桌面 + CLI 一体化 | 多设备开发者、MCP 重度用户 | Rust 内核高频 alpha 迭代，MCP 生命周期管理投入最大；桌面端宏伟但 Windows 稳定性拖后腿；Linux 桌面诉求极强（931 👍）。 |
| **Gemini CLI** | Gemini 模型原生体验 | Google 生态开发者、依赖 Gemini 长上下文用户 | 与 Gemini 模型深度绑定（3.6 Flash 支持），工程侧重视 Agent 行为评估体系（#24353 已有 76 个评估测试）；子代理"报喜不报忧"和挂起是当前最大的体验裂痕。 |
| **Kimi Code** | 轻量、聚焦核心编辑体验 | 追求简单可靠的个人开发者 | 社区体量最小，但跨会话记忆需求（#1283）呼声最高；数据完整性 bug 当日提交修复（#2594），响应及时但暴露基础文件操作防护不足。 |
| **OpenCode** | 开源可定制、V2 架构演进 | 开源爱好者、自托管/多提供商用户 | 明确分为 CLI v1.18 与 V2 next 双线；TUI 交互打磨最细（排队/打断/压缩语义）；重视配置兼容（混合格式）与可迁移性（导入导出）；Go 订阅的透明度问题最尖锐。 |
| **Qwen Code** | 多模型兼容 + 自有模型生态 | Qwen 生态用户、代理/中转场景用户 | 安全议题集中爆发（只读绕过、信任域、`.env` 加载，均已有修复 PR）；Live Host 起步；hooks 回归（#8622）暴露核心扩展机制稳定性不足。 |

---

## 五、社区热度与成熟度

### 社区活跃度分层
- **第一梯队（超大规模）**：**Claude Code**——单 Issue 达 1486 评论、692 👍，是当前 AI CLI 社区情绪最强烈的仓库；**OpenAI Codex**——高频 alpha 发布 + 10 PR/日，工程节奏最快。
- **第二梯队（活跃争议）**：**Qwen Code**——151 评论的免费额度政策争议；**OpenCode**——功能需求点赞数高（#32157 达 67 👍），TUI 讨论深入。
- **第三梯队（平稳推进）**：**Gemini CLI**——稳定版 + preview 双轨发布，P1 issue 讨论务实；**Kimi Code**——社区体量小，但功能提案讨论质量高。

### 成熟度特征
- **快速迭代期**：OpenAI Codex（alpha 序列日更）、Gemini CLI（nightly 每日滚动）、Qwen Code（nightly + 新子产品 live-host）。
- **稳定维护期**：Claude Code（正式版 + 高频 issue 治理）、Open

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---

# Claude Code 社区动态日报 — 2026-08-07

## 今日速览

v2.1.223 正式发布，新增 GitHub Org 级 marketplace 通配符管理能力；与此同时，Max 订阅限额问题（#16157）以 1486 条评论持续发酵，成为仓库内长期热度最高的 Issue。社区对子代理/后台任务的 token 失控消耗、以及桌面版与 CLI 功能不对等的问题讨论显著升温。

## 版本发布

### v2.1.223
- **Marketplace 通配符管理**：在 `strictKnownMarketplaces` 与 `blockedMarketplaces` 管理设置中新增 `"owner/*"` 通配符条目，可批量允许或阻止某个 GitHub 组织下的所有 marketplace 仓库
- **新增警告**：当 workflow agents、forked skills、slash commands 或恢复的后台任务（原文截断）运行时，会触发新警告

## 社区热点 Issues

### 1. Max 订阅瞬间触发使用限制
[#16157](https://github.com/anthropics/claude-code/issues/16157) | 1486 评论 | 👍 692

自 2026-01-03 创建至今持续发酵，Max 用户报告在常规使用中"瞬间"耗尽周限额，社区强烈质疑计费/限额系统的准确性。这是当前仓库内关注度最高的单条 Issue。

### 2. Workflow 多代理恢复后静默从头重跑
[#65796](https://github.com/anthropics/claude-code/issues/65796) | 13 评论

带可复现用例。Workflow 在 auto-compaction 后恢复会从头重新执行，已完成的子代理被静默重跑。直接影响复杂多代理任务的成本与结果正确性。

### 3. 子代理陷入无限循环，消耗大量 token
[#72080](https://github.com/anthropics/claude-code/issues/72080) | 7 评论

Linux/VS Code 环境下，子代理反复进入 `count <invoke...` 循环，即使主代理干预后仍会复发，用户反馈已消耗大量 token。

### 4. Linux/IntelliJ OAuth 登录死循环
[#77966](https://github.com/anthropics/claude-code/issues/77966) | 25 评论

登录时 `state` 参数在 "sign in again to continue" 重定向后丢失，导致 OAuth 无限循环。平台特定问题，直接影响 Linux + IntelliJ 用户使用 Claude 账号。

### 5. PreToolUse/PostToolUse additionalContext 变更导致提示词缓存失效
[#839

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-07

## 今日速览

过去 24 小时，Codex 发布了 `rust-v0.147.0-alpha.13` 内部迭代版本；社区热度持续聚焦三大方向：**Linux 桌面应用支持**（#11023 已获 931 👍）、**Windows 平台稳定性问题**（冻结、进程风暴、窗口闪烁等），以及 **MCP 资源泄漏与会话失控**（单次会话消耗 42 亿 tokens）。PR 方面，大量 `copyberry[bot]` 自动化提交集中优化 MCP 生命周期管理、插件系统与模型切换逻辑，架构内部治理节奏明显加快。

## 版本发布

- **rust-v0.147.0-alpha.13**：过去 24 小时发布了 0.147.0-alpha.13。仓库未提供详细 changelog，属于高频迭代的 alpha 版本序列，预计主要包含内部架构优化与 bug 修复。

## 社区热点 Issues（10 个）

1. **[#11023] Codex desktop app for Linux**  
   评论 202 | 👍 931  
   作者因 macOS 上 App 功耗问题（#10432）而强烈希望 Linux 桌面版可用，目前是社区赞同数最高的 Issue，反映出 Linux 开发者对 Codex App 的显著需求缺口。  
   https://github.com/openai/codex/issues/11023

2. **[#20214] Codex App 在 Windows 11 Pro 上频繁冻结/卡顿**  
   评论 91 | 👍 81  
   系统资源充足（Ryzen 5 5600 + 32GB RAM）仍出现严重性能问题，是 Windows 平台反馈最集中的 Issue 之一，说明桌面端在 Windows 上的渲染/进程模型存在系统性缺陷。  
   https://github.com/openai/codex/issues/20214

3. **[#34260] Windows Desktop: taskkill.exe/conhost.exe 无界清理风暴耗尽 WMI**  
   评论 33 | 👍 11  
   桌面端进入无界进程清理循环，数百个 `taskkill.exe` 与 `conhost.exe` 常驻，反复查询 Win32_Process 导致 WMI 配额耗尽、系统整体卡死，属于 Windows 专属的严重稳定性 bug。  
   https://github.com/openai/codex/issues/34260

4. **[#30408] MCP 服务器进程泄漏：每个线程产生一组进程且从不回收（9+ GB RSS）**  
   评论 25 | 👍 7  
   app-server 为每个新线程生成全套全局 MCP 服务器进程，归档/关闭线程时不会 kill，导致孤儿进程无限累积。这是当前 MCP 资源管理最突出的缺陷。  
   https://github.com/openai/codex/issues/30408

5. **[#23999] Codex Desktop 侧边栏聊天历史消失，更新后仍无法恢复**  
   评论 12 | 👍 3  
   macOS 最新版桌面端侧边栏历史记录整体丢失，即使用户手动升级或重启也无法恢复，直接冲击核心工作流，社区信任成本高。  
   https://github.com/openai/codex/issues/23999

6. **[#26227] 将 side chats 持久化为附着在主线程下的子线程**  
   评论 11 | 👍 22  
   增强需求：side chat 是长任务中最高效的交互模式，但当前设计为临时性，会在关闭或更新后消失。社区希望 side chats 能作为主线程的子线程持久保存。  
   https://github.com/openai/codex/issues/26227

7. **[#26613] Windows Desktop 轮询后台进程时闪烁可见的 PowerShell/控制台窗口**  
   评论 11 | 👍 1  
   桌面端频繁启动短生命周期 `powershell.exe` 进程且带有可见控制台窗口，影响用户专注度，也暴露了 Windows 进程启动方式上的粗糙实现。  
   https://github.com/openai/codex/issues/26613

8. **[#26907] 远程启动的 Codex 线程不接收 codex_app 线程管理工具**  
   评论 10 | 👍 10  
   用户从 MacBook 远程控制 Mac Studio 启动 Codex 线程后，线程缺少 app 级管理工具，导致远程工作流不完整。多设备/远程场景正在成为高频使用方式。  
   https://github.com/openai/codex/issues/26907

9. **[#37282] 无人值守会话从一条提示运行 16.5 小时：7,395 次请求、42 亿 tokens、无中断路径**  
   评论 2 | 👍 0  
   一条提示触发后连续运行 16.5 小时，消耗 42 亿 tokens，用户无法中断，最终以认证错误结束。这是目前最严重的失控会话案例，直接指向缺少预算/中断保护机制。  
   https://github.com/openai/codex/issues/37282

10. **[#35470] Codex 将同一镜像文件复制 150,000 次，消耗 400 GiB 磁盘空间**  
    评论 3 | 👍 0  
    Windows CLI 0.145.0 在上下文/子代理处理过程中对同一镜像文件进行了 15 万次复制，消耗 400+ GiB 磁盘。属于极端资源浪费 bug，暴露文件去重机制的缺失。  
    https://github.com/openai/codex/issues/35470

## 重要 PR 进展（10 个）

1. **[#37260] Fix first-turn model switching and rollback**  
   修复首轮切换模型时无先前设置可比对、回滚后模型指令残留的问题。对 multi-agent 和模型动态切换场景有直接影响。  
   https://github.com/openai/codex/pull/37260

2. **[#37273] Reuse MCP handlers across sampling steps**  
   在会话生命周期内缓存 MCP handlers，避免每个 sampling step 重复构建 schema。性能优化类 PR，降低 MCP 调用开销。  
   https://github.com/openai/codex/pull/37273

3. **[#37261] Start cached MCP servers lazily for subagents**  
   子代理复用已缓存的 MCP 工具定义时，不再预先启动所有可选服务器，改为使用时按需启动，减少资源占用。  
   https://github.com/openai/codex/pull/37261

4. **[#37204] Add durable user-message queue dispatch**  
   新增持久化用户消息队列：支持列出、添加、编辑、重排、删除和显式启动排队消息；线程空闲后按 FIFO 顺序派发。  
   https://github.com/openai/codex/pull/37204

5. **[#37206] Add a unified image budget**  
   引入 `unified_image_budget` 特性，对支持原始图像细节或 Responses Lite 的模型统一应用 6000 像素 / 10,000 patch 预处理上限，统一图像处理逻辑。  
   https://github.com/openai/codex/pull/37206

6. **[#37267] Support plugin roots in the host skill loader**  
   Host skill loader 支持插件根路径：携带插件身份、命名空间、根路径和发现模式，并拒绝不符合直接子级发现的插件技能。  
   https://github.com/openai/codex/pull/37267

7. **[#37210] Fetch remote installed plugins across all scopes**  
   改为一次无 `scope` 查询获取全部已安装插件快照（全局/用户/工作区），替代原有的分区请求，简化插件的缓存与同步。  
   https://github.com/openai/codex/pull/37210

8. **[#37191] Preserve legacy semantics during rollout migration**  
   旧版 rollout 中的历史回滚、压缩检查点、子代理复制等记录在迁移时需保持原有语义，避免恢复后的可见对话或模型上下文发生改变。  
   https://github.com/openai/codex/pull/37191

9. **[#37190] Interrupt cyber model turns after one Guardian denial**  
   针对目录中 specialty 为 `cyber` 的模型，在 Guardian 第一次拒绝后即中断整个 turn，其他模型维持原有阈值。安全相关策略收紧。  
   https://github.com/openai/codex/pull/37190

10. **[#37198] Prefer persisted cwd when reading local threads**  
    线程读取时优先使用 state 数据库中持久化的 `cwd`（非空时），避免 rollout 中记录的旧路径与线程元数据不一致导致列表错乱。  
    https://github.com/openai/codex/pull/37198

## 功能需求趋势

- **Linux 桌面应用**：#11023 以 931 👍 高居榜首，是当前社区最强烈的功能诉求。
- **Windows 稳定性专项**：冻结、taskkill 风暴、PowerShell 窗口闪烁、Computer Use 枚举失败等 Windows 专属问题密集出现，且多个被标记为 `Papercuts 2026`，说明官方已开始系统治理 Windows 体验。
- **会话持久化与历史管理**：侧边栏历史

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报（2026-08-07）

## 今日速览

- 官方发布 v0.54.0 稳定版，并同步推出 v0.55.0-preview.1 与最新夜间版，重点修复 macOS 沙箱配置缺失问题。
- 社区对 Agent 稳定性反馈集中：子代理卡死、错误报告成功、Shell 命令执行后挂起等 P1 级 Issue 讨论活跃。
- PR 侧持续改善核心体验：修复消息融合 Bug、新增 Gemini 3.6 Flash 模型支持、增强 MCP OAuth 与上下文管理能力。

## 版本发布

- **v0.54.0（稳定版）**：面向稳定渠道发布，主要包含历史变更日志整理与版本号升级（v0.53.0-preview.0 → v0.54.0）。
- **v0.55.0-preview.1**：预览版例行更新，同步夜版变更日志。
- **v0.55.0-nightly.20260806.g761f604c1**：修复 macOS 上嵌入式 seatbelt 配置文件缺失时无法回退的问题；新增 PR 生成器核心模块（环境配置解析器、命令执行器、GitHub 交互）。

## 社区热点 Issues

挑选出讨论热度高、直接影响日常使用的 10 个 Issue：

1. **[#22323] Subagent 在 MAX_TURNS 后被误报为 GOAL 成功**（P1，12 条评论）  
   `codebase_investigator` 子代理实际因达到最大轮次而中断，却上报 `status: success`，导致主代理误判任务完成并掩盖中断原因。  
   🔗 https://github.com/google-gemini/gemini-cli/issues/22323

2. **[#21409] 通用型 Agent 无限挂起**（P1，8 条评论）  
   一旦 gemini-cli 将任务委派给 generalist 子代理，就永久阻塞（建文件夹这种简单操作也会卡死），用户最多等待 1 小时仍无响应；禁用子代理后恢复正常。  
   🔗 https://github.com/google-gemini/gemini-cli/issues/21409

3. **[#19873] 利用模型的原生 bash 能力：零依赖 OS 沙箱与执行后意图路由**（P2，8 条评论）  
   建议让模型在安全沙箱中自由使用 grep/cat/sed/awk 等 POSIX 工具，在执行后再根据结果路由意图，兼顾安全性与模型原生工作方式。  
   🔗 https://github.com/google-gemini/gemini-cli/issues/19873

4. **[#24353] 健壮的组件级评估（EPIC）**（P1，7 条评论）  
   目前已有 76 个行为评估测试并覆盖 6 种 Gemini 模型，但需进一步构建组件级评估体系，追踪独立 Agent 组件的回归。  
   🔗 https://github.com/google-gemini/gemini-cli/issues/24353

5. **[#22745] 评估 AST 感知的文件读取/搜索/代码库映射**（P2，7 条评论）  
   希望利用 AST 精确读取方法边界、减少无效轮次并降低 token 噪声，为 `codebase_investigator` 等提供更高效的代码库导航。  
   🔗 https://github.com/google-gemini/gemini-cli/issues/22745

6. **[#21968] Gemini 不会主动使用 skills 和子代理**（P2，6 条评论）  
   用户反映即使配置了 gradle、git 等自定义技能，模型仍几乎不会主动调用，只有显式指示才会执行，导致技能价值大打折扣。  
   🔗 https://github.com/google-gemini/gemini-cli/issues/21968

7. **[#26522] Auto Memory 会无限重试低信号会话**（P2，5 条评论）  
   当提取 Agent 判断某会话低信号而跳过读取时，该会话不会被标记为已处理，后续会被反复拿出来重试，浪费上下文与成本。  
   🔗 https://github.com/google-gemini/gemini-cli/issues/26522

8. **[#25166] Shell 命令执行完成后卡在 "Waiting input"**（P1，4 条评论）  
   极简单的命令执行完成后 Gemini 仍显示命令运行中，界面停留在等待输入状态，需要人工干预才能继续。该问题高频复现。  
   🔗 https://github.com/google-gemini/gemini-cli/issues/25166

9. **[#26525] Auto Memory 需确定性脱敏并减少日志**（P2，4 条评论）  
   本地转录内容被发送给提取模型时，脱敏发生在内容进入模型上下文之后；同时服务可能记录已有技能等敏感信息，存在隐私风险。  
   🔗 https://github.com/google-gemini/gemini-cli/issues/26525

10. **[#22093] v0.33.0 起子代理在未授权情况下自动运行**（P2，3 条评论）  
    用户明确在配置中禁用 Agents 模式，但升级后 generalist 等子代理仍被自动调用，与预期权限模型不符。  
    🔗 https://github.com/google-gemini/gemini-cli/issues/22093

## 重要 PR 进展

1. **[#28700] 修复“新用户消息被并入未应答工具响应”的 Bug**  
   工具调用被中断（流失败或按 ESC）后，下一条用户消息会被合并进中断轮次，模型误读为待续文本而不是新指令。该修复阻止消息融合，解决模型“替你补全句子”的问题。  
   🔗 https://github.com/google-gemini/gemini-cli/pull/28700

2. **[#19638] 限制搜索工具输出并优化上下文溢出提示**  
   为 SearchText（grep/ripgrep）设置输出上限，避免宽泛查询返回成千上万行导致上下文窗口溢出；同时将警告改为可操作的错误提示。  
   🔗 https://github.com/google-gemini/gemini-cli/pull/19638

3. **[#28673] 新增 Gemini 3.6 Flash 与 3.5 Flash-Lite 模型配置**  
   在 core 包中配置基础模型定义、能力（thinking、multimodalToolUse）、别名与代码执行支持，为后续版本提供新模型接入能力。  
   🔗 https://github.com/google-gemini/gemini-cli/pull/28673

4. **[#28679] 改进 Vertex AI 401 错误提示**  
   当用户使用“顶点 AI 认证”却只配置了标准 API key 时，目前会请求失败且难排查。PR 优化错误信息，引导用户正确配置 GCP 凭证。  
   🔗 https://github.com/google-gemini/gemini-cli/pull/28679

5. **[#28586] 保留 functionCall 中的 thoughtSignature，修复 400 错误**  
   v0.53.0 引入的回归导致并行工具调用时 `thoughtSignature` 被意外剥离，继而触发 400 Bad Request。该修复在序列化过程中保留该字段。  
   🔗 https://github.com/google-gemini/gemini-cli/pull/28586

6. **[#28676] 向 relaunch 子进程转发终止信号**  
   当通过

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-08-07**

## 今日速览

过去 24 小时无新版本发布，社区动态集中于两件事：一是针对 `StrReplaceFile` 破坏非 UTF-8 字节的严重数据损坏问题，同日即有修复 PR 提交（#2594）；二是跨会话记忆系统（#1283）作为最高讨论量的功能提案持续发酵。与此同时，VSCode 插件体验与 CLI 渲染稳定性继续收到开发者反馈。

## 社区热点 Issues

今日共有 8 条活跃 Issue，全部列出：

- **#1283 [feature] Memory System - Persistent context across sessions**（评论 20｜👍 0）
  当前讨论度最高的功能提案，要求实现跨会话持久化记忆，覆盖 AI 自动管理的笔记和用户手动定义的指令。20 条评论说明社区对 Agent 工具上下文连续性的期待很高。
  [查看 Issue](https://github.com/MoonshotAI/kimi-cli/issues/1283)

- **#2591 [bug] StrReplaceFile corrupts undecodable bytes outside the edited region**（评论 1｜👍 0）
  严重数据完整性缺陷：编辑文件时使用 `errors="replace"` 导致编辑区域外的非 UTF-8 字节被静默改写为 `U+FFFD` 并写回磁盘。此问题会永久损坏二进制文件，须优先修复。值得欣慰的是 PR #2594 已在同一天提交。
  [查看 Issue](https://github.com/MoonshotAI/kimi-cli/issues/2591)

- **#2474 [bug] CLI 界面抖动并重新渲染整个对话**（评论 2｜👍

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

## OpenCode 社区动态日报 — 2026-08-07

> 数据来源：github.com/anomalyco/opencode

---

### 1. 今日速览

过去 24 小时无新版本发布，社区讨论集中于**模型路由与上下文窗口争议**（#40409、#40928）、**提供者流异常静默吞错**（#37852）以及**Go 订阅隐私政策回退**（#39875）三件大事。PR 侧则呈现明显的 **TUI 交互打磨**趋势（5 个 UI 修复 PR 同日提交），另有 **Hosted Workspace 执行**（#40784）与 **会话导入/导出**（#40914）两项重量级功能进入代码评审。

---

### 2. 版本发布

过去 24 小时无新 Release。当前版本线：CLI v1.18.14 / V2 next 分支，Desktop v1.18.3。

---

### 3. 社区热点 Issues（Top 10）

**#40409 — OpenCode Go `deepseek-v4-flash` 名不副实，实际返回 V3.2**
👍 高热度 | 评论 13 | 更新于 08-06
用户指控 OpenCode Go Zen API 将 `deepseek-v4-flash` 模型 ID 静默映射到旧版 V3.2（知识截止 2025-05），构成计费与服务质量不匹配。这是模型路由可信度问题，若属实将动摇用户对 Go 订阅的信心。
🔗 https://github.com/anomalyco/opencode/issues/40409

**#37852 — 提供者流中止被记录为“干净停止”，子代理静默返回空结果**
👍 52（本周最高赞）| 评论 11 | 更新于 08-06
当提供者流在无 finish reason / usage chunk 的情况下中断时，opencode 以 `finish=unknown` 和零 token 记入助手消息，随后**正常退出代理循环且不报错**。对于依赖子代理结果的自动化流程，这会导致静默失败，排查极其困难。
🔗 https://github.com/anomalyco/opencode/issues/37852

**#39875 — 要求恢复 Go 隐私措辞与提供商署名，并将遥测写入隐私政策**
👍 44 | 评论 6 | 更新于 08-06
用户指出近两周两个 commit 静默移除了 OpenCode Go 对第三方提供商的归属声明，并请求将新增遥测纳入隐私政策。叠加此前 #39860、#39857 等系列 issue 未获实质回应，社区信任情绪正在累积。
🔗 https://github.com/anomalyco/opencode/issues/39875

**#27906 — v1.15.1+ 破坏 Bun 全局安装**
👍 13 | 评论 22 | 更新于 08-06
新版要求运行 postinstall 生命周期脚本，但 Bun 等非 npm 包管理器默认禁止该行为。影响所有使用 Bun 安装 opencode 的用户，回退版本成为唯一解法。
🔗 https://github.com/anomalyco/opencode/issues/27906

**#32157 — [2.0] 可配置运行中提示投递：queue vs steer，带压缩感知语义**
👍 67（全列表最高赞）| 评论 3 | 更新于 08-06
V2 功能请求：区分“排队”与“打断引导”两类运行中输入，并定义压缩（compaction）期间的语义。点赞数极高但评论稀少，说明需求强烈且设计讨论尚浅。PR #40922（Option+Enter 排队）已部分实现该愿景。
🔗 https://github.com/anomalyco/opencode/issues/32157

**#26195 — `opencode mcp auth` OAuth 流程无法打开浏览器**
👍 11 | 评论 8 | 更新于 08-06
Google Drive MCP 认证时输出 “Authentication successful!” 但浏览器从未打开、token 未保存。MCP 生态的拦路虎，直接影响依赖 GDrive 的开发者。
🔗 https://github.com/anomalyco/opencode/issues/26195

**#38801 — TUI 反复出现 “exiting loop” 消息，治理无果**
评论 21 | 更新于 08-06
用户困扰于 TUI 在切换多种 OpenAI API 时反复进入 `step=80` 循环上限并打印 “exiting loop”。评论数多但点赞少，属于低频但棘手的 TUI 交互缺陷。
🔗 https://github.com/anomalyco/opencode/issues/38801

**#15059 — 多系统提示导致 Qwen3.5-* 模型崩溃**
评论 14 | 更新于 08-06
插件或工具注入额外系统提示时，Qwen3.5 系列直接不工作。已在插件侧修复，但核心应具备最低限度的组合保护。
🔗 https://github.com/anomalyco/opencode/issues/15059

**#24628 — [bug, core] 会话取证静默停止持久化消息**
评论 11 | 更新于 08-06
自 1 月 31 日起 `~/.local/share/opencode/storage/` 不再落盘，尽管 processor 日志正常。数据持久化是核心承诺，静默失效比报错更危险。同日相关 issue #25304 也被顶起。
🔗 https://github.com/anomalyco/opencode/issues/24628

**#40928 — 为何只有 Nemotron 3 Ultra 在免费层保留完整 1M 上下文？**
评论 1 | 创建于 08-06
DeepSeek V4 Flash（原生 1M）被砍到 ~200K，Laguna S 2.1（原生 1M）被砍到 ~270K，而 Nemotron 3 Ultra 却保留完整 1M。模型能力配额的不透明分配引发质疑。
🔗 https://github.com/anomalyco/opencode/issues/40928

---

### 4. 重要 PR 进展（Top 10）

**#40784 — feat(core): 带 modal 驱动的 Hosted Workspace 执行（V2）**
贡献者 PR。Workspace 作为持久执行环境（机器而非仓库），Session 通过现有 runner graph 运行，支持同一套工具与权限。这是 V2 架构的重要拼图。
🔗 https://github.com/anomalyco/opencode/pull/40784

**#40914 — feat(cli): 会话导入与导出**
新增 `SessionTransfer` schema、`GET/POST /api/session/...` 端点及 `opencode2 export/import` 交互命令，导出自动净化敏感信息。直接回应 #36661 类导出失败问题。
🔗 https://github.com/anomalyco/opencode/pull/40914

**#40922 — feat(tui): Option+Enter 排队提示**
Enter 显式打断当前回复；Option+Enter / Alt+Enter 将提示排入队尾，并显示在独立的底部 dock 中而非污染转录区。这是 #32157 功能请求的落地第一步。
🔗 https://github.com/anomalyco/opencode/pull/40922

**#40925 — chore: 提升增量类型检查性能**
为 Effect Drizzle 查询图添加显式方差标注、启用 Core 的持久化增量元数据、使 TUI 消费 Core 声明而非源码。从工程基建层面缩短每次增量编译时间。
🔗 https://github.com/anomalyco/opencode/pull/40925

**#40919 — feat(core): 规范化混合配置格式**
摒弃整文件 V1/V2 检测，改为字段级编码归一化，支持混合 MCP/压缩/实验配置，并容错非法集合条目。解决 V1→V2 迁移期配置兼容性痛点。
🔗 https://github.com/anomalyco/opencode/pull/40919

**#40929 — feat(core): 限制工具输出**
依据 `tool_output` 行/字节限制截断本地工具文本；完整文本保留在受管文件中并 7 天自动清理，`read` 工具增加 `metadata.truncated` 标记。回应长输出撑爆上下文的问题。
🔗 https://github.com/anomalyco/opencode/pull/40929

**#40125 — feat(opencode): 按 MCP 服务器的信任配置**
支持指纹固定（fingerprint pinning）信任特定自签名证书，替代全局 `insecure: true`；`caFile` 处理私有 CA。MCP 安全配置精细化。
🔗 https://github.com/anomalyco/opencode/pull/40125

**#40931 — feat(core): 续跑子代理会话**
为前台子代理增加可选 `sessionID` 输入，保留子会话历史并校验父会话归属与代理身份；`sessionID` 随完成信封返回，拒绝不合规的运行请求。
🔗 https://github.com/anomalyco/opencode/pull/40931

**#40869 — fix(core): 去重 websearch 同意提示**
以进程级信号量串行化 websearch 提供商选择；拿到许可后重新检查已选提供商并退出锁再重试搜索；锁内流程一分钟超时，防止废弃表单阻塞其他搜索。
🔗 https://github.com/anomalyco/opencode/pull/40869

**#40907 — refactor(core): Workers AI 原生路由**
将通用 `@ai-sdk/openai-compatible` 目录条目改走 `opencode-ai/ai/providers/openai-compatible`，为 Cloudflare Workers AI 增加原生 provider 入口，并从配置推导账户 URL。减少对 AI SDK 构造钩子的依赖。
🔗 https://github.com/anomalyco/opencode/pull/40907

> 其他值得留意：#40310（新增 llmgateway-providers）、#27554（LAN 提供商自动发现）、#39206（桌面端 file:// 链接可点击）、#40845（桌面设置重构 beta）、#40925（类型检查性能）。

---

### 5. 功能需求趋势

从全部 Issues 中可提炼出四条主线：

| 方向 | 代表 Issues / PRs | 信号强度 |
|---|---|---|
| **TUI 交互深度打磨** | #40922（排队 vs 打断）、#32954（多技能选择）、#38801（循环消息）、#34078（粘贴两次） | 最高 |
| **运行中提示控制（队列/打断/压缩语义）** | #32157（67👍）、#40922 | 高，点赞数第一 |
| **模型路由与配额透明度** | #40409（模型名实不符）、#40928（上下文长度差异）、#15059（系统提示兼容） | 高 |
| **数据持久化与可迁移性** | #24628（取证失效）、#36661（导出失败）、#40914（导入/导出） | 中高 |
| **隐私与遥测合规** | #39875（44👍）、#39857/#39860 系列 | 中，情绪累积 |

值得注意的冷门信号：**MCP 信任配置**（#40125）与子代理权限细化（#35238）属于安全类需求，尽管讨论量不高，但 PR 已进入实质评审，预计后续迭代重点。

---

### 6. 开发者关注点

**高频痛点：**

1. **提供者错误静默吞掉** — #37852（52👍）揭示“流中断被记录为干净停止”，子代理返回空结果且无任何错误提示。这比报错更让开发者困扰——自动化流程无法区分“真完成”和“被截断”。
2. **Go / Zen 服务可靠性** — #30221（全订阅 “terminated” 错误）、#40409（模型降级）、#40915（连续两日 upstream error），多条独立线路同时指向 OpenCode Go 的稳定性与策略性问题。
3. **安装与升级阻力** — #27906：Bun 用户无法升级到 v1.15.1+，postinstall 脚本是罪魁祸首。包管理器生态的断层对推广有实际影响。
4. **静默数据不落盘** — #24628：会话取证自 1 月底起停止写入，用户直到数周后才发现，且 process 日志一切正常，排查成本极高。
5. **上下文长度配额不透明** — #40928：免费层中同属 1M 上下文的模型被砍至 200–270K，唯独 Nemotron 3 Ultra 保留完整窗口。没有公开的配额规则，用户只能靠猜测。
6. **子代理模型覆盖失效** — #40619：`opencode.json` 中指定的子代理 `model` 字段被忽略，永远回退到主代理模型。配置声明的语义需要立即修正。
7. **Web UI 实时性缺失** — #40502、#40809：Web 端不自动刷新会话列表与新消息，在 Docker 部署场景（Coolify + Traefik + 反向代理）下问题尤甚。
8. **OAuth / MCP 集成阻断** — #26195：`opencode mcp auth gdrive` 输出成功但浏览器从未打开，认证流程名存实亡。

---

*报告生成时间：2026-08-07 · 数据窗口：过去 24 小时 GitHub 更新动态*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-08-07）

## 今日速览

- 昨日发布 `v0.21.6-nightly` 与 `live-host-v0.1.0`，主要涉及测试稳定性与 CI 基础设施改进。
- 安全议题集中爆发：只读 shell 分类器绕过、信任目录边界越权、`.env` 从 DO_NOT_TRUST 祖先目录加载等多项漏洞被披露，对应修复 PR 已进入队列。
- `#3203`（OAuth 免费额度政策调整）以 151 条评论成为社区争议焦点；`0.21.6` 的 hooks 回归问题（#8622）被确认为高优先级缺陷。

---

## 版本发布

### v0.21.6-nightly.20260806.cb3dc107f
包含一项测试稳定性修复：`test(core): deflake glob external-path test`（改用专用空目录，不再复用 `/tmp`）。
▶️ [查看 Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.6-nightly.20260806.cb3dc107f) ｜ [PR #8604](https://github.com/QwenLM/qwen-code/pull/8604)

### live-host-v0.1.0
Qwen Live Host 首个正式版本，随附 CI 改进：Windows merge queue 测试迁移至 ECS 运行，并开始为 GitHub review 准备 evidence-image 工具链。
▶️ [查看 Release](https://github.com/QwenLM/qwen-code/releases/tag/live-host-v0.1.0)

### live-host-latest
稳定版安装源滚动更新。

---

## 社区热点 Issues

### 1. Qwen OAuth 免费额度政策调整（🔥 151 条评论）
**[#3203] [OPEN] [feature-request]** 提议将每日免费请求数从 1,000 次削减至 100 次，并计划在 20XX 年逐步关闭免费入口。评论激烈反对，认为这将严重破坏开发者体验。
▶️ [查看 Issue](https://github.com/QwenLM/qwen-code/issues/3203)

### 2. 0.21.6 回归：核心 hooks 不再触发（P1）
**[#8622] [OPEN] [bug]** `PreToolUse`、`PostToolUse`、`PreCompact`、`SessionStart` 在 0.21.6 中全部失效，仅 `UserPromptSubmit` 和 `Stop` 正常。此前用 `PreToolUse` 做工具调用门控的用户完全失去控制能力，严重影响安全策略落地。
▶️ [查看 Issue](https://github.com/QwenLM/qwen-code/issues/8622)

### 3. Windows 桌面版启动崩溃：`EISDIR lstat 'C:'`（P1）
**[#8615] [OPEN] [bug]** 安装 `Qwen-Code-Desktop_0.1.0_x64-setup.exe` 后，打开工作区即崩溃，bundled runtime 报 `EISDIR lstat 'C:'`。Windows 用户无法正常使用桌面客户端。
▶️ [查看 Issue](https://github.com/QwenLM/qwen-code/issues/8615)

### 4. 只读 shell 分类器可被命令替换绕过（P1，安全）
**[#8582] [OPEN] [bug/security]** `isShellCommandReadOnlyAST` 与运行时替换检测可被行续行符和 `${var@P}` 机制绕过，导致“只读”命令实际执行任意代码并被自动批准，无需二次确认。
▶️ [查看 Issue](https://github.com/QwenLM/qwen-code/issues/8582)

### 5. 信任目录规则被祖先覆盖（P2，安全）
**[#8627] [OPEN] [bug/security]** 当父目录存在 `TRUST_FOLDER` 规则时，显式设置的 `DO_NOT_TRUST` 会被静默覆盖，导致不受信任的工作区可注入 `qwen serve` 的 bearer token。
▶️ [查看 Issue](https://github.com/QwenLM/qwen-code/issues/8627)

### 6. serve 快速路径从不可信祖先加载 `.env`（P2，安全）
**[#8643] [OPEN] [bug/security]** `findEnvFilesFastPath` 只对起始目录评估一次信任状态，然后沿目录树向上加载所有 `.env` 候选文件；一个受信任的子目录可能会吞入来自 DO_NOT_TRUST 祖先的密钥。
▶️ [查看 Issue](https://github.com/QwenLM/qwen-code/issues/8643)

### 7. Anthropic 模型 ID 解析缺陷：`claude-opus-4.8` 被拒，缺少 Opus 5 token 上限（P2）
**[#8584] [OPEN] [bug]** 代码中将点分次要版本（如 `claude-opus-4.8`）解析失败，且 token 上限配置尚未包含 Opus 5，在 LiteLLM/Vertex/Bedrock 等代理场景下会静默降级。
▶️ [查看 Issue](https://github.com/QwenLM/qwen-code/issues/8584)

### 8. 缩小终端窗口导致滚动区内容重复打印（P2）
**[#8557] [OPEN] [bug/ui/rendering]** macOS + Warp 下，窗口变窄时已打印的会话记录会重复堆叠进 scrollback，同一段内容出现多份，干扰阅读。
▶️ [查看 Issue](https://github.com/QwenLM/qwen-code/issues/8557)

### 9. 取消 prompt 后内容不恢复到输入框（UX）
**[#8316] [OPEN] [bug]** 用户在 agent 思考过程中按下 `Ctrl+C`，已输入的内容不会还原到输入框，只能手动重新输入，修改 prompt 的成本很高。
▶️ [查看 Issue](https://github.com/QwenLM/qwen-code/issues/8316)

### 10. 桌面版 UI 语言切换无效（P2，已关闭）
**[#8592] [CLOSED] [bug/ui]** 在设置中切换语言（如简体中文）后，整个界面仍保持英文，选择不生效。同族问题 #8641（原生菜单语言未持久化）也已关闭，预计后续版本修复。
▶️ [查看 Issue](https://github.com/QwenLM/qwen-code/issues/8592)

---

## 重要 PR 进展

### 1. 修复 read-only git 命令可被仓库配置执行任意程序
**[#8645] [OPEN]** `git status/diff/log/show/blame` 等白名单子命令只按命令文本放行，但 git 会执行仓库本地配置中的程序。本 PR 增加二次确认机制。
▶️ [查看 PR](https://github.com/QwenLM/qwen-code/pull/8645)

### 2. 关闭只读分类器行续行与 `${var@P}` 绕过
**[#8590] [OPEN]** 针对 #8582 的修复：AST 分类器不再信任行续行组合后的伪只读命令，运行时替换检测同步增强。
▶️ [查看 PR](https://github.com/QwenLM/qwen-code/pull/8590)

### 3. ACP agent fan-out 并发执行并突破工具调用上限
**[#8631] [OPEN]** 此前 daemon 侧前三轮工具调用串

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*