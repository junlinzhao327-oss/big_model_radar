# OpenClaw 生态日报 2026-09-12

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-12 00:22 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报
**日期：2026-09-12** | 数据来源：github.com/openclaw/openclaw

---

## 一、今日速览

今日项目维持**极高活跃度**：24 小时内 Issues 更新 500 条（新开/活跃 272、关闭 228），PR 更新 500 条（待合并 268、合并/关闭 232），并发布 `v2026.9.4`。整体健康度呈现**"高吞吐 + 高升级摩擦"**的双面特征——更新/迁移类缺陷（update、doctor、plugin pin、handoff lease）占据了 P0 级 Issue 的绝大多数，且 2026.9.4 刚发布即出现"发布分支缺补丁"（#144742）与"托管更新回滚到已迁移状态"（#145192）等连锁问题。Gateway 事件循环阻塞（同步持久化 / 同步 PRAGMA 完整性检查）与子进程泄漏（僵尸进程）构成两条持续性的稳定性主线。值得肯定的是，维护者 @steipete 今日密集提交了十余个 macOS / Web UI / 依赖更新相关的修复与重构 PR，工程节奏明显在向"收敛回归面"倾斜。

---

## 二、版本发布

### v2026.9.4 已发布

**核心亮点：兼容性失败更新可回滚恢复**

> 当 schema 与配置校验证明回滚安全时，保留上一版本包，并连同先前配置与服务一并恢复；数据库迁移仍

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报（2026-09-12）

> 数据来源：`github.com/OpenHands/software-agent-sdk` ｜ 统计窗口：过去 24 小时
> 注：PR 评论数字段在本次数据中缺失（显示为 `undefined`），社区热点部分以 Issue 评论数为主要排序依据。

---

## 1. 今日速览

- **整体处于高活跃但"吞吐失衡"状态**：过去 24 小时有 20 条 Issue、50 条 PR 更新，但 PR 侧仅 4 条合并/关闭，**46 条待合并**，审查队列压力显著。
- **社区讨论集中在"Agent Profile 模型自描述性"与"子代理（Sub-agent）能力/事件可见性"两大主题**，由 @simonrosenberg 主导的一串架构类 Issue 形成明显的设计讨论集群。
- **安全与稳定性清理成效明显**：`ACPAgent` 跨提供方密钥物化（#4923）、`libtmux` 子进程日志泄漏密钥（#4951）、`LLM.modify_params` 过期移除（#4955）等 5 条 Issue 于今日关闭。
- **无新版本发布**，仓库稳定在 v1.47.0 附近，但多条 Issue 已标记 `release-note-required`，暗示下一版本将有用户可见变更。
- **风险点**：Windows 原生 PowerShell 终端"中毒"（#4963，`priority:high`）与严格 OpenAI 兼容提供方拒收空文本块（#4965）是今日新报的实质性缺陷，且暂无对应 fix PR。

---

## 2. 版本发布

**无新版本发布。** 今日无 Release 记录，本节略。

---

## 3. 项目进展

今日 4 条 PR 合并/关闭（明细未在数据集中展开），但通过 Issue 关闭情况可反推推进方向：

| 关闭 Issue | 主题 | 意义 |
|---|---|---|
| [#3979](https://github.com/OpenHands/software-agent-sdk/issues/3979) | Skills & MCP：去掉内嵌 profile skills，统一为服务端目录 + per-profile 引用 | 收敛了语义分裂的"双技能通道"，是 Profile 数据模型的一次重要归一化 |
| [#4923](https://github.com/OpenHands/software-agent-sdk/issues/4923) | `ACPAgent` 物化全部提供方文件密钥 | **安全修复**：注册任一 harness 不再影响其他 harness 的密钥可见性 |
| [#4951](https://github.com/OpenHands/software-agent-sdk/issues/4951) | 从 libtmux 子 logger 输出中脱敏密钥 | **安全修复**：`send-keys` 中的 API Key 不再落日志 |
| [#4955](https://github.com/OpenHands/software-agent-sdk/issues/4955) | 按 v1.47.0 截止期移除 `LLM.modify_params` | 解除 CI 弃用门禁失败，恢复 `main` 分支绿灯 |
| [#4936](https://github.com/OpenHands/software-agent-sdk/issues/4936) | 硬配额耗尽时不应重试退避、应直接切回退模型 | 已关闭，配套 PR [#4938](https://github.com/OpenHands/software-agent-sdk/pull/4938) 待合并 |

**推进评估**：今日的主线是"**债务清理与安全加固**"而非新功能落地。CI 弃用门禁修复（#4955）属于解除阻塞性进展；两个安全 Issue 的关闭提升了多 harness/多租户场景下的信任度。但从 46:4 的 PR 合并比看，**项目净前进量有限，瓶颈在审查端而非开发端**。

---

## 4. 社区热点

按 Issue 评论数排序：

1. **#3979（8 条评论，已关闭）** — [Skills & MCP 统一目录](https://github.com/OpenHands/software-agent-sdk/issues/3979)
   讨论最激烈的一条。核心矛盾是 `skills: list[Skill]`（完整对象，`mcp_tools` 可携带密钥）与 `skill_refs`（名称过滤，默认 `[]`）的语义不对称，且与 `mcp_server_refs` 的 `None` 默认值不一致。诉求：**降低 profile 模型的隐式复杂度，避免密钥随 profile 序列化泄露**。

2. **#3907（6 条评论，仍开放）** — [转发子代理内层事件到实时流](https://github.com/OpenHands/software-agent-sdk/issues/3907)
   `TaskToolSet` 派生的子代理运行在独立的 `LocalConversation` 中，其内部事件**永远不会进入父级实时事件流**，导致 agent-server 的 WebSocket 消费者在子代理工作期间"失明"。这是可观测性层面的真实痛点，且与 #4953 的能力边界问题同源。

3. **#4849（4 条评论）** — [从 ConversationState + StoredConversation 派生 ConversationInfo](https://github.com/OpenHands/software-agent-sdk/issues/4849)
   `ConversationInfo` 重复声明了约 20 个已存在于状态对象上的字段，`_compose_conversation_info()` 靠 `model_dump` 手工合并。诉求是**消除字段漂移风险**，属类型/架构债。

4. **#4671（3 条评论，Epic）** — [流式：分离线格式与持久事件记录](https://github.com/OpenHands/software-agent-sdk/issues/4671)
   指出流式文本走"持久事件回调链"与"Token delta 直投 PubSub"两条互不知晓的通道，**缺乏排序保证与统一追踪**。

5. **#4957（3 条评论）** — [放宽 shell 以减少 combined heredoc 被拒](https://github.com/OpenHands/software-agent-sdk/issues/4957)
   由 `all-hands-bot` 提交，观察到 `gpt-5.6` 等模型频繁触发 shell 拒绝，转而直接改文件。

**分析**：今日热点的共同底色是 **"Agent Profile 作为契约不够完整"**——客户端无法查询 profile 会得到哪些工具（#4958）、无法选择系统提示模板（#4956）、子代理可绕过 profile 的工具/MCP 限制（#4953，安全相关）、profile 模型不自描述导致客户端硬编码版本号（#4964）。这构成一个清晰的产品化信号：**Profile 正在从"配置项集合"演进为需要对外承诺的公共接口**。

---

## 5. Bug 与稳定性

按严重程度排列：

### 🔴 高优先级

- **[#4963](https://github.com/OpenHands/software-agent-sdk/issues/4963)（OPEN｜windows, priority:high, tools, release-note-required, ready-for-dev）**
  原生 Windows 上，持久 PowerShell 会话（`WindowsTerminal`）**一旦遭遇终止性错误或中断即被"永久毒化"**，后续命令全部失效。
  *Fix PR：暂未发现* ｜ 标签含 `ready-for-dev`，建议优先排期。

- **[#4923](https://github.com/OpenHands/software-agent-sdk/issues/4923)（CLOSED｜security）**
  `ACPAgent` 默认物化全部已注册提供方的文件密钥，注册新 harness 会改变所有其他 harness 的行为。**已关闭/修复**。

### 🟡 中优先级

- **[#4965](https://github.com/OpenHands/software-agent-sdk/issues/4965)（OPEN｜今日新报｜priority:medium, sdk, ready-for-dev）**
  `Message.to_chat_dict()` 会发出**空白 text block 与空 content 数组**，被严格的 OpenAI 兼容提供方以 HTTP 400/422 拒绝。
  *Fix PR：暂未发现*。影响面广（所有第三方兼容端），建议尽快跟进。

- **[#4934](https://github.com/OpenHands/software-agent-sdk/issues/4934)（OPEN｜priority:medium, llm）**
  SDK 向 `minimax/MiniMax-M3` 发送默认 `reasoning_effort=high`，LiteLLM 抛 `UnsupportedParamsError`，导致切换到 M3 后下一次 LLM 调用即失败。
  *Fix PR：暂未发现*。

- **[#4936](https://github.com/OpenHands/software-agent-sdk/issues/4936)（CLOSED｜llm）**
  确定性配额错误（`usage_limit_reached` / `insufficient_quota`）被纳入完整指数退避重试，而非立即回退。
  *Fix PR：[#4938](https://github.com/OpenHands/software-agent-sdk/pull/4938)（OPEN，等待合并）*。

### 🟢 低优先级 / 已有修复在途

- **[#4951](https://github.com/OpenHands/software-agent-sdk/issues/4951)（CLOSED｜security）** — libtmux 日志泄漏密钥，已修复。
- **[#4944](https://github.com/OpenHands/software-agent-sdk/issues/4944)（OPEN｜priority:low, testing）** — 行为测试 PR 评论复用了 "Integration Tests Results" 标题，易与常规集成测试混淆。
- **[#4582](https://github.com/OpenHands/software-agent-sdk/pull/4582)**（OPEN）— `FileEditor.insert` 在无尾换行文件 EOF 处插入会粘连末行，含 4 个回归测试。
- **[#4703](https://github.com/OpenHands/software-agent-sdk/pull/4703)**（OPEN）— LLM 生成标题未剥离内联 `<think>` 推理块。
- **[#4406](https://github.com/OpenHands/software-agent-sdk/pull/4406)**（OPEN）— mcp 2.x 下 `browser_use` 无法构造。
- **[#4490](https://github.com/OpenHands/software-agent-sdk/pull/4490)**（OPEN）— DeepSeek `prompt_cache_hit_tokens` 未计入遥测。
- **[#4412](https://github.com/OpenHands/software-agent-sdk/pull/4412)**（OPEN）— agent-server `close()` 强制取消 run task，导致客户端会话卡在 RUNNING。

**健康度判断**：安全类缺陷的响应速度良好（当日关闭 2 条）。但**平台兼容性缺陷（Windows、严格 OpenAI 兼容端、MiniMax）三条均无 fix PR**，是当前稳定性的主要敞口。

---

## 6. 功能请求与路线图信号

**强信号：Agent Profile 能力边界与自描述（很可能是下一版本主线）**

| Issue | 诉求 | 关联 PR / 判断 |
|---|---|---|
| [#4964](https://github.com/OpenHands/software-agent-sdk/issues/4964) | Profile 模型不自描述，客户端硬编码版本号猜测服务端接受的字段 | 类比 `

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报
**日期：2026-09-12**

---

## 1. 今日速览

LiteLLM 今日维持**极高开发活跃度**：24 小时内 PR 更新达 **303 条**（待合并 185、已合并/关闭 118），Issues 更新 48 条（新开/活跃 38、关闭 10），并发布 1 个 dev 版本。项目正处于密集迭代期，合并/关闭量接近待处理量的 2/3，说明维护团队响应速度较快、积压消化能力较强。社区热度集中在**安全事件追踪（#24518，119 评论/136 👍）**与多个 provider 兼容性问题（Bedrock、VLLM、Ollama）。同时，3 月旧 Issue 仍被持续更新，显示部分长期问题尚未完全闭环，项目健康度整体良好但技术债需关注。

---

## 2. 版本发布

### v1.102.0-dev.2（开发预发布版）

- **版本类型**：dev 预发布版，非稳定 release，建议仅用于测试环境验证。
- **核心内容**：强调所有 LiteLLM Docker 镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 签名，并与 commit [`0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0) 引入的密钥保持一致，用于供应链安全验证。
- **破坏性变更**：发布说明中未披露。
- **迁移注意事项**：dev 版本不建议生产直接升级；如需验证镜像签名，请按官方 cosign 流程执行 `cosign verify`，并核对签名密钥指纹与上述 commit 一致。

> 链接：https://github.com/BerriAI/litellm/releases

---

## 3. 项目进展

今日合并/关闭 **118 条 PR**，覆盖路由、UI、延迟追踪、CI 与价格同步等多个方向，项目整体向前推进明显：

| PR | 状态 | 内容 | 价值 |
|---|---|---|---|
| [#40788](https://github.com/BerriAI/litellm/pull/40788) | CLOSED | feat(proxy): 暴露复杂度路由（complexity routing）响应头 | 无需自定义 callback 即可观测 tier/cause/score/effort，提升路由可解释性 |
| [#29696](https://github.com/BerriAI/litellm/pull/29696) | CLOSED | fix(latency-routing): 修复延迟追踪器的丢失更新竞态 | 解决并发完成时的 read-modify-write 竞争，提升延迟路由准确性 |
| [#28761](https://github.com/BerriAI/litellm/pull/28761) | CLOSED | fix(ui): 会话日志抽屉侧边栏分页 + Shift+J/K 快捷键 | 修复 Log Details 静默截断至前 50 条的问题（关联 #28224） |
| [#29824](https://github.com/BerriAI/litellm/pull/29824) | CLOSED | fix(ci): create_daily_oss_agent_shin_branch 工作流 git push 认证 | 修复定时 CI 失败 |
| [#29829](https://github.com/BerriAI/litellm/pull/29829) | CLOSED | fix(auth): passthrough access groups 前增加 valid_token None 检查 | 修复 mypy 类型检查失败 |
| [#29833](https://github.com/BerriAI/litellm/pull/29833) | CLOSED | fix: Cloudflare Workers AI chat 响应解析 | 兼容 `result.choices[0].message.content` 形态 |
| [#29835](https://github.com/BerriAI/litellm/pull/29835) | CLOSED | fix(ci): 重复 Issue 检查对 Unicode 行分隔符健壮化 | 修复自动关闭步骤从未执行的问题 |
| [#29841](https://github.com/BerriAI/litellm/pull/29841) | CLOSED | 更新 OpenRouter Qwen3.7 / MiniMax 价格 | 价格数据准确性 |

**整体评估**：今日进展以「可观测性增强 + 稳定性修复 + CI 健壮化」为主线，同时清理了一批 6 月遗留的 stale PR，说明维护者在推进新功能（复杂度路由、Guardrails 集成）的同时也在系统性消化历史积压。

---

## 4. 社区热点

### 🔥 #24518 — 供应链安全事件追踪（119 评论 / 136 👍）
- 链接：https://github.com/BerriAI/litellm/issues/24518
- 状态：OPEN，创建于 2026-03-24，持续更新至 2026-09-11
- 摘要：Trivy 供应链投毒事件（影响 PyPI v1.82.7 / v1.82.8）已**受控**，受影响包已删除，当前版本无污染代码。官方已发布 [Security Townhall](https://docs.litellm.ai/blog/security-townhall-updates) 说明。
- **诉求分析**：这是社区最关心的议题，136 个 👍 反映用户对供应链安全的极高关注。用户期望获得完整时间线、影响范围清单与后续防护措施（如 SBOM、签名验证、CI 审计）。

### #19384 — Bedrock BedrockException（9 评论 / 5 👍）
- 链接：https://github.com/BerriAI/litellm/issues/19384
- 状态：CLOSED（stale）
- 摘要：Cursor + LiteLLM 场景下 Bedrock `toolConfig` 校验报 11 项错误。
- **诉求分析**：工具调用与 Bedrock 的兼容性长期痛点，虽已关闭但可能只是 stale 清理而非真正解决，建议关注是否有后续回归。

### #22984 — VLLM cached_tokens 成本计算（5 评论 / 5 👍）
- 链接：https://github.com/BerriAI/litellm/issues/22984
- 状态：OPEN
- 摘要：VLLM 作为 provider 时，token 成本计算未处理 cached tokens 信息。
- **诉求分析**：自托管 VLLM 用户的成本核算准确性需求，直接影响账单口径。

### #27300 / #27171 / #30208 — 预算与流式相关（4–5 评论）
- [#27300](https://github.com/BerriAI/litellm/issues/27300)（CLOSED）：月度重置后 `max_budget` 被忽略。
- [#27171](https://github.com/BerriAI/litellm/issues/27171)（CLOSED）：`budget_limits` 未序列化导致 `ResetBudgetJob` 全局崩溃。
- [#30208](https://github.com/BerriAI/litellm/issues/30208)（OPEN）：希望为所有 provider（至少 OpenAI）支持通用 fake streaming。

### #32353 — ReDoS 导致代理崩溃循环（3 评论 / 2 👍）
- 链接：https://github.com/BerriAI/litellm/issues/32353
- 状态：OPEN，创建于 2026-07-07
- 摘要：`secret_redaction.redact_string()` 在大异常字符串上发生灾难性正则回溯，阻塞事件循环数分钟，导致 liveness probe 失败、代理崩溃循环。
- **诉求分析**：生产级稳定性与安全性的高危组合问题，应优先处理。

---

## 5. Bug 与稳定性

按严重程度排列：

### 🔴 严重（可导致服务不可用）

| Issue | 描述 | Fix PR |
|---|---|---|
| [#32353](https://github.com/BerriAI/litellm/issues/32353) | ReDoS in `secret_redaction.redact_string()`，阻塞事件循环、崩溃循环 | ❌ 未见 |
| [#40564](https://github.com/BerriAI/litellm/issues/40564) | 终端用户预算重置超出 PostgreSQL 32,767 绑定变量限制，永不完成 | 已 CLOSED（需确认修复方式） |
| [#27171](https://github.com/BerriAI/litellm/issues/27171) | `budget_limits` 未序列化 → 全局 `ResetBudgetJob` 崩溃 | 已 CLOSED |

### 🟠 高（功能受损 / 数据丢失）

| Issue | 描述 | Fix PR |
|---|---|---|
| [#36426](https://github.com/BerriAI/litellm/issues/36426) | Responses-API bridge 丢弃非流式 `/v1/chat/completions` 的 SpendLogs 行 | ❌ 未见 |
| [#40582](https://github.com/BerriAI/litellm/issues/40582) | `parse_tool_call_arguments` 静默丢弃拼接 JSON 参数的 tool calls | ❌ 未见（`split_concatenated_json_objects` 已存在但未调用） |
| [#40675](https://github.com/BerriAI/litellm/issues/40675) | 客户端已设 `cache_control` 时，`cache_control_injection_points` 被整体丢弃 | ❌ 未见 |
| [#40761](https://github.com/BerriAI/litellm/issues/40761) | `store_model_in_db` 下 config 修改导致模型被驱逐且不恢复 | ❌ 未见 |
| [#40398](https://github.com/BerriAI/litellm/issues/40398) | JWT 认证每次刷新生成新 virtual key，Usage 页被污染 | ❌ 未见 |
| [#40654](https://github.com/BerriAI/litellm/issues/40654) | Responses-to-Chat bridge 流式/非流式丢失 `reasoning_text` | ❌ 未见 |
| [#40649](https://github.com/BerriAI/litellm/issues/40649) | Admin UI 模型编辑后 Azure 花费记录为 $0 | ❌ 未见 |

### 🟡 中（兼容性 / 配置问题）

| Issue | 描述 | Fix PR |
|---|---|---|
| [#40735](https://github.com/BerriAI/litellm/issues/40735) | `bedrock_converse` 拒绝携带 tool-call 历史但不重新声明 `tools` 的后续轮次 | ❌ 未见 |
| [#40080](https://github.com/BerriAI/litellm/issues/40080) | Bedrock 跨区域 GPT-5.6 图像输入失败（误走 Converse） | ❌ 未见 |
| [#40575](https://github.com/BerriAI/litellm/issues/40575) | Qwen3.8 tool result 在原生 Ollama provider 下未被消费 | ❌ 未见 |
| [#40563](https://github.com/BerriAI/litellm/issues/40563) | Vertex AI Realtime `pcm16` 采样率硬编码 24000，影响转写质量 | ❌ 未见 |
| [#40578](https://github.com/BerriAI/litellm/issues/40578) | OpenAI 兼容流式 `chunk_parser` 静默丢弃 in-band error 事件 | 已 CLOSED |
| [#40651](https://github.com/BerriAI/litellm/issues/40651) | `lite codex` 在子命令后传 `-c` 时静默绕过代理 | ❌ 未见 |
| [#34890](https://github.com/BerriAI/litellm/issues/34890) | `silent_model` 导致 Responses/Messages API 主请求 500 | ❌ 未见 |
| [#40728](https://github.com/BerriAI/litellm/issues/40728) | Azure AI Model Router 无成本追踪 | ❌ 未见 |
| [#31968](https://github.com/BerriAI/litellm/issues/31968) | `STORE_MODEL_IN_DB=True` 被 config 中 `store_model_in_db=false` 覆盖 | ❌ 未见 |

**整体观察**：今日报告的 Bug 集中在 **Bedrock/Converse 路径、工具调用参数解析、缓存控制注入、成本/花费记录**四类。多数无直接 fix PR，建议维护者优先处理 #32353（ReDoS）、#40582（tool calls 静默丢失）、#36426（SpendLogs 丢失）三个影响面最广的问题。

---

## 6. 功能请求与路线图信号

| Issue/PR | 需求 | 判断 |
|---|---|---|
| [#30208](https://github.com/BerriAI/litell

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目日报 · 2026-09-12

---

## 1. 今日速览

- **发布节奏强劲**：`v1.32.0` 正式发布，Standalone Activities 与 start delay 默认开启并 GA，是本期最重要的里程碑。
- **PR 吞吐量高**：过去 24 小时 49 条 PR 更新，其中 19 条合并/关闭、30 条待合并，合并闭环率约 39%，项目处于高速迭代状态。
- **Issue 侧相对平静**：仅有 2 条 Issue 更新（均为活跃讨论，无关闭），但其中包含一条高分老 Issue（#2617，13 👍）和一条潜在 bug（#9945）。
- **整体健康度**：活跃度 **高**，工程重心集中在 release 分支稳定性（v1.30/v1.31/v1.32 补丁）与 Nexus/SAA 等新能力收敛；需关注的是积压队列中存在多条被标记 `[stale]` 的 5 月 PR。

---

## 2. 版本发布

### v1.32.0 —— Standalone Activities 正式 GA

> 链接：https://github.com/temporalio/temporal/releases（v1.32.0）

**核心变化**

| 变更项 | 说明 |
|---|---|
| Standalone Activities GA | 通过 `activity.enableStandalone` 默认启用，无需再使用实验性开关 |
| Start Delay 默认开启 | 由 `activity.startDelayEnabled` 控制，支持延迟启动 |
| Operator APIs | 可对 Activity 执行 **暂停 / 恢复**，并可 **重置其 attempt** |
| 批处理操作 | 新增对 Activity 的批量运维能力 |
| Standalone Activities 支持范围 | 新增延迟启动、运维 API、批操作，覆盖此前仅 Workflow 具备的能力 |

**破坏性变更 / 迁移注意事项**

- `activity.enableStandalone` 与 `activity.startDelayEnabled` 默认值由 `false` 翻转为 `true`。**依赖旧行为做灰度或金丝雀的集群应在升级前显式复核动态配置**，避免 Standalone Activity 路径在生产意外放量。
- 新增 Operator API 与批处理接口属于 **能力扩展**，不构成 API 破坏，但配套 SDK/前端需同步版本以获得完整支持。
- 结合同期 PR #12023（合并 `NexusHandler` 变体回调支持）的描述中明确提到 "This will introduce a breaking change"，**调用 Nexus 回调的用户在跟进后续版本时需留意回调契约变化**。

**配套 release 分支动作**（同日）
- #12037 `[CLOSED]` 升级 `go.temporal.io/auto-scaled-workers` 至 `v0.0.0-1.31.2`（#12021 的回移）→ https://github.com/temporalio/temporal/pull/12037
- #12034 `[CLOSED]` Cloud/v1.32.0-163：修复 branch-token 分页问题（cherry-pick #11940、#11983）→ https://github.com/temporalio/temporal/pull/12034
- #12032 `[CLOSED]` 修复 release/v1.30.x 分支 CI，cherry-pick 六个测试修复 → https://github.com/temporalio/temporal/pull/12032

---

## 3. 项目进展

今日合并/关闭的 19 条 PR 中，以下几条对项目推进价值较高：

**① 修复 release/v1.30.x 分支 CI（#12032，已关闭）**
为 features job 设置 `component.nexusoperations.useSystemCallbackURL`，并回移 #9003 / #9489 / #9496 / #9514 / #9541 / #9587 六个测试修复。解决了分支切出后累积的三个无关失败，恢复了旧版本的可持续维护能力。
→ https://github.com/temporalio/temporal/pull/12032

**② 修复 branch-token 分页（#12034，已关闭）**
将 #11940 与 #11983 的 branch-token 错误与 stale-metadata 分页修复回移到 163 release 分支。这是一类典型的**分页游标 + 元数据过期**一致性缺陷，直接影响可见性与列表 API 的正确性。
→ https://github.com/temporalio/temporal/pull/12034

**③ 禁用 scaler 时清理 scaleInfo（#12035，已关闭，源自 #12026）**
此前禁用 scaler 时 `scaleInfo` 未被清除，导致客户端仍基于残留的 `scaleInfo.Read` / `scaleInfo.Write` 继续读写。修复后"关闭 scaler"成为干净、彻底的回落，避免自动扩缩容控制器状态污染。
→ https://github.com/temporalio/temporal/pull/12035

**④ 自动扩缩容 worker 依赖升级（#12037，已关闭）**
从伪版本升级到带 tag 的 `v0.0.0-1.31.2`，使依赖可追溯、可复现。
→ https://github.com/temporalio/temporal/pull/12037

**整体推进评估**：今日进展呈"两头并进"格局——一侧是 v1.32.0 GA 带来的能力面扩张（Standalone Activities、Operator API、批处理），另一侧是多条 release 分支的稳定性回移。**项目在功能与维护两个维度均明显向前推进，属于高产出日**。

---

## 4. 社区热点

### 🔥 #2617 按工作流完成类型设置保留期（13 👍 / 8 评论）
- 作者：@tsurdilo｜创建：2022-03-17｜更新：2026-09-11｜状态：OPEN
- 链接：https://github.com/temporalio/temporal/issues/2617

**诉求分析**：当前 retention period 仅按 namespace 维度配置，无法区分工作流"Completed"与"Failed"等完成类型。用户希望**对成功与失败的执行采用不同保留策略**——典型场景是失败工作流需要保留更久用于排障，而成功工作流可以更快清理以降低成本。该 Issue 已持续 **4 年半**，累计 13 个 👍，是社区长期高共识需求，也是当前讨论热度最高的条目。

### ⚠️ #9945 Matching 服务 Prometheus 指标基数无界增长（1 👍 / 4 评论）
- 作者：@Sanil2108｜创建：2026-04-14｜更新：2026-09-11｜状态：OPEN
- 链接：https://github.com/temporalio/temporal/issues/9945

**诉求分析**：用户期望 matching 的 Prometheus 基数应大致被 **活跃物理任务队列集合** 所约束（namespace × queue × task type × partition），但 `PhysicalTaskQueueManager` 卸载或任务队列空闲后，OTel gauge 仍持续累积标签组合。这是**可观测性层面的资源泄漏**，直接影响大规模集群的 Prometheus 存储与查询成本，属于运维人员高度敏感的议题。

---

## 5. Bug 与稳定性

按严重程度排序：

| 级别 | 问题 | 状态 | 是否有 Fix PR |
|---|---|---|---|
| 🟠 中高 | **#9945** Matching 服务指标基数无界增长（潜在内存/存储压力 + 监控成本） | OPEN | ❌ 暂无 |
| 🟠 中 | **#12008** 复制 reset 分支时 base workflow 锁提前释放，retention cleanup 可在 lookup 与 fork 之间介入，导致历史分支被清理 | OPEN | ✅ #12008 自身即修复 |
| 🟡 中 | **#11921** Nexus WF 更新的瞬时持久化读失败边界情况：workflow 已关闭、完成事件已记录于 `UpdateInfos`，但持久化读瞬时失败被误吞 | OPEN | ✅ #11921 含修复+测试 |
| 🟡 中 | **#11968** 执行关闭后 `SignalWithStart` 请求 ID 去重失效，重试会启动新 run 或重复投递 signal | OPEN | ✅ #11968 含修复，并新增 `SignalWithStartWorkflowStartDeduped` 指标 |
| 🟡 中 | **#12020** SAA（Standalone Activity）活动任务校验路由错误：需从 Matching 携带 CHASM 组件引用到 History | OPEN | ✅ #12020 自身即修复 |
| 🟢 低 | **#12012** Cassandra 分页场景下，重命名 namespace 可能被误报为物理删除，触发注册表条目误驱逐 | OPEN | ✅ #12012 自身即修复 |
| 🟢 低 | **#12001** search attribute 缓存刷新失败后并发读者重复发起被拒的 metadata 操作，缺少退避 | OPEN | ✅ #12001 自身即修复 |
| 🟢 低 | **#12036** namespace auto-forwarding 下，成功请求可能返回更早的 `NamespaceNotActive` 错误 | OPEN | ✅ #12036 自身即修复 |

**小结**：今日无崩溃级或线上回归级问题。8 项中 7 项已自带修复 PR，仅 **#9945 尚未有对应修复**，建议优先分派。整体看，今日新出现的问题集中在 **并发时序 / 缓存一致性 / 分页边界** 三类经典分布式陷阱上，反映出项目在复杂路径上的测试与防护持续加强（如 #11998 新增复制接收端暂停故障钩子、#11967 为被动复制测试引入严格状态校验）。

---

## 6. 功能请求与路线图信号

**已落地（v1.32.0）**
- ✅ Standalone Activities GA + Start Delay 默认开启
- ✅ Activity 级别的 pause / resume / reset attempt Operator API
- ✅ Activity 批处理操作

**高概率进入下一版本**
- **NexusHandler 变体回调统一（#12023）**：该 PR 是"添加 `NexusHandler` 变体完成回调到 Workflow、Workflow Update、Standalone Activity 及 Standalone Nexus Operation"的系列合并，此前这些实体完全不支持完成回调。已进入 review 且更新频繁，**建议关注其 breaking change 说明并提前规划 SDK 兼容**。→ https://github.com/temporalio/temporal/pull/12023
- **Cassandra GoCQL v2 迁移（#9993）**：驱动大版本升级，含 API 变更与废弃调用清理。这是一项基础设施级改造，一旦合并将影响所有 Cassandra 部署方，属于典型的"跨版本"事项。→ https://github.com/temporalio/temporal/pull/9993

**待观察（路线图信号）**
- **#2617 按完成类型设置保留期**：社区共识强（13 👍 / 4.5 年）但至今**无对应实现 PR**。考虑到 v1.32.0 已在 namespace 级 retention 之外扩展了 Activity 级运维能力，该需求在架构上具备可行性，建议纳入路线图评估。
- **#9945 指标基数治理**：虽以 bug 形式提出，实质是 matching 服务可观测性架构的功能性需求（需要引入 gauge 生命周期管理或标签清理机制）。

---

## 7. 用户反馈摘要

- **成本敏感度上升**：从 #2617（按完成类型差异化 retention）与 #9945（指标基数导致 Prometheus 成本膨胀）两条高关注 Issue 可看出，用户痛点正从"功能是否可用"转向**"运行成本是否可控"**——存储保留策略与监控

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*