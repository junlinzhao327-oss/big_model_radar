# OpenClaw 生态日报 2026-08-07

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-06 22:35 UTC

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

## Hermes Agent 项目动态日报 — 2026-08-07

### 1. 今日速览

过去 24 小时项目活跃度极高，Issue 与 PR 更新均达 500 条，其中新开/活跃 Issue 474 条、待合并 PR 388 条，说明社区反馈与贡献者提交均处于高峰状态。两个高热度讨论线程值得关注：输出截断 Bug（#7237，54 条评论）以关闭告终，而仓库级 god-file 分解 Epic（#78647，42 条评论）正吸引大量架构讨论。整体来看，项目正处于一次大规模代码结构重构（god-file sharding）与稳定性修复并行推进的阶段，桌面端问题（权限、进程泄漏、渲染性能）占比显著，是当前最集中的用户痛点；今日无新版本发布，但 112 条 PR 已合并/关闭，合并流转效率良好。

---

### 2. 版本发布

今日无新版本发布（Releases 为 0 个），故省略。

---

### 3. 项目进展

过去 24 小时共有 112 条 PR 被合并/关闭，以下为可追踪的重要合入与闭环：

- **[合并] feat: 会话守卫 Session Guard Context Engine v1.0（#76128）** — 新增会话守卫插件，在上下文压缩达上限时强制提醒用户总结并新建会话，针对嵌套摘要偏差与 token 浪费问题。涉及会话状态与压缩链路，需关注后续兼容性反馈。
- **[关闭] refactor(gateway): 提取 46 个斜杠命令处理器至独立包（#71444）** — 该 PR 此前为草稿状态，今日关闭；但已由新 PR **#80617**（re-port 至最新 main）接力推进。
- **[关闭] Tracking: 核心工具集性能批次——terminal & file-ops 轮次效率（#77056）** — 追踪 12 个 PR 的性能改进批次上线，涵盖减少无效工具轮次、错误信息去模糊化、schema 精简等工作。
- **[新增] 其他值得关注的待合并 PR**（未合入，但体现实质进展）：`fix(agent): bound synchronous Relay execution`（#79780，修复工具永不 resolve 导致会话永久卡死）、`fix(delegation): honor pinned delegation.provider`（#80465，修复委派模型 pin 被父级 fallback 链静默替换）、`fix(gateway): classify provider-resolution failures`（#80587，不再将配额用尽误报为认证失败）、`fix(cli): exec env-shebang relaunch scripts`（#80580，修复 git 安装恢复会话崩溃）。

整体而言，项目在会话状态安全、错误分类准确性、CLI 健壮性三个方向上有明显推进；god-file 分解进入批量执行阶段（详见下文）。

---

### 4. 社区热点

今日讨论最活跃的 Issue/PR 及其背后诉求：

- **[#7237] Error: Response truncated due to output length limit（CLOSED，54 评论，👍 7）** — Hermes Agent 在 CLI chat 与 Telegram/Discord/Slack 网关中生成长文时频繁中途截断并抛错。这是网关用户最直接的使用障碍，评论数高企说明受影响面广；该 Issue 今日关闭，但需确认修复已随代码发布。
- **[#78647] Epic: Shard all 20 god files — 仓库级 god-file 分解（OPEN，42 评论）** — 由 @andrexibiza 发起，宣布 2026-08 起“所有 god file 必须拆分、不得回退”的仓库政策。配套大量 `Shard xxx.py` 子 Issue（#78636、#78645、#78637、#78632、#78635 等），是该仓库当前最大的架构治理工程，社区关注度高。
- **[#25267] Claude Agent SDK model provider with subscription OAuth（OPEN，👍 48，16 评论）** — 用户希望在 Claude 订阅（Max/Pro）下使用 Hermes，而不必额外支付 per-token API 费用。48 个 👍 说明这是社区强烈需求；同族 Issue #40014 已关闭，但 OAuth 路由问题仍存在（见下文 Bug 部分）。
- **[#7545] Bang（!）前缀在 chat 输入中内联执行 shell 命令（CLOSED，👍 14）** — 类似 Claude Code 的 `!ls` 快捷方式，今日关闭，建议核实是已实现还是被拒绝，关闭原因未在数据中呈现。

---

### 5. Bug 与稳定性

按严重程度排列（P1 最高）：

- **[P1] TUI /sessions 与 /models 覆盖层不可见（#69592）** — 加载 ambient widget dock 后，会话恢复与模型切换功能完全不可用，且 `/reload` 静默失败。Issue 更新提及“Day 13”，已持续近两周，社区耐心受到考验。**暂无对应 fix PR 出现。**
- **[P1] send-path 修复意外改写持久化历史（PR #80616）** — `_canonicalize_api_tool_calls` 承诺 copy-on-write，但实际会污染持久化会话历史，属数据完整性风险，正在审查中。
- **[P2] 全盘文件访问权限在每次 Desktop 更新后被撤销（#52010）** — macOS FDA 权限需手工重新授予，与已存在的 Accessibility 问题（#43365、#43788）不同，属于独立权限类别。**暂无 fix PR，但频发更新场景下影响较大。**
- **[P2] xAI grok-4.5 'Invalid PNG image' 400 永久锁死会话（#69078）** — 一次性图片错误导致会话所有 API 调用（包括纯文本）失败，恢复仅能删除会话，用户数据不可找回。已有针对类似问题（#25837）的 matcher，但该变体未被覆盖。**暂无 fix PR。**
- **[P2] vi/Desktop 更新后 read_file 将合法 UTF-8 文本误报为二进制（#76886）** — 0.19.1 回归，1000 字节采样点恰好切断多字节字符导致误判。影响 Obsidian 笔记用户。**暂无 fix PR。**
- **[P2] lifecycle_guard 因 `ValueError: embedded null byte` 崩溃（#77780，CLOSED）** — 终端命令扫描时异常未被捕获，直接阻断所有终端命令；今日已关闭，预计修复已合入。
- **[P2] 桌面端渲染/GPU 进程空转 100%+ CPU（#73082）** — Electron renderer 与 GPU helper 在无操作时持续渲染循环，macOS 报告最高能耗；与 #53902（fontations 循环）疑似同族，均无 fix PR。
- **[P2] Windows 更新循环：updater 将自身后端识别为 venv 占用者（#77277）** — 杀掉 PID 也无济于事，因为后端持续重生，更新永远失败。

---

### 6. 功能请求与路线图信号

- **Claude 订阅 OAuth 计费打通（#25267，👍 48）** — 社区强烈回声。相关 PR #80610（headless provider OAuth PKCE）与 #80618（将 Anthropic Console spend-limit 400 重分类为 billing）已在同一领域推进，虽不直接解决订阅计费，但方向一致，值得期待下一版本。
- **多租户 Hermes（#34352）** — 用户提出 memory 操作绕过 hook 系统，多租户隔离必须 fork 核心；作者已在生产运行数月，希望官方采纳。该问题贴着 `needs-decision` 标签，目前无官方决策回复，但并发会话污染问题（#46303）持续加重诉求。
- **可配置有界 auto-continue（#16004）** — 当达到最大 tool-call 迭代次数时，允许配置自动继续而非强制人类介入，适合 ACP/VS Code 与长会话网关场景。暂无对应 PR，但有 `needs-decision` 标记。
- **xAI/Grok 功能对齐 Campaign（#80424）** — 元 Issue 汇总 xAI 平台功能对齐诉求（推理、流式、Imagine 图像、Voice/TTS 等），与 @andrexibiza 发起的 god-file 分解形成两个并行运动。
- **桌面端可激活式 Profiles + 自包含安装器（PR #80613 + #79599）** — 前者允许选择下次启动激活的 profile，后者将安装器打包为完全离线、单文件自包含产物，对应部署领域长期被抱怨的首次启动下载问题。
- **Bang（!）命令已关闭（#7545）** — 若为已实现，则 CLI 交互体验对标 Claude Code 的能力将补上；若为拒绝，建议维护者明确回复原因，避免重复提案。

---

### 7. 用户反馈摘要

- **截断错误让长文用户沮丧**（#7237）：用户报告生成稍长内容就被 `Response truncated` 打断，且无法强制继续，中文/Heredoc 等长格式场景尤其明显。
- **桌面更新割让权限，安全与便利冲突**（#52010）：用户明确区分 FDA 与 Accessibility/Microphone 问题，希望更新流程保留权限而非强制重授权，否则每次更新都需要手动进入系统设置。
- **会话永久损坏导致数据丢失**（#69078）：xAI 一次图片解析失败就让整个会话“永远无法使用”，即使重启网关也不行，只能删除会话；用户强调源图片已验证有效，是服务端/客户端匹配问题。
- **TUI 用户耐心逼近极限**（#69592）：更新中明确标注“Day 13”，两个核心工作流（/sessions、/models）持续不可用，`/reload` 也不生效；这是长期回归问题，用户情绪偏负面。
- **性能回退影响日常使用**（#76886）：更新后 Obsidian 笔记无法打开，用户原以为是文件损坏，“turned out it isn't the files”——是 1000 字节采样的多字节边界问题，用户对回归原因表示困惑。
- **Windows 更新死循环**（#77277）：用户尝试手动杀 PID 仍失败，因为 app 后端不断重生，“Update aborted: another Hermes process is using this installation” 报错极具误导性。
- **进程泄漏是桌面端系统性问题**（#67026、#58619）：47 个僵尸进程、serve 进程以每 15-30 分钟一个的速度堆积，用户担心内存耗尽与能耗。

---

### 8. 待处理积压

- **[P1] TUI /sessions 与 /models 覆盖层不可见（#69592，13+ 天未修复）** — 核心交互功能长时间不可用，且唯一的 workaround（卸载 ambient widgets）与文档推荐模式冲突，建议维护者优先响应。
- **[P1] xAI 会话永久锁死（#69078，17 天未解决）** — 用户数据不可恢复的严重问题，等待错误匹配逻辑补全。
- **[P2] macOS 全盘访问权限每次更新被撤销（#52010，已开放 44 天）** — 高频率更新 + 强制手工授权，属于桌面端体验的重大阻碍，需要安装器层面解决。
- **[P2] 多租户隔离问题（#34352，已开放 70 天）** — 生产级用户已自行 fork 修复，官方 `needs-decision` 尚无结论；此问题直接影响企业采用决策。
- **[P2] 桌面端 zombie serve 进程堆积（#67026、#58619，分别已开放 20/33 天）** — 同一根因（serve 无 `--replace` 语义）的重复报告，建议将 `--replace` 标志纳入近期规划。
- **[P1] 并发会话内存与 git worktree 交叉污染（#46303，已开放 54 天）** — 涉及数据隔离与安全边界，且与多租户 Issue 相互印证需求迫切性。
- **[P3] god-file 分解系列（#78647 及 6 个追踪子 Issue）** — 虽为 P3，但已升级为仓库政策（2026-08），若长期无对应 PR 合入，社区对治理透明度的信任会受损；目前仅有 #80617（gateway slash_commands）与 #80620（auth_remote_session）两个相关 PR 支撑。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目日报 — 2026-08-07

## 1. 今日速览

过去24小时项目活跃度极高：**280条PR更新**（其中94条已合并/关闭）、**64条Issue更新**（37条新开/活跃，27条关闭）表明项目正处在密集迭代期。尽管当日无新版本发布，但一个值得注意的信号是**PR #36057「promote staging to main」**已开出，意味着项目团队正在准备新的开发版本。PR集中在**UI/playground重构**（#36128-36134系列）与**OTEL追踪链路**（#35514/#35515）两大主题，同时**v1.95.0的多个成本与流式回归问题**（#36094、#36083、#36016）成为社区主要抱怨点。总体而言，项目处于快速演进阶段，但近期版本引入的回归问题需引起维护团队重视。

---

## 2. 版本发布

**今日无新版本发布。** 但注意到 [#36057 [OPEN] chore: promote staging to main](https://github.com/BerriAI/litellm/pull/36057) 已提交，描述为 "We're cutting a new dev release for @tin-berri to give to client and get feedback"——预示新开发版本即将发布，值得关注。

---

## 3. 项目进展

今日合并/关闭的PR中，以下对项目推进较为关键：

- **[#35384 [已合并] fix(model_management): stop persisting model cost map pricing as a deployment override](https://github.com/BerriAI/litellm/pull/35384)** — 修复「UI中保存模型时会将价格映射固化为部署覆盖值」的问题，使`litellm_params`成为定价的唯一事实来源。解决了Reload Price Data后价格不更新、清空价格后重新保存又恢复的顽固bug，属于模型管理核心链路的稳定性改进。

- **[#36118 [已合并] feat(proxy): add experimental LiteLLM Headroom gateway](https://github.com/BerriAI/litellm/pull/36118)** — 新增了一个可选的LiteLLM网关，置于本地Headroom代理之前，保留现有的直接Headroom路径作为回退。通过loopback-only ASGI网关提供健康检查和就绪检查端点，同时保持Codex响应、SSE、凭据和文档兼容性。这表明项目在**扩展Codex/Headroom生态集成**方面迈出了一步。

- **[#36117 [开放] fix(ci): tell stale branches to pull latest staging on vacuous type-check runs](https://github.com/BerriAI/litellm/pull/36117)** — 改善 CI 的「空洞类型检查」失败信息，明确告诉贡献者拉取最新 staging 代码，降低开源贡献者的困惑和阻塞。

- **[#36128 [已合并] feat(ui): migrate playground chat to shadcn and fix MCP routing](https://github.com/BerriAI/litellm/pull/36128)** — 将 Playground 聊天组件从 Ant Design/Tremor 迁移至 shadcn，并修复了 MCP 工具路由问题。配合 #36129-36134 系列（Playground 迁移、MCP 工具修复、实时 Playground 重构、虚拟键模型加载），可见 **UI 重构正在进行大规模推进**，涉及约 6 个 PR 的串行/并行工作。

**总体评估**：今日合并的PR集中于模型管理修复、UI框架迁移和周边网关集成，未涉及核心LLM路由逻辑的架构性变更。项目仍处于新UI上线的收尾阶段。

---

## 4. 社区热点

今日讨论热度最高的议题分布：

### 🔥 长期置顶的愿望清单
- **[#361 [已关闭] 🎅 I WISH LITELLM HAD...](https://github.com/BerriAI/litellm/issues/361)** — 476条评论，持续至2026-08-06仍有更新。这是社区的**长期需求收集帖**，记录了用户对LiteLLM的功能期望。虽然已标记为CLOSED，但持续有互动说明该帖仍被用作需求讨论甚至情感连接的场所。

### 🔥 Python 3.14 兼容性
- **[#20933 [开放] LiteLLM Proxy fails to start on Python 3.14 due to uvloop incompatibility](https://github.com/BerriAI/litellm/issues/20933)** — 10个👍，5条评论。用户对 Python 3.14 的 uvloop 兼容性问题表现出明确关注，虽然该问题已存在近6个月，但从点赞数看这是社区普遍关心的话题。

### 🔥 成本计算回归
- **[#36094 [开放] azure/gpt-5.6-luna under-reports cost by 5x on main](https://github.com/BerriAI/litellm/issues/36094)** — 在v1.95.0之后成本计算偏差达**5倍**，且影响Azure GPT-5.6-luna主模型定价，属于直接损害用户利益的缺陷。
- **[#36083 [开放] v1.95.0 streaming usage drops cached_tokens and overcharges cached input](https://github.com/BerriAI/litellm/issues/36083)** — 流式响应中 cached_tokens 丢失导致缓存输入被超额计费，同样与成本直接相关。
- **[#36016 [开放] Inconsistent GPT-5.6 prices for Bedrock](https://github.com/BerriAI/litellm/issues/36016)** — Bedrock上的GPT-5.6定价与Azure/OpenAI不一致，272k以上的成本和模型模式缺失。

### 🔥 安全问题讨论
- **[#35664 [开放] Security - UI cookie JWT contains reusable API key material](https://github.com/BerriAI/litellm/issues/35664)** — UI认证Cookie中的JWT携带API密钥材料，可被重放用于其他会话认证，属于安全敏感问题，值得优先处理。

**分析**：社区当前情绪集中在 **「v1.95.0/1.96.0 引入的成本与流式回归」** 以及 **「GPT-5.6 系列新模型的定价准确性」** 两个方向。这两类问题直接关系到生产用户的账单和支出，因此讨论热度最高。

---

## 5. Bug 与稳定性

按严重程度排列如下：

### 🔴 高严重度

| 问题 | 描述 | 状态 |
|------|------|------|
| [#36094 azure/gpt-5.6-luna under-reports cost by 5x on main](https://github.com/BerriAI/litellm/issues/36094) | v1.95.0后Azure GPT-5.6-luna成本被低估约5倍 | 开放，暂无修复PR |
| [#36083 v1.95.0 streaming usage drops cached_tokens and overcharges cached input](https://github.com/BerriAI/litellm/issues/36083) | 流式回复重组过程中丢失 `usage.prompt_tokens_details.cached_tokens`，导致缓存输入被超额计费 | 开放，暂无修复PR |
| [#35664 UI cookie JWT contains reusable API key material](https://github.com/BerriAI/litellm/issues/35664) | UI Cookie 的JWT携带可直接重放使用的API密钥（`key` claim），另一个浏览器/会话复制后可完成认证 | 开放，安全敏感 |
| [#36121 PR: re-assert the authenticated identity on passthrough requests](https://github.com/BerriAI/litellm/pull/36121) | 透传请求体可将自身的消费与预算重定向到其他用户/团队/组织/最终用户 | **已有修复PR** |

### 🟡 中严重度

| 问题 | 描述 | 状态 |
|------|------|------|
| [#36085 Model-level guardrails not applied on /v1/messages](https://github.com/BerriAI/litellm/issues/36085) | 通过Admin UI绑定到模型的guardrails在`/v1/messages`端点不生效 | 开放 |
| [#36088 WebSocket passthrough not registered for OpenAI prefixes](https://github.com/BerriAI/litellm/issues/36088) | `/openai/*`前缀未注册WebSocket透传路由，`client.responses.connect()`不可用 | 开放 |
| [#36091 Anthropic /v1/messages bridge drops cache accounting](https://github.com/BerriAI/litellm/issues/36091) | OpenAI Responses API上游的缓存命中在Anthropic格式的usage中始终显示`cache_read_input_tokens: 0` | 开放 |
| [#35767 github copilot Reverse GPT5.6 model error](https://github.com/BerriAI/litellm/issues/35767) | v1.95.0 中 `gpt-5.6-terra` 通过 GitHub Copilot 不可用 | 开放 |

### 🟢 低严重度（已有关闭或修复）

| 问题 | 描述 | 状态 |
|------|------|------|
| [#36081 Price cuts in azure/gpt-5.6-luna and azure/gpt-5.6-terra cost map may not match actual costs](https://github.com/BerriAI/litellm/issues/36081) | 对定价地图的降价提出质疑 | 已关闭 |
| [#35958 Regression on interrupted streaming /v1/messages getting logged](https://github.com/BerriAI/litellm/issues/35958) | 中断的流式请求被记录为日志（回归） | 开放 |
| [#35800 Standalone virtual-key soft_budget alert not sent to Slack](https://github.com/BerriAI/litellm/issues/35800) | 单独虚拟密钥的`soft_budget`超限不触发Slack告警 | 开放 |

**稳定性趋势总结**：v1.95.0之后的**成本计算**（#36094、#36083、#36016）和**流式传递/计费**问题是当前主要回归来源。同时，**安全面**（#35664、#36121）的议题在最近两天集中出现，需要重视。

---

## 6. 功能请求与路线图信号

结合今日Issues与PR，以下功能信号值得关注：

### 已在开发中的功能

| 功能 | 相关PR | 状态 |
|------|--------|------|
| **Playground UI 全面重构（shadcn/Base UI）** | [#36131 shared vercel-style playground chat composer](https://github.com/BerriAI/litellm/pull/36131)、[#36129 migrate playground chat controls to shadcn](https://github.com/BerriAI/litellm/pull/36129)、[#36130 restore playground model filtering by endpoint](https://github.com/BerriAI/litellm/pull/36130)、[#36134 playground MCP across tool-capable endpoints](https://github.com/BerriAI/litellm/pull/36134)、[#36133 restyle realtime playground and fix concurrent responses](https://github.com/BerriAI/litellm/pull/36133)、[#36132 load virtual key models and show human select labels](https://github.com/BerriAI/litellm/pull/36132) | 6个PR并行开发中，作为系列栈推进 |
| **OTEL 多租户追踪** | [#35514 resolve a request's trace destinations from its identity](https://github.com/BerriAI/litellm/pull/35514)、[#35515 export the trace to the resolved destinations](https://github.com/BerriAI/litellm/pull/35515) | 开放中，按团队/组织权限路由OpenTelemetry导出目标 |
| **用户预算应用到团队密钥** | [#36102 add apply_user_budget_to_team_keys opt-in](https://github.com/BerriAI/litellm/pull/36102) | 开放中，这是#32005的重做（带opt-in标记），说明该功能需求已被多个用户提过 |
| **LiteLLM Headroom 网关** | [#36118 experimental LiteLLM Headroom gateway](https://github.com/BerriAI/litellm/pull/36118) | 已合并 |

### 潜在路线图信号

- **模型级Guardrails的Anthropic端点支持**（#36085）——用户在 `chat/completions` 能用、在 `/v1/messages` 不能用，属于一致性问题，很可能被纳入后续版本。
- **自动路由预设模型与通配符模型组匹配**（#36111）——当模型以 `anthropic/*`、`openai/*` 通配部署时，Auto Router的预设模板应能正确匹配，改善配置体验。
- **WebSocket 透传在 OpenAI 前缀的注册**（#36088）——Responses API 的 `connect()` 和实时API的WebSocket通路完善。

---

## 7. 用户反馈摘要

以下是从今日活跃 Issues/PR 评论中提炼的真实用户声音：

### 正面反馈
- 一位贡献者在 #35384（模型价格覆盖修复）的评论中对该修复表达了认可，认为清空价格后重新保存恢复预期值的逻辑更加合理。

### 痛点与不满

| 用户痛点 | 来源 | 情绪/诉求 |
|----------|------|-----------|
| **v1.95.0 后成本超收** — "streaming usage drops cached_tokens and overcharges cached input" | [#36083](https://github.com/BerriAI/litellm/issues/36083) | 成本敏感，期望尽快修复 |
| **Azure GPT-5.6 成本低估5倍** — 用户账单偏差较大 | [#36094](https://github.com/BerriAI/litellm/issues/36094) | 期望精确定价，避免预算误判 |
| **UI Cookie 安全风险** — "JWT contains reusable API key material" | [#35664](https://github.com/BerriAI/litellm/issues/35664) | 安全合规诉求 |
| **Passthrough 请求可重定向消费/预算到其他用户** — 这是严重的安全漏洞 | [#36121](https://github.com/BerriAI/litellm/pull/36121) | 修复PR已出，但尚未合并，用户等待中 |
| **Bedrock 批量推理凭证字段被静默丢弃** — "credential fields and model silently dropped"（#25104，已关闭） | [#25104](https://github.com/BerriAI/litellm/issues/25104) | 已解决，但用户等待了约4个月 |
| **max_parallel_requests 计数在中断流式请求后持续递增** — 最终所有请求都被拒绝 | [#27955](https://github.com/BerriAI/litellm/issues/27955) | 生产可用性影响大，已存在约3个月 |

### 长期积压的情绪信号
- **#20933**（Python 3.14 + uvloop 不兼容）自2026年2月报告至今未解决，获得10个👍，用户明显期待官方支持Python 3.14。
- **#29284**（Embedding缓存合并损坏 `data[*].index`）已有1个👍，影响下游客户端处理。

---

## 8. 待处理积压

以下为值得维护团队关注的重点积压项：

### ⚠️ 安全与身份问题（高优先级）

| 条目 | 持续时间 | 说明 |
|------|----------|------|
| [#35664 UI cookie JWT contains reusable API key material](https://github.com/BerriAI/litellm/issues/35664) | 4天 | 安全敏感，Cookie中携带可重放的API密钥材料 |
| [#36121 re-assert authenticated identity on passthrough requests](https://github.com/BerriAI/litellm/pull/36121) | 1天 | 透传请求可重定向消费/预算至其他用户，

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-07

## 1. 今日速览

过去 24 小时 Temporal 处于**稳定高活跃开发状态**：PR 更新 26 条，其中 20 条待合并、6 条已合并/关闭，反映出核心团队在持续推动功能开发与可靠性加固；Issue 侧仅新增 1 条（且是同一作者提交的潜在 bug 报告与修复 PR 配套出现），社区反馈量较小、无明显争议性讨论。今日无新版本发布，但已出现 1.32.0 发布分支准备 PR（#11435），预示接近版本发布节点。整体来看，项目健康度良好：修复类 PR 覆盖面广（资源泄漏、gRPC 连接释放、陈旧目标探测等），并有多个长期可靠性计划（reliability-2026）的 PR 在持续推进中。

---

## 2. 版本发布

今日无新版本发布。

> 注：PR #11435（[Prepare release branch: 1.32.0](https://github.com/temporalio/temporal/pull/11435)）已合并/关闭，表明 1.32.0 版本发布流程已启动，预计近期将正式发布。

---

## 3. 项目进展

今日可见的已合并/关闭 PR 共 5 条；从内容看，项目主要在**版本发布准备**与**系统可靠性**两个方向持续推进：

- **[#11435] Prepare release branch: 1.32.0**（[链接](https://github.com/temporalio/temporal/pull/11435)）— 由 temporal-cicd[bot] 提交，覆盖 governance 文件并更新依赖，是 1.32.0 发布前的标准 prepare release 流程，标志新版本进入发布倒计时。

- **[#11426] Gate worker deployment version demotion signals**（[链接](https://github.com/temporalio/temporal/pull/11426)）— 新增 `matching.enableWorkerDeploymentVersionDemotionSignal` 全局动态配置（OSS 默认关闭），保留 signal 路径并恢复旧版 `SyncWorkerDeploymentVersion` 更新路径，为升级提供安全切换开关，是 worker versioning 功能稳定性补强。

- **[#11376] New functional test for time skipping behavior during pause and unpause**（[链接](https://github.com/temporalio/temporal/pull/11376)）— 为 workflow 暂停/恢复期间的时间跳过行为补充端到端测试，覆盖"暂停时允许设置时间跳过配置、暂停期间不跳过、恢复后继续跳过"的时序场景，降低该能力回归风险。

- **[#11343] Health check settings for grpc endpoints**（[链接](https://github.com/temporalio/temporal/pull/11343)）— 将健康检查逻辑集中到 `health.SignalAggregator`，统一基于延迟分位数和错误比率的健康检测，是系统自愈能力的基础设施改进，后续可用于任意需健康检测的场景。

- **[#11189] Add TemporalNamespaceDivision group by column allowlist**（[链接](https://github.com/temporalio/temporal/pull/11189)）— 为 NamespaceDivision 分组添加列白名单，允许系统 workflow 跨原型聚合，扩展了可观测性维度。

此外，多个重要 PR 处于开放状态但仍在活跃推进（今日有更新），包括功能测试外部化（#11441）、backlog 感知的客户端拉取负载均衡（#11114）、replication 流最大生命周期限制（#11356）等。

---

## 4. 社区热点

今日数据中评论数均为 `undefined`，无法直接按评论量排序。但结合内容与关联性，以下两个话题最受关注：

- **[Issue #11429] 当 Temporal k8s Pod 重启后，healer 仍探测旧 Pod IP？**（[链接](https://github.com/temporalio/temporal/issues/11429)）— 用户 @fm2022aa 报告在 Kubernetes 环境下，frontend Pod 重启后 `statichosts.New(hostPorts...)` 仍持有旧 IP，导致 temporal-worker 持续访问已不存在的地址。该问题直接指向 `common/membership/ringpop/monitor.go`，且作者同日提交了对应修复 PR（#11431），说明这是真实生产环境痛点、影响面清晰。

- **[PR #11441] Make functional tests available to external runners**（[链接](https://github.com/temporalio/temporal/pull/11441)）— 将 137 个根测试体迁移到可导入的注册表，并支持按名称、正则、谓词选择测试，同时为 testcore 增加 runner 级集群路由与分片清单。这是测试基础设施的一次架构级改进，社区外部贡献者运行功能测试的门槛将大幅降低，潜在影响所有基于 Temporal 做二次开发的团队。

**诉求分析**：k8s 场景下 Pod IP 易变导致成员发现失效，反映用户对 Temporal 在动态基础设施下的韧性有较高要求；功能测试外部化则反映社区对"可编程、可筛选、可独立运行"测试能力的普遍需求。

---

## 5. Bug 与稳定性

按严重程度排列：

**高 — 成员发现探针指向陈旧 Pod IP（已有修复 PR）**
- Issue [#11429](https://github.com/temporalio/temporal/issues/11429)：k8s Pod 重启后，ringpop healer 持续探测旧 Pod IP，导致 gateway 日志报错、worker 无法连接新 frontend。根因是 `DiscoverProvider: statichosts.New(hostPorts...)` 使用静态主机列表且不感知成员变更。
- 修复 PR：[#11431](https://github.com/temporalio/temporal/pull/11431)（OPEN）— 将静态 bootstrap 列表替换为动态 discovery provider，从持久化存储刷新活跃成员地址，并附带单元测试覆盖刷新行为与错误传播。该 PR 由同一作者同日提交，修复路径直接；但处于待合并状态，需维护者及时 review。

**中 — 工作流删除竞态导致 DLQ 误入（WIP 修复中）**
- PR [#11440](https://github.com/temporalio/temporal/pull/11440)（[WIP]，OPEN）：源集群删除 workflow 时，`SYNC_VERSIONED_TRANSITION` 任务在目标集群执行会触发 NotFound，`HandleErr` 启动 best-effort cleanup 时若删除任务执行后无内容可删，可能造成不必要的 DLQ 投递。作者正在修复该竞态，当前为草稿状态。

**低 — 版本检查响应体未关闭/请求无超时（已有修复 PR）**
- PR [#11437](https://github.com/temporalio/temporal/pull/11437)（OPEN）：`versioninfo.Caller.Call` 仅在 200 状态码路径上关闭响应体，且请求无超时；由于传输层设置了 `DisableKeepAlives`，非 200 响应会导致连接泄漏。修复后所有路径关闭 body、请求受超时限制。

**低 — gRPC 连接/SDK 客户端生命周期未释放（修复中）**
- 相关 PR（均今日提交，OPEN）：
  - [#11438](https://github.com/temporalio/temporal/pull/11438) — `RPCFactory` 持有并关闭 gRPC 连接，`CreateLocalFrontendGRPCConnection` 改为 memoized 单例；
  - [#11436](https://github.com/temporalio/temporal/pull/11436) — `parentclosepolicy.Processor` 与 `scanner.Scanner` 正确停止其启动的 SDK worker 和 client。
  虽然不属于严重功能 bug，但连接/worker 泄漏在生产长稳运行中会积累资源压力，属于典型的可靠性加固。

---

## 6. 功能请求与路线图信号

今日无新增功能请求类 Issue。从活跃 PR 中可识别出以下明确的路线图信号（可靠性方向占主导）：

- **功能测试外部化**（[#11441](https://github.com/temporalio/temporal/pull/11441)）：开放 137 个根级功能测试给外部 runner，预计将改善社区贡献体验，是 OSS 生态建设的重要信号。
- **Backlog 感知的客户端 poll 负载均衡**（[#11114](https://github.com/temporalio/temporal/pull/11114)）：消费服务端下发的每分区 backlog 计数，将 poller 权重导向有积压的分区，避免轮询器困在空分区上。该能力直接提升大规模命名空间下的任务调度效率，符合可靠性路线图的容量治理方向。
- **Replication 流客户端侧生命周期上限**（[#11356](https://github.com/temporalio/temporal/pull/11356)，reliability-2026）：为 replication stream 引入最大生命周期与抖动系数，定期优雅重建流，防止长连接状态腐化。
- **Worker deployment version demotion 开关**（[#11426](https://github.com/temporalio/temporal/pull/11426)，已关闭）：通过动态配置默认关闭 demotion signal，为 OSS 用户提供安全迁移路径，后续可能默认启用。

以上 PR 如顺利合并，大概率随 1.32.0 或后续版本发布。

---

## 7. 用户反馈摘要

今日仅有 1 条 Issue（#11429），无评论：

**真实用户痛点**：@fm2022aa 在 Kubernetes 环境部署 Temporal 时，遇到 frontend Pod 重启后 **healer 长期探测旧 Pod IP** 的问题。从描述看，该用户采用了 statichosts 配置方式，现象为 gateway 日志不断报错、temporal-worker 无法切换到新 Pod 地址。这暴露了静态成员发现在动态基础设施（Pod 重建）下的脆弱性。

**使用场景**：生产环境 k8s 部署，Pod 生命周期较短、IP 频繁变更；用户期望 Temporal 在基础设施拓扑变化时自动收敛到最新成员列表，无需人工干预或重启组件。

**满意/不满意**：不满意点在于当前 ringpop healer 的静态探测机制在 Pod 重启后不能自愈；积极面是用户给出了明确的代码定位（monitor.go#L204），并直接提交了修复 PR（#11431），体现出社区贡献意愿。

> 限于今日 Issue 数据量（仅 1 条），无法给出更丰富的用户反馈归纳；建议后续关注 #11431 的 review 反馈与合入情况。

---

## 8. 待处理积压

以下为长期开放但近期有更新（或长期未动）的重点 PR，提醒维护者关注：

- **[#10502] DLQ CHASM pure task if valid after execution, add unit test verifications to test framework**（[链接](https://github.com/temporalio/temporal/pull/10502)）— 创建于 2026-06-03，已开放 **65 天**，属于 reliability-2026 专项。该 PR 解决纯任务执行后仍有效时任务卡死的问题，通过抛错并移入 DLQ 避免执行停滞；上一更新为今天（08-06），但依旧未合并。长期积压且与可靠性目标直接相关，建议优先 review。

- **[#11114] matching: backlog-aware client poll load balancing**（[链接](https://github.com/temporalio/temporal/pull/11114)）— 创建于 2026-07-16，已开放 22 天，期待值较高（影响大规模轮询效率），作者 @carlydf 持续更新中，需要关注服务端/客户端兼容性细节。

- **[#11232] VLN-1574: remediate checkout-below-v7**（[链接](https://github.com/temporalio/temporal/pull/11232)）— 安全自动化工具创建的 HIGH 严重级别修复，针对 CI 中 checkout action 低于 v7 的问题，已开放 15 天。安全类 PR 建议尽快处理（即使只是确认风险可接受并关闭）。

- **[#11311] Fence Backfiller tasks by generation**（[链接](https://github.com/temporalio/temporal/pull/11311)）— 创建于 2026-07-27，通过持久化 task sequence 替代时间比较来防范 backfill 重复，解决与旧二进制共存时的任务编号问题，长期开放可能有设计 review 上的拉锯，值得关注。

**未响应 Issue**：当前可见的 Issue 库中没有超过 24 小时未响应的新 Issue；暂无长期无人处理的重要 Issue 积压。

---

**总结**：Temporal 项目当前处于 1.32.0 发布前的密集开发期，PR 活跃度高、代码质量管控严格（大量测试补充）；社区反馈量暂时较小，但 k

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*