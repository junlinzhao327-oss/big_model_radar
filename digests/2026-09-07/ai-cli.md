# AI CLI 工具社区动态日报 2026-09-07

> 生成时间: 2026-09-06 22:35 UTC | 覆盖工具: 7 个

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

*数据来源：github.com/anthropics/skills | 数据截止：2026-09-07*

---

## 一、热门 Skills（PR）排行

按仓库评论热度排序，当前展示的 PR 均处于 **Open** 状态，以下是关注度最高的 8 个：

### 1. skill-creator：run_eval.py 评测召回率恒为 0% 的修复 [PR #1298]
- **功能**：修复 `run_eval.py` 对所有 Skill 描述一律报 `recall=0%` 的严重缺陷，打通「评测 → 优化描述」闭环。根因是评测产物未真正安装为 skill，同时修复 Windows 流读取、触发检测与并行 worker 问题（关联 Issue #556，12 条评论、7 👍）。
- **社区热点**：这是 skill-creator 工具链当前最大的可靠性痛点，Issue #556 已有 10+ 独立复现报告，直接影响所有技能的自动化优化。
- **状态**：OPEN（2026-06-10 创建，06-23 更新）
- 链接：https://github.com/anthropics/skills/pull/1298

### 2. document-typography：AI 生成文档的排版质量控制 [PR #514]
- **功能**：新增面向文档排版的技能，解决 AI 生成文档的典型问题——孤词换行、标题滞留页尾（寡妇段）、编号错位等。
- **社区热点**：这类"用户很少主动要求但影响专业度"的隐性质量问题引发讨论，被视为提升 AI 文档交付质量的基础能力。
- **状态**：OPEN（2026-03-04 创建，03-13 更新）
- 链接：https://github.com/anthropics/skills/pull/514

### 3. scnet-hpc：HPC 集群运维技能 [PR #1615]
- **功能**：通过 profile 化 SSH 与 Slurm 工作流操作 SCNet HPC 集群，覆盖连接管理、分区/内存/模块配置、Slurm 作业生成、集群发现等场景。
- **社区热点**：代表了将 Claude Code 从日常开发扩展到科学计算/高性能计算领域的社区诉求。
- **状态**：OPEN（2026-08-20 创建，08-24 更新）
- 链接：https://github.com/anthropics/skills/pull/1615

### 4. ODT：OpenDocument 创建/填充/转换技能 [PR #486]
- **功能**：支持 .odt/.ods 文件的创建、模板填充、读取，并可将 ODT 解析为 HTML，覆盖 LibreOffice 及 ISO 标准格式需求。
- **社区热点**：文档类技能（DOCX/PDF/ODT）持续热门，表明办公文档处理是 Claude Code 生态的高频刚需。
- **状态**：OPEN（2026-03-01 创建，04-14 更新）
- 链接：https://github.com/anthropics/skills/pull/486

### 5. frontend-design 技能优化 [PR #210]
- **功能**：修订 frontend-design 技能，提升清晰度与可执行性，确保每条指令可在单次对话内落地，并让指导足够具体以约束模型行为。
- **社区热点**：讨论围绕"技能指令应可行动而非描述性文字"，与 #202（skill-creator 应更新为最佳实践）形成呼应。
- **状态**：OPEN（2026-01-05 创建，03-07 更新）
- 链接：https://github.com/anthropics/skills/pull/210

### 6. skill-quality-analyzer + skill-security-analyzer 元技能 [PR #83]
- **功能**：向 marketplace 新增两个元技能——质量分析器（结构/文档、示例、资源等五维度评估）与安全分析器，用于对 Claude Skills 本身做体检。
- **社区热点**：反映了社区开始关注"技能的质量度量与安全治理"这一上层议题，呼应 #492 的安全信任边界讨论。
- **状态**：OPEN（2025-11-06 创建，2026-01-07 更新，最老牌的活跃 PR 之一）
- 链接：https://github.com/anthropics/skills/pull/83

### 7. Hivemind：零成本多智能体编排 [PR #1628]
- **功能**：让 Claude Code 将机械性工作委托给运行免费模型的 headless opencode worker，Claude 仅担任规划、评审与合并角色，以"省上下文"为核心卖点。
- **社区热点**：多智能体协作与成本优化方向热度上升，讨论集中在"昂贵模型的上下文才是最稀缺资源"这一理念。
- **状态**：OPEN（2026-08-21 创建，08-24 更新）
- 链接：https://github.com/anthropics/skills/pull/1628

### 8. ServiceNow 平台技能 [PR #568]
- **功能**：覆盖 ServiceNow 全平台的助手型技能，含 ITSM、ITOM、ITAM/SAM、FSM、HRSD、SPM、CSDM、IntegrationHub 等模块。
- **社区热点**：讨论点在于"平台级广度技能"与"窄脚本助手"的定位取舍，以及企业级软件领域的技能设计模式。
- **状态**：OPEN（2026-03-08 创建，08-12 仍在更新，长线活跃）
- 链接：https://github.com/anthropics/skills/pull/568

---

## 二、社区需求趋势（来自 Issues）

### 1. 技能的安全与信任边界（热度最高）
Issue #492（43 条评论）揭露：社区技能在 `anthropic/`

---



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

## 今日速览

- 过去 24 小时无新版本 Release，但 PR 合并活跃，机器人提交集中在 TUI managed worktree、voice-host 音频管线与 MCP user verification 等领域。
- 社区 Issue 热点集中在 Windows 桌面端：宠物（Pets）点击穿透、应用启动失败、项目上下文同步失败等问题密集发酵，其中宠物交互问题已有多个高赞重复报告。
- Codex 配额/用量异常继续聚集，多个独立 Issue 指向同一用户可见症状，已形成跨报告追踪 Issue。

## 社区热点 Issues

### 1. [bug, windows-os, app, app-server] Windows 26.820：Codex Desktop 无法启动——bundled codex.exe 从 WindowsApps 重定位失败
- 评论 44 | 👍 2 | #40700
- 涉及 Windows 桌面端启动级故障，影响用户无法进入应用，评论区讨论热烈但点赞不高，说明问题真实但可能影响范围有限。
- https://github.com/openai/codex/issues/40700

### 2. [bug, windows-os, app, pets] Windows 浮动宠物点击穿透且无法拖动
- 评论 21 | 👍 33 | #41465
- 33 个 👍 是今日最高，说明大量用户受“宠物不可交互”困扰。同类报告还有 #41513、#41960，已形成明显 Issue 簇。
- https://github.com/openai/codex/issues/41465

### 3. [bug, app, session] macOS：服务端已删除的对话重新出现在 Recents 且无法移除
- 评论 22 | 👍 16 | #40219
- 会话状态与远端不一致，用户删除后仍“复活”，直接影响聊天记录可信度，点赞数较高。
- https://github.com/openai/codex/issues/40219

### 4. [bug, rate-limits] Codex 配额/用量异常跨报告追踪
- 评论 22 | 👍 10 | #41220
- 被社区用作汇总帖，收集“配额消耗速度远超预期”“与本地 token 证据不符”等报告，属于高敏感计费/配额问题。
- https://github.com/openai/codex/issues/41220

### 5. [bug, windows-os, app] Windows ChatGPT Work：项目上下文同步反复失败
- 评论 16 | 👍 0 | #42215
- 在已有 ChatGPT Project 中无法启动本地 Work 聊天，失败发生在文件系统同步阶段，阻断正常开发流。
- https://github.com/openai/codex/issues/42215

### 6. [bug, windows-os, exec, CLI, tool-calls] WSL2 下 codex-code-mode-host 0.147.0 每次 shell exec 崩溃（SIGTRAP），0.146.1 正常
- 评论 13 | 👍 0 | #38417
- 影响 WSL2 用户的 CLI 高频操作路径，是一次明显的版本回归，开发者关注度高。
- https://github.com/openai/codex/issues/38417

### 7. [bug, app] macOS：首条消息后 Composer 消失，需重启窗口才能恢复
- 评论 9 | 👍 7 | #42583
- 较新版本中出现，输入框直接消失会中断对话，用户已确认与键盘焦点无关，疑似 UI 状态机问题。
- https://github.com/openai/codex/issues/42583

### 8. [bug, app] Linux 应用更新后在 libqxcb 中启动崩溃
- 评论 5 | 👍 0 | #42148
- Ubuntu 24.04 上从 26.820.60940 升级到 26.831.20005 后无法启动，Qt 插件级崩溃，影响 Linux 桌面用户。
- https://github.com/openai/codex/issues/42148

### 9. [bug, windows-os, app] 新 ChatGPT Windows 桌面版向免费/Go 用户显示“GPT 5.6 Sol”模型，造成误导
- 评论 2 | 👍 0 | #41631
- 模型选择器对无权限用户展示高规格模型，用户在较低订阅层级下会误以为自己可以使用该模型。
- https://github.com/openai/codex/issues/41631

### 10. [bug, iOS, app, session, remote] iOS Remote 项目列表与 Codex Desktop 未同步
- 评论 6 | 👍 0 | #36454
- Remote 场景下项目列表没有以 Desktop 为数据源，导致 iOS 端看到的项目内容不一致，影响跨端工作流。
- https://github.com/openai/codex/issues/36454

## 重要 PR 进展

### 1. Add a managed worktree browser to the TUI
- #43286
- 为 `/worktree` 增加可搜索的 “Browse worktrees” 入口，可查看 owner metadata 并支持恢复 owner thread 或复制工作树路径。
- https://github.com/openai/codex/pull/43286

### 2. Defer managed worktree transitions to fresh TUI loop iterations
- #43298
- 将 managed worktree 的 setup/checkout 等阶段拆分为独立事件循环迭代，避免在 ChatWidget 构造函数中同步执行大任务。
- https://github.com/openai/codex/pull/43298

### 3. Include linked worktrees in TUI session discovery
- #43279
- 目录级会话发现会遗漏同一仓库 linked worktrees 中的会话；该 PR 将 linked worktrees 纳入发现范围。
- https://github.com/openai/codex/pull/43279

### 4. Add managed worktree creation to TUI session commands
- #43120
- 新增 `/worktree` 命令支持在新会话或 fork 当前会话时创建 managed checkout，并优化 `/new` 与 `/fork` 交互。
- https://github.com/openai/codex/pull/43120

### 5. Show read-only conversations when resume encounters an active writer
- #43253
- 当恢复的会话在其他端被占用时，不再直接报错，而是提供只读历史视图，用户可关闭占用端后重试。
- https://github.com/openai/codex/pull/43253

### 6. Use server defaults when starting TUI background tasks
- #43261
- 从 agents overview 启动后台任务时改用服务端默认配置，避免客户端模型设置覆盖正确目的目录配置。
- https://github.com/openai/codex/pull/43261

### 7. Connect voice-host RTP audio to speaker playback
- #43248
- 将 voice host 收到的 RTP 音频包接入解码与扬声器输出，配合 speaker suppression 边界管理，补齐语音播放链路。
- https://github.com/openai/codex/pull/43248

### 8. Add bounded GStreamer playback components to the voice host
- #43244
- 增加带边界的 GStreamer 播放组件，支持部分写入、播放 epoch 变化取消及延迟统计，提升音频播放健壮性。
- https://github.com/openai/codex/pull/43244

### 9. Add capability-gated MCP user-verification handling
- #43289
- 当客户端声明支持 `userVerification` 时，通过 `openai/elicitation/create` 处理验证请求，并校验字段、大小限制与 base64url 编码。
- https://github.com/openai/codex/pull/43289

### 10. Add experimental user verification API contracts
- #43265
- 新增 `userVerification/status`、`enroll`、`delete`、`verify` 实验性 API 契约，并导出 schema

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-09-07**  
数据来源：[github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)

---

## 1. 今日速览

昨日发布 v0.60.0 nightly 新版本，但社区讨论焦点集中在 **P1 级可靠性 bug** 上：子代理在超时后误报 GOAL 成功、通用代理无限挂起、Shell 命令结束后卡在等待输入等。此外，围绕 **Auto Memory 自动记忆系统** 的安全与重试机制问题形成了密集的 issue 簇，建议关注这些对日常自动化工作流有直接影响的稳定性缺陷。

---

## 2. 版本发布

**v0.60.0-nightly.20260906.g85aca163f**  
- 常规 nightly 更新。[查看完整变更日志](https://github.com/google-gemini/gemini-cli/compare/v0.60.0-nightly.20260905.g85aca163f...v0.60.0-nightly.20260906.g85aca163f)

---

## 3. 社区热点 Issues

以下按讨论热度与影响范围筛选出

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>



</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

## Qwen Code 社区动态日报 — 2026-09-07

### 1. 今日速览
今日发布预览版 v0.23.1-preview.1，主要包含 Web Shell 动态工作流运行可视化与性能优化。社区层面，数据隐私与安全问题集中爆发（Raw 工具错误文本上传、技能安全钩子在 `--continue` 后失效），同时 Web Shell 的性能与功能增强成为 PR 主力方向。

---

### 2. 版本发布

#### v0.23.1-preview.1
[Release 链接](https://github.com/QwenLM/qwen-code/releases) | 基于 `release/v0.23.1-preview.1` 分支生成。

**更新内容**
- **feat(web-shell): visualize and manage dynamic workflow runs** by @qqqys in [#10594](https://github.com/QwenLM/qwen-code/pull/10594)
- **perf(web-shell): derive the session workflow project** (性能优化)

> 注：同时存在 v0.23.0-nightly 构建，携带相同变更集。

---

### 3. 社区热点 Issues（10 个）

1. **遥测上传未脱敏的原始工具错误文本（含 Shell 命令行）**
   - **优先级**: P1 | 安全/数据隐私
   - **概要**: 默认启用的 usage-statistics 通道将原始工具错误文本上传至 RUM 端点，无任何脱敏处理，涉及 Shell 错误详情。这是 `main` 上已存在的问题，影响面大于此前 #10916 的单个字段。
   - [Issue 链接](https://github.com/QwenLM/qwen-code/issues/11198)

2. **技能 `PreToolUse` 钩子在 `--continue` 后停止执行**
   - **优先级**: P1 | 安全
   - **概要**: SKILL.md 声明的 `PreToolUse` 钩子作为安全闸门，在断点续跑后不再执行，而技能指令仍在上下文中。安全门禁失效可能导致授权命令在缺失 session ID 时被执行。
   - [Issue 链接](https://github.com/QwenLM/qwen-code/issues/11180)

3. **导出 HTML 不再内嵌 Web Shell 运行时后，mermaid（~6MB）仍被扁平化**
   - **状态**: 已关闭 | 性能
   - **概要**: #9812 已修复 HTML 内联渲染器问题（改为 SRI 引用的外部脚本），但 mermaid 库（约 6 MB）仍被打包进导出文件，导致文件体量异常。
   - [Issue 链接](https://github.com/QwenLM/qwen-code/issues/11091)

4. **停止在每个 HTML 文件中嵌入 Web Shell 运行时**
   - **状态**: 已关闭 | P1 | 性能
   - **概要**: `/export html` 当前将整个浏览器依赖图（React + Web Shell 运行时）嵌入导出文件，即使空会话也会生成 **19.5 MB** 的 HTML。此问题已修复。
   - [Issue 链接](https://github.com/QwenLM/qwen-code/issues/11031)

5. **将 TUI 渲染层从 ink 迁移至 OpenTUI（跟踪）**
   - **状态**: OPEN | P3 | 增强
   - **概要**: 当前 TUI 基于 ink 7 + React 19，附带大量自定义补丁（含 1037 行的 `ink+7.0.3.patch`）与虚拟视口模式。存在闪烁等结构性缺陷，难以在 ink 内修复。跟踪 issue 共收到 30 条评论，是社区长期关注的基础设施重构方向。
   - [Issue 链接](https://github.com/QwenLM/qwen-code/issues/8662)

6. **Release 流程重复干活，且某 20 分钟步骤零验证**
   - **优先级**: P2 | CI/CD | 开发
   - **概要**: `release.yml` 大量占用墙钟时间重复劳动，且一个耗时 20 分钟的步骤实际无任何验证作用。今日已有两次 release run 超时（[run1](https://github.com/QwenLM/qwen-code/actions/runs/33957952281), [run2](https://github.com/QwenLM/qwen-code/actions/runs/33963757913)）。
   - [Issue 链接](https://github.com/QwenLM/qwen-code/issues/11109)

7. **核心调度器：预中止的工具请求可能在无关的活跃批次后等待**
   - **优先级**: P2 | Bug
   - **概要**: `CoreToolScheduler.schedule()` 在调度器忙时会将已取消的请求加入队列。若该请求在信号中止后未能及时移出队列，会阻塞在无关批次之后，导致取消操作无法及时生效。
   - [Issue 链接](https://github.com/QwenLM/qwen-code/issues/11146)

8. **WebShell 切换后恢复 VS Code 消息编辑与回退能力**
   - **状态**: OPEN | 功能请求 | IDE 集成
   - **概要**: WebShell 切换（#9811）有意未恢复旧版 VS Code 逐条消息编辑/回退交互。但嵌入式 VS Code Host 仍以 ACP 为运行时边界，二者存在功能落差，需设计统一的编辑/回退体验。
   - [Issue 链接](https://github.com/QwenLM/qwen-code/issues/9911)

9. **SDK 规范器在转录回放时丢弃用户 `resource_link` 附件**
   - **优先级**: P2 | SDK | Bug
   - **概要**: TypeScript daemon 的 UI 规范化器在 `user_message_chunk` 事件中静默丢弃 ACP 的 `resource_link` 内容，导致基于 SDK 重建历史视图时附件卡片消失。
   - [Issue 链接](https://github.com/QwenLM/qwen-code/issues/11178)

10. **`/effort` 命令未传播至通用 OpenAI 兼容后端**
    - **优先级**: P2 | Bug | 兼容性
    - **概要**: 使用本地 NInfer（OpenAI 兼容 API）时，`/effort` 更新了 Qwen Code 内的设置，但未作为参数传递至 HTTP 请求，导致推理强度调整无效。
    - [Issue 链接](https://github.com/QwenLM/qwen-code/issues/11227)

---

### 4. 重要 PR 进展（10 个）

1. **fix(vscode): 规范化工作区路径**
   - 在启动 WebShell daemon、持久化活跃会话、启动内嵌 shell 及导出来前，对 VS Code 工作区路径做符号链接解析（如 macOS `/tmp` → `/private/tmp`），避免路径不一致引发会话错乱。
   - [PR 链接](https://github.com/QwenLM/qwen-code/pull/11201)

2. **feat: 将子智能体回合委托给外部 ACP 智能体（优先支持 Claude Code）**
   - 子智能体定义可声明 `executor` 命令块，回合通过 ACP 协议派发给外部编码智能体执行，并将执行过程重新发布为该子智能体的内部事件。这对多智能体生态有重要扩展意义。
   - [PR 链接](https://github.com/QwenLM/qwen-code/pull/11003)

3. **fix(ci): 为瞬时全部绿灯的 macOS E2E 分片死机增加一次重试**
   - 为 macOS E2E 增加与 Linux `sandbox:none` 相同的单次、预算限制重试机制，提升 CI 稳定性。
   - [PR 链接](https://github.com/QwenLM/qwen-code/pull/11134)

4. **fix(core): 捕获工具结果脚手架与系统提示回显泄漏**
   - 消灭 #10797 中两种绕过现有泄漏防御的用户可见输出：a) 回复以工具结果 XML 标签开头；b) 系统提示回显型泄漏。仍处于开放讨论中。
   - [PR 链接](https://github.com/QwenLM/qwen-code/pull/11189)

5. **fix(core): 在 Ctrl+Y 不可用时自动重试瞬时网络错误**
   - 将实为网络层故障的 4xx（如 `400 network error ... EOF`）归类为可重试传输错误，使有限次自动重试机制生效，而非直接 fail-fast。
   - [PR 链接](https://github.com/QwenLM/qwen-code/pull/10347)

6. **feat(web-shell): gzip 压缩会话加载响应**
   - 针对 #6181 的 serve 层优化：对 `POST /session/:id/load` 等大型转录加载响应启用 gzip，压缩体积以缓解移动端会话切换卡顿。
   - [PR 链接](https://github.com/QwenLM/qwen-code/pull/11220)

7. **feat(web-shell): 在右侧栏增加 Context Usage 标签页**
   - 新增会话级 `context_usage` 面板，实时展示上下文窗口占用，提供堆叠层图标入口，与现有 Token Usage 标签页并列。
   - [PR 链接](https://github.com/QwenLM/qwen-code/pull/11177)

8. **feat(web-shell): 增加有界历史转录视窗**
   - 实现 2B 阶段的会话级上下文回溯：可在只读历史窗口内浏览超页记录、恢复被逐出的间隙，并返回实时尾部。适合长会话翻查，显著提升 Web Shell 的大会话可用性。
   - [PR 链接](https://github.com/QwenLM/qwen-code/pull/11208)

9. **feat(serve): 支持具备会话栅栏的并发独立守护进程**
   - 在保留 #10924 单写者租约的前提下，允许多个守护进程共享 Conversations 存储并并发运行独立会话。将为高级多会话工作流提供基础。
   - [PR 链接](https://github.com/QwenLM/qwen-code/pull/11207)

10. **fix(vscode): 关闭权限 Diff 后交还编辑权**
    - 修复用户手动关闭 Host 拥有的权限 Diff 后，因 `DiffManager.cancelDiff` 触发 `ide/diffClosed`

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*