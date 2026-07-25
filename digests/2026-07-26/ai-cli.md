# AI CLI 工具社区动态日报 2026-07-26

> 生成时间: 2026-07-25 23:16 UTC | 覆盖工具: 7 个

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

好的，各位技术决策者与开发者朋友们，大家好。

基于今日（2026年7月26日）各主流 AI CLI 工具的社区动态日报，我为您整理了一份横向对比分析报告。本报告旨在捕捉当前 AI 开发工具生态的核心脉动，帮助您把握发展趋势、洞悉工具定位，为技术选型和开发实践提供参考。

---

# AI CLI 工具生态横向分析报告 (2026-07-26)

### 1. 生态全景

当前，AI CLI 工具市场呈现出 **“多元竞合，百家争鸣”** 的繁荣景象，竞争已从单纯的“可用性”转向“可靠性”、“自治性”与“无缝体验”的综合较量。各大工具均在不同维度上遭遇成长的烦恼：**稳定性是共同痛点**，无论是低级的资源泄漏、OOM，还是高级的 Agent 决策失误，都在消耗开发者的信任。与此同时，**自动化与 Agent 化是明确的演进方向**，各工具正通过子代理、工作流、记忆系统等功能，力争从“提问-回答”的辅助者，升级为能够独立规划并执行复杂任务的“AI 工程师”。社区反馈显示，**跨平台、跨设备的一致性**正成为决定重度用户去留的关键因素。

### 2. 各工具活跃度对比

| 工具 | 热点 Issues | 活跃 PRs | 版本发布 | 社区焦点 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 10 (高热度) | 3 | 1 (小版本) | 模型权限、跨端统一、桌面端功能完善 |
| **OpenAI Codex** | 10 (高热度) | 10 | 4 (Alpha) | 速率限制、Windows 稳定性、Credits 消耗 |
| **Gemini CLI** | 10 (中高热度) | 10 | 0 | Agent 可靠性、内部自动化基建、安全加固 |
| **GitHub Copilot CLI** | 10 (高热度) | 0 | 0 | 会话稳定性、核心命令失效、插件市场问题 |
| **Kimi Code CLI** | 2 (低热度) | 4 | 0 | 远程会话、会话恢复 Sticky Bug |
| **OpenCode** | 10 (中高热度) | 10 | 0 | UI 布局争议、CPU 性能退化、稳定性回归 |
| **Qwen Code** | 10 (高热度) | 10 | 1 (Nightly) | 终端渲染回归、MCP 兼容性、扩展系统问题 |

**分析**:
- **Claude Code、OpenAI Codex、Qwen Code** 社区热度最高，且问题集中、反馈专业，呈现出成熟工具的社区生态。
- **GitHub Copilot CLI** 虽无 PR 活动，但爆出多个高优先级 Bug，表明可能正处于修复瓶颈期。
- **OpenCode** 和 **Qwen Code** 在加速迭代，PR 活跃度高，但伴随而来的是较多的稳定性回归问题。
- **Kimi Code CLI** 社区规模相对较小，但也在积极修复核心问题，处于稳步追赶阶段。

### 3. 共同关注的功能方向

尽管各工具定位不同，但社区反馈指向了以下六大共同诉求：

1.  **会话稳定性与可靠性**：
    - **所有工具** 均存在相关问题。例如：Claude Code 的自动压缩丢失上下文；OpenAI Codex 的上下文压缩丢失操作；Gemini CLI 的子代理超时误报；GitHub Copilot CLI 的 OOM 恢复失败；OpenCode 的切换项目冻结；Qwen Code 的 Plan 模式退出通知缺失。

2.  **模型访问透明性与权限管理**：
    - **Claude Code**（Fable 5 降级）、**OpenAI Codex**（Credits 消耗异常）和 **OpenCode**（自托管 vs 代理模型透明度）的社区对此高度敏感。用户要求清晰、可预测的模型准入和计费逻辑。

3.  **MCP 集成与扩展生态**：
    - **Claude Code**（MCP 权限同步）、**OpenAI Codex**（插件 MCP 过滤）、**Gemini CLI**（MCP OAuth 刷新）、**Kimi Code CLI**（扩展系统）和 **Qwen Code**（Unity MCP 连接失败）均在巩固其插件体系。MCP 已成为行业标准，但互操作性、安全性和稳定性是当前挑战。

4.  **终端与桌面 UI 体验**：
    - **Claude Code**（桌面端 Bug）、**OpenAI Codex**（UI 交互问题）、**Gemini CLI**（Shell 假死）、**GitHub Copilot CLI**（鼠标滚动失效）、**OpenCode**（UI 布局争议）和 **Qwen Code**（终端滚动偏移、输入法错位）都在提醒我们：**基础的交互体验优化远未完成**。

5.  **跨平台与跨设备无缝体验**：
    - **Claude Code**（三端统一）、**OpenAI Codex**（Windows 远程控制失效）、**Gemini CLI**（Windows CRLF 问题）和 **Kimi Code CLI**（远程会话）使这一问题成为阻碍重度用户工作流流畅性的首要障碍。

6.  **安全性**：
    - **Claude Code**（`settings.local.json` 注入）、**OpenAI Codex**（未配置跳过 MCP 过滤）、**Gemini CLI**（`restore` 路径穿越）和 **Qwen Code**（凭证文件权限）表明，随着 Agent 权限增大，安全已是不可忽视的刚需。

### 4. 差异化定位分析

| 工具 | 核心定位 | 功能侧重 | 目标用户 | 技术路线 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | **全能型 AI 工程师** | Agent 自主性、多模态、深度上下文管理 | 追求极致效率、复杂任务自动化的高级开发者 | 强大底层模型驱动，强调理解的深度和行动的自主性 |
| **OpenAI Codex** | **平台化 Agent 生态** | 插件市场、远程控制、自动化工作流 | 企业级用户、跨设备协作团队 | 构建开放平台，通过插件和 MCP 实现高度可定制化 |
| **Gemini CLI** | **系统集成式开发伴侣** | 深度代码理解 (AST)、A2A 协议、OAuth 集成 | 复杂项目、内部工具链成熟的开发者 | 强调与 Google 生态及开源工具链（如 Git）的原生集成 |
| **GitHub Copilot CLI** | **IDE 体验的无缝延伸** | VS Code 深度集成、会话管理、代码上下文 | 以 VS Code 为中心的 GitHub 生态用户 | 强调与 IDE 体验的一致性，提供低摩擦的 CLI 交互 |
| **Kimi Code CLI** | **轻量级国产 Agent 工具** | 基本 Agent 能力、简洁 UI | 国内市场、寻求易用且免费/低价方案的开发者 | 追求快速迭代，紧贴国内开发者需求，功能走精简化路线 |
| **OpenCode** | **开源的社区驱动工具** | 高度可配置性、社区优先、TUI/Desk两栖 | 偏好开源、重视隐私、喜欢 DIY 的独立开发者 | 由社区需求驱动，迭代迅速，功能灵活但稳定性是挑战 |
| **Qwen Code** | **阿里系云原生开发伴侣** | 阿里云集成、企业级功能、快速迭代 | 阿里云生态用户、中国市场、多语言开发者 | 紧跟行业热点（MCP，子代理），追求功能丰富度和迭代速度 |

### 5. 社区热度与成熟度

- **最活跃 & 最成熟**：**Claude Code** 和 **OpenAI Codex** 社区规模最大，讨论质量最高，能够提出像“暴露 session_id 给 AI”这样的高级技术诉求，显示出用户群体对工具的理解非常深入。
- **高热度 & 快速迭代**：**OpenCode** 和 **Qwen Code** 处于快速成长期，PR 和 Issue 数量很大，但“增长痛”明显，稳定性回归问题多发。其社区更像一个“共建者”而非“使用者”，参与度高但有风险。
- **专注 & 专业**：**Gemini CLI** 社区虽然数量可能不占优，但讨论问题极其深入（AST、A2A），显示出其吸引的是高技术水平、对系统架构有要求的开发者。
- **生态捆绑**：**GitHub Copilot CLI** 和 **Kimi Code CLI** 的社区动态与母公司（GitHub/阿里）生态高度绑定。前者问题集中在 IDE 集成体验，后者则反映了国内市场的特定需求。

### 6. 值得关注的趋势信号

- **从“工具”到“工程师”的范式转移**：Claude Code 的“三端统一”、Gemini CLI 的“内部自动化基建”、OpenAI Codex 的“远程控制”等都表明，行业不再满足于一个代码补全或问答工具，而是追求一个能 **融入开发者完整工作流、主动规划并执行任务** 的 AI 工程师。
- **Agent 自主性的“阿喀琉斯之踵”**：Gemini CLI 被指出“不主动使用自定义技能”，这是一个具有里程碑意义的反馈。它揭示了当前模型的 **工具使用“惰性”** ：模型更倾向于依赖其内部知识，即使有现成、更优的工具。打破这一壁垒，将是 Agent 能力跃升的关键。
- **“成本失控”的隐忧**：OpenAI Codex 用户报告一个“计划”消耗约 100 Credits，Gemini CLI 的无限重试，以及 GitHub Copilot CLI 的密码屏蔽引发额外 Token 消耗。随着 Agent 自主性增强，**缺乏预见性的资源消耗** 正变成开发者对 AI 工具的新恐惧。
- **AI 原生安全挑战**：OpenCode 的安全研究员发现 Agents.md 文件可被静默修改，Gemini CLI 则防御性地修复了路径穿越。这标志着 AI CLI 工具已成为攻击面，**Agent 权限和提示的完整性与安全性** 将成为严肃团队选型的重要考量。
- **跨平台一致性是“及格线”而非“加分项”**：macOS/Linux 用户享受完整功能，而 Windows 用户却面临大量 Bug（换行符、远程控制、崩溃），这种割裂体验已导致社区强烈不满。对于任何志在主流市场的工具，**保证核心体验在不同平台（尤其是 Windows）上的无差别稳定**，已是不可妥协的底线。

**结论**：
当前 AI CLI 工具生态正处于从“百花齐放”向“精耕细作”转型的十字路口。**谁能在保证 Agent 强大能力的同时，率先解决稳定性、成本透明度和无缝体验这三大核心问题，谁就将赢得下一阶段竞争的先机。** 对于技术决策者而言，工具选型不应只看演示 Demo 的惊艳，更需关注其社区对 **Session 恢复、模型权限、长任务可靠性** 等“成事”能力的讨论深度。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，作为专注于 Claude Code 生态的技术分析师，以下是根据您提供的 GitHub 数据生成的社区热点报告。

---

### **Claude Code Skills 社区热点报告 (数据截至 2026-07-26)**

#### **1. 热门 Skills 排行 (Top 5 by PR评论热度)**

1.  **`skill-creator` 核心工具链修复 (PR #1298)**
    *   **功能**: 修复了 `run_eval.py` 脚本在多个系统（特别是 Windows）下报告 0% 召回率（Recall）的关键 Bug。
    *   **社区讨论热点**: 这是目前社区关注的绝对焦点。大量的 Issue (#556, #1061, #1169) 都在反馈 `run_eval.py` 无法正常工作，导致技能描述优化循环（`run_loop.py`）失效，开发者无法有效评估和迭代自己的 Skill。
    *   **当前状态**: Open (开放中)
    *   **链接**: https://github.com/anthropics/skills/pull/1298

2.  **`document-typography` 文档排版技能 (PR #514)**
    *   **功能**: 解决 AI 生成文档中的常见排版问题，如孤行（Orphan）、寡段（Widow）和编号错位。
    *   **社区讨论热点**: 社区对 AI 生成内容的“最终呈现质量”有较高要求。这个 Skill 直接切中了许多用户对专业文档格式的痛点，被认为是提升 AI 输出实用性的重要补充。
    *   **当前状态**: Open (开放中)
    *   **链接**: https://github.com/anthropics/skills/pull/514

3.  **`odt` OpenDocument 格式支持 (PR #486)**
    *   **功能**: 支持创建、填写、读取和转换 ODT/ODS 等开源文档格式。
    *   **社区讨论热点**: 反映了社区对“政府/企业级”办公套件（如 LibreOffice）兼容性的强烈需求。这是一个重要的平台扩展，表明用户不满足于仅支持 Microsoft Office 格式。
    *   **当前状态**: Open (开放中)
    *   **链接**: https://github.com/anthropics/skills/pull/486

4.  **`self-audit` 推理质量审计技能 (PR #1367)**
    *   **功能**: 在交付前对 AI 输出进行机械文件验证和四维度推理质量审查。
    *   **社区讨论热点**: 这是一个“元技能”，反映了社区对 AI 输出可靠性和安全性的更高追求。社区讨论焦点在于如何标准化“推理质量”的评估标准，并将其作为通用交付流程的一部分。
    *   **当前状态**: Open (开放中)
    *   **链接**: https://github.com/anthropics/skills/pull/1367

5.  **`testing-patterns` 测试模式技能 (PR #723)**
    *   **功能**: 添加了覆盖全栈测试（单元测试、React 组件测试、端到端测试）的综合性技能，并引入了“测试奖杯”等哲学理念。
    *   **社区讨论热点**: 开发者对提升 Claude 生成代码的可测试性和健壮性有极高热情。该技能不仅是指导，更像一套最佳实践指南，社区讨论核心是如何将其与 CI/CD 流程结合。
    *   **当前状态**: Open (开放中)
    *   **链接**: https://github.com/anthropics/skills/pull/723

6.  **`color-expert` 颜色专家技能 (PR #1302)**
    *   **功能**: 一个自包含的颜色专业知识技能，涵盖多种颜色命名系统（ISCC-NBS, XKCD, RAL等）和色彩空间选择指南。
    *   **社区讨论热点**: 这是一个高度专业化、领域细分的 Skill 范例。它展示了 Skill 不仅可以指导编程，还可以封装特定领域的“专家知识”，让 Claude 在特定任务（如设计、数据可视化）中表现得像真正的专家。
    *   **当前状态**: Open (开放中)
    *   **链接**: https://github.com/anthropics/skills/pull/1302

7.  **`pyxel` 复古游戏开发技能 (PR #525)**
    *   **功能**: 为 Pyxel 复古游戏引擎添加 Skill，支持“编写 → 运行 → 观察 → 迭代”的闭环工作流。
    *   **社区讨论热点**: 展现了 Skills 在创意和娱乐领域的应用潜力。社区关注点在于如何将 MCP 服务器与 Skills 结合，为特定工具（如 Pyxel）提供结构化、可重复的开发流程。
    *   **当前状态**: Open (开放中)
    *   **链接**: https://github.com/anthropics/skills/pull/525

#### **2. 社区需求趋势 (从 Issues 提炼)**

1.  **安全与信任 (Security & Trust)**: 社区对将社区贡献的 Skill 与官方 Skill 放置在同一命名空间下的做法感到担忧（Issue #492），认为这可能导致信任边界滥用。这表明社区强烈需要一个清晰的**技能审核与认证机制**。

2.  **企业协作与分发 (Enterprise Sharing)**: 开发者渴望更便捷地**在组织内部共享技能**（Issue #228）。当前的手动下载和上传流程效率低下，说明社区需要官方提供类似“组织技能库”或“一键分享链接”的功能。

3.  **工具链稳定性 (Tooling Stability)**: `skill-creator` 及其相关脚本（如 `run_eval.py`）在 Windows 系统和特定编码环境下频繁报错（Issues #556, #1061, #1169），严重影响了开发者创作和优化技能。核心诉求是**加固官方工具链，确保跨平台的可靠性**。

4.  **高级能力需求 (Advanced Capabilities)**: 社区开始探索更复杂、更前沿的技能方向。例如，用于 AI Agent 系统的**代理治理与安全模式**（Issue #412），以及用于长对话上下文的**紧凑记忆表示法**（Issue #1329）。这表明社区正思考如何通过 Skills 构建更复杂、更安全的 Agent 系统。

#### **3. 高潜力待合并 Skills**

以下 PR 评论活跃且功能完整，一旦修复技术问题或完成细节沟通，有望很快合并：

*   **`self-audit` (PR #1367)**: 作为“推理质量审计”的元技能，其价值已被社区认可，是提升 AI 输出可靠性的关键尝试。
*   **`testing-patterns` (PR #723)**: 满足开发者对代码质量的核心诉求，内容详实，实用性强。
*   **`color-expert` (PR #1302)**: 代表了将领域专家知识封装为 Skill 的优秀模式，具有示范意义。
*   **`pyxel` (PR #525)**: 与特定 MCP 服务器深度整合的范例，展示了 Claude 生态的外部拓展能力。

#### **4. Skills 生态洞察**

**一句话总结**: 当前社区最集中的诉求是 **“提升技能生态的可靠性、安全性和可共享性，同时通过固化工具基础设施（win平台兼容、编码问题）和引入高级治理/审计模式，为构建更可信、更强大的 AI Agent 系统铺平道路。”** 社区的热点已从“如何创建更多技能”转向了“如何让技能生态更健壮、更安全、更易于企业级协作”。

---

好的，各位开发者朋友们，早上好。这里是 **2026年7月26日** 的 Claude Code 社区动态日报，由 AI 开发工具技术分析师为您呈送。

---

### 1. 今日速览

过去24小时内，Claude Code 发布了v2.1.220小版本，主要进行稳定性修复。社区最激烈的讨论集中在 **Fable 5 模型**在 Max 计划上的访问权限问题上，尽管该模型已成为 Max 标配，但仍有部分用户遭遇“需要额度”的错误，并被迫降级。此外，实现 **Desktop、Mobile 与 CLI 三端统一**的呼声依旧很高，而**桌面端定时任务无法更改默认模型**的bug也持续引发关注。

### 2. 版本发布

#### v2.1.220 (最新)
- **更新内容**：仅包含错误修复和可靠性改进，无新增功能特性。
- **链接**：[查看完整 Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.220)

### 3. 社区热点 Issues (Top 10)

1.  **[[BUG] Max 计划用户无法使用 Fable 5](https://github.com/anthropics/claude-code/issues/79337)**
    - **热度**：🔥🔥🔥 (44 评论，14 👍)
    - **摘要**：自7月20日Fable 5成为Max计划标配后，多位用户反馈在Max计划下无法使用该模型，并被静默降级至Opus 4.8，系统提示需要“使用额度”。这引发了用户对计划权益和模型权限系统一致性的严重质疑。社区反应激烈，是目前最受关注的 Bug。

2.  **[[Feature] 跨端统一会话、设置与项目](https://github.com/anthropics/claude-code/issues/42050)**
    - **热度**：⭐ (5 评论，24 👍)
    - **摘要**：用户强烈建议实现 Desktop、Mobile 和 CLI 三端体验的统一，包括跨端访问和恢复同一会话、项目。这是目前点赞数最高的功能请求，反映了用户对无缝工作流的核心诉求。

3.  **[[BUG] 桌面端定时任务忽略模型设置，始终使用 Sonnet](https://github.com/anthropics/claude-code/issues/36496)**
    - **热度**：🔧 (5 评论，19 👍)
    - **摘要**：一个存在已久的 Bug。用户在 Desktop 端创建或编辑定时任务时，无论选择何种模型，任务运行后都会默认使用 Sonnet。该问题已经获得广泛共鸣，但至今尚未解决，影响了自动化工作流的灵活性。

4.  **[[BUG] Fable 5 模型 “无效或无法访问” 错误](https://github.com/anthropics/claude-code/issues/68137)**
    - **热度**：🕵️ (9 评论)
    - **摘要**：在v2.1.170版本中，用户在会话中突然遭遇 `Invalid or inaccessible model claude-fable-5` 错误，导致会话中断。该问题与#79337类似，但发生时间更早，表明Fable 5的权限问题由来已久。

5.  **[[Feature] 将 `session_id` 和 `context_window` 使用量暴露给 AI 模型](https://github.com/anthropics/claude-code/issues/36678)**
    - **热度**：💡 (8 评论, 2 👍)
    - **摘要**：开发者提出，当前AI模型无法感知自己的会话ID和上下文窗口使用情况，导致无法主动管理上下文或进行会话相关的操作。这个反馈切中了提升AI自主性的需求，技术含量较高。

6.  **[[BUG] Claude Code 持续无视项目级 CLAUDE.md 指南](https://github.com/anthropics/claude-code/issues/62087)**
    - **热度**：⚠️ (8 评论, 1 👍)
    - **摘要**：用户反映，在长时间的开发会话中，AI会系统性地忽略 `CLAUDE.md` 中定义的项目规范，需要用户反复纠正。这严重影响了其在严格遵守项目约定场景下的可靠性。

7.  **[[BUG] Cowork 模式下远程设备文件桥频繁断开](https://github.com/anthropics/claude-code/issues/77385)**
    - **热度**：⚙️ (3 评论, 1 👍)
    - **摘要**：在 Desktop 应用的 Cowork 模式下，与远程设备的文件桥接(远程文件、命令等)会间歇性断开，且无法自动恢复。这是远程协作功能的一个关键缺陷。

8.  **[[Feature] 允许个人账户设置默认模型用于新聊天和定时任务](https://github.com/anthropics/claude-code/issues/68924)**
    - **热度**：🎯 (3 评论, 1 👍)
    - **摘要**：非组织用户的个人账户目前无法设置默认模型，导致每次新建聊天或定时任务都需要手动切换，体验不佳。该请求是对#36496的补充，体现出用户在模型选择上的个性化需求。

9.  **[[Bug] 自动化工作流在 HTTP 429 限流下无限制重试，消耗大量 Token](https://github.com/anthropics/claude-code/issues/64328)**
    - **热度**：💰 (4 评论, 1 👍)
    - **摘要**：用户报告称，在运行包含97个Agent的工作流时，遭遇API限流（HTTP 429），但工作流系统并未停止或按指数退避，而是疯狂重试，在34秒内烧掉了200万Token。这是一个严重的成本控制与稳定性问题。

10. **[[Security] `settings.local.json` 缺少完整性保护，可被静默注入](https://github.com/anthropics/claude-code/issues/62506)**
    - **热度**：🔒 (2 评论)
    - **摘要**：安全研究员指出，用于控制免审批工具调用的 `settings.local.json` 文件没有完整性保护，同一系统上的恶意进程可注入权限，实现任意命令的静默预授权。这是一个值得关注的安全漏洞。

### 4. 重要 PR 进展

1.  **[[PR] 移除前端设计 Skill 中的“复古未来主义”建议](https://github.com/anthropics/claude-code/pull/39043)**
    - **状态**：OPEN
    - **摘要**：由知名开发者 @t3dotgg 提交，以其标志性的简洁风格“Trust me on this one.”阐述，旨在改善前端设计相关的默认行为。

2.  **[[PR] 修复 hookify 插件的 Python 导入路径](https://github.com/anthropics/claude-code/pull/15727)**
    - **状态**：CLOSED
    - **摘要**：修复了 hookify 插件因 `CLAUDE_PLUGIN_ROOT` 环境变量指向路径与 import 语句不匹配而导致的 `No module named 'hookify'` 错误。

3.  **[[PR] 重构：提取共享的 GitHub API 客户端](https://github.com/anthropics/claude-code/pull/49596)**
    - **状态**：CLOSED (已合并)
    - **摘要**：对代码库进行重构，将共享的 GitHub API 客户端逻辑提取到单独的文件 `github-api.ts` 中，并为其编写了测试。这是提升代码可维护性和可测试性的良好实践。

### 5. 功能需求趋势

- **模型访问与权限**：社区对“模型已订阅但无法使用”的问题非常敏感，尤其是在模型归属计划后，权限校验系统需要更加可靠和透明。
- **跨平台/跨端体验统一**：用户不再满足于单一工具，强烈期望在 Desktop、Mobile、CLI 三个平台上拥有同步的会话、项目和设置。
- **桌面端功能完善**：桌面端不仅仅是 CLI 的图形化外壳，用户对定时任务、模型选择、快捷键自定义等深度功能有明确需求，且对当前的稳定性问题（如任务模型无法自定义）感到不满。
- **MCP 集成与权限管理**：随着 MCP 的普及，用户开始关注 MCP 连接器在 CLI 和 Desktop 之间的权限设置不同步问题，以及 MCP 工具调用的安全性与可控性。
- **上下文与成本控制**：开发者开始关注 AI 如何更好地管理自身上下文（如暴露窗口使用率），并期望系统能更智能地处理限流和成本失控的情况。

### 6. 开发者关注点

- **Fable 5 访问受限**：Fable 5 模型是过去24小时当之无愧的“话题中心”。Max 用户被降级、普通用户直接报错，这表明模型准入和计划匹配系统可能存在漏洞或逻辑不严谨。**这是当前最优先需要工程师关注和解决的高频痛点。**
- **自动化行为不可控**：无论是定时任务模型被锁定，还是工作流遇到限流时的“疯狂重试”行为，都指向了系统在自动化场景下的**行为确定性不足**。开发者需要的是可预测、可配置的自动化引擎，而不是“黑盒”。
- **AI 可靠性待提升**：AI 无视 CLAUDE.md 指南、对自己的行为产生幻觉...... 这些问题直击AI辅助开发的核心——**可信赖度**。如果不能稳定地遵循项目上下文，再强大的模型也是不可靠的。
- **跨端体验碎片化**：不同平台下功能不一致（如 Desktop 和 CLI 的 MCP 权限不同）、设置不互通，使得用户的工作流被迫“割裂”。**统一、无缝的体验**是所有重度用户的最基础也最迫切的期待。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

好的，作为专注于 AI 开发工具的技术分析师，我已根据您提供的 GitHub 数据，为您生成了 2026-07-26 的 OpenAI Codex 社区动态日报。

---

## **OpenAI Codex 社区动态日报 | 2026-07-26**

### **今日速览**

过去24小时，Codex 社区的核心关注点集中在 **速率限制的可预测性改进** 与 **Windows 平台的多项持续性 Bug** 上。开发团队则完成了包括 **macOS 二进制签名修复**、**JSON-RPC 帧大小限制** 在内的多项关键基础设施加固，同时推进了 **远程技能注入**与 **网络策略处理** 等新特性的落地。值得注意的是，关于“Credits消耗异常”和“应用频繁崩溃”的新 Issue 在今日集中涌现，显示出兼容性与稳定性仍是当前迭代的重点。

### **版本发布**

过去24小时内，官方发布了 **Rust SDK** 的四个 Alpha 版本，均为 `0.146.0-alpha` 系列的微小迭代。由于缺乏详细的变更日志，推测为针对内部测试或特定场景的修复版本。具体版本号如下：
- **rust-v0.146.0-alpha.10.1**
- **rust-v0.146.0-alpha.10**
- **rust-v0.146.0-alpha.9**
- **rust-v0.146.0-alpha.8**

### **社区热点 Issues**

以下是过去24小时内更新的、最值得关注的10个 Issue：

1.  **[🔥] #9508: 使每周额度重置具有确定性**
    - **链接**: https://github.com/openai/codex/issues/9508
    - **重要性**: 这是社区对现有速率限制机制感到沮丧的集中体现。用户期望额度重置时间、剩余额度显示能更透明、可预测。
    - **社区反应**: 热门话题，47条评论，32个赞。

2.  **[🔥] #4003: Windows 系统上补丁文件出现混合换行符**
    - **链接**: https://github.com/openai/codex/issues/4003
    - **重要性**: 影响所有Windows用户。Codex在修改文件时未遵循文件原有的换行符格式（CRLF vs LF），可能会导致代码评审混乱或与项目已有风格不一致。
    - **社区反应**: 获得**72个赞**，表明这是Windows用户最痛点的问题之一。

3.  **[🔥] #1457 (已关闭): Python UV 在 Codex 沙箱中运行失败**
    - **链接**: https://github.com/openai/codex/issues/1457
    - **重要性**: 尽管已关闭，但高达61条的评论数表明该问题曾严重阻碍了使用 `uv` 工具的用户。其解决方案对于维护环境工具的兼容性至关重要。
    - **社区反应**: 焦点问题，已得到官方处理。

4.  **[🔝] #31836: 项目排序功能仅对项目内的任务排序，而非项目本身**
    - **链接**: https://github.com/openai/codex/issues/31836
    - **重要性**: 这是一个明显的UI/UX Bug。用户期望通过“最后更新”来整体排序项目，但该功能失效，影响组织和管理多个项目的效率。
    - **社区反应**: 32条评论，35个赞，说明有较多人遇到了这个误导性的UI交互。

5.  **[🔝] #29356: 上下文压缩丢失操作连续性；建议保留最后5个操作步骤**
    - **链接**: https://github.com/openai/codex/issues/29356
    - **重要性**: 深度用户反馈。自动上下文压缩在长任务中会丢失关键的上下文信息，导致模型“失忆”。该Issue提出了具体的改进建议（保留最后5步）。
    - **社区反应**: 20条评论，0赞，但来自Pro用户，反馈内容专业，代表了高级用户对长会话体验的诉求。

6.  **[🔝] #26379: Codex CLI 持久化格式错误的 tool_search_call 参数**
    - **链接**: https://github.com/openai/codex/issues/26379
    - **重要性**: 这是一个严重的CLI Bug。当会话被持久化并恢复时，格式错误的工具调用参数会导致API返回400错误，直接中断工作流。
    - **社区反应**: 9条评论，2个赞，但问题影响核心功能。

7.  **[🔝] #31786 & #31973: Windows 远程控制功能完全失效或卡在“重连中”**
    - **链接**: https://github.com/openai/codex/issues/31786 , https://github.com/openai/codex/issues/31973
    - **重要性**: 这两个Issue同时出现，指向Windows端远程控制功能存在严重的连通性和恢复性问题，影响使用手机控制PC的体验。
    - **社区反应**: 分别有11条和11条评论，且创建时间很近，说明了问题的紧迫性。

8.  **[🔔] #35400 & #35399: 一个“计划”消耗约100个Credits / Credits管理混乱**
    - **链接**: https://github.com/openai/codex/issues/35400 , https://github.com/openai/codex/issues/35399
    - **重要性**: 这两个新Issue直接指向了用户对 Credits 计费模型的困惑与不满。高额消耗和计费不透明会严重影响用户信任和付费意愿。
    - **社区反应**: 均为今日创建的Open Issue，预示着一个新的焦点争议。

9.  **[🔔] #34471: Computer Use 插件无法加载 @oai/sky**
    - **链接**: https://github.com/openai/codex/issues/34471
    - **重要性**: 影响macOS 26系统上Computer Use功能的使用，该功能是Codex自动化的核心，此Bug会完全阻止其运行。
    - **社区反应**: 5条评论，0赞，但问题很具体，影响关键插件。

10. **[🔔] #35403 & #35402: Windows端Computer Use连接不可用 / 定时任务无法同步**
    - **链接**: https://github.com/openai/codex/issues/35403, https://github.com/openai/codex/issues/35402
    - **重要性**: 进一步印证了Windows平台在Computer Use和自动化同步等核心功能上存在大量新出现的问题。
    - **社区反应**: 今日新创建的Issue，凸显了Windows端问题的集中爆发。

### **重要 PR 进展**

以下是过去24小时内更新或合并的10个关键 PR：

1.  **[🔒] #35264: 对打包的 macOS 辅助二进制文件进行签名**
    - **链接**: https://github.com/openai/codex/pull/35264
    - **内容**: 修复了macOS发布流程中的一个关键漏洞，确保打包的 `rg` 和 `zsh` 等辅助工具能被正确的代码签名和公证，避免系统安全警告。
    - **重要性**: 直接影响macOS用户的应用可用性和安全性。

2.  **[🔒] #31782: 绑定 stdio JSON-RPC 帧大小**
    - **链接**: https://github.com/openai/codex/pull/31782
    - **内容**: 对 stdio JSON-RPC 帧大小设置了64MB的上限，防止恶意或行为异常的 exec-server 导致内存无限增长。
    - **重要性**: 重要的安全加固措施，提升了CLI与子进程通信的鲁棒性。

3.  **[🔒] #35280: 未配置允许列表时跳过插件 MCP 过滤**
    - **链接**: https://github.com/openai/codex/pull/35280
    - **内容**: 优化了插件MCP（模型上下文协议）服务器的过滤逻辑，若无配置则跳过过滤，避免误拦截。
    - **重要性**: 提升了插件的兼容性和灵活性，减少配置意外。

4.  **[🔒] #35267: 强化网络审批的取消与并发处理**
    - **链接**: https://github.com/openai/codex/pull/35267
    - **内容**: 重构了网络审批逻辑，解决并发和取消场景下的状态管理问题，避免资源泄漏或审批状态卡死。
    - **重要性**: 提升了高并发场景下网络策略的执行可靠性。

5.  **[🔒] #35271: 在 Responses Lite 元数据中包含 code-mode 工具名**
    - **链接**: https://github.com/openai/codex/pull/35271
    - **内容**: 将 `code_mode_tool_names` 添加到 Responses Lite 的元数据中，便于客户端识别和路由。
    - **重要性**: 为即将到来的 Code Mode 相关功能提供了必要的数据支持。

6.  **[🔒] #35266: 允许禁用进程内 code-mode host 回退**
    - **链接**: https://github.com/openai/codex/pull/35266
    - **内容**: 新增配置选项，允许在独立code-mode host启动失败时，不降级到内嵌V8，而是直接报错。
    - **重要性**: 为开发者提供了更明确的错误处理方式，而非静默降级。

7.  **[🔒] #35275: 追踪远程 exec-server 连接建立过程**
    - **链接**: https://github.com/openai/codex/pull/35275
    - **内容**: 增加了对远程环境连接建立过程的详细追踪日志，涵盖连接、环境注册、Noise协议、WebSocket等阶段。
    - **重要性**: 极大提升了远程环境启动问题的排查能力。

8.  **[🔒] #29752 (Open): 集成实验性凭据代理器**
    - **链接**: https://github.com/openai/codex/pull/29752
    - **内容**: 核心集成实验性凭据代理器，允许用占位符替换真实凭据，防止敏感信息泄露。
    - **重要性**: 一个长期运行的大型PR，对安全性有重大意义。

9.  **[🔒] #31810: 性能优化：管线化祖先目录发现**
    - **链接**: https://github.com/openai/codex/pull/31810
    - **内容**: 优化远程项目启动时，对项目祖先目录（查找 `.agents`、技能目录等）的发现过程，改为并行和管线化处理。
    - **重要性**: 显著提升远程项目的启动速度。

10. **[🔒] #35262 & #35261: 追踪远程插件ID至技能调用分析 & 元数据**
    - **链接**: https://github.com/openai/codex/pull/35262 , https://github.com/openai/codex/pull/35261
    - **内容**: 将远程插件的唯一ID传播到技能调用的分析事件和元数据中。
    - **重要性**: 为未来分析远程插件使用情况和性能提供了基础数据。
    - **团队反应**: 连续两个PR处理此功能，表明团队正在积极完善远程插件体系。

### **功能需求趋势**

从过去24小时的社区反馈中，可以提炼出以下关键功能需求趋势：

1.  **提升限额体验与可预测性**: 用户强烈要求将总量、重置周期、消耗速度变得更为透明和可预测。（#9508, #16423）
2.  **强化 Windows 平台兼容性**: 用户正遭遇Windows独有的大量Bug，包括换行符、远程控制、应用崩溃、插件安装失败等。已成为社区最集中的诉求。（#4003, #31786, #34299, #21674）
3.  **改进远程控制与跨设备体验**: 从Windows到Android/iOS的远程控制功能问题频发，用户期望一个稳定、无缝的远程连接体验。（#31786, #31973, #35403）
4.  **上下文与长会话优化**: 用户（尤其是Pro用户）担忧在长任务中，自动上下文压缩会丢失关键信息，要求更智能的上下文管理策略。（#29356）
5.  **增强自动化与技能**: 社区期望项目级别的技能自动发现、更可靠的定时任务执行、以及对Computer Use等自动化核心功能的稳定性提升。（#21907, #35402, #34471）

### **开发者关注点**

总结开发者与深度用户在反馈中的核心痛点：

- **速率限制的“黑箱”行为**: 许多用户依赖于每周额度来规划工作，非确定性的重置时间点打乱了他们的工作节奏，导致挫败感强烈。
- **Windows平台稳定性是首要矛盾**: 从文件处理到UI交互，再到核心的远程控制和自动化，Windows版Codex暴露出大量问题，严重影响了该平台用户的工作效率。
- **应用崩溃与数据损坏**: 用户报告了应用在访问任务时崩溃、本地状态文件损坏等问题（#35401, #29593），数据安全与稳定性是用户的底线关切。
- **Credits消耗不透明**: 新出现的关于单一“Plan”动作消耗约100个Credits的反馈（#35400），引发了社区对于新型功能计费模式的质疑与担忧，迫切需要官方的详细解释。
- **CLI 会话持久化缺陷**: 会话恢复时出现400错误

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

好的，这是为您生成的 2026 年 7 月 26 日 Gemini CLI 社区动态日报。

---

# Gemini CLI 社区动态日报 | 2026-07-26

## 今日速览

今日社区动态以深度技术改进和内部基础设施升级为主，未见新版本发布。**Agent 系统的稳定性和可靠性**是社区讨论的焦点，包括子代理成功状态误报和挂起问题。**内部团队正大力推进自动化 PR 生成（SSR Pipeline）和机器人评估（Caretaker）框架**的开发，表明项目正向着更自动化的运维和代码生成方向演进。

## 社区热点 Issues

1.  **[(#22323) 子代理超时后误报成功](https://github.com/google-gemini/gemini-cli/issues/22323)**
    - **重要性**: 🔴 高。这是一个核心 P1 级别的 Bug，直接导致用户对 Agent 执行结果的信任度降低。子代理明明因达到最大轮次限制而中断，却向主代理报告“成功”，这会误导用户决策。
    - **社区反应**: 该问题获得12条评论，是今日最活跃的讨论。开发者 @matei-anghel 详细报告了复现步骤，社区对此类“隐藏”故障深表关切。

2.  **[(#21409) 通用代理 (Generalist Agent) 挂起问题](https://github.com/google-gemini/gemini-cli/issues/21409)**
    - **重要性**: 🔴 高。作为一个 P1 的 Bug，它阻塞了所有需要通用代理处理的核心任务（如创建文件夹）。社区用户表示唯一规避方法是要求模型“不使用子代理”，这极大地限制了工具的实用性。
    - **社区反应**: 有 8 条评论和 8 个 👍，反映出这是一个影响广泛的普遍性问题。用户 @turmanticant 的反馈直接点出了关键痛点。

3.  **[(#28439) OAuth 认证缺失问题](https://github.com/google-gemini/gemini-cli/issues/28439)**
    - **重要性**: 🔴 高。这是一个关于安全与配置体验的 P2 Bug。用户期望开箱即用地进行 OAuth 认证，但当前强制要求手动设置 API Key 或环境变量，增加了使用门槛。
    - **社区反应**: 开发者 @0wwafa 的提问直接，5 条评论表明这不是个例，社区需要一个更友好的认证流程。

4.  **[(#25166) Shell 命令执行后假死/等待输入](https://github.com/google-gemini/gemini-cli/issues/25166)**
    - **重要性**: 🟠 中。P1 级别 Bug，严重影响交互式用户体验。命令明明已结束，但 CLI 界面显示仍在等待输入，用户被迫中断会话。
    - **社区反应**: 有 4 条评论和 3 个 👍，表明此问题反复出现。开发者将其标记为“effort/medium”，是团队正在关注的核心体验问题。

5.  **[(#24353) 鲁棒的组件级评估](https://github.com/google-gemini/gemini-cli/issues/24353)**
    - **重要性**: 🟠 中。这是一个 P1 的 EPIC Issue，是提升 Agent 质量的系统性工程。通过创建更细粒度的单元测试（Behavioral Evals），来保障每个组件（如 Shell、文件工具）的稳健性。
    - **社区反应**: 虽然外部评论不多，但该 Issue 作为内部工作流程的一部分，对推动产品质量有深远意义。

6.  **[(#26522) 自动记忆 (Auto Memory) 无限重试低价值会话](https://github.com/google-gemini/gemini-cli/issues/26522)**
    - **重要性**: 🟠 中。P2 级别 Bug，指出 Auto Memory 功能存在逻辑缺陷，会无限重试处理被自己判定为“低信号”的会话记录，造成计算资源和 Token 的浪费。
    - **社区反应**: 开发者 @SandyTao520 详细描述了问题，这属于系统内部优化问题，但对内部性能有显著影响。

7.  **[(#22745) 评估 AST 感知文件读取/搜索/映射的价值](https://github.com/google-gemini/gemini-cli/issues/22745)**
    - **重要性**: 🟢 低（但具有前瞻性）。这是一个 P2 的 EPIC Issue，探讨利用抽象语法树（AST）来提升 Agent 对代码的理解能力，例如精确读取一个方法，而不是整行。这能显著减少 Token 消耗和错误。
    - **社区反应**: 讨论集中在技术可行性上，显示了项目团队对前沿技术探索的追求。

8.  **[(#21968) Gemini 不会主动使用自定义技能 (Skills) 和子代理](https://github.com/google-gemini/gemini-cli/issues/21968)**
    - **重要性**: 🟠 中。P2 级别 Bug，揭示了模型在工具选择（Tool Calling）上的“惰性”。用户已经配置好了 Gradle、Git 等自定义技能，但 Gemini 在遇到相关任务时不会主动调用，必须用户明确指令。
    - **社区反应**: 用户 @rnett 的观察非常细致，这个问题直接关系到扩展生态的实际可用性。

9.  **[(#22672) Agent 应主动阻止/劝阻破坏性行为](https://github.com/google-gemini/gemini-cli/issues/22672)**
    - **重要性**: 🟢 低（但值得关注）。这是一个 P2 功能建议，触及到 Agent 安全使用的根本：模型有时会使用 `git reset --force` 等破坏性命令，社区希望 Agent 在行动前能有“风险意识”并提示用户。
    - **社区反应**: 仅有少量评论，但代表了用户对于 Agent 安全性的高期望。

10. **[(#21983) 浏览器子代理在 Wayland 上失败](https://github.com/google-gemini/gemini-cli/issues/21983)**
    - **重要性**: 🟠 中。P1 级别 Bug，明确指出了浏览器代理与特定显示服务器协议（Wayland）的兼容性问题。这会影响大量 Linux 用户的使用体验。
    - **社区反应**: 开发者 @sigmaSd 提供了错误日志，而团队也已在排查中（标签 `status/need-retesting`）。

## 重要 PR 进展

1.  **[#28401: 限制 Shell 命令输出长度](https://github.com/google-gemini/gemini-cli/pull/28401)**
    - **重要性**: 🔴 高。这是一个直接的关系到 Token 消耗和模型回复质量的关键修复。PR 为 Shell 工具的输出设置了上限，防止 `git log` 或 `find /` 等命令输出海量文本冲垮模型上下文。
    - **状态**: 等待进一步审查和合并。

2.  **[#28481: 修复 MCP OAuth 令牌刷新问题](https://github.com/google-gemini/gemini-cli/pull/28481)**
    - **重要性**: 🔴 高。针对 MCP (Model Context Protocol) 服务器的 OAuth 令牌刷新失败问题。此 Bug 会导致用户凭证失效，必须重复认证。修复此项对使用第三方工具的开发者至关重要。
    - **状态**: 等待合并。

3.  **[#28348: 修复 MaxListenersExceededWarning 和无限认证循环](https://github.com/google-gemini/gemini-cli/pull/28348)**
    - **重要性**: 🔴 高。修复了两个关键问题：API 重试时的内存泄漏和 Windows 平台上的无限 OAuth 认证循环。这直接提升了 CLI 的稳定性和跨平台体验。
    - **状态**: 已合并，对社区有直接影响。

4.  **[#28535: 修复性能测试中 Ripgrep 路径引用](https://github.com/google-gemini/gemini-cli/pull/28535)**
    - **重要性**: 🟠 中。一个快速的修复，确保性能测试能与最新的 API 兼容，防止 CI 流程因函数找不到而失败，维护了开发者内部测试流程的稳定性。
    - **状态**: 等待合并。

5.  **[#28534: 修复 CI 中 `staging-tmp` dist-tag 移除失败](https://github.com/google-gemini/gemini-cli/pull/28534)**
    - **重要性**: 🟠 中。修复了自动化发布流程中的一个时序问题，确保持续集成/持续部署（CI/CD）管道的可靠性。对社区无直接影响，但对保证发布质量很重要。
    - **状态**: 等待合并。

6.  **[#28531: 修复 Windows 上 CRLF 导致差异对比失败](https://github.com/google-gemini/gemini-cli/pull/28531)**
    - **重要性**: 🟠 中。解决了 Windows 用户在使用 Gemini Code Assist 时，代码变更的差异对比视图无高亮的问题。根因是 CRLF 和 LF 换行符的冲突。
    - **状态**: 等待合并。

7.  **[#28353: 防止 a2a 服务器 restore 命令的路径穿越](https://github.com/google-gemini/gemini-cli/pull/28353)**
    - **重要性**: 🟠 中。一个重要的安全加固。通过防御性编程，防止恶意用户通过 `restore` 命令读取系统任意文件（如 `/etc/passwd`）。
    - **状态**: 已合并。

8.  **[#28530 - #28532: PR 生成器 (pr-generator) 框架和评估工具](https://github.com/google-gemini/gemini-cli/pull/28530)**
    - **重要性**: 🟢 低（但具有前瞻性）。这是一个大型的内部项目“SSR Pipeline”的一部分。该系列 PR 引入了`pr-generator-core`、`pr-generator-orchestrator`、`pr-generator-agent`、`pr-generator-db`、`pr-generator-infra` 等一系列新包。
    - **简述**: 这套框架旨在自动化地将社区 Issue 转化为 PR 并部署测试，是项目向自动化运营迈出的一大步。PR 数量多（共6个），代码量巨大，值得关注。

9.  **[#28532: 为机器人评估 (caretaker) 添加黄金测试集收集工具](https://github.com/google-gemini/gemini-cli/pull/28532)**
    - **重要性**: 🟢 低（但具有前瞻性）。与 PR #28530 对应，这是一个用于评估 Issue 分类机器人（Caretaker Agent）的测试框架，通过收集“黄金”用例来客观评测机器人性能。
    - **状态**: 等待合并。

10. **[#28484: (已关闭) 修复 a2a 服务器 restore 命令](https://github.com/google-gemini/gemini-cli/pull/28467)**
    - **重要性**: 🟠 中。更新了流水线数据库（Firestore）的 schema，增加了错误追踪和 PR 编号字段。这是对现有的 Issue 分类机器人（caretaker-agent）后端进行功能增强。
    - **状态**: 等待合并。

## 功能需求趋势

从过去 24 小时的 Issue 和 PR 来看，社区关注的重点趋势如下：

- **Agent 系统可靠性与健壮性**: 这是最核心的趋势。多个 P1/P2 的 Bug（如超时误报、挂起、命令假死、不主动使用工具）都直接指向了 Agent 核心执行逻辑的不稳定。社区最迫切的需求是让 Agent“稳定地完成”任务。
- **内部评估与自动化基础设施**: 大量新 PR（`pr-generator-*` 和 `caretaker-*`）和 Issue（`#24353`）表明，团队正投入巨大精力构建自动化测试、代码生成和 Issue 分类管道。这是从“能工作”向“高质量、可持续”演进的关键。
- **安全与内容隔离**: 从 `#28439`（OAuth 缺失）到 `#26525`（记忆系统的确定性脱敏）再到 `#28353`（路径穿越修复），安全和隐私是高级用户的核心顾虑。
- **Agent“自我意识”与工具使用能力**: 社区希望 Agent 能更好地理解和使用自身生态。`#21968`（不主动用技能）和 `#21432`（准确了解自身 CLI 标志和热键）都反映了这种期望，即 Agent 应像一位“专家”一样使用自己的工具。

## 开发者关注点

- **稳定性痛点**: 通用代理挂起、子代理误报成功、Shell 命令假死——这些都是开发者日常使用中“打断工作流”的致命问题。开发者宁可功能少一点，也希望基础交互是可靠的。
- **配置与易用性**: 缺少开箱即用的 OAuth 认证、自定义技能不被主动使用，这些问题提高了使用门槛，开发者希望工具能“更智能”地适配自己的环境。
- **Token 与性能敏感**: 开发者非常在意 Token 的消耗。对 Shell 输出截断的 PR、以及 AST 感知工具的探索，都表明社区和团队都在积极优化性价比，避免因输出过多导致模型“变笨”或成本飙升。
- **跨平台兼容性**: 浏览器代理在 Wayland 上失败、Windows 上差异对比因换行符问题失效，这些细分平台的 Bug 反映出跨平台兼容性仍需打磨，尤其是对 Linux 桌面用户而言。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-07-26

## 今日速览
今日无新版发布，但社区提交了多项高影响 bug 报告，包括会话恢复时内存溢出（OOM）、`/ask` 命令频繁无响应、插件市场注册后不持久等严重问题。多个涉及会话生命周期与模型配置的缺陷集中爆发，开发者体验可能受到明显影响。

## 版本发布
（无新版本）

## 社区热点 Issues
以下为过去24小时内活跃或新提交的10个值得关注的 Issue（按优先级排列）：

1. **#4251** — [area:sessions] 恢复大型会话时 OOM / 单核 100% 持续约70分钟（1.0.74 回归）  
   [链接](https://github.com/github/copilot-cli/issues/4251)  
   **关键点**：版本 1.0.74 相比 1.0.73 内存占用高出 3–4 倍，导致长期运行的大会话无法恢复。社区已给出 A/B 复现数据，影响面广。

2. **#4253** — `/ask` 频繁返回无结果（1.0.75）  
   [链接](https://github.com/github/copilot-cli/issues/4253)  
   **关键点**：用户反馈 `/ask` 命令执行后无输出也无错误，严重影响日常查询功能。当前版本号最新，可能为新引入的 bug。

3. **#4246** — [area:sessions] `archive_session` 超时后遗留大型 worktree 孤儿  
   [链接](https://github.com/github/copilot-cli/issues/4246)  
   **关键点**：归档超时后 session 和 worktree 无法安全回收，导致磁盘空间泄漏，且无法重用 session 分支。

4. **#4247** — [area:plugins] 插件市场 `add` 显示成功但注册未持久化  
   [链接](https://github.com/github/copilot-cli/issues/4247)  
   **关键点**：`copilot plugin marketplace add` 成功后，`list` 和 `browse` 均提示 “not found”，说明磁盘写入缺失，插件安装流程失效。

5. **#4183** — [area:context-memory] 自动压缩未防止 CAPI 5MB 限制来自积累的工具历史  
   [链接](https://github.com/github/copilot-cli/issues/4183)  
   **关键点**：虽然模型上下文 token 未超限，但序列化后的请求体超过 5MB 限制，自动压缩策略对此无效。会话越长越容易触发，社区投 👍 达 10 次。

6. **#4252** — [area:sessions] 会话退出时将启动时的 `model` 写回 settings.json，覆盖用户后续编辑  
   [链接](https://github.com/github/copilot-cli/issues/4252)  
   **关键点**：多会话场景下，退出时的写回操作会回滚其他会话或手动修改的配置，导致模型设置自行“回血”，属隐蔽数据丢失。

7. **#4241** — [area:tools] 密码屏蔽功能反而导致 agent 用额外 token 读取原始字节  
   [链接](https://github.com/github/copilot-cli/issues/4241)  
   **关键点**：密码屏蔽触发 agent 自动用 Python 绕过屏蔽读取原始文件，既浪费 token 又可能陷入密码解析死循环，设计缺陷。

8. **#4244** — [area:sessions] 在 VS Code agent 会话中不支持 `/rename`，且 agent 无法主动调用  
   [链接](https://github.com/github/copilot-cli/issues/4244)  
   **关键点**：终端 CLI 已有 `/rename`，但 VS Code 内嵌 agent 窗口缺失，用户只能通过 VS Code UI 操作，且 agent 无法编程式重命名，限制跨 IDE 一致性。

9. **#4249** — [area:sessions] 计划指示器在 headless 会话切换后泄漏到另一会话  
   [链接](https://github.com/github/copilot-cli/issues/4249)  
   **关键点**：IDE 在不同对话间切换同一进程时，plan indicator 未正确清理，导致上下文污染。

10. **#2205** — [area:terminal-rendering] 鼠标滚动在 Terminator 中无法滚动历史输出，反而滚动输入列表  
    [链接](https://github.com/github/copilot-cli/issues/2205)  
    **关键点**：长期存在的终端渲染可用性问题，社区 13 条评论、14 个 👍，影响鼠标交互用户。

## 重要 PR 进展
过去24小时内仅有两条 PR 被更新，均不涉及功能改进或 bug 修复：

- **#23**（已关闭）—— 早期设计文档，无实际代码变更。  
  [链接](https://github.com/github/copilot-cli/pull/23)

- **#4228**（已关闭）—— 提交者自行撤回，原因是 PR 错误修改了文档而非私有剪贴板运行时实现。  
  [链接](https://github.com/github/copilot-cli/pull/4228)

**结论**：今日无实质性 PR 合并或新功能推进。

## 功能需求趋势
从所有活跃 Issue 可提炼出社区最关注的几个方向：

1. **会话生命周期稳定性**：多会话并发、恢复、归档、切换时出现 OOM、超时、内容泄漏、配置回滚等严重问题，请求优化会话管理机制。
2. **IDE 深度集成**：`/rename` 支持、密码屏蔽行为、计划指示器等在终端与 VS Code 代理之间不一致，要求统一体验。
3. **插件/市场可靠性**：市场注册不持久、技能列表超过32个后不可见、部分市场 schema 验证失败，插件生态的基础设施需要打磨。
4. **大型模型会话性能**：自动压缩无法应对 CAPI 5MB 限制、恢复时内存暴涨，急需改进长会话的序列化与分页策略。
5. **配置持久化安全**：`model` 字段在退出时覆盖用户手动修改，暴露配置竞争问题，期望采用显式同步或时间戳防冲突。

## 开发者关注点
综合反馈，当前开发者体验中高频痛点包括：

- **资源占用过高**（#4251）—— 版本升级导致 OOM，影响日常开发。
- **核心命令失效**（#4253）—— `/ask` 无响应，相当于丢失了最重要的提问入口。
- **插件生态不可靠**（#4247、#1464、#1996）—— 安装、注册、使用各环节均出现失败，降低采用信心。
- **隐蔽的数据覆盖**（#4252）—— 配置静默回退，用户可能长时间未察觉。
- **跨 IDE 行为不一致**（#4244）—— 功能碎片化增加学习成本。

建议贡献者与用户优先关注上述 Issue，并考虑在下一个版本中修复这些影响基础体验的缺陷。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-07-26）

## 今日速览

过去 24 小时内，Kimi Code CLI 社区主要聚焦于 **远程会话控制**（#1282）的长期讨论热度不减，同时新上报的 **死循环 bug**（#2557）引发开发者关注。在代码层面，开发者 @Nas01010101 连续关闭了三个修复 PR，重点解决了会话恢复时系统提示冻结、Web 文件重传以及 fork/undo 上下文截断的问题；另有开发者提交了 Windows 测试兼容性修复 PR #2558。

## 社区热点 Issues（共 2 条）

### #1282 [增强] 远程控制：支持从任意设备继续本地会话
- **作者**：@CatKang
- **创建**：2026-02-27 | **更新**：2026-07-25
- **状态**：Open | **评论**：8 | **👍**：16
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/1282
- **摘要**：提议增加远程控制功能，允许用户通过手机、平板或浏览器继续本地的 Kimi Code CLI 会话，以实现工作流无缝切换，保持完整的本地环境。
- **重要性**：该 issue 长期获得较多关注（16 👍），反映了用户对跨设备连续工作的强烈需求。虽然已提出近 5 个月，但仍未落地，可能是 CLI 架构上的挑战。

### #2557 [Bug] 死循环
- **作者**：@zxpdemonio
- **创建**：2026-07-25 | **更新**：2026-07-25
- **状态**：Open | **评论**：0 | **👍**：0
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2557
- **摘要**：用户运行 kimi-cli 1.44.0 并使用 Kimi Code 订阅时遇到死循环问题，未提供更多信息。
- **重要性**：这是新上报的严重 bug，虽无评论和点赞，但死循环直接影响使用体验。建议开发者尽快复现并定位原因。

## 重要 PR 进展（共 4 条）

### #2520 [已合并] 修复(session)：对齐 fork/undo 上下文截断到 wire turns
- **作者**：@Nas01010101
- **创建**：2026-07-19 | **更新**：2026-07-25
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2520
- **摘要**：修复 #2517，同时解决 #1974（wire-only slash turns 导致 undo 截断偏移）和 #2049（fork/undo 后历史不匹配）。PR 还提到与 #2386 的关系。
- **重要性**：解决了长期存在的会话 fork 和 undo 历史错乱问题，属于核心稳定性修复。

### #2519 [已合并] 修复(app)：会话恢复时刷新过期冻结的系统提示
- **作者**：@Nas01010101
- **创建**：2026-07-19 | **更新**：2026-07-25
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2519
- **摘要**：修复 #2420。恢复会话时无条件采用 context.jsonl 中冻结的 `_system_prompt`，导致新增技能（`~/.kimi/skills/`）或 `AGENTS.md` 修改无法生效。修复后允许用户自定义配置动态更新。
- **重要性**：解决了用户自定义技能无法在恢复后生效的痛点，提升可扩展性。

### #2518 [已合并] 修复(web)：持久化上传文件的 .sent 标记，避免服务重启后重新发送文件
- **作者**：@Nas01010101
- **创建**：2026-07-19 | **更新**：2026-07-25
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2518
- **摘要**：修复 #2413。`kimi web` 模式下，服务器重启后会将之前所有已上传的文件（包括图片）再次随下一条提示发送，污染会话。通过持久化 `.sent` 标记避免重复上传。
- **重要性**：显著改善 Web 模式下的用户体验，避免不必要的资源浪费和会话混乱。

### #2558 [Open] 修复(测试)：改进 Windows 跨平台测试兼容性
- **作者**：@panandicoding
- **创建**：2026-07-25 | **更新**：2026-07-25
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2558
- **摘要**：修复两个 Windows 兼容性问题：1）`test_background_tools.py` 中 `Path.write_text()` 未设置 `newline=""` 导致 `\n` 被转换为 `\r\n`；2）其他未列出的问题（小于 100 行）。
- **重要性**：提升 CI 在 Windows 环境下的可靠性，降低跨平台测试失败率。

## 功能需求趋势

从近期 issue 和 PR 中可看出社区关注的核心方向：

1. **远程协作与跨设备**：issue #1282 获得持续关注，用户希望从手机/浏览器远程控制 CLI 会话，实现工作流连续性。
2. **会话稳定性与上下文管理**：多个 PR（#2520、#2519）聚焦于会话恢复、fork/undo 逻辑，表明用户对会话一致性和自定义配置持久化的要求日益增长。
3. **多平台兼容性**：Windows 测试问题 PR #2558 体现开发者对平台一致性的重视，尤其在跨平台工作流场景下。
4. **Web 模式体验优化**：修复文件重复上传（#2518）表明 Web 前端用户正在增多，对状态持久化有明确需求。

## 开发者关注点

- **会话恢复后自定义技能失效**（#2519 修复）是长期痛点，开发者希望自定义配置能够动态生效。
- **Web 模式文件重复上传**（#2518 修复）严重影响使用体验，尤其在多次重启场景下。
- **死循环 bug**（#2557）为刚报告的新问题，需快速定位以避免影响用户体验。
- **Windows 测试兼容性**（#2558）虽然是小改动，但反映出跨平台 CI 仍存在碎片化问题。
- **远程控制**（#1282）虽未实现，但该需求若满足，将极大扩展 Kimi Code CLI 的适用场景，可能成为下一个重大特性。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 | 2026-07-26

> 数据来源：[github.com/anomalyco/opencode](https://github.com/anomalyco/opencode)  
> 统计周期：2026-07-25 日更新内容

---

## 今日速览

社区最受关注的两大话题：**新版桌面 UI 布局争议**（#37012，33评论）与 **CPU 飙升问题**（#30086，36评论）持续发酵。同时，大量用户反馈 Desktop v1.18.5 存在项目关闭/切换冻结、后端服务间歇性返回 500 等稳定性问题。PR 方面，一批长期积压的「自动化清理」PR 于今日统一合并，并有一个新 PR 尝试优化会话自动压缩时机。

---

## 版本发布

过去 24 小时内无新版本发布。

---

## 社区热点 Issues（Top 10）

1. **[#30086] High CPU usage in newer versions of OpenCode**  
   🔥 36 评论 / 19 👍  
   用户反馈近期更新后 CPU 占用飙升，从可同时运行 10 个会话退化到 3 个即卡顿，鼠标延迟明显。社区正在积极排查，可能与后台轮询或渲染循环有关。  
   [查看详情](https://github.com/anomalyco/opencode/issues/30086)

2. **[#37012] [FEATURE]: keep legacy layout option**  
   🔥 33 评论 / 31 👍  
   大量用户呼吁保留旧版布局，认为新 UI 层级过深、功能入口分散。该议题支持数极高，是当前 UI 改版争议的核心。  
   [查看详情](https://github.com/anomalyco/opencode/issues/37012)

3. **[#24649] OpenCode Go: clarify which models are self-hosted vs. proxied**  
   💬 13 评论 / 31 👍  
   用户质疑 Go 订阅计划文档中关于基础设施的描述，要求明确哪些模型是自托管、哪些经过第三方代理。涉及定价透明度。  
   [查看详情](https://github.com/anomalyco/opencode/issues/24649)

4. **[#32747] @ file mentions do not include files created after startup**  
   💬 12 评论 / 9 👍  
   新创建的文件在 TUI 中无法通过 `@` 提及，需重启应用。已定位到搜索状态未及时刷新。  
   [查看详情](https://github.com/anomalyco/opencode/issues/32747)

5. **[#38789] Desktop v1.18.5: UnsupportedContentType error on project reload**  
   💬 7 评论  
   升级后启动时提示“UnsupportedContentType”，根源在客户端 SDK 生成代码对某个字段类型处理不兼容。  
   [查看详情](https://github.com/anomalyco/opencode/issues/38789)

6. **[#31217] TUI prompt input fail on Enter**  
   💬 6 评论  
   终端输入框中按 Enter 后文字消失但未提交，中英文均受影响。斜杠命令正常，疑似事件处理逻辑缺陷。  
   [查看详情](https://github.com/anomalyco/opencode/issues/31217)

7. **[#20252] [FEATURE]: 建议出年费套餐，并且支持开发票**  
   💬 6 评论  
   企业用户需求：增加年费选项并支持发票，便于公司采购。  
   [查看详情](https://github.com/anomalyco/opencode/issues/20252)

8. **[#38801] message="exiting loop"**  
   💬 5 评论  
   用户反复遇到“exiting loop”错误导致 TUI 无法正常使用，涉及 OpenAI 兼容 API 的循环退出条件判断。  
   [查看详情](https://github.com/anomalyco/opencode/issues/38801)

9. **[#36677] core: long-lived V2 server enters persistent allocation loop**  
   💬 3 评论  
   长期运行的 `opencode2 serve` 进程出现高频 JS 分配循环，吃掉一个 CPU 核和 1.1~1.3 GB 内存，属于核心性能回归。  
   [查看详情](https://github.com/anomalyco/opencode/issues/36677)

10. **[#34442] Windows Desktop installer is broken offline: ripgrep not bundled**  
    💬 2 评论 / 3 👍  
    离线环境安装后三个核心工具（grep, glob, skill）因缺少 ripgrep 而失效，严重影响企业内网用户。  
    [查看详情](https://github.com/anomalyco/opencode/issues/34442)

---

## 重要 PR 进展（Top 10）

1. **[#38901] fix(session): defer auto-compaction until the next model input**  
   🆕 新提交，待审查  
   将自动上下文压缩从助手步骤结束后延迟到下一次模型输入前执行，避免在会话滚动或切换时触发不必要的压缩运算。  
   [查看详情](https://github.com/anomalyco/opencode/pull/38901)

2. **[#38200] feat: add support for Solidity file type and highlighting**  
   🕐 进行中  
   为 Solidity 智能合约代码添加语法高亮支持。  
   [查看详情](https://github.com/anomalyco/opencode/pull/38200)

3. **[#33950] fix(acp): show real tool context in permission prompt title**  
   ✅ 已合并  
   ACP 权限对话框标题原只显示工具类型（bash/edit），现在显示实际上下文内容，减少用户困惑。  
   [查看详情](https://github.com/anomalyco/opencode/pull/33950)

4. **[#33948] fix(tui): avoid rendering "1000.0K" in compact number formatting**  
   ✅ 已合并  
   修复 TUI 中数字格式化显示“1000.0K”的不规范问题，统一为“1.0M”。  
   [查看详情](https://github.com/anomalyco/opencode/pull/33948)

5. **[#33943] fix(app): restore timeline scroll position**  
   ✅ 已合并  
   在切换标签页或重载时，保留会话时间线的精确滚动位置（包括虚拟行和视口偏移）。  
   [查看详情](https://github.com/anomalyco/opencode/pull/33943)

6. **[#33927] fix(vcs): prevent crash when repo has thousands of untracked files**  
   ✅ 已合并  
   仓库含大量未追踪文件（1200+）时，VCS 层不再崩溃，改用流式/分批处理。  
   [查看详情](https://github.com/anomalyco/opencode/pull/33927)

7. **[#33925] feat(core): load native provider packages**  
   ✅ 已合并  
   重构核心配置和提供者加载逻辑，支持 flat package/settings 模式，为后续原生包集成奠定基础。  
   [查看详情](https://github.com/anomalyco/opencode/pull/33925)

8. **[#33912] fix(upgrade): authenticate GitHub release checks**  
   ✅ 已合并  
   版本检查时使用 `GITHUB_TOKEN` 作为 Bearer Token，避免 API 限流导致升级检测失败。  
   [查看详情](https://github.com/anomalyco/opencode/pull/33912)

9. **[#33900] feat(opencode): implement VCS backend commit primitive (Phase 1A)**  
   ✅ 已合并  
   实现 Git 版本控制面板的第一阶段：无状态 `/vcs/commit` 后端原语，为后续 UI 操作提供支持。  
   [查看详情](https://github.com/anomalyco/opencode/pull/33900)

10. **[#33897] fix(lsp): send pyright venv initialization**  
    ✅ 已合并  
   修复 Pyright LSP 在检测到项目虚拟环境后，未正确发送 `venvPath` / `venv` 配置的问题。  
    [查看详情](https://github.com/anomalyco/opencode/pull/33897)

---

## 功能需求趋势

从近期 Issue 中可以提炼出社区最关注的几个功能方向：

- **UI 可配置性**：旧版布局保留需求（#37012）支持数高达 31 👍，说明用户对新 UI 的适配有强烈保留意见，希望提供“经典模式”开关。
- **企业级订阅**：年费套餐、发票支持（#20252）反复出现，指向大型团队采购场景。
- **离线与自部署**：Windows 离线安装 ripgrep 缺失（#34442）、LAN 内 Ollama 连接失败（#38854）等，体现对完全离线/内网环境稳定运行的刚性需求。
- **输入与交互改进**：移动端粘贴问题（#38850）、TUI 斜杠命令误触（#31217）、会话滚动位置保持（#33943一致）等，反映社区对基础交互体验的精细要求。
- **模型透明性**：自托管 vs 代理模型澄清（#24649），用户希望在定价和基础设施上获得更高透明度。

---

## 开发者关注点

- **性能退化**：CPU 飙升（#30086）和内存泄漏（#36677）是当前最严重的痛点，直接影响日常使用体验。
- **桌面端稳定性**：v1.18.5 的“UnsupportedContentType”错误（#38789）、关闭项目冻结（#38885）、切换项目不刷新（#37534）等，表明桌面版近期存在多处回归。
- **API/Backend 故障**：7月25日部分用户报告托管模型连续返回 500 / 超时（#38874），以及“exiting loop”错误（#38801），影响免费和付费用户。
- **跨平台差异**：Windows 离线安装、macOS 下 LAN 连接 Ollama、Android 粘贴失效等，测试覆盖存在盲区。
- **会话管理**：新文件无法通过 `@` 提及（#32747）、导入会话后循环卡死（#38791），索引和消息 ID 排序逻辑有改进空间。

---

*以上日报基于 2026-07-25 的 GitHub 数据自动整理，供社区参考。*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 | 2026-07-26

## 今日速览
- **Nightly 版本发布**：v0.21.0-nightly.20260725 修复了 insight 时区显示问题，并重构了 autofix 扩展机制。
- **社区核心 bug 集中爆发**：v0.21.0 引入的终端滚动偏移、输入法候选框错位、技能自动补全断裂等问题成为用户反馈热点，多个 P2 级 issue 被激活。
- **新功能方向加速**：子代理模型等级选择、外部上下文提供者配置、数学公式显式语法提案等特性需求收到社区积极讨论。

---

## 版本发布
- **[v0.21.0-nightly.20260725](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.0-nightly.20260725.1183a4c82)**  
  包含两个主要变更：
  - `fix(cli):` 将 insight 统计中的天和小时统一为本地时间测量（#7670）
  - `refactor(autofix):` 对 autofix 扩展层进行重构（后续补全）

---

## 社区热点 Issues（10 条）

1. **#5800** — 终端超长回复最后一行被覆盖  
   [链接](https://github.com/QwenLM/qwen-code/issues/5800)｜8 评论  
   *重要性*：影响默认终端模式下所有长回复用户，属渲染层根本性 bug，上游依赖 Ink#973。社区已给出复现步骤，等待 triage。

2. **#7665** — 新手安装后报错 520/522  
   [链接](https://github.com/QwenLM/qwen-code/issues/7665)｜5 评论  
   *重要性*：用户刚安装桌面版即遇到 HTTP 错误，严重阻碍上手。虽可能是临时网络问题，但缺乏清晰错误指引，社区关注度高。

3. **#7684** — Command 模式下输入法候选框显示位置错误（macOS）  
   [链接](https://github.com/QwenLM/qwen-code/issues/7684)｜5 评论  
   *重要性*：影响 macOS 中文输入用户日常工作流，属于多行 statusline 引发的 UI 位置计算偏差，P2 级别。

4. **#7697** — VS Code 扩展无法连接 Unity MCP（Claude Code 可连接）  
   [链接](https://github.com/QwenLM/qwen-code/issues/7697)｜4 评论  
   *重要性*：明确暴露出 MCP 集成与 VS Code 扩展之间的兼容性 gap，对游戏开发场景用户关键。

5. **#7717** — 多技能连续触发时自动补全断裂  
   [链接](https://github.com/QwenLM/qwen-code/issues/7717)｜2 评论  
   *重要性*：更新后回归 bug，影响批量技能调用效率，已标记 `ready-for-agent` 等待修复。

6. **#7713** — v0.21.0 输入一个字符终端自动上滚一行  
   [链接](https://github.com/QwenLM/qwen-code/issues/7713)｜1 评论  
   *重要性*：提示行高度计算偏差（off-by-one）导致每次按键终端上滚，严重破坏交互体验，属于 P2/P1 级问题。

7. **#7700** — 数学公式显式语法提案  
   [链接](https://github.com/QwenLM/qwen-code/issues/7700)｜3 评论  
   *重要性*：希望定义一种源保持的数学标记合同，解决当前 `$x$` 识别遗漏、复制/表格/流式渲染不一致的问题，是 math-heavy 用户的核心需求。

8. **#7585** — 外部上下文提供者配置提案  
   [链接](https://github.com/QwenLM/qwen-code/issues/7585)｜6 评论  
   *重要性*：提出通过扩展机制让 CLI 进程共享仓库级上下文，不修改核心。反映出社区对知识服务集成（如记忆或合规知识库）的强烈需求。

9. **#7719** — CLI 不显示 token 用量/百分比  
   [链接](https://github.com/QwenLM/qwen-code/issues/7719)｜3 评论  
   *重要性*：用户无法监控会话 token 消耗，对付费 API 用户尤为关键。属于暴露性缺失，提出后将获不少关注。

10. **#7671** — Plan 模式手动退出时模型未收到通知 + 拒绝错误不友好  
    [链接](https://github.com/QwenLM/qwen-code/issues/7671)｜3 评论  
    *重要性*：涉及 Plan 模式状态管理，模型在手动切换模式时得不到清理，且错误提示含糊，影响子代理工作流的可靠性。

---

## 重要 PR 进展（10 条）

1. **[#7728](https://github.com/QwenLM/qwen-code/pull/7728)** — feat(webui): 新增 workspace Channel 管理 hook  
   为 WebUI 增加工作区级别的 Channel 数据层，支持加载目录、创建/更新配置、启停管理。

2. **[#7710](https://github.com/QwenLM/qwen-code/pull/7710)** — feat(triage): 添加沙箱 `/verify` 深度验证通道  
   在 triage 工作流中增加按需深度验证：评论 `@qwen-code /verify` 可触发 A/B 构建测试、空测试检查、mock-free wire oracle 等。

3. **[#7729](https://github.com/QwenLM/qwen-code/pull/7729)** — feat(core): 添加 Goal v3 worker tools  
   引入 read/update 两个 worker 工具，允许精确回合内访问 Goal 快照、证据目录及验证反馈。

4. **[#7529](https://github.com/QwenLM/qwen-code/pull/7529)** — fix(core): 修复 `humanReadableCron` 命名可能不发生的间隔  
   `*/N` 步骤现在只在字段内实际有效时才显示友好文本，否则回退原始表达式。

5. **[#7620](https://github.com/QwenLM/qwen-code/pull/7620)** — fix(web-shell): 解析 ANSI 256 色和真彩色序列  
   `parseAnsi` 此前将 `38`/`48`/`58` 的参数误当作简单代码，现在正确消费扩展颜色参数。

6. **[#7726](https://github.com/QwenLM/qwen-code/pull/7726)** — fix(weixin): 创建账号凭证文件时直接设为私有权限  
   修复文件先写入后收紧权限的时间窗，避免 API token 被组/其他用户读取。

7. **[#7531](https://github.com/QwenLM/qwen-code/pull/7531)** — fix(core): 补全 `AUTO` 破坏性 git 保护中的强制标记和 checkout 缺口  
   扩大 `DESTRUCTIVE_GIT_PATTERNS` 覆盖范围，确保 `git clean` 和 `git checkout` 的变体形式均被拦截。

8. **[#7725](https://github.com/QwenLM/qwen-code/pull/7725)** — fix(ci): 去除 tool-control E2E 的 flaky 并添加 autofix 波动检测  
   将 5 个依赖真实模型的测试迁移至 `fake-openai-server`，并在 autofix 工作流中增加波动预检。

9. **[#7727](https://github.com/QwenLM/qwen-code/pull/7727)** — fix(channels): GitHub 适配器使用 username 作为 senderId  
   修复因使用数字 user ID 导致 allowlist 门控失效的问题，使配对存储和机器人自过滤正确工作。

10. **[#7730](https://github.com/QwenLM/qwen-code/pull/7730)** — fix(core): 上下文文件优先级高于基础 prompt 默认值  
    在系统提示中明确声明 `QWEN.md`/`AGENTS.md` 规则覆盖基础 prompt 冲突时的优先级。

---

## 功能需求趋势

从过去 24 小时的 Issues 中提炼出社区最关注的几个方向：

| 方向 | 代表 Issue | 说明 |
|------|-----------|------|
| **MCP 集成与扩展互操作** | #7585、#7697、#7618 | 外部上下文提供者、Unity MCP 连接失败、Cua Driver 上游依赖关系 |
| **终端渲染 & 数学公式** | #5800、#7700、#7699 | 长回复覆盖、数学标记不一致、源保持语法提案 |
| **子代理 & 模型等级选择** | #7685、#7702 | 子代理 spawn 时选择不同模型等级（small/medium/high） |
| **Token 使用量监控** | #7719 | CLI 界面缺少 token 消耗统计 |
| **技能系统优化** | #7717、#7347 | 多技能自动补全断裂、技能默认禁用可覆盖性 |
| **记忆与持久化** | #6801、#7671 | 只读 pinned 目录保护、Plan 模式退出通知 |
| **认证与授权** | #7726、#7503 | OAuth 回调转发文档、微信凭证文件权限 |

---

## 开发者关注点

- **终端 UI 回归**：v0.21.0 引入的滚动偏移（#7713）和输入法候选框错位（#7684）严重干扰日常操作，社区反馈集中，开发者应优先排查渲染层高度计算逻辑。
- **技能自动补全断裂**：多技能连续输入时只有第一个触发补全（#7717），属于近期更新导致的回归，影响批量工作流。
- **CI 稳定性问题**：E2E 测试 flaky（#7712）和自动修复工作流的重复标记冲突（#7723）暴露出测试基础设施的维护压力。
- **扩展安装失败**：#7568 显示从一个扩展仓库安装多个子扩展时因 id 归属检查失败，提示不够友好。
- **数学公式渲染不一致**：`$x$` 等单字符表达式被错过、/copy 和流式 tokenization 分歧（#7699），对学术/科研用户是刚需 bug。
- **子代理保护不足**：扩展提供的子代理可被修改（#7242），社区期待更严格的读写权限隔离。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*