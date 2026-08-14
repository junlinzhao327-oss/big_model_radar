# OpenClaw 生态日报 2026-08-15

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-14 22:36 UTC

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

# 个人 AI 助手 / 自主智能体开源生态横向对比分析报告

**日期：** 2026-08-15  
**分析对象：** Hermes Agent、OpenHands SDK、LiteLLM、Temporal、OpenClaw（参照）


## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态正处于 **“高活跃度、强稳定性焦虑、架构探索期”** 。从今日数据看，头部项目均保持每日数百级的 Issue/PR 流（Hermes Agent 达 393/500，LiteLLM 达 86/279），代码产出与社区反馈双旺；但 **Windows 平台回归、会话持久化失败、崩溃恢复损坏数据** 等稳定性问题成为多项目共同痛点，反映出功能高速迭代后进入质量巩固阶段。与此同时，**多租户隔离、跨平台会话共享、可移植插件规范、远程 agent 执行** 等架构级诉求正在社区中积累势能，预示下一代智能体框架将围绕分布式执行、标准化扩展与上下文连续性展开竞争。


## 2. 各项目活跃度对比

| 项目 | Issues（更新/关闭） | PRs（待合并/合并关闭） | Release | 健康度评估 |
|---|---|---|---|---|
| **Hermes Agent** | 393（334/59） | 500（351/149） | 无（v0.20.0） | **中等偏上**：活跃度极高、修复响应快，但 Windows 更新链路与长期积压架构需求值得警惕 |
| **OpenHands SDK** | 31（20/11） | 17（11/6） | 无 | **良好**：High 级 bug 当天报告当天出 fix PR，响应迅速；插件规范子任务稳步推进 |
| **LiteLLM** | 86（73/13） | 279（176/103） | 无 | **中上**：迭代强度高、稳定性 Sprint 已启动，但 Issue 关闭率仅 15%，响应存在积压 |
| **Temporal** | 3（3/0） | 75（62/13） | 无 | **良好**：PR 合并流稳定，但今日 Issue 零关闭，响应速度略慢；Nexus 可靠性方向投入明确 |
| **OpenClaw** | 数据缺失 | 数据缺失 | 数据缺失 | 数据缺失 |

> 注：OpenClaw 作为核心参照，但摘要中未提供具体数据，无法纳入定量对比。


## 3. OpenClaw 在生态中的定位

由于本次未提供 OpenClaw 的具体仓库数据，以下基于社区公开认知与角色定位进行推演：

- **生态锚点地位**：OpenClaw 作为个人 AI 助手的核心参照项目，扮演的是“基线标准”角色——社区讨论（如 Hermes Agent 用户诉求）中频繁出现 “OpenClaw 已有功能” 或 “与 OpenClaw 对齐” 的隐含对标，说明它定义了个人助手的基础能力边界。
- **技术路线差异**：从生态共性看，Hermes Agent 侧重多平台桥接（微信/QQ/Telegram/Discord）与桌面端体验，OpenHands SDK 强化安全内核（AST 级 shell 检测）与插件规范，LiteLLM 深耕模型网关与成本观测，Temporal 则解决分布式工作流可靠性。**OpenClaw 的差异化大概率在于“开箱即用的完整个人助手闭环”**——集对话、工具调用、记忆、多通道接入于一体，更接近端用户产品而非开发框架。
- **社区规模与生态位**：鉴于 Hermes Agent 日更 393 条 Issues、OpenHands 聚焦开发者基础设施，OpenClaw 若处于中心参照位，其社区规模应与 Hermes Agent 同级（日更数百条），但更偏向**终端用户反馈驱动**，而非开发者工具链驱动。


## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **稳定性与回归控制** | Hermes Agent（Windows gateway 静默死亡 #83683/#84185）、OpenHands SDK（崩溃恢复损坏会话 #4487）、LiteLLM（Prisma 连接 503 #36428）、Temporal（request-timeout 畸形 header #11569） | 多项目同时出现“升级后回归”“静默失败无日志”“数据损坏”类问题，反映快速迭代期需要更强回归测试与可观测性 |
| **多租户 / 隔离性** | Hermes Agent（#34352，内存 hook 绕过租户隔离）、OpenHands SDK（profile 激活不一致 #4494）、LiteLLM（跨账户 Bedrock 签名 #36449） | 从单用户单进程走向多用户、多 profile、多云账户隔离，权限边界与密钥管理成为核心挑战 |
| **会话/上下文连续性** | Hermes Agent（压缩续会话 #82001、跨进程租约 #67442、跨平台共享 #4335）、OpenHands SDK（崩溃恢复 tool_result 孤儿 #4487、condensation 残留 #4498）、Temporal（Nexus 操作 auto-close #11577） | 与会话压缩、持久化、跨进程/跨平台续接相关的错误集中爆发，说明“记忆连续性”是智能体落地的关键痛点 |
| **可扩展插件体系** | OpenHands SDK（Agent Plugins 规范 #4405、命名空间映射 #4496）、Hermes Agent（外挂记忆 provider #85622、远程 agent #18715）、LiteLLM（模型路由元数据 #4421） | 社区对标准化插件/Provider/工具扩展接口的诉求高度一致，MCP 协议影响下，项目开始构建自身插件层级 |
| **协议合规与互操作** | Temporal（Nexus request-timeout #11569）、LiteLLM（AWS 跨账户签名 #36449）、Hermes Agent（Discord REST v10 适配 #86419） | 对外部协议/API 的适配深度（包括错误语义、单位格式、认证传递）正在成为质量分水岭 |


## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|---|---|---|---|
| **Hermes Agent** | 多平台消息桥接（IM/桌面/Discord）、桌面应用、本地工具执行 | 个人用户/高级玩家，追求“一个 agent 接入所有聊天渠道” | 桥接网关 + 桌面应用 + 动态配置，重渠道适配层，生态位最接近终端用户 |
| **OpenHands SDK** | 智能体开发框架、安全执行（AST 级 shell 检测）、可移植插件规范 | 开发者/ISV，构建自主 agent 产品 | 核心引擎 + 插件规范（dev.openhands 命名空间）+ MCP 兼容，重安全与可扩展性 |
| **LiteLLM** | 统一 LLM 网关、路由/成本观测/多云适配 | 平台工程团队、SRE，管理多模型接入 | 代理网关架构，100+ Provider 适配，重心在“模型连接与观测”，非 agent 自身 |
| **Temporal** | 分布式工作流编排、Nexus 协议、持久化执行 | 后端开发者，构建可靠业务工作流 | 持久化执行引擎 + Worker 模型，Durable Execution，与 agent 无直接绑定但可承载 agent 状态机 |
| **OpenClaw** | 个人 AI 助手一体化（参照定位） | 端用户/轻度开发者，追求即插即用的全功能助手 | 应为核心单体 + 可插拔通道，强调“零配置可用”与本地优先 |


## 6. 社区热度与成熟度

**第一梯队 — 快速迭代期（功能扩展与稳定性並行）：**
- **Hermes Agent**：日更 393 Issues / 500 PRs，合并 149 条，处于典型的高吞吐迭代阶段。社区反馈旺盛且激烈，但存量问题（Windows 回归、架构级诉求 fork 自维护）提示需要投入治理。
- **LiteLLM**：日更 279 PRs / 86 Issues，合并 103 条，迭代速度同属第一梯队。但其 Issue 关闭率仅 15%，说明社区大量反馈正在积累，官方已启动 Stability Sprint（#30484）应对。

**第二梯队 — 质量巩固期（方向明确，响应迅捷）：**
- **OpenHands SDK**：日更 31 Issues / 17 PRs，体量小于第一梯队但**响应速度惊人**——High 级 bug（#4494/#4487/#4493）均当天收到修复 PR，深度重构（AST 安全检测）能稳定落地。处于“小而精”的质量巩固阶段。
- **Temporal**：日更 3 Issues / 75 PRs，呈现**PR 驱动、Issue 沉默**的典型“平台型项目”特征。13 条合并全部集中在工程团队自有路线（Nexus、测试设施），社区参与度深度低但可靠性投入明确。


## 7. 值得关注的趋势信号

### 信号一：“稳定性回归”已成为智能体生态的最大公敌
Hermes Agent 的 Windows gateway 静默死亡、OpenHands SDK 的崩溃恢复损坏会话、LiteLLM 的 Prisma 503、Temporal 的畸形 header——四个项目同日出现稳定性 Bug，且多与**升级后回归**或**静默失败**相关。**对开发者的启示：** 智能体系统涉及长生命周期状态（会话、记忆、连接），引入任何变更时需配套**回归注入工具与优雅降级策略**；监控不仅要覆盖“进程存活”，更要覆盖“会话连续性与数据完整性”。

### 信号二：“跨实例/跨平台会话连续性”是下一代刚需
Hermes Agent 的远程 agent（#18715，26 👍）与跨平台共享（#4335）、OpenHands 的插件命名空间、Temporal 的持久化执行，共同指向一个方向：**agent 不再绑定单个进程或单台设备**。未来的个人助手必须在“用户的多台设备、多个平台、多个进程”之间漫游，同时保持记忆与上下文一致。**对开发者的启示：** 设计 agent 状态管理时，应优先考虑 **DB 级持久化与租约机制**而非内存态，否则跨进程/跨设备场景将无解。

### 信号三：安全边界正在从“执行检测”升级到“数据隔离与权限传递”
OpenHands SDK 将 shell 检测从 regex 升级为 AST 解析（#2721/#3944）；Hermes Agent 出现多 profile secrets 泄漏（#82936）、WhatsApp 文件权限收紧（#86304）、终端配置桥 fail-closed（#61882）；LiteLLM 修复跨账户签名（#36449）。安全议题不再是单一工具链问题，而是**贯穿配置、执行、存储、网络传输的全链路**。**对开发者的启示：** 智能体的权限模型应默认最小化，并在异常时 **fail-closed**（如在容器中降级运行）而非静默降权。

### 信号四：插件规范标准化进入实质落地阶段
OpenHands SDK 的 Agent Plugins 1.0 持续推进（命名空间映射 dev.openhands），LiteLLM 的模型路由元数据、Hermes Agent 的 Discord 适配均显示出对 **“生态可插拔”** 的共识。MCP 协议之外，各项目开始定义自己的插件分层与边界。**对开发者的启示：** 若在构建 agent 产品，应尽早抽象出“核心引擎 + Provider/Plugin 接口”，避免后续功能扩展时陷入硬编码适配（如 Hermes Agent 的 WhatsApp/Discord 适配器）。

### 信号五：社区“用脚投票”现象值得警惕
Hermes Agent 的多租户 issue（#34352）出现“作者称已生产运行修复数月，呼吁合入核心”的评论，表明核心项目对架构级 PR 的响应速度慢于社区需求时，**会出现 fork 自维护与重复造轮子的生态分裂风险**。**对项目维护者的启示：** 除了合并与关闭 PR，需要建立对高赞长期 Issue 的“路线图回应机制”，否则社区热度会转化为对竞品（如 OpenClaw）的迁移。


## 结语

2026 年 8 月中旬的智能体生态呈现典型的“**二次曲线拐点**”特征：基础设施型项目（Temporal、LiteLLM）在打磨可靠性与协议互操作，应用型项目（Hermes Agent、OpenHands SDK）在快速迭代中艰难维持稳定，而社区已经开始提出“下一个时代的架构问题”（远程执行、跨平台记忆、可移植插件）。对于技术决策者而言，选择技术栈时应重点考察项目的**回归测试完整度、插件抽象成熟度、以及状态管理的持久化程度**——这将决定智能体应用能否从 demo 走向生产。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-15

---

## 1. 今日速览

过去 24 小时 Hermes Agent 仓库活跃度处于高位：共更新 **393 条 Issues**（新开/活跃 334，关闭 59）与 **500 条 PR**（待合并 351，合并/关闭 149），无新版本发布。社区讨论集中在 **Windows 平台 gateway 静默死亡/重启回归**（#83683、#84185）、**会话压缩与持久化失败**（#82001）、**多租户隔离**（#34352）三大方向，且均有对应修复 PR 在途（#86409、#86410、#86414 等）。安全类修复（终端配置桥 fail-closed、WhatsApp 桥接文件权限）与桌面端体验优化（首次运行直达聊天、pt-BR 本地化）是今日 PR 的主要构成，整体项目健康度**中等偏上**——活跃度高、修复响应快，但 Windows 更新链路稳定性与长期积压功能（远程 agent、跨平台会话共享）仍值得关注。

---

## 2. 版本发布

今日无新版本发布（最新 Release 为空）。当前版本停留在 **v0.20.0**（2026.8.3）。多个 Windows 相关 issue 指向 v0.20.0 的回归问题（见第 5 节），预计下一个补丁版本将聚焦更新链路稳定性。

---

## 3. 项目进展

今日虽无正式 Release，但 PR 合并/关闭量达 **149 条**，开发管线保持高吞吐。从最新 PR 列表看，以下方向取得了实质性推进：

### 3.1 会话持久化与压缩修复
- **[#86409 fix(agent): adopt live compression continuation when flushing to a closed session](https://github.com/NousResearch/hermes-agent/pull/86409)** — 解决 #82001 中 agent 在会话被压缩关闭后 flush 失败、误报“磁盘满”的问题。该 PR 与 #82001 形成直接对应，是今日最重要的稳定性修复。
- **[#86267 fix(compression): reframe preserved todos as planning context](https://github.com/NousResearch/hermes-agent/pull/86267)** — 调整压缩时 todos 的处理方式，以零额外开销修复 #84718 方向的问题。

### 3.2 桌面端与 Gateway 生命周期
- **[#86410 fix(gateway): stop treating desktop-session INVOCATION_ID as gateway supervision](https://github.com/NousResearch/hermes-agent/pull/86410)** — 修复手动在桌面终端运行的 gateway 被误判为服务托管、`/restart` 后永久死亡的问题。
- **[#86414 fix(desktop): the main agent's model pick persists as the profile default](https://github.com/NousResearch/hermes-agent/pull/86414)** — 修复桌面端主 agent 模型选择在切换后不保留的问题。
- **[#86415 Desktop first run opens straight into a working chat](https://github.com/NousResearch/hermes-agent/pull/86415)** — 新安装用户跳过 provider 选择墙，直接进入可聊天界面。

### 3.3 安全修复
- **[#61882 fix(security): fail closed when terminal config bridge is unavailable](https://github.com/NousResearch/hermes-agent/pull/61882)** — 冷启动时若配置桥未就绪，终端默认在 Docker 容器内运行而非宿主机，消除静默逃逸风险。
- **[#86304 fix(whatsapp): enforce owner-only bridge files](https://github.com/NousResearch/hermes-agent/pull/86304)** — WhatsApp 桥接文件权限收紧至 0600/0077，防止多用户泄露。

### 3.4 工具能力增强
- **[#86406 fix(terminal): archive oversized output before the head/tail cap drops it](https://github.com/NousResearch/hermes-agent/pull/86406)** — 终端工具超限输出先归档再截断，符合 `tool_result_storage.py` 的“保留大输出”契约。
- **[#86419 feat(discord): outbound reaction actions for REST v10](https://github.com/NousResearch/hermes-agent/pull/86419)**、**[#86324 feat(discord): typed outbound embed builder for REST v10](https://github.com/NousResearch/hermes-agent/pull/86324)** — Discord Omniscience 系列持续落地，补齐 reaction 与 embed 能力。
- **[#86342 feat(computer-use): user-facing authorization for cua-driver browser attachment](https://github.com/NousResearch/hermes-agent/pull/86342)** — 浏览器自动化授权机制，经真实 cua-driver 0.19.3 验证。

整体来看，项目今日围绕 **稳定性修补（压缩/持久化/gateway 生命周期）** 与 **安全加固** 双主线推进，同时 Discord/桌面端功能迭代未停歇。

---

## 4. 社区热点

### 4.1 讨论最激烈
| Issue | 标题 | 评论数 | 点赞 | 核心诉求 |
|---|---|---|---|---|
| [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) | skills-index-watchdog 索引过期 | 30 | 0 | 自动化探针报警：技能索引 29.8h 未更新（限制 26h），影响文档站技能发现 |
| [#34352](https://github.com/NousResearch/hermes-agent/issues/34352) | 解决多租户 Hermes 问题 | 30 | 3 | 内存操作绕过 hook 系统导致租户隔离无法实现；作者称已生产运行修复数月，呼吁合入核心 |
| [#83683](https://github.com/NousResearch/hermes-agent/issues/83683) | 桌面重启收割 gateway 且不重启（回归） | 25 | 0 | Windows 桌面应用每次重启都杀死 gateway，微信/QQ/Telegram 静默直至手动重启 |
| [#82001](https://github.com/NousResearch/hermes-agent/issues/82001) | Agent flush 不采用压缩后的续会话 | 17 | 0 | 压缩关闭会话时客户端仍在写入，turn 失败并误报“磁盘满”，根因是会话身份交接缺口 |
| [#67442](https://github.com/NousResearch/hermes-agent/issues/67442) | 跨进程 turn 序列化需 DB 级租约 | 16 | 0 | CLI 续会话与 gateway 分属不同进程时，缺少数据库级租约，存在边缘并发问题 |

### 4.2 高赞功能需求
- **[#18715 支持远程 Hermes agent + 本地工具执行](https://github.com/NousResearch/hermes-agent/issues/18715)** — **👍 26**，为今日最高赞 issue。用户希望 Machine A 作为客户端，Machine B 作为远程 agent 实例（保留技能/记忆/会话/模型配置），但工具在本地执行。这一需求指向**分布式 agent 架构**，可能是未来路线图的重要方向。
- **[#4335 跨平台会话上下文共享（CLI ↔ Telegram）](https://github.com/NousResearch/hermes-agent/issues/4335)** — 👍 3，多平台会话孤岛问题，用户希望 CLI 与 Telegram 能共享上下文。
- **[#80424 Grok/xAI 功能对齐活动](https://github.com/NousResearch/hermes-agent/issues/80424)** — 10 条评论，社区在推动 Hermes 与 xAI 平台功能对齐（推理、流式、语音、图像等）。

### 4.3 诉求分析
今日热点呈现清晰的“**稳定性焦虑**”：Windows 用户连续遭遇 gateway 被杀、更新后静默死亡等回归（#83683、#84185），引发大量讨论；而**架构级诉求**（多租户、远程 agent）虽点赞高但长期未决，社区开始有人绕过核心 fork 自维护，这值得维护者警惕。

---

## 5. Bug 与稳定性

### P1（严重，影响核心功能）
| Issue | 问题 | 修复 PR |
|---|---|---|
| [#83683](https://github.com/NousResearch/hermes-agent/issues/83683) | **Windows 桌面重启杀死 gateway 不再拉起（回归）** — 微信/QQ/Telegram 全部静默 | 暂无直接 PR，[#86410](https://github.com/NousResearch/hermes-agent/pull/86410) 间接相关（修复 gateway 重启被误判） |
| [#84185](https://github.com/NousResearch/hermes-agent/issues/84185) | **Windows gateway 在 hermes update 后静默死亡** — 无日志、无 PID 文件、无退出记录，离线至手动重启 | 暂无 |
| [#82001](https://github.com/NousResearch/hermes-agent/issues/82001) | **Agent flush 不采用压缩后续会话** — 误报“磁盘满”，实际磁盘健康 | ✅ **[#86409](https://github.com/NousResearch/hermes-agent/pull/86409) 已提交修复** |
| [#72924](https://github.com/NousResearch/hermes-agent/issues/72924) | **hermes update 运行时重建静默丢弃声明 extras**（Telegram、语音等依赖缺失） | 暂无 |

### P2（中等严重）
| Issue | 问题 |
|---|---|
| [#82936](https://github.com/NousResearch/hermes-agent/issues/82936) | **多配置文件 secrets 泄漏** — 默认 profile 的 secrets 在 secondary profile 的 terminal/Kanban 子进程中可见（安全边界） |
| [#83846](https://github.com/NousResearch/hermes-agent/issues/83846) | **ZIP 回退删除桌面应用且不重建** — 后续更新报 Already up to date，应用消失 |
| [#71047](https://github.com/NousResearch/hermes-agent/issues/71047) | **config set 重复创建顶级键** + Telegram 流式回复重复投递 |
| [#83390](https://github.com/NousResearch/hermes-agent/issues/83390) | **DeepSeek 标题生成 HTTP 400** — response_format 类型不可用 |
| [#83680](https://github.com/NousResearch/hermes-agent/issues/83680) | **Termux 上 cryptography 50.0.0 Rust 扩展无法解析 PyLong_Type** — 升级回归 |

### P3（轻微/边缘）
| Issue | 问题 |
|---|---|
| [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) | 技能索引自动探针报警，索引 29.8h 未刷新 |
| [#77253](https://github.com/NousResearch/hermes-agent/issues/77253) | 桌面端无语言标记的代码块被误判为 prose 不渲染 |
| [#85622](https://github.com/NousResearch/hermes-agent/issues/85622) | 外部记忆 provider 抑制内置 MEMORY.md/USER.md 注入，违背“additive”契约 |
| [#58705](https://github.com/NousResearch/hermes-agent/issues/58705) | mem0 OSS + Qdrant 锁冲突，agent 工具调用失败 |
| [#30230](https://

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报（2026-08-15）

## 1. 今日速览

过去 24 小时项目保持高度活跃：31 条 Issue 更新（其中 20 条新开或活跃、11 条关闭），17 条 PR 更新（11 条待合并、6 条已合并或关闭）。值得关注的是，多个 high 优先级 Bug（#4494、#4487、#4493）在一天内集中报告并快速获得修复 PR，体现出维护团队对稳定性问题的快速响应。同时，Agent Plugins 可移植插件规范持续推进（#4496 新 PR 落地命名空间映射），LLM 路由元数据与聚合器上下文上限等后端能力也有实质进展。整体项目活跃度高、健康度良好。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日合并/关闭的 PR 主要推进了以下方向：

- **安全加固落地**：[PR #3944](https://github.com/OpenHands/software-agent-sdk/pull/3944) 完成并关闭，将 shell 命令检测从 regex 升级为 AST 解析，实现 #2721 Phase 2b，修复了引号/路径/嵌套三种绕过方式。
- **崩溃恢复修复**：[PR #4489](https://github.com/OpenHands/software-agent-sdk/pull/4489) 关闭，使崩溃恢复错误正确关联到被中断的 action 分支，配合 [#4488](https://github.com/OpenHands/software-agent-sdk/pull/4488) 修复 #4487 的会话损坏问题。
- **LLM 路由能力**：[PR #4423](https://github.com/OpenHands/software-agent-sdk/pull/4423) 关闭，解决路由 providers（如 OpenRouter）的 provider 特定运行时元数据解析，对应 Issue #4421/#4428。
- **上下文管理**：[PR #4461](https://github.com/OpenHands/software-agent-sdk/pull/4461) 关闭，condenser 的 token 上限现在会由 agent 上下文窗口封顶，避免超出模型限制。
- **CI 与测试稳定性**：[PR #4486](https://github.com/OpenHands/software-agent-sdk/pull/4486)（补充 `synchronize` 触发条件）、[PR #4290](https://github.com/OpenHands/software-agent-sdk/pull/4290)（Windows Ctrl-C 测试稳定化）均关闭。

## 4. 社区热点

- [#976 Daily Examples Run Results](https://github.com/OpenHands/software-agent-sdk/issues/976)（63 评论）：CI 自动化的每日示例运行结果占位 issue，虽非人工讨论，但持续被更新，说明示例回归监控稳定运行。
- [#1440 Plugin 1.0 Definition](https://github.com/OpenHands/software-agent-sdk/issues/1440)（26 评论，已关闭）：关于 SDK 插件基础能力范围的定义讨论，涉及 MCP config 等未来方向的取舍，体现了社区对插件标准化的高度关注。
- [#1522 Microagents for uv and deno](https://github.com/OpenHands/software-agent-sdk/issues/1522)（21 评论，1 👍）：用户希望用 microagents 适配 `uv`/`deno` 等现代工具链，反映社区对开发工具链时效性的需求。
- [#2721 tree-sitter-bash 安全分析提案](https://github.com/OpenHands/software-agent-sdk/issues/2721)（15 评论，1 👍）：从 regex 升级到 AST 解析的安全重构，目前已进入实施阶段（PR #3944），说明该方向获认可且得到落地验证。

**信号**：社区对可扩展插件体系（#1440、#4405）和现代工具链适配（#1522）有持续诉求；安全模块深度改造（#2721）在获得实际进展后也保持了较高的关注度。

## 5. Bug 与稳定性

按严重程度排列：

- **High — 默认 LLM 忽略激活 profile**（[#4494](https://github.com/OpenHands/software-agent-sdk/issues/4494)）：agent-server 报告的活跃 profile 与实际 `agent_settings.llm` 不一致，自动任务可能以陈旧 keyless 模型启动。→ Fix PR [#4497](https://github.com/OpenHands/software-agent-sdk/pull/4497) 已提交。
- **High — 崩溃恢复打断工具调用并损坏会话**（[#4487](https://github.com/OpenHands/software-agent-sdk/issues/4487)）：在三个真实 Agent Canvas 会话中复现，重启后孤儿 tool_result 永久破坏后续轮次。→ Fix PR [#4488](https://github.com/OpenHands/software-agent-sdk/pull/4488) 与 [#4489](https://github.com/OpenHands/software-agent-sdk/pull/4489) 已提交。
- **High — rootless Podman 下 MCP 自连接 405 错误**（[#4493](https://github.com/OpenHands/software-agent-sdk/issues/4493)）：阻断所有对话，升级到 `latest`（SDK v1.36.0）仍复现。→ 尚未见 fix PR。
- **Medium — 增量视图路径跳过 enforce_properties**（[#4498](https://github.com/OpenHands/software-agent-sdk/issues/4498)）：condensation 后可能残留孤立的 tool_result/tool_uses 并被发送给 LLM。→ Fix PR [#4499](https://github.com/OpenHands/software-agent-sdk/pull/4499) 已提交。
- **Medium — DeepSeek prompt cache 未计入遥测**（[#4491](https://github.com/OpenHands/software-agent-sdk/issues/4491)）：`prompt_cache_hit_tokens` 等字段未被正确解析记录。→ Fix PR [#4490](https://github.com/OpenHands/software-agent-sdk/pull/4490) 已提交。
- **长期未修复 — agent-server 对话卡死**（[#3842](https://github.com/OpenHands/software-agent-sdk/issues/3842)，6 月 22 日创建）：`execution_status=idle` 但 `/run` 返回 409，每次新用户消息都无法触发运行，只能重启进程。尚未见修复。

## 6. 功能请求与路线图信号

- **Agent Plugins 规范实施**（[#4405](https://github.com/OpenHands/software-agent-sdk/issues/4405)）是当前最大功能方向，今日系列子任务推进明显：
  - [#4452 客户端扩展命名空间映射](https://github.com/OpenHands/software-agent-sdk/issues/4452) → 新 PR [#4496](https://github.com/OpenHands/software-agent-sdk/pull/4496) 落地 `dev.openhands` 命名空间；
  - [#4453 路径包含验证与故障边界](https://github.com/OpenHands/software-agent-sdk/issues/4453)、[#4451 mcp.json loader](https://github.com/OpenHands/software-agent-sdk/issues/4451) 与 [#

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-15


## 1. 今日速览

过去 24 小时，LiteLLM 保持高强度迭代节奏：**86 条 Issue 更新**（73 条新开/活跃，13 条关闭），**279 条 PR 更新**（176 条待合并，103 条已合并/关闭），**无新版本发布**。PR 合并率约 37%，Issue 关闭率约 15%，代码产出旺盛但社区问题响应速度存在一定积压。值得关注的是，官方在本周发起了 **Stability Sprint 路线图（#30484）** 并将稳定性提升为最高优先级，已有多项基础设施稳定性相关 PR（Prisma 连接恢复、AWS 跨账户签名修复）被合入。社区侧最强烈的单一诉求仍是 **Dark Mode（#10177）**——63 条评论、71 个 👍、持续 477 天未闭环。


## 2. 版本发布

无。


## 3. 项目进展

今日合入/关闭的 PR 与 Issue 集中体现了三个方向：**稳定性补强、多云集成修复、成本计算精度提升**。

### 稳定性

- **[#36428] fix(proxy): force prisma recreate on postgres cached-plan error** — 已合并。修复 Postgres 缓存计划失效后数据库连接未重建、导致认证接口持续 503 的问题。对生产环境 Prisma 依赖的部署有直接帮助。
  https://github.com/BerriAI/litellm/pull/36428

### 多云集成

- **[#36449] fix(bedrock): forward litellm_params AWS auth to batch create signing** — 已合并。修复跨账户 Bedrock 批量任务因签名时丢失部署级 AWS 认证信息而报 "Cross-account pass role is not allowed" 的问题。
  https://github.com/BerriAI/litellm/pull/36449

### 成本精度与 UI

- **[#36914] fix(transcription): stop a zero output rate from zeroing transcription cost** —

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-15

## 1. 今日速览

过去 24 小时 Temporal 项目保持高活跃度：共 75 条 PR 更新，其中 13 条已合并/关闭，合并流稳定；3 条新 Issue 均为 bug 报告，暂无关闭。开发重点集中在 Nexus 协议可靠性、Worker-variant callbacks 功能实现，以及测试基础设施的 canonical reporting pipeline 重构。无新版本发布。整体健康度良好，但 Issue 侧响应速度略慢于 PR 侧。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日有 13 条 PR 合并/关闭，但由于未披露具体清单，以下从活跃 PR 判断项目主要推进方向：

- **Nexus 可靠性提升**：多项 PR 围绕 Nexus 展开，包括出站 HTTP 请求链路追踪（[#11559](https://github.com/temporalio/temporal/pull/11559)）、HTTP/2 keepalive 启用（[#11581](https://github.com/temporalio/temporal/pull/11581)）、Elasticsearch datetime 格式统一（[#11564](https://github.com/temporalio/temporal/pull/11564)），以及 operations auto-close policy 原型（[#11577](https://github.com/temporalio/temporal/pull/11577)）。
- **Worker-variant callbacks**：实际实现 PR（[#11589](https://github.com/temporalio/temporal/pull/11589)）与 CHASM Callback 组件更新（[#11456](https://github.com/temporalio/temporal/pull/11456)）已在集成中，预计将引入新的回调类型，扩展 Nexus 之外的工作流触发能力。
- **测试基础设施重构**：一系列 stacked PR（[#11513](https://github.com/temporalio/temporal/pull/11513) 至 [#11518](https://github.com/temporalio/temporal/pull/11518) 等）正在将测试运行器的结果记录、诊断解析、JUnit 渲染统一到 canonical attempt 模型，旨在提升测试报告的准确性和可维护性。12 条 PR 构成完整链路，反映项目在长期稳定性工具上的投入。

## 4. 社区热点

今日讨论热度普遍不高，唯一有评论的 Issue 为：

- **Issue [#11569](https://github.com/temporalio/temporal/issues/11569)** — Nexus 服务器可能发送畸形 `request-timeout` header（负值及非法单位）。该问题由维护者 @mjameswh 提出，1 条评论，关注协议合规性和互操作性。

在其他活跃 PR 中，以下可能获得较高关注：

- **[#11589](https://github.com/temporalio/temporal/pull/11589)** — Worker-variant callbacks，标记为“THIS IS IT!”，功能实现完整，但属于 stacked PR，需合并入 `feature/worker-callbacks` 分支。
- **[#11564](https://github.com/temporalio/temporal/pull/11564)** — ES datetime 格式调整，对使用 Elasticsearch 的部署有行为影响，值得用户关注。

## 5. Bug 与稳定性

今日 3 条新 Issue 均为 bug 报告，按严重程度排序：

| 严重程度 | Issue | 描述 | 状态 |
|---------|-------|------|------|
| 中高 | [#11569](https://github.com/temporalio/temporal/issues/11569) | Nexus 服务器可能生成不符合自身语法规则的 `request-timeout` header（包含负值及非法单位），可能导致与严格客户端的互操作失败 | 1 条评论，暂无 fix PR |
| 中 | [#11571](https://github.com/temporalio/temporal/issues/11571) | `ProcessOutgoingSearchAttributes` 将持久化限流导致的 `ResourceExhausted` 扁平化为 `Unavailable`，掩盖真实错误类型，影响客户端重试决策和监控 | 无评论，暂无 fix PR |
| 中低 | [#11586](https://github.com/temporalio/temporal/issues/11586) | `tdbg dlq` 命令不支持 archival DLQ（task category 5），导致运维人员无法对归档任务进行 `list`/`merge`/`purge` 操作 | 无评论，暂无 fix PR |

目前均无已关联的修复 PR，建议维护者确认优先级并分配。

## 6. 功能请求与路线图信号

- **Worker-variant callbacks**（[#11589](https://github.com/temporalio/temporal/pull/11589) / [#11456](https://github.com/temporalio/temporal/pull/11456)）：实现趋于完整，预期在功能分支完成合入后进入主线版本。
- **Nexus operation auto-close policy**（[#11577](https://github.com/temporalio/temporal/pull/11577)）：原型阶段，若落地将为 Nexus 操作增加自动关闭策略，减少长时间挂起的 operations。
- **测试基础设施 canonical pipeline**（[#11515](https://github.com/temporalio/temporal/pull/11515) / [#11517](https://github.com/temporalio/temporal/pull/11517) 等）：重构完成后有望提升 flaky test 报告质量、为 bisecting 提供更准确数据，属于 `reliability-2026` 年度计划的一部分，预计持续集成到后续版本。

## 7. 用户反馈摘要

- **协议一致性诉求**（[#11569](https://github.com/temporalio/temporal/issues/11569)）：提交者期望服务器发出的 `request-timeout` header 严格遵守 Nexus 语法（仅 `ms`/`s`/`m` 单位，无符号），避免因非法格式导致严格客户端拒绝或行为异常。这表明社区对协议互操作性的重视。
- **错误分类准确性**（[#11571](https://github.com/temporalio/temporal/issues/11571)）：用户指出持久化限流错误应保留为 `ResourceExhausted` 而不是转换为 `Unavailable`，以便客户端采取正确的退避策略。反映运维监控与客户端行为对错误语义的敏感依赖。
- **运维工具完整性**（[#11586](https://github.com/temporalio/temporal/issues/11586)）：`tdbg` 是运维人员常用的 DLQ 工具，不支持 archival 类别影响了他们对归档任务的故障恢复能力。存在清晰的使用场景。

## 8. 待处理积压

- **PR [#11033](https://github.com/temporalio/temporal/pull/11033)** — 创建于 2026-07-13，已超一个月仍未合并。它处于测试运行器结果返回的依赖链底部，建议确认是否有阻塞或计划合并时间。
- **测试基础设施依赖链**（[#11487](https://github.com/temporalio/temporal/pull/11487) / [#11488](https://github.com/temporalio/temporal/pull/11488) / [#11512](https://github.com/temporalio/temporal/pull/11512) 至 [#11518](https://github.com/temporalio/temporal/pull/11518) 共 8 条 PR）：形成密集的 stacked 依赖，需维护者关注合并顺序，避免长期停留在 open 状态导致分支漂移。
- **Issues [#11571](https://github.com/temporalio/temporal/issues/11571) 与 [#11586](https://github.com/temporalio/temporal/issues/11586)**：无评论、无 fix PR，建议维护者迅速确认严重性并给出回应，避免积压。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*