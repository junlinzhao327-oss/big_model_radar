# OpenClaw 生态日报 2026-09-17

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-16 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-09-17

---

## 1. 今日速览

OpenClaw 今日维持**高活跃度但高压力**状态：过去 24 小时 Issues 更新 500 条（新开/活跃 322、关闭 178），PR 更新 500 条（待合并 291、已合并/关闭 209），无新版本发布。问题侧呈现明显的**稳定性事故集中期**特征——内存泄漏、僵尸进程、事件循环饥饿、更新失败四类系统性故障同时占据 P0/P1 榜单，其中 2026.9.3 → 2026.9.4 的升级链路暴露出多个阻断性缺陷。维护者 `@steipete` 今日提交/推动约 15 个 PR，主攻 Gateway 异步化、device token 存储重构、插件生命周期释放与 CI 稳定性，项目在"止血与重构"双线推进。社区情绪偏紧张，用户对资源耗尽和升级失败的抱怨集中在高评论 Issue 中。

---

## 2. 版本发布

今日无新版本发布。当前生产环境主流版本为 2026.9.3 / 2026.9.4，围绕这两个版本的升级可靠性问题已形成独立追踪 Issue（[#145252](https://github.com/openclaw/openclaw/issues/145252)），建议维护者在下一版本前优先收敛升级路径。

---

## 3. 项目进展

今日合并/关闭方向以**基础设施加固与目录清理**为主，未见大型功能落地。值得关注的推进：

| PR | 方向 | 价值 |
|---|---|---|
| [#150223](https://github.com/openclaw/openclaw/pull/150223) | `fix(models): keep large fleets responsive during model preparation` (P1) | 直接对应 [#149538](https://github.com/openclaw/openclaw/issues/149538) 632-agent 编队事件循环饥饿，把 `buildSnapshotBatch` 移出主线程微任务队列 |
| [#150153](https://github.com/openclaw/openclaw/pull/150153) | 跨共享 Gateway 更新保持任务恢复 (P1) | 修复 sibling Gateway 使用已移除模块 chunk 导致任务中断 |
| [#149971](https://github.com/openclaw/openclaw/pull/149971) | 阻止会话列表读取阻塞 Gateway | 冷缓存扫描完整 session 清单导致的请求延迟 |
| [#150349](https://github.com/openclaw/openclaw/pull/150349) / [#150346](https://github.com/openclaw/openclaw/pull/150346) | device token 存储 await/fence + SQL 内核抽取 | 为后续 worker 迁移铺路，属依赖步骤，无用户可见变更 |
| [#150274](https://github.com/openclaw/openclaw/pull/150274) | reload 后释放已退役插件状态 | 修复插件 reload 后状态滞留与临时分配过多 |
| [#150344](https://github.com/openclaw/openclaw/pull/150344) | node-host 原生 session/policy 所有权 | 复用 Swift/Rust Gateway 客户端的架构 seam |

**整体推进度评估**：今日无版本发布，合并内容偏向"承重墙维护"——异步化、生命周期释放、CI 假失败治理。项目在架构层面朝"事件循环不阻塞、进程状态可回收"方向前进了一步，但用户侧可感知的功能演进有限。

---

## 4. 社区热点

按评论数与反应排列，今日最受关注的条目集中在**资源泄漏与并发正确性**：

1. **[#97616](https://github.com/openclaw/openclaw/issues/97616) — 僵尸进程累积（30 评论，👍1，OPEN，P1）**
   hook/tool 子进程未回收，`openclaw-hooks`、`bash`、`codex` 在主进程下堆积为 zombie，长期导致运行时退化。这是今日讨论量最高的 Issue，社区对"长期运行稳定性"高度敏感。

2. **[#91588](https://github.com/openclaw/openclaw/issues/91588) — Gateway 内存泄漏（25 评论，👍1，OPEN，P1）**
   RSS 从 350MB 涨至 15.5GB，2–3 天触发 OOM，引发 `launchd-handoff` 反复重启。已挂 `clawsweeper:no-new-fix-pr` 与 `needs-maintainer-review`，说明尚未有可合并修复。

3. **[#144911](https://github.com/openclaw/openclaw/issues/144911) — MCP 初始化超时拖垮 Gateway（21 评论，OPEN，P1，💎 diamond lobster）**
   stdio MCP 服务器 30s 超时触发子进程清理路径的 **unhandled rejection**，直接打崩整个 Gateway。带 `clawsweeper:queueable-fix` 标签，修复路径已明确。

4. **[#119720](https://github.com/openclaw/openclaw/issues/119720) — 同步持久化阻塞事件循环（20 评论，OPEN，P1，💎）**
   已有部分修复落地（#140231、#138984），但仍需产品决策，属"半修复"状态。

5. **[#111897](https://github.com/openclaw/openclaw/issues/111897) — 同 session lane 并发投递重复回复（19 评论，👍1，OPEN，P1）**
   与 #54488（lane starvation）相关但不同：这里是**并发**而非**延迟**派发。

6. **[#150201](https://github.com/openclaw/openclaw/issues/150201) — Windows 更新候选快照失败（14 评论，P0，💎，OPEN）**
   今日新开，Windows 平台 2026.9.3 升级到候选版本时 Gateway SQLite 检查超时。

**背后诉求**：这些讨论共同指向一个主题——**OpenClaw 在长时运行、大编队、多进程钩子场景下的资源生命周期管理不足**。用户不是在做功能请求，而是在报告"跑着跑着就崩"的生产级可靠性缺口。

---

## 5. Bug 与稳定性

### 🔴 P0 / 阻断级

| Issue | 问题 | Fix PR 状态 |
|---|---|---|
| [#150201](https://github.com/openclaw/openclaw/issues/150201) | Windows 更新候选快照失败；Gateway SQLite 检查超时（2026.9.3） | 有 `queueable-fix`，未见 PR |
| [#149538](https://github.com/openclaw/openclaw/issues/149538) | main (1611ca6d) Gateway ready 但不服务，/health 全部超时，632-agent 编队事件循环饥饿 | ✅ 关联 [#150223](https://github.com/openclaw/openclaw/pull/150223) |
| [#146394](https://github.com/openclaw/openclaw/issues/146394) | global-install-failed（2026.9.3，linux/arm64） | 无 |
| [#144739](https://github.com/openclaw/openclaw/issues/144739) | 2026.9.3 → 2026.9.4 npm 升级时对 schema-17 候选状态跑旧版本 | 无 |
| [#148681](https://github.com/openclaw/openclaw/issues/148681) | finalize:doctor 升级失败（2026.9.4） | 无 |
| [#70903](https://github.com/openclaw/openclaw/issues/70903) | 持久化 provider 冷却在计费恢复后仍封禁用户数小时 | 无 |
| [#145929](https://github.com/openclaw/openclaw/issues/145929) | ✅ 已关闭 — auth profile 写入永久 lock-may-be-busy | 已解决 |
| [#111578](https://github.com/openclaw/openclaw/issues/111578) | ✅ 已关闭 — Gateway auth token 从 service-env 丢失（复发） | 已解决 |

### 🟠 P1 严重

- [#97616](https://github.com/openclaw/openclaw/issues/97616) 僵尸进程累积（30 评论）— 无 fix PR
- [#91588](https://github.com/openclaw/openclaw/issues/91588) Gateway 内存泄漏 15.5GB（25 评论）— 无 fix PR
- [#144911](https://github.com/openclaw/openclaw/issues/144911) MCP 超时未处理拒绝崩溃（21 评论）— ✅ `queueable-fix`
- [#119720](https://github.com/openclaw/openclaw/issues/119720) 同步持久化阻塞事件循环（20 评论）— 部分修复
- [#111897](https://github.com/openclaw/openclaw/issues/111897) 并发运行重复回复（19 评论）— 无
- [#137332](https://github.com/openclaw/openclaw/issues/137332) 混合 requester-settle 批次无限重试（12 评论）— ✅ `queueable-fix`
- [#136311](https://github.com/openclaw/openclaw/issues/136311) reindex 锁不可释放 + 19GB 孤儿临时 DB（11 评论）— 无
- [#146265](https://github.com/openclaw/openclaw/issues/146265) 重启后 AsyncWorkScope 保持关闭（8 评论）— 无
- [#148707](https://github.com/openclaw/openclaw/issues/148707) 回复丢失 "no active tool authority snapshot"（7 评论）— 无
- [#134925](https://github.com/openclaw/openclaw/issues/134925) ARM64/Pi 每回合主线程 100% CPU（7 评论）— 无
- [#108395](https://github.com/openclaw/openclaw/issues/108395) 助手伪造 "Human:" 消息自我授权（6 评论）— 安全相关，无
- [#121187](https://github.com/openclaw/openclaw/issues/121187) NO_REPLY 被当作缺失输出重试（6 评论）— 有 `linked-pr-open`

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报
**日期：2026-09-17** ｜ 数据窗口：过去 24 小时 ｜ 数据源：[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)

---

## 1. 今日速览

- **问题吞吐量维持高位**：24 小时内 Issues 更新 500 条（新开/活跃 310，已关闭 190），关闭率约 38%，分诊与修复闭环基本跟得上流入速度。
- **PR 侧出现明显积压**：500 条 PR 更新中待合并 431 条，已合并/关闭仅 69 条，合并率约 **13.8%**，review 带宽已成为当前最突出的工程瓶颈。
- **今日无版本发布**，主分支以大量小型修复 PR + 一项大型架构 PR 并行推进的方式演进。
- **社区情绪焦点集中在"可靠性"**：安装/更新链路（Debian 安装、`hermes update`）、计费一致性和 cron/网关生命周期是讨论最密集的三个方向。
- 单个争议度最高的缺陷是 [#103483](https://github.com/NousResearch/hermes-agent/issues/103483)（muse-spark 流式回答中途截断），获得 11 个 👍，且今日仍无关联修复 PR。

---

## 2. 版本发布

今日无新版本发布，Releases 列表为空。项目当前版本线停留在 v0.21.3 / 2026.9.14（由已关闭的 [#111942](https://github.com/NousResearch/hermes-agent/issues/111942) 报告内容佐证）。

**风险提示**：由于 v0.21.3 存在启动即崩溃的 P0 回归（见下节），且尚未通过新版本渠道修复，使用稳定发行版的用户仍暴露在该缺陷中，建议尽快切出补丁版本。

---

## 3. 项目进展

> 说明：今日已合并/关闭的 69 条 PR 未在数据集中给出明细，以下以**已关闭 Issue** 与**在途 PR 的修复对象**作为落地证据。

**已确认闭环的重要缺陷（已关闭）**

| Issue | 内容 | 严重度 |
|---|---|---|
| [#111942](https://github.com/NousResearch/hermes-agent/issues/111942) | CLI 启动崩溃 `NameError: file_signature`，系 #111408 引入的回归 | **P0** |
| [#87093](https://github.com/NousResearch/hermes-agent/issues/87093) | Debian 13.6 标准安装失败，`uv.lock` 与 npm install 双双报错 | **P0** |
| [#110912](https://github.com/NousResearch/hermes-agent/issues/110912) | Nous Portal 在订阅额度耗尽后按 full/list 价计费 | **P1** |
| [#105104](https://github.com/NousResearch/hermes-agent/issues/105104) | 桌面 Bot Mode 侧边栏点击无响应 | P1 |
| [#93618](https://github.com/NousResearch/hermes-agent/issues/93618) | 聊天记录消失、Bot 会话不刷新 | P2 |
| [#96570](https://github.com/NousResearch/hermes-agent/issues/96570) | 群聊每次重建 system prompt，前缀缓存永久 miss | P3 |

**在途修复已就绪、等待合并**

- [#113459](https://github.com/NousResearch/hermes-agent/pull/113459) / [#113458](https://github.com/NousResearch/hermes-agent/pull/113458)：堵住 `execute_code` 直接改写 `config.yaml` 的审批绕过路径（关闭 #113421）。
- [#113544](https://github.com/NousResearch/hermes-agent/pull/113544)：网关关闭时持久化被中断的 run 记录（关闭 #113541）。
- [#112833](https://github.com/NousResearch/hermes-agent/pull/112833)：对"仅推理内容被提升为最终回答"加能力门控（关闭 #111761）。
- [#113542](https://github.com/NousResearch/hermes-agent/pull/113542)：按 provider 上限驱逐图片以保住 prompt-cache 前缀（**P0**，直击用量成本）。

**整体推进评估**：项目在**缺陷修复层面推进扎实**（多个 P0/P1 收敛），但在**新能力合入层面明显减速**——431:69 的待合并/已合并比例意味着大量已完成的工作停留在 review 队列，架构类 PR [#106742](https://github.com/NousResearch/hermes-agent/pull/106742) 已开放 8 天仍未落地。健康度评级：**修复健康，交付受阻**。

---

## 4. 社区热点

**#1 [#88584](https://github.com/NousResearch/hermes-agent/issues/88584) — 108 条评论（今日最高）**
`scheduled Nous-to-Enterkey merge` 因 `cron/jobs.py` 冲突而阻塞，dashboard updater 停留在上一个已验证的 Enterkey 版本。标签为 `invalid, comp/cron, P3`，但讨论热度与标签严重不匹配。
→ **诉求**：自动化同步管道的冲突需要可观测的告警与人工兜底，而不是静默卡死一个月（创建于 8-17，今日仍在更新）。

**#2 [#87093](https://github.com/NousResearch/hermes-agent/issues/87093) — 28 条评论 / 4 👍（已关闭）**
Debian 13.6 全新安装走 `curl | bash` 标准路径直接失败。
→ 官方安装脚本在主流发行版上的首装体验是信任入口，任何失败都会被放大讨论。

**#3 [#110912](https://github.com/NousResearch/hermes-agent/issues/110912) — 20 条评论（已关闭）**
订阅额度到期后部分模型路由（glm/glm-flash/kimi）按原价计费，被怀疑是折扣路由 bug 而非额度耗尽。
→ **诉求**：计费透明与可解释性。涉及真实金钱，用户容忍度极低。

**#4 [#103483](https://github.com/NousResearch/hermes-agent/issues/103483) — 16 条评论 / 11 👍（反应最高）**
muse-spark 在 `finish_reason=stop` 时以一段无关的短文本提前结束整轮任务。
→ 这是数据集中**共鸣最强的缺陷**，且至今无关联修复 PR，建议优先排期。

**#5 [#107402](https://github.com/NousResearch/hermes-agent/issues/107402) — 19 条评论**
`hermes update` 在延迟重启网关时留下永久 "did not restart running gateways" 警告，状态卡在 `partial`。
→ 与 #86207（更新后 dashboard 仍跑旧代码）共同指向同一根因：**更新流程缺少单一事实来源**，正是 [#88683](https://github.com/NousResearch/hermes-agent/issues/88683) 架构提案要解决的问题。

**PR 侧热点**：评论最集中的 PR 均由维护者 @teknium1 提交，聚焦 Bot Mode / 群聊体验（[#113384](https://github.com/NousResearch/hermes-agent/pull/113384)、[#113382](https://github.com/NousResearch/hermes-agent/pull/113382)、[#113420](https://github.com/NousResearch/hermes-agent/pull/113420)）与架构级 [#106742](https://github.com/NousResearch/hermes-agent/pull/106742)。

---

## 5. Bug 与稳定性

### P0 — 阻断级

| Issue / PR | 状态 | 说明 | Fix PR |
|---|---|---|---|
| [#111942](https://github.com/NousResearch/hermes-agent/issues/111942) | ✅ CLOSED | v0.21.3 交互式 CLI

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 · 2026-09-17

> 数据来源：github.com/earendil-works/pi
> 统计窗口：过去 24 小时

---

## 1. 今日速览

Pi 项目今日延续高强度迭代状态：24 小时内 Issues 更新 63 条（关闭 45 条、新开/活跃 18 条），关闭率高达 71%，PR 更新 20 条（合并/关闭 9 条、待合并 11 条），整体呈现"高吞吐清理 + 新功能并行推进"的健康态势。核心维护者 @mitsuhiko 亲自关闭了跨会话系统消息（#9548）并新开 prompt 缓存预热实验性 PR（#9668），显示项目正在为下一阶段性能优化铺路。Bug 侧仍有一批高优先级问题悬而未决，主要集中在会话生命周期（#5886）、并行启动鉴权（#8928）与 TUI 大上下文性能（#9410）三个方向。今日无新版本发布，代码改动主要通过 PR 累积。

---

## 2. 版本发布

今日无新版本发布，跳过。

---

## 3. 项目进展

今日共 9 个 PR 被合并/关闭，覆盖剪贴板、压缩队列一致性、bash 钩子安全语义、TUI 兼容性等多个模块，项目稳定性向前推进明显。

| PR | 说明 | 影响 |
|---|---|---|
| [#9548](https://github.com/earendil-works/pi/pull/9548) | **Mid conversation system messages**（@mitsuhiko） | ⭐ 架构级变更：系统提示与工具变更成为 transcript 的一部分，支持记录指令变更历史、恢复分支状态、保持缓存前缀，是后续 prompt cache 优化的基础 |
| [#9677](https://github.com/earendil-works/pi/pull/9677) | 修复压缩队列回滚会重放已接受消息 | 消除 compaction 场景下的消息重复/状态错乱风险 |
| [#9662](https://github.com/earendil-works/pi/pull/9662) | user_bash 钩子异常时 fail closed | **行为变更**：钩子抛错不再静默回退本地 shell，需注意迁移；已附 breaking change 文档 |
| [#9601](https://github.com/earendil-works/pi/pull/9601) | 精确 session ID 查找替代全量 transcript 扫描 | 修复 #9440，4K+ transcript 场景启动从 ~16s 降至接近瞬时 |
| [#9682](https://github.com/earendil-works/pi/pull/9682) | 修复 macOS pbcopy 回退时非 ASCII 文本损坏 | 修复 #9684，UTF-8 不再被按 MacRoman 编码 |
| [#9655](https://github.com/earendil-works/pi/pull/9655) | Windows ConPTY 下 raw mode 后再启用鼠标追踪 | 修复 Windows 鼠标事件丢失 |
| [#9663](https://github.com/earendil-works/pi/pull/9663) | SDK 示例替换已废弃的 `getModel` | 文档/示例现代化，降低新用户接入门槛 |
| [#9648](https://github.com/earendil-works/pi/pull/9648) / [#9646](https://github.com/earendil-works/pi/pull/9646) | Baseten provider session affinity 头 | 修复 Baseten 提供商的会话粘性 |

**整体评估**：今日进展约等于"一次中型版本"的内容量——一个架构级 PR + 六个 Bug 修复 + 一个 API 清理。值得关注的是 #9548 与 #9668 的组合，暗示下一版本可能围绕 **prompt caching / 会话状态持久化** 形成主题性发布。

---

## 4. 社区热点

按评论数与 👍 排序，今日讨论最集中的议题如下：

### 🔥 #5886 — AgentSession settlement/continuation 生命周期元问题
- 评论 12 · 👍 4 · 作者 @mitsuhiko · 始于 2026-06-18
- https://github.com/earendil-works/pi/issues/5886
- 由维护者本人创建的"元 issue"，汇总了"后置运行逻辑试图从已被裁剪的 transcript 继续 agent"这一类反复出现的 Bug。讨论长达三个月，说明这是一个系统性架构缺陷，而非孤立缺陷。**诉求**：需要一次性的架构收口，而不是逐个打补丁。

### 🔥 #8928 — 并行启动时因其他 provider 的过期 OAuth 凭证报"无 API key"，持续约 48s
- 评论 9 · 作者 @deandevz · [inprogress]
- https://github.com/earendil-works/pi/issues/8928
- 用户提供了确定性复现与计时数据，并给出生产环境 3 小时的排查记录。**诉求**：错误信息指向活跃 provider 的凭证，具有强误导性，多进程场景下几乎必然触发。已被标记 inprogress，预计近期有修复 PR。

### 🔥 #5323 — 改进 Vertex + GCP metadata server 支持
- 评论 9 · 👍 2 · 始于 2026-06-02
- https://github.com/earendil-works/pi/issues/5323
- 指出现有 `is Vertex authed?` 检查是同步 `existsSync`，无法覆盖 GCP metadata server 场景。**诉求**：企业级 GCP 部署（Workload Identity / GKE）用户被排除在外。

### 🔥 #8791 — 向扩展暴露 ModelRuntime
- 评论 4 · 👍 5（今日最高赞）
- https://github.com/earendil-works/pi/issues/8791
- 扩展开发者希望在 `ExtensionContext` 上以只读属性方式拿到 `ModelRuntime`，用于创建隔离的进程内 agent session。**诉求**：扩展生态的能力边界需要进一步开放。

### 其他高关注
- [#9165](https://github.com/earendil-works/pi/issues/9165)（已关闭，8 评论）Claude Opus 5 via OpenRouter 拒绝 per-message output_config
- [#9294](https://github.com/earendil-works/pi/issues/9294)（已关闭，7 评论）claude-fable-5 内置 fallback 模型已失效导致 400

---

## 5. Bug 与稳定性

按严重程度排列（🔴 高 / 🟠 中 / 🟡 低）：

### 🔴 高严重度

| Issue | 问题 | Fix PR |
|---|---|---|
| [#8928](https://github.com/earendil-works/pi/issues/8928) | 并行启动时误报"No API key found"，错误指向错误 provider，持续 ~48s | 无（标记 inprogress） |
| [#9410](https://github.com/earendil-works/pi/issues/9410) | 大上下文（~465k tokens）下按 Escape 中断流式输出导致 TUI 冻结 ~58s | 无 |
| [#9602](https://github.com/earendil-works/pi/issues/9602) | Compaction 将此前请求中已省略的 thinking 消息重新纳入，导致溢出 | 无（与 #9652 同源问题，后者已修） |
| [#9571](https://github.com/earendil-works/pi/issues/9571) | 畸形 `Retry-After` HTTP-date 导致 `Date.parse` 返回 NaN，退避为 0，形成紧密重试循环 | 无，`provider-retry.ts:61` 定位明确 |

### 🟠 中严重度

| Issue | 问题 | Fix PR |
|---|---|---|
| [#9216](https://github.com/earendil-works/pi/issues/9216) | Ollama qwen3.8:27b 流式 `terminated` 错误（0.84.x→0.85.x 回归），且自动压缩首轮后不再触发 | 无 |
| [#9129](https://github.com/earendil-works/pi/issues/9129) | Windows 上 bash 超时 kill 遗留管道孤儿进程（MSYS2 中间进程未清理） | 无 |
| [#9255](https://github.com/earendil-works/pi/issues/9255) | `TuiMainScreen.doRender()` 几乎每帧走 fullRender，长 transcript 剧烈跳动/文字重影 | 无 |
| [#9099](https://github.com/earendil-works/pi/issues/9099) | pi.dev provider registry 对非 batch Anthropic 模型返回缺少 `/v1` 的 baseUrl，agent 收到 HTML 404 | 无（inprogress） |

### 🟡 低严重度 / 已修复

- [#9654](https://github.com/earendil-works/pi/issues/9654) `read` 工具无视 offset/limit 先全量读入内存 → 已关闭
- [#9684](https://github.com/earendil-works/pi/issues/9684) macOS pbcopy 回退损坏非 ASCII 文本 → 已由 [#9682](https://github.com/earendil-works/pi/pull/9682) 修复
- [#9680](https://github.com/earendil-works/pi/issues/9680) 能力探测错误禁用 usage-in-streaming，token 全记为 0 → 已关闭
- [#9676](https://github.com/earendil-works/pi/issues/9676) Vercel AI Gateway 无签名 thinking 被丢弃 → 已关闭
- [#9664](https://github.com/earendil-works/pi/issues/9664) openai-responses 在转译网关下第二轮 400 → 已关闭
- [#9652](https://github.com/earendil-works/pi/issues/9652) Claude Fable 拒绝含 thinking block 的压缩请求 → 已关闭
- [#9585](https://github.com/earendil-works/pi/issues/9585) "fail to touch upstream" 未被识别为可重试 → 已关闭

**稳定性小结**：今日关闭的 Bug 数量（>15）远超新增，净稳定性为正。但仍有 4 个高严重度问题无 fix PR 关联，建议优先处理 #9571（修复成本低、影响面广）与 #9602（与刚关闭的 #9652 同源，可能有现成思路）。

---

## 6. 功能请求与路线图信号

结合今日 Issue 与在途 PR，以下需求最可能进入下一版本：

### 已有对应 PR，落地概率高 ✅

| 需求 | Issue | PR | 状态 |
|---|---|---|---|
| 扩展可向系统提示追加内容 | [#9432] | [#9434

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目日报 · 2026-09-17

> 数据窗口：2026-09-16 至 2026-09-17 · 数据来源：[github.com/BerriAI/litellm](https://github.com/BerriAI/litellm)

---

## 一、今日速览

- **活跃度极高，工程吞吐处于峰值区间**：24 小时内 Issue 更新 94 条（新开/活跃 74、关闭 20，关闭率约 21%），PR 更新 361 条（待合并 205、已合并/关闭 156，合并/关闭率约 43%）。
- **发布进入双通道并行**：`v1.103.0-dev.1`（开发主线）与 `v1.102.0-rc.2`（候选版）同时推进，v1.102.0 正式版临近。
- **今日议题主线高度收敛于"钱与配额"**：零成本模型绕过预算、团队按模型限流重复计数、并发首次请求绕过默认预算，构成一组同源的计费/鉴权正确性问题。
- **跨协议桥接的流式计费一致性**是第二大焦点：Anthropic `/v1/messages` ↔ OpenAI Chat Completions 桥接下的 usage / 缓存 Token 丢失问题集中爆发。
- **稳定性出现明确回归**：`hosted_vllm` 自 1.100.0 起丢失 `reasoning_content`，同日已有多个针对性修复 PR 提交，维护者响应链路健康。

---

## 二、版本发布

今日发布 2 个预发布版本，正式版尚未落地。

### 1. [v1.103.0-dev.1](https://github.com/BerriAI/litellm/releases)（开发版）

- **性质**：主线开发快照，用于提前验证 1.103 系列变更。
- **发布说明内容**：本次 release notes 主体为 **Docker 镜像签名验证指引**——所有 LiteLLM Docker 镜像均通过 [cosign](https://docs.sigstore.dev/cosign/overview/) 签名，签名密钥沿用 commit [`0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0) 引入的同一把密钥。
- **破坏性变更**：所提供数据中未披露具体变更条目，建议以完整 CHANGELOG 为准。
- **迁移建议**：生产环境**不建议**跟进 dev 通道；如需验证，请在隔离环境部署。

### 2. [v1.102.0-rc.2](https://github.com/BerriAI/litellm/releases)（候选版）

- **性质**：1.102.0 正式版前的第二个候选版本，说明 rc.1 阶段已发现并修复了若干问题。
- **发布说明内容**：与 dev 版一致，主体为 cosign 镜像签名验证指引，未列出具体功能/修复条目。
- **迁移注意事项**：
  1. 升级前请先校验镜像签名（`cosign verify`），确保供应链完整性；
  2. rc 版本已接近冻结，是预生产环境验证 1.102 行为的**最佳窗口期**；
  3. 关注本日报第五节所列计费类缺陷是否在 rc.2 中已包含修复。

> ⚠️ **说明**：两次 release 的公开说明仅包含签名验证段落，具体变更内容未在本次数据中提供，实际升级决策请以仓库 CHANGELOG / commit diff 为准。

---

## 三、项目进展

今日 PR 流转量为 361 条，其中 **156 条已合并/关闭**，205 条待合并。以下为已关闭/合并通道中代表性条目，以及今日高价值待合并变更。

### ✅ 已合并/关闭的重要 PR

| PR | 标题 | 推进内容 |
|---|---|---|
| [#37075](https://github.com/BerriAI/litellm/pull/37075) | `fix(vertex-live)`: bill Gemini Live sessions end to end | 修复 Gemini Live 全链路计费：使用别名声明的 Live 会话此前被记为 `unknown` 且**完全不计费**；同时修复 grounded Live 请求未携带 Google 按查询计费、Responses usage bridge 中计数器中断、`turn_detection: null` 无 traceback 静默杀会话等问题。属**计费准确性**关键修复 |
| [#40843](https://github.com/BerriAI/litellm/pull/40843) | `fix(proxy)`: release completed max-parallel slots promptly | 修复已完成请求在日志延迟期间仍占用并发槽位，导致紧随其后的请求被错误返回 429 的问题；在 awaited post-call 路径中及时释放槽位并对清理路径串行化。直接影响**并发限流可用性** |

### 🚧 高价值待合并 PR（今日提交/更新）

- **[#41495](https://github.com/BerriAI/litellm/pull/41495)** `fix(utils)`：在"流式转非流式"的转换路径上补跑 post-call deployment hook——此前 Response tagging、enrichment 与 `CustomGuardrail` 的 post_call 校验会**静默不执行**。属隐蔽的钩子缺失类缺陷。
- **[#41497](https://github.com/BerriAI/litellm/pull/41497)** `fix(streaming)`：中断的 Anthropic 流在仅有 reasoning 内容时按 `message_start` 占位符计费；新模型占位符为 8 而非 1，导致原有 `== 1` 重置逻辑失效，且回退逻辑只统计文本 Token。**直接影响账单准确性**。
- **[#40842](https://github.com/BerriAI/litellm/pull/40842)** `fix(proxy)`：对 guardrail 动态添加的 tag 补做预算校验——此前 tag 预算在 auth 阶段检查、guardrail 之后不再复查，可**无限超支**。
- **[#41485](https://github.com/BerriAI/litellm/pull/41485)** `feat(proxy)`：在网关 `/token` 端点支持 **RFC 8693 Token Exchange**，让仅有 IdP JWT 的客户端（如 Claude Code）无需浏览器往返即可换取网关密钥。这是通向企业 SSO 无密码化的重要一步。
- **[#41364](https://github.com/BerriAI/litellm/pull/41364)** `fix(mcp)`：上游凭证缺失时 **fail-closed**——不完整的 OBO 配置此前可绕过 token 交换，属安全加固。
- **[#41500](https://github.com/BerriAI/litellm/pull/41500)** `feat(rust)`：新增独立 framing crate，提供可复用的 AWS EventStream 与 SSE 分帧原语。**架构信号**：Rust 内核（`litellm-rust`）持续解耦。
- **[#41250](https://github.com/BerriAI/litellm/pull/41250)** `refactor(ocr)`：将 OCR provider 转换逻辑按 `litellm-rust/crates/core/src/llms/<provider>/ocr/*` 结构重组，与 [#41500](https://github.com/BerriAI/litellm/pull/41500) 共同指向 **Python → Rust 核心迁移**的持续推进。
- **[#41402](https://github.com/BerriAI/litellm/pull/41402)** `feat(e2e)`：使 provider 响应缓存在多次构建间可复用，并让 Bedrock 走缓存——此前共享缓存仅复用约 5% 的路由调用，每次构建都要重复付费，且 Bedrock 503 是上周 flaky 主因。**CI 成本与稳定性双优化**。
- **[#40934](https://github.com/BerriAI/litellm/pull/40934)** `fix(logging)`：每条日志记录此前被 secret 正则扫描两次；debug 级别下 8MB 的 `/v1/ocr` 日志行在 0.5 CPU 上阻塞事件循环约 11 秒，已超 uvicorn 5 秒 worker 超时阈值。**这是导致 worker 被误杀的潜在根因**。
- **[#41498](https://github.com/BerriAI/litellm/pull/41498)** `fix(otel)`：OpenInference 每消息属性此前硬编码上限 8 条，8 轮对话即丢失 `llm.input_messages.1.*`，且忽略 `OTEL_SPAN_ATTRIBUTE_COUNT_LIMIT`。
- **[#41094](https://github.com/BerriAI/litellm/pull/41094)**

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目日报
**日期：2026-09-17** ｜ 数据源：github.com/temporalio/temporal

---

## 1. 今日速览

Temporal 今日维持**高强度的代码交付节奏**：24 小时内 50 条 PR 发生更新，其中 14 条合并/关闭，PR 吞吐量处于本阶段高位。代码侧主线集中在 **CHASM 状态机框架、Nexus 事件重放、命名空间复制迁移、Standalone Activity API 一致性**四条线上，其中命名空间复制 PR0–PR2（#12112/#12113/#12115）当日提交当日关闭，节奏极快。**Issue 侧则出现"零关闭"信号**：6 条全部为新开或活跃状态，无一条被关闭，且新问题质量很高（涉及静默配置失败、持久化重试风暴、PostgreSQL 全表扫描）。整体判断：**开发推进健康，但运维/稳定性类反馈的消化速度落后于流入速度**，建议关注 triage 积压。

| 指标 | 数值 | 评估 |
|---|---|---|
| Issues 更新/关闭 | 6 / 0 | ⚠️ 流入 > 消化 |
| PR 更新/关闭 | 50 / 14 | ✅ 高吞吐 |
| 新版本发布 | 0 | 常规 |

---

## 2. 项目进展（今日合并/关闭的重要 PR）

今日顶层 20 条 PR 中有 7 条已关闭（另有 7 条关闭 PR 未进入展示列表），推进方向如下：

**① 命名空间复制向 CHASM 迁移正式启动（最重要）**
- [#12112](https://github.com/temporalio/temporal/pull/12112) `namespace replication: extract shared replication helpers (PR0)` — 抽出 `common/namespace/nsreplication` 复制门控与 detail→task-attributes 转换，供 legacy / CHASM 双路径复用。
- [#12113](https://github.com/temporalio/temporal/pull/12113) `add inert CHASM library (PR1)` — 引入惰性 CHASM 组件、状态机、服务 API 与 protobuf，建模 source commit 的 CAS 排序与 receiver 侧 apply-if-higher 语义。
- [#12115](https://github.com/temporalio/temporal/pull/12115) `wire shadow CHASM transport (PR2)` — 新增 `legacy` / `shadow` / `chasm` 三态全局动态配置，**默认 `legacy`**，shadow 模式下通过分层 history client 路由前端写请求。
> 这是一个 7 连 PR 栈的前 3 环，且**采用影子模式灰度 + 默认走老路径**，属于典型的低风险渐进式迁移设计。项目已从"设计"进入"可运行影子链路"阶段。

**② CHASM 组件能力补齐**
- [#12096](https://github.com/temporalio/temporal/pull/12096) `Return a sentinel error for CHASM component lookup misses` — 统一组件查找未命中的错误语义。
- [#11985](https://github.com/temporalio/temporal/pull/11985) `[oss-foundations] Add AdminDescribeMutableState to pod-level rate limiting` — 行为中性重构，将限流器构造与路由表组装解耦，并把 `DescribeMutableState` 纳入新的 pod 级优先级表，避免管理类调用挤占命名空间级配额。

**③ 运维工具与云分支维护**
- [#10376](https://github.com/temporalio/temporal/pull/10376) `Add tdbg schedule audit command` — 历时 **115 天**后关闭，为 `tdbg schedule` 增加定时任务审计（对比规划触发时间 vs 实际执行），解决了"schedule 没触发却查不出原因"的排障盲区。
- [#12111](https://github.com/temporalio/temporal/pull/12111) `Cloud/v1.32.0-163: Log context for version delete propagation failures` — 云分支 backport，补上版本删除传播失败的 task-queue/revision 上下文日志。

**净推进量评估：** 今日真正的"能力增量"来自命名空间复制 CHASM 栈（框架级迁移）+ 限流治理；其余多为韧性修补与可观测性补强。项目主线清晰，未见方向性摇摆。

---

## 3. 社区热点

⚠️ 数据说明：本次数据中 PR 的评论数字段为 `undefined`，无法按评论量排序，以下按**议题影响面与讨论实质**挑选。

**🔥 #11547 — 一次瞬时 `Unavailable` 抖动引发持续重试风暴**（唯一有评论的 Issue，2 条）
[链接](https://github.com/temporalio/temporal/issues/11547) ｜ 作者 @ggbata ｜ 开于 2026-08-13（已 35 天）
> 机制非常具体：History 集群在持久化 QPS 上限运行时，**仅靠 `ResourceExhausted` 把队列 reader/task executor 打入长退避**来维持稳定、摊平负载。一旦持久化出现短暂抖动，退避被重置，集群立刻陷入持续重试风暴。
这是典型的"**稳定性依赖错误类型

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*