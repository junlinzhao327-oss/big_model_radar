# AI CLI 工具社区动态日报 2026-09-03

> 生成时间: 2026-09-02 22:35 UTC | 覆盖工具: 7 个

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



---



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-09-03

## 今日速览

昨日密集发布了 `v1.0.83-2` 与 `v1.0.83-3` 两个版本，主要补强了自定义 agent 的模型回退链、加入了 `claude-fable-5.1` 支持，并为 Linux 沙箱加固网络出口限制。社区侧，**大量会话内存溢出（OOM）崩溃**与 **MCP 连接不稳定**成为最集中的吐槽点，另有若干与自定义 agent/技能在恢复或子代理场景下失效的回归报告。

---

## 版本发布

### [v1.0.83-3](https://github.com/github/copilot-cli/releases/tag/v1.0.83-3)
- 仅包含修复与常规变更，无新增特性说明。推测针对 v1.0.83-2 发布后的小规模回归或兼容性问题。

### [v1.0.83-2](https://github.com/github/copilot-cli/releases/tag/v1.0.83-2)
**新增**
- 自定义 agent 现可在 `model` 字段中声明多个模型，按顺序尝试直至某一个可用；`model-policy: required` 可强制保持在候选列表中切换，避免被替换为默认模型。
- 新增对 `claude-fable-5.1` 的支持。

**改进**
- Linux 沙箱网络出口限制为仅允许连接所配置的代理服务器（此前为宽松放行），从系统层面收紧 MCP/工具调用的越权网络访问面。

---

## 社区热点 Issues

### 1. 恢复长会话时直接堆内存溢出（OOM）
[#4664](https://github.com/github/copilot-cli/issues/4664) — `[area:sessions, area:context-memory]`
- **现象**：在恢复一个长时间运行的大会话时，Node.js/V8 堆内存耗尽，进程在用户尚未继续工作之前就已崩溃。
- **为什么重要**：这已是本周内第 3 个同类报告（另见 [#4686](https://github.com/github/copilot-cli/issues/4686)、[#4699](https://github.com/github/copilot-cli/issues/4699)），指向会话序列化体积不受控 + 恢复时全量加载导致的历史性问题。多位用户报告 4 GiB 堆上限被触及，说明问题并非偶发。

### 2. MCP 错误地从现代握手回退到旧版 `initialize`，导致 -32022
[#4525](https://github.com/github/copilot-cli/issues/4525) — `[area:mcp]`
- **现象**：1.0.81-1 对使用 Python MCP SDK 2.0.0 双

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>



</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报

**日期：2026-09-03**（数据截至 2026-09-02 UTC）


## 今日速览

Qwen Code 的 TUI 架构迁移（ink → OpenTUI）仍在持续推进，今天发布了 `live-host-v0.2.0`，并有多个相关 PR 合并/更新。与此同时，社区核心 Bug 集中在两大方向：一是**内容生成管道中 XML/工具调用标签泄漏到用户可见输出**，涉及至少 4 个 open issues；二是 **CI 稳定性问题**，过去 24 小时内有超过 15 个由机器人自动追踪的"Main CI failed" issue 被创建。此外，MCP 图像预算绕过（P2）和依赖 CVE 审计失败（P1，安全）值得关注。


## 版本发布

### live-host-v0.2.0
- **Release 链接**: https://github.com/QwenLM/qwen-code/releases
- **主要变更**：
  - `fix(ci)`: 使共享 ECS Vitest 并发度可调（PR #10667）
  - `feat(cli)`: OpenTUI migration batch 4（上下文截断，细节待查）
- **分析**: 该 Release 同时服务于 CI 基础设施的灵活性与 CLI 终端 UI 的渐进式迁移。OpenTUI 迁移批次进行到第 4 批，说明这是一次有规划的、分步骤完成的重构。


## 社区热点 Issues（Top 10）

### 1. #10818 — [P1] Monitor pulse storm 可 DoS 交互式会话：ESC 取消无效、用户输入被饿死
- **链接**: https://github.com/QwenLM/qwen-code/issues/10818
- **作者**: @chiga0 ｜ 创建: 2026-09-02 ｜ 评论: 3 ｜ 状态: OPEN
- **为什么重要**: 严重程度为 **P1**。Agent 在运行中产生大量 monitor pulse 事件，导致按键输入（包括 ESC 取消）完全无法响应。涉及的 transcript 高达 25MB、13,806 条记录，是真实场景下的严重可用性问题，直接阻塞用户对 Agent 的控制权。
- **社区反应**: 刚创建即获得 3 条评论，尚在讨论中。

### 2. #10850 — [P1/安全] 依赖 CVE 审计全仓库失败：fast-uri/qs/uuid 新公告
- **链接**: https://github.com/QwenLM/qwen-code/issues/10850
- **作者**: @yiliang114 ｜ 创建: 2026-09-02 ｜ 评论: 2 ｜ 状态: OPEN
- **为什么重要**: 安全相关（**P1**）。`npm audit --omit=dev` 报出 **4 个漏洞（1 low, 2 moderate, 1 high）**，涉及 fast-uri、qs、uuid 等核心依赖，导致 main 分支 CI 在 2026-09-02 16:30Z–17:20Z 期间全仓库失败。任何依赖 qwen-code 的用户都可能受影响，建议尽快跟进升级。

### 3. #8662 — 将 TUI 渲染层从 ink 迁移到 OpenTUI（tracking issue）
- **链接**: https://github.com/QwenLM/qwen-code/issues/8662
- **作者**: @chiga0 ｜ 创建: 2026-08-07 ｜ 更新: 2026-09-02 ｜ 评论: 22 ｜ 状态: OPEN
- **为什么重要**: 本仓库目前最核心的架构级重构。当前基于 **ink 7 + React 19** 的渲染器存在闪烁等结构性缺陷，需打 1037 行 patch + 自定义 Virtual Viewport（VP）模式才能工作。社区讨论热度最高（22 条评论），且多个 PR 在围绕此 issue 推进。
- **社区反应**: 该 tracking issue 仍在持续吸引关注，讨论涉及迁移批次规划。

### 4. #9942 — 隐藏顶级斜杠补全中的技能命令
- **链接**: https://github.com/QwenLM/qwen-code/issues/9942
- **作者**: @ChivuAndrei2003 ｜ 创建: 2026-08-24 ｜ 更新: 2026-09-02 ｜ 评论: 5 ｜ 状态: OPEN
- **为什么重要**: 安装了大量 skills 后，输入 `/` 的补全菜单被技能命令挤满，内建命令难找。属于**CLI 可用性/信息架构**问题，直接反映插件生态壮大后的新痛点。需要社区讨论补全分层/分组机制。

### 5. #7167 — Fleet Shepherd Dashboard（自动维护）
- **链接**: https://github.com/QwenLM/qwen-code/issues/7167
- **作者**: @qwen-code-dev-bot ｜ 创建: 2026-07-18 ｜ 更新: 2026-09-02 ｜ 评论: 3 ｜ 状态: OPEN
- **为什么重要**: 机器人自动维护的仪表盘 issue，用来跟踪整个 bot fleet 的状态（PR 检查、同步、发布、清理等）。本次 tick 显示所有指标正常（syncs: 0, dispatches: 0, releases: 0, cleanups: 0），可用于观测项目的自动化运维健康度。

### 6. #10692 — [P2] XML tool_call 方言泄漏为纯文本，fallback 只恢复 invoke 方言
- **链接**: https://github.com/QwenLM/qwen-code/issues/10692
- **作者**: @yiliang114 ｜ 创建: 2026-09-01 ｜ 更新: 2026-09-02 ｜ 评论: 2 ｜ 状态: OPEN
- **为什么重要**: 模型在 content/text 字段中输出原始 XML 工具调用而非结构化 `tool_calls` 数组时，恢复机制漏掉了 `<tool_call>` 方言——**这正是 qwen-code 系统提示词教模型使用的格式**。属于上下文/工具调用可靠性问题，会导致模型输出污染。

### 7. #10791 — [P2] 平衡的 content-only `<thinking>` 块仍泄漏到用户可见输出
- **链接**: https://github.com/QwenLM/qwen-code/issues/10791
- **作者**: @yiliang114 ｜ 创建: 2026-09-02 ｜ 更新: 2026-09-02 ｜ 评论: 2 ｜ 状态: OPEN
- **为什么重要**: 防御机制只捕获未闭合的 thinking 标签，但**格式正确的、成对平衡的** thinking 块在 content-only turn 中仍会泄漏到 UI。说明当前的清洗逻辑不够完备，需要更鲁棒的检测策略。

### 8. #10797 — [P2] 非思考性脚手架标签（tool-result 块、system-reminder）回显到用户可见输出
- **链接**: https://github.com/QwenLM/qwen-code/issues/10797
- **作者**: @yiliang114 ｜ 创建: 2026-09-02 ｜ 更新: 2026-09-02 ｜ 评论: 2 ｜ 状态: OPEN
- **为什么重要**: 在已知的 thinking/analysis 泄漏之外，又发现两种新的内部脚手架泄漏形状：tool-result 风格 XML 块被模拟/回显为 content、系统提醒进入用户可见输出。内容净化覆盖面需要扩大。
- **状态**: 标记为 `welcome-pr`，欢迎社区贡献修复。

### 9. #10700 — [P2] 孤立的工具调用闭合标签（`</parameter>`、`</invoke>`）泄漏为纯文本
- **链接**: https://github.com/QwenLM/qwen-code/issues/10700
- **作者**: @yiliang114 ｜ 创建: 2026-09-01 ｜ 更新: 2026-09-02 ｜ 评论: 2 ｜ 状态: OPEN
- **为什么重要**: XML 恢复逻辑只匹配平衡的 invoke 对，遇到只输出闭合标签的情况会漏掉。与 #10692、#10791、#10797 一起构成**内容生成可靠性**问题族，影响模型输出的最终展示质量。

### 10. #10834 — [P2] MCP 工具返回的图片绕过 read_file 图像预算，全分辨率进入上下文
- **链接**: https://github.com/QwenLM/qwen-code/issues/10834
- **作者**: @yiliang114 ｜ 创建: 2026-09-02 ｜ 更新: 2026-09-02 ｜ 评论: 2 ｜ 状态: OPEN
- **为什么重要**: `read_file` 读取图片时会经过共享视觉预算（最长边最多 1568px），但 MCP 工具返回的图片**没有任何尺寸限制**、逐字节转发给模型。会导致上下文窗口被超大图迅速耗尽，同时增加 token 成本。


## 重要 PR 进展（Top 10）

### 1. #10858 — [OPEN] fix(ci): 给 scripts 测试套件共享 ECS 超时上限
- **链接**: https://github.com/QwenLM/qwen-code/pull/10858
- **作者**: @qwen-code-dev-bot ｜ 创建: 2026-09-02 ｜ 更新: 2026-09-02
- **内容**: 让仓库的脚本测试套件也获得共享自托管 ECS 池的超时上限配置，同时移除 autofix 工作流契约套件中 7 个重复的按测试用例超时设置。
- **意义**: 纯 CI 基础设施改进，减少超时导致的不稳定失败。注意：最新 Release live-host-v0.2.0 的 release notes 中提到的 #10667 PR 与该 PR 标题相关，但 #10667 本身不在列表中。

### 2. #10831 — [OPEN] fix(cli): 补齐 OpenTUI 提交路径缺口，恢复其 E2E 测试
- **链接**: https://github.com/QwenLM/qwen-code/pull/10831
- **作者**: @chiga0 ｜ 创建: 2026-09-02 ｜ 更新: 2026-09-02 ｜ 标签: autofix/takeover
- **内容**: 让 OpenTUI 渲染器的提交路径与 ink 渲染器对齐：① 提交时携带用户输入原始文本（与发往模型的内容分开）② `@` 提及内容能以所引用文件的完整内容到达模型 ③ 另有 2 个待查细节。
- **意义**: 这是 OpenTUI 迁移 #8662 的关键收尾工作，该 PR 将恢复被禁用的 E2E 测试。

### 3. #10855 — [OPEN] fix(ci): main CI 无测试结果失败时标注失败 job 名称
- **链接**: https://github.com/QwenLM/qwen-code/pull/10855
- **作者**: @qwen-code-dev-bot ｜ 创建: 2026-09-02 ｜ 更新: 2026-09-02
- **内容**: 当 main CI 失败但没有报告任何测试结果时，机器人 filed issue 现在会带上失败 job 与 step 的名字，而不是只写 commit 哈希。
- **意义**: 提升失败问题的可操作性，降低开发者定位 CI 故障的成本。与今天批量出现的 "Main CI failed" issues 高度相关。

### 4. #10842 — [OPEN] fix(release): 防止单个 flaky 测试导致稳定版发布失败
- **链接**: https://github.com/QwenLM/qwen-code/pull/10842
- **作者**: @yiliang114 ｜ 创建: 2026-09-02 ｜ 更新: 2026-09-02
- **内容**: 稳定版发布现在会对失败的 workspace 测试做重试（此前只有 nightly/preview 有此机制）；同时加固 6 个曾实际阻塞发布的测试，使其不再依赖重试。
- **意义**: release 质量门禁由约三万测试组成，单个 flake 不应阻塞稳定版发布。这是**发布管道健壮性**的直接提升。

### 5. #10857 — [OPEN] fix(web-shell): 将弹窗中全选操作限定在字段值内
- **链接**: https://github.com/QwenLM/qwen-code/pull/10857
- **作者**: @LizunovSergey ｜ 创建: 2026-09-02 ｜ 更新: 2026-09-02
- **内容**: 修复 "Current field value" 弹窗中 Cmd+A / Ctrl+A 会选中整个页面文本的问题。现在该快捷键只选中当前值框中的内容。
- **意义**: 小但典型的 UI 细节修复。Web Shell 作为交互入口，这类操作体验问题直接影响日常工作效率，也是新贡献者容易上手的切入点。

### 6. #10841 — [OPEN] feat(skills): 扩展技能以 "扩展名:技能名" 形式命名
- **链接**: https://github.com/QwenLM/qwen-code/pull/10841
- **作者**: @nerdalytics ｜ 创建: 2026-09-02 ｜ 更新: 2026-09-02
- **内容**: 扩展技能注册时改为 `<extensionName>:<authoredName>`。比如 rust 扩展提供的 pdf 技能在斜杠命令列表、tool 查找、restriction 匹配、设置界面等处都显示为 `rust:pdf`。
- **意义**: 解决多扩展技能重名/混淆问题。**命名空间化**是生态扩张后的必要演进，也回应了 #9942 中的混杂性问题。

### 7. #10455 — [OPEN] fix(cli): 输出语言文件不可写时不再导致启动崩溃
- **链接**: https://github.com/QwenLM/qwen-code/pull/10455
- **作者**: @qwen-code-dev-bot ｜ 创建: 2026-08-29 ｜ 更新: 2026-09-02 ｜ 标签: review/self-reported, autofix/needs-human
- **内容**: CLI 每次启动都会向全局配置目录写入一个建议性输出语言规则文件。当目录不可创建（只读 home 或共享 runner 上 root 所有权的残留目录）时，未受保护的写入会直接导致启动崩溃。该 PR 提供防护。
- **意义**: 面向 CI/共享环境健壮性的重要修复，避免容器化或受管环境中不可用问题。

### 8. #8927 — [OPEN] feat(channels): 使用 sessionRotation 限定会话生命周期
- **链接**: https://github.com/QwenLM/qwen-code/pull/8927
- **作者**: @qwen-code-dev-bot ｜ 创建: 2026-08-11 ｜ 更新: 2026-09-02 ｜ 标签: review/self-reported, autofix/needs-human
- **内容**: 增加每通道 `sessionRotation` 选项，当路由上的当前 session 超过限制后，下一条消息自动开启新会话。支持两种 bound：`maxTurns`（消息数）和按时间（截断未明）。
- **意义**: 针对长时间运行的 channel 任务提供会话过期机制，防止上下文无限膨胀。

### 9. #9768 — [OPEN] feat(review): 将 coverage 变为密封的分类账本
- **链接**: https://github.com/QwenLM/qwen-code/pull/9768
- **作者**: @wenshao ｜ 创建: 2026-08-23 ｜ 更新: 2026-09-02 ｜ 标签: autofix/takeover, autofix/ne

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*