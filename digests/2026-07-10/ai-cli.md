# AI CLI 工具社区动态日报 2026-07-10

> 生成时间: 2026-07-09 23:40 UTC | 覆盖工具: 7 个

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

好的，作为专精 AI 开发工具生态的技术分析师，我已根据您提供的七份 AI CLI 工具社区动态日报，完成了数据的整理、分析与横向对比。以下是 2026-07-10 的生态综合分析报告。

---

## AI CLI 开发工具生态横向对比分析报告 (2026-07-10)

### 1. 生态全景

当前 AI CLI 工具生态正呈现 **“百花齐放，快速迭代”** 的繁荣态势。主流工具均维持着极高的更新频率，部分工具（如 OpenAI Codex、OpenCode）甚至在同一日发布多个补丁版本。社区反馈显示，开发者已从对 AI 编码助手的新奇感，转向对 **稳定性、成本可控性、安全性和精细化控制权** 的务实要求。同时，**“回归 Bug”** 和 **“新功能副作用”** 成为社区高频抱怨点，表明在追求功能创新的同时，质量保障（QA）流程面临巨大挑战。工具间的功能趋同现象明显，差异化竞争正聚焦于**特定工作流深度优化**和**开源生态建设**。

### 2. 各工具活跃度对比（2026-07-10）

| 工具名称 | 版本发布 | 热点 Issues (Top 10) | 重要 PR (Top 10) | 社区活跃度评估 | 核心态势 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 无 | 26条评论+ | 4个 (含社区贡献) | 高 | 核心痛点：Token 消耗异常、权限系统、Agent控制、跨平台稳定性。 |
| **OpenAI Codex** | 3个 (含1个Alpha) | 176条评论+/279个👍 | 10个 | 很高 | 功能迭代快，但 “新版本Bug” 多。核心痛点：新模型兼容性、信用额度、Windows性能、MCP进程泄漏。 |
| **Gemini CLI** | 无 | 聚焦4个核心Bug | 10个 (含重要安全修复) | 中高 | 聚焦代理稳定性和安全。核心痛点：Subagent误报、Agent挂起、Wayland兼容性。 |
| **Copilot CLI** | 1个 (v1.0.70-0) | 10个 (含多个新功能请求) | 0个 (当日) | 中 | 功能更新较稳，社区需求偏向于**配置灵活性和平台兼容性**。核心痛点：TUI挂死、模型控制、插件作用域。 |
| **Kimi Code CLI** | 无 | 2个 | 3个 | 低 | 社区规模较小，但正向演进。积极拥抱生态兼容性（如支持 CLAUDE.md）。 |
| **OpenCode** | 3个 (补丁日) | 聚焦复制Bug、CPU高、V2稳定性 | 10个 | 高 | V2 版本进入密集修复期，社区反馈集中在**基础体验**（复制功能）。核心痛点：剪贴板、子Agent挂起、V2稳定性。 |
| **Qwen Code** | 1个 (cua-driver) | 聚焦图片粘贴回归、多工作区、安全问题 | 10个 | 中高 | 功能迭代密集，安全与性能问题曝光率上升。核心痛点：图片粘贴、凭证泄漏、Glob OOM、IDE集成。 |

**结论：** OpenAI Codex 和 Claude Code 是社区关注度最高、讨论最热烈的两大头部工具。OpenCode 和 Qwen Code 则展现出极强的迭代速度，属于“追赶者”。Gemini CLI 和 Copilot CLI 社区规模稳定，但问题也相对集中。

### 3. 共同关注的功能方向

多个工具的社区不约而同地指向了以下四个核心方向：

| 功能方向 | 涉及工具 | 社区具体诉求 |
| :--- | :--- | :--- |
| **1. Token 消耗与成本透明** | **Claude Code** (#67506, #64961), **OpenAI Codex** (#30364), **Copilot CLI** (#2627) | 要求模型实际行为与宣传性价比一致；需要实时消耗统计、硬性上限和成本预测；对“Token 失控”和异常 Session 消耗感到焦虑。 |
| **2. Agent 控制与任务管理** | **Claude Code** (#34476), **Gemini CLI** (#21409, #22323), **OpenCode** (#33028), **Qwen Code** (#6569) | 呼吁精细的权限控制（如复合命令）；要求能够优雅地取消或停止正在运行的子 Agent；希望有更清晰的子 Agent 执行轨迹和干预能力。 |
| **3. 安全与权限控制** | **Claude Code** (#16561), **Gemini CLI** (#28319, #28232, #28327), **Qwen Code** (#6601, #6599), **OpenCode** (#36159) | 需要更严格的沙箱隔离和凭证保护（如环境变量泄漏）；要求更智能的权限审批模式（如读写分离）；对CI/CD管道中的供应链攻击风险深感不安。 |
| **4. 跨平台稳定性** | **Claude Code** (#68146, #76187), **OpenAI Codex** (#20214, #28855), **Gemini CLI** (#21983), **Copilot CLI** (#4069) | **Windows** 和 **Linux** 用户普遍感到体验不佳。核心痛点包括应用冻结、输入延迟、特定终端的 TUI 挂死、Wayland 兼容性、以及 Docker 环境下守护进程不稳定。 |

### 4. 差异化定位分析

| 工具名称 | 功能侧重 | 目标用户画像 | 技术路线与社区策略 |
| :--- | :--- | :--- | :--- |
| **Claude Code** | **全能开发助手**，强调**安全与协作** | 专业的独立开发者与小团队。重视工作流安全、代码质量和上下文理解。 | 封闭生态但有开放的权限和安全控制。近期社区重心在修复稳定性 Bug 和优化成本。 |
| **OpenAI Codex** | **模型能力驱动**，快速集成前沿模型 | 追求最新模型能力的早期采用者和探索者。对性能和多智能体架构有较高要求。 | 开放生态（多模型支持），但由 OpenAI 主导核心架构。迭代速度快，但 Bug 也多。 |
| **Gemini CLI** | **代理 (Agent) 任务编排** | 希望利用 AI Agent 处理复杂、多步骤自动化任务的开发者，尤其是Google生态用户。 | 强调整合Google模型 (Gemini) 和 Agent 框架。安全修复积极，但核心代理稳定性仍是短板。 |
| **Copilot CLI** | **GitHub 生态深度集成**的“副驾驶” | 深度使用 GitHub 生态，尤其是需要 PR review、Git 命令、代码搜索的团队。 | 与 GitHub 功能深度绑定，功能创新相对保守。社区需求偏向于配置灵活性和企业集成。 |
| **Kimi Code CLI** | **“小而美”的降本方案**，注重兼容性 | 希望从高价工具（如Claude Code）迁移的用户，以及关注成本和简洁性的开发者。 | 走“兼容并包”路线，通过支持 `CLAUDE.md` 降低迁移门槛。社区规模小但需求明确。 |
| **OpenCode** | **开源社区驱动的“瑞士军刀”** | 追求极致定制化和高度可控的开源爱好者，喜欢折腾TUI的开发者。 | 开源社区驱动，迭代极快，社区参与度高。V2 版本是当前主旋律，但稳定性问题也主要围绕V2。 |
| **Qwen Code** | **阿里系模型** (Qwen) 的旗舰 CLI，强在**本地化**与**多工作区** | 中文开发者社区，尤其是阿里云生态用户。关注多工作区管理、IDE集成和本地性能。 | 技术路线激进，功能更新密集。虽然问题不少，但修复速度也快。安全相关问题曝光率上升。 |

### 5. 社区热度与成熟度

-   **社区最活跃/讨论热度最高：** **OpenAI Codex** 和 **Claude Code**。两者均拥有庞大的用户基数和高度的社区参与度，但高质量的讨论被大量同质化的 Bug 报告所淹没。
-   **处于快速迭代/追赶阶段：** **OpenCode** 和 **Qwen Code**。这两个工具功能更新最为密集，几乎每天都有多个 PR 合入或新版本发布。社区活跃度高，但仍在处理大量早期采用者遇到的稳定性问题。OpenCode 的 V2 版本是其当前焦点。
-   **社区稳定/成熟度相对较高：** **GitHub Copilot CLI**。其功能迭代周期更长，社区讨论更偏向于“锦上添花”的功能请求，而非“救火”式的 Bug 报告。这表明其核心功能已相对稳定。
-   **社区规模较小，但定位清晰：** **Kimi Code CLI** 和 **Gemini CLI**。Kimi Code 通过兼容性策略吸引特定用户群，而 Gemini CLI 则专注于 Agent 领域，但都尚未形成大规模的热议。

### 6. 值得关注的趋势信号

对于开发者和技术决策者来说，以下趋势信号值得高度关注：

1.  **“成本可视化”将成为必备功能，而非增值功能：** “看不见的账单”是几乎所有头部工具社区的头号公敌。能够提供实时、透明且可控的 Token 消耗查询及防失控熔断机制，将是赢得开发者的关键。
2.  **“Agent 管理”是下一个战场：** 随着 AI Agent 能力增强，如何**优雅地启动、停止、监控和调试 Agent** 成为核心痛点。谁能最先解决“Agent 失控”和“子任务管理”问题，谁就能在高级开发者心中占据高地。
3.  **“供应链安全”不再只是口号：** Gemini CLI 和 Qwen Code 的 PR/Issue 表明，社区对 CI/CD 管道中的 “零点击 RCE” 和 “凭证泄漏” 风险极度敏感。这意味着 AI 编码工具本身也成为攻击面，其安全设计将直接影响企业客户的采纳决策。
4.  **“功能趋同”已成定局，“生态互操作性”决定迁移成本：** 当所有工具都能完成基本的编码任务时，工具间的迁移成本将成为用户留存的关键。Kimi Code 主动支持 `CLAUDE.md` 文件，就是一个降低竞争对手用户迁移门槛的聪明策略。
5.  **“回归 Bug”正在侵蚀用户信任：** 无论是 OpenAI Codex 的 `code-mode-host` 缺失，还是 OpenCode 的复制功能反复故障，都表明在追求快速迭代的过程中，基础稳定性正在付出代价。开发者对“功能发布后需要修复两个紧急补丁”的模式已经感到厌倦。

**结论：** 2026 年的 AI CLI 工具市场已进入“下半场”。比拼的不再是谁的功能更多，而是 **谁更稳定、谁更可控、谁更安全、谁的成本更透明**。对于开发者而言，选择一个工具需综合考量其迭代质量（而非速度）及其解决问题的能力，而非单纯追求最新模型或最炫功能。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，遵照您的指示，以下是为您生成的 Claude Code Skills 社区热点报告（数据截止 2026-07-10）。

***

## Claude Code Skills 生态热点报告 (2026-07-10)

### 1. 热门 Skills 排行

以下是根据 PR 评论活跃度与社区关注度筛选出的热门 Skills/修复，反映了当前社区的核心关注点。

1.  **`skill-creator` 修复与改进 (多 PR 联合)**
    *   **功能**: `skill-creator` 是官方提供的用于创建、评估和优化 Skills 的元技能。多个热门 PR (#1298, #1099, #1050, #362, #1261, #1323) 集中修复其核心评估脚本 `run_eval.py` 的缺陷。
    *   **讨论热点**: **零召回率 (0% recall) 问题**是所有讨论的核心。大量社区成员报告 `run_eval.py` 无法正确检测技能是否被触发，导致优化循环失效。此外，还有严重的 **Windows 兼容性问题**（子进程调用、编码、管道读取）和 **YAML 解析问题**。
    *   **状态**: 大多为 `OPEN`。该问题是社区最大痛点，多个 PR 从不同角度尝试修复。
    *   **链接**: [#1298](https://github.com/anthropics/skills/pull/1298), [#1099](https://github.com/anthropics/skills/pull/1099), [#1050](https://github.com/anthropics/skills/pull/1050), [#362](https://github.com/anthropics/skills/pull/362), [#1261](https://github.com/anthropics/skills/pull/1261), [#1323](https://github.com/anthropics/skills/pull/1323)

2.  **`document-typography` (文档排版技能)**
    *   **功能**: 对 Claude 生成的文档进行排版质量控制，修复孤字、寡行（标题在页面底部）、编号错位等常见问题。
    *   **讨论热点**: 这是一个直接从用户痛点出发的需求：**Al生成内容的质量细节**。评论关注该技能如何量化排版规则，以及如何在不干扰内容创造的前提下实现自动化纠错。
    *   **状态**: `OPEN`，讨论度极高，待合并。
    *   **链接**: [#514](https://github.com/anthropics/skills/pull/514)

3.  **`color-expert` (颜色专家技能)**
    *   **功能**: 一个全面的颜色专业知识库，涵盖 ISCC-NBS、Munsell、CSS 等多种色彩命名系统，以及 OKLCH、OKLAB 等色彩空间的使用指南。
    *   **讨论热点**: 社区对 **专业领域知识注入** 表现出浓厚兴趣。该技能试图解决 Claude 在色彩选择和描述上不够精确的问题，特别是对设计师和前端开发者有很高价值。
    *   **状态**: `OPEN`，内容新颖，受到关注。
    *   **链接**: [#1302](https://github.com/anthropics/skills/pull/1302)

4.  **`testing-patterns` (测试模式技能)**
    *   **功能**: 提供一个全面的测试指南，涵盖单元测试、组件测试、端到端测试，并具体到 React Testing Library、Vitest 等框架的最佳实践。
    *   **讨论热点**: 这是**软件工程工作流自动化**的典型需求。社区关注如何让技能指令足够具体、可执行，以便 Claude 生成符合团队规范的测试代码，而不是泛泛而谈。
    *   **状态**: `OPEN`，讨论度高，是工程化方向的热门候选。
    *   **链接**: [#723](https://github.com/anthropics/skills/pull/723)

5.  **`self-audit` (自我审计技能)**
    *   **功能**: 在 Claude 交付最终输出前，自动进行审计。包含“机械性文件验证”（确认文件存在）和“四维推理质量审计”（按严重性排序检查逻辑错误）。
    *   **讨论热点**: 这是一个高阶的“**元技能**”，即让 AI 检查 AI 的输出。社区热议其作为“质量门禁”的潜力，以及其优先级排序（damage-severity order）的合理性。
    *   **状态**: `OPEN`，概念新颖，代表了技能从“执行”向“治理”演进的趋势。
    *   **链接**: [#1367](https://github.com/anthropics/skills/pull/1367)

6.  **`frontend-design` (前端设计技能改进)**
    *   **功能**: 对原有的前端设计技能进行修订，使其指令更清晰、更具可操作性，确保 Claude 能在单次对话中有效遵循。
    *   **讨论热点**: 讨论集中在 **Skill 的内部一致性与指令质量** 上。社区认为“清晰的指令”比“包罗万象的内容”更重要，这反映了用户对技能标准化和可靠性的追求。
    *   **状态**: `OPEN`，体现了社区对现有技能进行深度打磨的期望。
    *   **链接**: [#210](https://github.com/anthropics/skills/pull/210)

7.  **`meta-skills` (技能质量与安全分析器)**
    *   **功能**: 向市场添加两个元技能：`skill-quality-analyzer`（从五个维度分析技能质量）和 `skill-security-analyzer`（分析技能安全风险）。
    *   **讨论热点**: 这是对 **技能生态治理** 的探索。社区讨论如何量化一个“好”的技能，以及如何防范恶意或有风险的技能，呼应了 #492 号 Issue 的安全关切。
    *   **状态**: `OPEN`，是社区自下而上推动生态健康发展的标志性PR。
    *   **链接**: [#83](https://github.com/anthropics/skills/pull/83)

---

### 2. 社区需求趋势

从 Issues 中可以提炼出以下几个关键需求趋势：

1.  **生态安全与治理潮**: 这是最突出的需求。Issue #492 (34 条评论) 强烈呼吁解决社区 Skill 在 Anthropic 官方命名空间下分发导致的“信任边界滥用”问题。社区迫切需要官方建立**技能审核、签名和命名空间管理机制**，以区分官方与社区贡献，保障用户安全。

2.  **组织级协作与分发**: Issue #228 代表了企业用户的呼声：**需要一个中心化的技能库或分享链接**，以便于团队内部共享技能，而不是通过文件传输和手动安装的繁琐流程。这是 Skills 从“个人工具”走向“团队资产”的关键一步。

3.  **核心工具的稳定与跨平台**: `skill-creator` 的 Bug 报告（#556, #1169, #1061）获得了大量关注。社区的核心诉求是官方尽快修复 `run_eval.py` 的**零召回率 Bug** 以及 **Windows 兼容性问题**。这直接影响了用户创建和优化自定义技能的能力。

4.  **特定领域技能的深化**: 社区对“专家级”技能有明确需求。例如 Issue #1329 提出的 `compact-memory`（紧凑记忆），旨在解决长期运行 Agent 的上下文膨胀问题；#412 提出的 `agent-governance`（代理治理），关注 AI Agent 系统的安全模式。这表明社区需求正从通用任务向**高价值的专业化场景**演进。

---

### 3. 高潜力待合并 Skills

以下 PR 尚未合并，但因其功能性、讨论热度和社区价值，具有很高的落地潜力：

*   **[#514: Add document-typography skill](https://github.com/anthropics/skills/pull/514)**：直接解决 Al 生成文档的排版痛点，普适性强，落地价值高。
*   **[#1367: feat(skills): add self-audit](https://github.com/anthropics/skills/pull/1367)**：代表 Al 输出“质量门禁”的新方向，概念先进，对生产级应用至关重要。
*   **[#723: feat: add testing-patterns skill](https://github.com/anthropics/skills/pull/723)**：满足开发者对工程化自动化的核心需求，如果能成功合并，将极大提升测试编写效率。
*   **[#1302: Add color-expert skill](https://github.com/anthropics/skills/pull/1302)**：填补了特定设计领域的知识空白，对设计师和前端社区吸引力巨大。
*   **[#83: Add skill-quality-analyzer and skill-security-analyzer](https://github.com/anthropics/skills/pull/83)**：作为“元技能”，它们是构建健康、可信赖的 Skill 生态的基础设施，长远意义重大。

---

### 4. Skills 生态洞察

当前社区最集中的诉求是：**修复核心工具 (skill-creator) 的严重缺陷并建立可信赖的生态治理框架（安全、共享、质量），以此为基础，再向专业化和工程化的工作流方向深入发展。** 社区的热情已从“如何创建技能”转向“如何创建高质量、可信和可靠的技能”。

---

好的，作为专精 AI 开发工具的技术分析师，我已根据您提供的 GitHub 数据，为您整理出 2026 年 7 月 10 日的 Claude Code 社区动态日报。

---

## 2026-07-10 Claude Code 社区动态日报

### 今日速览

昨日社区议题活跃度依然较高，多个关于 **Token 消耗异常**和 **权限系统** 的长期 Bug 讨论热度不减。同时，一个关于 **Cowork 功能在 Windows 平台** 上无法挂载项目文件夹的新 Bug 被迅速报告。值得关注的是，社区贡献者提交了多个针对 **插件事例与 CI 检测** 的文档与代码修复 PR，体现了社区对提升工具易用性的积极参与。

### 社区热点 Issues

1.  **Bash 复合命令权限解析** (`#16561`)
    -   **重要性**: **高**。社区长期关注的核心权限问题。当前权限系统将 `&&`、`||` 等复合命令视作整体匹配，导致即使所有子命令都有权限，仍需频繁审批。该 Issue 获得 173 个 👍 和 46 条评论，表明这是开发者工作流中的主要痛点。
    -   **社区反应**: 普遍支持该增强，认为其能显著减少不必要的权限审批干扰。
    -   **链接**: [https://github.com/anthropics/claude-code/issues/16561](https://github.com/anthropics/claude-code/issues/16561)

2.  **Cowork 功能无法添加私有 GitHub Marketplace** (`#28125`)
    -   **重要性**: **高**。33 条评论，说明在团队协作场景中，对私有插件和工具的支持是刚需。该问题可能阻碍企业级用户广泛采用 Cowork 功能。
    -   **社区反应**: 用户积极提供排查信息，期待官方解决。
    -   **链接**: [https://github.com/anthropics/claude-code/issues/28125](https://github.com/anthropics/claude-code/issues/28125)

3.  **Fable 5 Token 消耗不符预期** (`#67506`)
    -   **重要性**: **高**。22 条评论，直接关系到用户的核心成本。用户发现新模型的实际 Token 消耗远超其宣称的性价比，引发了关于模型计费透明度的讨论。
    -   **社区反应**: 用户分享了各自的消耗数据，普遍表达了困惑与不满，等待 Anthropic 官方澄清。
    -   **链接**: [https://github.com/anthropics/claude-code/issues/67506](https://github.com/anthropics/claude-code/issues/67506)

4.  **Opus 4.7/4.8 Token 使用回归 & 频繁断连** (`#64961`)
    -   **重要性**: **高**。另一个与模型消耗和稳定性相关的高关注度问题。用户反馈更新后，Token 消耗增加了 2-3 倍，且 Opus 4.8 频繁断开连接，严重影响使用体验。
    -   **社区反应**: 多家用户表示遇到类似问题，要求回滚或紧急修复。
    -   **链接**: [https://github.com/anthropics/claude-code/issues/64961](https://github.com/anthropics/claude-code/issues/64961)

5.  **Linux 平台下 `claude agents` 守护进程周期性重生** (`#68146`)
    -   **重要性**: **中**。虽然评论数不多 (8条)，但描述的问题非常具体且严重：在 Linux (特别是 Docker 环境) 下，打开 `claude agents` 视图会导致后台守护进程每 ~52 秒重启一次，导致所有 MCP 连接和 claude.ai 桥接中断。
    -   **社区反应**: 问题描述清晰，是 Linux 环境下的一个严重稳定性 Bug。
    -   **链接**: [https://github.com/anthropics/claude-code/issues/68146](https://github.com/anthropics/claude-code/issues/68146)

6.  **Cowork (Windows) 项目上下文文件夹无法挂载** (`#76187`)
    -   **重要性**: **高**。昨日新提交的 Issue，影响范围可能很大。报告指出在 Windows 上，Cowork 功能无法在新会话中挂载项目文件夹，且添加文件夹的对话框无法确认。
    -   **社区反应**: 少数用户已复现，指出为回归问题，期待快速修复。
    -   **链接**: [https://github.com/anthropics/claude-code/issues/76187](https://github.com/anthropics/claude-code/issues/76187)

7.  **Mac Pro 计划异常 Token 消耗** (`#65406`, `#57278`)
    -   **重要性**: **高**。多起关于“无限”或“异常”Token 消耗的报告被标记为重复。`#57278` 描述了一场失控的会话消耗了整周限额，`#65406` 则报告了付费计划在故障后持续的异常消耗，引发用户对账单保护的担忧。
    -   **社区反应**: 用户焦虑，希望官方提供更健壮的防止 Token 失控的熔断机制。
    -   **链接**: [https://github.com/anthropics/claude-code/issues/65406](https://github.com/anthropics/claude-code/issues/65406) | [https://github.com/anthropics/claude-code/issues/57278](https://github.com/anthropics/claude-code/issues/57278)

8.  **无法取消/停止已派生的 Agent 团队** (`#34476`)
    -   **重要性**: **中**。此功能需求体现了 Agent 工作流中“控制权”的缺失。用户一旦派生了多个并行的 sub-agent，就无法停止它们，只能结束整个 Session，这对资源控制和任务管理是显著的短板。
    -   **社区反应**: 用户表达了对此功能的强烈渴望，希望能在不丢失主会话上下文的情况下管理子任务。
    -   **链接**: [https://github.com/anthropics/claude-code/issues/34476](https://github.com/anthropics/claude-code/issues/34476)

9.  **Daemon 控制 Socket 绑定竞争导致崩溃 (2.1.195 回归)** (`#72334`)
    -   **重要性**: **中**。社区功能: 该 Bug 由 Claude Code 自身通过日志分析发现和定位。描述了一个在负载下启动多个实例时，守护进程因端口绑定冲突 (EADDRINUSE) 而直接退出，属于典型的回归问题。
    -   **社区反应**: 展示了 AI 工具辅助自身 Debug 的有趣案例。
    -   **链接**: [https://github.com/anthropics/claude-code/issues/72334](https://github.com/anthropics/claude-code/issues/72334)

10. **Intel Mac 在高负载下内核崩溃** (`#74805`)
    -   **重要性**: **低** (平台特定)。但属于严重影响系统稳定性的 Bug。报告指出在 Intel Mac 上大量使用 Claude Code CLI 时，会触发 WindowServer 看门狗超时，导致内核崩溃。
    -   **社区反应**: 用户提供了详细的诊断信息，问题可能指向 GPU 资源竞争。
    -   **链接**: [https://github.com/anthropics/claude-code/issues/74805](https://github.com/anthropics/claude-code/issues/74805)

### 重要 PR 进展

1.  **docs(plugin-dev): 使用扁平格式编写 .mcp.json 示例** (`#76029`)
    -   **摘要**: 修正了插件开发文档中的示例代码，将 `.mcp.json` 文件从嵌套的 `mcpServers` 对象改为正确的扁平格式，避免了初学者的困惑。
    -   **链接**: [https://github.com/anthropics/claude-code/pull/76029](https://github.com/anthropics/claude-code/pull/76029)

2.  **docs(plugin-dev): 修复 README 中的市场名称** (`#76028`)
    -   **摘要**: 修复了插件开发 README 中错误的安装命令，将 `plugin-dev@claude-code-marketplace` 修正为与其他插件文档一致的 `@anthropic/claude-code-plugin-dev`，解决了安装失败问题。
    -   **链接**: [https://github.com/anthropics/claude-code/pull/76028](https://github.com/anthropics/claude-code/pull/76028)

3.  **fix: 在 load-context 示例中使用目录测试检测 GitHub Actions CI** (`#76023`)
    -   **摘要**: 修复了 SessionStart Hook 示例中的逻辑错误。原有的 CI 检测使用 `-f` (文件) 测试 `.github/workflows` 目录，导致永远无法检测成功。现已修正为 `-d` (目录)。
    -   **链接**: [https://github.com/anthropics/claude-code/pull/76023](https://github.com/anthropics/claude-code/pull/76023)

4.  **fix(sweep): 通过 Search API 修复 markStale 脚本** (`#75938`)
    -   **摘要**: 修复了自动化清理脚本 (markStale) 的一个严重 Bug。该脚本由于直接从 Issues 列表中遍历，且“跳过”项会永久占用列表位置，导致无法有效标记旧 Issue。
    -   **链接**: [https://github.com/anthropics/claude-code/pull/75938](https://github.com/anthropics/claude-code/pull/75938)

### 功能需求趋势

从近期 Issue 分析，社区对 Claude Code 的关注方向高度聚焦：

1.  **成本与 Token 管理**：这是最核心的痛点。用户强烈要求更透明、可控的 Token 消耗机制，包括：
    -   **模型消耗与描述不符**: 期望模型实际表现与定价/描述一致。
    -   **防失控熔断**: 需要更可靠的机制，防止异常 Session 或自动化 Agent 无限消耗配额。
    -   **上下文压缩**: 请求优化长会话的上下文管理，避免因 Session 膨胀被迫使用昂贵的 1M 上下文计费。
2.  **精细化权限与安全控制**：开发者希望工作流更流畅，减少不必要的干扰：
    -   **复合命令匹配**: 解析 `&&`, `|` 等复合命令，使其子组件可以单独匹配权限。
    -   **自定义权限模式**: 允许用户更精细地定义允许/拒绝的规则。
3.  **Agent 与协作控制**：随着 AI Agent 能力增强，控制权成为焦点：
    -   **任务取消**: 能够优雅地停止正在运行的 sub-agent/Spawned Agent。
    -   **上下文隔离**: sub-agent 在多项目工作时应能正确创建独立的工作空间。
4.  **跨平台稳定性**：特别是 **Linux** (Docker 环境) 和 **Windows** 的稳定性问题报告增多，主要集中在对平台特性的适配 (如文件路径、网络配置) 上。
5.  **更好的 TUI/UI 体验**：包括可滚动的长文本预览、清晰的屏幕清除 (不影响上下文)、更直观的权限审批界面等。

### 开发者关注点

综合来看，近期开发者反馈中的主要痛点和高频需求包括：

-   **“看不见的账单”**：对 Token 消耗的不透明性和意外超支的抱怨最多。开发者希望能有实时消耗统计、预测和硬性上限设置。
-   **“失控的 Agent”**：无法在不中断主会话的情况下停止或管理由 Claude Code 派生的子 Agent，导致资源浪费和工作流混乱。
-   **“破碎的复合命令”**：权限系统对 `&&`、`||` 等常用 Bash 习语的“一刀切”处理，打断了开发者的心流。
-   **“回归的焦虑”**：用户对更新后出现的回归问题 (如 Daemon 崩溃、Windows Cowork 损坏) 感到沮丧，期望更严格的回归测试。
-   **“被遗忘的 MCP 连接”**：在 Linux 环境下，守护进程的周期性重启导致 MCP 服务器连接频繁断开和重建，严重影响依赖外部工具的开发者。

**结论**：当前社区对 Claude Code 的期望已经从“能用”转向了“稳定、可控、透明”。开发者愿意为强大的 AI 能力付费，但前提是成本可预测、工作流可控、工具稳定可靠。Anthropic 若能在 **成本可视化**、**Agent 控制权** 和 **跨平台稳定性** 上重点发力，将有效提升用户满意度和忠诚度。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

好的，作为专注于AI开发工具的技术分析师，我将根据您提供的GitHub数据，为您生成2026年7月10日的OpenAI Codex社区动态日报。

---

## OpenAI Codex 社区动态日报 | 2026-07-10

### 今日速览

今日Codex社区的核心动态围绕**v0.144.0/v0.144.1版本的快速迭代**展开。一方面，`v0.144.0`引入了广受期待的“写入权限确认模式”和信用额度重置选择功能，但同时也引入了`codex-code-mode-host`缺失的严重Bug，导致CLI用户无法使用；另一方面，**GPT-5.5模型的推理令牌聚类问题** (#30364) 成为社区讨论的绝对热点，已有176条评论和279个点赞，开发者普遍认为这是导致复杂任务性能下降的关键因素。

---

### 版本发布

当前主要版本为 `v0.144.1`，紧随其后的 `v0.144.0` 和 `v0.145.0-alpha.1` 也已发布。

*   **`rust-v0.144.1` (最新补丁版本)**
    *   **链接**: `https://github.com/openai/codex/releases/tag/rust-v0.144.1`
    *   **内容**: 这是一个针对`v0.144.0`的紧急修复版本。
        *   修复了当GitHub返回压缩或重排序的release元数据时，**独立安装失败**的问题。
        *   确保macOS软件包安装时，**`codex`可执行文件与`codex-code-mode-host`同时存在**。
        *   在后端二进制文件不可用时，通过回退机制保持代码模式正常工作。

*   **`rust-v0.144.0` (最新功能版本)**
    *   **链接**: `https://github.com/openai/codex/releases/tag/rust-v0.144.0`
    *   **内容**: 引入了两个关键功能：
        *   **信用额度重置**: 重置信用额度时，现在会显示其类型和到期时间，并允许开发者选择使用哪个信用额度进行重置。
        *   **`writes`应用审批模式**: 新增一种审批模式，该模式允许声明为只读的操作自动执行，但会在涉及写入操作时向用户**弹出确认提示**，极大提升了安全性。
        *   此外，MCP工具现在可以**请求交互式身份验证**。

*   **`rust-v0.145.0-alpha.1` (预览版)**
    *   **链接**: `https://github.com/openai/codex/releases/tag/rust-v0.145.0-alpha.1`
    *   **内容**: 下一个版本的早期预览，包含为社区体验新功能。

---

### 社区热点 Issues (Top 10)

1.  **GPT-5.5 推理令牌聚类问题** `#30364`
    *   **链接**: `https://github.com/openai/codex/issues/30364`
    *   **重要性**: **社区最关注的问题**。开发者发现`gpt-5.5`模型的推理输出令牌数量高度集中在`516/1034/1552`等固定边界，这被认为与模型在复杂任务上的性能下降有关。这暗示了模型推理策略可能存在问题。

2.  **CLI版 code-mode-host 缺失** `#31831`
    *   **链接**: `https://github.com/openai/codex/issues/31831`
    *   **重要性**: **v0.144.0的致命Bug**。更新后，Codex CLI无法启动，报错“codex-code-mode-host”缺失。该问题在发布后迅速被社区反馈，并在`v0.144.1`中得到部分解决，但影响广泛，评论和点赞数激增。

3.  **Windows桌面版频繁卡顿/冻结** `#20214`
    *   **链接**: `https://github.com/openai/codex/issues/20214`
    *   **重要性**: **长期存在的Windows性能痛点**。即使在用户拥有足够系统资源（32GB RAM）的情况下，应用仍会频繁冻结。此问题已持续数月，是Windows用户最希望解决的Bug之一。

4.  **Windows桌面版导致系统输入延迟** `#28855`
    *   **链接**: `https://github.com/openai/codex/issues/28855`
    *   **重要性**: 另一个严重的Windows性能问题。打开Codex桌面版会导致整个系统的鼠标和键盘输入出现间歇性延迟，严重影响用户体验。

5.  **`gpt-5.6-sol` 新模型的多智能体路由隐藏问题** `#31814`
    *   **链接**: `https://github.com/openai/codex/issues/31814`
    *   **重要性**: **新模型引入的配置冲突**。`gpt-5.6 Sol`模型会自动激活新的多智能体架构V2，但该架构默认隐藏了子代理路由的控制面板，导致开发者无法精确控制子代理行为，引发了对新版本控制权的担忧。

6.  **Azure 用户使用新模型时出现HTTP 400错误** `#31882`
    *   **链接**: `https://github.com/openai/codex/issues/31882`
    *   **重要性**: **企业级用户的核心痛点**。`gpt-5.6-sol/terra/luna`等新模型硬编码了一些特定设置，导致在Azure OpenAI等非ChatGPT后端上使用时请求失败（返回400错误），这直接影响了企业用户的使用。

7.  **MCP服务器进程泄漏问题** `#30408`
    *   **链接**: `https://github.com/openai/codex/issues/30408`
    *   **重要性**: **资源消耗的严重Bug**。每次新建对话线程都会生成新的MCP服务器进程，但当线程关闭或归档后进程未被清理，导致内存占用（RSS）飙升至9GB以上。对于长时间使用Codex Desktop的用户来说，这是不可持续的资源浪费。

8.  **信用额度重置失败导致额度消失** `#31601`
    *   **链接**: `https://github.com/openai/codex/issues/31601`
    *   **重要性**: **付费用户的信任危机**。用户尝试使用版本新增的信用额度重置功能，但重置操作失败，*原有额度也不翼而飞*。这对于Pro用户而言是一个极度敏感且严重的问题。

9.  **版本更新提示异常** `#31826`
    *   **链接**: `https://github.com/openai/codex/issues/31826`
    *   **重要性**: **用户体验Bug**。部分用户（如NVIDIA用户）遇到Codex持续提示需要更新到最新版本，但当前版本已是最新的情况。这会打断工作流程并造成困惑。

10. **GitHub自动代码审查静默失败** `#15477`
    *   **链接**: `https://github.com/openai/codex/issues/15477`
    *   **重要性**: **核心功能的信任问题**。Codex Cloud的自动代码审查功能出现静默失败：仪表盘显示仍有可用配额，但实际执行时却提示已达限制。这种不一致的行为会严重影响开发者在CI/CD流程中对Codex的信任。

---

### 重要 PR 进展 (Top 10)

1.  **修复 code-mode-host 安装问题** `#31890`
    *   **链接**: `https://github.com/openai/codex/pull/31890`
    *   **内容**: 这是一个**外部贡献者(非OpenAI)** 提交的重要PR，直接针对`v0.144.0`中`codex-code-mode-host`缺失的根本问题进行修复，旨在彻底解决CLI不可用的问题。

2.  **支持SQLite禁用降级模式** `#31509`
    *   **链接**: `https://github.com/openai/codex/pull/31509`
    *   **内容**: 恢复显式关闭SQLite本地状态数据库的支持。这对于在网络文件系统（NFS）等不稳定的文件存储上运行Codex至关重要，防止因数据库锁定或损坏导致的崩溃。

3.  **实现托管的Bedrock登出/登录API** `#31325` & `#31326` & `#31327`
    *   **链接**: `https://github.com/openai/codex/pull/31325`
    *   **链接**: `https://github.com/openai/codex/pull/31326`
    *   **链接**: `https://github.com/openai/codex/pull/31327`
    *   **内容**: 这是一套为Amazon Bedrock用户提供的认证管理功能。旨在让用户可以像管理Codex主认证一样，通过程序化管理在AWS上的API密钥登录和登出，简化了多云环境下的配置。

4.  **存储rollout记录的序号** `#31859` & **引入双向JSONL扫描器** `#31891`
    *   **链接**: `https://github.com/openai/codex/pull/31859`
    *   **链接**: `https://github.com/openai/codex/pull/31891`
    *   **内容**: 这是为了**优化大数据量会话的恢复和加载速度**。通过给分页记录添加序号并引入高效的双向扫描器，Codex可以更快地定位到所需的历史记录，而不是遍历整个文件。

5.  **展平协作模式状态 (1/5)** `#31734`
    *   **链接**: `https://github.com/openai/codex/pull/31734`
    *   **内容**: 作为重构系列的第一部分，旨在清理内部状态管理。将协议中的`CollaborationMode`对象展平，避免状态重复，为未来更复杂的步骤级（step-scoped）所有权变更打下基础。

6.  **将推理成本转移到步骤上下文 (5/5)** `#31737`
    *   **链接**: `https://github.com/openai/codex/pull/31737`
    *   **内容**: 完成状态管理重构的最后一步。将“推理成本”这个与单次请求紧密相关的属性，从持久的`TurnContext`移至更精确的`StepContext`中，使得成本追踪更准确。

7.  **缓存 `rg --files` 文件清单** `#31939`
    *   **链接**: `https://github.com/openai/codex/pull/31939`
    *   **内容**: **性能优化关键PR**。通过缓存文件搜索命令（`rg --files`）的结果，避免在大型仓库中重复扫描整个文件系统。报告称，在34GB的巨型仓库中，每次调用可节省约3.5秒，这对多智能体场景下的性能提升至关重要。

8.  **实现工作区根路径具体化** `#31892`
    *   **链接**: `https://github.com/openai/codex/pull/31892`
    *   **内容**: 修复了exec-server中的一个安全与功能缺陷。之前，象征性的`:workspace_roots`权限可能在设置沙箱策略时被错误地放宽，导致文件系统访问范围意外扩大。此PR通过“具体化”根路径来确保沙箱边界正确。

9.  **支持多个外部代理导入源** `#31945`
    *   **链接**: `https://github.com/openai/codex/pull/31945`
    *   **内容**: 增强Codex的**代理生态系统**。此PR引入适配器模式以支持从不同来源（如不同仓库、仓库）导入外部代理配置，并提供了TUI源选择器和兼容性迁移引导，将使社区代理的分享和复用变得更加方便。

10. **添加通用进程生命周期钩子** `#31852`
    *   **链接**: `https://github.com/openai/codex/pull/31852`
    *   **内容**: 通过添加进程（如插件脚本）的生成、取消和终端生命周期回调，为**插件系统的监控和遥测**奠定了基础。这使得将来可以跟踪插件脚本的执行状态，为开发者提供更深度的洞察。

---

### 功能需求趋势

从今日的Issues数据中，可以提炼出社区最关注的几个功能方向：

1.  **模型行为透明性与控制权**: 开发者不仅关注新模型的性能（如`gpt-5.6-sol`），更希望了解其内部行为（如推理令牌聚类 `#30364`）并拥有控制权（如多智能体V2路由 `#31814`）。**“黑盒”模型是不被接受的。**
2.  **企业级与多云集成**: 以Azure `#31882` 和Amazon Bedrock (`#31325`等) 为代表的非ChatGPT后端集成问题频发，表明企业级用户是重要群体，Codex需要提供更健壮、非侵入式的集成方案。
3.  **系统资源优化与性能**: Windows系统上的卡顿 (`#20214`)、输入延迟 (`#28855`) 和内存泄漏 (`#30408`) 是持续的高频痛点。开发者要求Codex在资源消耗上更克制，尤其是在长时间或复杂任务场景下。
4.  **信用额度与配额管理的可靠性**: 信用额度重置功能是`v0.144.0`的主打新功能，但相关的Bug (`#31601`, `#31532`) 直接触碰了付费用户的底线。**需要确保所有与付费相关的功能万无一失**。
5.  **插件与MCP生态成熟度**: MCP工具调用回归 (`#19871`) 和进程泄漏 (`#30408`) 揭示了MCP生态仍不稳定。同时，对外部代理导入源的支持 (`#31945`) 表明社区正在推动生态走向更开放和标准化的方向。

### 开发者关注点

高频痛点主要集中在新功能的“副作用”和核心稳定性上：

1.  **`v0.144.0`更新兼容性问题**: `code-mode-host` 缺失问题 (`#31831`, `#31906`) 是**本次更新最严重的倒退**，直接中断了CLI用户的使用，引发大量负面反馈。
2.  **新模型部署的“水土不服”**: 引入`gpt-5.6`系列模型时，硬编码的设置排除了Azure等大型客户 (`#31882`)，且其内部机制（如多智能体V2、推理令牌聚类）引发了控制权丧失和性能异常的担忧。
3.  **Windows平台的持续性低质量体验**: 应用冻结、系统输入延迟等基础体验问题长期未得到根本性解决，让Windows用户感觉自己是“二等公民”。
4.  **付费功能的信任危机**: 信用额度重置失败并导致额度丢失 (`#31601`) 是严重的产品事故，极大地损害了Pro用户对平台新功能的信任。
5.  **状态管理的不一致**: “数据库被锁” (`#31184`)、”回话状态丢失” (`#31074`) 以及”版本提示异常” (`#31826`) 等一系列问题，表明Codex的本地状态管理和服务器端状态同步仍存在许多边界情况未处理，影响了用户的持续使用体验。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 | 2026-07-10

## 📌 今日速览
社区本周聚焦代理稳定性和安全修复。**Subagent 误报成功**（#22323）和**Generalist agent 挂起**（#21409）仍是影响用户体验的核心 Bug；同时，**a2a-server 零点击 RCE 漏洞**（PR #28319）和**CI 供应链攻击面**（PR #28232）的修复被合并，安全防御力度显著提升。此外，Auto Memory 系统（#26522）和评估框架（PR #28344）的改进持续推进。

---

## 🔥 社区热点 Issues（Top 10）

### 1. Subagent 达到 MAX_TURNS 后误报为成功
- **#22323** `[priority/p1, kind/bug]`  
  `codebase_investigator` 子代理在达到最大轮次后，仍报告 `status: "success"` 和 `Termination Reason: "GOAL"`，隐藏了真正的中断原因，误导用户认为任务已完成。社区期望能区分“意外中断”和“正常达成目标”。  
  🔗 [https://github.com/google-gemini/gemini-cli/issues/22323](https://github.com/google-gemini/gemini-cli/issues/22323)

### 2. Generalist agent 挂起（hangs）
- **#21409** `[priority/p1, kind/bug]`  
  当 Gemini CLI 将任务委托给 Generalist agent 时，经常永久挂起（文件夹创建等简单操作也会挂起 1 小时以上）。用户通过禁止使用子代理可临时规避，开发团队正在添加超时和重试机制。  
  🔗 [https://github.com/google-gemini/gemini-cli/issues/21409](https://github.com/google-gemini/gemini-cli/issues/21409)

### 3. Shell 命令执行后卡在“Waiting input”
- **#25166** `[priority/p1, kind/bug]`  
  在简单 CLI 命令执行完成后，工具提示仍显示“Awaiting user input”，导致流程无法继续。此问题复现率极高，社区反馈 +3 个 👍。  
  🔗 [https://github.com/google-gemini/gemini-cli/issues/25166](https://github.com/google-gemini/gemini-cli/issues/25166)

### 4. Browser subagent 在 Wayland 下失败
- **#21983** `[priority/p1, kind/bug, agent/browser]`  
  Wayland 环境下，Browser agent 无法正常启动，最终显示 `Termination Reason: GOAL` 但并未完成预期操作。影响 Linux 用户对浏览器自动化的使用。  
  🔗 [https://github.com/google-gemini/gemini-cli/issues/21983](https://github.com/google-gemini/gemini-cli/issues/21983)

### 5. Gemini 不主动使用自定义 Skills 和 Sub-agents
- **#21968** `[priority/p2, kind/bug]`  
  即使定义了 Gradle、Git 等技能，Gemini 很少主动调用它们，仅在用户明确指示时才使用。社区期望模型能根据任务描述自动匹配已有技能，减少手动干预。  
  🔗 [https://github.com/google-gemini/gemini-cli/issues/21968](https://github.com/google-gemini/gemini-cli/issues/21968)

### 6. Auto Memory 对低信号会话无限重试
- **#26522** `[priority/p2, kind/bug]`  
  当提取代理判断某个会话“低信号”并跳过读取后，该会话仍保留在索引中，下次扫描会被再次发现，导致无限重试。社区建议增加“已忽略”标记或阈值。  
  🔗 [https://github.com/google-gemini/gemini-cli/issues/26522](https://github.com/google-gemini/gemini-cli/issues/26522)

### 7. 工具数量超过 128 时返回 400 错误
- **#24246** `[priority/p2, kind/bug]`  
  当启用工具数超过 400（或 128）时，Gemini CLI 返回 HTTP 400 错误。用户期望系统能自动限制或分页工具列表，而不是直接崩溃。  
  🔗 [https://github.com/google-gemini/gemini-cli/issues/24246](https://github.com/google-gemini/gemini-cli/issues/24246)

### 8. Symlink 格式的 Agent 文件不被识别
- **#20079** `[priority/p2, kind/bug]`  
  `~/.gemini/agents/` 目录下的符号链接不会被识别为子代理。用户希望支持符号链接，便于跨机器同步配置。  
  🔗 [https://github.com/google-gemini/gemini-cli/issues/20079](https://github.com/google-gemini/gemini-cli/issues/20079)

### 9. 组件级评估框架（EPIC）
- **#24353** `[priority/p1, kind/customer-issue]`  
  规划中的组件级行为评估，目标是让 76 个已有行为评估测试在 6 个 Gemini 模型上自动化运行，提升回归测试覆盖率。该项目已进入实施阶段。  
  🔗 [https://github.com/google-gemini/gemini-cli/issues/24353](https://github.com/google-gemini/gemini-cli/issues/24353)

### 10. 评估 AST 感知文件读取与搜索的价值
- **#22745** `[priority/p2, kind/feature]`  
  调查是否引入 AST 感知工具（如精确读取方法边界、减少 token 噪声、提升导航效率），预期能降低多轮交互中的误读次数。社区对减少 Token 消耗和提升准确率持积极态度。  
  🔗 [https://github.com/google-gemini/gemini-cli/issues/22745](https://github.com/google-gemini/gemini-cli/issues/22745)

---

## 🚧 重要 PR 进展（Top 10）

### 1. 修复 a2a-server 零点击 RCE 漏洞
- **#28319** `size/xl`  
  通过重构启动序列和环境加载机制，强制检查工作区信任，防止未受信任工作区引发远程代码执行。这是一个关键安全修复。  
  🔗 [https://github.com/google-gemini/gemini-cli/pull/28319](https://github.com/google-gemini/gemini-cli/pull/28319)

### 2. 修复任务取消后仍保持执行的问题
- **#28316** `size/l`  
  解决 Agent 模式下，任务取消后底层执行流未终止导致的“幽灵执行”问题，同时修复多个竞态条件和内存泄漏。  
  🔗 [https://github.com/google-gemini/gemini-cli/pull/28316](https://github.com/google-gemini/gemini-cli/pull/28316)

### 3. 修复 CI 供应链 RCE（Eval 工作流分拆）
- **#28232** `size/l`  
  将 `eval-pr.yml` 中的 `pull_request_target` 拆分为 `pull_request` + `workflow_run`，避免 fork 代码在具备 API Key 的环境下执行。  
  🔗 [https://github.com/google-gemini/gemini-cli/pull/28232](https://github.com/google-gemini/gemini-cli/pull/28232)

### 4. 添加 `eval:validate` 静态分析命令
- **#28344** `size/xl`  
  新增 CLI 命令，可静态检查 eval 源文件是否符合 9 条规则，并以退出码 1 标记违反项，便于集成到 CI 中做门禁。  
  🔗 [https://github.com/google-gemini/gemini-cli/pull/28344](https://github.com/google-gemini/gemini-cli/pull/28344)

### 5. 限制单次用户请求的递归推理轮数
- **#28164** `size/m`  
  实现硬性限制（默认 15 轮），防止无限循环耗尽本地 CPU 和模型配额。可自定义配置。  
  🔗 [https://github.com/google-gemini/gemini-cli/pull/28164](https://github.com/google-gemini/gemini-cli/pull/28164)

### 6. 修复 `resolveToRealPath` 对含 `%` 文件名的破坏
- **#28327** `size/s`  
  之前无条件执行 `decodeURIComponent`，导致 `report%202026.txt` 被错误解码为 `report 2026.txt`。现在仅对 `file://` URL 进行解码。  
  🔗 [https://github.com/google-gemini/gemini-cli/pull/28327](https://github.com/google-gemini/gemini-cli/pull/28327)

### 7. 修复 `isAuthenticationError` 误判 401 子串
- **#28328** `size/s`  
  之前任何包含 `401` 子串（如 URL 端口 4012、错误行号 401）都被误认为认证错误，触发不必要的 OAuth 回退流程。  
  🔗 [https://github.com/google-gemini/gemini-cli/pull/28328](https://github.com/google-gemini/gemini-cli/pull/28328)

### 8. 修复 JSON / IPYNB 文件写入与替换时损坏
- **#28223** `size/m`（已合并）  
  `write_file` 和 `replace` 工具在处理 `.json` 和 `.ipynb` 文件时，因 LLM 自动纠正导致内容损坏。本 PR 对这两种文件类型跳过 LLM 修正，保持原始内容完整性。  
  🔗 [https://github.com/google-gemini/gemini-cli/pull/28223](https://github.com/google-gemini/gemini-cli/pull/28223)

### 9. 修复 `/privacy` 显示原始后端错误消息
- **#28304** `size/l`  
  企业/工作区账号执行 `/privacy` 时，原本显示“User does not have a current tier”等原始消息，现改为用户友好的提示。  
  🔗 [https://github.com/google-gemini/gemini-cli/pull/28304](https://github.com/google-gemini/gemini-cli/pull/28304)

### 10. 实现代理初始化停滞检测与引导恢复
- **#28331** `size/m`  
  引入“停滞断路器”（Stagnation Circuit Breaker），当模型在 `/rewind` 或纯文字响应后未产生工具调用时，自动触发引导恢复机制，避免流程过早终止。  
  🔗 [https://github.com/google-gemini/gemini-cli/pull/28331](https://github.com/google-gemini/gemini-cli/pull/28331)

---

## 📈 功能需求趋势

1. **Agent 行为可预测性**：社区强烈希望 Gemini 能更智能地使用自定义技能和子代理（#21968），并能意识到自身能力边界（如精确的 CLI 标志、热键、自我执行）（#21432）。  
2. **Memory 系统完善**：Auto Memory 一直是开发焦点，包括避免低信号会话循环（#26522）、确定性脱敏（#26525）、无效补丁隔离（#26523）以及质量改进（#26516）。  
3. **AST 感知工具**：多个 Issue 提出利用抽象语法树来提升文件读取、搜索和代码库映射的精确度（#22745、#22746），以减少 Token 消耗和交互轮次。  
4. **评估框架标准化**：从“组件级评估”（#24353）到静态验证工具（PR #28344），社区在推动可靠、可复现的回归测试体系。  
5. **安全与权限细粒度控制**：包括工作区信任（PR #28319）、TOCTOU 漏洞修复（PR #28330）、CI 供应链保护（PR #28232）以及避免破坏性命令（#22672）等。  

---

## 🔧 开发者关注点（痛点/高频需求）

- **误导性成功报告**：子代理即使被中断也报告“GOAL 成功”，容易掩盖真实故障（#22323）。  
- **挂起与死锁**：Generalist agent 和 Shell 命令执行后卡死是最常见的用户反馈（#21409、#25166）。  
- **环境兼容性**：Wayland 下 Browser agent 无法使用（#21983）；终端 resize 时闪烁（#21924）。  
- **配置灵活性不足**：`settings.json` 中的配置（如 `maxTurns`）被 Browser agent 忽略（#22267）；符号链接不被识别（#20079）。  
- **工具数量限制**：超过 128/400 个工具时直接 400 错误（#24246），期望动态过滤或分组。  
- **调试信息缺失**：`/bug` 报告不包含子代理上下文（#21763），子代理轨迹无法通过 `/chat share` 共享（#22598）。  
- **非授权行为**：v0.33.0 后子代理在配置禁用后仍被调用（#22093），令用户感到意外。  

--- 

> **报选题、反馈或投稿请联系编辑部**。  
> 数据来源：GitHub `

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-07-10

## 今日速览

- **v1.0.70-0 发布**：新增插件 SHA 锁定、沙箱会话开关以及 `/refine` 重写指令。
- **终端 TUI 挂死 Bug（#4069）** 引发社区关注，WSL2 + Windows Terminal 下会话中途清屏、输入失效，且 Ctrl+C 无法脱出。
- **社区持续呼吁模型家族别名、项目级插件作用域及可配置系统提示**，多项高赞功能需求仍在积极推进。

---

## 版本发布

**v1.0.70-0** — 2026-07-09 发布  
更新内容（**Added**）：
- 插件源配置支持通过 `sha` 字段将插件固定到精确的 commit SHA。
- 新增 `--sandbox` / `--no-sandbox` 标志，允许在当前会话中临时开启或关闭 OS 级 shell 沙箱，无需修改已保存的沙箱设置（可与 `-p` 配合使用）。
- 新增 `/refine` 指令，用于重写已有输出。

---

## 社区热点 Issues（10 条）

### 1. #1595 [OPEN] 企业策略间歇性封锁模型列表
- **描述**：企业 Copilot 账户显示剩余 premium 请求约 40%，但 `/models` 命令始终报 “access denied by Copilot policy”，怀疑是策略缓存或权限判定 bug。
- **热度**：👍 10 | 💬 28 | 创建于 2026-02-21  
- **链接**：https://github.com/github/copilot-cli/issues/1595

### 2. #1665 [CLOSED] 支持项目/仓库级插件作用域
- **描述**：当前插件全局安装，用户无法为不同项目启用不同的插件集。大量团队希望插件能按项目或仓库自动切换。
- **热度**：👍 18 | 💬 13 | 已关闭（官方或已采纳）  
- **链接**：https://github.com/github/copilot-cli/issues/1665

### 3. #970 [OPEN] macOS Gatekeeper 阻拦 Copilot CLI（企业安全策略）
- **描述**：每次通过 HomeBrew 升级后，macOS 都会弹出“无法验证恶意软件”警告，用户需手动前往隐私与安全设置放行，严重影响自动化部署体验。
- **热度**：👍 21 | 💬 7 | 创建于 2026-01-14  
- **链接**：https://github.com/github/copilot-cli/issues/970

### 4. #4069 [OPEN] TUI 中途挂死 — 屏幕清空、输入失效（WSL2 + Windows Terminal）
- **描述**：v1.0.70-0 上使用 `claude-opus-4.7` 时，会话进行中突然清屏，输入区域无响应，Ctrl+C 和 Ctrl+\ 均无效。日志显示 stdout 发生 EIO 错误，Rust JSON-RPC 传输层触发 EPIPE。该 bug 影响大量 WSL 用户。
- **热度**：👍 7 | 💬 6 | 创建于 2026-07-09（最新严重 Bug）  
- **链接**：https://github.com/github/copilot-cli/issues/4069

### 5. #2792 [OPEN] 自动切换规划模型与执行模型
- **描述**：用户希望 Copilot 能在任务规划阶段使用一个配置模型（如更强的 Opus），在具体执行阶段自动切换为另一个模型（如更快的 Sonnet），以兼顾质量与速度。
- **热度**：👍 14 | 💬 4 | 创建于 2026-04-17  
- **链接**：https://github.com/github/copilot-cli/issues/2792

### 6. #2627 [OPEN] 可配置系统提示 — 降低固定 token 开销
- **描述**：当前 Copilot CLI 会话启动时系统提示消耗约 20,500 token，工具定义再占 8,500 token，对 200K 上下文窗口来说浪费 10%+ 空间。用户希望精简或自定义系统提示。
- **热度**：👍 18 | 💬 3 | 创建于 2026-04-10  
- **链接**：https://github.com/github/copilot-cli/issues/2627

### 7. #2193 [OPEN] `/fleet` 子代理默认模型配置
- **描述**：`/fleet` 生成的子代理无法继承用户的全局/项目模型设置，每次需在提示中重复指定，希望支持全局或项目级默认模型。
- **热度**：👍 4 | 💬 2 | 创建于 2026-03-20  
- **链接**：https://github.com/github/copilot-cli/issues/2193

### 8. #3399 [OPEN] BYOK 模式下允许自定义 HTTP 请求头
- **描述**：部分企业 LLM 网关要求发送 `X-Tenant-ID`、`X-Organization-ID` 等自定义头，目前 Copilot CLI 不支持设置，导致 BYOK（自带密钥）无法接入这些服务。
- **热度**：👍 5 | 💬 2 | 创建于 2026-05-19  
- **链接**：https://github.com/github/copilot-cli/issues/3399

### 9. #4076 [OPEN] 内置 research agent 的 MCP 工具可配置
- **描述**：`/research` 子代理硬编码了 `github/*` 和 `web/grep/glob/view` 工具集，无法使用用户其他已配置的 MCP 服务器，希望允许在 agent 定义中自定义工具。
- **热度**：👍 0 | 💬 1 | 新功能请求（2026-07-09）  
- **链接**：https://github.com/github/copilot-cli/issues/4076

### 10. #4068 [OPEN] 允许模型家族别名（如 `opus`、`sonnet`）自动解析为最新稳定版
- **描述**：用户需要手动锁定具体版本（如 `claude-opus-4.8`），随着版本迭代（4.5→4.8），每次都要修改配置。希望使用 `opus` 等家族名自动跟随最新稳定版。
- **热度**：👍 0 | 💬 0 | 新功能请求（2026-07-09）  
- **链接**：https://github.com/github/copilot-cli/issues/4068

---

## 重要 PR 进展

当日无新的 Pull Requests 合并或更新。

---

## 功能需求趋势

从近 24 小时活跃的 Issues 中可以提炼出社区最关注的几个方向：

1. **模型灵活性与自动化**  
   - 支持模型家族别名（如 `opus`、`sonnet`）自动解析最新版本（#4068）。  
   - 任务规划与执行阶段自动切换不同模型（#2792）。  
   - 子代理（`/fleet`）继承全局模型配置（#2193）。

2. **插件与作用域管理**  
   - 项目级/仓库级插件作用域（#1665 已关闭，但需求热度高）。  
   - 插件固定到 commit SHA（已在 v1.0.70-0 实现）。

3. **企业/安全集成**  
   - BYOK 自定义 HTTP 头（#3399）。  
   - macOS Gatekeeper 自动放行（#970）。  
   - 企业策略间歇性封锁（#1595）。

4. **性能与资源优化**  
   - 可配置系统提示以降低固定 token 开销（#2627）。  
   - 持久化事件日志句柄避免每次写入触发 Windows Defender 扫描（#4063）。

5. **UI/UX 与终端兼容性**  
   - TUI 挂死（#4069）、输出粘贴导致输入区错乱（#4060、#4070）。  
   - 会话列表仅显示当前会话（#4071）。  
   - 退出时提示使用会话名称而非 ID（#4066）。

6. **MCP 与工具扩展**  
   - 内置 research agent 支持自定义 MCP 服务器（#4076）。

---

## 开发者关注点

- **企业用户痛点**：策略误判、BYOK 无法设置自定义请求头、插件无法按项目隔离，影响大型组织采用。  
- **平台兼容性**：macOS Gatekeeper 每次升级需手动操作；WSL2 + Windows Terminal 下 TUI 不稳定；HTTP 代理缺失导致 `/research` 在企业内网失效（#4019 已关闭但仍为痛点）。  
- **会话与状态**：会话恢复不一致（#3931）、PR 状态小部件显示错误（#4062）、模型设置不生效（#4067）。  
- **性能开销**：系统提示固定消耗 20K+ token，用户希望裁剪；事件日志频繁文件 I/O 在 Windows 上触发 Defender 扫描，影响 CPU 和电池（#4063）。  
- **新版本体验**：v1.0.70-0 新增的 `--sandbox` 和 `/refine` 受到欢迎，但 TUI 挂死 bug 需要紧急热修复。

---

*以上内容基于 GitHub Copilot CLI 公开仓库（github.com/github/copilot-cli）截至 2026-07-10 的数据整理。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

好的，作为专注于 AI 开发工具的技术分析师，我已根据您提供的 GitHub 数据生成 2026-07-10 的 **Kimi Code CLI 社区动态日报**。

---

## Kimi Code CLI 社区动态日报

**日期:** 2026-07-10

### 1. 今日速览

过去 24 小时内，Kimi Code CLI 社区没有发布新版本，但有两项进展值得关注。一是社区正在热烈讨论关于 **SSL 证书忽略** 的功能增强，这反映了企业级用户在代理或安全软件环境下的真实痛点。二是社区贡献者正在推动对 **Claude Code 配置文件（CLAUDE.md）的兼容性支持**，这有助于降低从其他 AI 编码助手迁移的成本。

### 2. 版本发布

过去 24 小时内无新版本发布。

### 3. 社区热点 Issues

过去 24 小时内仅更新了 2 个 Issue，均值得关注：

- **#2458 [增强] 添加忽略 SSL 证书的选项**
  - **重要性**: ⭐⭐⭐⭐⭐
  - **摘要**: 用户在具有中间人（MiTM）检测功能的企业级防病毒软件环境下无法登录。该请求旨在增加一个 `--ignore-ssl` 或类似选项，以便在受控环境中绕过证书验证问题。
  - **社区反应**: 共 5 条评论，讨论集中在如何在保证安全的同时解决企业网络限制问题，暂无项目维护者回应。
  - **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2458

- **#2318 [Bug] 请求到达组织 TPD 速率限制，当前：1505241**
  - **重要性**: ⭐⭐⭐⭐
  - **摘要**: 用户报告使用 `kimi 2.6` 版本时，遇到了 API 速率限制问题，且反馈显示的 TPD（每日请求数）数据可能不准确。此问题关系到生产环境下的 API 使用体验和稳定性。
  - **社区反应**: 1 条评论，用户认为这是一个 “Critical Bug”，但项目维护者尚未正式回复。
  - **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2318

### 4. 重要 PR 进展

过去 24 小时内更新了 3 个 PR，是近期以来较为活跃的一次更新，集中在功能兼容性和稳定性修复上。

- **#2487 [功能] 支持加载 CLAUDE.md 文件**
  - **重要性**: ⭐⭐⭐⭐⭐
  - **功能**: 在 `load_agents_md()` 函数中增加了对 `CLAUDE.md` 和 `.claude/CLAUDE.md` 文件的发现和加载。这意味着项目如果已有 Claude Code 的配置，可以直接被 Kimi CLI 无缝使用，极大降低了从其他工具迁移的成本。
  - **链接**: https://github.com/MoonshotAI/kimi-cli/pull/2487

- **#2324 [修复] Web 模式下处理 BrokenPipeError 异常**
  - **重要性**: ⭐⭐⭐⭐
  - **功能**: 修复了在 Web 运行模式下，当子进程在消息发送前意外退出时，`send_message` 方法因未捕获 `BrokenPipeError` 导致程序崩溃的问题。提升了 Web UI 的稳定性。
  - **链接**: https://github.com/MoonshotAI/kimi-cli/pull/2324

- **#2449 [修复] 在字符串长度检查前去除换行符**
  - **重要性**: ⭐⭐⭐
  - **功能**: 修复了 `shorten_middle` 函数在输入文本较短时，未先删除换行符就进行长度检查的逻辑缺陷。这改进了工具调用参数摘要的渲染效果，确保单行显示的正确性。
  - **链接**: https://github.com/MoonshotAI/kimi-cli/pull/2449

### 5. 功能需求趋势

从近期活跃的 Issues 和 PRs 中，可以提炼出社区最关注的功能方向：

- **企业级安全与配置**:
  - **趋势**: 社区对在企业网络、VPN 或安装了安全软件的环境中工作的需求日益增长。核心需求包括忽略 SSL 证书错误、自定义证书链等。
  - **代表性 Issue**: #2458

- **跨平台与跨工具兼容性**:
  - **趋势**: 降低开发者从其他 AI 编码助手（如 Claude Code）迁移的门槛是关键。支持加载通用的项目配置文件（如 `CLAUDE.md`）是一个明确的信号。
  - **代表性 PR**: #2487

- **运行时稳定性**:
  - **趋势**: 开发者希望 CLI 在各种使用模式（Web 模式、Pipe 模式）下都能稳定运行，对未捕获的异常和进程管理漏洞的容忍度很低。
  - **代表性 PR**: #2324, #2449

### 6. 开发者关注点

总结开发者反馈中的核心痛点和需求：

- **企业环境的使用障碍**: 许多开发者希望 Kimi CLI 能在严格的企业网络策略下“开箱即用”。当前的 SSL 证书验证机制是最大的障碍，导致无法完成登录，这直接影响该工具在大型组织中的推广。
- **API 使用体验**: 用户对 API 速率限制（TPD）的反馈机制和准确性表示担忧。一个不准确或模糊的速率限制错误信息会让开发者感到困惑，并削弱对服务的信任。
- **对已有配置的复用**: 开发者不希望重复配置。支持读取 `CLAUDE.md` 等标准格式的配置文件，表明 Kimi CLI 正在积极拥抱生态，这是一个非常受欢迎的工程决策。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 (2026-07-10)

## 今日速览

- **连续发布三个补丁版本**：v1.17.16~v1.17.18，核心修复了 Copilot 零计费批次导致的崩溃，改进了 Meta、Grok 等模型的处理，并优化了桌面端 UI。
- **“复制到剪贴板”问题持续发酵**：已有 109 条评论、102 个 👍 的经典 Issue #4283 依然是社区最大痛点，同时新增 #24713（Linux 终端复制无效）和 #30472（SSH/tmux 修复 PR）表明问题正在被集中攻关。
- **V2 版本进入密集修复期**：多个 V2 相关 Issue 和 PR 被关闭，涉及事件可见性、中断耐久性、目录附件、TUI 同步等，标志着 V2 稳定性的关键冲刺。

## 版本发布

### v1.17.18
- **修复**：GitHub Copilot 返回零计费批次模型时不再崩溃，定价数据正确。
- **改进**：为 Meta Muse Spark 添加模型专属系统提示。
- [查看 Release](https://github.com/anomalyco/opencode/releases/tag/v1.17.18)

### v1.17.17
- **Core**：改进 Meta 模型推理变体和 provider 请求的处理。
- **Desktop**：修复模型选择器标签中文字被裁剪的问题；新增可关闭的标签页介绍弹窗和更新后的帮助入口；优化子代理任务行显示。
- [查看 Release](https://github.com/anomalyco/opencode/releases/tag/v1.17.17)

### v1.17.16
- **Core**：暴露 Grok 模型的推理努力（reasoning effort）变体；改进 xAI 的 prompt 缓存路由，为 Responses 模型添加 PDF 文件支持。
- **Desktop**：项目首页增加“打开包含文件夹”操作；为文件/命令新增 composer 添加菜单。
- [查看 Release](https://github.com/anomalyco/opencode/releases/tag/v1.17.16)

## 社区热点 Issues（10 个）

### 1. 复制到剪贴板功能失效（#4283） ⭐ 最热门
- **现象**：选中响应文本后无法复制到剪贴板，影响所有操作系统。
- **社区反应**：109 条评论，102 个 👍，持续数月未彻底解决。最新评论区有用户反馈 v1.17.x 中依然存在。
- [Issue 链接](https://github.com/anomalyco/opencode/issues/4283)

### 2. Gemma 4 通过 Ollama 工具调用失败（#20995）
- **现象**：使用 `ollama/gemma4:e4b` 时，模型正确返回 `tool_calls`，但 OpenCode 无法识别流式工具调用。
- **重要性**：表明对新兴模型（Gemma 4）的兼容性不足，社区已经在讨论修复方案。
- [Issue 链接](https://github.com/anomalyco/opencode/issues/20995)

### 3. 高 CPU 占用（#30086）
- **现象**：自约一周前更新后，CPU 占用急剧上升，从可同时运行 10+ 会话降至仅能运行 3 个。
- **社区反应**：19 条评论，12 个 👍，用户怀疑与最近的后台任务或 watcher 有关。
- [Issue 链接](https://github.com/anomalyco/opencode/issues/30086)

### 4. Linux 终端复制显示成功但实际无效（#24713）
- **现象**：在 Linux 终端中复制后弹出“已复制”提示，但剪贴板内容未改变。
- **特殊性**：与 #4283 相关但平台特定，已有关联 PR #30472 尝试修复（见下文）。
- [Issue 链接](https://github.com/anomalyco/opencode/issues/24713)

### 5. 子代理在 bash 工具调用后无限挂起（#33028）
- **现象**：快速 bash 调用后，子代理（和主代理）的下一次 LLM 流式调用永不完成且不超时，只能强制终止。
- **影响**：跨模型（glm-5.2、minimax-m3）复现，与 provider 路径相关。
- [Issue 链接](https://github.com/anomalyco/opencode/issues/33028)

### 6. GPT 5.6 模型认证错误（#36133）
- **现象**：使用 GPT 5.6 系列模型时请求失败，而 GPT 5.5 正常。错误提示与 API key 或模型名称有关。
- **热度**：5 条评论，已关闭（可能很快修复），但表明新模型适配仍有遗漏。
- [Issue 链接](https://github.com/anomalyco/opencode/issues/36133)

### 7. 应用补丁权限视图只显示第一个文件（#36119）
- **现象**：当 apply patch 请求修改多个文件时，用户只能看到第一个文件的变更，无法审查其他文件。
- **严重性**：影响安全审批流程，可能误批准未看到的改动。
- [Issue 链接](https://github.com/anomalyco/opencode/issues/36119)

### 8. LSP 容器化支持：processId 应为 null（#36162）
- **现象**：容器内运行的 LSP 因发送了进程 ID 而在 3 秒后被关闭。
- **需求**：请求支持 `processId: null` 以适配 Docker 等容器环境中的 LSP。
- [Issue 链接](https://github.com/anomalyco/opencode/issues/36162)

### 9. 子代理忽略 frontmatter 中的 `model:` 字段（#35126、#36132）
- **现象**：通过 task 工具启动子代理时，子代理强制继承父代理的模型，忽略自身 markdown 前文中声明的 `model:`。
- **社区反应**：#35126 有 2 条评论，1 个 👍；#36132 有 2 条评论。该问题直接违反文档，影响工作流灵活性。
- [Issue 链接](https://github.com/anomalyco/opencode/issues/35126) | [Issue 链接](https://github.com/anomalyco/opencode/issues/36132)

### 10. 配置 `tool_call: false` 无法禁用工具（#35432）
- **现象**：在模型配置中设置 `tool_call: false` 后，prompt loop 仍强制发送工具，导致不支持工具的 provider（如不启用 `--enable-tools` 的 morphllm）报错。
- **根本原因**：代码无条件解析 SessionTools 并设置 `tool_choice=auto`。
- [Issue 链接](https://github.com/anomalyco/opencode/issues/35432)

## 重要 PR 进展（10 个）

### 1. **fix(tui): support copying over ssh with tmux** (#30472)
- **内容**：为 SSH + tmux 场景实现正确的剪贴板管理（使用 `set-clipboard on`），关闭 #25253、#25252、#19982、#15907（均为复制问题）。
- **状态**：Open，但已获得核心贡献者关注，是复制问题的重要修复方向。
- [PR 链接](https://github.com/anomalyco/opencode/pull/30472)

### 2. **fix(app): preserve timeline bottom anchoring** (#36160)
- **内容**：升级 `@tanstack/solid-virtual` 库，修复浏览器裁剪时底部锚定失效的问题，确保新消息自动滚动到底部。
- **状态**：Open，Hona 提交。
- [PR 链接](https://github.com/anomalyco/opencode/pull/36160)

### 3. **fix(core): restore resilient compaction** (#36163)
- **内容**：改进 session 历史压缩机制，始终尝试手动压缩和 provider 溢出恢复；保留流式错误并报告空历史。
- **状态**：Open，rekram1-node 提交。
- [PR 链接](https://github.com/anomalyco/opencode/pull/36163)

### 4. **fix(tui): forward environment to worker** (#35925)
- **内容**：修复 Bun workers 不继承 `process.env` 的问题，恢复 `OPENCODE=1` 和 `AGENT=1` 环境变量，使命令在 worker 中正常运行。
- **状态**：已合并（Closed），由 opencode-agent 提交。
- [PR 链接](https://github.com/anomalyco/opencode/pull/35925)

### 5. **feat(observability): add v2 genai tracing** (#35935)
- **内容**：通过 OTLP 为 V2 添加端到端 GenAI 可观测性，记录每个 agent 轮次、模型步骤、HTTP/WS 传输、本地工具、重试、压缩、子代理等链路。附带 Dash0 配置文档。
- **状态**：Open，StarpTech 提交。
- [PR 链接](https://github.com/anomalyco/opencode/pull/35935)

### 6. **refactor(form): model links as fields** (#36129)
- **内容**：将模型 URL 请求重构为表单中的 `link` 字段，支持在 TUI 中打开、复制和手动完成；要求 questions 至少包含一个字段；空 schema 的 MCP 表单立即接受。
- **状态**：Open，rekram1-node 提交。
- [PR 链接](https://github.com/anomalyco/opencode/pull/36129)

### 7. **fix(app): clarify status indicator severity** (#36031)
- **内容**：状态指示器保持绿色（服务器/目录服务健康），非阻塞的 MCP/LSP 问题使用警告色，只有服务器离线才使用红色。统一弹窗投影。
- **状态**：Open，Hona 提交。
- [PR 链接](https://github.com/anomalyco/opencode/pull/36031)

### 8. **fix(app): align context tokens with usage** (#36015)
- **内容**：修复上下文字段中 tokens 和 cost 的显示不一致问题：cost 来自 session 总量，tokens 和用量来自最新助手上下文。
- **状态**：已合并（Closed），Hona 提交。
- [PR 链接](https://github.com/anomalyco/opencode/pull/36015)

### 9. **fix(app): show tree while opening files** (#36018)
- **内容**：在“打开文件”占位符激活时强制显示嵌入式文件树，并保留用户折叠树的偏好。
- **状态**：已合并（Closed），Hona 提交。
- [PR 链接](https://github.com/anomalyco/opencode/pull/36018)

### 10. **fix(core): preserve agent permission precedence** (#36159)
- **内容**：修复权限优先级：全局规则作为默认值，然后应用内置 agent 策略及用户覆盖；防止迁移后的遗留 `bash` 规则重新启用 `shell`；移除重复的 schema 默认权限条目。
- **状态**：Open，rekram1-node 提交。
- [PR 链接](https://github.com/anomalyco/opencode/pull/36159)

## 功能需求趋势

从近 24 小时更新的 Issues 中可提炼出以下社区最关注的功能方向：

1. **模型兼容性扩展**
   - 对 GPT-5.6、Gemma 4、Grok 等新模型的即时支持，包括推理变体（reasoning effort）、工具调用、流式适配。
   - 自动从 OpenAI 兼容 API (`/v1/models`) 获取自定义模型 ID (#35855)。

2. **子代理（Sub-agent）控制粒度**
   - 支持通过环境变量 `OPENCODE_SUBAGENT_MODEL` 单独指定子代理模型 (#36147)。
   - 要求子代理尊重 frontmatter 中的 `model:` 字段，而非强制继承父代理 (#35126, #36132)。

3. **复制/剪贴板体验改进**
   - 跨平台（Linux、SSH、tmux）的剪贴板一致性，包括显示正确反馈和实际复制内容 (#24713, #30472)。

4. **LSP 与容器化开发环境**
   - 支持容器内运行 LSP（`processId: null`）、自签名 TLS 证书 (#35365)，以及 Vue/Nuxt 等特殊框架的 LSP 配置。

5. **V2 稳定性和耐久性**
   - 机器重启后中断任务保持 spinning 状态、TUI 同步多个客户端模型切换、事件可见性定义、目录附件正确传递给 provider 等。

6. **权限与安全**
   - 更清晰的补丁审批 UI（多文件显示）、配置 `tool_call: false` 实际生效、子代理权限继承混乱 (#36159)。

## 开发者关注点

- **复制功能依然是头号痛点**：Issue #4283 已存在 8 个月，相关 PR #30472 仍在开放，Linux + SSH 场景尤其严重。
- **新模型适配有滞后**：GPT-5.6 和 Gemma 4 的适配问题在最近版本中频繁出现，提示需要更系统的模型测试框架。
- **V2 版本 BUG 集中爆发**：虽然 V2 步入密集修复期，但目录附件、事件广播、TUI 同步、中断恢复等基础功能仍存在问题，预计后续几个版本将继续快速迭代。
- **性能回归警告**：高 CPU 占用 (#30086) 可能与前几天的 watcher 改动有关，若下周未解决可能成为新的社区焦点。
- **子代理模型控制缺失**：用户希望精细控制子代理使用的模型以节省成本或分配不同能力，当前强制继承父模型的设计限制了高级工作流。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 **2026-07-10 Qwen Code 社区动态日报**。

---

# 2026-07-10 Qwen Code 社区动态日报

**日报日期:** 2026-07-10 (基于过去24小时数据)

---

## 今日速览

1.  **cua-driver 发布 v0.7.1**，新增相对坐标支持，并为 macOS 提供公证后的通用二进制和 `.app` 包。
2.  **社区最热议题**集中在上传/粘贴图片功能回归（#6560，18条评论）与多工作区 daemon 架构（#6378，19条评论）两大方向。
3.  **安全与性能问题**曝光率上升：Shell 子进程泄漏凭证（#6601，P1）、Glob 工具 OOM（#6614，P1）等紧急 Bug 正在被积极修复。

## 版本发布

### cua-driver-rs v0.7.1
- **更新内容**: 发布预编译二进制包 (vendored under `packages/cua-driver`)，主要特性为 **启用相对坐标**。
- **平台支持**:
    - macOS: 已公证+签名，提供通用二进制及 `QwenCuaDriver.app`。
    - Linux: 未签名 (x86_64 + arm64, glibc 2.31+)。
    - Windows: 未签名 (x86_64 + arm64)。
- **链接**: [Release 页](https://github.com/QwenLM/qwen-code/releases/tag/cua-driver-rs-v0.7.1)

---

## 社区热点 Issues（精选 10 条）

1.  **#6378 [RFC] 支持单个 daemon 管理多个工作区**  
    *P2 / feature-request / 19 评论*  
    核心架构讨论，当前模型为 "1 daemon = 1 workspace × N sessions"。RFC 规划扩展为单个 `qwen serve` 进程支持多个独立工作区，同时保证现有单工作区行为不变。社区参与度高，正等待讨论定稿。  
    [查看详情](https://github.com/QwenLM/qwen-code/issues/6378)

2.  **#6560 恢复对话中直接上传/拖拽图片和文档**  
    *P3 / bug+feature-request / 18 评论*  
    用户在 CLI 对话界面无法粘贴截图或拖拽文件（CV, 拖拽均无响应），只能通过 `read_file` 工具读取本地文件，体验剧降。该功能在之前版本可用，重新安装后仍无效，引发广泛共鸣。  
    [查看详情](https://github.com/QwenLM/qwen-code/issues/6560)

3.  **#6581 JetBrains ACP agent 用户提示未转发至 Qwen Code agent**  
    *P2 / bug / 8 评论*  
    用户在 IntelliJ IDEA 中将 Qwen Code 作为 AI Assistant 使用本地 Ollama 模型时，IDE 只发送了 bootstrap 上下文，用户输入完全不被传递给 agent。严重影响 IDE 集成体验，已标记需分诊。  
    [查看详情](https://github.com/QwenLM/qwen-code/issues/6581)

4.  **#6601 Shell 子进程继承敏感环境变量导致凭证泄露**  
    *P1 / bug / 2 评论*  
    `run_shell_command` 产生的子进程继承整个 daemon 的环境变量（含 `QWEN_SERVER_TOKEN`、API Key 等），agent 执行任意 shell 命令时可能暴露凭证。属于 **安全紧急问题**，欢迎 PR。  
    [查看详情](https://github.com/QwenLM/qwen-code/issues/6601)

5.  **#6614 Glob 工具在扫描大目录时 OOM**  
    *P1 / bug / 2 评论*  
    子 agent 执行 `glob` 工具（pattern `**`）时触发 Node 进程堆内存耗尽，输出截断机制在 OOM 之前未生效。影响高频文件搜索场景，需优化内存控制。  
    [查看详情](https://github.com/QwenLM/qwen-code/issues/6614)

6.  **#6595 qwen3.7-max 在长上下文中泄漏 `<analysis>/<summary>` 标签**  
    *P2 / bug / 3 评论*  
    使用 `qwen3.7-max` 模型时，部分响应内直接暴露内部协议标签，导致工具调用中断及后续动作失效。建议在客户端做后处理过滤。  
    [查看详情](https://github.com/QwenLM/qwen-code/issues/6595)

7.  **#6565 认证失败：连接 Qwen Coder 时出现 Internal Error**  
    *P3 / bug / 7 评论*  
    用户（疑似国际用户）连接 Qwen Coder 服务时反复弹出 "Internal Error"，日志显示认证层问题。影响订阅用户的正常使用，需进一步收集信息。  
    [查看详情](https://github.com/QwenLM/qwen-code/issues/6565)

8.  **#3696 综合热重载系统：skills/extensions/MCP/配置无需重启生效**  
    *P1 / feature-request / 5 评论*  
    跟踪 Issue，计划实现运行时热重载技能、扩展、MCP 服务器、LSP 和配置变更。部分已实现，剩余工作需持续跟进。是提升开发效率的关键特性。  
    [查看详情](https://github.com/QwenLM/qwen-code/issues/3696)

9.  **#6582 审批模式切换时 UI 提示中英文混杂**  
    *P2 / bug / 3 评论*  
    使用 Shift+Tab 切换审批模式时，状态栏和弹窗部分显示英文、部分显示中文，不跟随 `general.language` 设置。本地化一致性待改进。  
    [查看详情](https://github.com/QwenLM/qwen-code/issues/6582)

10. **#6487 记忆索引在 `/remember` 后过期，压缩时丢失记忆内容**  
    *P2 / bug / 2 评论*  
    长会话中，手动或自动记忆保存后，`MEMORY.md` 索引写入磁盘但未更新系统指令；记忆压缩后已有内容丢失。影响长时间对话的上下文保持能力。  
    [查看详情](https://github.com/QwenLM/qwen-code/issues/6487)

---

## 重要 PR 进展（精选 10 条）

1.  **#6617 fix(channels): 截断频道记忆召回提示**  
    为防止过量记忆注入导致 token 浪费，PR 限制注入的频道记忆前缀长度，并添加显式截断标记。已被合并（Closed）。  
    [查看详情](https://github.com/QwenLM/qwen-code/pull/6617)

2.  **#6631 feat(cli): 支持列出非主工作区的归档/归类会话**  
    一个 daemon 托管多个工作区时，为受信任的非主工作区也提供与主工作区相同的会话列表视图（归档、固定分组、过滤）。扩展多工作区能力。  
    [查看详情](https://github.com/QwenLM/qwen-code/pull/6631)

3.  **#6556 fix(core): 将 max_tokens 钳制到上下文窗口，移除输出预留**  
    自动压缩策略回归：基于完整上下文窗口决定何时压缩，每次请求向模型索取窗口剩余空间可容纳的输出量，消除之前人为制造固定大输出的预留逻辑。  
    [查看详情](https://github.com/QwenLM/qwen-code/pull/6556)

4.  **#6615 fix(channels): 仅返回最终 ACP 响应文本**  
    修复通道 agent 多轮工具调用时中间思考文本被拼接进最终响应的问题。将计划更新与权限请求视为轮次边界，彻底分离中间文本。  
    [查看详情](https://github.com/QwenLM/qwen-code/pull/6615)

5.  **#6630 fix(core): YOLO 模式下保持模式，不被 `enter_plan_mode` 切换**  
    当 session 处于 YOLO 模式时，模型发起的 `enter_plan_mode` 工具调用不再将 session 切换到只读 Plan 模式，而是保持当前模式并提示模型继续。  
    [查看详情](https://github.com/QwenLM/qwen-code/pull/6630)

6.  **#6591 feat(web-shell): 新增 artifact 右侧面板**  
    为 Web Shell 添加可拖拽的右侧面板，展示编辑文件的差异统计、可展开的逐行 diff、文件列表/树导航。提升在线 IDE 体验。  
    [查看详情](https://github.com/QwenLM/qwen-code/pull/6591)

7.  **#6599 ci: 添加可疑评论附件守卫**  
    新增 GitHub Actions 工作流，自动检查社区评论中是否包含高风险文件链接（安装程序、脚本、二进制等），发现后立即删除。增强仓库安全性。  
    [查看详情](https://github.com/QwenLM/qwen-code/pull/6599)

8.  **#6495 feat(channels): 支持 webhook 触发的频道任务**  
    daemon 管理的频道可配置外部 webhook 源；POST 事件到 `qwen serve` 后，Qwen 将事件作为上下文生成响应，并由频道工作者主动交付到聊天会话。  
    [查看详情](https://github.com/QwenLM/qwen-code/pull/6495)

9.  **#6489 feat(hooks): 添加 MessageDisplay 钩子支持流式中途展示**  
    新增 `MessageDisplay` hook 事件，在 assistant 回复流式输出过程中反复触发，而非仅在结束时的 `Stop` 事件。让终端 UI 和 ACP 能实现增量观察，补足 #6488 所描述的空缺。  
    [查看详情](https://github.com/QwenLM/qwen-code/pull/6489)

10. **#6019 feat(cli): `/model --compaction` 支持配置专用压缩模型**  
    允许用户通过 `/model --compaction` 命令单独设置用于对话压缩（auto-compact）的模型，与主模型解耦。已在 CI 中推进多轮评审。  
    [查看详情](https://github.com/QwenLM/qwen-code/pull/6019)

---

## 功能需求趋势

从过去 24 小时的 Issues 和 PR 中可以提炼出以下社区聚焦方向：

- **多工作区/多 session 管理** – 从单 daemon 单工作区向多工作区扩展，支持频道、通道、归档等高级管理功能（#6378, #6631, #5976）。
- **子 Agent 可观测性与干预能力** – 用户希望在子 agent 执行时能够实时查看其行为、完整执行轨迹，并支持手动干预（#6569, #6580）。
- **IDE 集成深度优化** – 修复 JetBrains 提示丢失问题（#6581），完善审批模式切换 UI 本地化（#6582），提升与 IDE 交互的一致性。
- **安全与凭证保护** – 社区愈发关注 shell 子进程凭证泄漏（#6601）、GitHub 评论恶意附件（#6597）、以及敏感变量隔离。
- **高负载/长上下文稳定性** – 解决 Glob 工具 OOM（#6614）、PDF 读取无图像回退死循环（#6586）、内部标签泄漏（#6595）等问题。
- **热重载与无重启配置** – #3696 跟踪 Issue 持续活跃，期望技能、扩展、MCP 等变更无需重启 session 即可生效。

---

## 开发者关注点

- **粘贴/上传图片功能回归** – #6560 获得 18 条评论，多个用户确认 Ctrl+V / 拖拽在 macOS 和 Windows 下均失效，根因是原生模块 `@teddyzhu/clipboard` 未打包（#6590, #6594, #6577）。临时工作区：使用 `read_file` 工具读取本地图片，但体验远不如直接粘贴。
- **Windows 兼容性痛点** – 乱码输出（#6214）、扩展安装失败（#6334）、Alt+V 粘贴无效（#6577）持续困扰 Windows 用户，社区期待针对 Win32 的专用修复。
- **认证与连接错误** – #6565 和 #6477 反映部分用户无法使用订阅/令牌登录，返回 “Internal Error” 或 “Can not use my subscription”，可能与服务器端认证策略或 Token Plan 有关，需官方介入排查。
- **日志与调试不完整** – #6600 指出 `--debug` 模式下虽然打印日志路径但文件未被实际创建，给问题定位带来障碍，属于基础功能一致性 bug。
- **记忆与上下文退化** – 长会话中记忆索引不同步（#6487）以及压缩后的内容丢失，开发者期望能改善记忆持久性和准确合并。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*