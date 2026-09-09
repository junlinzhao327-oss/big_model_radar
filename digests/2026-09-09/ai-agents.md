# OpenClaw 生态日报 2026-09-09

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-09 00:21 UTC

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



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报（2026-09-09）

## 1. 今日速览

过去 24 小时项目保持中等偏高活跃度：30 条 Issue 更新（其中 20 条新开/活跃、10 条关闭），50 条 PR 更新，无新版本发布。最值得关注的是 v1.46.0 发布流程已启动（#4908），同时伴随着一个针对该版本的 cloud-proxy router 修复 PR #4914 正在推进。Issue 侧出现了一批值得注意的高质量问题——包括 ACP 子进程孤儿化（#4901/#4910）、MCP 故障导致会话中止（#4891）、沙箱暂停后会话无法恢复（#4893）等，且大量由 AI 代理（OpenHands-based agent）自动创建，显示项目正在被自身技术驱动维护。目前有大量 issue 仍停留在 `needs-triage` 状态，部分已存活超过 5 个月，维护者响应压力值得关注。


## 2. 版本发布

**无新版本发布。** 但 v1.46.0 的发布 PR（#4908）已于昨日开启，正在执行发布检查清单（集成测试、行为测试、安全扫描均已勾选通过）。另有热修复 PR #4914 将 cloud-proxy router cherry-pick 到 `rel-1.46.0` 分支，预计 1.46.0 将包含 Agent Canvas 所依赖的运行时代理能力。


## 3. 项目进展

今日合并/关闭的 PR 数量较少（3 条），但结合关闭的 Issue 可以看出项目在以下方向的实质推进：

- **LLM 成本追踪精准度修复**：`#4816`（自定义 `litellm_proxy/*` 模型名成本记录为 $0）和 `#4817`（LLM span 成本忽略 prompt-cache tokens）均已关闭，表明这两个影响可观测性/计费准确性的 Bug 已获得处理方案。
- **异构响应处理问题关闭**：`#3992`（弱模型/本地模型下 `ResponseDispatchMixin` 对称性缺陷导致代理终止）已关闭，该 issue 存活约 2 个月、拥有 14 条讨论，关闭意味着相关修复已落地或达成共识。
- **文档补全**：#4657（图像处理辅助函数文档）已关闭，SDK 中 agent.py 的 docstring 缺口获补。
- **线上发布准备**：PR #4908（Release v1.46.0）全部检查项通过；#4914 正在为发布分支补齐 cloud-proxy 能力。

在等待合并的长线 PR 队列中，`#4889`（从 source schema 派生 ConversationInfo，消除 ~20 个字段重复声明）与今日新开的 feature issue `#4849` 形成对应，若合并将显著降低 API 响应结构与 `ConversationState` 之间的 drift 风险。


## 4. 社区热点

| Issue/PR | 标题 | 评论数 | 关注焦点 |
|---|---|---|---|
| [#4248](https://github.com/OpenHands/software-agent-sdk/issues/4248) | Missing required parameters for function 'execute_bash': {'security_risk'} | 15 | DeepSeek-reasoner 调用 execute_bash 时缺少 `security_risk` 参数，会话无法继续 |
| [#3992](https://github.com/OpenHands/software-agent-sdk/issues/3992)（已关闭） | Asymmetric handling of content-without-tool-call responses terminates agents driven by weaker/local models | 14 | 讨论本地/弱模型兼容性的核心架构缺陷 |
| [#4245](https://github.com/OpenHands/software-agent-sdk/issues/4245) | Agent-Server Webhook Connection Failures Cause Container Crashes | 12 | docker 容器因 webhook 连接失败反复崩溃，影响生产部署稳定性 |
| [#4246](https://github.com/OpenHands/software-agent-sdk/issues/4246) | MCP 工具初始化超时后 agent 无反馈地 idle | 12 | 失败时无视觉/错误提示，可用性差 |
| [#4533](https://github.com/OpenHands/software-agent-sdk/issues/4533) | Conversation launch drops LLM api_key when seeded default agent profile is active | 7 | 有趣的信号：OpenHands-based agent（@smolpaws）自托管时发现的真实 Bug，属于项目"dogfooding"的正面案例 |

**社区诉求分析**：
- 前四大热点 Issue（#4248、#4245、#4246、#4252）共同指向**本地/自托管部署体验**问题，包括 Ollama 超时、LM Studio 配置、浏览器沙箱和 MCP 工具等——社区自托管需求正在快速增长。
- 有多个热点 Issue 的评论持续跨数月（#4248 创建于 4 月 25 日但 9 月 8 日仍有更新），说明用户在等待修复的过程中不断追加信息，但也反映**长尾 Bug 的排期压力**。


## 5. Bug 与稳定性

按严重程度排列（标注是否存在修复 PR）：

**🔴 高严重度**
- **ACP 子进程孤儿化（POSIX）**：#4901（2 条评论，9月8日创建）指出 `ACPAgent._shutdown_runtime` 仅 kill 顶层 PID，导致 `npx`/`sh -c` 链的更深处孙进程（如实际 agent 进程）在线程关闭后被遗留；#4910 是同问题的单行报告。当前无修复 PR。
- **安全审计：RemoteWorkspace host 验证缺口（已关闭）**：#4261 —— 严重度 CRITICAL 的"air-gap 绕过"问题（fork 审计发现 host 验证缺口导致非预期 egress），已在今日关闭。修复通过与否未能确认，建议维护者关注其关闭理由。
- **Conversation 卡死于 RUNNING（不可恢复）**：#4893 —— sandbox 在运行中被暂停/停止后，会话的 `execution_status` 永远停留在 RUNNING，且无法通过 API 恢复，对远程 agent 运维场景有阻断性影响。无修复 PR。

**🟠 中严重度**
- **MCP 连接失败中止整个 send_message**：#4891 —— 某个可选 MCP server 不可达时，`MCPError` 在 agent 初始化阶段直接传播，导致用户消息永远无法送达 LLM。被判断为设计缺陷（optional 依赖不应阻断主链路）。已有 `ready-for-dev` 标记。
- **LLM api_key 丢失**：#4533 —— 当 seeded `default` agent profile 激活时，conversation launch 会丢弃 LLM api_key 并触发 litellm AuthenticationError。已有 `priority:medium` + `security-related` + `ready-for-dev` 标记。
- **Pre-flight 校验错误拒绝 ChatGPT 订阅用户**：#4896（已关闭）—— ChatGPT subscription profile 保存时预检失败并返回 "Incorrect API key provided: None"，对 OAuth 用户造成误导。关闭于 9 月 8 日，标记 `priority:high`。

**🟡 低-中严重度（长时间未分诊）**
- #4245（docker webhook 崩溃，1 月创建）、#4246（MCP 超时无反馈，3 月创建）、#4248（execute_bash 缺 security_risk，4 月创建）、#4255（Ollama 5 分钟超时杀死任务，已关闭）、#4250（Workers AI context window 校验失败）等老 issue 至今停留在 `needs-triage`，数条已存活 4-7 个月。这组数据的堆积程度反映了 **triage 积压是当前项目健康度的最大威胁**。
- **CI 盲区**：#4912（9月8日新增，1 条评论）指出 path-gated 测试任务未包含 `openhands-sdk/**`，导致 SDK 变更可在所有 required check 全绿的情况下破坏下游包——这是一个典型的"隐性风险"问题，值得尽快修复。

**🔧 修复 PR 已存在但待合并的（供参考）**
- `#4412`（fix agent-server close() 中 force-cancel run task）→ 关联 #4387/#4893 一类"会话运行状态异常"问题
- `#4770`（cloud sandbox resume 后重新指向 client）→ 与 #4893 的恢复路径相关
- `#4703`（从 LLM 生成的标题剥离 inline reasoning）→ 修复 #4530
- `#4582`（EOF 无换行时的 insert 拼接 Bug）→ 修复 #4583


## 6. 功能请求与路线图信号

**已有明确实现/PR 支撑的需求（可能进入下一版本）**
- **Custom title generation prompts**（#4564，PR 挂 `integration-test`）—— 让用户自定义会话标题生成提示词，对多语言/垂直场景用户有价值。
- **Cursor 成为内置 ACP provider**（#4874，PR 已 live-verified）—— 补上 Cursor CLI 的 ACP 支持，完善 ACP provider 生态。
- **DAG 任务执行**（#4894，feature issue，2 条评论）—— 在沙箱 AST 环境中支持 `run_dag` 与依赖屏障，供动态 workflow 脚本使用。当前沙箱禁止 `import asyncio`，使用者需要一个原生并发原语；尚无对应 PR。

**

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-09-09


## 1. 今日速览

过去24小时内，LiteLLM 仓库保持**高活跃度**：Issues 更新 70 条（新开/活跃 58 / 已关闭 12），PR 更新高达 307 条（其中 106 条已合并/关闭，201 条仍在待合并队列中）。PR 提交量与合并量同步放大，说明团队当前正处于高频开发迭代周期，多项功能集中在 guardrails 管道、Azure AI Foundry 计价修复、流式处理与认证安全修复方向。值得留意的是，PR 队列中由 `devin-ai-integration[bot]` 提交的自动化修复占比显著，人工维护的 core PR（如 Rust SDK 重构、MCP schema discovery 代理）与自动化 PR 形成了混合推进节奏。版本发布方面，过去一天内 **无新 Releases**。

> 活跃度评估：**极高**。24 小时 377 条 Issue + PR 综合更新量处于近期高位，且自动化 bot 主导的 CI/修复型 PR 大幅推高 PR 计数。需关注 201 条待合并 PR 的积压消化速度。


## 2. 版本发布

今日无新版本发布。


## 3. 项目进展

昨日合并/关闭的 106 条 PR 中，有几个信号值得关注：

- **Fireworks AI Responses 路径流中断修复（#40268，已关闭）**：将 `instructions`、developer 条目以及重放的 reasoning 条目折叠为一条 system 消息，修复 Codex CLI 在 `fireworks_ai/` 部署上"仅首次提问有效，后续全部流中断"的问题。这暗示团队在持续打磨 Codex 与 Responses API 兼容层。
- **价格与模型目录持续完善（#40189, #40309 等）**：`azure_ai` Foundry 有 7 个在线目录条目未配置单价（导致成本 $0 计费）、路由器费用被重复计算等问题正在修复；diskcache 漏洞忽略有效期被再度延长，说明上游漏洞暂无法解决，团队选择以时间换空间。
- **Guardrails 管道重构进入密集期（#40284/#40271/#40274/#40327 等一组 PR）**：围绕旧式 post-call hook 在流式管道中的执行问题（rewrite 丢失、block 拦截未达）、Responses 后台请求漏执行策略管道、guardrail scan id 无法溯源到具体 guardrail/stage/provider 等，正在对 guardrails 执行体系做系统性补强。这是当前开发资源集中度最高的方向之一。
- **Rust SDK 化持续深入（#40070）**：为"Rust 执行路由 + 回调 Python 原生对象"的过渡做准备，引入 retained callback 机制，避免按值传递导致现有集成失效。

整体来看，项目正在经历一次**架构与功能双线推进**：核心层向 Rust SDK 迁移 + guardrails 管道能力补全 + AI Gateway/模型路由的兼容性修补。


## 4. 社区热点

- **[#361 [CLOSED] "I Wish LiteLLM Had..." 愿望清单帖（评论 479 👍 0）](https://github.com/BerriAI/litellm/issues/361)** — 从 2023-09-13 至今持续 3 年的"许愿池"帖子，今日仍有活跃评论（最后更新 2026-09-08）。该帖是社区需求的长期汇聚地，但已关闭（几乎无官方回应，状态更像是"存档箱"）。潜在引导信号：用户的新需求如果只是回复到此帖子，大概率不会被追踪；需要单开 issue 才会进入官方 triage 流程。

- **[#24677 [OPEN] "虚拟密钥 TPM 限流错误"（评论 17 👍 4）](https://github.com/BerriAI/litellm/issues/24677)** — 用户明确指出现象在 v1.82.3 中依然复现，且此前在 #18953（v1.80.0）曾被标记为已解决。**"声称已修复但实际仍存在"** 的回归反复，是社区信任度的重大消耗点，值得维护者优先回溯。

- **[#14257 [OPEN] "模型不仅按名称暴露，还能按类型暴露"（评论 9）](https://github.com/BerriAI/litellm/issues/14257)** — 用户抱怨代理接口（proxy API）上暴露的模型超出了配置范围，涉及模型可见性与 access-control 的边界。此 issue 已持续一年（2025-09 创建），至今未关闭，说明同类可见性泄漏问题被多次触达但修复优先级不高。


## 5. Bug 与稳定性

按严重程度从高到低排列：

### 高危

- **[#34140 v3 限流器将团队每模型限制（model_per_team）双倍计数 → 实际 RPM/TPM 只有配置的一半](https://github.com/BerriAI/litellm/issues/34140)**（创建 2026-07-21，开放中，评论 5）— 配置值 N 在 ~N/2 请求后即开始 429，直接影响企业客户 SLA。双倍计数的根源位于 v3 parallel_request_limiter 的 key 聚合逻辑。**尚无 fix PR 关联。**

- **[#40095 并发的未知 end user 首个请求绕过默认预算](https://github.com/BerriAI/litellm/issues/40095)**（创建 2026-09-07，开放中，评论 3）— 自定义认证 + `max_end_user_budget_id` 配置下，并发首次请求可绕过预算检查，造成费用失控风险，涉及**资金安全**。新近上报，尚无 fix PR。

- **[#40217 认证拒绝信息泄露密钥哈希与模型白名单](https://github.com/BerriAI/litellm/issues/40217)**（创建 2026-09-08，开放中，评论 2）— 401 响应回显了该密钥的哈希值，403 暴露了该 key 的完整模型允许列表。属于**认证信息侧信道泄露**，便于攻击者离线破解/了解策略。尚无 fix PR。

### 中危

- **[#24677 TPM/RPM 限流在实际执行中未被正确强制](https://github.com/BerriAI/litellm/issues/24677)**（详见上"社区热点"）— v1.80.0 标记 solved，v1.82.3 复现。属于回归修复不彻底。

- **[#30053 流式 fast_path 打破工具调用连续性（v1.87.0 引入，PR #28289）](https://github.com/BerriAI/litellm/issues/30053)**（创建 2026-06-09，开放中）— Claude via Bedrock 在工具调用后续流中返回 XML 而非文本。**该 issue 从 2026-06 至今 3 个月无 fix**，影响所有依赖 Bedrock + 工具调用的流式用户。

- **[#39715 DELETE /v1/files/{file_id} 在 Bedrock 上返回 500 "does not support file deletion"](https://github.com/BerriAI/litellm/issues/39715)**（创建 2026-09-04，开放中）— 文件上传可用但删除不可用，管理面功能不完整。已提交 P72 工程师 issue（说明有企业客户实际受影响）。

- **[#30065 Redis 集群分组绕过 CROSSSLOT 错误修复缺失 → Azure Redis Enterprise 直接报错](https://github.com/BerriAI/litellm/issues/30065)**（创建 2026-06-09，开放中）— `_group_keys_by_hash_tag()` 仅对 OSS Cluster 生效，导致 Azure Redis Enterprise（非 OSS 模式）上出现 CROSSSLOT 错误。**已在积压超过 3 个月。**

### 低危 / 监控面 / 新近

- **[#38459 token_counter 对 `input_audio` 内容块报错，导致上下文窗口&提示缓存检查静默跳过、/utils/token_counter 接口 500](https://github.com/BerriAI/litellm/issues/38459)**（2026-08-27）— 同类问题已覆盖 image/video/file 块，audio 是新暴露的一种。
- **[#30121 OTel 回调在 `/v1/messages` 上不设置 `gen_ai.input.messages`/`gen_ai.output.messages`](https://github.com/BerriAI/litellm/issues/30121)**（2026-06-10 创建，仍未解决）— 影响可观测性。
- **[#30079 /metrics 端点因 307 重定向返回空数据（v1.88.0 回归）](https://github.com/BerriAI/litellm/issues/30079)**（2026-06-10 创建）— 至今已积压 3 个月未修复。
- **[#37726 Azure Entra Redis 认证无法在 cluster 模式下启动代理](https://github.com/BerriAI/litellm/issues/37726)** — `init_redis_cluster` 缺少 credential provider 路径，属于企业部署阻塞问题。


## 6. 功能请求与路线图信号

- **模型组组合（"group of groups"）需求（#28125）已于昨日关闭** — 该 feature 曾被标记为 enhancement，用户在 2026-05 请求允许 `model_name` 引用其他模型组作为成员，实现模型组嵌套组合，最终被关闭（可能已在内部支持或判定为低优先级）。社区若仍需要此能力，应关注关闭原因。

- **社区呼声较高的新功能**：
  - [#36150 [Feature] 官方 QwenCloud 迁移路径（DashScope → QwenCloud），厂商直接提交 issue 请求接入](https://github.com/BerriAI/litellm/issues/36150)（👍 0，开放中）— 国际开发者平台的接入需求。
  - [#40096 [Feature] /search 端点统一 start_date/end_date 日期范围过滤](https://github.com/BerriAI/litellm/issues/40096)（2026-09-07 新开）— 底层已有一些 provider 支持日期过滤，建议在 LiteLLM 层做归一化。

- **PR 中体现的官方路线图方向**（来自昨日活跃 PR，可能进入下个里程碑）：
  - **MCP Schema Discovery 代理模式**（#40298）：新增 `/mcp/proxy`，支持 `search_tools`、`get_tool_schema`、`call_tool`，解决大型 MCP 目录的按需发现，而非全量加载。
  - **CLI 增加 Claude Code 配置命令**（#40319）：`lite configure claude` / `lite unconfigure claude`，免手工编辑 `~/.claude/settings.json`；#40330 同时在 Claude Code/Codex 状态栏展示实际路由到的模型与会话节省金额（有端到端闭环的意图）。
  - **Auto-router 增加会话级可观测性**（#40330 配套 `GET /auto_router/session` 接口，回传 routed model 与 session 节省）。
  - **Hosted vLLM 增加 image edit 支持**（#40329）— 接入 `/v1/images/edits`。


## 7. 用户反馈摘要

- **"修复未生效 / 回归反复"引发信任危机信号**：#24677 的用户开头即写道"该问题最初在 #18953 中上报并标记为 solved，但我们仍然在 v1.82.3 看到同样的行为"。建议内部核查该 issue 被 auto-close 或 wide-fix 的机制是否存在验证盲区。
- **遗留修复等待跨版本交付**：#39145 用户认为此前 #37623（v1.99.0）里针对 prompt_cache_key 的修复"是错误的，很可能破坏了缓存"，反映出近期多个 issue 都集中在 Anthropic→OpenAI 翻译层，社区对该层代码的稳定性不满意。
- **配置覆盖逻辑存在零成本场景异常**：#25204（已关闭）指出若配置显式设置 `input_cost_per_token: 0`，LiteLLM 仍会忽略零成本覆盖并套用内置 Anthropic 定价表计费。该 issue 标签为 stale 并被关闭，但值得追踪释放到哪个版本修复。
- **对日志噪音敏感但功能重要的用户**（#32778，已关闭）：工具权限护栏（Tool Permission Guardrail）对预期/无需上报的事件以 WARNING 级打日志，造成大量噪音。用户期待一种"按预期拦截不告警"的默认行为。

> 整体用户情绪：核心痛点集中在**限流/预算的准确性与安全性**（TPM 计数错误、双倍计数、绕过预算）、**缓存翻译的正确性**（prompt_cache_key、encrypted_content 丢失）、以及**长时间不动的积压 bug**（3个月+未处理）。对项目在 guardrails 管道与 CLI 易用性上的改进方向反馈相对中性，尚无大面积负面情绪。


## 8. 待处理积压

以下为**超过 90 天未关闭**且对生产环境有实际影响的开放问题：

| Issue/PR | 核心痛点 | 积压时长 | 最后活跃 |
|---|---|---|---|
| [#30053 流式 fast_path 工具调用续流被破坏（Bedrock）](https://github.com/BerriAI/litellm/issues/30053) | 客户端收到 XML 而非文本；引入于 v1.87.0 | 3 个月 | 2026-09-09 |
| [#30065 Redis 分组绕过导致 Azure Redis Enterprise CROSSSLOT 错误](https://github.com/BerriAI/litellm/issues/30065) | 集群模式对非 OSS Redis 完全不可用 | 3 个月 | 2026-09-09 |
| [#30079 /metrics 端点 307 导致 Prometheus 拉取空数据](https://github.com/BerriAI/litellm/issues/30079) | 可观测性失效（v1.88.0 回归） | 3 个月 | 2026-09-09 |
| [#37726 Azure Entra Redis 认证 cluster 模式无法启动](https://github.com/BerriAI/litellm/issues/377

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-09-09

## 今日速览

过去 24 小时，Temporal 项目处于**高强度开发与密集合并周期**：PR 更新达 49 条，其中 18 条已合并/关闭，31 条仍在等待合并；相比之下 Issue 侧较为平静，仅 2 条更新且无新关闭。无新版本发布，但有多个指向 v1.32.0 及 cloud/v1.32.0 的发布分支修复 PR 被合并，表明维护团队正在同步推进主分支特性开发与旧版本稳定性修补。项目整体健康度良好，开发主力集中在 Nexus/Worker Callbacks 特性栈、复制可靠性增强及测试基础设施加固上。

---

## 项目进展

今日合并/关闭的 PR 主要集中在**发布分支修复**与**工程质量改进**两条线上，最能说明项目当前推进方向：

### Schedule V2→V1 回滚阻塞修复（已合并）

- [#11955 [CLOSED] fix: Don't block schedule rollback on a closed dummy sentinel](https://github.com/temporalio/temporal/pull/11955) — 修复 schedulev2 回滚未正确识别 V1 sentinel workflow 状态的问题。原实现在快速回滚场景下会因错误检查 V1 workflow 状态而阻塞，导致回滚逻辑无法在 15 分钟窗口内生效。
- [#11964 [CLOSED] Simplify non-occupying workflow handling in schedule migration](https://github.com/temporalio/temporal/pull/11964) — 作为 #11955 的后续，将 not-found 与 non-running 两种 workflow 状态合并为单一非占用分支，简化迁移判断逻辑。Review 意见已被吸收。
- [#11971 [OPEN] Cloud/v1.32.0 163](https://github.com/temporalio/temporal/pull/11971) — 将上述两个修复 cherry-pick 到 cloud/v1.32.0 分支，修复 V2→V1 回滚中 sentinel 值未被正确检查的问题，另附少量格式调整。

### Nexus callback 兼容性修复（已合并至 release/1.32.0）

- [#11965 [CLOSED] [release/1.32.0] Make Nexus callback source header opt-in](https://github.com/temporalio/temporal/pull/11965) — 默认不再为 legacy HSM worker Nexus targets 自动附带 source header，改为通过 `callback.inspectSourceHeader` 配置项显式开启，向后兼容性优先的修复。

### 测试与代码质量持续加固

- [#11464 [OPEN] Refactor frontend interceptors](https://github.com/temporalio/temporal/pull/11464) — Nexus frontend interceptors 大规模重构，已完成 built / 手动测试 / 单元测试三轮验证，等待合并中。
- [#11970 [OPEN] Render alerts details as code blocks in test summaries](https://github.com/temporalio/temporal/pull/11970) — 修复 GitHub test summary 中诊断输出因 Markdown 语法被错误渲染的问题。
- [#11962 [OPEN] Retry post-test artifact uploads](https://github.com/temporalio/temporal/pull/11962) — 针对 GitHub Actions 间歇性 403 artifact 上传失败增加复合重试动作（5s / 15s 退避）。
- [#11972 [OPEN] Use await.RequireTrue in matcher backlog-forwarding test](https://github.com/temporalio/temporal/pull/11972) — 消除 `require.Eventually` 超时后遗留 goroutine 读写 `t.childMatcher` 导致的跨测试数据竞争。

**整体评估**：主分支功能开发仍活跃推进中，但今天的合并重心明显偏向 release/1.32.0 与 cloud 分支的稳定性修复，说明项目正处在 **"开发新特性 + 维护已发布版本"并存**的阶段。

---

## 社区热点

今日 Issue/PR 的评论数据整体偏低，最受关注的是以下两条：

### #11691 — SQL 会话刷新导致"僵尸集群"问题（3 条评论 · 2 👍）

[SQL session refresh can close the connection pool irrecoverably ("sql: database is closed"); membership heartbeat then fails silently forever, leaving a zombie cluster that reports SERVING](https://github.com/temporalio/temporal/issues/11691)

这是近 24 小时讨论度最高的 Issue，核心痛点：

- SQL session refresh 会不可恢复地关闭连接池（`sql: database is closed`）
- membership heartbeat 随后静默失败
- 集群仍报告 `SERVING` 状态，但**已无法分发任何任务**——即"僵尸集群"

该 Issue 已持续 20 天（8/20 创建），至今无 fix PR 关联，用户诉求集中在**自愈能力**上：要么 SQL session refresh 能从错误状态恢复，要么 heartbeat 持续失败时应触发进程重启。2 个 👍 说明至少还有一位用户遇到过相同问题。

### #11958 — CallbackState request_id 语义歧义（1 条评论）

[Fix ambiguities related to `chasmcallbackpb.CallbackState::request_id`](https://github.com/temporalio/temporal/issues/11958)

由 @chrsmith 昨日新开，属于 Worker-callbacks 特性设计讨论。指出 `CallbackState` 中新增的 `request_id` 字段（用于标识"添加了 callback 的请求"）存在语义模糊且已被错误使用，强调 **callback 投递必须携带稳定 ID** 以避免去重逻辑出错。这是设计层面的纠偏，预计会推动 proto 定义与实现同步更新。

---

## Bug 与稳定性

按严重程度排列：

| 严重程度 | 问题 | 状态 | Fix PR |
|---|---|---|---|
| 🔴 严重 | [#11691 SQL 会话刷新导致连接池不可恢复关闭，集群成为"僵尸"且无自愈机制](https://github.com/temporalio/temporal/issues/11691) | Open · 20 天无修复 | ❌ 无 |
| 🟠 高 | [#11968 SignalWithStart 原 workflow 关闭后重试会启动新 run / 发送重复 signal](https://github.com/temporalio/temporal/pull/11968) | Fix PR 已提交 | ✅ #11968（open） |
| 🟠 高 | [#11955/#11964 Schedule V2→V1 回滚被已关闭的 dummy sentinel 阻塞](https://github.com/temporalio/temporal/pull/11955) | 已修复 | ✅ 已合并 |
| 🟡 中 | [#11970 GitHub test summary 中诊断输出含 Markdown 语法导致报告不可读](https://github.com/temporalio/temporal/pull/11970) | Fix PR 已提交 | ✅ #11970（open） |
| 🟡 中 | [#11972 测试超时后遗留 goroutine 读写共享状态导致数据竞争](https://github.com/temporalio/temporal/pull/11972) | Fix PR 已提交 | ✅ #11972（open） |
| 🟡 中 | [#11962 GitHub artifact 上传间歇性 403 导致 CI 失败](https://github.com/temporalio/temporal/pull/11962) | Fix PR 已提交 | ✅ #11962（open） |

**重点关注**：#11691 是当前唯一悬而未决的严重问题，涉及 SQL 存储后端集群的可用性，且无关联修复 PR。考虑到用户明确描述了自愈路径期望（terminate process 让 supervisor 重启），此类问题可能在生产环境中导致长时间不可用，建议维护者提高优先级。

---

## 功能请求与路线图信号

尽管今日没有新的用户功能请求 Issue，但多个在途 PR 清晰展示了 Temporal 接下来的技术方向：

### Worker-variant Callbacks（确定性路线图项）

由 @chrsmith 主导的 stacked PR set（目标分支 `feature/worker-callbacks`）持续推进中：

- [#11589 Support Worker-variant callbacks](https://github.com/temporalio/temporal/pull/11589) — 特性主体实现
- [#11567 Add completion callbacks to SANOs](https://github.com/temporalio/temporal/pull/11567) — 为 SANOs 接入完成回调
- [#11566 Make supported callback kinds configurable](https://github.com/temporalio/temporal/pull/11566) — callback 类型可配置化

这套 PR 栈已持续近一个月（8/13-8/14 创建），是当前最长线的特性分支之一。搭配 Issue #11958 对 request_id 语义的修正讨论，该特性正处于**实现与设计打磨并行**的阶段。

### 复制可靠性增强

- [#11492 Gradual connect shedding tasks](https://github.com/temporalio/temporal/pull/11492) — 为 globalized namespaces 增加渐进连接窗口期，期间按比例削减复制流量（等待手动 force-replicate 兜底），用于平滑地进行跨集群切换。
- [#11967 Add strict state validation to passive replication tests](https://github.com/temporalio/temporal/pull/11967) — 将被动的状态复制验证前置到 replication task 流转过程中，从测试端保障复制状态一致性。

### 基础设施韧性

- [#11969 Track and skip bad ES hostname IPs](https://github.com/temporalio/temporal/pull/11969) — 自研 dial context + 小缓存跳过不可达 ES IP（30s TTL），帮助 Temporal 在 AZ 分区故障后自动恢复。
- [#11966 Replace per-limiter refresh timer with an atomic deadline](https://github.com/temporalio/temporal/pull/11966) — 性能优化：去除 token 操作路径上的 runtime timer 锁竞争。

### 可观测性

- [#11927 Tag Nexus completion callback metrics with nexus_completion_source](https://github.com/temporalio/temporal/pull/11927) — 为 callback 指标新增来源标签，便于区分不同 nexus completion 来源并定位问题。

这些 PR 如按当前节奏推进，Nexus callback observability 与 schedule 迁移稳定性有望进入下一版本。

---

## 用户反馈摘要

### 来自 Issue #11691 的真实痛点

> "A cluster that cannot dispatch a single task should..."

用户描述的场景非常具体：使用 SQL 存储后端的集群在经历一次 session refresh 后，连接池不可恢复地关闭；membership heartbeat 静默失败后集群既不报错也不自愈，而是继续对外宣称 `SERVING`，但**实际上完全无法派发任务**。用户界定的期望行为是：

1. SQL session refresh 应能从自身创建的错误状态

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*