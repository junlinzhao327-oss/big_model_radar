# AI CLI 工具社区动态日报 2026-09-06

> 生成时间: 2026-09-05 22:35 UTC | 覆盖工具: 7 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

# AI CLI 工具横向对比分析报告（2026-09-06）

> 说明：本次快照中，Claude Code、OpenAI Codex、Gemini CLI、OpenCode 四个仓库在统计窗口内未返回可解析的动态数据，以下分析以 Copilot CLI、Qwen Code、Kimi Code 三个工具的实际动态为基础展开。


## 1. 生态全景

AI CLI 工具正从“单点代码助手”向“长时运行的生产力基础设施”过渡。头部工具呈现明显的**功能分化**：以 Copilot CLI 为代表，依托编辑器生态与桌面端深度绑定，主攻企业级工作流与 MCP 工具链集成；以 Qwen Code 为代表的开源工具，则率先将后台 daemon 常驻、Web Shell 动态工作流可视化等“重型特性”推进至 nightly/preview 阶段，探索 AI 编程工具的形态边界；而以 Kimi Code 为代表的第三方模型接入方案，仍停留在补齐基础体验与生态文档阶段。三个活跃项目反映出的共同信号是：**模型能力已不再是唯一竞争点，更新机制可靠性、MCP/Agent 工具链稳定性、前端渲染 fidelity 正在成为社区口碑的分水岭。**


## 2. 各工具活跃度对比

| 工具 | 活跃 Issues 数 | 新增 Issues | PR 数（合并/活跃） | Release | 说明 |
|------|--------------|------------|-------------------|---------|------|
| **GitHub Copilot CLI** | 19 条（精选 10 条） | 约 8 条（9/5 集中提交） | 过去 24h 无更新 | **v1.0.84-1**（新增 GPT-6 Astra 支持） | 迭代节奏平稳，问题反馈密度最高 |
| **Qwen Code** | 10 条入选（含 P1/P2/P3） | 至少 8 条（9/5 集中提交） | **10 个 PR 活跃**（多为 fix） | **v0.23.1-preview.0** + **nightly** 双通道发布 | 修复节奏最快，前后端并行推进 |
| **Kimi Code CLI** | 2 条 | 1 条（#2635） | 无 | 无 | 社区规模较小，反馈量有限 |
| Claude Code | — | — | — | — | 本期无数据 |
| OpenAI Codex | — | — | — | — | 本期无数据 |
| Gemini CLI | — | — | — | — | 本期无数据 |
| OpenCode | — | — | — | — | 本期无数据 |

*Issue 数取各自日报“热点/活跃”口径，Qwen Code 包含 PR 关联 Issue，Copilot CLI 为总活跃量。*


## 3. 共同关注的功能方向

| 功能方向 | Copilot CLI | Qwen Code | Kimi Code | 共性诉求 |
|----------|------------|-----------|-----------|----------|
| **MCP/工具链可靠性** | #4731 取消后 tools/list 刷新超时导致工具被永久移除；#4721 参数 JSON-RPC 序列化损坏；#4729 子代理引用不存在的工具 | #11118 session 回收逻辑中进程 busy 定义不一致，活跃会话永不回收 | — | MCP/长期运行架构中，**取消、超时、回收等边界场景的状态一致性**正在成为大规模使用的核心障碍 |
| **终端/UI 渲染保真度** | #4722 Markdown 未闭合强调符导致前导 `_` 被吞 | #11108 Cmd+A 在 composer 中全选整页而非输入内容 | #2635 VS Code 渲染层丢字 | 跨工具出现“模型输出正确但 UI 吃字符/错选”类问题，说明渲染层正成为信任链上的薄弱环节 |
| **会话生命周期与升级安全性** | #4734 桌面版升级后所有 worktree 会话全挂；#4728 自动更新覆盖正在运行的 exe 导致会话断开 | #11119 session 运行时回收后后台输出/通知被静默丢弃 | — | 升级与会话恢复的健壮性是共同痛点：**用户可容忍功能缺失，但不接受静默丢状态** |
| **模型选型与行为可预测性** | #4732 模型突然切换至 GPT-5 mini 并中途停止 | #11093 新增持久化 focus 模式，隐藏推理行以获得更安静记录 | #1210 文档中 K2 Thinking 切换方式过于简略 | 用户对模型“自作主张”切换/行为漂移的容忍度正在降低，要求更明确的选择与控制 |
| **导出/分享体积控制** | — | #11031 空会话导出 19.5MB；#11091 mermaid 6MB 被扁平化进渲染器 | — | 只有 Qwen 在追——导出 HTML 嵌入了完整 Web Shell 运行时，暗示其当前架构的**依赖图治理**尚未成熟 |
| **后台/自动化场景** | #4723 `--interactive` 自定义插件下启动提示被丢弃 | #11119/#11118 daemon 回收导致通知丢失；#11015 worktree 隔离任务 | — | CLI 作为后台 agent/CI 进程运行时，其**状态持久化与进程回收语义**需要更明确的设计 |


## 4. 差异化定位分析

| 维度 | GitHub Copilot CLI | Qwen Code | Kimi Code CLI |
|------|-------------------|-----------|---------------|
| **核心用户画像** | 企业开发团队 / VS Code 桌面端重度用户 | 开源社区 / 喜欢尝鲜 nightly 的开发者 / daemon 化工作流探索者 | 使用 Kimi 模型的 Claude Code 用户 / 轻量用户 |
| **功能侧重** | GitHub 生态内嵌 + MCP 工具链 + 企业级模型策略 | Web Shell 可视化 + 自我修复 + 后台运行架构（daemon/serve） | 模型接入亲和性 + VS Code 插件体验 + 配置简易 |
| **技术路线关键词** | 与 Copilot 桌面应用共享运行时、worktree 隔离、GPT-6 Astra 等新模型快速跟进 | 每夜构建 + preview 双通道、子代理审批持久化、滚动渲染性能调优、增量式导出瘦身 | 第三方 Agent 文档兼容、环境变量配置、渲染层修复 |
| **迭代模式** | 稳定单版本 + 社区反馈驱动 bug 修复（但 PR 合入节奏放缓） | 激进双轨发布 + PR 高吞吐修复，功能迭代与稳定性并重 | 慢速维护模式，Issue 数量少、响应周期长 |
| **结构性优势** | GitHub 生态绑定深、桌面 App + CLI 联动 | 开源 + 社区透明治理，日更节奏适合快速验证 | Moonshot 模型接入场景中转化成本最低 |

一个值得注意的差异：**Copilot CLI 的问题集中在“版本升级带来的次生灾害”**（#4734、#4728），说明其主体功能已相对稳定，摩擦来自与新桌面客户端的集成复杂度；而 **Qwen Code 的问题集中在“主动架构变革中的成长阵痛”**（Web Shell 运行时嵌入、daemon 回收竞态），显示产品形态仍在大幅演进中。


## 5. 社区热度与成熟度

| 工具 | 热度评估 | 阶段判断 |
|------|----------|----------|
| **GitHub Copilot CLI** | **最活跃**：19 条活跃 Issue，单日新增约 8 条；高赞需求（👍28）已沉淀；反馈者在认真描述复现路径与影响。 | **成熟稳定期 + 生态磨合期**。核心编码能力趋于稳定，矛盾点转向桌面/CLI 生命周期管理和企业策略控制。 |
| **Qwen Code** | **修复最密集**：单日 10 个 PR 并行，10 个热点 Issue 追踪中。Issue 带 P1/P2/P3 分级、含 perf/fix/feat 多种定向，反馈质量高。 | **快速迭代期（功能爆发 + 架构演进并行）**。夜夜发版已是常态，问题呈现“边建边修”特征。社区自证了较高的 dogfooding 参与度，但产物结构尚不稳定。 |
| **Kimi Code CLI** | **最冷淡**：24h 内仅 2 条 Issue，其中 1 条讨论自今年 2 月持续至今才关闭，PR 为零。 | **早期维护期**。社区反馈基数极小，尚未形成稳定活跃的贡献者循环。 |


## 6. 值得关注的趋势信号

**① “升级即风险”成为信任破坏第一元凶，原子替换与回滚能力成为刚需**

Copilot CLI 连续出现“自动更新覆盖正在运行的 exe”（#4728）与“桌面版升级后全部 worktree 会话不可用”（#4734），Qwen Code 亦有 release 流程重复工作与超时问题（#11109）。对强调长时驻留的 AI CLI 工具，**更新机制本应是最不该出错的安全网**。企业决策者评估工具时，建议将“升级失败是否导致既有会话丢失”列入与技术能力同等权重的考察项。

**② MCP/Agent 异步边界的“取消与超时语义”尚无最佳实践**

Copilot CLI #4731 揭露了一个极具代表性的竞态：取消一个 stdio MCP 调用后，运行时立刻向同一 server 发送 `tools/list`，因 server 仍在处理被取消的任务而超时，进而**在进程生命周期内永久移除该 server 的全部工具**。代理系统中的取消不等于终止，被取消的任务仍占用资源——所有做 MCP 工具链的工具都需正视这一层语义设计，否则规模化后将不断出现“幽灵超时”类故障。

**③ UI fidelity 已成信任死角：字节流正确 ≠ 用户看到正确**

三个工具独立出现三个渲染层缺陷——Copilot CLI 的 Markdown 吞下划线（#4722）、Kimi VS Code 面板丢字（#2635）、Qwen Web Shell 的 Cmd+A 错选（#11108）。在 AI 编程工具中，用户无法直接区分“模型答错”和“界面显示错了”。**渲染层 bug 放大模型不信任感的杠杆极高**，值得工具团队将 UI 渲染纳入与核心生成链路同级别的测试覆盖。

**④ “后台/无人值守”正成为下一代 CLI 的核心战场，但谁都没完全准备好**

Qwen Code 围绕 daemon 回收丢通知（#11119）、busy 判定竞态（#11118）与 worktree 隔离（#11015）连发多 PR；Copilot CLI 则同时撞上非交互模式启动参数失效（#4723）。两者不约而同地跌进同一个深水区：**当 CLI 从“前台对话框”变成“后台 agent”，进程回收、通知投递、审批持久化的语义都需要重新发明**。这一赛道的先发者将定义未来 1-2 年 AI 编程工具的基础架构范式。

**⑤ 模型选择权正在从“自动”回归“显式”——用户开始警惕静默降级**

Copilot CLI #4732 中模型自行从旗舰切换到 mini 并清空用户 patch，Kimi 用户则要求更明确的 K2 Thinking 切换指引（#1210）。两者的共同指向是：**模型路由策略必须有用户可见性、可解释性和强制覆盖能力**。工具厂商若将“省钱/降延迟”的自动路由逻辑隐藏得太深，一旦用户感知到生成质量波动，将直接把账算到工具头上。

**⑥ 全栈渲染架构的轻量化迫在眉睫——Web 技术栈引入的依赖包袱被用户用体积投票否决**

Qwen Code 的导出 HTML 因内嵌完整 Web Shell 运行时膨胀至 19.5MB（#11031），连 mermaid（6MB）都未外链（#11091）。这是“Web 技术栈快速构建 UI”与“产物干净可用”之间的典型冲突。用户对 AI 工具产物的体积敏感度高于传统软件——**分享出去的 HTML 是产品口碑的隐形载体**，值得在架构早期就建立依赖图审计机制。

---

*报告基于 2026-09-06 GitHub 公开仓库动态整理。Copilot CLI / Qwen Code / Kimi Code 的数据分别来自对应社区日报，其余工具因无可用数据暂未纳入横向对比。*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 · 2026-09-06

## 今日速览

昨日发布 v1.0.84-1，新增 GPT-6 Astra 模型支持。社区讨论集中在**桌面端升级后会话失效 / Worktree 丢失**、**MCP 工具调用稳定性问题**以及**模型异常切换**三类高风险反馈；过去 24 小时无 PR 更新。

## 版本发布

- **v1.0.84-1**  
  新增：支持 GPT-6 Astra。  
  https://github.com/github/copilot-cli/releases

## 社区热点 Issues

本期从 19 条活跃 Issue 中挑选 10 条最值得关注：

### 1. #1857 允许用户取消或移除已排队消息
- 作者：@dorlugasigal | 评论：11 | 👍：28
- 定位：`area:input-keyboard`
- 价值：社区点赞最高需求。当 Agent 忙碌或执行 `/compact` 时，通过 `Ctrl+Q` / `Ctrl+Enter` 排队的消息无法取消，只能等待依次执行。
- 链接：https://github.com/github/copilot-cli/issues/1857

### 2. #4734 升级后所有项目会话报 “Worktree missing”
- 作者：@petrsnd | 更新：2026-09-05
- 影响：升级到 desktop 2.98.0 / runtime 1.1.15 后，所有基于 worktree 的会话（包括新建会话）都无法使用，必须手动重建 worktree。
- 链接：https://github.com/github/copilot-cli/issues/4734

### 3. #4728 自动更新重写正在运行的 copilot.exe，破坏 GitHub Copilot 桌面应用
- 作者：@doomslayer2k | 更新：2026-09-05
- 影响：在终端内运行 `copilot` 触发自动更新后，会覆盖其启动来源的 `copilot.exe`，导致桌面应用所有已有会话断开并显示 “Session unavailable”。
- 链接：https://github.com/github/copilot-cli/issues/4728

### 4. #4732 Copilot 突然切换到 GPT-5 mini 并在任务中途停止
- 作者：@yurivict | 更新：2026-09-05
- 现象：用户创建的 patch 被清空，模型自行停止；再次生成时同样中途停止。
- 链接：https://github.com/github/copilot-cli/issues/4732

### 5. #4731 对已取消 MCP 调用执行 tools/list 刷新会导致超时并永久移除工具
- 作者：@tecrogue | 更新：2026-09-05
- 定位：`area:mcp`, `area:tools`
- 关键点：一个 stdio MCP 工具调用超时取消后，运行时立刻向**同一服务器**发送 `tools/list` 刷新请求，因服务器仍被取消任务占用，刷新超时后该服务器上的工具在进程生命周期内被永久移除。
- 链接：https://github.com/github/copilot-cli/issues/4731

### 6. #4729 内置 research 子代理提示调用不存在的 github/get_me 工具
- 作者：@ayackel | 更新：2026-09-05
- 定位：`area:agents`, `area:mcp`
- 现象：research 子代理 prompt 要求先调用 `github/get_me`，但同会话 GitHub MCP server 并未暴露该工具，导致子代理反复尝试并泄漏推理过程。
- 链接：https://github.com/github/copilot-cli/issues/4729

### 7. #4723 使用本地插件自定义 Agent 时 `--interactive <prompt>` 启动提示被静默丢弃
- 作者：@floatingsidewal | 更新：2026-09-05
- 定位：`area:non-interactive`, `area:agents`, `area:plugins`
- 现象：TUI 正常启动且选中自定义 Agent，但命令行传入的起始 prompt 不会被提交。
- 链接：https://github.com/github/copilot-cli/issues/4723

### 8. #4722 以下划线开头的文本（如 `_test`）在聊天气泡中丢失
- 作者：@YiyaoZhangSGM | 更新：2026-09-05
- 定位：`area:input-keyboard`, `area:terminal-rendering`
- 原因推断：Markdown 解析未闭合的强调符导致前导 `_` 被吞掉。
- 链接：https://github.com/github/copilot-cli/issues/4722

### 9. #4721 Canvas open_canvas 参数被 CLI 损坏，疑似 JSON-RPC 序列化 Bug
- 作者：@arisng | 更新：2026-09-05
- 定位：`area:mcp`, `area:tools`
- 现象：模型调用 open_canvas 时参数被拼接上 `}{}` 后缀，变成畸形 JSON，数据被截断。
- 链接：https://github.com/github/copilot-cli/issues/4721

### 10. #4652 最新 Windows 25H2 下报告 “Sandboxing is enabled but is not supported on this host”
- 作者：@JohannesZahn | 更新：2026-09-05
- 定位：`triage` + Windows 平台
- 影响：用户使用 `--experimental --sandbox` 时 sandbox 功能不可用，官方提示需更新 Windows 支持版本。
- 链接：https://github.com/github/copilot-cli/issues/4652

## 重要 PR 进展

过去 24 小时无 PR 更新或合并。

## 功能需求趋势

从当前活跃 Issue 看，社区最关注的方向为：

- **模型支持与选型控制**：新版本适配 GPT-6 Astra 的同时，用户对模型自动切换、企业模型策略不可控表达明显焦虑（#4732、#4272）。
- **桌面应用与 CLI 的生命周期隔离**：自动更新、共享二进制文件和运行时版本升级连续造成会话不可用，用户期望 CLI 与桌面 App 集成更安全（#4734、#4728）。
- **MCP / Agent 工具链稳定性**：工具发现刷新、参数序列化错误、子代理引用了不存在的工具等，正成为规模化使用 MCP 的关键障碍（#4731、#4721、#4729）。
- **输入与终端体验**：排队消息不可取消、Ctrl+H 在 WSL2 下行为错乱、Markdown 渲染吞字符等，影响日常交互频率（#1857、#4328、#4722）。
- **非交互 / 自动化场景**：`--interactive` 在自定义插件下失效、server mode 流标记不一致，说明自动化接入仍是薄弱环节（#4723、#4677）。

## 开发者关注点

- **升级风险是当前最大信任破坏点**：自动更新覆盖被启动的 exe、桌面 App 升级后 worktree 会话全挂，开发者希望 release / update 机制有更好的回滚和原子替换策略（#4734、#4728）。
- **MCP 超时取消后状态恢复缺乏保障**：工具被永久移除、参数损坏等问题直接导致自动化流程中断（#4731、#4721）。
- **长会话稳定性不足**：存在 JavaScript heap out of memory、max_output_tokens 截断后事件丢失等问题，对长期后台使用不友好（#4725、#4733）。
- **模型行为偏移引发不信任**：模型突然切换成低配版本并中途停止，开发者需要更强的模型选择和显式控制能力（#4732）。

*数据来源：https://github.com/github/copilot-cli*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

## Kimi Code CLI 社区动态日报
**日期：2026-09-06 | 数据来源：github.com/MoonshotAI/kimi-cli**

---

### 1. 今日速览

过去 24 小时项目无新版本 Release、无新 PR 合入，社区动静主要集中在 Issue 区。两件事值得关注：一是 **#1210 第三方 Coding Agent 集成文档增强诉求被关闭**，或意味着文档迭代告一段落；二是新增 **#2635 VS Code 扩展渲染层丢字 BUG**，说明插件体验仍是用户高频碰撞点。

---

### 2. 版本发布

过去 24 小时无新版本 Release。

---

### 3. 社区热点 Issues

> 注：本期筛选窗口内活跃 Issue 数量较少（共 2 条），以下为全部条目。

#### 🔹 #1210 [已关闭] 完善「在第三方 Coding Agent 中使用」文档
- **作者**：@bosens-China  
- **创建/更新**：2026-02-23 / 2026-09-05  
- **评论**：1 | 👍 0  
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/1210  
- **内容摘要**：用户认为项目中「在 Claude Code 中可使用 tab 键切换 Kimi K2 Thinking 模型」等说明过于简略。同时指出**每次使用都需要手动 export 环境变量**不够友好，希望参考智谱文档的编排方式，提供更便捷的配置或引导。  
- **关注价值**：该诉求横跨**模型切换交互**与**环境配置简化**两个用户高频场景，且已关闭变绿，说明官方可能已采纳或正在落地相关改进，值得配置党回头验证文档更新。

#### 🔹 #2635 [开放] VS Code 扩展：流式聊天文本渲染/复制层丢失字符
- **作者**：@TserenTserenov  
- **创建/更新**：2026-09-05 / 2026-09-05  
- **评论**：0 | 👍 0  
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2635  
- **内容摘要**：在 Kimi Code 的 VS Code 扩展聊天面板中，**渲染出的助手消息偶尔会缺失部分字符**；但通过会话底层 Wire 日志核对后确认模型输出字节流完整，问题定位在**前端渲染或面板文本复制链路**。  
- **关注价值**：这类「模型没错、UI 吃了字」的缺陷最容易损耗用户信任感，虽暂无评论，但对团队来说应是需要尽快定位的高优前端 Bug。

---

### 4. 重要 PR 进展

过去 24 小时内无公开 PR 创建或更新。

---

### 5. 功能需求趋势

基于当前活跃 Issue（#1210、#2635）提炼，社区关注向以下三个方向集中：

| 方向 | 热度信号 | 代表 Issue |
|------|----------|-----------|
| **第三方 Agent 集成与文档完善** | 用户主动跨产品（Claude Code）对比体验，要求补充集成说明 | #1210 |
| **配置与鉴权流程简化** | 抱怨“每次 export 变量”繁琐，期望一键式或配置文件持久化 | #1210 |
| **IDE/编辑器侧的渲染稳定性** | VS Code 面板出现内容丢失，影响阅读与复制代码 | #2635 |

长期来看，**开发者体验文档（DX Docs）**和**编辑器扩展健壮性**仍是 CLI 工具链用户最敏感的两根神经。

---

### 6. 开发者关注点

- **文档颗粒度不够**：用户希望拿到“手把手”级别、带实际按键操作的第三方 Agent 接入说明，而不是一段 TIP 提示。
- **环境变量设置费时**：每次会话都要重新执行 `export` 被普遍视为一种摩擦点；参考业界方案（如智谱 Claude 工具文档）提供 `.env` 或配置文件导入方式是呼声较高的解法。
- **产出内容必须“字字不丢”**：VS Code 端 UI 丢字虽然不影响模型真实输出，但用户会下意识怀疑模型能力，属于负向体验放大器，值得开发者高优跟进。

---

*本日报由 AI 开发工具技术分析师整理，数据抓取自 GitHub Issue/PR 公开时间线。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

## 2026-09-06 Qwen Code 社区动态日报

### 1. 今日速览

Web Shell 动态工作流可视化功能进入 preview 与 nightly 版本，配套性能优化同步推进。社区最集中的反馈围绕**导出文件体积膨胀**（空会话导出仍达 19.5MB）与**后台任务通知可靠性**两大主题，多个 P1/P2 Issue 与修复 PR 并行活跃。此外，CI 超时与资源竞争问题成为本周开发者的高频痛点，已有针对性修复在途。

### 2. 版本发布

**v0.23.1-preview.0**
- feat(web-shell)：可视化并管理动态工作流运行（PR #10594）
- perf(web-shell)：派生会话工作流项目（session workflow project）

**v0.23.0-nightly.20260905.e3d26283e6**
- 与上述 preview 变更内容一致，包含 feat 与 perf 两项 web-shell 改动

链接：[v0.23.1-preview.0](https://github.com/QwenLM/qwen-code/releases) · [v0.23.0-nightly.20260905.e3d26283e6](https://github.com/QwenLM/qwen-code/releases)

### 3. 社区热点 Issues（Top 10）

**#11119 [P1] serve：后台 shell 输出与唤醒通知在 session 运行时回收后被静默丢弃**
daemon 场景下，会话运行时回收后，后台 shell 仍在运行和产出，但所有输出与后续唤醒通知全部丢失，导致会话被卡死。涉及后台自动化路线图，评论认为这是可靠性缺口。  
→ https://github.com/QwenLM/qwen-code/issues/11119

**#11031 [P1] fix(export)：停止在每个 HTML 文件中嵌入 Web Shell 运行时**
当前 `/export html` 会把完整浏览器依赖图（React + Web Shell 运行时）复制进每个导出文件，空会话导出约 19.5MB。已有 4 条评论讨论体积问题和拆分方向。  
→ https://github.com/QwenLM/qwen-code/issues/11031

**#11091 [P2] fix(export)：mermaid（约 6MB）仍被扁平化进导出的 transcript 渲染器**
继 #9812 合并后，导出 HTML 改为外链 unpkg 渲染器并带 SRI 锁定，但 mermaid 仍被打进渲染器包。社区在追踪体积与加载性能。  
→ https://github.com/QwenLM/qwen-code/issues/11091

**#11109 [P2] release.yml 重复执行同一 run 已做过的工作，且一个 20 分钟步骤未验证任何内容**
release 工作流大量时间浪费在重复工作上，且存在“验证了虚无”的 20 分钟步骤，两次 release run 今日超时。评论区指向具体超时的 actions run 链接。  
→ https://github.com/QwenLM/qwen-code/issues/11109

**#5883 [Feature Request] 将聊天面板（输入 + 会话流）统一到 web-shell**
提议将聊天面板在 web-shell、VSCode webview 与桌面端三端标准化，已有 4 条评论、1 👍，是 Web UI 统一方向的长期提案。  
→ https://github.com/QwenLM/qwen-code/issues/5883

**#11111 [P2] feat(search)：会话搜索应匹配对话内容而不只是标题**
当前搜索只匹配 session 标题，用户找不到之前聊过的技术细节。评论提到 Codex 已经支持内容级搜索，期望对齐。  
→ https://github.com/QwenLM/qwen-code/issues/11111

**#10865 [P2] perf(web-shell)：会话工作流投影每次渲染被计算三次**
每次渲染重复计算相同投影并重建索引，索引设计上是只建一次。属于 #8389 的后续，评论关注渲染性能退化。  
→ https://github.com/QwenLM/qwen-code/issues/10865

**#11118 [P2] fix(serve)：正在做 cron / goal / monitor / 历史写入的 session 永远无法被回收**
子进程上报两种不同的“busy”定义，导致持有集合判定与回收集合不一致，部分活跃会话永远不被回收。涉及后台自动化路线图。  
→ https://github.com/QwenLM/qwen-code/issues/11118

**#11100 [P2] fix(web-shell)：transcript 入口仍携带 daemon hook 运行时**
新增的只读 transcript 入口（#11038）仍通过组件依赖图引入 `daemon-react-sdk`，与移除 Web Shell 运行时的目标存在偏差。  
→ https://github.com/QwenLM/qwen-code/issues/11100

**#11108 [P3] fix(web-shell)：Cmd+A 在 composer 中全选整页而非输入内容**
光标在输入框时 Cmd+A/Ctrl+A 会选中整个页面文本，影响 Web Shell 用户复制体验，dogfooding 发现。  
→ https://github.com/QwenLM/qwen-code/issues/11108

### 4. 重要 PR 进展（Top 10）

**#11133 fix(core)：延迟后台任务通知，而非静默丢弃**
会话运行时回收（generation swap）会清空各 Registry 的通知回调。此 PR 将期间产生的通知延迟到重新绑定后再投递，修复静默丢失问题。  
→ https://github.com/QwenLM/qwen-code/pull/11133

**#11132 fix(core)：session 重新绑定时补发丢弃的后台 shell 通知**
后台 shell 到达终态（completed / failed / cancelled）时若无监听者，通知会被消费并丢失。此 PR 将其延迟到监听者就绪后重放。  
→ https://github.com/QwenLM/qwen-code/pull/11132

**#11015 feat(channels)：实现命名会话工作树重置（Part 4B）**
`/clear`、`/new`、`/reset` 现在可用于选定的 worktree 隔离任务，保留 daemon 认证的工作树、文件与分支的同时开启全新对话，附设计文档。  
→ https://github.com/QwenLM/qwen-code/pull/11015

**#11106 fix(test)：为 scripts 套件的安静主机预算配置独立 knob**
release 验证通道的 `Quality Checks (Scripts)` 因两个基于安静机器测得的 wall-clock 预算超时而失败。此 PR 移除这两个预算，统一收敛到已有的 `QWEN_SCRIPTS_TEST_TIMEOUT_MS`。  
→ https://github.com/QwenLM/qwen-code/pull/11106

**#11093 feat：添加持久化 focus 模式，获得更安静的终端记录**
新增可选 `/focus`：隐藏推理行、汇总工具组（含失败），复用 Ctrl+O 展开详情。默认关闭，跨重启持久化。  
→ https://github.com/QwenLM/qwen-code/pull/11093

**#10043 perf(cli)：降低虚拟化历史滚动延迟**
滚动调度改为 leading-edge 且 deadline-aware：首次 wheel/drag 立即应用，16ms 窗口内的后续更新仍合并，超预算渲染后不再等待整帧后才更新，减少可感知延迟。  
→ https://github.com/QwenLM/qwen-code/pull/10043

**#11070 fix(acp)：跨 cold resume 保持审批模式**
使 daemon 会话的审批模式在 ACP 子进程回收与冷加载/恢复后仍然持久化，含 Plan 会话返回模式的恢复。  
→ https://github.com/QwenLM/qwen-code/pull/11070

**#11083 fix(serve)：workspace 为 home 时，从用户 scope 读取 channel 设置**
当 daemon 的工作目录恰为 home 时，channel 配置对管理 API 和 Web Shell 变为不可见。此 PR 增加 workspace scope 失效时回退到用户配置 scope 的逻辑。  
→ https://github.com/QwenLM/qwen-code/pull/11083

**#11139 fix：API leader 与本地 worker 使用独立凭据**
让原生 subagents 与 Agent Team 在 API-backed leader + 本地 worker（含 Ollama）混搭时更安全，并补充配置文档。  
→ https://github.com/QwenLM/qwen-code/pull/11139

**#11134 fix(ci)：重试一次瞬时性的全绿 macOS E2E shard 死亡**
为 macOS E2E 增加与 Linux sandbox:none 相同的预算受限重试逻辑，shard 命令移入 `run_shard()` 函数，失败时在剩余预算内最多执行两次。  
→ https://github.com/QwenLM/qwen-code/pull/11134

### 5. 功能需求趋势

- **Web Shell 统一与导出瘦身**：多个 Issue 指向将聊天

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*