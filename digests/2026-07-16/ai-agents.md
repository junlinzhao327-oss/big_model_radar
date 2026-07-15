# OpenClaw 生态日报 2026-07-16

> Issues: 486 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-15 23:25 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目日报（2026-07-16）

## 1. 今日速览

过去24小时项目保持极高活跃度：共产生 **486 条 Issue 更新**（新开/活跃 318，已关闭 168）和 **500 条 PR 更新**（待合并 348，已合并/关闭 152）。新版本 **v2026.7.2-beta.1** 发布，带来远程编码会话、原生自动化节点等重磅特性。与此同时，社区报告了多个 **P0 级启动崩溃** 和 **关键回归**，主要集中在 **2026.7.1 遗留下的状态迁移故障** 上，不过维护团队已快速响应，提交了多组修复 PR。整体上项目处于高强度迭代阶段，健康度高风险亦高。

---

## 2. 版本发布

### v2026.7.2-beta.1
- **发布链接**：[Releases](https://github.com/openclaw/openclaw/releases/tag/v2026.7.2-beta.1)
- **核心亮点**：
  - **远程编码会话**：允许在云 Worker 上运行 Control UI 会话；在终端中打开 Codex 和 Claude Catalog 会话并恢复 OpenCode / Pi 会话。
  - **原生自动化与节点**：提供更底层的自动化编排能力（详细条目因 Release Note 截断未能完全展示）。
- **潜在破坏性变更**：尚未在公告中明确列出，但从 Issue 趋势看，状态迁移模块逻辑进一步收紧，可能要求用户主动运行 `openclaw doctor --fix` 或手动处理遗留索引文件。

---

## 3. 项目进展

今日共有 **152 个 PR 被合并或关闭**，以下为推进关键功能/修复的代表性合并：

- **`@steipete` 维护组集中修复**：合并了 **#108495** (测试覆盖率比对)、**#108497** (重构 provider 插件根目录以消除死导出)、**#108493** (恢复完整代码库格式化)、**#108492** (拆分 Control UI 侧边栏展示逻辑)、**#108491** (修复 workboard 工作终端投递)、**#108489** (回传 Anthropic 实时探测关联)。
  - 这些合并显著提升了代码库整洁度、测试可靠性，并修复了多个扩展模块的边界问题。
- **`#108474` [OPEN]** – 重构 Codex 文本 Provider 并入 OpenAI，附带 `doctor` 迁移路径。虽然尚未合并，但已获得 maintainer 标签，预示下一版本将消除 Codex 和 OpenAI 的冗余身份，有望解决 #105561 等 catalog 问题。
- **`#107735` [OPEN，P1]** – 修复心跳在工具调用失败后仍报告成功的问题，被标记为“ready for maintainer look”，预计很快合入。

整体来看，项目向 **2026.7.2 稳定版** 迈进，维护团队正集中火力清理 2026.7.1 中的启动崩溃和状态迁移死锁。

---

## 4. 社区热点

| Issue / PR | 评论数 | 👍 | 核心诉求 |
|-----------|-------|---|---------|
| [#75 – Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75) | 113 | 81 | 要求为 Linux 和 Windows 提供与 macOS/iOS 同等功能的本地客户端应用，属于长期最热门的功能请求。 |
| [#104721 – 所有工具结果返回字面字符串 "(see attached image)"](https://github.com/openclaw/openclaw/issues/104721) | 17 | 1 | P0 回归：文件读取和工具输出被错误替换为占位符字符串，完全阻断正常使用。 |
| [#102020 – 第二消息报错 "reply session initialization conflicted"](https://github.com/openclaw/openclaw/issues/102020) | 14 | 1 | 跨频道 Position 依赖的初始化冲突，影响 Signal 和 DM 等双频道场景。 |
| [#91009 – Codex 预工具钩子导致 CPU 满载](https://github.com/openclaw/openclaw/issues/91009) | 12 | 2 | P1 崩溃循环：Codex 调用产生短生命周期进程消耗 100% CPU，阻塞网关 RPC。 |
| [#94518 – DeepSeek 缓存命中率降至 <10%](https://github.com/openclaw/openclaw/issues/94518) | 9 | 10 | 6.x 升级后边界感知缓存破坏前缀匹配，导致 API 成本暴增，用户反响强烈。 |

**分析**：社区最迫切的需求依然是 **客户端扩展**（#75）、**严重交互回归**（#104721）和 **性能成本问题**（#94518）。尤其是 #104721 和 #91009 直接导致用户无法正常使用工具链，需要优先处理。

---

## 5. Bug 与稳定性

| 严重等级 | 标题 | 链接 | 是否有 Fix PR？ |
|---------|------|------|--------------|
| P0 | [Bug] 所有工具结果返回 "(see attached image)" 字面字符串 | [#104721](https://github.com/openclaw/openclaw/issues/104721) | 未见关联 PR，仍待分配 |
| P0 | 2026.7.1 启动崩溃：遗留记忆索引冲突被视作致命错误 | [#107220](https://github.com/openclaw/openclaw/issues/107220) | **有**：多个 PR 正在审查中（如 #107227 相关修复） |
| P0 | 启动迁移门控致命，`doctor` 无法解决冲突 | [#107227](https://github.com/openclaw/openclaw/issues/107227) | 已关闭，官方修复路径待验证 |
| P0 | 网关因严格迁移警告无法启动 | [#107694](https://github.com/openclaw/openclaw/issues/107694) | 未见独立 PR，预计随 #107227 修复 |
| P0 | 更新至 2026.7.1 后网关无法就绪（插件安装元数据冲突） | [#107727](https://github.com/openclaw/openclaw/issues/107727) | 已关闭，猜测为重复报告 |
| P1 | Codex 预工具钩子导致 CPU 满载 | [#91009](https://github.com/openclaw/openclaw/issues/91009) | 有链接 PR 但未合并 |
| P1 | cron 工具 JSON Schema 与 llama.cpp 解析器不兼容 | [#107449](https://github.com/openclaw/openclaw/issues/107449) | 有 linked PR |
| P1 | 模型回退链未在配额耗尽时触发 | [#85103](https://github.com/openclaw/openclaw/issues/85103) | 未标注 fix PR |
| P2 | 遗留状态迁移警告在 `doctor --fix` 后仍出现 | [#90213](https://github.com/openclaw/openclaw/issues/90213) | 未见独立修复 |
| P2 | 写入工具和 exec heredocs 插入 literal `\n` 而非换行符 | [#93139](https://github.com/openclaw/openclaw/issues/93139) | 无关联 PR |
| P2 | 时钟公告投递触发会话抢占错误 | [#84583](https://github.com/openclaw/openclaw/issues/84583) | 有 linked PR 但未合并 |
| – | 多个老版本回归（#77012 会话转录覆盖、#85773 工作区被忽略等） | 见列表 | 多数仍为 OPEN |

**结论**：**2026.7.1 引入的启动崩溃** 是今天最集中的问题，至少 4 个 P0 直接相关。维护团队已在 #107227 和 #107220 等线程中提交修复 PR，但部分尚未合并或验证。其他 P1/P2 回归问题也存在多个，社区处于“新版本可用但不敢升”的观望状态。

---

## 6. 功能请求与路线图信号

| 功能要求 | 链接 | 分析 |
|---------|------|------|
| Linux/Windows Clawdbot 应用 | [#75](https://github.com/openclaw/openclaw/issues/75) | 长期呼声最高，但尚未有相关 PR 或开发者认领，可能排期靠后。 |
| Webhook 会话多轮支持（sessionKey 复用） | [#11665](https://github.com/openclaw/openclaw/issues/11665) | 文档与实际行为不匹配，已存在 linked PR，预计近期修复。 |
| Exec-approval 黑名单支持 | [#6615](https://github.com/openclaw/openclaw/issues/6615) | 安全增强，已有社区共识，但无专门 PR。 |
| 内存生命周期管理与 LLM 策展 MEMORY.md | [#87660](https://github.com/openclaw/openclaw/issues/87660) | 功能需求，尚无实现。 |
| AI 安全与质量可观测性事件 | [#82548](https://github.com/openclaw/openclaw/issues/82548) | 企业级需求，可能配合 OTEL 集成。 |
| 智能多 LLM 路由器（按任务选择模型） | [#107686](https://github.com/openclaw/openclaw/issues/107686) | 新用户请求，P3 标签，短期内难以落地。 |
| CLAW.md 清单支持 | [#106888 (PR)](https://github.com/openclaw/openclaw/pull/106888) | **已有实现 PR**，开启可读清单格式，若合并将影响所有包管理。 |
| 安全技能写入 API | [#108482 (PR)](https://github.com/openclaw/openclaw/pull/108482) | 新增安全 API 用于技能创建，涉及插件和未来学习工作流，属于路线图级别。 |

**路线图信号**：**CLAW.md 清单** 和 **安全技能写入 API** 两个 PR 今日提交，表明项目在向更规范、更安全的插件生态发展。其他长期功能（如跨平台客户端）仍缺乏实质性进展。

---

## 7. 用户反馈摘要

从今日 Issue 评论中提炼的真实痛点：

- **“完全无法使用”** – #104721 用户明确表示工具链完全被破坏，所有文件读取返回 `"(see attached image)"` 字面字符串，导致自动化流程瘫痪。
- **“升级后无法启动”** – #107220、#107227、#107694 等多位用户反映升级到 2026.7.1 后网关崩溃循环，`openclaw doctor` 无法自动修复，需要手动删除状态文件，对非技术用户极不友好。
- **“第二消息就失败”** – #102020 用户反馈在 Signal 和 DM 中发送第一条消息成功，第二条消息必失败，严重影响日常聊天使用。
- **“缓存命中率骤降”** – #94518 用户抱怨 DeepSeek 缓存命中率从正常水平跌至 10% 以下，API 账单飙升，要求回滚或提供配置开关。
- **“模型选择器不持久”** – #101763 用户反映托管 Molty 实例的模型 ID 被错误地替换为带点的 `claude-opus-4.8`，导致每次请求都失败。
- **“启动迁移警告反复出现”** – #90213 用户执行 `doctor --fix` 后警告依然存在，怀疑是迁移逻辑有遗漏。
- **“CPU 消耗过高”** – #91009 用户描述 Codex 集成导致 `openclaw-hooks` 进程 CPU 100%，系统响应缓慢。

**满意点**：部分用户对 v2026.7.2-beta.1 的远程编码会话表示期待，认为这是“提升开发效率的关键特性”。

---

## 8. 待处理积压

以下 Issue / PR 长时间未获维护者关注或进展缓慢，建议优先跟进：

| 项目 | 类型 | 链接 | 停滞天数（估算） | 影响 |
|------|------|------|----------------|------|
| [Bug] WebChat 会话转录每轮被覆盖（5.2 回归） | Issue (P1) | [#77012](https://github.com/openclaw/openclaw/issues/77012) | ~72 天 | 用户丢失所有历史消息 |
| [Bug] 模型回退链在 provider 配额耗尽时不触发 | Issue (P1, stale) | [#85103](https://github.com/openclaw/openclaw/issues/85103) | ~55 天 | 高可用性受损 |
| [Bug] iOS Talk 实时会话关闭后音频无法追加 | Issue (P1, stale) | [#91007](https://github.com/openclaw/openclaw/issues/91007) | ~40 天 | 语音交互完全不可用 |
| [PR] 在溢出压缩前截断工具结果 | PR (P1, waiting on author) | [#81190](https://github.com/openclaw/openclaw/pull/81190) | ~65 天 | 长会话可能卡死 |
| [Feature] 内存 LanceDB 注册

---

## 横向生态对比

好的，作为资深技术分析师，我为您呈上基于上述各项目日报的横向对比分析报告。

---

### AI 智能体与个人 AI 助手开源生态全景分析报告 (2026-07-16)

**报告日期：** 2026-07-16
**分析师：** [您的姓名/代号]

---

#### 1. 生态全景

当前，个人 AI 助手与自主智能体开源生态正处于 **“功能竞赛”与“稳定性阵痛”并存的快速迭代期**。一方面，以 OpenClaw 和 OpenHands SDK 为代表的项目正积极推进远程编码、会话管理等重磅功能，探索智能体的深度能力边界；另一方面，社区对 **连接可靠性、工具调用兼容性、会话持久化性能和升级后稳定性** 的呼声空前高涨，几乎所有重点项目都面临着因快速迭代而引入的 P0/P1 级回归 Bug 的困扰。整体上，生态正从“能用”向“好用”和“可靠”过渡，基础设施的打磨和稳定性的巩固已成为当前最核心的挑战。

#### 2. 各项目活跃度对比

下表量化了各项目在报告周期内的核心活跃度指标：

| 项目 | 新开/活跃 Issues | 关闭 Issues | 待合并 PRs | 合并/关闭 PRs | 版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 318 | 168 | 348 | 152 | ✅ v2026.7.2-beta.1 | **高风险高回报**：高强度迭代，社区活跃度最高，但稳定性（P0 Bug）问题突出。 |
| **Hermes Agent** | 168* (500 总更新) | 332 | 440 | 60 | ❌ 无 | **处理瓶颈**：社区参与度极高，但 PR 积压严重，维护团队响应能力饱和。 |
| **OpenHands SDK** | 11 | 3 | 8 | 7 | ✅ v1.36.1 | **健康高效**：活跃度适中，合并效率高，有版本发布，社区讨论聚焦于长期功能。 |
| **Pi** | 13* (54 总更新) | 41 | 5 | 6 | ❌ 无 | **积极修复**：虽无新版本，但 Bug 修复关闭率高，维护者响应迅速。 |
| **LiteLLM** | 69 | 27 | 221 | 91 | ✅ v1.94.0-dev.1 | **功能驱动**：专注于供应商兼容性和测试覆盖，PR 处理量大，社区问题集中。 |
| **Temporal** | 1 | 1 | 43* (70 总更新) | 27 | ❌ 无 | **后台优化**：PR 活动集中于内部组件优化和测试，社区讨论相对平稳。 |

*(注：Hermes 和 Pi 的数据为总更新量，具体新开数未明确)*

**结论**：OpenClaw 和 Hermes Agent 是社区活跃度的领头羊，但都面临着“量大管饱却消化不良”的挑战。LiteLLM 和 OpenHands SDK 则展现出更稳健的迭代节奏。Temporal 作为更底层的服务，活跃度体现在其内部工程优化上。

#### 3. OpenClaw 在生态中的定位

OpenClaw 在生态中扮演着 **“全能型平台探索者”** 的角色，其定位与竞争对手存在显著差异：

- **优势与差异化**：
  - **功能广度**：从远程编码会话、原生自动化节点到 Control UI，OpenClaw 试图提供一个高度集成的、面向开发者的“操作系统”级体验，远超普通的 Agent 编排工具。
  - **社区规模**：其 Issue/PR 活动量是其他项目的数倍，表明其社区规模最大，影响也最广。`#75 (Linux/Windows 客户端)` 这种长期热帖也侧面印证了其庞大的用户基础。
  - **技术野心**：直接挑战状态迁移、Provider 冗余代码合并 (#108474) 等深层架构问题，显示出其团队在推动技术演进上的决心。

- **劣势与风险**：
  - **稳定性成为最大短板**：多个 P0 启动崩溃和严重的回归 Bug (如 #104721) 表明，其快速迭代的代价是用户体验的剧烈波动。“新版本可用但不敢升”的社区氛围对平台心智信誉构成威胁。
  - **维护压力巨大**：348 个待合并 PR 是一个巨大的积压，可能成为社区贡献者士气的瓶颈。

- **与同类对比**：相比 Hermes Agent 的插件生态路线，OpenClaw 更像是一个“大一统”的复杂系统；对比 Pi 项目的“极客向终端工具”，OpenClaw 的目标是成为更通用的开发平台。其最大对手可能不是其他智能体项目，而是来自自身复杂性的管理挑战。

#### 4. 共同关注的技术方向

多个项目不约而同地涌现出相似的技术诉求，揭示了当前生态的通用瓶颈：

- **LLM 输出“幻觉”与严格格式校验的矛盾**：
  - **涉及项目**：OpenClaw (`#104721` 所有工具结果返回占位符)、Pi (`#6278` Claude 编辑工具因模型发明额外字段而失败)、LiteLLM (`#33221` gpt-5.6 工具调用因参数错误失败)。
  - **诉求**：社区强烈要求 Agent 方案能更好地包容 LLM 的“幻觉”行为，特别是在工具调用（function calling）的格式、字段校验和输出上，需要更鲁棒的容错机制。

- **升级与配置迁移的痛苦**：
  - **涉及项目**：OpenClaw (`#107220` 升级后启动崩溃)、Hermes Agent (`#26847` 服务集成后权限不符)、Pi (`#6619` Windows 路径问题)、LiteLLM (`#25762` SSO 许可证限制)。
  - **诉求**：用户期望无缝、低侵入的升级体验。配置的向后兼容、环境变量的灵活处理以及清晰的迁移文档，是所有项目需要立刻加强的环节。

- **会话管理与持久化**：
  - **涉及项目**：OpenClaw (`#102020` 第二消息冲突)、OpenHands SDK (`#3140` 急切加载性能问题)、Pi (`#6674` 会话管理增强)。
  - **诉求**：从简单的聊天记录管理到复杂的多会话、跨频道会话支撑，智能体需要更强大的会话管理和存储系统，包括懒加载、组织和搜索功能。

- **成本与性能优化**：
  - **涉及项目**：OpenClaw (`#94518` DeepSeek 缓存命中率骤降)、Pi (`#6665` TUI 高 CPU 占用)、OpenHands SDK (`#4100` 会话懒加载)。
  - **诉求**：随着智能体应用的深入，API 调用成本和本地资源占用问题日益突出。社区需要更智能的缓存策略、更高效的内存管理和更精确的配额控制。

#### 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent | Pi | OpenHands SDK | LiteLLM | Temporal |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **功能侧重** | 全能型开发平台 | 插件生态与集成 | 终端极致体验 | 构建 Agent 的基础 SDK | 统一模型 API 代理 | 分布式工作流编排 |
| **目标用户** | 技术型开发者 | 系统集成商、高级用户 | 极客、个人开发者 | 构建自定义 Agent 的团队 | 企业与开发团队 | 后端工程师、架构师 |
| **技术架构** | 复杂单体，高度集成 | 模块化，强插件系统 | 轻量终端应用 | 结构化 SDK，抽象层次高 | 轻量代理层，中间件 | 高可用分布式系统 |
| **主要竞争对手** | 传统 IDE Agent 插件 | 其他 Agent 框架 | 终端复用器+LLM | LangChain, AutoGen | 其他模型网关 | Azure Durable Functions |
| **当前状态** | 颠覆式创新，极不稳定 | 社区繁荣，维护瓶颈 | 精细打磨，稳定成熟 | 稳健发展，专注底层 | 兼容为王，稳步迭代 | 后台优化，架构演进 |

#### 6. 社区热度与成熟度

- **第一梯队（热度极高，快速迭代，稳定性挑战巨大）**：
  - **OpenClaw**: 创新的发动机，也是 Bug 的重灾区。社区处于“爱恨交织”的状态。
  - **Hermes Agent**: 社区参与度狂热，但维护团队明显成为瓶颈，PR 积压严重。项目成熟度受限于合并速度。

- **第二梯队（热度高，迭代快，可靠性基本稳固）**：
  - **Pi**: 社区规模虽不及前两者，但问题聚焦，修复迅速，属于“小而美”的典范，成熟度极高。
  - **LiteLLM**: 作为核心基础设施，其开发节奏稳健，聚焦于解决第三方集成问题，成熟度很高。

- **第三梯队（后台优化，面向开发者/专业用户）**：
  - **OpenHands SDK**: 作为底层工具，用户基数可能不直接反映在 Issue 数量上，但其开发节奏健康，社区讨论价值高。
  - **Temporal**: 项目和社区都偏后台，专注于分布式系统的稳健性，其活跃度体现在内部架构和测试的优化上。

#### 7. 值得关注的趋势信号

1.  **稳定性成为平台“心智”的基石**：OpenClaw 的教训表明，在 AI 智能体领域，功能的堆叠不再能完全补偿稳定性的缺失。用户对“不可预测”的容忍度正在迅速降低，因为智能体一旦不可靠，其生产力价值便会归零。**任何项目，在推动新功能的同时，必须将回归测试和升级迁移体验作为最高优先级的“特性”**。

2.  **LLM “幻觉”是智能体落地的最大工程障碍**：从 OpenClaw 到 Pi 再到 LiteLLM，多个项目都在与 LLM 输出的不规范性作斗争。未来的创新点可能不再是如何让 LLM 更强，而是如何设计鲁棒的 **“适配层”** 来消化 LLM 的“错误答案”，这将成为智能体工程的核心竞争力。

3.  **“厂商锁定”的新形态**：Hermes Agent 社区对 xAI OAuth 分级访问的愤怒（#26847）是一个强烈警示：**API 提供商的服务条款和认证机制，已成为影响开源项目用户体验和稳定性的新变量**。开发者需要警惕，对单一 AI 服务的深度依赖，可能引入隐性的“锁定”和风险。

4.  **“低成本基础设施”成为刚需**：DeepSeek 缓存问题（OpenClaw）、TUI 性能问题（Pi）、会话加载问题（OpenHands SDK）都指向同一个方向：**成本和资源效率是智能体能否被广泛采用的关键**。这不仅仅是优化 API 调用费，更是对整个软件栈（内存、CPU、存储）的精打细算。

---
**最终建议**：对于技术决策者，如果您追求**最前沿的功能和最大化的自由度**，且能接受可能的稳定性问题，**OpenClaw** 是首选。如果您需要**一个开箱即用、插件生态丰富但需要容忍配置复杂度的平台**，可选 **Hermes Agent**。对于追求**稳定、极客化、个人级的终端助手**，**Pi** 是最出色的选择。而 **OpenHands SDK** 和 **LiteLLM** 则是构建您自有系统的坚实底座。请务必关注各项目共同暴露出的 **“LLM 幻觉处理”** 和 **“升级迁移体验”** 两大核心痛点，这将是未来一段时间内行业竞争的焦点。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，以下是根据提供的 Hermes Agent GitHub 数据生成的 2026-07-16 项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026-07-16

## 1. 今日速览

项目进入高活跃度阶段。过去24小时内，项目处理了 **500条 Issues** 及 **500条 PRs**，展现了极高的社区参与度和开发者响应速度。虽然关闭了332个Issue，但 **440个待合并的PR** 形成了巨大积压，表明项目维护团队能力正面临严重考验，合并瓶颈是当前最突出的风险信号。社区关注点集中在 **Dashboard/Docker 认证**、**Telegram 插件适配** 以及 **xAI OAuth 集成**等关键痛点上。

## 2. 版本发布

**无新版本发布。**

## 3. 项目进展

过去24小时内，**60个PR被合并/关闭**，**332个Issue被关闭**，显示项目在持续消化积压工作。尽管合并总量不大，但修复了许多关键Bug。以下是几个重要的合并/关闭项，表明项目在稳定性和功能完善上取得了进展：

- **修复桌面端项目成员过载问题** (`#65262`)：修复了桌面客户端在加载项目 CWD/仓库成员时，会错误应用全局会话上限导致成员不完整的问题。
- **修复 Codex 迁移路径** (`#65261`)：修复了 `migrate()` 函数在某些情况下未正确使用 `CODEX_HOME` 环境变量的问题，增强了对自定义配置的兼容性。
- **修复 xAI OAuth 403 错误** (`#26847`)：社区广泛关注的 xAI OAuth 登录 Bug 已被关闭，但摘要未提及具体的根因和修复方式，需要关注后续排查记录。
- **大量 Dashboard 认证相关 Bug 被关闭** (`#58626`, `#58810`, `#55130`)：几个因 `BasicAuthProvider` 与 Dashboard 集成不当导致 HTTP 500 的 Bug 已被标记为 `implemented-on-main`，表明已在主分支上修复，可能在下一个版本中发布。

> 虽然许多 Bug 被关闭，但其中部分标记为 `duplicate` 或 `sweeper:implemented-on-main`，这意味着修复可能尚未正式发布，用户可能需要等待下一个 Release。

## 4. 社区热点

- **🔥 讨论最多：xAI OAuth 访问限制 (`#26847`，29 条评论)**
    - **链接**: [https://github.com/NousResearch/hermes-agent/issues/26847](https://github.com/NousResearch/hermes-agent/issues/26847)
    - **诉求**: 用户购买 `SuperGrok` 订阅 (30美元/月) 后，通过 OAuth 登录时后端返回 403 错误，拒绝对话。用户指责其营销宣传与实际权限不符，只允许 Heavy 用户使用。这引发了用户对 xAI 服务可靠性和承诺真实性的强烈质疑。
    - **信号**: 服务集成不仅仅是 API 调用，更需要处理好权限分层和订阅验证逻辑。

- **💡 社区规划：插件接口扩展追踪 (`#64182`，11 条评论)**
    - **链接**: [https://github.com/NousResearch/hermes-agent/issues/64182](https://github.com/NousResearch/hermes-agent/issues/64182)
    - **诉求**: 项目维护者 `@teknium1` 发起了插件接口扩展的社区讨论追踪。社区希望明确插件开发的方向，并为长期等待合并的 PR 提供一个可行的稳定发布路径。
    - **信号**: 插件生态是项目生命力的核心，社区急切需要更明确的扩展标准和更快的集成流程。

- **📣 Bug 回响：Dashboard Docker 认证问题 (`#59113`，8 条评论)**
    - **链接**: [https://github.com/NousResearch/hermes-agent/issues/59113](https://github.com/NousResearch/hermes-agent/issues/59113)
    - **诉求**: Docker 部署的 Dashboard 无法正常工作，这是一个持续引发讨论的热点问题，多个 Issue (`#58626`, `#58810`, `#55130`) 都在讨论类似问题。用户抱怨内置认证和后端限制导致在反向代理等复杂部署场景下难以使用。
    - **信号**: Docker 部署是用户重要使用场景，认证和网络配置的复杂性是需要优先解决的痛点。

## 5. Bug 与稳定性

| 严重程度 | Issue/PR | 描述 | 状态 |
| :--- | :--- | :--- | :--- |
| **P1** | `#26847` | xAI OAuth 返回403错误，后端子订阅限制与文档不符。 | **已关闭** (根因待查) |
| **P2** | `#59113` | Docker 部署的 Dashboard 在非内置认证环境下功能失效。 | 开放中 |
| **P2** | `#56004` | Qwen模型在 vLLM 推理时，多轮对话的思考链上下文丢失。 | 开放中 (已有 PR `#63255` 可能相关) |
| **P2** | `#64674` | Telegram 适配器在 `multiplex_profiles: true` 且 Token 位于非默认配置文件时启动失败。 | 开放中 (已有修复 PR `#63256`) |
| **P2** | `#62726` | Dashboard 跨标签页会话串线及创建新会话 (`/new`) 卡死。 | 开放中 |
| **P3** | `#56704` | `computer_use` 工具在 Linux/WSL 上因 `list_windows` 返回 `null` 值而崩溃。 | **已关闭** (已在主分支修复) |

**观察**：Dashboard 的认证和相关Bug数量众多，且重复率高（如 `#58626`, `#58810`, `#55130`），是当前稳定性方面最严重的问题。Telegram 配置相关问题 (`#64674`) 也是值得关注的热点。

## 6. 功能请求与路线图信号

- **即将纳入？**
    - **Telegram 渠道路由 (PR `#63256`)**: 修复 `multiplex_profiles` 功能，使单个 Telegram Bot 能根据不同聊天路由到不同 Hermes 配置。`#64674` Bug 的修复与此紧密相关，有望在下一版本得到支持。
    - **插件工具权限系统 (Issue `#21849`)**: 社区长时间呼吁的“按工具授予权限”系统，虽然默认未启用，但已有相关PR在推进，表明该功能已被列入待办。
    - **Tool Loop Guardrails 默认启用 (Issue `#25823`)**: 默认关闭的防止模型无限循环的工具护栏，社区希望默认启用。
- **热度较高，需观察**:
    - **可配置温度参数 (PR `#17565`, 10 👍)**: 用户强烈需求，但当前PR状态不明，热度持续不减。
    - **跨平台会话共享 (PR `#4335`)**: 用户期望 CLI 和 Telegram 等不同平台间的会话上下文能够共享。
    - **Vaultwarden 原生支持 (PR `#33126`, 6 👍)**: Bitwarden 用户希望直接用 Vaultwarden 替换 Bitwarden Secrets Manager 作为凭证后端。

## 7. 用户反馈摘要

- **满意点**:
    - 用户承认 Hermes Agent 功能强大，插件生态潜力大，社区规划积极（`#64182`）。
    - 报告 Bug 后得到快速确认和分类（部分 Issue 被标记为 `sweeper:implemented-on-main`），说明团队响应积极。
- **满意点/痛点**:
    - **配置复杂**: 用户普遍反映配置复杂，尤其是在 Docker、反向代理和多平台集成场景下（`#59113`, `#64674`）。
    - **文档与实际不符**: xAI 的 403 错误引发了对服务商信誉的信任危机（`#26847`）。
    - **默认行为不友好**: 如 `tool_loop_guardrails.hard_stop_enabled` 默认关闭，导致模型容易陷入死循环；`reasoning_effort` 在 Ollama 上被忽略（`#25758`）。
    - **桌面端体验**: 桌面客户端在远程网关连接成功时仍显示错误（`#41566`），以及会话过长导致输入不可见（`#53641`），用户体验较差。

## 8. 待处理积压

- **核心Agent功能长期未响应**: **`#17565` (可配置温度参数)** - 自4月29日提出，获得10个 👍 ，是该列表中最受欢迎的请求之一，但长期未得到实质性推动。
- **安装与上手教程问题**: **`#37246` (安装错误)** - 这是一个老生常谈的安装问题，用户从6月2日求助至今，虽更新频繁但未解决，可能影响新用户的第一印象。
- **安全与权限**: **`#21849` (工具权限门控系统)** - 虽然被关闭，但其核心诉求是构建更细粒度的安全模型，建议维护者将其作为规划的一部分，而不是一个简单的功能请求。
- **平台适配**: **`#40173` (Telegram频道路由)** - 这是一个高质量的功能请求，明确描述了问题和清晰的解决方案，但一直停留在“开放”状态，缺乏进展。结合最新的 PR #63256，希望该功能能被优先合并。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 | 2026-07-16

**数据采集时段**：2026-07-15 00:00 UTC ~ 2026-07-16 00:00 UTC  
**数据来源**：GitHub (OpenHands/software-agent-sdk)

---

## 今日速览

过去 24 小时内，OpenHands SDK 项目保持高活跃度：共产生 14 条 Issue 更新（11 条新开/活跃，3 条关闭）和 15 条 PR 更新（8 条待合并，7 条已合并/关闭）。**v1.36.1 正式发布**，主要修复了持久化订阅 LLM 的水化问题，并扩展了 agent-server 插件 API。与此同时，团队已启动 **v1.37.0 版本发布流程**（PR #4123），标志着新一轮功能和修复的集成。社区围绕结构化输出、工具集向后兼容等长期需求持续讨论，多个性能优化和安全性 PR 在本周期内完成合并，整体项目健康度良好。

---

## 版本发布

### v1.36.1（补丁版本）

- **发布时间**：2026-07-15  
- **链接**：[GitHub Release](https://github.com/OpenHands/software-agent-sdk/releases/tag/v1.36.1)
- **更新内容**：
  - `fix(sdk): rehydrate persisted subscription LLMs` – 修复持久化订阅 LLM 在恢复会话时状态不一致的问题
  - `feat: surface plugin contents in the agent-server plugins API` – 在 agent-server 插件 API 中公开插件内容，方便客户端获取已安装插件信息
- **破坏性变更**：无
- **迁移注意事项**：无需特殊迁移操作，建议所有使用 v1.36.x 分支的用户升级到此版本。

> **注意**：v1.37.0 的发布 PR（#4123）已于同日创建，包含更多功能和修复，预计近期发布。

---

## 项目进展

本周期内项目在性能、安全性、可观测性、会话管理等方面取得显著进展。以下为已合并/关闭的重点 PR：

| PR | 标题 | 关键贡献 |
|----|------|---------|
| [#4120](https://github.com/OpenHands/software-agent-sdk/pull/4120) | Release v1.36.1 | 完成版本发布 |
| [#4100](https://github.com/OpenHands/software-agent-sdk/pull/4100) | Lazily hydrate persisted conversations | **重大性能优化**：延迟加载持久化会话，大幅降低启动时的内存占用和加载时间（由 @neubig 提交） |
| [#4030](https://github.com/OpenHands/software-agent-sdk/pull/4030) | feat(agent-server): support deployment context on profile launches | 允许 Canvas 在按 ID 启动 Agent Profile 时注入部署特定的运行时服务指令和 Canvas 自有工具 |
| [#4110](https://github.com/OpenHands/software-agent-sdk/pull/4110) | feat(conversation): add client message context | 为客户端消息增加上下文元数据，提升可追踪性 |
| [#4010](https://github.com/OpenHands/software-agent-sdk/pull/4010) | fix(observability): stamp tool_call_id onto the TOOL span | 在可观测性链路中注入工具调用 ID，便于调试和导出 |
| [#3918](https://github.com/OpenHands/software-agent-sdk/pull/3918) | Fix REST API contract summary deduplication | 修复 PR 描述中 REST API 变更章节重复的问题（质量流程改进） |
| [#4125](https://github.com/OpenHands/software-agent-sdk/pull/4125) | feat(browser): record visible sessions as WebM | 浏览器模块新增会话录屏功能（WebM 格式） |

项目整体向 **更低资源消耗、更强部署灵活性、更好可观测性** 的方向迈出坚实一步。特别是 #4100 的合并将为拥有大量本地会话的用户带来立即可感知的体验提升。

---

## 社区热点

本周期内讨论最活跃的 Issue 集中于**结构化输出支持**和**工具集向后兼容**两大主题：

1. **[Feature] Structured Output**  
   - Issue [#2566](https://github.com/OpenHands/software-agent-sdk/issues/2566) | 评论数：16 | 👍 0  
   - 该需求自 2026-03-25 提出，至今仍是社区呼声最高的功能之一。用户希望在 SDK 中提供对 LLM 结构化输出的原生支持（类似 JSON mode / function calling 的加强版），以简化下游解析逻辑。虽然评论区已有 16 条讨论，但尚未有对应的 PR 或路线图明确归属。

2. **Research strategies for updating toolset while maintaining backward compatibility with persisted sessions**  
   - Issue [#2667](https://github.com/OpenHands/software-agent-sdk/issues/2667) | 评论数：8  
   - 社区对工具集演化中如何保持持久会话的兼容性充满关注。评论中探讨了 `DelegateTool` → `TaskToolSet` 等替换方案，期望有清晰的策略文档和迁移工具。

3. **SwitchLLMTool: LLM can't detect external profile switches**（已关闭）  
   - Issue [#3291](https://github.com/OpenHands/software-agent-sdk/issues/3291) | 评论数：7  
   - 该问题描述了当 LLM 配置文件被外部切换时，Agent 无法感知导致回答使用过时配置的问题。虽然已关闭，但其提出的观察影响了后续 PR #4030 的设计思路。

**分析**：社区对 SDK 的 **鲁棒性** 和 **灵活性** 要求越来越高，尤其是涉及多会话、多配置文件切换的场景。结构化输出需求长期未满足，建议团队在 v1.37.0 或后续版本中给予明确回应。

---

## Bug 与稳定性

本周期内报告的 Bug 按严重程度排列如下：

| 严重等级 | Issue | 描述 | 修复状态 |
|---------|-------|------|---------|
| **严重** | [#4121](https://github.com/OpenHands/software-agent-sdk/issues/4121) | Cloud Codex ACP 会话中 `CODEX_AUTH_JSON` 凭证刷新后未被后续会话继承，导致认证失败 | 已有 fix PR [#4124](https://github.com/OpenHands/software-agent-sdk/pull/4124) （待合并） |
| **严重** | [#4093](https://github.com/OpenHands/software-agent-sdk/issues/4093) | ACP 0.11 删除了 `NewSessionResponse` 中的 `models` 字段，导致 Gemini CLI 0.46 无法正常工作 | 无修复 PR，需依赖版本上限约束 |
| **中** | [#4098](https://github.com/OpenHands/software-agent-sdk/issues/4098) | 未认证情况下，LLM 初始化仍会调用 managed LiteLLM proxy 的模型信息接口 | 无修复 PR，但可通过移除空认证头时的请求优化 |
| **中** | [#3140](https://github.com/OpenHands/software-agent-sdk/issues/3140) | 服务启动时急切加载所有持久化会话，导致 1000+ 会话时内存和启动时间恶化 | 已通过 PR #4100 合并的懒加载方案解决 |
| **低** | [#3500](https://github.com/OpenHands/software-agent-sdk/issues/3500) | Anthropic Opus 4.8 模型不被支持，生成标题时出错 | 可能为模型配置缺失，未安排修复 |
| **绩效** | [#3153](https://github.com/OpenHands/software-agent-sdk/issues/3153) | 综合 profiling 发现的 19 个性能与正确性问题跟踪 | 部分已被 PR #4100 等解决，仍需持续关注 |

**关键动态**：性能最严重的 “急切加载” 问题（#3140）已通过 #4100 合入解决，大幅提升了大规模会话场景下的启动速度。而 ACP 协议版本兼容问题（#4093）需要团队决策是否对 `agent-client-protocol` 设置版本上限。

---

## 功能请求与路线图信号

以下功能请求获得较多关注，且与当前开发方向高度吻合，**可能被纳入 v1.37.0 或后续版本**：

1. **[Feature] Structured Output**  
   - Issue [#2566](https://github.com/OpenHands/software-agent-sdk/issues/2566) | 16 条评论  
   - 虽无直接关联 PR，但同为 “增强结构化能力” 的 PR [#3890](https://github.com/OpenHands/software-agent-sdk/pull/3890)（Selective Context Activation）处于开放状态，可能间接推动相关能力。

2. **SDK + agent-server: public from_persisted() entry points for AgentSettings and PersistedSettings**  
   - Issue [#3084](https://github.com/OpenHands/software-agent-sdk/issues/3084) | 标签：priority:medium  
   - 该需求要求公开持久化设置迁移的公共 API，与近期对会话持久化重构（#4100）紧密相关，存在纳入下个版本的可能性。

3. **Selective Context Activation**  
   - PR [#3890](https://github.com/OpenHands/software-agent-sdk/pull/3890) | 处于 Draft 状态  
   - 该功能通过消除仓库特定 AGENT.md 中的上下文膨胀，允许子 Agent 仅获得所需信息。虽然本周未合并，但若完善，可显著改善复杂项目中的 context window 管理。

4. **Expose Python conversation/event search APIs**  
   - Issue [#2623](https://github.com/OpenHands/software-agent-sdk/issues/2623) | 标签：investigation, proposal  
   - 提议在 Python SDK 中提供与 REST API 等价的搜索/过滤 API，使客户端开发者无需直接调用 HTTP 接口。该提案若被采纳，将大大提升 SDK 的易用性。

**路线图信号**：v1.37.0 的发布 PR（#4123）中包含了 `integration-test`, `behavior-test`, `security-scan` 等标签，尚未包含上述功能。建议社区关注后续里程碑。

---

## 用户反馈摘要

从近期 Issue 评论中提炼的真实用户痛点和期望：

- **痛点 – 凭证刷新不持久**：使用 Cloud Codex 的用户反馈，自动刷新的 ChatGPT 令牌在后续会话中丢失，每次必须手动重新认证。PR #4124 正在解决此问题。
- **痛点 – 配置文件切换无感知**：Agent 无法感知由 UI 或 API 触发的 LLM profile 切换，导致基于旧配置生成回答。该问题虽已关闭，但衍生了 `deployment context` 支持（#4030 已合并）。
- **痛点 – 性能负载高**：拥有上千个持久会话的团队反馈服务启动过慢、内存浪费严重。懒加载合并后，部分用户已在 #4100 评论区表示“加载速度快得多，内存使用大幅下降”。
- **期望 – 结构化输出原生支持**：多位开发者（如 @chase-prescient）希望 SDK 直接支持 LLM 输出解析，而非手动依赖函数调用。目前社区尚无明确时间表。
- **期望 – Anthropic 新模型支持**：@udt666 报告 Opus 4.8 报错，但未获得及时跟进，社区对此表达了一定不满（评论数虽仅 1 条，但标签 Stale 表明长期未处理）。

---

## 待处理积压

以下 Issue 或 PR 长期未获响应或进展放缓，建议维护者优先关注：

| 类型 | 编号 | 标题 | 创建时间 | 最后更新 | 备注 |
|------|------|------|---------|---------|------|
| Issue | [#2566](https://github.com/OpenHands/software-agent-sdk/issues/2566) | [Feature] Structured Output | 2026-03-25 | 2026-07-15 | 16 条评论，社区呼声极高，但无官方回应 |
| Issue | [#2667](https://github.com/OpenHands/software-agent-sdk/issues/2667) | Research strategies for updating toolset while maintaining backward compatibility | 2026-04-02 | 2026-07-15 | 带 `Stale` 标签，可能被自动标记 |
| Issue | [#2623](https://github.com/OpenHands/software-agent-sdk/issues/2623) | Expose Python conversation/event search APIs | 2026-03-31 | 2026-07-15 | 已有初步设计，但无对应 PR |
| Issue | [#3084](https://github.com/OpenHands/software-agent-sdk/issues/3084) | Public from_persisted() entry points | 2026-05-06 | 2026-07-15 | 标有 `priority:medium`，关联近期重构 |
| PR | [#3890](https://github.com/OpenHands/software-agent-sdk/pull/3890) | Selective Context Activation | 2026-06-26 | 2026-07-15 | Draft 状态超过 3 周，作者 @jmacd867 未更新 |
| Issue | [#3500](https://github.com/OpenHands/software-agent-sdk/issues/3500) | Anthropic Opus 4.8 not supported | 2026-06-04 | 2026-07-15 | `Stale` 标签，用户等待响应 |

**建议**：对于 `Stale` 标签的 Issue，维护者应主动判断是否需要关闭、重新标记或继续讨论。结构化输出 (#2566) 和工具集兼容策略 (#2667) 应被视为高优先级路线图讨论项，建议在 v1.37.0 发布后以 RFC 形式推进。

---

**总结**：OpenHands SDK 本周在性能和安全性上取得实质性突破，社区对结构化输出和工具演化的需求持续发酵。v1.36.1 修复了关键水化问题，v1.37.0 的发布流程已启动，项目整体处于健康向上的发展轨道。

*— 报告由 AI 分析师自动生成，数据截至 2026-07-15 UTC 24:00。*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，以下是为您生成的 Pi 项目 2026年7月16日 项目动态日报。

---

## Pi 项目动态日报 | 2026-07-16

### 1. 今日速览

项目社区在过去24小时内保持高度活跃，共产生54条 Issue 更新和11个 PR。虽无新版本发布，但团队修复效率极高：关闭/合并了41个 Issue 和6个 PR。社区焦点主要围绕 **OpenAI Codex 连接稳定性** 与 **Claude 模型编辑工具兼容性** 两大问题，同时涌现出多个围绕 `session-id` 头部处理、TUI 渲染性能及 Windows 平台兼容性的中优先级 Bug 修复。总体来看，项目健康状况良好，维护者响应迅速，社区贡献积极。

### 2. 版本发布

**无**

### 3. 项目进展

过去24小时，团队合并或关闭了6个 PR，推进了多个关键领域的修复与优化：

- **关键Bug修复**：
    - **[PR #6659]** 修复了 `openai-codex` 的 `session-id` 头部未被正确截断（clamped）的问题，该问题曾导致请求失败。此 PR 直接关闭了 Issue #6630。
    - **[PR #6681]** 修复了 Windows 平台上 `npm` 包检查后终端标题未被重置的问题，关闭了 Issue #6629。
    - **[PR #6667]** 为 TUI 的 `Box` 和 `Container` 渲染组件添加了空值保护，防止在扩展安装/卸载后因组件引用失效而导致的程序崩溃。
- **配置与兼容性优化**：
    - **[PR #6683]** 修复了 `coding-agent` 无法正确加载带命名空间的技能（如 `inc:ship-it`）的问题，解决了启动时错误报告“技能冲突”的困扰。
- **功能增强**：
    - **[PR #6671]** 开始在分支摘要、压缩和工具结果条目中添加使用量（usage）元数据，为后续更精准的用量统计和分析奠定了基础。
- **文档更新**：
    - **[PR #6660]** 为 `coding-agent` 添加了关于 ACP 分支的计划说明，提升了项目透明度。

**总结**：项目在关键 Bug 修复上取得了显著进展，尤其是解决 Codex 连接和 TUI 稳定性问题。同时，对扩展和技能系统的兼容性修补，体现了项目在对社区生态的支持上持续投入。

### 4. 社区热点

本周社区讨论的焦点高度集中在 **AI供应商的连接与兼容性问题**。

- **🔥 最热 Issue: `openai-codex` 连接可靠性问题** 🔥
    - **[Issue #4945]** 以 **75条评论** 和 **30个 👍** 成为今日讨论焦点。用户报告 `openai-codex` / `gpt-5.5` 在 TUI 交互时频繁卡死在 `Working...` 状态，只能通过按 `Escape` 恢复。问题在过去几天内重复出现，说明这是一个影响广泛且体验糟糕的严重问题。
    - **关联 Issue**: [#6673] 指出 Codex 返回的 Cloudflare 520 错误页面会暴露用户 IP 和 Ray ID，存在信息泄露风险。

- **🌶️ 次热 Issue: Claude 模型与编辑工具兼容性差**
    - **[Issue #6278]** 获得 **22条评论** 和 **9个 👍**。用户反馈新版 Claude 模型在与 Pi 的 `edit` 工具协作时，有高达 **20%** 的编辑操作会因 LLM 发明了额外的 `new_text_x`, `type` 等字段而失败。这指向了当前工具调用格式验证的僵化问题，可能需要增加对 LLM 幻觉的容错。

**分析**：社区的核心诉求是 **可靠性和兼容性**。用户期待 Pi 能稳定连接各种 AI 后端（尤其是主流的 OpenAI 和 Anthropic 模型），并在工具调用上展现更好的鲁棒性。修复这两类问题应作为下一版本的最高优先级。

### 5. Bug 与稳定性

除上述社区热点外，今日还报告了多个 Bug，按严重程度排列如下：

1.  **严重 - TUI 高 CPU 占用与性能问题**:
    - **[Issue #6665]** 报告在长对话流式输出时，`Intl.Segmenter` 未缓存及 Markdown 全文重绘导致单个 CPU 核心占用 **~100%**。这是一个核心性能回归问题。
    - **[Issue #6652]** 指出 TUI 的崩溃日志路径被硬编码为 `~/.pi/agent/pi-crash.log`，忽略了 `PI_CODING_AGENT_DIR` 环境变量，导致用户自定义配置失效。

2.  **中等 - 身份验证与会话处理**:
    - **[Issue #6657] (进行中)** AWS Bedrock 的 `AWS_PROFILE` 身份验证持续失效，返回 `AccessDeniedException: 403`。
    - **[Issue #6686] / [#2725]** 用户反映 Pi 会随机自动登出 GitHub，影响 `github-copilot` 等功能的正常使用。
    - **[Issue #6690]** 切换回历史会话时，消息可能出现顺序错乱，工具调用和助手消息混杂在一起。

3.  **轻微 - 平台兼容与配置**:
    - **[Issue #6619] (进行中)** Windows 平台上，依赖同 npm 包的扩展显示为绝对路径而非友好名称。
    - **[Issue #6647] (进行中)** 会话压缩（Compaction）操作在一次瞬时的网络流中断后直接失败，缺乏重试机制。

**已有修复 PR**: 针对 [#6665] 和 [#6652] 的性能与日志问题，目前暂无已合并的 Fix PR。针对 [#6619] 的 Windows 路径问题， **[PR #6680]** 已提交并处于开放状态。

### 6. 功能请求与路线图信号

今日收到的功能请求主要围绕 **会话管理和扩展性**：

- **会话管理增强**:
    - **[Issue #6674]** 用户希望 Pi 能够支持浏览、重命名、分组（文件夹）和归档会话，将当前扁平的会话列表变成一个可管理的组织系统。
    - **[Issue #5263]** 提议将“模型切换”和“思考级别”的更改默认设为“仅当前会话生效”，并通过 `/settings` 菜单提供一个全局默认值的设置入口，以区分临时调整和永久配置。

- **扩展与开发支持**:
    - **[Issue #6691]** 请求提供一个独立的、极简的“前端编排器”扩展示例代码，以指导社区开发者如何创建和管理子代理。
    - **[Issue #6688]** 指出扩展的通用选择器 `ctx.ui.select` 没有视口滚动功能，当选项过多时会导致内容超出屏幕。这是一个影响扩展开发体验的 UI 缺陷。

- **集成与模型**:
    - **[PR #6651] (打开中)** 增加了对 xAI 设备的 OAuth 认证，并将 `grok-4.5` 模型路由到新的 Responses API。
    - **[PR #6216] (打开中)** 尝试为 Amazon Bedrock 的 Mantle 服务添加 OpenAI Responses API 提供者。

**路线图信号**: 从 [PR #6651] 和 [PR #6216] 可以看出，项目正努力支持更多新兴的 AI 模型和服务接口。会话管理 ([#5263]) 是用户呼声较高的显性需求，很可能成为下一个版本的重点开发方向。

### 7. 用户反馈摘要

- **痛点与不满**:
    - “`openai-codex` 卡在 `Working...` 后只能 `Escape` 退出，体验极差。” — *#4945*
    - “Claude 的编辑失败率高达 20%，完全无法接受。” — *#6278*
    - “`Intl.Segmenter` 性能太差，模型说话时整个终端卡死。” — *#6665*
- **使用场景与建议**:
    - 用户希望配置 **会话内临时模型切换** 以实现快速测试，而无需每次修改全局文件。— *#5263*
    - **长期用户** 希望 Pi 能提供文件夹和归档功能来管理大量会话。— *#6674*
- **满意之处**:
    - 用户对团队处理 [PR #6659] 和 [PR #6681] 等 Bug 修复合并的速度和效率表示认可。

### 8. 待处理积压

以下为当前未解决的重要 Issue，提醒维护者关注：

- **[Issue #2310]: 创建 `flake.nix`**
    - **评论**: 6 | **👍**: 16
    - **状态**: 已关闭，标记为 `[no-action]`。该 Issue 请求支持 Nix 包管理器，用户关注度高（16个 👍），但项目团队似乎未计划推进。建议明确回复社区该功能是否会在后续路线图中考虑，以避免用户反复提报。
- **[Issue #4945]: `openai-codex` 连接可靠性问题**
    - **评论**: 75 | **👍**: 30
    - **状态**: 打开中（进行中）。这是社区当前的绝对焦点，涉及项目核心使用体验，应优先解决。
- **[Issue #6278]: 新版Claude模型编辑失败**
    - **评论**: 22 | **👍**: 9
    - **状态**: 打开中。这是第二大用户痛点，同样影响核心工作流。
- **[PR #6594]: 实现 SQLite 会话存储**
    - **评论**: 0
    - **状态**: 打开中。这是一个重大架构级改动，旨在用 SQLite 替代现有文件存储，可能对性能和可靠性有较大提升。目前缺乏讨论，建议维护者尽快审阅并给予反馈。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

## LiteLLM 项目动态日报 — 2026-07-16

### 1. 今日速览
- 过去 24 小时 Issue 活动 96 条（新开/活跃 69，关闭 27），PR 活动 312 条（待合并 221，已关闭/合并 91），整体**非常活跃**。
- 发布开发版 `v1.94.0-dev.1`，聚焦 Docker 镜像签名验证，无公开破坏性变更。
- 社区讨论集中：SSO 无限登录（#25762, 14 评论）、模型列表对普通用户空白（#17475, 13 评论）以及 OpenAI gpt‑5.6 系列工具调用失败（#33221）是高热度议题。
- 多项关键修复与功能 PR 今日密集提交，包括 Langfuse v4 SDK 升级（#33391）、Bedrock Nova 模型检测修复（#33469/#33470）、PEP 604 类型注解兼容（#33466）等。
- 测试覆盖持续提升：新增 MCP 网关端到端测试（#33102/#33263）、Claude Code e2e 测试修复（#33433/#33426）。

---

### 2. 版本发布
- **v1.94.0-dev.1**（开发版）  
  - 主要变更：统一使用 Cosign 签名所有 Docker 镜像，提供可验证的签名密钥（commit `0112e53`）。  
  - 影响与迁移：此版本无破坏性变更；用户可通过 `cosign verify` 检查镜像完整性。因是 dev 版本，建议仅用于测试环境。

---

### 3. 项目进展 — 今日合并/关闭的重要 PR
| PR | 标题 | 状态 | 影响 |
|----|------|------|------|
| [#33449](https://github.com/BerriAI/litellm/pull/33449) | feat(ui): add reusable BetaBadge and use it for Projects sidebar item | **已合并** | UI 组件化，提升项目侧边栏可维护性 |
| [#33438](https://github.com/BerriAI/litellm/pull/33438) | build: raise requires-python cap to <3.15 so Python 3.14 installs current releases | **已关闭** | 扩展 Python 版本兼容至 3.14 |
| [#33102](https://github.com/BerriAI/litellm/pull/33102) | test(e2e): cover MCP gateway auth headers and per‑server max concurrency | **已合并** | 完善 MCP 网关的端到端测试 |
| [#33263](https://github.com/BerriAI/litellm/pull/33263) | test(e2e): cover MCP core happy paths: upstream auth, access control, allowed_tools, aggregate routing | **已合并** | 增强 MCP 核心功能测试覆盖率 |
| [#33391](https://github.com/BerriAI/litellm/pull/33391) | feat(langfuse): upgrade SDK and OTel ingestion to v4 | **已合并** | 解决用户长期期待的 Langfuse v4 支持 Issue (#24123) |
| [#33261](https://github.com/BerriAI/litellm/pull/33261) | fix(proxy): share CLI SSO login sessions across workers without enable_redis_auth_cache | **已合并** | 修复多 worker 下 SSO 会话不共享问题 (#33253) |
| [#33471](https://github.com/BerriAI/litellm/pull/33471) | fix(router): strip foreign Gemini thought signatures on vertex_ai/gemini fallback | **已合并** | 修复 Gemini 回退时 thought 签名污染问题 (#32140) |
| [#33466](https://github.com/BerriAI/litellm/pull/33466) | fix: handle PEP 604 union type hints in function_to_dict | **已合并** | 消除工具函数中使用 `str | None` 等联合类型时的 AttributeError |
| [#33467](https://github.com/BerriAI/litellm/pull/33467) | fix(utils): report missing API keys in validate_environment for sambanova, hyperbolic, lambda_ai | **已合并** | 补全三个供应商的环境验证漏洞 |
| [#33469](https://github.com/BerriAI/litellm/pull/33469) | fix(bedrock): recognize jp and global geo prefixes in Nova 2 model detection | **已合并** | 修复日本区域 Nova 2 模型无法识别问题 (#33211) |
| [#33470](https://github.com/BerriAI/litellm/pull/33470) | fix(pricing): replace nonexistent apac.amazon.nova-2-lite-v1:0 with jp geo id | **已合并** | 修正 Nova 2 Lite 定价映射键，避免计费错误 (#33211) |

今日共合并/关闭 91 个 PR，以上为最具代表性部分。项目在**测试基础设施建设、第三方 SDK 兼容性、供应商特定修复**方面取得显著进展。

---

### 4. 社区热点
1. **[#25762](https://github.com/BerriAI/litellm/issues/25762) — Feature: unlimited SSO Login with Standard Plan**  
   - **评论 14 / 👍 13**，用户强烈要求移除 Standard Plan 5 用户限制。  
   - 诉求：企业用户需更多 SSO 账户，但不想升级付费。预计将导向定价策略调整。

2. **[#17475](https://github.com/BerriAI/litellm/issues/17475) — Bug: LiteLLMProxy no longer show the list of models to the users**  
   - **评论 13 / 👍 5**，自某次更新后普通用户在 UI 上看不到模型列表，管理功能受损。  
   - 该问题持续 7 个月仍未解决，社区不满度上升。

3. **[#24123](https://github.com/BerriAI/litellm/issues/24123) — Feature: Support Langfuse Python SDK v4**  
   - **评论 8 / 👍 11**，今日已随 PR #33391 合并而解决，社区反馈积极。

4. **[#33221](https://github.com/BerriAI/litellm/issues/33221) — Bug: Function tools fail with reasoning_effort error for OpenAI gpt‑5.6 family**  
   - 新开 bug，3 个评论，但因其涉及最新 GPT 模型立即受阻且影响大，推测很快会有修复 PR。

---

### 5. Bug 与稳定性
| Issue | 严重程度 | 问题简述 | 修复状态 |
|-------|---------|---------|---------|
| [#33221](https://github.com/BerriAI/litellm/issues/33221) | 🔴 严重 | gpt‑5.6 系列工具调用因 `reasoning_effort` 错误失败，阻断上游新模型使用 | 暂无目标 PR |
| [#33404](https://github.com/BerriAI/litellm/issues/33404) | 🟠 中等 | 流式上游重置被转换为合成 `finish_reason: stop`，导致下游误判 | 无修复 |
| [#33328](https://github.com/BerriAI/litellm/issues/33328) | 🟡 低危 | Replicate 运行时回退时秒/毫秒单位混用，影响计费准确性 | 需确认是否已修复 |
| [#33327](https://github.com/BerriAI/litellm/issues/33327) | 🟡 低危 | Provider 预算配置缺少 `max_budget` 时误移除其部署 | 无修复 |
| [#32218](https://github.com/BerriAI/litellm/issues/32218) | 🟡 低危 | Z.AI 文档中 `glm-5.2[1m]` 模型返回 `Unknown Model` | 无修复 |
| [#32335](https://github.com/BerriAI/litellm/issues/32335) | 🔴 严重 | /responses API 多轮对话中丢失 Reasoning Items，v1.83.7 回归 | 无修复 |
| [#26752](https://github.com/BerriAI/litellm/issues/26752) | 🟠 中等 | /v1/messages 忽略客户端指定的 `timeout`，与 /chat/completions 行为不一致 | 已关闭（未修复） |
| [#25691](https://github.com/BerriAI/litellm/issues/25691) | 🟠 中等 | AgentCore: Strands 代理 SSE 流事件被静默丢弃 | 已僵持 3 个月 |

**重点关注**：gpt‑5.6 不兼容性和 /responses API 回归直接影响用户当前工作流，亟待修复。

---

### 6. 功能请求与路线图信号
| 需求 | 热度 | 对应 PR / 状态 |
|------|-----|----------------|
| SSO 无限登录 (#25762) | 🔥🔥🔥 | 暂无，可能影响商业模式 |
| Langfuse v4 支持 (#24123) | ✅ 已实现 | PR #33391 今日合并 |
| MCP 工具增强：权限、路由、auth (#33102/#33263) | ✅ 已测试 | 测试覆盖完成 |
| yarl 安全修复 (#33410) | 🟡 待审查 | 依赖升级 `yarl>1.23.0` |
| 团队批量更新成员 (#32958) | 🟡 开放中 | PR #32958 需 review |
| Tag Wildcard Budgets (#10873) | ❄️ 已关闭 | 旧需求，已关闭标记 stale |

未来版本大概率包含：Langfuse v4 正式发布、SSO 登录改进、MCP 生产级特性支持。

---

### 7. 用户反馈摘要
- **正面**：Langfuse v4 升级获得大量 👍，用户表示“终于可以跟上 Langfuse 最新版本”。  
- **痛点**：
  - 模型管理 UI 对非管理员无效（#17475）：“升级后普通用户看不到任何模型，工作无法继续。”  
  - SSO 5 用户限制：“我们团队 15 人，却要为每个人购买付费许可证，不合理。”  
  - gpt‑5.6 全系不兼容：“已迁至 GPT‑5.6，但 LiteLLM 不支持，无法使用 function calling。”  
  - Streaming 可靠性：“工具流中偶尔丢失 tool_use.input，重新请求可能成功，无法在生产环境信任。”  
  - 多轮对话回归：“升级到 1.83.7 后 /responses API 总是 400，回退到稳定版才正常。”  

- **建议**：多位用户呼吁增加自动化测试覆盖流式场景、优化 SSO 定价策略。

---

### 8. 待处理积压 — 长期未响应的重要 Issue / PR
| 项目 | 类型 | 最后更新 | 概述 | 需关注的维护者 |
|------|------|---------|------|---------------|
| [#17475](https://github.com/BerriAI/litellm/issues/17475) | Bug | 7 个月前 | 模型列表对普通用户不可见 | @ishaan-jaff |
| [#13840

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目日报 (2026-07-16)

---

## 1. 今日速览

过去 24 小时内，Temporal 项目保持了极高的开发活跃度，共产生 **70 条 Pull Request 更新**（其中 27 条已合并或关闭），反映出团队在多个功能线（CHASM 优化、测试基础设施改进、稳定性修复）上持续投入。Issues 层面则相对平稳，仅处理了 2 条（1 新开、1 已关闭），无新版本发布。整体来看，项目正处于密集的迭代期，重点打磨内部组件（如匹配服务、调度器、Nexus 操作）和测试体系。

---

## 2. 版本发布

**无** — 过去 24 小时内无新版本发布。

---

## 3. 项目进展

以下为本日报送周期内 **已合并或关闭** 的重要 PR，它们推动了关键功能与稳定性改进：

| PR | 标题 | 状态 | 简述 |
|----|------|------|------|
| [#11000](https://github.com/temporalio/temporal/pull/11000) | Load balance mixedbrain frontend RPCs | **CLOSED** | 改变前端请求固定路由策略，改为在双服务器间负载均衡，用于暴露混合脑模式（mixedbrain）的 bug。 |
| [#11047](https://github.com/temporalio/temporal/pull/11047) | Fix reset backlog count after gap | **CLOSED** | 修复当 `priTaskReader` 通过 `setReadLevelAfterGap` 推进 ack level 后未显式写入内存状态，导致 backlog 计数无法正确重置的问题。 |
| [#10874](https://github.com/temporalio/temporal/pull/10874) | Dynamic partitioning: sync backlog counts | **CLOSED** | 在分区缩放状态中引入量化后的 backlog 计数，并用于简单缩放器，为基于大 backlog 的缩放和负载均衡奠定基础。 |

此外，还有多个面向稳定性的修复合并，例如：
- [#11096](https://github.com/temporalio/temporal/pull/11096) / [#11095](https://github.com/temporalio/temporal/pull/11095) / [#11093](https://github.com/temporalio/temporal/pull/11093)：一组 **cherry‑pick** 到不同云版本的补丁，为匹配 handler API 统一添加 panic 捕获。

**项目向前迈进的总结**：  
- **稳定性**：修复了重置操作后 backlog 计数的逻辑错误，并强化了匹配 handler 的容错能力。  
- **可观测性**：动态分区缩放开始纳入 backlog 指标，为运营监控提供依据。  
- **测试质量**：PR [#11069](https://github.com/temporalio/temporal/pull/11069) 和 [#10129](https://github.com/temporalio/temporal/pull/10129) 推动测试集群资源优化与隔离，减少 CI 峰值等待时间。

---

## 4. 社区热点

尽管 PR 评论数在本次数据中未显示，但以下议题因讨论深度或涉及长期痛点而值得关注：

- **[#3769](https://github.com/temporalio/temporal/issues/3769) [Enhancement] Any plan to support MS SQL Server?**  
  创建于 2023 年，至今仍有 6 条评论，并在昨日（2026‑07‑15）被更新。用户明确表达了对 Microsoft SQL Server 后端的迫切需求，尤其是面向本地化部署场景。该议题反映了企业级用户对数据库生态多样性的诉求。

- **[#11024](https://github.com/temporalio/temporal/pull/11024) VTS: add a circuit breaker for time skipping**  
  引入固定窗口计数器检测时间跳跃无限循环，防止资源浪费。该功能直接改进了「虚拟时间」在测试中的鲁棒性，受到关注。

- **[#11084](https://github.com/temporalio/temporal/pull/11084) Add opt-in poller_scale_decision metric**  
  增加可观察性指标以理解匹配服务 poller 自动调优的决策原因。这有助于运维人员定位扩缩容异常，属于社区高频请求的“为什么”类指标。

**社区诉求分析**：  
长期未决的 MSSQL 支持与新的可观测性指标表明，社区一方面希望拓展部署灵活性，另一方面渴望更细粒度的运行时行为洞察。

---

## 5. Bug 与稳定性

- **[#10690](https://github.com/temporalio/temporal/issues/10690) [CLOSED] ResetWorkflowExecution returns "workflow not found" when targets an older run**  
  严重性：**中等**。该 Bug 涉及重置操作在目标 run 已删除且无当前执行时返回错误。已在昨日关闭，推测有对应修复合并（如 PR [#11042](https://github.com/temporalio/temporal/pull/11042) 可能覆盖此场景）。

- **[#11097](https://github.com/temporalio/temporal/pull/11097) [OPEN] fix task token invalidation after resetting an activity**  
  严重性：**高**。独立活动被重置后，旧的 task token 仍可 heartbeat 或完成，导致状态不一致。PR 通过引入单调递增的活动尝试戳（`activity_attempt_stamp`）来强制校验，正在审查中。

- **[#11081](https://github.com/temporalio/temporal/pull/11081) [OPEN] Block concurrent schedule changes during V2-to-V1 migration**  
  严重性：**中**。调度器 V2→V1 迁移期间若收到并发更新/删除请求，可能导致自动化行为暂停/数据不一致。PR 通过增加 fence 机制予以封锁。

- **[#11094](https://github.com/temporalio/temporal/pull/11094) [OPEN] Clean up test resources after versioning suites**  
  属于测试稳定性改进，虽非生产 Bug，但长期残留的 workflow 可能污染后续测试结果。

**综合评估**：昨日报告的 Bug 集中在重置操作、活动 token 校验和调度迁移并发问题上，当前均有活跃修复 PR。整体稳定性维持在良好水平。

---

## 6. 功能请求与路线图信号

- **MS SQL Server 支持**（[#3769](https://github.com/temporalio/temporal/issues/3769)）  
  仍为开放需求，无明确 PR 关联。若团队考虑扩展数据库支持，此议题可能被纳入下一版本路线图。

- **Standalone Activities 操作命令**（[#10106](https://github.com/temporalio/temporal/pull/10106) [OPEN]）  
  实现 `PauseActivityExecution`、`ResetActivityExecution` 等服务器端控制 API，将活动生命周期管理从工作流代码中解耦。该 PR 已有数月历史，近期仍有更新，说明团队持续投入，有望在未来版本落地。

- **CHASM Scheduler 默认值保护**（[#11099](https://github.com/temporalio/temporal/pull/11099) & [#11098](https://github.com/temporalio/temporal/pull/11098)）  
  两个 PR 均针对 CHASM 调度器的克隆问题与 `MaxActionsPerExecution` 边界校验，属于对已有功能的安全加固，路线图信号偏向“健全化”而非新特性。

- **SignalWorkflow 作为重置后操作**（[#11042](https://github.com/temporalio/temporal/pull/11042)）  
  实现 `ResetWorkflowExecution` 中支持 signal 作为后置操作，增强重置场景的灵活性。已进入审查阶段，预计较快合入。

---

## 7. 用户反馈摘要

从两条最新 Issue 的评论中可提取以下用户声音：

- **MSSQL 支持需求强烈**（[#3769](https://github.com/temporalio/temporal/issues/3769)）：用户 @raymondsze 表示 Temporal 解决其分布式事务问题，但因客户强制要求 MS SQL Server，当前 MySQL/PostgreSQL 仅支持无法满足 on‑premise 部署场景。评论中另有多位用户表达类似愿望，说明这是一项真实的商业化瓶颈。

- **重置操作遗留问题得到修复**（[#10690](https://github.com/temporalio/temporal/issues/10690)）：报告者 @jiechenz 详细描述了当 workflor 当前运行被删除时，重置会误报“workflow not found”。该问题已关闭，用户满意度应得到提升。

- **无负面评价**：当前未发现对性能或 API 设计的明显抱怨。

---

## 8. 待处理积压

| 编号 | 标题 | 创建时间 | 最后更新 | 状态 | 备注 |
|------|------|----------|----------|------|------|
| [#3769](https://github.com/temporalio/temporal/issues/3769) | Any plan to support MS SQL Server? | 2023-01-03 | 2026-07-15 | **OPEN** | 超过 3.5 年无官方实质性回应。社区贡献者可能需要指导。 |
| [#10106](https://github.com/temporalio/temporal/pull/10106) | Implement Pause/Unpause/Reset/UpdateOptions for standalone activities | 2026-04-28 | 2026-07-15 | **OPEN** | 持续活跃但长期未合并，建议团队评估优先级并给出预期上线时间。 |
| [#10129](https://github.com/temporalio/temporal/pull/10129) | Reduce test runner resources | 2026-04-30 | 2026-07-15 | **OPEN** | 测试基础设施优化，虽非功能缺陷，但影响 CI 效率和开发者体验。 |

**提醒**：上述积压项若无维护者介入，可能会逐渐降低社区贡献意愿。建议至少对 [#3769](https://github.com/temporalio/temporal/issues/3769) 给出正式答复（例如“当前无计划”或“接受社区贡献”）。

---

**总体健康度**：⭐⭐⭐⭐（4/5）  
项目开发节奏强劲，合并/关闭率较高；社区热点集中于数据库扩展和可观测性，团队已在对应方向上产出相关 PR。仅需注意长期积压的“信号”性 Issue 的响应及时性。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*