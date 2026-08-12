# AI CLI 工具社区动态日报 2026-08-13

> 生成时间: 2026-08-12 23:05 UTC | 覆盖工具: 7 个

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

# AI CLI 工具社区动态横向对比分析报告

**报告日期：2026-08-13**

> **数据说明**：本次报告基于 Claude Code、OpenAI Codex、Gemini CLI、GitHub Copilot CLI、Kimi Code CLI、OpenCode、Qwen Code 七个项目的社区动态摘要。其中 OpenAI Codex、Kimi Code CLI、OpenCode、Qwen Code 有完整的社区数据；Claude Code、Gemini CLI、GitHub Copilot CLI 在本次数据收集中未提供动态摘要（已标注为"数据未收录"）。


## 1. 生态全景

AI CLI 工具正从"单点代码助手"快速演变为**覆盖编码、代理协作、桌面端与云端调度的完整开发平台**，头部工具均以"日更"节奏持续迭代。当前社区反馈的核心矛盾集中在**平台稳定性（尤其 Windows 桌面端）**、**付费/计费系统透明度**和**跨会话上下文记忆能力**三大方向。工具之间在底层技术路线上分化明显：OpenAI Codex 基于 Rust 工具链深耕基础设施，OpenCode 以"多模型聚合网关"姿态快速兼容各家新模型，Qwen Code 则依托阿里云生态（Vertex AI、DashScope）加速桌面端与 WebShell 布局。与此同时，MCP（Model Context Protocol）正从"可选特性"演变为各工具的标准配置能力，2026 新协议版本已开始落地。


## 2. 各工具活跃度对比

| 工具 | 状态 | Issues 数 | PR 数 | Release 数 | 最热议题（评论数） |
|---|---|---|---|---|---|
| **OpenAI Codex** | 高活跃 | 50（更新） | 49（更新） | 1（rust-v0.148.0-alpha.9） | #20214 Windows 卡顿（97 评论，82 👍） |
| **OpenCode** | 高活跃 | 10 个热点（总数未披露） | 10 个重要进展（总数未披露） | 1（v1.18.17） | #14273 免费额度误判（40 评论） |
| **Qwen Code** | 高活跃 | 10 个热点（总数未披露） | 10 个重要进展（总数未披露） | **5**（CLI 2 个 + Desktop 2 个 + 1 个冒烟测试） | #7040 自动记忆召回 RFC（10 评论） |
| **Kimi Code CLI** | 稳步推进 | 1（更新活跃） | 2（更新活跃） | 0 | #1283 Memory System 功能请求（35 评论） |
| **Claude Code** | — | 数据未收录 | 数据未收录 | 数据未收录 | — |
| **Gemini CLI** | — | 数据未收录 | 数据未收录 | 数据未收录 | — |
| **GitHub Copilot CLI** | — | 数据未收录 | 数据未收录 | 数据未收录 | — |


## 3. 共同关注的功能方向

### 3.1 跨会话记忆与持久上下文 — *最强共性需求*

| 工具 | 具体诉求 |
|---|---|
| **Kimi Code CLI** | #1283 请求实现自动 + 手动双层记忆系统，持续讨论近半年（35 评论），是当前最集中的功能期待 |
| **Qwen Code** | #7040 RFC 讨论自动记忆召回的时机、质量与遥测，已进入 PR2 设计修订阶段，说明已在产品路线图内 |
| **OpenCode** | 会话压缩保留完整最新轮次（v1.18.17 已修复），但社区仍在反馈 compact 后上下文丢失问题 |

**信号**：跨会话记忆已不是"锦上添花"，而是各工具下一阶段竞争的制高点。

### 3.2 会话恢复与稳定性

| 工具 | 具体诉求 |
|---|---|
| **OpenAI Codex** | #37398 打开本地会话需等待 5 秒固定超时（实际读取仅需 200ms） |
| **OpenCode** | #42110 订阅升级前的旧会话永久卡死在重试循环 |
| **Qwen Code** | #8678 大会话恢复超时后丢失当前会话（P1，已被 PR #8691 修复） |

**信号**：长会话、断点续跑、升级/迁移场景下的"会话完整性"是开发者对 CLI 工具的基本信任底线。

### 3.3 Windows 平台适配 — *Codex 独有痛点，其他工具需引以为戒*

| 工具 | 具体诉求 |
|---|---|
| **OpenAI Codex** | 4 个 Windows 相关问题同时登榜：App 卡顿（97 评论）、Computer Use 截屏失败、EPERM 权限失败（ACL 约束）、安装引导卡死。Windows 问题占比达 40%（4/10） |

**信号**：桌面化是趋势，但 Windows 的碎片化环境（Win10/11、WSL2、WindowsApps ACL）对 Electron/WebView 类应用是巨大挑战。OpenCode 的 Linux 僵尸进程问题（#41806）也说明跨平台稳定性仍有系统性短板。

### 3.4 MCP 能力增强

| 工具 | 具体诉求 |
|---|---|
| **OpenAI Codex** | PR #38245 为 MCP 服务器增加动态 HTTP Header 助手（支持 shell 命令动态生成请求头） |
| **OpenCode** | 提出 per-MCP-server 信任配置 + 远程 MCP OAuth token 自动刷新 |
| **Qwen Code** | PR #8992 新增 MCP 2026 core 客户端切片 + WebShell Apps 宿主 |

**信号**：MCP 正从"支持协议"走向"生态深度集成"——动态鉴权、协议协商、资源校验成为标配能力。

### 3.5 新模型快速适配

| 工具 | 具体诉求 |
|---|---|
| **OpenCode** | Gemini 3 Pro 函数调用失败（33 评论，14 👍）、DeepSeek V4 Flash 免费额度异常、Kimi K2.5/MiniMax 兼容问题 |
| **Qwen Code** | 新增 Kimi 与小米 MiMo 提供商、Anthropic 模型 ID 兼容与流安全保护 |
| **Codex** | 社区用户指出"GPT-5.6 已可用但 IDE Context 是坏的"，新模型能力与扩展稳定性脱节 |

**信号**：模型迭代速度已超过 CLI 工具的适配速度。多模型聚合能力正在成为 OpenCode 一类"中立型"工具的核心竞争力。


## 4. 差异化定位分析

| 维度 | OpenAI Codex | OpenCode | Qwen Code | Kimi Code CLI |
|---|---|---|---|---|
| **功能侧重** | 桌面 App + IDE 集成 + Computer Use（UI 自动化）；深度打磨基础设施（credential broker、gRPC 会话、时序化会话历史） | 多模型聚合网关 + 自有计费平台（Zen/Go）+ Desktop 与 CLI 双端；对社区新模型适配响应最快 | CLI + Desktop 双线并行；WebShell 与后台代理/多代理编排；深度绑定阿里云生态（Vertex AI、DashScope、DSW EAS） | 轻薄 CLI 工具，专注核心交互体验；社区规模较小但方向聚焦 |
| **目标用户** | OpenAI 生态重度用户、Windows 桌面开发者、需要 IDE 上下文自动附带的日常开发者 | 多模型比较型用户、追求最新模型的早期采用者、对计费敏感的独立开发者 | 阿里云/GCP 用户、需要无人值守长任务与多代理协作的中大型项目团队 | 偏好轻量工具的开发者、Moonshot/Kimi 生态用户、中文开发者 |
| **技术路线** | Rust 工具链、桌面 GUI（疑似 Electron/WebView）、gRPC 通信、凭据代理架构 | TypeScript 全栈、SDK 聚合层（Groq/Mistral/xAI/DeepSeek）、业务侧网关（Zen/Go）、SolidJS 桌面 UI | Rust 核心 + 桌面/浏览器混合架构、MCP 2026 先行者、workflow 级多代理编排、Chromium 桥接 | Python 实现、web runner 子进程模型、轻量优先 |
| **迭代速度** | 每日预发布（alpha.9 节奏），PR 密集（49 条/日），但 Windows 老大难问题数月未解 | 版本节奏稳定（v1.18.x），自动化 bot 贡献占比高（SDK 兼容类 PR 大量由 bot 提交） | 日发 5 版（含 desktop 系列），迭代全生态最激进 | 非每日发版，以社区 PR 驱动为主 |


## 5. 社区热度与成熟度

### 第一梯队：OpenAI Codex — 体量最大，但"痛并热闹着"
50 Issue / 49 PR 的日更新量显著领先；最热 Issue 达 97 评论、82 👍，且是"连续数月未解决"的 Windows 卡顿问题。社区热度高但被稳定性问题消耗严重，属于典型的"高关注度 + 高期待落差"状态。

### 第一梯队：OpenCode — 高活跃，付费问题引发信任危机
虽然热点 Issue 评论数绝对值不如 Codex，但**计费相关的多个问题同时发酵**（免费额度误判、订阅后旧会话卡死、区域限制），用户情绪激烈且直接指向信任层面。相比之下，其 SDK 兼容 PR 大量来自自动化 bot，说明核心人力有限，但有社区协作网络在支撑。

### 第二梯队：Qwen Code — 快速迭代，工程化能力突出
日发 5 版，PR 涵盖 MCP 2026、内存防护、Git worktree 安全等深度工程议题。社区规模中等但问题质量高（RFC 类、P1 级），整体处于**从"能用"走向"可靠"的快速爬坡期**。

### 第三梯队：Kimi Code CLI — 社区规模小，但进入良性协作期
过去 24 小时仅 1 个活跃 Issue、2 个活跃 PR，且均由同一位社区开发者（@Ricardo-M-L）提交。社区处于早期阶段，但已出现外部开发者主动修复细粒度 bug 的积极信号，说明项目进入了生态自生长的起点。

> **注**：Claude Code、Gemini CLI、GitHub Copilot CLI 本次无数据收录，无法评估其当前活跃度。


## 6. 值得关注的趋势信号

### 6.1 桌面端是兵家必争之地，但 Windows 是"翻车重灾区"
Codex 的 Windows 问题（卡顿、Computer Use 缺陷、安装引导失败）已占据其 Issue 榜半壁江山；OpenCode 的 Desktop 端也存在数据库迁移崩溃；Qwen Code 桌面版同样在快速迭代修复。**行业正在经历"从终端到 GUI"的阵痛期**，Windows 的兼容性治理（ACL、权限模型、多版本碎片化）将成为未来 6 个月的竞品分水岭。

### 6.2 "无人值守"和"长任务"开始成为硬需求
Qwen Code 中文用户明确要求"能跑整夜/数天的长任务"并称 Kimi "完胜"；Codex 在探索 gRPC 断线重连；OpenCode 在修复无限重试。**AI CLI 从"交互式结对编程"走向"后台自主代理"的范式转移已明确出现**，但前提是会话恢复、错误熔断、进度可观测三者必须先行。

### 6.3 计费与额度透明度将成为付费 CLI 的信任基石
OpenCode 多条高热度 Issue 都在反映同一件事：**用户付了钱，但系统不认**。误判免费额度、订阅状态不同步、区域限制不透明——这些问题出现在"AI 编程工具开始大规模商业化"的当下，具有行业警示意义。任何引入自有计费体系的 CLI 工具，都需要将"额度状态可查、扣费逻辑可解释"作为一等公民来设计。

### 6.4 MCP 从"支持协议"走向"生态深度集成"
2026 新协议版本已在 Qwen Code 落地，Codex 在 MCP 服务器侧增强动态鉴权，OpenCode 社区在推动 MCP 信任配置与 OAuth 刷新。**MCP 正在复制 npm/PyPI 的生态演化路径：先解决"能不能连"，再解决"连得安不安全、管不管得住"**。开发者可关注各工具对 MCP 2026 的跟进速度作为选型维度之一。

### 6.5 多模型适配能力 = 新竞争力
OpenCode（Kimi/MiniMax/Gemini/DeepSeek）、Qwen Code（Kimi/小米 MiMo/Anthropic）、Codex（GPT-5.6 与 IDE Context 脱节）——**模型即插即用已不是加分项，而是基础能力**。对于开发者而言，选择"中立型"聚合工具还是"绑定型"生态工具，将直接影响使用最新模型的时效性和切换成本。


## 总结

2026 年 8 月中旬的 AI CLI 赛道呈现出"基础设施趋同、体验分化"的竞争格局：各工具都在会话管理、MCP、多模型接入上投入重兵，但真正的差异化在**平台稳定性（Windows/桌面端）、长任务可靠性和商业模式透明度**三个层面。对开发者而言，选型不应只看模型能力或功能列表，更应关注社区反馈中暴露的"信任类"问题（计费误判、会话丢失、升级回归）——这些才是决定日常开发效率与心情的关键变量。

---

*报告完*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截止 2026-08-13）

> 注：本次快照中所有 PR 均处于 Open 状态，暂未看到合并闭环；PR 评论数为 undefined，按仓库提供的"评论数排序"参考热度。

---

## 1. 热门 Skills 排行

### 🥇 #1298 — 修复 skill-creator 评估链路（run_eval.py 恒报 0% recall）
- **功能**：修复 `run_eval.py` 及其下游 `run_loop.py` / `improve_description.py` 的评估失效问题——所有 skill 描述无论内容如何都得到 `recall=0%`，导致优化循环在"对着噪声做优化"。
- **社区热点**：直指 #556（12 条评论、7 👍）和 #1169 两个高热度 Bug，10+ 独立复现。修复涵盖：将 eval artifact 安装为真实 skill、Windows 流读取、触发检测、并行 worker。
- **状态**：Open。
- 链接：https://github.com/anthropics/skills/pull/1298

### 🥈 #514 — document-typography 技能（文档排版质检）
- **功能**：拦截 AI 生成文档的常见排版问题：孤儿单词换行（1-6 个单词溢出到下一行）、段落标题滞留页尾（widow）、编号错位。
- **社区热点**：覆盖所有 Claude 生成的文档场景，用户很少主动要求排版质量——这是一类"AI 默认应该做好"的隐性能力，讨论度高。
- **状态**：Open。
- 链接：https://github.com/anthropics/skills/pull/514

### 🥉 #83 — skill-quality-analyzer + skill-security-analyzer（元技能）
- **功能**：新增两个"关于技能的技能"：质量分析器从结构/文档（20%）、示例、资源等五个维度评估 SKILL.md；安全分析器用于技能安全审查。
- **社区热点**：与 #492 信任边界 Issue 呼应，社区开始关注技能本身的质量与安全审计，是生态治理方向的热门探索。
- **状态**：Open。
- 链接：https://github.comanthropics/skills/pull/83

### #1367 — self-audit 技能（交付前审核门禁）
- **功能**：交付前先做机械性文件验证（每个声称的输出文件是否真实存在），再按损坏严重度优先级做四维推理审核。通用性强，适配任何项目/技术栈/模型。
- **社区热点**：与 #1385 的"三段式推理质量门禁"提案联动，代表社区对 AI 输出质量管控的持续诉求。
- **状态**：Open。
- 链接：https://github.com/anthropics/skills/pull/1367

### #723 — testing-patterns 技能（测试模式全景）
- **功能**：覆盖完整测试栈：Testing Trophy 模型、单元测试 AAA 模式、React 组件测试（Testing Library）、查询优先原则等。
- **社区热点**：测试是 AI 生成代码质量的刚需方向，技能体系化程度高，讨论活跃。
- **状态**：Open。
- 链接：https://github.com/anthropics/skills/pull/723

### #568 — ServiceNow 平台技能（企业级大而全）
- **功能**：横跨 ITSM、ITOM、ITAM/SAM、FSM、HRSD/CSM、SPM/PPM、漏洞响应、安全事件响应、IntegrationHub 的 ServiceNow 平台助理，非窄脚本助手。
- **社区热点**：企业平台类 Skill 的代表性 PR，直到 08-12 仍在更新，说明作者持续维护、社区持续关注。
- **状态**：Open。
- 链接：https://github.com/anthropics/skills/pull/568

### #525 — pyxel 技能（复古游戏开发）
- **功能**：为 pyxel-mcp（Pyxel 复古游戏引擎的 MCP 服务器）编写，覆盖 write → run_and_capture → inspect → iterate 工作流。
- **社区热点**：作者 @kitao 是 Pyxel 引擎本身的原作者，自带社区影响力；游戏开发是创意类技能的高人气赛道。
- **状态**：Open。
- 链接：https://github.com/anthropics/skills/pull/525

### #541 — 修复 docx 技能 tracked change 的 w:id 冲突
- **功能**：修复带书签的文档添加修订时损坏的问题——OOXML 中 `w:id` 是书签、修订、批注、移动范围共享的 ID 空间，硬编码低 ID 会冲突。
- **社区热点**：文档类技能（docx/pdf/odt）是 PR 密集区，#538（pdf 大小写

---



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报

**日期：2026-08-13** | 数据来源：github.com/openai/codex

---

## 今日速览

过去 24 小时 Codex 仓库共更新 50 条 Issue 与 49 条 PR，Windows 平台稳定性问题持续占据社区焦点，其中“Windows 上 Codex App 频繁卡顿”以 97 条评论、82 个 👍 成为最热议题。版本方面发布 `rust-v0.148.0-alpha.9` 预发布构建；PR 侧则以大量基础设施类改动为主（会话历史时间戳、MCP 服务器能力增强、插件指标采集等），并合入了实验性 credential broker 集成。

---

## 版本发布

### rust-v0.148.0-alpha.9
- **链接**：https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.9
- **内容**：发布版本 `0.148.0-alpha.9`，未附带详细变更说明，属于 Rust 工具链的预发布迭代构建。

---

## 社区热点 Issues（10 个）

### 1. #20214 — Codex App 在 Windows 11 Pro 上频繁卡顿/掉帧
- **链接**：https://github.com/openai/codex/issues/20214
- **状态**：OPEN ｜ 评论 97 ｜ 👍 82
- **重要性**：连续数月未解决的最热 Issue。用户配置（Ryzen 5 5600 + 32GB RAM）远超最低要求，但应用仍出现明显卡顿。高赞与高评论数表明该问题波及大量 Windows 用户，是当前社区第一大痛点。

### 2. #25178 — Windows Computer Use 截屏失败（SetIsBorderRequired 报错）
- **链接**：https://github.com/openai/codex/issues/25178
- **状态**：OPEN ｜ 评论 25 ｜ 👍 13
- **重要性**：Computer Use 在 Windows 10 22H2 上可列出窗口、发送键盘输入，但任何请求截屏的 `get_window_state` 调用都会在捕获前报 `0x80004002 不支持此接口`。说明 Windows 平台 Computer Use 的 UI 自动化层存在系统性兼容缺陷。

### 3. #31553 — VS Code 扩展更新后不再自动附带 IDE 上下文
- **链接**：https://github.com/openai/codex/issues/31553
- **状态**：OPEN ｜ 评论 17 ｜ 👍 12
- **重要性**：远程容器（.vscode-server）场景下，扩展 26.623.141536 更新后 IDE 上下文自动包含功能失效，直接影响远程开发者的核心工作流，属于高频回归类问题。

### 4. #37398 — 打开本地未加载会话需等待约 5 秒超时
- **链接**：https://github.com/openai/codex/issues/37398
- **状态**：OPEN ｜ 评论 14 ｜ 👍 9
- **重要性**：会话实际读取/恢复耗时不足 200ms，但固定的 owner-discovery 超时导致用户感知延迟高达 5 秒。这是一个典型的非必要等待问题，影响桌面端日常使用体验。

### 5. #37415 — Windows Computer Use 因 EPERM 失败；沙箱提权在 WindowsApps ACL 上失败
- **链接**：https://github.com/openai/codex/issues/37415
- **状态**：OPEN ｜ 评论 13 ｜ 👍 4
- **重要性**：Computer Use 在 Windows 上运行时 `spawn EPERM`，且提升沙箱权限时因 WindowsApps 目录 ACL 约束失败。与 #25178、#37743 共同构成 Windows Computer Use 的三连击问题。

### 6. #33967 — ChatGPT for Windows 卡在“Complete Windows setup”无法进入受限模式
- **链接**：https://github.com/openai/codex/issues/33967
- **状态**：OPEN ｜ 评论 12 ｜ 👍 0
- **重要性**：用户完全无法完成桌面端初始设置，属于阻断型（blocker）安装缺陷，影响新用户上手。

### 7. #34920 — IDE Context 在 26.715.x 扩展中报 RPC 序列化错误
- **链接**：https://github.com/openai/codex/issues/34920
- **状态**：OPEN ｜ 评论 10 ｜ 👍 5
- **重要性**：影响 VS Code 与 Devin 多个 IDE，涉及 26.707.91948、26.715.31925、26.715.61943 三个版本。用户指出“GPT-5.6 已可用但 IDE Context 是坏的”，说明新模型能力与扩展稳定性脱节。

### 8. #35419 — WSL2 下 VS Code IDE 上下文自动禁用且选区文本丢失
- **链接**：https://github.com/openai/codex/issues/35419
- **状态**：OPEN ｜ 评论 6 ｜ 👍 10
- **重要性**：WSL2 是大量 Linux 开发者的首选环境，扩展 26.721.41059 在该环境下自动禁用 IDE Context，且选中文本不随请求附加，对日常编码辅助影响显著。

### 9. #23517 — 功能请求：增加禁用自动滚动（autoscroll）的开关
- **链接**：https://github.com/openai/codex/issues/23517
- **状态**：OPEN ｜ 评论 5 ｜ 👍 8
- **重要性**：产品体验类需求，用户反馈长消息响应时自动滚动造成视觉不适，希望桌面 App 提供与终端一致的滚动控制能力。评论虽少但 👍 数较高，代表一批用户的共同诉求。

### 10. #37493 — macOS 桌面版 ≥26.730 在 16GB Apple Silicon 上启动崩溃循环
- **链接**：https://github.com/openai/codex/issues/37493
- **状态**：CLOSED ｜ 评论 3
- **重要性**：V8 “JavaScript heap out of memory” 导致启动后 6–15 秒崩溃，同一构建在 48GB 机器上正常，疑似内存预算与设备内存不匹配。虽然已关闭，但反映了桌面 App 在低内存 Mac 上的适配风险。

---

## 重要 PR 进展（10 个）

### 1. #38272 — 为会话历史条目添加创建时间戳
- **链接**：https://github.com/openai/codex/pull/38272
- **要点**：为本地生成的 user/developer/agent/tool-output 条目添加毫秒级 Unix 创建时间，并在后续请求中保留已有时间戳。有助于会话回放、审计与排序的准确性。

### 2. #38270 — 后端客户端增加按线程（per-thread）用量查询
- **链接**：https://github.com/openai/codex/pull/38270
- **要点**：新增 `Client::get_thread_usage`，可查询线程的预估积分/美元消耗，并暴露模型、推理强度、速度、token 等可选维度。为用量可视化与限额管理打基础。

### 3. #38268 — 从 `skills.read` 暴露执行器技能根目录
- **链接**：https://github.com/openai/codex/pull/38268
- **要点**：执行器（executor）级技能可包含捆绑脚本，本次在 `skills.read` 响应中新增 `skill_root` 字段，便于调用方定位技能目录中的资源。

### 4. #29752 — 集成实验性凭据代理（credential broker）
- **链接**：https://github.com/openai/codex/pull/29752
- **要点**：合入代理持有的凭据代理功能，可为子进程替换为占位凭据，并在整个命令生命周期中传递。对多子进程场景的凭据隔离有重要意义，是本次唯一由人类作者（@viyatb-oai）主导的核心架构 PR。

### 5. #38265 — Windows 受管代理使用有界回退端口
- **链接**：https://github.com/openai/codex/pull/38265
- **要点**：Windows HTTP/SOCKS5 代理端口被占用时，改为在协议首选端口范围内扫描，并独立预留 HTTP 与 SOCKS5 监听器，避免端口冲突导致的功能异常。

### 6. #38257 — 宿主重启后自动重连 gRPC code-mode 会话
- **链接**：https://github.com/openai/codex/pull/38257
- **要点**：gRPC 宿主停止后自动重开缓存的 code-mode 会话，序列化并发重连并协调关闭；cell ID 按新宿主代际隔离，防止回调错乱。

### 7. #38245 — 为 MCP 服务器增加动态 HTTP Header 助手
- **链接**：https://github.com/openai/codex/pull/38245
- **要点**：本地 streamable HTTP MCP 服务器可通过配置 shell 命令动态生成请求头（每次连接执行一次并缓存），显著提升 MCP 服务器对接动态鉴权/环境信息的能力。

### 8. #38244 — 按 rollout ID 解析分页线程历史
- **链接**：https://github.com/openai/codex/pull/38244
- **要点**：修复 `thread/revert` 后逻辑线程 ID 不变但 rollouot 已切换，导致按线程 ID 读取历史可能访问错误 rollout 的问题，改为集中解析当前 rollout。

### 9. #38242 — 缓存稳定的活动单元格布局测量值
- **链接**：https://github.com/openai/codex/pull/38242
- **要点**：对高度稳定的活动 transcript 单元格复用期望/渲染高度，仅在 cell 身份、版本、宽度、渲染模式或语法主题变化时失效。直接降低渲染

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-08-13）

## 今日速览

过去 24 小时，Kimi Code CLI 没有新版本发布。社区方面，备受关注的 **Memory System（跨会话持久上下文）** 功能请求（#1283）持续活跃，累计收获 35 条评论，成为当前最集中的功能期待；同时，两个来自社区开发者 Ricardo-M-L 的 bug 修复 PR 获得更新，主要围绕工具调用摘要格式与 web 运行器稳定性。整体动态体现出社区对**跨会话记忆能力**与**细节稳定性**的双重关注。

## 版本发布

过去 24 小时无新版本发布。

## 社区热点 Issues

> 说明：受数据源限制，过去 24 小时内更新活跃的 Issue 共 1 个，以下为全部高价值条目。

### #1283 [功能请求] Memory System - 跨会话持久上下文

- **作者**: @CatKang
- **创建**: 2026-02-27
- **更新**: 2026-08-12
- **评论**: 35 | 👍: 0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/1283

**为什么重要**：这是社区对 Kimi Code CLI 最核心的功能期待之一。该 Issue 请求实现一套完整的记忆系统，既包含 AI 自动管理的笔记（自动记忆），也支持用户手动定义的指令（手动记忆），以便跨会话保留项目模式、用户偏好和有用上下文。由于涉及会话机制、存储方案、隐私控制等多个方面，该需求自 2 月提出以来持续讨论近半年， 35 条评论说明开发者对方案细节有较高参与度。

**社区反应**：虽然 👍 数暂为 0，但讨论热度高，社区在该功能上的沟通集中在如何平衡自动化记忆与用户控制权，以及如何与现有 CLI 工作流平滑集成。

## 重要 PR 进展

> 说明：过去 24 小时内更新活跃的 PR 共 2 个，以下为全部重要进展。

### #2449 修复(string): shorten_middle 在长度检查前移除换行符

- **作者**: @Ricardo-M-L
- **创建**: 2026-06-13
- **更新**: 2026-08-12
- **评论**: 无
- **链接**: https://github.com/MoonshotAI/kimi-cli/pull/2449

**修复内容**：`shorten_middle(text, width, remove_newline=True)` 被 `extract_key_argument` 用于渲染工具调用关键参数的**单行摘要**。但原实现会在短输入时提前返回，导致换行符尚未被剥离。该 PR 将换行符清理逻辑提前到长度检查之前，确保所有输入都能得到真正的单行摘要。这个修复能显著提升日志和调试输出中工具调用摘要的可读性。

### #2324 修复(web): 处理 SessionProcess.send_message 中的 BrokenPipeError

- **作者**: @Ricardo-M-L
- **创建**: 2026-05-19
- **更新**: 2026-08-12
- **评论**: 无
- **链接**: https://github.com/MoonshotAI/kimi-cli/pull/2324

**修复内容**：在 `src/kimi_cli/web/runner/process.py` 中，`SessionProcess.send_message` 调用 `start()` 之后向 `process.stdin` 写入数据，但未考虑子进程在此期间可能已退出的情况。如果子进程意外退出，`write` 和 `drain()` 会触发 `BrokenPipeError`，导致整个 web 运行器崩溃。该 PR 为写入过程增加守护，避免因子进程退出而引发未捕获异常，提升了 web 模式下进程通信的稳健性。

## 功能需求趋势

- **跨会话记忆系统**：当前最醒目的功能需求。社区希望 CLI 能像“AI 助手”一样记住项目模式、用户偏好和关键上下文，从而减少重复描述，提升连续任务执行效率。该需求已从简单“记忆上下文”扩展为包含自动管理和手动管理的复合系统。
- **稳定性与健壮性修复**：从两个 PR 可以看出，社区对子进程通信错误、输出格式异常等边界情况的修复非常重视。这类细节直接影响用户在长时间、复杂场景下的使用体验。

## 开发者关注点

- **减少重复描述**：开发者希望在多会话中维持上下文，避免每次重新描述项目背景、代码风格或约束条件。
- **工具调用输出可读性**：对于 CLI 展示的工具调用关键参数，社区伙伴主动修复换行符问题，说明单行摘要等格式化细节是实际使用中的痛点。
- **Web/子进程通信可靠性**：`BrokenPipeError` 的修复表明，开发者在使用 web 交互模式时可能遇到进程崩溃、响应中断等问题，需要更稳健的异常兜底。
- **社区参与积极性**：本期两个活跃 PR 均由同一位社区开发者提交，反映出社区不仅提交功能需求，也越来越多地主动修复细粒度问题，是项目进入良性演进阶段的信号。

---
*以上数据来自 [github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)，统计时间节点为 2026-08-13。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-13

## 今日速览

过去 24 小时，OpenCode 社区的核心讨论集中在 **OpenCode Zen/Go 免费额度误判与订阅状态同步故障**，大量付费用户在余额充足或已订阅的情况下仍遭遇 “Free usage exceeded” 错误，该问题成为当前影响面最广的痛点。同时，项目发布了 **v1.18.17** 修复版本，改善会话压缩与自动重试机制；大量由自动化 bot 提交的 SDK 兼容性 PR（如 Groq、Mistral、xAI 的 reasoning effort 透传）也在此期间密集合并，标志着社区贡献趋于活跃。

---

## 版本发布

**v1.18.17**（过去 24 小时内发布）

- **核心修复**：
  - 会话压缩（Session compaction）现可保留完整的最新对话轮次，并能为小型模型生成更清晰的摘要。
  - 为 MERGE Gateway 添加了推理变体支持，相关模型选项现可正常工作（致谢 @MatthewFeroz）。
  - 自动会话重试增加次数上限并引入抖动机制，减少反复重试导致的卡死。

---

## 社区热点 Issues（10 个）

1. **[BUG] 免费额度被误判：付费用户频繁遭遇 “Free usage exceeded”**
   - [#14273](https://github.com/anomalyco/opencode/issues/14273)（评论 40，👍 1）
   - 用户在使用 Kimi K2.5 / MiniMax2.5 免费版本时向报错，且 Zen 账户存在 $3 余额仍被拦截。此问题自 2 月创建至今仍在更新，评论区持续累积，是最受关注的历史遗留问题之一。

2. **[BUG] Gemini 3 Pro 函数调用失败：缺少 thoughtSignature 支持**
   - [#4832](https://github.com/anomalyco/opencode/issues/4832)（评论 33，👍 14）
   - 使用 `gemini-3-pro-preview` 时，函数调用请求失败。👍 数高达 14，表明该模型在开发者中需求量很大，兼容性缺陷影响较广。

3. **[BUG] 付费仍触发免费额度限制（200 次限制未排除）**
   - [#33495](https://github.com/anomalyco/opencode/issues/33495)（评论 6）
   - 拥有余额 ≥$20 的账户仍被限制为免费档，收到的 429 错误表明计费系统未正确识别付费状态，引发对 Zen 计费逻辑的质疑。

4. **[BUG] DeepSeek V4 Flash Free 首次请求即报超额，无法使用**
   - [#42128](https://github.com/anomalyco/opencode/issues/42128)（评论 7，👍 5）
   - 全新账户首次调用 DeepSeek V4 Flash Free 即报 “Free usage exceeded”，疑似新用户免费额度默认值有误，或者策略发生了断裂，新用户冷启动体验受损。

5. **[BUG] 订阅 Go 后，存量会话仍卡死在 “Free usage exceeded” 重试循环**
   - [#42110](https://github.com/anomalyco/opencode/issues/42110)（评论 4）
   - 订阅 Go 并添加 token 后新会话可正常使用，但升级前活跃的旧会话永久卡在重试循环中，无法通过任何操作恢复。该问题直接影响用户工作流，情绪反应强烈。

6. **[BUG] 订阅 Go 后 DeepSeek 仍显示不可用/受限**
   - [#42132](https://github.com/anomalyco/opencode/issues/42132)（评论 4）
   - 用户购买了 Go 订阅后，聊天仍提示额度超限；且 DeepSeek for Go 仅限中国大陆使用，用户主力模型无法切换，反馈了国际化/区域限制对非大陆用户的困扰。

7. **[BUG] Linux 下 OpenCode 启动时 git 子进程未被回收导致无限卡死**
   - [#41806](https://github.com/anomalyco/opencode/issues/41806)（评论 3）
   - TUI 正常渲染但 Enter 无法开启会话，原因是初始化时 spawn 的 git 子进程退出后成为 `<defunct>` 僵尸进程，bootstrap 永不完成。属于 Linux 平台严重稳定性问题。

8. **[BUG] LLM 重试无上限，流式错误导致无限循环**
   - [#41848](https://github.com/anomalyco/opencode/issues/41848)（评论 3）
   - `RETRY_MAX_DELAY` 被设置为约 24 天，DeepSeek 流式错误触发后 UI 永远停留在 “Thinking...”，用户无法感知错误。重试机制缺乏熔断与用户反馈。

9. **[BUG] Desktop 端会话加载崩溃：no such column: project_id**
   - [#42170](https://github.com/anomalyco/opencode/issues/42170)（评论 2）
   - Desktop 1.18.17 启动时加载会话崩溃，sidecar 返回 500 错误。部分构建替换了 workspace 表结构导致字段缺失，属于桌面端数据库迁移问题。

10. **[FEATURE] 在聊天中渲染 Mermaid 图表**
    - [#3366](https://github.com/anomalyco/opencode/issues/3366)（评论 10，👍 26）
    - 用户希望 ChatGPT 类聊天 UI 能直接渲染 Mermaid 图（如流程示意、架构图），👍 26 为本次统计中最高，显示开发者对可视化能力有较高期待。

---

## 重要 PR 进展（10 个）

1. **[beta] refactor(app): 对齐 UI 组件与 SolidJS 最佳实践**
   - [#41977](https://github.com/anomalyco/opencode/pull/41977)（@Hona）
   - 重构 app、ui、session-ui 包，修复组件传参等模式问题，属于桌面端 UI 架构质量提升。

2. **[beta] fix(app): 服务端同步与 TUI 生命周期对齐**
   - [#41930](https://github.com/anomalyco/opencode/pull/41930)（@Hona）
   - 修复模型对话框空白、provider 只显示自定义项、agent 下拉丢失、Session 逃逸等一系列关联问题，根因定位为服务同步的生命周期设计缺陷。

3. **fix(core): 恢复 workspace.project_id 字段映射**
   - [#42169](https://github.com/anomalyco/opencode/pull/42169)（@DatScreamer）
   - 直接修复 #42170，恢复被新的 provider/binding schema 替换掉的 `project_id` 列，解决 Desktop 会话加载崩溃。

4. **[beta] fix(cli): 处理损坏的 stdio 管道（EPIPE）**
   - [#41968](https://github.com/anomalyco/opencode/pull/41968)（@Hona）
   - 修复后台服务 stdout/stderr 消费者退出时，写日志触发 EPIPE 导致整个服务崩溃的问题，提升 CLI 稳定性。

5. **[contributor] fix(groq): 透传 reasoning effort（推理力度）参数**
   - [#42166](https://github.com/anomalyco/opencode/pull/42166)（@opencode-agent[bot]）
   - 放宽 Groq SDK 的枚举限制，使任意字符串可透传到 provider，并添加回归测试。同类 PR 还包括 Mistral（#42164）和 xAI（#42160），体现对新型推理模型参数的支持补齐。

6. **[beta] feat(app): 非模态设置页重新设计**
   - [#40845](https://github.com/anomalyco/opencode/pull/40845)（@Hona）
   - 重构设置导航，拆出外观与通知独立页面，新增 Projects 和 Extensions 视图并接入真实服务器配置与 MCP 状态，改善桌面端设置体验。

7. **[contributor] fix(catalog): 在 lab 路由下提供 app shell**
   - [#42159](https://github.com/anomalyco/opencode/pull/42159)（@kitlangton）
   - 修复 Cloudflare Assets 对内部路径的 HTML canonicalization 重定向问题，使目录应用 shell 能正确在 `dev.opencode.ai/lab/catalog` 访问。

8. **fix(core): 会话标题使用 catalog 小型模型**
   - [#36563](https://github.com/anomalyco/opencode/pull/36563)（@rekram1-node）
   - 标题生成优先使用 `Catalog.model.small(provider)`，无显式模型时自动降级到小型模型，提升标题生成性能与成本效率。

9. **fix(opencode): Process.stop() 增加 SIGKILL 回退**
   - [#36559](https://github.com/anomalyco/opencode/pull/36559)（@beowulfof）
   - 原先只发送 SIGTERM 且无超时，现补充 SIGKILL 回退机制，防止进程无法正常终止。

10. **[contributor] fix(xai): 透传 reasoning effort（推理力度）**
    - [#42160](https://github.com/anomalyco/opencode/pull/42160)（@opencode-agent[bot]）
    - 同时覆盖 xAI Chat 与 Responses 两套 API，支持 `xhigh` 等非标准推理力度值，适配新型 grok 模型。

---

## 功能需求趋势

从过去 24 小时的 Issue 与活跃讨论中，社区关注的功能方向较为集中：

- **计费与额度系统透明化**：关于 “Free usage exceeded” 的讨论贯穿多条 Issue，用户对免费额度判定、余额与订阅状态同步、区域限制（DeepSeek for Go 仅中国）的困惑是当前第一大需求。
- **新模型与 API 兼容适配**：Gemini 3 Pro、DeepSeek V4 Flash、MiniMax、Kimi K2.5、Azure 大模型（gpt-5.6-luna/sol 等）均有兼容性报障，说明社区积极尝试最新模型，期待 OpenCode 加速适配。
- **MCP 能力增强**：提出 per-MCP-server 信任配置（#40111）与远程 MCP 服务器 OAuth token 自动刷新（#34582），表明开发者对 MCP 安全性和可用性提出更高要求。
- **会话稳定性**：compact 后上下文丢失、压缩退化为重复输出、无限重试等问题频发，会话管理的鲁棒性成为明显短板。
- **桌面端/容器集成体验**：VSCode Server 中剪贴板失效、项目文件夹混淆（foo/foo2 无法区分）、Linux 下僵尸进程卡死等问题，反映多环境适配仍待完善。

---

## 开发者关注点

- **付费被误伤是当前最高频的抱怨**：不止一位用户表示已购买 Go 订阅或 Zen 余额充足，却仍被提示 “Free usage exceeded”，甚至旧会话卡死无法恢复。此类问题直接破坏信任，开发者情绪明显。
- **自动重试机制形同虚设，甚至变成灾难**：24 天 max delay、无上限重试、UI 永远 “Thinking” —— 开发者期望的是“快速失败 + 明确报错”，而非静默循环。
- **上下文压缩功能可靠性不足**：中文社区用户亦反馈 `/compact` 后模型忘记上下文、输出结构异常（#41268），该问题在多个版本中反复出现。
- **对内置默认配置的敏感度提高**：MiniMax 模型落到 Claude 默认提示词（#41031）、Gemini 3 Pro 函数调用缺参（#4832），用户期望 provider 模型差异化支持更加精细。
- **CI/协作类小问题也进入视野**：如 close-prs 工作流静默失败（#42153）、shell 输出分页保留尾部（#36554）等，反映社区已开始关注工程细节与协作效率改善。

---

*本日报由 AI 辅助整理，数据来源：[github.com/anomalyco/opencode](https://github.com/anomalyco/opencode)。*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

## Qwen Code 社区动态日报（2026-08-13）

### 1. 今日速览

Qwen Code 在过去 24 小时内发布了 5 个版本，包括 CLI 预览版和桌面版双更新，重点修复了 WebShell 会话导航安全性和桌面端项目内存作用域问题。社区侧，中文用户反馈"长任务无法自动运行"和图片加载崩溃回归成为焦点，同时后台代理协调缺陷、Vertex AI 认证问题等核心痛点持续发酵。PR 侧则涌现了 Kimi/小米 MiMo 新模型提供商支持、MCP 2026 协议实现等多方向进展。

### 2. 版本发布

过去 24 小时共发布 5 个版本：

- **v0.21.11-preview.0** — 修复 WebShell 会话导航安全性问题（prompt-safe session navigation），并新增 serve 会话连续性日志记录。[查看发布](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.11-preview.0)
- **v0.21.10-nightly.20260812.a64d1291d2** — 包含与 preview.0 相同的 WebShell 修复和 serve 日志增强。[查看发布](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.10-nightly.20260812.a64d1291d2)
- **desktop-v0.2.1** — 桌面版补丁：默认项目记忆作用域调整为工作区级别（#8856），并同步会话生命周期遥测。[查看发布](https://github.com/QwenLM/qwen-code/releases/tag/desktop-v0.2.1)
- **desktop-v0.2.0** — 桌面版 0.2 系列首个版本：修复 WebShell 会话历史分页稳定性（#8914），新增会话目录共享功能。[查看发布](https://github.com/QwenLM/qwen-code/releases/tag/desktop-v0.2.0)
- **dsw-eas-smoke-20260812-281542bfdc** — DSW EAS 基础设施冒烟测试构建，非生产版本，不发布 SWE 分数。[查看发布](https://github.com/QwenLM/qwen-code/releases/tag/dsw-eas-smoke-20260812-281542bfdc)

### 3. 社区热点 Issues（10 个）

1. **RFC：可靠自动记忆召回 — 时机、质量与遥测**（#7040，10 评论）
   自动记忆召回项目的状态追踪，PR2 已根据测量结果修订设计，是理解 Qwen Code 记忆功能演进的关键入口。[链接](https://github.com/QwenLM/qwen-code/issues/7040)

2. **长任务无法自动运行**（#8963，9 评论）
   中文用户反馈：无论 yolo 还是 auto 模式，运行需要整夜/数天的长任务时会卡住不动，并称 Kimi Code "完胜"。该问题直接指向无人值守场景的核心短板。[链接](https://github.com/QwenLM/qwen-code/issues/8963)

3. **[回归] 0.21.2+ 读取图片即崩溃**（#8957，8 评论）
   用户反馈从 0.21.1 升级后，读取图片瞬间崩溃，严重阻塞多模态工作流。已被标记 need-information 和 need-retesting。[链接](https://github.com/QwenLM/qwen-code/issues/8957)

4. **大会话恢复超时后丢失当前会话**（#8678，7 评论，P1）
   当大体积会话恢复超时时，serve 端应保留当前会话。PR1 已合并（#8691），实现超时契约、迟到请求安全和可观测性。[链接](https://github.com/QwenLM/qwen-code/issues/8678)

5. **Vertex AI 无法使用 Application Default Credentials 认证**（#9016，4 评论）
   Vertex AI 认证逻辑强制要求 API key，而任何 key 都会导致 401。ADC 正确配置后仍无法工作，影响 Google Cloud 用户。[链接](https://github.com/QwenLM/qwen-code/issues/9016)

6. **--approval-mode 和 --auth-type 从 --help 消失**（#8897，5 评论）
   CLI 接受的参数却不显示在帮助信息中，开发者难以发现这些重要选项。[链接](https://github.com/QwenLM/qwen-code/issues/8897)

7. **后台代理协调缺陷：重复工作、过早完成、send_message 无响应**（#8097，6 评论）
   多个后台 Explore 子代理并行时，父代理会重复子代理的工作，且 send_message 通信不可靠，影响多代理协作效率。[链接](https://github.com/QwenLM/qwen-code/issues/8097)

8. **tmux 分屏闪屏问题**（#8562，7 评论）
   MacBook 通过 iTerm2 SSH 到 Ubuntu server，在 tmux 中对话时屏幕闪烁。用户用 Qwen 3.8 Max 排查后确认是 Qwen Code 版本问题。[链接](https://github.com/QwenLM/qwen-code/issues/8562)

9. **Shell 忽略 tools.truncateToolOutputThreshold 配置**（#8922，4 评论）
   官方文档声明该配置对 Shell 生效，但 Shell 实际使用固定的 30,000 字符预算，配置不生效。[链接](https://github.com/QwenLM/qwen-code/issues/8922)

10. **Anthropic wire 缺失 OpenAI wire 已有的流安全保护**（#9005，3 评论，P1）
    Anthropic 内容生成器缺少 OpenAI 路径已有的流式安全保护，相关 SDK 还停留在 2025 年 1 月的 v0.36.1。[链接](https://github.com/QwenLM/qwen-code/issues/9005)

### 4. 重要 PR 进展（10 个）

1. **feat(auth): 新增 Kimi 与小米 MiMo 提供商**（#8368）
    为 /auth 增加 Kimi（Coding Plan / 中国 API / 国际 API）和 Xiaomi MiMo（按量付费 + 中国/新加坡端点）预设。[链接](https://github.com/QwenLM/qwen-code/pull/8368)

2. **feat(web-shell): 重新设计 Channel 策略与工作区管理**（#8848）
    为所有可管理适配器开放直接消息、群组访问、会话路由和工作区所有权控制，支持全部发件人与群组策略设置。[链接](https://github.com/QwenLM/qwen-code/pull/8848)

3. **fix(serve): 按字节限制 ACP HTTP 预附加缓冲区**（#9007）
    修复 ACP HTTP 预附加（pre-attach）阶段的内存失控风险，统一按字节数限制缓冲区大小。[链接](https://github.com/QwenLM/qwen-code/pull/9007)

4. **feat(serve): 截断前自适应增长 live-journal 上限**（#8905）
    当进行中的 turn 超出日志上限时，先尝试扩容（上限翻倍并等比例扩大条目数），避免直接丢弃最早的 replay 条目。[链接](https://github.com/QwenLM/qwen-code/pull/8905)

5. **feat(core): 为 workflow 调度写入每个 agent 的 transcript**（#8971）
    每个 workflow 中的 agent() 调度现在都会留下与 Agent 工具启动的子代理相同格式的 JSONL transcript，含调度 prompt。[链接](https://github.com/QwenLM/qwen-code/pull/8971)

6. **feat(daemon): 防护跨工作树 Git 变更**（#8687）
    内置宿主端防护，识别 -C / --work-tree / --git-dir 的 git 仓库重定位，阻止越出会话工作树的变更命令。[链接](https://github.com/QwenLM/qwen-code/pull/8687)

7. **feat(mcp): 新增 MCP 2026 core 与 WebShell Apps 宿主**（#8992）
    首个 MCP 2026 客户端切片 + daemon-backed WebShell 的 Apps 宿主，自动协商现代协议、保留 ui:// 工具元数据并校验 HTML 资源。[链接](https://github.com/QwenLM/qwen-code/pull/8992)

8. **feat(serve): 跨会话共享 Chrome bridge（多客户端 /cdp 隧道）**（#8740）
    让 daemon 的 /cdp 隧道支持多客户端，非 daemon 进程也能使用，多个会话共享一个 Chrome 扩展桥接，避免重复直连 Chrome。[链接](https://github.com/QwenLM/qwen-code/pull/8740)

9. **feat(core): 允许 workflow agent 固定目录并超出默认边界**（#8972）
    workflow 子代理可通过 agent({workingDir}) 固定到调用方已有的 git worktree，突破原有的短时和原地限制。[链接](https://github.com/QwenLM/qwen-code/pull/8972)

10. **feat(web-shell): 用结构化数据本地化后台任务通知**（#8989）
    后台 shell、监视器和后台代理完成时的通知不再硬编码英文，daemon 附带结构化数据，支持本地化渲染。[链接](https://github.com/QwenLM/qwen-code/pull/8989)

### 5. 功能需求趋势

从活跃 Issues 中可提炼出社区最关注的六个方向：

- **无人值守与长任务执行**（#8963、#9011）：用户明确要求"无脑接受模式"和可稳定跑通数天的长任务，这是 CLI 模式的核心竞争力。
- **会话管理/恢复可靠性**（#8678、#8979、#8923）：session 恢复超时、MAX_TOKENS 恢复后 transcript 不一致、/clear 后保留手动会话名等，均围绕"会话完整性"展开。
- **多代理协作与编排**（#8097、#8971、#8972）：后台子代理协调、per-agent transcript、worktree 固定目录等，说明多代理正从实验走向生产级可靠。
- **新模型与认证接入**（#8368、#8584、#9005、#9016）：Kimi/小米 MiMo 加入、Anthropic 模型 ID 兼容和流安全、Vertex AI ADC 认证，反映社区对多云多模型的无缝接入刚需。
- **工具输出与上下文预算**（#7306、#8922、#8447）：工具输出截断阈值、文本展示负载上限、日志自适应扩容，目标都是解决长会话中的上下文膨胀问题。
- **桌面

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*