# OpenClaw 生态日报 2026-09-01

> Issues: 448 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-01 01:19 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-09-01

## 1. 今日速览

过去 24 小时 OpenClaw 仓库保持极高活跃度：**448 条 Issue 更新**（新开/活跃 212，关闭 236）与 **500 条 PR 更新**（待合并 242，合并/关闭 258），并发布 **v2026.8.1 稳定版**。社区关注焦点明显向**稳定性与升级迁移**倾斜：多个用户报告从 2026.7.x 升级到 2026.8.1 后 Gateway 无法启动、`doctor --fix` 陷入循环、迁移误删/隔离有效配置等问题，同时内存泄漏、消息丢失、子进程泄漏等长期问题仍在发酵。项目整体处于**高迭代、高反馈、高修复压力**的状态——功能推进与缺陷修复并行，但升级体验与生产稳定性是当前最大挑战。

## 2. 版本发布

### [v2026.8.1](https://github.com/openclaw/openclaw/releases) — OpenClaw 2026.8.1（稳定版）

- [发布说明](https://docs.openclaw.ai/releases/2026.8.1)
- 官方更新提示：若自动更新失败，可使用本地编码工具链（local coding harness）协助完成更新、诊断迁移错误并验证 Gateway 正常启动；更新前务必备份配置与状态数据。

**已知迁移与兼容性问题（社区反馈汇总）：**

- **Gateway 启动失败 / crash-loop**：[#133813](https://github.com/openclaw/openclaw/issues/133813)（macOS LaunchAgent 升级后启动 fail-close，`doctor --fix` 被 `ExecApprovalsMigrationRequiredError` 阻塞）；[#133984](https://github.com/openclaw/openclaw/issues/133984)（2026.7.1-2 → 2026.8.1 后启动与 `doctor --fix` 均跳过 config-key 迁移，需约十余步手动修复）。
- **`doctor --fix` 自身缺陷**：[#133999](https://github.com/openclaw/openclaw/issues/133999)（提示“Legacy exec approvals exist… Run `openclaw doctor --fix`”，即 fix 命令要求先运行自身）；[#134445](https://github.com/openclaw/openclaw/issues/134445)（零字节 workspace attestation 文件导致迁移卡死）。
- **数据迁移误伤**：[#133347](https://github.com/openclaw/openclaw/issues/133347)（cron 迁移将有效任务隔离为 `invalid-schedule` 并静默丢弃活跃清单）；[#133478](https://github.com/openclaw/openclaw/issues/133478)（自动转录迁移因缺少 agent 数据库维护权限而拒绝迁移）；[#119884](https://github.com/openclaw/openclaw/issues/119884)（已关闭，迁移后未执行 ANALYZE，导致会话操作慢至 15s、事件循环饥饿 30–57s）。

## 3. 项目进展

今日合并/关闭的 PR 中，以下方向取得实质推进：

**稳定性与性能修复**

- [PR #134554](https://github.com/openclaw/openclaw/pull/134554)（已关闭）：降低 Gateway 会话查找/清理期间的内存占用，元数据读取不再加载保存的 prompt 快照与大型工具结果，缓解多 GB 级峰值内存问题。
- [PR #134236](https://github.com/openclaw/openclaw/pull/134236)（已关闭，P0）：修复 shell 安装器 `--silent` 覆盖 `--loglevel error` 导致失败日志为空、EEXIST/ENOTEMPTY 恢复不可见的问题。
- [PR #130993](https://github.com/openclaw/openclaw/pull/130993)（已关闭）：修复 Responses 长会话压缩管线中的 6 个缺陷，包括上下文边界丢失导致过早压缩、多状态回放估算错误等。

**功能与 UI**

- [PR #128995](https://github.com/openclaw/openclaw/pull/128995)（已关闭）：将侧边栏中的完整会话操作（固定、标记未读、设置图标、复制 ID、移入分组）提升到聊天窗口头部菜单。
- [PR #120900](https://github.com/openclaw/openclaw/pull/120900) / [PR #116489](https://github.com/openclaw/openclaw/pull/116489)（已关闭）：Control UI 支持管理员审阅安装策略警告并显式确认后继续安装；CLI 侧要求输入插件名确认。

**其他修复（待合并）**

- [PR #134590](https://github.com/openclaw/openclaw/pull/134590)：修复“孤立安装记录”（插件文件已删但记录存在）阻塞 `plugins update --all` 与卸载的问题。
- [PR #133358](https://github.com/openclaw/openclaw/pull/133358)：grep 工具支持显示 ripgrep 以 base64 形式输出的非 UTF-8 文件名。
- [PR #134593](https://github.com/openclaw/openclaw/pull/134593)：CI 复用依赖安装与声明构建，减少重复成本。

## 4. 社区热点

今日讨论最活跃的 Issue：

- **[#91588 Critical: Gateway Memory Leak — RSS 从 350MB 涨至 15.5GB 并反复 OOM](https://github.com/openclaw/openclaw/issues/91588)**（23 评论，P1，6 月创建仍未关闭）。这是目前最受关注的问题：正常使用 2–3 天后 RSS 飙升至 15.5GB，触发 OOM killer 与 `launchd-handoff` 重启循环。社区诉求：尽快定位泄漏源并给出临时缓解手段（如定期重启、内存上限配置）。
- **[#102175 embedded prompt cache 跨边界失效](https://github.com/openclaw/openclaw/issues/102175)**（18 评论，P2）。长会话的 provider 提示词缓存会在房间事件、授权、队列、压缩、恢复等边界处失效，导致 token 成本与延迟上升。用户希望跨边界保持缓存复用。
- **[#22676 Signal daemon stop() 竞态条件（已关闭）](https://github.com/openclaw/openclaw/issues/22676)**（17 评论，P1）。SIGUSR1 重启时旧 signal-cli 未退出即启动新实例，导致端口/文件锁冲突与发送失败。该问题已关闭，证明团队在推进修复。
- **[#96834 WhatsApp 1:1 图片消息楔住主通道约 3 分钟](https://github.com/openclaw/openclaw/issues/96834)**（14 评论，P1）。原生多模态图片注入导致 `active_reply_work` 悬挂，消息处理被阻塞。用户关注消息延迟与丢失。
- **[#79077 Telegram bot-to-bot 与 guest-bot 模式支持](https://github.com/openclaw/openclaw/issues/79077)**（13 评论，8 👍）。Telegram 官方 2026-05-07 新特性，社区呼声较高，但状态为 `needs-product-decision`，尚无排期信号。

## 5. Bug 与稳定性

按严重程度排列（均附链接；标注修复状态）：

**P0 / 升级阻断**

- [Bug: required Codex runtime dead-ends on capability consent](https://github.com/openclaw/openclaw/issues/133793)（P0）：macOS 全新安装 2026.8.1 时，Codex 运行时能力同意步骤未完成，交互式应用报错并

---

## 横向生态对比

# 个人 AI 助手/自主智能体开源生态横向对比分析报告

**日期：2026-09-01**


## 一、生态全景

个人 AI 助手与自主智能体开源生态正处于**高迭代、高反馈、高修复压力**的高速发展期。头部项目（OpenClaw、Hermes Agent）单日分别产生近千条 Issue/PR 更新，同时发布重大版本，表明功能推进与稳定性加固正处于白热化并行阶段。值得关注的是，多个项目的社区反馈焦点惊人一致：**升级迁移体验、内存与资源管理、Gateway/守护进程稳定性、密钥安全管理**成为制约生产落地的共性瓶颈。与此同时，以 LiteLLM 为代表的代理/网关层和以 Temporal 为代表的编排基础设施，正在为智能体的规模化部署与可靠性提供底层支撑——生态已初步形成“**端侧助手（OpenClaw/Hermes/Pi）→ 开发工具链（OpenHands SDK）→ 代理网关（LiteLLM）→ 编排引擎（Temporal）**”的完整分层格局。


## 二、各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | Release 情况 | 合并/关闭率 | 健康度评估 |
|---|---|---|---|---|---|
| **OpenClaw** | 448 条（新开/活跃 212，关闭 236） | 500 条（待合并 242，合并/关闭 258） | **v2026.8.1 稳定版** | PR 合并率 51.6%，Issue 关闭率 52.7% | ⚠️ 高迭代，但升级阻断与 P0 问题多发，生产稳定性承压 |
| **Hermes Agent** | 500 条（新开/活跃 314，关闭 186） | 500 条（待合并 324，合并/关闭 176） | **v0.21.0 “The Pantheon Release”**（约 5,800 commits、760+ 贡献者） | PR 合并率 35.2%，Issue 关闭率 37.2% | ✅ 高活跃，大型版本收敛中，桌面端整合型 PR 密集；Gateway 稳定性有隐忧 |
| **LiteLLM** | 78 条（新开/活跃 43，关闭 35） | 267 条（待合并 157，合并/关闭 110） | 无（1.99.0 发布流水线因 Docker 依赖失败阻塞） | PR 合并率 41.2%，Issue 关闭率 44.9% | ✅ 高速发展，工程质量导向；发版阻塞属于外部依赖问题 |
| **Pi** | 60 条（新开/活跃 7，关闭 53） | 18 条（合并/关闭 14，待合并 4） | 无（0.84.4 仍为最新） | PR 合并率 77.8%，Issue 关闭率 88.3% | ✅ 健康良好；供应商扩展活跃，但 TUI 层长期 bug 悬而未决 |
| **OpenHands SDK** | 14 条（新开/活跃 5，关闭 9） | 50 条（合并/关闭 7，待合并 43） | 无 | PR 合并率 14%，Issue 关闭率 64% | ⚠️ 活跃度中等；安全修复有进展（密钥泄露、模型输出 mask），但积压 PR 较多 |
| **Temporal** | 2 条（新开 1，关闭 1） | 51 条（合并/关闭 15，待合并 36） | 无（1.32.0 分支在收尾） | PR 合并率 29.4% | ✅ 稳定迭代；reliability-2026 方向持续投入，调度器静默停止 bug 需关注 |

> 说明：OpenHands SDK 为 SDK 类项目，体量天然小于端侧助手类项目；Temporal 为后端基础设施，Issue 节奏以“少而精”为特征。


## 三、OpenClaw 在生态中的定位

### 核心地位

OpenClaw 是当前生态中**社区规模最大、迭代速度最快的个人 AI 助手基础设施项目**。单日 448 条 Issue 更新与 500 条 PR 更新在各项目中居首（与 Hermes Agent 并列第一梯度），v2026.8.1 稳定版的发布频率与用户覆盖面均显示其处于生态核心位置。

### 优势

- **社区体量与响应速度**：Issue/PR 更新量为 Pi 的 7~28 倍、LiteLLM 的 2~6 倍，反馈闭环极快
- **功能广度**：覆盖 Gateway、Control UI、CLI、插件系统、多通道（Telegram/WhatsApp/Signal）、多模态等完整个人 AI 助手能力栈
- **生态控制力**：Control UI 安装策略审阅、CLI 插件确认等治理机制已超越“个人工具”阶段，向可管理的企业级平台演进

### 技术路线差异

| 对比维度 | OpenClaw | Hermes Agent | Pi |
|---|---|---|---|
| 架构取向 | 重型常驻服务（Gateway + LaunchAgent + Control UI + 插件系统） | 重量级全栈（Desktop 端 + Compressor + 多后端），桌面体验优先 | 轻量终端优先（TUI），本地/远程双模式 |
| 部署模型 | 服务器/常驻进程模式，自带自更新与迁移框架 | 桌面应用模式，更新器与安装器复杂度高（Windows/Linux 蓝屏问题） | 纯 CLI/TUI 工具，无守护进程负担 |
| 核心复杂度来源 | 升级迁移、Gateway 稳定性、多通道接入 | 跨平台桌面端、会话压缩/合成器、多 provider 一致性 | TUI 渲染、会话生命周期、供应商目录维护 |

### 规模对比

- OpenClaw：单日 448 Issues + 500 PRs，v2026.8.1 版本迭代
- Hermes Agent：单日 500 Issues + 500 PRs，v0.21.0 为最大版本跃迁（760+ 贡献者）
- 其余项目体量级差显著（LiteLLM 78/267，Pi 60/18，OpenHands 14/50，Temporal 2/51）

**结论**：OpenClaw 是个人 AI 助手赛道的“主战场”项目，面临的压力也最大——用户基数大导致升级迁移问题被放大并成社区焦点；但其高迭代速度与生态治理能力使其仍是该赛道的参照基准。


## 四、共同关注的技术方向

多个项目不约而同地指向以下共性技术诉求：

### 1. 升级迁移与版本平滑性
- **OpenClaw**：v2026.8.1 多起升级后 Gateway 无法启动、`doctor --fix` 陷入循环、迁移误删配置（#133813、#133984、#133999、#134445、#133347）
- **Hermes Agent**：`hermes update` 破坏 Debian 安装、Windows ZIP fallback 删除桌面应用（#83529、#83846）
- **LiteLLM**：Docker 发布流水线因 python 3.14/uvloop 不兼容失败

### 2. 内存泄漏与资源管理
- **OpenClaw**：Gateway RSS 从 350MB 涨至 15.5GB 并反复 OOM（#91588），PR #134554 降低会话查找内存占用
- **Hermes Agent**：本地后端被无端杀死、死进程占用资源（#96266）
- **OpenHands SDK**：Tom 处理历史可检查点未被索引的事件（#4667）

### 3. 密钥安全与配置脱敏
- **OpenHands SDK**：`sanitized_env()` 泄露 `OH_SECRET_KEY` 和 session-key 至子进程（#4802，high 优先级）；模型输出未 mask（#4678，已关闭）
- **LiteLLM**：Redis 缓存超时导致消息内容泄露到日志（#11157）；PII 脱敏不生效（#14516）；`/v1/models` 泄露访问组名称（#25550）

### 4. 调度器/定时任务可靠性
- **Temporal**：调度器 workflow 存在 pending timer 但无物理 timer task，静默停止触发（#11869）；V1 调度器迁移数据丢失（#11880）
- **OpenClaw**：cron 迁移将有效任务隔离为 `invalid-schedule`（#133347）

### 5. 长会话/压缩管线优化
- **OpenClaw**：embedded prompt cache 跨边界失效导致 token 成本上升（#102175）；Responses 压缩管线 6 个缺陷修复（PR #130993）
- **Hermes Agent**：压缩器接受 `reasoning_content` 作为摘要（PR #99888）；自动化压缩回归（#97963）
- **Pi**：压缩期间排队提示词丢失（#5886 元 issue）；上下文预算忽略 maxTokens 输出保留（#8061）

### 6. 多模态与消息阻塞问题
- **OpenClaw**：WhatsApp 图片消息楔住主通道约 3 分钟（#96834）
- **Pi**：TUI 流式输出渲染错乱（#8584）、大 diff 渲染崩溃（#8036）
- **Hermes Agent**：桌面端会话面板滚动/焦点抢占（#99881、#99891）

### 7. 可观测性与日志治理
- **OpenClaw**：shell 安装器日志为空（PR #134236）
- **LiteLLM**：畸形虚拟密钥导致 ERROR 日志刷屏（#38712）；Bedrock provider 头部信息丢失（#38357）；团队级日志回调覆盖透传路由（#38979）
- **Temporal**：Nexus 日志增加 `nexus-stage` 标签（#11757）


## 五、差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 核心架构 | 差异化特征 |
|---|---|---|---|---|
| **OpenClaw** | 全功能个人 AI 助手（多通道、插件、自动化、Control UI） | 个人/开发者/小型团队 | 重型常驻服务（Gateway + Agent + 插件系统 + 配置迁移框架） | **最完整的端侧助手栈**；升级迁移与稳定性是当前主要矛盾；社区驱动，功能覆盖最广 |
| **Hermes Agent** | 桌面优先的 AI 助手（Desktop 端 + 会话压缩 + 多后端合成器） | 桌面用户/专业个人用户 | 桌面应用 + 本地后端；大规模会话管理 | **桌面端体验极致化**；v0.21.0 为生态最大版本跃迁；整合型 PR 表明治理能力成熟 |
| **OpenHands SDK** | Agent 开发 SDK（子代理、工具调用、镜像构建、密钥安全） | Agent 应用开发者 | SDK + agent-server 镜像 + TypeScript client | **面向开发者的核心基础设施**；安全加固（密钥 mask、版本对齐）是近期亮点；镜像体积优化是社区痛点 |
| **Pi** | 终端 AI 编程伴侣（TUI、多 provider、/fork 等会话操作） | CLI 重度用户/开发者 | 单二进制 + TUI + 本地/远程后端 | **轻量、快速、供应商生态扩展迅猛**（单日 +3）；TUI 渲染稳定性待提升；Rust 实现，性能优势明确 |
| **LiteLLM** | LLM 代理网关（多 provider 路由、认证、预算、团队管理） | 企业平台团队/运维 | Python 代理服务 + Rust 桥接层 + UI | **企业级代理/网关定位**；团队隔离与认证边界加固方向明确；可观测性（日志降噪、透传路由覆盖）持续投入 |
| **Temporal** | 工作流编排引擎（持久化执行、重试、调度器） | 后端平台团队/SRE | Go 服务端 + 持久化（PostgreSQL/ES/Cassandra） | **生产级可靠性工程**；reliability-2026 专项；调度器迁移与数据完整性是当前重心；不是 AI 专用，但被广泛用于 Agent 编排 |


## 六、社区热度与成熟度

### 第一梯度：超活跃 · 快速迭代期
- **OpenClaw**（448 I / 500 PR）与 **Hermes Agent**（500 I / 500 PR）处于同一热度量级。两者均发布重大版本（v2026.8.1 / v0.21.0），社区反馈与开发响应双向流转极快。OpenClaw 的 Issue 关闭率（52.7%）高于 Hermes（37.2%），但双方都面临“功能推进快、回归风险高”的典型成长期问题。
- **特征**：Issue/PR 近千条/日，发布频率高，社区极其活跃，但升级迁移与稳定性问题被放大。

### 第二梯度：高活跃 · 质量控制期
- **LiteLLM**（78 I / 267 PR）：PR 数量显著高于 Issue，说明核心团队主导开发，社区反馈相对受控。工程导向明显，团队隔离、Rust 桥接重构、日志治理等质量主线清晰。
- **特征**：发布节奏受外部依赖影响；团队侧驱动为主，系统性工程质量建设。

### 第三梯度：中等活跃 · 生态扩张期
- **Pi**（60 I / 18 PR）：Issue 关闭率高达 88.3%，PR 合并率 77.8%，维护效率高。单日合并 3 个新供应商 PR，处于生态快速扩张阶段，但 TUI 核心稳定性（大 diff 崩溃、长行渲染错乱）仍存在未收敛的长期问题。
- **OpenHands SDK**（14 I / 50 PR）：PR 活跃但合并率较低（14%），存在合并积压风险。安全修复与镜像优化方向正确，但项目整体节奏与头部项目差距较大。
- **特征**：体量适中；维护效率高；在各自细分方向上稳步推进。

### 第四梯度：稳定迭代 · 成熟期
- **Temporal**（2 I / 51 PR）：Issue 极少但 PR 持续，说明核心功能已稳定，正在做发布分支收敛与可靠性加固（reliability-2026）。这是最接近“成熟产品”状态的项目。
- **特征**：已过功能爆发期；以可靠性、可观测性、存储优化为主；社区反馈以深度生产问题为主。


## 七、值得关注的趋势信号

### 1. 稳定性正取代功能成为竞争焦点
OpenClaw 的“升级迁移是最大挑战”、Hermes 的“更新器/安装器破坏”、LiteLLM 的“发布流水线因依赖失败”——三个头部项目同一天在不同层面遭遇稳定性痛点。**对于 AI 智能体开发者：工具链的“升级体验”与“版本平滑性”即将成为新的竞争维度。** 采用滚动发布、自动回滚、迁移预检的项目将获得显著竞争优势。

### 2. 从“单 Agent”走向“多 Agent/子 Agent”架构
OpenHands SDK 的“服务端子会话启动”（#4781）、LiteLLM 的“团队级隔离与回调”、OpenClaw 的插件系统治理、Pi 的 `/fork` 会话操作——均在向**可组合、可嵌套的 Agent 架构**演进。多 Agent 协作的安全边界（密钥隔离、权限继承）是最突出的共性技术挑战。

### 3. 密钥/凭证管理成为安全最短板

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-09-01

> 数据区间：2026-08-31 ~ 2026-09-01 · 数据来源：GitHub Issues / PRs / Releases

---

## 1. 今日速览

过去 24 小时项目保持极高活跃度：**500 条 Issue 更新**（新开/活跃 314，关闭 186）与**500 条 PR 更新**（待合并 324，合并/关闭 176）几乎同量级，说明社区反馈与维护者响应形成了密集的双向流转。**v0.21.0（代号 The Pantheon Release）正式发布**，自 v0.20.0 以来累计约 5,800 commits、2,475 个合并 PR、2,100 个 Issue 关闭、760+ 贡献者，是项目迄今规模最大的一次版本跃迁。值得关注的是，桌面端（Desktop）在今日 PR 流中占据绝对主导，出现多组"supersedes 多个旧 PR"的整合型修复，表明维护者正在系统性地收敛此前分散的会话状态与合成器相关问题；与此同时，一批 P1 级 Windows 平台严重 Bug（含蓝屏、更新器破坏安装）已随 v0.21.0 标记关闭。整体健康度良好，但 Gateway 稳定性（SIGSEGV、DB 损坏）与自动化压缩回归（#97963）仍是当前最值得警惕的风险点。

---

## 2. 版本发布

### Hermes Agent v0.21.0（v2026.8.31） — The Pantheon Release

- **发布日期**：2026-08-31
- **版本规模**：v0.20.0 至今约 5,800 commits、2,475 个合并 PR、5,680 个文件变更（+869k / −135k 行）、约 2,100 个 Issue 关闭、760+ 贡献者
- **定位**：官方称 "v0.20.0 made Hermes the herald —"，后续描述被截断，完整发布说明可参考 [Releases 页面](https://github.com/NousResearch/hermes-agent/releases)

**可交叉验证的修复范围**（从今日关闭的 Issue 推断）：

| 关联 Issue | 问题 | 状态 |
|---|---|---|
| [#89614](https://github.com/NousResearch/hermes-agent/issues/89614) | Windows 下通过 stale-PID `taskkill /F /PID` 误杀 `svchost.exe`，导致 0xEF 蓝屏 | 已关闭 |
| [#83529](https://github.com/NousResearch/hermes-agent/issues/83529) | `hermes update` 直接在 Debian 上破坏安装 | 已关闭 |
| [#83846](https://github.com/NousResearch/hermes-agent/issues/83846) | Windows ZIP fallback 更新删除桌面应用且永不重建 | 已关闭 |
| [#54220](https://github.com/NousResearch/hermes-agent/issues/54220) | Windows 桌面 GUI 子进程 spawn 时控制台窗口闪现 | 已关闭 |
| [#94058](https://github.com/NousResearch/hermes-agent/issues/94058) | Linux `.desktop` 的 Exec 解析 venv 符号链接错误 | 已关闭 |
| [#95003](https://github.com/NousResearch/hermes-agent/issues/95003) | xAI 拒绝 `tool_search` 保留函数名，Grok 提供商不可用 | 已关闭 |
| [#96266](https://github.com/NousResearch/hermes-agent/issues/96266) | Linux 桌面端强制本地后端在 READY 后约 10s 被杀死 | 已关闭 |

**迁移注意事项**：建议桌面端用户优先通过官方更新通道升级，避免使用 ZIP fallback（#83846 修复亦在此版本）；Windows 用户升级后确认 `svchost.exe` 相关防护逻辑（#89614）已生效。

---

## 3. 项目进展

今日可见的合并/关闭 PR 主要集中在**桌面端会话状态与合成器体验**，且呈现明显的"整合收敛"特征——多个新 PR 直接 supersedes 此前分散的修复：

### 桌面端大规模整合（今日新增，OPEN）

| PR | 内容 | 整合范围 |
|---|---|---|
| [#99881](https://github.com/NousResearch/hermes-agent/pull/99881) | 隐藏会话面板不再抢占可见聊天的滚动/焦点 | supersedes #81829, #98316, #98681, #95503, #99370 |
| [#99885](https://github.com/NousResearch/hermes-agent/pull/99885) | 远程配置文件在共享 Dashboard 上保持各自模型设置 | supersedes #96714 |
| [#99888](https://github.com/NousResearch/hermes-agent/pull/99888) | 压缩器接受 `reasoning_content` 作为摘要（DeepSeek/Qwen/Kimi） | supersedes #95231, #98496 |
| [#99890](https://github.com/NousResearch/hermes-agent/pull/99890) | 重新生成被拒绝时恢复聊天记录 | supersedes #95848，closes #95745 |
| [#99891](https://github.com/NousResearch/hermes-agent/pull/99891) | 已失效运行时不再抢占合成器焦点 | supersedes #97874, #98455, #98568, #98629, #97887 |
| [#99892](https://github.com/NousResearch/hermes-agent/pull/99892) | 过期的合成器模型不再固定到新聊天 | supersedes #91482 |

### 今日已合并/关闭的桌面端修复

- [#98455](https://github

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

好的，作为开源项目分析师，我根据 OpenHands SDK 在 2026-09-01 的 GitHub 数据，为您整理了这份项目动态日报。

---

### OpenHands SDK 项目动态日报 (2026-09-01)

#### 1. 今日速览
今日项目活跃度**高**。过去24小时内，PR 更新达 50 条，Issues 更新 14 条，显示出社区提交与审阅热情高涨。虽然无新版本发布，但多项针对 SDK 安全、镜像体积优化和核心工具链的 PR 正处于活跃的讨论与合并阶段。一个值得注意的动向是，**安全与密钥管理**成为当前开发的重点，高优先级的安全 Issue 与修复 PR 同步出现。整体来看，项目正处于密集的功能迭代与稳定性加固期。

#### 2. 版本发布
今日无新版本发布。

#### 3. 项目进展
今日虽有 7 个 PR 被合并/关闭，但未列出具体条目。从关闭的 Issues 来看，项目在以下方面取得了明确进展：
- **修复安全盲点**：`[Security] Model output is never masked on the standard Agent path` [#4678](https://github.com/OpenHands/software-agent-sdk/issues/4678) 已关闭，意味着模型输出中密钥泄露的问题已在标准 Agent 路径上得到修复，这是重要的安全加固。
- **强化发布一致性**：`Enforce version parity between SDK packages and TypeScript client` [#4778](https://github.com/OpenHands/software-agent-sdk/issues/4778) 已关闭，表明 SDK 包与 TypeScript 客户端的版本对齐机制已落地，有助于减少未来版本碎片化问题。
- **优化镜像体积**：`Make OpenVSCode Server, Chromium, Docker Engine, and the desktop stack optional` [#4645](https://github.com/OpenHands/software-agent-sdk/issues/4645) 已关闭，结合关联的 `[Feature]: Reorganise agent-server image build` [#4643](https://github.com/OpenHands/software-agent-sdk/issues/4643) 中“Steps 0–2 done”的状态，说明官方已着手将可选能力从 agent-server 镜像中解耦，未来将显著降低镜像体积。

#### 4. 社区热点
- **镜像体积与可定制性** (评论: 4, 已关闭): Could not be more clearly stated. 在 `Make OpenVSCode Server, Chromium, Docker Engine, and the desktop stack optional` [#4645](https://github.com/OpenHands/software-agent-sdk/issues/4645) 中，用户指出非核心组件占镜像体积高达 34.5% (564.9 MB / 1.64 GB)，且“nothing currently tracks them”。这反映出用户对**轻量化、可按需定制镜像**的强烈诉求，是部署灵活性和资源效率的核心痛点。
- **数据一致性与可靠性** (评论: 3): `[Bug]: Tom processing history can checkpoint events that were never indexed` [#4667](https://github.com/OpenHands/software-agent-sdk/issues/4667) 得到了较多讨论。该问题涉及会话处理历史的底层数据一致性，社区对此类隐蔽的 P0 级数据风险非常关注，讨论热度反映了对**核心数据管道健壮性**的高要求。
- **安全与密钥泄露** (评论: 1, 但优先级高): `[security, priority:high]` 的 Issue `sanitized_env() leaks OH_SECRET_KEY...` [#4802](https://github.com/OpenHands/software-agent-sdk/issues/4802) 虽然评论数不多，但高优先级标签使其成为焦点，社区对**子进程环境变量中敏感信息泄露风险**极为敏感。

#### 5. Bug 与稳定性
今日报告的 Bug 按严重程度排列如下：

- **严重 (High)**:
    - **环境变量密钥泄露** (Ready-for-dev): `sanitized_env() leaks OH_SECRET_KEY and V1 session-key slots to agent subprocesses` [#4802](https://github.com/OpenHands/software-agent-sdk/issues/4802)。这是高危安全漏洞，影响所有调用 agent 子进程的工具（bash, file_editor, grep等），易造成核心密钥泄露。**待修复**。

- **中等 (Medium)**:
    - **数据索引不一致**: `Tom processing history can checkpoint events that were never indexed` [#4667](https://github.com/OpenHands/software-agent-sdk/issues/4667)。可能导致数据丢失或检索异常。
    - **功能模块失效**: `Skills marketplace returns empty against the current extensions manifest layout` [#4665](https://github.com/OpenHands/software-agent-sdk/issues/4665)。加载器逻辑与现行仓库结构不匹配，导致技能市场功能不可用。
    - **并发数据竞争**: `Concurrent stdout and stderr chunks can reuse BashOutput order values` [#4659](https://github.com/OpenHands/software-agent-sdk/issues/4659)。会导致输出流顺序错乱，影响 Agent 对执行结果的解析。

- **较低 (Low)**:
    - **数据一致性风险**: `ConversationService: stored fields mutated in memory before save_meta() with no rollback on failure` [#4800](https://github.com/OpenHands/software-agent-sdk/issues/4800)。写入失败时内存与磁盘状态不一致。
    - **CI 可用性问题**: `TypeScript client endpoint audit fails on every fork PR` [#4798](https://github.com/OpenHands/software-agent-sdk/issues/4798)。由于令牌权限不足，所有 fork 提交的 PR 都无法通过该检查。**已有修复 PR** ([#4796](https://github.com/OpenHands/software-agent-sdk/pull/4796))。

#### 6. 功能请求与路线图信号
- **核心服务端能力扩展** (Ready-for-dev): `Add a server-side tool for launching same-backend child conversations` [#4781](https://github.com/OpenHands/software-agent-sdk/issues/4781)。该请求旨在将对话创建逻辑从客户端转移到服务端，以支持更可靠的架构。这可能是迈向更复杂多智能体协作场景的重要一步，有望被纳入近期路线图。
- **镜像构建体系重构** (进行中): `Reorganise agent-server image build — selectable capabilities, parameterised provider set...` [#4643](https://github.com/OpenHands/software-agent-sdk/issues/4643)。该功能请求与已关闭的 [#4645](https://github.com/OpenHands/software-agent-sdk/issues/4645) 直接相关，明确提出了“Make image contents an explicit, selectable contract”，是镜像优化的路线图核心。
- **工程效率工具链** (Ready-for-dev):
    - `check_deprecations.py should catch overdue Pydantic Field-level deprecations` [#4794](https://github.com/OpenHands/software-agent-sdk/issues/4794) 旨在强化 CI 对过时代码的检查。
    - `Remove the overdue deprecated org_config field from SkillsRequest` [#4793](https://github.com/OpenHands/software-agent-sdk/issues/4793) 则是清理历史技术债务。这两点说明项目已进入**工程化与代码健康度提升**的阶段。

#### 7. 用户反馈摘要
- **痛点：镜像臃肿** (#4645)：用户明确算了一笔账（564.9 MB 的未使用组件），表达了“被迫为不需要的功能买单”的不满，反馈非常具体且具有说服力。
- **痛点：配置/数据不生效** (#4800, #4665)：用户反馈了因底层设计缺陷导致的功能失效或状态不一致问题，如 save_meta 失败无回滚、技能市场加载为空，这会直接影响用户体验和对项目的信任度。
- **特性渴望：更强的服务端能力** (#4781)：用户设计了一个需要服务端支持的新特性，但发现当前架构下实现复杂且有缺陷，期望项目提供更底层的服务端支持，体现了对平台扩展能力的期待。

#### 8. 待处理积压
以下 PR 长期处于开放状态，建议维护者重点关注：
- **>1个月无更新**:
    - `fix: decrypt LLM profiles for subagents` [#4183](https://github.com/OpenHands/software-agent-sdk/pull/4183) (创建于 07-22)。这是一个影响子代理配置的功能修复，长期未合并可能阻塞相关功能。
    - `fix(agent-server): do not force-cancel the run task finally block during close()` [#4412](https://github.com/OpenHands/software-agent-sdk/pull/4412) (创建于 08-07)。修复关闭时强制取消任务导致状态异常的问题。

- **>2周无更新**:
    - `fix(profiles): sync seeded default AgentProfile llm_profile_ref...` [#4372](https://github.com/OpenHands/software-agent-sdk/pull/4372) (创建于 08-05)。
    - `fix(tools): shim mcp 1.x Server decorators so browser_use constructs under mcp 2.x` [#4406](https://github.com/OpenHands/software-agent-sdk/pull/4406) (创建于 08-07)。该修复对使用特定 MCP (Model Context Protocol) 版本环境下的工具兼容性至关重要。
    - `fix(sdk): Track DeepSeek prompt cache hits in telemetry` [#4490](https://github.com/OpenHands/software-agent-sdk/pull/4490) (创建于 08-14)。

---
**总结**：OpenHands SDK 项目保持高速迭代，社区活跃。当前重点在**安全加固**（密钥泄露、模型输出mask）和**架构优化**（镜像解耦）。大量 "ready-for-dev" 标签的 Issue 和存在已久但未合并的 PR，提示项目维护者需要在**功能开发与合并积压**之间找到平衡，以维持社区的贡献热情。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-09-01

## 1. 今日速览

过去 24 小时 Pi 项目更新频繁：**60 条 Issue 更新**（其中新开/活跃 7 条，关闭 53 条，关闭中大部分为 untriaged/新增供应商请求的批量处理），**18 条 PR 更新**（14 条已合并/关闭，4 条待合并）。值得关注的是 8 月 31 日至 9 月 1 日出现了密集的“新供应商接入”和“Bug 修复”提交潮：**CoralBricks、Melious、腾讯 Token Plan 三个新 provider 的 PR 在同一天合并**，同时 4 个并发/生命周期相关的修复 PR（#8902、#8908、#8929、#8930）也集中落地。无新版本发布（0.84.4 仍为当前版本）。整体项目健康：Issue 关闭率高（88%），PR 合并率高（78%），但部分长期存在的 TUI/并发稳定性问题（#8036、#8061、#8134）仍悬而未决。

---

## 2. 版本发布

**无新版本发布**（最新仍为 0.84.4）。当前主分支已积累多项修复与新功能，预计近期会有一个 0.84.x 补丁或 0.85 里程碑发布（见下文 PR 合并情况）。

---

## 3. 项目进展

今日合并/关闭的 PR 可归为 4 个主题：

### 3.1 新供应商接入（共 3 个）

| PR | 供应商 | 说明 |
|---|---|---|
| [#8925](https://github.com/earendil-works/pi/pull/8925) | CoralBricks | 内置 provider，模型目录由 models.dev 自动同步，支持 OpenAI-compatible API（对应 issue #8926） |
| [#8903](https://github.com/earendil-works/pi/pull/8903) | Melious | 欧洲基础设施的开放权重模型服务，无 models.dev 条目，自带模型列表生成脚本 |
| [#8876](https://github.com/earendil-works/pi/pull/8876) | 腾讯 Token Plan | 支持 tc-code-latest、DeepSeek V4 系列、GLM-5.2、MiniMax-M2.7 |

### 3.2 会话生命周期与并发修复（共 3 个）

- [#8908](https://github.com/earendil-works/pi/pull/8908) — 保留压缩（compaction）期间排队的提示词，修复 #5886 中的“compaction/input-hook 竞态”
- [#8929](https://github.com/earendil-works/pi/pull/8929) — 内存中 `/fork` 操作先结算当前 turn 再分支，防止进行中的工具调用被错误写入新会话
- [#8930](https://github.com/earendil-works/pi/pull/8930) — 新增 `ctx.hasQueuedAgentMessages()`，让扩展能观察排队的 `steer`/`followUp` 消息（修复 #8891 的核心能力）

### 3.3 模型目录与计费修正（共 2 个）

- [#8915](https://github.com/earendil-works/pi/pull/8915) — DeepSeek V4 目录价格更新为高峰/低谷费率的中点值（对应 issue #8491）
- [#8873](https://github.com/earendil-works/pi/pull/8873) — DeepSeek V4 系列从 OpenAI Completions API 迁移到 Responses API

### 3.4 其他修复（共 6 个）

- [#8907](https://github.com/earendil-works/pi/pull/8907) — 扩展发现机制支持 `.disabled` 目录（此前仅文件支持）
- [#8898](https://github.com/earendil-works/pi/pull/8898) — 修复 seccomp 受限策略下 SIGWINCH 信号被拦截的问题（#8897）
- [#8879](https://github.com/earendil-works/pi/pull/8879) — fork 产生的元数据条目不再导致会话解析失败
- [#8901](https://github.com/earendil-works/pi/pull/8901) — 新增 TCP/WebSocket 传输与实验性 server/client、Ollama provider
- [#8887](https://github.com/earendil-works/pi/pull/8887) — 文档：models.md 新增远程 OpenAI 兼容 provider 示例
- [#8902](https://github.com/earendil-works/pi/pull/8902) — 将循环中压缩检查路由到完整阈值检查流程

**结论**：项目在供应商生态拓展（单日 +3）、稳定性修复和 TUI/协议层实验性功能（TCP/WS transport）三个方向均有实质推进。特别是并发/生命周期相关的 3 个 PR 同日合并，说明维护者正在系统性地解决 `AgentSession` 的“结算/延续”类问题（#5886 元 issue）。

---

## 4. 社区热点

### 4.1 最热 Issue：#8584 — TUI 流式输出错乱（25 评论，9 👍）

[#8584](https://github.com/earendil-works/pi/issues/8584)（已关闭）是过去 24 小时讨论最激烈的问题：工具输出长行后，assistant 文本流被错误地“每行一个词”渲染。用户 `@ractive` 在 8 月 24 日报告后，获得了大量社区共鸣。该问题本质是 TUI 渲染层在处理工具输出的宽行后，终端宽度状态未被正确重置。虽然已被关闭，但 25 条评论说明这是日常高频痛点（长行工具输出是常见场景）。

### 4.2 元问题：#5886 — AgentSession 生命周期 bug 类（10 评论，4 👍）

[#5886](https://github.com/earendil-works/pi/issues/5886) 是 `@mitsuhiko` 提出的“元 issue”，归纳了一类“会话后逻辑从未正确结算的 transcript 续接”问题。过去 24 小时内多个 PR（#8908、#8929、#8930）都直接服务于此，说明维护者认可了该分类并正在系统性修复。

### 4.3 潜在高影响：#8036 — 大 diff 渲染崩溃（7 评论）

[#8036](https://github.com/earendil-works/pi/issues/8036) 与 #8584 同属 TUI 渲染层问题：`edit` 工具处理 ~14.5MB 的 diff 时直接崩溃，且在会话恢复时也会复现。目前仍是 OPEN 状态，暂无对应修复 PR。

---

## 5. Bug 与稳定性

按严重程度排列：

### 5.1 严重（核心功能不可用/崩溃）

| Issue | 问题 | 状态 | 对应修复 |
|---|---|---|---|
| [#8036](https://github.com/earendil-works/pi/issues/8036) | 编辑大文件产生大 diff 时 TUI 崩溃；会话恢复时复现 | OPEN（08-12 报告） | ❌ 无 |
| [#8061](https://github.com/earendil-works/pi/issues/8061) | 上下文预算忽略 maxTokens 输出保留：78% 输入占用即被拒绝；自动压缩重试同样失败 | OPEN（08-13 报告） | ❌ 无 |
| [#8134](https://github.com/earendil-works/pi/issues/8134) | 经正向代理访问纯 HTTP provider 时，首个工具调用后 Agent 停止（0.84.0 回归） | OPEN（08-14 报告） | ❌ 无 |

### 5.2 中等（特定场景故障）

| Issue | 问题 | 状态 | 对应修复 |
|---|---|---|---|
| [#8845](https://github.com/earendil-works/pi/issues/8845) | `/tree` 分支摘要硬编码 `maxTokens: 2048`，大分支确定性失败 | OPEN（08-30 报告） | ❌ 无 |
| [#8927](https://github.com/earendil-works/pi/issues/8927) | 凭证存储快照读取使用独占锁；同步路径仅 ~200ms 预算 → 并发会话报“Lock file is already being held” | CLOSED（untriaged） | ❌ 无公开修复 |
| [#8928](https://github.com/earendil-works/pi/issues/8928) | 并发启动时误报“No API key found”（因其他 provider 过期 OAuth 凭据阻塞） | CLOSED（untriaged） | ❌ 无公开修复 |
| [#8891](https://github.com/earendil-works/pi/issues/8891) | `clearQueue()` 返回已清除，但 steering 消息在压缩后仍被发送 | CLOSED | ✅ #8930 提供观察 API，待验证 |
| [#8752](https://github.com/earendil-works/pi/issues/8752) | Bedrock 的 `usage.input` 未跨模型家族归一化：Anthropic 报净额，OpenAI 报毛额 → 错误缓存未命中提示、成本翻倍 | CLOSED | ❌ 无 |

### 5.3 轻微（体验/兼容性）

| Issue | 问题 | 状态 | 对应修复 |
|---|---|---|---|
| [#8684](https://github.com/earendil-works/pi/issues/8684) | `PI_OFFLINE` 静默禁用所有模型发现，与文档描述不符 | CLOSED | ❌ 无（应补充文档或修改行为） |
| [#8760](https://github.com/earendil-works/pi/issues/8760) | OpenRouter `:free` 模型因 `max_tokens` 超限报 400 | CLOSED | ❌ 无 |
| [#8894](https://github.com/earendil-works/pi/issues/8894) | CLI 值选项缺少值时吞掉后续 flag（如 `pi -ne --provider` 将 `--provider` 当作值） | CLOSED | ❌ 无 |
| [#8877](https://github.com/earendil-works/pi/issues/8877) | `read` 工具将 U+202F 窄不换行空格规范化为普通空格 → 本地化 macOS 截图名 ENOENT | CLOSED | ❌ 无 |
| [#8789](https://github.com/earendil-works/pi/issues/8789) | Windows 下 `child_process` 未设 `windowsHide: true`，控制台窗口频繁闪烁抢焦点 | CLOSED | ❌ 无 |

### 5.4 已修复（今日合入）

- #5886 相关竞态 → #8908、#8929
- #8884（压缩检查未

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-09-01

## 1. 今日速览

过去24小时项目活跃度极高，**Issues 更新78条（新开/活跃43条，关闭35条）**，**PR 更新267条（待合并157条，合并/关闭110条）**，无新版本发布。PR 合并/关闭率约 41%，说明当前开发流高速运转，大量维护性修复与功能推进并行。从 PR 分布看，团队重点集中在 **代理稳定性（日志降噪、认证边界、团队隔离）**、**向量存储/推理集成（Milvus gRPC、嵌入凭证解析）** 以及 **Rust/Python 桥接层架构重构** 三方面。Issue 侧用户反馈集中在 **PII 脱敏不生效、健康检查失败处理、模型/团队配置可在 UI 与 API 间回读** 等使用层问题，存在若干长尾历史 issue 有待处理。


## 2. 版本发布

过去24小时无新版本发布。

> 关联观察：PR #39048 提到 **1.99.0 稳定版发布流水线的全部 6 个 Docker 镜像作业失败**——Wolfi 仓库已将未固定版本的 `python3` 解析为 Python 3.14，而 uvloop 0.21.0 尚无 3.14 wheel，导致 sdist 构建失败。该 PR 正在将修复（`#38917`）cherry-pick 到 `rc/1.99.0` 分支。这解释了为何今日未见新版本产出，预计修复合并后将重新触发发布流水线。

- PR #39048: [fix(docker): pin apk python to 3.13 on rc/1.99.0 (cherry-pick #38917)](https://github.com/BerriAI/litellm/pull/39048)


## 3. 项目进展

今日合并/关闭的 PR 反映了团队在**代理稳健性**和**UI/API 一致性**两条主线的持续收敛：

### 已合并/关闭

- **无效虚拟密钥日志降噪（双 PR 合并）**：#38712 与 #38641 先后被合并，将畸形虚拟密钥（如 `Bearer undefined`）触发的代理日志从 `ERROR` 降为 `INFO`/`WARNING`（stdout），HTTP 401 响应行为不变。这直接回应了用户对接入方 SDK/浏览器配置错误导致日志刷屏、告警风暴的投诉，是显著的可观测性改进。
  - [#38712](https://github.com/BerriAI/litellm/pull/38712) | [#38641](https://github.com/BerriAI/litellm/pull/38641)

- **UI 凭证保存修复被回滚**：#39047 的修复（保留 LiteLLM Params JSON 中 `litellm_credential_name` 字段）被 #39046 回滚，原因待确认，但 #39005（修复 Add Model 静默丢弃该字段导致 Vertex ADC 降级失败）曾因此被 revert。可能引入了新的回归，需关注后续跟进 PR。
  - [Revert #39046](https://github.com/BerriAI/litellm/pull/39046) | [原修复 #39005（已关闭）](https://github.com/BerriAI/litellm/pull/39005)

### 待合并（关键信号）

- **团队隔离与凭证安全（#38932）**：修复精确部署 ID 绕过团队所有权检查、命名凭证缺失时返回不完整配置，改为 fail-closed。这是企业多租户场景的重要安全加固。
- **团队别名可读性（#39045）**：为 `GET /v2/team/list` 补上 `litellm_model_table` 字段，使团队 `model_aliases` 可被 API 读回。直接闭环了 issue #26312。
- **团队级日志回调接入透传端点（#38979）**：让 Langfuse/Datadog 等团队级回调覆盖 /gemini、/anthropic、/bedrock 等约 20 条透传路由，补齐了可观测性缺口。
- **Rust 桥接层架构拆分**：连续提交 `rust: extract domain-neutral Python interop`（#39026）、`python-bridge: split non-streaming bridge modules`（#39031）、`test(build): validate release wheel contracts`（#39021），显示团队在推进 Rust/Python 桥的模块化与发布质量门禁。

整体来看，项目在**认证与多租户边界、日志噪音治理、透传路由可观测性、构建发布可靠性**四个方向均有明确推进，工程质量导向明显。


## 4. 社区热点

今日讨论最活跃的 Issues/PRs 集中在以下几处：

### Issues

- **[#14516 [已关闭] `output_parse_pii` 设置无效（12 条评论，2 👍）](https://github.com/BerriAI/litellm/issues/14516)**
  用户尝试在 UI、`config.yml`、请求参数三层设置 `output_parse_pii: True`（配合 Presidio），响应中的敏感信息仍被掩码。该问题已关闭并标记 `stale`，但评论数高，说明不少用户关注 PII 脱敏的正确配置方式。

- **[#31555 [开放] 基于马尔可夫决策过程的自适应路由策略功能请求（11 条评论）](https://github.com/BerriAI/litellm/issues/31555)**
  由 `@Tibo2403` 提出，建议引入马尔可夫决策过程，根据实时运维指标持续调整 provider 选择，实现 token 成本套利。这是对路由策略的高级增强需求，反映用户对成本优化的深度诉求。

- **[#34281 [开放] 健康检查应优雅失败（10 条评论）](https://github.com/BerriAI/litellm/issues/34281)**
  用户 `@luckylinux`（HomeLab 场景）报告：当某些主机仅按需上线时，健康检查会硬失败，希望支持优雅降级而非直接不可用。这暴露了 LiteLLM 在不可靠/间歇性基础设施下的适配短板。

- **[#25550 [开放] 模型访问组名称泄露到 `/v1/models` 响应（8 条评论）](https://github.com/BerriAI/litellm/issues/25550)**
  当虚拟密钥的 `models` 字段引用不存在的模型时，`/v1/models` 会返回访问组名称，造成配置信息意外泄露。数据边界问题，涉及安全与正确性。

### PR

- [#39048](https://github.com/BerriAI/litellm/pull/39048)（Docker 构建修复）与 [#39025](https://github.com/BerriAI/litellm/pull/39025)（E2E UI 自动化）是今日新提交中关注度较高的 PR，前者阻塞发版，后者代表工程质量投入。
- [#38932](https://github.com/BerriAI/litellm/pull/38932)（团队范围强制）评论为 0，但从内容看是安全相关重要修复，已纳入上文项目进展讨论。

**核心洞察**：社区讨论热度集中在 **PII 脱敏配置可用性**（需求量大但文档/实现滞后）、**成本优化路由**（高级用户诉求）、**基础设施韧性**（HomeLab/边缘场景）三个方向。


## 5. Bug 与稳定性

按严重程度排列：

### 🔴 严重

- **[#38357：Bedrock Converse/InvokeModel 处理程序完全忽略 `httpx.Response.headers`，`x-amzn-RequestId` 等所有 provider 头部丢失（4 条评论）](https://github.com/BerriAI/litellm/issues/38357)**
  `response._hidden_params["additional_headers"]` 始终为空字典，导致 AWS 请求 ID 等排障关键信息不可用。影响所有 Bedrock 用户的可观测性。暂无对应 fix PR。

- **[#11157（2 条评论，2025-05-26 创建，长期未解决）：Redis 缓存超时导致消息内容泄露到日志](https://github.com/BerriAI/litellm/issues/11157)**
  尽管 `litellm_settings` 已配置隐藏内容，超时异常仍会将完整消息内容写入日志。涉及数据隐私合规，是历史遗留问题，今日仍在更新，值得重视。

### 🟠 回归

- **[#20727：Gemini（vertex_ai）透传在 v1.81.3 停止工作，错误使用默认 fallback（8 条评论）](https://github.com/BerriAI/litellm/issues/20727)**
  v1.81.0→v1.81.3 升级后回归，所有透传集成测试失败。该 issue 已存在数月，今日仍在更新，尚未看到明确的修复 PR。

- **[#29808：`MidStreamFallbackError` 未被重试（vertexAI，5 条评论）](https://github.com/BerriAI/litellm/issues/29808)**
  流式中途限流触发 `MidStreamFallbackError`，但代理未按预期重试 fallback，导致请求失败。影响流式场景的可靠性。

### 🟡 一般

- **[#34281：健康检查硬失败（10 条评论，见上文）](https://github.com/BerriAI/litellm/issues/34281)** — 优雅降级缺失。
- **[#33969：间歇性 `InternalServerError: OpenAIException`（3 条评论）](https://github.com/BerriAI/litellm/issues/33969)** — 偶发连接异常导致重试，需进一步定位根因。
- **[#38358：`request_timeout` 在上游静默不返回首字节时不生效（3 条评论）](https://github.com/BerriAI/litellm/issues/38358)** — 流式请求被接受但永不发送数据时，超时机制失效。
- **[#29005：`streamGenerateContent` 对缺失模型返回 500 而非 404（4 条评论）](https://github.com/BerriAI/litellm/issues/29005)** — 语义错误，影响客户端错误处理。
- **[#25563：缺少每模型 SOCKS5/出站代理支持（5 条评论，6 👍）](https://github.com/BerriAI/litellm/issues/25563)** — 仅支持进程级全局代理，无法满足多出口需求。
- **[#36929：Gemini reasoning 内容泄露到 `output_text` 破坏严格 `json_schema`（3 条评论）](https://github.com/BerriAI/litellm/issues/36929)** — 在 `reasoning.effort=medium|high` 时，思维链内容污染输出，影响结构化输出。

**Fix PR 对应情况**：#34281 暂无对应 PR；#20727 暂无明确 fix；#38357 暂无；#36929 暂无。整体上 bug 修复存在滞后，较多 issue 处于"已报告待处理"状态。


## 6. 功能请求与路线图信号

结合今日更新的 issue 与 PR，以下功能请求值得关注：

### 高潜力（已有配套 PR/开发迹象）

- **团队级功能闭环**：`GET /v2/team/list` 返回 `model_aliases`（PR #39045）、团队级日志回调（PR #38979）、团队范围强制（PR #38932）——三个 PR 同时改善团队管理能力，方向明确，大概率进入下一版本。
- **向量存储/嵌入凭证增强**：Milvus gRPC 搜索支持（PR #39039）、每请求解析嵌入凭证（PR #38936）——显示向量存储集成正在扩展和加固。
- **MCP OpenAPI 规范支持**：PR #38952 支持 YAML OpenAPI 规范加载，补全 MCP 工具接入能力。

### 值得关注（社区呼声高）

- **#31555：Markov 决策过程路由策略**（11 条评论）— 成本套利与自适应路由，目前是纯功能请求，没有 PR，但代表了高级用户对路由优化的未来方向。
- **#25563：每模型 SOCKS5/出站代理**（6 👍）— 多出口网络场景刚需，当前仅环境变量级全局代理，实现跨度较大。
- **#26312（已关闭）/ #39045（PR）**：团队模型别名在 API 中可读回——该功能通过 PR 方式落地，说明团队在系统性地补齐配置回读一致性。
- **#38438：每用户日/月支出阈值 Slack 告警 + 支出异常检测**（devin bot 提交）— 若被接收，将显著增强企业级成本管控能力。
- **#31649：OpenAI Workload Identity Federation（OIDC token exchange）支持**（已关闭）— 以关闭告终，可能已被内部处理或以其他形式推进。

### 信号解读

项目近期路线图信号明确：**团队级治理与权限边界**和**代理层可观测性**是两个主攻方向；**向量存储集成**在扩容；**Rust 桥接

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-09-01

## 1. 今日速览

过去24小时内，Temporal 项目保持中等偏高的开发活跃度：PR 更新达 51 条（其中 15 条已合并/关闭，36 条仍在待合并状态），显示核心团队与社区贡献者的提交节奏稳定。Issues 侧更新较少（仅 2 条），但其中包含一条新提交的潜在严重 bug（调度器静默停止触发），需关注。此外，今日无新版本发布，项目当前处于常规迭代周期。

---

## 3. 项目进展

过去24小时共有 15 条 PR 被合并/关闭，以下为关键变更：

**🚀 合并/关闭的重要 PR**

- **[#11829] [reliability-2026, release/1.32.0] Visibility Elasticsearch 分页 token 修复** — 当结果集大小小于 page size 时返回空 page token，部分回滚 #10540 的改动。此修复进入 1.32.0 发布分支，解决了因始终返回分页 token 导致的非必要查询开销问题。
  https://github.com/temporalio/temporal/pull/11829

- **[#11757] [reliability-2026] 按生命周期阶段标记 Nexus 日志** — 为 Nexus 相关日志增加 `nexus-stage` 标签，方便运维人员区分 Nexus 生命周期中的具体环节（如任务投递、回调等），并通过 RequestID 跨阶段关联日志。
  https://github.com/temporalio/temporal/pull/11757

- **[#10723] version clamp 3155** 与 **[#10683] scheduler ceiling WIP** — 两条由 @liam-lowe 提交的 PR 于今日关闭（具体内容为空/草稿状态），推测为无效或已废弃的变更，可能被内部清理。

**📊 活跃 PR（仍在推进中）**

- **[#11868] 修复 late parent replication 后的子流程完成恢复** — 处理父流程 StartChildExecution 任务在复制延迟后重新生成时，子流程已关闭的场景，当前正在代码审查阶段。
  https://github.com/temporalio/temporal/pull/11868

- **[#11880] 修复调度器迁移数据转换** — 针对 V1 调度器迁移到 CHASM 过程中的已完成动作时间戳、上次完成结果以及自定义 memo 字段的数据丢失/错误问题提出修复。
  https://github.com/temporalio/temporal/pull/11880

- **[#11878] 在 V1 迁移期间保留 fresh backfill 边界** — 确保从 CHASM 回滚到 V1 调度器时，backfill 范围不被错误重置。
  https://github.com/temporalio/temporal/pull/11878

**📌 小结**：项目整体在可靠性工程（reliability-2026）方向的投入明显，包括日志可观测性、Elasticsearch 查询语义修正、调度器迁移数据完整性等。此外，多个历史遗留 PR（如 #10723）被清理关闭，反映出维护者在积极治理积压。

---

## 4. 社区热点

过去24小时讨论最集中的议题包括：

**🔥 [#11869] 调度器静默停止触发 — 潜在严重 Bug**
- 作者 @odoucet 报告：Temporal Server 1.31.0，PostgreSQL/Elasticsearch，512 个 history shards，约 32 个 schedule 运行在 v1 workflow-backed 调度器上。调度器 workflow 中存在一个 pending timer，但没有对应的物理 timer task，导致调度静默停止触发。
- 诉求：这是一个生产环境可靠性问题，用户对调度器“无声失败”表达了担忧，期望尽快定位根因并提供修复。
- 链接：https://github.com/temporalio/temporal/issues/11869

**🔥 [#10095] Mutation testing tool [WiP] — 长期开放的大型 PR**
- 作者 @stephanos 提交的变异测试工具已开放逾 4 个月（2026-04-28 创建），今日仍在更新。该工具旨在通过变异测试提高 Temporal 核心代码的测试质量，属基础质量建设类工作，讨论热度集中在“何时能合并”以及测试覆盖率提升的具体预期。
- 链接：https://github.com/temporalio/temporal/pull/10095

**📈 分析**：今日社区热点集中在**调度器可靠性**与**测试基础设施**两大主题，前者直接关系到生产用户对 Temporal 的信任度，后者反映项目长期健康度投资。

---

## 5. Bug 与稳定性

按严重程度排序：

**🔴 高 — 调度器静默停止触发**
- Issue #11869：scheduler workflow 保留了一个 pending timer，但物理 timer task 不存在，导致调度停止且无报错。影响所有 v1 workflow-backed 调度器用户。目前**暂无直接 fix PR**，但 #11880 与 #11878 修复的调度器迁移数据问题可能有关联，建议维护者调查是否同一根因。
- 报告版本：Temporal Server 1.31.0 | PostgreSQL | Elasticsearch
- 链接：https://github.com/temporalio/temporal/issues/11869

**🟡 中 — SignalWithStart 绕过 continue-as-new backoff**
- PR #11810（修复中）：SignalWithStart 在工作流发起 continue-as-new 后未尊重首次 workflow task 的 backoff，导致信号立即触发任务执行。修复方案：信号立即记录，但 workflow task 等待 backoff 到期后再调度；同时保留初始工作流启动时的现有行为。
- 链接：https://github.com/temporalio/temporal/pull/11810

**🟡 中 — 调度器迁移数据转换错误**
- PR #11880：V1 调度器迁移到 CHASM 时，已完成动作的时间戳（ScheduleTime）被破坏、last-completion 结果丢失、自定义 memo 字段转换异常。修复中。
- 链接：https://github.com/temporalio/temporal/pull/11880

**🟡 中 — 父流程复制延迟后子流程完成恢复失败**
- PR #11868：当 active Parent 的 StartChildExecution 任务因 late replication 重新生成时，若子流程已关闭，当前逻辑无法正确恢复。修复中（通过 GetMutableState 重新解析子流程当前 run）。
- 链接：https://github.com/temporalio/temporal/pull/11868

**🟢 低/已修复 — 其他已解决项**
- Visibility Elasticsearch 分页 token 非必要返回（#11829，已合并至 1.32.0）
- Retry jitter 被截断为 no-op（#11397，修复 PR 开放中）
- ResourceExhausted 错误缺少显式 Scope（#11036，修复 PR 开放中）
- Post-close signal requestID 清理需求（#4029，功能请求/讨论中）

---

## 6. 功能请求与路线图信号

**📌 可能被纳入后续版本的功能/改进：**

- **[#4029] 工作流关闭后清理 signal requestID**（enhancement, up-for-grabs）
  - 请求：工作流关闭后，所有 signal 请求都会被拒绝，用于去重的 signal requestID 不再需要，应被清理以节省存储。
  - 状态：开放中，欢迎社区贡献。该议题已存在较久，属资源优化类改进，可能随存储优化相关工作被纳入。
  - 链接：https://github.com/temporalio/temporal/issues/4029

- **[#9626] JWT claim mapper 支持嵌套 claim 键**（stale）
  - 请求：在 `PermissionsClaimName` 的查询中支持 JMESPath 以读取嵌套 JWT claim。由于 PR 被标记为 stale，需要维护者明确是否仍计划合入。
  - 链接：https://github.com/temporalio/temporal/pull/9626

- **[#11355] 保留 logger tags 跨 Skip()**（可用性改进）
  - 变更：`zapLogger.Skip()` 现在会将已有 tags 传递到返回的 clone，与 `baseZl` 字段行为一致。这对使用 throttle logger 的场景（如限制日志频率时保留 service 标签）有价值。
  - 链接：https://github.com/temporalio/temporal/pull/11355

- **[#11397] 修复 retry jitter 未生效的问题**
  - 变更：`addJitter` 函数在 `common/backoff/retrypolicy.go` 中始终未真正应用 jitter，修复后 2s base + 10% jitter 将产生 2.0s–2.2s 的随机延迟。这属于避开 thundering herd 的关键基础设施修复。
  - 链接：https://github.com/temporalio/temporal/pull/11397

---

## 7. 用户反馈摘要

**🗣️ 来自 Issue 评论与 PR 讨论的真实用户声音：**

- **调度器静默失败是最令人不安的问题**（#11869）：报告者 @odoucet 详细描述了生产环境现象——调度器无任何日志错误却停止触发，且“pending timer 无对应物理任务”的状态让人难以排查。该类问题的核心诉求是**可观测性**：用户期望在调度器异常时得到明确告警而非静默降级。

- **社区对 AI 辅助代码审查的接受度**（#11852）：@chrsmith 在 PR 描述中直接说明“I had the AI rewrite the changes to make them easier to review”，反映部分贡献者已开始使用 AI 工具辅助重构以提升可读性，社区对此持开放态度。

- **测试基础设施一致性的呼声**（#11879）：@cbsandeep10 将 matching 测试的内存 TaskManager 替换为 SQLite，理由是“store semantics（CAS、GC、metadata）必须与生产环境一致”，间接反映了用户对测试有效性的关注。

---

## 8. 待处理积压

**⚠️ 长期未响应的 Issue/PR，建议维护者关注：**

| 项目 | 创建时间 | 最后更新 | 状态 | 说明 |
|------|---------|---------|------|------|
| [#10095] Mutation testing tool [WiP] | 2026-04-28 | 2026-09-01 | OPEN | 变异测试工具，开放超 4 个月仍为 WiP，需要明确进展与合入计划 |
| [#9626] jwt_claim_mapper: allow nested claim keys | 2026-03-23 | 2026-09-01 | OPEN（stale） | 被标记为 stale，功能需求明确（JMESPath 支持嵌套 claim），需要决定是否推进 |
| [#4029] Clear signal requestID on workflow close | 2023-03-08 | 2026-08-31 | OPEN | 已开放超 3 年，标记为 up-for-grabs，可考虑纳入社区贡献引导清单 |
| [#11036] Set explicit scope on ResourceExhausted errors | 2026-07-13 | 2026-08-31 | OPEN | 修复推进中但未被合并，建议确认 reviewer 进度 |

**重点关注**：#11869 作为新提交的高影响 bug，建议尽快分配至调度器模块维护者，并与 #11880、#11878 关联排查。

---

*本日报由 AI 助手根据 Temporal GitHub 仓库公开数据自动生成，数据截至 2026-09-01。*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*