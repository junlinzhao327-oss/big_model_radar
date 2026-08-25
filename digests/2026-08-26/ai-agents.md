# OpenClaw 生态日报 2026-08-26

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-25 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 开源项目动态日报 — 2026-08-26

---

## 今日速览

过去 24 小时内，OpenClaw 项目保持了极高的社区活跃度：累计 500 条 Issue 更新（新开/活跃 435 条，关闭 65 条）和 500 条 PR 更新（待合并 310 条，已合并/关闭 190 条）。值得关注的是，今日无新版本发布（当前最新为 v2026.8.1-beta.3），项目正处于 beta 验证与发布冲刺的关键阶段。P1 级 Bug 报告密集（涉及消息丢失、会话状态损坏、崩溃循环等可靠性问题），但同时有大量修复 PR 处于待审查和合并状态，说明维护团队正在积极回应社区反馈。此外，大量长期未解决的"陈年"Issue（最早可追溯至 2026 年 2 月）仍在持续获得评论更新，反映了社区对稳定性问题的持续关注。

---

## 版本发布

今日无新版本发布。当前最新版本为 [v2026.8.1-beta.3](https://github.com/openclaw/openclaw/releases/tag/v2026.8.1-beta.3)。相关发布验证 Issue [#125626](https://github.com/openclaw/openclaw/issues/125626) 已关闭（18 条评论），建议关注后续正式版本发布公告。

---

## 项目进展

### 今日合并/关闭的 PR 要点

| PR | 标题 | 状态 | 核心内容 |
|---|---|---|---|
| [#125471](https://github.com/openclaw/openclaw/pull/125471) | fix(models): keep Claude CLI OAuth available in Control UI | ✅ 已关闭 | 修复 Gateway 重启后 Claude CLI OAuth 刷新所有权丢失的问题，避免遗留配置导致矛盾状态 |
| [#128371](https://github.com/openclaw/openclaw/pull/128371) | fix(release): authorize focused beta evidence | ✅ 已关闭 | 解决 beta.3 发布阻塞：允许仅针对修改范围（Slack 测试）的聚焦验证清单 |

### 当前值得关注的在途 PR（已就绪待审查）

- **修复消息丢失**：[#127342](https://github.com/openclaw/openclaw/pull/127342) — 修复 Gateway 重启后恢复的主会话回复被静默写入记录而未送达用户渠道的问题（关闭 #127339），评级 🦞 diamond lobster，merge-risk 标记为 message-delivery
- **安全边界加固**：[#129604](https://github.com/openclaw/openclaw/pull/129604)（P0）— 强制共享终端输入遵守会话权限，防止代理绕过执行权限控制；[#104872](https://github.com/openclaw/openclaw/pull/104872)（P0）— 拒绝伪造的插件所有者权限
- **性能优化**：[#129652](https://github.com/openclaw/openclaw/pull/129652) — 消除 provider policy 加载时的传输图编译，避免事件循环长时间阻塞
- **Web UI 修复**：[#129426](https://github.com/openclaw/openclaw/pull/129426)（gateway，ready for maintainer look）— 修复隐藏用户回合后真实助手回复被丢弃的问题
- **会话状态持久性**：[#129510](https://github.com/openclaw/openclaw/pull/129510) — 修复代理特定模型选择时反复扫描插件导致的秒级停顿

整体来看，项目虽处于 beta 收尾阶段，但社区提交的修复 PR 质量较高、范围明确，有持续合并推进的迹象。

---

## 社区热点

### 高讨论度 Issue

以下 Issue 在今天获得了最多的评论与关注，反映了社区的核心痛点：

1. **[#125626 — OpenClaw 2026.8.1 beta 反馈（已关闭）](https://github.com/openclaw/openclaw/issues/125626)**（💬 18 条）
   发布验证专用反馈频道，已关闭，建议关注正式版 Release 说明。

2. **[#80319 — QA 工具默认值套件混淆 Codex 原生工具与 OpenClaw 动态工具对等性](https://github.com/openclaw/openclaw/issues/80319)**（💬 17 条，👍 1）
   讨论核心：QA 测试工具将 Codex 原生工具（`read`、`write`、`edit` 等）与 OpenClaw 动态工具做对等断言，导致误报。社区和开发者共同澄清这是 QA 框架层面的问题，而非真实运行时缺陷。该讨论凸显了开发者对 **CI/CD 测试可靠性的高度关注**。

3. **[#67777 — 子代理完成投递在直连宣布超时/排空/孤儿清理时丢失（P1，diamond lobster）](https://github.com/openclaw/openclaw/issues/67777)**（💬 13 条）
   子代理结果通过"同步直连"方式传回请求方会话，在忙通道/超时/重启恢复时可能丢失且无兜底队列。该问题直接威胁多代理协作的正确性，是社区**高度关注的可靠性问题**。

4. **[#50093 — WhatsApp 重连后消息补发功能请求（P1，platinum hermit）](https://github.com/openclaw/openclaw/issues/50093)**（💬 12 条，👍 1）
   断线期间消息静默丢失，社区呼吁增加 backfill 机制。虽为 Feature Request，但用户明确使用了"silently lost"来描述问题，反映了对**消息不丢失机制**的刚需。

5. **[#97616 — Hook/工具子进程泄漏导致僵尸进程累积（P1）](https://github.com/openclaw/openclaw/issues/97616)**（💬 9 条，👍 1）
   长期运行后 zombie 进程不断累积，导致运行时性能退化。该问题被标记为 Regression（以前正常，现在异常），影响平台稳定性。

### 趋势洞察

讨论热度最高的议题集中在三个领域：**（1）消息/会话数据不丢失的强一致性保障；（2）QA 体系与 CI 的可靠性；（3）长时间运行时的资源泄漏**。这说明社区用户已将 OpenClaw 从"可用的聊天机器人框架"推向"生产级多代理网关平台"的更高标准。

---

## Bug 与稳定性

以下为今日最值得关注的 Bug 报告，按严重程度排序：

### 🔴 严重（消息丢失 / 数据丢失 / 安全边界）

- **[#126900 — maxActiveTranscriptBytes 在压缩后仍超阈值时无限循环压缩，阻塞管道](https://github.com/openclaw/openclaw/issues/126900)**（P1，diamond lobster）— 压缩后仍未降到阈值以下时，会无限触发压缩，导致通道卡死。已有相关 PR 在推进。
- **[#126246 — Telegram 持久化外发投递卡在 send_attempt_started，重启后消息丢失](https://github.com/openclaw/openclaw/issues/126246)**（P1，diamond lobster，message-loss）
- **[#126906 — 拒绝 write 工具将静默禁用记忆持久化，代理仍报告保存成功](https://github.com/openclaw/openclaw/issues/126906)**（P1，data-loss，diamond lobster）— 工具裁剪导致记忆功能暗默失效，且无任何启动/诊断/代理层提示。
- **[#125570 — Skill Workshop 更新覆盖活动技能描述，静默破坏技能路由](https://github.com/openclaw/openclaw/issues/125570)**（P1，data-loss，diamond lobster）
- **[#128067 — beta.7 现场报告：6 类可靠性缺陷 + 3 个次要问题](https://github.com/openclaw/openclaw/issues/128067)**（P1，multi-agent gateway 3 周生产证据）— 涵盖持久化、投递、重启恢复的复合缺陷报告。

### 🟠 中高（会话状态损坏 / 崩溃循环 / 认证异常）

- **[#97616 — 子进程泄漏导致 Zombie 累积和运行时退化](https://github.com/openclaw/openclaw/issues/97616)**（P1，Regression，crash-loop）
- **[#108379 — Xiaomi MiMo 提供商重复生成尝试导致重复叙述文本](https://github.com/openclaw/openclaw/issues/108379)**（P1）
- **[#80178 — resolveCliAuthEpoch 在凭据存储切换时使所有在线 CLI 会话失效](https://github.com/openclaw/openclaw/issues/80178)**（P1，diamond lobster）
- **[#60398 — 家目录位于外部 APFS 卷时 gateway install 失败](https://github.com/openclaw/openclaw/issues/60398)**（P1，crash-loop，maturity:stable）
- **[#56217 — 密钥提供商崩溃循环耗尽 1Password 服务账户速率限制](https://github.com/openclaw/openclaw/issues/56217)**（P1，linked-pr-open）
- **[#127239 — deepseek-v4-flash 上下文窗口静默回退为 200k 而非实际 1M](https://github.com/openclaw/openclaw/issues/127239)**（P1，diamond lobster）

### 🟡 中（UX 摩擦 / 功能异常）

- **[#128657 — Control UI 加载骨架屏每帧重绘](https://github.com/openclaw/openclaw/issues/128657)**（P2，maintainer 标记，recovery-stuck）
- **[#126631 — Sandbox skills bind-mount 创建 root 所有的目录，锁定沙箱用户](https://github.com/openclaw/openclaw/issues/126631)**（P1，linked-pr-open）
- **[#127176 — Windows 上 CLI 与 Node Host 交替使用不同的设备元数据](https://github.com/openclaw/openclaw/issues/127176)**（P1，linked-pr-open）
- **[#125626（已关闭）](https://github.com/openclaw/openclaw/issues/125626) 所涉及的 beta.3 验证问题**已通过 [#128371](https://github.com/openclaw/openclaw/pull/128371) 解决。

### 修复 PR 状态汇总

已有关联修复 PR 的 Bug：

| Issue | 状态 | 关联 PR |
|---|---|---|
| [#127339](https://github.com/openclaw/openclaw/issues/127339)（重启后回复静默完成） | 📌 有 PR | [#127342](https://github.com/openclaw/openclaw/pull/127342)（ready for look） |
| [#124946](https://github.com/openclaw/openclaw/issues/124946)（终端权限绕过） | 📌 有 PR | [#129604](https://github.com/openclaw/openclaw/pull/129604)（P0，needs proof） |
| [#129373](https://github.com/openclaw/openclaw/issues/129373)（未读提醒消失） | 📌 有 PR | [#129386](https://github.com/openclaw/openclaw/pull/129386)（XL，waiting on author） |
| [#129466](https://github.com/openclaw/openclaw/issues/129466)（VCR 镜像空输入） | 📌 有 PR | [#129467](https://github.com/openclaw/openclaw/pull/129467) |
| [#129378](https://github.com/openclaw/openclaw/issues/129378)（Inbox 提醒作用域） | 📌 有 PR | [#129379](https://github.com/openclaw/openclaw/pull/129379) |
| [#56217](https://github.com/openclaw/openclaw/issues/56217)（1Password 限流崩溃循环） | 📌 有 PR | 状态标注 linked-pr-open |

---

## 功能请求与路线图信号

### 高潜力功能需求（有社区共鸣 + 参与者）

1. **[Onboarding 向导应包含 Memory/Embedding 必选配置步骤（#16670）](https://github.com/openclaw/openclaw/issues/16670)**（P2，diamond lobster，9 条评论）
   用户指出 `openclaw setup` 完全未提及 embedding provider 配置，导致新手用户的 `memory_search` 功能静默不可用。得到 🦞 diamond lobster 高评级，已获得 maintainer 注意。

2. **[暴露 OpenRouter 使用成本给代理运行时（#9016）](https://github.com/openclaw/openclaw/issues/9016)**（P2，8 条评论）
   社区希望代理能感知每次请求的 OpenRouter 费用并将成本信息附加到回复中，便于用户掌握支出。属 lightweight 但用户价值直接的增强。

3. **[优雅的子代理超时（超时前预警）（#6625）](https://github.com/openclaw/openclaw/issues/6625)**（P3，6 条评论）
   建议在 `runTimeoutSeconds` 到期前注入系统消息，让子代理有时间保存进度。对多代理任务可靠性有明显提升。

4. **[网关层图片批处理/媒体组缓冲（#39343）](https://github.com/openclaw/openclaw/issues/39343)**（P2，diamond lobster，5 条评论，👍 1）
   将快速连续的多张图片归并为一次代理请求，避免代理逐张回复造成刷屏。对 LINE/Telegram 相册场景实用性强。

### 与现有 PR 形成呼应

- **记忆系统改进**：[#114612（SQLite 无界增长）](https://github.com/openclaw/openclaw/issues/114612) 与 [#44395（标题感知分块 + 实体提取）](https://github.com/openclaw/openclaw/issues/44395) 共同表明"记忆/嵌入"正在成为下一阶段重点优化方向。

- **TUI 可访问性**：[#9637（禁用 emoji 选项）](https://github.com/openclaw/openclaw/issues/9637) 与 [#95601（VoiceOver 友好聊天记录）](https://github.com/openclaw/openclaw/issues/95601)（👍 2）表明社区对无障碍体验的诉求在上升，可能成为 upcoming release 的 polish 项。

- **路由/调度**：[#64103（会话状态字段误导代理产生重复会话）](https://github.com/openclaw/openclaw/issues/64103) 与 [#79252（全局熔断器按工具类型计数可被绕过）](https://github.com/openclaw/openclaw/issues/79252) 指向代理编排机制仍需加固。

---

## 用户反馈摘要

从今日更新的 Issue 评论中，提取以下真实用户反馈：

- **多代理生产环境的可靠性焦虑**（来自 #128067）：一名用户以"单网关 + 6 代理 + 重度 cron + telegram/webchat"的生产级部署，收集了三周内的 6 类可靠性缺陷证据，包括持久化失败、投递丢失、重启恢复异常。用户虽表示"愿意提供脱敏日志"，但也流露出对 beta 版本作为生产依赖的担忧。

 > "All items reproduced multiple times over ~3 weeks; happy to provide redacted logs per item."

- **对静默失败的高度不满**（来自 #126906、#99925、#125570）：多个用户反映了同一模式：OpenClaw 在某种配置或异常情况下**静默地不做正确的事**，而系统本身给出了"成功"的信号。例如拒绝 write 工具后记忆保存"看似成功"、WebChat 新会话"零上下文"、Skill Workshop 更新导致技能路由"静默失效"。这种"不报错但错误"的行为对用户信任的打击极大。

- **Windows/桌面端用户体验问题**（来自 #127176、#99925）：Windows 用户报告设备元数据混乱、WebChat 会话上下文丢失等问题，反映桌面端（尤其是 Windows）的成熟度仍落后于 macOS/L

---

## 横向生态对比

# 个人 AI 助手/自主智能体开源生态横向对比分析报告 — 2026-08-26

---

## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态正处于「从可用原型向生产级平台跃迁」的关键阶段。OpenClaw、Pi 等端侧代理项目已积累大规模社区（单日 Issue/PR 更新合计达数百条），用户诉求已从"聊天功能"全面转向消息不丢失、会话恢复、成本可控等生产级可靠性指标。与此同时，LiteLLM、Temporal 等基础设施层项目在协议桥接（Anthropic↔OpenAI Responses API）、多集群复制、资源泄漏治理等方向持续加固，为上层 Agent 提供更稳定的模型接入与工作流底座。值得注意的是，Gemini CLI 退役、Bedrock/OpenRouter 等 Provider 兼容性修复频繁出现，说明模型生态的快速变化正在倒逼代理框架加强适配层的鲁棒性。

---

## 2. 各项目活跃度对比

| 项目 | Issue 更新（新开/活跃 / 关闭） | PR 更新（待合并 / 已合并关闭） | Release | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-26

---

## 1. 今日速览

过去 24 小时项目活跃度处于近期

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-08-26

## 1. 今日速览

过去24小时项目活跃度较高：Issue 侧新开/活跃 12 条、关闭 12 条，PR 侧 7 条待合并、6 条已合并/关闭，无新版本发布。值得关注的是今日 4 个闭环动作高度集中在 ACP 与 Gemini CLI 退役的善后处理（#4624、#4629）、异步执行器挂死修复（#4546 → #4548）以及 CI 就绪检查的体验优化（#4631 → #4632），显示项目正处于「迁离 Gemini CLI 的过渡期 + 稳定性修补」并行推进的阶段。尽管自动化测试 issue（#4633）与工具链问题（#4631）体现了一定的流程噪音，但整体维护节奏健康，社区参与度稳健。

---

## 2. 版本发布

今日无新版本发布。但 [#4628](https://github.com/OpenHands/software-agent-sdk/pull/4628) 已发起 **v1.44.0** 的 Release PR，目前集成测试、行为测试与安全检查仍在进行中，预计近期完成发布，值得关注其是否包含 ACP 修复与稳定性改动。

---

## 3. 项目进展

今日合并/关闭的 PR 主要围绕 **问题修复、CI 流程打磨、生态合作** 三个方面：

- **[#4548](https://github.com/OpenHands/software-agent-sdk/pull/4548) fix(sdk): bound AsyncExecutor.close() so it cannot hang forever** — 合入。直接修复 [#4546](https://github.com/OpenHands/software-agent-sdk/issues/4546) 中 `AsyncExecutor.close()` 可能永久阻塞并卡死会话关闭的高优先级问题，是今日最重要的稳定性推进。
- **[#4632](https://github.com/OpenHands/software-agent-sdk/pull/4632) Relax ready-for-dev heading check to accept h2 headings** — 合入。修复 [#4631](https://github.com/OpenHands/software-agent-sdk/issues/4631)，使 `ready-for-dev` 检查兼容 h2/h3 标题，减少对自由格式 issue 的误判。
- **[#4625](https://github.com/OpenHands/software-agent-sdk/pull/4625) chore(ci): clarify issue readiness bot comment and reference templates** — 合入。改进了 readiness 机器人评论，直接关联 issue 模板，减少贡献者困惑。
- **[#4611](https://github.com/OpenHands/software-agent-sdk/pull/4611) feat: add manifest to installed canvas extension responses** — 合入。为 canvas 扩展响应补充 manifest 信息，完善扩展机制的可发现性。
- **[#4612](https://github.com/OpenHands/software-agent-sdk/pull/4612) docs: refresh AGENTS.md guidance** — 合入。为 AI/LLM 代理贡献者更新协作指南，降低 bot 与人类的协作摩擦。
- **[#4576](https://github.com/OpenHands/software-agent-sdk/pull/4576) 50/50 RevShare Integration: OpenHands & AIML API** — 关闭（未合入）。AIML API 提议以 50/50 分成方式成为 OpenHands 的已验证 provider，最终未合并，可能涉及商业模式评估。

整体判断：项目在 **关键稳定性缺陷修复** 上取得实质进展，同时通过 CI 与文档的打磨提升了贡献者体验。

---

## 4. 社区热点

今日讨论热度最高的几个 Issue：

- **[#2186 — feat(delegation): Advanced Features for Markdown-based Agents](https://github.com/OpenHands/software-agent-sdk/issues/2186)**（14 条评论，最终关闭）— 这是跨 6 个月的长生命周期 issue，累计追踪了 Markdown-based Agent 的大量高级特性。最终关闭且其中的需求全部完成，是社区与维护者长期协作的正面案例。
- **[#3176 — Proposal: extend defense_in_depth PatternSecurityAnalyzer with Agent Threat Rules signatures](https://github.com/OpenHands/software-agent-sdk/issues/3176)**（13 条评论，最终关闭）— 围绕安全检测规则扩展的讨论，从 5 月持续至今关闭，说明安全团队有在接收社区的安全模式贡献。
- **[#3495 — step-3.7-flash: vision support not detected at runtime](https://github.com/OpenHands/software-agent-sdk/issues/3495)**（8 条评论，仍开放）— 关于 LiteLLM 代理层 `model_info` 未传递导致视觉能力被静默跳过的问题，当前有 8 条评论但尚未定位根因，牵涉集成测试覆盖率盲区，是值得维护者关注的 runtime 兼容性问题。
- **[#4577 — Add per-key tag endpoints to avoid read-modify-write on PATCH /api/conversations/{id}](https://github.com/OpenHands/software-agent-sdk/issues/4577)**（5 条评论）— 提出新增 `POST/DELETE /tags/{key}` 端点以避免整表覆盖写入，已有对应 PR [#4617](https://github.com/OpenHands/software-agent-sdk/pull/4617)，社区方案与官方实现形成了良好联动。

**需求洞察：** 社区一方面期望更细粒度的 API 控制（#4577），另一方面对模型能力检测的准确性（#3495）与 ACP 兼容性（#4624、#4629）有较高关注度，反映出项目已进入「企业级/平台化」使用阶段。

---

## 5. Bug 与稳定性

按严重程度排列今日活跃的 Bug：

| 严重度 | Issue | 描述 | Fix PR 状态 |
|---|---|---|---|
| 🔴 高 | [#4546](https://github.com/OpenHands/software-agent-sdk/issues/4546) | `AsyncExecutor.close()` 永久阻塞，导致会话关闭卡死 | ✅ 已合入 [#4548](https://github.com/OpenHands/software-agent-sdk/pull/4548) |
| 🔴 高 | [#3842](https://github.com/OpenHands/software-agent-sdk/issues/3842) | 会话卡在 `execution_status=idle` 但 `/run` 返回 409，需重启才能恢复 | ❌ 无，已关闭（可能为 Stale） |
| 🟠 中 | [#4555](https://github.com/OpenHands/software-agent-sdk/issues/4555) | Agent Server 事件端点因 `LocalConversation` 清理阻塞而无限挂起 | ❌ 无 |
| 🟠 中 | [#4629](https://github.com/OpenHands/software-agent-sdk/issues/4629) | Gemini CLI 已退役的 OAuth 会优先于可用 API key，且 ACP Gemini pin 版本落后十个次要版本 | ❌ 无（#4624 为迁移方案） |
| 🟡 低 | [#3495](https://github.com/OpenHands/software-agent-sdk/issues/3495) | `step-3.7-flash` 视觉支持在运行时未被检测到，集成测试被静默跳过 | ❌ 无 |

**重点关注：**
- [#4546](https://github.com/OpenHands/software-agent-sdk/issues/4546) 的修复已合入，但建议通过 v1.44.0 尽早在生产环境验证。
- [#4555](https://github.com/OpenHands/software-agent-sdk/issues/4555) 与 #4546 同属「并发/清理阻塞」问题域，尚未有 PR，可能与 `LocalConversation` 的内部锁机制相关，建议优先排查。
- [#4629](https://github.com/OpenHands/software-agent-sdk/issues/4629) 反映 Google Gemini CLI 6 月 18 日退役后，SDK 的 ACP Gemini 路径仍未完全适配，影响使用 Gemini 的用户。

---

## 6. 功能请求与路线图信号

今日出现的功能请求与路线图信号：

**🎯 高可能性纳入下个版本：**

- **[#4577 — Per-key tag endpoints](https://github.com/OpenHands/software-agent-sdk/issues/4577)** — 新增 `POST/DELETE /api/conversations/{id}/tags/{key}`，已有 PR [#4617](https://github.com/OpenHands/software-agent-sdk/pull/4617) 处于待合并状态，预计随 v1.44.0 或之后小版本进入。
- **[#4631 — ready-for-dev 检查支持 h2 标题](https://github.com/OpenHands/software-agent-sdk/issues/4631)** — 已通过 PR [#4632](https://github.com/OpenHands/software-agent-sdk/pull/4632) 修复，改善开发者体验。

**🧭 中期路线图信号：**

- **[#4627 — Harness Watch: 自动化对比 OpenHands 与其它 ACP harnesses](https://github.com/OpenHands/software-agent-sdk/issues/4627)**（8月25日新建）— 一个横跨多 repo 的 umbrella issue，目标是构建「harness 中立遥测」的自动化对比评估平台，与项目近期对 eval 基础设施的投入（#3949）方向一致。
- **[#4624 — 从 Gemini CLI 迁移至 Antigravity CLI (agy)](https://github.com/OpenHands/software-agent-sdk/issues/4624)** — Google 已宣布 Gemini CLI 退役，迁移到 Antigravity CLI 是 ACP 开发体验的刚需，目前处于 `ready-for-dev`，预计会被排入开发队列。
- **[#4626 — 澄清 readiness 检查评论并引用模板](https://github.com/OpenHands/software-agent-sdk/issues/4626)** — 已合入 PR [#4625](https://github.com/OpenHands/software-agent-sdk/pull/4625)，完成闭环。

**💡 长期/架构级需求（有待评估）：**

- [#4187](https://github.com/OpenHands/software-agent-sdk/issues/4187) — 支持 server-owned 会话 + 远程执行专用 workspace（架构级改动）
- [#3907](https://github.com/OpenHands/software-agent-sdk/issues/3907) — 将子代理（TaskToolSet）事件转发到父会话实时流
- [#4239](https://github.com/OpenHands/software-agent-sdk/issues/4239) 与 [#4240](https://github.com/OpenHands/software-agent-sdk/issues/4240) — 跨仓库感知与 CLI/GUI 共享会话历史，均为 roadmap 级用户诉求

---

## 7. 用户反馈摘要

从今日 Issues/PR 的评论中可提炼以下真实用户声音：

- **对于并发/阻塞类 Bug，用户表达「卡死即不可用」的强烈挫败感：** [#4546](https://github.com/OpenHands/software-agent-sdk/issues/4546) 作者描述"Everything looked healthy. I got two 200s back, but every attempt to open the conversation just ti…"，自托管环境下健康检查通过但实际操作全部卡死，此类问题对自托管用户的信任伤害较大。
- **对 API 语义有精细化诉求：** [#4577](https://github.com/OpenHands/software-agent-sdk/issues/4577) 用户明确指出 `UpdateConversationRequest.tags` 的整表替换语义「correctly documented but operationally次优」，期望提供增量更新的端点，是典型的平台化演进需求。
- **对「静默降级」表达不满：** [#3495](https://github.com/OpenHands/software-agent-sdk/issues/3495) 中视觉能力未被检测导致集成测试被 `SKIPPED`，用户并非直接抱怨测试跳过，而是对运行时能力检测不可靠表示担忧。
- **社区对自动化流程噪音有感知：** [#4633](https://github.com/OpenHands/software-agent-sdk/issues/4633) 是项目自身为验证 event-triggered triage 自动化而创建的测试 issue，被标记为「请忽略」。虽为内部测试，但侧面说明流程切换期会有少量噪音。
- **积极信号：** 用户在 PR 中多次反馈「Validated. Human thinks this is correct also.」（如 [#4623](https://github.com/OpenHands/software-agent-sdk/pull/4623)），说明 AI 驱动开发流程在人工复核下质量得到认可。

---

## 8. 待处理积压

以下为值得维护者关注、但已长时间未获回应的重大问题：

- **[#4239 — Multi-repo/Cross-repo Awareness](https://github.com/OpenHands/software-agent-sdk/issues/4239)** — 创建于 2025-09-23，近一年只有 1 条评论，是社区高赞需求（+1），涉及跨仓库依赖上下文感知，属于重大路线图能力，建议官方给出明确排期。
- **[#4240 — Conversations should be shared between CLI and GUI](https://github.com/OpenHands/software-agent-sdk/issues/4240)** — 创建于 2025-10-31，+2 赞，至今仅有 2 条评论。该诉求直接影响 CLI + GUI 双端用户的日常体验，优先级应高于许多新建 issue。
- **[#4187 — Support server-owned conversations with remote execution-only workspaces](https://github.com/OpenHands/software-agent-sdk/issues/4187)** — 创于 2026-07-22，当前仅 1 条维护者评论，这是「OpenHands 走向多用户服务端部署」的关键架构能力，建议纳入架构组评审。
- **[#3673 — feat(sdk): add ask_oracle tool](https://github.com/OpenHands/software-agent-sdk/pull/3673)** — 自 2026-06-11 发起至今已超过 2 个月未合并，仍标记为 `integration-test` 与 `review-this`

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-26

## 1. 今日速览

过去 24 小时 Pi 项目保持高速迭代节奏：共 226 条 Issue 更新，其中 **209 条已关闭、17 条新开/活跃**；PR 更新 32 条，**24 条已合并/关闭、8 条待合并**。无新版本发布。合并的 PR 覆盖了 Bedrock 图片兼容、Opper 新 Provider、eager tool execution、read 工具行数计算修复等多项功能与稳定性改进。社区讨论热度集中在 Windows 支持、Claude 模型 edit 工具兼容性以及 auto-compaction 触发机制三个焦点上。综合来看，项目合并效率高、Issue 清理及时，整体健康度良好。

---

## 3. 项目进展

今日无新版本发布，但通过 PR 合并推进了多项实质性改进：

| 方向 | PR | 内容 |
|---|---|---|
| 新 Provider | [#8639](https://github.com/earendil-works/pi/pull/8639) | 新增 **Opper** 内置 OpenAI 兼容 Provider（含模型目录、注册、文档） |
| 模型兼容 | [#8642](https://github.com/earendil-works/pi/pull/8642) | 修复 Bedrock 上 OpenAI 模型拒绝 `toolResult` 内嵌图片的问题，将图片提升为同级 content block |
| 模型兼容 | [#8633](https://github.com/earendil-works/pi/pull/8633) | 修复 Responses API 在 compaction 时发送无 tools 的 `tool_choice: none` 导致部分 Provider 拒绝请求的问题 |
| 模型兼容 | [#8570](https://github.com/earendil-works/pi/pull/8570) | 为 OpenAI Codex 请求补齐 `thread-id` affinity header，维护会话亲和性 |
| 模型兼容 | [#8614](https://github.com/earendil-works/pi/pull/8614) | 修复 OpenRouter reasoning-mandatory 模型（如 `stealth/ox-alpha`）因显式 `reasoning:{effort:"none"}` 被拒绝的问题 |
| 新功能 | [#8629](https://github.com/earendil-works/pi/pull/8629) | 引入 **eager tool execution**（opt-in）：对 finalize 且显式 discard-safe 的本地 `read` 调用提前预执行，正常 dispatch 时直接复用结果 |
| Bug 修复 | [#8623](https://github.com/earendil-works/pi/pull/8623) | 修复 `read` 工具将文件末尾换行误计为一行的 phantom line 问题（影响截断提示、续读 hint 等） |
| Bug 修复 | [#8627](https://github.com/earendil-works/pi/pull/8627) | 扩展工具（read/write/edit/grep 等）改为优先使用 `ctx.cwd`（会话真实 cwd），避免并发会话路径错乱 |
| Bug 修复 | [#8641](https://github.com/earendil-works/pi/pull/8641) | 当 `bash` 可用而 `read` 不可用时正确加载 skills 段，并补充系统提示回归测试 |
| TUI | [#8547](https://github.com/earendil-works/pi/pull/8547) | （待合并）支持鼠标点击将 editor 光标移动到目标位置，提升 TUI 编辑体验 |

> 注：以上基于展示的 20 条 PR（共 32 条）统计，其余 12 条未展示。

---

## 4. 社区热点

| Issue/PR | 讨论热度 | 核心诉求 |
|---|---|---|
| [#7547](https://github.com/earendil-works/pi/issues/7547) — [Windows] 如何使用 Pi？遇到了什么问题？ | **49 评论**，开放中 | 大量 Windows 开发者反馈运行方式碎片化（WSL/原生/pwsh 等），希望官方明确推荐路径并集中修复核心 bug |
| [#6278](https://github.com/earendil-works/pi/issues/6278) — Claude 新模型与 edit 工具兼容问题 | 24 评论，10 👍，已关闭 | Claude 模型在 edit 调用中会生成 `new_text_x`、`closeenough` 等额外字段，导致约 **20% 编辑失败**，验证错误来自 extra properties |
| [#6879](https://github.com/earendil-works/pi/issues/6879) — auto-compaction 在上下文超 100% 后仍不触发 | 23 评论，**19 👍**，开放中 | 长时 agentic 任务中 footer 持续超过阈值直到 API 在 373k tokens 拒绝请求，compaction 才被触发；用户希望每个 agent turn 后都主动检查 |
| [#8584](https://github.com/earendil-works/pi/issues/8584) — TUI 流式输出行损坏 | 8 评论，5 👍，已关闭 | 工具输出长行后 assistant 文本被拆成每行一个单词，疑似渲染宽度状态错乱 |

**分析**：Windows 支持是当前社区呼声最高的平台诉求；Claude 模型兼容性直接影响日常使用效率；而 **auto-compaction 机制缺陷**（#6879）关注度最高（19 👍），说明长会话用户对 token 成本与任务连续性高度敏感。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue | 描述 | 状态/对应修复 |
|---|---|---|---|
| 🔴 高 | [#6879](https://github.com/earendil-works/pi/issues/6879) | auto-compaction 在上下文超 100% 后仍不触发，直到 provider 报错；长任务 token 浪费 | 开放中，无 fix PR |
| 🔴 高 | [#6278](https://github.com/earendil-works/pi/issues/6278) | Claude 新模型 edit 工具约 20% 失败率（额外字段导致 validation 错误） | 已关闭 |
| 🟠 中 | [#8409](https://github.com/earendil-works/pi/issues/8409) | 回归：abort 后 `stopReason` 为 `"error"` 而非 `"aborted"` | 已有修复 PR [#8635](https://github.com/earendil-works/pi/pull/8635)（待合并） |
| 🟠 中 | [#8642](https://github.com/earendil-works/pi/pull/8642) | Bedrock OpenAI 模型拒绝 `toolResult` 内嵌图片，导致带图 tool 结果后会话失败 | 已合并 |
| 🟠 中 | [#8584](https://github.com/earendil-works/pi/issues/8584) | TUI 流式输出行损坏（工具长输出后 assistant 文本逐词换行） | 已关闭 |
| 🟠 中 | [#8434](https://github.com/earendil-works/pi/issues/8434) | v0.84.2 TUI 无响应、输入回显乱码（Ubuntu 24.04.4 / VS Code 终端） | 已关闭

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-26

## 1. 今日速览

过去24小时内，LiteLLM 项目保持高活跃度：**94 条 Issues 更新**（其中 62 条新开或活跃、32 条已关闭）与 **261 条 PR 更新**（其中 92 条已合并/关闭、169 条待合并），表明社区反馈与核心开发双线并行。值得关注的是，本周合并/关闭的 PR 集中于 **Anthropic Messages Responses 桥接修复**（文档块丢失）、**Together AI 兼容性优化**、**Bing Grounding 搜索提供商新增**等方向，说明项目当前正积极补齐主流 provider 的协议兼容性与能力对齐。新版本发布数为 0，但 PR 合并节奏较快，预计近期将有新版本释出。整体项目健康度良好，社区诉求响应及时，但存在少量长期未关闭的旧 Issue 需关注。

---

## 2. 版本发布

过去24小时内 **无新版本发布**。不过考虑到今日合并/关闭了 92 条 PR（含多项功能新增与修复），预计下一版本（可能为 v1.97.x 或 v1.98.0）将包含较多变化，建议关注 Release 页面。

---

## 3. 项目进展

今日合并/关闭的 PR 中，以下几项值得注意，它们分别在 **协议桥接、Provider 兼容性、搜索能力** 三个维度推进了项目：

| PR | 内容 | 状态 | 意义 |
|---|---|---|---|
| [#38267](https://github.com/BerriAI/litellm/pull/38267) | `/v1/messages` 用户内容中的 document 块现在会正确转换为 Responses API 的 `input_file` 部分，不再丢失 PDF 等文件 | 已关闭 | 修复 Anthropic → OpenAI 桥接时文件丢失的缺陷 |
| [#38261](https://github.com/BerriAI/litellm/pull/38261) | `tool_result` 中的 document 块同样转换为 `input_file` 部分，Claude Code 通过网关的 PDF 读取不再只剩文本 stub | 已关闭 | 补齐工具结果中的多模态内容桥接 |
| [#38265](https://github.com/BerriAI/litellm/pull/38265) | 对未注册在 registry 中的 Together AI 模型，工具调用默认 **fail open**（透传并由上游验证），而非直接 400 或静默剥离 | 已关闭 | 提升未收录模型的可用性 |
| [#38119](https://github.com/BerriAI/litellm/pull/38119) | 新增 **Bing Grounding** 作为搜索提供商，支持 Foundry Responses API 的 `/v1/search` 与 chat webserach 拦截 | 已合并 | 扩展搜索提供商生态 |
| [#38252](https://github.com/BerriAI/litellm/pull/38252) | 优化 PR 模板：Caveats 按严重程度分级，并明确要求使用平实的工程语言 | 已关闭 | 内部工程流程改进 |

此外仍有 169 条 PR 待合并，其中包括 MCP OAuth Token 清理与重新授权（[#36831](https://github.com/BerriAI/litellm/pull/36831)）、共享 JSONFragmentAccumulator 流式性能优化（[#36610](https://github.com/BerriAI/litellm/pull/36610)）等。

---

## 4. 社区热点

今日讨论热度最高的 Issues 集中在 **Claude 空内容 bug**、**功能请求聚合帖** 与 **代理集成问题**：

- **[#18686](https://github.com/BerriAI/litellm/issues/18686)（21 条评论）**：LiteLLM 社区的 Models / Providers / Endpoints 功能请求与投票中心。该帖长期置顶，持续吸引用户对新增模型/提供商支持的诉求，是产品路线图的重要参考。
- **[#24498](https://github.com/BerriAI/litellm/issues/24498)（10 条评论）**：使用 Claude 模型时，LiteLLM 偶尔直接返回 `[System: Empty message content sanitised to satisfy protocol]`，用户困惑且影响输出质量，是今日最热门的 bug 讨论。
- **[#22878](https://github.com/BerriAI/litellm/issues/22878)（7 条评论，已关闭）**：Claude Code 2.1.69 通过 LiteLLM 代理 GitHub Copilot 模型时出现 `Bad Request`，最终被关闭（stale），但获得 2 个 👍，说明有一定影响面。
- **[#22173](https://github.com/BerriAI/litellm/issues/22173)（6 条评论，已关闭）**：最新 Helm Chart 指向不存在的镜像，导致 `ImagePullBackOff`。该问题获得 5 个 👍，是用户部署时的高频痛点，但最终被作 stale 关闭，可能需要重新确认是否真正修复。

**诉求分析**：社区讨论的热点呈现出两个方向——一是对 **模型/提供商覆盖度** 的持续需求（#18686），二是对 **主流工具链（Claude Code、Helm）集成稳定性** 的高敏感度。

---

## 5. Bug 与稳定性

今日报告的 Bug 中，按严重程度排序如下：

**高严重度**

- **[#38202](https://github.com/BerriAI/litellm/issues/38202)（新开）**：LiteLLM 与 Python 3.10 存在兼容性问题，且被外部项目（deepset-ai/haystack-core-integrations）汇总指出多处问题。考虑到 Python 3.10 仍有大量用户，此问题可能影响 SDK 的安装与使用，建议尽快响应。目前已获 2 条评论。
- **[#36926](https://github.com/BerriAI/litellm/issues/36926)（持续活跃）**：持续负载下错误触发 `BudgetExceededError`（429），报告显示 `Current cost = max_budget + recent spend`，无 Redis 环境下约 2 分钟自愈。该问题涉及预算模块的竞态条件，影响生产计费正确性，值得优先排查。已获 4 条评论与 1 个 👍。

**中严重度**

- **[#34614](https://github.com/BerriAI/litellm/issues/34614)**：Redis 缓存/预算计数器在 v1.93.0 中因 `ssl_check_hostname` 参数不被 `AbstractConnection.__init__` 接受而失败。环境为 Docker 镜像 `litellm-database:v1.93.0`，影响使用 Redis over TLS 的用户。已获 4 条评论。
- **[#28735](https://github.com/BerriAI/litellm/issues/28735)**：合成的 `include_usage` chunk 违反 OpenAI spec——usage 事件中带有非空 choices 而非 `choices: []`。与已关闭的 #8450 同症状，#8751 的修复 PR 未合并。已获 4 条评论。
- **[#38180](https://github.com/BerriAI/litellm/issues/38180)（新开）**：`n>1` + `stream=True` 时，多个流式 completion 被合并为一次计费与日志记录。涉及计费准确性。

**低严重度 / 边缘场景**

- **[#28499](https://github.com/BerriAI/litellm/issues/28499)**：模型名含多个 `/` 时 webserach 拦截失败，错误路由到 `openai` provider。
- **[#28568](https://github.com/BerriAI/litellm/issues/28568)**：Anthropic Messages 适配器在非 Anthropic 后端时，`response.id` 与 spend logs 的 `request_id` 不一致。
- **[#24004](https://github.com/BerriAI/litellm/issues/24004)**：Anthropic `/v1/messages` 路由类型不支持流式中途 fallback。

---

## 6. 功能请求与路线图信号

今日用户提出的功能请求中，以下方向值得关注：

- **Workload Identity Federation（OIDC）支持**：[#31649](https://github.com/BerriAI/litellm/issues/31649)（OpenAI）与 [#28607](https://github.com/BerriAI/litellm/issues/28607)（Anthropic）均请求支持 OIDC token exchange。这两个请求分别获得 1 个和 3 个 👍，说明企业用户对云环境下的无密钥认证有明确需求，但当前未见到对应 PR，建议纳入路线图评估。
- **Azure AI 非 chat 路径的 Entra ID token fallback**：[#37727](https://github.com/BerriAI/litellm/issues/37727) 请求 `azure_ai/` 的 image generation 与 OCR 路径支持 `enable_azure_ad_token_refresh`。属于对已有能力的补齐，优先级可能中等。
- **Vertex AI Gemini 结构化输出通道可选**：[#34943](https://github.com/BerriAI/litellm/issues/34943) 请求允许用户放弃自动的 `responseJsonSchema`，改用原生 `responseSchema`。**已有关联 PR**：[#38255](https://github.com/BerriAI/litellm/pull/38255) 正在实现该功能，大概率会进入下个版本。
- **Fireworks AI 成本条目更新**：[#37274](https://github.com/BerriAI/litellm/issues/37274) 请求补充 Fireworks Serverless 模型的最新成本数据。
- **Together AI reasoning_effort 映射**：虽然未出现在 Issue 中，但 PR [#38263](https://github.com/BerriAI/litellm/pull/38263) 正在为不同 model class 映射 `reasoning_effort` 的合法值，说明团队正在主动补齐该能力。

---

## 7. 用户反馈摘要

从今日 Issues 与 PR 评论中提炼的用户声音：

- **对 Claude 空内容输出感到困惑**（#24498）：用户报告使用 Claude 模型时偶发返回 `[System: Empty message content sanitised to satisfy protocol]` 的占位文字，而非真实错误。这既影响下游输出质量，也增加了排查成本。
- **Helm Chart 镜像不存在的低级错误影响信任**（#22173）：用户按照官方文档部署遭遇 `ImagePullBackOff`，问题虽已 stale 关闭，但对新用户上手体验伤害较大。
- **对 Python 3.10 兼容性下降表示担忧**（#38202）：用户直言 "we're veering off course with Python 3.10+ compat"，说明开发者社群对兼容性回归较为敏感。
- **预算计算在高负载下误报**（#36926）：用户描述了具体的复现场景（100-130 请求/40 分钟），说明生产环境下的稳定性问题会影响计费可信度。
- **MCP/工具调用链路的可观测性不足**（#37358）：用户反馈 streaming `/responses` 中链式 MCP 工具调用只在 spend logs 中记录了第一次工具调用和第一次 LLM 轮次，其余被吞。说明 gateway 编排场景下的计量需求在上升。
- **对小众/边缘 Provider 的成本与元数据准确性有要求**（#25950、#37274、#37584）：用户积极报告 `cache_read_input_token_cost` 未生效、模型条目缺失或价格数据过时等问题，体现出社区对成本核算精度的重视。

---

## 8. 待处理积压

以下 Issue / PR 长期开放但未获足够关注，建议维护团队评估：

| 编号 | 创建时间 | 最后更新 | 问题 | 备注 |
|---|---|---|---|---|
| [#12793](https://github.com/BerriAI/litellm/issues/12793) | 2025-07-21 | 2026-08-25 | `pip install` 在定义 `url_database` 时崩溃 | 已开放超过一年，影响自托管部署 |
| [#22878](https://github.com/BerriAI/litellm/issues/22878) | 2026-03-05 | 2026-08-25 | Claude Code 2.1.69 代理 GitHub Copilot 时 `Bad Request` | 今日被 stale 关闭，但获 2 个 👍，有用户仍受影响 |
| [#24004](https://github.com/BerriAI/litellm/issues/24004) | 2026-03-18 | 2026-08-25 | Anthropic `/v1/messages` 路由不支持流式中途 fallback | 获 2 个 👍，关联上游 Anthropic SSE 错误处理 |
| [#28607](https://github.com/BerriAI/litellm/issues/28607) | 2026-05-22 | 2026-08-25 | 支持 Anthropic Workload Identity Federation | 获 3 个 👍，企业认证需求明确 |
| [PR #35419](https://github.com/BerriAI/litellm/pull/35419) | 2026-07-31 | 2026-08-25 | `/rerank` 接口缺失 latency 与 cost headers | 由 devin-ai 提交，开放近一个月，建议 review |

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-26


## 1. 今日速览

过去 24 小时 Temporal 项目保持了较高的开发活跃度，PR 活动量显著（69 条更新），主要集中于 Scheduler V1→V2 迁移、XDC 缓冲事件覆盖、worker 命令任务队列等方向。Issue 侧更新量较少（4 条），且全部处于开放状态，无新关闭的 Issue，整体问题解决节奏有所放缓。合并/关闭 PR 18 条，说明部分长期推进的工作已完成落地。新版本发布为 0，项目处于功能积累和合并阶段，而非发布周期。项目整体健康度良好，但需注意 Issue 关闭率偏低的问题。

---

## 2. 版本发布

过去 24 小时内无新版本发布。

---

## 3. 项目进展

今日关闭/合并的 PR 中，以下几项反映了项目实质性的进展：

- **[#11556] Isolate ALLOW_ALL schedule completion state**（已关闭）：修复 CHASM Scheduler V2 中 `ALLOW_ALL` 重叠策略未正确隔离完成状态的问题，与 V1 行为对齐。来源：https://github.com/temporalio/temporal/pull/11556
- **[#11411] Add version to deletion workflow replication task**（已关闭）：删除执行的复制任务现在携带 failover version，并在 apply 时跳过旧版本，增强了多集群删除操作的一致性保障。来源：https://github.com/temporalio/temporal/pull/11411
- **[#11631] Align CHASM ALLOW_ALL lifecycle with V1**（已关闭）：确保所有 CHASM scheduler workflow start（包括 `ALLOW_ALL` 场景）都附加完成回调，以保障滚动升级期间 start 请求的安全性。来源：https://github.com/temporalio/temporal/pull/11631
- **[#11785] Clean up LRU cache test assertions**（已关闭）：清理大量 linter 问题（数百个），属于代码质量基础设施改进。来源：https://github.com/temporalio/temporal/pull/11785
- **[#11481] Skip worker commands task queues in missing TQ check**（已关闭）：在版本升级（SetCurrent/SetRamping）的缺失任务队列检查中，跳过 SDK worker 使用的系统任务队列（`temporal-sys/worker-commands/...`），避免误报。来源：https://github.com/temporalio/temporal/pull/11481

整体来看，Scheduler 相关修复与复制/多集群方向（reliability-2026）的任务推进明显，项目正在系统地收敛 V1→V2 迁移的兼容性问题。

---

## 4. 社区热点

以下 Issue/PR 是近期讨论最集中、关注度最高的条目：

- **[#10888] 为 archival task executor 增加 ActiveInCluster 检查**（2 条评论）：用户指出全局命名空间中 active 和 standby 集群都在执行归档任务，给归档系统带来额外压力。讨论背后是对多集群复制场景下资源浪费的普遍关注。链接：https://github.com/temporalio/temporal/issues/10888
- **[#10841] SignalWithStart 在孤儿 current-execution 指针上永久挂起**（2 条评论）：该 Issue 已开放两个月，用户报告 `SignalWithStartWorkflowExecution` 在某些情况下不做任何进展，直到客户端超时。这类问题直接影响生产可用性，评论区有持续跟进。链接：https://github.com/temporalio/temporal/issues/10841
- **[#11743] PostgreSQL 分页查询改用 tuple cursors**（2 条评论）：贡献者提出两个 PostgreSQL 分页查询仍在使用基于 OR 的复合游标，导致查询计划器无法高效利用索引范围，深分页时性能线性恶化。链接：https://github.com/temporalio/temporal/issues/11743
- **[#11589] Worker-variant callbacks**（开放中）：大规模功能 PR，实现 Worker 回调能力。虽然目前合并到 feature 分支，但社区关注度高，属于 SDK 侧重大功能。链接：https://github.com/temporalio/temporal/pull/11589
- **[#9076] Programmable grpc fault injection**（开放中）：已开放超 7 个月，为功能性测试引入 gRPC 故障注入能力，属于测试基础设施的长期持续改进。链接：https://github.com/temporalio/temporal/pull/9076

---

## 5. Bug 与稳定性

按严重程度排列：

1. **高 — SignalWithStart 永久挂起**（[#10841](https://github.com/temporalio/temporal/issues/10841)）
   - 现象：orphaned current-execution 指针导致 `SignalWithStartWorkflowExecution` 不推进、不返回。
   - 影响：API 层面死等，影响工作流可靠性和用户 SLA。
   - 状态：开放中，尚无关联 fix PR。

2. **中 — 双集群重复归档**（[#10888](https://github.com/temporalio/temporal/issues/10888)）
   - 现象：active 和 standby 集群同时执行 archival，增加归档系统压力。
   - 影响：潜在资源浪费和重复数据写入。
   - 状态：开放中，已有解决方案讨论但未落地。

3. **中 — Scheduler ALLOW_ALL 策略处理不符合 V1 语义**（[#11556](https://github.com/temporalio/temporal/pull/11556) / [#11631](https://github.com/temporalio/temporal/pull/11631)）
   - 现象：CHASM Scheduler V2 中 `ALLOW_ALL` 重叠完成状态未正确隔离。
   - 影响：可能引起 schedule 回调丢失或错误完成状态。
   - 状态：已修复并合并，进入发布流程。

4. **低 — PostgreSQL 深分页性能退化**（[#11743](https://github.com/temporalio/temporal/issues/11743)）
   - 现象：OR-based composite cursor 导致查询规划器无法使用复合索引边界，深分页时线性退化。
   - 影响：大规模 PostgreSQL 部署的 list/scan API 性能下降。
   - 状态：开放中，已有初步 PR 意愿。

5. **低 — worker 命令任务队列被误报为缺失**（[#11481](https://github.com/temporalio/temporal/pull/11481)）
   - 现象：版本提升检查中 SDK worker 系统队列被误判。
   - 影响：版本发布流程中可能出现误报。
   - 状态：已修复并合并。

---

## 6. 功能请求与路线图信号

- **[#11780] Expose `connectAttributes` to PostgreSQL**：用户请求在 PostgreSQL 数据存储配置中支持 `connect_timeout` 等连接属性。目前 `config_template.yaml` 只对 MySQL8 暴露该选项。属于配置能力补全，社区有真实需求。链接：https://github.com/temporalio/temporal/issues/11780
- **[#10888] archival 的 ActiveInCluster 检查**：在 replication 场景下避免 active 和 standby 同时归档，若被接受，将纳入 multi-cluster 可靠性改进路线。链接：https://github.com/temporalio/temporal/issues/10888
- **Worker callbacks（[#11589]）**：可作为 Temporal 近期一个重要功能方向，实现 Worker 侧回调能力，已在 feature 分支推进。
- **动态分区负载均衡改进（[#11699]）**：使用 AddTask 到 root partition 的概率来估算整体任务速率，替代均匀分布假设，提升动态分区的自适应能力。链接：https://github.com/temporalio/temporal/pull/11699
- **批处理操作迁移至 system namespace（[#11509]）**：将 admin batch 运行在 `temporal-system`，改进多 namespace 的运维与管理方式。链接：https://github.com/temporalio/temporal/pull/11509

---

## 7. 用户反馈摘要

从近期 Issue 评论中可提炼出以下用户声音：

- **PostgreSQL 用户关注深分页性能**（[#11743](https://github.com/temporalio/temporal/issues/11743)）：用户在大型 Temporal 部署中遇到列表/查询类 API 随游标深入性能线性下降的问题，对索引优化有明确诉求。这说明 PostgreSQL 生产部署规模在扩大，性能和扩展性问题开始浮现。
- **SignalWithStart 可靠性困扰**（[#10841](https://github.com/temporalio/temporal/issues/10841)）：用户明确指出 API 调用在客户端 deadline 内没有任何进展，对系统透明性表示不满。此类问题一旦触发，对线上工作流运行的信心打击较大。
- **多集群归档资源消耗的担忧**（[#10888](https://github.com/temporalio/temporal/issues/10888)）：来自维护者（@tsurdilo）的反馈，指出 active/standby 双写对 archival 管线造成额外压力。说明团队自身也在积极审视复制场景的资源效率。
- **配置能力不对等**（[#11780](https://github.com/temporalio/temporal/issues/11780)）：用户通过 `temporalio/auto-setup` 镜像使用 PostgreSQL 时，发现 `connect_timeout` 无法配置，而 MySQL8 可以，体现出不同数据库后端配置能力不一致带来的使用摩擦。

---

## 8. 待处理积压

以下 Issue/PR 开放时间较长或对项目健康度影响较大，提醒维护者关注：

- **[#10841] SignalWithStart 挂起问题** — 已开放 2 个月，属于高影响 bug，目前无 fix PR，建议优先排查。链接：https://github.com/temporalio/temporal/issues/10841
- **[#10888] archival ActiveInCluster 检查** — 已开放近 2 个月，有明确改进方案但未落地。链接：https://github.com/temporalio/temporal/issues/10888
- **[#9076] Programmable gRPC fault injection** — 已开放超 7 个月，功能测试基础设施的重要增强，长期未合并，可能影响测试能力的迭代。链接：https://github.com/temporalio/temporal/pull/9076
- **[#11743] PostgreSQL tuple cursor 优化** — 开放不到一周，但涉及数据库查询性能优化，是明确的社区贡献机会，建议维护者提供 review 指导。链接：https://github.com/temporalio/temporal/issues/11743
- **[#11509] admin batch 运行在 temporal-system** — 开放2周，功能性 PR，涉及批量操作运维方式的改进，建议推进 review。链接：https://github.com/temporalio/temporal/pull/11509

---

**总结**：Temporal 项目当前处于活跃开发期，Scheduler 和 replication 可靠性方向的修复持续落地，社区贡献活跃，整体健康。需要重点关注 SignalWithStart 挂起问题的根因定位，以及 PostgreSQL 配置/性能相关反馈的响应速度。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*