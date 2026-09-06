# AI CLI 工具社区动态日报 2026-09-06

> 生成时间: 2026-09-05 23:59 UTC | 覆盖工具: 7 个

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

# Gemini CLI 社区动态日报 · 2026-09-06

## 1. 今日速览

昨日发布 v0.60.0 nightly 版本，重点修复了扩展对环境变量的静默修改以及命令安全中的工作区路径边界问题。与此同时，社区针对“`--model gemini-2.5-flash` 被静默改写为 `gemini-3.5-flash`”这一高影响 Bug 提交了两个修复 PR（#29217、#29222），成为当前最受关注的开发热点。Issue 队列方面，Google 维护团队对大量积压 issue 进行了批量状态更新（need-retesting / need-information），表明内部正在推进一轮集中回归与验证。

## 2. 版本发布

[v0.60.0-nightly.20260905.g85aca163f](https://github.com/google-gemini/gemini-cli/releases) 于昨日发布，更新要点：

- **扩展系统安全性修复**：扩展在修改环境变量前必须先征得用户同意，并清理可能改变运行时行为的环境变量（PR [#28863](https://github.com/google-gemini/gemini-cli/pull/28863)）。
- **命令安全加固**：增强了工作区路径边界检查与 symlink 解析逻辑，降低逃逸风险。

## 3. 社区热点 Issues

**#22323 Subagent MAX_TURNS 中断被误报为 GOAL 成功**（💬 13 · 更新 09-05）
[issue #22323](https://github.com/google-gemini/gemini-cli/issues/22323)
`codebase_investigator` 子代理明明在达到最大轮次后中断、未做任何分析，却仍以 `status: success` 和 `GOAL` 作为终止原因上报，误导主代理判断。目前状态为 need-retesting，是子代理可靠性的核心缺陷，也是昨日评论数最高的 issue。

**#29213 显式指定 gemini-2.5-flash 被映射到 gemini-3.5-flash**（💬 4 · 新建 09-04）
[issue #29213](https://github.com/google-gemini/gemini-cli/issues/29213)
在 Vertex AI 后端上，`--model gemini-2.5-flash` 被静默改写为 `gemini-3.5-flash`，而无权访问后者的环境直接请求失败。这是一个影响生产环境的高优先级配置 Bug，社区已迅速提交修复，参见下方 PR。

**#21409 Generalist agent 永久挂起**（👍 8 · 💬 8 · 更新 09-05）
[issue #21409](https://github.com/google-gemini/gemini-cli/issues/21409)
一旦 defer 到 generalist agent，即使是“创建文件夹”这类简单操作也会永久挂起，用户最长等待 1 小时后手动取消。在提示词中禁用子代理后问题消失。该 issue 已获 8 个 👍，是遭受影响用户最多的 Agent 议题之一。

**#19873 利用模型的 bash 原生能力：零依赖 OS 沙箱与执行后意图路由**（💬 9）
[issue #19873](https://github.com/google-gemini/gemini-cli/issues/19873)
Gemini 3 模型天然熟悉 bash 工具链（grep/sed/awk），该 issue 主张在不牺牲安全性的前提下，通过 OS 级沙箱放开模型执行 shell 命令的能力，并在命令执行后引入“意图路由”机制。代表了 Agent 工具设计的一个关键探索方向。

**#21968 Gemini 不会主动使用 skills 和 sub-agents**（💬 6）
[issue #21968](https://github.com/google-gemini/gemini-cli/issues/21968)
用户反馈实际使用中 Gemini CLI 几乎从不主动调用自定义 skills 和子代理，即便任务与已定义的 skill 高度相关（如 gradle/git skill），只有显式指示才会使用。这反映了 Agent 自主规划能力的不足，也说明 skill 的触发机制需要改进。

**#22745 AST 感知文件读取与代码库映射影响评估**（💬 7 · EPIC）
[issue #22745](https://github.com/google-gemini/gemini-cli/issues/22745)
一个 EPIC 级 issue，系统评估“AST 感知”工具（精确读取方法边界、语义化搜索、代码库映射）在减少 token 噪声和提升导航精度上的价值。

**#25166 Shell 命令执行完成后卡在 “Waiting input”**（👍 3 · 💬 4）
[issue #25166](https://github.com/google-gemini/gemini-cli/issues/25166)
极简 CLI 命令执行完毕后，终端仍显示命令激活并等待用户输入，导致 Agent 挂起。属于破坏日常使用体验的 P1 问题。

**#20079 ~/.gemini/agents/ 中的 symlink 不被识别为 agent**（💬 4）
[issue #20079](https://github.com/google-gemini/gemini-cli/issues/20079)
当自定义 agent 文件是 symlink 时，Gemini CLI 无法将其识别为 subagent，限制了用户通过

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

# Qwen Code 社区动态日报 — 2026-09-06

## 今日速览

昨日发布两个新版本（v0.23.1-preview.0 与 v0.23.0 nightly），核心改动聚焦于 Web Shell 动态工作流运行的可视化与管理。社区讨论集中在导出功能体积过大、serve 会话回收机制缺陷、Windows 平台安全弱化等问题上，其中多个 P1 级 bug 已进入讨论或修复阶段。值得关注的是，关于 Web Shell 统一聊天面板的提案仍在持续收获关注。

## 版本发布

**v0.23.1-preview.0 / v0.23.0-nightly.20260905.e3d26283e6**

两个版本均包含：
- **feat(web-shell):** 可视化管理动态工作流运行（PR #10594）
- **perf(web-shell):** 派生会话工作流项目时的性能优化

https://github.com/QwenLM/qwen-code/releases

## 社区热点 Issues

### 1. 导出功能：Mermaid 被扁平化进导出渲染器
**#11091** | `P2` · 性能 · 构建系统 | 评论 6
即便 #9812 已让导出 HTML 不再内联 renderer，Mermaid（约 6 MB）仍被打入导出 transcript renderer，导致导出文件继续膨胀。社区在持续收窄导出体积。
https://github.com/QwenLM/qwen-code/issues/11091

### 2. 导出文件内嵌完整 Web Shell runtime，空会话达 19.5 MB
**#11031** | `P1` · UI · 性能 | 评论 4
`/export html` 会把 React 与 Web Shell 完整运行时复制进每个 HTML 文件，即使空会话也达 19.5 MB。社区提出的方向是拆出只读 transcript 入口、按需加载资源。
https://github.com/QwenLM/qwen-code/issues/11031

### 3. serve：后台 shell 输出与唤醒通知在会话回收时被静默丢弃
**#11119** | `P1` · 会话管理 · daemon | 评论 3
daemon 托管的 Web Shell 会话中，`run_shell_command` 启动的后台轮询在 turn 结束后输出被丢弃，最终导致会话卡死。与 #5823 同属 background-automation 路线图下的关键问题。
https://github.com/QwenLM/qwen-code/issues/11119

### 4. 正在执行 cron / goal / monitor 任务的会话永远无法被回收
**#11118** | `P1` · 会话管理 · daemon | 评论 2
`qwen serve` 判定空闲可回收时，子进程对 "busy" 有两种不一致的定义，导致正在做后台工作的会话无法进入可回收集合，资源无法释放。
https://github.com/QwenLM/qwen-code/issues/11118

### 5. /loop cron 任务静默触发，模型无法列出或停止自己的定时任务
**#5823** | `P2` · CLI · 会话管理 | 评论 6（已关闭）
用户回到 VSCode 后发现每个新会话 Qwen 都会自动开始工作，用户完全不知情。该问题已关闭，但暴露出的 cron 可见性和可控性缺失仍值得关注。
https://github.com/QwenLM/qwen-code/issues/5823

### 6. release.yml 与 PR CI 共用 runner，互相抢占资源
**#10879** | `P1` · CI/CD | 评论 4
release 主机 hk4 由于仍带有共享 ecs-qwen label，发布验证任务会和 PR CI 在同一台宿主上抢 CPU，导致分片测试超时。已在考虑为发布任务隔离标签。
https://github.com/QwenLM/qwen-code/issues/10879

### 7. release.yml 大量重复劳动，20 分钟步骤零验证
**#11109** | `P2` · CI/CD | 评论 3
今日已有两次 release run 超时。该 issue 指出发布流程中大部分时间在重复同一 run 已完成的工作，且一步耗时 20 分钟的步骤实际上什么都没验证。
https://github.com/QwenLM/qwen-code/issues/11109

### 8. 新添加的模型无法设为当前模型：Set model failed: Invalid params
**#11112** | `P2` · 配置 · 模型切换 | 评论 2
在 Daemon Web Shell 中通过 "+ 增加模型" 添加后，点 "设为当前" 即报 `POST /session/:id/model: Invalid params`。影响模型管理与切换的核心链路。
https://github.com/QwenLM/qwen-code/issues/11112

### 9. Web Shell 中 Cmd+A 选中整页而非输入框内容
**#11108** | `P3` · UI · 快捷键 | 评论 3
macOS/Windows/Linux 下当 composer 聚焦时按 Cmd+A/Ctrl+A 会选中整页文本，与用户对输入框的预期行为不同。涉及常见编辑器体验。
https://github.com/QwenLM/qwen-code/issues/11108

### 10. 提案：聊天面板统一到 web-shell（VSCode / 桌面 / Web 共用）
**#5883** | feature-request · UI 整合 | 评论 4 · 👍 1
提出将消息流与输入 composer 标准化到 `packages/web-shell` 的最近重构上，使 Web Shell、VSCode webview 和桌面端共享同一套聊天面板实现。
https://github.com/QwenLM/qwen-code/issues/5883

## 重要 PR 进展

### 1. 模型推理能力配置（reasoning capabilities）
**#10999** | `autofix/takeover`
为 provider 模型增加声明式推理能力配置，贯通 model registry → ACP → 会话恢复 → TUI effort 控制 → OpenAI 兼容请求全链路。原生 `deepseek-v4-pro` 条目已启用。
https://github.com/QwenLM/qwen-code/pull/10999

### 2. 后台任务通知延迟投递而非静默丢弃
**#11133** | `review/self-reported`
针对 #11119 会话 runtime 回收导致通知丢失的问题，将回调清理改为延迟到 runtime 就绪后再投递，避免任务完成后通知永久丢失。
https://github.com/QwenLM/qwen-code/pull/11133

### 3. Web Shell 显示 Shell 与 Monitor 任务输出
**#10906** | `autofix/takeover`
将 Shell 与 Monitor 的 stdout/stderr 持久化，并在 Web Shell 任务详情面板中直接展示；daemon 新增限定了 live-session-owner 范围的 sanitized tail 端点。
https://github.com/QwenLM/qwen-code/pull/10906

### 4. 子代理通过 ACP 委托给外部 agent（首发 Claude Code）
**#11003**
子代理定义可声明 `executor` 命令，turn 经 ACP 驱动到外部编码 agent 执行，执行过程重新发布为子代理事件。扩展了多 agent 协作的边界。
https://github.com/QwenLM/qwen-code/pull/11003

### 5. 将全局扩展目录绑定到 workspace runtime
**#11086** | `autofix/takeover`
把扩展状态同步到各 workspace 的运行时，提供 workspace 限定的 daemon/SDK 访问，并更新了扩展管理、composer 添加菜单和 `@` 引用。
https://github.com/QwenLM/qwen-code/pull/11086

### 6. CLI 输出语言文件不可写时的启动崩溃修复
**#10455** | `review/self-reported`
每次 CLI 启动会向全局配置目录写入 output-language 文件；若主目录只读或目录创建失败，未保护的写入会直接抛错。该 PR 使此类场景不再影响启动。
https://github.com/QwenLM/qwen-code/pull/10455

### 7. /compress E2E 事件预算去 flake
**#11094** | `review/self-reported`
关闭该套件中的后台内存提取器，并放宽压缩遥测事件的等待窗口，使慢但正确的压缩不再被误判为失败。
https://github.com/QwenLM/qwen-code/pull/11094

### 8. 为 Skill frontmatter hooks 注册斜杠命令路径
**#11068** | `review/self-reported`
此前 SKILL.md frontmatter 里声明的 hooks 只在模型调用 skill 时注册；通过 `/skill-name` 斜杠命令直接调用时不会触发 hooks。该 PR 补齐了斜杠路径的 hook 注册。
https://github.com/QwenLM/qwen-code/pull/11068

### 9. 交互式 PTY 会话清理时等待进程真正结束
**#11001** | `review/self-reported`
测试 rig 在结束 PTY 会话时改为阻塞等待子进程真正退出，避免清理阶段竞态导致测试间相互污染。
https://github.com/QwenLM/qwen-code/pull/11001

### 10. compactTaskExecutionOutput 保留 skills 字段
**#11079** | test-only
在压缩 fixture 中固定 `skills` 字段，断言其不被压缩器丢弃。测试仅 8 行，无生产代码改动。
https://github.com/QwenLM/qwen-code/pull/11079

## 功能需求趋势

- **Web Shell 成为统一前端平台**：聊天面板合并（#5883）、任务输出可视化（#10906）、动态工作流管理（release）、模型设置与搜索增强（#11112、#11111）都表明社区在推动 Web Shell 作为 VSCode、桌面与 Web 的共用层。
- **后台任务生命周期治理**：cron/background 的可见性、可控性与回收问题连续出现（#5823、#11118、#11119），属 roadmap/background-automation 重点方向。
- **导出/数据可移植性**：多个 issue 围绕 export HTML 体积（#11031、#11091、#11100、#11096），要求剥离运行时依赖、按版本从 unpkg 加载、减小文件体积。
- **模型配置与能力声明**：新增模型选择报错（#11112）、推理能力配置（#10999）表明模型管理体验和不同厂商能力抽象是活跃开发区域。
- **CI/CD 稳定性与资源隔离**：release 与 PR CI 共用 runner（#10879）、release.yml 重复工作与超时（#11109）引起维护者关注。

## 开发者关注点

- **导出文件过大**：空会话 HTML 即达 19.5 MB，被认为不可接受；反复出现在多个 issue 中，开发者期望只读 transcript 入口能显著瘦身。
- **serve 后台任务状态不透明**：cron/后台 shell 的输出和通知在无人值守场景下被静默丢弃，用户无法感知任务仍在运行或已失败。
- **Windows 安全语义偏差**：`O_NOFOLLOW` 在 Windows 上缺失、dev/ino 校验形同虚设，社区希望补齐平台测试与防护（#8227）。
- **错误信息不具可操作性**：例如日志中直接输出 `[object Object]`（#11123）使用户无法定位失败原因。
- **搜索与检索局限**：会话搜索仅匹配标题而不匹配对话内容（#11111），开发者希望获得类似 Codex 的内容级搜索能力。
- **模型切换不稳**：新增模型无法“设为当前”，错误信息只给 Invalid params，未能说明具体参数问题（#11112）。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*