# OpenClaw 生态日报 2026-07-23

> Issues: 408 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-22 23:27 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-07-23

---

## 1. 今日速览

过去 24 小时项目活跃度极高：**408 条 Issue 更新**（其中 258 条新开/活跃、150 条关闭），**500 条 PR 更新**（308 条待合并、192 条已合并/关闭），无新版本发布。维护者 @steipete 主导了多项大规模重构与测试清理，12 个 PR 在当日被合并。同时，大量高优先级（P0/P1）Bug 仍在讨论或等待评审，社区焦点集中在 **性能回归、网关启动崩溃、安全边界与会话状态一致性** 上。整体来看，项目处于密集开发和问题修复并行阶段，健康度中等偏积极，但积压的重度缺陷需要持续关注。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日合并（CLOSED）的重要 PR 包括（按时间顺序）：

| PR | 标签 | 解决的问题 |
|----|------|------------|
| [#112789](https://github.com/openclaw/openclaw/pull/112789) | `agents, maintainer, size: XL` | 重构重启恢复测试固定夹具，将 5909 行的单文件测试拆分为可维护结构 |
| [#112775](https://github.com/openclaw/openclaw/pull/112775) | `gateway, agents, maintainer, size: L` | 移除未使用的 JSONL 会话路径，统一为 SQLite 后端 |
| [#112772](https://github.com/openclaw/openclaw/pull/112772) | `gateway, commands, agents, maintainer, size: M` | 合并模型引用规范化函数，减少代码重复 |
| [#112739](https://github.com/openclaw/openclaw/pull/112739) | `gateway, maintainer, size: S` | 审计暂存 finalize 围栏，消除不必要的稳定性等待 |
| [#112792](https://github.com/openclaw/openclaw/pull/112792) | `docs, channel: signal, channel: slack, maintainer, size: XL` | 将 Slack 和 Signal 的 Zod schema 定义移入插件，解耦核心与外部插件 |
| [#112777](https://github.com/openclaw/openclaw/pull/112777) | `docs, channel: signal, app: macos, gateway, security, maintainer, size: M` | 为非默认 profile 分配独立的网关日志文件，避免日志混淆 |
| [#112738](https://github.com/openclaw/openclaw/pull/112738) | `commands, maintainer, size: XL` | 修复 onboarding 流程：确保设置效果应用到正确的默认代理 |
| [#112786](https://github.com/openclaw/openclaw/pull/112786) | `docs, channel: discord, channel: telegram, maintainer, size: M` | 将 Discord 和 Telegram 中的重试/文本截断帮助器提取为共享模块 |
| [#112785](https://github.com/openclaw/openclaw/pull/112785) | `docs, scripts, maintainer, size: XL` | 将 Google Meet、Teams、Zoom 的会议适配器运行时胶水提取到公共层 |

此外，以下**关键修复/功能 PR**仍处于 OPEN 状态，但已获得 **ready for maintainer look** 或 **needs proof** 标签，预计近期合并：

- [#112558](https://github.com/openclaw/openclaw/pull/112558)（修复设备认证升级时 Control UI 访问丢失）
- [#112788](https://github.com/openclaw/openclaw/pull/112788)（Android 原生设置聊天界面）
- [#112678](https://github.com/openclaw/openclaw/pull/112678)（将隐式 main-agent fallback 移至加载时注入）
- [#112763](https://github.com/openclaw/openclaw/pull/112763)（序列化插件生命周期变更，保留需要 setup 的安装）

整体来看，项目在**代码结构清理、插件解耦、会话模型统一**方面取得了显著进展，为后续功能迭代奠定了更稳健的基础。

---

## 4. 社区热点

以下 Issue/PR 在过去 24 小时讨论最活跃（评论数/👍最多）：

### 🔥 [#75 – Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)
- **评论** 115 | **👍** 80
- **长期功能请求**：希望为 Linux 和 Windows 提供类似 macOS 的桌面应用。自 2026 年 1 月创建以来持续高热度，代表跨平台用户的核心诉求。

### 🔥 [#85333 – `openclaw doctor --fix` 4-5x 性能回归](https://github.com/openclaw/openclaw/issues/85333)
- **评论** 17 | **👍** 1
- **性能回归**：版本 2026.5.20 相比 5.19，同一命令从 55s 飙升至 229s+，根因是会话快照路径遍历瓶颈。用户提供了详细复现步骤和日志，目前标签为 `needs-maintainer-review`。

### 🔥 [#13583 – 预响应强制执行钩子（hard gates）](https://github.com/openclaw/openclaw/issues/13583)
- **评论** 16 | **👍** 2
- **安全增强**：要求提供机械性的“必须调用某工具后才能回复”机制，而不是软提示。适用于量化金融、安全等高风险场景。

### 🔥 [#91009 – Codex PreToolUse native hook 导致 CPU 满载](https://github.com/openclaw/openclaw/issues/91009)
- **评论** 15 | **👍** 2
- **稳定性**：Codex 集成中，pre_tool_use 事件反复生成 CPU 密集型进程，导致网关 RPC 停滞。已有 linked PR 正在修复。

### 🔥 [#10659 – 掩码密钥（Masked Secrets）](https://github.com/openclaw/openclaw/issues/10659)
- **评论** 15 | **👍** 4
- **安全**：希望代理能**使用** API 密钥但不**看到**明文，防止提示注入泄露凭据。受到社区广泛支持。

### 🔥 [#96857 – 工具文本输出退化为图片占位符](https://github.com/openclaw/openclaw/issues/96857)
- **评论** 13 | **👍** 4
- **Bug**：普通文本输出被替换为 `(see attached image)`，导致代理无法读取命令输出。影响所有使用工具的会话。

**分析**：社区注意力明显聚焦在**安全（密钥掩码、强制执行钩子）、性能回归、跨平台应用**三大方向。高 👍 数的功能请求反映了用户对安全管控和通用平台的迫切需求。

---

## 5. Bug 与稳定性

以下为今日报告中涉及的 Bug/回归问题，按严重程度排列：

### P0 (Critical – 阻塞功能或导致不可用)

| Issue | 描述 | 当前状态 |
|-------|------|----------|
| [#108435](https://github.com/openclaw/openclaw/issues/108435) | 升级到 2026.7.1 后网关无法启动（Error: gateway did not start） | OPEN，`needs-maintainer-review`，无 linked PR |
| [#98674](https://github.com/openclaw/openclaw/issues/98674) | macOS 安装应用图标无法点击（.dmg 缩放问题） | CLOSED（已修复） |

### P1 (High – 严重影响用户体验或导致数据/会话问题)

| Issue | 描述 | 修复状态 |
|-------|------|----------|
| [#85333](https://github.com/openclaw/openclaw/issues/85333) | `doctor --fix` 性能回归 4-5x（55s→229s） | OPEN，`needs-maintainer-review` |
| [#91009](https://github.com/openclaw/openclaw/issues/91009) | Codex PreToolUse hook 导致 CPU 满载、RPC 停滞 | OPEN，`linked-pr-open` |
| [#92043](https://github.com/openclaw/openclaw/issues/92043) | 180s 压缩超时无部分进度复用，导致长时间压缩每次失败 | OPEN，`linked-pr-open` |
| [#99054](https://github.com/openclaw/openclaw/issues/99054) | Teams 应用删除/重加保留前次 DM 会话历史 | OPEN，已有修复 PR [#104690](https://github.com/openclaw/openclaw/pull/104690) |
| [#108580](https://github.com/openclaw/openclaw/issues/108580) | 2026.7.1 中 cron 工具 schema 与 llama.cpp 语法约束不兼容 | OPEN，`linked-pr-open` |
| [#86031](https://github.com/openclaw/openclaw/issues/86031) | Windows 网关监听但健康检查超时，Telegram 轮询阻塞 | OPEN，`needs-maintainer-review` |
| [#90840](https://github.com/openclaw/openclaw/issues/90840) | 子代理完成输出误传给聊天用户（替代父代理摘要） | OPEN，`needs-maintainer-review` |
| [#99773](https://github.com/openclaw/openclaw/issues/99773) | 热重载丢失 include 定义的模型，导致“Unknown model”故障转移错误 | OPEN，`needs-live-repro` |
| [#39807](https://github.com/openclaw/openclaw/issues/39807) | 计费错误 (402) 导致无限重试死亡螺旋（无退避） | OPEN，`linked-pr-open` |
| [#85103](https://github.com/openclaw/openclaw/issues/85103) | 模型 fallback 链在 Provider 配额耗尽时不触发 | CLOSED（已关闭，但未说明修复） |
| [#84610](https://github.com/openclaw/openclaw/issues/84610) | 升级后网关每 90s 被 SIGTERM 杀死（WSL2） | CLOSED（可能已修复） |
| [#83968](https://github.com/openclaw/openclaw/issues/83968) | macOS 网关因 `assert(!this.paused)` 崩溃 | CLOSED（已修复） |

### P2 (Medium – 影响功能但可用绕行方案)

- [#87318](https://github.com/openclaw/openclaw/issues/87318) – Amazon Bedrock Haiku 4.5 推理配置文件 ARN 不支持
- [#87314](https://github.com/openclaw/openclaw/issues/87314) – 网关内存泄漏（读文件错误导致每日增长 ~60MB）
- [#94626](https://github.com/openclaw/openclaw/issues/94626) – LINE 频道 `/status` 偶尔无响应
- [#87980](https://github.com/openclaw/openclaw/issues/87980) – `exec` 工具静默破坏 `2>&1` / `2>/dev/null` 重定向参数

**小结**：今日活跃的 Bug 中，**P0 级别 1 个未修复**（网关启动失败），**P1 级别 10+ 个**，其中 4 个已有 linked PR 在推进。性能回归和会话状态问题仍是主要风险区。

---

## 6. 功能请求与路线图信号

### 用户明确提出的新功能需求（基于 Enhancements 标签）

| Issue | 简述 | 社区认可度 | 可能纳入下版本？ |
|-------|------|------------|-----------------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | Linux/Windows 原生桌面应用 | 👍 80，最高热度 | 长期路线图 |
| [#13583](https://github.com/openclaw/openclaw/issues/13583) | 预响应强制执行钩子（硬门控） | 👍 2 | 可能性中（已有 linked PR？未发现） |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | 掩码密钥（masked secrets） | 👍 4 | 较高（安全相关，社区呼声高） |
| [#38568](https://github.com/openclaw/openclaw/issues/38568) | 在系统提示中注入上下文窗口百分比 | 👍 2 | 较低（P3，近期未更新） |
| [#9912](https://github.com/openclaw/openclaw/issues/9912) | 添加 `maxTurns`/`maxToolCalls` 配置限制代理迭代次数 | 👍 1 |

---

## 横向生态对比

好的，作为专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师，以下是基于您提供的六份项目日报生成的横向对比分析报告。

---

### 个人 AI 智能体/自主智能体开源生态横向分析报告 (2026-07-23)

#### 1. 生态全景

整体生态在2026年7月23日呈现**高活跃度、分化发展**的态势。一方面，以 **OpenHands SDK**、**OpenClaw** 和 **Pi** 为代表的通用型 Agent 框架正从“功能可用”向“架构稳定、体验一致”过渡，焦点集中于**会话状态一致性、安全审计和跨平台兼容性**。另一方面，以 **LiteLLM** 为代表的模型网关和以 **Temporal** 为代表的工作流引擎，则在为上述 Agent 系统提供更健壮、可扩展的底层基础设施。值得注意的是，**社区对安全、性能和记忆持久化的诉求已成为跨项目的共同痛点**，标志着生态正从“玩转大模型”走向“构建可靠的生产级智能体应用”。

#### 2. 各项目活跃度对比

| 项目名称 | 24h Issues 动态 | 24h PR 动态 | 新版本发布 | 分析师健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 258 新开/活跃, 150 关闭 | 500 更新, 308 待合并, 192 关闭 | 无 | **中等偏积极** (密集开发与问题修复并行，积压较重) |
| **Hermes Agent** | 78 新开, 38 关闭 | 500 更新, 362 待合并, 138 关闭 | 无 | **高强度迭代** (功能驱动为主，合并率低，稳定性滞后) |
| **OpenHands SDK** | 约 23 新开/活跃, 5 关闭 | 50 更新, 约 36 待合并, 14 关闭 | 无 (v1.37.0 测试中) | **快速演进** (核心功能落地，代码审查严格，健康度良好) |
| **Pi** | 9 活跃, 61 关闭 | 30 更新, 8 待合并, 22 关闭 | 无 | **积极** (大量回归性 Bug 修复，维护节奏强劲) |
| **LiteLLM** | 45 新开, 5 关闭 | 263 总更新, 多数已合并/关闭 | v1.95.0-dev.1 & v1.94.0-rc.3 | **极高度活跃** (Rust核心迁移+高强度Bug修复，迭代速度极快) |
| **Temporal** | 0 新开 | 62 更新, 39 待合并, 23 关闭 | 无 | **健康度良好** (集中于功能收尾与稳定化冲刺) |

#### 3. OpenClaw 在生态中的定位

- **核心/参考实现地位**：从“核心参照”的定位和极高的 Issue/PR 处理量来看，OpenClaw 扮演着生态**基础架构和标准制定者**的角色。其维护者（如 @steipete）主导的大规模重构（如测试夹具拆分、插件解耦），旨在提升项目长期的可持续性和扩展性，这与追求短期功能快速迭代的其他项目形成对比。
- **技术路线差异**：OpenClaw 更强调**模块化与解耦**（如将 Zod schema 移入插件、统一会话后端）。这使其比其他项目（如 Hermes Agent）具备更优的架构弹性，但也意味着开发和调试的复杂度更高。
- **社区规模与成熟度**：凭借 400+ Issue 和 500+ PR 的日活跃度，以及大量标注为 `maintainer` 的 PR，表明其拥有**最庞大和最专业的开发者社区**。其讨论焦点（如性能回归、网关崩溃、安全边界）也反映出用户群体偏技术向、对系统稳定性要求严苛。

#### 4. 共同关注的技术方向

| 共同方向 | 涉及项目 | 具体诉求/表现 |
| :--- | :--- | :--- |
| **会话状态一致性与持久化** | **OpenClaw** (#90840 子代理输出错误, #99054 Teams历史残留)；**Hermes Agent** (#8457/#4335 跨平台记忆共享, #27013 会话重启忘事)；**OpenHands SDK** (#4080 单事件反序列化导致会话丢失) | 用户普遍要求 Agent 的“记忆”更可靠、可持久化、能跨平台共享。 |
| **安全与隐私** | **OpenClaw** (#13583 强制执行钩子, #10659 掩码密钥)；**OpenHands SDK** (#4190 秘密值泄露, #4157 安全分析器信任模型自评风险)；**LiteLLM** (#34217 删除团队后密钥仍有效) | 社区对**密钥/凭据的遮蔽、操作的机械性门控、基于角色的访问控制**的需求急剧上升。 |
| **性能与资源优化** | **OpenClaw** (#85333 性能回归)；**OpenHands SDK** (#3153 性能跟踪, #3266 闲置会话未清理)；**Pi** (#6879 自动压缩不触发) | 长时间运行后出现的内存泄漏、上下文压缩失效、并发处理瓶颈是普遍痛点。 |
| **跨平台支持** | **OpenClaw** (#75 Linux/Windows 桌面应用)；**Hermes Agent** (桌面端Ctrl+V失效)；**Pi** (#6817 Windows find工具失败) | 用户对 macOS 之外平台的体验要求日益提高，Windows 支持是主要短板。 |

#### 5. 差异化定位分析

| 项目 | 核心定位 | 功能侧重 | 目标用户 | 关键架构差异 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 个人 AI 助手的核心框架与基础设施 | 插件化、模块化、高度可定制的基础平台 | 开发者、系统集成商、追求极致控制力的高级用户 | 强调核心-插件分离，拥有复杂的网关与会话管理 |
| **Hermes Agent** | 面向大众的通用型个人AI助手 | 开箱即用、多平台 (CLI/Telegram/Discord)、会话记忆共享 | 希望快速获得强大Agent能力的广泛开发者与用户 | 追求易用性和丰富的第三方平台集成 |
| **OpenHands SDK** | 面向软件开发场景的 Agent SDK | 软件工程任务 (代码编写、命令行)、持久化记忆 | 希望将 Agent 能力集成到 IDE/CI/CD 中的应用开发者 | 提供底层 SDK，专注于软件工程环境的交互与监控 |
| **Pi** | 高性能、本地优先的编程/调试助手 | 代码理解、文件搜索、与 IDE/Terminal 深度集成 | 程序员、DevOps，注重开发效率与性能 | 强调终端交互体验，对 `find`、`exec` 等工具优化深入 |
| **LiteLLM** | 统一的 LLM API 网关和成本管理 | 百种模型接入、计费/配额、访问控制、性能监控 | 企业 AI 平台团队、SaaS 提供商 | 模型路由和成本追踪是其核心价值，正向 Rust 和现代 UI 转型 |
| **Temporal** | 分布式工作流编排引擎 (执行 Agent 的“操作系统”) | 工作流状态管理、重试、超时、恢复 | 构建高可靠性、长周期运行的 Agent 应用的工程师 | 提供确定性重放和可靠执行保障，本身不直接提供 LLM 交互能力 |

#### 6. 社区热度与成熟度

- **快速迭代与功能扩张期**：**Hermes Agent** 和 **LiteLLM** 处于此阶段。它们的 PR 合并率低、新功能/新平台请求多，表现出强烈的“先跑通再优化”特征。社区充满活力，但稳定性和代码质量面临挑战。
- **质量巩固与架构优化期**：**OpenClaw**、**OpenHands SDK**、**Pi** 均处于此阶段。它们虽然也有新功能，但更多精力投入到**模型解耦、会话统一、Bug 修复和性能回归处理**上。代表项目从“能做”走向“做好”。
- **专业稳定与下沉赋能期**：**Temporal** 是典型的底层基础设施项目，其社区讨论高度集中于内部机制（如 CHASM/SAA 的兼容性）。其高合并率表明开发流程成熟，社区主要为贡献代码的专业工程师。

#### 7. 值得关注的趋势信号

1.  **从“软约束”到“硬门控”的安全范式转移**：多个项目（**OpenClaw**, **OpenHands SDK**）社区都在要求对 Agent 行为进行**无法通过提示注入绕过的机械性安全控制**，如“强制执行钩子”、“秘密遮蔽”。这表明开发者已意识到单纯依赖模型安全提示的脆弱性，**强约束、可审计的安全模型**将成为 Agent 框架的核心竞争力。

2.  **“可编程记忆”成为 Agent 智能的核心载体**：**OpenHands** 的 `MEMORY.md` 功能和 **Hermes** 社区对“跨平台记忆共享”的强烈呼声，共同指向一个趋势：记忆系统不再是简单的日志拼接，而是**结构化的、可被编程读取的“长期知识库”**。未来的 Agent 将通过学习、总结并写入结构化记忆来实现真正的个性化与适应性进化。

3.  **Agent 性能瓶颈正从“模型推理”转向“系统开销”**：**OpenClaw** 的“`doctor --fix` 性能回归”、**OpenHands** 的“会话加载失败”及 **Pi** 的“自动压缩不触发”，这些 Bug 的根源已不再是模型本身的推理速度，而是会话快照、数据反序列化、上下文压缩等**系统层操作的效率问题**。这表明，当模型能力日益趋同后，**Agent 框架的工程效率**将成为决定用户体验的关键分水岭。

4.  **“跨平台”与“本地优先”并存的部署模式**：一方面，**OpenClaw** 和 **Pi** 社区对 Linux/Windows 原生应用的呼声高涨，表明桌面端仍是重交互场景的主战场；另一方面，**Pi** 对 `llama.cpp` 等本地模型支持的关注，以及 **LiteLLM** 对自托管模型的错误处理，反映出**对数据主权和离线能力的追求**正在成为深层需求。未来 Agent 的成熟形态将是“云-边-端”混合部署。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，这是为您生成的 Hermes Agent 项目动态日报。

---

### Hermes Agent 项目动态日报 | 2026-07-23

**分析师点评：** 项目社区活跃度极高，24小时内产生了369条 Issue 和 500条 PR 讨论，显示出庞大的用户基础与开发热情。然而，新开 Issue 与待合并 PR 的数量远高于已关闭/合并的量，表明功能的快速迭代和 Bug 修复正面临一定的积压压力。项目核心架构（如记忆系统、网关平台适配）的稳定性与扩展性成为社区关注的焦点，多个高赞功能请求已进入开发流程。

---

### 1. 今日速览

今日项目处于 **高强度迭代** 状态。社区贡献活跃，贡献者提交了500个 PR，但合并率仅为 27.6%（138/500），大量的代码变更正在等待审核与合并。与此同时，新报告的 Bug 和需求层出不穷，围绕 **会话持久化、跨平台记忆共享、高性能上下文压缩** 等方向展开了深入讨论。项目整体呈现出 **功能驱动、稳定性滞后** 的早期快速发展特征，维护团队需要在高频的社区输入与代码质量/稳定性保障之间寻找平衡。

---

### 3. 项目进展

通过分析被合并的 PR，可以看到项目在 **桌面客户端稳定性和 CI/CD** 方面取得了一些进展：
- **修复桌面端压缩后渲染错误**：[PR #69682](https://github.com/NousResearch/hermes-agent/pull/69682) 修复了桌面客户端在上下文压缩后，会错误地追加旧的用户提示信息，导致界面显示错乱的问题。
- **改进 CI 与 E2E 测试**：[PR #69631](https://github.com/NousResearch/hermes-agent/pull/69631) 将桌面端 E2E 测试的截图和差异对比结果集成到代码审查评论中，提升了代码审查效率。
- **修复 TUI 界面皮肤错误**：[PR #69671](https://github.com/NousResearch/hermes-agent/pull/69671) 修复了在深色背景的皮肤设置下，部分文字不可见的Bug，提升了用户体验。
- **清理技术债务**：合并了数个自动化格式修复 PR（如 [PR #69673](https://github.com/NousResearch/hermes-agent/pull/69673)），保持了代码库的整洁。

此外，多个涉及 **Kanban 看板粘性、WhatsApp 平台功能扩展、多Profile会话处理** 的 PR 处于待合并状态，表明这些功能方向即将被纳入主干。

---

### 4. 社区热点

今日讨论热度最高的议题主要集中在 **核心功能与第三方平台适配** 的摩擦上：

1.  **Codex CLI 兼容性问题**：[Issue #13834](https://github.com/NousResearch/hermes-agent/pull/13834) 获得 **18条** 评论和 3个 👍。用户报告在同样的 macOS 和网络环境下，官方 Codex CLI 可以正常工作，但 Hermes Agent 的 `openai-codex` 模式却反复失败。该问题直指**核心功能的可靠性**，引发了社区对底层连接和认证机制的广泛讨论。

2.  **持久化会话记忆与跨平台共享**：[Issue #8457](https://github.com/NousResearch/hermes-agent/pull/8457) 和 [Issue #4335](https://github.com/NousResearch/hermes-agent/pull/4335) 合计获得 **22条** 评论。社区表达了强烈的对于 *会话记忆永不丢失* 和 *在 CLI/Telegram/Discord 间同步记忆* 的渴望。这反映了用户愿意将 Hermes 作为核心生产力工具，并期望其记忆系统像现代浏览器或笔记软件一样可靠。
    -   *分析师注：* 这被定位为“Feature Request”，是项目**路线图上的强信号**。

3.  **桌面版体验 Bug**：[Issue #24860](https://github.com/NousResearch/hermes-agent/pull/24860) 关于 Dashboard 中 Ctrl+V 粘贴和图片粘贴失效的问题，获得了 **12条** 评论和 4个 👍。这表明桌面客户端是用户广泛使用的重要界面，基础的交互体验问题会严重影响用户留存。

---

### 5. Bug 与稳定性

今日上报的 Bug 普遍为中等严重级别（P2、P3），缺乏 P0（致命）级问题，但 **“会话损坏”**和 **“会话阻塞”** 类的问题值得高度警惕。

| 严重等级 | 关键 Bug | 摘要 | Fix PR 状态 |
| :--- | :--- | :--- | :--- |
| **紧急 (P1)** | [Worker 死锁](https://github.com/NousResearch/hermes-agent/issues/68915) | 当 Agent 通过 shell `&` 将服务器进程放入后台时，子进程的 stdout 管道未被关闭，导致主 Worker 进程永久死锁。 | **无** |
| **高 (P2)** | [xAI Grok 4.5 图片导致会话永久损坏](https://github.com/NousResearch/hermes-agent/issues/69078) | 当会话历史中包含 xAI 无法解析的 PNG 图片后，该会话的所有 API 调用（甚至纯文本）都会返回 400 错误，且重启无法恢复，只能删除会话。 | **无** |
| **中 (P3)** | [Telegram 大文件上传超时](https://github.com/NousResearch/hermes-agent/issues/62936) | 配置的环境变量 `HERMES_TELEGRAM_HTTP_WRITE_TIMEOUT` 对媒体上传操作无效，导致超过 ~15MB 的文件上传总是失败。 | **无** |
| **中 (P3)** | [Kimi CN 中文搜索流式解压失败](https://github.com/NousResearch/hermes-agent/issues/28049) | 使用 Kimi K2.6 模型时，brotli 流式解压会引发错误，导致返回空响应，造成任务重试和放弃。 | **无** |
| **待修复 (P2)** | [桌面端 `default` Profile 会话侧边栏空白](https://github.com/NousResearch/hermes-agent/issues/67600) | 更新后，名称为 `default` 的 Profile，其会话列表在侧边栏空白。 | **无** |

- **新增关注点**：`[PR #69681](https://github.com/NousResearch/hermes-agent/pull/69681)` 修复了 SQLite 连接泄漏问题，这是导致长期运行后资源耗尽和卡死的潜在元凶之一。

---

### 6. 功能请求与路线图信号

尽管项目积压较多，但从讨论热度和点赞数可以清晰看到社区最期望的方向：

1.  **支持 Mistral 作为 LLM 提供商**：[Issue #20859](https://github.com/NousResearch/hermes-agent/issues/20859) 获得 **23个** 👍，是目前最受欢迎的功能请求。用户对集成 Mistral 生态有强烈需求，且已有基础，难度可控。**强烈建议纳入下一版本计划。**
2.  **内置自动备份与版本控制**：[Issue #12238](https://github.com/NousResearch/hermes-agent/issues/12238) 获得 **19个** 👍。用户对代理数据（记忆、技能）的安全性有很高要求，希望有类似 Git 的自动备份和追踪机制。这是一个基础架构层面的重大特性。
3.  **可配置记忆后端**：[Issue #47349](https://github.com/NousResearch/hermes-agent/issues/47349) 获得 14条评论。社区期望能禁用默认的 `memory.md` 文件，转而使用 honcho 或 fact_store 等更结构化的记忆后端。这反映了用户对更可控、更专业记忆系统的追求。
4.  **跨平台会话记忆共享**：[Issue #4335](https://github.com/NousResearch/hermes-agent/issues/4335) 获得 8条讨论。用户期望在多终端（CLI、Telegram）间工作的 Agent 能拥有统一且连贯的记忆。**这一需求与 `[Issue #8457]` 的持久化记忆结合，构成了项目记忆系统发展的核心路线图。**

- **已进入开发流程的信号**：`[PR #69675](https://github.com/NousResearch/hermes-agent/pull/69675)` 提出了“per-function tool filtering”，允许用户精细控制禁用特定工具（如 `skill_manage`, `write_file`）。`[PR #53378](https://github.com/NousResearch/hermes-agent/pull/53378)` 实现了“Hey Hermes”语音唤醒功能。`[PR #69670](https://github.com/NousResearch/hermes-agent/pull/69670)` 为 WhatsApp 平台增加了历史消息 API。

---

### 7. 用户反馈摘要

从今日的 Issue 评论中可以提炼出以下有价值的用户反馈：

- **痛点：调试困难**：大量 Bug 报告（如 #69078 #62936）显示，当出现错误时，用户的唯一手段是“删除会话”或“重启”，缺乏有效的中间恢复或调试工具。社区在 [#44456](https://github.com/NousResearch/hermes-agent/issues/44456) 中也抱怨 `compress` 命令在桌面客户端失效。
- **痛点：上下文丢失**：多位用户（如 #27013）抱怨 Agent 在会话重启时会忘记关键的项目上下文甚至凭空捏造项目信息，这严重影响了其在复杂项目中的可靠性。
- **诉求：对“Power User”的友好度**：用户提出了精细化的控制需求，例如“按模型/提供商设置不同的压缩阈值”（#18733）、“支持按 Cron 任务设置不同的推理力度”（#23524）。这表明社区中存在一批深度使用用户，他们需要更灵活、更底层的配置。
- **不满意：新手引导不足**：[Issue #13834] 中用户指出官方 CLI 工作正常而 Hermes 的同样功能失败，这反映出项目在特定模块的默认配置或依赖处理上存在文档或逻辑缺失，对新手不友好。

---

### 8. 待处理积压

以下 Issue 和 PR 长期未得到响应或被阻塞，需要维护团队关注：

- **长期开放的高热度特性**：
    - **[Issue #4335](https://github.com/NousResearch/hermes-agent/issues/4335) (2026-03-31，P3)**：跨平台会话共享功能，已开放近4个月，但热度不减。讨论已趋于成熟，可能需要决策者拍板或在架构层面进行设计。
    - **[Issue #12238](https://github.com/NousResearch/hermes-agent/issues/12238) (2026-04-18，P3)**：自动备份与版本控制，19个 👍 保持高水平关注，但无实质性进展。

- **被阻塞的PR**：
    - **[PR #68387](https://github.com/NousResearch/hermes-agent/issues/68387) (2026-07-21)**：Google Chat 适配器的 Bug 报告，状态为 `blocked`。这表明该网关整合遇到了难以推进的技术问题。

- **高风险待审 PR**：
    - **[PR #66520](https://github.com/NousResearch/hermes-agent/pull/66520) (2026-07-17)**：将 CI 迁移至 GKE 自托管运行器。这是一个大规模基础设施变更，因其影响面广（`sweeper:risk-automation`），且已开放近一周，亟需经验丰富的 maintainer 审核。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

好的，这是为您生成的 2026-07-23 OpenHands SDK 项目动态日报。

---

### OpenHands SDK 项目日报 | 2026-07-23

**分析师:** AI 智能体 & 个人 AI 助手领域开源项目分析师
**数据来源:** github.com/OpenHands/software-agent-sdk

---

### 1. 今日速览

项目今日活跃度极高，共处理了 **28 条 Issues** 和 **50 条 Pull Requests**，显示出一个大型开源项目在核心开发周期中的高频迭代状态。尽管没有新版本发布，但社区和核心贡献者在功能开发、性能优化和关键 Bug 修复上均有显著推进。值得关注的是，本周期的 PR 合并率（28%）相对较低，反映出目前有大量的工作在审查或阻塞状态，另一方面也说明项目在代码质量上把关严格。社区讨论集中在安全审计、模型兼容性、以及会话管理稳定性等关键领域，项目整体健康状况良好，处于快速演进阶段。

### 2. 版本发布

- **无新版本发布。** 上一个准备发布的 PR (`#4196`) 在今日创建，目标版本为 v1.37.0，目前正处于测试和审查阶段。上一个版本发布候选 PR (`#4123`) 已于今日关闭，表明存在一些阻碍因素导致其未能完成。

### 3. 项目进展

今日项目迎来了多项重要功能合并和问题关闭，主要进展如下：

- **持久化记忆功能落地**：备受期待的 **跨会话持久化记忆（Memory）** 功能已通过 PR `#4178` 合并。该功能允许代理将学习到的用户偏好和代码库模式写入 `MEMORY.md` 文件，并在每次会话开始时自动注入到系统提示中，极大地增强了代理的连续学习和自适应能力。这标志着项目在 `behavior-initiative` 路线图上迈出了关键一步。
- **MCP 协议能力增强**：PR `#3894` 的合并让 SDK 现在支持 MCP 服务器的 `tools/list_changed` 通知。这使得 MCP 工具集可以动态变化，而无需重启会话或服务，为更先进的渐进式工具发现机制铺平了道路。相关的 Issue `#4059` 也随之关闭。
- **关键 Windows 兼容性修复**：PR `#4155` 修复了 `WindowsTerminal` 无法提交多行 PowerShell 命令的严重 Bug。该问题导致包含 OpenHands 元数据的脚本无法执行，影响所有 Windows 端用户。此修复确保了跨平台体验的一致性。
- **安全性增强**：PR `#4191` 修复了 `SecretRegistry` 的一个逻辑漏洞，确保所有注册的秘密（Secret）值都能在终端输出中被正确遮蔽，而不仅仅是那些在命令中引用了名称的秘密。这对防止敏感信息泄露至关重要。
- **新功能框架搭建**：PR `#4188` 引入了在 `agent-server` 中持久化父子会话关系的能力，为 Agent Canvas 启动子会话等复杂交互场景提供了基础支持。

### 4. 社区热点

今日讨论热度集中在以下几个议题：

1.  **ACP 协议兼容性问题**: Issue `#4093` (6条评论) 讨论了 ACP 0.11 版本中一个不稳定字段的移除，导致 Gemini 模型状态无法正确解析。这反映出社区对底层协议稳定的高依赖性，以及在无上限版本约束下潜在的兼容性风险。该讨论引发了关于依赖管理策略的思考。
2.  **可视化器 (Visualizer) 性能与准确性**: Issue `#4189` (1条评论) 及其对应的 Fix PR `#4193` 指出并行工具调用场景下，可视化器中的性能指标显示存在重复计算问题。这说明精细化监控和调试工具是社区重度用户的核心需求，对“所见即所得”的指标准确性要求很高。
3.  **安全分析器的潜在风险**: Issue `#4157` (2条评论) 指出 `LLMSecurityAnalyzer` 信任 LLM 自我评估的风险等级。当配置为仅对高风险操作进行人工确认时，模型可将风险标记为“低”来自动绕过安全审查。该讨论直指 AI Agent 安全的核心矛盾：**由被审计方（模型）去评估自身行为的风险**，引发了广泛关注。

### 5. Bug 与稳定性

今日报告的 Bug 主要涉及安全、会话管理及模型兼容性，按严重程度排列如下：

- **[严重] 秘密值泄露**: **Issue `#4190`** 报告了 `SecretRegistry` 的秘密值遮蔽存在逻辑漏洞，已通过 **PR `#4191`** 修复。这是今日最高优先级的修复，直接关系到用户敏感信息安全。
- **[高] 会话加载失败导致数据丢失**: **Issue `#4080`** (7条评论) 指出，如果单个事件反序列化失败（例如使用了未注册的 `observation.kind`），会导致整个会话加载失败且“静默丢失”。这是一个严重的数据可靠性问题，目前尚无 Fix PR。
- **[高] 非对称响应处理导致会话终止**: **Issue `#3992`** (8条评论) 描述了一个设计问题：当 LLM 返回“仅内容无工具调用”的响应时，处理逻辑不对称，这会导致能力较弱的本地模型驱动的代理任务失败。该问题直接影响模型的通用兼容性。
- **[中] 服务器重启后会话丢失**: **Issue `#4192`** 报告了 `agent-server` 过快重启会导致所有历史会话丢失。如果是为了防止数据损坏而设的“锁定”机制过于敏感，这可能是一个破坏用户数据的严重回归。目前尚无 Fix PR。

### 6. 功能请求与路线图信号

今日用户提出的新功能需求显示了几个明确的路线图方向：

- **增强 Markdown-based Agent**: **Issue `#2186`** (热门) 继续追踪 Markdown Agent 的高级特性，其需求清单已部分完成 (`[X]`)。这预示着该功能将从实验性向正式功能转变。
- **远程执行工作空间**: **Issue `#4187`** 提出要解耦会话放置与工作空间类型，支持“远程执行”工作空间。这符合云原生和去中心化 Agent 架构的趋势，可能与 Agent Canvas 的协作功能有关。
- **外部安全策略集成**: **Issue `#4195`** 提出希望有一个接口，让外部沙箱或安全系统能将其“封禁/判定”结果以 Agent 观察（Observation）的形式注入回会话。这显示了用户希望将 Agent 与自有安全基础设施集成的强烈需求。

### 7. 用户反馈摘要

从今日的 Issues 评论中可以提炼出以下用户反馈：

- **对模型兼容性的关注**: `#3992` 和 `#4093` 的讨论表明，用户（尤其是使用非 OpenAI 或本地模型的用户）非常在意框架是否能公平地处理不同模型的能力差异。对 `openhands/*` 模型的无认证请求 (`#4098`) 也显示了用户对框架网络行为的关切。
- **对资源管理和性能的抱怨**: `#3141` 和 `#3153` 的持续讨论，以及新提出的 `#4189` 都表明，在生产环境中运行的社区用户对内存泄漏（无会话闲置超时）、性能瓶颈和监控指标准确性非常敏感。
- **对配置复杂性的困惑**: `#4019` 的讨论反映了用户对 ACP CLI 和 SDK 配置之间重复和冲突感到困惑。`#4158` 报告的 `switch_profile` 半应用问题则暴露了运行时状态与文件状态不同步的配置管理痛点。

### 8. 待处理积压

以下是一些长期存在的 Issue 和 PR，它们对项目健康度有重要影响，需要维护者关注：

- **长期性能跟踪 Issue**: **Issue `#3153`** 创建于5月，总结了 19 个性能问题。尽管其中一些可能已有进展，但其作为性能改进的“主追踪 Issue”至今仍有 1 条评论，表明整体性能优化尚未形成闭环。
- **未响应的性能修复 PR**: **PR `#3266`** “fix(agent-server): evict idle terminal conversations” 旨在解决 `#3141` 中描述的性能问题。该 PR 创建于5月，状态为待合并，是解决内存泄漏的关键步骤，需要推动审查与合并。
- **长期未结的增强请求**: **Issue `#2755`** “Implement HookType.PROMPT” 是一个功能增强请求，创建于4月，标签为 `help wanted`。该请求的 `HookType.PROMPT` 概念与今日合并的“持久化记忆”功能相关（记忆本质上也是一种Prompt Hook），建议重新评估其优先级。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报（2026-07-23）

## 1. 今日速览

过去 24 小时项目整体活跃度较高：共处理 70 条 Issues，其中 61 条已关闭，9 条仍在活跃；30 个 PR 中有 22 个被合并或关闭，8 个待合并。大量回归性 Bug 得到修复（如 `httpIdleTimeoutMs` 失效、自动登出、Windows 扩展路径错误等），同时社区关注的 Copilot Enterprise 兼容性、`llama.cpp` 默认模型识别等问题仍未闭合。无新版本发布。**项目维护节奏强劲，但关键路径问题（如自动压缩、find 工具 Windows 兼容）仍待解决，整体健康度呈积极态势。**

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日合并/关闭的 PR 推动了以下功能与修复：

- **外部编辑器启动优化**：`#6903` 将临时文件写入私有子目录而非 `os.tmpdir()` 根目录，解决拥堵目录下启动缓慢的问题（对应 `#6774`）。
- **TUI 崩溃日志路径修复**：`#6958` 使 crash log 遵守 `PI_CODING_AGENT_DIR` 配置，不再硬编码 `~/.pi/agent/pi-crash.log`（对应 `#6652`）。
- **Windows 下扩展依赖显示修复**：`#6964` 修复了 npm 包引入的兄弟扩展在 banner 中显示绝对路径的问题（完成 `#6619`）。
- **Bash 工具执行事件透出**：`#6967`（未合并但已标记完成）暴露会话元数据至 bash 子进程，方便扩展和脚本读取 session / provider 信息。另有 `#6971`（待合并）增加 `bash_execution_update` 事件，为前端实时更新提供支持。
- **OpenRouter 原生 OAuth**：`#6927` 合并，通过 PKCE S256 浏览器授权实现一键登录。
- **Provider 成本报告**：`#6881`（待合并）支持从响应中读取已计费成本，优先于目录价格计算，提升计费准确性。
- **StepFun 提供者**：`#6960` 新增四个面向中国和全球的 StepFun 模型 API 提供商。
- **OpenAI WebSocket 异常处理**：`#6955` 处理 `previous_response_not_found` 错误，自动重置缓存重建连接。

此外，`#6987`（待合并）尝试对齐 TUI 中的 Unicode 字宽与终端实际显示，提升混合文字（如中文、Emoji）的渲染准确性。`#6980`（待合并）使提供商重试支持 `AbortSignal`，解决 Retry-After 过长的阻塞问题（修复 `#6911`）。

## 4. 社区热点

| 编号 | 标题 | 状态 | 评论数 | 👍 |
|------|------|------|--------|----|
| [**#6768**](https://github.com/earendil-works/pi/issues/6768) | Copilot Enterprise 下无法压缩上下文 | 开放 | 8 | 8 |
| [**#6476**](https://github.com/earendil-works/pi/issues/6476) | 自托管 OpenAI 兼容提供商的 `httpIdleTimeoutMs` 回归 | 已关闭 | 12 | 0 |
| [**#6686**](https://github.com/earendil-works/pi/issues/6686) | Pi 自动退出 GitHub 登录 | 已关闭 | 10 | 0 |
| [**#6210**](https://github.com/earendil-works/pi/issues/6210) | `/scoped-models` 无法选择含括号的模型 ID | 开放 | 8 | 0 |
| [**#6922**](https://github.com/earendil-works/pi/issues/6922) | `llama.cpp` 设为默认模型时启动报错“No models available” | 开放 | 2 | 7 |

**分析**：`#6768` 获得 8 个赞，反映 **Copilot Enterprise 用户** 在上下文压缩功能上遇到了严重阻碍，OpenAI API 返回 421 错误，Anthropic 模型同样失败，问题涉及跨提供商兼容性。`#6476` 虽有 12 条评论但已关闭，表明回归得到确认并可能已修复。`#6922` 虽然评论少但赞数高，说明本地模型用户对默认模型识别失败的痛点强烈。社区对 **企业级 / 自托管模型的支持** 以及 **基本配置可靠性** 关注度最高。

## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue | 描述 | 状态 | 关联 PR |
|----------|-------|------|------|---------|
| **严重** | [#6879](https://github.com/earendil-works/pi/issues/6879) | 自动压缩在上下文超 100% 后不会触发，直到提供商拒绝请求才压缩 | 开放 | 无 |
| **严重** | [#6768](https://github.com/earendil-works/pi/issues/6768) | Copilot Enterprise 下压缩完全失败 | 开放 | 无 |
| **高** | [#6922](https://github.com/earendil-works/pi/issues/6922) | `llama.cpp` 默认模型导致启动失败 | 开放 | 无 |
| **高** | [#6476](https://github.com/earendil-works/pi/issues/6476) | `httpIdleTimeoutMs` 被忽略导致自托管模型超时 | 已关闭 | 无（可能已在代码中修复） |
| **高** | [#6817](https://github.com/earendil-works/pi/issues/6817) | Windows 下 `find` 工具无法匹配含路径分隔符的模式（如 `src/**/*.ts`） | 开放 | 无 |
| **中** | [#6911](https://github.com/earendil-works/pi/issues/6911) | OpenAI SDK 重试时遵守完整 Retry-After（可能几天），且无法中断 | 已关闭 | [#6980](https://github.com/earendil-works/pi/pull/6980)（待合并） |
| **中** | [#6975](https://github.com/earendil-works/pi/issues/6975) | TUI 启动基准测试始终在进入交互模式前退出 | 已关闭 | [#6976](https://github.com/earendil-works/pi/pull/6976)（已合并） |
| **中** | [#6957](https://github.com/earendil-works/pi/issues/6957) | AWS Bedrock 提供商忽略 profile，优先使用环境变量凭证 | 已关闭 | 无 |
| **中** | [#6920](https://github.com/earendil-works/pi/issues/6920) | 自动补全时 `fuzzyMatch` 因非字符串值崩溃（已关闭，标记为 no-action） | 已关闭 | 无 |
| **低** | [#6652](https://github.com/earendil-works/pi/issues/6652) | crash log 硬编码路径，忽略 `PI_CODING_AGENT_DIR` | 已关闭 | [#6958](https://github.com/earendil-works/pi/pull/6958)（已合并） |
| **低** | [#6774](https://github.com/earendil-works/pi/issues/6774) | Ctrl+G 外部编辑器启动慢（因临时目录拥堵） | 已关闭 | [#6903](https://github.com/earendil-works/pi/pull/6903)（已合并） |
| **低** | [#6940](https://github.com/earendil-works/pi/issues/6940) | OpenRouter 缓存断点在工具调用轮次后停止推进 | 已关闭 | 无 |

**注意**：`#6879` 和 `#6768` 是两个最影响体验的开放性严重 bug，尚无关联 PR。

## 6. 功能请求与路线图信号

- **约束采样（Constrained Sampling）**：`#6341`（PR，待讨论）添加可选配置 `constrainedSampling`，使工具可请求提供商侧 JSON 模式约束，已获得 core 成员 mitsuhiko 关注，有望进入下一版本。
- **Bedrock Mantle 提供者**：`#6216`（PR，开放）添加了基于 OpenAI 协议的 Amazon Bedrock Mantle 服务，适合 AWS 用户。
- **隐藏环境变量**：`#6923`（已关闭，no-action）希望添加命令隐藏全局环境变量以免被 Pi 读取。社区有需求但未获得实现承诺。
- **添加 README 安装说明**：`#6907`（开放）为提高新用户 onboarding 体验，已获 2 条讨论，建议采纳。
- **技能子文件夹支持**：`#6479`（开放）用户要求 `~/.agents/skills/` 下子文件夹中的技能能被自动发现，目前只支持顶层文件。属于易用性增强。
- **`--no-session` 临时目录清理**：`#6924`（开放，inprogress）在子进程方式下避免残留临时目录。
- **AgentHarness 执行工具**：`#6916`（已合并）引入 `AgentHarnessTool` 抽象，允许在扩展中传递任意应用上下文，为未来多 Agent 编排铺路。
- **`get_available_thinking_levels` RPC**：`#6865`（已合并）新增 RPC 命令，便于扩展查询当前模型的思考级别。

**路线图信号**：约束采样、AgentHarness 上下文扩展、多提供商原生支持（StepFun、Bedrock Mantle）是近期方向。自动压缩、Windows 兼容仍是修复优先项。

## 7. 用户反馈摘要

以下从 Issues 评论中提炼真实痛点与使用场景：

- **升级恐慌**：`#6476` 用户反馈从 v0.80.3 升级到 v0.80.6 后自托管模型（vLLM）所有请求立即超时，即使 `httpIdleTimeoutMs` 设置很大。回退版本后恢复。凸显了 **版本回归测试** 的重要性，用户对升级持谨慎态度。
- **自动登出**：`#6686` 用户在 macOS 和 Linux VM 上均遇到 Pi 自动退出 GitHub 登录，且与 v0.80.7 相关，影响 CI/ 自动化场景。虽然标记为 no-action，但用户表达强烈不满。
- **Copilot Enterprise 用户受阻**：`#6768` 用户指出不仅 OpenAPI 返回 421，就连 Anthropic 模型也无法进行上下文压缩。企业用户依赖该功能进行长对话管理，目前无法绕过。
- **Windows 用户困境**：`#6817` 和 `#6619` 反应 Windows 上 find 工具路径模式无效、扩展依赖显示异常。Windows 支持短板明显。
- **缓存与成本困惑**：`#6940` 用户细致分析 OpenRouter 缓存断点问题，指出工具调用轮次后缓存未正确更新，导致 token 浪费。体现高级用户对计费和效率的敏感。
- **扩展体验**：`#6972` 报告扩展 `pi-goal-x` 在多终端会话间“渗透”，影响隔离性，社区呼吁加强沙箱。

**满意度**：大部分已关闭的 Bug 获得用户感谢，但开放性严重问题（如自动压缩、Copilot、llama.cpp）尚未解决，情绪以等待和重复反馈为主。

## 8. 待处理积压

以下为长期未响应或持续待解决的重要 Issue/PR，需维护者关注：

| 类型 | 编号 | 标题 | 创建日 | 最后更新 | 备注 |
|------|------|------|--------|----------|------|
| Issue | [#2557](https://github.com/earendil-works/pi/issues/2557) | `tool_call` `edit` 在编辑冲突时仍触发事件，且扩展无法检测冲突 | 2026-03-24 | 2026-07-22 | 影响扩展开发和冲突处理准确性 |
| Issue | [#5566](https://github.com/earendil-works/pi/issues/5566) | 代码块渲染显示字面反引号而非样式化边框 | 2026-06-09 | 2026-07-22 | 基础的 UI/UX 问题，影响阅读体验 |
| Issue | [#6210](https://github.com/earendil-works/pi/issues/6210) | `/scoped-models` 无法选择含括号的模型 ID（已标记 inprogress） | 2026-07-01 | 2026-07-22 | 已有 inprogress 标签但未见 PR，需加速 |
| Issue | [#6479](https://github.com/earendil-works/pi/issues/6479) | 技能子文件夹不被识别 | 2026-07-10 | 2026-07-22 | 轻微 but 可接受？社区小需求 |
| Issue | [#6768](https://github.com/earendil-works/pi/issues/6768) | Copilot Enterprise 压缩失败（高赞） | 2026-07-17 | 2026-07-22 | 无 PR，企业用户强烈关注 |
| Issue | [#6879](https://github.com/earendil-works/pi/issues/6879) | 自动压缩在超阈值后不触发 | 2026-07-20 | 2026-07-22 | 严重影响长会话，无 PR |
| Issue | [#6817](https://github.com/earendil-works/pi/issues/6817) | Windows find 工具路径模式失效 | 2026-07-19 | 2026-07-22 | 平台兼容性需求 |
| Issue | [#6922](https://github.com/earendil-works/pi/issues/6922) | `llama.cpp` 默认模型启动失败（高赞） | 2026-07-21 | 2026-07-22 | 无 PR，本地模型用户基数大 |
| PR | [#6341](https://github.com/earendil-works/pi/pull/6341) | 约束采样功能 | 2026-07-05 | 2026-07-22 | 已标记 to-discuss，需决策是否合并 |
| PR | [#6216](https://github.com/earendil-works/pi/pull/6216) | Bedrock Mantle 提供者 | 2026-07-01 | 2026-07-22 | 长期开放，需 review |

**建议**：优先处理 `#6879`（自动压缩）、`#6768`（Copilot Enterprise）和 `#6922`（llama.cpp），它们是健康度和口碑的核心堵点。同时 `#2557` 和 `

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

好的，作為一名 AI 智能體與個人 AI 助手領域的開源項目分析師，以下是根據您提供的 LiteLLM (github.com/BerriAI/litellm) GitHub 數據生成的 2026-07-23 項目動態日報。

---

# LiteLLM 項目動態日報 | 2026年7月23日

## 1. 今日速覽

項目今日極度活躍，總計有 **263 次** Issue/PR 更新，主要由大量的 PR 提交和合併活動驅動。Issue 討論區保持健康的新增/關閉比率（45:5），顯示維護者持續關注社區回饋。最引人注目的是，項目正處於大規模的 **Rust 核心遷移** 和 **UI 現代化** 進程中，同時針對多個嚴重的後端穩定性 Bug（如數據丟失、快取溢出、預算繞過）進行了密集的修復。團隊在過去 24 小時內合併/關閉了 67 個 PR，並發布了兩個新版本（v1.95.0-dev.1 和 v1.94.0-rc.3），展現了極高的開發強度和迭代速度。

## 2. 版本發布

- **v1.95.0-dev.1**: 下一個主版本的開發預覽版。除了強調 Docker 鏡像簽名驗證外，無具體變更日誌。建議新功能探索者與開發者使用，但不建議用於生產環境。
- **v1.94.0-rc.3**: 即將發布的 v1.94.0 的第三個候選版本。主要關注點仍是安全性（Docker 簽名驗證）。建議現有用戶在生產環境升級 v1.93.x 前，先在此版本上進行充分測試。

**遷移/注意事項**:
- 兩個版本均無明確指出的破壞性變更，但作為候選版本，建議用戶在升級到生產環境前，務必參考 [官方更新日誌](https://github.com/BerriAI/litellm/releases) 以確認完整變更。
- **安全性提醒**：所有版本均導入 Docker 鏡像簽名，從 v1.94.0-rc.3 及之後版本開始，團隊建議用戶在部署前使用 `cosign` 驗證鏡像完整性。

## 3. 項目進展（過去 24 小時合併/關閉的重要 PR）

團隊在過去 24 小時內合併或關閉了 **67 個 PR**，項目在多個方向取得顯著進展：

- **核心穩定性與適配**：
    - **Anthropic 輸出格式（Output Format）修復**：PR [#34313](https://github.com/BerriAI/litellm/pull/34313) 和 [#34319](https://github.com/BerriAI/litellm/pull/34319) 修復了因無效 Schema 關鍵詞導致的 Anthropic API 調用錯誤，這是對 Cursor 等工具相容性修復的重要組成部分。
    - **Cost Tracking 成本追蹤**：PR [#34046](https://github.com/BerriAI/litellm/pull/34046) 修復了 OpenAI 快取寫入 token 未正確映射到 `prompt cache creation billing` 的問題，確保計費準確性。
    - **Cursor 整合**：PR [#34029](https://github.com/BerriAI/litellm/pull/34029) 使 `/cursor/chat/completions` 端點能正常支持 Cursor 的 Agent 模式，這對 Cursor BYOK 用戶至關重要。

- **後端與性能**：
    - **Pydantic 版本相容性**：修復了與 Pydantic v2 的不相容問題。
    - **HyperDXR/Multi-manager 支援**：增強了對 HyperDXR 部署的支持。
    - **數據庫遷移修復**：修復了數據庫遷移腳本中的邏輯錯誤。

- **UI 現代化**：
    - **Shadcn UI 遷移**：PR [#34303](https://github.com/BerriAI/litellm/pull/34303) 將 Playground 頁面的 `transform-request` 面板從 Antd/Tremor 遷移到 Shadcn UI，減少了依賴，並修復了水平溢出問題。

## 4. 社區熱點

- **🔥 [Feature Request] LiteLLM Rust Migration (Issue #31263)**: [https://github.com/BerriAI/litellm/issues/31263](https://github.com/BerriAI/litellm/issues/31263)
    - **分析**：這是一個引發廣泛討論的重大架構升級議題。使用者對亞毫秒級延遲的承諾表現出極大興趣（14 👍），但評論中也透露出對遷移期間相容性、穩定性以及是否需要整體更換的擔憂。這是影響項目未來性能路線圖的關鍵信號。

- **🔧 [Bug] Usage data lost on client disconnect (Issue #14457)**: [https://github.com/BerriAI/litellm/issues/14457](https://github.com/BerriAI/litellm/issues/14457)
    - **分析**：這是一個已存在近一年的嚴重計費問題，今天仍有用戶回饋。問題描述了當客戶端中斷串流時，LiteLLM 丟失最終 chunk 中的使用資料，導致計費缺口和配額追蹤不完整。這直接影響企業用戶的計費準確性和成本控制。

## 5. Bug 與穩定性

以下為今日報告的 Bug，按嚴重程度排列：

- **嚴重（需立即關注）**：
    - **快取溢出(CRITICAL)** ([Issue #34299](https://github.com/BerriAI/litellm/issues/34299))：當 Redis 連接中斷時，`RedisCache` 會靜默吞噬異常，導致斷路器無法生效，進程陷入不可服務狀態。**已有修復 PR？** 無，但此問題可能觸發整套服務中斷。
    - **預算繞過(CRITICAL)** ([Issue #34238](https://github.com/BerriAI/litellm/issues/34238))：當 Redis 計數器過期後，端用戶預算可被繞過，導致費用失控。**已有修復 PR？** 無，對成本敏感型企業用戶是巨大風險。
    - **團隊刪除後密鑰仍有效** ([Issue #34217](https://github.com/BerriAI/litellm/issues/34217))：`POST /team/delete` 未清理認證快取，導致已刪除團隊的虛擬金鑰仍可被使用。這是安全漏洞。**已有修復 PR？** 無。

- **中等（功能異常）**：
    - **Bedrock `CountTokens` 圖表 400 錯誤** ([Issue #34272](https://github.com/BerriAI/litellm/issues/34272))：在跨區域推理模式下，設定 `CountTokens` 時因前綴被移除而返回 400 錯誤。**已有修復 PR？** 已知修復：PR [#34312](https://github.com/BerriAI/litellm/pull/34312)。
    - **Tool Call IDs 長度超限** ([Issue #34239](https://github.com/BerriAI/litellm/issues/34239))：Bedrock 上 `zai.glm-5` 模型多輪 Tool Calling 因 `toolUseId` 超過 64 字符而失敗。**已有修復 PR？** 無。
    - **OpenAI Reasoning 模型溫度驗證錯誤** ([Issue #34301](https://github.com/BerriAI/litellm/issues/34301))：LiteLLM 錯誤地將 GPT-5.5/5.6 等模型標記為支援溫度參數，導致 API 調用時被提供商拒絕。**已有修復 PR？** 無。
    - **Claude Tool Calling 中斷** ([Issue #19858](https://github.com/BerriAI/litellm/issues/19858))：Claude 模型在使用 Tool Calling 時（特別是在 OpenRouter 和 Vertex 上）出現問題。**已有修復 PR？** 懷疑與 Anhtropic 輸出格式修復（PR #34313, #34319）相關。

## 6. 功能請求與路線圖信號

- **AI 搜索支援** ([Issue #31819](https://github.com/BerriAI/litellm/issues/31819))：用戶請求將 Amazon Bedrock AgentCore Web Search 作為原生搜索提供者整合到 LiteLLM 的 `litellm.search()` 和代理 Web 搜索攔截功能中。這反映了企業用戶對集成安全、可審計的搜索功能的需求。
- **Aliyun AI Search 支援**：類似於 Bedrock AgentCore，用戶也提出了對阿里雲 AI Search 的支援請求，顯示了對多雲環境中原生搜索能力的廣泛需求。
- **Access Group 強化** ([Issue #34296](https://github.com/BerriAI/litellm/issues/34296))：用戶回饋當前的 Access Groups 僅作為「附加授權」而非「允許列表」，無法真正限制模型訪問路徑。這對需要精細化權限控制的企業場景至關重要。

## 7. 用戶回饋摘要

從 Issue 評論中，我們提煉出以下真實用戶痛點：

- **「不當客」的模組導入行為** ([Issue #22159](https://github.com/BerriAI/litellm/issues/22159))：用戶將 LiteLLM 導入時預設發起 HTTP 請求的行為描述為「**hostile**」（有敵意的），認為其緩慢且不必要，應改為惰性加載。這反映了用戶對高性能、可預測行為的嚴苛要求。
- **集群環境下的預算不安全感** ([Issue #26233](https://github.com/BerriAI/litellm/issues/26233))：用戶報告當 `cache_params` 中包含任何鍵時，Redis 環境變數被忽略，導致多 Pod 部署下的消費追蹤中斷。這在生產環境中會直接造成成本失控。
- **對新版本穩定性信心不足** ([Issue #30534](https://github.com/BerriAI/litellm/issues/30534), [Issue #29397](https://github.com/BerriAI/litellm/issues/29397))：升級到 v1.89.0 後快取代碼拋出 `TypeError`，而 `AdaptiveRouter` 在重啟後因統計資料錯誤而崩潰，這些反覆出現的回歸問題讓用戶對新版本穩定性產生擔憂。

## 8. 待處理積壓

- **Issue #14457**: `[Bug]: Usage data lost when streaming responses are terminated early...` 自 2025年9月11日創建，累計 7 條評論，3 個 👍。這是一個影響計費的嚴重問題，雖然有 PR 嘗試修復，但似乎仍未完全解決。建議維護者優先處理。
- **Issue #19858**: `[Bug]: Claude models with tool calling are broken` 自 2026年1月27日創建，累計 5 條評論。Claude Tool Calling 的穩定性問題被反覆提及，雖然今日有相關修復（PR #34313），但該 Issue 尚未關閉，建議跟進確認修復效果。
- **Issue #22159**: `[Bug]: litellm is calling an http GET on module import` 自 2026年2月26日創建，累計 5 條評論。該問題雖然不是崩潰性 Bug，但用戶情緒強烈，建議將此行為改為可選項，以改善用戶體驗和啟動性能。

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于您提供的数据生成的 Temporal 项目动态日报。

---

### Temporal 项目动态日报 2026-07-23

**数据快照:** 2026-07-22 18:00 UTC 至 2026-07-23 18:00 UTC

---

### 1. 今日速览

Temporal 项目本日依然维持极高的开发活跃度，共产生 **62 条** PR 更新，其中 **23 条** 已合并或关闭，**39 条** 仍在待合并状态。尽管当日没有新 Issue 或版本发布，但该 PR 数量远高于行业平均水平，表明核心团队正集中精力进行大规模的代码集成与功能收尾工作。项目无明显停滞或阻塞，健康度良好，正处于“功能冲刺”或“稳定化冲刺”的密集回合并发期。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

今日有 23 个 PR 被合并或关闭，涵盖了功能改进、Bug 修复和测试稳定性等多个方面，标志着项目在关键特性上取得了实质进展。

- **核心功能稳定化 (CHASM & SAA):**
    - CHASM Nexus 操作完成功能回退（[#11028](https://github.com/temporalio/temporal/pull/11028)）已被合并，解决了工作流重置后的完成兼容性问题，弥补了与 HSM 实现的功能差距。
    - 独立活动（SAA）的多个 PR 被合并，包括：解决滚动升级期间的 Token 验证问题（[#11217](https://github.com/temporalio/temporal/pull/11217)）、禁用延迟启动的默认配置（[#11218](https://github.com/temporalio/temporal/pull/11218)）。
- **基础设施与测试改进:**
    - 动态分区客户端重构（[#11132](https://github.com/temporalio/temporal/pull/11132)）已关闭，简化了匹配客户端的代码逻辑，并修正了转发行为。
    - PostgreSQL 测试数据库的清理问题得到修复（[#11215](https://github.com/temporalio/temporal/pull/11215)），提升了 CI 环境的可靠性。
    - 修复了分区缩放功能测试的稳定性问题（[#11221](https://github.com/temporalio/temporal/pull/11221)）。
- **调度器优化:**
    - V2 调度器的 `RecentActions` 存储上限被削减至 5 条（[#11201](https://github.com/temporalio/temporal/pull/11201)）以匹配 V1 行为并优化存储，该 PR 已被合并。

**总结：** 项目在完善“CHASM”和“独立活动”（SAA）两个核心新特性的同时，也在不断修复基础设施缺陷和提升代码质量。今日的合并工作清楚地表明项目正在向稳定版本冲刺。

### 4. 社区热点

本日没有产生大量评论互动的 PR，但以下几个开放 PR 值得关注，它们代表了当前开发的核心焦点：

- **[#11219](https://github.com/temporalio/temporal/pull/11219) fix retry backoff calculation for workflow activities** (#11219 ＃11219): 修复了工作流活动重试间隔计算的溢出 bug。这是一个关键的可靠性修复，防止因特定配置导致的重试异常。
- **[#11224](https://github.com/temporalio/temporal/pull/11224) saa: make heartbeatTimer a SingletonTask** (#11224 ＃11224): 将心跳计时器改为单例任务，防止重复注册。这是对 SAA 机制的进一步优化，旨在提升性能和防止状态错乱。
- **[#11199](https://github.com/temporalio/temporal/pull/11199) activity-parity: allow SAA to be manually completed by ID** (#11199 ＃11199): 允许通过 ID 手动完成独立活动。这是为了实现与现有工作流活动（WFA） API 的“活动对等性”（activity-parity），是用户长期期待的功能。

**核心诉求分析：** 这些 PR 背后反映了开发团队及社区的两个核心诉求：一是**增强系统健壮性**，通过修复溢出和重复注册等隐患；二是**实现功能对等性**，确保新的独立活动（SAA）功能链路上不缺失用户已习惯的操作能力。

### 5. Bug 与稳定性

本日没有新报告的 Bug Issue，但在已合并或待处理的 PR 中，我们识别出以下已修复或正在修复的关键 Bug：

| 严重程度 | Bug 描述 | 状态 | 处理 PR |
| :--- | :--- | :--- | :--- |
| **高** | 工作流活动重试间隔计算在特定配置下会溢出，导致返回零或负值。 | **已修复** (Open PR) | [#11219](https://github.com/temporalio/temporal/pull/11219) |
| **高** | 更新工作流活动（WFA）重试策略时，会丢失 `NonRetryableErrorTypes` 字段。 | **已修复** (Open PR) | [#11214](https://github.com/temporalio/temporal/pull/11214) |
| **高** | 暂停状态下的工作流活动（WFA）在耗尽重试预算后无法被正确终止。 | **已修复** (Open PR) | [#11191](https://github.com/temporalio/temporal/pull/11191) |
| **中** | 独立活动（SAA）Token 在滚动升级阶段验证会失败。 | **已修复** (已合并) | [#11217](https://github.com/temporalio/temporal/pull/11217) |
| **低** | 分区缩放功能测试在随机条件下阵发性失败。 | **已修复** (已合并) | [#11221](https://github.com/temporalio/temporal/pull/11221) |

**结论：** 项目在稳定性方面投入巨大，数个由社区或内部测试发现的高价值 Bug 已得到快速响应和修复，特别是围绕新功能（WFA、SAA）的边界情况。

### 6. 功能请求与路线图信号

以下 PR 体现了正在研发并极有可能被纳入下一版本的关键功能：

- **虚拟时间跳转 (VTS):** [#11220](https://github.com/temporalio/temporal/pull/11220) 和 [#11223](https://github.com/temporalio/temporal/pull/11223) 共同构建了 VTS 功能的多个关键组件，包括“最大跳过”限制 (`max skip`)、“描述”接口 (`Describe`) 和“轮询快进完成” (`Poll fast-forward completion`)。这表明 “Time Skipping” 这一高级开发调试/测试功能已经进入实质性开发阶段。
- **CHASM Nexus 操作百分比灰度发布:** [#10950](https://github.com/temporalio/temporal/pull/10950) 引入了基于命名空间和百分比的灰度发布能力，允许运营商逐步将生产流量切换到 CHASM 实现的 Nexus 操作。这为后续全面启用该特性提供了安全网。
- **独立活动操作指令:** [#11216](https://github.com/temporalio/temporal/pull/11216) 引入了 `history.enableStandaloneActivityOperatorCommands` 配置标志，虽然当前默认为关闭，但这为未来开放独立活动的 Operator 命令（如 Reset、Pause）奠定了基础。

**路线图信号：** 以上 PR 清晰表明，未来版本将重点发布**虚拟时间跳转（VTS）** 功能，并通过**灰度机制**平滑推进 **CHASM** 的全面落地。

### 7. 用户反馈摘要

由于今日无新增 Issue，我们无法从 Issue 评论中提炼新的用户反馈。然而，从 PR 动机中可以推断出以下痛点：

1.  **API 歧义与行为不一致:** PR [#11191](https://github.com/temporalio/temporal/pull/11191) 和 [#11214](https://github.com/temporalio/temporal/pull/11214) 的修复，暗示了用户在使用“暂停”和“更新重试策略”这类操作时，WFA 和 SAA 的行为存在差异或缺陷，这是对开发者体验的直接优化。
2.  **工具链集成成本:** PR [#10817](https://github.com/temporalio/temporal/pull/10817) “添加 V1 调度器版本上限”旨在解决向后兼容问题，这通常是为了方便使用更老 SDK 的工作者集群能平滑过渡，反映了社区在系统升级时的实际运维痛点。

### 8. 待处理积压

以下 PR 在本日数据中被标记为“待处理”，因其创建时间较早或对项目健康度影响较大，建议维护者重点关注：

1.  **[#10817](https://github.com/temporalio/temporal/pull/10817) add workflow version clamp to the V1 scheduler's recorded version** (创建于 2026-06-23): 该 PR 已开放整整一个月，涉及关键的 V1 调度器版本兼容性问题。其长期未合并可能会影响使用旧版调度器的用户进行升级。建议评估状态并推动合并或关闭。
2.  **[#11035](https://github.com/temporalio/temporal/pull/11035) Convert Nexus completion tokens across HSM and CHASM** (创建于 2026-07-13): 这是一个解决 HSM 与 CHASM 切换时的 Token 转换问题的关键 PR。作为两大新架构迁移的核心组件，其状态（仍在 Open）值得关注。

---

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*