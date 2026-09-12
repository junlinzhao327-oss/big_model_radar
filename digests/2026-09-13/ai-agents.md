# OpenClaw 生态日报 2026-09-13

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-12 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-09-13

---

## 1. 今日速览

今日项目维持**极高活跃度**：过去 24 小时有 500 条 Issue 更新（270 条新开/活跃、230 条关闭）与 500 条 PR 更新（241 条待合并、259 条已合并/关闭），无新版本发布。整体看，社区投入集中在 **2026.9.3/2026.9.4 升级与恢复可靠性**（P0 追踪 Issue #145252 领衔）和**子代理/Swarm 编排的静默失败**两条主线上，两者合计占据了今日高评论量 Issue 的大半。维护者侧（@steipete、@eleqtrizit、@obviyus、@roboclaw-bot）在 UI 性能、Gateway 可见性、配置类型收敛等方向持续产出，PR 合并节奏稳健。同时，一批长期存在的 P0/P1 问题（设备配对恢复、僵尸进程、子代理完成丢失）仍未收敛，**积压结构性风险在上升**。总体健康度：**贡献管线旺盛，但回归与升级路径的质量是当前最大短板**。

---

## 2. 版本发布

无新版本发布。最新稳定线仍为 **2026.9.4**（多个 Issue 以该版本为复现环境），但需注意 2026.9.3 → 2026.9.4 的升级路径在今日暴露多个 P0 阻塞（见第 5 节）。

---

## 3. 项目进展

今日关闭/合并的 PR 与 Issue 显示，项目在**运行时

---

## 横向生态对比

> 说明：本次输入中 **Hermes Agent、OpenHands SDK、LiteLLM、Temporal** 无正文动态数据，以下定量对比仅覆盖 **OpenClaw** 与 **Pi**；其余项目以“未提供/数据缺失”标记，不做推断性评估。

---

## 1. 生态全景

2026-09-13 可见样本显示，个人 AI 助手/自主智能体开源生态处于 **“高吞吐迭代 + 可靠性补课”并行阶段**。头部项目 OpenClaw 日 Issue/PR 更新各达 500 条，社区规模与治理压力远超 Pi 的 42/10，显示核心平台型项目已进入大规模协作与积压治理期。Pi 则围绕 TUI、会话树、OAuth 提供商扩展快速推进，终端编码代理的体验竞争仍在加剧。多项目共同暴露的问题从“功能缺失”转向 **升级回归、连接可靠性、子代理静默失败、可观测性不足**。今日无新 Release，社区重心更偏向修复与稳定窗口积累。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | Release | 健康度评估 |
|---|---:|---:|---|---|
| **OpenClaw** | 500：270 新开/活跃，230 关闭 | 500：241 待合并，259 合并/关闭 | 无；最新稳定线 2026.9.4 | 极高活跃，贡献管线旺盛；但 2026.9.3→9.4 升级/恢复 P0、子代理/Swarm 静默失败、设备配对/僵尸进程等积压未收敛，结构性风险上升 |
| **Pi** | 42：17 新开/活跃，25 关闭 | 10：3 待合并，7 合并/关闭 | 无；上一版 0.85.1 | 高强度活跃，关闭/合并率 59.5%/70%，吞吐健康；但 #4945 openai-codex 连接可靠性、Windows 边缘问题仍是拖累 |
| **Hermes Agent** | 未提供 | 未提供 | 未提供 | 数据缺失，无法评估 |
| **OpenHands SDK** | 未提供 | 未提供 | 未提供 | 数据缺失，无法评估 |
| **LiteLLM** | 未提供 | 未提供 | 未提供 | 数据缺失，无法评估 |
| **Temporal** | 未提供 | 未提供 | 未提供 | 数据缺失，无法评估 |

补充指标：OpenClaw 今日 Issue 净增约 40 条、待合并 PR 241 条；Pi Issue 净减 8 条、PR 净减 4 条。前者体现规模优势与治理压力并存，后者体现更健康的收敛节奏

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目日报 · 2026-09-13

> 数据窗口：2026-09-12 至 2026-09-13（过去 24 小时）
> 数据来源：github.com/earendil-works/pi

---

## 一、今日速览

过去 24 小时 Pi 项目维持**高强度活跃**：Issues 更新 42 条（新开/活跃 17、关闭 25），PR 更新 10 条（待合并 3、合并/关闭 7），关闭/合并率分别达 **59.5%** 和 **70%**，维护吞吐处于健康区间。今日无新版本发布，但社区提交了多个面向 TUI 体验、会话树管理、OAuth 提供商扩展的高质量 PR，其中 Google Antigravity/Cursor Pro 提供商、会话树分支删除、全屏提示事件补全等已落地。与此同时，长期悬而未决的 **#4945 openai-codex 连接可靠性问题**仍以 78 条评论、33 个 👍 占据热度榜首，是当前最需要集中火力的稳定性风险点。整体判断：**修复产能强劲，但核心 Codex 传输稳定性与 Windows 平台边缘问题仍是拖累项**。

---

## 二、版本发布

**无新版本发布。** 上一版本为 0.85.1（多个 Issue 中引用），今日无 Release 活动。

---

## 三、项目进展

今日合并/关闭 7 个 PR，推进方向集中在「TUI 体验」「会话树管理」「生态提供商扩展」「AI 采样参数修复」四条线：

| PR | 状态 | 推进内容 |
|---|---|---|
| [#9529](https://github.com/earendil-works/pi/pull/9529) | CLOSED | **新增 Google Antigravity 与 Cursor Pro 两个订阅制 OAuth 提供商**，无需 API Key，Antigravity 走 `accounts.google.com` Cloud Code Assist 客户端 + 本地回调端口 51123；对应关闭 Issue #9530。这是本月最大的生态扩展之一。 |
| [#9531](https://github.com/earendil-works/pi/pull/9531) | CLOSED | **会话树支持永久删除分支**：新增 `SessionManager.pruneBranch()` / `countSubtree()`，保护活跃路径、保留叶子、重链 labels、重定向 surviving compactions，并在 `/tree` 选择器加入 `shift+d` 交互。 |
| [#9523](https://github.com/earendil-works/pi/pull/9523) | CLOSED | 修复 #9522：Pi 自身的阻塞式对话框（模型选择器、设置、resume、session tree）此前不发出 `ui_prompt_start/_end`，现统一经 `showSelector()` 补全事件，使状态集成能正确报告「等待用户」。 |
| [#9517](https://github.com/earendil-works/pi/pull/9517) | CLOSED | TUI 将连续 ≥6 次工具调用折叠为聚合行，失败调用保留并提供点击展开，附带渲染测试。 |
| [#9514](https://github.com/earendil-works/pi/pull/9514) | CLOSED | 将 TUI 编辑器/输入框/模型选择器中的硬编码快捷键改为可配置 keybinding；新增 Ctrl+C 清空搜索、Shift 修饰删除等回归测试。注：coding-agent 测试因环境缺少构建产物未通过，与本改动无关。 |
| [#9505](https://github.com/earendil-works/pi/pull/9505) | CLOSED | 修复 `openai-completions` 流式路径丢弃 `model.samplingParams` 的问题（vLLM/llama.cpp 的 `repetition_penalty`、`dry_multiplier` 等引擎级参数此前静默失效）。 |
| [#9532](https://github.com/earendil-works/pi/pull/9532) | CLOSED | 空描述 PR（作者 @ma

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*