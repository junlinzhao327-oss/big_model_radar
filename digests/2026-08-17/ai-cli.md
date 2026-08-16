# AI CLI 工具社区动态日报 2026-08-17

> 生成时间: 2026-08-16 22:41 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-08-17）

> 数据来源： Claude Code、OpenAI Codex、Gemini CLI、GitHub Copilot CLI、Kimi Code CLI、OpenCode、Qwen Code 的 GitHub 社区动态摘要。  
> 口径说明：以下 Issue/PR 数量为各仓库当日动态中可统计的提及条目，并非仓库完整总量。

---

## 1. 生态全景

当前 AI CLI 工具已从“单点可用”进入“规模化落地”阶段，但社区反馈高度聚焦在稳定性与可控性：上下文丢失、后台 Agent 静默失败、MCP/插件集成故障、跨平台兼容问题集中爆发。各家都在快速迭代基础设施——Codex 在重构 TUI 与沙箱，Gemini 在修复 subagent 状态上报，Copilot 在处理 MCP 回归，OpenCode 在治理 V2 资源泄漏。整体态势是：模型能力竞争趋缓，工程可靠性、生态集成与安全边界成为新的主战场。

---

## 2. 各工具活跃度对比

| 工具 | Issues（当日提及/精选） | PR（当日提及） | Release |
|---|---|---|---|
|

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告

**数据源**: github.com/anthropics/skills | **统计截止**: 2026-08-17
**样本**: 50 条 PR + 50 条 Issue（按社区互动量排序，当前展示的 PR 全部处于 OPEN 状态）

---

## 一、热门 Skills 排行

**1. skill-creator 评估链路修复**
- **PR**: [#1298](https://github.com/anthropics/skills/pull/1298)
- **功能**: 修复 `run_eval.py` 对所有描述一律报 `recall=0%` 的严重故障，同时覆盖 Windows 子进程流读取、触发检测逻辑与并行 worker。
- **讨论热点**: 评论量居首，直接回应 Issue #556（12 评论、7 👍）。社区共识是：描述优化循环一直在"优化噪声"，评估工具已失真。
- **状态**: OPEN

**2. document-typography 新 Skill**
- **PR**: [#514](https://github.com/anthropics/skills/pull/514)
- **功能**: 对 AI 生成文档做排版质量控制，覆盖孤词换行（1-6 词溢出到下一行）、孤立段落标题、编号错位三类高频问题。
- **讨论热点**: "用户很少主动要求排版质量"——讨论聚焦于这类隐性质量缺陷是否值得沉淀为 Skill。
- **状态**: OPEN

**3. pdf SKILL.md 大小写引用修复**
- **PR**: [#538](https://github.com/anthropics/skills/pull/538)
- **功能**: 修复 `skills/pdf/SKILL.md` 中 8 处大小写不一致（`REFERENCE.md`→`reference.md` 等），解决 Linux/macOS 等大小写敏感文件系统上的 Skill 加载失败。
- **讨论热点**: 简单明确的 bug 修复，反映了官方 Skill 自身质量审查的必要性。
- **状态**: OPEN

**4. ODT（OpenDocument）新 Skill**
- **PR**: [#486](https://github.com/anthropics/skills/pull/486)
- **功能**: 支持 .odt/.ods 文件的创建、模板填充、读取及 ODT→HTML 转换，覆盖 LibreOffice 与 ISO 标准办公文档场景。
- **讨论热点**: 社区对 docx 之外"第二个办公文档格式"的期待较高，与既有 pdf/docx Skill 形成生态互补。
- **状态**: OPEN

**5. skill-quality-analyzer 与 skill-security-analyzer 元技能**
- **PR**: [#83](https://github.com/anthropics/skills/pull/83)
- **功能**: 新增两个元 Skill——分别从结构/文档/示例/可执行性等五维度评估 Skill 质量，以及检测 Skill 的安全风险。
- **讨论热点**: 与 Issue #492（安全信任边界）形成呼应，社区关注 Skill 生态的"质检"与"安检"基础设施。
- **状态**: OPEN

**6. self-audit 推理质量门 Skill**
- **PR**: [#1367](https://github.com/anthropics/skills/pull/1367)
- **功能**: 交付前先做机械性文件校验，再按损害严重度对输出做四维度推理审计

---

# Claude Code 社区动态日报 — 2026-08-17

> 数据来源：[github.com/anthropics/claude-code](https://github.com/anthropics/claude-code) · 覆盖时段：2026-08-16 更新动态

## 今日速览

昨日无新版本发布，社区讨论焦点集中在两个核心问题：上下文压缩导致 `.claude/project-context.md` 指令丢失（#9796，27 条评论）以及 Telegram 插件在所有会话中强制自动加载（#38098，24 条评论）。此外，两条安全相关的 PR 修复了 glob 匹配语义和 YAML frontmatter 解析问题，值得关注。

## 社区热点 Issues

以下按关注度精选 10 条昨日活跃的 Issue：

**1. Context compaction 抹除 project-context.md 指令** ⚠️ 核心功能
[#9796](https://github.com/anthropics/claude-code/issues/9796) · 👤 @nickfox · 💬 27 评论 · 已关闭
上下文压缩（Context compaction）会丢失 `.claude/project-context.md` 中的项目指令，影响长会话中的行为一致性。作为评论数最高的 Issue，社区反响强烈。

**2. Telegram 插件在所有会话中自动加载** ⚠️ 插件机制
[#38098](https://github.com/anthropics/claude-code/issues/38098) · 👤 @neuralneeraj · 💬 24 评论 · 已关闭
Telegram 插件未按预期仅在 `--channels` 会话中启用，而是全量加载。社区期望插件支持更细粒度的会话级隔离。

**3. 请求向 Claude 暴露结构化时间戳** ✨ 增强建议
[#49084](https://github.com/anthropics/claude-code/issues/49084) · 👤 @pleasedodisturb · 💬 14 评论
Claude Code 会话中缺少时间概念，无法感知消息/工具调用间隔、计算持续时间或检测过期状态。若实现，将显著增强时间感知推理能力。

**4. 后台代理空闲且未发送最终 SendMessage 报告**
[#74113](https://github.com/anthropics/claude-code/issues/74113) · 👤 @lebaige · 💬 11 评论 · 状态：开启
Windows 上后台代理频繁进入空闲状态，最终报告未投递，需 re-ping 才能恢复。影响 agent 工作流的可靠性。

**5. Cowork 跨平台同步故障导致对话和聊天记录消失**
[#81658](https://github.com/anthropics/claude-code/issues/81658) · 👤 @HSBE31 · 💬 11 评论 · 状态：开启
Desktop/Web/Android 三端同步失败，疑似服务端事故。对依赖多端衔接的开发者影响较大。

**6. Chrome 集成回归：交互式 CLI 的 Chrome MCP 客户端无法启动**
[#84814](https://github.com/anthropics/claude-code/issues/84814) · 👤 @jadshaker · 💬 2 评论 · 状态：开启
作者测试了 2.1.212（正常）→ 2.1.220/224/228（均异常），定位到明确回归点，适合工程团队快速排查。

**7. Workflows 右侧面板静默截断代理列表**
[#71515](https://github.com/anthropics/claude-code/issues/71515) · 👤 @kumaakh · 💬 3 评论 · 状态：开启
当阶段含 5 个以上 agent 时，右栏仅显示“最近 9 个”的滑动窗口，与左栏计数器不一致，属可见性缺陷。

**8. 终端焦点事件被误判为权限对话框的“拒绝”**
[#72188](https://github.com/anthropics/claude-code/issues/72188) · 👤 @dwalend · 💬 3 评论 · 已关闭
终端重新获得焦点时发送的 focus-in 事件被 TUI 权限输入处理器消费，导致误拒绝；影响 IntelliJ 系 IDE 内嵌终端。

**9. PyCharm Terminal 滚动失效**
[#74781](https://github.com/anthropics/claude-code/issues/74781) · 👤 @sgallant17 · 💬 3 评论 · 状态：开启
Linux 下 PyCharm 终端内 Claude Code TUI 滚动行为异常，IDE 集成兼容问题持续积累。

**10. 从终端滚动缓冲区复制内容时丢字符**
[#74815](https://github.com/anthropics/claude-code/issues/74815) · 👤 @akuney · 💬 2 评论 · 状态：开启
屏幕渲染完整，但鼠标选中复制后会丢失中段字符，影响代码/报错信息的复制体验。

## 重要 PR 进展

昨日共 3 条 PR 更新：

**1. 修复 security-patterns glob 语义：`**` 改为可匹配零深度路径** 🛡️ 安全相关
[#87079](https://github.com/anthropics/claude-code/pull/87079) · 👤 @anishsamant
将 `_glob_match` 从 `fnmatch` 语义纠正为 glob 语义——原实现下 `**/*.ts` 无法匹配顶层文件，导致安全规则被静默绕过。对安全规则而言这是 silent failure，修复意义重大。

**2. 修复 PR Review Toolkit 中全部 agent 的无效 YAML frontmatter**
[#87077](https://github.com/anthropics/claude-code/pull/87077) · 👤 @anishsamant
agent 的描述是未加引号的标量，其中包含 `Daisy: "..."` 这类会被 YAML 解析为嵌套映射的文本，导致 frontmatter 为空（name/description 丢失）。修复后 agent 可正确加载。

**3. 新增 Python Conda 包构建工作流**
[#87125](https://github.com/anthropics/claude-code/pull/87125) · 👤 @Salamyamadi
新增 `python-package-conda.yml`，为仓库补充 Conda 包构建的 CI 配置（含 commit hash，属基础设施类改动）。

## 功能需求趋势

从昨日活跃 Issues 中提炼的社区最关注方向：

- **时间感知能力**（#49084）：呼声最高的增强点，让模型能够感知会话时长、工具调用间隔和状态过期，属于基础能力补全。
- **插件/工具的会话级隔离**（#38098）：社区需求从“能用”走向“可控”——按频道、按项目、按会话精细管控插件与工具的加载范围。
- **跨平台/多端同步可靠性**（#81658）：Cowork 桌面端/Web/移动端同步问题凸显了多端工作流的刚性需求。
- **可配置的 UI 元素**（#65396）：用户期望能隐藏使用量限制警告横幅等占用注意力的界面元素。
- **子代理（agent）任务可观测性**（#74113、#71515）：后台代理报告丢失、流程视图截断，表明代理运行状态的可视化与可靠性亟需加强。

## 开发者关注点

**高频痛点**

- **安全过滤器的误报问题**（@sworrl 系列：#72337、#72328、#72351 等）：多起合法安全研究/逆向工程工作被服务端安全过滤器中断，用户反馈“session-halted”级误报，对专业安全开发者影响严重。
- **后台代理任务可靠性**（#74113）：代理空闲不返回最终报告，需要手动 re-ping，浪费 token 且打断工作流。
- **终端集成兼容性**（#74781、#72188）：PyCharm 滚动失效、IntelliJ 焦点事件冲突，IDE 内嵌终端体验仍是短板。
- **TUI 文本选择/复制缺陷**（#74815）：渲染完整但复制丢字符，直接影响日常开发复制粘贴效率。
- **失败任务仍被计费**（#72278）：`/ultrareview` 失败但消耗免费运行次数，引发对计费透明度的讨论。

**文档缺口（昨日新增 3 条）**

- PowerShell 工具后代进程继承 pwsh 7 的 PSModulePath，破坏 Windows PowerShell 5.1 模块加载（[#84431](https://github.com/anthropics/claude-code/issues/84431)）
- Hook 参考文档缺少 PowerShell 工具的 `tool_input` schema，导致 PreToolUse Hook 无法正确配置（[#83647](https://github.com/anthropics/claude-code/issues/83647)）
- 账单/税务文档缺少 VAT 号相关说明（[#84203](https://github.com/anthropics/claude-code/issues/84203)）

---

**一句话总结**：昨日属于“问题暴露期”——上下文丢失、插件失控、代理静默、同步故障集中浮现，而这些恰是开发者日常最依赖的能力；安全 glob 修复和 YAML 修复则提醒我们，工具链自身的基础设施质量同样值得关注。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-08-17）

## 今日速览

昨日社区焦点高度集中在 **Windows 平台体验问题**：多个高赞 Issue 持续追踪桌面应用卡顿、鼠标停滞与 WSL 路径混乱，用户反响强烈。同时，**CLI/TUI 基础设施重构** 成为 PR 主力，涉及工作目录切换、沙箱隔离与配置系统增强，并发布了 rust-v0.148.0-alpha.20 版本。

## 版本发布

### rust-v0.148.0-alpha.20
- 链接：https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.20
- 仅标注 `0.148.0-alpha.20`，未附带详细发布说明。作为核心 Rust 包的新 alpha，预计为后续 Codex CLI/Desktop 的不稳定通道更新铺路（建议关注关联 PR 以了解功能走向）。

## 社区热点 Issues

以下 10 个 Issue 最能反映当前社区讨论热度与核心痛点：

### 性能与卡顿相关（热度最高）
1. **#20214**：Codex App 在 Windows 11 Pro 上频繁冻结/卡顿（106 评论 / 85 👍）
   链接：https://github.com/openai/codex/issues/20214
   重要性：当前社区最关注的 Issue，用户反馈“尽管系统资源充足”依然卡顿，评论中大量复现报告与配置讨论。
2. **#38546**：Windows 桌面应用导致系统级鼠标光标停滞（31 评论 / 13 👍）
   链接：https://github.com/openai/codex/issues/38546
   重要性：严重影响日常操作的“系统级”问题，涉及无管理员权限运行时的光标卡顿，范围远超应用本身。

### 功能增强请求（高赞）
3. **#25319**：将 Codex VS Code 聊天范围限定到当前工作区/项目（28 评论 / 62 👍）
   链接：https://github.com/openai/codex/issues/25319
   重要性：62 个 👍 表明多项目开发者强烈的隔离需求，社区希望避免跨项目会话历史污染。
4. **#23200**：为 Codex 移动端支持无桌面在线的远程 Linux 主机（18 评论 / 48 👍）
   链接：https://github.com/openai/codex/issues/23200
   重要性：移动端作为控制层 + 常开 Linux 服务器是高频开发场景，社区支持度很高。
5. **#11765**：管理 MCP 服务器 UX 增强（5 评论 / 45 👍）
   链接：https://github.com/openai/codex/issues/11765
   重要性：希望在不修改 `config.toml` 的前提下实现 MCP 服务器的启用/禁用，适合团队协作场景。

### 明确 Bug 报告
6. **#28094**：WSL 下桌面应用将 `/home` 重写为 `C:\home`，导致项目关联丢失（26 评论）
   链接：https://github.com/openai/codex/issues/28094
   重要性：WSL 用户路径映射严重错误，导致会话关联中断和目录误报，复现稳定。
7. **#37487**：Codex CLI 0.147.0 向 Azure Responses API 发送空工具描述（12 评论）
   链接：https://github.com/openai/codex/issues/37487
   重要性：Azure 用户无法正常使用工具调用，阻断性较高。
8. **#28248**：Windows 沙箱在断电后所有读取操作报 “apply deny-read ACLs” 错误（11 评论）
   链接：https://github.com/openai/codex/issues/28248
   重要性：断电后沙箱 ACL 机制锁死，导致无法读取任何文件，数据安全性受损。
9. **#20864**：桌面应用扫描全部 `~/.codex/sessions` 文件导致卡顿（20 评论）
   链接：https://github.com/openai/codex/issues/20864
   重要性：明确指向性能瓶颈根因——未利用索引而是全量扫描 rollout 文件，Pro/企业用户受影响。
10. **#27928**：CLI `/review` 后续对话报 `Expected an ID that begins with 'msg'`（12 评论）
    链接：https://github.com/openai/codex/issues/27928
    重要性：Azure 配置下代码评审功能完全不可用，涉及 Azure OpenAI/Foundry 用户的实际阻断。

## 重要 PR 进展

过去 24 小时 PR 集中展示了 Codex 在 TUI 交互、沙箱安全、配置系统三方面的深度优化：

1. **#38894**：TUI 新增 `/cd` 工作目录切换命令
   链接：https://github.com/openai/codex/pull/38894
   内容：支持在保留会话历史的情况下切换本地会话工作目录，并自动重新加载项目配置。
2. **#38830**：将外部编辑器缓冲区与沙箱可写路径隔离
   链接：https://github.com/openai/codex/pull/38830
   内容：防止编辑器缓冲区被受限文件系统策略暴露为可写目录，提升沙箱安全性。
3. **#38827**：为 `codex doctor` 增加端点保护检测
   链接：https://github.com/openai/codex/pull/38827
   内容：自动检测 macOS/Windows 上常见端点保护产品，并提示需要验证的 Codex 排除项。
4. **#38902**：遵守按环境的 Shell 变量策略
   链接：https://github.com/openai/codex/pull/38902
   内容：区分每个环境的 `ShellEnvironmentPolicy`，保证 shell 命令与用户任务使用正确的环境策略。
5. **#38823**：避免超链接装饰时逐字符分配内存
   链接：https://github.com/openai/codex/pull/38823
   内容：改用栈缓冲区编码字符，消除每次分配的 `String` 临时对象，提升 TUI 渲染性能。
6. **#38822**：避免克隆 TUI 历史 span 内容
   链接：https://github.com/openai/codex/pull/38822
   内容：通过引用历史 span 内容减少内存拷贝，优化 TUI 长历史会话的内存占用。
7. **#38819**：为预留给线程 ID 提供元数据暂存支持
   链接：https://github.com/openai/codex/pull/38819
   内容：允许调用方在 Core 启动线程前关联宿主状态，并拒绝通过预留 ID 恢复已有线程。
8. **#38817**：TypeScript SDK 增加原始配置覆盖能力
   链接：https://github.com/openai/codex/pull/38817
   内容：支持 `configOverrides` 以 `--config key=value` 形式传递 TOML 配置，解决权限映射中字面路径键无法通过结构化 API 表示的问题。
9. **#38837**：跨 TUI 编辑器组件共享 keymap
   链接：https://github.com/openai/codex/pull/38837
   内容：聊天编辑器与内嵌文本域共享同一份 keymap 快照，自定义快捷键在组件间一致生效。
10. **#38893**：独立恢复线程时间戳最大值
    链接：https://github.com/openai/codex/pull/38893
    内容：分别加载 `updated_at_ms` 与 `recency_at_ms` 的持久化最大值，避免两个计数器相互覆盖。

## 功能需求趋势

综合全部 Issues 与 PR，社区最关注的功能方向如下：

- **Windows 平台稳定性与性能**：卡顿、鼠标停滞、沙箱 ACL 问题占比最高，且高赞 Issue 频出，表明 Windows 用户体验是当前最大短板。
- **远程与多机开发支持**：移动端控制远程 Linux 主机、VS Code Remote 远程历史一致性、桌面端 SSH 会话分组等需求持续升温。
- **会话与上下文精细化管理**：按项目/连接/线程三层组织会话、阻止不必要自动压缩、保留本地历史不被清理，社区对会话数据的掌控力提出了更高要求。
- **MCP 可管理性与扩展**：希望提供 UI 来管理 MCP 服务器（启用/禁用/配置），而非只依赖 `config.toml` 的团队协作式管理。
- **TUI/编辑器操作效率**：撤销/重做、快速切换模型与推理强度、工作目录切换、可自定义 keymap 等“编辑器体验”类需求保持活跃。

## 开发者关注点

从 Issue 与 PR 中可以提炼出开发者反馈的高频痛点：

- **Windows 性能问题呈系统性**：不仅 Codex 应用自身卡顿，还波及系统级鼠标；用户对“资源充足但卡顿”的反馈强烈，分析指向会话索引而非全量文件扫描。
- **WSL 路径处理一致性差**：`/home` 被误写为 `C:\home`、新建本地会话失败等问题，说明 WSL 支持仍欠打磨。
- **会话历史易丢失或损坏**：桌面端历史消失、远程 VS Code 会话重复/空白、线程 ID 错误等报告频发，开发者对会话连续性信任度下降。
- **沙箱与审批流在 Windows/远程场景下不灵活**：断电导致 ACL 锁死、远程 SSH 桌面端审批按钮失效、MCP 进程反复启动不被回收，影响自动化流程。
- **Azure 兼容性受阻**：空工具描述与 `msg` ID 错误让 Azure 用户无法使用工具调用与代码评审，企业级用户影响突出。

---

以上日报覆盖 2026-08-17 的 OpenAI Codex 社区主要动态，如需进一步跟踪，可关注对应 GitHub Issue/PR 的评论更新。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-17

> 数据来源：github.com/google-gemini/gemini-cli

## 今日速览

过去 24 小时，Gemini CLI 社区的讨论焦点集中在 **subagent 稳定性与行为透明度** 上：既有 `MAX_TURNS` 被误报为 `GOAL` 成功的状态上报缺陷，也有 generalist agent 无限挂起的老问题被反复提及。与此同时，**Auto Memory 安全性** 与 **MCP 工具 Schema 兼容性** 成为代码提交热点，多个 P1 修复 PR 正在推进。夜间版本 v0.56.0-nightly.20260816 已发布，主要包含常规改动。

---

## 版本发布

### v0.56.0-nightly.20260816.g2a87e7be1
- **类型**：Nightly 预发布版
- **变更范围**：详见 [Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260815.g2a87e7be1...v0.56.0-nightly.20260816.g2a87e7be1)
- **备注**：本次为滚动夜间构建，无独立功能公告；重点关注近期提交的 SSR Agent 自动修复项是否进入此版本。

---

## 社区热点 Issues（10 个）

### 1. Subagent 到达 MAX_TURNS 后被误报为 GOAL 成功
- **#22323** | [链接](https://github.com/google-gemini/gemini-cli/issues/22323)
- **关键信息**：`codebase_investigator` 等在超限后经最后一次恢复调用上报 `Termination Reason: "GOAL"`，实际并未完成分析。状态：`need-retesting`；评论 12 条，为过去 24 小时讨论量最高。
- **社区反应**：用户质疑任务完成的真实性，开发者已提交修复 PR（见下方 #28815）。
- **为何重要**：直接掩盖 agent 失败，可能导致用户对自动化结论产生错误信任。

### 2. Generalist agent 无限挂起
- **#21409** | [链接](https://github.com/google-gemini/gemini-cli/issues/21409)
- **关键信息**：自 v0.33.0 起，`gemini-cli` 转交 generalist agent 后频繁无限等待，用户最长等待 1 小时；显式禁用 subagent 可绕过。
- **社区反应**：获得 8 个 👍，是近期关注度最高的 bug 之一。评论 8 条。
- **为何重要**：基础路径的可靠性问题，影响所有依赖 subagent 的复杂任务。

### 3. 组件级评估体系（Component Level Evaluations）
- **#24353** | [链接](https://github.com/google-gemini/gemini-cli/issues/24353)
- **关键信息**：EPIC：在已有 76 个行为评估测试的基础上，建设更细粒度的组件级评估能力，覆盖 6 个受支持的 Gemini 模型。评论 7 条。
- **为何重要**：反映官方对 agent 质量保障体系的投入，是长期稳定性的基础设施。

### 4. AST 感知的文件读取、搜索与映射影响评估
- **#22745** | [链接](https://github.com/google-gemini/gemini-cli/issues/22745)
- **关键信息**：EPIC：评估通过 AST 感知工具实现精准读取方法边界、减少 token 噪声、优化导航与代码库映射的收益。评论 7 条。
- **为何重要**：探索 AI 编程工具的"下一级"代码理解能力，可能会显著改善大仓库场景下的上下文效率。

### 5. 模型不主动使用自定义 skills 与 subagents
- **#21968** | [链接](https://github.com/google-gemini/gemini-cli/issues/21968)
- **关键信息**：用户观察：即使配置了 `gradle`、`git` 等 skill，模型在相关任务中几乎从不主动调用，必须显式指令。评论 6 条。
- **社区反应**：偏向体验反馈，多位用户表示遇到同类现象。
- **为何重要**：直接关系 Gemini CLI 的自动化程度与生态价值（如 prompt 工程资产复用）。

### 6. Shell 命令执行完成但仍卡在 "Waiting input"
- **#25166** | [链接](https://github.com/google-gemini/gemini-cli/issues/25166)
- **关键信息**：执行完极简单的 CLI 命令后，TUI 仍显示命令运行中且等待输入，只能手动取消。评论 4 条，👍 3。
- **为何重要**：高频干扰，严重影响交互流畅度，属于核心体验痛点。

### 7. Auto Memory 对低信号会话无限重试
- **#26522** | [链接](https://github.com/google-gemini/gemini-cli/issues/26522)
- **关键信息**：后台提取 agent 判断某 session 为低价值并跳过时，该 session 仍留在待处理索引中，会被反复拉起重试。评论 5 条。
- **为何重要**：造成反复的无意义模型调用，浪费算力成本；Auto Memory 系列问题持续发酵。

### 8. Auto Memory 缺乏确定性脱敏且日志过多
- **#26525** | [链接](https://github.com/google-gemini/gemini-cli/issues/26525)
- **关键信息**：提取 prompt 虽然在语义上要求模型脱敏，但密文已先进入模型上下文；此外后台任务会记录已有 skill 内容等日志。评论 4 条。
- **为何重要**：安全与隐私类缺陷，对于企业级用户是关键关注点。

### 9. Browser subagent 在 Wayland 下失败
- **#21983** | [链接](https://github.com/google-gemini/gemini-cli/issues/21983)
- **关键信息**：Wayland 环境下 browser agent 以 `GOAL` 终止但实际功能不可用。评论 4 条。
- **为何重要**：Linux 桌面环境兼容性问题，影响面包括主流发行版。

### 10. 自 v0.33.0 起 subagents 在未授权情况下运行
- **#22093** | [链接](https://github.com/google-gemini/gemini-cli/issues/22093)
- **关键信息**：用户 agents mode 设置为 disabled，更新后 generalist 等 subagent 仍被自动调用。评论 3 条。
- **为何重要**：配置不生效属于权限控制缺陷，可能引发用户对 CLI 自主行为的失控感与安全担忧。

---

## 重要 PR 进展（10 个）

### 1. [SSR Agent] 防止 TUI 无限挂起：增加执行超时
- **#28812** | [链接](https://github.com/google-gemini/gemini-cli/pull/28812) | **P1**
- **内容**：修复 #21477：裸 Linux 终端下 `getProcessInfo()` 依赖 `execAsync` 执行 `ps`，异常时导致 "Initializing..." 卡死。增加超时保护。
- **意义**：直接解决终端初始化路径的稳定性问题。

### 2. [SSR Agent] 保留 subagent 恢复时的原始终止原因
- **#28815** | [链接](https://github.com/google-gemini/gemini-cli/pull/28815) | **P1**
- **内容**：修复 #22323：subagent 到达 `MAX_TURNS`/`TIMEOUT` 后在最终恢复轮成功调用 `complete_task` 时，应保留原始终止原因而非改写为 `GOAL`。
- **意义**：提升 agent 状态报告的可信度，与今日热点 issue 直接对应。

### 3. [SSR Agent] 更新性能测试的 ripgrep 导入
- **#28838** | [链接](https://github.com/google-gemini/gemini-cli/pull/28838) | **P1**
- **内容**：修复 `perf-tests/globalSetup.ts` 仍引用已删除的 `canUseRipgrep`，导致 nightly 性能测试在全局 setup 即中止的问题。
- **意义**：保障 CI 基础设施可持续运行。

### 4. 规范化 MCP 工具 Schema：确保根节点 `type: object`
- **#28839** | [链接](https://github.com/google-gemini/gemini-cli/pull/28839) | **P2**
- **内容**：MCP 服务器可能返回缺失 `type` 或结构非法的工具 schema，导致 Vertex AI（严格模式）等解析失败。此补丁在转发前做规范化。
- **意义**：提升与第三方 MCP 生态的兼容性，降低集成的隐性故障。

### 5. ACP：在 PromptResponse 中填充缓存与思考 token
- **#28840** | [链接](https://github.com/google-gemini/gemini-cli/pull/28840) | **P2**
- **内容**：修复 `_meta.quota` 仅返回 input/output tokens 的问题，补全 `cachedContentTokenCount` 和 thoughts token 计数。此前 ACP 客户端对重度缓存会话的成本估算偏高约 3 倍。
- **意义**：对依赖精确计费的 ACP 集成方（如网关、护栏工具）是重要修复。

### 6. A2A Server：深度合并嵌套设置，防止用户配置

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-17** | 数据来源：[github.com/github/copilot-cli](https://github.com/github/copilot-cli)

---

## 今日速览

今日社区更新 16 条 Issue、1 条 PR。最核心的动向是 **MCP（Model Context Protocol）认证与连接稳定性问题集中爆发**（#4490、#4463、#4472），1.0.80 版本存在明确回归；同时 **内存管理出现严重 bug**（#4506）：内存看门狗在上下文仅用 23% 时强制压缩，循环直到 OOM。插件更新文件锁、会话恢复后不可用也是开发者的高频痛点。

---

## 版本发布

过去 24 小时无新版本发布。当前版本线为 1.0.80，但多个 Issue 指向该版本在 MCP OAuth 认证、权限请求超时方面存在回归。

---

## 社区热点 Issues（10 个最值得关注）

### 1. [#4506] 内存压力看门狗在 23% 上下文使用率时强制压缩，循环直至 OOM
- **作者**: @jay-tau | 创建: 08-16 | 状态: 开放（triage）
- 长会话在上下文使用率仅 ~23% 时被触发强制压缩，每次仅恢复 0.003% token，随后循环压缩直到进程 OOM。触发源不是上下文压力而是**进程内存水位**，建议官方重新审视压缩触发策略。
- **链接**: https://github.com/github/copilot-cli/issues/4506

### 2. [#4490] Atlassian MCP OAuth 认证在 1.0.80 中破坏（RFC 8414 §3.3 回归）
- **作者**: @ChandrasekarCK | 创建: 08-14 | 状态: 开放
- 授权服务器对外声明的 issuer 与元数据发现 URL 不匹配，CLI 拒绝连接；该流程在 1.0.78 中正常。此问题直接影响所有 Atlassian MCP 用户，确认是版本升级引入的回归，需要优先修复。
- **链接**: https://github.com/github/copilot-cli/issues/4490

### 3. [#4472] 远程 MCP 并发工具调用在 token 刷新期间互相取消
- **作者**: @jmtt89 | 创建: 08-13 | 状态: 开放
- 当多个并发工具调用共享同一个已过期的访问令牌时，每个调用各自触发刷新并创建新的 `rmcp::service` 实例，导致在途调用全部中断（`transport closed before the tool responded`）。暴露的是 token 刷新流程缺乏并发的去重/共享控制。
- **链接**: https://github.com/github/copilot-cli/issues/4472

### 4. [#4463] Windows 平台 MCP OAuth 间歇性失败（socket error 10013）
- **作者**: @msosav | 创建: 08-12 | 状态: 开放
- Windows 特定问题：OAuth 授权流程尚未进入浏览器即因 socket 权限错误（错误码 10013）中断。该问题间歇性出现，标注了 `area:platform-windows`，Windows 用户受影响较大。
- **链接**: https://github.com/github/copilot-cli/issues/4463

### 5. [#4505] 恢复会话后所有提示失败：`400 input item ID does not belong to this connection`
- **作者**: @Adamkadaban | 创建: 08-16 | 状态: 开放（triage）
-

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

## Kimi Code CLI 社区动态日报 — 2026-08-17

> 本期数据范围：2026-08-16 更新（截至 2026-08-17 08:00 UTC）

---

### 1. 今日速览

过去 24 小时，Kimi Code CLI 仓库无新版本发布，但社区讨论活跃集中在三个方向：**Session 管理缺失**（#1783）、**Windows 路径兼容问题**（#2600）和**长期记忆层不足**（#1478）。另外，一个关于**定时任务无管理入口**的新 issue（#2605）在创建当日即被关闭，但用户诉求并未解决。

---

### 2. 版本发布

过去 24 小时无新 Release（最新版本仍为 0.33）。

---

### 3. 社区热点 Issues

*本期数据量有限（共 4 条更新），以下为全部值得关注的 Issue。*

#### 🔥 会话管理

**#1783 [Feature Request] 添加 /delete 命令删除 Session**
- 作者: @proccl | 创建: 2026-04-07 | 更新: 2026-08-16 | 💬 6 评论 | 👍 1
- **摘要**：请求新增 `/delete` 或 `/remove` 斜杠命令，用于直接删除 session，避免用户手动到 `~/.kimi/sessions/` 目录下删除文件夹。使用场景包括：session 列表过多、清理旧 session 释放磁盘空间、删除包含敏感信息的 session。
- **为什么重要**：这是社区长期诉求（4 月提出，8 月仍在更新），说明 Session 管理入口一直是用户刚需，但尚未被官方实现。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/1783

#### 🐛 Windows 兼容性

**#2600 [bug] Windows PowerShell7 从 D 盘启动时找不到路径**
- 作者: @RooKichenn | 创建: 2026-08-11 | 更新: 2026-08-16 | 💬 5 评论
- **摘要**：v0.33 版本下，当 PowerShell7 默认工作目录设置为 D 盘而非系统盘时，启动 kimi code 后无法找到正确路径。
- **为什么重要**：Windows 用户自定义 PowerShell 默认目录是常见操作，该 bug 影响使用体验，且已持续 5 天，说明可能涉及路径解析逻辑的深层问题。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2600

#### 🧠 记忆层

**#1478 [enhancement] 优化记忆层，大项目支持不足**
- 作者: @hahy36 | 创建: 2026-03-17 | 更新: 2026-08-16 | 💬 4 评论
- **摘要**：请求优化记忆层（memory layer），指出官方参考文档中仅见 `agent.md`，缺乏类似 `MEMORY.md`、`memory/` 目录等长期记忆机制，导致处理大型项目时上下文管理困难。作者还提供了其他工具的记忆层目录结构作为参考。
- **为什么重要**：3 月提出，8 月仍在讨论，可见记忆层设计是社区长期关注的核心痛点之一，对大型项目开发效率影响显著。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/1478

#### ⚠️ 定时任务管理（当日关闭）

**#2605 [CLOSED] 定时任务无用户可见的管理入口**
- 作者: @WilliamLambertCN | 创建: 2026-08-16 | 更新: 2026-08-16 | 💬 1 评论
- **摘要**：模型通过 `CronCreate` 工具创建的定时任务，在 TUI 中完全没有管理入口：无 `/cron` 命令，`/tasks` 面板也不显示定时任务。任务文件仅存在于 `~/.kimi-code/cron/<目录哈希>/<任务ID>.json`，用户无法通过界面查看或管理。
- **为什么重要**：虽然 issue 当日被关闭，但用户明确指出了工具能力（CronCreate）与用户界面管理能力之间的功能缺口，很可能被官方转向内部处理。
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2605

---

### 4. 重要 PR 进展

*本期仅有 2 个 PR 有更新，均来自同一位贡献者 @Ricardo-M-L。*

**#2324 [fix(web)] 修复 SessionProcess.send_message 中的 BrokenPipeError**
- 作者: @Ricardo-M-L | 创建: 2026-05-19 | 更新: 2026-08-16
- **摘要**：`src/kimi_cli/web/runner/process.py` 中的 `send_message` 方法在 `start()` 与写入 `process.stdin` 之间未检查子进程是否已退出，`drain()` 可能抛出 `BrokenPipeError`。该 PR 补充了防护逻辑。
- **价值**：修复 Web 模式下子进程退出竞态问题，提升稳定性。
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2324

**#2449 [fix(string)] 修复 shorten_middle 在长度检查前未去除换行符的问题**
- 作者: @Ricardo-M-L | 创建: 2026-06-13 | 更新: 2026-08-16
- **摘要**：`shorten_middle(text, width, remove_newline=True)` 用于 `extract_key_argument` 渲染单行摘要，但函数在短输入时会提前返回，未执行换行折叠逻辑，导致包含换行符的 key argument 仍以多行形式展示。
- **价值**：修复工具调用参数摘要显示异常，改善对话可读性。
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2449

---

### 5. 功能需求趋势

从当前 Issue 及近期讨论中，社区最关注的功能方向为：

1. **Session 管理能力** — 用户期望通过斜杠命令（如 `/delete`、`/remove`）直接管理会话，而非手动操作文件系统。（#1783）
2. **记忆层（Memory Layer）** — 官方尚未提供明确的长期记忆机制，社区希望有类似 `MEMORY.md` 或持久化记忆目录的结构来支持大型项目。（#1478）
3. **定时任务可视化** — 模型已具备创建定时任务（CronCreate）的能力，但缺少对应的 TUI 管理界面（如 `/cron` 命令或 `/tasks` 面板集成）。（#2605）
4. **跨平台路径兼容性** — Windows 下非默认工作目录启动时的路径解析问题，说明当前路径处理逻辑仍需适配更多系统配置。（#2600）

---

### 6. 开发者关注点

- **高频痛点**：
  - **手动文件操作负担**：Session 无法通过命令管理，用户被迫手动删除文件夹（#1783）。
  - **大项目上下文不足**：缺少长期记忆机制，项目规模变大后模型容易“失忆”（#1478）。
  - **功能可见性缺失**：后台任务（定时任务）创建后无入口查看/取消，用户对系统状态缺乏感知（#2605）。
  - **环境差异导致的不稳定**：Windows 下 PowerShell 非默认目录启动引发路径错误，影响开箱即用体验（#2600）。
- **整体反馈倾向**：用户对“后台能力”的管理入口要求日益增加，希望 CLI 能提供与“模型能做的事”（创建任务、管理 session 等)相匹配的“用户能用的操作界面”。

---

*本日报由 AI 自动生成，数据来自 GitHub 公开仓库，如有遗漏请以官方信息为准。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-17

> 数据来源：github.com/anomalyco/opencode | 分析时段：2026-08-16 更新内容

## 今日速览

过去 24 小时无新版本发布，社区重心集中在 V2 稳定性（OpenTUI 临时文件泄漏、TUI 退出后鼠标残留）、计费系统缺陷（Zen 余额/Go 订阅额度不生效）以及 Web UI 版本显示不一致等高频问题上。PR 侧多个 TUI/核心修复合入，另有 session request 钩子、便携模式等新功能提案。

## 社区热点 Issues

### 1. Ctrl+C 退出冲突 — 49 👍 / 16 评论
**#7957** | [链接](https://github.com/anomalyco/opencode/issues/7957)
Ctrl+C 在 OpenCode TUI 中直接退出程序，与 Windows/Linux 通用复制快捷键冲突。用户误按导致会话丢失，社区共鸣强烈（49 个赞），是最受关注的 UX 问题。

### 2. Desktop 5 分钟 Headers Timeout
**#26602** | [链接](https://github.com/anomalyco/opencode/issues/26602)
OpenCode Desktop 对本地 OpenAI 兼容 provider 的请求在恰好 5 分钟时中断，即使配置 `"timeout": false` 也无效。本地大模型推理耗时长，该问题严重阻碍慢速 provider 的使用。

### 3. Zen 付费余额仍触发免费额度限制
**#33318** | [链接](https://github.com/anomalyco/opencode/issues/33318)
用户已充值 $20 并启用 billing，仍收到 "Free usage exceeded" 错误。计费系统判定逻辑存在缺陷，影响付费用户信任度。

### 4. V2 CLI 无头命令加载 OpenTUI 并泄漏临时文件
**#37671** | [链接](https://github.com/anomalyco/opencode/issues/37671)
`--version`、`--help`、`service status` 等无需 TUI 的命令也会加载 13.1 MiB 的 `libopentui.so` 到临时目录且不清理，反复调用会持续消耗磁盘空间（关联 #42880）。

### 5. TUI 退出后鼠标转义序列乱码
**#20458** | [链接](https://github.com/anomalyco/opencode/issues/20458)
退出 TUI 后终端出现 `35;89;19M...` 等鼠标准义序列乱码，影响终端复用。虽与 #3199 分开处理，但用户仍需要手动 reset 终端。

### 6. Qwen 3.5/3.8 多系统消息兼容性
**#16560** / **#42909** | [链接](https://github.com/anomalyco/opencode/issues/16560) / [链接](https://github.com/anomalyco/opencode/issues/42909)
新版 Qwen 模型拒绝包含多个 system message 的请求，报 "System message must be at the beginning"。OpenCode 的 agent 机制常发送多条系统指令，导致 nvidia provider 和本地 ollama 模型均无法使用。

### 7. Web UI 版本号显示滞后
**#24286** / **#29301** / **#42920** | [链接](https://github.com/anomalyco/opencode/issues/24286) / [链接](https://github.com/anomalyco/opencode/issues/29301) / [链接](https://github.com/anomalyco/opencode/issues/42920)
多个用户报告 Web UI 显示的版本号比 CLI 低一个小版本（如 1.18.18 显示为 1.18.17）。虽非致命，但造成升级确认困惑，已有多条重复 issue。

### 8. Go 订阅额度用尽后不回退 Zen 余额
**#42938** | [链接](https://github.com/anomalyco/opencode/issues/42938)
Go 计划月度额度用尽后进入 12 小时冷却，即使开启 "Use balance" 且 Zen 余额有 $39.89 也不兜底。与现有文档描述不符，影响订阅用户连续性。

### 9. /tmp 目录高频生成 .so 文件损害 SSD
**#42880** | [链接](https://github.com/anomalyco/opencode/issues/42880)
用户报告 opencode 以极高频率生成 .so 文件，不得不将 /tmp 挂载为 tmpfs 并加定时清理任务来保护 SSD。V2 资源管理问题亟待修复。

### 10. zsh 补全缺少顶层 flags
**#42913** | [链接](https://github.com/anomalyco/opencode/issues/42913)
`opencode <TAB>` 不提示 `--continue`、`--session`、`--fork` 等顶层 flags，影响命令行效率，刚提交即获 3 条评论。

## 重要 PR 进展

### 1. 修复后台 subagent 状态误标
**#42944** | [链接](https://github.com/anomalyco/opencode/pull/42944)
避免将前台活动 subagent 标记为 background，并让指示器在后台子会话活跃时保持动画，含回归测试覆盖。

### 2. 会话请求钩子（session request hook）
**#37347** | [链接](https://github.com/anomalyco/opencode/pull/37347)
新增 `ctx.session.hook("request")`，可在请求序列化、鉴权之后、发送之前拦截并替换 Web Request，支持 AI SDK provider fetch 透传。

### 3. 同步 provider 插件启动流程
**#37351** | [链接](https://github.com/anomalyco/opencode/pull/37351)
修复 OpenAI/OpenCode 连接状态注册时机，移除无法在 Effect 测试时钟下推进的轮询，并同步设备授权测试。

### 4. TUI：提示框激活时禁用会话快捷键
**#37352** | [链接](https://github.com/anomalyco/opencode/pull/37352)
防止在权限/表单 prompt 弹出时，按下箭头误打开 subagent 活动查看器，改善 TUI 交互安全性。

### 5. 流式 shell 进度输出优化
**#37374** | [链接](https://github.com/anomalyco/opencode/pull/37374)
shell 进度改为最新 25 行替换快照，并附截断提示及完整输出路径，减少长输出对 TUI 的渲染压力。

### 6. 内容过滤拒绝原因透出
**#37392** | [链接](https://github.com/anomalyco/opencode/pull/37392)
当 Anthropic 返回 `stop_reason: "refusal"` 时，不再显示单一硬编码提示，而是展示具体拒绝分类与解释。

### 7. apply_patch 移动目标路径权限检查
**#37386** | [链接](https://github.com/anomalyco/opencode/pull/37386)
`apply_patch` 移动操作此前仅按源路径申请权限，现在同时检查目标路径，避免越权写入。

### 8. 文件 API 保留文本原始空白
**#37385** | [链接](https://github.com/anomalyco/opencode/pull/37385)
修复文件 API 对解码文本调用 `trim()` 导致首尾空白丢失的问题。

### 9. Desktop 便携模式（Portable Mode）
**#37325** | [链接](https://github.com/anomalyco/opencode/pull/37325)
支持从 U 盘或自定义目录直接运行 Desktop 应用，数据与配置随应用目录携带。

### 10. 命令面板隐藏模型循环命令
**#37363** | [链接](https://github.com/anomalyco/opencode/pull/37363)
将模型循环 keybind 命令从 command palette 中移除，减少误操作。

## 功能需求趋势

- **V2 架构稳定性**：多条 issue 指向 OpenTUI native 库被无头命令加载、临时文件泄漏、后台/前台 subagent 状态混乱。社区对 V2 的资源管理和生命周期治理有强烈诉求。
- **计费与额度系统透明化**：Zen 余额不抵扣、Go 订阅额度用尽后无回退机制、支付验证失败（Stripe/Alipay）等问题密集出现，说明计费状态机需要更清晰的日志和用户可见性。
- **混合本地模型兼容性**：Qwen 系列多 system message 拒绝、Desktop 5 分钟超时不可配置等，反映本地/第三方 OpenAI 兼容 provider 的使用场景日益重要，需要更灵活的适配层。
- **Web UI 与 CLI 一致性**：版本号显示不统一虽是小事，但连续出现 3 条以上 issue，说明 Web UI 的构建/发布流程存在系统性问题。
- **CLI 体验细节**：Ctrl+C 冲突、zsh 补全不全、session 深链 QR 码等建议，体现出用户对命令行交互效率要求更高。

## 开发者关注点

- **数据安全与磁盘损耗**：`/tmp` 下高频生成 .so 文件被用户视为「SSD 杀手」，已有人用 tmpfs + 定时清理自救，官方需要尽快修复临时文件生命周期。
- **误触退出导致上下文丢失**：Ctrl+C 退出无确认或撤销机制，开发者希望至少支持「再次按 Ctrl+C 才退出」或可配置键位。
- **付费信任危机**：充值后仍被限流、Go 订阅被锁死 12 小时，用户对计费系统的「确定性」产生怀疑，需要更透明的额度计算和错误信息。
- **TUI 残留污染终端**：鼠标序列、会话切换后状态错乱等终端卫生问题，影响 TUI 工具的专业感知。
- **多 provider 支持**：开发者正在尝试 nvidia、ollama、Z.AI、Dokploy MCP 等多种第三方服务，兼容性报错（400、超时、消息顺序）占据相当比例，需要更友好的错误诊断。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报

**日期：2026-08-17** | 数据来源：github.com/QwenLM/qwen-code


## 1. 今日速览

昨日社区围绕 **多智能体团队协作** 暴露出一批新问题（消息传递、任务分派、提示词矛盾），相关修复 PR 已迅速跟上；与此同时，**/review 管线的安全与可靠性** 仍是持续攻坚重点，P1 级 PAT 隔离问题有新进展，autofix 验证门正在迁入容器。终端体验方面，tmux 兼容性和中文输入法失效问题持续引发用户共鸣。


## 2. 版本发布

### v0.21.12-preview.5
预览版发布，基于 v0.21.12 的增量更新。完整变更日志见：[compare/v0.21.12...v0.21.12-preview.5](https://github.com/QwenLM/qwen-code/compare/v0.21.12...v0.21.12-preview.5)

### v0.21.11-nightly.20260816.5677823abb
夜间构建，包含一项 autofix 增强：
- **feat(autofix)**: deny-by-default footprint gate and positional window censuses（默认拒绝的足迹门控 + 位置窗口普查），作者 @wenshao，见 [#9156](https://github.com/QwenLM/qwen-code/pull/9156)

### DSW EAS 基准测试（r2 / r3）
两次针对 v0.21.12 的端到端基准重跑，覆盖 **SWE-bench Verified（500 项）** 与 **Terminal-Bench 2.0（89 项）**，在将 DSW 包代理作用域限定为仅验证器依赖出口后重新验证，最终仍发布同一版本。


## 3. 社区热点 Issues

### 🔴 #9089 — autofix：携带 PAT 的作业与不受信任的代码共享主机（P1/安全）
> **为什么重要**：当前唯一 P1 级问题。PR #8961 已在 Actions 步骤层面加固，但运行器级隔离无法在步骤内闭合，需要架构层面的容器隔离方案。
> **社区反应**：5 条评论，设计已在 #9214 中进入实施阶段（Phase 1+2）。
> [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9089)

### 🔴 #9276 — 团队成员无法向 leader 发送普通消息（P2/多智能体）
> **为什么重要**：团队成员发送普通完成/状态消息被误判为 shutdown 请求并报错 `Only the team leader can request shutdowns.`，直接影响多智能体协作的基础通信。
> **社区反应**：5 条评论，与 #9282/#9283/#9281 构成一组多智能体问题集群。
> [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9276)

### 🟠 #9290 — 打开出错的 agent-team 标签页导致交互会话崩溃（P2/UI）
> **为什么重要**：渲染错误穿过 FATAL 边界直接退出整个会话，用户无恢复手段。修复 PR #9292 已提交。
> **社区反应**：3 条评论，问题复现路径清晰。
> [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9290)

### 🟠 #9282 — 手动分配团队任务不派发工作（P2/多智能体）
> **为什么重要**：leader 可将任务置为 `in_progress` 并指定 owner，但空闲成员收不到任何提示，唯一投递路径只认未认领的 `pending` 任务，导致任务卡死。
> **社区反应**：3 条评论，修复 PR #9289 已提交。
> [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9282)

### 🟠 #9283 — Agent-team 提示词与自动投递行为矛盾（P2/多智能体）
> **为什么重要**：运行时已支持空闲时自动转发未上报的最终答案，但普通/计划提示仍要求显式 `send_message`，文档与实现不一致会误导 agent。
> **社区反应**：3 条评论，修复 PR #9284 已提交。
> [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9283)

### 🟠 #9281 — task_list 将空字符串过滤器当作有效过滤器（P2/工具）
> **为什么重要**：`owner=""` 或 `blockedBy=""` 被当作真实过滤条件，导致 `No tasks found.`，而工具描述声称空过滤器等于未传。
> **社区反应**：3 条评论，已有作者自己的修复 PR #9286。
> [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9281)

### 🟠 #5966 — 0.19.3 UI 中文输入法完全失效（P2/UI）
> **为什么重要**：中文用户无法在交互界面中输入中文，只能打拼音且无任何报错，定位困难。此问题已持续近 2 个月仍在等待信息补充。
> **社区反应**：5 条评论，状态为 need-information，欢迎 PR。
> [查看 Issue](https://github.com/QwenLM/qwen-code/issues/5966)

### 🟠 #8962 — tmux 下无法正常使用（P2/UI）
> **为什么重要**：tmux 或远程终端下屏幕持续闪烁，缩小显示尺寸后才勉强可用，影响大量服务器端用户。
> **社区反应**：3 条评论，用户情绪较强。
> [查看 Issue](https://github.com/QwenLM/qwen-code/issues/8962)

### 🟠 #9291 —

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*