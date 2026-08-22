# OpenClaw 生态日报 2026-08-23

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-22 22:42 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-23

> 数据窗口：过去 24 小时 | 数据来源：github.com/openclaw/openclaw

## 1. 今日速览

过去 24 小时项目保持极高度活跃：共处理 500 条 Issue 更新（其中 480 条新开/活跃、20 条关闭）和 500 条 PR 更新（其中 427 条待合并、73 条已合并/关闭），表明社区参与度和维护者响应频率均处于高位。但需注意两大健康度隐患：其一，大量 P1/P2 Issue 长期停留在 `needs-maintainer-review` / `needs-product-decision` 状态，维护者评审积压明显；其二，两个 P0 级稳定性 Bug（事件循环阻塞、SQLite 损坏）正在影响 beta 版本用户，暂无修复 PR，项目健康度面临挑战。当日无新版本发布，但有多项重要 PR 等待维护者审阅，预示着下一补丁版本可能包含安全、UI 和稳定性方面的修复。

## 2. 版本发布

本期无新版本发布。

---

## 3. 项目进展

过去 24 小时有 73 条 PR 被合并或关闭。在展示的 PR 中，以下几项已关闭并代表了项目的重要推进：

### 安全与合规
- **[feat(security): require acknowledgement for install policy warnings](https://github.com/openclaw/openclaw/pull/116489)**（#116489，已关闭）
  安全安装策略新增 `warn` 返回模式：当插件/技能安装存在风险时，CLI 交互式安装将展示受限原因与发现，并要求操作者输入精确目标名称以确认继续。这是对安装供应链安全的重要加固。
- **[feat(ui): review install policy warnings](https://github.com/openclaw/openclaw/pull/120900)**（#120900，已关闭）
  作为上述 CLI 改动的 Control UI 配套，允许已认证管理员在 Web 界面审阅安装策略警告并显式确认继续。两项合并意味着安装策略警告从“仅提示”升级为“需明确确认”的双端闭环。

### 多通道与会话修复
- **[fix(gateway): keep conversation delivery within agent bindings](https://github.com/openclaw/openclaw/pull/126424)**（#126424，已关闭）
  修复多 agent 运维场景下，会话投递工具可绕过 agent 绑定的问题，影响 Discord、Telegram、Slack、Feishu 等全部主流渠道。合并该 PR 后，消息投递将严格限定在 agent 所属绑定的对话范围内。

### 模型与认证
- **[fix(models): keep Claude CLI OAuth available in Control UI](https://github.com/openclaw/openclaw/pull/125471)**（#125471，已关闭）
  解决 Gateway 重启后 Claude CLI OAuth 因历史 `auth.profiles` 条目冲突而丢失刷新所有权、并在 UI 中显示为“missing”的问题。对依赖 Claude CLI OAuth 的生产用户是一项关键修复。

### 等待维护者关注（ready for maintainer look）
以下高优先级 PR 已由提交者标记为“待维护者审阅”，建议优先处理：
- [#127713 fix: macOS onboarding waits for Gateway restart](https://github.com/openclaw/openclaw/pull/127713)（P1，macOS 新用户激活流程修复）
- [#128048 perf(cron): skip history checks for future jobs](https://github.com/openclaw/openclaw/pull/128048)（P3，Cron 调度性能优化）
- [#127231 fix(exec): isolate background result retention per process](https://github.com/openclaw/openclaw/pull/127231)（P2，后台进程结果保留隔离）
- [#120491 feat(tools): per-turn per-target send budget guard for message tools](https://github.com/openclaw/openclaw/pull/120491)（P1，消息工具发送预算防护）

---

## 4. 社区热点

### 最热 Issue：Release validation v2026.8.1-beta.2
- **[#125626 Release validation: v2026.8.1-beta.2](https://github.com/openclaw/openclaw/issues/125626)**（评论 19 条，维护者发起）
  这是官方发起的 beta 发布验证流程，要求每位测试者按 worksheet 完成一次真实 Gateway 升级验证并追加评论。高热度说明社区正集中测试 v2026.8.1-beta.2，但结合下述多个 beta 相关 Bug（#124788、#126821、#124284），验证流程本身也暴露了 beta 的稳定性短板。

### 社区反馈最强：流式看门狗超时阈值不可配置
- **[#68596 Feature Request: Configurable streaming watchdog timeout threshold](https://github.com/openclaw/openclaw/issues/68596)**（评论 15 条，👍 8 个）
  用户使用 Kimi-K2.5、DeepSeek-R1 等长思考模型时频繁触发 `streaming watchdog: no stream updates for 30s; resetting status` 警告。该 Issue 自 4 月 18 日创建以来持续活跃，积累了 8 个 👍，但一直滞留在 `needs-product-decision` 状态。这是推理模型的“慢思考”特性与固定 30 秒看门狗设计之间的根本矛盾。

### 高讨论量 Bug：WhatsApp 图片消息阻塞
- **[#96834 WhatsApp 1:1: inbound image wedges main lane ~3min](https://github.com/openclaw/openclaw/issues/96834)**（评论 14 条，👍 1 个）
  发送图片后消息通道被卡住约 3 分钟才被处理，导致多模态运行卡在 `active_reply_work` / `queued_work_without_active_run` 状态。该问题被标记为 `🐚 platinum hermit` 高影响评级，且在 6 月 10 日可复现。

### 值得关注的 PR：Composer 支持向后台会话发送提示
- **[#128050 feat(ui): send composer prompts to background sessions](https://github.com/openclaw/openclaw/pull/128050)**（AI-assisted，开放中）
  由 `@clawsweeper` 提交，允许用户在 Control UI 的 Composer 中直接向后台会话发送任务，无需切换会话。关闭 #128037，并关联多个历史 Issue（#80901、#81946、#84827、#123247），可能是 UI 工作流的重要改进，但目前仍在开放状态。

---

## 5. Bug 与稳定性

### 🔴 P0：影响面大、暂无修复 PR

- **[#124788 beta.2 gateway: event loop blocks ~100s every ~10 min](https://github.com/openclaw/openclaw/issues/124788)**（P0，更新于 8-22）
  v2026.8.1-beta.2 的 Gateway 每 ~10.9 分钟事件循环阻塞 100–120 秒，导致 WebSocket 断连、HTTP `/ready` 无响应、Cron 停摆。即使禁用全部记忆插件仍复现。当前无修复 PR。
- **[#126821 SQLite corruption recurs on pristine rebuilt DBs within 15–24h](https://github.com/openclaw/openclaw/issues/126821)**（P0，更新于 8-22）
  2026.8.1-beta.2 + WSL2 环境，重建后的干净 SQLite 在 15–24 小时内出现 freelist miscount，并伴随“gateway 瘫痪但进程不退出”的异常模式。5 天内发生 5 起。当前无修复 PR。

### 🟠 P1：高影响

| Issue | 问题 | 影响 | Fix PR |
|---|---|---|---|
| [#96834](https://github.com/openclaw/openclaw/issues/96834) | WhatsApp 图片消息阻塞主通道约 3 分钟 | 消息延迟、多模态运行状态卡死 | 无（`no-new-fix-pr`） |
| [#85030](https://github.com/openclaw/openclaw/issues/85030) | MCP 工具未注入子代理会话，bundle-mcp 与 allowlist 均被忽略 | 子代理仅获得内置工具，安全边界失效 | 无 |
| [#89278](https://github.com/openclaw/openclaw/issues/89278) | Codex OAuth 刷新成功但 Cron/心跳 10 秒超时失败 | 定时任务与心跳认证中断 | 有相关 PR 开放（`linked-pr-open`） |
| [#97616](https://github.com/openclaw/openclaw/issues/97616) | Hook/工具子进程未回收，僵尸进程累积 | 运行时性能逐步劣化 | 无 |
| [#45224](https://github.com/openclaw/openclaw/issues/45224) | Playwright CDP 断言错误未捕获，导致 Gateway 进程退出 | 进程崩溃、依赖 launchd 重启 | 无 |
| [#113701](https://github.com/openclaw/openclaw/issues/113701) | 大工具输出超出上下文窗口，压缩无法恢复，会话进入失败循环 | 会话不可用 | 无 |
| [#99910](https://github.com/openclaw/openclaw/issues/99910) | Memory Dreaming 运行将 Gateway 事件循环占用约 10 分钟 | Gateway 无响应、渠道丢弃 | 无 |

### 🟡 其他值得关注的回归与行为 Bug

- **[#124284](https://github.com/openclaw/openclaw/issues/124

---

## 横向生态对比

# AI 智能体开源生态横向对比分析报告 — 2026-08-23

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态正处于 **"从功能扩张转向稳定性与可信度加固"** 的关键阶段：OpenClaw 社区体量遥遥领先但遭遇 P0 级稳定性瓶颈，OpenHands SDK 在并发锁粒度与崩溃恢复上快速补课，Pi 在 Windows 兼容与长会话可靠性上承受社区压力，Temporal 则作为底层编排基础设施持续加固 SQL 存储一致性与跨集群复制能力。多项目不约而同地暴露出 **长会话上下文管理、子代理并发隔离、持久化存储可靠性** 三大共性痛点，同时安全（供应链确认、安装策略）与生态兼容（MCP/AgentSpec/插件市场）正成为新的竞争焦点。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新（新开/活跃 / 关闭） | PR 更新（待合并 / 已合并或关闭） | Release | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 500 条（480 / 20） | 500 条（427 / 73） | 无 | ⚠️ 极高活跃但维护者评审积压，2 个 P0 bug 无修复 PR（事件循环阻塞 #124788、SQLite 损坏 #126821），beta 稳定性承压 |
| **Hermes Agent** | 数据暂缺 | 数据暂缺 | 无数据 | 无法评估 |
| **OpenHands SDK** | 11 条（6 / 5） | 17 条（6 / 11） | 无 | ✅ 健康。3 个核心修复（#4571/#4488/#2888）当日合并，high 级问题均有修复 PR 跟进，社区响应"正常偏快" |
| **Pi** | 8 新开 / 54 关闭 | 11 条（4 开放 / 7 关闭） | 无 | 🟡 关闭量>>新开量，处于系统性 triage 与稳定化阶段；2 个 high 级 open bug（compaction 失效 #6879、主题残留 #8212）暂无修复 |
| **LiteLLM** | 数据暂缺 | 数据暂缺 | 无数据 | 无法评估 |
| **Temporal** | 2 条新增 | 20 条（18 / 2） | 无（1.32.0 发布分支已建立 #11729） | ✅ 健康。SQL 存储加固与复制可靠性密集推进，#11721 配置语义 bug 当日即收到修复 PR，稳定性态势良好 |

---

## 3. OpenClaw 在生态中的定位

**OpenClaw 是个人 AI 助手赛道中社区体量最大、渠道覆盖最广的"全能型网关"项目。**

- **社区规模断层领先**：单日 500 Issue + 500 PR 的动态量级，是 OpenHands SDK（11/17）与 Temporal（2/20）的数十倍。高热度背后是庞大的用户基数和插件/渠道生态。
- **技术路线差异化**：核心是 **多渠道消息网关（Discord/Telegram/Slack/Feishu/WhatsApp）+ agent 绑定 + 安装策略安全闭环**，面向"个人助手即服务"的场景；而 OpenHands SDK 聚焦软件工程 agent 的 server 架构与对话状态管理，Pi 则押注终端 TUI + 本地模型（llama.cpp），Temporal 是通用工作流编排层，不直接面向终端用户。
- **优势与隐患并存**：渠道抽象和安装供应链安全（#116489 CLI + #120900 UI 双重确认）是其护城河；但 P0 稳定 bug 未修复（beta.2 事件循环阻塞、SQLite 反复损坏）+ 维护者评审积压，可能侵蚀其"个人助手首选"的地位。**"热度最高但稳定性口碑最受挑战"** 是当前最准确的定位描述。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **长会话/大上下文可靠性** | OpenClaw（#113701 工具输出超窗、#124788 事件循环阻塞）、Pi（#6879 auto-compaction 失效、#8464 超限自动续跑） | 固定超时/压缩阈值与推理模型"慢思考"矛盾；需在 agent 循环各步之间触发压缩检查，而非依赖 API 报错 |
| **并发隔离与锁粒度** | OpenHands（#4537/#4569 全局锁阻塞 UI）、OpenClaw（#124788 事件循环阻塞）、Pi（#99910 Memory Dreaming 占满事件循环） | 子代理/后台任务运行时不得阻塞主循环或跨会话互相干扰，从全局锁向 per-conversation/per-process 粒度演进 |
| **持久化存储健壮性** | OpenClaw（#126821 SQLite 反复损坏）、Temporal（#11714 条件更新、#11713 跳过无变更写入、#11712 分页优化） | SQLite/PostgreSQL 在长跑 agent 场景下的事务正确性、损坏恢复与写放大优化 |
| **插件/MCP 生态兼容** | OpenHands（#1457 对齐 Claude Code & AgentSpec）、OpenClaw（#85030 MCP 工具注入子代理失败）、Pi（#8157 mermaid 渲染迁移）、OpenHands #2185（MCP OAuth 超时） | 插件市场标准化、MCP 工具在子代理作用域内正确注入、MCP 认证链路稳定 |
| **供应链安全** | OpenClaw（#116489 安装策略强制确认）、OpenHands（#4543 自托管 GitLab token） | 安装/克隆操作的显式确认与凭据正确处理，防止供应链攻击面扩大 |
| **跨平台支持** | Pi（Windows/ConPTY #8484/8485、启动性能 #8474）、OpenClaw（macOS 引导 #127713） | Windows/macOS 一等公民体验：终端兼容、启动性能、安装引导 |

---

## 5. 差异化定位分析

| 维度 | OpenClaw | OpenHands SDK | Pi | Temporal |
|---|---|---|---|---|
| **核心定位** | 个人 AI 助手网关 | 软件工程 agent 开发 SDK | 终端 TUI 编码 agent | 持久化工作流编排引擎 |
| **功能侧重** | 多渠道接入、安装策略安全、会话绑定 | 子代理委派、崩溃恢复、插件市场、记忆 | **本地模型优先**（llama.cpp 路由）、Windows 终端体验、自动压缩 | SQL 存储一致性、跨集群复制、搜索 API 扩展 |
| **目标用户** | 个人/家庭用户、多频道运维者 | 构建 agent 产品的开发者 | CLI 重度用户、本地模型偏好者 | 大规模分布式应用的基础设施工程师 |
| **架构关键差异** | 网关中心 + agent bindings + 双端 UI | agent-server + ConversationState + 事件流 | 纯 TUI + provider 适配层 + 扩展 API | 强一致状态机 + 持久化队列 + 可见性索引 |
| **当前阶段** | 功能丰富但 beta 稳定性承压 | 常态化快速修复 | 功能整合与平台补课 | 发版前加固（1.32.0 已冻结） |
| **生态接口** | 自有插件体系 + 安装策略 | Claude Code/AgentSpec 兼容 | 内置 providers + 扩展 hooks | worker callbacks + 搜索运算符扩展 |

---

## 6. 社区热度与成熟度

**分层判断：**

- **Tier 1 — 超高速迭代/社区驱动**：**OpenClaw**（500/500 日动态）。社区规模是最大资产，但也因维护者评审积压与 P0 bug 暴露"跑得太快、地基不稳"的风险。处于 **"功能冲刺 vs. 质量治理" 的博弈期**。
- **Tier 2 — 主动收敛/稳定化**：**Pi**（8 新开 vs 54 关闭）。issue 关闭量 6.75 倍于新开，释放明确的 triage 信号；Windows 兼容和 compaction 两项修复是下一版本的关键筹码。
- **Tier 3 — 稳健质量巩固**：**OpenHands SDK**（11/17）。当日 3 个高价值修复合并、2 个 high 问题已有 PR，呈"发现问题→提交 PR→合并"的敏捷闭环，健康度最好。
- **Tier 4 — 基础设施成熟期**：**Temporal**（2/20）。无新 bug 事件、发布分支就绪、核心存储层主动加固，是生态中最接近企业级 GA 质量的项目。
- **数据缺口**：Hermes Agent 与 LiteLLM 当日数据暂缺，建议补充后纳入下一期对比。

---

## 7. 值得关注的趋势信号

1. **"长跑型 agent"成为测试场，淘汰固定超时设计。** Pi 用户在 2 小时 agentic run 中因 auto-compaction 未触发而耗尽上下文（#6879），OpenClaw 用户遭遇 30 秒流式看门狗与长思考模型冲突（#68596）。**固定阈值/固定超时的架构正在被"自适应、按需触发"的诉求取代** —— 建议 agent 框架在设计 watchdogs 和压缩策略时将控制权交给用户/模型。

2. **子代理规模化暴露了全局共享状态的脆弱性。** OpenHands 的全局生命周期锁冻结 UI（#4537/#4569）与 OpenClaw 的事件循环阻塞（#124788、#99910）本质是同一类问题：**共享状态粒度没有跟上子代理/后台任务并行度的发展**。per-conversation / per-process 隔离将是未来 agent runtime 的标配。

3. **MCP 与插件生态从"能连"走向"合规"。** OpenHands 主动对齐 Claude Code & AgentSpec 插件标准（#1457），OpenClaw 强化安装策略强制确认（#116489/#120900），MCP 工具的**作用

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-08-23

## 1. 今日速览

过去 24 小时内，OpenHands SDK 项目保持了较高的活跃度：**共 11 条 Issue 更新（6 条新开/活跃，5 条关闭）和 17 条 PR 更新（6 条待合并，11 条关闭/合并）**。尽管没有新版本发布，但项目在**并发性能重构、崩溃恢复修复、Git 认证和 MCP 生态兼容性**等方面取得了实质性推进。其中最值得关注的是围绕 `TaskToolSet` 全局锁导致 UI 冻结的 high 级别问题（#4537 / #4569），形成了 issue 报告 → 修复 PR 的完整闭环；另有 2 个 high 优先级 bug（#4487、#4569）均已有对应 fix PR。整体项目健康度良好，修复效率和社区响应速度均处于正常偏快水平。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日有多项重要 PR 被合并/关闭，推动了以下关键改进：

- **[#4571 fix(workspace): honor explicit provider host when injecting git clone tokens](https://github.com/OpenHands/software-agent-sdk/pull/4571)（已合并）** — 修复了从自托管 GitLab 实例克隆时 token 被忽略的问题，对应的安全 bug（#4543）随此合并得到解决。
- **[#4488 fix(agent-server): keep crash recovery result on interrupted action branch](https://github.com/OpenHands/software-agent-sdk/pull/4488)（已合并）** — 修复了 agent-server 重启后恢复过程中丢失中断工具结果、导致后续对话永久损坏的问题（#4487）。
- **[#2888 fix: sanitize malformed tool call arguments in LLM history](https://github.com/OpenHands/software-agent-sdk/pull/2888)（已合并）** — 该 PR 修正在 LLM 产生畸形 JSON 工具参数时向事件流写入原始错误参数的问题，阻断 malformed 参数流入后续 LLM 调用，属于长期积累的稳定性修复。
- **[#3905 Optimize conversation search and count](https://github.com/OpenHands/software-agent-sdk/pull/3905)（已合并）** — 优化对话搜索与计数性能，改善大规模会话管理场景下的效率。
- **[#3266 fix(agent-server): evict idle terminal conversations](https://github.com/OpenHands/software-agent-sdk/pull/3266)（已合并）** — 增加可配置的空闲 TTL 和 GC 间隔，自动清理已终结的空闲会话，避免内存泄漏。
- **[#1457 [plugins] Plugin Marketplace Compatibility: Align with Claude Code & AgentSpec](https://github.com/OpenHands/software-agent-sdk/pull/1457)（已合并）** — 实现与 Claude Code Plugins 和 AgentSpec 标准的完整兼容，使插件市场 monorepo 与 Python 包共享同一插件结构。
- **[#2185 fix: MCP OAuth timeout regression - pin fastmcp <3 and add configurable timeout](https://github.com/OpenHands/software-agent-sdk/pull/2185)（已合并）** — 修复 MCP OAuth 服务器超时回归，通过固定 fastmcp 上界和增加可配置超时解决。
- **[#2810 Memory: Research & Implementation Plan for Persistent Auto-Learning](https://github.com/OpenHands/software-agent-sdk/pull/2810)（已关闭）** — 关闭了持久化自动学习记忆的研究与实施计划，实际落地仍需后续推进。
- **[#3782 chore(examples): move 43_mixed_marketplace_skills to 05_skills_and_plugins](https://github.com/OpenHands/software-agent-sdk/pull/3782)（已合并）** — 示例代码目录结构调整，改善项目组织。
- **[#3800 [automated] Update verified_models.py with latest benchmark models](https://github.com/OpenHands/software-agent-sdk/pull/3800)（已合并）** — 自动更新已通过全部 5 项基准测试的模型列表。

**净进展评估**：今日合并的 3 个核心修复（#4571、#4488、#2888）解决了 3 个不同层面的稳定性/认证问题。特别是 #4488 和 #2888 都直接关系到 Long-running agent 场景下的数据完整性，这些修复对生产部署具有实质性意义。

## 4. 社区热点

今日讨论最活跃的 Issues/PRs（按评论数排序）：

- **[#3303 [Feature]: ToolBuild hooks](https://github.com/OpenHands/software-agent-sdk/issues/3303) — 11 条评论（已关闭, Stale）** — 要求提供在工具构建前后对工具列表进行运行时操作的 hooks。该 issue 经过 3 个月讨论后最终被标记为 Stale 关闭。
- **[#4511 [Bug]: `Message.to_chat_dict` emits `cache_control` when caching is disabled](https://github.com/OpenHands/software-agent-sdk/issues/4511) — 5 条评论（开放，ready-for-dev）** — 讨论 SDK 在禁用缓存时仍向 LLM 请求发送 `cache_control` 标记的问题，涉及 LLM 接口层的语义一致性。
- **[#4543 [Bug]: Cannot use a token to clone from a self-hosted Gitlab](https://github.com/OpenHands/software-agent-sdk/issues/4543) — 4 条评论（已关闭）** — 自托管 GitLab 认证问题，今日已通过 #4571 修复并关闭。
- **[#4537 [Bug]: TaskToolSet delegation holds the parent ConversationState lock...](https://github.com/OpenHands/software-agent-sdk/issues/4537) — 4 条评论，1 👍（开放, priority:high）** — 子代理委派任务期间全局锁导致 UI 冻结的高优先级问题，是社区近期最关注的性能/并发 bug 之一。
- **[#4569 perf: replace global _lifecycle_lock with per-conversation locks](https://github.com/OpenHands/software-agent-sdk/issues/4569) — 2 条评论（开放, priority:high）** — 与 #4537 同源问题的性能优化提案，同样已有对应 PR #4570。

**热点分析**：社区讨论集中在两个主题：一是**并发与锁粒度**（#4537/#4569）——当 agent 委派子任务时，全局锁会阻塞整个 agent canvas UI，说明真实用户已在多会话/子代理场景中受到影响，这是一个需要尽快解决的可扩展性瓶颈；二是**LLM 接口层的精细控制**（#4511、#3303）——用户对 SDK 的底层可调控性需求在持续增长。

## 5. Bug 与稳定性

按严重程度排列（High → Medium）：

| 级别 | Issue | 问题描述 | Fix PR | 状态 |
|---|---|---|---|---|
| 🔴 High | [#4537 TaskToolSet delegation holds parent ConversationState lock...](https://github.com/OpenHands/software-agent-sdk/issues/4537) | 子代理运行期间持有父会话状态锁，导致 executor 池饱和、agent canvas UI 对话列表冻结 | [#4570](https://github.com/OpenHands/software-agent-sdk/pull/4570)（开放） | 已有修复，待合并 |
| 🔴 High | [#4569 replace global _lifecycle_lock with per-conversation locks](https://github.com/OpenHands/software-agent-sdk/issues/4569) | 全局生命周期锁导致跨会话互相阻塞，并发压测可复现 | [#4570](https://github.com/OpenHands/software-agent-sdk/pull/4570)（开放） | 已有修复，待合并 |
| 🔴 High | [#4487 crash recovery orphans interrupted tool result...](https://github.com/OpenHands/software-agent-sdk/issues/4487) | agent-server 重启后中断的工具调用永久损坏事件分支（已关闭） | [#4488](https://github.com/OpenHands/software-agent-sdk/pull/4488)（已合并） | ✅ 已修复 |
| 🟡 Medium | [#4543 Cannot use a token to clone from self-hosted Gitlab](https://github.com/OpenHands/software-agent-sdk/issues/4543)（已关闭） | 非 gitlab.com 实例的 GitLab token 被忽略 | [#4571](https://github.com/OpenHands/software-agent-sdk/pull/4571)（已合并） | ✅ 已修复 |
| 🟡 Medium | [#4511 `Message.to_chat_dict` emits `cache_control` when caching is disabled](https://github.com/OpenHands/software-agent-sdk/issues/4511) | 禁用缓存时仍输出 cache_control 标记，可能导致不必要的缓存行为 | 暂无 | 待处理，已标记 ready-for-dev |
| 🟡 Medium | [#4554 CriticMixin always calls evaluate() with git_patch=None](https://github.com/OpenHands/software-agent-sdk/issues/4554) | 评估系统始终以 None 作为 git_patch，导致评估基于 transcript 而非 diff | 暂无 | 待处理 |
| 🟢 未定级 | [#4578 Switching to GPT-5.6 fails with colon-delimited tool-call IDs](https://github.com/OpenHands/software-agent-sdk/issues/4578) | 历史记录中的并行 MCP 工具调用 ID 含冒号导致切换模型失败 | [#4580](https://github.com/OpenHands/software-agent-sdk/pull/4580)（开放） | 已有修复，待合并 |

**稳定性评估**：今日合入的 #4488 和 #4571 直接解决了一个 high 和 一个 medium 级别的数据损坏/安全问题。当前最紧迫的未解决项是 #4537/#4569 的并发锁问题，其修复 PR #4570 仍在待合并状态，内容上已通过测试，建议尽快完成 review。

## 6. 功能请求与路线图信号

- **[#4577 Add per-key tag endpoints to avoid read-modify-write on PATCH /api/conversations/{id}](https://github.com/OpenHands/software-agent-sdk/issues/4577)**（新开，2 条评论）— 用户提出为对话标签增加 per-key 的增删改端点，避免现有整体替换语义带来的并发读取-修改-写入问题。这是一个合理的 API 设计改进，考虑到对话管理是多客户端协作场景，该请求可能会被纳入 agent-server API 的下一次迭代。

- **[#4576 50/50 RevShare Integration: OpenHands & AIML API](https://github.com/OpenHands/software-agent-sdk/pull/4576)**（新开 PR）— AIML API（提供 1000+ 模型访问的聚合平台，40 万+用户）主动提交了提供商集成方案，并提出收入分成合作。此类生态合作伙伴的 PR 通常需要维护团队进行仔细的商业和技术评估。

- **[#4566 fix(agent-server): propagate load_memory preference to all launch paths](https://github.com/OpenHands/software-agent-sdk/pull/4566)**（开放）— 修复 `load_memory` 偏好仅在部分启动路径生效的问题（源 Issue：#4542）。这是对记忆功能的完善，属于细化调整的方向。

- **[#3303 ToolBuild hooks](https://github.com/OpenHands/software-agent-sdk/issues/3303)** — 虽然已在 Stale 规则下关闭，但该请求反映的核心诉求（在工具构建前后对工具列表进行运行时操作）仍未得到满足，未来仍可能被社区重新提出。

## 7. 用户反馈摘要

- **并发场景的痛点（来自 #4537）**：用户报告当 agent 进行 TaskToolSet 子代理调用时，"Agent Canvas conversation list stops rendering for the entire duration of the delegated task"，直接影响多任务并行操作时的可视化体验。该反馈已获 1 👍，反映了真实用户在复杂 agent 工作流中的阻塞感。

- **自托管 GitLab 用户的认证困境（来自 #4543）**：用户在非 `gitlab.com` 的 GitLab 实例上使用 token 克隆仓库失败，这意味着大量企业/私有化部署用户无法正常使用 OpenHands 的 Git 集成为能。修复 #4571 已合入，但值得关注的是 root cause 是 URL host 与写死的 SaaS 主机不一致——未来建议将 provider host 识别逻辑做得更通用。

- **模型兼容性焦虑（来自 #4578）**：用户从 Kimi K3 切换到 GPT-5.6 时，因历史记录中并行 MCP 工具调用 ID 含冒号而失败。这暴露了跨模型切换时数据格式规范化不足的问题，对依赖多模型切换的用户影响较大。好在 #4580 已提交修复。

- **评估系统准确性质疑（来自 #4554）**：用户指出 CriticMixin 在评估时始终传 `git_patch=None`，意味着整个评估系统实际在评论文本记录而非代码 diff。这直接影响评估结果的可信度，是一个相对隐蔽但意义重大的缺陷。

## 8. 待处理积压

- **[PR #4438 fix(sdk): prevent double provider-prefix strip for names

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-23

## 今日速览

过去 24 小时 Pi 项目呈现出两个明显特征：一是 issue 关闭量远大于新开量（54 关闭 vs. 8 新开），表明维护团队正在进行系统性 triage 与积压清理；二是 PR 合并/关闭链条紧凑，多与 Windows/ConPTY 终端兼容性、llama.cpp 集成与 TUI 稳定性相关。值得关注的是社区对自动压缩（auto-compaction）失效问题的强烈诉求（#6879，18 👍），以及对 Windows 支持的持续讨论（#7547，39 评论），均指向"长会话可靠性"与"跨平台体验"两大核心痛点。新版本发布为 0，项目处于典型的功能整合与稳定化阶段。

## 版本发布

今日无新版本发布（最新 Releases 为空），无破坏性变更或迁移事项需要提示。

## 项目进展

今日 11 条 PR 中 7 条已关闭（含合并），4 条仍处于开放状态。核心进展集中在以下方向：

- **Windows/ConPTY 修复**：[#8485](https://github.com/earendil-works/pi/pull/8485) 通过在 TUI 主屏渲染时禁用 autowrap，修复了 Windows Terminal 下编辑长文本时 ConPTY 自动换行导致光标漂移的问题（对应 issue #8484）；[#8486](https://github.com/earendil-works/pi/pull/8486) 配套添加了 editor 滚动的捕获与验证工具。这组 PR 直接回应了 Windows 用户的核心痛点。
- **启动性能优化**：[#8474](https://github.com/earendil-works/pi/pull/8474) 由 mitsuhiko 提交，将 pi-coding-agent 的打包方式改为大幅减少文件加载数量，旨在解决 Windows 上因 Defender 扫描导致的启动缓慢问题。虽处于早期测试阶段，但方向明确。
- **llama.cpp 集成补全**：[#8479](https://github.com/earendil-works/pi/pull/8479) 使未加载的 llama.cpp 预设模型在选择器中可见，解决了 #8167 报告的路由模式下模型列表缺失问题。
- **TUI 细节改进**：[#8459](https://github.com/earendil-works/pi/pull/8459) 修复了全屏模式下双击选择路径时 `/` 和 `-` 被错误打断的行为；[#8295](https://github.com/earendil-works/pi/pull/8295) 为 `/settings` 增加了中英文 locale 切换能力。
- **新增 provider**：[#8488](https://github.com/earendil-works/pi/pull/8488) 将 MindsHub 作为内置 pi-ai provider 合入（对应 issue #8489），拓展了模型网关的接入范围。

整体来看，项目在"平台兼容性补课"和"TUI 交互细节打磨"上向前迈进了一步，但大型功能（如 loadout 管理 #7148）仍处于 draft 状态，尚未进入合并轨道。

## 社区热点

1. **[#7547 — Windows 使用体验调研（39 评论）](https://github.com/earendil-works/pi/issues/7547)** — 以 issue 形式发起的 Windows 用户问题征集，至今仍然开放且持续获得更新。讨论热度高，反映了 Windows 用户群体对 pi 的期待与当前体验中的诸多摩擦点。用户 @petrroll 作为维护者主动发起调研，说明团队已意识到平台覆盖的重要性，但问题较分散（终端兼容、key-binding 冲突、文件 IO 性能等），尚未收敛成明确的重构方向。

2. **[#6879 — auto-compaction 失效（20 评论，18 👍）](https://github.com/earendil-works/pi/issues/6879)** — 当前最高赞 issue。用户报告在 gpt-5.6-sol 的 2 小时 agentic run 中，footer 超过 compaction 阈值但系统未触发，直到 373k tokens 时被 API 拒请求。背后诉求是"自动压缩必须在 agent 循环的每个步骤之间进行检查"，而非依赖 API 报错。这直接关系到长会话的用户信任度，需要维护者认真对待。

3. **[#8157 — grok-mermaid 迁移到 lovely-mermaid（9 评论）](https://github.com/earendil-works/pi/issues/8157)** — 社区成员希望将 pi 内置的 mermaid 渲染实现从质量较差的 1:1 移植版迁移到更用心的 lovely-mermaid。讨论集中在渲染引擎的替换成本与兼容性，属于底层依赖升级方向，可能影响 TUI 图表展示质量。

4. **[#8167 — llama.cpp 模型不可选（9 评论）](https://github.com/earendil-works/pi/issues/8167)** — 用户报告 llama-server 的模型在 router 模式下不出现于模型列表。该 issue 今天已由 [#8479](https://github.com/earendil-works/pi/pull/8479) 解决，体现了社区反馈到修复的高效闭环。

## Bug 与稳定性

| 严重程度 | Issue | 状态 | 说明 |
|---|---|---|---|
| 高 | [#6879 auto-compaction 不触发](https://github.com/earendil-works/pi/issues/6879) | OPEN | 会话超时/超长时压缩失效，直到 API 拒请求才被迫行动。无 fix PR，需从架构上重构压缩检查时机 |
| 高 | [#8442 Backspace 在 Kitty 协议下被忽略](https://github.com/earendil-works/pi/issues/8442) | CLOSED | herdr pane 内 legacy `0x7f` 在 KKP 激活后被忽略，Ctrl+Backspace 可删除。协议事件过滤问题，与 #7130 同源 |
| 中 | [#8484 Windows/ConPTY 光标漂移](https://github.com/earendil-works/pi/issues/8484) | CLOSED | 编辑器视图看似滚回顶部，实际是 autowrap 在 ConPTY 上的渲染漂移。**已有 fix PR #8485 合入** |
| 中 | [#8212 主题切换产生残留色](https://github.com/earendil-works/pi/issues/8212) | OPEN | 头部、树标签等区域保留旧主题颜色，0.84.2 回归。**无 fix PR** |
| 中 | [#8468 GitHub Copilot 登录超时](https://github.com/earendil-works/pi/issues/8468) | CLOSED | 在 checkout #8254 的 commit 后复现，等待 release 验证 |
| 低 | [#8456 Gemini 3.7 Flash 拒绝 MINIMAL thinking](https://github.com/earendil-works/pi/issues/8456) | CLOSED | `/tree` 分支摘要未携带 `reasoning` 参数导致失败，适配器需补充该字段 |
| 低 | [#8454 OpenRouter reasoning-mandatory 模型报 400](https://github.com/earendil-works/pi/issues/8454) | CLOSED | 后台调用显式发送 `reasoning:{effort:"none"}` 被模型拒绝，需在适配器层处理 |

**趋势观察**：昨日批量关闭的 bug 中，相当部分属于"已定位根因但修复尚在途"的类型；真正仍开放的高优先级问题集中在 compaction 调度（#6879）与主题切换残留（#8212）两项上，建议维护者优先安排。

## 功能请求与路线图信号

今日功能请求呈现出清晰的几个集群：

- **上下文与会话管理**：[#8464](https://github.com/earendil-works/pi/issues/8464) 请求在模型真正触达输出上限时自动继续运行，并在工具调用轮次之间检查自动压缩——与 #6879 的需求完全互补，是未来 v0.86 或 v0.87 的重要候选功能。
- **模型生态图谱**：[#8469](https://github.com/earendil-works/pi/issues/8469) 请求新增 deepseek-v4-flash-vision-exp；[#8489](https://github.com/earendil-works/pi/issues/8489) 请求内置 MindsHub provider（**接口 #8488 已合入**）。模型目录的更新已是高频例行事务。
- **扩展体系治理**：[#8431](https://github.com/earendil-works/pi/issues/8431) 要求 `--exclude-extensions` 排除特定扩展；[#8385](https://github.com/earendil-works/pi/issues/8385) 提出 SQLite 记忆扩展方案；[#8380](https://github.com/earendil-works/pi/issues/8380) 希望 provider 生命周期 hooks 共享 request ID。三者指向扩展生态即将进入"深度定制"阶段。
- **远程使用场景**：[#8481](https://github.com/earendil-works/pi/issues/8481) 提议在 RemoteSession 模式下本地跑 TUI、远程保留 agent 状态，符合 Kubernetes devbox 的工作方式。该请求若落地，将打开远程开发的另一维度。

**路线图判断**：结合已合并的 #8488（MindsHub provider）与在途的 #8474（Node runtime 打包）、#7148（loadout 管理），下一版本大概率聚焦于"启动性能 + 扩展管理 + 模型接入"三件事；compaction 相关的两个 issue（#6879 + #8464）则可能成为 0.85 或 0.86 的架构级改动。

## 用户反馈摘要

从今日 issue 评论中可提炼出以下真实用户声音：

- **Windows 用户仍在"用爱发电"**（#7547）：用户反馈集中在"不知道哪种运行方式是被官方支持的""终端 key-binding 冲突频繁""Windows Defender 拖慢启动"等。社区虽活跃，但缺乏官方明确的 Windows 支持矩阵，这是提升采纳率的主要障碍。
- **长会话稳定性是信任底线**（#6879）：用户明确表示"我以为它会在 footer 达到阈值时压缩，结果它硬跑到 API 拒请求才停下来"。这反映出用户对自动压缩有预期，但实现没有兑现承诺。
- **llama.cpp 用户对模型选择器的苛求**（#8167）：自建 llama-server 的用户需要"可见即可选"的模型列表，而不是依赖 autoload 行为。该需求已被接受，显示项目对本地模型的重视。
- **对 TUI 细节的认真反馈**（#8459、#8484、#8212）：双击选路径、ConPTY 渲染漂移、主题残留等细节问题被逐一提交并附有复现步骤，说明用户愿意深度参与打磨了。
- **开发者对扩展 API 的期待**（#8380）：一位扩展作者表示"没有共享 request ID，我无法在 provider 请求的 before/after 之间可靠地配对状态"，这是扩展 API 成熟度的重要信号。

整体情绪：**积极但有耐心的不满**。用户对 pi 的潜力认可度高，但对 Windows 兼容性、长会话可靠性这两块短板期待大幅改进。

## 待处理积压

以下重要 issue/PR 长期未获明确推进，建议维护者关注：

1. **[#6879 auto-compaction 全面失效（18 👍）](https://github.com/earendil-works/pi/issues

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-23

## 今日速览

过去24小时内，Temporal 核心仓库保持了高强度的开发节奏：共产生 20 条 PR 更新（其中 18 条待合并、2 条已关闭），虽无新版本发布，但 PR 数量较前日明显上升，活跃度处于高位。Issue 侧相对平稳，新增 2 条（1 个 bug、1 个功能请求）。值得注意的是，围绕 SQL 持久化可靠性（#11714、#11712、#11713）和跨集群复制可观测性（#11707、#11705）有多条来自同一团队的密集提交，显示核心存储层和复制路径正在经历系统性的加固。另有 1 个针对昨日动态配置 bug（#11721）的修复 PR 已提交，问题响应速度较快。

---

## 版本发布

**今日无新版本发布。** 但注意 PR #11729 为 1.32.0 准备发布分支（含治理文件覆盖与依赖更新），该分支已建立，预示着 1.32.0 版本已进入发布准备阶段，正式发布或将临近。

- [#11729 Prepare release branch 1.32.0](https://github.com/temporalio/temporal/pull/11729)

---

## 项目进展

今日无直接合并进 `main` 的功能性 PR，但有两条已关闭的 PR 值得关注，另有若干高价值 PR 处于开放状态，反映了项目下一步的技术方向。

**已关闭：**

- **1.32.0 发布分支已就绪**（#11729）：CI/CD bot 自动准备发布分支，包含治理文件覆盖和依赖更新。这是一个明确的信号：Temporal 1.32.0 版本候选分支已经存在，版本内容已冻结，接下来是新版本的回归测试和最终发布。另有一条测试分片盐值更新的自动 PR（#11708）也已关闭。
  - [#11729](https://github.com/temporalio/temporal/pull/11729)

**待合并但高价值（反映正在推进的实质工作）：**

- **SQL 持久化一致性加固**（#11714，修复 #11711）：SQL 执行更新时，在 UPDATE 谓词中加入预期记录版本（prior record version）或 next event ID 条件，使 PostgreSQL/MySQL/SQLite 的更新操作同时获得行锁与条件校验，防止基于过期快照的写入。该 PR 直接增强了 SQL 存储后端的事务正确性。
  - [#11714](https://github.com/temporalio/temporal/pull/11714)

- **PostgreSQL 元组游标分页**（#11712，修复 #11709）：将历史节点、历史节点元数据、定时任务的向前分页从 `OR` 表达式改为行值比较（row-value comparison），消除分页深时 `OR` 条件带来的索引低效问题。
  - [#11712](https://github.com/temporalio/temporal/pull/11712)

- **跳过无变更的 current execution 更新**（#11713，修复 #11710）：锁定并校验 current-execution 行后，若所有持久化字段均无变化，则跳过 `UpdateCurrentExecutions` 写入，减少不必要的锁竞争和写入放大。
  - [#11713](https://github.com/temporalio/temporal/pull/11713)

- **跨集群复制可靠性提升**（#11707、#11705）：新增 parent-child workflow 生命周期 wide events（#11707），为父子工作流的失败与恢复路径记录执行身份、initiated event ID/version、错误及本地状态（如 `Zombie`），大幅提升分布式工作流调试的可观测性；同时增加了 passive 集群上子工作流缺失时的异步补偿恢复路径（#11705），并加入去重机制。
  - [#11707](https://github.com/temporalio/temporal/pull/11707)
  - [#11705](https://github.com/temporalio/temporal/pull/11705)

**整体判断：** 项目当前正在推进三条主线——一是 SQL 存储后端的事务正确性与性能（#11714/#11712/#11713），二是跨集群复制场景下的可靠性与可观测性（#11707/#11705/#11411），三是 worker callbacks 功能栈的持续完善（#11566/#11520/#11380）。

---

## 社区热点

今日社区讨论热度集中在两条 Issue 上：

- **#11721 MaximumAttempts 动态配置冲突 Bug**（3 条评论）：用户 `@M0NsTeRRR` 报告了一个配置冲突问题——当服务端通过动态配置设置 `history.defaultActivityRetryPolicy.MaximumAttempts=5` 时，客户端工作流中显式传入 `maximum_attempts=0`（表示无限重试）的行为被覆盖。该问题触及 proto3 无法区分 "字段未设置" 与 "显式设置为 0" 的经典陷阱，服务端将显式的 0 视为未设置进而套用默认值，导致用户无法可靠地关闭默认重试限制。

- **#11718 CLI 工具随发布归档分发的功能请求**（1 条评论）：用户 `@sinux-l5d` 希望 Temporal 发布归档中能包含 `temporal` 开发 CLI 二进制文件，以便通过 Mise 等依赖管理工具直接安装使用，无需额外步骤。

- **#11728 LIKE / NOT LIKE 搜索运算符**：虽然直接评论不多，但这可能是今天最值得关注的 PR 之一——它为核心搜索 API 增加了 `LIKE`/`NOT LIKE` 运算符，为 keyword 类型 search attributes 提供子串匹配能力，并需要为 Elasticsearch、SQL 等多个后端分别实现翻译层，涉及面较广。

- [#11721](https://github.com/temporalio/temporal/issues/11721)
- [#11718](https://github.com/temporalio/temporal/issues/11718)
- [#11728](https://github.com/temporalio/temporal/pull/11728)

---

## Bug 与稳定性

**高优先级 Bug：**

1. **MaximumAttempts=0 被服务端动态配置覆盖**（#11721）：用户显式设置工作流/活动的 `maximum_attempts=0`（无限重试），但服务端 `defaultActivityRetryPolicy` 中有非零默认值时，proto3 无法区分 "未设置" 与 "显式 0"，导致用户配置被覆盖。这是一个影响语义正确性的 bug，打破了用户的显式意图。
   - **状态：已有修复 PR**（#11727）在今日提交。该 PR 通过调整动态配置合并逻辑，保留用户显式设置的 `MaximumAttempts=0` 值。
   - [Issue #11721](https://github.com/temporalio/temporal/issues/11721) | [修复 PR #11727](https://github.com/temporalio/temporal/pull/11727)

**可靠性修复类 PR（待合并，非新出 bug）：**

2. **SQL 连接池强制刷新期间的句柄丢失风险**（#11730）：在检查 SQL 会话刷新是否被限流（throttled）之前就清空并关闭了当前连接池，若刷新被限流，则旧池已被销毁而新池未建立，数据库句柄会处于临时不可用状态。修复为先检查限流、再决定是否丢弃连接池。
   - [#11730](https://github.com/temporalio/temporal/pull/11730)

3. **批量活动恢复操作的可见性查询范围被替换**（#11725）：基于活动类型的批量 unpause 操作原先会用活动类型谓词替换调用方提供的可见性查询，导致查询范围被意外改变。修复为安全组合两者。
   - [#11725](https://github.com/temporalio/temporal/pull/11725)

**整体评估：** 今日无崩溃级或数据完整性级别的严重 bug 报告。主要问题集中在配置覆盖语义和连接池管理边界，均有修复 PR 跟进，稳定性态势良好。

---

## 功能请求与路线图信号

1. **LIKE / NOT LIKE 搜索运算符**（PR #11728）：为 keyword search attributes 增加 `LIKE`/`NOT LIKE` 支持，使子串过滤（Contains）成为可能。实现包括：查询解析接受 `LikeStr`/`NotLikeStr`、Elasticsearch 后端映射到 wildcard 查询、SQL 后端透传 LIKE 模式。该功能将显著增强 Temporal 搜索的灵活度，实现对已有运算符体系的重要补充。该 PR 由外部贡献者 `@Rasu-Dev` 提交。
   - [#11728](https://github.com/temporalio/temporal/pull/11728)

2. **CLI 随发布归档分发**（Issue #11718）：用户希望 `temporal` 开发 CLI 直接打包在 GitHub Release 的归档中，便于通过 Mise、asdf 等版本管理工具直接获得。对于尚未使用 Docker 的开发工作流，这是一个流畅性改善请求。实现成本较低，值得维护团队考虑。
   - [#11718](https://github.com/temporalio/temporal/issues/11718)

3. **Worker callbacks 功能栈持续演进**（#11566/#11520/#11380）：三条约在 7 月底至 8 月中旬创建的 PR 仍在迭代中，均为同一特性栈的不同层次（配置化回调类型、CallbackInfo.outcome 填充、新 `commonpb` 回调变体识别）。这表明该特性正处于密集开发期，预计会在未来版本中进入 `main`。
   - [#11566](https://github.com/temporalio/temporal/pull/11566)
   - [#11520](https://github.com/temporalio/temporal/pull/11520)
   - [#11380](https://github.com/temporalio/temporal/pull/11380)

---

## 用户反馈摘要

- **配置覆盖是真实的权益痛点**（#11721）：用户在评论区描述了实际场景——团队通过服务端动态配置统一设置默认重试次数为 5，但特定工作流需要用穷尽重试（0 = 无限）来等待外部依赖恢复。当前行为让用户感到"显式意图被静默忽略"，且 proto3 的语义限制使问题在协议层面难以完美解决，需要服务端做出特殊的零值处理。
  - 链接：https://github.com/temporalio/temporal/issues/11721

- **开发者工具链的集成诉求**（#11718）：用户依赖 Mise 管理项目依赖，希望 Temporal CLI 能像其他工具一样从发布归档直接安装。这一请求反映了 Temporal 开发者生态中，有相当数量的用户倾向于本地二进制而非 Docker 容器，工具分发的便捷度直接影响开发体验。
  - 链接：https://github.com/temporalio/temporal/issues/11718

- **外部贡献者活跃**：今日值得注意的外部贡献包括 `@Rasu-Dev`（LIKE 运算符）、`@waterWang`（MaximumAttempts 修复）、`@abenn135`（文档更新）。多个外部 PR 获得了维护者的关注和更新，社区参与度良好。

---

## 待处理积压

以下为长期未合并或讨论度不足但值得注意的项：

1. **Gcloud archiver 查询增强**（PR #9449，stale）：创建于 2026-03-10，已超过 5 个月无进展。该 PR 试图解决 gcloud 归档中按 workflow ID 和 runId 过滤能力不足的问题，目前只能按时间范围做前缀搜索。对于使用 GCS 归档的用户，这仍是一个可改进点。
   - [#9449](https://github.com/temporalio/temporal/pull/9449)

2. **PostgreSQL 文档版本与用户名更正**（PR #10002，stale）：创建于 2026-04-21，一个微小但实用的文档修复（Homebrew 已无 PostgreSQL 9.6，且文档中的用户名与实际命令不一致）。长时间未合并可能只是因为优先级低，但合并成本也很低。
   - [#10002](https://github.com/temporalio/temporal/pull/10002)

3. **复制削峰（gradual connect shedding）机制**（PR #11492）：创建于 2026-08-12，已开放 11 天。该 PR 为全局命名空间引入渐进式连接期，在恢复期间按比例削减复制流量以平滑峰压。此类对核心复制路径的改动通常需要较长的评审周期，但功能本身对大规模多集群部署具有重要意义。
   - [#11492](https://github.com/temporalio/temporal/pull/11492)

---

*报告生成时间：2026-08-23*
*数据来源：github.com/temporalio/temporal 公开仓库活动数据*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*