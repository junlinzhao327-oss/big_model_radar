# OpenClaw 生态日报 2026-09-19

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-19 15:06 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告



---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报  
**日期：2026-09-19**  
**数据来源：github.com/OpenHands/software-agent-sdk**

---

## 1. 今日速览

- 项目今日保持高活跃：过去 24 小时 Issues 更新 9 条、PR 更新 50 条，但新版本发布为 0。
- PR 侧呈现明显“入口宽、出口窄”：待合并 PR 达 46 条，已合并/关闭仅 4 条，合并/关闭比例约 8%，积压压力突出。
- 高优先级问题集中在三类：LLM provider 兼容性（#5181、#5168）、ACP 会话恢复失败（#5094）、Hosted Cloud 鉴权异常（#5189）。
- 积极信号是 #5184 已关闭，`sdk-tests` 在 `main` 上的红灯问题得到处理，有助于解除对开放 PR 的 CI 阻塞。
- 路线图信号以扩展模型/ provider 支持和 Agent Plugins 可移植插件标准为主，OCI Generative AI provider 已有对应 PR。

---

## 2. 版本发布

**今日无新版本发布。**

Releases 数据为空，暂无需说明破坏性变更或迁移注意事项。

---

## 3. 项目进展

### 已确认推进
- **关闭 #5184：修复 `main` 分支 `sdk-tests` 红灯**  
  该问题为 `kimi-k2.5` 的 `reasoning_effort` 期望值过期，导致模型特性测试失败，并影响所有开放 PR 的 CI 状态。已关闭意味着主分支测试阻塞被解除。  
  链接：https://github.com/OpenHands/software-agent-sdk/issues/5184

- **高优 Bug 已有配套修复 PR，待合并**
  - #5094 ACP `session/load` 失败静默开新会话 → 对应修复 PR #5095  
    Issue：https://github.com/OpenHands/software-agent-sdk/issues/5094  
    PR：https://github.com/OpenHands/software-agent-sdk/pull/5095
  - #5188 请求 OCI Generative AI provider 支持 → 对应 PR #5186  
    Issue：https://github.com/OpenHands/software-agent-sdk/issues/5188  
    PR：https://github.com/OpenHands/software-agent-sdk/pull/5186

### 功能/架构推进中的 PR
- #5151 `feat(agent-profiles): select every tool from one server catalog`：让 Agent Profile 从单一服务器目录选择工具，并移除 `enable_sub_agents`、`enable_switch_llm_tool`，与 #4958 相关。  
  https://github.com/OpenHands/software-agent-sdk/pull/5151
- #5182 `feat(security): emit SecurityAnalysisEvent with the analyzer's verdict per action batch`：为安全分析结果引入事件记录。  
  https://github.com/OpenHands/software-agent-sdk/pull/5182
- #4961 `feat: support Git identity in agent profiles`：支持 Agent Profile 级别的 Git 身份，并保留全局 Git 身份作为回退。  
  https://github.com/OpenHands/software-agent-sdk/pull/4961
- #5185 `Add newly released LLM models to verified lists`：由机器人提交，扩充已验证模型列表。  
  https://github.com/OpenHands/software-agent-sdk/pull/5185

### 数据缺口说明
今日 PR 更新中“已合并/关闭 4 条”，但给定数据未提供这 4 条 PR 的编号与标题；展示的 Top 20 PR 均为 OPEN，因此无法逐一确认已合并内容。PR 评论数也标记为 `undefined`，无法据此判断合并 PR 的讨论热度。

**整体判断：** 今日项目在 CI 阻塞解除和 Bug 修复配套方面有明确进展，但功能合并吞吐有限，大量 PR 仍停留在待合并状态。

---

## 4. 社区热点

按 Issues 评论数与反应数排序：

| 热度 | Issue | 评论 | 👍 | 状态 | 核心诉求 |
|---|---:|---:|---:|---|---|
| 1 | [#5168](https://github.com/OpenHands/software-agent-sdk/issues/5168) Telemetry `_cache_buckets` AttributeError | 7 | 1 | OPEN | 无 prompt caching 的 provider 不应导致崩溃，MiniMax 等自定义模型兼容性 |
| 2 | [#4405](https://github.com/OpenHands/software-agent-sdk/issues/4405) 支持 Agent Plugins 可移植包格式 | 6 |

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报
**日期：2026-09-19** ｜ 数据源：github.com/earendil-works/pi

---

## 一、今日速览

今日 Pi 项目呈现"高吞吐收敛"状态：过去 24 小时共处理 28 条 Issue，其中 **26 条被关闭**（关闭率 93%），6 条 PR 完成合并/关闭，说明维护团队正在进行一轮密集的 triage 与清理。值得关注的是，关闭队列中以 `[untriaged]` 标记的中小 bug/功能请求为主，多为当日提交、当日处理，响应速度极快。但同时有 3 条遗留 Issue（#7730、#9129）长期 OPEN，且 6 条 PR 仍待合并，其中 #8158、#5268 已是跨越 1 个月以上的长尾条目。**无新版本发布**，当前最新版本仍为 0.85.1。整体健康度良好，但"关闭多、合并少"的态势说明部分修复可能仍停留在 Issue 层而未落地为代码。

---

## 二、项目进展（今日合并/关闭的重要 PR）

今日共有 6 条 PR 被合并或关闭，覆盖 TUI 渲染、扩展 API、会话身份识别、崩溃防护四条主线：

| PR | 主题 | 价值 |
|---|---|---|
| [#5268](https://github.com/earendil-works/pi/pull/5268) | fix(tui): 默认渲染硬件光标，失焦时提示符光标变空心 | **跨度 110 天的长尾 PR 终于关闭**，修复 #3896，解决"未聚焦窗口仍显示为活跃"的视觉误导 |
| [#9434](https://github.com/earendil-works/pi/pull/9434) | feat(coding-agent): 允许扩展向 session system prompt 追加内容 | 关闭 #9432，为扩展生态开放 append-only 的 `systemPromptAppend` 贡献点，带顺序、来源元数据与错误隔离 |
| [#9772](https://github.com/earendil-works/pi/pull/9772) | fix(tui): 停止主屏 scrollback 清除/重放，修复 ConPTY 自动换行漂移 | 关闭 #9583，解决 Windows Terminal / pwsh 下 `eager` 提交换行导致的渲染错位 |
| [#9483](https://github.com/earendil-works/pi/pull/9483) | fix(coding-agent): tool cwd 解析改为 opt-in 的 `customCwd` | 回滚 #8627 引入的行为变更，恢复显式 `cwd` 的向后兼容，`ctx.cwd` 作为 fallback |
| [#9762](https://github.com/earendil-works/pi/pull/9762) | fix(coding-agent): 防护 TUI 遇到无 content 数组的工具结果 | 关闭 #9761，消除扩展工具返回非规范对象时的 `TypeError` 崩溃退出 |
| [#9754](https://github.com/earendil-works/pi/pull/9754) | fix(coding-agent): 同一仓库的 worktree 视为同一项目，解析 session-dir 符号链接 | 关闭 #9753，消除 worktree 会话恢复时误报"跨项目 Fork"的干扰 |

**推进评估**：本轮合并以稳定性与兼容性修补为主，无破坏性 API 变更迹象（#9483 反而是修复兼容性）。扩展生态得到两处增强（system prompt 追加、tool result 规范化防护），TUI 跨平台渲染质量提升明显。

---

## 三、社区热点

按评论数与点赞数排序，今日讨论最集中的条目如下：

**1. [#7730](https://github.com/earendil-works/pi/issues/7730) — macOS 长会话高 CPU 占用（16 评论，👍10，OPEN）**
今日绝对热点。用户 @gterzian 报告在 macOS 上 Pi 的 CPU 占用在 50%–110% 之间摆动，内存 600–800MB，疑似与上下文长度/会话时长相关。**该 Issue 自 8 月 6 日创建已开放 44 天**，是当前评论区最活跃的问题，10 个 👍 说明复现面较广。背后的核心诉求是：长会话场景下的资源管理（可能涉及 TUI 重渲染、消息历史处理）已成为 macOS 用户的真实瓶颈。

**2. [#7885](https://github.com/earendil-works/pi/issues/7885) — npm search 未索引新发布的 pi-packages（9 评论，已关闭）**
围绕 pi.dev/packages 画廊索引失效的持续讨论。用户指出 `npm search pi-affix-prompt` 无结果，导致新包无法出现在画廊。该问题与 [#7987](https://github.com/earendil-works/pi/issues/7987)（重新发布后仍缺席画廊，5 评论、👍2）互为印证，**共同指向包发现链路的结构性缺陷**——今日两者均已关闭，但需观察是否真正修复或仅被 `[no-action]` 归档。

**3. [#9690](https://github.com/earendil-works/pi/issues/9690) — OpenCode Zen 拒绝 Pi 会话 ID（4 评论，👍2，已关闭 [no-action]）**
Pi 0.85.1 内置 OpenCode provider 请求 OpenCode Zen 时返回 HTTP 403，原因是 Pi 生成的 session ID 不被识别为合法 OpenCode 会话。虽已关闭，但 `[no-action]` 标签意味着**很可能被判定为上游/第三方问题**，受影响用户在 0.85.1 上仍需规避。

**4. [#9129](https://github.com/earendil-works/pi/issues/9129) — Windows bash 超时 kill 遗留孤儿进程（4 评论，OPEN）**
`taskkill /F /T /PID <bash pid>` 在 Git for Windows (MSYS2) 下无法杀掉管道中间进程，导致超时后整条命令链未被真正终止。与 #7730 并列为当前仅存的两个 OPEN Issue 之一。

**5. [#8019](https://github.com/earendil-works/pi/issues/8019) — 保留硬换行与软换行语义（👍4，已关闭）**
获 4 个 👍 但评论仅 2 条，反映 TUI 鼠标选择复制时软换行被错误拼接的长期痛点，与 #506、#7721 形成问题簇。

---

## 四、Bug 与稳定性

按严重程度排列，标注修复状态：

###

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*