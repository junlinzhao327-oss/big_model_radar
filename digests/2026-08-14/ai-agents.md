# OpenClaw 生态日报 2026-08-14

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-13 23:07 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

⚠️ 摘要生成失败。

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-14

## 1. 今日速览

过去24小时项目处于**高活跃度**状态：累计 427 条 Issue 更新（314 新开/活跃 vs 113 关闭）、500 条 PR 更新（325 待合并 vs 175 已合并/关闭），并发布补丁版本 v0.20.1（v2026.8.13）。社区讨论热度集中在 **token 开销优化**（#6839 获 39 评论）、**插件接口标准化**（#64182/#64231 合计 61 评论）与 **Windows/macOS 桌面端稳定性回归**（#83683/#84185/#52010 均为 P1/P2 Bug）。v0.20.1 作为 v0.20.0 发布以来的约 656 个 PR 的稳定汇总标签，为下游（Docker、托管部署、tag 安装）提供了明确基线，整体项目健康度良好，但桌面端多平台回归与 session 状态问题仍需关注。

---

## 2. 版本发布

### Hermes Agent v0.20.1 (v2026.8.13)
- **发布日期：** 2026年8月13日
- **性质：** Patch Release —— 将 v0.20.0 以来约 **656 个 PR** 汇总为稳定标签，供 Docker 镜像、托管部署及按 tag 安装的下游消费者使用。
- **变更内容：** 补丁级修复与稳定性改进（未披露具体破坏性变更）；无显式迁移步骤说明。
- 📎 [Release 页面](https://github.com/NousResearch/hermes-agent/releases)

---

## 3. 项目进展

过去 24 小时**合并/关闭 PR 175 条**，对应一批 Issue 状态更新，反映以下方向的实际推进：

- **插件体系收尾**：#64182（插件接口扩展追踪）、#64178（全表面 hook 投递对齐）、#64161（流式输出 observer hooks）均转为 **CLOSED**，说明社区插件接口扩展的标准化工作已阶段性完成。
- **记忆与状态修复**：#5820（记忆同步召回选项）已关闭；#69603（state.db 修复后复损坏的 schema 级根因）已关闭，session 存储层的稳定性问题得到解决。
- **CLI/Browser 依赖修复**：#43564（`hermes update` 误删 agent-browser 依赖）已关闭，更新链路可靠性提升。

**关键待合并 PR（推进中）：**
- [#84876](https://github.com/NousResearch/hermes-agent/pull/84876)：序列化 API server 中同一 session 的并发 agent turns，修复会话历史竞争 —— 直接回应 P1 问题 #84185 等一批 stall 报告。
- [#81605](https://github.com/NousResearch/hermes-agent/pull/81605)：子代理使用独立 SessionDB 连接而非共享父句柄，salvage #81267/#81343。
- [#85687](https://github.com/NousResearch/hermes-agent/pull/85687) 与 [#85689](https://github.com/NousResearch/hermes-agent/pull/85689)：Kanban 子卡 session 继承与 review-handoff 防滞留。

---

## 4. 社区热点

| 排名 | Issue/PR | 评论数 | 主题 | 核心诉求 |
|---|---|---|---|---|
| 1 | [#6839](https://github.com/NousResearch/hermes-agent/issues/6839) | 39 | Lazy Tool Schema Loading | 每次 API 调用注入全部工具 schema（50+ 工具约 3500-5000 tokens），本地模型上成本与延迟极高，要求双通道懒加载 |
| 2 | [#64182](https://github.com/NousResearch/hermes-agent/issues/64182) | 35 | 插件接口扩展追踪（已关闭） | 社区长期 PR 需要稳定、公开的插件接口标准才能合入 |
| 3 | [#34352](https://github.com/NousResearch/hermes-agent/issues/34352) | 27 | Multi-Tenant Hermes | 记忆操作绕过 hook 系统导致多租户隔离无法实现，用户已自维护生产补丁数月 |
| 4 | [#64231](https://github.com/NousResearch/hermes-agent/issues/64231) | 26 | 生命周期事件目录与 hook 分类 | 一次性梳理挂起的 observer-hook PR 集群，避免逐个零散合入 |
| 5 | [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) | 24 | Skills 索引自动探测失败 | 文档站 skills-index 已过期 29.8h（限制 26h），自动化 freshness 探针持续告警 |

**分析：** 社区最强烈的信号是**降低 token 开销**与**插件/钩子体系的标准化**。前者直接影响本地模型用户的可用性与成本；后者是大量社区 PR 长期滞留的根因 —— 维护者需尽快就 #64231 的「事件目录 + hook 验收标准」做出决策。

---

## 5. Bug 与稳定性

### P1 严重（按影响面排序）

| Issue | 平台 | 问题描述 | Fix PR 状态 |
|---|---|---|---|
| [#83683](https://github.com/NousResearch/hermes-agent/issues/83683) | Windows | 桌面应用重启即杀掉网关且不重启（WeChat/QQ/Telegram 全部静默）；0.20.0 回归 | 无直接对应 PR，需排查 |
| [#84185](https://github.com/NousResearch/hermes-agent/issues/84185) | Windows | `hermes update` 后网关冷启动静默死亡，无日志/PID/退出记录 | 无直接对应 PR |
| [#82001](https://github.com/NousResearch/hermes-agent/issues/82001) | 跨平台 | 压缩后 session 续接失败，误导用户「磁盘已满」；DB 正常 | [#84876](https://github.com/NousResearch/hermes-agent/pull/84876)（序列化并发 turns，可能缓解） |
| [#69592](https://github.com/NousResearch/hermes-agent/issues/69592) | TUI | 加载 ambient widgets 后 `/sessions`、`/models` 覆盖层不可见，**已持续 13 天** | 无 |
| [#78069](https://github.com/NousResearch/hermes-agent/issues/78069) | 多平台 | 工具自由文本响应间歇性无法绑定 pending clarify 调用，turn 无限挂起 | 无 |

### P2 中等

| Issue | 平台 | 问题描述 |
|---|---|---|
| [#52010](https://github.com/NousResearch/hermes-agent/issues/52010) | macOS | 每次桌面更新后 Full Disk Access 被吊销，需手动重新授权 |
| [#73082](https://github.com/NousResearch/hermes-agent/issues/73082) | 桌面端 | Renderer/GPU 进程空闲时 100%+ CPU，持续重渲染循环 |
| [#82936](https://github.com/NousResearch/hermes-agent/issues/82936) | 跨平台 | 多 profile 模式下默认 profile 的 secrets 泄漏到次级 profile 的 terminal 与 Kanban 子进程 |
| [#82887](https://github.com/NousResearch/hermes-agent/issues/82887) | Linux | terminal 工具执行二进制路径时崩溃 `embedded null character in path`（根因 `_read_script_in_env`） |
| [#68321](https://github.com/NousResearch/hermes-agent/issues/68321) | 桌面端 | 切换 chat 再切回后所有 assistant 消息消失（DB 完好） |
| [#32528](https://github.com/NousResearch/hermes-agent/issues/32528) | QQ Bot | C2C 私聊按钮审批永远判为 unauthorized（chat_type dm vs c2c 不匹配） |
| [#43564](https://github.com/NousResearch/hermes-agent/issues/43564) | CLI | `hermes update` 误删 agent-browser 依赖（已关闭，修复已合入） |

### P3 低等级
- [#66616](https://github.com/NousResearch/hermes-agent/issues/66616)：Skills 索引 cron 过期，文档站信息陈旧。
- [#83390](https://github.com/NousResearch/hermes-agent/issues/83390)：DeepSeek 上辅助 title_generation 报 HTTP 400（response_format 不可用）。
- [#58596](https://github.com/NousResearch/hermes-agent/issues/58596)：Python 3.14 下 `DaemonThreadPoolExecutor` 因 `_initializer` 属性移除崩溃，影响所有并发功能。
- [#69603](https://github.com/NousResearch/hermes-agent/issues/69603)：state.db 修复后复损坏的 schema 根因（已关闭）。

---

## 6. 功能请求与路线图信号

| 功能需求 | Issue | 相关 PR / 状态 | 纳入下一版本可能性 |
|---|---|---|---|
| Lazy Tool Schema 双通道注入 | [#6839](https://github.com/NousResearch/hermes-agent/issues/6839) | 无对应 PR；39 评论、18 👍 | **高** —— 直接解决 token 成本痛点 |
| MCP 非交互式工具配置 | — | [#85688](https://github.com/NousResearch/hermes-agent/pull/85688)、[#85686](https://github.com/NousResearch/hermes-agent/pull/85686)（均 8-13 新开） | **高** —— 适配 CI/脚本化运维需求 |
| Webhook 执行注册表（状态/取消） | [#84834](https://github.com/NousResearch/hermes-agent/issues/84834) | [#85674](https://github.com/NousResearch/hermes-agent/pull/85674) | **高** —— Webhook Revolution 战役第 11 项 |
| Webhook 签名回调（SSRF 防护） | #4386/#73828 | [#85675](https://github.com/NousResearch/hermes-agent/pull/85675) | **高** —— 安全合规必备 |
| 跨平台 session 共享（CLI↔Telegram） | [#4335](https://github.com/NousResearch/hermes-agent/issues/4335) | 无；14 评论、3 👍 | 中 —— 需求存在但涉及架构改动 |
| Signal 原生引用/编辑/撤回 | [#39043](https://github.com/NousResearch/hermes-agent/issues/39043) | 无；3 👍 | 中 —— 平台差异化能力 |
| 多租户 Hermes | [#34352](https://github.com/NousResearch/hermes-agent/issues/34352) | 用户自维护补丁，等待官方架构决策 | 低（短期）—— 需核心重构 |
| 桌面端关闭到托盘 / 磨砂玻璃 | — | [#78343](https://github.com/NousResearch/hermes-agent/pull/78343)、[#84329](https://github.com/NousResearch/hermes-agent/pull/84329) | 高（若桌面团队有容量） |
| OpenRouter 实际成本记录 | — | [#85690](https://github.com/NousResearch/hermes-agent/pull/85690) | 高 —— 用量/成本透明化趋势 |

**路线图信号：** 8 月 13 日密集出现了 **MCP 可脚本化**、**webhook 可观测**、**provider 成本记录**三类 PR，预示下一版本将强化**可运维性（Ops-friendly）** 与**成本治理**能力。

---

## 7. 用户反馈摘要

**高频痛点（按声量排序）：**

1. **Token 开销失控**（#6839）：50+ 工具全量注入 schema 导致本地模型每次请求多花 3500-5000 tokens，用户明确表示「无论对话是否需要这些工具都如此」—— 这是本地模型部署的最大阻力。
2. **Windows 桌面端更新/重启即断连**（#83683、#84185）：用户形容「WeChat/QQ/Telegram 全部静默」「spawned 进程立即死亡且无任何日志」，且属 0.20.0 回归，信任损伤较大。
3. **TUI 核心功能连续 13 天不可用**（#69592）：`/sessions`、`/models` 是切换会话和模型的基础操作，用户以「Day 13 since this broke」反复更新，表达强烈不满。
4. **macOS 权限反复吊销**（#52010）：每次桌面更新需手动重授 Full Disk Access，长期消耗用户信任。
5. **多租户隔离不可用**（#34352）：用户「已在生产环境自维护补丁数月」，希望官方采纳而非 fork 核心。
6. **stall/hang 问题面广**（#84047）：社区成员主动通读 77 个 open stall 报告，归纳为 7 种机制，并指出「约三分之一不是运行时问题而是安装器问题」—— 说明 issue 分类与引导需改进。

**积极反馈：**
- #69603 的修复（schema 修复串行化 + cookie bump）已关闭，说明 session 存储层根因修复有效。
- 插件系列（#64182/#64178/#64161）关关闭标志着社区期待的插件接口稳定化尘埃落定。

---

## 8. 待处理积压

**长期未决的重要 Issue：**

| Issue | 创建时间 | 滞后期 | 备注 |
|---|---|---|---|
| [#6839](https://github.com/NousResearch/hermes-agent/issues

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-08-14

## 今日速览

过去24小时项目活跃度较高：7条Issue更新（5条活跃、2条关闭），28条PR更新（24条待合并、4条已合并/关闭），无新版本发布。核心焦点集中在 **agent-server 性能修复**（#4480/#4481/#4483 三连修复生产环境阻塞与侧边栏慢问题）与 **ACP（Agent Client Protocol）可观测性增强**（#4368/#4485）。同时，SDK 仓库的工程规范化持续推进——ready-for-dev 工作流门禁已落地（#4464 已合并/关闭），并新增了并发负载测试任务（#4477）。项目整体处于功能迭代与稳定性加固并行的健康状态。

---

## 版本发布

无新版本发布。

---

## 项目进展

今日共 **4 条 PR 已合并/关闭**（对应 Issue 均已关闭），核心成果如下：

| PR | 对应 Issue | 说明 |
|---|---|---|
| [#4481 [合并] fix(agent-server): move bash event search off event loop and replace glob with scandir](https://github.com/OpenHands/software-agent-sdk/pull/4481) | #4480 | 修复 agent-server 在 bash_events 目录上阻塞事件循环的问题，用 scandir 替代 glob，并对 `BashEventService.search_bash_events` / `get_bash_event` 做异步化改造，消除对并发会话与搜索的饥饿效应 |
| [#4483 [合并] perf(agent-server): cache unchanged conversation summaries](https://github.com/OpenHands/software-agent-sdk/pull/4483) | — | 缓存未变化的会话摘要，修复服务端会话侧边栏在长运行环境下的剩余性能瓶颈 |
| [#4482 [合并] feat(file-router): add POST /file/create_directory](https://github.com/OpenHands/software-agent-sdk/pull/4482) | — | 新增文件路由的建目录端点，基于端到端实测验证（agent-server 在 :18923 端口启动并完整驱动） |
| [#4464 [合并] Add ready-for-dev issue and PR gates](https://github.com/OpenHands/software-agent-sdk/pull/4464) | #4463 | 从 OpenHands/OpenHands 移植 ready-for-dev 工作流：Issue 就绪度评估 + PR 关联 Issue 校验门禁，提升仓库协作规范 |

**整体评价**：性能问题从"发现"到"修复合并"在 24 小时内完成闭环，体现了项目对生产环境稳定性问题的高响应速度；工程规范建设（门禁自动化）也有实质推进。

---

## 社区热点

**1. #976 — [Tracker] Daily Examples Run Results**（62 条评论）
🔗 https://github.com/OpenHands/software-agent-sdk/issues/976

这是每日示例脚本运行结果的自动跟踪 Issue（创建于 2025-10-31，仍在持续更新），作为 CI 计划任务（`.github/workflows/run-examples.yml`）的结果看板，持续监控示例代码的健康度。社区对其保持关注，说明 SDK 示例的回归稳定性是用户关心的重点。

**2. #4405 — Spec: Support Agent Plugins 可移植包格式**（4 条评论）
🔗 https://github.com/OpenHands/software-agent-sdk/issues/4405

讨论 Agent Plugins（agent-plugins.org）这一厂商中立的插件打包标准（v1.0.0）在 SDK 中的支持方案。该标准的技术指导委员会成员来自 Amazon、Cursor、Microsoft 等核心厂商，属于行业级的互操作性方向。配套的 #4453（路径安全）也处于 Needs Design 状态，表明该方向仍在设计中。

**3. #[PR #4461] fix(sdk): cap condenser token limit by agent context**（标记为 review-this）
🔗 https://github.com/OpenHands/software-agent-sdk/pull/4461

虽评论数未显示，但作为 `[review-this]` 重点审查 PR，涉及对话压缩器（condenser）的 token 上限与 agent 上下文窗口的匹配问题——这直接影响长对话场景下的上下文管理质量，是 SDK 核心调用路径的重要调优。

---

## Bug 与稳定性

按严重程度排列：

| 严重度 | Issue/PR | 说明 | 状态 |
|---|---|---|---|
| 🔴 高 | [#4480 — agent-server 在 bash_events 目录上阻塞事件循环](https://github.com/OpenHands/software-agent-sdk/issues/4480) | 生产环境性能回归：同步 glob 遍历无界目录导致事件循环阻塞，饥饿并发会话与搜索。作者 @neubig 在长运行实例上成功复现 | ✅ 已关闭，由 #4481 修复（已合并） |
| 🔴 高 | [#4368 — ACP 对话对 Laminar 观测平台不可见](https://github.com/OpenHands/software-agent-sdk/issues/4368) | ACP 对话产生的 spans 中缺少 assistant 轮次/工具调用/token 用量，导致与"agent 未运行"在结构上无法区分，破坏可观测性 | ⏳ 待修复，#4485 PR 尝试解决（见下） |
| 🟡 中 | [#4477 — 缺少并发会话的廉价负载测试](https://github.com/OpenHands/software-agent-sdk/issues/4477) | 近期回归曾导致 LLM 调用无法并行，agent-server 在 LLM 慢时退化为单线程。当前无廉价负载测试可捕获此类问题 | ⏳ 待开发（已标记 ready-for-dev） |
| 🟢 低 | #4482 关闭时无相关 bug | 已合并，无遗留问题 | ✅ |

**相关修复 PR 追踪**：观察 #4485（feat(tracing): record ACP turn usage）描述，其提到 #4368 中列出的 4 个观测性缺口（LLM 等价 spans/TOOL spans/token 属性/model 标识）中，前两个已被 PR #4376 覆盖，该 PR 补足后两个。

---

## 功能请求与路线图信号

**1. Agent Plugins 标准支持（#4405 + #4453，均标记 Needs Design）**
🔗 https://github.com/OpenHands/software-agent-sdk/issues/4405
🔗 https://github.com/OpenHands/software-agent-sdk/issues/4453

行业级插件互操作标准（agent-plugins.org v1.0.0）的集成提案。配套的安全设计（路径包含校验、窄失败边界）也进入设计阶段。该方向涉及多家大厂，是 SDK 走向开放生态的关键布局，预计后续会有设计文档产出。

**2. 并发负载测试（#4477，标记 ready-for-dev）**
🔗 https://github.com/OpenHands/software-agent-sdk/issues/4477

直接源自并发回归事故，属于工程效能型需求，已可作为新人友好任务。

**3. Pi ACP provider 内置支持（PR #4419）**
🔗 https://github.com/OpenHands/software-agent-sdk/pull/4419

在 ACP_PROVIDERS 注册表中添加 Pi 编码代理，并在 Docker 镜像中预装 `pi-acp`。呼应 OpenHands/OpenHands#16204，预计随下一版本合并。

**4. 基础设施：Provider Connection 端点（PR #4455，标记"Blocks all other PRs"）**
🔗 https://github.com/OpenHands/software-agent-sdk/pull/4455

"一次连接 provider、从所有模型中选用"功能的后端基础，采用命名密钥存储。因阻塞多个后续 PR，属高优先级合并对象。

---

## 用户反馈摘要

- **生产环境性能痛点（真实声音）**：Issue #4480 作者 @neubig 从长运行实例的实测中发现 bash 事件目录的 glob 阻塞问题，并指出与已关闭的 #674 是不同层级（remote-workspace 过滤 vs agent-server 事件循环阻塞）。同类问题在 #4483 中也有体现（会话侧边栏缓慢）。

- **企业级持久化诉求（PR #4476）**：企业临时沙箱在恢复时会丢失 `~/.openhands`，用户要求所有用户态路径尊重 `OH_PERSISTENCE_DIR` 环境变量。这暴露了企业部署中状态持久化的实际场景需求。

- **开发者工具链反馈**：多位贡献者提交"低价值测试删除 + 简化"（#4484）、`str_replace` 上下文窗口不完整（#4472）、终端别名重复添加（#4471）等经验性问题，反映活跃的外部贡献者群体在使用中主动打磨细节。

- **可观测性不满**：ACP 对话在 Laminar 上不可见（#4368），用户明确表示"ACP 对话与 agent 从未运行的会话在结构上不可区分"，对调试和成本追踪造成困扰。

---

## 待处理积压

| 项目 | 类型 | 待办时长 | 说明 | 建议 |
|---|---|---|---|---|
| [#976 Daily Examples Run Results](https://github.com/OpenHands/software-agent-sdk/issues/976) | 自动跟踪 Issue | 自 2025-10-31 起持续 | 62 条评论，作为示例回归看板长期开放 | 建议评估是否补充自动化告警，避免异常结果被淹没在评论流中 |
| [#4115 Fix agent server on Windows crash](https://github.com/OpenHands/software-agent-sdk/pull/4115) | PR | 开放约 1 个月（2026-07-14 创建） | Windows 平台崩溃修复，作者已在干净环境本地验证，无 review 进展 | 建议分配 Windows 环境 reviewer 验证并推进合并 |
| [#3673 feat(sdk): add ask_oracle tool](https://github.com/OpenHands/software-agent-sdk/pull/3673) | PR | 开放约 2 个月（2026-06-11 创建） | 功能已由人类测试验证，提供视觉 walkthrough，标记 review-this + integration-test，但仍未合并 | 建议维护者评估优先级——这是 LLM 自我纠错能力的重要增强 |
| [#4455 Provider Connection 端点（阻塞多个 PR）](https://github.com/OpenHands/software-agent-sdk/pull/4455) | PR | 开放 4 天（2026-08-10 创建） | 声明"Blocks all other PRs"，属于基础设施级合并前置 | 建议优先安排 review，避免成为依赖链瓶颈 |

---

*数据基于 GitHub API 截至 2026-08-14 的过去 24 小时更新。*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，这是 Pi 项目 2026 年 8 月 14 日的项目动态日报。

---

## Pi 项目动态日报 — 2026-08-14

### 1. 今日速览

过去 24 小时项目活跃度极高。Issue 与 PR 的总更新量达 62 条，其中 Issue 关闭数（32）显著高于新开/活跃数（17），表明维护团队正在积极处理社区反馈并关闭积压问题。PR 方面，有 6 条被合并或关闭，其中包含多项针对 TUI 终端卫生与 CLI 参数解析的重要修复。社区对 `auto-compaction` 失效类问题的讨论热度最高，反映了用户对长会话稳定性的核心诉求。当前无新版本发布，项目处于频繁迭代与问题修复阶段。

### 2. 版本发布

无。

### 3. 项目进展

今日合并的 PR 主要围绕稳定性和终端体验修复，项目整体向更稳健的方向迈进了一步。

- **修复大型会话恢复导致终端被刷屏的问题**：[#8082](https://github.com/earendil-works/pi/pull/8082) 已合并。该 PR 还修复了 SIGINT 后终端进入 raw mode 无法恢复的问题，属于终端卫生方面的关键修复。
- **修复布尔扩展标志吞掉后续命令行参数的问题**：[#8084](https://github.com/earendil-works/pi/pull/8084) 已合并。此修复解决了 `pi -p --plan "prompt"` 这类命令因标志类型未知而错误消费 prompt 的问题。
- **增强 Gemini 工具调用兼容性**：[#8086](https://github.com/earendil-works/pi/pull/8086) 已关闭。当某些端点拒绝未知 JSON Schema 字段时，自动回退到旧版 Gemini 工具 schema。
- **废弃 PR 清理**：[#7993](https://github.com/earendil-works/pi/pull/7993) 被作者主动关闭，标注为 "agent gone wild"，已清理。

### 4. 社区热点

- **[Bug] auto-compaction 从不触发，直到上下文超过 100% 直至 provider 溢出** ([#6879](https://github.com/earendil-works/pi/issues/6879))
  - **热度**：19 条评论，17 个 👍，是过去 24 小时讨论最激烈、关注度最高的问题。
  - **详情**：用户在 GPT-5.6-sol 上单次 agentic 任务运行超 2 小时，footer 显示上下文已超过压缩阈值但并未触发，直到 API 在 373k tokens 时拒绝请求才被迫处理。
  - **诉求**：用户强烈要求在每个 agent turn 之后检查上下文长度，并自动触发压缩，而不是等到 API 报错。这反映了长任务场景下对会话连续性的核心需求。

- **[Bug] Mac OS 上长会话导致高 CPU 占用** ([#7730](https://github.com/earendil-works/pi/issues/7730))
  - **热度**：11 条评论，8 个 👍。
  - **详情**：在 Mac OS 上运行 Pi 时，CPU 占用在 50-110% 之间波动，内存占用 600-800MB，且与上下文大小或会话长度相关。
  - **诉求**：用户希望提升长会话下的资源使用效率。该问题与 #8029 的输入性能问题共同指向了大规模文本处理时的性能瓶颈。

### 5. Bug 与稳定性

按严重程度排列今日报告的 Bug：

- **严重 - 上下文溢出导致任务中断**：[#6879](https://github.com/earendil-works/pi/issues/6879) 压缩机制失效，导致 API 请求被拒。目前无直接 fix PR，为高优先级。
- **严重 - 终端状态损坏**：[#8080](https://github.com/earendil-works/pi/issues/8080) SIGINT 后终端进入 raw mode，需要 `reset` 恢复。**已有对应 fix PR [#8082](https://github.com/earendil-works/pi/pull/8082) 并已合并**。
- **中等 - 性能退化**： [#8029](https://github.com/earendil-works/pi/issues/8029) 大缓冲区下编辑器移动光标性能极差（7000 行时 1650ms）。**已有对应 fix PR [#8066](https://github.com/earendil-works/pi/pull/8066) 提交，为视觉行添加了缓存**。
- **中等 - 功能异常**：[#8087](https://github.com/earendil-works/pi/issues/8087) 指出 `pi-output-classifier` 已过时，应替换为 `pi-auto-classifier`。
- **中等 - 兼容性问题**：[#8031](https://github.com/earendil-works/pi/issues/8031) `openai-codex` 中途失败重试会导致整个响应重复输出。
- **轻微 - 显示与一致性问题**：包括 [#8060](https://github.com/earendil-works/pi/issues/8060) 流式输出时颜色闪现、[#8079](https://github.com/earendil-works/pi/issues/8079) 大型会话恢复时刷新终端（已有修复 PR）、[#8081](https://github.com/earendil-works/pi/issues/8081) 未知斜杠命令被当作普通消息发送。

### 6. 功能请求与路线图信号

- **为 `openai-completions` 跟踪 Kimi 的 `cached_tokens` 用量** ([#8075](https://github.com/earendil-works/pi/issues/8075))：用户请求精确统计缓存命中的 token 消耗。这是一个明确且低成本的功能改进，很可能被纳入下一版本。
- **在 HTML 导出中渲染 Mermaid 和 LaTex** ([#8041](https://github.com/earendil-works/pi/issues/8041))：用户期望 HTML 导出的 markdown 渲染效果与 TUI 一致。
- **为 Codex 后端处理 `end_turn: false`** ([#7689](https://github.com/earendil-works/pi/issues/7689))：该功能与部分后端提供的 `response.completed` 扩展字段有关，可能需要更深入的协议支持。
- **支持 Anthropic 服务端拒答回退** ([#8017](https://github.com/earendil-works/pi/issues/8017))：面对 Claude 分类器误判时，压缩能通过回退机制成功执行。

### 7. 用户反馈摘要

- **对长会话稳定性不满**：用户 `@alexanderkreidich` 在 #6879 中描述了因压缩失效导致 2 小时任务成果丢失的风险，言辞中透露出明显的挫败感，并呼吁“需要每一个 agent turn 后都进行检查”。
- **性能问题影响核心体验**：用户 `@affanali2k3` 在 #8029 中反馈，在 7000 行文本下按一次上箭头需要 1650ms，严重影响了编辑体验。
- **对终端恢复机制的需求**：用户 `@frankieyep` 在 #8080 和 #8079 中报告了 `SIGINT` 和回放历史导致终端被破坏的问题，这属于基础体验问题，直接影响用户对工具可靠性的信任。
- **对未知命令的困惑成本**：用户 `@frankieyep` 在 #8081 中提到，误输入 `/exit` 会被当作聊天消息发送，造成不必要的模型调用和困惑。

### 8. 待处理积压

- **核心功能缺失 PR 长期未合并**：[#6216](https://github.com/earendil-works/pi/pull/6216) feat: Add Amazon Bedrock Mantle OpenAI Responses provider。此 PR 自 7 月 1 日开启，已开放超过 6 周，仍处于待合并状态。这可能意味着维护者对其有更深入的技术考量，但长期搁置会消耗贡献者热情。
- **性能改进建议与现状冲突**：[#4254](https://github.com/earendil-works/pi/issues/4254) 关于通过共享 `jiti` 实例来加速扩展加载的问题，虽被标记为 `closed-because-bigrefactor` 关闭，但其提出的启动时间问题在今天的 #7739 中再次被提及，说明此痛点依旧存在，值得维护者在后续重构中纳入考量。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-14

---

## 1. 今日速览

过去 24 小时 Temporal 项目保持了较高的开发活跃度：**82 条 PR 更新**，其中 24 条已合并/关闭、58 条待合并，反映了持续且密集的代码交付节奏。Issue 方面有 **10 条更新**，全部处于开放状态（新开/活跃：10，关闭：0），其中 3 条为当日新报告，包含 2 个高严重度问题（工作流 API 永久挂起、版本删除永久失败）。社区侧无新版本发布，但多个 PR 已推进至收尾阶段，特别是 **OpenTelemetry HTTP 追踪**（Nexus 可观测性）、**Worker Callbacks 新变体**以及 **replication 生命周期事件**三条主线。整体来看，项目在可观测性、可靠性工程和 worker 功能扩展方面有明显投入，但存量 Bug 的关闭速度偏慢（今日 0 关闭），值得关注。

---

## 2. 版本发布

今日无新版本发布。可在下期关注上文所述功能主线的合入节点（预计随 v1.32 或 1.33 落地）。

---

## 3. 项目进展

过去 24 小时有 **24 条 PR 被合并或关闭**，以下按主题梳理关键进展：

### 3.1 复制（Replication）可靠性增强 — 已合入
- [#11479 replication: emit source_task_id and source_cluster on passive-side lifecycle events](https://github.com/temporalio/temporal/pull/11479)（已关闭）
  - 在被动侧 `executing` 和 `applied` 生命周期事件中补充 `source_cluster`、`source_shard` 和 `source_task_id`，让运维和调试能追溯复制任务的完整来源链路。
- [#11459 Record what a replication task carried on the sent lifecycle event](https://github.com/temporalio/temporal/pull/11459)（已关闭）
  - 修复 `sent` 事件只记录"任务已发出"、不记录任务载荷的问题，避免后续难以重建复制事件的完整上下文。
- [#11401 Emit handover watermark and shard readiness wide events](https://github.com/temporalio/temporal/pull/11401)（已关闭）
  - 在命名空间 handover 完成路径上补充 watermark 和 shard 就绪事件，为复制切换的协调与监控提供数据基础。

### 3.2 CHASM / 组件更新 — 已合入
- [#11169 [CHASM] Support WithRequestID on UpdateComponent](https://github.com/temporalio/temporal/pull/11169)（已关闭）
  - `UpdateComponent` 现在支持请求级幂等（request ID），通过 API 传入的请求 ID 会被持久化，重复的相同请求 ID 不再重复执行更新逻辑。

### 3.3 OpenTelemetry 追踪（Nexus 可观测性）— 进行中
以下为一组 stacked PR（合并顺序依赖），目标是为 Nexus HTTP 路径引入完整的 OpenTelemetry 追踪能力：
- [#11558 Add OpenTelemetry HTTP instrumentation](https://github.com/temporalio/temporal/pull/11558) — 基础层：可复用的 HTTP client/server OTel 包装器
- [#11559 Trace outbound Nexus HTTP requests](https://github.com/temporalio/temporal/pull/11559) — 出站呼叫注入 trace context
- [#11560 Trace inbound Nexus HTTP requests](https://github.com/temporalio/temporal/pull/11560) — 入站路由级 server span
- [#11561 Annotate Nexus spans](https://github.com/temporalio/temporal/pull/11561) — 补充 namespace、endpoint、service、operation 等 Nexus 语义属性
- [#10739 Annotate worker task spans](https://github.com/temporalio/temporal/pull/10739) — workflow/activity/Nexus worker-task span 的任务级标注

### 3.4 Worker Callbacks 新变体（feature 分支）
- [#11380 Recognize the new `commonpb` Worker callback variant](https://github.com/temporalio/temporal/pull/11380)、[#11520 Populate CallbackInfo.outcome](https://github.com/temporalio/temporal/pull/11520)、[#11566 Make supported callback kinds configurable](https://github.com/temporalio/temporal/pull/11566) — worker 回调新变体持续推进，当前集中在 feature 分支，尚未进入 main。

### 3.5 其他值得关注的合并
- [#11464 Refactor Nexus frontend interceptors](https://github.com/temporalio/temporal/pull/11464) — 重构 Nexus 前端拦截器，不影响对外 API
- [#11565 Preserve schedule-to-close timer bit on passive activity retry](https://github.com/temporalio/temporal/pull/11565) — 修复被动侧 activity 重试时 schedule-to-close timer 位被重置的问题
- [#11554 Only count reader reads that left tasks behind as stuck attempts](https://github.com/temporalio/temporal/pull/11554) — 修复 reader 卡顿检测的误报
- [#11564 [Elasticsearch] datetime 格式统一包含纳秒](https://github.com/temporalio/temporal/pull/11564) — 避免 ES 日期字段比较时出现意外的截断/边界问题

---

## 4. 社区热点

今日讨论热度最高的几个 Issue/PR，反映了用户对可靠性和部署体验的关注：

- [#10841 SignalWithStart hangs forever on an orphaned current-execution pointer（2 条评论）](https://github.com/temporalio/temporal/issues/10841)  
  这是 **6 月 25 日创建、今日仍活跃**的问题：在使用 `SignalWithStartWorkflowExecution` 且存在 orphaned current-execution pointer 时，API 可能永久挂起。该问题直接影响工作流信号/启动这一核心操作，社区用户持续补充讨论，但尚未被认领。

- [#11534 Fairsim partial counter configuration resets unspecified defaults（1 条评论）](https://github.com/temporalio/temporal/issues/11534)  
  新报告的 fair simulation 工具配置 bug。用户指出部分配置（如 `{"CMS":{"W":100}}`）会覆盖未指定的默认值，与 README 文档的预期不符。虽属工具链问题，但影响本地压力测试的准确性。

- [#8490 Scheduled Actions doesn't clear ContinuedFailure on null success payloads（2 条评论、2 👍）](https://github.com/temporalio/temporal/issues/8490)  
  老问题（2025-10 创建），今日依然有活跃讨论。核心痛点：Scheduled Actions 在成功执行但 payload 为 null 时，`ContinuedFailure` 未被清除，导致后续动作持续收到错误状态。已有 2 个 👍，但未分配修复。

- [#11547 A brief `Unavailable` blip resets History queue backoff, causing a sustained retry storm](https://github.com/temporalio/temporal/issues/11547)  
  新报告的高影响稳定性问题：History 集群在系统持久化 QPS 达到上限时，依赖长 backoff 稳定运行；但如果持久化层出现短暂 `Unavailable`，backoff 被重置，会引发持续的 retry storm。评论数当前为 0，但影响面大，建议优先处理。

**热门 PR** 方面，[#11558 Add OpenTelemetry HTTP instrumentation](https://github.com/temporalio/temporal/pull/11558) 及其 stacked PR（#11559-#11561）是一个高关注度的功能组合——Nexus 可观测性一直是一个诉求明确的方向，将 gRPC 之外的 HTTP 路径纳入统一追踪，对排查跨服务调用问题很有价值。

---

## 5. Bug 与稳定性

按严重程度排序（高→低）：

| 级别 | Issue | 描述 | 修复 PR |
|---|---|---|---|
| 🔴 高 | [#10841 SignalWithStart hangs forever on an orphaned current-execution pointer](https://github.com/temporalio/temporal/issues/10841) | 核心 Workflow API 可能永久挂起，不返回、不超时 | 无 |
| 🔴 高 | [#11539 DeleteWorkerDeploymentVersion fails permanently when a version summary outlives its version workflow](https://github.com/temporalio/temporal/issues/11539) | 版本清理永久失败，导致 `maxVersionsIn

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*