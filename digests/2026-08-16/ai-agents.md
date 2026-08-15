# OpenClaw 生态日报 2026-08-16

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-15 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，这是 2026-08-16 的 OpenClaw 项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-08-16

> **数据时效性声明：** 本次提供的数据快照（截至 2026-08-15 23:59 UTC）包含 500 条 Issue 与 500 条 PR 更新，但所有展示条目的最后更新时间均停留在 2026-08-15，**没有实际落入 8 月 16 日 24 小时窗口内的新增数据**。因此，本报告基于最近完整活跃周期（8 月 14-15 日）的数据生成，以反映项目当前的真实状态。

---

## 1. 今日速览

OpenClaw 在 8 月 15 日保持高强度迭代，尽管存在大量标记为 `clawsweeper:needs-*` 等待维护者/产品决策的 Issue，但核心 PR 流水线活跃，已有多个 **P1 修复**（如 Windows Cron、claude-cli 缓存）进入待合并状态。**稳定性问题仍是社区关注焦点**：大量 P1 级 Bug 集中在消息丢失、会话状态错乱和崩溃循环上，且不少处于“需实时复现”阶段。**新版本 v2026.8.1-beta.2 已发布**，重点加强 Secret 出口绑定及 GPT-5.6 Ultra 支持。总体来看，项目功能推进迅速，但**技术债务与回归问题（特别是多通道消息丢失）正在显著消耗社区信任与维护者精力**。

---

## 2. 版本发布

### v2026.8.1-beta.2
**发布时间：** 2026-08-15
**链接：** [OpenClaw 2026.8.1-beta.2](https://github.com/openclaw/openclaw/releases)

**主要更新内容：**

1. **Secret egress host binding（安全强化）**
   - 将共享存储中的 Secret 严格绑定到 HTTPS 目标主机（覆盖 CLI、Gateway RPC 和 Control UI）。
   - 若未绑定 sentinel 则直接失败关闭，防止明文外泄。
   - *致谢：@shakkernerd*

2. **GPT-5.6 Ultra 与运行时切换**
   - 支持 GPT-5.6 Ultra 模型。
   - 新增运行时切换能力，允许在不同模型后端之间动态迁移。

**关于破坏性变更与迁移：** 由于 Secret 绑定策略收紧，使用共享存储 Secret 且未显式配置目标 Host 的部署在升级后可能遭遇“失败关闭”（fail closed）。**建议所有生产环境用户在升级前检查 Secret 配置，确保已绑定正确的 egress 主机。**

---

## 3. 项目进展

过去 24 小时内有 46 个 PR 被合并/关闭，以下为已合入主干的**关键工作**（基于快照中标注为 CLOSED 的 PR）：

| PR | 标题 | 状态 | 影响 |
|---|---|---|---|
| [#124209](https://github.com/openclaw/openclaw/pull/124209) | fix: keep Codex plugin aligned during stable upgrades | ✅ Merged | 修复稳定版升级时 Codex 插件配置报错的问题，提升升级平滑度。 |
| [#116489](https://github.com/openclaw/openclaw/pull/116489) | feat(security): require acknowledgement for install policy warnings | ✅ Merged | **重大安全特性**：新增 `installPolicy` 警告确认机制，防止恶意插件/技能被静默安装。 |
| [#120900](https://github.com/openclaw/openclaw/pull/120900) | feat(ui): review install policy warnings | ✅ Merged | 配合上一个 PR，在 Control UI 中提供管理员审核并批准安装的功能。 |
| [#124257](https://github.com/openclaw/openclaw/pull/124257) | fix(ui): stop inferring session sharing identity kind from ID strings | ✅ Merged | 修复 UI 将 ID 中包含 `channel:` 字符串的用户误判为频道的渲染 bug。 |
| [#124261](https://github.com/openclaw/openclaw/pull/124261) | fix(ui): use native placement for the lobster dismiss menu | ✅ Merged | 修复 UI 组件（龙虾宠物菜单）在不同窗口尺寸下定位偏移的问题。 |

**进展评估：** 核心进展集中在**安全加固**与 **UI 体验修复**。特别是 `installPolicy` 警告确认机制的上线，对于防范供应链攻击具有重要意义。相对于 500 条的 PR 总量，合并率（9.2%）偏低，大量 PR 因 `needs proof` 或 `waiting on author` 而停滞，**维护者带宽是当前主要瓶颈**。

---

## 4. 社区热点

以下是在数据快照中讨论最热烈、最能反映社区诉求的 Issue：

### 1. [ #91009 ](https://github.com/openclaw/openclaw/issues/91009) — Codex PreToolUse 钩子导致 CPU 飙升与 Gateway RPC 停滞
- **评论/回应：** 20 条 | **👍：** 2
- **核心诉求：** 使用 `@openclaw/codex` 集成时，Codex 的 `pre_tool_use` 事件触发大量 `openclaw-hooks` 进程，每个进程占用 100%+ CPU，最终拖垮整个 Gateway。
- **热点分析：** 这是 **P1 级性能/崩溃问题**，直接冲击核心工作流。评论数最多表明有大量用户遭遇类似问题，且急切希望官方给出解决方案。

### 2. [ #121953 ](https://github.com/openclaw/openclaw/issues/121953) — Cron 任务在 DeepSeek 上因消息前缀被降优先级而卡死
- **评论/回应：** 19 条
- **核心诉求：** 由 OpenClaw 生成的 `[cron:<jobId> <name>] ` 前缀导致 DeepSeek API 将该请求视为低优先级，从而出现数十秒到数分钟的停顿。
- **热点分析：** 暴露了**第三方模型兼容性**问题。随着 DeepSeek 等国产模型的普及，用户对非 OpenAI/Anthropic 模型的适配要求越来越高。

### 3. [ #79902 ](https://github.com/openclaw/openclaw/issues/79902) — 增加 Companion 友好的 SQLite 转录/会话接口
- **评论/回应：** 13 条 | **👍：** 2
- **核心诉求：** 希望在新版 database-first 运行时之上，提供稳定的 SQLite 层接口，方便外部工具读取会话数据，而不必解析不透明的二进制 blob。
- **热点分析：** 这是**高级用户与生态开发者**的呼声，代表社区希望 OpenClaw 不仅仅是一个聊天机器人，更是一个可编程的 AI 代理平台。

### 4. [ #69208 ](https://github.com/openclaw/openclaw/issues/69208) — 伞形 Issue：多通道下的重复转录、回放与会话组装问题
- **评论/回应：** 13 条
- **核心诉求：** 该 Issue 汇总了 MSTeams、webchat、Telegram、followup 队列等多个通道中出现的**重复消息**问题，指向一个共通的根因。
- **热点分析：** 这是**跨通道的系统性架构问题**，用户在多个平台均遇到类似 bug，极易引发社区对核心架构稳定性的担忧。

---

## 5. Bug 与稳定性

### 严重级别：P0（紧急）

| Issue | 标题 | 影响 | 是否有 Fix PR |
|---|---|---|---|
| [#70903](https://github.com/openclaw/openclaw/issues/70903) | 持久化文件级 Provider 冷却导致账单恢复后仍被屏蔽数小时 | 用户充值后仍无法使用服务，**直接损失** | ❌ 无（已 stale） |

### 严重级别：P1（高）

| Issue | 标题 | 影响 | 是否有 Fix PR |
|---|---|---|---|
| [#91009](https://github.com/openclaw/openclaw/issues/91009) | Codex PreToolUse 钩子 CPU 占用过高且阻塞 RPC | **崩溃循环**、消息丢失 | ❌ 无 |
| [#121953](https://github.com/openclaw/openclaw/issues/121953) | DeepSeek 上 Cron 任务因前缀被降级而卡死 | 任务停滞 | ❌ 无 |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | 2026.3.2 版本 Google Vertex/Gemini 报 "Cannot convert undefined" | **回归**，核心功能不可用 | ❌ 无（已存留数月） |
| [#103231](https://github.com/openclaw/openclaw/issues/103231) | `claude-cli` 后端错误声明原生压缩能力，导致会话无限制膨胀 | **会话状态**损坏、恢复路径失效 | ❌ 无 |
| [#123799](https://github.com/openclaw/openclaw/issues/123799) | 生产环境受 Codex compact 404 影响，亟需升级/回退指南 | **数据/服务不可用**，运营受阻 | ❌ 无（已关闭，无后续指引） |
| [#119333](https://github.com/openclaw/openclaw/issues/119333) | Codex 在 Default 模式下暴露 `request_user_input` 工具但运行时拒绝 | 功能行为不一致 | ❌ 无 |
| [#92241](https://github.com/openclaw/openclaw/issues/92241) | Gateway 在更新/回滚后持有陈旧模块路径，静默丢弃消息 | **消息丢失** | ❌ 无 |
| [#86214](https://github.com/openclaw/openclaw/issues/86214) | Codex 客户端在大型 `logs_2.sqlite` 下处理图片/工具请求时中途关闭 | **消息丢失**、会话中断 | ❌ 无 |
| [#119087](https://github.com/openclaw/openclaw/issues/119087) | Gateway 冷启动时间从 beta.1 到 beta.7 回退约 2.5 倍 | **性能回退** | ❌ 无 |
| [#123073](https://github.com/openclaw/openclaw/issues/123073) | dev 通道更新失败：npm 遇到 `workspace:*` 协议报错 | 开发者无法更新 | ✅ 有（[#124293](https://github.com/openclaw/openclaw/pull/124293)，Windows Cron 修复，待合并） |

### 关键观察
- **消息丢失（message-loss）** 是所有 P1 问题中出现频率最高的关键词，影响范围覆盖 Telegram、Discord、Feishu、Codex 等多个入口，**跨通道的消息可靠性是当前最大的稳定性短板**。
- 很多 P1 Bug（如 #38327）长期无法关闭，且被标记为 `needs-live-repro`，说明**维护者难以稳定复现，社区与官方之间存在信息断层**。

---

## 6. 功能请求与路线图信号

### 高潜力功能（有对应 PR 或明确实现路径）

| Issue | 标题 | 信号 |
|---|---|---|
| [#10687](https://github.com/openclaw/openclaw/issues/10687) | 全动态模型发现（OpenRouter 等） | 已有 [#124288](https://github.com/openclaw/openclaw/pull/124288) 修复相关性能问题，实现或许不远。 |
| [#116489](https://github.com/openclaw/openclaw/issues/116489) | 安装策略警告确认机制 | 已合并。属于**供应链安全**方向，未来可能扩展更多安全策略。 |
| [#66252](https://github.com/openclaw/openclaw/issues/66252) | 按 Agent 设置 TTS/STT 覆盖 | 社区呼声较高，但暂无直接 PR，可能进入下一版本规划。 |

### 关注度较高但无明确进展

| Issue | 标题 | 信号 |
|---|---|---|
| [#13219](https://github.com/openclaw/openclaw/issues/13219) | 按模型的使用量日志，用于成本核算 | 对于商业用户是刚需，当前只能解析 JSONL，体验差。 |
| [#39343](https://github.com/openclaw/openclaw/issues/39343) | Gateway 层图片批量/媒体组缓冲 | 涉及 LINE/Telegram 相册场景，属于体验优化，优先级可能不高。 |
| [#79902](https://github.com/openclaw/openclaw/issues/79902) | SQLite 转录/会话接口 | 生态开发者呼声高，属于平台化方向，**建议作为中期路线图重点**。 |

---

## 7. 用户反馈摘要

- **痛点：路径硬编码问题引发信任危机**
  - 在 [ #51429 ](https://github.com/openclaw/openclaw/issues/51429) 中，用户发现代码中硬编码了 `/Users/wangtao` 路径并随版本发布，导致新安装用户的工作区被强制指向此目录。该 Issue 已存在近 5 个月仍无修复，**严重损害了用户对项目代码审查质量的信心**。
- **中文用户社区活跃，但存在沟通壁垒**
  - 多个中文 Issue（如 [ #50490 ](https://github.com/openclaw/openclaw/issues/50490) Feishu 激活模式无效）反馈清晰且附有复现步骤，但大多停滞在 `needs-maintainer-review`，**建议官方增加中文维护者或明确多语言支持策略**。
- **对“生产就绪”标签的渴望**
  - [ #73537 ](https://github.com/openclaw/openclaw/issues/73537) 中，用户以家庭/商业助手身份表达了对项目的高度认可，但强烈希望官方能提供**生产就绪稳定性标签**，以便在关键场景中放心使用。这反映了**用户从“尝鲜”到“依赖”的心态转变**。
- **对崩溃与数据丢失的强烈不满**
  - [ #123799 ](https://github.com/openclaw/openclaw/issues/123799) 中，受 Codex compact 404 影响的生产用户表示，仅得到一个“已修复”的关闭通知，**缺乏具体的升级/规避指南**，导致其运维团队处于焦虑状态。

---

## 8. 待处理积压

以下问题因长期未解决、影响面广或标记为 stale，需要维护者重点关注：

### 高优先级积压

| 编号 | 标题 | 已开放时间 | 优先级 | 风险 |
|---|---|---|---|---|
| [#70903](https://github.com/openclaw/openclaw/issues/70903) | Provider 冷却时间过长 | 2026-04-24 | P0 | 用户直接流失 |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | Gemini 3.1 模型不可用 | 2026-03-06 | P1 | 核心功能不可用 |
| [#51429](https://github.com/openclaw/openclaw/issues/51429) | 工作路径硬编码 | 2026-03-21 | P2 | 信任危机 |
| [#77930](https://github.com/openclaw/openclaw/issues/77930) | Discord 通道加载回归 | 2026-05-05 | P2 | 大用户群受影响 |
| [#92241](https://github.com/openclaw/openclaw/issues/92241) | Gateway 更新后静默丢弃消息 | 2026-06-11 | P1 | 严重消息丢失 |

### 长期搁置的重要 PR

| 编号 | 标题 | 创建时间 | 状态 |
|---|---|---|---|
| [#112811](https://github.com/openclaw/openclaw/pull/112811) | 支持多个 MSTeams 机器人账号 | 2026-07-23 | 待维护者审查 |
| [#115670](https://github.com/openclaw/openclaw/pull/115670) | 支持在 `claws add` 中采用现有工作区 | 2026-07-29 | 需补充证明 |
| [#46303](https://github.com/openclaw/openclaw/pull/46303) | SIGUSR1 重载前清空入站防抖缓冲区

---

## 横向生态对比

# 个人 AI 助手与自主智能体开源生态横向对比分析（2026-08-16）

> **数据口径说明**：OpenClaw 数据快照为 8/14–15 完整窗口；OpenHands SDK、LiteLLM、Temporal 为 8/16 当日 24 小时数据。Hermes Agent 与 Pi 在本次摘要中未提供数据，暂不参与对比。

---

## 1. 生态全景

当前生态呈现“**头部平台高速迭代、基础设施层稳步加固**”的双轨态势。OpenClaw 以全栈功能与最大社区关注度维持核心参照地位，但消息丢失、回归问题与技术债务正在显著消耗信任；LiteLLM 作为 LLM 网关保持极高 PR 吞吐，安全治理与成本审计成为最突出议题；OpenHands SDK 与 Temporal 分别聚焦组件化 SDL 稳定性与工程基础设施重构。跨项目共同关键词已从“模型能力”转向“**安全、可靠性与可编程性**”，表明个人 AI 智能体正从“能用”向“敢用、好用”过渡。

---

## 2. 各项目活跃度对比

| 项目 | Issues 活跃 | PR 活跃 | Release | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 500 条更新* | 500 条更新*，46 合并/关闭 | v2026.8.1-beta.2 | 🔴 高活跃但技术债务重：P0/P1 问题密集，维护者带宽不足，合并率仅 9.2% |
| **OpenHands SDK** | 6 条更新 |

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报（2026-08-16）

---

## 1. 今日速览

过去24小时内，OpenHands SDK 项目保持了较高的迭代频率：共产生 6 条 Issue 更新和 17 条 PR 更新，其中 5 个 PR 已合并/关闭，显示出核心维护团队（@neubig 等）正在持续清理积压的 PR 队列。值得关注的是，安全和稳定性相关的修复占据了今日合并 PR 的多数份额（LLM 配置预检、技能迁移修复、MCP 依赖固定等），并出现了 1 个高优先级安全 Bug（#4505，密钥脱敏大小写绕过）尚未关联可见修复 PR。此外，数个由外部贡献者提交的功能 PR 仍处于待合并状态（如后台任务生命周期、仓库访问预检等）。整体而言，项目活跃度高，维护节奏稳定，但新版本发布暂缺。

---

## 2. 版本发布

**今日无新版本发布。**

> 提示：上一版本至今已有较长时间，且多个修复功能（如 #4422 LLM 预检端点、#4320 技能迁移修复）已确认合并，建议维护者考虑近期进行一次版本发布，以便用户通过正常升级路径获得这些修复。

---

## 3. 项目进展

今日共有 5 个 PR 被合并/关闭，均为功能落地或修复定型，具体如下：

- **[PR #4422] feat: add pre-flight LLM validation endpoint（已合并）**
  新增 `POST /api/profiles/{name}/validate` 端点，在保存 LLM Profile 前发送最小请求（1-token 调用）以校验配置是否正确。这是对 Issue #4429 的落地，为用户提供了配置错误的早期预警，避免运行时才发现模型/凭证配置不可用。
  https://github.com/OpenHands/software-agent-sdk/pull/4422

- **[PR #4320] fix(profiles): repair v1 skills migration（已合并）**
  修复了 agent server 升级后遗留的 `default` 通用 Profile 无法编辑的问题。移除了已退役的嵌入 `skills` 字段，并删除了冗余的 v3 迁移步骤。对应 Issue #4431 已关闭。该修复保障了用户升级路径的平滑性。
  https://github.com/OpenHands/software-agent-sdk/pull/4320

- **[PR #4458] feat: carry ConversationErrorEvent on ConversationRunError（已合并）**
  让 `ConversationRunError` 携带 SDK 已有的类型化 `ConversationErrorEvent`，使工作流自动化完成回调能够直接序列化错误详情。这是 OpenHands/automation 配套改进的 SDK 侧实现，提升了自动化场景下错误诊断的精确度。
  https://github.com/OpenHands/software-agent-sdk/pull/4458

- **[PR #4303] fix(mcp): pin fetch server runtime dependencies（已合并）**
  固定了 MCP fetch server 的运行时依赖，解决了 `mcp` 2.0.0 中 `McpError` → `MCPError` 重命名导致的兼容性问题。CI 已恢复绿灯，MCP 相关测试通过。
  https://github.com/OpenHands/software-agent-sdk/pull/4303

- **[PR #4325] ci: remove release security scan（已关闭，未合并）**
  CI 变更：移除了发布流程中的安全扫描步骤。从上下文看，该变更未被接受而关闭。
  https://github.com/OpenHands/software-agent-sdk/pull/4325

**整体评估**：上述 5 个合并 PR 表明项目重心集中在 LLM 配置稳定性、升级数据迁移可靠性、自动化集成错误传递以及依赖兼容性维护上。这些改动虽非用户可见的新功能，但对项目健康度的提升有务实贡献。

---

## 4. 社区热点

- **[Issue #976] [Tracker] Daily Examples Run Results — 63 条评论**
  这是每日自动运行示例脚本结果发布的标准占位 Issue，评论数量高但为自动化累积，不代表社区讨论热度。该 Issue 已持续近一年，可视为项目自动化健康监控的一个窗口。
  https://github.com/OpenHands/software-agent-sdk/issues/976

- **[Issue #4505] [Bug] `redact_text_secrets` misses lowercase and mixed-case secret keys（高优先级，安全）**
  由 @yifanxiong272 报告，SDK 的密钥脱敏工具 `redact_text_secrets` 无法处理小写/混合大小写的密钥名称。该问题涉及安全敏感场景（日志脱敏绕过），目前有 1 条评论，且标记了 `priority:high` 和 `security` 标签，被社区关注的显著性强。截至目前尚无直接的修复 PR 关联，但这是一个明确的行动信号。
  https://github.com/OpenHands/software-agent-sdk/issues/4505

- **[Issue #3759] `is_git_url()` 无法识别 ssh:// scheme — 已关闭**
  该问题自 2026-06-16 报告，历时两个月后于昨日关闭（未直接显示合并 PR，可能通过相关修复解决）。问题本身影响了使用 `ssh://` URL 的插件源配置，是涉及客户支持的痛点。
  https://github.com/OpenHands/software-agent-sdk/issues/3759

**分析**：社区活跃点聚焦于安全敏感型 Bug（secret 脱敏）和长期繁琐但重要的工具链问题（ssh URL 支持）。#4505 的出现值得注意——它在首次报告后一天内即被标记为高优先级并待开发（`ready-for-dev`），说明维护者对安全问题响应迅速，但也暴露出 SDK 在输入处理边界上的防御深度仍需加强。

---

## 5. Bug 与稳定性

按严重程度从高到低排列：

| 严重程度 | Issue/PR | 描述 | 状态 |
|---------|----------|------|------|
| 🔴 高（安全） | [#4505](https://github.com/OpenHands/software-agent-sdk/issues/4505) | `redact_text_secrets` 无法匹配小写/混合大小写的密钥名，导致日志或输出中的敏感信息可能未被脱敏。标记 `priority:high`、`security`、`ready-for-dev` | 状态：OPEN 无可见关联修复 PR |
| 🟡 中 | [#4500](https://github.com/OpenHands/software-agent-sdk/issues/4500) | `Condensation` 事件写入会话历史后，增量视图缓存会跳过 `enforce_properties` 检查，导致出现孤立的 action/obs 半对（有 action 无 obs，反之亦然） | 状态：OPEN **已有修复 PR #4501（待合并）** |
| 🟡 中 | [#4487 → PR #4488](https://github.com/OpenHands/software-agent-sdk/pull/4488) | Agent server 在 `ActionEvent` 持久化后、`base_` 持久化前崩溃，导致重启后状态损坏。已在真实 Agent Canvas 会话中发现 3 例 | 修复 PR #4488 待合并 |
| 🟡 中 | [#3759](https://github.com/OpenHands/software-agent-sdk/issues/3759) | `is_git_url()` 不识别 `ssh://` scheme，导致插件源解析失败并报误导性错误 | 状态：CLOSED（已解决） |
| 🟢 低 | [#4095 → PR #4095](https://github.com/OpenHands/software-agent-sdk/pull/4095) | LiteLLM 空流式响应被重组为 `None` 后触发裸 `AssertionError`，绕过重试策略。修复方向为非流式路径同样视为可重试错误 | 修复 PR 待合并（7月12日创建，已超一个月） |
| 🟢 低 | [#4437 → PR #4437](https://github.com/OpenHands/software-agent-sdk/pull/4437) | ACP Claude Code 模型选择器中缺少 `claude-fable-5` 选项 | 修复 PR 待合并 |

**小结**：有两类 Bug 与记忆/状态管理有关（Condensation 孤儿对、崩溃恢复），这暗示项目在长对话/持久化场景下的健壮性正在经历集中修复，值得在下一版本中重点验证。

---

## 6. 功能请求与路线图信号

结合今日合并/关闭的 PR 及新增 Issue，可以观察到以下路线图信号：

| 方向 | 相关 Issue/PR | 说明 | 可能性判断 |
|------|--------------|------|-----------|
| **LLM 配置可观测性与预检** | #4429（已关闭）/ [#4422](https://github.com/OpenHands/software-agent-sdk/pull/4422)（已合并） | 预检验证端点已落地，属于 LLM Profile 管理体验的明显提升 | ✅ 已进入主线 |
| **后台任务生命周期管理** | [#4503](https://github.com/OpenHands/software-agent-sdk/pull/4503)（待合并） | 引入进程内后台委托，包含稳定任务 ID、显式状态机、并行执行和协作取消 | 🔶 外部贡献，功能完整，等待社区审查/合并 |
| **安全的仓库访问预检** | [#4504](https://github.com/OpenHands/software-agent-sdk/pull/4504)（待合并） | 在既有 git 路由中新增认证的仓库验证端点，支持可选 ref 验证，并将 provider 凭证严格保留在服务端 | 🔶 外部贡献，有较好的信任边界分析背景 |
| **LLM Provider 连接层** | [#4492](https://github.com/OpenHands/software-agent-sdk/pull/4492)（待合并） | 在保留现有 LLM Profile 可运行配置的基础上，增加向后兼容的 provider-connection 引用层。这是 OpenHands/OpenHands#15492 的轻量后端替代方案 | 🔶 外部贡献，涉及架构层面，可能需较长时间评估 |
| **Client 扩展命名空间** | [#4496](https://github.com/OpenHands/software-agent-sdk/pull/4496)（待合并） | 将 client extensions 映射到 `dev.openhands` 命名空间下，并清理重复代码 | 🔶 外部贡献，命名空间设计会影响平台规范，需谨慎评估 |
| **工作区默认 LLM 与 Profile 对齐** | [#4497](https://github.com/OpenHands/software-agent-sdk/pull/4497)（待合并） | 修复未固定 profile 的自动化任务使用过期 keyless LLM 的问题，使默认模型与 UI 展示一致 | ✅ 修复明确，预计近期合并 |

**提示**：上述待合并 PR 中，[#4095](https://github.com/OpenHands/software-agent-sdk/pull/4095)（空流重试）等待时间已超过一个月，建议维护者优先处理，以免增加后续合并冲突风险。

---

## 7. 用户反馈摘要

基于今日活跃 Issues 和 PR 评论中的一手用户声音：

- **ssh:// 支持缺失引发困扰**（来自 #3759）：用户 @jpshackelford 报告，当插件源使用 `ssh://git@bitbucket.example.com:7999/team/repo.git` 格式时，SDK 在解析阶段便报出误导性错误 "Unable to parse"。该问题持续 2 个月才关闭，期间用户依靠 workaround 绕过，反映了对私有仓库/自建 Git 服务场景支持不够充分。

- **Secret 脱敏存在安全盲区**（来自 #4505）：用户 @yifanxiong272 在标题中直接点出脱敏工具对大小写变体的缺陷，这意味着在实际使用中，以 `api_key`、`ApiKey`、`API_KEY` 等不同大小写形式出现的密钥可能泄露到日志或输出中。虽然该 Issue 发布时间较短，但已经获得维护者的标签确认，预计会快速进入修复流程。

- **后台任务与工作流自动化需求增强**（来自 #4458 周边）：合并的通信改进（ConversationErrorEvent 传递）说明用户（尤其自动化工作流使用者）在排查失败任务时需要精确的结构化错误上下文，而不是笼统的异常字符串。这从侧面反映社区用户正将 SDK 深度集成到自动化流水线中。

- **Windows 浏览器兼容性问题持续关注**（来自 #4502）：外部贡献者 @KirschBluteX 提交了在 Windows 上优先使用 Playwright Chromium 的修复，说明 Windows 环境下浏览器发现失败问题虽非高发（无独立 Issue），但已影响实际用户，且被外部开发者视为重要到值得自行修复。

---

## 8. 待处理积压

- **[PR #4095] fix(sdk): retry empty streaming responses**（待合并已超 1 个月）
  空流式响应重试修复，涉及 SDK 的核心 LLM 调用路径。长时间未合并可能导致与其他代码冲突，建议维护者在本周内安排 review。 
  https://github.com/OpenHands/software-agent-sdk/pull/4095

- **[PR #4437] fix(acp): add claude-fable-5 to Claude Code model picker options**（待合并 7 天）
  为 ACP Claude Code 会话补充新模型选项。属于微小改动但长期搁置，可能阻塞用户使用新模型。
  https://github.com/OpenHands/software-agent-sdk/pull/4437

- **[PR #4456] fix(agent-server): page bash events after filtering**（待合并 6 天）
  修复 #4388 中 bash 事件过滤后分页结果的缺口。该修复已 rebase 到最新 main，说明贡献者花了较大精力适配新代码，建议尽快合并。
  https://github.com/OpenHands/software-agent-sdk/pull/4456

- **[Issue #976] Daily Examples Run Results 占位 Issue**（持续 300

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

## LiteLLM 项目日报 — 2026-08-16

### 今日速览

过去 24 小时项目保持非常高的活跃度：共 52 条 Issues 更新、208 条 PR 更新，其中 95 条 PR 被合并或关闭。新版本发布为 0，但多个修复集中指向代理稳定性（Prisma 启动竞态、批次成本核算、入站请求透传）。值得关注的是社区连续提交了 3 份安全审查报告（#37052 / #37053 / #37054）与 1 个长期悬而未决的预算绕过问题（#28033），安全治理成为当前最突出的信号。

---

### 版本发布

今日无新版本发布。当前最新版本为 v1.96.2（来自 #36922 的版本信息），但该版本被报告存在 FastAPI 依赖兼容性问题，详见下文 Bug 部分。

---

### 项目进展

今日合并/关闭的 PR 主要集中在批量任务管理、Guardrails 细节修复、MCP 权限收敛与开发者工具链四个方向：

- **Guardrails 补全** — #37036 修复了 PANW AIRS 被拦截请求仅返回部分扫描字段的问题，现在完整透传 `prompt_detection_details`、`prompt_masked_data` 等审计信息。
- **影子评测 UI 升级** — #36994 为 shadow evals 仪表盘加入了方向选择器和反向模式显示，使反向评测结果不再以正向标签渲染。
- **MCP 安全收敛** — #35045 将 RFC 8707 的 `resource` 参数真正用于 MCP 会话令牌，使 bearer 令牌不再携带用户超出单个 server 的完整 MCP 权限。
- **Bedrock 批量输出修复** — #36634 与 #37047 共同解决了批量任务完成后输出无法下载、成本无法记录的问题，统一了所有读取路径上的凭据快照构建。
- **开发者工具链优化** — #36988 引入了机器级 slot lock，避免并行 `make check` 互相拖垮机器；#28203 修复了 MCP 检查器粘贴参数的多余空白问题。

---

### 社区热点

1. **#10177 Dark Mode（👍 71，💬 63）** — 自 2025 年 4 月开启后依然是社区最活跃的帖子，评论数在过去一天继续增加。诉求很直白：管理面板缺少暗色主题，用户“快瞎了”。这反映出 UI 体验细节对日常运维人员的重要程度。
2. **#25429 GPT-5.4 空响应（💬 18）** — 使用 `litellm.responses()` 时 GPT-5.4 返回空 final output，`completion()` 桥接则报 “Unknown items in responses API response”。该问题持续四个月，与 responses API 桥接层的稳定性直接相关。
3. **安全审查三连（#37052 / #37053 / #37054）** — 同一位安全人员提交了三个基于只读代码审查的发现（预算自提升、SSRF/密钥外泄、无认证默认配置），虽然都标记为 Low/Medium 且已由维护者关闭，但集中出现说明外部安全社区正在对 LiteLLM 做系统性的攻击面审视。

---

### Bug 与稳定性

按严重程度排序：

| 严重度 | Issue | 问题摘要 | 状态 |
|---|---|---|---|
| 🔴 高 | #37054 | 未设置 `LITELLM_MASTER_KEY` 时代理完全无认证运行，且自带 docker-compose 默认未设置 | 已关闭 |
| 🔴 高 | #35766 | `LiteLLM_SpendLogs` 缺少 `(api_key, startTime)` 索引，预算窗口重算全表扫描导致 RDS P2028 事务超时 | 开放中 |
| 🔴 高 | #27704 | 滚动部署时 Prisma Query Engine 未就绪即启动后台任务，造成 spend 数据丢失 | 开放中 |
| 🟠 中 | #37053 | 客户端可控 `api_base` 在特定认证模式下可导致 SSRF / 供应商密钥外泄，现有校验为死代码 | 已关闭 |
| 🟠 中 | #37052 | 非管理员 key 持有者可通过 `/key/update` 的 `temp_budget_increase` 自行提升 `max_budget` | 已关闭 |
| 🟠 中 | #36922 | `uv tool update` 到 v1.96.2 后 FastAPI `get_flat_dependant` 签名不兼容，代理无法启动 | 开放中 |
| 🟠 中 | #28033 | 存在演示仓库的预算绕过漏洞，与 #37052 相关但口径更广 | 开放中（stale） |
| 🟡 低 | #33986 | 托管 Bedrock 批次无法通过 `/v1/batches/{id}/cancel` 取消，上游明确不支持 | 开放中 |

另有多个翻译层回归：OpenAI→Anthropic 工具参数丢失（#27469，已关闭）、聊天→Responses 流式 usage 丢失（#27459，已关闭）、Gemini system 消息序列化键名错误（#37028）、Ollama api_base 被忽略导致每次请求增加约 8 秒超时（#37041）等。其中 #37041 有明确的最小复现路径，值得优先跟进。

---

### 功能请求与路线图信号

- **新模型/供应商支持**（较大概率进入下一版本）：
  - #35091：新增 `voyage-4` 系列与 `voyage-context-4`，同时修复 contextual 输入对 `list[str]` 的处理
  - #36820：新增尚未正式发布的 `voyage-code-4` 嵌入模型
  - #32516：新增完整的 TokenLab 供应商支持（含测试，已通过本地检查）
- **功能增强**：
  - #28026：为 `litellm.image_generation` 增加 Ollama 文生图支持（当前调用返回空 `data`）
  - #27830：对自托管 vLLM/OpenAI 兼容后端自动填充 `max_input_tokens` / `max_output_tokens`
  - #28032：允许模型访问组嵌套组合，子组更新自动联动父组
- **基础设施修复**（虽然以 Bug 形式出现，但实际是架构缺口）：
  - #37058：透传时不再把客户端的 `Accept-Encoding` 原样转发给上游，解决 Anthropic 启用 brotli 后代理因缺少解码库而转发乱码的问题（已提交 fix）
  - #36741：将 Langfuse 回调从已退役的 SDK v2 迁移至 v4（已提交 fix）

---

### 用户反馈摘要

- **“升级后一切坏了”的回归焦虑**：#36922 用户执行 `uv tool update` 后代理直接无法启动；#22997 用户报告升级到 1.81.14 后 thinking 和 tools 同时失效，回退到 1.81.12 才恢复。这种“小版本升级即风险”的体验是用户对 LiteLLM 稳定性最直接的抱怨。
- **对 responses API 桥接的困惑**：#25429 中用户用最标准的 `litellm.responses()` 调用 GPT-5.4 得到空结果，且 `completion()` 桥接抛出的错误信息完全不可读；#36928 则报告 `interactions.create()` 静默丢弃 `response_format`。多个入口行为不一致正在消耗用户信任。
- **管理员对审计能力的迫切需求**：#36997 指出 Admin UI 的登录 cookie 是非 HttpOnly 的 JWT 且直接携带用户真实代理密钥，属于严重的设计缺陷；#36880 则反映 guardrail 拦截的 `/v1/responses` 请求上报为零 token 消耗，导致实际成本与审计记录脱节。
- **积极的信号**：部分用户（如 #28026、#35091、#32516 的提交者）愿意主动补齐模型信息和集成代码，说明第三方生态贡献意愿强，项目拥有良好的外部发展动力。

---

### 待处理积压

- **#10177 Dark Mode** — 2025-04-20 创建，👍 71，长期高活跃未关闭。作为管理面板的基础可用性提升，建议正式排期。
- **#33986 Bedrock 批次取消不支持** — 2026-07-20 创建，6 条评论，仍在寻求规避方案。若无法快速支持，建议在文档中明确标注“Beta 功能不支持 cancel”。
- **#27704 Prisma 启动竞态导致数据丢失** — 2026-05-12 创建，涉及滚动部署下的核心计费数据正确性，虽已有 3 条讨论但未有 fix PR，建议提升优先级。
- **#28033 预算绕过** — 2026-05-16 创建，已带公开 PoC 仓库，虽标 stale 但属于安全风险，建议维护者公开评估结论。
- **#35766 数据库索引问题** — 2026-08-04 创建，已被标记为 P2028 生产事故，3 条评论后暂无修复动作，建议尽快补充索引或提供迁移脚本。

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

## 1. 今日速览

过去24小时 Temporal 仓库无新 Issue（新开/活跃/关闭均为 0）、无新版本发布，外部用户侧动态平静。PR 侧活跃度较高：共 35 条更新，其中 17 条已合并/关闭、18 条待合并。核心动态集中在三方面：一是 @stephanos 的 canonical Go test reporting pipeline 系列 PR 集中合入，测试基础设施重构明显提速；二是 reliability-2026 计划的 flaky 报告改进与任务处理器可靠性修复持续推进；三是 1.32.0 release 分支已创建，版本发布流程正式启动。综合来看，项目处于"外部反馈平静、内部工程迭代密集"的状态，整体健康度良好。

## 2. 版本发布

本日报周期内无新版本发布（最新 Releases 为空）。值得注意的是 **[#11591](https://github.com/temporalio/temporal/pull/11591) "1.32.0: Prepare release branch"** 已合并，创建了 1.32.0 发布分支并更新依赖与治理文件，说明 1.32.0 已进入发布准备阶段，可预期后续将有 RC 版本推出。

## 3. 项目进展

今日合并/关闭 17 条 PR，重要进展如下：

**测试报告流水线重构（重大工程推进）**

@stephanos 的系列 PR 今日集中合入，标志 Temporal 测试基础设施向 `go test -json` 标准化迁移迈出关键一步：

- **[#11513](https://github.com/temporalio/temporal/pull/11513)**：加固共享 JUnit 报告 IO，读取拒绝尾部 XML、写入改为原子替换，防止中断写入损坏既有报告。
- **[#11512](https://github.com/temporalio/temporal/pull/11512)**：将 testrunner 报告输入输出统一到共享 JUnit 文档类型，为后续解析替换建立边界。
- **[#11487](https://github.com/temporalio/temporal/pull/11487)**：将诊断解析与超时解析拆分为独立文件，行为不变，为后续语义化重构铺路。
- **[#11514](https://github.com/temporalio/temporal/pull/11514)**：定义 package-aware canonical attempt 结果模型，固定失败叶节点、不完整执行、重试安全等查询语义。
- **[#11488](https://github.com/temporalio/temporal/pull/11488)**：将测试输出分析切换到 canonical 诊断体系，通过临时兼容适配器隔离生产环境切换风险。
- **[#11515](https://github.com/temporalio/temporal/pull/11515)**：记录器落地，直接运行 `go test -json` 并记录 canonical 尝试结果，涵盖事件归属、构建失败、超时、进程状态等。

**可靠性修复**

- **[#11570](https://github.com/temporalio/temporal/pull/11570)**：修复 priTaskReader 的读/确认级别移动回退问题，包括丢弃低于当前 ack level 的任务、防止基于过期读级别执行 gap 设置、禁止 ack level 回退。这是继 #11048 后对任务处理器的又一重要加固。

**可见性归档能力补全**

- **[#11298](https://github.com/temporalio/temporal/pull/11298)**：s3store 和 gcloud visibility archivers 现在接受归档查询中的 `ExecutionStatus` 过滤器，与 filestore 行为对齐，同时将 `convertStatusStr` 抽取为统一的 `ConvertStatusStr`，消除了三个存储后端间的行为差异。

**发布准备**

- **[#11591](https://github.com/temporalio/temporal/pull/11591)**：创建

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*