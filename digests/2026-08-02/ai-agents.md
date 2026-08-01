# OpenClaw 生态日报 2026-08-02

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-01 22:36 UTC

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



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报 — 2026-08-02

## 1. 今日速览

过去 24 小时 Pi 项目保持高活跃度：Issues 更新 44 条（新开/活跃 8，关闭 36），PR 更新 26 条（待合并 7，已合并/关闭 19），无新版本发布。关闭/合并数量显著高于新增，说明维护团队正在高效消化积压问题。值得关注的是，多个长期存在的问题（如模型可用性刷新停滞 #7301、图片 URL 直传 #6151）今日均有关联修复 PR 落地或提交，项目整体处于快速迭代与稳定性加固并行的阶段。

---

## 2. 版本发布

**无新版本发布。** 当前最新版本仍为上期 Release。多个 PR 已合并，预计下一版本将包含大量稳定性修复与新功能（见下文）。

---

## 3. 项目进展

今日合并/关闭了 19 个 PR，核心进展集中在以下方面：

### 稳定性修复

- **[#7421] fix(coding-agent): recover model availability after a stalled refresh**（已合并）— 修复 #7301，解决 `forceRefreshAvailability()` 链式等待永不 settle 的 promise 导致模型可用性刷新永久不可恢复的问题，直接提升了运行时在瞬时故障后的自愈能力。
  https://github.com/earendil-works/pi/pull/7421

- **[#7441] fix(ai): tolerate missing finish_reason on non-empty openai-completions streams**（已合并）— 修复部分网关不发送终止 `finish_reason` 导致所有会话被杀死的兼容性问题，对使用非标准 OpenAI 兼容网关的用户是重要改进。
  https://github.com/earendil-works/pi/pull/7441

- **[#7463] fix(coding-agent): SessionManager._persist should not crash with ENOENT**（已合并）— 修复会话目录缺失时写入崩溃的问题，覆盖 workspace reset 等外部清理场景。
  https://github.com/earendil-works/pi/pull/7463

### 新功能与提供方支持

- **[#7422] feat(ai): support direct image URLs in ImageContent**（已合并）— 关闭 #6151。允许将图片 URL 直接透传给原生支持 URL 的 provider，避免一律 base64 编码的开销与限制。
  https://github.com/earendil-works/pi/pull/7422

- **[#7453] feat(ai): add Cline API and ClinePass providers**（已合并）— 新增 Cline（按量计费）与 ClinePass（订阅制）两个 OpenAI 兼容 provider，统一通过 `CLINE_API_KEY` 认证，扩大了对第三方网关的覆盖。
  https://github.com/earendil-works/pi/pull/7453

- **[#7456] fix(auth): support short-lived OAuth tokens**（已合并）— 修复五分钟左右有效期的 OAuth token 每次请求都刷新、无法缓存的问题，对使用短期凭据的企业 OAuth 场景有实际意义。
  https://github.com/earendil-works/pi/pull/7456

### 性能与可扩展性

- **[#7431] Make SQLite branch caching scalable**（已合并）— 用显式 `branch_tips` 表替换连接级分支簿记，使用 `INSERT ... SELECT` 事务复制前缀，避免长历史上 SQLite 变量数量限制，100k 条目规模下压缩路径查询性能显著提升。
  https://github.com/earendil-works/pi/pull/7431

- **[#7450] Use type index for SQLite compaction discovery**（已合并）— 压缩发现改为从既有类型索引驱动，只扫描匹配的压缩条目，避免全量扫描缓存路径，在 100k 条目下每次查询无需遍历完整索引。
  https://github.com/earendil-works/pi/pull/7450

### 跨平台与工程基建

- **[#7426] fix(harness): make path utilities cross-platform on Windows**（已合并）— 修复四个路径工具函数和 FileInfo 助手的 POSIX-only 假设导致 Windows 上 `loadSkills` 崩溃的问题。
  https://github.com/earendil-works/pi/pull/7426

- **[#7462] feat(coding-agent): add PI_JITI_CACHE env var**（已合并）— 允许打包者（如 nixpkgs）将 jiti 转译缓存指向持久目录，改善只读商店环境下的可用性。
  https://github.com/earendil-works/pi/pull/7462

- **[#7411] feat(coding-agent): add experimental CLI option parser**（已合并）— 为实验性组合/服务端/客户端 CLI 模式添加纯解析器，保持经典 `parseArgs()` 流程不变。
  https://github.com/earendil-works/pi/pull/7411

**整体评估：** 今日合入的 PR 质量较高，既有关键稳定性修复，也有新 provider 接入与 SQLite 后端性能优化，并且多个修复直接对应社区提交的 issue（#7301、#6151），体现了良好的社区反馈闭环。

---

## 4. 社区热点

### 讨论热度最高的 Issues

- **[#6879] auto-compaction never triggers after context grows past 100% until provider overflow** — 8 条评论，👍 6，OPEN
  用户发现一个 agentic turn 运行超过 2 小时后，上下文比例超过 100% 仍未触发压缩，直到 API 在 373k token 处拒绝请求才被迫压缩。社区共鸣度高（6 个 👍），反映出长时运行任务下的上下文管理是真实痛点。用户建议在每个 agent 步骤后检查上下文水位。
  https://github.com/earendil-works/pi/issues/6879

- **[#7161] anthropic-messages never sends x-client-request-id, unlike all OpenAI paths** — 8 条评论，OPEN
  用户 @mteam88 的代理在多个 Claude 账号间轮询，依赖 `x-client-request-id` 做会话亲和性分组，但 `anthropic-messages` 路径不发送该 header，导致多账号轮询时会话无法正确路由。该 issue 已有对应的贡献提案 #7438。
  https://github.com/earendil-works/pi/issues/7161

- **[#5931] Copy-paste from TUI introduces extra spaces and line breaks** — 7 条评论，CLOSED（no-action）
  从 Pi TUI 复制文本到编辑器时，在换行点引入多余空格和换行。7 条评论说明该问题影响了不少用户。
  https://github.com/earendil-works/pi/issues/5931

- **[#7010] Normalize optional object tool schemas for OpenAI-compatible providers** — 6 条评论，OPEN
  用户 @hsm-lv 指出 `pi-ai` 在转发工具 JSON Schema 时未规范化 `required` 字段，可能影响部分 OpenAI 兼容 provider 的工具调用解析。
  https://github.com/earendil-works/pi/issues/7010

**诉求分析：** 高热度问题集中在三方面——长会话上下文管理（#6879）、多账号/网关下的会话亲和性（#7161、#7010）、TUI 体验细节（#5931、#6662、#7385）。其中上下文管理和 TUI 渲染性能在近期多个 issue 中反复出现，说明长会话场景是当前用户群体的核心使用方式。

---

## 5. Bug 与稳定性

按严重程度排列（✅ = 已有修复 PR / 已合并 PR 修复）：

### 高严重度

- **[#6879] auto-compaction 在上下文超 100% 后不触发，直到 provider 溢出报错** — OPEN，👍 6
  一个 agentic turn 运行超 2 小时，上下文超过 100% 仍未压缩，最终 API 在 373k token 处拒绝。这会导致长任务中断、token 消耗不可控。尚无直接修复 PR。
  https://github.com/earendil-works/pi/issues/6879

- **[#7301] 模型可用性刷新停滞且永久不可恢复** — CLOSED ✅
  `forceRefreshAvailability()` 链到已卡死的 promise 上，后续所有 `getAvailable()`/`refresh()` 都永远不 settle。**已由 PR #7421 修复并合并。**
  https://github.com/earendil-works/pi/issues/7301

- **[#7385] 键盘输入延迟随对话长度线性增长（~160 个工具调用时 350-520ms/字符）** — CLOSED
  `tool-result-renderer` 绕过了 Text 组件的渲染缓存，每次按键都重新处理全部工具结果内容。CPU profile 显示 `wrapTextWithAnsi`/`visibleWidth` 等函数是热点。
  https://github.com/earendil-works/pi/issues/7385

- **[#7402] 粘贴孟加拉语后按空格导致行视觉重复，differential renderer 与终端光标失步** — CLOSED
  宽度计算（overcounting）导致差异渲染器不同步，每次按键光标行都视觉重复。
  https://github.com/earendil-works/pi/issues/7402

### 中严重度

- **[#7315] Fireworks 请求偶尔瞬时失败 "Request timed out."** — OPEN
  failed turns 内容为空、token 用量为零，像是握手/连接阶段就超时。**有 PR #7435（增加连接尝试超时到 2s）待合并，可能解决该问题。**
  https://github.com/earendil-works/pi/issues/7315

- **[#6600] pi update --extensions 因 npm 11.16.0 默认阻止安装脚本而失效** — OPEN
  npm 11.16.0 默认阻止 install scripts，导致 pi 的扩展更新流程无法正常安装依赖，且报错不透明。这是上游工具变更带来的兼容性问题。
  https://github.com/earendil-works/pi/issues/6600

- **[#7446] RpcClient 硬编码 30s 超时导致长命令（如 compact）误报失败** — CLOSED
  所有 RPC 命令统一使用 30s 超时，压缩等长耗时操作可能超时，需要按需配置超时时间。
  https://github.com/earendil-works/pi/issues/7446

- **[#7443] `/model <name>` 在 pi.dev 目录不可达时永久挂起** — CLOSED ✅
  网络静默丢包时 `/model` 命令无响应。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报（2026-08-02）

## 1. 今日速览

过去 24 小时内，Temporal 核心仓库保持中等偏高的开发活跃度：共更新 15 条 PR（8 条开放中，7 条已合并/关闭），关闭 1 条长期遗留 Issue，无新版本发布。项目已进入 **1.32.0 发布分支准备阶段**（[#11392](https://github.com/temporalio/temporal/pull/11392)），同时围绕 standalone activity（CHASM 独立活动）的 GA 化有一批关键 PR 正在密集推进。值得注意的是，今日关闭的 [#7821](https://github.com/temporalio/temporal/issues/7821) 是创建于一年前的历史遗留问题，说明维护者正在清理积压事项。整体来看，工程化收尾（CI 修复、测试回退）与功能补强（S3 可见性、worker API 分类）并行，项目健康度良好。

## 2. 版本发布

过去 24 小时无新版本发布。

**前瞻信号**：[#11392 "1.32.0: Prepare release branch"](https://github.com/temporalio/temporal/pull/11392)（@temporal-cicd[bot]，已关闭）已完成发布分支准备，包括覆盖 governance 文件与更新依赖。这标志着 **1.32.0 版本已进入发布冲刺阶段**，预计正式版本将在近期发布，建议下游用户关注随后的 release notes 以评估升级影响。

## 3. 项目进展

今日关闭的 7 条 PR 中，以下推进了实际功能或工程收尾：

- **1.32.0 发布分支准备**（[#11392](https://github.com/temporalio/temporal/pull/11392)，已关闭）：版本周期正式启动。
- **默认启用 standalone activity start delay**（[#11378](https://github.com/temporalio/temporal/pull/11378)，@fretz12，已关闭）：移除测试临时覆盖，将 start delay 作为独立活动默认行为开启。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*