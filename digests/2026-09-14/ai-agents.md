# OpenClaw 生态日报 2026-09-14

> Issues: 494 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-13 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报
**日期：2026-09-14** | 数据来源：github.com/openclaw/openclaw

---

## 1. 今日速览

- **活跃度维持高位**：过去 24 小时 Issues 更新 494 条（新开/活跃 285，关闭 209），PR 更新 500 条（待合并 229，已合并/关闭 271），属于典型的高吞吐维护日。
- **更新/升级可靠性是今日绝对主线**：P0 级 issue 集中在 2026.9.2 → 2026.9.4 迁移路径上（#146394、#145192、#147160、#145929，#145252 为跟踪索引），部分已导致服务停机或回滚失败。
- **稳定性债集中暴露**：僵尸子进程、消息静默丢失、上下文溢出恢复、会话状态错乱构成 P1 主题群，且多数标记为 `clawsweeper:no-new-fix-pr`，说明修复 PR 尚未成形。
- **无新版本发布**：今日 0 个 release，结合大量 P0/P1 未收敛，短期内发布节奏可能被质量门禁压制。
- **维护者直接参与修复**：steipete、vincentkoc、roboclaw-bot 等在当日提交多条修复/重构 PR，覆盖重启恢复、插件热重载、UI 与 doctor 性能。

---

## 2. 版本发布

今日无新版本发布（0 个 release），无 Releases 数据。

---

## 3. 项目进展

今日已合并/关闭的 PR 以**内部质量与性能收敛**为主，未见大型功能落地：

| PR | 状态 | 推进内容 | 链接 |
|---|---|---|---|
| #147467 | CLOSED | `perf(plugins)`：避免对 artifact 目录做多余的 state 探测，减少热缓存查找时的文件系统开销 | https://github.com/openclaw/openclaw/pull/147467 |
| #147464 | CLOSED | `fix(doctor)`：在大型 SQLite transcript 上提前终止校验，避免无谓的 JSON 解码与内存占用 | https://github.com/openclaw/openclaw/pull/147464 |
| #146695 | CLOSED | `refactor`：将 provider setup 的选项构建统一到现有 flow owner，移除冗余路径 | https://github.com/openclaw/openclaw/pull/146695 |

**待合并队列中的重要推进**（尚未合并，但方向明确）：

- #147486 `fix: resume interrupted work when new messages arrive after restart`（维护者 steipete）— 修复 Gateway 重启后 "restart recovery claim changed before agent adoption" 导致的中断工作卡死。https://github.com/openclaw/openclaw/pull/147486
- #147472 `fix: preserve pending chats during plugin hot reload` — 修复插件热重载导致已接受聊天请求被标记为 "Interrupted before the agent started it"。https://github.com/openclaw/openclaw/pull/147472
- #145117 `fix(gateway): persist durable terminal receipts` — 将 terminal `agent.wait` 结果从进程内存下沉为持久化回执，直接影响重启后运行状态判定。https://github.com/openclaw/openclaw/pull/145117

**整体前进度评估**：今日项目在"关闭旧账"（209 issue 关闭、271 PR 合并/关闭）上表现积极，但新增/活跃量（285 issue、229 PR 待合并）几乎持平或更高，净积压未显著下降，属**高强度清理但仍在追赶**的状态。

---

## 4. 社区热点

按评论数与 👍 排序的 Top 讨论：

1. **#25592 — 工具调用之间的文本泄漏到消息渠道**（40 评论，1 👍，P1，🦞 diamond lobster）
   https://github.com/openclaw/openclaw/issues/25592
   自 2026-02-24 起持续 6 个多月未关闭。Agent 在工具调用之间产生的内部处理文本（错误处理、确认语、叙述）被路由为 Slack/iMessage 等渠道的可见消息。诉求核心是 **内部推理输出与用户可见输出的边界隔离**，同时叠加 `impact:security` 标签，说明被视为信息泄露风险。

2. **#97616 — Hook/Tool 子进程未回收，僵尸进程累积**（30 评论，P1）
   https://github.com/openclaw/openclaw/issues/97616
   长时间运行实例上 `openclaw-hooks`、`bash`、`codex` 等子进程成为僵尸，导致运行时性能退化。属于长时间驻留部署的典型稳定性问题。

3. **#44925 — Subagent 完成静默丢失（无重试、无通知、无自动重启）**（28 评论，2 👍，P1，🦞 diamond lobster）
   https://github.com/openclaw/openclaw/issues/44925
   Telegram forum bot 场景下，子 Agent 任务结果静默丢失，存在多种失败模式（completion announce 失败 E31/E42/E45 等）。反映**多 Agent 编排的可观测性缺失**。

4. **#135111 — 间歇性 "malformed JSON arguments"（claude-sonnet-5）**（27 评论，已关闭，P1，🐚 platinum hermit）
   https://github.com/openclaw/openclaw/issues/135111
   自 v2026.8.1 升级后约 6 次/天出现，已关闭，说明修复或缓解措施已落地。

5. **#119720 — 同步 Agent 持久化阻塞 Gateway 事件循环**（19 评论，P1，🦞 diamond lobster）
   https://github.com/openclaw/openclaw/issues/119720
   在规模化场景下，同步的 transcript 维护阻塞事件循环，已有 #140231、#138984 部分修复，但问题仍开放。

**诉求分析**：热点高度集中于**"静默失败"**这一类问题——消息丢失、结果丢失、内部文本外泄。用户并不排斥功能缺失，但无法容忍"看起来正常、实则丢数据"的行为，这直接侵蚀对 Agent 平台的信任基础。

---

## 5. Bug 与稳定性

### P0 — 阻断级（更新/升级与凭据）

| Issue | 状态 | 摘要 | Fix PR |
|---|---|---|---|
| #146394 | OPEN | 2026.9.3 `global-install-failed` 更新失败，linux/arm64 | 无 |
| #145252 | OPEN | [Tracking] 2026.9.3/9.4 更新、升级、Doctor、回滚、重启可靠性协调索引 | 跟踪类 |
| #145192 | OPEN | macOS 2026.9.2→9.4 在 candidate-Doctor 因 v1 handoff lease 拒绝，回滚后落在 9.4 已迁移状态 | 无 |
| #147160 | OPEN | 2026.9.4 `finalize:doctor` 更新失败（darwin/x64） | 无（需更多信息） |
| #145929 | OPEN | 一次被中断的自更新后，auth profile logout/write 永久失败（lock-may-be-busy） | 无 |
| #140162 | CLOSED | Windows gateway restart 在 181s 超时后杀死正在启动/已就绪的 gateway | 已关闭 |
| #145563 | CLOSED | WeChat 渠道回复分发因 `PreparedModelCatalogConfigReplacedError` 全部失败 | 已关闭 |
| #146958 | CLOSED | 2026.9.2→9.3 更新在 llm-task 包属主元数据处失败，服务停摆 | 已关闭 |

> **判断**：更新链路的 P0 密度是今日最突出的健康度风险。多条报告均指向 "Doctor 校验阶段拒绝 + 回滚后状态不一致"，属于**发布流程本身的正确性问题**，而非单一平台问题。

### P1 — 高严重度

| Issue | 类别 | 摘要 | Fix PR |
|---|---|---|---|
| #144911 | crash-loop | stdio MCP server 初始化超时引发未处理 Promise 拒绝，**整个 Gateway 崩溃** | 标记 `fix-shape-clear`/`queueable-fix`，可排队修复 |
| #139847 | message-loss | 回复运行中到达的消息被丢弃（"no active tool authority snapshot"，2026.9.2 回归） | 标记 `queueable-fix` |
| #137332 | session-state | 混合 terminal requester-settle 批次在归属检查后永久重试 | 标记 `queueable-fix` |
| #145152 | message-loss | 卡死会话恢复把 force-clear 报告为 abort，未标识 run/owner 身份 | 标记 `queueable-fix` |
| #132765 | message-loss | `agents_wait` 忽略 `timeoutSeconds`，约 60s 后以工具错误终止 | 无 |
| #141474 | session-state | Collector 子进程调用 `sessions_yield` 使 `agents_wait` 永久搁浅；`outputSchema` 在 claude-cli 后端静默失效 | 无 |
| #101929 | data-loss | context-overflow 预检查高估 token 约 2.3–2.6×，误触发截断 | 无（`fix-shape-clear`） |
| #113701 | session-state | 大工具输出超上下文窗口，compaction 无法恢复，会话进入失败循环 | 无 |
| #81182 | session-state | 溢出恢复应先截断工具结果，而非等待 900s 自动 compaction 超时 | linked-pr-open |
| #86214 | message-loss | Codex app-server 客户端在图像/工具请求中途关闭（大 logs_2.sqlite） | 无 |
| #25592 | security | 工具调用间文本泄漏到消息渠道 | linked-pr-open |
| #97616 | crash-loop | 子进程僵尸累积，运行时退化 | 无 |
| #44925 | data-loss

---

## 横向生态对比



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



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报
**日期：2026-09-14** ｜ 数据源：github.com/BerriAI/litellm

---

## 1. 今日速览

LiteLLM 今日维持**极高活跃度**：24 小时内 51 条 Issue 更新、500 条 PR 更新，并发布 1 个 RC 版本。但活跃度与吞吐量严重不对称——Issues 新开/活跃 37 条对已关闭 14 条（净增 23），PR 待合并 484 条对已合并/关闭 16 条（**合并率仅约 3.2%**），积压压力进一步扩大。今日动向集中在**安全与数据正确性修复**（guardrail 绕过、embeddings index 错乱、认证信息泄露）与**计费准确性**（Vertex rerank、缓存 token、预算预留）。项目最大战略信号仍是 **Rust 迁移**（#31263，26 条评论、20 👍），热度远超其他议题。

---

## 2. 版本发布

### v1.102.0-rc.1（预发布）

- 链接：https://github.com/BerriAI/litellm/releases
- **版本性质**：RC（Release Candidate），非稳定版，不建议生产直接升级。
- **已披露内容**：本次发布公告主体为**供应链安全说明**——所有 LiteLLM Docker 镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 签名，签名密钥沿用 commit [`0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0) 引入的同一密钥，并附带验证步骤。
- **破坏性变更 / 迁移注意事项**：本次提供的数据中**未包含**功能变更清单、破坏性变更说明或迁移指引，无法确认。建议运维团队以官方 release note 与 `v1.102.0` 正式版公告为准。
- **运维提示**：若 CI/CD 中启用了镜像签名校验，需确认 cosign 公钥与上述 commit 一致，否则拉取新 RC 镜像会校验失败。

---

## 3. 项目进展

今日已合并/关闭 PR 共 16 条，但公开数据中仅 1 条明确标记为 `CLOSED`，未披露其余合并明细。以下为可见的重点推进项：

| PR | 状态 | 推进内容 |
|---|---|---|
| [#41015](https://github.com/BerriAI/litellm/pull/41015) | CLOSED | 修复 versioned Vertex Claude ID 被静默套用 4096 max_tokens 默认值（应为 8192+）。该 PR 系 supersede 前序 #40376 后关闭，24 个单测通过 |
| [#41019](https://github.com/BerriAI/litellm/pull/41019) | OPEN | 修复 `litellm_internal_staging` 上 Postgres 测试红灯（DEFAULT_IN_MEMORY_TTL 竞态）、TQ003 测试质量门禁、UI 类型同步——**CI 健康度修复** |
| [#41018](https://github.com/BerriAI/litellm/pull/41018) | OPEN | 稳定分支回移：阻止内部 litellm 参数（如 `model_alias_map`）泄漏进 provider 请求体，修复 GPT-5.4 + function tools 的 400 错误 |
| [#40938](https://github.com/BerriAI/litellm/pull/40938) | OPEN | 新特性：Bedrock / Bedrock Mantle 原生端点直通，跳过 Invoke / Converse / Responses-to-chat 翻译层，减少字段丢失 |

**整体推进评估**：今日主要进展是**修复性维护与 CI 稳定化**，而非新功能落地。484:16 的待合并比例表明社区贡献速度远超维护者评审带宽，项目"向前迈进"的净速度受评审资源制约。

---

## 4. 社区热点

### 🔥 #31263 — Rust Migration：the fastest and litest AI Gateway（sub 1ms overheads）
- 评论 **26** ｜ 👍 **20** ｜ 2026-06-25 开，2026-09-13 仍有更新
- https://github.com/BerriAI/litellm/issues/31263
- 作为 Rust 迁移的**母票（parent ticket）**，作者为 @ishaan-berri。关联博客 https://docs.litellm.ai/blog/litellm-rust-launch 与 Beta 测试者招募表单。
- **诉求分析**：社区对 Python 网关的**延迟与吞吐天花板**有明确不满，"sub 1ms overhead" 直指代理层性能。这是项目当前最具战略性的方向，也解释了为何大量 Python 层 PR 长期滞留——部分修复可能被 Rust 重写覆盖。

### #26097 — 自托管安装因 `prisma generate` 失败（stale）
- 评论 **7** ｜ 👍 **4** ｜ https://github.com/BerriAI/litellm/issues/26097
- 基础安装脚本被 prisma 权限阻断，属**入门体验阻塞型**问题，长期挂 stale 标签但仍有讨论。

### #40583 — guardrail 无法拦截 Anthropic `/v1/messages` 格式的 MCP 工具
- 评论 **5** ｜ https://github.com/BerriAI/litellm/issues/40583
- `custom_code` 与 `tool_permission` guardrail 在 pre_call 模式下**看不到也无法阻断** Anthropic 兼容端点发出的 MCP 工具调用，属安全语义缺口。已有 fix PR [#41011](https://github.com/BerriAI/litellm/pull/41011)。

### #27949 — OWASP ASI06 记忆投毒防御（stale）
- 评论 **5** ｜ https://github.com/BerriAI/litellm/issues/27949
- 针对 agent 跨会话持久记忆的投毒威胁，希望 LiteLLM 提供集成级防御。

### #40887 — Responses-to-Chat 流式丢失 reasoning 进度
- 评论 **4** ｜ https://github.com/BerriAI/litellm/issues/40887
- 桥接层只在 `response.completed` 附加 `reasoning_items`，未映射增量 reasoning item。

**热点共性**：社区焦点已从"多模型接入"转向 **agent 工作流可靠性 + 安全治理 + 代理层性能**，这三者是下一阶段的核心叙事。

---

## 5. Bug 与稳定性

按严重程度排列（🔴 高 / 🟠 中 / 🟡 低）：

### 🔴 高严重度

**1. `/v1/embeddings` 缓存命中混批时返回重复 `index`** — [#41002](https://github.com/BerriAI/litellm/issues/41002)（新报，1 评论）
- 单请求内混合"已缓存输入"与"新输入"时，返回 HTTP 200、JSON 合法、向量数量正确，但 `index` **重复或错误**。任何按 index 映射 `data` 的 OpenAI 兼容客户端会拿到错位向量——**静默数据损坏**，最危险的一类 Bug。暂无 fix PR。

**2. 预算预留被跳过，并发超支风险** — [#35524](https://github.com/BerriAI/litellm/issues/35524)
- 无法估算正向最大成本时，乐观预算预留路径**直接返回不预留**。成本不可估的模型/路由在并发下可突破已配置预算。暂无 fix PR。

**3. Guardrail 可被 Anthropic 格式绕过** — [#40583](https://github.com/BerriAI/litellm/issues/40583)
- 见社区热点。**已有 fix PR [#41011](https://github.com/BerriAI/litellm/pull/41011)**（pre_call 改用共享 Anthropic 工具名解析）。

**4. 401 响应泄露内部表名与完整 key 哈希** — 修复 PR [#39787](https://github.com/BerriAI/litellm/pull/39787)（OPEN）
- 错误 key 的 401 会回显内部 key 表名并附带提交 key 的 SHA-256 全量哈希。安全加固 PR 已就绪但尚未合并。

### 🟠 中严重度

| 问题 | Issue | fix PR |
|---|---|---|
| Responses-to-Chat 流式丢失 reasoning 进度与缓存 reasoning 状态 | [#40887](https://github.com/BerriAI/litellm/issues/40887) | 相关 [#41014](https://github.com/BerriAI/litellm/pull/41014)、[#31332](https://github.com/BerriAI/litellm/pull/31332) |
| 流式 usage

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*