# OpenClaw 生态日报 2026-08-27

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-26 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告



---

## 横向生态对比

# 个人 AI 助手 / 自主智能体开源生态横向对比分析

> 说明：本次输入中 **OpenClaw、Hermes Agent、Pi、Temporal 四个项目未提供可用的动态数据**，以下分析将严格基于 OpenHands SDK 与 LiteLLM 两个有完整数据的项目展开；涉及其他项目时明确标注“未提供”，不进行无据推测。

---

## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态仍处于 **快速迭代与生态整合** 阶段。从有数据的两个项目来看，社区关注点不再局限于单点模型调用，而是转向 **智能体协议标准化、LLM 网关的兼容性与可靠性、供应链安全、资源可部署性** 等工程化议题。OpenHands SDK 在推进 ACP（Agent Client Protocol）评估与子 Agent 控制能力，LiteLLM 则在持续修补多模型计费、缓存与镜像签名细节，两者共同揭示了生态从“可用”走向“好用”的典型特征。由于其余四个项目动态缺失，难以对全景做完整量化判断，但仅从核心数据看，生态整体活跃度处于高位。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新数 | PR 更新数 | Release | 健康度评估 |
|---|---|---|---|---|
| OpenClaw | 未提供 | 未提供 | 未提供 | 未提供数据，本次被列为“核心参照” |
| Hermes Agent | 未提供 | 未提供 | 未提供 | 未提供数据 |
| OpenHands SDK | 30 条（21 新开/活跃，9 关闭） | 20 条（15 待合并，5 合并/关闭） | 无 | 健康度良好，社区讨论积极，但 PR 积压需关注 |
| Pi | 未提供 | 未提供 | 未提供 | 未提供数据 |
| LiteLLM | 101 条（60 新开/活跃，41 关闭） | 332 条（141 合并/关闭） | v1.100.0-dev.1 | 高活跃，处理节奏快；但 191 个 PR 待合并，长期遗留 issue 也有积累 |
| Temporal | 未提供 | 未提供 | 未提供 | 未提供数据 |

---

## 3. OpenClaw 在生态中的定位

由于本日 OpenClaw 动态摘要为空，仅能从预设的“核心参照”定位做定性判断：OpenClaw 很可能扮演 **个人 AI 助手统一框架 / 基准实现** 的角色，社区规模与项目完整度在生态中具有指向性意义。但无法从数据层面量化其与技术路线差异。

与 OpenHands SDK（专注软件智能体开发套件）和 LiteLLM（专注 LLM 网关）相比，OpenClaw 若作为端到端个人助手，目标层次更偏向“最终用户体验”，而不仅是开发者基础设施。这一差异性定位需要后续数据验证。

---

## 4. 共同关注的技术方向

在已提供数据的两个项目中，以下技术方向同时涌现，具备跨项目共性：

| 方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **LLM 供应商兼容性细节** | OpenHands SDK、LiteLLM | OpenHands 修复订阅制 LLM 的 condenser 不触发问题；LiteLLM 修复 Gemini 语音设置、DeepSeek 视觉请求丢图、Vertex AI 成本计费等问题 |
| **供应链与安全加固** | OpenHands SDK、LiteLLM | OpenHands 将明文密钥警告覆盖至全部敏感字段；LiteLLM 使用 cosign 对所有 Docker 镜像签名，保证可验证来源 |
| **会话与缓存稳定性** | OpenHands SDK、LiteLLM | OpenHands 修复 session resume 因字段序列化丢值问题；LiteLLM 修复 Fireworks prompt 缓存因随机 trace_id 导致完全失效的问题 |
| **资源优化与瘦身** | OpenHands SDK（LiteLLM 镜像签名间接体现） | OpenHands 发布 python-lite 镜像、推进镜像构建重组；LiteLLM 镜像供应链验证也引入新的部署运维考虑 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|---|---|---|---|
| **OpenHands SDK** | 软件智能体开发框架：ACP 协议、Harness 评估体系、子 Agent 控制、镜像定制 | 开发者/研究团队，需构建可审计的自主 Agent 系统 | 以 SDK 形式提供，深度集成 ACP 协议与事件总线，强调子 Agent 生命周期治理与评估 |
| **LiteLLM** | LLM 统一网关：多供应商接入、计费/成本追踪、缓存、代理稳定性 | 后端/平台工程师，需统一管理多种 LLM API | 以代理/网关形态部署，覆盖数百种模型供应商，侧重请求路由、成本核算与兼容性修补 |
| **OpenClaw（未提供数据）** | 推测为个人 AI 助手完整解决方案 | 终端用户/助手开发者 | 架构未知 |
| **Hermes Agent / Pi / Temporal** | 未提供数据，无法分析 | — | — |

两者互补性明显：OpenHands 解决“Agent 怎么开发与编排”，LiteLLM 解决“Agent 底层模型怎么接入与管控”。

---

## 6. 社区热度与成熟度

从已有数据看，OpenHands SDK 与 LiteLLM 均处于 **活跃迭代期**，但阶段侧重不同：

- **OpenHands SDK**：当前处于 **生态构建与质量巩固阶段**。30 条 Issue / 20 条 PR 的规模不算大，但围绕 Harness Watch 一次性创建 8 个 P0/P1 子任务，表明项目正在将重点从“功能扩张”转向“标准化评估与可靠性加固”。社区讨论更有深度（如 #2186、#3176），属于技术社区驱动型。
- **LiteLLM**：处于 **快速迭代与兼容性覆盖阶段**。单日 101 条 Issue、332 条 PR 更新，体量远超 OpenHands，说明项目已进入大规模社区使用期，反馈量极大；但同时 191 个待合并 PR 和 15 个月未解决的暗色模式等长期 issue，也反映出快速增长的“治理债”问题。

其余四个项目因数据缺失，无法纳入活跃度分层。

---

## 7. 值得关注的趋势信号

1. **Agent 协议与评估体系开始标准化**：OpenHands 的 Harness Watch epic（#4627）及多个 P0 子任务，标志着软件智能体从“私有实现”走向“可对比评估”的确定性阶段。开发者应关注 ACP 协议生态，早期绑定可降低未来迁移成本。
2. **子 Agent / 多 Agent 协作控制成为刚需**：OpenHands 中 #2047（非阻塞后台子 Agent）、#3907（子事件回流父流）、#4654（每任务 LLM profile）等诉求长期存在，说明智能体复杂任务分解已进入实践，但父-子控制模型仍不成熟，是明确的创新空间。
3. **LLM 网关计费与缓存精确性成为核心痛点**：LiteLLM 集中修复 Google Maps 成本为 0、Fireworks prompt 缓存失效等问题，折射出多模型时代，成本可观测性和缓存一致性是生产落地的关键瓶颈。
4. **供应链安全在 AI 基础设施中加速落地**：LiteLLM 对所有 Docker 镜像引入 cosign 签名，OpenHands 同步加固密钥泄露警告，显示主流项目开始将软件供应链安全视作默认要求，而非可选项。
5. **镜像/部署轻量化成为生态竞争力**：OpenHands 推出 python-lite 镜像并重组镜像构建参数（#4643/#4645），侧面反映开发者对 AI 基础组件在边缘/自托管场景的部署密度越来越在意；可插拔的 provider 集和更小镜像体积可能成为后续项目标配。

> 对开发者的参考价值：若正在构建智能体应用，应优先采用支持 ACP 协议的 SDK，规划好多 Agent 任务控制与事件回流；若运维多模型接入，需重点评估网关的缓存策略、计费准确性和供应链可验证能力。这两个方向已成为当前生态竞争的高地。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

## OpenHands SDK 项目动态日报 — 2026-08-27

### 1. 今日速览

项目昨日（8月26日）活跃度处于高位，**共 30 条 Issues 更新（21 条新开/活跃、9 条关闭），20 条 PR 更新（15 条待合并、5 条已合并/关闭）**，无新版本发布。核心焦点集中在 **ACP（Agent Client Protocol）生态建设**：维护者 @simonrosenberg 系统性推进了 "Harness Watch" 评估体系（epic #4627 及 8 个子任务）、agent-server 镜像重组（#4643）以及许可证合规（#4644）；同时两个高优先级 bug 得到闭环（#4515 已修复、#4537 有活跃 PR 及关联提案）。项目健康度良好，社区讨论活跃（#2186 有 15 条评论），但需注意待合并 PR 积压较多（15 条），部分已有较长等待时间。

---

### 2. 版本发布

本日无新版本发布。

---

### 3. 项目进展

今日共 5 个 PR 被合并/关闭，覆盖了 **关键 bug 修复、安全改进、文档与镜像构建** 多个维度：

| PR | 类型 | 内容 | 影响 |
|---|---|---|---|
| [#4517](https://github.com/OpenHands/software-agent-sdk/pull/4517) | fix（已合并） | **为订阅类 LLM 启用 condenser**，修复 #4515，通过现有 completion dispatch 解决了 Codex 订阅认证下上下文压缩不触发的问题 | 高优先级稳定性修复，覆盖 ChatGPT 订阅用户的长期会话场景 |
| [#4649](https://github.com/OpenHands/software-agent-sdk/pull/4649) | fix（已合并） | **CriticResult.message 默认值修复为 None**，修复 session resume 因 `exclude_none` 导致的事件序列化/反序列化不匹配 | 修复会话恢复的隐蔽缺陷 |
| [#4618](https://github.com/OpenHands/software-agent-sdk/pull/4618) | fix（已合并） | **agent-server 明文密钥保存警告覆盖全部敏感字段**（critic_api_key、MCP secrets、agent_context.secrets），不再仅限 llm.api_key | 安全加固，修复 #4609 |
| [#4648](https://github.com/OpenHands/software-agent-sdk/pull/4648) | docs（已合并） | 刷新 AGENTS.md，记录持久化不变式 | 文档维护 |
| [#4101](https://github.com/OpenHands/software-agent-sdk/pull/4101) | feat（已合并） | **发布 python-lite 镜像**，跳过预装 ACP providers，镜像标签以 `-lite` 区分 | 镜像体积优化，与 #4643/#4645 呼应 |

整体来看，项目在 **订阅模型兼容性、会话可靠性、密钥安全** 三个维度都有实质进展，同时通过 python-lite 镜像为镜像瘦身打下了基础。

---

### 4. 社区热点

最受关注的 Issues/PRs（按评论数）：

| 排名 | Issue/PR | 评论数 | 关注点 |
|---|---|---|---|
| 1 | [#2186](https://github.com/OpenHands/software-agent-sdk/issues/2186) Advanced Features for Markdown-based Agents | 15 | 用户 @VascoSch92 跟踪 Markdown Agent 的高级功能缺口，**部分已完成（checklist 已勾选）**，但仍是社区关注焦点 |
| 2 | [#3176](https://github.com/OpenHands/software-agent-sdk/issues/3176) PatternSecurityAnalyzer 扩展提案 | 14 | 社区成员贡献安全检测签名扩展的详细提案，讨论充分 |
| 3 | [#2047](https://github.com/OpenHands/software-agent-sdk/issues/2047) 非阻塞后台子 Agent 执行 | 7 | 长期需求（2 月提出），父 Agent 在子任务运行时可继续工作 |
| 4 | [#4537](https://github.com/OpenHands/software-agent-sdk/issues/4537) TaskToolSet 死锁/UI 冻结 | 5 | 高优先级 bug + 性能问题，社区 1 个 👍，涉及核心体验 |

**分析**：
- **ACP/Harness 系列**（#4627 及 #4634-#4642、#4639、#4635 等）虽各只有 1 条评论，但 **8 个 P0/P1 子任务在一天内密集创建**，是当前项目最明确的路线图信号。
- 底层诉求集中在 **父 Agent 对子任务的控制力**（#2047 后台执行、#4654 每任务 LLM profile、#3907 子事件回流）以及 **镜像/资源的可选性**（#4643、#4645）。

---

### 5. Bug 与稳定性

按优先级排序：

| 严重度 | Issue | 状态 | 说明 |
|---|---|---|---|
| 🔴 高 | [#4537](https://github.com/OpenHands/software-agent-sdk/issues/4537) TaskToolSet delegation 持锁导致 executor 池饱和、Canvas UI 冻结 | OPEN，5 评论 | 性能与死锁风险，**尚无直接 fix PR**；关联提案 #3907（子事件转发）可能缓解，但未解决锁问题 |
| 🟠 高（已修复） | [#4515](https://github.com/OpenHands/software-agent-sdk/issues/4515) 订阅 LLM condenser 禁用，上下文压缩永不触发 | CLOSED | ✅ 由 PR #4517 修复并合并 |
| 🟡 中 | [#4629](https://github.com/OpenHands/software-agent-sdk/issues/4629) 已废弃的 gemini-cli OAuth 优先级高于可用 API key；ACP Gemini pin 过期 | OPEN，1 评论 | ✅ 已有修复 PR [#4646](https://github.com/OpenHands/software-agent-sdk/pull/4646)（待合并） |
| 🟡 中 | [#4653](https://github.com/OpenHands/software-agent-sdk/issues/4653) run-examples 工作流：`28_ask_agent_example.py` 触发 Anthropic 400（孤儿 tool_use 无 tool_result） | OPEN，0 评论 | 新报 bug（8/26），**暂无 fix PR**，影响 CI |
| 🟡 中 | [#4077](https://github.com/OpenHands/software-agent-sdk/issues/4077) 流式事件管线存在正确性与资源安全缺陷 | OPEN，4 评论 | 长期审计结果，涉及 token/delta 管线，暂无明确修复计划 |
| ⚪ 低 | [#4633](https://github.com/OpenHands/software-agent-sdk/issues/4633) 自动化测试 issue | CLOSED | 已关闭，非真实 bug |

值得注意：**#4537 是当前最严重的公开稳定性问题**——子 Agent 任务导致整个对话列表不可交互，直接影响核心 product 体验，且评论中有用户明确遭遇（Canvas conversation list 停止渲染），需要优先排期。

---

### 6. 功能请求与路线图信号

**最高清晰度路线图信号**：@simonrosenberg 创建的 **Harness Watch epic（#4627）** 及其子任务代表确定性 ACP harness 对比评估体系，覆盖 OpenCode、Pi、Hermes 等新 provider 接入（#4639/#4635/#4634）、确定性报告（#4642）、调度（#4637）、遥测（#4638）、诊断（#4641）。多个任务标记为 **P0**，明确进入实施阶段。

**近期可能纳入下一版本的功能需求**：

| 功能 | Issue | 对应 PR | 状态 |
|---|---|---|---|
| 每任务工具可指定 LLM profile | [#4654](https://github.com/OpenHands/software-agent-sdk/issues/4654) | [#4510](https://github.com/OpenHands/software-agent-sdk/pull/4510)（待合并） | 功能已在 PR 实现，待 review |
| 子 Agent 内部事件转发至父对话流 | [#3907](https://github.com/OpenHands/software-agent-sdk/issues/3907) | 暂无 | Opt-in 设计，默认关闭 |
| 非阻塞后台子 Agent 执行 | [#2047](https://github.com/OpenHands/software-agent-sdk/issues/2047) | 暂无 | 长期需求，7 个月未实现 |
| ACP provider 扩展：Antigravity CLI | [#4624](https://github.com/OpenHands/software-agent-sdk/issues/4624) | 暂无 | 已验证可行性，`ready-for-dev` |
| agent-server 镜像可选能力（VSCode/Chromium/桌面） | [#4645](https://github.com/OpenHands/software-agent-sdk/issues/4645) | 暂无 | 34.5% 镜像体积，诉求强烈 |
| 镜像构建重组（参数化 provider 集） | [#4643](https://github.com/OpenHands/software-agent-sdk/issues/4643) | [#4651](https://github.com/OpenHands/software-agent-sdk/pull/4651)（待合并） | 有实现尝试 |
| 多仓库/跨仓库感知 | [#4239](https://github.com/OpenHands/software-agent-sdk/issues/4239) | 暂无 | 2 👍，roadmap 级，近 1 年未动 |

**判断**：Harness Watch 系列为短期（P0/P1 本迭代）目标；LLM profile 覆盖（#4654 + PR #4510）由于实现已就绪，极可能进入下一版本；镜像瘦身（#4643/#4645）与后台执行（#2047）是中期高价值方向。

---

### 7. 用户反馈摘要

从 Issues 评论中提炼的真实反馈：

- **UI 冻结影响核心体验**（#4537）：用户 @quickbearattack 描述 "Agent Canvas conversation list stops rendering for the

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报（2026-08-27）

> 数据来源：github.com/BerriAI/litellm | 统计周期：2026-08-26 ~ 2026-08-27

---

## 1. 今日速览

过去24小时 LiteLLM 项目处于高活跃状态：**Issue 侧**共更新 101 条（新开/活跃 60 条，关闭 41 条，关闭率约 40%），**PR 侧**共更新 332 条（合并/关闭 141 条），双向处理节奏较为健康。项目发布了 v1.100.0-dev.1 开发版，重点配套 Docker 镜像 cosign 签名验证说明。值得关注的是，当前仍有 **191 个 PR 处于待合并状态**，且多条高热度 Issue（暗色模式 15 个月未解决、Prisma 连接稳定性问题）长期悬置，社区对项目治理节奏已有一定期待。

---

## 2. 版本发布

### v1.100.0-dev.1（开发版）

- 链接：https://github.com/BerriAI/litellm/releases
- 核心变更：**所有 LiteLLM Docker 镜像已通过 [cosign](https://docs.sigstore.dev/cosign/overview/) 签名**，每个 Release 均使用同一签名密钥（始于 commit `0112e53`），用户现可验证镜像来源与完整性。
- 破坏性变更：无明确说明。
- 迁移注意：这是 v1.100.0 的 dev.1 预发布版本，主要面向管道验证与镜像签名测试；如你的 CI 依赖 Docker 镜像拉取，建议先行校验 cosign 签名流程，确保新镜像可正常验证。

---

## 3. 项目进展

今日合并/关闭了一批高价值 PR，主要在以下方向推进：

### 3.1 Gemini 系列修复（语音、成本、接地）
- **保留客户端语音设置**：PR [#38395](https://github.com/BerriAI/litellm/pull/38395)（以及此前同向的 [#36885](https://github.com/BerriAI/litellm/pull/36885)）修复了 Gemini / Vertex AI 原生音频 Live 静默忽略客户端所请求语音的问题——此前 `speechConfig` 被剥除，客户端无法自定义话音。
- **Google Maps grounding 成本追踪**：PR [#35965](https://github.com/BerriAI/litellm/pull/35965) 修复了使用 `googleMaps` 工具时 `tool_usage_cost` 恒为 0 的问题，成本将按 grounding 实际使用正确入账。

### 3.2 模型兼容性与接入
- **DeepSeek 视觉内容转发**：PR [#38397](https://github.com/BerriAI/litellm/pull/38397)（及 [#37854](https://github.com/BerriAI/litellm/pull/37854)）彻底修复 DeepSeek 视觉请求丢图问题，仅在 vision 模型 + 用户消息 + 全 web 图片块条件下转发图像，避免破坏非视觉模型。

### 3.3 缓存与网关稳定性
- **Fireworks AI prompt 缓存**：PR [#35754](https://github.com/BerriAI/litellm/pull/35754) 不再将每次请求生成的 `litellm_trace_id` 用作会话亲和性 key，修复了 Fireworks prompt 缓存完全失效的问题。

整体来看，今日 PR 重心偏向 **API 兼容性细节打磨 + 计费准确性修复**，没有引入大规模重构或破坏性变更，项目处于稳健的增量迭代阶段。

---

## 4. 社区热点

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*