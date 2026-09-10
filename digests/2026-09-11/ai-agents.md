# OpenClaw 生态日报 2026-09-11

> Issues: 427 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-10 22:36 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报
**报告日期：2026-09-11** ｜ 数据窗口：2026-09-10（过去 24 小时）

---

## 1. 今日速览

OpenClaw 今日维持**极高活跃度**：24 小时内 Issue 更新 427 条（新开/活跃 242、关闭 185），PR 更新 500 条（待合并 252、已合并/关闭 248），社区提交与维护者吞吐基本持平。LTS 线发布收官版本 `v2026.6.35`，以"安全边界收紧"为核心主题。然而，当日讨论热度最高的议题仍集中在**资源泄漏、SQLite 写竞争与 2026.9.x 系列回归**三大类，多条 P0/P1 问题处于 `clawsweeper:needs-maintainer-review` 状态，亟待维护者决策。整体判断：**社区输入旺盛、修复管道通畅（248 条 PR 已合并/关闭），但高优先级缺陷的解化速度落后于报告速度，积压风险上升。**

---

## 2. 版本发布

### v2026.6.35 — June 2026 Extended Stable (LTS) 最终版

> 链接：https://github.com/openclaw/openclaw/releases/tag/v2026.6.35

这是 **2026 年 6 月 LTS 分支的最后一个扩展稳定版**，意味着该分支将进入维护终止阶段，后续安全修复预计只在 2026.8/2026.9 线上推进。

**更新亮点（Highlights）**
- **更安全的 provider 与 channel 边界**：内置 provider 和 channel 适配器现在会限制不可信响应体大小（bound untrusted response bodies），并在执行昂贵操作前拒绝超大输入（reject oversized inputs before expensive work）。
- 保留安全恢复路径（preserve safe recovery），确保边界收紧不会把正常流程判为失败。

**迁移注意事项**
- 该版本为 **LTS 收官版**，使用 2026.6.x 的生产环境应规划升级到 2026.8/2026.9 线。需注意 9.x 线目前存在多条未收敛回归（见第 5 节），**不建议在高负载/多 agent 网关上无验证直升 9.x**。
- 响应体与输入大小限制可能影响依赖超大 payload 的自定义 provider/channel 插件——升级前请确认插件侧的上限配置。
- 发布说明在数据中被截断，完整的破坏性变更列表请以 Release 原文为准。

---

## 3. 项目进展

今日 248 条 PR 被合并/关闭，以下为进入 Top 讨论榜的关键推进。

### 今日关闭/合并的代表性条目

| 条目 | 类型 | 说明 |
|---|---|---|
| [#144429](https://github.com/openclaw/openclaw/pull/144429) | CLOSED | `fix(agents)`: 用捕获的元

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目日报 — 2026-09-11

## 1. 今日速览

- 项目维持**极高活跃度**：过去 24 小时 445 条 Issue 更新、500 条 PR 更新，但新版本发布为 0，属于高频迭代与密集修复期。
- **桌面端插件 SDK 加载崩溃**是今日最集中的修复焦点，同日出现 4 个针对同一根因的 PR 并快速关闭/收口，对应 Issue #107288。
- 稳定性压力仍然显著：P1 级 cron 心跳死锁、web_server 事件循环卡顿、MCP OAuth 跨进程冲突、多 Profile 新建会话失效等问题持续在线。
- 社区讨论集中在**跨平台会话上下文共享、Bot 群聊脱离桌面端、turn-level 实时时间感知**等体验与架构需求。
- 积压侧，3–5 月创建的多项高赞功能请求仍处于 OPEN，PR 待合并量达 355 条（占当日 PR 更新约 71%），维护者需关注重复提交与路线图回应。


## 2. 版本发布

无新版本发布。


## 3. 项目进展

### 3.1 桌面端运行时插件加载崩溃集中修复
今日可见的已关闭 PR 高度集中在同一故障：生产构建下所有磁盘插件因 SDK 命名空间为 `undefined` 而加载失败，报错 `Cannot convert undefined or null to object`。

- PR #107309 [CLOSED]：容忍 null SDK 命名空间，准备运行时插件 shim → https://github.com/NousResearch/hermes-agent/pull/107309
- PR #107507 [CLOSED]：延迟绑定插件 SDK 全局变量，使打包运行时插件可加载 → https://github.com/NousResearch/hermes-agent/pull/107507
- PR #107338 [CLOSED]：隔离缺失的插件 SDK 命名空间，避免每个磁盘插件失败 → https://github.com/NousResearch/hermes-agent/pull/107338
- PR #107303 [CL

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报
**日期：2026-09-11**

---

## 1. 今日速览

过去 24 小时，Pi 项目保持高活跃度：Issue 侧共 133 条更新，其中 **103 条关闭、30 条新开/活跃**，关闭/新增比约 3.4:1，显示维护者正在集中清理积压与收敛历史问题；PR 侧 19 条更新，**11 条合并/关闭、8 条待合并**。今日无新版本发布。社区讨论集中在上下文预算与溢出恢复失败（#8061）、全屏模式交互体验（#9052）以及 per-model compaction 配置（#8133）等方向。整体健康度良好，但多个影响核心稳定性的长期 Issue（#8061、#9276、#9265）仍处开放状态，是本周期主要风险点。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日合并/关闭的重要 PR（11 条合并/关闭），主要围绕 **稳定性防护、TUI 渲染修复与模型目录维护**：

| PR | 内容 | 推进方向 |
|---|---|---|
| [#9431](https://github.com/earendil-works/pi/pull/9431) | feat(agent): 为所有工具调用增加 **3 分钟默认超时** | 修复工具无界阻塞导致 agent 挂死；填补除 bash/powershell 外工具无超时的空白 |
| [#9443](https://github.com/earendil-works/pi/pull/9443) | fix(ai): 捕获并回放 openai-completions 工具调用中的 Gemini `thoughtSignature` | 修复 OpenAI 兼容网关下 Gemini 工具链签名丢失 |
| [#9438](https://github.com/earendil-works/pi/pull/9438) | fix(tui): 让 overlay 覆盖终端内联图片 | 修复截图残留在 `/agents` 等浮层之上遮挡 UI |
| [#9435](https://github.com/earendil-works/pi/pull/9435) | 为 model provider `baseUrl` 增加值解析 | 对应 #9422，改善自定义 provider 配置体验 |
| [#9425](https://github.com/earendil-works/pi/pull/9425) | feat(ai): 新增 DeepSeek V4.1 Flash | 模型目录扩充，支持 off/low/high 思考等级 |
| [#9416](https://github.com/earendil-works/pi/pull/9416) | fix(coding-agent): skill 名称允许点号与下划线 | 兼容其他 harness（如 Claude）共享的 skill 目录 |
| [#9297](https://github.com/earendil-works/pi/pull/9297) | fix(ai): 移除失效的 Fable 5 fallback 目标 | 回应 #9294，避免 API 400 拒绝 |
| [#8799](https://github.com/earendil-works/pi/pull/8799) | feat(tui): 优化 “Working...” spinner | 输入框边框动画、匹配思考等级颜色、处理重试态 |
| [#9430](https://github.com/earendil-works/pi/pull/9430) | 移除 subagent 示例中不可达的 `tool_result_end` 监听 | 代码清理 |
| [#9407](https://github.com/earendil-works/pi/pull/9407) / [#9404](https://github.com/earendil-works/pi/pull/9404) | examples: 新增 model-preference-guard（多选 + 搜索） | 防止误用模型产生意外费用 |

此外，一批历史 Issue 于今日关闭，包括 **#8133（per-model compaction settings，5 👍）**、**#5366（会话树删除分支，2 👍）**、**#2374（tmux 内 Kitty 内联图片，自 3 月挂起）**，以及多个 no-action 类 issue（#9258、#9338、#9210、#8463、#9231）。

**整体推进评估**：今日落地的 PR 以“防御性修复 + 边界体验”为主，工具超时（#9431）与 Gemini 签名回放（#9443）属于对 agent 可靠性有实质影响的改动，项目在稳定性方向上向前迈进了明显一步。

---

## 4. 社区热点

按评论数与点赞数排序，今日讨论最活跃的话题：

1. **[#9323](https://github.com/earendil-works/pi/issues/9323) [CLOSED] Improve fireworks-specific config** — 14 评论（今日最高）
   围绕 Fireworks 专属配置函数的行为展开，作者明确说明报告由本人撰写、研究过程部分借助 AI。讨论热度高但已关闭，说明维护者已给出结论或处理方案。

2. **[#8061](https://github.com/earendil-works/pi/issues/8061) [OPEN][inprogress] Context budget ignores maxTokens output reservation** — 8 评论，2 👍
   输入上下文仅占模型窗口 ~78% 即被 provider 拒绝，自动 compact-and-retry 恢复在同一原因下**再次失败**。这是典型的“错误处理

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报
**日期：2026-09-11** | 数据窗口：过去 24 小时

---

## 1. 今日速览

LiteLLM 今日维持极高活跃度：过去 24 小时 PR 更新量达 **500 条**（其中 369 条合并/关闭，处理率约 73.8%），Issues 更新 **86 条**（新开/活跃 64 条，关闭 22 条），并发布 **2 个版本**（v1.100.1 稳定版与 v1.101.0-rc.2 预发布版）。从 PR 侧看，项目推进节奏强劲，重点集中在 **成本计费准确性（缓存音频、分层定价）**、**Redis/熔断稳定性**、**MCP 与 Agent 365 治理集成**、以及 **数据库连接池（PgBouncer）与 Redis IAM 认证**等基础设施方向。不过 Issues 关闭率仅约 25.6%，且列表中大量 issue 带有 `stale` 标签，说明**长期积压问题仍是项目健康度的主要隐忧**。整体评估：**开发活跃度优秀，但 issue 治理与响应时效需要加强**。

---

## 2. 版本发布

今日发布 2 个版本，均为签名验证说明型 Release Note，未在给定数据中呈现具体功能变更：

| 版本 | 类型 | 链接 |
|---|---|---|
| **v1.100.1** | 稳定版 | https://github.com/BerriAI/litellm/releases |
| **v1.101.0-rc.2** | 预发布（RC） | https://github.com/BerriAI/litellm/releases |

**说明与注意事项：**
- 两个版本均强调 **Docker 镜像签名验证**：所有 LiteLLM Docker 镜像使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 签名，密钥沿用 commit [`0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0) 引入的同一密钥。
- 生产环境部署建议在拉取镜像后执行 cosign 验签，确保供应链安全。
- **破坏性变更 / 迁移注意事项**：给定 Release Note 未披露具体 API 或配置变更。考虑到 v1.101.0 为 RC 版本，建议在生产环境继续使用 v1.100.1，并关注 v1.101.0 正式版的完整 changelog 后再升级。

---

## 3. 项目进展

今日合并/关闭的重要 PR（按主题归类）：

### 基础设施与稳定性
- **[#39683] feat(proxy): 容器内 PgBouncer 跨 worker 共享数据库连接（已关闭）** — https://github.com/BerriAI/litellm/pull/39683
  解决每个 proxy worker 各自向 Postgres 开连接池、Pod 占用随 worker×replica 膨胀的问题，对连接数有硬上限的数据库尤为关键。
- **[#38413] feat(redis): 新增 ElastiCache IAM 认证（已关闭）** — https://github.com/BerriAI/litellm/pull/38413
  为 Valkey/Redis 协议提供 AWS ElastiCache IAM 认证能力，解决 YAML 配置无法构造 Python 凭证 provider 的问题。
- **[#40626] test(proxy): 修复 marketplace 归档测试参数问题（已关闭）** — https://github.com/BerriAI/litellm/pull/40626
  修复因 #40496 与 #40518 合并冲突导致的 `proxy-endpoints` CI job 全红问题，恢复主干 CI 健康。

### 计费与成本准确性
- **[#35448] fix(proxy): 允许 internal user 读取自己请求的 prompt/response（已关闭）** — https://github.com/BerriAI/litellm/pull/35448
  直接对应 issue #34099，修复 `internal_user` 在日志抽屉中看不到自身请求内容的权限问题，并修正了"存储未启用"的错误提示。
- **[#39296] fix(proxy): `/v1/models` 从 deployment 而非 alias 解析限制（已关闭）** — https://github.com/BerriAI/litellm/pull/39296
  修复别名模型上报错误 token 上限（如 200k 上下文被显示为 1M）的问题。

### 待合并中的高价值 PR（已开启，代表项目方向）
- **[#40545] feat(proxy): 将 spend tracking 卸载到 Pod 本地 collector sidecar** — https://github.com/BerriAI/litellm/pull/40545
- **[#40484] feat(batches): 支持 Mistral Files/Batches 与按页 OCR 批处理成本追踪** — https://github.com/BerriAI/litellm/pull/40484
- **[#40623] feat(proxy): 容器内 PgBouncer 支持轮换 RDS IAM 与 Azure Entra token** — https://github.com/BerriAI/litellm/pull/40623
- **[#40568] feat(guardrails): 为 Microsoft Agent 365 guardrail 增加 Entra Agent ID 认证模式** — https://github.com/BerriAI/litellm/pull/40568

**整体推进评估**：今日项目在**性能与稳定性基础设施**（PgBouncer、Redis IAM、熔断器降噪）与**成本计费正确性**两条主线上均有实质落地，属于结构性改进而非零散修补。PR 吞吐量表明维护团队与自动化 Agent（多个 `devin-ai-integration[bot]` 提交）协同紧密。

---

## 4. 社区热点

### Issue 讨论热度 Top 5

1. **[#16073] fal.ai 模型支持（13 评论，👍9）** — https://github.com/BerriAI/litellm/issues/16073
   用户请求为 fal.ai 增加 Sora 2、Veo 3.1 等视频模型支持，赞数最高，反映**多模态视频生成需求正在快速上升**。
2. **[#34281] 健康检查优雅失败（12 评论）** — https://github.com/BerriAI/litellm/issues/34281
   HomeLab 用户反馈主机临时离线时健康检查"硬失败"，希望改为优雅降级，属于典型自治运维场景。
3. **[#16582] Spendlog 清理失效（9 评论）** — https://github.com/BerriAI/litellm/issues/16582（已关闭）
   K8s 双副本环境下保留策略不生效，日志仅有空错误信息。
4. **[#68] ollama / HuggingFace / HF Inference Endpoint 支持（8 评论）** — https://github.com/BerriAI/litellm/issues/68（已关闭）
   三年老 issue 关闭，标志早期 provider 平权目标达成。
5. **[#24771] MCP OAuth2 回调 404（6 评论）** — https://github.com/BerriAI/litellm/issues/24771
   OAuth2 GitHub App 方式的 MCP server 回调跳到不存在的 `/ui/mcp/oauth/callback`。

### PR 关注点（评论数据缺失，按主题归纳）
- **Redis 熔断器降噪成为今日 PR 密集区**：#40624、#40620 均围绕"熔断打开时每个请求打印完整 traceback 导致 CPU 打满"的问题，说明这是一个被多个贡献者独立识别的高频痛点。
- **成本计费修复**：#40627（缓存音频 token 按音频缓存读取费率计费）、#40622（未知模型请求用占位符记录日志，避免 prompt 泄入 spend 表）显示社区对**计费准确性与数据泄漏防护**高度敏感。

**背后诉求分析**：社区关注点正从"支持更多模型"转向"**生产级可靠性 + 成本可审计性 + 企业治理**"，尤其是 Redis/DB 故障降级、MCP OAuth 流程完整性和计费边角案例。

---

## 5. Bug 与稳定性

按严重程度排列：

### 🔴 严重（数据丢失 / 资源耗尽 / 计费错误）

| Issue | 描述 | 状态 | 关联 Fix PR |
|---|---|---|---|
| [#37611](https://github.com/BerriAI/litellm/issues/37611) | 后台健康检查将整张 `LiteLLM_HealthCheckTable` 加载进每个 worker，导致近 OOM 内存 + DB 风暴 | **已关闭** | ✅ 已修复 |
| [#35563](https://github.com/BerriAI/litellm/issues/35563) | 重用 `x-litellm-call-id` 导致 spend-log 行被静默丢弃（主键冲突） | 开放 | ❌ 暂无 |
| [#30135](https://github.com/BerriAI/litellm/issues/30135) | `*_above_200k_tokens` 分层定价字段被忽略，所有 token 按基础费率计费 | 开放 | ❌ 暂无 |
| [#35691](https://github.com/BerriAI/litellm/issues/35691) | 自定义模型 spend log 记录成本 $0（`cost_breakdown.total_cost=0`） | 开放 | ❌ 暂无 |
| [#40020](https://github.com/BerriAI/litellm/issues/40020) | `litellm_settings.max_budget` 触发进程本地 `_current_cost` 上限且永不重置 | 开放 | ❌ 暂无 |

### 🟠 中等（功能回归 / 兼容性）

| Issue | 描述 | 状态 | 关联 Fix PR |
|---|---|---|---|
| [#37039](https://github.com/BerriAI/litellm/issues/37039) | `chatgpt/*` 非流式 chat completion 自 1.88.1 起回归失败（流式正常） | 开放 | ❌ 暂无 |
| [#30079](https://github.com/BerriAI/litellm/issues/30079) | 升级 1.88.0 后 `/metrics` 因 307 重定向返回空数据 | 开放（stale） | ❌ 暂无 |
| [#27955](https://github.com/BerriAI/litellm/issues/27955) | Anthropic adapter 下 `max_parallel_requests` 在客户端取消流式请求时只增不减 | 开放 | ❌ 暂无 |
| [#29764](https://github.com/BerriAI/litellm/issues/29764) | `/v1/messages/count_tokens` 忽略 `api_base`，硬编码 `api.anthropic.com` | 开放（st

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*