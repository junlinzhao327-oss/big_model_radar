# OpenClaw 生态日报 2026-08-14

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-13 22:36 UTC

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

# AI 智能体与个人 AI 助手开源生态横向对比分析报告

**报告日期：** 2026

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-14

> 数据窗口：2026-08-13 ~ 2026-08-14（GitHub 时间） | 数据来源：NousResearch/hermes-agent

---

## 1. 今日速览

过去 24 小时项目保持极高活跃度：**430 条 Issues 更新**（新开/活跃 319，关闭 111）与 **500 条 PR 更新**（待合并 318，已合并/关闭 182），并发布了 **v0.20.1 补丁版本**，将此前约 656 个 PR 合并为稳定发布。整体项目的健康度较好，但平台稳定性和回归类问题（尤其是 Windows/macOS 桌面端）占据了 Bug 报告的主要部分；社区讨论焦点集中在**工具 schema 的 token 开销**、**多租户隔离**和**Webhook/插件基础设施重构**三个方面。值得注意的是，今日有多个 P1 级桌面/网关问题被报告或更新，且部分已存在**针对性修复 PR**（如 #85679），说明维护者响应速度较快。

---

## 2. 版本发布

### v2026.8.13 — Hermes Agent v0.20.1 (Patch Release)

- **发布日期：** 2026-08-13
- **发布类型：** 补丁版本（Patch）
- **核心内容：** 将 v0.20.0 以来合并的 **~656 个 PR** 整合为一个稳定标签，供 Docker 镜像、托管部署及通过最新标签安装的下游用户使用。
- **破坏性变更：** Release 说明未指明破坏性变更；作为 patch release，预期以修复和稳定性为主。
- **迁移注意事项：** 本次发布聚焦“降低下游消费风险”，建议通过 `hermes update` 或重新拉取最新标签进行升级；Windows 用户升级时应注意已知的 gateway 冷启动问题（见 #84185，已有修复 PR #85679）。

🔗 [前往 Releases 页面](https://github.com/NousResearch/hermes-agent/releases)

---

## 3. 项目进展

过去 24 小时 **182 条 PR 已合并/关闭**，以下是最值得关注的推进方向（含新合并与高价值进行中工作）：

| 方向 | 关键 PR | 状态 | 说明 |
|---|---|---|---|
| **桌面更新链路修复** | [#85679 fix(desktop-update): drive the Windows hand-off through the venv python](https://github.com/NousResearch/hermes-agent/pull/85679) | OPEN | 修复 Windows 更新后 gateway 被 `hermes.exe` shim 置死的问题，直击 #84185 |
| **Agent 历史翻倍 Bug** | [#85678 fix(gateway): prevent response history doubling](https://github.com/NousResearch/hermes-agent/pull/85678) | OPEN | 修复 OpenAI Responses API 在返回持久化完整转录时导致对话历史翻倍的缺陷 |
| **推理模型超时适配** | [#85682 fix(agent): add reasoning stale-timeout floors for kimi-k3 and raise qwen3](https://github.com/NousResearch/hermes-agent/pull/85682) | OPEN | 为 OpenRouter 推理模型添加流式超时下限，避免长思考期被误杀 |
| **工具安全与状态一致性** | [#85654 fix(tools): do not adopt a stale cwd after an interrupted command](https://github.com/NousResearch/hermes-agent/pull/85654) | OPEN | 修复被中断命令留下的旧 cwd 被后续会话误继承 |
| **MCP OAuth 生命周期** | [#84963 fix(mcp-oauth): close teardown lock lifecycle](https://github.com/NousResearch/hermes-agent/pull/84963) | OPEN | 关闭 MCP OAuth teardown-lock 失败类问题（关联 #38193） |
| **Webhook 基础设施** | [#85636 fix(webhook): separate liveness from readiness](https://github.com/NousResearch/hermes-agent/pull/85636) | OPEN | Webhook Revolution 战役 Task 17：分离存活/就绪探针，避免敏感信息暴露 |
| **包管理修复** | [#85681 fix(nix): add registration lifecycle to pyproject.toml](https://github.com/NousResearch/hermes-agent/pull/85681) | CLOSED | Nix 构建注册生命周期修复 |
| **MCP 路径统一** | [#85677 fix(mcp): resolve Hermes home through one profile-aware helper](https://github.com/NousResearch/hermes-agent/pull/85677) | CLOSED | 将 `mcp_serve.py` 中 4 处重复的路径解析收敛为统一 profile 感知辅助函数 |

此外，**#85676 fix(tui): scope config writes to session profile** 修复了桌面/全局会话下配置写入错位问题；**#84065** 修复了 PKCE cookie 因 RFC 6265 分段而失效的 Dashboard 认证缺陷。整体来看，项目今日修复面覆盖了"桌面端更新/网关可靠性、对话状态一致性、OAuth 生命周期、Webhook 可观测性"等多个关键链路。

---

## 4. 社区热点

今日讨论最活跃的议题（按评论数排名）：

### 🔥 1. Lazy Tool Schema 加载 — 降低 Token 开销（#6839）
- **39 条评论 / 18 👍** | [链接](https://github.com/NousResearch/hermes-agent/issues/6839)
- **诉求：** 当前每次 API 调用都注入全部 50+ 工具集 schema，固定消耗 3,500-5,000 tokens（本地模型更严重）。社区呼声很高——用户希望实现"两遍式工具注入"，只在需要时加载工具 schema。
- **分析：** 这是当前社区对 **usage-cost 领域最强烈的诉求**，属于优化类需求而非 Bug，预计会影响后续 tool-loading 架构决策（标签中含 `needs-decision`）。

### 🔥 2. 插件接口扩展 / Hook 生命周期（#64182 / #64231）
- **35 + 26 条评论** | [#64182](https://github.com/NousResearch/hermes-agent/issues/64182) / [#64231](https://github.com/NousResearch/hermes-agent/issues/64231)
- **诉求：** 社区希望确立清晰的插件 hook 分类标准与生命周期事件目录，将大量"排队中的 hook PR"批量裁决（合并或关闭），而不是任其腐烂。
- **分析：** 插件基础设施正在经历规范化整理，`teknium1` 作为主要推动者，相关 PR 也已陆续进入 review（如 #64178、#64161）。这属于项目从"功能堆叠"向"结构性治理"过渡的信号。

### 🔥 3. 多租户 Hermes 问题（#34352）
- **27 条评论 / 3 👍** | [链接](https://github.com/NousResearch/hermes-agent/issues/34352)
- **诉求：** 用户 `@NimbleCoAI` 在生产环境运行多租户（multi-tenant）agent 数月，发现 memory 操作完全绕过 hook 系统，导致租户隔离必须 fork 核心分支才能实现。
- **分析：** 这是 **架构层面的长期痛点**，涉及 `comp/agent`、`comp/gateway`、`tool/memory` 三个组件，且标有 `needs-decision`。若未来 Hermes 想覆盖 B 端多用户场景，此问题必须解决。

### 🔥 4. Windows 桌面重启吞掉网关（#83683）
- **19 条评论** | [链接](https://github.com/NousResearch/hermes-agent/issues/83683)
- **诉求：** Windows 桌面版每次重启会强制杀死消息网关且不重新拉起，导致微信/QQ/Telegram 全部静默。被标记为 P1 回归。
- **分析：** 这是桌面端可靠性问题的典型代表，同批还有 #84185（update 后 gateway 静默死亡）、#52010（macOS 权限被撤销）。今日已有对应修复 PR #85679，值得持续跟踪。

### 🔥 5. Webhook Revolution — 战役级重构（#84834）
- **16 条评论** | [链接](https://github.com/NousResearch/hermes-agent/issues/84834)
- **诉求：** 对 Hermes 全部 Webhook 表面（ingress、execution、delivery、config、UI、部署、文档）进行 5×2×3 的 graph-gated 修复战役。
- **分析：** 这是 `@andrexibiza` 发起的宏大技术债清理计划，今日已有子 PR #85636（liveness/readiness 分离）跟进。

---

## 5. Bug 与稳定性

按严重程度汇总今日在途的 Bug 类 Issue（含回归、崩溃、静默失败），并标注是否已有修复 PR：

### P1 级（严重）

| Issue | 描述 | 平台/组件 | 修复 PR |
|---|---|---|---|
| [#83683](https://github.com/NousResearch/hermes-agent/issues/83683) | 桌面重启强制杀死网关且不重启，微信/QQ/Telegram 全部静默（回归） | Windows / Desktop | 关联 [#85679](https://github.com/NousResearch/hermes-agent/pull/85679) |
| [#84185](https://github.com/NousResearch/hermes-agent/issues/84185) | `hermes update` 后网关进程静默死亡（无日志、无 PID） | Windows / Desktop | [#85679](https://github.com/NousResearch/hermes-agent/pull/85679) |
| [#82001](https://github.com/NousResearch/hermes-agent/issues/82001) | 上下文压缩后 agent flush 不采用后续会话，误报"磁盘已满" | Agent / GC | 暂无直接 fix |
| [#78069](https://github.com/NousResearch/hermes-agent/issues/78069) | clarify 工具自由文本响应间歇性无法绑定，导致回合永久挂起 | Gateway / 多平台 | 暂无直接 fix |
| [#69592](https://github.com/NousResearch/hermes-agent/issues/69592) | `/sessions`

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报（2026-08-14）

## 1. 今日速览

过去 24 小时项目更新活跃：共产生 7 条 Issue 更新（5 条活跃、2 条关闭）和 29 条 PR 更新（25 条待合并、4 条已合并/关闭），无新版本发布。整体来看，项目处于高频迭代状态，社区贡献持续涌入，核心维护者（如 @neubig、@enyst）也在集中处理性能与基础设施问题。今日最重要的事件是修复了 agent-server 事件循环阻塞的高严重度性能 Bug（#4480 已关闭，修复 PR #4481 已合并），并合入了会话侧边栏性能优化（#4483）。此外，Agent Plugins 开放标准支持已进入设计讨论阶段（#4405），多项功能 PR 正在审查中。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日共有 4 个 PR 关闭/合并，标志着多个关键修复和功能落地：

- **修复 agent-server 事件循环阻塞（#4481）**：该 PR 针对 Issue #4480，将 bash 事件搜索从事件循环中移出，并用 `scandir` 替代 `glob.glob`，避免无界目录扫描导致的服务阻塞。这是一个直接影响生产稳定性的修复，合并后应显著改善长期运行实例的响应速度。  
  https://github.com/OpenHands/software-agent-sdk/pull/4481

- **缓存会话摘要，优化侧边栏性能（#4483）**：通过缓存未变动的会话摘要，避免每次请求都完整解析 `base_state.json`，修复了会话列表页面的性能退化。  
  https://github.com/OpenHands/software-agent-sdk/pull/4483

- **新增 file-router 目录创建 API（#4482）**：为文件路由服务添加 `POST /file/create_directory` 端点，补齐文件系统操作能力，且已有端到端验证。  
  https://github.com/OpenHands/software-agent-sdk/pull/4482

- **引入 ready-for-dev Issue/PR 门禁（#4464）**：将 OpenHands 主仓库的“就绪度评估”工作流移植到 SDK 仓库，自动化验证 Issue 描述质量与 PR 链接的 Issue 是否可开发，提升协作效率。对应 Issue #4463 亦已关闭。  
  https://github.com/OpenHands/software

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-14

## 1. 今日速览

过去24小时项目活跃度中等偏上，Issue 处理量较大（49条更新，32条关闭），PR 数量平稳（13条）。高优先级问题集中在 **上下文压缩触发机制**、**Mac 高 CPU 占用** 和 **TUI 性能** 三大方向；合并的修复主要覆盖 CLI 参数解析、终端恢复和会话持久化。今日无新版本发布，但多个修复已合入主干，项目整体处于“快速修 bug + 关键性能优化”的密集迭代阶段。

---

## 2. 版本发布

**无新版本发布**。当前可见版本为 0.84.1（多个 Issue 中提及，部分问题已在修复中）。

---

## 3. 项目进展

### 已合并/关闭的重要 PR

| PR | 内容 | 影响 |
|---|---|---|
| [#8086](https://github.com/earendil-works/pi/pull/8086) | Gemini 工具调用 schema 端点在拒绝未知字段时，自动回退到 legacy Schema | 修复兼容性，保证 Gemini 工具调用可用 |
| [#8084](https://github.com/earendil-works/pi/pull/8084) | 修复 boolean 扩展标志后 CLI 参数被吞掉的问题（如 `--plan "prompt"` 丢失 prompt） | 恢复 CLI 可靠性，避免静默空会话 |
| [#8082](https://github.com/earendil-works/pi/pull/8082) | TUI 全量渲染仅渲染可见视口；SIGINT 时恢复终端状态 | 修复恢复大会话刷屏、终端残留问题（对应 #8079/#8080） |
| [#8067](https://github.com/earendil-works/pi/pull/8067) | 用户可见字符串统一使用 APP_NAME | 改善 rebrand 场景的一致性 |

**关键信号**：#8082 的合入同时解决了“恢复大会话刷屏”“SIGINT 终端不恢复”两个稳定性问题，且新增了可见视口渲染优化，对 TUI 用户体验提升明显。

---

## 4. 社区热点

### 最热 Issue

**[#6879](https://github.com/earendil-works/pi/issues/6879) — auto-compaction never triggers until provider overflow（评论 19，👍 17）**
- 用户报告 session 在 GPT-5.6-sol 上上下文使用率超过 100% 后仍不自动压缩，直到 API 报错。问题已持续近一个月，用户期待每次 agent 回合后进行检查。
- **诉求**：压缩不应依赖 provider 拒绝请求才触发，应在每个 agentic turn 结束后主动检查。

**[#7730](https://github.com/earendil-works/pi/issues/7730) — High CPU usage on Mac OS（评论 11，👍 8）**
- 长时间 session 在 macOS 上 CPU 占用 50%-110%，内存 600-800MB。社区推测与上下文尺寸或 session 长度相关。
- **诉求**：针对长 session 的性能优化，尤其是 TUI 渲染和内存中状态管理。

**[#7836](https://github.com/earendil-works/pi/issues/7836) — Edit fuzzy match 对空白长度敏感（评论 10，👍 1）**
- `normalizeForFuzzyMatch` 不会折叠连续空白或去除行前空白，导致小模型在编辑时因空白不一致而匹配失败。
- **诉求**：增强模糊匹配的健壮性，降低对空白差异的敏感度。

---

## 5. Bug 与稳定性

按严重程度排序：

### 高严重度

| Issue | 问题 | 状态 | 修复 PR |
|---|---|---|---|
| [#6879](https://github.com/earendil-works/pi/issues/6879) | 上下文压缩直至 API 溢出时才触发，可能造成令牌浪费或请求失败 | OPEN，已活跃近 1 个月，需要维护者关注 | 无 |
| [#7730](https://github.com/earendil-works/pi/issues/7730) | Mac 上长会话 CPU 高占用（50-110%） | OPEN，讨论中，尚未定位根因 | 无 |
| [#8080](https://github.com/earendil-works/pi/issues/8080) | SIGINT 中断后终端残留 raw mode、窗口标题未恢复 | CLOSED（已修复） | [#8082](https://github.com/earendil-works/pi/pull/8082) ✅ |

### 中严重度

| Issue | 问题 | 状态 | 修复 PR |
|---|---|---|---|
| [#8029](https://github.com/earendil-works/pi/issues/8029) | 大 buffer 下 prompt 编辑器光标移动延迟（7000 行 ~1650ms） | OPEN，in-progress | [#8066](https://github.com/earendil-works/pi/pull/8066)（视觉行缓存） |
| [#7761](https://github.com/earendil-works/pi/issues/7761) | TUI 复制显示“Copied!”但剪贴板实际为空（VTE 终端） | OPEN，待确认修复 | 无 |
| [#8031](https://github.com/earendil-works/pi/issues/8031) | openai-codex 中途失败后重试，导致部分输出重复显示 | CLOSED（已确认） | 无公开 PR，需跟进 |
| [#8060](https://github.com/earendil-works/pi/issues/8060) | 流式 thinking 输出部分内容短暂显示为标题颜色 | CLOSED（已确认，待修复） | 无 |

### 低严重度 / 边缘场景

| Issue | 问题 | 状态 |
|---|---|---|
| [#8055](https://github.com/earendil-works/pi/issues/8055) | CJK 终端中 Ambiguous-width 字符计宽错误导致表格错位 | 待确认 |
| [#8074](https://github.com/earendil-works/pi/issues/8074) | MCP 工具无 renderResult 时 Ctrl+O 折叠失效 | 待确认 |
| [#7829](https://github.com/earendil-works/pi/issues/7829) | Windows 下 settings.json 路径转义错误导致误导性报错 | 待改进错误提示 |

**稳定性观察**：核心 TUI 终端恢复问题已随 #8082 修复，性能瓶颈（#8029）已有针对性优化 PR，进展积极；但 auto-compaction（#6879）和 Mac 高 CPU（#7730）仍是影响长期使用的关键隐患。

---

## 6. 功能请求与路线图信号

- **[#7689](https://github.com/earendil-works/pi/issues/7689) — 支持 Codex `end_turn: false`**（👍 2）：Codex 后端在 response.completed 中可能返回 `end_turn: false`，需要处理该信号。该功能对 Codex 后端深度集成有影响，可能进入后续版本。
- **[#7607](https://github.com/earendil-works/pi/issues/7607) — per-tool 参数校验 opt-out**：允许 host 对工具 schema 严格而内部宽松，适合有特殊验证需求的场景。
- **[#8041](https://github.com/earendil-works/pi/issues/8041) — HTML 导出渲染 mermaid 和 LaTeX**：延续 #7956 的努力，提升导出文档的可用性和美观度。
- **[#8017](https://github.com/earendil-works/pi/issues/8017) — Anthropic 侧拒绝对话时 server-side fallback**：应对 Anthropic 分类器误判导致的压缩失败，有现实需求。
- **[#8075](https://github.com/earendil-works/pi/issues/8075) — 支持 Kimi `cached_tokens` 统计**：对使用 Kimi API 的用户有实际意义，改动较小，可能被快速纳入。

**路线图判断**：`end_turn: false`（#7689）及 Kimi 统计（#8075）属于后端适配型需求，代码侵入小，下个版本合入概率高；Mermaid/LaTeX HTML 导出（#8041）需要 TUI 与 HTML 渲染层转换，预计周期较长。

---

## 7. 用户反馈摘要

- **@alexanderkreidich（#6879）**：真实使用中一次 agentic turn 运行超过 2 小时，footer 超过压缩阈值后仍继续增长，直到 API 拒绝请求（373k tokens）。用户期望压缩更主动，让长任务更可靠。
- **@robjgray（#7836）**：反馈小模型在编辑时因空白差异导致匹配失败，说明当前 edit 工具对模型输出要求偏高，希望能更宽容。
- **@odafeng（#7829）**：Windows 用户在 settings.json 中未转义反斜杠，导致启动时报“bash not found”，实际是 JSON 解析失败。用户希望错误提示能更明确。
- **@gterzian（#7730）**：macOS 用户观察 CPU 占用与 session 长度相关，但未确认具体触发点，希望有更细致的 profiling 或优化。
- **@frankieyep（#8079/#8080）**：恢复大 session 时大量历史输出刷屏，影响工作流；SIGINT 后终端需要 reset 才能恢复，已随 #8082 修复。

---

## 8. 待处理积压

| 类型 | 编号 | 说明 | 持续时间 |
|---|---|---|---|
| Issue | [#6879](https://github.com/earendil-works/pi/issues/6879) | auto-compaction 不触发的关键 bug，评论与点赞均最多，已近 1 个月未解决 | 2026-07-20 创建 |
| PR | [#6216](https://github.com/earendil-works/pi/pull/6216) | 新增 Amazon Bedrock Mantle OpenAI Responses 提供商，已开放 1 个多月未合并 | 2026-07-01 创建 |
| Issue | [#4254](https://github.com/earendil-works/pi/issues/4254) | 扩展加载性能优化（jiti moduleCache），虽已关闭但收集了性能优化需求，暗示启动速度仍是痛点 | 2026-05-07 创建 |
| Issue | [#7739](https://github.com/earendil-works/pi/issues/7739) | 设置启动预算，与 jcode 对比启动延迟和内存，已开放近 1 周，未有人认领 | 2026-08-06 创建 |
| Issue | [#7787](https://github.com/earendil-works/pi/issues/7787) | `PI_*` guideline 导致无关任务出现多余权限提示，可能影响使用流畅度 | 2026-08-07 创建 |

---

**总结**：今日项目展现出高效的 bug 修复与社区反馈响应速度，尤其在 TUI 终端卫生和 CLI 参数方面；但核心的上下文压缩时机（#6879）和 macOS 性能（#7730）问题仍悬而未决，建议维护团队优先投入。若 #8066（视觉行缓存）能快速合入，prompt 编辑器卡顿问题也有望在下个版本得到明显改善。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-14

> 数据来源：github.com/BerriAI/litellm
> 数据窗口：2026-08-13 至 2026-08-14（北京时间）

---

## 1. 今日速览

过去 24 小时 LiteLLM 项目活跃度处于**极高水平**：Issue 侧 62 条更新（43 条活跃、19 条关闭），PR 侧 276 条更新（176 条待合并、100 条已合并/关闭），并发布了 1 个 dev 版本。值得注意的信号：大量 PR 集中在 MCP OAuth 令牌管理、团队/访问组清理、UI 组件库迁移（antd→shadcn）与成本计算修正四条主线上；同时一批 3–4 月创建的 stale Issue 仍在获得社区讨论，反馈积压问题尚未完全消化。整体看，项目迭代速度很快，社区参与度高，但长期未关闭 Issue 的存量也需要关注。

---

## 2. 版本发布

**v1.98.0-dev.2**（发布时间：2026-08-13/14 窗口内）

该 dev 版本未附带详细 changelog，仅包含 Docker 镜像 cosign 签名验证说明（所有镜像使用 commit `0112e53` 引入的同一签名密钥）。作为 `v1.98.0` 的第二个 dev 预发布版，预期包含本次日报中提到的 MCP、团队管理、UI 迁移等新特性，**但注意 dev 版本不应直接用于生产环境**。

- Release 链接：https://github.com/BerriAI/litellm/releases
- 签名说明参考：https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0

---

## 3. 项目进展

今日合并/关闭的 PR 中，以下几条对项目健康度有显著正向贡献，按模块分类如下：

### 稳定性和并发修复
- **#36824 — 并发创建 spend views 容错**：多个副本同时冷启动时，视图创建竞争不再导致启动崩溃。此前崩溃发生在 detached 任务中、无人感知，修复后 CREATE 竞争失败被视为成功，真正的 DDL 错误仍会抛出。https://github.com/BerriAI/litellm/pull/36824
- **#36699 — 显式 `budget_duration: null` 与 UI 可清除预算下拉**：`/team/new`、`/key` 创建路径上，显式传 `null` 不再被默认值覆盖，UI 表单也能选择/恢复"永不重置"，修复了配置默认值抢占用户意图的问题。https://github.com/BerriAI/litellm/pull/36699

### 测试覆盖
- **#36802 — E2E 覆盖网关自身 AWS 身份访问 Bedrock**：此前所有 Bedrock 测试都硬编码静态 AWS Key，新增测试用例验证生产环境中真正使用的"网关自带身份"路径，避免该路径悄然回归。https://github.com/BerriAI/litellm/pull/36802

### 其他值得关注的待合并 PR（已被维护者 pick up）
- MCP OAuth 令牌清除与撤销（#36831、#36840）
- Team/访问组引用清理与权限收窄（#36819、#36825、#36837）
- Vertex 区域端点价格修正（#36833）
- UI 持续的 antd→shadcn 迁移（#36834、#36838）

整体评估：**项目在同步推进"数据正确性、权限安全、技术债清理"三条线**，且 UI 迁移和 MCP 治理属于较大的结构性改进。

---

## 4. 社区热点

### 最热 Issue
| Issue | 评论数 | 👍 | 状态 | 核心诉求 |
|---|---|---|---|---|
| [#23869 添加自定义 MCP Server 报错](https://github.com/BerriAI/litellm/issues/23869) | 17 | 9 | OPEN（stale） | UI 添加 MCP Server 时后端报 `Could not find...`；创建于 3 月，至今仍在获得回复 |
| [#24549 Xiaomi MiMo 模型 output_config 参数报错](https://github.com/BerriAI/litellm/issues/24549) | 8 | 0 | OPEN（stale） | Claude Code 调用 MiMo-V2 系列时 `output_config` 触发 AsyncCompletions 失败 |
| [#18654 OCI Gemini 工具调用异常](https://github.com/BerriAI/litellm/issues/18654) | 8 | 1 | CLOSED | OCI 上 Gemini 模型工具调用（流式/非流式均）异常；今日关闭，疑似已定位 |
| [#24659 Azure OpenAI Realtime WebRTC 流程问题](https://github.com/BerriAI/litellm/issues/24659) | 7 | 0 | OPEN | 临时令牌铸造到 WebRTC 连接的过程无法走通 |
| [#36192 Azure GPT-5.6 Terra/Luna 价格行错误](https://github.com/BerriAI/litellm/issues/36192) | 7 | 0 | OPEN | Azure 价格误用 OpenAI 直连价，实际 Azure 从未降价 |

### 分析
两个高热度问题的诉求有共性：**LiteLLM 作为代理层，对上游新增模型/新 API 形态（MCP、Realtime、MiMo）的支持存在滞后或不完整，且错误信息不足以帮助用户自助排查**。#36192 则属于成本数据正确性 -- 直接影响用户账单和内部核算，此类问题通常优先级较高。

---

## 5. Bug 与稳定性

按严重程度排列（🔴 高 / 🟡 中 / 🟢 低）：

| 严重度 | Issue/PR | 描述 | 状态 |
|---|---|---|---|
| 🔴 | [#31441 `end_user` 钉在首请求的 `user` 上（v1.87.0 回归）](https://github.com/BerriAI/litellm/issues/31441) | 共享虚拟密钥下，后续请求的 `end_user` 列均记录为第一个请求的 `user` -- SpendLogs 数据污染 | OPEN，无关联 fix PR |
| 🔴 | [#36192 Azure GPT-5.6 价格错误](https://github.com/BerriAI/litellm/issues/36192) | Azure Terra/Luna 沿用 OpenAI 降价后价格，未按 Azure 实际计费表修正 | OPEN，无 fix PR（#36833 类似修复仅覆盖 Vertex） |
| 🔴 | [#27884 429 错误体泄露完整 SHA-256 token 哈希](https://github.com/BerriAI/litellm/issues/27884) | 限流响应 JSON 包含 64 字符虚拟密钥哈希，存在安全隐患 | OPEN（stale） |
| 🟡 | [#36759 `gen_ai.system` 仍以 None 到达 OTel exporter](https://github.com/BerriAI/litellm/issues/36759) | PR #26713 只修了 span 属性一处调用点，metrics/events 路径仍触发类型错误 | OPEN，今日新报告 |
| 🟡 | [#36566 content_filter guardrails 评估结果不出现在日志/监控](https://github.com/BerriAI/litellm/issues/36566) | 元数据有记录但 Guardrails Monitor 不展示 | OPEN |
| 🟡 | [#32474 用户 max budget 无法重置为 Unlimited](https://github.com/BerriAI/litellm/issues/32474) | 与已关闭 #19781 同源，internal user 场景仍存在 | OPEN |
| 🟡 | [#36366 Azure Responses 转发空 namespace 描述](https://github.com/BerriAI/litellm/issues/36366) | Codex CLI 0.147.0 默认发送的 namespace tools 未经规范化直接转发 | OPEN |
| 🟢 | [#36765 OpenAPI→MCP 工具生成丢失 $ref body schema](https://github.com/BerriAI/litellm/issues/36765) | FastAPI/Pydantic 生成的 $ref 请求体在 MCP tool inputSchema 中为空 | OPEN，今日新报告 |
| 🟢 | [#18654 OCI Gemini 工具调用异常](https://github.com/BerriAI/litellm/issues/18654) | 已关闭，等待 changelog 确认修复版本 | CLOSED |

**回归风险提示**：`#31441`（end_user 回归）和 `#36759`（OTel 修复不完整）均属于"修复了 A 路径但漏了 B 路径"的典型半修复问题，建议维护者在合入相关 PR 时排查同类调用点。

---

## 6. 功能请求与路线图信号

### 今日活跃的功能请求
1. **[#27213 Custom Transport 支持（httpx client 注入）](https://github.com/BerriAI/litellm/issues/27213)** -- 允许向 `acompletion` 传自定义 `httpx.Client`，简化代理、TLS、连接池定制。5 月提出，已 stale，但请求合理且不破坏现有 API，适合作为 SDK 增强。
2. **[#36559 系统中途插入导致 prompt-cache 前缀失效](https://github.com/BerriAI/litellm/issues/36559)** -- `AnthropicMessagesConfig._normalize_system_role_messages` 将中间 system 消息提升为顶层字段，使此前所有缓存前缀失效。这不是新功能而是**性能回归**，但修复方向可能涉及配置项调整，值得关注。
3. **MCP 相关（间接需求）** -- PR #36831 和 #36840 分别增加 MCP OAuth 令牌清除与反选 server 时撤销授权，说明维护者正在系统性完善 MCP 治理能力。社区对 MCP 的诉求已从"能连"升级为"能管"。

### 可能进入下一版本的方向（基于今日 PR）
- **成本正确性**：`off_peak_pricing`（#31725，6 月底提出，今日仍有更新）、Vertex 区域价格修正（#36833）、模型表刷新（#36788）-- 成本方向明显在加速。
- **UI 现代化**：#36834/#36838 两个 shadcn 迁移 PR 今日同时提交，antd/Tremor 退出路线图在稳步执行。
- **Observability**：#36827 在 Playground 聊天响应中展示 provider prompt cache tokens，说明可观测性继续向"更细粒度"演进。

---

## 7. 用户反馈摘要

从今日活跃 Issues 的评论中提炼以下真实用户声音：

1. **"错误信息不够 actionable"**（来源 #23869、#36765、#25447）
   用户添加 MCP Server 失败时只看到 `Could not find`，不清楚缺的是配置项还是上游地址；OpenAPI 转 MCP 后工具 schema 为空也没有 warning。用户普遍希望**错误信息能指出缺失的具体字段/步骤**。

2. **"修复回归比新功能更影响信任"**（来源 #31441、#20975、#25447）
   #25447 的响应串线问题虽然今日关闭，但期间用户承受了极大的信任成本。"同一个 key 下用户 A 可能收到用户 B 的响应"这类问题在评论中被称为 "critical"。任何涉及此类数据隔离的改动都值得最高优先级回归测试。

3. **"成本数据错误直接导致内部对账失败"**（来源 #36192）
   评论中用户明确表示 Azure 价格未反映实际账单，导致企业客户**无法将 LiteLLM 作为成本核算的唯一来源**，需要额外手动修正。

4. **"stale 标签让用户感到被忽视"**（来源 #23869、#24549）
   多个 5 个月前创建、至今仍未被 close 或修复的 Issue 挂上了 `stale` 标签，但用户仍在评论区持续回复补充信息。`stale` 机器人应该区分"无人问津"和"已知问题但未排期"。

---

## 8. 待处理积压

以下为长期未响应/未解决、但社区关注度较高的条目，提醒维护者关注：

| 条目 | 创建时间 | 关注度 | 备注 |
|---|---|---|---|
| [#23869 添加自定义 MCP Server 报错](https://github.com/BerriAI/litellm/issues/23869) | 2026-03-17 | 17 评论 / 9 👍 | 已 stale，但仍在收到新评论；MCP 是当前重点功能，建议排查 |
| [#24549 Xiaomi MiMo output_config 失败](https://github.com/BerriAI/litellm/issues/24549) | 2026-03-25 | 8 评论 | 已 stale；影响 Claude Code 用户对新模型的使用 |
| [#27884 429 响应泄露 token 哈希](https://github.com/BerriAI/litellm/issues/27884) | 2026-05-14 | 2 评论 | 安全问题，虽评论少但性质严重，已 stale 超过 3 个月 |
| [#27213 Custom Transport 支持](https://github.com/BerriAI/litellm/issues/27213) | 2026-05-05 | 4 评论 | SDK 增强请求，评论中有用户补充使用场景 |
| PR [#31725 时间维度 off-peak 定价](https://github.com/BerriAI/litellm/pull/31725) | 2026-06-30 | -- |

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-14

## 1. 今日速览

过去 24 小时项目活跃度较高：PR 更新 83 条（60 条待合并，23 条已合并/关闭），Issue 更新 10 条（全部处于开放状态，无新增关闭），未发布新版本。PR 提交集中在可靠性工程（[reliability-2026]）、可观测性（OpenTelemetry HTTP 插桩、Span 注解）、Nexus 集成以及 Elasticsearch 可见性日期格式修复等方向。值得关注的是 10 条活跃 Issue 中有多条涉及调度器（Schedules）的稳定性与死锁问题，且无一条在 24 小时内被关闭，显示 issue 积压未减。项目整体处于活跃开发状态，但调度器与复制路径上的潜在缺陷需要警惕。

## 2. 版本发布

今日无新版本 Release。

## 3. 项目进展

今日合并/关闭了 23 条 PR，以下为较重要的几条（按主题归类）：

- **幂等性与请求 ID 支持**：[#11169](https://github.com/temporalio/temporal/pull/11169)（CLOSED）— 为 `UpdateComponent` 增加 `WithRequestID` 支持，实现执行级幂等保护，这是 CHASM 可靠性计划的一部分。
- **复制任务可观测性**：[#11459](https://github.com/temporalio/temporal/pull/11459)（CLOSED）— 在复制任务发送时记录其携带的内容（如 `LastUpdateVersionedTransition` 状态），避免后续因状态被覆盖而无法追踪任务负载。
- **泄漏检测工具增强**：[#11505](https://github.com/temporalio/temporal/pull/11505)（CLOSED）— 为 `objectleak` 增加进程生命周期基线追踪，过滤运行时无法追踪的小型指针分配，使泄漏报告更可操作。

此外，仍有 60 条 PR 待合并，其中包含若干关键修复（见下节）。整体来看，今日代码合入以可靠性工具链和可观测性为重心，核心服务逻辑变更相对保守，项目处于稳步迭代状态。

## 4. 社区热点

- **[#10841](https://github.com/temporalio/temporal/issues/10841) SignalWithStart 在孤立 current-execution 指针上永久挂起** — 2 条评论，+2 个反应（含作者）。该 Issue 创建于 6 月，但仍在活跃讨论中。用户报告 `SignalWithStartWorkflowExecution` 可能因孤儿 current-execution 指针永久阻塞，且怀疑其他依赖 current execution 的 API 也有类似风险。这是核心工作流 API 的正确性问题，社区关注度高。

- **[#8490](https://github.com/temporalio/temporal/issues/8490) 调度操作未清除 Successful 后的 ContinuedFailure** — 2 条评论，+2 👍。用户反馈：当调度动作失败后设置 `ContinuedFailure`，后续成功的调度不会清除该 payload，导致成功执行仍携带失败信息。涉及调度器状态清理逻辑，已持续近 10 个月未修复。

- **[#11534](https://github.com/temporalio/temporal/issues/11534) Fairsim 部分计数器配置重置未指定默认值** — 1 条评论。用户提交了一个很具体的 bug 报告：`tools/fairsim` 的 `-counter-params` 只应覆盖指定字段，但实际会重置其他未指定字段的默认值。属于工具链易用性问题但影响开发体验。

社区讨论整体偏技术细节，主要围绕调度器语义、API 正确性和开发工具链。

## 5. Bug 与稳定性

今日活跃的 Bug 按严重程度排列：

**高严重度：**

- **[#10841](https://github.com/temporalio/temporal/issues/10841) `SignalWithStart` 在孤儿 current-execution 指针上永久挂起** — 核心 API 可能阻塞至客户端超时，影响面大。暂无关联 fix PR。
- **[#11547](https://github.com/temporalio/temporal/issues/11547) `Unavailable` 瞬时抖动重置 History 队列退避，引发持续重试风暴** — 在持久化 QPS 接近上限时，短暂的 `Unavailable` 错误会让队列读者/任务执行器退出长退避状态，导致重试风暴，可能进一步压垮系统。这是一个典型的级联故障触发器，需要紧急关注。相关 PR [#11554](https://github.com/temporalio/temporal/pull/11554) 正在修复 reader 卡住计数的判定逻辑（仅当读取的批次切片仍遗留任务时计入卡住尝试），可缓解误判导致的退避重置，但并非完全对应的修复。
- **[#11539](https://github.com/temporalio/temporal/issues/11539) `DeleteWorkerDeploymentVersion` 在版本摘要比版本工作流存活更久时永久失败** — 用户无法清理已排空的版本，最终可能阻塞新版本注册。暂无 fix PR。
- **[#10579](https://github.com/temporalio/temporal/issues/10579) Schedule 在 Workflow ID 复用后死锁（retry chain 场景）** — 调度器内部工作流在 `refreshWorkflows` 中永久阻塞，导致整个 Schedule 失效。暂无关联 fix PR。

**中严重度：**

- **[#8490](https://github.com/temporalio/temporal/issues/8490) `Scheduled Actions` 不清理成功后的 `ContinuedFailure`** — 成功结果被错误地标记为失败延续。已开放 10 个月，仍无 fix PR。
- **[#9522](https://github.com/temporalio/temporal/issues/9522) MySQL 8.0.45 创建 visibility schema 失败（Error 1064）** — 自托管用户部署被阻塞，可能与 MySQL 版本兼容性有关。暂无明确 fix。
- **[#11534](https://github.com/temporalio/temporal/issues/11534) Fairsim 部分计数器配置重置未指定默认值** — 低风险工具 bug，但影响本地测试体验。

**低严重度：**

- [#11314](https://github.com/temporalio/temporal/issues/11314) Cassandra schema 仍使用 LCS 而非 Cassandra 5.x 默认的 UCS — 属于长期技术债。

## 6. 功能请求与路线图信号

来自 Issue 侧的新需求信号：

- **[#8087](https://github.com/temporalio/temporal/issues/8087) Schedules 跳过动作指标** — 用户希望新增 metric，在调度因 overlap policy、catchup window 或 buffer overflow 跳过运行时发出计数。该 Issue 已开放超过一年，仍无实现计划。若被采纳，预计会进入 Schedules 模块的可观测性增强中。
- **[#11314](https://github.com/temporalio/temporal/issues/11314) 将 Cassandra 压缩策略从 LCS 迁移到 UCS** — 适配 Cassandra 5.x 默认策略，属于基础设施现代化诉求，与项目长期演进方向一致。

来自 PR 侧的新功能信号（可能进入下一版本）：

- **[#11520](https://github.com/temporalio/temporal/pull/11520)** 与 **[#11380](https://github.com/temporalio/temporal/pull/11380)** — 推进 Worker Callbacks 功能：前者填充 `CallbackInfo.outcome`，后者识别新的 `commonpb` worker callback 变体。属于较大的功能特性。
- **[#11558](https://github.com/temporalio/temporal/pull/11558) OpenTelemetry HTTP 插桩** — 为 Nexus 的 HTTP 路径提供通用追踪支持，补齐 gRPC 之外的观测能力。
- **[#11563](https://github.com/temporalio/temporal/pull/11563) Namespace CRUD 生命周期宽事件** — 发布 namespace 注册、更新、failover、删除的控制面事件，推动事件驱动可观测性。

## 7. 用户反馈摘要

从活跃 Issue 的用户评论和报告中提炼的要点：

- **自托管部署的数据库兼容性痛点持续存在**（[#9522](https://github.com/temporalio/temporal/issues/9522)）：用户使用 MySQL 8.0.45 自托管 v1.29，在 `manage-schema-visibility-store` job 中遇到 SQL 语法错误，导致部署流程中断。该用户处于等待响应状态。
- **调度器和核心 API 的稳定性是用户最大痛点**：多个报告（[#10579](https://github.com/temporalio/temporal/issues/10579)、[#10841](https://github.com/temporalio/temporal/issues/10841)）指向工作流无法进展或永久阻塞的问题，且都是生产环境会遇到的严重故障，用户对修复时效有较高期待。
- **对调度语义的期望与实现有落差**（[#6173](https://github.com/temporalio/temporal/issues/6173)）：用户明确指出 Schedule 的 `StartAt` 参数未参与间隔计算，认为文档与实际行为不符。该 Issue 自 2024 年 6 月起一直开放，至今无维护者回应。
- **Cassandra 用户对存储策略有明确技术倾向**（[#11314](https://github.com/temporalio/temporal/issues/11314)）：提交者主动对比了 LCS 与 UCS 的适用场景，认为 LCS 不适合通用型负载，建议默认改用 UCS，体现用户对底层存储调优的深度参与。
- **工具链细节影响开发效率**（[#11534](https://github.com/temporalio/temporal/issues/11534)）：fairism 配置覆盖行为不符合直觉，用户期望部分覆盖仅影响指定参数。这是一个小而真实影响模拟测试体验的问题。

## 8. 待处理积压

以下 Issue/PR 长期未得到维护者响应或修复，值得重点关注：

- **[#6173](https://github.com/temporalio/temporal/issues/6173) Schedule "StartAt" 不参与间隔计算（2024-06-19 创建）** — 已开放超过 2 年，至今无维护者评论。用户明确给出了复现条件和预期行为，指向调度模块的语义缺陷。
- **[#8087](https://github.com/temporalio/temporal/issues/8087) 调度跳过动作指标（2025-07-22 创建）** — 功能请求已开放超过一年，属于合理的可观测性增强，但一直未被纳入开发计划。
- **[#8490](https://github.com/temporalio/temporal/issues/8490) Scheduled Actions 的 ContinuedFailure 未清除（2025-10-15 创建）** — 缺陷明确、影响可感知（成功执行携带失败 payload），但 10 个月无修复 PR，用户加了 2 个 👍 也未能引起足够关注。
- **[#10579](https://github.com/temporalio/temporal/issues/10579) Schedule 因 Workflow ID 复用而永久死锁（2026-06-06 创建）** — 严重度高（调度器完全不可用），但当前 0 评论、0 反应，可能尚未被维护者看到。

此外，PR 队列也存在长期滞留情况，如 [#10739](https://github.com/temporalio/temporal/pull/10739)（Annotate worker task spans）自 6 月 16 日起开放至今，仍在等待依赖 PR 合入。此类长期开放的 PR 和 Issue 累积会消耗社区信任，建议维护者定期 triage 并给出明确状态更新。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*