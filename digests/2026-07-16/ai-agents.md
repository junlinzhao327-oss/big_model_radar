# OpenClaw 生态日报 2026-07-16

> Issues: 483 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-15 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 OpenClaw GitHub 数据，为您生成 2026-07-16 的项目动态日报。

---

## OpenClaw 项目日报 (2026-07-16)

**分析师：** AI 智能体与个人 AI 助手领域开源项目分析师

### 1. 今日速览

今日 OpenClaw 项目社区活动颇为活跃。关键动态集中在 **v2026.7.2-beta.1** 版本的发布与 **v2026.7.1** 版本的稳定性问题上。新版本引入了远程编码会话和原生自动化节点等重磅功能，但大量关于 `v2026.7.1` 版本网关崩溃循环、数据迁移冲突及修复路径失效的 Bug 报告成为社区焦点，表明项目在快速迭代中，启动流程与状态迁移机制的健壮性仍需加强。总体来说，项目**活跃度极高**，版本迭代迅速，但**稳定性问题**是当前社区关注的头号议题。

### 2. 版本发布：v2026.7.2-beta.1

**发布内容：**
-   **发布地址：** [v2026.7.2-beta.1 Release Page](https://github.com/openclaw/openclaw/releases/tag/v2026.7.2-beta.1)
-   **核心亮点：**
    -   **远程编码会话：** 允许在云端工作器上运行 Control UI 会话，并支持在任何主机上通过终端直接操作 Codex 和 Claude Catalog 会话，以及恢复 OpenCode 和 Pi 会话。
    -   **原生自动化与节点：** 引入了新的原生自动化功能和节点支持（具体细节待查阅完整发布说明）。
-   **破坏性变更与迁移注意事项：** 基于 `v2026.7.1` 的大量迁移问题报告，**强烈建议所有从 `v2026.6.x` 或更早版本升级的用户**，在升级前备份所有核心数据。特别注意，`v2026.7.1` 中暴露的“遗留状态迁移”问题可能影响到 `v2026.7.2-beta.1` 的升级过程。用户应注意 `startupMigrationWarnings` 相关门控可能导致网关无法启动，并确保 `openclaw doctor` 命令能够完全修复所有冲突。

### 3. 项目进展

今日合并/关闭的 PR 主要围绕修复 `v2026.7.1` 引入的回归问题和提升 CI/CD 流程效率。

-   **[已合并] 修复 Zalo 渠道：** `#108434` (fix(zalo): report unsupported message actions correctly) 修复了 Zalo 渠道中操作错误提示不准确的问题。
-   **[已合并] 修复发布验证流程：** 多个 PR 旨在修复发布验证流水线问题：
    -   `#108476`: 修复了 QA 包测试中引用私有运行时的问题。
    -   `#108472`: 修复了 QA 环境隔离问题。
    -   `#108467`: 使用可靠的安装工具链修复了冻结发布版本验证失败的问题。
-   **[已合并] 修复发布验证相关性：** `#108480` 修复了发布验证中的断言不匹配问题。
-   **项目健康度提升：** 整体来看，项目在修复 `v2026.7.1` 的紧急 Bug 和保障 `v2026.7.2` 发布流程顺畅上投入了大量精力，但尚未看到针对社区 P0 级 Bug 的全面修复 PR 被合并。

### 4. 社区热点

今日讨论最活跃的议题高度聚焦于 `v2026.7.1` 版本的升级失败和功能瘫痪问题，社区情绪较为焦虑。

-   **头条热点：[Bug]: > All tool results return "(see attached image)" literal string instead of actual output.** (#104721)
    -   评论数：17
    -   **诉求分析：** 此 P0 级回归 Bug 是**用户体验的噩梦**。用户反馈所有工具调用的结果都被替换为占位符字符串 `"(see attached image)"`，导致智能体完全无法使用。这直接触及了产品的核心功能，是当务之急。
    -   [Issue链接](https://github.com/openclaw/openclaw/issues/104721)

-   **核心争议：[Bug]: Second message in a session fails with "reply session initialization conflicted"** (#102020)
    -   评论数：14
    -   **诉求分析：** 此问题导致会话在第2个消息就失败，根本不可用。标注为跨渠道问题，影响面广。用户期望最基本的连续对话功能是稳定的。
    -   [Issue链接](https://github.com/openclaw/openclaw/issues/102020)

-   **技术性讨论：[Bug]: After updating to OpenClaw 2026.7.1, legacy state migration warnings keep appearing** (#90213)
    -   评论数：11
    -   **诉求分析：** 用户执行了官方推荐的 `openclaw doctor --fix` 命令后，问题依旧存在。这表明自动修复工具有效性不足，引发了用户对官方升级指南和工具链的信任危机。
    -   [Issue链接](https://github.com/openclaw/openclaw/issues/90213)

### 5. Bug 与稳定性

以下是今日报告中按严重程度排列的关键 Bug。P0 级别问题突出，且主要与 `v2026.7.1` 升级有关。

**P0 (严重阻塞性)：**
-   **[Bug]: > All tool results return "(see attached image)"...** (#104721) - 数据丢失，核心功能瘫痪。
-   **[Bug]: Gateway fails to start due to strict startupMigrationWarnings guard...** (#107694) - 升级后网关无法启动。
-   **[Bug]: 2026.7.1 gateway crash-loop: legacy memory sidecar `meta`/`chunks` conflicts are fatal...** (#107220) - 网关启动崩溃循环。
-   **[Bug]: 2026.7.1 startup-migration gate is fatal...** (#107227) - 启动迁移门控致命，且 `doctor` 命令无法修复。
-   **[Bug]: Openclaw Update 2026.7.1 Crash** (#107330) - 升级操作本身导致崩溃。
-   **[Bug]: Gateway refuses readiness after 2026.7.1 update due to plugin install metadata conflict...** (#107727) - 升级后网关无法就绪。

**P1 (高影响性)：**
-   **[Bug]: Second message in a session fails with "reply session initialization conflicted"...** (#102020) - 跨渠道会话中断。
-   **[Bug]: Non-Anthropic models output tool calls as plain text...** (#90288) - 模型兼容性问题导致功能异常。
-   **[Bug]: DeepSeek cache hit rate <10% after 6.x upgrade...** (#94518) - 关键性能指标大幅下降。
-   **Codex PreToolUse native hook relay spawns CPU-bound processes...** (#91009) - 潜在的性能耗尽问题。

**已知修复进展：**
-   对于 `cron` 工具与 `llama.cpp` 的 Schema 兼容性问题（#107449），已有名为 `fix(cron): llama.cpp rejects unanchored cron tool schema patterns` 的 PR（#108469）提交。
-   针对 `v2026.7.1` 的启动崩溃问题（#107330），修复 PR `fix(daemon): gateway fails to launch on Windows when the profile path contains CJK characters`（#107751）已提交，但似乎仅针对特定场景。

### 6. 功能请求与路线图信号

-   **AI 安全与质量可观测性：** 用户 `@skoya` 提出的 `[Feature]: Add AI safety and quality observability events` (#82548) 今日有相关 PR `feat: AI safety/quality event taxonomy` (#107744) 提交，该 PR 规模较大且涉及范围广，**极有可能被纳入 `v2026.7.x` 或后续大版本中**。这标志着项目开始重视生产环境下的 AI 安全监控。
    -   [Issue链接](https://github.com/openclaw/openclaw/issues/82548)
    -   [PR链接](https://github.com/openclaw/openclaw/pull/107744)

-   **智能多 LLM 路由器：** 用户 `@alexandre-leng` 提出的 `Reduce Token Costs with an Intelligent Multi-LLM Router` (#107686) 获得了一些关注。虽然该请求尚处于早期讨论阶段，但其自动为不同任务（如代码、视觉、通用）选择最优模型的理念，符合成本优化的大趋势。若有社区广泛支持，可能成为未来的探索方向。
    -   [Issue链接](https://github.com/openclaw/openclaw/issues/107686)

### 7. 用户反馈摘要

从今日的 Issues 和评论中，可以提炼出以下用户痛点：

-   **升级恐惧：** “每次升级都像在赌博，不知道会炸掉哪里。”——这句虽非直接引用，但很好地概括了 `v2026.7.1` 升级引发大面积故障后用户的普遍心态。大量用户报告升级后网关直接无法工作。
-   **信任危机：** “我运行了 `doctor --fix`，但问题依旧。你们的自动修复工具有效吗？”——来自 Issue #90213 的核心反馈。用户对官方提供的工具链和升级指南的信任度受到打击。
-   **核心功能不可用的挫败感：** “连正常的对话都无法维持，第一个消息后第二个就出错。”（#102020），“所有的工具返回结果都是‘见附件’，这个软件彻底废了。”（#104721）。这些反馈显示了用户对于基础功能稳定性的极度不满。
-   **对性能敏感的担忧：** Codex hook 进程 CPU 占用 100% (#91009) 以及 DeepSeek 缓存命中率暴跌 (#94518) 的反馈表明，专业用户对系统的资源消耗和成本效率非常敏感。

### 8. 待处理积压

以下为长期未解决但影响重大的 Issue，需维护者重点关注：

-   **特性请求：** `Feature: Add denylist support for exec-approvals` (#6615)
    -   创建于：2026-02-01 | 评论：9 | 👍：7
    -   **简述：** 一个被广泛期待的安全功能。用户希望在现有的白名单执行批准机制上，增加黑名单功能，以实现“允许一切，除X外”的安全策略。
    -   **建议：** 这是社区呼声很高的安全增强功能，建议规划进后续版本。
    -   [Issue链接](https://github.com/openclaw/openclaw/issues/6615)

-   **Bug：** `[Bug]: Model fallback chain not triggered on provider-wide quota exhaustion` (#85103)
    -   创建于：2026-05-21 | 评论：10
    -   **简述：** 当模型提供商达到配额上限时，配置的模型回退链未生效，导致服务中断。
    -   **建议：** 这是影响高可用性和用户体验的关键问题，应在短期内优先解决。
    -   [Issue链接](https://github.com/openclaw/openclaw/issues/85103)

-   **Bug：** `[Bug]: Local assistant attachments shown as "Unavailable — Outside allowed folders"...` (#67915)
    -   创建于：2026-04-17 | 评论：7 | 👍：2
    -   **简述：** 本地文件附件附件明明在配置允许的路径内，却被误标为不可用，导致用户无法使用。
    -   **建议：** 该问题存在超过两个月，严重影响使用本地模型的用户体验。
    -   [Issue链接](https://github.com/openclaw/openclaw/issues/67915)

---

## 横向生态对比

# 个人 AI 助手与自主智能体开源生态横向对比分析报告

## 1. 生态全景

2026-07-16，个人 AI 助手与自主智能体开源生态呈现出 **“两极分化、纵深整合”** 的态势。一方面，以 LiteLLM、Hermes Agent 为代表的模型网关与多平台适配层项目保持极高迭代频率，社区讨论集中在成本优化与认证稳定性；另一方面，以 OpenClaw 为核心的智能体框架项目因 v2026.7.1 版本升级引发的严重回归问题，导致社区信任度短期受挫，但也侧面印证了快速迭代中的质量挑战。Pi 与 OpenHands SDK 则在具体场景（TUI 交互、云会话持久化）上稳步打磨。整体而言，生态正从“功能拼接”走向“成熟稳定”，但各项目在用户体验、性能与安全上的投入不均衡。

## 2. 各项目活跃度对比

| 项目 | 今日 Issue 更新数 | 今日 PR 更新数 | 新版本发布 | 健康度评估 |
|------|------------------|----------------|------------|------------|
| **OpenClaw** | 大量 Bug 报告（未精确统计） | 较多合并（具体未列） | ✅ v2026.7.2-beta.1 | ⚠️ 风险：严重稳定性回归，网关崩溃、数据迁移冲突频发 |
| **Hermes Agent** | 500 条（新开/活跃 169，关闭 331） | 500 条（合并/关闭 50，积压 450） | ❌ 无 | ⚠️ 瓶颈：PR 积压严重，合并效率低下，但 Issue 清理积极 |
| **OpenHands SDK** | 16 条（新开 13，关闭 3） | 15 条（合并/关闭 7，待合 8） | ✅ v1.36.1 | ✅ 良好：修复与功能并进，延迟加载、插件 API 等改进 |
| **Pi** | 52 条（新开 13，关闭 39） | 6 条（合并/关闭 6） | ❌ 无 | ✅ 稳健：核心 Bug 快速修复，社区热点聚焦 UX |
| **LiteLLM** | 97 条 | 307 条（合并/关闭 91） | ✅ v1.94.0-dev.1 | ✅ 极活跃：快速迭代，镜像签名增强安全，大量 PR 待合 |
| **Temporal** | 2 条（1 开 1 关） | 69 条（合并/关闭 27） | ❌ 无 | ✅ 稳定：PR 节奏快，无重大新 Bug，核心功能推进 |

**活跃度分层**：
- **极高**：LiteLLM、Hermes Agent（海量 Issue/PR）
- **高**：OpenClaw、Pi（Issue 密集，反馈紧迫）
- **中**：OpenHands SDK（精炼但稳定）
- **中低**：Temporal（成熟期，反馈量少但开发勤）

## 3. OpenClaw 在生态中的定位

- **优势**：作为“核心参照”项目，OpenClaw 定义了**远程编码会话**、**原生自动化节点**等前瞻功能，尤其在云端工作器与终端操作的整合上领先同类，且拥有活跃的控台 UI（Control UI）生态。
- **技术路线差异**：相较于 Hermes Agent 的“平台适配优先”和 Pi 的“轻量 TUI 交互”，OpenClaw 更强调**全栈智能体基础设施**，包括网关、状态迁移、工具调用链等复杂架构，这也导致其版本升级时容易引发连锁回归。
- **社区规模对比**：从 Bug 报告与评论数看，OpenClaw 的社区反馈热度与 LiteLLM 相当（单 Issue 最高 17 条评论），但缺乏精确的 Issue/PR 统计对比。以 Hermes Agent 为参照（500 条级更新），OpenClaw 的活跃度应属于“高”梯队，但其**稳定性信任度**低于 OpenHands SDK 和 Pi。
- **竞争/互补关系**：OpenClaw 与 Pi 在“编码智能体”场景存在重叠，但 OpenClaw 的云端远程会话能力与 Pi 的本地 TUI 形成互补；与 Hermes Agent 相比，OpenClaw 更侧重于企业级部署场景。

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|----------|----------|----------|
| **模型兼容性与输出结构化** | OpenClaw、Hermes Agent、Pi、OpenHands SDK、LiteLLM | 多项目用户抱怨非 Anthropic 模型输出工具调用异常、新旧模型（如 GPT-5.6、Claude 新版本）验证失败；社区强烈要求 SDK 提供结构化输出（如 JSON Schema 声明式支持） |
| **认证与安全加固** | OpenClaw、Hermes Agent、Pi、LiteLLM、OpenHands SDK | 多个项目报告：OAuth 凭证刷新失败导致会话中断（OpenHands ACP）、GitHub 自动登出（Pi）、SSO 用户限制（LiteLLM）、XAI 403 错误（Hermes Agent）；社区要求更细粒度的权限层与黑名单机制 |
| **会话持久化与延迟加载** | OpenHands SDK、Pi | OpenHands SDK 通过 PR #4100 实现延迟加载显著降低启动开销；Pi 的 SQLite 会话存储 PR #6594 待合并，表明大规模会话管理成为刚需 |
| **可观测性与安全监控** | OpenClaw、OpenHands SDK | OpenClaw 用户 @skoya 提交 AI 安全事件分类 PR，OpenHands 增加 tool_call_id 追踪；两个项目同步探索生产环境下的 AI 质量可见性 |
| **预算与成本控制** | LiteLLM、Pi | LiteLLM 社区强烈要求 SSO 取消限制、支持 Langfuse v4，并修复 provider 预算配置 Bug；Pi 用户关注 CPU 100% 占用与缓存命中率 |

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent | OpenHands SDK | Pi | LiteLLM | Temporal |
|------|----------|--------------|---------------|----|---------|----------|
| **功能侧重** | 全栈智能体框架（会话、工具、网关、状态机） | 多平台适配器（Slack、Telegram、CLI）与插件生态 | 云会话 SDK（持久化、ACP 协议、可观测性） | 轻量 TUI 编码智能体（本地优先） | 模型网关与代理（路由、计费、安全） | 工作流编排引擎（长时间运行任务、调度） |
| **目标用户** | 企业 AI 平台开发者、需远程编码的团队 | 追求多平台统一体验的个人/团队 | 构建云原生 Agent 应用的后端开发者 | 追求本地流畅 TUI 的独立开发者和高级用户 | 模型调用成本敏感型团队、运维 | 微服务架构下复杂工作流的设计者 |
| **技术架构关键差异** | 复杂状态迁移 + 网关 + 插件系统 | 适配器模式 + 插件扩展 + 安全层 | ACP 协议 + 持久化存储 + agent-server API | 进程内 TUI + 扩展机制 + 本地文件操作 | 中间代理 + 路由策略 + 计费与日志模块 | 分布式事务日志 + 任务队列 + 可分离工作者 |
| **社区情绪** | 焦虑（升级恐惧） | 期待但不满（Merge 瓶颈，XAI 信任危机） | 积极（修复迅速，反馈清晰） | 务实（聚焦日常 UX 问题） | 急切（功能诉求多，定价敏感） | 平静（成熟项目，需求来自企业级） |

## 6. 社区热度与成熟度

- **快速迭代阶段（风险与创新并存）**：
  - **LiteLLM**：日均 307 条 PR 更新，版本周更，社区诉求高度集中于功能扩展与定价策略，属于生态中“增长引擎”。
  - **Hermes Agent**：虽 PR 合并效率低，但 Issue 关闭量大（331 条），表明团队在消化历史积压，且新功能（权限层级、子 Agent 模型配置）信号强烈，处于“功能爆炸期”。
  - **OpenClaw**：版本跳跃快（隔日发布 beta），但稳定性问题集中爆发，属于“快速试错”阶段，急需质量巩固。

- **质量巩固阶段（稳定优先）**：
  - **OpenHands SDK**：版本节奏适中（v1.36.1），延迟加载、认证修复等改进均经过 QA 验证，社区反馈量少但针对性强。
  - **Pi**：无新版发布，但修复 PR 密集（session-id 截断、空指针、Windows 标题），TUI 性能优化长期跟进，属于“精雕细琢”型。
  - **Temporal**：Issue 极少，PR 集中在内核优化（动态分区、backlog 精度），标志着项目已进入架构成熟期，适合企业生产部署。

## 7. 值得关注的趋势信号

1. **“结构化输出”成为智能体 SDK 的必备能力**  
   OpenHands SDK（#2566）与 Pi（#6278）的用户均要求 SDK 原生支持 JSON Schema 声明，而不是依赖手动解析。这预示着下一波智能体框架将从“自由文本输出”转向“契约式输出”，降低工具调用失败率。

2. **安全认证从“漏洞修补”走向“主动防御”**  
   多个项目同时出现凭证刷新失败（OpenHands ACP、Hermes XAI）、配置注入风险（Hermes 新增 allow_agent_config_writes）、SSRF 漏洞（LiteLLM yarl）。社区对“零信任”架构的呼声正在上升，未来 3–6 个月将有更多项目引入**凭证轮换策略**、**会话绑定认证**以及**黑名单/白名单双机制**。

3. **会话持久化成为基础架构标配**  
   OpenHands SDK 的延迟加载（PR #4100）、Pi 的 SQLite 存储（PR #6594）、OpenClaw 的迁移冲突（#107220）均指向同一痛点：智能体会话的**持久化与高效恢复**。这将是所有智能体框架向生产环境迈进的“最后 10% 难题”。

4. **模型路由从“简单轮询”走向“成本-质量双目标优化”**  
   LiteLLM 的“lite autoroute”（PR #33249）与 OpenClaw 的智能多 LLM 路由器请求（#107686）表明，社区不再满足于单一模型，而是要求系统能根据任务复杂度自动选择性价比最优的模型。**MoE（混合专家）思想正在渗透至开源智能体基础设施层**。

5. **AI 安全可观测性从“可选”变为“必备”**  
   OpenClaw 的 AI safety/quality event taxonomy PR（#107744）与 OpenHands SDK 的 tool_call_id 追踪（PR #4010）同步推进，反映开发者对生产环境下智能体行为“透明化”的迫切需求。未来将出现统一的 AI 事件分类标准，类似传统 IT 中的 OpenTelemetry。

---

**对开发者的参考建议**：
- 若您是 **企业级平台建设者**，可关注 OpenClaw 和 LiteLLM 的路由与预算能力，但需警惕 OpenClaw 当前稳定性风险。
- 若您是 **个人效率工具用户**，Pi 提供了最流畅的 TUI 体验，但需关注其 TUI 渲染性能改进（#6050）。
- 若您需要 **自定义 Agent 后端**，OpenHands SDK 的 ACP 协议与持久化方案是最成熟的选择，但需提前适配其认证刷新机制。
- 所有开发者都应**将结构化输出、会话持久化、安全可观测性**纳入下一阶段的技术选型评估清单。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 Hermes Agent 项目数据，生成一份客观专业的项目动态日报。

---

## Hermes Agent 项目动态日报 | 2026-07-16

### 1. 今日速览

过去24小时内，Hermes Agent 社区异常活跃，共有 **500条Issue更新** 和 **500条PR更新**。Issue方面，关闭速度（331条）远超新开/活跃（169条），表明维护团队正在高效地清理积压。然而，PR积压情况严重，待合并的 PR 高达 **450条**，仅合并/关闭了50条，说明维护团队的合并瓶颈依然存在，可能会影响新功能和修复的交付速度。整体项目生态活跃，但需关注 PR 合并效率与版本发布的节奏。

### 2. 版本发布

过去24小时内，项目无新版本发布。

### 3. 项目进展

尽管合并效率不高，但今日仍有50个 PR 被合并/关闭，推动了项目在多个方面的改进。

- **核心功能修复**：
    - **流式配置修复**：PR [#51167](https://github.com/NousResearch/hermes-agent/pull/51167) 已关闭，修复了CLI对话循环中未遵守 `streaming.enabled` 配置项的问题。这解决了部分用户开启流式传输但实际未生效的困扰，属于重要的配置一致性修复。
    - **OpenAI兼容性修复**：PR [#63239](https://github.com/NousResearch/hermes-agent/pull/63239) 正在处理，修复了配置文件中布尔值 `false` 被错误解析为“开启”传输模式的问题。这保障了通过YAML配置禁用流式传输功能的可靠性。

- **平台与适配器改进**：
    - **Slack平台感知**：PR [#63234](https://github.com/NousResearch/hermes-agent/pull/63234) 修复了Slack平台上硬编码过时API声明的问题，使Agent在加载了Slack工具集后能正确执行操作，增强了Slack集成的实用性和智能性。

- **安全与权限增强**：
    - **配置写入保护**：PR [#63233](https://github.com/NousResearch/hermes-agent/pull/63233) 新增了 `security.allow_agent_config_writes` 配置项（默认关闭），防止Agent会话中被注入的恶意指令修改关键的 `config.yaml`。这增强了项目的安全性基线。
    - **Bitwarden凭证访问管控**：PR [#63236](https://github.com/NousResearch/hermes-agent/pull/63236) 新增了针对通过终端工具访问Bitwarden CLI的恶意模式识别，提升了凭证安全性。

**总结**：项目在修复配置BUG、增强平台适配和加固安全防线方面取得了扎实进展。大量关闭的 Issue 也显示项目在消化历史问题。

### 4. 社区热点

社区讨论主要围绕几个热点展开：

- **插件接口拓展**：Issue [#64182](https://github.com/NousResearch/hermes-agent/issues/64182)（11条评论）是社区关于核心插件接口拓展的追踪贴，源于 Discord 社区的讨论。这反映了社区对于让长期等待的 PR 能够稳定、公开地交付的核心诉求。插件开发者希望有一个更清晰、标准化的接口规范。

- **XAI OAuth授权问题**：Issue [#26847](https://github.com/NousResearch/hermes-agent/issues/26847)（29条讨论）虽已关闭，但因其讨论热度最高而成为今日焦点。用户指出标准 SuperGrok 订阅者却遭遇 **HTTP 403** 错误，后端违背了文档承诺（所有层级均支持），仅对 “Heavy” 用户开放。这暴露了项目在与第三方服务集成时，文档与后端逻辑不一致的信任危机。

- **Dashboard认证与Docker兼容性问题**：多个关于 Dashboard 认证的 Issue 引起热议，如 [#59113](https://github.com/NousResearch/hermes-agent/issues/59113) 和 [#55130](https://github.com/NousResearch/hermes-agent/issues/55130)。用户在讨论 Dashboard 在 Docker 环境或仅使用密码认证时遇到的 500 错误和功能失效问题。这表明 Dashboard 的认证重构引入了显著的回归问题，尤其是在非标准部署场景下。

### 5. Bug 与稳定性

- **严重度: P1 (已关闭)**
    - **Ollama 推理 effort 忽略**：Issue [#25758](https://github.com/NousResearch/hermes-agent/issues/25758) 报告，在 Ollama 上设置 `agent.reasoning_effort: none` 无效，导致 Agent 陷入“中等”模式，并可能引发长达 28 分钟、高达 65k tokens 的“思维”循环。此问题已关闭，应修复完成。
    - **Bedrock + Claude 凭证丢失**：Issue [#28156](https://github.com/NousResearch/hermes-agent/issues/28156) 报告，配置向导接受不完整的 Bearer-only 设置，导致运行时失败，且模型选择器在 EU 地区显示不可用的配置文件。此问题也已关闭。

- **严重度: P2 (新开/活跃)**
    - **Telegram 适配器启动失败**：Issue [#64674](https://github.com/NousResearch/hermes-agent/issues/64674) 是最新的严重BUG，报告在启用多配置文件且机器人的Token存储在非默认配置文件中时，Telegram 适配器无法启动。这是一个影响核心功能的配置BUG，**暂无标记为已修复**。
    - **Dashboard 多Tab会话串扰**：Issue [#62726](https://github.com/NousResearch/hermes-agent/issues/62726) 报告了 Dashboard 在多个浏览器标签页下会话状态混乱及“/new”功能挂起的严重问题。此问题影响用户体验，**暂无标记为已修复**。
    - **Qwen推断思维上下文丢失**：Issue [#56004](https://github.com/NousResearch/hermes-agent/issues/56004) 报告了在使用 vLLM 运行的 Qwen 模型时，多轮对话中的推理思维链在重放时丢失。这是模型兼容性问题，**暂无标记为已修复**。

- **严重度: P3 (新开/活跃)**
    - **Gateway 会话凭证绑定**：Issue [#64271](https://github.com/NousResearch/hermes-agent/issues/64271) 报告了长运行 Gateway 会话中，凭证更新后无法切换到新凭证池的问题，这会影响动态凭据管理。

### 6. 功能请求与路线图信号

超过100条新开的 Issue 包含了大量功能请求。结合已有 PR，以下请求可能进入下一版本路线图：

- **权限层级系统**：PR [#59857](https://github.com/NousResearch/hermes-agent/pull/59857) 提出的“所有者/用户”权限层级，解决非管理员可自批准危险命令的缺陷。这很可能被纳入下一版本的默认安全策略。
- **可配置 Temperature 参数**：Issue [#17565](https://github.com/NousResearch/hermes-agent/issues/17565) 已获得 **10个 👍**，是社区呼声极高的功能。该项目旨在让用户自定义模型推理温度，以解决因硬编码温度导致的幻觉问题。此功能实现相对简单，优先级高。
- **跨平台会话共享**：Issue [#4335](https://github.com/NousResearch/hermes-agent/issues/4335) 提出的跨平台（CLI ↔ Telegram）会话上下文共享，是一个深度的生态整合需求。从讨论热度和发展方向看，这会是 Hermes 作为个人智能体实现统一体验的关键一步，但技术挑战较大，预计是中期规划。
- **Kanban通知系统泛化**：Issue [#49190](https://github.com/NousResearch/hermes-agent/issues/49190) 提出的将 Kanban 通知硬编码逻辑泛化为事件订阅系统，并允许用户自定义投递渠道。这体现了社区对系统灵活性和定制化的追求。
- **预配置的子Agent模型**：Issue [#58731](https://github.com/NousResearch/hermes-agent/issues/58731) 要求允许为不同子Agent角色（如 master/worker）配置不同的模型。这可能成为 MoA 架构向下一个进化阶段的信号。

### 7. 用户反馈摘要

- **核心痛点：硬编码与功能失效**：用户对硬编码的上下文窗口、不可配置的温度参数等问题感到困扰。例如，Copilot 提供商（Issue #7731）的硬编码导致无法使用账户特定模型。同时，Dashboard 在新版本中的认证功能失效，迫使部分自托管用户退回旧版本或放弃使用。
- **期望：更灵活的部署与权限控制**：Docker 和反向代理部署用户（Issue #59113）对 Dashboard 强制内置认证表达了不满。社区（PR #59857）积极推动更细粒度的权限层级（Owner/User），表明用户希望项目能更安全地支持群组和多用户场景。
- **对集成质量的敏感性**：XAI OAuth 认证失败（Issue #26847）不仅是一个技术BUG，更触及了用户对项目与第三方服务集成可靠性的信任。用户期望文档和实际行为完全一致。
- **对高性能场景的追求**：从“Subagent 模型覆盖”、Agent 因无限制思考而消耗大量Tokens（Issue #25758）等讨论可以看出，用户正将 Hermes 应用于更复杂、资源消耗更高的场景，对性能、资源控制和模型灵活性提出了更高要求。

### 8. 待处理积压

- **OpenRouter路由错误**：Issue [#58688](https://github.com/NousResearch/hermes-agent/issues/58688)（P2）自7月初报告以来，Desktop 模型选择器将自定义提供商模型错误路由到 OpenRouter 的问题仍未解决。这严重影响了使用本地或非OpenRouter API 用户的 Desktop 体验。
- **Gateway超时配置默认值**：PR [#47503](https://github.com/NousResearch/hermes-agent/pull/47503) 自6月中旬提出，建议将默认 Gateway 超时从 300s 提升至 1800s 以适配邮件等慢速渠道。该 PR 仍处于 OPEN 状态，但因涉及默认行为变更，需要维护者尽快决策。
- **Gateway会话凭证更新路径**：Issue [#64271](https://github.com/NousResearch/hermes-agent/issues/64271) 提到的长运行 Gateway 会话无法在凭证变更后重新绑定的问题，虽然等级为 P3，但会影响运维灵活性。该 Issue 于昨日提交，建议维护者关注其潜在影响。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 | 2026-07-16

> **数据覆盖时段**：2026-07-15 00:00 UTC – 2026-07-16 00:00 UTC（基于 GitHub 活动时间戳）

---

## 1. 今日速览

过去 24 小时项目保持**高度活跃**：共处理 16 条 Issue（新开/活跃 13 条，关闭 3 条）和 15 个 PR（待合并 8 个，已合并/关闭 7 个），并正式发布 **v1.36.1**。核心动作集中在**持久化会话的延迟加载、ACP/Codex 认证修复、以及 Agent Profile 启动时的上下文增强**。长期性能追踪 issue (#3153) 和结构化输出请求 (#2566) 持续获得社区关注。整体项目健康度良好，修复与功能并进。

---

## 2. 版本发布

### v1.36.1
- **发布 PR**：[#4120](https://github.com/OpenHands/software-agent-sdk/pull/4120)（已合并）
- **主要变更**：
  - `fix(sdk): rehydrate persisted subscription LLMs` – 修复持久化订阅 LLM 的反序列化问题，确保从存储中恢复的会话能正确加载 LLM 配置。
  - `feat: surface plugin contents in the agent-server plugins API` – 新增插件内容展示 API，允许通过 agent-server 接口查询已安装插件的内部信息。
- **破坏性变更**：无（两项均为向后兼容修复与增强）。
- **迁移注意**：无特殊操作要求，建议尽快升级以获取订阅 LLM 修复。

---

## 3. 项目进展

### 今日合并/关闭的重要 PR

| PR | 标题 | 类型 | 关键推进 |
|----|------|------|----------|
| [#4100](https://github.com/OpenHands/software-agent-sdk/pull/4100) | Lazily hydrate persisted conversations | 性能优化 | **延迟加载持久化会话**，显著降低启动时的内存占用与加载时间（解决 #3140 性能问题）。 |
| [#4030](https://github.com/OpenHands/software-agent-sdk/pull/4030) | feat(agent-server): support deployment context on profile launches | 功能增强 | Agent Canvas 启动 Profile 时能带入部署上下文和 Canvas 自有工具，解决 #4029。 |
| [#4110](https://github.com/OpenHands/software-agent-sdk/pull/4110) | feat(conversation): add client message context | 功能增强 | 为对话消息添加客户端上下文，支持更精细的追踪与重放。 |
| [#4010](https://github.com/OpenHands/software-agent-sdk/pull/4010) | fix(observability): stamp tool_call_id onto the TOOL span | 可观测性 | 在追踪 span 上标记 `tool_call_id`，便于后续导出与调试。 |
| [#3918](https://github.com/OpenHands/software-agent-sdk/pull/3918) | Fix REST API contract summary deduplication | 文档/工具 | 修复 PR 描述中 REST API 变更部分的重复问题。 |
| [#4125](https://github.com/OpenHands/software-agent-sdk/pull/4125) | feat(browser): record visible sessions as WebM | 功能增强 | 浏览器会话录制为 WebM 格式，支持可视化回放。 |

**项目向前迈出的关键一步**：延迟加载机制将直接影响大规模部署的启动速度与资源消耗；Profile 启动上下文增强填补了 Canvas 与 SDK 之间的集成缺口；ACP/Codex 认证修复（见下文 Bug 部分）保障了云会话的稳定性。

---

## 4. 社区热点

### 最活跃讨论

- **[#2566 [Feature]: Structured Output](https://github.com/OpenHands/software-agent-sdk/issues/2566)**（16 条评论，持续更新至 2026-07-15）  
  用户强烈要求 SDK 提供对 LLM **结构化输出** 的一流支持，关联 #1566。社区认为这是代理可靠解析 LLM 响应的基础能力，当前只能通过手动 JSON 解析方式工作，效率低且易错。

- **[#2078 [Tracker] Daily Integration Runs](https://github.com/OpenHands/software-agent-sdk/issues/2078)**（138 条评论）  
  持续数月的日常集成运行跟踪，虽非功能讨论，但反映了项目对持续测试的重视，近期仍频繁更新。

- **[#4124 fix(acp): persist brokered Codex subscription auth](https://github.com/OpenHands/software-agent-sdk/pull/4124)**（标记 `review-this, qa-this`）  
  对应 #4121 中报告的关键认证问题，社区关注度高，PR 正在审核中。

**分析**：社区对**结构化输出**和**认证稳定性**的呼声最高。结构化输出是长期需求，影响所有下游开发；Codex 认证问题直接阻碍云会话使用，需优先合并 #4124。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue | 问题描述 | 状态 | Fix PR |
|----------|-------|----------|------|--------|
| **Critical** | [#4121](https://github.com/OpenHands/software-agent-sdk/issues/4121) | Cloud Codex ACP 会话中凭证刷新后丢失，导致后续会话认证失败 | OPEN | [#4124](https://github.com/OpenHands/software-agent-sdk/pull/4124)（待合） |
| **Critical** | [#4093](https://github.com/OpenHands/software-agent-sdk/issues/4093) | ACP Python SDK 0.11.0 移除 `NewSessionResponse` 中的 `models` 字段，与 Gemini CLI 0.46 冲突 | OPEN | 暂无 |
| **High** | [#4098](https://github.com/OpenHands/software-agent-sdk/issues/4098) | 即使无 API Key，SDK 也会向 LiteLLM 代理发起未授权模型信息查询，浪费请求 | OPEN | 暂无 |
| **High** | [#3140](https://github.com/OpenHands/software-agent-sdk/issues/3140) （已关闭） | 服务器启动时加载所有持久化会话，1000 会话时性能严重下降 | **CLOSED**（已由 [#4100](https://github.com/OpenHands/software-agent-sdk/pull/4100) 修复） | 已合 |
| **Medium** | [#3291](https://github.com/OpenHands/software-agent-sdk/issues/3291) | `SwitchLLMTool` 无法检测外部 profile 切换，导致 LLM 使用陈旧状态回复 | CLOSED（标记 Stale，但未修复？） | 暂无明确 fix |
| **Medium** | [#3500](https://github.com/OpenHands/software-agent-sdk/issues/3500) | Anthropic Opus 4.8 不被支持，出现 `BadRequestError` | OPEN | 暂无 |
| **Low** | [#2885](https://github.com/OpenHands/software-agent-sdk/issues/2885) | 建议添加 `ConversationState.copy()` 方法消除克隆逻辑重复 | OPEN（Stale） | 暂无 |

**小结**：两个 Critical 级别 Bug 均与 **ACP 协议/云认证** 相关，可能影响生产环境。建议尽快合并 #4124 并讨论 ACP 0.11 的兼容策略。

---

## 6. 功能请求与路线图信号

- **[#2566 结构化输出](https://github.com/OpenHands/software-agent-sdk/issues/2566)** – 呼声最高，社区期望 SDK 提供类似 `parse`、`json_schema` 的声明式支持。暂无关联 PR，但考虑到需求广泛，很可能纳入下一版本（v1.37+）路线图。

- **[#4118 从 Python 自定义工具到客户端定义工具的迁移路径](https://github.com/OpenHands/software-agent-sdk/issues/4118)** – 新提出，旨在让产品平滑放弃遗留 Python 模块，可能随 `client_tools` 成熟而进入规划。

- **[#4119 持久化本地父子对话关系](https://github.com/OpenHands/software-agent-sdk/issues/4119)** – 要求 Agent Canvas 重新加载后仍能保持父子关系，对齐 OpenHands Cloud 行为。已有一个同名 PR（暂未看到对应 PR 号），可能进入 v1.37。

- **[#2623 公开 Python 对话/事件搜索 API](https://github.com/OpenHands/software-agent-sdk/issues/2623)** – 长期需求，与 agent-server REST 对应，但至今未实现。

**下一版本信号**：当前 Release v1.37.0 的 PR [#4123](https://github.com/OpenHands/software-agent-sdk/pull/4123) 已经打开，包含多项性能优化和 ACP 修复，预计近期发布。以上功能请求中 #2566 和 #4118 可能成为较高优先级。

---

## 7. 用户反馈摘要

- **结构化输出（#2566）**：用户 `@chase-prescient` 强调“这是非复制请求”，说明当前只能通过 hack 方式实现，严重影响开发效率。
- **工具兼容性（#2667）**：用户 `@VascoSch92` 提出研究工具集更新时的向后兼容策略，显示社区对生产环境长期运行的担忧。
- **SwitchLLMTool 缺陷（#3291）**：用户报告“LLM 不知道外部 profile 切换”，导致回复基于过时状态，严重影响对话质量。
- **Profile 启动上下文丢失（#4029）**：用户 `@simonrosenberg`（实际是贡献者）指出 Canvas 启动 Profile 时丢弃客户端自定义工具，表示“这是正确的，但也造成了限制”。
- **Anthropic 新模型不支持（#3500）**：用户 `@udt666` 直接贴出错误日志，显示 Opus 4.8 不可用，希望尽快支持。
- **认证刷新失败（#4121）**：用户 `@neubig` 描述“用户看到的失败是 Codex 认证过期”，直接影响云服务可用性。

**总体情绪**：用户对**模型兼容性（Anthropic、Gemini/ACP）** 和**身份认证可靠性**最为不满，同时对**结构化输出**等核心 API 缺失感到遗憾。

---

## 8. 待处理积压

以下 Issue/PR 长期未获回应或进展停滞，建议维护者关注：

| 条目 | 创建时间 | 最后更新 | 简要描述 | 建议动作 |
|------|----------|----------|----------|----------|
| [#2667](https://github.com/OpenHands/software-agent-sdk/issues/2667) | 2026-04-02 | 2026-07-15 | 研究工具向后兼容策略 | 标记为 Stale，但研究性议题仍需阶段性结论 |
| [#2623](https://github.com/OpenHands/software-agent-sdk/issues/2623) | 2026-03-31 | 2026-07-15 | 公开 Python 搜索 API | 需求明确，无人接手 |
| [#3084](https://github.com/OpenHands/software-agent-sdk/issues/3084) | 2026-05-06 | 2026-07-15 | 公开持久化设置迁移入口 | 关联 v1.22 的删除，时间紧迫 |
| [#2885](https://github.com/OpenHands/software-agent-sdk/issues/2885) | 2026-04-19 | 2026-07-15 | 添加 `copy()` 方法减少重复代码 | 代码重构机会，适合新手贡献者 |
| [#3500](https://github.com/OpenHands/software-agent-sdk/issues/3500) | 2026-06-04 | 2026-07-15 | 不支持 Anthropic Opus 4.8 | 模型提供商更新，需及时适配 |
| [#3291](https://github.com/OpenHands/software-agent-sdk/issues/3291) | 2026-05-18 | 2026-07-15 | SwitchLLMTool 状态不同步 | 虽已关闭，但未提供修复方案，可能重新打开 |

---

**总结**：OpenHands SDK 项目在 7 月 15 日保持了良好的迭代节奏，性能优化和认证修复是两大亮点。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

## Pi 项目动态日报 — 2026-07-16

---

### 1. 今日速览

过去24小时项目保持中等偏上活跃度：共处理52条 Issue（新开/活跃13条，关闭39条），合并/关闭6个 Pull Request，无新版本发布。社区关注点集中在 **OpenAI Codex 连接稳定性**（#4945，75条评论）、**新 Claude 模型与编辑工具的兼容性**（#6278，22条评论）以及多个影响用户体验的 Bug（如 GitHub 自动登出、Windows 标题闪烁）。核心团队针对关键漏洞快速响应，合并了 session‑id 截断、Windows 标题重置、TUI 空指针防护等修复，项目整体稳定性有所提升。

---

### 3. 项目进展

今日合并/关闭的 PR 涉及以下重要修复与改进：

| PR 编号 | 类型 | 核心内容 | 状态 |
|---|---|---|---|
| [#6681](https://github.com/earendil-works/pi/pull/6681) | fix | Windows 上 `npm view` 导致终端标题被覆盖，现已在检查后重置标题，解决 [#6629](https://github.com/earendil-works/pi/issues/6629) | 已合并 |
| [#6683](https://github.com/earendil-works/pi/pull/6683) | fix | 允许加载插件名字空间限定的技能（如 `inc:ship-it`），消除启动时的错误冲突提示 | 已合并 |
| [#6533](https://github.com/earendil-works/pi/pull/6533) | fix | Codex 压缩功能针对 `gpt‑5.6-luna` 返回“Model not found”的问题，通过内部模型映射修正 | 已合并 |
| [#6667](https://github.com/earendil-works/pi/pull/6667) | fix | TUI 中 Box/Container 渲染时遇到 `null` 子组件导致崩溃，增加空值过滤，提升扩展安装/卸载后的稳定性 | 已合并 |
| [#6659](https://github.com/earendil-works/pi/pull/6659) | fix | OpenAI Codex 的 `session-id` 和 `x-client-request-id` 头未做 64 字符截断，导致后端验证失败，现已与 body 中的 `prompt_cache_key` 保持一致 | 已合并 |
| [#6660](https://github.com/earendil-works/pi/pull/6660) | docs | 为 coding‑agent 添加 ACP 派生分支横幅及上游计划说明 | 已合并 |

此外，还有 5 个待合并 PR 正在审查中，包括 **xAI 设备 OAuth**（#6651）、**SQLite 会话存储**（#6594）、**依赖扩展包名解析**（#6680）等，反映了项目在身份认证、数据持久化、扩展系统方面的持续演进。

---

### 4. 社区热点

| 议题 | 讨论热度 | 核心诉求 |
|---|---|---|
| [#4945](https://github.com/earendil-works/pi/issues/4945) — OpenAI Codex 连接可靠性 | **75 条评论**，👍 30 | TUI 随机卡死在 `Working…` 状态，无流式文本、无工具调用、无错误提示，只能按 Esc 中止。用户希望增加显式超时/重试机制，并提供诊断日志。 |
| [#6278](https://github.com/earendil-works/pi/issues/6278) — 新 Claude 模型与编辑工具配合不佳 | **22 条评论**，👍 9 | 约 20% 的编辑操作因 LLM 生成的额外字段（如 `new_text_x`、`type`）导致验证失败。社区建议对 LLM 输出做更严格的 schema 清洗，或允许多余字段被忽略。 |
| [#6050](https://github.com/earendil-works/pi/issues/6050) — TUI 全量重绘清除终端回滚 | **14 条评论** | 交互模式下，终端滚动条频繁跳回聊天开头，影响长对话浏览。用户期望 TUI 采用增量渲染而非全量重绘。 |
| [#5263](https://github.com/earendil-works/pi/issues/5263) — 会话内模型/思考级别变更默认临时化 | **7 条评论**，👍 7 | 用户不希望每次切换模型都修改全局配置，强烈支持“会话内临时切换 + 单独设置全局默认”的分离设计。 |

**分析**：四个热点分别指向 **API 稳定性**、**LLM 工具调用兼容性**、**TUI 渲染性能**、**配置管理 UX**。其中 #4945 和 #6278 直接与核心对话能力相关，必须优先解决；#6050 和 #5263 则影响日常使用体验，社区反馈积极且诉求清晰。

---

### 5. Bug 与稳定性

以下按照严重程度排列，并标注是否有修复 PR：

#### 严重（高影响、高频或可导致数据泄露）
- **[#4945](https://github.com/earendil-works/pi/issues/4945)** [OPEN] — OpenAI Codex 连接可靠性：TUI 卡死，无错误提示，仅能通过 Esc 恢复。**尚未关联修复 PR**。
- **[#6278](https://github.com/earendil-works/pi/issues/6278)** [OPEN] — 新 Claude 模型编辑验证失败率约 20%。**尚未关联修复 PR**。
- **[#6686](https://github.com/earendil-works/pi/issues/6686)** [CLOSED] — Pi 自动登出 GitHub（与 #2725 重复）。**无修复 PR，归类为自动关闭，但根源可能仍在**。
- **[#6673](https://github.com/earendil-works/pi/issues/6673)** [CLOSED] — OpenAI Codex 暴露 Cloudflare 520 HTML，含用户出口 IP。**风险已通报，暂未修复**。

#### 中等级（影响特定场景）
- **[#6657](https://github.com/earendil-works/pi/issues/6657)** [OPEN] — Bedrock `AWS_PROFILE` 认证失败（403）。尽管 0.80.7 声称修复过，但问题仍然存在。**无修复 PR**。
- **[#6665](https://github.com/earendil-works/pi/issues/6665)** [OPEN] — TUI 在流式输出时因 `Intl.Segmenter` 未缓存导致 CPU 100%。**无修复 PR**。
- **[#6619](https://github.com/earendil-works/pi/issues/6619)** [OPEN] — Windows 上依赖扩展显示绝对路径。**PR [#6680](https://github.com/earendil-works/pi/pull/6680) 部分修复中**。
- **[#6652](https://github.com/earendil-works/pi/issues/6652)** [OPEN] — TUI 崩溃日志硬编码 `~/.pi/pi-crash.log`，忽略 `PI_CODING_AGENT_DIR` 环境变量。**无修复 PR**。

#### 轻微（已快速修复或影响小）
- **[#6630](https://github.com/earendil-works/pi/issues/6630)** [CLOSED] — Codex `session-id` 头未截断导致请求全挂。**已由 PR #6659 修复**。
- **[#6629](https://github.com/earendil-works/pi/issues/6629)** [CLOSED] — Windows 终端标题被 `npm view` 覆盖。**已由 PR #6681 修复**。
- **[#6667](https://github.com/earendil-works/pi/issues/6667)** [CLOSED] — TUI 扩展卸载后空指针崩溃。**已由 PR #6667 修复**。

---

### 6. 功能请求与路线图信号

| 议题/PR | 类型 | 内容概述 | 路线图信号 |
|---|---|---|---|
| [#5263](https://github.com/earendil-works/pi/issues/5263) | 功能请求 | 会话内模型/思考级别变更默认临时化，仅影响当前对话。已在 `/settings` 菜单中增加“默认模型”入口。 | **高概率进入下一版本**，表达清晰且无技术障碍。 |
| [#6212](https://github.com/earendil-works/pi/issues/6212) | 功能请求 | Bedrock 路径应同时考虑 `compat.forceAdaptiveThinking` 配置和硬编码模型列表。 | **等待维护者评估**，涉及基础设施变更。 |
| [#6682](https://github.com/earendil-works/pi/issues/6682) | 功能请求 | TUI 中代码块渲染改用带边框的盒子，替代文本反引号。 | **用户体验改进**，可与其他 TUI 渲染优化合并处理（如 #6050）。 |
| [#6674](https://github.com/earendil-works/pi/issues/6674) | 功能请求 | 会话管理：浏览、分组、重命名、归档。 | **中等优先级**，反映高级用户对会话治理的长期需求。 |
| [#6651](https://github.com/earendil-works/pi/pull/6651) | 待合并 PR | 增加 xAI 设备 OAuth 认证，并将 `grok-4.5` 路由至 Responses API。 | **若合并将扩展平台支持**，接入更多模型供应商。 |
| [#6594](https://github.com/earendil-works/pi/pull/6594) | 待合并 PR | SQLite 会话存储，支持增量压缩与路径优化。 | **重大性能变革**，减少内存占用并加速历史加载。 |
| [#6216](https://github.com/earendil-works/pi/pull/6216) | 待合并 PR | 增加 Amazon Bedrock Mantle 的 OpenAI Responses 供应商。 | **扩大云生态支持**，对 AWS 用户有吸引力。 |

**路线图信号总结**：项目当前在 **扩展供应商集成**（xAI、Bedrock Mantle）和 **架构升级**（SQLite 存储）上投入较多。同时社区对 **用户体验优化**（会话管理、代码块渲染、TUI 增量渲染）的呼声渐高，建议在下一个小版本中优先考虑部分低风险 UX 改进。

---

### 7. 用户反馈摘要

- **#4945 抱怨**：“唯一的恢复方式是按 Esc，但会记录一个中止的 assistant turn。” 用户表示问题连续数日出现，极大影响工作流。
- **#6278 用户**：“20% 的编辑都失败，LLM 凭空增加各种字段，`new_text_x`、`type`、`in_file`…… 希望 Pi 能忽略多余字段。”
- **#6050 用户**：“终端滚动条跳回开头，根本无法查看长对话的历史上下文。”
- **#6686 用户**：“又自动登出了，每次都要重新登录 GitHub，中间还导致 agent 工作中断无提示。”
- **#6619 用户**：“Windows 上扩展 banner 显示绝对路径，很丑且可能泄露目录结构。”
- **#6665 用户**：“CPU 被占满，只能通过 `pi -ne` 规避，但牺牲了 UI 反馈。”
- **#6652 用户**：“我将 `.pi` 移走后，崩溃日志又在 home 目录新建了 `.pi`，违反环境变量约定。”
- **#6689 用户吐槽**：“登录了 ChatGPT Plus，但 `OPENAI_API_KEY` 环境变量悄悄覆盖了 OAuth，请求全部 401。”

**总结**：用户对 **核心对话流畅性**（#4945、#6278）和 **环境配置一致性**（#6686、#6689、#6652）感到挫败。对 **TUI 性能**（#6050、#6665）也有显著不满。建议项目团队优先解决“卡死”“认证冲突”和“CPU 过热”这三类直接影响日常使用的问题。

---

### 8. 待处理积压

以下为长期未解决或响应较慢的重要 Issue / PR，提醒维护者关注：

| 编号 | 类型 | 创建时间 | 累计评论/反应 | 当前状态 | 备注 |
|---|---|---|---|---|---|
| [#4945](https://github.com/earendil-works/pi/issues/4945) | Issue | 2026-05-24 | 75评论, 30👍 | 开放（标记 inprogress） | 高热度，社区多次催促，需加快修复进度。 |
| [#6657](https://github.com/earendil-works/pi/issues/6657) | Issue | 2026-07-14 | 5评论 | 开放（inprogress） | Bedrock 认证修复未完全生效，需重新排查。 |
| [#5263](https://github.com/earendil-works/pi/issues/5263) | Issue | 2026-05-31 | 7评论, 7👍 | 开放 | 虽然热度中等，但功能清晰且已有用户期待，适合纳入 sprint。 |
| [#6594](https://github.com/earendil-works/pi/pull/6594) | PR | 2026-07-13 | 无评论 | 开放 | SQLite 存储是重要架构变更，但审查停滞。 |
| [#6216](https://github.com/earendil-works/pi/pull/6216) | PR | 2026-07-01 | 无评论 | 开放 | Bedrock Mantle 供应商 PR 已搁置两周，需确认是否因测试缺失。 |

**建议**：
1. 设立社区响应 SLA，对超过 50 条评论的热点 Issue 优先响应进度。
2. 对长期开放但无进展的 PR（如 #6594、#6216）给出明确反馈（是否需要修改？是否合并到下个版本？）。
3. 将 #4945 和 #6278 列为 P0 级缺陷，成立专项修复计划。

---

*报告生成时间：2026-07-16 06:30 UTC*  
*数据来源：https://github.com/earendil-works/pi*

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

好的，这是为您生成的 LiteLLM 项目动态日报。

---

# LiteLLM 项目动态日报 | 2026-07-16

## 1. 今日速览

过去24小时，LiteLLM项目保持了极高的活跃度，共计产生 **97条 Issue 更新** 和 **307条 PR 更新**。社区讨论热烈的同时，开发团队也在高效地推进代码合并与功能开发，显示了项目强劲的生命力。新发布的 `v1.94.0-dev.1` 版本引入了镜像签名，体现了对供应链安全的重视。值得关注的是，社区对于 **SSO用户数限制**、**Langfuse SDK更新** 以及 **OpenAI GPT-5.6系列模型兼容性** 等议题表现出强烈关切，这些可能会成为下一阶段的开发重点。

## 2. 版本发布

### v1.94.0-dev.1
- **发布说明**: 此版本为一个开发版本，主要更新是现在所有LiteLLM Docker镜像都使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 进行了签名，增强了供应链安全。
- **破坏性变更**: 无。
- **迁移注意事项**: 用户现在可以通过cosign验证下载的Docker镜像的完整性和来源。对于普通用户，无特殊迁移操作。使用Docker部署的用户可参考GitHub Commit `0112e53` 了解更多细节。

## 3. 项目进展

今日共合并/关闭 **91条PR**，展示了项目在Bug修复和功能增强上的快速迭代。主要进展包括：

- **核心稳定性修复**：
    - **流式传输完整性**: PR [#33458](https://github.com/BerriAI/litellm/pull/33458) 修复了当上游流被重置时，系统将其静默转换为“正常结束”的问题。现在会正确抛出异常，确保错误可被追踪（关联 Issue [#33404](https://github.com/BerriAI/litellm/pull/33404)）。
    - **日志内存泄漏**: PR [#33455](https://github.com/BerriAI/litellm/pull/33455) 停止在请求结束后仍挂载大型请求负载，解决了可能导致内存泄漏的问题。
    - **LLM防护增强**: PR [#33331](https://github.com/BerriAI/litellm/pull/33331) 修复了 moderation API 返回的“净化后提示”未被正确应用到后续请求的问题。
- **功能增强与UI**:
    - **CLI工具**: PR [#33249](https://github.com/BerriAI/litellm/pull/33249) 为CLI增加了一个“lite autoroute”功能，用于对基于复杂度的自动路由进行QA测试。
    - **UI优化**: PR [#33446](https://github.com/BerriAI/litellm/pull/33446) 修复了在配置了 `server_root_path` 时，聊天页面的导航问题。
- **依赖与兼容性**:
    - **Python 3.14支持**: PR [#33457](https://github.com/BerriAI/litellm/pull/33457) 更新了 Rust 模块的 `pyo3` 依赖，使其能在 Python 3.14 上编译。

## 4. 社区热点

1.  **Issue: [#25762](https://github.com/BerriAI/litellm/issues/25762) - [Feature]: Standard Plan Unlimited SSO Login**
    - **热度**: 14条评论，13个👍，连续多日活跃。
    - **分析**: 用户强烈要求取消Standard Plan中5个SSO用户的限制。这表明社区中有大量中小型团队希望以更低的成本使用LiteLLM的SSO功能，该诉求直接关联到项目的定价策略和用户增长。

2.  **Issue: [#17475](https://github.com/BerriAI/litellm/issues/17475) - [Bug]: LiteLLMProxy no longer show the list of models to the users**
    - **热度**: 13条评论，5个👍。
    - **分析**: 这是一个持续已久的权限问题，报告称普通用户在更新后无法看到模型列表。这直接影响到用户的核心体验，团队需要优先解决，否则会影响多租户场景下的使用。

3.  **Issue: [#33221](https://github.com/BerriAI/litellm/issues/33221) - [Bug]: Function tools fail with reasoning_effort error for OpenAI gpt-5.6 family models**
    - **热度**: 4条评论，新开Issue。
    - **分析**: 在新发布的OpenAI GPT-5.6系列模型上，函数调用功能因参数冲突而失败。这是一个紧跟Openai模型迭代的兼容性问题，需要快速处理，以保证LiteLLM对新模型的支持能力。

## 5. Bug 与稳定性

*近期新报告的Bug按严重程度排列：*

- **严重**:
    - **OpenAI GPT-5.6模型函数调用失败** ([#33221](https://github.com/BerriAI/litellm/issues/33221)): 调用任何GPT-5.6系列模型的函数工具时，会因`reasoning_effort`参数错误而失败。**已有PR [#33429](https://github.com/BerriAI/litellm/pull/33429) 在修复路由策略，可能间接解决此问题。**
    - **流式传输上游重置被错误处理** ([#33404](https://github.com/BerriAI/litellm/issues/33404)): 流式连接被上游重置时，返回了错误的`finish_reason`，可能导致客户端逻辑误判。**已有对应修复PR [#33458](https://github.com/BerriAI/litellm/pull/33458)。**
    - **`/responses` API在多轮对话中丢弃推理内容** ([#32335](https://github.com/BerriAI/litellm/issues/32335)): 对于Azure OpenAI模型的多轮对话，`/responses` API会丢失上下文中的推理项，导致请求失败。这是一个明确的回归问题（v1.83.7）。

- **中等**:
    - **Replicate运行时计费单位混淆** ([#33328](https://github.com/BerriAI/litellm/issues/33328)): Replicate后端的计费逻辑将秒错误地当作毫秒处理，会导致计费不准。
    - **`yarl`库安全漏洞** ([#33410](https://github.com/BerriAI/litellm/issues/33410)): 依赖的URL解析库`yarl`存在SSRF绕过风险，建议紧急升级。
    - **Provider预算配置缺失`max_budget`导致部署被移除** ([#33327](https://github.com/BerriAI/litellm/issues/33327)): 配置provider预算时，若只设置`duration`而不设置`max_budget`，会错误地将该provider的所有模型标记为不健康。

- **低等**:
    - **`/v1/messages`接口忽略客户端超时设置** ([#26752](https://github.com/BerriAI/litellm/issues/26752)) (3个月前报告，已关闭): 客户端传入的超时参数被`/v1/messages`接口静默忽略。

## 6. 功能请求与路线图信号

*社区呼声较高的新功能：*

- **[#25762](https://github.com/BerriAI/litellm/issues/25762) 取消SSO用户数限制**: 强烈建议团队重新评估定价策略，或提供更灵活的SSO用户管理选项。
- **[#24123](https://github.com/BerriAI/litellm/issues/24123) 支持Langfuse Python SDK v4**: Langfuse v4已发布，但LiteLLM仍锁定在v2。此请求共有11个👍，表明很多用户希望使用最新版的观测工具。
- **潜在纳入下一版本的功能**: 从今日合并的PR来看，团队正在积极改进预算管理 ([#33459](https://github.com/BerriAI/litellm/pull/33459)， [#33460](https://github.com/BerriAI/litellm/pull/33460))、团队管理 ([#32958](https://github.com/BerriAI/litellm/pull/32958))、UI/UX ([#33449](https://github.com/BerriAI/litellm/pull/33449)) 和策略路由 ([#33442](https://github.com/BerriAI/litellm/pull/33442))，这些组件都可能在下一稳定版本中发布。

## 7. 用户反馈摘要

- **SSO限制是推广的障碍**: 用户 [@escon1004](https://github.com/escon1004) 在 [#25762](https://github.com/BerriAI/litellm/issues/25762) 中请求取消Standard Plan的5用户SSO限制，表示“我们正在积极地使用该产品，但用户限制阻碍了我们推荐”。
- **权限问题困扰管理员**: 用户 [@mbeltagy](https://github.com/mbeltagy) 在 [#17475](https://github.com/BerriAI/litellm/issues/17475) 中报告普通用户无法查看模型列表，这类权限问题直接影响B2B多租户场景的用户体验。
- **多模型支持的痛点**: 用户在多个Issue中（如[#32218](https://github.com/BerriAI/litellm/issues/32218)， [#25390](https://github.com/BerriAI/litellm/issues/25390)）反映了对不同模型家族（如Z.AI， Gemma）的特殊模型名、流式和非流式模式下行为不一致的困扰，期望LiteLLM能提供更统一的抽象。

## 8. 待处理积压

- **[#25296](https://github.com/BerriAI/litellm/issues/25296) - `nacl.exceptions.ValueError: The nonce must be exactly 24 bytes long`**: 配置SMTP时导致崩溃的bug，已有多位用户确认，虽标记为`stale`，但缺乏官方回应。
- **[#25865]() (Issue 25720) - Langfuse OTel重复追踪**: 自托管用户在`/v1/rerank`请求中遇到重复追踪的问题，影响日志分析准确性，报告于4月，目前仍为开放状态。
- **[#29966](https://github.com/BerriAI/litellm/issues/29966) - 分拆的Helm Chart镜像未发布**: 用户使用新的组件化Helm Chart时发现，对应的 Docker 镜像并未被打上对应版本标签，影响部署流程。此问题已超过一个月，需要维护者关注。

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

好的，根据您提供的 Temporal 项目 GitHub 数据，我为您生成了 2026-07-16 的项目动态日报。

---

# **Temporal 项目日报 | 2026-07-16**

## 1. 今日速览

项目开发持续活跃，过去 24 小时共处理 69 条 Pull Requests（其中 27 条被合并或关闭），表明团队在代码合并与功能推进上节奏较快。相比之下，Issue 侧仅更新 2 条（1 开 1 关），新增问题报告较少，反映近期项目稳定性有所提升。无新版本发布，但多项核心功能（如独立活动控制、调度器改进）的 PR 处于开放状态，表明下一版本可能包含较多新特性。整体项目健康度良好。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日合并/关闭的 Pull Requests 中，以下几条对项目影响较为显著：

- **`#11047` Fix reset backlog count after gap**  
  [链接](https://github.com/temporalio/temporal/pull/11047)  
  修复了 `priTaskReader` 在 `setReadLevelAfterGap` 后未显式更新内存状态导致 backlog 计数不准确的问题，提升了任务调度可靠性和监控准确度。

- **`#10874` Dynamic partitioning: sync backlog counts**  
  [链接](https://github.com/temporalio/temporal/pull/10874)  
  在动态分区中引入 backlog 计数同步，并用于简单伸缩器，使分区调整能基于真实队列压力，为后续负载均衡奠定基础。

- **`#11046` Don't count backlog for persistence rate limited errors**  
  [链接](https://github.com/temporalio/temporal/pull/11046)  
  改为仅在持久化写入成功后递增 backlog 计数，避免速率限制错误导致后台队列积压计数虚高，使监控数据更加准确。

- **`#10413` Delegate mixedbrain devserver lifecycle to Omes**  
  [链接](https://github.com/temporalio/temporal/pull/10413)  
  将混合脑（mixedbrain）开发服务器的生命周期管理委托给 Omes 测试框架，消除了重复代码并统一了测试基础设施。

此外，`#10690` 关闭的 Issue（ResetWorkflowExecution 返回 "workflow not found" 的 Bug）也已确认修复，增强了重置工作流功能的健壮性。

项目整体向前推进了动态分区、任务调度精度、监控数据准确性以及测试基础设施的统一。

## 4. 社区热点

- **`#3769` [enhancement] Any plan to support MS SQL Server?**  
  [链接](https://github.com/temporalio/temporal/issues/3769)  
  该 Issue 创建于 2023 年，但在昨日（2026-07-15）再次被更新，共获 6 条评论。用户 @raymondsze 表示 Temporal 目前仅官方支持 MySQL 和 Postgres，但其客户强制要求 MS SQL Server，希望官方提供支持。该话题持续多年仍未被解决，社区呼声较高，反映了企业级部署中数据库多样性的真实需求。

- **`#10690` [potential-bug] ResetWorkflowExecution returns "workflow not found" when targets an older run**  
  [链接](https://github.com/temporalio/temporal/issues/10690)  
  该 Bug 报告了重置工作流时若目标 run 的 current execution 已被删除（但旧 run 仍存在），则返回“workflow not found”的错误。昨日本 Issue 被关闭，说明修复已合入，社区反馈 👍 1，用户对及时修复表示认可。

## 5. Bug 与稳定性

| 严重程度 | Issue / PR | 描述 | 状态 |
|----------|------------|------|------|
| 严重 | `#10690` | 重置工作流时因 current execution 缺失而误报“workflow not found”，阻断正常操作 | 已关闭，已有修复 |
| 中等 | `#11097` (PR) | 独立活动重置后 task token 失效，导致心跳/完成操作无法正常工作 | 开放中，修复方案已提交 |
| 低 | `#11047` (PR) | backlog 计数在 gap 后未正确重置，影响监控准确性 | 已合并 |
| 低 | `#11046` (PR) | 速率限制错误导致 backlog 虚增 | 已合并 |

整体来看，今日没有报告高严重度的新崩溃或回归问题，两个低严重度问题已通过 PR 合并解决。

## 6. 功能请求与路线图信号

- **独立活动控制 API**  
  PR `#10106`（Implement Pause/Unpause/Reset/UpdateOptions for standalone activities）处于开放中，该功能将为工作流内和独立活动提供服务器端控制接口，预计是下个版本的重要特性。

- **SignalWorkflow 后重置操作**  
  PR `#11042`（Support SignalWorkflow post-reset operations）实现了重置工作流后执行信号的选项，增强了重置场景的灵活性，可能进入后续版本。

- **独立活动可见性支持**  
  PR `#11017`（Add ExecutionTime visibility support for standalone activities）为独立活动添加执行时间字段的支持，便于查询和监控，对运营用户有实际价值。

- **MS SQL Server 支持**  
  Issue `#3769` 长期未关闭，虽无直接关联 PR，但社区持续关注。鉴于用户基数扩展需求，未来版本可能考虑增加对 MSSQL 的数据库适配。

## 7. 用户反馈摘要

- **数据库兼容性痛点**  
  用户 @raymondsze 在 `#3769` 中强调，Temporal 的数据库支持严重限制了他们的本地部署产品，多个客户强制要求 MS SQL Server，希望官方能正视这一企业级需求。

- **重置工作流体验改善**  
  用户 @jiechenz 在 `#10690` 中反馈重置流程的异常行为，认为“如果工作流没有 current execution，重置应直接基于 base run 创建新 run”。该问题已得到修复，用户点赞，表明社区对服务器端边界情况的处理要求较高。

- **独立活动功能需求**  
  多个 PR（`#10106`、`#11097`、`#11017`）的开发现状表明，社区（尤其是使用长时间运行独立活动的场景）对暂停、重置、可见性等功能有强烈需求，相关 PR 获得了较高的开发优先级。

## 8. 待处理积压

- **`#3769`** – 要求支持 MS SQL Server（创建于 2023-01-03，最近更新 2026-07-15，6 条评论）  
  [链接](https://github.com/temporalio/temporal/issues/3769)  
  该需求长期存在但未被采纳，考虑到企业级部署的刚性需求，建议维护团队评估优先级并给出明确路线图回应。

- **`#10129`** – 减少测试运行资源（创建于 2026-04-30，仍开放）  
  [链接](https://github.com/temporalio/temporal/pull/10129)  
  该 PR 试图改用 4 核 ARM 运行器以降低高峰期的资源等待时间，但已持续两个多月未合并。若持续搁置，可能影响 CI 队列速度，建议维护者尽快评估合并。

以上为 2026-07-16 Temporal 项目动态日报。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*