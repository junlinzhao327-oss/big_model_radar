# AI CLI 工具社区动态日报 2026-08-25

> 生成时间: 2026-08-24 22:36 UTC | 覆盖工具: 7 个

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



---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告

> 数据来源：github.com/anthropics/skills | 数据截止：2026-08-25

---

## 1. 热门 Skills 排行

以下为社区评论/讨论热度最高的 8 个 PR（当前均为 Open 状态）：

### ① skill-creator：评估链路 0% 召回率修复（#1298）
- **功能**：修复 `run_eval.py` 在所有测试查询下均报告 `recall=0%` 的核心缺陷，使描述优化循环不再对着噪音调参；同时修复 Windows 流读取、触发器检测与并行 worker 问题。
- **讨论热点**：该问题已在 #556 中被 10+ 用户独立复现，直接影响 skill-creator 的自动优化功能，是当前社区最关注的质量缺陷。
- **状态**：Open | [查看 PR](https://github.com/anthropics/skills/pull/1298)

### ② document-typography：AI 生成文档排版质量检查（#514）
- **功能**：新增 `document-typography` skill，针对 AI 生成文档中常见的孤儿行、孤儿段落标题、编号错位等排版问题进行质量控制。
- **讨论热点**：社区普遍认为这些问题普遍存在于 Claude 生成的所有文档中，但用户极少主动要求排版优化，属于"虽不显眼却高频"的痛点。
- **状态**：Open | [查看 PR](https://github.com/anthropics/skills/pull/514)

### ③ Hivemind：零成本多智能体编排（#1628）
- **功能**：新增 `hivemind` skill —— 将机械性工作委托给运行免费模型的 headless opencode worker，Claude Code 保留规划、审查、合并的决策权。
- **讨论热点**：核心观点是"昂贵模型的上下文才是稀缺资源"，社区围绕多智能体协作成本与上下文压缩展开讨论，8 月底提交后迅速升温。
- **状态**：Open | [查看 PR](https://github.com/anthropics/skills/pull/1628)

### ④ testing-patterns：全栈测试模式技能（#723）
- **功能**：新增 `testing-patterns` skill，覆盖测试哲学（Testing Trophy 模型）、单元测试（AAA 模式）、React 组件测试（Testing Library）等完整测试栈。
- **讨论热点**：社区关注"该测什么 vs 不该测什么"的边界，以及将测试策略沉淀为可复用 skill 的可行性。
- **状态**：Open | [查看 PR](https://github.com/anthropics/skills/pull/723)

### ⑤ ODT：OpenDocument 文档创建与转换（#486）
- **功能**：新增 `odt` skill，支持创建、填充、读取 OpenDocument 格式文件（.odt/.ods），并可将 ODT 解析为 HTML。
- **讨论热点**：围绕 LibreOffice/开源格式在办公场景中的需求，以及 ISO 标准格式与 docx 的互操作问题。
- **状态**：Open | [查看 PR](https://github.com/anthropics/skills/pull/486)

### ⑥ ServiceNow：企业级平台综合技能（#568）
- **功能**：新增 `servicenow` skill，覆盖 ITSM、ITOM、ITAM/SAM Pro、FSM、HRSD、CSDM、IntegrationHub 等广泛平台领域，定位为"平台助手"而非单一脚本工具。
- **讨论热点**：企业用户关注 ServiceNow 技能如何与 Claude Code 现有工作流结合，以及技能的知识体量是否过大。
- **状态**：Open | [查看 PR](https://github.com/anthropics/skills/pull/568)

### ⑦ self-audit：交付前机械验证 + 四维推理质检（#1367）
- **功能**：新增 `self-audit` skill —— 先机械验证所有输出文件是否真实存在，再按损害严重性优先级对推理结果进行四维审计。
- **讨论热点**：该设计独立于技术栈和模型，社区认为它补齐了"AI 输出交付前最后一公里"的质检空白，与 #1385 推理质量门控提案呼应。
- **状态**：Open | [查看 PR](https://github.com/anthropics/skills/pull/1367)

### ⑧ pdf：大小写敏感文件引用修复（#538）
- **功能**：修复 `skills/pdf/SKILL.md` 中 8 处大小写不匹配的文件引用（`REFERENCE.md` → `reference.md` 等），解决 Linux 等大小写敏感系统上的文件引用失效问题。
- **讨论热点**：问题虽小，但直接导致 pdf skill 在常见环境下不可用，评论活跃度高，属于等待合并的低风险修复。
- **状态**：Open | [查看 PR](https://github.com/anthropics/skills/pull/538)

---

## 2. 社区需求趋势

从 Issues 看，社区最期待/最关切的 Skill 方向集中在以下五类：

### 安全与信任边界治理（🔥 关注度最高）
- #492：社区技能被放到 `anthropic/` 命名空间下分发，模拟官方技能造成信任边界滥用，用户可能向非官方技能授予高权限。
- #1175：在 SKILL.md 中直接编写 SharePoint 访问控制逻辑时的安全性与上下文溢出担忧。
- **趋势**：社区需要官方提供技能包签名验证、来源标注或安全审查机制。

### 上下文窗口效率
- #1487：`claude-api` skill 单次调用即注入约 156k tokens，直接耗尽上下文窗口。
- #189：`document-skills` 与 `example-skills` 插件包含相同技能，导致重复加载、浪费上下文。
- **趋势**：技能需要更克制的资源加载策略，并按需注入而非全量注入。

### 企业级 Skill 共享与分发
- #228：要求支持组织内直接共享技能，而非手动下载 .skill 文件再通过聊天工具传输。
- #29：如何在 AWS Bedrock 环境中使用 Skills。
- **趋势**：企业部署场景需要组织级技能库、权限管理及云平台兼容。

### 代理治理与输出质量保障
- #412：提议 agent-governance 技能，涵盖策略执行、威胁检测、信任评分与审计跟踪。
- #1385：推理质量门控管道 —— 任务前校准 → 对抗审查 → 交付验证。
- **趋势**：社区正从"功能型技能"转向"治理型技能"，关注 AI 代理的安全与可靠性。

### Agent 记忆与状态压缩
- #1329：compact-memory 技能提案，用符号化记法压缩长时运行 agent 的持久记忆，减少上下文占用。
- **趋势**：长会话场景下，技能需具备记忆压缩与状态管理能力。

---

## 3. 高潜力待合并 Skills

以下 PR 评论活跃、改动边界清晰或功能完整，有较大概率在近期合并：

| PR | 说明 | 潜力原因 |
|---|---|---|
| [#538](https://github.com/anthropics/skills/pull/538) | pdf skill 大小写引用修复 | 8 处明确错误、改动零风险，直接影响可用性 |
| [#539](https://

---

# Claude Code 社区动态日报（2026-08-25）

## 今日速览

过去 24 小时无新版本发布，但社区出现一个紧急回归：**v2.1.242 在 Linux x64 上每次启动即段错误**（含 `--version`），v2.1.241 正常，严重性极高。功能需求方面，**跨机器 Multi-Agent 协作协议**（#28300）以 43 条评论持续霸榜，成为社区最受关注的方向。与此同时，桌面端稳定性问题（Intel 集显崩溃、排序失效）与 MCP 生态相关的 bug 也在持续发酵。

## 社区热点 Issues

### 1. [P0 回归] v2.1.242 Linux x64 启动即段错误（含 `--version`）
**#89334**｜`bug, has repro, platform:linux, area:packaging, regression`｜创建 2026-08-24｜👍 3
```text
v2.1.242 (native install, Linux x64) 每次调用都 segfault，崩溃发生在 pre-main。
根因：v2.1.242 首次将捆绑的 mimalloc 导出为 versioned glibc allocator 符号，
其 free 无 NULL 检查，而 glibc newlocale 在 pre-main 阶段会调用 free(NULL)。
v2.1.241 及更早版本不受影响。
```
**重点关注**：这是今天最关键的回归，直接影响所有 Linux x64 原生安装用户，建议开发团队立即排查并热修复。链接：https://github.com/anthropics/claude-code/issues/89334

### 2. [呼声最高] 跨机器 Multi-Agent 协作（Agent-to-Agent 协议）
**#28300**｜`enhancement, area:agents`｜创建 2026-02-24｜评论 43
```text
[FEATURE] Multi-agent collaboration across machines (Agent-to-Agent protocol)
问题陈述：现代软件工程需要多智能体跨机器协作，当前缺少标准化的
Agent-to-Agent 通信协议。
```
**重点关注**：评论数 43 条稳居第一，虽然 👍 为 0 但讨论热度极高，说明社区对多 Agent 编排有强烈诉求。链接：https://github.com/anthropics/claude-code/issues/28300

### 3. [高赞] 桌面端排序失效：按项目分组后"按最近"无效
**#56060**｜`area:desktop`｜创建 2026-05-04｜评论 15｜👍 13
```text
Claude Desktop App 中，当 Group by: Project 开启时，Sort by: Recency 完全失效，
会话列表不会按最近活动排序。
```
**重点关注**：13 个 👍 是本轮最高赞 bug，直接影响桌面端日常使用体验。链接：https://github.com/anthropics/claude-code/issues/56060

### 4. 桌面端 MSIX 在 Intel 集显上崩溃
**#83028**｜`bug, area:desktop`｜创建 2026-08-01｜评论 13
```text
使用浏览器面板时崩溃，可复现，无 workaround，影响 Intel 集成 GPU 用户。
```
**重点关注**：13 条评论说明受影响用户较多，且无临时规避方案，属于桌面端稳定性短板。链接：https://github.com/anthropics/claude-code/issues/83028

### 5. [已关闭] Max20x 计划每周限额异常跳变
**#69430**｜`bug, platform:macos, area:cost`｜创建 2026-06-18｜评论 8｜👍 6
```text
一小时内在几乎没有使用的情况下从 ~50% 跳到 100%，用户质疑限额计算逻辑。
```
**重点关注**：6 个 👍 说明成本/限额类问题有较高共鸣，虽已关闭但值得关注后续修复是否彻底。链接：https://github.com/anthropics/claude-code/issues/69430

### 6. 同仓库多个会话静默切换彼此的 Branch
**#60295**｜`enhancement, platform:macos, area:core`｜创建 2026-05-18｜评论 5
```text
同一工作目录运行多个 Claude Code 会话时，一个会话 git checkout 会静默影响
另一个会话的工作树，且后者无法感知其 branch 心智模型已过期。
```
**重点关注**：这是多会话协作场景下的严重一致性问题，与 #28300 的多 Agent 需求形成呼应。链接：https://github.com/anthropics/claude-code/issues/60295

### 7. Subagent 结果路由错误
**#69212**｜`bug, platform:linux, area:agents`｜创建 2026-06-17｜评论 4｜👍 3
```text
Teammate agent 派生的 subagent，其结果没有返回给派生它的 teammate，
而是直接路由到了 root agent，行为与预期不符。
```
**重点关注**：3 个 👍 表明这是多 Agent 场景下的明确 bug，影响任务分发和

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报
**2026-08-25**

---

## 今日速览

今日 Codex 生态聚焦于 **认证稳定性** 与 **Multi-Agent 架构收敛**：macOS/Windows 端多个会话恢复导致登录失效的 Issue 持续发酵，其中 #39162 评论达 51 条，成为社区最关注问题；同时 PR 侧密集合并了一批围绕 **子代理所有权、Guardian 审查范围、Windows 沙箱修复** 的内部改动。版本方面，`rust-v0.150.0-alpha.8` 与 `rust-v0.149.1` 相继发布，后者为主要补丁版本。

---

## 版本发布

### rust-v0.149.1（补丁版）
- **变更内容**：未随附明确说明，完整变更见 [Changelog](https://github.com/openai/codex/compare/rust-v0.149.0...rust-v0.149.1)
- **建议**：若你正在使用 `0.149.x` 系列，建议升级以获取修复

### rust-v0.150.0-alpha.8（预发布）
- **变更内容**：暂无详细说明

### rust-v0.149.0-alpha.4.3（预发布）
- **变更内容**：暂无详细说明

> 小提示：两个 alpha 版本均为预发布通道，生产环境请关注正式版 `rust-v0.149.1`。

---

## 社区热点 Issues（Top 10）

### 1. [macOS] 打开现有会话导致 ChatGPT 认证失效并跳转登录页
- **Issue**: [#39162](https://github.com/openai/codex/issues/39162)
- **标签**: `bug` / `auth` / `app`
- **数据**: 51 条评论 | 31 👍 | 更新于 8/24
- **分析**: 在 macOS 26.814.41407 上，打开历史会话即触发 ChatGPT 认证失效。已知最后可用版本为 26.810.52044，属回归问题，影响面广，社区讨论激烈。

### 2. [macOS] 桌面端无法恢复远程控制/CLI 线程：`already has an active writer`
- **Issue**: [#37403](https://github.com/openai/codex/issues/37403)
- **标签**: `bug` / `app` / `remote`
- **数据**: 30 条评论 | 27 👍 | 更新于 8/24
- **分析**: 8月7日更新后，通过手机远程恢复 Mac 上的 CLI 线程失败。该问题波及远程办公场景，与 #39162 同属会话恢复链路缺陷。

### 3. `gpt-5.6-luna` 被错误标记为 MultiAgent V1，V2 拒绝执行
- **Issue**: [#35097](https://github.com/openai/codex/issues/35097)
- **标签**: `bug` / `CLI` / `subagent`
- **数据**: 29 条评论 | 51 👍 | 更新于 8/24
- **分析**: 51 个 👍 为今日最高。模型元数据与 Multi-Agent 版本不匹配导致 `spawn_agent` 拒绝调用。核心矛盾是 V1/V2 的模型能力标记体系尚未统一。

### 4. 分页历史丢弃合法的扁平 rollout 记录并重用序号
- **Issue**: [#35746](https://github.com/openai/codex/issues/35746)
- **标签**: `bug` / `CLI` / `session`
- **数据**: 25 条评论 | 1 👍 | 更新于 8/24
- **分析**: `RolloutLine` 解码在分页场景下不一致，可能造成历史记录错乱。虽 👍 不多，但属数据完整性关键缺陷。

### 5. [Windows][WSL] 集成终端在 PTY 启动前静默失败
- **Issue**: [#37104](https://github.com/openai/codex/issues/37104)
- **标签**: `bug` / `windows-os` / `app` / `Papercuts 2026`
- **数据**: 19 条评论 | 9 👍 | 更新于 8/24
- **分析**: 底部和侧边面板无法打开，整个终端功能在 WSL 环境下失效，属于 Windows 用户的阻塞性问题。

### 6. 应用内近期线程历史消失，但 CLI 中仍存在
- **Issue**: [#17354](https://github.com/openai/codex/issues/17354)
- **标签**: `bug` / `context` / `app`
- **数据**: 14 条评论 | 7 👍 | 更新于 8/24
- **分析**: 已有 4 个月未被修复的历史遗留问题。桌面端与 CLI 数据不同步，用户复产成本高。

### 7. 自动压缩：将压缩能力暴露给 Agent
- **Issue**: [#21777](https://github.com/openai/codex/issues/21777)
- **标签**: `enhancement` / `context`
- **数据**: 9 条评论 | 9 👍 | 更新于 8/24
- **分析**: 功能需求，希望 Agent 在上下文窗口快满时主动触发压缩，而非被动等待系统压缩。涉及体验与 token 成本的平衡。

### 8. 工作区终端无法启动：`setup refresh had errors`
- **Issue**: [#39841](https://github.com/openai/codex/issues/39841)
- **标签**: `bug` / `windows-os` / `tool-calls` / `app`
- **数据**: 7 条评论 | 0 👍 | 更新于 8/24
- **分析**: Windows 11 上工作区终端完全不可用。新问题，但暂无社区热度。

### 9. Windows Chrome/Computer Use 浏览器控制全面失败
- **Issue**: [#40048](https://github.com/openai/codex/issues/40048)
- **标签**: `bug` / `windows-os` / `computer-use` / `browser`
- **数据**: 7 条评论 | 0 👍 | 更新于 8/24
- **分析**: `about:blank` 页面、JS 内核超时、URL 检测失败，Windows 上浏览器自动化功能不可用。涉及 Computer Use 核心能力。

### 10. Codex Desktop 更新丢失项目/侧边栏会话历史映射
- **Issue**: [#26157](https://github.com/openai/codex/issues/26157)
- **标签**: `bug` / `app` / `session`
- **数据**: 7 条评论 | 1 👍 | 更新于 8/24
- **分析**: 更新后本地会话文件仍在，但 UI 无法正确关联项目与侧边栏。与 #17354、#33771 同属会话元数据持久化问题。

---

## 重要 PR 进展（Top 10）

> 以下 PR 多数由 `copyberry[bot]` 提交，均于 8/24 合并或关闭，显示官方正密集推进内部架构收敛。

### 1. 添加根 Turn ID 至 Turn 与工具分析
- **PR**: [#40486](https://github.com/openai/codex/pull/40486)
- **说明**: 为分析事件增加 `root_turn_id`，用于将子代理活动关联到顶层 Turn，同时避免 steering 场景下的旧关联歧义。对可观测性体系有实质改进。

### 2. 子环境中的凭据代理别名
- **PR**: [#40484](https://github.com/openai/codex/pull/40484)
- **说明**: 即使父环境的规范 provider 变量在子环境中被过滤，也能发现并代理继承的凭据；同时支持替换嵌在较长子环境值中的匹配凭据。安全与兼容性并重。

### 3. 支持 Amazon Bedrock 托管 AWS 访问密钥
- **PR**: [#40481](https://github.com/openai/codex/pull/40481)
- **说明**: 新增实验性 `amazonBedrockAccessKeys` app-server 登录流，可将凭据持久化至配置的 auth store，并用于 SigV4 签名请求。对 AWS 用户是重要增量。

### 4. 新增 Computer-Use 专用 Guardian V2 审查范围
- **PR**: [#40480](https://github.com/openai/codex/pull/40480)
- **说明**: 通过 `computer_use_only` 范围，将异步分类和快速审批限定在浏览器与 Computer Use REPL 工具，其他工具继续走同步审批路径。安全策略更精细化。

### 5. 子代理重载改道父代理
- **PR**: [#40477](https://github.com/openai/codex/pull/40477)
- **说明**: Multi-Agent V2 子代理恢复时改由父代理路由，避免直接用调用方设置重建子代理，保证权限与配置的一致性。

### 6. 更新 Windows 沙箱 ACL 时请求读取控制
- **PR**: [#40475](https://github.com/openai/codex/pull/40475)
- **说明**: 修复 `SetSecurityInfo` 因目录句柄仅有 `WRITE_DAC` 而被拒绝的问题，附带 Windows 回归测试。

### 7. 扩展支持结构化完整审批审查
- **PR**: [#40472](https://github.com/openai/codex/pull/40472)
- **说明**: 将审批审查拆分为快速决策路径（现有证据）与完整审查路径（结构化审查），后者可获 action 证据、对话历史、线程元数据等输入，为第三方扩展提供更强能力。

### 8. 支持终端内渲染 Markdown 链接为可点击标签
- **PR**: [#40471](https://github.com/openai/codex/pull/40471)
- **说明**: 在识别支持的终端中，将链接标签渲染为青色下划线，隐藏重复的目标 URL；未知终端、multiplexer 或非终端输出中保留可见地址。

### 9. 网络代理功能配置新增凭据代理
- **PR**: [#40466](https://github.com/openai/codex/pull/40466)
- **说明**: 新增 `features.network_proxy.credential_broker` 配置项，并保护相关变量不受项目配置覆盖，防止 Broker 启用与 provider 上下文变量被恶意篡改。

### 10. 记录 Guardian 分类器输入截断指标
- **PR**: [#40465](https://github.com/openai/codex/pull/40465)
- **说明**: 针对 Guardian v2 的 actions、transcript 条目和图片记录截断与遗漏情况，输出 `codex.guardian_v2.classification.truncation` 计数器及字节直方图，提升安全透明的可观测性。

---

## 功能需求趋势

### 🔥 认证与会话持久性（最热）
- 多个 Issue 指向相同痛区：**更新后认证失效**（#39162、#39218、#40267）、**会话恢复不稳定**（#37403）。社区对登录状态和线程恢复的可靠性要求已从“建议”变为“强烈要求”。
- 新增的 `amazonBedrockAccessKeys` 登录流（#40481）说明官方在认证体系上正扩展更多服务商兼容。

### 🔥 Multi-Agent V2 生态
- 模型被错误标记为 V1 导致 V2 拒绝执行（#35097）说明 **V1/V2 的模型能力元数据需统一**。
- 多个 PR（#40477、#40464、#40449、#40437、#40486）围绕“子代理由父代理全权控制”进行集中修复，所有权模型正在收紧。

### 🔥 Windows 平台体验
- WSL 终端静默失败（#37104）、工作区终端不可用（#39841）、浏览器控制失效（#40048）、内核崩溃（#40119）——Windows 已是高频问题平台，社区期待更多的 Windows 专属测试覆盖。

### 📈 沙箱与安全策略精细化
- “Computer-Use 专用 Guardian 范围”（#40480）与“结构化审批审查”（#40472）表明安全体系正从粗粒度向场景化策略演进。
- 多个 Windows ACL 修复（#40475、#40441）补上了沙箱权限控制的地基。

### 📈 Agent 自主性增强
- “自动压缩暴露给 Agent”（#21777）与“Markdown 链接可点击”（#40471）显示 Agent 想要更多“自理”能力和终端交互体验改进。

---

## 开发者关注点

### 1. 认证可靠性：核心痛点
> “打开现有会话导致退出登录”在 macOS 与 Windows 上反复出现，且 `refresh_token_invalidated` 后重新登录只能在很短时间内保持有效（#40267、#39162、#39218）。

- **社区要求**：OAuth 刷新令牌必须持久化到位，且更新/恢复流程不得触发 token 重置。

### 2. 会话历史与项目映射的持久化
- 多个 Issue 指向一个共通症状：**UI 侧历史消失，底层数据仍在**（#17354、#26157、#33771、#35135）。
- **开发者痛点**：项目与聊天的映射在更新/重建后无法恢复，导致上下文断层，返工成本高。

### 3. 更新回归频发
- 多个“已知最后可用版本”明确列出的案例：26.810 → 26.814 之间出现认证回归（#39162）、8/7 更新破坏远程恢复（#37403）、8/19 合并版更新破坏桌面 UI（#39513）。
- **社区期待**：更完善的自动化升级回归测试，尤其是 Windows 与 WSL 组合。

### 4. Multi-Agent 元数据与版本兼容
- `gpt-5.6-luna` 被错误打标导致 V2 拒绝执行（#35097），开发者希望官方提供 **模型版本与 Multi-Agent 版本兼容性矩阵**。
- 若你正使用 Multi-Agent V2，请确认模型中未被标记为 V1。

### 5. Hooks 与扩展的可观测性
- `PostToolUse` 没有失败信号字段（#34289）、MCP Stop hook 在 MCP server 缺失时 fail-open（#39858）——插件作者需要更完整的回调语义和错误传递机制。

---

> **编辑备注**：数据截至 2026-08-24 23:59 UTC，统计范围为过去

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-08-25**  
**数据来源：** github.com/google-gemini/gemini-cli

---

## 今日速览

今日社区焦点集中在子代理（Subagent）可靠性、自动记忆（Auto Memory）安全性和 Git 环境变量处理上。一个 P1 级 Bug 被曝光：子代理在达到 MAX_TURNS 后被误报为 GOAL 成功，掩盖了真实中断，引发社区共鸣。与此同时，多项安全修复 PR 聚焦 Git 环境变量清理，文档完善类 PR 也集中出现。

---

## 版本发布

**v0.56.0-nightly.20260824.g5411f113c**

过去 24 小时发布了新的 nightly 版本。完整变更日志详见：[compare v0.56.0-nightly.20260823...v0.56.0-nightly.20260824](https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260823.g5411f113c...v0.56.0-nightly.20260824.g5411f113c)

---

## 社区热点 Issues

### 1. 子代理在 MAX_TURNS 后被误报为 GOAL 成功，掩盖中断 ⚠️
- **#22323** | P1 / bug | 13 条评论 | 👍 2
- **重要性：** `codebase_investigator` 子代理在达到最大轮次限制后仍返回 `status: "success"` 且 `Termination Reason: "GOAL"`，而实际上

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-08-25）

> 数据来源：github.com/github/copilot-cli  
> 统计窗口：2026-08-24 更新内容

## 1. 今日速览

过去 24 小时仅发布 1 个补丁版本 `v1.0.81-9`，主要改进 `/model` 选择器中的模型数据保留警告。社区讨论热度集中在 MCP OAuth 兼容性、交互模式工具权限、以及会话可靠性问题；其中“CLI 持续出现 400 错误”和“交互模式工具白名单”两个 Issue 评论与反应数最高。

## 2. 版本发布

### v1.0.81-9
- **改进**：在 `/model` 选择器中展示模型数据保留警告，并附带相关文档链接。
- 影响：帮助用户在选择模型时更明确地了解数据保留策略。

链接：https://github.com/github/copilot-cli/releases

## 3. 社区热点 Issues

以下挑选过去 24 小时更新中最值得关注的 10 个 Issue：

### #1274 CLI 持续收到 400 错误（invalid request body）
- 作者：@unusualbob | 评论：27 | 👍：11 | 状态：Open
- 摘要：用户反馈最近约 95% 的 diff 文件代码审查请求返回 400 错误，原因可能在服务端校验或 CLI 构造请求方式。
- 为什么重要：高频 400 错误直接影响核心代码审查工作流，社区关注度最高。

链接：https://github.com/github/copilot-cli/issues/1274

### #1973 请求：交互模式工具白名单
- 作者：@Dicer-J | 评论：12 | 👍：27 | 状态：Open
- 摘要：交互模式每个工具调用都需要手动批准，包括 `grep`、`cat`、`git log` 等只读操作；而 `/allow-all` 又会放行危险操作。社区希望有工具级白名单。
- 为什么重要：开发者对“安全与效率平衡”的需求强烈，👍 数量全场最高。

链接：https://github.com/github/copilot-cli/issues/1973

### #4490 Atlassian MCP OAuth 在 1.0.80 中回归
- 作者：@ChandrasekarCK | 评论：5 | 👍：0 | 状态：Closed
- 摘要：Atlassian MCP 的 OAuth 认证失败，报错为 `MCPOAuthError: Incompatible authorization server`（RFC 8414 §3.3）。
- 为什么重要：1.0.78 可用、1.0.80 回归，且后续仍有用户报告同类问题（见 #4584）。

链接：https://github.com/github/copilot-cli/issues/4490

### #4421 MCP initialize 握手的 60 秒超时不可配置且无重试
- 作者：@devinj-msft | 评论：2 | 👍：0 | 状态：Open
- 摘要：MCP 初始化握手固定 60 秒超时，超时后该 MCP server 在整个会话中不再拉起；npx 启动的 stdio server 约 29% 会失败。
- 为什么重要：MCP 生态下常见初始化慢的 server 会直接不可用，属于可靠性设计缺陷。

链接：https://github.com/github/copilot-cli/issues/4421

### #4582 MCP OAuth authorize 请求缺少 `scope` 参数（Entra ID）
- 作者：@mikemassa84 | 评论：2 | 👍：0 | 状态：Open
- 摘要：对使用静态 `oauthClientId` 的 Entra ID MCP server 登录时，authorize 请求未携带 `scope`，导致 `AADSTS900144`。
- 为什么重要：新出现的认证兼容性问题，影响企业 Entra ID 用户。

链接：https://github.com/github/copilot-cli/issues/4582

### #4566 Agent 反复确认“已处理”但不实际执行工具
- 作者：@kloudkon | 评论：2 | 👍：1 | 状态：Open
- 摘要：Agent 会回复确认收到任务，但不会调用任何工具，导致任务无法推进。
- 为什么重要：这是 Agent 行为正确性问题，会让用户感觉模型“空转”。

链接：https://github.com/github/copilot-cli/issues/4566

### #4568 `--cloud` owner 选择器挂起、 reconnect 崩溃、轮询 429
- 作者：@haflidif | 评论：1 | 👍：0 | 状态：Open
- 摘要：`copilot --cloud` 无仓库上下文时卡在 `Loading available owners...`；有仓库上下文时任务停留在 `session.requested` 直到超时，并伴随 429。
- 为什么重要：Cloud 模式在当前版本中基本不可用，影响远程开发场景。

链接：https://github.com/github/copilot-cli/issues/4568

### #3255 异常退出残留 `inuse.<pid>.lock` 锁文件
- 作者：@shachaf-ashkenazi | 评论：1 | 👍：0 | 状态：Open
- 摘要：SIGKILL、崩溃等非正常退出会残留锁文件，导致后续恢复会话失败。
- 为什么重要：长期存在的会话状态管理问题，影响用户重启工作流。

链接：https://github.com/github/copilot-cli/issues/3255

### #4572 后台压缩丢失并行 GPT 工具结果并导致 HTTP 400
- 作者：@koboldul | 评论：1 | 👍：0 | 状态：Open
- 摘要：长上下文 `gpt-5.6-sol` 会话在自动压缩后报 `400 No tool output found for function call`，工具实际已执行但结果被压缩丢弃。
- 为什么重要：上下文压缩是长会话关键能力，数据丢失会导致任务中断。

链接：https://github.com/github/copilot-cli/issues/4572

### #4588 非 Anthropic 模型未启用 MCP 工具搜索（tool deferral），空 prompt 消耗 21k tokens
- 作者：@ArlindNocaj | 评论：0 | 👍：0 | 状态：Open
- 摘要：MCP tool deferral 仅对 Claude 模型生效，OpenAI、Gemini、Grok 等模型每轮都携带全部工具 schema；一个 “hi” 请求消耗 21.6k 输入 token。
- 为什么重要：成本和性能问题突出，直接影响多模型用户的日常使用。

链接：https://github.com/github/copilot-cli/issues/4588

## 4. 重要 PR 进展

过去 24 小时仅更新 1 条 PR，且并无可合并的功能代码：

### #4573 Rename README.md to README.mdmain
- 作者：@phuongnam467 | 创建：2026-08-23 | 更新：2026-08-24 | 状态：Open
- 摘要：该 PR 仅将 `README.md` 重命名为 `README.mdmain`，疑似误操作或无效改动，无实际功能意义。
- 链接：https://github.com/github/copilot-cli/pull/4573

> 说明：在统计窗口内没有其他 PR 提交或更新，因此无更多 PR 可评估。

## 5. 功能需求趋势

从近期 Issue 中可以看出社区最关注的几个功能方向：

- **交互模式粒度权限控制**：希望在 `/allow-all` 之外增加只读工具白名单、按工具授权，而非每次弹窗批准或全量放行（#1973）。
- **会话管理增强**：`/ask` 多轮对话、`/fork` 在新终端中打开、支持 CLI 级 `--fork` 等，多次被提出（#4577、#4578、#4579、#4580）。
- **Token 成本可视化**：用户希望在状态栏显示 raw token 数量，并希望 MCP 工具定义能够按需延迟加载，减少空 prompt 的 token 消耗（#4588、#4589）。
- **模型能力扩展**：支持 PDF 上传分析、生成图片资产（图标、favicon、OG 图）等非代码输入输出（#4581、#4583）。
- **MCP 兼容性**：修复 OAuth、初始化超时、参数模板等问题，让 MCP server 能稳定接入更多企业 IdP 和启动方式（#4421、#4582、#4239）。

## 6. 开发者关注点

- **MCP OAuth 是企业用户的核心痛点**：Atlassian、Entra ID、agentgateway、GitHub Enterprise 均出现认证失败，且不同版本间存在回归问题（#4490、#4582、#4584、#4408）。
- **长会话可靠性不足**：后台压缩丢失工具结果、锁文件残留、extension hook processor 被 dispose、断线重连崩溃等问题频繁出现，严重影响日常使用（#3255、#4572、#4568、#4590）。
- **交互模式安全与效率矛盾**：只读操作也需要手动授权，而 `/allow-all` 风险过高；用户需要更细粒度的安全模型（#1973）。
- **Agent 行为不可控**：出现 Agent 只确认不执行工具、空转的情况，需要更严格的工具调用协议（#4566）。
- **Windows 平台插件安装冲突**：VS Code 运行时会锁定插件文件，导致 `copilot plugin install/update` 失败，影响 Windows 开发者体验（#4570）。
- **本地会话被远程 origin 验证阻断**：`git fetch` 失败或 SSH remote 无法验证时，甚至无法创建本地会话，被用户视为“项目完全不可用”（#4585）。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-08-25）

> 数据快照基于 GitHub `MoonshotAI/kimi-cli` 仓库实时数据。当前统计窗口（过去 24 小时）内仓库活跃度较低，无版本发布，社区讨论集中在计费链路与编辑安全性两个方向。

## 1. 今日速览

- 过去 24 小时**无新版本发布**，仓库处于常规迭代期。
- 社区争议焦点在 **Issue #1994**：用户反映 K2.6 思维链导致 token 消耗过快，并对订阅用量的计算口径产生质疑。
- 唯一活跃 PR **#2595** 针对非 UTF-8 文件编辑时的数据损坏风险提出修复，正在等待评审。

## 2. 版本发布

过去 24 小时无新版本 Release，CLI 最新功能特性请参考上一期日报。

## 3. 社区热点 Issues

> 本轮统计窗口内，符合"过去 24 小时内更新"条件的 Issue 仅有 **1 条**，不足以进行十选排序，故只列出实际活跃条目。

### #1994 [OPEN] kimiCode 用量计算有问题

- **作者** : @wanghonghust
- **创建** : 2026-04-22 | **更新** : 2026-08-24
- **评论** : 8 | **👍** : 7
- **链接** : https://github.com/MoonshotAI/kimi-cli/issues/1994

**为什么重要：**  
用量计费直接关系到订阅用户的核心体验。该用户称 2 个任务就消耗完 2 小时额度，"订阅会员 2 小时只能问 2 次"。用户认为官方文档表述是"按 API 请求次数"计费（每 5 小时约 300-1200 次请求），但实际 CLI 按 token 消耗计费，K2.6 较长的思维链使 token 快速耗尽，导致预期与实际的严重偏差。

**社区反应：**  
8 条评论、7 个赞说明这不是孤例。讨论焦点集中于：

- K2.6 思维链的 token 消耗是否超出合理预期
- 订阅页面的宣传口径是否与 CLI 实际计费模式一致
- 希望提供用量明细的实时查询面板，而不是额度耗尽后被动感知

## 4. 重要 PR 进展

> 本轮统计窗口内，处于活跃状态的 PR 仅有 **1 条**，故只列出实际条目。

### #2595 [OPEN] fix(StrReplaceFile): refuse to edit files that are not valid UTF-8

- **作者** : @shoemoney
- **创建** : 2026-08-06 | **更新** : 2026-08-24
- **评论** : 0 | **👍** : 0
- **链接** : https://github.com/MoonshotAI/kimi-cli/pull/2595

**功能/修复内容：**  
AI 编辑文件时常用的 `StrReplaceFile` 工具当前使用 `errors="replace"` 对全文件进行 UTF-8 解码。这意味着文件中任何非 UTF-8 字节（即使远离编辑区域）都会被替换为 U+FFFD 替换字符，并在回写时永久破坏原始数据。

该 PR 修复了 #2591，方案是在执行编辑前先校验文件是否为合法 UTF-8，若不合法则拒绝编辑并明确报错，避免静默损坏二进制或非 UTF-8 编码文件。

**意义：**  
对处理多语言环境、页面编码不规范的项目或二进制资源文件的开发者来说，这是一次重要的防数据损坏加固。目前 PR 暂无评论，处于早期评审阶段。

## 5. 功能需求趋势

基于当前活跃 Issue 的讨论，社区最关注的功能方向如下：

| 方向 | 具体诉求 | 来源 |
|------|----------|------|
| 计费透明度 | 在 CLI 内提供实时的 token/额度消耗明细；对齐订阅说明与后台计费口径 | #1994 |
| 长思维链成本控制 | 针对 K2.6 提供"精简推理"模式或全局最大 token 预算上限 | #1994 |
| 错误操作可逆性 | 编辑工具在对非 UTF-8 文件进行改动前应做安全校验，避免不可逆损坏 | PR #2595 关联讨论 |

## 6. 开发者关注点

- **痛点：** token 消耗速度快于预期，复杂推理任务下"2 小时额度仅够 2 次问答"，性价比感知低。
- **困惑：** 官方宣传中按"API 请求次数/并发"的表述与 CLI 实际按 token 计费的逻辑不一致，导致用户对计费机制产生误解。
- **高频呼吁：** 请求在产品侧增加明确的"当前会话预计消耗 token"预估提示，并支持对思维链长度的手动限制（如关闭深度思考/极速回答模式）。

---
*本日报由 AI 编程工具观测系统自动生成，数据截止 2026-08-25 00:00（UTC+8）。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-25

## 今日速览

今日 OpenCode 发布补丁版本 **v1.18.22**，主要修复设备登录链接与 OpenAI 兼容提供商参数兼容性问题。社区方面，网络错误（`network_error`）类报告集中爆发，尤其是 **Ox Alpha Free** 免费模型稳定性引发大量用户反馈；同时 **MCP Apps 支持**（👍50）与 **一次性会话（Ephemeral Sessions）** 成为最受期待的新功能方向。

---

## 版本发布

### v1.18.22
**发布链接**：https://github.com/anomalyco/opencode/releases

本次为补丁版本，包含 3 项修复：

- **移除过时营销信息**：清理了 OpenCode Go 首月折扣相关文案，避免误导用户
- **修复设备登录链接**：解决服务器返回相对验证 URL 或使用 base path 时登录链接无法打开的问题
- **修复 `textVerbosity` 兼容性**：不再向不支持该参数的 OpenAI 兼容提供商发送此字段

---

## 社区热点 Issues（Top 10）

### 1. 网络错误集中爆发：`network_error` 成高频词
- **#44528**：`[OPEN] Bug Report, network error` — 19 条评论
  Windows 10 用户反馈 v1.18.21 在数天未使用后启动即报网络错误，Opencode Go 与 Ollama Cloud 均受影响。
  https://github.com/anomalyco/opencode/issues/44528

  同类问题还包括 #44328、#44379、#44689、#44742 等多条报告，指向 **Ox Alpha Free 与 Console 提供商** 的上游不稳定。

### 2. MCP Apps 支持：社区最高赞功能请求（👍50）
- **#10884**：`[OPEN] [FEATURE]: Add Support for MCP Apps in the desktop app` — 12 条评论
  随着 MCP 规范 v2026-01-26 趋于稳定，用户强烈希望 OpenCode 桌面端原生支持 MCP Apps。50 个 👍 表明这是当前社区最迫切的功能需求。
  https://github.com/anomalyco/opencode/issues/10884

### 3. `opencode run` 一次性会话设计讨论（👍15）
- **#4489**：`[CLOSED] [FEATURE]: Ephemeral one-off sessions for opencode run` — 14 条评论
  社区成员 @kamilchm 主动提出愿参与实现：当前 `opencode run` 每次都会持久化完整会话，希望支持不落盘的临时会话。15 个 👍 说明该需求受到广泛认同，设计讨论已相当深入。
  https://github.com/anomalyco/opencode/issues/4489

### 4. TUI 侧边栏 “Modified Files” 整体消失（👍14）
- **#30877**：`[OPEN] [Bug] v1.16.0: TUI sidebar "Modified Files" section completely hidden` — 11 条评论
  路径截断修复后引入回归，未提交文件在 TUI 右侧边栏完全不可见，而非简单的截断问题。14 个 👍 显示受影响用户较多。
  https://github.com/anomalyco/opencode/issues/30877

### 5. 持久化会话记忆：跨会话上下文连续（14 条评论）
- **#16077**：`[OPEN] [FEATURE] Persistent Session Memory` — 14 条评论，👍3
  用户希望 OpenCode 启动时能从本地文件加载历史对话上下文，使 CLI AI 助手具备跨会话记忆能力。与 #4489（一次性会话）互补，反映出社区对会话生命周期管理的高度关注。
  https://github.com/anomalyco/opencode/issues/16077

### 6. GitHub Action 在新仓库上失败：OIDC sub 格式变更（👍11）
- **#37823**：`[CLOSED] GitHub action fails on repos created after 2026-07-15` — 6 条评论
  2026-07-15 之后创建的 GitHub 仓库因 OIDC `sub` 格式改为不可变 ID，导致 Action 报 `p.rest` 未定义错误。影响所有新仓库的自动化流程，11 个 👍 表明关注度高。
  https://github.com/anomalyco/opencode/issues/37823

### 7. Kimi K3 模型选择后立即报错（👍6）
- **#37815**：`[OPEN] [Bug] Error from provider (Console Go): Upstream request failed — Kimi K3` — 7 条评论
  Kimi K3 出现在模型列表中但选择后即抛上游请求失败，Console Go 上其他模型均正常。该问题已持续一个多月仍未解决，社区耐心正在消耗。
  https://github.com/anomalyco/opencode/issues/37815

### 8. Ox Alpha Free 免费模型不稳定：同一会话内持续报错
- **#44379**：`[OPEN] Provider finish_reason: network_error with Ox Alpha Free (unlimited)` — 6 条评论，👍4
  用户反馈 `ox-alpha-free` 在正常使用中反复弹出红色 `network_error` 横幅，且同一会话内持续存在，只能开新会话临时绕过。
  https://github.com/anomalyco/opencode/issues/44379

### 9. 模型 ID 含 `/` 时解析失败：NVIDIA NIM 模型不可用
- **#44799**：`[OPEN] [Bug] Model resolution fails when the model ID itself contains "/"` — 1 条评论
  新发现的高价值 bug：当模型 ID 本身含斜杠（如 NVIDIA NIM 的 `nvidia/nemotron-...`），模型注册与解析逻辑会失效，甚至提示“找不到模型”时给出的建议 ID 与用户输入完全一致。
  https://github.com/anomalyco/opencode/issues/44799

### 10. 2.0 插件 API：事件订阅从未触发（beta）
- **#44788**：`[OPEN] [2.0] plugins: event.subscribe delivers no events` — 2 条评论
  Beta 频道 0.0.0-beta-18050 版本中，V2 插件 API 的 `ctx.event.subscribe` 注册后收不到任何事件，`ctx.session.hook("context")` 也无法将上下文注入模型提示词。对依赖插件生态的开发者影响较大。
  https://github.com/anomalyco/opencode/issues/44788

---

## 重要 PR 进展（Top 10）

### 1. 修复 TUI 侧边栏 Modified Files 回归（关联 #30877）
- **#44796**：`[OPEN] fix(opencode): restore TUI sidebar modified-files diff`
  重构 `Session.diff` 使其聚合每条用户消息的 turn diff，而非生成全量快照，从而恢复侧边栏的修改文件展示。
  https://github.com/anomalyco/opencode/pull/44796

### 2. 修复 reasoning item ID 缺失导致的流式响应异常
- **#44794**：`[OPEN] fix(ai): recover missing reasoning item ids`
  为缺失 ID 的 reasoning item 分配内部合成标识，并在流式各阶段复用；当提供方后续下发真实 ID 时无缝切换，合成 ID 不会泄漏到 provider 元数据。
  https://github.com/anomalyco/opencode/pull/44794

### 3. 新增 partial JSON 解析器
- **#44792**：`[OPEN] feat(ai): add partial JSON parser`
  引入内部 partial JSON 解析器，支持不完整字符串、数字、集合与字面量解析，基于 Effect Schema 做严格与实际修复解码。将提升流式响应中 JSON 片段的容错能力。
  https://github.com/anomalyco/opencode/pull/44792

### 4. 忽略未知 Gemini 响应部分
- **#44745**：`[CLOSED] fix(ai): ignore unknown Gemini response parts`
  对入站 Gemini 响应中无法识别 handler 的 part 做透明忽略，同时保持对 null 容错字段的兼容，避免新字段导致下游解析崩溃。
  https://github.com/anomalyco/opencode/pull/44745

### 5. 支持 workspace 相对路径的

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*