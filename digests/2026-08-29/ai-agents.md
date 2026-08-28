# OpenClaw 生态日报 2026-08-29

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-28 22:36 UTC

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



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-29

## 今日速览

过去 24 小时项目活跃度极高：**395 条 Issue 更新**（337 条活跃/新开，58 条关闭）与 **500 条 PR 更新**（428 条待合并，72 条已合并/关闭）均处于历史高位。社区讨论焦点集中在 **Desktop 持久化会话与多网关连接**（跟踪 Issue #94724 宣布 29 个 PR 全部合并）、**Webhook 功能包修复**（meta-issue #84834）、以及 **Skills 索引自动巡检告警**（#66616 评论数达 113 条）三大方向。当前无新版本发布，但大量已合并 PR 尚未形成正式 Release，项目处于「功能密集合入、版本待打包」的高迭代阶段。需留意的是 428 条待合并 PR 形成较大积压，且多起 P1 级会话状态损坏问题仍在排查中。

---

## 项目进展

### 标志性里程碑
- **Desktop 持久化多网关连接战役收官** — [#94724](https://github.com/NousResearch/hermes-agent/issues/94724)（已关闭）跟踪的 29 个 PR 全部合并，2 个同日回归已修复，15 个 salvaged 集群已交付。该战役为 Desktop 带来了持久化多网关连接能力，是近期最大的功能推进。

### 今日值得关注的合入/关闭 PR
- **feat(desktop): 可配置群聊轮次上限 + 模型感知限制 + Token 预算守卫** — [#96842](https://github.com/NousResearch/hermes-agent/pull/96842)（已关闭）：将硬编码的 `GROUP_CHAT_MAX_ROUNDS` 改为配置驱动，支持免费模型无限轮次及硬上限保护。
- **fix(provider): 模型解析优先查询当前提供商目录** — [#97487](https://github.com/NousResearch/hermes-agent/pull/97487)（开放）：修复 ACP 路径上 OpenRouter 目录劫持当前提供商模型的问题。

### 整体进度评估
Desktop 相关修复（约 10+ PR）与状态管理加固（如 SQLite 损坏防护、SOUL.md 漂移检测）正在快速推进中。项目已从「功能扩张期」进入「稳定性修复期」，预计 0.21.0 版本将主要包含桌面端体验修复与会话状态可靠性改进。

---

## 社区热点

### 讨论热度 Top 3 Issues

1. **[#66616](https://github.com/NousResearch/hermes-agent/issues/66616) Skills 索引过期告警（113 条评论）**
   - 状态：`degraded`，索引已 29.8 小时未刷新（限制 26 小时）
   - 分析：这是由 `nousbot-eng` 自动巡检机器人报告的持续性问题，社区围绕自动重建延迟、刷新频率设置展开了大量讨论，侧面反映用户对 Skills Hub 文档依赖度较高。

2. **[#88584](https://github.com/NousResearch/hermes-agent/issues/88584) Nous 集成被阻塞（38 条评论）**
   - 状态：`cron/jobs.py` 合并冲突，自动集成停滞
   - 分析：外部 `enterkey-io` 工作流与上游不一致导致集成失败，社区关注自动合并管道的健壮性。

3. **[#84834](https://github.com/NousResearch/hermes-agent/issues/84834) Webhook 功能包修复 meta-issue（24 条评论）**
   - 状态：5×2×3 graph-gated 修复计划进行中
   - 分析：覆盖 Webhook 入口、执行、投递、配置、UI、部署、文档全链路，显示项目对基础设施完备性的重视。

### 值得关注的 PR 讨论
- **feat(gateway): 新增 Bale 消息平台**[#97477](https://github.com/NousResearch/hermes-agent/pull/97477)：复用 Telegram 成熟的传输层，扩展新平台成本极低，反映了项目的高可组合性。
- **feat(auth): Codex 授权码 OAuth 流** [#97058](https://github.com/NousResearch/hermes-agent/pull/97058)：针对禁用设备码 OAuth 的企业用户，社区关注度高。

---

## Bug 与稳定性

### P0/P1 级紧急问题

| 严重度 | Issue | 描述 | 状态 |
|--------|-------|------|------|
| P0 | [#87093](https://github.com/NousResearch/hermes-agent/issues/87093) | Debian 13.6 安装失败（uv.lock & npm install），已获 4 👍 | 已关闭（评论 23 条） |
| P1 | [#96282](https://github.com/NousResearch/hermes-agent/issues/96282) | Electron Desktop 启动超时：`HERMES_BACKEND_READY` sentinel 输出到 stderr 后未被捕获，涉及 6d4e851d8 提交 | 已关闭 |
| P1 | [#93888](https://github.com/NousResearch/hermes-agent/issues/93888) | Desktop 向远程网关发送本地运行期 ID，导致会话恢复失败：「Restore failed — Session not found」 | 开放中 |
| P1 | [#60323](https://github.com/NousResearch/hermes-agent/issues/60323) | macOS 上 Desktop 本地后端可能错过 `HERMES_BACKEND_READY` 信号，90000ms 超时 | 开放中（1 👍） |
| P1 | [#94248](https://github.com/NousResearch/hermes-agent/issues/94248) | macOS arm64 网关在委派 worker 600 秒截止时发生 SIGSEGV，12 份崩溃报告 | 开放中（相关 PR [#68499](https://github.com/NousResearch/hermes-agent/pull/68499) 分离生命周期与任务结果，可能修复） |
| P1 | [#90837](https://github.com/NousResearch/hermes-agent/issues/90837) | 生产网关 state.db 在 18 天内损坏 11 次，外部原因全部排除 | 开放中 |
| P1 | [#66887](https://github.com/NousResearch/hermes-agent/issues/66887) | 多路复用网关中，次要配置文件的 Telegram 会话错误写入默认配置文件状态库 | 开放中 |

### 已有关联修复 PR 的 Bug
- **桌面启动器 Exec= 损坏** — [#92095](https://github.com/NousResearch/hermes-agent/issues/92095)、[#94058](https://github.com/NousResearch/hermes-agent/issues/94058)：uv 安装下 venv 符号链接被 `.resolve()` 解引用，点击图标启动即崩。属于同一根因的两个 Manifestation，预计会在后续版本统一修复。
- **TUI Shift+字母被小写化** — [#90663](https://github.com/NousResearch/hermes-agent/issues/90663)：Ghostty 终端下 Ink TUI 输入大写字母失效，平台相关 bug。

---

## 功能请求与路线图信号

### 高潜力合并方向
1. **实时语音 Provider 抽象（RFC #77111）**
   - 链接：https://github.com/NousResearch/hermes-agent/issues/77111
   - 信号：社区已有 4 个双向语音 PR 竞争，AGENTS.md 明确要求 3+ PR 同类别时先设计 ABC。此接口设计大概率进入路线图。

2. **统一 Slash 命令注册表（Spec #96692）**
   - 链接：https://github.com/NousResearch/hermes-agent/issues/96692
   - 信号：跨 CLI/Desktop/Gateway/TUI 的统一命令契约，属于架构规范化方向，有 meta-issue 气质，被合入的可能性较高。

3. **工具输出压缩集成 headroom-ai（#39691，17 👍）**
   - 链接：https://github.com/NousResearch/hermes-agent/issues/39691
   - 信号：token 压缩需求长期存在（5 月提出），社区讨论活跃。目前仍处于 needs-decision 状态，但 17 个 👍 表明用户期望值高。

### 观察中的需求（可能进入下一版本）
- **Mistral 作为 LLM 提供商支持** — [#20859](https://github.com/NousResearch/hermes-agent/issues/20859)（27 👍，但标记 wontfix，需维护者重新评估）
- **Alibaba Coding Plan 专用提供商** — [#2220](https://github.com/NousResearch/hermes-agent/issues/2220)（3 月提出，长期未响应）
- **群聊注意力标记行为优化** — PR [#93993](https://github.com/NousResearch/hermes-agent/pull/93993)、[#93903](https://github.com/NousResearch/hermes-agent/pull/93903) 已在推进。

---

## 用户反馈摘要

- **满意点**：多网关连接战役（#94724）获得社区正面评价（1 👍），Desktop 持久化连接功能大幅提升了多机工作流的可用性。Webhook 修复包的推进也回应了企业用户的基础设施需求。
- **核心痛点**：
  - **安装与升级断裂感**：Debian 安装失败（#87093）、uv.lock 冲突（#88361）、macOS 更新后 `/Applications/Hermes.app` 过期（#52339）等问题反复出现，用户对安装脚本的健壮性存在不满。
  - **会话状态脆弱性**：「恢复失败」「会话被永久损坏」（如 xAI 图片 400 永久锁死会话 #69078）、state.db 反复损坏（#90837）等问题消耗用户信任，「杀死会话」成为唯一的恢复手段。
  - **平台体验不一致**：Linux .desktop 启动器失效（#92095）、Windows 下 UI 冻结（#58576）、macOS TUI 大写输入失效（#90663），跨平台质量参差不齐。

---

## 待处理积压

### 长期未响应的重要 Issue
- **[#2220](https://github.com/NousResearch/hermes-agent/issues/2220) Alibaba Coding Plan 专用提供商（2026-03-20 提出）**
  - 超过 5 个月未获维护者响应，社区用户仅能用通用 OpenAI 兼容配置替代，可能会影响用户体验。
- **[#20859](https://github.com/NousResearch/hermes-agent/issues/20859) Mistral 支持（2026-05-06 提出，27 👍）**
  - 标记为 wontfix，但高点赞量表明真实需求，建议维护者重新审视。

### 长期开放的 PR（超过 1 个月）
- **[#68499](https://github.com/NousResearch/hermes-agent/pull/68499) 委托生命周期与任务结果分离（2026-07-21 开放）**
  - 与 #94248 SIGSEGV 崩溃直接相关，长期未合并可能会影响崩溃修复进度。
- **[#73179](https://github.com/NousResearch/hermes-agent/pull/73179) 延迟工具调用参数校验（2026-07-28 开放）**
  - 涉及 MCP/插件安全边界，建议尽快推进。
- **[#72253](https://github.com/NousResearch/hermes-agent/pull/72253) SOUL.md 漂移检测（2026-07-26 开放）**
  - 已标记为「不再重建系统提示词」，说明设计方向已有变动，需更新 PR 说明或关闭。

### 风险提示
- **Skills 索引持续降级**（#66616）：自动巡检已连续多日告警，索引过期会影响 `docs` 站点和技能发现功能，建议优先处理部署流水线。
- **428 条待合并 PR 积压**：其中包含大量 `type/bug` 和 `sweeper:risk-session-state` 标记的修复，长时间不合并会加剧主分支与 PR 分支的冲突风险，也可能让用户问题迟迟得不到解决。

---

*数据区间：2026-08-28 至 2026-08-29 | 数据来源：Hermes Agent GitHub 仓库*

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

## OpenHands SDK 项目动态日报 — 2026-08-29

### 1. 今日速览

过去24小时项目保持高活跃度：35条Issue更新、33条PR更新，并发布了v1.44.1（主要包含ACP构建参数、lmnr依赖升级与DeepSeek v4 Flash验证）。值得关注的是，以@VascoSch92为代表的贡献者围绕streaming架构史诗#4671提交了一组关联的高优Bug（webhook token洪泛、secret masking覆盖不足、idle timer失效等），其中#4672已被快速关闭，显示出维护团队对安全与架构治理类议题响应迅速。项目整体处于架构打磨与安全加固阶段，社区反馈与代码提交形成良性循环。

---

### 2. 版本发布

**v1.44.1**（[Release 链接](https://github.com/OpenHands/software-agent-sdk/releases)）

更新内容：
- `feat(agent-server)`: 新增 `INSTALL_ACP_PROVIDERS` 构建参数（PR [#4687](https://github.com/OpenHands/software-agent-sdk/pull/4687)），允许在构建agent-server镜像时按需安装ACP provider依赖，有助于缩小镜像体积。
- `chore(deps)`: 升级 `lmnr` 至 0.7.60（PR [#4688](https://github.com/OpenHands/software-agent-sdk/pull/4688)）。
- 验证DeepSeek v4 Flash模型兼容性。

**破坏性变更**：无。镜像体积优化方向与此前 #4645（将OpenVSCode/Chromium/桌面栈设为可选）一致，预计后续版本将逐步推行。

---

### 3. 项目进展

过去24小时无合并PR明细披露（4条合并/关闭中未列出具体编号），但多个已关闭Issue反映出重要的功能修复与架构演进：

- **修复ACP项目技能重复注入**（[#4019](https://github.com/OpenHands/software-agent-sdk/issues/4019) 已关闭）：通过PR #4018修复了ACP profiles重复加载项目skills的问题，使ACP CLI与SDK的skills注入路径对齐。
- **修复EventLog O(N²)性能问题**（[#3906](https://github.com/OpenHands/software-agent-sdk/issues/3906) 已关闭）：`EventLog.append()`不再每次全量listdir，对应PR [#4697](https://github.com/OpenHands/software-agent-sdk/pull/4697) 正在推进，使写入路径从O(N²)降为常数级。
- **修复browser-use iframe导致DOM提取失败**（[#3753](https://github.com/OpenHands/software-agent-sdk/issues/3753) 已关闭）：解决了广告/分析类iframe导致整个DOM提取失败的回归问题。
- **修复LLM profile timeout重启丢失**（[#4032](https://github.com/OpenHands/software-agent-sdk/issues/4032) 已关闭）。
- **修复webhook每token delta都POST的严重问题**（[#4672](https://github.com/OpenHands/software-agent-sdk/issues/4672) 已关闭）：已修复流式场景下webhook被token delta刷爆的缺陷。

---

### 4. 社区热点

1. **#4019 — ACP profiles重复注入project skills**（[链接](https://github.com/OpenHands/software-agent-sdk/issues/4019)）｜ 16条评论，今日关闭
   社区对该问题的广泛关注源于ACP CLI与SDK对AGENTS.md的重复解析，影响所有ACP用户。修复方向是使ACP路径与OpenHands路径行为一致（`load_project_skills=True`），但引发了关于默认行为是否正确的讨论。

2. **#4251 — OWASP Agent Memory Guard集成**（[链接](https://github.com/OpenHands/software-agent-sdk/issues/4251)）｜ 15条评论
   Memory poisoning（记忆投毒）防御需求持续获得关注。用户希望在agent的长期记忆中引入安全防护层，反映社区对agent安全性的整体焦虑。

3. **#4259 — 面向reviewer的evidence gates**（[链接](https://github.com/OpenHands/software-agent-sdk/issues/4259)）｜ 11条评论
   用户希望agent执行关键动作（如写文件、执行命令）时能向reviewer展示证据（diff、终端输出等），便于人工审批。这是对agent可观测性和可控性的直接诉求。

4. **@VascoSch92发起的streaming架构系列Issue**（[#4671 Epic](https://github.com/OpenHands/software-agent-sdk/issues/4671) 及其子Issue #4672/#4673/#4674/#4677/#4678/#4695/#4696）｜ 1-3条评论不等
   虽然单条评论不多，但该系列从"wire format与durable event分离"的架构视角，系统性地揭示了当前实现中的多个深层问题（见下一节）。

---

### 5. Bug 与稳定性

按严重程度排列：

**🔴 高优 — 安全相关**

| Issue | 状态 | 描述 |
|-------|------|------|
| [#4677](https://github.com/OpenHands/software-agent-sdk/issues/4677) | OPEN / ready-for-dev | **Secret masking仅覆盖13个工具中的1个**（terminal），file_editor、grep、glob、apply_patch、browser_use等工具均未做mask，模型可读到原始密钥。 |
| [#4678](https://github.com/OpenHands/software-agent-sdk/issues/4678) | OPEN / ready-for-dev | **模型输出在标准Agent路径上完全未做mask**（仅ACP路径和terminal有处理），属于跨会话的敏感信息泄露风险。 |
| [#4695](https://github.com/OpenHands/software-agent-sdk/issues/4695) | OPEN / ready-for-dev | **Token deltas不再重置runtime idle timer**，长流式输出可能导致pod被误回收（#4689变更引入的回归）。 |

**🟠 中优 — 功能异常**

| Issue | 状态 | 描述 |
|-------|------|------|
| [#4692](https://github.com/OpenHands/software-agent-sdk/issues/4692) | OPEN / ready-for-dev | **TaskManager强制子agent `stream=False`**，导致使用ChatGPT订阅（不允许非流式调用）的用户子agent直接失败。 |
| [#4674](https://github.com/OpenHands/software-agent-sdk/issues/4674) | OPEN / ready-for-dev | **ConversationState单一FIFOLock**守护6个独立关注点（事件、状态、token等），存在锁竞争和死锁风险。 |
| [#4673](https://github.com/OpenHands/software-agent-sdk/issues/4673) | CLOSED | Telemetry的`event_count_bucket`将token deltas计入事件数，使指标跨会话不可比（已修复）。 |

**🟢 低优 — 性能与长期**

| Issue | 状态 | 描述 |
|-------|------|------|
| [#4697](https://github.com/OpenHands/software-agent-sdk/pull/4697) | OPEN | EventLog.append常数级性能修复PR，与#3906对应。 |

**提示**：#4677和#4678属于安全敏感缺陷，建议维护团队优先分配资源，在下一patch版本中至少完成标准Agent路径的输出mask与扩展工具覆盖。

---

### 6. 功能请求与路线图信号

| 功能需求 | Issue/PR | 潜在纳入版本信号 |
|----------|----------|------------------|
| **OWASP Memory Guard记忆投毒防御** | [#4251](https://github.com/OpenHands/software-agent-sdk/issues/4251) | 暂无PR，但社区关注度高（15评论）；若与#4671 streaming重构结合，可能在下个大版本评估架构级方案。 |
| **Reviewer-facing evidence gates** | [#4259](https://github.com/OpenHands/software-agent-sdk/issues/4259) | 无直接PR，与OpenHands主线human-in-the-loop方向一致，值得roadmap关注。 |
| **可插拔durable execution后端** | [#4254](https://github.com/OpenHands/software-agent-sdk/issues/4254) | 无PR；长任务场景真实存在，但实现复杂度高，短期纳入概率低。 |
| **Run-scoped LLM extra headers** | [#4064](https://github.com/OpenHands/software-agent-sdk/issues/4064 已关闭) | 已关闭但无对应PR可见，可能被内部处理或延后。 |
| **镜像瘦身：OpenVSCode/Chromium/桌面栈可选** | [#4645](https://github.com/OpenHands/software-agent-sdk/issues/4645) | v1.44.1新增`INSTALL_ACP_PROVIDERS`构建参数是该方向的第一步，说明维护者已在行动。 |
| **TypeScript client移入monorepo** | PR [#4702](https://github.com/OpenHands/software-agent-sdk/pull/4702) | 与SDK架构统一方向一致，值得关注review进展。 |

**路线图信号**：enyst在6月提出的OpenAI gateway系列roadmap（#3598/#3599/#3600/#3601/#3602）仍在开放状态且持续小范围讨论；结合v1.44.1的DeepSeek v4 Flash验证，#3599（gateway操作性打磨）可能优先于Responses API（#3601）落地。

---

### 7. 用户反馈摘要

从今日活跃Issue评论中提炼的真实反馈：

- **用户对模型输出安全有明确担忧**（#4678、#4677）：一位贡献者明确表示"标准Agent路径上模型输出完全未做mask"，这会让通过`file_editor`等工具读取的密钥直接暴露给模型并可能写入长期记忆。该问题在@VascoSch92的分析中被定位为#4671架构重构的独立前置任务。

- **配置持久化是长期痛点**（#4292）：用户发现`_apply_prompt_caching`只能设置5分钟缓存TTL，无法达到provider支持的1小时prompt cache TTL，且试图在代码中搜索相关配置时找不到任何覆盖途径。

- **模型生态碎片化困扰用户**（#4269 Grok 0auth、#4692 ChatGPT订阅）：部分模型供应商（如Grok、ChatGPT订阅）在认证方式或流式约束上与SDK假设不一致，用户希望SDK能更灵活地适配。

- **多租户隔离存在疑问**（#4266）：用户在对fork进行安全审计时提出agent-server的多用户场景下per-UID sandbox/mTLS实现未见文档说明，表达了部署层面的不确定性。

- **关于#4672 webhook被token delta刷爆的反响**：用户@VascoSch92在描述时用"every token delta is POSTed to that webhook"强调了问题的严重性，触发该问题的场景是"if a conversation has a webhook configured and the agent streams"——影响范围是所有使用webhook集成且开启流式输出的用户。

**满意点**：#3906这类性能问题提出后很快有对应的PR（#4697），且维护者合并速度不错；#4672在提出次日即被关闭（修复完成），显示出较高的响应效率。

---

### 8. 待处理积压

**长期未响应的Issue（以创建时间排序）**

| Issue | 创建时间 | 最后更新 | 说明 |
|-------|----------|----------|------|
| [#4251](https://github.com/OpenHands/software-agent-sdk/issues/4251) OWASP Memory Guard | 2026-05-14 | 2026-08-28 | 15条评论，已超过3个月，无官方回应或关联PR。 |
| [#4262](https://github.com/OpenHands/software-agent-sdk/issues/4262) air-gap回归测试缺失 | 2026-07-05 | 2026-08-28 | 指出来源扫描无法证明air-gap在升级后不被破坏，属CRITICAL级别，1条评论，无维护者答复。 |
| [#4266](https://github.com/OpenHands/software-agent-sdk/issues/4266) 多租户隔离疑问 | 2026-07-05 | 2026-08-28 | 超过7周无维护者回应。 |
| [#4304](https://github.com/OpenHands/software-agent-sdk/issues/4304) CI稳定性审计 | 2026-07-29 | 2026-08-28 | 已满1个月，仅1条评论，无跟进。 |
| [#4015](https://github.com/OpenHands/software-agent-sdk/issues/4015) 技能加载冲突可视化 | 2026-07-07 | 2026-08-28 | 提出用户可见的skill加载警告，无回应。 |

**长期未合并的PR（按创建时间排序）**

|

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目日报 — 2026-08-29

## 今日速览

项目活跃度高且健康：24小时内处理了51条 Issue（其中45条关闭/解决），18条 PR 中10条已合并/关闭。发布 v0.84.4 新版本，新增终端能力覆盖与扩展 UI 事件，并修复了长期困扰用户的自动压塑不触发、TUI 渲染异常等问题。社区对 XDG 目录规范（52👍）、压塑失败（20👍）等诉求关注度高，整体处于快速迭代与问题收敛并行的良好节奏。

---

## 版本发布

### v0.84.4
**链接**: https://github.com/earendil-works/pi/releases/tag/v0.84.4

- **终端能力覆盖（Terminal capability overrides）**：允许用户手动覆盖检测到的终端超链接、图像与 truecolor 支持，适配有误检测或特殊需求的终端环境。详见 [Capability Overrides 文档](https://github.com/earendil-works/pi/blob/v0.84.4/packages/coding-agent/docs/terminal-setup.md#capability-overrides)。
- **扩展 UI 提示事件（Extension UI prompt events）**：新增扩展相关的 UI 事件，便于扩展开发者感知并响应界面提示流程（详情见 Release 页面）。

未提及破坏性变更，升级风险较低；扩展 UI 事件新增为扩展开发者提供了更多自定义空间。

---

## 项目进展

今日合并/关闭的关键 PR 在稳定性与体验两个维度均有显著推进：

| PR | 内容 | 影响 |
|---|---|---|
| [#8782](https://github.com/earendil-works/pi/pull/8782) | **compact before post-tool model requests**：在工具调用后的下一轮请求前执行阈值压塑 | 直接修复 #6879（自动压塑超过100%不触发），避免 API 因超限报错 |
| [#8787](https://github.com/earendil-works/pi/pull/8787) | **限制 Codex WebSocket→SSE 回退范围**：仅在 oversized frame（close code 1009）时回退 | 解决 #4133 带来的过度回退副作用，提升连接稳定性 |
| [#8674](https://github.com/earendil-works/pi/pull/8674) | **Markdown 软换行渲染为空格**，修复 thinking block 显示为锯齿行的问题 | 显著改善 TUI 阅读体验，修复 #8673 |
| [#8764](https://github.com/earendil-works/pi/pull/8764) | **尊重 `settings.shellPath`**：`!` 命令解析时读取自定义 shell 配置 | Windows 用户配置兼容性修复（#8763） |
| [#8786](https://github.com/earendil-works/pi/pull/8786) | **Slash 自动补全按 skill 裸名匹配** | 修正 `/idea` 被错误匹配到 `skill:deep-research` 的排序问题 |
| [#8784](https://github.com/earendil-works/pi/pull/8784) | **MiniMax-M3 的 `max_tokens` 上限按模型截断**（OpenRouter/GMICloud 524,288 上限） | 修复生产者返回 400 的兼容性问题 |
| [#6848](https://github.com/earendil-works/pi/pull/6848) | **压塑摘要增加指数退避重试** | 修复 #6647（瞬时流中断导致压塑失败） |

整体来看，项目今日重点在修复压塑流程、TUI 渲染细节与模型接入兼容性，同时有 5 条涉及 TUI 体验与主题的新 PR 处于待审状态，下一版本 UI 表现值得期待。

---

## 社区热点

### 1. [#6879 auto-compaction 不触发（已关闭）](https://github.com/earendil-works/pi/issues/6879)
- **数据**：评论 24 | 👍 20 | 关闭于今日
- **诉求**：在 GPT-5.6-sol 上单轮 agentic 运行超 2 小时，footer 显示上下文超过 100% 仍未自动压塑，直到 API 在 373k tokens 处拒绝请求。用户建议在 agent 循环后检查压塑需求。
- **今日进展**：PR #8782 已合并，修复该问题。

### 2. [#2870 遵循 XDG Base Directory（已关闭）](https://github.com/earendil-works/pi/issues/2870)
- **数据**：评论 20 | 👍 52 | 关闭于今日（历史最高赞 issue）
- **诉求**：应用在 Linux 上以 `~/.pi` 而非 `$XDG_CONFIG_HOME` 存放配置/状态目录，要求遵循开源社区标准，解放用户 home 目录。52 个 👍 表明这是社区呼声很高的规范化需求。

### 3. [#8584 TUI 流式渲染行损坏（打开）](https://github.com/earendil-works/pi/issues/8584)
- **数据**：评论 22 | 👍 9 | 更新于今日
- **诉求**：工具调用输出长行后，助手文本流式渲染出现“一行一个词”的错乱。多用户可复现，极大影响阅读。
- **状态**：仍未修复，今日有活动但无指定 PR。

### 4. [#7128 系统提示过度鼓励 bash 调用（打开）](https://github.com/earendil-works/pi/issues/7128)
- **数据**：评论 11 | 👍 13
- **诉求**：新加入的“检查 PI_* 环境变量”提示词导致 agent 频繁执行不必要的 env 检查命令，偏向过度使用 bash。反映社区对提示词精准性的高要求。

---

## Bug 与稳定性

### 已修复（今日合并 PR）

| 严重度 | Issue | 问题 | Fix PR |
|---|---|---|---|
| 🔴 高 | [#6879](https://github.com/earendil-works/pi/issues/6879) | 自动压塑在超过100%后不触发，直到 provider 溢出报错（20👍） | [#8782](https://github.com/earendil-works/pi/pull/8782) 已合并 |
| 🟠 中 | [#8166](https://github.com/earendil-works/pi/issues/8166) | 扩展在工具批处理中途注入自定义消息，破坏了 tool_calls→tool 邻接性，导致 DeepSeek 400 错误 | 已关闭（推测含修复） |
| 🟠 中 | [#8673](https://github.com/earendil-works/pi/issues/8673) | TUI 中 Markdown 软换行被渲染为硬换行，thinking block 显示为锯齿列 | [#8674](https://github.com/earendil-works/pi/pull/8674) 已合并 |
| 🟠 中 | [#8762](https://github.com/earendil-works/pi/issues/8762) | `--resume` 会话选择器全量解析每个 session 文件，导致大文件卡顿 | 已关闭（有改进方向） |
| 🟡 低 | [#8789](https://github.com/earendil-works/pi/issues/8789) | Windows 上 `child_process` 缺少 `windowsHide: true`，导致控制台窗口闪烁/抢焦点 | 已关闭 |

### 仍开放中

| 严重度 | Issue | 问题 | 备注 |
|---|---|---|---|
| 🔴 高 | [#8584](https://github.com/earendil-works/pi/issues/8584) | TUI 流式渲染“一行一个词”错乱（22评论，9👍） | 无 fix PR，需关注 |
| 🟠 中 | [#8620](https://github.com/earendil-works/pi/issues/8620) | 0.84.3 升级后所有全局扩展报错 “Cannot find module '@earendil-works/pi-coding-agent'” | 影响 ~/.pi/agent/extensions/，今日更新于 0.84.4 后待确认 |
| 🟡 低 | [#7128](https://github.com/earendil-works/pi/issues/7128) | 系统提示词过度鼓励 bash 调用 | 11评论，13👍，行为类问题 |

---

## 功能请求与路线图信号

### 已有 PR 支撑，可能进入下一版本

| Issue | 需求 | 对应 PR | 状态 |
|---|---|---|---|
| [#5958](https://github.com/earendil-works/pi/issues/5958) | 扩展向用户展示 changelog | [#8790](https://github.com/earendil-works/pi/pull/8790) feat(coding-agent): extensions changelog | 打开待审 |
| [#8796](https://github.com/earendil-works/pi/issues/8796) | 基于项目制品的成功令牌验证门禁 | [#8795](https://github.com/earendil-works/pi/pull/8795) feat: artifact verification repair gate | 已关闭（测试失败，待迭代） |
| [#8761](https://github.com/earendil-works/pi/issues/8761) | 向扩展暴露 TUI 的 openUrl 处理器 | 无直接 PR，但为扩展 API 增强方向 | — |

### 社区新提出（今日）

- **#8791**：向扩展暴露 `ModelRuntime`（3👍），用于创建独立 in-process agent 会话——反映深度用户对扩展生态的进阶诉求。
- **#8798**：`/reload` 时自定义编辑器会丢失 prompt history——扩展自定义 UI 的边界条件 bug。
- **#8800/#8799/#8801**（均为 `cristinaponcela` 提交）：TUI 搜索控件优化、更美观的 “Working…” spinner、alt-mode 滚动条美化——UI 精致化是当前提交者的自发方向。
- **#8802**：新增 `permissions` 配置块（镜像 Codex CLI 的 `sandbox_mode`×`approval_policy` 矩阵）——安全层面向 Codex 对齐的信号。
- **#8792**：`pi update --all` 应尊重 pnpm 的 `minimumReleaseAge`——包管理细节的合规诉求。

---

## 用户反馈摘要

### 真实痛点

1. **压塑不可靠**（#6879，20👍）：“agentic 单轮运行 2 小时，上下文超过 100% 也不压塑，直到 API 拒绝请求”——压塑是长会话用户的刚性需求，已修复。
2. **TUI 渲染错乱**（#8584）：“工具输出长行后，助手文本变成一行一个词，几乎不可读”——高频复现，等待修复。
3. **目录规范**（#2870，52👍）：“应用把 `.pi` 直接丢在 home 目录，污染用户空间”——Linux 用户的强标准化诉求，已修复关闭。
4. **扩展生态摩擦**（#8620）：“升级 0.84.3 后所有扩展都挂了，

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 2026-08-29

## 1. 今日速览

过去 24 小时内 Temporal 项目整体活跃度较高，共产生 63 条 PR 动态（其中 45 条待合并、18 条已合并/关闭），Issue 侧更新 3 条（1 条新开、2 条关闭）。开发重点明确集中在几个方向：**Scheduler V1/V2 演进**、**Nexus 模块重构与日志治理**、**Worker Deployment / Worker Command 可靠性加固（reliability-2026）**。值得关注的是，今日新报告了一个严重 Bug（#11842）：Worker Deployment 的 `routingConfigUpdateState` 永久卡在 `IN_PROGRESS`，导致工作流+活动任务队列无法成为 current，阻塞所有 rollout，目前尚无修复 PR。项目无新版本发布。

---

## 2. 版本发布

无新版本发布，本节省略。

---

## 3. 项目进展

今日共有 18 条 PR 被合并或关闭，以下为对项目功能推进具有重要意义的部分：

- **[#11630] Fix invoker action limit across phases（已合并）**  
  https://github.com/temporalio/temporal/pull/11630  
  修复了 `ExecuteTask` 中终止、取消、启动各阶段独立消耗 `MaxActionsPerExecution` 的问题，改为各阶段共享同一份 action 预算，避免超限。属于命令执行路径的可靠性修复。

- **[#11052] Handle zombie and orphan workflows on replication create path（已合并）**  
  https://github.com/temporalio/temporal/pull/11052  
  在被动复制应用路径上，当 `currentRunID == ""` 时，现在会保留传入的执行状态并以 `CreateWorkflowModeBypassCurrent` 模式持久化，正确处理“孤儿/僵尸工作流”。该 PR 从 7 月 14 日创建至今，是复制稳定性方向的长期改进。

- **[#11827] Sort BufferedStarts by due time on CHASM-to-V1 rollback（已合并）**  
  https://github.com/temporalio/temporal/pull/11827  
  修复 CHASM 调度器回滚到 V1 时，`BufferedStarts` 未按 `ActualTime` 排序的问题，使回滚后的事件触发顺序与原有逻辑一致。

- **[#11850] Allow delegation of user batch to admin batch（已合并）**  
  https://github.com/temporalio/temporal/pull/11850  
  `tdbg`（Temporal Debugger）新增能力，可在 `temporal-system` namespace 中执行用户批量操作，用于在用户 namespace 被限流等极端情况下辅助取消工作流。

- **[#11648] Documentation for worker command task queue kind（已合并）**  
  https://github.com/temporalio/temporal/pull/11648  
  补充文档说明：worker command 控制队列使用 `TASK_QUEUE_KIND_WORKER_COMMANDS`，为开发者提供指引。

此外，多个关键 PR 仍在待合并状态，属于较大功能块，包括：
- **Worker callbacks 功能**（#11589）——进入 `feature/worker-callbacks` 分支，整个功能尚未合入 `main`。
- **Scheduler V2 replay fidelity**（#11463）——包含 V1 历史收集器、replay CLI、CHASM 状态比对等。
- **Scheduler V1 版本控制 stack**（#11831 + #11856）——先是按迭代重新评估 V1 版本上限，再新增 namespace 级 promotion 控制，以激活更高版本行为。

---

## 4. 社区热点

- **[#11842] Worker Deployment routingConfigUpdateState 卡死问题（新开/严重 Bug）**  
  https://github.com/temporalio/temporal/issues/11842  
  今日新开的 Issue，作者 @pnoker 详细报告了使用 `SetWorkerDeploymentCurrentVersion` 提升 build 到 current 后，`routingConfigUpdateState` 永远停留在 `IN_PROGRESS`，导致工作流/活动任务队列永远无法变为 current，所有 rollout 被卡死。虽然暂无评论，但问题性质属于生产阻断级别，预计将引发大量关注。

- **[#11718] 在 release archive 中提供 temporal development CLI（已关闭，2 条评论）**  
  https://github.com/temporalio/temporal/issues/11718  
  用户 @sinux-l5d 使用 Mise 管理项目依赖，希望官方 release archive 中直接包含 development CLI 二进制，以方便自动化工具安装。该 Issue 目前已关闭，但评论和讨论可能涉及替代方案（如单独分发 CLI）。

- **[#11856] Scheduler：新增 `worker.schedulerV1VersionOverride`（新 PR）**  
  https://github.com/temporalio/temporal/pull/11856  
  作为 2/2 stack 中的高层控制 PR，该 PR 为 Scheduler V1 提供 namespace 级行为版本控制。它与 #11831 配合，解决“动态配置只能设置上限、但无法主动激活更新版本行为”的困境。这反映了社区对 Scheduler 版本演进可控性的迫切需求。

---

## 5. Bug 与稳定性

按严重程度排列：

- **[严重] Worker Deployment routingConfigUpdateState 永久卡住（#11842，无 fix PR）**  
  https://github.com/temporalio/temporal/issues/11842  
  新报告的严重 Bug，影响所有使用 Worker Deployment + versioning 的生产用户。`routingConfigUpdateState` 无法推进到 `COMPLETED`，导致无法将新 build 设为 current，所有 rollout 被阻塞。当前没有关联的修复 PR，需要维护者尽快排查。

- **[中] Worker shutdown poll 注册竞争（#11841，有 fix PR）**  
  https://github.com/temporalio/temporal/pull/11841  
  修复了 worker 关闭期间 poll 注册与 shutdown cache 检查之间的竞态：先注册 poll，再检查 shutdown 状态，避免关闭请求遗漏正在启动的 poll。

- **[中] perNamespaceWorker 初始化数据竞争（#11825，有 fix PR）**  
  https://github.com/temporalio/temporal/pull/11825  
  修复 `perNamespaceWorker` 初始化时未持有锁就注册动态配置回调的问题，防止回调在 `ns`/`count`/`opts` 被赋值前触发导致 nil 引用。

- **[中] 检测 missing worker command poller 耗时过长（#11851，有 fix PR）**  
  https://github.com/temporalio/temporal/pull/11851  
  当 worker 消失时，每次 `DispatchNexusTask` 尝试会阻塞 goroutine 长达 10 秒。该 PR 在失败原因仅为 `UpstreamTimeout`（poller 超时）时停止重试，而 gRPC 不可达等传输错误仍会重试。

---

## 6. 功能请求与路线图信号

- **[#11844] Rust SDK 支持（新开，已关闭）**  
  https://github.com/temporalio/temporal/issues/11844  
  用户请求官方 Rust SDK。虽然 Issue 在 24 小时内被关闭（可能是重复 Issue 或已通过其他渠道响应），但这是社区反复出现的需求信号。结合 Temporal 已提供 TypeScript、Java、Go、Python 等 SDK 的现状，Rust SDK 是否纳入路线图值得关注。

- **[#11718] Release archive 包含 development CLI（已关闭）**  
  https://github.com/temporalio/temporal/issues/11718  
  用户希望通过 Mise 等工具直接安装 Temporal CLI。关闭可能意味着已在其他仓库（如 `temporalio/cli`）解决，但仍反映用户对开箱即用工具链的期望。

- **Scheduler V1 版本控制方向（#11831 + #11856）**  
  这两个 PR 构成一个完整的功能栈：允许按 namespace 动态调整 Scheduler V1 的行为版本，而不是只能依赖二进制内静态版本。这暗示团队正在为 Scheduler 引入更平滑的版本升级路径。

- **Worker callbacks 大型功能（#11589）**  
  虽然 PR 仍在 `feature/worker-callbacks` 分支中，但鉴于它汇聚了多阶段 PR 栈，说明该功能正在推进中。从 PR 描述来看，它实现了完整的 Worker callbacks 机制，可能是下一个里程碑版本的重要能力。

---

## 7. 用户反馈摘要

- **Mise 用户希望 CLI 随 release archive 分发（#11718）**  
  用户 @sinux-l5d 使用 Mise 管理依赖，发现 Mise 只安装 release archive 中的二进制，而 Temporal development CLI 不在其中。用户不得不寻找替代安装方式，属于工具链集成体验问题。

- **生产 rollout 被严重阻塞（#11842）**  
  用户 @pnoker 在 Issue 中提供了完整复现路径和预期行为对比：`SetWorkerDeploymentCurrentVersion` 后，路由配置应快速传播完成，但实际永久卡在 `IN_PROGRESS`。这直接影响生产环境的部署效率和稳定性，是最紧迫的用户痛点。

- **Rust 开发者对官方 SDK 的期待（#11844）**  
  用户 @hongbo-miao 的请求非常简洁，仅表达“Rust SDK 会很棒”。虽然信息量有限，但代表了 Rust 生态开发者对 Temporal 的持续兴趣。

---

## 8. 待处理积压

- **[#11463] Schedule V2 replay fidelity（PR，8 月 10 日创建，至今开放）**  
  https://github.com/temporalio/temporal/pull/11463  
  这是 Schedule V2 的重要质量保障 PR，涉及 replay 工具链、预算控制、数据脱敏等。开放式时间较长，可能因为功能复杂或在等待 review，建议维护团队关注。

- **[#11757] Tag Nexus logs by lifecycle stage（PR，8 月 24 日创建）**  
  https://github.com/temporalio/temporal/pull/11757  
  为 Nexus 日志添加 `nexus-stage` 标签，便于运维关联不同生命周期阶段的日志。属于可观测性改进，等待合并中。

- **[#11790] Add test-only passive replication hook seams（PR，8 月 25 日创建）**  
  https://github.com/temporalio/temporal/pull/11790  
  为被动复制测试栈添加 namespace 级测试钩子，是复制测试基础设施的补充。当前仍待 review。

- **[#11807] Dedupe visibility archival（PR，8 月 26 日创建）**  
  https://github.com/temporalio/temporal/pull/11807  
  针对 S3/GCS visibility archival 提供 opt-in 的内容感知去重（SHA-256 哈希比对）。该 PR 可显著降低对象存储成本，但需要评估哈希碰撞和兼容性影响。

---

**总体评估**：Temporal 今日开发节奏紧凑，Scheduler、Nexus、Worker 可靠性三条主线并进。项目健康度总体良好，但 #11842 的严重 Bug 需要优先处理，建议维护者尽快定位根因并给出修复时间表。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*