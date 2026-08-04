# OpenClaw 生态日报 2026-08-05

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-04 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-05

## 1. 今日速览

OpenClaw 项目在过去 24 小时内保持极高活跃度：共有 500 条 Issue 更新（其中新开/活跃 448 条，关闭 52 条）和 500 条 PR 更新（其中待合并 387 条，已合并/关闭 113 条），新增 2 个修复版本（v2026.7.1-1、v2026.7.1-2）。值得注意的是，多个 P1 级高优先级问题（包括 DeepSeek v4 Flash 静默失败、Gateway 主线程饱和、会话状态卡死等）已经积累了很高的社区关注度，其中 #116277 评论数高达 104 条，反映用户对消息可靠性和会话稳定性的诉求强烈。同时，维护者（maintainer）标记的 PR 在持续增多，QA/审计类基础设施 PR 占比高，说明项目在追求功能迭代的同时也在系统性加固质量保障体系。

- **Issue 更新**：500 条（新开/活跃 448，已关闭 52）
- **PR 更新**：500 条（待合并 387，已合并/关闭 113）
- **新版本发布**：2 个

## 2. 版本发布

### v2026.7.1-2 — openclaw 2026.7.1-2
- **修复内容**：npm 插件更新机制——接受新版 npm 客户端产生的单例数组元数据，确保受追踪的官方插件能够正常安装并更新到修复版本。（[#108336](https://github.com/openclaw/openclaw/issues/108336)）

### v2026.7.1-1 — openclaw 2026.7.1-1
- **修复内容**：
  - **Codex 进度回复**：保持 app-server 轮次在发送进度消息后继续运行，使 GPT/Codex 能够到达其权威的最终回复，而不是中途停止。（[#106961](https://github.com/openclaw/openclaw/issues/106961)、[#108487](https://github.com/openclaw/openclaw/issues/108487)，感谢 @joshavant）
  - **Memory Core 启动修复**：恢复派生的旧版索引和缓存修复逻辑（描述被截断）。

> **迁移注意事项**：两个版本均为修复性发布，无破坏性变更提示。建议所有 2026.7.x 用户跟进更新至 v2026.7.1-2，特别是使用 npm 插件机制和 Codex 集成的用户。

## 3. 项目进展

过去 24 小时有 113 个 PR 被合并或关闭。以下亮点 PR 标记为 **"ready for maintainer look"** 且已有充分验证，表明接近合并或已进入合并队列：

### 核心稳定性与安全修复
- **[fix(commands): restore tool inventory for dynamic models](https://github.com/openclaw/openclaw/pull/119306)**（#119306，@vincentkoc）：修复动态提供商会话中 `/tools` 命令可能出现的临时清单元效问题，Beta 8 发布通道中也被复现。维护者标记，自动化合并风险。

- **[fix(fs): adopt fs-safe 0.5.2 untrusted filename sanitization](https://github.com/openclaw/openclaw/pull/119363)**（#119363，@steipete）：采纳 `@openclaw/fs-safe` 0.5.2 的不受信任文件名净化能力，剥离 Windows 非法字符（`<>:"|?*`、C1 控制符）并为 Windows 保留名（`CON`、`AUX` 等）加下划线后缀。对跨平台安全一致性意义重要。

- **[fix: prevent denied MCP tools from reaching native agent runs](https://github.com/openclaw/openclaw/pull/119364)**（#119364，@joshavant，关闭 #119310）：修复了直接传递给原生 Claude、Codex 和 Gemini 客户端的 MCP 服务器绕过 OpenClaw 完整的 `tools.allow` / `tools.deny` 分层过滤的问题。这是一项重要的安全边界修复。

### 通道与消息可靠性
- **[fix(slack): preserve channel context in bot-opened threads](https://github.com/openclaw/openclaw/pull/119023)**（#119023，@scootscooob）：修复了用户在频道中启动 Slack 对话后，agent 打开回复线程时丢失频道上下文的问题。

- **[fix(imessage): thread replies with thread_originator_guid](https://github.com/openclaw/openclaw/pull/119289)**（#119289，@dkattan）：修复 iMessage 回复线程化问题，确保 OpenClaw 的回复在 Messages.app 中正确显示为线程回复。P1，需进一步验证。

### 质量保障体系
- **[fix(qa): repair release validation scenarios](https://github.com/openclaw/openclaw/pull/119150)**（#119150，@vincentkoc）：修复发布验证场景中的确定性测试基础设施失败，包括 provider-native 工具标识分歧、compaction 对真实 Code Mode 执行结果类型的假设等问题。

- **[chore(qa): cover doctor CLI recovery paths](https://github.com/openclaw/openclaw/pull/118926)**（#118926，@vincentkoc）：为 `doctor` 命令的网关认证检查、外部端口诊断、systemd 启动限制引导等路径新增 QA 场景覆盖。

### UI/UX 修复
- **[fix(ui): clear split-pane questions after answers and cancellations](https://github.com/openclaw/openclaw/pull/118787)**（#118787，@steipete）：修复用户在 Control UI 中回答/取消问题后可能卡在等待指示器和禁用聊天面板的问题。P1，diamond lobster 评级。

- **[fix(ui): restore settings search, media previews, clipboard, and native chat](https://github.com/openclaw/openclaw/pull/116654)**（#116654，@steipete）：修复 Control UI 设置搜索缺失元组字段、签名媒体 URL 丢失媒体类型、剪贴板状态回退、原生聊天/语音将非文本事件块视为文本等问题。

**整体判断**：项目正在从功能扩张阶段转向稳定性加固阶段。安全边界（MCP 工具过滤）、跨平台一致性（Windows 文件名净化）、长期存在的 UI 状态问题都在系统性地被解决。QA 自动化投入显著增加，预示着未来发布节奏可能会更快且更稳。

## 4. 社区热点

### 讨论热度最高

| Issue/PR | 评论数 | 核心主题 |
|----------|--------|----------|
| [#116277 DeepSeek v4 Flash 静默回复失败](https://github.com/openclaw/openclaw/issues/116277) | 104 | 模型静默失败，仅回退到通用错误消息，影响 Telegram 群组消息 |
| [#116201 Realtime voice 会话状态无限增长](https://github.com/openclaw/openclaw/issues/116201) | 58 | Realtime voice 会话在慢/停滞/突发 provider 行为下保留超限的咨询工作、大帧等 |
| [#115326 崩溃循环抑制器永久压制 Discord/WhatsApp](https://github.com/openclaw/openclaw/issues/115326) | 25 | 崩溃循环断路器永久抑制通道，文档化恢复路径（channels.start）失败 |
| [#118846 Gateway 主线程被插件元数据快照饱和](https://github.com/openclaw/openclaw/issues/118846) | 14 | 主线程 100% 占用，本地 RPC 在 ws_upgrade 处死亡（1006） |
| [#43367 多智能体编排不稳定](https://github.com/openclaw/openclaw/issues/43367) | 13 | 并发 agent 配置互相覆盖、会话锁失败、子任务脱离 |

### 热点诉求分析

**1. 消息静默丢失/失败是最响亮的社区呼声。** #116277（DeepSeek v4 Flash 静默失败）以 104 条评论遥遥领先，核心痛点在于模型失败后只有一条冷冰冰的 fallback 消息，用户完全不知道发生了什么。这一问题的深层诉求是**透明性**——失败时应当告知原因、可重试、可诊断。

**2. Realtime voice 的资源治理缺位。** #116201 讨论的 unbounded state 保留问题暴露了 Realtime voice 功能在资源上限设计上的不足，社区在等待一个明确的 ownership 边界模型。

**3. 恢复路径的可靠性。** #115326 中用户遵循文档执行 `channels.start` 却得到 WebSocket 1006 错误，文档给出的恢复路径本身不可用——这是比 bug 本身更伤害信任的问题。

**4. 主线程健康。** #118846 指向插件元数据快照导致的主线程 100% 饱和，说明插件体系的性能开销开始成为 gateway 稳定性的瓶颈。

## 5. Bug 与稳定性

### 🔴 P1 级严重问题（消息丢失/崩溃类）

| Issue | 问题 | 状态 | Fix PR |
|-------|------|------|--------|
| [#116277 DeepSeek v4 Flash 静默回复失败](https://github.com/openclaw/openclaw/issues/116277) | 模型静默失败，仅产生通用 fallback，影响 Telegram 群消息 | CLOSED | 已有关联 PR |
| [#118846 Gateway 主线程饱���](https://github.com/openclaw/openclaw/issues/118846) | 插件元数据快照 + fs statting 使主线程 100%，本地 RPC 死掉（ws_upgrade 1006） | OPEN | 无 |
| [#115908 会话转录投影 livelock](https://github.com/openclaw/openclaw/issues/115908) | 持续写入下转录投影进入非收敛重建循环，阻塞主线程数十秒 | OPEN | 无 |
| [#119263 Agent DB v14→v15 迁移失败](https://github.com/openclaw/openclaw/issues/119263) | `no such column: entry_valid`，迁移回滚，gateway 拒绝启动 | OPEN | 已有 linked PR |
| [#115326 崩溃循环断路器永久抑制 Discord/WhatsApp](https://github.com/openclaw/openclaw/issues/115326) | 通道被永久压制，`channels.start` 恢复失败（WS 1006） | CLOSED | 无（需验证） |
| [#89278 Codex OAuth 刷新超时](https://github.com/openclaw/openclaw/issues/89278) | OAuth 刷新成功但 cron/heartbeat 10s 超时失败 | OPEN | 无 |
| [#72015 active-memory 阻塞回复 + QMD 启动过载](https://github.com/openclaw/openclaw/issues/72015) | 多 agent gateway 上启用 active-memory 导致回复慢/不可靠 | OPEN | 无 |

### 🟡 P2 级问题

- **[#116010 所有持久会话被限制在 128k 上下文](https://github.com/openclaw/openclaw/issues/116010)**：无论模型或配置的 contextTokens 如何设置，持久会话始终被截断在 128k。已有 linked PR。
- **[#115700 chat.send 报 "thread switched branches"](https://github.com/openclaw/openclaw/issues/115700)**：模型完成（尤其内部重试/回退/压缩后）`expectedLeafEntryId` 过期导致后续 send 被拒。已有 linked PR。
- **[#97616 子进程泄漏导致僵尸进程堆积](https://github.com/openclaw/openclaw/issues/97616)**：hook/tool 执行后子进程未回收，运行时性能退化。

### 稳定性观察

- **新出现的迁移问题**（#119263）值得警惕：v14→v15 数据库迁移失败阻止 gateway 启动，对升级路径影响严重，且是昨天刚报告的新问题。
- **会话状态类问题集中**：`session-state` 标签在多条高热度 issue 中反复出现（#115908、#116010、#115700、#111498），说明会话持久化与并发控制是需要优先投入的方向。

## 6. 功能请求与路线图信号

### 高潜力功能请求

| Issue | 功能 | 信号强度 |
|-------|------|----------|
| [#45508 自托管 STT/TTS 支持（webchat 路由到 gateway）](https://github.com/openclaw/openclaw/issues/45508) | webchat 的"朗读"按钮和语音输入走 OpenClaw 配置的 TTS/STT 提供商而非浏览器 Web Speech API | ⭐⭐⭐⭐⭐ 评论 7，👍 2，diamond lobster |
| [#9016 向 agent 运行时暴露 OpenRouter 使用成本](https://github.com/openclaw/openclaw/issues/9016) | 按消息跟踪 OpenRouter 成本并让 agent 可附加到回复中 | ⭐⭐⭐⭐ 评论 7，👍 1 |
| [#71736 Control UI 插件贡献槽位（RFC）](https://github.com/openclaw/openclaw/issues/71736) | 数据驱动的插件 UI 贡献点：聊天模式、审批卡片、事件分类器、输入守卫等 | ⭐⭐⭐⭐ 评论 9，👍 1，needs-security-review |
| [#45771 内置 pace-aware 限流](https://github.com/openclaw/openclaw/issues/45771) | 自主 agent 循环中跟踪消费速率

---

## 横向生态对比

# AI 智能体开源生态横向对比分析报告
**日期：2026-08-05**

---

## 1. 生态全景

个人 AI 助手与自主智能体开源生态正处于**“功能竞争转向稳定与安全竞争”**的关键阶段。以 OpenClaw 为代表的高活跃项目，单日处理 500 条 Issue/PR 并发布 2 个修复版本，社区诉求高度集中在消息可靠性、会话稳定性与安全保障上；同时，以 OpenHands SDK 为代表的开发者基础设施类项目，正围绕可观测性、扩展安全架构等深水区精耕细作。多项目不约而同地投入可观测性、安全边界、插件治理等方向，说明生态正由“能做什么”向“能否可靠、安全地规模化运行”演进。整体上，头部项目已具备庞大的社区基础与健全的 QA 体系，行业正在走向成熟。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | Release | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 500（新开/活跃 448，关闭 52） | 500（待合并 387，已合并/关闭 113） | 2 个修复版（v2026.7.1-1 / -2） | ★★★★★ 极高活跃，QA 与安全加固并行，但 P1 问题较多，存在稳定性压力 |
| **OpenHands SDK** | 19（活跃 16，关闭 3） | 50（待合并 45，已合并/关闭 5） | 无 | ★★★★☆ 较高活跃，可观测性修复闭环速度快，安全设计系列推进中 |
| **Hermes Agent** | 无当日动态 | 无当日动态 | 无 | 数据不足，无法评估 |
| **Pi** | 无当日动态 | 无当日动态 | 无 | 数据不足，无法评估 |
| **LiteLLM** | 无当日动态 | 无当日动态 | 无 | 数据不足，无法评估 |
| **Temporal** | 无当日动态 | 无当日动态 | 无 | 数据不足，无法评估 |

> 注：后四个项目在本次摘要中未提供动态信息，下文不做横向推断。

---

## 3. OpenClaw 在生态中的定位

OpenClaw 是**个人 AI 助手 / 自主智能体框架**领域的头部项目，与 OpenHands SDK 相比，二者并非直接竞品，而是生态中的互补层：

- **优势**：
  - **社区规模与迭代速度断层领先**：单日 500 条 Issue + 500 条 PR，远超 OpenHands SDK（19/50），反映出庞大的用户基数和极高的问题反馈密度。
  - **全渠道集成深度**：覆盖 Telegram、Slack、iMessage、Discord、WhatsApp、Web 等多通道，且已在处理各通道的具体可靠性问题（如 Slack 线程上下文、iMessage 线程回复），说明其作为“个人助手中枢”的定位已深入真实场景。
  - **多模型供应商接入**：支持 Claude、Codex、Gemini、DeepSeek 等多种模型，并针对各模型的异常行为（如 DeepSeek 静默失败、Codex OAuth 超时）进行专项修复。

- **技术路线差异**：
  - OpenClaw 走**一体化全家桶**路线，将聊天、语音、自动化、插件、控制 UI 集成于同一框架；OpenHands SDK 则走**模块化 SDK** 路线，提供底层构建模块供开发者嵌入自己的产品。
  - OpenClaw 的 bug 分布显示其复杂度已相当高（数据库迁移、主线程饱和、崩溃断路器），正在从“功能加法”转向“稳定性治理”；OpenHands SDK 同样在安全与可观测性上加大投入，但处于更早期的功能成型阶段。

- **社区规模对比**：OpenClaw 的 Issue/PR 流量是 OpenHands SDK 的 10 倍以上，且维护者响应密集（当日 113 个 PR 被合并/关闭），属于生态中的“超级活跃项目”；OpenHands SDK 则更像一个快速成长的开发者生态，协作健康度良好但规模尚小。

---

## 4. 共同关注的技术方向

多个项目在同一时间段涌现出相似的技术需求，这往往代表了生态层面的共性痛点：

| 方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **安全边界与权限隔离** | OpenClaw、OpenHands SDK | OpenClaw 修复 MCP 工具绕过 allow/deny 过滤、Windows 非法文件名净化；OpenHands SDK 为 Canvas Extensions 设计路径穿越防护、CSRF 确认、API 权限字段等安全基线 |
| **可观测性与 trace 质量** | OpenHands SDK（明确）、OpenClaw（质量保障体系） | OpenHands 修复 TOOL span 丢失父级、工具 LLM 调用泄漏进 trace、ACP 对话不可见；OpenClaw 增加 QA/审计类 PR 占比，强调发布验证与 doctor 诊断 |
| **会话状态管理与持久化** | OpenClaw | 会话状态卡死、上下文被截断在 128k、数据库迁移失败、线程分支冲突——集中反映持久化与会话并发控制的脆弱性 |
| **插件系统的稳定性治理** | OpenClaw、OpenHands SDK | OpenClaw 插件元数据快照导致主线程饱和、npm 插件更新机制修复；OpenHands SDK 的 Canvas Extensions 需要安装原子性、版本固定、审计日志 |
| **消息可靠性与透明性** | OpenClaw | 用户强烈要求“静默失败”不再发生：需要明确失败原因、可重试、可诊断 |
| **本地/自托管模型集成** | OpenHands SDK | ACP + ollama 本地配置下 agent-server 无响应，说明本地模型链路仍是痛点 |

---

## 5. 差异化定位分析

| 维度 | OpenClaw | OpenHands SDK |
|---|---|---|
| **功能侧重** | 完整的个人 AI 助手：多渠道收发消息、语音、自动化、插件、控制 UI、多模型路由 | 面向软件 agent 的构建工具包：MCP 工具管理、ACP、可观测性、Canvas 扩展、子代理任务 |
| **目标用户** | 希望拥有“个人 AI 助理”的终端用户/极客，以及需要集成多消息渠道的团队 | 开发 agent 产品的工程师/ISV，需要将 agent 能力嵌入自有软件 |
| **技术架构** | 单体应用 + gateway 进程 + 插件体系，侧重运行时稳定与跨平台一致性 | SDK 形态，强调模块化、可编程性、与外部协议（ACP、MCP、FastMCP）的兼容 |
| **生态位置** | 更接近消费者级/个人生产力工具 | 更接近 B2D（开发者基础设施） |
| **当前痛点** | 体量大带来的复杂系统熵增（迁移失败、主线程饱和、通道崩溃抑制器误伤） | 功能尚未完全成熟，扩展安全、可观测性、本地模型链路仍在校验中 |

---

## 6. 社区热度与成熟度

- **第一梯队：极速迭代 + 质量巩固并举**
  - **OpenClaw** 处于典型的“大规模复杂项目”阶段：功能扩张速度依然很快，但已开始系统性加固 QA（发布验证、doctor 恢复路径测试）和安全边界（MCP 过滤、文件名净化）。同日发布两个修复版本，体现其快速响应用户问题的能力。
  - **OpenHands SDK** 处于“功能密集落地 + 安全前置设计”阶段：可观测性 bug 当日修复闭环，同时以 10 个 issue 系统设计 Canvas Extensions 的安全架构，显示其功能建设仍有很大空间。

- **第二梯队：数据不足**
  - Hermes Agent、Pi、LiteLLM、Temporal 在本次摘要中无动态，无法评估。根据历史定位，LiteLLM 与 Temporal 属于相对稳定、迭代节奏平稳的基础设施项目；Hermes、Pi 为新兴的智能体框架/个人助手项目，仍需更多数据。

---

## 7. 值得关注的趋势信号

1. **“静默失败”容忍度趋于零**  
   OpenClaw 的高热度 issue（DeepSeek 静默失败，104 条评论）表明：用户可接受失败，但不可接受没有原因、无重试路径、无法诊断的失败。未来 agent 框架必须内置失败透明机制——错误原因、重试建议、诊断信息缺一不可。

2. **可观测性成为 agent 基础设施的“刚需”**  
   OpenHands SDK 在可观测性上密集投入（trace 上下文、LLM 调用标记），说明 agent 的生命周期调试比传统软件更复杂。没有高质量的 trace，就无法定位多 agent、并行工具调用、子任务归属等问题。这对所有 agent 开发者都是一个提醒：**可观测性不能后期补，必须从架构设计期开始考虑**。

3. **插件/扩展系统的“安全前置”成为行业惯例**  
   OpenClaw 在文件系统层做安全净化，OpenHands SDK 在扩展安装层做路径穿越防护、原子交换和模糊测试——两者逻辑一致：**扩展能力越强，安全门槛越高**。未来的 agent 扩展生态若要健康发展，必须默认安全，而非事后补丁。

4. **本地/自托管模型链路仍是短板**  
   OpenHands SDK 中 ACP + ollama 配置故障持续三周未解决，OpenClaw 也有自托管 STT/TTS 的高潜力需求。个人 AI 助手的用户越来越希望摆脱云端依赖，但本地模型工具链的成熟度依旧不足。这既是痛点，也是新的机会窗口。

5. **数据库迁移与升级路径是“隐形杀手”**  
   OpenClaw 的 v14→v15 迁移失败会直接阻止 gateway 启动，属于升级场景中的致命错误。项目在功能高速迭代时，必须把迁移测试纳入发布强制门槛，否则会快速消耗用户信任。

6. **“上下文管理”范式正在重新定义**  
   OpenClaw 的持久会话被限制在 128k、线程分支冲突等问题，本质上是 agent 上下文模型尚不成熟的表现。如何高效、经济地管理长会话、子任务和并发上下文，仍是下一代 agent 框架的核心技术挑战。

---

> **一句话总结**：个人 AI 智能体生态已跨越“可用”门槛，当前竞争焦点是**可靠性、安全性与可观测性**；OpenClaw 是社区规模最大的集成型选手，OpenHands SDK 是快速崛起的开发者基础设施，两者的不同路径共同指向同一个未来——**agent 必须既能干，又可信、可查、可修**。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-08-05

## 1. 今日速览

过去 24 小时项目保持高速迭代，共产生 **19 条 Issue 更新**（活跃 16 / 关闭 3）和 **50 条 PR 更新**（待合并 45 / 已合并关闭 5），无新版本发布。**Canvas Extensions 安全架构系列**（#4348–#4357）成为绝对主线，围绕扩展安装安全、REST API、持久化与测试矩阵展开系统性设计；**可观测性修复**取得实质进展，2 个相关 PR（#4359、#4360）已合并且 Issue #4358 关闭；**MCP 领域**持续活跃，涉及动态工具快照（#4367，已合入）及后续修复（#4369）。整体看，项目正处于功能密集落地与安全加固并行阶段，维护者响应速度快，协作健康度良好。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日共 **5 条 PR 被合并/关闭**，主要集中在可观测性修复、MCP 能力增强和依赖升级：

| PR | 类型 | 说明 |
|---|---|---|
| [#4359](https://github.com/OpenHands/software-agent-sdk/pull/4359) | 可观测性 | 为 `generate_title` / `ask_agent` 等工具 LLM 调用添加元数据标记，使其在 Laminar 中不再与常规 agent 输出混淆，直接修复 #4358 的一半问题 |
| [#4360](https://github.com/OpenHands/software-agent-sdk/pull/4360) | 可观测性 | 放弃依赖 lmnr 库传播 trace context，改为在并行工具调用时显式传递上下文，修复 TOOL span 在并行执行场景下丢失父级的问题（#4358 的另一半） |
| [#4367](https://github.com/OpenHands/software-agent-sdk/pull/4367) | MCP | 支持动态更新 agent 工具快照（reconcile），经 FastMCP streamable-HTTP 集成测试验证，使 SDK 的 MCP 工具管理能力对齐 OpenCode |
| [#4366](https://github.com/OpenHands/software-agent-sdk/pull/4366) | 基础设施 | 为 SDK 子进程设置 `AI_AGENT` 环境变量，与行业趋势对齐，便于子进程识别自身运行环境 |
| [#4312](https://github.com/OpenHands/software-agent-sdk/pull/4312) | 依赖 | 将 aiohttp 从 3.13.4 升级至 3.14.3（Dependabot 自动更新） |

其中 **#4359 与 #4360 的合入**直接呼应了昨日 open 的 #4358（可观测性 bug），一天内完成从问题发现到修复合入的闭环，体现了较强的迭代效率。此外 #4367 的合入引入了新的回归问题，已由 #4369 跟进修复（见 Bug 部分）。

---

## 4. 社区热点

### 4.1 Canvas Extensions 安全设计系列（今日最密集讨论）

由 @VascoSch92 主导，一口气提出 **#4348–#4357 共 10 个 Issue**，从不同维度拆解 Canvas 扩展机制的安全落地：

- [#4348](https://github.com/OpenHands/software-agent-sdk/issues/4348) manifest 模型与校验、入口点路径包含检查（路径穿越/符号链接逃逸）
- [#4350](https://github.com/OpenHands/software-agent-sdk/issues/4350) 安装持久化：修复 disabled-by-default 与自愈自动启用问题
- [#4351](https://github.com/OpenHands/software-agent-sdk/issues/4351) 分阶段安装 + 原子交换 + 两阶段刷新（check/apply）
- [#4352](https://github.com/OpenHands/software-agent-sdk/issues/4352) REST API 表面设计
- [#4353](https://github.com/OpenHands/software-agent-sdk/issues/4353) Phase 1 测试矩阵
- [#4354](https://github.com/OpenHands/software-agent-sdk/issues/4354) OpenAPI spec 与 TypeScript client 发布
- [#4355](https://github.com/OpenHands/software-agent-sdk/issues/4355) 审计日志 + `agentServer.request` 遥测
- [#4356](https://github.com/OpenHands/software-agent-sdk/issues/4356) manifest API-scope 字段 + CSRF 确认 + 保留名称
- [#4357](https://github.com/OpenHands/software-agent-sdk/issues/4357) 对抗性模糊测试（受 #4353 阻塞）
- [#4349](https://github.com/OpenHands/software-agent-sdk/issues/4349) 安装记录增加 `requested_ref` 字段

**诉求分析**：这一系列 Issue 表明项目正在为 Canvas Extensions 设计一套**生产级安全基线**——从安装原子性（防中断损坏）、路径逃逸防护（防恶意扩展）、到审计追溯（防滥用）。其中多个 Issue 标注 `security` 或 `priority:high`，说明安全是核心关注点。这类一次性拆解多个相关 Issue 的方式也便于并行开发和独立追踪，是大型功能落地的健康信号。核心冲突点在于：**扩展带来的灵活性 vs. 沙箱安全**——例如 #4350 中 `enabled` 默认值的反复，以及 #4351 中对刷新机制拆分 check/apply 两阶段的设计，都体现了这一张力。

### 4.2 #4267 — ACP 本地自动化配置故障（最热 Bug 讨论，5 条评论）

[#4267](https://github.com/OpenHands/software-agent-sdk/issues/4267)（7 月 12 日创建，昨日更新）：用户 @azcoffeehabit 在 agent-canvas 中通过本地 ACP + opencode + ollama 配置 GitHub 仓库监控自动化时遭遇 `agent-server` 无响应。该 issue 持续 3 周仍为 open 状态，真实反映本地 LLM 工具链集成的不顺畅，评论区可能有配置指导或复现信息。

### 4.3 #1317 — 交互式 vs 非交互式 Agent 默认提示词（已关闭，6 条评论）

[#1317](https://github.com/OpenHands/software-agent-sdk/issues/1317)（2025 年 12 月创建，昨日关闭）：讨论 CLI 用户等待 agent 完成任务时，过于冗长的输出令人沮丧；而云端应用用户可多任务等待，详尽输出更可接受。该 issue 作为行为倡议（behavior-initiative）被标记 stale 后关闭，但其背后的产品思考（不同使用场景需要不同的 verbosity 策略）可能已融入后续设计。

---

## 5. Bug 与稳定性

### 高严重度

| Issue | 描述 | 状态 |
|---|---|---|
| [#4368](https://github.com/OpenHands/software-agent-sdk/issues/4368) | **ACP 对话在 Laminar 中完全不可见**：span 无 LLM 调用、无工具调用、无 token/cost 属性，结构性等同于"agent 从未运行"，导致可观测性失效 | Open，无 fix PR，严重度 high |
| [#4267](https://github.com/OpenHands/software-agent-sdk/issues/4267) | **agent-server ACP 无响应**：本地 ACP + opencode + ollama 配置下，GitHub 自动化触发时服务无响应 | Open，持续 3 周+，无 fix PR |

### 中严重度

| Issue | 描述 | 状态 |
|---|---|---|
| [#4365](https://github.com/OpenHands/software-agent-sdk/issues/4365) | **子代理（task 工具）trace 归属错乱**：共享父级 `trace_id` 但携带独立 `session_id`，导致一个 trace 横跨两个 session，span 交错排序 | Open，Needs Design |
| [#3759](https://github.com/OpenHands/software-agent-sdk/issues/3759) | **`is_git_url()` 不识别 `ssh://` scheme**：插件源以 `ssh://git@...` 形式配置时在解析阶段即失败，报误导性错误 "Unable to parse" | Open，持续 7 周+ |
| [#4363](https://github.com/OpenHands/software-agent-sdk/issues/4363) | **`InstallationManager.update()` 静默丢弃固定版本引用**：总是以 `ref=None` 重新拉取，忽略用户固定的 SHA/tag | Open，release-note-required |
| [#4369](https://github.com/OpenHands/software-agent-sdk/pull/4369) | **#4367 引入的 MCP 回归**：动态工具快照 reconcile 功能存在遗漏，@VascoSch92 已提交 fix PR | Fix PR 待合并 |

### 已修复

| Issue | 描述 | 修复 PR |
|---|---|---|
| [#4358](https://github.com/OpenHands/software-agent-sdk/issues/4358) | 两个可观测性 bug：TOOL span 在并行工具执行下丢失父级；工具 LLM 调用（generate_title/ask_agent）泄漏进 trace | ✅ [#4359](https://github.com/OpenHands/software-agent-sdk/pull/4359) + [#4360](https://github.com/OpenHands/software-agent-sdk/pull/4360) 已合入 |

**观察**：可观测性是今日 bug 焦点——#4358、#4368、#4365 三个 issue 均属该领域，且修复速度很快（#4358 当天合入修复）。ACP 相关 bug（#4267、#4368）呈现聚集趋势，建议优先排查 ACP server 与可观测性组件的集成。ss`ssh://` scheme 问题已存在 7 周未响应，建议维护者评估修复优先级（涉及插件生态可用性）。

---

## 6. 功能请求与路线图信号

### 可能纳入下一版本的功能

| 功能 | Issue/PR | 证据与判断 |
|---|---|---|
| **Canvas Extensions（完整安全架构）** | [#4348–#4357](https://github.com/OpenHands/software-agent-sdk/issues/4348) 等 10 个 issue | 系列 issue 拆解详尽，标注 security/priority:high，且今日无对应 PR 提出，可能仍处于设计阶段。预计将分批实现，安全相关（#4348/#4351）可能优先 |
| **清理 LLM Profile**（[#4343](https://github.com/OpenHands/software-agent-sdk/issues/4343)） | 对应 PR [#4344](https://github.com/OpenHands/software-agent-sdk/pull/4344) 已提交 | 小模型修正 agent 对外输出（Slack/GitHub/chat）的乱码问题。作者 @smolpaws 表示已参考 `ask_oracle` 模式并跑通单测

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*