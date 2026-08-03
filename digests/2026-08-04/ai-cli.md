# AI CLI 工具社区动态日报 2026-08-04

> 生成时间: 2026-08-03 23:31 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告

**报告日期：2026-08-04** | 覆盖工具：Claude Code / OpenAI Codex / Gemini CLI / Copilot CLI / Kimi Code / OpenCode / Qwen Code

---

## 一、生态全景

当前 AI CLI 工具已全面走出"演示可用"阶段，竞争焦点从**模型调用能力**转向**工程化底座**：MCP 生态进入精细化治理期（认证、隐私、兼容性成为高频词），Agent 运行时可靠性（子代理状态误报、中断语义、权限链路）成为多工具共同痛点。Windows/WSL 混合环境不再是"边缘场景"而是被反复报告的**主流故障源**，桌面端作为 CLI 的自然延伸正在经历第一轮产品化打磨。与此同时，成本透明度（Prompt 缓存保持、模型上下文上限）与安全边界（工具执行护栏、可信运行时）开始成为开发者选择工具的**决策变量**，而不仅是锦上添花。

---

## 二、各工具活跃度对比

| 工具 | 热点 Issues（24h） | PR 更新（24h） | Release | 社区规模信号 |
|---|---|---|---|---|
| **Claude Code** | 10 个（最高 22 评论 / 14👍） | 2 个（均为文档） | 无 | 讨论热度集中于 MCP/OAuth，无功能性代码合并，处于**稳定期** |
| **OpenAI Codex** | 10 个（最高 30 评论 / 37👍） | 10+ 个（MCP/并发/元数据） | 2 个 alpha 补丁版 | PR 密集，MCP 基础设施与模型门控为方向，处于**快速迭代期** |
| **Gemini CLI** | 50 个更新（P1 级 Bug 发酵中） | 46 个 | 1 个 nightly | Issue/PR 双高，维护者对 subagent 行为做系统性收敛，处于**高强度打磨期** |
| **GitHub Copilot CLI** | 未提供数据 | 未提供数据 | 未提供数据 | 数据缺失，建议后续补充追踪 |
| **Kimi Code CLI** | 3 个更新 | 8 个（全部社区贡献） | 无 | 活跃度较低但外部贡献者驱动明显，处于**社区早期成长期** |
| **OpenCode** | 10 个（最高 👍118） | 10+ 个（另有 20+ 自动化重提旧 PR） | 无 | 高赞功能诉求与多个阻断性 Bug 并存，处于**功能扩张与体验修补并行期** |
| **Qwen Code** | 10 个（P1 桌面会话丢失） | 10 个（修复/性能/重构） | 2 个（含 v0.21.4 正式版） | 正式版桌面化落地 + 大量 P2 修复，处于**版本化推进期** |

> 注：Gemini 的 50 个 Issue 与 46 个 PR 为所有工具中最高；Claude Code 与 Kimi 的 PR 活跃度显著低于其他工具。

---

## 三、共同关注的功能方向

| 方向 | 涉及工具 | 具体诉求 |
|---|---|---|
| **MCP 生态可靠性** | Claude Code / Codex / Gemini / OpenCode / Qwen | 认证稳定性（OAuth DCR 重复注册、凭据孤立）、隐私（GMail 链接重写为追踪 URL）、连接恢复（无状态化后上下文丢失）、工具暴露面细粒度控制 |
| **Agent 状态与执行可靠性** | Gemini / OpenCode / Qwen | 子代理中断被误报为成功（Gemini #22323）、子代理权限请求静默挂起（OpenCode #13715）、中断后状态错乱（Qwen Ctrl+C / APIUserAbortError） |
| **Windows / WSL 环境适配** | Codex / Qwen / Kimi | OneDrive 路径导致流断开（Codex #35420）、WSL Git 检测误判（#35119）、Windows 挂起（Kimi #2582）、WSL MCP 路径映射（#29639） |
| **跨会话记忆与状态持久化** | Kimi / Claude Code / Qwen / Codex | 跨会话记忆系统（Kimi #1283）、`--resume` 会话文件污染（Claude Code #69013）、桌面会话静默删除（Qwen #8400）、线程元数据膨胀（Codex #21211） |
| **成本与上下文透明化** | Codex / Claude Code / Qwen | 模型规格上下文 vs 实际目录上限不符（Codex #31860）、5 小时限额消耗不透明（Claude Code #70045）、microcompaction 破坏 Prompt 缓存（Qwen #8452） |
| **认证与账户链路** | Claude Code / OpenCode / Codex | OAuth `state` 参数丢失导致登录循环、GitHub OAuth 空 email 写库失败、刷新令牌过期时静默失败 |
| **桌面端体验** | OpenCode / Qwen / Codex | 滚动抖动、长文本粘贴卡死、垂直标签页、远程控制入口缺失、Web Shell 桌面化 |

---

## 四、差异化定位分析

| 工具 | 核心定位 | 技术路线 | 目标用户 |
|---|---|---|---|
| **Claude Code** | **企业级 MCP 与权限治理** | 插件生态规范化（MessageDisplay/skipLfs 文档补齐）、细粒度权限（M365 按 plan 控制、Workflow 触发收紧）、稳定性优先（无频繁发布） | 企业开发者、已有 Anthropic 订阅的团队，重视合规与可控性 |
| **OpenAI Codex** | **模型能力驱动的 Rust 原生 CLI** | Rust 重写 + MultiAgent V2 + 模型能力门控（Luna/Sol 分级）、MCP 客户端一致性测试 | 前沿模型使用者、多 agent 编排场景，追求与 OpenAI 模型路线同步 |
| **Gemini CLI** | **Agent 运行时可靠性攻关** | 大量 PR 聚焦上下文损坏修复、子代理状态审计、MCP 安全加固；nightly 发布节奏验证修复 | Google 生态开发者、重度依赖 subagent 复杂任务编排的用户 |
| **GitHub Copilot CLI** | 数据缺失，暂无法有效评估 | — | — |
| **Kimi Code CLI** | **轻量、社区共建的 CLI** | 外部开发者提交 5 个稳定性修复 PR；核心诉求聚焦"记忆系统"与 Web UI 可用性 | 中文开发者、Moonshot 平台用户，偏好轻量工具链 |
| **OpenCode** | **开源 TUI 体验创新试验场** | 高度响应社区（👍118 的可点击链接）、深耕 TUI 交互（快捷键、标签页、滚动）、多提供商连接 | 开源爱好者、终端重度用户，重视可定制性与视觉体验 |
| **Qwen Code** | **桌面化落地 + 成本工程** | Web Shell 升级为正式桌面应用；聚焦 Prompt 缓存保持（低水位清理、延迟工具发现）；探索 Agent 安全边界（确定性工具执行） | 中国云生态用户、Alibaba 模型用户、长会话重成本敏感型团队 |

**总结而言**：
- **Claude Code 最"企业级"**——权限颗粒度与生态文档先行；
- **Codex 最"模型驱动"**——版本与模型能力绑定紧密；
- **Gemini 正处于"可靠性补课期"**——大量 PR 在修补 subagent 行为缺陷；
- **OpenCode 是"社区驱动的 TUI 先锋"**——高赞功能与 Bug 并列暴露其快速扩张中的质量挑战；
- **Qwen Code 最关注"成本与安全工程"**——缓存优化与运行时信任边界是其独特标签。

---

## 五、社区热度与成熟度

### 高活跃 — 快速迭代期
- **Gemini CLI**：50 个 Issue + 46 个 PR/日，P1 级 Bug 持续发酵且维护者高度介入（多个 workstream-rollup），呈现"发现问题→批量修复→回归验证"的密集循环。属于**成熟度中等、迭代速度最快**。
- **OpenAI Codex**：PR 内容丰富（MCP 基础设施、进程树管理、模型能力门控），伴随每日 alpha 版本发布。属于**工程投入大、社区预期高的成长期**。
- **OpenCode**：20+ PR 自动化重提说明项目活跃度依赖自动化流程；高赞功能（👍118）与阻断性 Bug 并存，属于**功能快速扩张、体验追赶期**。

### 中活跃 — 版本化推进
- **Qwen Code**：正式版本 + 多 P2 修复 + 性能重构，呈现有节奏的版本化管理，社区反馈真实使用场景中的问题（中断、缓存、桌面丢失），属于**从实验室走向生产的过渡期**。
- **Claude Code**：无 Release、PR 仅 2 个文档，但 Issues 讨论深度高（OAuth 循环 22 评论、MCP 隐私持续 2 个月未关）。属于**功能稳定、生态治理期**——社区在"用"而不是"试"。

### 低活跃 — 早期积累
- **Kimi Code CLI**：3 个 Issue / 8 个社区 PR，活跃度全部来自外部贡献者，核心需求（记忆系统）持续积累评论。属于**社区共建的早期成长期**。

### 数据缺失
- **GitHub Copilot CLI**：本次摘要未包含

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---

# Claude Code 社区动态日报

**日期：2026-08-04** | 数据来源：github.com/anthropics/claude-code

---

## 一、今日速览

过去 24 小时 Claude Code 无新版本发布，社区讨论热度集中于 **OAuth 登录循环**（#77966，22 条评论）与 **MCP 生态可靠性**问题（OAuth 重复注册、GMail 隐私追踪、Business Central 会话丢失）。此外，两个插件开发文档 PR 提交，分别补充了 `MessageDisplay` 流式语义与 `skipLfs` 市场源的说明。

---

## 二、版本发布

过去 24 小时无新版本发布。

---

## 三、社区热点 Issues（Top 10）

### 1. 🔴 OAuth 登录循环：`state` 参数在跳转后丢失
**#77966** | [链接](https://github.com/anthropics/claude-code/issues/77966) | 评论 22 | 👍 14

Claude 账号登录在 "sign in again to continue" 重定向后出现 OAuth 循环，`state` 参数被丢弃，导致无法完成认证。该问题影响 IntelliJ 平台 Linux 用户，是当前社区最热门的 Bug 话题。

### 2. 🟠 "Server is busy" 错误频发
**#52765** | [链接](https://github.com/anthropics/claude-code/issues/52765) | 评论 16 | 👍 2

Windows 平台 Claude Cowork Desktop 持续报 "Server is busy" 错误，虽已标记关闭，但仍积累了大量用户反馈，反映桌面端并发处理能力的不足。

### 3. 🟠 更新后拒绝启动：误报"另一实例正在运行"
**#41743** | [链接](https://github.com/anthropics/claude-code/issues/41743) | 评论 9 | 👍 4

应用更新后启动失败，提示另一实例在运行，但任务管理器中并无相关进程。该问题已关闭并标记 stale，但 9 条评论说明仍有一定影响面。

### 4. 🟡 功能请求：按计划启用 Microsoft 365 写入工具
**#81317** | [链接](https://github.com/anthropics/claude-code/issues/81317) | 评论 7 | 👍 2

用户希望管理员能按订阅计划（而非全局）控制 Microsoft 365 写入工具的启用，以更细粒度地管控权限。这是目前最活跃的功能讨论。

### 5. 🟡 隐私问题：GMail MCP 重写链接为 Google 追踪 URL
**#66010** | [链接](https://github.com/anthropics/claude-code/issues/66010) | 评论 5 | 👍 4

GMail MCP 工具在返回邮件时会将原始 URL 重写为带 Google 追踪参数的链接，引发隐私担忧。该问题已持续近两个月仍处于 Open 状态，社区关注度较高。

### 6. 🟡 MCP OAuth：每次认证重复注册 DCR，orphan 旧凭据
**#59460** | [链接](https://github.com/anthropics/claude-code/issues/59460) | 评论 5 | 👍 6

MCP OAuth 客户端每次执行 `authenticate` 都重新进行动态客户端注册，导致已签发的 `client_id` 和 `refresh_token` 被孤立。问题虽已关闭，但 6 个 👍 表明开发者在自托管 MCP 场景中确实遇到了凭据管理痛点。

### 7. 🟡 Workflow 工具触发条件过宽
**#64524** | [链接](https://github.com/anthropics/claude-code/issues/64524) | 评论 4 | 👍 5

只要用户消息中包含 "workflow" 一词就会触发 Workflow 工具，即使与多代理编排完全无关。这会导致不必要的昂贵多代理模式调用，社区期待更精准的触发条件。

### 8. 🟡 会话恢复污染对话文件
**#69013** | [链接](https://github.com/anthropics/claude-code/issues/69013) | 评论 4 | 👍 0

使用 `claude --continue` 或 `--resume` 恢复会话时，JSONL 会话文件被大量重复的 `mode` / `permission-mode` 系统消息污染，导致历史对话在 UI 中不可见。

### 9. 🟡 功能请求：VSCode 扩展输入框拼写检查
**#70049** | [链接](https://github.com/anthropics/claude-code/issues/70049) | 评论 3 | 👍 8

用户希望在 VSCode 扩展的聊天输入框中支持拼写检查，但该功能被上游 microsoft/vscode#214367 阻塞。8 个 👍 说明这是一项被广泛认可的小而美的体验改进。

### 10. 🟡 Microsoft Business Central MCP：无状态化后上下文丢失
**#81965** | [链接](https://github.com/anthropics/claude-code/issues/81965) | 评论 1 | 👍 0

自 2026-07-28 stateless spec 上线后，Business Central MCP 服务器所有工具调用均失败，报 `Internal_CompanyNotFound`——原先通过 header 传递的上下文（如公司标识）在每次请求中丢失。这是 stateless MCP 迁移后兼容性问题的一个典型样本。

---

## 四、重要 PR 进展

过去 24 小时仅有 **2 个 PR**，均为插件开发文档更新，无功能性代码合并。

### 1. 📝 docs(plugin-dev): 补充 MessageDisplay 流式语义说明
**#83374** | [链接](https://github.com/anthropics/claude-code/pull/83374) | 作者 @iCodeCraft

在 Hook Development skill 的触发描述、事件指南和速查表中补全 `MessageDisplay` 支持说明。该事件此前已实际存在但未被文档收录，属于文档与实现对齐的修正。

### 2. 📝 docs(plugin-dev): 记录 skipLfs 市场源配置
**#77977** | [链接](https://github.com/anthropics/claude-code/pull/77977) | 作者 @superdiaodiao

为插件市场的 `github` 和 `git` 源补充 `skipLfs` 配置项文档，并新增 GitHub shorthand 与 Git URL 跳过 LFS 下载的示例，方便在大型仓库场景中优化插件安装性能。

---

## 五、功能需求趋势

### 1. MCP 生态进入"精细化"阶段
社区不再满足于"能连"，转而关注 **认证可靠**（OAuth DCR 复用 #59460、OAuth fallback #69758）、**隐私**（GMail 链接追踪 #66010）和 **兼容性**（Business Central 无状态化 #81965）。MCP 已从"能用"迈向"好用、可信"。

### 2. IDE 集成体验持续被关注
- VSCode 聊天输入框拼写检查（#70049，8 👍）
- 带空格路径的文件链接可点击（#70070）
- 跨 IDE 的拼写、渲染、打开行为的细节优化成为高频诉求。

### 3. 权限管理与控制粒度
从 M365 写入工具按 plan 区分（#81317），到 Workflow 触发条件收紧（#64524），再到 API 错误 Hook（#70026）——开发者希望获得 **更细粒度的控制** 与 **更可预期的行为**。

### 4. 桌面端与多设备协同
固定 routine 运行到侧边栏（#70093）、跨设备共享内存/任务交接（#70072）、Desktop 端 ECONNRESET（#77733），反映出桌面端产品形态仍在成长期，用户对"桌面端 = CLI 的补充"期待正转化为具体功能需求。

---

## 六、开发者关注点

### 痛点 1：OAuth 与认证稳定性
- `state` 参数丢失导致登录循环（#77966，22 评论/14 👍）
- MCP OAuth 重复注册 orphaning 凭据（#59460）
- `claude --print` 在无交互会话时 401 回归（#69864）

### 痛点 2：模型行为与回归
- Opus 4.6 上下文保持能力回归（#70098）
- Workflow 误触发导致不必要的多代理调用（#64524）
- 长请求 ~60-95s 超时死亡螺旋（#70008）

### 痛点 3：会话与状态管理
- `--resume` 后对话历史被系统消息污染（#69013）
- git 子模块中的会话未出现在 resume 选择器（#70078）
- 无进程可见的 "another instance running" 误报（#41743）

### 痛点 4：成本与配额透明度
- 5 小时限额在几分钟内被大量消耗（#70045）
- 缺乏对 API 错误（5xx/429/529）的 Hook 事件通知（#70026）

---

> **一句话总结**：OAuth 认证与 MCP 服务可靠性是当前社区的绝对焦点；与此同时，插件文档的补齐表明生态正在快速走向规范化——基础连接已不再是问题，精细控制与可信度才是下一阶段的关键词。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-04

## 今日速览

昨日发布了两个 Rust 版本（0.147.0-alpha.6 与 0.147.0-alpha.1.2），均为补丁级迭代。社区讨论热度集中在三类问题：Windows/WSL 环境的连接与沙箱故障（#35420、#35119、#29639）、模型能力（如 GPT-5.6 Luna/Sol）在实际使用中与目录配置不符（#35097、#31860）、以及多语言用户对 RTL 支持的持续呼吁（#19504）。PR 方面，MCP 基础设施成为重点，多个 PR 围绕 MCP 配置解析、并发控制与一致性测试展开。

## 版本发布

### rust-v0.147.0-alpha.6
- 链接: https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.6
- 发布说明为标准的 "Release 0.147.0-alpha.6" 模板，未见新增特性说明，推测为面向内部验证的迭代版本。

### rust-v0.147.0-alpha.1.2
- 链接: https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.1.2
- 同样为标准模板发布，无额外通告内容。

> 注：昨日发布密度较低，社区并未出现针对这两个 Alpha 版本的集中反馈。

## 社区热点 Issues

### 1. OneDrive 工作区导致 Codex 流反复断开 🔥（30 评论）
- **#35420** | [链接](https://github.com/openai/codex/issues/35420)
- 当 Windows 工作区位于 OneDrive 备份目录且 OneDrive 降级运行时，Work/Codex 流会反复返回 `stream disconnected before completion`。已产生多个 request ID，问题可稳定复现。
- **关注理由**：评论数当日最高，直接阻断生产工作流，且与 OneDrive 深度耦合，修复路径可能涉及 Windows 文件系统监控层。

### 2. Windows 应用缺失“控制其他设备”入口 ⭐（26 评论 / 30 👍）
- **#28919** | [链接](https://github.com/openai/codex/issues/28919)
- Windows 版 Codex 应用的 Settings > Connections 中缺少 “Control other devices” 选项卡，导致用户无法发起远程控制。
- **关注理由**：30 个 👍 表明这是 Windows 用户的高频诉求，且与 Remote 功能的入口一致性有关。

### 3. GPT-5.6 Luna 被标记为 MultiAgent V1，V2 spawn_agent 拒绝调用（14 评论 / 37 👍）
- **#35097** | [链接](https://github.com/openai/codex/issues/35097)
- 模型目录将 `gpt-5.6-luna` 标记为 `MultiAgent V1`，而启用 `multi_agent_v2` 时 `spawn_agent` 会直接拒绝该模型。用户期望 Luna 能跟随 Sol 一起进入 V2 体系。
- **关注理由**：37 个 👍 为今日之最，反映开发者对新模型能力与 MultiAgent 版本矩阵不匹配的高度敏感。

### 4. GPT-5.6 Sol 上下文窗口被目录限制在 372K（14 评论 / 26 👍）
- **#31860** | [链接](https://github.com/openai/codex/issues/31860)
- 模型规格支持 1.05M 上下文，但 Codex App 的 model catalog 将 Sol 的上下文窗口定为 353.4K（有效值），差距显著。用户要求放开目录上限。
- **关注理由**：直接影响长上下文任务，属于“规格与实现不符”的典型问题，社区认可度高。

### 5. 阿拉伯语/希伯来语 RTL 支持缺失（24 评论 / 19 👍）
- **#19504** | [链接](https://github.com/openai/codex/issues/19504)
- 请求在 Codex 和 Chat 面板中完整支持 RTL 文本方向；目前阿拉伯语的对齐、标点和阅读方向均不正确。
- **关注理由**：属于本地化基础能力缺口，虽非功能性故障，但影响特定语言用户群体的日常使用。

### 6. 线程导航/加载性能：无界元数据 + 大历史记录（23 评论）
- **#21211** | [链接](https://github.com/openai/codex/issues/21211)
- 根因包括 `threads.title` 被写为完整首条用户消息，导致 SQLite 线程列表膨胀；本地诊断显示线程元数据无上限增长且历史记录 eager 加载过重。
- **关注理由**：长期性能问题，影响会话多、历史长的重度用户，关联原有 issue #21154。

### 7. WSL 仓库被误判为非 Git，报告 “Git is unavailable”（14 评论 / 13 👍）
- **#35119** | [链接](https://github.com/openai/codex/issues/35119)
- 更新至 26.721.3404 / app-server 0.146.0-alpha.3 后，WSL ext4 文件系统中的有效 Git 仓库被标记为非 Git。
- **关注理由**：回归性缺陷，直接影响 WSL+Git 用户的日常操作，且涉及 app-server 层逻辑。

### 8. WSL 工作区中 Browser Use Node REPL 失败（14 评论）
- **#29639** | [链接](https://github.com/openai/codex/issues/29639)
- Desktop app 自动生成的 `node_repl` MCP server 使用 Windows 可执行文件，却收到 Linux/WSL 的 `sandboxCwd`，导致浏览器类工具全部不可用。
- **关注理由**：Windows + WSL 混合环境的典型路径映射问题，具有一定代表性。

### 9. Ubuntu 24.04 上 Bubblewrap 沙箱失败（13 评论）
- **#29908** | [链接](https://github.com/openai/codex/issues/29908)
- `apply_patch` 与普通受管沙箱命令均因 Bubblewrap loopback/USerns 报错而无法执行，与仓库权限无关。环境为 kernel 6.17 + Bubblewrap 0.9.0。
- **关注理由**：Linux 沙箱兼容性问题，可能阻塞 Ubuntu 24.04 用户的 patch 与工具调用。

### 10. Codex Cloud 自动代码审查静默失败 + 配额状态显示不符（11 评论）
- **#15477** | [链接](https://github.com/openai/codex/issues/15477)
- GitHub 自动代码审查：刷新令牌过期时静默失败，且 dashboard 显示额度充足但实际报 “limit reached”。
- **关注理由**：“静默失败 + 状态不一致”的组合会严重消耗信任，属于后台自动化场景的典型体验陷阱。

## 重要 PR 进展

### 1. 新增 MCP 客户端一致性回归门
- **#36810** | [链接](https://github.com/openai/codex/pull/36810)
- 新增测试工具链，在官方 MCP client conformance suite 上跨越 HTTP/stdio 传输、OAuth 场景及多个协议版本对 Codex 可执行文件进行回归验证，并覆盖 App 应用服务器路径。

### 2. `exec resume --last` 优先使用状态数据库
- **#36809** | [链接](https://github.com/openai/codex/pull/36809)
- 成功执行 `codex exec resume --last` 时不再审计全部 rollout 文件，而是优先查询状态数据库并将首个可用匹配视为权威结果，同时校验其属于有效的 active/archived 集合。

### 3. 避免命令审批后重复注入权限说明
- **#36800** | [链接](https://github.com/openai/codex/pull/36800)
- 将已批准的命令前缀与稳定权限指令分开追踪，policy 修订后仅输出新增前缀，不再追加完整权限块，可减少 token 消耗并降低上下文噪音。

### 4. 新增 Agent Plugins MCP 配置解析
- **#36796** | [链接](https://github.com/openai/codex/pull/36796)
- 增加 `parse_agent_plugin_mcp_config`，可将 Agent Plugins v1 的 `mcp.json` 翻译为 Codex MCP server 配置，兼容 stdio/streamable HTTP、`PLUGIN_ROOT`/`PLUGIN_DATA` 展开和嵌套插件。

### 5. 终止超时 Git 进程树
- **#36793** | [链接](https://github.com/openai/codex/pull/36793)
- Git 元数据命令在 Unix 使用独立进程组、在 Windows 使用 Job Object，确保命令包装器退出后不会残留 helper 进程。

### 6. 按模型能力门控插件使用说明
- **#36792** | [链接](https://github.com/openai/codex/pull/36792)
- 在模型元数据中新增 `include_plugin_usage_instructions`（默认 false），仅当所选模型支持时输出通用插件指引；交互式模型预置将启用该能力。

### 7. 新增按 MCP 工具暴露面控制
- **#36781** | [链接](https://github.com/openai/codex/pull/36781)
- MCP servers 可通过 `omit_tools_from` 选择工具是否出现在直接暴露、工具搜索或 Code Mode 调用中，而无需全局禁用工具。

### 8. 提高 Codex Apps 目录上限至 8,192
- **#36772** | [链接](https://github.com/openai/codex/pull/36772)
- 主机拥有的 `codex_apps` 注册允许最多 8,192 个目录项，标准 MCP 的 2,048 限制仍对第三方 server 生效，避免大型工具目录被截断。

### 9. 加固 Linux 受管代理辅助进程生命周期
- **#36771** | [链接](https://github.com/openai/codex/pull/36771)
- 修复受管代理辅助进程在沙箱命令退出后仍持有标准流、继承已关闭描述符导致就绪失败、以及 zombie owner 残留陈旧 socket 目录的问题。

### 10. 整合 `ModelMessages` 中的模型指令
- **#36787** | [链接](https://github.com/openai/codex/pull/36787)
- 移除 `ModelInfo.base_instructions` 作为内存指令源，统一使用 `model_messages.instructions_template`，并兼容 bundled、remote、fallback 与 override 元数据。

> 另外值得留意的是：**#36807** 将音频准备逻辑抽取为独立工具 crate（`codex-utils-audio`），为后续音频输入能力扩展铺路；**#36797** 对 `rusty_v8` 校验和清单统一 LF 行尾，避免 Windows 构建的 CRLF 兼容问题。

## 功能需求趋势

从本次 50 条 Issue 样本中，社区呼声最高的功能方向如下：

- **模型与 MultiAgent 兼容矩阵**：多起 issue（#35097、#34700、#34027）指向模型（Luna/Sol）与 MultiAgent V1/V2 或账号等级的兼容性混乱。开发者期望模型能力标记、目录信息与实际行为保持一致。
- **Windows + WSL 深度集成**：超过 6 条 Issue 涉及 Windows/WSL 混合场景（#35119、#29639、#30529、#34652 等），包括 Git 检测、路径映射、clipboard 图片传递和远程审批按钮。说明 WSL 已成为 Windows 用户的默认开发环境，而 Codex 的适配仍存在明显断层。
- **上下文窗口透明化**：#31860 并非孤例，用户对“模型规格 vs 实际上下文上限”的差异越来越敏感，要求 Codex 提供更透明的模型能力面板和移除不必要的目录限制。
- **本地化与可访问性（RTL）**：#19504 是社区持续推动的本地化项目，涉及文本方向、对齐与标点处理，属于全球化产品的必填项。
- **代理/自动化运维能力**：来自 #29922 的 `monitor` 工具请求（后台事件驱动唤醒）、#30418 的多账号 Gmail 连接器，代表用户希望 Codex 从“对话式”走向“事件驱动 + 多服务编排”。
- **多账号与用量归属分析**：#30418 和 #28985 表明，随着 Codex 覆盖 Web/CLI/App 多端，用户开始要求按客户端、会话维度进行用量归属与追踪，并支持同时接入多个外部账号（Gmail 等）。

## 开发者关注点

-

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-04

## 今日速览
过去 24 小时社区高活跃：共 1 个 nightly 版本发布、50 个 Issue 更新、46 个 PR 推进。核心关键词是 **“Agent 可靠性”**：P1 级 Bug 持续发酵（Generalist agent 挂起、Shell 命令卡死、Subagent 状态误报成功），同时大量 PR 集中在上下文损坏修复、模型配额回退、MCP 安全加固与依赖升级。官方维护者多个 workstream-rollup 仍处于 bot-triaged / need-retesting 状态，显示内部正在对 subagent 行为做系统性收敛。

## 版本发布
- **[v0.55.0-nightly.20260803.gf47d6c6f7](https://github.com/google-gemini/gemini-cli/releases/tag/v0.55.0-nightly.20260803.gf47d6c6f7)** — 过去 24 小时发布。当前仅提供对比上一个 nightly 的 [Full Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.55.0-nightly.20260802.gf47d6c6f7...v0.55.0-nightly.20260803.gf47d6c6f7)，无显著变更摘要。

## 社区热点 Issues（10 个）
1. **[#22323 Subagent recovery after MAX_TURNS is reported as GOAL success, hiding interruption](https://github.com/google-gemini/gemini-cli/issues/22323)** — P1，12 条评论。`codebase_investigator` 子代理因达到 MAX_TURNS 中断，却被上报为 `status: success`。错误状态掩盖真实原因，直接影响 Agent 上层决策；已进入 need-retesting。
2. **[#21409 Generalist agent

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-08-04）

## 今日速览
过去 24 小时无新版本发布。社区活跃度集中在稳定性修复：外部开发者 @ayaangazali 一人提交 5 个修复 PR，覆盖控制台编码崩溃、钩子任务被回收、Shell 进程挂起等问题。跨会话记忆系统功能请求（#1283）持续获得讨论，仍是社区关注度最高的功能方向。

## 社区热点 Issues
过去 24 小时共更新 3 个 Issue，均未关闭：

1. **[#1283] 功能请求：记忆系统——跨会话持久上下文**  
作者：@CatKang | 创建于 2026-02-27 | 更新于 2026-08-03 | 评论：15  
探讨为 Kimi Code CLI 实现自动 + 手动记忆机制，使项目模式与用户偏好跨会话持久化。虽然是老 Issue，但评论数持续增长，说明社区对该功能诉求强烈且讨论深入。  
https://github.com/MoonshotAI/kimi-cli/issues/1283

2. **[#2573] Bug：Web UI 切换会话时无限 "Connecting to session..." 加载**  
作者：@belenov-maker | 更新于 2026-08-03 | 评论：1  
kimi-cli 1.48.0 Web 技术预览版在 Chrome 150 下，切换会话时界面出现无限加载，严重影响 Web UI 的可用性。  
https://github.com/MoonshotAI/kimi-cli/issues/2573

3. **[#2582] Bug：CLI 流式生成期间无限挂起，会话不可用**  
作者：@bobtu56 | 更新于 2026-08-03 | 评论：0  
kimi-cli 0.31.1 + Moonshot Platform API + kimi-k2.7-code 模型，在 Windows x64 上稳定复现生成挂起，属于阻断性可用性问题，开发者反馈暂无临时绕过手段。  
https://github.com/MoonshotAI/kimi-cli/issues/2582

## 重要 PR 进展
过去 24 小时共更新 8 个 PR，全部由社区贡献者提交：

1. **[

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-04

## 今日速览

今日社区焦点集中在 **TUI/桌面端交互体验** 与 **连接稳定性** 两大方向：高赞功能请求 "可点击链接" (#1168, 👍118) 持续活跃，多个关于死连接无错误挂起、子代理权限静默卡死的 bug 报告引发共鸣。代码方面，有 20+ 个 PR 今日被更新（多数为 automated cleanup 重提的旧 PR），其中新提交的 PR 包括重新设计的 workspace 流程、可配置的权限模式快捷键、桌面端 localhost 浏览器预览等。

## 版本发布

过去 24 小时无新版本 Release。

## 社区热点 Issues

**1. 子代理权限请求静默挂起，会话永久卡死**
[#13715](https://github.com/anomalyco/opencode/issues/13715) — 当子代理再生成子代理并请求权限（如 bash）时，权限提示永远不会渲染在 TUI 中，会话无限期挂起等待。`children()` memo 实现被指为问题根源，属于深度使用场景下的严重阻断性问题。

**2. 可点击链接请求持续火爆**
[#1168](https://github.com/anomalyco/opencode/issues/1168) — 获得 118 个 👍 的长期功能请求：希望 URL 支持 Ctrl+左键点击在默认浏览器打开。这是终端和编辑器类应用的标准能力，社区需求强烈但迟迟未实现。

**3. /tmp 目录泄漏数百 GB 临时 .so 文件**
[#28089](https://github.com/anomalyco/opencode/issues/28089) — OpenCode 在 /tmp 下生成的临时 ELF 共享对象文件得不到清理，长期运行可消耗数百 GB 磁盘空间。对服务器环境用户影响严重，需要尽快修复。

**4. 死连接导致 `opencode run` 无输出且永不退出**
[#40330](https://github.com/anomalyco/opencode/issues/40330) — 当 provider 的 baseURL 端口拒绝 TCP 连接（如本地 llama.cpp 未启动）时，非交互模式下不输出任何错误信息，重试无限期进行。同症状的还有 [#40319](https://github.com/anomalyco/opencode/issues/40319)（60 秒无报错重试），说明连接错误处理是当前一大短板。

**5. DeepSeek V4 Flash 长输出被 Q 字符污染**
[#40321](https://github.com/anomalyco/opencode/issues/40321) — 长工具调用生成场景下，模型响应出现大量重复 Q 字符和乱码，输出完全不可读。疑似与模型端或流式解析的问题有关，影响使用免费模型的用户。

**6. 新 UI 强制水平标签，垂直标签页呼声再起**
[#36942](https://github.com/anomalyco/opencode/issues/36942) — 新 UI 只支持水平标签，难以同时查看超过 5 个会话标题。垂直标签页请求获得 16 个 👍，代表了一批重度多会话用户的心声。

**7. Go 服务 SSE 事件流不完整，破坏 Codex 客户端兼容**
[#40171](https://github.com/anomalyco/opencode/issues/40171) — `/v1/responses` 接口的流式响应缺少 `response.output_item.added` 和 `response.content_part.added` 事件，导致基于 OpenAI Responses API 规范的客户端无法正常工作。

**8. GitHub OAuth 登录失败：email 参数为空**
[#39207](https://github.com/anomalyco/opencode/issues/39207) — 通过 GitHub 登录 opencode.ai 时，OAuth 回调写库 email 为空，导致 SQL 更新失败。账户体系的基础功能故障，直接影响新用户注册转化。

**9. 桌面端应用滚动体验问题集中爆发**
[#20600](https://github.com/anomalyco/opencode/issues/20600) + [#17996](https://github.com/anomalyco/opencode/issues/17996) + [#29094](https://github.com/anomalyco/opencode/issues/29094) — 多个独立的滚动 bug 被报告：随机跳到对话中间、快速上滑时跳过整页内容、LLM 回复期间阅读历史会被吸回底部。桌面端聊天体验的稳定性亟待加强。

**10. Zen 注册流程在 Google/GitHub 认证成功后失败**
[#39414](https://github.com/anomalyco/opencode/issues/39414) — 两个认证提供商均成功完成跳转，但回到 OpenCode 后提示 "Invalid email" 并显示空白页。与 #39207 同为认证链路故障，影响 Zen 付费用户转化。

## 重要 PR 进展

**1. 新布局添加 workspace 选择流程**
[#38790](https://github.com/anomalyco/opencode/pull/38790) — 为会话新建流程增加 Local/New/Existing workspace 选择：支持持久化校验草稿、按项目记忆默认选项，并采用设计稿更新的菜单文案、长列表搜索等交互细节。

**2. 权限模式快捷键可配置**
[#40334](https://github.com/anomalyco/opencode/pull/40334) — TUI 中切换自动审批权限模式的快捷键目前无法自定义，此 PR 将其变为可配置项（Closes #40331）。

**3. 桌面端新增 localhost 浏览器预览**
[#40337](https://github.com/anomalyco/opencode/pull/40337) — 在桌面应用中直接以面板形式预览当前会话的开发服务器，无需切换窗口即可查看和交互，不过标注 `[needs:compliance]` 待合规审核。

**4. 为所有代理应用安全默认值**
[#40316](https://github.com/anomalyco/opencode/pull/40316) — 将共享的外部目录和 `.env` 读取策略下沉为通用代理默认值，同时放行受管工具的输出、临时及全局配置目录，内置和自定义代理统一生效。

**5. 细化 diff 查看器**
[#40285](https://github.com/anomalyco/opencode/pull/40285) — 更新 oc-2 的红/绿令牌样式，左侧栏宽收窄至 2px 并移除红条虚线纹理，行号列布局焕新，属于 UI 打磨型改动。

**6. 修复 Azure 上 gpt-5.5+ 的 reasoningEffort 报错**
[#40265](https://github.com/anomalyco/opencode/pull/40265) — Azure 合流下 gpt-5.5 与 `reasoningEffort` 参数冲突，此修复沿用之前 `useCompletionUrls` 的处理方式解决（Closes #40257）。

**7. Zen API 请求体积限制为 10MB**
[#35237](https://github.com/anomalyco/opencode/pull/35237) — 为 Zen API 增加请求体大小硬限制，`readJsonBody` 在读取前校验 content-length 并在流式消费中计数，防止超大上下文拖垮控制台资源。

**8. 子代理命令支持后台运行**
[#35233](https://github.com/anomalyco/opencode/pull/35233) — 将 `subagent` 加入 V2 命令配置（保留 `subtask` 别名），子代理命令作为子会话立即后台运行，并向父会话注入状态/完成通知，`/review` 标记为子代理命令。

**9. 桌面端深链接适配新布局**
[#35223](https://github.com/anomalyco/opencode/pull/35223) — 修复 `opencode://open-project` 和 `opencode://new-session` 深链接在重新设计的桌面布局中失效的问题（Closes #35225）。

**10. MCP 资源订阅 API 与插件 Skills API**
[#35197](https://github.com/anomalyco/opencode/pull/35197) + [#35196](https://github.com/anomalyco/opencode/pull/35196) — 两个由 `@sjawhar` 提交的能力补齐 PR：前者实现 MCP 资源订阅及自动提示（partial #28567），后者通过 `PluginInput.skills` 向插件暴露 Skills API（Closes #18688），均为 rebase 后的重新提交。

## 功能需求趋势

- **TUI/桌面端交互体验优化**：最集中的方向。包括可点击链接（#1168, 👍118）、垂直标签页（#36942）、毫秒级时间戳（#35348）、滚动稳定性（#20600/#17996/#29094）、粘贴长文本卡死（#38932）。
- **配置系统的灵活性与可编程性**：`{cmd:}` 凭证占位符（#12710）、任意文件附加为工具上下文（#40341）、桌面版 MCP/skill GUI（#31399/#40335）、按模型限制覆盖（#35198）。
- **连接与错误处理的可观测性**：死连接无报错挂起（#40330/#40319）、重试策略透明度、非 SSE 协议的 chunkTimeout 支持（#26487）。
- **模型/提供商兼容性**：Azure 推理参数修复（#40265）、DeepSeek V4 Flash 输出损坏（#40321）、OpenAI Responses API SSE 事件完整性（#40171）。
- **认证与账户体系建设**：GitHub OAuth 空 email（#39207）、Zen 注册失败（#39414）、邀请链接失效（#40295）。

## 开发者关注点

1. **连接失败的静默失败不可接受**：无论是 TCP 拒绝还是 baseURL 不可达，期待快速失败 + 明确错误，而不是无限重试或空输出（#40330、#40319）。
2. **权限请求在子代理链中丢失**：静默挂起导致会话无法恢复，需要 TUI 层完整的 ask 事件链路（#13715 及修复 PR #35199）。
3. **桌面端聊天体验是重灾区**：滚动跳动、长文本粘贴卡死等问题高频出现，多个 PR 正在改写布局，用户期待基础体验的稳定优先于新功能。
4. **临时文件泄漏的系统性清理**：/tmp 泄漏 .so 文件在长期运行后造成磁盘灾难，开发者希望建立临时目录的自动回收机制。
5. **认证与邀请流程影响商业化转化**：OAuth 空 email、Zen 注册失败、邀请链接失效等多个账户链路问题被报告，社区反馈积极（有 👍、有截图），团队需优先排查。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-08-04）

## 今日速览

昨日（2026-08-03）Qwen Code 动态密集：官方发布 **v0.21.4**，Web Shell 正式升级为 release-ready 桌面应用；与此同时，社区提交的 Issue 与 PR 数量均处于高位，核心关注点集中在 **Agent 运行时可信边界、会话/中断语义正确性、Prompt 缓存保持、以及 Web Shell/桌面端体验** 等方向。此外，多起 P1/P2 级 Bug 被报告，涉及桌面端会话静默丢失与 ACP 会话恢复等问题。

## 版本发布

### v0.21.4（正式版）
- **Web Shell 正式成为 release-ready 的桌面应用**：引入完整原生生命周期管理、单实例行为、自动更新支持。([#8132](https://github.com/QwenLM/qwen-code/pull/8132))
- **Web Shell 历史记录分页增强**：对于超大 turn 的处理更加优雅，避免极端数据导致的渲染问题。
- 关联 PR：Web Shell 相关改动 [#8132](https://github.com/QwenLM/qwen-code/pull/8132)

### v0.21.3-nightly.20260803
- `docs`: 完善 TUI 键盘快捷键参考文档（by @DragonnZhang）。([#8327](https://github.com/QwenLM/qwen-code/pull/8327))
- `fix(core)`: 修复历史分页在特定超长输出下被阻塞的问题。

## 社区热点 Issues（Top 10）

1. **[P2] Desktop 0.0.5 / Windows: 应用重启后会话静默自动删除（ACP session/load 失败，workspace cwd 不匹配）**
   作者报告 Desktop 版在重启后 UI 中所有会话消失，应用因 provider loader 返回 0 条消息而自动删除本地会话镜像，且无任何确认。涉及数据安全，社区讨论度高，是当前最严重的桌面端事件之一。([#8400](https://github.com/QwenLM/qwen-code/issues/8400))

2. **[P3/feature-request] 为可信任的 Agent Runtime 提出确定性工具执行边界**
   该提案建议将 LLM 置于信任边界之外，使运行时能确定性约束、授权、观察和评估模型动作。已获 13 条评论，为 Agent 安全方向铺路，社区关注度最高。([#8102](https://github.com/QwenLM/qwen-code/issues/8102))

3. **[P2] 使用 Alibaba token plan 时模型名过长导致 UI 截断**
   通过移动端 Paseo 调用时，模型列表中的前缀 `[ModelStudio token plan]` 过长，模型全名显示不全。影响移动端用户体验，社区有 5 条评论。([#8470](https://github.com/QwenLM/qwen-code/issues/8470))

4. **[P2] Duplicate provider tool call id**
   用户在调用工具时频繁遇到 `"Duplicate provider tool call id"` 及 `"not recorded"` 错误，导致后续环境操作失败。已获得维护者确认，需要进一步排查 provider 侧与客户端侧的 ID 分配逻辑。([#8382](https://github.com/QwenLM/qwen-code/issues/8382))

5. **[P2] Size-triggered microcompaction 反复导致 prompt cache 失效**
   PR #5111 引入的阈值触发机制在连续 ToolResult 轮次中，可能反复重写已缓存的会话前缀。对长会话性能和成本影响较大，社区 3 条评论持续关注。([#8452](https://github.com/QwenLM/qwen-code/issues/8452))

6. **[P2] SDK-Embedded MCP Server 工具在恢复会话后续查询中全部失败**
   首次查询正常、恢复会话后直接调用 MCP 工具失败，影响 SDK 集成场景，已获 3 条评论。([#8433](https://github.com/QwenLM/qwen-code/issues/8433))

7. **[P2] `isAbortError` 无法识别 OpenAI SDK 的 `APIUserAbortError`**
   `auth_type=openai` 路径下用户取消请求不能被正确归类为 abort，导致后续流程状态错乱。([#8398](https://github.com/QwenLM/qwen-code/issues/8398))

8. **[P2] 新的 Agent thinking 展示效果抖动严重，难以阅读**
   动态 thinking 区域高度变化导致整个面板上下跳动，连非 thinking 内容也受到影响，社区 3 条评论吐槽交互体验。([#8319](https://github.com/QwenLM/qwen-code/issues/8319))

9. **[P3] 取消 Prompt（Ctrl+C）后内容未恢复到输入框**
   用户输入较长 prompt 取消后内容丢失，需重新输入。此前 Ctrl+C 可恢复，现回归，已获 7 条评论。([#8316](https://github.com/QwenLM/qwen-code/issues/8316))

10. **[P3] 桌面客户端 @ 引用搜索不到项目中的文件**
   用户项目中存在 `KuaiShouOrderService.java` 但 @ 引用搜索不到，影响 IDE 使用体验。社区 5 条评论响应。([#8123](https://github.com/QwenLM/qwen-code/issues/8123))

## 重要 PR 进展（Top 10）

1. **[fix(core)] 一个从未送达的 MCP 调用应视为首次投递，而非重放**
   修复 #8387 引入的回归：当 MCP 服务器已知断开时，客户端错误地触发重放保护，测试在 main 分支持续失败。现做确定性修复。([#8482](https://github.com/QwenLM/qwen-code/pull/8482))

2. **[feat(acp)] 针对重复工具执行失败增加保护机制**
   基于 #8176 / #8180 冻结的执行结果合约，增加 prompt 内保守的保护逻辑，统计带解析 tool_call 的终端失败。([#8469](https://github.com/QwenLM/qwen-code/pull/8469))

3. **[fix(core)] 在延迟工具发现期间保持 prompt 缓存稳定**
   通过 `tool_search` 在模型可见结果中提供匹配 schema，并用稳定的 `deferred_tool_call` 桥接后续调用，避免主会话 provider 工具声明和系统指令频繁变化。([#8276](https://github.com/QwenLM/qwen-code/pull/8276))

4. **[feat(cli)] 为附件添加音频桥接**
   当主模型不支持音频时（如文本模型），用户 `@` 附件或 ACP 音频 prompt 将自动通过配置的批量语音模型转写，并以不可信机器转写标记替换。([#8332](https://github.com/QwenLM/qwen-code/pull/8332))

5. **[fix(core)] 加固 Qwen 3.8 Reasoning Effort 线上结构（wire shape）**
   针对 #8472 合并后的 review 发现，处理 `enable_thinking`/`thinking_budget` 与 `reasoning_effort` 冲突等问题。([#8488](https://github.com/QwenLM/qwen-code/pull/8488))

6. **[perf(core)] 清理工具结果至低水位，保护 prompt 缓存**
   当可压缩工具结果累计超过阈值时，客户端现在会清理最旧的结果至阈值一半的低水位（而非刚低于阈值即停），同时保留 `-1` 停用支持。([#8464](https://github.com/QwenLM/qwen-code/pull/8464))

7. **[perf(review)] 将独立 setup 调用合并到一次响应中**
   实测一个小 PR 的高投入 review 中，从 `parse-args` 到首个 agent 启动耗时 7 分钟。该 PR 将顺序模型调用（fetch-pr、pr-context、comment-status、规则加载）合并为单次响应，显著缩短评审关键路径。([#8487](https://github.com/QwenLM/qwen-code/pull/8487))

8. **[refactor(core)] 将 review skill 的事故叙述迁移至 DESIGN.md**
   将 `SKILL.md` 中的 incident narratives（冗长的失败案例说明）移至 `DESIGN.md`，减少每次评审约 60 轮上下文重复计费，节省 token 开销。([#8489](https://github.com/QwenLM/qwen-code/pull/8489))

9. **[feat(review)] 构建/测试范围支持 Maven 多模块**
   为 Maven 多模块 monorepo 同 npm workspace 一样，将变更文件映射到对应模块构建与测试，并在构建测试前加载 CLAUDE.md 规则。([#8416](https://github.com/QwenLM/qwen-code/pull/8416))

10. **[feat(review)] 当 bundle 版本落后于 review 代码时明确提示**
   Review 运行前检查构建 stamp 是否与当前工作树源码匹配，若不匹配则直接提示，避免因 bundle 陈旧导致的假阳性/假阴性。([#8390](https://github.com/QwenLM/qwen-code/pull/8390))

## 功能需求趋势

从近 24-48 小时活跃的 Issues/PR 中可提炼以下社区关注的功能方向：

1. **Agent 运行时安全与可信边界**：`#8102 确定性工具执行边界` 提案讨论度最高，目标是将 LLM 置于信任边界之外，配合 `#8125 外部工具守护 provider` 等项目，预示未来将在护栏、审计、授权上持续发力。
2. **多渠道接入与自动化**：`#8281 请求新增 Email channel（IMAP/SMTP）`、`#8389 计划与审查（Plan & Review）工作流` 均显示用户希望 Qwen Code 更深入地融入日常开发流与背景自动化。
3. **Prompt 缓存与成本控制**：`#8452 microcompaction 破坏 cache`、`#8276 延迟工具发现时保持缓存稳定`、`#8464 低水位清理` 表明大型会话的 token 成本与缓存命中率已成为高频关注点。
4. **Web Shell / 桌面应用体验**：`#8132 Web Shell 桌面化` 是当前官方重点；`#8494 Web-shell artifact 操作定位错误`、`#8389 工作流可视化` 等说明 Web Shell 生态正在快速迭代。
5. **多模态与移动端适配**：`#8332 音频桥接`、`#8470 移动端模型名截断` 显示用户正尝试在手机/Paseo 等终端上使用更丰富的输入类型。
6. **模型支持广度与兼容性**：`#8432 Bailian Token Plan 模型列表同步`、`#8488 Qwen 3.8 reasoning effort wire shape` 说明新模型接入与兼容性问题始终伴随发布周期。

## 开发者关注点

- **中断与取消语义不完善**：多个 Issue 反映中断（Ctrl+C / APIUserAbortError）后状态错乱——输入框不恢复内容（#8316）、后续 turn 不写入 transcript（#8356）、控制调度器被意外终止（#8398）、取消的工具仍可能修改文件（#8493）。中断路径的正确性修复呼声最高。
- **会话数据安全**：`#8400 桌面会话静默删除` 这类数据丢失问题被列为 P1，凸显用户对本地会话数据持久化的高度敏感。
- **终端兼容性仍具碎片化**：Windows 下 ConEmu/Cmder 闪烁（#8385）、Warp 下 Ctrl+Tab 快捷键冲突（#8330）、VS Code 终端复制失效（#8317）等多款终端出现兼容性问题。
- **工具调用可靠性**：`Duplicate provider tool call id`（#8382）与 `MCP 工具在恢复会话后失败`（#8433）说明工具编排层在多轮、并发场景下仍需加固。
- **渲染与交互体验**：Agent thinking 展示抖动（#8319）、模型名过长截断（#8470）等 UI 细节虽优先级不高，但直接影响日常使用好感度。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*