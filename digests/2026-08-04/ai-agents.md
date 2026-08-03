# OpenClaw 生态日报 2026-08-04

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-03 23:31 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-04

## 1. 今日速览

过去24小时项目活跃度极高：**500 条 Issue 更新**（新开/活跃 465

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报 — 2026-08-04

## 1. 今日速览

过去 24 小时项目活跃度处于高位：共 50 条 Issue 更新（新开/活跃 45 条，关闭 5 条），50 条 PR 更新（待合并 42 条，合并/关闭 8 条）。无新版本发布。Issue 侧讨论热度集中在 ACP 配置注入、LLM 兼容性、安全风险自评信任三个方向，多条高赞问题持续发酵；PR 侧保持稳定的合并节奏，涵盖可观测性（Weave 集成）、安全加固（webhook 内存上限、VSCode 路径校验）与稳定性改进（LLM 流式降级、Git 日志降噪）。整体健康度良好，但安全类报告占比偏高，需重点关注。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日合并/关闭的 PR 揭示了项目在可观测性、稳定性与安全性上的稳步推进：

- **可观测性增强**：[PR #1446](https://github.com/OpenHands/software-agent-sdk/pull/1446) 合并，新增 Weights & Biases Weave 集成，为 SDK 可观测性模块提供全面的 agent 操作追踪能力。这是从 OpenHands 主仓库的移植适配，补全了 SDK 侧追踪缺口。
- **安全加固**：[PR #4323](https://github.com/OpenHands/software-agent-sdk/pull/4323) 合并，限制 agent-server webhook 投递的内存使用，防止并发事件发布时无限增长。
- **稳定性改进**：[PR #4020](https://github.com/OpenHands/software-agent-sdk/pull/4020) 合并，`stream=True` 但未绑定 `on_token` 回调时优雅降级而非硬抛异常；[PR #4341](https://github.com/OpenHands/software-agent-sdk/pull/4341) 合并，将 Git 回退探测的预期失败从 error 级降为 debug，减轻 Datadog 日志噪音。
- **追踪完善**：[PR #4054](https://github.com/OpenHands/software-agent-sdk/pull/4054) 合并，在可观测性 trace 中实时回填 git 仓库身份信息，并验证了元数据更新可落盘至 Laminar root span。
- **流程清理**：[PR #4337](https://github.com/OpenHands/software-agent-sdk/pull/4337) 合并，删除不再需要的 assign-reviews.yml 工作流，迁移至自动化。

另有 6 条 PR 保持打开待合并状态（见第 8 部分），其中 [PR #4282](https://github.com/OpenHands/software-agent-sdk/pull/4282)（VSCode URL 端点工作区目录未验证）属安全修复，建议优先推进。

## 4. 社区热点

今日讨论最活跃的 Issue 集中反映三类诉求：

- **配置注入与重复加载**：[#4019](https://github.com/OpenHands/software-agent-sdk/issues/4019)（16 评论）讨论 ACP profiles 注入的 workspace 项目技能与 ACP CLI 已摄入的 AGENTS.md 重复。源于 #4018 将 `load_project_skills` 默认开启，社区关注重复加载的潜在冲突与冗余。
- **弱模型/本地模型兼容性**：[#4248](https://github.com/OpenHands/software-agent-sdk/issues/4248)（14 评论）报告 DeepSeek-reasoner 调用 `execute_bash` 时缺少必填参数 `security_risk`；[#3992](https://github.com/OpenHands/software-agent-sdk/issues/3992)（13 评论）指出 `ResponseDispatchMixin` 对「有内容无工具调用」响应的不对称处理会终止弱模型驱动的 agent。两者共同指向同一深层问题：**SDK 对非 GPT 级模型的容错不足**。
- **并发限制失效**：[#4063](https://github.com/OpenHands/software-agent-sdk/issues/4063)（13 评论）指出 `max_concurrent_runs` 仅限制同步回退路径，`EventService.run()` 原生异步会话不受控，可能导致资源超卖。这是配置语义与实现不一致的典型问题。

PR 侧热点：[#4332](https://github.com/OpenHands/software-agent-sdk/pull/4332)（GLM 模型重复错误卡死检测）、[#4342](https://github.com/OpenHands/software-agent-sdk/pull/4342)（浏览器工具启动失败不应导致对话失败）与社区反馈的本地模型体验问题直接相关，建议关注其合并进展。

## 5. Bug 与稳定性

按严重程度降序排列，重点标注是否有 fix PR：

| 严重程度 | Issue/PR | 问题描述 | 状态 |
|---|---|---|---|
| **高（安全）** | [#4271](https://github.com/OpenHands/software-agent-sdk/issues/4271) | GitHub 凭据在 git remote URL 中未脱敏，终端输出泄露 | 无 fix PR |
| **高（安全）** | [#4157](https://github.com/OpenHands/software-agent-sdk/issues/4157) | LLMSecurityAnalyzer 信任模型自评的 `security_risk`，LOW 风险动作自动执行绕过人工确认 | 无 fix PR |
| **高（安全）** | [#4263](https://github.com/OpenHands/software-agent-sdk/issues/4263) | `get_litellm_model_info` 在 LLM 初始化时发起未经验证的 `httpx.get` 调用，存在 egress 风险 | 无 fix PR |
| **高（安全）** | [PR #4282](https://github.com/OpenHands/software-agent-sdk/pull/4282) | VSCode URL 端点 `workspace_dir` 参数未验证，中等严重度 | 待合并 |
| **中（功能）** | [#4245](https://github.com/OpenHands/software-agent-sdk/issues/4245) | agent-server webhook 连接失败导致容器崩溃及 sandbox 连接错误 | 关联 PR #4323 已合并（内存上限） |
| **中（功能）** | [#4248](https://github.com/OpenHands/software-agent-sdk/issues/4248) | DeepSeek-reasoner 调用 `execute_bash` 缺少必填参数 `security_risk` | 无 fix PR |
| **中（功能）** | [#4063](https://github.com/OpenHands/software-agent-sdk/issues/4063) | `max_concurrent_runs` 不限制原生异步会话 | 无 fix PR |
| **中（功能）** | [#4158](https://github.com/OpenHands/software-agent-sdk/issues/4158) | ACP 会话 `switch_profile` 半应用：状态文件已更新但 live 会话仍用旧 agent | 无 fix PR |
| **中（功能）** | [#4256](https://github.com/OpenHands/software-agent-sdk/issues/4256) | agent-server Docker 镜像中 browser-use 启动 Chromium 缺 `--no-sandbox`，导致超时 | 相关 PR #4342 已提交 |
| **中（功能）** | [#4080](https://github.com/OpenHands/software-agent-sdk/issues/4080) | 单个事件反序列化失败导致整个会话加载失败且静默丢弃 | 无 fix PR |
| **低（体验）** | [#4255](https://github.com/OpenHands/software-agent-sdk/issues/4255) | Ollama 任务超过 300 秒被强制终止，UI/settings.json 超时配置无效 | 无 fix PR |
| **低（兼容）** | [#4093](https://github.com/OpenHands/software-agent-sdk/issues/4093) | ACP 0.11 移除 `NewSessionResponse.models` 字段，破坏 Gemini CLI 模型状态同步 | 无 fix PR |
| **低（兼容）** | [#4098](https://github.com/OpenHands/software-agent-sdk/issues/4098) | 无 API key 时仍对 `openhands/*` 模型发起未认证 model-info 查询 | 无 fix PR |

## 6. 功能请求与路线图信号

- **[#3903](https://github.com/OpenHands/software-agent-sdk/issues/3903) — 大命令输出按需加载**（7 评论）：单条命令输出超 20k tokens 全部注入上下文，请求支持按需加载更多输出。该需求直指 token 成本与上下文窗口压力，落地概率高。
- **[#3884](https://github.com/OpenHands/software-agent-sdk/issues/3884) — 可观看的浏览器会话录制**（6 评论）：借鉴 e2e harness 技术，为浏览器会话提供录制回放能力，便于调试与审查。
- **[PR #3673](https://github.com/OpenHands/software-agent-sdk/pull/3673) — `ask_oracle` 工具**：允许 agent 在遇到困难时向更强的 LLM 寻求第二意见，已有人工测试记录，处于待合并状态。
- **[PR #4311](https://github.com/OpenHands/software-agent-sdk/pull/4311) — 自动化完成回调中报告累计 LLM 成本**：面向成本可观测性的功能增量，与 #3903 的 token 关注点一脉相承。
- **[PR #2694](https://github.com/OpenHands/software-agent-sdk/pull/2694) — 服务级 MCP 服务器管理**：支持 MCP 服务器注册一次、按 ID 跨会话引用，属架构级能力增强。
- **[#2725](https://github.com/OpenHands/software-agent-sdk/issues/2725) — SDK vs Agent Server 兼容性差距收敛**：官方已发布兼容性矩阵，属路线图级任务，将持续牵引后续版本迭代方向。

## 7. 用户反馈摘要

- **本地模型/弱模型支持不足是最大痛点**：#3992 明确描述了「内容无工具调用」响应导致 agent 直接终止的现象；#4247（LM Studio 未提供 LLM Provider）、#4250（Workers AI 上下文窗口过小被拒）均反映第三方模型接入门槛偏高。用户期待 SDK 对非主流模型有更好的容错与降级策略。
- **安全机制存在信任盲区**：#4157 的评论显示社区对「LLM 自评风险等级」的安全模型不信任，「自动执行任何 LOW 风险动作」被质疑为安全漏洞而非特性。#4271 的凭据泄露报告进一步加剧了安全顾虑。
- **配置复杂度影响上手体验**：#4247、#4255、#4267（ACP 本地配置无响应）共同指向配置链路不透明、错误提示不明确的问题。用户在评论区反馈「照文档操作仍失败」「超时配置不生效」等挫败感。
- **沙箱环境体验待优化**：#4253（Web 浏览器不可用）、#4257（无法创建预览链接/打开浏览器标签）说明沙箱内浏览器能力缺失是 Web 开发场景的关键瓶颈，直接影响「用 OpenHands 开发并验证 Web 应用」的核心工作流。

## 8. 待处理积压

以下重要问题或 PR 长期未获得解决/合并，建议维护者关注：

| 时间线 | Issue/PR | 说明 | 优先级建议 |
|---|---|---|---|
| 2026-01-28 创建（超 6 个月） | [#4245](https://github.com/OpenHands/software-agent-sdk/issues/4245) | agent-server webhook 失败致容器崩溃，长期未获得根本修复（#4323 仅缓解内存维度） | 高 |
| 2026-04-06 创建（4 个月） | [#2725](https://github.com/OpenHands/software-agent-sdk/issues/2725) | SDK vs Agent Server 兼容性矩阵已发布但差距收敛无时间表 | 中 |
| 2026-04-03 打开（4 个月） | [PR

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

## Pi 项目日报 2026-08-04

### 1. 今日速览
过去 24 小时项目活跃度极高：**Issues 更新 136 条**（其中 112 条已关闭），**PR 更新 45 条**（39 条已合并/关闭），显示出核心维护者与社区的高频协作。开发重点集中在 **Windows/WSL 兼容性修复**、**上下文压缩（Compaction）逻辑重构** 以及 **Harness v2 会话架构推进** 上。合并 PR 中包含了针对“JSON 流式输出二次复杂度”和“手动/自动压缩竞态”的关键修复，整体项目健康度良好，但 WSL/Windows 相关历史 Bug 仍是最大的用户痛点。今日 **无新版本发布**。

---

### 3. 项目进展（合并/关闭 PR 分析）
今日合并的 PR 在多个维度上显著提升了 Pi 的稳定性与架构先进性：

- **上下文压缩 (Compaction) 修复**：
  - [#7370](https://github.com/earendil-works/pi/pull/7370) 修复了手动 `/compact` 与自动压缩触发的竞态条件（对应 Issue #7253）。
  - [#7540](https://github.com/earendil-works/pi/pull/7540) 允许在因“上下文长度限制”中断后自动恢复，并在压缩后清理可重试错误。
- **流式输出与性能**：
  - [#7394](https://github.com/earendil-works/pi/pull/7394) 与 [#7561](https://github.com/earendil-works/pi/pull/7561) 将 JSON/RPC 模式下的 `message_update` 改为仅增量传输，消除累积状态序列化导致的二次方输出问题（对应 Issue #7395）。
- **Harness v2 架构落地**：
  - [#7503](https://github.com/earendil-works/pi/pull/7503) 和 [#7396](https://github.com/earendil-works/pi/pull/7396) 进一步推进了 Harness v2 的会话基础层，新增了 `InMemorySessionStorage` 与持久化 Server 后端。
- **平台兼容性（Windows/WSL）**：
  - [#7569](https://github.com/earendil-works/pi/pull/7569) 重构了 `find` 工具的路径规范化逻辑，修复了 Windows 根目录路径损坏问题。
  - [#7552](https://github.com/earendil-works/pi/pull/7552) 修复了使用符号链接目录存储的会话在发现时被静默忽略的问题。
- **新增基础设施与 Provider**：
  - [#7571](https://github.com/earendil-works/pi/pull/7571) 新增欧洲 Provider **Cortecs** 的官方支持。
  - [#7568](https://github.com/earendil-works/pi/pull/7568) 支持在 `models.json` 中配置通用采样参数（如 `dry_multiplier`、`xtc_probability`），利好 llama.cpp/vLLM 用户。
  - [#7562](https://github.com/earendil-works/pi/pull/7562) 为 Anthropic 增加了可选的服务端故障转移支持。

---

### 4. 社区热点
热门讨论聚焦于 **WSL 体验缺陷** 与 **企业级功能不可用**：

- **#6187 WSL 中 Copilot 登录挂起**（20 条评论）：在浏览器中完成设备授权后，Pi 客户端无法检测授权状态导致永久挂起。这是 WSL 用户遭遇的最大障碍，已持续超一个月。
- **#6768 企业版 Copilot 无法使用压缩（Compaction）**（17 条评论，👍 18）：使用 Copilot Enterprise 许可证时，OpenAI 返回 `421 Misdirected Request`，Anthropic 模型同样失败。该 Issue 获得高赞，说明企业用户群对核心功能的稳定性高度敏感。
- **#6879 自动压缩在超限后不触发**（10 条评论，👍 13）：有用户会话运行超过 2 小时，上下文超过 100% 直到 API 拒绝请求（373k tokens）才触发压缩。社区呼吁每次 agent 轮次后都应检查上下文阈值。
- **#7064 WSL 绝对路径处理异常**（11 条评论）：`read`/`write`/`edit` 工具在 WSL 中频繁因路径处理失败，导致 Agent 退化使用命令行进行整文件重写。
- 此外，[#7547](https://github.com/earendil-works/pi/issues/7547)（“如何在 Windows 上使用 Pi”）虽为今日新建（5 条评论），但作为维护者（@petrroll）发起的收集帖，明确指向开发资源将向 Windows 方向倾斜。

---

### 5. Bug 与稳定性
按严重程度排列今日活跃的关键问题：

- **严重 - 认证/登录阻断**：
  - [#6187](https://github.com/earendil-works/pi/issues/6187) WSL 内 GitHub Copilot 设备授权后客户端无响应。
  - [#7027](https://github.com/earendil-works/pi/issues/7027)（API-key 登录在模型目录刷新停滞时可能挂起）与 [#7113](https://github.com/earendil-works/pi/issues/7113)（TUI 在 `/login` 时冻结）**已有对应修复 PR [#7451](https://github.com/earendil-works/pi/pull/7451)**（为模型目录刷新添加了时限与取消机制），今日已合并。
- **高 - 上下文压缩中断**：
  - [#6879](https://github.com/earendil-works/pi/issues/6879) 自动压缩失效直到 Provider 溢出；需在每次 agent 轮次后主动检查。暂无直接修复 PR。
  - [#7413](https://github.com/earendil-works/pi/issues/7413) 企业 GHE.com 账户执行 `/compact` 报 `unknown stamp "prod-cus-01"` 错误，普通会话正常。
- **中 - Windows 特有工具缺陷**：
  - [#6817](https://github.com/earendil-works/pi/issues/6817) `find` 工具在 Windows 无法匹配包含分隔符的通配符路径（如 `src/**/*.spec.ts`）。
  - [#6596](https://github.com/earendil-works/pi/issues/6596) Node.js 24 环境下 `spawn("taskkill")` 抛出 `ENOENT`（需使用 System32 绝对路径）。
- **中 - 渲染与输入**：
  - [#7130](https://github.com/earendil-works/pi/issues/7130) Kitty 终端退格键删除 2 个字符（Release 事件未过滤）。
  - [#7399](https://github.com/earendil-works/pi/issues/7399) `truncateToWidth()` 在截断时破坏 OSC 8 超链接平衡，导致终端出现悬空链接。
- **已修复**：[#7539](https://github.com/earendil-works/pi/pull/7539) 修复了认证头删除标记丢失（#7030）问题；[#7550](https://github.com/earendil-works/pi/pull/7550) 修复了终端批量颜色方案报告解析错误（#7538）。

---

### 6. 功能请求与路线图信号
- **配置压缩时的思考级别**：[#7553](https://github.com/earendil-works/pi/issues/7553)（3 条评论）请求允许手动/自动压缩使用独立的 thinking level，避免高推理模型在压缩时消耗过多 token。
- **通用采样参数**：[#7568](https://github.com/earendil-works/pi/pull/7568)（已合并）通过 `models.json` 透传引擎特定参数，符合本地推理（llama.cpp/vLLM）用户的深度定制诉求，预计将随下一版本发布。
- **运行时切换 UI 模式**：[#7555](https://github.com/earendil-works/pi/pull/7555) 已合并，允许在运行时切换 UI 模式，但维护者表示仍在探索更优方案。
- **OpenAI 后台模式（Background Mode）**：[#7339](https://github.com/earendil-works/pi/pull/7339)（Draft）开始实现并在等待设计评审。
- **更完善的 TUI 渲染**：[#7541](https://github.com/earendil-works/pi/issues/7541) 用户提交了“保留渲染（retained-rendering）”方案以减少长会话/图像会话中的输入延迟，虽标记为 no-action 但为 TUI 优化提供了用户侧参考实现。
- **Harness v2 持续演进**：`SessionStorage` 与 `SessionRepo` API 的引入，以及 Server 端会话持久化，预示着 Pi 正朝着更稳健的多端同步架构迈进。

---

### 7. 用户反馈摘要
- **满意的部分**：维护者对 Issue 的响应速度较快（今日关闭 112 条），用户提出的高质量 PR（如 #7541、#7554）得到了维护者的积极回应。
- **核心痛点 - WSL/Windows 体验割裂**：用户反馈 Pi 在 WSL 下处理路径时，经常无法使用原生 `read`/`write` 工具，被迫退化为“全量写入”或调用命令行工具，这实际降低了 Agent 的效率与安全性（[#7064](https://github.com/earendil-works/pi/issues/7064)）。
- **核心痛点 - 压缩与长会话**：多位用户（[#6879](https://github.com/earendil-works/pi/issues/6879)、[#7020](https://github.com/earendil-works/pi/issues/7020)）在使用“协调者”型长会话时频繁遭遇压缩失败、卡顿或不触发的问题，严重影响工作流连续性。
- **特定环境困扰**：`find` 工具的路径处理在 Windows 上（#6104、#6817）以及符号链接目录的会话发现（#7497）问题，导致部分资产无人发现与工具不可用。此外，Bengali 等宽字符粘贴导致的渲染错乱（#7402）反映了本地化处理仍需加强。

---

### 8. 待处理积压
- **[#6187](https://github.com/earendil-works/pi/issues/6187)（严重）**：WSL 登录挂起问题仍未解决，已开放超 35 天，20 条评论无明确修复 PR。建议维护者优先调查 WSL 环境下的授权回调检测机制

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-04

## 1. 今日速览

LiteLLM 在过去 24 小时保持极高活跃度：**69 条 Issue 更新**（新开/活跃 57、已关闭 12）与 **206 条 PR 更新**（待合并 146、已合并/关闭 60）双向并行，另有 **4 个新版本发布**（含 1 个 RC 和 3 个稳定版）。当前开发重心清晰：一方面深入推进 **Rust 扩展落地**（Rust-backed pip binary 相关 CI 与工具链工作），另一方面由 @yucheng-berri 主导的 **OTEL 租户级可观测性大特性**（6 个关联 PR 同时在飞）正在形成完整闭环——从凭证管理、身份解析、追踪分发到 UI 管理面全部覆盖。Issue 侧社区反馈集中在 Claude 空内容消息、GPT-5.6 家族工具调用、镜像发布完整性等问题，维护者响应速度整体良好，项目处于功能扩张与质量加固并进的高活跃状态。

---

## 2. 版本发布

过去 24 小时发布 **4 个版本**，Release notes 均为同一模板（Docker 镜像 cosign 签名验证指引）：

| 版本 | 类型 | 说明 |
|------|------|------|
| [v1.96.0-rc.1](https://github.com/BerriAI/litellm/releases/tag/v1.96.0-rc.1) | 预发布 RC | 下一功能版本的候选 |
| [v1.95.0](https://github.com/BerriAI/litellm/releases/tag/v1.95.0) | 稳定版 | 最新稳定功能版 |
| [v1.94.1](https://github.com/BerriAI/litellm/releases/tag/v1.94.1) | 补丁版 | 修复版 |
| [v1.93.1](https://github.com/BerriAI/litellm/releases/tag/v1.93.1) | 补丁版 | 修复版 |

**值得注意的异常**：社区用户报告 v1.94.1 和 v1.95.0 的 GHCR 镜像已发布且 cosign 签名有效，但仓库中**没有对应的 git tag 和 GitHub Release**（见 [Issue #35683](https://github.com/BerriAI/litellm/issues/35683) 和 [#35684](https://github.com/BerriAI/litellm/issues/35684)）。这直接违反了 Release 说明中的"镜像 tag 与 git tag 一一对应"的验证指引，属于发布流程一致性缺口，已由用户标记为 potential-duplicate 并被维护者关注。

**迁移注意事项**：由于 Release notes 为模板内容，无法从本次数据中获取具体变更日志。建议升级用户关注 [CHANGELOG](https://github.com/BerriAI/litellm/blob/main/CHANGELOG.md) 或对比 v1.93.x → v1.96.0-rc.1 之间合并的 60 条 PR 以评估影响面。

---

## 3. 项目进展

过去 24 小时 **60 条 PR 被合并或关闭**，其中已展示的合并/关闭条目包含 2 条，但整体合并量表明项目快速迭代中。以下按主题归纳值得关注的方向：

### 🚀 OTEL 租户级可观测性（大特性进行中，6 个 PR）
这是一个正在快速推进的完整功能系列，目标是在多租户场景下实现按团队/组织隔离的可观测性：

- [#30873 feat(otel/v2)!: admin-owned, identity-scoped trace destinations](https://github.com/BerriAI/litellm/pull/30873) — 主 PR，管理员可注册 trace 目的地并按身份（团队/组织）路由
- [#35513 feat(credentials): admin-owned logging credential, access shape, and destination mapping](https://github.com/BerriAI/litellm/pull/35513)
- [#35514 feat(otel): resolve a request's trace destinations from its identity](https://github.com/BerriAI/litellm/pull/35514)
- [#35515 feat(otel): export the trace to the resolved destinations](https://github.com/BerriAI/litellm/pull/35515)
- [#35516 feat(proxy): disclose resolved destinations on team and organization info](https://github.com/BerriAI/litellm/pull/35516)
- [#35517 feat(ui): manage admin-owned logging destinations](https://github.com/BerriAI/litellm/pull/35517)

该系列解决的核心痛点是：此前 OTEL traces 只能发送到一个代理级全局目的地，租户 A 的 traces 可能被租户 B 在共享观测工具中看到。合并后将支持精细化的 trace 路由、管理面 UI 配置、且客户端无法影响 trace 去向（安全增强）。

### 🛠️ 重要修复
- [#35716 fix(bedrock/realtime): nova sonic tool calling via content field](https://github.com/BerriAI/litellm/pull/35716) — 修复 Nova Sonic 工具参数在 content 而非 input 导致的工具调用丢失问题
- [#35636 fix(vertex_ai): keep all embeddings in multimodal embedding response](https://github.com/BerriAI/litellm/pull/35636) — 修复多模态 embedding 响应中 elif 链只保留第一个 embedding 导致图片+文本 embedding 静默丢失的问题
- [#35687 fix(datadog): read team callback dd_* params from kwargs instead of blocked dynamic params](https://github.com/BerriAI/litellm/pull/35687) — 已合并，OSS 修复端口迁移

### 🧪 工程效率
- [#35697 test(ui): tier the MCP create tests into unit and integration](https://github.com/BerriAI/litellm/pull/35697) — 将 77 个 MCP 创建测试拆分为 61 个单元测试（9ms）+ 精简集成测试，UI CI 耗时显著下降
- [#35694 refactor(ui): extract the MCP create form's logic and field groups](https://github.com/BerriAI/litellm/pull/35694) — 已合并，1389 行巨型组件拆分为纯类型模块
- [#35519 ci(circleci): install a pinned Rust toolchain on the Linux jobs](https://github.com/BerriAI/litellm/pull/35519) — 修复 CI 中 Rust 工具链漂移问题

---

## 4. 社区热点

### 🔥 讨论热度最高（按评论数）

**1. [#24498 Claude 模型返回空内容消息占位符（9 条评论）](https://github.com/BerriAI/litellm/issues/24498)**
自 3 月提交以来持续活跃，用户在 Claude 模型使用中遇到 `[System: Empty message content sanitised to satisfy protocol]` 作为响应返回的情况。评论数最多说明该问题波及面广，涉及 Anthropic 协议的空消息处理机制。

**2. [#31261 LiteLLM Rust pip 二进制安装问题（7 条评论，👍 4）](https://github.com/BerriAI/litellm/issues/31261)**
官方发起的中心化 issue，用于收集即将推出的 Rust-backed pip binary 安装问题。👍 数最高，社区对 Rust 化方向关注度极高。该 issue 关联到当前 CI 中 Rust 工具链固定工作（[PR #35519](https://github.com/BerriAI/litellm/pull/35519)），表明 Rust 化正处于落地前夜。

**3. [#33221 GPT-5.6 家族函数工具 + reasoning_effort 报错（6 条评论，👍 1）](https://github.com/BerriAI/litellm/issues/33221)**
7 月中旬提交，涉及 gpt-5.6-sol/luna/terra 三个新模型的工具调用与 reasoning_effort 参数冲突，反映了新模型发布后 LiteLLM 适配的滞后性。

### 🌟 值得关注的反馈模式
- 多个用户在镜像发布完整性（[#35683](https://github.com/BerriAI/litellm/issues/35683)、[#35684](https://github.com/BerriAI/litellm/issues/35684)）上与官方发布流程"较真"，说明企业用户对供应链安全极为重视
- OTEL 系列 PR 虽然没有公开评论，但作为跨 5+ PR 的大型特性，其被合并后将大幅提升 LiteLLM 在企业级多租户场景的竞争力

---

## 5. Bug 与稳定性

按严重程度排列：

### 🔴 高严重度

**1. [Issue #35683/#35684: GHCR 镜像版本与 git tag 不匹配](https://github.com/BerriAI/litellm/issues/35683)**
v1.94.1 和 v1.95.0 镜像已发布且签名有效，但没有对应 git tag 和 Release。影响用户验证镜像完整性（cosign 验证需要对应 tag），且反映发布流程存在自动化缺口。**已有关注，无明确 fix PR**。

**2. [Issue #35632: /cursor/chat/completions 流式请求全部 500](https://github.com/BerriAI/litellm/issues/35632)**
`cursor_data_generator()` 收到意外的 `request` 关键字参数，导致 Cursor 客户端（始终 stream: true）完全无法使用该端点。功能级不可用。

**3. [Issue #35657: 预算超限后用户级虚拟密钥 UI 全面故障](https://github.com/BerriAI/litellm/issues/35657)**
用户级 key 超过预算后，Usage 部分无法显示、key 列表加载失败，而 Admin 密钥正常工作——说明权限/预算状态在 UI 数据层存在交叉影响。

### 🟡 中严重度

**4. [Issue #35699: Debug 日志急切构建导致性能损耗](https://github.com/BerriAI/litellm/issues/35699)**
审计发现 291 个文件中的 1347 处 debug 日志调用使用 f-string 急切插值，禁用 debug 时仍产生格式化开销。性能敏感的代理场景下这是可量化的浪费。**已有改进方向（延迟求值）**。

**5. [Issue #35645: DeepSeek Anthropic 路由错误映射 budget_tokens](https://github.com/BerriAI/litellm/issues/35645)**
`output_config.effort` 和 adaptive thinking 被映射为 DeepSeek 不支持的 `budget_tokens`，导致 deepseek-v4-flash 在 `/v1/messages` 下行为异常。

**6. [Issue #35655: Bedrock 上 GLM-5 和 DeepSeek V3.2 结构化输出失败](https://github.com/BerriAI/litellm/issues/35655)**
走了 dummy tool call 路径，但 Bedrock 模型卡显示原生支持结构化输出，说明转换逻辑未按模型能力分支。

### 🟢 低严重度 / 边界问题

**7. [Issue #35680: 移除 max_budget 配置不生效](https://github.com/BerriAI/litellm/issues/35680)** — 删除 config.yaml 中 `litellm_settings.max_budget` 后，default_user_id 行仍残留旧值，属于状态清理遗漏。
**8. [Issue #34692: ollama_chat→Anthropic 流式工具调用 stop_reason 错乱](https://github.com/BerriAI/litellm/issues/34692)** — 流式中工具调用表现为 `end_turn` + 空文本块，影响 Claude Code 类工具链的流式解析。

---

## 6. 功能请求与路线图信号

### 📌 可能被纳入下一版本（已有对应 PR）

| 功能请求 | 对应 PR | 状态 |
|---------|---------|------|
| [OTEL 多租户 trace 隔离（Issue #30873 系列）](https://github.com/BerriAI/litellm/pull/30873) | 6 个关联 PR | 进行中，核心部分已接近可合并 |
| [数据飞（DataFog）PII 护栏提供方](https://github.com/BerriAI/litellm/pull/31991) | [PR #31991](https://github.com/BerriAI/litellm/pull/31991) | 待合并，覆盖 pre/during/post-call、流式、工具调用等多个阶段 |
| [Auto-router 模板选择器](https://github.com/BerriAI/litellm/pull/35199) | [PR #35199](https://github.com/BerriAI/litellm/pull/35199) | 待合并，内置 Anthropic/OpenAI 复杂度路由预设 |
| [成本优化面板增加 net auto-router 节省统计](https://github.com/BerriAI/litellm/pull/35521) | [PR #35521](https://github.com/BerriAI/litellm/pull/35521) | 待合并 |

### 🆕 新出现的功能需求

**1. [#28168 导出 UI 管理的代理状态为声明式文件](https://github.com/BerriAI/litellm/issues/28168)**（3 条评论）
多环境运维（dev/staging/prod）需要将 UI 中的配置导出为声明式 config 以便复制。LiteLLM 当前 config.yaml 只覆盖代码化配置，UI 管理的状态（key、团队、预算）无法导出。这是 GitOps 工作流的关键缺口。

**2. [#35410 支持 morph 平台的 kimi k3、glm 5.2 等模型](https://github.com/BerriAI/litellm/issues/35410)**
用户请求增加对新模型提供方 Morph 的支持，此类请求通常会在 1-2 周内由维护者合并模型列表更新。

### 🧭 路线图信号
- **Rust 化正在实际落地**：Rust toolchain 固定（[PR #35519](https://github.com/BerriAI/litellm/pull/35519)）+ [Issue #31261](https

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*