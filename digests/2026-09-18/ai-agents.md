# OpenClaw 生态日报 2026-09-18

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-17 22:35 UTC

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

# 横向对比分析报告｜个人 AI 助手 / 自主智能体开源生态  
**报告日期：2026-09-18**  
**数据缺口说明：** OpenClaw、Hermes Agent、Temporal 当日摘要为空，无法参与量化对比。以下量化分析主要覆盖 OpenHands SDK、Pi、LiteLLM；OpenClaw 仅作生态位定性判断。

---

## 1. 生态全景

2026-09-18 的社区动态显示，个人 AI 助手 / 自主智能体生态已从“能力演示”进入“生产可靠性 + 生态标准化”阶段。高活跃项目集中处理 Docker 会话运行时、流式挂起、上下文压缩、计费准确性和插件安全等硬问题。OpenHands SDK 在快速清剿 Docker 缺陷并推进 Agent Plugins，Pi 在压缩与 T

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报
**报告日期：2026-09-18** ｜ 数据窗口：过去 24 小时
**仓库：** [OpenHands/software-agent-sdk](https://github.com/OpenHands/software-agent-sdk)

---

## 1. 今日速览

今日项目处于**高活跃度状态**：24 小时内 Issues 更新 34 条（新增/活跃 23、关闭 11），PR 更新 50 条（待合并 43、合并/关闭 7），并连续发布 2 个补丁版本（v1.49.1、v1.49.2）。活动高度集中在 **Docker 会话运行时（`OH_CONVERSATION_RUNTIME=docker`）** 的稳定性修复上，一波由 @neubig 主导的 Docker 相关问题集中关闭并落地为 release。同时，@juanmichelini 围绕「LLM 请求中 system 消息必须先于首条 user 消息」这一仓库级不变量（invariants）批量创建了 7 个追踪类 Issue（#5144–#5150），预示着一项系统性的消息构造规范化工程正在启动。另一方面，Agent Plugins 便携插件格式（#4405）持续推进，已进入一致性测试与官方兼容客户端申报阶段。

整体判断：**项目健康度良好**——bug 修复响应快（当日报告当日关闭多个高优先级 Docker 问题），但待合并 PR 积压达 43 条，其中多条已 open 超过 1 个月，需关注审阅吞吐。

---

## 2. 版本发布

### v1.49.2（最新）
[Release v1.49.2](https://github.com/OpenHands/software-agent-sdk/releases)

**更新内容（均为 Docker agent-server 修复）：**
- `fix(agent-server): preserve legacy conversations in Docker catalogs` — [#5128](https://github.com/OpenHands/software-agent-sdk/pull/5128)（@neubig）
- `fix(agent-server): stop rescanning Docker conversations` — [#5137](https://github.com/OpenHands/software-agent-sdk/pull/5137)（@neubig）
- 另含一项 `feat(plu…)` 特性改动（release note 被截断，未能确认全貌）。

**破坏性变更：** 从已披露内容看，本版本为**补丁级（patch）修复**，无 API 破坏性变更。

**迁移注意事项：**
- 使用 `OH_CONVERSATION_RUNTIME=docker` 的自托管部署，**建议尽快升级**：v1.49.2 修复了切换 Docker 运行时后历史本地会话不可见的问题（对应 Issue [#5127](https://github.com/OpenHands/software-agent-sdk/issues/5127)），以及避免对会话目录做全量重扫描的性能退化（对应 Issue [#5136](https://github.com/OpenHands/software-agent-sdk/issues/5136)）。
- 若你的部署保留有旧版 Docker conversation catalog，升级后可自动兼容，无需手动迁移。

### v1.49.1
[Release v1.49.1](https://github.com/OpenHands/software-agent-sdk/releases)

**更新内容：**
- `fix(agent-server): preserve Docker conversation metadata route` — [#5112](https://github.com/OpenHands/software-agent-sdk/pull/5112)（@neubig）
- Release 由 @all-hands-bot 自动化发布 — [#5113](https://github.com/OpenHands/software-agent-sdk/pull/5113)

**说明：** v1.49.1 → v1.49.2 在同日连续发布，说明维护者对 Docker 元数据路由问题采取了「快速迭代、小步修复」策略。完整变更日志见 [Full Changelog](https://github.com/OpenHands/software-agent-sdk/compare)。

---

## 3. 项目进展

### 已合并 / 已关闭的重要 PR
| PR | 标题 | 意义 |
|---|---|---|
| [#4940](https://github.com/OpenHands/software-agent-sdk/pull/4940) | `feat: register deepseek-v4.1-flash as a verified model` | 将 `deepseek-v4.1-flash` 注册为 SDK 已验证模型，并推动其成为 OpenHands Cloud 默认模型（替换 `deepseek-v4-flash`）。SDK 作为验证模型的单一事实来源，此合并会让自托管部署也能开箱提供该模型。 |
| [#5128](https://github.com/OpenHands/software-agent-sdk/pull/5128) / [#5137](https://github.com/OpenHands/software-agent-sdk/pull/5137) / [#5112](https://github.com/OpenHands/software-agent-sdk/pull/5112) | Docker catalog / 元数据路由修复 | 随 v1.49.x 发布落地，解决了 Docker 运行时下会话目录兼容性与性能问题。 |

### 今日集中关闭的 Issue（Docker 运行时系列）
一天内关闭了 6 个与 Docker 运行时直接相关的问题，形成一次明显的「缺陷清剿」：

- [#5127](https://github.com/OpenHands/software-agent-sdk/issues/5127) `[priority:high, security]` 切换到 Docker 运行时后历史本地会话丢失
- [#5129](https://github.com/OpenHands/software-agent-sdk/issues/5129) `[priority:medium]` Docker 运行时拒绝新建 Canvas 会话工作区
- [#5131](https://github.com/OpenHands/software-agent-sdk/issues/5131) Docker 会话删除与重连竞态
- [#5136](https://github.com/OpenHands/software-agent-sdk/issues/5136) Docker 模式下全量 catalog 重扫描导致搜索变慢
- [#5139](https://github.com/OpenHands/software-agent-sdk/issues/5139) Docker 代理丢失根会话路径
- [#5114](https://github.com/OpenHands/software-agent-sdk/issues/5114) `GET /api/conversations/search` 在 `limit > 100` 时返回 500（查询约束笔误 + 误用 assert）

### Agent Plugins 标准化推进
- [#4453](https://github.com/OpenHands/software-agent-sdk/issues/4453) `[CLOSED, security-related]` 路径包含（path-containment）强制 + 失败边界收敛 —— **已关闭**
- [#5156](https://github.com/OpenHands/software-agent-sdk/issues/5156) `[CLOSED]` Agent Plugins 端到端测试（打通官方示例插件到配置后 agent）—— **已关闭**
- [#5159](https://github.com/OpenHands/software-agent-sdk/issues/5159) `[OPEN]` 申报 OpenHands 进入官方 Compatible Clients 页面 —— 母任务 #4405 的最后一个未勾选项

**进展评估：** 今日项目在「Docker 运行时稳定性」这一高优先级方向上前进了一大步，Docker 相关的核心阻塞性问题已基本闭环。模型生态方面新增 DeepSeek 新模型支持。Agent Plugins 从「设计」跨入「一致性验证 + 生态申报」阶段。

---

## 4. 社区热点

> 注：本次数据中 PR 的评论数字段为 `undefined`，无法按评论数排序，以下热点以 Issues 讨论量为主。

| 排名 | Issue | 评论 | 核心诉求 |
|---|---|---|---|
| 1 | [#4405](

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 · 2026-09-18

> 数据来源：github.com/earendil-works/pi | 统计窗口：2026-09-17 至 2026-09-18

---

## 一、今日速览

- **维护吞吐极高**：过去 24 小时共 101 条 Issue 更新，其中 77 条关闭、24 条新开/活跃，关闭率约 76%，Issue 分诊与收敛节奏健康。
- **PR 处理同样活跃**：11 条 PR 更新中 8 条已合并/关闭，仅 3 条待合并，积压压力小。
- **无新版本发布**，但代码层面动作密集，多个压缩（compaction）相关修复与评估基础设施 PR 被关闭/推进。
- **今日问题主线集中在压缩链路、Provider 目录漂移和 openai-codex 连接可靠性**，均为长期高热度话题的延续。
- **整体评估：项目处于高活跃、高收敛的健康状态**，但 openai-codex 可靠性问题（#4945）已开放近 4 个月，是当前最需要关注的稳定性欠账。

---

## 二、版本发布

今日无新 Release，本节略。

---

## 三、项目进展

今日合并/关闭的 PR 覆盖 TUI 稳定性、压缩正确性、扩展 API 与测试基建四条线，项目整体稳步向前。

| PR | 状态 | 推进内容 |
|---|---|---|
| [#9717](https://github.com/earendil-works/pi/pull/9717) | ✅ 已关闭 | 限制压缩摘要中「仅含 thinking」的消息体量，直接回应 #9602 的压缩溢出问题 |
| [#9692](https://github.com/earendil-works/pi/pull/9692) | ✅ 已关闭 | TUI 差分渲染遇到超宽行时改为裁剪而非抛异常，修复 #9691 的整会话崩溃 |
| [#9630](https://github.com/earendil-works/pi/pull/9630) | ✅ 已关闭 | `pi.on(...)` 支持取消订阅，并在派发时复制 handler 列表，避免迭代中增删导致的不一致 |
| [#9693](https://github.com/earendil-works/pi/pull/9693) | ✅ 已关闭 | footer cwd 测试改用 `node:path.sep`，Windows 上不再假红 |
| [#9694](https://github.com/earendil-works/pi/pull/9694) | ✅ 已关闭 | DeepSeek 模型引用更新至 `deepseek-v4-flash`，修复 `tsgo --noEmit` 失败 |
| [#9705](https://github.com/earendil-works/pi/pull/9705) / [#9706](https://github.com/earendil-works/pi/pull/9706) | ✅ 已关闭 | 评估基建：TUI context footer 评估、基于 transcript 的 eval prompt 校验 |
| [#9719](https://github.com/earendil-works/pi/pull/9719) | ✅ 已关闭 | 新增 `toolShellPaddingY` 设置，默认工具外壳垂直内边距可配置 |
| [#9714](https://github.com/earendil-works/pi/pull/9714) | 🔵 待合并 | Azure Foundry Chat Completions 部署支持（实现 #9645），可解锁 DeepSeek V4 Pro |
| [#9668](https://github.com/earendil-works/pi/pull/9668) | 🔵 待合并 | Prompt cache 预热实验性支持（WIP） |

**进展评估**：压缩正确性与 TUI 稳定性两块「硬骨头」今日均有关键修复落地；扩展 API 的取消订阅补齐了长期存在的工程细节。整体向前迈进约「一个中等修复批次」的量级，但尚未形成功能版本。

---

## 四、社区热点

### 1. [#4945](https://github.com/earendil-works/pi/issues/4945) — openai-codex 连接可靠性（79 评论 / 33 👍 / `inprogress`）
今日绝对焦点。`openai-codex` + `gpt-5.5` 反复出现 TUI 卡在 `Working...`、无流式文本、无工具调用、无报错的「静默挂起」，用户只能按 Escape 中止，留下被标记为 aborted 的助手回合。79 条评论与 33 个 👍 说明这是**跨用户、可复现、持续数日**的高频痛点，且至今未被根治（仍为 OPEN + inprogress）。

### 2. [#7836](https://github.com/earendil-works/pi/issues/7836) — Edit 模糊匹配漏掉空白长度差异（12 评论 / 已关闭）
`normalizeForFuzzyMatch` 未折叠连续空白、未剥离行首空白，导致 `oldText` 在内容等价但空白不同的情况下匹配失败。作者明确指向「小模型在 edit 上表现不佳」的根因，属于影响本地小模型可用性的关键修复。

### 3. [#8684](https://github.com/earendil-works/pi/issues/8684) — `PI_OFFLINE` 静默禁用 Provider 模型发现（10 评论 / OPEN）
文档只声明 `PI_OFFLINE` 关闭启动期网络（更新检查、遥测），实际却连带禁用了整个会话的 Provider 模型目录发现。用户诉求核心是**「文档与行为必须一致」**，属于典型的信任型问题。

### 4. [#5952](https://github.com/earendil-works/pi/issues/5952) — 扩展需要安全的会话替换 API（7 评论 / `no-action` 关闭）
请求暴露 `pi.newSession(...)` 或 `pi.requestSessionReplacement(...)`，让受信任的异步 UI 扩展能走与内置 `/new` 相同的路径。今日以 no-action 关闭，说明维护者倾向于不开放该能力。

**诉求分析**：社区焦点一半在「别卡死/别报错」的稳定性底线，一半在「扩展能用但别越权」的 API 边界。前者是产品口碑问题，后者是生态治理问题。

---

## 五、Bug 与稳定性

按严重程度排列（🔴 严重 / 🟠 高 / 🟡 中）：

### 🔴 崩溃与死锁
- **[#9036](https://github.com/earendil-works/pi/issues/9036)** — openai-codex SSE 解析器将整个响应缓冲进单个字符串，触发 V8 致命堆 OOM，进程直接终止。**暂无 fix PR。**
- **[#8331](https://github.com/earendil-works/pi/issues/8331)** — Provider 流中途停滞但连接不关闭时，`streamAssistantResponse` 的 `for await` 永久等待，agent loop 无限挂起。Anthropic 529 过载窗口期间一次冻结 4 个长会话。**暂无 fix PR。**
- **[#4945](https://github.com/earendil-works/pi/issues/4945)** — openai-codex TUI 静默卡死（见社区热点）。**标记 inprogress，长期未闭环。**

### 🟠 正确性与兼容性
- **[#9602](https://github.com/earendil-works/pi/issues/9602)** — 压缩把此前被模型请求省略的 thinking 消息重新计入，导致上下文溢出。✅ **已由 [#9717](https://github.com/earendil-works/pi/pull/9717) 修复。**
- **[#9391](https://github.com/earendil-works/pi/issues/9391)** — 手动压缩后，陈旧的签名 thinking block 每轮被重放，Anthropic 每次请求都报 `prefix_binding_mismatch` 丢弃 15 个块。**暂无 fix PR。**
- **[#9652](https://github.com/earendil-works/pi/issues/9652)** — `/compact` 在 `claude-fable-5` 上失败：`serializeConversation` 把 thinking block 转入摘要 prompt，被 Anthropic `reasoning_extraction` 分类器拦截。**暂无 fix PR。**
- **[#9579](https://github.com/earendil-works/pi/issues/9579)** — 图片溢出恢复使用固定 16 MiB 预算（源自 Anthropic 32 MiB 限制），对小请求体上限的 Provider 失效，重试仍超限。**暂无 fix PR。**
- **[#9361](https://github.com/earendil-works/pi/issues/9361)** — Windows 上加载扩展后 `shellPath` 被非确定性忽略，PATH 回退最终执行 WSL 的 `System32 bash.exe`。**暂无 fix PR。**

###

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报

**日期：2026-09-18** ｜ 数据源：github.com/BerriAI/litellm

---

## 1. 今日速览

LiteLLM 今日维持**极高活跃度**：过去 24 小时 Issues 更新 88 条、PR 更新 318 条，PR 吞吐量是 Issues 的 3.6 倍，反映出维护团队正在集中消化合并队列。但**无新版本发布**，207 个 PR 处于待合并状态（占比 65%），合并管线存在明显积压。Issue 侧仍有 64 条新开/活跃，其中 `llm translation`（模型翻译层）与 `proxy` 相关缺陷占主导，流式（streaming）场景下的 usage/计费与工具调用问题集中爆发，稳定性风险需重点关注。今日 24 条 Issue 关闭，但其中多条被标记 `stale`，说明部分关闭是自动化清理而非真正修复。

---

## 2. 版本发布

**今日无新版本发布**，无破坏性变更或迁移事项。

---

## 3. 项目进展

> ⚠️ **数据限制说明**：本日数据仅列出评论数最多的 20 条 PR，**全部为 OPEN 状态**，未包含今日实际合并/关闭的 111 条 PR 明细。以下基于已关闭 Issue（24 条）与可见 PR 主题进行推断。

### 已关闭 Issue 推进的方向

| 领域 | 关闭 Issue | 说明 |
|---|---|---|
| 计费正确性 | [#41344](https://github.com/BerriAI/litellm/issues/41344) | 修复「零成本预算绕过」漏洞——免费模型预算耗尽后经 fallback 路由到付费部署可无限制消耗 |
| 计费正确性 | [#41605](https://github.com/BerriAI/litellm/issues/41605) | 修复 Azure AI Foundry 同步请求间歇性记录 `$0` 成本 |
| Azure/Bedrock 翻译 | [#40735](https://github.com/BerriAI/litellm/issues/40735) | 修复 `bedrock_converse` 拒绝携带工具调用历史但不重新声明 `tools` 的后续轮次 |
| 模型元数据 | [#27830](https://github.com/BerriAI/litellm/issues/27830)（👍12） | 自托管 vLLM/OpenAI 兼容后端自动填充 `max_input_tokens`/`max_output_tokens` |
| RAG | [#35599](https://github.com/BerriAI/litellm/issues/35599) | `/v1/rag/query` 改用 `vector_store_registry` 解析凭据 |
| Provider 扩展 | [#41042](https://github.com/BerriAI/litellm/issues/41042) | Bourse 作为 OpenAI 兼容 provider（因重复关闭） |

### 待合并 PR 中的重点推进项

- **[#41354](https://github.com/BerriAI/litellm/pull/41354) 项目级 spend 追踪与预算执行**——当前 project-scoped key 从不写入项目 spend，导致 `/project/info` 恒为 0、项目预算永不生效。这是**预算体系的结构性缺口**。
- **[#41681](https://github.com/BerriAI/litellm/pull/41681) JWT/SSO 请求继承组织别名、预算与速率限制**——修复 org TPM/RPM 对 JWT 请求完全失效的问题。
- **[#40256](https://github.com/BerriAI/litellm/pull/40256) 后台 `/v1/responses` 重复计费**——同一次生成因客户端轮询被记录 3–5 次 spend。
- **[#36741](https://github.com/BerriAI/litellm/pull/36741) Langfuse SDK 回调迁移至 v4**——v2 SDK 已退役，`langfuse>=4` 环境下回调完全不可用。
- **[#41800 系列] 流式安全**——[#41541](https://github.com/BerriAI/litellm/pull/41541) 将提示注入启发式检查移出事件循环；[#41685](https://github.com/BerriAI/litellm/pull/41685) 修复 `llm_api_check` 审核回调被静默跳过。

**整体推进评估**：项目在**计费准确性**与**预算/权限继承**两条主线上有明显前进，但合并率仅 35%（111/318），大量修复停留在待合并状态达 1–2 周，交付节奏落后于提交节奏。

---

## 4. 社区热点

### 🔥 讨论最活跃（按评论数）

1. **[#25762](https://github.com/BerriAI/litellm/issues/25762) — 17 评论 / 👍27**（`enhancement, proxy`）
   Standard Plan 取消 SSO 5 用户上限，要求支持无限 SSO 登录账户。**点赞数全场最高**，且自 2026-04-15 持续至今 5 个月仍 OPEN，是商业化政策的直接用户反馈。

2. **[#26886](https://github.com/BerriAI/litellm/issues/26886) — 17 评论 / 👍11**（`bug, proxy`）
   Prisma 查询引擎进程周期性崩溃导致 proxy pod 不稳定。**持续时间长、影响生产可用性**，是运营类最高优先级缺陷。

3. **[#8328](https://github.com/BerriAI/litellm/issues/8328) — 16 评论 / 👍2**（`bug`）
   Key alias 在全体用户间必须全局唯一，导致不同用户无法使用相同 alias。**创建于 2025-02-06，已超 19 个月未解决**，属最资深积压项。

4. **[#26071](https://github.com/BerriAI/litellm/issues/26071) — 11 评论 / 👍16**（`enhancement, proxy`）
   支持以 SSH key / GitHub token 认证拉取私有仓库中的 Claude Skills，点赞数第二高。

### 🔥 反应最强烈

- **[#27830](https://github.com/BerriAI/litellm/issues/27830) — 👍12**（已关闭）：vLLM 模型元数据自动填充，自托管用户共鸣强烈。
- **[#25762](https://github.com/BerriAI/litellm/issues/25762) — 👍27**：SSO 用户数限制，企业采购决策受阻的直接体现。
- **[#26071](https://github.com/BerriAI/litellm/issues/26071) — 👍16**：私有仓库 Skills 集成。

**诉求分析**：高热度 Issue 集中在三类——①**商业化/授权边界**（SSO 用户数、私有仓库权限）；②**自托管场景的元数据自动化**；③**多租户隔离语义**（Key alias 唯一性）。这些均为**架构层设计选择**，而非简单 bug，因此长期悬而未决。

---

## 5. Bug 与稳定性

### 🔴 P0 — 生产可用性 / 数据正确性

| Issue | 严重度 | 状态 | 说明 |
|---|---|---|---|
| [#26886](https://github.com/BerriAI/litellm/issues/26886) Prisma 重连失败 | 🔴 高 | OPEN，无 fix PR 可见 | query engine 进程崩溃，proxy pod 周期性不稳定，17 评论持续 4.5 个月 |
| [#36168](https://github.com/BerriAI/litellm/issues/36168) 流式丢失上游

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*