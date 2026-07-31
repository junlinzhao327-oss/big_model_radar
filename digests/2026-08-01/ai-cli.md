# AI CLI 工具社区动态日报 2026-08-01

> 生成时间: 2026-07-31 23:26 UTC | 覆盖工具: 7 个

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



---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告

**数据范围**：github.com/anthropics/skills 官方仓库 ｜ 截止 2026-08-01

---

## 1. 热门 Skills 排行

> 按讨论热度（评论数）排序，当前所有热门 PR 均处于 **Open** 状态。

**① skill-creator 评估体系修复（#1298）— 热度最高**
修复 `run_eval.py` 对所有描述恒定报告 `recall=0%` 的严重缺陷（关联 #556，已有 10+ 独立复现），同时覆盖 Windows 流读取、触发检测和并行 worker 问题。社区讨论核心：描述优化循环目前是在"对噪声做优化"，整个 skill-creator 工作流失真。这是当前仓库最聚焦的痛点。
🔗 https://github.com/anthropics/skills/pull/1298

**② document-typography 文档排版技能（#514）**
针对 AI 生成文档的典型排版问题：孤立单词换行、标题悬挂在页底、编号错位。社区认为这类问题"每一个 Claude 生成的文档都会遇到"，属于高频刚需。
🔗 https://github.com/anthropics/skills/pull/514

**③ ODT 办公文档技能（#486）**
覆盖 OpenDocument 格式（.odt/.ods）的创建、模板填充、读取及转 HTML。社区关注点是开源/ISO 标准格式的文档生产能力，与现有 DOCX/PDF 技能形成互补。
🔗 https://github.com/anthropics/skills/pull/486

**④ frontend-design 技能可操作性改进（#210）**
重构前端设计技能，确保每条指令都能在单次会话中被 Claude 实际执行，强调"足够具体以约束行为"。讨论焦点：技能描述从"面向人阅读的文档"转向"面向 Claude 执行的操作手册"。
🔗 https://github.com/anthropics/skills/pull/210

**⑤ skill-quality-analyzer + skill-security-analyzer 元技能（#83）**
新增两个元技能：质量分析器从结构/文档/示例等五个维度评估 SKILL.md；安全分析器聚焦技能安全审计。讨论热点：社区开始自发建设"技能的技能"，即对 Skill 本身的质检与安全审查。
🔗 https://github.com/anthropics/skills/pull/83

**⑥ testing-patterns 测试模式技能（#723）**
覆盖完整测试栈：Testing Trophy 模型、单元测试 AAA 模式、React 组件测试（Testing Library）、以及"什么该测/什么不该测"。讨论核心是沉淀一套可执行的测试方法论而非零散模板。
🔗 https://github.com/anthropics/skills/pull/723

**⑦ pyxel 复古游戏开发技能（#525）**
由 Pyxel 引擎作者 @kitao 提交，接入 pyxel-mcp，支持"写码→运行截帧→检查→迭代"的 retro/pixel-art 游戏工作流。社区关注：MCP + Skills 结合的游戏开发闭环。
🔗 https://github.com/anthropics/skills/pull/525

**⑧ self-audit 交付前自审计技能（#1367）**
先做机械化文件验证（检查所有声明输出的文件是否存在），再按"损害严重度优先级"执行四维度推理审计，定位为通用型技能。讨论热点：把交付质量门禁前置到输出环节。
🔗 https://github.com/anthropics/skills/pull/1367

---

## 2. 社区需求趋势

**① 工具链可靠性（最强烈）**
- `run_eval.py` 触发率恒为 0%、优化循环失效（#556，12 评论、7 👍）、同主题复现 #1169、Windows 兼容性 #1061——skill-creator 自身的质量已严重拖累 Skill 开发效率。
- #202（已关闭）直指 skill-creator"读起来像开发者文档而不是可操作技能"，要求按最佳实践重写。

**② 安全与信任边界**
- #492（43 评论，全场最高）社区技能在 `anthropic/` 命名空间下分发，构成信任边界滥用风险——用户可能误将社区技能当作官方技能授予高权限。
- #1175 关注 SharePoint Online 场景下在 SKILL.md 中编写访问控制逻辑的安全性与上下文窗口问题。

**③ 企业级协作与共享**
- #228（16 评论、8 👍）呼声最高的功能需求：组织级 skill 共享。当前手动下载/传输/上传的流程严重阻碍团队推广。
- #189 两个插件安装后内容重复，导致上下文窗口被浪费。

**④ 智能体记忆与治理**
- #1329 提出 compact-memory 技能：用符号化记法压缩长时运行 agent 的持久记忆，减少上下文开销。
- #412 提议 agent-governance 技能：策略执行、威胁检测、信任评分与审计追踪。
- #1385 提出三段式推理质量门流水线（任务前校准→对抗评审→交付验证）。

**⑤ 平台与互操作**
- #16 呼吁将 Skills 暴露为 MCP，统一 AI 软件 API 协议；#29 询问 AWS Bedrock 支持；Windows 兼容问题多次出现（#1061）。

---

## 3. 高潜力待合并 Skills

以下 PR 讨论活跃、问题定位明确，近期落地概率较高：

| PR | 内容 | 潜力分析 |
|---|---|---|
| [#1298](https://github.com/anthropics/skills/pull/1298) | skill-creator eval 修复 | 直击 #556，与 #1099/#1050/#1323/#1261 形成修复合力，属官方优先事项 |
| [#538](https://github.com/anthropics/skills/pull/538) | pdf 技能大小写引用修复 | 单点修复、影响明确（大小写敏感文件系统直接报错），易合入 |
| [#541](https://github.com/anthropics/skills/pull/541) | docx 修订 w:id 冲突修复 | 修复文档损坏级 bug，OOXML 原理分析扎实 |
| [#539](https://github.com/anthropics/skills/pull/539) | skill-creator YAML 引号校验 | 防御性校验，防止 description 被静默截断，与 #1298 同属工具链加固 |
| [#514](https://github.com/anthropics/skills/pull/514) | document-typography | 高频刚需、覆盖面广，评审通过后可快速落地 |
| [#723](https://github.com/anthropics/skills/pull/723) | testing-patterns | 内容完整、结构清晰，测试方向是社区长期关注点 |
| [#1302](https://github.com/anthropics/skills/pull/1302) | color-expert | 自包含、知识密度高（ISCC-NBS/Munsell/OKLCH 等），作者为知名色彩库维护者 |
| [#1479](https://github.com/anthropics/skills/pull/1479) | plan-file-hygiene | 回应 #1417，针对规划产物无生命周期的明确缺口，话题热度上升中 |

---

## 4. Skills 生态洞察

**一句话总结**：当前社区最集中的诉求是"让 Skill 工具链本身先可靠起来"——skill-creator 评估循环的 0% recall 缺陷、Windows 兼容性和安全信任边界问题是讨论热度最高的三大主线，而新 Skill 方向则明显向**文档排版质量、测试方法论、智能体治理与记忆管理**这些横切能力倾斜。

---



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-08-01）

## 1. 今日速览

今日 Codex 发布了 3 个 Rust 版预发布版本（v0.147.0-alpha 系列），但均无详细发布说明。社区讨论热度集中在两大方向：一是配额/用量相关的争议性 bug（后台轮询消耗模型额度、子代理 busy-waiting 烧完一周配额），二是 Windows 平台上的稳定性问题（启动崩溃、沙箱失效、项目丢失）。PR 侧则以大型架构重构为主，涉及 MCP 配置整合、线程历史所有权、沙箱 V8 支持等关键改动。

## 2. 版本发布

**rust-v0.147.0-alpha 系列（3 个版本）**

- [rust-v0.147.0-alpha.4](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.4)
- [rust-v0.147.0-alpha.3](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.3)
- [rust-v0.147.0-alpha.1.1](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.1.1)

三个版本均未附带详细变更日志，仅有占位描述。建议关注后续完整的 release notes，以了解 CLI 侧的功能演进。

## 3. 社区热点 Issues（Top 10）

### 🔥 高热度需求

**[#28969] 建议增加禁用“60 秒自动解析”的设置**（64 评论，185 👍）
作者：[antoyo](https://github.com/antoyo) | [链接](https://github.com/openai/codex/issues/28969)
> 用户希望在 Codex CLI 中增加一个开关，禁用交互模式下 60 秒无回复即自动结束/resolve 的行为。这是当前 Issue 区评论数和点赞数最高的需求，反映出大量用户受困于长任务处理时被超时打断的问题。

**[#30712] Windows 桌面版注入 split writable roots，导致 apply_patch 失败并迫使 agent 绕过沙箱**（16 评论，13 👍）
作者：[PurpleDevX](https://github.com/PurpleDevX) | [链接](https://github.com/openai/codex/issues/30712)
> Windows 上 apply_patch 因错误的可写根目录配置而失效，agent 被迫回退到 PowerShell 写入文件，完全绕过了沙箱保护。这不仅是功能 bug，更涉及安全底线，Windows 用户应重点关注。

### 🐛 严重性能/资源问题

**[#30408] MCP server 进程泄漏：每线程进程永不清理（RSS 超 9GB）**（21 评论）
作者：[kkkayye](https://github.com/kkkayye) | [链接](https://github.com/openai/codex/issues/30408)
> app-server 为每个会话重新拉起全套 MCP server 进程，但归档/关闭线程时从不销毁它们。长期使用后内存占用可达 9GB+，是当前最严重的资源管理 bug 之一。

**[#25779] Codex Desktop 元 bug：无界 session/turn 状态导致冻结、上下文膨胀和失控**（13 评论）
作者：[FromAriel](https://github.com/FromAriel) | [链接](https://github.com/openai/codex/issues/25779)
> 会话状态无边界累积，导致应用冻结、上下文过多、活动 turn 控制丢失。该 issue 被标记为 meta-bug，关联多个下游问题，是桌面端体验的核心瓶颈。

**[#35259] Desktop 在等待/状态轮询期间反复进入模型，消耗大量额度**（8 评论）
作者：[dimasyankauskas](https://github.com/dimasyankauskas) | [链接](https://github.com/openai/codex/issues/35259)
> 在 Ultra 和多 agent 工作流中，模型仅为了等待或轮询终端状态就被反复调用，实测这类无意义 turn 占原始 token 消耗的 19.8%。直接关联用户的配额消耗痛苦。

**[#36396] 子代理 busy-waiting 烧掉一周配额：11 天会话中 6,932 次阻塞等待**（2 评论）
作者：[phyrexia](https://github.com/phyrexia) | [链接](https://github.com/openai/codex/issues/36396)
> 一个长会话中，子代理的阻塞等待消耗了账户总 token 用量的 71%，其中 23.7% 等待返回为空。作者指出问题不在配额计算，而是客户端把配额花在了无意义的等待上。这是配额问题方向的又一力证。

### 💥 功能故障

**[#31864] 所有 GPT-5.6 Sol turn 失败：MultiAgentV2 使用了保留的 collaboration.spawn_agent**（6 评论，14 👍）
作者：[spadaval](https://github.com/spadaval) | [链接](https://github.com/openai/codex/issues/31864)
> 受影响的会话中，每个请求在模型处理前就报错：`'collaboration.spawn_agent' is reserved for use by this model`。这会导致 MultiAgentV2 相关功能在 GPT-5.6 Sol 上完全不可用。

**[#36225] Windows 统一版应用启动崩溃："Invalid weekday string: MON"**（2 评论）
作者：[kevinwingz](https://github.com/kevinwingz) | [链接](https://github.com/openai/codex/issues/36225)
> 更新到新的 unified ChatGPT/Work/Codex 桌面应用后，主进程每次启动即崩溃，仅系统托盘进程存活。属阻断级启动故障。

### 📊 配额/计费争议

**[#36353] ChatGPT Plus 每周 Codex 用量计算疑似错误（24 小时内额度耗尽）**（6 评论）
作者：[abdoulbaribenhima](https://github.com/abdoulbaribenhima) | [链接](https://github.com/openai/codex/issues/36353)
> 用户订阅 Plus 后第一天下午开始使用，次日早上整个每周额度就已耗尽。若属实，涉及每周配额重置逻辑和后端计费系统的正确性。

**[#32540] Codex Reset 显示"Expires 7/12"却未使用即消失**（4 评论，3 👍）
作者：[sakuseishi-m](https://github.com/sakuseishi-m) | [链接](https://github.com/openai/codex/issues/32540)
> 用户存储的 Reset 额度在过期日前无故消失，引发对额度状态同步机制（尤其 Windows 端）的质疑。

## 4. 重要 PR 进展（Top 10）

**[#36373] 新增 `--approve-for-me` CLI 标志**（已合并）
[链接](https://github.com/openai/codex/pull/36373)
> 为 interactive 和 exec 命令新增自动审批标志，将审批请求路由到自动审查。配置为 `approval_policy="on-request"` + `workspace-write` 沙箱。对需要无人值守运行的高级用户非常实用。

**[#36374] 为 code mode 启用沙箱化 V8**（已合并）
[链接](https://github.com/openai/codex/pull/36374)
> Windows MSVC 仍在用非沙箱版 V8 预编译包，此 PR 直接启用 `v8_enable_sandbox` feature，补齐了 Windows 端的安全沙箱能力。

**[#36365] 为 MCP elicitation 添加严格自动审查**（已合并）
[链接](https://github.com/openai/codex/pull/36365)
> 识别 `codex_strict_auto_review` 标记，将标记的审批请求路由到自动审查器，且仅接受规范的自动审查结果，无用户提示时 fail closed。增强 MCP 场景下的安全边界。

**[#36361] 将 Cursor 管理的 skills 迁移到 Codex**（已合并）
[链接](https://github.com/openai/codex/pull/36361)
> 自动发现并导入 home 级 `skills` 和 `skills-cursor` 目录，仓库级迁移仅限 `skills`。这是与 Cursor 生态互操作的重要一步，降低用户迁移成本。

**[#36389] 强制所有线程历史的单写者所有权**（已合并）
[链接](https://github.com/openai/codex/pull/36389)
> 为 legacy 和 paginated 线程统一加上跨进程写者锁，避免多进程并发写同一线程导致的数据竞态。属于底层数据一致性加固。

**[#36380] 添加线程 section 管理 API**（已合并）
[链接](https://github.com/openai/codex/pull/36380)
> 新增 `threadSection/create|update|delete` app-server 方法，支持在 SQLite 中持久化自定义 section（UUIDv7 身份），并带裁剪与显示校验。为 UI 层的会话组织功能铺路。

**[#36384] 使用分页查询加载 turn 摘要**（已合并）
[链接](https://github.com/openai/codex/pull/36384)
> 此前加载摘要视图时为每个返回的 turn 单独发一次查询；现在直接 join 每个 turn 的首条用户消息和最后 agent 消息到分页查询中。减少 N+1 查询，提升大型会话的加载性能。

**[#36378] 优先从状态数据库加载本地会话选择器**（已合并）
[链接](https://github.com/openai/codex/pull/36378)
> 本地 resume/fork 列表改为优先读取 indexed state DB 元数据，远程工作区仍走原 store 逻辑。并保持跨分页时选择模式不变，优化了会话列表的启动速度。

**[#36393] 避免冗余文件系统探测**（已合并）
[链接](https://github.com/openai/codex/pull/36393)
> 一次性加载 `environments.toml`，仅当确认文件缺失时才回退默认环境；直接尝试连接默认 daemon socket，省去先检查 socket 路径再连接的额外步骤。细微但有效的性能改进。

**[#36402] 声明实验性插件搜索 API**（已合并）
[链接](https://github.com/openai/codex/pull/36402)
> 新增实验性 `plugin/search` 请求，包含搜索词、作用域、工作目录、游标和限制参数，返回分页的插件列表（含 marketplace 名称和可选本地路径）。这是插件生态的重要基础能力。

## 5. 功能需求趋势

从近期 Issues 中提炼出社区最关注的五个方向：

1. **配额/用量透明化与节约**（#35259、#36396、#36353、#32540）
   用户对"额度被无意义消耗"的不满集中爆发，核心诉求是：等待轮询不应计费、子代理不应 busy-wait、配额计算必须正确且展示清晰。

2. **Windows 平台体验补齐**（#30712、#36225、#26168、#35855、#27453）
   从启动崩溃、窗口泄漏到沙箱失效、项目丢失，Windows 端问题密度远高于其他平台。社区期待官方对 Windows 做一轮系统性修复。

3. **MCP 生态治理**（#30408、#36359、#36360、#36365）
   MCP 服务器进程泄漏引发内存灾难，同时 PR 侧正在重构 MCP 配置编辑、绑定目录和审查流程。MCP 正从"能跑"走向"跑得稳、跑得安全"。

4. **沙箱安全与可用性平衡**（#17459、#30712、#36398）
   Windows 沙箱下 HTTPS（Schannel）失败、apply_patch 失效等问题，迫使 agent 绕过沙箱执行，安全问题严峻。社区希望沙箱既安全又好用，而不是被绕过。

5. **子代理体验精细化**（#29649、#19186、#31864）
   用户希望子代理名称可自定义/动态生成、优先用户定义名称而非运行时昵称，同时 MultiAgentV2 在 GPT-5.6 Sol 上的兼容性 bug 亟待修复。

## 6. 开发者关注点

- **资源泄漏是头号信任杀手**：MCP 进程不清理（9GB+ RSS）、session 状态无界增长、线程历史并发写入，这些底层问题直接导致桌面端卡死、崩溃和上下文混乱，开发者对应用的长期稳定性信心受影响。
- **配额消耗争议持续发酵**：多个独立 issue 从不同角度指向同一问题——模型把大量额度花在"等待"而非"干活"上。#28969（60 秒自动解析）获得 185 个 👍，说明用户对"被迫中断"和"无效等待"的双向浪费都已无法忍受。
- **Windows 用户感到被忽视**：从沙箱、网络栈、窗口行为到应用启动，Windows 专属 bug 占比极高且修复进度缓慢。社区对 Windows 端的质量控制有强烈提升预期。
- **安全边界不可妥协**：开发者明确反感因工具 bug 导致的沙箱绕过（如 #

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# 🤖 Gemini CLI 社区动态日报 — 2026-08-01

## 📌 今日速览

项目今日发布 v0.53.1（稳定版）与 v0.54.0-preview.1（预览版）两个补丁版本，共同包含 InvalidStreamError 细节向 UI 层传播的修复，其中稳定版 cherry-pick 存在冲突待手动解决。社区讨论热度集中在 Subagent 可靠性上（挂起、误报成功、不主动调用 Skills），同时安全侧迎来两项重要 PR（SSRF 修复与 MCP OAuth Token 刷新修复）。

---

## 🚀 版本发布

### v0.53.1（稳定版）
- **内容**：cherry-pick 提交 f47d6c6（对应 PR #28566，InvalidStreamError 细节向 UI 传播）至 v0.53.0，生成补丁版本。
- **注意**：该 cherry-pick 出现合并冲突，需手动解决。
- 🔗 [查看 Release](https://github.com/google-gemini/gemini-cli/releases/tag/v0.53.1) | [Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.53.0...v0.53.1)

### v0.54.0-preview.1（预览版）
- **内容**：将同一修复（f47d6c6）打入 v0.54.0-preview.0，生成 v0.54.0-preview.1。
- 🔗 [查看 Release](https://github.com/google-gemini/gemini-cli/releases/tag/v0.54.0-preview.1) | [Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.53.0...v0.54.0-preview.1)

> 💡 **解读**：PR #28566 的核心改动是将 `InvalidStreamError` 的 `type` 和 `message` 从核心层传递到 CLI UI，从而能向用户展示具体建议（例如提示使用 `/compress` 以降低上下文）。本次跨两个版本线同步，说明其重要程度较高。

---

## 🔥 社区热点 Issues

以下为过去 24 小时更新最活跃的 10 个 Issue（按评论数排序）：

### 1. #22323 — Subagent 超过 MAX_TURNS 后被误报为 GOAL 成功 ⚠️ P1
- **现象**：`codebase_investigator` 子代理在未做任何分析时就触发了最大轮次限制，但最终状态被报告为 `success` / `Termination Reason: "GOAL"`，完全掩盖了中断事实。
- **为什么重要**：误导性的成功信号会让用户基于错误结果做决策，是 Agent 可信度的严重缺陷。
- 📝 12 条评论 | 👍 2
- 🔗 [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22323)

### 2. #21409 — Generalist Agent 挂起 ⚠️ P1
- **现象**：一旦 `gemini-cli` 转交给 generalist agent，就会永久挂起（用户最长等待 1 小时）。即使创建文件夹这类简单操作也会触发。用户可通过指示模型不要转交子代理来规避。
- **为什么重要**：8 个 👍 表明受影响的用户较多，且直接阻断核心工作流。
- 📝 8 条评论 | 👍 8
- 🔗 [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21409)

### 3. #19873 — 利用模型的 Bash 原生能力：零依赖 OS 沙箱 ✨ P2
- **核心诉求**：Gemini 3 模型天然擅长链式使用 POSIX 工具（`grep`/`cat`/`sed`/`awk`），建议通过零依赖 OS 沙箱 + 执行后意图路由，在保证安全的前提下释放模型这一能力。
- **为什么重要**：代表了社区对"发挥模型原生能力"与"安全沙箱"结合的探索方向。
- 📝 8 条评论 | 👍 1
- 🔗 [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/19873)

### 4. #24353 — 稳健的组件级评估 ⚠️ P1
- **内容**：作为行为评估体系的后续 EPIC，已有 76 个行为评估测试，覆盖 6 个支持的 Gemini 模型，希望进一步推进到组件级。
- **为什么重要**：评估体系是保障 Agent 行为质量的基础设施，直接影响所有后续迭代。
- 📝 7 条评论
- 🔗 [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/24353)

### 5. #22745 — 评估 AST 感知的文件读取/搜索/映射影响 ✨ P2
- **内容**：EPIC 跟踪一系列调研，评估 AST 感知工具能否通过单次调用精确读取方法边界、减少 Token 噪声、改善代码库导航。
- **为什么重要**：AST 感知有望从底层提升代码理解和编辑效率。
- 📝 7 条评论 | 👍 1
- 🔗 [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22745)

### 6. #21968 — Gemini 不会主动使用 Skills 和 Sub-agents ✨ P2
- **现象**：即使配置了 `gradle`、`git` 等技能，模型也不会自主调用，必须显式指示才使用。
- **为什么重要**：Skills 是用户扩展 CLI 能力的关键机制，模型不主动使用会使其价值大打折扣。
- 📝 6 条评论
- 🔗 [查看 Issue](https://github.com/google

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**2026-08-01** | 数据来源：[github.com/github/copilot-cli](https://github.com/github/copilot-cli)

---

## 1. 今日速览

- 发布 **v1.0.78-0**（距离 v1.0.77 仅隔一天），新增 `/permissions` 批准模式切换、ACP `closeSession` 支持，并引入沙箱缓存配置 `allowDevToolCaches`
- 社区集中反馈 **plan 模式回归**（#4188）与 **autopilot 强制执行覆盖用户指令**（#4318）两大痛点，另有多个新 issue 指向 **计划审查挂起** 与 **会话恢复空白**
- 数据中出现了 `.mcp.json` 注释不被支持、未文档化的 `.security-key` 文件等工程化/隐私问题，反映

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-08-01）

## 今日速览
过去 24 小时无新版本发布，但有一项重要的社区 PR 提交：修复工具调用参数双重 JSON 编码问题（#2572）。Issue 方面，跨会话记忆系统（#1283）仍是社区讨论最热烈的话题，同时一个新的滚动输出体验 Bug（#2422）获得开发者关注。

## 版本发布
无新版本发布。

## 社区热点 Issues
> 数据说明：过去 24 小时仅更新 3 条 Issue，以下为完整清单。

### 1. [Feature Request] Memory System - Persistent context across sessions（#1283）
- **状态**：Open | 作者：@CatKang | 更新：2026-07-31 | 评论：8 | 👍：0
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/1283
- **为什么值得关注**：这是已持续 5 个月的高讨论度功能需求，要求实现跨会话的持久化记忆系统，涵盖 AI 自动记忆（项目模式、上下文笔记）与手动记忆（用户自定义指令）。近期再次更新说明社区对该特性的呼声未减，且讨论数量（8 条）已属活跃水平，是产品团队需要重点评估的方向。

### 2. [Bug] 对话完成后滚动查看输出会自动调到底部（#2422）
- **状态**：Open | 作者：@venus0707 | 更新：2026-07-31 | 评论：2 | 👍：1
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2422
- **为什么值得关注**：影响 1.46.0 版本，在 Linux 桌面环境 + kimi2.6 模型下，用户完成对话后想回看长输出时，滚动操作会被强制拉回底部，属于干扰核心工作流（代码审查、日志回看）的交互缺陷。已有 1 个 👍，说明并非个例，需要前端/TUI 团队尽快复现修复。

### 3. [Closed] error: the message at position 1 with role（#796）
- **状态**：Closed | 作者：@bravery | 更新：2026-07-31 | 评论：1 | 👍：0
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/796
- **为什么值得关注**：旧版 KimiCLI/1.3 在 macOS 上调用 kimi-for-coding 时出现的 provider 400 角色错误，今日被关闭，说明该问题已被修复或标记为重复。对开发者而言是正向信号——早期兼容性 bug 正在收敛。

## 重要 PR 进展
> 数据说明：过去 24 小时仅更新 1 条 PR，以下为完整内容。

### [PR #2572] fix(kosong): recursively unwrap double-encoded JSON in tool-call arguments
- **状态**：Open | 作者：@aalhadxx | 更新：2026-07-31 | 评论：暂无
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2572
- **功能/修复**：当供应商（如 Moonshot API）对 `function.arguments` 中的嵌套数组/对象做二次 JSON 编码时，`SetTodoList`、`ExitPlanMode`、`StrReplaceFile` 等工具调用会触发 Pydantic 校验错误。此 PR 递归解包双重编码的 JSON，显著改善多 provider 场景下的工具调用兼容性——这是影响实际 agent 工作流的关键修复，建议保持关注审阅进展。

## 功能需求趋势
从近期 Issue 和 PR 动态中，社区最关注的功能方向集中在：

1. **跨会话持久记忆**（#1283）：希望 CLI 能记住项目模式、用户偏好，实现自动 + 手动的记忆管理。这是对编码助手从“会话级”走向“项目级”的显性需求。
2. **工具调用健壮性与多 provider 适配**（#2572）：开发者在使用非默认模型/API 时，对嵌套 JSON 的解析容错有较高要求，防止工具调用因数据格式边缘情况失败。
3. **终端交互体验精细化**（#2422）：输出回看、滚动行为等基础交互仍存在高频痛点，社区期待更稳定的 TUI 行为。

## 开发者关注点
- **输出区交互稳定性**：目前至少有 1 个活跃 Issue 反映滚动回看被强制拉到底部，直接影响长上下文场景下的使用效率。
- **模型错误处理透明度**（#796）：早期版本中 provider 返回 400 角色错误的信息不够直观，社区希望错误提示能更明确地指向参数或角色配置问题。
- **旧问题关闭节奏**：今日 #796 被关闭，从 1 月至今耗时约 6 个月，开发者可能期待对已知 issue 的响应更及时，尤其是那些影响早期用户的问题。

---
*本文数据来自 GitHub MoonshotAI/kimi-cli 仓库公开信息，统计时间截至 2026-08-01 00:00 UTC。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

好的，这是 2026 年 8 月 1 日的 OpenCode 社区动态日报。

---

## OpenCode 社区动态日报 — 2026-08-01

### 今日速览

1. **OpenCode Go 服务端故障持续发酵**：[#38257](https://github.com/anomalyco/opencode/issues/38257) 中关于 Go 订阅所有模型返回 401 的问题已有 42 条评论，成为当前最热门故障，用户抱怨服务端故障频发。
2. **新模型支持呼声高涨**：DeepSeek V4 Flash 正式版发布后，社区立刻在 [#39823](https://github.com/anomalyco/opencode/issues/39823) 中询问何时登陆 OpenCode Go/Zen。
3. **核心代码库出现大规模清理**：`opencode-agent[bot]` 提交了 20 余个重构 PR，专注于删除无用代码和依赖，表明项目在功能开发之外正在积极进行内部代码卫生治理。

### 社区热点 Issues

本周社区讨论焦点主要集中在服务稳定性、新模型支持和核心体验优化上。

1. **[Bug] OpenCode Go: 返回 401 "Request blocked by upstream provider"** — [#38257](https://github.com/anomalyco/opencode/issues/38257)
   - **热度**：42 评论 / 11 👍 | **状态**：开放
   - **详情**：用户反馈从 7 月 22 日起，Go 订阅下所有模型的 `chat/completions` 均返回 401，但 `/v1/models` 正常。该问题被认定为服务端故障，已持续超过一周，严重影响了付费用户体验。

2. **[Feature] DeepSeek V4 Flash 正式版在 Go/Zen 上可用了吗？** — [#39823](https://github.com/anomalyco/opencode/issues/39823)
   - **热度**：22 评论 / 20 👍 | **状态**：开放
   - **详情**：社区对 DeepSeek-V4-Flash-0731 正式版的 Agent 能力提升（如 Terminal Bench 82.7）表现出极大兴趣，用户急切希望官方确认在 OpenCode Go/Zen 上的上线时间。

3. **[Bug] TUI 黑屏问题再次出现** — [#10221](https://github.com/anomalyco/opencode/issues/10221)
   - **热度**：33 评论 / 17 👍 | **状态**：已关闭
   - **详情**：尽管该问题已关闭，但 33 条评论和 17 个赞表明这是 TUI 历史上最严重且低频复现的 Bug 之一。另一类似问题 [#4140](https://github.com/anomalyco/opencode/issues/4140) 也有 37 条讨论，说明黑屏问题在不同版本中反复出现，严重影响了用户信任。

4. **[Feature] 允许在 TUI 中选择文本** — [#927](https://github.com/anomalyco/opencode/issues/927)
   - **热度**：13 评论 / 29 👍 | **状态**：已关闭
   - **详情**：该问题自 2025 年提出至今仍被高频点赞，是本季度最受关注的 UI/UX 改进项。用户希望能在 TUI 中直接复制 Prompt、输出和错误信息。

5. **[Feature] 插件/代理/技能市场** — [#28696](https://github.com/anomalyco/opencode/issues/28696)
   - **热度**：6 评论 / 23 👍 | **状态**：开放
   - **详情**：社区对统一的市场/注册表（Marketplace/Registry）需求强烈，希望以此解决插件、Agent 和技能的发现、安装与分发问题。

6. **[Feature] 撤销 Go 隐私措辞与供应商归属的静默移除** — [#39875](https://github.com/anomalyco/opencode/issues/39875)
   - **热度**：4 评论 / 20 👍 | **状态**：开放
   - **详情**：付费用户对 OpenCode 在近期更新中“静默”改变隐私政策条款和移除模型供应商归属信息表示担忧，要求增加遥测和保留策略的透明度。该话题是 Go 订阅用户信任度下降的信号。

7. **[Bug] session/update 通知在 end_turn 后发送** — [#17505](https://github.com/anomalyco/opencode/issues/17505)
   - **热度**：15 评论 / 10 👍 | **状态**：开放
   - **详情**：ACP（Agent Client Protocol）集成方反馈时序问题，导致客户端会在收到 `end_turn` 后展示不完整内容。这说明 ACP 协议适配仍不稳定，影响下游生态发展。

8. **[Bug] “exiting loop” 消息烦扰** — [#38801](https://github.com/anomalyco/opencode/issues/38801)
   - **热度**：19 评论 / 0 👍 | **状态**：开放
   - **详情**：用户以讽刺口吻抱怨反复出现的 "exiting loop" 错误，导致其对 TUI 失去信心。该问题虽点赞数不多，但从评论数量看，是许多用户在使用第三方 OpenAI API 时的常见痛点。

9. **[Bug] Qwen 3.6 35b-a3b 裸工具调用导致进程挂起** — [#24316](https://github.com/anomalyco/opencode/issues/24316)
   - **热度**：20 评论 / 2 👍 | **状态**：开放
   - **详情**：用户报告在使用 llama.cpp 本地部署的 Qwen 3.6 模型时，控制台出现裸工具调用标记，导致 Agent 运行暂停。这体现了本地模型与 OpenCode 工具调用解析的兼容性问题。

10. **[Bug] 自定义 OpenAI 兼容 provider 流式工具调用报错** — [#26412](https://github.com/anomalyco/opencode/issues/26412)
    - **热度**：10 评论 / 2 👍 | **状态**：开放
    - **详情**：在使用 vLLM 后端时，所有工具调用（Read/Edit/Bash）因 `Expected 'function.name' to be a string` 失败。该问题阻塞了自建模型服务的用户，是开源社区路线图上的关键卡点。

### 重要 PR 进展

1. **[修复] 长连接流式响应 SSE 静默中断问题** — [#39970](https://github.com/anomalyco/opencode/pull/39970)
   - **重要性**：高。修复网关长时间无响应时客户端“假死”的问题，对依赖流式输出的实际体验有显著提升。

2. **[修复] 保留 Provider 错误状态** — [#39976](https://github.com/anomalyco/opencode/pull/39976)
   - **重要性**：高。优化了错误分类机制，将“Payload 过大”区别于“模型上下文溢出”，有助于用户更快定位报错原因。

3. **[重构] 统一 Prompt 缓存配置** — [#39965](https://github.com/anomalyco/opencode/pull/39965)
   - **重要性**：中高。将 `none`、自动模式和显式模式整合为统一配置，并优化缓存 key，可能大幅降低用户在 OpenAI Responses 和 OpenRouter 通道下的使用成本。

4. **[功能] 按 Agent 覆盖全局 subagent_depth 配置** — [#37226](https://github.com/anomalyco/opencode/pull/37226)
   - **重要性**：中。允许在 Agent 的 `.md` 前置元数据中配置独立的递归深度上限，对管理复杂多智能体任务的团队非常有用。

5. **[功能] 本地局域网 (LAN) Provider 自动发现** — [#27554](https://github.com/anomalyco/opencode/pull/27554)
   - **重要性**：中。结合 mDNS 实现局域网内 OpenAI 兼容服务器的一键发现与模型自动加载，是私有化部署和本地开发环境的杀手指纹。

6. **[主题] 导出 expandTheme 公共 API** — [#39967](https://github.com/anomalyco/opencode/pull/39967)
   - **重要性**：低中。完善了主题包的公共接口导出，方便主题开发者复用工具函数。

7. **[清理] 移除 MoveSession 控制面服务及相关测试** — [#39974](https://github.com/anomalyco/opencode/pull/39974)
   - **重要性**：低。V2 控制面中未使用的服务被移除，从侧面反映项目在重构过程中对废弃代码的及时清理。

8. **[清理] 移除 Core 中无用的 semver 和 sqlite 依赖** — [#39973](https://github.com/anomalyco/opencode/pull/39973)
   - **重要性**：低。跟随 AI 辅助的大规模代码清理浪潮，有助于减少安装体积和潜在安全面。

9. **[清理] 移除未使用的 `stopVoice` 和 `AudioVoice` 类型** — [#39969](https://github.com/anomalyco/opencode/pull/39969)
   - **重要性**：低。TUI 音频模块的冗余代码清理，包含 590 个通过测试的验证成果。

10. **[清理] 移除生产环境未使用的 `formatDuration` 和 revert diff 解析器** — [#39964](https://github.com/anomalyco/opencode/pull/39964)
    - **重要性**：低。与上面类似，这类 PR 虽小，但代表了当前 OpenCode 社区对核心库瘦身和工程质量的高频投入。

### 功能需求趋势

- **新模型支持**：DeepSeek V4 Flash、GPT-5.6-Luna、Qwen 3.7 Max 等新模型的支持是当前最关键需求。社区不仅在等待模型本身，更关注在 OpenCode Go/Zen 上的可用性、稳定性与计费合理性。
- **插件生态建设**：从 #28696 的市场需求到 #37226 的 Agent 深度配置，社区正在经历从“单体工具”向“可插拔生态”演进的阵痛期，统一的包管理和发现机制成为必然诉求。
- **隐私与透明性**：Go 订阅用户的隐私担忧（#39875）反映出社区对模型提供方和数据流处理的透明度要求越来越高。
- **可访问性与 UI 优化**：文本选择（#927）、TUI 黑屏（#10221）反复出现、子代理 Token 计数（#39880）等细节问题依旧是开发者高频吐槽的点。

### 开发者关注点

- **服务稳定性**：OpenCode Go/Zen 服务端连续出现 401、计费异常（#36399）、订阅撤销（#39895）等问题，极大地透支了用户信任。付费用户对服务可靠性和计费透明度的容忍度正在快速下降。
- **TUI 遗留问题复发**：黑屏、“exiting loop”、输入区被遮挡（#38773）等问题在不同版本中反复出现，说明 TUI 重构压力大，低版本兼容性测试或需加强。
- **流式响应质量**：除了 SSE 中断（#39970）外，`gpt-5.6-luna` 的重复输出和内容截断（#39881）引发的讨论较多，用户对生成质量的期望值也在提升。
- **会话数据完整性**：SQLite 约束失败（#39165）和会话更新时序错误（#17505）暴露了核心数据层和 ACP 协议适配上仍有隐患，这会阻碍需要可靠会话恢复的复杂工作流。
- **国际化与文档完善**：[#39925](https://github.com/anomalyco/opencode/issues/39925) 反馈中文汉化不完整，以及 [#39904](https://github.com/anomalyco/opencode/issues/39904) 声称找不到已购买的 Go API，从侧面说明文档指引和多语言支持还有提升空间。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*