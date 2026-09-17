# OpenClaw 生态日报 2026-09-17

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-17 00:39 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报
**日期：2026-09-17** ｜ 数据源：github.com/openclaw/openclaw

---

## 一、今日速览

1. 项目维持**极高活跃度**：过去 24 小时 Issues 更新 500 条（新开/活跃 324、关闭 176）、PR 更新 500 条（待合并 285、合并/关闭 215），单日吞吐量处于大型项目的头部水平。
2. **积压压力仍然偏大**：Issues 净增长约 +148 条，PR 待合并数（285）显著高于关闭数（215），关闭率仅约 35% / 43%，维护带宽被持续吞噬。
3. **风险高度集中在"更新/升级可靠性"**：2026.9.3 → 2026.9.4 的迁移、Doctor 预演、Windows 快照路径衍生出多条 P0 级 issue（#150201、#146394、#144739、#148681），已形成专门的协调追踪单。
4. **运行时稳定性问题持续发酵**：Gateway 内存泄漏、子进程僵尸堆积、MCP 初始化超时崩溃、632-agent 集群启动 12 分钟等"长尾性能债"仍无对应 fix PR 合并。
5. 今日无新版本发布，**无破坏性变更或迁移注意事项**。

---

## 二、版本发布

今日无新版本发布，亦无预发布/候选版本推送。（此处按规范省略详细说明。）

---

## 三、项目进展

今日合并/关闭 PR 共 **215 条**，关闭 Issue 共 **176 条**。在可见的 Top 样本中，明确的推进项包括：

| 方向 | 条目 | 说明 |
|---|---|---|
| 会话列表性能优化 | [#150103](https://github.com/openclaw/openclaw/pull/150103) **[CLOSED]** | 重构会话列举路径，避免为每个已加载会话分配独立 model-source 对象，减少临时对象分配，行为无变化。与 [#149291](https://github.com/openclaw/openclaw/pull/149291)（会话列表 CPU 耗时诊断）、[#148630](https://github.com/openclaw/openclaw/pull/148630)（把自动维护的 DB 工作移到 worker）构成一组"Gateway 主线程减负"的组合拳。 |
| 大附件/上传健壮性 | [#90098](https://github.com/openclaw/openclaw/issues/90098) **[CLOSED]** | Control UI 大 PDF 上传栈溢出（`RangeError: Maximum call stack size exceeded`）问题关闭，涉及把 data URL 全量物化 + 全字符串正则的路径做栈安全改造。 |
| 认证与密钥状态 | [#145929](https://github.com/openclaw/openclaw/issues/145929)、[#111578](https://github.com/openclaw/openclaw/issues/111578) **[CLOSED]** | `auth store lock may be busy` 永久失败、以及 Gateway auth token 在更新后从 service-env 丢失（反复回归）两条均已关闭。 |
| 重启后状态恢复 | [#146265](https://github.com/openclaw/openclaw/issues/146265) **[CLOSED]** | Gateway 重启后共享 `AsyncWorkScope` 保持 closed 导致所有 agent 工具报错，而 health 仍报 OK 的问题关闭。 |
| 沙箱/容器 | [#31331](https://github.com/openclaw/openclaw/issues/31331)、[#119125](https://github.com/openclaw/openclaw/issues/119125) **[CLOSED]** | Docker-outside-of-Docker 的 workspaceAccess 挂载、Codex `sandboxExecServer` 传非绝对路径 cwd 两个问题关闭。 |
| 安全侧 | [#111985](https://github.com/openclaw/openclaw/issues/111985) **[CLOSED]** | `memory-core` 将 ChatGPT/Codex OAuth token 作为 bearer 发往 `api.openai.com/v1/embeddings` 的凭证泄漏路径关闭。 |
| macOS 客户端 | [#94147](https://github.com/openclaw/openclaw/issues/94147) **[CLOSED]** | `CLLocationManager` 每秒重建导致 TCC 权限请求风暴的问题关闭。 |

**整体推进评估**：今日进展集中在"性能细节打磨 + 历史遗留清理"，而非新能力交付。真正卡住项目咽喉的 2026.9.3/9.4 更新链路问题，目前仍以"PR 在途、未合并"为主（见第五节），因此**项目净向前位移属于中等偏弱**——关闭数量可观，但高风险面未收敛。

---

## 四、社区热点

今日讨论最密集的条目（按评论数排序）：

1. **[#97616](https://github.com/openclaw/openclaw/issues/97616)** ｜ 30 评论 ｜ 🦪 silver shellfish
   `Runtime degradation`：OpenClaw 从 hook/tool 执行路径泄漏未回收的子进程（`openclaw-hooks`、`bash`、`codex`），僵尸进程随时间堆积在主进程下，导致运行时逐渐退化。已挂 `clawsweeper-recovery-stuck` 标签，说明自动恢复流程本身也卡住了。
   → **诉求**：长期运行的守护

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目日报 · 2026-09-17

---

## 1. 今日速览

Hermes Agent 今日维持**高活跃度**：过去 24 小时 Issues 更新 500 条（新开/活跃 241、关闭 259），PR 更新 500 条（待合并 313、合并/关闭 187），关闭量与新增量接近 1:1，说明维护团队在高速清理积压的同时仍持续接收新报告。核心开发者 @teknium1 今日主导了一轮 **Bot Mode / Group Chat 批量修复与功能落地**（至少 6 个 PR 集中在同一功能域），并有 **P0/P1 级修复**（#113619 图像驱逐保缓存、#111942 CLI 崩溃、#112522 update ImportError）当日关闭或在途。整体健康度评估：**活跃、修复导向，但待合并 PR 池（313）偏高，Bot Mode 火车式合并已出现一次 main typecheck 变红（#113621）**，提示合并节奏需要更严的 CI 门控。

---

## 2. 版本发布

今日**无新版本发布**（0 个），无 Releases 内容可分析。当前主线版本停留在 v0.21.3（2026.9.14），大量修复以合并 PR 形式堆积，预计下一版本将是一次较大的 patch 汇总。

---

## 3. 项目进展

今日合并/关闭的 187 个 PR 中，以下为高信号项：

### Bot Mode 集中推进（@teknium1 主导的功能火车）
| PR | 状态 | 内容 | 链接 |
|---|---|---|---|
| #113409 | OPEN | 群聊房间 `@mentions` 渲染为内联引用，Bot 消息带 "Reply to @handle" | https://github.com/NousResearch/hermes-agent/pull/113409 |
| #113416 | OPEN | 群聊输入框随长 prompt 自增行高 | https://github.com/NousResearch/hermes-agent/pull/113416 |
| #113410 | OPEN | `message_agent` 解析友好名 / Desktop `@`-slug，修复 DM 被 `profiles/default/` 劫持 | https://github.com/NousResearch/hermes-agent/pull/113410 |
| #113401 | OPEN | 仅有 1 个本地 Bot + 远程 Bot 时也可新建群聊 | https://github.com/NousResearch/hermes-agent/pull/113401 |
| #113382 | OPEN | 群聊成员按所属连接与 profile 正确标注标题/头像 | https://github.com/NousResearch/hermes-agent/pull/113382 |
| #113183 | CLOSED | Bot DM 瞬时失败重试且仅投递一次 | https://github.com/NousResearch/hermes-agent/pull/113183 |

### 架构级推进
- **#106742（OPEN，P1）"One gateway owns every local session"**：让 CLI、TUI、Desktop、API、ACP、bots、cron 全部挂载到同一个 gateway 拥有的会话，而非在同一 `state.db` 上各自跑 agent。这是今日最重要的架构 RFC/实现，直接对应多起会话状态类 bug（#46303、#109966）。
  https://github.com/NousResearch/hermes-agent/pull/106742

### 稳定性修复（已关闭）
- #113194 压缩后 `skill_view`/`read_file` 结果可重新加载，`/compress` 重置会话去重。
- #113191 计划心跳 `NO_REPLY`/`[SILENT]` 不再刷警告气泡。
- #113189 后台/回合外辅助调用保留 OpenCode session header，避免回退到付费路由。
- #113184 `HERMES_DEBUG_INTERRUPT=0/false/off` 不再误开启调试。
- #113185 STT helper 失败报真实错误而非 `AttributeError`。
- #113621 紧急修复 main 分支 desktop typecheck 变红（`onNewSection` 缺失）。

**推进幅度评估**：项目在 **Bot Mode 可用性** 与 **多会话/gateway 统一** 两个方向上明显前进；但 313 个待合并 PR 的池子意味着合并吞吐仍需提升。

---

## 4. 社区热点

### 讨论最活跃 Issues（按评论数）

1. **#88584 [OPEN] Automated Nous integration is blocked** — 108 评论
   `cron/jobs.py` 冲突导致 Nous→Enterkey 定时合并被阻塞。**诉求**：这是一条自动化流水线故障，长期 108 条评论无 👍，说明是维护者/机器人之间的长链对话，非社区热度。
   https://github.com/NousResearch/hermes-agent/issues/88584

2. **#110912 [CLOSED] Nous Portal 折扣路由 bug** — 20 评论，👍 1
   订阅额度耗尽后日账单飙升约 3 倍，`glm/glm-flash/kimi` 路由被按全价计费。**诉求**：计费透明度与折扣路由正确性，已关闭，属高优先级收入/信任问题。
   https://github.com/NousResearch/hermes-agent/issues/110912

3. **#103483 [OPEN] muse-spark 回合中途结束** — 16 评论，👍 11（今日最高反应数）
   Responses wire 下 `finish_reason=stop` 却输出一个不相关的单词截断。**诉求**：流式响应完整性与 provider 适配，11 个 👍 表明这是较广的用户体感问题。
   https://github.com/NousResearch/hermes-agent/issues/103483

4. **#107402 [OPEN] `hermes update` 永久警告** — 19 评论
   延迟重启 gateway 后留下 `state: stale` 与 `fleet_restart` 警告。
   https://github.com/NousResearch/hermes-agent/issues/107402

5. **#112639 [OPEN] RFC: script-speed computer use** — 12 评论，作者 @kvnloo
   语义状态 + runahead 执行 + autoresearch 的计算机使用提速 RFC；结合 #111237 "Self-tuning harness"，@kvnloo 正在系统性提出**自进化/低延迟**路线。
   https://github.com/NousResearch/hermes-agent/issues/112639

### 讨论最活跃 PR
- **#106742**（gateway 统一）与 Bot Mode 系列 PR 均于 09-17 持续更新，评论数在数据中为 `undefined`（API 未返回），但更新频率显示其为当前审查焦点。

---

## 5. Bug 与稳定性

按严重程度排列：

| 级别 | Issue | 状态 | 描述 | 是否有 fix PR |
|---|---|---|---|---|
| **P0** | #113619 | OPEN | agent 未在 provider 图像上限处驱逐图像，破坏 prompt-cache 前缀；@teknium1 P0 follow-through | 本身即 PR（作者 @JoaoMarcos44） https://github.com/NousResearch/hermes-agent/pull/113619 |
| **P0** | #111942 | CLOSED | CLI 启动即崩 `NameError: file_signature`（#111408 回归） | 已修复关闭 https://github.com/NousResearch/hermes-agent/issues/111942 |
| **P1** | #112522 | CLOSED | `hermes update` 期间 `ImportError: file_signature`，atexit 再次触发 | 已修复关闭 https://github.com/NousResearch/hermes-agent/issues/112522 |
| **P1** | #110912 | CLOSED | Nous Portal 折扣路由失效，账单 3 倍 | 已关闭 https://github.com/NousResearch/hermes-agent/issues/110912 |
| **P1** | #107402 | OPEN | `hermes update` 延迟重启后永久 stale 警告 | 待修复 https://github.com/NousResearch/hermes-agent/issues/107402 |
| **P1** | #103483 | OPEN | muse-spark 回合中途截断（Responses wire） | 待修复 https://github.com/NousResearch/hermes-agent/issues/103483 |
| **P1** | #80449 | OPEN | Compressor 保留超大单轮，token 预算被击穿 | 待修复 https://github.com/NousResearch/hermes-agent/issues/80449 |
| **P2** | #109966 | OPEN | state.db WAL 交接导致长持有者阻塞新 opener 数小时（reporter 已证实 #109841/#110544 修掉主链） | 部分修复 https://github.com/NousResearch/hermes-agent/issues/109966 |
| **P2** | #101007 | OPEN | `mcp_servers.<name>.lazy` 永不生效（`ttl_ms: 0` 被视为过期） | 待修复 https://github.com/NousResearch/hermes-agent/issues/101007 |
| **P2** | #46303 | OPEN | 并发会话交叉污染（共享 memory 注入 + 共享 git worktree） | 部分由 #106742 覆盖 https://github.com/NousResearch/hermes-agent/issues/46303 |
| **P2** | #95459 | OPEN | Desktop 内置浏览器重启后拒绝 agent 操作（`isActiveEvent` false） | 待修复 https://github.com/NousResearch/hermes-agent/issues/95459 |
| **P2** | #86565 | OPEN | Desktop 会话状态点在等待审批时仍显示蓝色 | 待修复 https://github.com/NousResearch/hermes-agent/issues/86565 |
| **P2** | #92352 | OPEN | 切换本地/远程 gateway 后会话列表不刷新 | 待修复 https://github.com/NousResearch/hermes-agent/issues/92352 |
| **P2** | #86207 | OPEN | systemd 托管 dashboard 更新后跑旧代码，`/api/model/options` 500 | 待修复 https://github.com/NousResearch/hermes-agent/issues/86207 |
| **P2** | #108575 | OPEN | `profile create --clone` 未继承 `agent.max_turns`，克隆 profile 只有 4 回合预算 | 待修复 https://github.com/NousResearch/hermes-agent/issues/108575 |
| **P3** | #97065 | OPEN | Keet gateway setup 崩溃 `TypeError` | 待修复 https://github.com/NousResearch/hermes-agent/issues/97065 |
| **P3** | #45983 | OPEN | 技能密集型 orchestrator profile 约 19 回合后 chatloop | 待修复 https://github.com/NousResearch/hermes-agent/issues/45983 |
| **P3** | #112879 | OPEN | Desktop Memory tab 404 `Plugin not found` | 待修复 https://github.com/NousResearch/hermes-agent/issues/112879 |
| **P2** | #47954 | OPEN | honcho memory provider 启动竞态警告 | 待修复 https://github.com/NousResearch/hermes-agent/issues/47954 |

**趋势**：更新/安装链路（#107402、#112522、#86207、#113177）是今日最集中的稳定性风险域，涉及"更新后仍跑旧代码/丢失惰性后端"一类问题，建议维护者系统性收敛。

---

## 6. 功能请求与路线图信号

| 需求 | 提出者 | 已有关联 PR | 纳入下一版本可能性 |
|---|---|---|---|
| **单 gateway 拥有所有本地会话**（CLI/TUI/Desktop/API/ACP/bot/cron 统一） | @teknium1 #106742 | 是，P1 且持续更新 | **高**——已是实现中的 P1 主线 |
| **script-speed computer use**（语义状态 + runahead + autoresearch） | @kvnloo #112639 | 无直接 PR | 低-中——属 RFC 阶段，需设计决策 |
| **Self-tuning harness**（本地隔夜 evolver，仅保留统计显著 tweak） | @kvnloo #111237 | 无 | 低-中——与 #111189/#111200 构成系列，方向清晰但工程量大 |
| **MCP lazy 加载真正生效** | @Summer9212 #101007 | 无（但 #103760 修 MCP keepalive） | 中——小范围 bug-fix 性质 |
| **MCP/connector/plugin 工具调用显示参数预览** | @teknium1 #113614（gemini-cli#29341 移植） | 是 | **高**——PR 已开 |
| **Codex picker 移除已退役 gpt-5.4 / 5.4-mini** | @teknium1 #113615（cline#14011 移植） | 是 | **高**——PR 已开 |
| **Desktop Memory tab provider 配置** | @vidaunited #112879 | 无 | 中——需先修 404 根因 |
| **profile multiplexing 作为唯一 gateway 模式** | @teknium1 #109417 | 与 #106742 呼应 | **高**——tracking issue 已建 |

**信号总结**：路线图重心正从"多 surface 各自为政"转向 **gateway 统一 + profile 多路复用**；同时 @teknium1 大量"移植上游项目修复"（cline、gemini-cli）显示团队在主动吸收外部生态经验。

---

## 7. 用户反馈摘要

**痛点**
- **计费信任**：#110912 订阅额度耗尽后被按全价计费、日支出 3 倍，用户对折扣路由与账单透明度高度敏感（👍 1，20 评论）。
- **更新链路不可靠**：#107402、#86207、#112522、#113177 集中反映 `hermes update` 后的陈旧进程、stale 状态与惰性后端丢失，用户需要"更新完就能用"。
- **会话状态建模混乱**：#46303（并发会话交叉污染）、#109966（WAL 交接阻塞）、#93618/#105104（Bot 聊天不刷新、点击无响应）反映用户对"哪个会话在跟谁说话"缺乏信心。
- **Desktop 状态指示失真**：#86565（等待审批仍显示蓝色）、#92352（切换 gateway 会话列表不刷新）影响日常可用性。
- **profile 克隆陷阱**：#108575 克隆 profile 只有 4 回合预算，Kanban 调度直接失败，属"静默错误配置"。

**满意点**
- 修复响应快：P0 CLI 崩溃 #111942、update ImportError #112522 均当日关闭；Bot Mode 系列在同一天内批量落地。
- 上游移植（cline、gemini-cli）让用户较快获得其他生态已验证的体验改进。

**使用场景观察**
- 技能密集型 orchestrator（247 skills / 2.8 MB 上下文，见 #45983）、Kanban 调度、Desktop Bot Mode 群聊、SSH 远程 gateway（#95532）是主要实际负载，也是 bug 高发区。

---

## 8. 待处理积压

以下为长期未关闭、且影响面较大的项目，建议维护者优先排期：

| 项目 | 创建 | 悬置时长 | 为什么值得关注 |
|---|---|---|---|
| #45983 技能密集型

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目日报 · 2026-09-17

---

## 1. 今日速览

- **整体活跃度：极高。** 24 小时内 Issues 更新 106 条（新开/活跃 85、关闭 21），PR 更新 348 条（待合并 190、已合并/关闭 158），是典型的高吞吐维护节奏。
- **主线工程推进显著：** OTel/Langfuse v2 可观测性、Router 策略开关、Vertex AI 批量文件流式下载、ChatGPT OAuth 透传、A2A/Foundry 接入等多条并行推进。
- **集中"清库"信号明显：** 今日关闭的 Issue 中大量带有 `stale` 标签（多为 6 月提交），说明 stale bot 正在批量清理 90 天未响应项——健康度改善，但部分真实 Bug 被"埋掉"的风险需警惕。
- **发布节奏处于候选/开发阶段：** 无正式 release，仅有 v1.103.0-dev.1 与 v1.102.0-rc.2，未附变更说明。
- **高优先级风险项：** 速率限制双重计数（#34140）、零成本预算绕过/被误拦（#38515、#41344）、流式 usage 丢失导致计费偏高（#36168）等涉及**计费与配额正确性**的问题仍是社区核心关切。

---

## 2. 版本发布

今日共发布 2 个版本，但**均为签名验证模板内容，未附带实质性 changelog**，无法给出破坏性变更与迁移说明。

| 版本 | 类型 | 说明 |
|---|---|---|
| [v1.103.0-dev.1](https://github.com/BerriAI/litellm/releases) | 开发版（dev） | 内容仅含 Docker 镜像 cosign 签名验证说明，签名密钥沿用 [commit `0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0) |
| [v1.102.0-rc.2](https://github.com/BerriAI/litellm/releases) | 候选版（rc） | 同上，签名验证说明 |

**分析师提示：**
- `v1.103.0-dev.1` 为下一 minor 的开发分支起点，`v1.102.0-rc.2` 是候选版第二轮，**v1.102.0 正式版临近**，建议关注 rc 到 GA 之间的回归修复。
- 签名验证流程已标准化（cosign + 固定密钥），供应链安全实践**稳定无变更**。
- **建议维护者：** 为 rc/dev 版本补充变更摘要，否则下游无法评估升级风险——这已是连续多版发布模板化的问题。

---

## 3. 项目进展

今日合并/关闭侧的高价值 PR（含已关闭但结论明确者）：

**可观测性（OTel v2 / Langfuse）**
- [#35210 [CLOSED] fix(otel): map Langfuse trace user, session, name, and tags in the v2 mapper](https://github.com/BerriAI/litellm/pull/35210) — 修复 OTel v2 mapper 丢失 trace user/session/name/tags 的回归，引入 `RequestAnnotations` 类型，将 `user.id`、`session.id`、tags 打回 span。
- [#41140 [OPEN] fix(otel v2): map the caller's Langfuse user, session and tags onto the root and generation spans](https://github.com/BerriAI/litellm/pull/41140) — 是 #35210 的接续/补齐版本，修复 `langfuse_otel` 丢失 `trace_user_id`、`session_id`、`tags` 及对应 proxy header。

> **判断：** 这是同一问题的两轮修复（#35210 关闭后由 #41140 重开补齐），说明前一轮修复未完全覆盖 caller 透传路径。可观测性链路是当前团队投入最集中的方向之一。

**CI / 工程效率**
- [#41494 [CLOSED] ci: auto-merge provider-info-sync PRs when CI, Greptile and Bugbot are clean](https://github.com/BerriAI/litellm/pull/41494) — 新增 `auto-merge-price-sync` workflow，对 provider 价格同步 PR（`berriai-litellm-provider-info-sync[bot]`）在 CI + Greptile + Bugbot 全绿时自动合并。**这是明显的维护成本削减举措。**

**关联关闭的 Issue（问题闭环）**
- [#11359 Add cost tracking when using bedrock passthrough](https://github.com/BerriAI/litellm/issues/11359)（👍10）— Bedrock 直通模式下的成本追踪终于闭环。
- [#36759 gen_ai.system 仍以 'None' 到达 OTel exporter](https://github.com/BerriAI/litellm/issues/36759) — 修复了 #26713 只覆盖 span-attribute 调用点的遗漏。
- [#41344 零成本预算绕过在 fallback 到付费模型时泄漏无界支出](https://github.com/BerriAI/litellm/issues/41344) — 提交次日即关闭，响应速度极快。
- [#40735 bedrock_converse 拒绝携带 tool-call 历史但无 tools 数组的后续轮次](https://github.com/BerriAI/litellm/issues/40735)、[#24158 Bedrock 无 tools= 时误抛 UnsupportedParamsError](https://github.com/BerriAI/litellm/issues/24158) — Bedrock 工具调用兼容性批量收敛。

**整体推进量评估：** 158 条 PR 关闭 + 21 条 Issue 关闭，但其中相当比例为 stale 清理。**实际功能性净推进约在"中高"档位**：可观测性、CI 自动化、Bedrock 兼容性三条线最清晰。

---

## 4. 社区热点

按评论数与 👍 排序的 Top 讨论：

**① [#8328 [OPEN] [bug] Key alias 在所有用户间唯一](https://github.com/BerriAI/litellm/issues/8328) — 16 评论｜👍2｜存活 19 个月**
- 现象：用户 A 创建的 key alias，用户 B 无法复用；用户期望 alias 是用户内命名空间隔离的。
- 关联 [#2932](https://github.com/BerriAI/litellm/issues/2932)。
- **诉求：** 多租户场景下 alias 应做 per-user 唯一，而非全局唯一。这是一条**长期未决的数据模型类争议**，涉及既有用户迁移，修复成本高。

**② [#14398 [OPEN] [Feature] 每日请求/Token 速率限制](https://github.com/BerriAI/litellm/issues/14398) — 13 评论｜👍9**
- 现状仅支持 per-minute RPM/TPM；用户需要 RPD/TPD。
- 动机直接：OpenAI 免费/Pro 层给的是 1M GPT-…/天 这类日限，proxy 无法对齐上游配额。
- **诉求强烈（👍9），是本次清单中点赞第二高的开放 Issue。**

**③ [#11359 [CLOSED] Bedrock passthrough 成本追踪](https://github.com/BerriAI/litellm/issues/11359) — 13 评论｜👍10｜已闭环**
- 场景非常有代表性：用 Claude Code + LiteLLM + Bedrock，正常 chat 可用，但只能走 passthrough 才能跑通，代价是**失去成本追踪**。

**④ [#34140 [OPEN] v3 限流器对 team per-model 限额重复计数](https://github.com/BerriAI/litellm/issues/34140) — 8 评论**
- `POST /team/update {metadata:{model_rpm_limit:{...}}}` 配置 N，实际约 N/2 就返回 429，**有效配额被砍半**。
- 报告者提供了明确 repro + root cause，属于可直接排期的高质量报告。

**⑤ [#20962 [OPEN] 非管理员用户无法创建 API Key：UI 要求选 team，API 却禁止指定 team_id](https://github.com/BerriAI/litellm/issues/20962) — 6 评论｜👍6**
- `internal_user` 角色被 UI 与 API 的双重约束卡死，形成**完全不可用路径**。这是 UX 与权限模型冲突的经典案例。

**[#27830 [OPEN] 为自托管 vLLM/OpenAI-like 模型自动填充 max_input/output_tokens](https://github.com/BerriAI/litellm/issues/27830) — 👍12，为本次清单最高赞**
- 虽仅 2 条评论，但**赞数最高**，属"沉默多数"型强需求。已有对应 PR [#41508](https://github.com/BerriAI/litellm/pull/41508) 提出实现路径（见第 6 节）。

---

## 5. Bug 与稳定性

按严重程度排序（🔴 计费/配额正确性 > 🟠 功能不可用 > 🟡 数据展示/边缘场景）：

### 🔴 高危：计费与配额正确性

| Issue | 现象 | Fix PR | 状态 |
|---|---|---|---|
| [#34140](https://github.com/BerriAI/litellm/issues/34140) | v3 限流器 `model_per_team` 重复计数，有效 RPM/TPM 仅为配置值一半 | 未在今日 PR 列表中见到 | OPEN，8 评论，含 root cause |
| [#36168](https://github.com/BerriAI/litellm/issues/36168) | 流式响应在上游 final chunk 带非空 `choices` 时丢弃 `usage`，导致 cached_tokens 丢失、按全价计费 | 未见 | OPEN，👍1 |
| [#40095](https://github.com/BerriAI/litellm/issues/40095) | 自定义认证下，未知 end user 的并发首请求绕过默认预算 | 未见 | OPEN |
| [#38515](https://github.com/BerriAI/litellm/issues/38515) | 个人 `max_budget` 耗尽后，零成本模型被一并拦截（auth 层实现缺陷） | 未见 | OPEN |
| [#41344](https://github.com/BerriAI/litellm/issues/41344) | 零成本预算绕过基于"请求的"模型组判断，fallback 到付费部署后绕开预算 | — | **CLOSED（提交次日关闭，未附 PR 链接）** |

> ⚠️ **重点提示：** #41344 与 #38515 是同一"零成本预算"逻辑的两面——前者是**放行过多（漏计费）**，后者是**拦截过多（误伤）**。前者已在 24 小时内关闭，后者仍开放且无进展。建议维护者确认两者的修复是否互斥或需统一重构。

### 🟠 中危：功能不可用 / 连接中断

| Issue | 现象 | 状态 |
|---|---|---|
| [#38223](https://github.com/BerriAI/litellm/issues/38223) | Gemini/Vertex 拒绝工具结果中含 JSON Schema `$ref`/`$defs` 的后续请求 | OPEN |
| [#31562](https://github.com

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*