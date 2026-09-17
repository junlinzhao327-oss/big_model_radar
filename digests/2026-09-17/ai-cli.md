# AI CLI 工具社区动态日报 2026-09-17

> 生成时间: 2026-09-17 00:39 UTC | 覆盖工具: 7 个

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
**日期：2026-09-17｜口径：基于所给 GitHub 公开摘要，非全量 API 统计**

> 数据边界：Claude Code、Codex、Copilot CLI、Kimi CLI、OpenCode 有可用摘要；Gemini CLI、Qwen Code 本期内容为空。部分工具原文截断，PR/Issue 精确总数无法确认，下表以“摘要中可见”为准，避免虚构全量数据。

---

## 1. 生态全景

当前 AI CLI 工具已从“能不能用”进入“能不能稳定运营”的阶段：多端扩展、MCP 生态、多代理编排、权限沙箱、额度成本成为共同战场。发布节奏明显分化——Codex 处于高频 alpha 迭代，Copilot/Claude 走稳定小版本，OpenCode/Kimi 则更依赖社区修复或早期验证。社区痛点从功能缺失转向可靠性、可诊断性与成本控制：静默失败、限流重试、认证阻断、升级回归最伤用户信任。同时，Desktop/Web/IDE 与 CLI 的能力对齐、UI 可回退性，正在成为新的体验竞争点。

---

## 2. 各工具活跃度对比

| 工具 | 摘要中可见 Issues | PR 动态 | Release 情况 | 活跃度判断 |
|---|---|---|---|---|
| **Claude Code** | Top 10 + 3 条今日新提交被点名 | 3 条 PR，均集中在 `mods/diff` 面板策略 | **v2.1.274**，新增内存告警、MCP 启动等待环境变量、CLI `effort` | 高活跃、平台成熟；治理

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

## Claude Code Skills 社区热点报告  
数据截止：2026-09-17  
说明：PR 评论数字段缺失，无法严格按评论数排序；以下结合原始列表顺序、更新时间与关联 Issue 综合判断。样本中

---

# Claude Code 社区动态日报

**日期：2026-09-17** ｜ 数据来源：github.com/anthropics/claude-code

---

## 1. 今日速览

- 发布 **v2.1.274**，新增内存临界告警与 `CLAUDE_CODE_MCP_STARTUP_WAIT_MS` 环境变量，用于约束非交互首轮等待 MCP 服务器连接的时间；同时为 CLI 配置引入 `effort` 属性。
- 社区讨论集中在 **桌面端 / Desktop 的稳定性与可配置性**：MCP 配置路径错误、Remote Control 403、浏览器面板权限与会话生命周期问题占据了评论数前列。
- 值得注意的治理动向：昨日有一批 7 月提交的 enhancement 被 **stale 机器人批量关闭**（#81837、#81856、#81883、#81889、#81892、#81895、#81897、#81928、#81943 等），提示社区对需求积压处理的关注度可能上升。

---

## 2. 版本发布

### v2.1.274
- **内存告警**：内存占用达到临界值时显示可见警告，并给出释放内存或安全重启的步骤。
- **新增环境变量 `CLAUDE_CODE_MCP_STARTUP_WAIT_MS`**：限定首次非交互轮次等待 MCP 服务器连接的最长时间（设为 `0` 表示不等待）。这对 CI、脚本化调用场景下的启动可预测性非常关键。
- **CLI 配置新增 `effort` 属性**：与模型推理档位（effort tier）相关的配置项开始暴露到 CLI 配置层。

> 关联社区反馈：#94893 报告 `effortLevel` 设置无法持久化 UI 提供的 "Max" 档位，v2.1.274 的 `effort` 属性可能与该问题方向相关，建议关注后续是否闭环。

---

## 3. 社区热点 Issues（Top 10）

| # | Issue | 状态 | 热度 | 关注理由 |
|---|---|---|---|---|
| 1 | [#26073](https://github.com/anthropics/claude-code/issues/26073) Windows MSIX "Edit Config" 打开错误的 `claude_desktop_config.json` | OPEN | 23 评论 / 👍33 | 本日讨论量最高。MCP 服务器**静默加载失败**属于最难排查的一类问题，且已持续 7 个月未修复，跨平台桌面端配置路径管理是明显短板。 |
| 2 | [#42700](https://github.com/anthropics/claude-code/issues/42700) 响应 TTS 朗读 + Remote Control 会话的语音模式 | OPEN | 22 评论 / 👍30 | 高赞无障碍/语音需求，与 Remote Control 远程会话场景强绑定，反映社区对"非手不离键盘"交互范式的期待。 |
| 3 | [#87500](https://github.com/anthropics/claude-code/issues/87500) 持续出现 `ECONNRESET` API 连接中断 | CLOSED | 9 评论 | 网络层错误影响 Windows 平台可用性，虽已关闭但用户侧报告"持续 5 小时不可用"，提示需关注连接稳定性与错误可诊断性。 |
| 4 | [#79305](https://github.com/anthropics/claude-code/issues/79305) Desktop 支持自定义主题/强调色（对齐 CLI 主题系统） | OPEN | 8 评论 / 👍16 | 典型的 **CLI 与 Desktop 能力不对等**诉求；多显示器用户靠颜色识别窗口，属于低成本高感知的体验改进。 |
| 5 | [#82700](https://github.com/anthropics/claude-code/issues/82700) Pro 订阅被阻断："organization has disabled subscription access" | OPEN | 7 评论 | 认证/授权链路问题，用户完成全量重新鉴权与支持升级后仍未解决，涉及付费可用性，优先级应高。 |
| 6 | [#91717](https://github.com/anthropics/claude-code/issues/91717) 桌面更新后 Remote Control 返回 HTTP 403，`/remote-control` 重试无法恢复 | OPEN | 5 评论 | 带 `has repro` 标签，属于**升级回归**类缺陷，远程控制是新功能面，回归会直接影响信任度。 |
| 7 | [#93156](https://github.com/anthropics/claude-code/issues/93156) 浏览器面板无法授予持久站点权限 | OPEN | 5 评论 | 即使配置 `launchPreviewAllowedOrigins`、工具白名单与 `bypassPermissions` 也无效，弹窗只有"拒绝/允许一次"。权限模型的设计缺口，会显著拖慢自动化工作流。 |
| 8 | [#93835](https://github.com/anthropics/claude-code/issues/93835) VSCode 扩展会话列表只能归档，无法删除 | OPEN | 4 评论 / 👍5 | IDE 集成侧的会话管理能力缺失，长期使用后列表不可控，属于高频日常痛点。 |
| 9 | [#94893](https://github.com/anthropics/claude-code/issues/94893) `effortLevel` 无法持久化 UI 提供的 "Max" 档位 | CLOSED | 1 评论 | 状态栏确认选择为 `Opus 5 Max`，但 `max` 无法写入配置。与今日 v2.1.274 的 `effort` 属性直接呼应，是版本发布后的即时验证点。 |
| 10 | [#94415](https://github.com/anthropics/claude-code/issues/94415) Cowork 云调度任务在设备休眠后永久禁用、无法自动恢复 | OPEN | 2 评论 | 带 `has repro`；`suspension_reason=device_absent` 后不再自动恢复，暴露出云端调度与本地设备状态耦合的可靠性风险。 |

**其他值得留意的新提交（今日创建）**
- [#94897](https://github.com/anthropics/claude-code/issues/94897) macOS MFA 验证失败："Could not verify the account security policy"（认证阻断）。
- [#94898](https://github.com/anthropics/claude-code/issues/94898) Desktop Code 侧栏在 `Group by: None` 时显示项目文件夹名。
- [#94771](https://github.com/anthropics/claude-code/issues/94771) Web 端 Stop hook 在 squash merge 删除远程分支后误报 "unpushed commit(s)"。

---

## 4. 重要 PR 进展

> ⚠️ 说明：过去 24 小时内仅有 **3 条 PR** 更新，均为 `mods/diff`（差异预览面板）相关的小范围修复，无法凑满 10 条。以下为全部内容。

1. [#94847](https://github.com/anthropics/claude-code/pull/94847) **OPEN**｜diff：仅在确有文件可列出时才打开面板（作者 @bcherny）
   - 修复点：此前会话首次成功的 Edit / Write / NotebookEdit 会**在拉取数据之前**自动打开面板；当写入发生在仓库外、被忽略的文件或不同 worktree 时，会弹出一个空面板（"No tracked changes"）。现在改为有内容才展开。

2. [#94843](https://github.com/anthropics/claude-code/pull/94843) **CLOSED**｜diff：提示文案 hook 读取 viewport 布局的方式可能在类型上不成立（作者 @poteat）
   - 修复点：`mods/diff` 在提示 hook 中读取 `viewport.isFullscreen`，当引擎的 `RenderViewport` 尚未声明该字段时类型检查失败（运行时行为其实正确）。改为更安全的读取方式，属于类型健壮性修复。

3. [#94653](https://github.com/anthropics/claude-code/pull/94653) **CLOSED**｜diff：仅在布局支持停靠的位置打开面板（作者 @poteat）
   - 修复点：此前只要终端宽度 ≥144 列就打开面板，但主屏模式（`CLAUDE_CODE_NO_FLICKER=0`）下没有停靠能力，面板会以内联形式挤在输入框上方。现在按布局能力判断。

**观察**：三条 PR 都指向同一模块的"面板自动打开策略"，可以看出 diff 面板的**触发时机与布局判定**正在被系统性收敛——建议关注该模块后续是否会有统一的布局/生命周期抽象。

---

## 5. 功能需求趋势

从本期 50 条 Issue 中可提炼出以下方向：

- **Desktop 与 CLI 的能力对齐（最集中）**
  自定义主题/强调色（#79305）、字体大小（#94208）、UI 密度（#81883）、隐藏 diff 预览（#81889）、会话标题旁显示项目目录（#94898）。桌面端正被要求补齐 CLI/TUI 已有的可配置性。
- **权限模型的持久化与可预测性**
  浏览器面板无法"始终允许"（#93156）、站点级权限与 `bypassPermissions` 语义不一致。开发者希望一次授权、长期生效，而非逐动作弹窗。
- **MCP 生态的可靠性与可观测性**
  配置路径错误导致静默失败（#26073）；官方则以 `CLAUDE_CODE_MCP_STARTUP_WAIT_MS` 回应启动时序可控性。方向明确：**MCP 需要更好的错误暴露与启动边界控制**。
- **远程/云端会话（Remote Control、Cowork、Web）的稳定性**
  403 回归（#91717）、云调度任务休眠后不恢复（#94415）、Web 端 Stop hook 误报（#94771）。远程执行链路的会话生命周期管理是新的问题密集区。
- **Agent / 子会话编排原语**
  程序化批量派生命名子会话（#89783）、会话 pinning 在 CLI 不可见（#82581）。社区在期待**非交互式的 agent 编排 API**，而不只是 UI 点击。
- **语音与无障碍（a11y）**
  TTS 朗读与语音模式（#42700，高赞）。目前是少数获得高认同度的新交互需求。
- **IDE 集成深度**
  VSCode 会话删除（#93835）、多文件多行选择高亮（#81895）。相较 Cursor/Codex 扩展，仍被认为存在功能差距。

---

## 6. 开发者关注点

- **"静默失败"最伤人**：MCP 服务器加载失败（#26073）、Chrome 扩展原生消息静默失败（#77458）、浏览器面板权限被静默忽略（#93156）——三者共同点是用户看不到错误原因。**可诊断性**（明确日志、明确报错）比新增功能更能降低支持成本。
- **认证与计费的硬阻断**：Pro 订阅被组织策略阻断（#82700）、MFA 验证失败（#94897）、连接中断（#87500）。这类问题直接切断使用，属于最高优先级类别。
- **升级回归的敏感性**：桌面更新后 Remote Control 立刻 403（#91717），说明用户对"更新即坏"的容忍度很低，需要更强的回归测试与快速回滚手段。
- **资源与生命周期可见性**：内存临界告警（v2.1.274）与浏览器面板 30 分钟空闲被销毁（#92610）形成呼应——开发者希望**资源行为可配置、可预期**，而不是被硬编码阈值（如 `idleTimeoutMs=18e5`）支配。
- **需求积压治理**：昨日一批 7 月提交的 enhancement 被 stale 机器人集中关闭（含 UI 定制、TPS 显示、Bash 模式不入上下文等）。对于 `!!` 这类明显有实际用途的请求，社区通常在重新提交时会附带更强论证——建议关注官方是否会对 stale 流程做出说明。

---

*本报告基于过去 24 小时内公开的 Release、Issue 与 PR 元数据自动汇总，评论数与点赞数为报告生成时快照。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 · 2026-09-17

数据来源：github.com/openai/codex

---

## 一、今日速览

1. **0.155.0 alpha 进入高频迭代期**：过去 24 小时内 `rust-v0.155.0-alpha` 系列连发 8 个版本（alpha.9 / alpha.10–14 与 alpha.2.5–2.6 两条并行序列），同时 `rusty-v8-v152.2.0` 更新，而当前稳定线仍为 0.154.0。
2. **社区焦点高度集中在“额度与连接”**：本期热评 Issue 中，超过半数与 token 空转、限流、模型容量、流式断连相关，其中 #35259（wait/status 轮询重复调用模型，占本地 token 量 19.8%）以 26 条评论、22 个 👍 位居榜首。
3. **PR 侧聚焦工程基建与平台健壮性**：Guardian 审查链路的测试整合、Windows 沙箱凭据修复、MCP 只读策略、TUI 无障碍（屏幕阅读器）与 Mermaid 渲染成为今天合并/关闭的主要方向。

---

## 二、版本发布

过去 24 小时共 9 个 Release，均为构建/预发布版本，未附带详细 changelog：

| 版本 | 说明 |
|---|---|
| `rusty-v8-v152.2.0` | rusty-v8（V8 绑定）依赖更新 |
| `rust-v0.155.0-alpha.9` ~ `alpha.14` | Codex Rust 0.155.0 主 alpha 序列 |
| `rust-v0.155.0-alpha.2.5` / `alpha.2.6` | 同一 minor 下的另一条并行序列 |

**解读**：`0.155.0` 处于密集 alpha 阶段，两条 alpha 序列（`.2.x` 与 `.9–.14`）并存，通常意味着主干功能推进与补丁/回移分支并行。当前 Issue 中大量环境信息仍显示稳定线为 `codex-cli 0.154.0`，短期内建议生产使用继续停留在稳定版本。

---

## 三、社区热点 Issues（精选 10 条）

### 1. [#35259](https://github.com/openai/codex/issues/35259) Codex Desktop 在等待/轮询状态时反复重入模型，消耗大量额度
`bug · rate-limits · tool-calls · app · subagent` | 26 评论 · 22 👍
在 Ultra 与多智能体模式下，仅用于 wait/status 轮询的模型轮次占到**本地原始 token 量的 19.8%**（在“重置到 49% 用量”的窗口内测得）。这是本期最具共鸣的成本议题，说明多 agent 编排的“空转开销”已成为真实账单问题。

### 2. [#38503](https://github.com/openai/codex/issues/38503) ChatGPT 网页端 “Too many requests” 阻断会话，扰乱 Work 任务
`bug · codex-web · rate-limits · app` | 22 评论 · 17 👍
桌面端与网页端同账号并行时触发会话级封禁弹窗，跨端限流策略的叠加效应被反复质疑，至今仍为 OPEN。

### 3. [#40060](https://github.com/openai/codex/issues/40060) Windows execpolicy 误报：Start-Process 与无关 URL 同脚本即被拦截
`bug · windows-os · sandbox · CLI` | 19 评论
在 0.146.0/0.149.0 及最新 main 均可复现，分类器逻辑问题明确。对 Windows 用户是高频阻塞项，社区要求给出误报收敛方案。

### 4. [#17401](https://github.com/openai/codex/issues/17401) 功能请求：为 AGENTS.md 增加 `@include` 组合指令
`enhancement · context` | 13 评论 · 21 👍
希望 CLI 在指令组装阶段解析 `@path/to/file.md` 并内联内容，实现模块化、可维护的上下文配置。这是本期 👍 最多的增强诉求，反映社区对上下文工程化（而非堆砌）的强烈期待。

### 5. [#34873](https://github.com/openai/codex/issues/34873) `model_reasoning_summary="detailed"` 只输出标题、无正文
`bug · model-behavior · exec · CLI` | 9 评论 · 12 👍
持久化的 reasoning 项只含一个加粗状态标题，推理摘要形同虚设，直接影响可观测性与调试体验。

### 6. [#42937](https://github.com/openai/codex/issues/42937) GPT-5.6 Sol / GPT-6 Astra：智能更高，但自主完成度与运行可靠性下降
`bug · model-behavior · app` | 8 评论 · 5 👍
一条持续更新的长线跟踪帖（含 9 月 7 日证据更新），讨论新模型“监督负担”上升、交付结果反而变差的问题。对模型选型与版本升级决策有参考价值。

### 7. [#45925](https://github.com/openai/codex/issues/45925) `stream disconnected before completion` 呈账号相关性，切换账号失败率差约 7 倍
`bug · app · connectivity` | 6 评论
把此前被归因于网络的断流问题定位到**账号维度**，为排查服务端路由/配额策略提供了关键线索，属于今天新增的高价值复现。

### 8. [#45841](https://github.com/openai/codex/issues/45841) 功能请求：为 Codex 引入“群体智能/专家模型网络”
`enhancement · codex-web · subagent` | 6 评论
主张从单体模型扩展转向多专家模型网络编排，与 #35259 的空转问题形成张力——社区既想要更强编排，又担心成本失控。

### 9. [#45886](https://github.com/openai/codex/issues/45886) Windows Desktop 第二轮提示无法发送，发送按钮置灰（CLI 正常）
`bug ·

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-09-17）

## 1. 今日速览
- 今日发布 v1.0.86-1、v1.0.86-0 及 v1.0.85，重点包括自定义代理可选用仓库指令文件、会话恢复健壮性提升、Vim 模式全量开放。
- 社区高赞需求集中在**自定义代理的推理努力配置**与**子代理工具调用详情展示**，相关 Issue 虽已关闭但讨论热度高。
- MCP 配置加载、OAuth 认证及远程容器支持仍是 Open Issue 中的主要痛点。

## 2. 版本发布

### v1.0.86-1
- **新增**：自定义代理可通过 frontmatter 设置 `include-custom-instructions: true`，选择加入仓库指令文件（AGENTS.md、copilot-instructions.md、CLAUDE.md）。
- **修复**：在没有插件目录、发现或工作目录覆盖的情况下恢复活动会话时保持稳定（原文截断）。

### v1.0.86-0
- **修复**：即使转录文件包含可恢复的损坏，也能正常恢复会话。
- **修复**：紧凑时间线中扩展的推理文本不再变暗，可读性与时间线其余部分一致。
- **修复**：Autopilot 在接受任务完成后停止，不再意外继续执行。

### v1.0.85（2026-09-16）
- **Vim 模式向所有人开放**：通过 `/vim` 或设置 `editorMode` 为 `vim` 启用，输入时显示当前模式。
- **新增 `/settings` 选项**：可选择为代理和子代理启用上下文管理工具。
- 设置 transcriptView...（原文截断）

## 3. 社区热点 Issues

1. **#2904 [CLOSED] Custom Agent YAML Frontmatter Should Support Reasoning Effort**  
   作者：@brian-kelley-intel | 评论：9 | 👍：23  
   **为什么重要**：自定义代理支持 `model` 字段但无法按代理设置推理努力，只能全局配置。高赞表明社区对细粒度模型控制需求强烈。  
   链接：https://github.com/github/copilot-cli/issues/2904

2. **#1322 [CLOSED] Feature request: Show subagent tool call details**  
   作者：@cephalin | 评论：7 | 👍：25  
   **为什么重要**：CLI 中子代理仅显示状态，而 VS Code Copilot Chat 可深入查看工具调用。25 个赞反映用户对执行透明度的迫切需求。  
   链接：https://github.com/github/copilot-cli/issues/1322

3. **#2050 [CLOSED] Claude Sonnet 4.6 - Execution failed: HTTP/2 GOAWAY**  
   作者：@tinonetic | 评论：9 | 👍：4  
   **为什么重要**：模型响应失败并重试 5 次，涉及网络连接稳定性。虽已关闭，但同类错误可能影响生产使用。  
   链接：https://github.com/github/copilot-cli/issues/2050

4. **#4542 [OPEN] Workspace .mcp.json detected by 'mcp list' but not connected in actual agent session**  
   作者：@ssolomentsev | 评论：3 | 👍：1  
   **为什么重要**：MCP 服务器在 `mcp list` 中显示启用，但实际会话未连接。配置生效链路断裂，影响 MCP 生态使用。  
   链接：https://github.com/github/copilot-cli/issues/4542

5. **#3009 [OPEN] MCP OAuth callback unreachable in remote container / Codespaces**  
   作者：@velimattiv | 评论：2 | 👍：1  
   **为什么重要**：远程容器中 OAuth 回调指向 localhost 无法访问，且无手动粘贴 token 回退机制，阻碍远程开发场景。  
   链接：https://github.com/github/copilot-cli/issues/3009

6. **#3100 [OPEN] HTTP MCP server with Bearer token fails OAuth discovery**  
   作者：@vladk2854-max | 评论：1 | 👍：10  
   **为什么重要**：配置 Bearer token 后 CLI 仍尝试 OAuth 发现并失败，未回退到 headers 认证。10 个赞说明该认证缺陷影响广泛。  
   链接：https://github.com/github/copilot-cli/issues/3100

7. **#4765 [OPEN] copilot cli fails to read config from working directory which isn't a repo root**  
   作者：@johnmreynolds | 评论：2 | 👍：0  
   **为什么重要**：多仓库工作区（非单一 Git 仓库根）无法读取 `.mcp.json` 或 hook 文件，影响非 monorepo 项目配置。  
   链接：https://github.com/github/copilot-cli/issues/4765

8. **#4886 [OPEN] `--plugin-dir` skills load but are omitted from `/skills` and `/env`**  
   作者：@zendu | 评论：1 | 👍：0  
   **为什么重要**：本地插件技能后端可发现，但交互式 `/skills` 和 `/env` 不显示，导致用户无法确认技能是否生效。  
   链接：https://github.com/github/copilot-cli/issues/4886

9. **#4819 [OPEN] Default model choice fails when org policy loads model list after copilot load**  
   作者：@jeffreybwilson | 评论：1 | 👍：2  
   **为什么重要**：企业组织策略加载时序导致默认模型选择失败，影响企业环境下开箱即用体验。  
   链接：https://github.com/github/copilot-cli/issues/4819

10. **#4220 [CLOSED] Plan mode blocks read-only `gh api` GET/GraphQL queries as "may modify the workspace"**  
    作者：@grantborthwick | 评论：2 | 👍：1  
    **为什么重要**：计划模式将只读 `gh api` 调用误判为修改工作区，产生假阳性阻止，影响调查类任务。  
    链接：https://github.com/github/copilot

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-09-17）

**数据边界**：过去 24 小时 Releases 为 0，Issues 更新 1 条，PR 更新 1 条。样本量较小，以下按实际数据生成，不虚构扩列。

## 1. 今日速览

- 无新版本发布。
- 今日最重要动态是 Issue #2647：会话触发 `403 provider.auth_error: 5-hour usage limit` 后，主代理持续重试 14+ 小时，子代理还启动 detached 重试循环调用 Kimi CLI，导致配额继续被消耗。
- PR #2648 新增 `PreToolUse` + HOL Guard 示例，尝试在 Shell 命令执行前加入安全门禁，反映社区对工具调用前置审查的关注。

相关链接：  
- Issue #2647：https://github.com/MoonshotAI/kimi-cli/issues/2647  
- PR #2648：https://github.com/MoonshotAI/kimi-cli/pull/2648  

## 2. 版本发布

无新 Release。

## 3. 社区热点 Issues

> 过去 24 小时仅 1

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 · 2026-09-17

> 数据来源：github.com/anomalyco/opencode

## 1. 今日速览

今日社区焦点几乎被**新版 UI 强制迁移**的争议占据：多个高赞 Issue 要求恢复旧布局、提供切换开关并补回 workspaces/worktrees，开发者反馈新界面严重影响多项目/多会话工作流。另一方面，**Zen/Go 免费模型的工具调用持续失败**（503 Endpoint unavailable）成为最高讨论量的技术故障，且 agent 循环在 `unknown` finish reason 下无限重试的问题当日即被 PR 修复。整体上，UI 体验与提供商网关稳定性是当前两大主线。

---

## 2. 版本发布

过去 24 小时无新 Release。

---

## 3. 社区热点 Issues（10 个）

### ① #37546 — Web 新布局无法回退，且缺失 workspaces/worktrees
👍 24 | 💬 6 | OPEN
升级到 `v1.17.19` 后 Web 端自动启用「顶部 tabs」新布局，**没有任何 UI 可切回旧版**，且新布局完全未实现 git worktree 工作区。对依赖工作区的用户等于功能被砍。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*