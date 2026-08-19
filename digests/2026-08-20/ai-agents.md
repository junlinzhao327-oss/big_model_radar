# OpenClaw 生态日报 2026-08-20

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-19 22:36 UTC

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

# 个人 AI 助手 / 自主智能体开源生态横向对比分析报告

**报告日期：2026-08-20** | 数据窗口：2026-08-19 00:00 UTC → 2026-08-20 00:00 UTC

---

## 1. 生态全景

当前个人 AI 助手与自主智能体生态正处于**密集迭代与分化并存的爆发期**。终端侧由 Hermes Agent（桌面多平台）与 Pi（终端原生）领跑，围绕会话体验、模型切换与工具调用可靠性展开高强度打磨；基础设施侧 LiteLLM 承担模型网关角色，正成为连接 Claude Code 等 Agent 生态的关键桥梁；Temporal 则在智能体长时间运行的持久化与调度底层持续加固。全生态的共性焦点已从“能调用模型”转向“**可靠地完成长任务**”——会话稳定性、成本核算准确性、工具调用可观测性与供应链安全成为今日四大高频议题。整体健康度良好，但多数项目存在“活性极高、待合并积压与稳定问题并行”的特征。

---

## 2. 各项目活跃度对比

| 项目 | Issue 更新 | PR 更新 | Release | 合并/关闭率 | 健康度评估 |
|------|-----------|--------|---------|------------|-----------|
| **Hermes Agent** | 413（新开/活跃 356，关闭 57） | 500（待合并 396，合并/关闭 104） | 无（最新 v0.20.4） | Issue 13.8%；PR 20.8% | 中等偏上 — 极高活跃，但桌面端“profile 切换/会话加载”P1 问题积压明显 |
| **Pi** | 67（新开/活跃 13，关闭 54） | 32（合并/关闭 25，待合并 7） | 无 | Issue 80.6%；PR 78.1% | 良好 — 密集修复与打磨阶段，关闭率高，健康度最优 |
| **LiteLLM** | 72（新开/活跃 53，关闭 19） | 306（待合并 184，合并/关闭 122） | v1.99.0-dev.1（预发布） | Issue 26.4%；PR 39.9% | 良好 — 高迭代，122 个 PR 合入，UI 重构与 Bug 修复并行 |
| **Temporal** | 22（新开/活跃 20，关闭 2） | 80（待合并 51，合并/关闭 29） | 无 | Issue 9.1%；PR 36.3% | 良好 — 密集迭代期，讨论聚焦长期运营主题 |
| **OpenClaw**（核心参照） | — | — | — | — | 本次数据窗口未提供，暂无法量化评估 |
| **OpenHands SDK** | — | — | — | — | 本次数据窗口未提供 |

> 注：OpenClaw 与 OpenHands SDK 在本次日报中未包含可量化数据，以下分析基于其余四个已提供完整数据的项目展开。

---

## 3. OpenClaw 在生态中的定位

OpenClaw（github.com/openclaw/openclaw）在本生态中被明确标注为**核心参照项目**，即其余 Agent 项目在功能设计、社区运营与迭代节奏上均以其为对标锚点。虽然本次数据窗口未提供其指标，但从生态结构可推断其定位：**处于终端 Agent（Hermes、Pi）与基础设施层（LiteLLM、Temporal）之间的枢纽位置**——上游承接多模型接入，下游输出可扩展的工具调用范式。其余项目的功能演进（如 Hermes 的 skill 沉淀方法论、Pi 的扩展事件暴露、LiteLLM 的 Claude Code 接线）实质上是围绕 OpenClaw 确立的 Agent 交互范式进行外围补全。建议后续报告补充其 Issue/PR/Release 数据以完善对比。

---

## 4. 共同关注的技术方向

以下技术方向在今日报告中至少两个项目同时涌现，代表生态共性诉求：

| 方向 | 涉及项目 | 具体诉求 |
|------|---------|---------|
| **Agent 工具调用可靠性** | LiteLLM（#37273/#37031 Claude Code 流式翻译工具调用 Bug）、Hermes（工具 provider 路由修复）、Pi（流启动时暴露工具元数据 #7953） | 工具调用链路的端到端可观测性与故障修复是当前最高优先级 |
| **成本核算与计费准确性** | Pi（Anthropic 降级计费 #8352、DeepSeek 代理计费 #8359）、Hermes（DeepSeek 计费修复）、LiteLLM（网关计费） | 降级模型计价、代理路由中 reasoning 识别等边界场景的计费错误集中爆发 |
| **Claude Code 生态集成** | LiteLLM（`lite login --config-claude` #37507）、Pi（GitHub Copilot 登录 429 问题 #8121） | Agent 的登录/配置体验正从手工改写配置向“登录即接线”演进 |
| **会话状态持久化与稳定性** | Hermes（profile 切换/会话加载 P1 缺陷群）、Pi（JSONL 尾部修复 #8346、压缩不触发 #8328）、Temporal（Worker Deployment 版本删除死锁 #11539） | 长会话的崩溃恢复、压缩策略与版本生命周期管理是共同攻坚点 |
| **可观测性与运维操作化** | Temporal（成员 per-service gauges #11146、灰失败节点驱逐 #11108）、Pi（内置斜杠命令事件暴露 #8364）、LiteLLM（E2E replay 匹配键升级 #37525） | 从“能跑”到“能查、能管”，事件暴露与运维接口成为扩展生态核心诉求 |
| **UI/用户体验现代化** | LiteLLM（antd→shadcn 大规模迁移）、Pi（全屏 TUI 滚动配置 #8369、工具输出块折叠 #8344）、Hermes（Telegram/Discord 多端对齐） | 桌面/终端/Web 三端体验均在重构，为下一阶段用户增长铺路 |
| **供应链安全** | Temporal（Go 1.26.3 CVE-2026-42507 #11495）、LiteLLM（cosign 镜像签名 v1.99.0-dev.1） | 企业用户的安全合规压力正在向开源项目传导，成为发布流程的必选项 |
| **Windows 用户支持** | Pi（#7547 Windows 体验征集帖 31 评论）、Hermes（桌面端多平台） | 终端 Agent 在 Windows 下的配置陷阱、快捷键冲突是明确痛点 |

---

## 5. 差异化定位分析

| 维度 | Hermes Agent | Pi | LiteLLM | Temporal |
|------|-------------|-----|---------|----------|
| **核心定位** | 个人 AI 助手（桌面 + Telegram/Discord 多端） | 终端内原生 Agent（TUI 优先） | LLM 网关 / AI Proxy 基础设施 | 持久化工作流编排引擎 |
| **典型用户** | 桌面端个人用户、多平台消息流重度使用者 | 终端重度用户、Vim/CLI 文化开发者 | 平台团队、企业 LLM 接入治理者 | 需要长时运行/可恢复业务的工程组织 |
| **技术架构特征** | Skill/playbook 方法论沉淀（feature-parity-alignment），多端功能对齐驱动 | 深度的 TUI 扩展系统，模型/思维级别会话作用域，多 provider 适配器 | 权限模型（model access groups）、E2E record-and-replay 测试基建、Dashboard 组件库重构 | 匹配队列、Nexus 协议、Worker Deployment 版本化、时间跳跃调度 |
| **差异化优势** | 跨平台渠道覆盖广度 + 方法论固化能力 | 会话语义精细度（ephemeral 模型设置、压缩策略）+ 扩展事件透明性 | Claude Code 生态集成深度 + 企业级访问控制 | 底层可靠性工程（GC 边缘情况、schedule 修复、CVE 响应） |
| **关注重心** | 功能对齐速度、桌面端稳定性 | 长会话稳定性、模型成本准确性 | 接入兼容性、架构清理 | 生产环境鲁棒性、可运维性 |

---

## 6. 社区热度与成熟度

**活跃度分层：**

- **第一梯队 — 超高速迭代期**：**Hermes Agent** 单日 500 条 PR 更新、413 条 Issue 更新，是其余项目的数倍。但合并率仅 20.8%，且多个 P1 问题在 24 小时内新增/修复并存，属于“高压推进，边修边建”状态。
- **第二梯队 — 高迭代 + 架构整理并行**：**LiteLLM** 单日 306 条 PR 更新，在 122 条合入的同时推进 antd→shadcn 大规模迁移，体现“功能开发与架构治理并行”的成熟项目节奏；**Temporal** 80 条 PR 更新，合并率 36.3%，集中于调度与匹配可靠性，属于稳扎稳打型。
- **第三梯队 — 质量巩固阶段**：**Pi** 虽然绝对量级较小（67 条 Issue、32 条 PR），但关闭率高达 80.6% / 78.1%，且修复精准指向已确认缺陷（15 个 Bug 中有 12 个当日关闭），呈现出**“少而精、高闭合”**的收敛态，是当前生态中健康度最优的项目。

**成熟度判断：** Hermes 的 Issue/PR 巨大体量与其桌面端多 P1 缺陷并存，反映其可能处于用户规模快速扩张期；Pi 与 Temporal 的社区讨论深度（多评论长线程、生产环境故障报告）暗示其用户以专业开发者为主；LiteLLM 的 PR 积压（184 待合并）需要关注合并瓶颈。

---

## 7. 值得关注的趋势信号

1. **Claude Code 正成为 Agent 网关的“事实标准兼容层”** — LiteLLM 专门为其增加登录配置链路并集中修复其流式工具调用 Bug，Pi 的代理路由检测也专门覆盖 Claude 系列模型。对开发者：优先保证与 Claude Code 的互操作性，是进入企业级市场的有效切入口。

2. **会话级配置语义（ephemeral vs global）成为 Agent 体验的分水岭** — Pi 的 #5263（👍 13）合并表明，用户对“会话内临时修改不应污染全局配置”有强需求。这预示 Agent 产品需在设计之初区分“会话

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-20

> 数据窗口：2026-08-19 00:00 UTC 至 2026-08-20 00:00 UTC（GitHub 拉取时间戳为 2026-08-19 更新）

## 今日速览

过去 24 小时项目活跃度极高：**413 条 Issue 更新（356 条新开/活跃，57 条关闭）**、**500 条 PR 更新（396 条待合并，104 条已合并/关闭）**，单日变更总量处于近一周高位。虽然无新版本发布（最新 Release 仍为 v0.20.4 前后），但 104 条 PR 合入/关闭说明代码库仍在持续推进。今日 PR 中出现多笔针对已知 P1/P2/P3 缺陷的定向修复（如 `TERMINAL_CWD` 误报、DeepSeek 计费、工具 provider 路由），显示维护者正在系统性清理存量问题。**桌面端“profile 切换/会话加载/更新机制”仍是当前最集中的风险区**，多个 P1 级问题在 24 小时内被报告或修复。整体健康度：**中等偏上，活跃但稳定性问题积压明显**。

## 项目进展

今日合并/关闭的 PR 共 104 条，其中可见的代表性成果：

- **[#79898](https://github.com/NousResearch/hermes-agent/pull/79898)（已合并）**：新增 `feature-parity-alignment` skill，将 Telegram Feature Package（#78791）的 5×2×3 方法论沉淀为可复用 playbook，为后续 Discord、Webhook 等对齐活动提供标准剧本。
- **[#86419](https://github.com/NousResearch/hermes-agent/pull/86419)（已合并）**：新增 Discord REST v10 反应动作模块（`tools/discord_api/reactions.py`，157 行），关闭 [#86418](https://github.com/NousResearch/hermes-agent/issues/86418)，推进 Discord M3 里程碑。

其他 102 条合并/关闭的 PR 虽未在 top 列表中展示，但其分布覆盖 webhook 修复、文档更新、依赖安全约束（如 #

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-20

## 1. 今日速览

过去24小时内 Pi 项目保持**高活跃度**：共产生 67 条 Issue 更新（其中新开/活跃 13 条，关闭 54 条）和 32 条 PR 更新（其中合并/关闭 25 条，待合并 7 条）。项目今日无新版本发布，但合并了多个关键修复，涉及**模型/思维级别会话作用域**、**OpenRouter reasoning_details 往返**、**Bedrock 加密推理内容**以及**内置斜杠命令扩展可视化**等方向。社区方面，Windows 使用体验讨论（#7547）维持高热度和高关注，其余 Issue 集中在模型成本核算、超时处理、压缩策略等稳定性话题。整体来看，项目正处于密集修复与功能打磨阶段，健康度良好。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日合并/关闭的 PR 集中体现了以下进展：

- **模型/思维级别更改默认会话作用域** — PR #8356（关闭，修复 #5263）：`/model` 和思维级别更改不再写回全局默认值，避免影响未来启动设置；显式通过 `/settings` 菜单修改才会持久化。同时增强了 `/settings` 中的 "Default model" 入口。
- **OpenAI Completions reasoning_details 往返修复** — PR #8246（关闭，修复 #7994）：通过合成 OpenRouter 流复现了签名 `reasoning.text`/`reasoning.summary` 被丢弃的问题，修复后 assistant 消息级 `reasoning_details` 得以保留。
- **Anthropic 降级成本计算修复** — PR #8352（关闭，修复 #8319/#8285）：降级后返回的模型（如 `claude-opus-4-8`）不再按被拒的原始请求模型（如 `claude-fable-5`）计价。
- **为七个 API 适配器添加 Pi 默认 User-Agent** — PR #8361（关闭，修复 #8305）：覆盖 openai-responses、openai-completions、anthropic-messages、azure-openai-responses、google-generative-ai、google-vertex、mistral-conversations。
- **内置斜杠命令事件可见性** — PR #8365/#8366（关闭，对应 Issue #8364）：为 `/share`、`/export`、`/settings` 等内置命令发出 `input` 事件，扩展获得零可见性缺口被填补。
- **全屏模式滚轮滚动行数可配置** — PR #8369（关闭）：新增全屏 TUI 鼠标滚轮滚动行数设置，解决 Termius 等终端快速滚动失效问题。
- **npm 包更新检查尊重 min-release-age** — PR #8377（关闭）：`getLatestNpmVersion` 不再使用忽略 `min-release-age` 截断的 `npm view <spec> version --json`，更新提示更准确。
- **fork 前先中止活动 run** — PR #8374（关闭）：fork 选择器在活动 agent run 仍在执行或重试休眠时可能产生竞态，现在会先 settle 再 fork。
- **Bedrock 加密推理内容往返** — PR #8314（关闭）：支持 Bedrock Converse 返回的 `redactedContent` 加密推理内容。
- **恢复状态从 record 查询推导** — PR #7784（关闭）：移除 recovery 专用查询 API（如 `findOpenOperations()`），通过有界 `findRecords()` 调用推导恢复状态，简化 SQLite 操作查询路径。
- **流启动时暴露工具元数据** — PR #7953（关闭）：在 JSON/RPC `toolcall_start` 事件中包含固定大小 `id` 和 `toolName` 字段，同时移除累积的 `message`/`partial` 快照，保持流大小线性增长。
- **代理/网关路由下 DeepSeek reasoning_content 检测** — PR #8359（关闭）：通过 LiteLLM、opencode zen 等代理访问 DeepSeek 时也能正确识别 `reasoning_content`。
- **未终止会话尾部修复** — PR #8346（待合并，修复 #8345）：检测并修复 JSONL 会话文件损坏/未终止尾部，加载时保持只读，追加前完成修复。

同时，TUI 视觉行缓存优化、Amazon Bedrock Mantle 新 provider 支持等 PR 也在推进中。

## 4. 社区热点

- **[#7547] [Windows] [sink-thread] How do you use Pi on windows? What issues are you seeing?**（31 评论，👍 1）— 作者 @petrroll 发起 Windows 使用体验征集，讨论 Windows 上运行 Pi 的多种方式及痛点，是当前社区最活跃的讨论线程。反映了 Pi 希望系统性收集 Windows 用户反馈、确定精力投放方向的意图。链接：https://github.com/earendil-works/pi/issues/7547

- **[#5263] Make in-session model and thinking-level changes ephemeral by default**（11 评论，👍 13）— 社区高赞需求，希望 `/model` 和思维级别更改仅影响当前会话，全局默认值只在 `/settings` 中显式修改。今日 PR #8356 已合并，该需求落地。链接：https://github.com/earendil-works/pi/issues/5263

- **[#3200] Support video/audio content in prompt command**（9 评论，👍 5) — 扩展 `prompt` RPC 命令以支持视频/音频内容传递给多模态模型。目前仅支持 `images`，用户希望跟进 Gemma 4、GPT-4o 等模型能力。链接：https://github.com/earendil-works/pi/issues/3200

## 5. Bug 与稳定性

按严重程度排列：

**高严重度**

- **[#8323] OpenAI client created with no timeout**（关闭）— `createClient` 未设置 `timeout`，回退到 OpenAI SDK 600 秒默认值，本地模型思考超过 10 分钟会被切断。影响自托管模型用户。（无独立 fix PR，属于新增 Bug）链接：https://github.com/earendil-works/pi/issues/8323

- **[#7855] Pi stops with "Response was truncated before completion."**（关闭）— 任何 OpenAI 兼容 API 随机出现响应截断错误，需手动提示继续。VLLM 本地环境复现。链接：https://github.com/earendil-works/pi/issues/7855

- **[#7829] Invalid settings.json silently ignored; misleading 'bash not found' error on Windows**（关闭）— Windows 路径中未转义反斜杠导致 settings.json 成为无效 JSON，但 Pi 静默忽略并给出误导性的 "bash not found" 错误。对 Windows 用户不友好。链接：https://github.com/earendil-works/pi/issues/7829

**中严重度**

- **[#8337] UTF-8 BOM breaks frontmatter parsing and settings.json loading**（关闭）— UTF-8 BOM 导致 frontmatter 解析失败，`normalized.startsWith("---")` 检查不通过；settings.json 加载同样受影响。链接：https://github.com/earendil-works/pi/issues/8337

- **[#8328] Threshold compaction never fires for zero-usage providers**（关闭）— OpenAI 兼容 provider 不返回 `usage` 块时，阈值压缩永远不会触发，会话可能无限增长。链接：https://github.com/earendil-works/pi/issues/8328

- **[#8322] isRecoverableLength misses exact-limit truncation**（关闭）— `usage.output < desiredMaxOutput` 应为 `<=`，当模型恰好达到 `max_output_tokens` 时误判为不可恢复。链接：https://github.com/earendil-works/pi/issues/8322

- **[#8321] streamSimple drops timeoutMs**（关闭）— `streamSimple` 构建内部流选项时遗漏 `options.timeoutMs`，导致超时设置不生效。链接：https://github.com/earendil-works/pi/issues/8321

- **[#8245] `after_provider_response` never fires on Google Generative AI**（关闭）— Google Generative AI 传输层未调用 `onResponse`，文档声明与实际行为不符。链接：https://github.com/earendil-works/pi/issues/8245

**低严重度**

- **[#8121] Getting error 429 Too Many Requests when logging in with Github Copilot**（关闭）— 即使 0.84.2 声称修复，用户仍遇到 429 错误，需手动 workaround。链接：https://github.com/earendil-works/pi/issues/8121

- **[#7994] reasoning_details round-trip only supports encrypted entries**（关闭）— 870 次试验基准揭示 OpenRouter 三 API 表面的往返问题，已由 #8246 修复。链接：https://github.com/earendil-works/pi/issues/7994

- **[#8285] Anthropic fallback usage is priced with the requested model**（关闭）— 降级后仍按请求模型计价，已由 #8352 修复。链接：https://github.com/earendil-works/pi/issues/8285

- **[#8336] glm-5.3 zai catalog entry makes thinking levels a no-op**（关闭）— 目录条目缺少 `thinkingLevelMap` 和 `supportsReasoningEffort: false`，思维级别选择器形同虚设。链接：https://github.com/earendil-works/pi/issues/8336

## 6. 功能请求与路线图信号

- **按作用域配置模型选择持久化**（#8376，关闭/未定型）— 提出 `modelSelectionScope` 设置，支持 `session`/`directory`/`global` 三级作用域。与 #5263 的会话作用域方向一致，可能被纳入后续版本。链接：https://github.com/earendil-works/pi/issues/8376

- **暴露扩展上下文中的 navigateTree()**（#5932，开放）— 用户正在实现自定义 `/goal`，需要 `ExtensionContext` 上暴露 `navigateTree()`（目前仅在 `ExtensionCommandContext` 上）。功能性需求，实现成本低，可能被采纳。链接：https://github.com/earendil-works/pi/issues/5932

- **按模型配置压缩设置**（#8133，开放）— 提议 `compaction.profiles` 映射，按模型 ID 设置不同 `reserveTokens`。对混合使用大/小模型的用户有价值。链接：https://github.com/earendil-works/pi/issues/8133

- **全屏 TUI 工具输出块独立展开/折叠**（#8344，关闭/未定型）— 点击单个工具输出块切换展开/折叠，保留 `Ctrl+O` 全局操作。改善长会话的浏览体验。链接：https://github.com/earendil-works/pi/issues/8344

- **内置斜杠命令执行前发出事件**（#8364，关闭）— 已由 PR #8365/#8366 实现，扩展获得 `/share`、`/export` 等命令的可见性。链接：https://github.com/earendil-works/pi/issues/8364

- **扩展检测排队中的自定义继续指令**（#8349，开放）— 扩展无法检测 `agent_end` 期间排队的自定义 continuation，影响扩展编排能力。链接：https://github.com/earendil-works/pi/issues/8349

- **等待用户输入状态暴露**（#5329，开放）— 主机集成需要区分"agent 正在运行"与"agent 正在等待用户输入"，cmux bridge 是典型场景。已有 PR #8355 添加 `ui_prompt_start`/`ui_prompt_end` 事件，实现中。链接：https://github.com/earendil-works/pi/issues/5329

- **prompt 命令支持视频/音频**（#3200，开放）— 多模态模型能力扩展需求，涉及 RPC 接口设计。链接：https://github.com/earendil-works/pi/issues/3200

- **内置 --profile 支持隔离 Pi 状态**（#3966，关闭）— 通过 `--profile` 实现独立 auth/sessions/settings/models/extensions 隔离。对多项目管理有实际需求。链接：https://github.com/earendil-works/pi/issues/3966

- **steering message 可选择不唤醒 agent**（#5895，关闭）— 允许发送只在 agent 仍在工作时才追加的 steering message。链接：https://github.com/earendil-works/pi/issues/5895

## 7. 用户反馈摘要

- **Windows 生态是明确的痛点**（#7547、#7829、#8372、#8183）— 开发者大量反馈 Windows 下运行 Pi 的配置陷阱、终端快捷键冲突（如 Windows Terminal 的 `Ctrl+Shift+F` 与全屏搜索冲突）、路径转义导致配置静默失效等问题。用户期待 Pi 官方针对 Windows 场景给出系统性的文档和修复，而非逐个特判。

- **会话级模型/思维设置是刚需**（#5263，👍 13）— 用户对 "`/model` 更改意外影响全局配置" 感到困扰，希望默认行为是 ephemeral，只有显式修改默认值才持久化。该需求今日已通过 PR #8356 合并，预计下一版本可用。

- **长会话稳定性是核心关切**（#7855、#8328、#8322）— 用户报告响应截断、压缩不触发、长度判断边界错误等问题，直接影响长时间编码任务的连续性。多个修复 PR 已合并，反馈积极。

- **扩展生态透明度不足**（#8364、#8349、#5932）— 扩展作者反馈内置命令、排队继续指令、UI 提示状态等事件对外不可见，限制了自定义集成能力。项目正通过事件系统逐步开放这些接口。

- **成本计算准确性受关注**（#8285、#6509）— 降级模型计价错误和扩展外部 LLM 调用的费用展示需求，反映用户对成本透明度的重视。

## 8. 待处理积压

- **[#7547] Windows 使用体验征集贴**（开放，31 评论）— 讨论量大但尚未形成明确的行动项。建议维护者整理反馈清单，标记可执行项并分配责任人。链接：https://github.com/earendil-works/pi/issues/7547

- **[#3200] prompt 命令支持视频/音频**（开放，创建于 2026-04-15，4 个月未关闭）— 多模态模型需求明确，但尚无 PR。建议评估实现成本并规划到路线图。链接：https://github.com/earendil-works/pi/issues/3200

- **[#5932] ExtensionContext 暴露 navigateTree()**（开放，创建于 2026-06-21）— 功能性 API 缺口，实现成本低，但长期未处理。链接：https://github.com/earendil-works/pi/issues/5932

- **[#5329] 暴露等待用户输入状态**（开放，👍 9）— 已有 PR #8355 覆盖 `ui.select`/`ui.confirm`/`ui.input` 等场景，但 Issue 尚未关闭，建议跟踪 PR 合并后验证并关闭。链接：https://github.com/earendil-works/pi/issues/5329

- **[#8133] 按模型配置压缩设置**（开放，👍 1，创建于 202

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报（2026-08-20）

## 1. 今日速览

LiteLLM 作为开源 AI Gateway / Proxy 项目，今日保持高强度迭代：过去 24 小时共产生 72 条 Issue 更新（新开/活跃 53 条、关闭 19 条）和 306 条 PR 更新（待合并 184 条、已合并/关闭 122 条），并发布 1 个预发布版本。社区侧呈现两个明显热点：一是 Claude Code 与 Anthropic `/v1/messages` 流式翻译相关的工具调用 Bug 集中爆发（`#37273`、`#37031`）；二是 UI 大规模弃用 antd、向 shadcn 组件库迁移的重构 PR 批量提交，说明项目正在为下一阶段 Dashboard 架构做清理。整体活跃度处于高位，Issue 关闭率约 26%（19/72），PR 合并/关闭率约 40%（122/306），项目健康度良好。

## 2. 版本发布

- **[v1.99.0-dev.1](https://github.com/BerriAI/litellm/releases)**（预发布版）
  - 当前 release notes 的核心内容是 Docker 镜像签名说明：所有 LiteLLM 镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 签名，签名密钥自 commit `0112e53` 起保持一致。意味着后续每次发布都可按官方指引验证镜像完整性，降低供应链风险。
  - 变更与迁移注意事项：该版本为 `v1.99.0` 系列首个 dev 版，notes 中**未列出具体功能变更清单**，因此暂无可确认的破坏性变更。建议生产环境用户等待正式版 v1.99.0 发布，或至少评估 dev 版稳定性后再升级。验证镜像签名的具体命令与流程参照 Sigstore cosign 官方文档即可。

## 3. 项目进展

过去 24 小时共有 122 个 PR 被合并/关闭，184 个 PR 停留在待合并状态。从已关闭的 PR 可以看出，项目在**权限模型、CLI 体验、测试基建**三个方向有明确推进：

- **访问控制修复**：[#37492 fix(auth): resolve bare model names against wildcard deployments in model access groups](https://github.com/BerriAI/litellm/pull/37492)
  修复了 access group 配置 `openai/*` 时，裸模型名无法匹配的问题——此前管理员必须在每次调用前缀 `openai/`，本次统一了 group lookup 与 routing 共用的 pattern helper，消除该不一致。
- **CLI 补全 Claude Code 配置链路**：[#37507 feat(cli): add `lite login --config-claude` to wire Claude Code at login](https://github.com/BerriAI/litellm/pull/37507)
  解决了 Claude Code 用户每次登录后需手动改写 `~/.claude/settings.json` 的问题，并修复了 `lite up` 写入的 apiKeyHelper 格式错误。将 Claude Code 接线收拢进登录动作，属于对 Agent 生态开发者体验的明显补强。
- **测试基建升级**：[#37525 feat(e2e): canonical content-based match keys for record-and-replay](https://github.com/BerriAI/litellm/pull/37525)
  E2E replay 测试由“按 verb + path + 录制顺序匹配”升级为“基于规范化内容的匹配键”，修复了请求体变化时静默回放陈旧响应、以及独立调用乱序导致 replay 失败的隐患。
- 其余 119 个合并/关闭的 PR 未在 Top 列表展开，但考虑到 184 个待合并 PR 仍大量堆叠，项目短期内合并压力不小，值得关注。

## 4. 社区热点

今日讨论热度集中在模型接入、密钥安全与 Claude Code 工具调用三

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

## Temporal 项目动态日报 — 2026-08-20

---

### 1. 今日速览

过去 24 小时，Temporal 项目社区活跃度较高：共产生 22 条 Issue 更新（新开/活跃 20 条，关闭 2 条）和 80 条 PR 更新（待合并 51 条，已合并/关闭 29 条）。无新版本发布。PR 流动量大且每日新增提交密集，说明当前正处于密集迭代期；Issue 侧讨论多聚焦于成员管理、Nexus 协议和版本部署等长期主题，整体项目健康度良好。

---

### 3. 项目进展

今日关闭/合并的 PR 数量为 29 条，主要覆盖调度、匹配和稳定性修复。以下是值得关注的已关闭 PR：

- [**matching: resume gc after acks that land during an in-flight gc pass**](https://github.com/temporalio/temporal/pull/11389)  
  修复匹配服务在 GC 进行期间收到 ack 时可能跳过后续 GC 的边缘情况，提升匹配队列清理的可靠性。

- [**edge case fixes for time skipping propagation and fast-forward completion**](https://github.com/temporalio/temporal/pull/11373)  
  修复了 fast-forward 完成时间早于 `ms.Now()` 时时间跳跃未正确关闭的边界问题，并改进了相关传播逻辑，提升调度正确性。

另有大量 PR 处于开放但活跃推进状态，例如：
- [**admin-batch-1: run admin batch in temporal-system**](https://github.com/temporalio/temporal/pull/11509)：将批量管理操作迁移至系统命名空间，提升跨命名空间操作隔离性。
- [**Fix schedule action delay after refresh**](https://github.com/temporalio/temporal/pull/11588)：修复刷新后调度动作延迟问题，依赖 #11652，属于 Scheduler V1 工作流改进系列。

---

### 4. 社区热点

今日讨论最活跃的 Issue（评论数相对最多）集中在以下几条：

- [**Membership: emit per-service reachable/available/draining member gauges**](https://github.com/temporalio/temporal/issues/11146)（3 条评论）  
  用户 @wankhede04 在调查滚动重启期间请求路由到 draining/stopping 成员的问题（#10730）时，发现成员包缺少按服务的可达/可用/排空指标，期望补充可观测性。隐含诉求是：**提升成员状态的可观测性，帮助运维人员定位路由异常**。

- [**DeleteWorkerDeploymentVersion fails permanently when a version summary outlives its version workflow**](https://github.com/temporalio/temporal/issues/11539)（3 条评论）  
  用户遇到 Worker Deployment 版本无法删除的问题，导致 `maxVersionsInDeployment` 被撑满、新版本无法注册。这直接阻塞版本部署流程，是部署实践中的关键痛点。

- [**Membership: provide an operator-facing way to evict a "gray-failed" host**](https://github.com/temporalio/temporal/issues/11108)（2 条评论）  
  生产环境出现 History 节点磁盘故障进入“灰失败”状态后，无法通过带内机制将其从成员环中驱逐，只能人工干预。诉求明确：**需要 operator 可操作的驱逐命令或 API**。

另外，PR 方面今日新开的 [**Support MySQL multi-host and SRV connections**](https://github.com/temporalio/temporal/pull/11659) 也获得一定关注，展示了社区对部署灵活性的需求。

---

### 5. Bug 与稳定性

以下为今日报告/活跃的 Bug，按严重程度排列：

| 严重程度 | Issue | 描述 | 是否有 Fix PR |
|---------|-------|------|--------------|
| 🔴 严重 | [#11495](https://github.com/temporalio/temporal/issues/11495) | Go 1.26.3 受 CVE-2026-42507 影响（net/textproto 漏洞），需升级至 1.26.4 | 无对应 PR，仅 Issue 建议 |
| 🔴 严重 | [#11188](https://github.com/temporalio/temporal/issues/11188) | History 队列 pending task 数超阈值触发 mitigation 时，特定竞态下服务直接 fatal crash | 暂无 |
| 🔴 严重 | [#11402](https://github.com/temporalio/temporal/issues/11402) | `RegisterWorkerInVersion` task 丢失后，该 task queue 的 activity dispatch 被永久禁用 | 暂无 |
| 🟠 中高 | [#11547](https://github.com/temporalio/temporal/issues/11547) | 短暂的 `Unavailable` 错误会重置 History 队列 backoff，造成持续重试风暴，冲击持久化 QPS | 暂无 |
| 🟠 中高 | [#11539](https://github.com/temporalio/temporal/issues/11539) | `DeleteWorkerDeploymentVersion` 在版本 summary 存活时间超过对应 workflow 时永久失败 | 暂无 |
| 🟠 中高 | [#11600](https://github.com/temporalio/temporal/issues/11600) | UpdateWithStart 中 `ExecutionState.Status` 在 workflow 锁释放后被读取，存在数据竞争（已关闭） | 已关闭，未明确是否修复 |
| 🟡 中 | [#11569](https://github.com/temporalio/temporal/issues/11569) | Nexus 服务端可能发送格式非法的 `request-timeout` header（负值、非规范单位） | 暂无 |
| 🟡 中 | [#11594](https://github.com/temporalio/temporal/issues/11594) | PostgreSQL visibility v1.14 schema 升级未纳入 v1.10–v1.13 的优化重写逻辑，升级效率低 | 暂无 |
| 🟡 中 | [#11571](https://github.com/temporalio/temporal/issues/11571) | 持久化 rate-limit 的 `ResourceExhausted` 在 `ProcessOutgoingSearchAttributes` 中退化为 `Unavailable` | 暂无 |
| 🟢 较低 | [#11230](https://github.com/temporalio/temporal/issues/11230) | 客户端 TLS 配置无法自动感知 root CA 刷新，需重启进程才生效 | 暂无 |
| 🟢 较低 | [#11429](https://github.com/temporalio/temporal/issues/11429) | K8s Pod 重启后，healer/worker 仍探测旧的 Pod IP | 暂无 |

---

### 6. 功能请求与路线图信号

以下功能请求反映了社区的主要诉求，结合已有 PR 可推测其在路线图中的优先级：

- [**Add a built-in Kubernetes service account ClaimMapper**](https://github.com/temporalio/temporal/issues/11607)（新开，2026-08-18）  
  用户希望在 `authorization.claimMapper` 中直接选择内置的 Kubernetes Service Account 映射器，无需自定义二进制。该能力将大幅降低 K8s 自托管用户的门槛，属于**高价值、中成本**功能，值得纳入下一版本规划。

- [**Replace LeveledCompactionStrategy with UnifiedCompactionStrategy (Cassandra 5.x)**](https://github.com/temporalio/temporal/issues/11314)  
  建议将 Cassandra schema 中默认压缩策略迁移至 UCS，以适配 Cassandra 5.x 默认行为。属于基础设施现代化方向，可能需要兼容性评估。

- [**Migrate Cassandra driver from gocql v1.7.0 to apache/cassandra-gocql-driver/v2**](https://github.com/temporalio/temporal/issues/11124)  
  依赖升级请求，跟随后端生态演进，涉及面广、风险中等，属常见技术债清理。

- [**Emit per-service member gauges**](https://github.com/temporalio/temporal/issues/11146)  
  成员状态可观测性增强，与 #11108（驱逐灰失败节点）形成系列，可能是成员管理模块的下一个改进方向。

- 新 PR [**Support MySQL multi-host and SRV connections**](https://github.com/temporalio/temporal/pull/11659)  
  提升 MySQL 持久化的高可用和连接灵活性，属于部署体验改进，可能跟随下一版本合并。

---

### 7. 用户反馈摘要

从 Issue 描述中提炼出的用户真实声音：

- **生产事故痛点**：用户 @soohunee 在 [#11108](https://github.com/temporalio/temporal/issues/11108) 中详细记录了 K8s 节点磁盘故障导致的 History 节点灰失败经历，最后只能靠删除 Pod 恢复。反馈核心：**缺少带内驱逐手段**，希望 Temporal 提供 operator 可执行的驱逐命令。

- **部署持续受阻**：用户 @noamyehudai 在 [#11539](https://github.com/temporalio/temporal/issues/11539) 中报告 Worker Deployment Version 无法删除，导致 `matching.maxVersionsInDeployment` 被占满，**新版本无法注册**。这是版本管理流程中的“死锁”场景，影响 CI/CD 自动化。

- **集群稳定性担忧**：用户 @ggbata 在 [#11547](https://github.com/temporalio/temporal/issues/11547) 中描述了由短暂 `Unavailable` 引发的重试风暴，将原本均衡的负载因 backoff 重置变成脉冲式 QPS 峰值，**表达了对集群在高负载下鲁棒性的担忧**。

- **安全合规压力**：两个独立用户（@Anuj8109、@antigravity-sketch）分别提交了 Go 工具链 CVE 和 AWS Inspector 漏洞报告，反映出**企业用户对镜像安全扫描和合规的强要求**。

- **UI 权限误伤**：用户 @robertpenz 在 [#11639](https://github.com/temporalio/temporal/issues/11639) 中反馈 namespace-scoped admin token 无法打开 Web UI，属于权限模型边界不清晰的问题，影响日常管理体验。

---

### 8. 待处理积压

以下为创建时间较长但仍未关闭或未合并的重要 Issue / PR，建议维护者重点关注：

| 类型 | 项目 | 创建时间 | 状态 | 备注 |
|------|------|----------|------|------|
| Issue | [#11124](https://github.com/temporalio/temporal/issues/11124) Cassandra 驱动迁移 | 2026-07-17 | 开放，1 评论 | 技术债，影响后续 Cassandra 版本支持 |
| Issue | [#11108](https://github.com/temporalio/temporal/issues/11108) 灰失败节点驱逐 | 2026-07-16 | 开放，2 评论 | 生产环境痛点，建议优先规划 |
| Issue | [#11146](https://github.com/temporalio/temporal/issues/11146) 成员 gauges |

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*