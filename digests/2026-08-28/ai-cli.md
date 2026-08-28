# AI CLI 工具社区动态日报 2026-08-28

> 生成时间: 2026-08-28 06:10 UTC | 覆盖工具: 7 个

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

# AI CLI 工具社区动态横向对比分析报告

**报告日期：2026-08-28**
**数据范围：Claude Code、Gemini CLI、Kimi Code CLI、OpenCode、Qwen Code**
**说明：OpenAI Codex 与 GitHub Copilot CLI 今日无公开社区动态数据，不纳入对比。**


## 1. 生态全景

当前 AI CLI 工具已从“能用”进入“可信赖”的竞争阶段，Agent 自主性与可靠性取代功能数量成为社区最核心的关注点。安全与信任机制正在从附加功能变为基础设施，多款工具不约而同地强化沙箱、受限模式与环境变量治理。同时，各工具在模型兼容性、MCP 生态与跨平台支持上的投入明显加大，但 Windows、移动端等长尾环境仍是共同短板。整体上，工具间功能趋同加速，差异化更多体现在生态绑定、扩展机制与工程治理深度上。


## 2. 各工具活跃度对比

| 工具 | 今日活跃 Issues | 今日活跃 PR | 今日版本发布 | 社区热度信号 |
|------|:---:|:---:|:---:|------|
| **Claude Code** | 10（热点列表） | 未披露 | 2 个补丁版本（v2.1.248 / v2.1.250） | 最高热 Issue 395 👍 / 110 评论，社区基数大 |
| **Gemini CLI** | 10（热点列表） | 10 | 1 个 nightly（v0.59.0-nightly.20260828） | 单 Issue 最高 13 评论，P1 bug 密集 |
| **Kimi Code CLI** | 6 | 3 | 0 | 单 Issue 最高 1 👍，讨论量低，社区规模小 |
| **OpenCode** | 10（热点列表） | 10 | 2 个补丁版本（v1.18.24 / v1.18.25） | 最高热 Issue 43 👍 / 41 评论，UI 争议激烈 |
| **Qwen Code** | 10（热点列表） | 10 | 1 个 nightly（v0.22.2-nightly.20260828） | 单 Issue 最高 13 评论，架构讨论活跃 |
| **OpenAI Codex** | 无数据 | 无数据 | 无数据 | — |
| **GitHub Copilot CLI** | 无数据 | 无数据 | 无数据 | — |

> 注：各工具日报均只展示热点 Issue/PR 子集，不代表当日全量数据。


## 3. 共同关注的功能方向

### 3.1 Agent 自主性与任务可靠性（最突出）
- **Gemini CLI**：子代理达到 MAX_TURNS 仍误报成功（#22323）；不会主动使用 skills/sub-agents（#21968）
- **Kimi Code CLI**：Plan 模式下模型死循环不产出计划（#2623）
- **Qwen Code**：autofix 回归漏洞——连续失败不计入刹车机制（#10188）
- **OpenCode**：提出 Auto-Drive 自主执行引擎，让 Agent 从“提示-暂停”转向“自主巡航”（#45852）

社区共识：Agent 不能只在“被要求时”正确，更要在“自主决策时”可信。

### 3.2 钩子/事件扩展机制
- **OpenCode**：请求新增 SessionStart 钩子（#5409），向 Claude Code 对齐
- **Kimi Code**：修复 UserPromptSubmit 钩子中 prompt 恒为空的问题（#2176）
- **Qwen Code**：hooks 增加“智能体发起提问”事件触发（#10348），打通飞书/桌面推送

事件驱动正成为各工具的标配扩展点，且诉求从“执行命令前后”延伸到“会话生命周期”与“Agent 主动交互”。

### 3.3 远程 MCP 与连接可靠性
- **OpenCode**：远程 MCP 客户端缺少传输层重试机制（#25287）
- **Kimi Code**：远程 MCP 凭据不跨会话保存（#1211）
- **Claude Code**：远程控制自动重连失效（#34255）
- **Gemini CLI**：工具数超 128 个触发 400 错误（#24246）

MCP 生态能否落地，取决于“连得上、不断线、免重配”这三件事。

### 3.4 流式响应与超时挂死
- **Qwen Code**：120 秒无流活动超时（#5975）；Anthropic 流缺少看门狗（#9005，PR #9945）
- **Gemini CLI**：shell 命令执行完仍卡 “Waiting input”（#25166）
- **OpenCode**：DONE 哨兵处结束聊天流，避免挂起（#45850）

流式链路的稳定性已成为多款工具共同的工程痛点。

### 3.5 文档与 Office 文件处理
- **Claude Code**：请求支持 Word 修订模式（#9631）；PDF 依赖 poppler-utils 未文档化（#23704）
- **OpenCode**：PDF 被错误转发给不支持 PDF 的模型（#21908）；离线预览 docx/xlsx/pptx/pdf 的 PR（#45853）

企业文档场景需求上升，但当前各工具在该领域的能力仍偏薄弱。

### 3.6 安全与信任边界（多工具同日推进）
- **Claude Code**：v2.1.248 新增 `--restricted` 受限模式，移除命令执行类工具并限制文件访问
- **Gemini CLI**：当日 4+ PR 涉及安全——移除不安全 diff.external 覆盖（#28930）、GIT_CONFIG 三元组一致性（#28938）、信任对话框反向披露漏洞（#27901）、fail-closed 工作区信任（#29099）
- **Kimi Code**：升级 asyncssh 修复两个已知安全漏洞（#2622）

安全已经不是“应该做”，而是“正在做”的竞争维度。


## 4. 差异化定位分析

| 维度 | Claude Code | Gemini CLI | Kimi Code | OpenCode | Qwen Code |
|------|-------------|------------|-----------|----------|-----------|
| **功能侧重** | 安全边界、企业级管控 | Agent 可靠性、浏览器自动化、AST 感知 | Plan 模式、MCP 生态、IDE 集成 | 多模型聚合、UI 自定义、兼容性 | 架构治理、TUI 现代化、协议统一 |
| **目标用户** | 企业团队、受管环境 | Google 生态开发者、Agent 重度用户 | 中文开发者、Kimi API 用户 | 多模型用户、追求灵活性的开发者 | 中文开发者、Qwen 模型使用者 |
| **技术路线** | 功能全面、封闭生态、稳扎稳打 | nightly 高频迭代，安全问题当日修 | 跟随型迭代，社区驱动 | 激进创新（Auto-Drive）、兼容并包（读 CLAUDE.md） | 系统性重构（core/cli 分离、OpenTUI 迁移） |
| **独特信号** | `--restricted` 受限模式为当前独有的安全能力 | 浏览器代理韧性、AST 感知工具为前瞻方向 | 社区体量小但反馈直接，API 一致性问题引发强烈不满 | 同时维护新旧 UI 引发社区分裂，是典型的“演进阵痛” | 主动发起架构级重构，重视技术债治理 |

**简评：**

- **Claude Code** 凭先发优势和全功能覆盖，在企业市场占位最稳；今日新增受限模式进一步拉高安全上限。
- **Gemini CLI** 迭代速度最快、安全问题响应最积极，但 P1 bug 积压待回归测试，工程闭环需要加速。
- **OpenCode** 创新意愿最强（Auto-Drive 执行引擎），UI 改版引发的社区反弹也说明其用户粘性与主见并存。
- **Qwen Code** 处于重构期，社区讨论的技术深度高（架构审查、OpenTUI 迁移），短期以“还技术债”为主基调。
- **Kimi Code** 相对早期，社区活跃度有限，但 Plan 模式死循环和 API 空 content 问题直接影响核心体验，亟待解决。


## 5. 社区热度与成熟度

| 成熟度梯队 | 工具 | 判断依据 |
|-----------|------|---------|
| **成熟稳定型** | Claude Code | 版本节奏稳（补丁而非大改）、社区讨论内容偏向使用体验与安全边界，用户基数大 |
| **快速迭代型** | Gemini CLI / OpenCode | Gemini 每日 nightly、安全问题当日修复；OpenCode 两日两补丁、创新 PR 密集 |
| **重构演进型** | Qwen Code | 当前重心在架构治理与工程化，E2E CI 失败追踪 Issue 密集出现，处于“先稳后快”阶段 |
| **早期追赶型** | Kimi Code | 日活跃 Issue 仅 6 个、评论量低，版本发布节奏慢，仍处于功能补齐阶段 |

**综合热度排序（依据 Issue 评论量、👍 数与讨论深度）：**
Claude Code > OpenCode ≈ Qwen Code ≈ Gemini CLI >> Kimi Code


## 6. 值得关注的趋势信号

### 6.1 “可信自主执行”是下一阶段的核心竞争力
多个工具的社区反馈指向同一结论：Agent 的可靠性（不误报成功、不死循环、不悬挂）比新增功能更重要。开发者在意的不是“能做什么”，而是“能不能放心让它自己做”。建议开发者在评估工具时，将 **Agent 失败模式的可观测性**（中断是否明确、超时是否可重试）作为一等筛选条件。

### 6.2 安全边界从“可选项”走向“差异化卖点”
Claude Code 的 `--restricted` 模式与 Gemini 同日多项安全修复形成对照：前者通过产品化设计兜底，后者通过工程修复堵漏。对技术决策者而言，选择工具时应关注其 **安全模型是“设计内置”还是“事后修补”** ——这决定了在受管环境中的适配成本。

### 6.3 多模型/本地模型兼容成为基本盘
Qwen Code（LM Studio grammar 解析失败、Moonshot schema 报错）、OpenCode（Gemma 工具循环无法使用）、Kimi Code（openai_legacy 配置易错）都在同一天暴露了第三方模型兼容问题。AI CLI 工具正从“单模型专用终端”演变为“多模型通用入口”，**协议兼容性与 schema 健壮性将直接影响工具的天花板**。

### 6.4 扩展机制正在经历“标准化收敛”
Claude Code 的钩子模式（SessionStart 等）正在被 OpenCode、Qwen Code、Kimi Code 等行业内工具效仿；CLAUDE.md 文件格式也已被 OpenCode 用户主动请求兼容。马太效应初现：**Claude Code 定义的交互范式正在成为行业事实标准**。后发工具与其自造轮子，不如兼容已有生态以降低用户迁移成本。

### 6.5 跨平台与长尾环境的补齐仍需时间
Windows（Gemini grep_search EFTYPE、OpenCode ARM64 崩溃、Qwen longpaths）与移动端（OpenCode Termux 请求有 22 👍）的问题反复出现。对于在 Windows 或混合环境下工作的开发者，**当前 AI

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告

**数据截止**：2026-08-28  
**数据源**：github.com/anthropics/skills（PR 50 条 / Issues 50 条）

> 说明：以下 PR 均处于 **OPEN** 状态（截至数据收集日）。

---

## 1. 热门 Skills 排行

按仓库内评论热度排序，选取关注度最高的 8 个 PR。

### 1.1 fix(skill-creator): run_eval.py 始终报告 0% recall
- **作者**：@MartinCajiao | 创建于 2026-06-10
- **功能**：修复 run_eval.py 对所有 skill 描述一律报告 `recall=0%` 的问题；将评估产物安装为真实 skill，同时修复 Windows 流读取、触发检测及并行 worker 缺陷。
- **热点**：对应 Issue #556（12 条评论、7 个 👍），已被 10+ 独立复现。描述优化循环一直在对抗噪音，直接影响 skill-creator 核心流程。
- **链接**：https://github.com/anthropics/skills/pull/1298

### 1.2 Add document-typography skill
- **作者**：@PGTBoos | 创建于 2026-03-04
- **功能**：为 AI 生成文档提供排版质量控制，覆盖孤词换行、寡段标题滞留页底、编号错位等典型问题。
- **热点**：直击 AI 生成文档的普适痛点——用户很少主动要求排版质量，但问题影响所有文档输出。
- **链接**：https://github.com/anthropics/skills/pull/514

### 1.3 Add Hivemind: 零成本多智能体编排
- **作者**：@Hanishchow | 创建于 2026-08-21
- **功能**：让 Claude Code 将机械性工作委托给跑免费模型的 headless opencode workers，Claude Code 只负责规划、审查与合并。
- **热点**：发布 3 天即进入热度榜，核心观点是"昂贵模型的上下文才是稀缺资源，而非其智能"，切中上下文成本焦虑。
- **链接**：https://github.com/anthropics/skills/pull/1628

### 1.4 Add scnet-hpc skill
- **作者**：@lql341 | 创建于 2026-08-20
- **功能**：通过基于 profile 的 SSH 和 Slurm 工作流操作 SCNet HPC 集群，涵盖连接配置、Slurm 作业生成、集群发现与计算节点管理。
- **热点**：面向 HPC 科研场景的垂直 skill 需求浮现，更新活跃（08-24 仍有改动）。
- **链接**：https://github.com/anthropics/skills/pull/1615

### 1.5 Update claude-api skill: 标记四个退役模型 ID
- **作者**：@adi-IL | 创建于 2026-08-18
- **功能**：将 `claude-opus-4-1`、`claude-sonnet-4-0`、`claude-opus-4-0`、`claude-3-haiku-20240307` 四个模型 ID 标记为退役（Fixes #1603）。
- **热点**：官方 skill 的 API 准确性维护，社区对官方 skill 信息时效性有持续关注。
- **链接**：https://github.com/anthropics/skills/pull/1607

### 1.6 feat(skills): add self-audit — 推理质量门控
- **作者**：@YuhaoLin2005 | 创建于 2026-06-28
- **功能**：AI 输出交付前的审计 skill——先做机械文件验证（所有声明文件必须存在），再按损害严重性优先级执行四维推理审计，v1.3.0，声称通用任何项目/技术栈。
- **热点**：对应 Issue #1385（推理质量门控管线提案），反映社区对 AI 输出可信度的治理诉求。
- **链接**：https://github.com/anthropics/skills/pull/1367

### 1.7 feat: add testing-patterns skill
- **作者**：@4444J99 | 创建于 2026-03-22

---

# Claude Code 社区动态日报 — 2026-08-28

> 数据来源：github.com/anthropics/claude-code | 更新时间：2026-08-28

## 1. 今日速览

今日发布两个补丁版本，其中 v2.1.248 新增 `--restricted` 受限模式，可移除命令执行类工具并限制文件访问范围，强化安全边界。社区讨论热度集中在模型输出质量下降（#77136）与远程控制默认开启/自动重连问题（#34255、#88094、#90179），同时新出现多个安全与数据完整性 Issue（#90002、#90265），值得关注。

## 2. 版本发布

- **[v2.1.250](https://github.com/anthropics/claude-code/releases)** — Bug fixes and reliability improvements（修复和可靠性改进）。
- **[v2.1.248](https://github.com/anthropics/claude-code/releases)** — 新增 `--restricted`（或环境变量 `CLAUDE_CODE_RESTRICTED=1`）：移除执行命令或代码的内置工具及 `WebFetch`（除非在 `--tools` 中显式指定），文件工具仅限工作目录内，拒绝 `bypassPermissions`，并忽略用户、项目及本地设置文件。适合高风险/受管环境。

## 3. 社区热点 Issues（10 个）

1. **模型输出质量：Claude 4.7/4.8/5.0/Fable 趋于重复修辞，连贯性变差** — [#77136](https://github.com/anthropics/claude-code/issues/77136)
   - 作者：@pbower | 评论 110 | 👍 395
   - 社区最热 Issue：用户反映即使给出明确风格指令，模型仍频繁出现套话式表达，难以生成连贯散文，直接影响日常编码与文档工作。

2. **远程控制自动重连失效：连接静默断开且无恢复** — [#34255](https://github.com/anthropics/claude-code/issues/34255)
   - 作者：@BluCreator | 评论 69 | 👍 106
   - 高赞问题：Remote Control 连接在弱网/切换环境时静默丢失，不会自动重连，影响跨设备协作体验。

3. **已有订阅账户登录被重定向到 onboarding** — [#36797](https://github.com/anthropics/claude-code/issues/36797)
   - 作者：@migas5000 | 评论 34 | 👍 15
   - 虽然被标记为 `invalid`，但讨论量大，且今天仍有更新。活跃付费用户无法正常登录，官方应澄清是否为误标签或已修复。

4. **功能请求：支持 Microsoft Word (.docx) 编辑与修订（track changes）** — [#9631](https://github.com/anthropics/claude-code/issues/9631)
   - 作者：@ceaston-trumid | 评论 26 | 👍 30
   - 企业用户高频诉求：目前 Claude Code 无法直接编辑 .docx，需要间接转换，希望原生支持修订模式。

5. **PDF 读取依赖 poppler-utils 但未文档化，安装后无检测** — [#23704](https://github.com/anthropics/claude-code/issues/23704)
   - 作者：@carrotRakko | 评论 17 | 👍 20
   - Read 工具声称支持 PDF，但实际依赖 `pdftoppm`，常见镜像未预装，且缺少错误提示和安装引导，导致功能“看似支持实则不可用”。

6. **多行输入时 Up/Down 箭头跳转历史而非移动光标（回归约 2.1.15）** — [#63670](https://github.com/anthropics/claude-code/issues/63670)
   - 作者：@seanmartinsmith | 评论 19 | 👍 11
   - 全平台 TUI 回归：当输入内容软

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-28

## 今日速览

今日发布了 `v0.59.0-nightly.20260828` 版本，持续迭代。社区讨论焦点集中在 Agent 可靠性问题（子代理中断误报成功、shell 命令悬挂）以及安全相关修复（git 环境变量泄漏、工作区信任机制），多个人工维护的 P1 Bug 正在等待回归测试，同时 AST 感知工具与 Agent 自主使用 skills/sub-agents 的能力成为 feature 方向的核心讨论点。

## 版本发布

**v0.59.0-nightly.20260828.g3c311beac**
- 发布链接：[GitHub Release](https://github.com/google-gemini/gemini-cli/compare/v0.59.0-nightly.20260827.g3c311beac...v0.59.0-nightly.20260828.g3c311beac)
- 关联 PR：[#29113 chore/release: bump version to 0.59.0-nightly.20260828.g3c311beac](https://github.com/google-gemini/gemini-cli/pull/29113)
- 该版本为常规 nightly 自动发布，未包含面向用户的显著功能变更说明，完整变更请查看上方 compare 链接。

## 社区热点 Issues（10 个）

1. **[#22323] Subagent 达到 MAX_TURNS 后被误报为 GOAL 成功，隐藏中断** [priority/p1, kind/bug]
   - 作者：@matei-anghel | 评论：13 | 👍：2
   - 重要性：`codebase_investigator` 子代理在自身报告触发最大轮次限制、未执行任何分析的情况下，仍返回 `status: "success"`。这直接影响 Agent 任务执行的可信度，是 Agent 可靠性关键问题，社区讨论热烈。
   - 链接：https://github.com/google-gemini/gemini-cli/issues/22323

2. **[#28018] Gemini CLI 最新版本陷入无限认证循环** [priority/p1, kind/bug]
   - 作者：@skbr1234 | 评论：5 | 👍：5
   - 重要性：Google 登录后不断要求重新认证，无法结束。认证是使用 CLI 的第一道门槛，获得 5 个 👍 表明影响面较广，严重阻塞用户体验。
   - 链接：https://github.com/google-gemini/gemini-cli/issues/28018

3. **[#25166] Shell 命令执行完成后卡在 "Waiting input" 状态** [priority/p1, kind/bug]
   - 作者：@rnett | 评论：4 | 👍：3
   - 重要性：简单的 CLI 命令执行完毕后 Gemini 仍显示等待输入，命令悬挂不退出。Agent 自动化场景下此类悬挂会导致任务链无法推进，属于高频 P1 痛点。
   - 链接：https://github.com/google-gemini/gemini-cli/issues/25166

4. **[#22784] Windows 平台 grep_search 工具 spawn EFTYPE 错误** [priority/p2, kind/bug, help wanted]
   - 作者：@luo007 | 评论：8
   - 重要性：ripgrep 二进制与操作系统/架构不兼容导致搜索工具不可用。Windows 平台兼容性是开发者持续关注的问题，8 条评论表明有不少用户遇到同类问题。
   - 链接：https://github.com/google-gemini/gemini-cli/issues/22784

5. **[#22745] 评估 AST 感知的文件读取、搜索与代码库映射的影响** [priority/p2, kind/feature]
   - 作者：@gundermanc | 评论：7 | 👍：1
   - 重要性：EPIC 级 feature 追踪。AST 感知工具可通过一次调用精确读取方法边界、减少 token 噪音、改善代码库导航。这代表了 Agent 代码理解能力的演进方向。
   - 链接：https://github.com/google-gemini/gemini-cli/issues/22745

6. **[#21968] Gemini 不会主动使用 skills 和 sub-agents** [priority/p2, kind/bug]
   - 作者：@rnett | 评论：6
   - 重要性：用户反馈 Gemini 几乎不会自主调用自定义 skills（如 gradle/git）和子代理，除非显式指令。这关系到 Agent 自动化程度的根本体验。
   - 链接：https://github.com/google-gemini/gemini-cli/issues/21968

7. **[#22232] 增强 browser_agent 韧性：自动会话接管与锁恢复** [priority/p3, kind/feature]
   - 作者：@hsm207 | 评论：4
   - 重要性：浏览器代理在遇到 profile 锁定时采用 fail-fast 策略导致任务失败，建议实现自动接管和锁恢复。持久化会话模式下该问题影响显著。
   - 链接：https://github.com/google-gemini/gemini-cli/issues/22232

8. **[#27901] 信任对话框展示与执行引擎逻辑相反，存在安全披露风险** [priority/p1, kind/bug]
   - 作者：@acoderacom | 评论：2
   - 重要性：SessionStart 钩子中嵌套的钩子形状实际会执行但不在对话框中显示，而展示的扁平钩子却被丢弃，形成"反向披露"漏洞。涉及安全信任边界，P1 优先级（虽已关闭，但严重性高）。
   - 链接：https://github.com/google-gemini/gemini-cli/issues/27901

9. **[#26522] 阻止 Auto Memory 无限重试低信号会话** [priority/p2, kind/bug]
   - 作者：@SandyTao520 | 评论：5
   - 重要性：Auto Memory 只记录成功 `read_file` 的会话为已处理，低信号会话会反复出现。这会消耗不必要的 token 和后台资源，社区对内存系统质量关注度上升。
   - 链接：https://github.com/google-gemini/gemini-cli/issues/26522

10. **[#24246] 工具数量超过 128 个时 Gemini CLI 报 400 错误** [priority/p2, kind/bug]
    - 作者：@gundermanc | 评论：3
    - 重要性：工具数量达到上限后 API 直接报错，用户期望 Agent 能更智能地按需限制工具范围。这影响 MCP 生态下工具规模扩展的可行性。
    - 链接：https://github.com/google-gemini/gemini-cli/issues/24246

## 重要 PR 进展（10 个）

1. **[#28930] 移除不安全的 `diff.external` 覆盖** [priority/p1, size/m]
   - 修复 #28928：PR #28792 添加的 `['diff.external', '']` 在 git 中不被解释为"禁用外部 diff"，反而可能造成意外行为，此 PR 将其移除。
   - 链接：https://github.com/google-gemini/gemini-cli/pull/28930

2. **[#28938] 保持 `GIT_CONFIG_*` 环境变量三元组内部一致** [priority/p1, size/l]
   - 防止脱敏操作删除编号键值对的一半后，Git 配置环境变量无法解析；同时确保 ShellExecutionService 不会在脱敏后恢复敏感 Git 配置。
   - 链接：https://github.com/google-gemini/gemini-cli/pull/28938

3. **[#28939] 避免持久化中断响应的占位符文本** [priority/p1, size/l]
   - 修复 #28927：工具响应中断后，占位符文本 `[The previous response was interrupted...]` 被当作合成模型响应写入会话，后续 model 可能重复该文本，污染会话历史。
   - 链接：https://github.com/google-gemini/gemini-cli/pull/28939

4. **[#29110] `read_file` 内容路由改为通过 FileSystemService** [area/agent, size/l]
   - 修复 `read_file` 绕过 `FileSystemService` 直接读本地磁盘的问题，使 ACP 客户端通过 `fs.readTextFile` 能力声明时能够正确拦截和代理文件读取，与 `write_file`/`replace` 行为对齐。
   - 链接：https://github.com/google-gemini/gemini-cli/pull/29110

5. **[#28863] 扩展更新需用户同意，并清理运行时环境变量注入** [size/l]
   - 修复扩展更新绕过用户同意检查、向 MCP server 进程注入未授权环境变量的问题；将 MCP server 环境配置纳入同意字符串生成，并清理自定义环境变量。
   - 链接：https://github.com/google-gemini/gemini-cli/pull/28863

6. **[#29099] 强制执行 fail-closed 工作区信任并过滤 mcpServers** [size/l]
   - 在不受信任或受限环境中，A2A server 启动时过滤仓库定义的 `mcpServers`，防止意外进程执行，确保环境信任签名一致。
   - 链接：https://github.com/google-gemini/gemini-cli/pull/29099

7. **[#28926] 为 CONTRIBUTING.md 添加 Windows longpaths 设置指南** [priority/p2, size/xs]
   - Windows 下克隆仓库因默认 MAX_PATH 260 字符限制失败，产生约 3000 个脏暂存文件；此 PR 补充 `core.longpaths=true` 配置与恢复步骤。
   - 链接：https://github.com/google-gemini/gemini-cli/pull/28926

8. **[#28942] sandbox launcher 中 DEBUG 环境变量使用严格布尔解析** [area/platform, size/l]
   - 修复 #28885：原本用 JavaScript 字符串真值判断 DEBUG，导致 `DEBUG=false`/`DEBUG=0` 被错误视为开启调试，产生三个可观察 bug。
   - 链接：https://github.com/google-gemini/gemini-cli/pull/28942

9. **[#29104] 为斜杠命令自动补全添加 [Skill] 标签** [priority/p2, size/s, help wanted]
   - 在 `/` 自动补全菜单和 `/help` 中为 skill 类斜杠命令增加 `[Skill]` 标签，与现有 `[MCP]`/`[Agent]` 视觉区分保持一致，提升可发现性。
   - 链接：https://github.com/google-gemini/gemini-cli/pull/29104

10. **[#28827] 避免对 401 子串产生虚假认证错误** [priority/p2, size/s]
    - 修复 #28203：`isAuthenticationError` 误将包含 `401` 的无头值（如端口号、退出码）判为认证失败；新逻辑要求 `401` 位于消息开头或 HTTP 状态上下文中。
    - 链接：https://github.com/google-gemini/gemini-cli/pull/28827

## 功能需求趋势

- **Agent 自主性与可靠性**：多个 issue 聚焦于 Agent 能否更主动、更正确地使用已有能力——包括主动调用 skills/sub-agents（#21968）、子代理中断不应误报成功（#22323）、shell 命令执行完不悬挂（#25166）。这表明社区对 Agent 从"能执行"走向"可信赖地自主执行"有强烈期待。
- **AST 感知的代码理解工具**：#22745 及其子 issue #22746 提出用 AST 感知工具改进文件读取（精确方法边界）和代码库映射（如 tilth/glyph 工具），目标是减少 token 消耗并提高导航精确度，是值得关注的 Agent 效率方向。
- **安全与信任机制加固**：信任对话框与实际执行逻辑不一致（#27901）、环境变量脱敏（#28938）、MCP server 环境注入同意（#28863）、fail-closed 工作区信任（#29099）等多条 issue/PR 指向安全边界的系统性收紧。
- **Windows 平台支持**：grep_search EFTYPE 错误（#22784）、longpaths 克隆失败（#28926）等持续暴露 Windows 兼容短板，跨平台体验是用户高频反馈领域。
- **大规模工具集管理**：超过 128 个工具触发 400 错误（#24246），社区期望 Agent 能按需裁剪工具范围，而非硬性报错。
- **浏览器代理韧性**：persistent 模式下 profile 锁定导致失败（#22232）、Wayland 下浏览器代理失败（#21983）、settings.json 覆盖被忽略（#22267）——浏览器自动化场景的稳定性需求集中。

## 开发者关注点

- **P1 Bug 积压待回归**：#22323、#21983、#22186 均长期处于 `status/need-retesting`，社区反馈的问题在修复后未能及时验证关闭，建议维护者加快回归节奏。
- **认证与账号体验**：#28018 无限认证循环获得 5 个 👍，另有 #15986 Antigravity 账号资格问题，登录链路稳定性影响用户第一印象。
- **破坏性命令风险**：#22672 提出 Agent 在复杂 git 操作（`git reset`/`--force`）和数据库维护中应主动规避破坏性命令，并理解资源修改的危险性——安全性不能只依赖模型自觉。
- **Auto Memory / 记忆系统质量**：#26522 低信号会话无限重试、#26525 脱敏机制在内容进入模型上下文后才生效、#26523 内存补丁静默丢弃——多个 issues 指向记忆子系统仍需打磨。
- **非 UTF-8 页面解码**：#27980 指出 `web-fetch` 硬编码 UTF-8

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-08-28** | 数据源：github.com/MoonshotAI/kimi-cli

---

## 今日速览

今日社区最突出的动态有两点：一是 **Plan 模式暴露严重稳定性问题**——K3 模型在探索完成后陷入 `Bash echo`/`ReadFile` 死循环，迟迟不产出计划（#2623），明显影响核心工作流；二是 **开发者对 Kimi API 工具调用返回空 `content` 的行为表达了强烈不满**（#2621），该消息原样回传即触发 400 错误，沟通成本极高。此外，一项修复 `asyncssh` 安全漏洞的 PR 已提交（#2622），建议关注合入进度。

---

## 社区热点 Issues

本日共有 6 个活跃 Issue，以下按关注度与影响面排序：

### 1. [#2623] [bug] Plan mode：agent 在 Bash echo / ReadFile 上无限循环，始终不写计划
**作者** @zheng001001001 | **👍 0** | **评论 1** | **状态：OPEN**

- **详情**：Kimi Code CLI 0.38.0 + K3 模型，Linux 环境。Plan 模式下，模型探索完成后不调用 `ExitPlanMode`，而是无限循环执行 `Bash echo <任意字符>` 与 `ReadFile`，导致计划永远无法生成。
- **为什么重要**：作为核心协作模式，Plan 模式的循环会直接阻塞开发者日常任务执行，属高优 bug，有望获得维护团队快速响应。链接：https://github.com/MoonshotAI/kimi-cli/issues/2623

### 2. [#2621] [bug] Kimi API 工具调用返回空 content，原样回传即报 400
**作者** @Valen-akm | **👍 1** | **评论 0** | **状态：OPEN**

- **详情**：开发者在模型调用工具时发现返回消息中 `content` 为空，将这条 API 自己返回的消息原样回传后得到 `400: text content is empty`。社区不得不自行添加逻辑删除空 content 才能继续调用。
- **为什么重要**：虽言辞激烈，但该问题直指 API 设计的一致性缺陷，工具调用链路上“发出的消息无法被自身接收”极不合理，且对中下游开发者影响较大。链接：https://github.com/MoonshotAI/kimi-cli/issues/2621

### 3. [#1211] [bug] Notion Remote MCP 凭据不跨会话保存
**作者** @ghost | **👍 0** | **评论 3** | **状态：CLOSED**

- **详情**：v1.12.0 + macOS（MacBook Air M4）环境下，执行 `kimi mcp auth n...` 后，Notion 远程 MCP 的凭据仅存活于当前会话，重开会话需重新认证。
- **为什么重要**：远程 MCP 是扩展 Kimi 生态的核心途径，凭据持久化缺失会严重降低实际可用性。今日状态更新为 CLOSED，值得留意修复方案。链接：https://github.com/MoonshotAI/kimi-cli/issues/1211

### 4. [#1279] [enhancement] 原生 git-ai 集成，支持 AI 代码溯源
**作者** @deshes | **👍 0** | **评论 0** | **状态：CLOSED**

- **详情**：建议原生支持 [git-ai](https://git-ai.com) 标准，让开发者直接在 `git blame` 中识别某行代码来自 Kimi 还是人工编辑，实现 AI 生成代码的标准化追溯。
- **为什么重要**：AI 代码溯源正在成为团队协作与代码审查中的刚需，该请求代表社区对可审计 AI 生产力的前瞻性诉求。链接：https://github.com/MoonshotAI/kimi-cli/issues/1279

### 5. [#1272] [enhancement] JetBrains AI Assistant 中 ACP 调用 Kimi 无法识别文件
**作者** @yuweni99 | **👍 0** | **评论 1** | **状态：CLOSED**

- **详情**：在 JetBrains AI Assistant 中通过 ACP 调用 Kimi 时，拖入 IDE 的文件无法被自动识别，必须在提示词中给出完整文件路径，体验割裂。随附截图对比说明了问题。
- **为什么重要**：IDE 集成是开发者高频使用场景，而“看不见文件”会让 ACP 能力形同虚设，该 Issue 体现了社区对编辑器生产力一致性的高要求。链接：https://github.com/MoonshotAI/kimi-cli/issues/1272

### 6. [#2624] [docs] openai_legacy 托管接口缺少完整配置示例
**作者** @cursor[bot] | **👍 0** | **评论 0** | **状态：OPEN**

- **详情**：`providers.md` 文档已覆盖 `openai_legacy`，但三个细节容易被配错：① `type` 必须为 `openai_legacy`（而非 `openai_responses`）；② 走 Chat Completions wire 格式；③ 与 `/login` 模式的区别。
- **为什么重要**：配置文档是开发者自托管网关的第一入口，补齐清晰示例可显著减少接入摩擦。链接：https://github.com/MoonshotAI/kimi-cli/issues/2624

---

## 重要 PR 进展

本日共有 3 个活跃 PR，以下全部收录：

### 1. [#2622] deps: 升级 asyncssh 至 2.23.1（pykaos），修复安全公告
**作者** @katsugtgz | **👍 0** | **状态：OPEN**

- **内容**：将 `packages/kaos/pyproject.toml` 中 `asyncssh` 从 2.21.1 升级至 2.23.1，对应修复 GHSA-2wxc-x7rj-hg8f 与 GHSA-qr67-gv47-xwwh 两个安全漏洞，OSV 报告相关影响已在 `uv.lock` 中验证。
- **重要性**：安全补丁优先级高，建议维护团队尽快 review 合入，避免 pykaos 工作区暴露已知漏洞。链接：https://github.com/MoonshotAI/kimi-cli/pull/2622

### 2. [#2176] fix(hooks): 从 ContentPart 中提取文本供 UserPromptSubmit 钩子使用
**作者** @tears-mysthrala | **👍 0** | **状态：OPEN**

- **内容**：此前当 `user_input` 为 `list[ContentPart]`（消息默认格式）时，`UserPromptSubmit` 钩子中的 `prompt` 和 `matcher_value` 始终为空字符串，导致正则匹配类规则全部失效。本 PR 从 ContentPart 中正确抽取文本，修复 #2148。
- **重要性**：直接关系到钩子生态的可用性——当前很多基于关键词的自动化规则实际上处于静默失效状态。链接：https://github.com/MoonshotAI/kimi-cli/pull/2176

### 3. [#2595] fix(StrReplaceFile): 拒绝编辑非 UTF-8 文件
**作者** @shoemoney | **👍 0** | **状态：OPEN**

- **内容**：`StrReplaceFile` 此前通过 `errors="replace"` 解码整个文件，任何无效 UTF-8 字节（哪怕远离编辑位置）都会以 `U+FFFD` 落盘，最终损坏文件。本 PR 改为在编辑前校验文件编码，拒绝操作以避免破坏数据，修复 #2591。
- **重要性**：防止工具在二进制或混合编码文件中造成数据损坏，是编辑类工具可靠性的关键防线。链接：https://github.com/MoonshotAI/kimi-cli/pull/2595

---

## 功能需求趋势

综合近期 Issue 与 PR 内容，社区最关注的功能方向可归纳为 4 条主线：

| 方向 | 证据 | 说明 |
|------|------|------|
| **IDE 深度集成** | #1272 JetBrains ACP 文件识别失败 | 编辑器内无缝体验是刚需，拖拽/打开的文件应被 AI 自动感知，而非手动输路径 |
| **AI 代码可追溯性** | #1279 原生 git-ai 集成 | 团队协作场景下，区分 AI 与人工代码正在成为刚需，`git blame` 级别的溯源能力被期待 |
| **MCP 生态可用性** | #1211 远程 MCP 凭据持久化失效 | 远程 MCP 认证状态需跨会话保存，否则真实业务中每次重启都要重新授权 |
| **API 行为一致性** | #2621 空 content 回传报 400 | 平台自身返回的数据应保证合法，开发者不应被迫为官方行为写 workaround |

---

## 开发者关注点

开发者反馈与诉求中反复出现以下痛点：

- **工具调用链路自洽性**：最激烈的反馈来自 #2621——API 返回的空 `content` 在回传时反而触发 400 错误，迫使开发者额外编写容错逻辑。此类 API 一致性问题直接影响上层工具链的稳定性。
- **Plan 模式可靠性**：K3 在 Plan 模式下的死循环（#2623）已干扰正常开发，开发者期待维护团队为 Plan 模式引入更明确的终止条件与超时机制。
- **配置文档的实战性**：#2624 表明开发者更期望看到“开箱即用”的 provider 配置示例，而非概念性描述；差之毫厘的字段选择（如 `openai_legacy` vs `openai_responses`）会直接导致对接失败。
- **数据安全底线**：#2595 PR 侧面反映编辑工具对文件中非法编码的敏感度——开发者明确要求 AI 工具宁可不编辑，也不能破坏现有文件。

---

*本日报由 AI 自动编译，数据截至 2026-08-28 23:59 UTC。如有疏漏，欢迎指正。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-28

## 1. 今日速览

昨日连发两个补丁版本（v1.18.24 / v1.18.25），重点修复了 Azure 认证对 Bun 的硬依赖，并解决了 Bedrock 推理响应被错误缓存的问题。社区侧，围绕“旧版布局保留”的讨论热度持续攀升（41 条评论），Gemma 系列模型的工具调用循环问题也再次引发关注。此外，多个与消息历史回放、流结束处理相关的核心 PR 在今日集中提交，预示着一波稳定性修复正在路上。

## 2. 版本发布

**v1.18.25**
- 修复 Azure 认证：无需 Bun 即可完成 Azure CLI 登录。

**v1.18.24**
- 修复 Bedrock 推理响应被缓存为不可重放空消息的问题。
- Azure 提供商支持通过 Azure CLI 使用 Microsoft Entra ID 登录，不再强制要求 API Key。
- V1 版本开始读取受支持的 V2 配置字段，提升配置兼容性。

## 3. 社区热点 Issues

1. **[#37012] 保留旧版布局选项** — 41 条评论 / 43 👍
   社区强烈呼吁保留旧版布局，认为新版本需要在应用内多次导航才能找到选项，而旧版所有功能在主窗口即可触达。是当前社区分歧最大的 UI 议题。
   https://github.com/anomalyco/opencode/issues/37012

2. **[#21034] Gemma-4-26b/31b 在 OpenCode 中触发工具循环** — 21 条评论 / 20 👍
   即使在最新 tokenizer 修复和引擎补丁下，Gemma 模型仍无法在 OpenCode 中正常使用，频繁出现工具调用循环或失败，影响面较大。
   https://github.com/anomalyco/opencode/issues/21034

3. **[#961] Termux 支持请求** — 13 条评论 / 22 👍
   老牌需求，用户在移动端 Termux 环境无法正常使用 OpenCode，希望官方提供适配方案。
   https://github.com/anomalyco/opencode/issues/961

4. **[#5409] 新增 SessionStart 钩子** — 7 条评论 / 18 👍
   开发者希望在会话生命周期关键节点（如会话启动）增加类似 Claude Code 的 `SessionStart` 钩子，用于自动化流程编排。
   https://github.com/anomalyco/opencode/issues/5409

5. **[#21908] PDF 工具结果被转发给不支持 PDF 输入的模型** — 7 条评论
   `read.ts` 读取的合法 PDF 会被 `MessageV2.toModelMessagesEffect()` 转发给不支持 `input.pdf` 的模型，导致误报“文件损坏”。
   https://github.com/anomalyco/opencode/issues/21908

6. **[#44958] OpenCode Go 拒绝响应被隐藏且会话历史消失** — 6 条评论
   使用 `muse-spark-1.2-contributor` 时，HTTP 流已成功完成但 UI 不显示任何响应或错误，有时运行会无限期挂起。
   https://github.com/anomalyco/opencode/issues/44958

7. **[#37527] 不要弃用多项目/会话布局** — 6 条评论
   虽然旧布局仍可切换，但用户希望官方明确承诺不弃用旧版多项目/会话布局，并稳定新标签页布局下的阅读区域。
   https://github.com/anomalyco/opencode/issues/37527

8. **[#25287] MCP 远程客户端缺少传输层重试机制** — 6 条评论
   当远程 MCP 服务器暂时不可达（重启、休眠恢复、TCP 失效）时，客户端没有任何恢复机制，连接直接失效。
   https://github.com/anomalyco/opencode/issues/25287

9. **[#17436] 支持 .claude/CLAUDE.md 项目文件** — 6 条评论
   希望兼容 Claude Code 的项目记忆文件（`CLAUDE.md` / `.claude/CLAUDE.md`），降低迁移成本。
   https://github.com/anomalyco/opencode/issues/17436

10. **[#45087] 自动更新器吃掉 266 GB 磁盘** — 5 条评论
    长驻的 `opencode2 serve --service` 进程每 10 分钟重复安装 OpenCode beta 包，最终在 `~/.npm/_cacache` 积累 266 GB 垃圾数据。
    https://github.com/anomalyco/opencode/issues/45087

## 4. 重要 PR 进展

1. **[#45845] 移除 Azure 认证中的 Bun 依赖** — 已合并
   将 Azure 插件中的 `Bun.which` 替换为运行时中立的可执行文件查找，并通过跨平台 `Process.run` 执行 Azure CLI 命令。对应 v1.18.25 修复。
   https://github.com/anomalyco/opencode/pull/45845

2. **[#45840] 将 AISDK 网络故障归类为传输错误** — 已合并
   此前 undici `terminated`、Bun `ECONNRESET`、SSE 块超时等网络异常未被 SDK 包装为 `APICallError`，会落入 `UnknownProviderError`。现在统一归为传输错误。
   https://github.com/anomalyco/opencode/pull/45840

3. **[#45843] 强化后台 Shell 执行指导** — 已合并
   明确自动完成通知会包含命令输出，并禁止 sleep 命令和输出文件轮询等待，避免后台任务滥用。
   https://github.com/anomalyco/opencode/pull/45843

4. **[#45847] 忽略迟到的 Bedrock Converse 工具增量** — 已合并
   记录已完成的工具索引，忽略内容块停止后到达的工具输入增量，避免脏数据写入会话。
   https://github.com/anomalyco/opencode/pull/45847

5. **[#45850] 在 DONE 哨兵处结束聊天流** — 已合并
   保留 Chat Completions 的 `[DONE]` 哨兵，处理完 finish 和 usage 块后立即终止流，不再读取开放响应体。
   https://github.com/anomalyco/opencode/pull/45850

6. **[#45839] 回放时丢弃无模型可见内容的助手轮次** — OPEN
   修复 Moonshot/Kimi、DeepSeek、Azure 等严格提供商因空 assistant 消息返回 400 的问题，关闭 #37946 和 #31046。
   https://github.com/anomalyco/opencode/pull/45839

7. **[#45853] 离线文档预览（docx/xlsx/pptx/pdf）** — OPEN
   实现本地文件离线预览，支持 Office 文档的列宽、合并单元格、冻结窗格、工作表标签等，附带插件调用路由和 i18n。
   https://github.com/anomalyco/opencode/pull/45853

8. **[#45852] 自主自动领航执行引擎（Auto-Drive）** — OPEN
   引入“自动驾驶”式会话续跑机制：跨轮次追踪初始用户目标、综合上下文，让 Agent 从“提示-暂停”模式转向“自主巡航”，实现无需人工干预的连续执行。
   https://github.com/anomalyco/opencode/pull/45852

9. **[#45844] Windows ARM64 回退到 x64 构建** — OPEN
   原生 windows-arm64 构建因 bun:ffi 不可用导致 OpenTUI 初始化崩溃，此 PR 在 ARM64 上回退使用 x64 构建以恢复可用性。
   https://github.com/anomalyco/opencode/pull/45844

10. **[#45848] TUI 支持含斜杠的频道名** — OPEN
    修复从分支名派生的频道（如 `feature/foo`）被当作路径段处理而无法正常存储的问题。
    https://github.com/anomalyco/opencode/pull/45848

## 5. 功能需求趋势

- **布局与 UI 自定义**：旧版布局保留（#37012）、多项目/会话布局不弃用（#37527）、恢复旧版 UI 并进入 Build 模式（#34055）成为最集中的 UI 诉求。
- **会话生命周期钩子**：`SessionStart` 等事件钩子（#5409）的呼声日益增长，开发者希望像 Claude Code 一样拥有精细的自动化控制点。
- **MCP 生态可靠性**：远程 MCP 连接重试（#25287）、大数据量传输截断（#32497）等问题显示 MCP 稳定性是当前集成体验的主要瓶颈。
- **新模型与提供商兼容性**：Gemma 4 工具调用（#21034）、Qwen3.8 Flash 文档补充（#45836）、Thinking/推理选项未按模型能力过滤（#34323）等，反映社区对多模型适配的高敏感度。
- **文档与 Office 文件处理**：PDF 被错误转发（#21908）、离线文档预览 PR（#45853），文档类工作流正在成为关注点。
- **移动与终端环境支持**：Termux 支持（#961）虽为老 issue 但持续获赞，移动端需求依然存在。
- **稳定性与资源占用**：自动更新器磁盘占用（#45087）、桌面端 CPU 占用过高（#34236）、CLI 长时运行后定时器失效（#34372）等稳定性问题高频出现。

## 6. 开发者关注点

- **Gemma 模型不可用**：工具循环/失败问题迟迟未解，即使引擎侧已修复，OpenCode 集成层仍不兼容。
- **Azure 认证依赖链**：v1.18.25 修复前，Azure CLI 登录居然要求 Bun 运行时，属于明显的环境依赖漏洞。
- **空消息回放导致严格提供商报错**：空文本/空 assistant 消息被持久化后回放，多个严格提供商返回 400/422，是高频痛点。
- **旧布局迁移阵痛**：新 UI 的信息密度和操作效率不如旧版，用户希望保留选择权而不是被迫迁移。
- **远程 MCP 恢复能力缺失**：服务器短暂不可达后客户端完全无法自愈，只能手动重启会话。
- **自动更新器失控**：常驻进程在内存中持续按旧版本检查更新，导致每 10 分钟重复下载安装包，磁盘占用量惊人。
- **Windows 集成细节**：PowerShell 5.1/7 混用（#17372）、VS Code 扩展启动竞态（#33659）、Windows ARM64 崩溃（#45844）等问题表明 Windows 平台体验仍粗糙。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-28

## 今日速览

今日发布了 `v0.22.2-nightly` 版本，修复 Web Shell 会话差异恢复及钉钉富文本问题。社区层面，流式响应超时问题（#5975）和核心/CLI 架构重构讨论（#4063）热度持续走高，TUI 渲染层迁移至 OpenTUI 的提案（#8662）也吸引了大量关注；此外，多个 E2E CI 失败自动追踪 Issue（#10356 等）集中出现，提示测试稳定性成为当前开发重点。

## 版本发布

**v0.22.2-nightly.20260828.7357136dd1**

- fix(web-shell): restore saved session diffs（恢复已保存的会话差异）
- fix(channels): preserve DingTalk rich-text multi-（保留钉钉富文本多段格式，内容截断，详见 Release 页）

发布页：https://github.com/QwenLM/qwen-code/releases

## 社区热点 Issues

**1. [API Error: No stream activity for 120000ms after 19 chunks](https://github.com/QwenLM/qwen-code/issues/5975)** ★ 评论 13
自 v0.19.3 起频繁出现流空闲超时，影响多轮对话。此前必有 "Thought" 但无输出，随后报错。社区攒了较多复现信息，属于高优先级 P2 回归问题。

**2. [refactor: core + cli 架构 Review — 12 项结构性问题清单](https://github.com/QwenLM/qwen-code/issues/4063)** ★ 评论 11
社区核心贡献者 @pomelo-nwu 主导的架构审查，列出 136 个文件直接依赖 `@google/genai` 类型等 P0 问题，讨论活跃，已进入 in-progress 状态。

**3. [Migrate TUI rendering layer from ink to OpenTUI (tracking)](https://github.com/QwenLM/qwen-code/issues/8662)** ★ 评论 10
ink 渲染器存在结构性问题（闪烁、虚拟视口补丁达 1037 行），提案迁移至 OpenTUI，属 roadmap/terminal-ux 方向，社区讨论热烈。

**4. [自定义模型供应商无法对话](https://github.com/QwenLM/qwen-code/issues/10227)** ★ 评论 7
Moonshot 兼容接口报 `tools.function.parameters is not a valid moonshot flavored json schema`，说明工具输出 Schema 兼容性需要加固。

**5. [design(core): make derived Config context ownership explicit](https://github.com/QwenLM/qwen-code/issues/8083)** ★ 评论 7
关于 Config 原型链继承导致的上下文所有权不明确，尽管已关闭，但设计讨论对理解 Config 体系很有价值。

**6. [LM Studio 0.4.21: request fails with "failed to parse grammar"](https://github.com/QwenLM/qwen-code/issues/10065)** ★ 评论 6
本地模型场景下即使关闭 MCP 和 tools.core，仍出现 grammar 解析失败，影响 LM Studio 用户，状态已标记 ready-for-human。

**7. [The Anthropic wire is missing stream-safety protections](https://github.com/QwenLM/qwen-code/issues/9005)** ★ 评论 5
Anthropic 流式接口缺少 OpenAI wire 已有的空闲/生命周期保护，属 P1 优先级，已有对应 PR #9945 在推进。

**8. [Main CI failed: E2E Tests on 148273956b5c](https://github.com/QwenLM/qwen-code/issues/10356)** ★ 评论 4
主分支 E2E 测试在报告任何测试结果前即失败，CI 基础设施或测试隔离需关注，已自动追踪。

**9. [hooks 触发事件增强](https://github.com/QwenLM/qwen-code/issues/10348)** ★ 评论 4
希望 hooks 支持「智能体发起提问」事件触发，以便后台任务通过飞书/桌面推送通知，社区需求明确。

**10. [proposal(serve): L2 能力分层 — DaemonWorkspaceService](https://github.com/QwenLM/qwen-code/issues/4542)** ★ 评论 4
架构提案，讨论 ACP 与 REST 等价替代所缺的文件 I/O、设备流登录、agents/memory CRUD 收口方案。

## 重要 PR 进展

**1. [fix(core): guard Anthropic streams with idle and lifetime watchdogs](https://github.com/QwenLM/qwen-code/pull/9945)**
将 OpenAI wire 的流式看门狗（空闲/生命周期守护）应用到 Anthropic generator，静默或持续输出 thinking 帧时以可重试 `ETIMEDOUT` 中断，避免 CLI 挂死。

**2. [fix(core): clean up project snapshots for temporary working directories](https://github.com/QwenLM/qwen-code/pull/9110)**
为一次性工作目录启动的会话增加快照清理路径：优雅关闭时删除非 ACP/非 handoff 会话快照，防止 `projects/` 存储积累垃圾。

**3. [fix(omni): harden policy tool contracts](https://github.com/QwenLM/qwen-code/pull/10364)**
对 #10351 的后续加固：剪辑视频时保留音频、字幕/摘要证据记录到正确媒体通道、对齐补丁网格后强制执行视觉 token 预算，并修复 EXIF 坐标契约。

**4. [fix(cua): harden Computer Use sessions and instructions](https://github.com/QwenLM/qwen-code/pull/10319)**
Node REPL Computer Use 路径四项加固：原生调用接入真实 AbortSignal（25 秒默认超时）、类型化超时/取消错误、授权过期处理、指令注入防护。

**5. [fix(autofix): charge regressions to the brake and gate test weakening](https://github.com/QwenLM/qwen-code/pull/10188)**
修复 autofix 循环两处漏洞：连续失败刹车此前只统计未推送的轮次，回归成本为零；本 PR 将回归计费到刹车机制，堵住「免费引入新问题」的漏洞。

**6. [fix(ci): route release pipeline Linux jobs to the ECS runner pool](https://github.com/QwenLM/qwen-code/pull/10036)**
将 release 流水线的 prepare/quality/integration_none/integration_docker 四个 Linux job 路由到 ECS runner 池，提升 CI 稳定性。

**7. [fix(cli): derive bootstrap --help from shared option definitions](https://github.com/QwenLM/qwen-code/pull/8902)**
快速帮助路径不再显示手动维护的过时选项子集，从真实 parser 共享定义派生 `qwen --help`，避免文档漂移。

**8. [feat(daemon): support scoped workspace memory tasks](https://github.com/QwenLM/qwen-code/pull/9895)**
为无会话托管记忆的 remember/forget 增加 `project`/`user` 目标作用域，覆盖 REST、ACP 扩展方法及 TypeScript daemon SDK，支持能力协商。

**9. [fix(test): isolate tool-control E2E from shared state](https://github.com/QwenLM/qwen-code/pull/10340)**
针对 E2E 运行 #33140800509（对应 Issue #10356）暴露的 tool-control 测试 flake：隔离共享 Qwen 状态和 managed-memory 干扰，减少 Docker 分片失败。

**10. [feat(web-shell): unblock git update on dirty working tree](https://github.com/QwenLM/qwen-code/pull/9769)**
Web Shell 的「Update Project」在遇到未提交变更时不再死路：提供分支选择器弹层，给出两种解决方式，提升 Git 操作体验。

## 功能需求趋势

- **架构重构与解耦**：超一半高热度 Issue 集中在架构层——核心类型系统对 `@google/genai` 的过度依赖（#4063）、slash-command 契约与 UI 状态耦合（#9150）、Config 派生上下文所有权（#8083）。社区对「可维护性/可测试性」诉求强烈。
- **终端 UX 现代化**：TUI 从 ink 迁移 OpenTUI（#8662）、渲染性能优化（#9970）、推理更新乱序修复（#9475），terminal-ux 已列为 roadmap 专项。
- **协议与集成统一**：ACP stdio/HTTP 双路径合一并升级 SDK 到 1.x（#10061）；serve 层 L2 能力收口（#4542）；Aone 成为一等 PR 绑定平台（#10287）。跨平台集成体验正在被体系化梳理。
- **钩子/事件能力深化**：请求 hooks 支持智能体提问触发（#10348），希望打通飞书/桌面推送等外部通知链路。
- **本地与自定义模型兼容性**：LM Studio、Moonshot、Ollama 等多个自定义/本地模型接入问题（#10065、#10227、#9438）说明社区实际部署环境多样，Schema 兼容与消息格式健壮性需加强。

## 开发者关注点

- **0.22 版本回归**：#10147 明确反馈升级 0.22 后本地命令执行和文件编辑完全失效，开发者要求「允许禁用自动升级」，此类升级回归影响面大，建议尽快定位。
- **流式超时与挂死**：#5975（120s 无流活动）、#9005（Anthropic 流缺看门狗）反映流式链路的稳定性是高频痛点，好在 #9945 已给出修复方向。
- **CI/测试稳定性**：#10356、#10350、#10349 等一批 E2E 自动失败追踪 Issue 密集出现，社区与维护者共同关注测试基础设施的可靠性。
- **小屏幕/复杂交互渲染**：#9475 推理内容在屏幕中间更新打乱布局，TUI 渲染路径仍需打磨。
- **对自动升级的控制**：部分开发者希望在配置中提供「禁止自动升级」开关，以便在回归出现时保持可用版本。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*