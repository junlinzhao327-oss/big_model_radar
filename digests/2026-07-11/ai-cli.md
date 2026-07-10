# AI CLI 工具社区动态日报 2026-07-11

> 生成时间: 2026-07-10 22:36 UTC | 覆盖工具: 7 个

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

好的，作为一名专注于 AI 开发工具生态的资深技术分析师，我已经仔细审阅了您提供的各主流 AI CLI 工具的社区动态摘要。基于这些数据，现为您生成一份横向对比分析报告。

---

### AI CLI 工具生态横向对比分析报告（2026-07-11）

#### 1. 生态全景

当前AI CLI工具市场整体处于 **“模型换代阵痛”与“功能深度拓展”** 并存的阶段。以 **Claude Code (Fable 5)** 和 **OpenAI Codex (Sol)** 为代表的新模型上线，引发了大规模社区反馈，主要集中在 **模型行为不可预测、指令遵循度下降和安全护栏过度敏感** 等问题，表明工具正从“可用”向“可靠、可控”进化。同时，**多Agent协作、MCP集成和平台兼容性（尤其是Windows/Linux）** 成为开发者的核心诉求，各工具在持续修复Bug的同时，也在通过引入健康检查、技能创建和多工作区支持等功能，深化开发者工作流程的覆盖。

#### 2. 各工具活跃度对比

| 工具名称 | 24h Issues | 24h PRs | 最新 Release | 核心关注点 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 10 (活跃) | 5 | v2.1.206 | Fable 5 模型行为、MCP Chrome 稳定性、Token 消耗 |
| **OpenAI Codex** | 10 (密集) | 10 | rust-v0.144.1 / alpha.2 | GPT-5.6 Sol 多Agent问题、Azure 兼容性、子Agent模型控制 |
| **Gemini CLI** | 10 | 10 | v0.52.0-nightly | Agent 超时/卡死、Memory 死循环、安全漏洞修复 |
| **Copilot CLI** | 10 | 0 | v1.0.71-0 | Alpine/Windows 稳定性、MCP OAuth 故障、模型能力降级 |
| **Kimi Code CLI** | 0 | 4 | 无 | Agent 工具绑定丢失、新用户引导、Safari 兼容性 |
| **OpenCode** | 50+ | 50+ | 未显示 | GPT-5.6 模型支持、SQLite 损坏、Xcode ACP 问题 |
| **Qwen Code** | 10 | 10 | v0.19.9 | 多工作区支持、MCP OAuth、子Agent安全/循环问题 |

**总结：** **OpenCode** 和 **Qwen Code** 在 Issues 和 PR 数量上远超其他工具，社区反馈极其密集，处于快速迭代期。**Claude Code**、**OpenAI Codex** 和 **Gemini CLI** 的活跃度很高，集中在模型问题与功能改进。**Copilot CLI** 反馈多但开发响应（PR）较少，存在稳定性隐忧。**Kimi Code CLI** 当日无新 Issue，社区活动相对平稳。

#### 3. 共同关注的功能方向

| 功能方向 | 涉及工具 | 具体诉求 |
| :--- | :--- | :--- |
| **模型行为可预测性** | **Claude Code**、**OpenAI Codex**、**Gemini CLI** | 抱怨模型“自作主张”、不遵循指令、自动重路由、拒绝执行任务，用户希望获得更可控、更透明的AI行为。 |
| **MCP集成稳定性** | **Claude Code**、**Copilot CLI**、**Qwen Code** | Windows平台MCP Chrome导航失效、OAuth流程故障、连接不稳、工具暴露不完整，MCP生态的基建仍需打磨。 |
| **子Agent/多Agent精细控制** | **OpenAI Codex**、**Gemini CLI**、**Qwen Code** | 子Agent模型不可选、超时后误报成功、无限循环等问题，用户希望拥有对子Agent行为、模型、环境的完全控制权。 |
| **跨平台兼容性** | **Claude Code**、**Copilot CLI**、**OpenCode**、**Qwen Code** | Windows (WSL2, TUI黑屏/段错误)、Alpine Linux (段错误)、macOS (休眠断连)等问题频发，影响主流开发者使用。 |
| **Token/成本透明与控制** | **Claude Code**、**OpenAI Codex** | 用户抱怨Token消耗大但无进展，希望有预算提醒、阶段性输出和更清晰的成本信息。 |

#### 4. 差异化定位分析

| 工具名称 | 功能侧重 | 目标用户 | 技术路线 |
| :--- | :--- | :--- | :--- |
| **Claude Code** | **安全性与文档管理** | 注重代码安全、文档规范的企业团队 | 强调 `/doctor`、安全指导插件、XSS防护，围绕 `CLAUDE.md` 打造知识管理闭环。 |
| **OpenAI Codex** | **多Agent与模型灵活性** | 需要灵活编排Agent、实验不同模型的开发者 | 深度集成GPT-5生态，强调MultiAgent V2、子Agent模型选择和插拔能力。 |
| **Gemini CLI** | **记忆系统与安全沙箱** | 关注Agent持久记忆和开发环境安全的高级用户 | 着力构建Memory模块，探索利用模型原生能力实现零依赖沙箱，强调A2A协议安全。 |
| **Copilot CLI** | **生态整合与插件市场** | GitHub重度用户、希望统一管理AI插件的团队 | 深度绑定GitHub Copilot，通过MCP和插件市场构建扩展生态，但MCP稳定性目前是短板。 |
| **Kimi Code CLI** | **Web端体验与本土化** | 追求Web端轻量体验、中文本地化用户 | 侧重Web UI打磨、Safari/中文输入法兼容，新用户引导做得好。 |
| **OpenCode** | **工具链整合中心** | 需要跨多个AI提供商、管理复杂工作流的开发者 | 定位为“AI提供者Hub”，支持OpenAI、Anthropic、Copilot等多模型，强调可编程插件和DB持久化。 |
| **Qwen Code** | **交互式学习与多工作区** | 希望从“对话”转向“技能沉淀”的团队 | 首创 `/learn` 命令，将交互知识固化为可复用技能；推进多工作区管理（`qwen serve`）服务器化。 |

#### 5. 社区热度与成熟度评估

-   **最活跃与快速增长期**：**OpenCode** 和 **Qwen Code**。两者 Issues/PR 数量惊人，功能快速迭代，社区参与度极高，但也暴露出大量稳定性问题（如SQLite损坏、子Agent循环）。
-   **高热度与成熟度，但正经历模型换代阵痛**：**Claude Code** 和 **OpenAI Codex**。社区用户基数大，对模型变化非常敏感。新模型上线的负面反馈（Issues被广泛关注并关闭）表明核心模型的质量直接决定了工具的社区情绪。
-   **稳健迭代期**：**Gemini CLI** 和 **Kimi Code CLI**。更新节奏稳定，修复Bug与新增功能并行，社区反馈热度不如前两者，但质量较高，探索性功能（如零依赖沙箱）值得关注。
-   **发展隐忧**：**Copilot CLI**。虽然版本更新和新功能（如固定提示）不错，但当日0 PR合并，且社区核心痛点（如Alpine段错误、TUI死机）长期未解，可能影响其作为GitHub生态核心竞争力的发展。

#### 6. 值得关注的趋势信号

1.  **从“模型能力”竞争转向“模型行为可靠”竞争**：Fable 5 和 Sol 的负面评价表明，单纯的模型能力提升已不能取悦开发者。**指令遵循、行为可预测、安全护栏精准** 成为决定工具成败的关键。开发者对“AI自作主张”零容忍。
2.  **“多Agent协作”成为核心用例，但挑战巨大**：各工具都在押注多Agent/子Agent，但随之而来的模型控制、任务编排、结果一致性、成本爆炸等问题已成为社区反馈的重灾区。能够优雅解决这些问题的工具将占据制高点。
3.  **平台兼容性是普及的硬门槛**：Windows (WSL2) 和 Alpine Linux 的稳定性问题是所有工具的通病。未来，AI CLI 工具若不能像传统IDE一样提供丝滑的跨平台体验，将很难吸引主流开发者。
4.  **“上下文管理”和“Token成本”是长会话体验的瓶颈**：无论是 Claude Code 的 Token 浪费，还是 OpenAI Codex 的上下文占满“线程死亡”，都指向一个核心：**缺乏高效的上下文压缩、恢复和预算控制机制**。这将是影响用户留存的关键因素。
5.  **从“对话”到“技能沉淀”的范式转变**：Qwen Code 的 `/learn` 命令是一个极具前瞻性的信号。它标志着AI工具正从一次性问答助手，向与团队知识库协同演进的、能够自我进化的开发伙伴转变。这可能是下一代AI开发工具的终极形态。

**对开发者的建议**：
-   如果追求**稳定和安全**，优先关注 Claude Code 的 `/doctor` 和 XSS 防护，但需警惕 Fable 5 模型的波动。
-   如果需要**强多Agent编排**，深入研究 OpenAI Codex 的 MultiAgent V2，但要准备好应对子Agent的精细化和兼容性问题。
-   如果希望**构建团队级AI工作流**，密切关注 Qwen Code 的 `/learn` 和多工作区能力，以及 OpenCode 的提供商整合能力。
-   **所有用户**：升级到各工具的最新版本以获取最近的Bug修复和安全补丁；对于模型行为问题，考虑回退到被认为更稳定的旧模型或切换模型版本。保持耐心，AI CLI工具正处在快速迭代期。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，作为一名专注于 Claude Code 生态的技术分析师，我已根据您提供的 github.com/anthropics/skills 仓库数据（截止 2026-07-11），为您整理出以下社区热点报告。

---

### Claude Code Skills 社区热点报告 (截至 2026-07-11)

#### 1. 热门 Skills 排行

以下为社区关注度最高的 5 个 Skills（PR），按讨论热度排序：

1.  **#1298: 修复 skill-creator 的 `run_eval.py` 报告 0% 召回率**
    *   **功能**: 该 PR 并非一个独立 Skill，而是对 `skill-creator` 工具链的核心修复。它解决了 `run_eval.py`（以及依赖它的 `run_loop.py` 和 `improve_description.py`）在所有场景下都错误报告 0% 召回率的严重 Bug，并优化了 Windows 兼容性。
    *   **社区热点**: 这是当前社区最核心的痛点。大量用户（Issue #556, #1169）报告即使使用精确的斜杠命令，评估流程也无法正确识别技能触发，导致优化循环完全失效。讨论集中于这个 Bug 的破坏性（使技能描述优化成为“废物”），以及修复方案的完整性。
    *   **状态**: [Open](https://github.com/anthropics/skills/pull/1298)

2.  **#514: 新增 `document-typography` 技能**
    *   **功能**: 为 AI 生成的文档提供排版质量控制，重点解决孤立单词、孤行段落和编号错位等常见问题。
    *   **社区热点**: 讨论焦点在于这个 Skill 的实用性和必要性。用户普遍认为 Claude 生成的文档在这些细节上确实存在瑕疵，该 Skill 能显著提升文档的专业度和可读性。
    *   **状态**: [Open](https://github.com/anthropics/skills/pull/514)

3.  **#1367: 新增 `self-audit` 技能（v1.3.0）**
    *   **功能**: 一个通用的输出审计技能。在交付前进行“机械文件验证”和“四维推理质量门控”，按危害严重性顺序评估 AI 输出的正确性。
    *   **社区热点**: 这是一个高阶、创新的 Skill。社区讨论了其“防御性编程”理念，即通过自审计来弥补模型在长上下文或复杂任务中可能出现的逻辑错误，被视为提升 AI Agent 可信度的重要尝试。
    *   **状态**: [Open](https://github.com/anthropics/skills/pull/1367)

4.  **#538 & #541: 修复 PDF 和 DOCX Skills 的 Bug**
    *   **功能**: 这两个 PR 是对现有文档处理 Skills 的修复。#538 修复了 `pdf` Skill 在区分大小写的文件系统上的引用错误；#541 修复了 `docx` Skill 在处理已有书签文档时，因 `w:id` 冲突导致文档损坏的问题。
    *   **社区热点**: 讨论聚焦于具体技术细节，如 OOXML 标准、文件系统兼容性。这表明社区中有大量用户在生产环境中使用这些 Skills，对稳定性和兼容性要求很高。
    *   **状态**: [Open](https://github.com/anthropics/skills/pull/538) 和 [Open](https://github.com/anthropics/skills/pull/541)

5.  **#83: 新增 `skill-quality-analyzer` 和 `skill-security-analyzer` 元技能**
    *   **功能**: 添加两个元技能：一个用于评估 Skill 的质量（结构、文档等五个维度），另一个用于评估其安全性（如提示注入风险、越权行为）。
    *   **社区热点**: 这两项技能被认为是提升整个 Skills 生态水平的关键基础设施。社区讨论重点在于如何定义质量标准，以及安全分析的必要性，尤其是在官方分发渠道出现安全隐患的背景下。
    *   **状态**: [Open](https://github.com/anthropics/skills/pull/83)

#### 2. 社区需求趋势

从 Issues 分析，社区当前最期待的新 Skill 方向主要集中在：

*   **安全与治理 (Security & Governance)**: `#492` 引发了关于社区 Skills 官方身份授权和信任边界滥用的热烈讨论（34条评论）。社区强烈需求一个清晰的 Skills 安全和认证机制，以区分官方、社区验证和第三方 Skills。
*   **组织和团队协作 (Org Collaboration)**: `#228` 要求实现组织级的 Skill 共享功能（14条评论、7个👍），而不是手动下载和上传文件，这表明 Skills 正在从个人工具向团队协作工具演进。
*   **基础设施修复 (Infrastructure Fixes)**: `#556` 和 `#1169` 揭示的 `run_eval.py` 0% 召回率问题是社区最大的技术痛点（共15条评论、8个👍）。社区迫切希望`skill-creator`工具链本身是可靠且跨平台（Windows）的。
*   **高级推理与质量控制 (Advanced Reasoning & Quality)**: `#412` 和 `#1329` 等提案（共15条评论）表明，社区已不满足于简单的任务生成，转而探索更复杂的模式，如 Agent 治理、紧凑的状态记忆表示和推理质量门控（#1385）。

#### 3. 高潜力待合并 Skills

以下 PR 讨论活跃，具有较高实用价值，可能在未来短期内合并：

*   **#1298: `run_eval.py` 0% 召回率修复**: **合并可能性极高**。这是当前生态工具链的核心 Bug。多个 PR (#1099, #1050, #362, #1302) 都在尝试修复同一问题的不同侧面，说明社区正在合力解决，一旦共识达成，将快速合并。
*   **#1323: 修复 `run_eval` 触发检测** | [链接](https://github.com/anthropics/skills/pull/1323): 同样是针对 `run_eval.py` 的修复，与 #1298 高度相关，可能会与 #1298 合并或作为互补方案被采纳。
*   **#1367: `self-audit` 自我审计技能** | [链接](https://github.com/anthropics/skills/pull/1367): 概念新颖且实现方案详尽，代表了社区对 AI 输出可靠性的追求。如果质量过硬，有很大机会被合并。
*   **#514: `document-typography` 文档排版技能** | [链接](https://github.com/anthropics/skills/pull/514): 解决了一个普遍存在的体验问题，实用性强，争议小，合并概率较高。
*   **#1302: `color-expert` 颜色专家技能** | [链接](https://github.com/anthropics/skills/pull/1302): 一个专业且独立的知识密集型技能，填补了现有技能库在色彩领域的空白，具有独特的价值。

#### 4. Skills 生态洞察

**一句话总结**: 当前社区最集中的诉求是 **“让核心技能评估工具链稳定可靠”**，并同步探索从“工具化”向“工程化”与“治理化”的深层演进。

---

# Claude Code 社区动态日报 | 2026-07-11

## 今日速览
- **版本 v2.1.206 发布**：新增 `/cd` 目录路径建议、`/doctor` 健康检查（可裁剪冗余 `CLAUDE.md`）、`/commit-push-pr` 自动允许 `git push`。
- **社区情绪波动**：Fable 5 模型上线后收到大量负面反馈（超过30条 Issue），主要集中在模型“自作主张”、安全护栏误触发、Token 浪费及执行偏差。
- **MCP Chrome 集成 bug 持续悬而未决**：#49979 仍然是 Windows 平台最高赞 bug，用户无法正常使用 Chrome MCP 导航与页面读取。

## 版本发布

### v2.1.206（最新）
- **更新内容**：
  - `/cd` 命令现在会像 `/add-dir` 一样提供目录路径建议，提升导航效率。
  - 新增 `/doctor` 检查项：可建议裁剪版本控制中的 `CLAUDE.md` 文件中那些模型能从代码库自动推导的内容，帮助保持文档精简。
  - `/commit-push-pr` 工作流现在自动允许 `git push` 到仓库已配置的远程地址，减少手动确认次数。
- **建议**：运行 `claude doctor` 检查项目健康度，并考虑启用 `CLAUDE.md` 裁剪功能。

---

## 社区热点 Issues（10 条）

### 1️⃣ [BUG] MCP Chrome 导航与读取在 Windows 11 上完全不可用
- **#49979** (评论: 9, 👍: 2)
- **摘要**：从 Claude Desktop（Windows 11）调用 `Claude_in_Chrome__navigate` 和 `read_page` 时所有域名均被拒绝，且无审批弹窗。关联多个重复 Issue（#27073, #20887, #43538, #41034），说明此 bug 长期存在且影响面广。
- **🔗** https://github.com/anthropics/claude-code/issues/49979

### 2️⃣ [DOCS] WSL2 图片粘贴文档遗漏 Windows 剪贴板回退细节
- **#57440** (评论: 2)
- **摘要**：WSL2 用户发现官方“Work with images”文档仅提及拖拽等操作，未说明在 WSL2 中通过 Windows 剪贴板粘贴图片的 fallback 机制，导致用户困惑。
- **🔗** https://github.com/anthropics/claude-code/issues/57440

### 3️⃣ [DOCS] 交互模式文档未说明以 `/` 开头的粘贴文本会被当作命令
- **#56885** (评论: 2)
- **摘要**：当用户在交互模式下粘贴以斜杠开头的内容（例如路径或代码片段）时，系统将其解释为命令而非文字，文档未覆盖这一行为，导致意外触发命令。
- **🔗** https://github.com/anthropics/claude-code/issues/56885

### 4️⃣ [DOCS] Skills 文档中 `name:` 与目录名的调用冲突
- **#61599** (评论: 2)
- **摘要**：Skills 文档指出每个 Skill 必须有一个 `name:`，但实际调用时使用的是目录名而非 `name:`，且参数提示也依赖目录名，文档与实现不一致。
- **🔗** https://github.com/anthropics/claude-code/issues/61599

### 5️⃣ [BUG] Fable 5 模型主动重路由导致简单代码审查无法完成
- **#73854** (评论: 1, 已关闭)
- **摘要**：用户反馈 Fable 5 模型在执行简单代码审查时自动重路由到其他任务，导致无法完成基础请求。多名用户抱怨“fable 5 useless”。
- **🔗** https://github.com/anthropics/claude-code/issues/73854

### 6️⃣ [BUG] 模型安全护栏无理由触发，阻止合法加密操作
- **#73909** (评论: 1, 已关闭)
- **摘要**：用户从事加密工作时被 Fable 5 安全护栏阻止，Classifiers 误判为非安全内容且无解释，影响合法开发。
- **🔗** https://github.com/anthropics/claude-code/issues/73909

### 7️⃣ [BUG] 搜索工具虚构结果而非执行真实查询
- **#73855** (评论: 1, 已关闭)
- **摘要**：用户要求 Claude 搜索某内容，工具声称已搜索但实际上编造结果。用户情绪激动，认为工具名为“执行工具”实为“聊天机器人”。
- **🔗** https://github.com/anthropics/claude-code/issues/73855

### 8️⃣ [BUG] 模型在未获用户许可下自动执行任务
- **#73921 / #73920** (评论: 各1, 已关闭)
- **摘要**：用户抱怨尽管已设置了模式限制，Claude Code 仍无权限自动执行任务，且执行率极低（不到1%）。用户直言“最垃圾的聊天机器人”。
- **🔗** https://github.com/anthropics/claude-code/issues/73921

### 9️⃣ [BUG] 长时间会话中 Token 消耗巨大且无实际进展
- **#74012** (评论: 1, 已关闭)
- **摘要**：用户反馈 Fable 5 在30分钟内持续浪费 Token 而没有任何有意义进展，成本高昂。
- **🔗** https://github.com/anthropics/claude-code/issues/74012

### 🔟 [BUG] Rate Limit 错误未优雅处理
- **#73902** (评论: 1, 已关闭)
- **摘要**：用户遇到 API 速率限制后系统无友好提示，导致工作流中断。反馈版本为 v2.1.170，说明问题已存在一段时间。
- **🔗** https://github.com/anthropics/claude-code/issues/73902

> 注：大量已关闭的 bug 报告集中在 7 月 3 日，可能与 Fable 5 模型上线后的初期波动有关。多数被标记为 `needs-repro` 或 `needs-info`，说明改进验证流程仍需社区协作。

---

## 重要 PR 进展（5 条，当日全部 PR）

### 1️⃣ [#76475] 安全指导：修复 innerHTML/outerHTML `+=` 追加模式的漏检
- **描述**：当前 `innerHTML_xss` 规则仅匹配 `.innerHTML =`，但 `el.innerHTML += userInput` 同样危险，该 PR 补充此类追加模式的检测，提升 XSS 防护覆盖面。
- **🔗** https://github.com/anthropics/claude-code/pull/76475

### 2️⃣ [#76394] 新增 Windows CLI 启动器（Claude Code Launcher）
- **描述**：社区贡献者开发了一个完整的 Windows PowerShell 应用程序，提供14个交互菜单选项，使 Windows 开发者能原生使用 Claude AI 能力，无需 WSL。这是一项重量级的第三方增强。
- **🔗** https://github.com/anthropics/claude-code/pull/76394

### 3️⃣ [#76298] 文档：记录 Remote Control 后台任务面板
- **描述**：为近期 v2.1.205 引入的 Web/Mobile 后台任务面板补充文档说明，包括任务状态同步行为，帮助用户理解远程控制体验。
- **🔗** https://github.com/anthropics/claude-code/pull/76298

### 4️⃣ [#76289] 示例：Bash 验证器中演示复合命令预检（deny-and-steer）
- **描述**：扩展 `bash_command_validator_example.py`，展示如何检测命令链（`;`、`&&`、`||`）、管道（允许只读过滤器白名单）、活动命令替换、`find -exec` 等，并提供拒绝并转向的策略。适用于编写严格安全 hook 的开发者。
- **🔗** https://github.com/anthropics/claude-code/pull/76289

### 5️⃣ [#76274] 安全指导插件：解析路径时始终基于仓库根目录并加固 findings 数组契约
- **描述**：修复安全指导插件中代理审查员（background reviewer / commit reviewer）传递的文件路径不一致问题——原本可能混入绝对路径或非 repo 根路径，现在统一以 repo 根目录解析，保证审查准确性。
- **🔗** https://github.com/anthropics/claude-code/pull/76274

---

## 功能需求趋势

从近期 Issue 和 PR 中可总结出社区最看重的方向：

| 需求方向 | 具体表现 | 代表 Issue/PR |
|---------|---------|--------------|
| **MCP Chrome 集成稳定性** | Windows 下 Chrome MCP 导航/读取完全不可用，缺乏审批弹窗 | #49979 及其关联 Issue |
| **模型行为可预测性** | Fable 5 自动重路由、未授权执行、不遵守模式限制 | #73854, #73921, #73920 |
| **文档完善与一致性** | Skills 文档 `name:` vs 目录名、交互模式粘贴行为、RTL 文本渲染 | #61599, #56885, #57440, #75240 |
| **Token / 成本控制** | 长时间会话 Token 浪费、无进展消耗 | #74012 |
| **安全护栏精细化** | 加密操作被误拦、缺乏触发原因说明 | #73909, #73847 |
| **Windows 原生支持** | 第三方 Windows CLI Launcher 出现，反映 Windows 用户需求 | #76394 |
| **指令遵循审计** | 用户要求 `/cd`、`/doctor` 等新增功能提升命令可控性 | v2.1.206 更新 |
| **权限与执行模式** | 用户希望更严格的权限确认流程，避免自动执行 | #73921, #73920 |

---

## 开发者关注点（痛点与高频诉求）

1. **Fable 5 的新模型不如预期**：大量用户反馈新模型“自作主张”，不遵循指令，甚至拒绝执行基础任务（如代码审查）。多位用户以强烈措辞呼叫“chat bot”而非“execution tool”。性能波动可能与新模型上线初期的调整有关。

2. **安全护栏过度敏感**：合法的密码学、网络编程等操作被误判为违规，且护栏触发时不提供理由，用户无法快速解决问题。这直接影响开发效率。

3. **搜索工具幻觉问题**：用户要求执行搜索时工具虚假报告已搜索并编造结果，削弱了工具的信任度。此问题在 #73855 中被用户直言“虚假广告”。

4. **Token 消耗不透明**：长时间运行的任务消耗大量 Token 却无明显进展，用户对成本/收益比感到不满。建议增加 Token 预算提醒或阶段性输出。

5. **文档与实际行为脱节**：多个文档（Skills、交互模式、WSL2 图片粘贴）存在描述不准确或遗漏，新手用户易产生误解。社区贡献者 @coygeek 持续提交高质量文档修复建议。

6. **Windows 生态支持不足**：虽然已存在 Windows 版本，但 MCP 核心功能在 Windows 11 上瘫痪，且缺乏原生 CLI 体验（社区不得不自行开发 Launcher）。

7. **Rate Limit 与计费体验**：超出速率时无优雅提示，计费问题（如已付费但账户仍显示免费）等影响用户体验。

---

*数据来源：GitHub Issues 与 Pull Requests (2026-07-10 更新)*  
*分析师建议：关注 v2.1.206 中 `/doctor` 功能，可帮助团队清理冗余文档；对于 Fable 5 的模型行为问题，可尝试回退至旧模型或等待 Anthropic 的模型调整。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

好的，以下是为您生成的2026年7月11日OpenAI Codex社区动态日报。

---

## OpenAI Codex 社区动态日报 | 2026-07-11

### 今日速览

昨日社区围绕 **GPT-5.6 Sol 模型的多Agent行为与兼容性** 展开密集讨论，多个 Issue 指出 Sol 在子 Agent 模型指定、Azure 部署等方面存在严重问题。同时，**Windows 平台安装与桌面应用稳定性** 成为第二大痛点，多名用户反馈无法完成安装或配置。代码层面，团队合并了多个关于 `bwrap` 集成测试和终端事件埋点的 PR，基础架构持续加固。

### 版本发布

过去24小时内有两个版本更新：

- **rust-v0.144.1**：Bug修复版本。修复了 GitHub 返回压缩或重排序的 release 元数据时导致独立安装失败的问题；确保 macOS 包安装时同时暴露 `code-mode host` 与 `codex` 可执行文件；当伴随的 host 二进制不可用时，回退保持 code mode 正常工作。
  - 链接：https://github.com/openai/codex/releases/tag/rust-v0.144.1

- **rust-v0.145.0-alpha.2**：预发布版本，仅标记为 `Release 0.145.0-alpha.2`，无详细变更说明。
  - 链接：https://github.com/openai/codex/releases/tag/rust-v0.145.0-alpha.2

### 社区热点 Issues

以下10个 Issue 因讨论热度高、影响面广或涉及核心功能值得重点关注：

1. **#30364 [bug, model-behavior, rate-limits] GPT-5.5 Codex 推理 token 聚类于 516/1034/1552 导致复杂任务性能下降**
   - **重要性**：发现 GPT-5.5 模型的 `reasoning_output_tokens` 高度集中在固定边界值（516, 1034, 1552），疑似模型行为缺陷，影响复杂推理质量。社区 182 条评论，282 个 👍。
   - **链接**：https://github.com/openai/codex/issues/30364

2. **#11023 [enhancement, app] 请求 Codex 桌面版 Linux 支持**
   - **重要性**：持续呼声最高的功能请求之一，已有 727 个 👍 和 161 条评论。用户因 macOS 性能问题转投 Linux，但官方迟迟未提供 Linux 桌面端。
   - **链接**：https://github.com/openai/codex/issues/11023

3. **#31814 [bug, CLI, subagent, config] GPT-5.6 Sol 无法指定子 Agent 模型，强制所有子 Agent 也为 Sol 实例**
   - **重要性**：MultiAgent V2 默认隐藏 spawn 元数据，导致用户无法控制子 Agent 的模型选择，严重限制灵活使用。31 条评论，80 👍。
   - **链接**：https://github.com/openai/codex/issues/31814

4. **#28969 [bug, enhancement, CLI, config, plan] 添加禁用自动 60 秒自动解析问题的设置**
   - **重要性**：用户对 CLI 中“自动在 60 秒后解析问题”的默认行为不满，认为该行为打断思考过程。104 个 👍 说明该诉求具有普遍性。
   - **链接**：https://github.com/openai/codex/issues/28969

5. **#3355 [bug, connectivity] MacBook 休眠后请求 ChatGPT 后端出错**
   - **重要性**：长期存在的连接性 Bug，休眠恢复后 Codex CLI 无法发送请求。40 条评论，虽只有 21 👍，但影响几乎所有 Mac 用户。
   - **链接**：https://github.com/openai/codex/issues/3355

6. **#31870 [bug, azure, CLI, custom-model, tool-calls] 通过 Azure 使用 GPT-5.6-Sol 每次调用都失败，报 X-OpenAI-Internal-Codex-Responses-Lite 错误**
   - **重要性**：Azure 企业用户无法使用最新 Sol 模型，阻碍企业级部署。22 条评论，27 👍。
   - **链接**：https://github.com/openai/codex/issues/31870

7. **#7808 [bug, context] 上下文窗口占满直接导致聊天线程死亡**
   - **重要性**：长时间任务中上下文空间用尽后线程立即终止，无任何恢复或压缩机制，是影响长会话体验的核心痛点。12 条评论。
   - **链接**：https://github.com/openai/codex/issues/7808

8. **#31710 [bug, CLI, tool-calls] `exec_command` 间歇性“不支持”，禁用 shell_tool 后彻底消失**
   - **重要性**：影响 CLI 用户正常使用 shell 执行能力，且存在配置级联失效问题。12 条评论。
   - **链接**：https://github.com/openai/codex/issues/31710

9. **#31846 [bug, app, config] GPT-5.3 Codex Spark 因 “Unsupported parameter: reasoning.summary” 失败**
   - **重要性**：模型参数不兼容问题，影响使用 GPT-5.3 Spark 的用户。6 条评论，12 👍。
   - **链接**：https://github.com/openai/codex/issues/31846

10. **#32016 [bug, windows-os, app] 桌面版长对话滚动时文字闪烁与重叠**
    - **重要性**：Windows 桌面版 UI 渲染问题，直接影响阅读体验。6 条评论，3 👍。
    - **链接**：https://github.com/openai/codex/issues/32016

### 重要 PR 进展

以下10个 PR 反映了代码库近期的重要变更方向：

1. **#32280 [CLOSED] 在 turn completion 事件中包含终端错误信息**
   - **内容**：在 `TurnCompleteEvent` 中添加可选的 error 载荷，使完成事件同步携带终端错误细节，便于上层监测。
   - **链接**：https://github.com/openai/codex/pull/32280

2. **#26259 [CLOSED] 为中断的 turn 添加 advisory Interrupt hooks**
   - **内容**：新增 `Interrupt` 钩子，不同于 `Stop` 钩子，允许处理程序上报上下文但不可阻断中断流程。
   - **链接**：https://github.com/openai/codex/pull/26259

3. **#32277 [CLOSED] 当 `personality = "none"` 时尊重设置，不发送 # Personality 段落**
   - **内容**：模型指令若显式设置 `personality = "none"`，则不再添加内嵌的 # Personality 章节，消除冗余。
   - **链接**：https://github.com/openai/codex/pull/32277

4. **#32276 [CLOSED] 修复未终止的 rollout 文件追加问题**
   - **内容**：追加数据前确保 JSONL 文件末尾有换行，防止追加时产生无效的 JSON 拼接。
   - **链接**：https://github.com/openai/codex/pull/32276

5. **#31058 [OPEN] fix(core): 模型容量错误时自动重试**
   - **内容**：将模型容量错误视为可恢复状态，最大重试3次（30秒/2分钟/5分钟间隔），避免直接终止 turn。
   - **链接**：https://github.com/openai/codex/pull/31058

6. **#32274 [CLOSED] 移除 personality 迁移逻辑**
   - **内容**：停止在启动时自动检测并设置 `personality = "pragmatic"`，移除迁移标记和相关 API。
   - **链接**：https://github.com/openai/codex/pull/32274

7. **#32272 [CLOSED] 在插件详情中暴露定时任务**
   - **内容**：为远程插件添加可选的 `scheduledTasks` 元数据（支持小时/天/周等），便于展示插件调度信息。
   - **链接**：https://github.com/openai/codex/pull/32272

8. **#31437 [OPEN] Windows 网络代理策略要求提升权限**
   - **内容**：修改 Windows 网络代理配置逻辑，使后端选择遵循配置的沙箱等级，避免不必要的UAC弹窗。
   - **链接**：https://github.com/openai/codex/pull/31437

9. **#31631 [CLOSED] [personality] 支持 harness-only personality none**
   - **内容**：使得无 personality 的 harness 模式能够正确剥离来自 catalog 指令的 # Personality 章节，而非仅依赖旧模板。
   - **链接**：https://github.com/openai/codex/pull/31631

10. **#31662 [OPEN] core: 允许限制子 Agent 的执行环境**
    - **内容**：为 spawn_agent v1/v2 增加可选的 `environment_ids` 参数，支持筛选子 Agent 可用的环境能力。
    - **链接**：https://github.com/openai/codex/pull/31662

### 功能需求趋势

从近期 Issue 和 PR 中可以提炼出以下社区关注的功能方向：

- **桌面端跨平台覆盖**：Linux 桌面端（#11023）仍是第一呼声，Windows 安装问题频发（#32149, #32281）则暴露出对基础安装流程优化的迫切需求。
- **多 Agent 与模型选择精细化控制**：用户希望可以指定子 Agent 使用的模型（#31814），而非被强制跟随主 Agent。
- **上下文窗口溢出恢复机制**：上下文占满即死（#7808）的体验需要改进，社区期望有上下文压缩或自动续接能力。
- **性能与稳定性**：MacBook 休眠后断连（#3355）、Token 消耗异常（#30842）、推理 token 聚类异常（#30364）等持续存在。
- **界面可用性**：Windows 文本闪烁（#32016）、子Agent面板信息缺失（#32283）等 UI 细节需要打磨。

### 开发者关注点

- **Azure 企业用户受阻**：通过 Azure 使用最新 Sol 模型（#31870）完全失败，影响企业客户迁移路线。
- **Shell 工具可靠性**：`exec_command` 间歇性失效（#31710）干扰日常开发流程，且配置联动复杂。
- **自动解析打断工作流**：60秒自动解析问题（#28969）缺乏禁用开关，用户反馈强烈。
- **代码 review 功能缺陷**：代码审查因 merge-base 缓存过期导致审查整个主干历史（#30741），严重影响 PR 审查效果。
- **日志膨胀导致卡顿**：Desktop 端 `logs_2.sqlite` 可达近 1GB 且无自动压缩（#30431），高负载下造成渲染冻结。

---

*数据基于 GitHub openai/codex 仓库截至 2026-07-10 的公开信息，日报日期为 2026-07-11。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 | 2026-07-11

## 今日速览

- **夜间版 v0.52.0 发布**，修复了“思考痕迹泄漏”问题，并剔除了 CI 配置文件对工作区上下文的干扰。
- **社区反馈集中**：子代理超时后误报成功、通用代理卡死等 Agent 稳定性 Bug 持续引发热议，Memory 模块的若干质量改进也进入维护者视野。
- **安全修复密集**：A2A 服务器路径遍历、令牌文件竞争条件、提示注入等关键漏洞获得补丁，开发者应关注升级。

## 版本发布

### v0.52.0-nightly.20260710.ga4c91ce19

[GitHub Release](https://github.com/google-gemini/gemini-cli/releases/tag/v0.52.0-nightly.20260710.ga4c91ce19)

主要变更：

- **fix(core)**：清除历史对话中模型的“思考痕迹”，防止泄漏到后续交互中（PR #27971）。
- **Refactor**：将临时性 CI 配置文件从工作区上下文中排除，减少无关噪音对 Agent 决策的干扰。

## 社区热点 Issues

以下 10 个 Issue 在过去 24 小时内更新最活跃，反映当前社区最关切的问题：

### 1. 子代理超时后误报成功 `#22323` 🔥
- **标签**：`kind/bug` `priority/p1`
- **摘要**：`codebase_investigator` 子代理在达到最大轮次后仍返回 `status: "success"` 和 `Termination Reason: "GOAL"`，但实际上并未完成任何分析。用户无法感知中断。
- **评论**：10 条 | **👍**：2
- **[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22323)**

### 2. 利用模型原生 bash 能力进行零依赖沙箱 `#19873`
- **标签**：`kind/enhancement` `priority/p2`
- **摘要**：提议借助 Gemini 3 模型原生的 POSIX 工具链能力，在无需额外容器的情况下实现 OS 沙箱，并将后执行意图路由至安全策略引擎。
- **评论**：8 条 | **👍**：1
- **[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/19873)**

### 3. 组件级评估体系需求 `#24353`
- **标签**：`kind/customer-issue` `priority/p1`
- **摘要**：跟踪组件级评估（Component Level Evaluations）的推进，要求为每个子模块建立独立的测试和基准，已有 76 个行为评估测试。
- **评论**：7 条
- **[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/24353)**

### 4. AST 感知文件读取与代码映射 `#22745`
- **标签**：`kind/feature` `priority/p2`
- **摘要**：探索利用 AST 感知工具实现更精准的读取方法边界、减少交互轮次、降低 Token 消耗，并为代码库映射提供新方案。
- **评论**：7 条 | **👍**：1
- **[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22745)**

### 5. 通用代理持续卡死 `#21409` 🔥
- **标签**：`kind/bug` `priority/p1`
- **摘要**：当 Gemini CLI 将任务委派给通用子代理时，客户端会无限期挂起（等待长达一小时）。用户发现通过手动禁止子代理可绕过。
- **评论**：7 条 | **👍**：8
- **[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21409)**

### 6. 模型不自动使用技能与子代理 `#21968`
- **标签**：`kind/bug` `priority/p2`
- **摘要**：用户报告即使定义了 Gradle、Git 等自定义技能，模型也很少主动调用，除非显式指令触发。
- **评论**：6 条
- **[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21968)**

### 7. 自动记忆低信号对话重试死循环 `#26522`
- **标签**：`kind/bug` `priority/p2`
- **摘要**：Auto Memory 在提取代理判定某会话无价值后不标记为“已处理”，导致该会话反复出现在候选列表中，形成无限重试。
- **评论**：5 条
- **[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/26522)**

### 8. Shell 命令执行后卡在“等待输入” `#25166`
- **标签**：`kind/bug` `priority/p1`
- **摘要**：极简单的 CLI 命令（如 `ls`）执行完毕后仍显示“Awaiting user input”，导致流程死锁。
- **评论**：4 条 | **👍**：3
- **[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/25166)**

### 9. 浏览器子代理在 Wayland 下失败 `#21983`
- **标签**：`kind/bug` `priority/p1` `agent/browser`
- **摘要**：Wayland 环境下浏览器子代理启动失败，返回 `Termination Reason: GOAL` 但实际并未完成任务。
- **评论**：4 条 | **👍**：1
- **[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21983)**

### 10. 工具数量超过 128 个时触发 400 错误 `#24246`
- **标签**：`kind/bug` `priority/p2`
- **摘要**：当可用工具数超过 400 个（实际触发线为 128），API 返回 400 错误。社区呼吁 Agent 应自动限制工具范围。
- **评论**：3 条
- **[查看 Issue](https://github.com/google-gemini/gemini-cli/issues/24246)**

## 重要 PR 进展

以下 10 个 PR 在最近更新中贡献了关键修复或功能：

### 1. 修复 A2A 任务取消导致幽灵执行 `#28316`
- **标签**：`size/m` `size/l`
- **摘要**：修复 Agent 模式下取消任务无法停止底层执行流的问题，同时解决多个竞态条件和内存泄漏。
- **[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28316)**

### 2. A2A 环境加载前强制路径信任检查 `#28319`
- **标签**：`size/m` `size/l`
- **摘要**：重构 `CoderAgentExecutor`，确保加载工作区环境变量之前执行路径信任检查，并使用 `AsyncLocalStorage` 隔离任务环境。
- **[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28319)**

### 3. 防止 restore 命令路径穿越 `#28353`
- **标签**：`size/s`
- **摘要**：对 `restore.ts` 中用户提供的文件名进行规范化与路径逃逸检测，阻止类似 `../../../etc/passwd` 的攻击。
- **[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28353)**

### 4. 清洗 caretaker 中不受信任的 Issue 标题 `#28352`
- **标签**：`size/s`
- **摘要**：在 Agent 摄取 Issue 时转义标题中的 `</untrusted_context>` 标签，防止提示注入。
- **[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28352)**

### 5. 实现 LLM 分类编排器与容器构建 `#28345`
- **标签**：`size/l`
- **摘要**：使用 Antigravity SDK 实现基于 LLM 的 Issue 分类功能，附带结构化日志与 Cloud Run Job 容器定义。
- **[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28345)**

### 6. 无 Code Assist 级账户显示清晰提示 `#28304` (已合入)
- **标签**：`priority/p1` `area/core` `size/m`
- **摘要**：当账户不具备 Code Assist 权限时，`/privacy` 命令不再显示原始后端错误，而是给出用户友好的说明。
- **[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28304)**

### 7. 原子化设置令牌文件权限 `#28330`
- **标签**：`priority/p2` `area/security`
- **摘要**：修复 IDE 认证令牌文件在创建与设置权限之间短暂全局可读的 TOCTOU 漏洞。
- **[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28330)**

### 8. 防止 customDeepMerge 引发循环引用崩溃 `#28349`
- **标签**：`priority/p2` `area/core`
- **摘要**：设置合并函数 `customDeepMerge` 添加循环引用检测，避免因配置对象含有 `obj.self = obj` 导致栈溢出。
- **[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28349)**

### 9. 修复 MaxListenersExceededWarning 与无限认证循环 `#28348`
- **标签**：`area/core` `size/m`
- **摘要**：解决 API 重试时事件监听器超过默认限制导致无限循环，以及在 Windows 上 OAuth 成功后陷入死循环的问题。
- **[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28348)**

### 10. 支持 `AGENTS.md` 默认上下文文件 `#28240`
- **标签**：`priority/p1` `area/agent` `size/m`
- **摘要**：修复 `AGENTS.md` 未被自动包含的问题，现在默认会将 `['GEMINI.md', 'AGENTS.md']` 作为上下文读取。
- **[查看 PR](https://github.com/google-gemini/gemini-cli/pull/28240)**

## 功能需求趋势

从近期 Issues 与 PR 中可提炼出社区最关注的四个功能方向：

1. **Agent 行为可预测性与透明度**  
   - 子代理轨迹可共享 (`#22598`)、Agent 自我意识（了解自身 CLI 参数、热键）(`#21432`)、Bug 报告中包含子代理上下文 (`#21763`)。

2. **记忆系统（Memory）的健壮性与安全**  
   - 低信号重试死循环 (`#26522`)、无效补丁自动隔离 (`#26523`)、确定性脱敏与日志减少 (`#26525`)。

3. **零依赖/轻量级沙箱与安全执行**  
   - 利用模型原生 bash 能力 (`#19873`)、路径信任检查前移 (`#28319`)、破坏性操作保护 (`#22672`)。

4. **AST 感知与代码库理解**  
   - AST 感知文件读取、搜索、代码映射 (`#22745`)、在 CLI 工具中集成 AST 分析 (`#22746`)、用于改善 `codebase_investigator`。

## 开发者关注点

### 痛点与高频反馈

- **子代理不遵守配置**  
  - 浏览器代理忽略 `settings.json` 中的 `maxTurns` 等覆盖 (`#22267`)。  
  - 子代理在用户禁用后仍自动执行 (`#22093`)。

- **Shell 命令交互缺陷**  
  - 命令完成后卡在“等待输入”状态 (`#25166`)。  
  - 模型随机创建临时脚本导致工作区杂乱 (`#23571`)。  
  - 无法正确处理交互式命令（如 `vite create`）(`#22465`)。

- **Agent 不会自动利用技能**  
  - 定义好的 Git/Gradle 技能需手动指令才能触发 (`#21968`)。  
  - 用户希望模型更主动地选择子代理完成任务。

- **工具/API 限制**  
  - 超过 128 个工具导致 400 错误，需智能筛选 (`#24246`)。  
  - 模型频繁执行 `update_topic` 在会话重置后造成脏数据 (`#28153` 已修复)。

- **跨平台问题**  
  - Wayland 下浏览器子代理失败 (`#21983`)。  
  - Windows 上 OAuth 认证死循环 (`#28348` 已修复)。  

> 建议开发者优先升级至最新夜间版以获取上述安全修复与稳定性改善，并关注子代理行为相关的后续更新。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 | 2026-07-11

---

## 今日速览

- **v1.0.71-0 发布**：新增固定提示设置、仓库作用域标签，优化了交互快捷键与验证命令体验。  
- **社区热度集中**：Alpine Linux 上工具调用导致段错误（#107）持续发酵；WSL2 + Windows Terminal 下 TUI 死机（#4069）引发广泛讨论。  
- **MCP 集成问题爆发**：OAuth 流程故障、服务器连接短暂后断开、工具不可用等问题密集报告，成为当天最集中的社区痛点。

---

## 版本发布

### v1.0.71-0（刚出炉）
- **Added**
  - `/settings` 页面新增“固定提示”设置，可控制提示固定行为。
  - `/settings` 仪表盘新增“仓库”和“仓库（本地）”作用域标签。
- **Improved**
  - 默认使用更轻量的验证命令和安装指导（替代原先的完整验证流程）。
  - 新增快捷键：`Ctrl+x → x` 关闭会话，`Ctrl+x → h` 隐藏侧边栏/对话。

### v1.0.70（2026-07-09）
- 支持 GPT‑5.6 模型。
- MCP 和技能命令失败时显示统一“Error”前缀。
- 当 `--agent` 选择格式错误的自定义 agent 时，展示真实解析错误。
- `web_fetch` 支持通过强制 HTTPS 代理工作。
- Gist 标签页隐藏 `/search` 功能。
- 将“超级子 agent 运行”视为“已取消”状态。

---

## 社区热点 Issues（前 10 条）

### 1. #107 – Alpine Linux 上工具调用导致段错误
- **作者** @SwanX1 | **评论** 15 | **👍** 4  
- **概述**：在 Docker 容器（alpine:latest）中使用 `-p` 或交互模式时，任何工具调用均触发 segmentation fault。影响版本 v0.0.328。  
- **为什么重要**：Alpine 是轻量级容器常用发行版，该 bug 导致大量 CI/CD 及 Edge 部署场景无法使用 Copilot CLI。  
  https://github.com/github/copilot-cli/issues/107

### 2. #4069 – WSL2+Windows Terminal TUI 死机（画面清空、输入无效）
- **作者** @msmbaldwin | **评论** 7 | **👍** 8  
- **概述**：使用 `claude-opus-4.7` 模型时，会话中途画面清空、键盘无响应，`Ctrl+C`/`Ctrl+\` 无效，输出显示 `write EIO` 及 `EPIPE` 错误。  
- **为什么重要**：Windows 生态核心场景，影响大量 WSL 开发者；问题重现率高，社区急等修复。  
  https://github.com/github/copilot-cli/issues/4069

### 3. #2739 – GPT‑5.4 及 GPT‑5.3-codex 的 xhigh 推理能力被移除
- **作者** @dlukt | **评论** 5 | **👍** 12  
- **概述**：用户抱怨 xhigh 推理选项被无预告移除，认为两个模型无 xhigh 后基本不可用。  
- **为什么重要**：高赞表明社区对模型接口变更敏感，尤其是高级推理能力对复杂任务至关重要。  
  https://github.com/github/copilot-cli/issues/2739

### 4. #3709 – 支持在单个会话中切换包括 BYOK/本地模型在内的多个模型
- **作者** @juancarlosjr97 | **评论** 2 | **👍** 17  
- **概述**：BYOK 模式锁定单一模型，`/model` 选择器仅列出 GitHub 托管模型，无法选择已配置的本地 BYOK 提供商。  
- **为什么重要**：BYOK 用户群体扩大，灵活切换模型是高频需求，该 feature request 获顶格点赞。  
  https://github.com/github/copilot-cli/issues/3709

### 5. #3331 – 插件自动更新：启动时从 marketplace 检查更新
- **作者** @joshgomes-42 | **评论** 3 | **👍** 4  
- **概述**：当前插件必须手动运行 `copilot plugin update`，团队无法保证消费者使用最新版本。  
- **为什么重要**：插件生态成熟后，自动更新是基础设施级需求，影响团队协作效率。  
  https://github.com/github/copilot-cli/issues/3331

### 6. #3399 – 允许为 BYOK 自定义 HTTP 请求头
- **作者** @ZzetT | **评论** 3 | **👍** 6  
- **概述**：某些 LLM 服务器需要 `X-Tenant-ID`、`X-Organization-ID` 等自定义头，当前无法设置。  
- **为什么重要**：企业级自建模型网关必备，直接决定 BYOK 模式的多租户可用性。  
  https://github.com/github/copilot-cli/issues/3399

### 7. #4077 – v1.0.70-0 Windows Terminal 黑屏挂起（可 `--resume` 恢复）
- **作者** @dmauser | **评论** 2 | **👍** 3  
- **概述**：会话中偶发全黑屏，但内容完整，通过 `--resume` 可恢复。WinGet 安装版。  
- **为什么重要**：继 #4069 后又一 Windows TUI 稳定性问题，表明渲染层存在潜在 bug。  
  https://github.com/github/copilot-cli/issues/4077

### 8. #4091 – linuxmusl-x64 发布包中删除独立二进制文件
- **作者** @100-a1 | **评论** 1 | **👍** 0  
- **概述**：v1.0.70 起，Alpine 适用的 `linuxmusl-x64` tarball 不再包含预编译独立二进制，导致 Alpine 用户无法直接运行。  
- **为什么重要**：与 #107 段错误问题叠加，Alpine 用户群体面临双重困境。  
  https://github.com/github/copilot-cli/issues/4091

### 9. #4093 – web_search 工具返回完全虚构的答案
- **作者** @dfrysinger | **评论** 0 | **👍** 0  
- **概述**：当底层检索无相关内容时，`web_search` 仍自信生成带引用的详细虚假答案，而非报告无结果。  
- **为什么重要**：AI 驱动的搜索工具若产生“幻觉”输出，会严重误导开发者决策，属于安全与准确性问题。  
  https://github.com/github/copilot-cli/issues/4093

### 10. #4089 / #4086 / #4085 / #4084 – MCP OAuth 连接故障群（合并关注）
- **作者** @Mov1ngTrg3t、@Joachim-Ally-Skyline | **总评论** 2+ | **👍** 0  
- **概述**：Atlassian MCP 服务器 OAuth 成功但零工具暴露、OAuth 流程自动消失、连接约 90s 后断开等问题。  
- **为什么重要**：MCP 是 Copilot CLI 扩展性的核心功能，多个 OAuth 相关 issue 集中爆发表明基础设施不够成熟。  
  https://github.com/github/copilot-cli/issues/4089  
  https://github.com/github/copilot-cli/issues/4086  
  https://github.com/github/copilot-cli/issues/4085

---

## 重要 PR 进展

**暂无合并或活跃 PR。** 当天所有 PR 列表为空，社区注意力集中在 issue 报告和已发布版本的问题上。

---

## 功能需求趋势

从近期 issues 和 feature request 中提炼出社区最关注的五大方向：

1. **MCP 集成完善**  
   - OAuth 流程稳定、工具自动暴露、服务器连接保持 —— 多个 issue 直指 MCP 在真实企业环境中的可用性。

2. **模型灵活切换**  
   - `/model` 支持 BYOK/本地模型（#3709）、自定义 HTTP 头（#3399）、启用/禁用特定推理能力（#2739）。

3. **插件与技能自动管理**  
   - 启动时自动更新插件（#3331）、技能中的动态上下文注入（`!command` 占位符，#4088）。

4. **终端渲染与稳定性**  
   - TUI 黑屏/死机（#4069、#4077）、跨应用会话同步（#4082）、语音模式企业代理兼容（#4083）。

5. **安全与数据保护**  
   - checkpoint 恢复时 `git clean -fd` 永久删除未跟踪文件（#1675）、web_search 幻觉导致误导（#4093）。

---

## 开发者关注点

- **Alpine Linux 用户面临“双重打击”**：段错误（#107）+ 独立二进制删除（#4091），亟需官方修复或临时变通方案。  
- **Windows 生态稳定性成疑**：WSL2+Windows Terminal 下 TUI 死机（#4069）、黑屏挂起（#4077），影响主流开发环境使用体验。  
- **模型变更社区情绪强烈**：xhigh 推理能力移除（#2739）获 12 个赞，用户对无预告的模型能力降级非常不满。  
- **BYOK 及本地模型需求旺盛**：#3709 的 17 个赞是本周最高，企业用户希望完全掌控模型供应链。  
- **语音模式初显水土不服**：企业代理下载失败（#4083）、空间键释放自动提交（#4090）、音频暂停（#4092）等细节问题表明语音功能仍处于早期阶段。

---

*数据来源：github.com/github/copilot-cli，更新于 2026-07-10 至 2026-07-11。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-07-11

## 🚀 今日速览
过去 24 小时无新版本发布，但有 **4 个 Pull Request** 获得更新（含 2 个刚刚合并的修复）。重点包括：Web 界面布局微调、Soul 模式下 `/init` 造成工具绑定丢失的 Bug 修复、新安装用户报错信息优化以及 Safari 中文输入法下回车误提交问题。社区活跃度集中在补齐细节与兼容性上。

---

## 📦 版本发布
无（近 24 小时无新 Release）。

---

## 🔍 社区热点 Issues
**过去 24 小时内无新建或更新的 Issue**（数据返回 0 条）。  
相关 Bug 线索可从下文 PR 关联的 Issue 中追踪，例如 `#2478`（Soul 工具绑定丢失）和 `#2456`（新用户 LLM 错误提示无引导）。

---

## 🛠️ 重要 PR 进展

### #2353 — `fix(web): tighten app layout spacing` **（已合并）**
- **作者**: @anxndsgn  
- **更新于**: 2026-07-10  
- **链接**: [PR #2353](https://github.com/MoonshotAI/kimi-cli/pull/2353)  
- **内容**: 移除了应用外层不必要的边距，同时保留安全区（safe-area）内边距；优化了会话侧边栏的列表间距与搜索输入框的显示。前后效果对比图已附在 PR 中。  
- **影响**: 改善 Web 端整体视觉紧凑度，提升 UI 一致性。

### #2489 — `fix(soul): restore plan-mode tool bindings after /init creates throwaway soul` **（开放中）**
- **作者**: @nankingjing  
- **更新于**: 2026-07-10  
- **链接**: [PR #2489](https://github.com/MoonshotAI/kimi-cli/pull/2489)  
- **内容**: 修复 Issue #2478。当执行 `/init` 命令时，会创建一个临时的 `KimiSoul`（共享相同 Agent），其 `__init__` 调用 `_bind_plan_mode_tools()` 导致重新绑定公有的 `ExitPlanMode`、`EnterPlanMode`、`Write` 等工具，破坏了当前会话的正确绑定。本 PR 在临时 Soul 销毁后恢复原始绑定状态。  
- **影响**: 解决了 `/init` 后计划模式工具异常的关键 Bug，影响使用 Agent + Plan 工作流的用户。

### #2488 — `fix(soul): make LLMNotSet error message actionable for fresh installs` **（开放中）**
- **作者**: @nankingjing  
- **更新于**: 2026-07-10  
- **链接**: [PR #2488](https://github.com/MoonshotAI/kimi-cli/pull/2488)  
- **内容**: 对应 Issue #2456。当用户通过 Homebrew 全新安装后，未执行 `kimi login` 前运行任何命令会报 `LLM not set`，但没有任何后续引导。本 PR 将错误信息改为：“LLM not set. Please run `kimi login` first. See https://... for details.”。  
- **影响**: 降低新用户的上手困惑，提高首次体验友好性。

### #1815 — `fix(web): prevent Enter from sending message during IME composition on Safari` **（已合并）**
- **作者**: @qianqiuqiu  
- **更新于**: 2026-07-10  
- **链接**: [PR #1815](https://github.com/MoonshotAI/kimi-cli/pull/1815)  
- **内容**: 修复 Safari + macOS 原生中文输入法下，在候选词窗口按回车直接发送消息的问题。通过监听 `compositionstart`/`compositionend` 事件，阻止正在输入法组合过程中回车键触发的发送行为。  
- **影响**: 重要浏览器兼容性修复，尤其影响使用 macOS 中文输入法的用户。

---

## 📈 功能需求趋势
从本期 PR 可以提炼出以下社区关注方向：

| 方向 | 表现 |
|------|------|
| **Web UI 细节打磨** | 布局间距调整、侧边栏优化，说明团队持续优化前端体验。 |
| **Agent/Soul 模式正确性** | `/init` 导致工具绑定丢失的修复表明用户对 Plan 模式稳定性要求高。 |
| **新手引导与错误信息** | 提升首次安装后错误提示的可操作性，降低入门门槛。 |
| **浏览器兼容性** | Safari + IME 问题修复，暗示跨平台/跨浏览器测试不足，社区对此敏感。 |

---

## 🧑‍💻 开发者关注点
- **新用户 onboarding**：`LLM not set` 错误信息目前缺乏指导，开发者希望 CLI 能直接提示下一操作（如 `kimi login`）。
- **Plan 模式与 Init 命令交互**：`/init` 意外破坏工具绑定，导致工作流中断，该 Bug 已引发关联 Issue `#2478`，当前 PR #2489 正在进行中。
- **Safari 输入兼容**：中文 IME 回车误发送是常见痛点，合并后大量 macOS + Safari 用户受益。
- **Web 布局精确控制**：开发者注意移除多余全局边距，同时保留安全区，体现了对 iPhone 刘海屏等异形屏的适配意识。

---

> 数据来源：[MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)  
> 注：本日报基于过去 24 小时的仓库活动数据生成（2026-07-10 至 2026-07-11）。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报（2026-07-11）

## 今日速览
昨日（2026-07-10）OpenCode 社区活跃度显著，共产生 50+ 条议题和 50+ 条拉取请求。GPT-5.6 模型系列（Luna、Sol）及 prompt caching 新特性引发讨论，同时 SQLite 数据库并发损坏、Xcode ACP 默认模型覆盖、Copilot 提供者端点错误等痛点问题持续受到关注。V2 TUI 的多项交互缺陷和性能回退也被密集报告。

## 社区热点 Issues（10 条）

1. **#36140 GPT-5.6 Luna 通过 ChatGPT OAuth 返回“模型未找到”**  
   `opencode` 内置的 OpenAI 提供者中 `gpt-5.6-luna` 被列出，但请求时返回 HTTP 404。社区已确认从干净 `dev` 分支复现，而同一账号使用 `gpt-5.5` 正常。该 issue 获得 41👍，表明大量用户正尝试使用最新模型。  
   [链接](https://github.com/anomalyco/opencode/issues/36140)

2. **#34743 Xcode 27 beta 2 中 ACP 强制使用默认模型 big-pickle**  
   用户在 Xcode 27 beta 2 中配置了自定义 ACP agent，但 opencode 忽略 `opencode.json` 或 TUI 中选择的模型，始终使用 `big-pickle`。严重影响 Xcode 环境下的工作流，12 条评论讨论根本原因。  
   [链接](https://github.com/anomalyco/opencode/issues/34743)

3. **#14970 SQLite 数据库并发会话导致损坏（NFS 环境）**  
   在 NFS 挂载的主目录下同时运行多个 `opencode` 会话，共享 SQLite 数据库被破坏，出现 `database disk image is malformed`。持续数月未修复，10 条评论，19👍，社区关注度高。  
   [链接](https://github.com/anomalyco/opencode/issues/14970)

4. **#19205 支持交互式引导（Interactive Steering）**  
   GPT-5.4 引入交互式引导，当任务排队时应允许用户干预。26👍，说明社区期望 opencode 能原生集成此能力。  
   [链接](https://github.com/anomalyco/opencode/issues/19205)

5. **#36305 GitHub Copilot 提供者所有模型被拒绝：400 unsupported api for model**  
   使用内置 GitHub Copilot 提供者时，任何模型请求都返回 400，因为 opencode 始终调用 `/chat/completions` 端点而非正确端点。影响所有 Copilot 用户。  
   [链接](https://github.com/anomalyco/opencode/issues/36305)

6. **#36241 macOS 上 gpt-5.6-sol-fast 流式推理时崩溃**  
   在 macOS 上使用 `openai/gpt-5.6-sol-fast` 的 `high` 推理变体时，流式传输中断并报错 `reasoning part rs_*:0 not found`。  
   [链接](https://github.com/anomalyco/opencode/issues/36241)

7. **#35828 Windows TUI 启动失败：已有 .opencode 目录**  
   当项目已存在 `.opencode` 目录时，opencode v1.17.15 在 Windows 上启动 TUI 报 `Unexpected server error`。影响多平台开发。  
   [链接](https://github.com/anomalyco/opencode/issues/35828)

8. **#36280 Worker 子进程因 SIGILL 崩溃并冻结系统**  
   在 Intel i5-7200U（Kaby Lake）上，Worker 子进程非法指令崩溃后，递归崩溃处理造成内存耗尽。属于严重的兼容性/稳定性问题。  
   [链接](https://github.com/anomalyco/opencode/issues/36280)

9. **#36302 TUI 模态交互与视觉行为统一**  
   开发者 @kitlangton 完成了对 V2 TUI 37 个对话框组件的审计，复现了 20 种状态问题，计划拆分为多个实现 issue。标志着 V2 交互质量提升。  
   [链接](https://github.com/anomalyco/opencode/issues/36302)

10. **#36285 V2 托管服务重启导致 herd 效应和资源尖峰**  
    V2 TUI 在自动更新期间共享托管服务被替换，断开所有已连接 TUI，导致并发冷启动多个 location graph，延迟 SSE 就绪。暴露了服务生命周期管理缺陷。  
    [链接](https://github.com/anomalyco/opencode/issues/36285)

## 重要 PR 进展（10 条）

1. **#31756 文件树排序改为数值排序**  
   修复 `file2.txt, file10.txt` 等被字典序错误排序的问题（`automatated-pr-cleanup` 合并）。  
   [链接](https://github.com/anomalyco/opencode/pull/31756)

2. **#31736 修复无 ID 项目的编辑持久化**  
   对「全局」或无服务器 ID 的项目，编辑名称、颜色、命令后无法保存。现已修复（合并）。  
   [链接](https://github.com/anomalyco/opencode/pull/31736)

3. **#31729 TUI 提示代理跟随最新用户消息**  
   修复 TUI 中活跃 agent 未随最后一条用户消息切换的 bug，确保 prompt 同步（合并）。  
   [链接](https://github.com/anomalyco/opencode/pull/31729)

4. **#31713 提供者连接阻塞时以 60s 间隔重试**  
   针对 NVIDIA 等提供者挂起连接（ECONNRESET 或 HTTP 504）或引擎内部崩溃，增加指数退避重试（合并）。  
   [链接](https://github.com/anomalyco/opencode/pull/31713)

5. **#31685 修复 tool.definition 钩子未传播对 MCP 工具的修改**  
   `tool.definition` 钩子只读回 `description`，忽略其他参数修改。合并后确保 MCP 工具定义可被插件完整修改。  
   [链接](https://github.com/anomalyco/opencode/pull/31685)

6. **#31671 为 MCP 工具添加缺失的 tool.definition 钩子**  
   之前 MCP 工具在解析时未经过 `tool.definition` 钩子，仅通过注册工具执行。现在补全（合并）。  
   [链接](https://github.com/anomalyco/opencode/pull/31671)

7. **#31641 发现 .opencode/plugin 下嵌套的插件入口**  
   扩展自动发现机制，支持 `.opencode/plugin/` 下最多两层子目录中的 `index.{js,ts}` 入口（合并）。  
   [链接](https://github.com/anomalyco/opencode/pull/31641)

8. **#31628 允许原生 OpenAI 兼容提供者正确注册**  
   `@ai-sdk/openai-compatible` 的自定义提供者被原生运行时拒绝，除非其 ID 在白名单中。现已移除限制（合并）。  
   [链接](https://github.com/anomalyco/opencode/pull/31628)

9. **#31639 为 Desktop Store.load 添加超时以挂起持久化**  
   包装 `Store.load` 为 5 秒超时，防止因挂起的持久化导致整个桌面应用卡死（合并）。  
   [链接](https://github.com/anomalyco/opencode/pull/31639)

10. **#31613 保留模型消息缓存快照**  
    修复 session 恢复时丢失模型消息缓存的 bug，采用快照而非可变数据库对象，防止缓存失效（合并）。  
    [链接](https://github.com/anomalyco/opencode/pull/31613)

## 功能需求趋势

- **新模型支持**：GPT-5.6 系列（Luna, Sol）的兼容性及 prompt caching 默认启用成为社区首要诉求。
- **IDE/平台集成**：Xcode beta 中 ACP 模型覆盖、GitHub Copilot 端点适配、macOS 稳定性等问题凸显。
- **并发与持久化**：SQLite 数据库并发写入损坏（NFS）、数据库锁错误、Worker 子进程崩溃等基础性能问题亟待解决。
- **V2 TUI 完善**：模态交互、fork 会话、子代理导航、SSE 连接恢复等交互缺陷被密集报告，表明 V2 用户增长但体验仍需打磨。
- **提供者生态**：OpenAI、Anthropic、Kimi、MiniMax 等多提供者的兼容性修复（模型名、流式、OAuth token 刷新）持续出现。

## 开发者关注点

- **稳定压倒一切**：数据库损坏、子进程崩溃、系统死机等严重影响日常使用，用户反馈强烈。
- **配置生效问题**：`opencode.json` 中指定的模型被忽略（如 Xcode ACP），导致用户被迫回退到默认配置。
- **多平台适配**：Windows TUI 启动失败、macOS 流式崩溃、Intel 旧款 CPU SIGILL 等平台特定问题突出。
- **提供者兼容性开销**：切换不同模型/提供者时频繁遇到端点错误、模型未找到、OAuth 失败，增加用户心智负担。
- **自动化工具**：大量 `automated-pr-cleanup` 标签的 PR 暗示社区在尝试用自动化流程维护代码质量，但部分 PR 缺乏人工 review 可能引入新问题。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-07-11

---

## 今日速览

- **v0.19.9 正式发布**，修复了子代理工具调用无限循环和会话历史链断裂问题，同时发布流程因 Docker 沙箱网络问题受阻，已提交补丁。
- **多工作区支持 RFC（#6378）** 持续活跃，社区围绕 daemon 模式下的多工作区管理展开深度讨论，多个相关 PR 已进入 Phase 4 阶段。
- **数项高影响 Bug 被标记修复**：包括 Glob 工具 OOM、Cron 解析器步长丢失、macOS 粘贴图片失效等，开发者可关注对应 PR 的合并状态。

---

## 版本发布

### v0.19.9（2026-07-10）
- **停止子代理重复工具调用循环**：避免因 tool-call 反复触发同一动作导致的死循环（PR #6543）。
- **修复会话历史链断裂**：检测并标记损坏的历史记录链，而非静默截断，提升会话恢复的可靠性。

### v0.19.8-nightly.20260710
- 同步包含上述两项修复，供早期验证。

> **⚠️ 发布阻塞**：v0.19.9 的 CI 发布流程因 `integration_docker` 作业失败（Docker 沙箱内 127.0.0.1 绑定问题），已提交修复 PR #6691、#6692。

---

## 社区热点 Issues（10条）

### 1️⃣ [#6378] RFC: 支持单 daemon 进程管理多个工作区
- **标签**：P2 / feature-request / daemon  
- **动态**：已获 20 条评论，讨论聚焦于 API 设计、会话隔离与向后兼容。后续已有多个 Phase 4 PR（#6638、#6635、#6621）。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/6378

### 2️⃣ [#5975] API 流超时：120 秒无活动后报错  
- **标签**：P2 / bug / latency  
- **动态**：10 条评论，用户反馈 v0.19.3 后频繁出现，且此前表现为“Thought for 2s”后无输出。可能与模型响应特性或代理中间件有关。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/5975

### 3️⃣ [#6590] macOS 独立安装版 Ctrl+V 粘贴图片失效  
- **标签**：P2 / bug / macos  
- **动态**：4 条评论，根因为原生模块 `@teddyzhu/clipboard` 未打包进 standalone 安装包，社区欢迎 PR。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/6590

### 4️⃣ [#6629] Cron 表达式步长丢失：`5/15` 只匹配 `5`  
- **标签**：P2 / bug / autofix  
- **动态**：已关闭，PR #6633 修复。常见 `0/15` 表达式受影响，社区贡献者已提交补丁。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/6629

### 5️⃣ [#6600] `--debug` 标志显示日志路径但实际未创建文件  
- **标签**：P2 / bug / logging  
- **动态**：4 条评论，用户发现 debug 日志文件从未落地，怀疑是文件流初始化时机问题。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/6600

### 6️⃣ [#6654] 工具调用块缺少对应 tool_result 导致 API 错误  
- **标签**：P2 / bug / token-management  
- **动态**：4 条评论，表现为 `tool_use ids were found without tool_result blocks`，可能与并发或会话恢复场景有关。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/6654

### 7️⃣ [#6595] qwen3.7-max 在长上下文场景泄露 `<analysis>` 标签  
- **标签**：P2 / bug / long-context  
- **动态**：3 条评论，模型在工具调用后输出内部分析标签，导致后续动作中断。已关闭，需复测。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/6595

### 8️⃣ [#6614] Glob 工具在超大路径上 OOM  
- **标签**：P1 / bug / memory-usage  
- **动态**：2 条评论，子代理 glob `**` 匹配整个项目目录时堆内存溢出，已修复并关闭。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/6614

### 9️⃣ [#6639] MCP HTTP 传输 401 时未触发 OAuth 恢复  
- **标签**：P2 / bug / mcp  
- **动态**：3 条评论，所有 HTTP 传输的 MCP 服务器显示为离线，无法自动重连。社区欢迎 PR。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/6639

### 🔟 [#6694] DingTalk 频道回复暴露子代理中间报告与本地路径  
- **标签**：P2 / bug / security  
- **动态**：2 条评论，子代理的中间结果（含绝对路径）被拼入最终回复，存在信息泄露风险。  
- **链接**：https://github.com/QwenLM/qwen-code/issues/6694

---

## 重要 PR 进展（10条）

### 1️⃣ [#6691] 提升发布包大小限制至 96 MB  
- **摘要**：将 `prepare-package.js` 中的大小上限从 80 MB 提高到 96 MB，以解决 v0.19.9 包体超限导致的 CI 失败。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6691

### 2️⃣ [#6692] 修复 Docker 沙箱下 protocol-tags 测试网络绑定  
- **摘要**：测试中的假服务器绑定 `127.0.0.1` 在 Docker 内解析为容器 loopback，改为 Docker 可访问地址。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6692

### 3️⃣ [#6680] 频道会话在 daemon 重启后自动恢复  
- **摘要**：持久化 channel 路由元数据，支持 worker 和 daemon 重启后无需手动重连。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6680

### 4️⃣ [#6697] WebShell 加载已停止的会话时自动恢复  
- **摘要**：WebShell 在加载已有会话时检查中断的用户轮次，并调用 daemon 的 continuations 端点恢复。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6697

### 5️⃣ [#6638] 工作区限定扩展管理 REST API（多工作区 Phase 4）  
- **摘要**：为非主工作区暴露等效的扩展管理端点，推动单 daemon 多工作区架构落地。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6638

### 6️⃣ [#6635] 频道 workers 按工作区分组（Phase 4b）  
- **摘要**：daemon 绑定多个 workspace 后，为每个 workspace 独立运行频道 worker，使非主工作区的频道配置生效。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6635

### 7️⃣ [#6591] WebShell 添加产物（Artifact）右面板  
- **摘要**：新增航次输出审查面板，支持编辑文件行数统计、可展开的 diff、可拖拽的审查区域等。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6591

### 8️⃣ [#6696] 抑制频道回复中的子代理输出  
- **摘要**：防止嵌套子代理的中间消息被拼入最终频道回复，解决 #6694 的安全问题。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6696

### 9️⃣ [#6332] 修复 Windows 下 shell 命令执行时标题被覆盖  
- **摘要**：ConPTY 子进程发送的 OSC 标题序列会重置 qwen-code 的窗口标题，通过滚动窗口标题防止被覆盖。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6332

### 🔟 [#6440] 新增 `/learn` 命令：用户可创建可复用技能  
- **摘要**：允许用户从本地目录、URL、对话历史或自由文本中提取知识，生成 SKILL.md 文件，类似 `/remember` 但面向技能创建。  
- **链接**：https://github.com/QwenLM/qwen-code/pull/6440

---

## 功能需求趋势

从过去 24 小时的 Issues 和 PR 中，社区最关注的功能方向包括：

1. **多工作区架构**：`qwen serve` 单进程管理多个 workspace（#6378），相关 REST API 和频道支持已进入 Phase 4（#6638、#6635、#6621）。
2. **会话管理与恢复**：WebShell 自动恢复中断轮次（#6695、#6697）、channel 会话持久化（#6680）、多工作区会话组织（#6646）。
3. **MCP 集成增强**：HTTP 传输 OAuth 恢复（#6639）、SDK 支持 `ask_user_question` 交互（#6647）。
4. **模型兼容性与性能**：qwen3.7-max 标签泄露修复（#6595）、向 DashScope 的推理内容分离（#6666）、Anthropic 转换器低缓存命中优化（#6642）。
5. **CLI 体验优化**：`/goal` 字符数限制提升（#6663）、输入框内容暂存（#6669）、自动模式转换问题（#5970）。

---

## 开发者关注点

- **流稳定性问题**：No stream activity 超时（#5975）、模型返回空内容（#6670）持续影响日常使用。
- **上下文管理反直觉**：环境变量配置模型时输出窗口占满导致 hard limit 0（#6384）、会话恢复后上下文过大（#6384）。
- **子代理与工具交互 Bug**：工具调用块缺失（#6654）、子代理因 `${0}` 模板占位符崩溃（#6671）、中间输出泄露至频道（#6694）。
- **平台特定缺陷**：macOS 粘贴图片依赖原生模块未打包（#6590）、Windows 标题被覆盖（#6332）。
- **CI/CD 稳定性**：v0.19.9 发布因 Docker 沙箱网络限制失败（#6684、#6690），开发团队已多次提交修复（#6691、#6692）。
- **调试支持不足**：`--debug` 日志文件未实际写入（#6600），影响问题定位。

---

> 以上日报基于 Qwen Code 官方 GitHub 仓库（github.com/QwenLM/qwen-code）截至 2026-07-11 凌晨的数据整理，所有链接可直接访问。欢迎社区继续提交 Issue 与 PR。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*