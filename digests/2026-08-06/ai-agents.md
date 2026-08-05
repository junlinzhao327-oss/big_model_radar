# OpenClaw 生态日报 2026-08-06

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-05 23:26 UTC

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

## 分析说明

本次对比以包含有效动态数据的 **Pi**、**LiteLLM**、**Temporal** 三个项目为核心；**OpenClaw** 虽被指定为“核心参照”，但当日快照未提供其 Issues/PR/Release 数据，**Hermes Agent** 与 **OpenHands SDK** 同样无动态数据，因此无法纳入量化对比。

---

## 1. 生态全景

当前个人 AI 助手与自主智能体生态呈现“应用层创新 + 基础设施加固”双轨并行的态势。Pi 在终端交互、模型选择、扩展机制上高频迭代，LiteLLM 则在成本计量、多 provider 适配、网关稳定性上密集合入修复，Temporal 则聚焦底层调度可靠性与复制一致性。社区反馈对路线图影响直接，Issue 到 PR 的闭环速度较快。整体看，AI 智能体正在从“能对话”迈向“能可靠执行、可治理、跨平台可用”的阶段。

---

## 2. 各项目活跃度对比

| 项目 | Issue 动态 | PR 动态 | Release | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 未提供 | 未提供 |

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

## 1. 今日速览

Pi 项目今日活跃度极高，24 小时内处理 73 条 Issue 更新（关闭 58 条）与 37 条 PR 更新（合并/关闭 30 条），表现出维护团队对社区反馈的高度响应性。当前最高热度议题是 Windows 使用体验调研（#7547），反映项目正在扩展跨平台支持。无新版本发布，但 PR 集中展示了 **OSC 8 超链接修复、AGENTS.override.md 支持、Qwen 新模型接入、事件总线泄漏修复**等多项实质进展，项目整体处于健康的快速迭代节奏。

---

## 3. 项目进展

今日合并/关闭的 PR 覆盖多项功能和修复，主要进展集中在以下几方面：

**新功能落地**
- **AGENTS.override.md 支持**（[#7681](https://github.com/earendil-works/pi/pull/7681)、[#7664](https://github.com/earendil-works/pi/pull/7664)）：同一目录下存在 AGENTS.override.md 时优先于 AGENTS.md/CLAUDE.md 加载，实现 per-directory 上下文覆盖，两个 PR 均已合并。
- **@file 引用支持行范围**（[#7679](https://github.com/earendil-works/pi/pull/7679)）：支持 `@file#L122-L145` 语法，按 GitHub 风格精确引用文件片段，对齐 `read` 工具的 EOF 处理。
- **Qwen Token Plan 模型更新**（[#7670](https://github.com/earendil-works/pi/pull/7670)）：将 `qwen3.8-max-preview` 替换为 GA 版 `qwen3.8-max`，并映射 `low`/`medium`/`xhigh` 推理 effort 级别。
- **模型选择器自然排序**（[#7692](https://github.com/earendil-works/pi/pull/7692)、[#7690](https://github.com/earendil-works/pi/pull/7690)）：`/model` 与 `/scoped-models` 共享比较器，按大小写不敏感、数字感知方式排序，提升含上下文窗口变体模型的导航体验。

**关键修复**
- **事件总线泄漏修复**（[#7656](https://github.com/earendil-works/pi/pull/7656)）：解决 #7193 — 扩展监听器在会话重载/销毁后残留在共享事件总线的问题，将监听器作用域限定到所属扩展运行时。
- **Copilot 模型列表修复**（[#7672](https://github.com/earendil-works/pi/pull/7672)）：`availableModelIds` 为空的问题，通过保留 `model_picker_enabled` 信号 + Individual 端点无可用模型时回退到 policy 启用模型来解决。
- **OSC 8 超链接截断修复**（[#7657](https://github.com/earendil-works/pi/pull/7657)、[#7665](https://github.com/earendil-works/pi/pull/7665)）：`truncateToWidth()` 截断超链接标签时自动闭合链接，并优化纯文本前缀的扫描路径，附带回归测试。
- **lgtm 逗号识别修复**（[#7663](https://github.com/earendil-works/pi/pull/7663)）：`LGTM, please submit...` 这类带逗号的审批评论现在能正确触发自动合并流程。
- **bunfig.toml 自动加载禁用**（[#7685](https://github.com/earendil-works/pi/pull/7685)）：编译后的独立二进制通过 `--no-compile-autoload` 避免 cwd 下 `preload` 导致的启动崩溃。

**基础设施**
- **Harness v2 R2**（[#7669](https://github.com/earendil-works/pi/pull/7669)）：新增纯函数 lane reducer，定义 `LaneReductionInput → LaneReductionResult` 契约，从有界恢复记录中派生持久化 LaneState 与终端故障来源。
- **可配置 Harness 工厂**（[#7686](https://github.com/earendil-works/pi/pull/7686)，开放中）：为 coding-agent 增加内部 Harness 构造工厂，保留调用方提供的工具、激活配置等选项。
- **工具提示贡献收集**（[#7671](https://github.com/earendil-works/pi/pull/7671)，开放中）：将内置工具的 system-prompt 片段与实现代码放置在一起，便于维护，并增加回归覆盖。
- **open_operation_id 投影**（[#7654](https://github.com/earendil-works/pi/pull/7654)）：在 lane 级别为 `open_operation_id` 建立投影，使存储层能强制每条 lane 最多一个进行中的 open 操作。

---

## 4. 社区热点

**🔹 Windows 使用体验大调研（[#7547](https://github.com/earendil-works/pi/issues/7547)，17 条评论，开放中）**
维护者 @petrroll 主动发起的议题，向 Windows 用户收集使用方式与痛点。评论区热度最高，预计将引导项目在 Windows 支持上的资源分配方向。该议题对项目路线图有直接影响，值得持续关注。

**🔹 truncateToWidth() OSC 8 超链接悬挂（[#7399](https://github.com/earendil-works/pi/issues/7399)，12 条评论，已关闭）**
用户报告了终端输出截断时留下未闭合 OSC 8 超链接导致的显示异常。该问题已由 PR #7657/#7665 修复，展示了社区从 bug 报告到修复的快速闭环。

**🔹 WSL 绝对路径处理缺陷（[#7064](https://github.com/earendil-works/pi/issues/7064)，12 条评论，开放中）**
WSL2 环境中 `read`/`write`/`edit` 工具频繁失败，原因是 Windows 路径解析有误。已获 1 个 👍，目前仍无对应修复 PR，是跨平台优先级较高的待处理问题，与 #7547 的 Windows 调研直接相关。

---

## 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 状态 |
|---|---|---|---|
| 🔴 高 | [#7634](https://github.com/earendil-works/pi/issues/7634) | Copilot 登录后 `/model` 无模型可用（`availableModelIds` 恒为空） | **已有修复 PR #7672**（已合并） |
| 🔴 高 | [#7064](https://github.com/earendil-works/pi/issues/7064) | WSL 下绝对 Windows 路径被错误处理，导致 read/write/edit 工具失败 | 开放中，无修复 PR |
| 🟠 中 | [#7444](https://github.com/earendil-works/pi/issues/7444) | WebSocket 重试仅覆盖两种错误码，其他瞬态错误直接终止 turn | 开放中，无修复 PR |
| 🟠 中 | [#7666](https://github.com/earendil-works/pi/issues/7666) | Bash 工具中输入多行命令时，未以 `;`/`&&`/`\|` 结尾的行被折叠为空格，导致下一行成为上一命令的参数 | 开放中，无修复 PR |
| 🟠 中 | [#7601](https://github.com/earendil-works/pi/issues/7601) | Node 20 下因 undici CacheStorage 需要 ≥22.19 导致启动崩溃 | 已标记 [no-action]（环境要求），非代码缺陷 |
| 🟡 低 | [#7594](https://github.com/earendil-works/pi/issues/7594) | 发布二进制缺少 `node:sqlite` 内置模块，导致 `pi-total-recall` 等扩展加载失败 | 已标记 [no-action]，可能为构建配置问题 |
| 🟡 低 | [#7613](https://github.com/earendil-works/pi/issues/7613) | 重试成功但红色错误行永久留在聊天界面，造成误判 | 开放中，无修复 PR |
| 🟡 低 | [#7616](https://github.com/earendil-works/pi/issues/7616) | TUI 聊天滚动跳动：工具块超过视口时触发全屏重绘，且缺 PageUp/PageDown 历史滚动 | 开放中，无修复 PR |
| 🟡 低 | [#7193](https://github.com/earendil-works/pi/issues/7193) | 扩展事件总线监听器在会话重载后泄漏 | **已有修复 PR #7656**（已合并） |
| 🟢 参考 | [#6675](https://github.com/earendil-works/pi/issues/6675) | `pi update --self` 因一次瞬时连接失败即终止 | 已关闭（可视为已处理） |
| 🟢 参考 | [#5291](https://github.com/earendil-works/pi/issues/5291) | Anthropic 订阅用户会话卡在 “Working...”，需手动中断恢复 | 已关闭 |

---

## 6. 功能请求与路线图信号

今日新增的功能请求反映了以下方向，部分已进入实现阶段：

**✅ 已被 PR 实现/即将落地**
- **`@file#L122-L145` 行范围引用**（[#7673](https://github.com/earendil-works/pi/issues/7673) → 已由 [#7679](https://github.com/earendil-works/pi/pull/7679) 实现）— 面向 Neovim Pi 插件等编辑器集成场景。
- **AGENTS.override.md per-directory 上下文覆盖**（[#7642](https://github.com/earendil-works/pi/issues/7642) → 已由 [#7681](https://github.com/earendil-works/pi/pull/7681) 实现）。
- **Qwen Token Plan Individual 独立 provider**（[#7631](https://github.com/earendil-works/pi/issues/7631) → 对应 PR [#7659](https://github.com/earendil-works/pi/pull/7659) 开放中），精确匹配 Individual 订阅的文本模型白名单。
- **扩展 API 持久化 API-key 凭证到 auth.json**（[#7658](https://github.com/earendil-works/pi/issues/7658)）— 当前仅能用 `registerProvider()` 注册 provider 但无法程序化保存密钥。
- **TUI 组件鼠标事件支持**（[#7683](https://github.com/earendil-works/pi/issues/7683)）— 可选 `Component.onMouse()` 接收相对坐标事件，在滚动条/选择处理之前分发。
- **TUI 底部填充标记**（[#7682](https://github.com/earendil-works/pi/issues/7682)）— 零宽 fill marker，让组件可将短会话固定在屏幕底部。
- **provider 重试的 onRetry 回调**（[#7649](https://github.com/earendil-works/pi/issues/7649)）— 将重试细节暴露给调用方。

**🔮 路线图信号**
- **Mermaid 图表渲染**（[#7623](https://github.com/earendil-works/pi/issues/7623)）— 用户建议使用 grok-mermaid 库。
- **JetBrains IDE 作为语言后端**（[#7641](https://github.com/earendil-works/pi/issues/7641)）— pi-serena 目前仅支持 LSP 后端，Jet

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目日报 — 2026-08-06

## 1. 今日速览

过去24小时项目保持高活跃度：**73条Issue更新**（新开/活跃47，已关闭26）、**323条PR更新**（待合并191，已合并/关闭132），并发布开发版本 `v1.97.0-dev.1`。社区讨论热度集中在UI暗色模式（62条评论、70个👍）和每日速率限制功能请求上；开发侧则围绕成本映射准确性、密钥轮换安全性、流式计费可靠性等多个稳定性方向集中合入修复。整体看，项目在功能迭代与稳定性加固双线上均有明显推进，健康度良好。

---

## 2. 版本发布

### v1.97.0-dev.1（开发版）
- **发布说明要点**：本次为开发版发布，说明内容聚焦 Docker 镜像签名验证——所有 LiteLLM Docker 镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 签名，每次发布使用自 commit [`0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0) 引入的同一密钥。
- **破坏性变更**：无（开发版，内容有限）
- **注意事项**：正式部署用户建议关注后续 `v1.97.0-stable` 版本的发布说明。

---

## 3. 项目进展

今日合入/关闭的 PR 集中在**成本计量、安全加固与合规一致性**三个方向：

- **[#36010](https://github.com/BerriAI/litellm/pull/36010)（已合并）**：`add_known_models` 中重建 `models_by_provider`，使"重载价格数据"后成本映射能正确传递到通配符模型列表。新价格模型无需重启即可出现在 `/v1/models` 和 key/team 下拉菜单中。该修复直接对应社区反馈的"价格更新后模型列表延迟生效"问题。
- **[#36011](https://github.com/BerriAI/litellm/pull/36011)（已合并）**：将请求参数检查从仅覆盖 body 扩展到 path、form 输入，修复了路径形式指定的 deployment 名跳过目的地检查、bracket 形式 form 元数据跳过参数检查等安全一致性漏洞。⚠️ 此 PR 标记为 `fix(proxy)!`，**含破坏性变更**，升级时需关注请求参数校验行为变化。
- **[#33972](https://github.com/BerriAI/litellm/pull/33972)（已合并）**：将通用的 `error` finish_reason 映射为 `stop`，修复 `core_helpers` 中流式结束状态处理。
- **[#24817](https://github.com/BerriAI/litellm/pull/24817)（已合并）**：更新 `test_gemini` 测试中已弃用的 `gemini-2.0-flash` 为 `gemini-2.5-flash`，修复集成测试 404 失败。

**关键 PR（待合并但值得关注）**：

- **[#36019](https://github.com/BerriAI/litellm/pull/36019)**：将 managed 文件统一 ID 生成改为确定性 `uuid5`，解决并发注册时同一 provider 文件产生多个不同 ID 的竞态问题。
- **[#36020](https://github.com/BerriAI/litellm/pull/36020)**：config 中 agent id 改为仅对 `agent_name` 做哈希，密钥轮换后授权不再失效，修复 403 误伤。

---

## 4. 社区热点

| Issue/PR | 评论数 | 👍 | 状态 | 热点分析 |
|----------|--------|-----|------|----------|
| [#10177 暗色模式](https://github.com/BerriAI/litellm/issues/10177) | 62 | 70 | OPEN | 创建于15个月前，至今仍为活跃讨论榜首。用户呼声高但迟迟未落地，是 UI 方向最强烈的长期需求。 |
| [#14398 每日/每令牌速率限制](https://github.com/BerriAI/litellm/issues/14398) | 11 | 7 | OPEN | 请求/令牌按分钟限制已支持，但多家 provider 免费/Pro 层有**按日配额**，用户需要按日维度限流，运维场景刚需。 |
| [#18654 OCI Gemini 工具调用异常](https://github.com/BerriAI/litellm/issues/18654) | 8 | 1 | OPEN（标记 stale） | OCI 提供方在流式/非流式下工具调用均报异常，已标记 stale，但仍有持续讨论，需关注。 |

社区对 **UI 体验**（暗色模式）、**配额管理**（按日限速）、**OCI 提供商稳定性** 三个方面诉求较突出。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue | 描述 | 相关 PR |
|----------|-------|------|---------|
| 🔴 严重 | [#25447 Redis Cluster 串线](https://github.com/BerriAI/litellm/issues/25447) | OpenShift 多副本 Redis Cluster 环境下偶发**响应返回给错误客户端**，数据泄露风险。 | 未发现对应 fix PR |
| 🟠 高 | [#34309 缓存成本丢失](https://github.com/BerriAI/litellm/issues/34309)（已关闭） | OpenAI Responses API 中 `cache_read_cost` / `cache_creation_cost` 始终为 null，成本拆分缺失。 | 已修复（关闭） |
| 🟠 高 | [#33772 缓存写入成本未计价](https://github.com/BerriAI/litellm/issues/33772)（已关闭） | OpenAI `cache_write_tokens` 未参与定价，缓存写入请求计价偏低。 | 已修复（关闭） |
| 🟠 高 | [#35357 批处理轮询整体中断](https://github.com/BerriAI/litellm/issues/35357)（已关闭） | `CheckBatchCost` 中单个 batch 异常导致整个轮询周期终止，其他 batch 被搁置。 | 已修复（关闭） |
| 🟠 高 | [#33988 批处理文件重复包装](https://github.com/BerriAI/litellm/issues/33988)（已关闭） | 重复调用 `GET /v1/batches/{id}` 可能将 `output_file_id` 嵌套包装成另一managed ID，导致下载异常。 | 修复方向与 [#36019](https://github.com/BerriAI/litellm/pull/36019) 一致 |
| 🟡 中 | [#27183 Ollama VLM 缺 pillow](https://github.com/BerriAI/litellm/issues/27183) | Ollama 视觉模型调用因镜像缺少 `pillow` 失败，影响容器部署用户。 | 未发现对应 fix PR |

**稳定性修复观察**：批量文件管理（#33988/#28294/#36019/#34092）和流式计费（#35971/#36008）是近期集中修的两个方向，说明项目正在处理**分布式一致性**与**按量计费准确性**类深水区问题。

---

## 6. 功能请求与路线图信号

**高热度新功能请求**：

- **[#10177 暗色模式](https://github.com/BerriAI/litellm/issues/10177)**：UI 方向呼声最高，评论区可看到多轮 UI 相关的增强讨论，预计后续会进入 UI 迭代计划。
- **[#14398 按日速率限制](https://github.com/BerriAI/litellm/issues/14398)**：月度/日额度管理对生产用户是刚需，与现有按分钟限流形成互补，纳入路线图可能性较高。
- **[#31819 Bedrock AgentCore Web Search 作为原生搜索提供商](https://github.com/BerriAI/litellm/issues/31819)**：扩展 `litellm.search()` 生态的需求，若落地将极大便利 Bedrock 用户。
- **[#35781 OpenAI 兼容 Fusion 模型（Auto Router 之上做模型融合）](https://github.com/BerriAI/litellm/issues/35781)**（新开）并行 fan-out + 聚合模型合成答案的 MoA 范式，社区用户已提出明确使用场景。

**近期 PR 预示的路线图方向**（均 OPEN，可能进入下一版本）：

- **[#35915](https://github.com/BerriAI/litellm/pull/35915) + [#36015](https://github.com/BerriAI/litellm/pull/36015)**：复杂度路由引入**用户自定义层级分类**与**LLM 分类器成本透明化**，路由能力进一步增强。
- **[#35969](https://github.com/BerriAI/litellm/pull/35969)**：将 NIM/vLLM 的扩展参数翻译为 Fireworks 原生参数，提升跨平台迁移兼容性。
- **[#36012](https://github.com/BerriAI/litellm/pull/36012)**：新增 **BytePlus** 提供商（VolcEngine 国际版），覆盖 Chat/Embeddings/Image Gen/TTS/Responses，国际化扩张信号明显。
- **[#36014](https://github.com/BerriAI/litellm/pull/36014)**：Guardrails 新增 `scan_only_tool_results` 开关，可将检测范围限定到工具输出，解决 agent 场景误报。

---

## 7. 用户反馈摘要

**🙁 痛点反馈**：

- **[#23941](https://github.com/BerriAI/litellm/issues/23941)（已关闭）**：用户对升级过程艰难表达了不满——"升级时 prisma 侧总是列缺失和迁移错误，即使下载最新 schema 也无法应用"。虽然该 issue 已关闭（stale），但暴露了 **升级文档与迁移工具链不完善**的问题，建议维护者提供更系统的升级指南。
- **[#32218](https://github.com/BerriAI/litellm/issues/32218)**：Z.AI Coding Plan 文档宣传 `glm-5.2[1m]` 但 LiteLLM 代理返回 "Unknown Model"，**文档与实际支持不一致**，影响用户信任。
- **[#20975](https://github.com/BerriAI/litellm/issues/20975)**：Azure Responses API 流式响应缺少必需 SSE 事件类型，客户端实现可能因此中断。

**😊 积极信号**：

- 今日关闭的 26 个 Issue 中，多个成本计算、批处理相关的 bug（#34309、#33772、#35357）均由社区用户报告并快速修复，说明 **用户反馈→修复的闭环效率较高**。
- Langfuse 团队官方成员（@hassiebp）直接提交了 [#33383](https://github.com/BerriAI/litellm/issues/33383) 升级集成请求，体现生态合作伙伴

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-08-06

## 1. 今日速览
过去 24 小时 Temporal 项目保持较高开发活跃度：PR 侧共 36 条动态（26 条待合并、10 条已合并/关闭），Issue 侧仅有 1 条关闭记录、无新开 Issue。开发重心明显集中在 `reliability-2026` 计划相关工作上，包括复制流韧性、调度器迁移、Worker Deployment 版本管理等方向。无新版本发布，但多个修复与功能已合入主干，项目在稳定性与可观测性维度稳步推进，整体健康度良好。

## 2. 版本发布
今日无新版本发布。

## 3. 项目进展
过去 24 小时合并/关闭的 PR 主要围绕稳定性修复与测试基建：

- **#11425 [CLOSED]** 修复 CHASM 调度器 pause-on-failure 的冲突令牌（conflict token）问题：自动暂停已提交后，过期的 Describe token 不再能覆盖持久化的暂停状态，并补充了回归测试。
- **#11166 [CLOSED]** 修复调度器迁移中同一时间点多个 pending start 身份重复的问题：为 V2→V1 迁移的 starts 生成唯一 `RequestId`/`WorkflowId`，避免冲突。
- **#11421 [CLOSED]** 新增 Worker Deployment 降级版本（demote-version）回放测试语料库，包含 20 个 Deployment 与 11 个 Version 历史，覆盖信号驱动的版本降级路径。
- **#11423 [CLOSED]** 修复批处理（batcher）对终端状态错误无限重试的问题，同时修复 `activity_api_batch_cancel/terminate` 两个 flaky 测试。
- **#11385 [CLOSED]** 独立活动（CHASM）重试失败信息现按工作流活动同策略截断，消除两者在 `LastFailureDetails` 上的行为差异。

这些合入表明项目在调度器正确性、复制/重试语义一致性、测试覆盖完整性上均有实质推进。

## 4. 社区热点
- **#10358 [CLOSED]**：唯一拥有 4 条评论的 Issue，讨论从 1.29.3 升级至 1.30.4 时因 schema 迁移导致必须停机的问题。该 Issue 昨日被关闭，但报告中未关联修复 PR，无法确认是否已提供解决方案。用户对自托管升级路径的期望与现实之间的落差，是当前社区最需要关注的信号。

其余 PR 的评论数未在数据中提供，无法量化排序；但从标签分布看，`reliability-2026` 系列 PR 是当前开发与讨论的绝对焦点。

## 5. Bug 与稳定性
| 严重度 | 条目 | 状态 | 说明 |
|--------|------|------|------|
| 高 | [#10358](https://github.com/temporalio/temporal/issues/10358) | 已关闭 | 升级 1.30.4 必须停机，schema 迁移具有破坏性；用户为自托管 + Postgres，直接阻塞生产升级路径。目前无关联修复 PR。 |
| 中 | [#11425](https://github.com/temporalio/temporal/pull/11425) | 已修复（已合并） | CHASM 调度器 pause-on-failure 冲突令牌缺陷，修复后过期 token 无法覆盖自动暂停状态。 |
| 中 | [#11422](https://github.com/temporalio/t

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*