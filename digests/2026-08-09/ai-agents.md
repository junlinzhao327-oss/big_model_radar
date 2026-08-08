# OpenClaw 生态日报 2026-08-09

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-08 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-09

## 1. 今日速览

OpenClaw 项目过去 24 小时活跃度极高：共更新 Issues 500 条（新开/活跃 456，关闭 44），PR 500 条（待合并 349，已合并/关闭 151），并发布了 v2026.6.33 和 v2026.6.34 两个安全加固版本。社区讨论热度集中在 DeepSeek v4 Flash 静默失败（164 条评论）、子代理结果静默丢失、网关内存泄漏（P0）等稳定性议题。修复侧，clawsweeper 机器人自动修复 PR 与维护者手动修复同步推进，关闭了 `stopReason` 轨迹缺失、凭据泄露、macOS LaunchAgent 停机等 5 个可见 PR。整体上项目处于高速迭代期，但多个 P0 级稳定性问题（内存泄漏、升级后网关无法启动）仍悬而未决，是当前最大的健康度隐患。

---

## 2. 版本发布

过去 24 小时发布了 2 个版本，均为 6.x 维护分支的安全加固版。重点方向一致：**收紧网络与凭据边界**，未包含破坏性变更。

### v2026.6.34
- **发布要点**：更安全的浏览器和网络边界：
  - 沙箱化浏览器路由
  - 受信任 DNS 目标
  - 自定义浏览器来源
  - 环回（loopback）提供方端点现在会拒绝不安全访问路径
- **涉及 PR**：#97958、#38290、#103075、#110693
- **致谢贡献者**：@eleqtrizit、@brunowowk、@mosidevv、@pgondhi987
- **迁移注意**：若使用了自定义浏览器来源或环回提供方端点，需确认访问路径符合新的安全校验规则。
- 🔗 https://github.com/openclaw/openclaw/releases

### v2026.6.33
- **发布要点**：更安全的网络和 secret 边界：
  - 提供方流、Discord REST 响应、浏览器抓取、OAuth 路径和日志现在会限制恶意响应大小
  - Telegram 凭据不再出现在诊断信息中
- **涉及 PR**：#96989、#95412、#99428
- **致谢贡献者**：@wangmiao0668000666、@Alix-007
- **迁移注意**：诊断日志中 Telegram 凭据相关字段将被移除，依赖日志排查问题的用户需注意新的脱敏格式。
- 🔗 https://github.com/openclaw/openclaw/releases

---

## 3. 项目进展

今日共合并/关闭 151 个 PR，重点推进了以下 5 个方向：

**稳定性修复**

| PR | 内容 | 关联 Issue |
|---|---|---|
| [#118685](https://github.com/openclaw/openclaw/pull/118685) | 在完成轨迹中记录标准化 assistant `stopReason`，使 token 截断不再伪装成正常完成，并可防止先前尝试的产物被误并入 | #118673 |
| [#120729](https://github.com/openclaw/openclaw/pull/120729) | 修复长嵌入式 Responses 会话中压缩后的两个失败：`function_call_output` 在压缩后被丢弃，以及压缩 checkpoint 被拒绝时的处理 | #120457 |

**基础设施与架构清理**

- [#120726](https://github.com/openclaw/openclaw/pull/120726) — 将 `node-pairing` 门面折叠进统一的 `device-pairing`，消除 JSON→SQLite 迁移后遗留的双词汇表，涉及 20+ 调用点。
- [#120720](https://github.com/openclaw/openclaw/pull/120720) — 修复 Memory Host 会话文件测试套件在 Windows 上的可靠性问题。

**安全修复**

- [#120728](https://github.com/openclaw/openclaw/pull/120728) — 修复助手在帮助用户连接 Telegram 时可能要求将 bot token 粘贴到对话中的不安全引导，防止凭据进入 assistant 对话记录（关闭 #120656，由 @Sedrak-Hovhannisyan 报告）。

**关键进展评估**：本轮合并展现出对可观测性（stopReason）、压缩可靠性、凭据安全三个方向的集中投入，但内存泄漏、静默失败投递等核心稳定性问题尚未有对应修复合入。

---

## 4. 社区热点

今日讨论热度最高的 Issues/PRs 及背后诉求：

- **[#116277](https://github.com/openclaw/openclaw/issues/116277) — DeepSeek v4 Flash 静默回复失败（已关闭，164 评论）**：模型（`deepseek/deepseek-v4-flash`）静默无法生成回复，用户收到泛化 fallback 消息 *"No reply was generated..."*。这是今日评论数最高的 Issue，反映用户对模型失败**可诊断性**的强烈诉求。
- **[#7707](https://github.com/openclaw/openclaw/issues/7707) — 记忆信任标签（31 评论）**：要求按来源为用户命令、网页抓取、第三方技能等记忆条目打上信任级别，防止恶意指令通过不可信内容植入记忆进而污染后续行为。社区对**记忆投毒攻击**的担忧持续升温。
- **[#44925](https://github.com/openclaw/openclaw/issues/44925) — 子代理完成静默丢失（24 评论）**：子代理任务编排存在多种静默失败模式——完成通知失败、无重试、无通知、超时不自动重启。用户要求失败可见性。
- **[#91588](https://github.com/openclaw/openclaw/issues/91588) — 网关内存泄漏 RSS 350MB→15.5GB（P0，23 评论）**：运行 2-3 天后被 OOM kill，触发反复重启，是当前最高优先级稳定性隐患。
- **[#68596](https://github.com/openclaw/openclaw/issues/68596) — 可配置流式看门狗超时（15 评论，8 个 👍）**：长推理模型（kimi-k2.5、DeepSeek-R1）触发 30s 无更新误报，用户希望阈值可调。高赞表明该痛点覆盖面较广。

**诉求共性**：用户对"静默失败"（模型无回复、子代理丢失、投递未达）的容忍度降到最低，对失败可观测性和可配置性需求强烈。

---

## 5. Bug 与稳定性

### 🔴 P0 级（今日活跃，尚无直接 fix PR）

| Issue | 描述 | 备注 |
|---|---|---|
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | 网关内存泄漏：RSS 350MB→15.5GB，OOM 反复崩溃 | 6/9 创建至今

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-09

## 1. 今日速览

过去24小时项目活跃度极高：**Issues 更新 368 条**（新开/活跃 288，关闭 80），**PR 更新 500 条**（待合并 292，合并/关闭 208），合共 868 条动态，显示项目仍处于密集开发与社区反馈双高阶段。无新版本发布。当前社区关注焦点集中在 **#78647 仓库级 god-file 分片 Epic**（62 条评论，拖了 5 天的特大重构议题）、**#64182 插件接口扩展跟踪**（30 条评论）以及多个 **P1 级稳定性 Bug**（桌面端 UI 死锁、上下文压缩丢工具链、SSH 进程泄漏）。合并/关闭的 208 条 PR 中包括多项实质修复（Windows 安装器、CJK 文件误判、SimpleX 适配器丢消息等），项目整体在稳定性与工具正确性方面有明显推进，但 session 状态安全与平台兼容类问题仍是积压最重的领域。

## 2. 版本发布

过去 24 小时无新版本发布（最新 Releases 为空）。

## 3. 项目进展

今日合并/关闭的 PR 与 Issue 合计 288 条，其中可确认的重要进展：

- **Windows 平台修复落地**：#46260（安装器 npm install 退出码 1）与 #65274（桌面端项目作用域会话回退 home cwd）均标记 `implemented-on-main` / 已关闭，Windows 安装与项目会话行为得到修正。
- **文件工具回归修复**：#76886（`read_file` 将含多字节字符的合法 UTF-8 文本误判为二进制，0.19.1 回归）和 #80308（CJK 文件误判 + `search_files` 全零结果）均已在 8 月 8 日关闭，文件工具链的非 ASCII 支持明显改善。
- **消息投递修复**：#46265（SimpleX 适配器静默丢弃 DM 回复）与 #11349（Discord 文档六处漂移 + `/voice join` 缺失）已关闭，平台适配器正确性提升。
- **流式工具调用修复**：#69442（Doubao seed-2-1 流式 tool_call JSON 截断导致 `write_file` 静默失败）标记 `implemented-on-main`，第三方模型兼容性改善。
- 新提交的 20 条 PR 中既有基础设施类（#82042 备份 SQLite busy-retry 有界化、#82039 网关重启循环熔断器），也有用户可见功能类（#82045 e2a 邮件技能、#82044 桌面端插件管理），反映项目在稳定性和功能扩展上双线推进。

总体判断：项目在过去 24 小时完成了多批早前积压的修复合并，尤其集中清理了 Windows 平台与文件工具链的回归问题，项目健康度良好。

## 4. 社区热点

- **#78647 [Epic] 仓库级 god-file 分解** — 62 条评论（🔥 最高）
  链接：https://github.com/NousResearch/hermes-agent/issues/78647
  8 月 4 日创建后持续发酵，目前已确立 "all god files are sharded, never reverted" 为常设政策。社区讨论集中在 god-file 分片的边界划分、共享接口设计，以及如何在 20 个巨型文件上协调并行重构而不产生合并冲突。这是当前社区最大的协作焦点。

- **#64182 插件接口扩展跟踪（社区创意，2026 年 7 月）** — 30 条评论
  链接：https://github.com/NousResearch/hermes-agent/issues/64182
  长期跟踪 issue，汇聚 Discord 社区对插件接口的扩展建议，目标是让排队已久的贡献者 PR 能够落地为稳定的公开接口。适合关注插件生态的贡献者参与。

- **#63047 桌面端 macOS 27 beta 上约 5 条消息后完全无响应** — 18 条评论，P1
  链接：https://github.com/NousResearch/hermes-agent/issues/63047
  用户报告在 macOS 27 beta 上 Hermes Desktop 约 5 条消息后 UI 完全冻结（不仅仅是 #40692 的输入卡顿），连设置界面也无法打开，只能依靠"碰运气"的解除冻结。属于高影响稳定性问题，讨论热度高。

- **#23717 RFC：可插拔 SessionDB Provider（PostgreSQL、MySQL 等）** — 16 条评论，4 👍
  链接：https://github.com/NousResearch/hermes-agent/issues/23717
  围绕"热更新死亡螺旋"（`git pull` 与运行中 Hermes 共享 SQLite `state.db` 导致冲突）的讨论，社区对更健壮的会话存储方案诉求明确。

- **#17565 可配置 Temperature 参数** — 13 👍（本期 👍 最高）
  链接：https://github.com/NousResearch/hermes-agent/issues/17565
  用户强烈要求暴露 LLM `temperature` 配置项，当前硬编码导致的幻觉问题引发共鸣。13 个 👍 在展示的所有 issue 中最高，说明此需求覆盖面广。

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue / PR | 描述 | 状态 |
|---|---|---|---|
| P1 | [#63047](https://github.com/NousResearch/hermes-agent/issues/63047) | Desktop 在 macOS 27 beta 上约 5 条消息后完全无响应（含设置界面） | 开放，无对应 fix PR |
| P1 | [#79278](https://github.com/NousResearch/hermes-agent/issues/79278) | 上下文压缩可能丢弃执行中的工具链——副作用已完成但结果未达 agent，agent 重放导致非幂等操作风险 | 开放，无对应 fix PR |
| P1 | [#58619](https://github.com/NousResearch/hermes-agent/issues/58619) | Desktop 重连时 spawn 无界 serve 进程，旧进程不清理；建议 `--replace` 信号量 | 开放，无对应 fix PR |
| P1 | [#65365](https://github.com/NousResearch/hermes-agent/issues/65365) | Anthropic OAuth（Claude Pro/Max）下暴露 `memory` / `session_search` 工具 schema 即触发 HTTP 400 "out of extra usage" | 开放，影响付费用户 |
| P1 | [#82039](https://github.com/NousResearch/hermes-agent/pull/82039) | 网关重启循环熔断器无法识别慢崩溃周期（#81642） | 已有 fix PR，开放 |
| P2 | [#67629](https://github.com/NousResearch/hermes-agent/issues/67629) | Windows 原生 `search_files` 绝对路径失败：`_bash_safe_path` 改写 MSYS 路径，原生 rg 无法解析 | 开放，无对应 fix PR |
| P2 | [#50707](https://github.com/NousResearch/hermes-agent/issues/50707) | SSH 终端后端硬编码 ControlMaster，Windows 原生 OpenSSH 报 "getsockname failed: Not a socket" | 开放，无对应 fix PR |
| P2 | [#80308](https://github.com/NousResearch/hermes-agent/issues/80308) | `read_file` 误判合法 UTF-8 CJK 文件为二进制，`search_files` 全查询返回 0 | 已关闭（修复完成） |
| P2 | [#76886](https://github.com/NousResearch/hermes-agent/issues/76886) | `read_file` 在 1000 字节采样切断多字节字符时误判二进制（0.19.1 回归） | 已关闭（修复完成） |
| P2 | [#46260](https://github.com/NousResearch/hermes-agent/issues/46260) | Windows 安装器在 "desktop" 阶段 npm install 退出码 1 | 已关闭（implemented-on-main） |
| P2 | [#75598](https://github.com/NousResearch/hermes-agent/issues/75598) | 更新后程序不稳定，多 gateway 配置互相冲突 | 已关闭 |

稳定性评价：**文件工具链回归已基本清完，但 session 状态安全（P1 三连）仍是最大风险敞口**。特别是 #79278 的非幂等重放问题，属于数据安全级缺陷，建议维护者优先安排修复。

## 6. 功能请求与路线图信号

- **#78647 god-file 分片 Epic**（62 评论）：已升级为常设政策，预计后续 PR 会大量围绕此展开，是当前最明确的架构方向。
- **#23717 可插拔 SessionDB Provider**（16 评论，4 👍）：解决 SQLite 热更新冲突，需求论证扎实，RFC 已就绪，若纳入路线图将是基础设施层的重要升级。
- **#47349 可配置记忆后端**（15 评论）：要求将 `memory.md` 重命名为 `rules.md` 并支持禁用 memory.md、仅用 honcho/fact_store。
- **#13332 混合工具预选（语义 + 关键词）**（9 评论，4 👍）：通过 RAG 式 schema 注入降低 ~14k token 开销，与 #6839 的懒加载方案互补。
- **#17565 可配置 Temperature**（13 👍）：硬编码温度导致的幻觉问题有广泛共鸣，实现成本低、用户价值高，有望进入下一版本。
- **#509 认知记忆操作**（7 评论，4 👍）：LLM 驱动的记忆编码、整合与自适应检索，受 CrewAI 启发，方向前沿但实现复杂。
- **#28056 cron/agent 运行的有界重试质量门控**：面向安全巡检、合规检查等场景，需求明确。
- **#79890 WhatsApp 功能对齐运动**：与 WhatsApp Business Platform Cloud API 对齐的 meta-issue，反映平台适配器完整性的持续投入。

支撑性 PR 信号：#82045（e2a 邮件技能）、#82048（技能作者 v2.1.0）、#82044（桌面端插件管理）等新功能 PR 密集提交，说明技能生态与插件管理是当下功能开发的热点方向。

## 7. 用户反馈摘要

- **升级回归伤害真实用户**（#76886）：用户更新后 Obsidian 笔记突然打不开——"它们是纯 UTF-8 markdown，更新前一直读得好好的"。此类回归直接打击用户对自动更新的信任，好在当日已修复。
- **桌面端死锁影响核心使用**（#63047）：macOS 用户报告"约 5 条消息后完全无响应，只能碰运气解冻"，且已明确这不是 #40692 的输入卡顿，而是全局 UI 冻结。该问题已开放近一个月，用户耐心在消耗。
- **AI 辅助报告成为常态**（#31584、#46260）：多份 issue 注明"AI 辅助起草，用户审核后提交"，显示 Hermes 用户群体已开始用 AI 代理来写 Bug 报告，这也侧面验证了项目核心场景的价值。
- **付费用户受阻**（#65365）：Claude Pro/Max 订阅用户使用 OAuth 时，只要工具列表包含 `memory` 或 `session_search` 就被 Anthropic 拒绝——"我已经为 Claude 付费，却被拒之门外"，这是对既有订阅用户的实际伤害。
- **温度参数缺失引发幻觉抱怨**（#17565）：用户称"硬编码温度导致严重幻觉"，13 个 👍 表明大量用户希望像控制采样参数一样控制推理行为。
- **中文用户需求**（#80821）：中文用户请求在桌面聊天 UI 中支持 LaTeX/MathJax 渲染，当前 KaTeX 未激活，数学公式以原始文本显示。

## 8. 待处理积压

以下为已开放较久、讨论充分但尚未获得实施或维护者明确回应的重要条目：

- **#23717 可插拔 SessionDB Provider RFC**（5 月 11 日创建，16 评论，4 👍）
  链接：https://github.com/NousResearch/hermes-agent/issues/23717
  热更新冲突问题论证成熟，RFC 已成型，建议维护者给出接受/拒绝/排期决策。

- **#17565 可配置 Temperature**（4 月 29 日创建，13 👍）
  链接：https://github.com/NousResearch/hermes-agent/issues/17565
  高赞、低实现成本，长期未获回应，社区耐心有限。

- **#63047 桌面端 macOS 死锁**（7 月 12 日创建，P1，18 评论）
  链接：https://github.com/NousResearch/hermes-agent/issues/63047
  P1 严重度，开放近一个月无 fix PR，且影响 macOS 27 beta 用户。

- **#13332 混合工具预选**（4 月 21 日创建，4 👍）
  链接：https://github.com/NousResearch/hermes-agent/issues/13332
  解决真实 token 开销痛点（30+ 工具时约 14k tokens），与懒加载提案 #6839 需要协调。

- **#509 认知记忆操作**（3 月 6 日创建，4 👍）
  链接：https://github.com/NousResearch/hermes-agent/issues/509
  已积压 5 个月，属于较大功能设计，建议明确

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报（2026-08-09）

## 1. 今日速览

- 过去 24 小时仓库活跃度较高：11 条 Issue 更新（全部 Open），17 条 PR 更新（全部待合并），无 Release，无已关闭 Issue / 已合并 PR。
- 核心维护者 @neubig 密集提交 9 个跟踪 Issue 与对应 PR，覆盖 LLM 路由元数据、预检验证、profiles 迁移修复、telemetry 增强等，显示 SDK 正在经历一次系统性的能力补全与治理优化。
- 社区讨论热度集中在插件体系：既有 7 个月未决的 Plugin 1.0 定义（#1440，26 评论），也有新提出的 Agent Plugins 开放标准支持（#4405），插件生态已成为社区与维护者的共同关注焦点。
- 稳定性修复覆盖多个真实痛点：headless 模式 `max_input_tokens` 不生效、MCP fetch 依赖未固定、Windows 下 ACP 无法启动、URL 查询参数中 API key 明文泄露等。
- 整体评估：项目处于“高产出 + 社区活跃”的良性阶段，但合并速度待提升——17 个待合并 PR 中没有 1 个在过去 24 小时被合并。

## 2. 版本发布

过去 24 小时无新版本发布。

## 3. 项目进展

虽然过去 24 小时没有 PR 被合并或关闭，但 17 个待合并 PR 清晰勾勒出项目即将落地的能力版图：

- **LLM 配置与路由**：`feat(llm): resolve provider-specific runtime metadata for routed models`（#4423）、`feat: add pre-flight LLM validation endpoint`（#4422）、`refactor(sdk): centralize LLM call context`（#4159）——将使 OpenRouter 等路由提供商的动态 limit 被正确识别，并在保存 profile 前用 1-token 请求前置校验配置。
- **插件架构**：`refactor(plugin): extract PluginFormat strategy`（#4420）为支持 Agent Plugins 等多样插件格式做铺垫，与 #1440、#4405 路线图呼应。
- **稳定性修复**：`fix(profiles): repair v1 skills migration`（#4320）、`fix(mcp): pin fetch server runtime dependencies`（#4303）、`fix(settings): inherit condenser max_tokens from LLM effective_max_input_tokens`（#4435）均为明确的 bug 修复。
- **可观测性与安全**：`feat(observability): allow selecting Laminar instruments`（#4434）、`fix(sdk): add logging filter to redact URL query parameters containing secrets`（#4424）在减少数据泄露风险的同时优化初始化延迟。
- **Windows 支持**：`fix(acp): resolve launch commands via PATHEXT-aware lookup`（#4408）解决 ACP 在 Windows 上的启动问题。

这些 PR 多由维护者或认证贡献者提交，且大部分已有对应 Issue 跟踪，说明项目路线图正在被快速执行。但目前 17:0 的“开放：合并”比例意味着团队需要尽快安排 review 与 merge，避免积压。

## 4. 社区热点

- [#1440 [enhancement] Plugin 1.0 Definition](https://github.com/OpenHands/software-agent-sdk/issues/1440)：26 条评论，是今日讨论最热 Issue。用户 @jpelletier1 于 2025-12-18 提出，至今仍 Open。核心争议点在“Plugin 是 SDK 概念还是 OpenHands 概念”、是否纳入 MCP config 与 runtime config。该 Issue 已成为插件路线图的基础参考。
- [#3746 [bug] max_input_tokens 在 headless CLI 模式不生效](https://github.com/OpenHands/software-agent-sdk/issues/3746)：4 条评论，用户 @xiaolei373 报告 `agent_settings.json` 中配置被忽略，属于影响实际使用的配置缺陷，已由 PR #4435 修复，社区反馈与修复形成闭环。
- [#4405 [enhancement] Spec: Support the Agent Plugins portable package format](https://github.com/OpenHands/software-agent-sdk/issues/4405)：2026-08-06 提出，2 天内即获维护者标记 `Needs Design`，体现了对社区开放标准的积极态度。Agent Plugins 由 Amazon、Cursor、Microsoft、OpenAI 等维护者推动，若被 SDK 支持，将显著提升插件的可移植性。

## 5. Bug 与稳定性

按严重程度和影响面排列：

1. **敏感信息泄露（高）**：PR [#4424](https://github.com/OpenHands/software-agent-sdk/pull/4424) 指出生产 Datadog 日志中存在 32+ 条用户 API key 以明文出现在 URL 查询参数中的记录，来自 httpx/httpcore 的错误日志。该 PR 为日志过滤器提供修复，建议优先合并并发布安全补丁。
2. **功能失效（中）**：[#3746](https://github.com/OpenHands/software-agent-sdk/issues/3746) `llm.max_input_tokens` 在 headless CLI 模式不生效，导致用户无法控制上下文长度。已有 PR [#4435](https://github.com/OpenHands/software-agent-sdk/pull/4435) 修复（root cause 为 `build_condenser()` 中配置被丢弃）。
3. **迁移回归（中）**：[#4431](https://github.com/OpenHands/software-agent-sdk/issues/4431) 旧版 `default` agent profile 在升级后失去可编辑性，属于 v1→v2 迁移 bug。修复 PR [#4320](https://github.com/OpenHands/software-agent-sdk/pull/4320) 已移除冗余的 embedded `skills` 字段并保持 schema v2。
4. **运行时依赖不稳定（低）**：[#4432](https://github.com/OpenHands/software-agent-sdk/issues/4432) `mcp` 2.0.0 将 `McpError` 重命名为 `MCPError`，导致 fetch server 运行失败。PR [#4303](https://github.com/OpenHands/software-agent-sdk/pull/4303) 已锁定依赖并保证 CI 通过。
5. **Windows 兼容性（低）**：[PR #4408](https://github.com/OpenHands/software-agent-sdk/pull/4408) 修复 ACP 在 Windows 无法 spawn 的问题，因为 `CreateProcess` 只追加 `.exe`，无法处理 `.cmd`/`.bat`。
6. **其他**：[#4153](https://github.com/OpenHands/software-agent-sdk/pull/4153) 允许 `security_risk` 参数出现在只读工具（如 finish）上，减少 Agent Canvas 的噪声日志。

## 6. 功能请求与路线图信号

以下功能请求与正在开发的 PR 高度关联，极有可能进入下一版本：

- **插件生态**：
  - [#1440 Plugin 1.0 Definition](https://github.com/OpenHands/software-agent-sdk/issues/1440) 与 [#4405 Agent Plugins 标准](https://github.com/OpenHands/software-agent-sdk/issues/4405) 共同指向插件格式的标准化。配套重构 PR [#4420](https://github.com/OpenHands/software-agent-sdk/pull/4420) 已提取 `PluginFormat` 策略，为多格式支持铺路。
- **LLM 能力增强**：
  - [#4428 / #4421 路由模型运行时元数据](https://github.com/OpenHands/software-agent-sdk/issues/4428)：解决 OpenRouter 等路由提供商静态 catalog 与实际 endpoint limit 不一致的问题，PR [#4423](https://github.com/OpenHands/software-agent-sdk/pull/4423) 已实现。
  - [#4429 预检 LLM 验证端点](https://github.com/OpenHands/software-agent-sdk/issues/4429)：新增 `POST /api/profiles/{name}/validate`，在保存配置前做 1-token 验证，防患于大量无效配置。PR [#4422](https://github.com/OpenHands/software-agent-sdk/pull/4422) 为后端实现。
- **可观测性与部署**：
  - [#4434 可选择性启用 Laminar instruments](https://github.com/OpenHands/software-agent-sdk/pull/4434)（延迟从 5.971s 降至 0.370s）
  - [#4427 telemetry 区分自动化对话](https://github.com/OpenHands/software-agent-sdk/issues/4427)（PR #4425）
  - [#4426 observability 延迟初始化](https://github.com/OpenHands/software-agent-sdk/pull/4426)
- **MCP 动态性**：PR [#4402](https://github.com/OpenHands/software-agent-sdk/pull/4402) 让活跃会话能刷新后端拥有的 MCP 工具，适用于 E2B 中跨版本部署场景。

## 7. 用户反馈摘要

- **配置失效的直接反馈**：用户 @xiaolei373 在 [#3746](https://github.com/OpenHands/software-agent-sdk/issues/3746) 中明确表示 `max_input_tokens` 配置未生效，并贴出脱敏配置。该类反馈反映了“配置项是否真正贯通调用链”是

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-09

## 今日速览

过去 24 小时 Pi 项目整体活跃度较高，以 Issue 关闭（32 条）和 Bug 修复 PR 合并（7 条）为主。社区讨论焦点集中在两个长期问题上：`openai-codex` 连接可靠性（#4945，76 条评论）和 auto-compaction 触发策略缺陷（#6879，15 条评论）。今日无新版本发布，但有多个稳定性修复 PR 合入（DeepSeek `max_tokens`、并发 compaction 崩溃、全屏复制换行等），项目健康度良好，维护节奏稳定。长期未响应的 #4945 和 #6879 值得维护者重点关注。

---

## 版本发布

今日无新版本发布。

---

## 项目进展

今日合入/关闭的 PR 共 7 条，主要覆盖 **AI 提供商兼容性修复、TUI 体验优化、扩展机制修复** 三个方向，项目整体向前迈进了实质性的一步。

### 已合并/关闭 PR 亮点

- **DeepSeek 原生模型请求参数修复**（[#7811](https://github.com/earendil-works/pi/pull/7811)）— 修复 Pi 向原生 DeepSeek 模型发送 `max_completion_tokens`（被忽略）而非文档要求的 `max_tokens` 的问题。直接影响 DeepSeek 用户输出长度控制的正确性，属实际可用性 Bug 修复。

- **`--version` 增加运行时标注**（[#7834](https://github.com/earendil-works/pi/pull/7834)）— 输出从 `0.84.1` 变为 `0.84.1 (bun/node/deno)`，便于 issue 报告和自动化诊断快速区分运行时相关问题。关闭 #7244。

- **修复并发触发 compaction 导致 TUI 崩溃**（[#7810](https://github.com/earendil-works/pi/pull/7810)）— 快速连按 `/compact` 或快捷键时 `AbortController` 被覆盖，产生 "Cannot read properties of undefined (reading 'signal')" 崩溃。此修复直接提升交互稳定性。

- **全屏模式复制不再产生多余换行**（[#7721](https://github.com/earendil-works/pi/pull/7721)）— 长行自动换行时，按视觉行复制会把一行拆成多行粘贴。修复后按原始内容边界复制。

- **OpenAI-compatible provider `length` 停止原因识别**（[#7817](https://github.com/earendil-works/pi/pull/7817)）— 兼容 Doubao / Volcengine Ark 等返回 `incomplete_details.reason = 'length'` 的 provider，避免误判为错误。

- **notify 示例扩展从 `agent_end` 改为 `agent_settled`**（[#7833](https://github.com/earendil-works/pi/pull/7833)）— `agent_end` 在每次低层 run 结束后即触发（早于重试、compaction、后续 follow-up），导致通知时机不准。改用 `agent_settled` 后通知更准确。不影响核心逻辑，但改善扩展开发者的示例体验。

- **从 oh-my-pi 移植 A 级 agent 能力**（[#7823](https://github.com/earendil-works/pi/pull/7823)）— 移植 stream rules、subagent tools、advisor、cross-session memory 四项能力到 pi 核心。按功能拆分了 commit，便于审查。

### 待合并 PR（5 条）

- [#7610](https://github.com/earendil-works/pi/pull/7610) — 新增 LLM Gateway 和 LLM Gateway DevPass provider（OpenRouter 风格路由）
- [#7713](https://github.com/earendil-works/pi/pull/7713) — telemetry 上下文支持 stream assistant/config（harness v2 基础）
- [#7801](https://github.com/earendil-works/pi/pull/7801) — 语法高亮 grammar 懒加载，作者为 mitsuhiko
- [#7807](https://github.com/earendil-works/pi/pull/7807) — 原生 DeepSeek V4 Flash 支持 `low` reasoning effort
- [#7784](https://github.com/earendil-works/pi/pull/7784) — recovery state 改为基于 record queries 推导

---

## 社区热点

今日讨论热度集中在两条长期 Issue 上，既有代表性又反映了真实的使用痛点。

### 1. `openai-codex` 连接可靠性问题（[#4945](https://github.com/earendil-works/pi/issues/4945)）— 76 条评论，👍 31

**状态**：OPEN / [inprogress]

**核心诉求**：`openai-codex` / `gpt-5.5` 在交互式 TUI 中频繁卡在 `Working...` 状态，无文本流、无工具调用、无报错，只能按 Escape 中止。该问题已持续数月（5 月底至今），且今日有新的关联 Issue [#7820](https://github.com/earendil-works/pi/issues/7820) 补充了详细数据：约 30% 的长思维链请求（3-25 分钟）因 WebSocket 1006 传输错误中断，且 stream 请求缺少 `retryProviderRequest` 包装，中断即 fatal。

**分析**：这是目前社区呼声最高、最影响日常使用体验的问题。已有 76 条评论说明用户投入了大量排查精力，但不清楚进展如何。**强烈建议维护者尽快给出 fix 时间表或 progress update。**

### 2. Auto-compaction 触发策略缺陷（[#6879](https://github.com/earendil-works/pi/issues/6879)）— 15 条评论，👍 15

**状态**：OPEN / [bug]

**核心诉求**：上下文显示超过 100% 后 auto-compaction 仍不触发，直到 API 在 373k tokens 处拒绝请求。用户认为应在每个 agentic step 之后检查，而非整轮 agent loop 结束后。

**分析**：这是模型长跑场景（agentic turn 超过 2 小时）下的关键稳定性问题，与今日关闭的 [#7821](https://github.com/earendil-works/pi/issues/7821)（auto-compaction 只在 `agent_end` 后检查）直接相关，且 #7821 详细定位了根因。两条 Issue 相互印证，fix 方向明确。

---

## Bug 与稳定性

按严重程度排列（高→低）：

| 严重程度 | Issue/PR | 描述 | 状态 |
|---------|----------|------|------|
| 🔴 严重 | [#7825](https://github.com/earendil-works/pi/issues/7825) | **恶意包报告**：`@baylarsadigov/omp-undo-redo@1.2.3` 导致每次发送消息延迟 2-5 秒，卸载后恢复正常。已标记 [package-report] | 已关闭 |
| 🟠 高 | [#6879](https://github.com/earendil-works/pi/issues/6879) | auto-compaction 超过 100% 仍不触发，直到 provider 溢出（373k tokens） | OPEN |
| 🟠 高 | [#7820](https://github.com/earendil-works/pi/issues/7820) | `openai-codex` stream 请求无 `retryProviderRequest` 包装，30% 长请求因 WebSocket 1006 中断即 fatal | 已关闭（discussion） |
| 🟠 高 | [#7782](https://github.com/earendil-works/pi/issues/7782) | Bedrock 生成的 tool call 含空 key，Pi 接受并执行后永久污染 session，每次回放都被拒绝，会话被 brick | 已关闭 |
| 🟡 中 | [#7810](https://github.com/earendil-works/pi/pull/7810) | 并发 compaction 导致 `Cannot read properties of undefined (reading 'signal')` 崩溃 | ✅ 已修复 |
| 🟡 中 | [#7829](https://github.com/earendil-works/pi/issues/7829) | Windows 下无效 `settings.json` 被静默忽略，随后报误导性的 "bash not found" | 已关闭 |
| 🟡 中 | [#7806](https://github.com/earendil-works/pi/issues/7806) | macOS 终端流式输出时滚轮自动回顶，无法停留查看历史（0.84.1） | 已关闭 |
| 🟡 中 | [#7734](https://github.com/earendil-works/pi/issues/7734) | print mode + 扩展 + subagent 场景下进程退出时挂起（0.84.0/0.83.0） | 已关闭 |
| 🟢 低 | [#7832](https://github.com/earendil-works/pi/issues/7832) | Mermaid 渲染不支持 `:::className` class-assign 语法 | 已关闭 |
| 🟢 低 | [#7835](https://github.com/earendil-works/pi/issues/7835) | Edit tool 拒绝单对象 `edits` 参数（仅接受数组） | 已关闭 |
| 🟢 低 | [#7836](https://github.com/earendil-works/pi/issues/7836) | Edit fuzzy match 不折叠连续空白，导致缩进差异时匹配失败 | 已关闭 |

---

## 功能请求与路线图信号

### 高优先级信号（可能进入下一版本）

- **Meta Model API 支持**（[#7543](https://github.com/earendil-works/pi/issues/7543)，👍 3）— 用户请求接入 Meta 的 Muse Spark，PR 描述为 "trivial change"。考虑到今天已有新增 LLM 提供商的 PR（#7610），此类 provider 扩充需求实现成本低，验收可能性较高。

- **LLM Gateway / DevPass 内置 provider**（[#7610](https://github.com/earendil-works/pi/pull/7610)）— OpenRouter 风格的统一网关，替换了被 auto-closed 的 #7480。已提交 4 天，待维护者 review。

- **多登录账号支持**（[#7814](https://github.com/earendil-works/pi/issues/7814)）— 用户有两个 ChatGPT Plus 订阅，希望不通过自定义 provider 扩展即可同时使用。体现了多账号并发管理的真实需求，若 OpenAI 侧无 API 限制，实现上可行。

- **多配置档案（profiles）**（[#7813](https://github.com/earendil-works/pi/issues/7813)）— 通过 CLI 参数 / 环境变量 / per-project 切换不同的 `settings.json` 配置。对团队场景和多项目切换有明显价值。

### 中低优先级（长期积累的 UX 优化）

- 全屏 TUI 逐行滚动（[#7830](https://github.com/earendil-works/pi/issues/7830)）— 最小键盘滚动步长目前是半页，用户希望有可按键绑定的逐行滚动。
- 鼠标滚轮步长可配置（[#7765](https://github.com/earendil-works/pi/issues/7765)）— 硬编码 1 行，建议可调。
- 删除当前活跃 Session（[#7818](https://github.com/earendil-works/pi/issues/7818)）— 目前只能删除非活跃 session，交互不直观。
- `immediateUserMessage` 设置（[#7819](https://github.com/earendil-works/pi/issues/7819)）— 用户期望按 Enter 后消息立即本地显示，而非等 agent 处理后回显（当前延迟约 1 秒）。
- Cmd+V 粘贴图片（[#4332](https://github.com/earendil-works/pi/issues/4332)）— macOS 上 bracketed paste 为空时检查剪贴板图片。被标记为 no-action 和 "closed-because-weekend"。

---

## 用户反馈摘要

### 正面反馈（来自 PR/Issue 中的间接信息）
- 用户对修复 DeepSeek `max_tokens` 的 PR 给出了明确的 API 文档对照和测试结果，说明社区对这类精准修复认可度较高。
- `--version` 标注运行时（#7834）被定位为"方便 issue 报告者与自动化诊断"，体现出社区对可诊断性的重视。

### 负面痛点（重点倾听）
- **`openai-codex` 连接可靠性是当前最大痛点**（#4945）：用户反复遇到卡死在 `Working...`、只能 Escape 中止的体验，且 30% 的长请求失败率（#7820）对深度使用是灾难性的。
- **上下文压缩策略不够智能**（#6879/#7821）：用户对"超过 100% 仍不压缩，直到 API 拒绝"表示明显不满，说明现有迁移/压缩策略在长 agentic 任务下不够可靠。
- **恶意/可疑扩展影响真实使用**（#7825）：用户明确上传了有问题的包名和版本，报告卸载后立即恢复。生态扩展的安全性需要更明确的审查机制或提示。
- **session 隔离不明确**（#7812）：并行运行多个 Pi 进程时会复用默认 session，导致测试结果互相污染。用户希望有文档说明或加保护。

---

## 待处理积压

| 条目 | 创建时间 | 更新 | 评论量 | 状态 | 建议 |
|------|---------|------|--------|------|------|
| [#4945](https://github.com/earendil-works/pi/issues/4945) `openai-codex` 连接可靠性 | 2026-05-24 | 2026-08-08 | 76 | OPEN / [inprogress] | ⚠️ 已存在 2.5 个月，评论 76 条，是社区关注度最高的 Issue。今日有 #7820 补充根因数据。建议维护者给出明确的时间表或阶段性结论 |
| [#6879](https://github.com/earendil-works/pi/issues/6879) auto-compaction 超过 100% 仍不触发 | 2026-07-20 | 2026-08-08 | 15 | OPEN / [bug] | ⚠️ 已有 #7821 从代码层面定位根因，fix 方案明确。建议尽快安排修复 |
| [#7610](https://github.com/earendil-works/pi/pull/7610) LLM Gateway provider | 2026-08-04 | 2026-08-08 | — | OPEN | 已等待 4 天，无 review 活动。属于新增 provider 的低风险改动 |
| [#

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报（2026-08-09）

## 1. 今日速览

过去 24 小时 Temporal 核心仓库呈现 **「开发侧活跃、社区侧静默」** 的态势。Issues 层面无任何新增、关闭或活跃讨论，但 PR 侧有 9 条更新，其中 3 条已合并/关闭，6 条仍在开放中。最值得关注的是 **1.32.0 release 分支已被创建**（#11449），标志着新版本进入发布准备阶段。同时，可靠性（reliability-2026）系列持续推进，本周已合并了回调验证器（#11442）和队列积压年龄指标（#11255）两项实质性改进。整体项目健康度良好，开发主线稳健向前。

## 2. 版本发布

今日无新版本正式发布，但出现一个重要信号：

- **[#11449] 1.32.0: Prepare release branch**（已关闭，2026-08-08）
  - 链接：https://github.com/temporalio/temporal/pull/11449
  - 由 `@temporal-cicd[bot]` 自动创建，说明 1.32.0 已进入发布候选阶段。该 PR 的主要工作是覆盖 governance 文件和更新依赖，通常意味着版本冻结与最终测试的开始。
  - **对下游的影响**：若你正在使用 Temporal Server，建议关注后续 1.32.0 的正式 Release Notes，提前规划升级窗口。

## 3. 项目进展

今日有 3 个 PR 被合并/关闭，均对项目的可靠性、可观测性和版本管理有实质贡献：

### 已合并/关闭（3 条）

| PR | 内容 | 意义 |
|---|---|---|
| [#11449](https://github.com/temporalio/temporal/pull/11449) | 1.32.0 发布分支准备 | 版本冻结，进入发布流程 |
| [#11442](https://github.com/temporalio/temporal/pull/11442) | 将 Callback Validator 应用于 Workflow Update Callbacks | `[reliability-2026]` 系列的一部分，统一了回调校验逻辑的覆盖范围，避免不同调用场景下行为不一致。附带新增单元测试 |
| [#11255](https://github.com/temporalio/temporal/pull/11255) | 新增即时队列积压年龄指标 `shardinfo_immediate_queue_backlog_age` | 这是 `shardinfo_immediate_queue_lag` 的时间维度补充。由于即时任务键不携带时间戳，该指标通过其他方式计算年龄，为排查队列积压问题提供了更全面的可观测性数据 |

**整体评估**：这 3 个 PR 的合入意味着 Temporal 在 **可靠性加固** 和 **可观测性完善** 上继续稳步推进，且 1.32.0 发布流程已启动，项目正处于一个常规的迭代节奏中。

## 4. 社区热点

由于过去 24 小时没有新的 Issues 或评论数据，热点主要集中于 **当前开放中的 6 条 PR** 的讨论与推进上：

- **[#11415] Add completion callbacks to SANOs**（开放中）
  - 链接：https://github.com/temporalio/temporal/pull/11415
  - 作者：`@chrsmith`
  - 这是一个 **stacked PR** 的一部分，为 worker callbacks 功能新增 `completion_callbacks` API 面。说明回调功能正在经历较大规模的重构与扩展。

- **[#11413] Persist Callback terminal failures**（开放中）
  - 链接：https://github.com/temporalio/temporal/pull/11413
  - 作者：`@chrsmith`
  - 同样属于 stacked PR 系列，为 CHASM Callback 组件新增字段以持久化终态失败。这两个 PR 共同指向一个方向：**让回调机制在失败场景下更加可靠和可追溯**。

- **[#11134] Fix: v1->V2 schedules migration guard & fix**（开放中，已 22 天）
  - 链接：https://github.com/temporalio/temporal/pull/11134
  - 作者：`@davidporter-id-au`
  - 这是一个**长期开放**的 PR，涉及 V1 到 V2 调度器迁移的防护与修复。摘要中明确提到“修复 3rd party SDK 在迁移过程中崩溃”的问题，是社区开发者可能比较关心的实际痛点。

**分析**：上述 PR 的活跃更新表明，**调度器迁移稳定性** 和 **回调持久化** 是目前开发团队投入最大的两个方向，很可能与下一版本的路线图强相关。

## 5. Bug 与稳定性

今日无新报告的 Bug Issue，但从开放 PR 中可以观察出若干待修复的稳定性问题：

| 严重程度 | 问题描述 | 相关 PR | 状态 |
|---|---|---|---|
| 中 | **调度器迁移导致的 SDK 崩溃**：V1->V2 迁移过程中，3rd party SDK 可能出现崩溃。已有修复方案但尚未合入 | [#11134](https://github.com/temporalio/temporal/pull/11134) | Fix PR 开放中 |
| 中 | **CHASM 纯任务执行后未重新校验**：`Node.EachPureTask` 中的一个 TODO，即纯任务执行后若仍有效，应返回 `serviceerror.Internal` 软断言。该问题可能掩盖某些不该继续执行的任务 | [#11433](https://github.com/temporalio/temporal/pull/11433) | Fix PR 开放中 |
| 低 | **迁移数据的 ID 生成行为变更**：V2->V1 迁移后，调度器启动时需要保留已迁移的 workflow ID/request ID，而非重新生成 | [#11427](https://github.com/temporalio/temporal/pull/11427) | Fix PR 开放中 |
| 低 | **测试任务管理器适配不足**：新的 matcher 未在测试任务管理器中完全适配，影响测试稳定性 | [#11443](https://github.com/temporalio/temporal/pull/11443) | Fix PR 开放中 |

## 6. 功能请求与路线图信号

今日没有新的功能请求 Issues，但开发中的 PR 通常预示着路线图方向：

- **回调功能的增强与终态持久化**（[#11415](https://github.com/temporalio/temporal/pull/11415)、[#11413](https://github.com/temporalio/temporal/pull/11413)）
  - 这两个 PR 属于同一 stacked 系列，为 worker callbacks 增加 `completion_callbacks` 并持久化终态失败。结合 [#11442](https://github.com/temporalio/temporal/pull/11442) 的合入，可以判断 **回调机制（Callback）正在经历一次系统性的可靠性升级**，未来版本中 SDK 层面可能暴露新的回调形态。

- **调度器迁移的长期改进**（[#11134](https://github.com/temporalio/temporal/pull/11134)、[#11427](https://github.com/temporalio/temporal/pull/11427)）
  - V1/V2 调度器迁移一直是近期重点。今日数据中有两个 PR 都在处理迁移过程中的 ID 保留、防护与 SDK 兼容性问题。背后的信号是：**官方在积极支持从老版本平滑迁移到新调度器，并修复第三方 SDK 的兼容性**。

- **可观测性指标补全**（[#11255](https://github.com/temporalio/temporal/pull/11255) 已合入）
  - 即时队列积压年龄指标已合入，说明团队在持续增强 `shardinfo` 指标集，为大规模部署提供更精确的排障手段。

## 7. 用户反馈摘要

> 数据说明：本次数据快照中未采集到 Issues 评论内容，以下反馈基于 PR 摘要中的上下文间接提炼。

- **调度器迁移的 SDK 兼容性是实际痛点**（来自 [#11134](https://github.com/temporalio/temporal/pull/11134) 摘要）
  - 存在 3rd party SDK 在 V1->V2 迁移过程中崩溃的场景。开发者需要更平滑的迁移路径，而非依赖 SDK 自行规避。

- **回调失败的可追溯性不足**（来自 [#11413](https://github.com/temporalio/temporal/pull/11413) 摘要）
  - 目前回调的终态失败未能持久化存储，导致用户在回调最终失败后难以排查原因。社区希望看到更完整的失败追溯能力。

## 8. 待处理积压

以下是一个值得维护者关注的长期未合入 PR：

- **[#11134] Fix: v1->V2 schedules migration guard & fix**
  - 链接：https://github.com/temporalio/temporal/pull/11134
  - 创建于 2026-07-18，已开放 **22 天**，最近一次更新在 2026-08-07。
  - 该 PR 包含测试复现、迁移路径修复等一系列改动，较大且涉及面广，但涉及 SDK 兼容性问题，优先级可能比表面积看起来更高。与其配套的 [#11427](https://github.com/temporalio/temporal/pull/11427) 也在等待合并，说明整个迁移修复链条可能需要整体评估与推进。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*