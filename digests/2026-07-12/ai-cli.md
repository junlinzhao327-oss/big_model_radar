# AI CLI 工具社区动态日报 2026-07-12

> 生成时间: 2026-07-11 22:35 UTC | 覆盖工具: 7 个

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

好的，各位技术决策者和开发者，早上好。以下是根据 2026 年 7 月 12 日各主流 AI CLI 工具社区动态生成的横向对比分析报告。

---

### AI CLI 开发生态横向分析报告 (2026-07-12)

#### 1. 生态全景

当前AI CLI工具生态正处在一个 **“技术军备竞赛”与“痛点收敛”并存**的阶段。一方面，各工具通过频繁的版本迭代（如Claude Code v2.1.207、OpenAI Codex Rust v0.145.0-alpha）快速增加如“Auto Mode”、“多Agent协作”、“YOLO模式”等差异化功能。另一方面，社区反馈揭示了几个普遍的行业级痛点：**MCP（模型上下文协议）集成不稳定**、**跨平台（特别是Windows/WSL）体验欠佳**、以及**Agent自动化与安全控制的平衡难题**。整体呈现出从“能用”向“好用、可控、可信”演进的过渡特征。同时，**成本透明度和Agent“自我认知”** 正在成为决定用户从尝鲜到付费转化的关键因素。

#### 2. 各工具活跃度对比

| 工具名称 | 今日Issues数* | 今日PR数* | 今日Release/版本更新 | 社区总评论数（热门issue） |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 10 | 6 | **1** (v2.1.207) | ~180+ |
| **OpenAI Codex** | 10 | 10 | **2** (v0.145.0-alpha.3/.4) | ~185+ |
| **Gemini CLI** | 10 | 7 | 0 | ~45+ |
| **Copilot CLI** | 10 | 1 | 0 | ~7+ |
| **Kimi Code CLI** | 1 | 3 | 0 | 0 |
| **OpenCode** | 10 | 10 | 0 | ~260+ |
| **Qwen Code** | 10 | 10 | **1** (Nightly) | ~60+ |

**注：*数据源自日报摘要中列举的热点议题/PR，并非当日仓库全部动态。评论数为所列举热点议题评论数之和。*

#### 3. 共同关注的功能方向

多个工具社区的反馈高度聚焦于以下四个方向：

1.  **MCP（模型上下文协议）集成的健壮性**：
    - **Claude Code** (`#12164`): MCP服务器“幽灵连接”，工具无法暴露。
    - **Copilot CLI** (`#4096`): 第三方MCP OAuth token未桥接，工具未注入会话。
    - **Qwen Code** (`#6639`): MCP HTTP传输遇401时未触发OAuth恢复。
    - **Gemini CLI** (`#24246`): MCP工具过多时API返回400错误。

2.  **Agent的“自我认知”与上下文管理**：
    - **Claude Code** (`#65696`): 请求Agent能主动感知并管理自己的Token预算。
    - **OpenAI Codex** (`#21753`): 请求实现与Claude Code同级的完整Hook接口，增强自动化能力。
    - **Gemini CLI** (`#22323`): Subagent达到最大轮次后误报“成功”，用户无法了解真实状态。

3.  **自动化与安全/权限控制的平衡**：
    - **OpenCode** (`#8463`): 请求 `--dangerously-skip-permissions`（YOLO模式）以实现无中断自动化。
    - **Claude Code** (`#51798`): 即使配置了沙箱禁用和Allow权限，系统仍会弹窗确认。
    - **Qwen Code** (`#5970`): YOLO模式被模型自动进入Plan模式，破坏了“只管执行”的预期。

4.  **跨平台体验的一致性**（特别是Windows & WSL2）：
    - **Claude Code** (`#74649`, `#64986`): Windows 11上Cowork功能无法工作，WSL2中认证失败。
    - **OpenAI Codex** (`#18506`, `#24040`): WSL下路径泄露，Windows插件注册表缺失。
    - **Copilot CLI** (`#4095`): Windows下插件更新因VS Code文件锁而失败。

#### 4. 差异化定位分析

*   **Claude Code**: **“Agent生态的集大成者”**。通过丰富的Hook系统、Workflow Agent和MCP协议支持，为用户提供高度的自动化和集成定制能力。关注点在于Agent的**稳定性、安全边界和成本控制**（如Auto Mode、沙箱、重试循环修复）。
*   **OpenAI Codex**: **“模型策略的试验田”**。版本发布活跃但描述模糊，暗示其核心在底层引擎和模型（如GPT-5.6 Sol/Spark）的适配。社区高度关注**多模型策略（MultiAgent V2）、配额管理和VS Code扩展兼容性**，反映出其用户群向专业开发者和模型重度使用者倾斜。
*   **Gemini CLI**: **“多工具集成的稳健派”**。没有花哨的大版本，而是聚焦于修复**核心Agent可靠性**（挂起、卡死、子Agent状态误报）和**安全性**（破坏性命令防护、Auto Memory脱敏）。其技术路线更强调在多模型、多工具（Skill）环境下的稳定与安全。
*   **GitHub Copilot CLI**: **“IDE生态的自然延伸”**。当前声量较小，但问题集中在**语音模式**和**MCP集成**上，这与微软Copilot在VS Code和GitHub场景的深度绑定策略一致。其关注点在于自然语言交互（语音）与外部工具（MCP）的无缝衔接。
*   **Kimi Code CLI**: **“小而美的追赶者”**。社区体量最小，但提交的问题非常具体，直指**元数据解析、UI精确性和服务端（ACP）配置一致性**。其定位是快速修复已知短板，提升基础体验。
*   **OpenCode**: **“社区驱动的全能选手”**。社区极度活跃，高赞需求（YOLO模式、/btw命令、自动发现模型）反映了其用户画像多为**追求效率最大化的极客和自动化场景开发者**。性能问题和模型兼容性是其当前最大短板。
*   **Qwen Code**: **“企业级工作流程设计师”**。核心聚焦在 **“多工作区管理”** 这一高阶场景，并为此完善Daemon管理、Session持久化、WebShell和IDE（JetBrains）集成。技术路线上，它正试图从单一工具进化成一个**可管理多项目、支持团队协作的开发平台**。

#### 5. 社区热度与成熟度

*   **第一梯队（高热度，高互动）**：
    *   **OpenCode**: 以极低门槛（高赞功能请求）和活跃的用户-开发者双向反馈著称，社区参与感极强，正快速迭代，但基础设施（性能）尚需打磨。
    *   **Claude Code**: 用户群体专业度高，问题讨论深入（如成本、自动化流程），成熟度高，但“Regression”频发，说明功能快速扩张伴随稳定性挑战。
*   **第二梯队（中高热度，关注点集中）**：
    *   **OpenAI Codex**: 社区讨论集中在核心功能（模型、配额、跨平台），受OpenAI生态影响大。模型策略调整会直接引发社区反弹（如#31814）。
*   **第三梯队（稳定修复期）**：
    *   **Gemini CLI & Qwen Code**: 社区反馈以Bug Report和明确的功能改进为主，项目处于打磨内部架构和拓展高阶能力的阶段，迭代稳健。
*   **低活跃但精准**：
    *   **Kimi Code CLI**: 社区体量小，但反馈精准。**GitHub Copilot CLI**：当前处于静默期，但依赖强大IDE生态，其动态更具战略意义。

#### 6. 值得关注的趋势信号

1.  **Agent的“自我认知”是下一轮竞争焦点**：用户不再满足于Agent执行命令，而是希望Agent能**主动了解自身状态**（Token预算、任务轮次、可用工具），并能据此做出决策或向用户反馈。这将是区分新一代“智能Agent”与“自动化脚本”的关键。
2.  **MCP是“双刃剑”**：MCP协议在快速扩展工具生态的同时，其**认证（OAuth）、连接状态、资源发现**的可靠性问题已成为普遍痛点。企业级用户在拥抱MCP之前，必须对工具链的稳定性进行充分评估。
3.  **“隐形”成本正浮出水面**：从Claude Code的“重试循环膨胀35倍”到OpenCode的“DeepSeek降价后要求调配额”，用户对**API调用的显隐性成本**变得空前敏感。未来，内置成本监控仪表盘或将成为一个标配功能。
4.  **“开发者体验”的内涵正被重新定义**：它不再仅是漂亮的终端输出，而是更关注 **“自动化流程的确定性”** （Hook、权限是否真的被遵守）和 **“跨平台/跨工具的会话连续性”** （从WSL到Windows，从CLI到IDE的会话同步）。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，以下是基于 `anthropics/skills` 仓库数据的社区热点报告。

---

## Claude Code Skills 社区热点报告 (数据截至 2026-07-12)

### 1. 热门 Skills 排行 (Top PRs)

以下是根据社区讨论热度（评论数）选出的 5~8 个最受关注的 Skills PR。

1.  **`fix(skill-creator): run_eval.py always reports 0% recall`** (`#1298`)
    - **功能**: 修复了 `skill-creator` 核心评估脚本 `run_eval.py` 的一个致命缺陷，该问题导致所有技能描述的召回率均为 0%，使得整个描述优化循环（`run_loop.py`、`improve_description.py`）失效。
    - **讨论热点**: 这是仓库当前最核心的 Bug 修复 PR，直接回应了 Issue `#556` 中社区多人复现的“触发率 0%”问题。修复涉及 Windows 流读取、并行工作进程等多个方面。
    - **状态**: OPEN | [链接](https://github.com/anthropics/skills/pull/1298)

2.  **`Add document-typography skill`** (`#514`)
    - **功能**: 新增一个文档排版技能，用于解决 AI 生成文档中常见的排版问题，如单词孤行、段落孤寡、编号错位等。
    - **讨论热点**: 社区对 AI 文档的质量有普遍诉求，该技能直接切中痛点，提供了明确的检查和修正规则，是一个高度实用的高质量技能。
    - **状态**: OPEN | [链接](https://github.com/anthropics/skills/pull/514)

3.  **`fix(pdf): correct case-sensitive file references`** (`#538`)
    - **功能**: 修复 PDF 技能 `SKILL.md` 文件中 8 处文件名大小写不匹配问题（如 `REFERENCE.md` -> `reference.md`），以兼容大小写敏感的文件系统。
    - **讨论热点**: 这是一个典型的跨平台兼容性修复，体现了社区对技能在 Linux/macOS 等系统上可靠运行的关注。该类问题虽小，但影响面广。
    - **状态**: OPEN | [链接](https://github.com/anthropics/skills/pull/538)

4.  **`Add ODT skill — OpenDocument text creation`** (`#486`)
    - **功能**: 增加对 OpenDocument 格式（ODT, ODS）文件的创建、填充、读取和转换支持，填补了生态中对于开源办公文档格式的空白。
    - **讨论热点**: 社区对于非微软 Office 格式（如 LibreOffice）的支持需求明确，该技能扩展了 Claude Code 在文档处理方面的能力边界。
    - **状态**: OPEN | [链接](https://github.com/anthropics/skills/pull/486)

5.  **`Improve frontend-design skill clarity and actionability`** (`#210`)
    - **功能**: 对现有的前端设计技能进行重构，旨在提升指令的清晰度、可操作性和内部一致性，确保 Claude 能基于具体流程执行。
    - **讨论热点**: 社区的关注点在于技能的质量而非数量。该 PR 展示了如何将一个过于宽泛的概念性指导，转化为 Claude 可精确执行的指令清单。
    - **状态**: OPEN | [链接](https://github.com/anthropics/skills/pull/210)

6.  **`fix(docx): prevent tracked change w:id collision`** (`#541`)
    - **功能**: 修复了 DOCX 技能在插入修订时，因 `w:id` 与文档中已有书签、注释等 ID 冲突导致的文档损坏问题。
    - **讨论热点**: 与 `#538` 类似，体现了社区对核心文档技能（如 DOCX, PDF）在复杂场景下稳定性的高度关注。
    - **状态**: OPEN | [链接](https://github.com/anthropics/skills/pull/541)

7.  **`feat(skills): add self-audit`** (`#1367`)
    - **功能**: 提出了一个通用的“自审计”技能，在交付前对 AI 输出进行机械性文件校验和四维推理质量审计。
    - **讨论热点**: 这是一个比较新颖的元技能概念，旨在提升输出的整体质量和可靠性，代表了社区对技能“质量控制”的探索方向。
    - **状态**: OPEN | [链接](https://github.com/anthropics/skills/pull/1367)

8.  **`Add skill-quality-analyzer and skill-security-analyzer to marketplace`** (`#83`)
    - **功能**: 增加两个元技能：“技能质量分析器”和“技能安全分析器”，用于对技能本身进行评估和审计。
    - **讨论热点**: 该 PR 与后续的安全 Issue (`#492`) 相呼应，表明社区已开始高度重视技能本身的质量与安全性，并寻求通过工具化的方式解决。
    - **状态**: OPEN | [链接](https://github.com/anthropics/skills/pull/83)

### 2. 社区需求趋势 (From Issues)

从 Issues 中可以提炼出社区最期待的几个技能发展方向：

1.  **安全与信任治理**: Issue `#492`（34条评论）指出社区技能被放在 `anthropic/` 命名空间下分发，可能造成信任边界滥用。社区强烈希望 Anthropic 明确官方技能与社区技能的标识，并建立安全审计机制。
2.  **组织级技能共享**: Issue `#228`（14条评论）要求支持跨组织的技能共享功能，而不是依赖手动传输 `.skill` 文件。这揭示了企业用户对技能管理和分发效率的迫切需求。
3.  **技能创作工具的稳定性**: Issue `#556`（12条评论）和 `#1169`（3条评论）反复投诉 `run_eval.py` 的“0%召回率”问题，这直接阻塞了社区贡献者开发新技能。**修复 skill-creator 工具链是目前社区最迫切的需求。**
4.  **高效状态与记忆管理**: Issue `#1329`（9条评论）提出了“紧凑记忆 (compact-memory)”技能，用符号化表示法来节省长对话中的上下文空间，反映了社区对提升 Agent 效率和降低 Token 成本的探索。
5.  **代理治理 (Agent Governance)**: Issue `#412`（6条评论）提出了专门的“代理治理”技能，用于策略执行、威胁检测和审计，这表明社区已开始思考更复杂的多代理或自动化场景下的安全控制。

### 3. 高潜力待合并 Skills (Open PRs)

以下 PR 讨论活跃且极具价值，很可能在未来短期内被合并：

-   **`#1298` (评测修复)**: 作为修复核心流水线 Bug 的 PR，这是合并优先级最高的，不合并则社区贡献的积极性将严重受挫。
-   **`#514` (文档排版)**: 功能定义清晰、实用性强，且属于普适性需求，是典型的高质量社区贡献。
-   **`#538` & `#541` (PDF & DOCX 修复)**: 针对核心技能的关键 Bug 修复，合并可能性高。
-   **`#486` (ODT 支持)**: 填补了关键的技术栈空白，合并后将完善 Skills 生态中对于开源办公文档的支持。
-   **`#1367` (自审计)**: 尽管概念较新，但它直接回应了社区对输出质量的担忧，有潜力成为重要的质量控制工具。

### 4. Skills 生态洞察

**一句话总结**: 当前社区最集中的诉求是 **“工具链的可靠性”与“技能生态的安全与质量”**——社区渴望一个稳定、可用的 `skill-creator` 评测工具，并要求官方在技能的分发、审计和安全性上建立明确的治理标准，而不仅仅是新增功能。

---

好的，各位开发者，早上好。这里是 2026 年 7 月 12 日的 **Claude Code 社区动态日报**。

---

## Claude Code 社区动态日报 | 2026-07-12

### 1. 今日速览

今日最核心的变化是 **v2.1.207 版本**发布，取消了 Auto Mode 的 `CLAUDE_CODE_ENABLE_AUTO_MODE` 环境变量限制，现已对 Bedrock、Vertex AI 和 Foundry 用户默认开放。同时，社区对 **Windows Cowork 功能**的兼容性问题关注度极高，已有 51 条评论。此外，多起关于**权限管理、成本控制和模型回归**的深度讨论仍在发酵。

### 2. 版本发布

**v2.1.207** 主要包含两项改动：
- **Auto Mode 扩展**：在 **Bedrock、Vertex AI 和 Foundry** 平台上，Auto Mode 现在无需设置 `CLAUDE_CODE_ENABLE_AUTO_MODE` 环境变量即可直接启用。用户可通过设置中的 `disableAutoMode` 选项关闭。
- **终端稳定性修复**：修复了在流式输出包含超长列表、表格或段落时，终端可能出现的**冻结和按键延迟**问题。

**简评**：Auto Mode 的开放无疑是本期最大亮点，对于重度依赖 Amazon Bedrock 和 Google Vertex AI 的用户来说，极大降低了使用门槛。终端卡顿的修复则提升了日常编码体验。

### 3. 社区热点 Issues

1.  **[BUG] Windows 11 Pro 上 Cowork 功能无法工作** ([#74649](https://github.com/anthropics/claude-code/issues/74649))
    - **重要性**: 🔥极高 | **评论**: 51 | **状态**: 开放
    - **摘要**: 用户在 Windows 11 Pro 上启动 Cowork 功能失败，错误指向丢失 `vfpext` HCS 服务。这是目前社区最关注的 Bug，反映出 Claude Code 在 Windows 生态下的兼容性短板。
    - **社区反应**: 多名 Windows 用户确认复现，并提供了相关系统日志，期望 Anthropic 能尽快发布针对 Windows 环境的修复方案。

2.  **[BUG] `PreToolUse` 权限已被允许，但在沙箱禁用时仍会弹窗确认** ([#51798](https://github.com/anthropics/claude-code/issues/51798))
    - **重要性**: 🔥高 | **评论**: 31 | **状态**: 已关闭
    - **摘要**: 一个自 2.1.116 版本起的回归问题。当 `dangerouslyDisableSandbox: true` 时，即便 Hook 返回了 `permissionDecision: "allow"`，系统仍会弹窗询问用户是否确认执行 Bash 命令。这与自动化工作流的预期完全不符。
    - **社区反应**: 该 Bug 严重破坏了自动化流程，开发者社区反应强烈，已获得多个 👍 支持，最终被定位并关闭，推测已在更高版本修复。

3.  **[BUG] MCP 服务器连接成功，但工具未暴露给 Assistant** ([#12164](https://github.com/anthropics/claude-code/issues/12164))
    - **重要性**: 🔥高 | **评论**: 15 | **状态**: 已关闭
    - **摘要**: 一个持续了数月的经典 Bug。MCP 服务器状态显示已连接，但 Claude 无法调用其提供的工具。这暴露了 MCP 协议集成中可能存在的“幽灵连接”问题。
    - **社区反应**: 用户尝试了多种 MCP 服务端均出现此问题，社区通过长时间复现和讨论，最终帮助官方定位并关闭了该 Issue。

4.  **[BUG] v2.1.92 回归：自动压缩阈值在 Opus 4.6 上降至 400k** ([#43989](https://github.com/anthropics/claude-code/issues/43989))
    - **重要性**: 🔥高 | **评论**: 11 | **状态**: 已关闭
    - **摘要**: 一个影响深远的成本/效率回归。Opus 4.6 本应支持 1M 上下文，但系统自动压缩的阈值却被无端降至 400k token，导致用户在未达到实际阈值前就损失了大量上下文上下文。
    - **社区反应**: 用户对此“未记录”的回归非常不满，提供了详尽的测试数据，并获得了 7 个 👍。该 Bug 引起了开发团队对模型特性和上下文管理的重视。

5.  **[Feature Request] Hook 输入 JSON 中应包含 `session_name`** ([#36058](https://github.com/anthropics/claude-code/issues/36058))
    - **重要性**: 🚀中等 | **评论**: 6 | **状态**: 已关闭
    - **摘要**: 用户希望在 Hook 的输入 JSON 中，除了 `session_id` 外，还能获得用户可读的 `session_name`。这对于在桌面通知等 Hook 场景中区分不同任务至关重要。
    - **社区反应**: 该功能请求获得了 5 个 👍，表明 Hooks 功能已进入深度使用阶段，社区对人机交互的细节提出了更高要求。

6.  **[BUG] Oversized-image 400 错误引发重试循环，导致成本膨胀约 35 倍** ([#65636](https://github.com/anthropics/claude-code/issues/65636))
    - **重要性**: 💰高 | **评论**: 5 | **状态**: 已关闭
    - **摘要**: 当上传超大图片时，API 返回 400 错误，但 Claude Code 没有优雅处理，而是陷入无限重试循环。每次重试都会使之前的 Prompt 缓存失效，导致 API 调用成本激增。
    - **社区反应**: 这是一个触目惊心的成本问题。用户警告开发者在处理大文件时要格外小心。该问题已被修复，但为所有开发者敲响了 API 调用优化的警钟。

7.  **[BUG] WSL2 环境下 `--bg-pty-host` 注入 `BROWSER=true` 杀死所有基于浏览器的认证** ([#64986](https://github.com/anthropics/claude-code/issues/64986))
    - **重要性**: 🔧中等 | **评论**: 4 | **状态**: 已关闭
    - **摘要**: 在 WSL2 中使用 `--bg-pty-host` 模式时，系统错误地设置了 `BROWSER=true` 环境变量，导致所有需要浏览器打开登录的第三方 API (如 GitHub Copilot, Cloudflare) 认证流程静默失败。
    - **社区反应**: 此 Bug 定位难度高，因为所有认证都静默失败。社区的详细排查为 WSL2 用户扫清了障碍。

8.  **[BUG] Workflow-tool 创建的 Worktree 从未被清理** ([#65645](https://github.com/anthropics/claude-code/issues/65645))
    - **重要性**: 🗑️中等 | **评论**: 4 | **状态**: 已关闭
    - **摘要**: 当使用 Workflow agent 时，其创建的 git worktree 在任务结束后不会被清理。无论用户是否配置了 `WorktreeRemove` Hook，都无法触发默认的清理动作。
    - **社区反应**: 这是一个资源泄漏问题。对于长期运行的 Agent 来说，积累大量废弃 worktree 会浪费磁盘空间并造成混乱。

9.  **[Feature Request] 添加自动上下文使用监控功能** ([#65696](https://github.com/anthropics/claude-code/issues/65696))
    - **重要性**: 🧠中等 | **评论**: 3 | **状态**: 已关闭
    - **摘要**: 用户指出，Claude Agent 在会话中没有内省自身上下文预算的能力，无法主动管理 Token 使用。尽管 `/context` 命令存在，但 Agent 无法自主使用它。
    - **社区反应**: 这代表了对更“智能” Agent 管理的期待。开发者希望 Agent 能感知并主动管理自己的上下文窗口，避免忘记关键信息。

10. **[BUG] LLM 输出了不当短语 "The money shot"** ([#76540](https://github.com/anthropics/claude-code/issues/76540))
    - **重要性**: ⚖️中等 | **评论**: 2 | **状态**: 开放
    - **摘要**: 用户报告称，LLM 在回复中包含了可能被视为不恰当或具有误导性的短语 “The money shot”。
    - **社区反应**: 这反映了社区对 LLM 输出内容的语义安全性和专业性越来越敏感，即便是个别词汇也需要得到规范。

### 4. 重要 PR 进展

1.  **[OP] 移除前端设计技能中的 "retro-futuristic" 推荐** ([#39043](https://github.com/anthropics/claude-code/pull/39043))
    - **摘要**: 一个略显幽默但务实的 PR。作者 `t3dotgg` 建议移除 `Frontend Design Skill` 中的 “retro-futuristic”（复古未来主义）风格推荐。
    - **影响**: 这体现了社区对 Claude 前端“品味”的微调，旨在减少生成过于花哨、不符合主流审美的界面。

2.  **[CL] 修复 macOS 系统证书加载及 NO_PROXY 黑洞问题** ([#76640](https://github.com/anthropics/claude-code/pull/76640))
    - **摘要**: 核心修复。针对 v2.1.17+ 引入的 Bun 运行时，解决了 macOS 上因 SSL 上下文未加载系统证书，以及 `NO_PROXY` 配置导致连接“黑”掉的 Bug。
    - **影响**: 对于使用 Bun 运行时的 macOS 用户，这是一个关键的稳定性修复。

3.  **[CL] 修复：再现性审计中确认的设计缺陷** ([#76673](https://github.com/anthropics/claude-code/pull/76673))
    - **摘要**: 一个大规模的 Bug 修复 PR，涉及 Issue 生命周期管理、Hook 状态隔离等多个方面，目标是修复系统自身的内部逻辑缺陷。
    - **影响**: 体现了 Anthropic 团队在系统层面的“自愈”和改进能力，对平台稳定性有长远利好。

4.  **[OP] 修复 plugins：加固 YAML、路径和符号链接处理** ([#76581](https://github.com/anthropics/claude-code/pull/76581))
    - **摘要**: 安全增强。加强了官方插件脚本中 YAML 解析、路径遍历和符号链接的操作，以防止凭证覆盖等攻击。
    - **影响**: 对插件开发者和用户都是重要的安全更新，防止第三方插件引入安全漏洞。

5.  **[OP] 修复 plugin-dev：使 `userConfig` 文档与 Hook 验证器对齐** ([#76576](https://github.com/anthropics/claude-code/pull/76576))
    - **摘要**: 文档与行为一致性修复。更新了插件开发指南，使其与 v2.1.207 中关于 Shell 注入修复的验证器规则保持一致。
    - **影响**: 帮助插件开发者避免因新版本安全策略变更而导致插件失效。

6.  **[CL] 修复：再见性审查确认的设计缺陷（日文修复）** ([#76633]（注：原文#76673，摘要已涵盖）
    - **摘要**: 同上，该 PR 主要为日语环境的再现性审查修复。

### 5. 功能需求趋势

从过去24小时的议题和讨论中，可以提炼出社区最关心的三大功能方向：

1.  **更智能的内存与上下文管理 (Memory & Context)**
    - **趋势**: 不再满足于简单的文件存储。社区希望 **Agent 能主动感知并管理 Token 消耗**（`#65696`），并支持**跨项目的用户全局记忆**（`#62026`），同时要求能**自定义或抑制自动注入的上下文**（如 `userEmail`, `currentDate`，`#53231`）。这表明开发者正将 Claude Code 视为一个更长期、更智能的“副驾驶”。

2.  **跨平台体验的一致性与可靠性 (Cross-Platform Parity)**
    - **趋势**: Windows 和 WSL2 用户的问题持续突出。从 Cowork 功能不可用（`#74649`）到认证失败（`#64986`），再到工作区目录权限问题（`#65629`），社区强烈要求 Claude Code 在 **Windows 和 Linux 平台（尤其是WSL2）** 上获得与 macOS 同等的稳定体验。

3.  **成本控制与检测 (Cost Control & Transparency)**
    - **趋势**: 不再是“能用就行”，社区开始关注**可量化的成本**。重试循环导致成本膨胀 35 倍（`#65636`）、未记录的上下文自动压缩（`#43989`）等事件，让用户对隐性成本非常警觉。集成商和重度用户迫切需要一个**更直观的成本仪表盘或预警机制**。

### 6. 开发者关注点

除了上述趋势，几个具体的痛点也值得所有开发者注意：

- **回归问题依旧高频**: “Regression” 标签在 Issues 中频繁出现。建议开发者**更新至最新版本后再复现**老的 Bug，或尝试在新版本中保留旧版本的核心配置文件，以减少被回归问题影响的风险。
- **信息孤岛问题**: 多个 Issues 反映了系统内部或系统与开发者之间的信息不通畅。例如，Agent 不知道自己的上下文预算（`#65696`），Plan 面板的评论不能自动传递给 Claude（`#75399`），子 Agent 会忽略用户的否决指令继续抓取数据（`#65684`）。
- **自动化与手动控制的冲突**: 当用户试图通过 Hook 或配置文件（如 `effortLevel`、`attribution.commit`）自动化工作流时，系统有时会忽略这些设置，使得自动化变得不可靠（`#51798`, `#65651`, `#65657`）。这要求开发者在依赖自动化时必须进行充分测试。
- **配置的极限与边界**: `dangerouslyDisableSandbox: true` 和 Hook 的结合存在多个已知问题，使用该配置的用户需要特别留意权限和稳定性的权衡。对于 MCP 的使用，出现工具“幽灵连接”（#12164）时，应同时检查客户端和服务端日志。

---
**以上就是今天的 Claude Code 动态。希望大家开发顺利，下期见！**

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 | 2026-07-12

> 数据来源：GitHub `openai/codex`（截至 2026-07-11 更新）

---

## 📌 今日速览

- **GPT-5.6 Sol 的多智能体模型强制继承问题**（#31814）成为社区焦点，获 100 个 👍 和 47 条评论，用户反馈 Sol 会强制所有子代理使用相同模型，导致配置失效。
- **两个 Rust 小版本（v0.145.0-alpha.3/4）** 在过去 24 小时内发布，但未附带详细变更说明。
- **VS Code 扩展在 Linux 上出现空白 WebView（#32041）** 以及 **“重置配额”失效 bug（#31606）** 持续引发用户抱怨，评论分别达 22 条和 30 条。

---

## 🚀 版本发布

### rust-v0.145.0-alpha.4 / alpha.3
- **标签**：`rust-v0.145.0-alpha.4`、`rust-v0.145.0-alpha.3`
- **说明**：两个连续的小版本更新，描述仅标注 `Release 0.145.0-alpha.4` 和 `Release 0.145.0-alpha.3`，未提供具体变更列表。推测为针对 CLI 和核心引擎的增量修复或预发布测试。
- 🔗 [v0.145.0-alpha.4](https://github.com/openai/codex/releases/tag/rust-v0.145.0-alpha.4) | [v0.145.0-alpha.3](https://github.com/openai/codex/releases/tag/rust-v0.145.0-alpha.3)

---

## 🔥 社区热点 Issues（Top 10）

### 1. #31814 — GPT-5.6 Sol 强制所有子代理同为 Sol 实例
- **作者**：@spadaval | **👍** 100 | **评论** 47
- **摘要**：GPT-5.6 Sol 通过模型元数据选择 MultiAgent V2，并默认隐藏子代理元数据，导致用户无法为子代理指定不同模型。社区认为这破坏了多智能体灵活性。
- 🔗 https://github.com/openai/codex/issues/31814

### 2. #31606 — “重置”失败：消耗一次重置次数但未生效
- **作者**：@otpl8855-hash | **👍** 38 | **评论** 30
- **摘要**：Pro 用户在 Codex App 中使用重置配额时，重置次数减少但实际限额未恢复，影响用户体验。Windows 平台频繁复现。
- 🔗 https://github.com/openai/codex/issues/31606

### 3. #21753 — 实现与 Claude Code 完整的 Hook 接口（29+ 项）
- **作者**：@oxysoft | **👍** 19 | **评论** 25
- **摘要**：社区期望 Codex 的自动化钩子系统达到 Claude Code 的完整覆盖率，涵盖生命周期、工具调用、权限检查等场景。属于长期跟踪型增强请求。
- 🔗 https://github.com/openai/codex/issues/21753

### 4. #32041 — VS Code 扩展在 Linux 上打开空白 WebView（新版 26.5707）
- **作者**：@AK25789 | **👍** 1 | **评论** 22
- **摘要**：Linux 用户发现最新扩展版本（26.5707.*）只能显示空白 WebView，降级到 26.5623 后正常但缺失 GPT-5.6 Sol 支持。社区期待快速修复。
- 🔗 https://github.com/openai/codex/issues/32041

### 5. #5538 — CLI 响应时输入消息消失
- **作者**：@BobbyWang0120 | **👍** 10 | **评论** 19
- **摘要**：使用 Codex CLI 时，已输入的文本会在模型响应过程中部分消失，需要重新输入。持续近一年未彻底解决。
- 🔗 https://github.com/openai/codex/issues/5538

### 6. #31836 — 项目排序仅作用于任务组内，不改变项目顺序
- **作者**：@yagaC64 | **👍** 8 | **评论** 13
- **摘要**：macOS App 中“按最后更新排序”选项实际只排序任务组内的任务，项目容器本身顺序不变，导致用户困惑。
- 🔗 https://github.com/openai/codex/issues/31836

### 7. #21653 — 支持多行状态行（TUI）
- **作者**：@EveGoodEvening | **👍** 39 | **评论** 10
- **摘要**：CLI/TUI 的状态行在配置较多选项时会被截断，社区希望支持换行显示。点赞数高反映大量用户有此需求。
- 🔗 https://github.com/openai/codex/issues/21653

### 8. #24040 — Windows 桌面 App + Chrome 扩展：注册表缺失导致原生消息主机无法连接
- **作者**：@JCEY289 | **👍** 0 | **评论** 10
- **摘要**：Codex Chrome 扩展在 Windows 上因 Native Messaging Host 注册表键缺失无法工作，影响浏览器集成。
- 🔗 https://github.com/openai/codex/issues/24040

### 9. #18506 — Windows + WSL：UNC 路径、终端、配置泄露三重问题
- **作者**：@blockedby | **👍** 14 | **评论** 10
- **摘要**：通过 UNC 路径打开 WSL 项目时，集成终端无法打开、Windows 配置泄露到 WSL，且 `CODEX_HOME` 需要 WSL 原生路径。Windows 用户常见痛点。
- 🔗 https://github.com/openai/codex/issues/18506

### 10. #31846 — GPT-5.3 Codex Spark 报错“Unsupported parameter: reasoning.summary”
- **作者**：@osipovgleb | **👍** 17 | **评论** 9
- **摘要**：使用 GPT-5.3 模型时，Codex App 持续返回参数错误，用户怀疑是模型版本与 API 不兼容或配置问题。
- 🔗 https://github.com/openai/codex/issues/31846

---

## 🔧 重要 PR 进展（Top 10）

### 1. #31526 — 限制托管线程仅使用服务器注册的工具
- **作者**：@richardc-oai | **状态**：已合并
- **摘要**：为托管 app-server 客户端添加 `server_registered_tools_only` 特性，允许精确限制工具白名单，防止多余工具注入。
- 🔗 https://github.com/openai/codex/pull/31526

### 2. #32485 — 技能切换视图使用可用宽度显示名称
- **作者**：@copyberry[bot] | **状态**：已合并
- **摘要**：修复技能名称被截断为 21 字符的问题，现在自适应弹窗宽度完整显示。
- 🔗 https://github.com/openai/codex/pull/32485

### 3. #32461 — 渲染 TUI diff 时将 Tab 展开为空格
- **作者**：@copyberry[bot] | **状态**：已合并
- **摘要**：替换 diff 文本中的 Tab 为 4 个空格，避免终端渲染错位。
- 🔗 https://github.com/openai/codex/pull/32461

### 4. #32460 — 守护进程中断时发送线程空闲生命周期
- **作者**：@copyberry[bot] | **状态**：已合并
- **摘要**：当守护（Guardian）重复审核拒绝后中断活跃回合时，现在正确触发 `thread-idle` 生命周期事件，方便扩展感知。
- 🔗 https://github.com/openai/codex/pull/32460

### 5. #32441 — 保留父沙箱策略供内存合并使用
- **作者**：@copyberry[bot] | **状态**：已合并
- **摘要**：内存合并代理现在继承父回合的权限配置和沙箱覆盖，避免权限丢失导致合并失败。
- 🔗 https://github.com/openai/codex/pull/32441

### 6. #31806 — 发布新版本到 Cloudflare R2（影子备份）
- **作者**：@zsol-openai | **状态**：已合并
- **摘要**：在 GitHub Release 之外，将安装包同步到 Cloudflare R2 作为冗余分发渠道，不改变现有 URL 和通道。
- 🔗 https://github.com/openai/codex/pull/31806

### 7. #30135 — CI：发布带版本号的 Bash fork 构件
- **作者**：@bolinfest | **状态**：已合并
- **摘要**：恢复 Bash fork 支持，并为独立版本化构建管道，无需每次随 Rust 版本重建。
- 🔗 https://github.com/openai/codex/pull/30135

### 8. #30036 — 使 Windows 可执行文件解析确定性
- **作者**：@jif-oai | **状态**：已合并
- **摘要**：当 `lpApplicationName` 缺失时，Windows 可能先于 Codex 的环境变量应用选择执行文件。此 PR 强制在配置环境中解析，避免混乱。
- 🔗 https://github.com/openai/codex/pull/30036

### 9. #30016 — 核心：在子代理中继承当前步骤的环境
- **作者**：@sayan-oai | **状态**：已合并
- **摘要**：支持延迟执行器后，子代理应继承请求实际使用的环境（而非回合开始时的快照），修复环境不一致问题。
- 🔗 https://github.com/openai/codex/pull/30016

### 10. #29960 — 缓存稳定执行器技能并按模型步骤投影
- **作者**：@jif-oai | **状态**：已合并
- **摘要**：技能元数据应在环境 ID 稳定后只发现一次，避免每次采样步骤重复读取，提升性能。
- 🔗 https://github.com/openai/codex/pull/29960

---

## 📈 功能需求趋势

从近期 Issues 和 PR 中可提炼出社区最关注的 **四大功能方向**：

| 方向 | 代表 Issue/PR | 说明 |
|------|---------------|------|
| **自动化与钩子系统完善** | #21753（Claude Code Hook Parity）、#32460（守护生命周期） | 社区期望 Codex 提供全面的生命周期钩子，支持外部工具和自动化脚本深度集成。 |
| **多行/可配置 TUI** | #21653（多行状态行）、#32461（Tab 展开） | 终端用户对界面可定制性要求日益增长，包括状态行换行、diff 格式优化等。 |
| **跨平台与远程支持** | #18506（Windows+WSL）、#23200（无桌面 App 的 Linux 远程）、#13802（FreeBSD CLI） | 开发者希望在 Linux、FreeBSD 甚至无桌面环境下也能高效使用 Codex CLI 或移动端远程控制。 |
| **模型选择与配额管理** | #31814（Sol 强制子代理模型）、#32486（GPT-5.6 上下文越限） | 随着多模型策略推出，社区对模型选择灵活性、配额透明度和越限警告的需求明显上升。 |

---

## 🧑‍💻 开发者关注点

综合近期 Issue 反馈，开发者普遍遇到的 **痛点和高频需求** 包括：

- **配额重置异常**：多个 Issue 反映重置次数被无端消耗（#31606、#32484），且周限额无故归零（#32279），严重影响 Pro 用户信任。
- **VS Code 扩展稳定性**：Linux 用户遭遇空白 WebView（#32041），Windows 用户反馈扩展频繁发送未处理广播导致卡顿（#31149），且存在插件注册表缺失（#24040）。
- **WSL 集成混乱**：Windows + WSL 场景下存在路径解析错误（#18506、#24268）、终端无法启动、配置泄露等连锁问题，仍是 Windows 用户最大痛点。
- **新模型兼容性**：GPT-5.6 Sol 的 MultiAgent V2 默认行为与现有配置冲突（#31814），GPT-5.3 Spark 参数不兼容（#31846），表明新模型的引入缺乏平滑迁移方案。
- **安全与防病毒冲突**：Windows 上 Norton 拦截 PowerShell（#25425）、Smart App Control 阻止未签名二进制（#32487），提示需要加强代码签名和兼容性说明。

---

*本日报基于 GitHub `openai/codex` 公开数据自动生成，仅供参考。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 | 2026-07-12

---

## 一、今日速览

过去 24 小时无新版本发布，但社区围绕 **Agent 可靠性** 与 **核心稳定性** 的讨论持续升温。`Subagent` 在达到最大轮次后误报“成功”（#22323）成为最热议题；同时，通用代理挂起（#21409）和 shell 命令执行后无故卡死（#25166）的 Bug 反复出现；多项涉及 **Auto Memory 安全性与策略优化** 的 Issue 获得维护者关注。7 个活跃 PR 中，**VS Code 终端焦点修复** 与 **shell 包装器剥离增强** 等合并候选已进入审查阶段。

---

## 二、版本发布

无新版本（最新 Release 早于 24 小时前）。

---

## 三、社区热点 Issues（10 个）

### 1. #22323 – Subagent 达到最大轮次后误报成功  
**链接**: [https://github.com/google-gemini/gemini-cli/issues/22323](https://github.com/google-gemini/gemini-cli/issues/22323)  
**简述**: `codebase_investigator` 子代理明明因 `MAX_TURNS` 被中断，却报告 `status: "success"` 和 `Termination Reason: "GOAL"`，掩盖了实际中断。  
**重要性**: 直接影响用户对代理完成度的信任，需要优先修复。社区有 10 条评论，2 个 👍。

### 2. #21409 – 通用代理挂起  
**链接**: [https://github.com/google-gemini/gemini-cli/issues/21409](https://github.com/google-gemini/gemini-cli/issues/21409)  
**简述**: 只要 Gemini CLI 将任务转给通用代理，就会无限挂起，直至手动取消。简单文件夹创建也会触发。  
**重要性**: 高频复现 Bug，影响基本使用。8 个 👍 表明社区深受困扰。

### 3. #25166 – Shell 命令执行后卡在“等待输入”  
**链接**: [https://github.com/google-gemini/gemini-cli/issues/25166](https://github.com/google-gemini/gemini-cli/issues/25166)  
**简述**: 命令已执行完毕，但界面仍显示“Awaiting user input”，导致无法继续工作。  
**重要性**: 突破性用户体验 bug，用户“反复”遇到。3 个 👍，标注 `effort/medium`。

### 4. #21968 – Gemini 不主动使用自定义技能和子代理  
**链接**: [https://github.com/google-gemini/gemini-cli/issues/21968](https://github.com/google-gemini/gemini-cli/issues/21968)  
**简述**: 即使配置了 gradle、git 等技能，模型几乎从不主动调用，只有在显式指令下才使用。  
**重要性**: 核心功能落地问题，关系 Agent 生态的可扩展性。6 条评论。

### 5. #26522 – Auto Memory 对低信号会话无限重试  
**链接**: [https://github.com/google-gemini/gemini-cli/issues/26522](https://github.com/google-gemini/gemini-cli/issues/26522)  
**简述**: 提取代理因低信号跳过阅读，导致该会话永远不被标记为“已处理”，每次循环都会再次出现。  
**重要性**: 内存系统的逻辑缺陷，浪费资源。5 条评论。

### 6. #26525 – Auto Memory 日志缺少确定性脱敏  
**链接**: [https://github.com/google-gemini/gemini-cli/issues/26525](https://github.com/google-gemini/gemini-cli/issues/26525)  
**简述**: 提取代理在发送会话内容前仅提示脱敏，但实际内容已进入模型上下文；且服务可能记录含秘密的技能。  
**重要性**: 安全合规风险，需要前置脱敏。3 条评论。

### 7. #23571 – 模型在随机位置创建临时脚本  
**链接**: [https://github.com/google-gemini/gemini-cli/issues/23571](https://github.com/google-gemini/gemini-cli/issues/23571)  
**简述**: 模型被限制采用 shell 执行后，会在各种目录生成 edit 脚本，造成清理负担。  
**重要性**: 工作流整洁度问题，用户需手动清理。3 条评论。

### 8. #22672 – 代理应阻止破坏性行为  
**链接**: [https://github.com/google-gemini/gemini-cli/issues/22672](https://github.com/google-gemini/gemini-cli/issues/22672)  
**简述**: 模型在 git 操作、数据库维护中可能使用 `git reset --force` 等危险命令，缺乏安全防护。  
**重要性**: 安全增强需求，1 个 👍，3 条评论。属于 customer-issue。

### 9. #22267 – 浏览器代理忽略 settings.json 覆盖  
**链接**: [https://github.com/google-gemini/gemini-cli/issues/22267](https://github.com/google-gemini/gemini-cli/issues/22267)  
**简述**: 即使全局或项目级别 `settings.json` 中设置了 `maxTurns` 等参数，浏览器代理完全不生效。  
**重要性**: 配置不生效导致用户无法调整行为，降低可控性。3 条评论。

### 10. #24246 – 工具超过 128 个时返回 400 错误  
**链接**: [https://github.com/google-gemini/gemini-cli/issues/24246](https://github.com/google-gemini/gemini-cli/issues/24246)  
**简述**: 当可用工具数超过 400（实际触发阈值约 128）时，API 返回 400，代理无法继续。  
**重要性**: 扩展性瓶颈，用户启用大量 MCP 工具后必然遇到。3 条评论。

---

## 四、重要 PR 进展（7 个）

### 1. #28183 – VS Code 扩展：关闭 diff 标签后保持终端焦点  
**状态**: Open | **大小**: M | **标签**: help wanted  
**链接**: [https://github.com/google-gemini/gemini-cli/pull/28183](https://github.com/google-gemini/gemini-cli/pull/28183)  
**简述**: 批准文件编辑后，VS Code 的 diff 预览会关闭并抢走终端焦点，用户必须手动点击终端。此 PR 使焦点保持在终端，提升编辑流畅度。

### 2. #28359 – 增强 shell 包装器剥离逻辑  
**状态**: Open | **大小**: S/M | **标签**: need-issue  
**链接**: [https://github.com/google-gemini/gemini-cli/pull/28359](https://github.com/google-gemini/gemini-cli/pull/28359)  
**简述**: `stripShellWrapper` 仅识别裸 `-c`，无法处理 `bash -lc "..."` 等登录/交互式包装。修复后策略引擎能正确重新检查包装内的命令。

### 3. #28349 – 修复 customDeepMerge 循环引用崩溃  
**状态**: Open | **大小**: M | **标签**: area/core  
**链接**: [https://github.com/google-gemini/gemini-cli/pull/28349](https://github.com/google-gemini/gemini-cli/pull/28349)  
**简述**: `customDeepMerge` 在遇到循环引用（如 `obj.self = obj`）时无限递归，导致 `RangeError`。增加了循环检测以保护设置管理器。

### 4. #28319 – A2A 服务器：强制执行路径信任检查顺序  
**状态**: Open | **大小**: M/L/XL | **标签**: need-issue  
**链接**: [https://github.com/google-gemini/gemini-cli/pull/28319](https://github.com/google-gemini/gemini-cli/pull/28319)  
**简述**: 重构 `CoderAgentExecutor` 初始化，确保在加载工作区环境变量之前先进行路径信任检查；同时引入 `AsyncLocalStorage` 隔离任务环境。

### 5. #28164 – 限制递归推理轮数（已合并关闭）  
**状态**: CLOSED | **大小**: M | **标签**: need-issue  
**链接**: [https://github.com/google-gemini/gemini-cli/pull/28164](https://github.com/google-gemini/gemini-cli/pull/28164)  
**简述**: 为单次用户请求添加严格的递归推理轮数限制（默认 15 轮），防止无限循环消耗 CPU 和 API 配额。

### 6. #28248 – 文档：解释 MCP 环境变量扩展  
**状态**: Open | **大小**: S | **标签**: docs  
**链接**: [https://github.com/google-gemini/gemini-cli/pull/28248](https://github.com/google-gemini/gemini-cli/pull/28248)  
**简述**: 新增 `mcpServers` 路径/环境变量扩展文档，说明 `$VAR`、`${VAR:-fallback}` 等语法，并指出不支持的格式（如 `{{VAR}}`、`~`）。

### 7. #28247 – 修复 ls 忽略模式按相对路径匹配  
**状态**: Open | **大小**: M | **标签**: status/pr-nudge-sent  
**链接**: [https://github.com/google-gemini/gemini-cli/pull/28247](https://github.com/google-gemini/gemini-cli/pull/28247)  
**简述**: `ls` 命令的忽略模式原先只匹配 basename，导致包含路径分隔符的模式（如 `build/*`）失效。改为使用 `picomatch` 支持 `**` 通配，并保留原有 basename 行为（如 `*.log`）。

---

## 五、功能需求趋势

从所有活跃 Issue 中提炼出社区最关注的四个方向：

1. **Agent 行为智能化与可控性**  
   - 希望模型更主动地使用自定义技能和子代理（#21968）。  
   - 需要子代理轨迹可共享以方便调试（#22598）。  
   - 要求代理具备“自我认知”，能准确报告自身标志、热键和用法（#21432）。

2. **安全与沙箱强化**  
   - 零依赖 OS 沙箱（#19873）呼声较高，希望利用模型原生的 bash 能力但隔离破坏性命令。  
   - 阻止危险 git/db 操作（#22672）。  
   - Auto Memory 日志需要在发送前确定性脱敏（#26525）。

3. **性能与稳定性**  
   - 修复各种挂起、卡死、无限重试问题（#21409、#25166、#26522）。  
   - 终端 resize 时不闪烁（#21924）。  
   - 限制工具数量过大导致 400 错误（#24246）。

4. **配置与扩展的灵活性**  
   - 子代理支持 symlink（#20079）。  
   - 浏览器代理、全局设置应正确合并覆盖（#22267）。  
   - 支持 AST 感知的文件读取与代码导航（#22745、#22746），减少 token 消耗。

---

## 六、开发者关注点（痛点 / 高频需求）

- **子代理状态错误**：达到最大轮次后报告成功，导致用户误以为任务完成（#22323）。  
- **代理挂起 / 无响应**：通用代理（#21409）和 shell 执行后等待输入（#25166）最影响日常使用。  
- **破坏性命令风险**：模型自动执行 `git reset --force` 等操作，用户担心数据丢失。  
- **临时文件污染**：模型在随机目录生成临时脚本，增加清理成本（#23571）。  
- **配置不生效**：settings.json 中的 `maxTurns` 等参数被浏览器代理忽略（#22267）。  
- **工具数量限制**：开启大量 MCP 工具后 API 返回 400，无法继续工作（#24246）。  
- **内存系统缺陷**：低信号会话被无限重试（#26522）且存在隐私泄露风险（#26525）。  
- **终端焦点丢失**：VS Code 扩展中 diff 预览关闭后焦点不回到终端（#28183 PR 正在解决）。

---

*数据更新时间：2026-07-11 23:59 UTC。获取最新动态请关注 [github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)。*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 (2026-07-12)

## 今日速览
昨日（2026-07-11）社区无新版本发布，但涌现了多项关键Bug报告。**MCP（模型上下文协议）集成**成为最大焦点：OAuth 流程断裂、工具无法注入会话的问题集中爆发，多个用户报告 Atlassian 等远程 MCP 服务器“假连接”。此外，**语音模式**的ASR模型静默失败、Windows插件更新权限错误、以及 `web_search` 工具产生幻觉回答等问题也引发开发者关注。仅有一项 PR 进展，为安装脚本的 PATH 去重改进。

## 版本发布
无新版本发布。

## 社区热点 Issues (10条)

1. **#4024 语音模式：所有内置 ASR 模型静默失败**  
   - 作者: @sylvanc | 👍: 0 | 评论: 7  
   - `/voice` 录音正常（电平显示），但三种模型（nemotron-3.5-asr-streaming-0.6b 等）均返回空转录。疑似 MultiModalProcessor 路由 Bug。  
   - 链接: https://github.com/github/copilot-cli/issues/4024

2. **#4096 第三方 MCP 服务器显示“已连接”，但工具未出现在会话中（OAuth Token 未桥接）**  
   - 作者: @bugale | 👍: 0 | 评论: 0  
   - 通过 GitHub Copilot 应用 UI 登录 Atlassian 远程 MCP 服务器后显示绿色“Connected”，但 CLI 会话中永远没有工具可用。  
   - 链接: https://github.com/github/copilot-cli/issues/4096

3. **#4095 Windows：插件更新因 VS Code 运行而失败（os error 5）**  
   - 作者: @FBakkensen | 👍: 0 | 评论: 0  
   - `copilot plugin update` 在 VS Code 开启时失败，Copilot 扩展持有 watcher 句柄导致文件锁。  
   - 链接: https://github.com/github/copilot-cli/issues/4095

4. **#4094 删除会话未从 session-store.db 移除，导致 VS Code Chat 中出现孤立会话**  
   - 作者: @evdbogaard | 👍: 0 | 评论: 0  
   - 应用内删除会话后，底层数据库（data.db、session-store.db）及 VS Code 缓存仍保留记录，造成混乱。  
   - 链接: https://github.com/github/copilot-cli/issues/4094

5. **#4083 语音模式下载因企业代理失败（ENOTFOUND）**  
   - 作者: @sebastianh6r | 👍: 0 | 评论: 0  
   - 通过 NuGet 下载 Foundry Local Core 时被公司代理拦截，已提供修复脚本但期望官方支持代理。  
   - 链接: https://github.com/github/copilot-cli/issues/4083

6. **#4082 跨应用会话同步：CLI 与桌面应用的会话互不可见**  
   - 作者: @omkarnikam24 | 👍: 0 | 评论: 0  
   - 在 CLI 开启的会话无法在桌面应用查看，反之亦然；期望双向同步或至少单向导入。  
   - 链接: https://github.com/github/copilot-cli/issues/4082

7. **#4088 技能（Skill）动态上下文注入（`!command` 占位符）**  
   - 作者: @mumenthalers | 👍: 0 | 评论: 0  
   - 提议在 `SKILL.md` 中支持类似 `!command` 的占位符，以便技能调用时动态注入命令输出。  
   - 链接: https://github.com/github/copilot-cli/issues/4088

8. **#4092 语音捕获期间临时静音系统播放**  
   - 作者: @daweins | 👍: 0 | 评论: 0  
   - 用户希望在按下语音快捷键时自动静音 Spotify 等系统播放，防止扬声器干扰麦克风。  
   - 链接: https://github.com/github/copilot-cli/issues/4092

9. **#4090 语音模式：松开空格键时自动提交转录文本**  
   - 作者: @DavidHollman | 👍: 0 | 评论: 0  
   - 当前 PTT 松开后需再按 Enter 提交，请求改为松键即发。  
   - 链接: https://github.com/github/copilot-cli/issues/4090

10. **#4093 web_search 工具返回捏造答案（幻觉）**  
    - 作者: @dfrysinger | 👍: 0 | 评论: 0  
    - AI 驱动搜索在无相关结果时仍生成“自信、详尽但完全虚构”的答案，并有虚假引用。  
    - 链接: https://github.com/github/copilot-cli/issues/4093

## 重要 PR 进展 (1条)

- **#2565 install: 防止重复安装时 PATH 条目重复**  
  - 作者: @marcelsafin | 未合并  
  - 当前安装脚本依赖 `command -v copilot` 检查，但需要重启 shell 才能生效，导致二次安装向 shell profile 追加重复 PATH。本 PR 修复检查逻辑。  
  - 链接: https://github.com/github/copilot-cli/pull/2565

## 功能需求趋势

从近期 Issue 可见社区最关注的功能方向：

- **语音模式体验优化**：ASR 模型静默失败、自动提交、系统播放静音、代理下载支持 —— 语音交互是当前迭代核心。
- **MCP 集成稳定性**：OAuth 流程断裂、工具不可用、会话中资源不暴露等问题集中爆发，开发者对第三方 MCP 服务器（Atlassian、WorkIQ 等）的接入体验期望很高。
- **会话生命周期管理**：跨应用同步、删除清理、数据库一致性 —— 用户需要统一的会话管理体验。
- **动态上下文注入**：Skill 中通过 `!command` 占位符执行命令并注入结果，提升自动化能力。
- **模型自定义与发现**：BYOK 模式下 CLI 无法自动查询提供商模型列表，用户希望减少手动配置。

## 开发者关注点

- **Windows 文件锁痛点**：VS Code 运行时插件更新失败率高，需要更优雅的句柄释放或重试机制。
- **代理/企业环境兼容**：语音模式下载未考虑企业代理，导致部署受阻。用户已提供补丁但期望官方修复。
- **OAuth 流程断裂**：多个 MCP 服务器出现“连接成功但无工具”现象，OAuth 令牌未正确桥接到会话进程，影响所有远程 MCP 服务。
- **web 搜索可靠性**：AI 搜索的幻觉问题严重，用户建议当无相关结果时应明确返回“无结果”，而非编造答案。
- **文档模糊**：全局指令 md 文件（AGENTS.md/CLAUDE.md）的默认行为未清晰说明，导致用户困惑。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 | 2026-07-12

## 今日速览

过去24小时没有新版本发布，但社区提交了3个修复性PR和一个关于插件元数据错误的Issue。其中**CHANGELOG.md被误识别为技能**的Bug影响用户使用`/skill`自动补全体验，而三个PR分别修复了后台Agent任务耗时记录、字符串截断长度计算偏差以及ACP服务器未加载全局MCP配置的严重功能缺口。

---

## 版本发布

无（过去24小时无新Release）

---

## 社区热点 Issues

### #2491 Bug: kimi-datasource CHANGELOG.md incorrectly listed as a skill  
- **作者**: @zhangleilaoge  
- **状态**: Open  
- **摘要**: 在使用`/skill`自动补全时，`CHANGELOG`被列为技能选项，实际指向插件的CHANGELOG.md文件而非真正的技能。  
- **为什么重要**: 该Bug直接破坏技能自动补全的可用性，使用户可能误选CHANGELOG.md作为技能，导致错误调用或混淆。社区尚无评论，但问题定义清晰，属于元数据解析逻辑缺陷。  
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2491

---

## 重要 PR 进展

### #2493 Fix: record started_at for background agent tasks so duration is reported  
- **作者**: @nankingjing  
- **状态**: Open  
- **功能/修复**: 背景Agent任务从未设置`runtime.started_at`，导致运行耗时丢失；背景Bash任务已正确处理。本PR为Agent任务补齐该字段。  
- **开发者反馈**: 暂无评论，修复后用户可准确获取后台Agent任务执行时长，利于性能监控。  
- **链接**: https://github.com/MoonshotAI/kimi-cli/pull/2493

### #2492 fix: shorten_middle output exceeds target width by ellipsis length  
- **作者**: @nankingjing  
- **状态**: Open  
- **功能/修复**: 字符串截断函数`shorten_middle`未将`"..."`（3个字符）计入宽度计算，导致输出总比指定宽度多出最多3字符。修复后严格符合预期长度。  
- **开发者反馈**: 虽为微小UI细节，但在终端布局、表格渲染等场景下直接影响对齐美感。  
- **链接**: https://github.com/MoonshotAI/kimi-cli/pull/2492

### #2490 fix(acp): load global MCP config in kimi acp server  
- **作者**: @nankingjing  
- **状态**: Open  
- **功能/修复**: `kimi acp`（多会话ACP服务器）从未加载用户全局配置的MCP服务器，导致ACP客户端（如Zed、JetBrains AI Assistant）只能看到内置工具，与交互式`kimi`存在功能差距。本PR修复此缺口，关联Issue #2464。  
- **开发者反馈**: 这是对IDE集成场景的关键修复，直接影响Kimi Code CLI在外部编辑器中的可用性。  
- **链接**: https://github.com/MoonshotAI/kimi-cli/pull/2490

---

## 功能需求趋势

从今日仅有的1个Issue和3个PR看，社区当前最关注的方向集中在：

1. **元数据与依赖解析的准确性**（#2491）—— 插件技能注册逻辑需要更严格的校验，避免非技能文件被误纳入技能列表。  
2. **后台任务执行状态记录**（#2493）—— Agent任务与Bash任务的对等性，表明用户对后台任务的可观测性有持续要求。  
3. **字符串与UI排版的一致性**（#2492）—— 即使是截断函数的小偏差也被提报修复，反映社区对终端输出精度的重视。  
4. **MCP/ACP集成扩展**（#2490）—— 全局MCP配置在非交互式服务中的缺失修复，显示IDE和第三方工具集成的需求正在上升。

---

## 开发者关注点

- **技能自动补全的可靠性**: #2491 Bug暴露了插件技能注册机制缺陷，开发者希望避免“假技能”干扰正常工作流。  
- **后台任务可观测性缺失**: #2493反映Agent任务缺乏耗时记录，开发者期望所有异步任务都能提供统一的运行时日志。  
- **外部工具链集成差距**: #2490指出`kimi acp`与`kimi`交互模式的配置不一致，开发者强烈要求保持全局配置在服务端也生效。  
- **小细节修正的紧迫性**: #2492虽然影响微小，但被独立提报并提交PR，说明社区对用户体验零容忍。

---

*数据来源：GitHub - MoonshotAI/kimi-cli*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 | 2026-07-12

## 📌 今日速览
- DeepSeek V4 Pro 永久降价 75% 后，社区集中讨论调整 OpenCode Go 用量限制（#28846，93 条评论）；同时 GPT-5.6 Luna 模型通过 OAuth 访问时返回 404，引发广泛关注（#36140）。
- 多项性能相关 Issue 持续发酵，多起高 CPU 使用率报告（#30086、#19466）成为用户核心痛点。
- 功能请求方面，YOLO 模式（--dangerously-skip-permissions）、/btw 命令以及自动发现模型等呼声极高，高赞数反映社区对自动化与效率的强烈需求。

---

## 🚀 版本发布
过去 24 小时内无正式版本发布。

---

## 🔥 社区热点 Issues（Top 10）

### 1. #28846 [CLOSED] 调整 Go 用量限制以匹配 DeepSeek V4 Pro 降价
- **评论/赞**：93 / 83  
- **摘要**：DeepSeek V4 Pro API 价格永久降低 75%，用户建议同步调整 OpenCode Go 订阅的用量限制。  
- **为什么重要**：经济影响直接，涉及付费用户的成本优化，社区讨论热烈。  
- **链接**：https://github.com/anomalyco/opencode/issues/28846

### 2. #8463 [OPEN] 添加 `--dangerously-skip-permissions`（YOLO 模式）
- **评论/赞**：28 / 91  
- **摘要**：在自动化或可信环境中，权限提示会打断工作流，提议增加跳过所有权限的启动参数。  
- **为什么重要**：高赞反映自动化场景需求迫切，但安全风险需评估。  
- **链接**：https://github.com/anomalyco/opencode/issues/8463

### 3. #4751 [CLOSED] 添加配置选项禁用“选中即复制”
- **评论/赞**：25 / 18  
- **摘要**：用户阅读时习惯高亮文本，导致剪贴板被频繁污染。  
- **为什么重要**：小但烦人的 UX 问题，评论多，最终已关闭（可能已实现）。  
- **链接**：https://github.com/anomalyco/opencode/issues/4751

### 4. #30086 [OPEN] 新版本 OpenCode 高 CPU 使用率
- **评论/赞**：24 / 13  
- **摘要**：近期更新后 CPU 飙升，从 10+ 会话流畅到 3 会话即卡顿。  
- **为什么重要**：性能问题影响大范围用户，复现简单，急需定位。  
- **链接**：https://github.com/anomalyco/opencode/issues/30086

### 5. #16992 [OPEN] 添加 `/btw` 命令
- **评论/赞**：18 / 153  
- **摘要**：效仿 Claude Code，允许开发者键入 `/btw` 插入额外提示而不中断当前思考。  
- **为什么重要**：153 个 👍 是本日最高赞，社区呼声极高。  
- **链接**：https://github.com/anomalyco/opencode/issues/16992

### 6. #36140 [OPEN] GPT-5.6 Luna 通过 ChatGPT OAuth 返回“模型未找到”
- **评论/赞**：16 / 68  
- **摘要**：尽管内置 OpenAI Provider 中列出了 `gpt-5.6-luna`，但请求返回 HTTP 404。  
- **为什么重要**：新模型兼容性问题，影响大量订阅 ChatGPT 的用户。  
- **链接**：https://github.com/anomalyco/opencode/issues/36140

### 7. #8816 [OPEN] 提供 llms.txt 和 markdown 格式的文档
- **评论/赞**：16 / 35  
- **摘要**：希望官方提供易于解析的文档结构（llms.txt），便于 LLM 工具集成。  
- **为什么重要**：开发者和 LLM 生态整合的基础需求。  
- **链接**：https://github.com/anomalyco/opencode/issues/8816

### 8. #6231 [OPEN] 自动发现 OpenAI 兼容 Provider 的模型列表
- **评论/赞**：16 / 169  
- **摘要**：当前需手动配置所有本地模型（LM Studio、Ollama 等），建议自动发现。  
- **为什么重要**：169 👍 是今日第二高赞，简化配置的痛点明显。  
- **链接**：https://github.com/anomalyco/opencode/issues/6231

### 9. #19466 [OPEN] 空闲时也占用 50% CPU
- **评论/赞**：14 / 11  
- **摘要**：当 OpenCode 因 API 限速等待重试时，单核 CPU 占用约 50%。  
- **为什么重要**：进一步佐证性能问题，资源浪费明显。  
- **链接**：https://github.com/anomalyco/opencode/issues/19466

### 10. #22132 [OPEN] OpenCode 1.4.3 在本地 Ollama Provider 上挂起
- **评论/赞**：12 / 5  
- **摘要**：简单 prompt 即导致挂起，但直接调用 `/v1/chat/completions` 正常。  
- **为什么重要**：本地模型用户基数大，兼容性影响开发体验。  
- **链接**：https://github.com/anomalyco/opencode/issues/22132

---

## 📦 重要 PR 进展（Top 10）

### 1. #35866 [OPEN] 更新 xAI 品牌为 SpaceXAI
- **类型**：文档  
- **摘要**：将界面中 xAI 名称更新为 SpaceXAI，涉及 Provider 标签、OAuth 方法、模型目录等。  
- **链接**：https://github.com/anomalyco/opencode/pull/35866

### 2. #31955 [CLOSED] 添加本地 Whisper 语音输入
- **类型**：新功能  
- **摘要**：为 prompt 编辑器添加多语言语音输入按钮，使用本地 Whisper 模型。  
- **链接**：https://github.com/anomalyco/opencode/pull/31955

### 3. #31952 [CLOSED] 支持从 `$CONFIG/opencode/desktop-themes/` 注册主题
- **类型**：新功能  
- **摘要**：允许用户将自定义主题文件放入指定目录自动加载。  
- **链接**：https://github.com/anomalyco/opencode/pull/31952

### 4. #31947 [CLOSED] 修复通过 SSH 时终端能力检测
- **类型**：Bug 修复  
- **摘要**：解决 1.16.0 起 TUI 在 SSH 下渲染错误（16 色、错误主题、无 tmux 感知）。  
- **链接**：https://github.com/anomalyco/opencode/pull/31947

### 5. #31946 [CLOSED] 修复 Windows 会话路径、Shell 环境、错误信息及自动补全
- **类型**：Bug 修复  
- **摘要**：综合修复 Windows 桌面子进程路径、Shell 环境变量、错误提示等多项问题。  
- **链接**：https://github.com/anomalyco/opencode/pull/31946

### 6. #31945 [CLOSED] 使用父子关系而非 ID 顺序判断循环退出
- **类型**：Bug 修复  
- **摘要**：修复 Web 客户端提供的 messageID 可能导致无限循环的 issue。  
- **链接**：https://github.com/anomalyco/opencode/pull/31945

### 7. #31940 [CLOSED] 支持 MCP Resource 内容
- **类型**：新功能  
- **摘要**：支持 MCP 资源引用、图片 blob 作为原生附件、添加 `list_mcp_resources`/`read_mcp_resource` 工具。  
- **链接**：https://github.com/anomalyco/opencode/pull/31940

### 8. #31933 [CLOSED] 隐藏 Windows 选定应用子进程
- **类型**：Bug 修复  
- **摘要**：修复使用选定应用打开文件时可能产生多余子进程窗口的问题。  
- **链接**：https://github.com/anomalyco/opencode/pull/31933

### 9. #31929 [CLOSED] 修复 Codex OAuth 不遵守 OpenAI baseURL
- **类型**：Bug 修复  
- **摘要**：确保 ChatGPT 订阅/Codex OAuth 请求使用用户配置的 `provider.openai.options.baseURL`。  
- **链接**：https://github.com/anomalyco/opencode/pull/31929

### 10. #31922 [CLOSED] 限制 SSE 事件积压并断开僵死消费者
- **类型**：Bug 修复 / 性能  
- **摘要**：为每个订阅者设置 SSE 事件缓冲区上限，停止消费的连接将被自动断开，防止内存泄漏。  
- **链接**：https://github.com/anomalyco/opencode/pull/31922

---

## 📊 功能需求趋势

从近期 Issues 中可提炼以下主要方向：

| 方向 | 代表 Issue | 社区热度 |
|------|------------|----------|
| **自动化与工作流** | YOLO 模式 (#8463)、/btw 命令 (#16992)、自动发现模型 (#6231) | ⭐⭐⭐⭐⭐ |
| **模型兼容与成本** | DeepSeek 价格调整 (#28846)、GPT-5.6 Luna 修复 (#36140) | ⭐⭐⭐⭐⭐ |
| **性能优化** | 多起高 CPU 报告 (#30086、#19466、#4804) | ⭐⭐⭐⭐ |
| **本地/离线体验** | Ollama Provider 挂起 (#22132)、本地 Whisper 输入 (PR#31955) | ⭐⭐⭐⭐ |
| **文档与生态** | llms.txt 支持 (#8816)、用户目录 (#36460) | ⭐⭐⭐ |

此外，`/btw` 和 `--dangerously-skip-permissions` 的高赞数表明，开发者希望 OpenCode 更无缝地融入 CI/CD 和脚本化场景。

---

## 🛠 开发者关注点

### 🔴 痛点（高频反馈）
1. **CPU 占用过高**：多用户报告空闲或重试时 CPU 异常，严重拖慢开发体验。希望官方优先排查渲染引擎或轮询逻辑。
2. **模型访问兼容性**：GPT-5.6 Luna 通过 OAuth 报 404、本地 Ollama 挂起等问题说明新模型集成测试不足。
3. **日志与调试困难**：`--log-level DEBUG` 在日志文件超过 10 个时失效（#17846），影响排障。
4. **会话管理异常**：会话不自动重命名（#36439）、重复消息（#27928）、初始消息丢失（#35988）等 UI/UX 问题。
5. **配置繁琐**：手动列出所有模型（#6231）是用户最大期待改进点。

### ✅ 期望
- 提供更宽松的权限控制（YOLO 模式）以适配无人值守场景。
- 支持 `/btw` 等快捷命令提升交互效率。
- 提供标准化文档格式（llms.txt）以利于 AI 工具集成。
- 自动发现 Provider 模型，降低配置心智负担。

---

*日报基于 GitHub 仓库 [anomalyco/opencode](https://github.com/anomalyco/opencode) 数据生成，统计时间截止 2026-07-11 23:59 UTC。*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 | 2026-07-12

**数据来源**：[github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)

---

## 今日速览

- **夜版发布**：`v0.19.8-nightly.20260711` 修复了 YOLO 模式下模型调用 `enter_plan_mode` 时不再丢失 YOLO 状态，并新增 CLI 前端 `ask_user` 转发功能。
- **多工作区 (multi-workspace) 成为核心议题**：RFC #6378 讨论热烈（20条评论），且多个关联 PR 和 Issue（#6646、#6726、#6745）正在推进工作区动态增删、会话组织等能力。
- **Session 恢复与稳定性修复密集**：Daemon 重启后的会话恢复、中断会话区分、`tool_use` 缺失报错、聊天记录持久化等问题均有 PR 和 Issue 推进，可见项目在打磨可靠性和体验一致性。

---

## 版本发布

### v0.19.8-nightly.20260711.0ef3a76bd

- **修复**：`fix(core): keep YOLO mode when the model calls enter_plan_mode` – 防止模型在 YOLO 模式下自动进入 Plan 模式，保持用户设定的审批级别。
- **新增**：`feat(cli): forward ask_user` – 命令行支持将用户交互提示转发至前端（如 ACP/WebShell），增强多端协作。

---

## 社区热点 Issues（10 条）

### 1. [RFC] 支持单个 daemon 管理多个工作区（#6378）
- **链接**：https://github.com/QwenLM/qwen-code/issues/6378
- **评论**：20 | **状态**：OPEN
- **为什么重要**：这是多工作区功能的基础设计 RFC，当前模型是“1 daemon = 1 workspace × N sessions”，社区希望能在不破坏现有单工作区行为的前提下，实现多工作区并存。评论中讨论了会话隔离、API 路径、扩展管理等内容，是近期最热争议点。

### 2. JetBrains ACP 未转发用户 Prompt（#6581）
- **链接**：https://github.com/QwenLM/qwen-code/issues/6581
- **评论**：8 | **状态**：CLOSED
- **为什么重要**：用户使用 Ollama/Qwen 作为 IntelliJ 的 AI 助手时，ACP 只发送了 bootstrap 上下文，未包含用户输入的 prompt。影响面大（IDE 集成用户众多），已关闭但需关注后续是否完全解决。

### 3. macOS 独立安装版 Ctrl+V 粘贴图片失效（#6590）
- **链接**：https://github.com/QwenLM/qwen-code/issues/6590
- **评论**：5 | **状态**：CLOSED
- **为什么重要**：macOS 用户通过 standalone 安装包使用时，CLI 无法粘贴剪贴板图片，原因是缺少原生模块 `@teddyzhu/clipboard`。已标记 `welcome-pr`，社区可贡献修复。

### 4. tool_use 缺少对应 tool_result 导致 API 错误（#6654）
- **链接**：https://github.com/QwenLM/qwen-code/issues/6654
- **评论**：5 | **状态**：CLOSED
- **为什么重要**：生产环境关键错误，当工具调用结果未及时返回时会报 `messages.24: tool_use ids were found without tool_result blocks`。影响对话连贯性，修复后将提升工具链稳定性。

### 5. MCP HTTP 传输遇到 401 时未触发 OAuth 恢复（#6639）
- **链接**：https://github.com/QwenLM/qwen-code/issues/6639
- **评论**：3 | **状态**：CLOSED
- **为什么重要**：使用 `.mcp.json` 配置的 MCP 服务器若返回 HTTP 401，Qwen Code 不会自动执行 OAuth 流程，导致服务器显示为“离线”。此问题阻碍了企业级外部工具的集成。

### 6. YOLO 模式自动进入 Plan 模式回归（#5970）
- **链接**：https://github.com/QwenLM/qwen-code/issues/5970
- **评论**：5 | **状态**：CLOSED
- **为什么重要**：用户用 `qwen -y` 启动 YOLO 模式后，模型仍会自动切换为 Plan 模式并询问权限，破坏了 YOLO 的“只管执行”预期。最新夜版虽已修复，但说明该问题易反复，需持续关注。

### 7. 延迟工具发现导致 Prompt 缓存前缀失效（#6721）
- **链接**：https://github.com/QwenLM/qwen-code/issues/6721
- **评论**：4 | **状态**：OPEN
- **为什么重要**：当模型调用隐藏工具时，Qwen Code 实际上会修改 `GeminiClient.setTools()`，这破坏了 prompt 缓存前缀，降低响应速度。影响长对话性能，社区正在讨论延迟工具发现架构改进。

### 8. 托管内存内容被微压缩清除（#6713）
- **链接**：https://github.com/QwenLM/qwen-code/issues/6713
- **评论**：3 | **状态**：CLOSED
- **为什么重要**：`managed-memory` 主题文件内容在离开工具结果窗口后被替换为 `[Old tool result content cleared]`，导致模型丢失持久记忆。影响需要长期记忆的场景（如项目知识库）。

### 9. WebShell 支持会话中断后自动继续（#6695）
- **链接**：https://github.com/QwenLM/qwen-code/issues/6695
- **评论**：3 | **状态**：OPEN
- **为什么重要**：WebShell 用户当前无法在环境重启后自动恢复未完成的对话回合。该功能是 WebShell 完善体验的关键需求，与 daemon 恢复机制紧密相关。

### 10. 审批模式切换 UI 中英文混杂（#6582）
- **链接**：https://github.com/QwenLM/qwen-code/issues/6582
- **评论**：3 | **状态**：CLOSED
- **为什么重要**：切换 Plan/Auto/YOLO 模式时，状态栏提示部分英文部分中文，影响非英文用户的使用体验。已标记 `welcome-pr`，适合本地化贡献。

---

## 重要 PR 进展（10 条）

### 1. Extension Management v2（#6638）
- **链接**：https://github.com/QwenLM/qwen-code/pull/6638
- **状态**：OPEN
- **内容**：为 `qwen serve` 引入扩展管理 V2，支持工作区级别的扩展激活策略。多工作区功能的基石。

### 2. 默认超时设置 for 前台 shell 命令（#6628）
- **链接**：https://github.com/QwenLM/qwen-code/pull/6628
- **状态**：OPEN
- **内容**：新增 `tools.shell.defaultTimeoutMs` 配置项，允许用户自定义 shell 工具默认超时，提高可控性。

### 3. 修复 WebShell 分视图无法显示跨工作区会话（#6746）
- **链接**：https://github.com/QwenLM/qwen-code/pull/6746
- **状态**：OPEN
- **内容**：多工作区 daemon 下，Split View “添加会话”选择器和 session overview 只显示主工作区会话。此 PR 修复该问题。

### 4. 忽略目标评估中的推理内容（#6738）
- **链接**：https://github.com/QwenLM/qwen-code/pull/6738
- **状态**：OPEN
- **内容**：防止模型隐藏的推理文本污染 `/goal` 评估的 JSON 裁决，提升目标评估准确性。

### 5. 添加 `/reload-env` 命令（#6707）
- **链接**：https://github.com/QwenLM/qwen-code/pull/6707
- **状态**：OPEN
- **内容**：允许用户不重启 CLI 即可热加载 API Key 和环境变量，提升开发效率。

### 6. 集成 `zvec-grep` 语义搜索工具（#6096）
- **链接**：https://github.com/QwenLM/qwen-code/pull/6096
- **状态**：OPEN（持续更新）
- **内容**：提供语义搜索和精确搜索两种模式，支持代码发现，将对大型代码库的导航产生重大影响。

### 7. MCP OAuth 恢复修复（#6732）
- **链接**：https://github.com/QwenLM/qwen-code/pull/6732
- **状态**：CLOSED
- **内容**：修复 Streamable HTTP MCP 服务器遇到 401 时无法触发 OAuth 恢复的问题，已合并到主线。

### 8. Daemon 重启后恢复频道会话（#6680）
- **链接**：https://github.com/QwenLM/qwen-code/pull/6680
- **状态**：CLOSED
- **内容**：在 daemon 或频道 worker 重启后保留频道对话，避免会话丢失。提升服务可靠性。

### 9. 增加无效模型流重试次数（#6712）
- **链接**：https://github.com/QwenLM/qwen-code/pull/6712
- **状态**：CLOSED
- **内容**：将短暂无效模型流的重试预算从 2 次增加到 4 次，同时保留线性回退逻辑，减少网络波动导致的失败。

### 10. 聊天记录持久化失败可见性（#6743）
- **链接**：https://github.com/QwenLM/qwen-code/pull/6743
- **状态**：OPEN
- **内容**：当 JSONL 写入失败时，明确停止对应 recorder 并保留错误链供 `flush()` 检查，防止静默丢记录。

---

## 功能需求趋势

1. **多工作区支持**：从 RFC 到多个关联 PR (workspace removal, session organization, transcript reader)，社区对在单个 daemon 下管理多个项目目录的需求急剧上升。
2. **WebShell 体验增强**：大量 feature request 集中在 WebShell 上——工具栏添加工作区选择器、Git 分支显示、会话组自定义颜色、自动继续中断会话等，说明 WebShell 正在从实验性走向主力 UI。
3. **Session 恢复与持久化**：daemon 重启后会话丢失、聊天记录写入失败、微压缩清除记忆等问题受到高频关注，反映出社区对稳定性和数据可靠性的高要求。
4. **IDE 集成与 ACP**：JetBrains 用户 prompt 未转发、MCP OAuth 恢复、ACP 中 tool_use/tool_result 校验等问题表明工具链与企业级开发环境的集成仍在深化。
5. **新模型适配**：Claude Opus 4.6–4.8 的 token 限制错误（#6734、#6719）、DashScope 模型返回 `<think>` 标签（#6666）等 Issue 显示社区积极尝试新模型，但兼容性细节仍需打磨。

---

## 开发者关注点

- **macOS 独立安装包原生模块缺失** (#6590)：粘贴图片功能因缺少 `@teddyzhu/clipboard` 模块而失效，影响 macOS 用户的工作流。
- **审批模式切换时中英文混杂** (#6582)：体验不一致，本地化社区可低成本贡献修复。
- **模型输出流不稳定** (#6670, #6712)：DashScope/Qwen 模型偶现空响应，虽增加了重试次数，但根源仍待解决。
- **聊天记录写入异步导致数据丢失** (#6742)：当前将入队视为成功，若队列写入失败则记录丢失，PR #6743 正在改进。
- **延迟工具发现破坏 Prompt Cache** (#6721)：性能敏感用户应关注后续架构调整。

---

*日报自动生成于 2026-07-12，基于 GitHub 公开数据。*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*