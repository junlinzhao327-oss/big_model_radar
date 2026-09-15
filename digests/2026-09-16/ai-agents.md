# OpenClaw 生态日报 2026-09-16

> Issues: 470 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-15 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报

**日期：2026-09-16** ｜ 数据来源：github.com/openclaw/openclaw

---

## 一、今日速览

- **活跃度评级：极高（异常繁忙）**。过去 24 小时 Issues 更新 470 条（新开/活跃 297、已关闭 173），PR 更新 500 条（待合并 331、已合并/关闭 169），单日维护吞吐量处于高位，但新增与积压几乎同速增长。
- **无新版本发布**，当前 stable/beta 线均为 `2026.9.4 (3a9d69d)`；但围绕 2026.9.3→2026.9.4 升级失败的多个 P0 报告同日被关闭，说明发布链路问题正在收口。
- **核心矛盾集中在 Gateway 稳定性**：内存泄漏、僵尸/泄漏子进程、WAL 膨胀、崩溃循环等 P0/P1 问题占据了今日讨论热度榜前列。
- **安全与会话状态类问题值得警惕**：内部文本泄漏到消息频道、权限读取门控、以及大量 “no active tool authority snapshot” 回复丢失回归，均与 `impact:security` / `impact:session-state` 相关。
- 项目整体健康度：**维护响应积极，但发布时间线与核心稳定性仍承压**，多个长期 P1 问题（如 #25592）持续活跃近 7 个月仍未闭环。

---

## 二、版本发布

今日无新版本发布（最新 Releases 为空）。

---

## 三、项目进展

> 注：本次采样的 30 条 PR 均为 `OPEN` 状态，故无法逐条列举“已合并”PR；以下进展主要依据今日 **已关闭 (CLOSED)** 的重要 Issue 反映。

今日关闭的 Issue 集中在**更新链路与崩溃循环**两类高优先级问题上，显示维护者正在系统性清理 2026.9.x 发布期的稳定性欠账：

| Issue | 优先级 | 主题 | 链接 |
|---|---|---|---|
| #148866 | P0 | Gateway 永久重启循环（`gateway.bind=lan`，Ubuntu/systemd）已关闭 | [链接](https://github.com/openclaw/openclaw/issues/148866) |
| #148614 | P0 | 更新失败 `runtime-verification-failed`（2026.9.3）已关闭 | [链接](https://github.com/openclaw/openclaw/issues/148614) |
| #123326 | P0 | 显式多智能体 Codex 迁移导致 Gateway 启动崩溃循环（maintainer issue）已关闭 | [链接](https://github.com/openclaw/openclaw/issues/123326) |
| #115367 | P1 | 特权聊天面（slack/discord/matrix/msteams/feishu）读取被锁死在当前会话的安全边界问题 | [链接](https://github.com/openclaw/openclaw/issues/115367) |
| #145152 | P1 | 卡死会话恢复被误报为 abort、释放回复通道逻辑错误 | [链接](https://github.com/openclaw/openclaw/issues/145152) |
| #80520 | P1 | Telegram 消息静默丢弃、无 sendMessage 日志 | [链接](https://github.com/openclaw/openclaw/issues/80520) |

**推进方向判断**：更新演练（candidate migration / Doctor rehearsal）与启动恢复路径是今日关闭批次的共同主线，对应 PR 侧也有直接修复在队列中：
- #149449 `fix(update): avoid rehearsal failures while databases are active` — 针对更新演练中 SQLite WAL 活跃导致快照/清单失败的修复，[链接](https://github.com/openclaw/openclaw/pull/149449)
- #149455 `fix: unblock core lint for update handoff tests` — 解除主分支 lint 阻塞（含 700 行上限问题），[链接](https://github.com/openclaw/openclaw/pull/149455)
- #149370 `fix: prevent rejected queued handoffs from replaying` — 防止被拒绝的排队交接在恢复时重放，[链接](https://github.com/openclaw/openclaw/pull/149370)

整体看，项目今日**更偏“止血”而非“上新”**：没有新功能落地，主要精力用于修复 9.x 系列的升级与启动路径。

---

## 四、社区热点

今日讨论最活跃的 Issue（按评论数）：

1. **#25592 — 工具调用之间的文本泄漏到消息频道**（40 评论 ｜ P1 ｜ 🦞 diamond lobster ｜ `impact:security`）
   内部处理输出（错误

---

## 横向生态对比

# 个人 AI 助手 / 自主智能体开源生态横向对比分析
**日期：2026-09-16**  
**说明：Hermes Agent、Pi、Temporal 本次摘要为空；OpenClaw、OpenHands SDK、LiteLLM 部分内容被截断。以下分析基于可见数据，未对缺失项目做推断。**

---

## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态仍处于**高活跃、强迭代、但稳定性与安全欠账集中暴露**的阶段。头部项目单日 Issue/PR 吞吐量可达数百条，维护者主要精力从“加功能”转向“止血”：Gateway 崩溃循环、内存/子进程泄漏、会话状态丢失、凭据泄漏、计费不准成为共同焦点。安全与凭据治理正从附属能力上升为核心架构议题，多个项目同日关闭高危密钥/权限类 Issue。与此同时，LLM 网关层的成本核算、限流一致性和流式 fallback 可靠性，正在成为智能体生产化的信任基础。整体看，生态尚未形成统一的兼容性、可观测性和安全运行时标准，各项目仍以“自建闭环”为主。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | Release | 健康度评估 |
|---|---:|---:|---|---|
| **OpenClaw** | 470（活跃 297 / 关闭 173） | 500（待合并 331 / 合并关闭 169） | 无新版本，stable/beta 均为 `2026.9.4` | 极高活跃；社区规模最大；但发布线与核心稳定性承压，更新链路“止血”中 |
| **OpenHands SDK** | 24（活跃 14 / 关闭 10） | 50（待合并 46 / 合并关闭 4） | **v1.48.0** | 高活跃；安全收口明显；PR 合并/待处理比约 1:11.5，评审带宽瓶颈突出 |
| **LiteLLM** | 67（活跃 52 / 关闭 15） | 334（待合并 215 / 合并关闭 119） | **v1.101.0** | 极高活跃；自动化小步快跑；计费/限流/流式 fallback 仍存系统性风险 |
| **Hermes Agent** | 未提供 | 未提供 | 未提供 | 无数据 |
| **Pi** | 未提供 | 未提供 | 未提供 | 无数据 |
| **Temporal** | 未提供 | 未提供 | 未提供 | 无数据 |

**横向观察**：  
- OpenClaw 单日 Issues/PR 总量最高，是生态中最活跃的协作场。  
- LiteLLM PR 吞吐量极高，且自动化 Agent 账号参与明显，工程流水线成熟度较高。  
- OpenHands 虽体量较小，但关闭了多项安全与崩溃类高优先级 Issue，处于质量巩固阶段。  
- 三者均存在待合并 PR 显著高于已合并/关闭的情况，维护评审带宽是共性瓶颈。

---

## 3. OpenClaw 在生态中的定位

**优势：**
- **社区规模最大**：单日 Issues 470、PR 500，远超 OpenHands SDK（24/50）和 LiteLLM（67/334），是生态核心参照。
- **集成

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报
**日期：2026-09-16** | 数据源：github.com/OpenHands/software-agent-sdk

---

## 1. 今日速览

- **活跃度：高。** 过去 24 小时 Issue 更新 24 条（新开/活跃 14、关闭 10）、PR 更新 50 条（待合并 46、已合并/关闭 4），并发布 1 个新版本 v1.48.0。
- **合并/关闭比严重失衡**：待处理 PR（46）与已合并/关闭 PR（4）之比约 11.5:1，PR 队列积压明显，维护者评审带宽可能成为瓶颈。
- **安全与凭据治理是今日主线**：多条涉及明文密钥、会话令牌暴露、CI 依赖管控的高优先级 Issue 集中更新或关闭。
- **修复节奏稳健**：10 条 Issue 关闭中包含 #5082（pickle 崩溃）、#4399（密钥明文写入 .git/config）等高优先级问题，显示维护对关键 Bug 的响应及时。
- **社区贡献活跃**：外部贡献者（Shimada666、saminou、ksk2023、Lin-Artificial 等）持续提交修复型 PR，但多数仍处待合并状态。

---

## 2. 版本发布

### v1.48.0
🔗 Release 页面：https://github.com/OpenHands/software-agent-sdk/releases

本次发布的可见变更包括：

| 类型 | 内容 | PR |
|---|---|---|
| CI 修复 | 为合并产物清理流程自动开启 PR | [#4933](https://github.com/OpenHands/software-agent-sdk/pull/4933) |
| 安全修复（工具） | 新增日志过滤器，对 libtmux 日志输出中的密钥进行脱敏 | [#4871](https://github.com/OpenHands/software-agent-sdk/pull/4871) |
| SDK 修复 | changelog 内容在提供的数据中被截断，完整列表见 Release 页面 | — |

**破坏性变更 / 迁移提示**：从现有更新日志片段来看，本次为修复型补丁版本，未见明确标注的破坏性变更（Breaking Changes）或发布说明强制（release-note-required）条目。建议升级前仍以上游 Release Notes 全文为准，尤其是涉及 libtmux 日志脱敏的行为变化——依赖原始 tmux 日志做调试的集成方需注意输出内容会被过滤。

---

## 3. 项目进展

今日已合并/关闭的 PR 仅 4 条（未在展示列表中），但 **10 条 Issue 关闭**代表了实质推进：

**安全与架构（高价值关闭）**
- [#4288](https://github.com/OpenHands/software-agent-sdk/issues/4288) `[CLOSED]` **仅引用型凭据与安全运行时交付设计**（架构 / 安全）——由 @simonrosenberg 推动，历经仓库迁移，属重量级设计收敛。
- [#4399](https://github.com/OpenHands/software-agent-sdk/issues/4399) `[CLOSED]` CustomSecretsSection 提示词示例将密钥明文写入 `.git/config`（优先级:高）——直接消除了一个真实泄密路径。

**稳定性与正确性**
- [#5082](https://github.com/OpenHands/software-agent-sdk/issues/5082) `[CLOSED]` `ask_agent()` 在 LLM 调用进行中被调用时崩溃 `cannot pickle 'generator' object`（优先级:高，release-note-required）。
- [#4530](https://github.com/OpenHands/software-agent-sdk/issues/4530) `[CLOSED]` LLM 生成的会话标题泄漏原始 `<think>` 推理块。
- [#5041](https://github.com/OpenHands/software-agent-sdk/issues/5041) `[CLOSED]` 搜索接口 `limit` 校验失效导致 HTTP 500（应为 422）。
- [#4387](https://github.com/OpenHands/software-agent-sdk/issues/4387) `[CLOSED]` agent-server `close()` 10s 超时与 `wait_for_pending` 30s 上限冲突。
- [#4386](https://github.com/OpenHands/software-agent-sdk/issues/4386) `[CLOSED]` 事件线程异常被静默吞掉，stats 与 LLM 日志事件丢失。
- [#5084](https://github.com/OpenHands/software-agent-sdk/issues/5084) `[CLOSED]` examples CI 因缺失 `k8s_agent_sandbox` 模块失败。

**工程效率**
- [#4430](https://github.com/OpenHands/software-agent-sdk/issues/4430) `[CLOSED]` 移除 release 阶段的安全扫描（CI 精简）。

**整体推进评估**：今日以"**收口**"为主——把安全设计、密钥泄漏、高优先级崩溃三类遗留问题闭环，而非开启新的大功能。项目在**安全基线**上向前迈进了明显一步。

---

## 4. 社区热点

按评论数与关注度排序：

| 排名 | 条目 | 评论 | 状态 | 链接 |
|---|---|---|---|---|
| 1 | #2725 SDK vs Agent Server 兼容性缺口 | 6 | OPEN | [链接](https://github.com/OpenHands/software-agent-sdk/issues/2725) |
| 2 | #4382 ACP 派生成本计算错误 | 3 | OPEN | [链接](https://github.com/OpenHands/software-agent-sdk/issues/4382) |
| 3 | #4288 凭据安全设计文档 | 3 | CLOSED | [链接](https://github.com/OpenHands/software-agent-sdk/issues/4288) |
| 4 | #481 浏览器工具支持模态弹窗 | 3 | OPEN | [链接](https://github.com/OpenHands/software

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目日报 · 2026-09-16

---

## 1. 今日速览

LiteLLM 今日维持**极高活跃度**：24 小时内 Issues 更新 67 条（新开/活跃 52、关闭 15），PR 更新高达 334 条（待合并 215、已合并/关闭 119），并发布 1 个新版本 v1.101.0。PR 吞吐量约为 Issues 的 5 倍，且其中相当比例来自自动化 Agent 账号（`devin-ai-integration[bot]`），说明项目已建立起高度机械化的小步快跑修复流水线。今日新增修复集中在 **spend 追踪准确性、代理鉴权/路由、MCP 与 UI 可观测性**三条主线，同时累计关闭了 8 个历史 Issue（含多个长期挂起的 stale 项）。整体健康度良好，但**计费准确性、限流缓存一致性、流式中断时不触发 fallback** 三类问题反复出现，构成系统性的稳定性风险。待合并 PR 数量（215）显著高于已合并数（119），存在一定合并队列积压。

---

## 2. 版本发布

### v1.101.0

**核心内容：Docker 镜像签名与供应链安全**

- 所有 LiteLLM Docker 镜像现已使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 签名。
- 每个版本均使用同一把密钥签名，该密钥由 commit [`0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0) 引入。
- Release Notes 主体为「Verify Docker Image Signature」的验签指引，属于**文档/合规性增强**，未披露功能性变更。

**破坏性变更与迁移注意**：本次发布数据中未显示破坏性变更或迁移要求。若你的 CI/CD 或镜像校验流程此前依赖未签名镜像的指纹，需改为基于 cosign 公钥校验，请参照官方文档更新流水线。

**版本节奏信号**：Issue [#41299](https://github.com/BerriAI/litellm/issues/41299) 中提到用户已在 `litellm[proxy]==1.102.0rc1` 上复现问题，表明 **v1.102.0 已进入 RC 阶段**，下一版本窗口临近。

---

## 3. 项目进展

今日已合并/关闭的 PR 中，以下两项构成一次**计费准确性专项修复**：

| PR | 状态 | 解决的问题 |
|---|---|---|
| [#41171](https://github.com/BerriAI/litellm/pull/41171) | CLOSED（backport-stable） | 修复「部署钩子将流式请求转为非流式」后 spend 追踪被跳过的问题 —— 自 v1.99.0 起此类调用会触发 `failed_tracking_spend` 告警且不写入 spend 行；开启缓存后重复调用甚至返回 HTTP 错误 |
| [#41169](https://github.com/BerriAI/litellm/pull/41169) | CLOSED | 将转换后的流式调用按流式记录日志，使成本回调保留 `standard_logging_object`，避免 v1.100.0 上 Headroom CCR 后的 Bedrock Claude 流式调用被记为 $0 |

这两项修复直接回应了 v1.99.0–v1.100.0 引入的**计费回归**，属于 P0 级别的正确性回收。

**同期关闭的重要历史 Issue**：

- [#30164](https://github.com/BerriAI/litellm/issues/30164)（CLOSED）— `get_daily_activity` 分页导致的非确定性、虚高 spend 总额问题关闭，直接改善成本报表可信度。
- [#36566](https://github.com/BerriAI/litellm/issues/36566)（CLOSED）— `litellm_content_filter` 评估结果未出现在请求日志与 Guardrails Monitor 的问题关闭，补齐护栏可观测性。
- [#40548](https://github.com/BerriAI/litellm/issues/40548)（CLOSED）— 模型管理页 `Created By` / `Updated At` 显示 `Unknown` 的 UI 缺陷关闭。
- [#40598](https://github.com/BerriAI/litellm/issues/40598)（CLOSED）— Organization API 未校验企业 License 的授权漏洞关闭。
- [#26552](https://github.com/BerriAI/litellm/issues/26552)、[#28444](https://github.com/BerriAI/litellm/issues/28444)、[#25940](https://github.com/BerriAI/litellm/issues/25940) — 三个长期 stale 项随修复或清理关闭。

**整体推进幅度评估**：今日项目在**「成本核算可信度」**上取得了明确进展（分页聚合 + 流式转换 + 缓存命中三条路径的 spend 写入均被修合），这是 LiteLLM 作为网关产品最核心的信任基础。但在限流一致性、流式 fallback、代理鉴权边界三方面，修复尚未落地。

---

## 4. 社区热点

### 🔥 #1 [#14398](https://github.com/BerriAI/litellm/issues/14398) — 按天维度的请求/Token 限流（12 评论 · 8 👍 · 已开放近一年）
作者 @rutkk 于 **2025-09-10** 提出，至今仍是最热 Issue，且是本次数据中 👍 数最高者。

> **诉求**：当前仅支持 requests/tokens per minute，但 OpenAI 等厂商在免费/Pro 层普遍采用**每日限额**（如 1M GPT token/天）。网关无法表达这一约束，用户只能在上层自行实现。

**背后信号**：这是 LiteLLM 从「分钟级限流」走向「厂商配额语义对齐」的关键缺口。考虑到近期新增的 [#34734](https://github.com/BerriAI/litellm/issues/34734)（上游配额/余额探测）也指向同一方向，**跨厂商配额建模**可能正在成为下一阶段的产品主线。

### 🔥 #2 [#30164](https://github.com/BerriAI/litellm/issues/30164) — 分页导致 spend 总额虚高（7 评论 · 已关闭）
用户实测 `/user/daily/activity` 与 `/team/daily/activity` 的返回总额会随 `page_size` 变化，甚至两次相同请求结果不同，聚合端点虚高可达真实值的数倍。**今日已关闭**，是社区对计费数据可信度长期不满的一次集中释放。

### 🔥 #3 [#39713](https://github.com/BerriAI/litellm/issues/39713) — 虚拟 Key 缓存后每客户 RPM 限制失效（6 评论）
Per-customer `rpm_limit` 在虚拟 Key 被缓存后不再生效。**限流在老用户身上静默失效**是典型的成本失控场景，属高优先级。

### 🔥 #4 [#31866](https://github.com/BerriAI/litellm/issues/31866) — 提议新增 `disable_entity_spend_updates` 开关（6 评论）
作者 @deepanshululla 指出高 QPS 下，每次请求对 8 类实体表做 `_batch_database_updates` 的 UPDATE 成为写放大瓶颈，提出保留 SpendLogs 写入、关闭实体计数更新的开关。**这是性能与计费粒度的权衡诉求**，已附带实现方案，落地可能性较高。

### 🔥 #5 [#30301](https://github.com/BerriAI/litellm/issues/30301) — 防止内部 `optional_params` 泄漏进请求体（6 评论）
LiteLLM 内部字段被透传至严格校验的上游导致 400，作者指出这**不是孤立 Bug 而是同一失败类**。该 Issue 已关联多个同类单点问题，属于架构级健壮性提案。

### 🔥 #6 [#20962](https://github.com/BerriAI/litellm/issues/20962) — 非管理员用户无法创建 API Key（5 评论 · 6 👍 · stale）
UI 强制要求选团队，API 又禁止非管理员指定 `team_id`，形成死锁。**易用性痛点明确且获较多认同**，但已被标记 stale。

---

## 5. Bug 与稳定性

按严重程度排列（含是否已有 fix PR 判断）：

### 🔴 严重

| Issue | 问题 | 影响 | Fix PR |
|---|---|---|---|
| [#35536](https://github.com/BerriAI/litellm/issues/35536) | Responses ID 安全校验对**原始 ID / 无主 ID fail open** | **安全问题**：可绕过响应归属校验，存在跨租户数据访问风险 | ❌ 未见 |
| [#34534](https://github.com/BerriAI/litellm/issues/34534) | 每次 MCP tool call **永久泄漏一个 `max_parallel_requests` 槽位**，即使完全串行，约 N 次后 Key 被永久限流直到重启代理 | **可用性雪崩**：网关重启才能恢复，生产环境致命 | ❌ 未见（#41314 仅涉及 MCP OAuth 持久化，非此问题） |
| [#40404](https://github.com/BerriAI/litellm/issues/40404) | 上游流式响应异常中断（截断/卡死/畸形 chunk）时**fallback 完全不被调用**，fallback 部署收到 0 请求 | **容灾形同虚设**，配置了 fallback 却无兜底 | ❌ 未见 |
| [#28216](https://github.com/BerriAI/litellm/issues/28216) | `Router.aresponses(stream=True)` 中 `MidStreamFallbackError` **绕过 fallback 链** | 与上条同源的跨 provider 容灾失效 | ❌ 未见（stale） |
| [#33871](https://github.com/BerriAI/litellm/issues/33871) | 项目级 spend **从未被记录**，

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*