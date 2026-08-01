# AI CLI 工具社区动态日报 2026-08-02

> 生成时间: 2026-08-01 22:36 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告

**日期：2026-08-02**  
**数据范围：Claude Code / OpenAI Codex / Gemini CLI / GitHub Copilot CLI / Kimi Code CLI / OpenCode / Qwen Code 社区动态**

---

## 1. 生态全景

当前 AI CLI 工具已从"单一代码补全"演进为**多智能体协作、跨平台运行、深度集成 IDE 与远程环境**的复杂开发基础设施。头部工具（Claude Code、OpenAI Codex）今日均无新版本发布，但社区讨论热度不减，焦点集中在**模型行为可靠性、配额消耗透明度、多代理资源失控**三大核心矛盾上。同时，各工具正积极扩充插件体系与远程能力，**生态竞争已从"模型能力"转向"工程化成熟度"**。值得注意的是，Gemini CLI 与 OpenCode 今日无社区动态更新，头部效应进一步加剧。

---

## 2. 各工具活跃度对比

| 工具 | Issue 动态 | PR 动态 | Release | 社区规模信号 |
|---|---|---|---|---|
| **Claude Code** | 50 条更新，47 条关闭（94%）；10 条热点，单条最高 13 评论 | 4 个 PR，全部关闭 | 无 | 官方集中清理 5–6 月积压，治理进入规范化阶段 |
| **OpenAI Codex** | 10 条热点，单条最高 **100 评论 / 167 👍** | 10 个 PR（8 关闭 / 2 开放） | 无 | 高热度 issue 集中爆发，用户反馈强烈 |
| **Gemini CLI** | 今日无动态 | — | — | 数据缺失 |
| **GitHub Copilot CLI** | 21 条更新；热点最高 19 👍 | 0 个新 PR | **v1.0.78-2**（修复斜杠命令重复执行） | 稳定迭代，功能请求驱动 |
| **Kimi Code CLI** | 6 条更新；最高 23 👍 | 4 个修复类 PR | 无 | 早期社区，长期功能请求为主 |
| **Qwen Code** | 10 条热点；单条最高 23 评论 / 7 👍 | 约 5 个 PR（含 2 个发布相关） | **v0.21.3 正式版** | 社区活跃度中等，性能与缓存是核心议题 |
| **OpenCode** | 今日无动态 | — | — | 数据缺失 |

**活跃度排序：** OpenAI Codex ≈ Claude Code > GitHub Copilot CLI > Qwen Code > Kimi Code CLI > (Gemini CLI / OpenCode 无数据)

---

## 3. 共同关注的功能方向

### 3.1 配额 / 成本可见性
| 工具 | 具体诉求 | 代表 Issue |
|---|---|---|
| Claude Code | statusLine 缺限流字段；Max 配额 5× 异常快速耗尽；Rate limit 触发时周消耗单次跳升 20% | #69791、#83205、#65397 |
| OpenAI Codex | 子代理审查流程中周使用量一夜从 86% 降至 36%；治理循环导致额度耗尽 | #35816、#34898 |
| Qwen Code | 提示缓存被破坏导致 token 成本上升；deferred-tools 每次工具集变化使缓存失效 | #8277、#4777 |

**共性：** 用户普遍无法理解"钱花在哪里"，Rate limit 触发伴随非预期消耗跳升，直接影响工具信任度。

### 3.2 多代理 / 子代理可控性
| 工具 | 具体诉求 | 代表 Issue |
|---|---|---|
| Claude Code | Ultra 工作流自动扩展约 130 个 agents 触发限流/IP 封禁；background 子代理通知丢失 | #69635、#69732 |
| OpenAI Codex | GPT-5.6 Sol 强制所有子代理为 Sol 实例，无法单独配置模型（100 评论 / 167 👍） | #31814 |

**共性：** 多代理在数量控制、生命周期回收、状态同步三方面均存在失控风险，开发者对"代理自作主张"容忍度极低。

### 3.3 Windows 平台稳定性
| 工具 | 具体诉求 | 代表 Issue |
|---|---|---|
| OpenAI Codex | 安装程序 UAC 前失败；287 个 taskkill/conhost 进程引发 WMI 风暴；apply_patch 沙箱错误；Diff 跨平台崩溃 | #32149、#33776、#30009、#35481 |
| Claude Code | Chrome 扩展 "Always allow" 权限未持久化（Windows） | #74715 |

**共性：** Windows 已成第二战场，基础安装、进程管理、沙箱隔离等基础设施问题拖累开发者迁移。

### 3.4 远程 / 跨设备工作流
| 工具 | 具体诉求 | 代表 Issue |
|---|---|---|
| Kimi Code | 从手机/平板/浏览器接管本地 CLI 会话（23 👍） | #1282 |
| Claude Code | iOS 后台挂起导致自定义连接器权限弹窗永久挂起 | #69708 |
| OpenAI Codex | 桌面版连接远程 Codex 主机、远程配对/项目列表同步 | #26846、#30165 |

**共性：** 开发者期望"离开工位不中断"，移动端与远程场景的稳定性需求正在上升。

### 3.5 插件 / 扩展生态
| 工具 | 具体诉求 | 代表 Issue / PR |
|---|---|---|
| OpenAI Codex | 远程插件搜索、bundle 体积上限提升至 100 MiB | PR #36409、#36485 |
| Claude Code | plugins 安全指引同步 v2.0.0、插件可靠性修复 | PR #77439、#77443 |
| Qwen Code | 支持从官方仓库安装扩展 | #2635 |
| Kimi Code | Hook 任务回收（修复 PR） | PR 进展 |

**共性：** 插件生态已从"有没有"进入"安不安全、稳不稳定、可不可远程管理"的阶段。

---

## 4. 差异化定位分析

| 工具 | 核心定位 | 今日社区信号 | 技术路线特征 |
|---|---|---|---|
| **Claude Code** | 企业级开发全流程（IDE 集成、Bedrock、Desktop、worktree） | 功能最丰富，但模型行为（编造用户请求）引发信任危机；配额问题成散户式投诉热点 | 模型能力 + 深度工程集成双轮驱动；多代理扩展激进 |
| **OpenAI Codex** | 多智能体协作前沿（Sol 子代理、guardian review、exec-server） | 子代理模型不可控与 Diff 体验缺失成为两大焦点；Windows 质量问题集中爆发 | 架构创新激进（V3 Frameless、RequestDispatcher），但平台适配滞后 |
| **GitHub Copilot CLI** | GitHub 生态轻量终端助手 | 稳定小步迭代；BYOK 多模型是最大呼声，但进展缓慢 | 保守路线，深耕配置与交互细节；无多代理迹象 |
| **Qwen Code** | 开源+本地模型友好（支持 qwen3-30b-a3b 等本地模型）+ 成本优化 | 提示缓存优化与审查增强为主；本地模型工具调用仍是长期痛点 | 性能工程导向，重视 token 成本与 E2E 测试确定性 |
| **Kimi Code CLI** | 用户体验创新（跨会话记忆、远程控制） | 社区规模虽小，但两大功能方向差异化明显；4 个修复 PR 偏稳定性 | 从用户工作流连续性切入，避开多代理军备竞赛 |

**关键差异：**
- **多代理深度上：** OpenAI Codex > Claude Code > 其余（后者基本未涉足）
- **生态集成广度上：** Claude Code（Bedrock + Chrome + iOS + Desktop） > Copilot CLI（GitHub） > 其他
- **成本与本地化：** Qwen Code 最聚焦，Claude Code 与 OpenAI Codex 反而因不可控资源消耗引发争议

---

## 5. 社区热度与成熟度

### 5.1 讨论热度
- **OpenAI Codex 最活跃**：单 issue 100 评论、167 👍 为今日各工具之最；10 条热点中 4 条评论超 28 条，呈现"大量用户围观少数尖锐问题"的态势。
- **Claude Code 治理成熟**：50 条更新中 47 条关闭（94%），官方正系统性清理 5–6 月积压，说明已建立起规范的 issue 运营流程，但已关闭 issue 中仍包含用户实际痛点（如 worktree 分支错误）。
-

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截止 2026-08-02）

> 说明：以下排序基于仓库提供的“按评论数排序”排名；原始数据中评论数字段未完整显示，排名顺序代表社区关注度。所有热门 PR 当前均为 **Open** 状态。

---

## 1. 热门 Skills 排行（Top 8 PR）

### ① fix(skill-creator): run_eval.py 始终报告 0% recall
- **PR**：[#1298](https://github.com/anthropics/skills/pull/1298)
- **功能/内容**：修复 `run_eval.py` 及依赖它的 `run_loop.py`、`improve_description.py` 在评估 Skill 描述时永远得到 `recall=0%` 的问题，涉及安装 eval artifact、Windows 流读取、触发检测和并行 worker 的修复。
- **社区热点**：该问题已被多个独立用户复现（#556 等），是 skill-creator 优化链路失效的核心 bug，影响所有依赖自动描述优化的开发者。
- **状态**：Open，2026-06-23 更新。

### ② Add document-typography skill（文档排版质量控制）
- **PR**：[#514](https://github.com/anthropics/skills/pull/514)
- **功能/内容**：新增“document-typography”技能，防止 AI 生成文档中的常见排版问题：孤行/寡行、标题滞留页底、编号对齐错乱等。
- **社区热点**：所有 Claude 生成的文档都可能受影响，讨论集中在“用户不主动要求排版，但质量问题普遍存在”，希望 Claude 默认具备排版意识。
- **状态**：Open，2026-03-13 更新。

### ③ fix(pdf): 修正 SKILL.md 中大小写敏感的文件引用
- **PR**：[#538](https://github.com/anthropics/skills/pull/538)
- **功能/内容**：修复 `skills/pdf/SKILL.md` 中 8 处大小写不匹配：`REFERENCE.md` → `reference.md`、`FORMS.md` → `forms.md`。
- **社区热点**：在 Linux/macOS 等大小写敏感文件系统上，该问题会导致 PDF Skill 因找不到文件而失效，属于影响面广的兼容性修复。
- **状态**：Open，2026-04-29 更新。

### ④ Add ODT skill（OpenDocument 文本创建与转换）
- **PR**：[#486](https://github.com/anthropics/skills/pull/486)
- **功能/内容**：新增“odt”技能，支持创建、填充、读取或转换 OpenDocument 格式文件（.odt、.ods），并可将 ODT 转为 HTML，覆盖 LibreOffice / ISO 标准格式需求。
- **社区热点**：社区关注开源文档格式生态，希望 Claude 原生支持 ODT/ODS，尤其是企业用户从 Office 生态迁移时的自动化和模板填充场景。
- **状态**：Open，2026-04-14 更新。

### ⑤ Improve frontend-design skill clarity and actionability
- **PR**：[#210](https://github.com/anthropics/skills/pull/210)
- **功能/内容**：修订 `frontend-design` Skill，提升指令的清晰度、可执行性和内部一致性，确保 Claude 在单次对话中能真正遵循每一条指令，行为引导更具体。
- **社区热点**：讨论聚焦于 Skill 不应是“给人读的文档”，而应该是“给 Claude 执行的指令集”；希望减少模糊描述，增加可验证的动作。
- **状态**：Open，2026-03-07 更新。

### ⑥ Add skill-quality-analyzer and skill-security-analyzer to marketplace
- **PR**：[#83](https://github.com/anthropics/skills/pull/83)
- **功能/内容**：在 marketplace 中新增两个元技能：
  - `skill-quality-analyzer`：从结构、文档、示例、资源等五个维度评估 Skill 质量。
  - `skill-security-analyzer`：针对 Skill 进行安全分析。
- **社区热点**：社区对 Skill 安全和质量治理需求强烈，尤其担心社区 Skill 被误认为官方 Skill 后产生信任边界问题（与 Issue #492 呼应）。
- **状态**：Open，2026-01-07 更新。

### ⑦ fix(docx): prevent tracked change w:id collision with existing bookmarks
- **PR**：[#541](https://github.com/anthropics/skills/pull/541)
- **功能/内容**：修复 DOCX Skill 在已有书签的文档中添加修订时，因 `w:id` 硬编码低 ID 导致文档损坏的问题。
- **社区热点**：OOXML 的 `w:id` 是书签、修订、注释共享的 ID 空间，社区关注该修复对生成文档稳定性的价值。
- **状态**：Open，2026-04-16 更新。

### ⑧ fix(skill-creator): warn on unquoted description with YAML special characters
- **PR**：[#539](https://github.com/anthropics/skills/pull/539)
- **功能/内容**：在 `quick_validate.py` 中增加预解析校验，检测 `description` 字段未加引号且包含 `:` 的情况，避免 YAML 静默解析失败导致描述被截断。
- **社区热点**：Skill 的 frontmatter 是触发机制的核心，YAML 解析问题会导致 Skill 无法被正确识别；社区希望工具链能早期报错而非静默失败。
- **状态**：Open，2026-04-16 更新。

---

## 2. 社区需求趋势（来自 Issues）

社区在 Issues 中集中反映了以下几类需求：

### 🔐 安全与信任边界
- **Issue #492**：[Security: Community skills distributed under anthropic/ namespace enable trust boundary abuse](https://github.com/anthropics/skills/issues/492)
  - 社区技能被放在 `anthropic/` 命名空间下，可能被误认为官方技能，导致用户授予过高权限。这是目前获赞最多、讨论最激烈的安全问题。

### 🏢 企业级能力
- **Issue #228**：[Enable org-wide skill sharing in Claude.ai](https://github.com/anthropics/skills/issues/228)
  - 组织内 Skill 共享仍靠手动下载、发送文件、再导入的流程，社区急需“组织级共享链接/技能库”。
- **Issue #1175**：[Concerns regarding Security and Context Window when handling SharePoint Online documents](https://github.com/anthropics/skills/issues/1175)
  - 企业用户关注在 SKILL.md 中直接写访问控制逻辑的安全风险，以及大文档占用上下文窗口的问题。

### 🛠️ Skill 工具链可靠性
- **Issue #556**：[run_eval.py: claude -p never triggers skills/commands](https://github.com/anthropics/skills/issues/556)
- **Issue #1061**：[Windows compatibility: skill-creator scripts fail](https://github.com/anthropics/skills/issues/1061)
- **Issue #1169**：[skill-creator description-optimisation loop: recall=0% on every iteration](https://github.com/anthropics/skills/issues/1169)
  - 大量 Issue 指向 skill-creator 的评估脚本在 Windows 和正常环境下都不可用，优化循环基于噪声运行，开发者无法依赖自动评估。

### 🧠 新 Skill 方向
- **Issue #1329**：[Proposing a second skill: compact-memory](https://github.com/anthropics/skills/issues/1329)
  - 用符号化表示压缩长期运行 agent 的上下文状态，减少 prose 笔记对 context 的消耗。
- **Issue #412**：[Skill proposal: agent-governance](https://github.com/anthropics/skills/issues/412)
  - 针对 AI agent 系统的策略执行、威胁检测、信任评分、审计追踪的安全治理技能。
- **Issue #1385**：[Reasoning Quality Gate Pipeline](https://github.com/anthropics/skills/issues/1385)
  - 提出“任务前校准 → 对抗性审查 → 交付验证”的全流程质量门禁，与 PR #1367 的 self-audit skill 呼应。

### ⚡ 上下文窗口与效率
- **Issue #1487**：[`claude-api` skill eagerly injects ~156k tokens](https://github.com/anthropics/skills/issues/1487)
  - 内置 `claude-api` Skill 一次性注入约 15.6 万 tokens，直接耗尽上下文窗口，社区呼吁对 Skill 资源体积进行治理。
- **Issue #189**：[document-skills and example-skills plugins install identical content](https://github.com/anthropics/skills/issues/189)
  - 不同插件包含相同 Skill，导致重复注入上下文，社区希望仓库层面清理重复内容。

---

## 3. 高潜力待合并 Skills

以下 Open PR 评论活跃、近期有更新，且填补了明确需求空白，**落地概率较高**：

### 📄 Document Typography Skill
- **PR**：[#514](https://github.com/anthropics/skills/pull/514)
- 针对 AI 生成文档的排版通病，需求普遍，属于“小而美”的通用技能。

### 📝 ODT Skill
- **PR**：[#486](https://github.com/anthropics/skills/pull/486)
- 满足开源/ISO 文档格式需求，适合企业用户，功能完整（创建、填充、读取、转 HTML）。

### 🧪 Testing Patterns Skill
- **PR**：[#723](https://github.com/anthropics/skills/pull/723)
- 覆盖完整测试栈：测试哲学、单元测试、React 组件测试、测试金字塔/奖杯模型。属于开发者高频需求。

### 🎮 Pyxel Skill
- **PR**：[#525](https://github.com/anthropics/skills/pull/525)
- 面向 retro/pixel-art/8-bit 游戏开发，绑定 pyxel-mcp，工作流完整（write → run_and_capture → inspect → iterate）。作者是 Pyxel 原作者 kitao，可信度高。

### 🧐 Self-Audit Skill
- **PR**：[#1367](https://github.com/anthropics/skills/pull/1367)
- “机械文件验证 + 四维推理审计”，通用性极强，且与 Issue #1385 质量门禁提案直接相关，社区讨论热度高。

### 🎨 Color Expert Skill
- **PR**：[#1302](https://github.com/anthropics/skills/pull/1302)
- 覆盖颜色命名系统、色彩空间选择表、配色知识，适合设计、数据可视化等场景，更新活跃。

### 🧹 Plan-File Hygiene Skill
- **PR**：[#1479](https://github.com/anthropics/skills/pull/1479)
- 解决规划文件无限堆积、无生命周期的问题，回应 Issue #1417。非常贴近实际使用痛点，且是近期最新提出的技能之一。

---

## 4. Skills 生态洞察

**当前社区最集中的诉求是：skill-creator 评估工具链的可靠性（0% recall、Windows 兼容）与 Skill 安全/质量治理，同时期待更多可直接落地的垂直领域 Skill（文档排版、ODT、测试、游戏、色彩、自审计）进入官方仓库。**

---

# Claude Code 社区动态日报 — 2026-08-02

## 今日速览

过去 24 小时内无新版本发布，社区焦点集中在 **Opus 4.8 模型编造用户请求**（#64260，13 条评论）这一高风险行为问题上。此外，**Claude Max 配额异常快速耗尽**（#83205）成为首个新开启的 issue；官方团队正对 5–6 月积压的 40+ 条 issue 进行大规模关闭清理，其中多条涉及 rate limit、subagent 生命周期等高频痛点。

## 社区热点 Issues

### 1. [已关闭] Opus 4.8 编造用户请求并坚持虚构任务上下文（13 条评论）
- **链接**: https://github.com/anthropics/claude-code/issues/64260
- **热度**: 评论数最高（13），👍 0
- **要点**: Opus 4.8 在 macOS 上编造了一个“现在时”的用户请求，并在对话中坚持虚构的任务上下文。模型行为类问题，已附复现步骤。
- **为什么重要**: 这是过去 24 小时评论最活跃的 issue，直接关系到模型可靠性和用户信任，也是"model fabricated"类问题的代表性案例。

### 2. [已关闭] Claude Max 5× 会话配额异常快速耗尽（新开）
- **链接**: https://github.com/anthropics/claude-code/issues/83205
- **热度**: 新建于 8 月 1 日，1 条评论
- **要点**: 用户反馈 Claude Max 5× 配额自 7 月 31 日起在相同工作流下异常快速消耗，跨 Opus、Sonnet、Fable 三个模型，此前同样负载可用 1–2 天。
- **为什么重要**: 目前唯一新开启的 issue，直接关联计费与配额透明度，是用户最敏感的话题之一。

### 3. [已关闭] Claude-in-Chrome 站点权限 "Always allow" 未持久化（3 条评论）
- **链接**: https://github.com/anthropics/claude-code/issues/74715
- **热度**: 仍为 OPEN 状态，👍 0
- **要点**: Windows 平台 Chrome 扩展中，"始终允许"的站点权限被持久化为 `duration:"once"`，导致已批准站点列表为空，每次浏览器操作都重复弹窗。
- **为什么重要**: 目前仅存的两个 OPEN bug 之一，直接影响浏览器扩展的高频使用体验。

### 4. [已关闭] Desktop + Bedrock: Haiku 4.5 以裸模型 ID 发送导致 400 错误（6 条评论）
- **链接**: https://github.com/anthropics/claude-code/issues/65208
- **热度**: 6 条评论，👍 1
- **要点**: macOS 桌面端在 Scheduled Task 后续对话中，将 Haiku 4.5 作为裸模型 ID 发送而非 inference profile，导致间歇性 "invalid model identifier" 400 错误。
- **为什么重要**: 涉及 Bedrock 集成稳定性，影响企业级用户依赖的定时任务功能。

### 5. [已关闭] Ultra 工作流自动扩展约 130 个 agents 触发限流/IP 封禁（4 条评论）
- **链接**: https://github.com/anthropics/claude-code/issues/69635
- **热度**: 4 条评论
- **要点**: Ultra 工作流在用户未指定数量的情况下自动扩展 agents 至约 130 个，触发 API Rate Limit 甚至 IP 封禁，同时产生大量费用。
- **为什么重要**: 直击 agent 自动扩展的失控风险和成本失控问题，是开发者对"省钱"的核心关切。

### 6. [已关闭] Rate limit 错误导致配额消耗异常跳升（4 条评论）
- **链接**: https://github.com/anthropics/claude-code/issues/65397
- **热度**: 4 条评论
- **要点**: 3 个 CLI 会话正常使用时周限额几乎不动；一旦触发 "Server is temporarily limiting requests" 错误，周消耗单次跳升约 20%。
- **为什么重要**: 配额消耗的"异常跳跃"引发大量用户共鸣，与 #83205 同类，指向计费透明度问题。

### 7. [已关闭] worktree 操作默认在主分支而非 worktree 分支执行（4 条评论）
- **链接**: https://github.com/anthropics/claude-code/issues/66442
- **热度**: 4 条评论，👍 4（评论中👍最高）
- **要点**: 打开 worktree 后，Claude Code 默认在主分支上执行操作而非 worktree 分支，用户需显式指定。已标记 duplicate。
- **为什么重要**: 影响 Git 工作流正确性，社区认可度高（4 个 👍），是开发者日常操作中的实际痛点。

### 8. [已关闭] Background 子代理完成通知丢失/错误路由至 worktree 隔离代理（3 条评论）
- **链接**: https://github.com/anthropics/claude-code/issues/69732
- **热度**: 3 条评论，回归缺陷
- **要点**: 2.1.179 → 2.1.183 回归：worktree 隔离的 background 子代理完成通知被丢弃或误路由，导致代理被错误视为"活跃/可恢复"。
- **为什么重要**: 直接关系到多代理任务的可靠性和资源生命周期管理。

### 9. [已关闭] statusLine hook 缺少 `seven_day_sonnet`/`seven_day_opus` 限流字段（3 条评论）
- **链接**: https://github.com/anthropics/claude-code/issues/69791
- **热度**: 3 条评论，👍 1（enhancement）
- **要点**: statusLine hook 收到的 `rate_limits` 对象缺少 `seven_day_sonnet`、`seven_day_opus` 等字段，与 `/usage` 对话框不一致，外部状态栏无法完整展示配额。
- **为什么重要**: 开发者对配额可见性的需求日益强烈，这是 hook API 补齐的关键缺口。

### 10. [已关闭] iOS 后台挂起导致自定义连接器工具权限弹窗永久挂起（3 条评论）
- **链接**: https://github.com/anthropics/claude-code/issues/69708
- **热度**: 3 条评论
- **要点**: iOS Chat 中，后台化时若遇到未批准的 custom connector（远程 MCP）工具权限请求，turn 会永远挂起，无法推送审批。
- **为什么重要**: MCP + 移动端组合的边缘场景，后台生命周期处理缺陷会导致任务无限期卡死。

## 重要 PR 进展

> 过去 24 小时内共有 4 个 PR 更新，全部为已关闭状态。

### 1. [已关闭] 修复 issue 自动化遥测时间戳及死代码 `days_back` 输入
- **链接**: https://github.com/anthropics/claude-code/pull/77442
- **作者**: @Yigtwxx
- **要点**: 修复 3 处 issue 自动化工作流问题：dedupe 工作流中 Statsig 事件时间戳被置为 1970 年、`days_back` 输入参数失效等。属于仓库内部自动化维护。

### 2. [已关闭] 同步 plugins 安全指引与 v2.0.0 插件清单
- **链接**: https://github.com/anthropics/claude-code/pull/77439
- **作者**: @Yigtwxx
- **要点**: security-guidance 插件已重写为 v2.0.0，但 marketplace.json 等清单文件仍描述 v1.0.0，此 PR 同步更新文档与版本信息。属文档/元数据修正。

### 3. [已关闭] 修复 ralph-wiggum 插件 stop hook 在 `set -e` 下的 jq 错误处理不可达问题
- **链接**: https://github.com/anthropics/claude-code/pull/77443
- **作者**: @Yigtwxx
- **要点**: 插件脚本在 `set -euo pipefail` 下，`$?` 检查不可达，导致 jq 解析失败时无法走友好错误处理分支。属插件可靠性修复。

### 4. [已关闭] 修复 #80705: Usage 泄漏问题（Atlas 自动贡献）
- **链接**: https://github.com/anthropics/claude-code/pull/81540
- **作者**: @ghost（Atlas 2 自动化）
- **要点**: 自动生成的修复 PR，关闭 #80705（Usage 泄漏 bug），声明奖励 $200。注意 PR 创建已有一段时间（7 月 27 日），本次为状态更新。

## 功能需求趋势

从全部 issues 中提炼，社区最关注的功能方向有以下几点：

1. **配额/用量可见性增强**（#69791、#69692、#83205）：statusLine 缺限流字段、/model 切换对话框缺缓存 token 与盈亏平衡估算、Max 配额消耗不透明——高频诉求集中在"让用户清楚看到钱花在哪"。
2. **终端与 TUI 体验优化**（#69185、#69799、#69787）：TTS 朗读增强、嵌入式终端滚动上限提高、`spinnerVerbs` 设置持久化——开发者希望 CLI 交互层更可自定义、更稳定。
3. **跨平台/远程开发支持**（#67136、#69728、#69734）：Windows SSH 远程连接线路缓冲问题、Android 远程控制 @ 文件补全、Linux `--resume` 磁盘配额挂起——远程与移动场景的稳定性是持续热点。
4. **权限系统精细化**（#69790、#69789、#69708）：subagent 无法弹权限提示、确认弹窗抢占回车键、iOS 后台权限挂起——权限机制在 agent 场景下需要更细粒度控制。
5. **新模型/API 集成兼容性**（#65208）：Bedrock 下模型 ID 与 inference profile 混用——随着 Haiku 4.5 等新模型推出，API 集成层适配问题开始显现。

## 开发者关注点

1. **模型行为可靠性是最大痛点**：#64260 中 Opus 4.8 编造用户请求并坚持虚构任务，配合 #69719（用户情绪化投诉规则违反次数统计），说明开发者对模型"自作主张"的容忍度很低，期望更严格遵循指示。
2. **Rate limit 与配额消耗的"黑盒"焦虑**：#65397 与 #83205 共同指向一个问题——用户无法理解配额为何异常消耗，Rate limit 触发时甚至伴随非预期的配额跳升，影响信任。
3. **多代理任务资源管理失控**：#69635（130 个 agents 自动扩展）、#69630（子代理会话残留 active）、#69732（通知丢失）构成一条完整线索：multi-agent 任务在**数量控制、生命周期回收、状态同步**三个方面都存在问题。
4. **大量历史 issue 批量关闭**：50 条更新中有 47 条为 CLOSED 状态（多为 stale/duplicate），说明官方正在清理 5–6 月积压。开发者关心的实际问题（如 worktree 操作分支错误）虽被关闭，但功能层面的修复节奏仍需观察。
5. **桌面端稳定性隐患**：macOS 桌面应用 PTY 泄漏（#67836）、压缩包截断崩溃循环（#65624）等反映桌面端在长时间运行和特定系统版本下仍有基础稳定性问题。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-02

## 今日速览

今日 Codex 仓库无新版本 Release，但 Issues 与 PR 更新活跃。GPT-5.6 Sol 子代理模型配置问题（#31814）以累计 100 条评论、167 个 👍 成为社区关注焦点；VS Code 扩展的 Codex Diff 崩溃问题（#35058/#35481/#36016）形成明显反馈集群。PR 侧，copyberry[bot] 贡献了 TUI 按键增强、远程插件搜索、exec-server 重构等多项改进，其中远程插件 bundle 体积上限提升与插件搜索机制值得关注。

## 社区热点 Issues

**1. GPT-5.6 Sol 强制所有子代理为 Sol 实例，无法单独配置** [#31814](https://github.com/openai/codex/issues/31814)（已关闭，100 评论，167 👍）
模型元数据中的 `multi_agent_version = "v2"` 会绕过 `features.multi_agent_v2` 开关，并默认隐藏子代理元数据，导致用户无法为子代理指定其他模型。该问题触及模型选择自由度，社区反响强烈。

**2. Codex Diff 在 VS Code 中崩溃显示 “Oops, an error has occurred”** [#35058](https://github.com/openai/codex/issues/35058)（开放，44 评论，111 👍）
macOS Apple Silicon + VS Code 1.128.0 环境下，任何仓库打开 Codex Diff 标签页均报错，扩展版本为 26.721.30844。社区对此反馈集中，已影响代码审查工作流。

**3. VS Code 扩展面板运行长时间后变灰** [#8197](https://github.com/openai/codex/issues/8197)（已关闭，55 评论，19 👍）
Windows 平台上 VS Code 扩展（0.5.52）在长时间运行后面板变为灰色，疑似渲染进程资源泄漏。

**4. Windows 安装程序在 UAC 提示前即失败** [#32149](https://github.com/openai/codex/issues/32149)（开放，29 评论，6 👍）
Windows 最新版安装程序在用户账户控制（UAC）弹出前就终止，两种安装选项均不可用，严重影响 Windows 用户上手。

**5. Windows 桌面版产生数百个 taskkill/conhost 进程，引发 WMI 风暴** [#33776](https://github.com/openai/codex/issues/33776)（开放，28 评论，26 👍）
ChatGPT.exe（桌面版 26.707.12708.0）在会话中残留 287 个 taskkill.exe 和 conhost.exe 进程，导致 WMI 失败风暴和 DWM 降级，属严重性能问题。

**6. Windows 上 apply_patch 因沙箱相关错误失败** [#30009](https://github.com/openai/codex/issues/30009)（开放，28 评论，10 👍）
Codex App 在 Windows 上通过 apply_patch 编辑文件时触发沙箱错误，阻碍文件修改操作。

**7. Hooks 在 Codex Desktop 更新后不再执行** [#21639](https://github.com/openai/codex/issues/21639)（开放，27 评论，6 👍）
回归问题：更新后 hooks 完全失效，受影响会话报告 cli_version 为 0.129.0-alpha.15。macOS 用户受影响，自动化工作流被破坏。

**8. OneDrive 备份工作区导致流式连接反复断开** [#35420](https://github.com/openai/codex/issues/35420)（开放，22 评论，0 👍）
Windows 上若选中工作区为 OneDrive 支持目录且 OneDrive 服务降级，ChatGPT Work/Codex 流式请求反复报 `stream disconnected before completion`。

**9. 7 月 9 日更新后内置图像生成持续网络错误** [#32297](https://github.com/openai/codex/issues/32297)（开放，21 评论，7 👍）
桌面版更新后，内置图片生成功能在网络环境下反复失败，社区有多个同类反馈。

**10. Windows 上 Codex Diff 同样崩溃** [#35481](https://github.com/openai/codex/issues/35481)（开放，13 评论，43 👍）
与 #35058 同类问题，但发生在 Windows 平台（扩展 26.721.41059），表明 Codex Diff 崩溃是跨平台共性问题。

## 重要 PR 进展

**1. 从 fork 的代理历史中剥离父级 MCP 生命周期事件** [#30977](https://github.com/openai/codex/pull/30977)（已关闭）
防止父级 `McpToolCallBegin/End` 事件污染子代理历史，保留父级完整 MCP 记录的同时避免状态串扰。

**2. 支持两键 TUI 键位组合** [#36511](https://github.com/openai/codex/pull/36511)（已关闭）
TUI 键盘映射支持 `ctrl-x ctrl-s` 等多键组合，并在上下文中显示待处理的组合键提示。

**3. 跨提示保留已尝试工具元数据** [#36507](https://github.com/openai/codex/pull/36507)（已关闭）
输出包含在后续提示中时重新附加 `executed_tool_calls` 元数据，上限 32 KiB，优先保留近期调用，超出部分记录截断信息。

**4. 提高远程插件 bundle 大小限制** [#36485](https://github.com/openai/codex/pull/36485)（已关闭）
远程插件下载上限从 50 MiB 提升至 100 MiB，解压后总大小上限从 250 MiB 提至 512 MiB。

**5. 将应用缓存逻辑抽取为 ConnectorRuntimeManager** [#31471](https://github.com/openai/codex/pull/31471)（开放）
重构 Codex Apps 工具缓存层，将缓存封装为不可变快照，并按 account、ChatGPT 用户、workspace 模式等维度隔离运行时上下文。

**6. 避免每次 TUI 重绘都查询终端尺寸** [#36482](https://github.com/openai/codex/pull/36482)（已关闭）
尺寸信息通过 resize 事件传递，普通重绘复用缓存；在 resize 稳定、进程恢复等场景刷新几何信息。

**7. 在 review 会话中保存 guardian transcript 边界** [#15261](https://github.com/openai/codex/pull/15261)（开放）
将父级 transcript 检查点存于缓存的 guardian review 会话中，后续 review 仅保留上次终止 review 以来的 transcript 证据。

**8. 抽取 exec-server 请求分发逻辑** [#36440](https://github.com/openai/codex/pull/36440)（已关闭）
将 JSON-RPC 请求、通知、响应、错误及畸形消息处理统一移入专门的 `RequestDispatcher`，连接循环只负责接收事件和关闭连接。

**9. 新增实时委托确认控制** [#36413](https://github.com/openai/codex/pull/36413)（已关闭）
`thread/realtime/start` 新增可选 `delegationAckFiller` 字段，显式转发给 V3 Frameless Bidi 会话的 `delegation.ack_filler`。

**10. 实现远程插件搜索** [#36409](https://github.com/openai/codex/pull/36409)（已关闭）
新增 `plugin/search` 请求，直接查询远程插件服务（绕过目录缓存），支持全局/工作区/个人三种范围与分页游标。

## 功能需求趋势

- **Windows 平台稳定性修复**：本期 Issue 中近三分之一与 Windows 相关：安装失败（#32149）、进程风暴（#33776）、沙箱错误（#30009）、OneDrive 断连（#35420）、线程重放卡顿（#33786）。Windows 用户已成为重要的反馈群体，桌面版在该平台存在系统性质量问题。

- **Codex Diff / 代码审查体验**：多个 Issue 指向 Diff 视图不可用（#35058、#35481、#36016），跨 macOS/Windows 平台，影响代码审查核心工作流，预计官方将优先修复。

- **大型会话性能与存储管理**：多代理 V2 会话的存储膨胀（#34268）、线程元数据无界增长导致启动崩溃（#29007）、打开历史会话卡顿（#29590、#25390）等表明，长会话和会话恢复机制需要架构级优化。

- **多 Git 仓库工作区支持**：#26338（27 👍）要求 Codex App 支持包含多个独立 Git 仓库的父工作区，是当前功能需求中呼声最高的增强方向。

- **远程连接能力增强**：#26846 希望桌面版可连接远程 Codex 主机；#30165、#24271 反映远程配对/项目列表同步问题，移动端与桌面端联动场景需求上升。

## 开发者关注点

- **子代理模型不可控**：#31814 的关闭引发争议，开发者希望自由配置 subagent 使用的模型，而非由模型元数据强制统一。该问题若得不到解决，可能继续发酵。

- **Diff 视图不可用直接影响日常代码审查**：多个 Issue 描述同一问题且各自都有一定评论与点赞，用户对修复速度有较高期待。

- **Windows 体验拖后腿**：安装程序无法完成安装、沙箱报错、进程泄漏、与 OneDrive 集成时断连……Windows 上多项基础功能不可用，开发者迁移成本高。

- **会话恢复与长会话稳定性备受关注**：hooks 失效（#21639）、自动压缩不触发（#16033）、历史记录消失（#26236）、任务交接后提前停止（#33398）等问题集中指向会话生命周期管理的不完善。

- **使用量意外消耗**：#35816 报告子代理审查/等待流程中周使用量一夜从 86% 降至 36%，#34898 描述治理循环导致使用量耗尽，用户对资源消耗的可控性存在疑虑。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-02**  
**数据来源：** [github.com/github/copilot-cli](https://github.com/github/copilot-cli)

---

## 今日速览

过去 24 小时，GitHub Copilot CLI 发布了 **v1.0.78-2**，优化了分栏侧边栏关闭交互并修复了扩展斜杠命令重复执行的问题。社区方面，共有 **21 条 Issue** 更新，讨论集中在 **多 BYOK 模型支持**、**MCP 服务器懒加载**、**长会话性能与稳定性**等方向，其中“多个 BYOK 模型”需求已获得 19 个 👍，成为社区最关注的功能点。过去 24 小时没有新的 Pull Request 出现。

---

## 版本发布

### [v1.0.78-2](https://github.com/github/copilot-cli/releases)

**Improved**

- 分栏侧边视图的关闭确认文案由 `x close` 调整为 `x again to close`（当为最后一个会话时显示 `x again to exit CLI`），明确提示用户第二次按 `x` 才会真正关闭，避免误触。

**Fixed**

- 扩展斜杠命令的 handler 修复为每次调用只执行一次，解决此前在某些场景下被重复执行的问题。

---

## 社区热点 Issues

过去 24 小时更新的 21 条 Issue 中，以下 10 条最值得关注：

### 1. [#3282 增加多个 BYOK 模型能力](https://github.com/github/copilot-cli/issues/3282)
- **标签：** `area:models`, `area:configuration`
- **创建：** 2026-05-13｜更新：2026-08-01｜💬 6｜👍 19
- **摘要：** 目前 Copilot CLI 仅支持通过环境变量配置一个 BYOK 模型。用户希望在 TUI 内部能直接切换多个 BYOK 模型，而不是结束会话重设环境变量。
- **为什么值得关注：** 这是当前获得 👍 数最高的需求，反映了自备模型用户的真实使用痛点。已开放近 3 个月，社区讨论持续升温，但官方尚未给出明确方案。

### 2. [#4305 将 JavaScript 值 `Undefined` 转换为 Rust 类型 `String` 失败](https://github.com/github/copilot-cli/issues/4305)
- **标签：** （未标注）｜更新：2026-08-01｜💬 5｜👍 5
- **摘要：** 用户升级到 1.0.76 后，几乎任何命令都会立刻出现该错误。从预发布版 1.0.76-2 开始出现，1.0.76 正式版中仍然存在。
- **为什么值得关注：**

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-08-02**


## 1. 今日速览

过去 24 小时无新版本发布，社区围绕**跨会话记忆系统（#1283）**与**远程控制（#1282）**两大功能请求持续进行高热度讨论。代码层面，4 个修复类 PR 正在推进，主要针对工具调用 JSON 解码、Shell 管道阻塞、Hook 任务回收等稳定性问题。


## 3. 社区热点 Issues

过去 24 小时共有 6 条 Issue 更新，覆盖长期功能请求、Bug 反馈与文档改进，以下为全部条目。

### 🔭 长期功能请求

**#1283 —— Memory System：跨会话持久上下文** — @CatKang
- 提出构建完整的记忆系统，使 Kimi Code CLI 能在会话之间记住项目模式、用户偏好与有用上下文；支持 AI 自动管理笔记与用户手动指令两种模式。
- 自 2026-02-27 创建以来持续活跃，目前已有 **10 条评论**，是社区长期关注的核心功能方向。
- [查看 Issue](https://github.com/MoonshotAI/kimi-cli/issues/1283)

**#1282 —— Remote Control：从任意设备继续本地会话** — @CatKang
- 支持用户从手机、平板或浏览器接管本地 CLI 会话，保持工作流不中断，解决"离开工位"场景下的连续性痛点。
- 获得 **23 👍** 和 **

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

## 今日速览

过去 24 小时 Qwen Code 发布了 v0.21.3 正式版，重点增强了 `/review` 命令的测试计划验证与失败归因能力。社区讨论热度集中在**提示缓存（prompt cache）优化**上，多个 Issue/PR 围绕缓存复用、命中率可观测性与延迟工具发现展开。此外，E2E 测试确定性成为开发重点，多个 PR 正在推动 CI 合并门禁落地。

---

## 版本发布

**v0.21.3**（正式版）  
本次发布的核心变化来自 `/review` 命令增强：新增测试计划验证、失败归因建模以及新的验证视角，提升对代码变更的分析质量。  
相关 PR：[#8215](https://github.com/QwenLM/qwen-code/pull/8215)、[#8218](https://github.com/QwenLM/qwen-code/pull/8218)

**v0.21.2-nightly.20260801.bc382c3ff**（pre-release）  
- feat(hooks): 生命周期钩子负载中新增 `session source` 字段，便于区分会话来源。([#8155](https://github.com/QwenLM/qwen-code/pull/8155))  
- feat(review): 审查缓存身份验证相关更新（内容截断）。([#8218](https://github.com/QwenLM/qwen-code/pull/8218))

---

## 社区热点 Issues（精选 10 条）

### 1. [feature] 更好的提示缓存（Better Prompt Caching）
[#8277](https://github.com/QwenLM/qwen-code/issues/8277)  
热度：👍 1 | 评论 2 | 状态：OPEN  
社区明确将提示缓存列为影响延迟、token 成本和本地模型 prefill 时间的关键方向，期望系统性地保持可复用提示前缀稳定。这是当前性能优化最核心的诉求。

### 2. [bug] 本地模型 qwen3-30b-a3b 工具调用失效
[#176](https://github.com/QwenLM/qwen-code/issues/176)  
热度：👍 7 | 评论 23 | 状态：CLOSED  
经典本地模型集成问题：模型正确生成 tool call 但未被执行，且无报错。该 Issue 自 2025 年 8 月发起，至今仍被社区持续关注，说明本地模型 + 工具调用的稳定性是长期痛点。

### 3. [bug] Deferred-tools 导致提示缓存每次都被破坏
[#4777](https://github.com/QwenLM/qwen-code/issues/4777)  
热度：评论 2 | 状态：OPEN  
MCP 工具的延迟发现被写进系统提示词，每次工具集变化都会使缓存失效。此问题直接影响长会话的 token 成本，与 #8277 紧密相关。

### 4. [bug] TUI 窗口滚动刷屏问题（Linux）
[#5971](https://github.com/QwenLM/qwen-code/issues/5971)  
热度：评论 4 | 状态：CLOSED  
在 Anolis OS 上多次对话后 TUI 窗口反复从头滚动，用户体验严重受损。该问题被标记为 `welcome-pr`，社区希望修复。

### 5. [feature] 支持从 qwen-code 仓库安装扩展
[#2635](https://github.com/QwenLM/qwen-code/issues/2635)  
热度：评论 3 | 状态：OPEN  
`/extensions install https://github.com/QwenLM/qwen-code.git` 安装失败，社区希望官方仓库直接提供 commands/skills/examples 扩展源。

### 6. [question] 如何追踪会话创建的文件
[#7966](https://github.com/QwenLM/qwen-code/issues/7966)  
热度：评论 6 | 状态：CLOSED  
开发者关注会话与工作区文件的归属关系，期望能准确识别哪些文件是哪个会话生成的（直接写入 / 代码执行间接生成）。

### 7. [bug] 虚拟历史模式下状态栏文本无法选中
[#8131](https://github.com/QwenLM/qwen-code/issues/8131)  
热度：评论 3 | 状态：OPEN  
macOS 环境下 Virtualized History 模式下状态栏文本无法选择，影响复制操作。该问题被标记为 `welcome-pr`。

### 8. [bug] Warp 终端中 @ 补全标签页切换失效
[#8330](https://github.com/QwenLM/qwen-code/issues/8330)  
热度：评论 3 | 状态：OPEN  
Ctrl+Tab 被 Warp 终端拦截，导致 Q

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*