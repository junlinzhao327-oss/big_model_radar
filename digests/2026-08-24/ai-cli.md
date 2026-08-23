# AI CLI 工具社区动态日报 2026-08-24

> 生成时间: 2026-08-23 22:36 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-08-24）

> 数据来源：各工具 GitHub 社区日报；OpenAI Codex、Gemini CLI 本期未提供动态数据，不纳入横向对比。

---

## 1. 生态全景

本期可见 AI CLI 工具已进入**“功能快速迭代 + 稳定性问题集中暴露”**阶段：Claude Code、GitHub Copilot CLI、Qwen Code 同日均有 Release 或 nightly 更新，OpenCode 则有密集的 bug 修复 PR。社区不再只关心“能跑通 Demo”，而是更关注**模型行为可控性、token 成本治理、跨会话记忆、多代理编排稳定性**等生产级问题。同时，Windows 平台兼容性、插件安全边界、配额透明度成为多工具共有的信任短板。整体上，AI CLI 正在从“单次对话式编码助手”演进为“可编排、可扩展、有状态”的 Agent 工作台。

---

## 2. 各工具活跃度对比

| 工具 | Issues（今日收录） | PR（今日收录） | Release 情况 |
|---|---|---|---|
| Claude Code | 10 条（另有 50 条活跃/历史 issue 池） | 1 | v2.1.241（维护版） |
| GitHub Copilot CLI | 3+ 条（原文截断，含 #2306、#4535、#4572） | 1 | v1.0.81-8 |
| Kimi Code CLI | 3 条（2 条有效，1 条空/关闭） | 2 | 无 |
| OpenCode | 10 条 | 3 | 无 |
| Qwen Code | 10 条 | 10 | v0.22.0-nightly.20260823 |
| OpenAI Codex | 暂无数据 | 暂无数据 | 暂无数据 |
| Gemini CLI | 暂无数据 | 暂无数据 | 暂无数据 |

**简评**：Qwen Code 今日 PR 数量显著领先，处于高频迭代状态；Claude Code 的 issue 讨论深度和用户影响力最高（单 issue 获 351 👍）；OpenCode 通过快速 PR 回应流式稳定性问题；Kimi Code 社区规模较小但存在长期高热度需求。

---

## 3. 共同关注的功能方向

### 3.1 跨会话记忆 / 持久化上下文
- **Claude Code**：#73024 用户反馈“Claude 什么都不记得”，memory 可靠性存疑。
- **Kimi Code CLI**：#1283 要求完整的跨会话记忆系统，已持续讨论近 6 个月。
- **GitHub Copilot CLI**：#4535 `store_memory` 在预发布版失败，说明记忆功能已进入实现阶段但仍有回归。

### 3.2 成本透明与 token 配额治理
- **Claude Code**：#73615 会话显示 $60、实际账单 $300；#73601 单子代理 3 小时烧掉 1000 万 token。
- **Kimi Code CLI**：#2604 用户通过插桩实测，Vivace 付费配额疑似缩水 3–5 倍且无公告。

### 3.3 多代理 / 后台任务可靠性与恢复
- **Claude Code**：#48965 多会话协调原语缺失；#80881 Plan Mode 并行子代理报错；#73601 子代理死循环。
- **Qwen Code**：#8586 需要后台 Agent 健康跟踪与失去响应后的恢复机制。
- **OpenCode**：#41469 空响应后会话静默停止，用户被迫手动“Keep going”。

### 3.4 模型行为可控性与透明降级
- **Claude Code**：#77136 用户集中抱怨模型“修辞套话”；多个 issue 反馈 Fable 5 静默降级到 Opus 4.8 且无提示。
- **OpenCode**：#32366 流式错误后 UI 卡死，无错误恢复路径。
- **Qwen Code**：#5975 流式请求 120 秒无活动即超时，影响长思考过程。

### 3.5 平台稳定性（Windows 优先）
- **Claude Code**：#7134 Windows 文件编码破坏问题悬置近一年。
- **Qwen Code**：#8625 Windows 终端中文输入拼音显示不清。
- **OpenCode**：#44528 Windows 上网络错误；#44337 macOS ARM64 TUI 空帧。
- **GitHub Copilot CLI**：社区反馈 Windows 插件安装与 VS Code 冲突。

### 3.6 安全 / 权限边界
- **Claude Code**：Fable 5 安全分类器误报，将正常开发行为判定为不安全。
- **Qwen Code**：#9827 `permissions.allow` 只影响 UI 展示，实际请求仍发送全部内置工具。
- **Kimi Code CLI**：#2614 主动澄清插件边界，并补充安全与数据持久化说明。

---

## 4. 差异化定位分析

| 工具 | 功能侧重 | 目标用户 | 技术路线 / 社区特征 |
|---|---|---|---|
| **Claude Code** | 多代理编排、插件/Hook 生态、Fable 模型集成 | 高级开发者、企业自动化团队 | 功能最全、生态沉淀深，但模型行为和成本控制成为主要痛点 |
| **GitHub Copilot CLI** | GitHub 生态深度绑定、企业策略/认证、多模型支持（含 Grok） | GitHub 重度用户、企业 Copilot 客户 | 以 GitHub 平台能力为中心，插件/skills 热加载持续改进 |
| **Kimi Code CLI** | 记忆系统、配额透明度、移动端远程配对 | 中英文开发者、注重长上下文与成本可见性的用户 | 社区规模较小但需求聚焦，移动端“旁观+否决”模式有差异化 |
| **OpenCode** | TUI 体验、MCP 工具链、本地模型（Ollama）集成 | 开源、自定义/本地优先的开发者 | 快速修复流式稳定性和会话恢复，社区议题偏向“基础设施可靠性” |
| **Qwen Code** | `/review` 审查流程工程化、多渠道接入（DingTalk/Telegram/Web Shell） | 企业开发者、中文社区、需要审查/协作闭环的团队 | PR 数量多、迭代快，明显向“团队协作 + 可视化 + 流程化”演进 |
| **OpenAI Codex / Gemini CLI** | 本期无动态数据 | — | — |

---

## 5. 社区热度与成熟度

- **Claude Code**：用户基数最大、issue 影响力最强。高 👍 issue 反映模型层问题已形成大规模共识；但维护版本更新粒度较小，部分 Windows/编码问题长期未修复，社区有一定“怨气积累”。
- **Qwen Code**：今日最活跃的工程迭代方。10 个 PR 覆盖 `/review`、Web Shell、VS Code 扩展、渠道集成，说明团队正在快速补齐企业协作场景。
- **OpenCode**：处于“快速增长后的稳定性修补期”。多个 issue 围绕空响应、流式错误、TUI 卡死，PR 则直接对应这些缺陷，修复链路清晰。
- **GitHub Copilot CLI**：发布节奏稳定，但认证间歇性失效和插件冲突问题持续影响体验。社区热度中等，更偏向企业用户。
- **Kimi Code CLI**：目前数据量较小，但 #1283 的 27 条长期讨论说明其核心用户粘度高，且 #2604 的计量质疑很尖锐。
- **OpenAI Codex / Gemini CLI**：本期无数据，无法判断。

总体判断：**Claude Code 最成熟但受制于模型层不确定性；Qwen Code 迭代最快，正向“企业级审查协作平台”倾斜；OpenCode 是典型的社区驱动型工具，稳定性修复效率高。**

---

## 6. 值得关注的趋势信号

1. **“模型行为可控性”正在成为 AI CLI 的核心竞争点**  
   用户不再满足于“能写代码”，而是要求文风稳定、降级透明、记忆可靠。Claude Code 的 #77136 和多个 Fable 误报 issue 说明：模型层问题会直接侵蚀工具层口碑。

2. **Token 成本治理将从“可选项”变为“必备能力”**  
   从 10M token 失控事故到账单 5 倍差额，再到 Kimi 用户自建插桩计量，社区都在要求官方提供：成本预估、用量仪表盘、子代理 token 上限、熔断机制。

3. **“有状态 Agent”是下一阶段的分水岭**  
   Kimi 的跨会话记忆、Claude 的多会话协调原语、Copilot 的 `store_memory`，共同指向一个方向：Agent 必须能在会话之间保留项目模式与用户偏好，否则难以在大型项目中真正落地。

4. **安全边界需要“配置即承诺”**  
   Qwen Code 的 `permissions.allow` 未真正生效、Claude 的安全分类器误报，说明当前权限体系仍停留在“表面控制”。对企业和安全敏感用户来说，这是采用前必须解决的问题。

5. **远程/移动端/Messenger 接入正在成为新战场**  
   Qwen Code 接入钉钉/Telegram、Kimi 的移动端配对、Web Shell 的持续增强，意味着 AI CLI 的使用场景正从“个人终端”扩展到“团队远程协作”和“移动审批”。

6. **社区对可观测性和可恢复性的要求已超过对“生成能力”的关注**  
   多个工具的高频 issue 不是“模型写不出好代码”，而是“为什么静默停止”“为什么卡死”“为什么不报错”。对开发者而言，选择工具时除了看模型能力，更要关注其错误处理、日志透明度和恢复机制——这会直接影响自动化流程的稳定性。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告

**数据截止**：2026-08-24 ｜ **来源**：[anthropics/skills](https://github.com/anthropics/skills) ｜ 说明：本次数据中 PR 评论数字段缺失（undefined），以下热门排序以仓库"按评论数排序"的呈现顺序为基准。

---

## 1. 热门 Skills 排行（Top 8）

| # | Skill / PR | 功能与热点 | 状态 |
|---|-----------|-----------|------|
| 1 | **skill-creator 评估链路修复** ([#1298](https://github.com/anthropics/skills/pull/1298)) | 修复 `run_eval.py` 对所有技能描述均报告 recall=0% 的致命缺陷（关联 issue [#556](https://github.com/anthropics/skills/issues/556)，10+ 独立复现），并覆盖 Windows 流读取、触发检测、并行 worker。核心争议：官方"描述优化循环"一直在对着噪声优化 | OPEN |
| 2 | **document-typography 排版技能** ([#514](https://github.com/anthropics/skills/pull/514)) | 治理 AI 文档的孤行（1-6 词溢出）、寡段（页尾孤立标题）、编号错位三大高频缺陷。社区共识：这是 Claude 生成文档的普遍痛点，用户很少主动要求排版质量 | OPEN |
| 3 | **ODT 办公文档技能** ([#486](https://github.com/anthropics/skills/pull/486)) | 新增 OpenDocument 格式（.odt/.ods）创建、模板填充与 ODT→HTML 转换能力，覆盖 LibreOffice 与 ISO 标准文档场景。讨论热点：与既有 docx/pdf 技能形成格式互补矩阵 | OPEN |
| 4 | **pdf 大小写引用修复** ([#538](https://github.com/anthropics/skills/pull/538)) | 修复 `SKILL.md` 中 8 处 `REFERENCE.md`/`FORMS.md` 大小写不匹配导致的"区分大小写文件系统"失效。暴露官方技能本身的可靠性短板 | OPEN |
| 5 | **frontend-design 技能重构** ([#210](https://github.com/anthropics/skills/pull/210)) | 修订目标：确保每条指令可在单次对话内被执行、可操作、内部自洽。讨论焦点：技能应"指导行为"而非"教育人类"，与 issue [#202](https://github.com/anthropics/skills/issues/202) 批评 skill-creator 语气过于学术形成呼应 | OPEN |
| 6 | **sk-quality-analyzer + skill-security-analyzer 元技能** ([#83](https://github.com/anthropics/skills/pull/83)) | 双元技能：前者按"结构与文档（20%）、示例、资源…"五维评分技能质量；后者做安全分析。反映社区对技能"质控"的自觉需求 | OPEN |
| 7 | **Hivemind 零成本多智能体编排** ([#1628](https://github.com/anthropics/skills/pull/1628)) | 让 Claude Code 把机械性工作委托给跑在免费模型上的 headless [opencode](https://opencode.ai) worker，自己保留规划/审查/合并权。金句："昂贵模型的上下文才是稀缺资源，而非其智能" | OPEN |
| 8 | **self-audit 输出质量审计** ([#1367](https://github.com/anthropics/skills/pull/1367)) | 交付前先机械校验输出文件真实性，再按损害严重度执行四维推理审计。通用无技术栈绑定，与 issue [#1385](https://github.com/anthropics/skills/issues/1385) 提出的三闸门管线（预任务校准→对抗审查→交付验证）同源 | OPEN |

**趋势观察**：热门榜呈"两极化"——一半是**新技能补给**（文档、编排、质控），另一半是**官方工具链自愈**（skill-creator 评估失效、pdf 引用、frontend-design 可操作性）。且 Top 20 PR 全部处于 OPEN 状态，无一条已合并，说明官方存在明显评审积压。

---

## 2. 社区需求趋势（来自 Issues）

1. **安全与信任治理（最热）**：[#492](https://github.com/anthropics/skills/issues/492)（43 评论）——社区技能被分发在 `anthropic/` 命名空间下，造成信任边界滥用，用户可能误将社区技能当官方技能授予高权限。
2. **组织级协作**：[#228](https://github.com/anthropics/skills/issues/228)（8👍）——要求 Claude.ai 支持组织内技能库/分享链接，替代"下载文件→聊天工具传输→手动上传"的原始流程。
3. **官方工具链可靠性**：三连击。[#556](https://github.com/anthropics/skills/issues/556)（7👍）触发率为 0 的 bug、[#62](https://github.com/anthropics/skills/issues/62) 技能神秘消失、[#202](https://github.com/anthropics/skills/issues/202) 批评 skill-creator 写得像给

---

# Claude Code 社区动态日报 — 2026-08-24

## 1. 今日速览

- 官方发布维护版本 **v2.1.241**，仅包含 bug 修复与可靠性改进。
- 模型文风问题持续成为社区最大争议：issue **#77136** 以 351 👍 / 89 评论高居热度榜首，用户集中抱怨 Claude 4.7/4.8/5.0 及 Fable 的"修辞套话"问题。
- Windows 历史顽疾（文件编码破坏 #7134）仍在发酵，连续第二年未获解决；此外 Fable 5 安全分类器误报、子代理 token 失控等成为开发者高频痛点。

## 2. 版本发布

### v2.1.241（最新）
- 发布内容：**Bug fixes and reliability improvements**
- 说明：小版本维护更新，官方未披露具体修复明细，建议关注后续 release notes 或 changelog。
- 链接：https://github.com/anthropics/claude-code/releases

## 3. 社区热点 Issues

以下按热度与影响力筛选 10 条（其中 #77136、#7134、#74558、#87472、#80881 仍处于 Open 状态，其余已关闭但仍具参考价值）：

### 3.1 🔥 模型文风退化引发大规模共鸣（OPEN）
- **#77136** [BUG] Claude 4.7/4.8/5.0 与 Fable 普遍出现重复性修辞套话，即便给出明确风格指令仍难以产出连贯散文
- 作者：@pbower | 👍 351 | 评论 89
- 为什么重要：评论数远超其他 issue，且 👍 数为全库最高，说明大量用户正遭遇生成质量一致性问题，可能指向模型层（采样/系统提示）而非工具层缺陷。
- https://github.com/anthropics/claude-code/issues/77136

### 3.2 Windows 文件编码破坏问题悬而未决（OPEN）
- **#7134** [BUG] Claude Code 不尊重文件编码，破坏 Windows-1252 文件
- 作者：@edlyra | 👍 23 | 评论 27
- 为什么重要：2025-09 创建至今仍在 Open 状态，Windows 平台用户持续受影响，已积累 27 条评论，属于老牌高复现 bug。
- https://github.com/anthropics/claude-code/issues/7134

### 3.3 Fable 5 音频/文本块被静默吞掉（OPEN）
- **#74558** [BUG] Fable 5：turn 中途的 assistant 文本块偶尔被交付为"摘要思考块"，turn 看起来是沉默的
- 作者：@randalmurphal | 👍 8 | 评论 9
- 为什么重要：影响流式输出在终端与 `--output-format stream-json` 两种场景下的一致性，对自动化工具链开发者是关键可靠性问题。
- https://github.com/anthropics/claude-code/issues/74558

### 3.4 桌面浏览器面板阻断内网子资源（OPEN）
- **#87472** [BUG] 浏览器面板以 `net::ERR_BLOCKED_BY_CLIENT` 阻断所有私有网络（RFC1918）LAN 子资源，页面永远无法渲染
- 作者：@bignay2000 | 👍 0 | 评论 3
- 为什么重要：新提交（08-17）的桌面端 bug，影响本地开发场景中加载内网 Web 应用，可能导致企业用户无法使用 Claude Desktop 内置浏览器调试内部系统。
- https://github.com/anthropics/claude-code/issues/87472

### 3.5 Plan Mode 并行子代理报 API 400（OPEN）
- **#80881** [area:agents] API Error 400: 在 Plan Mode 下启动并行子代理时 system content 必须包含至少一个 block
- 作者：@askku39 | 评论 1
- 为什么重要：Plan Mode + 并行后台子代理是高级用户的常见工作流组合，该错误阻断了多线程规划场景。
- https://github.com/anthropics/claude-code/issues/80881

### 3.6 多会话协调原语缺失（CLOSED，含 11 条讨论）
- **#48965** [Feature] 多会话协调原语：跨会话消息、会话注册表、压缩抗性状态、共享任务看板
- 作者：@ThatDragonOverThere | 评论 11
- 为什么重要：用户已用 1 个 Opus PM 会话 + N 个 worker 会话跑通多代理编排，但现有工具（Agent/ScheduleWakeup/Memory）在设计上缺少跨会话通信机制。已关闭可能因 stale，但需求描述完整，值得官方参考。
- https://github.com/anthropics/claude-code/issues/48965

### 3.7 Notebook 读取工具缺失
- **#60844** [Feature Request] 添加 NotebookRead 工具以高效提取 Jupyter notebook 单元格
- 作者：@artemisart | 评论 5
- 为什么重要：当 notebook 内嵌大量 output 导致体积膨胀时，`Read` 工具会被阻塞，现有 workaround（jq/python 提取）脆弱且耗 token。在数据科学工作流中是明确痛点。
- https://github.com/anthropics/claude-code/issues/60844

### 3.8 Claude "什么都不记得"（CLOSED）
- **#73024** [BUG] Claude 什么都不记得（memory 相关）
- 作者：@fireproofsocks | 评论 4
- 为什么重要：标题直指 memory 功能失效，虽已关闭（可能 stale 标记），但 memory 可靠性问题对长会话场景影响重大。
- https://github.com/anthropics/claude-code/issues/73024

### 3.9 子代理陷入死循环烧掉千万 token（CLOSED）
- **#73601** [BUG] Resumed 子代理陷入自寻址重试循环，3 小时烧掉约 1000 万 token，零输出
- 作者：@OrenHorev-PD | 评论 1
- 为什么重要：单次事故消耗约 10M token，属于成本与资源控制层面的极端案例，对使用长时后台任务的团队有警示意义。
- https://github.com/anthropics/claude-code/issues/73601

### 3.10 动态工作流成本报告与账单不符（CLOSED）
- **#73615** [BUG] 动态工作流成本报告：会话显示花 $60，实际账单为 $300
- 作者：@rjmackay | 评论 1
- 为什么重要：成本可见性直接影响用户预算管理。5 倍差额若是普遍现象，将动摇用户对费用预估的信任。
- https://github.com/anthropics/claude-code/issues/73615

## 4. 重要 PR 进展

过去 24 小时内数据源中仅收录到 **1 条 PR**（仓库可能处于 PR 静默期）：

### 4.1 为插件开发文档补充 MessageDisplay 事件（OPEN）
- **#83374** docs(plugin-dev): document MessageDisplay streaming semantics
- 作者：@iCodeCraft | 更新：2026-08-23
- 内容：为内置 Hook Development skill 补充 `MessageDisplay` 事件的触发描述、事件指南及速查表说明，该事件此前在文档中缺失。
- 意义：改善插件开发者对 Hook 事件流的理解，属于文档补全类 PR，虽小但有助于生态建设。
- https://github.com/anthropics/claude-code/pull/83374

## 5. 功能需求趋势

从全部 50 条活跃/历史 issue 中，可提炼出以下社区需求方向：

| 方向 | 代表 Issue | 说明 |
|------|-----------|------|
| **模型行为可控性** | #77136、#73024、#73609 等 | 用户希望获得更稳定的文风输出、可靠的记忆、可解释的模型降级/回退机制 |
| **多代理/多会话编排原语** | #48965、#80881、#73601 | 社区在自行搭建 PM-worker 协作模式，需要官方提供跨会话通信、会话注册、共享状态等原语 |
| **平台稳定性补强（Windows 优先）** | #7134、#73590 | Windows 上文件编码破坏、`~/.claude.json` 重复损坏并清空 MCP servers 的问题亟需修复 |
| **垂直场景工具扩展** | #60844（NotebookRead）、#87472（浏览器面板 LAN 访问） | 针对数据科学、内网 Web 开发等具体场景的工具能力缺失 |
| **成本透明与配额控制** | #73615、#73601 | 更精准的成本报告、子代理 token 上限/熔断机制成为刚需 |
| **远程/移动端控制完善** | #73617、#73565 | 远程控制缺少"输入"能力，bridge 重启会静默禁用 routines，移动端体验仍需打磨 |

## 6. 开发者关注点

- **安全分类器误报（Fable 5）**：至少 5 条独立 issue（#73604、#73609、#73599、#73594、#73598）反馈 Fable 将正常开发行为（如 UI 工作、Amiga 模拟器、Firecrawl 集成）判定为不安全并回退到 Opus。此类误报严重影响开发连续性与用户信任，是当前反馈最集中的痛点之一。
- **模型"悄悄降级"行为**：多名用户在未收到明确提示时被从 Fable 5 回退至 Opus 4.8（#73598），诉求是降级应透明化并给出原因。
- **Windows 平台老问题未解**：文件编码破坏（#7134）自 2025-09 起悬而未决；`~/.claude.json` 损坏清空 MCP servers（#73590）已 stale 关闭但未被修复，Windows 用户配置可靠性堪忧。
- **成本与资源失控**：会话显示 $60 但实际账单 $300（#73615）、单子代理 3 小时烧 10M token（#73601）——开发者对成本可见性和防护机制的要求愈发强烈

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

## GitHub Copilot CLI 社区动态日报（2026-08-24）

### 1. 今日速览

- **v1.0.81-8 发布**：新增 Grok 4.6 的 xhigh 推理支持，并大幅优化本地插件/技能热加载逻辑，开发者无需再手动执行 `/plugin update`。
- **稳定性问题集中爆发**：社区多个 Issue 聚焦后台压缩导致工具结果丢失、认证间歇性失效、Windows 插件安装与 VS Code 冲突等高频问题。
- **PR 侧活动较少**：过去 24 小时仅有 1 条 PR 更新（疑似标题拼写有误的 README 重命名），项目可能正处于发布收敛或主分支开发阶段。

---

### 2. 版本发布

#### v1.0.81-8
**新增**
- 支持 Grok 4.6 的 xhigh reasoning effort 级别。

**改进**
- **本地插件实时生效**：来自目录型 marketplace 的路径型插件现在直接从真实目录加载，编辑后 `/restart` 或开启新会话即可生效，无需再执行 `/plugin update`。
- **Skills 与自定义 Agents 发现机制增强**：提升了基于本地 marketplace 的 Skills 和自定义 Agents 的可发现性。

> 附注：Release 说明中 “Skills and custom agents are discover...” 疑似被截断，官方可能将在后续补全。

---

### 3. 社区热点 Issues（精选 10 条）

#### #2306 认证错误：要求启用企业/组织策略
- **作者**：@stewartadvt | **更新**：2026-08-23 | **评论**：9 | **👍**：3
- **链接**：https://github.com/github/copilot-cli/issues/2306

> **摘要**：用户遇到 `You are not authorized to use this Copilot feature, it requires an enterprise or organization policy to be enabled`，每周出现 2~3 次且自动消失。

**为什么重要**：该 Issue 从 3 月一直持续至今，至今仍是 Open 状态，说明认证/授权服务的稳定性问题尚未根治，且影响面较大（适用所有企业策略管控场景）。

---

#### #4535 `store_memory` 在 v1.0.81 预发布版失败：实例 ID 缺失
- **作者**：@DavidTeju | **更新**：2026-08-23 | **评论**：5 | **👍**：0
- **链接**：https://github.com/github/copilot-cli/issues/4535

> **摘要**：Copilot CLI 1.0.81 预发布版中 `store_memory` 始终失败，原因是 Rust 运行时在调用 memory writer 时未携带必需的实例 ID。

**为什么重要**：内存写入是基于长期记忆的关键功能，该回归直接影响新版本的可用性，社区已跟踪多个预发布版本。

---

#### #4572 后台

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 · 2026-08-24

> 数据来源：[github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

## 📌 今日速览

今日无新版本发布，社区讨论热度集中在**跨会话记忆系统**（#1283）与**配额计量异常**（#2604）两个议题上。其中 #1283 长期保持 27 条评论未关闭，显示开发者对持久化上下文的强烈诉求；#2604 则以用户实测数据质疑配额缩水，值得官方回应。另有两个新 PR 值得关注：远程手机配对（#2616）与插件文档安全澄清（#2614）。

## 🚀 版本发布

过去 24 小时无新 Release。

## 🔥 社区热点 Issues（共 3 条）

当前数据源仅包含 3 条最近更新的 Issue，全部列出如下：

### #1283 [OPEN] 功能请求：记忆系统 —— 跨会话持久上下文

- **作者**：@CatKang｜**创建**：2026-02-27｜**更新**：2026-08-23
- **评论数**：27 ｜ 👍 0
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/1283
- **摘要**：希望实现一套完整的**记忆系统**，让 Kimi Code CLI 跨会话记住有用的上下文、项目模式与用户偏好，涵盖 AI 自动管理的笔记（automatic memory）与用户自定义指令（manual memory）两类能力。
- **重要性**：该 Issue 已持续近 6 个月且长期活跃，是社区呼声最高的功能方向之一。跨会话上下文丢失是当前编码代理工具的通用痛点，记忆系统直接关系到 Agent 在大型项目中的实用性和连续工作能力。

### #2604 [OPEN] 每周配额被悄悄缩减 3–5 倍 —— 疑似计量回归或条款变更

- **作者**：@tobiu｜**创建**：2026-08-15｜**更新**：2026-08-23
- **评论数**：3 ｜ 👍 0
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2604
- **摘要**：用户以 Vivace 付费会员身份进行 Agentic Coding 工作负载测试，通过自建客户端插桩（wire-level JSONL ledger）每天记录原始 token 消耗（新增输入 + 缓存读取 + 输出）。实测发现当前实际可用额度与官宣相比缩减约 **3–5 倍**，且未见任何说明。用户怀疑是条款变更或计量系统回归。
- **重要性**：直接涉及付费用户的信任问题。社区对这种不透明扣减高度敏感，尤其当官方未提前公告条款变更时，容易引发对产品可持续性的质疑。3 条评论虽然不多，但数据驱动的实证分析往往能引起运营团队跟进。

### #2484 [CLOSED] 无标题（空 Issue）

- **作者**：@lin200083｜**创建**：2026-07-04｜**更新**：2026-08-23
- **评论数**：0 ｜ 👍 0
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2484
- **摘要**：无有效摘要内容。
- **重要性**：低。该 Issue 已被关闭，无有效讨论内容，推测为无效提交或误操作。不构成关注点。

## 📦 重要 PR 进展（共 2 条）

今日更新 2 个 PR，全部列出：

### #2616 [OPEN] 新增 Build Remote Agent 手机配对（gbr/1）

- **作者**：@LinespottingPrivate｜**创建/更新**：2026-08-23
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2616
- **内容**：为桌面 Agent 增加 **Build Remote Agent** 作为配对设备。通过免费 MIT 协议 [`gbr-agent`](https://github.com/LinespottingOrg/GrokBuildRemote-Agents)，付费 iOS/Android App 可旁观（spectate）本地会话，并支持注入（inject）操作。手机端作为"旁观 + 否决"角色，而非编排者。
- **价值**：这是一个将移动端与桌面 CLI Agent 联动的创造性尝试。引入"human-in-the-loop"的移动便捷维度，让用户可以不守在电脑旁审查/干预 Agent 行为。MIT 协议开放，降低接入门槛。

### #2614 [OPEN] 文档（plugins）：补充安全与持久化数据说明

- **作者**：@QIANLING-0831｜**创建**：2026-08-20｜**更新**：2026-08-23
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2614
- **内容**：仅作文档澄清，明确 `MoonshotAI/kimi-cli` 插件契约的范围：根目录 `plugin.json`、基于命令的工具、`inject`、安装目录 `~/.kimi/plugins/`。该文档**不**描述或改变另一独立的插件系统，并补充了安全与持久化数据的相关说明。
- **价值**：插件边界历来是生态混乱的重灾区。此 PR 主动划清范围并补充数据持久化说明，能有效减少用户误用、生产事故和插件间冲突，属于"生态基础设施"类贡献。

## 📊 功能需求趋势

> 分析口径：基于全部 3 个活跃 Issues 与 2 个 PR 中反映出的功能方向。

1. **记忆 / 持久化上下文**
   - 代表：#1283（记忆系统）
   - 这是当前最强烈的功能诉求。开发者期待 CLI 能记住项目模式、用户偏好与关键上下文，减少每次会话的重复描述与理解成本。这类需求本质上是将 CLI 从"无状态命令工具"推向"有状态的编码 Agent"。

2. **配额透明性与计量公平**
   - 代表：#2604（配额缩减质疑）
   - 用户希望消耗量可衡量、可预期，且配额变化应有提前公告。侧面反映社区对 Cloud Token 用量透明化的普遍要求——开发者需要准确预估成本，避免在关键时刻被配额腰斩。

3. **多设备协同 / Remote Agent**
   - 代表：#2616（手机配对）
   - 将桌面 Agent 的能力延伸至移动端，通过 App 旁观与注入实现远程干预。这并非核心功能请求，但预示着 Agent 使用场景从"单机编程"向"远程协作"演进。

4. **插件生态规范化**
   - 代表：#2614（插件边界文档）
   - 社区开始关注插件安装边界、安全风险与持久化数据的归属问题。随着插件数量增多，官方明确契约是生态健康发展的前提。

## 👨‍💻 开发者关注点

- **配额争议是当前最尖锐的信任痛点**：#2604 用户用插桩数据证明，Vivace 档位的实际可用 token 与宣传不符缩小 3–5 倍。高频反馈是"没有公告就被降配"，这直接影响付费会员的续费意愿。建议官方尽快给出定量说明或修复计量回归。

- **跨会话记忆的缺失正在拖慢实际工作流**：#1283 反映的场景非常具体：Agent 无法记住项目中的既有约定（如 API 风格、命名规范），导致每次新会话需要重新灌输上下文。开发者期望至少提供两档记忆：AI 自动维护（沉淀讨论结论）和用户手动固定（如指令/偏好），并要求记忆内容可查看、可删除、可导出。

- **插件的安全与数据持久化机制需进一步明确**：#2614 虽然澄清了 `plugin.json` 与目录约定，但开发者另有关注点——插件是否可以访问项目外数据？卸载后是否残留？这些细节直接影响开发者是否敢大规模引入三方插件。

- **移动端旁路操作（#2616）表现出兴趣，但持观望态度**：虽然遥控 Agent 很吸引人，但"spectator + veto"模式下安全边界如何保证（例如手机被劫持时的否决权滥用）尚不明确，可能需要官方或社区提供安全规范。

- **普遍缺少计量仪表盘**：从 #2604 的插桩方式来看，用户需要自行实现 JSONL 记账才能监控消耗，说明官方未提供内建的用量统计界面。这是一个明显的可观测性缺口。

---

> 报告生成时间：2026-08-24 ｜ 数据源仅覆盖过去 24 小时 GitHub 动态，N=5（3 Issues + 2 PRs）。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-24

## 今日速览

过去 24 小时无新版本发布，社区焦点集中在**会话稳定性**上：多个 issue 报告模型在空响应或网络错误后静默停止，用户被迫反复手动输入 "Keep going"。与此同时，#32157 提出的"中途提示传递"功能需求获得 **76 👍**，成为近期呼声最高的功能提案。PR 侧可见多条针对会话恢复与错误重试的修复正在快速推进。

---

## 社区热点 Issues

1. **会话在空 LLM 响应后静默停止** · #41469  
   OPEN，14 评论，👍 1  
   当模型返回 0 token 空响应（finish_reason 映射为 `unknown`）时，会话直接退出且无任何提示。用户需要手动重新发起请求，严重影响自动化流程。  
   [查看 issue](https://github.com/anomalyco/opencode/issues/41469)

2. **可配置中途提示传递：queue / steer / break** · #32157  
   OPEN，7 评论，👍 76  
   请求在模型生成过程中区分"排队""转向""打断"三种提示语义，并支持压缩感知的 steer 行为。高赞表明这是许多高级用户共同面临的交互瓶颈。  
   [查看 issue](https://github.com/anomalyco/opencode/issues/32157)

3. **本地 Ollama 工具调用完全失败** · #1034  
   CLOSED，31 评论，👍 16  
   使用 `qwen3:32b` 等支持工具调用的本地模型时，模型只思考不执行工具调用。该 issue 周期长、讨论热烈，反映本地模型集成仍是重要痛点。  
   [查看 issue](https://github.com/anomalyco/opencode/issues/1034)

4. **Bug Report: 网络错误导致无法使用** · #44528  
   OPEN，7 评论  
   用户报告 Windows 10 上 1.18.21 版本在离上次使用数天后启动即持续网络错误，疑似服务端或本地缓存问题，影响范围较大。  
   [查看 issue](https://github.com/anomalyco/opencode/issues/44528)

5. **UI 在流错误后无限卡在 "thinking"** · #32366  
   OPEN，7 评论，👍 1  
   流式错误（如 `AI_APICallError`、socket 关闭）后 TUI 不显示错误、不恢复状态，只能重启应用。会话状态机缺少错误恢复路径。  
   [查看 issue](https://github.com/anomalyco/opencode/issues/32366)

6. **LLM 响应期间阅读聊天记录仍会强制回到底部** · #29094  
   OPEN，6 评论，👍 2  
   这是 #4196 的重开。用户在生成期间向上滚动阅读历史，每来一个 token 就被拉回底部，多用户确认存在。  
   [查看 issue](https://github.com/anomalyco/opencode/issues/29094)

7. **MCP 工具结果中的 structuredContent 被丢弃** · #38923  
   OPEN，4 评论，👍 1  
   当 MCP 服务器同时返回 `content` 和 `structuredContent` 时，opencode 只转发 text，导致依赖结构化 JSON 数据的工具无法正常工作。影响 MCP 生态完整性。  
   [查看 issue](https://github.com/anomalyco/opencode/issues/38923)

8. **Zen API：包含 tools 的请求返回 "Endpoint is unavailable"** · #44300  
   OPEN，4 评论，👍 1  
   `x-preview-f-free` / `ox-alpha-free` 两个免费模型在 8 月 23 日起凡是带 `tools` 数组的请求全部失败，疑似服务端配置变更，影响免费版工具调用。  
   [查看 issue](https://github.com/anomalyco/opencode/issues/44300)

9. **Desktop：同一仓库两个 clone 显示同一项目名/路径** · #44101  
   OPEN，3 评论  
   项目 ID 由 git remote 归一化派生，导致同一仓库的多个本地副本被识别为一个项目，且重启不修复。多分支协作场景下容易误操作。  
   [查看 issue](https://github.com/anomalyco/opencode/issues/44101)

10. **TUI 在 macOS ARM64 上仅画空帧** · #44337  
    OPEN，3 评论  
   1.16.2/1.17.0/1.18.21 在 Apple Silicon 上服务器正常启动但渲染器完全不绘制 UI，涉及 WezTerm、Herdr 等多个终端，`--pure` 下也能复现。  
    [查看 issue](https://github.com/anomalyco/opencode/issues/44337)

---

## 重要 PR 进展

1. **feat(session): 自动重试空停止响应** · #44536  
   针对模型偶发返回 `finish_reason: stop` 且 0 token 的情况，自动触发重试，直接对应 #41469 的根治尝试。  
   [查看 PR](https://github.com/anomalyco/opencode/pull/44536)

2. **fix(ai): 重试 detail-free 响应错误** · #44537  
   将无详细内容的 Responses API 错误事件归类为瞬时故障，并保留原始 payload 便于诊断。  
   [查看 PR](https://github.com/anomalyco/opencode/pull/44537)

3. **fix(session): 修复重发 delta 时产生幻影 "unknown" 工具片段** · #44535  
   经排查，#33618 中的 phantom 工具调用由 opencode 自身产生而非模型发出，PR 修复了 delta 重放逻辑。  
   [查看 PR](https://github.com/anomalyco/opencode

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-08-24）

## 今日速览
- 发布新夜间版 `v0.22.0-nightly.20260823`，修复了 Web Shell 从概览面板打开会话时工作目录传递错误的问题。
- 社区围绕工具权限配置未真正生效（#9827）、斜杠命令间歇性失效（#9821）等 bug 展开热议，同时 `/review` 相关的增强与重构 PR 密集推进。
- 渠道集成（DingTalk、Telegram）和 Web Shell 体验优化成为当前最活跃的功能开发方向。

## 版本发布
**v0.22.0-nightly.20260823.1007bcacfc**  
- 修复 `web-shell`：从概览面板打开会话时传递 session workspace cwd。  
🔗 [查看 Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.22.0-nightly.20260823.1007bcacfc)

## 社区热点 Issues
1. **#9827 `permissions.allow` 不限制发送给模型的工具集**（OPEN, P2）  
   allowlist 只影响 CLI 内 `/tools` 显示，实际 API 请求仍包含全部内置工具，安全预期与实际行为不符。4 条评论，反映用户对权限控制真实落地的关注。  
   🔗 https://github.com/QwenLM/qwen-code/issues/9827

2. **#9821 原生斜杠命令间歇性缺失**（OPEN, P2）  
   用户级 `commands/*.md` 约 50% 概率无法通过 Skill 工具调用，影响版本 0.21.8+。该问题跨项目复现，社区普遍期待快速修复。  
   🔗 https://github.com/QwenLM/qwen-code/issues/9821

3. **#5975 流式请求 120 秒无活动后报错**（OPEN, P2, welcome-pr）  
   升级到 v0.19.3 后频繁出现 `No stream activity for 120000ms`，思考过程长时间无输出导致超时。11 条评论，1 个 👍，是使用稳定性的重要投诉点。  
   🔗 https://github.com/QwenLM/qwen-code/issues/5975

4. **#8625 Windows 终端输入中文时拼音显示不清**（OPEN, P2）  
   Windows 终端下中文输入法的拼音无法辨识，严重影响中文用户交互。8 条评论，期待渲染层修复。  
   🔗 https://github.com/QwenLM/qwen-code/issues/8625

5. **#9219 `/review` presubmit 重叠匹配仅支持精确行**（OPEN, P2）  
   多行范围与语义重复的评论无法被正确识别，导致 `noConflict` 误判。5 条评论，直指审查流程的准确性痛点。  
   🔗 https://github.com/QwenLM/qwen-code/issues/9219

6. **#8586 跟踪 activeWork 与后台 Agent 恢复**（OPEN, P2）  
   建议为 daemon 增加 `activeWork` 健康状态，并完善后台 Agent 失去响应时的恢复机制。4 条评论，属于后台自动化方向的核心需求。  
   🔗 https://github.com/QwenLM/qwen-code/issues/8586

7. **#8769 将 `/review` Step 3–5 编排迁移至工作流引擎**（OPEN, P2）  
   提议让审查的扇出、验证、反向审计变为确定性代码，摆脱模型驱动的不稳定性。4 条评论，体现社区对审查流程可控性的追求。  
   🔗 https://github.com/QwenLM/qwen-code/issues/8769

8. **#9145 审批模式值域在 20 个文件中手抄，已有 2 处错误**（OPEN, P3）  
   要求为 approval-mode 建立单一数据源，并在测试中强制一致性。4 条评论，是典型的“小问题大隐患”工程债。  
   🔗 https://github.com/QwenLM/qwen-code/issues/9145

9. **#8662 将 TUI 渲染层从 ink 迁移到 OpenTUI**（OPEN, P3, need-discussion）  
   当前 ink 的多项结构性问题（闪烁、补丁复杂）促使社区呼吁迁移到 OpenTUI，以获得 flicker-free 与鼠标支持。3 条评论，影响终端 UX 长远演进。  
   🔗 https://github.com/QwenLM/qwen-code/issues/8662

10. **#9831 与 craft-agents-oss 的关系询问**（OPEN, question）  
    用户发现两者界面几乎一致且共享会话，质疑项目间关系。2 条评论，虽为疑问，但涉及开源合规与品牌区分，值得维护者公开回应。  
    🔗 https://github.com/QwenLM/qwen-code/issues/9831

## 重要 PR 进展
1. **#9394 新增钉钉（DingTalk）工作群渠道**  
   基于已认证 DWS CLI 配置文件，支持私聊、@提及、文档通知与待办事件。社群多渠道集成能力再进一步。  
   🔗 https://github.com/QwenLM/qwen-code/pull/9394

2. **#9676 收缩内容生成器接口**  
   移除未使用的 token 计数与摘要思考能力，精简懒加载/日志装饰器及对应死测试，提升可维护性。  
   🔗 https://github.com/QwenLM/qwen-code/pull/9676

3. **#9768 `/review` 覆盖率改为封闭分类账**  
   为每个 chunk 记录身份、缺口原因，并独立报告读取范围与最终评论，使审查覆盖透明可审计。  
   🔗 https://github.com/QwenLM/qwen-code/pull/9768

4. **#9794 `/review` 以类型化契约向客户端报告发现**  
   新增 `report_findings` 核心工具，用结构化数据代替 Markdown，字段与枚举严格对齐评审产物。  
   🔗 https://github.com/QwenLM/qwen-code/pull/9794

5. **#9273 `/review` 增加 capture-tui 工具**  
   在私有 tmux server 中运行命令，输出 `.ans` 并可选渲染 PNG，为渲染回归提供可验证证据。  
   🔗 https://github.com/QwenLM/qwen-code/pull/9273

6. **#9496 将 MCP 服务器配置拆分为独立模块**  
   延续配置模块拆分模式，旧位置保留 re-export，调用方零迁移成本，降低大型配置模块复杂度。  
   🔗 https://github.com/QwenLM/qwen-code/pull/9496

7. **#9389 设置向导推荐实时模型列表**  
   当 provider 支持时，通过 `GET {baseUrl}/models` 动态拉取当前可用模型，替代发布时冻结的静态列表。  
   🔗 https://github.com/QwenLM/qwen-code/pull/9389

8. **#9657 Web Shell 紧凑 Agent 活动摘要**  
   将思考、工具调用、并行 agent 折叠为摘要，展开后保留原有明细，交互层级更清爽。  
   🔗 https://github.com/QwenLM/qwen-code/pull/9657

9. **#9719 VS Code 扩展默认采用 WebShell transcript 作为时间线**  
   通过共享 SDK 将 ACP 通知桥接到 WebShell 渲染器，统一 IDE 与 Web 的会话展示。  
   🔗 https://github.com/QwenLM/qwen-code/pull/9719

10. **#9802 Web Shell 增加异步提交准备钩子**  
    宿主可在本地命令处理后、提交门禁前替换待发送 prompt 与输入注解，扩展嵌入式场景可定制性。  
    🔗 https://github.com/QwenLM/qwen-code/pull/9802

## 功能需求趋势
- **审查流程工程化**：`/review` 相关 issue/PR 占比最高，社区强烈希望将审查的编排、重叠检测、结果上报与工具链深度集成，实现可复现、可验证、可恢复。
- **多渠道接入**：Telegram、DingTalk、Web Shell 等非 CLI 入口持续扩充，远程协作与自动化工单成为刚需。
- **渲染与交互体验**：Windows 中文显示、TUI 闪烁、Markdown 加粗 CJK 标点渲染等前端问题频繁出现，对终端/Web 渲染质量要求提高。
- **配置与权限安全**：`permissions.allow` 未真正限制模型工具集、值域分散手抄、PAT 凭据隔离等问题，显示用户对安全配置的完整性与一致性日益敏感。
- **会话与后台管理**：后台 Agent 健康跟踪、会话生命周期持久化、Telegram 会话同步等需求，指向更可靠的长时间运行与断线恢复能力。

## 开发者关注点
- **稳定性痛点**：流式响应无活动超时（#5975）、斜杠命令间歇失效（#9821）等高频 bug 直接影响日常使用，开发者期望团队优先修复。
- **权限配置落地**：用户发现尽管配置了 allowlist，完整工具集仍会发送至模型（#9827），认为“配置即承诺”应严格执行。
- **跨平台适配**：Windows 终端中文输入显示问题（#8625）长期存在，反映跨端渲染测试不足。
- **认证与安全**：Vertex AI ADC 认证不可用（#9016）、CI 中 PAT 凭据与不可信代码共存（#9089）等安全问题引发关注。
- **维护性焦虑**：大量重复的值域定义（#9145）与手写补丁（ink 补丁，#8662）导致修复风险，社区呼吁通过重构和单一数据源减少长期累积的工程债。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*