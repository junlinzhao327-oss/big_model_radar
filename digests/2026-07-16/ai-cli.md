# AI CLI 工具社区动态日报 2026-07-16

> 生成时间: 2026-07-15 22:35 UTC | 覆盖工具: 7 个

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

# AI CLI 开发工具横向对比分析报告（2026-07-16）

## 1. 生态全景

当前 AI CLI 工具已进入“功能成熟+生态整合”阶段，社区反馈从“能不能用”转向“好不好控”。稳定性（MCP插件断连、子代理挂起）、成本透明度（模型静默切换、上下文窗口强制使用）和用户控制权（自定义规则被忽视、自动记忆无限重试）成为三大核心痛点。同时，各工具正加速向 IDE 集成、远程会话、多工作区管理演进，竞争焦点从单点能力转向平台化体验。

## 2. 各工具活跃度对比

| 工具 | 今日 Release 版本数 | 今日热点 Issue 数 | 今日重要 PR 数 | 社区活跃度评级 |
|------|-------------------|-------------------|---------------|---------------|
| Claude Code | 1 (v2.1.210) | 10 (top10) | 4 | ★★★★☆ |
| OpenAI Codex | 3 (Rust alpha) | 10 (top10) | 10 | ★★★★★ |
| Gemini CLI | 1 (nightly) | 10 (top10) | 10 | ★★★★☆ |
| GitHub Copilot CLI | 2 (patch) | 10 (top10) | 0 | ★★★☆☆ |
| Kimi Code CLI | 0 | 0 | 1 | ★☆☆☆☆ |
| OpenCode | 1 (v1.18.2) | 10 (top10) | 10 | ★★★☆☆ |
| Qwen Code | 3 (nightly/preview + cua) | 10 (top10) | 10 | ★★★★☆ |

> **说明**：OpenAI Codex 和 Gemini CLI 的 PR 数量最多，社区讨论热度最高；Kimi Code 处于极低活跃期；OpenCode 虽 PR 多但 issue 评论偏少。

## 3. 共同关注的功能方向

| 方向 | 涉及工具 | 具体诉求 |
|------|----------|----------|
| **MCP生态稳定性** | Claude Code, OpenAI Codex, Gemini CLI, Copilot CLI, Qwen Code | 工具发现超时导致启动冻结、stdio连接10-20分钟断连、OAuth令牌未桥接、工具名兼容性差 |
| **代理（Agent）可靠性** | Claude Code, OpenAI Codex, Gemini CLI, Qwen Code | 子代理挂起、错误报告为“成功”、嵌套代理无限循环、达到步骤限制后状态误报 |
| **Windows平台兼容性** | Claude Code, OpenAI Codex, Gemini CLI, Copilot CLI | ARM64启动崩溃、serialport模块加载失败、性能严重卡顿、安全软件误报 |
| **模型选择与成本控制** | Claude Code, OpenAI Codex, Copilot CLI | 强制1M上下文、子代理被固定为昂贵模型、静默切换模型导致Token浪费 |
| **用户控制权** | Claude Code, OpenAI Codex, Gemini CLI | 自定义规则（CLAUDE.md）被忽略、自动记忆无限重试、60秒自动关闭提问 | | **语音交互完善** | Copilot CLI | 麦克风选择持久化、ASR路由Bug、PTT丢字 | | **IDE/远程集成** | Copilot CLI, OpenCode, Qwen Code | 远程附着会话、Codespaces认证失败、快捷键冲突 |

## 4. 差异化定位分析

| 工具 | 功能侧重 | 目标用户 | 技术路线 |
|------|----------|----------|----------|
| **Claude Code** | 代码质量门禁、权限规则、长时间任务可视化 | 注重代码规范的团队 | 插件化技能（code-quality-pipeline）；严格权限系统；实时计时器 |
| **OpenAI Codex** | 多Agent架构、模型级控制（GPT-5.6 Sol） | 追求最新模型的进阶开发者 | MultiAgent V2；子代理模型选择；MCP并发加载优化 |
| **Gemini CLI** | 代理安全沙箱、AST感知、自动记忆 | 对安全性和可靠性高要求的开发者 | Bash亲和性沙箱；环境变量扩展检测；递归推理限制 |
| **Copilot CLI** | 企业级权限、MCP OAuth集成、语音模式 | 企业团队、多工具链开发者 | 组织级Token控制；ACP模式；BYOK（自带密钥） |
| **Kimi Code** | 跨语言遥测对齐 | 可观测性敏感的内部团队 | Python ↔ TypeScript事件注册表统一；trace_id追踪 |
| **OpenCode** | Plan/Build模式切换、UI灵活性、MCP资源管理 | 追求高效交互流程的开发者 | 实验性Plan模式默认化；模糊搜索技能；子代理深度控制 |
| **Qwen Code** | 多工作区daemon、中文办公生态（钉钉）、通道集成 | 中国开发者、企业内嵌场景 | 单进程多工作区管理；钉钉交互卡片；daemon日志轮转 |

## 5. 社区热度与成熟度

- **高热+成熟**：Claude Code、OpenAI Codex — 每日稳定Release，Issue评论和点赞量高，社区参与积极，已形成插件生态。
- **中热+快速迭代**：Gemini CLI、Qwen Code — 每日多个PR合并，修复密度高，但部分核心问题（子代理挂起、版本检测）仍存。
- **中热+平台化**：Copilot CLI — 发布节奏慢但社区持续反馈企业级需求，MCP和语音是当前重点。
- **低热+早期**：Kimi Code — 仅一条PR，社区几乎无互动，处于基础设施对齐阶段。
- **中热+UI争议**：OpenCode — 虽PR活跃，但UI回归引发大量不满，社区信任度受考验。

## 6. 值得关注的趋势信号

1. **成本透明化成为硬需求**：用户对模型静默切换、强制长上下文、子代理固定模型的行为零容忍。未来工具需提供更细粒度的Token计量和用户授权机制。
2. **MCP标准化进程加速**：OAuth桥接、工具发现超时、连接持久性等问题跨工具出现，行业亟需统一的MCP服务治理规范。
3. **Windows平台成短板**：ARM64兼容性、serialport依赖、性能卡顿在多个工具中重复出现，制约了微软生态下的开发者采用。
4. **代理安全围栏升级**：环境变量泄露、shell注入绕过、递归深度限制等安全措施正在从“可选”变为“默认强制”。
5. **“自动记忆”争议**：Gemini和Qwen用户均抱怨自动记忆功能导致上下文浪费或无限重试。智能记忆的“主动”与“可控”矛盾亟待解决。
6. **跨IDE/远程会话趋势**：Copilot和Claude Code的远程附着、Qwen的多工作区daemon、OpenCode的ACE协议支持，预示AI CLI将向“后台服务+多端接入”模式进化。

> **建议**：开发者选型时优先评估自身对成本控制、平台兼容性（Windows/Linux）、代理自主性的容忍度；企业团队关注MCP稳定性和权限审计能力；个人开发者关注UI流畅度和自定义规则执行力。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（截至 2026-07-16）

## 一、热门 Skills 排行

以下按社区评论/关注度排序，选取最受关注的 5 个 Pull Requests：

### 1. skill-creator 核心漏洞修复：`run_eval.py` 始终报告 0% recall  
**PR #1298** | @MartinCajiao | [链接](https://github.com/anthropics/skills/pull/1298) | **状态：Open**  
该 PR 定位了 `run_eval.py`／`run_loop.py` 中一个系统性故障：所有技能描述均被评估为 `recall=0%`，导致优化循环针对噪声进行无效迭代。修复涉及 Windows 流读取、触发器检测和并行 worker 的兼容性。该问题在 Issue #556 中获得 12 条评论和 7 个 👍，是社区反应最剧烈的工具链故障。当前 **open**，尚未合入主线。

### 2. 文档排版技能：`document-typography`  
**PR #514** | @PGTBoos | [链接](https://github.com/anthropics/skills/pull/514) | **状态：Open**  
针对 AI 生成文档中的孤词换行、寡妇段落、编号错位等排版问题提供自动校正。社区讨论焦点：用户认为这类“隐形质量瑕疵”在 Claude 生成的长文档中高频出现，且很少有人工后处理，对提升交付品质有强烈需求。Open 状态，等待审核。

### 3. 跨平台兼容性：修复 PDF 技能中大小写敏感的文件引用  
**PR #538** | @Lubrsy706 | [链接](https://github.com/anthropics/skills/pull/538) | **状态：Open**  
修复 `skills/pdf/SKILL.md` 中 8 处大小写不一致（如 `REFERENCE.md` → `reference.md`），导致在大小写敏感的文件系统（如 Linux）上无法加载。该 PR 虽然改动简单，但反映了社区对“跨平台可搬运技能”的基本期望——此前已有多次类似 Issue 报告。Open 状态。

### 4. ODT 格式支持：`odt` 技能（OpenDocument 文本与模板）  
**PR #486** | @GitHubNewbie0 | [链接](https://github.com/anthropics/skills/pull/486) | **状态：Open**  
提供 ODT/ODS 文件的创建、填充、读取和转换为 HTML 的能力。社区讨论集中在 LibreOffice/OpenDocument 标准在企业文档场景中的必要性，以及如何与现有 DOCX 技能互补。Open，尚未合并。

### 5. 自我审计技能：`self-audit`（v1.3.0）  
**PR #1367** | @YuhaoLin2005 | [链接](https://github.com/anthropics/skills/pull/1367) | **状态：Open**  
提出一个通用质检技能——先进行“机械文件验证”（检查所有声称的输出文件是否存在），再进行“四维度推理审计”（按破坏严重性排序）。社区因其“跨项目、跨模型”的通用性而讨论热烈，认为这是技能从“功能补丁”走向“质量护栏”的重要尝试。Open 状态。

### 6. 技能质量分析器与安全分析器（meta-skill）  
**PR #83** | @eovidiu | [链接](https://github.com/anthropics/skills/pull/83) | **状态：Open**  
新增两个元技能：`skill-quality-analyzer`（五维度质量分析）和 `skill-security-analyzer`（安全审计）。社区认为这是生态建设的关键——帮助开发者自检技能质量。但部分用户指出其复杂度较高，可能影响技能本身的 token 效率。Open。

### 7. 测试模式技能：`testing-patterns`  
**PR #723** | @4444J99 | [链接](https://github.com/anthropics/skills/pull/723) | **状态：Open**  
覆盖完整测试栈的指南：测试哲学（Testing Trophy）、单元测试（AAA 模式）、React 组件测试、集成测试等。社区认为该技能填补了官方集合在“测试指导”上的空白，但反馈希望增加更多实际代码示例。Open。

---

## 二、社区需求趋势

从 Issues（按评论数排序）中提炼出以下核心需求方向：

| 需求方向 | 典型 Issue | 关注度 |
|----------|------------|--------|
| **安全与信任** | #492：社区技能在 `anthropic/` 命名空间下分发，用户可能误认为官方技能而授予过高权限（34 条评论） | 最高 |
| **组织级技能共享** | #228：期望直接在 Claude.ai 中跨成员共享 .skill 文件（14 条评论，7 👍） | 高 |
| **工具链稳定性** | #556（run_eval 0% recall）、#1061（Windows 兼容）、#1169（优化循环失效）等多条 Issue 反复出现 | 极高 |
| **技能去重与分类** | #189：两个插件包含完全相同技能，导致上下文窗口浪费（6 条评论，9 👍） | 中 |
| **复杂推理与记忆管理** | #1329：提出 `compact-memory` 技能，使用符号化表达优化长对话状态管理（9 条评论） | 中 |
| **集成 MCP** | #16：希望将 Skills 暴露为 MCP 协议接口（4 条评论） | 持续关注 |

**最大痛点：** 官方 skill-creator 工具链的可靠性严重不足，特别是 Windows 兼容性和评估脚本故障，正在阻碍开发者的技能编写与迭代。超过 5 个独立 Issue/PR 描述了完全相同的“recall=0%”问题，但修复尚未合入主线。

---

## 三、高潜力待合并 Skills

以下 PR 评论活跃且具备清晰功能价值，可能在近期落地：

| PR | Skills | 功能 | 状态 | 合并潜力 |
|----|--------|------|------|----------|
| #514 | `document-typography` | 文档排版质量检查与修复 | Open 4个月+ | 中等（需适配最新工具链） |
| #486 | `odt` | OpenDocument 格式处理 | Open 4个月+ | 中高（企业场景需求明确） |
| #1367 | `self-audit` | 通用推理质量审计 | Open 2周 | 高（创新性强，且作者持续更新） |
| #1302 | `color-expert` | 色彩命名系统、色空间建议 | Open 1个月 | 中高（小众但专业度深） |
| #723 | `testing-patterns` | 测试模式指南 | Open 4个月 | 中（需补充更多代码示例） |

**特别关注**：由同一位作者 @YuhaoLin2005 提交的 `self-audit`（PR #1367）和后续的 `Reasoning Quality Gate Pipeline`（Issue #1385）构建了一个完整的输出质量控制管道，若被采纳，将成为 Skills 生态中首个“质量保证框架”基座。

---

## 四、Skills 生态洞察

**当前社区最集中的诉求是：修复 skill-creator 工具链的核心故障（Windows 兼容、评估脚本失效、YAML 解析问题），并建立安全性与可共享性基础（官方命名空间治理、组织级分发），在此基础上才能支撑更多高质量技能（文档排版、格式支持、测试模式等）的健康增长。**  

--- 

*报告基于 `anthropics/skills` 仓库截至 2026-07-16 的 Issues 与 Pull Requests 数据统计*

---

好的，这是为您生成的 2026-07-16 的 Claude Code 社区动态日报。

---

## Claude Code 社区动态日报 | 2026-07-16

### 今日速览
- **版本更新**：v2.1.210 发布，优化了长时间运行任务的视觉体验，并引入权限规则的启动警告。
- **社区热议**：Issue #18467 成为焦点，用户反馈个人仓库在 Claude Web 端不可见，而组织仓库正常，评论和关注度极高。
- **代码质量新思路**：一个新插件 PR **`code-quality-pipeline`** 被提出，为代码合并定义了严格的、可执行的自动化质量门禁。

### 版本发布
**最新版本：v2.1.210**
- **实时计时器**：为“折叠的工具摘要行”添加了实时运行时间计数器，让长时间运行的工具调用看起来有“滴答”动画反馈，而非让人误以为程序卡死。
- **权限规则警告**：启动时增加警告，提示用户 `Write(path)`, `NotebookEdit(path)`, 和 `Glob(path)` 权限规则已弃用，请改用 `Edit(path)` 或 `Read(path)`。
[查看完整更新日志](https://github.com/anthropics/claude-code/releases/tag/v2.1.210)

### 社区热点 Issues
1.  **个人仓库 vs 组织仓库** (`#18467`) - *Bug*：用户强烈反映，通过 Claude Web (claude.ai/code) 连接时，个人 GitHub 账户下的仓库完全不可见，但组织仓库能正常使用。这严重影响了个人开发者的工作流，获得 65 个点赞和 25 条评论。
    [链接](https://github.com/anthropics/claude-code/issues/18467)

2.  **VS Code 扩展强制 1M 上下文** (`#64349`) - *Bug*：Pro 用户反馈，在 Windows 上使用 VS Code 扩展时，Claude Code 会强制使用 1M 上下文，导致不必要的成本消耗，与 `/usage` 命令显示的额度不符。
    [链接](https://github.com/anthropics/claude-code/issues/64349)

3.  **符号链接导致会话丢失** (`#46342`) - *Bug*：在 macOS 上，`claude -r` 命令无法找到已保存的会话，原因是在 `~/.claude/projects/` 下的项目条目是符号链接（symlinks）。这影响了使用项目符号链接管理多个仓库的用户。
    [链接](https://github.com/anthropics/claude-code/issues/46342)

4.  **Telegram 插件 CPU 占用 100%** (`#60886`) - *Bug*：一个严重的稳定性问题。当 MCP 的 stdio 传输通道因 `EPIPE` 断开时，`uncaughtException` 处理器会陷入无限循环，导致 Telegram 插件在 Linux 平台下 CPU 占用率飙升至 100%。
    [链接](https://github.com/anthropics/claude-code/issues/60886)

5.  **MCP stdio 连接持久性问题** (`#37482`) - *Bug*：用户报告所有 stdio 类型的 MCP 服务器在运行约 10-20 分钟后会断开与父进程的标准输入（stdin）管道，导致进程变为孤儿进程。这是一个影响所有 MCP 插件稳定性的核心问题。
    [链接](https://github.com/anthropics/claude-code/issues/37482)

6.  **Chrome 插件：保存截屏到本地** (`#66077`) - *Enhancement*：用户请求为 Claude in Chrome (Chrome 扩展) 增加一个功能，允许在会话过程中将 Claude 生成的屏幕截图直接保存到本地文件系统，而不是仅限剪贴板。
    [链接](https://github.com/anthropics/claude-code/issues/66077)

7.  **Android + Codespaces 认证失败** (`#66332`) - *Bug*：在 Android 设备上使用 Codespaces 时，OAuth 重定向流程出现问题，导致 Claude Code 认证失败，无法正常使用。
    [链接](https://github.com/anthropics/claude-code/issues/66332)

8.  **Claude 无视架构规则** (`#66007`) - *Bug*：一个值得关注的 bug，用户反映 Claude Code 在高强度任务压力下，会忽略 `CLAUDE.md` 中设定的最高优先级规则，例如内联 SQL、跳过测试等，引发了社区对模型行为一致性的讨论。
    [链接](https://github.com/anthropics/claude-code/issues/66007)

9.  **假阳性安全拦截** (`#66313`) - *Bug*：有研究者在进行结核病流行病学文献综述时，Claude Code 的 Agent 工具错误地触发了“使用政策”拦截，误判了合法的学术研究行为。
    [链接](https://github.com/anthropics/claude-code/issues/66313)

10. **Monitor 工具完成通知静默丢失** (`#66340`) - *Bug*：在 Windows 平台上，`Monitor` 工具执行完毕并通过 `until` 循环满足条件后，其“完成通知”会非确定性丢失，导致模型一直处于“等待状态”，需要用户手动介入。
    [链接](https://github.com/anthropics/claude-code/issues/66340)

### 重要 PR 进展
1.  **`code-quality-pipeline` 插件** (`#77916`) - *New Plugin*：引入一个全新的技能型插件，定义了从“代码编写完成”到“代码合并”之间的标准化质量门禁。它包括文件级和端到端两个阶段的自动化检查，旨在强制执行代码质量。
    [链接](https://github.com/anthropics/claude-code/pull/77916)

2.  **`settings-official-marketplace-only.json` 示例配置** (`#77709`) - *Docs Example*：新增一个配置示例，演示如何通过 `strictKnownMarketplaces` 将插件市场来源严格限制在 Anthropic 官方市场，满足对安全性有更高要求的用户。
    [链接](https://github.com/anthropics/claude-code/pull/77709)

3.  **修复 `validate-settings.sh` 验证脚本** (`#77705`) - *Bug Fix*：修复了文件验证脚本中的一个逻辑错误。当文件不包含 YAML frontmatter 时，脚本本应报错，但却错误地通过了检查。此修复确保了只有符合格式的文件才能被正确验证。
    [链接](https://github.com/anthropics/claude-code/pull/77705)

4.  **`claude-compare` 工具** (`#77613`) - *New Tool*：引入了一个名为 `claude-compare` 的新工具/功能，旨在帮助用户进行比较和对比任务。具体功能细节待进一步探索。
    [链接](https://github.com/anthropics/claude-code/pull/77613)

### 功能需求趋势
- **IDE 与工作流集成**：社区对 VS Code 扩展、Chrome 插件、以及远程开发环境（Codespaces）的集成问题反馈集中。包括会话重命名、快速保存截图、以及更可靠的认证方案。
- **模型行为与成本控制**：用户高度关注模型的选择（如 Opus）、上下文窗口的消耗（强制 1M 上下文）、Token 用量（特别是代理 Agent 模式下的超额消耗）。用户希望有更精细的控制和透明的计费指示。
- **稳定性与可靠性**：大量 bug 报告指向 MCP 插件的稳定性（断连、CPU 100%）、跨平台兼容性（特别是 Windows）及核心工具的异常行为（如 Monitor 工具通知丢失）。
- **功能特色与易用性**：用户期望更强的自定义能力，包括自定义命令不覆盖内置命令、在不重启会话的情况下热加载新 Agent、以及更可控的启动界面和权限系统。

### 开发者关注点
- **权限和集成问题**：个人仓库可见性问题是当前最大的痛点，直接阻碍了个人开发者使用 Claude Web 的体验。
- **MCP 稳定性**：MCP 插件（尤其是 Telegram 等需长连接的应用）的断连和 CPU 飙升问题，是影响开发者生产力和系统稳定的关键因素。
- **模型行为不一致**：Claude Code 在遵循用户自定义规则（如 CLAUDE.md）方面的不稳定表现，动摇了开发者的信任基础。
- **成本控制与透明度**：对 Token 消耗，特别是 Agent 模式下的超额使用，以及 Pro 计划中被强制使用长上下文的抱怨，反映了用户对成本的敏感和对透明度的期待。
- **基本 UI 和平台问题**：Windows 平台上的启动问题、文本框中光标闪烁过快等基本用户体验问题，依然是需要优先解决的低级错误。
- **功能性小缺陷**：如 `claude -r` 不支持符号链接、用户命令静默覆盖内置命令等，虽然是小细节，但积少成多数会显著影响开发者的日常使用流程。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

好的，这是为您生成的 2026-07-16 OpenAI Codex 社区动态日报。

---

# OpenAI Codex 社区动态日报 | 2026-07-16

## 📰 今日速览
今日社区焦点集中在 **GPT-5.6 Sol 模型的子代理配置问题** 上，相关 Issue 获得了高达 153 个赞，成为近期最热讨论。此外，**Windows 平台的性能与稳定性问题** 持续发酵，特别是关于 Windows ARM64 版本应用崩溃的多个报告引起了广泛关注。与此同时，官方 Bot 提交了一系列关于 **MCP 集成优化、性能并发与平台兼容性** 的 PR，显示出对基础设施稳定性的持续投入。

---

## 🚀 版本发布
### Rust 版本更新
过去 24 小时内，Codex Rust 版本密集发布了三个 Alpha 小版本：
- **`rust-v0.145.0-alpha.14`**：最新的 Alpha 14 版本。
- **`rust-v0.145.0-alpha.13`**：Alpha 13 版本。
- **`rust-v0.145.0-alpha.12`**：Alpha 12 版本。
- **备注**：发布说明均为 “Release 0.145.0-alpha.x”，未提供详细的变更日志。

---

## 🔥 社区热点 Issues
以下是过去 24 小时内最值得关注的 10 个 Issue：

1.  **#31814 GPT-5.6 Sol 无法指定子代理模型，强制所有子代理使用Sol实例** [`bug`, `CLI`, `subagent`, `config`]
    - **重要性**：🔥 **今日最热**。该问题指出 GPT-5.6 Sol 的元数据强制启用了 MultiAgent V2，导致用户无法为子代理指定其他模型（如更便宜的模型），所有子代理都成了昂贵的 Sol 实例。评论数高达 79，点赞 153，严重影响使用成本和灵活性。
    - [链接](https://github.com/openai/codex/issues/31814)

2.  **#20214 Codex App在Windows 11 Pro上频繁卡顿/冻结** [`bug`, `windows-os`, `app`, `performance`]
    - **重要性**：😤 **长期痛点**。这是一个长达数月的老问题，尽管用户系统资源充足，但应用依然卡顿。过去一天新增了大量讨论，社区持续追问解决方案，体现了用户对 Windows 桌面版体验的强烈不满。
    - [链接](https://github.com/openai/codex/issues/20214)

3.  **#28969 [功能请求] 增加设置以禁用60秒自动解决AI提问** [`enhancement`, `CLI`, `config`]
    - **重要性**：💡 **呼声极高**。许多开发者抱怨当 Codex 在 CLI 中提问时，如果未在60秒内回应，问题会被自动关闭。该功能请求希望增加一个开关让用户控制此行为，获得 123 个赞，反映了社区对工作流控制的精细化需求。
    - [链接](https://github.com/openai/codex/issues/28969)

4.  **#33381 Windows ARM64版App启动后崩溃循环** [`bug`, `windows-os`, `app`]
    - **重要性**：🐛 **新晋严重Bug**。刚刚发布的问题报告指出，Windows ARM64 设备上的 ChatGPT 桌面应用在启动后 10-15 秒内崩溃循环，系统日志指向 `serialport addon` 加载失败。对 ARM 设备用户影响巨大。
    - [链接](https://github.com/openai/codex/issues/33381)

5.  **#33375 [Windows App] 反复的 serialport.node 延迟加载失败导致严重 UI 卡顿** [`bug`, `windows-os`, `app`, `performance`]
    - **重要性**：🔄 **性能关联**。与 #33381 类似，该问题报告了 `serialport` 模块加载失败导致应用 UI 变得严重卡顿。这暗示了 Windows 版本的 `serialport` 依赖可能存在系统性问题，值得关注。
    - [链接](https://github.com/openai/codex/issues/33375)

6.  **#31846 Codex App: GPT-5.3 Codex Spark 因 "Unsupported parameter: reasoning.summary" 失败** [`bug`, `app`, `config`]
    - **重要性**：🤔 **模型兼容性**。报告称新一代 GPT-5.3 Codex Spark 模型与当前应用的参数传递存在不兼容问题。这预示着在推出新模型时，向后兼容性测试不足，可能影响 Pro 订阅用户的体验。
    - [链接](https://github.com/openai/codex/issues/31846)

7.  **#27159 Codex Desktop隐藏活跃本地线程，但数据库仍标记为未归档** [`bug`, `app`, `session`]
    - **重要性**：🔍 **数据可见性问题**。一个让用户感到困惑的 Bug：本地会话在侧边栏消失，但实际数据未丢失。虽然未造成数据丢失，但严重影响了会话管理和用户查找效率。
    - [链接](https://github.com/openai/codex/issues/27159)

8.  **#23198 Codex Desktop 在 Windows 上极其缓慢** [`bug`, `windows-os`, `app`, `performance`]
    - **重要性**：📉 **性能重灾区**。又一个关于 Windows 性能的长期问题，用户报告应用在日常使用中与系统资源不匹配的卡顿。这与 #20214 共同构成了 Windows 用户的“性能三重奏”。
    - [链接](https://github.com/openai/codex/issues/23198)

9.  **#26478 Windows Codex Desktop 拼写检查检测到错误但显示“未找到建议”** [`bug`, `windows-os`, `app`]
    - **重要性**：😵‍💫 **功能缺失**。拼写检查是编辑器的基础功能，但 Windows 版的建议功能完全失效。这虽然不是一个破坏性 Bug，但影响日常编码体验，社区已确认 Windows 原生拼写正常。
    - [链接](https://github.com/openai/codex/issues/26478)

10. **#33418 CLI静默切换了模型，浪费额外时间和Token** [`bug`, `model-behavior`, `CLI`]
    - **重要性**：💰 **成本问题**。用户报告 CLI 在未通知用户的情况下切换了模型，导致消耗了更多不必要的 Token 和等待时间。这直接关系到用户的金钱和时间成本，社区对此类“静默行为”十分敏感。
    - [链接](https://github.com/openai/codex/issues/33418)

---

## 📌 重要 PR 进展
以下是对社区或项目有重大影响的 10 个 Pull Request：

1.  **#33426 为导入设置添加对 Cursor 的支持** [`enhancement`]
    - **内容**：允许 Codex 从 Cursor 编辑器导入设置，包括沙盒权限、MCP 服务器、项目指令和最近聊天等。这是跨 IDE 生态融合的重要一步。
    - [链接](https://github.com/openai/codex/pull/33426)

2.  **#33432 为生成的子代理保留分页历史记录** [`feature`, `subagent`]
    - **内容**：当父代理使用分页历史模式时，生成的子代理现在也能继承此模式。这有助于大型子代理任务更有效地管理上下文窗口。
    - [链接](https://github.com/openai/codex/pull/33432)

3.  **#33430 避免在 Windows 沙盒中创建元数据路径** [`bug`, `windows-os`, `sandbox`]
    - **内容**：修复了 Windows 沙盒设置时可能错误地将内置的只读元数据保护转为拒绝写入路径的问题。这直接影响了 Windows 用户的文件系统稳定性。
    - [链接](https://github.com/openai/codex/pull/33430)

4.  **#33427 将延迟环境的性能根传播到 MCP** [`feature`, `mcp`]
    - **内容**：允许延迟环境（如远程主机）向 MCP（Model Context Protocol）提供其选定的性能根，确保 MCP 能知晓正确的路径和权限。
    - [链接](https://github.com/openai/codex/pull/33427)

5.  **#33525 通过世界状态刷新主机技能目录** [`feature`, `core`]
    - **内容**：实现了主机技能（如 VS Code 插件）的动态刷新能力。线程启动后，若技能有更新，无需重启对话即可在后续轮次中生效，提升灵活性。
    - [链接](https://github.com/openai/codex/pull/33425)

6.  **#33423 并发加载执行器插件声明** [`performance`]
    - **内容**：将 MCP 服务器和应用连接器的声明文件加载从顺序执行改为并发执行，减少远程环境的等待时间，是一次关键的性能优化。
    - [链接](https://github.com/openai/codex/pull/33423)

7.  **#33421 并发获取工作区连接器** [`performance`]
    - **内容**：与 #33423 思路一致，将工作区连接器的获取也改为并发。这些 PR 表明当前团队的重点之一是通过并发提升系统整体响应速度。
    - [链接](https://github.com/openai/codex/pull/33421)

8.  **#33411 在安装插件时将插件命令迁移为技能** [`feature`, `plugins`]
    - **内容**：将插件中的 Markdown 命令在安装时自动转换为 Codex 的“技能”（Skills），这可能是对旧有插件系统的一次现代化改造，使其与新架构对齐。
    - [链接](https://github.com/openai/codex/pull/33411)

9.  **#29500 特性：支持权限作用域的执行规则** [`feature`, `config`, `security`]
    - **内容**：一个仍在 OPEN 状态的长期 PR，旨在让执行规则（如命令批准）感知到当前的权限配置文件（如沙盒模式、管理模式），实现更细粒度的安全控制。
    - [链接](https://github.com/openai/codex/pull/29500)

10. **#33363 为独立安装程序添加可选的 releases.openai.com 支持** [`enhancement`, `installer`]
    - **内容**：在安装脚本中增加了从 OpenAI 官方 CDN (`releases.openai.com`) 获取更新的选项，为未来可能脱离 GitHub Releases 分发做准备。
    - [链接](https://github.com/openai/codex/pull/33363)

---

## 📈 功能需求趋势
从近期的 Issues 和 PR 中，可以提炼出社区最关注的三个功能方向：

1.  **用户控制权的增强**：社区不再满足于自动化的设定。无论是 **#28969**（禁用自动提问超时）还是 **#29702**（禁用定时自动解决），用户都希望获得更多开关，以精细控制 Codex 的行为，避免 AI 替用户做决定。
2.  **多Agent体系的可控性与稳定性**：随着 GPT-5.6 Sol 等新模型引入更复杂的 MultiAgent 机制，用户希望获得更多控制权，例如 **#31814** 要求能为子代理指定不同模型。同时，子代理超时不生效（**#24951**）等问题也亟需解决。
3.  **跨平台性能与兼容性平衡**：社区对 **Windows 平台性能** 的抱怨持续不断。同时，**Windows ARM64** 的崩溃问题（**#33381**）和 Apple Silicon 的一些问题表明，在推出新功能和模型时，对边缘平台和架构的兼容性测试是薄弱环节。

---

## 🧑‍💻 开发者关注点
以下是开发者在使用过程中反映最集中的痛点和需求：

1.  **Windows 平台的“慢性疼痛”**：性能卡顿（#20214, #23198）、安全软件误报（#30527, #32331）、Git 操作被 ACL 拒绝（#32880）等问题在 Windows 上反复出现，已成为阻碍 Windows 用户深度使用的核心障碍。
2.  **模型切换与配置的透明度**：用户对模型“静默切换”（#33418）以及子代理模型被强制锁定（#31814）等行为非常反感。开发者期望 Codex 的行为可预测、可审计，任何可能消耗更多 Token 或时间的操作都应提前告知。
3.  **应用稳定性与恢复能力**：用户无法容忍应用频繁崩溃，尤其是 **ARM64 启动即崩**（#33381, #33393）。此外，会话数据在侧边栏消失但搜索能查到（#27159）、升级后项目丢失（#31845）等问题，动摇了用户对数据持久性的信心。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

好的，这是为您生成的 2026-07-16 Gemini CLI 社区动态日报。

---

# Gemini CLI 社区动态日报 | 2026-07-16

## 今日速览

今日社区动态主要聚焦于 **代理（Agent）稳定性与可靠性** 的修复，特别是子代理在达到最大步骤限制后的错误报告问题。同时，团队针对 MCP 工具发现超时导致的界面冻结、聊天对话中断等关键 Bug 提交了重要修复 PR。安全方面，社区贡献者修复了一个可能通过环境变量泄露秘密的高危漏洞。

## 版本发布

- **[v0.52.0-nightly.20260715.gfa975395b](https://github.com/google-gemini/gemini-cli/releases/tag/v0.52.0-nightly.20260715.gfa975395b)**: 发布了最新的夜间版，主要包含过去 24 小时的错误修复和改进。具体变更可查看[更新日志](https://github.com/google-gemini/gemini-cli/compare/v0.52.0-nightly.20260714.gfa975395b...v0.52.0-nightly.20260715.gfa975395b)。

## 社区热点 Issues

1.  **[#22323] 子代理在达到最大步骤后错误报告为“成功”**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/issues/22323](https://github.com/google-gemini/gemini-cli/issues/22323)
    *   **重要性**: 这是当前社区最关注的 Bug 之一。`codebase_investigator` 子代理在达到 `MAX_TURNS` 限制时，会错误地将状态报告为 `"success"` 和 `"GOAL"`，从而隐藏了任务实际被中断的事实。这直接影响了用户对任务完成状态的判断，是代理可靠性方面的关键缺陷。

2.  **[#21409] 通用代理（Generalist agent）挂起**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/issues/21409](https://github.com/google-gemini/gemini-cli/issues/21409)
    *   **重要性**: 这是一个 P1 级别的 Bug，严重影响用户体验。当 CLI 将任务委派给通用子代理时，会无限期挂起。该问题已获得 8 个赞，表明很多用户都遇到了此问题。一个已知的临时解决方案是手动指示模型不要使用子代理。

3.  **[#25166] Shell 命令执行后卡在“等待输入”状态**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/issues/25166](https://github.com/google-gemini/gemini-cli/issues/25166)
    *   **重要性**: 另一个影响日常使用的关键 Bug。在 CLI 执行完简单命令后，界面会挂起并显示“等待输入”，即使命令已经完成。这严重影响了工作流程的顺畅性。

4.  **[#19873] 利用模型的 Bash 亲和性：零依赖操作系统沙箱与执行后意图路由**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/issues/19873](https://github.com/google-gemini/gemini-cli/issues/19873)
    *   **重要性**: 这是一个 Epic 级别的功能增强请求，讨论了如何利用 Gemini 3 模型原生操作 Bash 的能力。核心思路是通过沙箱来安全地执行命令，并使模型能够通过标准 POSIX 工具来探索和编辑代码库，无需牺牲用户体验或安全性。

5.  **[#24353] 稳健的组件级评估（Evaluations）**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/issues/24353](https://github.com/google-gemini/gemini-cli/issues/24353)
    *   **重要性**: 该项目长期关注点，旨在建立更精细化的“行为评估”测试体系。该 Epic 是前期工作的延续，目标是确保代理在各种组件上的行为表现稳健，这是提升 CLI 整体质量的基础。

6.  **[#22745] 评估 AST 感知的文件读取、搜索和映射的影响**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/issues/22745](https://github.com/google-gemini/gemini-cli/issues/22745)
    *   **重要性**: 这是一个探索性 Epic，旨在研究利用抽象语法树（AST）来提升代理在代码操作中的精确度和效率。如果能实现，有望减少模型因读取文件不精确而浪费的 Token 和交互次数，是提升开发体验的重要方向。

7.  **[#21968] Gemini 不充分使用技能（Skills）和子代理**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/issues/21968](https://github.com/google-gemini/gemini-cli/issues/21968)
    *   **重要性**: 与社区热点直接相关。用户反馈代理很少主动使用用户自定义的技能和子代理，仅在明确指示下才会使用。这表明代理的自主决策能力仍需改进，以更好地利用现有工具和知识库。

8.  **[#26522] 停止“自动记忆”（Auto Memory）无限重试低信号会话**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/issues/26522](https://github.com/google-gemini/gemini-cli/issues/26522)
    *   **重要性**: 揭示了“自动记忆”功能的一个设计缺陷。当记忆提取代理判断某个会话内容价值较低而不进行处理时，该会话会一直处于待处理状态，导致系统重复尝试。这可能导致资源浪费和性能问题。

9.  **[#21983] 浏览器子代理在 Wayland 下运行失败**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/issues/21983](https://github.com/google-gemini/gemini-cli/issues/21983)
    *   **重要性**: 平台兼容性问题。使用 Wayland 显示服务器的 Linux 用户无法正常使用浏览器子代理，这限制了 CLI 在部分 Linux 环境下的可用性。

10. **[#24246] Gemini CLI 在工具数超过 128 个时遇到 400 错误**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/issues/24246](https://github.com/google-gemini/gemini-cli/issues/24246)
    *   **重要性**: 随着用户安装更多 MCP 服务器或技能，可用的工具数量会增长。CLI 无法优雅地处理超过 API 限制的工具数量，直接返回 400 错误。这指向了工具管理和调度机制的优化需求。

## 重要 PR 进展

1.  **[#28410] 修复：缩短 MCP 工具发现超时**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/pull/28410](https://github.com/google-gemini/gemini-cli/pull/28410)
    *   **功能/内容**: 当 MCP 服务器未能响应 `tools/list` 请求时，CLI 启动时会静默冻结长达 10 分钟。此 PR 为发现过程添加了默认超时，使其能快速失败，解决了严重的启动阻塞问题。

2.  **[#28403] 修复：阻止通过 Shell 变量扩展绕过安全校验**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/pull/28403](https://github.com/google-gemini/gemini-cli/pull/28403)
    *   **功能/内容**: 一个重要的安全修复。之前的检测逻辑只阻止了`$()`和反引号，但`$VAR`和`${VAR}`形式的变量扩展可以被利用来泄露环境变量中的秘密（如 GITHUB_TOKEN）。此 PR 增强了检测逻辑，防止此类绕过。

3.  **[#28407] 修复：取消工具调用后阻止 400 错误**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/pull/28407](https://github.com/google-gemini/gemini-cli/pull/28407)
    *   **功能/内容**: 修复了一个严重问题：当用户在对话中拒绝或取消工具调用后，发送后续提示会导致 400 Bad Request 错误，彻底打断对话。此 PR 通过合并连续的角色消息来防止请求格式错误。

4.  **[#28406] 修复：将模型 ID 解析应用于工具子代理**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/pull/28406](https://github.com/google-gemini/gemini-cli/pull/28406)
    *   **功能/内容**: 修复了 API 用户（无预览访问权限）在使用 `web-search` 等工具时无法正常工作的问题。原因是这些工具子代理硬编码了预览模型 ID，而未通过统一的模型 ID 解析系统。

5.  **[#28164] 修复：限制单用户请求的递归推理轮次**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/pull/28164](https://github.com/google-gemini/gemini-cli/pull/28164)
    *   **功能/内容**: 针对代理可能陷入无限循环的潜在风险，此 PR 为单个用户请求设置了最多 15 轮递归推理的限制（可配置），以保护本地资源和 API 配额。

6.  **[#28405] 修复：防止用户滚动时内容更新导致滚动位置跳跃**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/pull/28405](https://github.com/google-gemini/gemini-cli/pull/28405)
    *   **功能/内容**: 解决了用户向上滚动查看历史内容时，因新内容到达而导致的滚动位置跳转回底部的问题。这是一个显著提升终端用户体验的 UI 修复。

7.  **[#28408] 重构：在工具映射中集中处理密集负载检测**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/pull/28408](https://github.com/google-gemini/gemini-cli/pull/28408)
    *   **功能/内容**: 一项代码重构，将用于判断工具消息内容是否密集的后端逻辑从 UI 组件中移出，集中到数据处理层。这有助于解耦，使 UI 更干净，并便于未来维护和修改。

8.  **[#28319] 重构：在加载环境变量前强制检查路径信任**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/pull/28319](https://github.com/google-gemini/gemini-cli/pull/28319)
    *   **功能/内容**: 一项安全与健壮性改进。在 A2A 服务器模式下，此 PR 确保在加载工作区级别的环境变量之前，先执行路径信任检查，并使用 `AsyncLocalStorage` 隔离任务环境，防止跨任务污染。

9.  **[#28305] 特性：在评估中添加工具调用格式化器和失败摘要**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/pull/28305](https://github.com/google-gemini/gemini-cli/pull/28305)
    *   **功能/内容**: 为行为评估工具增强了诊断能力。当评估失败时，现在会自动打印出一个带有编号的工具调用时间线，包括参数、状态和错误详情，极大方便了开发者在测试失败时定位问题。

10. **[#28275] 修复：使 GCP 遥测导出器成为可选**  
    *   **链接**: [https://github.com/google-gemini/gemini-cli/pull/28275](https://github.com/google-gemini/gemini-cli/pull/28275)
    *   **功能/内容**: 将直接依赖 Google Cloud 服务（Logging, Monitoring, Trace）的遥测导出器从核心运行时依赖中移除，改为可选。这有助于减少 CLI 核心组件的依赖树，对非 GCP 用户更友好。

## 功能需求趋势

社区最关注的功能方向集中在以下几个方面：

1.  **代理的自主决策与可靠性**：用户希望代理能更智能地决定何时使用子代理和技能（#21968），并能准确报告任务状态而非掩藏错误（#22323）。核心是提升代理作为“助手”的可靠性和主动性。
2.  **代码理解的深度与精确度**：社区积极探索利用抽象语法树（AST）来提升代理对代码库的感知能力（#22745），以更精准地读取、搜索和修改代码，减少 Token 浪费和反复操作。
3.  **安全与沙箱执行**：一个重要且持续的关注点。从利用模型的 Bash 亲和性进行沙箱操作（#19873）到防止环境变量泄露（#28403），都体现了对在执行复杂操作时兼顾安全性的强烈需求。
4.  **系统评估与稳健性**：建立更细粒度的组件级评估体系（#24353）成为长期重点，以确保各模块在复杂场景下的行为可靠性，这反映出社区对工具质量的高要求。
5.  **开发者体验的改进**：包括修复终端 UI 的闪烁和滚动问题（#21924, #28405），以及优化 MCP 工具的发现过程（#28410），都是为了让日常使用更流畅。

## 开发者关注点

从反馈中可以看出，开发者的主要痛点和高频需求为：

-   **代理稳定性是首要问题**：通用代理挂起、子代理错误报告成功、Shell 命令卡住等 Bug 是目前最影响用户体验的痛点。
-   **对“自动记忆”功能的疑虑**：用户发现该功能会在低价值会话上无限重试，且存在日志中可能泄露秘密的风险，对其可靠性和安全性表示担忧。
-   **MCP 集成体验有待优化**：MCP 服务器的不稳定会导致 CLI 启动时冻结，以及工具数量过多会引发 API 错误，这些集成问题亟待解决。
-   **平台兼容性仍需完善**：在 Wayland 等非主流环境下的问题依然存在，影响了部分 Linux 用户的使用。
-   **对工具调用透明度的需求**：开发者希望 `/bug` 报告能包含子代理的上下文信息（#21763），并通过 `/chat share` 分享子代理的执行轨迹（#22598），以便于调试和审查。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

## GitHub Copilot CLI 社区日报 — 2026-07-16

### 今日速览

- 📦 **两个补丁版本发布**：v1.0.71-2 新增 `/voice devices` 及画布支持，v1.0.71-3 修复了启动时无效 `settings.json` 的静默忽略问题及终端设置跳过 bug。
- 🔥 **MCP 生态成为社区焦点**：多个 Issue 围绕第三方 OAuth MCP 服务器连接后工具不可用、认证流程中断等问题展开，涉及 Atlassian、Azure DevOps 等主流服务。
- 🗣️ **语音模式持续打磨**：新版本新增麦克风持久化选择功能，但 Issue 中仍报告了全双工路由 bug 及 PTT 抖动丢字问题。

---

### 版本发布

#### v1.0.71-3
**修复**
- 启动时若 `settings.json` 中存在无效配置，现在会显示警告并指出具体错误值，而非静默忽略。
- 修复了在某些终端（无真实 kitty 键盘支持）上 `/terminal-setup` 跳过设置的问题。

#### v1.0.71-2
**新增**
- `/voice devices` 命令，支持选择并持久化语音模式所使用的麦克风。
- 可限制任务与子代理可访问的内置代理列表。
- CLI 中新增画布支持，用于扩展驱动的交互。

**改进**
- `/chronicle cost-tips` 成本建议推荐，增加更丰富的成本画像。

---

### 社区热点 Issues（10 条）

1. **#223 — “Copilot Requests” 权限在组织级 Token 中不可见**  
   - 评论：31 | 👍：76  
   - 重要性：企业级用户无法为自动化工具有效授权，影响大规模部署安全策略。  
   - [链接](https://github.com/github/copilot-cli/issues/223)

2. **#1477 — 模型完成后出现“Continuing autonomously (3 premium requests)”**  
   - 评论：11 | 👍：18  
   - 重要性：用户反馈免费额度用尽后 autopilot 模式行为不符合预期，视为 bug。  
   - [链接](https://github.com/github/copilot-cli/issues/1477)

3. **#4024 — 语音模式所有 ASR 模型无声失败（MultiModalProcessor 路由 bug）**  
   - 评论：8 | 👍：0  
   - 重要性：三大内置模型均返回空转录，影响语音交互可用性。  
   - [链接](https://github.com/github/copilot-cli/issues/4024)

4. **#4096 — 第三方 MCP 服务器显示“已连接”但工具在 CLI 会话中缺失**  
   - 评论：5 | 👍：2  
   - 重要性：Atlassian MCP OAuth 令牌未桥接到会话，导致集成无效。  
   - [链接](https://github.com/github/copilot-cli/issues/4096)

5. **#1979 — 移动端/浏览器远程附加到 Copilot CLI 会话**  
   - 评论：4 | 👍：53  
   - 重要性：呼声极高的功能需求，类似 Claude Code 的远程会话功能。  
   - [链接](https://github.com/github/copilot-cli/issues/1979)

6. **#1069 — 常用编辑快捷键（Ctrl+A/E 等）在用户输入中失效**  
   - 评论：3 | 👍：5  
   - 重要性：影响命令行日常使用体验，期望支持 Readline/Emacs 风格。  
   - [链接](https://github.com/github/copilot-cli/issues/1069)

7. **#2052 — 持久化的 Token/上下文占用指示器**  
   - 评论：3 | 👍：19  
   - 重要性：开发者希望实时看到上下文窗口利用率，避免超出限制。  
   - [链接](https://github.com/github/copilot-cli/issues/2052)

8. **#4034 — Hook 子进程 stdin 写端未关闭导致 `$(cat)` 模式卡死**  
   - 评论：3 | 👍：0  
   - 重要性：工具使用钩子的 stdin EOF 问题，影响钩子脚本可靠性。  
   - [链接](https://github.com/github/copilot-cli/issues/4034)

9. **#4016 — BYOK (`COPILOT_PROVIDER_*`) 在 `--acp` 模式下被拒绝**  
   - 评论：2 | 👍：3  
   - 重要性：自定义模型提供商在 ACP 模式下仍需 GitHub 登录，回归老问题。  
   - [链接](https://github.com/github/copilot-cli/issues/4016)

10. **#4097 — `apply_patch` 删除二进制文件后会话历史永久保留 diff，突破 5 MB 限制**  
    - 评论：2 | 👍：1  
    - 重要性：大文件删除导致会话膨胀，需手动 `/compact` 才能恢复。  
    - [链接](https://github.com/github/copilot-cli/issues/4097)

---

### 重要 PR 进展

**无新提交的 PR**（最新 Pull Requests 为 0 条）。

---

### 功能需求趋势

从近期 Issue 和版本更新中，可总结出社区最关注的方向：

- **MCP 深度集成与认证**：围绕 OAuth、HTTP MCP 服务器连接、工具暴露、分页支持等出现大量 Issue，说明第三方服务集成是当前最热切的需求。
- **语音模式完善**：新增设备选择功能后，仍有识别路由、PTT 丢字等 bug，语音交互的稳定性与准确性是持续打磨的重点。
- **上下文与 Token 管理**：用户强烈要求提供持久化的上下文占用指示器、大型模型（Opus 4.7）的 1M 窗口支持、以及自动压缩/清理机制。
- **远程会话与移动端支持**：类似 Claude Code 的远程附着功能获得了极高赞数，表明开发者希望摆脱终端束缚。
- **企业级权限与认证**：组织级 Token 权限缺失、BYOK 模式在 ACP 下失效等问题，凸显企业客户对安全合规的严苛要求。

---

### 开发者关注点

- **MCP 认证流畅性**：多个 Issue 反映“已连接”但工具不可用、OAuth 流程不弹出窗口或自动取消，开发者期望一次配置即用，无需反复切换。
- **大仓库性能**：`apply_patch` 处理大文件时导致会话溢出、`git worktree add` 全量检出超时等，大型项目用户迫切需要稀疏检出等优化。
- **终端兼容性**：快捷键重映射、NFS/GPFS 挂载下的 TUI 挂起、Windows 下 `/mcp add` 渲染错乱等，反映出跨平台终端体验的不一致。
- **输入编辑体验**：不支持 Emacs/Readline 快捷键、Markdown 缩进被折叠等问题，降低了专业用户的 CLI 编辑效率。
- **非交互模式稳定性**：MCP 服务器延迟连接导致空用户消息、钩子 stdin EOF 缺失等问题，影响 CI/CD 场景下的自动化工具体验。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 | 2026-07-16

## 今日速览

过去24小时内仓库无新版本发布，仅有一条新PR（#2500）处于OPEN状态，该PR旨在对齐Python侧遥测与TypeScript事件注册表，并新增`trace_id`及缺失事件，标志着Kimi Code CLI在跨语言遥测一致性上迈出关键一步。社区整体活跃度较低，暂无新增Issue，开发者对可观测性基础设施的关注正逐步加深。

## 重要 PR 进展

| PR # | 标题 | 作者 | 状态 | 简介 |
|------|------|------|------|------|
| [#2500](https://github.com/MoonshotAI/kimi-cli/pull/2500) | feat(telemetry): align events with TS schema, add trace_id and missing events | @7Sageer | OPEN | 对齐Python侧遥测与`agent-core-v2`的`events.ts`注册表，通过`with_raw_response`捕获`x-trace-id`响应头（支持流式和非流式），新增`trace_id`字段并补全缺失的事件类型，为后续分布式追踪和跨语言调试提供基础。 |

（注：当日仅此一条PR处于活跃状态，社区暂无其他PR进展。）

## 功能需求趋势

基于近24小时唯一活跃PR，以及近期仓库整体Issues与PR积累（未在数据中体现，但可推断），社区最关注的功能方向包括：

- **遥测与可观测性对齐** – 跨语言（Python ↔ TypeScript）事件模式统一，确保埋点数据可追溯、可聚合。
- **IDE集成** – 虽无直接Issues，但从PR背景（`agent-core-v2`）可看出底层架构正为IDE插件等场景做铺垫。
- **流式响应体验** – PR中明确处理流式与非法流式场景的`trace_id`捕获，说明实时交互条件下的端到端追踪是开发重点。

## 开发者关注点

尽管当日社区反馈极少，但通过对唯一PR的深入分析，可归纳以下痛点与高频需求：

- **追踪链路断裂** – 缺少`trace_id`导致无法将Python侧的遥测事件与TypeScript侧的`agent-core-v2`事件关联，影响问题排查效率。
- **事件类型不完整** – 现有Python遥测未覆盖所有在`events.ts`中定义的事件，造成数据空洞，不利于全链路监控。
- **无跟踪关联机制** – 当前PR解决了跨层追踪的关键缺口，侧面反映出开发者对“一键追踪请求全生命周期”的强烈需求。

> 日报基于实时GitHub数据生成，如您的仓库有更多动态，建议明日再次查询以获得完整覆盖。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 | 2026-07-16

## 📌 今日速览
- **v1.18.2 发布**：核心修复了子代理嵌套与 Meta 模型推理深度问题；桌面版新增 `Mod+N` 快捷键。
- **新 UI 布局引发大量争议**：多个用户反馈 Plan/Build 模式切换按钮消失、标签标题被截断，社区集中吐槽。
- **Plan 模式即将成为默认**：PR #32458 已合并，移除实验性标志，但 UI 适配问题仍未解决。

---

## 🚀 版本发布

### v1.18.2
> 2026-07-16 发布 | [Release 详情](https://github.com/anomalyco/opencode/releases/tag/v1.18.2)

**Core（核心）**
- 🐛 默认阻止子代理启动嵌套子代理，新增 `subagent_depth` 配置项可控。
- 🐛 优化 Meta 系列模型的默认推理深度，减少不必要计算。

**Desktop（桌面端）**
- ✨ 新增 `Mod+N` 快捷键用于打开新标签页。
- 🐛 修复若干未列出的桌面端 Bug。

---

## 🔥 社区热点 Issues

挑选了 10 个评论数最高或影响力最大的 Issue，覆盖内存、UI、功能缺失等方向。

| 序号 | Issue | 标题 | 评论 | 👍 | 摘要 & 为什么重要 |
|------|-------|------|------|----|-------------------|
| 1 | [#20695](https://github.com/anomalyco/opencode/issues/20695) | Memory Megathread | 109 | 89 | 内存问题集中贴，开发者要求用户提供堆快照而非猜测解决方案。社区关注度极高，影响所有用户。 |
| 2 | [#1764](https://github.com/anomalyco/opencode/issues/1764) | [FEATURE]: vim motions in input box | 34 | 172 | 希望输入框支持 Vim 快捷键（类似 Claude Code）。虽创建于去年，但持续获得高赞，是用户最期待的功能之一。 |
| 3 | [#36936](https://github.com/anomalyco/opencode/issues/36936) | Desktop: wtf is the new tab layout, tab titles dont fit | 14 | 11 | 直接吐槽新标签布局导致会话标题无法显示，用户要求回退到 1.17 版本。代表大量 UI 反馈。 |
| 4 | [#25239](https://github.com/anomalyco/opencode/issues/25239) | [FEATURE]: Expose GitHub Copilot "Auto" option | 19 | 14 | 希望模型选择器直接显示 Copilot 的“自动”模式，而非手动选择模型。提高易用性。 |
| 5 | [#36997](https://github.com/anomalyco/opencode/issues/36997) | [Bug] Desktop App v1.18.1 new layout hides agent switching UI | 9 | 2 | 新布局（newLayoutDesigns: true）隐藏了 Plan/Build 切换按钮，Tab 键也失效。严重影响工作流。 |
| 6 | [#37070](https://github.com/anomalyco/opencode/issues/37070) | Bug: Plan/Build mode toggle missing from chat UI | 9 | 10 | 与上一条类似，用户报告模式切换按钮完全消失，Windows 用户受影响。 |
| 7 | [#34222](https://github.com/anomalyco/opencode/issues/34222) | Issue using GitHub Copilot MAI-Code-1-Flash | 8 | 9 | 企业 Copilot 用户无法使用 MAI-Code-1-Flash 模型，提示端点不可用。影响大型组织选型。 |
| 8 | [#24038](https://github.com/anomalyco/opencode/issues/24038) | [FEATURE]: Claude support using ACP protocol | 6 | 6 | 用户希望基于 Agent Client Protocol (ACP) 支持 Claude Code 订阅，扩展模型生态。 |
| 9 | [#37158](https://github.com/anomalyco/opencode/issues/37158) | the button change de mode / build or plan mode has disappear | 5 | 0 | 刚创建即关闭（可能重复），但证实该问题在多个用户中独立出现。 |
| 10 | [#35013](https://github.com/anomalyco/opencode/issues/35013) | [bug, core, 2.0] Fable/Zen request-size 400 bypasses auto-compaction | 4 | 0 | V2 核心 Bug：长会话超出 Fable 请求大小边界后自动压缩不触发，导致会话断裂。影响高级用户。 |

---

## 🔧 重要 PR 进展

挑选 10 个近期活跃且具有实质改动（Bug 修复/新功能）的 PR，按关联 Issue 重要性排序。

| 序号 | PR | 标题 | 状态 | 核心内容 |
|------|----|------|------|----------|
| 1 | [#37190](https://github.com/anomalyco/opencode/pull/37190) | fix(notification): handle unavailable server during initialization | **OPEN** | 修复 WSL 环境下通知初始化崩溃，添加回退状态，使渲染器可继续加载。 |
| 2 | [#36752](https://github.com/anomalyco/opencode/pull/36752) | fix(opencode): read cache write tokens from raw usage | **OPEN** | 修复通过 OpenAI 兼容网关使用 Anthropic 模型时缓存写入 token 始终为 0 的问题，避免错误计费。 |
| 3 | [#32481](https://github.com/anomalyco/opencode/pull/32481) | fix(tui): attach auth token when editor port comes from env | **CLOSED** | 修复 VSCode/Cursor 集成时编辑器文件/选择上下文不同步的问题，提升 IDE 联动体验。 |
| 4 | [#32480](https://github.com/anomalyco/opencode/pull/32480) | feat(mcp): surface tool progress | **CLOSED** | 将 MCP 工具的进度通知映射到 OpenCode 现有的“运行中工具”进度界面，提升可观测性。 |
| 5 | [#32478](https://github.com/anomalyco/opencode/pull/32478) | feat(mcp): publish resource list change events | **CLOSED** | 支持 MCP 资源变更通知，为后续 MCP 资源管理功能奠基。 |
| 6 | [#32470](https://github.com/anomalyco/opencode/pull/32470) | fix(tui): truncate labels by display width | **CLOSED** | 修复 TUI 中标签按字符数截断导致显示空白的问题，改用 `Bun.stringWidth` 测量渲染宽度。 |
| 7 | [#32468](https://github.com/anomalyco/opencode/pull/32468) | fix(mcp): retry transient bootstrap failures | **CLOSED** | 桌面端睡眠恢复或网络变化后 MCP 启动失败时自动重试，增强稳定性。 |
| 8 | [#32462](https://github.com/anomalyco/opencode/pull/32462) | fix(filesystem): return empty list when listing a missing path | **CLOSED** | 修复 `list()` 在路径不存在时抛出的 `NotFound` 异常，改为返回空列表，符合预期。 |
| 9 | [#32458](https://github.com/anomalyco/opencode/pull/32458) | feat: make plan mode default (remove experimental flag gating) | **CLOSED** | **重要变化**：移除 Plan 模式的实验性标志，使其成为默认行为。可能与新 UI 布局冲突相关。 |
| 10 | [#32454](https://github.com/anomalyco/opencode/pull/32454) | feat(tui): fuzzy search on skill descriptions, recently used skills | **CLOSED** | 为 TUI 技能选择菜单增加模糊搜索、最近使用、技能详情视图，提升插件使用效率。 |

---

## 📊 功能需求趋势

综合所有 Issues 和 PR 主题，社区当前最关注的方向如下：

1. **UI/UX 重构适配**  
   - 新标签布局（水平/垂直）、Plan/Build 切换按钮可见性、标签标题显示 —— 用户对 1.18 系列 UI 改动容忍度低。
   - 强烈要求保留或恢复旧版 UI 切换选项。

2. **模型与提供商扩展**  
   - 要求直接暴露 GitHub Copilot “Auto” 模式。
   - 支持 Claude Code 通过 ACP 协议。
   - 企业级模型（如 MAI-Code-1-Flash）接入障碍修复。

3. **MCP 生态增强**  
   - MCP 工具进度通知、资源变更事件、每会话 MCP 选择（`serve`/`attach`）。
   - 社区 PR 密集，表明 MCP 是当前开发重点。

4. **性能与健壮性**  
   - 内存泄漏（#20695）、TUI 旧消息消失、子代理嵌套控制 —— 核心稳定性仍是首要任务。

5. **终端与快捷键**  
   - Vim 模式输入框（#1764）长期高赞。
   - IME 兼容性、Ctrl+P/R 等快捷键冲突修复。

---

## ⚠️ 开发者关注点（痛点/高频需求）

| 类别 | 具体问题 |
|------|----------|
| **UI 回归** | 1.18.1 起 Plan/Build 模式按钮消失，Tab 键无法切换，用户被迫回退到 1.17。 |
| **模型可访问性** | 企业 Copilot 用户无法使用 MAI-Code-1-Flash；OpenRouter 上 Qwen 3.7 Plus 出现严重幻觉。 |
| **WSL 兼容性** | 桌面端通知初始化崩溃（#37171），导致 WSL 用户无法正常启动。 |
| **快捷键冲突** | Ctrl+R 被浏览器刷新拦截，Ctrl+P 在 Windows 上完全失效（#37165）。 |
| **会话管理** | 新会话默认标题为“New session”，希望自动生成标题；多会话间 prompt 泄露（#35587）。 |
| **安全与配置** | 当前项目配置（opencode.json）被 AI 代理修改，建议分离安全配置（#37155）。 |
| **乱码输出** | 使用 GLM 5.2 等模型时出现大量中文乱码（#37127），可能与模型兼容性有关。 |

---

> **明日关注**：1.18.2 是否修复 Plan/Build 按钮消失问题？Plan 模式默认化后的 UI 调整进展。内存 Megathread 中开发者有没有提供新的 heap snapshot 指引？

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# 📋 Qwen Code 社区动态日报  
**2026-07-16** | 基于 GitHub [QwenLM/qwen-code](https://github.com/QwenLM/qwen-code) 过去 24 小时数据

---

## 1️⃣ 今日速览
- **多工作区 daemon 支持 RFC 获 23 条评论**，社区对 `qwen serve` 单进程管理多个工作区的需求强烈。
- **连续发布三个版本**：两个 nightly/preview 版本修复了 review 流程和 web-shell 工作区路径锁定，cua-driver-rs v0.7.2 新增相对坐标支持。
- **端到端测试 CI 频繁失败**：过去 24 小时内主分支 CI 出现至少 5 次失败，团队正通过自动修复脚本和超时调整缓解。

---

## 2️⃣ 版本发布
### v0.19.10-nightly.20260715
- **docs(review)**: 限制重复 review 回合后的 PR 范围。
- **feat(web-shell)**: 添加工作区路径锁定，防止在 split-view 中误操作。

### v0.19.9-preview.0
- 与上述 nightly 变更相同（预览版标签不同）。

### cua-driver-rs v0.7.2
- **新功能**：启用相对坐标模式（`relative-coordinate fork`）。
- **平台支持**：macOS 已签名并公证的通用二进制 + `.app`；Linux x86_64/arm64（glibc 2.31+）；Windows x86_64/arm64。
- 内置到 `packages/cua-driver` 目录中，安装器同步更新。

---

## 3️⃣ 社区热点 Issues（TOP 10）
1. **#6378 RFC: Support multiple workspaces in one qwen serve daemon**  
   [链接](https://github.com/QwenLM/qwen-code/issues/6378)  
   **23 条评论**，持续讨论中。当前单个 daemon 只能绑定一个工作区，用户希望同一进程管理多个项目，避免启动多个后台进程。社区对 API 设计、会话隔离、资源分配等细节展开激烈讨论。

2. **#6928 GitHub App authentication not injected into newly created workspaces**  
   [链接](https://github.com/QwenLM/qwen-code/issues/6928)  
   用户在创建新工作区时，私有仓库挂载成功，但 GitHub App 认证未注入，导致后续操作失败。已获 5 条评论，正在诊断。

3. **#5239 subagent和主会话之间的通信机制较弱**  
   [链接](https://github.com/QwenLM/qwen-code/issues/5239)  
   用户反馈子 agent 挂掉后主会话无感知，被迫使用文件监控变通。建议增加双向通信/通知机制。4 条评论，属于中长期需求。

4. **#6857 /update reports "up to date" on 0.19.9 when 0.19.10 is available**  
   [链接](https://github.com/QwenLM/qwen-code/issues/6857)  
   **已关闭**（bug）。`/update` 命令未正确检测 npm registry 上的新版，导致用户无法及时升级。修复已应用。

5. **#6936 isManagedMemoryAvailable() ignores enableManagedAutoMemory setting**  
   [链接](https://github.com/QwenLM/qwen-code/issues/6936)  
   用户关闭自动记忆后，系统提示仍注入 7-9 KB 的指令块，浪费上下文窗口。根源是门控逻辑不匹配。3 条评论，welcome-pr 标签。

6. **#6443 feat(channels): improve DingTalk channel with interactive cards**  
   [链接](https://github.com/QwenLM/qwen-code/issues/6443)  
   希望钉钉频道支持交互卡片（运行状态卡、停止按钮、表单卡）。3 条评论，社区对中文办公场景集成需求旺盛。

7. **#6970 MCP tool names accepted by Gemini are rejected by stricter providers**  
   [链接](https://github.com/QwenLM/qwen-code/issues/6970)  
   MCP 工具名包含点号时，Gemini 可接受，但 OpenAI/Anthropic 兼容提供商会拒绝。需要统一名称净化逻辑。2 条评论，影响跨模型兼容性。

8. **#6946 feat(serve): add bounded Todo continuation for daemon sessions**  
   [链接](https://github.com/QwenLM/qwen-code/issues/6946)  
   建议为 daemon/ACP 会话添加“Todo 停止守卫”机制：当 `todo_write` 留下未完成项时，允许最多两次自动继续。2 条评论。

9. **#6927 分类器报错**  
   [链接](https://github.com/QwenLM/qwen-code/issues/6927)  
   在 `tools.approvalMode = "auto"` 下，安全分类器持续 fail-close，阻塞所有需要批准的工具，形成死锁。2 条评论，紧急 bug。

10. **#6914 Fractional session and per-turn tool-call limits terminate runs prematurely**  
    [链接](https://github.com/QwenLM/qwen-code/issues/6914)  
    当 `maxSessionTurns` 或 `maxToolCallsPerTurn` 设置为小数（如 0.5）时，验证通过但实际比较使用整数计数器，导致第一次后直接终止。3 条评论，已关闭，修复中。

---

## 4️⃣ 重要 PR 进展（TOP 10）
1. **#6967 fix(core): Require explicit approval to exit Plan mode**  
   [链接](https://github.com/QwenLM/qwen-code/pull/6967)  
   强制用户在退出计划模式前确认，防止误操作导致未审核的计划自动执行。

2. **#6971 feat(web-shell): color-code each split pane by workspace**  
   [链接](https://github.com/QwenLM/qwen-code/pull/6971)  
   在 split-view 中为每个工作区着色，便于在窄屏/移动端快速区分。

3. **#6954 feat(serve): add workspace MCP management**  
   [链接](https://github.com/QwenLM/qwen-code/pull/6954)  
   为 Web Shell 和 daemon 添加工作区级别的 MCP 管理入口，支持插件管理、持久化 MCP 发现、类型化 SDK 状态控制。

4. **#6969 feat(cli): Add bounded daemon log rotation**  
   [链接](https://github.com/QwenLM/qwen-code/pull/6969)  
   为 daemon 日志添加固定路径 `debug/daemon/daemon.log`、10 MB 主动轮转 + 4 个归档，每条记录携带 `runId` 和 PID。

5. **#6981 fix(core): route id-less continuation chunks to a colliding tool-call opener's slot**  
   [链接](https://github.com/QwenLM/qwen-code/pull/6981)  
   修复流式工具调用解析器中，当第二个工具调用的 `id` 和 `name` 同时出现在空起始 delta 时，参数丢失的 bug。

6. **#6895 feat(core): propagate trusted invocation context**  
   [链接](https://github.com/QwenLM/qwen-code/pull/6895)  
   引入运行时 `InvocationContextV1`，追踪调用链的入口、原生会话、根提示和发起方 daemon 客户端，增强安全审计能力。

7. **#6955 perf(review): scope Agent 7's build/test to the workspaces the diff changed**  
   [链接](https://github.com/QwenLM/qwen-code/pull/6955)  
   让 review 的 Agent 7（构建测试）仅构建 diff 涉及的工作区及其依赖项，大幅减少 CI 耗时。

8. **#6950 fix(cli): Preserve channel startup failure details**  
   [链接](https://github.com/QwenLM/qwen-code/pull/6950)  
   将 daemon 管理的 channel 启动失败信息（脱敏后）传递到 supervisor 快照、动态控制响应和 `qwen channel set` 命令中。

9. **#6963 / #6975 ci: 新增前后端视觉效果对比预览**  
   [链接](https://github.com/QwenLM/qwen-code/pull/6963) (web-shell)  
   [链接](https://github.com/QwenLM/qwen-code/pull/6975) (daemon)  
   引入 before/after 像素对比和 JSON 响应差异，帮助 reviewer 直观评估 UI/API 变更影响。

10. **#6929 fix(core): force tool_choice in generateJson to prevent auto-mode classifier deadlock**  
    [链接](https://github.com/QwenLM/qwen-code/pull/6929)  
    在 `generateJson` 中强制设置 `tool_choice` 为 `ANY`，确保 AUTO 模式的分类器（如 `respond_in_schema`）不会因模型自由生成而陷入死锁。

---

## 5️⃣ 功能需求趋势
从近期 Issues 中可提炼出以下社区最关注的方向：

| 方向 | 代表 Issue / PR | 热度 |
|------|----------------|------|
| **多工作区 daemon 支持** | #6378 | 🔥🔥🔥🔥🔥 |
| **通道集成完善（钉钉/企业微信）** | #6443, #6883, #6939 | 🔥🔥🔥🔥 |
| **代理（subagent）通信与可靠性** | #5239, #6984 (PR) | 🔥🔥🔥 |
| **MCP 兼容性与安全管理** | #6970, #6917, #6954 (PR) | 🔥🔥🔥 |
| **会话控制与自动化** | #6946 (Todo Stop Guard), #6962 (channel source 持久化) | 🔥🔥 |
| **模型切换与热键** | #6486 (PR) | 🔥🔥 |

此外，“Plan 模式强制确认”、“Daemon 日志轮转”等质量改善也反映了用户对产品稳健性的期待。

---

## 6️⃣ 开发者关注点（痛点与高频需求）
- **版本更新检测不准确**：`/update` 命令未正确对比 npm registry，导致用户停留在旧版。已修复但需关注边缘情况。
- **内存自动管理开关无效**：关闭后仍注入指令块，浪费上下文。建议优先修复。
- **分类器死锁**：AUTO 模式下安全分类器阻塞所有工具，无法恢复。PR #6929 已提交修复。
- **MCP 工具名兼容性问题**：含点号的名称被部分供应商拒绝。跨模型一致性需标准化。
- **Shell 提醒频率过高**：用户期望只在任务结束时触发确认，而非每次工具调用都弹窗。
- **信任状态泄漏**：预览检查意外修改全局缓存，导致未确认的信任状态被持久化。PR #6900 已修复。
- **E2E 测试超时不稳定**：由于共享 CI 运行器速度差异，多个测试因超时而失败。团队正通过放宽超时和并行化解决。

> 日报数据采集时间：2026-07-16 00:00~24:00 UTC+8，基于 GitHub API 返回的过去 24 小时更新。  
> 感谢社区贡献者们的积极反馈与代码贡献！

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*