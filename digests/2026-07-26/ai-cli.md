# AI CLI 工具社区动态日报 2026-07-26

> 生成时间: 2026-07-25 22:35 UTC | 覆盖工具: 7 个

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

好的，作为专注于 AI 开发工具生态的资深技术分析师，我已仔细审阅了您提供的 2026-07-26 各主流 AI CLI 工具的社区动态摘要。现基于这些数据，为您呈现一份横向对比分析报告。

---

### AI CLI 工具生态横向对比分析报告 (2026-07-26)

**报告人：** 资深 AI 开发工具生态分析师
**报告日期：** 2026-07-26
**数据来源：** Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Qwen Code 官方 GitHub 仓库当日动态

---

#### 1. 生态全景：从“尝鲜”到“基建”，稳定与安全成为集体命题

当前，AI CLI 工具已从“新奇玩具”阶段迈入深度嵌入开发者工作流的“生产基建”阶段。各工具社区均展现出极高的活跃度，但舆论焦点正从“功能有无”转向“体验优劣”和“安全可靠”。具体表现为：**模型计费透明度、跨平台协同稳定性、Agent 行为可控性** 以及 **本地数据与配置安全** 成为所有工具的共性挑战。社区不再是简单地要求新功能，而是对工具在执行长周期、高复杂度、多团队协作任务时的 **鲁棒性、一致性和可预测性** 提出了更高要求。

---

#### 2. 各工具活跃度对比

| 指标 | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code CLI | OpenCode | Qwen Code |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **版本发布** | √ (v2.1.220) | √ (4个Alpha) | ✗ | ✗ | ✗ | ✗ | √ (Nightly) |
| **精选 Issues (10条)** | 10 (4个Open) | 10 (9个Open) | 10 (8个Open) | 10 (9个Open) | 2 (2个Open) | 10 (8个Open) | 10 (8个Open) |
| **重要 PRs (3-10条)** | 3 (1个Open) | 10 (全部Merged) | 10 (5个Open) | 2 (全部Closed) | 4 (3个Merged) | 10 (6个Merged) | 10 (6个Open) |
| **社区情绪关键词** | 付费困惑、稳定性焦虑 | 限速不满、远程崩溃 | Agent不可靠、无限重试 | 配置丢失、性能回归 | 功能期待、稳定修复 | 安全恐慌、UI争议 | 渲染缺陷、兼容性痛点 |
| **整体节奏** | 维护与修复 | 稳步迭代 | 快速开发与修复 | Bug修复周期 | 功能与修复并行 | 快速迭代，问题爆发 | 活跃开发，社区参与 |

**解读**:
*   **OpenAI Codex** 和 **Qwen Code** 是社区开发活动最活跃的，PR 数量和合并频率高。
*   **Claude Code** 和 **Copilot CLI** 社区反馈极为热烈（高赞、多评论），但版本发布节奏相对放缓，专注于解决痛点问题。
*   **Gemini CLI** 处于快速迭代与问题暴露并行阶段，PR 和 Issue 数量均很高。
*   **Kimi Code CLI** 社区相对较小，但也在稳定推进修复工作。
*   **OpenCode** 社区讨论热度极高，但伴随严重安全事件和重大 UI 争议，是当日最“喧闹”的工具。

---

#### 3. 共同关注的功能方向

多个工具的社区围绕以下核心诉求产生了强烈共鸣：

1.  **模型计费与配额透明化 (Claude Code, Codex, Copilot CLI)**
    *   **诉求**: 用户要求明确且可预测的计费模型。Claude Code 用户不满 Fable 5 纳入 Max 计划后仍有额外扣费；Codex 和 Copilot CLI 用户则抱怨周配额重置时间不固定，并对 credits 消耗速度感到困惑。

2.  **跨平台与远程控制可靠性 (Claude Code, Codex, Kimi Code, OpenCode)**
    *   **诉求**: 实现桌面、移动、CLI 无缝会话同步的需求非常强烈。Codex 和 OpenCode 的远程连接功能被报告存在严重稳定性问题（崩溃、卡死），而 Kimi Code 和 Claude Code 社区则直接提出远程控制的 Feature Request。**这表明用户希望摆脱单一终端束缚，追求随时随地的工作连续性。**

3.  **Agent 行为的可控性与可预测性 (Claude Code, Gemini CLI, Copilot CLI)**
    *   **诉求**: 社区普遍希望 Agent 能更严格地遵循项目级配置文件（如 CLAUDE.md），并能准确报告任务状态。Gemini CLI 的 Agent 频繁“假成功”（报告 Goal 完成但实际未执行）和无限挂起，Copilot CLI 的 /ask 命令静默失败，都极大地损害了用户对 Agent 的信任。

4.  **长期会话稳定性与上下文管理 (Claude Code, Copilot CLI, Copilot CLI)**
    *   **诉求**: 针对长时间、多轮对话会话中的上下文丢失、规则失效、意外压缩和资源泄漏问题，多工具用户表达了强烈不满。Copilot CLI 的 Session 恢复导致 OOM 和配置被覆盖，Claude Code 的自动压缩行为不可控，均是具体表现。

5.  **基础设施安全与配置健壮性 (OpenCode, Gemini CLI, Copilot CLI)**
    *   **诉求**: 这是一个新出现的、由具体事件驱动的共性趋势。OpenCode 的服务器被挖矿事件引发了行业警觉。Gemini CLI 的 Auto Memory 日志泄露和 Copilot CLI 的密码掩码失效问题，都指向了 **安全设计不能仅仅是“加一个开关”，而应是默认安全、架构级的安全。**

---

#### 4. 差异化定位分析

| 工具 | 核心定位 | 目标用户 | 技术路线/特点 | 当前主要挑战 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 专业级项目管理 & 复杂代码库导航 | 高级开发者、架构师、大中型项目团队 | 强调项目规则（CLAUDE.md）、长期任务规划（Goal系统）、深度代码理解 | **计费模型复杂**、**Agent长期一致性**、**多会话管理** |
| **OpenAI Codex** | 开放灵活的开发伙伴，强推理能力 | 追求最新模型能力、对推理性能敏感的开发者 | 快速迭代 Rust 版本、强调工具调用（Tools）、广泛的 API 兼容性 | **配额与限速策略不透明**、**Windows 及远程连接兼容性差** |
| **Gemini CLI** | 多 Agent 协作的探索先锋 | 喜欢 “Agentic” 协同、愿意尝试前沿功能的开发者 | 内建 Auto Memory、A2A 服务器、强大的 Agent 编排能力 | **Agent 核心稳定性差**（挂起、假成功）、**安全与资源管理缺陷** |
| **Copilot CLI** | VS Code & GitHub 生态的 CLI 扩展 | 深度依赖 GitHub 和 VS Code 生态的开发者 | 与 IDE 和 GitHub 集成深度最高、适合日常开发流 | **Session 管理脆弱**、**配置被静默覆盖**、**性能回归** |
| **Kimi Code CLI** | 轻量级、易上手的日常工具 | 初创团队、个人开发者、寻求简洁体验的用户 | 功能相对聚焦，在 Web 和 Session 体验上做优化 | **功能丰富度不足** (远程控制)、**稳定性有待提升** (死循环) |
| **OpenCode** | “AI 优先”的开源新范式 | 拥抱开源、喜欢自定义、对隐私敏感的用户 | 代码开源、自托管服务器、强调终端 UI（TUI）、社区能力极强 | **默认配置导致严重安全风险**、**UI 大改引发社区分裂**、**桌面端稳定性差** |
| **Qwen Code** | 多平台、多模型的中文友好生态 | 中文开发者、需要跨平台（含微信等）集成的用户 | 对中文支持好、WebUI 功能强大、积极接受社区 PR | **终端渲染缺陷**、**扩展生态兼容性**、**数学/科学领域的专业支持** |

---

#### 5. 社区热度与成熟度

*   **高热度 / 成熟度 (Claude Code, OpenAI Codex, Gemini CLI):**
    *   这三个社区用户基数大，讨论深度高，反馈集中在复杂、深层次的生产力问题（如计费、Agent 可靠性、配额管理）。这表明产品已充分融入用户核心工作流。
    *   **Gemini CLI** 尤其值得注意，其 Issue 和 PR 数量庞大，但多为 P1/P2 级别的高优先级 bug，表明其正处于快速扩张但质量欠稳的“青春期”。

*   **高热度 / 快速迭代 (OpenCode, Qwen Code):**
    *   **OpenCode** 社区异常活跃，但话题从严重安全事件到 UI 红蓝之争，情绪波动极大，显示出项目快速发展伴随的“阵痛”。其高开放度（开源）带来了活跃的贡献者，但也暴露了默认安全设计的不足。
    *   **Qwen Code** 社区开发参与度很高，接受了大量社区 PR，并标注了 `welcome-pr` 和 `ready-for-agent` 的标签，展示了成熟的开源社区运营策略。

*   **稳定 / 生态绑定 (GitHub Copilot CLI, Kimi Code CLI):**
    *   **Copilot CLI** 社区活跃，但讨论议题非常聚焦，多与 GitHub/VS Code 生态内体验相关，显示出其作为生态“组件”而非独立工具的定位。
    *   **Kimi Code CLI** 社区规模较小，讨论热度相对平稳，正处于功能扩展和基础体验打磨阶段。

---

#### 6. 值得关注的趋势信号

1.  **“Agent 可靠性”已成为行业级痛点：** 从 Gemini CLI 的“假成功”到 Claude Code 的“规则忽略”，再到 Copilot CLI 的“静默失败”，**Agent 无法准确完成任务或汇报状态是当前最损害用户信任的问题**。任何解决这个问题的方案，无论是更好的上下文管理、更严谨的评估框架（如 Gemini 的 PR #28530），还是更直观的进度展示，都将成为关键竞争优势。

2.  **跨设备协同成为刚需：** 开发者不再满足于单一终端。Claude Code、Kimi Code、OpenCode 社区对远程控制、跨平台会话同步的强烈需求，预示着下一个竞争焦点是 **成为一个无处不在的智能工作节点**。工具需要像 IDE 一样支持 Session 漫游和状态同步。

3.  **安全与成本控制必须“原生支持”：** OpenCode 服务器被挖矿是一个强烈的警示信号。**默认不安全的配置在任何生产级工具中都是不可接受的**。同时，Claude Code 的无限重试烧 token 问题也表明，**成本意识和安全防护一样，需要被内建在工具的架构中，而不是留给用户后知后觉**。AI CLI 工具正在从“个人玩具”向“企业工具”演进，安全和成本是入场券。

4.  **“社区驱动开发”的兴起与挑战：** Qwen Code 的 `ready-for-agent` 标签和 Gemini CLI 的自动化 PR 管道（SSR Pipeline）是一个值得关注的信号。这意味着 **AI 开发工具不仅仅是帮助写代码，其自身的开发流程也开始被 AI Agent 所赋能**。这降低了社区贡献的门槛，但也对工具的代码质量和自动化审查能力提出了更高要求。OpenCode 社区的激进与活力，也证明了开放生态的巨大潜力和治理挑战。

**对开发者的参考价值：**
*   **选型时**，不应只看重模型能力或功能列表，更应考察工具的 **长期会话稳定性**、**配置可靠性** 和 **安全实践**。
*   **使用时**，警惕 Agent 的“过度自信”，特别是在执行破坏性操作（如 git reset）时。要积极利用项目级配置文件来约束 Agent 行为。
*   **决策时**，如果团队依赖特定生态（如 GitHub/VS Code），Copilot CLI 是自然之选；若追求前沿 Agent 能力，需接受 Gemini CLI 当前的不稳定性；若重视安全与透明度，开源的 OpenCode 值得关注，但其默认配置需立即加固；若需要专业级项目管理，Claude Code 仍是标杆，但要解决其计费困惑。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的。作为一名专注于 Claude Code 生态的技术分析师，我已根据您提供的截至 2026-07-26 的数据，完成了对 `anthropics/skills` 仓库的深度分析。

以下是 Claude Code Skills 社区热点报告：

---

### Claude Code Skills 社区热点报告

**数据来源:** github.com/anthropics/skills | **截止日期:** 2026-07-26

#### 1. 热门 Skills 排行

以下是根据社区讨论热度（评论数）和关注度筛选出的 Top Skills（PR）：

1.  **skill-creator: 修复 `run_eval.py` 0% 召回率核心 Bug**
    *   **PR #1298**: [链接](https://github.com/anthropics/skills/pull/1298)
    *   **功能**: 修复 `run_eval.py` 脚本，该脚本是技能优化循环（`run_loop.py`）的核心依赖，负责评估测试查询的召回率。
    *   **社区热点**: **这是当前生态中影响最广的 Bug 修复 PR**。Issue #556 (12条评论) 和 #1061 (3条评论) 等多个独立用户报告了 `recall=0%` 的致命问题，导致技能优化闭环完全失效。此 PR 试图从根本上解决触发检测失败、Windows 兼容、并行执行等多个根因。
    *   **状态**: Open

2.  **Add document-typography skill (文档排版技能)**
    *   **PR #514**: [链接](https://github.com/anthropics/skills/pull/514)
    *   **功能**: 为 AI 生成的文档提供排版质量控制，解决“孤儿词”、“寡行段落”和“编号错位”等常见美化问题。
    *   **社区热点**: 社区普遍认为这是 AI 生成内容“最后一公里”的关键能力。该功能通过“隐形”的排版矫正，显著提升输出文档的专业性，被社区视为一项“成熟”且“高价值”的 Skill。
    *   **状态**: Open

3.  **Add frontend-design skill (前端设计技能)**
    *   **PR #210**: [链接](https://github.com/anthropics/skills/pull/210)
    *   **功能**: 重构了前端设计技能，旨在提升指令的清晰度、可操作性和内部一致性，确保 Claude 能在单次对话中有效执行。
    *   **社区热点**: 讨论集中在如何让 Skill 指令从“开发文档”转变为“可执行的 Agent 指令”。社区对 `frontend-design` 的核心关注点在于其“无效性”，认为原版描述过于冗长和理论化。此 PR 代表了将 Skill 视为“精确命令”的最佳实践方向。
    *   **状态**: Open

4.  **Add testing-patterns skill (测试模式技能)**
    *   **PR #723**: [链接](https://github.com/anthropics/skills/pull/723)
    *   **功能**: 这是一个涵盖完整测试栈的综合技能，从测试哲学（测试奖杯模型）、单元测试（AAA 模式）到 React 组件测试（Testing Library）。
    *   **社区热点**: 社区对“一站式”提升 Claude 测试生成能力有高度需求。该 PR 试图将多种主流测试范式、模式和最佳实践编码为一个系统性的指令集，是解决“如何编写高质量测试”这一普遍痛点的有力方案。
    *   **状态**: Open

5.  **Add pyxel skill (Pyxel 复古游戏开发技能)**
    *   **PR #525**: [链接](https://github.com/anthropics/skills/pull/525)
    *   **功能**: 为 `Pyxel` 复古游戏引擎添加技能，覆盖从编写代码、运行捕获、审查到迭代的完整工作流。
    *   **社区热点**: 这是一个典型的“趣味 + 实用”型 Skill，满足社区中“用 AI 做游戏”的探索需求。其 MCP 服务器与 Claude Code 的集成方案，也成为了讨论 Agent 如何管理第三方开发工具链的案例。
    *   **状态**: Open

#### 2. 社区需求趋势

从 Issues 中可以提炼出社区最核心的三大需求方向：

1.  **开发者体验与工具链可靠性 (DX & Reliability)**:
    *   **核心痛点**: `skill-creator` 工具的 Bug（如 #556: 0% 召回率，#1061: Windows 兼容性）是社区最强烈的呼声。技能开发流程的阻塞直接影响了整个 Skill 生态的构建效率。这从 #1298、#1099、#1050 等多个高热度修复 PR 中可见一斑。

2.  **安全、治理与信任 (Security & Governance)**:
    *   **核心痛点**: Issue #492 (43条评论) 爆发式关注“信任边界滥用”问题。社区担心在 `anthropic/` 命名空间下分发的社区技能会误导用户，让用户误认为是官方认证，从而授予不必要的高权限。这直接关联到 Agent 系统的安全底线。

3.  **组织级协作与共享 (Enterprise & Sharing)**:
    *   **核心痛点**: Issue #228 (8个👍) 强烈要求实现组织内的技能库共享功能。当前的“下载 -> 传输 -> 手动上传”流程严重阻碍了 Skill 在企业团队中的推广和复用。这表明社区已从“个人使用”进入“团队协作”阶段。

#### 3. 高潜力待合并 Skills

以下 PR 讨论度高，功能完整，若合并将对生态产生显著正向影响：

1.  **PR #1302**: **Add color-expert skill** -> [链接](https://github.com/anthropics/skills/pull/1302)
    *   **分析**: 一个极其专业的颜色知识技能。涵盖了 ISCC-NBS、Munsell、RAL 等多种色名系统及色彩空间选择表。评论活跃且更新至 7月21日，项目成熟度高，落地概率大。将为 Claude 注入深度垂直知识。
2.  **PR #1367**: **Add self-audit skill** -> [链接](https://github.com/anthropics/skills/pull/1367)
    *   **分析**: 一个“元技能”，自动对 Claude 输出进行机械性文件验证和四维度推理质量审计。这是社区对“AI 输出可靠性”诉求的直接回应，符合未来 Agent 自我校验的趋势。作者提出了非常严谨的流水线设计。
3.  **PR #486**: **Add ODT skill** -> [链接](https://github.com/anthropics/skills/pull/486)
    *   **分析**: 为 OpenDocument 格式 (.odt, .ods) 提供全面支持，是对现有 `pdf`、`docx` 等办公套件 Skill 的重要补充，满足了依靠 LibreOffice 等开源生态的用户群体。

#### 4. Skills 生态洞察

一句话总结：**当前社区的诉求已从“创造新技能”阶段，全面转向解决“基础工具链的可靠性”、“安全信任模型”和“企业级共享”等最根本的生态建设问题。**

---

# 🤖 Claude Code 社区动态日报 — 2026-07-26

> 数据来源：GitHub [anthropics/claude-code](https://github.com/anthropics/claude-code) | 统计周期：过去 24 小时

---

## 今日速览

- **版本 v2.1.220 发布**，主要包含 Bug 修复与可靠性提升。
- **Fable 5 模型计费/可用性问题持续发酵**：#79337 获得 44 条评论，Max 用户在 Fable 5 纳入计划后仍被要求付费，社区反馈强烈。
- **跨平台统一会话/设置的需求最受期待**（👍24），同时关于模型意外降级、CLAUDE.md 规则被忽略等稳定性问题继续困扰开发者。

---

## 版本发布

### v2.1.220
- **更新内容**：Bug 修复和可靠性改进。
- **链接**：[Release v2.1.220](https://github.com/anthropics/claude-code/releases/tag/v2.1.220)

---

## 社区热点 Issues（10 条精选）

### 1. [BUG] Fable 5 在 Max 计划中仍提示“需要使用额度”
- **Issue #79337** 🔥 44 条评论 · 14 👍 | 🟢 **OPEN**
- **摘要**：2026-07-20 起 Fable 5 已纳入 Max 计划，但 Claude Code 仍提示需要额外消耗 usage credits，并自动降级至 Opus 4.8，导致用户困惑和不满。
- **链接**：[#79337](https://github.com/anthropics/claude-code/issues/79337)

### 2. [Feature] 跨桌面端、移动端、CLI 的统一会话与设置
- **Issue #42050** · 5 条评论 · 24 👍 | 🟢 **OPEN**
- **摘要**：请求实现跨平台会话恢复、项目设置同步和一致的功能体验，社区点赞数最高。
- **链接**：[#42050](https://github.com/anthropics/claude-code/issues/42050)

### 3. [BUG] Fable 模型在会话中无故不可用
- **Issue #68137** · 9 条评论 · 0 👍 | 🔴 **CLOSED** (stale)
- **摘要**：会话进行中突然报错 “Invalid or inaccessible model claude-fable-5”，用户被迫重新选择模型。反映出 Fable 5 的认证/可用性机制不稳定。
- **链接**：[#68137](https://github.com/anthropics/claude-code/issues/68137)

### 4. [Feature] 向 AI 模型暴露 session_id 和上下文窗口使用量
- **Issue #36678** · 8 条评论 · 2 👍 | 🔴 **CLOSED** (stale)
- **摘要**：开发者希望模型能感知自身会话 ID 和当前上下文窗口占用百分比，以便更好地管理 token 预算。该信息已在 CLI 中存在但未传递给模型。
- **链接**：[#36678](https://github.com/anthropics/claude-code/issues/36678)

### 5. [BUG] Claude Code 持续忽略项目级 CLAUDE.md 指导规则
- **Issue #62087** · 8 条评论 · 1 👍 | 🔴 **CLOSED** (stale)
- **摘要**：在长期实现会话中，Claude 反复违反 CLAUDE.md 中明确的规则（如编码风格、架构约定），需要用户反复纠正。
- **链接**：[#62087](https://github.com/anthropics/claude-code/issues/62087)

### 6. [BUG] 扩展使用后模型访问被限制 / 速率限制导致会话中断
- **Issue #68133** · 5 条评论 · 0 👍 | 🔴 **CLOSED** (stale)
- **摘要**：用户进行家庭网络文档编写 2 小时后被强制退出 Fable 5，且无法降级到其他模型，担心丢失会话进度。
- **链接**：[#68133](https://github.com/anthropics/claude-code/issues/68133)

### 7. [BUG] 工作流管理器遇到 HTTP 429 时无限重试，34 秒内烧掉 2M tokens
- **Issue #64328** · 4 条评论 · 1 👍 | 🔴 **CLOSED** (stale)
- **摘要**：97 个代理并行运行时触发速率限制，系统无限重试，导致大量 token 浪费和费用飙升。用户支出风险高。
- **链接**：[#64328](https://github.com/anthropics/claude-code/issues/64328)

### 8. [BUG] 桌面版 Cowork 远程设备文件桥反复断开
- **Issue #77385** · 3 条评论 · 1 👍 | 🟢 **OPEN**
- **摘要**：Claude 桌面应用 Cowork 模式下的远程设备文件桥（device_stage_files / device_bash）经常在操作中断开且无法自动恢复，影响协作体验。
- **链接**：[#77385](https://github.com/anthropics/claude-code/issues/77385)

### 9. [BUG] 自动压缩在无警告时触发，导致上下文边界意外执行
- **Issue #68097** · 3 条评论 · 1 👍 | 🔴 **CLOSED** (stale)
- **摘要**：自动压缩（compaction）在没有预压缩警告的情况下触发，导致 pending action 被错误重新执行，属于回归 bug（同一问题此前被错误关闭）。
- **链接**：[#68097](https://github.com/anthropics/claude-code/issues/68097)

### 10. [BUG] 代理错误回忆自身行为，生产事件后提供虚假描述
- **Issue #68183** · 2 条评论 · 0 👍 | 🔴 **CLOSED** (stale)
- **摘要**：代理在造成生产事故后，对其先前操作提供错误且自信的叙述，反复纠正后才承认，暴露了模型对历史行为记忆的不可靠性。
- **链接**：[#68183](https://github.com/anthropics/claude-code/issues/68183)

---

## 重要 PR 进展（全部 3 条）

### 1. 🔄 [OPEN] 从前端设计技能中移除“复古未来主义”推荐
- **PR #39043** · 作者：@t3dotgg
- **摘要**：简洁修改——“相信我这个建议”。未提供更多技术细节，可能涉及内部设计规范调整。
- **链接**：[#39043](https://github.com/anthropics/claude-code/pull/39043)

### 2. ✅ [CLOSED] 修复 hookify 插件的 Python 导入路径
- **PR #15727** · 作者：@ship9599
- **摘要**：修复 hookify 插件因 import 路径错误导致的 `No module named 'hookify'` 失败问题。将 `from hookify.core.config_loader` 改为正确路径。
- **链接**：[#15727](https://github.com/anthropics/claude-code/pull/15727)

### 3. ✅ [CLOSED] 重构：提取共享 GitHub API 客户端并添加测试
- **PR #49596** · 作者：@bsene
- **摘要**：将重复的 GitHub API 调用逻辑提取到独立的 `github-api.ts` 模块，并添加单元测试，提升代码可维护性。
- **链接**：[#49596](https://github.com/anthropics/claude-code/pull/49596)

---

## 功能需求趋势

从所有活跃讨论中，社区最关注的功能方向集中在以下五个方面：

| 方向 | 关键词 | 代表 Issue |
|------|--------|------------|
| **跨平台统一体验** | 桌面/移动/CLI 会话同步、设置共享 | #42050 (👍24) |
| **模型访问与计费透明度** | Fable 5 计费、配额限制、降级通知 | #79337, #68133, #68137 |
| **上下文窗口可见性** | 向模型暴露 session_id、token 使用量 | #36678 |
| **Project CLAUDE.md 执行力** | 规则遵循、长期会话中的一致性 | #62087 |
| **MCP 权限与稳定性** | 远程设备桥断开、审批设置不生效 | #77385, #64521 |

此外，桌面端键盘快捷键不兼容（如法国 AZERTY 键盘）和会话自动压缩缺乏预警也引发了一些讨论。

---

## 开发者关注点

- **Fable 5 模型稳定性成最大痛点**：多位用户报告在 Max 计划下被收费或无故不可用，部分用户因此丢失工作进度，情绪明显。
- **长期会话中的规则遵循问题**：即使 CLAUDE.md 规则已加载，Claude 在持续多轮交互后仍会偏离约定，开发者需频繁干预。
- **工具调用安全性担忧**：`settings.local.json` 无完整性保护（#62506），恶意进程可注入许可，导致未授权命令执行。
- **速率限制与成本失控**：并行代理遇到 429 时无限重试，token 消耗激增（#64328），用户期望更智能的重试策略和预算控制。
- **会话自动压缩行为不可预测**：缺乏预通知，压缩后可能触发错误动作，影响开发流程连续性（#68097）。
- **桌面端 Cowork 模式体验不佳**：远程文件桥频繁断开，协作场景受阻。

---

*日报由 AI 分析师根据 GitHub 公共数据生成，仅供参考。如需更深入分析，请查阅原始仓库。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 | 2026-07-26

---

## 今日速览

过去 24 小时内 Codex 发布了 4 个 Rust alpha 版本（v0.146.0-alpha.8 ~ .10.1），迭代节奏稳定。社区对**每周限速重置不确定**（#9508）和**项目排序失效**（#31836）的讨论热度居高不下，两个 Issue 均获得大量评论与用户共鸣。基础设施方面，多个 PR 围绕 exec-server 网络策略、远程连接追踪以及 skill 元数据传递进行了合入，开发者在持续打磨底层稳定性与可观测性。

---

## 版本发布

- **[rust-v0.146.0-alpha.10.1](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.10.1)** — 0.146.0-alpha.10.1  
- **[rust-v0.146.0-alpha.10](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.10)** — 0.146.0-alpha.10  
- **[rust-v0.146.0-alpha.9](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.9)** — 0.146.0-alpha.9  
- **[rust-v0.146.0-alpha.8](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.8)** — 0.146.0-alpha.8

> 注：以上发布均未附带详细变更日志，推测为持续集成中的版本号迭代。

---

## 社区热点 Issues

选取过去 24 小时内评论数/热度最高的 10 个 Issue，按影响力排序：

### 🥇 #9508 — 让周限速重置变得可预测  
**标签**: enhancement, rate-limits | **评论**: 47 | **点赞**: 32  
用户希望 Codex 能够固定每周限速重置的具体时刻（如固定到某个时区/时间），而不是“任意时间”重置。该需求从 v0.87.0 时期就已提出，至今仍是社区高优痛点之一。  
[查看详情](https://github.com/openai/codex/issues/9508)

### 🥇 #31836 — 项目排序“最后更新”仅对任务分组内生效，不改变项目顺序  
**标签**: bug, app | **评论**: 32 | **点赞**: 35  
macOS 桌面端 `Projects` 视图的排序控件无法真正改变项目列表顺序。用户期望按最后更新时间排列项目，但实际只对每个项目内的任务分组有效。  
[查看详情](https://github.com/openai/codex/issues/31836)

### 🥉 #4003 — Windows 上补丁文件混合换行符  
**标签**: bug, windows-os, tool-calls | **评论**: 29 | **点赞**: 72  
Codex 在 Windows 下修改文件时未遵循原文件的换行格式，导致混用 CRLF/LF。该问题影响面广（72 赞），是 Windows 用户长期反馈的痛点。  
[查看详情](https://github.com/openai/codex/issues/4003)

### #16423 — 对任意周限速重置的挫败感（已关闭）  
**标签**: enhancement, rate-limits | **评论**: 12 | **点赞**: 36  
用户详细描述了限速重置对其规划使用方式的影响，建议应基于周期而非“随机”重置。该 Issue 虽已关闭，但反映了与 #9508 相同的诉求。  
[查看详情](https://github.com/openai/codex/issues/16423)

### #35058 — Codex Diff 在 VS Code 中崩溃：“Oops, an error has occurred”  
**标签**: bug, extension | **评论**: 11 | **点赞**: 10  
macOS Apple Silicon + VS Code 1.128.0 环境下，打开 Codex Diff 选项卡直接报错。是新出现的高影响 bug。  
[查看详情](https://github.com/openai/codex/issues/35058)

### #31786 — Windows 远程控制至 Android 完全无法连接  
**标签**: bug, windows-os, app, connectivity, remote | **评论**: 11  
配对流程通过，但手机端一直显示“connecting”，无法建立远程会话。  
[查看详情](https://github.com/openai/codex/issues/31786)

### #31973 — Windows 远程控制永久卡在“Reconnecting...”，无法远程恢复  
**标签**: bug, windows-os, app, connectivity, remote | **评论**: 11  
与 #31786 同为远程控制模块的严重缺陷。  
[查看详情](https://github.com/openai/codex/issues/31973)

### #26379 — CLI 持久化错误的 tool_search_call 参数，恢复时返回 400 错误  
**标签**: bug, CLI, tool-calls, session | **评论**: 9  
在 WSL2 上使用 gpt-5.5 时，CLI 会写入过长的属性名，导致恢复会话报错。  
[查看详情](https://github.com/openai/codex/issues/26379)

### #32533 — Responses Lite：调整 reasoning effort 会导致大会话被“Request blocked”卡住  
**标签**: bug, CLI, context, connectivity | **评论**: 5  
用户从自定义分支发现，改变推理强度后请求被阻塞，直至会话压缩才恢复。  
[查看详情](https://github.com/openai/codex/issues/32533)

### #34471 — Computer Use 1.0.1000451 在 macOS 26 上无法加载 @oai/sky  
**标签**: bug, app, computer-use | **评论**: 5  
由于 `nodeRepl.env` 为空，Computer Use 插件无法启动，影响 Pro 用户。  
[查看详情](https://github.com/openai/codex/issues/34471)

---

## 重要 PR 进展

选取过去 24 小时内合并或开放的 10 个关键 PR：

### ✅ #35375 — 让 keymap 操作菜单自适应宽度（已合并）  
由 copyberry[bot] 提交。在终端宽度不足时自动将动作描述堆叠到标签下方，保持对齐。  
[查看详情](https://github.com/openai/codex/pull/35375)

### ✅ #35365 — 保持 unified mention 结果新鲜（已合并）  
重启文件搜索，避免复用陈旧状态。  
[查看详情](https://github.com/openai/codex/pull/35365)

### ✅ #35364 — 限制 Code Mode 元数据兼容头大小（已合并）  
防止 HTTP/WebSocket 头部无限制增长。  
[查看详情](https://github.com/openai/codex/pull/35364)

### ✅ #35363 — 在 completion 事件中添加项目开始时间（已合并）  
新增 `started_at_ms` 字段，向后兼容旧事件。  
[查看详情](https://github.com/openai/codex/pull/35363)

### ✅ #35359 — 在客户端处理 exec-server 网络策略请求（已合并）  
支持允许、拒绝、询问三种决策，并绑定并发回调。  
[查看详情](https://github.com/openai/codex/pull/35359)

### ✅ #31582 — 从 skills/list 暴露线程选择的 skill（已合并，已完成代码审查）  
返回线程当前可用的 skill，包括来自 executor 的 skill，并给出不可用环境的警告。  
[查看详情](https://github.com/openai/codex/pull/31582)

### ✅ #30228 — 通知客户端线程选择 skill 的变化（已合并，已完成代码审查）  
当 skill 可用性变化时推送信号，避免客户端缓存过期。  
[查看详情](https://github.com/openai/codex/pull/30228)

### ✅ #29845 — 在 Windows 启动器中传递显式应用程序路径（已合并，已完成代码审查）  
为 Windows unified-exec 解析管线打下基础，不改变命令解析行为。  
[查看详情](https://github.com/openai/codex/pull/29845)

### ✅ #35280 — 未配置允许列表时跳过插件 MCP 过滤（已合并）  
若所有插件需求均未指定 `mcp_servers`，则保留原样；显式空列表视为全部拒绝。  
[查看详情](https://github.com/openai/codex/pull/35280)

### ✅ #35275 — 追踪远程 exec-server 连接建立（已合并）  
在远程环境后台启动时保留 tracing span，覆盖连接、注册、Noise 握手等阶段。  
[查看详情](https://github.com/openai/codex/pull/35275)

---

## 功能需求趋势

综合过去 24 小时的 Issues，社区关注的功能方向集中在以下几点：

1. **限速与配额管理** — #9508、#16423、#35400 等大量讨论集中在“周限速重置不可预测”以及“credits 消耗过度”上，用户亟需透明的配额重置机制。
2. **远程控制可靠性** — #31786、#31973、#25164 均报告 Windows → Android 远程连接失败或卡死，这一功能在近期版本中稳定性明显不足。
3. **项目（Projects）排序与组织** — #31836、#33077 指出排序控件无效，用户希望按最后更新、名称等方式正确排列项目。
4. **Windows 兼容性** — #4003（换行符）、#29593（本地状态损坏）、#34299（页面闪烁）等持续暴露 Windows 桌面的质量问题。
5. **IDE 扩展稳定性** — #35058（Codex Diff 崩溃）、#35362（Review diff 崩溃）表明 VS Code 扩展在 macOS 和 Windows 上均存在渲染问题。
6. **Skill 与插件生态** — #13174、#21907 等要求支持外部 skill 仓库、项目级 skill 自动发现，社区对 skill 可扩展性有较高期待。

---

## 开发者关注点

从用户反馈和 Issue 描述中提炼出的高频痛点：

- **限速重置缺乏透明度**：用户依靠每周配额规划工作，但重置时间任意，导致计划被打乱（#9508、#16423）。
- **远程控制模块在 Windows 端几乎不可用**：配对、重连均存在严重缺陷，跨平台远程体验断裂（#31786、#31973）。
- **Windows 桌面应用频繁崩溃或状态损坏**：本地文件 `chat_processes.json` 被写为全 NUL 字节、Work 页面持续闪烁、Scheduled tasks 不同步（#29593、#34299、#35402）。
- **项目排序形同虚设**：排序控件无法真正改变项目顺序，降低组织效率（#31836、#33077）。
- **文件换行符未遵守平台约定**：尤其在 Windows 上，Codex 修改文件后混入 LF，破坏团队协作规范（#4003）。
- **credits 消耗与模型选择不匹配**：用户报告在 Plan 模式下执行 1 次操作消耗约 100 credits，疑似计费不准（#35400）。
- **Codex Diff 完全不可用**：VS Code 扩展中的 Diff 功能在 macOS 和 Windows 均报错，影响代码审查流程（#35058、#35362）。

---

*编辑注：数据截止 2026-07-25 23:59 UTC，覆盖 GitHub 仓库 `openai/codex` 过去 24 小时内更新的 Release、Issue 和 Pull Request。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 | 2026-07-26

数据来源：github.com/google-gemini/gemini-cli  
统计周期：2026-07-25 至 2026-07-26（按 UTC 更新）

---

## 今日速览

- **Agent 稳定性问题持续发酵**：多个高优先级 bug 集中在子代理（Subagent）错误报告成功、通用代理挂起等方向，社区反馈强烈，开发者已进入复现与修复阶段。
- **自动化记忆（Auto Memory）模块的缺陷与安全风险被系统性揭露**：涉及无限重试、日志泄露、补丁静默跳过等问题，团队计划进行大规模改进。
- **基础设施与 CI 稳健性提升**：PR 主要集中在修复 CI 发布流程（npm dist-tag 竞态）、OAuth 令牌刷新、shell 输出截断等影响日常使用体验的细节。

---

## 版本发布

过去 24 小时内无正式版本发布。社区可关注下文中提到的修复类 PR，预计近期将进入 Patch 版本。

---

## 社区热点 Issues

挑选了 10 个最值得关注的 Issue，涵盖 Bug、功能需求和影响范围较大的议题。

### 1. #22323 – 子代理达到最大轮次后错误报告为“GOAL 成功”
- **重要性**：高优先级（p1），直接导致用户误以为任务完成，实际分析未执行。
- **社区反应**：12 条评论，2 个赞。开发者已标记为需要重新测试。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/22323

### 2. #21409 – 通用代理（Generalist agent）挂起无响应
- **重要性**：p1，严重阻塞日常操作（如创建文件夹），用户被迫等待长达 1 小时。
- **社区反应**：8 条评论，8 个赞，是近期赞数最高的 bug。临时绕过方案：禁止代理使用子代理。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/21409

### 3. #24353 – 稳健的组件级评估（EPIC）
- **重要性**：涵盖行为评估测试的长期计划，已积累 76 个测试用例，影响 Agent 质量保障。
- **社区反应**：7 条评论，项目内部持续推动。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/24353

### 4. #25166 – Shell 命令执行后卡在“等待输入”
- **重要性**：p1，高频复现，极简命令（如 `ls`）也在完成后挂起，严重破坏交互体验。
- **社区反应**：4 条评论，3 个赞。开发团队标记为 effort/medium。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/25166

### 5. #26522 – Auto Memory 对低信号会话无限重试
- **重要性**：p2，导致后台进程资源浪费，且无法跳过无意义对话。
- **社区反应**：5 条评论，开发者已提出修复方案。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/26522

### 6. #26525 – Auto Memory 缺乏确定性脱敏和日志控制
- **重要性**：安全风险 – 敏感内容在脱敏前已进入模型上下文，且日志可能记录技能内容。
- **社区反应**：4 条评论，团队正在设计红黑树级别的补丁方案。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/26525

### 7. #28439 – 缺少 OAuth 认证提示
- **重要性**：影响首次启动体验，用户反馈运行 `gemini` 后只看到环境变量要求，未触发 OAuth 流程。
- **社区反应**：5 条评论，0 赞（新用户报障）。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/28439

### 8. #21983 – 浏览器子代理在 Wayland 下失败
- **重要性**：p1，影响 Linux Wayland 用户群体，终止原因显示 GOAL 但实际失败。
- **社区反应**：4 条评论，1 个赞。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/21983

### 9. #22672 – 代理应阻止破坏性行为（如 `git reset --force`）
- **重要性**：p2，用户期望代理在危险操作前进行确认或选择更安全的方法。
- **社区反应**：3 条评论，1 个赞，属于长期功能需求。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/22672

### 10. #22267 – 浏览器代理忽略 settings.json 中的 maxTurns 等配置
- **重要性**：p2，用户自定义配置不生效，导致无法限制浏览器代理行为。
- **社区反应**：3 条评论，标记为需要重新测试。
- **链接**：https://github.com/google-gemini/gemini-cli/issues/22267

---

## 重要 PR 进展

选择 10 个涵盖不同类型和影响范围的 PR。

### 1. #28535 – 修复性能测试中 ripgrep 路径解析
- **内容**：使用 `resolveRipgrepPath()` 替代已删除的 `canUseRipgrep()`，确保测试兼容当前 API。
- **状态**：OPEN，p1，size/s。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28535

### 2. #28534 – 修复 CI 中 nightly 发布后 dist-tag 移除竞态
- **内容**：添加 `scripts/remove-npm-dist-tag.sh` 并重试逻辑，解决 npm 发布确认延迟导致标签删除失败。
- **状态**：OPEN，p1，size/l。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28534

### 3. #28481 – 修复 MCP OAuth 令牌刷新时丢失客户端 ID
- **内容**：修复通过动态客户端注册配置的 OAuth 服务器无法刷新令牌的问题，之前刷新会删掉凭证强制重新授权。
- **状态**：OPEN，p1，size/m。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28481

### 4. #28401 – 限制 Shell 工具输出大小，防止 token 膨胀
- **内容**：为 `shell` 工具添加输出上限，避免大命令（如 `find /`）将数百 KB 内容注入模型上下文。
- **状态**：OPEN，p1，size/m。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28401

### 5. #28353 – 防止 A2A 服务器 restore 命令路径遍历
- **内容**：对调用者提供的参数进行归一化和合法性检查，防御性地阻止 `../../../etc/passwd` 这样的路径逃逸。
- **状态**：已合并（CLOSED），size/s。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28353

### 6. #28348 – 修复 MaxListenersExceededWarning 及 OAuth 无限循环
- **内容**：解决 API 重试时的事件监听器泄漏和 Windows 上 OAuth 成功后无限认证循环。
- **状态**：已合并（CLOSED），size/m。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28348

### 7. #28531 – 修复 Windows 上 diff 视图无高亮（CRLF→LF）
- **内容**：将 `getProposedContent` 中 CRLF 行尾统一转换为 LF，使 Gemini Code Assist 侧边 diff 正常显示更改。
- **状态**：OPEN，size/m。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28531

### 8. #28530 – 新增 Triage 评估框架（Caretaker Agent）
- **内容**：引入 LLM-as-a-Judge 评估流水线，支持并行 Git Worktree 基准测试运行。
- **状态**：OPEN，size/l。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28530

### 9. #28532 – 添加 Golden Issue 数据集收集与 Firestore 同步工具
- **内容**：为 Caretaker 评测提供本地+云端黄金测试用例管理能力。
- **状态**：OPEN，size/l。
- **链接**：https://github.com/google-gemini/gemini-cli/pull/28532

### 10. #28435 等四连 PR – 实现 Issue-to-PR 自动生成管道（SSR Pipeline）
- **内容**：连续提交了配置解析、Firestore 双锁、Antigravity 代理、Cloud Run 作业等模块，构建完整的自动化代码生成与提 PR 流水线。
- **状态**：OPEN，size/l ~ xl。
- **链接集合**：
  - https://github.com/google-gemini/gemini-cli/pull/28435
  - https://github.com/google-gemini/gemini-cli/pull/28433
  - https://github.com/google-gemini/gemini-cli/pull/28434
  - https://github.com/google-gemini/gemini-cli/pull/28432
  - https://github.com/google-gemini/gemini-cli/pull/28431

---

## 功能需求趋势

从近期 Issue 和 PR 中可以提炼出社区最关注的四个方向：

1. **Agent 行为可控性与自省能力**
   - 用户希望代理能准确了解自身能力（CLI flags、热键、子代理使用边界）并主动提供指导（#21432）。
   - 需要阻止破坏性操作（#22672），并要求子代理轨迹可通过 `/chat share` 分享（#22598）。

2. **自动记忆（Auto Memory）系统的健壮性与安全性**
   - 核心诉求：避免无限重试（#26522）、无脱敏风险（#26525）、处理无效补丁（#26523）、提升提取质量（#26516）。

3. **浏览器代理与 Wayland 兼容性**
   - Wayland 下浏览器子代理崩溃（#21983）以及忽略自定义配置（#22267）是 Linux 用户的突出痛点。

4. **终端体验优化**
   - 高优先级：修复 shell 命令执行后挂起（#25166）、终端缩放时的高性能刷新（#21924）、退出外部编辑器后的终端渲染错乱（#24935）。

---

## 开发者关注点

- **Agent 的“假成功”问题**：子代理达到最大轮次后报告 `GOAL` 成功，容易误导用户相信任务已完，实际未做任何分析。这是目前最影响信任度的 bug。
- **通用代理挂起**：即使简单的文件夹创建也会导致无限等待，且无超时机制。用户必须手动取消或主动禁止子代理才能工作。
- **Shell 命令输出无界**：大输出直接塞给模型，不仅烧 token 还导致模型响应变差。社区期待 #28401 快速合并。
- **OAuth 配置混乱**：新用户首次运行未获授权提示，且 MCP OAuth 令牌刷新会清空凭证，严重影响第三方工具集成体验。
- **系统资源与安全风险**：Auto Memory 无限重试、日志泄露、路径遍历漏洞等问题表明基础设施稳健性仍有提升空间。

> 所有链接均以 `https://github.com/google-gemini/gemini-cli` 为根路径，可直接拼接 issue/PR 编号访问。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 | 2026-07-26

## 📌 今日速览

过去24小时内，社区活跃度保持高位，共有18条 Issue 更新（其中6条新增）、2条 PR 关闭。最值得关注的是 **1.0.74 版本在恢复大 Session 时出现 OOM 回归**（#4251），以及 **Session 退出时静默重写 `settings.json` 导致配置丢失**（#4252），这两项 bug 直接影响长期用户的生产力。此外，插件市场注册不持久化（#4247）、`/rename` 在 VS Code 代理窗口中不可用（#4244）等新报问题也引发讨论。

## 🚀 版本发布

过去24小时内无新版本发布。当前最新版本为 1.0.75。

---

## 🔥 社区热点 Issues（精选10条）

### 1. [#4251 – 恢复大 Session 在 1.0.74 中 OOM / 单核 100% 约 70 分钟](https://github.com/github/copilot-cli/issues/4251)
- **标签**: `area:sessions`  
- **重要性**: 🔴 严重性能回归。1.0.73 下正常恢复的同一 Session 在 1.0.74 中峰值 RSS 飙升 3-4 倍，导致 OOM 或长时间卡死。
- **社区反应**: 用户通过 A/B 测试明确锁定版本，请求紧急修复。

### 2. [#4252 – Session 退出时将启动时的 `model` 写回 settings.json，静默覆盖用户编辑](https://github.com/github/copilot-cli/issues/4252)
- **标签**: `area:sessions`, `area:models`, `area:configuration`  
- **重要性**: 🔴 配置安全漏洞。若用户在会话期间手动修改了 `~/.copilot/settings.json`，退出会话会无提示地将其覆盖为启动时的旧值，导致自持 stale 默认配置。
- **社区反应**: 零评论但获关注，属于数据一致性问题，急需修复。

### 3. [#2205 – 终端渲染：鼠标滚动失效，改为滚动“输入历史”而非“输出历史”](https://github.com/github/copilot-cli/issues/2205)
- **标签**: `area:terminal-rendering`  
- **重要性**: 🟠 影响日常交互。自某版本后鼠标滚轮不再上下滚动 agent 输出内容，而是滚动发送给 agent 的输入（被认为无用）。用户 `--no-mouse` 后滚轮仍被禁用。
- **社区反应**: 13 条评论，14 个 👍，社区强烈要求恢复原有行为。

### 4. [#4241 – 密码掩码功能失灵：agent 读取含密码文件时额外消耗 token](https://github.com/github/copilot-cli/issues/4241)
- **标签**: `area:tools`  
- **重要性**: 🟠 安全与效率双重问题。密码掩码功能在 agent 读取文件时并未真正隐藏密码，反而迫使 agent 用 Python 读取底层字节导致误判密码错误，浪费大量 token。
- **社区反应**: 零评论，但问题描述清晰，影响常见场景。

### 5. [#4244 – 在 VS Code Agent 窗口中 `/rename` 不可用](https://github.com/github/copilot-cli/issues/4244)
- **标签**: `area:sessions`, `area:agents`  
- **重要性**: 🟠 IDE 集成缺口。`/rename` 命令在终端 CLI 中有效，但在 VS Code 的 Agents 窗口中无响应，且 agent 无法主动调用该命令。
- **社区反应**: 表明 Copilot CLI 与 VS Code 集成体验仍需对齐。

### 6. [#4246 – archive_session 超时 60 秒后留下孤立大 worktree](https://github.com/github/copilot-cli/issues/4246)
- **标签**: `area:sessions`  
- **重要性**: 🟠 资源泄漏。当 `archive_session` 因 worktree 清理超时后，会话和 worktree 无法恢复且占用磁盘空间，阻止会话分支复用。
- **社区反应**: 零评论，但问题会影响 CI 或长时间运行的会话。

### 7. [#4247 – 插件市场添加报告成功但未持久化](https://github.com/github/copilot-cli/issues/4247)
- **标签**: `area:plugins`  
- **重要性**: 🟠 插件生态基础功能异常。执行 `copilot plugin marketplace add` 后显示成功，但 `list` 命令立即找不到新注册的市场，验证后确认未写入磁盘。
- **社区反应**: 零评论，属于功能不可用级别。

### 8. [#4248 – `/pr` 命令无法识别使用 SSH 主机别名的仓库](https://github.com/github/copilot-cli/issues/4248)
- **标签**: 无官方标签  
- **重要性**: 🟡 使用门槛。许多开发者使用 SSH 别名（如 `github.com` 指向其他 host），此时 `/pr` 报错“需要连接到 GitHub remote”。
- **社区反应**: 影响面较广，需扩大 remote 检测逻辑。

### 9. [#4253 – `/ask` 频繁无结果返回](https://github.com/github/copilot-cli/issues/4253)
- **标签**: 无官方标签  
- **重要性**: 🟡 核心命令可靠性。`/ask` 执行后无输出无错误，在 1.0.75 版本中复现。
- **社区反应**: 零评论，用户等待根因分析。

### 10. [#4183 – 自动压缩无法防止 CAPI 5MB 请求体限制](https://github.com/github/copilot-cli/issues/4183)
- **标签**: `area:context-memory`, `area:models`  
- **重要性**: 🟡 长会话稳定性。即使上下文 token 未超限，序列化后的 CAPI 请求体可能突破独立的 5MB 限制，自动压缩对此无效。
- **社区反应**: 10 个 👍，社区期待更智能的上下文管理。

---

## 📬 重要 PR 进展（共2条）

### 1. [#23 – Create monad.yml（已关闭）](https://github.com/github/copilot-cli/pull/23)
- **状态**: 已关闭  
- **内容**: 涉及“design, mystic standards, technology”，疑似非功能性或实验性文件，无实际代码变更可审阅。
- **评析**: 与该仓库主要功能无关，可能为误提交。

### 2. [#4228 – 撤回：因作用域不对应 #3534（已关闭）](https://github.com/github/copilot-cli/pull/4228)
- **状态**: 已关闭  
- **内容**: 作者自行撤回，原意是修改文档但实际应为私有剪贴板运行时实现。源分支已删除。
- **评析**: 无此 PR 的实质内容，不产生变化。

> 注：过去24小时无活跃的 open PR，社区开发活动主要集中在 Bug 报告上。

---

## 📊 功能需求趋势

从近期 Issue 中提炼出社区最关注的功能方向：

| 方向 | 代表性 Issue | 关注度 |
|------|--------------|--------|
| **会话管理与持久化** | #4251（OOM回归）、#4252（设置被覆盖）、#4246（超时孤立）、#4249（计划指示器泄漏） | 极高 |
| **IDE 集成（VS Code）** | #4244（/rename不可用）、#17（扩展高亮diff） | 高 |
| **终端交互体验** | #2205（鼠标滚动改进）、#4202（猜测）类 | 高 |
| **插件生态可靠性** | #4247（添加不持久化）、#1996（marketplace.json校验失败） | 中 |
| **密码/敏感信息处理** | #4241（掩码失效） | 中 |
| **SSH 别名支持** | #4248（/pr 无法识别） | 中 |
| **命令稳定性** | #4253（/ask 无结果） | 中 |
| **大规模技能管理** | #1464（超过32个技能不可达） | 低 |

---

## 🛠️ 开发者关注点

1. **1.0.74 版本性能回归**：大 Session 恢复耗时和内存消耗异常（#4251），部分用户被迫锁定 1.0.73。
2. **配置被静默覆盖**：Session 退出时自动写回 `settings.json`（#4252），极易导致用户手动修改丢失，需立即设计读写分离或提示机制。
3. **密码掩码的副作用**：不仅未真正隐藏密码，反而因 agent 的绕行操作增加 token 消耗和逻辑错误（#4241），该功能需要重新设计。
4. **插件市场基本流程断裂**：`add` 返回成功但未写入磁盘（#4247），从根本上阻塞了第三方插件安装流程。
5. **Session 清理超时与资源泄漏**：`archive_session` 超时后无恢复手段（#4246），可能导致 CI 环境磁盘爆满。
6. **SSH remote 检测局限**：使用 GitHub 别名或其他 SSH 配置的用户无法使用 `/pr` 命令（#4248），暴露了 remote 解析的单一性。
7. **`/ask` 命令间歇性失效**：无错误输出的静默失败（#4253）最影响信任感，用户期待增加错误提示或重试逻辑。

---

*数据来源：github.com/github/copilot-cli · 统计截至 2026-07-25 UTC+0*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 | 2026-07-26

## 今日速览
过去24小时社区保持活跃：2个Issue更新、4个PR合并或提交。其中**死循环Bug（#2557）** 为新报告，可能影响会话稳定性；远程控制功能请求（#1282）获得16个👍，社区呼声较高。PR方面，核心贡献者@Nas01010101集中修复了会话恢复、上传持久化和上下文截断三个问题，测试兼容性改进也已提交。

## 社区热点 Issues

### 1. [#1282 [enhancement] Feature Request: Remote Control](https://github.com/MoonshotAI/kimi-cli/issues/1282)
- **标签**：enhancement
- **作者**：@CatKang | 创建于2026-02-27 | 更新于2026-07-25
- **👍 16** | **评论 8**
- **摘要**：希望增加**远程控制**功能，允许用户从手机、平板或浏览器继续本地的Kimi Code CLI会话，实现工作流无缝衔接。
- **为什么重要**：代表开发者对**跨设备持续工作**的强烈需求，点赞数高表明关注度持续上升。

### 2. [#2557 [bug] Dead Loop](https://github.com/MoonshotAI/kimi-cli/issues/2557)
- **标签**：bug
- **作者**：@zxpdemonio | 创建并更新于2026-07-25
- **👍 0** | **评论 0**
- **摘要**：运行 `kimi-cli 1.44.0` 时出现**死循环**，使用Kimi Code订阅（Moonshot AI提供的编程助手订阅）。未提供更多详细信息。
- **为什么重要**：死循环直接导致工具不可用，属于严重稳定性问题。虽无评论，但需关注复现条件和修复进度。

## 重要 PR 进展

### 1. [#2520 fix(session): align fork/undo context truncation to wire turns](https://github.com/MoonshotAI/kimi-cli/pull/2520)
- **状态**：已合并（CLOSED）
- **作者**：@Nas01010101 | 更新于2026-07-25
- **摘要**：修复 #2517，同时解决 #1974（斜杠指令导致undo截断偏移）和 #2049（fork/undo后历史不匹配）的根因。改进fork/undo时上下文截断逻辑，使其与wire turns对齐。

### 2. [#2519 fix(app): refresh stale frozen system prompt on session resume](https://github.com/MoonshotAI/kimi-cli/pull/2519)
- **状态**：已合并（CLOSED）
- **作者**：@Nas01010101 | 更新于2026-07-25
- **摘要**：修复 #2420。会话恢复时无条件采用冻结的 `_system_prompt`，导致新添加的skills、`AGENTS.md`编辑不会生效。PR刷新system prompt，使其在恢复时重新读取用户配置。

### 3. [#2518 fix(web): persist uploads .sent marker so restarts do not re-send files](https://github.com/MoonshotAI/kimi-cli/pull/2518)
- **状态**：已合并（CLOSED）
- **作者**：@Nas01010101 | 更新于2026-07-25
- **摘要**：修复 #2413。`kimi web` 在服务重启后会重复发送之前上传的文件（包括图片），污染会话。PR持久化 `.sent` 标记，避免重复发送。

### 4. [#2558 fix(tests): improve Windows cross-platform test compatibility](https://github.com/MoonshotAI/kimi-cli/pull/2558)
- **状态**：开放（OPEN）
- **作者**：@panandicoding | 更新于2026-07-25
- **摘要**：修复两个Windows测试兼容性问题：`test_background_tools.py` 中 `Path.write_text()` 未指定 `newline=""` 导致行尾转换；另一个问题（PR描述未完整显示）。改进跨平台测试可靠性。

## 功能需求趋势
基于本次数据看，社区对**跨设备远程控制**（#1282）表现出浓厚兴趣，暗示用户期望更灵活的工作模式。此外，**稳定性**（死循环、session恢复、文件重发）是当前修复重点，而非新功能主导。

## 开发者关注点
- **会话恢复一致性**：#2519 解决skills和`AGENTS.md`编辑在恢复后失效的问题，表明用户对自定义配置持久化有高要求。
- **上传文件重复发送**：#2518 修复 `kimi web` 重启后图片重复发送的污染问题，反映Web模式下交互体验的痛点。
- **Windows测试兼容性**：#2558 显示有开发者在推进跨平台支持，但Windows端仍有测试环境差异需解决。
- **死循环Bug**：#2557 虽无详细报告，但直接导致工具不可用，需密切关注官方响应。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

好的，作为专注于 AI 开发工具的技术分析师，以下是基于您提供的 GitHub 数据生成的 2026-07-26 日《OpenCode 社区动态日报》。

---

## OpenCode 社区动态日报 - 2026-07-26

### 今日速览

OpenCode 社区在过去 24 小时内异常活跃。最值得关注的是，一个因默认配置不安全导致的 **严重安全漏洞** 被曝光（#38857），用户服务器已被用于部署挖矿程序。此外，社区围绕新版本 UI 与旧版布局的争议持续发酵，#37012 号“保留旧版布局”的请求获得了极高讨论度，反映了部分用户对重大界面改动的抗拒。同时，近期桌面版 v1.18.5 更新带来了多个 Bug，如项目加载错误和进程挂起，影响了用户体验。

---

### 版本发布

**无**

过去 24 小时内无版本发布。

---

### 社区热点 Issues

1.  **【安全】`opencode web` 服务器因默认配置致服务器被植入挖矿程序 #38857**
    *   **链接**: [https://github.com/anomalyco/opencode/issues/38857](https://github.com/anomalyco/opencode/issues/38857)
    *   **重要性**: **极高**。这是一起严重的安全事件。报告者证明，由于 `opencode web` 服务器默认监听 `0.0.0.0:4096` 且未要求设置 `OPENCODE_SERVER_PASSWORD`，导致攻击者可通过未认证的 bash 终端在用户服务器上部署 Monero (XMRig) 挖矿程序。这标志着从潜在风险到实际破坏的转变，社区迫切要求默认启用认证并添加访问日志。

2.  **【争议】请求保留旧版布局选项 #37012**
    *   **链接**: [https://github.com/anomalyco/opencode/issues/37012](https://github.com/anomalyco/opencode/issues/37012)
    *   **重要性**: **高**。该 Issue 获得了 33 条评论和 31 个赞，是社区内目前最热门的话题。用户强烈要求保留旧版布局，认为其交互更直接、功能访问更方便。这反映了新版本 UI 改变可能影响了核心用户的工作流，是 UX 设计的重大预警。

3.  **【服务宕机】多款 OpenCode 托管模型持续报错“内部服务器错误” #38874**
    *   **链接**: [https://github.com/anomalyco/opencode/issues/38874](https://github.com/anomalyco/opencode/issues/38874)
    *   **重要性**: **高**。报告称从 UTC 时间 7月25日15:53起，包括免费和 Go 订阅在内的多个 OpenCode 托管模型均出现 500、超时或不可用错误。这直接导致用户无法使用核心功能，可能是一次大规模服务故障或变更，官方急需回应。

4.  **【Bug】桌面版 v1.18.5 更新后项目加载报错 #38789**
    *   **链接**: [https://github.com/anomalyco/opencode/issues/38789](https://github.com/anomalyco/opencode/issues/38789)
    *   **重要性**: **高**。用户报告在更新到桌面版 v1.18.5 后，应用启动时因 “UnsupportedContentType” 错误无法加载当前工作区。此问题直接影响了所有更新到此版本并重启应用的开发者，是一个严重的发布质量问题。

5.  **【Bug】桌面版在 Windows 11 关闭项目时冻结 #38885**
    *   **链接**: [https://github.com/anomalyco/opencode/issues/38885](https://github.com/anomalyco/opencode/issues/38885)
    *   **重要性**: **中**。报告指出，在 Windows 11 上，每当用户尝试从项目列表关闭一个项目时，桌面版应用会直接冻结。即使进行全新安装后问题依然存在，表明这是一个与系统或状态管理相关的深层 Bug，严重影响了 Windows 平台用户的日常使用。

6.  **【Bug】TUI 输入框按回车后无响应 #31217**
    *   **链接**: [https://github.com/anomalyco/opencode/issues/31217](https://github.com/anomalyco/opencode/issues/31217)
    *   **重要性**: **中**。这是一个在终端用户界面（TUI）中的严重交互 Bug。输入提示后按回车，输入内容消失但消息未提交。这会严重困扰依赖 TUI 进行高效操作的用户，且影响中英文输入。

7.  **【Bug】`@` 文件引用无法找到新创建的文件 #32747**
    *   **链接**: [https://github.com/anomalyco/opencode/issues/32747](https://github.com/anomalyco/opencode/issues/32747)
    *   **重要性**: **中**。`@` 文件引用功能无法索引启动后创建的新文件，必须重启后才能使用。这破坏了开发中的即时引用体验，是会话能力的一个关键缺陷，可能影响编码效率。

8.  **【Bug】macOS 下无法连接局域网内的 Ollama 服务 #38854**
    *   **链接**: [https://github.com/anomalyco/opencode/issues/38854](https://github.com/anomalyco/opencode/issues/38854)
    *   **重要性**: **中**。用户试图用 OpenCode 连接 LAN 内的 Ollama 服务器失败，但 `curl` 命令可以正常连接。这限制了用户在本地或局域网部署私有模型的能力，影响了开源和自定义模型生态的发展。

9.  **【Feature】历史会话导入后可能导致无限循环 Bug #38791**
    *   **链接**: [https://github.com/anomalyco/opencode/issues/38791](https://github.com/anomalyco/opencode/issues/38791)
    *   **重要性**: **中**。技术分析指出，由于 `runLoop` 依赖消息 ID 的字符串排序来判断对话轮次，导入的非 OpenCode 原生会话可能导致死循环。这暴露了会话导入功能的不成熟，很可能导致托管服务因持续请求而产生高额费用或直接中断。

10. **【Bug】桌面 UI 新界面不直观 #38875**
    *   **链接**: [https://github.com/anomalyco/opencode/issues/38875](https://github.com/anomalyco/opencode/issues/38875)
    *   **重要性**: **低**。反馈明确提出“新 UI 有点不直观”。虽然没有详细说明，但这与 #37012 的呼声相互印证，表明当前版本的 UI 更改并未得到所有用户的认可，UI/UX 优化是当务之急。

---

### 重要 PR 进展

1.  **修复：权限提示中显示真实的上下文标题 #33950**
    *   **链接**: [https://github.com/anomalyco/opencode/pull/33950](https://github.com/anomalyco/opencode/pull/33950)
    *   **重要性**: 提升透明度和可用性。修复了 ACP（自动化代码流程）权限提示只显示工具类型（如“bash”）而非具体请求内容（如“删除文件”）的问题，使用户能更清楚地了解 AI 将要执行的操作。

2.  **修复：TUI 格式化显示中避免出现 “1000.0K” 的问题 #33948**
    *   **链接**: [https://github.com/anomalyco/opencode/pull/33948](https://github.com/anomalyco/opencode/pull/33948)
    *   **重要性**: 提升 UI 细节。修复了当数值恰好为100万时，TUI 错误地显示为“1000.0K”而非“1.0M”的格式化 Bug，体现了对产品细节的打磨。

3.  **新功能：增加 Solidity 语言支持和语法高亮 #38200**
    *   **链接**: [https://github.com/anomalyco/opencode/pull/38200](https://github.com/anomalyco/opencode/pull/38200)
    *   **重要性**: 扩大开发语言支持。为区块链开发者带来了原生支持，使 OpenCode 能更好地理解和生成 Solidity 代码，增强了其在 Web3 领域的实用性。

4.  **修复：恢复会话时间线滚动位置 #33943**
    *   **链接**: [https://github.com/anomalyco/opencode/pull/33943](https://github.com/anomalyco/opencode/pull/33943)
    *   **重要性**: 修复了长期存在的用户体验问题。使得用户在切换标签页或重新加载后，能自动回到之前浏览的消息位置，避免了每次都需要手动滚动的烦恼。

5.  **修复：防止 VCS 在仓库有海量未跟踪文件时崩溃 #33927**
    *   **链接**: [https://github.com/anomalyco/opencode/pull/33927](https://github.com/anomalyco/opencode/pull/33927)
    *   **重要性**: 提升稳定性。修复了当 Git 仓库中存在大量未跟踪文件（如 `node_modules` 或构建产物）时，应用直接崩溃的问题。这对处理大型项目至关重要。

6.  **修复：升级检查时对 GitHub 发行版进行认证 #33912**
    *   **链接**: [https://github.com/anomalyco/opencode/pull/33912](https://github.com/anomalyco/opencode/pull/33912)
    *   **重要性**: 修复自动化流程。解决了在离线环境或受限网络中，`opencode upgrade` 命令因未携带 `GITHUB_TOKEN` 而被 GitHub API 限速，导致无法检查更新的问题。

7.  **修复：移动端 Web 界面保留换行符 #33907**
    *   **链接**: [https://github.com/anomalyco/opencode/pull/33907](https://github.com/anomalyco/opencode/pull/33907)
    *   **重要性**: 改进移动端体验。修复了移动端 Web 输入框无法输入换行的 Bug，使手机用户在编写长提示或多段消息时更加方便。

8.  **修复：TUI 中忽略孤立的斜杠命令 #33904**
    *   **链接**: [https://github.com/anomalyco/opencode/pull/33904](https://github.com/anomalyco/opencode/pull/33904)
    *   **重要性**: 修复交互 Bug。当用户输入一个孤立的 `/` 时，会触发命令补全；直接按回车会错误地提交 `/agents` 命令。此 PR 修正了这一误操作，提升了 TUI 的鲁棒性。

9.  **新功能：实现 VCS 后端提交基础（第一阶段） #33900**
    *   **链接**: [https://github.com/anomalyco/opencode/pull/33900](https://github.com/anomalyco/opencode/pull/33900)
    *   **重要性**: 迈向重要功能的第一步。引入了新的后端 `/vcs/commit` 接口，为即将到来的“Git 源代码控制面板”功能奠定基础，这是一个社区呼声很高的功能。

10. **修复：确保 OpenAI 兼容接口返回非空内容 #33899**
    *   **链接**: [https://github.com/anomalyco/opencode/pull/33899](https://github.com/anomalyco/opencode/pull/33899)
    *   **重要性**: 提升兼容性和稳定性。一些第三方 API（如 GLM）在处理 AI SDK 发出的空字符串内容时会报错。此 PR 修正了这个问题，确保了对更多第三方模型的兼容性。

---

### 功能需求趋势

*   **UI/UX 稳定性与选择权**: 这是当前最强烈的呼声。围绕 #37012 和 #38875 的讨论表明，社区并非反对所有改变，但强烈要求提供 **保留旧版布局的选项**，避免强制更新带来的学习成本和工作流中断。
*   **订阅与服务透明度**: 用户对“免费额度”规则与“Go”订阅服务的模型托管方式存在疑问（#24649, #38869）。核心需求是 **清晰区分自托管模型与代理模型**，并希望计费和额度策略更加透明和合理。
*   **企业级功能支持**: 来自中文社区的需求 #20252（年费套餐+开发票）再次出现，显示了企业用户对 **便捷的采购和报销流程** 的需求，是商业化的关键一步。
*   **本地与开源模型生态**: #38854 连接局域网 Ollama 的问题反映了 **深度支持本地模型** 的重要性。用户希望 OpenCode 能成为连接各类模型（包括自部署）的通用桥梁。
*   **基础体验改善**: 来自 #38884 和 #38876 的需求表明，用户对 **字体大小调节** 和长对话中的 **快速回到顶部** 等基础 UI 功能仍有需求，基础体验的打磨不能松懈。

---

### 开发者关注点

*   **安全担忧加剧**: `opencode web` 服务器被用于挖矿的案例（#38857）引发了开发者对自托管服务 **默认安全配置** 的严重担忧。核心需求是：默认启用密码、禁止监听 `0.0.0.0`、并添加访问日志。
*   **更新稳定性成疑**: 桌面版 v1.18.5 带来的多个挂起和加载错误（#38789, #38885），让开发者对 **快速发布节奏下的质量保证** 产生怀疑。社区希望加强更新前的测试，并提供更顺畅的回滚机制。
*   **性能问题普遍存在**: CLI 命令因数据库过大启动缓慢（#38837），以及 `opencode2 serve` 进程长期运行后的内存泄漏（#36677），表明 **应用性能和资源占用** 已成为困扰社区开发者的普遍痛点，需要持续优化。
*   **跨平台兼容性攻坚**: Windows（#34442 离线安装、#38885 项目关闭冻结、#37096 WSL 集成问题）、macOS（#38854 Ollama 连接）、Android（#38850 粘贴问题）等多个平台均出现特有 Bug。用户要求 **针对不同平台进行全面的测试与适配**。
*   **对复杂操作鲁棒性不足**: 从历史会话导入死循环（#38791）到分代理流错误导致任务静默结束（#38866），再到 VCS 因大量未跟踪文件崩溃（#33927 MR），都指向一个核心问题：OpenCode 在处理非标准、边界情况或异常数据流时，健壮性有待大幅提升。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-07-26

---

## 📋 今日速览

昨夜发布了 **v0.21.0-nightly.20260725** 夜版，主要修复了 CLI 中洞察时间显示时区问题以及 autofix 模块的持续重构。 Issue 方面，**多行回复被终端裁切**（#5800）与 **Unity MCP 连接失败**（#7697）仍为社区最关注的高优先级 bug；与此同时，**子智能体模型等级选择**（#7685）、**pinned 只读记忆目录**（#6801）等新功能提案讨论热烈。PR 方面，**Goal v3 工作工具**（#7729）和 **WebUI 频道管理钩子**（#7728）等大型功能合并持续推进。

---

## 🚀 版本发布

### v0.21.0-nightly.20260725.1183a4c82

**发布说明**：  
- `fix(cli): measure insight days and hours in local time everywhere` — 修复 CLI 洞察功能中天数/小时以本地时间显示的问题。  
- `refactor(autofix): ext` — 对 autofix 模块进行扩展性重构。

> 详细变更参见 [Release 页面](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.0-nightly.20260725.1183a4c82)

---

## 🔥 社区热点 Issues（Top 10）

| 编号 | 标题 | 标签 | 讨论热度 | 为何重要 |
|------|------|------|----------|----------|
| [#5800](https://github.com/QwenLM/qwen-code/issues/5800) | bug(cli): 默认静态模式下终端超长回复最后一行被覆盖 | `P2`, `bug`, `ui`, `welcome-pr` | 8 comments | 影响所有 TUI 用户的阅读体验，上游依赖 Ink #973，社区已讨论一年多仍未完全解决。 |
| [#7697](https://github.com/QwenLM/qwen-code/issues/7697) | VS Code 扩展无法连接 Unity MCP，而 Claude Code 可以 | `bug`, `integration`, `mcp`, `vscode` | 4 comments | 标志性的 MCP 兼容性问题，阻碍游戏开发者使用 Qwen Code 替换 Claude Code。 |
| [#7665](https://github.com/QwenLM/qwen-code/issues/7665) | 桌面版持续报错 520/522 | `P3`, `bug`, `integration`, `need-information` | 5 comments | 刚安装即无法使用，用户反馈强烈但信息不足，需维护者进一步定位。 |
| [#7684](https://github.com/QwenLM/qwen-code/issues/7684) | Command 模式下多行状态栏导致输入法候选框偏移 | `P2`, `bug`, `ui`, `macos`, `welcome-pr` | 5 comments | macOS 中文用户高频痛点，影响编码效率。 |
| [#7685](https://github.com/QwenLM/qwen-code/issues/7685) | 子智能体生成时支持模型等级选择 | `P3`, `feature-request`, `subagents` | 4 comments | 社区期待更强的子智能体控制能力，已有对应 PR #7702 跟进。 |
| [#7719](https://github.com/QwenLM/qwen-code/issues/7719) | CLI 不显示 token 用量及百分比 | `P3`, `feature-request`, `ui` | 3 comments | 用户无法监控配额消耗，对 API 按量付费用户尤为重要。 |
| [#6801](https://github.com/QwenLM/qwen-code/issues/6801) | pinned/ 只读记忆目录，防止 /dream 合并 | `P2`, `feature-request`, `memory` | 3 comments | 内存系统增强方向，用户希望保护关键记忆不被自动压缩。 |
| [#7717](https://github.com/QwenLM/qwen-code/issues/7717) | 连续提及多个 skill 时自动补全失效 | `P2`, `bug`, `interactive`, `welcome-pr`, `ready-for-agent` | 2 comments | 影响多 skill 工作流，已标记为 agent 可处理。 |
| [#7712](https://github.com/QwenLM/qwen-code/issues/7712) | 主分支 E2E 测试失败 | `bug`, `ready-for-agent`, `autofix/skip` | 2 comments | CI 红障，直接影响开发者合并代码信心，自动标记待处理。 |
| [#7700](https://github.com/QwenLM/qwen-code/issues/7700) | 定义显式的、保留源码的数学编写契约 | `feature-request`, `rendering`, `markdown`, `need-discussion` | 3 comments | 数学/科学计算用户对 LaTeX 解析一致性的强烈需求，关联 PR #3680 和 #7699。 |

> 标注 `welcome-pr` 的 issue 欢迎社区直接贡献代码，`ready-for-agent` 表示已准备好让 AI agent 自动修复。

---

## 🔧 重要 PR 进展（Top 10）

| 链接 | 标题 | 状态 | 核心价值 |
|------|------|------|----------|
| [#7729](https://github.com/QwenLM/qwen-code/pull/7729) | feat(core): add Goal v3 worker tools | OPEN | 引入 Goal v3 工作工具，支持读取当前目标快照、证据目录和验证器反馈，是增强长期任务规划的重要基础设施。 |
| [#7728](https://github.com/QwenLM/qwen-code/pull/7728) | feat(webui): add workspace Channel management hook | OPEN | 为 WebUI 添加工作区频道管理数据层，支持频道目录加载、启动/停止、配对请求审批等，完善远程协作功能。 |
| [#7710](https://github.com/QwenLM/qwen-code/pull/7710) | feat(triage): add sandboxed /verify deep-verification lane | OPEN | 新增 `@qwen-code /verify` 注释驱动的深度验证通道，自动执行 A/B 负载测试、空检验证等，提升 PR 审查质量。 |
| [#7702](https://github.com/QwenLM/qwen-code/pull/7702) | feat(core): add model grade selection for subagent spawn | OPEN | 实现 #7685 提议的子智能体模型等级选择，用户可在 settings 中配置 `agents.modelGrades`，PR 与 issue 联动，社区高度关注。 |
| [#7203](https://github.com/QwenLM/qwen-code/pull/7203) | fix(core): fall back to system rg when bundled ripgrep cannot run | CLOSED | 解决 ripgrep 在 arm64/64K 页面系统上的兼容性问题（#2676），回退到系统 rg，修复多位用户困扰。 |
| [#7245](https://github.com/QwenLM/qwen-code/pull/7245) | fix(core): prevent updates to extension-provided agents | CLOSED | 修复扩展提供的子智能体可被意外修改的 bug（#7242），增强扩展安全隔离。 |
| [#7357](https://github.com/QwenLM/qwen-code/pull/7357) | feat(skills): add overridable default-disabled state | CLOSED | 实现 #7347 的 skill 默认禁用覆盖机制，允许项目/用户级设置灵活控制 skill 可用性。 |
| [#7724](https://github.com/QwenLM/qwen-code/pull/7724) | fix(web-shell): allow shell commands in new tasks without a session | OPEN | 改善 Web Shell 中新任务直接执行 `!` 命令的体验，懒创建会话，避免用户困惑。 |
| [#7725](https://github.com/QwenLM/qwen-code/pull/7725) | fix(ci): deflake tool-control E2E and add autofix flake detection | OPEN | 将 5 个易搓的 E2E 测试迁移到 fake-openai-server 确定性运行，并添加搓测自动检测，提升 CI 稳定性。 |
| [#7535](https://github.com/QwenLM/qwen-code/pull/7535) | fix(scripts): retry model calls and surface degraded release notes | OPEN | 稳定版发布说明生成器增加模型调用重试机制，并在降级时显式告警，防止静默失败。 |

---

## 📊 功能需求趋势

1. **子智能体与多 Agent 协作**：`模型等级选择`（#7685）、`agent tool model 参数` 等提案表明社区正推动更精细的子智能体调度和资源配置能力。
2. **UI/UX 体验增强**：Token 用量显示（#7719）、数学公式渲染契约（#7700）、输入法候选框修正（#7684）等高频需求集中出现，反映出用户对终端交互质量和透明度的期待。
3. **记忆与上下文管理**：`pinned/` 只读内存目录（#6801）和外部上下文提供者（#7585）显示社区希望更可控、更持久的知识存储机制。
4. **消息通道与集成**：Channel 管理钩子（#7728）、MCP OAuth 重定向文档（#7503）、微信/QQ 通道修复（#7721, #7726）表明远程协作和多平台集成仍是重点演进方向。
5. **质量与可靠性**：E2E 测试祛燥（#7725）、退化监控（#7535）、CI 失败自动标记（#7712）等表明开发者开始重视基础设施稳定性。

---

## 🧐 开发者关注点

- **兼容性痛点**：桌面版 520/522 错误（#7665）和 Unity MCP 连接失败（#7697）反映了新版本与外部服务/环境的兼容测试不足；arm64 上的 ripgrep 问题曾长期存在（#2676），虽已修复但提醒需加强多架构回归。
- **终端渲染缺陷高重复**：#5800（回复截断）和 #7713（输入滚动偏移）均属于 terminal 高度计算偏差导致的渲染 bug，用户多次反馈后维护者仍在排查。
- **扩展机制安全边界**：扩展提供的子智能体可被修改（#7242）提示当前扩展沙箱尚不完善，社区要求更严格的安全隔离和只读保护。
- **配置与热重载需求**：技能禁用硬锁定（#7347）、重试延迟不可配置（#7658）等展示用户希望更灵活的运行时设置而不必修改代码或重启。
- **中文用户特殊问题**：macOS 输入法候选框偏移（#7684）和微信频道账号凭据权限（#7726）表明本地化场景下的细节仍需打磨。

---

> 📌 以上日报基于 `2026-07-25 23:59 UTC` 数据生成，部分 Issue 和 PR 可能在您阅读时已有更新。欢迎通过 GitHub 链接查看最新讨论和代码变更。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*