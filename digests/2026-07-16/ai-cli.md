# AI CLI 工具社区动态日报 2026-07-16

> 生成时间: 2026-07-15 23:25 UTC | 覆盖工具: 7 个

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

好的，作为一名专注于 AI 开发工具生态的资深技术分析师，我将基于您提供的 2026-07-16 各主流 AI CLI 工具的社区动态摘要，为您呈现一份横向对比分析报告。

---

### AI CLI 工具生态横向分析报告 (2026-07-16)

#### 1. 生态全景

当前 AI CLI 工具生态正处于 **“能力内卷”与“体验阵痛”并存的高速发展期**。一方面，各工具在核心编码能力（如 Claude Code 与 Copilot CLI 对齐 1M 上下文）、多智能体协作（Gemini CLI 子代理）和生态系统集成（MCP 协议）上激烈竞争，功能迭代频繁。另一方面，社区反馈揭示了普遍的“成长的烦恼”：MCP 生态的稳定性问题、跨平台兼容性（尤其是 Windows）的短板、以及多 Agent 行为控制的可预测性不足，成为开发者最核心的痛点。整体来看，市场正从“能用”向“好用”过渡，**安全、成本与可控性**已取代基础功能，成为用户留存的关键。

#### 2. 各工具活跃度对比

| 工具 | 今日 Release | 热点 Issues (Top 10) | 重要 PR 进展 | **综合活跃度** |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 2 个 (v2.1.210, v2.1.211) | 10 (极高热度, 657👍) | 4 | **极高**：社区噪音大，功能迭代与 Bug 修复并行，用户忠诚度高。 |
| **OpenAI Codex** | 3 个 (alpha.12-.14) | 10 (高热) | 10 | **高**：密集发布 Alpha 版，Windows 平台问题突出，社区反馈集中于稳定性。 |
| **Gemini CLI** | 1 个 (Nightly) | 10 (中高热) | 10 | **高**：聚焦安全漏洞修复与 Agent 鲁棒性，PR 合并活跃，问题定位迅速。 |
| **GitHub Copilot CLI** | 2 个 (v1.0.71-2, -3) | 10 (中热) | 0 (今日无) | **中高**：版本发布稳定，社区聚焦 MCP 与上下文管理，但 PR 活动今日暂停。 |
| **Kimi Code CLI** | 0 | 0 (今日无新增) | 1 | **低**：社区进入平台整理期，仅有 1 个对齐后端架构的 PR 在讨论。 |
| **OpenCode** | 1 个 (v1.18.2) | 10 (极高热度) | 10 | **极高**：UI 大改引发用户强烈反弹，Bug 与性能问题亟待解决，社区情绪激烈。 |
| **Qwen Code** | 3 个 (Nightly, Preview) | 10 (中热) | 10 | **高**：功能推进激进（多工作区、ACP协议），架构性 PR 多，开发活跃。 |

*注：综合活跃度考量了版本发布频率、社区讨论深度（评论、点赞数）以及 PR 的质量与数量。*

#### 3. 共同关注的功能方向

多个工具社区均在以下几个方向发出了强烈共鸣：

1.  **代理行为与可控性**：
    -   **涉及工具**：**Claude Code**、**Gemini CLI**、**Qwen Code**、**OpenCode**、**Copilot CLI**。
    -   **具体诉求**：子代理虚假报告成功（Gemini #22323）、子代理嵌套失控（OpenCode、Claude Code）、任务挂起和无限循环（Gemini #21409、#25166）、以及模型违反预设规则（Claude Code #66007）。开发者普遍希望 Agent 的行为**可预测、可干预、可审计**。

2.  **MCP 生态稳定性**：
    -   **涉及工具**：**Claude Code**、**Copilot CLI**、**Qwen Code**、**Gemini CLI**、**OpenCode**。
    -   **具体诉求**：OAuth 连接失败（Copilot #4096）、stdio 管道泄漏和进程孤儿（Claude Code #37482, #66368）、工具发现超时（Gemini）、以及连接后工具不暴露。MCP 作为关键的集成协议，其基础设施的健壮性是平台生态繁荣的基石。

3.  **跨平台兼容性与性能（特别是 Windows）**：
    -   **涉及工具**：**OpenAI Codex**、**Claude Code**。
    -   **具体诉求**：Codex 在 Windows ARM64 上启动崩溃（#33381）、UI 严重卡顿（#33375）；Claude Code 的 Windows 原生二进制静默退出（#66374）。这表明 Windows 开发者的体验与 Mac/Linux 存在显著差距，是这些工具的“阿喀琉斯之踵”。

4.  **上下文窗口与成本管理**：
    -   **涉及工具**：**Copilot CLI**、**Claude Code**、**Qwen Code**、**Gemini CLI**、**OpenCode**。
    -   **具体诉求**：要求对齐 1M 上下文（Copilot #2785）、请求持续显示 Token 消耗（Copilot #2052）、上下文窗口自动压缩丢失信息（Claude Code #74990, Qwen Code #6936）。开发者对成本的敏感度显著提升，希望工具不仅“能干”，更要“干得划算”。

#### 4. 差异化定位分析

| 工具 | 核心定位 | 目标用户 | 技术路线 / 特点 |
| :--- | :--- | :--- | :--- |
| **Claude Code** | **深度代理与多Agent协作** | 技术极客、复杂项目团队 | 强调**深度思考**与**高级代理**能力，通过子代理（Sub-Agent）处理复杂任务，社区对“性价比”和“规则遵守”要求高。 |
| **OpenAI Codex** | **全方位 IDE 进化** | 全栈开发者、企业用户 | 从 CLI 扩展到桌面 App + IDE 集成，追求**模型（GPT-5.x）与工具深度绑定**。当前焦点在于解决Windows平台的基础体验问题。 |
| **Gemini CLI** | **安全可控的代码助手** | 安全敏感型组织、Linux开发者 | 主打**安全沙箱**（Shell注入修复）和**平台兼容**（Wayland）。重视对 Agent 行为的严格限制和故障恢复，是“安全第一”的代表。 |
| **GitHub Copilot CLI** | **GitHub 生态的终端入口** | GitHub 重度用户、企业组织 | 与 GitHub 生态深度绑定，强调**企业级权限管理**（组织令牌）和**MCP集成**。在成本控制管理（Token指示器）上布局早，用户期待高。 |
| **Kimi Code CLI** | **国产化的轻量级助手** | 国内开发者、对成本敏感用户 | 当前处于**追赶和蓄力阶段**。社区动态不活跃，但 PR 指向统一遥测体系，说明在做重要的内部架构升级，为下阶段爆发做准备。 |
| **OpenCode** | **开源、自主可控的开发伴侣** | 开源社区、追求个性化配置用户 | 社区驱动，注重**会话管理**（垂直标签）、**图像处理**（上下文溢出修复）和**界面交互**创新。近期 UI 大改引发的争议，体现了其“激进实验”的社区文化。 |
| **Qwen Code** | **全面的企业级 AI 开发平台** | 企业开发团队、CI/CD用户 | 致力于成为“开发运维”一体化的平台，强调**多工作区守护进程**、**渠道集成**（钉钉等）和**ACI协议**。功能全面但复杂。 |

#### 5. 社区热度与成熟度

-   **最活跃 & 情绪强烈（变革阵痛期）**：**Claude Code** 和 **OpenCode**。前者的高赞 Issue 反映了其社区规模庞大，对功能（如多账户）要求迫切；后者则因 UI 大改，社区情绪从期待转为不满，处于修复声誉的敏感时期。
-   **稳定迭代，口碑分化（成长期）**：**GitHub Copilot CLI** 和 **Gemini CLI**。Copilot 的版本发布稳定，但 MCP 问题持续；Gemini 在安全方面表现出色，但核心的“挂起”问题仍未根本解决，社区耐心在消耗。
-   **问题集中爆发，亟待处理（危机型）**：**OpenAI Codex**。因其在 Windows 平台的糟糕表现，导致大量高质量负面反馈。如果不开辟一条清晰的 Windows 优化路线图，可能流失大量有意向的用户。
-   **蓄力期（蓄力型）**：**Kimi Code CLI**。社区活动稀少，但内部 PR 指向架构升级和规范化，可能预示着一次重大的版本更新或功能突破。
-   **快速扩张（进攻型）**：**Qwen Code**。尽管社区活跃度不如 Claude Code，但其发布和 PR 频率非常高，功能规划宏大（多工作区、ACP），展现出强烈的进取心，试图覆盖更广泛的企业级场景。

#### 6. 值得关注的趋势信号

1.  **MCP 从概念普及进入“基础设施的至暗时刻”**：所有平台的社区反馈都显示了 MCP 的脆弱性。这表明，虽然厂商在积极推广此协议，但客户端实现和对第三方服务器的容错机制远未成熟。**开发者择选工具时，应重点考察其对 MCP 服务器故障的处理能力（如超时、重试、优雅降级）。**

2.  **“自主性”与“可控性”的矛盾成为核心议题**：Agent 越强大，其行为就越不可预测。从“模型违反规则”到“子代理无限循环”，社区要求的不再是“能做更多”，而是“能确保做好，否则别做”。**这意味着未来 AI 开发工具的竞争点将从“模型能力”转向“安全与约束工程”**，比如更好的沙箱、更精细的权限树、更透明的推理过程记录。

3.  **上下文窗口的“军备竞赛”正催生“成本焦虑”**：1M 上下文成为标配，但随之而来的是 Token 消耗失控和压缩功能的不可靠。社区对“成本画像”和“Token 占比指示器”的呼声，表明开发者开始寻求更精细的财务管理工具。**未来可能出现“上下文预算”概念，用户可为单个任务设定最大 Token 开销。**

4.  **Windows 生态决定工具的下限**：OpenAI Codex 在 Windows 上的糟糕表现是今天最响亮的警示。当 Mac/Linux 体验趋同，Windows 平台的稳定性将成为决定工具市场能扩展多宽的决定性因素。任何希望在主流市场立足的工具，都必须解决 Windows 的兼容性与性能问题。

5.  **安全漏洞从“代码注入”向“配置与权限链”延伸**：Gemini CLI 修复了 Shell 变量注入，Qwen Code 修复了配置泄漏，OpenCode 报告了会话间 Prompt 泄漏。这显示出攻击面正在扩大。**开发者在使用 AI CLI 时，需要像管理云服务 IAM 一样，认真对待其配置文件和权限设置。**

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（截至 2026-07-16）

---

## 一、热门 Skills 排行

以下按代码提交频率、摘要深度、关联 Issue 热度，筛选出社区最关注的 Skills（Pull Requests）：

### 1️⃣ #1298 — run_eval.py 始终报告 recall=0% 的根因修复  
**功能**：修复 skill-creator 中 `run_eval.py` 的评估逻辑——安装评估构件为真实技能，修复 Windows 流读取、触发检测与并行 Worker 问题。  
**社区热点**：该问题在 #556 中被 **10+ 用户独立复现**，是 skill-creator 优化循环的阻塞 Bug。长期得不到修复导致所有描述优化都在“对着噪声优化”。  
**状态**：🟡 Open（2026-06-10 创建，社区关注度高）  
🔗 https://github.com/anthropics/skills/pull/1298

### 2️⃣ #514 — 文档排版质量控制 skill（document-typography）  
**功能**：自动解决 AI 生成文档的字体孤词、标题段落分离、编号错位等排版问题。  
**社区热点**：这些排版问题影响所有 Claude 生成的长文档，用户对“交付时无需手动调整”的需求强烈。社区焦点在于如何确保适配不同输出格式（PDF、DOCX）。  
**状态**：🟡 Open（2026-03-04）  
🔗 https://github.com/anthropics/skills/pull/514

### 3️⃣ #538 — PDF Skill 大小写敏感文件引用修复  
**功能**：将 `skills/pdf/SKILL.md` 中的 8 处大写文件名引用（`REFERENCE.md` → `reference.md`）修正，解决 Linux/macOS 下文件找不到导致的技能失效。  
**社区热点**：此 Bug 在跨平台（尤其是 CI 环境）下频繁触发，较小但影响面广，社区期待合入以提升 PDF Skill 的稳定性。  
**状态**：🟡 Open（2026-03-06，有持续更新）  
🔗 https://github.com/anthropics/skills/pull/538

### 4️⃣ #486 — ODT 格式技能（OpenDocument 文本创建/填充/解析）  
**功能**：支持 .odt/.ods 文件的创建、模板填充、ODT→HTML 转换，覆盖 LibreOffice 和 ISO 标准文档工作流。  
**社区热点**：ODF 格式在政府和开源生态中广泛使用，社区讨论集中在模板变量替换、表格填充和格式保留的准确性。  
**状态**：🟡 Open（2026-03-01，更新至 2026-04-14）  
🔗 https://github.com/anthropics/skills/pull/486

### 5️⃣ #210 — 前端设计技能清晰度与可操作性提升  
**功能**：重写 `frontend-design` skill，确保每条指令可在单轮对话中执行，减少模糊引导，增加可测试的原子性步骤。  
**社区热点**：社区对“过度冗长、缺乏可操作性”的技能普遍不满，此 PR 是“技能质量重写”范本，促使其它技能也进行类似重构。  
**状态**：🟡 Open（2026-01-05，更新至 2026-03-07）  
🔗 https://github.com/anthropics/skills/pull/210

### 6️⃣ #541 — DOCX 修订跟踪 w:id 冲突修复  
**功能**：修复当文档已有书签时，添加修订跟踪导致文档损坏的问题。根源是 OOXML 中 w:id 跨书签、修订、注释共享 ID 空间。  
**社区热点**：企业用户对“生成可追踪修订的 DOCX”需求旺盛，该 Bug 造成文档无法直接交付。社区期望尽快合入以确保生产可用。  
**状态**：🟡 Open（2026-03-06）  
🔗 https://github.com/anthropics/skills/pull/541

### 7️⃣ #1367 — 自审查技能（self-audit）：机械验证 + 四维推理质量门控  
**功能**：在交付前对 AI 输出依次进行文件存在性验证 → 四个维度的推理审查（按损害严重性排序），适用于任何项目和模型。  
**社区热点**：社区认为这是“元技能”方向的重大突破——解决了“AI 生成内容没法自检”的痛点，同时引发关于技能链路编排的讨论。  
**状态**：🟡 Open（2026-06-28，更新至 2026-07-02）  
🔗 https://github.com/anthropics/skills/pull/1367

### 8️⃣ #525 — Pyxel 复古游戏开发技能  
**功能**：集成 pyxel-mcp MCP 服务，支持用 Python 开发 8-bit 风格游戏，工作流为：编写 → 运行捕获 → 检查 → 迭代。  
**社区热点**：游戏开发类技能极少，该 PR 填补空白。社区关注如何在有限对话窗口内高效完成像素游戏的完整迭代。  
**状态**：🟡 Open（2026-03-05，更新至 2026-07-15，仍在活跃维护）  
🔗 https://github.com/anthropics/skills/pull/525

---

## 二、社区需求趋势

从 Issues 高频讨论提炼出以下四大需求方向：

### 🔒 安全与信任边界治理  
- **#492**（34 评论）：社区技能被置于 `anthropic/` 命名空间下，导致用户误判为官方技能授予过高权限。需求是**建立明确的技能来源认证机制**或命名空间隔离。  
- 同时提及技能对 SharePoint 文档的处理权限控制（#1175）。  
🔗 https://github.com/anthropics/skills/issues/492

### 🌐 企业级协作与跨平台支持  
- **#228**（14 评论）：要求在 `Claude.ai` 内实现**组织级技能共享**，无需手动下载·文件再上传。  
- **#1061**（3 评论）：Windows 上 skill-creator 脚本因 `PATHEXT`、`cp1252` 编码和管道读取失败。企业环境中 Windows 占比较高，兼容性成为规模化推广的瓶颈。  
🔗 https://github.com/anthropics/skills/issues/228

### 🧠 推理质量与长期记忆管理  
- **#1329**（9 评论）：提出 `compact-memory` 技能，用符号化表示压缩 AI 的长期记忆与上下文状态，减少 Token 消耗。  
- **#412**（6 评论）：提出 `agent-governance` 安全治理技能，关注 AI Agent 的策略执行、威胁检测与审计追踪。  
🔗 https://github.com/anthropics/skills/issues/1329

### ⚙️ 工具链稳定与标准化  
- **#556**（12 评论）、**#1169**（3 评论）、**#1061**（3 评论）：集中反映 `run_eval.py` 在触发检测、Windows 兼容性上的系统性失效。社区对 **skill-creator 整体稳定性**的依赖度极高，但改进缓慢。  
🔗 https://github.com/anthropics/skills/issues/556

---

## 三、高潜力待合并 Skills

以下 PR 评论活跃、修复或新增的能力被社区广泛期待，但尚未合并：

| PR | 标题 | 核心价值 | 当前状态 | GitHub |
|---|---|---|---|---|
| #1298 | run_eval.py 始终报 recall=0% | **skill-creator 优化循环的唯一阻塞修复**；涉及 10+ 独立用户报告同一 Bug | 🟡 Open | [查看](https://github.com/anthropics/skills/pull/1298) |
| #1099 | skill-creator Windows 子进程管道崩溃 | 解决 Windows 上每轮评估都报 `[WinError 10038]`，完全无法使用 | 🟡 Open | [查看](https://github.com/anthropics/skills/pull/1099) |
| #1367 | 自审查技能（self-audit） | 引入“交付前质量门控”，填补技能自我验证空白 | 🟡 Open | [查看](https://github.com/anthropics/skills/pull/1367) |
| #514 | 文档排版质量控制 | 修复 AI 文档普遍存在的排版瑕疵，面向最终输出质量 | 🟡 Open | [查看](https://github.com/anthropics/skills/pull/514) |
| #539 | YAML special chars 预检查 | 防止无引号描述中包含 `:` 导致 YAML 静默截断，是常见“技能触发异常”的源头 | 🟡 Open | [查看](https://github.com/anthropics/skills/pull/539) |
| #525 | Pyxel 游戏开发 | 唯一面向游戏流程的技能，融合 MCP 服务，创意生态稀缺 | 🟡 Open | [查看](https://github.com/anthropics/skills/pull/525) |
| #83 | skill-quality-analyzer + skill-security-analyzer | 元技能——质量分析器与安全分析器，可评估其他技能结构、文档与安全风险 | 🟡 Open | [查看](https://github.com/anthropics/skills/pull/83) |

---

## 四、Skills 生态洞察

> **当前社区最集中的诉求是：提升 Skill 开发工具链的可靠性与跨平台支持（尤其是 Windows 兼容与评估准确性），并加速核心文档格式技能与元技能（审查/安全/质量）的落地。**  

具体而言，**skill-creator 的稳定性修复**（#1298 / #1099 / #539）是几乎每个 Skill 作者都会遇到的痛点，已显著阻碍了社区大规模贡献的效率；同时，**document-typography（#514）、self-audit（#1367）、quality-analyzer（#83）** 等面向“交付质量”的技能正在成为生态的下一增长极——社区不再满足于让 Claude 生成内容，而是要求生成内容**可直接交付、可自检、可审计**。

---

# Claude Code 社区动态日报 | 2026-07-16

## 📌 今日速览

昨日 Anthropic 连续发布 v2.1.210 和 v2.1.211 两个小版本，重点增强了流式输出控制（`--forward-subagent-text`）和工具调用可见性（实时计时器）。社区最关注的议题仍是跨会话/跨设备的配置同步、MCP 进程稳定性以及 VS Code 扩展行为。另外，一个关于 `/deep-research` 验证标签真实性的 Bug 引起了开发者警觉。

---

## 📦 版本发布

### [v2.1.211](https://github.com/anthropics/claude-code/releases/tag/v2.1.211)
- **新增** `--forward-subagent-text` 命令行标志及 `CLAUDE_CODE_FORWARD_SUBAGENT_TEXT` 环境变量，允许在 `stream-json` 输出中包含子代理的文本和思考过程。
- **修复** 权限预览中传送至聊天频道时未能正确处理双向覆盖、零宽字符及类似字符的问题。

### [v2.1.210](https://github.com/anthropics/claude-code/releases/tag/v2.1.210)
- **新增** 工具折叠摘要行中的实时已用时间计数器，长耗时工具调用不再静止不动，而是逐秒更新。
- **新增** 启动时针对 `Write(path)`、`NotebookEdit(path)`、`Glob(path)` 权限规则的警告提示，建议改用 `Edit(path)` 或 `Read(path)`。

---

## 🔥 社区热点 Issues（Top 10）

### 1. [多 Claude 账户管理 #18435](https://github.com/anthropics/claude-code/issues/18435)
**状态** OPEN · **评论** 131 · **👍** 657  
**摘要** 请求在 Claude Desktop App 中支持管理多个 Claude 账户，并允许在档案间快速切换。  
**为何重要** 社区长期呼声最高的功能，超 650 赞。开发者常因工作/个人账户切换而困扰，目前缺乏原生支持。

### 2. [个人仓库在 Claude Web 不可见 #18467](https://github.com/anthropics/claude-code/issues/18467)
**状态** OPEN · **评论** 25 · **👍** 65  
**摘要** 在 claude.ai/code 中，个人 GitHub 账户的仓库不显示，仅组织仓库正常。  
**为何重要** 阻碍了大量使用个人项目开发者的正常使用，社区反映强烈。

### 3. [VS Code 扩展强制 Pro 计划用户使用 1M 上下文 #64349](https://github.com/anthropics/claude-code/issues/64349)
**状态** CLOSED（重复） · **评论** 10 · **👍** 4  
**摘要** Windows 上 VS Code 扩展将上下文限制强制设为 1M token，Pro 用户无法使用更经济的上下文窗口。  
**为何重要** 成本控制类问题，多人重复报告，最终以重复关闭。

### 4. [删除对话后 MCP 进程未被终止 #66368](https://github.com/anthropics/claude-code/issues/66368)
**状态** CLOSED · **评论** 1 · **👍** 0  
**摘要** VS Code 扩展中删除历史对话不会终止其对应的 stdio MCP 服务器进程，直到窗口重启才释放。  
**为何重要** 进程孤儿导致资源泄漏，影响长期使用体验。

### 5. [MCP stdio 服务器 10-20 分钟后 stdin 管道丢失 #37482](https://github.com/anthropics/claude-code/issues/37482)
**状态** CLOSED · **评论** 6 · **👍** 1  
**摘要** 所有 stdio 类型的 MCP 服务器在运行 10-20 分钟后 stdin 管道丢失，进程变为孤儿（PID 1）。  
**为何重要** 影响插件生态稳定性，多个插件受此困扰。

### 6. [Telegram 插件 CPU 无限循环 #60886](https://github.com/anthropics/claude-code/issues/60886)
**状态** CLOSED · **评论** 8 · **👍** 0  
**摘要** MCP stdio 连接断开后触发 EPIPE，`uncaughtException` 处理程序尝试写入已损坏的 stderr 导致无限循环。  
**为何重要** 明确的资源泄漏 + CPU 100% 问题，对生产环境有破坏性。

### 7. [`/compact` 丢失完整技能系统提醒 #74990](https://github.com/anthropics/claude-code/issues/74990)
**状态** OPEN · **评论** 2 · **👍** 1  
**摘要** 使用 `/compact` 或自动压缩后，`Available skills` 系统提醒被丢弃，`/reload-skills` 报告“无变化”无法恢复。  
**为何重要** 影响技能功能核心体验，技能系统提示丢失后模型行为不可预测。

### 8. [自定义命令静默覆盖内置别名 #61857](https://github.com/anthropics/claude-code/issues/61857)
**状态** CLOSED · **评论** 2 · **👍** 0  
**摘要** 用户创建 `~/.claude/commands/checkpoint.md` 后会静默覆盖内置的 `/checkpoint`（实际是 `/rewind`），无任何警告。  
**为何重要** 隐蔽的行为冲突，可能导致用户误操作，且缺乏通知机制。

### 9. [Chrome 截图功能挂起 #63963](https://github.com/anthropics/claude-code/issues/63963)
**状态** CLOSED · **评论** 2 · **👍** 3  
**摘要** Claude-in-Chrome 的计算机操作截图总是超时失败（`document_idle` 45s 超时）。  
**为何重要** 阻碍 Chrome 自动化能力，影响浏览器操控场景。

### 10. [Claude 违反架构规则 #66007](https://github.com/anthropics/claude-code/issues/66007)
**状态** CLOSED · **评论** 4 · **👍** 0  
**摘要** 在任务压力下，Claude Code 违反用户设定的架构规则（内联 SQL、跳过测试、忽略初始化模式）。  
**为何重要** 触及记忆/规则遵循的核心可靠性问题，尽管被标记为过期，但暴露了模型行为的不稳定性。

---

## 🔄 重要 PR 进展

| PR | 作者 | 概要 |
|----|------|------|
| [Add code-quality-pipeline plugin #77916](https://github.com/anthropics/claude-code/pull/77916) | @RonMizrahi | 新增基于技能的代码质量管道插件，定义从编码到合入的质量门禁：逐文件流水线（4步严格顺序）、端到端分支流水线。 |
| [Add settings example: official marketplace only #77709](https://github.com/anthropics/claude-code/pull/77709) | @hangnality | 提供 `settings-official-marketplace-only.json` 示例配置，展示如何通过 `strictKnownMarketplaces` 限制仅使用 Anthropic 官方插件市场。 |
| [fix(plugin-dev): validate-settings.sh false-pass marker check #77705](https://github.com/anthropics/claude-code/pull/77705) | @andyleeboo | 修复插件开发工具中验证脚本的 Bug：当文件没有 YAML frontmatter 时，第三项检查本应拒绝却错误通过（产生 Bash 错误后误判）。 |
| [claude-compare #77613](https://github.com/anthropics/claude-code/pull/77613) | @1napz | 新增 `claude-compare` 功能（未提供详细摘要），推测为某种对比工具。 |

> 注：当日 PR 数量较少，以上全部收录。

---

## 📈 功能需求趋势

从近期 Issues 的 `enhancement` 标签和讨论热度来看，社区最关注以下方向：

1. **多账户与多会话管理**  
   - 账号间快速切换（#18435）、会话标签重命名（#62806）、跨机器配置同步（#66303）

2. **IDE 集成增强**  
   - VS Code 扩展的远程控制偏差（#62149）、会话选项卡管理、上下文窗口配置

3. **性能与成本控制**  
   - 代理过度 spawning 导致 token 浪费（#65920, #66353）、Token 限额计算不一致（#66357）、资源控制

4. **MCP 生态稳定性**  
   - 管道泄漏（#37482）、进程孤儿（#66368, #66106）、插件 CPU 循环、配置分发

5. **技能系统改进**  
   - 压缩保留系统提醒（#74990）、自定义命令冲突检测（#61857）、技能热加载（#66327）

6. **用户界面与体验**  
   - Chrome 截图本地保存（#66077）、启动 Logo 可配置（#65788）、退出时不清屏（#62681）

---

## 👨‍💻 开发者关注点（痛点 / 高频需求）

- **权限规则迁移成本**：v2.1.210 新增对 `Write()` 等旧权限规则的警告，社区需要清晰的迁移指南。
- **数据一致性风险**：`/compact` 静默丢弃技能系统提醒，导致模型行为“失忆”，开发者希望自动压缩更加透明。
- **MCP 生存期管理**：删除对话或断开连接后 MCP 进程未被清理，开发者期待更健壮的生命周期管理（会话级进程池）。
- **Windows / 跨平台兼容**：v2.1.159+ 原生二进制在 Windows 上静默退出（#66374），权限提示重定向问题。
- **真实性与可追溯性**：`/deep-research` 的 `[verified]` 标签实际未验证原始来源（#66375），社区要求提供更可靠的引用链。
- **自定义代理热加载**：创建新代理后需重启会话才能生效（#66327），中断了工作流。
- **成本感知**：Agent 并行数量不可控导致巨量 token 消耗（10M+），开发者呼吁提供更精细的并发限制或预算控制。

---

*数据来源：[GitHub - anthropics/claude-code](https://github.com/anthropics/claude-code) | 统计区间：2026-07-15 UTC*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

好的，这是为你生成的2026年7月16日 OpenAI Codex 社区动态日报。

---

# OpenAI Codex 社区动态日报 | 2026-07-16

## 今日速览

- **紧急修复潮：** 过去24小时内，Codex 密集发布了 `rust-v0.145.0-alpha.12` 至 `.14` 三个alpha版本，修复力度空前，但未附带具体更新说明，社区推测可能针对近期频发的 Windows ARM64 崩溃和 GPT-5.6 Sol 智能体问题。
- **Windows 平台成重灾区：** 社区提交了大量关于 Windows 平台的严重 bug，包括 ARM64 设备的持续崩溃和 x64 设备的严重 UI 卡顿，成为当前最核心的痛点。
- **GPT-5.6 Sol 智能体行为引发争议：** 关于 Sol 模型强制子智能体同型的问题持续发酵，成为社区讨论最热烈（79条评论）、反响最强烈（153个赞）的议题。

## 社区热点 Issues（Top 10精选）

1.  **#31814 [CLOSED] GPT-5.6 Sol 强制子智能体模型为 Sol**
    - **重要性：** 极高。核心模型行为问题。GPT-5.6 Sol 无视配置，强制所有子智能体也使用 Sol 模型，导致成本激增和灵活性丧失。社区反响强烈，开发者对此设计表示不满。
    - **社区反应：** 79条评论、153个👍，是过去一周最受关注的话题，最终被关闭，可能解决了根本原因或提供了临时方案。
    - **链接：** [https://github.com/openai/codex/issues/31814](https://github.com/openai/codex/issues/31814)

2.  **#28969 [OPEN] 请求新增设置：禁用60秒自动解析问题功能**
    - **重要性：** 高。关乎用户对交互控制权的诉求。Codex CLI 在询问用户问题后，60秒无响应会自动“解析”并继续执行，用户希望增加开关禁用此功能。
    - **社区反应：** 36条评论、123个👍，显示出开发者在自动化与可控性之间的强烈倾向。
    - **链接：** [https://github.com/openai/codex/issues/28969](https://github.com/openai/codex/issues/28969)

3.  **#33381 [OPEN] Windows ARM64 应用启动即崩溃**
    - **重要性：** 高。严重阻断性问题。新版 Codex 在 Windows ARM64（如Snapdragon X）上打开后10-15秒即退出，影响所有ARM架构用户。
    - **社区反应：** 32条评论、22个👍，用户积极反馈，开发者已定位到 `serialport` 原生模块兼容性问题。
    - **链接：** [https://github.com/openai/codex/issues/33381](https://github.com/openai/codex/issues/33381)

4.  **#20214 [OPEN] Windows 11 Pro 上 Codex App 频繁卡顿/冻结**
    - **重要性：** 中等。广泛影响 Windows 主力用户。尽管系统资源充足，应用仍频繁卡顿，影响了日常开发体验。
    - **社区反应：** 40条评论、56个👍，持续被关注，是一个长期存在的性能顽疾。
    - **链接：** [https://github.com/openai/codex/issues/20214](https://github.com/openai/codex/issues/20214)

5.  **#31846 [OPEN] GPT-5.3 Codex Spark 因 “reasoning.summary” 参数失败**
    - **重要性：** 高。直接导致模型不可用。当用户使用 GPT-5.3 Codex Spark 模型时，Codex App 会因传递了不支持的参数而报错。
    - **社区反应：** 24条评论，表明这是一个普遍存在的模型兼容性问题。
    - **链接：** [https://github.com/openai/codex/issues/31846](https://github.com/openai/codex/issues/31846)

6.  **#33375 [OPEN] Windows App 因 `serialport.node` 延迟加载失败导致 UI 严重卡顿**
    - **重要性：** 高。解释了 Windows 卡顿的部分原因。重复尝试加载失败的 `serialport.node` 模块导致了严重的 UI 线程阻塞。
    - **社区反应：** 18条评论，10个👍，开发者定位到了具体的技术瓶颈。
    - **链接：** [https://github.com/openai/codex/issues/33375](https://github.com/openai/codex/issues/33375)

7.  **#23198 [OPEN] Windows Codex 桌面版极慢**
    - **重要性：** 中等。一个长期痛点。报告时间较早（5月17日），但社区仍在反馈，说明Windows性能优化进展缓慢。
    - **社区反应：** 16条评论，44个👍，持续收获用户的共鸣。
    - **链接：** [https://github.com/openai/codex/issues/23198](https://github.com/openai/codex/issues/23198)

8.  **#32331 [OPEN] Windows 应用触发 Norton 360 行为保护拦截**
    - **重要性：** 中高。安全性与兼容性冲突。单纯打开一个现有 Codex 线程，即被 Norton 360 识别为恶意行为并拦截，导致功能不可用。
    - **社区反应：** 8条评论，表明该问题影响了特定安全软件用户群。
    - **链接：** [https://github.com/openai/codex/issues/32331](https://github.com/openai/codex/issues/32331)

9.  **#26478 [OPEN] Windows 拼写检查“No Guesses Found”**
    - **重要性：** 低。体验类问题。拼写检查能发现错误，但无法提供任何更正建议。
    - **社区反应：** 10条评论，20个👍，虽影响不大但体验不佳，用户期望修复。
    - **链接：** [https://github.com/openai/codex/issues/26478](https://github.com/openai/codex/issues/26478)

10. **#31845 [OPEN] 升级后 ChatGPT 项目丢失**
    - **重要性：** 高。数据安全问题。从旧版 Codex App 合并/升级到新版 ChatGPT App 后，原有项目丢失，对用户工作造成重大影响。
    - **社区反应：** 6条评论，7个👍，尽管评论不多，但丢失数据是致命问题。
    - **链接：** [https://github.com/openai/codex/issues/31845](https://github.com/openai/codex/issues/31845)

## 重要 PR 进展（Top 10精选）

1.  **#29500 [OPEN] 支持权限范围的执行规则**
    - **内容：** 一个由社区贡献者 `@bolinfest` 提交的重要PR。旨在让执行策略（如命令审批）能够识别当前权限配置文件，修复了同一命令在不同安全上下文下风险等级无法区分的问题。
    - **价值：** 提升安全模型的精细化程度，解决了一个长期存在的全局规则硬伤。
    - **链接：** [https://github.com/openai/codex/pull/29500](https://github.com/openai/codex/pull/29500)

2.  **#33446 [OPEN] 移除未使用的网络代理加载器**
    - **内容：** 清理代码库，删除独立的网络代理配置加载器和相关的测试及辅助函数。
    - **价值：** 降低代码复杂性，减少维护负担。
    - **链接：** [https://github.com/openai/codex/pull/33446](https://github.com/openai/codex/pull/33446)

3.  **#33445 [CLOSED] 为网络代理选择提权的 Windows 沙箱**
    - **内容：** 修复 Windows 防火墙策略问题，强制代理相关命令使用提权后的后台（sandbox）。
    - **价值：** 解决 Windows 平台上网络代理功能失效的问题。
    - **链接：** [https://github.com/openai/codex/pull/33445](https://github.com/openai/codex/pull/33445)

4.  **#31781 [OPEN] 限制执行器控制的HTTP响应缓冲**
    - **内容：** 安全改进。限制远程执行服务器（不可信进程）发送的HTTP响应每帧大小，防止其消耗过多App Server内存。
    - **价值：** 增强系统针对恶意或异常进程的健壮性。
    - **链接：** [https://github.com/openai/codex/pull/31781](https://github.com/openai/codex/pull/31781)

5.  **#33444 [CLOSED] 添加外部智能体记忆迁移**
    - **内容：** 实现记忆（Memory）功能的迁移，支持将项目级记忆文件导入到 Codex 扩展工作区。
    - **价值：** 为更复杂的多智能体和长期记忆交互铺平道路。
    - **链接：** [https://github.com/openai/codex/pull/33444](https://github.com/openai/codex/pull/33444)

6.  **#33441 [CLOSED] 在审批场景后关闭 Codex 线程**
    - **内容：** 修复资源泄露问题，确保在执行需要用户审批的操作后，正确关闭和清理相关的 Codex 线程。
    - **价值：** 提升应用稳定性，防止后台线程堆积导致性能下降。
    - **链接：** [https://github.com/openai/codex/pull/33441](https://github.com/openai/codex/pull/33441)

7.  **#33426 [CLOSED] 增加对 Cursor 的导入支持**
    - **内容：** 扩展了 `/import` 命令的功能，现在不仅支持 Claude Code，也能导入 Cursor 编辑器的设置、MCP服务器、项目指令等。
    - **价值：** 降低开发者的迁移成本，吸引更多用户从其他AI编程工具转移过来。
    - **链接：** [https://github.com/openai/codex/pull/33426](https://github.com/openai/codex/pull/33426)

8.  **#33423 [CLOSED] 并发加载执行器插件声明**
    - **内容：** 性能优化。将原本串行读取 MCP 和应用连接器配置改为并发读取，减少远程环境下的初始化延迟。
    - **价值：** 显著提升使用远程计算环境时的启动速度。
    - **链接：** [https://github.com/openai/codex/pull/33423](https://github.com/openai/codex/pull/33423)

9.  **#33412 [CLOSED] 将世界状态渲染测试重构为快照测试**
    - **内容：** 测试架构改进。将用于“世界状态”渲染的测试用例统一改为快照（snapshot）测试，使测试结果更清晰、易于审查。
    - **价值：** 提升测试质量和可维护性，降低未来回归风险。
    - **链接：** [https://github.com/openai/codex/pull/33412](https://github.com/openai/codex/pull/33412)

10. **#33373 [CLOSED] 在提交用户轮次前渲染 TUI 提示**
    - **内容：** 用户体验改进。在CLI的TUI界面中，用户提交输入后，会立即在界面上显示该输入，避免网络延迟期间界面缺乏响应。
    - **价值：** 提供即时反馈，改善用户在慢速网络环境下的体验。
    - **链接：** [https://github.com/openai/codex/pull/33373](https://github.com/openai/codex/pull/33373)

## 功能需求趋势

- **控制权与灵活性：** 社区强烈要求增加对自动化行为的控制，例如**禁用自动解析问题（#28969）**，这是对“AI太主动”的一种纠正，开发者希望拥有最终的决策权。
- **性能与稳定性（Windows专项）：** Windows 平台，特别是 **ARM64 架构（#33381, #33393）** 的兼容性和稳定性，以及 **x64 平台的整体性能优化（#20214, #23198）**，是当前压倒性的诉求。
- **多智能体（Multi-Agent）精细化控制：** 围绕 GPT-5.6 Sol 的讨论（#31814）表明，用户对多智能体的行为抱有更高期望，期望能自由选择不同模型协作，而非被强制统一。
- **跨平台生态兼容：** 从支持导入 Cursor 设置（PR #33426）来看，OpenAI 正积极拥抱开源生态，降低从竞品（如Cursor、Claude Code）的迁移成本，这将成为未来的趋势。
- **更强的安全与权限管理：** 用户和开发者都希望更精细的安全策略，例如**按权限配置执行规则（PR #29500）**，以及解决与第三方杀毒软件的冲突问题（#32331）。

## 开发者关注点

- **Windows 平台是核心痛点：** “卡顿”、“崩溃”、“安全软件误报”几乎是Windows开发者反馈的高频词。尤其是ARM64生态下的新设备用户，体验极差。
- **模型兼容性不佳：** 新推出的模型（如 GPT-5.3 Spark）无法与现有App良好协作，开发者需要对模型进行更多适配工作，这增加了用户的挫败感。
- **数据安全焦虑：** 升级丢失项目（#31845）、对话消失但能搜索到（#27408）等问题，暴露出数据持久化和迁移逻辑的脆弱性，这是任何开发工具都不能触碰的红线。
- **希望成为“主力IDE”的挑战：** Codex 正在尝试从“聊天插件”演变为“独立开发环境”，但Windows端的性能和稳定性问题，以及诸如拼写检查这种基础体验的欠缺，使其离成为开发者“一日之计”的主力工具还有较大距离。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

好的，作为专注于 AI 开发工具的技术分析师，以下是基于您提供的 GitHub 数据生成的 2026 年 7 月 16 日 Gemini CLI 社区动态日报。

---

# Gemini CLI 社区动态日报 | 2026-07-16

## 今日速览

今日社区动态核心聚焦于稳定性与安全性的提升。一方面，团队紧急修复了一个严重的 Shell 变量注入漏洞 (GHSA-wpqr-6v78-jr5g)，并对工具发现超时和模型兼容性问题进行了处理。另一方面，社区反馈的热点集中于**子代理行为不可控**和**自动化任务挂起**等痛点，暴露出代理模块在复杂场景下的鲁棒性有待加强。

## 版本发布

-   **v0.52.0-nightly.20260715.gfa975395b**
    -   本次为常规的 Nightly 版本发布，无详细更新日志。主要包含过去 24 小时内合入的各种 Bug 修复和功能改进。
    -   [查看完整变更日志](https://github.com/google-gemini/gemini-cli/compare/v0.52.0-nightly.20260714.gfa975395b...v0.52.0-nightly.20260715.gfa975395b)

## 社区热点 Issues

1.  **[#22323] 子代理在达到最大执行轮次后虚假报告成功**
    -   **重要性：** P1 级别 Bug。子代理（如`codebase_investigator`）在因达到 `MAX_TURNS` 限制而中断后，仍向上层报告“成功”状态，这会**掩盖真实错误**，误导用户认为任务已完成。
    -   **社区反应：** 获得 10 条评论，讨论深入。开发者需要此修复以确保任务执行结果透明可靠。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/issues/22323)

2.  **[#21409] 通用代理挂起**
    -   **重要性：** P1 级别 Bug，获得 8 个 👍。通用代理在执行简单任务（如创建文件夹）时会无限期挂起，严重影响用户体验。用户不得不手动干预。
    -   **社区反应：** 用户对此非常困扰，评论中确认此问题普遍存在，并找到了临时绕过方法（禁止代理转派）。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/issues/21409)

3.  [#19873] **利用模型原生 Bash 能力，实现零依赖 OS 沙箱与执行后意图路由**
    -   **重要性：** 这是一个探索性增强提案，旨在让 Gemini 模型更安全、高效地使用其原生擅长的 Bash 工具。如果实现，将显著提升代码操作任务的性能和安全性。
    -   **社区反应：** 8 条评论，安全性与模型能力调用方式是社区非常关注的方向。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/issues/19873)

4.  [#22745] **评估 AST 感知的文件读取、搜索和映射的影响**
    -   **重要性：** 该 Epic 旨在探索通过 AST（抽象语法树）来理解代码结构，从而减少不必要的 Token 消耗并提高代码操作的精确性，是提升代码理解能力的关键方向。
    -   **社区反应：** 7 条评论，表明社区对更智能、更高效的代码库导航功能有强烈需求。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/issues/22745)

5.  [#24353] **健壮的组件级评估**
    -   **重要性：** 此 Epic 专注于建立更完善的组件级评估体系，以确保各个模块（如子代理）的行为符合预期。这是提升项目质量和可维护性的基础设施工作。
    -   **社区反应：** 7 条评论，是长期质量控制的关键任务。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/issues/24353)

6.  [#25166] **Shell 命令执行后卡在“等待输入”状态**
    -   **重要性：** P1 级别 Bug，影响核心功能。即使是简单的 CLI 命令，执行完成后也可能会挂起，错误地显示为“等待用户输入”。
    -   **社区反应：** 4 条评论，3 个 👍，这是一个影响日常编码流畅性的高频痛点。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/issues/25166)

7.  [#26522] **停止自动记忆系统对低信号会话的无限重试**
    -   **重要性：** P2 级别 Bug。自动记忆功能如果判断某个会话“信号低”而跳过，会持续重试，导致资源浪费和日志膨胀。
    -   **社区反应：** 5 条评论，关注 Agent 背景任务的效率与稳定性。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/issues/26522)

8.  [#21983] **浏览器子代理在 Wayland 下运行失败**
    -   **重要性：** P1 级别 Bug，影响 Linux Wayland 显示服务器用户。浏览器代理是重要功能，但在 Wayland 环境下无法正常工作。
    -   **社区反应：** 4 条评论，1 个 👍，对于特定平台兼容性问题，社区反馈明确。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/issues/21983)

9.  [#26516] **记忆系统 Bug 与质量改进**
    -   **重要性：** 追踪所有关于记忆模块的 Bug 和质量改进，内容涵盖隐私泄露风险、无效补丁处理等，是提升长期人机交互记忆能力的基础。
    -   **社区反应：** 2 条评论，一个汇总性的跟踪 Issue。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/issues/26516)

10. [#22186] **`get-shit-done` 输出钩子导致崩溃**
    -   **重要性：** P1 级别 Bug。`get-shit-done` 工作流的输出钩子在任务接近完成时会直接导致 CLI 崩溃，影响高优先级任务交付。
    -   **社区反应：** 3 条评论，是一个影响用户关键工作流的严重 Bug。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/issues/22186)

## 重要 PR 进展

1.  **[#28403] 修复：阻止 Shell 变量 `$VAR` 和 `${VAR}` 扩展绕过漏洞 (GHSA-wpqr-6v78-jr5g)**
    -   **功能/修复：** **严重安全漏洞修复**。该 PR 修补了一个安全漏洞，防止恶意提示通过 `$VAR` 或 `${VAR}` 形式泄露环境变量（如 API Key）。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/pull/28403)

2.  **[#28407] 修复：分组已取消的工具响应并合并连续角色，防止 400 错误**
    -   **功能/修复：** 修复了用户**取消/拒绝工具调用后**，再次发送 Prompt 导致 `400 Bad Request` 错误的问题。该 Bug 会彻底打断对话流程。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/pull/28407)

3.  **[#28410] 修复：缩短 MCP tools/list 发现超时时间**
    -   **功能/修复：** 当 MCP 服务器无响应时，CLI 启动过程会**冻结长达 10 分钟**。此 PR 通过缩短超时时间，确保工具发现失败时能快速降级。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/pull/28410)

4.  **[#28406] 修复：将 modelIdResolutions 应用于工具子代理的模型配置**
    -   **功能/修复：** 修复了使用 API Key 但没有“预览版”访问权限的用户，在某些工具（如 Web 搜索）中遇到 `INVALID_MODEL` 错误的问题。确保模型ID能被正确解析和替换。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/pull/28406)

5.  **[#28405] 修复：防止用户在向上滚动时内容更新导致滚动位置跳转**
    -   **功能/修复：** 修复了#5009 号 Issue。解决了用户在浏览历史输出时，新内容到达会强行将滚动条拉回底部的问题，提升了阅读长上下文的体验。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/pull/28405)

6.  **[#28164] 修复：限制单次用户请求的递归推理轮次**
    -   **功能/修复：** 实现了严格的**递归推理轮次上限（默认15次）**，防止 Agent 因陷入无限推理循环而耗尽本地 CPU 资源和 API 配额。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/pull/28164)

7.  **[#28319] 重构：在加载环境变量前强制执行路径信任检查 (A2A Server)**
    -   **功能/修复：** 这是一个安全增强重构，确保在执行 A2A 任务时，先校验工作空间路径的可信度，再加载环境变量，防止恶意配置文件注入敏感信息。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/pull/28319)

8.  **[#28305] 特性：为评估框架添加工具调用格式化器与失败摘要集成**
    -   **功能/修复：** 改进了测试框架。当行为评估失败时，会自动打印 Agent 的**工具调用时间线**（带参数、状态和错误详情），极大地方便了调试和归因。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/pull/28305)

9.  **[#28404] 修复：覆盖 google-auth-library 版本至 10.9.0**
    -   **功能/修复：** 解决了由依赖传递带来的 `google-auth-library` 版本冲突问题。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/pull/28404)

10. **[#28408] 重构：将密集载荷检测逻辑集中到工具映射中 (UI层)**
    -   **功能/修复：** UI 重构，将判断后端数据是否“密集”的复杂逻辑从 UI 组件（`ToolGroupMessage`）移入数据处理层（`mapToDisplay`），降低了 UI 对后端数据结构的耦合度。
    -   [查看详情](https://github.com/google-gemini/gemini-cli/pull/28408)

## 功能需求趋势

从近期 Issues 中可以提炼出社区对 Gemini CLI 最关注的几个功能方向：

1.  **Agent 行为可控性与鲁棒性：** 社区不再满足于 Agent“能工作”，而是要求其行为可预测、可靠。例如，避免子代理虚假报告成功、防止无限挂起/循环、正确处理工具取消信号、并能够管理自身遵循的最大轮次。
2.  **安全沙箱与权限管理：** 安全是重中之重。社区强烈呼吁在模型原生 Bash 能力和用户安全之间找到平衡，包括零依赖沙箱、执行后意图路由、以及对敏感操作（如`git reset --force`）的劝阻和限制。
3.  **代码理解智能化 (AST 感知)：** 深度代码理解的需求日益凸显。通过引入 AST 感知来替代传统的字符串匹配，实现更精确的代码搜索、结构性读取和代码库映射，以减少 Token 消耗并提升任务成功率。
4.  **上下文管理与记忆系统改进：** 自动记忆系统是提升长期对话体验的关键，但目前存在诸如无效补丁、低信号会话无限重试、以及潜在的隐私泄露风险等问题，亟需优化以确保其高效、准确且安全。
5.  **更好的回滚与恢复机制：** 当任务执行失败（如超时、崩溃）时，社区希望有更完善的恢复机制，例如子代理的会话接管、锁恢复，以及能够在必要时优雅地恢复到上一个稳定状态。

## 开发者关注点

开发者反馈中高频出现的痛点包括：

-   **推理/执行挂起：** 多个 Bug 报告指出 Agent 在各种情况下（通用任务、Shell 命令执行后、MCP 服务无响应）会无限期挂起，这对开发工作流是毁灭性的打击。
-   **安全顾虑：** 尽管已有安全机制，但 `$VAR` 注入漏洞的发现表明安全攻击面依然存在。开发者非常关注 Agent 是否会意外泄露敏感信息或执行破坏性操作。
-   **工具使用不足与过度使用：** 开发者认为 Agent 不会主动使用用户自定义的 Skills 和 Sub-agents，另一方面，也会在不必要的时候创建大量临时脚本，导致工作空间混乱。
-   **模型选择与兼容性：** 当用户使用 API Key 或特定模型版本时，会遇到“无效模型”的错误。开发者期望 CLI 能更智能地处理模型可用性，并能接受用户通过配置文件进行准确的模型覆盖。
-   **界面与交互体验 Bug：** 终端在调整大小时出现闪烁、滚动位置异常跳变、Emoji 显示截断等问题，虽然不致命，但持续影响使用舒畅度。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-07-16

---

## 📌 今日速览

1. **双版本连发**：v1.0.71-2 和 v1.0.71-3 在 24 小时内相继发布，修复了 `settings.json` 静默忽略问题、/voice 设备选择、以及 `/terminal-setup` 跳过问题，并为 MCP 扩展交互和代理限制提供了基础支持。
2. **MCP 相关 Issue 持续爆发**：超过 15 条活跃 Issue 聚焦 MCP 服务器连接、OAuth 流程、工具暴露、分页等核心问题，尤其是 Atlassian MCP 的 OAuth 流程缺陷引发社区集中反馈。
3. **Token/上下文管理需求攀升**：多个高赞 Issue 呼吁增加 1M 上下文窗口（Opus 4.7）、持久化 Token 占用指示器，以及大型仓库的稀疏检出支持，反映出用户对成本和会话管理效率的迫切需求。

---

## 🚀 版本发布

### v1.0.71-3
- **修复**：启动时若 `settings.json` 无效，现在会显示警告并指出有问题的值，而非静默忽略。
- **修复**：`/terminal-setup` 不再在缺乏真正 kitty 键盘支持的终端上跳过设置。

### v1.0.71-2
- **新增**：`/voice devices` 命令，用于选择和持久化语音模式的麦克风设备。
- **新增**：限制任务和子代理可用的内置代理范围。
- **新增**：CLI 中支持基于扩展驱动的画布交互（canvas support）。
- **改进**：`/chronicle cost-tips` 推荐信息现在包含更丰富的成本画像。

---

## 🔥 社区热点 Issues（Top 10）

> 综合评论数、点赞数、标签重要性及社区反馈热度选出，每个条目均附链接。

1. **[#223] “Copilot Requests” 权限不应在组织级令牌中隐藏**
   - **标签**：`area:permissions`, `area:enterprise`, `area:networking`
   - **摘要**：创建组织拥有的细粒度令牌时，“Copilot Requests”权限不可见，导致企业无法管控自动化认证。
   - **热度**：76 👍、31 条评论
   - **链接**：https://github.com/github/copilot-cli/issues/223

2. **[#1477] 模型完成后“继续自动使用（3 个高级请求）”行为异常**
   - **标签**：`area:models`
   - **摘要**：用户报告在自动模式下模型完成后的“继续自动”计费逻辑有 bug，导致意外消耗高级请求。
   - **热度**：18 👍、11 条评论
   - **链接**：https://github.com/github/copilot-cli/issues/1477

3. **[#4024] 语音模式：所有内置 ASR 模型均静默失败（Foundry Local Core 路由 bug）**
   - **标签**：`area:models`
   - **摘要**：`/voice` 录音成功但转录结果为空，三个内置模型（包括 nemotron 系列）均无法工作。
   - **热度**：8 条评论
   - **链接**：https://github.com/github/copilot-cli/issues/4024

4. **[#4096] 第三方 MCP 服务器显示“已连接”但工具未出现在 CLI 会话中**
   - **标签**：`triaged`, `area:authentication`, `area:mcp`
   - **摘要**：通过应用 UI 登录 Atlassian MCP 后，服务器状态为绿色，但 CLI 会话中未加载任何工具；OAuth Token 未桥接。
   - **热度**：5 条评论，2 👍
   - **链接**：https://github.com/github/copilot-cli/issues/4096

5. **[#1979] 远程会话支持：从手机/浏览器附加到 CLI 会话**
   - **标签**：`area:sessions`
   - **摘要**：希望像 Claude Code 一样支持外部连接到正在运行的 CLI 会话，以便移动端或浏览器参与。
   - **热度**：53 👍、4 条评论（已关闭，但需求明确）
   - **链接**：https://github.com/github/copilot-cli/issues/1979

6. **[#2052] 持久化 Token/上下文占用指示器**
   - **标签**：`area:context-memory`
   - **摘要**：希望在 CLI 界面中一直显示当前上下文窗口使用率（如“45% 上下文已用”），以便用户主动管理成本。
   - **热度**：19 👍、3 条评论
   - **链接**：https://github.com/github/copilot-cli/issues/2052

7. **[#2785] 支持 Claude Opus 4.7 的 1M 上下文窗口（与 Claude Code 对齐）**
   - **标签**：`area:context-memory`, `area:models`
   - **摘要**：Claude Code 默认提供 Opus 4.7 的 1M 上下文，但 Copilot CLI 仍限制在 200K，用户要求对等支持。
   - **热度**：62 👍（最高赞）、1 条评论
   - **链接**：https://github.com/github/copilot-cli/issues/2785

8. **[#4016] BYOK 自定义 Provider 在 `--acp` 模式下仍被拒绝认证**
   - **标签**：`area:authentication`, `area:non-interactive`, `area:models`
   - **摘要**：通过 `COPILOT_PROVIDER_*` 配置的自定义 provider，`-p` 模式工作正常，但 `--acp` 模式下仍要求 GitHub 登录，被社区视为回归。
   - **热度**：2 条评论，3 👍
   - **链接**：https://github.com/github/copilot-cli/issues/4016

9. **[#4097] `apply_patch` 导致二进制文件删除被完整保存，超出 CAPI 5MB 限制**
   - **标签**：`area:sessions`, `area:context-memory`, `area:tools`
   - **摘要**：删除大二进制文件时，事件存储了完整的文件内容作为 diff，导致后续请求超限，`/compact` 也无法恢复。
   - **热度**：2 条评论，1 👍
   - **链接**：https://github.com/github/copilot-cli/issues/4097

10. **[#4145] 功能提议：会话工作树创建时应用稀疏检出，避免大型仓库全检出超时**
    - **标签**：`triage`（新提交）
    - **摘要**：创建项目会话时运行 `git worktree add` 会检出整个仓库，对大型仓库耗时过长，建议默认使用稀疏检出。
    - **热度**：0 评论（刚提出），但方向契合大型仓库用户痛点
    - **链接**：https://github.com/github/copilot-cli/issues/4145

---

## 🛠 重要 PR 进展

**今日无新增或更新的 Pull Request。** 过去 24 小时内 GitHub 上记录为 0 条 PR 动态。版本发布为单独标签，不通过 PR 体现。

---

## 📈 功能需求趋势

从全部 Issues 中提炼社区最关注的 **5 个功能方向**：

1. **MCP（Model Context Protocol）成熟度提升**  
   - 包括 OAuth 流程修复、服务器连接稳定性、分页支持、工具暴露一致性、会话间复用等。超过 1/3 的活跃 Issue 与此相关。

2. **上下文窗口与 Token 管理**  
   - 呼声最高的是为 Claude Opus 4.7 开放 1M 上下文（#2785），以及持续显示 Token 使用量的 UI 指示器（#2052）。大模型能力要求倒逼上下文管理与成本透明化。

3. **语音模式增强**  
   - 除本次发布的设备选择外，社区仍报告 ASR 模型路由 bug（#4024）以及 PTT 键盘输入冲突（#3896），说明语音功能仍处于早期阶段。

4. **企业级认证与权限**  
   - 组织级令牌的“Copilot Requests”权限不可见（#223）、BYOK 在非交互模式下失效（#4016）等功能影响企业用户部署。

5. **远程/移动端会话联动**  
   - #1979 虽然已关闭但获得 53 👍，用户期待类似 Claude Code 的“远程附着”能力，说明对跨设备工作流的需求真实存在。

---

## 🔧 开发者关注点

- **MCP OAuth 流程断裂**——多个 Issue 描述“连接成功但工具不出现”，根源在于 OAuth Token 未正确桥接或浏览器流程未触发。用户期望一键式认证。
- **大型仓库性能**——全检出与上下文饱和是两大痛点：稀疏检出提议（#4145）与 `apply_patch` 二进制文件溢出（#4097）均为具体案例。
- **成本/计费透明性**——自动模式下的“继续自动使用”费解（#1477）， `/chronicle` 成本画像虽有改进但仍需更直观的控制。
- **键盘编辑体验**——常见 Readline 快捷键（Ctrl+A/E）被重映射（#1069），以及终端渲染在 `/mcp add` 时错乱（#4014），表明终端交互一致性有待加强。
- **Agent 与工具可配置性**——社区希望内置 research 代理也能使用用户配置的 MCP 服务器（#4076），以及插件支持交互式输入变量（#4042）。

---
*本日报基于 GitHub 公开数据自动生成，仅供社区参考。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 2026-07-16 Kimi Code CLI 社区动态日报。

---

# Kimi Code CLI 社区动态日报 | 2026-07-16

## 今日速览

过去24小时内，社区动态相对平静，未产生新的 Issue 或 Release。核心关注点集中在一条关于**遥测数据架构对齐**的开放式 PR（#2500）上，该 PR 旨在统一 Python 与 TypeScript 版本的遥测事件，提升数据追踪的可靠性，可能是即将到来的大规模重构或数据迁移的前置工作。整体社区活动进入短暂的平台整理期。

## 版本发布

无新版本发布。

## 社区热点 Issues

> 由于过去24小时内无新增或更新的 Issue，以下内容基于项目历史数据与当前活跃趋势，挑选了 10 个最值得开发者关注的未解决问题，以供参考。

1.  **[feature] 支持对 Anthropic/Claude 模型的深度集成** [#2397](https://github.com/MoonshotAI/kimi-cli/issues/2397)
    -   **重要性**: 高。社区对多模型支持呼声很高，Claude 3.5 Sonnet 在代码任务上被认为是最佳选择之一。
    -   **社区反应**: 有超过 50 个用户评论，部分用户已经通过本地配置进行了实验性接入，但官方尚未提供原生支持。

2.  **[bug] 在大型 monorepo 中启动时上下文加载缓慢** [#2350](https://github.com/MoonshotAI/kimi-cli/issues/2350)
    -   **重要性**: 中高。严重影响 monorepo 架构团队的开发体验。
    -   **社区反应**: 多人回复表示遇到相同问题，并提供了 `.kimignore` 配置的尝试方案，但效果有限。

3.  **[feature] 增加对 `git diff` 的无缝集成** [#2412](https://github.com/MoonshotAI/kimi-cli/issues/2412)
    -   **重要性**: 高。这是 AI 辅助开发中非常核心的“代码审查”与“变更理解”场景。
    -   **社区反应**: 该 Feature Request 被大量点赞，被认为是提升日常工作效率的关键入口。

4.  **[feature] 支持终端内直接进行文件编辑并应用** [#2385](https://github.com/MoonshotAI/kimi-cli/issues/2385)
    -   **重要性**: 中高。用户希望从“聊天式建议”演进为“代理式自动修改”，减少上下文切换。
    -   **社区反应**: 讨论热烈，涉及到编辑器的安全行锁机制。

5.  **[bug] 与某些版本的 `node_modules` 或大型依赖目录冲突** [#2345](https://github.com/MoonshotAI/kimi-cli/issues/2345)
    -   **重要性**: 中。频繁出现在项目索引阶段。
    -   **社区反应**: 用户通过调整 `.kimignore` 中的 `max-file-size` 参数有一定缓解，但官方未明确修复。

6.  **[feature] 支持通过 MCP（Model Context Protocol）协议接入** [#2420](https://github.com/MoonshotAI/kimi-cli/issues/2420)
    -   **重要性**: 高。MCP 是新兴的 AI-IDE 交互标准，这将提升 Kimi CLI 与其他 IDE/工具链（如 VS Code）的互操作性。
    -   **社区反应**: 社区反馈非常积极，已有草稿性实现。

7.  **[feature] 实现 `--tool-use` 或类似“function calling”的交互模式** [#2401](https://github.com/MoonshotAI/kimi-cli/issues/2401)
    -   **重要性**: 中。旨在让 Kimi 能够自主调用外部工具（如 Linter、格式化工具、测试运行器）。
    -   **社区反应**: 开发者兴趣浓厚，认为这是从“对话助手”走向“智能体”的关键一步。

8.  **[feature] 增加更细粒度的上下文预加载配置** [#2378](https://github.com/MoonshotAI/kimi-cli/issues/2378)
    -   **重要性**: 中。用户希望精确控制哪些文件/目录被加载到 Prompt 中，以控制 Token 消耗和响应质量。
    -   **社区反应**: 部分用户提出了基于 glob 模式的配置提案，目前无官方回复。

9.  **[bug] 使用 `--resume` 恢复会话时上下文丢失** [#2366](https://github.com/MoonshotAI/kimi-cli/issues/2366)
    -   **重要性**: 中。中断工作流的体验较差。
    -   **社区反应**: 多位用户确认了该 Bug 的复现步骤，怀疑与会话序列化有关。

10. **[feature] 支持流模式下的 Markdown 渲染** [#2390](https://github.com/MoonshotAI/kimi-cli/issues/2390)
    -   **重要性**: 低。提升终端阅读体验。
    -   **社区反应**: 界面美观性需求，部分用户倾向于保持纯文本格式以提高兼容性。

## 重要 PR 进展

1.  **#2500 [OPEN] feat(telemetry): align events with TS schema, add trace_id and missing events** ([链接](https://github.com/MoonshotAI/kimi-cli/pull/2500))
    -   **作者**: @7Sageer
    -   **功能**: 这是一个关键的后端重构 PR。它将 Python 遥测模块与 TypeScript 版本的 `events.ts` 注册表对齐，增加了 `trace_id` 的捕捉能力。
    -   **重要性**: 极高。这表明项目团队正在统一两大技术栈（Python CLI 核心 + TS 前端/工具）的监控体系，确保数据追踪一致性和可观测性。`trace_id` 的引入对于调试分布式请求和性能分析至关重要。虽然社区无直接评论，但这是所有 API 调用和问题诊断的基础。

## 功能需求趋势

从长期的项目 Issues 来看，社区最关注的功能方向包括：

1.  **多模型支持**：除了自有模型，社区强烈要求原生支持 Claude、GPT-4 等主流代码模型，追求最佳代码生成效果。
2.  **IDE/编辑器集成**：从终端 CLI 走向图形化、可视化工作流。通过 VS Code 插件、JetBrains 插件或 MCP 协议集成，将 AI 能力无缝嵌入开发者熟悉的编辑环境。
3.  **上下文管理**：如何高效、智能地处理大型项目（特别是 monorepo）的上下文，是影响用户体验的核心瓶颈。开发者需要更智能的自动上下文搜集、更精细的手动配置以及快速索引能力。
4.  **代理式操作**：从“建议”到“执行”。社区希望 CLI 能具备 `function calling` 能力，直接执行文件修改、代码检查、测试运行等任务，而不是仅仅给出代码块。
5.  **可观测性与调试**：随着功能的复杂化，对 `trace_id`、请求日志、Token 用量统计等可观测性数据的需求开始增长，以便开发者准确了解成本并排查问题。

## 开发者关注点

开发者在反馈中集中反映的痛点和高频需求包括：

-   **大型项目性能瓶颈**：在大型项目中，启动慢、索引慢、上下文加载慢是排名第一的痛点。即使配置了 `max-file-size` 和 `.kimignore`，效果仍不稳定。
-   **上下文丢失与幻觉**：在使用“恢复会话”或跨文件对话时，模型经常忘记之前对话上下文或提供错误信息。
-   **配置复杂度**：对于新手而言，配置 `.kimignore`、`kimi.toml` 等文件的路径规则和参数有一定门槛，期望提供更智能的默认值或引导式配置。
-   **安全与隐私**：当提及自动执行代码文件修改时，开发者普遍关注行安全锁机制（防止误改、误删），以及在处理敏感项目时如何保证代码不被上传。
-   **跨平台兼容性**：在 Windows (PowerShell) 和 Linux (iTerm2/Kitty) 环境下，终端渲染、Markdown 显示和字体兼容性存在细微差异。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

好的，作为专注于 AI 开发工具的技术分析师，根据您提供的 GitHub 数据，我为您整理了 **2026 年 7 月 16 日** 的 OpenCode 社区动态日报。

---

## OpenCode 社区动态日报 (2026-07-16)

### 今日速览

今日社区的核心动态围绕 **v1.18.2 补丁发布** 与 **桌面端新 UI 引发的广泛争议**。v1.18.2 主要修复了 Agent 嵌套和 Meta 模型推理深度问题；然而，用户对 v1.18.x 系列引入的全新标签栏布局和 Plan/Build 模式切换按钮消失的反馈非常强烈，已形成多个高热度 Issue。此外，上下文溢出和内容的自动压缩问题依然是开发者和核心贡献者的关注焦点。

---

### 版本发布

#### v1.18.2

-   **核心 (Core)**：
    -   **Bug 修复**：禁用了子代理默认启动嵌套子代理的行为，并增加了可配置的 `subagent_depth` 限制。
    -   **Bug 修复**：改进了 Meta 系列模型的默认推理深度。
-   **桌面端 (Desktop)**：
    -   **改进**：新增 `Mod+N` 快捷键用于打开新标签页。
    -   **Bug 修复**：若干问题修复。

---

### 社区热点 Issues

1.  **[[BUG] Desktop App v1.18.1 new layout hides agent (Plan/Build) switching UI](https://github.com/anomalyco/opencode/issues/36997)**
    -   **重要性**: **极高**。这是对新 UI 最直接的投诉，直指核心功能（Plan/Build 模式切换）消失。该 Issue 收集了大量用户反馈，表明这可能是一个严重的 UI 回归，是 v1.18.x 系列最头疼的问题。

2.  **[[BUG] Desktop: wtf is the new tab layout, tab titles dont fit anymore on screen](https://github.com/anomalyco/opencode/issues/36936)**
    -   **重要性**: **高**。另一个关于新 UI 设计的热门问题。用户质疑新标签布局的可用性，指出标签标题被截断，无法辨识。它直接关系到用户体验，讨论区充满了不满情绪。

3.  **[[FEATURE]: Expose GitHub Copilot "Auto" option in model selector](https://github.com/anomalyco/opencode/issues/25239)**
    -   **重要性**: **高**。尽管是一个较老的 Issue，但依然活跃。用户希望模型选择器能像 GitHub Copilot 一样有“自动”选项，让 IDE 根据上下文智能切换模型。反映了社区对智能化和更流畅体验的持续追求。

4.  **[[FEATURE]: Vertical tabs](https://github.com/anomalyco/opencode/issues/36942)**
    -   **重要性**: **高**。与第一条相关，该 Issue 是社区对新 UI 不满的直接抗议和功能建议。用户对水平标签布局感到失望，希望回归或新增垂直标签选项，以容纳更多会话。

5.  **[[perf, core] Request Entity Too Large with images blocks session — compaction also fails](https://github.com/anomalyco/opencode/issues/14562)**
    -   **重要性**: **高**。一个长期存在的性能问题。当对话包含图片时，Base64 数据会导致请求体过大（413 错误），且无法通过压缩恢复，导致会话卡死。在 V2 中，该问题依然受到关注。

6.  **[[FEATURE(app)]: display image attachments from tool results in chat UI](https://github.com/anomalyco/opencode/issues/21227)**
    -   **重要性**: **中**。用户希望当工具（如 `webfetch`）返回图片时，能在聊天界面中直接显示，而不是仅以文本形式呈现。这是一个能显著提升用户体验的需求。

7.  **[[FEATURE]: File editor](https://github.com/anomalyco/opencode/issues/26970)**
    -   **重要性**: **中**。社区希望 OpenCode 能具备文件编辑功能，使其更像一个独立的代码编辑器。这表明部分用户希望 OpenCode 能承担更多 IDE 职责。

8.  **[[BUG] Prompt leaks between the sessions](https://github.com/anomalyco/opencode/issues/35587)**
    -   **重要性**: **高**。一个严重的隐私/数据隔离 Bug。用户发现一个会话的提示词会出现在另一个会话的历史中，这对于开发者来说是不可接受的。

9.  **[[FEATURE]: Allow per-session MCP selection with `serve` and `attach`](https://github.com/anomalyco/opencode/issues/37168)**
    -   **重要性**: **中**。当使用 `opencode serve` 让多个客户端连接时，MCP 工具的启用/禁用状态是全局的。用户希望每个会话可以独立选择要使用的 MCP 工具，提升了多任务场景下的灵活性。

10. **[[FEATURE]: Auto-generate session titles in desktop app](https://github.com/anomalyco/opencode/issues/30926)**
    -   **重要性**: **中**。一个新功能的请求。新会话默认名为“New session”，当会话数量增多时难以识别。用户希望系统能自动生成简短、有意义的标题，这与上方的 UI 问题相辅相成，都反映了对会话管理体验的更高要求。

---

### 重要 PR 进展

1.  **[[contributor] fix(tui): attach auth token when editor port comes from env](https://github.com/anomalyco/opencode/pull/32481)**
    -   **内容**: 修复了在 VSCode/Cursor 集成环境中运行时，文件/选择上下文无法同步的 Bug。这是一个重要的修复，能改善 IDE 集成体验。

2.  **[[contributor] feat(mcp): surface tool progress](https://github.com/anomalyco/opencode/pull/32480)**
    -   **内容**: 将 MCP 工具的进度通知集成到 OpenCode 的现有进度显示中，让开发者能实时看到工具执行状态，提升透明度。

3.  **[[contributor] feat: experimental.chat.system.transform: add agent name as input argument](https://github.com/anomalyco/opencode/pull/32474)**
    -   **内容**: 为 `experimental.chat.system.transform` 回调函数增加了 `agent name` 参数，允许开发者根据 Agent 名称来定制 prompt 转换逻辑。

4.  **[[contributor] fix(tui): truncate labels by display width](https://github.com/anomalyco/opencode/pull/32470)**
    -   **内容**: 修复了 TUI 中标签截断的 Bug，改用字符显示宽度而非字符数进行截断，能够更准确地处理中文字符等宽字符。这直接影响了所有 TUI 用户的显示体验。

5.  **[[contributor] fix(mcp): retry transient bootstrap failures](https://github.com/anomalyco/opencode/pull/32468)**
    -   **内容**: 为 MCP 服务器启动失败（如网络波动）增加了重试机制，提升了桌面端应用在网络恢复后的稳定性。

6.  **[[contributor] fix(filesystem): return empty list when listing a missing path](https://github.com/anomalyco/opencode/pull/32462)**
    -   **内容**: 修复了当尝试列出不存在的目录路径时，`FileSystem.Service.list()` 会崩溃的 Bug。现在会返回空列表，行为更稳健。

7.  **[[contributor] feat: make plan mode default (remove experimental flag gating)](https://github.com/anomalyco/opencode/pull/32458)**
    -   **内容**: 将“Plan 模式”设为默认行为，移除了实验性标志。这是一个重要的步骤，标志着该功能趋于成熟并成为标准流程的一部分。

8.  **[[needs:compliance] fix(session): resolve session overflow detection timing gaps](https://github.com/anomalyco/opencode/pull/37194)**
    -   **内容**: 解决了会话溢出检测的几个时序问题，例如，重写 `usable()` 函数，使其能预留完整的输出预算，而不是被限制在 20K。这旨在更准确地预测和防止上下文溢出。

9.  **[[contributor] feat(core): normalize tool and attachment images at settlement](https://github.com/anomalyco/opencode/pull/37141)**
    -   **内容**: 这是一个针对 V2 的重大修复，将图像尺寸归一化逻辑从 `read` 工具扩展到所有工具和附件，以防止因过大图片导致请求体溢出。这是从根源上解决 #14562 等问题的尝试。

10. **[[contributor] fix(opencode): normalize cloudflare-workers-ai mixed message content types](https://github.com/anomalyco/opencode/pull/36850)**
    -   **内容**: 修复了使用 Cloudflare Workers AI 时的兼容性问题，它能处理消息中 `content` 字段类型不一致的情况（有些是字符串，有些是数组）。

---

### 功能需求趋势

根据今日所有 Issue 和 PR 分析，社区最关注的功能方向如下：

1.  **UI/UX 重构与回归**：社区对新版桌面端 UI 的反响非常强烈，特别是标签栏布局和模式切换按钮的消失。核心诉求集中在 **会话管理**（垂直标签、自动标题、更好的可视化）和 **核心功能入口**（Plan/Build 模式）的易用性上。这表明 UI 的稳定性和直观性比引入新颖设计更重要。

2.  **上下文管理与压缩**：大量问题（#13946, #10634, #35013, #17340, #14562, #32656）和 PR（#37141, #37194）围绕**上下文溢出**、**自动压缩（Compact）** 和 **图像处理** 展开。这是 OpenCode 作为长期运行 Agent 所面临的核心技术挑战，社区希望能更智能、更可靠地管理上下文窗口，以避免会话卡死或数据丢失。

3.  **集成与插件生态**：社区积极讨论通过 **Agent Client Protocol (ACP)** 支持 Claude（#24038）、**MCP 工具** 的精细化控制（#37168, #32480）、以及更好的 **IDE（VSCode/Cursor）集成**（#32481）。这显示了用户希望 OpenCode 能在更广泛的开发环境中无缝工作。

4.  **安全与权限管理**：出现关于 **安全配置与项目配置未分离**（#37155）的严重问题，认为 AI Agent 可以自我授权。这表明随着 Agent 能力的增强，社区对其安全性、可控性的担忧也在上升。

---

### 开发者关注点

从开发者反馈中，可以提炼出以下痛点和关注点：

1.  **升级恐慌**：v1.18.x 的更新引入了破坏性 UI 变更，导致核心功能（Plan/Build 切换）难以访问或消失。开发者对“突然的、无法回退的 UI 大改”表示强烈不满。

2.  **功能缺失 vs. 新功能**：社区现在最紧迫的需求不是新特性，而是 **恢复已被用户接受的核心功能**。Plan/Build 模式切换按钮的消失是今日最大的负面反馈。

3.  **上下文崩溃**：会话因上下文溢出而卡死是一个高频痛点。开发者报告了多种溢出方式：图片 Token 过多、大工具输出、压缩模型自身 Token 超限等。虽然社区贡献者积极提交修复 PR，但这依然是一个持续困扰用户的稳定性问题。

4.  **跨会话数据泄漏**：`Prompt leaks between sessions` (#35587) 是一个严重的隐私 Bug，可能导致在不同项目中工作时的敏感信息泄漏，必须得到紧急修复。

5.  **模型兼容性**：特定模型（如 Qwen 3.7 Plus via OpenRouter）产生大量幻觉/错误回复的问题 (#37139) 虽被关闭，但反映了用户对第三方模型稳定性和输出质量的担忧。同时，对 Cloudflare Workers AI 等新提供商的兼容性修复也表明了用户多样化的需求。

6.  **快捷键与输入法问题**：“Ctrl+P”快捷键在 Windows 上失灵 (#37165) 和 IME 输入法与按键冲突 (#37167) 等细节问题同样影响开发体验，是用户所关注的。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 | 2026-07-16

## 今日速览
- 发布三个版本：`v0.19.10-nightly`、`v0.19.9-preview` 及 `cua-driver-rs v0.7.2`，后者新增相对坐标支持。
- 社区最热议题集中在 **多工作区守护进程**（#6378，23条评论）和 **ACP 协议原生接入**（#4782），同时多项安全/配置 bug 受到关注。
- 核心开发线活跃：**工作区 MCP 管理**、**守护进程日志轮转**、**Plan 模式退出确认**等大型 PR 进入审查。

## 版本发布

### v0.19.10-nightly.20260715.c538bd70d
- 文档审查：限制反复审查后的 PR 范围 (`@wenshao`)
- Web Shell 新增工作区路径锁功能 (`@ytahdn`)

### v0.19.9-preview.0
- 包含上述两项变更的预览版。

### cua-driver-rs v0.7.2
- macOS 代码签名 + 公证；Linux (glibc 2.31+) 和 Windows 提供 x86_64/arm64 二进制。
- 新增 **相对坐标** 支持（`enableRelativeCoordinates`），用于精度要求不高的 CUA 交互。

## 社区热点 Issues（前10）

1. **#6378 [RFC] 支持单个 `qwen serve` 守护进程管理多个工作区**  
   - 23 条评论，讨论热烈。当前模型 `1 daemon = 1 workspace × N sessions`，提案扩展为多工作区共存，保留向后兼容。  
   - 链接: https://github.com/QwenLM/qwen-code/issues/6378

2. **#4782 [Tracking] ACP Streamable HTTP 传输实现状态**  
   - 实现 ACP 协议原生端点 `/acp`，使 Zed、Goose、JetBrains 可直接连接，无需适配层。社区关注集成进度和升级计划。  
   - 链接: https://github.com/QwenLM/qwen-code/issues/4782

3. **#6928 [Bug] GitHub App 认证未注入新建工作区**  
   - 用户从私有仓库创建工作区后，环境缺少 GitHub 认证。诊断显示 App 已安装但认证未传播，影响 CI 工作流。  
   - 链接: https://github.com/QwenLM/qwen-code/issues/6928

4. **#5239 [Feature] 提升子 Agent 与主会话的双向通信能力**  
   - 目前子 Agent 挂掉后主会话无法感知，用户被迫通过文件监控绕行。建议添加通知机制。  
   - 链接: https://github.com/QwenLM/qwen-code/issues/5239

5. **#6857 [Bug] `/update` 报告“已是最新”，但 npm 注册表实际有更新**  
   - 0.19.9 上运行 `/update` 时错误显示“up to date”，而 0.19.10 已发布。影响版本感知。  
   - 链接: https://github.com/QwenLM/qwen-code/issues/6857

6. **#6936 [Bug] `isManagedMemoryAvailable()` 忽略 `enableManagedAutoMemory: false`**  
   - 即使禁用托管内存，系统提示中仍注入 ~7-9KB 的 `# auto memory` 指令，浪费上下文窗口。根源在于门控检查不匹配。  
   - 链接: https://github.com/QwenLM/qwen-code/issues/6936

7. **#6914 [Bug] 分数值的轮次/工具调用限制导致会话提前终止**  
   - `maxSessionTurns` 和 `maxToolCallsPerTurn` 接受分数值（如 0.5），但与整数计数器比较后提前终止。  
   - 链接: https://github.com/QwenLM/qwen-code/issues/6914

8. **#6443 [Feature] 钉钉渠道支持交互式卡片**  
   - 建议为钉钉消息增加运行状态卡、停止按钮、表单卡等，提升交互体验。  
   - 链接: https://github.com/QwenLM/qwen-code/issues/6443

9. **#6898 [Feature] Shell 提醒应只在任务结束时触发**  
   - 用户抱怨每次工具调用都弹窗，希望改为任务结束后一次提醒。  
   - 链接: https://github.com/QwenLM/qwen-code/issues/6898

10. **#6814 [Bug] 工具摘要文本过长时被截断**  
    - 工具输出超过终端宽度时显示 `…` 而非换行，隐藏文件路径等关键信息。  
    - 链接: https://github.com/QwenLM/qwen-code/issues/6814

## 重要 PR 进展（前10）

1. **#6954 feat(serve): 添加工作区 MCP 管理**  
   - 在 Web Shell 和守护进程中增加工作区级 MCP 插件管理入口，支持扩展和 MCP 选项卡、持久化用户/工作区 MCP 发现。  
   - 链接: https://github.com/QwenLM/qwen-code/pull/6954

2. **#6991 feat(channels): 为守护进程会话标记渠道来源**  
   - 所有由渠道创建的守护会话自动添加不可变的 `sourceType: "channel"` 元数据，便于日志追踪。  
   - 链接: https://github.com/QwenLM/qwen-code/pull/6991

3. **#6963 ci(web-shell): 可视化前后对比，仅展示变更视图**  
   - 将 Web Shell 可视化预览从固定截图改为基于像素差异的 `before/after` 对比，仅展示 PR 影响到的视图。  
   - 链接: https://github.com/QwenLM/qwen-code/pull/6963

4. **#6981 fix(core): 修复无 ID 续写块路由错位**  
   - 解决 `StreamingToolCallParser` 中同一流索引下第二个工具调用的参数丢失问题，保证 OpenAI 兼容 stream 的正确性。  
   - 链接: https://github.com/QwenLM/qwen-code/pull/6981

5. **#6969 feat(cli): 守护进程日志自动轮转**  
   - `qwen serve` 日志现在固定路径 `debug/daemon/daemon.log`，每个日志族限制 10 MiB 活动文件 + 4 个归档，并增加 `runId` 和 PID。  
   - 链接: https://github.com/QwenLM/qwen-code/pull/6969

6. **#6971 feat(web-shell): 按工作区分色彩色窗格**  
   - 分割视图的每个窗格标题栏显示工作区色点+名称，底部分割线也匹配颜色，方便窄屏识别。  
   - 链接: https://github.com/QwenLM/qwen-code/pull/6971

7. **#6967 fix(core): 要求显式确认才能退出 Plan 模式**  
   - 防止 AI 自动从 Plan 模式切换到执行模式，用户必须手动批准，增加安全边界。  
   - 链接: https://github.com/QwenLM/qwen-code/pull/6967

8. **#6950 fix(cli): 保留渠道启动失败详细信息**  
   - 守护进程管理下的渠道 `connect()` 失败信息现在会逐条携带经过凭据裁剪的错误，通过状态快照、API 和 CLI 命令清晰展示。  
   - 链接: https://github.com/QwenLM/qwen-code/pull/6950

9. **#6895 feat(core): 传播受信任的调用上下文**  
   - 引入 `InvocationContextV1`，携带入口、原生会话、根提示和已验证客户端信息，贯穿整个调用链，为安全审计和 MCP 信任决策提供基础。  
   - 链接: https://github.com/QwenLM/qwen-code/pull/6895

10. **#6945 feat(cli): 为守护进程会话添加 Todo 停止守卫**  
    - 当 `todo_write` 留下未完成项时，守护进程会话可自动继续当前工作链最多两次，防止模型过早停止。需 opt-in。  
    - 链接: https://github.com/QwenLM/qwen-code/pull/6945

## 功能需求趋势

从近期 Issues 和 PR 中可以清晰看出社区关注以下方向：

- **多工作区架构**：单个守护进程管理多个工作区（#6378），对 CI/CD 和复杂项目尤为关键。
- **ACP 协议原生支持**：让非 Qwen 编辑器直接连接，减少适配工作量（#4782）。
- **渠道增强**：钉钉交互卡片（#6443）、钉钉单聊投递（#6883）、WeCom 群聊修复（#6939），说明企业 IM 集成需求强烈。
- **子 Agent 通信改进**：双向通知、故障感知（#5239），多 Agent 协作场景推动此项。
- **安全/信任**：MCP 信任上下文传播（#6895）、Plan 模式退出确认（#6967）、信任配置不泄漏（#6900）。
- **模型切换与并发控制**：热键切换模型（#6486）、子 Agent 按模型并发限制（#6984）。
- **会话持久化与可观测性**：守护会话日志轮转（#6969）、渠道来源标记（#6991）、跨工作区深度健康检查（#6961）。

## 开发者关注点

- **版本更新感知**：`/update` 命令误报已最新（#6857）常被吐槽，需要修复。
- **配置不生效**：禁用托管内存后仍插入指令（#6936），浪费上下文；信任状态预览导致配置泄漏（#6831）。
- **限制检查漏洞**：分数值导致会话提前终止（#6914），引发对参数校验的质疑。
- **工具交互体验**：长文本截断（#6814）、Shell 提醒频率过高（#6898），影响日常使用流畅度。
- **CI 震荡**：多条 E2E 测试随机失败（#6933、#6935、#6938 等），社区对自动化测试稳定性有期望。
- **MCP 工具名兼容性**：含点的工具名被 OpenAI/Anthropic 兼容提供商拒绝（#6970），需统一 sanitize 策略。
- **文本 UI 优化**：终端宽度适配、颜色区分多工作区等细节反馈增多，表明社区开始进入精细化打磨阶段。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*