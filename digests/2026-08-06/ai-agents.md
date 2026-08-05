# OpenClaw 生态日报 2026-08-06

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-05 22:36 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-06

## 1. 今日速览

过去 24 小时项目活跃度极高：累计 500 条 Issue 更新（其中新开/活跃 473 条、关闭 27 条）与 500 条 PR 更新（其中待合并 424 条、已合并/关闭 76 条），但无新版本发布。当前项目健康度呈“高活跃、高积压”状态——自动化 bot（clawsweeper）持续批量产出修复 PR（今日至少 5 个），但核心 P0/P1 级会话状态与消息投递问题仍大量滞留（如 #116201、#44925、#86519 等），且存在 1 个 P0 级数据库迁移阻断发布（#119263）。社区讨论焦点集中在消息重复发送、子代理任务静默丢失、SQLite 快照一致性等稳定性痛点上。

---

## 2. 版本发布

今日无新 Releases，`2026.7.2` 仍为当前版本线，但已出现多个针对该版本的 P0/P1 回归报告（如 #119263 的 v14→v15 迁移失败、#116022 的 /new 会话恢复异常）。建议关注下一个补丁版本对上述问题的覆盖情况。

---

## 3. 项目进展

今日共有 **76 个 PR 被合并/关闭**，但因数据样本限制，以下仅列出来自 Top 30 讨论中的关键合并项：

- **✅ [#119672 fix(skills): keep installed verdicts scoped to publisher](https://github.com/openclaw/openclaw/pull/119672)**（已关闭）— 修复 Control UI 中 ClawHub 技能安全判定被同 slug 不同发布者覆盖的问题，保障安装来源溯源的隔离性。
- **✅ [#118846 Gateway main thread saturated from boot by plugin-metadata snapshot](https://github.com/openclaw/openclaw/issues/118846)**（Issue 已关闭）— 修复网关主线程自启动起被插件元数据快照及 fs stat 占满，导致本地 RPC 在 `ws_upgrade` 阶段以 1006 退出的严重问题，属于当日完成闭环的高价值修复。
- **✅ [#106779 Issue with 2026.7.1 (llama.cpp provider)](https://github.com/openclaw/openclaw/issues/106779)**（Issue 已关闭）— 解决了本地 llama.cpp provider 在 macOS 上无法生成 parser 模板的 400 错误。
- **✅ [#44134 Google Antigravity 误封问题](https://github.com/openclaw/openclaw/issues/44134)**（Issue 已关闭）— 确认因频繁 Tool Schema 重新加载触发 Google 反滥用检测，已收敛根因并修复。
- **✅ [#45082 fix(mattermost): proactive message tool sends ignore thread context](https://github.com/openclaw/openclaw/issues/45082)**（Issue 已关闭）— 修复 Mattermost 渠道中主动消息忽略线程上下文的问题。

**值得关注的待合并高价值 PR**（推进中的修复方向）：

- [#119731 fix(agents): bound task-completion result prompts](https://github.com/openclaw/openclaw/pull/119731)（clawsweeper 自动生成，P1）— 将任务完成结果文本限制在 6,000 UTF-16 码元，避免上下文撑爆，修复 #57148。
- [#119764 fix(gateway): keep uncommitted generated media while its session run is live](https://github.com/openclaw/openclaw/pull/119764)（P1，proof sufficient）— 修复生成的图片/音频/视频在 assistant 回合未结束时被 GC 误删。
- [#119765 fix: agent exec runs the configured default agent](https://github.com/openclaw/openclaw/pull/119765) — 修复 `openclaw agent exec` 硬编码 `main` agent、绕过配置默认 agent 的问题。
- [#119733 improve(gateway): defer inactive plugin runtime imports](https://github.com/openclaw/openclaw/pull/119733) — 延迟加载非活跃插件的运行时，部分修复 #119087 启动开销问题。

整体来看，项目在“会话状态一致性”和“消息投递可靠性”两个方向上的修复投入明显大于功能开发。

---

## 4. 社区热点

今日讨论最活跃的议题（按评论数排序）：

| Issue/PR | 评论数 | 核心诉求 |
|---|---|---|
| [#116201 Realtime voice work can retain unbounded provider and consult state](https://github.com/openclaw/openclaw/issues/116201) | 58 | 实时语音会话在慢/卡/突发 provider 行为下无限保留 superseded consult、大帧及 pre-ready 音频资源，缺少硬性所有权边界。 |
| [#44925 Subagent completion silently lost — no retry, no notification, no auto-restart on timeout](https://github.com/openclaw/open

---

## 横向生态对比

# 开源 AI 智能体生态横向对比分析报告（2026-08-06）

> 说明：本次对比以 OpenClaw、Pi、LiteLLM 为有效数据样本；Hermes Agent、OpenHands SDK、Temporal 今日动态摘要为空，未能纳入定量对比。

## 1. 生态全景

当前开源智能体生态呈现“核心助手层—终端工具链—LLM 网关层”三层并进格局。OpenClaw 以千级 Issue/PR 日更新量继续维持个人 AI 助手赛道最大社区热度，但“高活跃、高积压”状态明显，P0/P1 稳定性问题正在反噬交付节奏。Pi 在终端原生 Agent 体验上保持高强度迭代，Bug 闭环速度快，且社区对 Windows/WSL 适配的呼声正在上升。LiteLLM 则在 LLM 网关层维持极高 PR 流转量，费用核算准确性与多租户安全隔离成为当日最受关注议题。整体来看，社区重点已从“功能创新”转向“可靠性治理与生产化落地”。

## 2. 各项目活跃度对比

| 项目 | Issues 更新数 | PR 更新数 | Release | 健康度评估 |
|---|---:|---:|---|---|
| OpenClaw | 500（新开/活跃 473，关闭 27） | 500（待合并 424，合并/关闭 76） | 无（2026.7.2 仍为当前线） | 🔴 高活跃、高积压：P0/P1 残留多，DB 迁移阻断发布 |
| Pi | 73（新开/活跃 16，关闭 57） | 37（待合并 7，合并/关闭 30） | 无（0.83.0） | 🟢 高强度迭代、闭环快：当日开当日关比例极高 |
| LiteLLM | 72（新开/活跃 46，关闭 26） | 322（待合并 189，合并/关闭 133） | v1.97.0-dev.1 | 🟠 极高活跃、多线并行：安全修复有积压，风险中高 |
| Hermes Agent | 无数据 | 无数据 | 无数据 | 无法评估 |
| OpenHands SDK | 无数据 | 无数据 | 无数据 | 无法评估 |
| Temporal | 无数据 | 无数据 | 无数据 | 无法评估 |

数据亮点：
- OpenClaw 单日 PR 更新量达 500，但合并率仅 15.2%（76/500），大量 PR 拥堵在队列中。
- Pi 单日合并/关闭 30 个 PR，合并率 81%，且多数为质量问题修复，工程效率突出。
- LiteLLM 单日 PR 更新 322，合并/关闭 133，并发布 1 个 dev 版本，迭代速度最快。

## 3. OpenClaw 在生态中的定位

OpenClaw 在可观测数据中处于个人 AI 助手/自主智能体“核心平台”身位，社区规模显著大于其他样本：

- **优势**：Issue/PR 总量最大，讨论话题覆盖实时语音、子代理状态、ClawHub 技能、多平台渠道（Mattermost 等），是生态中少数同时在“会话状态管理 + 技能市场 + 多渠道投递”三层均有布局的项目。
- **技术路线差异**：OpenClaw 以“智能体会话生命周期与消息投递可靠性”为核心攻坚方向，并投入自动化 bot（clawsweeper）批量修复；Pi 更聚焦终端交互体验（OSC 8、diff 滚动、上下文覆盖文件）；LiteLLM 则专注模型统一网关与费用治理。
- **社区规模对比**：OpenClaw 单日 500+500 条 Issue/PR 更新，约为 Pi 的 9 倍、LiteLLM 的 2.5 倍；但其 P0/P1 积压、自动化 PR 批量产出与低合并率，也说明项目已进入“规模扩张后的质量债偿还期”。
- **定位判断**：OpenClaw 是生态中“智能体运行时”最接近平台化的项目，但当前最大瓶颈已不是功能缺失，而是会话一致性、消息不丢不重、存储迁移等基础设施级稳定性问题。

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **Agent 运行稳定性与数据隔离** | OpenClaw、Pi、LiteLLM | 消息重复发送/子代理静默丢失（OpenClaw #44925）、并行工具结果丢失（Pi #7053）、Redis Cluster 跨用户响应串话（LiteLLM #25447）——共同指向“强会话所有权、可重试恢复、跨租户隔离”。 |
| **模型/Provider 兼容适配** | OpenClaw、Pi、LiteLLM | llama.cpp 400 错误（OpenClaw）、Copilot 模型列表为空（Pi #7672）、OCI Gemini 工具调用崩溃（LiteLLM #18654）等，反映 provider 行为碎片化是通用痛点。 |
| **上下文/资源边界治理** | OpenClaw、Pi、LiteLLM | 任务结果无界撑爆上下文（OpenClaw #119731）、thinking budget 占用 max_tokens（Pi #7638）、按天速率限制缺失（LiteLLM #14398）均为同一类“资源失控”问题。 |
| **扩展/插件生态成熟度** | OpenClaw、Pi、LiteLLM | ClawHub 技能隔离性修复（OpenClaw #119672）、`node:sqlite` 缺失导致扩展无法加载（Pi #7594）、Langfuse SDK v4 集成（LiteLLM #333

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

# Pi 项目动态日报 — 2026-08-06

**数据窗口**：过去 24 小时（2026-08-05 至 2026-08-06）｜**数据来源**：GitHub Issues / PRs

---

## 今日速览

Pi 项目在过去 24 小时保持高强度迭代：共更新 Issues 73 条（其中 57 条关闭、16 条新开或活跃）、PR 37 条（30 条已合并/关闭，7 条待合并），**活跃度评级：高**。当日最显著的特征是一批「当日开、当日关」的快速闭环：`AGENTS.override.md` 支持从 Issue（#7642）到 PR 合并（#7681/#7664）仅用一天，OSC 8 悬空链接、Copilot 模型缺失、事件总线泄漏等 bug 也均已完成修复。当前无新版本发布（最新稳定版仍为 0.83.0），但代码仓库层面的功能推进与质量修复速度明显快于发版节奏。

---

## 项目进展

当日共合并/关闭 30 个 PR，以下为对项目影响最大的关键变更：

- **AGENTS.override.md 支持落地** — PR #7681 与 #7664 同日合并，实现每个目录层级的高优先级上下文覆盖文件。当同一目录同时存在 `AGENTS.override.md` 和 `AGENTS.md`/`CLAUDE.md` 时，仅加载覆盖文件；祖先目录分层和 worktree 去重行为保持不变。对应 Issue #7642 一并关闭。  
  → https://github.com/earendil-works/pi/pull/7681  
  → https://github.com/earendil-works/pi/pull/7664

- **Copilot 模型缺失修复** — PR #7672 修复了 `/login copilot` 后 `availableModelIds` 恒为空的问题。修复逻辑：`model_picker_enabled` 仍为主要可用性信号，但当 Individual 端点无可用 picker 模型时，回退到策略显式启用的模型。  
  → https://github.com/earendil-works/pi/pull/7672

- **OSC 8 悬空链接修复完成** — PR #7657 关闭被截断的 OSC 8 超链接（在重置和省略号前补充关闭序列，保留 BEL/ST 终止符），PR #7665 进一步优化：对不含 OSC 8 序列的普通前缀跳过扫描，避免逐字符 ANSI 解析的性能开销。  
  → https://github.com/earendil-works/pi/pull/7657  
  → https://github.com/earendil-works/pi/pull/7665

- **扩展事件总线泄漏修复** — PR #7656 将 `pi.events.on()` 订阅限定在注册它的扩展运行时内，reload/disposal 后清理过期监听器而不影响宿主监听器，对应 Issue #7193 关闭。  
  → https://github.com/earendil-works/pi/pull/7656

- **`@file` 行范围引用支持** — PR #7679 支持 1-based 的 `#L<start>-L<end>` 选择器语法，覆盖 CLI `@file` 引用、图片范围拒绝、EOF 边界与 read 工具对齐，对应 Issue #7673。  
  → https://github.com/earendil-works/pi/pull/7679

- **OpenAI 兼容端点的思考预算分离** — PR #7638 为 `openai-completions` 增加 `thinking_token_budget` 支持，解决 reasoning-heavy 回合耗尽 `max_tokens` 后无文本返回却被误判为任务完成的问题。  
  → https://github.com/earendil-works/pi/pull/7638

- **Qwen 模型目录更新** — PR #7670 将 `qwen3.8-max-preview` 替换为 GA 版本的 `qwen3.8-max`，并应用 3.8 的 reasoning effort 映射（low/medium/xhigh）。  
  → https://github.com/earendil-works/pi/pull/7670

- **编译二进制 bunfig 自动加载禁用** — PR #7685 为编译产物加 `--no-compile-autoload` 选项，避免项目内损坏或依赖过重的 `bunfig.toml` preload 导致 `pi --version` 也无法运行。  
  → https://github.com/earendil-works/pi/pull/7685

- **长 diff 扩展选择器可滚动** — PR #7597 将 diff 标题包裹在 ScrollView 中，固定 yes/no 操作按钮，使超长 diff 可滚动审阅。  
  → https://github.com/earendil-works/pi/pull/7597

- **模型选择器自然排序** — PR #7690/#7692 共享 `model`/`scoped-models` 选择器的自然排序比较器（大小写不敏感 + 数字感知），使上下文窗口变体更易导航。  
  → https://github.com/earendil-works/pi/pull/7690  
  → https://github.com/earendil-works/pi/pull/7692

- **Harness v2 R2 通道归约器** — PR #7669 新增 R2 纯通道归约器：`LaneReductionInput → LaneReductionResult` 契约，从有界恢复记录派生持久 `LaneState`、有效通道配置与终端失败溯源；同时 PR #7654 为通道增加 `open_operation_id` 投影，以限制同通道同时只能有一个 open 操作。  
  → https://github.com/earendil-works/pi/pull/7669  
  → https://github.com/earendil-works/pi/pull/7654

---

## 社区热点

| Issue/PR | 类型 | 评论数 | 状态 | 核心诉求/讨论焦点 |
|---|---|---|---|---|
| [#7547](https://github.com/earendil-works/pi/issues/7547) | Issue | 17 | OPEN | **Windows 支持路线讨论**：维护者主动发起，征集 Windows 用户的运行方式与痛点，意在确定核心团队应聚焦在哪些运行路径上（原生、WSL、MSYS 等），其余可交给社区扩展。讨论热度当日最高。 |
| [#7399](https://github.com/earendil-works/pi/issues/7399) | Bug | 12 | CLOSED | `truncateToWidth()` 在截断 OSC 8 超链接时留下悬空链接，导致终端文本错误地被关联到某 URL。已有 #7657/#7665 修复并附带回归测试，当日闭环。 |
| [#7064](https://github.com/earendil-works/pi/issues/7064) | Bug | 12 | OPEN | **WSL 路径处理缺陷**（仍在开放）：agent 的 read/write/edit 工具在处理 Windows 绝对路径时频繁失败，被迫回退到命令行全量写入。获 1 👍，WSL2 用户受影响面较大。 |
| [#5291](https://github.com/earendil-works/pi/issues/5291) | Bug | 8 | CLOSED | Anthropic Enterprise 订阅用户遭遇会话随机卡在 “Working...” 状态，打断/恢复有时无效。获 3 👍，是当日关闭的 Issue 中反响最高的。 |
| [#6675](https://github.com/earendil-works/pi/issues/6675) | Bug | 8 | CLOSED | `pi update --self` 对最新版本查询只做一次请求，瞬时网络故障即中止更新流程。获 2 👍，已被识别为需要重试机制。 |

**社区诉求分析**：今日热帖呈现出三个信号——(1) **Windows/WSL 生态是 Pi 最大的增量市场**，但路径处理和运行方式碎片化是主要障碍；(2) **企业级订阅用户（Anthropic Enterprise、Copilot）对会话可靠性和模型可见性格外敏感**；(3) 终端渲染细节（OSC 8、TUI 滚动）虽小，但对体验感知影响显著，社区愿意为此提交高质量修复。

---

## Bug 与稳定性

按严重程度排序：

**🔴 高严重度**

- **`node:sqlite` 缺失导致扩展无法加载**（#7594，CLOSED/[no-action]）— 发布二进制缺少 `node:sqlite` 内置模块，`pi-total-recall` 等扩展直接加载失败。被标记为 no-action，但扩展生态兼容性风险值得后续版本关注。  
  → https://github.com/earendil-works/pi/issues/7594

- **Node 20 崩溃：undici CacheStorage 要求 Node ≥22.19.0**（#7601，CLOSED/[no-action]）— Node 20.11.1 环境下运行即崩溃，与版本兼容策略直接相关。目前标记 no-action，但 Node 20 仍是主流 LTS 版本，需评估是否应内置 polyfill 或明确声明最低版本要求。  
  → https://github.com/earendil-works/pi/issues/7601

- **WSL 绝对路径反复处理失败**（#7064，OPEN）— agent 的 read/write/edit 工具无法解析 Windows 绝对路径，导致 WSL2 用户代理效率大幅下降。已开放 12 天，仍无修复 PR，**建议优先处理**。  
  → https://github.com/earendil-works/pi/issues/7064

**🟡 中严重度**

- **并行工具批次丢失已完成结果**（#7053，OPEN）— `executeToolCallsParallel` 中整体 `Promise.all` 等待全部工具完成后才生成 `toolResult`，某一工具停滞会导致同批次其他已完成结果丢失（“No result provided”）。#3503 只修了 UI 事件层，持久层问题仍在。  
  → https://github.com/earendil-works/pi/issues/7053

- **WebSocket 重试仅覆盖两个错误码**（#7444，OPEN）— 除 `previous_response_not_found` 和 `websocket_connection_limit_reached` 外的瞬时 `response.failed` 错误会直接硬停当前回合，缺乏通用重试策略。  
  → https://github.com/earendil-works/pi/issues/7444

- **Deepseek 下 `unknown role: developer`**（#7603，CLOSED/[no-action]）— 0.83.0 与 Deepseek API 的 role 兼容性问题，消息改写需做 provider 适配。  
  → https://github.com/earendil-works/pi/issues/7603

- **成功重试留下永久红色错误行**（#7613，CLOSED/[no-action]）— 请求重试成功后界面仍保留红色 `Error: fetch failed` 行，给用户成功/失败的误判。属于 UI 反馈状态管理问题。  
  → https://github.com/earendil-works/pi/issues/7613

**🟢 低严重度 / 体验类**

- **TUI 滚动跳变且无 Page Up/D

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-06

## 1. 今日速览

LiteLLM 今日处于**极高活跃度**状态：过去 24 小时共有 **72 条 Issue 更新**（新开/活跃 46，关闭 26）、**322 条 PR 更新**（待合并 189，已合并/关闭 133），并发布 1 个新开发版（v1.97.0-dev.1）。项目正围绕**安全加固**（Redis 响应隔离、API 密钥哈希持久化）、**UI/UX 修复**（项目 URL 深度链接、审计日志别名、分页同步）以及**新供应商接入**（BytePlus、Bedrock AgentCore）三条主线快速迭代。值得关注的是，一个涉及 Redis Cluster 环境下响应串话的严重安全 Bug（#25447）正在被社区激烈讨论，官方已有多项相关安全修复 PR 在途；同时 2025 年提出的 Dark Mode 需求（#10177）至今未落地，已有 70 个 👍 与 62 条评论，成为社区“积怨最久”的功能诉求。

## 2. 版本发布

### v1.97.0-dev.1（开发版）

- **发布时间**：2026-08-06
- **主要内容**：该版本主要聚焦发布工程基建，公布了 Docker 镜像的 cosign 签名验证方案——所有 LiteLLM Docker 镜像均使用 [commit `0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0) 引入的同一密钥进行签名。
- **迁移注意事项**：这是 dev 版本，无破坏性变更说明；但建议生产环境用户在升级前验证镜像签名，确保供应链安全（`cosign verify` 命令已可在项目文档中找到）。

## 3. 项目进展

| 合并/关闭项 | 类型 | 说明 |
|---|---|---|
| [#35972](https://github.com/BerriAI/litellm/pull/35972) | feat(ui) | Auto-router 模板预设现可与部署的底层模型 ID 进行匹配，解决管理员自定义 model_name 后预设无法高亮的痛点 |
| [#34309](https://github.com/BerriAI/litellm/issues/34309) | bug 关闭 | OpenAI Responses API 路径下 `cache_read_cost`/`cache_creation_cost` 读取逻辑修正，成本统计与 Anthropic 风格顶层 usage key 对齐 |
| [#33988](https://github.com/BerriAI/litellm/issues/33988) | bug 关闭 | Managed batch 输出文件重复检索时的双重包装问题已修复，配合 [#34092](https://github.com/BerriAI/litellm/pull/34092) 的“终态检索时注册托管输出文件”机制 |
| [#35357](https://github.com/BerriAI/litellm/issues/35357) | bug 关闭 | `CheckBatchCost` 轮询增加单任务故障隔离，不再因单个失败批次中断全部批次成本核算 |
| [#33772](https://github.com/BerriAI/litellm/issues/33772) | bug 关闭 | OpenAI `cache_write_tokens` 已纳入成本计算，缓存写入请求不再被错误定价 |
| [#35797](https://github.com/BerriAI/litellm/issues/35797) | bug 关闭 | key 轮换宽限期 `TypeError` 修复 |
| [#26443](https://github.com/BerriAI/litellm/issues/26443) | bug 关闭 | JSON 配置的兼容提供商（如 Scaleway）纳入 `openai_compatible_providers`，非标准参数正确包裹进 `extra_body` |

**整体评价**：项目今日重心明显偏向**费用核算准确性**与**管理后台可用性**，且大量关闭的 Bug 均有对应修复在当日合并或已在 PR 队列中，体现为“问题闭环速度快、工程质量控制严格”。新增 BytePlus provider（#36012）的 PR 表明国际化市场（VolcEngine 海外版）正在成为官方拓展方向。

## 4. 社区热点

| Issue/PR | 热度指标 | 核心诉求 |
|---|---|---|
| [#10177](https://github.com/BerriAI/litellm/issues/10177) Dark Mode | 62 评论 / 70 👍 | 管理后台 UI 缺乏深色主题，用户喊话“I'm going blind”。从 2025-04-20 存在至今已超 15 个月，是社区持续关注度最高的开放 Issue |
| [#14398](https://github.com/BerriAI/litellm/issues/14398) 每日请求/Token 速率限制 | 11 评论 / 7 👍 | 目前仅支持每分钟维度的限流，而 OpenAI 等厂商免费/Pro 套餐按日限制额度，需增加 requests/day 与 tokens/day 控制 |
| [#18654](https://github.com/BerriAI/litellm/issues/18654) OCI Gemini 工具调用异常 | 8 评论 | OCI 上 Gemini 模型工具调用在流式与非流式下均抛异常，已影响生产使用 |
| [#25447](https://github.com/BerriAI/litellm/issues/25447) Redis Cluster 响应泄漏 | 5 评论 / 安全级别 | OpenShift 多副本分布式部署下，偶发出现响应返回到错误客户端。这是本周最具威胁性的安全讨论 |
| [#33383](https://github.com/BerriAI/litellm/issues/33383) Langfuse SDK v4 集成 | 4 评论 / 6 👍 | Langfuse 官方工程师直接提交 Issue，要求适配 v4 新观测链路，属生态合作信号 |

**诉求分析**：社区当前最强烈的三股声音是——① **可观测性与成本可见性**（准确计费、LLM 调用链追踪）；② **UI 基础体验升级**（Dark Mode、路由回退时显示实际服务模型）；③ **多区域/多租户场景下的安全隔离**。其中安全类话题因涉及数据泄漏而获得远超平时的关注密度。

## 5. Bug 与稳定性

### 🔴 严重（安全 / 数据隔离）
- **[#25447](https://github.com/BerriAI/litellm/issues/25447)（OPEN）Redis Cluster 响应串话**：OpenShift 多副本环境下，用户可能收到其他用户的响应。目前暂无官方回复，但已涌现多条相关修复 PR（[#34092](https://github.com/BerriAI/litellm/pull/34092)、[#30736](https://github.com/BerriAI/litellm/pull/30736)）。**建议紧急排查 Redis 连接池与 key 解析逻辑。**

### 🟠 高（核心链路故障）
- **[#18654](https://github.com/BerriAI/litellm/issues/18654)（OPEN）OCI Gemini 工具调用崩溃**：已确认复用 #18166 的部分归因，目前缺少 `split_chunks` 逻辑（同步流），社区期待与 #24819 一并修复。
- **[#35357](https://github.com/BerriAI/litellm/issues/35357)（已关闭）CheckBatchCost 全批中断**：已有修复合入，单失败不再拖垮全局。
- **[#20975](https://github.com/BerriAI/litellm/issues/20975)（OPEN）Responses API SSE 事件缺失**：Azure Responses 流缺少 `response.created` 等必需 SSE 事件，破坏客户端兼容性。

### 🟡 中（功能降级 / 计费偏差）
- **[#27183](https://github.com/BerriAI/litellm/issues/27183)（OPEN）Ollama Vision 调用失败**：自建镜像缺少 `pillow` 依赖，图片输入场景直接报错。
- **[#34309](https://github.com/BerriAI/litellm/issues/34309)（已关闭）缓存成本始终为 null**：已修复。
- **[#33772](https://github.com/BerriAI/litellm/issues/33772)（已关闭）cache-write 不计价**：已修复。

**稳定性判断**：核心代理与流式链路仍存在多起未闭环 Bug（OCI Gemini、Responses SSE），但费用与批次管线的高优问题呈现“日清日结”态势。安全类问题修复 PR（#30736、#34092）较大但已积压超 1 个月，需警惕合入窗口期进一步拉长。

## 6. 功能请求与路线图信号

| 功能请求 | 来自 Issue | 对应 PR / 路线图信号 |
|---|---|---|
| **BytePlus 供应商支持**（Doubao/Skylark 海外版） | — | [#36012](https://github.com/BerriAI/litellm/pull/36012)（OPEN）已在实现 Chat/Embeddings/Image Gen/TTS/Responses 全模态 |
| **Bedrock AgentCore Web Search 作为原生搜索提供方** | [#31819](https://github.com/BerriAI/litellm/issues/31819) | 尚无可参考 PR，官方暂未表态；但问题描述已给出完整 `litellm.search()` API 设计，可能纳入 v1.98+ 规划 |
| **请求/Token 每日速率限制** | [#14398](https://github.com/BerriAI/litellm/issues/14398) | 属高频需求（11 评论 / 7 👍），官方未明确排期；考虑到现有 per-minute 架构，扩展 per-day 窗口的改动成本不高 |
| **A2A Agent 自定义/动态 Headers** | [#21409](https://github.com/BerriAI/litellm/issues/21409) | 需求明确（

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*