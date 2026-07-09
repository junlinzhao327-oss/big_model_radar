# OpenClaw 生态日报 2026-07-09

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-09 01:52 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目日报 (2026-07-09)

---

## 1️⃣ 今日速览

- 过去24小时内，项目共产生 **500 条 Issue 更新**（新开/活跃 458，关闭 42）和 **500 条 PR 更新**（待合并 413，已合并/关闭 87），表明社区极度活跃，但合并效率偏低（合并/关闭率仅 17.4%）。
- 无新版本发布，项目处于高强度 Bug 修复与功能迭代阶段，大量 **P1/P0 级 Session 稳定性和消息丢失问题** 持续占据社区关注中心。
- **关键趋势**：`#94228`（Anthropic thinking 块签名失效）、`#85333`（性能回退 4-5x）、`#99912`（心跳路由错误）等长时间未解决的钻石/铂金级 Bug 依然缺乏修复 PR，项目健康度面临持续压力。

---

## 2️⃣ 版本发布

无新版本发布。

---

## 3️⃣ 项目进展（今日已合并/关闭的 PR）

以下为今日合并/关闭的关键 PR（共 87 条，择要列举）：

| PR # | 标题 | 状态 | 影响范围 |
|------|------|------|----------|
| [#102331](https://github.com/openclaw/openclaw/pull/102331) | fix(google-meet): keep Meet sessions on the agent that joined them | **已合并** | 多 Agent 部署中 Google Meet 会话归属修复 |
| [#102343](https://github.com/openclaw/openclaw/pull/102343) | fix(codex): remote app servers can read OpenClaw skills | **已合并** | Codex 远程服务器对 SKILL.md 的读取修复 |

- 以上两项均属 **维护者直接修复（Label: maintainer）**，分别解决了多 Agent 场景下的音视频会话错乱和 Codex 集成中的权限问题，是项目推进的实质性成果。
- 其余 85 条合并在底层缓存、日志、配置等领域，但无大型功能分支关闭。

> 💡 社区贡献的 PR 合并/关闭率较低（~17%），大量 PR（413条）仍处于待合并/待审查状态，需要维护者加速处理。

---

## 4️⃣ 社区热点（今日讨论最活跃的 Issues/PRs）

### 4.1 评论数 Top 3 Issues
| # | 标题 | 评论数 | 👍 | 摘要 |
|---|------|--------|----|------|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | Text between tool calls leaks to messaging channels | **35** | 1 | 工具调用间隙文本泄漏到最终用户消息通道（Slack/iMessage），钻石级 Bug，存在已有 PR 但未修复 |
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | Subagent completion silently lost — no retry, no notification, no auto-restart on timeout | **21** | 1 | 子 Agent 完成结果静默丢失，无重试/通知/自动重启，钻石级 |
| [#48003](https://github.com/openclaw/openclaw/issues/48003) | Steer mode does not inject messages mid-turn for main sessions | **15** | 3 | `steer` 模式无法在运行中的回合内注入消息，导致延迟响应 |

- 社区讨论的焦点依然是 **会话状态丢失**、**消息错乱** 和 **子 Agent 协调** 三大顽疾，且多为**超过 4 个月未关闭的钻石级问题**。

### 4.2 热点 PR（评论数最多，但受限于数据中未列出评论数，故以 Rating 和风险标签判断关注度）
- [#102305](https://github.com/openclaw/openclaw/pull/102305)：修复 Agent 热重载后模型不生效的问题，标记为 `merge-risk: 🚨 session-state`，风险极高。
- [#99365](https://github.com/openclaw/openclaw/pull/99365)：解决方案**持久化消息去重**以防止网关重启后重复处理，是解决 `#97538` 的关键 PR，但仍有多个 `merge-risk` 标签。
- [#102331](https://github.com/openclaw/openclaw/pull/102331)（已合并）收到社区广泛认可，缓解了多 Agent 部署中的 Meet 会话归属痛点。

---

## 5️⃣ Bug 与稳定性（按严重程度排列）

### ⚠️ P0 / 铂金级（影响生产可用性）
| Issue | 标题 | 是否有 Fix PR | 影响 |
|-------|------|---------------|------|
| [#43661](https://github.com/openclaw/openclaw/issues/43661) | Session hangs indefinitely on compaction timeout → 重复发送 | **有 PR 链接** | 导致用户收到重复消息，会话卡死 |
| [#48920](https://github.com/openclaw/openclaw/issues/48920) | Live Docs 领先于发布版本 | 无 | 文档误导用户使用未发布的配置项 |
| [#43996](https://github.com/openclaw/openclaw/issues/43996) | Sandbox 容器因 `no-new-privileges` 立即退出 | 无 | 升级后 maker 沙箱完全不可用 |
| [#82662](https://github.com/openclaw/openclaw/issues/82662) | 孤立 cron 任务在所有回退模型前超时 | 无 | 2026.5.12 回归，任务无法启动 |
| [#94228](https://github.com/openclaw/openclaw/issues/94228) | Native Anthropic 路径中 thinking 块签名失效 | 无 | 长会话永久砖化（HTTP 400） |

### 🔴 P1 / 钻石级（常见且影响广泛）
| Issue | 标题 | 是否有 Fix PR | 影响 |
|-------|------|---------------|------|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | 工具调用间隙文本泄漏 | 有（但未合并） | 内部输出暴露给用户 |
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | 子 Agent 结果静默丢失 | 有（但未合并） | 任务失败无反馈 |
| [#48003](https://github.com/openclaw/openclaw/issues/48003) | Steer 模式未注入消息 | 有（但未合并） | 交互延迟 |
| [#45740](https://github.com/openclaw/openclaw/issues/45740) | gh-issues skill 注入不安全 issue body | 无 Fix PR | 安全风险 |
| [#45494](https://github.com/openclaw/openclaw/issues/45494) | Cron 任务在 API 500 时缓慢超时而非快速失败 | 无 | 资源浪费 |
| [#99912](https://github.com/openclaw/openclaw/issues/99912) | 心跳路由到错误 Agent 会话 | 无 | 隔离失效 |
| [#102321](https://github.com/openclaw/openclaw/pull/102344) (关联) | OpenAI refusal 字段未展示（部分已修复） | 有 PR（#102344, #102334） | 用户看到空白回复 |

### 🟡 P2 / 中等严重（影响功能但非阻塞）
- 性能回退：`#85333`（doctor --fix 慢 4-5x）
- 多 Agent 不稳定：`#43367`（并发 add 覆盖）
- 配置错误：`#45765`（OPENCLAW_HOME 嵌套）
- 数据丢失：`#40001`（write 工具缺 append 模式）
- 子 Agent 会话残留：`#47975`
- 不可视错误：`#45314`（模板变量未填充）
- 成本报告遗漏：`#46252`（.jsonl.reset 文件未计入）

### 📌 今日报告的新 Bug（新建或活跃）
- `#99912`：Agent 心跳路由到错误 Agent 的会话（新锐 Bug，发布于7月4日，7月9日仍有讨论）
- `#102321`（关联）：OpenAI 内容拒绝导致空白回复，已有多个 PR 尝试修复（#102334, #102344, #102342），但尚未合并统一方案。

---

## 6️⃣ 功能请求与路线图信号

| 功能请求 | 热度（👍） | 是否有 PR | 可能纳入版本 |
|----------|-----------|-----------|---------------|
| [Add MathJax/LaTeX Support to Control UI](https://github.com/openclaw/openclaw/issues/42840) | 👍9 | 无 | 低优先级，但近期讨论增加 |
| [tools.web.fetch.allowPrivateNetwork](https://github.com/openclaw/openclaw/issues/39604) | 👍11 | 无 | 安全配置需求强烈 |
| [Per-agent cost budget enforcement](https://github.com/openclaw/openclaw/issues/42475) | 👍1 | 无 | 企业运维特性 |
| [Pre-reset agentic memory flush](https://github.com/openclaw/openclaw/issues/45608) | 👍4 | 无 | 减少数据丢失 |
| [Gateway lifecycle hooks](https://github.com/openclaw/openclaw/issues/43454) | 👍1 | 无 | 高级扩展点 |
| [YAML config file format](https://github.com/openclaw/openclaw/issues/45758) | 👍2 | 无 | 易用性改进 |
| [Distributed Agent Runtime (separate control plane)](https://github.com/openclaw/openclaw/issues/42026) | 👍3 | 无 | 长期架构级 RFC |
| [Provider fallback by failure class](https://github.com/openclaw/openclaw/issues/47910) | 👍0 | 无 | 近期日志显示高频 auth 错误回退浪费 |

**路线图信号**：社区对 **安全性（私有网络、Issues 注入）**、**运维成本控制（预置预算、备份排除）**、**用户体验（LaTeX、抹除前内存刷新）** 需求强烈。但项目中**大量 P1 级 Bug 积压**，可能挤压功能开发资源。

---

## 7️⃣ 用户反馈摘要（从 Issue 评论提炼）

### 常见痛点
1. **“会话丢失/死锁” 反复出现**  
   @magnusbonnevier: “Subagent sessions persist after completion, main session becomes unresponsive — had to kill the gateway manually.”（#47975）  
   @thedanchez（#43661）: “Each timeout (~10 min) triggers a delivery retry that resends the same message repeatedly — with no recovery, no feedback.”

2. **配置热更新不生效**  
   @SunnyShu0925（PR #102305）: “Agent model hot-reload silently does not take effect; existing sessions keep the pre-reload model until full gateway restart.”

3. **媒体/图片渲染兼容性差**  
   @lsr911（PR #102337）: “Anthropic rejects HEIC/TIFF images; the error is opaque.”  
   @charzhou（#42820）: “Feishu message tool cannot send a plain file because poll fields pollute schema.”

4. **隔离模式与路由混乱**  
   @tyukara（#99912）: “Heartbeat executes in default agent’s session regardless of isolatedSession setting.”  
   @matthewpoe（#40611）: “Heartbeat drift fix causes aggressive retry that blocks Telegram during active conversations.”

### 正向反馈（较少，但可体现价值）
- PR #102340（允许配置 Slack App Home 文案）获得初步认可，满足了品牌白标需求。
- PR #102331（Google Meet 会话归属）获得“解决了多 Agent 下的混乱”反馈。
- Issue #42840（LaTeX 支持）👍9，用户称“数学公式显示为乱码严重影响教学场景”。

### 满意度判断
**总体不满情绪较高**：P0/P1 Bug 历史长（超过4个月）、修复进展缓慢，用户反复报告重复问题（如 Thinking 签名失效 #94228）。长期未解决的性能回退（#85333）和配置覆盖（#43367）导致部分用户考虑回退版本。

---

## 8️⃣ 待处理积压（长期未响应的重要 Issue/PR）

### 🔴 钻石级 Issue（无任何 Fix PR 或维护者回复）
- [#45740](https://github.com/openclaw/openclaw/issues/45740) — gh-issues skill 注入：创建于 2026-03-14，**已 117 天无实质修复**，存在安全风险。
- [#45494](https://github.com/openclaw/openclaw/issues/45494) — Cron 任务慢超时：创建于 2026-03-13，需产品决策。
- [#94228](https://github.com/openclaw/openclaw/issues/94228) — Anthropic thinking 签名：创建于 2026-06-17，虽为近期但直接影响长会话，且无 PR指向。

### 🟡 高评论数但无官方回复
- [#25592](https://github.com/openclaw/openclaw/issues/25592)（35条评论） — 文本泄漏：虽有 linked PR（未合并），维护者未在 Issue 中更新状态。
- [#44925](https://github.com/openclaw/openclaw/issues/44925)（21条评论） — 子 Agent 丢失：同无维护者更新。

### 📌 长期等待的 PR（超过30天未合并）
- [#83988](https://github.com/openclaw/openclaw/pull/83988) — fix(tts): defer text settlement for final-mode TTS（创建于5月19日，**52天**待合并，已被标记 `waiting on author`，但作者已提交 proof）
- [#99221](https://github.com/openclaw/openclaw/pull/99221) — feat(github-copilot): 支持 GitHub Enterprise（创建于7月2日，7天，但标签已标记 `ready for maintainer look`，需维护者加速审查）

> ⚠️ 建议：维护者应优先对 **已有 linked PR 但超过2周未合并的钻石级 Issue（如 #25592、#44925、#48003）** 给出明确决策（merge/close/need changes），以避免社区贡献者精力浪费。

---

*报告生成时间：2026-07-09 | 数据来源：GitHub Issues & PR API | 分析模型：OpenClaw 项目分析师 AI*

---

## 横向生态对比

# 个人 AI 助手开源生态横向对比分析报告 (2026-07-09)

---

## 1. 生态全景

当前个人 AI 助手/自主智能体开源生态正经历 **高速迭代与稳定性博弈** 的关键期。头部框架（OpenClaw、Hermes Agent）社区活跃度极高，单日 PR 更新均超 500 条，但严重 Bug 积压与合并效率低下警示着规模化后治理挑战。工具链项目（LiteLLM、OpenHands SDK）围绕模型路由、技能标准化和网关安全快速迭代，而底层调度引擎（Temporal）则持续强化工作流状态管理的鲁棒性。整体呈现出 **“大前端框架热衷多Agent会话，后端基础设施聚焦可靠性”** 的格局，会话状态持久化、模型推理格式兼容、MCP 工具互操作、供应链安全成为生态共同攻坚的四大方向。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新 (新开/活跃 / 关闭) | PR 更新 (待合并 / 合并关闭) | 合并率 | 今日发布 | 健康度评估 |
|------|-------------------------------|-----------------------------|--------|----------|------------|
| OpenClaw | 500 (458/42) | 500 (413/87) | 17.4% | 无 | 🔴 极高活跃但合并积压严重，P0/P1 Bug 长期未愈 |
| Hermes Agent | 252 (未细分) | 500 (348/152) | 30.4% | v0.18.2 | 🟢 高产、Kanban 系统大幅推进，但待审 PR 仍多 |
| OpenHands SDK | 13 (8/5) | 24 (14/10) | 41.7% | v1.33.0 | 🟢 稳健迭代，技能架构重构顺利 |
| Pi | 43 (未细分/37关闭) | 7 (1/6) | 85.7% | 无 | 🟢 高效修复 Bug，体验提升明显 |
| LiteLLM | 71 (51/20) | 78 (215/78 合并关闭) | (78)/(78+215)=26.6% | 3 (v1.91.1, v1.92.0-rc.2, v1.93.0-dev.1) | 🟡 高频发布，MCP 网关安全修复加速，但待合并 PR 堆积 |
| Temporal | 未明确 (新开/活跃数未给) | 65 (37/28) | 43.1% | 2 (v1.31.2, v1.30.6) | 🟢 专注核心功能（Nexus/CHASM），稳定性好 |

> **注**：OpenClaw 与 Hermes Agent 的 PR 总量并列最高（均为500），但 OpenClaw 的关闭比例显著更低，说明维护者审查能力不足或社区贡献质量参差。

---

## 3. OpenClaw 在生态中的定位

- **规模领跑**：单日 Issues/PR 交互量达 1000 条，远超其他项目，是社区话语权最大的个人 AI 助手框架。
- **技术路线**：主打多 Agent 会话编排、音视频集成（Google Meet 修复）、原生 Anthropic 路径支持，意图成为“全能型个人助理操作系统”。
- **劣势**：合并效率仅 17.4%，P0/P1 钻石级 Bug（会话状态丢失、Thinking 块签名失效、性能回退）长期无修复 PR，导致用户满意度下降；大量 PR 积压（413条）反映社区贡献者积极性与管理能力的失衡。
- **与竞品对比**：相比 Hermes Agent 的“Kanban 工作流+桌面端”定位，OpenClaw 更侧重 **即时交互场景**（消息、会议），但稳定性让位于功能堆砌。Hermes 的合并率高出 13 个百分点，在交付质量上更健康。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 | 生态信号 |
|----------|----------|----------|----------|
| **会话状态持久化与可靠性** | OpenClaw, Hermes, Pi, OpenHands | 子 Agent 结果丢失、重复消息、心跳路由错误、暂停/恢复无响应 | 多 Agent 协调的“容错死结”仍是普遍瓶颈 |
| **模型推理内容流式兼容性** | OpenClaw, Pi, LiteLLM | Anthropic thinking 块签名失效、OpenAI reasoning_content 格式错乱、DeepSeek V4 崩溃 | 推理模型格式碎片化，需要中间层适配规范 |
| **MCP / 工具互联协议** | LiteLLM, Hermes, OpenHands | MCP 网关流式丢失、MCP 工具零解析、技能双重注入 | MCP 正在成为事实上的 Agent 工具互操作标准 |
| **配置热更新与持久化** | OpenClaw, Hermes, OpenHands | 模型切换不生效、LLM 超时重置、只读配置锁 | 配置管理是生产环境部署的盲区 |
| **安全与供应链** | OpenClaw, LiteLLM, Temporal | gh-issues 注入、PyPI 恶意包、Docker 签名强化 | 安全事件加速社区对发布流水线零信任改造 |

---

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent | OpenHands SDK | Pi | LiteLLM | Temporal |
|------|----------|--------------|---------------|----|---------|----------|
| **功能侧重** | 多Agent会话、音视频集成、全栈助手 | Kanban工作流、桌面App、MCP工具桥 | Agent技能标准化、ACP协议、SDK解耦 | 轻量TUI、模型快速适配、日常效率 | LLM网关、多模型路由、成本/安全管控 | 分布式工作流状态管理、复制与恢复 |
| **目标用户** | 个人开发者、重度AI用户 | 个人开发者、企业自动化团队 | 技能/AI应用开发框架 | 终端用户、CLI爱好者 | DevOps、企业LLM运维团队 | SRE、后端架构师 |
| **技术架构** | 单体+多Agent运行时 | 模块化插件、独立桌面端 | 纯SDK（无服务端） | 轻量TUI+配置化 | 代理层（无状态） | 有状态分布式引擎 |
| **成熟度** | 功能丰富但稳定性欠缺 | 快速迭代中（v0.18） | 相对成熟（v1.33） | 早期（v0.80） | 高度成熟（v1.91） | 高度成熟（v1.31） |
| **合并效率** | 17.4%（低） | 30.4%（中） | 41.7%（高） | 85.7%（极高） | 26.6%（中低） | 43.1%（高） |

---

## 6. 社区热度与成熟度分层

| 层级 | 项目 | 特征 | 阶段判断 |
|------|------|------|----------|
| **🔥 极高热度·快速迭代** | OpenClaw, Hermes Agent | 日更新>500 PR，Issues讨论激烈，功能与Bug并行爆发 | **功能扩张阶段**，但OpenClaw面临稳定性拐点 |
| **🔥 高热度·稳定发布** | LiteLLM, Temporal | 日更新50-80 PR，版本发布高频，功能重点明确 | **质量巩固+新特性平衡阶段** |
| **🌱 中等活跃·聚焦打磨** | Pi, OpenHands SDK | 日更新<50 PR，合并率>40%，Bug修复为主 | **体验优化阶段**，适合寻求稳定性的用户 |

> **解读**：OpenClaw 虽用户基数最大，但若不能解决合并效率与 Bug 积压，可能促使部分贡献者流向 Hermes Agent 或收敛到 LiteLLM/Temporal 等更成熟工具链。

---

## 7. 值得关注的趋势信号

1. **会话状态管理成为生态瓶颈**：多个项目（OpenClaw 会话死锁、Hermes 子Agent静默丢失、Pi 无响应会话）反复暴露同一类问题，说明当前 Agent 架构缺乏经过验证的“会话容错模式”。开发者应考虑引入补偿事务、预写日志等经典分布式系统策略。

2. **推理模型输出格式标准化刻不容缓**：OpenAI `reasoning_content`、Anthropic `thinking` 块、DeepSeek 思维模式碎片化输出，导致客户端不得不各自适配。对工具链开发者而言，建议采用 **“独立推理通道”** 设计，避免与文本流混用。

3. **MCP 协议正从“可选”走向“必备”**：LiteLLM 将 MCP 网关作为核心功能大修，Hermes 和 OpenHands 也在积极整合。未来 Agent 间互联很可能以 MCP 为通语，建议优先支持 MCP 标准端点的中间件。

4. **供应链安全从“奢侈配置”变为“硬性启动条件”**：LiteLLM 恶意包事件（#24512 获 798👍）催生了 cosign 签名、Docker 镜像验证等强制措施。所有开源项目都应纳入自动签名、SBOM 生成、第三方依赖扫描到 CI 流水线。

5. **工作流暂停与资源控制需求从基础设施蔓延到 Agent 层**：Temporal 的长期 Issue #3006 指向工作流暂停，类似诉求在 OpenClaw 的 steer 模式注入、Hermes 的 Kanban 子任务暂停中也有所体现。用户期望 Agent 具有“可中断、可恢复”的细粒度控制，而不仅仅是“继续/终止”二元能力。

---

**总结建议**：
- 对 **技术决策者**：若追求生产稳定性，优先选择 LiteLLM（网关层） + Temporal（状态层） 组合，Agent 框架可基于 Hermes Agent（合并效率更高）或等待 OpenClaw

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据您提供的 GitHub 数据生成的 **Hermes Agent 项目动态日报**。

---

# Hermes Agent 项目动态日报 | 2026-07-09

## 1. 今日速览

今日项目社区活跃度极高，呈现明显的“高产出、高讨论”态势。过去24小时内，共有 **252条 Issues 更新** 和 **500条 PR 更新**，其中待合并的 PR 高达348条，显示维护团队和社区贡献者正在密集进行功能开发与代码合入。新发布了 **v0.18.2** 补丁版本。值得注意的是，大量 PR 围绕 **Kanban 看板系统** 和 **Python 3.14 兼容性** 展开，表明项目在核心工作流调度和前瞻性兼容上投入了显著精力。整体来看，项目正处于一个快速迭代、问题修复与功能增强并行的阶段。

## 2. 版本发布

- **Hermes Agent v0.18.2 (v2026.7.7.2)**
  - **发布日期**: 2026年7月7日
  - **更新内容**: 这是一个针对 v0.18.1 的当日补丁版本。核心修复是解决了在标记版本 Docker 构建中，因不当固定 Baileys 库的 git 提交版本而引发的问题。现在改用已发布至包管理器的稳定版 `7.0.0-rc13`。
  - **破坏性变更**: 无
  - **迁移注意事项**: 这是一个小版本补丁，用户按常规方式更新即可。对于使用 Docker 部署的用户，该修复能确保构建流程更稳定，Docker 运行不再因 Baileys 依赖而失败。

## 3. 项目进展

今日合并/关闭了 **152条 PR**（合并/关闭状态合计），推动了多项关键功能与稳定性改进：

- **核心功能与兼容性**:
  - `fix(agent): robust handling of context-window overflow on strict endpoints` [PR #61228](https://github.com/NousResearch/hermes-agent/pull/61228)：修复了与 vLLM 等严格 OpenAI 兼容端点的上下文窗口溢出问题，增强了模型适配性。
  - `feat(api): backend-acknowledged session model lock with runtime routing` [PR #61236](https://github.com/NousResearch/hermes-agent/pull/61236)：为 API 客户端（如浏览器扩展）新增会话级模型锁定功能，可指定每轮对话的模型提供商，高级功能进一步增强。
  - `feat(tools): add guarded codex exec bridge` [PR #61223](https://github.com/NousResearch/hermes-agent/pull/61223)：新增一个受保护的 `codex_exec` 工具，允许在保持授权和沙箱环境下将仓库工作委托给 Codex CLI，扩展了 Agent 的能力边界。

- **Kanban 看板系统大规模修复**：今日共有超过 **10个 PR** 专注于 Kanban 系统的 Bug 修复与优化，包括：
  - 修复子任务继承父任务优先级的问题 [PR#61232](https://github.com/NousResearch/hermes-agent/pull/61232)
  - 修复工作人员工作目录临时文件溢出 `/tmp` 的问题 [PR#61234](https://github.com/NousResearch/hermes-agent/pull/61234)
  - 修复模型覆盖参数在 Spawn 子命令中传递错误的问题 [PR#61235](https://github.com/NousResearch/hermes-agent/pull/61235)
  - 这些修复极大地提升了 Kanban 系统的健壮性，是工作流自动化的关键一步。

- **平台与桌面体验**:
  - `fix(web): harden desktop webapp chat and mobile controls` [PR #60829](https://github.com/NousResearch/hermes-agent/pull/60829)：强化了桌面应用在作为 WebApp 时的安全性和移动端控制能力。
  - `fix(desktop): re-apply UI zoom after minimize/restore on Windows` [PR #61245](https://github.com/NousResearch/hermes-agent/pull/61245)：修复了 Windows 桌面端窗口缩放比例在最小化/恢复后回弹的 Bug，改善用户体验。

## 4. 社区热点

今日讨论最活跃的 Issue 和 PR 反映了社区对以下核心能力的强烈诉求：

- **数据持久化与扩展性**：
  - **[Issue #23717](https://github.com/NousResearch/hermes-agent/issues/23717) (13条评论，P2)**: 关于“可插拔 SessionDB 提供商”的 RFC。社区正在积极讨论如何支持 PostgreSQL 和 MySQL 等外部数据库，以解决 SQLite 在热更新和并发场景下的“死循环”问题。这反映出用户对于生产环境高可靠性和扩展性的强烈需求。

- **基础设施与集成**：
  - **[Issue #34390](https://github.com/NousResearch/hermes-agent/issues/34390) (12条评论，P3)**: 请求为 Dashboard 添加 `--allowed-hosts` 标记，以便更好地支持反向代理和 Tailscale 访问。这显示出用户将 Hermes Agent 作为核心服务部署，并通过外部工具暴露访问的趋势。

- **模型支持与工具调用**：
  - **[Issue #6626](https://github.com/NousResearch/hermes-agent/issues/6626) (11条评论，4 👍)**: 关于 Gemma 4 模型工具调用支持的问题。用户报告了集成时的解析器和配置问题，表明社区对新模型（尤其是本地部署的模型）的支持非常关注，并且愿意作为先锋进行尝试。
  - **[Issue #37619](https://github.com/NousResearch/hermes-agent/issues/37619) (6条评论，7 👍)**: Windows 桌面端缺少缩放/UI缩放功能。虽然评论不多，但点赞数高，表明这是一个普遍影响 Windows 用户体验的痛点。

## 5. Bug 与稳定性

今日报告的 Bug 问题中，以下几个值得高度关注，已出现对应的修复 PR。

- **P1 (严重)**:
  - **[Issue #51587](https://github.com/NousResearch/hermes-agent/issues/51587) (已关闭)**: MCP 服务器工具连接成功但无法在 Agent 会话中使用。该问题已被标记为已解决（关闭），直接影响 MCP 生态集成。
  - **[Issue #55578](https://github.com/NousResearch/hermes-agent/issues/55578) (已关闭)**: Desktop 端异步委托完成任务会导致会话状态不一致（旧会话复活、新会话创建问题）。该问题已被修复，对多轮复杂任务场景影响较大。

- **P2 (高)**:
  - **[Issue #53443](https://github.com/NousResearch/hermes-agent/issues/53443) (5条评论)**: QQ 机器人适配器的 `connect()` 方法缺少 `is_reconnect` 参数，导致每次启动都报错。**已有重复报告 Issue #58646，但尚未看到直接修复 PR。**
  - **[Issue #59224](https://github.com/NousResearch/hermes-agent/issues/59224) (8条评论)**: Classic CLI 的 `/resume` 列表仅显示来源为 `cli` 的会话，隐藏了桌面、WebUI 等其他来源的会话，误导用户。
  - **[Issue #32617](https://github.com/NousResearch/hermes-agent/issues/32617) (5条评论)**: 切换模型提供商到 xAI OAuth 时，因重放旧的加密内容导致授权失败，影响会话连续性。
  - **[Issue #60821](https://github.com/NousResearch/hermes-agent/issues/60821) (5条评论, 最新创建)**: 在 OpenRouter 等第三方 OpenAI 兼容端点，`Completions.create()` 因接收到非预期的 `system` 参数而崩溃。**已有重复报告 Issue #61030，这是一个新的、紧急的回归问题。**

- **稳定性修复 PR**:
  - **[PR #61227](https://github.com/NousResearch/hermes-agent/pull/61227)**: 修复了检查点（checkpoint）垃圾回收在多并发会话下的 `dangling ref` 问题（P2）。
  - **[PR #61224](https://github.com/NousResearch/hermes-agent/pull/61224)**: 包含三个针对 Python 3.14 兼容性的修复，表明项目正在积极拥抱未来 Python 版本以确保稳定性。
  - **[PR #61244](https://github.com/NousResearch/hermes-agent/pull/61244)**: 修复轨迹压缩器在并发处理时，某个任务超时可能导致整个 `asyncio.gather` 崩溃的问题。

## 6. 功能请求与路线图信号

今日社区提出的功能请求中，以下需求反映了未来的发展方向：

- **外部数据库集成**：**[Issue #23717](https://github.com/NousResearch/hermes-agent/issues/23717)** 要求支持可插拔的 SessionDB，如 PostgreSQL、MySQL。这是规模化部署的关键需求，可能与路线图中的“企业级部署”或“高可用性”阶段相关。
- **Vault/密钥管理**：**[Issue #22791](https://github.com/NousResearch/hermes-agent/issues/22791) (13 👍)** 请求集成 Infisical 作为外部 Vault 后端。这是之前“外部Vault”计划的子任务，呼声很高，有可能在下一版本中被考虑。
- **本地模型与工具链**：**[Issue #523](https://github.com/NousResearch/hermes-agent/issues/523)** (4条评论, 3 👍) 提出创建一个“本地模型设置技能”，以简化 Ollama、llama.cpp、vLLM 等本地运行时的配置。这符合“让 Agent 更易本地运行”的社区趋势。
- **代理 (Proxy) 支持**：**[Issue #5454](https://github.com/NousResearch/hermes-agent/issues/5454)** (6条评论) 要求为所有 LLM API 调用提供统一的代理支持。这是企业用户和特定网络环境下用户的刚需。

## 7. 用户反馈摘要

从今日的 Issue 评论中，可以提炼出以下几点真实的用户声音：

- **痛点：MCP 工具集成体验问题**：在 **[Issue #51587](https://github.com/NousResearch/hermes-agent/issues/51587)** 中，用户感到沮丧：“配置的 MCP 服务器成功连接并启用了工具，但代理的会话工具集中根本没有它们。” 这暴露了 MCP 集成流程中缺乏清晰的反馈和验证机制，用户期望有更好的发现（descovery）或诊断（diagnostics）。
- **痛点：Windows 桌面应用中文支持不佳**：**[Issue #39534](https://github.com/NousResearch/hermes-agent/issues/39534)** 的用户提供了一个非常生动的例子：输入的中文 prompt 在发送后在窗口中被截断/显示异常。这直接影响了中文用户群体的核心体验，可能是字体渲染或文本换行逻辑的问题。
- **痛点：自定义模型配置不透明**：**[Issue #40480](https://github.com/NousResearch/hermes-agent/issues/40480)** 的用户指出，通过 CLI 配置的“自定义 OpenAI 兼容提供商”的模型，在 Desktop 应用的下拉菜单中不可见。“CLI 能用，但 UI 里没有”造成了混乱，说明 Desktop App 的配置同步存在盲区。
- **反馈：Kanban 工具分配逻辑不清晰**：**[Issue #61230](https://github.com/NousResearch/hermes-agent/issues/61230) (对应修复 PR)** 的 PR 摘要中提到“代理调用 kanban_create 时可靠地猜到了看似合理但实际不存在的分配者姓名，导致任务永远停留在 ready 状态”。这揭示了一个微妙的 UX 问题：模型会尝试智能分配但失败，用户（或开发者）需要更明确的指引或自动回退逻辑。

## 8. 待处理积压

以下为长时间未关闭或尚未有明确回复的重要 Issue，提醒维护者关注：

- **[Issue #5454](https://github.com/NousResearch/hermes-agent/issues/5454) (创建于 2026-04-06)**：“代理支持 LLM API 调用”。已开放三个月有余，涉及广泛的用户群体（如企业用户），但评论数不多，关注度可能被低估。其优先级（P2）暗示其重要性，但可能被更紧急的功能（如 MCP）压制。
- **[Issue #37619](https://github.com/NousResearch/hermes-agent/issues/37619) (创建于 2026-06-02)**：“Windows 桌面应用添加缩放/ UI 缩放支持”。虽是 P3 但获得 7 👍，是 Windows 用户的普遍诉求。随着桌面应用用户增多，该需求的优先级应该提升。
- **[Issue #19986](https://github.com/NousResearch/hermes-agent/issues/19986) (创建于 2026-05-05)**：“使非核心捆绑技能可选并保持默认安装最小化”。这是一个长期存在的、关于项目安装体积和模块化的讨论，需要项目组做出路线图决策。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-07-09

---

## 1. 今日速览

过去 24 小时项目保持 **高活跃度**：13 条 Issue 更新（8 条新开/活跃，5 条已关闭）、24 条 PR 更新（14 条待合并，10 条已合并/关闭），并正式发布 **v1.33.0**。社区讨论集中在 **技能/配置文件架构** 的重构（#4017、#4019、#4029）以及多项 **稳定性修复**（LLM 流式回调、Windows UTF-8 解码、LLM 超时持久化）。整体来看，SDK 正在向更健壮的技能管理与客户端-服务端分离方向迈进。

---

## 2. 版本发布

### v1.33.0 — 2026-07-08

- **变更内容**：
  - 修复：在异步 LLM 调用期间释放会话状态锁（`#4009`）
  - 文档：修正 DEVELOPMENT.md 中的 clone URL 及仓库布局名称（`#4021`）
- **破坏性变更**：无
- **迁移注意事项**：无特殊要求，建议升级以获取锁释放改进。

**GitHub Release**：https://github.com/OpenHands/software-agent-sdk/releases/tag/v1.33.0

---

## 3. 项目进展

今日合并/关闭的重要 PR 推动了以下能力提升：

| PR | 说明 | 状态 |
|---|---|---|
| [#4018](https://github.com/OpenHands/software-agent-sdk/pull/4018) | 技能选择改为 **拒绝列表（deny-list）** 模式，去除嵌入式技能，统一 ACP 与 OpenHands 路径 | 已合并 |
| [#4027](https://github.com/OpenHands/software-agent-sdk/pull/4027) | 自动化组件随 SDK 版本发布自动 bump，消除版本漂移 | 已合并 |
| [#4033](https://github.com/OpenHands/software-agent-sdk/pull/4033) | 修正种子默认 AgentProfile 生成“幽灵”LLM 配置的问题 | 已合并 |
| [#4025](https://github.com/OpenHands/software-agent-sdk/pull/4025) | 支持根目录 `SKILL.md` 的单技能插件加载（拓展私有市场） | 已合并 |
| [#3974](https://github.com/OpenHands/software-agent-sdk/pull/3974) | 清理已废弃的 CI 工作流（api-compliance、condenser） | 已合并 |
| [#4036](https://github.com/OpenHands/software-agent-sdk/pull/4036) | 防止 Laminar 初始化重复报错 | 已合并 |

这些更新显著增强了 **技能/配置的一致性**、**CI 整洁度** 以及 **LLM 配置文件的生命周期管理**。

---

## 4. 社区热点

以下 Issues/PR 讨论最为活跃：

- **[#4017](https://github.com/OpenHands/software-agent-sdk/issues/4017)**（4 评论）— 用户 @simonrosenberg 系统性地提出 AgentProfile 解析的 **多个根因缺陷**（无执行工具、无技能、无流式回调）。社区围绕统一默认值与覆盖逻辑展开深入讨论，并催生了 #4018 的拒列设计与后续 #4029 的客户端覆盖需求。
- **[#4019](https://github.com/OpenHands/software-agent-sdk/issues/4019)**（3 评论）— 关注 ACP 模式下项目技能被重复注入的问题，用户担心 ACP CLI 已自行摄取 `AGENTS.md`，而 SDK 又主动加载一遍导致冲突。开发者已意识到需要更精确的控制。
- **[#4039](https://github.com/OpenHands/software-agent-sdk/issues/4039)**（1 评论）— 关于 `LLM.stream=True` 时内部调用者（condenser、标题生成器）未传递 `on_token` 回调引发的异常。虽已关闭，但社区关注到该设计可能影响高级流式场景。

**背后诉求**：用户对 AgentProfile 与技能配置的 **一致性** 和 **可预测性** 有强烈需求，期望客户端与服务端之间的边界清晰，避免配置漏传或重复加载。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue | 问题描述 | 是否已有修复 PR |
|---|---|---|---|
| **高** | [#4032](https://github.com/OpenHands/software-agent-sdk/issues/4032) | LLM 配置文件超时在 agent-server 重启后重置为默认值，导致长任务中断 | 是 — [#4028](https://github.com/OpenHands/software-agent-sdk/pull/4028) |
| **高** | [#4034](https://github.com/OpenHands/software-agent-sdk/issues/4034) | Windows 上恢复会话时因 `base_state.json` 未指定 UTF-8 编码导致 `UnicodeDecodeError`（如含俄文/重音字符） | 是 — [#4035](https://github.com/OpenHands/software-agent-sdk/pull/4035) |
| **中** | [#4039](https://github.com/OpenHands/software-agent-sdk/issues/4039) | `LLM.stream=True` 时内部调用缺失 `on_token` 回调，引发异常（已在 v1.33.0 之前修复） | 已关闭，已在相关 PR 修复 |
| **低** | [#4031](https://github.com/OpenHands/software-agent-sdk/issues/4031) | 种子默认 AgentProfile 创建了一个“幽灵”LLM 配置（占位模型 `gpt-5.5`）持久化，可能误导用户 | 是 — [#4033](https://github.com/OpenHands/software-agent-sdk/pull/4033) |

其中 **#4032** 和 **#4034** 属于影响实际使用的回归，修复 PR 均已提交并进入审核。

---

## 6. 功能请求与路线图信号

- **[#4038](https://github.com/OpenHands/software-agent-sdk/issues/4038)** — 建议用 **类型化设计** 替换路径规则注入中的隐式 `getattr(action, "path")` 合约，提升可维护性与类型安全。
- **[#4029](https://github.com/OpenHands/software-agent-sdk/issues/4029)** + **[#4030](https://github.com/OpenHands/software-agent-sdk/pull/4030)** — 允许客户端在 `agent_profile_id` 路径上提供 **启动时覆盖**（如运行时服务配置），已在 PR 实现中。
- **[#4017](https://github.com/OpenHands/software-agent-sdk/issues/4017)** — 系统性地简化 AgentProfile 解析：默认值 + 覆盖模式，并合并技能模型（已部分纳入 #4018）。
- **[#3994](https://github.com/OpenHands/software-agent-sdk/pull/3994)** — 增加 **路径触发技能**（类似 Claude Code Rules），仍为 Draft 状态，预计需要更多讨论。
- **[#2911](https://github.com/OpenHands/software-agent-sdk/pull/2911)** — 长期 PR，增加 `ToolShieldLLMSecurityAnalyzer` 安全分析功能，虽未合并但属于路线图中的安全增强模块。

**风向**：下一版本很可能包含 **客户端覆盖机制**、**类型化路径合约** 以及 **更完善的技能加载规则**。

---

## 7. 用户反馈摘要

从今日 Issue 及评论中提炼的真实用户痛点与场景：

- **Windows 用户**（[#4034](https://github.com/OpenHands/software-agent-sdk/issues/4034)）反馈恢复包含非 ASCII 字符的会话时直接崩溃，@shneydermanmm 提到“只有重新启动容器才能继续使用”，体验极差。
- **自托管用户**（[#4039](https://github.com/OpenHands/software-agent-sdk/issues/4039)）使用自定义 OpenAI 兼容后端（LiteLLM + vLLM）时，因内部 LLM 调用未传 `on_token` 导致流式功能全局失效，被迫关闭 `stream=True`。
- **Canvas 用户**（[#4031](https://github.com/OpenHands/software-agent-sdk/issues/4031)）发现种子配置创建了一个名为 `default`、模型 `gpt-5.5` 且无 API key 的幽灵配置，开发者 @simonrosenberg 直指其“永久持久化了一个占位符”，影响实际使用。
- **ACP 集成用户**（[#4019](https://github.com/OpenHands/software-agent-sdk/issues/4019)）指出项目技能被双重加载，希望 ACP CLI 与 SDK 的职责边界更清晰。

**满意点**：用户对 #4018 的拒绝列表方案表示认可，认为比之前的“正选+硬编码”模式更灵活。

---

## 8. 待处理积压

以下 Issue / PR 长期未得到响应或合并，需维护者关注：

| 项目 | 创建时间 | 简述 | 建议行动 |
|---|---|---|---|
| [#2911](https://github.com/OpenHands/software-agent-sdk/pull/2911) | 2026-04-21 | `ToolShieldLLMSecurityAnalyzer` 安全分析 PR，超过 2.5 月未合并 | 安排代码审查，评估与现有安全模块的整合 |
| [#3266](https://github.com/OpenHands/software-agent-sdk/pull/3266) | 2026-05-15 | 空闲终端会话驱逐机制，提升资源回收效率 | 解决冲突或督促作者更新 |
| [#3969](https://github.com/OpenHands/software-agent-sdk/pull/3969) | 2026-07-02 | 处理 OpenAI 设备授权限速，避免 500 错误 | 审核未通过？需要作者补充测试 |
| [#3994](https://github.com/OpenHands/software-agent-sdk/pull/3994) | 2026-07-05 | 路径触发技能（Draft），功能需求明确但需重新评估 API 设计 | 邀请架构组讨论并决定是否进入下一个里程碑 |
| [#2078](https://github.com/OpenHands/software-agent-sdk/issues/2078) | 2026-02-14 | 日常集成运行 tracker（132 条评论），持续更新但无人关闭，建议评估是否仍需要 | 考虑关闭或转为里程碑式追踪 |

---

*日报生成时间：2026-07-09 09:00 UTC，数据基于 GitHub 公开活动。*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，以下是根据您提供的 Pi 项目 GitHub 数据生成的 2026-07-09 项目动态日报。

---

# Pi 项目动态日报 | 2026年7月9日

## 1. 今日速览

过去24小时内，Pi 项目维持了极高的活跃度，共处理了43条 Issue 和7个 PR。项目核心团队与社区贡献者高效协作，快速关闭了大量 Issue（37条）和 PR（6条），修复了包括 **Fork 菜单误操作、Linux 剪贴板失效、OpenAI 推理内容显示异常** 在内的多个关键 Bug。同时，针对 **Copilot 上下文窗口、代理会话行为** 等功能的优化补丁也已合并。尽管没有新版本发布，但大量 Bugfix 的落地使项目稳定性得到显著提升。社区讨论集中在 **会话管理** 和 **模型兼容性** 两大主题上。

## 2. 版本发布

*无新版本发布。*

## 3. 项目进展

今日项目进展显著，多项重要修复和功能改进已合并至主分支：

- **修复 Copilot 扩展上下文支持**：PR [#6437](https://github.com/earendil-works/pi/pull/6437) 已合并，根据 GitHub 官方公告，更新了 Copilot 模型的上下文窗口至1,000,000 tokens。用户现在可以无缝使用 Copilot 的扩展上下文功能。
- **优化 Fork 菜单交互**：PR [#6430](https://github.com/earendil-works/pi/pull/6430) 修复了用户在选择 Fork 分支时，因扩展拖慢进程而产生的“双击”误操作，避免生成多余会话。
- **修复 Linux 剪贴板粘贴问题**：PR [#6418](https://github.com/earendil-works/pi/pull/6418) 解决了 Linux/X11 环境下 Bun 编译版本中 `Ctrl+V` 粘贴图片无效的问题，通过回退到 `xclip` 工具作为备用方案。
- **修复推理/思考内容渲染**：PR [#6436](https://github.com/earendil-works/pi/pull/6436) 已合并，解决了 OpenAI Responses 推理内容中出现的空提示和多余标记问题，提升了 TUI 显示体验。
- **支持 JSONL 会话自定义元数据**：PR [#6417](https://github.com/earendil-works/pi/pull/6417) 已合并，在 V3 JSONL 会话头中增加了可选的 `metadata` 字段，为三方扩展和工具链集成提供了更大的灵活性。
- **增强本地版本信息**：PR [#6413](https://github.com/earendil-works/pi/pull/6413) 已合并，现在本地运行版本会显示 Git 信息，便于问题追踪。

这些合并的PR表明项目正在快速修复用户体验方面的痛点，并持续优化代码质量和扩展性。

## 4. 社区热点

- **#5700 支持多实时代理会话与 TUI 切换**：此 Issue 获得了9条评论，虽已关闭，但代表了社区对**多会话并发管理**的强烈需求。用户希望在后台运行一个代理会话的同时，在TUI中处理另一个，而不必关闭现有会话。这反映了从“单线程”到“多任务”的使用习惯演进。
  [链接](https://github.com/earendil-works/pi/issues/5700)

- **#5263 将会话内模型和思考层级变更设为默认临时的**：该 Issue 仍处于开放状态，获得了6个👍，是社区讨论的焦点。用户希望“会话内”的模型切换是临时和瞬态的，不影响全局默认设置。这背后是用户对**配置灵活性与可控性**的追求，期望能快速试验不同模型而不污染个人配置。
  [链接](https://github.com/earendil-works/pi/issues/5263)

- **#6204 mimo-v2-omni 是小米 MiMo Token 计划提供商中的“幽灵模型”**：获得了7条评论，反映了**模型与提供商兼容性**的常见痛点。用户在选择模型时，列表中存在但实际端点不支持会导致报错，这降低了对模型列表的信任度。社区期待更实时准确的模型可用性校验。
  [链接](https://github.com/earendil-works/pi/issues/6204)

## 5. Bug 与稳定性

今日报告的 Bug 集中在以下几个方面，按严重程度排序：

**严重 (Crash/Functionality Broken)**
- **DeepSeek V4 + 思维模式导致会话崩溃 (v0.80.3回归) [#6433](https://github.com/earendil-works/pi/issues/6433)**：使用 DeepSeek 模型并开启思考模式时，程序无声退出，是上一个版本的回归问题。需要紧急排查。
- **OpenAI Responses 模型自动压缩后 `max_output_tokens=1` 导致请求失败 [#6429](https://github.com/earendil-works/pi/issues/6429)**：会话自动压缩功能会写入一个不合理的输出 token 限制，导致后续所有 API 请求失败，影响使用连续性。
- **Gemini 工具调用通过 `streamProxy` 时因缺少 `thoughtSignature` 而失败 [#6414](https://github.com/earendil-works/pi/issues/6414)**：这是一个多代理交互场景下的严重协议兼容性问题。

**高 (User Experience Degraded)**
- **切换到小上下文模型时因未预压缩而导致请求溢出 [#6426](https://github.com/earendil-works/pi/issues/6426)**：模型切换时缺少前置压缩处理，导致第一次请求就会失败。
- **`/fork` 命令在 Fork 过程中允许用户多次选择，生成多余会话 [#6321](https://github.com/earendil-works/pi/issues/6321)**：此问题已有 PR [#6430](https://github.com/earendil-works/pi/pull/6430) 修复。
- **Linux/X11 下 `<Ctrl+V>` 图片粘贴失效 (v0.80.3回归) [#6250](https://github.com/earendil-works/pi/issues/6250)**：此问题已有 PR [#6418](https://github.com/earendil-works/pi/pull/6418) 修复。

**中 (Minor/Configuration)**
- **只读配置文件锁错误 [#6406](https://github.com/earendil-works/pi/issues/6406)**：将配置文件放在只读磁盘上会导致凭证读取失败，影响安全部署场景。
- **Git 交互式变基卡住 [#6432](https://github.com/earendil-works/pi/issues/6432)**：在使用 Git 编码工作流时，Agent 在完成冲突解决后卡住。

## 6. 功能请求与路线图信号

- **会话与模型管理**：Issue [#5263](https://github.com/earendil-works/pi/issues/5263) 关于“临时模型切换”的提议，与近日合并的 `metadata` 支持 (PR [#6417](https://github.com/earendil-works/pi/pull/6417)) 目的一致，表明项目正在向更精细的会话控制演进。PR [#6427](https://github.com/earendil-works/pi/pull/6427)（开放中）增加对提示缓存命中/未命中的追踪，符合社区对于性能和成本优化的期待，很可能进入下个版本。
- **提供商扩展**：用户明确请求将 **Novita AI** 作为内置提供商 [#6420](https://github.com/earendil-works/pi/issues/6420)，以及为 **Anthropic OAuth** 添加 **Claude Agent billing 标记** [#6421](https://github.com/earendil-works/pi/issues/6421)。这表明社区对平台多样性和兼容性的持续需求。
- **开发者体验**：用户请求导出 `InMemorySessionStorage` 实现 [#6435](https://github.com/earendil-works/pi/issues/6435)，以及对 `generate-image-models.ts` 脚本的输出格式进行标准化 [#6419](https://github.com/earendil-works/pi/issues/6419)，反映了社区中有开发者希望基于Pi进行二次开发的趋势。

## 7. 用户反馈摘要

- **满意度提升**：社区对于 Bug 修复的速度表示认可，特别是针对 `Ctrl+V` 粘贴问题和 Fork 菜单交互问题，相关 Issue 在有了修复 PR 后迅速被标记为待合并。
- **对性能优化的期待**：多个针对压缩、回退、上下文管理的 Bug（如 [#6425](https://github.com/earendil-works/pi/issues/6425), [#6424](https://github.com/earendil-works/pi/issues/6424), [#6426](https://github.com/earendil-works/pi/issues/6426)）均来自同一位用户 `@Blue-B`，显示资深用户会遇到长会话、大上下文场景下的性能瓶颈，并对此有明确的优化思路。
- **对稳定性的关切**：用户 `@daniel-ospina` 报告 DeepSeek V4 的崩溃是一个“回归”，这引起了社区对版本升级是否会引入新 Bug 的普遍担忧。
- **文档与错误信息改进**：用户对“幽灵模型” [#6204](https://github.com/earendil-works/pi/issues/6204) 和错误重试逻辑 [#6431](https://github.com/earendil-works/pi/issues/6431), [#6303](https://github.com/earendil-works/pi/issues/6303) 的讨论，反映出用户期待更精确和可操作的错误信息，以帮助他们自行排查问题。

## 8. 待处理积压

- **经典功能请求**：Issue [#5263](https://github.com/earendil-works/pi/issues/5263) (“将会话内模型和思考层级变更设为默认临时的”) 获得6个赞，评论活跃，但依然处于开放状态。该功能若实现，将极大改善用户体验，建议项目组关注。
- **复杂 Bug 元问题**：Issue [#5886](https://github.com/earendil-works/pi/issues/5886) 讨论了一个与 Agent 会话状态和助手生命周期相关的复杂 Bug 类别。维护者 `@mitsuhiko` 参与了讨论，但至今未提出修复方案，需要持续跟踪。
- **未响应的 PR**：PR [#6427](https://github.com/earendil-works/pi/pull/6427) (feat(coding-agent): add prompt cache miss tracking) 由核心贡献者 `@mitsuhiko` 提出，目前为开放状态，但无任何评论。鉴于其价值，建议团队尽快进行 Review 和合并。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-07-09

---

## 1. 今日速览

过去 24 小时内，LiteLLM 项目保持极高活跃度：共处理 71 条 Issue（其中新开/活跃 51 条，关闭 20 条），合并/关闭 78 个 PR（待合并 215 个），并发布了 3 个新版本。社区讨论热度集中在 MCP（Model Context Protocol）网关、Anthropic `/v1/messages` 端点适配、安全与稳定性修复等方向。版本发布节奏稳健，从 `v1.91.1` 到 `v1.93.0-dev.1` 表明团队在持续推进功能迭代与质量改进。

---

## 2. 版本发布

今日发布了三个版本：

| 版本 | 类型 | 主要变化 |
|------|------|----------|
| **v1.93.0-dev.1** | 开发版本 | 基于主分支的最新开发版本，包含近期的 PR 合并内容 |
| **v1.92.0-rc.2** | 候选版本 | 在 RC.1 基础上修复了关键问题，即将进入稳定版 |
| **v1.91.1** | 稳定版本 | 紧急修补版本，主要包含安全性与稳定性修复 |

**⚠️ 破坏性变更与迁移注意事项：**
- 所有版本均包含 Docker 镜像签名的强制执行（`cosign`），从 `commit 0112e53` 开始使用统一签名密钥。请确保 CI/CD 流水线已更新为验证签名。
- 若从 `v1.82.x` 旧版本直接升级，需注意 `v1.91.1` 已移除对部分废弃端点的支持（如旧版 `/models` 路由），建议查阅 [CHANGELOG](https://github.com/BerriAI/litellm/blob/main/CHANGELOG.md) 确认兼容性。

*链接：* [v1.93.0-dev.1](https://github.com/BerriAI/litellm/releases/tag/v1.93.0-dev.1) · [v1.92.0-rc.2](https://github.com/BerriAI/litellm/releases/tag/v1.92.0-rc.2) · [v1.91.1](https://github.com/BerriAI/litellm/releases/tag/v1.91.1)

---

## 3. 项目进展

今日合并/关闭的重要 PR 集中在以下几个方面：

### 3.1 MCP 网关稳定性增强
- **PR #32567**（fix: reject MCP gateway requests that resolve zero tools）：拒绝解析出零工具的 MCP 请求，避免静默失败。
- **PR #32566**（fix: emit terminal error event on MCP tool-execution / follow-up failures）：当工具执行或后续 LLM 调用失败时，向流式响应发送终止错误事件，防止客户端挂起。
- **PR #32565**（fix: surface MCP gateway initial-call failures）：修复 MCP 网关初始调用失败时，不再发出损坏的流，而是直接返回错误。
- **PR #32556**（feat: relay upstream 401/403 on client-forwarded pass-through tool calls）：在客户端转发的透传工具调用中正确转发上游的 401/403 状态码。

**影响**：上述 PR 解决了 MCP 端到端流式传输中多个严重的错误吞没和状态无响应问题，使生产环境中 MCP 网关的可靠性和可调试性显著提升。

### 3.2 代理层权限与路由改进
- **PR #32560**（fix: let org and team admins update teams via /team/update）：允许组织管理员和团队管理员通过 API 更新团队，完善了多租户权限模型。
- **PR #32542**（fix: walk Responses-API text taxonomy in shared content helpers）：修复 Responses API 的文本分类在 guardrail 处理中的路径问题。
- **PR #32559**（test: add key TPM rate limiting scenarios）：新增关键 TPM 速率限制的场景化集成测试，覆盖高 TPM key 的请求验证。

### 3.3 价格数据与模型支持
- **PR #32549**（feat: add xai/grok-4.5 model pricing and metadata）：新增 xAI Grok-4.5 的定价与元数据，用户可直接调用。
- **PR #32550**（fix: forward realtime health check params）：修复 Vertex AI 实时端点健康检查参数未正确传递的问题。

### 3.4 内容安全与日志审计
- **PR #32533**（fix: log optional_rerank_params at debug to stop leaking request content）：将 rerank 参数日志级别改为 debug，避免敏感信息泄漏。

**整体进展**：项目在 MCP 网关、代理权限、实时端点兼容性及新模型支持方面均取得实质性推进，同时强化了测试覆盖和安全性。

---

## 4. 社区热点

### 4.1 🔥 长期悬而未决的安全事件讨论仍在持续
**Issue #24512**（已关闭）—— 关于 PyPI 包 `litellm==1.82.8` 中包含恶意 `litellm_init.pth` 文件的安全报告，虽然已关闭，但今日仍有新评论，累计 487 条评论、798 个 👍。社区持续追踪后续影响与官方修复进度。*链接：* [#24512](https://github.com/BerriAI/litellm/issues/24512)

### 4.2 🆕 MCP 网关流式错误处理引发广泛关注
**Issue #32562**（今日新开，1 条评论）—— 报告 MCP 网关流在工具执行失败时丢失终止事件，导致客户端无限等待。此问题立即被 PR #32566 修复，展示了项目快速响应能力。*链接：* [#32562](https://github.com/BerriAI/litellm/issues/32562)

### 4.3 🧠 Claude Code 与推理模型适配持续摩擦
**Issue #30765**（7 条评论）—— 报告 `/v1/messages` 流式响应中，思考块（thinking block）结束后第一个文本 delta 被丢弃，影响 Claude Code 客户端。类似问题还有 **Issue #32357**（2 条评论，👍 2）—— OpenAI 推理模型的 `reasoning_content` 被错误流式化为 Anthropic 格式，导致客户端收到空内容。*链接：* [#30765](https://github.com/BerriAI/litellm/issues/30765) · [#32357](https://github.com/BerriAI/litellm/issues/32357)

### 4.4 🔄 Bedrock 推理配置类问题反复出现
**Issue #26625**（已关闭，7 条评论）—— Bedrock Application Inference Profiles 的 prompt caching 被静默丢弃。**Issue #20589**（已关闭，7 条评论）—— 使用 Bedrock 推理 profile 时流式校验和不匹配（500 错误）。社区对 Bedrock 特殊 ARN 格式的支持需求迫切。*链接：* [#26625](https://github.com/BerriAI/litellm/issues/26625) · [#20589](https://github.com/BerriAI/litellm/issues/20589)

---

## 5. Bug 与稳定性

根据严重程度排列如下：

| 严重程度 | Issue | 描述 | 是否已有 fix PR |
|---------|-------|------|----------------|
| 🔴 阻塞 | #32562 | MCP 流式传输在工具执行失败后无终止事件，客户端挂起 | 已修复（PR #32566） |
| 🔴 阻塞 | #32335 | `/responses` API 在多轮对话中丢失 Reasoning Items，造成 400 错误（v1.83.7 回归） | 无 PR（需排查） |
| 🟠 高 | #30765 | `/v1/messages` 流式输出中思考块后的首段文字被丢弃 | 无 PR（讨论中） |
| 🟠 高 | #32357 | 推理模型 `reasoning_content` 被错误流式封装，客户端收到空 content | 无 PR（讨论中） |
| 🟠 高 | #32281 | MCP 工具转换丢弃 `function` 包装键，导致 `hosted_vllm` 返回 400 | 无 PR |
| 🟠 高 | #32484 | Docker 1.90.0 中出现大量“未解析成本信息”日志 | 无 PR |
| 🟡 中 | #32489 | `openai/chat_completions/*` 路由在自定义 `api_base` 下不工作 | 无 PR |
| 🟡 中 | #26322 | `azure_ai/mistral-large-3` 不支持 `max_completion_tokens` | 无 PR |
| 🟡 中 | #25323 | `least_busy.py` 路由算法导致部分端点的流量被压制到零 | 无 PR |
| 🟡 中 | #32324 | Valkey 语义缓存中 `_get_async_embedding` 参数传递错误 | 无 PR |
| 🟢 低 | #32474 | UI 中无法将用户预算重置为“无限制” | 无 PR |
| 🟢 低 | #30101 | Opus 4.7/4.8 通过 Vertex `@default` 后缀调用时模型名检测失败 | 无 PR |

**回归问题重点关注**：#32335 明确标注为 v1.83.7 回归，建议紧急定位并回退或修复。

---

## 6. 功能请求与路线图信号

### 6.1 🚀 多 API Key 轮换与搜索工具（#32118）
用户请求在 `search_tools` 中支持声明多个 API key，并利用 LiteLLM 现有路由策略（`simple-shuffle`、`least-busy` 等）进行轮换，遇到 429/配额耗尽时自动切换并冷却。该需求与 MCP 网关的透传能力结合，有望成为下一版本的企业级功能。

### 6.2 🧩 可验证代理身份头（#24904，已关闭但思路清晰）
建议 LiteLLM 代理层注入 `X-Agent-UID` 加密头，使下游系统可验证调用方身份。该功能对于安全审计和 AI 水印（WTRMRK）集成具有前瞻意义，但尚未有对应 PR。

### 6.3 🔄 Cache Control Injection Points 开关导致模型配置损坏（#31887）
用户在 Anthropic 模型设置中开启“Cache Control Injection Points”后，模型无法再次保存。这暴露出模型配置编辑 UI 的健壮性问题，需优先修复。

### 6.4 📊 团队用量统计的完整聚合（#21381 PR 已提交但停滞）
该 PR 新增 `/team/daily/activity/aggregated` 端点以解决团队用量报告只能获取第一页数据的问题，虽在 2 月提交但至今未合并，可能因路由冲突或测试未通过。

---

## 7. 用户反馈摘要

### 7.1 正面反馈
- **MCP 网关改进得到认可**：多位用户在 Slack 中确认 PR #32565、#32566 解决了他们遇到的“流式无响应”问题，期待快速合并。
- **安全事件响应速度**：虽然 #24512 是安全危机，但社区对版本 `1.82.9` 后引入的 cosign 签名和强化发布流程表示肯定。

### 7.2 痛点与不满
- **“零配置”变成负配置**：部分用户抱怨自动推理模型（如 DeepSeek-R1）在 LiteLLM 代理下无法正常使用，需要手动调整多项参数。**Issue #32357** 中，用户 @ketor 写道：“实验性适配器产生空内容，迫使开发者自己写兼容层。”
- **Azure 特定参数转换不足**：`max_tokens` → `max_completion_tokens` 的自动转换至今在 Azure gpt-4o 上失效（#24779 已关闭但未修复根本问题），用户 @hvdlinden 表示“每次都要手动 polyfill，很繁琐”。
- **仪表板预算管理缺陷**：用户 @premtiwari5008 在 #32474 中提到“预算一旦设置就无法改回无限，必须直接操作数据库，这不符合管理直觉。”

### 7.3 典型使用场景
- **Claude Code 企业部署**：多位用户将 LiteLLM 作为代理层用于 Claude Code，需要稳定的 `/v1/messages` 端点和 Bedrock 推理配置支持。
- **多模型路由与成本管控**：团队使用 `least_busy` 或 `order-based` 路由在多个 LLM 服务间分配流量，但路由算法存在 Bug（如 #25323）。
- **MCP 工具集成**：开发者通过 LiteLLM 的 MCP 网关将外部工具连接到 LLM，希望在代理层统一管控。

---

## 8. 待处理积压

### 8.1 长期未响应的重要 Issue
| Issue | 标签 | 最后更新 | 备注 |
|-------|------|----------|------|
| #17696 | Gemini 缓存 token 过少时请求失败 | 2026-07-08 | 5 条评论，无官方回复已 7 个月 |
| #20793 | `reasoning_effort` 导致 KeyError（PR 已提交但停滞） | 持续更新 | PR 未被审核，关键功能缺陷 |
| #21363 | DashScope 多模态消息被丢弃（PR 已提交） | 持续更新 | 影响阿里云用户 |
| #21379 | `supports_structured_outputs` 标志重构（PR 已提交） | 持续更新 | 解决硬编码模型名问题 |
| #21384 | 更新对象时缺失 premium feature 字段名提示（PR 已提交） | 持续更新 | 改善企业用户使用体验 |
| #21385 | `request_headers` 未传入 response headers hook（PR 已提交） | 持续更新 | 影响自定义响应头注入 |

### 8.2 👀 需要维护者关注的信号
- **PR #21381**（团队用量聚合）：2 月提交，至今未合并，该功能对企业用户计费准确至关重要。
- **PR #20793**（`reasoning_effort` KeyError）：5 个月无维护者评论，该 Bug 影响所有使用推理参数的客户端。
- **Issue #17696**（Gemini 缓存）：社区已多次提出，但未得到官方计划回应。

建议优先对这些积压进行 triage，分配资源后明确回复社区。

---

**备注：** 本文档基于 GitHub 公开数据生成，统计窗口为 2026-07-08 00:00 UTC 至 2026-07-09 00:00 UTC。所有链接可点击跳转至原始页面。

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据 Temporal 项目截至 2026-07-09 的数据生成的动态日报。

---

### Temporal 项目动态日报 | 2026-07-09

**项目健康状况评估：高活跃度，功能迭代密集期。** 项目今日在核心功能（Nexus/CHASM 支持）、代码优化（Onebox 重构）及稳定性（动态分区、工作流暂停）方面均有显著进展。版本发布聚焦于安全更新与授权增强。社区讨论集中于长期悬而未决的功能请求。

---

### 1. 今日速览

- **开发活跃度极高**：过去 24 小时内共有 65 条 PR 更新，体现了团队密集的协作节奏，但待合并 PR 数量较多(37条)，合并率中等。
- **核心功能持续突破**: 围绕 Nexus 操作的 CHASM 支持（一种新的状态存储实现）是当前开发重心，多个相关 PR 正在推进，标志着工作流重置、可变状态重建等功能获得重大升级。
- **稳定性和安全性并重**: 新发布的 v1.31.2 和 v1.30.6 版本均修复了复制场景下的授权问题，并升级了基础镜像 (Alpine)，展现了项目对生产环境安全与稳定的重视。
- **社区反馈持续活跃**: 一个关于“工作流暂停”的长寿命功能请求 (#3006) 保持高热度，并有新的实现 PR (#10980) 提交，体现了社区核心需求与开发方向的一致性。

### 2. 版本发布

今日发布了两个补丁版本，主要针对复制环境下的授权与基础镜像进行改进，并包含潜在的破坏性变更。

- **v1.31.2**
    - **更新内容**: 升级了默认 CLI 版本至 v1.7.2；合并了对复制流端点进行授权的安全补丁 (`#9917`)；将基础镜像 Alpine 升级至 3.23.5。
    - **潜在破坏性变更及迁移**: 如果您在复制环境中使用了授权(Authorization)，请将动态配置项 `system.disableStreamingAuthorizer` 设置为 `true`，以选择退出本次发布的变更，避免复制链路中断。
    - **链接**: [v1.31.2 Release](https://github.com/temporalio/temporal/releases/tag/v1.31.2)

- **v1.30.6**
    - **更新内容**: 主要将基础镜像 Alpine 升级至 3.23.5。
    - **潜在破坏性变更及迁移**: 与 v1.31.2 相同，如果您在复制环境中使用了授权(Authorization)，必须设置 `system.disableStreamingAuthorizer` 为 `true` 以规避风险。
    - **链接**: [v1.30.6 Release](https://github.com/temporalio/temporal/releases/tag/v1.30.6)

### 3. 项目进展

以下为今日合并或关闭的关键 PR，标志着项目在多个核心领域取得进展：

- **Nexus & CHASM 支持**:
    - 合并 `#10962` 和 `#10937`，分别实现了**工作流重置（Reset）时 CHASM Nexus 操作的重新应用** 和**通过 HSM/CHASM 树正确路由 Nexus 操作取消**。这标志着 Nexus 操作与新的 CHASM 状态存储系统的兼容性大幅提升，解决了此前在特定场景下数据丢失或操作失败的问题。
- **稳定性与测试**:
    - 合并 `#10965`，**改进了动态分区（Dynamic Partitioning）模块的单元测试**，使用日志同步替代数据库写入同步，修复了测试脆弱性问题，提升了构建的可靠性。
- **SDK/开发者体验**:
    - 合并 `#10847`（临时调试构建），为**复制功能相位偏移问题**提供了调试手段，有助于运维人员排查复杂的集群复制问题。

### 4. 社区热点

- **`#3006`: Workflow Pause / Unpause**
    - **热度**: 21条评论，长期热门话题。
    - **状态**: 讨论中。一个新PR `#10980` 已提交，尝试解决此问题。
    - **分析**: 这是社区长期以来的核心诉求。用户希望在无需结束工作流的情况下，能够临时暂停其任务调度，以应对维护、依赖系统故障或人工审核等场景。该项目已形成一个完整的生态（从 Feature Request 到实现 PR），是社区与开发团队协作的典型范例。
    - **链接**: [Issue #3006](https://github.com/temporalio/temporal/issues/3006)

### 5. Bug 与稳定性

今日无新 Bug 报告。值得关注的稳定性相关改进：

- **高优先级**:
    - **动态分区测试脆弱性修复** (`#10965`, 已合并): 解决了单元测试中的竞态条件，有助于提升 CI/CD 管道的稳定性，防止因测试不稳定导致误报。
    - **工作流暂停后任务清理** (`#10980`, 已提交): 潜在修复了一个逻辑 Bug，即在取消暂停工作流时，如果处理不当可能会导致工作流任务创建失败。该 PR 旨在通过清除“待处理”的任务来确保逻辑正确性。

### 6. 功能请求与路线图信号

以下是今日活跃的功能需求，结合已有 PR 可窥见项目部分路线图：

- **工作流暂停/恢复**: `#3006` (已开4年+)。 新的实现PR `#10980` 表明该项目进入了开发阶段，极有可能被纳入后续的 **v1.32.x** 或 **v1.33.0** 版本中。
- **`SuggestContinueAsNew` 支持信号限制**: `#10941` (新提出)。 用户希望 `SuggestContinueAsNew` 建议能够将 `maximumSignalsPerExecution` 限制纳入考虑，以防止工作流因信号过多而“硬失败”。此需求反映了社区对工作流生命周期精细化管理的要求，有较高概率被采纳。
- **归档任务执行器增加集群活跃性检查**: `#10888` (新提出)。 在启用了复制 (Replication) 的全局命名空间中，防止备用(standby)集群也执行归档任务，避免对归档后端（如 S3）造成不必要的压力。这是一个实用的生产环境优化建议。

### 7. 用户反馈摘要

从今日的 Issues 与 PR 评论中，可以提炼出以下用户痛点与场景：

- **痛点 - 工作流生命周期管理**: 用户(`#3006`)表现出对工作流“暂停”这一基础、灵活的控制能力的迫切需求。现有方案（如修改工作流代码、外部信号控制）过于复杂或不优雅。
- **场景 - 以信号驱动的业务逻辑**: 用户(`#10941`)描述了一个典型的“信号驱动”场景（例如，使用数千个小型信号来更新聚合状态）。他们遇到的核心痛点是系统固有的硬限制 (`maximumSignalsPerExecution`) 与 SDK 提供的建议机制 (`SuggestContinueAsNew`) 脱节，导致工作流被迫失败，而不是优雅地通过“ContinueAsNew”续命。
- **痛点 - 多集群运维复杂性**: 用户(`#10888`) 指出了在多集群复制场景下，默认的归档行为会导致资源浪费和潜在压力。这表明用户对合理的、可预期的多集群资源消耗有较高要求。

### 8. 待处理积压

以下为长时间未有进展或被标记为待办的 Issue/PR，建议维护者关注：

- **`#9267`: CancelOutstandingPoll 修复**（2026-02 创建，`[stale]` 标签）。该 PR 旨在修复跨任务队列分区的轮询取消问题，影响任务分配的及时性和Worker资源的有效利用，建议重新评估其优先级。
    - 链接: [PR #9267](https://github.com/temporalio/temporal/pull/9267)
- **`#9391`: XDC 系统工作流 Dry-Run 模式**（2026-02 创建，`[stale]` 标签）。该功能允许在不实际执行操作的情况下测试全球化/故障转移控制面，对运维团队和系统测试非常有价值，建议评估其纳入规划的可行性。
    - 链接: [PR #9391](https://github.com/temporalio/temporal/pull/9391)
- **`#10218`: 独立活动取消命令下发**（2026-05 创建，长期开放）。此 PR 解决了当独立活动（如 Nexus 调用）被取消时，未通知 Worker 的问题。由于涉及 Core SDK 的交互，属于重要但实现复杂的特性，已开放超过两个月，值得关注。
    - 链接: [PR #10218](https://github.com/temporalio/temporal/pull/10218)

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*