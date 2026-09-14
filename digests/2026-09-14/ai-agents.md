# OpenClaw 生态日报 2026-09-14

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-14 00:16 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报
**日期：2026-09-14** | 数据源：github.com/openclaw/openclaw

---

## 1. 今日速览

- **维护吞吐量处于高位**：过去 24 小时共处理 1,000 条 Issue/PR 更新，其中 Issues 关闭 214 / 新增活跃 286（关闭率 42.8%），PR 合并或关闭 261 / 待合并 239（处理率 52.2%），项目处于高强度收敛节奏中。
- **更新与升级可靠性成为绝对主线**：当日出现至少 5 个 P0 级更新失败报告（#146394、#147160、#145192、#146958、#145252 跟踪帖），覆盖 2026.9.2 → 2026.9.4 全链路，且已有专门维护者跟踪帖，属于当前最高优先级风险面。
- **稳定性问题集中在"状态与消息丢失"**：会话状态（session-state）、消息丢失（message-loss）、子代理完成通知丢失是 P1 队列中最密集的标签组合，说明多代理编排与持久化路径仍是架构级薄弱点。
- **无新版本发布**，当日所有动作集中在修复、升级修复链路与文档/成熟度补齐。
- **资深维护者（steipete、RomneyDa、obviyus、roboclaw-bot）当日提交密集**，PR 侧以 UI、更新器、i18n、macOS 体验类小步快跑为主。

**健康度评估**：整体活跃度极高、响应及时，但 **P0 级更新失败聚集 + 长期存在的高评分开源 Issue 无修复 PR** 构成了两个明确的健康度扣分项。

---

## 2. 版本发布

**本日无新版本发布。**

---

## 3. 项目进展

当日 PR 侧呈现"维护者主导 + 社区贡献混合"的格局，主要推进方向如下：

### 3.1 更新器（Updater）可靠性链路重写
这是当日最成体系的一组工作，由 @RomneyDa 主导的多 PR 依赖链推进：
- [#144811](https://github.com/openclaw/openclaw/pull/144811) `fix(update): show the actual health check failure once` — 不再用泛化标题掩盖真实 CLI 失败原因，避免 JSON 与 CLI 双重重复输出。
- [#147581](https://github.com/openclaw/openclaw/pull/147581) `fix(update): retain configuration and plugin failure details` — 保留配置校验与插件注册表的可操作错误详情，并对敏感值做脱敏。
- [#147588](https://github.com/openclaw/openclaw/pull/147588) `fix(update): use plain language for update checks` — 将"linting"、"candidate"等术语替换为用户可理解表述。
- [#144836](https://github.com/openclaw/openclaw/pull/144836) `fix(update): report dirty checkouts as failed updates` — 修复开发态脏检出被误报为"成功但跳过更新"的问题。
- [#147584](https://github.com/openclaw/openclaw/pull/147584) `feat(update): accept owner-bound repair turns` — 为更新修复工人引入有界推理轮次，同时保留更新器对验证与恢复的所有权。

> **推进意义**：这组 PR 直接对应 #145252、#145192、#147160 等 P0 更新失败报告，是当前最关键的稳定性投资。

### 3.2 会话状态与任务生命周期
- [#142018](https://github.com/openclaw/openclaw/pull/142018) `fix(sessions): converge projections during active writes`（P1，merge-risk: session-state）— 允许 transcript 投影重建声明一个有界的同代 append-only 尾部，而非在活跃会话推进时反复重启；统一了 live indexing / suffix projection / rebuild catch-up 的追加分类器。这是对 #119720（同步持久化阻塞 Gateway 事件循环）方向的重要回应。
- [#147585](https://github.com/openclaw/openclaw/pull/147585) `fix(tasks): record execution ownership and settle orphaned records at restore` — 修复强制 Gateway drain 超时后，无子进程的 native task 记录残留 `running` 状态、导致继任者再次等待 drain 的问题（对应 #143420）。

### 3.3 客户端与用户体验
- [#147552](https://github.com/openclaw/openclaw/pull/147552) `fix: prevent cloud-session archives from stalling and reappearing` — 归档失败的云会话不再卡在无关的 provisioning 之后，侧栏也不再"先隐藏后复现"。
- [#147565](https://github.com/openclaw/openclaw/pull/147565) `fix(ui): keep chat images in place while loading` — 修复聊天图片加载时附件卡片消失、留白、图片把后续消息向下推的抖动问题。
- [#147540](https://github.com/openclaw/openclaw/pull/147540) `feat(macos): collapse completed work above chat replies` — macOS 聊天窗口折叠已完成的工作与工具调用，改善长对话可读性。
- [#143489](https://github.com/openclaw/openclaw/pull/143489) `feat(ui): render session references as accent links with a chat icon` — 会话引用由方框改为行内强调链接。
- [#147569](https://github.com/openclaw/openclaw/pull/147569) `fix: allow reordering plugin sidebar pages` — 插件侧栏页可拖拽排序且跨重载保持。

### 3.4 渠道、网关与互操作
- [#147573](https://github.com/openclaw/openclaw/pull/147573) `improve(routing): reduce work on cached Discord routes` — 已缓存路由不再重复做多角色处理。
- [#146230](https://github.com/openclaw/openclaw/pull/146230) `fix(macos): forward MCP app sandbox over remote SSH` — 修复 macOS 远程 SSH 模式下 MCP App / Board widget iframe 无法加载（对应 #145522）。
- [#140423](https://github.com/openclaw/openclaw/pull/140423) `fix: disable iOS branch switching during active runs` — Apple 客户端分支切换改为查询 Gateway 真实会话视图，而非仅凭本地活动判断（对应 #137843）。

### 3.5 质量与基础设施
- [#147536](https://github.com/openclaw/openclaw/pull/147536)（已关闭合并）`fix(qa-channel): preserve final replies and clear unfinished previews` — 修复 QA 最终回复被迟到的草稿覆盖或被清理删除的问题。
- [#116446](https://github.com/openclaw/openclaw/pull/116446) `test(qa): run Discord through Crabline` — 将 Discord 纳入免凭据的 Crabline QA 渠道驱动。
- [#143528](https://github.com/openclaw/openclaw/pull/143528) / [#143548](https://github.com/openclaw/openclaw/pull/143548) — 扩展成熟度分类，覆盖共享 Gateway 治理、外部协议互操作、fleet 执行与可移植会话状态生命周期。
- [#147527](https://github.com/openclaw/openclaw/pull/147527) `fix(pr): keep cleanup scoped to the requested worktree` — 修复 PR worktree 清理会波及无关 worktree 注册的问题。

**整体向前迈进程度**：中高。虽然无版本发布，但当日合并/关闭 261 个 PR，其中更新器链路、会话投影收敛、任务归属恢复三项属于架构级修复。

---

## 4. 社区热点

### 4.1 讨论最活跃的 Issues

| 排名 | Issue | 状态 | 评论 | 评分 | 核心诉求 |
|---|---|---|---|---|---|
| 1 | [#25592](https://github.com/openclaw/openclaw/issues/25592) 工具调用之间的文本泄漏到消息渠道 | OPEN | 40 | 🦞 diamond | 内部处理输出（错误处理、确认语、叙述）被当作可见

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目日报（2026-09-14）

---

## 1. 今日速览

- 项目维持**极高活跃度**：24 小时内 Issues 更新 500 条（新开/活跃 392、关闭 108），PR 更新 500 条（待合并 324、合并/关闭 176），但**关闭率偏低**（Issue 21.6%、PR 35.2%），积压呈扩大趋势。
- 今日最突出的技术主题是 **`state.db` WAL 代际生命周期事故群**：多个 P0/P1 Issue 描述同一类根因（短生命周期进程 unlink 活跃 WAL），并已被快速关闭，说明维护者响应迅速，但 **#109728 指出昨日合入的权限加固 #109509 又引入了新回归**，稳定性风险尚未收敛。
- Desktop（Bot Mode、会话创建、渲染内存）与 Cron 调度仍是故障高发区，前者贡献了今日多数 P1。
- 架构层面，`teknium1` 牵头的 **#106742「One gateway owns every local session」** 是当前最重量级的在途 PR，指向会话模型统一化。
- 无新版本发布，社区功能诉求集中在 **i18n 本地化**与**全局技能语义修正**。

---

## 2. 版本发布

今日无新 Release，无破坏性变更需公告。

---

## 3. 项目进展

今日合并/关闭的重要 PR（176 条已合并/关闭中的代表性项）：

| PR | 内容 | 意义 |
|---|---|---|
| [#110359](https://github.com/NousResearch/hermes-agent/pull/110359) [CLOSED] `fix(kanban): guard board writes by writer identity` | 通过 SQLite trigger 拒绝非规范写入者修改看板状态/结果，规范连接在连接时注册身份 | 收紧了多进程共享 `state.db` 下的写入边界，属安全加固 |
| [#85246](https://github.com/NousResearch/hermes-agent/pull/85246) [CLOSED] `fix(reasoning): hide unsupported effort choices in model pickers` | Desktop/Dashboard 模型选择器不再展示模型无法表达的 reasoning effort 档位 | 修复长期存在的 UI/后端能力错配 |
| [#110410](https://github.com/NousResearch/hermes-agent/pull/110410) [CLOSED] `feat(desktop): collapse Cursor tool chrome` | 将 Cursor/ACP/Copilot 转录中的工具活动归约为 Hermes 工具折叠块 | 桌面端转录可读性提升 |
| [#110411](https://github.com/NousResearch/hermes-agent/pull/110411) [CLOSED] `feat(desktop): nest plugin sidebar.nav children` | 插件侧边栏子项支持分组展开/折叠 | 插件生态 UI 容量问题初步缓解 |

**在途重点 PR**（尚未合入，但方向关键）：

- [#106742](https://github.com/NousResearch/hermes-agent/pull/106742) `One gateway owns every local session`（P1，自 09-09 持续更新）——让 CLI/TUI/Desktop/API/ACP/bots/cron 全部附加到同一个 gateway 持有的会话，直接回应了今日 WAL 事故群与多进程竞争问题。**若合入将是本季度最大的架构级推进。**
- [#110179](https://github.com/NousResearch/hermes-agent/pull/110179) `refuse held state.db publish; replay diverted transcripts`——针对 #65942/#90950 类「已 unlink WAL 仍被写入」问题的正面修复。
- [#108836](https://github.com/NousResearch/hermes-agent/pull/108836) `fix(clinical): repair protected responses before delivery`——跨 CLI/Gateway/ACP/消息通道的 fail-closed 交付前边界，合规向。

**整体推进评估**：今日以修复收尾为主，功能新增有限；架构统一（#106742）与状态库一致性（#110179）是决定下一版本稳定性的两条主线。

---

## 4. 社区热点

1. **[#88584](https://github.com/NousResearch/hermes-agent/issues/88584)（97 评论，👍0）** — `[P3] Automated Nous integration is blocked`
   定时 Nous→Enterkey 合并因 `cron/jobs.py` 冲突持续阻塞，dashboard updater 停留在最后一个已测试的 Enterkey release。虽是 P3 标签，但**评论数为全站之最**，反映的是发布流程/自动化流水线问题被长期挂起，而非单点 bug。

2. **[#109552](https://github.com/NousResearch/hermes-agent/issues/109552)（17 评论）** — `Label audit (unverified)`
   社区成员对 alt-glitch triage bot 打出的 `duplicate`/`invalid` 标签提出系统性质疑，强调「标签是检索提示，不是处置结论」。**这是治理层面的信号**：自动分诊的准确性正在侵蚀社区信任。

3. **[#40239](https://github.com/NousResearch/hermes-agent/issues/40239)（12 评论，👍4，今日仍在更新）** — 桌面端 pt-BR 本地化
   指出后端/TUI 已有 `locales/pt.yaml`（357+ 行），但 Desktop UI 仍无葡语选项，属明显的**能力断层**。

4. **[#5941](https://github.com/NousResearch/hermes-agent/issues/5941)（8 评论，👍30）** — 引入 Searxng 作为默认搜索后端
   **今日点赞最高的 Issue**，反映用户对搜索供应商锁定与自托管能力的强烈偏好。

5. **[#19451](https://github.com/NousResearch/hermes-agent/issues/19451)（9 评论，👍7）** — 「全局技能应真正跨 profile 全局」
   指出 `~/.hermes/skills/` 实际是「默认 profile 技能」而非「全局技能」，属于**术语与行为的语义错配**，多 profile 用户认知负担显著。

---

## 5. Bug 与稳定性

### 🔴 P0 —— `state.db` WAL 代际事故群（**今日最高优先级风险，建议优先跟进**）

| Issue | 状态 | 要点 | Fix PR |
|---|---|---|---|
| [#109687](https://github.com/NousResearch/hermes-agent/issues/109687) | CLOSED | 单次普通 CLI 调用即可孤立活跃 gateway 的 WAL 代际，gateway 继续服务但静默丢弃会话写入（Linux，`main@92df11f8`，复现于 #102589 修复之后） | 已被关闭，指向 #110179 类修复 |
| [#109786](https://github.com/NousResearch/hermes-agent/issues/109786) | CLOSED | 短命的 write-then-close 连接 unlink `state.db-wal/-shm`；**`hermes doctor` 会杀死正在运行的 gateway** | 已关闭 |
| [#109728](https://github.com/NousResearch/hermes-agent/issues/109728) | **OPEN** | **#109509 权限加固（`_secure_state_db_files()`）在 Linux 上关闭 fd 导致 SQLite POSIX 锁被取消，删除 WAL 代际** | ⚠️ 尚未见对应 fix PR，回归未收敛 |
| [#109727](https://github.com/NousResearch/hermes-agent/issues/109727) | **OPEN** | 任意第二个 Hermes 进程（甚至只读的 `hermes sessions list`）即可 unlink 活跃 WAL/SHM，gateway 陷入 `DeletedWalGenerationError` | 与 #110179 方向一致 |

> **分析**：这一组事故共享同一根因——多进程共享 `state.db` 时缺乏跨进程代际所有权。它同时解释了 #106742（单 gateway 持有全部本地会话）为何被提升到 P1 并持续推动。**#109728 的未修复状态是本日最大遗留风险**，建议在下一 patch 版本前解决。

### 🟠 P1

- **Desktop 渲染内存无界增长** [#77311](https://github.com/NousResearch/hermes-agent/issues/77311)（OPEN，自 08-03 挂起）——`apps/desktop/src/store/session.ts:409` 永久保留每个已打开会话的全部消息，重度使用后 fleet 内存达 5 GB。**已挂起 6 周，无 fix PR**。 ↑ 长期未解决
- **`hermes update` 留有永久 gateway 重启警告** [#107402](https://github.com/NousResearch/hermes-agent/issues/107402)（OPEN，16 评论）——当从 gateway 自身进程树内触发时，重启被正确推迟（见 #77184），但 updater 立刻校验并写入 `state: stale`，导致运行以 `partial` 结束。
- **Desktop Bot Mode 点击无响应** [#105104](https://github.com/NousResearch/hermes-agent/issues/105104)（OPEN）——非确定性，失败时后端零活动。
- **MCP OAuth 轮换凭证跨进程损坏** [#71335](https://github.com/NousResearch/hermes-agent/issues/71335)（OPEN，P1 + `risk-security-boundary`）——并发 Hermes 进程共享 `HERMES_HOME` 时，`mcp-tokens` 无跨进程锁，Notion 授权被破坏。**安全边界问题，自 07-25 挂起**。 ↑ 长期未解决
- **已恢复会话无法 reaction（4040）** [#80670](https://github.com/NousResearch/hermes-agent/issues/80670)（OPEN，自 08-07）——仅在历史/恢复会话中出现，新会话正常。

### ✅ 今日已关闭的高价值 P1 修复

- [#87654](https://github.com/NousResearch/hermes-agent/issues/87654) 视觉工具在首次可用性探测后消失（`_AuxProbeClientStub` 被缓存）
- [#102792](https://github.com/NousResearch/hermes-agent/issues/102792) 桌面多 profile 下新建会话丢失 owner 元数据
- [#103375](https://github.com/NousResearch/hermes-agent/issues/103375) Bot 磁贴无限重连耗尽 Warm Backend 池（20+ profile 场景）
- [#86366](https://github.com/NousResearch/hermes-agent/issues/86366) `archive_and_compact()` 重复写入尾部导致 recall 重复
- [#55712](https://github.com/NousResearch/hermes-agent/issues/55712)

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目日报 · 2026-09-14

> 数据源：github.com/OpenHands/software-agent-sdk ｜ 统计窗口：过去 24 小时

---

## 1. 今日速览

- **活跃度：高，但集中在"分类与规划"，而非"落地交付"。** 过去 24 小时共 18 条 Issue 更新、50 条 PR 更新，但 PR 侧仅 2 条合并/关闭，48 条仍在待合并状态，合并率 **4%**，评审管道压力显著。
- **Issue 侧呈"双轨"特征**：一边是 #3549 / #3903 / #3884 / #3914 / #3797 等 5 条 6 月历史 Issue 集中被 `Stale` 标签触碰（9/8/7/5/4 条评论），疑似批量 triage；另一边是 9 月 12–13 日由 @neubig 主导的一批 `ready-for-dev` 新 Issue，聚焦 **Agent Profile 密钥隔离与运行时契约解耦**。
- **无新版本发布**，路线图信号主要来自 Issue/PR 层面。
- 3 条 Issue 关闭：#5030（Profile 密钥作用域，已实现）、#4738（Node.js 环境 DOM API 守卫，4 月老 Bug）、#5021（误用自动化账号提交，由 #5023 取代）。
- 整体判断：**项目健康度良好（问题被快速识别并标记 ready-for-dev），但外部贡献 PR 的积压是当前最明显的瓶颈。**

---

## 2. 项目进展（今日合并/关闭）

今日 PR 合并/关闭数为 **2 条**，但均未进入"评论数最多 Top 20"榜单，因此无具体说明。从可见数据看，**今日没有可归因的重要功能落地**。

不过，以下关闭项代表清理性进展：

| 项 | 类型 | 说明 | 链接 |
|---|---|---|---|
| #5030 | Issue 关闭 | Agent Profile 无法按 agent 限定其可接收的 secrets —— 作为 OSS-10492 目标一（自定义 prompt / 工具 / secrets / LLM）的"secrets 一半"，已关闸，对应实现由 SDK #4931 系列承接 | [#5030](https://github.com/OpenHands/software-agent-sdk/issues/5030) |
| #4738 | Issue 关闭（积压 ~5 个月） | `RemoteWorkspace.downloadAndSave()` 使用浏览器独占 DOM API，在 Node.js 下无守卫；长期老 Bug 关停 | [#4738](https://github.com/OpenHands/software-agent-sdk/issues/4738) |
| #5021 | Issue 关闭（重复） | skill 资源泄漏问题由自动化账号误提，改由 #5023 正式跟踪 | [#5021](https://github.com/OpenHands/software-agent-sdk/issues/5021) |

**前进幅度评估：** 低。今日主要消耗在 triage 与规划，代码实质推进有限。

---

## 3. 社区热点

> 注：本期 PR 评论数元数据缺失（均为 `undefined`），以下以 Issue 讨论热度为准。

### 🔥 讨论最活跃 Issue

| 排名 | Issue | 评论 | 状态 | 核心议题 |
|---|---|---|---|---|
| 1 | [#3549](https://github.com/OpenHands/software-agent-sdk/issues/3549) | 9 | OPEN / Stale | `tests/cross/test_hello_world.py` 加载了真实 frozen LLM fixture，却在主流程前被合成 mock 响应替换 —— **测试有效性存疑**（"假绿"风险） |
| 2 | [#3903](https://github.com/OpenHands/software-agent-sdk/issues/3903) | 8 | OPEN / Stale | 单条命令输出注入上下文超 **20,000 tokens**，呼吁改为**按需加载** |
| 3 | [#3884](https://github.com/OpenHands/software-agent-sdk/issues/3884) | 7 | OPEN / Stale | 提议引入**可回看的浏览器会话视频录制**，借鉴 executor e2e harness 技术 |
| 4 | [#3914](https://github.com/OpenHands/software-agent-sdk/issues/3914) | 5 | OPEN / Stale | 建议废弃并移除自定义 Jinja system prompt 回退路径 |
| 5 | [#3797](https://github.com/OpenHands/software-agent-sdk/issues/3797) | 4 | OPEN / Stale | Laminar / agent-server 的 INFO 日志经第三方 stderr handler 输出，被误摄为 `status:error` |

**诉求分析：**
- **上下文经济性**（#3903）与 **可观测性噪音**（#3797）是用户侧的持久痛点，均属"日常使用摩擦"，但已 `Stale` 数月未决，说明维护优先级低于架构重构。
- **测试可信度**（#3549）是内部质量问题，9 条评论说明存在实质技术争议，值得单独排期。
- **#3884** 由 agent 身份账号（@smolpaws）提出，体现社区已开始以 agent 参与 SDK 演进的模式。

### 📌 新兴热点（今日新开）

- [#5031](https://github.com/OpenHands/software-agent-sdk/issues/5031) —— **可选持久化记忆边界**。由 MemCode 创始人 @memcodeoff 直接提出商业合作式诉求：SDK 应定义"单次运行瞬态上下文"与"应用级持久记忆"的边界。这是**首个来自外部厂商的架构级合作提案**，2 条评论即引发关注。

---

## 4. Bug 与稳定性

按严重程度排序：

### 🔴 High

**#5025 — LookupSecret 在 loopback 解析时自死锁 agent-server 事件循环**
- 标签：`bug, priority:high, sdk, security, ready-for-dev`
- `LookupSecret.get_value()` 执行**同步阻塞**的 `httpx.get()`，当 URL

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 · 2026-09-14

> 数据来源：github.com/earendil-works/pi | 统计窗口：2026-09-13 ~ 2026-09-14

---

## 1. 今日速览

今日项目呈现**高吞吐的分诊与清理态势**：24 小时内 Issues 更新 29 条，其中关闭 23 条（79.3%），新开/活跃仅 6 条；PR 更新 8 条，6 条已合并或关闭，2 条待合并。整体活跃度评为**高**，但需注意关闭的 Issue 中有大量为创建当日即关闭的 `[untriaged]` 条目，更接近批量分诊而非逐一修复，实际修复产出需谨慎解读。今日无新版本发布，功能推进主要来自 2 条仍在开放状态的重要 PR（#9548 对话中系统消息、#9488 Codex 轮次归因）。**稳定性风险集中在 TUI 渲染层**：#8036（大 diff 导致 TUI 崩溃）与 #9255（全屏重绘风暴）两条长期未决的开放 Issue 构成当前最突出问题。

---

## 2. 版本发布

今日无新版本发布（0 个 Release）。最近一次涉及的版本基线为用户反馈中反复出现的 **0.85.1** 与 **0.62.0**。

---

## 3. 项目进展

今日 6 条 PR 完成合并/关闭流程，2 条保持开放：

| PR | 状态 | 内容 |
|---|---|---|
| [#9531](https://github.com/earendil-works/pi/pull/9531) | CLOSED | `feat(tree)`：会话树永久分支删除。新增 `SessionManager.pruneBranch(entryId)` + `countSubtree()`，保护活动路径、保留叶子、重链 label、重定向存活的 compaction；`/tree` 选择器新增 `shift+d` 交互 |
| [#9558](https://github.com/earendil-works/pi/pull/9558) | CLOSED | Azure Foundry v3 支持：为 Anthropic 模型新增 `azure-foundry` 接入，补齐 stream / abort / empty / context overflow / unicode / tool-call / image / total-tokens / 跨 provider handoff 测试矩阵 |
| [#9556](https://github.com/earendil-works/pi/pull/9556) | CLOSED | `feat(ai): serverTools` —— 在模型配置中声明 provider 服务端工具（OpenAI Responses `web_search`、智谱 GLM coding-plan Responses 代理、Anthropic `web_search`） |
| [#9543](https://github.com/earendil-works/pi/pull/9543) | CLOSED | 为模型新增 `exit` 工具调用（配套 Issue #9544） |
| [#9541](https://github.com/earendil-works/pi/pull/9541) | CLOSED | `fix(tui)`：模型选择器改用人类可读的 `name` 作为主标签，而非原始模型/provider 标识符 |
| [#9550](https://github.com/earendil-works/pi/pull/9550) | CLOSED（Withdrawn） | 「发送前基于 system + tool token 做 compact」—— 作者主动撤回，未合入 |

**仍在开放的关键 PR：**

- [#9548](https://github.com/earendil-works/pi/pull/9548)（@mitsuhiko）**Mid conversation system messages**：把系统提示文本与工具变更变成转录记录的一部分，而非静默重写起始条件。可记录指令变更时刻、在恢复/分支导航后还原该状态，并保留缓存 prompt 前缀。这是今日**架构影响最大**的改动方向。
- [#9488](https://github.com/earendil-works/pi/pull/9488)（@dannote）**canonical Codex turn attribution**：引入 provider 中立的 `requestIdentity`，解决同一用户输入组内跨工具续跑、重试、steering、compaction 恢复的请求归因问题。

**净推进评估**：会话树管理（分支删除）与多云端接入（Azure Foundry）两条线各向前推进一步；但今日无版本发布，且 6 条关闭 PR 中至少 2 条为撤回/门控自动关闭，**实质性功能增量有限**。

---

## 4. 社区热点

按评论数与反应数排序：

1. **[#7739](https://github.com/earendil-works/pi/issues/7739) OPEN — 启动时间预算（8 评论）**
   要求为 Pi 设定启动时间/内存预算，对齐 jcode 的 README 基准（10 次交互式 PTY 启动的中位延迟对比，jcode v0.9.1888-dev vs pi 0.62.0）。**诉求**：Pi 在冷启动性能上存在可量化的差距，社区希望将其作为可验收指标而非模糊目标。自 08-06 开至今，讨论持续但无 PR。

2. **[#8036](https://github.com/earendil-works/pi/issues/8036) OPEN — Edit 工具大 diff 导致 TUI 崩溃（8 评论）**
   `edit` 工具渲染约 **14.5 MB** diff（源自物理行极长的 HTML 文件）时崩溃交互式 TUI，且 edit 本身执行成功。初次崩溃发生在 edit 完成后，**session resume 时再次复现**。**诉求**：diff 渲染需要有大小/行宽上限或流式增量渲染，且需防护恢复路径。

3. **[#4538](https://github.com/earendil-works/pi/issues/4538) CLOSED — 为 `/quit` 增加 `/exit`

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目日报 · 2026-09-14

> 数据来源：github.com/BerriAI/litellm | 统计窗口：过去 24 小时

---

## 1. 今日速览

- **Issue 侧基本健康**：24 小时内 69 条 Issue 发生更新，新开/活跃 46 条、关闭 23 条，关闭率约 33%，社区提问与维护响应仍在正常流动。
- **PR 侧出现严重拥堵**：500 条 PR 更新中待合并高达 479 条，已合并/关闭仅 21 条（约 4.2%），且当日展示的高活跃 PR 大多为 2026 年 4–6 月提交的长期存量，说明合并吞吐是当前最大的瓶颈。
- **战略级动向持续推进**：Rust 迁移母 Issue #31263 以 26 条评论、20 个 👍 稳居热度榜首，讨论已从 6 月延续至今，是项目最受关注的长期议题。
- **"静默失败"是今日 Bug 主题**：参数泄漏导致 400、计费日志丢失、reasoning 进度丢失、缓存 token 计数错误——多条问题都属于"不报错但结果不对"的类型。
- **新版本 v1.102.0-rc.1 发布**，主要内容为 Docker 镜像 cosign 签名验证说明，无功能性变更信号。

---

## 2. 版本发布

### v1.102.0-rc.1（Release Candidate）

- 链接：https://github.com/BerriAI/litellm/releases
- 本次 Release Note 的主要内容是**供应链安全声明**：所有 LiteLLM Docker 镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 签名，且所有 release 沿用 commit `0112e53` 引入的同一密钥。

**要点提示：**
- 这是 **rc（候选）版本**，非稳定版，生产环境建议等待正式版。
- **无功能性更新描述**，未发现破坏性变更或迁移要求。
- 对安全合规敏感的用户（金融、企业内部网关场景），可借此次发布核对镜像签名校验流程是否已接入 CI/CD；密钥自 `0112e53` 起未轮换，意味着历史校验逻辑无需调整。

---

## 3. 项目进展

由于 PR 数据中评论数缺失（均为 `undefined`），无法按互动量排序；以下按"新提交"与"存量待合并"两类梳理。

### 今日新提交的 PR（值得优先关注）

| PR | 内容 | 链接 |
|---|---|---|
| #41026 | `fix(spend)`：当 provider 返回 `"id": null` 时回退到 call id。此前会写入字符串 `"None"` 作为 spend 行主键，导致批量插入去重后**除首条外所有请求均不计费** | [PR #41026](https://github.com/BerriAI/litellm/pull/41026) |
| #41025 | `fix(llm)`：在 provider 请求边界过滤内部参数。针对 Bedrock chat/embedding 因内部参数触发 HTTP 400 的问题，同时保留 fallback 凭证与流式控制字段 | [PR #41025](https://github.com/BerriAI/litellm/pull/41025) |

这两条 PR 直接回应了今日热度较高的 #30301（内部参数泄漏）与计费完整性问题，定位精准、范围收敛，是今日**最有价值的新增贡献**。

### 已合并 / 关闭

- 今日已合并/关闭 PR 共 21 条，但样本中仅 **#29791（docs：移除 webhook-test 回调示例，改用 example.com 占位）** 标记为 CLOSED，且带 `[stale]` 标签。
- **结论偏保守**：今日未观察到明确的功能级推进落地。可判断 21 条关闭中相当比例来自 stale 自动清理，而非人工合并。

### 对照 Issues 侧的实质修复进展

- #28464（模型访问检查忽略直接绑定到 Virtual Key 的 `access_group_ids`）已 CLOSED —— 属于权限正确性修复，价值较高。
- #29913（流式 `/v1/responses` 成功日志崩溃导致**不计费**）已 CLOSED —— 与今日新 PR #41026 属同一类"计费静默丢失"问题族，可作为已修复路径的参照。
- #39354、#25532、#29011、#32613、#33326、#33329、#33873 等批量关闭，但多数带 `[stale]` 标签，**不代表已修复，而是长期无响应后被自动归档**。

**推进度评估**：项目整体约 **前进 0.2 步**——Issue 清理效率尚可，但 PR 合并管线近乎停滞，社区贡献无法转化为实际代码入库。

---

## 4. 社区热点

### 🔥 #31263 — LiteLLM Rust Migration：sub 1ms overheads
- 评论 26 | 👍 20 | 自 2026-06-25 持续活跃
- https://github.com/BerriAI/litellm/issues/31263
- **官方主导的战略议题**（作者 @ishaan-berri），作为 Rust 迁移的母工单收集所有相关问题，并配套博客与 Beta 测试者招募表单。
- **信号解读**：这是全项目唯一带有 20 个 👍 的 Issue，反映用户对**网关性能开销**的高度敏感。LiteLLM 作为代理层，任何毫秒级延迟都会乘以调用量放大，Rust 重写是社区期待的"质变"级改进。

### #19105 — Confused by the budgets（12 条评论）
- https://github.com/BerriAI/litellm/issues/19105
- 自 2026-01-14 起开放，**已持续讨论 8 个月**，今日仍有更新。
- 用户困惑于 team budget 与 team member budget 的叠加语义，即使"研读了文档"仍无法正确配置 `max_budget`。
- **信号解读**：不是 Bug，而是**语义设计与文档表达的双重失败**。预算/配额是 LiteLLM 商业化场景的核心能力，8 个月未收敛说明抽象层次存在问题，而非缺一段文档。

### #26097 — 自托管安装因 schema.prisma 失败（7 条评论 | 👍 4）
- https://github.com/BerriAI/litellm/issues/26097
- `prisma generate` 命令被拒绝导致基础安装脚本失败，自 2026-04-20 开放至今。
- **信号解读**：这是**新用户转化路径上的硬阻断**。安装即失败会让潜在用户直接流失，👍 数与评论数不成比例地高（4/7），说明踩坑者众、发声者少。

### #30301 — 加固 provider transforms，防止内部 optional_params 泄漏（5 条评论）
- https://github.com/BerriAI/litellm/issues/30301
- 用户系统性地指出：多个零散 Issue 实为同一失败类——LiteLLM 转发的内部字段被严格 provider 拒绝。
- **信号解读**：这是一位高质量贡献者的"根因归纳"，今日已有对应 PR #41025 落地，**闭环速度较快**。

### #40583 — custom_code / tool_permission guardrails 无法看到 MCP 工具（5 条评论）
- https://github.com/BerriAI/litellm/issues/40583
- 使用 Anthropic `/v1/messages` 格式时，pre_call 模式的护栏**完全无法检视或拦截 MCP 工具调用**。
- **信号解读**：**安全边界失效**。企业用户依赖护栏做工具级权限管控，此问题意味着通过 Anthropic 兼容端点可以绕过管控。

### #39057 — 缓存命中时 spend=0，但 token 列回放原始用量（4 条评论）
- https://github.com/BerriAI/litellm/issues/39057
- **信号解读**：典型的可观测性语义分歧。用户

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*