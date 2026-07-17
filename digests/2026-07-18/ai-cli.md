# AI CLI 工具社区动态日报 2026-07-18

> 生成时间: 2026-07-17 22:36 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-07-18）

## 1. 生态全景

当前 AI CLI 工具赛道正从“能力展示”向“生产可靠性”转型。社区反馈的核心矛盾集中在三个方面：**安全与效率的平衡**（误报/过严导致工作流中断）、**跨平台稳定性**（Windows 性能灾难、macOS 沙箱、Linux 后台 Agent 丢失）、**Agent 行为确定性**（子代理误报状态、无限循环、配置忽略）。与此同时，多工作区 / 多会话编排、MCP 协议标准化、模型 Provider 兼容性成为各工具共同探索的下一个增长点。整体来看，开源生态在快速迭代中暴露出大量“成长痛”，但也驱动着底层架构和安全机制的实质性改进。

## 2. 各工具活跃度对比（2026-07-18）

| 工具 | 当日 Release | 当日新 Issues (Top) | 当日 PR 进展 | 社区热度指标 |
|------|-------------|-------------------|-------------|-------------|
| **Claude Code** | v2.1.212 (功能更新) | 10 条（MCP 连接崩溃、安全误报、后台消息丢失等） | 10 项（安全强化、插件修复、文档纠正） | 高度活跃，Issue 评论多，安全争议议题突出 |
| **OpenAI Codex** | 2 个 Rust alpha 更新（无 changelog） | 10 条（Windows 卡死/HID 枚举/Git 孤立进程） | 10 项（会话管理、插件更新、性能优化） | 社区反应强烈，多个 60+ 赞 Issue，Windows 问题成焦点 |
| **Gemini CLI** | 无 | 10 条（子代理误报成功、无限挂起、命令注入绕过） | 10 项（安全加固 p1，沙箱/变量注入/死锁修复） | 高优安全 PR 密集，社区对 Agent 行为不确定性不满 |
| **GitHub Copilot CLI** | v1.0.72-1（插件标志、路径显示） | 10 条（语音 ASR 失效、Windows 权限、计划模式误判） | 0 项 | 活跃度稳定，Windows 兼容性为最大痛点 |
| **Kimi Code CLI** | 无 | 4 条（Wind 插件内网依赖、PS5.1 崩溃、K2.5 模型保留、TUI 渲染） | 0 项 | 小型社区，企业数据插件兼容性突发问题突出 |
| **OpenCode** | 无正式版（Next 频道测试中） | 10 条（Provider 自动发现、SSH 远程、数据库迁移错误） | 10 项（会话目标、LSP 修复、TUI 插件 API） | v2 兼容性攻坚期，功能请求与 Bug 并重 |
| **Qwen Code** | v0.19.11-nightly（daemon 追踪） | 10 条（多工作区 RFC、VS Code ACP 崩溃、子 Agent 挂起） | 10 项（多模态路由、Web Shell 增强、子 Agent 并发限制） | 多工作区 RFC 讨论热烈，Web Shell 改进快速迭代 |

## 3. 共同关注的功能方向

**3.1 安全策略透明化 & 误报治理**  
- **Claude Code**（Fable 5 分类器误报 `hello` 触发降级）、**Gemini CLI**（命令注入绕过修复、macOS 沙箱对齐）、**GitHub Copilot CLI**（计划模式只读命令误判）。社区共同诉求：允许本地/白名单绕过，提供可审计的决策日志。

**3.2 Agent 行为可靠性 & 错误处理**  
- **Claude Code**（后台 Agent 消息丢失）、**Gemini CLI**（子代理误报成功、Generalist 无限挂起）、**OpenCode**（子代理 Bash 后挂起）、**Qwen Code**（Explore Agent 因 `ask_user_question` 永久等待）。各工具均在通过轮次限制、并发控制和状态劫持自愈。

**3.3 跨平台兼容性（尤其 Windows）**  
- **OpenAI Codex**（Windows 卡死 / HID 枚举 / 周期性挂起）、**GitHub Copilot CLI**（插件权限拒绝、交互空白、会话恢复挂起）、**Kimi Code CLI**（PowerShell 5.1 安装崩溃）、**Qwen Code**（VS Code ACP 进程异常退出）。Windows 成为影响面最大的平台瓶颈。

**3.4 MCP 协议稳定性 & 生态扩展**  
- **Claude Code**（Streamable-HTTP 连接 “client capabilities not available”）、**OpenCode**（MCP 链式调用静默失败、权限 UI 卡死）。MCP 作为工具扩展的核心协议，其连接可靠性、错误处理和权限模型仍需行业级标准化。

**3.5 Provider 兼容与模型切换**  
- **OpenCode**（自动发现本地 OpenAI 兼容模型、xAI Grok 生成无意义命令）、**GitHub Copilot CLI**（Gemini 400 错误）、**Kimi Code CLI**（K2.5 vs K2.6 模型保留诉求）。用户希望更灵活的模型选择自由，避免供应商锁定。

## 4. 差异化定位分析

| 维度 | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | Kimi Code CLI | OpenCode | Qwen Code |
|------|------------|------------|-----------|-----------------|-------------|--------|---------|
| **核心定位** | 企业级安全审查 + MCP 插件生态 | 桌面端对话式编码 + 多平台 IDE | 安全沙箱 + 原生 Bash 亲和力 | 低摩擦 CLI 辅助 + 快速行动 | 中文企业场景 + 数据插件 | 开源 v2 重构 + 多 Provider 兼容 | 高效后端 + 多工作区 + Web Shell |
| **目标用户** | 高安全需求企业 / 审计合规团队 | 独立开发 / 跨平台桌面重度用户 | 对安全极致敏感的 Linux/macOS 开发者 | GitHub 生态用户 / 快速脚本编写者 | 中国量化/金融分析师 | 多模型实战者 / 自定义插件作者 | 团队协作 / 大规模仓库场景 |
| **技术特色** | 严格的 auto-mode 分级；Fable 安全分类器 | Rust 桌面应用；多会话线程；浏览器插件 | macOS Seatbelt 沙箱；变量注入防护 | 插件 / MCP / Skill 声明式集成 | 内置 Wind 等金融数据插件 | 开源、provider-agnostic；TUI 插件 API | daemon 架构；子 Agent 并发限制；Web Shell Git 感知 |
| **当前迭代阶段** | 成熟期（安全策略剧烈调整） | 打磨期（Windows 性能修复优先） | 安全加固期（多枚 p1 PR） | 稳定增长期（增量功能 + 平台兼容） | 早期（基础设施漏洞频发） | 重构期（v2 Next 频道测试） | 快速迭代期（每周 nightly + 密集 PR） |

## 5. 社区热度与成熟度

- **最活跃 / 社区呼声最大**：**Claude Code** 和 **OpenAI Codex** 分别以 Issue 热度和评论数领先。Claude Code 因安全误报引发强烈反弹（多议题获 10+ 评论），OpenAI Codex 因 Windows 卡死问题获 62👍 成为当日最具影响 Issue。
- **快速迭代 / 功能密度高**：**OpenCode**（v2 每日 CI 截图验证）和 **Qwen Code**（每日 nightly + 10 项功能 PR）处于高频开发期，代码活跃度极高。
- **安全前沿**：**Gemini CLI** 当日合并的 PR 全部为高优安全修复（变量注入、沙箱、死锁），体现其对安全的极端重视。
- **创业型 / 小步快跑**：**Kimi Code CLI** 仍处于早期阶段，每日仅 4 个新 Issue，但严重 Bug（Wind 插件内网依赖）暴露了企业级服务外部化的准备不足。
- **成熟但平台痛点**：**GitHub Copilot CLI** 版本号已到 1.0.72，但 Windows 新用户当日遭遇多个阻塞性问题，表明老牌工具在新平台覆盖上仍有盲区。

## 6. 值得关注的趋势信号

**6.1 “安全”正从争论走向工程化落地**  
Claude Code 的 Fable 5 误报、Gemini CLI 的命令注入修复、OpenCode 的权限 UI 卡死——各工具不再停留在“是否安全”的辩论，而是通过**白名单配置、沙箱策略对齐、日志可审计**等方式交付确定性安全机制。开发者应关注自己使用的工具是否提供“可控降级”能力（如 `claude auto-mode reset`）。

**6.2 Windows 平台成为新兴战场**  
OpenAI Codex、GitHub Copilot CLI、Kimi Code CLI 均在同一天暴露出 Windows 特有的致命 Bug（卡死、权限、安装崩溃）。随着 AI CLI 工具向全平台扩展，Windows 的进程管理、HID 设备交互、PowerShell 兼容性将成为重要的技术门槛。对于 Windows 开发者，建议优先选择有明确 Windows 修复计划或已验证版本的工具。

**6.3 多工作区 / 多会话编排是下一个架构级需求**  
Qwen Code 的 #6378 RFC 和 OpenAI Codex 的会话搜索、OpenCode 的 session-to-session messaging 表明，单一工作区的模型已无法满足大型项目协作。未来工具需要支持**独立 daemon 多工作区、子会话状态暴露、跨会话上下文复用**。开发者在选型时可关注工具对 `AGENTS.md` / `GEMINI.md` 等上下文文件的原生支持程度。

**6.4 模型 Provider 中立性成为竞争力**  
OpenCode 的 #6231（自动发现）获得 181 赞，GitHub Copilot CLI 对 Gemini 400 错误的热修，Kimi 用户对 K2.5/2.6 的反复要求——用户不再满足于绑定单一模型。工具若能在不牺牲性能的前提下支持多 Provider 切换、本地推理（LM Studio/Ollama），将在开发者社区中建立更强壁垒。

**6.5 开发者体验从“功能”转向“避险”**  
从常见 Issue 看，用户最在意的不是“能做什么”，而是“会不会中断我的工作”。子 Agent 挂起、自动记忆循环、配置被忽略等 Bug 直接破坏信任。建议开发者在评估工具时，优先检查其**错误恢复机制、轮次硬限制、自动回退方案**等“反脆弱”设计。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（截至 2026-07-18）

数据来源：github.com/anthropics/skills（官方 Skills 仓库），统计范围：PR 前 20 条、Issues 前 15 条。

---

## 1. 热门 Skills 排行

以下 7 个 PR 在高频社区 Issues 中有直接关联，讨论活跃、关注度高，均处于 **Open** 状态。

| 排名 | PR | 功能概要 | 社区讨论热点 | 状态 |
|------|----|----------|--------------|------|
| 1 | [#1298 fix(skill-creator): run_eval.py always reports 0% recall](https://github.com/anthropics/skills/pull/1298) | 修复描述优化循环（run_loop.py）中 recall 恒为 0% 的核心 Bug，包括 Windows 流读取、触发检测、并行 worker 等问题 | 关联 Issues [#556](https://github.com/anthropics/skills/issues/556)（12 评论）、[#1169](https://github.com/anthropics/skills/issues/1169)（3 评论），社区反复报告技能创建工具几乎不可用，是生态底层稳定性需求 | Open |
| 2 | [#514 Add document-typography skill](https://github.com/anthropics/skills/pull/514) | 提供 AI 生成文档的排版质量控制：防止孤词换行、寡妇段落、编号错位 | 排版问题是每个文档任务的刚需，但 PR 长期未合并，社区在 Issues 中多次提及类似“文档质量”诉求 | Open |
| 3 | [#1099 fix(skill-creator): Windows subprocess pipe crash](https://github.com/anthropics/skills/pull/1099) | 修复 Windows 上 `run_eval.py` 因子进程管道读取失败导致每次查询记录为“未触发”的致命问题 | 关联 Issues [#1061](https://github.com/anthropics/skills/issues/1061)（3 评论），Windows 用户不可用，成为阻碍跨平台使用的最大短板 | Open |
| 4 | [#1367 feat: add self-audit skill](https://github.com/anthropics/skills/pull/1367) | 一种输出前审计技能：机械文件验证 + 四维度推理质量门（按损害严重性优先级） | 关联 Issues [#1385](https://github.com/anthropics/skills/issues/1385)（3 评论），社区对 AI 输出质量保障的需求上升，是“安全护栏”方向 | Open |
| 5 | [#525 Add pyxel skill for retro game development](https://github.com/anthropics/skills/pull/525) | 针对 Pyxel 复古游戏引擎的技能，支持编写、运行、截图、迭代流程 | 作者持续更新至 7 月 15 日，游戏开发是创意类 Skills 中具象且热门的垂直场景 | Open |
| 6 | [#1302 Add color-expert skill](https://github.com/anthropics/skills/pull/1302) | 独立颜色专业知识技能：覆盖 ISCC-NBS、Munsell、OKLCH 等命名系统与色彩空间选择 | 社区对特定领域专业知识 Skills（如颜色、排版）的补全需求明显 | Open |
| 7 | [#723 feat: add testing-patterns skill](https://github.com/anthropics/skills/pull/723) | 全面的测试模式技能：涵盖测试哲学、单元测试、React 组件测试、端到端测试等 | 测试是开发者日常高频场景，社区期待规范化 Skills 来提升 Claude 在测试中的行为一致性 | Open |

---

## 2. 社区需求趋势

从 Issues 中可提炼出以下 4 个主要需求方向：

### 🔒 安全与信任边界
- **#492**（34 评论）：社区 Skills 被分发在 `anthropic/` 命名空间下，造成用户误认官方出品，存在提权风险。社区强烈要求建立命名隔离或签名机制。
- **#1175**（4 评论）：处理 SharePoint Online 文档时，将访问控制逻辑写入 SKILL.md 引发安全担忧，期望官方提供安全模式或最优实践指引。

### 🔄 协作与共享
- **#228**（14 评论，👍7）：企业组织内无法直接共享 Skills，需要手动下载传输，官方应提供组织级 Skills 库或直接分享链接。
- **#189**（6 评论，👍9）：`document-skills` 和 `example-skills` 插件安装后内容完全重复，浪费上下文窗口，社区呼吁正式拆分或合并。

### 🪟 跨平台稳定性
- **#1061**（3 评论，👍2）：`skill-creator` 脚本在 Windows 上因 `PATHEXT`、`cp1252` 编码、`select` 管道等问题完全不可用。这与 #556、#1169 共同构成对 `skill-creator` 工具的广泛不满——**当前优化循环在 Windows 上几乎无人能正常工作**。

### 🧩 新技能方向提案
- **#1329**（9 评论）：`compact-memory` — 使用符号符号表示压缩 Agent 长期记忆，减少上下文开销。
- **#412**（6 评论）：`agent-governance` — Agent 系统的安全治理模式：策略执行、威胁检测、信任评分。
- **#1385**（3 评论）：**Reasoning Quality Gate Pipeline** — 预任务校准 → 对抗审查 → 交付验证的三门管线，与 PR#1367 高度呼应。
- **#16**（4 评论）：将 Skills 暴露为 MCP（Model Context Protocol）接口，使其可被其他工具调用。

---

## 3. 高潜力待合并 Skills

以下 Open PR 评论活跃、更新频繁或与高频 Issues 直接挂钩，有较大概率在未来 1-2 个月内合并：

| PR | 理由 | 预估合并概率 |
|----|------|-------------|
| [#1298 run_eval 0% recall 修复](https://github.com/anthropics/skills/pull/1298) | 直接关联 Issues #556（12 评论），是 skill-creator 工具链的阻塞 Bug，社区呼声极高。作者 @MartinCajiao 更新至 6 月 23 日 | ⭐⭐⭐⭐⭐ |
| [#1099 Windows subprocess crash](https://github.com/anthropics/skills/pull/1099) | 与 #1050、#1061 合并可基本解决 Windows 兼容性问题，修复 1 行代码但价值极大 | ⭐⭐⭐⭐ |
| [#525 pyxel skill](https://github.com/anthropics/skills/pull/525) | 作者持续迭代至 7 月 15 日，内容完整，无争议，属于“小而美”的技能 | ⭐⭐⭐⭐ |
| [#1367 self-audit skill](https://github.com/anthropics/skills/pull/1367) | 与 #1385 提案互补，代表社区对输出质量门控的迫切需求 | ⭐⭐⭐ |
| [#514 document-typography](https://github.com/anthropics/skills/pull/514) | 排版问题是通用痛点，PR 已有 4 个月，若官方决定纳入，需尽快决策 | ⭐⭐⭐ |

---

## 4. Skills 生态洞察

> **社区当前最集中的诉求是：修复 skill-creator 工具链的核心稳定性 Bug（尤其是 Windows 支持与 recall 评估），并建立安全的命名空间与组织级共享机制，以释放社区创作 Skills 的生产力；同时，对“推理质量门控”和“专业知识补全”类 Skills 的期待正在快速增长。**

---

好的，这是为您生成的 2026-07-18 Claude Code 社区动态日报。

---

# Claude Code 社区动态日报 | 2026-07-18

## 今日速览

昨日发布的 `v2.1.212` 带来了两个重要变更：`/fork` 命令能力升级，以及新增恢复默认 auto-mode 配置的命令。社区方面，关于 **Streamable-HTTP MCP 连接器**的严重 bug 成为讨论焦点，同时大量关于 **Fable 5 安全分类器误报**的 issue 被标记为已关闭，反映 Anthropic 正在积极处理模型层面的争议问题。

## 版本发布

### v2.1.212

- **`/fork` 命令升级**: 现在执行 `/fork` 会将当前对话复制到一个新的后台会话中（在 `claude agents` 列表中显示为独立行），而不会中断你的当前工作。之前用于启动 in-session 子代理的功能已改为 `/subtask` 命令。
- **新增 `claude auto-mode reset`**: 该命令可将自动模式（auto-mode）配置恢复为默认设置，执行前会进行确认。

## 社区热点 Issues

1.  **[BUG] Streamable-HTTP MCP 连接器导致“客户端能力不可用”严重错误**
    - **Issue**: #78193
    - **摘要**: 当启用远程 Streamable-HTTP MCP 连接器时，Claude Desktop 会持续弹出“Client server capabilities not available”的致命错误提示。问题定位在客户端传输层，而非具体的 MCP 服务端。
    - **社区反应**: 该问题引发了社区的广泛关注（10条评论），说明 MCP 连接的稳定性是影响广泛用户的痛点。
    - **链接**: [https://github.com/anthropics/claude-code/issues/78193](https://github.com/anthropics/claude-code/issues/78193)

2.  **[BUG] 后台 Agent 丢失队列消息并跳过完成通知**
    - **Issue**: #78338
    - **摘要**: 在 Linux 环境下，背景 Agent 会丢失通过 `SendMessage` 排队的消息，并且有时会跳过任务完成的回执通知。该 Issue 由 AI 在受影响的会话中自行发现并撰写。
    - **社区反应**: 作为刚报告的新 Bug，涉及核心的 Agent 消息队列和任务调度机制，值得深度关注。
    - **链接**: [https://github.com/anthropics/claude-code/issues/78338](https://github.com/anthropics/claude-code/issues/78338)

3.  **[BUG] 安全管道全线崩溃的完整记录**
    - **Issue**: #78663
    - **摘要**: 用户详尽记录了在一天内经历的安全审查失败流程：代码审查触发5次误报拒绝、申诉信被系统拦截、CVP申请被模板式拒绝、最终发给用户安全团队的邮件只收到5封自动回复。标志着整个安全审查和申诉管道存在系统性困境。
    - **社区反应**: 作为一个高度详细的端到端报告，它揭示了从模型到人工审查的完整链条均存在问题，社区反响强烈。
    - **链接**: [https://github.com/anthropics/claude-code/issues/78663](https://github.com/anthropics/claude-code/issues/78663)

4.  **[BUG] Fable 5 安全分类器误报 `model_refusal_fallback`**
    - **Issue**: #66657
    - **摘要**: 用户在输入“hello”时，Fable 5 安全分类器错误地触发了 `model_refusal_fallback`，导致模型被静默切换为 Opus 4.8。原因是指纹误将静态请求前缀判定为用户恶意输入。
    - **社区反应**: 该问题及系列相似 Issue（#66595, #66696, #66681等）在今日被批量标记为“已关闭”，表明 Anthropic 已定位并修复了分类器逻辑。这曾是社区对滥用模型降级策略极为不满的核心问题。
    - **链接**: [https://github.com/anthropics/claude-code/issues/66657](https://github.com/anthropics/claude-code/issues/66657)

5.  **[BUG] 长期会话中的时间/日期状态漂移**
    - **Issue**: #66604
    - **摘要**: 在运行数小时甚至跨天的长时间 Claude Code 会话中，AI 助手会丢失当前日期/时间概念。即使在系统提醒消息更新日期后，后续回复仍可能使用错误的“今天/明天”表述。
    - **社区反应**: 该问题对进行大型重构、文档生成等任务的高强度用户影响显著，是长期会话体验的一个重要缺陷。
    - **链接**: [https://github.com/anthropics/claude-code/issues/66604](https://github.com/anthropics/claude-code/issues/66604)

6.  **[BUG] VSCode 扩展首次启动时配置探测子进程超时**
    - **Issue**: #60045
    - **摘要**: 在 VSCode 中打开新的 Claude Code 标签时，扩展会启动一个配置探测子进程，该进程会固定超时60秒，导致初始加载体验极差。
    - **社区反应**: 该问题已标记为“已关闭”，影响了大量 VSCode 用户。
    - **链接**: [https://github.com/anthropics/claude-code/issues/60045](https://github.com/anthropics/claude-code/issues/60045)

7.  **[BUG] 长期被忽视的 Issue 被关闭**
    - **Issue**: #58276
    - **摘要**: 一个从 5 月就存在的严重 Bug：在计划模式（plan mode）下，AI 流式输出会导致 CPU 占用 100% 和 UI 冻结。问题源于自动模式和快速模式在响应式状态中的无限循环。
    - **社区反应**: 该问题历时两月后终于被关闭，对受影响的用户是个好消息。
    - **链接**: [https://github.com/anthropics/claude-code/issues/58276](https://github.com/anthropics/claude-code/issues/58276)

8.  **[BUG] VSCode 中 AWS Bedrock 用户无法连接 Agent 窗口**
    - **Issue**: #59372
    - **摘要**: 当使用环境变量 `CLAUDE_CODE_USE_BEDROCK=true` 通过 AWS Bedrock API 时，VSCode 中的 Agent 窗口（Agent View）无法建立连接。
    - **社区反应**: 对使用自行托管或企业级模型的 Bedrock 用户来说至关重要。
    - **链接**: [https://github.com/anthropics/claude-code/issues/59372](https://github.com/anthropics/claude-code/issues/59372)

9.  **[BUG] Workflow 工具的可恢复缓存无法使用**
    - **Issue**: #63102
    - **摘要**: Workflow 工具的可恢复缓存（`resumeFromRunId`）功能需要前后调用的参数 (`args`) 完全字节一致才能触发。但大语言模型作为调度器时，无法完美转录复杂的 JSON 参数，导致该功能形同虚设。
    - **社区反应**: 开发者认为此功能设计存在缺陷，使其在复杂场景下毫无价值。
    - **链接**: [https://github.com/anthropics/claude-code/issues/63102](https://github.com/anthropics/claude-code/issues/63102)

10. **[BUG] 应用版本与 apt 仓库版本不匹配导致错误更新提示**
    - **Issue**: #66694
    - **摘要**: 通过稳定版 apt 仓库安装 Claude Code 后，用户界面仍会提示更新到最新频道（latest-channel）的版本，造成用户的困惑。
    - **社区反应**: 这是一个典型的用户体验问题，可能导致用户安装不稳定的版本。
    - **链接**: [https://github.com/anthropics/claude-code/issues/66694](https://github.com/anthropics/claude-code/issues/66694)

## 重要 PR 进展

1.  **GCP 网关 Terraform 示例修复与增强**
    - **PR**: #78532
    - **摘要**: 解决了 GCP 网关部署示例中 `PG16` 数据库实例因默认 `ENTERPRISE_PLUS` 版本导致创建失败的问题，并增加了可选的内部负载均衡器（ALB）配置。
    - **链接**: [https://github.com/anthropics/claude-code/pull/78532](https://github.com/anthropics/claude-code/pull/78532)

2.  **强化插件脚本的 YAML、路径和符号链接处理安全**
    - **PR**: #76581
    - **摘要**: 系统性地强化了官方插件脚本，防范 YAML 注入、路径遍历以及符号链接导致的凭据覆写等安全风险。
    - **链接**: [https://github.com/anthropics/claude-code/pull/76581](https://github.com/anthropics/claude-code/pull/76581)

3.  **为 `plugin-dev` 插件补充缺失的清单文件**
    - **PR**: #78446
    - **摘要**: 修复了 `plugin-dev` 是仓库中唯一缺少 `.claude-plugin/plugin.json` 清单文件的插件的 bug，确保其能被正确识别。
    - **链接**: [https://github.com/anthropics/claude-code/pull/78446](https://github.com/anthropics/claude-code/pull/78446)

4.  **纠正插件文档中与源码不符的描述**
    - **PR**: #78445
    - **摘要**: 发现并修正了插件索引和市场中三处插件描述与插件实际功能矛盾的问题，例如 `security-guidance` 插件的 Hook 事件和模式数量描述错误。
    - **链接**: [https://github.com/anthropics/claude-code/pull/78445](https://github.com/anthropics/claude-code/pull/78445)

5.  **修复 DevContainer 脚本的错误处理逻辑**
    - **PR**: #78441
    - **摘要**: PowerShell 脚本中的 `try/catch` 无法捕获原生 CLI 工具（如 `docker`）的非零退出状态。此 PR 修复了`run_devcontainer_claude_code.ps1` 的错误检测机制。
    - **链接**: [https://github.com/anthropics/claude-code/pull/78441](https://github.com/anthropics/claude-code/pull/78441)

6.  **限制代码审查插件为手动调用**
    - **PR**: #78425
    - **摘要**: 通过 `disable-model-invocation: true` 配置，强制 `/code-review` 命令只能由用户手动调用，防止模型或子代理在后台自动触发完整的多代理审查流程。
    - **链接**: [https://github.com/anthropics/claude-code/pull/78425](https://github.com/anthropics/claude-code/pull/78425)

7.  **强化 PR 审查工具包，限制审查者为叶节点 Agent**
    - **PR**: #77427
    - **摘要**: 将 `pr-review-toolkit` 中的代码审查者限制为只能使用仓库检查工具，并禁止其调用其他 Agent 或审查流程，以形成更清晰的权限边界。
    - **链接**: [https://github.com/anthropics/claude-code/pull/77427](https://github.com/anthropics/claude-code/pull/77427)

8.  **强化 `ralph-wiggum` 插件的安全性**
    - **PR**: #78371
    - **摘要**: 为强大的但危险的 `ralph-wiggum` 循环插件增加了安全限制：限制迭代次数、在 `push` / `publish` 前设置确认守护、修复停止钩子。
    - **链接**: [https://github.com/anthropics/claude-code/pull/78371](https://github.com/anthropics/claude-code/pull/78371)

9.  **修复 `EnterWorktree` 工具路径错误**
    - **Issue**: #48967 (已关闭)
    - **摘要**: `EnterWorktree` 工具错误地在 `.claude/` 目录下创建工作树，导致新的会话中斜杠命令和技能无法加载。此 Issue 在近日被关闭。
    - **链接**: [https://github.com/anthropics/claude-code/issues/48967](https://github.com/anthropics/claude-code/issues/48967)

10. **修复 VSCode 集成终端的会话恢复问题**
    - **Issue**: #66618 (已关闭)
    - **摘要**: 提出了关于在 VSCode 集成终端或继承了 Claude Code 环境变量的 Shell 中启动的会话，其 `transcript`/`resume` 功能故障的文档缺失问题。
    - **链接**: [https://github.com/anthropics/claude-code/issues/66618](https://github.com/anthropics/claude-code/issues/66618)

## 功能需求趋势

从近期 Issues 中可以提炼出社区的三大呼声：

- **AI 安全与模型行为控制**：社区核心讨论点不再仅限于“是否安全”，而是“安全策略是否过于严格和不透明”。具体表现为：需要**本地渗透测试**权限、希望禁止安全分类器静默降级模型、以及要求更高透明度的审查和申诉流程。
- **MCP 生态稳定性与可扩展性**：MCP 连接器的可靠性问题（如#78193）是高亮议题。同时，开发者希望获得更精细的控制，比如能够**将特定的子 Agent 路由到不同的 API 端点或 Key**（#66661）。
- **Agent 工作流可靠性**：背景 Agent 任务丢失（#78338）和工作流恢复缓存失灵（#63102）等 Bug 表明，社区对 Agent 执行任务的**确定性、可追溯性和鲁棒性**提出了更高要求。

## 开发者关注点

- **安全沙箱的“反生产力”效应**：大量开发者抱怨 Fable 5 安全分类器过于敏感，在用户进行正当的安全审计或编写安全代码时频繁降级或拒绝服务（如 #78663, #66657, #66595 等）。许多该类型 Issues 被关闭，说明 Anthropic 已采取行动，但社区的负面情绪仍需关注。
- **MCP 连接阵痛**：MCP 协议是 Claude Code 扩展能力的关键，但 `Streamable-HTTP` 连接器的致命 Bug 表明，其稳定性和错误处理机制仍有待完善。
- **后台 Agent 的可靠性**：Agent 在后台运行时消息丢失、任务无法完成的问题（#78338）是影响用户信任的严重缺陷，尤其是在执行长时间、多步骤的任务时。
- **VSCode 体验仍需打磨**：从配置探测子进程超时（#60045）到 AWS Bedrock 用户无法连接 Agent 窗口（#59372），VSCode 插件的稳定性和兼容性问题依然是开发者频繁反馈的点。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

好的，这是为您生成的 2026-07-18 OpenAI Codex 社区动态日报。

---

# OpenAI Codex 社区动态日报 | 2026-07-18

## 今日速览

今日社区焦点集中在 **Windows 桌面应用的性能与稳定性危机**上，多个关于应用卡死、高 GPU 占用和新版本导致无响应的问题集中爆发。与此同时，官方推送了大量面向基础设施优化的 **PR**，涵盖了插件发布、线程搜索、会话管理等核心功能的增强。

## 版本发布

昨日发布了两个 Rust 版本的 alpha 更新，但发行说明为空，无实质性功能变更描述。
- **rust-v0.145.0-alpha.22**: [查看详情](https://github.com/openai/codex/releases/tag/rust-v0.145.0-alpha.22)
- **rust-v0.145.0-alpha.20**: [查看详情](https://github.com/openai/codex/releases/tag/rust-v0.145.0-alpha.20)

## 社区热点 Issues

1.  **#20214：Codex App 在 Windows 11 Pro 上频繁卡顿及白屏**
    - **重要性**: 社区热度最高的问题，虽有充足系统资源，但应用频繁无响应，严重影响了 Windows 用户的核心体验。
    - **社区反应**: 累计获得 62 个👍，45 条评论，足见影响面之广。
    - **链接**: [https://github.com/openai/codex/issues/20214](https://github.com/openai/codex/issues/20214)

2.  **#33780：Windows 应用启动后因 HID 设备枚举卡死**
    - **重要性**: 这是一个新报告且诊断清晰的启动 Bug，当某个 HID 设备无响应时，应用会完全阻塞在“正在加载”状态，无法使用。
    - **社区反应**: 18 条评论，用户希望能有快速修复或 `--disable-hid` 之类的启动参数作为临时方案。
    - **链接**: [https://github.com/openai/codex/issues/33780](https://github.com/openai/codex/issues/33780)

3.  **#33873：更新至最新版后 Codex Desktop 频繁无响应**
    - **重要性**: 表明近期 Windows 版本的更新引入了新的稳定性问题，导致应用在启动后或使用中频繁进入“未响应”状态。
    - **社区反应**: 5 条评论，用户反馈此为全新问题，更新前未见。
    - **链接**: [https://github.com/openai/codex/issues/33873](https://github.com/openai/codex/issues/33873)

4.  **#33884：Windows 版 Codex 进入周期性挂起-恢复循环**
    - **重要性**: 揭示了另一个新的严重 Bug，应用以约 15 秒挂起、10 秒恢复的周期循环工作，几乎无法正常使用。
    - **社区反应**: 3 条评论，开发者正在尝试定位触发条件。
    - **链接**: [https://github.com/openai/codex/issues/33884](https://github.com/openai/codex/issues/33884)

5.  **#17229：Windows 版不断生成孤立的 Git 进程**
    - **重要性**: 这是一个持续存在的资源泄露问题，应用会反复 spawn `git status` 命令并留下孤立进程，长期运行会耗尽系统资源。
    - **社区反应**: 22 条评论，用户强烈要求优化 Git 状态检查的频率。
    - **链接**: [https://github.com/openai/codex/issues/17229](https://github.com/openai/codex/issues/17229)

6.  **#26736：macOS 版 Codex 在窗口可见时 GPU 占用过高**
    - **重要性**: macOS 用户的核心性能痛点，应用窗口只需保持可见就会导致 GPU 占用飙升，影响其他图形密集型任务。
    - **社区反应**: 9 条评论，用户尝试了窗口最小化等临时方法，希望官方优化渲染管线。
    - **链接**: [https://github.com/openai/codex/issues/26736](https://github.com/openai/codex/issues/26736)

7.  **#28919：Windows 版 Codex 缺少“控制其他设备”设置项**
    - **重要性**: 影响了系统间的远程协作功能，Windows 用户无法找到入口来连接和控制其他 Codex 实例，功能不完整。
    - **社区反应**: 16 条评论，23 个👍，是跨设备协作功能的高优先级需求。
    - **链接**: [https://github.com/openai/codex/issues/28919](https://github.com/openai/codex/issues/28919)

8.  **#31836：项目排序功能 Bug**
    - **重要性**: 一个常见的用户体验 Bug，`按最后更新排序` 功能仅在项目组内部生效，而无法对项目组本身进行排序，功能与预期不符。
    - **社区反应**: 22 条评论，用户认为这是一个明显的逻辑错误，影响了项目管理效率。
    - **链接**: [https://github.com/openai/codex/issues/31836](https://github.com/openai/codex/issues/31836)

9.  **#25247：浏览器插件启动失败：“浏览器客户端不被信任”**
    - **重要性**: 阻碍了用户使用 Codex 的浏览器自动化功能，这是一个关键的集成故障。
    - **社区反应**: 14 条评论，问题已持续一段时间，用户期待一个明确的修复方案。
    - **链接**: [https://github.com/openai/codex/issues/25247](https://github.com/openai/codex/issues/25247)

10. **#32791 等：Plus/Pro 账户使用时长限制显示异常**
    - **重要性**: 多个 Issue（如 #32791, #32707, #32635）报告了 5 小时或周使用额度显示丢失或错误的问题，这直接影响了用户对计费和可用服务的判断。
    - **社区反应**: 每个 Issue 都有 3-5 条评论，表明这是一个影响范围广泛的计费系统问题。
    - **链接**: [https://github.com/openai/codex/issues/32791](https://github.com/openai/codex/issues/32791)

## 重要 PR 进展

1.  **#33901：支持 ChatGPT 品牌桌面构建**
    - **重要性**: 解决了 macOS 上 `codex app` 命令可能忽略已安装的 ChatGPT.app 并创建重复 Codex.app 的 bug。现在应用在 macOS 上能同时识别 `Codex` 和 `ChatGPT` 两种命名，提升稳定性。
    - **链接**: [https://github.com/openai/codex/pull/33901](https://github.com/openai/codex/pull/33901)

2.  **#33908：允许通过共享更新发布插件**
    - **重要性**: 为插件生态的自动更新提供了基础，允许 `listed` 状态的插件通过 `share/updateTargets` API 进行更新。
    - **链接**: [https://github.com/openai/codex/pull/33908](https://github.com/openai/codex/pull/33908)

3.  **#33907：为分页线程添加内容搜索功能**
    - **重要性**: 新增实验性的 `thread/searchOccurrences` 方法，允许用户在不回放整个线程的情况下，在分页加载的长对话中进行大小写不敏感的关键词搜索。
    - **链接**: [https://github.com/openai/codex/pull/33907](https://github.com/openai/codex/pull/33907)

4.  **#33895：添加“SessionEnd”钩子以支持线程清理**
    - **重要性**: 为插件和自动化工作流提供了在会话（线程）结束时执行清理或记录操作的能力。
    - **链接**: [https://github.com/openai/codex/pull/33895](https://github.com/openai/codex/pull/33895)

5.  **#31058：修复核心错误：重试模型容量错误**
    - **重要性**: 提升应用健壮性。当 API 因模型容量不足而失败时，不再立即结束对话，而是在 30 秒至 5 分钟内重试最多 3 次，显著改善了高负载时的体验。
    - **链接**: [https://github.com/openai/codex/pull/31058](https://github.com/openai/codex/pull/31058)

6.  **#33906：在远程执行器上启动管理网络代理**
    - **重要性**: 这是一个针对远程执行功能的核心基础设施改进，确保在远程机器上运行的代码能够正常使用本地网络代理。
    - **链接**: [https://github.com/openai/codex/pull/33906](https://github.com/openai/codex/pull/33906)

7.  **#33889：集中管理线程的 MCP 连接**
    - **重要性**: 通过将 MCP（Model Context Protocol）连接集中到 `McpRuntime`，解决了连接竞争或状态不一致的问题，并简化了连接的生命周期管理。
    - **链接**: [https://github.com/openai/codex/pull/33889](https://github.com/openai/codex/pull/33889)

8.  **#33896：公开插件安装的中断要求**
    - **重要性**: 优化了插件的安装流程，允许服务器端告知客户端在安装特定插件时是否需要展示强制性的安装界面。
    - **链接**: [https://github.com/openai/codex/pull/33896](https://github.com/openai/codex/pull/33896)

9.  **#33905：在反向搜索期间批量读取持久化历史**
    - **重要性**: 性能优化。将逐条读取历史记录改为批量读取，显著加快了对长对话历史进行反向搜索的速度。
    - **链接**: [https://github.com/openai/codex/pull/33905](https://github.com/openai/codex/pull/33905)

10. **#33866：移除冗余的工具调度包装器**
    - **重要性**: 代码整洁与性能优化。移除了一个仅做转发而无实际功能的 `ToolRegistry::dispatch_any` 方法，简化了核心工具调度逻辑。
    - **链接**: [https://github.com/openai/codex/pull/33866](https://github.com/openai/codex/pull/33866)

## 功能需求趋势

- **性能与稳定性优化 (紧急)**：这是当前社区最强烈的声音，特别是 Windows 平台。用户迫切要求解决应用卡死、高资源占用和挂起问题。
- **UI/UX 改进**：社区对项目排序、各平台（Windows/macOS）视觉一致性、以及应用内导航流畅度有持续的改进需求。
- **远程协作与设备管理**：用户期望能通过应用无缝控制其他设备上的 Codex 实例，实现分布式工作流。
- **Rate Limit 与计费透明度**：多个 Issue 关注使用额度的显示和计算问题，用户对计费系统的正确性非常敏感。
- **插件与浏览器集成**：插件生态的稳定性和安装流程，特别是与 Chrome 浏览器集成的可靠性，是开发者和重度用户关注的重点。
- **上下文管理与 Hooks**：用户希望有更精细的上下文控制能力（如 pin 重要信息）以及更灵活的钩子系统。

## 开发者关注点

- **Windows 性能灾难**：昨日集中爆发的 Windows 性能 Bug（#33780, #33873, #33884 等）是开发者目前最头疼的问题，直接导致应用无法正常使用。
- **Rate Limit 信息混乱**：作为专业用户，开发者对计费信息的准确性要求极高（#32791, #32707），任何错误的显示都会造成信任危机。
- **多 Git 仓库支持缺失**：许多项目管理复杂，希望 Codex 能原生支持包含多个独立 Git 仓库的工作区（#26338），但目前支持不足。
- **浏览器插件信任问题**：`browser-client is not trusted` 错误（#25247）是一个明确的集成障碍，让依赖此功能的开发者感到挫败。
- **macOS GPU 占用过高**：对于在 Mac 上进行开发或运行其他图形应用的开发者，Codex 窗口保持可见就会消耗大量 GPU 资源，影响多任务效率。
- **TUI 协作模式不完善**：CLI 用户在界面提示（如协作模式指示器）和钩子系统（如 `systemMessage` 强制为 `warning` 级别）上体验不佳。
- **“控制其他设备”功能缺失**：Windows 版缺失此功能（#28919）限制了跨平台工作流。
- **频繁更新引入新问题**：从多个报错看，最新的 Windows 版本更新并未解决旧疾，反而引入了新的严重卡顿和周期性问题。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

好的，以下是 2026 年 7 月 18 日的 Gemini CLI 社区动态日报。

---

# Gemini CLI 社区动态日报 | 2026-07-18

## 今日速览

社区开发重点聚焦于安全加固与 Agent 可靠性。多枚高优 PR 正在修复命令注入绕过漏洞、macOS 沙箱权限过于宽松以及核心推理循环死锁等问题。同时，社区对 Agent 的行为（如子代理错误报告成功、无缘无故挂起）表达了强烈不满。

## 社区热点 Issues

1.  **[Bug] 子代理达到最大轮次后错误报告为“成功”**
    *   **Issue:** [#22323](https://github.com/google-gemini/gemini-cli/issues/22323)
    *   **重要性：** 这是一个严重的用户体验问题。当子代理因达到最大执行轮次 (MAX_TURNS) 而中断时，它没有被正确报告为“超时”或“失败”，而是被标记为“成功 (GOAL)”。这会让用户误以为任务已完成，但实际上没有进行任何实质分析，严重削弱了对 Agent 可靠性的信任。社区对此反应强烈（11 条评论，2 个赞）。

2.  **[Bug] Generalist Agent 无限期挂起**
    *   **Issue:** [#21409](https://github.com/google-gemini/gemini-cli/issues/21409)
    *   **重要性：** 当 Gemini CLI 将任务委托给通用的 `generalist` Agent 时，会无限期挂起，简单的任务（如创建文件夹）都无法完成。用户只能通过明确指示模型不要使用子代理来规避此问题。这个问题获得了社区 8 个赞，是目前影响范围最广的 bug 之一。

3.  **[Bug] Shell 命令执行完成后卡死在“等待输入”状态**
    *   **Issue:** [#25166](https://github.com/google-gemini/gemini-cli/issues/25166)
    *   **重要性：** 用户反复遇到在执行非常简单的 Shell 命令（如 `ls`）后，CLI 界面仍然显示“等待用户输入”，导致工具挂起。这是一个高频且影响开发流畅性的核心问题，获得了 3 个赞。

4.  **[需求] 利用模型的原生 Bash 亲和力实现无依赖沙箱**
    *   **Issue:** [#19873](https://github.com/google-gemini/gemini-cli/issues/19873)
    *   **重要性：** 这是一个长期的功能需求，提议利用 Gemini 模型作为“原生 Bash 用户”的能力。通过创建零依赖的操作系统沙箱（如 macOS Seatbelt），在保证安全的同时，充分发挥模型直接使用 `grep`, `sed` 等 POSIX 工具进行代码探索和编辑的能力。

5.  **[Bug] 模型随机创建临时脚本造成工作区污染**
    *   **Issue:** [#23571](https://github.com/google-gemini/gemini-cli/issues/23571)
    *   **重要性：** 模型在通过 Shell 执行代码时，倾向于在各种目录下生成临时的编辑脚本。这给用户的 Git 提交和工作区清理带来了巨大麻烦。该问题反映了 Agent 在文件操作层面的“不文明”行为。

6.  **[Bug] 浏览器 Agent 忽略 settings.json 中的配置覆盖**
    *   **Issue:** [#22267](https://github.com/google-gemini/gemini-cli/issues/22267)
    *   **重要性：** 用户发现，无论在全局还是项目级别的 `settings.json` 中配置参数（如 `maxTurns`），浏览器 Agent 都会完全忽略。`AgentRegistry` 虽然正确读取了配置，但 Agent 在执行时未应用，导致用户无法精细控制 Agent 行为。

7.  **[Bug] 超过 128 个工具时遇到 400 错误**
    *   **Issue:** [#24246](https://github.com/google-gemini/gemini-cli/issues/24246)
    *   **重要性：** 当可供调用的工具（如各种 Skill、Sub-agent）数量超过 400 个时，CLI 会直接返回 400 错误。这提示了工具选择机制的瓶颈，用户希望 Agent 能更智能地筛选当前任务所需的工具集合。

8.  **[Bug] AST 意识文件读取的评估影响**
    *   **Issue:** [#22745](https://github.com/google-gemini/gemini-cli/issues/22745)
    *   **重要性：** 这是一个探索性的大主题，旨在评估引入抽象语法树（AST）感知的文件读写和搜索功能。如果实现，可以让模型更精确地读取方法级别代码，减少 API 调用轮次，并更有效地理解代码库结构，是提升 Agent 代码理解能力的关键方向。

9.  **[Bug] (子)Agent 在 v0.33.0 后未经许可自动运行**
    *   **Issue:** [#22093](https://github.com/google-gemini/gemini-cli/issues/22093)
    *   **重要性：** 用户发现，在升级到 v0.33.0 后，即使所有配置都已禁用 Agent 模式，子代理（如 generalist）仍会未经许可自动运行。这引发了用户对工具自主性的担忧，并可能造成意外的资源消耗或安全风险。

10. **[Bug] 自动记忆系统重复处理低质量会话**
    *   **Issue:** [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)
    *   **重要性：** 自动记忆（Auto Memory）功能存在一个 bug：当提取 Agent 认为某个会话“信号低”而决定不读取时，该会话仍会被标记为“未处理”，导致它反复出现在待处理队列中，造成系统资源的浪费和潜在的无限重试循环。

## 重要 PR 进展

1.  **[PR #28429] 缓解无限 ReAct 循环和提示注入攻击**
    *   **链接:** [#28429](https://github.com/google-gemini/gemini-cli/pull/28429)
    *   **重要性：** **高优 (p1)**。此 PR 通过引入会话级默认轮次限制（15次）和增强的简化工具循环检测启发式算法，来防御由恶意工作区文件（间接提示注入）引发的无限推理循环和配额耗尽攻击。这是针对最近社区关注的安全问题的直接响应。

2.  **[PR #28424] 对齐 macOS 宽松沙箱配置**
    *   **链接:** [#28424](https://github.com/google-gemini/gemini-cli/pull/28424)
    *   **重要性：** **高优 (p1)**。更新了 macOS 的 Seatbelt 沙箱配置，使“宽松”模式也遵循“默认拒绝”的安全模型，与“严格”模式保持一致。这将大大提升工具在 macOS 上的默认安全基线。

3.  **[PR #28403] 修复变量扩展绕过安全检查的漏洞**
    *   **链接:** [#28403](https://github.com/google-gemini/gemini-cli/pull/28403)
    *   **重要性：** **高优 (p1)**。修复了 `detectBashSubstitution()` 函数中的一个不完整检查，该漏洞允许 `$VAR` 和 `${VAR}` 等变量扩展模式绕过已有的安全门禁。此 PR 还增强了工作流的安全性。

4.  **[PR #28164] 限制单次用户请求的递归推理轮次**
    *   **链接:** [#28164](https://github.com/google-gemini/gemini-cli/pull/28164)
    *   **重要性：** 此 PR 在核心推理引擎中强制执行了严格的递归推理轮次限制（默认 15 次/用户请求）。这是阻止模型陷入无限循环、保护用户本地 CPU 资源和 API 配额的关键修复，解决了社区最紧迫的痛点之一。

5.  **[PR #28346] 修复可运行钩子的信任对话框泄露问题**
    *   **链接:** [#28346](https://github.com/google-gemini/gemini-cli/pull/28346)
    *   **重要性：** **高优 (p1)**。修复了文件夹信任发现机制中的一个 bug，该 bug 可能导致错误的、无效的钩子条目被报告为可执行命令，向用户显示不准确的安全提示。

6.  **[PR #28386] 修复 VS Code 扩展中激活资源的正确追踪**
    *   **链接:** [#28386](https://github.com/google-gemini/gemini-cli/pull/28386)
    *   **重要性：** **高优 (p2)**。修复了 VS Code 插件激活路径中的一个 JS 逗号表达式错误，该错误导致多个 Disposable 对象未被正确追踪，可能引起资源泄露或功能异常。

7.  **[PR #28330] 原子化设置 Token 文件权限，修复 TOCTOU 窗口**
    *   **链接:** [#28330](https://github.com/google-gemini/gemini-cli/pull/28330)
    *   **重要性：** **高优 (p2)**。修复了 IDE 服务器中写入认证 Token 文件时的“检查时间-使用时间”（TOCTOU）竞态条件。原代码在 `writeFile` 和 `chmod` 之间存在时间窗口，可能导致 Token 被短暂暴露。

8.  **[PR #28240] 默认支持 AGENTS.md 上下文文件**
    *   **链接:** [#28240](https://github.com/google-gemini/gemini-cli/pull/28240)
    *   **重要性：** 修复了 `AGENTS.md` 文件默认被忽略的问题，除非用户明确在配置中列出。此 PR 将其与 `GEMINI.md` 一同作为默认上下文文件，提升了工具的开箱即用体验。

9.  **[PR #28275] 使 GCP 遥测导出器变为可选**
    *   **链接:** [#28275](https://github.com/google-gemini/gemini-cli/pull/28275)
    *   **重要性：** **高优 (p3)**。将 Google Cloud 的日志、监控和链路追踪导出器移出核心运行时依赖，使其变为可选。这简化了非 GCP 用户或不想使用 GCP 监控功能的用户的部署和依赖管理。

10. **[PR #20238] 修复反病毒软件对 JSON 错误报告的误报**
    *   **链接:** [#20238](https://github.com/google-gemini/gemini-cli/pull/20238)
    *   **重要性：** 将 CLI 生成的错误报告从系统临时目录 (`/tmp`) 移动到专用的 `~/.gemini/tmp/` 目录下。这解决了部分反病毒软件将错误报告文件标记为恶意代码的问题。

## 功能需求趋势

*   **安全与沙箱：** 社区对安全性的关注度极高，尤其是 macOS 沙箱（Seatbelt）和命令注入防护。从 Issue 到 PR，大量工作都围绕在允许模型执行复杂 Bash 命令（利用其原生能力）和确保用户系统安全之间取得平衡。
*   **Agent 的自我认知与行为控制：** 用户不再满足于 Agent 能够“做”，更希望 Agent 能够“说清楚”和“可控制”。相关需求包括：Agent 能准确解释 CLI 标志和热键 (#21432)、子代理轨迹对用户可见 (#22598)、以及阻止模型执行破坏性操作（如危险的 git 命令）(#22672)。
*   **代码理解能力的进化：** 社区普遍认为单纯的文本模式匹配已经不够。评估引入 AST 感知的文件读取、代码库映射 (#22745, #22746) 的需求日益增长，这将是提升 Agent 处理复杂代码库能力的关键。
*   **评估（Eval）与质量保障：** 随着 Agent 能力增强，如何系统性地评估其行为成为了焦点。社区正在推动建立更强的组件级评估体系 (#24353)，并出现了专门的 PR 来创建评估文件验证工具 (#28344)，显示出对质量控制的强烈需求。

## 开发者关注点

*   **Agent 行为的不确定性：** 最大的痛点是 Agent 行为不可预测。**子代理错误报告成功** (#22323)、**Generalist Agent 挂起** (#21409)、**自动使用未授权的 Agent** (#22093) 等问题都指向一点：Agent 的决策过程像“黑盒”，不可信赖。
*   **资源与效率问题：** **无限循环**和**Shell 命令卡死** (#25166) 是开发者最难以忍受的问题，因为它直接导致工作流程中断、浪费时间和 API 配额。同时，**模型随机创建临时文件** (#23571) 和**自动记忆系统重复重试** (#26522) 也造成了不必要的清理和资源开销。
*   **配置与自定义的冲突：** **settings.json 配置被 Agent 忽略** (#22267) 是一个典型的配置生效问题，开发者对工具的精细控制能力受阻，信任感下降。
*   **安全感知的“过”与“不及”：** 安全问题呈现两极分化。一方面，存在像**变量扩展绕过**的高危漏洞；另一方面，**反病毒软件对临时文件的误报** (#20238) 又影响了正常使用流程。开发者希望安全机制既能“防得住”，又能“不添乱”。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 | 2026-07-18

## 今日速览
- 项目发布 v1.0.72-1，新增插件、MCP 及技能相关 CLI 标志，同时改进了文件路径显示与计划审批确定性。
- 社区活跃度持续走高，过去 24 小时内新增/更新 23 条 Issue，其中 Windows 平台插件安装失败、语音模式 ASR 全模型静默失败、Gemini 模型 400 错误等问题成为关注焦点。
- 功能需求集中在权限精细化、模型兼容性扩展、会话状态可视化及终端交互改进上，开发者对计划模式误判和进程管理的抱怨较为突出。

---

## 版本发布

### v1.0.72-1
**Added**
- 新增 `--plugin`、`--mcp`、`--skill` 标志，支持插件相关变更操作。
- 为 `copilot plugins remove --skill` 添加技能移除能力。

**Improved**
- 展开紧凑编辑行时，现在会显示完整文件路径。
- 计划审批菜单的显示顺序在不同模型间保持一致。
- `/add-dir` 目录保持可见。

---

## 社区热点 Issues（挑选 10 条）

1. **#4024 – 语音模式：所有捆绑 ASR 模型静默失败**  
   - 重要性：核心语音功能完全不可用，影响所有语音用户。  
   - 社区反应：12 条评论，作者深入分析了 `MultiModalProcessor` 路由缺陷，涉及 `nemotron_speech` 模型。  
   - 链接：https://github.com/github/copilot-cli/issues/4024

2. **#3767 – 附件过大永久卡死会话（5MB CAPI 限制，无恢复机制）**  
   - 重要性：一旦触发，会话不可恢复，影响工作流连续性。问题已关闭但修复待验证。  
   - 社区反应：7 条评论，用户期待回收或降级机制。  
   - 链接：https://github.com/github/copilot-cli/issues/3767

3. **#3762 – `contextTier` 配置选项无效**  
   - 重要性：长上下文模型选择配置被忽略，用户需手动重选。  
   - 社区反应：6 条评论，开发者希望明确配置生效逻辑。  
   - 链接：https://github.com/github/copilot-cli/issues/3762

4. **#4151 – Windows 插件安装始终报“Access is denied”**  
   - 重要性：Windows 用户完全无法安装任何来源的插件，影响范围大。  
   - 社区反应：3 条评论，复现率高，涉及权限问题。  
   - 链接：https://github.com/github/copilot-cli/issues/4151

5. **#4160 – 计划模式过度阻止只读 Shell 命令（关键字误匹配）**  
   - 重要性：破坏计划模式可用性，用户被迫手动绕过。  
   - 社区反应：3 条评论，开发者详细分析了分类器基于子串而非语义的缺陷。  
   - 链接：https://github.com/github/copilot-cli/issues/4160

6. **#4158 – 暴露子会话的队列与活跃处理状态**  
   - 重要性：项目会话协调 API 缺乏子会话状态，导致父级无法判断进度。  
   - 社区反应：2 条评论，用户认为这是多会话工作流的关键缺失。  
   - 链接：https://github.com/github/copilot-cli/issues/4158

7. **#4163 – copilot CLI 1.0.71 未回收子进程，僵尸进程累积**  
   - 重要性：影响系统资源，长期运行后可能耗尽 PID。  
   - 社区反应：1 条评论，已量化每分钟产生约 2 个僵尸进程。  
   - 链接：https://github.com/github/copilot-cli/issues/4163

8. **#4116 – 复制输入框文本时包含左边框装饰符**  
   - 重要性：UI 细节问题，污染粘贴内容，降低日常体验。  
   - 社区反应：1 条评论，获得 1 个赞，用户希望快速修复。  
   - 链接：https://github.com/github/copilot-cli/issues/4116

9. **#4155 – Gemini 模型返回 400 Bad Request**  
   - 重要性：Google Gemini 模型完全不可用，影响多模型用户。  
   - 社区反应：0 条评论，但提供了完整复现步骤和错误 ID。  
   - 链接：https://github.com/github/copilot-cli/issues/4155

10. **#4150 – permissions-config.json 中带空格命令仍需审批**  
    - 重要性：权限白名单配置不符合预期，`make fix` 等命令无法自动允许。  
    - 社区反应：0 条评论，用户指出 `make` 单独配置有效，但组合命令失败。  
    - 链接：https://github.com/github/copilot-cli/issues/4150

---

## 重要 PR 进展

过去 24 小时内无新 Pull Request 更新或合并。

---

## 功能需求趋势

从近期 Issue 中提炼出社区最关注的功能方向：

1. **权限系统精细化**  
   - 要求支持命令路径前缀（#4157）、带空格命令白名单（#4150）、 `git branch -D` 等操作的正确分类（#4156）。

2. **模型兼容性扩展**  
   - 增加对 Gemini 模型的支持（#4155）、允许本地模型使用 `-max-ai-credits=0`（#4167）、禁用低信用警告（#4168）。

3. **会话状态与任务管理可视化**  
   - 暴露子会话处理/队列状态（#4158）、改进计划审批菜单确定性（v1.0.72-1 已部分改善）。

4. **Windows 平台稳定性**  
   - 修复插件安装权限（#4151）、交互模式空白（#4159）、 `--resume` 挂起（#4165）。

5. **终端交互体验**  
   - 添加 `j/k` 导航支持（#4152）、修复文本复制问题（#4116、#4154）。

6. **进程与资源管理**  
   - 修复僵尸进程泄漏（#4163）、优化附件大小提示重复（#4164）。

---

## 开发者关注点

- **Windows 兼容性阵痛**：插件安装、交互模式空白、会话恢复挂起等问题同时爆发，Windows 用户受影响严重。
- **计划模式假阳性**：只读命令被误判为危险操作，频繁打断工作流。
- **关键功能不可用**：语音 ASR 全模型失效、Gemini 400 错误、长上下文配置不起作用——三者均为破坏性 Bug。
- **会话灾难恢复缺失**：附件超限后无降级或回退机制，永久卡死会话；僵尸进程累积无自动清理。
- **配置行为不符合预期**：`contextTier`、权限白名单中的空格命令均未按文档工作，降低用户信任。
- **小型但恼人的 UI 问题**：复制含边框字符、重复警告提示、无法选择 TUI 文本等，影响日常效率。

> 日报数据来源：https://github.com/github/copilot-cli

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 | 2026-07-18

## 今日速览
昨日（7月17日）Kimi Code CLI 无新版本发布，但社区提交了 4 个新 Issue，其中 **Wind 插件因依赖指向内网完全不可用** 和 **Windows PowerShell 5.1 安装脚本崩溃** 是影响用户直接使用的严重问题；另外，用户对 **K2.5 模型保留** 的呼声仍在持续，TUI 的 Markdown 渲染 Bug 也值得关注。

---

## 版本发布
无

---

## 社区热点 Issues
（过去 24 小时内更新，共 4 条，全部列出）

### 1. [Wind 插件] 依赖安装指向内网，公网用户无法使用 [#2505]  
**作者**：@Steven-DD  
**摘要**：Kimi Work 桌面端 Wind 数据插件（`wind-allskill`）所有取数调用失败，根因是网关客户端 SDK `agent-gw-pysdk` 未随插件安装，而安装指引指向 Moonshot 内网 Git 服务器 `dev.msh.team`（公网不可达），导致插件完全不可用。  
**重要性**：严重阻塞依赖 Wind 数据的企业用户，属于 **功能阻断级 Bug**，需紧急修复依赖分发方式（如提供公网镜像或内置 SDK）。  
**链接**：https://github.com/MoonshotAI/kimi-cli/issues/2505

### 2. [BUG] install.ps1 在 Windows PowerShell 5.1 中崩溃 [#2504]  
**作者**：@lyp1938  
**摘要**：运行 `irm https://code.kimi.com/kimi-code/install.ps1 | iex` 安装 CLI 时，在 PowerShell 5.1 下因 `Invoke-WebRequest` 内部索引越界导致安装失败（目标版本 0.26.0）。  
**重要性**：影响仍使用旧版 PowerShell 的大量 Windows 开发者，属于 **平台兼容性 Bug**，需适配 5.1 或更新安装文档。  
**链接**：https://github.com/MoonshotAI/kimi-cli/issues/2504

### 3. [Enhancement] 请求支持 Kimi K2.5 模型及旧版系统提示词 [#1925]  
**作者**：@herrbasan  
**摘要**：用户认为 K2.6 模型过度思考抑制创造力、增加幻觉、失去个性，强烈要求允许切换回 K2.5 并使用旧版 system prompt。该 Issue 自 4 月提交以来已获 13 条评论，社区讨论活跃但官方尚未回应。  
**重要性**：反映资深用户对模型行为偏好的刚性需求，长期未解决可能导致用户流失。  
**链接**：https://github.com/MoonshotAI/kimi-cli/issues/1925

### 4. [BUG] TUI 中 Markdown 列表项换行时字符丢失或单词分裂 [#2379]  
**作者**：@bdragan  
**摘要**：在终端 UI（TUI）中使用 K2.6 模型输出时，渲染 Markdown 列表遇到换行会出现字符丢失或单词分裂现象（Linux 6.8.0，CLI 1.45.0）。  
**重要性**：影响终端阅读体验，属于 **显示渲染回归**，需修复以保持输出一致性。  
**链接**：https://github.com/MoonshotAI/kimi-cli/issues/2379

---

## 重要 PR 进展
过去 24 小时内无合并或更新的 Pull Request。

---

## 功能需求趋势
根据近期 Issue 分析，社区关注的核心方向包括：

- **模型选择与版本控制**：用户期望能自由切换 K2.5 / K2.6 模型，以适配不同场景（创造力 vs 精确度），#1925 持续 3 个月仍为 Open 状态，呼声较高。
- **企业级数据插件兼容性**：Wind 等插件的依赖管理需支持公网安装，避免内网地址泄露或不可达问题。
- **跨平台安装可靠性**：Windows 旧版 PowerShell、Linux 发行版差异导致的安装失败是基础体验痛点。
- **终端 UI 渲染一致性**：Markdown 列表、代码块、换行等元素的准确显示需持续优化。

---

## 开发者关注点
- **痛点**：
  - Wind 插件依赖 `agent-gw-pysdk` 指向内网 Git 服务器，公网用户根本无法安装，属于内部工具外部化时的网络隔离失误。
  - Windows PowerShell 5.1 安装脚本崩溃，降低 Windows 新用户转化率，建议使用更兼容的下载方式（如 `curl.exe` 或二进制包）。
  - K2.6 模型“过度思考”导致输出质量下降，部分用户认为其“失去了个性”，期望保留旧模型作为备选。
- **高频需求**：
  - 模型切换功能（#1925）已持续 3 个月，社区希望得到官方明确规划。
  - TUI 渲染 Bug（#2379）影响日常使用，建议优先修复。
  - 安装文档和脚本需简化网络依赖，避免内网地址泄漏或硬编码不可达域名。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

好的，各位开发者，早上好！这里是 2026 年 7 月 18 日的 OpenCode 社区动态日报。

---

## 📰 今日速览

1.  **OpenCode v2 兼容性攻坚**：v2 版本（Next 频道）依然是社区讨论焦点，集中暴露了与自定义 OpenAI 兼容 provider、插件系统以及配置迁移相关的多项关键 Bug，社区正在积极配合复现与修复。
2.  **模型 Provider 生态扩展**：社区对“自动发现本地 OpenAI 兼容 Provider 模型”的需求呼声极高（👍181），同时 KIMI K3、xAI Grok 等新模型在集成过程中也报出了特有的工具调用和计费问题。
3.  **布局与 SSH 远程访问成为高频需求**：“保留经典布局”与“SSH 远程连接”两个功能 Request 长期霸榜，体现了用户对新版 UI 的反馈和对远程开发场景的迫切需求。

## 📦 版本发布

今日暂无正式版本发布。项目在持续通过 CI 流程进行 PR 的截图验证（如 `pr-37526-screenshots` 等），确保界面改动符合预期。v2 Next 频道 (`opencode2 v0.0.0-next-15747`) 处于活跃开发测试中。

## 🔥 社区热点 Issues（Top 10）

1.  **[#6231] 自动发现 OpenAI 兼容 Provider 的模型列表** 💬 21 | 👍 181
    - **重要性**: 核心体验优化。用户希望对于 LM Studio、Ollama 等本地 provider，能自动拉取模型列表，而非手动在配置中逐一填写，避免繁琐和错误。
    - **链接**: [https://github.com/anomalyco/opencode/issues/6231](https://github.com/anomalyco/opencode/issues/6231)

2.  **[#7790] [Feature] 为桌面版添加 SSH 远程连接支持** 💬 15 | 👍 73
    - **重要性**: 高优功能请求。许多开发者在服务器上工作，社区强烈希望 OpenCode Desktop 能像 VS Code Remote SSH 一样，直接连接远程服务器上的 opencode 服务。
    - **链接**: [https://github.com/anomalyco/opencode/issues/7790](https://github.com/anomalyco/opencode/issues/7790)

3.  **[#31119] [Bug] 数据库报错："no such column: name"** 💬 13 | 👍 11
    - **重要性**: 严重 Bug。从旧版本升级后，应用因数据库 Schema 不匹配而完全无法使用，阻塞用户正常工作和开发流程。
    - **链接**: [https://github.com/anomalyco/opencode/issues/31119](https://github.com/anomalyco/opencode/issues/31119)

4.  **[#37012] [Feature] 保留经典布局选项** 💬 13 | 👍 16
    - **重要性**: UI/UX 争议焦点。部分用户反映新版布局（1.18.3）操作路径变长，强烈要求保留旧版多窗口/工作区的便捷操作体验。
    - **链接**: [https://github.com/anomalyco/opencode/issues/37012](https://github.com/anomalyco/opencode/issues/37012)

5.  **[#31041] [Bug] Zen API CORS 预检请求返回 404** 💬 10 | 👍 10
    - **重要性**: 影响所有基于浏览器的客户端。CORS 配置问题导致前端应用完全无法调用 Zen API 端点，这是一个协议层的阻断性 Bug。
    - **链接**: [https://github.com/anomalyco/opencode/issues/31041](https://github.com/anomalyco/opencode/issues/31041)

6.  **[#33998] [Bug] GLM-5.2 Prompt Cache 异常降低** 💬 10
    - **重要性**: 推理成本与性能问题。提示缓存随机掉落到极低水平（~500 token），即使系统提示完全相同，这将显著增加 API 调用成本和延迟。
    - **链接**: [https://github.com/anomalyco/opencode/issues/33998](https://github.com/anomalyco/opencode/issues/33998)

7.  **[#33028] [Bug] 子代理在调用 Bash 工具后无限挂起** 💬 6 | 👍 3
    - **重要性**: 工作流稳定性。这是开发流程中的关键断路问题，子代理执行简单命令后无法返回，导致整个对话/任务卡死，严重影响日常开发。
    - **链接**: [https://github.com/anomalyco/opencode/issues/33028](https://github.com/anomalyco/opencode/issues/33028)

8.  **[#34652] [Bug] 嵌套数组参数导致 SchemaError (Anthropic Provider)** 💬 5
    - **重要性**: Provider 兼容性问题。当 Anthropic 模型返回 JSON 字符串形式的数组参数时，工具调用会直接失败。这导致了特定模型（如 `todowrite`）功能失效。
    - **链接**: [https://github.com/anomalyco/opencode/issues/34652](https://github.com/anomalyco/opencode/issues/34652)

9.  **[#35403] [Bug] 插件版本落后导致 "no such column: replacement_seq"】 ** 💬 2 | 👍 2
    - **重要性**: 数据库版本管理问题。CLI 自动升级后，数据库迁移未同步，导致使用旧版插件的用户在执行子代理任务时立即崩溃。
    - **链接**: [https://github.com/anomalyco/opencode/issues/35403](https://github.com/anomalyco/opencode/issues/35403)

10. **[#37399] [Bug] xAI Grok 4.5 生成大量无用的 `true` 命令** 💬 3
    - **重要性**: 模型行为问题。该模型错误地持续执行返回无输出的 `true` 命令，浪费 token 并影响对话流，需要针对性 prompt 优化。
    - **链接**: [https://github.com/anomalyco/opencode/issues/37399](https://github.com/anomalyco/opencode/issues/37399)

## 🔗 重要 PR 进展（Top 10）

1.  **#37477** - **[Bug fix]** `fix: don't boot a full instance for session list`: 优化性能，修复 `session list` 命令会启动完整应用实例的 Bug，现在直接查询数据库，速度快得多。
    - [PR 链接](https://github.com/anomalyco/opencode/pull/37477)

2.  **#36710** - **[Bug fix]** `fix(core): bound event log compaction`: 增加事件日志的边界和清晰的状态显示，并提供安全（dry-run）的压缩命令，防止数据库无限膨胀。
    - [PR 链接](https://github.com/anomalyco/opencode/pull/36710)

3.  **#32743** - **[Feature]** `feat(session): native per-session goals`: 引入原生对话目标功能，支持 `/goal` 命令，可设置、追踪和自动推进开发目标。
    - [PR 链接](https://github.com/anomalyco/opencode/pull/32743)

4.  **#32741** - **[Bug fix]** `fix(lsp): let custom servers configure languageId`: 修复自定义 LSP 服务器问题，现在可以为第三方 LSP 正确配置 `languageId`，修复了某些语言服务（如 R 语言）无提示/补全的 Bug。
    - [PR 链接](https://github.com/anomalyco/opencode/pull/32741)

5.  **#37559** - **[Feature]** `feat(core): bound tool and admitted event payloads via session blobs`: v2 相关的核心优化，通过 Session Blobs 机制限制工具调用和事件负载大小，提升数据库性能和稳定性。
    - [PR 链接](https://github.com/anomalyco/opencode/pull/37559)

6.  **#32740** - **[Bug fix]** `fix(provider): don't send store to the perplexity-agent provider`: 修复 Perplexity provider 的兼容性问题，不再向其 API 发送不被支持的 `store` 字段。
    - [PR 链接](https://github.com/anomalyco/opencode/pull/32740)

7.  **#32739** - **[Bug fix]** `fix(session): don't let auto-title overwrite a title set mid-turn`: 修复对话进行中途用户手动修改标题后，自动生成标题会覆盖该修改的 Bug。
    - [PR 链接](https://github.com/anomalyco/opencode/pull/32739)

8.  **#32679** - **[Feature]** `feat(plugin): let tool.execute.before short-circuit with a result`: 增强插件系统，允许插件在 `tool.execute.before` 钩子中直接返回结果来“短路”工具执行，从而实现自定义的输入验证或逻辑替换。
    - [PR 链接](https://github.com/anomalyco/opencode/pull/32679)

9.  **#32703** - **[Feature]** `feat(tui): expose a prompt facade to TUI plugins`: 为 TUI 插件开放更底层的 Prompt 操作能力，如文本、光标和扩展标记（Extmarks），为社区开发类似 Copilot 的内联提示功能铺平道路。
    - [PR 链接](https://github.com/anomalyco/opencode/pull/32703)

10. **#32693** - **[Feature]** `feat(opencode): session-to-session messaging`: 实验性功能，为不同运行中的会话间通信提供了基础原语，是未来 Agent 间协作的重要一步。
    - [PR 链接](https://github.com/anomalyco/opencode/pull/32693)

## 📈 功能需求趋势

- **OpenAI 兼容性**: 社区最强烈的呼声是实现 **Provider 模型自动发现**（#6231）。这直接关乎到对 LM Studio、Ollama 等本地推理工具链的集成体验。
- **远程开发与架构**: **SSH 远程连接**（#7790, #33273）需求激增，从“feature request”变成了“desktop is useless without it”的强烈呼声，用户希望获得一致的远程开发体验。
- **UI/UX 与布局**: 新版 UI（v1.18.x）引发了关于 **“保留经典布局”** 的激烈讨论（#37012, #37527），表明用户对工作区、多任务组织有很强的路径依赖，界面变更需要更平滑的过渡。
- **模型与多模态支持**: 社区在积极适配新模型（KIMI K3, xAI Grok），但随之而来的是**工具调用兼容性**（#34652, #37399）和**费用显示**（#37524）等实际落地问题。
- **性能与稳定性**: **子代理挂起**（#33028）和 **CORS 阻断**（#31041）等严重影响开发流程的 Bug 受到高度关注，开发者对核心工作流的稳定性要求极高。

## 👨‍💻 开发者关注点

1.  **数据库迁移痛点**: 多次提及的 `no such column` 类错误（#31119, #35403）暴露了插件、CLI 与数据库 Schema 之间的版本管理问题。开发者希望有一个更健壮、无感的自动迁移机制。
2.  **Provider 兼容性陷阱**: 许多问题（#34652, #36834, #37531）集中在新版本（尤其是 v2）和不同 OpenAI 兼容 Provider 的交互上，表明 `@ai-sdk/openai-compatible` 的适配仍存在“边角案例”，尤其是关于 `reasoning` 字段的解析、CORS 处理等。
3.  **CORS 与 SSE 协议问题**: CORS 预检请求失效（#31041）和 WSL 下路径转换（#36902）是影响 Web 和桌面客户端连接的两个典型 **Server-Side** 问题，表明跨平台、跨协议的支持需要更细致的测试。
4.  **插件生态与 2.0 兼容性**: 用户反馈 2.0 版本 (Next) 的插件系统无法加载配置（#37533），同时插件版本与 CLI 版本不匹配会导致崩溃（#35403）。这警示在推进大版本更新时，需确保插件生态的向后兼容性或提供明确的迁移路径。
5.  **性能与资源管理**: 用户开始关注“**无意义的 token 消耗**”，如 xAI Grok 反复调用 `true` 命令（#37399）。此外，`ResourceExhausted` 错误（#35265）和 Prompt Cache 异常（#33998）表明，随着使用深入，资源调度和成本控制正成为高级用户的关注点。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-07-18）

> 基于 GitHub [QwenLM/qwen-code](https://github.com/QwenLM/qwen-code) 仓库数据生成。

---

## 今日速览

- 昨日发布 **v0.19.11-nightly.20260717**，重点改进 daemon 冷启动追踪和多工作区所有权修复。
- **多工作区支持（Multi-workspace）** 成为社区最热话题，RFC 讨论持续升温（29 条评论），相关 PR 和功能请求密集涌现。
- Web Shell 体验迎来多项增强：目录自动补全、拆分视图持久化、Git 状态芯片，以及多语言自动修复注释。

---

## 版本发布

### v0.19.11-nightly.20260717

发布地址：<https://github.com/QwenLM/qwen-code/releases/tag/v0.19.11-nightly.20260717.f8e6e8931>

**主要变更**：
- `feat(daemon): Trace cold first-session startup` — 为 daemon 冷启动添加追踪能力，辅助性能优化。
- `fix(serve): Harden multi-workspace ownership` — 加固多工作区所有权逻辑，提升可靠性。

---

## 社区热点 Issues（精选 10 条）

1. **#6378 [RFC] 支持单 daemon 多工作区**  
   🔗 <https://github.com/QwenLM/qwen-code/issues/6378>  
   - 评论：29｜标签：`daemon`、`scope/session-management`  
   - 核心讨论：打破“1 daemon = 1 workspace”的模型，提出在单进程内托管多个工作区，同时兼容现有客户端。当前设计需要定义会话所有权、`cd` 语义等，是未来架构升级的关键。

2. **#4748 优化 daemon 冷启动和快速路径延迟**  
   🔗 <https://github.com/QwenLM/qwen-code/issues/4748>  
   - 评论：6｜标签：`daemon`、`performance`  
   - 背景：早期 daemon 冷启+首次会话延迟约 2.5s，远超 CLI 的 0.7s。虽已优化 listener/health 路径，但剩余瓶颈仍待解决，社区持续关注。

3. **#7040 [RFC] 可靠的自动记忆召回——时机、质量与遥测**  
   🔗 <https://github.com/QwenLM/qwen-code/issues/7040>  
   - 评论：6｜标签：`roadmap/context-performance`  
   - 核心：缩小范围后，仅针对 Core 的记忆召回路径进行改进，提升所有用户的体验，不扩展为企业级记忆治理平台。包含三个独立可审查的部分，社区反馈积极。

4. **#7051 VS Code 侧边插件报错：ACP 进程异常退出**  
   🔗 <https://github.com/QwenLM/qwen-code/issues/7051>  
   - 评论：6｜标签：`bug`、`VS Code`  
   - 关键：Windows 上 ACP 进程退出代码 0，但 `acp` 和 `channel` 参数被 Electron 拦截，导致连接失败。影响所有 VS Code 用户，急需修复。

5. **#6809 Ctrl+S 多行 diff 预览乱码**  
   🔗 <https://github.com/QwenLM/qwen-code/issues/6809>  
   - 评论：4｜标签：`bug`、`rendering`  
   - 问题：编辑/写入文件时，多行 diff 在权限确认对话框中被错误拼接（如 `};timeout: 30000`），影响用户审查更改。

6. **#7044 升级后命令行报错**  
   🔗 <https://github.com/QwenLM/qwen-code/issues/7044>  
   - 评论：4｜标签：`bug`、`installation`  
   - 用户反馈升级到 v0.19.11 后，运行 `qwen` 直接报错。急需调查升级兼容性，欢迎社区贡献修复（`welcome-pr`）。

7. **#6806 状态行上下文使用百分比不刷新**  
   🔗 <https://github.com/QwenLM/qwen-code/issues/6806>  
   - 评论：3｜标签：`bug`、`token-management`  
   - 执行 `/compress` 后，状态栏仍显示旧 token 数，直到下一次模型请求才更新。影响用户体验，欢迎 PR。

8. **#6776 Ctrl-C 退出后终端按键错乱**  
   🔗 <https://github.com/QwenLM/qwen-code/issues/6776>  
   - 评论：3｜标签：`bug`、`keybindings`  
   - 连续按 Ctrl-C 退出后，后续 Ctrl-C 变成 `9;5u`，表明终端键映射未被正确清理。

9. **#6992 [BUG] 链式 MCP 调用静默失败，权限 UI 卡死**  
   🔗 <https://github.com/QwenLM/qwen-code/issues/6992>  
   - 评论：3｜标签：`MCP`、`Windows`  
   - 两大 bug：链式 MCP 调用因“Server configuration not found”失败；权限 UI 卡死无法恢复。严重影响 Windows 桌面端 MCP 工作流。

10. **#7126 Explore 子 Agent 无限挂起——挂载了 `ask_user_question`**  
    🔗 <https://github.com/QwenLM/qwen-code/issues/7126>  
    - 评论：1｜标签：`bug`、`sub-agents`、`multi-agent`  
    - 尽管是只读 Agent，Explore 却持有 `ask_user_question` 工具，导致 Prompt 触发后 Agent 永远等待人类响应，阻塞多 Agent 管线。已被修复（见 PR #7133）。

---

## 重要 PR 进展（精选 10 条）

1. **#7045 feat: 支持全轮多模态路由**  
   🔗 <https://github.com/QwenLM/qwen-code/pull/7045>  
   - 状态：OPEN｜作者：@yiliang114  
   - 当主模型为纯文本且配置了视觉 fallback 并声明 `capabilities.vision: true` 时，自动将含图片的轮次路由到对应模型，提升多模态场景可用性。

2. **#7100 fix(core): 重试错误的重复思考标签**  
   🔗 <https://github.com/QwenLM/qwen-code/pull/7100>  
   - 状态：OPEN｜作者：@yiliang114  
   - 检测并丢弃 ` <think></think><think> ` 等畸形结构，在到达渲染前重试，避免模型输出乱序。

3. **#7090 feat(cli): 支持同轮消息转向**  
   🔗 <https://github.com/QwenLM/qwen-code/pull/7090>  
   - 状态：OPEN｜作者：@LaZzyMan  
   - 允许在模型响应中输入消息以转向当前轮次，新增 `Ctrl+Q` 快捷方式将消息推迟到下一轮，工具执行期间的同轮消息保持逻辑一致性。

4. **#7099 fix(core): 持久化子 Agent 的解析模型**  
   🔗 <https://github.com/QwenLM/qwen-code/pull/7099>  
   - 状态：OPEN｜作者：@mvanhorn  
   - 子 Agent 使用模型覆盖启动时，在 `.meta.json` 中记录实际解析的模型而非父会话模型。修复 #7095。

5. **#7136 feat(web-shell): 跨刷新持久化拆分视图**  
   🔗 <https://github.com/QwenLM/qwen-code/pull/7136>  
   - 状态：OPEN｜作者：@wenshao  
   - 将拆分视图的活跃会话集保存到 `sessionStorage`，刷新后自动恢复，除非使用 `?split=` 深层链接。关闭拆分时清除持久化状态。

6. **#6984 feat(agents): 支持基于模型的子 Agent 并发限制**  
   🔗 <https://github.com/QwenLM/qwen-code/pull/6984>  
   - 状态：OPEN｜作者：@qwen-code-dev-bot  
   - 新增 `agents.maxParallelAgentsByModel` 配置项，可按具体模型 ID 限制后台子 Agent 并发数，补充全局 `maxParallelAgents`。

7. **#7054 feat(web-shell): Git 状态芯片、可视化工作区 diff 和侧边栏 Git 状态**  
   🔗 <https://github.com/QwenLM/qwen-code/pull/7054>  
   - 状态：OPEN｜作者：@wenshao  
   - 为 Web Shell 带来工作树 Git 感知：工具栏分支芯片显示脏状态、实时 diff 预览、侧边栏摘要。大幅提升浏览器端开发体验。

8. **#6931 fix(cli): 收紧 VP 模式控件占用，修复 shell 工具指示器重叠**  
   🔗 <https://github.com/QwenLM/qwen-code/pull/6931>  
   - 状态：OPEN｜作者：@chiga0  
   - 修复 VP 模式下任务面板、子 Agent 列表与对话内容的溢出问题；同时修复非 VP 模式下 shell 工具指示器与行号的重叠。

9. **#7125 feat(web-shell): 添加工作区添加对话框的目录自动补全**  
   🔗 <https://github.com/QwenLM/qwen-code/pull/7125>  
   - 状态：CLOSED (merged)｜作者：@zjunothing  
   - 用户在添加工作区时输入绝对路径，会实时弹出目录建议列表（从 daemon 主机读取），支持箭头/ Tab/点击选择，降低手动输入错误。

10. **#7133 fix(core): 从 Explore Agent 工具集中移除 `ask_user_question`**  
    🔗 <https://github.com/QwenLM/qwen-code/pull/7133>  
    - 状态：OPEN｜作者：@zjunothing  
    - 直接修复 #7126，删除只读 Agent 的等待人类输入工具，防止多 Agent 管线永久阻塞。添加注释说明原因。

---

## 功能需求趋势

根据本周（尤其是近 24 小时）的 Issues 和 PRs，社区最关注的方向包括：

| 方向 | 代表性 Issue / PR | 说明 |
|------|-------------------|------|
| **多工作区支持** | #6378、#7015、#7070、#7102 | 单 daemon 托管多个项目工作区，并定义会话所有权、cd 语义、API 扩展。 |
| **Web Shell 增强** | #7125、#7136、#7054、#7128、#7117 | 目录自动补全、拆分视图持久化、Git 状态、历史分页、输入框修复等。 |
| **子 Agent & 多 Agent 管线** | #7126、#7133、#7048、#6984 | 子 Agent 并发控制、模型解析持久化、默认后台运行、只读 Agent 工具治理。 |
| **性能优化（冷启动 & 延迟）** | #4748、#6907 | daemon 冷启动追踪和首次会话延迟优化仍是长期痛点。 |
| **记忆与上下文管理** | #7040、#6806 | 自动记忆召回质量、上下文压缩后的状态同步。 |
| **MCP 与工具集成** | #6992、#7103 | MCP 权限处理、链式调用可靠性、IM 通道工作区范围。 |
| **IDE 集成（VS Code）** | #7051、#7101 | ACP 启动问题、日志路由到输出面板。 |

---

## 开发者关注点

从 Issue 反馈中提炼的高频痛点：

1. **升级兼容性**：v0.19.11 升级后部分用户直接报错（#7044），需要关注版本间变化和迁移文档。
2. **终端渲染异常**：Ctrl+S diff 乱码（#6809）、Ctrl-C 退出后按键映射残留（#6776）、滚动代码块渲染崩坏（#7006）等持续困扰用户。
3. **模板/配置继承**：子 Agent 模型覆盖后元数据不准确（#7095），影响回放和调试。
4. **权限与安全**：MCP 权限 UI 卡死（#6992）、安全分类器死锁（#6927）导致自动审批模式下工具调用失败。
5. **CI 稳定性**：多个 CI 主分支 E2E 测试失败（#7096、#7111、#7086），开发团队正在积极修复，相关 Issue 被标记为 `autofix` 或 `ready-for-agent`。
6. **历史记录与分页**：Web Shell 刷新后输入框文本拼接（#7128）、恢复历史分页错误（#7117）影响长期使用体验。

---

*数据采集截至 2026-07-18 08:00 UTC。以上内容由 AI 生成，供技术开发者参考。*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*