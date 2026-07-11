# AI CLI 工具社区动态日报 2026-07-12

> 生成时间: 2026-07-11 23:14 UTC | 覆盖工具: 7 个

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

好的，作为专注于 AI 开发工具生态的资深技术分析师，我已仔细审阅并分析了今日（2026-07-12）各主流 AI CLI 工具的社区动态。以下是一份横向对比分析报告，旨在为您提供清晰、有数据支撑的行业洞察。

---

### AI CLI 工具生态横向对比分析报告 | 2026-07-12

#### 1. 生态全景

当前 AI CLI 工具生态呈现出 **“百花齐放，核心趋同，差异深化”** 的态势。各大厂商的 CLI 工具已从“技术演示”阶段进入“工程化落地”阶段，社区活跃度高，但**稳定性和可靠性**是普遍痛点。所有工具都在围绕**多代理协作（Multi-Agent）、MCP 协议集成以及安全沙箱**三大核心能力展开竞争，但在具体的工程实现、平台支持和目标用户上已出现显著分化。开发者反馈已从早期的“哇，它能写代码”转向了更务实的“请别在工作时卡死/误报/配置失效”。

#### 2. 各工具活跃度对比

| 工具名称 | 今日新增/热议 Issues 数 | 重要 PR 数 | 版本发布情况 | 社区关注核心事件 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 10 | 5 | ✅ `v2.1.207` | **回归 Bug (MCP 断连)**、**Windows Cowork 不可用**、Auto Mode 全面开放 |
| **OpenAI Codex** | 10 | 10 | ✅ `v0.145.0-alpha.4` | **子代理模型强制锁定 (GPT-5.6 Sol)**、配额丢失、VSCode 扩展 Linux 白屏 |
| **Gemini CLI** | 10 | 7 | ❌ 无新版本 | **子代理挂起/误报成功**、Shell 卡死、自动记忆无限重试 |
| **GitHub Copilot CLI** | 10 | 1 | ❌ 无新版本 | **MCP OAuth 连接后工具不可用**、语音模式全模型静默、Windows 更新锁 |
| **Kimi Code CLI** | 1 | 3 | ❌ 无新版本 | **插件资源被错误归类为技能**、ACP 服务器未加载全局 MCP 配置 |
| **OpenCode** | 10 | 10 | ❌ 无新版本 | **GPT-5.6 Luna 404**、**YOLO 模式争议**、高 CPU 占用、V2 TUI 配置修复 |
| **Qwen Code** | 10 | 10 | ✅ `v0.19.8-nightly` | **多工作区支持 (RFC)**、JetBrains 集成故障、macOS 剪贴板缺失、提示缓存失效 |

**解读：** Claude Code、OpenAI Codex 和 OpenCode 是今日社区讨论热度最高的三个工具，均出现了影响核心工作流的严重 Bug 或功能回归。Qwen Code 和 Gemini CLI 在新功能演进上表现积极，PR 数量多且覆盖面广。Kimi Code CLI 和 GitHub Copilot CLI 社区反馈量相对较少，但反馈问题同样尖锐。

#### 3. 共同关注的功能方向

多个工具社区的讨论同时指向了以下需求，表明这些已成为 **AI CLI 工具的核心竞争赛道**：

- **多代理 (Multi-Agent) 行为的可靠性与可预测性**:
    - **涉及工具**: OpenAi Codex (#31814), Gemini CLI (#22323, #21409), Claude Code (#76777)
    - **具体诉求**: 用户普遍反映子代理存在**行为不透明**（误报成功/隐藏中断）、**控制力不足**（无法指定子代理模型、子代理无视禁用配置）、**稳定性差**（无限挂起/陷入循环）等问题。社区强烈要求获得对子代理更精细的控制权，以及更诚实、可预测的状态报告。

- **MCP (Model Context Protocol) 集成的流畅性与安全性**:
    - **涉及工具**: GitHub Copilot CLI (#4089, #4096), Claude Code (#76769), Qwen Code (#6639), Kimi Code CLI (#2490)
    - **具体诉求**: 核心痛点在于 **OAuth 认证断裂**（连接成功但工具不可用，Token 未传递）、**连接稳定性差**（stdio MCP 服务器被无故切断）、**配置不一致**（ACP 模式与交互式模式下 MCP 配置不统一）。MCP 生态的潜力巨大，但当前的实现细节充满摩擦。

- **沙箱(Sandbox)与权限控制的精细化**:
    - **涉及工具**: Claude Code (#51798), OpenCode (#8463), Qwen Code (#5970)
    - **具体诉求**: 呈现两极分化趋势。一方面，像 OpenCode (YOLO 模式) 和 Qwen Code (YOLO 模式修复) 社区推动 **“零摩擦”的自动化模式**，允许用户跳过所有权限确认；另一方面，Claude Code 用户抗议配置项 (`dangerouslyDisableSandbox`) 失效后，Bash 权限弹窗再次回归，打乱了自动化流程。这表明社区既渴望高效自动化，又对安全控制的有效性高度敏感。

- **跨平台兼容性与 IDE 集成一致性**:
    - **涉及工具**: Claude Code (#74649), OpenAi Codex (#32041), Gemini CLI (#21983), GitHub Copilot CLI (#4095), Qwen Code (#6590, #6581)
    - **具体诉求**: **Windows 平台**是重灾区（Claude Code Cowork 不可用、Copilot 扩展文件锁、OpenCode 路径问题），**Linux 平台**的 VSCode 扩展偶发白屏。此外，CLI 与 VSCode、JetBrains 等 IDE 间存在**功能非对称性**（如某些 MCP 工具仅在 CLI 可用），用户体验割裂。

#### 4. 差异化定位分析

| 工具名称 | 定位与核心优势 | 目标用户 | 技术路线特色 | 当前最大短板 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | **全面性与稳定性优先** | 追求开箱即用、工作流稳定的专业开发者 | 强调**会话管理 (Cowork, Plan mode)**、**安全稳健的沙箱和 MCP 实现** | **版本回归频繁**，新特性常伴随关键问题 (MCP 断连、权限配置失效) |
| **OpenAI Codex** | **多代理与前沿模型驱动** | 追求最新模型能力、探索多代理编排的技术先锋 | 强依赖**GPT-5.x 系列模型**的复杂推理能力，**MultiAgent V2** 是核心卖点 | **模型兼容性和系统状态管理混乱** (子代理强制模型、配额/重置 Bug) |
| **Gemini CLI** | **原生工具偏好与子代理体系** | 偏好 POSIX 环境、深度使用子代理的工作者 | 强调**子代理生态**、AST 感知代码理解、利用原生 bash 工具链实现安全沙箱 | **子代理和 Shell 的执行可靠性极差** (挂起、误报、不触发技能) |
| **GitHub Copilot CLI** | **微软生态整合与 MCP 桥接** | 深度使用 GitHub、VSCode 和 Azure 生态的团队 | 通过 **Copilot 桌面应用**和 VSCode 生态管理 MCP 连接，强调**语音模式**与基础工具链 | **MCP 集成体验断裂**，语音模式质量堪忧，插件更新流程存在 Windows 平台缺陷 |
| **Kimi Code CLI** | **轻量级与 IDE 集成** | JetBrains / Zed 等 IDE 用户，追求简洁集成 | 通过 **ACP 协议** 拥抱第三方 IDE，功能简洁清晰 | **生态仍处早期**，功能深度与社区活跃度与前几名有较大差距 |
| **OpenCode** | **高度可配置与社区驱动** | 喜欢“折腾”、追求极致个性化和自动化的工作者 | **开源社区活力强**，功能（如 YOLO 模式、`/btw` 命令）由社区强烈驱动，迭代速度快 | **性能与稳定性问题突出** (CPU 高占用、模型兼容性) |
| **Qwen Code** | **多工作区 (Workspace) 管理与服务化** | 管理多个项目、追求本地化或远端开发服务的用户 | 核心特色是 **`qwen serve` 单 daemon 多工作区**模式，配合强大的 **Web Shell**，推动服务化演进 | **平台特定问题多** (macOS, JetBrains) ，功能迭代与稳定性保障之间需平衡 |

#### 5. 社区热度与成熟度

- **高热度 & 高成熟度 (成熟型)**: **Claude Code**。社区反馈量大、功能成熟，但用户对版本稳定性和预期行为一致性要求极高，“回归 Bug”是社区最敏感的触发词。
- **高热度 & 快速迭代 (成长型)**: **OpenAI Codex, OpenCode, Qwen Code**。这些工具社区活跃，新功能、新模型跟进快。但伴随而来的是问题较多，尤其是 OpenAI Codex 在多代理方面的“尚未打磨好”和 OpenCode 的性能稳定性问题。
- **中等热度 & 稳健发展 (稳健型)**: **Gemini CLI** 和 **GitHub Copilot CLI**。社区反馈问题聚焦明确，但整体迭代节奏相对平稳。Gemini 社区对子代理行为的一致性和可预测性呼声很高，而 Copilot CLI 则受到 MCP 集成和生态捆绑的挑战。
- **低热度 & 早期阶段 (萌芽型)**: **Kimi Code CLI**。社区反馈量少，问题较为基础，主要集中在配置一致性和资源解析上，尚处于功能补齐阶段。

#### 6. 值得关注的趋势信号

1.  **“子代理”的悖论**：所有工具都在押注“多代理”是未来，但社区的反馈一致指向了“子代理越多，不确定性越高”。**如何实现可控、可预测、可审计的多代理工作流**，将成为决定下一阶段产品竞争力的关键分水岭。`OpenAI Codex` 的“强绑定”和`Gemini CLI`的“弱可控”都是反面案例，`Claude Code`尝试通过更优雅的会话管理来平衡，但未从根本上解决问题。

2.  **MCP 从“潜力股”变成“问题少年”**：尽管 MCP 被广泛认为是连接 AI 与外部世界的标准协议，但当前的实现充满了“最后一公里”的摩擦（认证、连接、配置一致性问题）。**“MCP 连接成功了，但我无法使用里面任何工具”** 是今日最让开发者沮丧的体验之一。这预示着，MCP 的下一个发展阶段将是从“实现规范”转向“保障交付质量”。

3.  **安全与效率的二元对立**：沙箱、权限、内容审核等安全机制正在成为开发者追求极致效率（YOLO 模式）的阻碍。社区并非拒绝安全，而是拒绝**不可预测的弹窗**和**不透明的静默失败**。未来的趋势将是允许用户在高度信任的环境下选择“退出安全检查”，但同时需要提供清晰的审计日志和风险提示。

4.  **单一 CLI 到“服务化”演进**：`Qwen Code` 的 `qwen serve` 多工作区模式、`Kimi Code` 的 ACP 服务器、`OpenAI Codex` 的 `codex-rs` 守护进程，都指向一个趋势：**CLI 正在成为连接用户与远端 AI 服务的更轻量级客户端**。未来，我们可能会看到更多工具将核心 AI 计算服务化，CLI 本身则退化成一个表现层。

**对开发者的参考价值**:

- **选择工具**：如果您追求工作流的极致稳定，请优先考虑 Claude Code，但需密切关注其版本更新日志中的“regression”预测。如果您是习惯深度配置的“power user”，OpenCode 社区可能更符合您的喜好。若您的工作流强依赖多项目管理，Qwen Code 的“serve”模式值得尝试。
- **规避风险**：升级前，请务必浏览社区 Issues 列表中最新提交的、标题包含“Bug”、“Regression”的问题，尤其是关于子代理行为、MCP 连接和核心配置项的反馈。
- **拥抱趋势**：尽快熟悉 MCP 协议，理解其认证与连接模型，这将是未来主流集成方式。同时，要有意识地为您的 Agent 工作流设计“安全阈值”和“回退方案”，因为它随时可能“卡住”或“误报成功”。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，以下是根据您提供的 GitHub 仓库数据生成的 Claude Code Skills 社区热点报告。

---

## Claude Code Skills 社区热点报告（数据截至 2026-07-12）

### 1. 热门 Skills 排行

以下是社区关注度最高、讨论最活跃的 5 个 Skill 相关 PR，反映了核心痛点与创新方向。

- **#1298: fix(skill-creator): run_eval.py 修复**
  - **功能**: 修复 `run_eval.py` 在 Windows 和并行模式下的严重 Bug，并正确处理触发检测。
  - **社区焦点**: 这是整个生态的**头号问题**，关联 #556、#1169 等多个高票 Issue。`run_eval` 始终报告 0% 召回率，导致描述优化循环完全失效，社区参与者无法有效验证和改进自己的 Skill。
  - **状态**: OPEN
  - **链接**: https://github.com/anthropics/skills/pull/1298

- **#514: Add document-typography skill**
  - **功能**: 新增一个专注于文档排版质量的 Skill，解决“孤行”、“寡行”等AI生成文档中的常见问题。
  - **社区焦点**: 该 Skill 切中了 AI 生成文档的“最后一公里”痛点——排版细节。社区讨论集中在如何在输出前自动执行这些检查，以及对各种文档格式的兼容性上。
  - **状态**: OPEN
  - **链接**: https://github.com/anthropics/skills/pull/514

- **#1367: feat(skills): add self-audit skill**
  - **功能**: 引入一个“自我审计” Skill，在交付前对输出进行机械文件验证和四维度推理质量审查。
  - **社区焦点**: 这是一个**高价值创新**，从“被动输出”转向“主动质量门禁”。社区讨论热点在于其通用性、与现有工作流的集成，以及对不同大模型输出的适配能力。
  - **状态**: OPEN
  - **链接**: https://github.com/anthropics/skills/pull/1367

- **#723: feat: add testing-patterns skill**
  - **功能**: 一个全面的测试模式 Skill，涵盖单元测试、React组件测试、E2E测试等全栈测试策略。
  - **社区焦点**: 社区对**测试自动化**需求旺盛。讨论集中在Skill中推荐的“测试奖杯”模型是否足够具体，以及如何将其与 `skill-creator` 的优化循环结合，实现“测试即文档”。
  - **状态**: OPEN
  - **链接**: https://github.com/anthropics/skills/pull/723

- **#1302: Add color-expert skill**
  - **功能**: 一个专业的颜色专家 Skill，覆盖 ISCC-NBS、Munsell、CSS 等多种颜色系统及色彩空间使用建议。
  - **社区焦点**: 代表了**垂直领域深度**的 Skill 方向。讨论围绕如何在有限的 Prompt 中平衡“专家知识”与“通用性”，以及该 Skill 是否能与 `web-artifacts-builder` 等前端 Skill 良好协同。
  - **状态**: OPEN
  - **链接**: https://github.com/anthropics/skills/pull/1302

- **#210: Improve frontend-design skill clarity**
  - **功能**: 改进前端设计 Skill 的清晰度和可操作性，确保每个指令都具体且可执行。
  - **社区焦点**: 这反映了社区对现有 Skill **质量提升**的持续诉求。讨论集中在如何将抽象的设计原则转化为可供 AI 直接遵循的原子化步骤，避免输出风格漂移。
  - **状态**: OPEN
  - **链接**: https://github.com/anthropics/skills/pull/210

### 2. 社区需求趋势

从 Issues 中提炼出以下几个最受期待的 Skill 发展方向：

- **安全与信任**：`#492` (安全命名空间问题) 获得 34 条评论和 2 个赞，是最热 Issue。社区强烈呼吁官方建立**社区 Skill 的签名、审核与分发机制**，防止基于 `anthropic/` 命名空间的信任边界滥用。
- **组织级协作**：`#228` (组织内 Skill 共享) 获得 14 条评论和 7 个赞。用户急需一个**集中式 Skill 库或共享链接**，以替代当前“下载-传输-手动导入”的低效流程，实现团队内 Skill 的便捷分发。
- **文档与排版优化**：`#514` 和 `#198` (文档 Skills 重复) 表明，社区对**高质量、无歧义的文档处理**（特别是 ODT、PDF、DOCX 格式）有刚性需求。改善排版、避免处理错误是核心诉求。
- **AI 安全与治理**：`#412` (代理治理 Skill) 获得 6 条评论。社区开始探索将 Claude Code 用于更复杂的自主任务，因此需要**内置的安全策略执行、威胁检测和信任评分**等治理模式。
- **工具链集成**：`#16` (将 Skills 暴露为 MCP) 和 `#29` (与 Bedrock 集成) 表明，社区希望 Skills 能更好地融入现有开发者工具和工作流，而不仅限于 Claude Code 内部。

### 3. 高潜力待合并 Skills

以下 PR 讨论活跃且尚未合并，代表未来短期内可能落地的创新功能：

- **#514: document-typography skill**：精准打击 AI 生成文档的排版顽疾，实用价值极高，有望解决 C 端用户体验的一个关键破绽。
- **#1367: self-audit skill**：开创性地将质量审计引入 Skill 输出机制，是 Skill 从“生成工具”向“可信交付品”演进的关键一步。
- **#723: testing-patterns skill**：满足开发者对**代码质量和测试覆盖率**的核心诉求，能显著提升 Claude 在软件工程任务中的可靠性。
- **#486: ODT skill**：填补了 ODF 格式处理的空白，对于企业级用户尤为重要，是生态全面性的必要补充。
- **#1302: color-expert skill**：展示了 Skill 在**专业化知识下沉**上的巨大潜力，证明了除代码外，设计、排版等创造性领域同样值得深挖。

### 4. Skills 生态洞察

**一句话总结：当前社区最集中的诉求是，解决 `skill-creator` 工具链的可靠性问题（特别是触发检测失败导致的 0% 召回率 Bug），以解锁社区贡献的闭环，同时向组织协作、安全保障和文档处理的深度与广度扩展。**

---

好的，作为专注于 AI 开发工具的技术分析师，我已根据您提供的 GitHub 数据源 (github.com/anthropics/claude-code) 精心整理并生成了 2026-07-12 的 Claude Code 社区动态日报。

---

# 2026-07-12 Claude Code 社区动态日报

## 今日速览
今日社区最关注的是 `v2.1.207` 版本发布，其中 **Auto Mode** 在云平台全面可用是最大亮点。然而，该版本也引入了一个 **stdio MCP Server 在 4 小时后被 SIGINT 且不再重启** 的严重回归问题，引发了开发者的紧急反馈。此外，**Windows 平台上的 Cowork 功能故障** 和 **终端标题配置需求** 依然是社区讨论的焦点。

## 版本发布
**v2.1.207** 版本于昨日发布，是当前社区讨论的焦点。主要更新内容包括：
- **Auto Mode 全面开放**：无需再设置 `CLAUDE_CODE_ENABLE_AUTO_MODE` 环境变量，即可在 Bedrock、Vertex AI 和 Foundry 上直接使用。用户可通过设置中的 `disableAutoMode` 关闭此功能。
- **关键 Bug 修复**：修复了在流式传输包含超长列表、表格、段落等内容时，导致终端冻结和按键输入延迟的问题。

## 社区热点 Issues（Top 10）

1.  **[Bug] Windows 11 Pro 上 Cowork 功能不可用** (#74649)
    - **重要性**: 🔥🔥🔥🔥🔥 社区最热 Issue，评论数高达 51 条，但无人点赞，说明这是一个影响范围极广但尚未被官方确认的严重障碍。
    - **摘要**: 报错缺失 `vfpext` HCS 服务，导致 Windows 11 Pro 用户无法使用 Cowork 功能。
    - **链接**: [https://github.com/anthropics/claude-code/issues/74649](https://github.com/anthropics/claude-code/issues/74649)

2.  **[Bug, 回归] `dangerouslyDisableSandbox` 指令不再抑制 Bash 权限弹窗** (#51798)
    - **重要性**: 🔥🔥🔥🔥 虽已关闭，但获得 3 个 👍，表明该回归问题 (自 2.1.116+ 起) 严重影响了依赖自动化脚本的用户工作流。
    - **摘要**: 之前版本中，`PreToolUse` 钩子返回 `allow` 可以静默执行无沙箱的 Bash 命令，但自 2.1.116 起回归，即使配置了 `allow`，仍会弹出交互式确认提示。
    - **链接**: [https://github.com/anthropics/claude-code/issues/51798](https://github.com/anthropics/claude-code/issues/51798)

3.  **[Feature] 脚本化终端标题配置** (#17951)
    - **重要性**: 🔥🔥🔥🔥 获得高达 32 个 👍，是近期呼声最高的功能需求之一。
    - **摘要**: 希望 Claude Code 能够像 `statusLine` 一样，支持通过脚本动态设置终端标题，以更好地标识不同会话或任务。
    - **链接**: [https://github.com/anthropics/claude-code/issues/17951](https://github.com/anthropics/claude-code/issues/17951)

4.  **[Bug, 回归] v2.1.92 自动压缩阈值无故降低至 400K tokens** (#43989)
    - **重要性**: 🔥🔥🔥 获得 7 个 👍，这是个典型的不声张的回归，严重影响使用 Opus 4.6 大上下文窗口的用户体验。
    - **摘要**: 在 Opus 4.6 (1M context) 上，自动压缩阈值从 ~1M 被降至 ~400K，且发布日志中无任何相关说明。
    - **链接**: [https://github.com/anthropics/claude-code/issues/43989](https://github.com/anthropics/claude-code/issues/43989)

5.  **[Bug] v2.1.207 严重回归: stdio MCP Server 在 4h 后被主动断开且不重连** (#76769)
    - **重要性**: 🔥🔥🔥🔥 这是昨日新版本的紧急问题，直接影响长期运行任务的稳定性。
    - **摘要**: 一个长期运行的会话中，`stdio` 模式的 MCP 服务器在启动约 4 小时后会被发送 `SIGINT` 信号并停止，且不会自动重启，导致会话功能降级。
    - **链接**: [https://github.com/anthropics/claude-code/issues/76769](https://github.com/anthropics/claude-code/issues/76769)

6.  **[Feature] 允许在工作进行中使用 `/fork` 命令** (#76777)
    - **重要性**: 🔥🔥🔥 这是一个新颖且实用的功能请求，体现了开发者想要更灵活地并行控制会话的需求。
    - **摘要**: 希望在 Claude 正在思考或执行任务时，能够通过 `/fork` 命令创建一个新的分支会话，以便在不中断当前任务的情况下并行处理其他问题。
    - **链接**: [https://github.com/anthropics/claude-code/issues/76777](https://github.com/anthropics/claude-code/issues/76777)

7.  **[Bug] 模型输出包含不当短语 “The money shot”** (#76540)
    - **重要性**: 🔥🔥🔥 这是一个典型的模型安全性和内容审核问题，虽然只有 2 条评论，但性质敏感。
    - **摘要**: 报告指出 LLM 的输出中不应出现 “The money shot” 这类不当短语。
    - **链接**: [https://github.com/anthropics/claude-code/issues/76540](https://github.com/anthropics/claude-code/issues/76540)

8.  **[Bug] Hook 输入中缺少会话名称** (#36058)
    - **重要性**: 🔥🔥🔥 获得 5 个 👍，该需求虽然提出较早，但对于多会话管理的开发者来说是个实用痛点。
    - **摘要**: 在 Hook 输入中提供了 `session_id` (随机ID)，但未提供用户通过 `/rename` 设置的可读 **session_name**，导致难以在通知中区分不同会话。
    - **链接**: [https://github.com/anthropics/claude-code/issues/36058](https://github.com/anthropics/claude-code/issues/36058)

9.  **[Bug] Plan 面板的评论未传递给 Claude** (#75399)
    - **重要性**: 🔥🔥🔥 Plan 模式 UI 功能存在缺陷，影响协作体验。
    - **摘要**: Plan 模式 UI 中的“选中文本并添加评论”功能似乎并未将评论内容注入到 Claude 的上下文中，导致评论不生效。
    - **链接**: [https://github.com/anthropics/claude-code/issues/75399](https://github.com/anthropics/claude-code/issues/75399)

10. **[Bug] VSCode 插件中缺失 `mcp__ide__getDiagnostics` 工具** (#40766)
    - **重要性**: 🔥🔥🔥 获得 7 个 👍，凸显了 IDE 集成一致性是社区高度关注的领域。
    - **摘要**: 在 CLI 集成终端中可用的 `mcp__ide__getDiagnostics` 工具，在 VSCode 扩展面板中却缺失了。
    - **链接**: [https://github.com/anthropics/claude-code/issues/40766](https://github.com/anthropics/claude-code/issues/40766)

## 重要 PR 进展（共 5 条，全部列出）

1.  **PR: 移除前端设计技能中的“复古未来主义”建议** (#39043)
    - **重要性**: 🛠️ 一个来自社区名人 `@t3dotgg` 的有趣提案，旨在改善 Claude 在特定领域的生成质量。
    - **摘要**: 作者直接指出该技能建议过时或不合时宜，要求删除。
    - **链接**: [https://github.com/anthropics/claude-code/pull/39043](https://github.com/anthropics/claude-code/pull/39043)

2.  **PR: 修复 macOS 系统证书加载及 Bun 运行时 NO_PROXY 黑洞** (#76640)
    - **重要性**: 🛠️ 修复了 macOS 上使用 Bun 运行时的一个连接问题。
    - **摘要**: 解决了 macOS 系统下，Bun 运行时因未加载系统证书存储以及 `NO_PROXY` 变量处理不当导致的“Self-signed certificate detected”SSL 连接错误。
    - **链接**: [https://github.com/anthropics/claude-code/pull/76640](https://github.com/anthropics/claude-code/pull/76640)

3.  **PR: 强化插件脚本中的 YAML、路径和符号链接处理** (#76581 & #76576)
    - **重要性**: 🛠️ 核心安全加固，预防潜在的攻击向量。
    - **摘要**: 两个 PR 都专注于修复插件开发中的安全问题。前者加固了 YAML 注入、路径穿越及符号链接凭证覆盖；后者则同步更新文档以匹配 v2.1.207 对插件 hook、MCP 命令等 shell 注入的修复。
    - **链接**: [PR 1](https://github.com/anthropics/claude-code/pull/76581) & [PR 2](https://github.com/anthropics/claude-code/pull/76576)

4.  **PR: 修复重复性审计中发现的设计缺陷** (#76673)
    - **重要性**: 🛠️ 来自日本开发者的内部质量改进。
    - **摘要**: 该 PR 修复了在重复性审计中发现的一系列缺陷，包括 Issue 分类、状态管理、Ralph 状态隔离以及 Hookify 的语法问题。
    - **链接**: [https://github.com/anthropics/claude-code/pull/76673](https://github.com/anthropics/claude-code/pull/76673)

## 功能需求趋势
从近日的 Issues 中可以提炼出以下社区最关注的功能方向：
- **自动化与工作流增强**：呼声最高。除了新支持的 **Auto Mode**，社区还强烈要求能在工作过程中使用 `/fork` 命令，以及改进 **terminal title** 的自动化配置。
- **平台间功能一致性与协作**：**Windows 平台上的 Cowork** 功能是最大的痛点。同时，开发者期待 CLI 和 VSCode 等 IDE 插件之间的功能 (如 MCP 工具 `getDiagnostics`) 保持一致。
- **上下文管理与内存系统改进**：用户希望有更好的 **context usage monitoring**、**user-global memory** 以及更可控的 **MEMORY.md** 内容注入，以提升 Agent 在多项目、长会话场景下的表现。
- **安全性与内容审核**：模型输出内容审核（如不当短语）和插件系统安全（注入防护）受到持续关注。

## 开发者关注点
综合来看，开发者当前最关心的痛点和高频需求是：
- **稳定性与回归**：`v2.1.207` 发布的 **MCP Server 4h 断连** 问题是头号不稳定因素。此外，`dangerouslyDisableSandbox` 令不被遵守和 `autocompact` 阈值无故降低等问题也让开发者对版本稳定性产生忧虑。
- **平台兼容性**：**Windows 上的 Cowork** 无法工作是目前最影响使用的单一 bug，严重阻碍了 Windows 用户采用该核心功能。
- **配置项失效**：`effortLevel: "max"` 在会话开始时被降级、`attribution.commit` 设置被忽略等问题，凸显了部分配置项不够健壮，实际行为与预期不符。
- **信息透明度**：Hook 中缺少 `session_name`、Terminal Title 无法自定义，以及 Plan 面板评论不生效，都反映了开发者对更细粒度、更透明的信息控制和反馈机制的强烈需求。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 | 2026-07-12

## 今日速览

昨日发布了一个新的 Alpha 版本 `rust-v0.145.0-alpha.4`，但未附带详细更新说明。社区讨论热度集中在 **GPT-5.6 Sol 子代理模型强制默认行为**（#31814）和 **重置配额意外丢失**（#31606、#32484）两个核心问题上。此外，多个新提交的 Issue 指向 **GPT-5.x 模型配置异常**与 **Windows 沙箱兼容性**，反映出开发者在升级新版时遇到明显阻碍。

## 版本发布

- **rust-v0.145.0-alpha.4**  
  [Release 链接](https://github.com/openai/codex/releases/tag/rust-v0.145.0-alpha.4)  
  仅标注版本号，无额外变更日志。建议有条件的用户跟踪 Git 标签进行测试。

## 社区热点 Issues

1. **#31814 – GPT-5.6 Sol 无法指定子代理模型，强制所有子代理也为 Sol 实例**  
   [链接](https://github.com/openai/codex/issues/31814)  
   **为什么重要**：高赞 101、49 条评论。用户反映 Sol 模型的元数据自动启用 MultiAgent V2，且隐藏子代理元数据导致无法自定义子代理模型配置，严重影响多代理工作流。社区多人遇到类似问题，期待官方快速修复或提供覆盖机制。

2. **#31606 – “重置失败，未应用且浪费了 1 次重置”**  
   [链接](https://github.com/openai/codex/issues/31606)  
   **为什么重要**：30 条评论，39 个 👍。Pro 用户的重置按钮点击后计数器下降但未真正应用，属于数据一致性问题。多个用户反馈重置机制不可靠，影响每日使用体验。

3. **#32041 – VS Code 扩展 26.5707.* 在 Linux 上显示空白 Webview**  
   [链接](https://github.com/openai/codex/issues/32041)  
   **为什么重要**：22 条评论，Linux 用户无法使用最新扩展。回退到 26.5623 虽然可用但缺少 5.6-Sol 支持。暴露了新版扩展在 Linux 下的关键 UI 渲染 bug。

4. **#5538 – Codex CLI 响应时输入消息消失**  
   [链接](https://github.com/openai/codex/issues/5538)  
   **为什么重要**：持续近一年仍开放，19 条评论，10 个 👍。在 TUI 模式下，用户输入的部分内容会在模型响应时被截断或消失，属于基础可用性问题，至今未修复。

5. **#21653 – 支持多行状态行（TUI）**  
   [链接](https://github.com/openai/codex/issues/21653)  
   **为什么重要**：39 个 👍，10 条评论。用户自定义状态行过长时被截断，希望支持折行。反映了社区对 TUI 可配置性和信息密度的需求。

6. **#31846 – Codex 桌面 App：GPT-5.3 Codex Spark 因 “Unsupported parameter: reasoning.summary” 失败**  
   [链接](https://github.com/openai/codex/issues/31846)  
   **为什么重要**：18 个 👍，9 条评论。用户切换模型时遇到参数不兼容，说明模型间参数集未同步，影响多模型切换的平滑性。

7. **#28504 – Pro 账户缺少 Codex 重置银行和邀请/推荐权益**  
   [链接](https://github.com/openai/codex/issues/28504)  
   **为什么重要**：6 个 👍，7 条评论。付费用户（$200/月）无法获得应得的重置次数和推荐奖励，可能是服务端配置或账户同步问题，直接关联付费价值。

8. **#32486 – 默认 GPT-5.6 上下文可能越过 272K 高使用量阈值**  
   [链接](https://github.com/openai/codex/issues/32486)  
   **为什么重要**：最新 Issue（2026-07-11 提交），4 条评论。默认配置下会话上下文自动进入更高定价区间，用户未主动选择。影响成本控制和透明度。

9. **#32484 – 5 小时配额和每周总额无故消失**  
   [链接](https://github.com/openai/codex/issues/32484)  
   **为什么重要**：最新 Issue，3 条评论。用户重置后配额显示 100%，但立即消失，属于严重的配额计算或展示 bug。

10. **#32487 – Windows 沙箱因 Smart App Control 阻止未签名的 node_repl.exe 而失败**  
    [链接](https://github.com/openai/codex/issues/32487)  
    **为什么重要**：最新 Issue，3 条评论。Windows 11 Pro 用户启用 Smart App Control 后沙箱无法启动，影响 Codex 安全性依赖的沙箱功能在新系统环境下的兼容性。

## 重要 PR 进展

1. **#31526 – 限制 hosted 客户端仅使用注册的工具**  
   [链接](https://github.com/openai/codex/pull/31526)  
   **内容**：为 app-server 托管客户端引入 `server_registered_tools_only` 功能，通过 MCP 允许列表精确控制工具。有助于提升托管环境的工具安全性和可预期性。

2. **#32485 – 在切换视图中利用可用宽度显示技能名**  
   [链接](https://github.com/openai/codex/pull/32485)  
   **内容**：修复技能切换弹窗中名称被截断为 21 字符的问题，改为使用完整名称。提升 UI 可读性，避免同名技能混淆。

3. **#32461 – 渲染 TUI diff 时展开制表符**  
   [链接](https://github.com/openai/codex/pull/32461)  
   **内容**：将 diff 中的制表符替换为四个空格，防止换行错乱。提升 TUI 下 diff 显示的一致性和可用性。

4. **#32460 – 守护进程中断后发送线程空闲生命周期事件**  
   [链接](https://github.com/openai/codex/pull/32460)  
   **内容**：当守护进程因自动审查拒绝而中止活动 turn 时，正确触发 `thread-idle` 生命周期，扩展开发者可据此做出响应，提高与扩展系统的集成度。

5. **#32441 – 内存合并时保留父沙箱的强制策略**  
   [链接](https://github.com/openai/codex/pull/32441)  
   **内容**：将父 turn 的权限配置传递给合并代理，防止内存合并时绕过沙箱限制。属于安全加固，确保子代理不继承不适当的权限。

6. **#31806 – 将新发布同步到 Cloudflare R2**  
   [链接](https://github.com/openai/codex/pull/31806)  
   **内容**：在 GitHub Releases 之外，向 R2 写入安装包副本，为后续内容分发网络加速和冗余做准备。不改变现有下载路径。

7. **#32332 – 为分页的 rollout 记录添加序号**  
   [链接](https://github.com/openai/codex/pull/32332)  
   **内容**：为分页历史记录中的 `RolloutLine` 增加零基序号，便于消费者增量处理。属于基础设施改进，对依赖历史记录的应用有益。

8. **#32326 – 在迁移配置通知中使用规范链接**  
   [链接](https://github.com/openai/codex/pull/32326)  
   **内容**：更新 `codex-rs/config.md` 中的文档链接，使其直接指向 GitHub 配置文档，包括 MCP 服务器部分。提升文档可访问性。

9. **#32316 – 停止回退到旧版模型可用性公告**  
   [链接](https://github.com/openai/codex/pull/32316)  
   **内容**：修复公告逻辑：优先选择目录中的第一个可用性公告，当其达到展示上限后不再回退到低优先级公告。确保用户每次只看到最新公告。

10. **#32302 – Unix IDE 上下文优先使用 Codex 主目录的 socket**  
    [链接](https://github.com/openai/codex/pull/32302)  
    **内容**：Unix 下 IDE 上下文 socket 优先查找 `$CODEX_HOME/ipc/ipc.sock`，失败再回退到临时目录。有助于统一多用户的 socket 路径，提升团队协作场景的可靠性。

## 功能需求趋势

- **子代理模型自定义**：社区强烈要求允许为子代理指定不同于主模型的模型（尤其是 GPT-5.6 Sol 的强制行为），显示多代理工作流正在成为核心用例。
- **配额与重置机制透明化**：多个 Issue 指向配额丢失、重置不生效、阈值不清等问题，用户期望明确的、可审计的配额管理系统。
- **多平台兼容性**：Linux VS Code 扩展空白 Webview、Windows 沙箱失败、FreeBSD 支持等表明跨平台体验仍是短板。
- **TUI 可用性改进**：多行状态行、输入消息丢失、diff 显示优化等需求持续出现，反映大量用户通过 CLI 使用 Codex。
- **模型参数兼容性**：GPT-5.x 系列模型间参数集不统一（如 `reasoning.summary` 不支持），用户期待线性升级或自动适配。
- **扩展与插件系统**：缓存技能、插件元数据、MCP 工具注册等 PR 说明正在强化扩展体系，但同时也引入了新的兼容性问题（如 ngs-analysis 插件默认提示超长）。

## 开发者关注点

- **付费用户的权益保障**：Pro 用户多次反馈重置次数、邀请奖励、5小时配额异常消失，严重影响信任。
- **升级风险**：VS Code 扩展新版导致 Linux 完全不可用，用户被迫停留在旧版，而旧版又不支持新模型，形成了升级陷阱。
- **沙箱与安全策略冲突**：Windows Smart App Control 阻止未签名二进制文件，导致沙箱功能开启失败，开发者需要临时关闭系统安全策略才能使用。
- **性能与状态管理**：会话上下文膨胀、重置失败、守护进程中断等 bug 提示 Codex 的状态管理机制在高负载或复杂工作流下不够健壮。
- **配置与文档可发现性**：config.md 链接修复、socket 路径统一等 PR 说明当前配置文档和 IPC 路径存在碎片化，社区希望更清晰的指引。

---

*数据截止：2026-07-11（UTC），日报生成于 2026-07-12。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# 2026-07-12 Gemini CLI 社区动态日报

## 今日速览
昨日（07-11）Gemini CLI 仓库无新版本发布，但社区活跃度较高，共收到7个PR更新和大量Issue讨论。核心关注点集中在**子代理行为可靠性**（如误报成功、挂起、不主动使用技能）、**终端与Shell执行稳定性**（命令卡住、引用循环崩溃）以及**安全与日志治理**（自动记忆重试、路径信任检查）。另有一项重要的VS Code扩展体验修复值得关注。

---

## 社区热点 Issues（10条）

1. **#22323 – Subagent recovery after MAX_TURNS 误报为 GOAL success**  
   🔥 评论10 👍2 | P1 | bug  
   `codebase_investigator` 子代理在达到最大轮次后被中断，却报告 `status: "success"` 和 `Termination Reason: "GOAL"`，掩盖了实际中断行为。社区认为这是影响用户信任的严重逻辑错误。  
   [链接](https://github.com/google-gemini/gemini-cli/issues/22323)

2. **#21409 – Generalist agent 无限挂起**  
   🔥 评论7 👍8 | P1 | bug  
   每当 Gemini 委托给 generalist agent 就会永久挂起（哪怕简单的文件夹创建）。用户已通过禁止使用子代理临时规避。该问题评论数虽非最高，但点赞量最高，说明影响面广。  
   [链接](https://github.com/google-gemini/gemini-cli/issues/21409)

3. **#25166 – Shell 命令执行后卡在 "Waiting input"**  
   🔥 评论4 👍3 | P1 | bug  
   Gemini 执行极简单的 CLI 命令（如 `ls`）后，终端仍显示“Awaiting user input”导致挂起，严重影响日常使用。  
   [链接](https://github.com/google-gemini/gemini-cli/issues/25166)

4. **#21968 – Gemini 不主动使用自定义技能和子代理**  
   🔥 评论6 | P2 | bug  
   用户反映即使配置了 gradle/git 等技能且描述清晰，Gemini 仍极少自主调用，仅在明确指令下才使用。这削弱了技能生态的价值。  
   [链接](https://github.com/google-gemini/gemini-cli/issues/21968)

5. **#19873 – 利用模型 bash 亲和性实现零依赖 OS 沙箱**  
   🔥 评论8 👍1 | P2 | enhancement/large  
   提议让 Gemini 3 模型使用原生 POSIX 工具链，通过隔离沙箱执行，在安全前提下发挥模型强项。虽然进展缓慢，但社区对其长期架构影响期待较高。  
   [链接](https://github.com/google-gemini/gemini-cli/issues/19873)

6. **#26522 – Auto Memory 无限重试低信号会话**  
   🔥 评论5 | P2 | bug  
   自动记忆系统将低信号会话视为“未处理”，导致后台提取代理反复重试，浪费配额和 CPU。该问题与其他记忆系统问题（#26516、#26523、#26525）构成记忆子系统质量改进系列。  
   [链接](https://github.com/google-gemini/gemini-cli/issues/26522)

7. **#24353 – 组件级行为评估 (EPIC)**  
   🔥 评论7 | P1 | customer-issue  
   发起 76 个行为评估测试并持续扩展，旨在系统化提升子代理的鲁棒性。该EPIC是质量保证的关键基础设施。  
   [链接](https://github.com/google-gemini/gemini-cli/issues/24353)

8. **#22745 – 评估 AST 感知文件读取、搜索与映射的价值**  
   🔥 评论7 👍1 | P2 | feature  
   通过 AST 工具（如 tilth/glyph）更精确读取方法边界、减少token噪声、定位交叉引用。若证实有效，可大幅提升 agent 代码理解效率。  
   [链接](https://github.com/google-gemini/gemini-cli/issues/22745)

9. **#21983 – Browser subagent 在 Wayland 下失败**  
   🔥 评论4 👍1 | P1 | bug  
   Browser Agent 在 Wayland 环境下因显示服务器兼容性问题始终无法成功，Termination Reason 仍为 GOAL。Wayland 用户群体受困。  
   [链接](https://github.com/google-gemini/gemini-cli/issues/21983)

10. **#21000 – 用原生文件工具创建与维护任务追踪器**  
    🔥 评论4 | P3 | customer-issue  
    探索用 `grep`/`sed`/`awk` 等原生工具替代MCP-based任务追踪，降低依赖并提升离线可用性。社区认为这是简化架构的正确方向。  
    [链接](https://github.com/google-gemini/gemini-cli/issues/21000)

---

## 重要 PR 进展（7条全部列出）

1. **#28183 – fix(vscode-ide-companion): 保持终端焦点**  
   当通过 VS Code 扩展确认文件编辑后，关闭 diff 预览会窃走集成终端焦点，用户需重新点击。此 PR 修复此体验问题，提升编辑流程连续性。  
   [链接](https://github.com/google-gemini/gemini-cli/pull/28183)

2. **#28359 – fix(core): 剥离 login/interactive shell 包装**  
   `stripShellWrapper` 原先仅识别裸 `-c`，无法处理 `bash -lc "..."`、`bash -ic "..."` 等包装，导致策略引擎无法正确重新检查包装后的命令。现在支持多种常见登录/交互 shell 包装格式。  
   [链接](https://github.com/google-gemini/gemini-cli/pull/28359)

3. **#28349 – fix(cli): 防止 customDeepMerge 因循环引用崩溃**  
   设置对象包含循环引用（如 `obj.self = obj`）时，`customDeepMerge` 递归无限循环导致 `RangeError`。增加循环检测避免配置管理器崩溃。  
   [链接](https://github.com/google-gemini/gemini-cli/pull/28349)

4. **#28319 – refactor(a2a-server): 在加载环境变量前强制路径信任检查**  
   将工作区路径信任检查提前到环境变量加载之前，并引入 `AsyncLocalStorage` 隔离任务环境，防止未信任目录的环境变量泄露或误用。  
   [链接](https://github.com/google-gemini/gemini-cli/pull/28319)

5. **#28164 – fix(core): 限制递归推理轮数上限**  
   为单次用户请求设置默认15轮的递归推理轮数上限（可配置），防止模型陷入无限循环消耗本地CPU与API配额。该PR已被合并关闭。  
   [链接](https://github.com/google-gemini/gemini-cli/pull/28164)

6. **#28248 – docs: 解释 MCP 环境变量扩展**  
   补充 `mcpServers` 路径/环境扩展文档，明确支持的语法（`$VAR`、`${VAR}`、`${VAR:-fallback}`、Windows `%VAR%`），并提示 `{{VAR}}`、`${env:VAR}`、`~` 不支持。  
   [链接](https://github.com/google-gemini/gemini-cli/pull/28248)

7. **#28247 – fix(core): 按相对路径匹配 ls 忽略 glob**  
   `ls` 忽略模式若包含路径分隔符，则现在按工作区相对路径匹配，`**` 等 glob 模式正确生效；仅 basename 模式保持原有行为。修复 #28207。  
   [链接](https://github.com/google-gemini/gemini-cli/pull/28247)

---

## 功能需求趋势

从昨日更新的Issues和PR中可提炼出社区最关注的五大功能方向：

- **子代理行为可预测性与鲁棒性**：包括纠正误报成功/隐藏中断（#22323）、强制agent更主动使用技能（#21968）、避免破坏性操作（#22672）、限制递归推理轮数（#28164）。社区希望agent“诚实”报告状态，并自动采用最安全的工具。
- **零依赖/原生工具优先策略**：倾向使用POSIX shell工具（grep/sed/awk）替代MCP或外部依赖，如任务追踪（#21000）、零依赖沙箱（#19873）。这契合模型原生能力且减少运维负担。
- **AST感知的代码理解**：引入AST工具提升文件读取精度、代码映射效率（#22745、#22746），降低token消耗，优化agent在大型项目中的表现。
- **自动记忆系统的安全与精细控制**：多个相关Bug（#26516系列）表明用户对自动记忆的“无意识重试”和“红action”感到担忧，要求增加确定性红action、隔离无效补丁、减少日志泄露。
- **终端与集成体验改善**：VS Code扩展焦点保持（#28183）、终端resize高性能（#21924）、外部编辑器退出后屏幕刷新（#24935）等PR，反映了对日常使用流畅度的强烈需求。

---

## 开发者关注点

1. **Shell执行卡死与交互干扰**：`#25166` 描述的命令完成仍显示“awaiting input”问题，以及 `#22465` 的vite创建交互式提示卡死，严重影响开发流程，是最高优先级的痛点。
2. **配置和子代理启停行为不一致**：`#22093` 指出 v0.33.0 后子代理无视禁用配置自动运行；`#22267` 指出 Browser Agent 忽略 settings.json 中的 maxTurns 等覆盖。配置生效是基础信任前提。
3. **子代理崩溃/挂起/资源浪费**：`#21409` 通用agent无限挂起、`#22323` 误报成功、`#26522` 自动记忆无限重试，导致用户不得不频繁中断或手动清理，对自动化体验伤害极大。
4. **跨平台兼容性不足**：`#21983` Browser Agent 在 Wayland 下完全失效；`#20079` symlink 不被识别为 agent。开发者呼吁增加更多环境测试。
5. **工具数量限制与清理干扰**：`#24246` 当工具超过128个时返回400错误；`#23571` 模型随机创建临时脚本，造成工作区污染。社区希望agent更智能地仅暴露当前上下文所需的工具，并主动清理临时产物。

---

*以上日报基于 2026-07-11 日更新数据整理。*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-07-12）

## 今日速览
过去24小时内，社区围绕 **MCP（Model Context Protocol）OAuth 连接中断、语音模式全模型无声、以及 Windows 插件更新权限问题** 等痛点展开了密集讨论；同时，跨应用会话同步、动态技能上下文注入等新需求获得开发者关注。唯一活跃的 PR 专注于安装脚本重复 PATH 条目的修复。

---

## 版本发布
- 无新版本发布。

---

## 社区热点 Issues（精选10条）

### 1. 🚨 语音模式所有内置 ASR 模型静默失败
**#4024**：`/voice` 录音正常（麦克风电平响应、原始 PulseAudio 捕获确认），但所有三种模型（nemotron-3.5-asr-streaming-0.6b、nemotron-speech-streaming…）均返回空转录。初步定位为 `MultiModalProcessor` 路由 bug，与 `nemotron_speech (RNNT)` 在 Foundry Local Core 中的调度逻辑冲突。  
[查看详情](https://github.com/github/copilot-cli/issues/4024)  

### 2. 🔐 Atlassian MCP 服务器 OAuth 成功但工具无法暴露给会话
**#4089**：OAuth 顺利完成，服务器显示绿色连接，但 `agent` 会话中始终找不到任何工具（其他 HTTP MCP 服务器如 LeanIX、Lucid 工作正常）。用户反馈 Windows 环境下配置相同，问题可稳定复现。  
[查看详情](https://github.com/github/copilot-cli/issues/4089)  

### 3. 📄 全局指令文件（AGENTS.md / CLAUDE.md）文档澄清需求
**#3983**：开发者对 `AGENTS.md`、`CLAUDE.md` 等全局指令文件的默认加载行为缺乏明确文档，导致多项目环境中的上下文冲突。该 issue 获 2 个 👍，表明社区对规范化文档的迫切需求。  
[查看详情](https://github.com/github/copilot-cli/issues/3983)  

### 4. 🌐 BYOK/自定义提供商模型发现功能请求
**#3795**：使用自带密钥（BYOK）模式时，用户必须手动设置 `COPILOT_MODEL` 或 `--model` 参数。社区期望 CLI 能自动查询自定义提供商支持的模型列表，简化配置流程。  
[查看详情](https://github.com/github/copilot-cli/issues/3795)  

### 5. 🔄 第三方 MCP 服务器“已连接”但工具缺失（OAuth token 未传递到会话）
**#4096**：在 Copilot 应用 UI 中登录第三方 OAuth MCP 服务器后显示绿色“Connected”，但 CLI 会话中工具始终不可用。OAuth token 似乎未被正确桥接到子会话进程。  
[查看详情](https://github.com/github/copilot-cli/issues/4096)  

### 6. 🪟 Windows 下插件更新失败：VS Code 运行中导致文件权限锁定
**#4095**：当 VS Code 运行时，`copilot plugin update` 因 Copilot 扩展持有 `installed-plugins` 目录的 watcher 句柄而失败，错误为 `Access is denied (os error 5)`。需要关闭 VS Code 或手动释放句柄才能更新。  
[查看详情](https://github.com/github/copilot-cli/issues/4095)  

### 7. 🗑️ 应用内删除会话不传播至 session-store.db / VS Code Chat 历史（孤立会话）
**#4094**：从 Copilot 桌面应用删除会话后，`data.db`、`session-store.db` 及 VS Code 的 `vscode.session.metadata.cache.json` 中记录依然存在，导致历史记录残留，且 VS Code 扩展仍能访问已删除会话的引用。  
[查看详情](https://github.com/github/copilot-cli/issues/4094)  

### 8. 🌐 语音模式下载在企业代理环境下因 ENOTFOUND 失败
**#4083**：下载语音模式推理运行时 `Microsoft.AI.Foundry.Local.Core 1.2.3` 时，因公司代理配置导致 `api.nuget.org` 域名无法解析。用户附上了代理补丁脚本，但官方尚未内置代理支持。  
[查看详情](https://github.com/github/copilot-cli/issues/4083)  

### 9. 🔗 跨应用会话同步（CLI ↔ 桌面应用）
**#4082**：macOS 用户反馈 CLI 启动的会话在桌面应用不可见，反之亦然。请求实现双向会话同步，或至少支持导入/导出。  
[查看详情](https://github.com/github/copilot-cli/issues/4082)  

### 10. 🧠 技能动态上下文注入（`!command` 占位符）
**#4088**：建议在 Agent Skills (`SKILL.md`) 中添加类似 `!` + 反引号 `command` 的占位符，使得技能在被调用时可动态嵌入命令执行结果，从而支持更灵活的上下文生成。  
[查看详情](https://github.com/github/copilot-cli/issues/4088)  

---

## 重要 PR 进展

**#2565**：`install: guard against duplicate PATH entries on reinstall`  
该 PR 由 @marcelsafin 提交，修复了在不重启 shell 的情况下重复运行安装脚本导致 shell profile 中 `PATH` 配置行被追加多次的问题。目前仍处于开放状态，待审核合并。  
[查看详情](https://github.com/github/copilot-cli/pull/2565)  

---

## 功能需求趋势

从过去24小时的 Issues 中，社区最关注的功能方向如下：

| 方向 | 代表 Issue | 说明 |
|------|------------|------|
| **MCP 连接可靠性** | #4089, #4096, #4085, #4084, #4086 | OAuth 流程无法完成、工具暴露失败、连接时长不稳定，成为 MCP 生态系统最大痛点 |
| **语音模式完善** | #4024, #4090, #4092 | 转录模型静默失败、自动提交功能（松键即发送）、语音捕获时自动静音系统播放 |
| **跨应用数据同步** | #4082, #4094 | 会话在 CLI、桌面应用、VS Code 之间的同步与删除一致性 |
| **动态上下文/技能增强** | #3983, #4088 | 全局指令文档澄清、技能内嵌动态命令占位符 |
| **企业/代理支持** | #4083 | 企业代理环境下包下载失败，需内置代理配置 |
| **插件/安装体验** | #4095 | Windows 平台文件锁引起的更新失败 |

---

## 开发者关注点

1. **MCP 认证流程的断裂体验**：多个 Issue 指向 OAuth 服务器连接后工具不可用，开发者需要反复重试或手动设置 `needs-auth` 标记，严重影响第三方工具集成效率。
2. **语音模式可用性**：所有内置 ASR 模型统一静默失败表明核心路由层存在严重 bug，而空间释放自动提交等细节需求也体现出社区对语音交互流畅性的高期待。
3. **插件更新与环境隔离**：Windows 用户遇到的文件锁问题暴露出 Copilot 扩展与 CLI 之间的资源竞争，提示需要在设计上引入更完善的句柄管理或后台更新机制。
4. **会话生命周期管理**：删除会话后残留数据导致 VS Code Chat 历史紊乱，开发者期望符合预期的“删除即彻底消失”行为，而非仅 UI 层面移除。
5. **BYOK 配置简化**：自定义模型用户期望 CLI 能主动发现可用模型，减少手动设置 `COPILOT_MODEL` 的试错成本。

---

*数据来源：github.com/github/copilot-cli（截至 2026-07-12 12:00 UTC）*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

好的，以下是根据您提供的数据生成的日报。

---

# Kimi Code CLI 社区动态日报 | 2026-07-12

## 📢 今日速览
过去24小时社区活跃度平稳，未发布新版本。主要动态包括一个涉及**插件资源错误归类**的 Bug 报告（#2491），以及三项由社区贡献的修复 PR：**背景代理任务时间戳丢失**、**字符串截断函数宽度超限**以及**ACP 服务器未加载全局 MCP 配置**。开发者对工具内部一致性和 UI 精确性的关注度较高。

## 📦 版本发布
无新版本发布。

## 🔥 社区热点 Issues

### 1. Bug: `kimi-datasource` 的 CHANGELOG.md 被错误列为 skill
- **Issue**: [#2491](https://github.com/MoonshotAI/kimi-cli/issues/2491)
- **作者**: @zhangleilaoge
- **状态**: Open，0 条评论
- **重要性**: ⭐⭐⭐ 该 Bug 会导致用户在 `/skill` 自动补全中看到 `CHANGELOG` 条目并误选，与[插件文档](https://www.kimi.com/code/docs/en/kimi-code-cli/customization/plugins.html)描述行为不符，影响插件生态的可靠性。
- **社区反应**: 尚未有社区讨论，但问题定位清晰，属典型解析逻辑缺陷。

## 🚀 重要 PR 进展

### 1. [#2493](https://github.com/MoonshotAI/kimi-cli/pull/2493) Fix: 记录后台 agent 任务的 `started_at` 以正确报告运行时长
- **作者**: @nankingjing
- **摘要**: 后台 **bash** 任务能正确设置 `started_at`，但后台 **agent** 任务缺失此字段，导致运行时长丢失。PR 在 agent worker 启动时补充了该赋值。
- **意义**: 修复了监控和日志系统中的一个隐蔽统计缺陷，提升后台任务的可观测性。

### 2. [#2492](https://github.com/MoonshotAI/kimi-cli/pull/2492) Fix: `shorten_middle` 输出因未扣除省略号长度而超出目标宽度
- **作者**: @nankingjing
- **摘要**: `src/kimi_cli/utils/string.py` 中的 `shorten_middle` 函数在计算左右切片宽度时未考虑 `"..."` 的 3 个字符，导致结果始终比 `width` 参数多出最多 3 个字符。PR 修正了计算逻辑。
- **意义**: 改善终端 UI 中文本截断的精确性，避免布局溢出。

### 3. [#2490](https://github.com/MoonshotAI/kimi-cli/pull/2490) Fix(acp): `kimi acp` 服务器加载全局 MCP 配置
- **作者**: @nankingjing
- **摘要**: 交互式 `kimi` 命令会加载用户全局 MCP 服务器配置，但 `kimi acp`（多会话 ACP 服务器）不会，导致 ACP 客户端（Zed、JetBrains AI Assistant 等）仅能看到内置工具。PR 使其与交互式模式保持一致。
- **意义**: 修复了与其他 IDE/编排工具的集成兼容性问题，补全了功能对等性（Fixes #2464）。

## 📊 功能需求趋势
从近期 Issue 和 PR 可提炼以下社区关注方向：

1. **插件资源正确解析** (#2491)：社区期望 `/skill` 自动补全仅显示真实技能，而非插件中的通用文件（如 CHANGELOG）。
2. **API/服务器配置一致性** (#2490)：开发者要求 `kimi acp` 模式与交互式模式在加载用户自定义 MCP 服务器方面行为一致，消除集成时的功能鸿沟。
3. **后台任务可观测性** (#2493)：对后台 agent 任务运行时的精确记录需求，暗示社区在复杂工作流中依赖时长数据进行调试或调度。
4. **UI 尺寸精确性** (#2492)：涉及终端输出宽度计算的 Bug 修复，表明社区对命令行界面渲染品质有较高要求。

## 🔧 开发者关注点
- **Bug 反馈的即时响应**：唯一 Issue #2491 尚未获得官方回复，但同日即有多项修复 PR（#2490、#2492、#2493）被提出，显示社区贡献者活跃，官方维护节奏仍需留意。
- **集成兼容性是高频痛点**：ACP 服务器未加载全局配置的问题 (#2490) 直接影响了主流 IDE（Zed、JetBrains）的协作体验，开发者对工具链横向对齐的期望强烈。
- **细节正确性驱动质量提升**：三个 PR 均针对边界条件或偶发逻辑错误，反映出开发者对 CLI 稳定性与行为可预测性的追求。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-07-12

## 📋 今日速览

- **性能与模型问题持续升温**：GPT-5.6 Luna 模型在使用 ChatGPT OAuth 时返回 404，社区高赞抗议；同时多起 CPU 高占用、Ollama 挂起等性能故障反复出现，部分用户被迫降级。
- **V2 TUI 关键 bug 修复**：社区提交的 PR #36466 解决了 V2 中自定义 Leader Key 被忽略的问题，合并后用户可正常使用 `~/.config/opencode/tui.json` 配置。
- **功能需求两极分化**：一边是高风险 YOLO 模式 ( `--dangerously-skip-permissions` ) 获得 91 个 👍 但争议激烈；另一边是 /btw 命令、自动模型发现等实用性需求霸榜。

---

## 🚀 版本发布

*（过去 24 小时内无新 Release）*

---

## 🔥 社区热点 Issues（10 条）

| # | 标题 | 状态 | 评论 | 👍 | 链接 |
|---|------|------|------|----|------|
| 1 | **#8463 [FEATURE]: Add `--dangerously-skip-permissions` (YOLO mode)** | OPEN | 28 | 91 | [查看](https://github.com/anomalyco/opencode/issues/8463) |
| 2 | **#16992 [FEATURE]: add /btw command** | OPEN | 18 | 153 | [查看](https://github.com/anomalyco/opencode/issues/16992) |
| 3 | **#6231 Auto-discover models from OpenAI-compatible provider endpoints** | OPEN | 16 | 169 | [查看](https://github.com/anomalyco/opencode/issues/6231) |
| 4 | **#36140 GPT-5.6 Luna returns model not found with ChatGPT OAuth** | OPEN | 16 | 68 | [查看](https://github.com/anomalyco/opencode/issues/36140) |
| 5 | **#30086 High CPU usage in newer versions** | OPEN | 24 | 13 | [查看](https://github.com/anomalyco/opencode/issues/30086) |
| 6 | **#4751 [CLOSED] [FEATURE]: Add config option to disable copy-on-select** | CLOSED | 25 | 18 | [查看](https://github.com/anomalyco/opencode/issues/4751) |
| 7 | **#8816 [FEATURE]: provide llms.txt and docs as markdown** | OPEN | 16 | 35 | [查看](https://github.com/anomalyco/opencode/issues/8816) |
| 8 | **#22132 OpenCode 1.4.3 hangs with local Ollama provider** | OPEN | 12 | 5 | [查看](https://github.com/anomalyco/opencode/issues/22132) |
| 9 | **#29548 OpenAI provider headers timeout after 10000ms on 1.15.11** | OPEN | 12 | 4 | [查看](https://github.com/anomalyco/opencode/issues/29548) |
| 10 | **#36465 "Revert message" should not modify code** | OPEN | 4 | 0 | [查看](https://github.com/anomalyco/opencode/issues/36465) |

### 解读

- **#8463 YOLO 模式**：允许用户在受信任环境中跳过所有权限确认（如文件访问、命令执行），核心争议在于安全性与自动化便利性的平衡。虽然赞数高，但标记为 `dangerously` 表明团队持谨慎态度。
- **#16992 /btw 命令**：灵感来自 Claude Code，允许用户在不打断对话流的情况下附加上下文（如“顺便说一下...”）。社区非常期待，👍 数 153 最高。
- **#6231 自动发现模型**：针对本地提供者（LM Studio、Ollama）手动列举模型的痛点。用户希望服务端自动调用 `/v1/models` 获取可用模型列表，消除配置错误。
- **#36140 GPT-5.6 Luna 404**：OpenAI 最新模型 gpt-5.6-luna 在 ChatGPT OAuth 下返回 “Model not found”，影响大量已付费用户。社区呼吁紧急修复模型映射表。
- **#30086 / #22132 性能问题**：多个用户报告从 1.14.28 升级后 CPU 占用飙升，甚至无法同时运行 3 个会话。同时 Ollama 提供者挂起问题重现，可能与请求超时或流处理逻辑有关。
- **#4751 禁用复制-on-select**：用户习惯阅读时高亮文字，导致 OpenCode 自动复制到剪贴板，干扰日常使用。虽已关闭，但提供了宝贵的配置思路。
- **#8816 llms.txt 文档**：希望 OpenCode 提供标准化文档格式（llms.txt + docs map），方便 LLM 工具解析官方文档，提升上下文质量。
- **#36465 revert 不应修改代码**：用户误点旧会话的“revert”导致 Git 损坏。社区认为当前 revert 会实际回滚代码改动，且缺少警告，存在风险。

---

## 🔧 重要 PR 进展（10 条）

| # | 标题 | 状态 | 描述 & 意义 | 链接 |
|---|------|------|-------------|------|
| 1 | **#34794 feat(provider): add --model free** | OPEN | 新增 `--model free` 选项，在 `opencode run` 和 TUI 中随机选择一个 Zero‑cost 模型。减少新手选择负担，同时降低免费用户的决策成本。 | [查看](https://github.com/anomalyco/opencode/pull/34794) |
| 2 | **#36466 fix(cli): load v2 tui config** | CLOSED | 修复 V2 TUI 忽略 `~/.config/opencode/tui.json` 中自定义 Leader Key 的问题。经过 `bun test` 验证，解决 #36458。 | [查看](https://github.com/anomalyco/opencode/pull/36466) |
| 3 | **#35866 docs: update xAI branding to SpaceXAI** | OPEN | 随着 xAI 更名为 SpaceXAI，更新所有用户可见的 provider 标签、OAuth 方法名及模型目录。保持品牌一致性。 | [查看](https://github.com/anomalyco/opencode/pull/35866) |
| 4 | **#31955 feat(app): add local whisper voice input** | CLOSED | 在 prompt 编辑器中添加麦克风按钮，支持本地 Whisper 语音转文字（离线）。提升移动场景下的输入效率。 | [查看](https://github.com/anomalyco/opencode/pull/31955) |
| 5 | **#31947 fix(tui): restore terminal capability detection over ssh** | CLOSED | 修复 1.16.0 起 TUI 在 SSH 会话中显示 16 色、主题色错误、tmux 失效的问题。回退到 1.15.13 的检测逻辑。 | [查看](https://github.com/anomalyco/opencode/pull/31947) |
| 6 | **#31946 fix: Windows session path, shell env, error message, and autocomplete** | CLOSED | 批量修复 Windows 上桌面会话路径错误、环境变量传递、错误信息不清晰及自动补全失效等问题。改善跨平台体验。 | [查看](https://github.com/anomalyco/opencode/pull/31946) |
| 7 | **#31945 fix(session): use parent relationship instead of ID ordering for loop exit condition** | CLOSED | 修复 Web 客户端传入自定义 `messageID` 时，条件循环退出的逻辑缺陷（原按 ID 字典序判断导致无限循环）。现在根据父子关系确定退出。 | [查看](https://github.com/anomalyco/opencode/pull/31945) |
| 8 | **#31940 feat(opencode): support MCP resource content** | CLOSED | 引入 MCP 资源内容解析：支持 `list_mcp_resources` / `read_mcp_resource` 工具调用；图片资源作为原生图片附件；其他二进制资源按 MIME 类型描述。 | [查看](https://github.com/anomalyco/opencode/pull/31940) |
| 9 | **#31929 fix(opencode): honor OpenAI baseURL for Codex OAuth** | CLOSED | 当用户为 OpenAI 设置自定义 `baseURL` 时，Codex OAuth 认证请求仍转发到官方 API。现在改为也遵循 `baseURL` 配置，兼容自托管代理。 | [查看](https://github.com/anomalyco/opencode/pull/31929) |
| 10 | **#31922 fix(opencode): bound SSE event backlogs and disconnect stalled consumers** | CLOSED | 解决 SSE 端点中无限累积事件导致内存泄漏的问题。设置每个订阅者的缓冲区上限，并主动断开不再消费数据的连接。 | [查看](https://github.com/anomalyco/opencode/pull/31922) |

### 补充说明

- 多个 `automated-pr-cleanup` 标记的 PR（如 #31955、#31947 等）表明团队正在执行大规模自动化清理，一次性合并了大量累积的 PR，覆盖了 Windows、SSH、会话逻辑等高频 bug。
- #34794 仍在 Open 状态，社区讨论积极，但有用户担心随机选模型可能导致质量和费用不可控。

---

## 📊 功能需求趋势

从本期所有 Issues 中归纳出社区最关注的三大方向：

| 趋势 | 代表 Issue | 热度 |
|------|-----------|------|
| **安全与权限简化** | #8463 YOLO 模式、#4751 禁用复制-on-select、#35303 匿名数据分享 | ⭐⭐⭐⭐⭐ |
| **提供者与模型管理** | #6231 自动发现模型、#36140 GPT-5.6 Luna 修复、#36247 Codex 上下文限制 | ⭐⭐⭐⭐⭐ |
| **协作与发现** | #36460 社区用户目录、#36134 会话拾取器入口 | ⭐⭐⭐ |
| **文档与上下文增强** | #8816 llms.txt、#16992 /btw 命令 | ⭐⭐⭐⭐ |
| **本地化与离线** | #22132 Ollama 挂起修复、#31955 离线 Whisper 语音输入 | ⭐⭐⭐ |

**核心洞察**：社区不再仅满足于“能用”，而是追求 **零摩擦的自动化工作流**（YOLO 模式 + 自动模型发现）和 **更好的可发现性**（/btw 命令、会话拾取器）。性能与模型兼容性依然是基础，但容忍度正在降低 —— 用户明确要求服务端主动暴露模型列表，而不是依赖手动配置。

---

## 👨‍💻 开发者关注点

1. **CPU 功耗失控**：多条 Issue（#30086、#4804、#19466）指向新版 OpenCode 即使空闲也占用大量 CPU（如 i9-14900 上单核 50%）。用户被迫降级或限制会话数量，严重影响开发效率。
2. **OpenAI 模型兼容性问题**：GPT-5.6 Luna 在 ChatGPT OAuth 下不可用（#36140），同时 Codex OAuth 给出的上下文限制与实际不符（#36247），导致开发者无法正确预估算力配额。
3. **升级与日志故障**：`opencode upgrade` 因 GitHub API 未认证配额超限而失败（#36260）；`--log-level DEBUG` 日志轮转后不生效（#17846）。这些基础流程问题降低了社区对团队质量保障的信心。
4. **V2 TUI 迁移阵痛**：Leader Key 配置被忽略（#36458）、初始用户消息丢失（#35988）、GUI 假死“thinking”（#35986）等问题频发，部分用户仍停留在 V1 版本。
5. **Windows 生态短板**：桌面端子进程显示问题（#31933）、文件选择器路径错误（#31848）、会话附件消息重复（#27928）等跨平台 bug 持续被反馈，Windows 用户体验仍需打磨。

---

*数据来源：GitHub `anomalyco/opencode` 仓库，统计时间截至 2026-07-11 23:59 UTC。*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 | 2026-07-12

## 1. 今日速览

昨夜发布了 `v0.19.8-nightly` 版本，修复了 YOLO 模式下模型调用 `enter_plan_mode` 时的行为，并新增了 `forward ask_user` CLI 功能。社区多工作区支持（RFC #6378）讨论活跃，评论数达 20 条；多个 PR 聚焦于 Web Shell 功能增强、MCP OAuth 恢复和会话恢复机制。开发者对 macOS 剪贴板缺失、JetBrains 集成问题、模型切换步骤繁琐等痛点反馈集中。

## 2. 版本发布

### v0.19.8-nightly.20260711.0ef3a76bd
- **fix(core):** 保持 YOLO 模式——当模型调用 `enter_plan_mode` 时不再自动退出 YOLO 模式。
- **feat(cli):** 添加 `forward ask_user` 功能，允许 CLI 将用户输入转发至 daemon 或其他处理器。
- **发布说明**: [GitHub Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.8-nightly.20260711.0ef3a76bd)

## 3. 社区热点 Issues（10 条）

### 🔥 #6378 RFC: 支持单个 daemon 管理多个工作区
**评论数: 20 | 状态: OPEN**  
RFC 提案让 `qwen serve` 单进程同时服务多个工作区，同时保持现有单工作区的兼容性。社区高度关注，讨论涉及会话隔离、API 路由设计和向后兼容性。  
[Issue 链接](https://github.com/QwenLM/qwen-code/issues/6378)

### 🔥 #6565 连接 Qwen Coder 时出现 Internal Error
**评论数: 11 | 状态: CLOSED**  
用户报告“糟糕！连接到 Qwen Coder 时出现问题”的错误，涉及多语言环境。已关闭，但诊断细节值得排查同类问题。  
[Issue 链接](https://github.com/QwenLM/qwen-code/issues/6565)

### 🔥 #6581 JetBrains ACP agent 无法接收用户提示
**评论数: 8 | 状态: CLOSED**  
IntelliJ IDEA 中 Qwen Code 作为 AI Assistant Agent 时，用户提示未被转发给 Qwen Code agent，仅传递了引导上下文。对 JetBrains 用户影响大。  
[Issue 链接](https://github.com/QwenLM/qwen-code/issues/6581)

### 🔥 #6590 macOS standalone 安装缺失粘贴板原生模块
**评论数: 5 | 状态: CLOSED**  
macOS 上 Ctrl+V 粘贴图片无响应，原因在于 `@teddyzhu/clipboard` 模块未被打包。社区已确认 root cause，欢迎 PR 修复。  
[Issue 链接](https://github.com/QwenLM/qwen-code/issues/6590)

### 🔥 #6654 API 错误：tool_use 块缺少对应的 tool_result
**评论数: 5 | 状态: CLOSED**  
模型返回了缺少对应结果的 tool_use ID，导致会话消息数组格式错误。可能影响调用 Anthropic 等 API 的稳定性。  
[Issue 链接](https://github.com/QwenLM/qwen-code/issues/6654)

### 🔥 #5970 YOLO 模式自动进入 Plan 模式
**评论数: 5 | 状态: CLOSED**  
用户以 `-y` 启动后，模型自动切换到 Plan 模式并请求读取文件，违背“YOLO”无确认的预期。社区认为这是回归 bug。  
[Issue 链接](https://github.com/QwenLM/qwen-code/issues/5970)

### 🔥 #6721 延迟工具发现使提示缓存前缀失效
**评论数: 4 | 状态: OPEN**  
主会话中通过 `tool_search` 发现隐藏工具时，会重新设置工具声明，破坏了缓存的 prompt 前缀，导致每次请求都重新计算。性能影响大。  
[Issue 链接](https://github.com/QwenLM/qwen-code/issues/6721)

### 🔥 #6639 MCP HTTP 服务器返回 401 时不触发 OAuth 恢复
**评论数: 3 | 状态: CLOSED**  
MCP 服务器通过 HTTP 传输且返回 401 时，Qwen Code 不会自动启动 OAuth 流程，所有受影响服务器显示为离线。安全与可用性相关。  
[Issue 链接](https://github.com/QwenLM/qwen-code/issues/6639)

### 🔥 #5967 支持内联模型切换命令 `/model <id> <prompt>`
**评论数: 3 | 状态: CLOSED**  
希望在一行输入中完成模型切换和发送 prompt，减少操作步骤。社区对此功能需求强烈。  
[Issue 链接](https://github.com/QwenLM/qwen-code/issues/5967)

### 🔥 #6699 重新设计 Web Shell 组合工具栏
**评论数: 3 | 状态: OPEN**  
提议在 Web Shell 输入框下方增加工作区切换、执行上下文和 Git 分支按钮，灵感来自 Codex 桌面客户端。前端 UX 改进方向。  
[Issue 链接](https://github.com/QwenLM/qwen-code/issues/6699)

## 4. 重要 PR 进展（10 条）

### 🚀 #6638 feat(serve): 扩展管理 v2
在 `qwen serve` 中引入扩展管理第二版，支持基于策略的激活（全局默认 + 工作区级覆盖）。服务端架构重要升级。  
[PR 链接](https://github.com/QwenLM/qwen-code/pull/6638)

### 🚀 #6628 feat(core): 可配置的前台 Shell 命令默认超时
新增 `tools.shell.defaultTimeoutMs` 配置项，支持用户自定义前台 Shell 超时时间，提升灵活性。  
[PR 链接](https://github.com/QwenLM/qwen-code/pull/6628)

### 🚀 #6746 fix(web-shell): 跨工作区会话在分屏和概览中展示
修复多工作区 daemon 下 Web Shell 只能看到主工作区会话的问题，提升多工作区体验。  
[PR 链接](https://github.com/QwenLM/qwen-code/pull/6746)

### 🚀 #6738 fix(core): 在 /goal 评定中忽略推理内容
避免模型返回的 `reasoning`/`think` 标签污染目标自动评分的 JSON 解析，提高目标评估可靠性。  
[PR 链接](https://github.com/QwenLM/qwen-code/pull/6738)

### 🚀 #5928 feat(config): 添加 todosDirectory 配置项
允许将待办事项工具创建的 `todos` 存储到项目目录（如 `.qwen/todos`），方便 Git 同步与团队协作。  
[PR 链接](https://github.com/QwenLM/qwen-code/pull/5928)

### 🚀 #6707 feat(cli): 新增 `/reload-env` 命令热加载 API 密钥
无需重启 CLI 即可重新加载环境变量和 API 密钥，提升开发调试效率。  
[PR 链接](https://github.com/QwenLM/qwen-code/pull/6707)

### 🚀 #6096 feat(tool): 添加可选的 zvec-grep 代码搜索工具
集成 `zvec_grep`，支持语义搜索和正则搜索，可作为 workspace 搜索工具使用。  
[PR 链接](https://github.com/QwenLM/qwen-code/pull/6096)

### 🚀 #6723 fix: 保持延迟工具发现后 prompt 缓存前缀稳定
修复 #6721 中缓存失效问题：不再将发现工具实时暴露给 provider，而是作为模型可见内容返回。性能优化关键。  
[PR 链接](https://github.com/QwenLM/qwen-code/pull/6723)

### 🚀 #6732 fix(mcp): 在 HTTP 401 后恢复 OAuth 认证
针对 #6639 问题，增加 HEAD 探测和交互式 OAuth 流程，恢复 MCP 服务器认证能力。  
[PR 链接](https://github.com/QwenLM/qwen-code/pull/6732)

### 🚀 #6561 feat(web-shell): 添加工作区 Goals 页面，解决 daemon 重启后 /goal 丢失
为 Web Shell 增加 Goals 可视化页面，并修复 daemon 模式中 `/goal` 在会话恢复后被静默丢失的 bug。  
[PR 链接](https://github.com/QwenLM/qwen-code/pull/6561)

## 5. 功能需求趋势

从过去 24 小时的 Issues 和 PR 中可以识别出以下社区关注焦点：

- **多工作区/多会话管理**：RFC #6378 表明对单个 daemon 管理多个项目工作区的需求旺盛，配套的会话组织、跨工作区操作（#6646）成为高频话题。
- **Web Shell 前端增强**：大量 Issue 涉及 Web Shell 工具栏改进，包括工作区选择器（#6700）、Git 分支指示（#6702）、执行上下文、自定义颜色（#6744）等。
- **MCP 集成与认证**：HTTP 传输的 MCP 服务器在 401 时 OAuth 恢复（#6639）以及扩展管理 v2（#6638）显示社区对插件生态的重视。
- **模型切换与灵活配置**：内联模型切换（#5967）、模型切换热键（#6486）、热加载环境变量（#6707）说明用户追求更快的开发流。
- **会话持久化与恢复**：daemon 重启后会话/工作区丢失（#6726）、通道会话恢复（#6680）、聊天记录持久化（#6743）等说明可靠性仍是核心诉求。
- **性能优化**：提示缓存前缀被延迟工具发现破坏（#6721）受到关注，社区希望提升大模型交互的缓存命中率。
- **新模型支持**：Claude Opus 4.6-4.8 的 token limit 错误（#6719、#6734）被快速修复，表明社区对 SOTA 模型的适配及时性要求高。

## 6. 开发者关注点

- **平台特定问题**：macOS standalone 安装缺失图片粘贴模块（#6590）是开发者的常见痛点，需尽快修补。
- **IDE 集成稳定性**：JetBrains ACP 不转发用户提示（#6581）严重影响 IDE 用户体验。
- **审批模式与 UI 一致性**：Shift+Tab 切换审批模式时提示信息中英文混杂（#6582），影响多语言用户体验。
- **工具行为不一致**：`read_file` 渲染内容导致 `edit` 工具失败（#4077）、YOLO 模式自动进入 Plan 模式（#5970）等降低信任度。
- **会话中断恢复歧义**：daemon 重启后无法区分用户取消与意外中断（#6710），导致会话状态不可靠。
- **配置持久化**：待办事项只能存在全局目录（#5928）、模型切换需两步操作（#5967）等显式说明开发者希望更细粒度的控制。
- **安全与故障恢复**：MCP HTTP 401 不触发 OAuth 恢复（#6639）、daemon 重启丢失工作区注册（#6726）是生产环境关键风险。

> 以上信息基于 GitHub 仓库 [QwenLM/qwen-code](https://github.com/QwenLM/qwen-code) 过去 24 小时的公开数据（截至 2026-07-12 00:00 UTC）。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*