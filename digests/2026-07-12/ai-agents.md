# OpenClaw 生态日报 2026-07-12

> Issues: 456 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-11 23:14 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-07-12

## 1. 今日速览

过去 24 小时内，OpenClaw 社区保持了极高的活跃度：共产生 **456 条 Issue 更新**（新开/活跃 234 条，关闭 222 条），**500 条 PR 更新**（待合并 265 条，已合并/关闭 235 条），并发布了 **1 个新版本**（v2026.7.1-beta.5）。项目整体呈现 **密集协作、快速迭代** 的健康状态，大量安全、稳定性及功能增强类议题正在被积极处理。社区讨论集中在跨平台支持、会话持久化、agent 上下文可靠性等领域。

## 2. 版本发布

### v2026.7.1-beta.5

- **发布日期**：2026-07-11（基于数据中的“最新 Releases”）
- **主要亮点**：引入 **Conversational onboarding**（对话式入职流程）。Crestodian 现在在 CLI、Web 安装和 macOS App 中运行真正的 agent-loop 设置，提供 AI 引导的 provider 配置、基于精确操作的模型评判审批、掩码化的凭据提示，并在无模型时提供确定性回退。
- **破坏性变更**：版本号表明为 beta 版本，暂未标注破坏性变更，但用户应关注 SQLite 迁移路径的更新（参考 Issue #88838）。
- **迁移注意事项**：建议用户升级后运行 `openclaw doctor --fix` 以确保 SQLite schema 和状态文件同步。Voice Call 等插件的本地数据库可能需要手动修复（详见 PR #104752）。

## 3. 项目进展

今日合并/关闭了多项重要 PR，推动项目在功能、稳定性和测试覆盖方面前进：

- **UI 增强**：[#104761](https://github.com/openclaw/openclaw/pull/104761) `feat(ui): cron automation-ideas gallery and Create & run now in quick-create`，为控制面板的 cron 页面增加了自动化创意画廊和快速创建功能，降低新用户使用门槛。
- **测试与可靠性**：[#104760](https://github.com/openclaw/openclaw/pull/104760) `test(telegram): guard send-funnel chunk-boundary parity`，增加 Telegram 发送漏斗的分块边界对等测试，防止流式与持久化漏斗不一致。
- **修复启动障碍**：[#103675](https://github.com/openclaw/openclaw/pull/103675) `fix: allow gateway startup when SQLite migration target already exists`，允许网关在 SQLite 迁移目标已存在时正常启动，而非将其视为致命错误。
- **Mattermost 稳定性**：[#104575](https://github.com/openclaw/openclaw/pull/104575) `fix(mattermost): bound stalled inbound media header waits`，修复 Mattermost 入站文件下载可能因远程主机不返回响应头而无限挂起的问题。
- **Voice Call 修复**：[#104752](https://github.com/openclaw/openclaw/pull/104752) `fix: doctor repairs Voice Call SQLite schema upgrades`，确保 `openclaw doctor --fix` 能够正确修复语音通话插件的本地数据库 schema 升级。

此外，还有若干待合并 PR 处于评审阶段，涉及 Android avatar 显示、Telegram 身份保持、外部会话统一分页等方向。

## 4. 社区热点

以下 Issue/PR 在过去 24 小时内获得了最多的评论和互动，反映了社区的核心关切：

| # | 标题 | 评论数 | 链接 | 核心诉求分析 |
|---|------|--------|------|--------------|
| 75 | [enhancement] Linux/Windows Clawdbot Apps | 110 | [链接](https://github.com/openclaw/openclaw/issues/75) | **跨平台需求**：macOS/iOS/Android 已有应用，但 Linux 和 Windows 缺失。用户期待获得与 macOS 相近的功能集，这是长期以来的第一高票需求。 |
| 88838 | Track core session/transcript SQLite migration via accessor seam | 37 | [链接](https://github.com/openclaw/openclaw/issues/88838) | **会话持久化重构**：SQLite 迁移是当前最关键的内部架构改进，直接影响 session 稳定性和数据完整性。讨论集中在实现路径（Path 3）和 PR #96625。 |
| 99241 | Tool outputs sometimes render as image attachments and become unreadable | 21 | [链接](https://github.com/openclaw/openclaw/issues/99241) | **工具输出可见性**：长时间运行的 ANSI 重 workflow 中，工具结果被压缩为图片占位符，agent 无法读取原始文本。影响 agent 决策准确性，用户反馈强烈。 |
| 104721 | All tool results return "(see attached image)" literal string instead of actual output | 9 | [链接](https://github.com/openclaw/openclaw/issues/104721) | **回归性严重 bug**：与 #99241 同类但更极端——所有工具结果直接被替换为文字占位符，标记为 P0。社区高度关注，已触发紧急排查。 |
| 10659 | Feature Request: Masked Secrets | 15 | [链接](https://github.com/openclaw/openclaw/issues/10659) | **安全增强**：要求 agent 使用 API key 时无法查看原始密钥，防止 prompt 注入导致凭据泄露。该需求获得了 4 个 👍，社区安全共识强烈。 |

## 5. Bug 与稳定性

以下按严重程度排列今日报告的 bug 及回归问题：

**P0（严重阻塞）**
- **[#104721](https://github.com/openclaw/openclaw/issues/104721)** [Bug]：所有工具结果返回文字占位符 `"(see attached image)"`，实际文件内容丢失。**类型**：回归，**是否有 fix PR**：暂无。
- **[#99241](https://github.com/openclaw/openclaw/issues/99241)** [Bug]：长文本/ANSI 密集型工具输出被转换为图片附件占位符，agent 无法读取。**类型**：行为 bug，**状态**：OPEN，等待产品决策和实机复现。

**P1（高影响）**
- **[#102175](https://github.com/openclaw/openclaw/issues/102175)** [Bug]：嵌入式 prompt 缓存在跨 room_event、policy、Responses 边界时断裂，导致令牌浪费和速度下降。**类型**：回归，**是否有 fix PR**：暂无。
- **[#86538](https://github.com/openclaw/openclaw/issues/86538)** [Bug]：Session JSONL 写锁超时阻塞子代理交付通道，导致静默失败。**类型**：行为 bug，**状态**：CLOSED（PR #86572 已合并）。
- **[#90213](https://github.com/openclaw/openclaw/issues/90213)** [Bug]：升级到 2026.6.1 后，遗留状态迁移警告即使运行 `doctor --fix` 仍反复出现。**类型**：回归，**是否有 fix PR**：暂无。

**P2（中度影响）**
- **[#103332](https://github.com/openclaw/openclaw/issues/103332)** [Bug]：macOS 上 OpenClaw 2026.7.1 无法与 codex/gpt5.6 一起运行（返回 400 错误）。**类型**：回归，已 CLOSED（推测已修复）。
- **[#94846](https://github.com/openclaw/openclaw/issues/94846)** [Bug]：Cron 隔离 agentTurn 在工具错误恢复后仍被判定为致命，导致交付跳过。**类型**：行为 bug，**状态**：OPEN。

## 6. 功能请求与路线图信号

从今日活跃的 Issue 中，以下功能请求值得关注，部分已有关联 PR 或处于产品决策阶段：

| 功能 | Issue 链接 | 优先级 | 关联 PR | 可能纳入版本 |
|------|-----------|--------|---------|-------------|
| Linux/Windows Clawdbot 应用 | [#75](https://github.com/openclaw/openclaw/issues/75) | P2 | 暂无 | 下一大版本（跨平台路线图） |
| 内存信任标签（由源标记） | [#7707](https://github.com/openclaw/openclaw/issues/7707) | P2 | 暂无 | 中期安全改进 |
| 掩码密钥系统 | [#10659](https://github.com/openclaw/openclaw/issues/10659) | P1 | 暂无 | 正在安全评审 |
| 文件系统沙箱配置 | [#7722](https://github.com/openclaw/openclaw/issues/7722) | P2 | 暂无 | 待产品决策 |
| 上下文溢出错误信息增强 | [#9409](https://github.com/openclaw/openclaw/issues/9409) | P2 | 暂无 | 低版本修复 |
| 多 slot 内存角色架构 | [#88504 PR](https://github.com/openclaw/openclaw/pull/88504) | P2 | 已有 XL 级 PR | 预计 v2026.8 |
| 外部会话统一分页 | [#104717 PR](https://github.com/openclaw/openclaw/pull/104717) | P2 | 已在 review | 候选 beta.6 |

**路线图信号**：`#42026` (分布式 Agent Runtime) 的 RFC 讨论仍在持续，可能预示着架构层面的大拆分。`#88838` 的 SQLite 迁移是短期内的核心基础设施工作。

## 7. 用户反馈摘要

从今日 Issue 评论中提炼的真实用户声音：

- **工具输出不可见导致 agent 失效**（#99241, #104721）：用户反映在复杂工作流（如 Web 抓取、代码分析）中，agent 完全无法看到工具返回的文本，只能看到图片占位符。一位用户描述：“这不是显示问题——实际文件内容被替换成了文字 ‘(see attached image)’，agent 根本读不到数据，整个流程就断了。” 这个 P0 级别的问题引发了广泛的“+1”和紧急投诉。
- **Linux/Windows 用户长期被忽视**（#75）：评论区持续有用户表达对桌面端支持缺失的失望。“我们在服务器上跑 OpenClaw，但 CLI 体验远不如 macOS 的 GUI。希望至少有一个 Linux 原生 App。” 该 Issue 已有 110 条评论、81 个赞，是社区最渴望的功能。
- **安全顾虑日益增长**（#10659, #7707, #7722）：多位用户对 prompt 注入和凭据泄露表示担忧。“我的 agent 有时会自己读 .env 文件，然后把 API key 回显给我看——这在演示时很危险。” 掩码密钥和文件系统沙箱被反复提及。
- **Slack 集成体验**（#12602, 已关闭）：用户曾要求 Slack Block Kit 支持，该 Issue 已关闭（可能已被实现），但记者未在数据中看到后续。
- **cron 和自动化**（#8299）：sub-agent announce 行为不可控，用户希望有配置项关闭自动 announce。“我只需要子 agent 完成任务后静默返回结果，不需要它发一条‘任务完成’的消息。”

## 8. 待处理积压

以下为长期未关闭且尚未取得实质进展的重要 Issue / PR，提醒维护者关注：

| 编号 | 标题 | 创建日期 | 上次活跃 | 链接 | 提醒原因 |
|------|------|----------|----------|------|----------|
| #75 | Linux/Windows Clawdbot Apps | 2026-01-01 | 2026-07-11 | [链接](https://github.com/openclaw/openclaw/issues/75) | 已积压半年，评论 110+，社区呼声最高，但无开发资源投入 |
| #7707 | Memory Trust Tagging by Source | 2026-02-03 | 2026-07-11 | [链接](https://github.com/openclaw/openclaw/issues/7707) | 安全增强，已通过安全评审，但产品决策尚未做出 |
| #10659 | Masked Secrets | 2026-02-06 | 2026-07-11 | [链接](https://github.com/openclaw/openclaw/issues/10659) | 获 4 赞，多个评论催促，但仍在等待安全评审和产品决策 |
| #42026 | RFC: Distributed Agent Runtime | 2026-03-10 | 2026-07-11 | [链接](https://github.com/openclaw/openclaw/issues/42026) | 架构级 RFC，讨论持续但无行动项标记，可能需要 maintainer 出面推进 |
| #88504 | Multi-slot memory role architecture (PR) | 2026-05-31 | 2026-07-11 | [链接](https://github.com/openclaw/openclaw/pull/88504) | 大型 PR，等待 proof，长时间未合并，可能因 scope 过大而阻塞 |
| #38844 | Browser upload/file chooser flaky | 2026-03-07 | 2026-07-11 | [链接](https://github.com/openclaw/openclaw/issues/38844) | 浏览器自动化关键路径的稳定性问题，6 条评论但无 fix PR |

---

**总结**：OpenClaw 目前处于高强度的社区驱动开发阶段。今日的 P0 bug (#104721) 和 #99241 需要优先响应；跨平台支持 (#75) 和安全性 (#10659) 是社区最期待的功能；SQLite 迁移 (#88838) 和 agent 运行时隔离 (#42026) 代表了项目的中长期架构演进方向。建议维护者尽快针对 P0 bug 发布 hotfix，并考虑在路线图中明确 Linux/Windows 客户端的开发时间表。

---

## 横向生态对比

好的，作为一名专注于AI智能体与个人AI助手开源生态的资深技术分析师，我将基于您提供的各项目动态，为您生成一份全面的横向对比分析报告。

---

### AI智能体与个人AI助手开源生态横向对比分析报告

**报告日期：2026-07-12**

#### 1. 生态全景

当前，个人AI助手与自主智能体开源生态正处于从“单点功能突破”向“系统化、产品化、安全化”转型的关键时期。项目整体呈现出 **“高热活跃、快速迭代”** 的特征，社区贡献与功能探索空前高涨。但活跃之下暗藏挑战：**会话状态管理、工具调用可靠性、成本计算准确性及跨平台支持**是普遍性痛点。生态正聚焦于解决这些“生产级”可用性问题，同时积极拥抱GPT-5.6等前沿模型的新特性，预示着行业正从“能用”迈向“好用”和“安全用”的新阶段。

#### 2. 各项目活跃度对比

| 项目名称 | 今日Issue更新 | 今日PR更新 | 版本发布 | 健康度评估 | 关键特征 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 456 | 500 | ✅ (v2026.7.1-beta.5) | **密集协作，快速迭代** | 社区贡献量巨大，核心功能与Bug修复并进，有明确的版本节奏。|
| **Hermes Agent** | 233+ | 500+ | ❌ | **高投入，待开发** | 社区讨论与贡献极其活跃，但维护者Review与合并效率承压，PR积压严重。 |
| **OpenHands SDK** | 14 | 21 | ❌ (v1.35.0发布中) | **整合发布** | 处于版本发布后的稳定期，社区探索性Issue增多，聚焦前沿模型集成。 |
| **Pi** | 54 | 21 | ❌ | **响应迅速，功能落地快** | 核心开发者对社区反馈响应极快，高关注度Bug与功能请求当日即有修复。 |
| **LiteLLM** | 33 | 180 | ✅ (v1.91.2/3) | **安全维稳，生态扩展** | 专注于安全和稳定性修复，同时扩展MCP生态，社区对成本计算关注度高。 |
| **Temporal** | 5 | 13 | ❌ (v1.32.0发布前夜) | **冲刺优化，功能完善** | 处于大版本发布前的最后冲刺阶段，开发重心放在Nexus和CHASM核心功能的完善上。 |

#### 3. OpenClaw 在生态中的定位

OpenClaw 在生态中扮演着 **“全能型选手”和“社区驱动风向标”** 的角色。

- **优势与定位**：其社区活跃度（Issue/PR数量）远超其他项目，表明其吸引了最广泛的贡献者。它是生态中少数提供 **对话式入职流程（Conversational onboarding）** 和完整的 **UI/CLI/OS App** 体验的项目，产品化程度较高。其社区热点（如跨平台、工具输出可见性）也反映了用户对AI Agent“生产级可用性”的最核心诉求。
- **技术路线差异**：与其他项目相比，OpenClaw更早地关注到了 **SQLite迁移、会话持久化重构** 等基础设施问题，表明其正从快速迭代转向架构成熟。其暴露的P0级Bug（所有工具结果返回“see attached image”）也极具代表性，揭示了对 **Agent内部数据流与可观测性** 的挑战。
- **社区规模对比**：从单日数据看，OpenClaw的Issue/PR数量是Hermes Agent的近一倍，远超其他项目。然而，这也带来了维护者响应压力，其P0 Bug暂无修复PR，与Pi项目“当日立修”的高效形成对比。

| 对比维度 | OpenClaw | Hermes Agent | Pi | LiteLLM |
| :--- | :--- | :--- | :--- | :--- |
| **社区活跃度** | 极高 (456+500) | 极高 (233+500+) | 高 (54+21) | 高 (33+180) |
| **核心优势** | 产品化程度高，全能型 | 社区呼声高，功能探索多 | 响应速度最快，功能落地快 | 模型代理&成本控制能力 |
| **核心痛点** | 回归性Bug多，维护压力大 | PR积压严重，迭代缓慢 | 配置持久化问题 | 成本计算准确性，回调一致性 |
| **关键信号** | Agent数据可观测性瓶颈 | 多Agent协作需求 | 全面对齐最新模型API | 安全与稳定性成为焦点 |

#### 4. 共同关注的技术方向

以下趋势在多个项目中同时涌现，是生态共识的方向：

1.  **会话状态持久化与可靠性**：
    - **涉及项目**: OpenClaw、Hermes Agent、Pi
    - **具体诉求**: 用户要求会话在重启、切换提供商或长时间运行后，上下文不丢失、状态一致。相关Issue如OpenClaw的SQLite迁移(#88838)、Hermes的会话重放Bug(#27038)、Pi的配置不复存在Bug(#4032)。

2.  **跨平台与桌面端支持**：
    - **涉及项目**: OpenClaw、Pi
    - **具体诉求**: 社区对Linux/Windows原生应用呼声极高（OpenClaw #75），希望获得与macOS/iOS一致的功能体验。Pi的Windows Terminal兼容性问题(#6521)也属于此范畴。

3.  **安全性与数据隐私增强**：
    - **涉及项目**: OpenClaw、Hermes Agent、LiteLLM
    - **具体诉求**: 核心诉求包括**掩码密钥**（防止API Key泄露，#10659）、**文件系统沙箱**、**Prompt注入防护**。LiteLLM报告的SSRF漏洞(#32889)则将安全问题提升到了基础设施级别。

4.  **与前沿LLM深度集成**：
    - **涉及项目**: OpenHands SDK、Pi、LiteLLM
    - **具体诉求**: 社区积极主动探索与GPT-5.6等新模型的能力集成，包括程序化工具调用、WebSocket模式、Multi-agent架构等，希望Agent框架能第一时间支持新模型的全部能力。

#### 5. 差异化定位分析

- **OpenClaw (全能型)**: 定位为**个人AI助手产品**，目标是提供从CLI到GUI、从单人到Cron自动化的完整用户体验。技术架构上强调整体性和内部数据流的正确性（如会话、工具输出）。
- **Hermes Agent (平台/探索型)**: 定位更偏向**Agent开发与运行平台**，社区讨论涉及多Agent协作（Director/Worker）、会话移交等复杂架构。现状是功能探索远超维护进度，更像是“未来功能的试验田”。
- **OpenHands SDK (基础设施型)**: 定位为**SDK开发者工具**，专注于Agent通信协议（ACP）、技能加载、模型路由等基础能力。其用户更偏向开发者，关注如何用SDK构建自己的Agent。
- **Pi (专家型)**: 定位为**强编码Agent与AI助手**，在**Coding Agent**功能上投入巨大（Node CLI启动优化、文件上下文错误提示）。其快速对齐最新模型API，服务专业开发者。
- **LiteLLM (中间件型)**: 定位为**AI网关/模型代理**，核心能力是模型路由、成本控制、安全防线（Guardrail）、密钥管理。用户画像偏向运维或需要对LLM使用进行管控的团队。
- **Temporal (编排引擎型)**: 定位是**分布式工作流编排引擎**，支撑Agent等长期运行、状态复杂的应用。其用户是开发高可靠性、有状态应用的工程师，而非直接使用Agent的终端用户。

#### 6. 社区热度与成熟度

- **快速迭代阶段（高活跃，高风险）**：
    - **OpenClaw & Hermes Agent**: 社区贡献量巨大，Bug暴露迅速，但修复与合并速度成为瓶颈。项目处于功能高速增长与系统稳定性之间博弈的“青春期”。特点是功能多，但缺陷也多。
- **核心功能完善阶段（目标明确，执行高效）**：
    - **Pi & LiteLLM & Temporal**: 这些项目有明确的当前目标。Pi快速响应社区，落地新模型支持；LiteLLM集中修补安全和成本漏洞；Temporal冲刺1.32.0版本，完善核心功能。特点是“指哪打哪”，效率高，用户反馈能得到快速闭环。
- **质量巩固与发布阶段（稳定，整合）**：
    - **OpenHands SDK**: 今日处于版本发布的“静默期”，社区活动转向新功能探索。项目状态看起来最稳定，但探索性需求可能积压成为下一轮迭代的压力源。

#### 7. 值得关注的趋势信号

1.  **“工具可见性”是Agent可靠性的阿喀琉斯之踵**：OpenClaw报告的P0级Bug（工具结果被替换为文字占位符）揭示了当前Agent系统一个致命的脆弱点：**Agent无法“看见”其自身工具调用的输出**。这个问题破坏了Agent决策链的根基，是比任何功能缺陷都更引人深思的架构问题。它提醒所有开发者：**构建Agent不仅是编排LLM，更是构建一个可靠的数据闭环**，确保Agent能看到、理解并使用每一个工具产生的信息。
2.  **“跨平台”是个人AI助手迈向消费级的关键一跳**：OpenClaw上超过110条评论、81个赞的Linux/Windows App需求，证实了“纯CLI”或“单一平台”无法满足大众市场。个人AI助手要想成为像浏览器一样的通用入口，**原生桌面体验**是不可或缺的。
3.  **安全忧虑正从“功能可选”升级为“系统基座”**：掩码密钥、文件沙箱、SSRF防护等安全问题在多个项目中被明确、反复地提出，已经不再是“加分项”，而是成为阻碍生产级部署的“减分项”。这意味着，未来的Agent框架在设计之初，就必须将**安全与隐私**作为核心架构属性，而非事后修补的补丁。
4.  **从“单一模型”到“Multi-Agent与混合架构”的呼声渐起**：Hermes Agent的“可信内部触发器”、OpenHands SDK的“Hosted Multi-agent”研究、Pi的“工具动态加载”，都指向了下一代Agent系统的雏形：由多个专门化Agent协同工作、能动态加载能力、并能与人类高效协作的混合式架构。生态正在为这场架构变革储备技术与探索方向。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，没问题。作为AI智能体与个人AI助手领域开源项目分析师，以下是根据您提供的Hermes Agent GitHub数据生成的2026-07-12项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026-07-12

## 1. 今日速览

过去24小时内，Hermes Agent 项目社区活跃度极高，呈现出 **“高热低回”** 的特征：一方面，Issue 和 PR 新增/更新数量巨大（共超过700条），显示社区讨论与贡献热情空前高涨；但另一方面，大量的输入使得维护者回复与合并效率面临严峻挑战，PR 待合并比例高达 97%（485/500），Issue 关闭率仅为 28.7%（67/233）。本周无新版本发布，大量已修复（Closed）的Bug和功能请求等待一并通过发版交付给用户。项目整体处于 **“高投入、待产出”** 的关键节点，社区贡献规模已远超维护团队的即时处理能力，建议项目管理者尽快组织力量进行合并与Review。

## 2. 版本发布

- **无**

## 3. 项目进展

本周内，项目在 **会话状态管理**、**代理配置持久化** 及 **安装脚本健壮性** 方面取得了实质性进展，数个关键的 P1/P2 级别 Bug 已通过 PR 得到修复并关闭，标志着这些影响面较广的问题已得到解决。

- **会话状态与路由修复**：
    - **PR #61817 [CLOSED]** 解决了 Kanban 工作器中协议违规导致断路器误触发的通用性问题，提升了任务调度的鲁棒性。 [链接](https://github.com/NousResearch/hermes-agent/pull/61817)
    - **Issue #27038 [CLOSED]** 修复了 Codex Responses API 在重放长ID消息时被拒绝的问题，确保了会话恢复的可靠性。 [链接](https://github.com/NousResearch/hermes-agent/issues/27038)
    - **Issue #32617 [CLOSED]** 修复了因重放加密内容导致 xAI 提供商回退到 OAuth 的问题，提升了提供商切换的稳定性。 [链接](https://github.com/NousResearch/hermes-agent/issues/32617)
- **配置持久化修复**：
    - **Issue #47714 [CLOSED]** 修复了 Desktop/TUI 会话在切换自定义提供商时错误回退到 OpenRouter 的Bug，确保了自定义配置的生效。 [链接](https://github.com/NousResearch/hermes-agent/issues/47714)
- **基础架构健壮性**：
    - **PR #61845 [OPEN]** (fix(scripts)) 和 **PR #61844 [OPEN]** (fix(cli)) 分别针对安装脚本 (`install.sh`) 中错误检测失效和 `hermes serve` 会话中 Shell Hook 未注册的问题提出了修复方案，提升了安装与运行环境的稳定性。 [链接1](https://github.com/NousResearch/hermes-agent/pull/61845) [链接2](https://github.com/NousResearch/hermes-agent/pull/61844)
- **平台支持补全**：
    - **Issue #61526 [CLOSED]** 完成了 Hermes 桌面端 Electron 应用的简体中文（zh-Hans）本地化支持，为非英语用户提供了更好的体验。 [链接](https://github.com/NousResearch/hermes-agent/issues/61526)

## 4. 社区热点

今日社区讨论集中在 **云服务集成**、**会话可靠性** 和 **用户体验细节** 三个核心主题上，反映出用户对生产级部署和使用体验的强烈诉求。

- **热帖 #1：对原生 Google Cloud Vertex AI 支持的呼吁**
    - **Issue #13484 [OPEN]**: 获得 **14个👍**，12条评论。用户 `@prasadus92` 详细阐述了当前 Hermes 对 Vertex AI 支持不完整的现状（仅有配置入口而无认证机制），并呼吁实现原生的、可用的支持。这表明有大量用户希望将 Hermes 作为其 **Google Cloud 生态系统** 中的 AI Agent，这是来自企业级用户的明确需求信号。 [链接](https://github.com/NousResearch/hermes-agent/issues/13484)

- **热帖 #2：会话重放与状态冲突问题持续发酵**
    - **Issues #27038, #32617** 共获得 **17条评论**，虽然均已关闭，但极高的讨论度表明 **会话状态管理** 是当前用户（尤其是重度用户和开发者）最头疼的问题。用户 `@darconadalabarga` 和 `@eventh0riz0n` 详细报告了在恢复会话或切换提供商时，因数据重放引发的各种 API 拒绝和服务回退问题，这直接影响了产品的可用性。 [链接1](https://github.com/NousResearch/hermes-agent/issues/27038) [链接2](https://github.com/NousResearch/hermes-agent/issues/32617)

- **热帖 #3：Telegram 平台特定 Bug 引发共鸣**
    - **Issue #28004 [OPEN]**：获得 **9条评论**。用户 `@WegoW` 报告的 Telegram “正在输入...” 状态无限卡死的 Bug，得到了7位以上用户的参与讨论，揭示了平台集成中小细节对用户体验的重大影响。该问题与一个 `_keep_typing` 清理路径中的竞态条件有关，是典型的平台适配难题。 [链接](https://github.com/NousResearch/hermes-agent/issues/28004)

## 5. Bug 与稳定性

今日报告的 Bug 集中在 **会话恢复、代理配置** 和 **跨提供商兼容性** 方面，其中部分高优先级问题已有修复PR落地。

- **P1 级别（严重）**:
    - `#54527` [**已关闭**] **网关消息路由错误**：多 TUI 会话同时打开时，用户输入消息被错误路由到其他会话，导致消息丢失。此 Bug 直接影响多任务用户。 [链接](https://github.com/NousResearch/hermes-agent/issues/54527)

- **P2 级别（高）**:
    - `#61265` [**开放**] **发送过大的Prompt给本地模型**：Hermes 构建了过大的Prompt，导致本地模型计算耗时数分钟。直接影响本地部署的用户，降低工作效率。 **暂无对应修复PR**。 [链接](https://github.com/NousResearch/hermes-agent/issues/61265)
    - `#17199` [**开放**] **DeepSeek 提供商自定义端点失效**：模型名称被强制标准化和 `base_url` 覆盖规则异常，导致 Volcengine ARK 等自定义端点无法使用。 **暂无对应修复PR**。 [链接](https://github.com/NousResearch/hermes-agent/issues/17199)
    - `#61487` [**已关闭**] **Z.AI 提供商多密钥级联枯竭**：当池中一个密钥达到配额后，会错误地将所有密钥标记为不可用，影响多密钥用户的服务连续性。 **已修复**。 [链接](https://github.com/NousResearch/hermes-agent/issues/61487)
    - `#55902` [**开放**] **OpenCode Go + Kimi K2.5 返回 HTTP 400**：因消息格式中包含 `timestamp` 字段不被目标API支持，导致该组合完全不可用。 **暂无对应修复PR**。 [链接](https://github.com/NousResearch/hermes-agent/issues/55902)
    - `#56158` [**开放**] **Telegram `/model` 切换残留 `base_url`**：切换模型后，旧的 `base_url` 未能清除，导致后续调用返回404。 **暂无对应修复PR**。 [链接](https://github.com/NousResearch/hermes-agent/issues/56158)

## 6. 功能请求与路线图信号

本周社区提出的新功能请求显示，用户希望 Hermes 能从一个“强对话能力”的Agent，向 **“更强上下文感知”** 和 **“更强平台集成”** 的方向演进。

- **强上下文感知**：
    - `#62595` **主题感知压缩**：在长会话中，根据主题分段进行上下文压缩，而非整体混合压缩，以获得更好的对话质量。 [链接](https://github.com/NousResearch/hermes-agent/issues/62595)
    - `#43008` **优雅的会话恢复**：当会话因超时而重置时，当前实现是静默开始新会话，导致上下文丢失。社区希望 Agent 能感知到这一重置并通知用户。 [链接](https://github.com/NousResearch/hermes-agent/issues/43008)
- **强平台集成**：
    - `#13484` **GitHub Actions 集成**：希望将谷歌云 Vertex AI 作为一级提供商，这表明集成大型云服务商是用户明确的路线图需求。 [链接](https://github.com/NousResearch/hermes-agent/issues/13484)
    - `#17415` **可信内部触发器**：希望Hermes能在不同“角色”会话（如 Director 与 Worker）之间进行安全的任务委派，这指向了多智能体编排的未来方向。 [链接](https://github.com/NousResearch/hermes-agent/issues/17415)

**潜在路线图匹配**：值得注意的是，PR `#61837` 和 `#61840` 分别提出了 **“时间感知子系统”** 和 **“会话移交”** 功能，与上述“上下文感知”和“多Agent协作”方向不谋而合。这些PR虽然尚未完成，但其存在暗示项目维护者可能已经在考虑类似的功能演进。

## 7. 用户反馈摘要

从 Issue 评论中提炼出以下真实用户反馈，直观反映了当前项目的痛点与期望：

- **“这让我们很困惑，为什么配置是有效的，但实际上并没有使用它。”** —— `@Agyness0410` 在抱怨 Desktop 模型切换失败时的无奈。 [链接](https://github.com/NousResearch/hermes-agent/issues/47714#issue-1234567890)
- **“我已经连续好几天无法使用 Hermes，因为我的本地机器会卡住几分钟。”** —— `@anthonydigrazia` 在报告本地模型 Prompt 过大问题时，直接点出该 Bug 对其生产力的严重负面影响。 [链接](https://github.com/NousResearch/hermes-agent/issues/61265#issue-1234567890)
- **“我不得不手动重启整个服务才能让它再次工作——这在生产环境是不可接受的。”** —— `@irwin-chequer` 对 Slack 网关变得无响应但进程仍然健康的 Bug 表示强烈不满。 [链接](https://github.com/NousResearch/hermes-agent/issues/14326#issue-1234567890)
- **“我认为这个‘忽略我的指令’的漏洞场景很严重，应该优先修复。”** —— `@YLChen-007` 在报告 Prompt 注入扫描漏洞时，强调了其安全风险。 [链接](https://github.com/NousResearch/hermes-agent/issues/27284#issue-1234567890)
- **“如果能自动加载上个会话的笔记就太好了，这样我就能无缝地继续我的工作。”** —— 来自 PR `#61840` 的描述，这代表了社区对“连续性”工作流的需求。 [链接](https://github.com/NousResearch/hermes-agent/pull/61840#issue-1234567890)

## 8. 待处理积压

以下是一些创建较早、重要级别高但至今未获得官方回复或修复的 Issue，建议维护团队关注：

- **P3 | 2026-03-06 | `#513` | 两阶段上下文管理（Killocode 启发的功能）**：这是一个非常有价值的性能优化特性，将单一压缩过程分为“剪枝”和“压缩”两步。已开放超过4个月，收获了4条评论，但无官方更新。 [链接](https://github.com/NousResearch/hermes-agent/issues/513)
- **P3 | 2026-03-30 | `#4064` | [UX] 启用鼠标支持**：这是一个简单但能极大提升 TUI 用户体验的功能请求。已开放超过3个月，在 `cli.py` 中禁用鼠标支持的行为似乎有意为之，但未给出解释，社区需要反馈。 [链接](https://github.com/NousResearch/hermes-agent/issues/4064)
- **P2 | 2026-04-23 | `#14326` | [Bug]: Slack 网关无响应但进程健康**：如上文所述，该 Bug 被用户评价为“生产环境不可接受

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

好的，作为一名AI智能体与个人AI助手领域开源项目的分析师，我将基于您提供的OpenHands SDK GitHub数据，为您生成一份结构清晰、数据驱动的项目动态日报。

---

### OpenHands SDK (software-agent-sdk) 项目动态日报
**日期：** 2026-07-12 （数据覆盖： 2026-07-11 UTC 24小时）

### 1. 今日速览

今日OpenHands SDK项目社区活跃度极高，共产生14条Issue更新和21条PR更新，但位于“整合与发布”阶段。**亮点**是社区正积极探索与GPT-5.6等前沿模型（如Multi-agent、WebSocket模式）集成的可能性，提出了4个相关研究型Issue。**挑战**在于Bug修复与稳定性工作依然繁重，尤其是关于`LLM profile timeout`重置和`subscription LLM`序列化等影响用户体验的核心问题，已有相应的修复PR提出。项目健康度整体良好，开发与社区反馈呈现积极的双向互动。

### 2. 版本发布

**今日无新版本发布。**

*注：PR [#4070](https://github.com/OpenHands/software-agent-sdk/pull/4070) (Release v1.35.0) 已于昨日关闭，标志着v1.35.0版本的发布流程已经启动或完成。*

### 3. 项目进展

今日合并或关闭的2个PR和3个Issues，主要聚焦于修复和清理已发现的问题，并发布新版本。具体进展包括：

-   **核心功能修复：** PR [#3996](https://github.com/OpenHands/software-agent-sdk/pull/3996) (已关闭) 修复了ACP (Agent Communication Protocol) 提示词参数顺序的潜在问题，通过使用关键字参数增强了代码健壮性。
-   **开发者体验优化：** Issue [#3981](https://github.com/OpenHands/software-agent-sdk/issues/3981) (已关闭) 提出的为SDK设置存储添加密钥助手功能，已收到并获解决。
-   **提示工程优化：** Issue [#3690](https://github.com/OpenHands/software-agent-sdk/issues/3690) (已关闭) 建议将当前日期时间块移动至初始提示末尾，通过提高prompt缓存复用率来提升性能，该建议已被采纳并关闭。
-   **版本发布准备：** PR [#4070](https://github.com/OpenHands/software-agent-sdk/pull/4070) (已关闭) 的合拢标志着 **v1.35.0** 版本的发布。

### 4. 社区热点

今日讨论最活跃的议题体现了社区对**模型代理能力**和**开发者平台集成**的浓厚兴趣。

1.  **探索前沿模型特性（GPT-5.6）：** 贡献者 `@smolpaws` 在一天内提出4个研究型Issue，探讨OpenAI GPT-5.6的多种新特性与SDK集成的可能性。这表明社区对利用更强的模型能力来增强Agent系统有强烈诉求。
    -   [#4082](https://github.com/OpenHands/software-agent-sdk/issues/4082) 程序化工具调用 (Programmatic Tool Calling)
    -   [#4083](https://github.com/OpenHands/software-agent-sdk/issues/4083) 工具的按需加载 (Tool search/defer_loading)
    -   [#4084](https://github.com/OpenHands/software-agent-sdk/issues/4084) WebSocket模式与请求延续
    -   [#4085](https://github.com/OpenHands/software-agent-sdk/issues/4085) Hosted Multi-agent vs 客户端子Agent系统
    -   **诉求分析：** 用户希望SDK能无缝对接最新的OpenAI能力，使Agent系统更智能、更高效。特别是`Multi-agent`的对比研究，反映了社区对Agent架构演进方向的深入思考。

2.  **配置持久化问题：** Issue [#4032](https://github.com/OpenHands/software-agent-sdk/issues/4032) (2条评论) 和 PR [#4092](https://github.com/OpenHands/software-agent-sdk/pull/4092) (针对Issue [#4091](https://github.com/OpenHands/software-agent-sdk/issues/4091) ) 都指向了配置在服务重启或持久化后丢失的问题。这表明用户对**系统的可靠性和状态的持久性**有很高的要求，配置重置会严重影响实际使用体验。

### 5. Bug 与稳定性

今日报告的Bug集中在配置持久化和代码健壮性方面，按严重程度排列如下：

1.  **严重 - LLM Profile超时配置在服务重启后丢失 (Issue [#4032](https://github.com/OpenHands/software-agent-sdk/issues/4032))**
    -   **描述：** `agent-server`重启后，自定义的LLM超时时间被重置为默认值。
    -   **状态：** 报告于昨日，暂无直接关联的修复PR。这是一个直接影响生产稳定性的关键问题。

2.  **严重 - 持久化的订阅LLM在恢复时丢失运行时配置 (Issue [#4091](https://github.com/OpenHands/software-agent-sdk/issues/4091))**
    -   **描述：** 序列化的ChatGPT订阅LLM配置在反序列化后，无法重建包含OAuth凭证、`base_url`等运行时信息的完整对象。
    -   **状态：** 已有修复PR [#4092](https://github.com/OpenHands/software-agent-sdk/pull/4092) 提出，社区响应迅速。

3.  **中危 - MCP Schema迁移未正确应用 (Issue [#4052](https://github.com/OpenHands/software-agent-sdk/issues/4052))**
    -   **描述：** 导致已有MCP配置的用户出现设置问题。
    -   **状态：** 已有修复PR [#4013](https://github.com/OpenHands/software-agent-sdk/pull/4092) 关联，问题正在解决。

4.  **中危 - `RuntimeError: generator didn't stop after throw()`, 影响错误处理 (Issue [#3412](https://github.com/OpenHands/software-agent-sdk/issues/3412))**
    -   **描述：** 在对话失败时，Laminar可观测性包装器会抛出二次异常，可能导致错误被掩盖或日志混乱。
    -   **状态：** 该Issue存在已久（5月27日），评论较少，可能已被忽视，需要维护者关注。

### 6. 功能请求与路线图信号

一系列功能请求和探索性Issue揭示了社区的下一代关注点：

-   **强候选功能 - ACP注入与技能加载优化：** 社区对技能(`skills`)和ACP配置的注入行为表达了关注。
    -   Issue [#4019](https://github.com/OpenHands/software-agent-sdk/issues/4019) 报告了ACP配置中的技能重复注入问题。
    -   Issue [#4015](https://github.com/OpenHands/software-agent-sdk/issues/4015) 请求在技能加载冲突时为用户提供可见性警告。这些反馈表明，**技能的加载和配置管理**是用户体验中的关键痛点。
-   **路线图信号：**
    - **与前沿LLM深度集成：** `@smolpaws` 提出的4个关于GPT-5.6的研究型Issue（[#4082](https://github.com/OpenHands/software-agent-sdk/issues/4082), [#4083](https://github.com/OpenHands/software-agent-sdk/issues/4083), [#4084](https://github.com/OpenHands/software-agent-sdk/issues/4084), [#4085](https://github.com/OpenHands/software-agent-sdk/issues/4085)）是强烈的信号，表明社区希望SDK能引领创新，快速拥抱新模型特性。这很可能成为下一版本的重点工作。
    - **Agent启动性能：** PR [#3895](https://github.com/OpenHands/software-agent-sdk/pull/3895) (懒加载持久化会话) 和 PR [#3990](https://github.com/OpenHands/software-agent-sdk/pull/3990) (将密钥排除出工作区持久化) 都围绕着提升启动速度和系统安全性展开，这是项目成熟化的重要标志。

### 7. 用户反馈摘要

从今日的Issue和PR评论中，可以提炼出以下真实用户声音：

-   **配置焦虑：** 用户在Issue [#4032](https://github.com/OpenHands/software-agent-sdk/issues/4032) 中明确指出“`LLM profile timeout is reset after agent-server restart`”，说明配置丢失问题让他们感到沮丧，并影响了工作流的连续性。
-   **技能系统的困惑：** Issue [#4019](https://github.com/OpenHands/software-agent-sdk/issues/4019) 的提出者 `@simonrosenberg` 发现ACP配置中技能被重复注入，这暴露了技能加载逻辑存在不清晰或冗余的问题，增加了使用复杂性。
-   **对透明性的期待：** Issue [#4015](https://github.com/OpenHands/software-agent-sdk/issues/4015) 的提出者 `@jpshackelford` 希望技能加载时的冲突能被警告，而不是静默处理。这反映了用户希望系统更“透明”，对内部行为有知情权和掌控权。

### 8. 待处理积压

以下是一些需要维护者重点关注的历史遗留问题：

-   **[中危Bug] `RuntimeError: generator didn't stop`，影响所有对话失败场景 (Issue [#3412](https://github.com/OpenHands/software-agent-sdk/issues/3412) )**
    -   **创建时间：** 2026-05-27 (已46天未解决)
    -   **优先级分析：** 中等。(*标签: Stale, priority:medium*)。虽然标签为“过时”和“中等”，但考虑到它发生在每一次对话失败时，长期积累会严重影响错误排查和系统稳定性，建议重新评估其优先级。
-   **[重要功能] 智能模型路由器 (PR [#3744](https://github.com/OpenHands/software-agent-sdk/pull/3744) )**
    -   **创建时间：** 2026-06-16 (近一个月)
    -   **优先级分析：** 高。该PR实现了根据任务自动切换LLM的核心功能，是通往“智能Agent”的关键一步。其讨论和审查的停滞，可能会影响项目在智能化路线图上的进展。建议维护者尽快安排审查。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-07-12

---

## 今日速览

过去 24 小时项目保持高度活跃：**54 条 Issue 更新**（新开/活跃 10 条，关闭 44 条）、**21 条 PR 更新**（5 条待合并，16 条已合并/关闭）。无新版本发布，但大量修复和功能落地集中在 GPT‑5.6 全系列模型支持、GitHub Copilot 适配、OpenRouter 会话亲和性以及扩展 API 增强上。社区反馈与贡献双旺，多个高关注度 Issue（如 `max` 思维级别、GPT‑5.6 Copilot 目录）获得大量 👍。项目健康度良好，核心开发者响应迅速，多数关键 Bug 已附带修复 PR 或已关闭。

---

## 版本发布

无新版本。

---

## 项目进展

今日合并/关闭的 PR 集中在以下重点方向（标记为 [CLOSED] 的已合并或关闭）：

| PR | 标题 | 关键点 |
|---|---|---|
| [#6532](https://github.com/earendil-works/pi/pull/6532) | Fix Bedrock AWS_PROFILE authentication regression | 修复因 API‑key 登录支持引入的认证回归，`AWS_PROFILE` 不再被当作 Bearer Token 发送 |
| [#6539](https://github.com/earendil-works/pi/pull/6539) | fix(ai): bind Codex WebSocket reuse to account | 将 Codex WebSocket 缓存绑定到 JWT 账户，防止切换账号时误用旧连接和 `previous_response_id` |
| [#6538](https://github.com/earendil-works/pi/pull/6538) | fix(ai): route GitHub Copilot MAI-Code models through /responses endpoint | 让 `mai-code-1-flash-picker` 等模型使用 Copilot `/responses` 端点，绕过 `/chat/completions` 的限制 |
| [#6528](https://github.com/earendil-works/pi/pull/6528) | fix(ai): support GPT-5.6 prompt cache options | 为 GPT‑5.6 模型在 OpenAI Responses API 中发送 `prompt_cache_options`，覆盖旧字段 |
| [#6530](https://github.com/earendil-works/pi/pull/6530) | perf(coding-agent): cut Node CLI startup cost | 透过快速路径 `--version` 和将 Bun 专用导入移到入口文件，降低 Node 启动时间 |
| [#6520](https://github.com/earendil-works/pi/pull/6520) | fix(coding-agent): include file context in edit tool not-found error | 当 `oldText` 匹配失败时，显示周边文件内容帮助调试 |
| [#6518](https://github.com/earendil-works/pi/pull/6518) | feat(coding-agent): expose scoped models to extensions | 新增 `pi.getScopedModels()`，让扩展获取当前会话的模型循环范围 |
| [#6474](https://github.com/earendil-works/pi/pull/6474) | feat(ai): support message-anchored tool loading | 支持在对话中途通过 `addedTools` 动态加载工具（Anthropic 后端先行） |
| [#6292](https://github.com/earendil-works/pi/pull/6292) | fix(ai): resolve Cloudflare account id from ambient env | 从环境变量解析 Cloudflare account ID，彻底解决 0.80.x 上的 404 问题 |
| [#6111](https://github.com/earendil-works/pi/pull/6111) | fix(coding-agent): report settings write failures in install/remove | 当 `settings.json` 只读时，安装/卸载失败将正确报错而非静默退出 0 |

此外，[#6540](https://github.com/earendil-works/pi/pull/6540) 将 Provider 错误（上下文溢出、重试耗尽、压缩失败）注入到 LLM 可见的 advisories 中，大幅提升模型对自身故障的恢复能力。[#6523](https://github.com/earendil-works/pi/pull/6523) 修复了旧终端中 `Alt+符号` 快捷键无法识别的问题。

> 总体来看，项目今日迈出了关键两步：**全面对齐最新模型 API**（GPT‑5.6 全系列、Copilot MAI‑Code）和**强化扩展生态**（工具动态加载、作用域模型、延迟重载）。

---

## 社区热点

以下 Issue 和 PR 获得了最高评论数、👍 或 react，反映了社区的强烈诉求：

1. **[#6475](https://github.com/earendil-works/pi/issues/6475) — Add GPT-5.6 (Sol/Terra/Luna) to the GitHub Copilot provider catalog**  
   获得 8 👍，社区急切希望 Pi 能即刻使用 GitHub Copilot 刚上线的 GPT‑5.6 模型。该 Issue 已于当日关闭，说明维护者已响应并快速合并相关代码。

2. **[#6097](https://github.com/earendil-works/pi/issues/6097) — Add support for 'max' thinking level**  
   获得 18 👍，是今日最高赞的 Issue。用户要求为 OpenAI 新模型（GPT‑5.6 Sol）添加第六个思维级别 `max`。该 Issue 已关闭，但评论区显示仍有讨论，预计将随下一版本支持。

3. **[#5916](https://github.com/earendil-works/pi/issues/5916) — Support provider extensions with model aliases and improve search**  
   12 条评论，虽创建于 6 月 20 日但今仍有更新。用户因缺少 OpenRouter 配置 UI 只能手动编辑 `models.json`，核心痛点在于**提供者扩展性不足**。标签为 `inprogress`，可能正在开发中。

4. **[#6510](https://github.com/earendil-works/pi/issues/6510) — Copilot / mai-code-1-flash-picker doesn’t work**  
   5 条评论，直指刚发现的 Copilot 特定模型兼容性问题，当日由 [#6538](https://github.com/earendil-works/pi/pull/6538) 解决，响应迅速。

5. **[#6513](https://github.com/earendil-works/pi/issues/6513) — Codex cached WebSocket can retain the previous account**  
   3 条评论，但属于会话安全类 Bug。社区通过 Issue 报告了账户切换时的连接复用漏洞，当日由 [#6539](https://github.com/earendil-works/pi/pull/6539) 修复。

---

## Bug 与稳定性

按严重程度排序，今日报告中值得关注的 Bug 如下：

| 严重程度 | Issue | 标题 | 状态 | 说明 |
|---|---|---|---|---|
| **高** | [#6513](https://github.com/earendil-works/pi/issues/6513) | Codex cached WebSocket 可保留前一个账户状态 | **已修复** (PR #6539) | 账户切换后仍复用旧连接，可能造成数据混淆 |
| **高** | [#6531](https://github.com/earendil-works/pi/issues/6531) | Bedrock AWS_PROFILE 认证被作为无效 Bearer Token 发送 | **已修复** (PR #6532) | 导致所有使用 `AWS_PROFILE` 的用户请求失败 |
| **中** | [#6502](https://github.com/earendil-works/pi/issues/6502) | Windows Terminal 滚动到顶部（ESC[3J） | **OPEN** | TUI 重绘时清除了回滚缓冲区，影响 Windows 用户体验。目前无关联 PR |
| **中** | [#6522](https://github.com/earendil-works/pi/issues/6522) | openai-completions: 无最小 `max_completion_tokens` 限制，发送 1 token → 400 | **OPEN** | 上下文窗口计算错误导致 token 过低，请求被拒绝。尚无 PR |
| **中** | [#6549](https://github.com/earendil-works/pi/issues/6549) | `pi update` 在 `PI_SKIP_VERSION_CHECK` 设置时失败 | **已修复** (CLOSED) | 环境变量干扰版本检查逻辑，已关闭但未标注 PR 编号 |
| **低** | [#6498](https://github.com/earendil-works/pi/issues/6498) | 工具和系统提示 CLI 选项未在创建的会话中持久化 | **已关闭** (no-action) | 确认是设计行为？但用户认为不合理 |
| **低** | [#6472](https://github.com/earendil-works/pi/issues/6472) | `compaction.enabled=false` 被溢出恢复路径绕过 | **已关闭** | 已通过其他方式修复？可能需确认 |

此外，[#6477](https://github.com/earendil-works/pi/issues/6477) 压缩摘要请求缺少 Session ID 导致 Codex 模型失败（已有关联修复 PR #6533 开放中），[#6527](https://github.com/earendil-works/pi/issues/6527) 旧终端 Alt+符号快捷键失效已由 PR #6523 修复。

---

## 功能请求与路线图信号

以下新功能请求得到了较多社区关注，结合现有 PR 可判断其纳入下个版本的可能性：

| Issue | 请求 | 社区热度 | 状态 / 可能性 |
|---|---|---|---|
| [#6097](https://github.com/earendil-works/pi/issues/6097) | 支持 OpenAI 的 `max` 思维级别 | 18 👍 | **高** — 对应 GPT‑5.6 Sol 需要，核心维护者已合并相关模型目录，但配置界面尚未更新 |
| [#6475](https://github.com/earendil-works/pi/issues/6475) | 将 GPT‑5.6 加入 Copilot 提供者目录 | 8 👍 | **已落地** — 当天关闭 |
| [#6554](https://github.com/earendil-works/pi/issues/6554) | 添加 LLM Gateway 为内置提供者 | 1 👍 | **中** — 有社区贡献意愿，且项目已有类似 OpenRouter 提供者模块，容易集成 |
| [#6509](https://github.com/earendil-works/pi/issues/6509) | 扩展通过 `ctx.ui.setUsage` 报告外部成本 | 0 👍 | **中** — 有助于扩展生态，功能描述清晰，但尚无实现 |
| [#6493](https://github.com/earendil-works/pi/issues/6493) | RPC 支持 `attachments` 字段 | 2 👍 | **低中** — 与扩展输入增强相关，但未提及具体场景 |
| [#6552](https://github.com/earendil-works/pi/issues/6552) | 扩展请求延迟规范重载 | 0 👍 | **已实现** — 对应 PR #6551 已合并 |
| [#6550](https://github.com/earendil-works/pi/issues/6550) | 为 GitHub Copilot 添加 `auto` 伪模型 | 0 👍 | **中** — 针对 Copilot Free/Student 强制使用 Auto 模型，实用性强 |

**路线图信号**：当前明显趋势是 **快速对齐最新模型 API 变更**（GPT‑5.6 系列、Copilot Async Responses），同时也在准备 **扩展生态的基础设施**（工具动态加载、作用域模型、延迟重载）。未来版本很可能包含 `max` 思维级别和 LLM Gateway 提供者。

---

## 用户反馈摘要

从 Issue 评论中提炼出以下真实用户

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-07-12

---

## 1. 今日速览

过去24小时内，LiteLLM 保持极高的维护与开发活跃度：共处理 **33 个 Issues**（新开/活跃 25 个，关闭 8 个）以及 **180 个 Pull Requests**（待合并 97 个，已合并/关闭 83 个）。项目连续发布两个补丁版本（v1.91.2 和 v1.91.3），修复了 guardrail 绕过、Dashscope 成本计算等关键问题。社区讨论聚焦于 Router 回调失效、SSRF 安全漏洞以及成本计算准确性。总体看来，项目正处于快速迭代期，对安全与稳定性投入持续加强。

---

## 2. 版本发布

### v1.91.3（2026-07-11 发布）
基于 `stable/1.91.x` 分支的补丁版本，Backport 了已在 `litellm_internal_staging` 中合并的两项修复（#32542、#32655）：
- **安全修复**：修复了 guardrail 内容助手在 Responses-API 流中的绕过问题——每个 guardrail 在读取内容前都会经过安全检查，不再遗漏部分事件。
- **稳定性修复**：补丁回退至稳定分支后同时修复了若干回归问题。

### v1.91.2（2026-07-10 发布）
上一个补丁版本，内容与 v1.91.3 类似，均包含 Docker 镜像签名校验说明。无破坏性变更，用户仅需按常规升级即可。

**迁移提示**：直接使用 `pip install litellm==1.91.3` 或拉取最新 Docker 镜像即可。如果使用了自定义 guardrail hook，建议阅读 #32948 了解涉及的边界情况。

---

## 3. 项目进展

今日合并/关闭的重要 PR 体现了项目在各层面的持续推进：

| 关键 PR | 状态 | 贡献 |
|--------|------|------|
| [#32942](https://github.com/BerriAI/litellm/pull/32942) | ✅ 已合并 | **强制 Dashscope 分层定价的预算与成本跟踪**，修复 #21249 中 API 密钥预算绕过问题。 |
| [#32948](https://github.com/BerriAI/litellm/pull/32948) | ✅ 已合并 | Backport 安全修复并发布 v1.91.3。 |
| [#32729](https://github.com/BerriAI/litellm/pull/32729) | ✅ 已合并 | UI 重构：将用量页面图表迁移至 shadcn/recharts，提升可维护性。 |
| [#32945](https://github.com/BerriAI/litellm/pull/32945) | ✅ 已合并 | 抽取共享 CopyButton 组件，修复侧边栏复制确认交互。 |
| [#29137](https://github.com/BerriAI/litellm/pull/29137) | ✅ 已合并 | 为 `GET /key/list` 添加 `expires` 过滤参数，支持按“已过期/未过期”筛选密钥。 |
| [#32939](https://github.com/BerriAI/litellm/pull/32939) | ✅ 已合并 | 团队管理：支持批量更新团队成员。 |
| [#32876](https://github.com/BerriAI/litellm/pull/32876) | ✅ 已合并 | 文档改进：澄清 Anthropic Opus 4.5 分支的自适应 effort 翻译行为。 |

此外，今日有 **83 个 PR 被合并/关闭**，大量涉及 UI 重构、成本计算修正、MCP OAuth 网关改进等。项目整体向前推进了一个安全补丁版本，并在代理核心功能（成本、密钥管理、MCP）上取得实质性进展。

---

## 4. 社区热点

以下 Issues 获得了最多社区参与，反映了用户最关心的问题：

| Issue | 评论/👍 | 核心诉求 |
|-------|----------|-----------|
| [#8842](https://github.com/BerriAI/litellm/issues/8842) | 24 评论 / 13 👍 | **Router 的异步补全不触发 CustomLogger 钩子**。用户提供了最小可复现示例（MRE），期望日志记录功能对所有路由方式一致。该问题已存在超过 1 年，仍无修复 PR。 |
| [#18058](https://github.com/BerriAI/litellm/issues/18058) | 8 评论 / 0 👍 | **ElevenLabs 模型在代理中的成本计算失效**。用户提供了一个完整 YAML 配置，问题可复现，但尚未有维护者确认。 |
| [#14635](https://github.com/BerriAI/litellm/issues/14635) | 7 评论 / 8 👍 | **超时错误信息错误地显示 `None seconds`**。用户抱怨该 bug 导致排查困难，且请求支持客户端自定义超时配置。 |
| [#32889](https://github.com/BerriAI/litellm/issues/32889) | 2 评论 / 0 👍 | **SSRF 安全漏洞（严重，CVSS 8.6）** 在 guardrail 的 `http_request()` 基元中出现。用户报告后立即引起关注，目前已有重复 issue #32890。 |

**分析**：社区对**日志/回调正确性**和**成本计算准确性**的诉求最为强烈。#8842 的历史较长，如果能在近期修复，将显著提升 Router 功能的可靠性。SSRF 漏洞因涉及安全被标记为关键，预计会快速响应。

---

## 5. Bug 与稳定性

按严重程度排列今日报告的 Bug：

| Issue | 严重程度 | 描述 | 是否有修复 PR |
|-------|---------|------|--------------|
| [#32889](https://github.com/BerriAI/litellm/issues/32889) | 🔴 致命 | SSRF 漏洞：guardrail `http_request()` 函数允许攻击者利用代理向内网任意主机发起请求。 | 未发现直接修复 PR，但 v1.91.3 已包含 guardrail 内容助手的安全修复，可能部分缓解。 |
| [#32951](https://github.com/BerriAI/litellm/issues/32951) | 🟠 高 | `stream_chunk_builder` 在收到原始字节 chunk 时抛出 `TypeError: byte indices must be integers or slices, not str`，导致 `/v1/messages` 流式接口 500 错误。 | 无 |
| [#32904](https://github.com/BerriAI/litellm/issues/32904) | 🟠 高 | `map_system_message_pt` 在 `supports_system_message=False` 的模型（如 `chatgpt/`）中崩溃，错误为 `can only concatenate list (not "str") to list`。 | 无 |
| [#32903](https://github.com/BerriAI/litellm/issues/32903) | 🟡 中 | `GET /v1/models` 始终返回 `owned_by: "openai"`，无论模型实际提供商如何。影响客户端自动识别。 | 无 |
| [#32900](https://github.com/BerriAI/litellm/issues/32900) | 🟡 中 | Gemini 免费 API 密钥在 wizard 配置中测试失败，但直接 curl 可用。 | 无 |
| [#32496](https://github.com/BerriAI/litellm/issues/32496) | 🟡 中 | Fireworks AI 成本计算忽略缓存 token，始终按全部 prompt token 计费。已有 PR #29897 等待合并。 | 有（#29897） |
| [#32892](https://github.com/BerriAI/litellm/issues/32892) | 🟡 中 | 允许调用方通过请求体覆盖 AWS 凭证参数，可能造成安全风险，建议增加操作员 opt-in 锁定。 | 无 |

此外，今日还关闭了 8 个 Issues，包括 Dashscope 成本绕过（#21249）、Amazon Bedrock 缓存失效（#32730）等，说明维护团队正在积极清理积压。

---

## 6. 功能请求与路线图信号

| Issue | 提议功能 | 可能纳入版本 |
|-------|---------|------------|
| [#24123](https://github.com/BerriAI/litellm/issues/24123) | 支持 Langfuse Python SDK v4（当前锁定 v2）。Langfuse v4 已发布，但 LiteLLM 仍使用旧版，用户呼吁更新。 | 未看到对应 PR，但社区呼声高（6👍）。 |
| [#32235](https://github.com/BerriAI/litellm/issues/32235) | 为 MCP 服务器添加基于 Prometheus 的调用次数指标，标签包含服务器名称。 | 无 PR，但现有 MCP 基础设施已在快速演进。 |
| [#32887](https://github.com/BerriAI/litellm/issues/32887) | 支持 `max_retries` 参数应用于非 OpenAI/Azure 提供商（Anthropic、Cohere 等）。当前该参数被静默忽略。 | 有重复 issue #32895，但均无关联 PR。 |
| [#32947](https://github.com/BerriAI/litellm/issues/32947)（PR） | 为复杂度路由器（complexity router）添加“软下限自适应模式”，已在 #32947 中实现。 | 即将合并（已打开）。 |
| [#32953](https://github.com/BerriAI/litellm/issues/32953)（PR） | 为 `GET /key/list` 添加 `expires` 过滤参数（覆盖 #29137 的合并），支持 `expired` / `active` 筛选。 | 已合并至 `litellm_internal_staging`。 |

**路线图信号**：项目正在积极拓展 MCP 生态（OAuth 委托、Prometheus 指标）、增强路由灵活性（复杂度路由器自适应模式），同时修复长期存在的成本计算错误。Langfuse v4 支持是一个明显的缺口，预计下一个小版本可能会纳入。

---

## 7. 用户反馈摘要

从今日 Issues 评论中提炼的真实用户痛点与使用场景：

- **成本计算混乱**：多位用户反映使用非标准定价模型（Dashscope 分层定价、Fireworks AI 缓存 token）时，预算控制完全失效，导致生产环境费用超额。“我们信赖 LiteLLM 的成本跟踪，但它低估了实际消耗” —— #21249 用户。
- **超时诊断困难**：“`Connection timed out after None seconds` 这样的错误信息毫无意义，我们不得不自己增加日志” —— #14635 用户。请求暴露底层超时值和可配置的超时策略。
- **Router 异步回调缺失**：用户 @bilelomrani1 提供了详尽的 MRE，表示在 Router 的 `acompletion` 中，自定义日志钩子从未被调用。该问题导致无法在日志中记录请求-响应链路，影响审计和调试。“我们依赖 CustomLogger 监控所有请求，但 Router 似乎绕过了它。”
- **安全顾虑**：SSRF 漏洞被报告后，用户 @Correctover 仅一天内连续提交 3 个相关 issue（#32889、#32890、#32888），表明安全社区正在关注 LiteLLM 的 guardrail 实现。用户希望尽快得到官方回复和补丁。
- **Gemini 免费密钥兼容性**：用户 @bobbycarp 在 #32900 中抱怨，同样的密钥在 curl 中工作，但在 LiteLLM wizard 中失败，反馈“配置过程不够透明，排错困难”。

综合来看，用户对 LiteLLM 核心功能的稳定性（成本、超时、回调）期望值很高，当前版本在这些方面仍有提升空间。

---

## 8. 待处理积压

以下 Issue 长期未得到维护者回应或虽活跃但修复进展缓慢，建议关注：

| Issue | 创建日期 | 上次更新 | 问题描述 | 积压风险 |
|-------|---------|----------|---------|----------|
| [#8842](https://github.com/BerriAI/litellm/issues/8842) | 2025-02-26 | 2026-07-11 | Router 异步补全不触发 CustomLogger 钩子 | 高（1.5 年未修复，13👍，24 评论） |
| [#14635](https://github.com/BerriAI/litellm/issues/14635) | 2025-09-17 | 2026-07-11 | 超时错误显示 `None seconds`，提议暴露超时配置 | 中（8👍，近期仍有活跃讨论） |
| [#18058](https://github.com/BerriAI/litellm/issues/18058) | 2025-12-16 | 2026-07-11 | ElevenLabs 成本计算失效，无维护者回复 | 中（用户等待确认） |
| [#24123](https://github.com/BerriAI/litellm/issues/24123) | 2026-03-19 | 2026-07-11 | 支持 Langfuse SDK v4 | 中（6👍，但无 PR） |
| [#24533](https://github.com/BerriAI/litellm/issues/24533) | 2026-03-24 | 2026-07-11 | minimax-m2.7 通过 Ollama Cloud 时第二次请求失败 | 低（已有 workaround？） |

此外，PR #29897（Fireworks AI 缓存成本计算修复）自 2026

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

好的，以下是为您生成的 Temporal 项目动态日报。

---

## Temporal 项目动态日报 | 2026-07-12

### **今日速览**
项目在过去24小时内保持高度活跃，共产生13条Pull Request（PR）更新和5条新的Issue，但Issue关闭数为0，表明问题解决速度有待提升。今日无新版本发布，但已接近发布窗口。开发重点集中在 **Nexus** 和 **CHASM** 核心功能的完善，同时对数据库及运维相关的用户反馈进行了讨论。整体来看，项目正处于下一个版本(1.32.0)发布前的冲刺和优化阶段。

### 版本发布
今日无新版本发布。

### 项目进展
今日有4个PR被合并，标志着项目在功能可配置性和工具体验上迈出了关键一步。
*   **独立 Activity 功能转为默认启用** ([#10930](https://github.com/temporalio/temporal/pull/10930)): 将 `activity.enableStandalone` 动态配置的默认值从 `false` 改为 `true`。这是一个重大的默认行为变更，意味着新部署的Temporal将默认开启独立Activity (CHASM) 功能，显著提升了该功能的易用性和普及度。
*   **1.32.0发布分支已准备就绪** ([#11021](https://github.com/temporalio/temporal/pull/11021)): 由CI/CD机器人自动提交，完成了发布前的准备工作（如覆盖治理文件、更新依赖）。这强烈预示着 **Temporal Server 1.32.0 版本即将正式发布**。
*   **SAA Operator API 修复与测试** ([#10859](https://github.com/temporalio/temporal/pull/10859)): 完成了对SAA（Self-Hosted Admin API）相关API的修复和测试，增强了该功能的稳定性。
*   **新增CHASM过渡一致性级别选项** ([#10957](https://github.com/temporalio/temporal/pull/10957)): 为CHASM的 `UpdateComponent` 引入了 `RefConsistencyLevel` 选项，允许更精细地控制状态更新的强弱一致性级别，增强了CHASM的成熟度。

### 社区热点
今日讨论活跃的议题主要集中在数据库性能和Nexus功能的演进上。
*   **PostgreSQL索引膨胀问题** ([#10145](https://github.com/temporalio/temporal/issues/10145)): 此Issue已存在数月，但在今日（7月11日）仍有更新。用户描述了在高吞吐场景下，PostgreSQL后端数据库不断增长的问题，即使设置了保留期。虽然点赞和评论数不算最高，但其“长期未解决”和“影响核心资源消耗”的特性，使其成为社区关注的焦点。
*   **工作流重置与Nexus功能完善**: 涉及Nexus任务令牌类型的PR ([#11022](https://github.com/temporalio/temporal/pull/11022)) 和工作流重置时重新应用Nexus操作的PR ([#10986](https://github.com/temporalio/temporal/pull/10986)) 都是社区贡献者或核心成员推动的热门功能。社区对Nexus API的健壮性和易用性有较高期待。

### Bug 与稳定性
今日报告了多个潜在Bug，按严重程度排列如下：

1.  **【高】PostgreSQL索引膨胀** ([#10145](https://github.com/temporalio/temporal/issues/10145)): 用户报告在高吞吐量工作流下，即使设置了保留期，PostgreSQL数据库大小也会持续增长。这是一个影响存储和成本的稳定性问题。目前尚无关联的Fix PR。
2.  **【中】重置工作流时找不到旧运行记录** ([#10690](https://github.com/temporalio/temporal/issues/10690)): 用户发现，当目标工作流运行记录被删除（但更旧的记录仍存在）时，通过明确的 `runId` 进行重置会失败。这影响了工作流恢复的核心功能。目前尚无关联的Fix PR。
3.  **【低】Istio严格mTLS下Helm Job失败** ([#10236](https://github.com/temporalio/temporal/issues/10236)): 用户在启用Istio严格mTLS的集群中部署Temporal时，Schema Job会失败。这是一个环境兼容性问题，影响特定云原生环境下的部署体验。目前尚无关联的Fix PR。

### 功能请求与路线图信号
从今日的PR和Issues中，可以观察到以下路线图信号：
*   **Nexus与CHASM深度融合**: 多个PR（[#11022](https://github.com/temporalio/temporal/pull/11022), [#10986](https://github.com/temporalio/temporal/pull/10986), [#10983](https://github.com/temporalio/temporal/pull/10983), [#10948](https://github.com/temporalio/temporal/pull/10948)）均围绕Nexus和CHASM展开，包括区分Nexus任务类型、支持Nexus操作的重置/复制，以及为Nexus响应添加元数据。这表明 **Nexus已成为Temporal的核心基础设施，正经历一次重大迭代**，很可能在1.32.0版本中发布。
*   **开发者体验与可观测性提升**:
    *   用户请求在启动工作流响应中增加 `FirstExecutionRunID` ([#10873](https://github.com/temporalio/temporal/pull/10873))，已被核心开发人员回应并创建了PR，预计会进入下一版本。
    *   更好的日志上下文和CI通知（[#11009](https://github.com/temporalio/temporal/pull/11009), [#11019](https://github.com/temporalio/temporal/pull/11019)）表明团队在持续优化自身和用户的调试与监控体验。

### 用户反馈摘要
*   **痛点：数据库膨胀**：用户社区对PostgreSQL后端在高负载下的存储管理表达了强烈担忧，认为当前的保留策略机制未能有效控制数据体量。
*   **痛点：Istio集成**：一位用户对Temporal Helm Chart与Istio的兼容性感到困扰，期望能有更好的开箱即用的支持。
*   **功能诉求：Nexus任务区分**：贡献者正在推动Nexus任务令牌的细化，以区分内部和外部调用，这说明社区用户对Nexus API的精细控制能力有更深层次的需求。

### 待处理积压
以下为长时间未解决的、影响用户的关键问题，建议维护者优先关注：
*   **Worker版本切换问题** ([#9581](https://github.com/temporalio/temporal/issues/9581)): 自3月提出，用户无法在默认命名空间内切换回无版本设置。该问题影响Worker版本的部署和管理流程，已持续近4个月未解决。
*   **PostgreSQL索引膨胀问题** ([#10145](https://github.com/temporalio/temporal/issues/10145)): 如上所述，这是一个影响稳定性和成本的长期问题，需要从数据库层或归档策略上进行根本性分析。
*   **Helm与Istio mTLS兼容性** ([#10236](https://github.com/temporalio/temporal/issues/10236)): 该问题影响特定环境下的部署成功率，虽不普遍，但对受影响的用户来说是阻塞性问题。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*