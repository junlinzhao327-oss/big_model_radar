# AI CLI 工具社区动态日报 2026-08-30

> 生成时间: 2026-08-30 00:26 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-08-30）

## 1. 生态全景

当前 AI CLI 工具正处于**功能深化与平台兼容性磨合期**。各主流工具在 MCP 生态、插件体系、多代理能力上快速迭代，同时集中暴露出 **Windows 平台稳定性差、配额计费透明度不足、长会话可靠性存疑** 等共性问题。头部工具如 OpenAI Codex、GitHub Copilot CLI 已进入稳定版+频繁补丁阶段，OpenCode 等开源工具则以高 PR 数量保持着快速迭代节奏。整体而言，社区对“开箱即用”的跨平台体验和“成本可控”的透明机制提出了更高要求。

## 2. 各工具活跃度对比

| 工具 | 今日 Issue 情况 | 今日 PR 情况 | Release 情况 |
|------|----------------|-------------|--------------|
| Claude Code | 无数据（未提供摘要） | 无数据 | 无数据 |
| OpenAI Codex | 列示热点 10 个 | 列示合并且进展 10 个 | 1 个稳定版 + 3 个 alpha |
| Gemini CLI | 未提供具体数量（围绕子代理稳定性） | 未提供具体数量（密集修复 hooks、A2A、MCP） | 1 个 nightly |
| GitHub Copilot CLI | 近 24h 更新 7 个 | 3 个（2 关闭 + 1 开放） | 2 个补丁（v1.0.82 / v1.0.82-2） |
| Kimi Code CLI | 1 个 | 0 个 | 无 |
| OpenCode | 列示热点 10 个 | 列示 10 个 | 无新版本 |
| Qwen Code | 无数据（未提供摘要） | 无数据 | 无数据 |

> 注：表中“列示”表示数据源摘录的高优/重点条目，不等于当日全部条目；未提供具体数量的工具以文本描述为准。

## 3. 共同关注的功能方向

| 方向 | 涉及的工具有 | 具体诉求示例 |
|------|-------------|-------------|
| **配额 / 用量透明化** | OpenAI Codex、Kimi Code、OpenCode | Codex 要求永久移除 5h 限制并公开明细；Kimi 报告缓存计费放大 10 倍；OpenCode 显示百分比与实际用量不符甚至超 100% |
| **Windows 平台稳定性** | OpenAI Codex、Copilot CLI、OpenCode | Codex 多个 Windows Bug（行尾、插件更新、沙箱失败）；Copilot `--resume` 冷启动卡死；OpenCode 错误调用 PowerShell 5.1、GUI 标签页空白 |
| **MCP 兼容性与认证** | OpenAI Codex、Copilot CLI、OpenCode | Codex 扩展 MCP 工具结果检查与发现宽限期；Copilot 远程 ADO MCP OAuth 失败、chroma-mcp 回归；OpenCode 增加 per-MCP-server 信任配置 |
| **插件 / Agent 生态标准化** | Copilot CLI、OpenCode、Gemini CLI | Copilot 自定义 agent 不被发现、`.agents` 目录扩展；OpenCode 插件列表空白、GUI 插件管理入口缺失；Gemini 修复 hooks 迁移 |
| **会话 / 历史可靠性** | OpenAI Codex、Copilot CLI、OpenCode | Codex 分页解码错误、resume 游标不同步；Copilot Windows resume 卡死；OpenCode agent 非终止循环、上下文压缩后 MCP 工具清单归零 |
| **多代理 / 子代理可配置性** | OpenAI Codex、Gemini CLI、OpenCode | Codex 子代理忽略 `model_provider` 覆盖；Gemini 子代理 MAX_TURNS 超时误报成功；OpenCode 需要循环检测与熔断机制 |

## 4. 差异化定位分析

- **OpenAI Codex**：以 **Rust 重写 + 稳定版/alpha 双轨发布** 为技术路线，重点强化 MCP 工具链、插件目录和长会话一致性。PR 密集，注重沙箱权限与 exec 故障防护，面向追求工程化、多代理场景的专业开发者。
- **GitHub Copilot CLI**：深度绑定 **GitHub 工作流**（worktree、move、codespaces），发布节奏紧凑（双补丁）。侧重于 CLI 与 Git 操作的顺畅衔接，兼容性回归问题较多，说明其在激进演进的同时需补强回归测试。
- **Gemini CLI**：推 **A2A 协议** 与受限模式信任策略，关注子代理稳定性和 hooks 迁移。技术路线偏 Google 生态，nightly 版本意味着仍处于快速实验期。
- **OpenCode**：**开源、高度可配置**，TUI/Web/GUI 多端并进。PR 涵盖面广（webfetch 超时、NVIDIA NIM 兼容、iOS PWA、plans 目录自定义），体现出社区驱动的广谱适配，但对核心稳定性的打磨仍显不足。
- **Kimi Code CLI**：当前数据点较少，仅反映**付费配额与缓存计费问题**。可能正处于早期推广阶段，社区讨论以成本敏感型问题为主，或尚未形成活跃的第三方生态。
- **Claude Code / Qwen Code**：本次未提供有效动态数据，无法进行定位分析。

## 5. 社区热度与成熟度

| 工具 | 活跃度 | 成熟度 |
|------|--------|--------|
| OpenAI Codex | **极高**：多个热点 Issue 获得高赞（如 #34035 获 151 👍），10 个 PR 合并，Release 高频 | **高**：稳定版 + alpha 并进，系统性修复会话/权限/MCP 问题 |
| OpenCode | **极高**：10 个热点 Issue + 10 个 PR，覆盖 CLI/GUI/Web 多端 | **中高**：无新版本但 PR 密集，功能迭代快，稳定性问题仍存 |
| GitHub Copilot CLI | **较高**：7 个 Issue 更新 + 3 个 PR，双补丁发布 | **高**：版本稳定，但近期回归问题影响可信度 |
| Gemini CLI | **中**：有 nightly 发布和 PR 密集修复，但未提供具体数量 | **中**：仍在 nightly 阶段，协议层（A2A）探索中 |
| Kimi Code CLI | **低**：仅 1 个 Issue，无 PR 和 Release | **低/早期**：社区基数尚小，核心问题在计费 |
| Claude Code / Qwen Code | 无数据 | 无数据 |

## 6. 值得关注的趋势信号

1. **Windows 支持已成为共性短板**：Codex、Copilot、OpenCode 均出现大量与 Windows 相关的 Bug（路径、Shell、插件、GUI）。AI CLI 工具若想扩大用户池，必须将 Windows 作为一等公民对待。
2. **配额计费透明度决定付费用户信任**：从 Codex 的 151 👍 诉求到 Kimi 的缓存计费异常、OpenCode 的百分比显示错误，用户对“看不见的消耗”非常敏感。工具需要提供可审计的用量明细和更灵活的策略。
3. **MCP 正成为默认集成层，但仍缺乏成熟治理**：各工具都在扩张 MCP 能力，但认证失败、兼容性回归、per-server 信任问题频发。MCP 的标准化和安全性将是下一阶段竞争重点。
4. **长会话可靠性与资源控制是“重度使用”的门槛**：会话历史解码错误、resume 卡死、token 无限消耗等议题高频出现，说明开发者已将 AI CLI 用于数小时甚至跨天的任务，会话生命周期管理成为刚需。
5. **插件生态与多代理开始分化**：Copilot 关注 Agent Plugins 规范发现，Codex 强化多代理指令，OpenCode 构建插件列表，Gemini 修 A2A 协议。各工具正向“平台化”演进，但生态标准尚未统一。
6. **CLI 工具正在“GUI 化”**：OpenCode 的桌面端增强、Copilot 的计划卡片展开、Codex 的模型选择器刷新等，都表明纯终端交互已无法满足用户对可观测性和易用性的需求，混合界面成为新方向。

---

*数据来源：各工具 GitHub 仓库公开 Issues、PRs、Releases 摘要（2026-08-30）。*

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

## OpenAI Codex 社区动态日报 — 2026-08-30

### 今日速览
昨日共发布 1 个稳定版（rust-v0.151.0）及 3 个 alpha 版本，重点增强 MCP 工具链与插件目录管理能力。社区最关注的话题集中在两点：Windows 平台系列 Bug 的集中爆发（行尾混乱、远程信任验证失败、插件更新残留等），以及用量配额消耗透明度的强烈诉求（#34035 获得 151 个 👍）。此外，多项会话历史一致性修复 PR 已合并，反映官方正在系统性地解决长期会话的可靠性问题。

### 版本发布
**rust-v0.151.0**（稳定版）
- 新增可选 MCP 服务器的工具发现宽限期配置（#41199）
- 扩展可在工具结果到达模型前检查或替换 MCP 工具结果（#41202）
- 插件目录现支持合并仓库级配置，并会报告无效项目 marketplace

另有 3 个 alpha 版本：rust-v0.152.0-alpha.1、rust-v0.151.0-alpha.7.2、rust-v0.151.0-alpha.12（发布说明详见各自 Release 页）。

---

### 社区热点 Issues（10 个）

1. **#34035 [增强] 将 5 小时用量限制的临时移除永久化** — 151 👍 / 21 评论
   社区呼声最高的议题。用户要求将 Plus/Pro/Business 计划中临时取消的 5 小时限制永久化，同时保留每周用量限额。反映出用户对当前计费与速率限制政策的不确定性感到焦虑。
   https://github.com/openai/codex/issues/34035

2. **#4003 [已关闭] Windows 上修补文件出现混合行尾** — 75 👍 / 37 评论
   0.39.0 版本中 Codex 修改文件时不遵守原有行尾风格，导致 CRLF/LF 混杂。虽然是已关闭的历史 Issue，但高赞数说明该问题在 Windows 用户群体中影响深远。
   https://github.com/openai/codex/issues/4003

3. **#35746 [Bug] 分页历史记录丢弃有效扁平化记录并复用序号** — 34 评论
   分页 rollout 历史存在 `RolloutLine` 解码不一致，导致记录丢失和序号复用。会话历史的可靠性问题已成为近期开发者核心痛点之一。
   https://github.com/openai/codex/issues/35746

4. **#32706 [Bug] Windows/Edge：Chrome 插件更新遗留锁定主机、部分缓存及无法卸载的插件** — 17 评论
   涉及 Codex AppX、CLI 与 Chrome 扩展联动的复杂更新失败链，更新后插件状态不一致且无法自行修复，Windows 用户受影响严重。
   https://github.com/openai/codex/issues/32706

5. **#39855 [Bug] Windows 远程：每次新建 projectless 聊天都因路径格式错误而信任验证失败** — 9 👍 / 17 评论
   Windows 桌面版在远程会话中，新建聊天时信任验证总是中断。路径的 Windows 格式（如反斜杠）未能在远程上下文中被正确解析。
   https://github.com/openai/codex/issues/39855

6. **#38792 [Bug] 恢复长线程时定位到首轮：0.146.1 游标不同步且后续版本未修复** — 4 👍 / 15 评论
   在超长会话中执行 resume 时，线程历史投影游标错位，导致打开位置错误或内容缺失。该报告由 AI 助手代用户提交，测量数据详实。
   https://github.com/openai/codex/issues/38792

7. **#39699 [Bug] Windows 桌面版：每周配额在日常开发中消耗异常快速** — 10 评论
   用户报告没有明显高密度操作时配额快速下降，引发对配额计费透明度的质疑，是 #34035 之外另一个配额相关的高频反馈。
   https://github.com/openai/codex/issues/39699

8. **#40596 [Bug] Windows Codex App：统一执行失败，报 `helper_unknown_error: setup refresh had errors`** — 10 评论
   Windows 上启动统一 exec 终端时一致失败，属于 Windows 沙箱链路的持续性问题之一。
   https://github.com/openai/codex/issues/40596

9. **#40858 [Bug] 原生子代理忽略 `model_provider` 显式覆盖** — 4 👍 / 5 评论
   父模型与子代理使用不同模型时，子代理不读取配置中的 `model_provider`，导致多代理场景下无法灵活切换供应商，对自定义模型用户影响较大。
   https://github.com/openai/codex/issues/40858

10. **#40002 [Bug] Android 远程对受信任的 Windows 项目验证失败（路径大小写）** — 8 👍 / 12 评论
   从 Android 端发起远程连接 Windows 主机时，因路径大小写不一致导致信任校验失败。跨平台路径语义差异已成为远程功能的系统性问题。
    https://github.com/openai/codex/issues/40002

---

### 重要 PR 进展（10 个）

1. **#41569 加固诊断报告上传** — 已合并
   将核心报告事件与附件分离上传，每个附件以 gzip 压缩信封独立发送；同时限制编解码大小并对超大附件做格式感知截断。显著提升崩溃诊断的可靠性。
   https://github.com/openai/codex/pull/41569

2. **#41567 从自有设置快照恢复线程 cwd** — 已合并
   修复 resume 线程时 cwd 可能来自其他线程或被压缩移出回放窗口的问题，确保恢复的线程使用其最新保留的工作目录。
   https://github.com/openai/codex/pull/41567

3. **#41562 保留目标延续中的轮次归属** — 已合并
   自动目标延续的轮次现在可正确归属到创建目标的原始轮次，避免外部输入或目标编辑导致归属混乱和陈旧元数据残留。
   https://github.com/openai/codex/pull/41562

4. **#41477 将捆绑的 Rust 资源移入 asset 目录** — 已合并
   重构 Bazel 构建中 `core` 与 `tui` 的数据依赖，将运行时资源与源代码、测试夹具分离，减小编译树体积并提升构建清晰度。
   https://github.com/openai/codex/pull/41477

5. **#41467 从 app server 刷新 TUI 模型选择器** — 已合并
   模型选择器现在打开时异步拉取当前账户的模型列表，避免使用启动时缓存的过时目录；同时保留缓存占位以快速渲染。
   https://github.com/openai/codex/pull/41467

6. **#41464 更新会话元数据时保留权限快照** — 已合并
   推迟沙箱策略投影直到工作目录变更需要重新绑定；客户端名称/版本更新不再触发不必要的权限解析或变更。
   https://github.com/openai/codex/pull/41464

7. **#41457 从模型目录获取主动多代理指令** — 已合并
   模型元数据新增可选 `proactive` 多代理消息，`Ultra` 推理模式在无显式全局提示时使用目录内的消息，缺失时回退到内置指令。
   https://github.com/openai/codex/pull/41457

8. **#41454 重复执行主机故障后阻止目标** — 已合并
   跟踪每个活动目标中 `exec` 失败的次数，连续三次失败后标记目标为 blocked；任一工具成功后重置失败计数，且不跨目标转移失败状态。
   https://github.com/openai/codex/pull/41454

9. **#41452 上报代码模式主机请求持续时间** — 已合并
   Code mode 的 wall time 现在只测量主机操作本身（execute/wait/terminate），不再包含客户端响应延迟或空闲时间，提升性能指标的真实性。
   https://github.com/openai/codex/pull/41452

10. **#41447 支持 `openai/elicitation` 表单请求** — 已合并
    新增对 `openai/elicitation/create` 的处理，基于客户端声明的对象类型 `form` 能力来通告支持，不再依赖旧版 `openai/form` 能力推导。
    https://github.com/openai/codex/pull/41447

---

### 功能需求趋势

- **Windows 平台稳定性修复**：约半数近期 Issue 涉及 Windows（行尾、插件更新、沙箱初始化、路径大小写、宠物窗口交互等），已成为社区最集中的抱怨来源。
- **用量配额透明化与控制**：#34035（移除 5 小时限制）和 #39699（配额消耗过快）双双进入热点榜，用户期待给出更清晰的配额使用明细和更灵活的限制策略。
- **会话/历史记录可靠性**：分页解码错误、游标不同步、压缩导致上下文丢失、重复序号等大量相关 Bug，开发者需要长时间任务可恢复且不丢失上下文。
- **远程跨平台体验**：多个远程会话相关 Issue（#39855、#40002、#41532）指向文件路径、信任验证、资源预览的跨平台不一致问题。
- **多代理/子代理可配置性**：#40858（model_provider 覆盖）、#40131（符号链接自定义代理角色）表明高级用户对子代理自定义有更多需求。
- **UI/UX 细节打磨**：自动展开 Working 区域（#22334）、宠物窗口交互（#41465、#41501）、滚动定位（#38113）等，显示桌面 App 进入精细化打磨阶段。

### 开发者关注点

- **Windows 用户正遭受大面积 Bug 困扰**：从核心编辑（行尾）到沙箱执行、插件管理到 UI 交互，Windows 平台的问题跨度最广且数量最多，建议官方优先投入。
- **配额/费用安全引人担忧**：#40871 中用户被静默切回 2024 年的旧 API key，一夜产生约 758 美元费用，引发对计费安全机制的不信任。
- **长期会话的资源失控**：#35383（202 GB 临时文件堆积）、#40323（rollout 超过 16 GiB）表明持久化资源管理不足，用户要求更可靠的生命周期控制和体积上限。
- **恢复和续接体验是信任基石**：多个 Issue 指向 resume 后定位错误、历史缺失或冻结，已直接影响重度用户对 Codex 的依赖程度。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报（2026-08-30）

## 今日速览

Gemini CLI 发布 v0.59.0-nightly.20260829，在受限模式下强制工作区信任策略。社区议题继续围绕子代理稳定性展开：MAX_TURNS 超时被误报为成功、通用代理无限挂起等 bug 引发高频讨论；PR 侧则密集修复了 hooks 迁移、A2A JSON-RPC 解析与 MCP

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-08-30）

## 1. 今日速览

今日发布 Copilot CLI `v1.0.82` / `v1.0.82-2` 两个补丁版本，主要修复 `/worktree`、`/move` 切换场景下的输入丢失问题，并优化计划审批卡片的展开体验。社区方面，Windows 下 `--resume` 卡死、MCP 兼容性与认证失败、以及 patch 应用无限循环成为今日最集中的反馈热点。

## 2. 版本发布

**v1.0.82**（2026-08-29）  
- 修复在 `/worktree` 或 `/move` 准备 worktree 期间输入消息，导致切换失败的问题。  
- `Ctrl+E` 现在可以展开计划审批卡片，重新查看完整计划。  
- 认证失败时展示具体原因（如 `401 Bad credentials`），而不再只提示执行 `/login`。

**v1.0.82-2**  
- 同步包含上述 worktree 输入破损问题的修复。  
- 继续优化 `Ctrl+E` 展开计划审批卡片的行为。

发布链接：https://github.com/github/copilot-cli/releases

## 3. 社区热点 Issues

当前共有 7 个 Issue 在近 24 小时内更新，全部列出：

- **[#4165] copilot --resume 在 Windows 冷启动时卡在 Resuming session**  
  链接：https://github.com/github/copilot-cli/issues/4165  
  作者是 @asalcedo29，创建于 2026-07-17，已有 4 条评论、1 个 👍。问题影响 Windows PowerShell 用户：直接执行 `copilot --resume` 会卡在“Resuming session...”，但相同会话通过先启动 CLI 再恢复却能成功。这是长期未解决的高频痛点，涉及 sessions 与 Windows 平台两个 area。

- **[#4204] 请求在任意打开文件夹中支持 `.agents` 发现机制**  
  链接：https://github.com/github/copilot-cli/issues/4204  
  由 @mu88 提出，希望把现有 `.agents/skills` 约定扩展为可发现 instructions、agents、hooks，并且不局限于 Git 仓库。该需求若落地，将显著增强 Copilot CLI 在多目录场景下的标准化定制能力。

- **[#4647] v1.0.81 破坏与 chroma-mcp 的兼容性**  
  链接：https://github.com/github/copilot-cli/issues/4647  
  用户 @janwilch 报告从 v1.0.80 升级到 v1.0.81 后，chroma-mcp 无法正常使用。目前标记为 `triage`，2 条评论，说明版本升级带来的 MCP 回归需要尽快确认。

- **[#4655] Agent Plugins 1.0 规范中的自定义 agents 无法被发现**  
  链接：https://github.com/github/copilot-cli/issues/4655  
  @mcollier 在构建插件时发现，按 Agent Plugins 规范放置的 `com.github.copilot/agents` 自定义 agent 未被 CLI 识别。该问题直接影响插件生态建设，值得关注。

- **[#2955] `/allow-all` 无法抑制 bash 工具执行确认弹窗**  
  链接：https://github.com/github/copilot-cli/issues/2955  
  创建于 4 月，今日仍有更新。用户执行 `/allow-all` 后，每次调用 bash/shell 工具依然会弹出“Do you want to run this command?”权限对话框。这是权限模型一致性方面的重要反馈。

- **[#4660] 远程 ADO MCP Server 在 v1.0.81 WAM 实现下 OAuth 失败**  
  链接：https://github.com/github/copilot-cli/issues/4660  
  由 @dak-cimpeco 今日报告：Azure DevOps 远程 MCP server 加载时提示“requires authentication”，执行 `/mcp auth` 后又报“Authentication Failed”。涉及新版 WAM 认证实现，疑似回归问题。

- **[#4553] Copilot CLI 因 JSON 包装错误无限循环，apply_patch 持续失败**  
  链接：https://github.com/github/copilot-cli/issues/4553  
  用户 @hey-nikhil 反馈：在需要修改文件的编码任务中，CLI 反复尝试同一补丁，因 JSON 包装错误失败后不断重试，导致任务卡死。涉及 models 与 tools 两个核心 area，属于高影响稳定性问题。

## 4. 重要 PR 进展

今日有 3 个 PR 产生更新：

- **[#4659] Initial commit with exported changes from codespace**  
  链接：https://github.com/github/copilot-cli/pull/4659  
  由 @HACK55515 提交，内容是从 codespace 导出的变更，目前处于 Open 状态。描述较模糊，需要维护者判断是否为有效改动。

- **[#2381] install: 增加 fish shell 的 PATH 配置支持**（已关闭）  
  链接：https://github.com/github/copilot-cli/pull/2381  
  @marcelsafin 修复了 fish shell 用户安装时被归入 `*)` 分支、错误写入 `~/.profile` 的问题。fish 不读取 `~/.profile`，也不支持 `export PATH` 语法，因此原实现会静默失败。该 PR 对非 bash/zsh 用户很有价值。

- **[#4497] 处理 fork PR 关联缺失时的 invalid-label writer 逻辑**（已关闭）  
  链接：https://github.com/github/copilot-cli/pull/4497  
  @mrecachinas 修复了 fork PR 工作流中 GitHub 未填充 PR association 的场景：现在 writer 会基于可信工作流元数据查找，并要求恰好一个打开的 PR 来关联，以提升标签写入的可靠性。

## 5. 功能需求趋势

从今日 Issue 与 PR 中可以看到社区最关注的几个功能方向：

- **标准化 Agent/Instructions 发现机制**：多个 Issue 指向需要更统一的 `.agents` 目录约定，并希望支持非 Git 仓库、Agent Plugins 规范下的自定义 agents。
- **跨平台体验一致性**：Windows 下的 `--resume` 卡死是长期问题，社区期待更稳定的会话恢复机制。
- **MCP 生态兼容性**：新版本对 MCP server 的认证方式、兼容性改动引发了回归，社区需要更平滑的迁移路径。
- **Shell 集成完善**：fish shell 的 PATH 配置支持合并请求说明用户在非主流 shell 下的安装体验仍有欠缺。
- **权限控制可预期性**：`/allow-all` 行为不一致，开发者希望对权限允许/确认机制有更明确、可配置的控制。

## 6. 开发者关注点

综合今日反馈，开发者的主要痛点集中在：

- **会话与平台稳定性**：Windows 上 `--resume` 长时间无响应，影响日常恢复工作流。
- **MCP 认证链路脆弱**：远程 MCP server 在当前 WAM/OAuth 实现下容易出现“Authentication Failed”，且缺少足够可操作的错误信息。
- **补丁应用循环**：`apply_patch` 因 JSON 包装错误反复重试，导致任务无法推进。
- **权限弹窗干扰**：即使用户显式 `/allow-all`，bash 工具调用仍会触发确认提示，降低自动化流畅度。
- **版本升级回归**：v1.0.81 引入的 MCP 兼容性问题让部分用户不敢直接升级，期待更严格的回归测试。

> 提示：以上数据来自 GitHub 公开仓库 `github/copilot-cli` 的 Issues、PRs 与 Releases，统计时间为 2026-08-30。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-08-30）

> 数据源：github.com/MoonshotAI/kimi-cli  
> 说明：截至日报生成时，过去 24 小时数据源仅包含 1 条更新 Issue、0 条 PR，未达到“10 条热点/PR”的预设数量，因此以下列出全部可获取条目，并基于该条目进行趋势分析。

## 今日速览

- 过去 24 小时无新版本发布，也无 PR 更新。
- 社区唯一动态是一则付费用户提交的配额异常消耗 Issue（#2626）：轻度使用几分钟内 5 小时配额窗口损失约 40%，且日志显示 `cache_read` 每轮都被计费、`cache_creation` 始终为 0。
- 该问题直指缓存计费逻辑的可信度，预计会成为近期稳定性与计费修复的重点。

## 版本发布

过去 24 小时无新版本发布。

## 社区热点 Issues

由于数据源仅包含 1 条更新 Issue，以下为全部值得关注条目：

### #2626 [OPEN] 异常配额消耗：cache_read 每轮计费、cache_creation 始终为 0（>10 倍放大）

- 作者：[@ahmadyaseen35-coder](https://github.com/ahmadyaseen35-coder)
- 创建时间：2026-08-29 | 更新时间：2026-08-29 | 评论数：1 | 👍：0
- 链接：[https://github.com/MoonshotAI/kimi-cli/issues/2626](https://github.com/MoonshotAI/kimi-cli/issues/2626)
- **为什么重要**：付费年度订阅用户反馈，在轻度使用下，5 小时配额窗口在几分钟内损失约 40%；用户通过 CLI 日志发现 `cache_read` 在每一轮都被计费，且 `cache_creation` 始终为 0，导致缓存计费被放大超过 10 倍。这直接影响到用户对缓存机制和配额消耗的信任，属于计费正确性 / 服务端缓存策略相关的严重问题。
- **社区反应**：目前仅有 1 条评论，还没形成大规模讨论；但由于涉及真金白银的配额消耗，预计会快速吸引更多受影响用户参与。

## 重要 PR 进展

过去 24 小时内没有 PR 创建或更新，暂无条目可展示。

## 功能需求趋势

基于当前唯一 Issue，社区最突出的功能需求方向是：

- **缓存计费透明度**：用户希望能区分 `cache_read` 是否真正命中缓存，而不是每轮都按读取计费。
- **配额消耗诊断能力**：用户希望 CLI 能提供更细粒度的配额消耗日志、会话级统计或可视化面板，便于定位“几分钟内消耗 40%”的异常场景。
- **计费修复与补偿机制**：对于已发生的异常计费，用户期待官方提供账单核对入口或自动补偿。

## 开发者关注点

- **痛点**：付费用户配额异常消耗问题严重，且缺少缓存命中率 / 配额消耗的实时诊断手段。
- **高频需求**：
  - 修复 `cache_read` 与 `cache_creation` 比例异常的问题，避免空转计费。
  - 提供本地日志或遥测接口，量化每次请求的缓存命中情况和配额扣减明细。
  - 建立异常配额消耗的快速反馈通道，降低用户举证难度。

---

以上为 2026-08-30 Kimi Code CLI 社区动态日报。若后续数据源补充，可再扩展热点 Issue 和 PR 列表。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-30

## 今日速览
过去 24 小时无新版本发布，但社区围绕 **GUI 回归问题**、**配额计算准确性** 与 **agent 工具调用循环** 的讨论明显升温。Windows 桌面端 Plugins 标签页空白、LPU 菜单丢失等回归问题被集中报告；同时，多个提交修复了 webfetch 超时、NVIDIA NIM 兼容性、TUI 上下文计算等实际缺陷。

---

## 社区热点 Issues（10 条）

**1. Auto-sync 项目同步功能**
[#13626](https://github.com/anomalyco/opencode/issues/13626) — 在新设备/浏览器打开 OpenCode Web 时，应从服务器自动获取并同步项目列表。持续半年的高赞功能请求（👍 15，评论 15），反映了多设备工作流中项目同步的刚需。

**2. 文档误导：LSP 被描述为默认启用**
[#23566](https://github.com/anomalyco/opencode/issues/23566) — 实际 LSP 默认关闭，但文档中“Auto-installs for Kotlin projects”等描述暗示默认开启。社区高关注（👍 22），文档准确性问题直接影响新用户上手体验。

**3. LM Studio 显示未配置模型**
[#4232](https://github.com/anomalyco/opencode/issues/4232) — 清理配置后，OpenCode 仍显示 LM Studio 中不存在的模型。老问题（2025-11-12 创建）至今仍被讨论，说明本地模型提供商的兼容性验证存在缺口。

**4. GUI 配置 per-model 参数**
[#46153](https://github.com/anomalyco/opencode/issues/46153) — 希望直接在 GUI 中配置每个模型的 system prompt、temperature、context window 等参数，无需手改 `opencode.jsonc`。8/29 新建，评论 6，与近期 GUI 增强方向一致。

**5. 5 小时限制计算异常**
[#38570](https://github.com/anomalyco/opencode/issues/38570) — 用户仅消费 $1.50 却显示已用 47%，百分比计算明显不合理。配额信任问题引发讨论，直接影响付费用户对限额机制的信心。

**6. Windows 下错误使用 PowerShell 5.1**
[#17372](https://github.com/anomalyco/opencode/issues/17372) — 从 PowerShell 7 启动 OpenCode，但执行 bash 命令时却调用系统自带的 5.1，导致 profile 和环境变量不加载。Windows 开发者高频踩坑点。

**7. Copilot Student 计划无法使用 provider**
[#34644](https://github.com/anomalyco/opencode/issues/34644) — 完成 OAuth 后 `github-copilot` provider 不出现在模型选择器中，仅 Auto-only 模式可用。👍 17，学生用户群体影响面大。

**8. Windows GUI：Plugins 标签页空白（回归）**
[#46155](https://github.com/anomalyco/opencode/issues/46155) — 状态 popover 中 Plugins 标签在 Windows 上显示为空，疑似竞态条件导致插件列表未加载。8/29 新报告，属 GUI 严重回归。

**9. 恢复 LPU/Plugin 标签按钮菜单**
[#46151](https://github.com/anomalyco/opencode/issues/46151) — 请求恢复状态 popover 中已丢失的 LPU/Plugin 标签按钮菜单。与 #46155 同源，社区对插件管理入口的缺失感到不满。

**10. agent 陷入非终止循环**
[#43673](https://github.com/anomalyco/opencode/issues/43673) — 调查插件更新 toast 时，agent 连续执行数十次相同 grep 命令，无进展且持续消耗 token，直到用户手动中止。稳定性问题引发关注。

---

## 重要 PR 进展（10 条）

**1. fix(tui): reason-effort 变体作用于 agent**
[#46202](https://github.com/anomalyco/opencode/pull/46202) — 修复 TUI 将 reasoning-effort 变体按模型而非 agent 存储的问题，解决跨 profile 使用不同 effort 时被覆盖的缺陷，当前标记为 `needs:issue`。

**2. fix(webfetch): 超时覆盖响应体读取**
[#45235](https://github.com/anomalyco/opencode/pull/45235) — 修复服务器快速响应 headers 后 body 传输停滞导致的永久挂起，同时处理同一表达式中的两个次要缺陷。对应 #45229。

**3. fix(app): 保留 iOS PWA 状态栏空间**
[#46200](https://github.com/anomalyco/opencode/pull/46200) — 将 iOS 状态栏从 `black-translucent` 改为 `default`，避免 PWA 内容被刘海屏遮挡。关闭 #36142。

**4. feat: 可配置 plans 目录**
[#46199](https://github.com/anomalyco/opencode/pull/46199) — 允许自定义 `.opencode/plans/` 目录位置，并可选择跳过插件依赖安装，解决 plan 模式下项目目录被污染问题。关闭 #46189。

**5. feat: per-MCP-server 信任配置**
[#40125](https://github.com/anomalyco/opencode/pull/40125) — 支持为每个 MCP 服务器单独配置证书指纹固定（fingerprint pinning），替代全局禁用验证的方式。关闭 #40111，部分解决 #23506。

**6. docs(ecosystem): 添加 dejavu 插件**
[#44467](https://github.com/anomalyco/opencode/pull/44467) — 将跨会话错误门控插件 opencode-dejavu 收录到社区生态插件列表。

**7. fix(session): 溢出错误在放弃恢复而非尝试恢复时发布**
[#39571](https://github.com/anomalyco/opencode/pull/39571) — 修正 provider 返回 413/ContextOverflowError 且自动压缩开启时的错误发布路径。关闭 #39573。

**8. fix(provider): NVIDIA NIM GLM 模型注入 chat_template_kwargs**
[#39569](https://github.com/anomalyco/opencode/pull/39569) — NVIDIA NIM 的 GLM 模型不识别 `reasoningEffort` 参数，此 PR 自动生成并注入正确的 `chat_template_kwargs`。关闭 #39553。

**9. fix(tui): 上下文百分比按输入限制计算**
[#39558](https://github.com/anomalyco/opencode/pull/39558) — 修复 TUI 上下文条以 `context` 而非 `input` 为分母计算的 bug，避免 gpt-5.6-sol 等模型在 TUI 显示远未达到上限时过早触发压缩。关闭 #38851。

**10. feat(cli): 新增 console logout 命令**
[#39549](https://github.com/anomalyco/opencode/pull/39549) — V2 CLI 新增 `opencode console logout`，移除已存储的 OpenCode Console 凭据，保留 V1 风格的幂等反馈。

---

## 功能需求趋势

- **GUI/桌面端深度增强**：多条新 issue（#46153、#46151、#46152、#46154、#46156、#46157）集中请求在桌面 GUI 中提供 per-model 参数配置、插件数据面板、serve 监控模式、动态双行会话栏等，社区正推动 OpenCode 从纯 CLI 工具向完整 IDE 体验演进。
- **配额/用量计算透明化**：#38570、#41206、#46184、#46149 等多条 issue 报告配额百分比与实际用量不符，甚至出现超 100% 显示，用户对配额计算逻辑的信任度下降。
- **Agent 循环控制**：#43673、#43800、#46147 均描述 agent 重复执行相同工具调用、token 浪费的问题，社区希望引入循环检测/熔断机制。
- **远程 MCP 与安全配置**：#44790 指出 MCP OAuth `resource_metadata` URL 被忽略，#40125 请求 per-server 信任配置，远程 MCP 的标准化与安全配置成为关注点。
- **平台兼容性（Windows & iOS）**：#17372（PowerShell 5.1）、#36225（自定义标题栏）、#46200（iOS PWA 状态栏）反映桌面与移动端的平台适配需求仍在持续。

---

## 开发者关注点

- **Windows 生态高频问题**：PowerShell 版本错误、重复启动 MCP 进程导致多 GB 内存占用（#46174）、Windows Terminal 复制后 tab 标题消失（#44923）——Windows 桌面体验仍是反馈重灾区。
- **MCP 进程资源泄露**：`serve` 模式下 MCP 子进程随 Web 客户端重连不断累积直至 OOM（#46035），以及上下文压缩后 MCP 工具清单归零（#46190），资源管理与会话稳定性问题突出。
- **Agent 工具调用可靠性**：模型在生成 `<invoke>` 前反复输出冗长 preamble 进入死循环（#46147、#46197），开发者对 token 浪费十分敏感。
- **配额显示信任危机**：多项百分比超过 100%（#46184、#46149）或与用量历史不匹配（#41206），开发者希望尽快修正计算逻辑并补充说明。
- **文档与行为一致性**：#23566（LSP 默认状态描述误导）与 #4232（LM Studio 模型列表不精确）等老 issue 被持续讨论，社区对官方文档的准确性提出更高要求。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*