# OpenClaw 生态日报 2026-08-31

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-31 00:40 UTC

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

# Pi 项目动态日报 — 2026-08-31

## 1. 今日速览

过去24小时Pi项目保持高速运转：Issues更新40条，其中36条关闭（关闭率90%），PR合并/关闭6条（合并率75%），无新版本发布。值得注意的是，今日Issue中涌现出一批高信号量的bug报告（JSONL会话损坏、OOM死亡螺旋、工具调用被静默丢弃等），其中两个关键问题已有对应fix PR合并（#8852→#8853、#8845→#8862），显示出维护者响应迅速。社区对Windows支持问题的讨论持续升温（#7547累计51条评论），是当前最受关注的话题。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日共6个PR合并/关闭，其中4个为实质性修复，2个为新功能/改动。关键进展：

- **fix(coding-agent): expose host keybinding access on the extension API**（[PR #8872](https://github.com/earendil-works/pi/pull/8872)，已关闭）— 修复扩展API中keybinding访问问题（对应[#4748](https://github.com/earendil-works/pi/issues/4748)），解决了扩展加载时模块级单例断裂导致快捷键提示为空的问题。
- **fix(agent,coding-agent): derive branch summary output budget from reserveTokens**（[PR #8862](https://github.com/earendil-works/pi/pull/8862)，已关闭）— 修复`/tree`分支总结在大分支上确定性失败的问题（对应[#8845](https://github.com/earendil-works/pi/issues/8845)），不再硬编码`maxTokens: 2048`。
- **fix(agent): prevent duplicate JSONL writers**（[PR #8853](https://github.com/earendil-works/pi/pull/8853)，已关闭）— 修复同一会话文件在单进程内被打开两次导致序列号重复、文件损坏的问题（对应[#8852](https://github.com/earendil-works/pi/issues/8852)），按规范路径序列化写入操作，已通过123项会话测试。
- **fix(ai): unref codex WebSocket idle-cache timer**（[PR #8866](https://github.com/earendil-works/pi/pull/8866)，已关闭）— 修复Codex扩展导致`pi -p`单次运行后进程存活5分钟的问题，通过unref定时器并补充文档。

新功能方面：新增Tencent Token Plan Individual provider（[PR #8844](https://github.com/earendil-works/pi/pull/8844)，已关闭），覆盖tc-code-latest、deepseek-v4系列、glm-5.2等模型；另有pi web GUI PR（[PR #8840](https://github.com/earendil-works/pi/pull/8840)，已关闭），提供与TUI功能对等的浏览器界面，但该PR状态为关闭（未明确是否合入）。

整体来看，今日修复集中在扩展生态、会话存储完整性和Provider适配层面，项目在稳定性和可扩展性两个维度均有实质推进。

## 4. 社区热点

- **[#7547 [Windows] How do you use Pi on windows? What issues are you seeing?](https://github.com/earendil-works/pi/issues/7547)** — 51条评论，👍2。作者发起Windows使用情况调研，意图收集用户在Windows上运行Pi的各种方式及遇到的问题，以便聚焦精力。该帖子自8月3日开设至今持续活跃，说明Windows支持是社区强烈关注的方向，但维护者尚未给出明确行动方案。

- **[#3200 Support video/audio content in prompt command](https://github.com/earendil-works/pi/issues/3200)** — 10条评论，👍6。希望`prompt`命令像支持images一样支持video/audio多模态输入，以便Gemma 4、GPT-4o等模型消费。该请求已开放4个多月，点赞数在今日Issues中最高，反映多模态需求在Agent场景中的迫切性。

- **[#4748 pi-tui: getKeybindings() realm/instance singleton breaks extensions](https://github.com/earendil-works/pi/issues/4748)** — 6条评论，👍2。扩展加载时解析到私有pi-tui实例，导致全局keybindings单例与宿主不同步。该问题已有对应PR #8872修复，是今日"社区反馈→快速修复"的典型案例。

## 5. Bug 与稳定性

按严重程度排列：

**🔴 严重 — 可能导致数据损坏或进程崩溃**

- **JSONL会话文件重复序列号损坏**（[#8852](https://github.com/earendil-works/pi/issues/8852)）— 同一文件在单进程内打开两次会写入重复的`seq: 1`，且无报错。**已有fix PR #8853合并**，风险已解除。
- **长会话不可恢复死亡螺旋**（[#8864](https://github.com/earendil-works/pi/issues/8864)）— 上下文超限后`clampMaxTokensToContext()`将`max_tokens`钳制为1，模型返回1-token响应后估计锚点自我强化，会话永久卡死。**未见fix PR**，影响面较大。
- **请求组装缺陷：悬挂tool_use + 字节级413**（[#8859](https://github.com/earendil-works/pi/issues/8859)）— 分支后残留悬挂tool_use导致400错误；token-based压缩未考虑字节上限导致413。**未见fix PR**，已在真实会话中复现。

**🟠 中等 — 功能异常或静默错误**

- **两个工具调用共享index时第二个被静默丢弃**（[#8861](https://github.com/earendil-works/pi/issues/8861)）— openai-completions累加器只保留第一个调用，第二个完整工具调用丢失。**未见fix PR**。
- **markdown围栏包裹的tool arguments降级为`{}`**（[#8858](https://github.com/earendil-works/pi/issues/8858)）— 某些模型/网关返回代码围栏包裹的arguments，解析后成为空对象。**未见fix PR**。
- **0.84.3回归：持续推理+20GB+ OOM**（[#8746](https://github.com/earendil-works/pi/issues/8746)）— 0.84.3版本每天触发OOM killer，进程RSS达21-27GB，0.84.2正常。**未见fix PR**。
- **Anthropic prompt cache从不回读transcript**（[#8849](https://github.com/earendil-works/pi/issues/8849)）— `cacheRead`全程停留在system+tools前缀，`cacheWrite`每轮上升，导致成本远超预期。**未见fix PR**。

**🟡 轻量 — 体验问题**

- **Agent循环无工具执行超时**（[#8857](https://github.com/earendil-works/pi/issues/8857)）— 工具调用挂起时整体卡死（如psql等待数据库连接），LLM流超时和bash超时均不覆盖此阶段。**未见fix PR**。
- **/tree分支总结确定性失败**（[#8845](https://github.com/earendil-works/pi/issues/8845)）— 硬编码`maxTokens: 2048`导致大分支总结时token不足。**已有fix PR #8862合并**。

## 6. 功能请求与路线图信号

- **多模态prompt扩展**（[#3200](https://github.com/earendil-works/pi/issues/3200)）— 视频/音频内容转发至LLM。👍6，开放4个月，多模态Agent是明确方向。
- **Ollama Cloud内置provider**（[#4706](https://github.com/earendil-works/pi/issues/4706)）— 利用Ollama云服务运行deepseek-v4、gemma4等模型。今日新增腾讯Token Plan provider（PR #8844），说明第三方provider接入在持续推进。
- **系统提示词膨胀治理**（[#8854](https://github.com/earendil-works/pi/issues/8854)）— 第三方包注入大量promptGuidelines导致提示词臃肿，作者提议社区方案pi-prompt-diet。扩展生态繁荣后副作用开始显现。
- **bash工具可选description参数**（[#8863](https://github.com/earendil-works/pi/issues/8863)）— 在TUI中显示命令用途说明，改善可读性。
- **统一资源命名空间`pi.namespace`**（[#8834](https://github.com/earendil-works/pi/issues/8834)）— 对技能和提示词模板引入命名空间避免冲突。
- **`pi list`显示版本号**（[#8865](https://github.com/earendil-works/pi/issues/8865)）— 列出扩展类型及版本信息。
- **web GUI**（PR [#8840](https://github.com/earendil-works/pi/pull/8840)）— 浏览器GUI与TUI功能对等，虽PR已关闭，但方向值得关注。
- **zai-api provider**（[#6723](https://github.com/earendil-works/pi/issues/6723)）— 区分API端点和coding端点。
- **StepFun内置provider**（[#8867](https://github.com/earendil-works/pi/issues/8867)）— 面向中国市场新增模型供应商。

## 7. 用户反馈摘要

- **Windows用户的使用困惑**（[#7547](https://github.com/earendil-works/pi/issues/7547)）— 大量Windows开发者希望使用Pi，但运行方式碎片化（WSL、原生、Docker等），维护者难以聚焦优化方向。用户期待官方明确推荐的Windows使用路径。
- **OOM问题引发信任危机**（[#8746](https://github.com/earendil-works/pi/issues/8746)）— "同模型、同xhigh思考，0.84.2跑了十天没问题，更新到0.84.3两天被杀五次"。回归问题对用户信心影响显著，且暂未收到修复反馈。
- **成本焦虑**（[#8849](https://github.com/earendil-works/pi/issues/8849)）— 用户手动检查session JSONL发现prompt cache未生效，导致长会话成本远超预期。用户对透明度和成本可预测性有较高期待。
- **生态过载的信号**（[#8854](https://github.com/earendil-works/pi/issues/8854)）— 安装8-15个第三方包后系统提示词大量膨胀，用户主动提出"节食"方案，说明插件机制虽好但需要治理工具。
- **TUI细节体验**（[#8855](https://github.com/earendil-works/pi/issues/8855)）— thinking区域的换行显示异常，用户发现0.84.4中已修复，但0.84.3仍存在，提示版本碎片化问题。

## 8. 待处理积压

- **[#7547 Windows使用调研](https://github.com/earendil-works/pi/issues/7547)** — 开放28天，51条评论，2👍。信息量巨大但维护者未回应。建议官方据此制定Windows支持策略，避免社区热情消退。
- **[#3200 多模态prompt支持](https://github.com/earendil-works/pi/issues/3200)** — 开放4个月+，10条评论，6👍。点赞数揭示强需求，但长时间无assignee或milestone。
- **[#4706 Ollama Cloud provider](https://github.com/earendil-works/pi/issues/4706)** — 开放3个月，4条评论。本地模型厂商的云端延伸是重要补充，等待评估。
- **[#6723 zai-api provider](https://github.com/earendil-works/pi/issues/6723)** — 开放1.5个月，2条评论。涉及API端点区分的具体问题，贡献者已说明方案，等待维护者确认。
- **[#4748 keybinding单例问题](https://github.com/earendil-works/pi/issues/4748)** — 今日已有PR #8872修复，但Issue尚未关闭，建议维护者验证后关闭以保持积压清洁

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-31

## 1. 今日速览

过去 24 小时 LiteLLM 项目保持高活跃度：共产生 48 条 Issue 更新（37 新开/活跃、11 关闭）与 164 条 PR 更新（122 待合并、42 已合并/关闭），并发布 2 个 Release 候选版本。社区讨论焦点集中在 **Rust 迁移**（#31263，23 条评论、18 👍）这一长期战略方向上；与此同时，大量标记为 `stale` 的 PR 在今日被批量关闭（约 15+ 条），表明维护团队正在收缩历史积压。新 Issues 中出现数个值得关注的 bug（流式工具调用参数时序、可变默认参数、S3 日志丢失等），其中 #38926 已有配套回归测试 PR 跟进。总体判断：**项目活跃度高，但 PR 合并率偏低（约 26%）与 stale 积压问题需留意。**

## 2. 版本发布

今日发布 2 个 Release Candidate 版本：

- **[v1.100.0-rc.1](https://github.com/BerriAI/litellm/releases/tag/v1.100.0-rc.1)** — 里程碑版本候选（1.100）
- **[v1.99.0-rc.2](https://github.com/BerriAI/litellm/releases/tag/v1.99.0-rc.2)**

两个版本的官方发布说明均仅包含 Docker 镜像签名验证指引（自 commit `0112e53` 起所有镜像使用 Cosign 签名）。发布说明中未附详细变更日志，建议用户关注 RC 版本稳定性，生产环境建议等待正式版发布。

## 3. 项目进展

### 今日合并/关闭的 PR 亮点

**新增功能/新供应商集成：**
- [#38924](https://github.com/BerriAI/litellm/pull/38924) `feat: add llmman as an OpenAI-compatible provider` — 新增 llmman 本地模型运行器支持（已关闭，另有同内容 #38925 处于开放状态，疑似重复提交）

**历史 stale PR 批量关闭（多为超期未合并的社区贡献）：**
- [#24068](https://github.com/BerriAI/litellm/pull/24068) feat: add ModelsLab provider
- [#26371](https://github.com/BerriAI/litellm/pull/26371) feat: add Telnyx as OpenAI-compatible provider
- [#27562](https://github.com/BerriAI/litellm/pull/27562) fix(chatgpt): aggregate output items for non-streaming responses
- [#27797](https://github.com/BerriAI/litellm/pull/27797) fix(responses): emit function-call args from .done event
- [#28190](https://github.com/BerriAI/litellm/pull/28190) fix(streaming): guard raise_on_model_repetition against empty choices chunks
- [#28359](https://github.com/BerriAI/litellm/pull/28359) cookbook: SpendGuard runtime budget guardrails
- [#28785](https://github.com/BerriAI/litellm/pull/28785) fix(proxy): stream raw bytes for streamGenerateContent

这些 PR 多数带有 `[stale]` 标记且已存在数月，今日集中关闭意味着它们**未被纳入主线**。其中部分修复（如 #27797、#28190）可能已被其他实现取代，或需要贡献者基于最新 main 分支重新提交。

### 关闭的 Issue 暗示的收入修复

- [#28461](https://github.com/BerriAI/litellm/issues/28461) DeepSeek v4 Flash thinking 模式下 `reasoning_content` 不返回 — 已关闭
- [#26613](https://github.com/BerriAI/litellm/issues/26613) DB 模型 `litellm_params` 未生效 — 已关闭
- [#28778](https://github.com/BerriAI/litellm/issues/28778) 语义缓存导致工具返回内容丢失 — 已关闭

*注：今日关闭的 42 个 PR 中绝大多数是 stale 清理，实际合并的核心代码改进有限。*

## 4. 社区热点

### 🔥 最热 Issue：Rust 迁移

**[#31263 LiteLLM Rust Migration - the fastest and litest AI Gateway (sub 1ms overheads)](https://github.com/BerriAI/litellm/issues/31263)**
- 23 条评论 | 18 👍 | 创建 2026-06-25，持续活跃至今
- 作为 Rust 迁移的父 ticket，社区对性能表现（<1ms 开销）和 Beta 测试资格高度关注
- 释放出强烈信号：**LiteLLM 正将核心 Gateway 向 Rust 重写**，这是未来最重大的架构演进方向

### 高互动 Issue：GitHub Copilot 用量异常

**[#18155 [Bug]: GitHub Copilot Provider - Excessive Premium Request Usage](https://github.com/BerriAI/litellm/issues/18155)**（已关闭）
- 10 👍 | 6 条评论
- 长时多轮 agentic 场景下 Copilot Premium 请求被过量消耗，已获解决

### 高赞功能请求：中文本地化

**[#28772 Feature: 添加简体中文语言支持](https://github.com/BerriAI/litellm/issues/28772)**（已关闭）
- 48 👍 — 今日展示 Issue 中赞数最高
- 虽已关闭（标记 stale），但 48 个 👍 说明社区对 Dashboard UI 国际化的需求非常强烈

## 5. Bug 与稳定性

按严重程度排列：

### 🔴 高严重度

| Issue | 问题描述 | 状态 |
|-------|---------|------|
| [#38926](https://github.com/BerriAI/litellm/issues/38926) | `stream_options.include_usage=true` 导致工具调用参数在流结束时突发输出（vLLM 场景：原本 218 个增量事件被压缩为 3 个），破坏流式体验 | 🆕 今日新开，已有 [#38928](https://github.com/BerriAI/litellm/pull/38928) 提交回归测试 |
| [#38731](https://github.com/BerriAI/litellm/issues/38731) | litellm 停止转发模型请求（1.97.0 容器化部署 + 临时密钥自动删除场景） | ✅ 已关闭 |
| [#32202](https://github.com/BerriAI/litellm/issues/32202) | `pass_through_endpoints` + `forward_headers: true` 存在 **API key 泄露**风险：将代理 Authorization 转发至上游，且未剥离 `x-pass-` 前缀，与官方文档承诺矛盾 | 🟡 开放中，3 条评论 |

### 🟡 中严重度

| Issue | 问题描述 | 状态 |
|-------|---------|------|
| [#28907](https://github.com/BerriAI/litellm/issues/28907) | S3 批量 flush 未等待上传完成即清空队列，**日志丢失**风险 | 🟡 开放中 |
| [#25951](https://github.com/BerriAI/litellm/issues/25951) | `/team/member_add` 并发写入存在**竞态条件**，团队成员丢失 | 🟡 开放中，已提供根因分析 |
| [#24498](https://github.com/BerriAI/litellm/issues/24498) | Claude 模型偶发返回空消息占位符 `[System: Empty message content sanitised...]` | 🟡 持续开放，11 条评论 |
| [#38909](https://github.com/BerriAI/litellm/issues/38909) | `InfinityError` 构造函数使用**可变默认参数** `headers={}`，实例间共享状态 | 🟡 今日新开 |

### 🟢 低严重度

- [#38928](https://github.com/BerriAI/litellm/pull/38928) 正在为 #38926 撰写回归测试，尚未开始修复实现
- 多数 stale bug（如 #28766、#28773、#28782、#29261 等）今日被关闭

## 6. 功能请求与路线图信号

### 明确的路由器/网关层演进信号

- **Rust 迁移**（#31263）：LiteLLM 下一代核心架构方向，目标 <1ms 开销，官方已发布博客并招募早期 Beta 测试者
- [#24450](https://github.com/BerriAI/litellm/issues/24450)：MCP passthrough `/health` 端点 — 生态健康检查能力增强

### 新供应商集成 PR（可能进入后续版本）

今日有多个新 provider 的 PR 提交/关闭：

| PR | 供应商 | 状态 |
|----|--------|------|
| [#38924](https://github.com/BerriAI/litellm/pull/38924) / [#38925](https://github.com/BerriAI/litellm/pull/38925) | llmman（本地模型运行器，OpenAI 兼容） | 一关一开，待维护者处理 |
| [#23523](https://github.com/BerriAI/litellm/pull/23523) | Bedrock body 参数剥离 + thinking + websearch 修复 | 🟡 开放中（3 月提交） |
| [#29449](https://github.com/BerriAI/litellm/pull/29449) | Foundry Local provider | 🟡 开放中（stale） |
| [#24068](https://github.com/BerriAI/litellm/pull/24068) | ModelsLab | ❌ 已关闭 |
| [#26371](https://github.com/BerriAI/litellm/pull/26371) | Telnyx | ❌ 已关闭 |

### 管理面功能请求

- [#33392](https://github.com/BerriAI/litellm/issues/33392)：Terraform guardrail 资源支持（基础设施即代码方向）
- [#28772](https://github.com/BerriAI/litellm/issues/28772)：Dashboard 简体中文支持（48 👍，呼声最高）

## 7. 用户反馈摘要

**正面反馈：**
- Rust 迁移获得社区高关注度和积极预期（18 👍 + 活跃讨论）
- #18155 Copilot 过度用量问题成功关闭，说明该场景获得修复
- 多个长期 stale bug 被批量关闭，释放了"维护者正在清理问题"的信号

**负面反馈/痛点：**

1. **配置不生效问题反复出现**：#26613 用户报告通过 DB 配置的 `litellm_params`（如 `use_chat_completions_api`）未生效，类似问题在多个场景中被提及
2. **动态密钥生命周期管理存在隐患**：#38731 用户在使用 mgmt API 创建/自动删除临时密钥时遭遇请求停止转发，说明 ephemeral key 机制在边缘场景下不够健壮
3. **文档与实现不一致引发的安全问题**：#32202 中 `forward_headers` 文档承诺与实际行为严重不符（API key 泄露风险），用户对文档信任度受挫
4. **中文用户群体活跃**：#28772 以 48 👍 成为最高赞请求，凸显 LiteLLM 在中文社区的采用率与本地化诉求

## 8. 待处理积压

### 长期未合并的 PR（标 `stale`，已存在 3 个月以上）

| PR | 内容 | 持续时间 | 备注 |
|----|------|---------|------|
| [#23523](https://github.com/BerriAI/litellm/pull/23523) | Bedrock body 参数剥离、thinking 修复、API key 加载 | ~5.5 个月 | 作者称已在生产环境运行，建议维护者评估合并价值或关闭 |
| [#29398](https://github.com/BerriAI/litellm/pull/29398) | Adaptive Router 重载后 500 错误修复 | ~3 个月 | 有明确 bug 对应（#29397） |
| [#29260](https://github.com/BerriAI/litellm/pull/29260) | UI 过滤器面板空白修复 | ~3 个月 | 解决 LIT-3151 |
| [#29440](https://github.com/BerriAI/litellm/pull/29440) | Langfuse OTEL 集成支持 per-key environment | ~3 个月 | 与 #11289 功能对齐 |
| [#29384](https://github.com/BerriAI/litellm/pull/29384) | `/apply_guardrail` 返回结构化 guardrail_response | ~3 个月 | 增强 API 可用性 |

### 长期未解决的 Issue

| Issue | 问题 | 持续时间 | 当前状态 |
|-------|------|---------|---------|
| [#24498](https://github.com/BerriAI/litellm/issues/24498) | Claude 空消息占位符 | ~5 个月 | 11 条评论仍开放，影响面较大 |
| [#25951](https://github.com/BerriAI/litellm/issues/25951) | `/team/member_add` 竞态条件 | ~4.5 个月 | 已定位根因（read-modify-write），等待修复 PR |
| [#28907](https://github.com/BerriAI/litellm/issues/28907) | S3 日志上传丢失 | ~3 个月 | 已定位根因（未 await 批量任务），等待修复 PR |

---

*本日报基于 2026-08-31 的 GitHub 公开数据自动生成，仅供项目健康度参考。统计口径以数据概览为准。*

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*