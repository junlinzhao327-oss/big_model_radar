# AI CLI 工具社区动态日报 2026-09-05

> 生成时间: 2026-09-05 00:11 UTC | 覆盖工具: 7 个

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



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>



</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-09-05

## 今日速览

昨日连续发布 v1.18.28、v1.18.29 两个补丁版本，核心修复了 Codex OAuth 模型过滤问题，让 `gpt-6-astra` 正确出现在 OpenAI 订阅用户的模型列表中。Issue 方面，社区对数据库无限膨胀（13GB+ event 表）、CPU 占用飙升、后台 Shell 进程挂起等稳定性问题讨论热烈，同时多名用户对 OpenCode Go 套餐的计费/配额计算提出了质疑。

---

## 版本发布

### v1.18.29
- **Bugfix：** 修复 Codex OAuth 模型过滤逻辑，使其能识别 `gpt-6` 这类整数版本号（此前版本号比较逻辑只接受小数）
- **Bugfix：** 修复 OpenAI 订阅用户看不到 `gpt-6-astra` 模型的问题
- 感谢 2 位社区贡献者，其中 @Peter267 修复了中文文档中粗体渲染需要加空格的问题

🔗 https://github.com/anomalyco/opencode/releases/tag/v1.18.29

### v1.18.28
- **Core 改进：** 将 session ID 作为 GitHub Copilot 的 interaction header 发送，改进跨会话请求追踪
- **Desktop Bugfix：** OpenCode 账户设备认证时使用桌面端 client ID
- **Desktop Bugfix：** 增大"在应用中打开"图标尺寸，提升可见性

🔗 https://github.com/anomalyco/opencode/releases/tag/v1.18.28

---

## 社区热点 Issues（Top 10）

### 1. Memory Megathread — 官方内存问题汇总贴
**#20695** | 评论 139 | 👍 108 | 状态：OPEN

官方集中追踪所有内存相关问题的 megathread，自 4 月创建以来持续活跃。项目方明确呼吁用户不要"运行 LLM 猜测解决方案"，而是提供堆快照辅助定位——说明内存问题尚未根治，仍需要大量社区数据支持。

🔗 https://github.com/anomalyco/opencode/issues/20695

### 2. 新版本 CPU 占用飙升
**#30086** | 评论 50 | 👍 26 | 状态：OPEN

用户反馈约 7 天前开始 CPU 占用大幅上涨，此前可同时运行 10+ 个 OpenCode 会话，现在 3 个会话就会导致系统卡顿、鼠标延迟。该 Issue 与 #31664（iGPU 占用 50%+）相互印证：UI 动画与后台任务调度都可能存在性能回归。

🔗 https://github.com/anomalyco/opencode/issues/30086

### 3. `event` 表无限增长，opencode.db 达 13GB+
**#33356** | 评论 27 | 👍 9 | 状态：OPEN

事件溯源架构中的 `event` 表未设置保留/压缩策略，长期运行实例的本地 SQLite 数据库可膨胀至 13GB，将 22GB 分区撑满至 97–99%。其中大部分为 `message.updated.1` 快照。评论普遍认可该问题"迟早会击中每个重度用户"。

🔗 https://github.com/anomalyco/opencode/issues/33356

### 4. GPT-6 Astra 未出现在 Codex OAuth 模型选择器中
**#47363** | 评论 2 | 👍 19 | 状态：OPEN

同一账号在官方 Codex 客户端可选 `gpt-6-astra`，但 OpenCode 的 Codex OAuth 模型列表中缺失——这正是 v1.18.29 修复的问题。高赞说明受影响用户众多，也解释了为何 24 小时内连发两个 patch。

🔗 https://github.com/anomalyco/opencode/issues/47363

### 5. VSCode 中 Context Awareness 功能无效
**#22235** | 评论 13 | 👍 7 | 状态：OPEN

用户理解该功能应与 Claude Code 类似（自动将选中代码附加到上下文），但实际从未生效，且不清楚是否有前置配置要求。IDE 集成类问题持续是社区关注重点。

🔗 https://github.com/anomalyco/opencode/issues/22235

### 6. Web UI V2 窄屏下控件重叠发送按钮
**#43295** | 评论 6 | 👍 1 | 状态：OPEN

窄视口下模型/Agent 选择控件宽度超出可用空间，直接覆盖发送按钮，用户点击发送区域反而打开了选择器。对应 PR #43298 已提交修复。

🔗 https://github.com/anomalyco/opencode/issues/43295

### 7. 插件安装器超时导致插件静默死掉/启动挂起
**#44684** | 评论 4 | 👍 0 | 状态：OPEN

v1.18.21 中插件安装时拉取 npm 公共依赖超时，报 `NpmInstallFailedError`，导致插件静默失效、headless 模式挂起。且 v1.18.20 无此问题，疑似自动更新引入的回归。国内用户同时报告了 IPv6 黑洞网络导致 `opencode-go` 卡死的问题（#36808），两者都指向网络相关的稳定性隐患。

🔗 https://github.com/anomalyco/opencode/issues/44684

### 8. Bedrock 配置的 output limit 从未发送
**#46595** | 评论 3 | 👍 1 | 状态：OPEN

V2 版本中，即使模型配置了 `limit.output: 128000`，发送给 Bedrock Converse 的请求中也不会带上 `inferenceConfig.maxTokens`。长推理场景下输出会被 Bedrock 截断在 4096 tokens，模型能力严重受限。

🔗 https://github.com/anomalyco/opencode/issues/46595

### 9. V2：空的 signed reasoning 回合被重放到后续请求
**#46881** | 评论 4 | 👍 0 | 状态：OPEN

`to-llm-message.ts` 中将"仅含空 reasoning + provider 元数据"的 assistant turn 判定为有意义内容并保留，导致历史消息重放时发送大量无意义的 provider 元数据。影响请求体积与费用，社区希望过滤逻辑能对 `part.text === ""` 的情况做更严格处理。

🔗 https://github.com/anomalyco/opencode/issues/46881

### 10. Shell 工具在后台进程持有 stdio 时永不返回
**#47350** | 评论 3 | 👍 0 | 状态：OPEN

Shell 工具将 stdout/stderr 达到 EOF 视为命令结束，而非子进程真正退出。任何命令只要留下持有管道文件描述符的后台进程，就会导致工具永久挂起。这是典型的进程生命周期语义 bug，对自动化工作流影响较大。

🔗 https://github.com/anomalyco/opencode/issues/47350

---

## 重要 PR 进展（Top 10）

### 1. 修复截断长行时破坏 Unicode 字符的问题
**#47400** | 作者: @Suzu1Dev | OPEN

修复 Legacy Read 工具与分页 Core reader 在截断超长文本（2,000 字符）时可能截断 UTF-16 代理对的问题，避免出现乱码字符。

🔗 https://github.com/anomalyco/opencode/pull/47400

### 2. 修复配置 client scope 时丢失原生 Headers 条目
**#47395** | 作者: @Suzu1Dev | OPEN

v1/v2 SDK 在同时指定 `directory` 时使用对象展开方式复制 `config.headers`，导致原生 `Headers` 实例（如 Authorization）的条目被静默丢弃。修复后改为逐项复制或做类型转换。

🔗 https://github.com/anomalyco/opencode/pull/47395

### 3. 跳过与技能目录无关的配置变更引发的全量技能重扫
**#47397** | 作者: @kitlangton | OPEN

修改 `shell` 等无关配置时，当前实现会重建整个技能目录索引、拉取远端技能列表、重建 watcher。该 PR 先对比去重后的技能配置差异，仅在来源列表变化时才触发重扫。

🔗 https://github.com/anomalyco/opencode/pull/47397

### 4. 保留启动期间发生的技能配置更新
**#47396** | 作者: @kitlangton | OPEN

技能插件只在加载完成并注册 transform 后才订阅 `config.updated`，导致启动过程中发生的配置变更（如将远端技能源替换为本地目录）会丢失。该 PR 在加载期间缓存变更，注册后回放。

🔗 https://github.com/anomalyco/opencode/pull/47396

### 5. TUI：重载本地插件的依赖图
**#47388** | 作者: @kitlangton | OPEN

编辑本地 CLI 插件的被依赖文件时，入口文件虽然获得新的 import 身份，但依赖仍被缓存，导致新导出的 helper 报 missing-export 错误。修复后插件热更新时递归刷新整个依赖图。

🔗 https://github.com/anomalyco/opencode/pull/47388

### 6. 托管 Web 端引导用户添加服务器
**#47401** | 作者: opencode-agent[bot] | OPEN

托管 Web 版打开时若附带一个无法移除的 localhost 服务器，且连接失败时，会话查询将永久 pending、首页永远显示加载骨架屏。该 PR 为托管 Web 场景增加引导用户添加服务器的提示，避免僵死。

🔗 https://github.com/anomalyco/opencode/pull/47401

### 7. Web 搜索 provider 按会话保持粘性
**#47334** | 作者: @nexxeln | OPEN

将 `websearch.provider: "random"` 模式改为在单个会话内维持所选 provider 的粘性——即每个会话开始时随机选一个 provider，但其后整个会话内保持一致，而不是每次搜索都切换 provider，减少不确定性。

🔗 https://github.com/anomalyco/opencode/pull/47334

### 8. 修复 custom-elements.d.ts 类型引用错误
**#47390** | 作者: @LuisAlbertoMK | OPEN

`custom-elements.d.ts` 的 triple-slash reference 写法无效，触发 TS1128 报错导致 enterprise 包无法通过类型检查。该 PR 修复该声明文件的格式。

🔗 https://github.com/anomalyco/opencode/pull/47390

### 9. Codex GPT 版本号按 major/minor 分别比较
**#47385** | 作者: @rekram1-node | CLOSED

#47384 的 follow-up，将 GPT 版本解析为独立的 major/minor 再比较（`major > 5 || (major === 5 && minor > 4)`），正确处理省略次版本号及整数版本的情况。已合入 v1.18.29。

🔗 https://github.com/anomalyco/opencode/pull/47385

### 10. 窄屏下保持发送按钮可见
**#43298** | 作者: @bmpenuelas | OPEN

修复 #43295：窄视口下 prompt 控件溢出并覆盖发送按钮的问题。方案是让与模型/Agent 相关的控件在空间不足时收起/换行，保证发送按钮始终可点。

🔗 https://github.com/anomalyco/opencode/pull/43298

---

## 功能需求趋势

**新模型与 Provider 支持持续高频出现。** 社区对新增模型接入始终保持高关注：本日有请求支持加拿大 AI 服务商 Augure AI（#47312）、修复 `gpt-6-astra` 在 Codex OAuth 列表中的缺失（#47363）等。模型供给的广度和更新速度是用户选择 AI 开发工具的重要考量。

**计费与配额透明化需求上升。** 两条高相关 Issue 同时出现（#39822、#47317）：用户称 OpenCode Go 订阅的 5 小时 $12 配额消耗速度远超按 API 用量推算的预期（$0.35 用量即消耗 11% 配额）。社区普遍要求提供更细粒度的用量/计费明细。

**可观测性与企业管控能力被期待。** #47351 请求在托管配置中强制下发 OTLP 设置，使企业能够统一管控遥测导出，而不是仅依赖用户本地配置。

**权限自动批准的适用范围有待扩展。** #44007 指出 `--auto` 仅对当前选中的 session 生效，后台标签页仍会被权限请求阻塞，期望 CLI 的自动批准在所有并发的 tab/session 中一致生效。

**MCP 生态持续受到关注。** 既有 #47368（1.18.28 远程 MCP 回归）等 bug 反馈，也有 #47389 这类将 MCP 工具注册移入内置插件生命周期的架构级 PR，社区对 MCP 的稳定性与可扩展性期待较高。

---

## 开发者关注点

**性能退化是当前最突出的痛点。** 多项 Issue 相互佐证：CPU 使用率飙升（#30086）、iGPU 渲染负载过高（#31664）、SQLite event 表无限膨胀至 13GB+（#33356）。三个问题的组合使重度用户在长会话场景下几乎必然会遇到卡顿或磁盘耗尽。

**挂起/无响应类问题高频出现。** 模式集中在缺少超时控制：实例服务初始化无超时可无限挂起 bootstrap（#46166）、Shell 工具因后台进程持有 stdio 永不返回（#47350）、插件安装网络超时导致启动挂起（#44684）。开发者的核心诉求是**所有 I/O 和初始化操作必须有可配置的超时与失败降级路径**。

**对配置/代码变更的响应过于激进。** 修改任何配置都会触发全部技能重扫、LSP 无闲置回收机制（#47392）、长行截断破坏 Unicode（#47399/#47400）…… 细节问题虽小，但累积起来影响日常开发流的顺畅度。

**版本更新频繁伴随新回归，社区有所警醒。** 多个 Issue（#44684、#47368）都明确指出"xx 版本之前是好的，更新后才出问题"，且 v1.18.21 → v1.18.29 一周内密集发版。社区对快速迭代持肯定态度的同时，也期望灰度范围更广、回归测试更完善。

---

> 数据来源：[github.com/anomalyco/opencode](https://github.com/anomalyco/opencode) | 统计时段：2026-09-04 至 2026-09-05 | 本日报由 AI 自动生成

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-09-05

## 今日速览

过去 24 小时 Qwen Code 仓库无新版本发布，但社区讨论热度集中在几项 P1/P2 级缺陷上：Cerebras 提供商多轮请求 400 错误、`/export html` 产物体积过大、以及依赖 CVE 审计全线失败。核心功能层面，OpenTUI 渲染层迁移的跟踪 issue #8662（30 条评论）持续升温，成为社区最关注的结构性议题；与此同时，AUTO 模式审批绕过修复（#11025）、动态工作流对标 Claude Code 差距跟进（#11013）等 PR/Issue 也反映了项目在 agent 能力深水区的持续打磨。

---
## 社区热点 Issues

### 1. [TUI 渲染层从 ink 迁移到 OpenTUI（跟踪议题）](https://github.com/QwenLM/qwen-code/issues/8662)
- **优先级/标签**：P3、enhancement、terminal-ux、tracking
- **背景**：Qwen Code 现用的 TUI 构建在 heavily patched ink 7 + React 19 之上，补丁量达 1037 行，且存在难以在 ink 框架内根治的闪烁/渲染结构性问题。
- **为何重要**：评论数 30 条，为过去 24 小时讨论热度最高。该迁移直接影响所有交互式 CLI 用户的终端体验，是多个 UI 衍生 bug（如 #8177、#10905）的根因跟踪地。

### 2. [Cerebras（OpenAI 兼容）多轮请求全部失败：reasoning_content 被拒绝](https://github.com/QwenLM/qwen-code/issues/11045)
- **优先级/标签**：P1、bug、content-generation
- **现象**：经 OpenAI 兼容 provider 使用 Cerebras 托管模型时，首轮成功，后续每轮均报 `400 status code (no body)`。
- **为何重要**：P1 缺陷，直接阻断 Cerebras 用户的全部多轮会话。涉及 request body 中 reasoning 字段兼容性的通用问题，同类 provider 可能也受影响。

### 3. [`/export html` 将 Web Shell 运行时嵌入每个导出文件，空会话产物达 19.5MB](https://github.com/QwenLM/qwen-code/issues/11031)
- **优先级/标签**：P1、bug、performance、web-shell、export-data
- **现象**：每次导出 HTML 都携带完整 React + Web Shell 运行时依赖图，即使空会话文件也达到 19.5 MB。
- **为何重要**：P1 性能问题，直接影响所有使用导出功能的用户的文件分发效率和工具加载体验。

### 4. [语音听写无法使用 Token Plan ASR：resolveVoiceTransport 拒绝新模型 ID](https://github.com/QwenLM/qwen-code/issues/10932)
- **优先级/标签**：P2、bug、interactive、model-switching、ready-for-human
- **现象**：语音管线硬编码旧 ASR 模型 ID，导致 `qwen-audio-3.0-asr-flash` 等新 Token Plan 模型被拒绝，麦克风采集正常但无法转录。
- **为何重要**：语音功能是差异化卖点，模型 ID 硬编码问题暴露了 provider 模型演进与本地 allowlist 的同步滞后。

### 5. [macOS + tmux 本地 session 中输入法导致光标错位/文本乱码](https://github.com/QwenLM/qwen-code/issues/8177)
- **优先级/标签**：P2、bug、ui、rendering、macos、IME
- **现象**：中文输入时出现光标残影、拼音混入已输入文本、IME 候选窗与终端渲染重叠。
- **为何重要**：issue 已存活超一个月仍有持续更新（4 条评论），反映 TUI 在 IME 场景下的渲染顽疾，对中文用户是高频痛点。

### 6. [CI 测试时间被模块导入成本卡住，而非调度问题](https://github.com/QwenLM/qwen-code/issues/10908)
- **优先级/标签**：P2、enhancement、performance、ci-cd、testing
- **数据**：`cli` workspace 的 collect 耗时 2223s，而实际 tests 仅 1372s；core 同样为 546s vs 251s。
- **为何重要**：社区持续关注 CI 效率问题，该 issue 揭示了模块加载耗时已超越测试执行本身，需要结构性优化（如依赖预构建、按需加载）。

### 7. [Todo 计划状态在委托给 subagent 后过期（active-todo 提醒不再触发）](https://github.com/QwenLM/qwen-code/issues/10953)
- **优先级/标签**：P2、bug、session-management、subagents-tools、dogfooding
- **现象**：会话将大部分工作委托给前台 subagent 后，持久化的 Todo 计划冻结了 55 分 44 秒，实际工作已推进了 4 个计划节点。
- **为何重要**：影响多 agent 协作场景的进度可视性和提醒可靠性，是 subagent 工作流落地过程中的真实短板。

### 8. [为 thinking/reasoning 输出提供可插拔语言改写中间件](https://github.com/QwenLM/qwen-code/issues/10872)
- **优先级/标签**：P2、feature-request、core、extensions
- **诉求**：希望新增公开的中间件 API，在 thinking 输出发送给客户端之前做转换（如翻译成用户目标语言），同时支持交互式 CLI 和 `qwen serve` 守护进程。
- **为何重要**：与 #3787（ACP 模式下 thinking 语言与用户语言不一致）相互呼应，说明多语言用户对推理过程语言控制有持续需求。

### 9. [AUTO 模式下用户审批永远无法到达分类器，阻止不可覆盖；审批模式在重建会话后回退为 AUTO](https://github.com/QwenLM/qwen-code/issues/11019)
- **优先级/标签**：P2、bug、security、session-management、daemon、need-discussion
- **现象**：在 API 驱动的 host harness 中，agent 三次询问用户确认，用户三次肯定，但后续工具调用仍被阻断。
- **为何重要**：涉及安全审批链路的可靠性和状态持久化，直接影响生产环境数据变更场景的可控性。

### 10. [依赖 CVE 审计全线失败：fast-uri/qs/uuid 新公告影响主 lockfile](https://github.com/QwenLM/qwen-code/issues/10850)
- **优先级/标签**：P1、security、ci-cd、ready-for-human
- **数据**：`npm audit --omit=dev` 报告 4 个漏洞（1 low、2 moderate、1 high），影响 fast-uri、qs、uuid 等基础依赖。
- **为何重要**：P1 安全且 CI 全线变红，依赖链的漏洞响应速度直接影响项目可信度。

---
## 重要 PR 进展

### 1. [fix(core): allow manual retry after auto mode blocks](https://github.com/QwenLM/qwen-code/pull/11025)
- **内容**：AUTO 模式在分类器策略阻断后，现在提供一次性手动审查路径——相同工具、相同参数、相同工作目录的重试将绕过分类器并打开既有确认 UI；若工具/参数/目录变化则不做绕过。
- **关联**：直接回应 issue #11019，是审批可靠性问题的重要修复。

### 2. [feat(ipc): hold peer messages across review classes, let repositories only tighten inbound settings](https://github.com/QwenLM/qwen-code/pull/11026)
- **内容**：修复了跨会话入站审批矩阵的一处逻辑漏洞：此前未显式设置 `agents.crossSessionInbound` 时，接收方若审查每个动作，会接受来自任意发送方的所有消息。新逻辑让仓库只能收紧而不能放宽入站设置。
- **意义**：agent 间通信安全边界的收敛，防止越权消息渗透。

### 3. [feat(core): make todo_write opt-in](https://github.com/QwenLM/qwen-code/pull/10645)
- **内容**：将 `todo_write` 工具从默认工具面移除，改为通过 `tools.todoWrite.enabled: true` 显式开启。禁用时默认系统提示词和 Agent 工具 schema 同步调整。
- **讨论焦点**：需要 27 天仍未合并，社区对其是否符合默认 UX 存在分歧；但该 PR 对保持 prompt 精简有积极意义。

### 4. [feat(core): send session ID to Routify endpoints](https://github.com/QwenLM/qwen-code/pull/10896)
- **内容**：向 Routify 三个域的 HTTPS LLM 请求增加 `session_id` header，便于路由端做会话级观测与调度。
- **意义**：提升模型路由的可观测性，对企业用户尤为实用。

### 5. [perf(cli): reduce virtualized history scroll latency](https://github.com/QwenLM/qwen-code/pull/10043)
- **内容**：虚拟化历史滚动改为 leading-edge + deadline-aware 调度：首次滚轮/拖拽立即生效，16ms 窗口内的后续更新保持合并，超预算渲染后的更新不再阻塞等待。
- **意义**：直接改善长会话终端的滚动跟手度，是 UI 性能的精细优化。

### 6. [fix(cli): wait for the startup chat before an OpenTUI turn sends](https://github.com/QwenLM/qwen-code/pull/11046)
- **内容**：修复 OpenTUI 渲染器中会话启动瞬间输入被静默丢弃的问题——composer 已就绪但底层会话未初始化完成，导致 turn 立即以 `Chat not initialized` 结束。
- **关联**：对应 issue #11042，影响新会话启动时的首条消息。

### 7. [test(e2e): pass the harness's 60s initialize budget in qwen-serve-streaming](https://github.com/QwenLM/qwen-code/pull/11051)
- **内容**：为 `qwen-serve-streaming.test.ts` 传入 `--initialize-timeout-ms 60000`，与共享 daemon harness 对齐，避免套件沿用默认 10s 超时而导致的 E2E 失败。
- **意义**：CI 稳定性修复，解决主分支 E2E 测试反复失败的问题。

### 8. [refactor: anchor rewind mapping to stable prompt identity](https://github.com/QwenLM/qwen-code/pull/9466)
- **内容**：将 rewind（回退）映射从基于位置/轮次改为基于持久化的 prompt identity，使回退在会话恢复、headless `-p --rewind` 等会重排轮次的场景下仍精确命中目标。
- **意义**：多界面场景下回退一致性的关键架构调整。

### 9. [feat(core): auto-retry transient network errors (EOF) where Ctrl+Y is unavailable](https://github.com/QwenLM/qwen-code/pull/10347)
- **内容**：将 `400 network error ... EOF` 等实际为底层网络故障的错误归类为可重试传输错误，纳入有界自动重试，而不是 fail-fast。
- **意义**：改善不稳定网络环境下 headless/通道场景的健壮性，避免用户手动干预。

### 10. [feat(web-shell): make Session Workflow dependencies navigable and quiet its chrome](https://github.com/QwenLM/qwen-code/pull/10938)
- **内容**：补全 Session Workflow 界面的导航、形态与文档缺口：

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*