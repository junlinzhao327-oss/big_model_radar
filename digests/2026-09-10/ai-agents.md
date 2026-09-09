# OpenClaw 生态日报 2026-09-10

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-09 22:35 UTC

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

# Hermes Agent 项目动态日报 — 2026-09-10

## 今日速览

过去 24 小时项目活跃度处于高位：Issue 更新 396 条（新开/活跃 260 条，关闭 136 条），PR 更新 500 条（合并/关闭 194 条，待合并 306 条）。当前 open 的 PR 中，9 月 9 日当天新开的修复 PR 数量较多，涉及内存门控、Docker 根less 代理、Webhook 幂等、413 恢复等多个模块，显示出开发侧正在密集响应近期报告的稳定性问题。暂无新版本发布，但社区对各项 Bug 的讨论与 PR 提交均较活跃，整体项目处于高速迭代加固期。值得关注的是 #66616 已累计 186 条评论近两月未闭环、#100401 P1 级 cron 死锁尚无对应修复 PR，项目健康度受少量高影响积压拖累。

---

## 版本发布

今日无新版本发布（Releases: 0）。

---

## 项目进展

过去 24 小时共有 **194 条 PR 被合并/关闭**。从可观测的代表条目来看，今日完成的关键修复包括：

- **#106866** [CLOSED] — **修复上下文压缩静默超时与端点跳转问题**（compression no longer times out silently on aux retries and stays on the session's OpenAI endpoint）。该 PR 为 #98466 的挽救方案（salvage #98480），解决压缩阶段 aux 重试/回退无输出超时、以及会话端点被错误切换到 api.openai.com 导致代理密钥被隔离的问题，适用于对话压缩与长会话稳定性场景。
  https://github.com/NousResearch/hermes-agent/pull/106866

- **#106726** [CLOSED] — **修复 CLI 交互模式下 subagent 完成提示打断流式响应的问题**（subagent completion notices wait for the streamed response box to close），改善 CLI 人在回环中的输出体验。
  https://github.com/NousResearch/hermes-agent/pull/106726

- **#88275** [CLOSED] — 此前的 **桌面端空闲 CPU 占用 40-73% 的 P2 性能问题**已关闭，对应修复已随某次提交合入，macOS Intel 用户可关注下一版本验证。
  https://github.com/NousResearch/hermes-agent/issues/88275

此外，今日还有一批指向明确修复的新 PR 已提交（尚待评审/合并），反映维护者正针对近期多个 P1/P2 回归做定点修复，例如 #106921 / #106926（rootless Docker egress 不可达误报健康）、#106915（部分 413 错误走字节级恢复）、#106922（Webhook 按路由做投递幂等）、#106925（重复响应的 goal

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 2026-09-10

## 今日速览

过去24小时项目处理效率极高：共 261 条 Issue 更新，其中关闭 211 条（关闭率 80.8%），同时新增/活跃 50 条，显示维护团队保持高速响应。PR 端有 6 条全部关闭/合并，遗留待合并数为 0，但新版本发布为 0。值得关注的是，今日 Issue 处理中有相当数量属于系统性的 `x-opencode-session` 头缺失问题（OpenCode Go 自 9 月 6 日起强制要求该头），相关修复已在代码库中流转并部分关单。整体项目活跃度偏高，修复节奏紧凑。

---

## 版本发布

今日无新版本发布。但根据 Issue/PR 中的信息，最新已发布版本为 `@earendil-works/pi-ai@0.84.4`（来自 #9076 描述）和 `pi 0.74.2`（来自 #9258 描述），`@earendil-works/pi-coding-agent` 版本为 0.85.1（来自 #9229 描述），可供生态开发者确认自身环境时参考。

---

## 项目进展

今日 6 个 PR 已全部合并或关闭，核心进展如下：

1. **修复 RPC 模式 reload 导致 runner 失效的严重问题**（[#9374](https://github.com/earendil-works/pi/pull/9374)）— 在 reload 前检查 `isStreaming` 和 `isCompacting`，防止活动会话中 reload 后工具结果损坏内部 runner 状态。此前在 RPC 模式下，扩展命令可在工具执行期间触发 reload，导致 Pi 存储损坏的调用结果。对 headless/自动化使用场景是重要修复。
2. **修正 Mistral-hosted GLM-5.2 的推理参数发送方式**（[#9376](https://github.com/earendil-works/pi/pull/9376)）— Mistral API 对 `zai-glm-5-2` 只支持通过 `reasoning_effort` 启用推理，而当前代码发送的是 `prompt_mode: "reasoning"`，导致该模型推理模式无法正常工作。属于 provider 适配修复。
3. **文档导航结构化验证**（[#9380](https://github.com/earendil-works/pi/pull/9380)）— 将 `docs.json` 定为版本文档导航清单并增加测试覆盖。长期改善文档可维护性与可达性。
4. **TUI 历史导航光标行为修复**（[#9382](https://github.com/earendil-works/pi/pull/9382)）— 向上翻阅历史消息时始终将光标保持在行尾，与 bash 等其他 CLI 界面行为保持一致。
5. **文档整理**（[#9370](https://github.com/earendil-works/pi/pull/9370)）— 将交互式测试与发布指南提取为 skill 文档。

总体而言，今日没有大型功能合入，但完成了多个高质量的中小修复，涵盖一个可能造成状态损坏的并发缺陷、两个模型/provider 兼容性修复，以及若干 TUI/文档改进。代码库净质量提升明显。

---

## 社区热点

今日讨论最集中的几个话题：

1. **Session 挂起问题**（[#5291](https://github.com/earendil-works/pi/issues/5291)，10 评论，已关闭）— 用户报告使用 Anthropic Enterprise 订阅时 session 间歇性卡在 "Working..."，需中断/恢复多次，且常同时发生。该 Issue 已关闭，但 9/9 仍有最后更新，说明维护团队做了收尾处理。该问题是持续性的稳定性投诉热点。

2. **PI_OFFLINE 行为与文档不一致**（[#8684](https://github.com/earendil-works/pi/issues/8684)，7 评论，打开中）— 用户发现 `PI_OFFLINE` 除文档所述的启动操作外，还会**静默禁用所有 provider 的模型目录网络发现**。这一发现可能影响到依赖离线模式做模型发现的 CI/开发环境配置。

3. **并行启动时的 OAuth 过期凭证误报**（[#8928](https://github.com/earendil-works/pi/issues/8928)，6 评论，打开中）— 多进程并发启动时，若 `auth.json` 中某个非当前 provider 的 OAuth 凭证过期，会导致另一 provider 被误报 "No API key found"，误导排障方向（用户投入了 3 小时才定位根因）。该 Issue 关联 #1871、#4919、#6880 等同类问题，且提供了确定性复现方式和时间数据。

4. **OpenCode Go 强制 `x-opencode-session` 头引发的连锁反应**（#9381、#9230、#9290、#9326、#9302 等多条，每条 5-6 评论）— OpenCode Go 于 2026-09-06 强制要求带 `x-opencode-session` 头，Pi 的多个调用路径（内置 provider、extensions 的 `modelRegistry.complete()`、`@earendil-works/pi-ai` 库、out-of-loop summarization）均出现 400 MissingSessionID 报错。社区在一天内密集上报，其中部分已标记 `[no-action]` 关闭，暗示可能已在主分支修复或将被统一处理。

5. **pi-safe-compact 包安全审查请求**（[#9381](https://github.com/earendil-works/pi/issues/9381)，5 评论，已关闭）— 社区用户上报包 `pi-safe-compact` 版本 0.6.3 存在可疑/不安全行为，因为相关 GitHub 用户 `primp9053` 目前无法访问。Package Report 机制起到了第三方包安全预警的作用。

热点话题呈现两个明显方向：一是围绕 OpenCode 新策略的适配风暴；二是多进程/并发场景下因过期凭证导致的诊断困难。两者都反映出社区用户已将 Pi 深度用于生产环境。

---

## Bug 与稳定性

按严重程度排列：

| 严重度 | Issue | 问题描述 | 状态 |
|--------|-------|----------|------|
| 严重 | [#8720](https://github.com/earendil-works/pi/issues/8720) | 工具返回纯空格输出（如 Windows bash 的 `\r\n`）时，该消息被原样发给 provider，OpenAI 兼容 API 拒绝空白 tool 内容返回 400，且坏消息留在历史中导致**后续所有请求永久失败** | OPEN |
| 严重 | [#8928](https://github.com/earendil-works/pi/issues/8928) | 并行启动时过期 OAuth 凭证会引发误报 "No API key found"，持续约 48 秒，误导排障 | OPEN，有确定性复现 |
| 高 | [#8684](https://github.com/earendil-works/pi/issues/8684) | `PI_OFFLINE` 静默禁用所有 provider 模型发现，与文档定义范围不符 | OPEN |
| 高 | [#9276](https://github.com/earendil-works/pi/issues/9276) | grep 工具开启 context lines 时逐行读全文，导致内存堆耗尽（OOM），影响 headless SDK 模式 | OPEN |
| 中 | [#8760](https://github.com/earendil-works/pi/issues/8760) | OpenRouter `:free` 模型因 Pi 发送超出 provider 上限的 `max_tokens` 而 400 | OPEN，[inprogress] |
| 中 | [#8810](https://github.com/earendil-works/pi/issues/8810) | 扩展注册的 provider 在新 session 中间歇性忽略 `defaultProvider`/`defaultModel` 配置，静默回退到其他 provider | OPEN |
| 中 | [#9294](https://github.com/earendil-works/pi/issues/9294) | claude-fable-5 的 `allowedFallbackModels` 内置列表含已被 API 拒绝的 `claude-opus-4-8` | OPEN |
| 低 | [#9311](https://github.com/earendil-works/pi/issues/9311) | fullscreen TUI 模式下文本选中状态在 session 切换后仍残留 | OPEN |
| 低 | [#8827](https://github.com/earendil-works/pi/issues/8827) | LaTeX 经典字体切换命令（`\rm`、`\bf`、`\it`）导致整块数学公式回退为原始源码渲染 | OPEN |
| 低 | [#9298](https://github.com/earendil-works/pi/issues/9298) | Grok 的 403 额度错误被错误地标成 "OpenAI API error"，误导用户判断 | OPEN |
| 已修复或无需操作 | [#9230](https://github.com/earendil-works/pi/issues/9230)、[#9290](https://github.com/earendil-works/pi/issues/9290)、[#9326](https://github.com/earendil-works/pi/issues/9326)、[#9302](https://github.com/earendil-works/pi/issues/9302)、[#9229](https://github.com/earendil-works/pi/issues/9229)、[#9212](https://github.com/earendil-works/pi/issues/9212) | opencode-session 系列问题、Windows shell_path 忽略、sonnet-5 网关截断等，已按 `[no-action]` 或 CLOSED 处理 | CLOSED |

确认严重的 bug 中，**#8720（空白 tool 输出永久损坏会话）** 和 **#8928（过期 OAuth 误导诊断）** 值得优先关注。目前暂未见对应 fix PR 合入。

---

## 功能请求与路线图信号

今日有若干值得关注的功能/改进提案：

1. **OpenAI 异步工具调用支持**（[#9113](https://github.com/earendil-works/pi/issues/9113)，已关闭标记为 no-action）— 社区提出 Pi 是否支持 GPT-6 Astra 的 async tool calling，让 agent 在工具执行期间继续工作。该 Issue 被标记为 no-action 并关闭，可能意味着现阶段引擎架构不支持异步执行或优先级较低。

2. **Agent 重试退避上限可配置**（[#8826](https://github.com/earendil-works/pi/issues/8826)，已关闭）— 请求为 coding-agent 的指数退避增加可配置 cap，使长时间上游故障时重试间隔有上限，避免无限拉长。已关闭可能意味着已实现或另有方案。

3. **Device-code 登录体验优化**（[#9282](https://github.com/earendil-works/pi/issues/9282)，3 评论，👍1）— 建议允许 provider 主动打开验证页面并在设备码登录时自动拷贝 code 到剪贴板。GitHub Copilot provider 可受益。目前只是提议，未合并。

4. **JSON/RPC 暴露 provider 终端错误分类**（[#9247](https://github.com/earendil-works/pi/issues/9247)，已关闭）— 请求在 assistant 事件中结构化标注错误是否为确定性上下文溢出、安全拒绝、限流/不可用或未知错误，并提供重试属性。对 headless 编排很重要，但被标为 no-action。

5. **fuzzy session 搜索性能优化**（[#9267](https://github.com/earendil-works/pi/issues/9267)，3 评论，👍1）— 建议用 `String.indexOf()` 替代逐字符扫描以降低成本，不影响排序结果。属于低成本高收益的优化点，可能进入后续版本。

6. **协作/扩展方向功能请求**（[#9290](https://github.com/earendil-works/pi/issues/9290)、[#9302](https://github.com/earendil-works/pi/issues/9302) 等被关闭/标记 no-action）— 虽然这些是 bug 报告，但同步暴露了扩展 API 在传递 session 元数据时的能力缺口，提示未来扩展 API 可能需要提供会话级默认 HTTP 头的透传能力。

判断：今日无大规模的路线图信号；更多的是兼容性适配与体验打磨。真正具备下一版本候选特征的是 #9267（fuzzy 搜索优化）和 #8826（退避上限，虽已关闭但可能已纳入实现）。

---

## 用户反馈摘要

从今日活跃 Issues 评论中提炼的真实用户反馈：

1. **生产环境中的诊断困难**（[#8928](https://github.com/earendil-works/pi/issues/8928)）— 用户投入约 3 小时调试一个最终归因于过期 OAuth 凭证的误报错误。核心痛点是**错误信息指认错误的 provider**，导致排查方向完全错误。此类误导性报错在多进程架构中影响被放大。

2. **订阅用户对挂起问题的抱怨**（[#5291](https://github.com/earendil-works/pi/issues/5291)）— "session stuck on Working..." 同时出现，需要中断/等待/恢复循环。这类 session 无响应问题对

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-09-10

## 今日速览

- 过去 24 小时 Issues 侧零新增、零关闭，Issue 讨论相对安静；PR 侧保持活跃，共 36 条动态，其中 14 条关闭/合入，22 条仍在等待合并。
- 技术热点集中在三块：**SignalWithStart 可靠性修复**、**Nexus callback 安全/可观测性/发布分支改进**、**历史分页跨分支元数据变化的兼容性**。
- 无新版本发布；项目处于 v1.30.x/v1.31/v1.32 分支维护与 v1.33 版本号预升级的并行推进阶段。
- 整体项目健康度良好：没有出现新增 Issue 堆积，主要可靠性修复和稳定性加固通过 PR 持续落地，社区协作节奏正常。

## 版本发布

无。

## 项目进展

过去 24 小时关闭/合入的 PR 共 14 条，覆盖功能开关、可观测性、测试稳定性、发布流程自动化与文档工具升级等多个方向，主要进展包括：

- **Nexus callback

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*