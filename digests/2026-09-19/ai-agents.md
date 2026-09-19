# OpenClaw 生态日报 2026-09-19

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-19 00:25 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-09-19

---

## 1. 今日速览

OpenClaw 今日维持 **高活跃、高压力的维护状态**：24 小时内 Issues 更新 500 条（355 条新开/活跃，145 条关闭），PR 更新 500 条（254 条待合并，246 条已合并/关闭），但 **无新版本发布**。社区讨论高度集中在 **Gateway 性能退化、内存/WAL 膨胀、SQLite 损坏、子代理完成投递丢失** 等稳定性问题上，其中多条 P0/P1 级问题已持续数周未关闭（如 #91588 内存泄漏、#48003 steer 模式失效、#112423 SQLite 清理阻塞事件循环）。维护者今日提交了大量性能修复 PR（将 SQLite 枚举移出 Gateway 线程），显示团队正在系统性地解决"事件循环饥饿"这一根因。整体来看，项目**修复速度与社区报告速度较为匹配**，但核心运行时稳定性仍是制约项目健康度的最大风险。

---

## 2. 版本发布

**今日无新版本发布。** 结合 #151295（大型集群无法从 2026.9.4 升级）和 #150201（Windows 更新候选快照失败）等已关闭/活跃 Issue 来看，当前 2026.9.4 分支的升级链路仍存在摩擦，下一版本发布前可能需要先修复升级路径问题。

---

## 3. 项目进展

今日有 **246 个 PR 被合并/关闭**，重点推进以下方向：

### 性能与线程隔离（核心主线）
- **[#152005](https://github.com/openclaw/openclaw/pull/152005)** — 将 profile 枚举移出 Gateway 线程，改由共享状态 worker 执行。这是对 #112423、#149538 等"事件循环饥饿"根因的直接缓解。
- **[#152122](https://github.com/openclaw/openclaw/pull/152122)** — Matrix 机器人发现不再阻塞 Gateway 线程，凭证检查转由 SQLite worker 处理。
- **[#152270](https://github.com/openclaw/openclaw/pull/152270)** — 限制单 agent 名单查找的拷贝范围，减少多 agent 配置下的分配开销。
- **[#152294](https://github.com/openclaw/openclaw/pull/152294)** — 任务审计输出复用已备好的摘要，避免无谓排序。

### UI/UX 修复
- **[#152299](https://github.com/openclaw/openclaw/pull/152299)** — 修复 Control UI 对话完成后仍被标记为工作中、后续消息排队阻塞的问题（维护者 steipete 提交）。
- **[#152281](https://github.com/openclaw/openclaw/pull/152281)** — 同一页面在多个标签页打开时，聊天中的预览卡片不再重复显示。
- **[#152012](https://github.com/openclaw/openclaw/pull/152012)** — 云端配置重试时重置耗时计时器。

### 远程工作区与文件传输（feature 线）
- **[#150857](https://github.com/openclaw/openclaw/pull/150857)**、**[#150734](https://github.com/openclaw/openclaw/pull/150734)**、**[#152289](https://github.com/openclaw/openclaw/pull/152289)**、**[#150946](https://github.com/openclaw/openclaw/pull/150946)** — Kimiyu-186 提交的一组 stacked PR，实现 Gateway 与配对节点之间的文档读写、附件传输、Memory/Skills worker 接入。这是一条正在推进的**远程工作区"feature 主线"**，但均标记 `merge-risk: compatibility` 与 `security-boundary`，需谨慎审查。

### 流程与治理
- **[#152292](https://github.com/openclaw/openclaw/pull/152292)** — 撤销 #152226 未获授权的 duration-bucket 合并（`diagnostics-otel`），由任务请求者明确指示回滚。体现了对 agent 自主变更授权边界的管理。

**项目整体向前迈进的幅度**：性能线程隔离取得实质进展（4 个相关 PR），UI 稳定性小幅改善，远程工作区功能线继续推进但尚未合并。**未观察到重大功能落地或 API 变更被合并。**

---

## 4. 社区热点

### 🔥 讨论最活跃 Issues

| 排名 | Issue | 评论 | 👍 | 核心诉求 |
|---|---|---|---|---|
| 1 | **[#97616](https://github.com/openclaw/openclaw/issues/97616)** 僵尸子进程累积 | 30 | 1 | hook/tool 子进程未被回收，`openclaw-hooks`、`bash`、`codex` 僵尸堆积导致运行时退化 |
| 2 | **[#91588](https://github.com/openclaw/openclaw/issues/91588)** Gateway 内存泄漏 | 26 | 1 | RSS 从 350MB 涨到 15.5GB，2-3 天触发 OOM，引发 launchd-handoff 重启循环 |
| 3 | **[#149361](https://github.com/openclaw/openclaw/issues/149361)** WebUI 性能与稳定性总括 | 22 | 0 | 汇总桌面端与移动端 WebUI 的性能问题，保持小修复分组 |
| 4 | **[#48003](https://github.com/openclaw/openclaw/issues/48003)** steer 模式 mid-turn 注入失效 | 20 | **4** | 用户消息被排队到回合结束，而非在工具边界注入当前回合——高 👍 表明诉求普遍 |
| 5 | **[#149538](https://github.com/openclaw/openclaw/issues/149538)** Gateway 就绪但无法服务 | 19 | 0 | 632-agent 集群上 `[gateway] ready` 后所有 /health 探测超时，事件循环饥饿 + RSS 攀升 |
| 6 | **[#112423](https://github.com/openclaw/openclaw/issues/112423)** SQLite transcript 清理阻塞事件循环 | 17 | 0 | 归档大型 transcript 时在主线程做全量物化、压缩、I/O，导致事件循环阻塞 |

**分析**：讨论热度前 6 名中，**4 个直接指向 Gateway 事件循环饥饿/资源泄漏**（#97616、#91588、#149538、#112423），说明这是当前社区最集中的痛点。这些 Issue 均带有 `clawsweeper:no-new-fix-pr` 或 `needs-maintainer-review` 标签，**缺少可直接合并的修复 PR**，是维护者需要优先投入的方向。

### 🔥 讨论最活跃 PRs

| PR | 状态 | 主题 |
|---|---|---|
| **[#150857](https://github.com/openclaw/openclaw/pull/150857)** | OPEN, XL | Gateway ↔ 远程工作区附件传输（stacked） |
| **[#152289](https://github.com/openclaw/openclaw/pull/152289)** | OPEN, XL | 将 Memory/Skills 连接已配对节点 |
| **[#152118](https://github.com/openclaw/openclaw/pull/152118)** | OPEN, XL | 原生配额耗尽后继续已完成的文件工具工作（refs #151572） |
| **[#150946](https://github.com/openclaw/openclaw/pull/150946)** | OPEN, XL | 使用远程工作区文件驱动 Memory/Skills（已被更小 PR 取代） |
| **[#145169](https://github.com/openclaw/openclaw/pull/145169)** | OPEN, XL, P1 | 更新回滚失败时保留较新数据（关联 #144005、#142770） |

---

## 5. Bug 与稳定性

### 🔴 P0 — 严重（服务不可用/数据风险）

| Issue | 状态 | 摘要 | Fix PR |
|---|---|---|---|
| **[#149538](https://github.com/openclaw/openclaw/issues/149538)** | OPEN | 632-agent 集群 Gateway 就绪但不服务，/health 全部超时，事件循环饥饿 | ❌ 无 |
| **[#143524](https://github.com/openclaw/openclaw/issues/143524)** | OPEN | Windows 上 Agent SQLite WAL 增长到 1.4–2.8GB，阻断 Gateway 启动 | ❌ 无 |

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报
**日期：2026-09-19** ｜ 数据源：GitHub（NousResearch/hermes-agent）

> 数据说明：本次采样覆盖过去 24 小时内更新的 500 条 Issue 与 500 条 PR 的活动统计，明细仅展示评论数最高的 30 条 Issue 与 20 条 PR；PR 评论数字段缺失，相关排序依据 GitHub 返回顺序。以下分析基于该样本。

---

## 1. 今日速览

- 今日**无新版本发布**，项目处于纯开发/维护节奏，工作重心集中在缺陷修复与大规模代码重构。
- 流转吞吐维持高位：Issue 关闭 284 条 vs 新开/活跃 216 条，PR 合并/关闭 269 条 vs 待合并 231 条，**关闭量均超过新增量**，积压呈净收敛态势（Issue 约 -68、PR 约 -38）。
- 讨论热度最高的是自动化集成阻塞 Issue #88584（116 条评论），但其被标记为 `invalid`，属于机器人/CI 噪音型长尾讨论，需人工收口。
- 热点技术区域高度集中：**Desktop 客户端稳定性、Gateway/多平台消息投递、Cron/Kanban 调度正确性、安装更新流程**四大板块占据了今日高评论 Issue 的绝大多数。
- 代码侧正在推进两条主线：一是 `scripts/release.py`、`credential_pool.py`、`openviking` 等大文件的**模块化拆分（Part of #79962 / #79944 / #79912）**，二是针对 Windows 更新失败、Desktop SIGTRAP 崩溃、Matrix 安全边界等**高优 P1/P2 修复**。

---

## 2. 版本发布

本期无新版本发布（0 个 Release，Releases 列表为空），故略。

---

## 3. 项目进展

今日可见样本中，**Issue 侧关闭 284 条**，其中包含大量 P1/P2 缺陷的收口，是当日最主要的推进成果：

**已关闭的重要 Issue（按优先级）**
- #39609 [P1] Kanban 任务 `--initial-status blocked` 被 ~1 秒后无 actor 自动提升为 `ready`，**人类审批门被绕过** — 已关闭
  https://github.com/NousResearch/hermes-agent/issues/39609
- #68592 [P1] 非 Kanban 分发的 Cron Agent 被强制注入 `kanban_show` 协议 — 已关闭
  https://github.com/NousResearch/hermes-agent/issues/68592
- #105861 [P1] Cron Agent 任务成功投递结果被 "Interrupted by shutdown" 覆盖 — 已关闭
  https://github.com/NousResearch/hermes-agent/issues/105861
- #107224 [P1] `respawn-argv` 为未实现的伪重启机制，导致 `fleet_restart_pending` 长期悬挂 — 已关闭
  https://github.com/NousResearch/hermes-agent/issues/107224
- #92758 [P1] MCP OAuth 在 Desktop 上因回调丢弃 RFC 9207 `iss` 参数而失败 — 已关闭
  https://github.com/NousResearch/hermes-agent/issues/92758
- #85495 [P1] 一次性模式（`-z`）下 `--in <dir>` 被恢复的会话 cwd 静默覆盖 — 已关闭
  https://github.com/NousResearch/hermes-agent/issues/85495
- #20548 / #80125 [P1] 飞书 thread_id 回退导致全部回复挂载成线程；微信适配器 `ret=-2` 误报为限流 — 均已关闭
  https://github.com/NousResearch/hermes-agent/issues/20548 ｜ https://github.com/NousResearch/hermes-agent/issues/80125
- 其余已关闭： #80670（Desktop 表情回应 4040）、#49664（`show_reasoning` 开关无效）、#18473（`search_files` 隐藏目录返回 0）、#72529（WhatsApp 群消息不可达）、#83617（重命名对话框吞空格键）、#78486（聊天视图跳回历史块）、#60789（`session_search(profile=)` 失效）

**PR 侧（今日合并/关闭 269 条，样本内可见的关键项）**
- #115494 [CLOSED] `feat(skills): add evidence-first delivery workflow` — 当日提交当日关闭，新增「证据优先交付」内置 Skill（含行为契约测试），交付链路标准化再进一步
  https://github.com/NousResearch/hermes-agent/pull/115494
- #115495 [P1] `fix(windows): self-heal post-update gateway relaunch via Scheduled Task` — 解决 Windows `hermes update` 后网关无法存活的长期痛点
  https://github.com/Nous

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目日报 · 2026-09-19

> 数据来源：github.com/OpenHands/software-agent-sdk ｜ 统计窗口：过去 24 小时
> 说明：原始数据中 PR 评论数为 `undefined`，且未列出 2 个已合并/关闭 PR 的具体编号，相关分析基于可见摘要推断，已在文中标注。

---

## 1. 今日速览

- **活跃度处于高位**：24 小时内 31 条 Issue 更新（新开/活跃 24、关闭 7）、50 条 PR 更新，但仅 2 条 PR 被合并/关闭，**48 条仍待处理**，合并吞吐与提交量严重不匹配。
- **稳定性是本日主线**：`Telemetry._cache_buckets` 的 `PromptTokensDetailsWrapper.cache_creation_tokens` AttributeError 在三个独立 Issue（#5168、#5099、#5134）中重复出现，已成为跨 provider 的共性崩溃点。
- **安全与模型适配持续升温**：#2721（用 tree-sitter-bash 替换正则安全分析）以 16 条评论成为今日讨论中心；DeepSeek V4.x 与 MiniMax M3 的 `reasoning_effort` 兼容性问题集中爆发。
- **工程治理议题抬头**：发布流程（#4887）、Docker 运行时生命周期（#5177/#4993/#5004/#5007）、评审规范（#5175）等多条"ready-for-dev" 基础设施类 Issue 同日活跃。
- **健康度评价**：社区供给旺盛、方向明确，但 **PR 积压（含 6 月创建的 #3912/#3913）与 0 版本发布**构成主要风险，需警惕评审瓶颈。

---

## 2. 版本发布

本日**无新版本发布**。但 Issue #4887 揭示了发布工程的实质性隐患，值得关注：

- [#4887 Centralize release publication dispatches](https://github.com/OpenHands/software-agent-sdk/issues/4887)（`priority:medium`，4 条评论）
  - 发布流程混用显式 workflow dispatch 与 `release: published` 监听器；用 `GITHUB_TOKEN` 创建的 release **不会触发下游 workflow**。
  - 后果：v1.45.0 跳过了两个 TypeScript registry 发布器，PyPI 发布器也因版本号问题失败。
  - 影响：属于**发布链路的静默失败**，会直接造成制品缺失，建议优先修复。

---

## 3. 项目进展

本日数据未给出 2 条已合并/关闭 PR 的编号，因此无法逐一归类；从 Issue 侧可确认以下**已关闭**条目，代表近期推进方向已落地：

| 已关闭 Issue | 主题 | 意义 |
|---|---|---|
| [#2708](https://github.com/OpenHands/software-agent-sdk/issues/2708) | 扩展安全模式覆盖未覆盖的攻击族 | 安全防御纵深（defense-in-depth）补齐六类攻击面，与 #2721 的架构重构形成衔接 |
| [#4491](https://github.com/OpenHands/software-agent-sdk/issues/4491) | DeepSeek prompt cache hits 未计入 LLM 遥测 | 对应 PR [#4490](https://github.com/OpenHands/software-agent-sdk/pull/4490) 仍在 open，属"问题确认关闭、修复待合"状态 |
| [#4368](https://github.com/OpenHands/software-agent-sdk/issues/4368) | ACP 会话在 Laminar 中不可见（无 LLM/TOOL span） | 可观测性缺口修复，ACP 链路生产可用性提升 |
| [#4469](https://github.com/OpenHands/software-agent-sdk/issues/4469) | `FileEditor.str_replace` 校验片段起始行偏移一行 | 工具层正确性修复 |
| [#4388](https://github.com/OpenHands/software-agent-sdk/issues/4388) | `search_bash_events` 在 `order__gt` 下分页错误 | 修复客户端在空下一页上死循环的问题 |
| [#4443](https://github.com/OpenHands/software-agent-sdk/issues/4443) | PyInstaller 包缺失 `browser_use/js`（rrweb 录制） | 修复冻结版 `browser_start_recording` 的 FileNotFoundError |

**整体推进评估**：本日进展集中在**正确性与可观测性修复**（编辑器边界、分页、遥测、打包），而非新功能落地。以 50 条 PR 更新仅 2 条收口计算，**当日"净前进"有限**，绝大部分工作量仍处于等待评审状态。

---

## 4. 社区热点

按评论数与反应数排序：

1. **[#2721 Replace regex-based shell command analysis with tree-sitter-bash](https://github.com/OpenHands/software-agent-sdk/issues/2721)** — 16 评论，👍1，创建于 2026-04-06，标签 `security-related, proposal`
   - 诉求：安全模块基于"扁平化命令文本 + 正则"匹配，终端模块另用 `bashlex` 做切分与转义，两套语义不一致，存在绕过空间。主张统一到 tree-sitter-bash 的 AST 分析。
   - 分析：这是本仓库**生命周期最长、讨论最深的架构议题**（已持续 5 个月）。它决定了安全边界能否形式化，是 #2708 等模式补丁的上位问题。

2. **[#5168 AttributeError in Telemetry._cache_buckets](https://github.com/OpenHands/software-agent-sdk/issues/5168)** — 7 评论，👍1，`priority:medium, ready-for-dev`
   - 诉求：任何在 `prompt_tokens_details` 中缺少 cache 字段的 provider 都会在 profile 校验与 token 记账处崩溃，已用 MiniMax 复现。

3. **[#4405 Support Agent Plugins (agent-plugins.org) portable package format](https://github.com/OpenHands/software-agent-sdk/issues/4405)** — 6 评论，`Needs Design`
   - 诉求：对齐 v1.0.0 Working Draft 的厂商中立插件标准（TSC 含 Amazon、Cursor、Microsoft 等），使 OpenHands 组件可跨 agent 复用。子任务 [#5159](https://github.com/OpenHands/software-agent-sdk/issues/5159) 已推进到"提交 Compatible Clients 页面"。

4. **[#5099](https://github.com/OpenHands/software-agent-sdk/issues/5099) / [#5134](https://github.com/OpenHands/software-agent-sdk/issues/5134)** — 4 评论 / 2 评论
   - 与 #5168 同一根因的三个独立报告，反映该缺陷在 1.48.0 版本上的**广泛触达**，且分别来自不同用户与不同 provider。

**背后信号**：社区关注点正从"功能能用"转向"**边界是否安全、失败是否优雅**"。安全架构（#2721）与遥测健壮性（#5168 系列）分别是长期与短期两条主线。

---

## 5. Bug 与稳定性

按严重程度排列：

### 🔴 高：跨 provider 遥测崩溃（三报同源）
- [#5168](https://github.com/OpenHands/software-agent-sdk/issues/5168)｜[#5099](https://github.com/OpenHands/software-agent-sdk/issues/5099)｜[#5134](https://github.com/OpenHands/software-agent-sdk/issues/5134)
- 现象：`Telemetry._cache_buckets` 抛出 `'PromptTokensDetailsWrapper' object has no attribute 'cache_creation_tokens'`，**直接中断 LLM 调用与成本核算**，而非降级为 `cache_read=0`。
- 触发条件：provider 返回 cache read 但无 cache creation 字段（MiniMax M3、DeepSeek 兼容端点等）。
- 严重度说明：虽标 `priority:medium`，但实际表现为**用户侧硬崩溃**，建议上调。
- **Fix PR 状态**：PR [#4490](https://github.com/OpenHands/software-agent-sdk/pull/4490)（DeepSeek prompt cache hits 记账）触及同一模块，仍为 OPEN；针对本崩溃的直接修复 PR 尚未出现。**同日三报说明修复窗口已很紧迫。**

### 🔴 高：DeepSeek V4.x 推理参数依赖代理元数据
- [#5181](https://github.com/OpenHands/software-agent-sdk/issues/5181)｜`priority:high, ready-for-dev`，更新于 2026-09-19
- 现象：`reasoning_effort` 与输出上限依赖 proxy metadata——无元数据时参数被丢弃；有元数据时默认 384K 上限；`openai/` 前缀忽略覆盖值。
- 关联：#4934（停止基于通用 `supports_reasoning` 发送 `reasoning_effort`）、#4941（`deepseek-v4.1-flash` 成为云端默认模型）。
- **Fix PR 状态**：无。属"默认模型 + 参数推断"复合缺陷。

### 🟠 中：MiniMax M3 收到不支持的 reasoning_effort
- [#5173](https://github.com/OpenHands/software-agent-sdk/issues/5173)｜`priority:medium, duplicate-candidate`
- 现象：SDK 默认发送 `reasoning_effort=high`，LiteLLM 报 `UnsupportedParamsError`。
- 关键历史：同源 PR [#4935](https://github.com/OpenHands/software-agent-sdk/pull/4935) **已关闭未合并**，故障推断逻辑仍在。
- **Fix PR 状态**：无，且存在"修复被拒—问题复发"的循环风险。

### 🟠 中：ACP 子进程树在 POSIX 上成为孤儿
- [#4910](https://github.com/OpenHands/software-agent-sdk/issues/4910)｜`priority:medium, ready-for-dev`
- 现象：`process.terminate()` 只终止顶层 PID（如 `npx`），因未启用 `start_new_session=True`，`sh -c` 等后代进程残留。
- **Fix PR 状态**：✅ 已有 [PR #4909](https://github.com/OpenHands/software-agent-sdk/pull/4909)（进程组创建与回收），待合并。

### 🟠 中：TS 客户端丢弃 `acp_isolate_data_dir`
- [#5171](https://github.com/OpenHands/software-agent-sdk/issues/5171)｜`ready-for-dev, duplicate-candidate`
- 现象：`ACP_SETTINGS_KEYS` 缺少该键，每会话 CLI 数据目录隔离标志永不生效。**Fix PR 状态**：无。

### 🟠 中：Codex ACP 无头主机认证超时
- [#5167](https://github.com/OpenHands/software-agent-sdk/issues/5167)
- 现象：已登录

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报
**日期：2026-09-19** ｜ 数据源：github.com/temporalio/temporal

---

## 1. 今日速览

- **活跃度：高，且呈"清理+推进"双轨特征。** 过去 24 小时 Issues 更新 18 条（新开/活跃 3、关闭 15），PR 更新 60 条（待合并 40、已合并/关闭 20），并发布 1 个补丁版本 v1.31.3。
- **Issue 关闭率极高（83%）**，且关闭项多为历史 enhancement（部分可追溯至 2021–2024 年），显示维护团队正在进行一次集中的 Backlog 清理与分类归位；但仅 3 条为新开/活跃，社区新增输入相对低谷。
- **PR 侧是主要工作量所在**：40 条待合并 PR 构成较大队列，其中包含多条 7 段式堆叠 PR（namespace replication）、CHASM 迁移系列与动态分区调优系列，属大型架构工作而非零散修复。
- **稳定性方面有一好一忧**：arm64 上的指数退避 292 年溢出 Bug 已修复并关闭；但 MySQL 连接池无界增长（#9747，已挂起近 6 个月）与可见性写入静默失败（#12109）仍处开放状态。
- **整体健康度：良好偏积极**——补丁版本持续回填 v1.31 线，主线在 CHASM 化、Nexus 链接与分区弹性三个方向稳步推进；主要风险来自"高影响长期开放 Bug"与"待合并 PR 队列膨胀"。

---

## 2. 版本发布

### v1.31.3（补丁版本）

**性质：** v1.31 维护线 cherry-pick 回填版本，属稳定性/兼容性补丁，**无破坏性变更、无需特殊迁移步骤**，可按标准滚动升级执行。

| 变更 | 类型 | 说明 |
|---|---|---|
| Cherry-pick #11090 → [#11106](https://github.com/temporalio/temporal/pull/11106) | 稳定性加固 | 为 matching handler API 增加 panic 处理器，避免匹配服务在处理请求时因 panic 导致进程级影响。属"防御性"改动，对正常路径无行为变化。 |
| [#11982](https://github.com/temporalio/temporal/pull/11982) | 功能开关 | 为 v1.31 线加入 **Nexus callback source header 检查开关**（toggle）。注意其为默认关闭的开关项，启用后会对回调来源 header 进行校验，落地前需确认网关/代理是否透传相关 header。 |
| 依赖升级（go.tempor… 条目被截断） | 维护 | 推测为 `go.temporal.io/*` 系列依赖升级，通常修复上游兼容性问题，建议核对 go.mod diff。 |

**升级建议：** 若已启用 Nexus 回调相关能力，启用新开关前请在预发环境验证 header 透传链路；其余场景直接升级即可。

---

## 3. 项目进展

今日合并/关闭的 20 条 PR 中，以下具有实质推进意义：

**稳定性修复（已落地）**
- [#11992](https://github.com/temporalio/temporal/pull/11992) — 修复 `ExponentialRetryPolicy.ComputeNextDelay` 在 `maximumInterval == NoInterval` 时因溢出产生 ~292 年退避的问题（对应 Issue [#11991](https://github.com/temporalio/temporal/issues/11991)）。修复方式是在应用最大间隔与过期上限后，显式在达到 `MaxInt64` 纳秒时返回 `done`。**arm64 用户应重点关注**。
- [#11966](https://github.com/temporalio/temporal/pull/11966)（仍 OPEN）— 将 `DynamicRateLimiterImpl` 的每次刷新定时器替换为原子单调 deadline，规避 Go 1.23 起 timer channel 由运行时管理导致的每次取 token 都抢 timer 锁的性能损耗。

**CHASM 框架推进（架构主线）**
- [#12141](https://github.com/temporalio/temporal/pull/12141)（已关闭）— 从 CHASM 暴露 execution type 与 component path，为生成"执行完成回调"链接提供必要上下文。
- [#12070](https://github.com/temporalio/temporal/pull/12070)（已关闭）— 打通 `commonpb.Link_Callback` 与 `nexus.Link` 的双向转换。
- [#12139](https://github.com/temporalio/temporal/pull/12139)（已关闭）— verify transition task 不再需要加载 mutable state，改为在任务创建时捕获版本历史项，并可在获取工作流锁之前生成 verify task。属可观的延迟/锁竞争优化。
- [#12182](https://github.com/temporalio/temporal/pull/12182)（OPEN，今日新提交）— 修复 failover reset 后的 CHASM completion 回退问题。

**分区与调度弹性**
- [#12143](https://github.com/temporalio/temporal/pull/12143)（已关闭）— 为 `SimplePartitionScalerSettings` 增加 `{Fixed,Min,Max}AsMultipleOfOldCount`，支持相对于 `MatchingNumTaskqueueWritePartitions` 的相对缩放上下限，使托管式自动分区扩容更可控。
- [#12095](https://github.com/temporalio/temporal/pull/12095)（已关闭）— 补上动态分区"禁用"路径的 functional test（覆盖 #12026 修复的回归）。
- [#12138](https://github.com/temporalio/temporal/pull/12138)（OPEN）— 新增 scale manager 的 `Mode`（disabled/shadow/enabled），默认 shadow，为动态分区灰度上线提供安全阀。

**语义一致性**
- [#12081](https://github.com/temporalio/temporal/pull/12081)（已关闭）— 让已关闭 Schedule/Async Action 上的所有 operator 命令统一返回 `NotFound`，与 Workflow API 行为对齐。

**推进幅度评估：** 今日无"面向最终用户的单点大功能"落地，进展主要集中在**地基层**（CHASM 迁移、链接语义、分区控制面、锁竞争优化）。对项目健康度是正向的——但用户可感知的功能增量要等到这些堆叠 PR 全部合入后才会显现。

---

## 4. 社区热点

| 排名 | 条目 | 状态 | 热度指标 | 核心诉求 |
|---|---|---|---|---|
| 1 | [#9747](https://github.com/temporalio/temporal/issues/9747) MySQL Connector 在数据库持续不可用期间创建无界 sql.DB 池 | **OPEN**（自 2026-03-30） | 7 条评论，今日仍活跃 | 生产可靠性事故级问题：MySQL 宕机后恢复，`DatabaseHandle.reconnect()` 未遵守 `maxConns`，总连接数可超过 `(Pod 数) × (每 Pod 池数) × …`，存在打爆数据库连接上限的风险。**这是当前社区讨论最集中、也最需要维护者回应的一条。** |
| 2 | [#1203](https://github.com/temporalio/temporal/issues/1203) Add SignalWithReset | CLOSED | 👍 6（全场最高） | 来自社区论坛的 DSL workflow 场景，需基于信号重放/重执行历史任务。历经 5 年多终被关闭，是本次集中清扫的标志性条目。 |
| 3 | [#12162](https://github.com/temporalio/temporal/issues/12162) 在子工作流选项中暴露 start delay | CLOSED | 👍 5 | 客户端已支持 start delay，子工作流缺此能力，用户希望**功能对齐（feature parity）**。 |
| 4 | [#12153](https://github.com/temporalio/temporal/issues/12153) SDK 应提供原生 query builder | CLOSED | 4 条评论 | Visibility 查询能力强大，但 Go SDK 只能字符串拼接构造查询，"脆弱"且易错，用户希望类型安全的查询构造器。 |
| 5 | [#12151](https://github.com/temporalio/temporal/issues/12151) 工作流/活动失败的标准错误处理接口 | CLOSED | 2 条评论 | 各 SDK 硬编码失败日志方式，应用侧有上下文却无法介入，只能靠 correlation ID 事后关联。 |

**热点分析：** 今日热度榜呈现明显的"**补偿性需求**"特征——用户要的不是新抽象，而是**跨 SDK/跨 API 的能力一致性**（子工作流对齐客户端、错误处理统一、查询构造类型安全）。这类诉求若长期不回应，容易转化为多 SDK 各自为政的生态碎片化。

---

## 5. Bug 与稳定性

按严重程度排序：

### 🔴 高 — [#9747](https://github.com/temporalio/temporal/issues/9747) MySQL 连接池无界增长（OPEN，无 fix PR）
- **现象：** MySQL 掉线恢复期间，`DatabaseHandle.reconnect()` 持续创建新的 `sql.DB` 池，总连接数突破配置的 `maxConns` 上限。
- **影响面：** 所有使用 MySQL 作为持久化后端的集群；DB

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*