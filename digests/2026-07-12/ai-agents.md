# OpenClaw 生态日报 2026-07-12

> Issues: 412 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-11 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目日报 – 2026-07-12

**数据来源**: GitHub `github.com/openclaw/openclaw`  
**统计周期**: 2026-07-11 UTC 至 2026-07-12 UTC（数据截至 2026-07-12 日报生成时）

---

## 今日速览

过去 24 小时项目活跃度极高：共处理 **412 条 Issue** 更新（新开/活跃 237，关闭 175）、**500 条 PR** 更新（待合并 294，已合并/关闭 206），并发布了 **v2026.7.1-beta.5** 测试版本。社区讨论集中在**会话隔离失败、内存泄漏、工具输出丢失**等严重影响可用性的回归问题上；同时，大批量安全相关的文件读取容量限制 PR 正在排队合并，表明项目正系统性加固攻击面。总体而言，项目处于高频迭代与稳定性修复并行的阶段，健康度良好但需警惕多个 P0/P1 bug。

---

## 版本发布

### v2026.7.1-beta.5

- **发布时间**: 2026-07-11  
- **下载**: [GitHub Release](https://github.com/openclaw/openclaw/releases/tag/v2026.7.1-beta.5)

#### ✨ 主要亮点

- **对话式引导 (Conversational onboarding)**: Crestodian 现在在 CLI、Web 安装和 macOS 应用中运行完整的 agent-loop 设置，包括 AI 引导的 provider 配置、绑定精确操作的模型判定审批、掩码凭据提示，以及无模型时的确定性回退。
- **无需破坏性变更**: 该版本主要新增特性，未标记破坏性变更或迁移注意事项。建议用户在升级后运行 `openclaw doctor --fix` 以检查状态一致性。

---

## 项目进展

### 合并/关闭的重要 PR（过去 24 小时）

| PR | 类型 | 说明 |
|----|------|------|
| [#104740](https://github.com/openclaw/openclaw/pull/104740) | CI | 修复 Full Release Validation 中 target tool 版本固定错误，确保兼容性。 |
| [#104741](https://github.com/openclaw/openclaw/pull/104741) | 性能 | 隔离不同运行时的本地 embedding 服务，避免内存混乱。 |
| [#104739](https://github.com/openclaw/openclaw/pull/104739) | 性能 | 优化 ACP ledger 字节预算维护，将 O(events) 全表扫描降为插入时实时计算。 |
| [#104735](https://github.com/openclaw/openclaw/pull/104735) | 功能 | 在 Web UI 节点页面显示节点漂移 (drift) 和唤醒状态。 |
| [#104652](https://github.com/openclaw/openclaw/pull/104652) | 修复 | 修复设置页内容高度固定导致滚动异常的问题。 |
| [#104619](https://github.com/openclaw/openclaw/pull/104619) | 修复 | 确保 worker 启动失败详情中的 UTF-16 安全截断。 |
| [#104741](https://github.com/openclaw/openclaw/pull/104741) | 修复 | 隔离 memory-core 插件中的本地 embedding 服务生命周期。 |
| [#104750（推断，PR 未列出）] | — | 另有多个针对 unbounded file read 的安全修复 PR 被合并（详见下文 Bug 部分）。 |

**整体推进**: 项目在性能优化、UI 体验、CI 稳定性、资源隔离方面均有明确进展，同时安全加固 PR 的合入速度明显加快。

---

## 社区热点

以下 Issue / PR 在过去 24 小时内获得最高评论和社区关注：

1. **#75 – Linux/Windows Clawdbot Apps**  
   [链接](https://github.com/openclaw/openclaw/issues/75)  
   **评论**: 110 | **点赞**: 81  
   长期悬而未决的功能请求，社区对桌面客户端扩展的呼声极高。超过 200 天未解决，标签包含 `needs-product-decision`。

2. **#88838 – Track core session/transcript SQLite migration**  
   [链接](https://github.com/openclaw/openclaw/issues/88838)  
   **评论**: 37 | **点赞**: 3  
   核心存储迁移方案讨论，涉及 SQLite 翻转线，已有实施 PR #96625。

3. **#99241 – 工具输出有时变成图片附件不可读**  
   [链接](https://github.com/openclaw/openclaw/issues/99241)  
   **评论**: 21 | **点赞**: 2  
   严重 UX 问题：ANSI 长输出被替换为 `(see attached image)` 占位符，导致 agent 无法读取 stdout/stderr。

4. **#7707 – Memory Trust Tagging by Source**  
   [链接](https://github.com/openclaw/openclaw/issues/7707)  
   **评论**: 17 | **点赞**: 0  
   用户强烈希望按来源标记记忆信任等级，防范记忆投毒攻击。

5. **#102175 – 嵌入式 prompt cache 跨边界失效**  
   [链接](https://github.com/openclaw/openclaw/issues/102175)  
   **评论**: 16 | **点赞**: 1  
   回归 bug，影响长会话的 prompt 缓存连续性。

**社区诉求分析**: 用户最关心的是**可靠性**（输出丢失、会话状态损坏）和**安全**（凭证泄露、记忆污染、文件系统越权）。跨平台桌面客户端需求虽长期存在但进展缓慢。

---

## Bug 与稳定性

### 严重等级排列（从高到低）

| Issue | 等级 | 类型 | 摘要 | 修复 PR |
|-------|------|------|------|---------|
| [#104721](https://github.com/openclaw/openclaw/issues/104721) | **P0** | 回归 | 所有工具结果返回 `"(see attached image)"` 字面字符串而非实际输出，完全破坏工具使用。 | 暂无 |
| [#99241](https://github.com/openclaw/openclaw/issues/99241) | **P1** | 回归 | 工具输出在长 / ANSI 场景下变为图片占位符，agent 无法读取。 | 暂无 |
| [#84903](https://github.com/openclaw/openclaw/issues/84903) | **P1** | 孤立性 | 单个卡住的 session 阻塞整个 Gateway 事件循环，导致全网关不可用。 | 暂无 |
| [#87109](https://github.com/openclaw/openclaw/issues/87109) | **P1** | 内存 | macOS 空闲时 heap 增长至 1073MB+，cron 任务静默失败。 | 暂无 |
| [#55334](https://github.com/openclaw/openclaw/issues/55334) | **P1** | 内存 | `sessions.json` 无限增长导致 Gateway OOM（skillsSnapshot 重复）。 | 暂无 |
| [#102175](https://github.com/openclaw/openclaw/issues/102175) | **P2** | 回归 | 嵌入式 prompt 缓存跨 room_event / policy 边界失效。 | 暂无 |
| [#90213](https://github.com/openclaw/openclaw/issues/90213) | **P2** | 回归 | 更新到 2026.6.1 后遗留状态迁移警告无法消除。 | 暂无 |
| [#94846](https://github.com/openclaw/openclaw/issues/94846) | **P2** | 行为 | Cron 孤立 agentTurn 在恢复早期工具错误后误判为致命，跳过最终投递。 | 暂无 |
| [#102400](https://github.com/openclaw/openclaw/issues/102400) | **P1** | 竞态 | 回复会话初始化冲突在 Slack/Webchat 上静默丢弃消息（Telegram 已处理）。 | [#103562](https://github.com/openclaw/openclaw/pull/103562) (open) |
| [#98976](https://github.com/openclaw/openclaw/issues/98976) | **P2** | 功能缺失 | Provider refusal（Anthropic / OpenAI）不触发 fallback 链，直接失败。 | 暂无 |
| [#86996](https://github.com/openclaw/openclaw/issues/86996) | **P1** | 性能 | Active Memory + Codex 路径导致长延迟、hook 超时、启动中止。 | 暂无 |

**观察**: 多个 P0/P1 回归（#104721、#99241、#84903）直接影响核心功能，但尚无公开 fix PR。社区对内存泄漏和 session 隔离的抱怨持续升温。

---

## 功能请求与路线图信号

### 今日活跃的高票功能请求

| Issue | 标题 | 热度 | 是否可能纳入下一版本 |
|-------|------|------|----------------------|
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | 掩码 Secret 防止 agent 看到原始 API Key | 👍 4 | 可能，已有多个安全相关 PR 合并（如文件读取边界），且与 v2026.7.1-beta.5 的掩码凭据提示一致。 |
| [#6615](https://github.com/openclaw/openclaw/issues/6615) | Exec-approvals 增加拒绝列表支持 | 👍 7 | 中，社区呼声高但尚未看到对应实施 PR。 |
| [#7722](https://github.com/openclaw/openclaw/issues/7722) | 文件系统沙箱配置 `tools.fileAccess` | 👍 4 | 可能，安全加固是当前重点。 |
| [#42026](https://github.com/openclaw/openclaw/issues/42026) | 分布式 Agent Runtime（分离控制平面与计算） | 👍 3 | 低，属于重大架构改动，短期内不会实现。 |
| [#9986](https://github.com/openclaw/openclaw/issues/9986) | 上下文超限时触发模型 fallback | 👍 0 | 可能与 #98976 的 refusal fallback 一并考虑。 |
| [#8355](https://github.com/openclaw/openclaw/issues/8355) | 流式 TTS 管线（句子级） | 👍 2 | 低，语音通话功能优先级不高。 |
| [#7524](https://github.com/openclaw/openclaw/issues/7524) | groupScope 选项将群聊会话合并到主会话 | 👍 4 | 中，已有部分讨论和 linked PR。 |

**路线图信号**: 安全与隐私功能（secret masking、沙箱、信任标签）是社区强烈需求的共同方向，且与当前修复 PR 趋势吻合。架构级功能（分布式运行时、MCP Apps）则处于早期探索阶段。

---

## 用户反馈摘要

从 Issues 评论中提炼的典型用户声音：

- **工具输出丢失**（#104721）: 用户 @dennisd-hub 直接批评：“This is completely broken — the actual data is being replaced with a placeholder string”。该 bug 属于回归，严重影响所有使用工具的 workflow。
- **内存泄漏**（#87109）: 用户描述 Gateway 在 macOS 上空闲时 heap 从 558MB 涨到 1073MB+，cron 任务“静默失败——无输出、无推送、无错误上报”。对维护多个 agent 的用户打击很大。
- **安装困难**（#76042）: 用户抱怨自 2026.5.xx 以来新版本无法正常安装，等待时间过长。这提示 onboarding 流程可能存在网络或状态迁移问题。
- **多 agent 群聊歧义**（#43750）: 用户指出在 Discord 多 agent 频道中 `/new` 和 `/reset` 命令无法定向到特定 agent，所有 agent 都会响应，造成混乱。
- **谷歌聊天 replyToMode 无效**（#42510）: 用户反馈即使设置 `replyToMode: "off"`，消息仍然强制回复到线程，与文档不符。
- **Webhook 会话不支持多轮**（#11665）: 用户指出文档声称 `sessionKey` 可保持多轮对话，但实际上每次调用都创建新 session。

**正面反馈**: 无明显正面反馈出现在今日数据中，说明用户主要集中在报告问题和请求功能上。

---

## 待处理积压

以下为长期未响应或被标记 `needs-maintainer-review` / `needs-product-decision` 的重要问题，提醒维护者关注：

| Issue | 创建时间 | 标签 | 为何重要 |
|-------|----------|------|----------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | 2026-01-01 | enhancement, help wanted, P2 | 110 评论，81 👍 的 Linux/Windows 客户端请求，超过 200 天无实质进展。 |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | 2026-02-03 | P2, security | 记忆信任标签功能，多次被提及但无产品决策。 |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | 2026-02-06 | P1, security | 密钥掩码，直接关系凭证安全。 |
| [#6615](https://github.com/openclaw/openclaw/issues/6615) | 2026-02-01 | P2, security | Exec-approvals 拒绝列表，用户期望灵活策略。 |
| [#42026](https://github.com/openclaw/openclaw/issues/42026) | 2026-03-10 | P2 | 分布式运行时架构 RFC，虽为长期目标但需社区共识。 |
| [#86996](https://github.com/openclaw/openclaw/issues/86996) | 2026-05-26 | P1 | Active Memory + Codex 路径的严重性能问题，影响 Telegram 等简单消息。 |
| [#104721](https://github.com/openclaw/openclaw/issues/104721) | 2026-07-11 | P0, regression | 最新回归，无任何 fix PR，属于最高优先级的阻断问题。 |
| [#99241](https://github.com/openclaw/openclaw/issues/99241) | 2026-07-02 | P1 | 工具

---

## 横向生态对比

好的，作为AI智能体与个人AI助手领域的资深技术分析师，我已基于您提供的六个开源项目（OpenClaw、Hermes Agent、OpenHands SDK、Pi、LiteLLM、Temporal）的日报，为您生成一份横向对比分析报告。

---

### **2026年7月12日 AI智能体/个人助手开源生态横向对比分析报告**

#### **1. 生态全景**

当前，个人AI助手与自主智能体开源生态正处于 **“功能深化与稳定性博弈”** 的关键阶段。一方面，围绕 **GPT-5.6** 等前沿模型的适配与集成成为社区最热话题，驱动着项目快速迭代；另一方面，随着用户基数增长和用例深入，**内存泄漏、会话隔离失败、配置持久化异常**等稳定性问题开始集中暴露，成为制约用户体验提升的主要瓶颈。安全层面，从**凭证掩码到文件系统沙箱**，再到**SSRF漏洞修复**，各项目已普遍将安全加固作为核心任务，标志生态正从“功能可用”向“生产可靠”迈进。

#### **2. 各项目活跃度对比**

| 项目名称 | 核心定位 | 今日Issues更新 | 今日PR更新 | 今日版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 全能型个人AI助手平台 | 412 (高) | 500 (极高) | ✅ v2026.7.1-beta.5 | **高危活跃** - 迭代极快，但P0/P1回归Bug积压严重，稳定性风险高 |
| **Hermes Agent** | 通用Agent框架/网关 | 237 (高) | 500 (极高) | ❌ 无 | **高活跃** - 问题修复积极，但PR合并率极低（4.2%），存在较大积压风险 |
| **OpenHands SDK** | 软件Agent开发SDK | 15 (中) | 22 (中) | ❌ 无 | **健康** - 维护与前瞻探索并行，Bug响应快，社区讨论聚焦于前沿技术 |
| **Pi** | 高性能TUI/CLI Agent | 44 (高) | 16 (中) | ❌ 无 | **极健康** - 问题快速响应与修复，强烈关注前沿模型，社区反馈闭环高效 |
| **LiteLLM** | LLM统一代理/网关 | 33 (高) | 179 (高) | ✅ v1.91.2 | **健康** - 安全加固与成本精准化是亮点，但存在SSRF等严重安全漏洞待解决 |
| **Temporal** | 分布式工作流引擎 | 5 (低) | 4 (低) | ❌ 无 | **稳健** - 核心架构升级（CHASM/Nexus）稳步推进，社区关注高负载下的长期问题 |

#### **3. OpenClaw 在生态中的定位**

- **优势与差异化**：OpenClaw 是当前生态中**功能最全、社区最活跃**的“全能型”个人AI助手平台。其技术路线强调**终端用户开放性与深度集成**，通过 `v2026.7.1-beta.5` 中的对话式引导，试图降低新用户门槛。它在**多Agent群聊、Webhook会话、跨平台客户端**等方面的功能广度，是 Hermes 或 Pi 无法比拟的。
- **技术路线差异**：与 Hermes 的“网关/框架”定位和 LiteLLM 的“代理/路由”定位不同，OpenClaw 更倾向于构建一个**完整的、本地优先的AI操作系统**，其功能覆盖了会话管理、记忆、工具调用和工作流调度。
- **社区规模对比**：从 Issue/PR 数量级（单日数百条）看，OpenClaw 的社区**活跃度远高于**其他所有项目，表明其开发者基数和用户群体极为庞大。但这也带来了 **“高噪音”和“核心Bug被淹没”** 的风险，如 #104721 这类P0回归尚无修复PR，与其高活跃度形成反差。
- **潜在风险**：其**功能请求长期积压**（如 #75 桌面客户端请求已超200天），以及**内存泄漏** (#87109) 和**会话阻塞** (#84903) 等核心稳定性问题的持续存在，可能开始侵蚀社区信任。

#### **4. 共同关注的技术方向**

- **会话状态管理与可靠性**：**涉及项目**：OpenClaw、Hermes Agent、Pi。**具体诉求**：修复会话隔离失败导致的阻塞、会话状态迁移错误（Hermes #27038）、以及Prompt缓存跨边界失效（OpenClaw #102175）。这指向了**多会话、多场景下状态管理的健壮性**是通用痛点。
- **Provider集成与适配**：**涉及项目**：Pi、Hermes Agent、LiteLLM。**具体诉求**：快速适配新模型（如Pi对GPT-5.6全系列的支持）、修复与特定Provider（如Bedrock、Codex、Dashscope）的兼容性Bug。这表明项目对**模型多样性**的承诺至关重要。
- **配置持久化与一致性**：**涉及项目**：OpenHands SDK、LiteLLM、Hermes Agent。**具体诉求**：服务重启后配置（如超时、Provider凭证）不丢失、序列化后反序列化信息不损失。这要求项目在设计上强化**配置即代码**和**状态可恢复**的能力。
- **安全加固**：**涉及项目**：OpenClaw、LiteLLM、OpenHands SDK。**具体诉求**：限制文件读取容量（OpenClaw）、修复Guardrail SSRF漏洞（LiteLLM）、防止凭证泄露（OpenClaw #10659）、提供Secret掩码能力。**这是一个高优先级且有明确PR支撑的显性趋势。**
- **成本与计费精准化**：**涉及项目**：OpenClaw（ACP ledger）、LiteLLM。**具体诉求**：修复成本计算遗漏（如LiteLLM Fireworks/Dashscope）、提供更精确的Token和费用追踪。**可观测性**正在从功能监控向**财务运营**延伸。
- **用户体验优化**：**涉及项目**：OpenClaw、Hermes Agent、Pi。**具体诉求**：TUI兼容性（Pi Windows Terminal）、Telegram输入指示器卡死（Hermes）、UI滚动/布局Bug（OpenClaw）。这表明**交互细节**已成为区分项目成熟度的关键指标。

#### **5. 差异化定位分析**

- **功能侧重**：**Pi** 和 **Hermes** 聚焦于 **“核心Agent交互”**（TUI/CLI），强调极致性能和前沿模型适配；**OpenClaw** 提供 **“全栈应用”** （Web/CLI/Desktop），功能最庞杂；**LiteLLM** 和 **OpenHands SDK** 定位为 **“基础设施”** ，前者是路由网关，后者是开发工具包；**Temporal** 则是 **“工作流引擎”** ，定位最为底层。
- **目标用户**：**Pi** 和 **Hermes** 面向**开发者/技术用户**；**OpenClaw** 试图同时覆盖**普通用户和开发者**，难度最高；**LiteLLM** 面向**运维和平台团队**；**OpenHands SDK** 面向**Agent开发者**；**Temporal** 面向**后端/分布式系统开发者**。
- **技术架构**：**Pi** 追求**极简依赖和快速启动**；**OpenClaw** 和 **Hermes** 具有**复杂的插件/扩展系统**；**LiteLLM** 是典型的**代理/网关架构**；**Temporal** 是经典的**服务端-工作者架构**。架构的复杂度直接影响其面临的问题域（如OpenClaw P0回归多）。

#### **6. 社区热度与成熟度**

- **快速迭代与问题暴露期（高活跃，低稳定性）**：
    - **OpenClaw**：此阶段的典型代表。功能更新快，社区声量大，但Bug频出，P0/P1问题堆积，是其在追求广度时必然付出的代价。
    - **Hermes Agent**：同样处于此阶段。极高的PR提交量反映了活跃的开发，但极低的合并率暗示了**审查瓶颈或大量探索性/未成熟工作**，这是项目高速发展但管理未跟上的信号。
- **质量巩固与功能增强期（高活跃，高稳定性）**：
    - **Pi**：此阶段的明星项目。Bug响应速度极快（Bedrock回归数小时修复），社区反馈闭环出色，同时能迅速跟进GPT-5.6等前沿技术，显示了团队的高效和聚焦。
    - **LiteLLM**：介于两者之间。在快速修复成本、安全等关键问题的同时，也在推出v1.91.2的镜像签名等成熟度功能，体现了稳定与功能的平衡。
- **稳健发展期（低活跃，高稳定性）**：
    - **Temporal**：作为成熟的分布式基础设施，其Issue和PR数量保持在低位，核心开发聚焦于CHASM等架构级升级，社区主要关注PostgreSQL膨胀等长期运维问题，说明项目已进入稳定维护和演进阶段。
    - **OpenHands SDK**：活跃度相对较低，但社区讨论质量高，关注前沿集成（GPT-5.6）和安全工具（AST解析），属于平稳发展中的前瞻探索。

#### **7. 值得关注的趋势信号**

1.  **MCP (Model Context Protocol) 成为通用集成标准**：LiteLLM 和 OpenClaw 都在大力推进MCP相关功能（如OAuth委托、技能注入），这表明**标准化Agent扩展协议**正从概念走向实践，对开发者而言，拥抱MCP将是降低集成成本的关键。
2.  **Agent安全从“附加功能”变为“系统核心”**：OpenClaw 的Secret掩码、LiteLLM 的SSRF修复、OpenHands SDK 的AST安全分析器，表明**安全已不再是事后考虑，而是与功能开发并行的一等公民**。这预示着未来的Agent框架将内置更多安全原语。
3.  **成本管控成为可观测性的新维度**：LiteLLM 的精准计费Bug修复和OpenClaw的ACP ledger优化，表明**对AI服务的财务可见性**正成为平台必备能力。开发者需关注所选用项目是否提供了细粒度的成本追踪和预算管控机制。
4.  **“会话”作为核心抽象的重要性凸显**：从OpenClaw的会话隔离失败到Hermes的会话状态迁移错误，再到Pi的Compaction问题，都指向**会话生命周期管理的复杂性**。一个健壮的会话模型（能处理重置、恢复、迁移、过期）将是判断Agent框架成熟度的分水岭。
5.  **GPT-5.6效应：快速迭代与兼容性挑战**：Pi 和 Hermes 社区对GPT-5.6集成的狂热，表明**新模型的冲击会立即在开源社区引发适配浪潮**，同时也会暴露大量兼容性问题（如Pi的Compaction 404）。AI Agent开发者需做好持续应对“模型API变更”的准备。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，这是我根据您提供的 Hermes Agent 项目数据生成的 2026-07-12 项目动态日报。

---

# Hermes Agent 项目动态日报 | 2026年7月12日

## 1. 今日速览

Hermes Agent 项目今日呈现出极高的社区活跃度，过去 24 小时内产生了 237 条 Issue 和 500 条 PR 更新，表明开发与讨论非常热烈。**活跃度评级：★★★★★ (极度活跃)**。

尽管 PR 提交量巨大（500条），但合并率偏低（仅 21 条，约 4.2%），这暗示了项目可能正在进行大规模的重构、功能迭代或面临代码审查瓶颈。Issues 方面，社区积极响应项目动态，关闭了 67 个问题，清理效率尚可，但仍有大量（170 个）新问题涌现。当前项目有大量 PR 处于待合并状态（479条），这是一个需要关注的健康度信号，可能预示着积压风险。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

昨日没有 PR 被合并到主分支，但大量开放的 PR 展示了项目正在积极推进以下方向。这些 PR 处于待合并状态，一旦合并将显著提升项目稳定性和功能完整性：

- **稳定性与Bug修复**：大量 PR 聚焦于修复核心组件中的并发问题、资源泄露和边界情况。
    - `fix(email): skip startup UID backlog after trim` (#60677) 修复了邮件网关在启动时可能重放旧邮件的边缘情况。
    - `fix(compression): prevent lock TTL=0 from being swallowed` (#60665) 修复了上下文压缩锁的一个逻辑错误。
    - `fix(guardrails): prevent same-tool failure counter bypass` (#60661) 修复了工具调用护栏机制的绕过漏洞。
    - `fix(anthropic): serialize Claude Code OAuth refresh under auth lock` (#60639) 修复了 Anthropic OAuth 刷新时的竞态条件。
- **功能增强**：数个 PR 为桌面客户端和核心系统引入了新能力。
    - `feat(desktop): Cost Tracker` (#60673) 桌面客户端新增成本追踪功能，可与 `/status` 集成。
    - `feat(desktop): add Aurora theme` (#60649) 和 `feat(desktop): add Italian locale` (#60640) 丰富了桌面客户端的主题和国际化支持。
    - `feat(compression): configurable max_tail_message_floor` (#60662) 使用户能够自定义上下文压缩的行为，提供更精细的控制。
- **配置与安全**：
    - `feat: add config-pinned exact-once external approval (NLS-184)` (#62778) 为无人值守的终端命令引入了配置驱动的外部审批桥接，增强了安全性。
    - `fix(model): make picker discovery config-aware` (#60656) 改进了模型选择器的逻辑，使其能更智能地识别可用的自定义模型。

尽管这些 PR 尚未合并，但它们清晰地指明了项目在 Bug 修复、体验优化、功能扩展和安全加固方面的前进方向。

## 4. 社区热点

今日讨论热度最高的议题反映了用户在集成服务、用户体验细节和API一致性方面的强烈诉求。

- **`[Feature: native Google Cloud Vertex AI provider support]`** (#13484)
    - **评论数：12 | 👍 数：14**
    - **链接：** [https://github.com/NousResearch/hermes-agent/issues/13484](https://github.com/NousResearch/hermes-agent/issues/13484)
    - **分析：** 该 Issue 获得了最高的 14 个赞和 12 条评论，是社区呼声最高的功能请求。用户 `@prasadus92` 精确指出了现有 `google-vertex` 占位符与缺少的认证机制（短时效 OAuth Token）之间的差距，这表明用户对与 Google Cloud 生态的深度集成有真实且迫切的需求。

- **`[bug: Codex Responses API rejects replayed assistant message items with long id fields]`** (#27038)
    - **评论数：10**
    - **链接：** [https://github.com/NousResearch/hermes-agent/issues/27038](https://github.com/NousResearch/hermes-agent/issues/27038)
    - **分析：** 该问题（已关闭）探讨了与 OpenAI Codex API 的兼容性问题，当恢复长会话时，由于 `id` 字段过长，导致 API 拒绝请求。这反映了用户在高频使用场景下的痛点，并指向了一个关键的会话状态管理挑战。该 Bug 被标记为 P1 优先级，说明维护者也认为其影响严重。

- **`[Bug: Telegram typing indicator stuck indefinitely after response (_keep_typing race condition)]`** (#28004)
    - **评论数：9**
    - **链接：** [https://github.com/NousResearch/hermes-agent/issues/28004](https://github.com/NousResearch/hermes-agent/issues/28004)
    - **分析：** 这是一个典型的用户体验 Bug。`@WegoW` 不仅报告了问题，还进行了根因分析（`_keep_typing` 中的竞态条件），这有助于开发者快速定位和修复。该问题的热度说明了即时通讯平台（Telegram）作为主要使用界面时，小细节的稳定性对用户体验至关重要。

## 5. Bug 与稳定性

昨日报告的 Bug 主要集中在会话状态管理、跨 Provider 的兼容性和配置持久化问题上，按严重程度排列如下：

- **P1 (严重)**
    - `[CLOSED] bug: Codex Responses API rejects replayed assistant message items...` (#27038): 高优Bug，已关闭，预计已修复。
    - `[Bug]: xAI OAuth fallback after provider switch due to stale encrypted_content...` (#32617): 记录 Provider 切换导致 OAuth 回退和请求失败。已关闭。
    - `[Bug]: Stale credential pool entries cause removed providers to persist in model picker` (#55790): 删除 Provider 后仍在模型选择器中显示。已关闭。
- **P2 (中等)**
    - `[Bug]: Telegram typing indicator stuck indefinitely...` (#28004): 影响用户体验的竞态条件。开放中，已有根因分析。
    - `[Bug]: Hermes sends extremely large prompts to local OpenAI-compatible models...` (#61265): 导致本地模型数分钟卡顿，严重影响使用体验。开放中。
    - `[Bug]: GLM-5.2 context_length falls back to 200K...` (#47970): 模型上下文窗口识别错误，导致过早压缩。开放中。
    - `[Bug]: /model switch from Telegram persists stale base_url → 404...` (#56158): 切换模型后遗留错误的 `base_url`，导致API 404错误。开放中。
    - `[Bug]: Desktop model switch leaves stale base_url in config.yaml...` (#46759): 桌面端切换模型遗留配置。已关闭。
- **P3 (较低)**
    - `[Bug]: Memory and MCP prompt-injection scanners miss multi-word...` (#27284): 安全隐患，但触发条件复杂。开放中。
    - `[Bug]: Outbound/fresh emails have no way to set a subject...` (#46947): 邮件发送功能缺陷。开放中。

**总结：** 项目在 P1/P2 级别的 Bug 修复上较为积极（多个已关闭）。当前最突出的问题是：本地模型发送超大 Prompt (#61265)、Telegram 打字指示器问题 (#28004) 以及多个模型/Provider 切换时遗留的配置污染 Bug。好在已有多个 PR（如 #60656, #60665 等）在进行相关修复。

## 6. 功能请求与路线图信号

社区提出的新功能需求日益多样化，部分已有 PR 匹配，预示着这些功能可能很快被纳入主线。

- **高优先级呼声：**
    - **原生 Google Cloud Vertex AI 支持** (#13484): 呼声最高，虽然暂无对应 PR，但鉴于其高赞数，很可能是下个版本的路线图重点。
- **已有对应 PR 的高概率功能：**
    - **桌面客户端功能增强**：社区提出的 `Cost Tracker`、`Aurora 主题`、`中文 (zh-Hans) 本地化` (#61526, 已关闭, 标记为已实现) 在 PR 中均有对应实现（#60673, #60649, #61526）。
    - **提升会话可见性**：`graceful session resume / reset-awareness` (#43008) 提议让用户感知到会话被重置，这与项目正在关注的 `session-state` 问题域高度吻合，有望在未来版本中获得处理。
    - **Cursor Agent SDK 集成** (#30640): 社区对与 Cursor 等主流编码工具的深度集成兴趣浓厚（评论5），需要关注其未来的优先度。
- **路线图信号：**
    - **生产部署安全**：PR #60636 (`Harden Hermes for production deployment`) 和 #62778 (`config-pinned exact-once external approval`) 暗示开发者正在积极为 Hermes 在企业级或生产环境中的部署做准备，这将是项目走向成熟的关键一步。

## 7. 用户反馈摘要

从今日的 Issues 中，可以清晰地提炼出用户的真实体验反馈：

- **痛点反馈：**
    - `@anthonydigrazia` 在 #61265 中抱怨：“Hermes sends extremely large prompts... causing multi-minute stalls”，直指核心性能问题，严重影响使用本地模型的体验。
    - `@WegoW` 在 #28004 中对 Telegram 上“常驻的 typing 指示器”表达了挫败感，这是非常具体的交互体验痛点。
    - `@vincentee91g` 在 #46947 中提出邮件主题无法自定义，限制了自动化场景，是功能性上的缺失。
- **使用场景描述：**
    - `@crayfish-ai` 在 #62595 中详细描述了在 Feishu、Telegram 等多话题会话中，当前上下文压缩可能混合话题的问题，并提出了 `topic-aware compaction` 的解决方案。这表明用户正将 Hermes 用于复杂、持续的沟通场景。
    - `@DavidMetcalfe` 在 #55790 中描述了通过桌面UI管理多个 Provider Key 的场景，并发现了删除 Provider 后遗留状态的问题，这指向了多 Provider 管理功能的复杂性。

**整体来看，用户对 Hermes Agent 充满期待，并积极将其用于多种复杂场景。但项目在高负载稳定性、跨平台交互细节和配置一致性方面仍有待打磨。**

## 8. 待处理积压

以下是一些需要特别关注的长期未解决或正处于关键状态的重要 Issue/PR：

- **高关注度的开放功能请求：**
    - `#13484` **Feature: native Google Cloud Vertex AI provider support**: 社区反响最强烈，但尚无维护者明确回复或关联 PR。需要官方回应其路线图安排。
- **关键 Bug 待修复：**
    - `#61265` **Bug: Hermes sends extremely large prompts...**: 严重影响本地模型用户，评论数高，但尚未有明确解决路径。
    - `#28004` **Telegram typing indicator stuck...**: 影响面广（Telegram 用户基数大），已有根因分析，但 fix 未出现。
- **配置/兼容性长期问题：**
    - `#17199` **deepseek provider: model normalization and base_url override break custom endpoints**: 长期存在的配置兼容性问题（4月底提出），影响用户使用自定义后端，至今仍为 OPEN 状态。
    - `#52496` **Dashboard /api/model/set rewrites named custom provider...**: 与桌面端 Dashboard 模型选择相关的配置问题，同样是配置持久化的积病。

**建议：** 项目维护者应优先关注 `#13484` 给出官方回应，并对 `#61265` 和 `#28004` 这两个严重影响用户体验的 P2 Bug 安排修复资源。同时，需要审查 `#17199` 这类长期未解决的配置积压问题，以提升项目的稳定性口碑。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 OpenHands SDK 项目数据，我已为您生成了 2026 年 7 月 12 日的项目动态日报。

---

## OpenHands SDK 项目日报 (2026-07-12)

### 1. 今日速览

今日项目活跃度较高，共收到 15 条 Issue 更新和 22 条 PR 更新。社区讨论主要集中在修复已发现的中高优先级 Bug，例如 LLM 配置文件超时重置、以及订阅制 LLM 的持久化问题。同时，社区贡献者围绕 GPT-5.6 的新特性（如多智能体、WebSocket 模式）进行了初步的技术调研，标志着项目正在积极探索前沿大模型集成。值得注意的是，一个旨在提升项目安全性的 AST 解析工具（PR #3944）正在推进中。总体而言，项目处于 **“积极维护与前瞻性探索并存”** 的高健康度状态。

### 2. 版本发布

今日无新版本发布。

### 3. 项目进展

今日合并/关闭了 2 个 PR，主要集中在关键的 Bug 修复和基础设施优化上：
- **[修复] ACP 提示参数顺序问题** - [PR #3996](https://github.com/OpenHands/software-agent-sdk/pull/3996) 已关闭。该 PR 通过使用关键字参数调用 `conn.prompt(...)`，修复了因客户端版本参数顺序变化导致的潜在错误，增强了与 ACP 协议的兼容性。对应的 Issue #4061 也同步关闭。
- **[发布] v1.35.0 版本准备** - [PR #4070](https://github.com/OpenHands/software-agent-sdk/pull/4070) 已合并。该 PR 为发布 v1.35.0 版本做准备，表明项目正在进行一个常规的版本迭代，尽管今日最终版尚未发布。

此外，有多个重要的 PR 仍在活跃推进中，表明项目功能在不断演进：
- **[新功能] 安全分析器** - [PR #2911](https://github.com/OpenHands/software-agent-sdk/pull/2911) “添加 ToolShieldLLMSecurityAnalyzer” 仍在审查中，表明安全领域的能力是项目的长期关注点。
- **[新功能] 智能模型路由器** - [PR #3744](https://github.com/OpenHands/software-agent-sdk/pull/3744) “Intelligent model router” 仍在活跃开发，旨在为不同任务智能选择最优 LLM。
- **[新功能] Shell 命令解析安全** - [PR #3944](https://github.com/OpenHands/software-agent-sdk/pull/3944) “AST-backed shell command-name resolution” 正在进行，旨在通过语法分析增强 Shell 命令的安全性。

### 4. 社区热点

今日讨论最活跃的议题反映了社区对 **新功能 Bug 和新模型集成** 的高度关注：

- **最活跃 Issue：关于 LLM 超时重置的 Bug** - [Issue #4032](https://github.com/OpenHands/software-agent-sdk/pull/4032)
    - 作者 `@kripper` 报告了一个关于 LLM 配置超时在 Agent 服务器重启后重置为默认值的问题。该问题获得了 2 条评论，表明用户对配置持久化的稳定性和可靠性非常在意。此 Bug 若影响广泛，可能导致生产环境频繁出现超时错误。
- **前沿技术探索热潮**：用户 `@smolpaws` 在今日集中提交了 4 个与 OpenAI GPT-5.6 新功能相关的 Issue，包括：
    - [Issue #4082](https://github.com/OpenHands/software-agent-sdk/issues/4082) - 程序化工具调用
    - [Issue #4083](https://github.com/OpenHands/software-agent-sdk/issues/4083) - 工具搜索/延迟加载
    - [Issue #4084](https://github.com/OpenHands/software-agent-sdk/issues/4084) - WebSocket 模式
    - [Issue #4085](https://github.com/OpenHands/software-agent-sdk/issues/4085) - 托管式多智能体 vs 客户端子智能体
    - **分析**：这一系列 Issue 表明社区中的早期采用者和开发者正在积极探索如何将 OpenAI 最新的、可能改变游戏规则的功能（如托管多智能体）集成到 OpenHands 中。这不仅是功能请求，更是对 SDK 未来架构的讨论，可能预示着 SDK 核心设计方向的重要变化。

### 5. Bug 与稳定性

今日报告了多个 Bug，主要集中在配置持久化和运行时数据完整性方面：

- **[严重] 订阅 LLM 反序列化后运行时信息丢失** - [Issue #4091](https://github.com/OpenHands/software-agent-sdk/issues/4091)
    - **摘要**：用户 `@lufen` 报告，当序列化的订阅制 ChatGPT LLM 配置（如 OAuth 凭证、base_url）被重新加载时，运行时必须的传输信息（如凭证、URL、请求头）会丢失，导致服务无法正常工作。
    - **状态**：**已有修复 PR**。作者本人已提交了 [PR #4092](https://github.com/OpenHands/software-agent-sdk/pull/4092) 来解决此问题，这是一个非常积极的信号。
- **[中] LLM Profile 超时配置在服务重启后重置** - [Issue #4032](https://github.com/OpenHands/software-agent-sdk/issues/4032)
    - **摘要**：用户 `@kripper` 报告，重启 `agent-server` 后，已配置的 LLM 超时值丢失，回退到默认值。
    - **状态**：**待处理**。目前未关联到明确的修复 PR，需进一步排查。
- **[中] ACP Profiles 中技能重复注入** - [Issue #4019](https://github.com/OpenHands/software-agent-sdk/issues/4019)
    - **摘要**：用户 `@simonrosenberg` 报告，一个最近的修复导致 ACP 配置文件在加载时，总是从工作区技能和 ACP CLI 入口两次注入相同的技能。
    - **状态**：**待处理**。该 Bug 标记为 `needs-triage`，需等待维护者进一步评估。
- **[低] 生成器错误处理异常** - [Issue #3412](https://github.com/OpenHands/software-agent-sdk/issues/3412)
    - **摘要**：一个长期存在的 Bug，在对话失败时会触发一个次要的 `RuntimeError`。
    - **状态**：**待处理**。尽管有 2 个评论，但已被标记为 `Stale`，优先级中等，在积压中。

### 6. 功能请求与路线图信号

除了上述社区热点中的前沿探索，今日还有几个明确的功能请求：

- **[提升用户体验] 在对话 UI 中显示技能加载警告** - [Issue #4015](https://github.com/OpenHands/software-agent-sdk/issues/4015)
    - 用户 `@jpshackelford` 建议，当技能配置存在冲突（如 `paths:` 和 `triggers:` 同时定义）时，应在用户界面中显示警告信息，而不是默默处理。这表明社区对透明度和可观察性的要求越来越高，该功能很可能被纳入后续版本。
- **[基础设施] 添加 SDK 设置存储秘密辅助函数** - [Issue #3981](https://github.com/OpenHands/software-agent-sdk/issues/3981)
    - 此 Issue 已关闭，但所提功能非常重要。它提出了为下游应用提供 SDK 级别的秘密存储和加密导出功能，以提高安全性。由于 Issue 已经关闭，该功能可能已经或即将以其他方式实现。
- **[新功能] 支持运行范围的 LLM 请求头** - [PR #4066](https://github.com/OpenHands/software-agent-sdk/pull/4066)
    - 一个活跃的 PR，旨在允许在一次 Agent 运行期间，对所有 LLM 调用添加特定的请求头（如用于 tracing 的 ID），而无需修改全局 LLM 配置。这是一个实用性强、需求明确的功能。

### 7. 用户反馈摘要

从今日的 Issues 和 PR 评论中，可以提炼出以下用户反馈：

- **对配置持久化的强烈需求**：[Issue #4032](https://github.com/OpenHands/software-agent-sdk/issues/4032) 和 [Issue #4091](https://github.com/OpenHands/software-agent-sdk/issues/4091) 都直接反映了用户对“配置一致性”的痛点。用户期望在重启服务或使用序列化配置后，所有设定（特别是安全性相关的凭证和性能相关的超时）都能被准确、完整地还原。
- **对 MCP 模式迁移的关注**：[Issue #4052](https://github.com/OpenHands/software-agent-sdk/issues/4052) 指向了 MCP 模式迁移的修复。用户遇到现有 MCP 配置在升级后出现问题，表明模式迁移的向后兼容性需要重点保障。
- **贡献者感到满意且有信心**：[PR #4092](https://github.com/OpenHands/software-agent-sdk/pull/4092) 的作者 `@lufen` 表示“Reviewed and verified to fix the issue on my local system”， [PR #3996](https://github.com/OpenHands/software-agent-sdk/pull/3996) 的作者 `@neubig` 明确修复了问题，这体现了修复的直接有效性和贡献者信心。
- **对性能提升的积极肯定**：[PR #3895](https://github.com/OpenHands/software-agent-sdk/pull/3895) 的作者 `@jamiechicago312` 提供了一个 Youtube 链接来证明其 Lazyload 优化将应用启动时间缩短到了约 30 秒，这是一种非常直观且有说服力的正向反馈。

### 8. 待处理积压

以下是一些需要维护者特别关注的重要积压项：
- **[长期未处理] 安全分析器 PR** - [PR #2911](https://github.com/OpenHands/software-agent-sdk/pull/2911)
    - 状态：`OPEN`。创建于 2026-04-21，近 3 个月未进行实质性进展。鉴于该项目对安全性的重视，此 PR 的审查与合并应被提上日程。
- **[长期未处理] 生成器错误异常** - [Issue #3412](https://github.com/OpenHands/software-agent-sdk/issues/3412)
    - 状态：`OPEN`。虽然标记为 `priority:medium`，但该问题会“在每次对话失败时触发”，严重影响开发者体验和错误排查。该 Issue 已存在一个多月，建议维护者重新评估其优先级并给出回复或解决方案。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 GitHub 数据，我将为您生成 **Pi 项目 2026 年 7 月 12 日动态日报**。

---

## Pi 项目动态日报 | 2026-07-12

### 1. 今日速览

项目在过去 24 小时内保持了极高的活跃度，社区贡献与维护者响应均非常积极。尽管没有新版本发布，但 **44 个 Issue 和 16 个 PR 被关闭**，显示出强大的问题处理与代码合并能力。社区焦点高度集中在 **GPT-5.6 系列模型**的适配与优化上，相关讨论与 PR 占据了显著比例。同时，几个关键 Bug（如 Bedrock 认证回归、Codex WebSocket 凭证问题）已快速定位并修复，体现了项目对稳定性的重视。整体而言，项目处于健康的快速迭代阶段。

### 2. 版本发布
- **无新版本发布**

### 3. 项目进展

今日合并/关闭了多项重要 PR，显著推进了项目功能与稳定性：

- **GPT-5.6 模型支持深化**：
  - 通过 PR [#6528](https://github.com/earendil-works/pi/pull/6528) 为 GPT-5.6 系列添加了 `prompt_cache_options` 支持，以优化成本与性能。
  - 通过 PR [#6533](https://github.com/earendil-works/pi/pull/6533) 修复了使用 `openai-codex` 提供商的 GPT-5.6-luna 模型在 **Compaction** 时返回 “Model not found” 的 404 错误。
  - 通过 PR [#6544](https://github.com/earendil-works/pi/pull/6544) 修复了 GitHub Copilot 的 `mai-code-1-flash-picker` 模型因使用了错误的 API 端点而无法工作的问题。

- **关键 Bug 修复**：
  - 成功修复并合入了 PR [#6532](https://github.com/earendil-works/pi/pull/6532)，解决了由 PR [#6531](https://github.com/earendil-works/pi/issues/6531) 报告的 **Amazon Bedrock** 认证回归问题，该问题导致通过 `AWS_PROFILE` 认证失败。
  - 合并 PR [#6539](https://github.com/earendil-works/pi/pull/6539)，修复了 OpenAI-Codex 的 WebSocket 在用户凭证变更后仍保持旧连接的状态，避免了请求错乱。

- **新功能与扩展能力**：
  - 合并了实验性 PR [#6534](https://github.com/earendil-works/pi/pull/6534)，为消息系统引入了 **“开发者（developer）”消息角色**，这可能为未来的高级提示工程提供基础。
  - 通过 PR [#6518](https://github.com/earendil-works/pi/pull/6518) 向扩展系统暴露了当前会话的模型作用域 (`getScopedModels()`)，增强了扩展的上下文感知能力。
  - 合入 PR [#6540](https://github.com/earendil-works/pi/pull/6540) ，确保**提供商错误**（如上下文溢出、重试耗尽）能够通过 `advisories` 机制传递给 LLM，帮助模型更好地理解并尝试恢复。

- **基础设施与性能**：
  - PR [#6530](https://github.com/earendil-works/pi/pull/6530) 优化了 Node CLI 的**启动速度**，通过延迟加载模块，显著减少了命令执行前的等待时间。

### 4. 社区热点

今日讨论最热烈的议题几乎都与 **GPT-5.6 系列模型**有关，显示出社区对前沿模型的高度热情：

1.  **GPT-5.6 模型添加请求**：Issue [#6475](https://github.com/earendil-works/pi/issues/6475) 请求将 `gpt-5.6-sol`, `gpt-5.6-terra`, `gpt-5.6-luna` 加入 GitHub Copilot 提供商。该 Issue 获得了 **8 个赞**和 **9 条评论**，说明大量用户渴望立即使用这些新模型。该 Issue 已在当日被快速关闭。

2.  **“max”思考层级支持**：Issue [#6097](https://github.com/earendil-works/pi/issues/6097) 申请添加对 GPT-5.6 Sol 模型的第六级 `max` 思考层级的支持。以 **18 个赞**成为今日呼声最高的功能请求，用户期待 Pi 能完整支持 OpenAI 的最强模型。

3.  **Codex Compaction 故障**：Issue [#6477](https://github.com/earendil-works/pi/issues/6477) 报告使用开放式 `gpt-5.6-luna` 模型时 Compaction 功能完全失效。该问题获得了 **5 个赞**，表明它严重影响了核心工作流。随后 PR [#6533](https://github.com/earendil-works/pi/pull/6533) 被提交以修复此问题。

### 5. Bug 与稳定性

| 严重程度 | 问题描述 | Issue / PR | 状态 |
| :--- | :--- | :--- | :--- |
| **高** | **Amazon Bedrock 认证回归**：`AWS_PROFILE` 认证方式因新增的 API Key 支持而失效，导致请求 403。 | [#6531](https://github.com/earendil-works/pi/issues/6531) | **已关闭** (已修复于 [#6532](https://github.com/earendil-works/pi/pull/6532)) |
| **高** | **Codex Compaction 阻塞**：使用 `openai-codex` 的 GPT-5.6-luna 模型时，所有 Compaction 操作均因“Model not found”错误而失败。 | [#6477](https://github.com/earendil-works/pi/issues/6477) | **已关闭** (已修复于 [#6533](https://github.com/earendil-works/pi/pull/6533)) |
| **中** | **Codex WebSocket 凭证泄**：在同一个 Pi 会话中切换账户时，WebSocket 连接可能仍使用旧账户，导致请求错乱。 | [#6513](https://github.com/earendil-works/pi/issues/6513) | **已关闭** (已修复于 [#6539](https://github.com/earendil-works/pi/pull/6539)) |
| **中** | **Windows Terminal 滚动异常**：`pi-tui` 输出的 `ESC[3J` 序列导致 Windows Terminal 反复滚动到顶部。 | [#6502](https://github.com/earendil-works/pi/issues/6502) | **开放中** (未分配) |
| **中** | **Copilot MAI-Code 模型故障**：`mai-code-1-flash-picker` 模型因使用了错误的 API 端点而立即报错。 | [#6510](https://github.com/earendil-works/pi/issues/6510) | **已关闭** (已修复于 [#6544](https://github.com/earendil-works/pi/pull/6544)) |
| **中** | **Compaction 设置被绕过**：设置 `compaction.enabled: false` 无法完全禁用自动 Compaction，溢出恢复路径会强制触发它。 | [#6472](https://github.com/earendil-works/pi/issues/6472) | **已关闭** (已修复) |
| **低** | **max_tokens 负值导致 400 错误**：当上游提供商返回的上下文窗口过小时，Pi 可能发送 `max_completion_tokens: 1`，导致请求被拒绝。 | [#6522](https://github.com/earendil-works/pi/issues/6522) | **开放中** (未分配) |

### 6. 功能请求与路线图信号

- **高可能性采纳**：
  - **开发者消息角色**：PR [#6534](https://github.com/earendil-works/pi/pull/6534) 是核心维护者提交的实验性功能。通常，此类 PR 意味着该方向已被纳入内部路线图，并可能在后续版本中稳定发布。
  - **约束采样/提供商侧工具参数校验**：PR [#6341](https://github.com/earendil-works/pi/pull/6341) 作为开放中的 `[to-discuss]` PR，旨在为工具调用引入提供商侧的模式约束。如果实现，将显着提升工具调用的可靠性。

- **中等可能性采纳**：
  - **RPC 附件支持**：Issue [#6493](https://github.com/earendil-works/pi/pull/6493) 功能请求允许 RPC `prompt` 命令携带附件（如音频文件）。此项多为扩展开发者所需，取决于社区优先级与实现复杂度。
  - **扩展系统请求 Reload**：PR [#6551](https://github.com/earendil-works/pi/pull/6551) 和 Issue [#6552](https://github.com/earendil-works/pi/issues/6552) 均提出了类似概念，即为扩展提供请求宿主重载的能力。这可能会在下一版本中作为扩展 API 的一部分被考虑。

### 7. 用户反馈摘要

- **痛点**：
  - **扩展开发体验**：有用户反映 `import typebox/schema` 失败导致扩展无法加载（[#6512](https://github.com/earendil-works/pi/issues/6512)），暴露了扩展开发环境配置的潜在问题。
  - **配置覆盖与持久化**：用户抱怨 CLI 的 `-t` 和 `--system-prompt` 选项在会话恢复时不会生效（[#6498](https://github.com/earendil-works/pi/issues/6498)），需要重新设置，这打断了工作流。
  - **UI/UX 习惯冲突**：多位从 Codex 或 Claude 等工具迁移过来的用户提到，`Ctrl+P` 快捷键在 Pi 中用于切换模型而非回显上一条输入（[#6456](https://github.com/earendil-works/pi/issues/6456)），需要一定的适应成本。

- **满意点**：
  - **快速响应**：多个严重程度高的 Bug（如 Bedrock 回归、Codex Compaction 失败）在报告后数小时内即被修复，用户能感受到社区的高效与响应速度。
  - **紧跟前沿**：用户对于 GPT-5.6 系列模型的支持呼声极高，而项目维护者迅速应对，从添加模型到修复相关 bug，体现了项目对最新技术趋势的积极跟进。

### 8. 待处理积压

- **长期未响应问题**：
  - **Llama.cpp 超时问题**：Issue [#5294](https://github.com/earendil-works/pi/issues/5294)（创建于 6 月 1 日）报告了与 `llama.cpp` 后端的超时问题，尽管用户已配置 `http timeout = false`。此问题长期未解决，项目可能需要明确是 `llama.cpp` 的特性还是 Pi 的 Bug，并给出回复或临时解决方案。

- **重要开放议题**：
  - **OpenRouter Provider 扩展**：Issue [#5916](https://github.com/earendil-works/pi/issues/5916) 是关于支持 provider 扩展和模型别名的核心功能请求，已开放近一个月，讨论热烈（12 条评论）。这反映了高级用户对于更灵活配置 provider 的强烈需求。
  - **Windows Terminal 兼容性**：Issue [#6502](https://github.com/earendil-works/pi/issues/6502) 尚未被分配，但影响 Windows 用户的 TUI 体验。建议尽快响应和修复。
  - **平台不匹配导致请求失败**：Issue [#6522](https://github.com/earendil-works/pi/issues/6522) 报告了当使用代理时，由于上下文窗口估算错误导致请求被拒的边界情况。这属于稳定性问题，应评估其普遍性并考虑修复。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 (2026-07-12)

---

## 1. 今日速览

过去24小时LiteLLM项目保持高活跃度：**33条Issues**更新（新开/活跃25条，已关闭8条），**179条PR**更新（待合并101条，已合并/关闭78条）。发布新版本 **v1.91.2**，重点强化Docker镜像签名验证。社区讨论集中在 **SSRF安全漏洞**、**自定义日志回调失效**、**成本计算偏差** 等关键问题上。多个重要Bug修复PR（如Fireworks AI缓存计费、Dashscope预算绕过）已提交或合并，项目在稳定性和安全性方面稳步推进。

---

## 2. 版本发布

### v1.91.2 (2026-07-11)
- **更新内容**：所有LiteLLM Docker镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 进行签名，每次发布使用同一密钥（从commit `0112e53` 引入）。用户可通过cosign命令验证镜像签名。
- **破坏性变更**：无。
- **迁移注意事项**：建议所有使用Docker部署的用户更新签名验证流程，确保镜像完整性。
- **后续计划**：已存在 **PR #32948** 准备将两个已合并的修复（#32542、#32655）backport到 `stable/1.91.x` 分支并发布 **v1.91.3**，修复Responses-API guardrail内容绕过等问题。

> 链接：https://github.com/BerriAI/litellm/releases/tag/v1.91.2

---

## 3. 项目进展

今日合并/关闭了 **78条PR**，以下为关键进展：

### ✅ 已合并/关闭的重要PR
| PR | 描述 | 影响 |
|----|------|------|
| [#31760](https://github.com/BerriAI/litellm/pull/31760) | 修复`@default`端点后缀破坏adaptive thinking模型分类 | Vertex AI等提供商的端点后缀适配 |
| [#31786](https://github.com/BerriAI/litellm/pull/31786) | 流式响应中provider错误事件提升为APIError | 改善路由熔断、重试与日志准确性 |
| [#32712](https://github.com/BerriAI/litellm/pull/32712) | Guardrail UI模式下拉框按provider过滤 | 管理界面易用性提升 |
| [#32725](https://github.com/BerriAI/litellm/pull/32725) | UI用户代理与用量图表迁移至shadcn/recharts | 前端组件现代化 |
| [#32730](https://github.com/BerriAI/litellm/pull/32730) | 修复Amazon Bedrock添加`role:system`消息导致的缓存miss | 提升Claude Code等场景的缓存命中率 |
| [#32473](https://github.com/BerriAI/litellm/pull/32473) | 修复MCP DCR客户端重用导致redirect_uri永久失效 | 解决代理源变更后OAuth注册绑定问题 |
| [#32824](https://github.com/BerriAI/litellm/pull/32824) | MCP DCR桥接OAuth委托客户端通过单一信封令牌准入 | 推进MCP OAuth里程碑 |
| [#32931](https://github.com/BerriAI/litellm/pull/32931) | 新增重新设计的侧边栏账户菜单 | UI体验改进 |
| [#32943](https://github.com/BerriAI/litellm/pull/32943) | 复杂性路由记录每次决策原因 | 提升可观测性 |

### 🔄 仍在进行中的重要PR
- [#32942](https://github.com/BerriAI/litellm/pull/32942) **强制Dashscope tiered定价的预算与费用追踪**（关联 #21249, #30738）
- [#32935](https://github.com/BerriAI/litellm/pull/32935) **Guardrail扫描结果消毒处理后写入日志**（安全加固）
- [#32947](https://github.com/BerriAI/litellm/pull/32947) **复杂度路由器自适应软下限模式**（智能路由新特性）
- [#32936](https://github.com/BerriAI/litellm/pull/32936) **Content Filter支持pre_mcp_call钩子**（Guardrail能力扩展）

项目整体向 **安全增强、成本精准、MCP集成、UI现代化** 方向稳步推进。

---

## 4. 社区热点

### 🔥 评论/反应最多的Issues

| 编号 | 标题 | 评论 | 👍 | 链接 |
|------|------|------|----|------|
| #8842 | [Bug]: Router's async completion不触发CustomLogger回调 | 24 | 13 | [链接](https://github.com/BerriAI/litellm/issues/8842) |
| #18058 | [Bug]: ElevenLabs模型成本计算失效 | 8 | 0 | [链接](https://github.com/BerriAI/litellm/issues/18058) |
| #14635 | [Bug]: 超时显示"None seconds" | 7 | 8 | [链接](https://github.com/BerriAI/litellm/issues/14635) |
| #24123 | [Feature]: 支持Langfuse Python SDK v4 | 3 | 6 | [链接](https://github.com/BerriAI/litellm/issues/24123) |

### 📌 背后诉求分析
- **#8842**：用户深度依赖`CustomLogger`进行自定义监控与审计，路由器的异步调用不触发钩子导致监控断链。此问题从2025年2月持续至今，社区呼吁强烈。
- **#14635**：超时信息显示`None seconds`暴露了内部参数传递bug，用户无法诊断网络问题，影响生产调试体验。
- **#24123**：Langfuse已发布v4 SDK，LiteLLM仍锁定v2，阻碍用户采用最新特性（如新事件类型）。表明社区对第三方集成的时效性有较高要求。

---

## 5. Bug与稳定性

### 🔴 严重安全漏洞
| 编号 | 漏洞描述 | 严重程度 | 关联PR |
|------|----------|----------|--------|
| [#32889](https://github.com/BerriAI/litellm/issues/32889) / [#32890](https://github.com/BerriAI/litellm/issues/32890) | Guardrail `http_request()`原语存在SSRF，允许攻击者访问内部网络 | **Critical (CVSS 8.6)** | 无直接fix PR，但[#32911](https://github.com/BerriAI/litellm/pull/32911) 和 [#32935](https://github.com/BerriAI/litellm/pull/32935) 涉及guardrail日志与结果消毒，可能属于同一安全改进方向 |

### 🟠 关键功能Bug
| 编号 | Bug | 影响 | 已有FIX PR |
|------|-----|------|------------|
| [#32496](https://github.com/BerriAI/litellm/issues/32496) | Fireworks AI成本计算忽略`cached_tokens` | 多付费用 | [#29897](https://github.com/BerriAI/litellm/pull/29897) 和 [#32508](https://github.com/BerriAI/litellm/pull/32508) 均已提交 |
| [#21249](https://github.com/BerriAI/litellm/issues/21249) | Dashscope Qwen模型缺全局`input_cost_per_token`导致预算绕过 | 免费滥用 | [#32942](https://github.com/BerriAI/litellm/pull/32942) 已提交 |
| [#32904](https://github.com/BerriAI/litellm/issues/32904) | `map_system_message_pt`在处理content-block列表时崩溃 | 不支持system的模型出错 | 暂无 |
| [#32903](https://github.com/BerriAI/litellm/issues/32903) | GET /v1/models返回所有模型`owned_by: "openai"` | 元数据混乱 | 暂无 |

### 🟡 其他回归/次要Bug
- [#32854](https://github.com/BerriAI/litellm/issues/32854) Bedrock Mantle流式ID不满足OpenAI规范（每个SSE chunk唯一ID）
- [#25561](https://github.com/BerriAI/litellm/issues/25561) Anthropic `/v1/messages`流式端点丢失Gemini模型的tool_use参数
- [#32900](https://github.com/BerriAI/litellm/issues/32900) Gemini免费套餐密钥在wizard中无法使用
- [#32898](https://github.com/BerriAI/litellm/issues/32898) Ollama连接在Windows上被拒绝（`WinError 10061`）

---

## 6. 功能请求与路线图信号

### 📥 今日新增/活跃的功能请求
| 编号 | 请求内容 | 优先级信号 | 可能纳入下一版本 |
|------|----------|------------|------------------|
| [#32887](https://github.com/BerriAI/litellm/issues/32887) / [#32895](https://github.com/BerriAI/litellm/issues/32895) | **支持非OpenAI/Azure的`max_retries`参数** | 高（双提交） | ⭐ 已有关联PR？暂无，但需求明确 |
| [#32235](https://github.com/BerriAI/litellm/issues/32235) | **增加Per-MCP-Server Prometheus指标** | 中（运维场景） | ⭐ 与MCP集成路线图强相关 |
| [#24123](https://github.com/BerriAI/litellm/issues/24123) | **支持Langfuse Python SDK v4** | 高（6个👍） | ⭐ 依赖lib升级，预计下一里程碑 |
| [#32892](https://github.com/BerriAI/litellm/issues/32892) | **操作员可锁定AWS凭证参数，禁止调用方覆盖** | 中（安全场景） | 暂无PR |
| [#32947](https://github.com/BerriAI/litellm/pull/32947) | **复杂度路由自适应软下限模式** | 高（已有PR） | ✅ 正在审查，预计合并至v1.92 |

### 🗺️ 长期路线图信号
- **MCP集成深化**：今日多个PR（#32828, #32824, #32946）围绕DCR OAuth委托、交互式SSO登录，表明MCP成为核心发展方向。
- **成本与计费精准化**：Fireworks、Dashscope的修复表明正在系统化解决成本计算问题，可能统一cost calculator架构。
- **Guardrail安全体系**：SSRF漏洞和扫描结果消毒揭示了对安全原语的强化需求，未来可能引入URL白名单等。

---

## 7. 用户反馈摘要

### 👍 满意点
- **活跃的社区响应**：多个PR在提交后24小时内获得review并合并（如#32931 UI侧边栏）。
- **v1.91.2镜像签名验证**：用户对供应链安全增强表示认可（来自release note）。
- **MCP功能持续迭代**：用户对动态注册OAuth委托的推进持积极态度（#32824评论）。

### 👎 痛点与不满
- **超时错误信息不友好**：`Connection timed out after None seconds` 让用户无法定位网络瓶颈（#14635）。
- **成本计算不一致**：无论是ElevenLabs、Fireworks AI还是Dashscope，费用偏差导致财务报告不准确，用户需要手动校验（#18058, #32496, #21249）。
- **自定义日志钩子失效**：Router异步路径下`CustomLogger`完全不触发，迫使部分用户放弃路由功能（#8842）。
- **oAuth2-proxy集成问题**：部署在反向代理后UI重定向循环，需要手动添加cookie或修改代码（#19856）。

### 💡 典型使用场景
- **BYO LLM代理**：用户将多种模型（Gemini, Anthropic, Bedrock）统一接入LiteLLM，期待一致的接口与成本管控。
- **Claude Code增强**：多个Issue提及Claude Code场景（#32730缓存miss, #25561tool_use丢失），说明开发者工具集成是重要用例。
- **Guardrail驱动的内容审核**：企业用户依赖guardrail对敏感内容过滤，SSRF漏洞引发安全担忧。

---

## 8. 待处理积压

### 📌 长期未解决的重大问题

| 编号 | 标题 | 创建时间 | 最后更新 | 评论数 | 原因 |
|------|------|----------|----------|--------|------|
| [#8842](https://github.com/BerriAI/litellm/issues/8842) | Router's async completion不触发CustomLogger回调 | 2025-02-26 | 2026-07-11 | 24 | 涉及异步架构重构，

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，以下是基于您提供的 GitHub 数据生成的 Temporal 项目动态日报。

---

### Temporal 开源项目动态日报 (2026-07-12)

**分析师**：AI 智能体与个人 AI 助手领域开源项目分析师

---

### 1. 今日速览

今日 Temporal 项目整体处于**高度活跃**状态，开发与社区互动密集。过去 24 小时内，虽然有 5 个活跃的 Issue 和 4 个已合并的 Pull Request，但**未出现新的严重 Bug 报告或版本发布**。项目核心进展集中在 **CHASM** 和 **Nexus** 两大特性领域的深耕，包括对 Nexus 操作的重置支持、性能优化和日志改进。同时，社区对 **PostgreSQL 索引膨胀**和**工作流重置**的 Bug 报告持续关注，暗示在高负载场景下的稳定性仍需加强。整体来看，项目维持了稳健的迭代节奏，健康度良好。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

过去 24 小时内，共有 **4 个 Pull Request 被合并或关闭**，标志着项目在多个关键功能线上取得了实质性进展。

-   **CHASM (协作历史与状态机) 功能深化**：
    -   **PR #11021**：机器人提交的 `1.32.0: Prepare release branch` 已关闭，表明团队正在为下一个主要版本（1.32.0）做准备，包括覆盖治理文件和更新依赖。
    -   **PR #10930**：`Enable standalone activity by default` 已合并，正式将“独立活动”特性默认启用。这是 CHASM 特性成熟度的一个重要里程碑，意味着新项目将默认获得更灵活的活动执行模型。
    -   **PR #10957**：`Add RefConsistencyLevel CHASM transition option` 已关闭，该 PR 为 CHASM 的 `TransitionOption` 引入了读取一致性级别控制，提升了状态机操作的灵活性与精确性。

-   **SAA (服务化架构适配) 稳定性增强**：
    -   **PR #10859**：`SAA operator API fixes and tests` 已合并，该 PR 修复了操作符 API 的相关问题并增加了测试，为服务化架构的稳定性提供了保障。

这些合并表明，项目的核心开发工作正围绕 **CHASM 和 SAA 两大架构升级**稳步推进，为未来版本的性能和功能扩展奠定基础。

### 4. 社区热点

过去 24 小时，社区讨论焦点主要集中在对已知问题的反馈和协作上，其中较有代表性的是：

-   **`#10873` [OPEN] Add FirstExecutionRunID to start response**
    -   **链接**: [https://github.com/temporalio/temporal/pull/10873](https://github.com/temporalio/temporal/pull/10873)
    -   **热度**: 此 PR 虽属于开发中的特性增强，但关联了用户需求 Issue (`#8537`)，旨在解决 SDK 在创建重复工作流时无法获取首次运行 ID 的问题。这反映了社区对**提升工作流生命周期管理可观测性和简化客户端逻辑**的强烈需求。

-   **`#10145` [OPEN] [potential-bug] PostgreSQL - Index Bloat**
    -   **链接**: [https://github.com/temporalio/temporal/issues/10145](https://github.com/temporalio/temporal/issues/10145)
    -   **热度**: 该 Issue 已存在数月，但昨日（7月11日）仍有更新，且获得了 5 条评论与 2 个点赞。这表明在高吞吐量场景下使用 PostgreSQL 的用户正面临严重的**数据存储膨胀和索引管理困难**问题，这已成为一个长期困扰社区的稳定性与成本痛点。

### 5. Bug 与稳定性

今日未报告新的严重 Bug。社区讨论的 Bug 主要集中在以下长期存在的问题上：

-   **严重 (High)**：
    -   **`#10145` [OPEN] PostgreSQL - Index Bloat**: 高吞吐量场景下数据库索引无节制膨胀，即便设置了保留期。目前暂无关联的修复 PR。这是一个潜在的稳定性与资源管理隐患。[Issue链接](https://github.com/temporalio/temporal/issues/10145)

-   **中等 (Medium)**：
    -   **`#10690` [OPEN] ResetWorkflowExecution returns "workflow not found" when targets an older run**: 重置工作流到已删除当前运行的老版本时，因无法定位当前运行而失败。此问题影响工作流生命周期管理的准确性，尤其在异常处理场景下。暂无关联修复 PR。[Issue链接](https://github.com/temporalio/temporal/issues/10690)

-   **较低 (Low)**：
    -   **`#9581` [OPEN] Worker deployment set-current-version cannot switch to unversioned**: 在默认命名空间中，无法从有版本号的部署回退到无版本号的状态。这是一个 CLI 和 Server 交互的易用性问题。[Issue链接](https://github.com/temporalio/temporal/issues/9581)
    -   **`#10236` [OPEN] Temporal Helm schema Job containers fail with Istio STRICT mTLS**: Helm Chart 在 Istio 严格 mTLS 环境下部署任务时失败，影响了特定基础设施环境下的部署体验。[Issue链接](https://github.com/temporalio/temporal/issues/10236)

### 6. 功能请求与路线图信号

今日的 PR 活动清晰地揭示了下个版本（1.32.0）中可能包含的功能方向：

-   **Nexus 生态完善**：
    -   **`#10986` [OPEN] Support CHASM Nexus operations in workflow reset reapply**: 支持在重置工作流时重新应用 CHASM 支持的 Nexus 操作，这是确保状态一致性的关键步骤。
    -   **`#10948` [OPEN] system-nexus: add metadata flag to indicate response has a Payload**: 为 Nexus 代理增加响应元数据，以指示是否包含负载，优化代理处理逻辑。
    -   **`#11012` [OPEN] [NOT READY] Add Nexus tenant rate-limit interceptor**: 引入 Nexus 租户级别限流拦截器接口，为多租户场景下的资源管控提供扩展点。

-   **开发者体验与可观测性提升**：
    -   **`#10890` [OPEN] feat(events): structured event framework**: 引入结构化事件框架，旨在为命名空间、复制等生命周期事件提供统一、可插拔的日志和监控能力，这标志着项目**可观测性建设的重要升级**，有望在下一代版本中增强调试与运维能力。

### 7. 用户反馈摘要

从 Issues 评论中可提炼出以下用户痛点与场景：

-   **PostgreSQL 用户的核心痛点**：在高吞吐量（数十万工作流/小时）场景下，用户普遍反馈数据库大小不受保留期控制，即使数据表实际内容不大，整个数据库也会不断膨胀。用户希望 Temporal 能更好地管理索引，提升 PostgreSQL 方案的资源效率与可预测性。 (`#10145`)
-   **工作流恢复流程的“小陷阱”**：当工作流的“当前运行”被删除（例如手动清理）后，用户期望能通过指定 `runId` 来重置一个之前的运行。然而，当前行为会因为找不到“当前运行”而报错，这打断了预期的恢复流程，增加了故障处理的复杂性。 (`#10690`)
-   **部署与操作的门槛**：用户因误操作在默认命名空间创建了带版本号的 Worker 部署后，发现无法回退到无版本状态，表明版本管理功能在易用性和容错性上存在不足。 (`#9581`) 同时，与 Istio 等主流云原生组件的兼容性问题（`#10236`）也持续困扰着部分用户，增加了部署成本。

### 8. 待处理积压

以下 Issue 长期未得到有效解决，但在社区中仍有讨论，建议维护者重点关注：

-   **`#9581` Worker deployment set-current-version cannot switch to unversioned** (已开放 **115天**): 这个关于 Worker 版本回退的易用性 Bug 已存在近 4 个月，至今未有官方回复或修复迹象，可能影响用户对 Worker 版本管理功能的信心。[Issue链接](https://github.com/temporalio/temporal/issues/9581)
-   **`#10145` PostgreSQL - Index Bloat** (已开放 **72天**): 作为高负载场景下的关键稳定性问题，该 Issue 已存在超过 2 个月，且讨论热度不减。`potential-bug` 标签表明其已被认可为潜在问题，但缺乏明确的解决方案路径，可能成为社区信任度的潜在风险。[Issue链接](https://github.com/temporalio/temporal/issues/10145)

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*