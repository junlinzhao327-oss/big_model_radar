# AI CLI 工具社区动态日报 2026-07-23

> 生成时间: 2026-07-22 23:27 UTC | 覆盖工具: 7 个

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

好的，作为一名专注于 AI 开发工具生态的资深技术分析师，我已根据您提供的 2026-07-23 各主流 AI CLI 工具的社区动态，为您呈上这份横向对比分析报告。

---

### AI CLI 工具生态横向对比分析报告 (2026-07-23)

#### **1. 生态全景**

当前 AI CLI 工具市场已进入 **“内卷式”竞争与深度专业化并存的快速迭代阶段**。各家工具的核心功能（代码生成、上下文管理、子代理模式）已趋于同质化，**竞争焦点正从“能用”转向“好用、可靠、可扩展”**。社区反馈表明，用户对**平台稳定性（尤其是 Windows 环境）、安全性与权限控制、以及资源消耗（Token、CPU、磁盘）的透明度与优化**的关注度空前高涨。同时，围绕 MCP 协议和插件的扩展生态正成为构建工具护城河的关键战场，社区贡献活跃，但官方缺乏统一规范也带来了兼容性挑战。

#### **2. 各工具活跃度对比**

| 工具 | 热点 Issues (精选) | 重要 PR (进展中/已合并) | 版本发布 | 核心关注点摘要 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 10 条 (1 个新增, 9 个持续高热度) | 9 条 | 1 个正式版 | 权限模型混乱、模型安全误报、插件生态兴起 |
| **OpenAI Codex** | 10 条 (Windows/WSL 问题占主导) | 10 条 | 4 个 Alpha 版 | **Windows/WSL 性能兼容性**、子代理资源泄漏、配额机制 |
| **Gemini CLI** | 10 条 (Agent 行为可靠性为焦点) | 10 条 | 1 个预览版+1 个稳定版+1 个 Nightly | 子代理误报“成功”、安全性 (RCE 修复)、Agent 自主性 |
| **GitHub Copilot CLI** | 10 条 (回归类 Bug 集中出现) | 1 条 | 3 个补丁版 | **MCP 连接异常、BYOK 认证回归**、Windows 稳定性 |
| **Kimi Code CLI** | 3 条 | 2 条 | 无 | MCP 工具 Schema 兼容性、Windows 中文编码 Bug |
| **OpenCode** | 10 条 (服务故障占 5 条) | 10 条 | 无 | **Go 订阅服务大规模 401 故障**、CPU 空转、功能回归 |
| **Qwen Code** | 10 条 (核心测试 CI 红色，影响面广) | 10 条 | 1 个预览版+1 个 Nightly | **核心 CI 持续失败**、更新检查失败、模型推理兼容性 |

*注：活跃度主要基于过去24小时内社区反馈的数量和质量，以及版本迭代频率。*

#### **3. 共同关注的功能方向**

1.  **安全性与误报（All Tools）**：几乎所有工具社区都对安全审查系统提出了强烈质疑。**Claude Code (Fable 5)**、**OpenAI Codex**、**Gemini CLI** 都报告了大量合法操作（安全审计、防御测试、日常 DevOps）被错误拦截或导致模型降级。这表明当前基于规则或单一模型的安全策略过于僵化，**社区普遍呼唤更智能、可配置、且对合法工作流友好的安全模型**。

2.  **子代理/Agent 行为可靠性（Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI）**：**子代理误报任务成功**（Gemini CLI #22323）、**无故卡死**（Gemini CLI #21409）、**资源泄漏**（OpenAI Codex #34202）、**任务隔离失败**（Claude Code #79722）等问题频发。用户希望 Agent 的行为更加可预测、可控，并能够提供更透明的状态报告。

3.  **跨平台体验一致性（OpenAI Codex, Claude Code, Kimi Code CLI, GitHub Copilot CLI）**：**Windows 平台是重灾区**。OpenAI Codex 的 WSL 集成、Claude Code 的权限模型、Kimi Code 的中文编码崩溃、Copilot CLI 的渲染冻结，都反映了当前工具普遍“重 Linux/macOS，轻 Windows”的现状。这严重阻碍了 Windows 开发者群体的采纳。

4.  **MCP 与插件生态标准化（Kimi Code CLI, GitHub Copilot CLI, Claude Code, OpenAI Codex）**：MCP 连接失败、Schema 不兼容、服务挂起等问题频发。社区正在为 MCP 生态的稳定性“买单”，并表现出强烈的插件开发意愿（如 Claude Code 的 `account-profiles` 和 `twilight`），**市场急需官方提供统一的插件注册、发现和兼容性保障机制**。

#### **4. 差异化定位分析**

| 工具 | 核心定位 / 目标用户 | 技术路线侧重点 | 当前主要问题 / 短板 |
| :--- | :--- | :--- | :--- |
| **Claude Code** | **通用型全能助手**。目标覆盖全栈开发者，强调深度上下文与复杂任务规划。 | **插件生态驱动的扩展能力**、`/code-review` 等深度集成功能。 | **模型安全策略过于激进**，导致“误杀”合法场景，社区反弹强烈。权限模型复杂混乱。 |
| **OpenAI Codex** | **面向专业开发者与团队的协作平台**。侧重 Cowork 模式、远程控制与自动化。 | **Agent 子进程管理与 MCP 服务**、强大的会话管理能力。 | **Windows 体验严重拉胯**，成为最大短板。子代理资源泄漏问题突出，影响生产环境。 |
| **Gemini CLI** | **AI Agent 能力的试验场**。探索 Agent-to-Agent (A2A) 通信、沙箱化等前沿概念。 | **高级 Agent 行为控制**（通用代理、子代理）、**安全性不断加固**。 | **Agent 行为不可靠**（假成功、卡死）是最大痛点。模型自主决策能力弱，过度依赖用户指示。 |
| **GitHub Copilot CLI** | **GitHub 生态的坚固延伸**。强调与 GitHub 账户、仓库、Actions 的无缝集成。 | **企业级认证 (BYOK, ACP) 与安全策略**、MCP 服务集成。 | **回归 Bug 频繁**，核心功能更新质量不稳定。插件与扩展生态相对封闭，独立 Action 少。 |
| **Kimi Code CLI** | **轻量级、高性价比的中文友好工具**。面向快速原型和简单任务。 | 核心功能偏向实用，社区贡献以 Bug 修复为主。 | **社区规模较小，问题反馈周期长**。对非中文、尤其是复杂 MCP 场景的支持较弱。 |
| **OpenCode** | **高自由度、多提供商兼容的极客工具**。支持自定义后端（如 Ollama、LM Studio）。 | **模型提供商/插件自动发现**、高度定制化的 TUI。 | **付费订阅服务稳定性堪忧**（Go 401 故障）。核心功能（如 Plan/Build 模式）更新引发众怒。 |
| **Qwen Code** | **面向 Alibaba Cloud 生态与特定云服务 (DingTalk) 的集成工具**。 | **与企业内工具（如 DingTalk）的深度打通**、强调端到端的安全与审计。 | **核心发布流程不稳（CI 红色）**，影响迭代速度。安全策略与企业集成强相关，普适性待考。 |

#### **5. 社区热度与成熟度**

*   **高热度 & 成熟期 (Claude Code, OpenAI Codex)**：这些工具拥有最大的用户基数和最活跃的社区，Issue 讨论深入，PR 提交规范。社区不仅反馈 Bug，更主动参与功能设计与插件开发。但高活跃度也伴随着大量顽固的、长期未解决的痛点（如权限、Windows 兼容性）。
*   **高热度 & 快速迭代期 (Gemini CLI, GitHub Copilot CLI)**：社区反馈积极，版本迭代频繁（特别是 Alpha/Nightly 版本）。它们正在快速验证新功能（如 Agent 行为、MCP 集成），但同时也暴露了大量严重的回归和稳定性问题，说明产品尚未完全成熟。
*   **中等热度 & 追赶期 (OpenCode, Qwen Code)**：社区规模相对较小，但讨论聚焦于特定领域（OpenCode 的自定义能力、Qwen Code 的云集成）。它们面临的关键挑战是核心服务稳定性（OpenCode）或基础开发流程（Qwen Code CI）。
*   **低热度 & 早期阶段 (Kimi Code CLI)**：社区活跃度最低，反馈大多为基础 Bug 和功能缺失，尚未形成足够多的生态讨论或社区贡献。产品可能仍处于小范围用户测试或早期推广阶段。

#### **6. 值得关注的趋势信号**

1.  **“安全”成为双刃剑**：当前 AI CLI 的“安全”功能更多的是“阻碍”而非“保障”。过度的安全审查（模型降级、误报）不仅没有增强信任，反而极大地耗尽了开发者的耐心和精力，迫使社区寻求“绕过”方案。**未来 AI 工具的安全策略必须走向精细化、可配置和可解释性**，否则将面临严重的社区信任危机。

2.  **零依赖沙箱化呼声高涨**：Gemini CLI 社区提出的 #19873 “利用模型原生能力进行零依赖沙箱化”代表了行业一个新方向。这预示着**未来 AI 工具或将轻量化其执行环境，利用 LLM 的强大能力直接管理 OS 资源，以提升效率和安全性**。

3.  **“Windows 之痛”亟待解决**：从 OpenAI Codex 到 Kimi Code CLI，几乎所有非 Windows 原生工具都在遭遇在 Windows 上的“水土不服”。对于想要占领更大市场份额的工具而言，**专业化、高性能的 Windows 集成将是下一个必须攻克的战略高地**。

4.  **MCP 生态“基建”仍需夯实**：MCP 扩展了工具能力，但目前的连接稳定性、Schema 兼容性、资源泄漏等问题的集中爆发表明，**MCP 协议本身及其客户端实现还不够健壮**。官方需要投入更多精力制定标准，提供高质量的 SDK 和调试工具。

5.  **资源消耗与成本控制成为决策关键**：从 OpenAI Codex 的 RTK 过滤请求到 GitHub Copilot CLI 的预算控制需求，再到 OpenCode 的 CPU 空转，**开发者对 AI 工具带来的实际财务与计算成本变得越来越敏感**。提供透明、精细化的资源管理与优化能力将成为新工具脱颖而出的关键。

**对开发者的参考价值**：当前不建议将任何单一 AI CLI 工具作为“万能”依赖。对于追求**稳定与深度集成**的团队，可重点关注 **GitHub Copilot CLI** 与 **Claude Code**，但需预先评估其平台兼容性与误报风险。对于探索**前沿 Agent 能力**的开发者，**Gemini CLI** 值得投入研究，但要做好处理不稳定 Agent 行为的准备。若团队对 **Windows 或特定的云生态**有强依赖，建议优先选择针对性的工具（如 Qwen Code for Alibaba Cloud），或等待现有工具的痛点解决。核心策略是：**拥抱 AI 赋能，但保持工具链的多样性，并持续关注社区反馈以规避风险**。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，这是为您生成的 Claude Code Skills 社区热点报告。

---

## Claude Code Skills 社区热点报告 (数据截止：2026-07-23)

### 1. 热门 Skills 排行

以下是根据社区讨论热度与关注度筛选出的 5 个最受关注的 Skills（PR）：

1.  **fix(skill-creator): run_eval.py 触发检测与 Windows 兼容性修复**
    -   **功能**: 修复 skill-creator 工具链的核心脚本 `run_eval.py`，解决其在任何场景下均报告 0% 召回率（recall）的致命缺陷。该问题导致整个技能优化循环（`run_loop.py`）无法正常工作。
    -   **社区热点**: 该 PR 直接回应了社区反馈最强烈的 Bug（Issue #556），讨论点集中在技术实现方案，包括修复 Windows 管道流读取、并行工作器以及技能触发检测逻辑。用户普遍认为这是 skill-creator 工具链能够实际投入使用的关键。
    -   **状态**: **Open**
    -   **链接**: [PR #1298](https://github.com/anthropics/skills/pull/1298)

2.  **Add document-typography skill（文档排版技能）**
    -   **功能**: 增加一项专注于 AI 生成文档排版质量的技能，解决常见的孤字、孤行、标题悬沉等问题。
    -   **社区热点**: 社区认为这是一个精准、高价值的方向，直击 AI 生成内容在最终呈现阶段的痛点。讨论热度高，表明用户对“精修”阶段的质量控制有强烈需求。
    -   **状态**: **Open**
    -   **链接**: [PR #514](https://github.com/anthropics/skills/pull/514)

3.  **Add ODT skill（开放文档格式技能）**
    -   **功能**: 增加对 OpenDocument 格式（.odt, .ods）的创建、填充、读取与转换支持。
    -   **社区热点**: 社区普遍认为这是对现有文档技能集的重要补充，尤其对于使用 LibreOffice 或需要遵循 ISO 标准格式的用户。该 PR 持续有评论更新，表明用户对其进入官方集合有较高期待。
    -   **状态**: **Open**
    -   **链接**: [PR #486](https://github.com/anthropics/skills/pull/486)

4.  **Add testing-patterns skill（测试模式技能）**
    -   **功能**: 提供一个全面的测试技能，覆盖单元测试、React 组件测试、集成测试等，并引入“测试奖杯”哲学。
    -   **社区热点**: 社区认为这是一项提升输出代码质量的核心技能。讨论重点在于技能内容的全面性、可操作性与当前最佳实践的结合度。高质量代码生成是开发者社区的普遍追求。
    -   **状态**: **Open**
    -   **链接**: [PR #723](https://github.com/anthropics/skills/pull/723)

5.  **Add color-expert skill（色彩专家技能）**
    -   **功能**: 提供一个自包含的色彩专业知识技能，涵盖色彩命名系统、色彩空间选择（如 OKLCH）、无障碍对比度等。
    -   **社区热点**: 这是一个针对特定领域深度优化的技能示例。社区对其精细化的色彩空间指导表示认可，认为这是从“能用”到“用好”的重要工具，展示了 Skills 在专业领域的潜力。
    -   **状态**: **Open**
    -   **链接**: [PR #1302](https://github.com/anthropics/skills/pull/1302)

### 2. 社区需求趋势

从社区 Issues 反馈来看，当前用户的三大核心需求趋势如下：

-   **安全与信任治理**: 社区对在 `anthropic/` 官方命名空间下分发社区技能的安全性感到担忧（Issue #492）。用户强烈要求官方建立清晰的信任边界和审核机制，防止信任滥用。
-   **组织级协作与共享**: 用户非常希望 Skills 能在组织内直接共享（Issue #228），而非通过下载文件、手动上传的低效方式。这反映了 Skills 从个人工具向团队协作能力演进的迫切需求。
-   **基础工具链稳定性**: 大量的反馈（如 Issue #556, #1061, #1169）指向 `skill-creator` 等基础工具链的可靠性问题，特别是 Windows 兼容性和核心脚本的 Bug。这表明社区正在积极尝试开发自己的 Skills，但稳定可靠的开发工具是当前最大的瓶颈。

### 3. 高潜力待合并 Skills

以下是一些评论活跃、讨论成熟、预期将很快合并入主分支的技能：

-   **Add document-typography skill**: 精准解决用户痛点，功能定义清晰，技术实现明确。有较大概率被官方采纳。
    -   **链接**: [PR #514](https://github.com/anthropics/skills/pull/514)
-   **Add ODT skill**: 完善了文档格式生态，满足了特定群体的刚需，持续更新状态表明作者在积极跟进反馈。
    -   **链接**: [PR #486](https://github.com/anthropics/skills/pull/486)
-   **Add testing-patterns skill**: 紧密贴合开发者日常工作流，具有很高的实用价值，符合社区对提升代码质量的需求。
    -   **链接**: [PR #723](https://github.com/anthropics/skills/pull/723)
-   **Add color-expert skill**: 作为领域专家的典范，其精细化的设计思路和对质量的高要求，为 Skills 的深度发展提供了范本。
    -   **链接**: [PR #1302](https://github.com/anthropics/skills/pull/1302)

### 4. Skills 生态洞察

**一句话总结**: 社区当前最集中的诉求是**摆脱「纸老虎」状态**——即除了追求更具深度的功能性技能（如专业测试、文档排版）外，更迫切需要官方解决开发工具链（skill-creator）的可靠性、跨平台兼容性（尤其是 Windows）和触发验证机制，以实现“技能必须能真正落地生效”这一基础前提。

---

# Claude Code 社区动态日报  
**2026-07-23** | 数据来源：github.com/anthropics/claude-code  

---

## 今日速览  
- **v2.1.218 发布**：`/code-review` 改为后台子代理运行，不再占用会话上下文，同时新增屏幕朗读对文字删除操作的提示。  
- **Fable 5 安全分类器误报持续发酵**：多起 Issue 反映合法安全讨论、法律/安全审计工作被错误降级至 Opus 4.8，社区呼吁调整分类策略。  
- **桌面端 / 插件生态活跃**：新 PR 带来实验性的 `account-profiles` 插件（多账号隔离）和 `twilight` 插件（设计/实现工作流框架），显示社区对扩展能力的高度关注。  

---

## 版本发布  
**v2.1.218**（过去24小时）  
- `/code-review` 改为后台子代理运行，避免审核过程填充会话历史，且仍能正确处理连续斜杠命令。  
- 新增对 `Option+Delete`、`Ctrl+W`、`Cmd+Backspace` 等删除操作的屏幕朗读提示。  

---

## 社区热点 Issues（10 条精选）  

### 1️⃣ #5140 - 用户级权限设置未在项目层生效  
- **标签**：bug / has repro / platform:macos / area:tools,core,security  
- **摘要**：~/.claude/settings.json 中的用户级权限在 VS Code 中不被项目级配置继承，造成权限冲突。  
- **热度**：👍34 / 💬24  
- **链接**：https://github.com/anthropics/claude-code/issues/5140  

> **关注点**：该问题已存在近一年且持续被顶帖，涉及核心权限模型，影响所有 macOS 用户。

### 2️⃣ #61682 - GitHub 连接器显示“已连接”但 Cowork 中无工具暴露  
- **标签**：bug / platform:windows / area:cowork,desktop  
- **摘要**：Windows 11 桌面 App 中 GitHub 连接器状态正常，但无法调用任何工具。  
- **热度**：👍19 / 💬17  
- **链接**：https://github.com/anthropics/claude-code/issues/61682  

> **关注点**：Cowork 功能在 Windows 上的核心能力受损，影响团队协作场景。

### 3️⃣ #75571 - VS Code 扩展每 30-40 分钟挂起 90 秒  
- **标签**：bug / has repro / platform:macos (ARM64) / area:ide  
- **摘要**：本地 claude 进程在 kevent64 中空闲，但扩展 UI 冻结，疑似 IPC 通信阻塞。  
- **热度**：💬13  
- **链接**：https://github.com/anthropics/claude-code/issues/75571  

> **关注点**：严重的性能问题，直接影响开发者日常使用体验，附有详细重现步骤。

### 4️⃣ #71726 - 桌面 App 缺少 CLI 的“消息注入”功能  
- **标签**：feature / duplicate / area:desktop  
- **摘要**：CLI 中可在任务执行中途注入消息（steering），桌面 App 仅在轮次结束后才响应。  
- **热度**：👍16 / 💬8  
- **链接**：https://github.com/anthropics/claude-code/issues/71726  

> **关注点**：桌面 App 与 CLI 存在功能缺口，社区期望保持交互一致性。

### 5️⃣ #78933 - 远程控制从未成功连接  
- **标签**：bug / platform:windows / area:desktop  
- **摘要**：运行 `/remote-control` 时抛出 “Cannot read properties of undefined (reading 'session_url')”。  
- **热度**：💬7  
- **链接**：https://github.com/anthropics/claude-code/issues/78933  

> **关注点**：桌面 App 远程控制功能完全不可用，影响跨设备协作。

### 6️⃣ #75571 / #80348 - Fable 5 模型行为问题频发  
- **标签**：bug  
- **摘要**：用户报告 Fable 5 自信地声称“已验证更改”，但用户实际检查发现内容未变；另有多起安全分类误报导致模型降级。  
- **热度**：💬2+（多个相关 Issue）  
- **链接**：https://github.com/anthropics/claude-code/issues/80348  

> **关注点**：模型可靠性引发质疑，尤其在安全、审计等专业场景下。

### 7️⃣ #80189 - MCP 文件系统服务在 Windows 上从未被调用  
- **标签**：bug / platform:windows  
- **摘要**：tools/call 请求发送失败，尽管 handshake 成功，且跨传输协议和服务版本持续存在。  
- **热度**：💬3 / 👍1  
- **链接**：https://github.com/anthropics/claude-code/issues/80189  

> **关注点**：MCP 生态基础服务严重故障，影响文件操作能力。

### 8️⃣ #78121 - Stop Hook 重复触发导致 /goal 死循环  
- **标签**：bug / has repro / area:hooks  
- **摘要**：stop_hook_active: true 未被尊重，导致停止条件满足后仍反复触发 hook。  
- **热度**：💬1  
- **链接**：https://github.com/anthropics/claude-code/issues/78121  

> **关注点**：高级自动化功能（/goal 循环）可靠性问题，可能引发无限执行。

### 9️⃣ #80288 - Xcode 27 上 iOS 模拟器面板不可用  
- **标签**：bug / platform:macos  
- **摘要**：claude-ios-sim 助手写入硬编码的 PrivateFrameworks 路径，且 Metal 调用崩溃。  
- **热度**：💬1  
- **链接**：https://github.com/anthropics/claude-code/issues/80288  

> **关注点**：影响 iOS 开发者测试流程，涉及新版本 Xcode 兼容性。

### 🔟 #79722 - /fork 泄漏任务到父会话  
- **标签**：bug / area:fork  
- **摘要**：/fork <prompt> 创建的 fork 任务同时被父会话执行，可能导致重复副作用。  
- **热度**：💬1  
- **链接**：https://github.com/anthropics/claude-code/issues/79722  

> **关注点**：任务隔离机制缺陷，可造成意外操作风险。

---

## 重要 PR 进展（共 9 条，全部列出）  

### 1️⃣ #80353 - 文档：GCP 部署遇 checksum 不匹配时停止  
- **摘要**：改进 GCP gateway 部署脚本，在二进制校验失败时中止流程并清理。  
- **链接**：https://github.com/anthropics/claude-code/pull/80353  

### 2️⃣ #80326 - 新增 account-profiles 插件（实验性）  
- **摘要**：管理隔离的 CLAUDE_CONFIG_DIR 环境，支持个人/工作/客户账号快速切换，提供创建、诊断、删除命令。  
- **链接**：https://github.com/anthropics/claude-code/pull/80326  

### 3️⃣ #80294 - 文档：修复 1 个失效链接（通过 archive.org）  
- **摘要**：使用 Wayback 机器修复 README 中的 npm 包链接。  
- **链接**：https://github.com/anthropics/claude-code/pull/80294  

### 4️⃣ #80241 - 修复：控制台输出导致历史滚动到顶部  
- **摘要**：解决 Claude 向控制台追加文本时，界面自动回滚到顶部的问题。  
- **链接**：https://github.com/anthropics/claude-code/pull/80241  

### 5️⃣ #80229 - 文档：修复 1 个失效链接（通过 archive.org）  
- **摘要**：另一处文档链接修复。  
- **链接**：https://github.com/anthropics/claude-code/pull/80229  

### 6️⃣ #80196 - 修复：上下文达到 100% 时自动压缩不触发  
- **摘要**：修复状态栏报告“100% context used”但 auto-compact 不执行的 bug。  
- **链接**：https://github.com/anthropics/claude-code/pull/80196  

### 7️⃣ #80195 - 修复：Max 订阅用户瞬间耗尽使用配额  
- **摘要**：解决订阅 Max 用户报告的一启动即提示额度不足的问题。  
- **链接**：https://github.com/anthropics/claude-code/pull/80195  

### 8️⃣ #80112 - 增强 devcontainer 防火墙初始化的 DNS 容错  
- **摘要**：使防火墙脚本在单个域名解析失败时继续执行，避免整个设置中断。  
- **链接**：https://github.com/anthropics/claude-code/pull/80112  

### 9️⃣ #80008 - 新增 twilight 插件（实验性）  
- **摘要**：提供 spec-first 的设计/实现工作流，包含持久化焦点栈，可大幅提升复杂任务效果。  
- **链接**：https://github.com/anthropics/claude-code/pull/80008  

---

## 功能需求趋势  
从近期 Issues 和 PR 中可看出社区最关注的功能方向：  

1. **多账号隔离与配置管理**  
   - `account-profiles` 插件直接回应了开发者同时使用个人/公司账号的需求。  
   - Issue #67724 希望会话标题能自动使用用户的语言生成，而非固定英文。  

2. **状态栏/可视化增强**  
   - #56843 要求状态栏数据包含沙箱模式状态；#67724 要求多语言会话标题。  
   - 表明用户更希望从界面实时感知 session 状态。  

3. **跨平台体验一致性**  
   - #71726 指出桌面 App 缺少 CLI 的“消息注入”功能；Windows / Linux 上大量专用 bug 提示平台支持仍需打磨。  

4. **模型安全策略可配置性**  
   - 多起 Fable 5 误报事件催生 #67732、#67733 等请求，要求允许合法安全/审计工作使用高能力模型而不被降级。  

5. **Cowork & 远程协作稳定性**  
   - #61682（GitHub 连接器无工具）、#78933（远程控制连接失败）暗示协作功能仍是薄弱环节。  

---

## 开发者关注点（痛点 & 高频需求）  

- **权限系统混乱**：#5140（用户层 vs 项目层）、#67720（auto-mode 权限分类器错误拒绝）表明权限模型需要更清晰的层级和可覆盖机制。  
- **模型降级与误报**：Fable 5 的安全分类器对合法内容（论文阅读、安全审计、防御测试）频繁触发降级，开发者深感挫败，认为是“误导性安全”。  
- **性能瓶颈**：#75571（VS Code 扩展每30分钟挂起90秒）和自动压缩不触发（#80196）影响日常流畅度。  
- **MCP 生态稳定性**：#80189（Windows 上 MCP 文件系统从未被调用）、#78858（Hyper-V 服务缺失）显示插件/服务在 Windows 平台上问题集中。  
- **消息丢失/泄漏**：#79722（fork 泄漏任务到父会话）、#69234（Alt+V 图像粘贴永久失败）提示会话状态管理尚有缺陷。  
- **插件开发热情高涨但缺乏官方规范**：社区贡献的 `twilight`、`account-profiles` 插件展现了强烈的扩展意愿，但官方尚未推出统一的插件市场或指南。  

---  
*日报自动生成于 2026-07-23，数据截至 2026-07-22 23:59 UTC。所有链接指向原始 GitHub Issue 或 PR 详情页。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

好的，作为专注于 AI 开发工具的技术分析师，以下是根据您提供的 GitHub 数据生成的 OpenAI Codex 社区动态日报。

---

# OpenAI Codex 社区动态日报 | 2026-07-23

## 今日速览

社区动态主要聚焦于 Windows 平台体验的痛点修复与优化。昨日发布了 4 个 Rust 版本的 Alpha 更新，但未披露具体功能细节。社区反馈中，**Windows/WSL 环境下的性能与兼容性问题**成为绝对焦点，多个高热度 Issue 围绕 WSL 路径错误、界面卡顿及子代理资源占用展开。此外，关于**配额限制和模型选择灵活性**的讨论也引发了 Pro/Ultra 用户的热烈关注。

## 版本发布

- **Rust 客户端 (Codex CLI) 连续发布 4 个 Alpha 版本**
  - `rust-v0.146.0-alpha.1` 至 `rust-v0.146.0-alpha.3`: 三个小版本更新。
  - `rust-v0.145.0-alpha.30`: 一个迭代版本。
  - **分析师点评**: 高频的 Alpha 版本迭代可能暗示团队正在快速修复内部问题或为新特性做准备。由于未提供详细的 Release Notes，具体变更需要关注 Commit 记录。

## 社区热点 Issues (Top 10)

1.  **[#20214] Windows 11 上 Codex App 频繁卡顿/冻结 (72条评论, 71👍)**
    - **链接**: https://github.com/openai/codex/issues/20214
    - **重要性**: 该问题反映了 Windows 桌面客户端最大的性能痛点。用户即使在拥有 32GB RAM 的高配置 Win11 Pro 系统上，仍遇到严重卡顿，表明可能存在内存泄漏或渲染线程阻塞问题。极高的点赞数反映了其影响面之广。

2.  **[#16815] Windows WSL Agent 模式创建任务失败 (22条评论)**
    - **链接**: https://github.com/openai/codex/issues/16815
    - **重要性**: 此问题是 WSL 集成中一个持续了数月的严重 Bug。`AbsolutePathBuf` 的路径解析错误直接中断了开发者使用 WSL Agent 的核心工作流。该问题的长期存在可能阻碍了部分 Windows 用户采用 Codex。

3.  **[#34014] 独立 Windows App 高 CPU 占用 (18条评论, 11👍)**
    - **链接**: https://github.com/openai/codex/issues/34014
    - **重要性**: 该问题精确地定位到 `WMI Provider Host` 进程的 CPU 飙升，且 VS Code 扩展工作正常，说明桌面应用的特定实现存在缺陷，可能涉及系统信息轮询或资源监控逻辑。

4.  **[#34202] 子代理导致磁盘空间无限增长 (7条评论)**
    - **链接**: https://github.com/openai/codex/issues/34061
    - **重要性**: 磁盘空间是开发者的硬资源。子代理任务产生的数据未能得到有效清理，可能导致长时间任务后用户磁盘被占满，影响系统稳定性。

5.  **[#28015] 安全审查误报 (22条评论)**
    - **链接**: https://github.com/openai/codex/issues/28015
    - **重要性**: 安全功能误报会直接影响开发效率。该 Issue 指出常规的本地 DevOps 操作（如检查日志）被错误标记为“网络安全风险”并中断交互，这会降低用户对安全系统的信任。

6.  **[#27597] VS Code Remote-SSH 扩展加载失败 (15条评论)**
    - **链接**: https://github.com/openai/codex/issues/27597
    - **重要性**: 远程开发是现代工作流的核心。该问题直接切断了大量使用 SSH 远程服务器的用户通过 VS Code 使用 Codex 的路径，影响面较大。

7.  **[#23200] 支持 iOS 移动端连接无头远程 Linux 主机 (13条评论, 42👍)**
    - **链接**: https://github.com/openai/codex/issues/23200
    - **重要性**: 这是一个功能请求，但点赞数排名第二。它代表了用户（尤其是移动端用户）对随时随地、不依赖本地桌面电脑就能管理远程服务器任务的强烈需求。

8.  **[#19001] 请求为 CLI 添加 RTK (Real-Time Kernel) 过滤 (13条评论, 15👍)**
    - **链接**: https://github.com/openai/codex/issues/19001
    - **重要性**: 这是一个极具创新性的增强请求，旨在通过过滤Shell命令输出来减少60-90%的token消耗。这表明高级用户开始深入思考如何在保证上下文质量的同时，优化 API 调用成本。

9.  **[#34782] WSL 路径解析中断 (3条评论, 刚刚关闭)**
    - **链接**: https://github.com/openai/codex/issues/34782
    - **重要性**: 尽管很快被关闭，但此 Issue 描述了在 7月22日 商店更新后立即出现的严重回归 Bug（WSL 路径解析损坏），导致任务创建失败。这显示了微软商店更新流程可能存在验证不足的风险。

10. **[#34822] 请求恢复5小时限制或提供Ultra预算 (3条评论)**
    - **链接**: https://github.com/openai/codex/issues/34822
    - **重要性**: 此问题直接触及了 Pro/Ultra 用户的核心利益。有用户反映在“Ultra”模式下，一次长时间运行消耗了 Pro 20x 计划的 50-60% 配额，这引发了对现有配额模型合理性的质疑。

## 重要 PR 进展 (Top 10)

1.  **[#34840] 为线程添加持久化“置顶”功能**
    - **链接**: https://github.com/openai/codex/pull/34840
    - **功能**: 允许用户在客户端将重要线程置顶，并提供按 `isPinned` 过滤和分页的 API。这直接回应了用户对线程管理能力的迫切需求。

2.  **[#34839] 保留 MCP 启动中断时的用户输入**
    - **链接**: https://github.com/openai/codex/pull/34839
    - **功能**: 修复了在 MCP 工具正在加载时打断（Ctrl+C）会导致用户输入丢失的 Bug。这是对交互体验的重要打磨。

3.  **[#34835] 追踪线程压缩时间**
    - **链接**: https://github.com/openai/codex/pull/34835
    - **功能**: 在性能分析中添加 `compaction_ms` 指标，帮助开发者诊断因上下文压缩导致的性能瓶颈。这对优化长会话至关重要。

4.  **[#34831] 在进程内 App 服务器关闭前 Flush 分析数据**
    - **链接**: https://github.com/openai/codex/pull/34831
    - **功能**: 修复了一个可能导致分析事件丢失的 Bug。这有助于 OpenAI 收集更准确的使用数据以改进产品。

5.  **[#34825] 减少构建 Responses 请求时的内存拷贝**
    - **链接**: https://github.com/openai/codex/pull/34825
    - **功能**: 通过优化 JSON 序列化和 WebSocket 请求处理，来减少内存开销。这是一项典型的性能优化，对大规模使用场景有帮助。

6.  **[#34811] 修复沙箱提示中的网络访问渲染**
    - **链接**: https://github.com/openai/codex/pull/34811
    - **功能**: 修复了沙盒模板中网络访问状态无法正确显示的问题，确保权限提示准确无误。这有助于提升安全系统的清晰度。

7.  **[#34806] 使用路径 URI 作为 Shell 审批密钥**
    - **链接**: https://github.com/openai/codex/pull/34806
    - **功能**: 将 Shell 命令审批密钥的 `cwd` (当前工作目录) 存储为标准化的 `PathUri`，消除了路径比较时可能出现的歧义（如 `./` 和绝对路径）。这提高了安全审批的准确性。

8.  **[#34797] 在核心兼容的技能目录中抑制省略通知**
    - **链接**: https://github.com/openai/codex/pull/34797
    - **功能**: 为了与核心渲染器行为保持统一，在技能目录输出超出元数据预算而省略条目时，不再输出特定的省略通知。

9.  **[#34796] 跳过超长行（>4 KiB）的语法高亮**
    - **链接**: https://github.com/openai/codex/pull/34796
    - **功能**: 当输入行长度超过 4 KiB 时，自动跳过语法高亮以避免 CPU 或内存过度消耗。这是一个重要的防性能崩溃机制。

10. **[#34819] 启用跨平台的 Git 归属功能**
    - **链接**: https://github.com/openai/codex/pull/34819
    - **功能**: 在 App Server、MCP Server 等多个入口统一启用 Git 归属功能，确保模型在生成 Commit 信息时能正确遵守认证过的工作空间政策。

## 功能需求趋势

- **Windows/WSL 深度集成**：社区强烈要求修复 WSL 环境下的各种路径、性能和兼容性问题。这已成为 Windows 用户在 Codex 上获得与 Linux/Mac 同等体验的核心瓶颈。
- **性能与资源控制**：用户不仅要求 App 本身流畅，还希望 Codex 能更智能地管理子代理的资源消耗（如磁盘、CPU），并提供更好的Token使用透明度与优化工具（如 RTK 过滤）。
- **远程与移动能力**：对“无头”远程服务器的支持、以及移动端作为控制层的需求日益增长，反映了开发者工作流的多设备、多地域趋势。
- **配额与模型选择灵活性**：Pro/Ultra 用户对现有配额模型（特别是 Ultra 模式的消耗）表示担忧，希望能有更细粒度的预算控制或恢复更灵活的时长限制。

## 开发者关注点

- **平台稳定性（尤其是 Windows）**：Windows 桌面应用的卡顿、WSL 集成问题、路径错误和更新后的回归问题，是当前开发者反馈中最密集的痛点，影响了日常开发体验。
- **MCP 集成体验**：外部 MCP 服务器（如 Meta Ads）的 OAuth 登录失败，以及内部子代理 MCP 进程泄漏，表明 MCP 生态系统的稳定性和兼容性仍有待加强。
- **资源消耗与配额**：子代理导致的磁盘空间“爆炸式”增长，以及 Ultra 模式下配额快速消耗的问题，直接触动了用户的成本敏感神经，是潜在的用户流失风险点。
- **安全系统的“噪点”**：安全审查的误报不仅干扰了工作流，也破坏了用户对 AI Agent 信任度的建立。如何让安全系统更“聪明”地判断意图，是提升体验的关键。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

好的，各位开发者，早上好。这是 2026 年 7 月 23 日的 Gemini CLI 社区动态日报。

---

## Gemini CLI 社区动态日报 | 2026-07-23

### 今日速览

昨日社区发布了一个重要的预览版 `v0.53.0-preview.0`，重点修复了 A2A (Agent-to-Agent) 通信中因响应分组错误导致的 400 错误。此外，安全方面是绝对的重心：不仅在一个安全相关的 PR 中修复了 OAuth 认证的 `Premature close` 问题，最新发布的 `v0.52.0-nightly` 更是直接修复了一个严重的 A2A 服务器 RCE 漏洞。社区对于代理（Agent）的可靠性和行为可控性的讨论热度不减，多篇高关注度 Issue 聚焦于子代理的误报成功状态和性能问题。

### 版本发布

昨日共发布 3 个版本：

*   **[v0.53.0-preview.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.53.0-preview.0)**: 此预览版修复了 A2A 场景下的一个关键问题，即被取消的工具响应未正确分组，导致连续的对话角色合并触发了 400 Bad Request 错误。同时新增了基于 LLM 的 Triage 编排器功能，旨在自动化问题分类流程。
*   **[v0.52.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.52.0)**: 最新的稳定版，主要进行了内部重构，排除了 CI 配置文件对工作区上下文的干扰，并为“看门 Triage”功能奠定了基础。
*   **[v0.52.0-nightly.20260722](https://github.com/google-gemini/gemini-cli/releases/tag/v0.52.0-nightly.20260722.gc776c665b)**: 此每日构建版本是昨晚发布的热点，因为它修复了一个严重的 **RCE (远程代码执行) 漏洞**。漏洞源于 A2A 服务器未对工作区信任和执行任务进行隔离，现已修复。

### 社区热点 Issues

1.  **[子代理恢复被伪装成成功状态](https://github.com/google-gemini/gemini-cli/issues/22323)**
    *   **重要性**: 🔥🔥🔥🔥🔥 这是一个严重且具有误导性的 Bug。当子代理（如 `codebase_investigator`）因达到最大交互次数（MAX_TURNS）而中断时，系统将其报告为“成功”并显示“达到目标”。这掩盖了底层的问题，让用户误以为任务已完成，实际上什么也没做。
    *   **社区反应**: 高关注度，12 条评论，已打上 `priority/p1` 和 `kind/bug` 标签，说明开发者对其优先级和紧迫性的认可。

2.  **[通用代理（Generalist Agent）卡死](https://github.com/google-gemini/gemini-cli/issues/21409)**
    *   **重要性**: 🔥🔥🔥🔥🔥 影响核心交互流程的严重 Bug。当任务被委派给通用代理时，它会无限期地“挂起”，哪怕是很简单的操作（如创建文件夹）。这是一个持续了很久的高曝光问题。
    *   **社区反应**: 8 条评论，8 个 👍，社区反馈强烈。用户已经找到了临时绕过方法（指示模型不要使用子代理）。

3.  **[利用模型原生能力进行零依赖沙箱化](https://github.com/google-gemini/gemini-cli/issues/19873)**
    *   **重要性**: 🔥🔥🔥🔥 这不是一个 Bug，而是一个宏大的功能提议。核心思想是，既然 Gemini 模型天生擅长使用 Bash，不如构建一个零依赖的 OS 沙箱来充分发挥其能力，同时保证安全。这代表了社区对未来架构的一种激进但合理的设想。
    *   **社区反应**: 8 条评论，标记为 `effort/large`，预计实现工作量巨大。

4.  **[构建稳健的组件级评估](https://github.com/google-gemini/gemini-cli/issues/24353)**
    *   **重要性**: 🔥🔥🔥🔥 这是提升项目质量的关键基础设施。该 EPIC 旨在建立一套针对 CLI 各组件的独立评估体系，以确保代码修改不会破坏特定功能。
    *   **社区反应**: 7 条评论，反映了开发团队对持续交付质量的重视。

5.  **[探索 AST 感知的文件读取和搜索](https://github.com/google-gemini/gemini-cli/issues/22745)**
    *   **重要性**: 🔥🔥🔥🔥 该 EPIC 探讨引入 AST (抽象语法树) 感知能力来提升代理的理解精准度。通过精确读取方法体、减少“读取-重复-修正”的循环，可以显著降低 Token 消耗和执行步骤。
    *   **社区反应**: 7 条评论。这是一个非常专业和前瞻性的技术方向。

6.  **[Gemini 未能充分利用技能和子代理](https://github.com/google-gemini/gemini-cli/issues/21968)**
    *   **重要性**: 🔥🔥🔥 这反映了模型在自主决策上的局限性。即使配置了自定义技能和子代理，Gemini 也基本不使用，除非用户明确指示。这极大地限制了 CLI 的自动化和可扩展性。
    *   **社区反应**: 6 条评论。此为社区高频抱怨点，影响了自定义工作流的可用性。

7.  **[自动记忆（Auto Memory）对低信号会话的无限重试](https://github.com/google-gemini/gemini-cli/issues/26522)**
    *   **重要性**: 🔥🔥🔥 功能缺陷。Auto Memory 的提取代理只会将有读取操作的会话标记为“已处理”，导致那些因内容简短（低信号）而被跳过的会话会被无休止地再次尝试，造成资源和时间浪费。
    *   **社区反应**: 5 条评论。说明了记忆系统的实现逻辑还不够智能。

8.  **[Shell 命令执行后卡在“等待输入”](https://github.com/google-gemini/gemini-cli/issues/25166)**
    *   **重要性**: 🔥🔥🔥 一个非常恼人的 Bug。简单的命令执行完毕后，CLI 依然显示“等待输入”状态，导致用户长时间等待。这极大地影响了使用体验。
    *   **社区反应**: 4 条评论，3 个 👍。标记为 `priority/p1`，表明这是一个高优问题。

9.  **[浏览器子代理在 Wayland 下失败](https://github.com/google-gemini/gemini-cli/issues/21983)**
    *   **重要性**: 🔥🔥🔥 一个特定于环境的 Bug。在 Linux 的 Wayland 显示协议下，浏览器子代理无法正常工作，这影响了大量 Linux 用户。
    *   **社区反应**: 4 条评论，1 个 👍。这是一个持续性的平台兼容性问题。

10. **[子代理在未经许可的情况下运行](https://github.com/google-gemini/gemini-cli/issues/22093)**
    *   **重要性**: 🔥🔥🔥 严重的行为预期偏离。从 v0.33.0 开始，子代理在用户明确禁用且无配置文件的情况下被激活，违反了用户的显式配置。
    *   **社区反应**: 3 条评论。这是一个信任和安全问题，用户期望“关闭”就是完全关闭。

### 重要 PR 进展

1.  **[修复：从历史记录中过滤掉思考（Thought）部分](https://github.com/google-gemini/gemini-cli/pull/28509)**
    *   **功能**: 当上下文管理关闭时，`getHistoryTurns` 返回的历史记录中会包含模型的内部“思考”内容，这会导致后续对话中出现重复且无意义的推理块。此 PR 专门过滤掉这些内容，提升了对话质量。
    *   **链接**: `https://github.com/google-gemini/gemini-cli/pull/28509`

2.  **[修复：在模型降级时轮换会话 ID](https://github.com/google-gemini/gemini-cli/pull/28469)**
    *   **功能**: 当模型因故降级（例如，回退到 `gemini-2.5-flash`）时，如果使用相同的会话 ID 重试，API 会返回错误。此 PR 通过在降级时创建一个新的会话 ID，解决了这一阻塞问题。
    *   **链接**: `https://github.com/google-gemini/gemini-cli/pull/28469`

3.  **[修复：将 gemini-3.5-flash 加入所有用户的模型选择器](https://github.com/google-gemini/gemini-cli/pull/28485)**
    *   **功能**: 修复了一个模型可见性 Bug。尽管 `gemini-3.5-flash` 已被定义，但部分用户（v0.51.0）无法在模型选择器中看到它。此 PR 修复了模型列表的构建逻辑。
    *   **链接**: `https://github.com/google-gemini/gemini-cli/pull/28485`

4.  **[修复：/compress 命令支持可取消操作](https://github.com/google-gemini/gemini-cli/pull/28506)**
    *   **功能**: 为用户体验细节优化。为 `/compress` 命令添加了 `AbortSignal` 支持，使得后台压缩任务可以被用户取消，从而避免因网络请求无法中断带来的体验问题。
    *   **链接**: `https://github.com/google-gemini/gemini-cli/pull/28506`

5.  **[修复：使用原生 fetch 进行 OAuth 令牌交换](https://github.com/google-gemini/gemini-cli/pull/28446)**
    *   **功能**: 修复了在部分无头 VPS 环境中，`gemini login` 因 `Premature close` 错误而失败的问题。通过将底层的 HTTP 请求库替换为 Node.js 原生 `fetch` 来解决。
    *   **链接**: `https://github.com/google-gemini/gemini-cli/pull/28446`

6.  **[文档：修复 6 个缺失 .md 扩展名的交叉引用链接](https://github.com/google-gemini/gemini-cli/pull/28505)**
    *   **功能**: 一个纯粹的文档修复。修复了 `policy-engine.md` 和 `hooks/reference.md` 中指向其他页面的链接，由于缺少 `.md` 扩展名，在 GitHub 上会显示 404 错误。
    *   **链接**: `https://github.com/google-gemini/gemini-cli/pull/28505`

7.  **[CI/元：版本升级到 0.54.0 每日构建](https://github.com/google-gemini/gemini-cli/pull/28510)**
    *   **功能**: 自动化版本升级脚本。这本身没有功能性变化，但标志着下一个开发周期的开始。
    *   **链接**: `https://github.com/google-gemini/gemini-cli/pull/28510`

8.  **[功能：新增 eval 覆盖率报告命令](https://github.com/google-gemini/gemini-cli/pull/28169)**
    *   **功能**: 为开发者工具链添砖加瓦。新增了 `eval:coverage` 命令，可以交叉引用工具注册表与评估用例，生成内置工具的评估覆盖率报告。
    *   **链接**: `https://github.com/google-gemini/gemini-cli/pull/28169`

9.  **[基础设施：PR 生成器与 SSR 代码生成管线](https://github.com/google-gemini/gemini-cli/pull/28431)**
    *   **功能**: 这是一个基础设施 PR，为 Gemini CLI 的 SSR 代码生成 Pipeline 配置了 Cloud Run Job、Workflows 和 Dockerfile。这表明项目正在构建更自动化的代码生成能力。
    *   **链接**: `https://github.com/google-gemini/gemini-cli/pull/28431`

10. **[修复：限制 `tools.core` 通配符 DENY 仅作用于内置工具](https://github.com/google-gemini/gemini-cli/pull/28499)**
    *   **功能**: 策略引擎的一个 Bug 修复。当用户使用 `tools.core` 的通配符拒绝规则（DENY）时，该规则会错误地阻止所有 MCP（模型上下文协议）工具。此 PR 通过引入 `excludeMcp` 属性来解决。
    *   **链接**: `https://github.com/google-gemini/gemini-cli/pull/28499`

### 功能需求趋势

1.  **Agent 能力与可靠性是绝对核心**: 社区最关注的是如何让 Agent（特别是子代理）更可靠、更智能。包括但不限于：更稳健的终止条件判断（#22323）、更好的模型自主决策能力（#21968）、对代理行为的可观测性（#22598）。
2.  **安全性与沙箱化**: 安全议题热度极高。从修复 RCE 漏洞到社区提出的“零依赖 OS 沙箱”构想（#19873），都表明开发者对 Agent 执行代码的安全性有极高要求。
3.  **代码理解智能化（AST 集成）**: 开发者和用户普遍希望 CLI 能深入理解代码结构，而不仅仅是文本操作。AST 感知的文件读取、搜索和代码库映射是明确提出的方向（#22745, #22746）。
4.  **子代理决策透明化与可控性**: 用户希望知道子代理到底在执行什么、为什么失败，并且能够完全控制其启用与否（#21763, #22093）。
5.  **新模型与特性支持**: 社区对模型选择、OAuth 兼容性等问题敏感，希望 CLI 能及时跟进并适配新的模型和认证方式（#28485, #28446）。

### 开发者关注点

*   **子代理状态报告不透明**：最让开发者感到困惑和不安的是 #22323 中提到的“假成功”问题。这不仅浪费了时间，还可能掩盖了更深层的应用逻辑错误。
*   **核心交互流程不稳定**：#21409（通用代理卡死）和 #25166（命令卡在等待输入）是典型的“

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-07-23）

---

## 今日速览

昨日发布的小版本 **v1.0.74-1** 正式加入 **Gemini 3.6 Flash** 模型支持，并改善了多会话体验。与此同时，社区反馈集中在 **MCP 服务器连接异常**（#2282）和 **BYOK 在 --acp 模式下被拒绝**（#4016）两个回归问题，此外 **僵尸进程泄漏**（#4163）和 **CAPI 5 MB 请求体限制**（#4183）也引起广泛讨论。

---

## 版本发布

过去 24 小时共发布 3 个补丁版本，均为修复与变更：

- **v1.0.74-1**（主要更新）
  - **新增**：首次运行时显示闪屏，引导用户选择默认沙箱环境；支持 **Gemini 3.6 Flash** 模型。
  - **改进**：修复多会话复用时的对话框泄漏问题，系统托盘选择器在切换回会话后正常重新打开；`$` 交互式 Shell 快捷键功能优化。
- **v1.0.74-2 / v1.0.74-3**：仅标注“Fixes and changes”，未提供详细描述。

> 链接：[Releases](https://github.com/github/copilot-cli/releases)

---

## 社区热点 Issues（10 条）

以下选取过去 24 小时内最受关注的 10 条 Issue，涵盖回归、性能、平台兼容等关键领域：

1. **#2282**[CLOSED] — [area:mcp] 无法连接 MCP 服务器  
   - **摘要**：Windows 系统通过 WinGet 安装后，启动 Copilot CLI 即提示 `Failed to connect to MCP server 'github-mcp-server'`。已关闭，但仍有 11 条评论。  
   - **为什么重要**：MCP 是扩展生态的核心入口，该问题影响大量新用户首次体验。  
   - [Issue 链接](https://github.com/github/copilot-cli/issues/2282)

2. **#443**[OPEN] — [area:tools] 支持原生 PDF 阅读  
   - **摘要**：用户无法直接读取 PDF，需要手动安装 `pdftotext` 等工具。已有 33 个 👍 和 6 条评论。  
   - **为什么重要**：学术/技术文档场景高频需求，社区呼声极高。  
   - [Issue 链接](https://github.com/github/copilot-cli/issues/443)

3. **#4016**[OPEN] — [area:authentication, models] BYOK 在 `--acp` 模式下仍被拒绝（回归）  
   - **摘要**：使用自定义 Provider（`COPILOT_PROVIDER_*`）时，`copilot -p` 可免登录，但 `copilot --acp --stdio` 仍要求 GitHub 登录。与 #3048、#3902 同类问题。  
   - **为什么重要**：企业用户依赖 BYOK 控制模型与成本，该回归影响合规与自动化场景。  
   - [Issue 链接](https://github.com/github/copilot-cli/issues/4016)

4. **#4163**[OPEN] — [area:platform-linux, tools] 子进程僵尸累积  
   - **摘要**：v1.0.71 起，已结束的子进程未正确回收，以僵尸状态挂在 copilot 进程下，约 2 个/分钟。  
   - **为什么重要**：长时间运行会耗尽系统 PID 资源，影响服务器稳定性。  
   - [Issue 链接](https://github.com/github/copilot-cli/issues/4163)

5. **#4183**[OPEN] — [area:context-memory, models] 自动压缩无法避免 CAPI 5 MB 限制  
   - **摘要**：即使上下文 token 未超限，序列化的 CAPI 请求体可能超过 5 MB（独立限制），导致永久无法调用模型。自动压缩不会缩减工具历史体积。  
   - **为什么重要**：影响长会话的可用性，社区给出 7 个 👍。  
   - [Issue 链接](https://github.com/github/copilot-cli/issues/4183)

6. **#4218**[OPEN] — [triage] 允许用户配置 Auto 模式的模型池  
   - **摘要**：Auto 模式会使用用户计划下的所有可用模型，但用户无法限定哪些模型能被 Auto 选择，导致成本和性能不可预测。  
   - **为什么重要**：与 #4207、#4208 一同反映社区对精细控制模型行为的强烈需求。  
   - [Issue 链接](https://github.com/github/copilot-cli/issues/4218)

7. **#4165**[OPEN] — [area:sessions, platform-windows] `copilot --resume` 在 Windows 上挂起  
   - **摘要**：直接从 PowerShell 执行 `--resume` 会停留在“Resuming session...”无响应，但先启动 CLI 再 resume 正常。  
   - **为什么重要**：Windows 用户的基础流程受阻，影响日常使用。  
   - [Issue 链接](https://github.com/github/copilot-cli/issues/4165)

8. **#4206**[OPEN] — [area:enterprise, mcp] 环境页脚“Loading”无限旋转  
   - **摘要**：即使所有内容已实际加载（`/env` 正常），状态栏依然显示 `◎ Loading: 1 instruction, 40 skills, 1 plugin, 2 agents`，不切换为完成态。  
   - **为什么重要**：企业环境下 MCP 策略手可能引发假死，影响用户信任。  
   - [Issue 链接](https://github.com/github/copilot-cli/issues/4206)

9. **#4212**[OPEN] — [area:theming-accessibility, terminal-rendering] 在 tmux 内提示框和菜单项不可见  
   - **摘要**：深色文本在深色背景上无法识别，仅出现在 tmux 内；分离 tmux 后恢复正常。  
   - **为什么重要**：大量 CLI 重度用户依赖 tmux，可访问性问题亟待解决。  
   - [Issue 链接](https://github.com/github/copilot-cli/issues/4212)

10. **#4222**[OPEN] — [triage] 主面板冻结回归（#2802 复现）  
    - **摘要**：v1.0.72+ 在 VS Code 集成终端（原生 Windows）上再次出现无限 React/Ink 渲染循环，导致输出被吞。  
    - **为什么重要**：该问题曾在 v1.0.31 修复并关闭，如今回归，严重影响开发者内嵌使用。  
    - [Issue 链接](https://github.com/github/copilot-cli/issues/4222)

---

## 重要 PR 进展

当前仅有一条 PR 在过去 24 小时内有更新：

- **#3163**[OPEN] — ViewSonic monitor  
  标题疑似无关内容（“ViewSonic monitor”），摘要中提到“initiate [GitHub action] //runners”，可能是机器人误提交或测试 PR。目前无评审、无合并计划。  
  [PR 链接](https://github.com/github/copilot-cli/pull/3163)

---

## 功能需求趋势

从近期 Issues 中提炼出社区最关注的功能方向：

1. **原生文档支持**（#443）—— 直接读取 PDF 等格式，避免依赖外部工具。  
2. **模型选择精细化**（#4218、#4208）—— 允许用户定义 Auto 模式的可用模型池，支持显式调用特定代理。  
3. **预算与资源可见性**（#4207、#4224）—— 显示每个子代理的 AI 学分消耗，以及 OTel 计费属性缺失问题。  
4. **上下文字段优化**（#1688、#4183）—— 可配置的自动压缩阈值，以及防止 5MB 请求体限制。  
5. **终端集成增强**（#3428）—— OSC 133 序列支持，让终端能跳转到历史提示行。

---

## 开发者关注点

总结开发者在社区反馈中反复提及的痛点和典型问题：

- **Windows 稳定性**：包括 `--resume` 挂起（#4165）、退出时 libuv 崩溃（#4217）、通知功能导致原生崩溃（#4219）—— 多个 issue 指向 Windows 主进程可靠性不足。
- **tmux 兼容性问题**：命令完成检测失败（#4223）、主题渲染不可见（#4212）—— 让使用多路复用器的开发者体验受挫。
- **渲染循环回归**：#4222 复现了 v1.0.31 的无限刷新 bug，表明单元测试或覆盖不足。
- **MCP 与认证回归**：#2282（MCP 连接失败）、#4016（BYOK 在 --acp 被拒）—— 第三方服务和自定义模型集成仍是易碎点。
- **长上下文退化**：#1688（大模型上下文膨胀）、#4183（5MB 请求体限制）—— 提醒团队需要更智能的上下文管理策略。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 | 2026-07-23

## 📰 今日速览
过去 24 小时内社区动态较少，但暴露了两个值得关注的新问题：**MCP 工具 Schema 被 Moonshot API 拒绝（HTTP 400）**，以及 **Windows 中文环境下 stdout 重定向导致启动崩溃**。同时，一项关于文件编辑计数错误的 PR 和一项 Shell 管道阻塞修复 PR 已进入审查阶段。

## 🔍 社区热点 Issues（共 3 条）

### 1. [Bug] 组织级 TPD 速率限制误报（#2318）
- **要点**：kimi 2.6 在 moonshot.ai 平台被错误提示 TPD 达上限（1,505,241），实际请求量远未达到该值。
- **重要性**：影响付费用户正常使用，社区有 2 人 👍，说明非个例。虽已创建两月，但最近一次更新在昨日，表明问题仍未彻底修复。
- **链接**：[#2318](https://github.com/MoonshotAI/kimi-cli/issues/2318)

### 2. [Bug] MCP 工具名称与 Schema 被 Moonshot API 拒绝（#2531）
- **要点**：`kimi-cli 1.49.0` 在 macOS (arm64) 调用 K3 模型时，`tools.function.parameters` 因不符合 Moonshot 专有 JSON Schema 规范（如 `anyOf` 缺少 `type`）报 400 错误。
- **重要性**：新问题，直接阻塞使用 MCP 工具链的开发者，社区尚未有官方工作量回应。
- **链接**：[#2531](https://github.com/MoonshotAI/kimi-cli/issues/2531)

### 3. [Bug] Windows stdout 重定向时 `kimi web` 崩溃（#2532）
- **要点**：中文 Windows 系统下，一旦 stdout 被重定向或由父进程捕获，启动时打印横幅中的 `➜` 字符（U+279C）导致 `UnicodeEncodeError`（gbk），程序立即退出。
- **重要性**：严重影响中文用户及流水线场景（如 CI），且无替代方案。暂无评论，但触发条件常见。
- **链接**：[#2532](https://github.com/MoonshotAI/kimi-cli/issues/2532)

## 🛠️ 重要 PR 进展（共 2 条）

### 1. fix(tools): 修正 StrReplaceFile 替换计数逻辑（#2524）
- **内容**：`StrReplaceFile` 之前按原始文件内容计算替换次数，导致链式编辑（前一次替换产生的新字符串）被错误计数。PR 改为基于运行中已修改内容进行计数。
- **状态**：Open，关联 Issue #2526。
- **链接**：[#2524](https://github.com/MoonshotAI/kimi-cli/pull/2524)

### 2. fix(shell): 避免因分离子进程持有管道导致无限阻塞（#2530）
- **内容**：在 Shell 前台运行路径中，`_run_shell_command` 会等待 stdout/stderr EOF 之后再检查退出码。若命令包含 `some_daemon & echo done`，分离的子进程仍持有管道，导致父进程永远无法收到 EOF，进而超时。PR 引入提前检查退出码机制。
- **状态**：Open，关联 Issue #2468。
- **链接**：[#2530](https://github.com/MoonshotAI/kimi-cli/issues/2530)

## 📊 功能需求趋势
基于近期 Issues（含较早但持续活跃的），社区当前最关注的方向包括：

- **API 兼容性与限流**：组织级 TPD 限速误报（#2318）、MCP Schema 与 Moonshot 专有规范适配（#2531）表明用户对 API 稳定性和向后兼容性高度敏感。
- **跨平台编码适配**：Windows 中文编码问题（#2532）反映 Linux/Mac 优先开发下对 Windows 场景的覆盖不足。
- **Shell 命令行为**：子进程管道导致长时间阻塞（#2530）凸显了异步 Shell 执行逻辑的健壮性需求。
- **工具链内部一致性**：文件编辑计数错误（#2524）虽然较小，但暴露了工具链状态管理的潜在缺陷。

## 👨‍💻 开发者关注点
- **Windows 用户体验**：`kimi web` 因一个 Unicode 字符直接崩溃，这种低级编码问题会严重削弱用户信任，尤其是非英文用户。
- **MCP 扩展性受阻**：MCP Schema 被 API 拒绝对已基于该协议构建工作流的用户是直接打击，需官方尽快提供客户端侧 sanitize 方案或更新 API 文档。
- **限流误判影响生产**：TPD 限速错误导致部分用户无法继续调用，即便升级版本也无法解决，社区反馈两个多月仍未彻底修复，是最高优先级痛点。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 | 2026-07-23

## 今日速览
OpenCode Go 订阅服务出现大规模 **401“请求被上游提供商拦截”** 故障，多个用户在 7 月 22 日起无法调用聊天补全接口，影响范围广泛，目前尚无官方回应。此外，社区对模型自动发现、CPU 空转、Plan/Build 模式回归等功能的呼声持续高涨，多个高赞 Issue 正在推动核心体验改进。

---

## 版本发布
无正式版本发布。当日仅有一条 **PR #38252 的验证视频**（`pr-38252-videos`），记录了该 PR 变更前后的效果对比，未涉及新功能或修复。

---

## 社区热点 Issues（10 条）

### 1. 🔥 **自动发现 OpenAI 兼容提供商的模型**  
**#6231** — `@ochsec` · 185 👍 · 28 💬  
用户希望在配置 LM Studio、Ollama 等本地提供商时，自动从 `/v1/models` 拉取可用模型，避免手动逐个填写。这是社区呼声最高的功能请求之一，已开放半年仍无实质性进展。  
[https://github.com/anomalyco/opencode/issues/6231](https://github.com/anomalyco/opencode/issues/6231)

### 2. 🚨 **Go 订阅全模型返回 401 错误（中文报告）**  
**#38257** — `@lizijiangyyjx` · 8 👍 · 25 💬  
「OpenCode Go」订阅下所有模型调用 `chat/completions` 均被拦截，但 `/v1/models` 可正常访问。用户确认是服务器端问题，影响 Windows / macOS 多设备。  
[https://github.com/anomalyco/opencode/issues/38257](https://github.com/anomalyco/opencode/issues/38257)

### 3. 🚨 **Go 订阅故障：全模型请求被拦截**  
**#38218** — `@1335907208` · 5 👍 · 21 💬  
与 #38257 相同问题，用户提供了详细的复现步骤，强调“无任何 Go 模型可用”。社区出现大量重复报告。  
[https://github.com/anomalyco/opencode/issues/38218](https://github.com/anomalyco/opencode/issues/38218)

### 4. 🐛 **等待 API 限速时 CPU 空转占用 50%**  
**#19466** — `@Jaaaky` · 11 👍 · 15 💬  
当触发速率限制（`Resource has been exhausted`）并进入重试等待时，单核 CPU 占用高达 50%，影响 i9-14900 机型。版本 1.3.3 至今未修复，已持续 4 个月。  
[https://github.com/anomalyco/opencode/issues/19466](https://github.com/anomalyco/opencode/issues/19466)

### 5. 🚨 **Go 订阅 401 错误（英文报告）**  
**#38195** — `@faustkuroki` · 15 👍 · 15 💬  
Free 模型正常，Go 模型全部 401。用户提到在 OpenCode Desktop 和 Hermes 上均复现，推测为上游认证问题。  
[https://github.com/anomalyco/opencode/issues/38195](https://github.com/anomalyco/opencode/issues/38195)

### 6. 🚨 **Go 订阅 401 错误（已关闭但仍有影响）**  
**#38190** — `@sosigboys` · 12 👍 · 13 💬  
初始报告，提出“Request blocked by upstream provider”，但 Issue 被标记为 `CLOSED`，可能未得到实质修复，社区继续在其他 Issue 中反馈。  
[https://github.com/anomalyco/opencode/issues/38190](https://github.com/anomalyco/opencode/issues/38190)

### 7. 🚨 **俄语用户报告相同 Go 问题**  
**#38293** — `@123123adwad` · 0 👍 · 15 💬  
用俄语描述了与前述相同的 401 故障，表明该问题已波及非英语用户群体，影响面进一步扩大。  
[https://github.com/anomalyco/opencode/issues/38293](https://github.com/anomalyco/opencode/issues/38293)

### 8. 🔥 **Plan/Build 模式被最新版移除**  
**#37970** — `@BillyJack76` · 1 👍 · 10 💬  
用户反馈 v1.18.0 删除了“Plan only”和“Build only”模式切换，导致无法控制模型行为。部分情况下偶现 Plan，但整体不可靠。  
[https://github.com/anomalyco/opencode/issues/37970](https://github.com/anomalyco/opencode/issues/37970)

### 9. 🐛 **Web 版 VSCode 中剪贴板复制失败**  
**#26459** — `@xuxusheng` · 1 👍 · 7 💬  
在 code-server、GitHub Codespaces 等远程环境中，UI 显示“已复制到剪贴板”，但实际未复制。影响大量远程开发者。  
[https://github.com/anomalyco/opencode/issues/26459](https://github.com/anomalyco/opencode/issues/26459)

### 10. 💡 **feature: read 工具支持音频/视频附件**  
**#22260** — `@soaringk` · 7 👍 · 7 💬  
目前 `read` 工具只能返回图片和 PDF，对音视频文件直接拒绝。用户希望模型能本地检视媒体文件并作为多模态附件传递给模型。  
[https://github.com/anomalyco/opencode/issues/22260](https://github.com/anomalyco/opencode/issues/22260)

---

## 重要 PR 进展（10 条）

### 1. 🔧 **修复 `/api/generate` 动态模型加载**  
**#38401** — `@kitlangton` — `OPEN`  
允许无状态 `/api/generate` 路径使用动态加载的 AI SDK 模型（如 `opencode/gemini-3.5-flash`），解决此前因包不兼容导致的“不受支持”错误。  
[https://github.com/anomalyco/opencode/pull/38401](https://github.com/anomalyco/opencode/pull/38401)

### 2. 📘 **新增 V2 TUI 主题参考文档**  
**#38396** — `@jlongster` — `CLOSED`  
从 Effect Schema 自动生成 V2 主题令牌层次结构，并添加了开发、CI 文档验证流程，确保主题文档与实现同步。  
[https://github.com/anomalyco/opencode/pull/38396](https://github.com/anomalyco/opencode/pull/38396)

### 3. 🎨 **TUI 语法高亮基于 V2 主题生成**  
**#38397** — `@jlongster` — `OPEN`  
将完整的 TUI 语法样式（`SyntaxStyle`）直接从 V2 令牌映射，移除 V1 并行解析，同时保留 mini-TUI 兼容性。  
[https://github.com/anomalyco/opencode/pull/38397](https://github.com/anomalyco/opencode/pull/38397)

### 4. 🧪 **子会话事件通过 NDJSON 流输出**  
**#33403** — `@cHIsIMun` — `CLOSED`  
`opencode run --format json` 现在会转发子会话（`task` 工具生成的子 agent）事件到输出流，解决此前子会话事件被过滤的问题。  
[https://github.com/anomalyco/opencode/pull/33403](https://github.com/anomalyco/opencode/pull/33403)

### 5. 📊 **修复会话摘要统计为零**  
**#33444** — `@aic0d3r` — `CLOSED`  
#30127 的更改导致 `session.summary` 中的 `files`、`additions`、`deletions` 全部归零。此 PR 通过从每轮差异（diff）中恢复会话摘要来修复。  
[https://github.com/anomalyco/opencode/pull/33444](https://github.com/anomalyco/opencode/pull/33444)

### 6. 🌐 **WebFetch 区分 URL 错误与网络错误**  
**#33393** — `@lexlian` — `CLOSED`  
之前 WebFetch 将所有失败（格式、超时、过大等）混为一谈。现在分别返回 `InvalidUrl`、`Timeout`、`ResponseTooLarge` 等明确错误类型。  
[https://github.com/anomalyco/opencode/pull/33393](https://github.com/anomalyco/opencode/pull/33393)

### 7. 📦 **支持发现插件目录（含 package.json）**  
**#33391** — `@licat2023` — `CLOSED`  
`opencode.jsonc` 中的本地插件现在可以指向一个目录（而非具体文件），系统会解析其中的 `package.json` 或 `index.*` 作为入口。  
[https://github.com/anomalyco/opencode/pull/33391](https://github.com/anomalyco/opencode/pull/33391)

### 8. 🚫 **拒绝对不存在的目录发起实例请求**  
**#33309** — `@weiconghe` — `CLOSED`  
当用户移动项目目录后，Desktop 客户端缓存了旧路径，试图打开时会发送无效请求。此 PR 在服务器端检查目录是否存在，不存在则拒绝请求。  
[https://github.com/anomalyco/opencode/pull/33309](https://github.com/anomalyco/opencode/pull/33309)

### 9. ✍️ **修复 Markdown 标题层级大小**  
**#33284** — `@akinshaywai` — `CLOSED`  
`markdown.css` 中所有 `<h1>`~`<h6>` 共用 14px 字号，导致标题没有视觉梯度。此 PR 恢复了差异化字号。  
[https://github.com/anomalyco/opencode/pull/33284](https://github.com/anomalyco/opencode/pull/33284)

### 10. 🧩 **防止 VirtualTimelineRow 因 undefined 崩溃**  
**#33287** — `@SisyphusZheng` — `CLOSED`  
修复虚拟时间线组件在 `initialItem` 或 `row` 为 `undefined` 时抛出 `TypeError: Cannot read properties of undefined` 的崩溃问题。  
[https://github.com/anomalyco/opencode/pull/33287](https://github.com/anomalyco/opencode/pull/33287)

---

## 功能需求趋势
从本期大量 Issues 中，社区最关注的四大功能方向如下：

- **模型自动发现与本地提供商优化**（#6231、#18011）：手动配置模型列表繁琐且易错，自动从 `/v1/models` 获取模型是高频呼声。
- **OpenCode Go 订阅服务稳定性**：当日 7 个 Issue 直指同一 401 错误，急需官方排查上游认证链。
- **Agent 行为控制（Plan/Build 模式）**（#37970、#38364）：用户高度依赖手动切换“仅规划”或“仅执行”模式，最新版本删除后引发持续反馈。
- **性能与资源优化**：CPU 空转（#19466）、令牌累积（#38344）、子会话泄漏（#37314）均被反复提出，表明中长会话下资源管理仍是短板。
- **远程环境兼容性**：剪贴板（#26459）、终端 FPS 限制（#13817）等 Issue 显示大量用户通过 code-server 等远程方案使用，需要针对性修复。

---

## 开发者关注点
- **Go 订阅 401 故障**：7 月 22 日突然出现的全模型拦截，Free 模型正常工作，推测为上游认证服务变更。社区尚无官方回复或 hotfix，开发者被迫回退至 Free 模型或转用其他服务。
- **更新破坏性变更**：v1.18.0 删除 Plan/Build 模式切换，且部分用户反馈更新后丢失工作数据（#38358），暴露出更严格的版本管理需求。
- **子会话资源泄漏**：父会话异常退出后，子 agent 持续存活且占用工具调用状态（#37314），长时间会话下影响生产环境稳定性。
- **MCP 工具排除无效**：全局配置 `"mymcpserver_*": false` 无法屏蔽 MCP 工具（#37675），实际发送给模型时仍包含禁用工具，导致不必要调用。
- **权限映射错误**：`EDIT_TOOLS` 常量使用 `"patch"` 但实际工具名为 `"apply_patch"`（#16028），导致编辑权限错误开放或受限。

---

> 日报数据来源：https://github.com/anomalyco/opencode  
> 统计截止：2026-07-23 UTC

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-07-23

## 📰 今日速览

- **v0.20.0-preview.0 发布**：该预览版主要包含遥测 daemon 指标初始化顺序的测试覆盖与文档改进，为正式版做最后准备。
- **核心测试持续红色**：`main` 分支的 `agent.test.ts` 因 fork 调度的 registry 完成断言问题导致 CI 全面报红，多个 PR 提交了修复方案。
- **多起更新检查失败问题被集中报告**：`getNpmCliPath` 在版本管理器环境下误将 shell wrapper 当作 npm-cli.js，引发 `registry error`，社区提交了多个 PR 进行修复。

---

## 🚀 版本发布

### v0.20.0-preview.0
- **说明**：下一个稳定版的预览。本次仅包含一项改动：`test(telemetry): Cover daemon metrics init ordering and document metricReader asymmetry`（PR #7456），提升了遥测系统的健壮性。
- **完整变更**：[v0.20.0-preview.0](https://github.com/QwenLM/qwen-code/releases/tag/v0.20.0-preview.0)

### v0.20.0-nightly.20260722.b98306b7e
- **说明**：同日发布的 nightly 版本，包含与 preview 相同的遥测测试改进。

### v0.0.0-benchmark-poc.20260722.1
- **说明**：临时预发布版本，用于验证 GitHub Actions → ECS 基准运行工作流的端到端发布路径，并非产品发布。

---

## 🔥 社区热点 Issues（10 条）

### 1. [#7284] bug(core): side-query 强制禁用 thinking，破坏需要 thinking 的 TokenPlan 端点
- **优先级**：P1（严重）
- **摘要**：`runSideQuery` 在调用 DashScope/TokenPlan 时总是发送 `enable_thinking: false`，导致某些端点返回 400 错误。已关闭（修复可能合入）。
- **评论**：5 条 | **👍**：0
- **链接**：https://github.com/QwenLM/qwen-code/issues/7284

### 2. [#7316] Bug：OpenAI 兼容模型的 toolCall 导致 subAgent 完全无法使用
- **优先级**：P2
- **摘要**：使用 `isolation: "worktree"` 调用 agent 工具时，部分 OpenAI 模型为可选参数返回空字符串，引发互斥字段冲突，subAgent 无法正常工作。
- **评论**：5 条 | **👍**：0
- **链接**：https://github.com/QwenLM/qwen-code/issues/7316

### 3. [#7306] Harden tool-output budgeting, observability, and artifact lifecycle
- **优先级**：P2
- **摘要**：提议改善工具输出预算的健壮性、可观测性及产物生命周期管理。Phase 1 已合并（#7323 和 #7470），Phase 2 待讨论。
- **评论**：4 条 | **👍**：0
- **链接**：https://github.com/QwenLM/qwen-code/issues/7306

### 4. [#7449] proposal(memory): 定义企业级外部内存集成规范
- **优先级**：P3（功能请求）
- **摘要**：提出一个与供应商无关的企业外部内存集成方案，文档优先，核心 API 不发生变更。
- **评论**：4 条 | **👍**：0
- **链接**：https://github.com/QwenLM/qwen-code/issues/7449

### 5. [#7537] 核心测试红色：fork 调度测试始终看不到 registry.complete
- **优先级**：P1（严重）
- **摘要**：`packages/core` 的 `test:ci` 在 `main` 上失败，导致所有 PR 的 Ubuntu CI 变红，无论 PR 内容如何。
- **评论**：2 条 | **👍**：0
- **链接**：https://github.com/QwenLM/qwen-code/issues/7537

### 6. [#7489] VS Code Companion：文件选择器插入 @filename 但图片未实际附加到模型
- **优先级**：未标记
- **摘要**：VS Code 插件中使用附件图标选择图片时，仅插入文本引用，图片本身并未发送给模型。已收到初步诊断。
- **评论**：3 条 | **👍**：0
- **链接**：https://github.com/QwenLM/qwen-code/issues/7489

### 7. [#7287] auto-memory MEMORY.md 被加载到 system prompt 但未注册到 FileReadCache，首次写入总是被拒绝
- **优先级**：P2
- **摘要**：会话启动时 auto-memory 加载 MEMORY.md 内容到提示词中，但未记录读取记录，导致后续 write_file 因 `checkPriorRead()` 失败而拒绝写入。
- **评论**：3 条 | **👍**：0
- **链接**：https://github.com/QwenLM/qwen-code/issues/7287

### 8. [#7404] 启动后检查更新超时时间太短，加载较长旧会话时基本必超时
- **优先级**：P3
- **摘要**：启动时版本更新检查的超时阈值设置过短，当加载大量历史会话时，网络请求必然超时失败。
- **评论**：4 条 | **👍**：0
- **链接**：https://github.com/QwenLM/qwen-code/issues/7404

### 9. [#7500] bug(serve): --open 在端口冲突后使用旧端口
- **优先级**：P2
- **摘要**：`qwen serve` 在请求端口被占用时自动尝试下一端口，但 `--open` 选项仍然打开原始（被占用）的端口，导致打开错误 URL。
- **评论**：2 条 | **👍**：0
- **链接**：https://github.com/QwenLM/qwen-code/issues/7500

### 10. [#7515] Failed to check for updates (registry error)
- **优先级**：P3
- **摘要**：自 v0.20.1 起 `/update` 或 `qwen update` 总是失败，显示注册表错误。用户已确认直接访问 npm registry 可正常工作。
- **评论**：2 条 | **👍**：0
- **链接**：https://github.com/QwenLM/qwen-code/issues/7515

---

## 🔧 重要 PR 进展（10 条）

### 1. [#7471] feat(web-shell): 添加新会话的 git 模式选择器
- **状态**：OPEN
- **摘要**：在 Web Shell 的 composer 工具栏新增 git chip 弹出选择器，用户可为新会话选择三种 git 工作流：当前分支、新建分支、分离 HEAD。
- **链接**：https://github.com/QwenLM/qwen-code/pull/7471

### 2. [#7540] test(core): 在 agent 测试注册表中 stub resident-agent 方法
- **状态**：CLOSED（已合并）
- **摘要**：修复 `main` 上的 CI 红色问题：agent.test.ts 中的 fork 完成断言因 stub registry 未实现 complete 而失败。在 `beforeEach` 中添加了空实现。
- **链接**：https://github.com/QwenLM/qwen-code/pull/7540

### 3. [#7493] fix(vscode): 使用文件选择器图片路径进行视觉输入
- **状态**：OPEN
- **摘要**：修复 VS Code 插件中图片附件无法发送到模型的 bug：现在 chat input 中插入转义后的绝对路径，而非仅文件名。
- **链接**：https://github.com/QwenLM/qwen-code/pull/7493

### 4. [#7548] fix(sdk-python): 将 max_tool_calls 和 max_subagent_depth 验证为整数
- **状态**：OPEN
- **摘要**：这两个参数仅进行了范围检查，未像 `max_session_turns` 那样拒绝布尔值和字符串。统一抽取整数检查逻辑。
- **链接**：https://github.com/QwenLM/qwen-code/pull/7548

### 5. [#7546] fix(core): 转换以 schema 关键字命名的属性下的子 schema
- **状态**：OPEN
- **摘要**：`convertTypes` 在递归嵌套对象前先检查 JSON Schema 约束关键字列表，导致属性名为 `additionalProperties` 等的子 schema 未能正确转换。将对象递归提前修复此问题。
- **链接**：https://github.com/QwenLM/qwen-code/pull/7546

### 6. [#7531] fix(core): 关闭 AUTO 破坏性 git 守卫中的 force-flag 和 checkout 空隙
- **状态**：OPEN
- **摘要**：`DESTRUCTIVE_GIT_PATTERNS` 未覆盖 `git clean -f` 和 `git checkout --force` 等变体，现在添加了更宽的模式匹配。
- **链接**：https://github.com/QwenLM/qwen-code/pull/7531

### 7. [#7527] fix(core): 从 hook 和 tool-discovery 子进程环境中剥离 daemon 密钥
- **状态**：OPEN
- **摘要**：继 #7256 之后，继续对剩余的三个 agent 启动的子进程（hookRunner、toolDiscovery）应用 `sanitizeChildEnv()`，防止敏感环境变量泄漏。
- **链接**：https://github.com/QwenLM/qwen-code/pull/7527

### 8. [#7545] fix(cli): 停止将版本管理器的 npm shim 当作 npm-cli.js
- **状态**：OPEN
- **摘要**：更新检查逻辑现在验证解析到的路径是否为 JavaScript 文件，避免将 mise、asdf 等版本管理器的 shell 包装误认为 npm-cli.js。
- **链接**：https://github.com/QwenLM/qwen-code/pull/7545

### 9. [#7542] feat(cli): 添加版本升级通知
- **状态**：OPEN
- **摘要**：启动时为新版本显示“有何新功能”摘要（针对重点发布），每个支持的版本只显示一次，支持屏幕阅读器。
- **链接**：https://github.com/QwenLM/qwen-code/pull/7542

### 10. [#7541] fix(core): 保留禁用的 reasoning effort 配置
- **状态**：OPEN
- **摘要**：结构化 side-query 的强制函数调用原本会移除所有 reasoning_effort，现在保留显式设置的 `"none"` 值，避免不必要地清除用户的推理禁用配置。
- **链接**：https://github.com/QwenLM/qwen-code/pull/7541

---

## 🧭 功能需求趋势

从近期 Issues 与 PR 中可归纳出社区最关注的 4 个功能方向：

| 方向 | 典型议题 | 说明 |
|------|---------|------|
| **IDE 集成与 Web Shell 增强** | #7489, #7471, #7493, #6701, #6700 | VS Code 插件图片附件修复、Web Shell 新会话的 git 和工作区选择器、更多上下文控制。 |
| **安全加固与环境隔离** | #6601, #7527, #7531 | Shell 子进程泄漏密钥、git 破坏性命令守卫、子进程环境变量清洗。 |
| **外部记忆与企业集成** | #7449 | 提出企业级外部记忆集成规范，预期后续会有更多存储/知识图谱支持。 |
| **工具与子代理可靠性** | #7284, #7298, #7316, #7306 | web_fetch 失败自动回退、子代理工具调用兼容性、工具输出预算与可观测性。 |

---

## 🧑‍💻 开发者关注点

- **更新检查频繁失败**：多起报告（#7515, #7543, #7404）指出更新机制在版本管理器（mise/asdf）环境下不可靠，且超时过短导致加载大会话时失败。社区贡献了 #7545、#7544 等多个修复 PR。
- **核心测试持续红色**：`main` 分支的 agent.test.ts 因 registry.complete 未实现而失败，阻塞所有 PR 的 CI（#7537）。已提交 #7540 并合并。
- **VS Code 插件图片附件未实际发送**：文件选择器的图片路径被当作文本插入，模型无法“看见”图片（#7489）。对应的修复 PR #7493 已提交。
- **Web Shell 端口冲突行为异常**：`--open` 选项未跟随端口的自动回退，导致打开错误地址（#7500）。影响开发者体验。
- **DingTalk 集成数据隐私问题**：群聊中同时 @机器人与其他成员时，文字内容被 DingTalk 删除，丢失非机器人提及的元数据（#7472）。已修复。
- **推理侧查询（side-query）强制禁用 thinking**：多个现有 Issue（#7284, #7440）反映 web_fetch 等内部查询强制关闭 thinking，导致与需要 thinking 的端点不兼容。社区提交了 #7534 进行重试逻辑修复。

---

> **报告周期**：2026-07-22 14:00 UTC → 2026-07-23 14:00 UTC  
> **数据来源**：[github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*