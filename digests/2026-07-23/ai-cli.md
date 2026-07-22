# AI CLI 工具社区动态日报 2026-07-23

> 生成时间: 2026-07-22 22:35 UTC | 覆盖工具: 7 个

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

好的，作为专注于 AI 开发工具生态的资深技术分析师，基于您提供的 2026-07-23 社区动态摘要，我为您整理了以下横向对比分析报告。

---

### AI CLI 工具横向对比分析报告 (2026-07-23)

#### 1. 生态全景

当前 AI CLI 工具生态正经历从“功能探索”到“稳定落地”的阵痛期。各大工具均面临着**稳定性与性能**（如 Windows 平台卡顿、空闲资源消耗）、**安全与可用性平衡**（安全过滤误报、破坏性操作风险）以及**子代理编排可靠性**（假阳性成功、无限挂起）这三大核心挑战。各工具在快速迭代新功能的同时，社区反馈的核心矛盾已从“缺少什么功能”转向“现有功能能否可靠工作”，预示着行业竞争已进入比拼工程质量和用户体验的深水区。

#### 2. 各工具活跃度对比

| 工具 | 热点 Issues 数 | 重要 PR 数 | 版本发布 | 核心社区焦点 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 10 | 10 | v2.1.218 | 模型行为（Fable 5 误报）、资源消耗、数据安全 |
| **OpenAI Codex** | 10 | 10 | 4个 Rust Alpha 版本 | Windows 稳定性、WSL 集成、会话控制 |
| **Gemini CLI** | 10 | 10 | v0.53.0-preview.0 | 子代理行为、无限挂起、A2A 安全 |
| **Copilot CLI** | 10 | 1 (无效) | v1.0.74-2 | PDF 支持、回归 bug、认证问题 |
| **Kimi Code** | 3 | 0 | 无 | API 速率限制、MCP 兼容性、Win 编码 |
| **OpenCode** | 10 | 10 | 无 | Go 订阅大面积故障、模型发现 |
| **Qwen Code** | 10 | 10 | v0.20.0-preview.0 | CI 全红、版本检查失效、SubAgent 兼容性 |

#### 3. 共同关注的功能方向

尽管各工具生态存在差异，但多个社区不约而同地关注着以下几个方向：

- **子代理/多智能体编排的可靠性与可观测性**
    - **具体诉求**：子代理因 `MAX_TURNS` 中断却报告成功（**Gemini CLI**），进程资源泄漏（**Copilot CLI**），指令泄漏到所有子代理（**Claude Code**），以及缺乏对子代理行为的顶层协调（**OpenCode**）。开发者希望系统能清晰报告任务状态、资源消耗和失败原因。
- **安全与可用性的精细化平衡**
    - **具体诉求**：安全过滤过度敏感，误杀正常操作，如阻止凭证认证的 API 调用（**Claude Code**）、将 `git status` 识别为风险（**OpenAI Codex**）、在 Plan 模式下拦截只读命令（**Copilot CLI**）。社区渴望可配置、更智能的风险判断，而非一刀切的阻拦。
- **性能与资源消耗优化**
    - **具体诉求**：桌面端空闲时 CPU 及磁盘占用异常（**Claude Code**、**OpenAI Codex**），子进程僵尸进程累积（**Copilot CLI**），等待 API 限速时 CPU 占用过高（**OpenCode**）。资源管理效率成为影响用户留存的关键。
- **跨平台体验一致性（尤其是 Windows）**
    - **具体诉求**：桌面应用卡顿/崩溃（**OpenAI Codex**、**Copilot CLI**），WSL 路径与进程问题（**OpenAI Codex**），终端编码问题（**Kimi Code**），以及 VS Code Remote-SSH 兼容性（**OpenAI Codex**）。Windows 生态的体验短板已成为所有工具的共性问题。

#### 4. 差异化定位分析

- **Claude Code**: 定位为“高级个体开发者助理”，强调深度自动化工作流（如 `/code-review` 后台化）和模型能力（Fable 5）。社区议题高度聚焦于模型行为、安全审计等前沿场景，用户专业度较高。
- **OpenAI Codex**: 定位为“全栈平台”，不仅是 CLI，更是桌面 App 和 VS Code 扩展。其社区反馈更偏向**基础平台性能和稳定性**，特别是对 Windows 和 WSL 的适配，说明其目标用户群体更广，但也带来了更复杂的兼容性问题。
- **Gemini CLI**: 定位是“代理生态构建者”，重点在 A2A 协议、子代理编排和 LLM triage。问题多集中在**子代理行为和状态管理**的哲学性设计缺陷上，如假阳性成功。技术路线更具前瞻性，但稳定性待提升。
- **GitHub Copilot CLI**: 定位是“GitHub 深度集成与安全门禁”，既有传统 CLI 特性，又强调 Plan 模式和安全沙箱。社区需求呈现两极分化：**基础功能缺失**（PDF 阅读）与**高级认证/安全**问题（BYOK、Plan 误判）。
- **Kimi Code** & **Qwen Code**: 两者均代表非西方主流模型的 CLI 探索。**Kimi Code** 社区较小，问题停留在 API 兼容性和编码基础适配，尚未进入核心功能打磨阶段。**Qwen Code** 则展现出更强的工程能力，处理着子代理兼容性、CI 稳定性等更复杂的问题，并积极跟进“Goal v3”等前沿协议。
- **OpenCode**: 定位为“开源聚合平台”，支持多种模型提供商。其社区最大的单一事件（Go 订阅 401）揭示了依赖外部服务的脆弱性。同时，其用户在模型管理和 TUI 上的高赞需求（如模型自动发现）体现了开源社区对灵活性和控制权的极致追求。

#### 5. 社区热度与成熟度

- **高话题度与成熟度**：**Claude Code** 和 **OpenAI Codex** 社区讨论深入，问题种类多，覆盖性能、安全、功能、模型等各个层面，反映出用户基础庞大且使用场景复杂。它们正从“快速增长”向“成熟稳定”转型。
- **高活跃度但处于快速成长期**：**Gemini CLI**、**GitHub Copilot CLI** 和 **OpenCode** 社区非常活跃，但问题集中在**基础功能缺失**、**架构级 Bug** 或 **重大使用故障**上，表明它们仍在快速迭代，解决早期核心痛点的阶段。
- **低活跃度但具潜力的探索者**：**Kimi Code** 社区活跃度低，问题较少，可能处于早期用户积累或热度下降阶段。**Qwen Code** 社区在工程问题（CI、Bug）上的讨论很活跃，但功能需求讨论较少，可能更侧重于技术层而非用户层。

#### 6. 值得关注的趋势信号

- **“稳定性溢价”时代到来**：当各工具都能实现“写代码”的基本功能时，**平台稳定性、跨平台一致性、执行的可预测性**将取代功能数量，成为用户选择的核心决策因素。任何数据丢失、进程挂起、资源泄漏等行为都将严重损害品牌信任。
- **子代理/多 Agent 系统的“可靠性鸿沟”**：所有工具都在推进多 Agent 编排，但社区反馈表明，**缺乏可靠的终止状态、任务委派逻辑和资源隔离机制**是普遍短板。谁能率先解决“子代理编排”的可靠性和可观测性问题，谁就能在 AI 驱动的复杂工作流市场中占据制高点。
- **“安全”成为双刃剑**：过于激进的安全过滤正在反噬用户体验，从“保护者”变成“阻碍者”。未来 AI CLI 的安全策略必须向**更智能、更透明、更可配置**的方向演进，例如区分自动模式和人工审核模式，根据操作风险等级提供不同粒度的干预。
- **数据主权与隐私成为新战场**：从 OpenCode 的 Go 订阅故障到 Qwen Code 的环境变量泄漏修复，再到许多工具对 BYOK（自带密钥）支持的不稳定，表明**用户对 AI 服务的数据流动和成本消耗日益敏感**。支持本地优先、提供精细的成本与数据审计能力，将成为下一阶段的关键竞争力。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，这是基于您提供的 GitHub 数据生成的 Claude Code Skills 社区热点报告。

---

## Claude Code Skills 社区热点报告（数据截至 2026-07-23）

### 一、热门 Skills 排行（Top 8 by PR 热度）

以下是根据 Pull Requests 的评论活跃度（按排序顺序）筛选出的社区最关注的 Skills 动态：

1.  **`color-expert` (PR #1302)**
    *   **功能**：一个全面的颜色专业知识技能，涵盖 ISCC-NBS、Munsell、RAL 等多个颜色命名系统，并指导在不同场景下使用合适的色彩空间（如 OKLCH、OKLAB、CAM16）。
    *   **社区讨论热点**：该技能知识密度高，社区期待它能作为 Claude 的“颜色百科全书”，解决 AI 生成设计中色彩不准确的问题。
    *   **当前状态**：Open

2.  **`self-audit` (PR #1367)**
    *   **功能**：提出了一个“推理质量门”理念，在 AI 输出交付前进行机械文件验证和四维推理审计（按损害严重程度排序）。自称是通用技能，适用于任何项目。
    *   **社区讨论热点**：这是对 AI 输出质量控制的前沿探索，社区围绕其“预任务校准 - 对抗性审查 - 交付验证”的三门管线（Issue #1385）进行了深入讨论。
    *   **当前状态**：Open

3.  **`document-typography` (PR #514)**
    *   **功能**：专注于 AI 生成文档的排版质量，解决孤字成行、寡妇段落（标题在页底孤立）和编号不对齐等常见问题。
    *   **社区讨论热点**：该技能直击 AI 文档生成中最常见、最“隐形”的用户痛点，被认为是提升输出专业度的必备工具。
    *   **当前状态**：Open

4.  **`odt` (PR #486)**
    *   **功能**：增加对 OpenDocument 格式（.odt, .ods）的支持，实现文档创建、模板填充和 ODT 到 HTML 的转换。
    *   **社区讨论热点**：满足了政府、教育及开源社区对开放标准文档格式的核心需求，是生态系统多样性的重要补充。
    *   **当前状态**：Open

5.  **`testing-patterns` (PR #723)**
    *   **功能**：提供了一套全面的测试技能，涵盖测试哲学（测试奖杯模型）、单元测试、React 组件测试、E2E 测试和快照测试等。
    *   **社区讨论热点**：社区普遍认为这是提升 AI 生成代码质量的关键技能，讨论焦点在于如何让技能指导足够具体，以确保 Claude 能独立完成有效的测试编写。
    *   **当前状态**：Open

6.  **`pyxel` (PR #525)**
    *   **功能**：新增用于 Pyxel 复古游戏引擎的技能，为 Claude 接入 `pyxel-mcp` 服务器，实现从写代码到运行、截图、迭代的完整开发工作流。
    *   **社区讨论热点**：该技能展示了 MCP 集成的新模式，社区对其在创意编程和教育领域的应用充满期待。
    *   **当前状态**：Open

7.  **`frontend-design` (PR #210)**
    *   **功能**：对现有的前端设计技能进行重构，提升指令的清晰度、可操作性和内部一致性，确保每一条指令都能被 Claude 单次对话执行。
    *   **社区讨论热点**：社区非常关注 Skil l 本身的“质量”，即如何写出更高效、更不模糊的提示词。此 PR 是社区自发优化已有技能的标杆。
    *   **当前状态**：Open

8.  **`skill-quality-analyzer` & `skill-security-analyzer` (PR #83)**
    *   **功能**：提交了两个“元技能”，用于评估其他技能的质量（结构、文档、可维护性）和安全性（识别潜在的滥用风险）。
    *   **社区讨论热点**：与社区对安全与质量的整体关切高度相关（见 Issue #492），这两个技能被视为建立社区标准和信任的重要工具。
    *   **当前状态**：Open

### 二、社区需求趋势 (从 Issues 提炼)

1.  **安全与信任**：社区最强烈的声音来自于对**信任边界**的担忧（Issue #492）。用户在 `anthropic/` 命名空间下发现社区贡献的技能，担心这可能导致权限滥用。**建立官方与非官方技能的清晰标识和审查机制是核心需求。**
2.  **企业级工作流**：对**组织级技能共享**（Issue #228）的呼声很高。当前手动导出/导入 `.skill` 文件的方式效率低下，企业用户急需共享库或链接分享功能。
3.  **开发者工具链稳定性**：大量 Issue（如 #556, #1169, #1061）指向 `skill-creator` 工具集的问题，特别是 `run_eval.py` 在 Windows 和 Mac 上的**0% 触发率** bug。这表明社区中的技能贡献者（高阶用户）正因工具链不稳定而受阻。
4.  **智能体治理与记忆**：社区正在探索更深层的 AI 行为控制，例如 `agent-governance`（Issue #412，安全模式）和 `compact-memory`（Issue #1329，紧凑符号记忆）。这表明用户不再满足于单一技能，而开始要求**管理 AI 行为模式**（需要将 Cursorrules 转换为 Skills?）。

### 三、高潜力待合并 Skills（近期可能落地）

以下 PR 评论活跃、解决了核心痛点，且已完成初步代码，有望近期合并：

1.  **#1298 & #1323 & #1099 & #1050**：一整套针对 `skill-creator` 的跨平台修复，特别是**修复 Windows 兼容性**和**修复 `run_eval.py` 的 0% 召回率**。这是当前开发者工具链中最大的痛点和阻塞项，合并优先级极高。
2.  **#1367 `self-audit`**：提出了一个非常有前景的“输出质量门”概念，概念创新且讨论深入。虽复杂，但若落地将深刻改变 Skills 的使用方式。
3.  **#514 `document-typography`**：解决了一个具体而普遍的用户体验缺陷，代码结构清晰，功能独立，预计很快会通过审查。
4.  **#1302 `color-expert`**：内容扎实、独立性强，作为一个垂直领域的专家知识库，几乎没有争议，合并概率很高。

### 四、Skills 生态洞察

**一句话总结：社区正经历从“量”到“质”的阵痛期——最集中的诉求并非创造更多炫酷功能，而是迫切要求修复 skill-creator 开发者工具链的跨平台稳定性与安全信任机制，为整个生态的健康扩展奠定基础。**

---

好的，作为专注于 AI 开发工具的技术分析师，以下是为您整理的 2026 年 7 月 23 日 Claude Code 社区动态日报。

---

# Claude Code 社区动态日报 | 2026-07-23

## 今日速览

今日社区核心动态围绕 **性能与稳定性** 展开。新版本 `v2.1.218` 优化了 `/code-review` 工作流，使其在后台运行，不阻塞主对话。社区方面，大量有关 **Fable 5 模型误报** 和 **桌面端资源异常消耗** 的旧 Issue 被关闭，但讨论持续发酵。此外，一个关于 **多账号配置文件管理** 的实验性插件引起了社区关注，暗示了开发者对工作环境隔离的需求。

---

## 版本发布

### 📦 v2.1.218

**发布亮点**：改进了 `/code-review` 命令的执行方式，将其作为后台子代理运行。这意味着代码审查工作不再填充主对话，同时保留了连续斜杠命令作为审查目标的功能，提升了会话的清晰度和并发处理能力。

---

## 社区热点 Issues

1.  **#28557 [BUG] ECONNRESET 网络连接问题** (已关闭)
    - **链接**: https://github.com/anthropics/claude-code/issues/28557
    - **重要性**: ⭐⭐⭐⭐⭐ | **评论数**: 18
    - **摘要**: 一个持续已久的老问题，用户反馈在网络不稳定的环境中频繁出现 `ECONNRESET` 错误，导致会话中断。虽然被标记为“陈旧”并关闭，但其 18 条评论表明该问题影响范围广，社区强烈期望 Anthropic 能从根本上优化网络重连机制。

2.  **#78933 [BUG] 桌面版远程控制功能无法连接** (开放中)
    - **链接**: https://github.com/anthropics/claude-code/issues/78933
    - **重要性**: ⭐⭐⭐⭐⭐ | **评论数**: 7
    - **摘要**: **桌面应用**用户在使用 `/remote-control` 时遇到致命错误，根本无法连接。这是新近出现且持续开放的高影响力问题，会严重影响依赖该功能的远程开发工作流，社区关注度极高。

3.  **#58799 [BUG] Windows 桌面版空闲时 CPU 和磁盘写入异常** (已关闭)
    - **链接**: https://github.com/anthropics/claude-code/issues/58799
    - **重要性**: ⭐⭐⭐⭐ | **评论数**: 7
    - **摘要**: 用户揭露了 Windows 桌面客户端在闲置时，因使用 TanStack Query 的 `persistQueryClient` 导致整个会话缓存被频繁重写（约 45MB），造成约 25% 的 CPU 占用和 5MB/s 的磁盘持续写入。此问题虽然被标记为“陈旧”，但揭示了应用资源管理上的严重缺陷。

4.  **#80351 [BUG] Fable 模型固执地“纠正”用户正确输入** (开放中)
    - **链接**: https://github.com/anthropics/claude-code/issues/80351
    - **重要性**: ⭐⭐⭐⭐ | **评论数**: 1
    - **摘要**: 这是一个新报告的问题，用户抱怨 Fable 模型在与事实或记忆冲突时，会固执地反驳和“纠正”用户，忽略了用户的正确输入。这触及了 AI 对话的核心体验问题，如果普遍存在，将是 Fable 模型的一个重大缺陷。

5.  **#46444 [BUG] 工作树自动清理导致数据永久丢失** (已关闭)
    - **链接**: https://github.com/anthropics/claude-code/issues/46444
    - **重要性**: ⭐⭐⭐⭐ | **评论数**: 6
    - **摘要**: **非常严重的问题！** 用户报告 Claude Code 的“工作树自动清理”功能，在没有弹出任何警告的情况下，永久删除了 10 天未提交的项目工作。这直接涉及到数据安全，尽管被关闭，但该问题理应引起所有开发者的警惕。

6.  **#67696 [BUG] 过度严格的安全过滤阻止凭证认证的 API 调用** (已关闭)
    - **链接**: https://github.com/anthropics/claude-code/issues/67696
    - **重要性**: ⭐⭐⭐⭐ | **评论数**: 5
    - **摘要**: 用户指出 Claude Code 的安全过滤器过于激进，甚至会阻止由 Claude 自己生成的、需要凭证的 `curl` 请求。这严重限制了“自动模式”的实际可用性，使得 AI 无法自主执行一些合法的带认证操作。

7.  **#66419 [BUG] “用 Opus 规划”指令泄漏到所有子代理** (已关闭)
    - **链接**: https://github.com/anthropics/claude-code/issues/66419
    - **重要性**: ⭐⭐⭐ | **评论数**: 5
    - **摘要**: 用户发现，当指示“用 Opus 规划，按需使用工作流”时，模型会将 `model: 'opus'` 错误地应用到所有后续的子代理调用上，而不仅仅是规划阶段。这破坏了精细化的成本控制和工作流设计。

8.  **#56843 [FEATURE] 在状态栏添加沙盒模式指示** (已关闭)
    - **链接**: https://github.com/anthropics/claude-code/issues/56843
    - **重要性**: ⭐⭐⭐ | **评论数**: 6
    - **摘要**: 社区强烈希望能在状态栏中直观地看到当前会话是否开启了沙盒模式（Docker、本地或无）。这是一个提升用户体验和会话透明度的有用功能，表明用户越来越重视安全隔离环境的管理。

9.  **#62308 [BUG] macOS 下 Claude Code 进程空闲时 100% 占用 CPU** (已关闭)
    - **链接**: https://github.com/anthropics/claude-code/issues/62308
    - **重要性**: ⭐⭐⭐ | **评论数**: 6
    - **摘要**: macOS 用户反映，Claude Code 的后台进程在空闲状态时持续占用 100% CPU，后经分析为 libuv 的 `uv_backend_timeout()` 在特定场景下卡死。这是一个典型的性能问题，尤其是在笔记本电脑上会严重影响续航和散热。

10. **#67578 [BUG] Pro 计划用户被错误地拦截，提示“使用 1M 上下文需要充值”** (已关闭)
    - **链接**: https://github.com/anthropics/claude-code/issues/67578
    - **重要性**: ⭐⭐⭐ | **评论数**: 2 (👍: 4)
    - **摘要**: 尽管只有2条评论，但获得了4个赞，表明此为**高共识问题**。Pro 计划用户在首次使用时被错误提示需额外付费才能使用 1M 上下文，这引发了关于计费系统和用户配额计算逻辑的广泛担忧。

---

## 重要 PR 进展

1.  **#80353 [docs] GCP 部署脚本增加校验和校验**
    - **链接**: https://github.com/anthropics/claude-code/pull/80353
    - **重要性**: ⭐⭐⭐⭐
    - **摘要**: 为 GCP 网关部署流程增加了**下载二进制文件的校验和检查**，一旦发现文件损坏或篡改将立即停止部署。这极大地增强了部署过程的安全性和可靠性。

2.  **#80326 [plugin] 实验性插件：多账户配置文件管理**
    - **链接**: https://github.com/anthropics/claude-code/pull/80326
    - **重要性**: ⭐⭐⭐⭐
    - **摘要**: 名为 `account-profiles` 的实验性插件，允许用户在同一台电脑上为个人、工作等不同 Claude 账户创建并管理独立的、隔离的 `CLAUDE_CONFIG_DIR` 启动环境。该功能直击许多跨账户开发者的痛点，内部反响积极。

3.  **#80008 [plugin] “twilight”插件：规范优先的设计/实现技能**
    - **链接**: https://github.com/anthropics/claude-code/pull/80008
    - **重要性**: ⭐⭐⭐⭐
    - **摘要**: 名为 `twilight` 的插件，提出了一种“规范优先”（spec-first）的开发策略，通过设计、实现和焦点堆栈（focus stack）的组合来提升 Claude Code 处理复杂功能的能力。虽然作者声明其为实验性演示，但其设计思路对高级用户极具启发性。

4.  **#80241 [fix] 修复控制台粘贴文本时自动滚动到顶部的问题**
    - **链接**: https://github.com/anthropics/claude-code/pull/80241
    - **重要性**: ⭐⭐⭐
    - **摘要**: 一个由机器人 Agent 自动提交的 PR，修复了当 Claude 在控制台追加文本时，控制台会自动滚动到历史顶部的恼人问题。此 PR 虽小，但直接提升了终端的日常使用体验。

5.  **#80196 [fix] 修复“自动压缩”功能在上下文已达 100% 时仍不触发的问题**
    - **链接**: https://github.com/anthropics/claude-code/pull/80196
    - **重要性**: ⭐⭐⭐
    - **摘要**: 修复了一个关键 Bug，即状态栏显示上下文使用率已达到 100%，但自动压缩机制从未被触发。这会导致会话因上下文溢出而中断，修复此问题对长会话至关重要。

6.  **#80195 [fix] 修复 Max 订阅用户“瞬间达到使用限制”的问题**
    - **链接**: https://github.com/anthropics/claude-code/pull/80195
    - **重要性**: ⭐⭐⭐
    - **摘要**: 针对 Max（最大）订阅用户报告的“瞬间达到使用限制”问题提出修复方案。此问题引起了社区对配额计算逻辑的严重质疑，此 PR 有望澄清并解决这个影响付费用户权益的根本性问题。

7.  **#80112 [fix] 增强开发容器防火墙对 DNS 解析失败的弹性**
    - **链接**: https://github.com/anthropics/claude-code/pull/80112
    - **重要性**: ⭐⭐⭐
    - **摘要**: 改进了 `.devcontainer/init-firewall.sh` 脚本，防止因个别域名 DNS 解析失败而导致整个防火墙设置脚本出错退出的问题。提升了环境初始化过程的健壮性。

8.  **#80294 [docs] 修复 1 个失效的外部链接**
    - **链接**: https://github.com/anthropics/claude-code/pull/80294
    - **重要性**: ⭐⭐
    - **摘要**: 常规文档维护，使用 Wayback Machine 的存档修复了 `README.md` 中一个指向 npm 包的失效链接。

9.  **#80229 [docs] 修复 1 个失效的外部链接**
    - **链接**: https://github.com/anthropics/claude-code/pull/80229
    - **重要性**: ⭐⭐
    - **摘要**: 同样是修复了 `README.md` 中的一个失效 npm 包链接，与 #80294 类似，表明文档中有多处相同链接未被统一更新。

10. **#80326 [plugin] 与 #80008 [plugin]** (已在上文 #2 和 #3 中列出)
    - **重要性**: ⭐⭐⭐⭐
    - **摘要**: 这两个 PR 代表着社区官方插件生态的萌芽，尤其是账户管理和规范优先编码的理念，预示了未来用户个性化的工作流定制方向。

---

## 功能需求趋势

1.  **模型行为与可靠性**：大量 Issue（如 #80351, #67732, #67737）集中反映了社区对 **Fable 5** 模型在**错误记忆、安全过滤误报、模型降级**等方面的不满。用户希望模型更准确、更遵循指令，而非因过度“安全”而导致功能受阻。
2.  **性能与资源消耗**：多个高赞 Issue（如 #58799, #62308）持续关注**客户端空闲时的高 CPU 和磁盘占用**。社区对桌面客户端，尤其是 Windows 和 macOS 版本的基础性能优化有极高期待。
3.  **权限与成本控制**：用户非常关心**权限模型的细粒度控制**（如 #56843 沙盒状态指示，#67371 权限允许列表失效）和**配额消耗的透明化**（如 #67673, #67578）。开发者需要更清晰、更可控的方式来管理 AI 的安全边界和预算。
4.  **工作流与自动化可靠性**：Agent 工作流的稳定性是核心痛点。Issue #66419（模型指令泄漏）和 #46444（数据丢失）表明，用户期待更**可预测、更安全**的自动化行为，特别是在涉及文件系统和子代理调用时。
5.  **国际化与本地化**：Issue #67724 (已关闭) 提出自动生成的会话标题应**支持用户设置的语言**（如日语）。这表明社区，尤其是非英语母语用户，对本地化体验有开始有明确的功能诉求。

---

## 开发者关注点

*   **Fable 5 模型的错误“纠正”与安全误报频发**：这是当前社区最大的痛点。开发者抱怨在进行安全审计、法律咨询、网络安全等工作时，模型会**频繁地因错误的安全原因而拒绝对话或降级模型**，严重影响了“自动模式”和高级模型的实际可用性。
*   **权限确认机制混乱**：开发者反映“自动模式”下的权限分类器（Auto-mode permission classifier）会**错误地阻止用户已经明确授权或存在于计划中的操作**（如 #67720），导致工作流频繁中断。同时，MCP 权限允许列表也存在被忽略的问题（如 #67371）。
*   **资源消耗异常与计费不透明**：Windows 桌面端及 macOS 端的**空闲高资源占用**问题持续被提及。更严重的是，“Pro 计划用户被错误拦截”和“Max 订阅瞬间达到限制”等计费问题引发了广泛的**不信任感**，开发者担心第三方 API 调用和会话管理存在隐蔽的成本陷阱。
*   **数据丢失风险**：`worktree auto-cleanup` **在不经警告的情况下删除用户未提交的工作**（#46444），这触及了所有开发者的红线。虽然该 Issue 被标记为陈旧，但其背后反映的“AI 代理的副作用缺乏安全护栏”问题，是社区持续关注的焦点。
*   **终端用户体验打磨不足**：诸如“Thinking 状态无进度指示”（#67706）、“控制台滚动错乱”（#80241）、“代码审查阻塞主对话”（已被 v2.1.218 修复）等问题，反映出产品在**基础交互的稳定性和信息透明度**上仍有提升空间。
*   **关键功能不稳定**：如“远程控制连接失败”（#78933）、“自动压缩不触发”（#80196）等关键功能的 `bug` 频繁出现，影响了依赖于这些高级特性的深度用户的工作流可靠性。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 | 2026-07-23

## 📰 今日速览

过去 24 小时内，Codex 发布了 4 个 Rust 相关的 alpha 版本（v0.146.0-alpha.1~3 以及 v0.145.0-alpha.30），持续迭代底层运行时。社区反馈集中指向 Windows 平台的性能与稳定性问题——多个高赞 Issue 描述了应用卡顿、WMI 进程高 CPU、WSL 路径断裂等痛点，而“禁用自动 resolve”的请求以 151 个 👍 成为最强呼声。同时，一批 bot 主导的 PR 正在优化分析管道、修复沙箱渲染和 SQLite 配置，暗示内部工程侧对可观测性与基础设施的重视。

---

## 🚀 版本发布

过去 24 小时内发布了以下 Rust 通道的 alpha 版本：

- **rust-v0.146.0-alpha.3** — Release 0.146.0-alpha.3  
- **rust-v0.146.0-alpha.2** — Release 0.146.0-alpha.2  
- **rust-v0.146.0-alpha.1** — Release 0.146.0-alpha.1  
- **rust-v0.145.0-alpha.30** — Release 0.145.0-alpha.30  

发布说明仅有版本号，未提供具体变更日志。推测涉及 Codex 底层 CLI/App Server 的持续迭代，可能与性能修复或新模型适配有关。

---

## 🔥 社区热点 Issues（10 条）

### 1. [#20214] Codex App 在 Windows 11 Pro 上频繁卡顿/卡死
- **作者**: @squarepots  
- **评论 72 | 👍 71**  
- **链接**: https://github.com/openai/codex/issues/20214  
- **重要性**: 极高，长期遗留问题，用户配备 Ryzen 5 + 32GB 内存仍频繁卡顿，影响到日常开发。社区要求优先解决 Windows 平台的渲染与进程调度。

### 2. [#28969] 请求增加禁用“60 秒自动 resolve”的配置项
- **作者**: @antoyo  
- **评论 53 | 👍 151**  
- **链接**: https://github.com/openai/codex/issues/28969  
- **重要性**: 当前最受社区支持的 Feature Request。用户希望手动控制何时“解决问题”，而不是强制等待自动超时。CLI 高频用户强烈需求。

### 3. [#16815] WSL Agent 模式报错：AbsolutePathBuf 反序列化缺少基础路径
- **作者**: @cc345  
- **评论 22 | 👍 13**  
- **链接**: https://github.com/openai/codex/issues/16815  
- **重要性**: 长期存在的 WSL 集成 bug，切换 Agent 环境时失败，影响 Business 用户。表明 WSL 路径处理仍需完善。

### 4. [#28015] 假阳性网络安全检测打断正常本地仓库维护
- **作者**: @jyongchul  
- **评论 22 | 👍 3**  
- **链接**: https://github.com/openai/codex/issues/28015  
- **重要性**: 社区反馈安全检测机制过于敏感，将常规的 git 操作（如状态检查、清理）识别为风险，频繁弹窗干扰工作流。需要调优安全策略。

### 5. [#34014] 独立 Windows 应用打开项目时导致 WMI Provider Host CPU 100%
- **作者**: @tmyAudience  
- **评论 18 | 👍 11**  
- **链接**: https://github.com/openai/codex/issues/34014  
- **重要性**: 性能类新报告，与 #20214 不同，此问题明确指向 WMI 进程占用，且 VS Code 扩展环境正常，说明桌面应用的监控循环实现有缺陷。

### 6. [#27597] VS Code 扩展在 Remote-SSH 中加载失败（空白侧栏）
- **作者**: @lucastdeoliveira1-bit  
- **评论 15 | 👍 4**  
- **链接**: https://github.com/openai/codex/issues/27597  
- **重要性**: Codex 扩展在 VS Code Remote-SSH 场景下不可用，影响远程开发用户。回滚版本可解决，说明新版本有回归。

### 7. [#24103] Meta Ads MCP OAuth 登录失败：invalid_client_metadata
- **作者**: @canorionen  
- **评论 14 | 👍 4**  
- **链接**: https://github.com/openai/codex/issues/24103  
- **重要性**: 官方 MCP 集成缺陷，阻止广告类工作流的 OAuth 流程。影响依赖 Meta Ads MCP 的营销开发者。

### 8. [#19001] 建议在 CLI 中集成 RTK（实时令牌缩减）以减少 60–90% Token 开销
- **作者**: @klondikemarlen  
- **评论 13 | 👍 15**  
- **链接**: https://github.com/openai/codex/issues/19001  
- **重要性**: 社区提出的高效 Token 优化方案，通过过滤 Shell 命令输出来节省成本。获得中高认可，但尚未被官方采纳。

### 9. [#17574] Subagent 泄漏 stdio MCP helper 进程树（xcodebuildmcp、chrome-devtools-mcp 累积）
- **作者**: @jaewon-kim-dev  
- **评论 12 | 👍 0**  
- **链接**: https://github.com/openai/codex/issues/17574  
- **重要性**: 进程泄漏 Bug，在 macOS 和 Windows 上均可能发生。虽无赞，但评论数高且为 Pro 用户报告，表明存在资源泄漏隐患。

### 10. [#20730] 自定义 Pets 在 WSL 环境中因路径标准化失败
- **作者**: @xIGBClutchIx  
- **评论 11 | 👍 20**  
- **链接**: https://github.com/openai/codex/issues/20730  
- **重要性**: Pets 功能在 WSL 下无法使用，获 20 个 👍，社区中有相当用户期待 Pets 跨平台完整支持。

---

## 📌 重要 PR 进展（10 条）

### 1. [#34835] 在 turn profile 中跟踪压缩时间（已合并）
- 添加 `compaction_ms` 到 turn profile 以及分析事件，将手动/自动压缩从空闲时间中独立测量。
- https://github.com/openai/codex/pull/34835

### 2. [#34831] 在进程内 app server 关闭前刷新分析队列（已合并）
- 修复分析事件（如完成回合、接受行）可能因服务器关闭而丢失的问题。
- https://github.com/openai/codex/pull/34831

### 3. [#31320] 检测缺少 trusted connector ID 的 MCP UI URI（已合并）
- 当工具拥有非空 UI resource URI 但缺少 trusted connector ID 时发射计数器，便于定位配置错误。
- https://github.com/openai/codex/pull/31320

### 4. [#31393] 向 Codex App 广播 MCP App UI 支持能力（已合并）
- 使得 MCP 服务器能区分支持 WebView 渲染的客户端与纯文本客户端，改进 UI 资源的路由。
- https://github.com/openai/codex/pull/31393

### 5. [#34827] 移除 Windows Bazel lint 工具链覆写（已合并）
- 停止强制指定 Windows 主平台用于 argument-comment-lint 构建，简化构建配置。
- https://github.com/openai/codex/pull/34827

### 6. [#34825] 减少构建 Responses 请求时的克隆（已合并）
- 优化工具定义序列化：共享 raw JSON，而非每次重建 JSON 树；增量 WebSocket 请求避免克隆完整 item 前缀。
- https://github.com/openai/codex/pull/34825

### 7. [#34824] 标准化 Guardian review cwd 重用键（已合并）
- 将会话工作目录存储为 `PathUri`，使重用比较使用规范 URI 表示，避免路径匹配差异。
- https://github.com/openai/codex/pull/34824

### 8. [#34823] 在非 Windows Bazel CI 中运行 code-mode 测试（已合并）
- 让 Linux/macOS CI 跑完整 code-mode 集成套件，Windows 仅排除不兼容测试。
- https://github.com/openai/codex/pull/34823

### 9. [#34819] 跨 Codex 入口点启用 git attribution（已合并）
- 在 app server、MCP server、`codex debug prompt-input` 中安装 git attribution 扩展，确保工作区策略控制提交归因。
- https://github.com/openai/codex/pull/34819

### 10. [#31817] 自动更新 models.json（持续集成）
- 由 GitHub Actions 自动提交的模型列表更新，保持 Codex 对新模型的识别。
- https://github.com/openai/codex/pull/31817

---

## 🧠 功能需求趋势

从过去 24 小时的 Issue 与 PR 中可以提炼出以下社区重点关注方向：

| 趋势方向 | 说明 | 代表 Issue/PR |
|----------|------|---------------|
| **Windows 平台稳定性** | 卡顿、WMI 高 CPU、WSL 路径断裂、spellcheck 异常等大量 Windows 专属 bug 集中出现 | #20214 #34014 #34782 |
| **WSL 集成优化** | 子系统和路径处理（AbsolutePathBuf、自定义 Pets、SSH worktree 分组）持续被反馈 | #16815 #20730 #32082 |
| **MCP 协议与 UI 支持** | 官方 MCP 的认证、UI resource URI、trusted connector 等基础设施完善 | #24103 #31320 #31393 |
| **安全检测假阳性** | 网络安全检测频繁打断正常开发，用户期望更智能的风险判断 | #28015 #34725 |
| **资源与对话管理** | Subagent 泄漏、磁盘占用、侧边聊天持久化、会话自动 resolve 控制等 | #17574 #34061 #26227 #28969 |
| **Token 成本优化** | 减少提示占用的 token（如 RTK 建议），调用优化减少克隆 | #19001 #34825 |
| **远程开发体验** | VS Code Remote-SSH 扩展加载失败、PR 集成在 WSL 下失败 | #27597 #24601 #32323 |

---

## 🎯 开发者关注点

### 痛点汇总

- **Windows 卡顿与资源耗尽**：多款 Windows 11 Pro 机器上出现 Codex 桌面应用卡死、WMI Provider Host 占满 CPU、C 盘空间因 Subagent 日志暴涨等问题。
- **假阳性安全检测**：普通仓库维护操作（`git status`、`git clean`）被识别为“网络安全风险”，被迫弹窗中断付费会话，体验极差。
- **自动 resolve 机制不可控**：60 秒自动判断对复杂任务来说过于激进，用户希望有开关。
- **WSL 路径与进程问题**：WSL 环境下的路径序列化失败、自定义 Pets 加载失败、SSH worktree 不归组等高频报错。
- **VS Code Remote 兼容性**：扩展在 Remote-SSH 中空白侧栏、回滚旧版才能使用，说明持续集成存在回归。
- **MCP 登录配置困难**：官方 Meta Ads MCP OAuth 流程因 `invalid_client_metadata` 卡死在第一步。

### 高频诉求

- **提供全局/子代理的模型配置**（#19482）  
- **持久化侧边聊天到主线程**（#26227）  
- **支持 Ultra 预算或恢复 5 小时限制**（#34822）  
- **在 CLI 级别集成 RTK 减少 token 浪费**（#19001）  

以上动态反映了 Codex 社区对**跨平台稳定性、安全检测精度、会话控制灵活性**的强烈期待。建议开发团队优先聚焦 Windows 性能优化与 WSL 集成修复，同时考虑引入社区成熟的 Token 节省方案。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-07-23

## 📌 今日速览
昨日发布 **v0.53.0-preview.0**，主要修复 A2A 协议中工具响应分组与角色合并问题，并引入 LLM triage 编排器。安全方面，**v0.52.0-nightly** 针对 A2A 服务器执行了 RCE 漏洞修复。社区对子代理在达到最大轮次后错误报告为“GOAL 成功”的 Bug（#22323）以及通用代理无限挂起问题（#21409）讨论热烈，开发者高度关注。

---

## 📦 版本发布

- **[v0.53.0-preview.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.53.0-preview.0)**  
  修复了 A2A 场景下已取消工具响应的分组及连续角色合并以预防 400 错误；新增基于 LLM 的 triage 编排器及容器构建。

- **[v0.52.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.52.0)**  
  重构：从工作区上下文中排除临时 CI 配置文件；新增 triage worker 核心模块。

- **[v0.52.0-nightly.20260722](https://github.com/google-gemini/gemini-cli/releases/tag/v0.52.0-nightly.20260722.gc776c665b)**  
  安全修复：强制 A2A 服务器进行工作区信任检查和任务隔离，防止远程代码执行（RCE）。

---

## 🔥 社区热点 Issues

### 1. 子代理达到最大轮次后误报成功 (#22323)
**链接**：[#22323](https://github.com/google-gemini/gemini-cli/issues/22323)  
**标签**：priority/p1, kind/bug  
子代理 `codebase_investigator` 在因 `MAX_TURNS` 中断后报告 `status: "success"` 和 `Termination Reason: "GOAL"`，掩盖了真实的中断原因。社区讨论热烈（12 条评论），认为该行为会误导开发者信任错误的执行结果，需要重新设计终止状态传播逻辑。

### 2. 通用代理 (Generalist agent) 无限挂起 (#21409)
**链接**：[#21409](https://github.com/google-gemini/gemini-cli/issues/21409)  
**标签**：priority/p1, kind/bug  
用户报告每次 Gemini CLI 回退到通用代理时都会永久挂起（即使简单操作如创建文件夹）。临时解决方法是禁止模型委托子代理。8 条评论，8 个 👍，说明影响广泛。

### 3. 零依赖 OS 沙盒 & 意图路由 (#19873)
**链接**：[#19873](https://github.com/google-gemini/gemini-cli/issues/19873)  
**标签**：priority/p2, kind/enhancement  
提议利用 Gemini 3 模型原生的 bash 能力，通过零依赖沙盒实现安全执行，并在执行后根据意图路由结果。属于长期功能，8 条评论，受到社区认可。

### 4. 组件级评估框架 (#24353)
**链接**：[#24353](https://github.com/google-gemini/gemini-cli/issues/24353)  
**标签**：priority/p1, kind/customer-issue  
作为 #15300 的后续，已生成 76 个行为评估测试，但需要更鲁棒的组件级评估体系来覆盖更多场景。7 条评论，表明社区对质量保障的重视。

### 5. AST 感知文件读取与搜索 (#22745)
**链接**：[#22745](https://github.com/google-gemini/gemini-cli/issues/22745)  
**标签**：priority/p2, kind/feature  
探讨利用 AST 感知工具来更精确地读取方法边界、减少 token 噪音、提升导航效率。7 条评论，1 个 👍，开发者对减少回合数感兴趣。

### 6. 子代理使用不足 (#21968)
**链接**：[#21968](https://github.com/google-gemini/gemini-cli/issues/21968)  
**标签**：priority/p2, kind/bug  
用户反馈 Gemini CLI 几乎不会主动使用自定义 skill 和子代理，即使问题高度相关。6 条评论，建议改进代理规划和调用策略。

### 7. 自动记忆 (Auto Memory) 对低信号会话无限重试 (#26522)
**链接**：[#26522](https://github.com/google-gemini/gemini-cli/issues/26522)  
**标签**：priority/p2, kind/bug  
当提取代理跳过低信号会话时，该会话会永远停留在待处理状态，导致无限重试。5 条评论，需优化回溯机制。

### 8. Shell 命令执行后卡在“等待输入” (#25166)
**链接**：[#25166](https://github.com/google-gemini/gemini-cli/issues/25166)  
**标签**：priority/p1, kind/bug, effort/medium  
简单 shell 命令执行完成后，控制台仍显示“Awaiting user input”并无限挂起。4 条评论，3 个 👍，严重影响日常使用。

### 9. 浏览器代理锁恢复策略 (#22232)
**链接**：[#22232](https://github.com/google-gemini/gemini-cli/issues/22232)  
**标签**：priority/p3, kind/feature  
建议浏览器代理在遇到锁定的浏览器配置时尝试自动接管或恢复，而非直接失败。4 条评论，适合提升稳定性。

### 10. 确定性内容脱敏与减少日志 (#26525)
**链接**：[#26525](https://github.com/google-gemini/gemini-cli/issues/26525)  
**标签**：priority/p2, area/security, kind/bug  
Auto Memory 在读取本地记录后会将内容发送给模型，但脱敏指令执行在已发送之后，存在安全风险。3 条评论，需要前置脱敏与日志精简。

---

## 🚀 重要 PR 进展

### 1. 过滤推理部分（thought parts）以防上下文泄露 (#28509)
**链接**：[#28509](https://github.com/google-gemini/gemini-cli/pull/28509)  
当上下文管理禁用时，完全过滤掉历史中的 `thought: true` 内部独白部分，防止重复推理块泄露至后续请求。

### 2. 添加 `gemini-3.5-flash` 到模型选择器 (#28485)
**链接**：[#28485](https://github.com/google-gemini/gemini-cli/pull/28485)  
修复 v0.51.0 中用户无法在模型选择器中找到 `gemini-3.5-flash` 的问题。根源是旧路径只展示默认 Flash 模型，现已将所有有效模型加入列表。

### 3. 模型回退时轮转 Session ID 以防状态错误 (#28469)
**链接**：[#28469](https://github.com/google-gemini/gemini-cli/pull/28469)  
当永久回退到 `gemini-2.5-flash` 时自动轮换 session ID，避免 Code Assist 后端因同一 session 重试返回“请提交新查询”错误。

### 4. `/compress` 命令添加取消信号 (#28506)
**链接**：[#28506](https://github.com/google-gemini/gemini-cli/pull/28506)  
之前 `tryCompressChat` 未传递 `AbortSignal`，导致后台压缩无法取消。现创建 `AbortController` 并传递信号，用户可按 Esc 或启动新对话时取消。

### 5. OAuth 授权使用原生 fetch 避免“Premature close” (#28446)
**链接**：[#28446](https://github.com/google-gemini/gemini-cli/pull/28446)  
修复某些无头 VPS 上 `gemini login` 在 token 交换阶段因“Premature close”崩溃的问题。改用原生 fetch，避免对无法正常关闭连接的特定 HTTP 客户端依赖。

### 6. 策略引擎修复：tools.core 通配符 DENY 仅限内置工具 (#28499)
**链接**：[#28499](https://github.com/google-gemini/gemini-cli/pull/28499)  
`tools.core` 的通配符 DENY 规则错误地将所有 MCP 工具也排除在外。引入 `excludeMcp` 属性，将通配符规则范围限定为内置核心工具。

### 7. 文档修复：添加缺失的 `.md` 扩展名 (#28505)
**链接**：[#28505](https://github.com/google-gemini/gemini-cli/pull/28505)  
六处跨文档链接缺少 `.md` 扩展名且部分使用绝对路径，导致在 GitHub 渲染时返回 404。已全部修正。

### 8. 自动生成 v0.52.0 与 v0.53.0-preview.0 更新日志 (#28508, #28507)
**链接**：[#28508](https://github.com/google-gemini/gemini-cli/pull/28508)、[#28507](https://github.com/google-gemini/gemini-cli/pull/28507)  
机器人自动生成版本更新日志，供维护者审核合并。

### 9. 评估覆盖报告命令 (#28169 已合并)
**链接**：[#28169](https://github.com/google-gemini/gemini-cli/pull/28169)  
新增 `eval:coverage` 脚本，通过交叉引用评估库存工具列表与工具注册表，报告内置工具的测试覆盖率。

### 10. PR 生成器基础设施：Cloud Run Job 与 Workflows 配置 (#28431)
**链接**：[#28431](https://github.com/google-gemini/gemini-cli/pull/28431)  
为 SSR 代码生成流水线建立容器化运行时、Cloud Run Job 声明以及 Eventarc 触发的 Cloud Workflow 定义，为自动化 PR 生成铺路。

---

## 📊 功能需求趋势

- **子代理行为优化**：多篇 Issue 关注子代理主动使用不足（#21968）、未授权运行（#22093）、轨迹不可共享（#22598）等问题。
- **安全沙盒与执行控制**：零依赖 OS 沙盒（#19873）、破坏性操作防护（#22672）、A2A 服务器信任隔离（nightly 修复）体现了社区对安全执行的高度需求。
- **AST 感知工具**：文件读取与代码库映射的 AST 感知优化（#22745、#22746）被视为降低 Token 开销、提升准确率的关键方向。
- **评估与测试体系**：组件级评估（#24353）和评估覆盖率（#28169 PR）表明社区希望更全面的自动化质量保障。
- **记忆系统改进**：自动记忆的低信号会话处理（#26522）、脱敏机制（#26525）和无效补丁隔离（#26523）成为新的关注热点。
- **模型与提供者支持**：将 `gemini-3.5-flash` 纳入模型选择器（#28485）以及支持开源 LLM（#28498）反映了对模型灵活性的期待。

---

## 🧑‍💻 开发者关注点

- **子代理假阳性成功**：子代理因 `MAX_TURNS` 中断但报告成功（#22323）严重干扰调试，开发者希望明确区分正常完成与强制中断。
- **无限挂起与无响应**：通用代理挂起（#21409）和 Shell 命令结束后等待输入（#25166）是高频痛点，直接导致工具不可用。
- **浏览器代理兼容性**：Wayland 下失败（#21983）和设置覆盖忽略（#22267）使浏览器辅助场景不稳定。
- **配置与权限问题**：symlink 不被当作文本（#20079）、设置覆盖被忽略（#22267）、子代理未经授权运行（#22093）降低了配置系统的可靠性。
- **OAuth 登录失败**：特定环境下 “Premature close” 问题（#28446）阻碍新用户入门。
- **模型选择与版本回退**：用户找不到新模型（#28483）以及模型回退时 session 状态错误（#28469）影响了升级体验。

---

*数据来源：GitHub [google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli) 仓库（2026-07-22 UTC 更新）*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-07-23

## 📌 今日速览
- **Copilot CLI v1.0.74 连续发布两个补丁**，新增 Gemini 3.6-Flash 模型支持、首次运行 Splash 引导用户选择默认沙箱，并修复了多会话对话泄漏问题。
- **社区反馈集中爆发**：昨日有 15 个新 Issue 涌入，其中 5 个为 triage 状态。关键回归包括 React/Ink 无限渲染循环（#2802 回归）、Windows 退出崩溃、tmux 下命令完成检测失效。
- **高赞需求持续升温**：PDF 阅读支持（👍33）、自动模式模型池配置（👍6）、子 Agent AI 信用分解（👍6）等呼声最高。

## 🚀 版本发布

### v1.0.74-2
- **Fixes and changes**（具体内容未详细说明）

### v1.0.74-1
**新增**
- 首次运行 Splash 界面，引导用户选择默认沙箱。
- 支持 Gemini 3.6-Flash 模型。

**改进**
- 多会话复用场景下，某个会话的打开对话框不再泄漏到另一个会话；当用户切回时会重新打开符合条件的选择器。
- `$` 交互式 Shell 快捷操作优化（描述未完整，推测为补全类改进）。

> 注意：v1.0.74-2 紧随其后发布，推测修复了 v1.0.74-1 的紧急问题，建议用户升级至此版本。

## 🔥 社区热点 Issues（Top 10）

### 1. [#443 – 内置 PDF 阅读支持](https://github.com/github/copilot-cli/issues/443)
- **👍33 / 评论6** | 创建近 9 个月仍火热
- **摘要**：Copilot CLI 无法原生读取 PDF，用户需手动安装 pdftotext 等工具。社区希望 CLI 能内建 PDF 解析能力，便于处理学术论文、技术文档等。
- **重要性**：长期未被满足的核心功能需求，投票数最高，体现了用户对非结构化文档处理的强烈诉求。

### 2. [#4183 – 自动压缩无法防止 CAPI 5MB 上限失败](https://github.com/github/copilot-cli/issues/4183)
- **👍7 / 评论2** | 刚创建 4 天
- **摘要**：长时间的工具密集型会话即使未超出模型上下文 Token 限制，但序列化后的 CAPI 请求体可能超过 5MB 独立限制，自动压缩机制未能阻止该失败。
- **重要性**：直接影响长期会话的可用性，是架构级缺陷，开发者关注度高。

### 3. [#4016 – BYOK 在 --acp 模式下仍被拒绝](https://github.com/github/copilot-cli/issues/4016)
- **👍4 / 评论4** | 创建于 7 月 3 日，持续更新
- **摘要**：配置 `COPILOT_PROVIDER_*` 后，`copilot -p` 可免登录工作，但 `copilot --acp --stdio` 在 `session/new` 时仍要求 GitHub 登录（-32000）。该问题在 v1.0.61 曾修复，现回归。
- **重要性**：影响企业级 BYOK 用户，认证回归易导致信任问题。

### 4. [#4163 – 子进程僵尸累积](https://github.com/github/copilot-cli/issues/4163)
- **👍2 / 评论3** | 创建 5 天
- **摘要**：Linux 上 Copilot CLI 1.0.71 不回收已结束的子进程，僵尸进程以 ~2/min 的速度累积，21 分钟内可产生 8 个僵尸。
- **重要性**：资源泄漏问题，长时间运行可能导致系统 PID 耗尽。

### 5. [#4222 – 主面板冻结 / 无限渲染循环回归](https://github.com/github/copilot-cli/issues/4222)
- **👍0 / 评论0** | 昨日新增
- **摘要**：v1.0.72+ 上 #2802 报告的 React/Ink 无限渲染循环（“Maximum update depth exceeded”）再次出现，输入后 UI 显示“Working…”且无输出。仅影响 VS Code 集成终端 + 原生 Windows 环境。
- **重要性**：严重 UI 阻塞回归，影响日常交互。

### 6. [#4220 – Plan 模式误拦截只读 gh 命令](https://github.com/github/copilot-cli/issues/4220)
- **👍0 / 评论0** | 昨日新增
- **摘要**：Plan 模式下的命令门禁本应允许只读操作，却错误地将 `gh api GET` 和 `gh api graphql -f query=...` 标记为“可能修改工作区”并阻止执行。
- **重要性**：破坏开发工作流，尤其影响 GitHub 数据查询场景。

### 7. [#4206 – 环境页脚卡在“Loading:”](https://github.com/github/copilot-cli/issues/4206)
- **👍2 / 评论1** | 昨日新增
- **摘要**：环境状态页脚永远显示“◎ Loading: 1 instruction, 40 skills, 1 plugin, 2 agents”而不进入完成状态，但 `/env` 命令能正常列出所有已加载项。推测内置 GitHub MCP 握手在企业 MCP 策略下发生死锁。
- **重要性**：界面信息不准确，引发用户对加载状态的焦虑。

### 8. [#4224 – 子 Agent 的 OTel 跨度缺少计费属性](https://github.com/github/copilot-cli/issues/4224)
- **👍0 / 评论0** | 昨日新增
- **摘要**：当会话将工作委派给子 Agent 时，OTel 观察数据完全缺失 `github.copilot.nano_aiu` 和 `github.copilot.cost` 等计费属性，导致外部成本核算严重低估。
- **重要性**：影响企业信用审计，可造成计费不透明。

### 9. [#4218 – 允许用户配置自动模式使用的模型池](https://github.com/github/copilot-cli/issues/4218)
- **👍6 / 评论0** | 昨日新增
- **摘要**：自动模式虽可选用所有可用模型，但用户无法限制其范围，导致成本和行为难以预测。希望提供模型过滤配置（如仅用指定模型、优先低成本模型等）。
- **重要性**：高赞 Feature Request，直接关系到自动模式的成本控制。

### 10. [#4225 – 协调器卡在“Working”而子 Agent 在后台运行](https://github.com/github/copilot-cli/issues/4225)
- **👍0 / 评论0** | 昨日新增
- **摘要**：用户多次遇到主 UI 显示“Working”但无进展，实际上子 Agent 仍在后台运行，用户输入被排队但无反馈。日志分析由 Copilot 自行完成但仍存疑。
- **重要性**：多 Agent 编排的 UX 问题，导致用户误以为程序挂死。

## 🛠 重要 PR 进展

当前只有一个 Open PR（#3163），内容为“ViewSonic monitor”，描述提及与 #2591、#3561、#3559 相关，并触发 GitHub Action 运行。该 PR 标题和描述与 Copilot CLI 核心功能缺乏关联（可能为测试或误提交），**未发现其他实质性代码变更**。社区短期无可见的修复或功能 PR 合并。

## 📊 功能需求趋势

从过去 24 小时活跃的 Issues 中提炼出社区最关注的 **6 个功能方向**：

1. **内建文档格式支持（PDF 阅读）** – #443 持续领跑，用户希望 CLI 自身能解析 PDF，减少外部工具依赖。
2. **模型与 Agent 配置灵活性** – #4218（自动模式模型池配置）、#4208（inline agent 链式调用）、#4207（子 Agent 信用分解）显示用户对成本透明度和控制权要求提升。
3. **MCP 与企业集成** – #2282（MCP 连接失败）、#4206（MCP 握手卡死）反映企业级 MCP 服务器部署仍不稳定。
4. **终端兼容性与渲染** – #4222（渲染循环回归）、#4212（tmux 下颜色不可读）、#3428（OSC 133 序列支持）表明多终端环境适配是持续痛点。
5. **子 Agent 管道与任务编排** – #4225（协调器 UX）、#4224（OTel 计费）显示多 Agent 协作的可观测性和交互体验亟待改进。
6. **认证与安全** – #4016（BYOK 回归）、#4221（权限扫描误判）、#4220（plan 模式误拦截）体现安全策略精细化需求。

## 💡 开发者关注点

- **认证回归频发**：BYOK 和 `--acp` 模式的认证问题屡次修复又回归，开发者呼吁增加回归测试覆盖。
- **子进程资源管理**：僵尸进程累积（#4163）和 `tgrep` 索引器 OOM（#3976）显示内存和进程生命周期管理存在设计缺陷。
- **Windows 生态崩溃**：多个 Windows 特定问题（#4219 通知崩溃、#4217 退出崩溃、#4165 resume 挂起）表明跨平台测试不足。
- **无限渲染循环**：React/Ink 渲染循环在 v1.0.31 修复后再次出现（#4222），开发者质疑其根本原因未被彻底解决。
- **计划模式误判**：只读 `gh` 命令被误拦（#4220）以及 git `-L` 参数被错误扫描为路径（#4221）持续破坏实际工作流，用户希望提供更智能的命令分类或可配置白名单。

> 日报基于 `github.com/github/copilot-cli` 公共数据生成，所有链接均可直接跳转。关注 [Copilot CLI 仓库](https://github.com/github/copilot-cli) 获取最新动态。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 | 2026-07-23

## 今日速览
过去24小时内社区无新版本发布，但有三个新/更新的 Issue 值得关注：一是用户遭遇组织级 TPD 速率限制触发异常（持续至今未修复），二是 MCP 工具名称与 schema 因客户端未做清洗而被 Moonshot API 拒绝，三是 Windows 中文环境下 stdout 重定向导致 Unicode 编码崩溃。整体社区焦点集中在 API 兼容性、速率限制与跨平台编码问题上。

## 社区热点 Issues（共 3 条）

### 1. [bug] request reached organization TPD rate limit, current: 1505241
- **作者**: @globalvideos272-lab  
- **创建**: 2026-05-18 | **更新**: 2026-07-22 | **评论**: 1 | 👍: 2  
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2318  
- **重要性**: 该问题持续超过两个月仍未关闭，用户报告版本 2.6 下 TPD 计算错误，实际请求数远高于限制值，严重影响团队正常使用。社区已有 2 人点赞，表明同类问题普遍存在。  
- **社区反应**: 作者描述“Critical Bug: Incorrect TPD Calculation”，但官方尚未给出修复方案或临时绕过方法。

### 2. MCP tool names & schemas rejected by Moonshot API (HTTP 400) — sanitize client-side before sending
- **作者**: @sbdsam  
- **创建**: 2026-07-22 | **更新**: 2026-07-22 | **评论**: 1 | 👍: 0  
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2531  
- **重要性**: MCP（Model Context Protocol）是当前热门扩展机制，该问题直接导致自定义工具无法通过 API 调用，报错“tools.function.parameters is not a valid moonshot flavored json schema”。影响所有使用 MCP 工具的开发者。  
- **社区反应**: 用户明确指出需要“sanitize client-side”，表明问题根源在客户端未对参数 schema 做兼容性清洗。目前尚无官方回复。

### 3. kimi web crashes at startup on Windows when stdout is redirected: UnicodeEncodeError (gbk) in print_banner
- **作者**: @BFour666  
- **创建**: 2026-07-22 | **更新**: 2026-07-22 | **评论**: 0 | 👍: 0  
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2532  
- **重要性**: Windows 中文环境下使用管道或日志重定向时，启动横幅中的 `➜` (U+279C) 字符无法通过 GBK 编码，导致 `print_banner` 直接崩溃。该 Bug 阻塞了 CI/CD 或脚本化调用场景。  
- **社区反应**: 问题刚提出，尚无回复，但此类编码问题在跨平台 CLI 工具中非常典型，预计会引发较多关注。

## 功能需求趋势

从近期（含本期）提交的 Issue 中可提炼出社区最关注的功能方向：

- **API 速率限制优化**：用户对组织级 TPD 的计算逻辑和错误提示容忍度低，期望更精确的限速策略或客户端侧提前报错。
- **MCP 工具兼容性增强**：用户希望客户端自动对 tool schema 进行 JSON Schema 到 “moonshot flavored” 的格式转换，或至少给出清晰的校验错误信息。
- **跨平台编码适配**：尤其是 Windows 中文环境下的 Unicode 字符输出问题，需求集中在 `print_banner` 等启动阶段内容的编码 fallback 方案。

## 开发者关注点

- **TPD 速率限制的精确性与可预测性**：多位用户反馈实际请求触发限制的时间点与文档描述不符，急需官方澄清计算方式或提供客户端预警。
- **MCP 工具 schema 的客户端清洗**：目前开发者必须手动调整参数格式才能通过 API 验证，增加使用门槛；社区期待内置 sanitize 逻辑。
- **Windows stdout 重定向的编码回退**：对于需要在 Windows 服务器或 CI 环境中使用 `kimi web` 的用户，启动崩溃是致命缺陷，应尽快添加 `encoding='utf-8'` 或改用安全字符。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 | 2026-07-23

## 📌 今日速览

- **OpenCode Go 订阅大面积报错**：多个用户反馈所有 Go 订阅模型返回 `401 Request blocked by upstream provider`，free 模型正常，疑似服务端问题引发社区广泛关注（累计 80+ 评论）。
- **功能请求持续活跃**：#6231 关于从 OpenAI 兼容端点自动发现模型的提案获 185 次点赞，成为社区最受期待的功能之一。
- **多项自动化 PR 完成合入**：包括会话摘要修复、WebFetch 错误区分、TUI 主题生成等，代码质量与文档同步改进。

---

## 🚀 版本发布

过去24小时无正式版本发布，仅有一个 **PR verification 视频资源** 更新：

- **pr-38252-videos**  
  针对 PR #38252 的前后对比验证录屏，供评审人员参考。  
  [查看资源](https://github.com/anomalyco/opencode/tree/main?tab=readme-ov-file#pr-38252-videos)

---

## 🔥 社区热点 Issues（Top 10）

| # | Issue | 评论/👍 | 摘要 | 链接 |
|---|-------|---------|------|------|
| 1 | **#6231** Auto-discover models from OpenAI-compatible provider endpoints | 28 💬 185 👍 | 用户手动列举本地模型（LM Studio, Ollama 等）繁琐易错，建议自动发现。社区高度认同，讨论集中于 API 兼容性实现。 | [查看](https://github.com/anomalyco/opencode/issues/6231) |
| 2 | **#38257** OpenCode Go: 401 Request blocked by upstream provider — chat/completions 失败，/v1/models 正常 | 25 💬 8 👍 | 2026-07-22 起所有 Go 订阅模型返回 401，仅 `/v1/models` 可用。用户确认为服务端问题，影响大量付费用户。 | [查看](https://github.com/anomalyco/opencode/issues/38257) |
| 3 | **#38218** Bug: All subscription models return "Request blocked by upstream provider" | 21 💬 5 👍 | 与 #38257 类似，登录后所有模型调用均失败。社区在汇总根因，怀疑上游限流或鉴权变更。 | [查看](https://github.com/anomalyco/opencode/issues/38218) |
| 4 | **#19466** opencode 在等待 API 限速时用掉 50% CPU | 15 💬 11 👍 | `retrying in 18m 12s` 期间 i9-14900 单核占用 50%，用户认为应优化空闲等待时的资源消耗。 | [查看](https://github.com/anomalyco/opencode/issues/19466) |
| 5 | **#38293**（俄语）Go 订阅无法使用 | 15 💬 0 👍 | 用户报告同样 401 错误，俄语提交，增加了受影响用户的地域多样性。 | [查看](https://github.com/anomalyco/opencode/issues/38293) |
| 6 | **#38195** 401 AuthError: Request blocked by upstream provider | 15 💬 15 👍 | 跨平台复现（Windows/Mac, Desktop/Hermes），free 模型正常，Go 订阅失败。被确认为优先级最高的关键 bug。 | [查看](https://github.com/anomalyco/opencode/issues/38195) |
| 7 | **#38190** Request blocked by upstream provider（已关闭） | 13 💬 12 👍 | 用户提问如何修复，该 issue 已被关闭，但未给出解决方案，社区建议关注官方更新。 | [查看](https://github.com/anomalyco/opencode/issues/38190) |
| 8 | **#37970** Plan/Build 模式丢失 | 10 💬 1 👍 | 1.18.0 版本后 Plan/Build 模式切换选项消失，用户只能通过对话引导模型进入计划模式，体验下降。 | [查看](https://github.com/anomalyco/opencode/issues/37970) |
| 9 | **#26220** 工具调用后陷入无限循环（Zen/big-pickle） | 6 💬 3 👍 | 调用工具后进程不退出、不响应，需要重启，影响持续使用。 | [查看](https://github.com/anomalyco/opencode/issues/26220) |
| 10 | **#38356** 子代理任务向文件写入空字节导致损坏 | 2 💬 0 👍 | 子代理生成的文件被填充空字节，HTML 文件被破坏，属于严重的数据一致性问题。 | [查看](https://github.com/anomalyco/opencode/issues/38356) |

---

## 📦 重要 PR 进展（Top 10）

| # | PR | 状态 | 摘要 | 链接 |
|---|-----|------|------|------|
| 1 | **#38396** docs: 添加 TUI V2 主题参考文档 | 已合入 | 生成 V2 TUI 主题指南并接入文档导航，同时通过 CI 保证文档与 Effect Schema 同步。 | [查看](https://github.com/anomalyco/opencode/pull/38396) |
| 2 | **#38397** refactor(tui): 从 V2 主题生成语法高亮 | 开放中 | 将完整 TUI 的 `SyntaxStyle` 解析统一为 V2 Token，同时保留 mini-TUI 兼容性。 | [查看](https://github.com/anomalyco/opencode/pull/38397) |
| 3 | **#38398** feat(tui): 添加每轮 token 用量诊断 | 开放中 | 在 DevTools 中展示模型报告的 token 用量（新/缓存/总量），并支持隐藏通知。 | [查看](https://github.com/anomalyco/opencode/pull/38398) |
| 4 | **#33444** fix(session): 从每轮 diff 恢复会话摘要 | 已合入 | 修复了 #30127 导致会话摘要（文件数、行数）被清空的问题，恢复正确统计。 | [查看](https://github.com/anomalyco/opencode/pull/33444) |
| 5 | **#33393** fix(core): 区分 WebFetch URL 错误与网络错误 | 已合入 | 原先所有失败统一为“请求失败”，现区分格式错误、协议错误、超时等，便于调试。 | [查看](https://github.com/anomalyco/opencode/pull/33393) |
| 6 | **#33367** fix(cli): 为 stderr 输出补上缺失的换行符 | 已合入 | CLI 错误输出末尾缺少换行，导致日志混乱。AI 自动修复并添加测试。 | [查看](https://github.com/anomalyco/opencode/pull/33367) |
| 7 | **#33293** fix(acp): 暴露子代理会话并路由子权限 | 已合入 | 子代理生成的会话 ID 未注册到 ACP 会话存储，导致权限管理失效。现已修复。 | [查看](https://github.com/anomalyco/opencode/pull/33293) |
| 8 | **#33284** fix(ui): 恢复 Desktop/web 聊天中 Markdown 标题层级 | 已合入 | Markdown 的所有标题被统一为 14px，修复后 h1-h6 恢复正确字号和样式。 | [查看](https://github.com/anomalyco/opencode/pull/33284) |
| 9 | **#38395** docs: 在 websearch 文档中补充 Parallel 作为可选后端 | 开放中 | 原文档仅提及 Exa，实际支持 Exa 或 Parallel，本 PR 更新文档并添加对应配置项说明。 | [查看](https://github.com/anomalyco/opencode/pull/38395) |
| 10 | **#33450** feat(tui): 添加全局会话选择器切换 | 已合入 | 在 TUI 会话选择器中增加全局模式，允许用户发现并跳转到其他项目的会话。 | [查看](https://github.com/anomalyco/opencode/pull/33450) |

---

## 📊 功能需求趋势

从过去 24 小时的 Issues 和 PR 中，社区最关注的三大功能方向：

1. **模型与提供商管理**  
   - 自动发现 OpenAI 兼容本地模型（#6231）  
   - 支持更多 websearch 后端（Exa/Parallel，PR #38395）  
   - 解决 Go 订阅鉴权问题（#38257 等）

2. **用户体验与界面优化**  
   - 恢复 Plan/Build 模式切换（#37970）  
   - Tab 激活状态视觉区分（#38341，已关闭）  
   - 项目搜索功能（#38353）  
   - 右侧用户输入快速跳转侧栏（#32165）

3. **性能与资源控制**  
   - 等待限速时降低 CPU 占用（#19466）  
   - TUI 可配置 FPS 限制（#13817，已关闭）  
   - 减少每轮 token 累积（#38344，已关闭）  
   - 会话/子代理清理（#37314）

---

## 🔧 开发者关注点（痛点 / 高频反馈）

- **Go 订阅大面积故障**：超过 5 个独立 Issue 报告相同的 401 错误，影响范围广、用户情绪急切。free 模型正常，推测为上游 API 鉴权策略变更或服务端配置错误。社区期待官方尽快发布修复或公告。
- **数据损坏风险**：子代理写入空字节（#38356）是严重的可靠性问题，可能导致用户工作丢失，需优先调查。
- **CLI 行为不一致**：缺少换行符（PR #33367）、LaTeX 公式未渲染（#34407）等细节影响日常使用。
- **Web 终端剪贴板失效**：code-server、GitHub Codespaces 等环境下“复制到剪贴板”实际不生效（#26459），影响远程开发者。
- **配置变更无声失败**：项目编辑对话框中的颜色/名称修改在保存后丢失，且无错误提示（#32691），降低用户信任。

---

> **注**：以上动态基于 GitHub 数据整理，所有分数和时间均来自原始数据。Go 订阅问题若有进展，请关注 [OpenCode 官方公告](https://github.com/anomalyco/opencode/issues?q=label%3Ago+401)。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 | 2026-07-23

## 今日速览

昨日（2026-07-22）Qwen Code 发布了 **v0.20.0-preview.0** 预览版，重点强化了遥测模块的测试覆盖。社区活跃度维持高位，**side‑query 强制禁用 thinking** 导致的工具故障（#7284、#7440）已修复并关闭；核心测试套件因 fork 分发测试失败导致 `main` 分支 CI 全红（#7537），相关修复 PR 已提交。此外，**版本更新检查** 在 v0.20.1 后出现大面积失效（#7515、#7543），社区已提交多个修复方案。

## 版本发布

### v0.20.0-preview.0
- **更新内容**：测试(telemetry) – 补充守护进程指标初始化顺序覆盖率，并记录 `metricReader` 的不对称性。  
- **提交者**：@doudouOUC  
- **完整变更**：https://github.com/QwenLM/qwen-code/compare/v0.19.0...v0.20.0-preview.0  

### v0.20.0-nightly.20260722.b98306b7e
与预览版相同测试变更，为每日构建快照。

### v0.0.0-benchmark-poc.20260722.1
临时预发布版本，用于验证 GitHub Actions → ECS 基准测试工作流 → 结果发布链路，非产品发布。

## 社区热点 Issues

1. **#7284 – side‑query 强制 disable_thinking 导致 TokenPlan 端点 400 错误**  
   - **状态**：已关闭  
   - **影响**：`web_fetch`、分类器等所有依赖侧查询的功能失效，属 P1 级核心 Bug。社区确认后迅速合并修复，上游 PR #7534 对 `enable_thinking` 参数做了重试处理。  
   - 链接：https://github.com/QwenLM/qwen-code/issues/7284

2. **#7316 – OpenAI 兼容模型下 `subAgent` 因 toolCall 返回空字符串完全不可用**  
   - **状态**：已关闭  
   - **要点**：部分 OpenAI 代理对可选参数返回空字符串，导致子代理 tool call 出现语义互斥字段，社区反应强烈，已紧急修复。  
   - 链接：https://github.com/QwenLM/qwen-code/issues/7316

3. **#7537 – `main` 分支核心测试套件全红：fork 分发测试卡在 registry.complete**  
   - **状态**：打开（P1）  
   - **影响**：任何 PR 的 `Test (ubuntu-latest, Node 22.x)` 均失败，已拖慢合并流程。开发者 @he-yufeng 已在 PR #7540 中提交 stub 修复方案。  
   - 链接：https://github.com/QwenLM/qwen-code/issues/7537

4. **#7515 – 更新检查失败（registry 错误）**  
   - **状态**：打开  
   - **影响**：v0.20.1 后所有用户无法使用 `qwen update` 或 `/update` 检查新版本。社区定位为 `getNpmCliPath` 返回了非 JS 文件路径（#7543），已有两个修复 PR（#7545、#7544）待审核。  
   - 链接：https://github.com/QwenLM/qwen-code/issues/7515

5. **#7287 – 自动记忆系统未注册 MEMORY.md 到 FileReadCache，首次写入总是被拒绝**  
   - **状态**：打开（P2）  
   - **影响**：auto-memory 功能在会话开始后无法正确更新记忆文件，用户需手动重试。社区参与者 @pomelo-nwu 正在跟进根本原因。  
   - 链接：https://github.com/QwenLM/qwen-code/issues/7287

6. **#7489 – VS Code 伴侣扩展中文件选择器插入 @filename 但图片未实际附加**  
   - **状态**：打开  
   - **影响**：图片附件流程断裂，模型无法接收图像内容。@yiliang114 已提 PR #7493 修复。  
   - 链接：https://github.com/QwenLM/qwen-code/issues/7489

7. **#7404 – 启动时版本检查超时时间过短，加载长会话时必超时**  
   - **状态**：已关闭  
   - **影响**：用户启动时若加载历史较长的会话，版本检查几乎必定超时，影响启动体验。社区建议延长超时或改为异步非阻塞。  
   - 链接：https://github.com/QwenLM/qwen-code/issues/7404

8. **#7264 – 冷启动性能：ACP 子进程中遗留的惰性加载优化候选**  
   - **状态**：打开（P2）  
   - **影响**：ACP 子进程冷加载 17.24 MiB / 2420 个模块，增加启动延迟。开发团队正进入第二阶段优化。  
   - 链接：https://github.com/QwenLM/qwen-code/issues/7264

9. **#6577 – Windows PowerShell/终端中 Alt+V 无法粘贴剪贴板截图**  
   - **状态**：打开（P2，欢迎 PR）  
   - **影响**：Windows 用户无法粘贴截图，跨平台兼容性问题长期存在。社区希望统一键绑定机制。  
   - 链接：https://github.com/QwenLM/qwen-code/issues/6577

10. **#5958 – Web Shell 输入编辑器（CodeMirror）在移动浏览器中无法工作**  
    - **状态**：打开（P2，欢迎 PR）  
    - **影响**：通过 `qwen serve` 分享的 Web Shell 在 iOS Safari / Android Chrome 上完全无法输入，阻碍移动端使用。  
    - 链接：https://github.com/QwenLM/qwen-code/issues/5958

## 重要 PR 进展

1. **#7534 – fix(core): 当提供商要求 thinking 时重试请求**  
   - **功能**：解决 #7284 核心问题——当侧查询强制 `enable_thinking: false` 而提供商返回 400 时，自动重试并启用 thinking。  
   - 链接：https://github.com/QwenLM/qwen-code/pull/7534

2. **#7540 – test(core): 在代理测试注册表中 stub 常驻代理方法**  
   - **功能**：修复 `main` 分支 CI 红色（#7537），通过 mock `registry.complete` 使 fork 分发测试通过。  
   - 链接：https://github.com/QwenLM/qwen-code/pull/7540

3. **#7545 – fix(cli): 停止将版本管理器的 npm shim 解析为 npm-cli.js**  
   - **功能**：解决 #7515 更新检查失效，当 npm 被 mise/volta 等 shim 替换时，正确定位真正的 `npm-cli.js`。  
   - 链接：https://github.com/QwenLM/qwen-code/pull/7545

4. **#7544 – fix(cli): 将 npm wrapper 解析为 npm-cli.js**  
   - **功能**：与 #7545 目标相同但采用不同方法，社区同时提交了两个备选 PR，等待决策。  
   - 链接：https://github.com/QwenLM/qwen-code/pull/7544

5. **#7542 – feat(cli): 添加版本升级提醒**  
   - **功能**：在启动时展示“新版本新特性”提示，记录已显示版本，仅显示一次。提升用户对更新的感知。  
   - 链接：https://github.com/QwenLM/qwen-code/pull/7542

6. **#7527 – fix(core): 在 hook 和工具发现子进程中剥离 daemon 密钥**  
   - **功能**：安全修复——确保敏感环境变量（如 `QWEN_SERVER_TOKEN`）不会通过子进程泄露，接续已合入的 #7256。  
   - 链接：https://github.com/QwenLM/qwen-code/pull/7527

7. **#7493 – fix(vscode): 使用文件选择器图片路径作为视觉输入**  
   - **功能**：修复 #7489——图片附件现在传递绝对路径，确保模型收到图像内容。  
   - 链接：https://github.com/QwenLM/qwen-code/pull/7493

8. **#7531 – fix(core): 关闭 `git clean` 和 `git checkout` 的破坏性 git 守卫漏洞**  
   - **功能**：加固 `DESTRUCTIVE_GIT_PATTERNS`，覆盖此前未匹配的命令变体，防止自动化误操作导致代码丢失。  
   - 链接：https://github.com/QwenLM/qwen-code/pull/7531

9. **#7517 – feat(core): 引入 Goal v3 状态协议**  
   - **功能**：定义版本化的目标状态契约，包含生命周期、乐观并发控制、迁移等基础结构，为 #7494 多智能体规划奠定基础。  
   - 链接：https://github.com/QwenLM/qwen-code/pull/7517

10. **#7471 – feat(web-shell): 为新会话添加 git 模式选择器**  
    - **功能**：在 Web Shell 创作栏中添加弹窗选择器，用户可在创建会话时选择“当前分支”、“新分支”或“工作树”模式。提升多上下文管理体验。  
    - 链接：https://github.com/QwenLM/qwen-code/pull/7471

## 功能需求趋势

- **子代理/多智能体系统**：社区持续关注 subAgent 与 OpenAI 兼容性（#7316）、规划 DAG 可视化（#7525）、Goal v3 状态协议（#7517）等，表明多智能体协作是未来重点。
- **VS Code 扩展增强**：图片附件（#7489）、文件选择器、工作区选择器等需求旺盛，IDE 集成深度仍在提升。
- **Web Shell 功能完善**：git 模式选择（#7471）、开始位置选择（#6701）、工作区切换（#6700）等 PR 密集提交，Web Shell 正在成为主要交互入口。
- **安全与隐私**：环境变量泄露（#6601，已关闭）、子进程密钥剥离（#7527）等修复显示社区对凭证安全高度敏感。
- **性能冷启动优化**：持续有 lazy-loading 审计（#7264）、模块加载优化等讨论，ACP 子进程冷加载是当前性能瓶颈。

## 开发者关注点

- **版本更新检查失效**：v0.20.1 后大量用户反馈 `qwen update` 失败，根源在于 `getNpmCliPath` 未能正确处理版本管理器的 shell shim（#7515、#7543）。开发者贡献了两个修复方案，但尚未合并，需要团队尽快决策。
- **side‑query 与 thinking 参数的冲突**：本次日报中最高频的 bug 类型（#7284、#7440、#7298），已修复但暴露出参数传递机制的设计鲁棒性不足。
- **CI 稳定性**：`main` 分支测试套件全红（#7537）严重影响合并效率，开发者临时提了 stub 修复，但长期需要更健壮的测试隔离。
- **跨平台输入兼容**：Windows 截图粘贴（#6577）、移动端 Web Shell 输入（#5958）长期未解决，属于 “欢迎 PR” 标签但缺乏贡献者资源。
- **记忆系统缺陷**：auto-memory 首次写入被拒绝（#7287）影响记忆功能的可靠性，需要核心开发者优先处理。

---

*以上内容由 AI 自动生成，基于 GitHub 公共数据，仅供参考。*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*