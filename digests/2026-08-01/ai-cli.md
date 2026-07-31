# AI CLI 工具社区动态日报 2026-08-01

> 生成时间: 2026-07-31 22:36 UTC | 覆盖工具: 7 个

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

# Claude Code 社区动态日报 — 2026-08-01

## 今日速览

过去 24 小时无新版本发布，社区焦点集中在**桌面端 2.1.217 的 "Last Activity" 过滤功能回归**（#80279，9 评论 / 12 👍）——该问题在按 Project 分组会话时导致按时间筛选入口消失，目前仍为 OPEN 状态。与此同时，多个涉及**数据安全与丢失**（env 文件被删、会话记录损坏）及**模型自动路由**的旧 issue 仍维持较高讨论热度，显示社区对底层可靠性和成本优化的关注持续升温。

---

## 社区热点 Issues（10 个）

以下从过去 24 小时更新的 50 条 issues 中，按讨论热度与影响面筛选出 10 个值得关注的问题：

### 1. [OPEN] #80279 — "Last Activity" 过滤在按 Project 分组时消失（2.1.217 回归）
- **链接**: https://github.com/anthropics/claude-code/issues/80279
- **作者**: @Remenua | **评论**: 9 | **👍**: 12
- **重要性**: 当前唯一 OPEN 且高赞的活跃 issue。桌面应用自动更新到 2.1.217 后，按 Project 分组时侧边栏的按最近活动天数过滤选项消失，影响多项目用户的会话检索效率。社区反应积极，点赞数说明受此回归影响的用户面较广。

### 2. [CLOSED] #65034 — Claude 在代码操作中删除了 env 文件
- **链接**: https://github.com/anthropics/claude-code/issues/65034
- **作者**: @mrdev473 | **评论**: 5 | **👍**: 0
- **重要性**: 典型数据丢失问题——模型在执行代码操作时误删环境变量文件。虽已关闭，但此类问题触及开发者最敏感的资产安全底线，与 [#64082] 等数据丢失类报告共同构成社区强烈关注的痛点。

### 3. [CLOSED] #67239 — Bash 工具结果静默丢失，agent 无限等待
- **链接**: https://github.com/anthropics/claude-code/issues/67239
- **作者**: @mrvdot | **评论**: 4 | **👍**: 0
- **重要性**: 自 v2.1.167 起，Bash 工具调用间歇性不返回结果，命令实际完成但 harness 未交付 tool_result，导致会话永久挂起。该问题与 Remote Control 会话相关，直接影响 agent 的自动化稳定性，属于严重可靠性问题。

### 4. [CLOSED] #68435 — Windows 下程序化启动的会话写入 stub 记录，无法恢复
- **链接**: https://github.com/anthropics/claude-code/issues/68435
- **作者**: @MokebeGluszak | **评论**: 4 | **👍**: 0
- **重要性**: 在 Windows 上通过 launcher 程序化启动的会话，其 transcript 间歇性只写入单条 ai-title 记录，导致会话不可恢复。对依赖自动化工作流的开发者影响较大，涉及核心会话持久化机制的可靠性。

### 5. [CLOSED] #66079 — "Co-authored-by" 泄露真实邮箱（即使 git 配置了 noreply）
- **链接**: https://github.com/anthropics/claude-code/issues/66079
- **作者**: @yuki0ueda | **评论**: 3 | **👍**: 0
- **重要性**: 自 v2.1.165 起，git trailer 中会写入用户的真实账号邮箱，忽略 git 配置的 noreply 地址。这是隐私泄露问题，与 commit 签名、开源贡献等场景强相关，社区对回归类安全问题的容忍度很低。

### 6. [CLOSED] #63353 — [未解决] Windows 桌面应用无法打开文件夹，7 个 issue 未修复
- **链接**: https://github.com/anthropics/claude-code/issues/63353
- **作者**: @duncanmbarclay-arch | **评论**: 3 | **👍**: 2
- **重要性**: 用户情绪强烈（标题含 "UNACCEPTABLE/UNRESOLVED"），指出 Windows 桌面版无法打开文件夹，且存在 7 个相关未修复 issue，付费用户被锁在基本 IDE 功能之外 2 个多月。虽已关闭，但反映了 Windows 桌面端积压的质量问题。

### 7. [CLOSED] #68910 — Bash 工具误报 /tmp 空间满，造成 token 浪费
- **链接**: https://github.com/anthropics/claude-code/issues/68910
- **作者**: @gosocial2 | **评论**: 3 | **👍**: 2
- **重要性**: Opus 4.8 环境下 Bash 工具虚报 ENOSPC（尽管有 148GB 可用），导致 token 消耗无谓增加。成本相关且带复现价值的 bug，是社区对成本敏感性的典型体现。

### 8. [CLOSED] #69541 — 工具调用块被 "count" token 污染，导致解析失败
- **链接**: https://github.com/anthropics/claude-code/issues/69541
- **作者**: @VGMVS | **评论**: 3 | **👍**: 1
- **重要性**: 模型输出间歇性在 `<invoke>` 前注入字面量 "count" token，导致所有工具调用解析失败、回合中止。严重性较高（标题自标注 High），阻断 Bash/编辑器等核心工具链，直接影响 agent 可用性。

### 9. [CLOSED] #67389 — SessionStart hook 的 sessionTitle 在 `clear` 源下被静默忽略
- **链接**: https://github.com/anthropics/claude-code/issues/67389
- **作者**: @syd3n | **评论**: 2 | **👍**: 1
- **重要性**: Hook 返回的 `sessionTitle` 在 startup/resume 源下生效，但在 `clear` 源下被静默丢弃——这影响用户通过 hook 自定义会话标题的体验，属于插件开发者的高频触达点。

### 10. [CLOSED] #66596 — 所有会话显示在侧边栏但消息历史为空
- **链接**: https://github.com/anthropics/claude-code/issues/66596
- **作者**: @PlayoffBlitzDev | **评论**: 2 | **👍**: 1
- **重要性**: macOS 上侧边栏显示全部会话，但点开无消息记录。该问题与 [#68435] 类似，均指向会话持久化的数据一致性缺陷，社区对"会话内容无端消失"的容错度极低。

---

## 重要 PR 进展（5 条）

过去 24 小时共更新 5 条 PR，数量虽少但方向涉及 CI 修复、TUI 性能优化和新功能实现：

### 1. [OPEN] #82987 — 修复 CI cron 失败，并针对 TUI 输入延迟提出架构性修复
- **链接**: https://github.com/anthropics/claude-code/pull/82987
- **作者**: @ruok-dev
- **内容**: 解决 GitHub Actions 定时任务失败问题；提出针对高 agent 工作负载下 TUI 输入延迟的修复方案（关联 #82984）。对自动化流程和交互体验都有实际价值，值得关注其 TUI 延迟方案的讨论。

### 2. [OPEN] #82794 — code-review 插件实现置信度评分与 --threshold 标志
- **链接**: https://github.com/anthropics/claude-code/pull/82794
- **作者**: @hulincup
- **内容**: 将 code-review 插件从二元校验升级为 0–100 置信度评分，并增加 `--threshold` 参数，使其与文档对齐。属于插件生态的实用增强。

### 3. [CLOSED] #17776 — 为 security-guidance 插件补全 README
- **链接**: https://github.com/anthropics/claude-code/pull/17776
- **作者**: @skyvanguard
- **内容**: 为 plugins/ 目录下最后一个缺文档的插件补齐 README，涵盖 9 个安全模式说明。对插件生态的规范化有积极意义。

### 4. [OPEN] #39872 — 将 Node.js 版本从 20 升级到 24
- **链接**: https://github.com/anthropics/claude-code/pull/39872
- **作者**: @dijonkitchen
- **内容**: 为即将到来的 LTS 切换做准备，将运行环境升级至 Node 24。基础设施更新，影响面较广但收益偏长期。

### 5. [OPEN] #82981 — 仓库自动化库存管理（疑似测试/占位 PR）
- **链接**: https://github.com/anthropics/claude-code/pull/82981
- **作者**: @Eduardo-neira
- **内容**: 标题为 "Claude/automatizar inventario insumos w4n98s"，无描述，疑为测试或误提交的 PR，暂不具参考价值。

---

## 功能需求趋势

从近 24 小时更新的 issues 中，可以提炼出社区对以下功能方向的高频诉求：

### 1. 自动模型路由 / 性价比优化
- **代表**: #69561（根据任务复杂度自动选择模型）、#69530（将任务路由至最便宜的可用模型）
- **趋势**: 用户不再满足于手动 `--model` 参数，希望 Claude Code 能根据任务类型自动分配 Haiku/Sonnet/Opus，以降低成本。模型成本与质量的最佳平衡成为核心诉求。

### 2. 会话与数据持久化的可靠性
- **代表**: #68435（stub transcript）、#66596（会话历史为空）、#64082（扩展更新后会话丢失）
- **趋势**: 多个 issue 指向同一类问题——会话记录写入不完整或更新后丢失。开发者对"工作进度不可找回"零容忍，该方向的稳定性投入是社区迫切期待的。

### 3. WSL / 跨平台适配完善
- **代表**: #69256（Semgrep 插件在 WSL 上执行 Windows 二进制）、#69560（WSL 上 `/init` 误触发）、#63119（Windows Cowork 认证 token 缺失）
- **趋势**: WSL 用户数量增长带动了跨平台兼容性问题的集中暴露，尤其是插件脚本对 WSL_DISTRO_NAME 的处理、原生二进制选择等细节，成为高频踩坑点。

### 4. 指令与上下文的热更新
- **代表**: #69571（CLAUDE.md 修改后不热重载）
- **趋势**: 用户希望在会话中调整 CLAUDE.md / 项目说明后即时生效，不必重启会话即可改变行为。反映开发工作流对即时反馈的更高需求。

### 5. Hook 与插件机制的深度能力
- **代表**: #67389（SessionStart hook 的 sessionTitle 被忽略）、#69256（插件平台判断错误）
- **趋势**: 插件开发者对 hook 系统的一致性和跨环境行为更加敏感，期望所有 source 下钩子行为完全一致，且能正确区分 Windows/Linux/WSL 环境。

---

## 开发者关注点

### 高频痛点

1. **误删/数据丢失类问题最受关注**: #65034（env 文件被删）、#68435 / #66596（会话记录缺失）等 issues 虽部分已关闭，但每次出现都引发共鸣。开发者对"AI 主动修改文件系统"抱有警惕，期望更精细的文件操作授权与可回滚机制。

2. **模型输出不可靠导致的连锁故障**: #69541（"+count" token 污染 tool call）、#67239（Bash 结果静默丢失）让用户付出额外时间与 token 成本。工具链底层不可靠性会直接削弱对 Claude Code 的信任度。

3. **回归问题频繁出现**: #80279（过滤功能消失）、#66079（邮箱泄露）等均为较新版本引入的回归。社区强烈希望 Anthropic 能在发布前建立更完善的回归测试矩阵，尤其是针对会话 UI、git 集成、权限校验等关键路径。

4. **成本敏感度提升**: 多个 issue 提到 token 浪费（#68910、#69541），自动模型路由的呼声渐高。开发者正积极寻求控制 AI 工具支出的手段，功能与成本的平衡点成为选型关键。

5. **Windows 桌面端体验积弱**: #63353 及其关联的 7 个 issue 长期未解决，且社区情绪明显激化（"UNACCEPTABLE"）。Windows 不是 Claude Code 的主阵地，但其不断扩张的用户基础要求官方在 QA 资源投向上做出倾斜。

> 总体来看，本周社区声量集中于 **"数据安全" 与 "成本控制"** 两极，而模型自动路由与 WSL 兼容性是最具共识的演进方向。建议关注 #80279 的后续修复进度，以及 #82987 中 TUI 延迟修复方案的落地情况。

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

# Kimi Code CLI 社区动态日报 — 2026-08-01

## 今日速览

昨日社区动态集中在**跨会话记忆系统**的功能需求、**终端滚动体验**的缺陷反馈，以及一个针对 **工具调用参数双重编码** 的修复 PR 提交。目前无新版本发布，核心开发围绕稳定性和生态适配展开。

---

## 版本发布

过去 24 小时无新版本发布。

---

## 社区热点 Issues

> 以下为过去 24 小时内有更新的全部 3 条 Issue，均已附上链接。

### 1. [Feature Request] Memory System - Persistent context across sessions  
**#1283** | 作者：@CatKang | 👍 0 | 评论 8  
**链接：** https://github.com/MoonshotAI/kimi-cli/issues/1283  

**内容摘要：**  
希望实现一个全面的 **记忆系统**，让 Kimi Code CLI 能在会话间记住项目上下文、模式与用户偏好，包括自动记忆（AI 管理笔记）和手动记忆（用户自定义指令）。  

**为什么重要：**  
这是长期高频需求，直接关系到 CLI 在大型项目中的连续工作能力。8 条评论表明社区对该功能有持续讨论和细化预期，属于影响产品形态的关键诉求。

---

### 2. [Bug] 对话完成后滚动查看输出内容会自动调到底部  
**#2422** | 作者：@venus0707 | 👍 1 | 评论 2  
**链接：** https://github.com/MoonshotAI/kimi-cli/issues/2422  

**内容摘要：**  
在 Kimi Code CLI 1.46.0，使用 kimi2.6 模型，Linux 系统下，对话结束后向上滚动查看历史输出，界面会自动跳回底部，影响阅读。  

**为什么重要：**  
该问题直接影响终端交互体验，属于常见的滚动状态管理缺陷。有 1 个 👍，说明至少部分用户遇到同样困扰，反馈版本与系统信息完整，便于维护者复现。

---

### 3. [Closed] error: the message at position 1 with role  
**#796** | 作者：@bravery | 👍 0 | 评论 1  
**链接：** https://github.com/MoonshotAI/kimi-cli/issues/796  

**内容摘要：**  
KimiCLI/1.3 版本在 macOS 上调用 `kimi-for-coding` 模型时收到 400 错误，提示“message at position 1 with role”相关的问题（角色信息不合法）。  

**为什么重要：**  
虽然该 Issue 已关闭，但最近又有更新，说明可能在新的版本或使用场景中复现。角色校验错误属于 API 兼容性问题，对模型接入方有参考价值。

---

## 重要 PR 进展

> 过去 24 小时内更新的 PR 仅 1 条，已列出。

### [PR #2572] 递归解包工具调用参数中的双重编码 JSON  
**作者：** @aalhadxx | 👍 0 | 评论：无  
**链接：** https://github.com/MoonshotAI/kimi-cli/pull/2572  

**功能/修复内容：**  
针对部分供应商（如 Moonshot API）在 `function.arguments` 中返回双重编码的 JSON 字符串，导致 `SetTodoList`、`ExitPlanMode`、`StrReplaceFile` 等携带数组/对象参数的 Tool Call 出现 Pydantic 校验错误。PR 递归解包内层嵌套 JSON，解决参数结构解析失败问题。  

**重要性：**  
该修复直接提升多供应商兼容性与工具调用稳定性，属于影响实际可用性的底层问题，尤其对依赖工具调用的 Agent 场景至关重要。

---

## 功能需求趋势

基于当前活跃 Issue 与社区讨论，可提炼出以下趋势：

- **持久化记忆系统**：跨会话保存上下文、项目模式与用户偏好，是最高频的进阶需求，反映出用户对“连续协作”的期待。
- **终端交互体验优化**：如滚动行为、输出查看稳定性，说明基础 UI/UX 细节仍在持续反馈中。
- **API 兼容性与稳定性**：角色校验错误、工具参数编码问题，凸显多模型/多供应商适配是当前开发重点。

---

## 开发者关注点

- **跨会话连续性**：开发者希望 CLI 能“记住”对话内容，减少重复描述项目背景，提升长任务效率。
- **滚动行为异常**：对话后无法自由回看输出，打断工作流，属于明确的体验缺陷。
- **第三方服务对接问题**：不同平台返回的数据格式差异（如双重编码 JSON）导致工具调用失败，开发者期待更健壮的容错处理。

---

*数据来源：GitHub - MoonshotAI/kimi-cli，更新于 2026-08-01。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-01

> 数据来源：[github.com/anomalyco/opencode](https://github.com/anomalyco/opencode)

---

## 今日速览

今日社区最突出的事件是**OpenCode Go/Zen 服务端上游封锁**问题集中爆发——多个用户报告 401 错误和全部模型不可用（[#38257](https://github.com/anomalyco/opencode/issues/38257)、[#39827](https://github.com/anomalyco/opencode/issues/39827)），目前已影响 Go 与 Zen 双订阅体系。同时，**DeepSeek V4 Flash 正式版（0731）**发布引发社区强烈关注，已有 22 条讨论要求 OpenCode 快速适配。PR 方面，大量由 `opencode-agent[bot]` 提交的代码清理工作正在推进，另有 2 个功能性 PR（LAN 发现、SSE 鲁棒性）处于活跃状态。

---

## 版本发布

过去 24 小时无新版本发布。

---

## 社区热点 Issues

### 1. OpenCode Go 全线返回 401 上游封锁（42 条评论）
[#38257](https://github.com/anomalyco/opencode/issues/38257) — `[Bug] OpenCode Go: return 401 Request blocked by upstream provider`

自 7 月 22 日起，Go 订阅用户的 `chat/completions` 接口全部返回 `401 Request blocked`，但 `/v1/models` 正常。社区认为是服务端问题，**这是当前评论数最高、影响面最大的 Issue**，直接导致付费用户无法使用。👍 11。

**为什么重要**：付费核心服务不可用已持续约 10 天，且与同日爆发的 Zen 故障（[#39827](https://github.com/anomalyco/opencode/issues/39827)）指向同一根因。

### 2. DeepSeek V4 Flash 正式版上线确认（22 条评论）
[#39823](https://github.com/anomalyco/opencode/issues/39823) — `[Question] DeepSeek V4 Flash formal version (0731) — is it already live on OpenCode Go/Zen?`

DeepSeek 于 7 月 31 日发布 V4-Flash-0731 正式版，基准测试全面优于预览版（Terminal Bench 82.7、NL2Repo 54.2 等）。社区在询问 OpenCode Go/Zen 何时接入，同时有 4 条评论的衍生需求 [#39829](https://github.com/anomalyco/opencode/issues/39829) 要求支持其 **OpenAI Responses API**。👍 19。

**为什么重要**：最强的开源 Agent 能力模型，OpenCode 用户核心诉求是**第一时间接入**。

### 3. 黑屏问题“幽灵”不散（37 + 33 条评论）
[#4140](https://github.com/anomalyco/opencode/issues/4140)（Closed）— `[bug, opentui] black screen when using >1.0.46`
[#10221](https://github.com/anomalyco/opencode/issues/10221)（Closed）— `[bug] Black screen on just installed opencode`

两个已关闭的 TUI 黑屏 Issue 在 7 月 31 日再次被大量评论顶起，用户持续反馈新版本（包括 v2 分支 [38773](https://github.com/anomalyco/opencode/issues/38773)）仍出现输入区被黑矩形遮挡的问题。👍 13/17。

**为什么重要**：**TUI 可用性**是老用户的长期痛点，多个版本仍未根治。

### 4. gpt-5.6-luna 流式输出劣化（3 条评论）
[#39881](https://github.com/anomalyco/opencode/issues/39881) — `OpenCode Go: gpt-5.6-luna stream degradation (repeats, mid-stream cuts, junk tails); Codex path clean`

Go 订阅下 gpt-5.6-luna 的流式输出出现**重复回答、中途截断、垃圾尾部**，而同模型在 OpenAI Codex 侧正常，用户怀疑 OpenCode Go 网关的流式处理存在问题。

**为什么重要**：直接指向 Go 网关在**长流式响应的稳定性**上的短板。

### 5. Zen 订阅全部模型 AuthError（2 条评论）
[#39827](https://github.com/anomalyco/opencode/issues/39827) — `[Zen] AuthError: "Request blocked by upstream provider" — all Zen models broken`

Zen 用户报告**所有**免费/付费模型均返回 `AuthError`，而直连 DeepSeek/Anthropic 官方 API 正常。结合 #38257，推测 OpenCode 上游网关出现了全局性配置错误。👍 2。

**为什么重要**：Zen 与 Go 双线路同时故障，影响所有非 BYOK 用户。

### 6. Go 订阅隐私条款被静默移除（4 条评论）
[#39875](https://github.com/anomalyco/opencode/issues/39875) — `[FEATURE]: Revert silent removal of Go privacy wording and provider attribution, and add telemetry + retention to privacy policy`

用户发现近两周的两次提交**静默移除了 Go 的隐私措辞和 provider 归属声明**，要求恢复并补充 telemetry 和保留期说明。引用 #39860、#39857、#24649 等 5+ 个历史 Issue，均未获实质回应。👍 19。

**为什么重要**：**透明度与信任**问题，19 个 👍 表明付费用户对隐私变更非常敏感。

### 7. Qwen 3.6 工具调用裸输出卡死（20 条评论）
[#24316](https://github.com/anomalyco/opencode/issues/24316) — `Progress halts with qwen 3.6 35b-a3b with naked tool call in the console`

本地运行 Qwen 3.6 35b-A3B（llama.cpp）时，控制台出现裸 `<tool_call>` 标记并中断执行。社区在争论是 Qwen 的 bug、llama.cpp 的格式化问题，还是 opencode 的解析问题。

**为什么重要**：本地模型 + 工具调用是高频场景，**兼容性尚不稳固**。

### 8. ACP 协议时序缺陷：end_turn 后 session/update 延迟（15 条评论）
[#17505](https://github.com/anomalyco/opencode/issues/17505) — `session/update notifications sent after session/prompt response (end_turn)`

ACP 集成方（Fabriqa）发现 `session/update` 通知在 `end_turn` 响应之后才到达，导致客户端 UI 显示不完整内容。👍 10。

**为什么重要**：**ACP 生态兼容性**问题，影响依赖 OpenCode 作为后端的第三方应用。

### 9. 自定义 OpenAI 兼容 Provider 的 function.name 解析失败（10 条评论）
[#26412](https://github.com/anomalyco/opencode/issues/26412) — `Custom OpenAI-compatible provider: "Expected 'function.name' to be a string" on streaming tool call chunks`

vLLM 后端 + 自定义 provider 下，所有工具调用流式返回 `Expected 'function.name' to be a string`。问题持续近 3 个月仍未解决，影响 vLLM / llama.cpp / Ollama 等自托管场景。

**为什么重要**：**自定义 Provider 兼容性**的典型代表，长期未修复。

### 10. 统一插件/Agent/Skills 市场呼声高涨（6 条评论）
[#28696](https://github.com/anomalyco/opencode/issues/28696) — `[FEATURE]: Plugin/Agent/Skills/etc marketplace`

Master Issue：请求构建统一的 OpenCode 市场/注册表/包管理系统，覆盖发现、安装、更新等全流程。👍 23，位列今日功能需求最高赞。

**为什么重要**：生态建设的核心诉求，反映社区对**可扩展生态**的期待。

### 值得关注的其他 Issue

- **#39829**（👍 10）：DeepSeek V4 Flash 的 Responses API 支持 — 新模型适配的第二诉求。
- **#927（Closed）**（👍 29）：TUI 文本选择能力 — 用户体验类别的最高赞历史 Issue。
- **#36399**：Go 订阅下 qwen3.7-max 出现异常高频扣费（每 30 秒调用一次）。
- **#39895**：自动续费后取消订阅导致立即被撤销，疑似计费逻辑缺陷。

---

## 重要 PR 进展

### 功能类

**1. 本地 LAN Provider 自动发现**（[#27554](https://github.com/anomalyco/opencode/pull/27554)，Open）  
新增 `/connect` 中的 `Local (LAN)` 发现，结合 mDNS 自动发现局域网内的 OpenAI 兼容服务器并拉取模型列表。Closes #6231 / #27553。**属于用户呼声已久的自托管体验改进。**

**2. 长连接流式 SSE 静默终止修复**（[#39970](https://github.com/anomalyco/opencode/pull/39970)，Open）  
修复网关静默终止/停滞长 SSE 响应时的 3 个缺陷，Closes #39968。与今日 #39881（gpt-5.6-luna 流入退化）高度相关，**值得后续关注**。

**3. 每 Agent 自定义 subagent_depth**（[#37226](https://github.com/anomalyco/opencode/pull/37226)，Open）  
允许在 agent 配置（`.md` frontmatter 或 `opencode.json`）中覆写全局 subagent 深度，未设置时回退全局/默认值。**Agent 编排精细化的实用功能。**

**4. promptCacheKey 协议中立化**（[#39965](https://github.com/anomalyco/opencode/pull/39965)，Open）  
将 `promptCacheKey` 提升为 `LLMRequest` 通用字段，同时覆盖 OpenAI Responses 路由和 OpenRouter，并为不同请求类型设置有界缓存键。有助于**降低成本并提升多 Provider 一致性**。

**5. export expandTheme**（[#39967](https://github.com/anomalyco/opencode/pull/39967)，Closed 已合并)  
从 `@opencode-ai/theme/tui` 入口导出 `expandTheme`，**主题生态扩展的公共 API 基础**。

### 清理/重构类（opencode-agent[bot] 系列）

过去 24 小时出现大量由 `@opencode-agent[bot]` 驱动的死代码删除 PR（#39975、#39974、#39973、#39972、#39971、#39969、#39961、#39964、#39963、#39962、#39960、#39959、#39958、#39956、#39953），覆盖 core/tui/cli 各包，类型检查与测试均通过。**核心动机**：减少维护面、降低包体积、消除孤儿模块。以下为几个示例：

- [#39974](https://github.com/anomalyco/opencode/pull/39974) — 移除未使用的 V2 `MoveSession` 控制面服务及其测试套件
- [#39973](https://github.com/anomalyco/opencode/pull/39973) — 移除 Core 中未使用的 `semver`/`effect-sqlite-node` 依赖
- [#39969](https://github.com/anomalyco/opencode/pull/39969) — 移除 TUI 中未使用的 `stopVoice` audio 包装函数
- [#39963](https://github.com/anomalyco/opencode/pull/39963) — 移除未使用的 revert diff 解析器，并删除 TUI 对 `diff` 的直接依赖
- [#39953](https://github.com/anomalyco/opencode/pull/39953) — 移除 `component/prompt` 下的三个过渡性 re-export barrel

---

## 功能需求趋势

从今日 50 条 Issues 中提炼出以下社区最关心的方向：

### 🔥 高热度（多 Issue 并发 + 高 👍）

1. **新模型快速接入**（#39823、#39829 等）  
   DeepSeek V4 Flash 正式版发布当天即有 22+ 讨论，社区要求**官方托管平台第一时间上线新模型，并支持 Responses API**。

2. **服务端稳定性 / 上游故障**（#38257、#39827、#39881、#39883）  
   Go/Zen 双订阅出现 401 封锁、流式降级、计费异常，**付费服务的可靠性**成为用户最大焦虑。

3. **隐私与数据透明度**（#39875、#39860、#39857）  
   用户系统性追查 Go 订阅的隐私措辞、重试/遥测策略、数据保留期，要求**明确且可审计的隐私政策**。

4. **插件/市场生态**（#28696）  
   统一 Marketplace / Registry 的 Master Issue 获得 23 👍，包含发现、安装、更新分发全流程诉求。

### 🌱 持续需求

5. **TUI 稳定性与可用性**（#4140、#10221、#38773、#38801）  
   黑屏、输入框遮挡、循环退出——尽管多次尝试修复，但用户仍频繁反馈。

6. **自定义 Provider / 本地模型兼容性**（#26412、#24316、#27554）  
   vLLM/Qwen/llama.cpp 的兼容问题长期未解决；LAN 自动发现 PR 是缓解手段之一。

7. **会话管理**（#24017、#39936）  
   保存 Threads、按主题/书签管理会话；VS Code 中 agent 通知。

8. **计费与订阅体验**（#36399、#39895）  
   高频扣费与取消订阅后立即撤销的异常，需要计费逻辑的透明化与修复。

---

## 开发者关注点

### 高频痛点

- **服务端上游封锁（401）持续 10 天未解决**：Go 与 Zen 同时故障，`/v1/models` 正常但 `chat/completions` 全量 401，用户被迫降级到 BYOK 直连，付费价值归零。
- **TUI 黑屏/输入遮挡问题反复出现**：既有历史 Issue 被重新顶起（#4140、#10221），

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-01

## 今日速览

v0.21.2 正式版发布，Autofix 机制得到改进（5 轮后自动降级低优先级建议并给出可见提示）。社区围绕 `qwen serve` daemon 的多工作区资源控制、Anthropic 转换器兼容性及 CI 稳定性展开密集讨论，多轮长会话中的工具调用格式泄漏成为最受关注的稳定性问题之一。

## 版本发布

**v0.21.2**（正式版）

- Autofix 在五轮修复后自动推迟低严重性建议，并在因达到轮次限制而拒绝继续时发布可见通知（[#7913](https://github.com/QwenLM/qwen-code/pull/7913)、[#8067](https://github.com/QwenLM/qwen-code/pull/8067)）

另发布 nightly 构建 v0.21.1-nightly.20260731.702932cc7，含 CI 容器任务默认 shell 修复（[#7838](https://github.com/QwenLM/qwen-code/pull/7838)）及 web-shell 相关修复。


## 社区热点 Issues（Top 10）

**1. RFC：单 daemon 多工作区支持**（[#6378](https://github.com/QwenLM/qwen-code/issues/6378)）
评论 31 条 | 作者 @doudouOUC
讨论最热烈的 RFC，探索在单一 `qwen serve` daemon 进程中支持多个工作区，同时保持现有单工作区客户端的兼容性。当前模型为 “1 daemon = 1 workspace × N sessions”，此改动将影响 serve 架构的会话管理核心设计。

**2. daemon 资源使用上限跟踪**（[#8051](https://github.com/QwenLM/qwen-code/issues/8051)）
评论 9 条 | 作者 @doudouOUC
跟踪多工作区 daemon 的有界资源使用问题。现有实现仅按数量限制工作区和会话，未约束请求体字节数、WebSocket 组装缓冲区等实际内存占用，存在资源失控风险。

**3. 延迟工具发现破坏 prompt 缓存前缀**（[#6721](https://github.com/QwenLM/qwen-code/issues/6721)）
评论 7 条 | 作者 @water-in-stone
主会话中通过 `tool_search` 发现的延迟工具会触发 `GeminiClient.setTools()`，导致已缓存的 prompt 前缀失效。该问题直接影响长会话的响应延迟和 token 成本，是性能优化方向的典型反馈。

**4. Anthropic 4.6+ assistant-prefill 400 错误**（[#8039](https://github.com/QwenLM/qwen-code/issues/8039)）
评论 6 条 | 作者 @netbrah | 已关闭
影响所有 Claude Opus/Sonnet 4.6+ 及 5.x 系列模型。两个相关 bug：历史以模型回合结尾时 assistant 预填充出现 400 且无降级方案；`thinking.display` 在未指定时静默默认为 `omitted`。

**5. 工具调用格式泄漏为普通文本**（[#8207](https://github.com/QwenLM/qwen-code/issues/8207)）
评论 3 条 | 作者 @yiliang114
生产环境 0.21.0-preview.2 中，模型在第 6 轮 LLM 调用时（约 35K input tokens）未按预期输出结构化 `tool_call`，而是将工具参数序列化为纯文本，导致下游解析失败。同类问题也出现在 #8003（180K+ tokens 长会话中 XML 风格工具调用）。

**6. Windows 平台 @-file 读取保护弱化**（[#8227](https://github.com/QwenLM/qwen-code/issues/8227)）
评论 3 条 | 作者 @yiliang114
跟进 #7206 的 Windows 兼容性问题：`O_NOFOLLOW` 在 Windows 上不存在，且 dev/ino 身份校验可能为空操作，导致符号链接保护（symlink/TOCTOU）在 Windows 上形同虚设且缺乏测试覆盖。

**7. daemon 给每个 ACP 子进程 50% 宿主机内存上限**（[#8182](https://github.com/QwenLM/qwen-code/issues/8182)）
评论 3 条 | 作者 @doudouOUC
`getAcpMemoryArgs()` 对每个 `qwen --acp` 子进程都按宿主机总内存计算 V8 old-space 上限且不按子进程数量均分，多子进程场景下存在 OOM 风险。

**8. 子代理提问时用户无法应答**（[#7835](https://github.com/QwenLM/qwen-code/issues/7835)）
评论 3 条 | 作者 @byx1728 | 已关闭
子代理向用户提问时，主代理未收集并转发问题，用户无应答入口，子代理永久等待。该问题已被关闭，但揭示了 subagent 交互设计的关键缺口。

**9. Web Shell 已选中的 AI 回答不渲染**（[#8214](https://github.com/QwenLM/qwen-code/issues/8214)）
评论 3 条 | 作者 @yi-zelin
Web Shell 中选中 AI 回复文字时，仅出现快捷操作框但无选择范围高亮渲染，且仅影响 AI 回复，不影响普通文本。

**10. qqbot 频道截断发送者 openid**（[#8232](https://github.com/QwenLM/qwen-code/issues/8232)）
评论 3 条 | 作者 @Eric-GoodBoy-Tech
`prepareGroupMessage()` 将发送者 openid 截断为前 8 位十六进制字符加省略号，导致 LLM 无法使用 `<@OPENID>` 标签正确 @ 提及发送者。


## 重要 PR 进展（Top 10）

**1. Web Shell 权限选项去重**（[#8250](https://github.com/QwenLM/qwen-code/pull/8250)）
作者 @qwen-code-dev-bot | review/self-reported
在 ToolApproval 组件中增加 `deduplicateByLabel` 处理，折叠解析到相同 i18n key 或原始标签的权限选项，修复 #8248 中重复的 “Yes, allow once” 按钮问题。

**2. 保留每段推理的签名**（[#8260](https://github.com/QwenLM/qwen-code/pull/8260)）
作者 @netbrah | review/self-reported
修复 `geminiChat.ts` 历史合并仅保留首个 `thoughtSignature` 的问题。一个回合含多个推理段落（如每个并行工具调用对应一段推理）时，后续段落的签名被正确保留。

**3. 添加 OpenAI Responses API 内容生成器**（[#8169](https://github.com/QwenLM/qwen-code/pull/8169)）
作者 @netbrah
新增 `@qwen/openai-responses` 内容生成器，接入 OpenAI Responses API 作为新的生成后端，进一步扩展模型服务兼容面。

**4. 建立工作区运行时所有权**（[#8213](https://github.com/QwenLM/qwen-code/pull/8213)）
作者 @ytahdn | autofix/takeover
确立 WorkspaceRuntime 作为每个工作区 ACP 子进程生命周期的所有权边界，引入权威五态运行时快照、工作区级单调 epoch、物理工作租约及有界启停行为。

**5. 交互式 TUI 采用 Goal v3**（[#8005](https://github.com/QwenLM/qwen-code/pull/8005)）
作者 @qqqys | autofix/takeover
将交互式 TUI 接入 Goal v3 运行时，添加 `/goal` 生命周期命令、持久化生命周期卡片和页脚状态、Goal 感知的恢复与分支恢复，以及双通道输入队列。

**6. 工作流代理审批冒泡**（[#8240](https://github.com/QwenLM/qwen-code/pull/8240)）
作者 @qqqys | autofix/takeover
完成 Dynamic Workflow 前台权限路径：工作流代理遇到需要确认的 Shell/edit/MCP/信息请求时，挂起至所属运行，通过父 TUI、ACP host 或 stream-json 控制通道呈现给用户。

**7. 完成图片跨入口路由**（[#7206](https://github.com/QwenLM/qwen-code/pull/7206)）
作者 @yiliang114 | autofix/takeover
在 TUI、ACP 和非交互 CLI 三个入口完成本地图片 `@` 引用的完整路由，实施工作区边界、忽略规则、MIME 类型及文件身份校验，并新增自动化真实 Chrome 验收流程。

**8. /review 增加 Test Plan 校验与 A/B 测试框架**（[#8215](https://github.com/QwenLM/qwen-code/pull/8215)）
作者 @wenshao | autofix/takeover
为 `/review` 增加三项验证能力：Test Plan 声明检查、base-tree A/B 测试框架、per-hunk 探测，将维护者手动验证的流程自动化。

**9. Channel ACP 桥接唤醒恢复**（[#8211](https://github.com/QwenLM/qwen-code/pull/8211)）
作者 @yiliang114 | autofix/takeover
修复宿主长期休眠或事件循环停滞导致 channel ACP bridge 不可用的问题，在不重连消息适配器的前提下恢复桥接，避免进程在线但 ACP 子进程失联的场景。

**10. 跳过两个模型相关的 SDK E2E flaky 用例**（[#8259](https://github.com/QwenLM/qwen-code/pull/8259)）
作者 @qwen-code-dev-bot | review/self-reported
跳过两个依赖实时模型选择具体工具的 SDK E2E 用例（异步 MCP 工具处理器和子代理委派），以缓解 #8256 中描述的 main 分支间歇性 CI 失败。


## 功能需求趋势

**1. Daemon 架构演进与资源治理**（#6378、#8051、#8091、#7752、#8182）
社区对 `qwen serve` 的关注点正从单一功能开发转向生产级资源治理：多工作区隔离、内存上限均分、进程生命周期所有权、可拆分的审查粒度。核心诉求是让 daemon 在并发场景下可预测、可观测、可控制。

**2. Anthropic 互操作性持续增强**（#8039、#8169、#8159、#8160、#8161、#8260）
多个高优先级 issue/PR 围绕 Anthropic 协议转换器的边界 case：prefill 400、message 顺序约束、ID 字符集校验、孤儿 tool_use 清理、推理签名保留。表明社区对 Claude 4.6+/5.x 系列模型的支持需求非常迫切。

**3. 多模型长会话稳定性**（#8207、#8003、#6721、#8258）
工具调用格式在长会话中退化为纯文本、缓存前缀失效等问题集中出现，提示社区对 180K+ 长上下文场景下的结构化输出保持率和推理缓存利用率有更高的期待。

**4. Web Shell 产品化**（#8248、#8234、#8229、#8132、#8250）
Web Shell 相关 PR 覆盖桌面打包（Tauri）、权限 UI 去重、artifact 下载、运行中消息注入，显示 Web Shell 正从实验特性走向完整产品形态。

**5. CI 稳定性治理**（#8256、#8244、#8237、#8076、#8115、#8259）
多条 CI 失败 issue 集中于异步 MCP 工具处理器、cron 集成、子代理委派等 E2E 用例，且与模型行为相关。应对策略从盲目重试转向跳过已知不稳定用例 + 硬化自托管 runner，体现社区对可重复构建的重视。


## 开发者关注点

- **工具调用格式可靠性**：多起问题指向模型在长上下文/特定轮次下将结构化工具调用泄漏为纯文本（XML 风格或 JSON 风格）。开发者希望更强的格式强制与降级恢复机制，而非仅靠模型自觉。
- **子代理交互闭环**：子代理提问无人应答的问题虽已关闭，但暴露了 subagent 与用户之间缺乏消息透传机制的设计缺口，后续或出现系统性方案。
- **Windows 平台安全弱化**：`O_NOFOLLOW` 缺失导致 `@`-file 保护在 Windows 上明显弱于 Linux/macOS，且无测试覆盖。跨平台安全一致性是高频期待。
- **缓存与性能的平衡**：延迟工具发现带来的缓存失效、file-search 对同一目录的重复忽略规则检查（#8252 约 41 倍冗余）表明，性能细节优化仍有显著空间。
- **内置分发渠道问题**：Minified React error #185（#5199）持续影响部分 Windows 用户，涉及 CherryStudio 分发路径中的 qwen-code 包加载异常，建议稳定复现路径后优先处理。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*