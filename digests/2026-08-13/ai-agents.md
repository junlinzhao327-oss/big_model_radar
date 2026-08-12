# OpenClaw 生态日报 2026-08-13

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-12 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 开源项目动态日报 — 2026-08-13

> 数据周期：2026-08-12 ~ 2026-08-13 | 数据来源：github.com/openclaw/openclaw


## 1. 今日速览

过去 24 小时 OpenClaw 项目保持极高活跃度：累计 500 条 Issue 更新（新开/活跃 327 条，关闭 173 条）与 500 条 PR 更新（待合并 302 条，已合并/关闭 198 条），无新版本 Release。值得关注的是，高热度 Issue 集中在会话状态丢失、真实语音资源泄漏、以及消息静默失败等稳定性问题上，其中多个 P0/P1 级 Bug 已获得维护者响应并关联修复 PR。PR 侧则呈现多路并进的态势：既有对 Codex/ACP 子代理生命周期的深度修复，也有 Portal 暴露开发服务器等新功能尝试。整体来看，项目处于高强度迭代期，稳定性修复的密度与深度均在提升，但历史遗留问题（如 #116277 关闭后静默回复失败仍复发）说明部分修复的彻底性仍需验证。


## 2. 版本发布

无新版本发布（最新 Releases 为空）。当前代码库处于高频 PR 合并状态，下一个版本可能包含近期密集的安全与稳定性修复。


## 3. 项目进展

今日共有 198 个 PR 被合并或关闭，以下为本期值得关注的核心变更：

**子代理与 ACP 生命周期修复**

- [PR #122849 fix(agents): preserve ACP lifecycle ownership](https://github.com/openclaw/openclaw/pull/122849)（新开，M 规模）：将 ACP 运行保留在规范的 `acp` 任务所有者之下，同时保留子代理注册表中的拓扑/控制观察者身份，消除重复的 `subagent` 任务投影与子会话清理权限错位。
- [PR #122503 fix(codex): retain direct-child hook policy after parent yield](https://github.com/openclaw/openclaw/pull/122503)（等待作者响应，修复 #111010 / #118534）：修复 Codex 代理委托直接原生子代理后 yield 导致 hook 策略丢失的问题，影响面覆盖 docs/agents/codex/xai，标注了兼容性、会话状态与安全边界三重合并风险。

**渠道与消息可靠性**

- [PR #122832 [BACKPORT] fix(slack): stop repeated outage notices in active threads](https://github.com/openclaw/openclaw/pull/122832)（已关闭，Backport）：将已合并的 Slack 修复回溯至内部分支，避免活跃线程中重复推送 Codex 认证/后端故障通知。
- [PR #116232 fix(whatsapp): stop retrying transport-level timed-out sends](https://github.com/openclaw/openclaw/pull/116232)（待合并）：修复传输层超时但消息已实际送达时，重试导致重复投递的问题。

**开发者体验与工具链**

- [PR #122848 test(core): remove duplicate assertions](https://github.com/openclaw/openclaw/pull/122848)、[PR #122847 fix(tooling): fail deadcode report on scan errors](https://github.com/openclaw/openclaw/pull/122847)、[PR #122839 ci: keep dependency snapshots warm for package metadata](https://github.com/openclaw/openclaw/pull/122839)（已关闭）：三项由 @steipete 提交的基础设施清理，分别精简重复测试断言、修复 deadcode 扫描假阳性退出码、减少 CI 冷启动依赖构建时间。

**新功能探索**

- [PR #122536 feat: portals — expose agent-run dev servers to the operator](https://github.com/openclaw/openclaw/pull/122536)（新开，XL 规模）：当代理构建或修复 Web 应用时，以“门户”形式将开发服务器暴露给操作者，解决远程/容器环境下无法直接访问代理输出服务的痛点。
- [PR #122846 agent-core: add per-response tool-call block cap (maxCallsPerBlock)](https://github.com/openclaw/openclaw/pull/122846)（新开）：为单次响应中的工具调用数量设置上限，防止 CLI 回环关联缓冲区溢出时整批工具返回 `unknown`。

项目整体在“子代理所有权模型”“CLI/渠道消息可靠性”“开发者工具链体验”三线上同时推进。`maxCallsPerBlock` 与 Portal 特性属于新能力引入，前者补足工具调用安全边界，后者优化远程操作体验，均有可能进入下一版本。


## 4. 社区热点

**最热 Issue**

1. [Issue #121058 Silent reply failures still recurring after #116277 closed](https://github.com/openclaw/openclaw/issues/121058) — 91 条评论
   用户 @sloptop-the-terrible 报告，被标记关闭的静默回复失败问题仍在持续发生，监控 cron 在关闭后仍记录到新故障。高讨论度反映出社区对“修复未生效”类问题的高度敏感，也说明 #116277 的修复方案并未覆盖全部触发路径。

2. [Issue #116201 Realtime voice work can retain unbounded provider and consult state](https://github.com/openclaw/openclaw/issues/116201) — 65 条评论，diamond lobster 评级
   实时语音会话在高延迟/突发流量下，产生无界保留的 provider 帧、咨询工作与前音频播放状态。该问题已被 `clawsweeper` 标记，包含`needs-product-decision` 与 `needs-maintainer-review`，属于资源所有权设计层面的深度问题。

3. [Issue #25592 Text between tool calls leaks to messaging channels](https://github.com/openclaw/openclaw/issues/25592) — 47 条评论，diamond lobster 评级，P1
   工具调用之间的过程性文本（错误处理、状态说明）被误路由为 Slack/iMessage 可见消息，属于高频 UX 痛点。该问题自 2 月创建以来持续获得关注，当前仍处于安全审查与产品决策阶段，尚未有对应修复 PR。

**高反应 PR**

- [PR #122846 agent-core: add per-response tool-call block cap](https://github.com/openclaw/openclaw/pull/122846)（新开即获高关注）：单条消息超过 4-5 个工具调用时 TUI 整批报 `run error: unknown`，是 CLI 重度用户常见的挫败点。
- [PR #122536 feat: portals](https://github.com/openclaw/openclaw/pull/122536)：代理构建 Web 应用时的访问痛点引发广泛共鸣，远程/容器开发场景下缺乏一等公民的访问通道。

**社区诉求解析**：从热点议题来看，社区最强烈的诉求集中在两方面：一是会话状态与消息不丢失（静默失败、消息泄漏、子代理丢失），二是对长时间运行的代理任务的可观测性与可控性（实时语音、任务状态面板、开发者服务器门户）。这两类诉求均指向同一个核心——生产环境中 AI Agent 的可靠性。


## 5. Bug 与稳定性

**P0 / 严重（存在崩溃、数据丢失或大面积停机风险）**

- [Issue #91588 Gateway Memory Leak — RSS grows from 350MB to 15.5GB over days](https://github.com/openclaw/openclaw/issues/91588)（P0, platinum hermit）：Gateway 进程 RSS 从 350MB 增长至 15.5GB 后被 OOM 杀死，触发 launchd-handoff 反复重启。当前标记 `needs-live-repro`，尚未有对应修复 PR。

**P1 / 高（功能不可用或产生错误结果）**

- [Issue #97983 iOS/WebChat messages append but do not trigger assistant replies](https://github.com/openclaw/openclaw/issues/97983)（P1, diamond lobster）：消息进入转录但不触发回复，`--deliver` 亦无法投递。属于移动端核心链路故障，有稳定复现路径但无修复 PR。
- [Issue #103231 claude-cli backend ownsNativeCompaction assumption is false](https://github.com/openclaw/openclaw/issues/103231)（P1, platinum hermit）：`claude-cli` 声明拥有原生压缩权，但实际调用方式并不生效，导致会话超过 200% 上下文且无任何回收路径。
- [Issue #111857 CLI budget reopens full compacted JSONL branch](https://github.com/openclaw/openclaw/issues/111857)（P1, diamond lobster）：CLI 预算计算重新读取已压缩的完整 JSONL，导致父会话被反复压缩。已标记 `source-repro`，尚无修复 PR。
- [Issue #114234 Usage-cost refresh lock never releasable after PID reuse in containers](https://github.com/openclaw/openclaw/issues/114234)（P1, diamond lobster）：容器中 PID 复用导致 usage-cost 缓存永久冻结。已有链接 PR，fix 在路上。
- [Issue #97616 OpenClaw leaks unreaped hook/tool child processes](https://github.com/openclaw/openclaw/issues/97616)（P1）：子进程僵尸累积导致运行时退化，等待更多信息中。

**P2 / 中（功能异常但可绕过）**

- [Issue #115001 Hybrid memory search returns spurious 1.0 similarity scores via FTS LIKE-fallback](https://github.com/openclaw/openclaw/issues/115001)（P2, diamond lobster）：混合记忆搜索的 FTS LIKE 回退路径硬编码 textScore 为 1.0，产生虚假高相似度结果。已有链接 PR。
- [Issue #114154 bundle-mcp tool passes policy but agent sessions never bundle it](https://github.com/openclaw/openclaw/issues/114154)：MCP 工具在策略与健康检查均通过的情况下，代理会话永远无法加载该工具。
- [Issue #83337 Plugin/core version drift after upgrade causes silent channel failure](https://github.com/openclaw/openclaw/issues/83337)：核心升级后插件版本不同步导致渠道静默失效。

**已有关联修复 PR 的 Issue**

| Issue | 关联 PR | 状态 |
|---|---|---|
| [#111010 / #118534 Codex hook 策略丢失](https://github.com/openclaw/openclaw/pull/122503) | [PR #122503](https://github.com/openclaw/openclaw/pull/122503) | 等待作者 |
| [#98403 plugin.approval 拒绝 null 元数据](https://github.com/openclaw/openclaw/issues/98403) | [PR #103530](https://github.com/openclaw/openclaw/pull/103530) | 待合并 |
| [#122262 composer 能力子菜单溢出视口](https://github.com/openclaw/openclaw/issues/122262) | [PR #122296](https://github.com/openclaw/openclaw/pull/122296) | 待维护者关注 |
| [#41966 MEDIA: token 在代码块中被跳过无提示](https://github.com/openclaw/openclaw/issues/41966) | [PR #80396](https://github.com/openclaw/openclaw/pull/80396) | 待验证 |

**风险评估**：在全部待合并的 302 个 PR 中，有 8 个标注了 `merge-risk: 🚨 security-boundary`，5 个标注 `🚨 session-state`，4 个标注 `🚨 message-delivery`。这些 PR 尽管修复明确，但合并时需格外谨慎回归测试。


## 6. 功能请求与路线图信号

**高潜力新功能（已有对应 PR）**

- **Portal — 暴露代理开发服务器**（[PR #122536](https://github.com/openclaw/openclaw/pull/122536)）：为“代理构建 Web 应用”场景提供一等公民访问入口，贴合 AI 编程助手落地需求，预计进入下一版本讨论。
- **每响应工具调用上限 maxCallsPerBlock**（[PR #122846](https://github.com/openclaw/openclaw/pull/122846)）：缓解工具调用突发导致的回环缓冲溢出，是低成本高收益的稳定性改进。
- **Grok 4.6 目录与 OAuth xhigh 保留**（[PR #122762](https://github.com/openclaw/openclaw/pull/122762)）：跟进 xAI 旗舰模型发布，同步目录、能力元数据与 OAuth 行为。

**热门的纯功能请求（暂无对应 PR）**

- [Issue #42475 Per-agent cost budget enforcement at the gateway level](https://github.com/openclaw/openclaw/issues/42475)（23 条评论）：网关级按代理的日/月成本上限，防止失控支出。属于运营侧刚需。
- [Issue #42840 Add MathJax/LaTeX Support to Control UI](https://github.com/openclaw/openclaw/issues/42840)（8 条评论，👍 10）：控制 UI 数学公式渲染。科学计算用户的高频请求。
- [Issue #87295 LTS version](https://github.com/openclaw/openclaw/issues/87295)（5 条评论，👍 4）：企业用户对长期支持版本的呼声。
- [Issue #99583 Intelligent Session Auto-Titling](https://github.com/openclaw/openclaw/issues/99583)：基于 LLM 的会话自动命名（标题懒生成 + 话题感知重命名），已有 `llm-slug-generator` 基础。
- [Issue #50199 Skill Priority Configuration](https://github.com/openclaw/openclaw/issues/50199)：重叠技能的选择优先级配置，解决多技能冲突。
- [Issue #52640 Persistent task-status surface for long-running channel turns](https://github.com/openclaw/openclaw/issues/52640)：长时间运行的渠道轮次需要持久化任务状态面板。

**路线图信号**：结合合并中的 PR 与高热度请求，项目短期优先方向为 ① 子代理会话模型重构（#114388 multi-agent ownership 显式化），② 实时语音链路资源治理（#116201），③ 消息可靠性兜底（静默失败、重复投递、泄漏），④ 开发者体验（Portal、CLI 文档、命令参考自动生成）。


## 7. 用户反馈摘要

**频发的真实痛点**

1. **“修复了但又没修好”**：Issue #121058 中用户明确指出“#116277 关闭了但问题还在发生”，监控工具仍在记录新的失败事件。这提示维护者在关闭稳定性相关 Issue 前，需确认修复覆盖所有触发路径。
2. **子代理任务丢失**：Issue #44925 与 #47975 分别描述了子代理完成结果静默丢失、子代理会话持久化后主会话无响应的问题。在多代理编排场景下，这些直接影响任务可靠性。
3. **会话上下文失控**：Issue #103231 报告 claude-cli 后端会话增长超过 200% 上下文且所有回收路径静默失效；#111857 报告 CLI 预算错误读取完整 JSONL 导致父会话被反复压缩。用户对“上下文管理”相关的配置与默认行为有较高期待。
4. **渠道消息污染**：Issue #25592 中“工具调用之间的文本泄漏到 Slack”已收获 47 条评论，用户明确表示这是“显著的 UX 问题”。
5. **安装与升级破碎**：Issue #60398（home 目录在外部 APFS 卷时 gateway 安装失败）、#83337（插件版本错位导致渠道静默失效）反映出边缘环境下的体验仍需加强。

**正面反馈信号**
- PR #122503 中显式标注“AI-assisted implementation and review... sanitized local agent transcript included with user's approval”，说明开发者社区已开始在 OpenClaw 开发流程中深度使用 AI 辅助编码，并形成可追溯的协作范式。
- 多个 PR 附带了“proof: sufficient" / "proof: screenshot”，社区贡献者对验证质量的

---

## 横向生态对比

# AI Agent 开源生态横向对比分析报告

**报告日期：2026-08-13 | 数据窗口：过去 24 小时 | 覆盖项目：OpenClaw、Hermes Agent、Pi、LiteLLM（OpenHands SDK 与 Temporal 当日无动态数据）**

---

## 1. 生态全景

个人 AI 助手/自主智能体开源生态正处于**高强度迭代期**：4 个有数据的项目今日合计产生超过 1,080 条 Issue 更新与 1,300 条 PR 更新，但均无新版本 Release，说明各项目正为下一个版本密集储备代码。社区舆论重心高度一致——**会话可靠性、token 成本控制、子代理生命周期管理**成为横跨所有项目的共性痛点。各项目正从"功能铺量"转向"生产化打磨"，Windows 兼容性、本地模型支持和插件/技能生态开始浮现为新的差异化竞争点。整体生态竞争格局未定，OpenClaw 与 Hermes 在体量上领跑，但 Pi 的效率和质量控制指标更优。

---

## 2. 各项目活跃度对比

| 项目 | Issue 更新（新开/活跃） | Issue 关闭 | PR 更新（待合并） | PR 合并/关闭 | Release | 健康度评估 |
|---|---|---|---|---|---|---|
| **OpenClaw** | 500（327） | 173 | 500（302） | 198 | 无 | ⚠️ 高速迭代但稳定性存疑：P0 内存泄漏未修，静默失败问题"关闭后复发"（#121058），302 个待合并 PR 积累较重 |
| **Hermes Agent** | 439（353） | 86 | 500（398） | 102 | 无 | ✅ 架构清理收官：god-file sharding 20/20 完成，Windows 原子替换修复整合 5 个重复 PR，但 398 个待合并 PR 为积压隐患 |
| **Pi** | 70（14） | 56 | 31（7） | 24 | 无 | ✅ 质量巩固期标杆：Issue 关闭率 80%、PR 合并率 77%，响应迅速，但规模较小说明社区基数有限 |
| **LiteLLM** | 73（54） | 19 | 270（158） | 112 | 无 | ⚠️ 功能推进正常但存量问题积压：存在 3–6 个月未关闭的 P1 级 issue（Redis 计数泄漏 #27955、Anthropic 转换器 #27168） |
| **OpenHands SDK** | — | — | — | — | — | 当日无动态数据 |
| **Temporal** | — | — | — | — | — | 当日无动态数据 |

**体量分层**：OpenClaw 与 Hermes 处于同一量级（日均 500 PR 更新），约等于 LiteLLM 的 2 倍、Pi 的 16 倍。但**高 PR 量伴随高待合并积压**，OpenClaw 302 条 + Hermes 398 条待合并 PR 共同暗示：两个头部项目的维护者吞吐能力已接近瓶颈。

---

## 3. OpenClaw 在生态中的定位

### 核心优势

- **社区规模与讨论深度领先**：最热 Issue #121058（静默回复失败）达 91 条评论，远超 Hermes（70 条）、Pi（26 条）、LiteLLM（11 条）的热度峰值。`diamond lobster` 评级机制和 P0/P1 分级体系使问题可见度更高。
- **多 Agent 编排为第一公民**：唯一将子代理/ACP 生命周期所有权作为核心架构问题的项目（PR #122849 消除 `subagent` 任务投影冲突、PR #122503 修复 Codex 委托后 hook 策略丢失）。OpenClaw 的"任务所有权"模型比 Hermes 的"通用 ACP 客户端"提案（#5257）更早进入工程实现。
- **频道矩阵完整**：Slack/WhatsApp/iMessage/WebChat 全覆盖，配合 voice、Portal（暴露代理开发服务器）等新探索，是唯一同时押注"消息渠道 + Web 应用交付"双场景的项目。

### 相对短板

- **稳定性公信力受损**：#121058 中用户明确指出"#116277 关闭了但问题还在发生"，P0 级 Gateway 内存泄漏（350MB→15.5GB）长期无修复 PR。相比之下 Hermes 已将 P0 并发竞态（#64934）关闭，Pi 的 bug 修复周期控制在数天内。
- **合并效率偏低**：302/500 的 PR 待合并率（60%）高于 Pi（23%）和 LiteLLM（59%），8 个 `security-boundary` 风险 PR 加剧了合并决策的复杂度。

### 生态位总结

OpenClaw 是当前生态中**野心最大、覆盖最全的自主智能体网关**，定位偏向"多 Agent 生产的操作系统"；Hermes 是更务实的"多渠道助手 + 插件平台"；Pi 是"开发者个人的高效终端伙伴"；LiteLLM 则是底层的"模型流量调度层"，与前三者构成上下游关系而非直接竞争。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 | 热度信号 |
|---|---|---|---|
| **Token 成本控制** | Hermes、Pi、OpenClaw | Hermes：73% API 调用 token 消耗在固定开销（约 13.9K），要求 lazy tool schema 加载；Pi：auto-compaction 在 373k tokens 才触发导致 API 拒绝（17👍）；OpenClaw：claude-cli 上下文超 200% 无回收路径、CLI 预算错误重读完整 JSONL | 已从"优化建议"升级为"生产环境经济损失"级别的强诉求 |
| **会话/消息可靠性** | OpenClaw、Hermes、Pi | OpenClaw：静默回复失败复发、消息泄漏至频道（47 评论）、P0 内存泄漏；Hermes：state.db 修复后反复损坏、clarify 调用挂起；Pi：流式事件丢失 usage 数据（0.84.0 回归） | 各项目最热 issue 均属此类，是当前生态第一优先级 |
| **Windows 支持** | Hermes、Pi、LiteLLM | Hermes：今日合并原子替换修复、关闭 5 个重复 PR，桌面重启吞网关（#83683）；Pi：官方发起 Windows 体验调研（26 评论）；LiteLLM：Python 3.13 无可用 wheel | 头部项目多数在 Windows 有平台性缺陷，桌面端用户基数正在倒逼修复 |
| **多 Agent 编排标准化** | OpenClaw、Hermes | OpenClaw：ACP 所有权模型深度修复（PR #122849）；Hermes：Generalized ACP Client 提案（22👍），从 ACP 服务端扩展为可编排 Claude Code/Copilot/Codex 的中枢 | 双方路线不同（OpenClaw 自研生命周期，Hermes 做通用编排），但都确认 ACP 是核心方向 |
| **插件/技能生态** |

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-13

## 1. 今日速览

过去24小时项目活跃度极高：**439条 Issues 更新**（新开/活跃 353 条，关闭 86 条）与 **500条 PR 更新**（待合并 398 条，已合并/关闭 102 条）。值得关注的是，Repo 级 god-file sharding Epic（#78647）宣告 **20/20 全部完成**，标志着持续数周的架构清理战役收官；同时多个 Windows 平台 `atomic_replace` 修复 PR 在同日合并/关闭，结束了长期悬而未决的重复提交与功能回退问题。今日无新版本发布，但代码库合并活动密集（102 条 PR 被合并/关闭），整体项目健康度良好，社区讨论热度集中在 **token 成本优化** 与 **插件接口扩展** 两大方向。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日合并/关闭的 PR 集中在 **Windows 稳定性修复** 与 **架构清理沉淀** 两个维度：

- **#84852 [已合并]** `fix(utils): recover Windows renames contended by an open handle` —— 维护者整合了此前五个各有缺陷的修复 PR，统一解决了 Windows 上 `atomic_replace()` 因文件被其他句柄占用而失败、写入静默丢失的问题。这次合并同时关闭了 #36921、#73807、#45022、#79793、#57777 五个重复 PR，源码树得到一次有效清理。 → https://github.com/NousResearch/hermes-agent/pull/84852

- **#23998 [已合并]** `fix(bluebubbles): use 127.0.0.1 literal for loopback webhook URL` —— 修复 macOS 下 BlueBubbles 适配器将 127.0.0.1 改写为 localhost 导致 webhook 注册失败的问题。 → https://github.com/NousResearch/hermes-agent/pull/23998

- **#78647 [已关闭]** `[EPIC — COMPLETE] All Gods Must Die: 20/20 killed` —— god-file sharding epic 全部 20 个目标文件完成拆分，`needs-decision` 标签已移除。该 Epic 的完成意味着 repo 内不再有超大单体文件（此前最大的两个文件各超 7,000 行，见 #78642、#78641）。 → https://github.com/NousResearch/hermes-agent/issues/78647

- **#64934 [已关闭]** `Two turns can run concurrently on one gateway session` —— 此前标记为 **P0** 的会话并发竞态问题（两个 turn 同时运行导致 transcript 交错刷新）随 #67401 修复方案落地后正式关闭，相关修复已在近期版本中生效。 → https://github.com/NousResearch/hermes-agent/issues/64934

- **#63177、#67629 [均已关闭]** 两起 Windows `search_files` 绝对路径失败问题（MSYS_NO_PATHCONV 冲突、`_bash_safe_path` 重写导致 IO error）均标记为已解决，相关平台兼容性问题在近期代码中得到了统一处理。

---

## 4. 社区热点

今日讨论热度集中在一个已完成的 Epic 与三个存在长期争议的功能设计提案上：

- **#78647 — “All Gods Must Die” Epic（70 评论）** 虽然已关闭，但作为项目架构方向的标志性议题，其存量讨论仍在持续。社区对这一“god-file 全部打散、永不回退”的政策关注度极高。 → https://github.com/NousResearch/hermes-agent/issues/78647

- **#6839 — Lazy Tool Schema Loading（38 评论，18 👍）** 连续四个月保持热度。用户指出当前每次 API 调用注入全部工具 schema（50+ 工具约 3,500–5,000 token），在本地模型上开销尤其高昂。该提案主张采用 two-pass 工具注入以降低 token 消耗。 → https://github.com/NousResearch/hermes-agent/issues/6839

- **#64182 — Plugin Interface Expansion（32 评论）** 由 @teknium1 发起的社区插件接口扩展跟踪 Issue，收集了 Discord 社区在 #plugins-interface-ideas 频道的大量建议，目标是让长期排队中的 PR 能够基于稳定接口快速合入。 → https://github.com/NousResearch/hermes-agent/issues/64182

- **#34352 — Multi-Tenant Hermes Problem（25 评论，3 👍）** 作者报告在生产环境运行多租户修复已达数月，指出 memory 操作完全绕过 hook 系统导致 tenant 隔离无法在不 fork 核心代码的前提下实现。社区对“多人 agentic AI”的需求表达强烈。 → https://github.com/NousResearch/hermes-agent/issues/34352

- **#5257 — Generalized ACP Client（23 评论，22 👍）** 高赞提案，建议将 Hermes 从 ACP 服务端扩展为可编排所有 ACP 兼容编码 agent 的通用客户端（支持 Claude Code、Copilot、Codex 等），使 Hermes 成为多 agent 编排中枢。 → https://github.com/NousResearch/hermes-agent/issues/5257

---

## 5. Bug 与稳定性

### P0 级
- **#64934 [已关闭]** `Two turns run concurrently on one gateway session` — 已随 #67401 修复落地，正式关闭。 → https://github.com/NousResearch/hermes-agent/issues/64934

### P1 级
- **#78069 [OPEN]** `clarify tool free-text response intermittently fails to bind to pending clarify call` — 在 Discord/HomeAssistant 等平台上，工具的自由文本回复偶发无法绑定到挂起的 clarify 调用，导致 turn 无限期挂起。当前 **尚无关联 fix PR**。 → https://github.com/NousResearch/hermes-agent/issues/78069

- **#83683 [OPEN]** `Desktop restart reaps the live gateway but never relaunches it (WeChat/QQ go silent)` — Windows 0.20.0 回归问题：桌面应用每次重启都会强杀消息网关且不重启。**尚无关联 fix PR**。 → https://github.com/NousResearch/hermes-agent/issues/83683

- **#69603 [OPEN]** `state.db repair/re-corrupt cascade` — 数据库修复后数分钟内再次损坏，同一天发生四次。问题根因在于 schema 修复只在进程内串行化，且 sqlite_master 编辑不更新 schema cookie。**尚无关联 fix PR**。 → https://github.com/NousResearch/hermes-agent/issues/69603

- **#5709 [已关闭]** `Responses API paths should never replay tool messages with role=tool` — OpenAI Responses API 不兼容 `role=tool` 消息的问题，已关闭（修复已合入）。 → https://github.com/NousResearch/hermes-agent/issues/5709

- **#72451 [OPEN]** `Successful in-place compression exhausts the shared per-turn attempt budget in long tool loops` — 长工具循环中，即便每次压缩都成功，也会耗尽共享的每 turn 压缩尝试预算，导致后续无法再压缩。**已有相关讨论，但尚无 fix PR**。 → https://github.com/NousResearch/hermes-agent/issues/72451

### P2 级
- **#82936 [OPEN]** `default profile's secrets leak into secondary profile's terminal tool` — `gateway.multiplex_profiles` 开启后，默认 profile 的密钥会泄漏给次要 profile 的 terminal 工具及 Kanban 子进程。安全边界问题，**尚无 fix PR**。 → https://github.com/NousResearch/hermes-agent/issues/82936

- **#78820 [OPEN]** `TUI gateway crashes on Windows with OSError [Errno 22] on stdin readline` — Windows TUI 网关在 stdin 读取时崩溃，进行中的会话丢失。**尚无 fix PR**。 → https://github.com/NousResearch/hermes-agent/issues/78820

- **#63177 [已关闭]** `search_files silently returns 0 results on Windows (rg + MSYS_NO_PATHCONF)` — 已解决。 → https://github.com/NousResearch/hermes-agent/issues/63177

- **#73381 [已关闭]** `Windows Desktop update fails — venv missing cryptography + file locking` — 已关闭（与 #84852 合并的 Windows 文件锁修复相关）。 → https://github.com/NousResearch/hermes-agent/issues/73381

---

## 6. 功能请求与路线图信号

今日无新版本发布，但大量开放中的功能提案正在持续推进。以下信号值得关注：

**高概率进入下一版本：**
- **#6839 — Lazy Tool Schema Loading**（P2, 38 评论, 18 👍）：token 成本优化是社区最强烈的诉求之一。配套的 **#84842 PR** `fix(agent): unified tool dispatch for lazy-loaded MCP tools` 已提交，说明 lazy-load 机制已在开发中，该 PR 修复了懒加载 MCP 工具无法被对话循环识别的调度问题。两者合流后很可能在 0.21.0 落地。 → https://github.com/NousResearch/hermes-agent/issues/6839 | https://github.com/NousResearch/hermes-agent/pull/84842

- **#64182 + #64231 — Plugin Interface Expansion 系列**：@teknium1 主导的插件接口扩展（生命周期事件目录、hook 分类标准、批量处置 pending hook PR）。配套 PR **#84849**（webhook 签名验证提取为 mixin）已在今日提交，属于 “Webhook Revolution campaign” 的一部分，表明插件化重构已经动手。 → https://github.com/NousResearch/hermes-agent/issues/64182 | https://github.com/NousResearch/hermes-agent/issues/64231 | https://github.com/NousResearch/hermes-agent/pull/84849

**社区呼声高但尚处决策期：**
- **#5257 — Generalized ACP Client**（22 👍）：多 agent 编排需求，扩展 Hermes 为 ACP 客户端以统一调度 Claude Code、Copilot、Codex 等工具。若被采纳将显著拓宽 Hermes 的使用场景。
- **#34352 — Multi-Tenant Hermes**：多租户隔离是 B 端用户的核心诉求，但需要核心架构侵入性改动。
- **#8457 — Persistent Session Memory with Cross-Session Search & Auto-Compression**：会话持久化与跨会话搜索，与 #6839 同属 memory/context 成本优化方向。

**新功能 PR 今日入列：**
- **#84848** `fix(xai): preserve xhigh effort and priority service_tier for Grok 4.6` — 适配 Grok 4.6 新增的 xhigh 推理与优先级处理能力。 → https://github.com/NousResearch/hermes-agent/pull/84848
- **#84846** `feat(sessions): heal non-chat orphan rows after 24h idle` — 修复 CLI/cron/ACP/subagent 启动的会话永不关闭导致的 `state.db` 孤儿行膨胀问题（一个实例中 507 行中 215 行处于未关闭状态）。 → https://github.com/NousResearch/hermes-agent/pull/84846
- **#84847** `fix(desktop): resume is read-only; liveness requires real activity` — 修复桌面端已结束会话被误判为活跃状态的问题（#84821 引入的回归）。 → https://github.com/NousResearch/hermes-agent/pull/84847

---

## 7. 用户反馈摘要

- **token 成本焦虑是头号痛点**：#4379 的作者通过自建监控面板量化分析，发现 **73% 的 API 调用 token 消耗在固定开销**（约 13.9K token），在 Telegram/WhatsApp/Cron 多网关部署场景下成本压力明显。该分析得到了 #6839 中 18 个 👍 的社区共鸣。 → https://github.com/NousResearch/hermes-agent/issues/4379

- **多租户部署是真实的 B 端需求**：#34352 作者明确表示“Multiplayer agentic AI is the future. Hermes can and should lead”，并已在生产环境运行自定义修复数月，侧面反映官方实现滞后于用户需求。

- **Windows 用户体验持续承压**：今日关闭的 #73381 与 #42972 均指向 Windows Desktop 安装/

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 2026-08-13

## 今日速览

Pi 项目过去 24 小时保持极高活跃度：共产生 70 条 Issue 更新和 31 条 PR 更新。Issue 关闭率高达 80%（56/70），显示维护团队响应迅速；PR 合并/关闭率 77%（24/31），开发流程顺畅。无新版本发布，当前重心在于修复 Bug、整合社区功能 PR、完善扩展机制。社区关注焦点集中在 Windows 支持体验、上下文压缩（auto-compaction）可靠性、TUI 鼠标交互、编辑工具健壮性等方面。整体项目健康度良好，问题响应和修复效率处于健康区间。

## 项目进展

今日合并/关闭的 PR 覆盖多个方面，项目明显在向“更稳定的核心 + 更开放的扩展生态”方向推进：

- **修复流式事件丢失 usage 数据**（[#7982](https://github.com/earendil-works/pi/pull/7982)，已合并）：解决 0.84.0 回归问题，在 JSON 和 RPC 的 `message_update` 事件中恢复携带累计 usage 字段，同时保持流大小线性增长并补充回归测试。这是对核心协议层的重要修复。
- **TUI 鼠标事件分发机制落地**（[#8037](https://github.com/earendil-works/pi/pull/8037)、[#8032](https://github.com/earendil-works/pi/pull/8032)）：实现 #7683 提出的 `Component.onMouse` 钩子，让扩展组件能接收全屏 TUI 中的鼠标事件。两个 PR 各自独立实现，需关注后续整合。
- **修复 `triggerTurn: false` 仍触发新回合**（[#8022](https://github.com/earendil-works/pi/pull/8022)，已合并）：解决扩展 handler 发送展示用消息时意外启动 assistant 回合的问题。
- **修复技能目录加载误判**（[#8012](https://github.com/earendil-works/pi/pull/8012)，开放中）：`README.md`、`AGENTS.md` 等根级文档不再被误当作技能加载，消除验证警告。
- **修复 Edit 工具单对象参数**（[#8011](https://github.com/earendil-works/pi/pull/8011)，开放中）：支持模型将 `edits` 以单个对象而非数组传入的场景，提升与真实世界模型的兼容性。
- **新增 Grok 4.6 模型支持**（[#8042](https://github.com/earendil-works/pi/pull/8042)，已合并）：xAI Responses 模型集中加入 Grok 4.6。
- **MiniMax 图生图 + 同步语音生成**（[#8030](https://github.com/earendil-works/pi/pull/8030)、[#8014](https://github.com/earendil-works/pi/pull/8014)，已合并）：扩展多模态能力。

另有 Ollama 本地模型代理脚本（[#8049](https://github.com/earendil-works/pi/pull/8049)）、Bedrock 流诊断改进（[#8044](https://github.com/earendil-works/pi/pull/8044)）、HTML 导出支持 Mermaid 渲染（[#7956](https://github.com/earendil-works/pi/pull/7956)）等合并，生态工具链在持续补全。

## 社区热点

1. **[#7547 Windows 使用体验征集](https://github.com/earendil-works/pi/issues/7547)**（26 条评论，1 👍）
   项目方主动发起的 Windows 支持调研帖，已持续 10 天，仍是社区最活跃的讨论。核心诉求是希望明确 Pi 在 Windows 上的最佳运行方式、主要痛点与优先修复方向。这反映出 Windows 用户基数大且需求迫切，是项目需要重点投入的方向。

2. **[#6879 auto-compaction 触发时机过晚](https://github.com/earendil-works/pi/issues/6879)**（17 条评论，17 👍）
   这是当前社区反应最强烈的 Bug：上下文增长超过 100% 后自动压缩不触发，直到 API 在 373k tokens 处拒绝请求才生效。用户期望在每次 agentic 回合后都检查上下文占用。17 个 👍 表明大量用户遭遇过此问题，应列为高优先级。

3. **[#7836 Edit 模糊匹配对空白差异敏感](https://github.com/earendil-works/pi/issues/7836)**（9 条评论，1 👍，标记 inprogress）
   用户发现 Edit 工具的模糊匹配不折叠连续空白，导致内容相同仅空白有差异时匹配失败，实际影响小模型使用 Edit 工具的准确性。

4. **[#7683 TUI 组件鼠标事件支持](https://github.com/earendil-works/pi/issues/7683)**（9 条评论，已关闭）
   该 Feature Request 获得了快速响应，今日已有两个实现 PR（#8032、#8037）。社区对 TUI 扩展能力有明确需求，项目方采纳速度快。

5. **[#7062 OpenAI 兼容流解析缺陷](https://github.com/earendil-works/pi/issues/7062)**（8 条评论，1 👍）
   针对 Databricks 等非标准流式响应的兼容问题：数组形式 content 和缺失 finish_reason 导致解析失败。反映社区对更宽泛 OpenAI 兼容生态的需求。

## Bug 与稳定性

按严重程度排列：

| 严重度 | Issue | 状态 | 说明 |
|--------|-------|------|------|
| 🔴 高 | [#6879 auto-compaction 不触发](https://github.com/earendil-works/pi/issues/6879) | OPEN | 上下文超限直至 API 拒绝，浪费 token 且中断会话，17 👍 高关注 |
| 🔴 高 | [#7911 流事件丢失 usage](https://github.com/earendil-works/pi/issues/7911) | CLOSED | 0.84.0 回归，已由 #7982 修复 |
| 🟡 中 | [#7966 `--thinking` CLI 参数无效](https://github.com/earendil-works/pi/issues/7966) | CLOSED | CLI 参数被忽略，仍沿用上次模式，已复现 |
| 🟡 中 | [#7783 `triggerTurn:false` 仍触发回合](https://github.com/earendil-works/pi/issues/7783) | CLOSED | 已由 #8022 修复 |
| 🟡 中 | [#8008 RemoteSession 共享连接重连失败](https://github.com/earendil-works/pi/issues/8008) | CLOSED | 多个 session 共享 PiClient 时，第一个重连会破坏第二个 |
| 🟡 中 | [#8048 Resume 消息忽略 PI_CODING_AGENT_DIR](https://github.com/earendil-works/pi/issues/8048) | CLOSED | 自定义目录下会话恢复提示缺少环境变量 |
| 🟡 中 | [#8018 DeepSeek max_tokens 被忽略](https://github.com/earendil-works/pi/issues/8018) | CLOSED | `max_completion_tokens` 不兼容 DeepSeek API，输出长度限制失效 |
| 🟢 低 | [#7761 VTE 终端剪贴板无效](https://github.com/earendil-works/pi/issues/7761) | OPEN | TUI 显示“Copied!”但系统剪贴板为空 |
| 🟢 低 | [#8009 settings.json 写丢末尾换行](https://github.com/earendil-works/pi/issues/8009) | CLOSED | 对版本控制用户不友好 |

## 功能请求与路线图信号

1. **本地模型支持需求旺盛**
   - [#8049 Ollama 本地模型代理](https://github.com/earendil-works/pi/pull/8049)（已合并）+ [#8039 /add-local-model 扩展](https://github.com/earendil-works/pi/pull/8039)（已合并）共同指向本地/私有化部署场景，未来可能成为 Pi 的重要使用方式。
   - [#6165 新增 Scaleway 提供商](https://github.com/earendil-works/pi/issues/6165)（欧盟托管开放权重模型），虽被标记 no-action，但反映欧盟用户对数据本地化的需求。

2. **TUI 可扩展性持续增强**
   - [#7683 组件级鼠标事件](https://github.com/earendil-works/pi/issues/7683)已获两个实现，扩展 widget 生态将受益。
   - [#7765 滚轮滚动步长配置](https://github.com/earendil-works/pi/issues/7765)（标记 no-action）被拒，但类似的可配置化需求可能会以其他形式回归。

3. **编辑工具兼容性优化**
   - [#7835 单对象 edits 参数](https://github.com/earendil-works/pi/issues/7835)+[#7836 空白归一化](https://github.com/earendil-works/pi/issues/7836)均由同一用户提交且已有对应 PR（#8011、#8012），表明项目对小模型生态兼容性持开放态度。

4. **扩展 API 深化**
   - [#8023 持久化消息发布 API](https://github.com/earendil-works/pi/issues/8023)、[#8035 控制消息显示钩子](https://github.com/earendil-works/pi/issues/8035)、[#8006 明确 agent_settled 生命周期](https://github.com/earendil-works/pi/issues/8006) 等请求，说明重度扩展用户开始要求更精细的生命周期控制和异步能力，是扩展体系走向成熟的信号。

5. **体验细节优化**
   - [#8015 行中斜杠命令](https://github.com/earendil-works/pi/issues/8015)：输入 `/` 时，行中位置也应弹出命令菜单，提升交互流畅度。

## 用户反馈摘要

- **Windows 用户处于观望状态**（[#7547](https://github.com/earendil-works/pi/issues/7547)）：大量 Windows 开发者想用 Pi，但运行方式碎片化、文档不清晰、Bug 较多，项目方正在收集反馈以确定优先级。
- **auto-compaction 是高频痛点**（[#6879](https://github.com/earendil-works/pi/issues/6879)）：用户运行 2 小时以上的 agentic 任务时，上下文管理不可靠造成实质经济损失（token 浪费）和会话中断。
- **编辑工具对模型不友好**（[#7835](https://github.com/earendil-works/pi/issues/7835)、[#7836](https://github.com/earendil-works/pi/issues/7836)）：小模型在参数格式和空白处理上更容易出错，用户积极报告并推动工具链改进。
- **TUI 扩展开发者活跃**：多个 PR 围绕 TUI 组件能力展开（鼠标事件、滚动指示器 [#7970](https://github.com/earendil-works/pi/pull/7970)、主题覆盖 [#7722](https://github.com/earendil-works/pi/pull/7722)），扩展开发者社区正在形成。
- **DeepSeek 用户的实际困扰**（[#8018](https://github.com/earendil-works/pi/issues/8018)）：输出长度限制被静默忽略，可能产生意外长回复，影响使用体验和成本控制。

## 待处理积压

- **[#6879 auto-compaction 触发机制](https://github.com/earendil-works/pi/issues/6879)**：自 7/20 创建至今近一个月，17 👍 高关注，至今无 fix PR。涉及核心上下文管理逻辑，建议尽快排期。
- **[#7547 Windows 支持调研](https://github.com/earendil-works/pi/issues/7547)**：社区讨论度高但尚处信息收集阶段，需在收集完毕后产出行动项。
- **[#5262 Anthropic Vertex provider PR](https://github.com/earendil-works/pi/pull/5262)**：自 5/31 创建，已开放 2.5 个月，仍待合并。企业用户对 Google Cloud Vertex AI 集成有明确需求。
- **[#6596 taskkill ENOENT 修复](https://github.com/earendil-works/pi/issues/6596)**：Node.js 24 环境下 Windows 进程树终止失败，7/13 提交修复方案，一个月无人跟进。
- **[#8000 文件自动补全排序问题](https://github.com/earendil-works/pi/issues/8000)**：新提交但影响交互效率，等待 triage。

---

*数据窗口：2026-08-12 UTC ~ 2026-08-13 UTC | 数据来源：GitHub API*

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-13

## 1. 今日速览

过去 24 小时 LiteLLM 项目保持高活跃度：共发生 73 条 Issue 更新（新开/活跃 54 条，关闭 19 条），270 条 PR 更新（待合并 158 条，已合并/关闭 112 条），无新版本发布。开发侧重点集中在成本映射修正（GPT-5.6 系列）、MCP 稳定性、代理配置可靠性以及 UI 表单重构。社区侧最受关注的是私有仓库 AI 技能认证支持（👍13）与 Azure GPT-5.6 定价错误问题，两者均获得 5+ 条讨论。整体项目健康度良好，但存在一批 3-6 个月前报告的 stale 旧 Issue 尚未解决（如 Redis 并发计数器泄漏、failover 不触发等），需关注积压清理。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日合并/关闭的 PR 中，有 4 项值得关注：

- **[#36676](https://github.com/BerriAI/litellm/pull/36676) feat(terraform/aws): make VPC, Aurora, and Redis optional**（已合并）— Terraform AWS 模块现支持复用已有 VPC、Postgres 和 Redis，不再强制创建新网络资源。这对锁定的企业账号部署是重要灵活性提升。
- **[#36691](https://github.com/BerriAI/litellm/pull/36691) fix(router): never price a strategy-router alias**（已合并）— 修复 `auto_router` 模型组被跳过预算检查、真实花费却记在路由目标上的内部报告问题，直接关联 #33168 中“策略路由模型从 /v1/models 消失但仍在计费”的隐患。
- **[#36700](https://github.com/BerriAI/litellm/pull/36700) fix(ollama): ensure streaming chunks share consistent id and tool_calls finish_reason**（已合并）— 修复 Ollama 流式响应中每个 chunk 拥有不同 `id` 及 tool_calls 缺少 `finish_reason` 的问题，使 Zed 等严格 OpenAI 客户端可正常使用工具调用。
- **[#36701](https://github.com/BerriAI/litellm/pull/36701) chore: temporary CI spike**（已关闭）— 临时 CI 验证 PR，非产品代码，无实质影响。

此外，基础设施可观测性方面有多个开放 PR 在推进：spend-logs 保留清理限流（[#36594](https://github.com/BerriAI/litellm/pull/36594)）、auxiliary DB 任务单主选举（[#36618](https://github.com/BerriAI/litellm/pull/36618)）等，表明项目正加强大规模部署下的运维稳健性。

---

## 4. 社区热点

| 条目 | 类型 | 评论/反应 | 链接 | 焦点 |
|---|---|---|---|---|
| [Support adding skills to private repos with authentication](https://github.com/BerriAI/litellm/issues/26071) | 功能请求 | 8 评论 / 👍13 | [Issue #26071](https://github.com/BerriAI/litellm/issues/26071) | 用户需要向私有仓库添加 Claude skills 等 AI 技能插件，要求支持 SSH 密钥和 GitHub token 认证。这是当日社区需求最强烈的信号，说明企业用户已开始在生产中依赖技能/插件机制 |
| [LiteLLM_Config table is overwriting newly deployed config](https://github.com/BerriAI/litellm/issues/12875) | Bug | 11 评论（已关闭） | [Issue #12875](https://github.com/BerriAI/litellm/issues/12875) | 数据库中的配置表覆盖新部署配置，导致 `general_settings` 不生效。虽已关闭但评论最多，说明用户对配置管理机制有较高敏感度 |
| [Azure GPT-5.6 terra/luna cost-map rows carry OpenAI's prices](https://github.com/BerriAI/litellm/issues/36192) | Bug | 5 评论 | [Issue #36192](https://github.com/BerriAI/litellm/issues/36192) | 成本映射将 OpenAI 的降价错误应用到 Azure 模型上，导致费用计算偏差。该 Issue 与 #36698、#36017 等 PR 密切相关，定价准确性问题持续引发社区关注 |
| [Usage AI Chat fails when selected LiteLLM model name is a proxy alias / model group](https://github.com/BerriAI/litellm/issues/24513) | Bug | 5 评论 | [Issue #24513](https://github.com/BerriAI/litellm/issues/24513) | Usage 面板的 Ask AI 功能无法处理模型组别名，影响用户对用量分析功能的信任 |

**热点诉求分析**：社区当前最关心三件事——（1）技能/插件系统的私仓认证与审批流（#26071 与 PR #36677 呼应）；（2）成本与定价准确性（#36192、#36637、#36697）；（3）模型别名/模型组在网关各功能中的一致性（#24513、#33168）。

---

## 5. Bug 与稳定性

按严重程度排列：

### 🔴 高严重度

- **Azure GPT-5.6 terra/luna 成本映射错误**（[#36192](https://github.com/BerriAI/litellm/issues/36192)）：Azure 模型沿用了 OpenAI 的降价价格，导致账单偏差。**已有相关修复 PR**（[#36698](https://github.com/BerriAI/litellm/pull/36698)、[#36017](https://github.com/BerriAI/litellm/pull/36017)）在推进，分别修正 Bedrock Mantle 1M 上下文与成本映射。
- **`max_parallel_requests` Redis 计数器泄漏**（[#27955](https://github.com/BerriAI/litellm/issues/27955)）：客户端中断流式 `/v1/messages` 请求后计数器单调递增，最终所有请求被拒。5 月报告至今未关闭，影响 Claude Code 用户。
- **master-key-only 模式认证失败返回 500 而非 401**（PR [#35480](https://github.com/BerriAI/litellm/pull/35480)）：无数据库部署下所有认证失败均返回 HTTP 500，**修复 PR 开放中**。

### 🟡 中严重度

- **无 Python 3.13 可用 wheel**（[#36526](https://github.com/BerriAI/litellm/issues/36526)，已关闭）：1.96.1 版本仅发布 cp310 wheel，3.13 环境安装失败。虽已关闭但用户升级路径需验证。
- **`_should_start_new_content_block` 在空 choices 块上崩溃**（[#36553](https://github.com/BerriAI/litellm/issues/36553)，已关闭）：OpenAI 格式后端发送 usage-only chunk 时流式迭代器崩溃。
- **litellm_content_filter 评估未显示在 Guardrails Monitor**（[#36566](https://github.com/BerriAI/litellm/issues/36566)）：已配置的全局 guardrails 不出现在日志与监控中。
- **Ollama 流式响应 id 不一致**（PR [#36700](https://github.com/BerriAI/litellm/pull/36700)）：该问题今日已通过合并 PR 修复，影响严格 OpenAI 客户端。

### 🟢 低严重度 / 存量问题

- **Anthropic 转换器总是设置 effort 为 xhigh**（[#27168](https://github.com/BerriAI/litellm/issues/27168)）：导致 Claude Code 请求 400，5 月报告至今开放。
- **`aembedding` 缺少 `num_retries` 导致 embedding 零重试**（[#27363](https://github.com/BerriAI/litellm/issues/27363)）：embedding 模型组无法 failover。
- **`add_user_information_to_llm_headers` 未转发到 /v1/files 与 /v1/batches**（[#27641](https://github.com/BerriAI/litellm/issues/27641)）。
- **Snowflake Cortex API Base URL 错误**（[#27187](https://github.com/BerriAI/litellm/issues/27187)，已关闭）。

---

## 6. 功能请求与路线图信号

今日开放 PR 透露了明确的路线图方向，结合 Issue 诉求可判断以下能力可能进入下一版本：

| 方向 | 相关 PR | 对应 Issue 信号 | 入选判断 |
|---|---|---|---|
| **技能（Skills）自助提交与审批流** | [#36677](https://github.com/BerriAI/litellm/pull/36677) feat(skills): self-service skill submission with admin review | [#26071](https://github.com/BerriAI/litellm/issues/26071)（私仓认证，👍13） | 高。PR 已实现非管理员提交、管理员审批流程；#26071 的私仓认证是下一步自然延伸 |
| **Parallel AI 全量接入** | [#36704](https://github.com/BerriAI/litellm/pull/36704) feat(parallel_ai): add chat + responses LLM provider | — | 中高。这是新 provider 接入，扩大生态覆盖 |
| **MCP 稳定性与可配置性** | [#36599](https://github.com/BerriAI/litellm/pull/36599) oauth discovery 不阻断启动；[#33444](https://github.com/BerriAI/litellm/pull/33444) mcp_tool_search 默认 top_k | [#27635](https://github.com/BerriAI/litellm/issues/27635)（MCP OAuth2 注册崩溃） | 高。MCP 是当前企业采用重点，运维稳定性被反复提及 |
| **预算/成本控制精细化** | [#36699](https://github.com/BerriAI/litellm/pull/36699) 显式 null budget_duration；[

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*