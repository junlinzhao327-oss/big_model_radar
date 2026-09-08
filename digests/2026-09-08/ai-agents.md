# OpenClaw 生态日报 2026-09-08

> Issues: 488 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-08 00:30 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-09-08

> 数据来源：github.com/openclaw/openclaw | 统计区间：过去24小时

---

## 1. 今日速览

过去24小时项目活跃度**极高**：488条Issue更新（新开/活跃241，关闭247）与500条PR更新（待合并270，合并/关闭230）双双刷新近期高位，显示社区反馈与修复工作均处于密集期。然而**今日无新版本发布**（上一版本为2026.9.2），且大量高优Bug仍在等待维护者处理与修复PR，项目健康度呈"**高活跃、高积压**"态势——核心痛点集中在：会话/转录数据一致性、SQLite/事件循环阻塞、子进程泄漏，以及多智能体编排不稳定性。社区侧，`steipete` 等核心维护者今日集中提交了一批重构型PR（transcripts/cron/doctor资源释放等），表明项目正在为深层架构调整做准备。

---

## 3. 项目进展

今日没有新版本发布，但PR活动频繁，共有230条PR进入合并/关闭流程。值得关注的已合并/关闭PR（及其关联修复方向）：

- **#141620** [CLOSED] fix(btw): report usage for direct-provider answers — 修复直接 `/btw` 回答的用量缺失问题，该路径此前不向模型诊断和可选回复用量上报数据。
  🔗 https://github.com/openclaw/openclaw/pull/141620
- **#141674** [CLOSED] fix(media): avoid false empty-body download diagnostics — 区分"源端确实发送了字节但被适配器丢弃"与"真正的空响应"，消除误导性错误报告（关闭 #141667）。
  🔗 https://github.com/openclaw/openclaw/pull/141674
- **#135970** [CLOSED] codex 插件 dist/extensions/codex 缺少 node_modules（Managed Codex app-server binary not found）— 该修复解决了 `openclaw` 系统工具通过 Codex app-server 后端无法完成推理的问题。
  🔗 https://github.com/openclaw/openclaw/issues/135970

**架构演进信号**：维护者 `steipete` 今日集中提交了多个 refactor PR（transcripts summary 持久化与采集分离 #141695、cron 结果解析抽取 #141688、doctor 插件资源释放 #141692、Kova auth fixture 去冗余等待 #141693），这些多为后续大变更（资源生命周期管理，#140674 相关）铺路的小步重构。另有 **#141451**（gateway 启动被拒时保留状态）、**#140339**（checkpoint 与中断更新恢复）两个大型PR处于待维护者审查状态，若合并将分别提升升级安全性和更新中断恢复能力。

---

## 4. 社区热点

今日讨论最热烈（按评论数排序）的 Issue 揭示了用户最关切的三大主题：**升级回归、多智能体不可靠、会话状态泄漏**。

### 4.1 升级回归之痛 — 用户对版本质量敏感度上升

- **#135111**（17条评论）[P1/回归] v2026.8.1 间歇性报错 `Provider completed tool call with malformed JSON arguments`（claude-sonnet-5），约出现6次，无法绑定到具体文件/工具。用户从 v2026.7.1-2 升级后开始遇到，目前**无fix PR**。
  🔗 https://github.com/openclaw/openclaw/issues/135111
- **#136183**（10条评论）[P1/回归] 2026.8.1 起，命令执行器在 spawn ssh 时挂起——客户端已发送版本字符串但服务器 banner 永不返回，直至被 SIGTERM 杀死，8.2 中仍存在。**无fix PR**。
  🔗 https://github.com/openclaw/openclaw/issues/136183
- **#139578**（8条评论）[P1/回归] llama.cpp 托管的 EmbeddingGemma 在 2026.9.2 中回退到服务器默认 ubatch 512（此前 #134389 已修复）。**需要 live 复现**。
  🔗 https://github.com/openclaw/openclaw/issues/139578

### 4.2 多智能体与并发控制 — 最持久的社区痛点

- **#126360**（16条评论）[P1] 显式多智能体所有权下 `AgentSelectionRequiredError` 刷屏日志：logbook 插件、Control UI 全局 RPC、system-agent turns 均缺少 agentId 目标。
  🔗 https://github.com/openclaw/openclaw/issues/126360
- **#43367**（14条评论）[P1] 长期未解决的多智能体编排问题：并发 `agents add` 配置互相覆盖、session-lock 失败、子任务游离。3月11日创建至今仍**无fix PR**。
  🔗 https://github.com/openclaw/openclaw/issues/43367
- **#137332**（6条评论）[P1] requester-settle 批次在 ownership check 后可能永远重试（涉及 failed/timed-out/cancelled/orphaned 子代理运行）。**已有 queueable-fix 标记**。
  🔗 https://github.com/openclaw/openclaw/issues/137332

### 4.3 沉默的消息丢失 — 信任度杀手

- **#97616**（15条评论）[P1/回归] hook/tool 子进程未被收割，zombie 进程持续累积导致运行时性能劣化（openclaw-hooks、bash、codex 等）。该 Issue 已开放超两个月（6月29日创建），仍**无fix PR**。
  🔗 https://github.com/openclaw/openclaw/issues/97616
- **#125764**（6条评论）[P1] Telegram 适配器出站消息在网络失败后仅尝试一次即永久死信，announce/完成回复静默丢失，无重试、无告警。
  🔗 https://github.com/openclaw/openclaw/issues/125764

### 4.4 高赞但被关闭的需求 — 社区知情权

- **#79077**（15条评论，👍8）Telegram 2026-05-07 发布的 guest bots 与 bot-to-bot 通信支持请求被标记为 stale 后关闭。虽然关闭，但它代表了渠道适配器紧跟上游平台功能的真实诉求。**同类问题可能再次涌现**。
  🔗 https://github.com/openclaw/openclaw/issues/79077
- **#78963**（7条评论，👍1）WhatsApp listen-only / hooks-only 模式同样因 stale 关闭。用户需要仅通过 hook 接收消息做归档/ETL，**不触发 agent 运行或产生外呼流量**。
  🔗 https://github.com/openclaw/openclaw/issues/78963

---

## 5. Bug 与稳定性

### 5.1 P0 级别（发布阻断/崩溃级）— 共5个

| Issue | 概述 | Fix PR 状态 |
|---|---|---|
| [#89278](https://github.com/openclaw/openclaw/issues/89278) | [P0/回归] Codex OAuth 刷新成功但 cron/heartbeat 因 10s 超时失败 | 有linked PR |
| [#140497](https://github.com/openclaw/openclaw/issues/140497) | [P0] Discord 设置接受 application ID 作为 bot token，标记为已配置但永不启动 | 无 |
| [#138965](https://github.com/openclaw/openclaw/issues/138965) | [P0] 中断的 transcript rewrite 使过期分支成为活动会话 | 无 |
| [#140908](https://github.com/openclaw/openclaw/issues/140908) | [P0] doctor --fix 在 systemd --user 服务账户下 EACCES，阻塞所有升级后迁移 | 无 |
| [#140620](https://github.com/openclaw/openclaw/issues/140620) | [P0] 2026.7.1-2 → 2026.9.2 就地升级：27/~1500 会话导入后停住，升级前会话不可搜索 | 无 |
| [#106920](https://github.com/openclaw/openclaw/issues/106920) | [P0/回归] 2026.7.1 无法重启 gateway | 无（已关闭但值得关注） |

### 5.2 P1 高优先级热点（按今日评论热度）

- **#115908**（16条评论）— 会话转录投影重建在持续写入下不收敛，同步代码块占用 Node 主线程数十秒，拖垮所有渠道传输。
  🔗 https://github.com/openclaw/openclaw/issues/115908
- **#119720**（13条评论）— 同步 agent 持久化与转录维护在大规模下阻塞 Gateway 事件循环（planner-statistics 部分已修复，剩余 Gateway 线程问题仍在）。
  🔗 https://github.com/openclaw/openclaw/issues/119720
- **#117262**（9条评论）— SQLite 三并发写句柄导致 ~33s 事件循环停顿（DEF-61）。
  🔗 https://github.com/openclaw/openclaw/issues/117262
- **#137927**（8条评论，今日关闭）— `<BEGIN_OPENCLAW_INTERNAL_CONTEXT>` 内部上下文泄漏为 Telegram 可见文本 — **属于严重安全/隐私边界问题，今日已关闭**。
  🔗 https://github.com/openclaw/openclaw/issues/137927
- **#140535**（7条评论，今日关闭）— Discord `/new` 返回 "No reply was generated" 且不重置会话。
  🔗 https://github.com/openclaw/openclaw/issues/140535
- **#137613**（8条评论）— CLI 后端上 compaction 前内存 flush 被禁用，导致会话笔记在上下文压缩前从未落盘。
  🔗 https://github.com/openclaw/openclaw/issues/137613

### 5.3 稳定性趋势分析

今日数据中**与 SQLite/事件循环/转录一致性相关的 P0/P1 数量最多**，且大量标记 `source-repro` 与 `needs-maintainer-review`。从关联PR（#137381 sessions_yield history 保持、#130706 gateway 多工作区 stall 修复）来看，维护者正着手系统性地解决存储与会话层问题，但修复落地速度仍落后于用户报告速度。

---

## 6. 功能请求与路线图信号

### 6.1 可能进入下一版本的方向

- **#139714**（10条评论）update command 残留 `update_runs` 行导致 `openclaw status` 永远显示 "update in progress"。关联大型PR **#140339**（checkpoint + 中断恢复）已在维护者审查中，该 PR 有望系统性解决此类更新一致性问题。
  🔗 https://github.com/openclaw/openclaw/issues/139714 | 🔗 https://github.com/openclaw/openclaw/pull/140339
- **#137381** [PR open] `sessions_yield` 在长 SQLite 会话中保持转录历史可用 — 直接回应 #109638/#113190 的长期诉求，正在解决 yield 过程中历史暂时不可见的问题。
  🔗 https://github.com/openclaw/openclaw/pull/137381
- **#141121** [PR open] Control UI 在 Gateway 连接前从缓存渲染侧边栏与聊天 — 显著改善 UI 加载体验。
  🔗 https://github.com/openclaw/openclaw/pull/141121

### 6.2 高票功能建议

- **#126781**（5条评论）[P3] Detached managed Lobster runs after tool return — 评论指出 2026.9.1 已通过 `/loop` 与 TaskFlow 覆盖大部分需求，但可能仍需原生任务锚定支持。
  🔗 https://github.com/openclaw/openclaw/issues/126781
- **#141472**（4条评论）[P2] Workboard 卡片笔记与操作者评论中的 URL/Markdown 链接应可点击。
  🔗 https://github.com/openclaw/openclaw/issues/141472
- **#45503**（4条评论，👍2）[P3] 为工具结果提供手动上下文清理，而非仅依赖 TTL 自动裁剪。用户场景：大型工具结果（邮件、搜索结果）只在当下有用。
  🔗 https://github.com/openclaw/openclaw/issues/45503

### 6.3 值得注意：Telegram/WhatsApp 新功能支持双双因 stale 关闭

#79077（Telegram guest/bot-to-bot）与 #78963（WhatsApp hook-only 模式）虽被关闭，但需求真实存在——若社区呼声持续，建议维护者以正式 roadmap 项目或 reopen 方式重新评估。

---

## 7. 用户反馈摘要

- **升级即回归的挫败感**："Since upgrading from v2026.7.1-2 to v2026.8.1, agent runs intermittently fail"（#135111）；ssh 执行器

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-09-08

## 1. 今日速览

过去 24 小时项目活跃度处于**中高水平**，但形态上以“清理 + 修复”为主：61 条 Issue 更新中 48 条关闭（约占 79%），27 条 PR 更新中 17 条已合入或关闭，另有 10 条 PR 在等待合并。最值得关注的是 **Copilot GPT-6 Astra 路由错误**（#9209/#9277）在一天之内完成了报告、修复到合入的全流程（#9253）；与此同时，**x-opencode-session 请求头事件**（opencode.ai 自 2026-09-06 开始强制校验）引发了至少 4 个相关 Issue（#9290/#9237/#9230/#9298），是当前最集中的外部兼容性风险点。本次无新版本发布。长期热点 #4945（openai-codex 连接可靠性）持续占据最高讨论量，仍是项目最严重的稳定性短板。


## 2. 版本发布

过去 24 小时无新版本发布，当前最新版本停留在 0.85.1（社区 Issue 中提及）。


## 3. 项目进展

今日合入/关闭的 PR 中，以下对项目健康度有实质推进：

- **修复 GitHub Copilot GPT-6 Astra 路由错误**（[#9253](https://github.com/earendil-works/pi/pull/9253) — `petrroll`）：将 Copilot GPT 系列模型从 Chat Completions 端点切换到 Responses 端点，修复了 #9209 中 `gpt-6-astra` 被 `/chat/completions` 拒绝（400）的问题。该 PR 从 Issue 报告到合入在一天内完成，效率较高。
- **修复 Claude Fable 5 无效回退目标**（[#9297](https://github.com/earendil-works/pi/pull/9297) — `petrroll`，状态 OPEN）：移除被 API 拒绝的 `claude-opus-4-8` 内置回退模型，仅保留 Opus 5，并对回退元数据和 API-key/OAuth payload 补充覆盖。截至目前仍待合并，对应 Issue #9294 已关闭。
- **新增 Docker Sandboxes 文档**（[#9077](https://github.com/earendil-works/pi/pull/9077) — `mdelapenya`）：在 `containerization.md` 中补齐 Docker Sandbox 运行方式，关闭 #8788。对容器化部署场景的文档完善是实质补齐。
- **仓库链接统一 pi-mono → pi**（[#9278](https://github.com/earendil-works/pi/pull/9278) — `rwachtler`）：修正了 prompt 模板、注释、文档中过期仓库引用，降低新用户困惑。

其余关闭的 PR 中，部分为较长周期的社区贡献（如 #256 XDG Base Directory 支持、#5732 `allowCommands` 选项、#9 AGENTS.md 支持），今日由维护者或作者关闭，但具体合并状态不明确，暂不作“已合并功能”的确定性结论。


## 4. 社区热点

- **[#4945 openai-codex Connection Reliability Issues](https://github.com/earendil-works/pi/issues/4945)** — **77 条评论，33 👍，OPEN/INPROGRESS** | 今日数据中热度断层第一的 Issue。问题表现为 TUI 反复卡在 `Working...`，无流式输出、无工具调用、无错误提示，用户唯一能做的就是按 Esc 放弃整轮对话。自 2026-05-24 创建至今近三个半月仍未定论，已从“偶发”演变为社区公认的稳定性痛点。该问题横跨连接管理、流式解析、超时处理、TUI 状态同步多条链路，修复成本较高，但**不修复的代价是持续的用户流失**。

- **[#7547 Windows 使用情况调查](https://github.com/earendil-works/pi/issues/7547)** — **61 条评论，OPEN** | 这是一次有组织的社区调研。维护者正在系统性收集 Windows 用户的使用方式和遇到的问题，目的是确定核心团队应该集中精力支持哪条运行路径（原生、WSL、Docker、MSYS2 等），还是将非主流路径移交给社区扩展维护。这条 Issue 的高关注度从侧面表明 Windows 开发者群体规模可观，但 Pi 在 Windows 上的体验碎片化已成为准入门槛。


## 5. Bug 与稳定性

按严重程度排列：

**高危**

- **[grep 工具带上下文行数时可能 OOM](https://github.com/earendil-works/pi/issues/9276)**（#9276，已 CLOSED）— headless SDK 场景下进程直接因 JavaScript heap 溢出崩溃，core dump 显示堆内存被日志文件占满。grep 在 context >0 时逐个读取 match 而非流式处理。**对于将 pi-coding-agent 嵌入自有服务的用户，这是直接的服务可用性事故，建议修复后补充回归测试。**
- **[openai-codex 连接可靠性问题](https://github.com/earendil-works/pi/issues/4945)**（#4945，OPEN）— 反复出现 TUI 卡死无可恢复，当前唯一的“恢复”是放弃当前轮次。无 fix PR。持续 3.5 个月的严重问题，见“社区热点”。
- **[AgentSession settlement 生命周期缺陷](https://github.com/earendil-works/pi/issues/5886)**（#5886，OPEN）— 核心维护者 `mitsuhiko` 标记的 meta issue，涵盖“post-run 逻辑从已终止的 transcript 续跑 agent”等一系列关联缺陷。**尚未拆分出具体修复计划。**

**中危**

- **[全屏模式滚轮速度比普通模式慢 3 倍](https://github.com/earendil-works/pi/issues/9052)**（#9052，OPEN，3 👍）— 功能缺陷；用户从传统模式切换到全屏模式后滚动体验明显劣化。
- **[Bedrock 上 OpenAI 模型拒绝 toolResult 中嵌套图片](https://github.com/earendil-works/pi/issues/8643)**（#8643，OPEN）— Issue 中提到修复代码已在贡献者 fork 上就绪（原 #8642），等待合入路径。

**低危/已定位**

- **[Gemini 3.x 工具调用因缺 `thought_signature` 失败](https://github.com/earendil-works/pi/issues/6996)**（已 CLOSED）— 已有关闭记录。
- **[Grok 403 被误标为 “OpenAI API error”](https://github.com/earendil-works/pi/issues/9298)**（#9298，已 CLOSED）— 错误信息归类错误，误导用户向 OpenAI 排查，实际需要检查 Grok 订阅/credits。
- **[无法启动 0.84.1 — zstd 解压报错](https://github.com/earendil-works/pi/issues/7771)**（已 CLOSED）— Node 23 下 `zlib.createZstdDecompress` 缺失，属于运行环境兼容性问题。


## 6. 功能请求与路线图信号

x-opencode-session 头部事件暴露了 agent 生态中一个系统性问题：当外部 API 突然增加新请求头要求时，Pi 的核心层、扩展 API、社区桥接包都可能同时失效。

- **[opencode-go provider 缺少 x-opencode-session 请求头](https://github.com/earendil-works/pi/issues/9230)**（#9230，OPEN，1 👍）— 核心 provider 缺陷。上游 2026-09-06 开始强制要求，Pi 请求未携带导致报错。
- **[Extension API modelRegistry.complete() 同样缺失该请求头](https://github.com/earendil-works/pi/issues/9290)**（已 CLOSED）— 影响所有通过扩展 API 访问 opencode-go 模型的第三方开发者。
- **[社区包 pi-opencode-bridge@0.2.1 也无此请求头](https://github.com/earendil-works/pi/issues/9237)**（已 CLOSED）— Issue 作者同时请求“按 host 自动注入请求头”的核心能力。**这一请求值得维护者评估：与其让每个 provider/桥接包逐一追赶上游要求，不如在内核 HTTP 层提供可配置的请求头注入机制。**

值得关注的长期功能 PR：**Ollama Cloud 支持**（[#7742](https://github.com/earendil-works/pi/pull/7742)，OPEN，2026-08-07 提交）已搁置一个月无明确动向，该 PR 对本地+云端混合部署用户价值明确。


## 7. 用户反馈摘要

- **“连接卡死只能放弃整轮”** — #4945 中 openai-codex 用户反复报告 TUI 停留在 `Working...` 且无任何输出、无报错，按 Esc 恢复却意味着整轮对话作废。用户情绪已经从“报告 bug”转向“质疑该 provider 的可用的性”，33 个 👍 说明影响面覆盖了大量用户。

- **“Copilot 选对了模型却 400”** — #9209/#9277 表明 Pi 内置模型路由表与 GitHub Copilot 实际 API 支持不一致（`gpt-6-astra` 指向 Chat Completions 但 Copilot 仅支持 Responses）。这类问题即便修复快速，也会削弱用户对内置模型目录可靠性的信任。

- **“升级后偏好设置不再保留”** — #9273 指出自 0.84.3 起，手动选择模型或 Shift+Tab 调整推理强度的操作不再自动持久化到后续会话。有用户将其标记为 usability regression（可用性回退），并关联到 #5263 等早期 issue。

- **“全屏模式好用，但滚轮太慢”** — #9052 用户肯定了全屏模式固定输入框的价值，但 3 倍速差让长文档浏览变得难以忍受。这类“功能方向正确但细节粗糙”的反馈是产品打磨阶段的高价值信号。

- **“磁盘/目录映射撞车导致会话串号”** — #9073 揭示 `JsonlSessionRepo` 对 cwd 的编码可能产生碰撞（`tenant-a/project` 与 `tenant/a-project` 映射到同一会话目录），导致会话数据互相覆盖——多租户部署场景下的数据安全隐忧。


## 8. 待处理积压

以下问题时间跨度长、影响面大或持续无进展，建议维护者关注：

- **[#4945 openai-codex 连接可靠性](https://github.com/earendil-works/pi/issues/4945)** — 2026-05-24 创建，77 评论，33 👍，INPROGRESS 但无明确修复方案。项目健康度的最大拖累项。
- **[#5886 AgentSession settlement 生命周期 bug 合集](https://github.com/earendil-works/pi/issues/5886)** — 2026-06-18 创建，核心维护者标记，11 条讨论，暂未见拆解计划和修复 PR，建议尽快排期。
- **[#7588 / #7547 Windows 适配方向决策](https://github.com/earendil-works/pi/issues/7547)** — 2026-08-03 创建，61 条评论，调研已充分，建议尽快产出结论，明确核心支持路径。
- **[#7742 Ollama Cloud 支持 PR](https://github.com/earendil-works/pi/pull/7742)** — 2026-08-07 提交至今 1 个月无维护者反馈，若不计划合入请明确告知贡献

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-09-08

## 1. 今日速览

过去24小时内，Temporal 核心仓库保持平稳而持续的开发节奏：3 条 Issue 产生更新（全部处于开放状态），16 条 PR 处于活跃状态；无新版本发布，但 CICD 机器人已关闭 1.32.0 发布分支准备 PR（#11947），暗示下一轮版本发布临近。PR 侧仅有 2 条关闭，其余 14 条均在评审中，说明团队正处在较大规模功能整合前的集中评审期；Issue 侧讨论集中在 Schedule 年限限制、SQL 存储故障恢复、指标可观测性三个长期痛点上，社区关注度高但新增问题较少，整体项目健康度良好。

## 2. 版本发布

昨日无新版本 Release。

## 3. 项目进展

过去 24 小时合并/关闭的 PR 数量不多，但包含一个重要信号：

- **[#11947] 1.32.0: Prepare release branch**（已关闭，@temporal-cicd[bot]）— 覆盖治理文件并更新依赖，意味着 1.32.0 的发布分支已就绪，版本发布进入倒计时阶段。链接：https://github.com/temporalio/temporal/pull/11947
- **[#11347] Allow registering new task queue types at the family limit**（已关闭，@Shivs11）— 原计划允许已达 `MaxTaskQueues` 限制的 deployment version 为既有 task queue name 注册新的 task queue type，同时保留对真实新增 task queue family 的限制报错。该 PR 关闭后，作者随即于同日开出新的 [#11952](https://github.com/temporalio/temporal/pull/11952)，将方案从“放宽注册限制”调整为“在 worker deployment 层面对 task queue family 做精确快照（计数 + 序列化 Bloom filter）”，并新增 deployment workflow 更新校验器。这属于方案升级而非放弃，表明 Temporal 团队在 task queue family 治理上正收敛到一个更严格、可审计的设计。

此外，Go 工具链升级的配套修复已集中提交：**[#11929](https://github.com/temporalio/temporal/pull/11929) Update to Go 1.27.0**、[#11950](https://github.com/temporalio/temporal/pull/11950)（补漏 `go fix`）以及 [#11949](https://github.com/temporalio/temporal/pull/11949)（为 Nexus caller/child workflow 注册显式名称，规避 Go 1.27 对函数字面量命名的变更）。这三条 PR 组合说明项目正在快速跟进 Go 1.27 工具链，稳定性风险控制到位。

## 4. 社区热点

今日讨论热度集中于以下 Issue：

- **[#9383] Support configuring maxCalendarYear for Schedules beyond 2100**（评论 4 条）— 当前 `maxCalendarYear` 硬编码为 2100，用户无法编排跨越该年份的工作流或 Timer。该 Issue 自今年 2 月创建以来持续获得讨论，且已有一份对应 PR（见下节），说明这是一个真实且已被接受的长期需求。链接：https://github.com/temporalio/temporal/issues/9383

- **[#11691] SQL session refresh 导致连接池不可恢复关闭，成员心跳静默失败，集群“僵尸化”但仍上报 SERVING**（评论 2 条）— 讨论热度虽不算最高，但问题性质严重：集群已无法派发任何任务，却对外显示健康，用户对此表达了强烈担忧。comment 中关注点在于：故障恢复路径不足、错误被静默吞掉，缺乏 escalation 机制。链接：https://github.com/temporalio/temporal/issues/11691

此外 **[#6633](https://github.com/temporalio/temporal/issues/6633)**（支持 exponential/native histograms）虽仅 2 条评论，但积累了 3 个 👍，属于长期呼声较高的功能请求（详见第 6 节）。

## 5. Bug 与稳定性

按严重程度排列：

- **[严重] #11691 SQL session refresh 可使连接池不可恢复地关闭（"sql: database is closed"），成员心跳随后永久静默失败，集群僵尸化且错误上报 SERVING** — 属于存储层故障恢复缺陷，影响面为整个集群的可用性与可观测性。用户期望是：要么 SQL session refresh 能从自身引发的所有错误状态自愈，要么持续性心跳失败应升级处理（重建连接、或终止进程交由 supervisor 重启）。目前**无对应修复 PR**，建议维护者优先排查。链接：https://github.com/temporalio/temporal/issues/11691

- **[中] VersionChecker 缺少 HTTP 超时与 context 取消支持** — [#11948](https://github.com/temporalio/temporal/pull/11948) 修复此问题（对应 issue #11943），为版本检查 HTTP client 增加 10 秒默认超时，并实现 `CallWithContext`。该 PR 昨日刚提交，处于待评审状态。链接：https://github.com/temporalio/temporal/pull/11948

- **[低] Go 1.27 升级引发的 Nexus workflow 名称冲突** — Go 1.27 改变了函数字面量的标签方式，导致 caller/child workflow 均变为 `func1`。已在 [#11949](https://github.com/temporalio/temporal/pull/11949) 中通过显式命名解决，不构成运行时隐患，属工具链升级连带问题。

## 6. 功能请求与路线图信号

- **Schedule 年限上限可配置（#9383）**：`maxCalendarYear` 硬编码为 2100 被多位用户视为长期阻塞项。对应 PR **[#9396](https://github.com/temporalio/temporal/pull/9396)**（2 月提交，仍开放）尝试将 spec 校验上限提升至 9999，同时保留执行期日历搜索边界 2100 作为安全上限。该 PR 与问题已经共存超过 6 个月，可能需要 maintainer 明确决策，若被接受将进入较近的版本路线图。链接：https://github.com/temporalio/temporal/pull/9396

- **支持 exponential/native histograms（#6633）**：自托管环境因 metric series 数量过多导致监控成本高昂（用户点名 AWS CloudWatch Metrics、Grafana Cloud 按 active series 计费）。该请求已开放近两年并积累 3 个 👍，属于持续存在的可观测性成本优化诉求。目前无对应实现 PR，但考虑到 Temporal 近期有多项 telemetry 标准化工作（见 #11770），这一诉求有被后续纳入的可能。链接：https://github.com/temporalio/temporal/issues/6633

- **MySQL multi-host 与 SRV 连接支持（#11659）**：允许通过逗号分隔地址及 `tcp+srv` DNS SRV 记录配置多个 MySQL 主机，并在连接时做故障转移和只读主机感知。这是数据库高可用部署能力的重要补充，对依赖 MySQL 的 on-prem/self-hosted 用户是一大利好，整体设计已较完整，值得关注评审进展。链接：https://github.com/temporalio/temporal/pull/11659

## 7. 用户反馈摘要

从今日活跃 Issue 的评论内容来看，用户的核心情绪集中在两点：

- **对静默失败的高度不信任**：来自 #11691 的 issue 报告者 @enasikbst 明确指出了最令人不安的现象——“一个无法派发任何任务的集群，却上报为 SERVING”。用户期望的不只是修复，而是建立一条清晰的失败升级路径：要么自愈，要么让进程退出交由外部 supervisor 重启，绝不能让系统在“脑死亡”状态下继续对外宣称健康。这是对运维可观测性的强烈诉求。

- **对硬编码上限的长期不满**：#9383 的提出者强调了金融、科研等场景中超过 2100 年的调度需求，这是一个虽然小众但一旦遇到就完全无法绕过的限制。评论中的讨论方向已从“是否放开上限”转向“如何在 spec 校验安全与远期限调度之间做权衡”，说明社区对这一需求的合理性已有共识。

另 #6633 的用户表达了自托管场景下的成本敏感：大量 metric series 导致监控账单上涨，希望服务端/SDK 能输出原生直方图（native histograms），从而在不牺牲可观测性的前提下显著降低时序数据存储和计费成本。

## 8. 待处理积压

以下 Issue/PR 长期未获得维护者明确推进，建议关注：

- **[#6633] 支持 exponential/native histograms**（开放近 2 年，👍 3）— 可见需求真实、长期未得到排期回应，建议维护者给出明确意向。链接：https://github.com/temporalio/temporal/issues/6633

- **[#9396] Replace hardcoded maxCalendarYear with modified spec validation**（开放 6.5 个月）— 解决 #9383 的唯一实现 PR，至今未合并也未关闭，可能卡在方案分歧上，建议维护者尽快决策或给出修改意见。链接：https://github.com/temporalio/temporal/pull/9396

- **[#11770] Standardize Temporal telemetry for Nexus trace correlation** 与 **[#11771] Enforce JWT audience for Nexus HTTP handlers** — 均为 @stephanos 提交于 8 月 25 日、带有 `request-claude-review` 标签的安全/可观测性相关改动，搁置近两周未合并，建议 maintainer 安排评审以免错过 1.32.0 窗口。链接：https://github.com/temporalio/temporal/pull/11770 | https://github.com/temporalio/temporal/pull/11771

- **[#11691] SQL 连接池不可恢复关闭导致僵尸集群**（8 月 20 日提交，严重级别高）— 目前无对应 PR，也未看到 assignee，属于需要尽快响应的高影响 Issue。链接：https://github.com/temporalio/temporal/issues/11691

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*