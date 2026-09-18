# OpenClaw 生态日报 2026-09-18

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-18 00:28 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目日报 · 2026-09-18

---

## 1. 今日速览

- **活跃度极高**：过去 24 小时 Issues 更新 500 条（新开/活跃 323，关闭 177），PR 更新 500 条（待合并 296，已合并/关闭 204），但**新开问题数仍高于关闭数，积压呈净增长态势**。
- **零版本发布**，所有工作集中在 `main` 分支的修复与加固上，属于典型的"补丁密集期"。
- **稳定性是绝对主线**：P0/P1 级问题覆盖网关事件循环饥饿、消息丢失、MCP 子进程泄漏、崩溃循环等多个维度，多个高热度 Issue 已持续数周。
- **维护者批量推进"取消语义"修复**：以 @shakkernerd 为代表的一批 PR 集中解决 Feishu/Teams/Matrix/Zalo/Telegram 通道在调用方取消后仍发出请求的问题，今日已有 2 个关闭。
- **企业级部署场景压力显现**：632-agent 集群的启动时长（12 分钟）与就绪后不可服务问题成为最受关注的回归风险。

---

## 2. 版本发布

无新版本发布（0 个 Release）。项目处于无版本窗口期，建议关注 `main` 分支上已"ready for maintainer look"的 P0/P1 修复 PR，它们很可能是下一个补丁版本的核心内容。

---

## 3. 项目进展

今日共 204 个 PR 被合并/关闭、177 个 Issue 被关闭，推进方向集中在**取消/生命周期正确性**与**诊断工具可靠性**两条线：

**已关闭的 PR（示例）**
- [#151235](https://github.com/openclaw/openclaw/pull/151235) — 修复 Feishu 消息编辑在调用方取消后仍触达提供方的问题（基于 #151168 的请求所有权机制）。
- [#151237](https://github.com/openclaw/openclaw/pull/151237) — 修复 Teams Graph 操作在调用方关闭后继续执行（pin 流程 token 获取阶段）。

**已关闭的重要 Issue（实质推进）**
- [#150452](https://github.com/openclaw/openclaw/issues/150452)（P0, ux-release-blocker）— 2026.7.1-2 → 2026.9.4 升级需一天手工修复的严重升级事故。
- [#146719](https://github.com/openclaw/openclaw/issues/146719)（P0）— Windows 更新器因 `OPENCLAW_STATE_DIR` 未展开导致快照 mkdir 失败，阻塞 Windows 升级路径。
- [#145563](https://github.com/openclaw/openclaw/issues/145563)（P0）— WeChat 通道回复分发因 `PreparedModelCatalogConfigReplacedError` 失败。
- [#142965](https://github.com/openclaw/openclaw/issues/142965) — 会话结束后 per-session MCP 子进程不被回收、直到网关重启才清理。
- [#148898](https://github.com/openclaw/openclaw/issues/148898) — claude-cli 无输出看门狗把主机休眠时间计入静默预算，导致笔记本唤醒后杀掉在途回合。
- [#111985](https://github.com/openclaw/openclaw/issues/111985) — memory-core 将 ChatGPT/Codex OAuth token 发送至 OpenAI embeddings API 的凭据越界问题。
- [#138260](https://github.com/openclaw/openclaw/issues/138260)、[#77802](https://github.com/openclaw/openclaw/issues/77802) — `openclaw doctor` 自身的 lint 快照清理与 `--fix` 原子性失败问题。

**判断**：项目在"通道取消语义"和"诊断/升级工具链"两个方向上有实质推进，属于健康度正贡献；但关闭的多为存量问题，新增质量问题的涌入速度仍是主要风险。

---

## 4. 社区热点

| 排名 | 条目 | 评论 | 诉求分析 |
|---|---|---|---|
| 1 | [#97616](https://github.com/openclaw/openclaw/issues/97616) 僵尸子进程累积导致运行时退化 | 30 | 长期运行的网关（hooks/tool 子进程 `openclaw-hooks`、`bash`、`codex`）不回收，是典型的"跑得越久越慢"生产级痛点，社区讨论热度最高但**至今无 fix PR**。 |
| 2 | [#144911](https://github.com/openclaw/openclaw/issues/144911) MCP server init 超时崩溃网关 | 29 | stdio MCP 30s 内未完成 `initialize` 触发子进程清理路径的 unhandled rejection，直接打挂 Gateway。已带 `clawsweeper:queueable-fix`，修复路径清晰。 |
| 3 | [#149361](https://github.com/openclaw/openclaw/issues/149361) Umbrella: WebUI 性能与稳定性 | 21 | 维护者自己开的伞形 Issue，汇总桌面端与移动端 WebUI 问题，子项如 [#149727](https://github.com/openclaw/openclaw/issues/149727)（测量滚动补偿触发额外历史加载）。说明前端性能已被正式纳入路线。 |
| 4 | [#139847](https://github.com/openclaw/openclaw/issues/139847) 回复进行中到达的消息被丢弃 | 15 | `"Reply operation has no active tool authority snapshot"` 是当前**最高频的报错字符串**，同一根因在 #148707、#144809 中重复出现，跨 2026.9.2/9.4 两个版本，用户感知为"内容静默丢失"。 |
| 5 | [#149538](https://github.com/openclaw/openclaw/issues/149538) main 分支网关 ready 但不可服务（P0） | 15 | 632-agent 集群上事件循环饥饿、`/health` 全部超时、RSS 持续上涨至 OOM，与 [#148529](https://github.com/openclaw/openclaw/issues/148529)（启动 12 分钟）同源，是最具破坏力的当前回归。 |
| 6 | [#127229](https://github.com/openclaw/openclaw/issues/127229) / [#137332](https://github.com/openclaw/openclaw/issues/137332) | 各 14 | Telegram 持久化更新被误 tombstone；终端 requester-settle 批次无限重试。 |
| 7 | PR [#151273](https://github.com/openclaw/openclaw/pull/151273) 插件代际替换停滞时保留旧代际服务 | — | 来自

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
**日期：2026-09-18** · 数据源：github.com/OpenHands/software-agent-sdk

> 数据说明：本报告基于提供的 GitHub 快照生成。PR 评论区数据缺失（显示为 undefined），Release Notes 存在截断（`feat(plu...`），因此部分条目以现有可验证信息为准，不对缺失内容做推测性延伸。

---

## 1. 今日速览

- **活跃度：高。** 过去 24 小时 Issues 更新 33 条（新开/活跃 21、关闭 12），PR 更新 50 条（待合并 43、已合并/关闭 7），并连续发布 **v1.49.1 / v1.49.2** 两个补丁版本。
- **主线聚焦 Docker 运行时加固**：今日关闭的 Issues 中有 6 条集中于 `OH_CONVERSATION_RUNTIME=docker`（#5127、#5129、#5131、#5136、#5139 等），两个 Release 也全部是 agent-server / Docker 相关修复，说明 Docker 化路径正处在密集收敛期。
- **生态标准化动作加速**：Agent Plugins（agent-plugins.org）母 Issue #4405 持续发酵，今日衍生出端到端测试（#5156，已关闭）与官方兼容客户端收录申请（#5159，开放）两条子任务。
- **出现批量"不变量"治理**：@juanmichelini 单日提交 7 条同族 Issue（#5144–#5150），围绕"LLM 请求必须先 system 后 user"的仓库级约束，属于典型的架构债清算信号。
- **健康度提示：** 待合并 PR 43 条 vs 已合并/关闭 7 条，Issues 净增约 +9 条，**评审吞吐与问题增量之间存在明显缺口**，是当前最值得关注的项目健康度风险。

---

## 2. 版本发布

### v1.49.2
- `fix(agent-server): preserve legacy conversations in Docker catalogs` — @neubig（[PR #5128](https://github.com/OpenHands/software-agent-sdk/pull/5128)）
- `fix(agent-server): stop rescanning Docker conversations` — @neubig（[PR #5137](https://github.com/OpenHands/software-agent-sdk/pull/5137)）
- `feat(plu...`（Release Notes 截断，内容不可确认）

### v1.49.1
- `fix(agent-server): preserve Docker conversation metadata route` — @neubig（[PR #5112](https://github.com/OpenHands/software-agent-sdk/pull/5112)）
- Release 流程提交 — @all-hands-bot（[PR #5113](https://github.com/OpenHands/software-agent-sdk/pull/5113)）

**破坏性变更：** 从可见的 Release Notes 看，两个版本均为 **patch 级修复**，未声明破坏性变更。
**迁移注意事项：**
1. 使用 `OH_CONVERSATION_RUNTIME=docker` 的自托管部署**建议立即升级**——v1.49.2 修复了旧有本地会话在切换到 Docker 运行时后"不可见"以及目录被反复全量重扫的问题（对应 Issues [#5127](https://github.com/OpenHands/software-agent-sdk/issues/5127)、[#5136](https://github.com/OpenHands/software-agent-sdk/issues/5136)）。
2. v1.49.1 → v1.49.2 间隔极短，属热修复节奏，升级路径无特殊步骤。

---

## 3. 项目进展

### 已合入并随版本发布的修复
| 主题 | PR | 解决的用户问题 |
|---|---|---|
| Docker 目录保留历史会话 | [#5128](https://github.com/OpenHands/software-agent-sdk/pull/5128) | [#5127](https://github.com/OpenHands/software-agent-sdk/issues/5127) 切 Docker 后历史会话消失 |
| Docker 会话目录不再全量重扫 | [#5137](https://github.com/OpenHands/software-agent-sdk/pull/5137) | [#5136](https://github.com/OpenHands/software-agent-sdk/issues/5136) 首页搜索性能问题 |
| Docker 会话元数据路由保留 | [#5112](https://github.com/OpenHands/software-agent-sdk/pull/5112) | 元数据读取链路 |

### 今日关闭的重要 Issues（项目实际推进量）
- **[#5129](https://github.com/OpenHands/software-agent-sdk/issues/5129)**（priority:medium）+ **[#5139](https://github.com/OpenHands/software-agent-sdk/issues/5139)**（priority:medium）：Docker 运行时拒绝新建 Canvas 会话工作区、根会话路径经 Docker 代理丢失 — Docker 可用性的关键阻塞项。
- **[#5131](https://github.com/OpenHands/software-agent-sdk/issues/5131)**：Docker 会话删除与 WebSocket 重连竞态。
- **[#5114](https://github.com/OpenHands/software-agent-sdk/issues/5114)**：`GET /api/conversations/search?limit>100` 返回 500（根因为查询约束拼写错误 + 用 `assert` 做校验）——典型低门槛高影响 API 缺陷。
- **[#5157](https://github.com/OpenHands/software-agent-sdk/issues/5157)**：`enable_sub_agents` 在显式传入 `tools` 列表时被静默忽略——配置语义不一致问题。
- **[#4941](https://github.com/OpenHands/software-agent-sdk/issues/4941)**：注册 `deepseek-v4.1-flash` 为验证模型，替换 `deepseek-v4-flash` 作为托管默认。
- **[#4453](https://github.com/OpenHands/software-agent-sdk/issues/4453)** / **[#5156](https://github.com/OpenHands/software-agent-sdk/issues/5156)**：Agent Plugins 路径包含（path-containment）安全边界 + 端到端一致性测试，均为母 Issue #4405 的关键交付物。

**整体判断：** 今日推进的核心是"**把 Docker 运行时的坑填平**"，且已通过 v1.49.x 落地到用户可获取的版本中，属于实质性前进；Agent Plugins 从规范讨论进入测试与合规阶段，是路线图上的第二增长点。

---

## 4. 社区热点

| 排名 | 条目 | 评论数 | 链接 |
|---|---|---|---|
| 1 | #4405 Spec: Support the Agent Plugins portable package format | 6 | [链接](https://github.com/OpenHands/software-agent-sdk/issues/4405) |
| 2 | #5100 Profile 预检误报 + 重试阻塞约 2 分钟 |

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-09-18

> 数据源：github.com/earendil-works/pi ｜ 统计窗口：过去 24 小时

---

## 1. 今日速览

项目今日处于**高强度维护状态**：24 小时内 Issues 更新 103 条，其中关闭 79 条、新开/活跃 24 条，关闭率高达 77%，说明维护者正在集中清理积压议题。PR 侧 14 条更新中 11 条合并/关闭、仅 3 条待合并，合并节奏健康。当日**无新版本发布**，但从合并内容看，一批围绕**压密（compaction）溢出、AI 重试语义、TUI 渲染稳定性**的修复正被快速纳入主干，为下一版本蓄势。社区热度集中在 `openai-codex` 连接可靠性（#4945，79 评论 / 33 👍）与 `PI_OFFLINE` 行为不一致（#8684）两个长期议题上。整体判断：**项目健康度良好，处于“修复密集期”，但 Provider 稳定性与上下文压缩仍是系统性风险区**。

---

## 2. 版本发布

当日无新版本发布，本节略。

---

## 3. 项目进展

今日共 **11 条 PR 完成合并/关闭**，覆盖 AI 层、coding-agent 层与 TUI 层。按影响面归纳：

### 3.1 AI 层健壮性提升（3 条）
- **[#9724] fix(ai): 为畸形 Retry-After 日期回退到指数退避** — 修复格式错误的 HTTP-Date 导致 `NaN` 延迟、429 重试立即触发的缺陷，并在 `validateServerRetryDelayMs` / `abortableSleep` 拒绝非有限值。
  https://github.com/earendil-works/pi/pull/9724
- **[#9722] fix(ai): 重试无诊断体的不透明 4xx 错误** — 此前网关返回裸 4xx（如 `400 status code (no body)`）会被快速判死，现纳入 `4\d{2} status code` 可重试模式。
  https://github.com/earendil-works/pi/pull/9722
- **[#9720] fix(ai): 通过 thinkingLevelMap 驱动 Mistral 推理调度，新增 zai-glm-5-3** — 移除硬编码模型 ID 白名单，改由 `model.thinkingLevelMap` 判断，提升新模型接入的可扩展性。
  https://github.com/earendil-works/pi/pull/9720

### 3.2 上下文压缩修复（1 条，关键）
- **[#9717] fix(coding-agent): 在压缩摘要中限制仅含 thinking 的消息** — 直接回应 #9602，防止仅思考类消息被完整序列化导致压缩请求体积远超真实上下文。这是压缩系列问题的核心修复之一。
  https://github.com/earendil-works/pi/pull/9717

### 3.3 扩展 API 与 TUI（3 条）
- **[#9630] feat(coding-agent): 新增事件处理器取消订阅** — `pi.on(...)` 支持 unsubscribe，且 dispatch 时对 handler 列表做快照，避免“飞行中”增删导致行为不确定。
  https://github.com/earendil-works/pi/pull/9630
- **[#9719] feat(tui): 默认工具 shell 垂直内边距可配置** — 新增 `toolShellPaddingY`（0/1，默认 1）。
  https://github.com/earendil-works/pi/pull/9719
- **[#9692] fix(tui): 裁剪溢出渲染行而非崩溃** — 修复 #9691，差分渲染路径遇到超宽行会抛未捕获异常并使整个会话崩溃，现改为裁剪。
  https://github.com/earendil-works/pi/pull/9692

### 3.4 跨平台与测试（3 条）
- **[#9693] test(coding-agent): 页脚 cwd 测试跨平台化**、**[#9694] test(ai): DeepSeek flash 模型引用更新为 v4**、**[#9706]/[#9705] eval 验证与 TUI 上下文页脚 eval**。

**整体推进度评估**：今日合并以“补漏 + 稳定性”为主，非大功能交付，但精准命中近两周的高频报错面（压缩溢出、重试逻辑、渲染崩溃）。这对降低下一版本的回归率有实质意义。

---

## 4. 社区热点

### 🔥 #4945 openai-codex 连接可靠性问题（OPEN / inprogress）
- 评论 **79** ｜ 👍 **33** ｜ 创建 2026-05-24 ｜ 更新 2026-09-17
- https://github.com/earendil-works/pi/issues/4945
- **诉求分析**：`openai-codex` / `gpt-5.5` 间歇性卡死在 TUI 的 `Working...`，无流式文本、无工具调用、无可见错误，唯一恢复方式是按 Escape（并留下 aborted 记录）。该议题已持续近 4 个月、热度居高不下，说明这是**长时间未能根治的连接层顽疾**，与 #9036（SSE 解析器整串缓冲导致堆 OOM）、#8331（流停滞永久挂起）构成同一族问题。用户的核心不满是**缺乏可诊断性与自动恢复机制**。

### #7836 编辑模糊匹配漏掉空白差异行（CLOSED）
- 评论 **12** ｜ 👍 1
- https://github.com/earendil-works/pi/issues/7836
- 小模型在编辑时因空白不一致导致 `oldText` 模糊匹配失败。已关闭，反映社区对**弱模型兼容性**的关注。

### #8684 `PI_OFFLINE` 静默禁用全部 Provider 模型发现（OPEN）
- 评论 **10** ｜ 👍 0
- https://github.com/earendil-works/pi/issues/8684
- 文档声称仅关闭启动期网络维护操作，实际却禁用整会话的模型目录发现，属**文档与行为不一致**的隐蔽陷阱，对企业/离线部署用户尤为敏感。

### #9361 Windows 下 `shellPath` 被非确定性忽略（OPEN）
- 评论 **6** ｜ 👍 0
- https://github.com/earendil-works/pi/issues/9361
- 加载扩展后 shell 解析回落到 WSL 的 `System32/bash.exe`，执行环境不可预期。Windows 用户的长期痛点。

### #8331 Provider 流停滞导致 agent loop 永久挂起（OPEN）
- 评论 **6** ｜ 👍 **2**
- https://github.com/earendil-works/pi/issues/8331
- 实际事故复盘（Anthropic 529 过载窗口），SSE 不再推送事件也永不关闭，`for await` 永久等待。属于**生产可用性级别的缺陷**。

---

## 5. Bug 与稳定性

按严重程度排列：

### 🔴 P0 — 会话崩溃 / 数据风险
| Issue | 描述 | 状态 |
|---|---|---|
| **[#9036]** | `openai-codex` SSE 解析器将整个响应缓冲为单一字符串，触发 V8 致命堆 OOM（macOS / Node 26.7.0） | OPEN，无 fix PR |
| **[#4945]** | Codex 连接卡死，TUI 无法自恢复 | OPEN，标记 inprogress |
| **[#8331]** | Provider 流停滞 → agent loop 永久挂起，需人工中断 | OPEN，无 fix PR |
| **[#9708]** | 会话迁移**就地重写**旧格式文件且**不做备份**，中断即可能损坏 | CLOSED（已归档 no-action） |

链接：https://github.com/earendil-works/pi/issues/9036 ｜ https://github.com/earendil-works/pi/issues/8331 ｜ https://github.com/earendil-works/pi/issues/9708

### 🟠 P1 — 上下文压缩系统性缺陷（本周焦点）
| Issue | 描述 | 状态 |
|---|---|---|
| **[#9602]** | 压缩时会包含此前请求已省略的 thinking 消息，导致溢出 | OPEN ｜ **已有 fix PR #9717 并已合并** ✅ |
| **[#9652]** | `/compact` 被 Anthropic Claude Fable 的 `reasoning_extraction` 分类器拦截（转写 thinking 块） | OPEN |
| **[#9391]** | 压缩后每轮重放过期已签名 thinking 块，Anthropic 每次 `prefix_binding_mismatch` | OPEN |
| **[#9512]** | GPT-6 Astra max reasoning 下压缩命中摘要输出上限，恢复失败 | OPEN |
| **[#9579]** | 溢出图像恢复使用固定 16 MiB 预算，超出小额度 Provider 限制 | OPEN |
| **[#9051]** | `session_compact` 自定义消息错过立即溢出重试 | OPEN |

链接：https://github.com/earendil-works/pi/issues/9602 ｜ https://github.com/earendil-works/pi/issues/9652 ｜ https://github.com/earendil-works/pi/issues/9391

### 🟠 P1 — 执行与结果正确性
- **[#9577] CLOSED** — `createBashTool` 在 shell 被 SIGKILL/SIGTERM 杀死时仍**成功 resolve**，调用方无法区分失败（关联 #8992/#8882 的遗留问题）。
  https://github.com/earendil-works/pi/issues/9577
- **[#4854] CLOSED** — OpenAI 兼容工具重放可发送空 `tool_call_id`，导致后续请求 400。
  https://github.com/earendil-works/pi/issues/4854

### 🟡 P2 — 兼容性 / 配置 / 数据一致性
- **[#9760 / #8760] CLOSED** — OpenRouter `:free` 模型因发送超限 `max_tokens` 一律 400。
  https://github.com/earendil-works/pi/issues/8760
- **[#9664] CLOSED** — `openai-responses` 在转译为 Chat Completions 的网关上第二轮 400（`output_text` vs `text`）。
  https://github.com/earendil-works/pi/issues/9664
- **[#9455] CLOSED** — Google GenAI `thinkingLevel:"MINIMAL"` 在 gemini-3.8-flash 上 400。
  https://github.com/earendil-works/pi/issues/9455
- **[#9654] CLOSED** — `read` 工具在仅请求一行时仍读入整文件，128 MiB 文件可致崩溃。
  https://github.com/earendil-works/pi/issues/9654
- **[#9609] CLOSED** — 会话时间戳为本地时间却带 `Z`（UTC）后缀，误导性强。
  https://github.com/earendil-works/pi/issues/9609
- **[#9566] CLOSED** — 自定义 `models.json` 中 id 命中已有模型时，context/cost/maxTokens 回退到错误的 128k 默认值。
  https://github.com/earendil-works/pi/issues/9566

### 🟢 已由今日 PR 直接修复
- **[#9692] fix(tui)** — 超宽渲染行崩溃 → 已合并 ✅
- **[#9724] fix(ai)** — 畸形 Retry-After 导致立即重试 → 已合并 ✅
- **[#9722] fix(ai)** — 裸 4xx 不重试 → 已合并 ✅
- **[#9717] fix(coding-agent)** — 压缩包含 thinking-only 消息 → 已合并 ✅

---

## 6. 功能请求与路线图信号

结合今日 PR 与 Issue，以下几项**落地概率较高**：

| 特性 | 相关 Issue

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目日报（2026-09-18）

---

## 1. 今日速览

LiteLLM 今日维持**极高活跃度**：过去 24 小时 296 条 PR 更新、75 条 Issue 更新，其中 103 条 PR 完成合并/关闭、27 条 Issue 被关闭，清理节奏明显。但**无新版本发布**，且 296 条 PR 中仅 103 条落地，193 条待合并，积压压力仍然较大。今日合并/关闭了大量 `stale` 标签的历史 Issue（fal.ai、DashScope、分层定价、MCP OAuth 回调等），显示维护者正在集中清理旧账。值得警惕的是，高热度 Issue（如无限 SSO、Prisma 重连失败）长期处于 OPEN 状态，社区诉求与修复进度存在错配。整体健康度评估：**高吞吐、高积压、机器人贡献占比显著**。

---

## 2. 版本发布

**今日无新版本发布。**

增量信号：PR #41704（CLOSED）将 `stable/1.101.x` 分支从 1.101.0 提升至 **1.101.1**，是继 #41698 通配符许可证修复后的补丁版本准备。该 PR 已关闭/合并，v1.101.1 可能即将正式发布。相关链接：https://github.com/BerriAI/litellm/pull/41704

---

## 3. 项目进展

今日合并/关闭的重要 PR 与 Issue：

**功能推进**
- **策略引擎执行顺序**（#41571 CLOSED）：为 policy attachment 引入显式 `priority` 字段，支持 model 级策略先于 tag 级执行，覆盖 config/API/DB/Admin UI。https://github.com/BerriAI/litellm/pull/41571
- **依赖版本修正**（#41706 OPEN）：修正 Python 最低依赖版本（Pydantic 等），解决声明最低版本实际无法导入/安装的问题。https://github.com/BerriAI/litellm/pull/41706

**安全与稳定性修复**
- **soupsieve 安全升级**（#41679 CLOSED）：从 2.8.4 升至 2.9.2，修复 GHSA-gjv8-xp57-g29c 与 GHSA-j934-xhv5-fg8f 两个 ReDoS 漏洞，此前 osv-scan 在每个 PR 上都会失败。https://github.com/BerriAI/litellm/pull/41679
- **Azure 同步部署定价 $0**（#41605 CLOSED）：修复 `azure_ai/gpt-5.6-luna` 成功请求间歇性记录 `$0.00000000` 的成本 bug。https://github.com/BerriAI/litellm/issues/41605
- **MCP OAuth2 回调 404**（#24771 CLOSED）：`/ui/mcp/oauth/callback` 不存在的页面问题关闭。https://github.com/BerriAI/litellm/issues/24771
- **cursor:// MCP 回调 schema**（#23339 CLOSED）：支持 Cursor 的 `cursor://` 回调重定向。https://github.com/BerriAI/litellm/issues/23339

**批量 stale 清理（今日关闭）**
- #16073 fal.ai 模型支持（Sora 2 / Veo 3.1）
- #23352 自定义 LLM provider 被内置同名模型静默绕过
- #24500 `include_subpath` + auth 关闭时子路径 401
- #30033 pass-through 请求按上游 URL 自动打标（Langfuse）
- #30135 `*_above_200k_tokens` 分层定价被忽略
- #28763 DashScope / 通义千问图像生成支持
- #30126 `/cursor/chat/completions` 未写入 SpendLogs
- #30667 流式 pass-through 中途失败不记录用量
- #25286 团队 MCP 访问组更新后虚拟 key 403
- #27830 自托管 vLLM 自动填充 max_input/output_tokens（12 👍）
- #41042 Bourse 作为 OpenAI 兼容 provider（重复关闭）

**整体推进评估**：今日以「清理积压 + 安全修复 + 成本准确性修复」为主线，未见重大新功能落地。103 条 PR 关闭量健康，但 193 条待合并显示主干前进速度受限。

---

## 4. 社区热点

| 排名 | 条目 | 评论/👍 | 链接 |
|---|---|---|---|
| 1 | #25762 标准版无限 SSO 登录 | 17 💬 / 27 👍 | https://github.com/BerriAI/litellm/issues/25762 |
| 2 | #26886 Prisma 重连失败 | 17 💬 / 11 👍 | https://github.com/BerriAI/litellm/issues/26886 |
| 3 | #16073 fal.ai 模型支持 | 13 💬 / 9 👍 | https://github.com/BerriAI/litellm/issues/16073 |
| 4 | #26071 私有仓库 Skills 认证（SSH/Token） | 11 💬 / 16 👍 | https://github.com/BerriAI/litellm/issues/26071 |
| 5 | #27830 vLLM 自动填充 max tokens | 2 💬 / 12 👍 | https://github.com/BerriAI/litellm/issues/27830 |
| 6 | #24771 MCP OAuth2 回调 404 | 6 💬 | https://github.com/BerriAI/litellm/issues/24771 |

**诉求分析**：
- **商业化与授权限制矛盾**（#25762）：标准版 5 用户 SSO 上限被 27 人点赞，是当前最强社区情绪点。用户在「正向使用」场景下被硬性限制，属于商业策略与产品体验的冲突，非技术 bug，但热度最高。
- **生产环境稳定性焦虑**（#26886）：Prisma 查询引擎进程周期性崩溃导致 proxy pod 不稳定，17 条评论说明这是企业级部署的高频痛点。
- **生态扩展诉求**：fal.ai、DashScope、Bourse、Cursor、MCP 私有仓库 skills 等，反映社区希望 LiteLLM 成为「全 provider 网关」而非仅 LLM 聚合层。

---

## 5. Bug 与稳定性

**按严重程度排列：**

**🔴 高严重**

1. **#26886 Prisma 重连失败**（OPEN，无 fix PR）
   Prisma 查询引擎进程崩溃，proxy pod 周期性不稳定，影响数据库持久化。17 评论、11 👍，创建于 2026-04-30，已持续 4.5 个月。
   https://github.com/BerriAI/litellm/issues/26886

2. **#36168 流式 usage 丢失**（OPEN，无 fix PR）
   最终 chunk 的 `choices` 非空时上游 `usage` 被丢弃，导致 `cached_tokens` 丢失、按全量输入费率计费——**直接造成成本超收**。
   https://github.com/BerriAI/litellm/issues/36168

3. **#41611 流式护栏分块绕过**（OPEN，无 fix PR，2026-09-17 新报）
   敏感值被拆分到两个 SSE chunk 时可绕过逐块检查，属于**安全护栏失效**。
   https://github.com/BerriAI/litellm/issues/41611

**🟠 中严重**

4. **#41450 Usage 页显示管理员预算**（OPEN）：所有被筛选用户都显示登录管理员自己的 `$3,000.0000 limit`，隐藏 unlimited，缺失预算周期——**计费可视化错误**。https://github.com/BerriAI/litellm/issues/41450
5. **#30314 `cache_control_injection_points` 被拒**（OPEN，stale）：embeddings 请求报 "extraneous key not permitted"。https://github.com/BerriAI/litellm/issues/30314
6. **#30504 Complexity router 添加失败**（OPEN，3 评论）：Admin UI "Add auto router" 报错。https://github.com/BerriAI/litellm/issues/30504
7. **#24065 Cloudflare Workers AI API 错误**（OPEN，stale）：Nemotron 3 Super 120B 配置失败。https://github.com/BerriAI/litellm/issues/24065
8. **#27759 pi.dev + ollama 工具调用异常**（OPEN）：接入 LiteLLM 后 tool call 输出异常。https://github.com/BerriAI/litellm/issues/27759

**🟢 已修复/关闭**

9. **#41605 Azure 定价 $0**（CLOSED）
10. **#29764 Anthropic count_tokens 硬编码 api.anthropic.com**（CLOSED，对应 fix PR #29765 OPEN）https://github.com/BerriAI/litellm/pull/29765
11. **#23352 自定义 provider 被绕过**（CLOSED）
12. **#24500 pass-through 子路径 401**（CLOSED）

---

## 6. 功能请求与路线图信号

结合今日 OPEN PR，以下需求**较可能进入下一版本**：

| 功能需求 | Issue | 对应 PR | 判断 |
|---|---|---|---|
| 每模型预算（创建用户时） | — | #41708 OPEN | 表单一致性补齐，落地概率高 |
| 预算结转（带上限） | #41693 | #41693 OPEN | 新增 `rollover_max_budget` 字段，商业价值明确 |
| RFC 8693 IdP JWT 令牌交换 | — | #41485 OPEN | Claude Code 场景，网关鉴权增强 |
| Amazon Transcribe pass-through 计费 | — | #41515 OPEN | 补齐非 LLM 计费能力 |
| TypeSafe Jev 复杂度路由器分类器 | — | #41615 OPEN | 路由智能化扩展 |
| JWT key mapping 缓存驱逐 | — | #41707 OPEN | 修复已删除身份仍可调用模型 |
| `/key/update` 允许未分配 key 挂载项目 | — | #41700 OPEN | 免密钥轮换迁移路径 |
| `--validate_config` dry-run | — | #41705 OPEN | CI 前置校验，运维刚需 |
| Issue 自动分类标签 | — | #41695 OPEN | 缓解人工 triage |
| Langfuse SDK v4 迁移 | — | #36741 OPEN | 已停留 1 个月+，急需推进 |

**长期高赞但尚无 PR 的关键需求**：
- #25762 无限 SSO（27 👍）—— 商业政策问题，非工程问题
- #26071 私有仓库 skills 认证（16 👍）
- #24109 `/info` 或 `/version` 端点暴露版本（1 👍，3 月提出至今未解决）
- #41595 `/v1/models` 未应用 Team 成员 `allowed_models`（2026-09-17 新报）

---

## 7. 用户反馈摘要

**真实痛点**

1. **企业授权受限**：标准版 5 用户 SSO 上限阻碍团队规模化采用（#257

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目日报 · 2026-09-18

> 数据来源：github.com/temporalio/temporal ｜ 统计窗口：过去 24 小时
> 说明：本期 PR 评论数在数据源中显示为 `null`（未采集到），因此"社区热点"与"用户反馈"部分改为基于变更影响面、作者反馈摘要与 Issue 评论正文进行推断，凡属推断均已标注。

---

## 1. 今日速览

1. **代码流水高、社区议题少**：24 小时内 PR 更新 48 条（待合并 40、已合并/关闭 8），而 Issues 仅 2 条（新开/活跃 1、关闭 1），呈"工程推进快、外部反馈平"的典型发行周期特征。
2. **主线集中在三个方向**：① 命名空间复制的 CHASM 化改造（一个 7 连发 PR stack）；② Task Queue User Data 复制的 Cloud 分支 backport 与可观测性；③ History 任务处理的限流/重试与状态加载优化。
3. **一个补丁版本落地**：v1.30.7 已发布，属 v1.30.x 维护线的构建流水线与稳定性 cherry-pick，无明显破坏性变更。
4. **一项规模化性能问题闭环**：NVIDIA 工程师报告的 PostgreSQL 复合游标分页退化（#11709）已关闭，由 #11712 修复。
5. **健康度评估：良好偏健康**。无新增崩溃/回归类 Issue，待合并 PR 积压量（40）偏高，其中含 2 条自 5 月起长期挂起的 stale PR，需关注合并吞吐能否跟上提交速度。

---

## 2. 版本发布

### v1.30.7（补丁版本）

**更新内容：**

| 变更 | 说明 |
|---|---|
| 同步 manual docker build action 到 v1.30.x 分支 | 由 @lina-temporal 提交，[PR #10976](https://github.com/temporalio/temporal/pull/10976) |
| 同步更新 `docker-bake.hcl` | [PR #10977](https://github.com/temporalio/temporal/pull/10977) |
| Cherry-pick #11090：为 matching 组件添加 panic handler | 原始描述在数据源中被截断（"Add panic handlers to matchin…"） |

**破坏性变更**：从变更清单看**无 API / 配置层面的破坏性变更**，属维护线补丁。

**迁移注意事项：**
- 自建容器镜像的用户需注意 `docker-bake.hcl` 与构建 action 的同步更新，建议重新拉取模板而非沿用本地旧版构建脚本。
- matching panic handler 属稳定性增强（由 panic 转为受控处理），升级后建议观察 matching 服务的重启率与 panic 相关日志指标是否消失。

**链接**：https://github.com/temporalio/temporal/releases

---

## 3. 项目进展

### 今日已合并/关闭的 PR（8 条，以下为可见的重点项）

| PR | 状态 | 推进内容 |
|---|---|---|
| [#11712](https://github.com/temporalio/temporal/pull/11712) | CLOSED | **PostgreSQL 分页改用行值（tuple）游标**，覆盖 history_node、history-node metadata、timer tasks 三类查询，直接修复 #11709。同时为 timer-task 持久化测试套件补充了游标时间戳多 task ID 场景。 |
| [#11807](https://github.com/temporalio/temporal/pull/11807) | CLOSED | **Visibility 归档去重**：为 S3/GCS 归档引入基于 SHA-256 的内容感知去重，哈希写入对象元数据，命中相同哈希则跳过上传，不同则覆写。属于存储成本优化。 |
| [#12132](https://github.com/temporalio/temporal/pull/12132) | CLOSED | **新增 `task_queue_user_data_replication_per_type_data_dropped` 指标**，在冲突解决丢弃 clockless 且 `PerType` 非空的 payload 时打点并告警，附丢弃侧、双方时钟、命名空间/Task Queue 上下文。 |
| [#12140](https://github.com/temporalio/temporal/pull/12140) | CLOSED | 扩展上述日志与指标描述，覆盖 "clockless 与更旧 clocked" 两种被丢弃情形，并补充表驱动测试。 |

> 另有 4 条合并/关闭 PR 未进入"评论数最多前 20"的可见列表。

### 在途重要工作（仍 OPEN，代表项目前向方向）

- **命名空间复制的 CHASM 化（7 步 stack）** — 今日最重的结构性改造：
  - [#12112](https://github.com/temporalio/temporal/pull/12112)（PR0）抽取共享复制 helper 至 `common/namespace/nsreplication`
  - [#12135](https://github.com/temporalio/temporal/pull/12135)（PR1a）仅落地 wire contracts 与生成 API，便于独立评审 schema 兼容性
  - [#12113](https://github.com/temporalio/temporal/pull/12113)（PR1b）实现 inert CHASM 命名空间变更组件与生命周期状态机
  - [#12125](https://github.com/temporalio/temporal/pull/12125)（PR3）在 `chasm` 模式下启用权威传输路径，跳过 legacy 复制
- **History 任务限流**：[#12094](https://github.com/temporalio/temporal/pull/12094) 新增 throttle-aware 重试控制器，按 (cause, namespace, priority) 分组独立令牌桶，置于 `history.taskThrottleControllerEnabled` 开关之后（默认关闭）。
- **性能优化**：[#12139](https://github.com/temporalio/temporal/pull/12139) 让 verify transition 任务在加锁与加载 mutable state 之前即可生成已发送的 verify 任务，避免不必要的 mutable state 加载。
- **动态分区**：[#12138](https://github.com/temporalio/temporal/pull/12138) 为 `PartitionScaleManagerSettings` 增加 `Mode`（disabled/shadow/enabled），默认 shadow，标志分区扩缩容从观测走向实际生效。
- **可观测性/链路**：[#12141](https://github.com/temporalio/temporal/pull/12141)、[#12091](https://github.com/temporalio/temporal/pull/12091)、[#12073](https://github.com/temporalio/temporal/pull/12073) 分别聚焦 CHASM 执行信息暴露、NexusHandler 回调双向链接、以及 Nexus reapply 对"两棵树都不拥有该 operation"的事件跳过而非整批失败。

**整体推进度判断**：本日进展以"夯实复制与分区两条底层路径 + 云分支回归修复"为主，属于**基础设施级演进**而非用户可见功能；单日 8 条合并量在 40 条待合并的背景下，合并吞吐相对紧张。

---

## 4. 社区热点

> ⚠️ 数据源未提供 PR 评论数与 reaction 数，无法按"评论最多/反应最多"排序。以下按**影响面与受众规模**排序。

1. **[Issue #12101](https://github.com/temporalio/temporal/issues/12101) — Make the history scanner run interval configurable via dynamic config**（OPEN，1 条评论，作者 @tsurdilo）
   唯一的新增活跃 Issue，也是今日唯一有外部讨论的议题。history scanner（"scavenger"）负责回收孤儿 history 分支，其清理阈值已可通过 `worker.historyS…` 动态配置，但**扫描运行间隔似乎仍不可调**。诉求明确且低风险。
2. **[PR #12094](https://github.com/temporalio/temporal/pull/12094) — throttle-aware retry controller for history task processing**
   触及所有使用共享命名空间配额（namespace budget）用户的限流行为，潜在影响面最大；目前靠 feature flag 隔离，也是评审关注度最高的类型。
3. **[PR #11712](https://github.com/temporalio/temporal/pull/11712) / [Issue #11709](https://github.com/temporalio/temporal/issues/11709) — PostgreSQL 分页游标**
   虽已关闭，但由 NVIDIA 生产环境提出，关系到大规模 PostgreSQL 部署的分页延迟，属"高价值已解决"热点。
4. **[PR #12138](https://github.com/temporalio/temporal/pull/12138) — Dynamic partitioning scale manager mode**
   分区扩缩容从 shadow 走向 enabled 的开关，对大规模多分区部署用户具有路线图意义。

---

## 5. Bug 与稳定性

**今日无新增 Bug / 崩溃 / 回归类 Issue 报告**（唯一新开 Issue 为 enhancement 类）。以下为可见的稳定性相关动态：

| 严重程度 | 项 | 状态 | Fix PR |
|---|---|---|---|
| **高（规模化性能退化）** | [#11709](https://github.com/temporalio/temporal/issues/11709)：PostgreSQL 上 `history_node` 正向分页把复合主键写成 `OR` 表达式，**未将游标作为索引下界**，导致返回一页所需工作量随游标前历史行数线性增长 | 已 CLOSED | ✅ [#11712](https://github.com/temporalio/temporal/pull/11712) 改用 row-value 比较 |
| **中（进程健壮性）** | v1.30.7 通过 cherry-pick #11090 为 **matching 组件增加 panic handler**，说明 matching 路径存在可触发 panic 的场景 | 已随 v1.30.7 发布 | ✅ 已包含 |
| **中（复制数据一致性可观测性缺失）** | Task Queue User Data 冲突解决时会静默丢弃 incoming `PerType` 数据，此前无指标暴露 | 已 CLOSED | ✅ [#12132](https://github.com/temporalio/temporal/pull/12132)、[#12140](https://github.com/temporalio/temporal/pull/12140) |

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*