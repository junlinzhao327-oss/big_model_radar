# AI CLI 工具社区动态日报 2026-09-05

> 生成时间: 2026-09-04 22:35 UTC | 覆盖工具: 7 个

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

## Kimi Code CLI 社区动态日报（2026-09-05）

### 今日速览

过去 24 小时无新版本发布，社区动态主要集中在历史 Issue 的闭环与一项 PR 的推进：多个与 CLI 稳定性、终端体验及扩展机制相关的 Issue 被标记关闭，但与此同时 MCP 超时导致的整体不可用问题仍值得警惕。当前最活跃的 Open Issue #2634 聚焦 Windows Terminal 下按键改键失败，直接影响开发者编辑效率。

---

### 社区热点 Issues

> 当前时间窗口内共更新 7 个 Issue，均已列出；其中 #2634 为唯一 Open 状态，其余为近期 Closed。

- **#2634 [bug] kimi 终端改键位不成功，比如粘贴**（唯一新开启）  
  运行 0.40.1 版本，在 Windows Terminal + PowerShell 中 Ctrl+V 无法粘贴，与终端内部键位设置冲突有关。  
  链接: https://github.com/MoonshotAI/kimi-cli/issues/2634

- **#1316 [bug] MCP timeout 导致 kimi-cli 不可用**  
  当某个 MCP 连接超时，整个 CLI 被中断甚至挂起，缺少超时隔离与降级机制。更新于 2026-09-04，已过关闭，但该问题对依赖外部工具链的自动化场景影响显著。  
  链接: https://github.com/MoonshotAI/kimi-cli/issues/1316

- **#1315 [bug] Subagents keep running after hitting ESC**  
  在 Windows 上按 ESC 后，Task 子代理仍在后台继续执行，用户无法安全可靠地中断任务。涉及进程生命周期管理。  
  链接: https://github.com/MoonshotAI/kimi-cli/issues/1315

- **#1313 [enhancement] Add Hooks System for Notifications and Lifecycle Events**  
  用户希望引入 Hooks 机制，在长任务需要关注或事件触发时主动通知，避免一直盯着终端。获得 3 个 👍，反映真实需求。  
  链接: https://github.com/MoonshotAI/kimi-cli/issues/1313

- **#1319 [enhancement] 增加本地 skills 操作管理的方法**  
  建议提供 `/skills list`、`/skills rm` 等指令，统一查看版本、触发词、删除本地 skill，解决当前目录及管理方式不统一的问题。  
  链接: https://github.com/MoonshotAI/kimi-cli/issues/1319

- **#1320 [enhancement] Smart arrow key navigation for multiline input**  
  多行编辑中按上/下键总是切换历史记录，希望光标在当前多行文本内时优先做光标移动，类似常见编辑器的行为。  
  链接: https://github.com/MoonshotAI/kimi-cli/issues/1320

- **#290 [bug] Use openrouter with custom model returns 401**  
  使用 OpenRouter 自定义模型（gpt-5.1-codex）通过 kimi-for-coding 平台返回 401。较早期 Issue 于 2026-09-03 关闭。  
  链接: https://github.com/MoonshotAI/kimi-cli/issues/290

---

### 重要 PR 进展

> 过去 24 小时内仅 1 个 PR 有动态更新。

- **#2524 fix(tools): count StrReplaceFile replacements against the running content**  
  修复 `StrReplaceFile` 工具在链式编辑场景中的替换计数逻辑，避免因基于原始文件内容计数而漏算新增变更。相关 Issue: #2526。  
  链接: https://github.com/MoonshotAI/kimi-cli/pull/2524

---

### 功能需求趋势

- **MCP 健壮性与故障隔离**  
  现有 Issue 表明 MCP 超时会拖垮整个 CLI，社区需要更细粒度的错误隔离、超时配置与自动恢复机制。

- **终端交互细节改进**  
  包括：Windows 下键位绑定与粘贴行为、多行文本中方向键的智能导航、Esc 是否能真正中止子进程或子代理。

- **本地技能（Skills）管理能力**  
  开发者不满足于仅通过 `/skill` 加载，需要统一的查看、删除、版本管理入口，与 MCP 交互管理保持一致。

- **外部事件挂钩（Hooks）与通知**  
  面向长时间后台任务场景，社区越来越希望有生命周期事件、输出关键词等触发通知的方式，便于用户切换上下文。

---

### 开发者关注点

1. **终端环境兼容性不稳定**  
  尤其是 Windows Terminal + PowerShell 下的键位、粘贴与中断行为反复出现兼容问题，建议加强跨平台终端能力测试。

2. **MCP 单点故障影响面过大**  
  某一个 MCP 连接异常就直接中断整个 kimi-cli，引发对“默认安全”与依赖隔离的讨论。

3. **多行输入与命令历史的操作歧义**  
  在多行编辑场景中，用户希望方向键行为随光标位置变化，当前固定映射为历史导航造成明显心智负担。

4. **对子代理与后台任务的控制期待**  
  开发者希望有明确的中断契约，目前按 ESC 后子代理仍可能继续执行，会让用户对“停止”动作失去信任。

5. **扩展机制的完备性**  
  从 Hooks 提案和 Skills 管理需求看，社区不仅满足于开箱即用的 Agent 能力，也开始对 CLI 本身提出更高可扩展性要求。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-09-05

> 数据来源：github.com/anomalyco/opencode（过去 24 小时动态）

## 1. 今日速览

昨日发布 **v1.18.28**，核心改进是向 GitHub Copilot 交互请求中注入会话 ID、修复桌面端设备认证 ID。社区焦点仍集中在**性能问题**（CPU 飙升、SQLite 数据库膨胀至 13GB、内存泄漏），同时 **Zen/Go 网关计费与免费模型额度异常**（#47318、#39822、#47349）成为最新投诉热点，反映出模型供给与计费系统正在经受较大规模的真实流量考验。

## 2. 版本发布

### v1.18.28
> 链接：https://github.com/anomalyco/opencode/releases

- **Core**：发送会话 ID 作为 GitHub Copilot 的交互头，以改善跨会话的请求追踪。
- **Desktop**：
  - 修复设备认证流程中未使用桌面客户端 ID 的问题。
  - 增大“在应用中打开”图标尺寸，提升可见性。

## 3. 社区热点 Issues（Top 10）

1. **#20695 Memory Megathread — 内存问题集中贴**
   ，评论 139 👍 108 | 更新 09-04
   社区内存/堆快照问题的唯一聚合地，作者明确提醒用户不要用 LLM 猜测解决方案，需提供 heap snapshots 辅助定位。
   https://github.com/anomalyco/opencode/issues/20695

2. **#6231 Auto-discover models from OpenAI-compatible providers**
   ，评论 52 👍 228 | 更新 09-04
   高赞需求：对 LM Studio/Ollama/llama.cpp 等本地 OpenAI 兼容端点，应自动发现模型，而非手动写入 `opencode.json`。反映本地模型工作流已成为重要使用场景。
   https://github.com/anomalyco/opencode/issues/6231

3. **#30086 High CPU usage in newer versions**
   ，评论 50 👍 26 | 更新 09-04
   此前可同时开 10+ 会话，近期更新后 3 个会话即导致 CPU 飙升、鼠标卡顿。用户反馈指向近 7 天内的回归。
   https://github.com/anomalyco/opencode/issues/30086

4. **#33356 [2.0] event 表无界增长 — opencode.db 达 13GB+**
   ，评论 27 | 更新 09-04
   事件溯源表从不清理/压缩，长运行实例中数据库膨胀至 13GB、磁盘占用 97-99%。V2 架构下数据生命周期管理缺失。
   https://github.com/anomalyco/opencode/issues/33356

5. **#22235 IDE (VSCode)：Context Awareness 不生效**
   ，评论 13 👍 7 | 更新 09-04
   类似 Claude Code 的自动上下文附加功能未在 VSCode 中生效，用户困惑于是否需要额外配置。IDE 集成仍是高频短板。
   https://github.com/anomalyco/opencode/issues/22235

6. **#47318 Limit Exceeded — Zen 免费模型提示额度超限**
   ，评论 4 | 创建 09-04
   用户使用标示为“完全免费”的 Muse Spark 1.2/1.3 却收到 “Free usage exceeded, subscribe to Go”。免费额度判定逻辑疑似有误。
   https://github.com/anomalyco/opencode/issues/47318

7. **#43295 Web UI V2 prompt 控件在窄屏遮挡发送按钮**
   ，评论 6 | 更新 09-04
   窄视口下 agent/model 控件与发送按钮重叠，点击发送区域反而触发选择器。
   https://github.com/anomalyco/opencode/issues/43295

8. **#44684 1.18.21 插件安装器从 npm 获取公共依赖超时**
   ，评论 4 | 更新 09-04
   升级后从 registry.npmjs.org 拉取公共依赖超时，导致插件静默失效、headless 模式带插件启动挂起。从 1.18.20 起引入的回归。
   https://github.com/anomalyco/opencode/issues/44684

9. **#46881 [2.0] 仅含签名空推理的回合被重放至后续请求**
   ，评论 4 | 更新 09-04
   V2 会话 runner 会把仅含 provider 元数据与空文本的助手回合重新注入后续 LLM 请求，`signed-empty reasoning` 处理逻辑有缺陷。
   https://github.com/anomalyco/opencode/issues/46881

10. **#47368 1.18.28 远程 MCP 回归 — KitWright 工具不可用**
    ，评论 2 | 创建 09-04
    从 1.18.27 升级后，原本正常工作的远程 MCP 服务器（127.0.0.1:9155）无法连接，疑似 1.18.28 的回归。
    https://github.com/anomalyco/opencode/issues/47368

## 4. 重要 PR 进展（Top 10）

1. **[contributor] feat(worktree): 支持可配置插件策略**
   ，PR #47358 | 新增 `worktree.directory` 配置与 Effect/Promise 插件策略注册，将 worktree 能力插件化。
   https://github.com/anomalyco/opencode/pull/47358

2. **feat(core): transcript recall index — 语义化历史会话检索**
   ，PR #46850 | 本地 transcript embedding 索引实现跨会话语义搜索，Closes #41354。对长会话用户是重要效率提升。
   https://github.com/anomalyco/opencode/pull/46850

3. **[contributor] feat(app): 可选 PWA 推送通知**
   ，PR #47374 | 为 Web/PWA 增加后台通知（响应就绪、会话错误），服务端直连浏览器推送服务，无需 Electron 封装。
   https://github.com/anomalyco/opencode/pull/47374

4. **[contributor] fix(tui): 新建会话时保留预览标签**
   ，PR #47376 | 通过 `/new`、`/clear`、快捷键或 `+` 进入新会话页时，将临时会话标签转为固定标签。
   https://github.com/anomalyco/opencode/pull/47376

5. **[contributor] fix(app): 新会话 prompt 宽度扩展到 logo 之外**
   ，PR #47375 | prompt 宽度 720px→880px，logo 保持 720px 居中；小窗口下保留响应式尺寸。
   https://github.com/anomalyco/opencode/pull/47375

6. **[contributor] fix(app): 移除新会话 logo 淡入渐变并调节不透明度**
   ，PR #47378 | 默认 Wordmark 外观不变，新会话 logo 深色模式透明度 50%、浅色 40%。依赖 #47375。
   https://github.com/anomalyco/opencode/pull/47378

7. **[contributor] fix(app): 保持 pending-worktree composer 样式一致**
   ，PR #47377 | 修复 pending-worktree 视图未应用深色 composer 表面、且占位符被覆盖的问题。
   https://github.com/anomalyco/opencode/pull/47377

8. **fix(app): 桌面端 worktree 位置与 TUI 对齐**
   ，PR #47370 | 桌面端不再在仓库旁建 worktree，改用与 TUI 一致的项目数据目录；未显式指定时由服务端解析 `XDG_DATA_HOME`。
   https://github.com/anomalyco/opencode/pull/47370

9. **fix(tui): 重试“歧义提示”提交**
   ，PR #40523 | 修复因服务传输中断导致草稿保留、再次回车产生重复会话 ID 的问题。
   https://github.com/anomalyco/opencode/pull/40523

10. **fix(core): 恢复 Bedrock 默认 AWS 凭证链**
    ，PR #40522 | 在 #40165 将 Bedrock 路由移出 AI SDK 后丢失了默认凭证链支持，此 PR 恢复 profile、SSO、实例角色等解析，由服务端统一负责。
    https://github.com/anomalyco/opencode/pull/40522

## 5. 功能需求趋势

- **统一/订阅计费透明度**：多起 “免费模型限额外”、“Go 套餐用量计算与预期不符” 的 issue（#47318、#39822、#47349）显示，用户对 Zen/Go 网关的配额计算与“免费额度”定义极为敏感，价格信任成本正在上升。
- **按需模型发现与接入**：#6231（OpenAI 兼容端点自动发现模型）以 228 👍 高居榜首；新增模型支持请求持续出现（如 #47312 Augure AI）。
- **性能与资源治理**：CPU 回归（#30086）、SQLite 无界增长（#33356）、内存聚合贴（#20695）表明，V2 的数据生命周期与动画渲染开销已成为社区核心痛点。
- **V2/TUI 交互完成度**：会话标签生命周期（#47376）、窄屏/窄终端适配（#43295、#40435）等细节打磨 PR 密集出现，V2 正在经历工程化收尾。
- **插件与扩展机制演进**：worktree 策略可配置化（#47358）延续了将能力下沉为注册式插件的方向。

## 6. 开发者关注点

- **更新即回归**：1.18.21 的插件 npm 超时、1.18.28 的远程 MCP 回归，再叠加 #30086 的 CPU 飙升，使开发者对“自动更新”产生警惕，反馈中频繁出现“升级前一切正常”的字样。
- **低配机器与长会话用户付出性能代价**：多处抱怨集中在 3-5 个后台会话即让机器卡顿、数据库膨胀至 GB 级、重放冗余推理消息——这些对本地资源有限的用户尤为致命。
- **从“能用”到“可信”的计费/额度诉求**：免费模型显示超限、Go 套餐用量与账单不一致、地区性 IPv6 连接失败导致无法使用，属于影响信任的全局性阻断问题。
- **IDE/桌面体验细节**：Context Awareness 不生效、桌面与 TUI 的 worktree 路径不一致、窄屏 UI 重叠等问题，显示官方当前重心在核心架构（V2 数据层/性能治理），周边客户端体验仍需补课。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-09-05）

## 今日速览

过去 24 小时无新版本 Release，社区活跃度集中在渲染层重构、会话生命周期与安全合规三条主线上。OpenTUI 迁移（#8662）继续作为架构级追踪项积累讨论；多个 P1 级问题待处理——Cerebras 多轮请求失败、依赖 CVE 审计失败、Bash 允许规则绕过等。后台会话管理（Agent View）与 CI 导入性能优化则成为 PR 侧最集中的进展方向。

## 社区热点 Issues

**1. OpenTUI 渲染层迁移追踪 —— 终端体验重构的核心议题**
[#8662](https://github.com/QwenLM/qwen-code/issues/8662)（评论 30，P3/追踪）：当前 TUI 基于 ink 7 + React 19 及约 1037 行补丁，闪烁与结构性问题难以根除，官方正在推进向 OpenTUI 的整体迁移。这是 roadmap/terminal-ux 最值得关注的架构级变更，直接决定未来终端交互体验走向。

**2. Cerebras 多轮请求全部失败：reasoning_content 被上游拒收**
[#11045](https://github.com/QwenLM/qwen-code/issues/11045)（评论 3，P1）：通过 OpenAI 兼容 provider 使用 Cerebras 模型时，首轮成功、后续轮次全部返回 `400 status code (no body)`。根因指向将 `reasoning_content` 回传输入，属于跨模型网关兼容性问题，对第三方模型接入是阻断级缺陷。

**3. CI 测试耗时受模块导入成本拖累**
[#10908](https://github.com/QwenLM/qwen-code/issues/10908)（评论 8，P2）：Release CI 中 `cli` workspace 的模块导入收集耗时

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*