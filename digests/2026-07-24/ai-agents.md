# OpenClaw 生态日报 2026-07-24

> Issues: 351 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-23 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，这是为您生成的 OpenClaw 项目动态日报。

---

# OpenClaw 项目日报 - 2026-07-24

## 1. 今日速览

今日项目处于**高度活跃**状态。Issue 和 PR 的更新量均达到近期峰值（共 851 条），显示出社区极高的参与度。然而，项目健康度呈现两极分化：一方面有多个大型 PR 推进核心功能的架构重构（如 Cron 统一、Gateway 状态管理）；另一方面，大量 P0/P1 级别的严重 Bug 被报告，主要集中在会话状态丢失、数据迁移损坏和网关启动崩溃等关键路径上，需要维护团队优先响应。P0 级别的 Bug 数量增加，表明近期版本更新可能引入了需要紧急修复的回归问题。

## 2. 版本发布

- **无新版本发布。** 上一个版本仍为 2026.7.1 系列，但 `2026.7.2-beta.3` 版本的相关问题（如 #111519）已被报告，表明新版本正在测试中。

## 3. 项目进展

今日有多项关键 PR 被合并或推进，主要集中在核心架构的重构和稳定性修复上：

- **Cron 任务核心重构（#113165）：** 维护者 @steipete 提交了一个大型 PR，作为“一切皆 Cron”计划（#110950）的第 4 阶段，将`心跳（Heartbeat）`任务转换为独立的 Cron 作业。这是对项目调度系统的一次根本性改造。
- **Gateway 运行时状态统一（#113157）：** 另一个大型重构 PR，将 Gateway 中分散的聊天运行状态合并为统一管理，旨在减少生命周期管理遗漏和状态不一致的问题。
- **自动回复配置管道拆分（#113154，已合并）：** 对项目中最复杂的函数之一 `dispatchReplyFromConfigInner`（超过 2800 行）进行了解耦拆分，大大降低了未来维护和审查的难度。
- **数据库兼容性修复（#113151，已合并）：** 修复了在 Node.js 22.22.3 和 24.15.0 上，旧版 v13 Agent 数据库无法通过 SQLite 迁移的问题，这直接影响用户升级。
- **Telegram 富文本列表支持（#113158）：** 为 Telegram 频道增加了原生 Markdown 列表（包括任务列表）渲染支持，提升了消息的视觉表现力。
- **多客户端实时遥测（#113084）：** 新增了在 WebUI 和 Android 客户端中显示聊天回合的实时耗时和 Token 消耗的功能，改善了长任务期间的进度透明度。

## 4. 社区热点

- **跨平台客户端需求呼声最高（#75）：** 该 Issue 以 **115 条评论**和 **80 个点赞**高居榜首。用户 @steipete 的需求非常明确：项目已有 macOS、iOS 和 Android 客户端，但缺少 **Linux 和 Windows** 的原生桌面应用。这代表了社区对更广泛平台支持的强烈渴望。
- **“子代理静默丢失”问题引发深度讨论（#44925）：** 该 Bug 报告详细描述了多个子代理任务失败且无通知、无重试的场景，获 **22 条评论**。用户对这一严重影响可用性的“静默失败”模式表达了高度关注，期望系统能提供更强的恢复和通知机制。
- **“会话初始化冲突”问题（#102020）：** 在 Signal 和 Telegram 等跨渠道场景中，会话的第二条消息就会失败，引发 **15 条评论**。这暴露了多通道下会话管理状态的复杂性和脆弱性，是渠道间一致性的关键阻碍。

**链接：** [#75](https://github.com/openclaw/openclaw/issues/75) | [#44925](https://github.com/openclaw/openclaw/issues/44925) | [#102020](https://github.com/openclaw/openclaw/issues/102020)

## 5. Bug 与稳定性

今日报告的 Bug 数量和严重性均处于高位，以下为最严重的几个：

- **[P0] 网关启动崩溃（#108435）：** 升级到 2026.7.1 后，在 Systemd、Ollama 和手动启动三种方式下，Gateway 均无法启动。**严重性：** 最高，直接导致服务不可用。**已有用户提供详细日志，但暂无修复 PR 明确关联。**
- **[P0] 升级迁移导致数据损坏和渠道错误（#90378）：** 从 5.28 升级到 6.1 时，Cron 存储从 JSON 静默迁移到 SQLite，但未保留旧配置，并导致新任务默认模式出错。**严重性：** 极高，影响生产环境数据完整性。**有 Linked PR 在跟踪。**
- **[P0] Novita LLM 提供商模型列表无法加载（#103532，已关闭）：** 新集成的 Novita LLM 提供商因无法获取模型列表而无法使用。该问题已被标记为一个明确的可修复问题。**严重性：** 高，阻断特定提供商的使用。**问题已被修复并关闭。**
- **[P1] 子代理结果静默丢失（#44925）：** 多个子代理任务在完成通知、超时等环节失败，结果被静默丢弃。**严重性：** 高，导致任务不可靠且难以排查。**暂无关联的修复 PR。**
- **[P1] 原生 Anthropic 路径的 thinking 模块引发 400 错误（#94228）：** 使用原生 Anthropic API 进行长对话时，会永久性“卡住”，每次新回复都返回 `Invalid signature in thinking block` 错误。**严重性：** 高，导致特定集成路径完全不可用。**暂无关联修复 PR。**

## 6. 功能请求与路线图信号

- **“一切皆 Cron”统一调度计划稳步推进（#110950）：** 继今日的大型 PR #113165 实现“心跳转 Cron”后，该项目的主要方向愈发清晰。预计未来可以统一所有定时任务（心跳、Watcher、脚本）的配置和管理界面。
- **技能权限清单标准化（#12219）：** 社区对安全性的诉求日益强烈。该 Feature Request 提出了一个 `skill.yaml` 标准，用于声明技能所需的权限，用户可在安装前审查。这与近期强化安全性的 PR（如 #101981）趋势一致，可能会被提升优先级。
- **会话 TTL 自动清理（#45390）：** 用户报告会话持续运行 6 天以上，积累了 17w+ Token 并导致超时，建议增加会话最大生命周期的配置。鉴于 Context 膨胀是普遍痛点，此功能有较大概率被采纳。

## 7. 用户反馈摘要

- **痛点：** “子代理结果无缘无故丢失，没有任何提示，调试非常困难。”（源自 #44925）。这种“静默失败”模式是用户对系统可靠性不满的核心来源。
- **使用场景：** 大量用户将其用于 Telegram、Discord 等群聊场景的自动化成员。配置的复杂性（如 #41372 中提到的 25 项发现）是自托管用户的主要抱怨点。
- **不满意：** 升级体验糟糕。数据迁移不透明（#90378）、破坏性变更导致服务崩溃（#108435, #98672）是社区负面反馈的主要来源。用户期望更平滑、更安全的升级通道。
- **满意：** 社区对项目核心团队的响应速度基本满意，尤其是 @steipete 等核心维护者提交的大型重构 PR，表明项目在长期架构健康方面的投入，获得了社区技术用户的认可。

## 8. 待处理积压

以下为长期未关闭或未得到有效响应的严重问题，提请维护者关注：

- **💎 飞书消息工具“轮询字段污染”问题（#42820）：** 创建于 2026-03-10，影响飞书渠道发送文件。工具 Schema 中的轮询相关字段会误导模型，导致文件发送失败。标签为 `P1` 和 `platinum hermit`，但长期处于 `needs-live-repro` 状态。**链接：** [#42820](https://github.com/openclaw/openclaw/issues/42820)
- **💎 多 Agent 并发导致的 LLM 请求集体超时（#43374）：** 创建于 2026-03-11。这是个严重的并发瓶颈问题，所有并发 Agent 的 API 调用会同时超时。问题已被标记为 `P1` 和 `platinum hermit`，但同样长期未取得实质性进展。**链接：** [#43374](https://github.com/openclaw/openclaw/issues/43374)

---

## 横向生态对比

好的，作为一名专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师，我已经仔细审阅了您提供的 2026-07-24 的动态摘要。以下是我为您出具的横向对比分析报告。

---

### 2026-07-24 AI 智能体/个人 AI 助手开源生态横向对比分析报告

#### 1. 生态全景

当前个人 AI 助手与自主智能体开源生态正处于“**从野蛮增长到精细化运营**”的转型期。各项目均展现出极高的社区活跃度，但焦点已从单纯的功能堆叠转向了**生产级稳定性**（如 LiteLLM 的流式计费损失、Temporal 的竞态条件崩溃）、**成本优化**（如 Hermes Agent 的惰性工具加载、Pi 的硬编码 Token 上限）以及**跨平台无缝体验**（如 OpenClaw 的多客户端诉求）的激烈博弈。社区反馈日益成熟，对 **“静默失败”** 和 **“破坏性升级”** 的容忍度降至冰点，迫使各项目将架构重构（如 OpenClaw 的 Cron 统一、Pi 的模型解析）和可观测性提升（如 OpenHands SDK 的对话索引）提上日程。整体看，生态正加速分化：部分项目（如 Hermes Agent）在快速迭代中面临社区膨胀的管理挑战，而另一些（如 Temporal）则依托其基础设施定位，在稳定性和行为一致性上持续深耕。

#### 2. 各项目活跃度对比

| 项目 | 活跃性评估 | Issue 更新 | PR 更新 | 新版本 | 合并率/处理速度 | 健康度/风险亮点 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | **极高**，核心功能重构 | 851 条 (峰值) | 未单独统计 (含在851内) | 无 (beta测试中) | 高 (大型PR合并) | **风险**: 严重Bug爆发 (P0级崩溃/数据损坏)；**机会**: 架构重构 (Cron统一) 是长期利好 |
| **Hermes Agent** | **极高**，社区贡献爆炸 | 323 条 (新) | 500 条 (新) | 无 | 低 (271个待合并PR) | **风险**: PR积压严重，维护者审核压力巨大；**机会**: Lazy Tool等关键优化呼声高 |
| **OpenHands SDK** | **高**，稳步迭代 | 21 条 (更新) | 21 条 (更新) | **v1.37.0** | 高 (多个核心PR合并) | **健康**: 性能、安全、结构化输出均有明确进展，项目节奏平稳 |
| **Pi** | **高**，修复与兼容并重 | 78 条 (更新) | 22 条 (更新) | 无 | 高 (13条PR合并/关闭) | **健康**: 聚焦于特定提供商和本地模型体验优化，回应迅速 |
| **LiteLLM** | **极高**，代理层核心枢纽 | 145 条 (更新) | 237 条 (更新) | 无 | **低** (36.7%合并率) | **风险**: PR积压严重，计费、限流等生产环境核心Bug待解决 |
| **Temporal** | **高**，稳定且专注 | 4 条 (新) | 56 条 (22合并/34新) | 无 | 高 | **健康**: 聚焦行为一致性和测试覆盖，技术债务清理有序 |

**解读**：
*   **OpenClaw & Hermes Agent**：社区规模最大，但“成长的烦恼”最明显。高活跃度伴随高 Bug 率和瓶颈。
*   **OpenHands SDK & Temporal**：发展更稳健，社区管理高效，代码质量和稳定性是核心。
*   **LiteLLM**：作为基础代理层，承受着最大的生产环境压力，PR 积压问题是其最大挑战。
*   **Pi**：在 AI 助手工具中找到了独特定位（深度 CLI/本地模型），社区小而精，反馈精准。

#### 3. OpenClaw 在生态中的定位

*   **核心优势**：
    *   **全能型选手**：视野最广，覆盖了从核心（Cron重构、Gateway状态管理）到外围（Telegram富文本、多客户端遥测）的所有环节，致力于成为“大一统”的个人 AI 助手平台。
    *   **架构前瞻性**：“一切皆 Cron”计划是生态中最具想象力的架构改革之一，旨在从根本上解决复杂任务调度的一致性问题。
    *   **社区协作深度**：拥有 @steipete 这样的核心贡献者进行大型重构，显示出较高的社区技术领袖忠诚度。

*   **与同类（Hermes Agent、Pi）的技术路线差异**：
    *   **vs Hermes Agent**: OpenClaw 更像一个操作系统级平台，而 Hermes Agent 更像一个专注于“Agent 智能体”的容器。Hermes 的焦点在于工具加载、Token 优化和 RAG，更侧重 Agent 的“脑力”效率；OpenClaw 则在多平台、多客户端、任务编排上投入更多，侧重“行动力”和“生态”。
    *   **vs Pi**: Pi 是极致的文本/CLI 效率和用户本地控制，而 OpenClaw 追求的是“全家桶”式的图形界面 WebUI 和丰富的平台集成（如Telegram）。Pi 的强项在于本地模型推理和开发效率，OpenClaw 则在多 Agent 协作和复杂工作流管理上更胜一筹。

*   **社区规模对比**：
    *   **规模**: 从数据看，与 Hermes Agent 共同处于**第一梯队**，远超 OpenHands SDK、Pi 和 Temporal。
    *   **质量**: 拥有大量深度参与的大型 PR 和架构讨论，表明其吸引了高水平的开发者。但 P0/P1 级 Bug 的爆发也表明，其社区增长的“粗糙面”——大量用户涌入后，稳定性和易用性问题被快速暴露。

#### 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求/表现 |
| :--- | :--- | :--- |
| **会话/上下文/内存管理** | **OpenClaw**, **Hermes Agent**, **OpenHands SDK** | **OpenClaw** (#102020): 跨渠道初始化冲突；**Hermes** (#4335, #28279): 跨平台共享 vs 隔离内存；**OpenHands** (#4205): 持久化记忆功能。 |
| **安全性加固** | **Hermes Agent**, **LiteLLM**, **OpenHands SDK** | **Hermes** (#70341等): 大量PR修复SSRF和凭证泄露；**LiteLLM** (#22159): 导入模块HTTP请求；**OpenHands** (#4180): 默认绑定localhost。 |
| **Token/成本优化** | **Hermes Agent**, **Pi**, **LiteLLM** | **Hermes** (#6839): 惰性工具加载；**Pi** (#7034): 移除硬编码Token上限；**LiteLLM** (#14457): 流式用量丢失导致计费缺口。 |
| **跨平台/客户端支持** | **OpenClaw**, **Hermes Agent**, **OpenHands SDK** | **OpenClaw** (#75): Linux/Windows原生桌面应用呼声；**Hermes**: 桌面端跨标签页消息泄露；**OpenHands**: 父子对话关系持久化。 |
| **代理/路由层稳定与弹性** | **LiteLLM**, **Temporal** | **LiteLLM**: TPM限制不准、健康检查崩溃、流式中断；**Temporal**: 幂等性、竞态条件、失败重试。 |

**核心洞察**：**“记忆”** 和 **“成本”** 是当前 AI 智能体从“能用”走向“好用”的两座大山。用户不再满足于“单次对话”，而是要求 Agent 具备连续性、继承性和经济性。

#### 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent | OpenHands SDK | Pi | LiteLLM | Temporal |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **功能侧重** | **个人全栈助手平台** | **强化Agent脑力与效率** | **开发者构建框架** | **极致CLI/本地模型** | **多模型代理/路由层** | **分布式工作流/编排** |
| **核心创新点** | “一切皆Cron” 调度 | Lazy Tool, 会话内存控制 | 结构化输出, 凭证管理 | Llama.cpp动态输出上限 | 多窗口预算, 可观测性 | SAA/WFA行为对齐 |
| **目标用户** | 寻求开箱即用体验的个人/极客 | 深度使用Agent能力的开发者 | 构建定制化Agent的开发者/企业 | 追求极致效率的开发者/隐私党 | 企业API治理/成本管控团队 | 构建复杂可靠后端的平台团队 |
| **技术架构** | 高度模块化, 强调统一调度 | 插件化, 聚焦智能体核心 | SDK化, 定义清晰API契约 | 轻量级, 强绑定本地优先 | 代理层, 路由和治理中心 | 分布式, 强一致性状态引擎 |
| **社区生态** | 全能型, 社区广而杂 | Agent聚焦, 生态活跃 | 框架定位, 开发者社区 | 小而精, 深度用户社区 | 企业级, 承受压力大 | 基础设施, 生态稳定 |

#### 6. 社区热度与成熟度

*   **第一梯队（快速迭代，野蛮生长）**:
    *   **OpenClaw** & **Hermes Agent**: 社区规模巨大，Issue/PR 数量惊人，处于功能快速扩展期。但面临严重的质量管控和社区管理挑战，Bug 率和 PR 积压是两个最明显的“成长痛”。
*   **第二梯队（稳步迭代，质量巩固）**:
    *   **OpenHands SDK** & **LiteLLM** & **Pi**: 社区规模中等，发布节奏更稳定。项目团队对核心问题的响应更及时，修复 PR 的合并率更高。其中 LiteLLM 因代理层的特殊定位，承受的生产环境压力使其问题清单看似较长，但均指向了明确的核心诉求。
*   **第三梯队（基础设施，成熟稳定）**:
    *   **Temporal**: 社区活跃度体现在高质量、小批量的技术讨论上。项目关注点聚焦于行为一致性和边缘情况覆盖，对“破坏性变更”极度敏感，是生态中最成熟、最稳健的一环。

#### 7. 值得关注的趋势信号

1.  **“静默失败”成为众矢之的**: 从 OpenClaw 的子代理丢失结果到 Hermes Agent 的插件静默失效，再到 LiteLLM 的流式用量丢失，用户对 **“无反馈”** 的故障模式深恶痛绝。未来的 Agent 框架必须将“可观测性”和“错误通知”作为第一优先级，而非事后追查。
2.  **从“能用”到“可控”与“可管理”**: 用户不再满足于功能实现，而是要求精细管控。LiteLLM 的多窗口预算、OpenClaw 的会话 TTL 清理、Hermes Agent 的技能权限白名单，都指向了**可视化、可配置、可审计**的管理能力需求。
3.  **Agent 行为的一致性是下一个护城河**: Temporal 专注于 SAA/WFA 的行为对齐不是一个孤立事件。随着 Agent 架构日益复杂（多客户端、多通道、多模型），**保证 Agent 在不同场景下行为（尤其是失败处理）的一致性**，将成为决定一个框架能否从“玩具”走向“工具”的关键。
4.  **代理层 / 网关层的重要性凸显**: LiteLLM 的极高活跃度（145个Issue, 237个PR）是一个强烈的信号。**AI 智能体的“高速公路”——API 路由、限流、计费、安全——已成为一个独立的、高价值的基础设施层**，并吸引了最多的生产环境压力和社区讨论。
5.  **对“升级灾难”的零容忍**: OpenClaw 和 Hermes Agent 的多起 P0/P1 级 Bug 都源于升级过程。数据迁移不透明、破坏性变更、回归 Bug，正在透支用户对项目的信任。**平滑、安全的升级通道**将是所有项目走向成熟必须跨越的门槛。

**对开发者/技术决策者的参考价值**：

*   **选择技术栈时**：评估一个项目，不仅要看其功能多强大（OpenClaw, Hermes），更要看其对 **“静默失败”** 和 **“升级风险”** 的治理能力。（参考 OpenHands SDK 和 Temporal 的稳健做法）
*   **开发 Agent 应用时**：优先考虑具备 **“会话隔离/共享”** 和 **“Token 成本可视化”** 能力的框架（如 Hermes, LiteLLM）。这是提升用户体验和控制成本的关键。
*   **进行架构设计时**：应借鉴 **“一切皆调度”** （OpenClaw）的思维和 **“行为一致性”** （Temporal）的教条，这有助于构建健壮、可预测的复杂 Agent 系统。不要让“智能”成为不可控的混沌。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是为您生成的 Hermes Agent 项目动态日报。

---

# Hermes Agent 项目日报 | 2026-07-24

## 今日速览
项目今日保持极高的活跃度，社区贡献与反馈量巨大。过去24小时内，共产生了 **323条** Issues 和 **500条** PR 的更新，显示出一个蓬勃发展的开源生态。然而，大量的待处理项（271个待合并PR）也表明维护团队的审核压力巨大。焦点集中在**多会话/平台隔离问题**、**Token利用率优化**以及在**安全性**方面的持续加固。尽管没有新版本发布，但社区对核心功能的改进需求（如惰性工具加载、永久记忆系统）讨论非常热烈，项目健康度总体积极但面临快速增长的挑战。

## 项目进展
今日项目核心进展体现在对多个长期存在的 Bug 和安全问题的修复上，整体推进了稳定性与安全性。

- **安全性加固**：多个来自 @zapabob 的 PR (#70341, #70342, #70343, #70336) 着重修复了 SSRF 和凭证泄露风险，覆盖了 BlueBubbles 附件下载、语音命令子进程环境变量以及 Skills Hub API 请求。这标志着项目在安全边界上的一次系统性提升。
- **跨会话场景优化**：PR #59295 和 #70105 正在推进 `session_search` 功能的作用域默认限制在当前聊天，这是对全局内存泄露问题 (`#4335`, `#28279`) 的直接响应，意在从根源上解决会话隔离问题。
- **API 层改进**：PR #70083 针对 GPT-5.5 系列模型修复了 Prompt 缓存问题，这对于控制用户使用成本至关重要。该 PR 被标记为 P0 优先级，体现了其紧迫性。

## 社区热点
今日社区讨论最为热烈且最具代表性的议题如下：

- **[#6839] Feature: Lazy Tool Schema Loading** - **讨论焦点**: **Token 优化先行者**
    - **链接**: https://github.com/NousResearch/hermes-agent/issues/6839
    - **热度**: 30条评论, 16个 👍
    - **分析**: 这是社区对**核心基础设施效率**最强烈的呼声。用户指出，即使在简单的对话中，也必须加载所有可用工具（50+）的完整架构，消耗大量 Token。该特性要求实现“两阶段工具注入”，即模型首先生成意图，再根据意图选择性注入对应工具。如果实现，将极大提升本地模型的推理速度并显著降低 API 调用成本。这是一个典型的“高需求、低实现复杂度”的优质 Feature Request。

- **[#4335] Cross-platform session context sharing** - **讨论焦点**: **打破信息孤岛**
    - **链接**: https://github.com/NousResearch/hermes-agent/issues/4335
    - **热度**: 9条评论, 2个 👍
    - **分析**: 该议题已持续近4个月，但热度不减。用户在多平台（CLI、Telegram等）使用Agent时，发现会话信息完全不互通。背后是用户对 **“Agent即分身”** 的无缝体验的渴望，他们期望Agent具备跨平台上下文记忆能力。当前的全局内存无法满足这一需求，而按聊天隔离的设计又走向了另一个极端。该议题与 #28279 (Per-Chat Memory Isolation) 构成了一体两面，是项目在内存架构设计上需要解决的核心矛盾。

## Bug 与稳定性
今日报告的 Bug 质量较高，主要集中在对用户体验的破坏性影响上。

| 严重程度 | Issue/PR 链接 | 问题描述 | 修复状态 |
| :--- | :--- | :--- | :--- |
| **P1 - 致命** | [#63047](https://github.com/NousResearch/hermes-agent/issues/63047) | **macOS 桌面端**在~5次消息后完全无响应（含设置）。 | 待处理 |
| **P1 - 致命** | [#63719](https://github.com/NousResearch/hermes-agent/issues/63719) (推测, 描述缺失) | **代码回滚危机**。内容缺失，但P1标记表明存在重大风险。 | 待处理 |
| **P1 - 致命** | [#62708](https://github.com/NousResearch/hermes-agent/issues/62708) (已关闭) | 上下文溢出时无警告（压缩被阻断），导致模型静默失效。 | 已修复/关闭 |
| **P2 - 严重** | [#63679](https://github.com/NousResearch/hermes-agent/issues/63679) (已关闭) | 桌面端更新后，每条助手消息渲染两次。 | 已修复/关闭 |
| **P2 - 严重** | [#66875](https://github.com/NousResearch/hermes-agent/issues/66875) | 从插件页面切回聊天时，最新会话无法切换。 | 待处理 (有修复PR #67091) |
| **P2 - 严重** | [#67762](https://github.com/NousResearch/hermes-agent/issues/67762) | 网关重启后，会话成本估算重置为 $0，影响计费展示。 | 待处理 |
| **P0 - 紧急** | [#70083](https://github.com/NousResearch/hermes-agent/pull/70083) | GPT-5.5 模型 Prompt 缓存失效，导致成本飙升。 | 有修复PR (已创建) |

**今日稳定性亮点**: #62708 和 #63679 的关闭显示了团队对近期回归Bug的快速响应能力。此外，针对 #67001 (MacBook唤醒时桌面应用抢焦点) 的社区抱怨，也表明桌面端体验仍需打磨。

## 功能请求与路线图信号

- **短期/下一版本强信号**:
    - **Lazy Tool Schema Loading (#6839)**: 呼声极高，落地后能解决老生常谈的Token浪费问题，可能是下一个主要版本的核心特性。
    - **知识库 RAG 系统 (#844)**: 虽然是一个长期请求，但作为“工作区”概念的核心部件，结合当前对会话隔离的讨论，其需求度再次凸显。
    - **插件 API 版本化与稳定性契约 (#64179)**: 这是社区开发者生态成熟的标志，正式确立 API 稳定性将吸引更多第三方插件贡献。该 PR 已在申请中，未来被采纳的可能性很大。

- **中期思考**:
    - **会话隔离/共享**: 社区对于内存模型没有达成共识。是全局 (现有)、按聊天隔离 (#28279) 还是可跨平台共享 (#4335)？这需要项目核心团队做出明确的架构决策。相关 PR #59295 的尝试预示着可能走向“默认隔离，可配置共享”的方案。

## 用户反馈摘要

- **📈 性能与成本焦虑**: 大量评论 (如 #6839) 反映了用户对本地模型推理速度和API调用成本的极度敏感。`Lazy Tool Loading` 和 `GPT-5.5 缓存修复` 直接回应了这一痛点。用户明确意识到“加载无用工具”是一种隐形浪费。
- **🔀 混乱的会话体验**: #59305 (跨标签页消息泄露)、#66875 (无法切换到最新会话) 和 #67001 (Mac唤醒抢焦点) 共同描绘了桌面端会话管理混乱的现状。用户期望的是一个稳定、可预期的操作环境。
- **🔒 对安全基线的担忧**: #69449 (API Key明文存储) 和 #69424 (慢后端导致无限重试) 展示了用户对基础安全与资源保护的诉求。用户不仅关注模型能力，更关注 Agent 对自身环境和资源的“边界感”。
- **💡 对 Agent 连续性的渴望**: #4335 (跨平台会话) 和 #28279 (隔离内存) 看似矛盾，实则反映了用户对 Agent 智能同一性的更高要求。用户希望 Agent“记住”关于他自己的事，但不要混淆不同用户的对话。

## 待处理积压

- **重要待审核 Issue**:
    - [#21341] [Bug]: nixosModule 文件安装路径错误 (自2026-05-07) - 影响NixOS用户的正确部署。
        - 链接: https://github.com/NousResearch/hermes-agent/issues/21341
    - [#12651] [Bug]: `.env` 清理器无法移除 `KEY=***` 占位符 (自2026-04-19) - 可能导致配置混乱和安全风险。
        - 链接: https://github.com/NousResearch/hermes-agent/issues/12651
    - [#2765] [Bug]: Hindsight 插件静默失败 (自2026-03-24) - 重要插件在错误配置时不报错，极大影响调试体验。
        - 链接: https://github.com/NousResearch/hermes-agent/issues/2765

- **长期待合并 PR**:
    - [#55252] feat: add api-gateway optional skill (自2026-06-29) - 一个旨在集成140+第三方服务的大型功能PR，架构影响大，需要仔细评估。
        - 链接: https://github.com/NousResearch/hermes-agent/pull/55252
    - [#16717] feat(webui): browser audio playback for TTS output (自2026-04-27) - 完善WebUI TTS体验，但迟迟未能合并。
        - 链接: https://github.com/NousResearch/hermes-agent/pull/16717

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

好的，这是为您生成的 OpenHands SDK 项目动态日报。

---

## OpenHands SDK 项目动态日报 — 2026-07-24

### 1. 今日速览

本日项目活跃度极高，共有21条Issue和21条PR更新，同时发布了v1.37.0新版本。两大亮点值得关注：一是社区在**性能优化**和**内存管理**方面取得了显著进展，多个与之相关的PR已被合并；二是此前呼声很高的**结构化输出**功能（#2566）有了具体的实现PR（#4207），标志着项目在Agent能力上迈出重要一步。此外，关于**凭证生命周期管理**的一系列Issue和PR显示出项目在生产环境稳定性和安全性方面的持续投入。项目整体健康度良好，处于快速迭代阶段。

### 2. 版本发布

- **v1.37.0**: [查看发布详情](https://github.com/OpenHands/software-agent-sdk/releases/tag/v1.37.0)
  - **主要更新**:
    - **性能提升**: 实现了对话的“惰性加载”（Lazy hydration），仅在需要时恢复已持久化的对话，减少了启动开销 (#4100)。
    - **功能增强**: Agent Server现在支持在启动profile时配置`deployment context`，增强了部署的灵活性 (#4030)。
    - **可观测性修复**: 修复了部分可观测性方面的问题。
  - **破坏性变更与迁移**: 此版本未提及破坏性变更。用户可正常升级。

### 3. 项目进展

今日多个核心功能和性能修复被合并，项目进展迅速。主要进展包括：

- **内存与性能优化**:
    - **对话内存泄漏修复**: `perf(agent-server): evict idle conversations from memory after a configurable TTL` (#4202) 已被合并。此PR解决了已结束对话占用内存未释放的问题，是提升服务器稳定性的关键修复。
    - **搜索性能提升**: `perf(agent-server): index conversation execution status for search/count` (#4201) 已被合并。该修复通过索引优化了基于状态的对话搜索和计数，解决了在大规模对话场景下的性能瓶颈 (#3142)。
    - **并行工具调用指标修复**: `fix: parallel tool metrics` (#4193) 已被合并。此修复解决了在并行工具调用场景中，每个ActionEvent重复显示相同请求指标的错误 (#4189)。

- **安全与稳定性增强**:
    - **默认绑定主机调整**: `fix(agent-server): default bind host to loopback without a session API key` (#4180) 被合并。在没有会话API密钥的情况下，服务器默认只监听本地回环地址，提升了开箱即用的安全性。
    - **父子对话关系持久化**: `feat(agent-server): persist parent/child conversation relationships` (#4188) 被合并。此功能满足了Agent Canvas和其他客户端对父子对话关系持久化的需求 (#4119)。
    - **VSCode URL修复**: `fix(agent-server): /api/vscode/url without base_url advertises the configured VSCode port` (#4181) 被合并，修复了端口冲突问题。

- **核心功能推进**:
    - **结构化输出实现**: `Feat/2566 structured output` (#4207) 被提出，这是对长期功能需求 #2566 的具体实现。该PR允许为工具指定Pydantic模型以获得格式化输出。
    - **凭证生命周期管理**: 与Codex凭证生命周期相关的系列Issue（#4169, #4170, #4171）和PR被提出和更新，这表明开发团队正在系统地解决生产环境中凭证失效的关键问题。

### 4. 社区热点

- **最活跃 Issue**: [#4208 - check-pr-artifacts 工作流在Fork的PR上因403错误失败](https://github.com/OpenHands/software-agent-sdk/issues/4208)
  - **分析**: 这是一个由CI流程引发的问题。`check-pr-artifacts` 工作流在Fork的PR上运行时，由于令牌权限不足而失败。虽然评论数不多，但它直接阻碍了外部贡献者的PR流程，属于影响社区协作的关键问题。对应的修复PR #4209 也已提交，显示出社区对此类阻碍的快速响应。

- **高关注度 PR**: [Feat/2566 structured output (#4207)](https://github.com/OpenHands/software-agent-sdk/pull/4207)
  - **分析**: 此PR实现了呼声很高的结构化输出功能。背后是用户对更可靠、可预测的Agent输出的追求。通过Pydantic模型定义输出结构，能极大地提升下游应用的解析效率和稳定性。此功能落地后，预计将吸引更多开发者基于SDK构建需要与Agent进行复杂数据交互的应用。

- **持续关注 Issue**: [#85 - 不同系统应有不同的系统提示词](https://github.com/OpenHands/software-agent-sdk/issues/85)
  - **分析**: 创建于2025年9月，但今日仍有更新。它讨论的是跨平台（如Windows与Linux）命令兼容性问题，例如将`execute_bash`重命名为`execute_powershell`。这是一个长期存在的设计议题，反映了社区对Agent跨平台运行能力的关注。

### 5. Bug 与稳定性

- **高严重性**:
  - **[CI/CD] `check-pr-artifacts` 工作流在Fork的PR上硬失败**: [#4208](https://github.com/OpenHands/software-agent-sdk/issues/4208)。这是由GitHub Action权限限制导致的流程故障，会阻塞所有来自社区Fork仓库的贡献直到修复。
    - **已有Fix PR**: [#4209](https://github.com/OpenHands/software-agent-sdk/pull/4209)

- **中等严重性**:
  - **[视觉器] 并行工具调用指标重复显示**: [#4189](https://github.com/OpenHands/software-agent-sdk/issues/4189) (已关闭)。此问题导致开发者调试体验下降，难以准确追踪每次请求的Token消耗。
    - **已通过**[#4193](https://github.com/OpenHands/software-agent-sdk/pull/4193) 修复。

- **中等严重性**:
  - **[Agent Server] 对话状态查询性能差**: [#3142](https://github.com/OpenHands/software-agent-sdk/issues/3142) (已关闭)。对大量对话进行搜索和计数时，需遍历所有对话，导致CPU和内存开销巨大。
    - **已通过**[#4201](https://github.com/OpenHands/software-agent-sdk/pull/4201) 修复。

- **低严重性**:
  - **[Agent Server] 已结束对话的内存泄漏**: [#3141](https://github.com/OpenHands/software-agent-sdk/issues/3141) (已关闭)。已结束的对话依然占用内存，长期运行会导致OOM。
    - **已通过**[#4202](https://github.com/OpenHands/software-agent-sdk/pull/4202) 修复。

### 6. 功能请求与路线图信号

- **结构化输出**: [#4207](https://github.com/OpenHands/software-agent-sdk/pull/4207) 的实现是明确的路线图信号，表明项目正致力于提升Agent输出的规范性和可编程性。这很可能被纳入下一版本v1.38.0中。
- **凭证生命周期管理**: 一系列关于Codex凭证的Issue (#4170, #4171) 表明，项目正投入资源解决多会话环境下凭证安全与一致性的复杂问题，这对于企业级部署至关重要。
- **标题生成LLM偏好**: [#4199](https://github.com/OpenHands/software-agent-sdk/issues/4199) 要求将标题生成的LLM偏好配置暴露给用户。虽然已有底层支持，但缺少UI配置入口。这暗示了项目正在完善用户个性化配置体系。
- **持久化记忆功能**: [#4205](https://github.com/OpenHands/software-agent-sdk/pull/4205) 提出了将`agent_context.load_memory` 暴露在agent-settings schema中。这与此前关闭的持久化记忆追踪Issue #2037 相关，表明该功能可能正在从内部走向公开配置。

### 7. 用户反馈摘要

- **性能痛点得到解决**: 从Issue #3142 和 #3141 及其对应的修复PR #4201 和 #4202 来看，用户（特别是@csmith49）在部署大量对话后遇到了明显的性能瓶颈。这些问题的快速修复反映了开发者对反馈的积极响应。
- **CI流程阻碍贡献**: Issue #4208 的提出者@luciobaiocchi 报告了社区贡献者在Fork仓库提交PR时遇到的CI失败问题。这表明社区对顺畅的贡献流程非常在意，这类问题会直接影响外部开发者的积极性。
- **部署安全考量**: PR #4180 的作者@neubig 调整了服务器默认绑定地址，这呼应了用户（可能是@harish-chandramowli，在PR #4181中提到端口冲突）在部署时遇到的安全和端口冲突问题。
- **结构化输出长期缺席**: 新提出的PR #4207 背后是#2566(2025年12月)和#2808 等长期未解决的请求。这表明社区对Agent输出“强类型化”的需求已经压抑已久，此功能的引入将获得广泛欢迎。

### 8. 待处理积压

- **高优先级**:
  - **视觉支持检测问题**: [#3495](https://github.com/OpenHands/software-agent-sdk/issues/3495) - `step-3.7-flash` 模型的视觉支持在运行时未被正确检测。该Issue自6月3日提出，标记为`Stale`，但问题描述清晰，且直接影响特定模型的评估。建议维护者投入精力复现并修复。

- **中优先级**:
  - **Agent Server 500错误**: [#3515](https://github.com/OpenHands/software-agent-sdk/issues/3515) - `POST /api/conversations` 间歇性返回500错误，影响通过Slack和GitHub等外部工具启动的对话。该Issue也标记为`Stale`，但作为生产环境的偶发性错误，值得优先排查。
  - **交互式Agent提示优化**: [#1317](https://github.com/OpenHands/software-agent-sdk/issues/1317) - 该Issue讨论了CLI（交互式）与云端（非交互式）环境下Agent应使用不同默认提示词的问题，自去年12月提出后讨论不多但概念明确。随着CLI用户的增加，此问题将变得更关键。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，请看以下为您生成的 Pi 项目动态日报。

---

# Pi 项目动态日报 | 2026-07-24

## 1. 今日速览

今日项目活跃度极高，共处理了 78 条 Issue 更新，其中关闭了 67 条，显示了强劲的维护与修复节奏。PR 方面，有 22 条更新，其中 13 条被合并或关闭，技术债务清理和功能迭代并行推进。社区讨论焦点集中在对 **AI 提供商的兼容性修复**（如 AWS Bedrock、Qwen、DeepSeek、OpenAI Gateway）和对 **本地模型/边缘设备支持** 的优化上。项目健康度良好，正在快速响应用户反馈并解决稳定性和兼容性问题。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日合并或关闭了多项重要 PR，在功能推进和问题修复上均有显著进展：

- **关键Bug修复：**
    - **Llama.cpp 输出限制修复**：PR [#7034](https://github.com/earendil-works/pi/pull/7034) 被合并，移除了 Llama 提供者中硬编码的 16384 token 输出上限，改为从模型上下文中动态获取，解决了用户无法使用大输出窗口的问题。
    - **模型配置热重载回归修复**：PR [#7036](https://github.com/earendil-works/pi/pull/7036) 已提交，旨在解决 [#6999](https://github.com/earendil-works/pi/issues/6999) 中提到的 `/model` 界面无法在会话中实时重载 `models.json` 的问题。
    - **Wayland 剪贴板错误处理**：PR [#7009](https://github.com/earendil-works/pi/pull/7009) 被合并，修复了 `/copy` 命令中未检查 `wl-copy` 退出码导致误报成功，并无法触发 fallback 的问题。
    - **测试隔离性增强**：PR [#6965](https://github.com/earendil-works/pi/pull/6965) 被合并，通过环境变量白名单隔离测试环境，提升了 CI/CD 的稳定性。

- **新功能/体验优化：**
    - **TUI 显示优化**：PR [#7017](https://github.com/earendil-works/pi/pull/7017) 增加了实验性设置，允许在长会话中不完全重绘转录记录；PR [#7015](https://github.com/earendil-works/pi/pull/7015) 则修复了窄终端中滚动指示器被截断的问题。
    - **Bash 执行事件**：PR [#6971](https://github.com/earendil-works/pi/pull/6971) 被合并，为 `bash_execution_update` 事件添加了 `id` 字段，便于客户端处理并行执行。
    - **LGTM 工具优化**：PR [#7023](https://github.com/earendil-works/pi/pull/7023) 被合并，优化了 lgtm 工具的交互逻辑，减少了误用。
    - **重试机制改进**：PR [#6980](https://github.com/earendil-works/pi/pull/6980) 被合并，将 Anthropic 和 OpenAI SDK 的内部重试替换为可中断的通用重试机制。

## 4. 社区热点

今日社区讨论最活跃的议题反映了用户对**特定厂商 API 兼容性**和**核心功能回归**的强烈关注：

- **Copilot Enterprise 兼容性问题** ([#6768](https://github.com/earendil-works/pi/issues/6768))：此 Bug 获得 **9 个👍** 和 9 条评论。用户报告在 Copilot Enterprise 许可证下无法使用压缩功能，提示 421 错误。这暴露了项目在支持企业级 AI 服务时的认证或协议适配问题，是社区高优先级诉求。
- **AWS Bedrock 配置文件忽略问题** ([#6957](https://github.com/earendil-works/pi/issues/6957))：用户发现当存在 AWS 环境变量时，awc-bedrock 提供商会忽略已配置的 profile，导致凭证意外覆盖。这影响到使用复杂 AWS IAM 配置的用户。
- **Qwen 与 DeepSeek 模型设置错误** ([#6951](https://github.com/earendil-works/pi/issues/6951), [#6998](https://github.com/earendil-works/pi/issues/6998))：用户指出 Pi 对 Qwen 和 DeepSeek 等新模型的 `thinkingLevelMap` 和 `thinkingFormat` 配置不正确，导致推理能力无法正常使用。这表明社区对新兴模型支持有着很高的期待和测试热情。

## 5. Bug 与稳定性

今日报告的 Bug 主要集中在兼容性、功能异常和用户体验方面，部分已有修复 PR：

| 严重程度 | Issue/PR 编号 | 描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **高** | [#6879](https://github.com/earendil-works/pi/issues/6879) | 自动压缩在长时间 Agent 任务中不会触发，直到 API 拒绝请求。 | **未修复** |
| **高** | [#6948](https://github.com/earendil-works/pi/issues/6948) | 内置 `llama.cpp` 提供者的 `defaultModel` 在启动时因竞态条件无法生效。 | **未修复** |
| **高** | [#7030](https://github.com/earendil-works/pi/issues/7030) | 通过 Cloudflare AI Gateway 使用 OpenAI 模型时，提供者前缀被错误丢弃。 | **未修复** |
| **中** | [#6970](https://github.com/earendil-works/pi/issues/6970) | `github-copilot` 使用插件集成导致令牌在多设备上过快失效。 | **未修复** |
| **中** | [#6999](https://github.com/earendil-works/pi/issues/6999) | `models.json` 热重载功能在 0.80.8+ 版本后丢失。 | **已有修复 PR** [#7036](https://github.com/earendil-works/pi/pull/7036) |
| **中** | [#6994](https://github.com/earendil-works/pi/issues/6994) | llama 提供者对输出 token 有 16384 的硬编码上限。 | **已修复** (PR [#7034](https://github.com/earendil-works/pi/pull/7034)) |
| **低** | [#7033](https://github.com/earendil-works/pi/issues/7033) | 安装包内 `pi` 清单格式错误会导致会话启动崩溃循环。 | **已关闭** |
| **低** | [#7021](https://github.com/earendil-works/pi/issues/7021) | CJK 等宽字符在编辑器中的上下移动光标位置计算错误。 | **未修复** |

## 6. 功能请求与路线图信号

社区提出了多个有意义的新功能请求，结合已有 PR，以下项目可能被纳入未来版本规划：

- **增强的模型/工具语法控制**：
    - Issue [#6306](https://github.com/earendil-works/pi/issues/6306) 提出增加对“严格模式”（Strict Tools）或“约束采样”（Constrained Sampling）的支持。这是一个重要的功能方向，PR [#6341](https://github.com/earendil-works/pi/pull/6341) 已提出草案，允许工具要求提供者侧进行受约束的参数生成。
    - Issue [#6951](https://github.com/earendil-works/pi/issues/6951) 和 [#6998](https://github.com/earendil-works/pi/issues/6998) 要求为 Qwen 和 DeepSeek 模型提供更准确的推理设置，这部分信号强烈，可能会推动 Pi 的模型配置文件更加灵活。

- **更好的会话/缓存管理**：
    - Issue [#6621](https://github.com/earendil-works/pi/issues/6621) 建议防止动态系统提示导致缓存意外失效，这对使用本地模型（如 AMD 平台）的用户非常重要，因为其预填充（prefill）速度较慢。
    - Issue [#7026](https://github.com/earendil-works/pi/issues/7026) 提出为通过网关路由的 OpenAI 模型增加 `prompt_cache_key` 兼容性覆盖。

- **平台与集成扩展**：
    - Issue [#4742](https://github.com/earendil-works/pi/issues/4742) 和 [#7013](https://github.com/earendil-works/pi/issues/7013) 都请求增加 [Siliconflow](https://docs.siliconflow.com/en/usercases) 作为内置提供者，这是一个类似 OpenRouter 的模型聚合平台，反映出用户对更多模型选择的需求。
    - Issue [#7037](https://github.com/earendil-works/pi/issues/7037) 请求增加提供者级别的缓存支持，这可能成为下一轮性能优化的重要组成部分。虽然今日未进入 Top 30，但值得关注。

## 7. 用户反馈摘要

从今日的 Issue 和评论中，可以提炼出以下用户真实场景和痛点：

1.  **企业用户与特定平台的兼容性阵痛**：使用 Copilot Enterprise 许可证的用户无法使用压缩功能（[#6768](https://github.com/earendil-works/pi/issues/6768)），使用 DeepSeek 官方 API 的模型不可见（[#6986](https://github.com/earendil-works/pi/issues/6986)）。这表明 Pi 在适配不同模型的认证、API 版本差异上仍面临挑战。
2.  **本地模型用户对性能敏感**：用户报告在 AMD 统一内存设备（如 strix halo）上，动态提示语意外导致缓存失效，加剧了慢预填充的问题（[#6621](https://github.com/earendil-works/pi/issues/6621)）。他们希望 Pi 能更智能地管理缓存和预填充，最大化本地推理效率。
3.  **“功能丢失”导致用户困惑与不满**：`models.json` 热重载功能（[#6999](https://github.com/earendil-works/pi/issues/6999)）和 `defaultModel` 启动问题（[#6948](https://github.com/earendil-works/pi/issues/6948)）都是旧有体验的退化。用户对于“曾经能用，升级后不能用”感到沮丧，这强调了回归测试的重要性。
4.  **对沙箱与安全环境的支持需求**：多位用户（[#6872](https://github.com/earendil-works/pi/issues/6872), [#7012](https://github.com/earendil-works/pi/issues/7012)）报告在 `bwrap` 等沙箱环境中剪贴板和命令执行受影响。这些用户深入使用 Pi，并希望其能在受限环境中正常工作。

## 8. 待处理积压

以下是一些虽然讨论热度不高，但可能对项目长期健康或特定用户群至关重要，需要维护者关注的长期未响应议题：

- **扩展重载安全请求** ([#5735](https://github.com/earendil-works/pi/pull/5735))，自 2026-06-14 开启，是一个关于安全、可靠地处理扩展重载请求的重要 PR，目前仍处于等待讨论状态。
- **Anthropic Bearer Token 支持** ([#6148](https://github.com/earendil-works/pi/pull/6148))，自 2026-06-28 开启，尝试解决 Anthropic 提供者认证问题，但作者本人也承认方案不够优雅，需要进一步探讨。
- **SiliconFlow 提供者请求** ([#4742](https://github.com/earendil-works/pi/issues/4742))，作为社区长期诉求，自五月起就已提出，但至今未进入开发议程。随着 AI 模型的多样性增加，此类聚合平台会越来越重要。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 | 2026-07-24

---

## 1. 今日速览

过去 24 小时项目社区保持极高活跃度：**145 条 Issue 更新**（新开/活跃 98 条，关闭 47 条），**237 条 PR 更新**（待合并 150 条，已合并/关闭 87 条）。无新版本发布。合并率约 36.7%，待合并 PR 积压明显，但修复与功能类 PR 持续推进。全天共关闭 47 个 Issue，显示出维护者正在积极清理积压及回归问题。社区热点集中在代理层限流、流式用量丢失、Claude 工具调用异常等生产级稳定性问题。

---

## 2. 版本发布

**无新版本发布**（最近一次版本不在此报告范围内）。

---

## 3. 项目进展

今日合并/关闭的 87 个 PR 中，重要进展包括：

- **代理与路由**：`#27921`（已合并）修复 Azure 代码解释器容器 ID 解码为 `None` 的路由逻辑，避免原生 Azure 容器请求被直接处理或丢回；`#34429`（待合并）使 `fail_closed_budget_enforcement` 真正覆盖原子预算预订写失败场景，防止 Redis 故障时超支。
- **用户与预算**：`#34437`（已合并）为用户表新增 `budget_limits` 列，支持多窗口预算（类似 API Key 和团队的 `budget_limits`），包括花费追踪与强制执行。
- **响应与适配**：`#34438`（待合并）修复上游删除错误在代理层返回 500 的问题，保留真实错误状态；`#34433`（待合并）修复 Anthropic 单次流适配器硬编码空 `text` 块导致推理模型出现多余空内容的 bug。
- **日志与可观测性**：`#34418`（待合并）通过 `contextvars` 新增可选的 `session_id` 和 `trace_id` 日志关联字段，方便线上追溯。

**整体评估**：项目正向预算精细化、代理可观测性、多 provider 适配完备性稳步推进，但仍有大量 PR 处于待合并状态，维护者需加快评审节奏。

---

## 4. 社区热点

以下为今日评论数或反应最多的 Issue/PR：

| 标题 | 类型 | 评论/反应 | 核心诉求 |
|------|------|-----------|----------|
| [#24677 Incorrect TPM limiting for virtual keys](https://github.com/BerriAI/litellm/issues/24677) | Bug | 14 评论，4 👍 | 用户报告 v1.82.3 中虚拟 key 的 TPM 限制仍然不准确，尽管此前标记已修复。 |
| [#14457 Usage data lost when streaming responses are terminated early](https://github.com/BerriAI/litellm/issues/14457) | Bug | 8 评论，3 👍 | 客户端提前断开流式请求时用量记录丢失，导致计费缺口和配额异常。 |
| [#34281 Fail Gracefully for Health Checks](https://github.com/BerriAI/litellm/issues/34281) | Bug | 6 评论 | HomeLab 用户希望健康检查在主机离线时优雅降级，而非抛硬错误。 |
| [#22159 litellm is calling an http GET on module import](https://github.com/BerriAI/litellm/issues/22159) | Bug | 6 评论 | 模块导入时默认发起 HTTP 请求，被批评为“hostile”，要求懒加载或 opt-in。 |
| [#19858 Claude models with tool calling are broken](https://github.com/BerriAI/litellm/issues/19858) | Bug | 6 评论 | 升级后通过 OpenRouter/Vertex 使用 Claude Sonnet 4.5 时工具调用失败，影响 Kilo Code 等客户端。 |

**分析**：社区对限流准确性和连接生命周期管理非常敏感，流式用量丢失是生产环境关键痛点。模块导入 HTTP 请求问题因涉及安全性也引发了较多讨论。

---

## 5. Bug 与稳定性

按严重程度排列今日活跃的 Bug（含新增与回归）：

### 🔴 严重（生产可用性受损）
- **TPM 限制不准确** (`#24677`) — 虚拟 key 限流与实际不符，已报告但仍未完全解决。
- **Claude 工具调用损坏** (`#19858`) — 部分 provider 上 Claude 4.5 模型的 tool calling 返回错误，影响 Agent 工具链。
- **流式用量丢失** (`#14457`) — 客户提前断开时用量完全丢失，导致计费空窗。
- **有效 API 密钥被拒绝** (`#24680`) — 升级至 1.82.3 后部分之前创建的 key 被误判为无效。

### 🟡 中等（功能降级/配置缺陷）
- **转录 JSON 格式 pydantic 校验失败** (`#33764`) — 同时影响 SDK 和 Proxy。
- **Bedrock Converse 并行工具调用失败** (`#22637`) — `parallel_tool_calls: true` 配合 Bedrock Claude 4.5 报 `BedrockException`。
- **reasoning_effort='none' 对 Azure 自定义部署返回 400** (`#31243`) — 忽略 `base_model` 基础模型配置。
- **健康检查硬错误** (`#34281`) — 无法自动降级不可用主机。
- **Guardrails 误报“功能不可用”** (`#24734`) — v1.82.3 升级后编辑 API Key 即使未配置 guardrail 也触犯错误。
- **缓存代码类型错误** (`#30534`) — `float` + `str` 导致 TypeError，影响高并发调用。

### 🟢 低严重（边界情况/UI 问题）
- `/v2/user/info` 遗漏用户级 `rpm_limit`/`tpm_limit` (`#33347`)
- 项目预算未参与原子预订 (`#34101`)
- Bedrock 托管批次无法通过 `/v1/batches/{id}/cancel` 取消 (`#33986`)
- Databricks `response_format` 模型信息未更新 (`#34143`)

**关联修复 PR**：部分 Bug 已有对应 PR·如 `#34429`（原子预算拒绝）、`#34438`（删除错误状态）、`#34433`（Anthropic 适配修复）。`#24677` 和 `#14457` 等核心 Bug 尚未见针对性 PR。

---

## 6. 功能请求与路线图信号

以下为今日用户提出的新功能或强化需求，结合已有 PR 判断纳入时间：

| 需求 | Issue/PR | 状态 | 预计纳入 |
|------|----------|------|----------|
| **货币单位环境变量** | `#8513` | OPEN 19 评论 | 低优先级，UI 硬编码$被多次提及，但无对应 PR |
| **自定义 provider 模型发现** | `#20064` | OPEN 8 评论 | 已有 `config.yaml` wildcard 方案，可能进入下个 minor |
| **代理自定义路由（与 SDK 同能力）** | `#25297` | OPEN 4 评论 | 高需求，`#34416` 已提供每部署失败策略/冷却覆盖，是路由自定义的前置 |
| **禁用实体花费计数 Update 仅保留日志** | `#31866` | OPEN 4 评论 | 高吞吐场景优化，已有详细方案，可能一起合入 |
| **每部署 SSE 心跳避免负载均衡超时** | `#34423` | PR OPEN | 直接关闭关联 Issue，预计快速合并 |
| **日志记录关联 session_id/trace_id** | `#34418` | PR OPEN | 增强可观测性，配合文档 PR 一起推进 |
| **覆盖传出 user 参数为 key 哈希** | `#34417` | PR OPEN | 防提供商按 user 参数封禁，属于安全增强 |
| **UI 日志独立路由 + 标签页路由重构** | `#34430`、`#34435` | PR OPEN | 属于 UI 基础设施改进，不影响核心逻辑 |
| **展示请求由 auto-router 处理** | `#34434` | PR OPEN | 增强仪表盘信息密度 |

**路线图信号**：未来版本将强化代理自定义行为、多窗口预算、可观测性及自动化路由可视化。

---

## 7. 用户反馈摘要

从今日活跃讨论中提炼真实用户痛点：

- **“TPM 限制修复后仍无效”** — 用户 `@yuri-alias` 在 `#24677` 中强调，尽管 `#18953` 曾经标记为解决，`v1.82.3` 仍然存在相同问题，说明回归验证不足。
- **“流式中断后用量丢失无法追回”** — `@jasonpnnl` 在 `#14457` 中详细描述了计费缺口和配额追踪问题，并建议增加最后块持久化或信号续传。
- **“Health Check 不应直接崩溃”** — `@luckylinux` 在 `#34281` 中表示其 HomeLab 主机不定期离线，期望健康检查返回错误代码而非完全中断。
- **“模块导入默认发 HTTP 请求很 hostile”** — `@nonZero` 在 `#22159` 中要求改为懒加载或 opt-in，反映了对安全性和加载速度的关切。
- **“预发布版本的 .npmrc 配置错误导致构建失败”** — `@Kontinuation` 在 `#25057` 中报告 `min-release-age` 配置无效，影响 npm install，已被 PR `#24838` 尝试解决但留下问题。
- **“Lakera v2 guardrail 忽略 skip 配置”** — `@deepanshululla` 在 `#34396` 中报告 `skip_system_message_in_guardrail` / `skip_tool_message_in_guardrail` 不起作用，暴露泛型配置与具体实现间的脱节。

**整体评价**：用户对限流弹性、连接稳定性、模块启动性能有较高期待，且希望配置能够精准生效而不产生副作用。

---

## 8. 待处理积压

以下 Issue 长期未得到有效响应或修复，部分已被标记 `[stale]`，建议维护者优先关注：

| Issue | 创建日期 | 最后更新 | 标签 | 风险 |
|-------|----------|----------|------|------|
| [#8513 Set currency by env variable](https://github.com/BerriAI/litellm/issues/8513) | 2025-02-13 | 2026-07-23 | `stale`, `feature` | 19 评论，非英语用户强烈需求，但已停滞超 500 天 |
| [#9198 Support Alibaba Cloud Qwen](https://github.com/BerriAI/litellm/issues/9198) | 2025-03-13 | 2026-07-23 | `stale`, `enhancement` | 14 评论，社区对 Qwen 集成呼声高，但缺乏维护者响应 |
| [#14457 Stream usage data lost](https://github.com/BerriAI/litellm/issues/14457) | 2025-09-11 | 2026-07-23 | `bug`, `llm translation` | 计费核心漏洞，长期未关闭，已有 8 评论 |
| [#18457 Child process died](https://github.com/BerriAI/litellm/issues/18457) | 2025-12-27 | 2026-07-23 | `stale` | 虽已关闭，但原因为 `--num_workers` 问题，未从根本上解决 |
| [#19334 Azure AI FLUX models fail](https://github.com/BerriAI/litellm/issues/19334) | 2026-01-19 | 2026-07-23 | `stale`, `bug` | 升级后特定 Azure 模型调用失败，已有回复但无修复 |
| [#25057 .npmrc min-release-age breaks build](https://github.com/BerriAI/litellm/issues/25057) | 2026-04-03 | 2026-07-23 | `stale`, `bug` | 影响前端构建流程，已有 PR 但未解决问题本身 |

**建议**：对上述积压 Issue 重新分类、回复或关闭，避免社区因长期无反馈产生不满。特别是计费相关 Bug `#14457` 优先级应设为高。

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据您提供的 Temporal 项目 GitHub 数据生成的 2026-07-24 项目动态日报。

***

### Temporal 项目动态日报 | 2026-07-24

---

#### 1. 今日速览

Temporal 项目今日保持高度活跃的开发节奏。过去 24 小时内，共有 22 个 Pull Request (PR) 被合并或关闭，同时有 34 个新 PR 被提出，显示出强大的社区贡献力度和内部开发效率。Issue 方面，有 4 个新问题被提交，主要集中在功能请求和潜在 Bug 上，整体健康度良好。当前开发重点明显集中在**独立活动 (SAA) 与工作流活动 (WFA) 的 API 行为对齐**以及**CHASM Nexus 功能的稳定性与覆盖度提升**上。

#### 2. 版本发布

无

#### 3. 项目进展

今日合并/关闭的 22 个 PR 中，**社区贡献显著**（例如 `@GautamSharma99` 提交的 `#11237`），在以下关键领域取得了重要进展：

- **SAA (独立活动) 行为对齐与修复**：
    - `#11150` (合并至 `#11203`): 修复了活动描述响应（Describe Response）中 `nextAttempt` 和 `current_retry_interval` 字段的计算错误，提升了SAA状态反馈的准确性。
    - `#11237` (合并): 优化了任务匹配（matching）逻辑，确保被轮询者（poller）接受但未能启动的失败任务，在报告给处理钩子时能被正确标记为“不匹配”，从而改善重试和队列管理行为。
- **功能增强**：
    - `#11248` (合并): 在`DescribeWorkflowExecution` API 中添加了时间跳过（fast-forward）信息，方便用户了解工作流的时间运行状态，这是一个实用的可观测性改进。
    - `#11245` (合并): 新增一个 RPC 基准测试工具 (`cmd/tools/rpsbench`)，为开发者提供了一种对核心WorkflowService RPC进行性能压测的便捷方式。
- **稳定性与合规性修复**：
    - `#11227` (合并): 修复了worker命令任务队列（worker command task queue）在轮询时错误地处理版本控制属性（versioning attributes）的问题，增强了版本控制功能的健壮性。

#### 4. 社区热点

今日社区讨论热度相对平稳，没有出现评论数特别高的“爆款” Issue 或 PR。然而，以下几个议题值得关注，它们反映了社区对**核心可靠性和行为一致性**的持续关注：

- **`#11234` [OPEN]**: 一个关于“使 `RecordActivityTaskStarted` 在取消/暂停/重置期间变得幂等”的 PR。该修复致力于解决匹配服务（Matching）重试时的竞争条件问题。这表明多节点并发环境下记录的幂等性仍是稳定性挑战。
- **`#11249` [OPEN]**: 与 `#11250` (已合并) 紧密相关，都是关于SAAs与WFAs在失败处理上的行为对齐。`#11249` 提出将 `nil` 失败的 `RespondActivityTaskFailed` 请求视为可重试的，以达到与工作流活动 (WFA) 的完全一致性。这体现了社区对API行为一致性的极致追求。
- **`#11243` [OPEN]**: 为 XDC (跨数据中心) Nexus 复制测试增加了混合标志取消的覆盖。这反映了在复杂的多集群、多特性（CHASM与旧版Nexus）共存场景下，对测试覆盖度和质量的高度要求。

#### 5. Bug 与稳定性

昨日报告的 4 个新 Issue 中，有 2 个被识别为潜在的 Bug 或稳定性问题：

- **严重 (Crash)**：
    - `#11188`: **[Potential Bug]** 历史服务在处理积压任务队列（pending task queue）时存在竞态条件，可能导致服务因致命错误而崩溃。这是一个比较严重的问题，但方案仍处于讨论阶段，暂无关联的修复 PR。
- **严重 (功能缺陷)**：
    - `#11230`: **[Bug]** 客户端 TLS 配置无法自动刷新已更改的根 CA 证书。这意味着在证书轮换后，需要重启进程或重新创建客户端配置，否则新连接将失败。这是一个影响生产环境安全性和运维效率的问题，目前无修复 PR。
- **其他 (回归风险)**：
    - `#11203` (已合并/关闭) 的变更（`Breaking change to current_retry_interval`）被标记为“破坏性变更”，这可能影响依赖该字段的客户端逻辑，开发者需升级时关注。

#### 6. 功能请求与路线图信号

- **短期 / 增量改进**：
    - `#11026`: 请求在 UI 上直接显示活动任务的 STDOUT 日志，以解决日志混杂问题。虽未分配到新版本，但这是一个高频的开发者体验痛点，有理由相信可能会在未来版本中考虑。
    - `#11025`: 请求为一等的可持久化订阅集，用于“定时工作流扇出”模式。这代表社区对一个通用、内置解决方案的强烈需求，以避免重复实现。结合`#11220`和`#11223`关于`TimeSkipping`的 PR，Temporal 团队正在积极构建支持“虚拟时间”模式的基础设施，这类功能请求可能与之结合或启发未来更高级的调度模式。

#### 7. 用户反馈摘要

由于所有列出的 Issue 和 PR 评论数均为 0，没有直接的对话可供提炼。但从 Issue 摘要文本中，可以推断出用户当前的痛点：

- **开发者体验**: 用户 `@ohadmata` 对在 UI 中直接查看活动任务 STDOUT 的强烈渴望，背后是“在 worker 日志中筛选混杂信息”的低效与挫败感。
- **平台能力与模式化**: 用户 `@Frost-Leo` 希望 Temporal 提供内建的“订阅集”模式，这表明社区不再满足于仅用 API 拼凑复杂模式，而是期望平台提供更高阶的抽象，从而减少重复劳动和出错概率。

#### 8. 待处理积压

- **`#10804` [OPEN]**: 一个从 2026-06-22 就已提出的 PR，旨在为 worker deployment 的自动创建添加限流，以防昂贵的可见性检查造成系统压力。该 PR 已经待处理超过 30 天，且摘要提及为“昂贵的、无界的”问题，可能长期影响大规模部署下匹配服务的性能。维护团队需要评估其优先级和实现方案。

    [Issue #10804](https://github.com/temporalio/temporal/issues/10804) / [PR #10804](https://github.com/temporalio/temporal/pull/10804)

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*