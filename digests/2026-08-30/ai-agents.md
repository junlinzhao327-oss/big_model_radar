# OpenClaw 生态日报 2026-08-30

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-30 00:26 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-30

## 1. 今日速览

过去 24 小时项目保持高活跃度:`Issues` 更新 500 条(新开/活跃 423,关闭 77),`PR` 更新 500 条(待合并 336,合并/关闭 164)。当日无新版本发布,但社区围绕 **Gateway 内存泄漏、消息丢失/截断、会话路由异常** 等 P1 级稳定性问题展开密集讨论,多个高评论 Issue 仍处于 `clawsweeper:needs-maintainer-review` 状态。与此同时,PR 侧有多项针对 Codex 集成、UI 性能、Android 对齐的修复推进,整体呈现“**活跃讨论、修复跟进中、发布窗口静默**”的状态。项目健康度中等偏稳定:问题响应及时,但部分核心稳定性缺陷仍待维护者明确决策。

## 2. 版本发布

当日无新版本 Release。

## 3. 项目进展

当日合并/关闭 PR 164 条,重点集中在以下方向的修复与演进:

| 方向 | 代表 PR | 说明 |
|---|---|---|
| **Codex 集成修复** | [#132936](https://github.com/openclaw/openclaw/pull/132936) | Backport 已合并的 Codex app-inventory 修复,使插件在 read-only/prompt 模式下 app 不消失,当前发布线可用 |
| **Gateway 稳定性** | [#132933](https://github.com/openclaw/openclaw/pull/132933) | 修复同进程内反复 restart 导致的堆内存增长(对应 issue #132914),属于长期内存管理优化 |
| **UI 与客户端对齐** | [#125900](https://github.com/openclaw/openclaw/pull/125900) | Control UI 批量合并 board 元数据查询,减少重复读取,优化大会话量场景下的渲染性能 |
| | [#132849](https://github.com/openclaw/openclaw/pull/132849) | Android 端对齐 Web UI 的聊天、侧边栏和外观,统一多端交互体验,消除导航路径分歧 |
| **语音/TTS 可靠性** | [#118727](https://github.com/openclaw/openclaw/pull/118727) | 将长回复分块发送 TTS,避免超过 `TELEPHONY_DEFAULT_TTS_TIMEOUT_MS` 被静默丢弃 |
| **Agent 工具链** | [#132469](https://github.com/openclaw/openclaw/pull/132469) | 修复 multi-agent 部署下 exec auto-reviewer 和 setup wizard 缺少 ambient owner 导致的 `AgentSelectionRequiredError` |
| **Web Search 错误处理** | [#132755](https://github.com/openclaw/openclaw/pull/132755) | 自托管 provider 缺失 base URL 时按不可用降级,不再将错误结果当作成功返回 |
| **插件工具解析** | [#132753](https://github.com/openclaw/openclaw/pull/132753) | 修复命名空间为 `<prefix>__<tool>` 的 allowlist 条目无法构建插件工具的问题 |

整体来看,项目正在 **通过小步快跑的 PR 修复稳定既有功能**,而非引入大功能变更,为下一个版本窗口积累修复量。

## 4. 社区热点

当日讨论最集中、评论数最高的 Issues 反映了用户对 **稳定性与消息可靠性** 的强烈关注:

| Issue | 评论 | 核心诉求 |
|---|---|---|
| [#91588 Gateway 内存泄漏:350MB → 15.5GB 直至 OOM](https://github.com/openclaw/openclaw/issues/91588) | 22 | 常驻 Gateway 进程 2-3 天即被 OOM kill,触发反复 `launchd-handoff` 重启循环。用户已在 roadmap 中尝试定位泄漏源,但暂无明显修复 PR |
| [#121953 Cron agent 在 DeepSeek 上停顿](https://github.com/openclaw/openclaw/issues/121953) | 13 | OpenClaw 会为 cron agent 消息加 `[cron:<jobId> <name>]` 前缀,导致 DeepSeek API edge 将该请求放入低优先级队列,停顿数十秒至分钟。属于特定供应商行为兼容问题 |
| [#74586 AM embedded run 中止 memory_search](https://github.com/openclaw/openclaw/issues/74586) | 13 | active-memory 插件在 embedded run 中调用 `memory_search` 被中止,模型已完成但被判为 timeout。影响记忆检索功能日常使用 |
| [#84516 Codex 回复静默截断在 ~1000-1100 字符](https://github.com/openclaw/openclaw/issues/84516) | 12 | `openclaw message` 调用 Codex/OAuth agent 时,长回复被截断但 `aborted=false`、`stopReason=null`,用户收到不完整信息且无感知 |
| [#132762 overflow-retry 成功结束但未最终投递](https://github.com/openclaw/openclaw/issues/132762) | 10 | 重试成功后最终 transcript 项是 `toolResult`,缺少 assistant 最终回复,导致多阶段文档工作流未完成交付 |
| [#39476 A2A sessions_send 造成重复消息](https://github.com/openclaw/openclaw/issues/39476) | 12 | Agent B 可反向调用 `sessions_send` 回 Agent A,造成重复投递,超出同步工具语义 |

**热点诉求**:用户普遍期望 OpenClaw 提供 **可预测的会话语义** 和 **强一致的消息投递保证**。尤其是消息截断、重复、延迟、丢失组合出现时,社区对“信任度”的质疑明显上升。

## 5. Bug 与稳定性

当日所列 Bug 中,按严重程度排列如下(**标注是否有 fix PR**):

### P0 / 崩溃级
- **[CLOSED] [#124788](https://github.com/openclaw/openclaw/issues/124788) beta.2 Gateway 事件循环每 ~10.9 分钟阻塞 100-120s**(anchor timer;字符串构建 + fs 扫描;关闭 memory 插件仍复现)。当日已关闭,暂未看到对应 fix PR,属于已解决状态。

### P1 / 严重功能受损
| Issue | 问题 | 标签/状态 | fix PR |
|---|---|---|---|
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | Gateway 内存泄漏至 15.5GB,OOM 反复崩溃 | `no-new-fix-pr`, `needs-maintainer-review` | 无 |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | hook/tool 子进程不回收,产生 zombie 积累,拖慢运行时 | `needs-maintainer-review`, `needs-info` | 无 |
| [#84516](https://github.com/openclaw/openclaw/issues/84516) | Codex 长回复静默截断(~1100 字符),`aborted=false` | `needs-maintainer-review` | 无 |
| [#121953](https://github.com/openclaw/openclaw/issues/121953) | Cron agent 在 DeepSeek 因消息前缀被降级,停顿数十秒 | `needs-product-decision` | 无 |
| [#102534](https://github.com/openclaw/openclaw/issues/102534) | Cron scheduler 在 heavy timeout 后永久停止触发,restart 无效 | `needs-maintainer-review` | 无 |
| [#132762](https://github.com/openclaw/openclaw/issues/132762) | overflow-retry 成功结束但缺少最终交付 | `needs-product-decision` | 无 |
| [#119884](https://github.com/openclaw/openclaw/issues/119884) | DB 迁移后未 ANALYZE,会话操作 15s 延迟 + 事件循环饥饿 | `linked-pr-open` | 有 PR 跟踪(状态待验证) |
| [#91144](https://github.com/openclaw/openclaw/issues/91144) | Windows 原生 CLI Scheduled Task 无法保持运行 | `linked-pr-open` | 有 PR 跟踪 |
| [#91931](https://github.com/openclaw/openclaw/issues/91931) | 预置 SOUL/IDENTITY/USER.md 导致 BOOTSTRAP 被提前删除 | `linked-pr-open` | 有 PR 跟踪 |

### P2 / 功能性缺陷
- **[#74586](https://github.com/openclaw/openclaw/issues/74586)** AM embedded run 中止 memory_search,误判 timeout
- **[#101929](https://github.com/openclaw/openclaw/issues/101929)** context-overflow 估算器高估 2.3-2.6 倍,触发误截断
- **[#69242](https://github.com/openclaw/openclaw/issues/69242)** Linux exec 工具对 find/grep 命令偶发 SIGKILL(无 OOM 证据)
- **[#120735](https://github.com/openclaw/openclaw/issues/120735)** Telegram sticker 入库后无描述、未落盘,agent 不可见
- **[#112160](https://github.com/openclaw/openclaw/issues/112160)** SSH sandbox 不向远端 workspace 暂存入站媒体
- **[#116893](https://github.com/openclaw/openclaw/issues/116893)** browser click 创建的新 tab 不被 tracking/cleanup 管理

### 已有关联修复 PR 的社区关注点
- **[#132908](https://github.com/openclaw/openclaw/pull/132908)** 修复 Codex 0.151.0 分页消息 fork 被拒(close #132893)——已准备合并
- **[#132933](https://github.com/openclaw/openclaw/pull/132933)** 修复 Gateway 同进程重启堆增长(close #132914)
- **[#121044](https://github.com/openclaw/openclaw/pull/121044)** 修复 memory_search 零命中时重建全索引(close #121043)——已 `proof: sufficient`
- **[#131604](https://github.com/openclaw/openclaw/pull/131604)** sandbox 内存 flush 原子追加,消除并发数据丢失

## 6. 功能请求与路线图信号

当日社区提出的功能需求集中在 **可观测性、成本控制、多租户、无障碍** 四个方向:

| 功能需求 | Issue/PR | 可能纳入下一版本的信号 |
|---|---|---|
| **`/models test-fallback` 命令** 验证 fallback 链 | [#6599](https://github.com/openclaw/openclaw/issues/6599) | P3 低优先级,社区自 2 月起持续关注,暂无 PR |
| **子代理完成隔离**(默认只返回状态 + 子会话链接) | [#96975](https://github.com/openclaw/openclaw/issues/96975) | 与 #78055 子代理 stale announce 问题强关联,若解决消息错投则此需求具备实现基础 |
| **多 Teams 机器人共用 Gateway** | [#71058](https://github.com/openclaw/openclaw/issues/71058) | 涉及配置 schema 变更

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目日报 — 2026-08-30

## 1. 今日速览

过去24小时项目整体活跃度高：共产生 **34 项更新**（5 条 Issues + 29 条 PR），全部为新增或活跃状态，无版本发布。值得关注的是，5 条新 Issues 中 4 条为 Bug 报告、1 条为功能请求，其中 2 个 Bug 已有对应 fix PR 挂出，反馈闭环速度良好。另一面，29 条待合并 PR 中有多条已滞留数周（最早可追溯至 6 月 20 日），且过去 24 小时 **0 条 PR 被合并或关闭**，合并通道明显阻塞，长期积压风险需关注。整体判断：社区贡献热情旺盛、Bug 反馈质量高，但维护者侧的审查/合并能力可能成为瓶颈。

---

## 3. 项目进展 （合并/关闭为 0，改看 PR 积累与关键修复就绪状态）

过去 24 小时 **0 条 PR 被合并/关闭**，项目净进展为零。但待合并队列中有多条高价值修复已就绪，等待维护者审查：

- **glob 进程级 cwd 污染修复已就绪**：PR [#4707](https://github.com/OpenHands/software-agent-sdk/pull/4707)（@aniketwaghh）改用 `root_dir` 参数替代 `os.chdir`，直接修复 Issue #4663 中描述的并发数据竞争问题，属于生产环境稳定性关键补丁。
- **事件日志性能优化已就绪**：PR [#4697](https://github.com/OpenHands/software-agent-sdk/pull/4697)（@VascoSch92）将 `EventLog.append` 的时间复杂度从「全目录重新计数」降为常量级，对长会话场景收益显著。
- **LLM 标题生成修复已就绪**：PR [#4703](https://github.com/OpenHands/software-agent-sdk/pull/4703)（@aniketwaghh）修复 Qwen3 等模型返回截断 `<think>` 块而非真实标题的问题（对应 Issue #4530）。
- **远程 WebSocket 客户端可注入化已就绪**：PR [#4135](https://github.com/OpenHands/software-agent-sdk/pull/4135)（@p1c2u）为 `RemoteConversation` 提供工厂注入能力，对应 Feature Issue #4708，设计上消除了模块级全局替换的 hack 方案。
- **Windows 浏览器发现修复已就绪**：PR [#4502](https://github.com/OpenHands/software-agent-sdk/pull/4502)（@KirschBluteX）让 Windows 平台优先使用 Playwright 托管的 Chromium，解决浏览器自动发现失败问题。

此外，队列中还有相当数量的中期 PR 已处于待合并状态，涵盖跨多个模块的修复与特性，按主题归类如下：

| 主题领域 | PR 列表 |
|---|---|
| Agent Server 与上下文 | [#4566](https://github.com/OpenHands/software-agent-sdk/pull/4566)（load_memory 偏好全路径传播）、[#4412](https://github.com/OpenHands/software-agent-sdk/pull/4412)（关闭流程不再强制取消运行任务） |
| MCP/工具兼容 | [#4406](https://github.com/OpenHands/software-agent-sdk/pull/4406)（mcp 1.x Server 装饰器 shim）、[#4322](https://github.com/OpenHands/software-agent-sdk/pull/4322)（anyOf 布尔值类型选择） |
| 遥测与模型适配 | [#4490](https://github.com/OpenHands/software-agent-sdk/pull/4490)（DeepSeek 缓存命中遥测）、[#4550](https://github.com/OpenHands/software-agent-sdk/pull/4550)（Azure API 版本更新） |
| 凭证/安全 | [#4183](https://github.com/OpenHands/software-agent-sdk/pull/4183)（子代理解密 LLM 配置文件）、[#4504](https://github.com/OpenHands/software-agent-sdk/pull/4504)（仓库访问预检） |
| 文件编辑 | [#4582](https://github.com/OpenHands/software-agent-sdk/pull/4582)（EOF 插入拼接修复） |
| 任务跟踪 | [#4470](https://github.com/OpenHands/software-agent-sdk/pull/4470)（稳定任务标识符） |
| 开发者体验/文档 | [#4656](https://github.com/OpenHands/software-agent-sdk/pull/4656)（图像辅助函数文档）、[#4496](https://github.com/OpenHands/software-agent-sdk/pull/4496)（dev.openhands 命名空间） |
| Profile 管理 | [#4372](https://github.com/OpenHands/software-agent-sdk/pull/4372)（默认 Profile 的 LLM 引用同步） |

> ⚠️ 上述所有 PR 均为 OPEN 待合并状态，无一条在过去 24 小时被合入。项目实际推进严重受限于审查带宽。

---

## 4. 社区热点

过去 24 小时讨论最活跃的议题集中在**并发安全**与**运行时可靠性**，是社区当前的核心痛点：

- **[Issue #4663] glob Python 回退方案污染进程级工作目录**（[链接](https://github.com/OpenHands/software-agent-sdk/issues/4663)）— 3 条评论，5 条新 Issue 中热度最高。`os.chdir` 的滥用导致并发执行器与无关线程产生竞态，社区对这类进程级副作用非常敏感。对应修复 PR #4707 已挂出，期待尽快合入。

- **[Issue #4695] token deltas 不再重置运行时空闲计时器，长流式输出可能导致 Pod 被回收**（[链接](https://github.com/OpenHands/software-agent-sdk/issues/4695)）— 由 `#4689` 的流式 delta 投递改为 opt-in 引发回归，`_EventSubscriber` 未选择接收流式增量，导致长任务期间空闲计时器持续累计。此问题直接威胁长时间运行的生产任务稳定性，属于高影响回归。

- **[Issue #4705] GitHub MCP 工具缺少 inputSchema，导致任务列表与自动化页状态不一致**（[链接](https://github.com/OpenHands/software-agent-sdk/issues/4705)）— Agent Canvas 自动化场景下日志出现 44 个验证错误，说明 MCP 工具定义与平台校验层存在契约不一致。

- **[Issue #4708] RemoteConversation 的 WebSocket 客户端不可注入**（[链接](https://github.com/OpenHands/software-agent-sdk/issues/4708)）— 功能请求却获得社区响应，说明有实际用户对传输层有自定义需求，对应 PR #4135 已经准备就绪。

**背后诉求分析**：这波热点集中在「并发正确性」「长任务存活保障」「MCP 生态兼容」三个方向。社区对运行时稳定性的敏感度明显提升，对 MCP 工具在自动化场景下的可靠性提出了更高要求。

---

## 5. Bug 与稳定性

今日 5 条新 Issue 中 4 条为 Bug，按严重程度排序如下：

| 严重程度 | Issue | 描述 | 状态 |
|---|---|---|---|
| 🔴 高 | [#4695](https://github.com/OpenHands/software-agent-sdk/issues/4695) | `#4689` 引入回归：token deltas 不再触发空闲计时器重置，长流式输出期间 Pod 可能被回收，会话中断 | 无 fix PR，需紧急处理 |
| 🔴 高 | [#4663](https://github.com/OpenHands/software-agent-sdk/issues/4663) | glob 的 Python 回退用 `os.chdir` 实现相对路径匹配，进程级副作用引发并发竞态 | 已有 PR [#4707](https://github.com/OpenHands/software-agent-sdk/pull/4707) |
| 🟠 中 | [#4705](https://github.com/OpenHands/software-agent-sdk/issues/4705) | 所有 GitHub MCP 工具缺失 `inputSchema`，自动化场景日志报 44 个校验错误，任务状态显示不一致 | 暂无 fix PR |
| 🟡 低 | [#4709](https://github.com/OpenHands/software-agent-sdk/issues/4709) | `AgentContext.current_datetime` 被持久化到 settings.json，导致后续运行中 prompt 携带过期时间 | 暂无 fix PR，涉及序列化设计问题 |

**风险评估**：`#4695` 属于回归性故障，直接影响长任务可靠性，且 stream delta 机制改动波及面较广，建议优先排查。`#4663` 修复方案已经成熟，合并门槛低。`#4709` 的持久化设计问题虽然严重性低，但对 Agent 上下文正确性有潜移默化的影响，涉及序列化 schema 调整，建议安排进下一个迭代。

---

## 6. 功能请求与路线图信号

今日唯一明确的功能请求是 **[Issue #4708] Injectable WebSocket client factory for RemoteConversation**（[链接](https://github.com/OpenHands/software-agent-sdk/issues/4708)），用户需要在不替换模块全局变量的前提下注入自定义传输层回调客户端。对应的 PR [#4135](https://github.com/OpenHands/software-agent-sdk/pull/4135) 已存在，且该 PR 自 7 月 17 日创建至今已超过 6 周仍未合并，可能说明维护者对 API 设计方向尚未达成一致。此特性有望进入下一版本，但需要维护者尽快表态。

**其他路线图信号**（来自待合并 PR 的隐含方向）：

- **自定义标题生成提示词**（PR [#4564](https://github.com/OpenHands/software-agent-sdk/pull/4564)）— 允许用户传入自定义 prompt 生成会话标题，属于个性化能力增强。
- **仓库访问预检**（PR [#4504](https://github.com/OpenHands/software-agent-sdk/pull/4504)）— 在 Git 路由器中新增认证仓库验证端点，支持可选的 ref 验证，属于信任边界加固方向。
- **稳定任务标识符**（PR [#4470](https://github.com/OpenHands/software-agent-sdk/pull/4470)）— 为 TaskTracker 引入跨重启稳定的 ID，是任务追踪基础设施的重要补强。
- **DeepSeek 缓存命中遥测**（PR [#4490](https://github.com/OpenHands/software-agent-sdk/pull/4490)）— 完善 token 成本核算，对使用 DeepSeek 模型的用户有实际价值。

---

## 7. 用户反馈摘要

- **并发环境下的工具副作用是真实痛点**（Issue [#4663](https://github.com/OpenHands/software-agent-sdk/issues/4663)）：用户指出 `os.chdir` 的进程级副作用在并发 executor 使用场景下会与无关线程产生竞态，说明已有用户在高并发环境中运行该 SDK，且对工具实现的进程安全性有明确期待。
- **流式输出与资源回收的矛盾**（Issue [#4695](https://github.com/OpenHands/software-agent-sdk/issues/4695)）：用户观察到长流式输出场景下 Pod 被回收（`pod reaped`），直接暴露了流式功能改造（`#4689`）对资源管理的副作用，这个反馈对平台稳定性至关重要。
- **MCP 工具与自动化平台集成的一致性问题**（Issue [#4705](https://github.com/OpenHands/software-agent-sdk/issues/4705)）：用户报告 Agent Canvas 自动化场景下 GitHub MCP 工具报 44 个校验错误，说明 MCP 工具在真实自动化流程中的验证需求被低估了。
- **配置持久化的“时间冻结”问题**（Issue [#4709](https://github.com/OpenHands/software-agent-sdk/issues/4709)）：社区用户（@RobG-git）发现 `current_datetime` 在本地序列化后无法刷新，导致 prompt 一直带着过期时间。这提示配置持久化不能「一刀切」，部分字段应排除在序列化之外。
- **传输层定制需求真实存在**（Issue [#4708](https://github.com/OpenHands/software-agent-sdk/issues/4708)）：用户希望注入自定义 WebSocket 客户端，说明有实际部署场景需要自定义传输行为（如代理、认证、心跳机制等）。

---

## 8. 待处理积压

以下 PR/Issue 长期未获维护者响应或合并，值得关注：

| 项目 | 创建时间 | 等待天数 | 说明 |
|---|---|---|---|
| PR [#3811](https://github.com/OpenHands/software-agent-sdk/pull/3811)（workspace `__del__` 防护） | 2026-06-20 | 71 天 | 修复部分初始化实例触发 `__del__` 异常的问题，属于防御性编程修复，风险极低 |
| PR [#4135](https://github.com/OpenHands/software-agent-sdk/pull/4135)（WebSocket 工厂注入） | 2026-07-

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 开源项目动态日报 — 2026-08-30

## 1. 今日速览

过去 24 小时项目活跃度极高。Issue 侧共 42 条更新，其中 37 条被关闭（含大量当天创建即被关闭的 untriaged 报告），另有 5 条新开/活跃；PR 侧共 11 条更新，其中 7 条已合并/关闭，4 条待合并。今日最值得关注的是社区贡献者提交了 4 个修复类 PR（窄终端崩溃、xAI tool_choice、扩展 provider 注册时序、realpath 导入），覆盖了此前用户报告的多个痛点。Issue 关闭率高（37/42 = 88%），说明维护者对社区反馈的处理速度快，项目整体处于健康活跃的迭代节奏。无新版本发布（当前最新为 0.84.4）。

## 2. 版本发布

过去 24 小时内无新版本发布。

## 3. 项目进展

今日有 7 个 PR 被合并/关闭，集中在 coding-agent 稳定性、TUI 渲染和 AI 提供方兼容性三个方面：

**coding-agent 核心稳定性**
- [#8297 fix(coding-agent): exclude superseded retry attempts from restored context](https://github.com/earendil-works/pi/pull/8297) — 修复了重试成功后，被替代的失败尝试仍混入上下文/压缩预算的问题。该 PR 覆盖了长度、token 预算、冷恢复等多个场景，是 coding-agent 上下文管理的重要改进。
- [#8725 fix(coding-agent): settle active turn before in-memory fork](https://github.com/earendil-works/pi/pull/8725) — 修复了 in-memory fork 时机不当导致 `toolResult` 落入错误会话、资源被错误清理的回归问题，对分叉/分支工作流有实质帮助。
- [#8812 fix(coding-agent): flush extension provider registrations before initial model resolution](https://github.com/earendil-works/pi/pull/8812) — 修复了扩展通过 `pi.registerProvider` 注册的 provider 无法用于初始模型解析的时序问题，对依赖第三方 provider 的用户很重要。

**TUI 与 AI 兼容性**
- [#8805 fix(tui): adaptive truncate instead of crash on narrow terminals](https://github.com/earendil-works/pi/pull/8805) — 将窄终端（80-88 列）下的硬崩溃改为自适应截断，直接解决了 #8806 的启动崩溃问题。
- [#8818 fix(ai): omit Responses tool_choice when no tools are sent](https://github.com/earendil-works/pi/pull/8818) — 修复 xAI Grok 在 compaction 时因 `tool_choice` 无对应 tools 数组而 400 报错的问题，对 xAI 用户是关键修复。
- [#8811 feat: add startup composer](https://github.com/earendil-works/pi/pull/8811) — 新增启动阶段输入合成器，允许用户在启动过程中开始输入，并将输入状态无缝带入正常交互模式，改善启动体验。
- [#8819 Fix project name from 'pi' to 'Pi'](https://github.com/earendil-works/pi/pull/8819) — 项目名称大小写修正。

## 4. 社区热点

今日讨论最集中的两个 Issue 均为老问题，评论数持续累积：

- **[#8584 TUI 流式输出行损坏：tool 输出后助手文本逐词换行](https://github.com/earendil-works/pi/issues/8584)** — 25 条评论，9 👍
  用户 @ractive 报告在工具调用输出较长的行后，助手文本流式输出被异常地逐词换行，严重影响阅读。该问题创建于 8 月 24 日，至今讨论热度不减，说明是用户高频遇到的 TUI 渲染缺陷。另一条 [PR #8751 修复 markdown 软换行渲染](https://github.com/earendil-works/pi/issues/8751) 可能部分相关，但 #8584 的触发条件（工具输出后）更为特定，可能涉及更底层的布局状态重置。

- **[#7730 Mac OS 长时间会话高 CPU 占用](https://github.com/earendil-works/pi/issues/7730)** — 13 条评论，9 👍
  用户在 Mac OS 上运行长会话时 CPU 占用在 50-110% 之间波动，内存 600-800MB，疑似与会话长度/上下文大小相关。这是目前最受关注的老问题之一，已开放 3 周多，仍无明确修复方案。

**诉求分析**：两个热点问题分别指向 TUI 渲染质量和长会话资源管理，都是日常重度用户最直接的体验痛点。高 👍 数和高评论数表明这些不是个例，而是影响面较广的共性问题。

## 5. Bug 与稳定性

今日报告的 Bug/回归问题按严重程度排列：

**严重 — 崩溃/不可用**
- [#8806 TUI 在窄终端（80-88 列）启动时硬崩溃](https://github.com/earendil-works/pi/issues/8806) — 启动时渲染行超宽直接报错中断。**已有 fix PR #8805**（合并后即可解决）。
- [#8829 wrapUIPromptContext 复制丢失 UI 原型方法](https://github.com/earendil-works/pi/issues/8829) — 类实例作为 UI 时方法丢失，SDK 扩展兼容性缺陷，直接影响第三方扩展开发。

**中等 — 功能失效/回归**
- [#8753 0.84.3 回归：reasoning_details 回显导致 Venice GLM 推理退化](https://github.com/earendil-works/pi/issues/8753) — 0.84.3 引入的 `preservedReasoningDetails` 回显机制在 Venice 上导致确定性推理退化，0.84.2 正常，属明确的版本回归。
- [#8838 DeepSeek 多轮/工具调用会话报连接错误](https://github.com/earendil-works/pi/issues/8838) — DeepSeek thinking 模式要求回显 `reasoning_content`，否则后续请求失败。API 兼容性问题。
- [#8820 openai-responses: tool_choice 无对应 tools 数组导致 xAI 400](https://github.com/earendil-works/pi/issues/8820) — **已有 fix PR #8818**。
- [#8825 wrapped markdown 表格单元格硬编码 SGR reset，NO_COLOR 失效](https://github.com/earendil-works/pi/issues/8825) — 0.84.3 起的回归，色盲/无障碍用户受影响。
- [#8780 thinking trail 在词边界或字符间换行](https://github.com/earendil-works/pi/issues/8780) — kimi-k3、glm-5.3 上出现，影响思考过程的可读性。
- [#8713 LMStudio 模型无法读取图片](https://github.com/earendil-works/pi/issues/8713) — 配置已启用但模型仍报告图片读取被禁用。
- [#8820 与 #8818 同源问题 — xAI compaction 失败](https://github.com/earendil-works/pi/issues/8820)，已有关联 PR。

**轻微 — 显示/体验问题**
- [#8809 Windows 图片回退路径显示反斜杠](https://github.com/earendil-works/pi/issues/8809) — 显示问题，不影响功能。
- [#8827 LaTeX 兼容字体命令（\rm、\bf）触发整体退化](https://github.com/earendil-works/pi/issues/8827) — 数学公式渲染回退为源码。

## 6. 功能请求与路线图信号

今日收集到的功能需求信号如下：

| 需求 | 来源 | 说明 |
|------|------|------|
| [Command Code 作为内置 provider](https://github.com/earendil-works/pi/issues/8836) | #8836 | 用户希望 `commandcode.ai` 内置在 provider 目录，无需插件 — provider 生态扩展方向 |
| [Opt-in package namespace (pi.namespace)](https://github.com/earendil-works/pi/issues/8834) | #8834 | 包级命名空间，统一管理 skills 和 prompt templates 的命名冲突 — 包管理规范化信号 |
| [暴露审批等待事件给扩展](https://github.com/earendil-works/pi/issues/8835) | #8835 | 扩展需要区分"等待危险工具审批"和"工具正在运行"，wrapper（如 Orca）需要此事件 — SDK 可观测性需求 |
| [@ 工具匹配 git-ignore 文件（带路径前缀时）](https://github.com/earendil-works/pi/issues/8837) | #8837 | 用户希望在 `@` 输入引用时能匹配 git-ignored 文件（显式路径时）— 输入体验优化 |
| [README 增加安装章节](https://github.com/earendil-works/pi/issues/6907) | #6907 | 新用户 onboarding 痛点，持续开放中 |
| [Skill 可见性 API](https://github.com/earendil-works/pi/issues/8533) | #8533 | 扩展可隐藏 Skill，deny-only 窄接口 — 扩展系统权限模型 |

**可能进入下一版本的方向**：#8811 已合入 startup composer，可提升启动体验；#8835 的审批事件暴露如果被接受，将增强扩展生态的集成能力；#8836 的内置 provider 属于低成本高收益的目录扩展。

## 7. 用户反馈摘要

- **包发布后未出现在 gallery**（[#8830](https://github.com/earendil-works/pi/issues/8830)）：用户报告 `@yaosu/pi-path-guard` 发布后，pi.dev 页面和 `pi install` 均正常，但从未出现在 pi.dev gallery 中，包管理可靠性问题影响发布者信心。
- **窄终端用户的挫败感**（[#8806](https://github.com/earendil-works/pi/issues/8806)）：80-88 列终端在启动时直接崩溃，用户明确表达了对硬崩溃的不满，好在 #8805 已提供修复。
- **DeepSeek 用户连接错误**（[#8838](https://github.com/earendil-works/pi/issues/8838)）：首次请求成功、后续请求全部失败，用户对"Connection error"的错误信息感到困惑，因为根因是 `reasoning_content` 未回显，错误提示未给出有效指引。
- **macOS 长会话资源问题**（[#7730](https://github.com/earendil-works/pi/issues/7730)）：用户希望确认是否与会话长度或上下文大小相关，虽然影响使用但反馈仍较为客观。
- **Venice GLM 用户遭遇 0.84.3 回归**（[#8753](https://github.com/earendil-works/pi/issues/8753)）：用户精确对比了 0.84.2 和 0.84.3 的行为差异，并在 issue 中附了详细的退化过程分析——这类反馈对定位回归非常有价值。
- **屏幕阅读器 NVDA 用户的不一致体验**（[#8831](https://github.com/earendil-works/pi/issues/8831)）：`pi -p`（打印模式）可靠，但交互模式输出不一致，无障碍访问问题需要更多关注。

## 8. 待处理积压

以下重要 Issue 长期未获明确修复，建议维护者关注：

- **[#3159 edit 工具超时终止（2026-04-14 创建，未关闭）](https://github.com/earendil-works/pi/issues/3159)** — 4 月报告至今近 4 个月，Qwen 27B 上 edit 工具频繁因超时终止。虽有 8 条评论讨论，但无明确修复方案。影响使用编码助手的核心编辑功能。
- **[#2282 OpenAI Codex OAuth 令牌交换忽略 HTTP_PROXY（2026-03-17 创建）](https://github.com/earendil-works/pi/issues/2282)** — 被标记为 possibly-openclaw-clanker，在受限地区用户中造成 OAuth 流程失败，长期未修复。
- **[#7730 Mac OS 高 CPU 占用（2026-08-06 创建，13 评论，9👍）](https://github.com/earendil-works/pi/issues/7730)** — 已开放超 3 周，至今无官方响应或修复计划，是当前社区关注度最高的开放问题之一。
- **[#8061 上下文预算忽略 maxTokens 输出预留（标记 inprogress）](https://github.com/earendil-works/pi/issues/8061)** — 78% 输入占用即被拒绝 + compact-retry 也失败的组合问题，已标记 `inprogress` 但尚无对应 PR，影响长上下文任务的可靠性。

---

*本日报基于 GitHub 公开数据自动生成，统计窗口为 2026-08-29 UTC 至 2026-08-30。*

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报（2026-08-30）

## 1. 今日速览

过去24小时项目维持**极高速迭代**。PR 更新量达 **235条**（其中99条已合并/关闭），为近期峰值水平，显示内部开发与社区贡献双线推进。Issues 侧 **44条**更新（29条活跃、15条关闭），安全与多租户数据泄露（#24530）和 MCP 自动执行劫持（#37031）成为讨论最集中的话题。值得关注的是多个高价值修复与功能 PR 在今日集中合并（如`content:null`保留、MCP bulk-import、Lakera PII 脱敏修复），同时一批围绕 auto-router 和 websearch 的边界问题在昨日集中上报，形成了"问题发现—快速修复"的良性循环。版本仅在8月10日发布过v1.96.0，已有较长时间未发布新正式版，考虑到今日合并量，预计近期将有版本发布。

---

## 3. 项目进展

今日有 **99条 PR 合并/关闭**，重点关注以下实质性变更：

### 重要修复合并
- **fix: preserve content:null on assistant tool-call turns (#37711)** — PR [#38196](https://github.com/BerriAI/litellm/pull/38196) 合并。修复了 LiteLLM 在传递 assistant 消息时删除 `content` 键的问题，该问题导致部分 provider（如 Anthropic）的反序列化器因缺少该键而报错。对于工具调用场景的正确性修复具有重要意义。
- **fix(proxy): list all non-team models for users with an empty model list** — PR [#38249](https://github.com/BerriAI/litellm/pull/38249) 合并。修复了无团队用户看到空模型列表页面但实际可调用所有模型的矛盾体验，现在列表与真实权限一致。
- **fix(guardrails): stop Lakera monitor mode forwarding unmasked PII on Responses-API bodies** — PR [#38841](https://github.com/BerriAI/litellm/pull/38841) 合并。修复了 Lakera `on_flagged: "monitor"` 模式下未脱敏 PII 被转发给模型的隐私漏洞，属于安全敏感修复。
- **feat(mcp): bulk-import Anthropic MCP connectors via API and admin UI** — PR [#38444](https://github.com/BerriAI/litellm/pull/38444) 合并。新增 admin-only `POST /v1/mcp/server/import` 端点，支持从 Anthropic 连接器 JSON 批量导入 MCP 服务器，显著降低迁移成本。

### 待合并的重要新功能（已进入 CI）
- **feat(complexity_router): opt-in modality-based capability routing for image requests** — PR [#38845](https://github.com/BerriAI/litellm/pull/38845)。解决图像请求落到纯文本 tier 模型导致 400 的问题，新增 `modality_routing` 选项。
- **feat(complexity_router): escalate oversized prompts to a tier that fits before dispatch** — PR [#38844](https://github.com/BerriAI/litellm/pull/38844)。根据提示词大小在分发前自动升级到合适的 tier，避免小型窗口模型的上下文溢出。
- **feat(ui): set a model access group's shared budget from the dashboard** — PR [#38843](https://github.com/BerriAI/litellm/pull/38843)。在 Models & Endpoints 页面新增 Model Access Group Budgets 标签页，支持设置/编辑/清除共享预算。
- **fix(responses): drop unsupported reasoning param for openai non-reasoning models** — PR [#38842](https://github.com/BerriAI/litellm/pull/38842)。修复 Codex 向 gpt-4o 等非推理模型发送 `reasoning` 参数被 OpenAI 400 的问题。
- **perf(sdk): measure and improve Python SDK load time and package size** — PR [#38849](https://github.com/BerriAI/litellm/pull/38849)。为 SDK 性能建立可复现的基线测量体系。

**项目整体前进幅度**：今日 PR 合并集中在（1）Anthropic/Claude Code 生态兼容性修复、（2）MCP 管理能力增强、（3）guardrails 安全修复、（4）dashboard/UI 功能补齐。auto-router 系列 PR 密集提交表明团队正在系统性地加强复杂路由能力。

---

## 4. 社区热点

### 最热 Issue：/metrics 未鉴权暴露多租户数据（#24530）
- 链接：[#24530](https://github.com/BerriAI/litellm/issues/24530)
- 评论数：8 | 创建于2026-03-24，至今仍开放
- **核心诉求**：`/metrics` Prometheus 端点**默认不鉴权**，在生产环境中暴露多租户 PII 数据。虽然有 `require_auth_for_metrics_endpoint: true` 可选配置，但不安全默认值导致广泛部署存在风险。
- **社区反应**：该 issue 长期活跃（6个月未关闭），说明用户对默认安全配置有强烈期待。结合 #35766（数据库索引问题）和 #36548（LoggingWorker 事件循环问题），社区对生产环境稳定性和安全性的关注度持续上升。

### 次热 Issue：MCP 自动执行劫持客户端工具（#37031）
- 链接：[#37031](https://github.com/BerriAI/litellm/issues/37031)
- 评论数：7 | 创建于2026-08-15，状态开放
- **核心诉求**：配置了 `require_approval: "never"` 的 MCP 工具在代理端自动执行，但当 Claude Code 等 agentic 客户端在同一请求中携带自己的工具（Read/Bash/Edit）时，自动执行循环会**劫持**客户端工具，导致所有非 MCP 工具报 "Error executing tool"。
- **影响面**：使用 Claude Code + MCP + LiteLLM 代理的组合用户受影响，涉及代理端自动执行与客户端工具执行的冲突语义。

### 值得关注：/ui/login 404（#29340）
- 链接：[#29340](https://github.com/BerriAI/litellm/issues/29340)
- 评论数：4 | 创建于2026-05-30，仍有用户受影响
- **核心诉求**：`/ui/login` 返回 404 而 `/fallback/login` 正常，用户怀疑与 nginx 规则有关，但 issue 被标记为 stale，尚未明确修复方案。

---

## 5. Bug 与稳定性

### 严重（安全或数据泄露风险）

- **[/metrics 未鉴权暴露 PII（#24530）](https://github.com/BerriAI/litellm/issues/24530)** — 默认未鉴权，多租户数据泄露。**开放中，无关联 fix PR**。严重度：★★★★★

### 高（重大功能异常或性能退化）

- **[MCP 自动执行劫持客户端工具（#37031）](https://github.com/BerriAI/litellm/issues/37031)** — 自动执行循环覆盖客户端自带工具，报"Error executing tool"。**开放中，无关联 fix PR**。严重度：★★★★
- **[LiteLLM_SpendLogs 缺少 (api_key, startTime) 索引（#35766）](https://github.com/BerriAI/litellm/issues/35766)** — 预算窗口花费重置时 seq-scan 全表，导致数据库饱和、事务 P2028 失败。**已关闭**，关联 fix PR [#38851](https://github.com/BerriAI/litellm/pull/38851)（将预算窗口种子从请求ID改为按时间边界）今日已提交。严重度：★★★★
- **[流式响应丢失上游 usage（#36168）](https://github.com/BerriAI/litellm/issues/36168)** — 最终 chunk 带非空 `choices` 时，`cached_tokens` 丢失，按全价计费。**开放中**。严重度：★★★★
- **[litellm 停止转发模型请求（#38731）](https://github.com/BerriAI/litellm/issues/38731)** — 使用 mgmt API 自动创建/删除临时密钥后，代理停止转发请求。**开放中，今日新上报**。严重度：★★★★
- **[LoggingWorker 事件循环切换丢失任务和队列（#36548）](https://github.com/BerriAI/litellm/issues/36548)** — 多事件循环进程下 `_ensure_queue` 未取消旧任务即切换，导致日志丢失。**开放中**。严重度：★★★
- **[Azure Responses API streaming 因 stream_options 失败（#28553）](https://github.com/BerriAI/litellm/issues/28553)** — 阻止 Codex 使用，**已关闭**。严重度：★★★

### 中（特定场景功能异常）

- **[websearch_interception 的 chat-completions agentic follow-up 崩溃（#38828/#38829）](https://github.com/BerriAI/litellm/issues/38828)** — `acompletion()` 收到重复的 `aws_region_name`；绕过后又报 "LLM Provider NOT provided"。**今日新上报，开放中**。
- **[vertex_ai Gemini embeddings 融合列表输入为一个向量（#38823）](https://github.com/BerriAI/litellm/issues/38823)** — 传 N 个输入只返回 1 个 embedding，但按 N 个计费。**今日新上报**。
- **[limit-busy routing 不够均衡（#37622）](https://github.com/BerriAI/litellm/issues/37622)** — 负载均衡策略未按预期工作。**开放中**。
- **[SSO 配置部分修改时回填 client_secret（#38177）](https://github.com/BerriAI/litellm/issues/38177)** — 编辑 SSO 配置部分字段时 `client_secret` 被意外回填。**开放中**。
- **[/model/new 返回 500 但配置已持久化（#38556）](https://github.com/BerriAI/litellm/issues/38556)** — 用户收到错误但实际已成功。**已关闭**。
- **[cache_control_injection_points 落在顶层字段而非消息上（#38718）](https://github.com/BerriAI/litellm/issues/38718)** — 长多轮工具调用对话中，`/v1/messages` 的缓存控制注入点错位。**开放中**。

### 低（体验或边缘问题）

- **[删除密钥确认对话框未忽略首尾空格（#38732）](https://github.com/BerriAI/litellm/issues/38732)** — 限制了密钥名不能包含首尾空格，但对话框比较时未忽略。**开放中**。
- **[arm64 Docker 镜像实际是 amd64 二进制（#29382）](https://github.com/BerriAI/litellm/issues/29382)** — 镜像标签错误，可正常运行但架构不符合预期。**开放中，标记 stale**。

---

## 6. 功能请求与路线图信号

### 高可能性进入下一版本（已有对应 PR）

| 功能需求 | 来源 Issue | 对应 PR | 状态 |
|---------|-----------|---------|------|
| Auto-router 模态感知路由（图像请求） | 社区反馈（无明确issue） | [#38845](https://github.com/BerriAI/litellm/pull/38845) | OPEN/待合并 |
| Auto-router 按提示词大小自动升级 tier | 同上 | [#38844](https://github.com/BerriAI/litellm/pull/38844) | OPEN/待合并 |
| Dashboard 设置模型访问组共享预算 | 用户需求 | [#38843](https://github.com/BerriAI/litellm/pull/38843) | OPEN/待合并 |
| MCP 连接器批量导入 | 迁移用户痛点 | [#38444](https://github.com/BerriAI/litellm/pull/38444) | 已合并 |
| SDK 性能测量基准 | 开发可观测性 | [#38849](https://github.com/BerriAI/litellm/pull/38849) | OPEN/待合并 |

### 社区提出的新功能需求（尚未有 PR）

- **[[Feature] vertex_ai Gemini embeddings 支持 per-input fan-out 或警告（#38823）](https://github.com/BerriAI/litellm/issues/38823)** — 建议增加参数控制列表输入的展开方式，或在返回单个向量时给出警告。
- **[[Feature] auto-router 分类器成本从 savings 中扣减（#38816）](https://github.com/BerriAI/litellm/issues/38816)** — 要求自动路由的 "savings" 计算考虑 classifier 成本，否则会夸大节省金额。
- **[[Feature] 在 /health 中将 auto-router 报告为 not applicable（#37967）](https://github.com/BerriAI/litellm/issues/37967)** — 自动路由器报告为"健康"会对用户产生误导，应标记为"不适用"。此 issue 已关闭，可能已在讨论中。

### 路线图信号

- **Auto-router 能力矩阵持续扩展**：从复杂度路由→模态感知→提示词大小感知，团队正将 auto-router 从"按复杂度分流"升级为"多维度智能路由"。这将是 LiteLLM 相比其他代理方案的核心差异化能力。
- **MCP 管理面快速补齐**：从单个连接器管理到批量导入，MCP 功能正在从"可用"走向"可运营"。

---

## 7. 用户反馈摘要

### 生产环境安全担忧
> "The `/metrics` Prometheus endpoint is **unauthenticated by default** and exposes sensitive multi-tenant data in production."
> — [#24530](https://github.com/BerriAI/litellm/issues/24530)

用户对默认不安全的配置强烈不满，尤其是在多租户生产部署中。6个月未关闭说明该问题可能涉及架构决策而非简单配置修改。

### 数据库性能在正常流量下崩溃
> "Under normal traffic, our proxy fleet started failing spend-update transactions with Prisma `P2028`... The Postgres instance (AWS RDS, 2 vCPU) was pinned..." — [#35766](https://github.com/BerriAI/litellm/issues/35766)

花费记录表缺少关键索引，导致预算功能在正常流量下即触发数据库饱和。**相关修复 PR [#38851](https://github.com/BerriAI/litellm/pull/38851) 今日已提交**，表明团队已定位根因。

### 成本统计不一致导致用户不信任
> "Returns HTTP 200, so callers silently lose N-1 vectors and are charged for all N inputs." — [#38823](https://github.com/BerriAI/litellm/issues/38823)

多个成本/用量计算问题（#36168、#38823、#30635）表明计费准确性是用户最敏感的痛点之一，尤其是"多收钱"或"少退钱"的情况。

### 复杂客户端生态协作问题
> "The auto-execute loop takes over... breaking all non-MCP tools with 'Error executing tool'." — [#37031](https

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*