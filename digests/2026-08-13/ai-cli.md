# AI CLI 工具社区动态日报 2026-08-13

> 生成时间: 2026-08-12 22:35 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-08-13）

## 1. 生态全景

当前 AI CLI 工具已从"单机对话式编码助手"演进为**可远程控制、可自托管、支持插件生态与自动化工作流的基础设施组件**。各工具迭代节奏差异明显：Gemini CLI 和 Qwen Code 保持高频发布，Claude Code 聚焦企业级能力补全，Kimi Code 则处于功能讨论与稳定性加固阶段。社区反馈的重心正从"能否生成代码"转向**结果可信度、状态上报准确性、上下文持久化与安全合规**等生产级问题。整体上，工具间的功能趋同（记忆、子代理、安全、评估）与差异化定位（企业集成、桌面端、云服务）并存，行业正处于从"可用"向"可靠"过渡的关键期。

## 2. 各工具活跃度对比

> 注：OpenAI Codex、GitHub Copilot CLI、OpenCode 在本次数据源中无更新信息，暂列为"无数据"。

| 工具 | Issues 动态 | PR 动态 | Release 情况 |
|---|---|---|---|
| **Claude Code** | 2 个核心开放 bug（插件市场）；1 个高热度已关闭 issue（金融域名屏蔽）；一批 6 月陈旧 issue 被集中处理 | 未单独披露 PR 数 | **v2.1.229**：Remote Control 会话恢复、自托管 Runner Hook、SSE 心跳 |
| **OpenAI Codex** | 无数据 | 无数据 | 无数据 |
| **Gemini CLI** | 10 个热点 Issues（5 个 P1 Bug、3 个功能/内部改进、2 个安全/隐私） | 至少 1 个功能 PR（#28730）；另有多个安全修复 PR 落地 | **v0.56.0-nightly**：修复模型容量误报、新增本地报告命令 |
| **GitHub Copilot CLI** | 无数据 | 无数据 | 无数据 |
| **Kimi Code CLI** | 近 24h 仅 1 条 issue 更新（#1283，35 评论）；整体讨论热度集中在记忆系统 | 2 个 PR（#2449、#2324）更新，聚焦稳定性 | 无新版本 |
| **OpenCode** | 无数据 | 无数据 | 无数据 |
| **Qwen Code** | 3 个热点 issues：自动记忆召回 RFC、长任务失效、图片加载崩溃 | 3 个 PR（#8931、#8856、#8914）合入；另有桌面端多个 PR | CLI **v0.21.11-preview.0** + 桌面端 **v0.2.0/v0.2.1**，节奏密集 |

## 3. 共同关注的功能方向

| 方向 | 涉及工具 | 具体诉求 |
|---|---|---|
| **跨会话记忆与上下文持久化** | Kimi Code（#1283）、Qwen Code（#7040）、Gemini CLI（#26522/#26525）、Claude Code（1M 上下文选项消失） | Kimi 和 Qwen 均提出"自动记忆"机制，Gemin 面临记忆低效重试与隐私脱敏问题，Claude 用户则在抱怨长上下文选项不一致。**"记住项目上下文"正成为各工具的标配需求。** |
| **子代理/Agent 执行可靠性** | Gemini CLI（#22323/#21409/#25166/#21983）、Qwen Code（#8963）、Kimi Code（#2324 子进程处理） | 共性痛点：子代理挂起、max turns 误报成功、Shell 命令卡死、长任务自动失效。**状态上报不真实直接破坏用户对 Agent 的信任。** |
| **安全、合规与隐私** | Gemini CLI（变量注入绕过、SSRF、MCP 配置损坏）、Claude Code（金融域名被屏蔽） | Gemini 集中修复安全漏洞，Claude 则因服务端域名屏蔽阻断合法金融自动化。安全能力正从"加分项"变为"准入门槛"。 |
| **插件/Skill/扩展市场成熟度** | Claude Code（插件市场更新 bug）、Gemini CLI（#21968 skills 使用率低） | Claude 插件版本管理有缺陷，Gemini 用户抱怨模型不主动调用 skill。**扩展生态的"最后一公里"（更新、自动触发）尚未跑通。** |

## 4. 差异化定位分析

- **Claude Code**：最明显的**企业级/基础设施导向**。v2.1.229 主打 Remote Control 会话恢复、自托管 Runner Hook、Gateway SSE 心跳，明显面向需要远程接入、私有化部署和网络稳定的组织用户。其插件市场与 1M 上下文选项问题也体现出"大组织、长会话、多扩展"的使用场景。
- **Gemini CLI**：**Agent 自动化与质量工程导向**。大量 issue 围绕子代理行为、评估体系（组件级评估、本地报告）和安全加固，社区讨论深入到协议层与内部机制。适合对 Agent 自主执行、评测可观测性和安全敏感的高级开发者。
- **Kimi Code CLI**：定位**轻量日常编码助手**。无新版本、无大量 bug 列表，但社区对跨会话记忆系统持续高热（35 评论，5.5 个月未平），说明产品主功能已相对稳定，正处于"补齐体验短板"阶段。
- **Qwen Code**：**多端协同与云原生导向**。CLI 与桌面端并行发布，功能集中在 web-shell 导航安全、会话生命周期、共享会话目录，与阿里云/DSW 等基础设施联动明显。发布节奏快，但社区 issue 数量相对不多，处于快速迭代追赶期。

## 5. 社区热度与成熟度

- **Gemini CLI 社区最活跃、讨论最深入**：10 个热点 issue 覆盖 P1 Bug、EPIC 设计、安全隐私，且维护者积极介入（标记 `maintainer only`、`need-retesting`）。多个 issue 持续半年仍被跟踪，说明社区参与度和维护响应均处于较高水平，但也反映部分顽疾未解。
- **Claude Code 传播热度高但 issue 治理略显粗放**：域名屏蔽事件获得 12 评论/7👍，显示出很强的行业共鸣；但插件市场 bug 长期无官方回应，且 6 月旧 issue 被集中关闭/翻新，暗示官方在收敛 issue 池，社区跟进体验可能受影响。
- **Qwen Code 处于快速迭代期，社区反馈密度略低**：一天内多次发布（CLI + 桌面端共 3 个版本），但热点 issue 评论数仅 10 左右，话题集中在自身功能缺陷而非生态讨论，属于"开发快于社区积累"。
- **Kimi Code 热度集中但活跃度平稳**：一个记忆系统 issue 独占 35 评论，其余更新寥寥。项目或许尚在成长初期，社区声量主要被单一痛点吸引。

## 6. 值得关注的趋势信号

1. **"跨会话记忆"将从增强功能升级为必备能力**  
   Kimi、Qwen、Gemini 不约而同围绕记忆展开讨论，且已细化到召回时序、脱敏、重试策略等实现层。对开发者而言，选择工具时需关注其记忆机制的**可控性（手动/自动）与隐私安全**，否则项目上下文越积越多，泄露与混淆风险也随之放大。

2. **Agent 的执行结果可信度危机**  
   Gemini 出现 "MAX_TURNS 误报 GOAL 成功"、子代理挂起但状态正常等严重问题，Qwen 长任务失效，Kimi 子进程异常——**"假成功"比"失败"更具破坏性**。开发者在设计自动化流水线时，应为 AI CLI 增加独立的"结果验证层"，不能仅信任工具返回的状态码。

3. **安全与合规已成为社区的第一梯队话题**  
   Gemini 的安全修复（变量注入、SSRF、MCP 数据损坏）与 Claude 的金融域名屏蔽事件表明，**AI CLI 已进入真实的生产业务流**，不再是本机玩具。企业采用前应评估工具的沙箱隔离、域名策略、敏感信息脱敏能力，并关注官方是否提供白名单/绕过机制。

4. **自托管/远程控制让 AI CLI 走向"基础设施化"**  
   Claude Code 的 Runner Hook、SSE 心跳、会话恢复，以及 Gemini 的本地评估报告，说明这些工具正被集成进 CI/CD、远程开发环境和企业网关。这意味着 AI CLI 的选型不再只看代码生成质量，还要看**可运维性：日志、心跳、断连恢复、评估可观测性**。

5. **插件/Skill 生态的"生命周期管理"成为下一个竞争焦点**  
   Claude 插件市场无法正确更新版本，Gemini 模型不主动调用 skill——前者是机制缺陷，后者是智能程度问题。开发者在使用插件时，应留意工具的版本锁定和回滚机制，并准备好通过显式指令兜底，等待生态的自动触发能力成熟。

6. **评估体系开始走向专业化**  
   Gemini 新增组件级评估 EPIC 和本地报告命令，Qwen 明确区分非生产冒烟版本与 SWE 分数。这说明**"AI CLI 的能力不能只靠感觉，需要可复现的度量"**。对技术决策者，可优先选择在评测基础设施上持续投入的工具，以便内部做 A/B 选型与质量验收。

---

**一句话总结**：AI CLI 正从"能写代码"进入"可放心生产使用"的竞赛阶段——谁能先解决记忆可靠性、状态真实性、安全合规和生态治理，谁就将在企业市场占据先机。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

## 1. 热门 Skills 排行

以下 PR 均为 Open 状态，按社区评论活跃度排序（数据源中按评论数降序）。

- **#1298 — skill-creator 评估链路修复**  
  功能：修复 `run_eval.py` 在所有场景下误报 `recall=0%` 的问题，使 skill 描述优化循环不再基于噪声运行；同时修复 Windows 流读取、触发检测与并行 worker 兼容性。  
  社区热点：该问题被 #556 等 10+ 独立复现，是 skill 开发流程稳定性的最大障碍。  
  [GitHub Link](https://github.com/anthropics/skills/pull/1298)

- **#514 — document-typography 技能**  
  功能：对 AI 生成的文档做排版质量检查，防止孤字换行、段落标题滞留页底和编号错位等 typographic 问题。  
  社区热点：AI 生成文档普遍存在“用户不主动关注但影响专业度”的排版缺陷，此技能补足了质量验收环节。  
  [GitHub Link](https://github.com/anthropics/skills/pull/514)

- **#486 — ODT 技能**  
  功能：创建、填充、读取或转换 OpenDocument 格式（.odt/.ods），支持解析为 HTML，适配 LibreOffice 和 ISO 标准场景。  
  社区热点：填补了官方技能在开放文档格式上的空白，受到政府/企业合规场景关注。  
  [GitHub Link](https://github.com/anthropics/skills/pull/486)

- **#210 — frontend-design 技能改进**  
  功能：重写前端设计技能，使每条指令更清晰、可执行，并保证在单次对话内可被 Claude 遵循。  
  社区热点：社区对“技能可操作性”和“指令具体粒度”的讨论集中体现于此。  
  [GitHub Link](https://github.com/anthropics/skills/pull/210)

- **#83 — skill-quality-analyzer 与 skill-security-analyzer**  
  功能：新增两个元技能，分别从结构/文档、安全性等维度评估 Claude Skill 本身的质量。  
  社区热点：标志着社区开始认真对待 skill 生态的自我治理与安全审查。  
  [GitHub Link](https://github.com/anthropics/skills/pull/83)

- **#1367 — self-audit 技能（v1.3.0）**  
  功能：交付前先做机械文件验证，再按损害严重度进行四维推理审计；不限定技术栈，可通用接入。  
  社区热点：与 #1385 “推理质量门”提案呼应，反映对 AI 输出可靠性的强烈需求。  
  [GitHub Link](https://github.com/anthropics/skills/pull/1367)

- **#723 — testing-patterns 技能**  
  功能：覆盖测试哲学（Testing Trophy）、单元测试 AAA、React 组件测试、测试命名与边界用例等全栈测试模式。  
  社区热点：软件测试自动化是长期高频需求，此技能试图将最佳实践沉淀为可执行指令。  
  [GitHub Link](https://github.com/anthropics/skills/pull/723)

- **#568 — ServiceNow 平台技能**  
  功能：覆盖 ITSM、ITOM、ITAM/SAM Pro、FSM、HRSD、SPM、CSDM、IntegrationHub 等企业级模块。  
  社区热点：企业平台类技能被视为扩展 Claude Code 场景的重要方向，该 PR 近期仍在更新（08-12）。  
  [GitHub Link](https://github.com/anthropics/skills/pull/568)

---

## 2. 社区需求趋势

从 Issues 讨论热度与赞数来看，社区关注点集中于以下方向：

- **安全与信任边界**：`#492`（43 评论）指出社区技能被放入 `anthropic/` 命名空间，可能让用户误以为是官方技能，产生越权风险。社区强烈期待官方规范 namespace 使用并提供安全审计。
  [Issue #492](https://github.com/anthropics/skills/issues/492)

- **组织级共享与安装**：`#228`（16 评论，👍 8）吐槽当前只能通过“下载文件 → 手动上传”的方式共享技能，希望支持 org-wide 技能库或直接分享链接。
  [Issue #228](https://github.com/anthropics/skills/issues/228)

- **skill-creator 工具链稳定性**：`#556`（12 评论，👍 7）和 `#1169` 等集中反馈 `run_eval.py` 触发率恒为 0%，导致描述优化完全失效；另有 `#62` 报告技能文件丢失问题。社区希望官方优先修复核心开发工具。
  [Issue #556](https://github.com/anthropics/skills/issues/556)

- **上下文效率与记忆**：`#1487` 指出 claude-api skill 一次注入约 156k tokens，直接撑爆上下文；`#1329` 提出 compact-memory 符号化记法；`#189` 报告插件重复安装导致上下文浪费。轻量、可组合的技能设计成为显性需求。
  [Issue #1487](https://github.com/anthropics/skills/issues/1487)

- **新技能方向涌现**：agent-governance 治理模式（#412）、推理质量门流水线（#1385）、MCP 化技能 API（#16）、AWS Bedrock 兼容（#29）等提案，反映社区正从“单点文档技能”转向“系统级治理与互操作”。
  [Issue #412](https://github.com/anthropics/skills/issues/412) | [Issue #1385](https://github.com/anthropics/skills/issues/1385)

---

## 3. 高潜力待合并 Skills

以下 PR 讨论热度高、功能完整，且近期仍有更新，可能较快落地：

- **#568 ServiceNow 平台技能**  
  最近更新至 2026-08-12，覆盖企业级 ServiceNow 全模块，是当前最活跃的开放 PR 之一。  
  [GitHub Link](https://github.com/anthropics/skills/pull/568)

- **#525 Pyxel 复古游戏开发技能**  
  基于 pyxel-mcp，适配 Python 写 8-bit/像素风游戏，最近更新 07-15，社区反响积极。  
  [GitHub Link](https://github.com/anthropics/skills/pull/525)

- **#1367 self-audit 技能**  
  与 #1385 质量门提案互相印证，v1.3.0 版本持续迭代，是 AI 输出可靠性方向的代表性技能。  
  [GitHub Link](https://github.com/anthropics/skills/pull/1367)

- **#723 testing-patterns 技能**  
  全栈测试模式全覆盖，已沉淀近一个月，合并可期。

---

# Claude Code 社区动态日报 — 2026-08-13

## 今日速览

v2.1.229 发布，补上 Remote Control 会话恢复、自托管 Runner 的 Hook 支持与 SSE 心跳。但社区真正关注的依然是两个老问题：**Opus 4.8 的 1M 上下文选项在多个平台消失**，以及**插件市场的更新与添加流程存在缺陷**（目前仅有的两个开放 bug 均在此）。此外，一批 6 月的陈旧 issue 在 8 月 12 日被集中关闭/翻新，其中成本相关反馈值得留意。

## 版本发布 — v2.1.229

- 为 `claude remote-control --continue` 补充文档，支持恢复最近的 Remote Control 会话。
- 自托管 Runner 会话新增服务端提供的 Claude Code Hook 支持，与托管环境行为对齐。
- Gateway 流式响应增加 SSE keepalive 心跳，改善长时间流式传输的断连检测。

## 社区热点 Issues

1. **[已关闭] Claude-in-Chrome 服务端域名屏蔽破坏金融业务自动化**（12 评论 / 👍7）
   用户报告 Wells Fargo、Charles Schwab 等银行/券商域名被 `api.anthropic.com/api/web/domain_info` 服务端屏蔽，合法自动化流程被阻断。社区讨论热度高，期望 Anthropic 提供企业白名单或绕过机制。  
   https://github.com/anthropics/claude-code/issues/40173

2. **[开放] 插件市场更新拉取新版本但不更新 installed_plugins.json**（3 评论）
   `claude plugin marketplace update` 会把新版本下载到缓存目录，但 `installPath` 和 `version` 字段不更新，新会话仍用旧版本。这直接影响所有插件开发者的迭代流程，目前无官方回应。  
   https://github.com/anthropics/claude-code/issues/76882

3

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-13

## 1. 今日速览

昨日发布 v0.56.0-nightly 版本，重点修复了虚假的模型容量耗尽误报问题，并为评估体系新增本地报告命令。社区层面，多个 P1 级 Agent 可靠性 Bug 持续发酵（子代理挂起、MAX_TURNS 误报成功、Shell 命令卡死）成为开发者吐槽焦点。安全修复呈集中态势：变量注入绕过、SSRF、MCP 配置损坏导致的数据丢失均有对应 PR 落地。

## 2. 版本发布

### v0.56.0-nightly.20260812.g5024443c7
- **fix(core,cli)**：修复虚假的模型容量耗尽（false model capacity exhaustion）误报；修正核心配额查找时的模型映射错误（[#28730](https://github.com/google-gemini/gemini-cli/pull/28730)）
- **feat(evals)**：新增本地报告（local report）命令并提供开发者文档

## 3. 社区热点 Issues（10 个）

### 🔥 高优先级 Bug

**1. Subagent MAX_TURNS 被误报为 GOAL 成功** — [#22323](https://github.com/google-gemini/gemini-cli/issues/22323)
优先级 P1 | 12 条评论 | 被标记 `maintainer only` 与 `need-retesting`
`codebase_investigator` 子代理在尚未做任何分析时即触发最大轮次限制，却返回 `status: "success"` 和 `Termination Reason: "GOAL"`，严重误导用户对执行结果的判断。社区认为这属于结果可信度的核心缺陷。

**2. Generalist Agent 无限期挂起** — [#21409](https://github.com/google-gemini/gemini-cli/issues/21409)
优先级 P1 | 8 条评论 | 8 👍
即使执行简单操作（如创建文件夹），只要委托给 generalist agent 就永久挂起，用户最长等待 1 小时无响应。反馈者确认"禁用子代理后问题消失"。该 Issue 已持续半年仍被 bot 标记 `need-retesting`。

**3. Shell 命令执行完成后卡在 "Waiting input"** — [#25166](https://github.com/google-gemini/gemini-cli/issues/25166)
优先级 P1 | 4 条评论 | 3 👍
极简 CLI 命令执行完毕后，终端仍显示命令处于活动状态并提示"等待用户输入"，且不会自动恢复。社区认为这严重破坏非交互式自动化场景。

**4. Browser 子代理在 Wayland 下失败** — [#21983](https://github.com/google-gemini/gemini-cli/issues/21983)
优先级 P1 | 4 条评论 | 1 👍 | 标记 `agent/browser`
浏览器子代理在 Wayland 会话中直接失败，Termination Reason 显示 GOAL 但实际未完成任务。Linux 桌面用户受影响较大，期待协议层适配。

**5. get-shit-done 输出钩子导致崩溃** — [#22186](https://github.com/google-gemini/gemini-cli/issues/22186)
优先级 P1 | 3 条评论
输出摘要接近完成时 Gemini CLI 反复崩溃，疑似钩子与渲染器存在生命周期竞争。目前仅 `maintainer only` 可见细节。

### 📌 功能与内部改进

**6. 评估体系升级：组件级评估（EPIC）** — [#24353](https://github.com/google-gemini/gemini-cli/issues/24353)
优先级 P1 | 7 条评论 | 标记 `aiq/eval_infra`
在现有 76 个行为评估测试基础上建立组件级评测体系，涵盖 6 个受支持的 Gemini 模型。说明官方正在系统化质量保障。

**7. 探索 AST 感知的文件读取与代码库映射** — [#22745](https://github.com/google-gemini/gemini-cli/issues/22745)
优先级 P2 | 7 条评论
EPIC 级调研：评估 AST 感知工具能否精准读取方法边界、降低 Token 噪声、减少对齐读取造成的多轮往返。文件中点名 tilth 和 glyph 作为候选实现。

**8. Gemini 对 skills 和 sub-agents 的使用率不足** — [#21968](https://github.com/google-gemini/gemini-cli/issues/21968)
优先级 P2 | 6 条评论
用户反馈即使已配置 gradle、git 等自定义 skill，模型在高度相关场景下仍不会主动调用，只有显式指令才生效。这直击 Agent 工具调用的智能程度痛点。

### 🔒 安全与隐私

**9. Auto Memory 对低信号会话无限重试** — [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)
优先级 P2 | 5 条评论
内存提取代理跳过低价值会话后，该会话不会被标记为已处理，导致无限期反复出现在候选列表中，造成资源浪费与索引膨胀。

**10. Auto Memory 需确定性脱敏并减少日志输出** — [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)
优先级 P2 | 4 条评论
本地会话记录在送入模型前未做确定性脱敏，而是依赖模型"自觉"对提示词中的内容进行脱敏，存在隐私泄露风险；同时服务日志可能

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

## Kimi Code CLI 社区动态日报  
**日期：2026-08-13**  
**数据来源：[MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)**

---

### 今日速览

- 近 24 小时内无新版本发布，项目处于功能讨论与稳定性加固阶段。  
- 特性需求 #1283（跨会话记忆系统）持续发酵，距今已累计 35 条评论，仍是社区讨论热度最高的议题。  
- 两项由社区开发者提交的稳定性修复 PR（#2449、#2324）于 8 月 12 日同步更新，聚焦输出格式与子进程异常处理。

---

### 版本发布

过去 24 小时内无新版本发布。

---

### 社区热点 Issues

> 数据源中，近 24 小时内更新的 Issue 共 1 条，见下方详细解读。

#### #1283 [OPEN] [enhancement] Feature Request: Memory System - Persistent context across sessions  
- **作者**：@CatKang  
- **创建时间**：2026-02-27 ｜ **最近更新**：2026-08-12  
- **评论数**：35  
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/1283  

**核心诉求**：为 Kimi Code CLI 引入一套**跨会话持久化记忆系统**，让 AI 在多次会话中记住项目上下文、编码模式与用户偏好。方案包含两种记忆形态：

- **自动记忆**：会话过程中由 AI 自动沉淀关键信息（类似管理型笔记）；  
- **手动记忆**：用户通过自定义指令，强制 AI 持久化某些规则或约定。  

**为什么值得关注**：该 Issue 已持续活跃约 5 个半月，评论数达到 35 条，说明“AI 频繁遗忘上下文”是社区中的普遍痛点。无论是大型代码库演进、长周期 Bug 追踪，还是工程

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 · 2026-08-13

## 今日速览

昨日发布节奏密集：CLI 预览版 `v0.21.11-preview.0` 与桌面端 `desktop-v0.2.0/v0.2.1` 先后上线，重点修复了 Web Shell 会话导航安全与桌面端会话生命周期管理。社区侧，自动记忆召回 RFC（#7040）持续高热，长任务自动运行失效（#8963）与图片加载崩溃回归（#8957）成为最受关注的两大痛点。

---

## 版本发布

### v0.21.11-preview.0（CLI 预览版）
- **fix(web-shell)**：强制提示安全的会话导航，避免切换会话时误取消或重放源提示词（PR #8931）。
- **chore(serve)**：增加会话延续准入日志，提升可观测性。

### desktop-v0.2.0 / v0.2.1（桌面端）
- **refactor(serve)**：默认项目记忆改为工作区范围（PR #8856）。
- **feat(telemetry)**：对齐会话生命周期埋点。
- **fix(web-shell)**：稳定转录历史分页（PR #8914）。
- **feat(web-shell)**：支持共享会话目录。

另：`dsw-eas-smoke-20260812` 为非生产基础设施冒烟测试版本，不对外发布 SWE 分数。

---

## 社区热点 Issues

### 1. #7040 RFC：可靠的自动记忆召回 — 时序、质量与遥测 💬10
[github.com/QwenLM/qwen-code/issues/7040](https

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*