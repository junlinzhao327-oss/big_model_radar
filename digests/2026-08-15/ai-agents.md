# OpenClaw 生态日报 2026-08-15

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-14 22:44 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 开源项目动态日报 — 2026-08-15

## 今日速览

过去 24 小时项目活跃度极高：共 500 条 Issue 更新（490 条新开/活跃、10 条关闭）和 500 条 PR 更新（404 条待合并、96 条已合并/关闭），但无新版本发布。社区讨论聚焦于长期未愈的稳定性和消息丢失问题（尤其是 #121058 静默回复失败复发，单日 94 条评论），同时 Web UI 侧边栏改进系列 PR（#123613、#123597、#123582 等）密集提交，显示界面重构正成为当前开发重点。值得警惕的是 P0 级内存泄漏（#91588）和文件工具路径破坏（#119270）仍在活跃，项目整体处于"高迭代、稳修复滞后"的状态。

---

## 项目进展

> 今日无新版本发布。以下为过去 24 小时内活跃度较高、可能被合并的 PR 方向：

### Web UI 侧边栏重构（多个 PR 并行）
社区与维护者正集中推进 Control UI 侧边栏的视觉统一与交互优化，涉及图标、排版、布局网格、账户区域和告警面板等多个维度，暗示 Web UI 将迎来一次较大规模的体验更新：
- **Unify sidebar iconography** — 统一侧边栏图标尺寸与描边权重（#123613）
- **Unify sidebar account footer and identity menu** — 整合账户页脚与身份菜单（#123582）
- **Consolidate sidebar issues into a quiet panel** — 将堆叠告警收敛为铃铛+计数面板（#123682）
- **Normalize sidebar typography** — 统一侧边栏字体规范（#123626）
- **Refactor sidebar chrome grid** — 建立统一的侧边栏结构网格（#123681）

### 渠道能力增强
- **feat(slack): include observed away duration in presence events** — 为 Slack 在线状态事件增加离席时长元数据，便于团队了解成员实际可用性（#123805）
- **feat(telegram): support copy-text presentation buttons** — 为 Telegram 富文本消息增加一键复制按钮，解决命令、Token 等精确文本复制痛点（#123837）

### 稳定性修复
- **fix(memory-core): stop hammering a billing-exhausted embeddings provider every turn** — 修复月度额度耗尽的 embedding 提供商每轮对话被重复请求的问题（#123855）
- **fix(gateway): keep node worker outcomes consistent under load** — 修复并发运行工作节点在容量饱和时错误失败、队列聊天误报终止的问题（#123869）

---

## 社区热点

### 1. Silent reply failures still recurring（#121058）— 94 条评论
**链接**: https://github.com/openclaw/openclaw/issues/121058

之前已关闭的 #116277 问题（静默回复失败）再次复发。监控 cron 持续记录到新失败事件，包括 2026-08-09 当天仍有发生。用户表达了明显的沮丧情绪。该问题同时获得 94 条评论，表明受影响用户群体较大，且修复效果不达预期。

### 2. Gateway Memory Leak — RSS 15.5GB 致 OOM 崩溃（#91588）— 24 条评论
**链接**: https://github.com/openclaw/openclaw/issues/91588

**P0** 级内存泄漏问题，讨论热度持续攀升。网关进程 RSS 从启动时 350MB 在 2-3 天内涨至 15.5GB，触发 OOM killer，导致反复重启。该问题自 6 月 9 日提出已超过两个月，仍未解决，社区对 Gateway 长时间运行的稳定性信心正在下降。

### 3. Cron agent turn stall on DeepSeek（#121953）— 20 条评论
**链接**: https://github.com/openclaw/openclaw/issues/121953

**P1** 问题：OpenClaw 为 cron 消息添加的 `[cron:<jobId> <jobName>] ` 前缀导致 DeepSeek API 边缘节点将请求降级处理，agent 停顿数十秒至分钟。开发者社区对特定模型提供商的边缘行为差异表现出高度关注。

### 分析
今日热点集中在**消息可靠性**（静默失败、cron 停顿、内存增长导致的静默降级）与**模型提供商兼容性**两大主题。社区诉求从"功能迭代"转向"稳定性修复"，对关键路径上的消息丢失问题容忍度明显降低。

---

## Bug 与稳定性

### P0（严重，需立即关注）

| Issue | 标题 | 状态 |
|---|---|---|
| [#91588](https://github.com/openclaw/openclaw/issues/91588) | Gateway 内存泄漏，RSS 350MB → 15.5GB，OOM 崩溃循环 | ⚠️ 无 fix PR |
| [#119270](https://github.com/openclaw/openclaw/issues/119270) | 文件工具剥离目标路径开头的 `@` 符号，导致写入/删除错误文件 | ⚠️ 无 fix PR |
| [#108435](https://github.com/openclaw/openclaw/issues/108435) | 升级 2026.7.1 后 gateway 无法启动（systemd / ollama / 手动均失败） | ⚠️ 无 fix PR |

### P1（高优先级）

| Issue | 标题 | 状态 |
|---|---|---|
| [#121058](https://github.com/openclaw/openclaw/issues/121058) | 静默回复失败复发（关闭 #116277 后仍在发生），无排队回复负载 | ⚠️ 无 fix PR，社区强烈关注 |
| [#121953](https://github.com/openclaw/openclaw/issues/121953) | cron agent 在 DeepSeek 上停顿——`[cron:]` 前缀被 API 降级 | ⚠️ 无 fix PR |
| [#96834](https://github.com/openclaw/openclaw/issues/96834) | WhatsApp 1:1 图片消息致主通道卡顿 ~3 分钟（多模态运行卡死） | ⚠️ 无 fix PR |
| [#62505](https://github.com/openclaw/openclaw/issues/62505) | Coding Agent 回归：不再完成任务（2026.4.2 之前正常） | ⚠️ 无 fix PR |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | "Cannot convert undefined or null to object" — gemini-3.1-pro-preview 在 2026.3.2 后失败 | ⚠️ 无 fix PR |
| [#86215](https://github.com/openclaw/openclaw/issues/86215) | Codex OAuth 刷新失败可致 agent 卡死数小时，无告警与轮换 | ⚠️ 无 fix PR |
| [#83959](https://github.com/openclaw/openclaw/issues/83959) | Codex app-server 启动重试在备用服务器就绪前耗尽 | ⚠️ 无 fix PR |
| [#87109](https://github.com/openclaw/openclaw/issues/87109) | Gateway heap 空闲状态涨至 1073MB+，cron 在内存压力下静默失败 | ⚠️ 无 fix PR |

### 值得注意：已有修复 PR 的问题

| Issue | 关联 PR | 说明 |
|---|---|---|
| [#120563](https://github.com/openclaw/openclaw/issues/120563)（历史不发送/Ollama 固定上下文） | 无直接 PR，但 [#123855](https://github.com/openclaw/openclaw/pull/123855) 缓解了同类的 provider 请求风暴问题 | — |
| [#99910](https://github.com/openclaw/openclaw/issues/99910)（Memory dreaming 钉住事件循环 ~10 分钟） | [#123855](https://github.com/openclaw/openclaw/pull/123855) 对 embeddings provider 做了退避止损，但仅为部分缓解 | — |

### 新提交的修复型 PR（过去 24 小时）
- **fix(skills): repair valid skills above the reviewer read cap** — 修复 20,000 字符以上技能无法读取截断的问题（[#123866](https://github.com/openclaw/openclaw/pull/123866)）
- **fix(memory): report truthful index outcomes for empty workspaces** — 空工作区不再误报"Memory index updated"（[#123863](https://github.com/openclaw/openclaw/pull/123863)）
- **fix(gateway): resolve cron owner for explicit agent rosters** — 修复显式 agent 名册下 cron 所有权解析失败（[#123865](https://github.com/openclaw/openclaw/pull/123865)）
- **fix(sessions): prevent cleanup from deleting readable transcripts** — 防止会话清理误删可读的 SQLite 转写内容（[#123495](https://github.com/openclaw/openclaw/pull/123495)）
- **fix(claws): recover lifecycle state safely** — 修复 Claw 运行时所有权过期/并发 MCP 变更下的生命周期恢复（[#123254](https://github.com/openclaw/openclaw/pull/123254)）

---

## 功能请求与路线图信号

### 社区高频请求（可能进入下一版本的方向）

| Issue/PR | 内容 | 信号强度 |
|---|---|---|
| [#10687](https://github.com/openclaw/openclaw/issues/10687) | **动态模型发现**（OpenRouter 等快速更新的模型目录） | ⭐⭐⭐（3👍，maintainer 关注） |
| [#13219](https://github.com/openclaw/openclaw/issues/13219) | **按模型用量日志**：原生聚合 token 消费/成本追踪 | ⭐⭐⭐（1👍，已有 open PR） |
| [#71142](https://github.com/openclaw/openclaw/issues/71142) | **Control UI 可配置上传大小限制**（当前硬编码 5MB） | ⭐⭐ |
| [#88154](https://github.com/openclaw/openclaw/issues/88154) | **Slack Modal 支持**结构化交互工作流 | ⭐⭐ |
| [#17840](https://github.com/openclaw/openclaw/issues/17840) | **表情反应触发 agent 轮次**（opt-in 机制） | ⭐⭐ |
| [#75947](https://github.com/openclaw/openclaw/issues/75947) | **UI 质量重构**（基于 UX 评分） | ⭐⭐（2👍） |

### 结合 PR 动向的判断

Web UI 侧边栏系列 PR（#123582/#123597/#123613/#123626/#123681/#123682）密集提交且标注 `maintainer`，**Control UI 界面重构几乎确定会进入下一版本**。同时 [#123837](https://github.com/openclaw/openclaw/pull/123837)（Telegram 复制按钮）与 [#123805](https://github.com/openclaw/openclaw/pull/123805)（Slack presence 时长）均为小体量、低风险、高用户感知的改动，合入概率较高。

---

## 用户反馈摘要

### 满意点
- **产品价值认可**：[#73537](https://github.com/openclaw/openclaw/issues/73537) 用户明确表示 OpenClaw "已成为家庭和日常工作的核心助手"（Telegram 集成、自动化、cron、Home Assistant 控制），对 Peter 和团队表达感谢。

### 核心痛点
1. **修复不彻底**（#121058）：问题关闭后依然复发，"我们追踪此故障模式的 cron 在 issue 关闭后持续记录新发生事件" — 用户对修复质量与验证流程存在质疑。
2. **数据安全风险**（#119270）：文件工具剥离 `@` 前缀导致"write 覆盖了错误的文件，edit 重写了另一文件的内容" — 这是数据损坏级别的严重问题，社区对其缓慢修复表示担忧。
3. **更新/回滚风险**（#92241、#108435）：网关进程持有陈旧模块路径，回滚后静默丢弃入站消息；升级后 gateway 无法启动。频繁的"升级-热修复-再升级"节奏正在消耗用户信任。
4. **长时间运行的稳定性滑坡**（#91588、#87109）：内存泄漏与 heap 增长导致 cron 静默失败、OOM 循环重启，家庭/企业用户对 7×24 运行场景的信心下降。

### 社区情绪
整体态度从早期的"积极尝鲜"转向"谨慎评估"——用户愿意投入时间提供详细复现信息（如 #121083 文档 bug 的完整 trace），但对 P0/P1 级问题长期滞留（如 #91588 自 6 月 9 日至今 2 个月未修复）表现出明显的不耐烦。

---

## 待处理积压

### 长期未修复的高优 Issue（超过 30 天仍开放）

| Issue |

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报（2026-08-15）

## 1. 今日速览

过去 24 小时项目整体活跃度较高，Issue 与 PR 更新合计 48 条。值得关注的是，昨日新开了一系列由核心维护者提交的高优 Bug（#4487、#4494、#4498、#4491），且均已配套提交修复 PR，显示项目对问题响应迅速。与此同时，Agent Plugins 标准支持工作（#4405）持续推进，衍生出多个设计子任务（#4451、#4452、#4453）并迎来首个命名空间映射 PR（#4496），表明该方向已进入密集实现阶段。项目无新版本发布，整体处于功能开发与稳定性修复并行的健康状态。


## 2. 版本发布

过去 24 小时无新版本发布。


## 3. 项目进展

今日有 6 个 PR 被合并/关闭，主要集中在安全加固、LLM 能力增强与 CI 优化三个方向：

- **安全分析基础设施重构迈出重要一步**：[PR #3944](https://github.com/OpenHands/software-agent-sdk/pull/3944)（feat(security): AST-backed shell command-name resolution, #2721 Phase 2b）已关闭。该 PR 是 #2721 的第二阶段实现，用 AST 解析替代正则匹配来解析 shell 命令名，修复了引号、路径、嵌套三种绕过方式。这标志着基于 tree-sitter-bash 的安全检测重构（#2721）进入收尾阶段。
- **路由模型运行时元数据能力落地**：[PR #4423](https://github.com/OpenHands/software-agent-sdk/pull/4423)（feat(llm): resolve provider-specific runtime metadata for routed models）已合并。该 PR 解决了 OpenRouter 等路由供应商各端点运行时限制不一致的问题，`LLM.effective_max_input_tokens` 将不再仅依赖静态模型目录，为后续基于动态元数据优化上下文管理铺平道路。
- **Condenser token 上限修复**：[PR #4461](https://github.com/OpenHands/software-agent-sdk/pull/4461)（fix(sdk): cap condenser token limit by agent context）已关闭。当 `agent context` 小于 condenser 配置的 token 上限时按 agent 上下文封顶，避免超出模型实际窗口。
- **Windows 终端测试稳定性改进**：[PR #4290](https://github.com/OpenHands/software-agent-sdk/pull/4290)（test(terminal): stabilize Windows Ctrl-C cleanup assertion）已关闭，CI 记录显示 Windows 测试已通过。
- **CI 触发逻辑修复**：[PR #4486](https://github.com/OpenHands/software-agent-sdk/pull/4486)（ci: re-run PR description check when new commits are pushed）已合并，修复了 `pr-description-check.yml` 未监听 `synchronize` 事件导致新提交推送后检查不重新运行的问题。

综合来看，安全模块的 AST 化重构已获得首个完整实现，LLM 路由元数据能力也已完成，项目在安全性与模型兼容性两个维度均有实质推进。


## 4. 社区热点

今日讨论活跃度最高的 Issue 呈现如下关注点：

- **[#2721 Proposal: Replace regex-based shell command analysis with tree-sitter-bash](https://github.com/OpenHands/software-agent-sdk/issues/2721)**（15 条评论）
  这是今日最受关注的技术方案讨论。用户 @VascoSch92 指出当前 `defense_in_depth` 安全模块基于正则匹配扁平化命令文本，terminal 模块使用 `bashlex` 做命令切分，两者在复杂 shell 语法（嵌套、引号、路径变换）面前均有绕过风险，建议统一迁移至 tree-sitter-bash。该 Issue 已历经 4 个月讨论，PR #3944 的关闭标志着讨论已转化为实际代码，社区对该方向的关注度将持续走高。

- **[#4405 Spec: Support the Agent Plugins portable package format](https://github.com/OpenHands/software-agent-sdk/issues/4405)**（6 条评论，Needs Design）
  引入 agent-plugins.org 开放标准（v1.0.0 Working Draft，技术委员会含 Amazon、Cursor、Microsoft 等核心维护者）。该 Issue 已衍生出 4 个子任务（#4451、#4452、#4453、#4495），并迎来首个实现 PR #4496，是当前项目的长线热点。

- **[#976 Daily Examples Run Results](https://github.com/OpenHands/software-agent-sdk/issues/976)**（63 条评论）
  每日示例脚本自动运行结果的占位 tracker（由 bot 自动发布）。持续产生大量自动化评论，是社区观察项目实际运行状态的窗口之一。

**讨论诉求分析**：安全模块的正则替代方案反映了社区对 AI Agent 工具调用安全性的深层关切——随着 Agent 自主性增强，命令注入和路径穿越的防御必须从"字符串匹配"升级为"语法解析"。Agent Plugins 标准的引入则体现了社区对插件生态可移植性、供应商中立性的明确期待。


## 5. Bug 与稳定性

今日共报告 12 个 Bug（含 4 个新开），另有 2 个此前报告的 Bug 获得修复 PR。按严重程度排列如下：

### 高优先级（均有 fix PR）

- **[#4487 [Bug]: crash recovery orphans interrupted tool result and permanently breaks subsequent turns](https://github.com/OpenHands/software-agent-sdk/issues/4487)**（新开，priority:high）
  在 agent-server 重启时，若有正在执行的工具调用，崩溃恢复可能永久破坏该会话的事件分支。已提交两个修复 PR：
  - [PR #4488](https://github.com/OpenHands/software-agent-sdk/pull/4488)（fix(agent-server): keep crash recovery result on interrupted action branch，OPEN）
  - [PR #4489](https://github.com/OpenHands/software-agent-sdk/pull/4489)（fix(agent-server): parent crash recovery errors to interrupted actions，CLOSED）
  两个 PR 从不同角度修复同一问题：#4488 将恢复结果保留在中断的 action 分支上，而 #4489 则将错误归属到中断的 action 上。

- **[#4493 [Bug]: Internal MCP self-connection fails with "405 Method Not Allowed" on rootless Podman](https://github.com/OpenHands/software-agent-sdk/issues/4493)**（priority:high）
  在 rootless Podman 环境下，内部 MCP 自连接失败，导致所有对话阻塞。当前尚无修复 PR，已关联 OpenHands/OpenHands#13861。

- **[#4494 [Bug]: workspace default LLM ignores active profile and can launch stale keyless model](https://github.com/OpenHands/software-agent-sdk/issues/4494)**（新开，priority:high）
  agent-server 报告的活跃 LLM profile 与实际 `agent_settings.llm` 中的模型/配置可能不一致，导致无人值守的自动化任务使用陈旧的 keyless 模型启动。已有修复 PR：
  - [PR #4497](https://github.com/OpenHands/software-agent-sdk/pull/4497)（fix(sdk): resolve workspace default from active LLM profile，OPEN）

### 中优先级

- **[#4498 Incremental view path skips enforce_properties after condensation](https://github.com/OpenHands/software-agent-sdk/issues/4498)**（新开，priority:medium）
  `ConversationState.view` 增量路径在应用 `Condensation` 后未调用 `enforce_properties`，导致孤儿 `tool_result`/`tool_use` 被发送给 LLM。已有修复 PR：
  - [PR #4499](https://github.com/OpenHands/software-agent-sdk/pull/4499)（fix: enforce view properties after condensation in incremental path，OPEN）

- **[#4491 [Bug]: DeepSeek prompt cache hits are not recorded in LLM telemetry](https://github.com/OpenHands/software-agent-sdk/issues/4491)**（新开，priority:medium）
  DeepSeek 兼容接口返回的 `prompt_cache_hit_tokens`（顶层字段）未被正确计入遥测。已有修复 PR：
  - [PR #4490](https://github.com/OpenHands/software-agent-sdk/pull/4490)（fix(sdk): Track DeepSeek prompt cache hits in telemetry，OPEN）

- **[#3842 agent-server: conversation wedges at execution_status=idle while /run returns 409](https://github.com/OpenHands/software-agent-sdk/issues/3842)**（priority:unset）
  会话永久卡死：`execution_status` 报告 `idle`，但 `/run` 返回 `409 conversation_already_running`，唯一恢复手段是重启 agent-server。该问题从 6 月 22 日至今已近两个月，尚未标注优先级，也没有关联修复 PR，建议维护者关注。

### 已关闭的 Bug

- **[#4034 Windows: UnicodeDecodeError on conversation resume](https://github.com/OpenHands/software-agent-sdk/issues/4034)**（已关闭）
  Windows 上恢复会话时 `base_state.json` 用系统默认编码而非 UTF-8 读取，导致含非 ASCII 字符时崩溃。已关闭，修复已完成。
- **[#4072 Remove browser_use logging monkey-patch once fixed upstream](https://github.com/OpenHands/software-agent-sdk/issues/4072)**（已关闭）
  上游已修复，移除了临时补丁。


## 6. 功能请求与路线图信号

### 核心路线图推进：Agent Plugins 标准支持

[#4405](https://github.com/OpenHands/software-agent-sdk/issues/4405) 正在从设计走向实现，其子任务和首个实现 PR 已在今日落地：

- **[PR #4496 feat(plugin): map client extensions under the dev.openhands namespace](https://github.com/OpenHands/software-agent-sdk/pull/4496)**（OPEN，draft）
  将 Claude-Code 起源的 `commands/`、`agents/`、`hooks/hooks.json`、`entry_command` 概念映射到 `dev.openhands` 反向域名命名空间下，对应子任务 [#4452](https://github.com/OpenHands/software-agent-sdk/issues/4452)。
- **[#4495 Plugin skills discovery duplicates load_skills_from_dir](https://github.com/OpenHands/software-agent-sdk/issues/4495)**（新开）
  插件格式自带的技能目录扫描器与公共 `load_skills_from_dir` 结构重复，需要代码去重。属于 #4405 实现过程中发现的技术债。
- **[#4453 Agent Plugins: path-containment enforcement + narrow failure boundaries](https://github.com/OpenHands/software-agent-sdk/issues/4453)**（Needs Design）
  为 `PluginFormat` 增加路径包含强制校验：所有包内解析路径在解析符号链接后必须保持在插件根目录内。当前无边界强制，存在路径逃逸风险。
- **[#4451 Agent Plugins: mcp.json loader + PLUGIN_ROOT/PLUGIN_DATA expansion](https://github.com/OpenHands/software-agent-sdk/issues/4451)**（Needs Design）
  增加 `mcp.json` 加载器及变量展开语义，但受制于 #4405 的开放问题 #6 和 #7。

### 其他值得关注的功能方向

- **[#4492 Add lightweight LLM provider connections](https://github.com/OpenHands/software-agent-sdk/pull/4492)**（OPEN）
  为 LLM 增加 `provider_connection_id` 和 `/api/llm/provider-connections` CRUD，作为 OpenHands/OpenHands#15492 的轻量后端替代方案，可能影响 LLM profile 的配置方式。
- **[#4455 Backend: Model providers — provider store + nested models + named-secret key](https://github.com/OpenHands/software-agent-sdk/pull/4455)**（OPEN，draft）
  "连接一次供应商，在其下管理多个模型"的 provider-first 数据模型，被标记为 Blocking other PRs。结合 #4492 来看，LLM 供应商管理正在成为 SDK 的下一重点模块。
- **[#4084 WebSocket mode + previous_response_id continuation for Responses (GPT-5.6)](https://github.com/OpenHands/software-agent-sdk/issues/4084)** 与 **[#4085 Hosted Multi-agent vs client-side subagents](https://github.com/OpenHands/software-agent-sdk/issues/4085)** 仍处于 study 状态，GPT-5.6 新能力的适配论证尚未进入设计阶段。
- **[#4118 Define migration path from Python custom tools to client-defined tools](https://github.com/OpenHands/software-agent-sdk/issues/4118)** 提出为 Python 自定义工具迁移到 JSON `client_tools` 定义明确的路径，核心思路是"容忍加载未知历史 action/observation 类型"。


## 7. 用户反馈摘要

- **对高优 Bug 的反馈速度表示认可**：从 Issue 提交到修复 PR 的间隔来看，多个高优 Bug（#4487、#4494、#4498、#4491）均为「昨日提交、当日或次日即有 PR」，社区对维护者的响应速度预期较好。

- **LLM Profile 身份管理是隐蔽的可靠性隐患**：用户 @simonrosenberg 在 [#3841](https://github.com/OpenHands/software-agent-sdk/issues/3841)（已关闭）和 [#3713](https://github.com/OpenHands/software-agent-sdk/issues/3713) 中系统性地讨论了 AgentProfile/LLMProfile 身份不对称的问题——LLM profile 缺少稳定 id，依赖 rename-safe active pointer + refs，这与 #4494 报告的"默认 LLM 忽略活跃 profile 启动 stale keyless model"遥相呼应，说明 profile 体系仍需加固。

- **会话卡死问题持续困扰用户**：Issue [#3842](https://github.com/OpenHands/software-agent-sdk/issues/3842) 中用户描述"每个新用户消息都会触发 `agent_already_running` 错误"，且唯一恢复手段是重启服务。该问题 6 月下旬即已报告，至今无修复 PR，受影响用户可能面临长期困扰。

- **技能/插件加载的静默冲突**：用户 @jpshackelford 在 [#4015](https://github.com/

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，这是 2026-08-15 的 Pi 项目动态日报。

---

# Pi 项目动态日报 | 2026-08-15

## 1. 今日速览

Pi 项目在过去 24 小时内保持极高的迭代活跃度（**Issue 更新 142 条，PR 更新 24 条**），标志着该项目已进入高频修复与生态扩张阶段。今日发布了 **v0.84.2** 版本，重点优化了 TUI 全屏体验。社区关注焦点集中在 **Windows/WSL 兼容性**、**上下文压缩（Compaction）失灵**以及 **Copilot 登录限流** 等痛点。此外，AI 提供商集成（如 Kimi、SiliconFlow）在今日出现了大量合并与修复，项目正快速扩展其多提供商支持版图。

## 2. 版本发布

**v0.84.2** 已于今日发布。主要更新内容：

- **全屏转录搜索（Fullscreen transcript search）**：用户可以在全屏模式下搜索并跳转到转录匹配项，极大提升了长会话的历史检索效率。相关快捷键文档见 [TUI Fullscreen Viewport](https://github.com/earendil-works/pi/blob/v0.84.2/packages/coding-agent/docs/keybindings.md#tui-fullscreen-viewport)。
- **可配置默认工具（Configurable default tools）**：允许用户在启动时自定义默认启用的工具集。

*注意：本次更新未报告破坏性变更，但涉及 TUI 快捷键与启动配置项的调整，建议用户在升级后检查并更新个人配置文件。*

## 3. 项目进展

过去 24 小时合入/关闭了 12 个 PR，主要集中在**提供商兼容性修正**与**终端体验修复**上：

- **剪贴板修复（关键）**：PR [#8110](https://github.com/earendil-works/pi/pull/8110) 修复了 TUI 在 VTE 终端（如 GNOME Terminal）上“显示 Copied! 但剪贴板为空”的欺骗性问题，现改为通过宿主剪贴板（Host Clipboard）路由复制，解决了一个长期被诟病的体验缺陷。
- **Kimi 提供商修复（里程碑）**：PR [#8109](https://github.com/earendil-works/pi/pull/8109) 修复了 `api.kimi.com` 端点未被识别为 Moonshot 导致报错的问题；PR [#8104](https://github.com/earendil-works/pi/pull/8104) 将 kimi-coding 请求的静态 User-Agent 从 `KimiCLI/1.5` 改为 `pi/<version>`。
- **新提供商接入**：PR [#8113](https://github.com/earendil-works/pi/pull/8113) 新增了内置的 **SiliconFlow** 提供商支持，遵循 moonshot/minimax 模式。
- **品牌化兼容**：PR [#8067](https://github.com/earendil-works/pi/pull/8067) 修复了部分用户可见字符串未使用 `APP_NAME` 变量的问题，方便二次分发或品牌定制。
- **依赖解析修复**：PR [#8112](https://github.com/earendil-works/pi/pull/8112) 修复了使用 pnpm 安装扩展时，jiti 解析器无法正确处理隔离 node_modules 布局导致依赖加载失败的问题。

## 4. 社区热点

- **Windows 使用策略讨论（#7547）**：该 Issue 在 27 条评论中成为社区对 Windows 支持现状的大讨论。作者 @petrroll 发起调研，旨在确定 Pi 在 Windows 上的最佳运行方式（原生/WSL/容器）及核心修复优先级，大量 Windows 开发者在此反馈了遇到的碎片化问题。这已成为项目制定 Windows 路线图的核心参考文档。 [讨论链接](https://github.com/earendil-works/pi/issues/7547)
- **上下文压缩失效引发共鸣（#6879）**：该 Bug 获得 **17 个 👍** 和 20 条评论。用户 @alexanderkreidich 报告了严重问题：在 GPT-5.6 上运行 2 小时以上后，上下文占用超过 100% 但自动压缩未触发，直到 API 拒绝请求（373k tokens）才被迫压缩。评论区大量用户反映遇到同类问题，要求“在每个 agent 动作后检查压缩”。 [讨论链接](https://github.com/earendil-works/pi/issues/6879)
- **Copilot 登录被 429 拦截（#7850 / #8010）**：两个 Issue 指向同一个问题：当组织拥有 20+ 可用模型时，GitHub Copilot 登录因限流（Rate Limiting）直接失败。该问题已标记为 `no-action`（可能是服务端限制），但获得了 7 个 👍，受到企业用户的高度关注。 [Issue #7850](https://github.com/earendil-works/pi/issues/7850) | [Issue #8010](https://github.com/earendil-works/pi/issues/8010)

## 5. Bug 与稳定性

**高严重度（阻塞/需紧急关注）：**

- **自动压缩不触发**：Issue [#6879](https://github.com/earendil-works/pi/issues/6879)。上下文窗口使用率超过 100% 依然不触发压缩，直至 provider 溢出报错。标记为 `[OPEN]`，暂无专门 Fix PR，社区期望高。 *（PR #8120 提出了一种实验性“append compaction”模式，可能会缓解该机制，但默认未开启。）*
- **TUI 占用单核 100%**：Issue [#6665](https://github.com/earendil-works/pi/issues/6665)，标记为 `[inprogress]`。长会话流式输出时，由于未缓存的 `Intl.Segmenter` 和逐块 Markdown 重建导致 CPU 峰值。已有维护者介入（investigate状态）。
- **提示编辑器卡顿**：Issue [#8029](https://github.com/earendil-works/pi/issues/8029)，标记为 `[bug, inprogress]`。当输入框缓冲较大（~7000 行）时，单次方向键操作耗时高达 1650ms，线性增长严重。目前处于性能优化进行中。

**中严重度（已存在修复 PR 或已定位）：**

- **编辑模糊匹配失灵**：Issue [#7836](https://github.com/earendil-works/pi/issues/7836)，标记为 `[inprogress]`。因空白符长度不同导致 `oldText` 匹配失败，严重干扰小模型的编辑成功率。正在进行修复。
- **扩展加载器无法解析 pnpm 依赖**：Issue [#8092](https://github.com/earendil-works/pi/issues/8092)，已标记 `[CLOSED]`，由 PR [#8112](https://github.com/earendil-works/pi/pull/8112) 解决。
- **Windows 测试套件崩溃**：Issue [#8047](https://github.com/earendil-works/pi/issues/8047)。Pi Server 在 Windows 上尝试绑定 Unix Socket 失败，导致 31 个测试失败 `EACCES`，影响 Windows 平台的本地开发验证。
- **指数退避无上限**：Issue [#6303](https://github.com/earendil-works/pi/issues/6303)，已关闭。`getRetrySettings()` 不返回 `maxDelayMs`，导致退避时间无限增长（默认情况下第 7 次重试需等待约 4 分钟）。

## 6. 功能请求与路线图信号

- **Grok 4.6 支持**：用户在 Issue [#8046](https://github.com/earendil-works/pi/issues/8046) 请求添加 Grok 4.6，对应的 PR [#8124](https://github.com/earendil-works/pi/pull/8124) **正在待合并**。该 PR 会将 xAI 模型路由切换至 Responses API 并将默认模型从 Grok 4.5 更新为 4.6。
- **非空 Assistant 内容兼容标志**：用户 Issue [#8063](https://github.com/earendil-works/pi/issues/8063) 提出新增 `requiresNonNullAssistantContent` 标志，以应对部分 OpenAI 兼容网关拒绝重放工具调用消息的问题（要求空字符串 `""`而非 `null`）。修复已由 PR [#8118](https://github.com/earendil-works/pi/pull/8118) 创建并待合并。
- **Kimi 缓存 Token 统计**：PR [#8119](https://github.com/earendil-works/pi/pull/8119) 解决了 Kimi 聊天补全中 `usage.cached_tokens` 被忽略的问题，这将使计费与成本分析更为准确。对应 Issue #8075。
- **附加式上下文压缩（实验性）**：PR [#8120](https://github.com/earendil-works/pi/pull/8120) 提出在 `PI_EXPERIMENTAL=1` 下启用追加压缩（Append Compaction），通过复用 Provider 的提示缓存来优化压缩成本，但保持独立压缩（Standalone）为默认模式。这反映了在长会话成本控制上的新探索。

## 7. 用户反馈摘要

- **“WSL 登录挂起让我很痛苦”**：Issue [#6187](https://github.com/earendil-works/pi/issues/6187)（26 条评论）反映出 WSL 环境下 Copilot 浏览器授权流程存在断点——浏览器成功但 CLI 无响应。这提示项目组需要重点优化 **WSL 子系统的后台进程唤醒机制**。
- **“小模型的编辑成功率堪忧”**：在编辑模糊匹配问题 [#7836](https://github.com/earendil-works/pi/issues/7836) 的讨论中，用户 @robjgray 指出：“我发现这是小型模型编辑失败的根源”。这暴露出当前编辑器对模型输出的**容错性**（允许细微格式差异）仍有提升空间。
- **“TUI 的复制提示是在骗我”**：Issue [#7761](https://github.com/earendil-works/pi/issues/7761) 与 PR [#8110](https://github.com/earendil-works/pi/pull/8110) 形成了“投诉-修复”的良性闭环。很多 VTE 终端（GNOME Terminal）用户反馈复制结果实为空。此次更新终于将“闪烁提示”与“真实剪贴板”绑定。
- **“企业用户被 Copilot 429 卡死”**：Issue [#8010](https://github.com/earendil-works/pi/issues/8010) 描述了由于企业新激活模型过多导致登录 429，且每次重试失败均消耗一次设备授权码，形成死循环。目前标记为 `no-action`，但社区要求重试退避策略或引导引导的呼声较高。

## 8. 待处理积压

- **Windows 支持重心

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目日报 — 2026-08-15

## 1. 今日速览

项目保持极高活跃度：过去24小时内 PR 更新 279 条（待合并 176 / 已合并或关闭 103），Issues 更新 86 条（新开或活跃 73 / 已关闭 13），显示开发与社区反馈双向强劲。无新版本发布，但合并/关闭的 103 条 PR 表明代码库持续快速演进，多个稳定性与兼容性修复已落地。值得关注的是官方推出的“LiteLLM Stability Sprint Roadmap”（#30484）仍在接收社区反馈，说明稳定性被列为当前最高优先级的迭代方向。整体项目健康度良好，活跃度处于高位。

## 2. 版本发布

过去24小时无新版本发布。

## 3. 项目进展

今日合并/关闭的 PR 共 103 条，其中以下修复已确认合入，标志着项目在关键稳定性方向上的实际推进：

- **fix(transcription): 转录成本计算修复**（[#36914](https://github.com/BerriAI/litellm/pull/36914)）：修复 43/55 个按秒计费转录模型成本为 $0 的问题。此前输出速率为 0 会静默抑制真实输入速率，导致 deepgram、assemblyai、elevenlabs、groq 所有相关条目计费错误。
- **fix(proxy): PostgreSQL cached-plan 错误强制重建 Prisma**（[#36428](https://github.com/BerriAI/litellm/pull/36428)）：此前 cached-plan 恢复路径跳过 Prisma recreate，导致认证接口持续 503；即使数据库可达，过期的 prepared statement 仍会造成阻塞。本次修复引入了 `force_recreate` 参数并跳过 15 秒重连冷却。
- **fix(bedrock): 跨账号 Batch 创建签名时透传 litellm_params 中的 AWS 认证**（[#36449](https://github.com/BerriAI/litellm/pull/36449)）：此前跨账号 Bedrock batch 作业因签名前丢弃部署级认证而报 "Cross-account pass role is not allowed"。
- **fix(ui): auto-router 预设模型与 tier 下拉列表的 model group 对齐**（[#36440](https://github.com/BerriAI/litellm/pull/36440)）：修复 Add Auto Router 模板选择器中模组预设被错误置灰的问题。

同时，多条关键修复已在今日提交待合并，包括 brotli 响应解码（[#36977](https://github.com/BerriAI/litellm/pull/36977)）、Anthropic Responses 工具属性保留（[#36979](https://github.com/BerriAI/litellm/pull/36979)）、MCP 工具 guardrail 评估记录（[#36978](https://github.com/BerriAI/litellm/pull/36978)）等。整体来看，项目的修复面覆盖了计费、认证、跨云厂商兼容性和 UI 体验，且修复速度较快。

## 4. 社区热点

本期评论量最高、社区反应最强烈的话题集中在以下几条：

- **[#10177 Feature: Dark Mode](https://github.com/BerriAI/litellm/issues/10177)**（63 评论 / 71 👍）
  创建于 2025-04-20，至今仍为 OPEN 状态。请求为 UI 面板增加深色主题，用户自述 "I'm going blind"，表达了对默认亮色界面的强烈不适。这是当前社区呼声最高、跨越时间最长的功能请求之一，维护团队值得给出正式回应。

- **[#30484 LiteLLM Stability Sprint Roadmap](https://github.com/BerriAI/litellm/issues/30484)**（25 评论 / 6 👍）
  官方发布的稳定性优先路线图，列出 "/v1/model/info 返回不一致响应" 等已知问题，并公开征集本轮 bug 修复优先级。25 条评论表明社区对稳定性主题有高参与度，这是观察项目下一步修复重点的重要窗口。

- **[#33221 gpt-5.6 系列函数工具调用失败](https://github.com/BerriAI/litellm/issues/33221)**（10 评论 / 已关闭）
  用户报告 gpt-5.6-sol/luna/terra 在 /chat/completions 使用 function tools 时触发 `reasoning_effort` 相关错误。该 issue 已关闭，说明团队已定位并修复，但用户对新一代模型兼容性的期盼仍值得关注。

- **[#19138 Vertex AI 自定义 api_base 凭证跳过逻辑缺失](https://github.com/BerriAI/litellm/issues/19138)**（11 评论）
  用户使用自定义代理 + 自定义 api_base 访问 Vertex AI 模型，但库仍强制要求 Google 凭证并报 DefaultCredentialsError。该问题已开放 7 个月，讨论热度未减，属于长期未获充分解决的痛点。

## 5. Bug 与稳定性

本期报告中值得关注的 Bug 按严重程度排列如下：

| 严重程度 | Issue | 描述 | 状态 |
|---------|-------|------|------|
| 🔴 高 | [#25260](https://github.com/BerriAI/litellm/issues/25260) | Prisma query engine 在 Windows 上首次查询即崩溃（影响 1.82.x/1.83.0，最后正常版本 1.81.16），属于回归问题 | OPEN |
| 🔴 高 | [#24549](https://github.com/BerriAI/litellm/issues/24549) | 小米 MiMo 模型 `output_config` 参数导致 Claude Code 的 AsyncCompletions.create() 失败 | OPEN |
| 🟠 中 | [#34747](https://github.com/BerriAI/litellm/issues/34747) | `store_prompts_in_spend_logs: true` 配置已加载，但 SpendLogs.messages 仍持久化为 `{}`，acompletion 与 aresponses 均受影响 | OPEN |
| 🟠 中 | [#36559](https://github.com/BerriAI/litellm/issues/36559) | AnthropicMessagesConfig 将对话中段的 system role 提升至顶层 system 字段，使 prompt-cache 前缀完全失效 | OPEN |
| 🟡 低 | [#27186](https://github.com/BerriAI/litellm/issues/27186) | Responses API 流式转换未处理 `response.incomplete` 事件，导致 content_filters 被丢弃 | OPEN |
| 🟢 已修复 | [#33221](https://github.com/BerriAI/litellm/issues/33221) | gpt-5.6 函数工具 reasoning_effort 错误 | CLOSED |
| 🟢 已修复 | [#20933](https://github.com/BerriAI/litellm/issues/20933) | Python 3.14 下 uvloop 不兼容 | CLOSED |

另有两条已关闭的 issue 值得注意：#27384（provider_endpoints_support.json 与 UI 渲染组件不一致、vllm 重复显示）和 #27388（arize_phoenix span 未导出），均已解决。

**已有对应 fix PR 的 Bug**：
- 针对 brotli 压缩导致 passthrough 响应不可读的问题，[#36977](https://github.com/BerriAI/litellm/pull/36977) 已提交 fix。
- 针对 gpt-5-chat 部署因 `max_tokens`/`max_completion_tokens` 命名问题导致的 400 错误，[#36857](https://github.com/BerriAI/litellm/pull/36857)、[#36859](https://github.com/BerriAI/litellm/pull/36859) 已提交修复。

## 6. 功能请求与路线图信号

以下功能请求在社区中呼声较高，结合现有 PR 可以判断其被纳入下一版本的可能性：

- **深色模式**（[#10177](https://github.com/BerriAI/litellm/issues/10177)）：71 👍 / 63 评论，是最受欢迎的功能请求，但暂无对应 PR。考虑到 UI 团队近期持续在改进 dashboard（如 [#36868](https://github.com/BerriAI/litellm/pull/36868)、[#36440](https://github.com/BerriAI/litellm/pull/36440)），深色模式有望被官方提上日程。
- **自定义 provider 模型发现**（[#20064](https://github.com/BerriAI/litellm/issues/20064)）：10 👍，希望支持 `my-custom-service/*` 通配符的模型发现。该需求与 LiteLLM 持续扩展 provider 生态的方向一致。
- **Azure AI Foundry Agents v2 支持**（[#25372](https://github.com/BerriAI/litellm/issues/25372)）：请求适配 Responses API 的 `agent_reference` 模式，随着 Azure Foundry 在企业端普及，落地概率较高。
- **Ollama 文生图支持**（[#28026](https://github.com/BerriAI/litellm/issues/28026)）：`litellm.image_generation` 对 `ollama/...` 返回空 payload，请求补齐。
- **Bedrock requestMetadata 透传**（[#36861](https://github.com/BerriAI/litellm/pull/36861)）：该 PR 已提交，将 LiteLLM 身份与 metadata 转发至 Bedrock 请求元数据，用于费用归属，符合企业客户对成本可观测性的需求。
- **Auto Router v2 session_key_fallback**（[#36930](https://github.com/BerriAI/litellm/pull/36930)）：PR 已提交，为 `ComplexityRouter` 和 `AdaptiveRouter` 增加自动派生 session key 的能力。

另外，[#27180](https://github.com/BerriAI/litellm/issues/27180)（Anthropic-native /v1/models 响应格式，支持 Claude Code 网关模型发现）已关闭，说明该功能已实现或已合入。

## 7. 用户反馈摘要

从本期 Issues 与 PR 评论中可以提炼出以下真实用户声音：

- **可用性痛点**："I'm going blind."（[#10177](https://github.com/BerriAI/litellm/issues/10177)）—— 用户以近乎恳求的语气请求深色主题，说明默认 UI 的亮色设计对部分用户已构成实际使用障碍。这类反馈虽不涉及功能缺陷，但对用户留存有直接影响。
- **升级回归之痛**：Windows 用户在 1.82.x/1.83.0 上遭遇 Prisma 崩溃，回退到 1.81.16 才能正常工作（[#25260](https://github.com/BerriAI/litellm/issues/25260

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-15

## 1. 今日速览

过去 24 小时 Temporal 项目活跃度处于**中高水平**：3 条新 Issue 全部开放（无关闭），75 条 PR 更新中 62 条待合并、13 条已合并/关闭，显示核心开发与社区反馈仍在持续流入。值得注意的是，**今日无新版本发布**，且三条新 Issue 均为潜在 Bug（Nexus 请求头格式、DLQ 命令、持久化错误分类），反映当前阶段项目重点可能偏向稳定性修复与内部可靠性工程。PR 侧则呈现两个明显热点：**Worker-variant callbacks 功能推进**（#11589, #11456）和**测试基础设施报告流水线重构**（#11515–#11518 等一组堆叠 PR）。整体来看，项目处于繁忙的迭代中段，功能开发与稳定性加固并行。

## 2. 版本发布

今日无新版本发布。相关 release 渠道处于静默期，上一个版本线（如 release/1.32.0）仍在接受修复性 PR（如 #11564 针对 Elasticsearch 可见性时间格式的补丁）。

## 3. 项目进展

由于今日 PR 合并/关闭列表未被详细列出（仅统计为 13 条），以下基于活跃 PR 的推进情况总结项目当前演进方向：

- **Worker-variant callbacks 功能进入实质实现阶段**（#11589 by @chrsmith）：该 PR 是堆叠 PR 组的一部分，标记为"THIS IS IT!"——即 Worker 回调功能的实际实现，将为 Callback 组件增加 Worker 变体支持，扩展服务间调用与投递语义，是近期最具突破性的功能 PR。同时 #11456 也在同一 feature 分支上推进 CHASM Callback 组件对 Worker-variant 的支持。两条 PR 均尚未合入 main，但标志该特性已从设计走向实现。
- **Nexus 可靠性增强**：两条 PR 分别从追踪（#11559：为出站 Nexus HTTP 请求添加 OpenTelemetry 跟踪）和连接健康（#11581：为 Nexus/callback 传输启用 HTTP/2 keepalive）维度强化 Nexus 的链路可观测性与稳定性，体现出对跨集群/跨服务调用场景的持续打磨。
- **测试报告管线大规模重构**：@stephanos 一人提交了约 8 条堆叠 PR（#11513–#11518, #11487, #11488, #11033），从"定义 canonical Go 测试尝试结果模型"（#11514）到"采用 canonical report 流水线"（#11518），系统性重构测试结果记录、诊断范围、JUnit 渲染和重试规划。这是一个工程量可观且低层侵入性较强的内部基础设施改进，预计将提升自测与 flaky 定位效率。
- **Elasticsearch 可见性修复**（#11564）：改变日期时间格式为始终包含纳秒部分，避免 ES 中日期比较因缺少组件导致意外结果，并补齐了 ES 环境下的集成测试。

综合来看，项目在**功能扩展**（Worker callbacks）、**分布式系统韧性**（Nexus 追踪与连接保持）以及**开发者基础设施**（测试报告流水线）三线并进，处于一个多方向同时推进的活跃期。

## 4. 社区热点

今日讨论热度整体不高，所有可见 Issue/PR 的评论数和 👍 数均较少。相对最受关注的是：

- **[Issue #11569] Nexus: server may send malformed `request-timeout` header**（[@mjameswh](https://github.com/mjameswh)，1 条评论）：该 Issue 指出服务端发出的 `request-timeout` 头可能包含负值以及 Nexus 语法之外的时间单位（如 `h` 或 `us`），违反其自身解析器所遵循的规范。这属于协议自洽性缺陷——服务端产出的东西自己都解析不了——在分布式系统中会引发隐性兼容风险。评论者正在讨论正确的修复位置。链接：https://github.com/temporalio/temporal/issues/11569

此外，PR #11589（Worker-variant callbacks）虽无评论，但因标有 "THIS IS IT!" 的里程碑性质，在关注 callbacks 特性的开发者群体中预计关注度较高。

## 5. Bug 与稳定性

今日无崩溃级或数据损坏级 Bug，但有 3 个新报告的可疑问题，按严重程度排列如下：

| 严重程度 | Issue | 描述 | 修复 PR | 链接 |
|---------|-------|------|--------|------|
| 中高 | #11569 | Nexus 服务端可能在 `request-timeout` 头中发送**负数时间值**及超出 Nexus 语法的时间单位（如 `h`/`us`），与服务器自身解析器接受的语法（无符号 + `ms`/`s`/`m`）不符。可能导致下游无法解析请求头而拒绝请求。 | 尚未见对应 PR | https://github.com/temporalio/temporal/issues/11569 |
| 中 | #11571 | `service/history/api/get_history_util.go:358` 将持久化限流器产生的 `*serviceerror.ResourceExhausted` 错误转换为 `*serviceerror.Unavailable`。这会**丢失"限流"语义**，使客户端收到 `Unavailable` 后可能立即重试而非遵循退避策略，进一步加重限流压力。 | 暂无 | https://github.com/temporalio/temporal/issues/11571 |
| 中低 | #11586 | `tdbg dlq` 命令拒绝处理**归档（archival）DLQ**（task category 5），而同类历史任务类别可正常 `list`/`merge`/`purge`。运维人员无法通过 tdbg 红驱归档死信任务，需手工介入。 | 暂无 | https://github.com/temporalio/temporal/issues/11586 |

三项 Bug 均暂未关联到已修复的 PR，提示这些是新进入队列的待处理问题，需要维护者分配标签并排期。

## 6. 功能请求与路线图信号

今日无用户直接提交的新功能请求（以 `[feature-request]` 等标签出现）。但从 PR 可观察到明确的路线图信号：

- **Worker-variant callbacks（#11589, #11456）**：已处于实现中且 PR 明确标注"逐步合入 feature 分支，整体完成后进入 main"，这是一个经过设计评审后进行中的主线特性，预计会随 feature 分支合入出现在后续版本中。
- **Nexus operation auto-close policy【prototype】（#11577）**：处于原型验证阶段，若设计确认，可能进入下几个版本的规划中，扩展 Nexus 操作的生命周期管理语义。
- **测试基础设施的 canonical attempt results 模型（#11514 等）**：这是内部工程质量的长期投资，短期不会对用户可见 API 产生影响，但将为未来 flaky test 治理、CI 速率提升打下基础。

综合来看，**Worker callbacks** 是近期最可能进入下一版本的用户可见特性；Nexus 相关的持续增强（可观测性、连接保持、超时语法）也在稳步推进。

## 7. 用户反馈摘要

由于今日 Issue 评论总体较少（仅 #11569 有 1 条评论），以下提炼自 Issue 描述所反映的用户痛点：

- **@mjameswh（#11569）**：作为 Temporal 内部或深度用户，明确指出服务器生成的头部字段违反自身声明的协议字典，透露出对**协议严谨性和跨版本兼容性**的高要求。这类反馈通常由长期维护大型生产集群的团队提出，他们的核心诉求是"服务端必须始终产出自洽的语义"，以便客户端可以信任协议契约。
- **@tsurdilo（#11586）**：来自运维/平台工程场景。当 DLQ 使用 `tdbg` 命令管理时遇到其无法处理归档任务，痛点在于**运维工具覆盖面不全**，导致本可通过命令行完成的日常运维操作被迫退化为手工数据库/API 操作，增加了操作复杂度和出错概率。
- **@dssysolyatin（#11571）**：关切点在于**错误类型的语义保真**。当客户端依赖 `ResourceExhausted` 做重试/退避决策时，被降级为 `Unavailable` 会破坏客户端侧的服务治理逻辑。这暗示用户的调用链上存在对错误类型敏感的弹性策略层。

整体反馈风格是技术深度较高、面向生产环境的严谨性诉求，当前未有"满意度"类正面或负面情感表达。

## 8. 待处理积压

以下为值得维护者特别关注的长周期未合并/未响应条目：

- **[PR #11033] Return test runner orchestration outcomes**（@stephanos，2026-07-13 创建，距今已 **33 天未合并**）：该 PR 是测试报告重构堆叠链中的一个环节，整体链条已有 PR 依赖关系（其依赖 #11514 等），因此单一 PR 的延迟并不代表停滞，但整条链路跨越一个多月，建议维护者关注堆叠链的整体合并节奏，避免技术债随时间积累。链接：https://github.com/temporalio/temporal/pull/11033

- **[Issue #11569] Nexus malformed request-timeout header**（2026-08-14 创建）：虽然刚创建，但因其属于**协议级正确性问题**，建议尽快分配 label 并给出确认，以免与后续涉及 Nexus 请求头的 PR 产出冲突。链接：https://github.com/temporalio/temporal/issues/11569

---

*本日报基于 2026-08-14 至 2026-08-15 的 GitHub 数据自动汇总生成。所有链接指向对应 GitHub Issue/PR 页面。*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*