# OpenClaw 生态日报 2026-09-16

> Issues: 463 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-16 00:30 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报

**报告日期：2026-09-16** ｜ 数据窗口：过去 24 小时

---

## 1. 今日速览

- **活跃度处于高位**：过去 24 小时 Issues 更新 463 条（新开/活跃 292、关闭 171），PR 更新 500 条（待合并 357、合并/关闭 143），但**零新版本发布**——工程注意力集中在修复与评审，而非发版。
- **稳定性债务是今日主线**：P0/P1 级别的崩溃、内存泄漏、进程僵尸化、SQLite WAL 膨胀、以及 2026.9.3 → 2026.9.4 的升级失败占据了大部分高优先级讨论。
- **评审积压明显**：待合并 PR（357）是已合并/关闭（143）的约 2.5 倍，其中大量为维护者 @steipete 提交的性能/会话状态优化，形成"产出快、合并慢"的瓶颈。
- **健康度评估**：贡献动能强（性能与稳定性修复密集落地），但 **2026.9.x 发布序列的回归密度值得警惕**，多个 P0 直指升级流程与 release blocker 标签。
- **信号**：今日有多个针对"会话放置/工具授权快照"类消息丢失问题的 fix PR（#149518、#149292），指向 2026.9.4 的一类共性回归正在被收敛。

---

## 2. 版本发布

**无新版本发布**（过去 24 小时 Releases 为 0）。

但需注意：Issues 中大量回归报告集中于 **2026.9.3 / 2026.9.4**（如 #144809、#148707、#146637、#144739），说明最近一次发布的稳定性仍在消化中，维护者当前更可能处于"修复未发版"阶段。

---

## 3. 项目进展

今日合并/关闭侧共 143 条，公开可见的高价值推进集中在**性能与状态一致性**方向（注：PR 列表未提供评论数，以下按标签与影响面挑选）：

| PR | 内容 | 意义 |
|---|---|---|
| [#149511](https://github.com/openclaw/openclaw/pull/149511) | 减少复用 shared-state 数据库时的开销 | 降低 SQLite schema 写入抖动，网关热路径提速 |
| [#149462](https://github.com/openclaw/openclaw/pull/149462) | 修复压缩后过早触发上下文溢出（Closes #149425） | P1，长会话可用性 |
| [#149005](https://github.com/openclaw/openclaw/pull/149005) | MCP/LSP stdio 清理不再过早超时 | 直接缓解"子进程清理身份丢失"类崩溃（关联 #144911） |
| [#149047](https://github.com/openclaw/openclaw/pull/149047) | 更新后重启通知写入正确 state 目录 | 修复路由更新的副作用 |
| [#149404](https://github.com/openclaw/openclaw/pull/149404) / [#149496](https://github.com/openclaw/openclaw/pull/149496) / [#149308](https://github.com/openclaw/openclaw/pull/149308) | 冷会话库搜索提速、复用 transcript root 策略、避免旧库检查 | 网关读路径系统性减负 |
| [#149372](https://github.com/openclaw/openclaw/pull/149372) | GitHub 发布账号发现缓存（原 p90 6.6s，1 小时 1328 次调用） | 生产环境可观测到的实打实延迟优化 |
| [#147886](https://github.com/openclaw/openclaw/pull/147886) / [#149497](https://github.com/openclaw/openclaw/pull/149497) | Feishu markdown 表格模式、混合大小写账号匹配 | 修复渠道启动阻塞 |
| [#137831](https://github.com/openclaw/openclaw/pull/137831) | Linux service unit 保留字面路径（Closes #137747） | 修复含空格/特殊字符路径的服务启动失败 |

**净推进判断**：项目在"网关吞吐/会话检索/插件加载"层面的工程化改进明显；但**功能面新增有限**，今日更接近一次大型性能与可靠性加固。

---

## 4. 社区热点

按评论数排序，讨论热度最高的议题呈现三条主线：

**A. 内部输出泄漏到用户可见渠道（安全 + UX）**
- [#25592](https://github.com/openclaw/openclaw/issues/25592)（40 评论，🦞 diamond lobster）— 工具调用之间的文本被路由到 Slack/iMessage 等渠道，暴露内部处理输出。标签包含 `needs-product-decision`、`needs-security-review`，**自 2 月 24 日挂起至今**。
- [#143278](https://github.com/openclaw/openclaw/issues/143278)（7 评论）— heartbeat 内部输出泄漏到 Telegram 私聊，2026.9.3 升级后出现。
- 背后诉求：Agent 的"内心独白"必须有明确的可信边界，否则既是 UX 事故也是信息泄露面。

**B. 资源泄漏与进程管理（运行时退化）**
- [#97616](https://github.com/openclaw/openclaw/issues/97616)（30 评论）— hook/tool 子进程僵尸堆积。
- [#91588](https://github.com/openclaw/openclaw/issues/91588)（25 评论）— 网关 RSS 从 350MB 涨到 15.5GB，数天后 OOM。**已过期（stale）但仍未见修复 PR**。
- [#91009](https://github.com/openclaw/openclaw/issues/91009)（24 评论，**P0**）— Codex PreToolUse hook 中继产生 CPU 满载的 `openclaw-hooks` 进程并阻塞网关 RPC。

**C. 会话/事件循环阻塞**
- [#119720](https://github.com/openclaw/openclaw/issues/119720)（20 评论）— 同步式 agent 持久化与 transcript 维护阻塞事件循环，虽有部分修复落地，但报告者认为规模化下仍存在。
- [#102175](https://github.com/openclaw/openclaw/issues/102175)（19 评论）— 嵌入式 prompt cache 在 room-event / policy / Responses 边界反复失效，涉及 `needs-security-review`。

---

## 5. Bug 与稳定性

### P0（发布阻塞级）

| Issue | 问题 | Fix PR 状态 |
|---|---|---|
| [#91009](https://github.com/openclaw/openclaw/issues/91009) | Codex hook 进程 CPU 满载、网关 RPC 停滞 | ❌ 未见 |
| [#143524](https://github.com/openclaw/openclaw/issues/143524) | Windows 上 agent SQLite WAL 涨到 1.4–2.8GB，阻塞启动 | ❌ 标签 `needs-info` |
| [#146637](https://github.com/openclaw/openclaw/issues/146637) | 2026.9.3 → 2026.9.4 npm 全局安装交换失败 | ❌ 未见 |
| [#144739](https://github.com/openclaw/openclaw/issues/144739) | 2026.9.4 更新时用旧版本跑 schema-17 候选状态 | ❌ 未见 |
| [#115642](https://github.com/openclaw/openclaw/issues/115642) | 计费冷却期长于故障本身，订阅认证被锁 5 小时 | ❌ 未见（建议加 probe 恢复 + 手动重置） |
| ~~[#148866](https://github.com/openclaw/openclaw/issues/148866)~~ | `gateway.bind=lan` 导致网关永久重启循环 | ✅ **

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报
**报告日期：2026-09-16** ｜ 数据源：github.com/OpenHands/software-agent-sdk

---

## 1. 今日速览

过去 24 小时项目维持**高活跃度**：22 条 Issue 更新（新开/活跃 12、关闭 10）、50 条 PR 更新（待合并 45、已合并/关闭 5），并发布 1 个新版本 v1.48.0。当日关闭的 Issue 中，安全类与 agent-server 稳定性类缺陷占主导（如 [#4399](https://github.com/OpenHands/software-agent-sdk/issues/4399) 密钥明文写入 `.git/config`、[#4386](https://github.com/OpenHands/software-agent-sdk/issues/4386)/[#4387](https://github.com/OpenHands/software-agent-sdk/issues/4387) 事件服务异常吞没与超时竞态），说明维护者正在清理安全与执行层技术债。**需要关注的是 PR 审查侧的结构性拥堵**：45 条待合并 PR 对 5 条合入，合并/关闭比约 1:9，且多条 PR 以 Draft 状态滞留数周（如 [#3403](https://github.com/OpenHands/software-agent-sdk/pull/3403) 自 5 月 27 日起、[#4183](https://github.com/OpenHands/software-agent-sdk/pull/4183) 自 7 月 22 日起）。社区外部贡献者活跃，今日新报缺陷（[#5082](https://github.com/OpenHands/software-agent-sdk/issues/5082)、[#5084](https://github.com/OpenHands/software-agent-sdk/issues/5084)）在数小时内即被闭环，响应速度良好。

---

## 2. 版本发布：v1.48.0

**发布内容（据现有数据，变更列表可能不完整）：**

| 类型 | 变更 | 作者 | PR |
|---|---|---|---|
| fix(ci) | 为已合并的 artifact 清理流程自动开启 PR | @enyst | [#4933](https://github.com/OpenHands/software-agent-sdk/pull/4933) |
| fix(tools) | 新增日志过滤器，从 libtmux 日志输出中**脱敏密钥** | @all-hands-bot | [#4871](https://github.com/OpenHands/software-agent-sdk/pull/4871) |
| fix(sdk) | （变更说明在数据源中被截断） | — | — |

**解读与迁移提示：**
- 本版本为**补丁级安全与 CI 修复版本**，未标注 `breaking-change` 标签，预期无破坏性变更。
- 重点关注日志脱敏修复：若你的部署从 libtmux 日志中采集遥测，升级后敏感字段将不再出现在日志流中，**依赖原始日志的下游解析规则可能需要调整**。
- 由于发布说明不完整（PR 列表被截断），建议以 v1.48.0 的完整 PR 列表为准核对是否包含其他 SDK 修复。

---

## 3. 项目进展（今日合并/关闭的重要变更）

**已关闭的 PR（1 条可见）：**
- [#5088](https://github.com/OpenHands/software-agent-sdk/pull/5088) `feat(agent-server): publish python-minimal image`（@neubig）：为 amd64/arm64 发布真正的 `python-minimal` 运行时镜像。此前 #5077 已加入 Debian 基础的 `binary-minimal` 目标，但发布工作流只推送完整 `binary` 目标（映射为 `python` / `python-slim`），用户无法从 GHCR 拉取最小运行时。**该项推进了镜像分发的完整性，降低了轻量部署的资源占用门槛。**

**已关闭的关键 Issue（体现问题清理进度）：**
- [#5082](https://github.com/OpenHands/software-agent-sdk/issues/5082)（priority:high）`ask_agent()` 在 LLM 调用进行中被调用时崩溃 `cannot pickle 'generator' object` — **当日报告、当日关闭**。
- [#5084](https://github.com/OpenHands/software-agent-sdk/issues/5084)（ci）examples CI 在 `17_convo_with_agent_sandbox_server.py` 上因缺少 `k8s_agent_sandbox` 模块持续失败 — 当日闭环。
- [#5041](https://github.com/OpenHands/software-agent-sdk/issues/5041) 四个搜索端点误用 `

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 · 2026-09-16

> 数据窗口：2026-09-15 ~ 2026-09-16（过去 24 小时）
> 仓库：[earendil-works/pi](https://github.com/earendil-works/pi)

---

## 一、今日速览

今日是**高强度的积压清理日**：157 条 Issue 更新中 127 条被关闭（关闭/新开比约 **4.2:1**），17 条 PR 中 11 条合并或关闭，维护团队的分诊与合入节奏明显处于高峰期。其中最受关注的一条是积压近 5 个月的 `#2870 Follow XDG Base Directory`（22 条评论、60 个 👍）终于关闭，属于社区长期诉求的兑现。与此同时，仍在 OPEN 的 Issue 集中在**上下文预算/压缩溢出、provider 适配器细节、Windows 平台路径解析**三类硬骨头上，说明表层易修问题正在被清空，剩余问题技术门槛更高。项目在**扩展（Extension）API 治理**方向动作密集（今日关闭 6 条相关 Issue + 3 条相关 PR），结合 mitsuhiko 提交的两条架构级 PR（`#9548` 会话中途 system message、`#6534` developer role），可以判断项目正处于一次**会话模型重构**的前夜。整体健康度**良好偏强**：无新版本发布，但代码与设计层推进显著。

---

## 二、版本发布

今日无新版本发布（Releases: 0）。当前社区讨论中出现的在版版本为 `0.85.1`、`0.84.4`、`0.83.0`，可作为下一轮发版前的基线参考。

---

## 三、项目进展

今日 11 条 PR 合并/关闭，按影响力排序：

### 架构与协议层
- **[#6534] feat(ai): add developer message role**（[@mitsuhiko](https://github.com/earendil-works/pi/pull/6534)）— 引入 `developer` 角色（关联 RFC 54 实验结果）。自 07-11 挂起，今日关闭，是消息模型的一次实质性扩展。
- **[#9548] Mid conversation system messages**（[@mitsuhiko](https://github.com/earendil-works/pi/pull/9548)）— 仍为 OPEN。让 system prompt 文本与工具变更**进入 transcript**而非静默改写起始条件，从而支持记录指令变更时点、分支恢复、以及缓存前缀保持。**这是今天最重要的方向性 PR**。
- **[#9620] feat(ai): 将 OrcaRouter 接入为一等 provider**（含 API-Key 与 OAuth 2.0 PKCE 双登录路径、能力过滤的实时模型列表）— [链接](https://github.com/earendil-works/pi/pull/9620)。

### Provider 适配修复
- **[#9619] fix(ai): 保留 Anthropic 模型可见的根级 schema 组合器**（关闭 #9134）— 此前 Anthropic 对根级 `anyOf/oneOf/allOf` 返回 400，适配器直接丢弃，导致模型看到的参数组合与运行时校验不一致。[链接](https://github.com/earendil-works/pi/pull/9619)
- **[#9646] / [#9648] Baseten provider header & session affinity**（[@AlexKer](https://github.com/earendil-works/pi/pull/9648)）— 从 `sessionId` 派发 Baseten 会话亲和性请求头。
- **[#9607] fix(coding-agent): 将 provider hooks 应用于摘要流** — 修复 compaction / branch summary 绕过 `before_provider_request` 钩子的问题。[链接](https://github.com/earendil-works/pi/pull/9607)

### 扩展 API 治理（今日主战场）
- **[#9642]** 导出 `ExtensionAPI.on()` 所需的全部事件与结果类型（`MessageEndEventResult`、`ThinkingLevelSelectEvent`、`ModelSelectSource`）。[链接](https://github.com/earendil-works/pi/pull/9642)
- **[#9611]** 移除 `prompt-url-widget` 扩展中已废弃的 `session_switch` 处理器（迁移至 `session_start` + `event.reason`），清理 API 迁移遗留。[链接](https://github.com/earendil-works/pi/pull/9611)
- **[#9483] fix(coding-agent): 将工具 cwd 解析改为 opt-in（`customCwd`）** — 修复 `#8627` 合并后引入的向后兼容回归。[链接](https://github.com/earendil-works/pi/pull/9483)
- **[#9635]** 隔离 documentation-lift 评测：host evals 与 Docker 对比分离，每个 `(case, variant, model, repetition)` 组合在全新容器中运行。[链接](https://github.com/earendil-works/pi/pull/9635)

### 用户可见功能
- **[#9615] feat(coding-agent): add `/forget` 命令**（[@robert896r1](https://github.com/earendil-works/pi/pull/9615)）— 从模型上下文中移除最近 N 轮用户输入，可选同步删除会话文件记录，支持 Soft/Hard 两种模式。

**整体推进度评估**：今日合入以**协议健壮性**（Anthropic schema、摘要流钩子、Baseten 亲和性）与**扩展 API 收口**为主，属于"消除技术债 + 为下一版铺路"型工作日，而非功能爆发日。

---

## 四、社区热点

### 🔥 [#2870] [CLOSED] Follow XDG Base Directory · 22 评论 / **60 👍**
[@mks-h](https://github.com/earendil-works/pi/issues/2870) | 创建 2026-04-06 → 关闭 2026-09-15
Linux 用户长期抱怨 Pi 把配置/状态目录散落在 `$HOME` 下，要求遵循 XDG 规范（`$XDG_CONFIG_HOME`，默认 `~/.config`）。**这是过去 24 小时内反应数最高（60 👍）的 Issue，且是积压最久（162 天）的一条**。它的关闭是 Linux 桌面用户群体的一次明确胜利，也说明维护团队在高优社区诉求上并未忽视，只是排期较长。

### [#8061] [OPEN][inprogress] Context budget 忽略 maxTokens 输出预留 · 9 评论
[@Nuctori](https://github.com/earendil-works/pi/issues/8061)
输入仅占模型窗口 ~78% 仍被 provider 拒绝，且自动 compact-and-retry 恢复在重试时**以同样原因再次失败**。涉及 1,048,576 token 上下文模型（Gemini 系经 OpenAI 兼容网关）。这是今日 OPEN 状态中评论最多的一条，直接指向上下文预算计算的核心逻辑缺陷。

### [#7010] [OPEN] 为 OpenAI 兼容 provider 规范化可选 object tool schema · 8 评论
[@hsm-lv](https://github.com/earendil-works/pi/issues/7010) | 创建 2026-07-23
`@earendil-works/pi-ai` 向 OpenAI 兼容 chat-completions provider 转发工具 JSON Schema 时，未对 object schema 的 `required` 做规范化。自 7 月底挂起，已积压 **55 天**。

### [#8791] [OPEN] 向扩展暴露 model runtime · 3 评论 / **5 👍**
[@rsolmano](https://github.com/earendil-works/pi/issues/8791)
希望 `ExtensionContext` 暴露 `modelRuntime`（readonly 属性），以便扩展创建进程内隔离的 agent session。反映**扩展生态正从"UI 装饰"走向"自建 agent 编排"**的真实需求。

**诉求分析**：社区热点明确分成两层——底层用户诉求聚焦**平台规范遵从与上下文预算的可靠性**（XDG、overflow 恢复），上层开发者诉求聚焦**扩展 API 能力的纵深**（runtime 暴露、事件类型导出、原子空闲提交）。两者都在今天得到了正向回应。

---

## 五、Bug 与稳定性

按严重程度排列（🔴 高 / 🟠 中 / 🟡 低）：

### 🔴 高严重度

| Issue | 摘要 | Fix PR 状态 |
|---|---|---|
| [#9306](https://github.com/earendil-works/pi/issues/9306) `[inprogress]` | 回合以 `error`/`aborted` 结束但 assistant 消息已流出 `toolCall` 块时，**未匹配的 toolCall 残留在上下文中**，导致下一次 `runAgentLoopContinue` 被 provider 直接拒绝 —— 会话陷入不可续状态 | 标记 `inprogress`，尚无关联 PR |
| [#8061](https://github.com/earendil-works/pi/issues/8061) `[inprogress]` | Context budget 未预留 `maxTokens` 输出空间；输入 78% 即被拒；**overflow 恢复重试以同因失败** | 标记 `inprogress`，无关联 PR |
| [#9571](https://github.com/earendil-works/pi/issues/9571) | `provider-retry.ts:61` 中，`retry-after` 为非数值时执行 `Date.parse(retryAfter) - Date

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 · 2026-09-16

> 数据来源：github.com/BerriAI/litellm ｜ 统计窗口：2026-09-15 ~ 2026-09-16（过去 24 小时）

---

## 一、今日速览

LiteLLM 今日维持**高强度迭代节奏**：24 小时内 Issues 更新 74 条（新开/活跃 53、关闭 21），PR 更新高达 346 条（待合并 210、已合并/关闭 136），合并/关闭率约 39%，并发布 1 个新版本 v1.101.0。整体看，项目处于"高吞吐、高积压"状态——新增 PR 数量远超消化速度，待合并 PR 池持续膨胀至 210 条，需关注评审带宽瓶颈。今日修复面集中在 **spend 追踪、组织/团队预算、MCP 与 OAuth 凭据、Cohere/Bedrock provider 转换**等核心链路，说明维护者正着力收敛企业级多租户场景的账务与鉴权缺陷。社区侧最强烈的信号是**按天（RPD/TPD）限流**与**配置 JSON Schema**两项诉求，均获得较高点赞但长期未落地。

---

## 二、版本发布

### v1.101.0

**发布要点（Release Note 摘要）：**

本次 Release 说明的核心内容是 **Docker 镜像签名验证机制**：

- 所有 LiteLLM Docker 镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 进行签名；
- 每个 release 均使用自 commit [`0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0) 引入的同一密钥签名；
- Release 正文提供了镜像签名校验的操作指引。

**破坏性变更 / 迁移注意事项：**

- 从本次披露的信息看，**未发现破坏性变更或强制迁移项**。v1.101.0 的公开说明聚焦于供应链安全（镜像签名校验），属于运维侧增强。
- 建议自托管用户在生产部署前，按 Release 指引补充 cosign 验签步骤，以对应上游安全基线。
- ⚠️ 注意：本次提供的 Release 内容被截断，其余变更条目（changelog）未包含在数据快照中，建议直接查阅 [Releases 页面](https://github.com/BerriAI/litellm/releases/tag/v1.101.0) 获取完整清单。

**关联维护动作：** 同期 PR [#41323](https://github.com/BerriAI/litellm/pull/41323) 已合并——将 #41230 回移至 `stable/1.99.x` 分支并发布 **1.99.2**，修复内容为：调用方自身超时不再导致共享 deployment 被冷却（cooldown），以及回退路径此前会跳过所有标记为 408 的响应。这是对稳定分支的重要补丁。

---

## 三、项目进展（今日合并/关闭的重要 PR）

今日共 **136 条 PR 被合并或关闭**，以下为推进项目前进的关键项：

### 🔐 认证与企业集成（进度最大）

| PR | 内容 | 状态 |
|---|---|---|
| [#35234](https://github.com/BerriAI/litellm/pull/35234) | **原生 OIDC 客户端元数据广播**：使 `lite login` 不再只能走 proxy 中介的 SSO；CLI 端可获知信任的 IdP，开启 headless 设备码登录路径 | CLOSED |
| [#30633](https://github.com/BerriAI/litellm/pull/30633) | **Azure 无密码数据存储认证**：PostgreSQL 支持 Entra token，Redis 支持 Azure AD 凭据提供者，贯通 writer/reader/CLI 启动路径，不再依赖静态密码 | CLOSED |
| [#30988](https://github.com/BerriAI/litellm/pull/30988) | **Skills Gateway 面向编码 Agent 开放**：新增 `/opencode/skills` 与 Agent Skills 发现端点，复用既有鉴权，仅暴露启用中的 skill | CLOSED |

> 这三项合并意味着 LiteLLM 正从"模型网关"向"**企业身份 + Agent 工具网关**"演进，是清晰的战略信号。

### 💰 账务与预算准确性（修复密集）

| PR | 内容 | 状态 |
|---|---|---|
| [#41302](https://github.com/BerriAI/litellm/pull/41302) | **Key 级 model rpm/tpm 覆盖优先级修正**：此前 Team 的 `model_rpm_limit` 反而压过 Key 自身覆盖，与文档承诺相反；现已对齐"Key metadata > Key model_max_budget > Team metadata" | CLOSED |
| [#41255](https://github.com/BerriAI/litellm/pull/41255) | **按成员统计组织花费**：修复 Organizations > Members 中 Spend 全部显示 `-`、成员花费恒为 0 的问题 | CLOSED |
| [#28274](https://github.com/BerriAI/litellm/pull/28274) | **Redis 语义缓存支持 Responses 输入**（Fixes #28272） | CLOSED |

### 🧩 Provider 与模型信息

| PR | 内容 | 状态 |
|---|---|---|
| [#41320](https://github.com/BerriAI/litellm/pull/41320) | **Gemini 2.5+ 通配基线回退**：未映射的 Gemini ID（如 `gemini/gemini-4-pro`）不再抛 "model isn't mapped yet"，并正确识别 `supports_reasoning` | CLOSED |
| [#41316](https://github.com/BerriAI/litellm/pull/41316) | **NVIDIA NIM 直通路由**：新增 `/nvidia_nim` 路由支持物体检测与 OCR 的 `POST /v1/infer`，此前一律 404 且绕过虚拟 Key 鉴权与花费记账 | CLOSED |

### 🚧 待合并高价值 PR（评审中）

- [#41314](https://github.com/BerriAI/litellm/pull/41314) `fix(mcp)`: JWT 用户的上游 OAuth 凭据持久化
- [#41330](https://github.com/BerriAI/litellm/pull/41330) `feat(team)`: 团队级 `model_max_budget` + Key 级覆盖
- [#41329](https://github.com/BerriAI/litellm/pull/41329) `feat(guardrails)`: Singulr v2 API 契约（`logging_only`、`pre/post_mcp_call`）
- [#41310](https://github.com/BerriAI/litellm/pull/41310) `feat(proxy)`: 可配置的模型访问拒绝消息（避免泄露 access group 与 fallback 映射）
- [#41177](https://github.com/BerriAI/litellm/pull/41177) `fix(proxy)`: 基于持久缓存历史估算 auto-router 基线成本
- [#41327](https://github.com/BerriAI/litellm/pull/41327) `feat(s3)`: `s3_log_prompts_only`，仅记录 prompt 不记录 response

**整体推进度评估：** 今日净推进显著，尤其在 **身份联邦（OIDC/Azure）、限流优先级语义、组织花费统计** 三个长期痛点上有实质修复。但 210 条待合并 PR 的存量表明，**评审吞吐已成为项目健康的头号约束**。

---

## 四、社区热点

### 讨论最活跃的 Issues

**1. [#8328](https://github.com/BerriAI/litellm/issues/8328) — Key alias 需在所有用户间唯一（15 条评论，👍2，OPEN，stale）**
> 创建于 2025-02-06，已挂起超过 **19 个月**。用户期望不同用户可以各自创建同名 key alias，由系统内部消歧。关联早期 issue #2932。

**背后诉求：** 多租户场景下 alias 被当作全局命名空间，导致用户无法用自己习惯的命名（如 `prod`、`default`）。这是**数据模型层面的设计债**，修复成本高，因此长期搁置 —— 但持续有人追问，说明影响面不小。

**2. [#10788](https://github.com/BerriAI/litellm/issues/10788) — 无法关闭请求 INFO 日志（13 条评论，CLOSED）**
> 用户反馈 `LITELLM_LOG=ERROR` 不生效，proxy 日志被每个请求的 INFO 行刷满。

**背后诉求：** 典型的生产环境日志成本问题（存储/采集费用 + 信噪比）。已关闭，值得在 Release Note 中确认修复版本。

**3. [#14398](https://github.com/BerriAI/litellm/issues/14398) — 按天请求/Token 限流（12 条评论，👍8 ⭐最高赞，OPEN）**
> 当前仅支持 RPM/TPM，缺乏 RPD/TPD。用户指出 OpenAI 免费/Pro 层普遍存在日限额（如 1M tokens/day）。

**背后诉求：** 这是**上游配额映射**的真实缺口——网关无法表达 provider 的日粒度限额，导致用户

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*