# AI CLI 工具社区动态日报 2026-08-09

> 生成时间: 2026-08-08 22:35 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-08-09）

---

## 1. 生态全景

当前 AI CLI 工具已完成「能写代码」的基础能力建设，竞争重心正转向**多会话协调、记忆持久化与生态稳定性**——Claude Code 的消息队列诉求（184👍）与 Qwen Code 的跨会话通信提案在同一天成为社区焦点，表明「打断式交互」已成为全行业共识短板。稳定性问题（MCP 内核崩溃、runaway 生成、模型收费失控）开始动摇用户信任根基，各工具纷纷以成本透明化、权限白名单、信任机制等方式修复信任赤字。值得关注的是，工具间功能差距正在缩小——Claude Code、Qwen Code、Copilot、OpenCode 四大社区不约而同地卷入同一批议题（代理协调、浏览器控制、成本可见性），行业进入「长跑耐力赛」阶段。

---

## 2. 各工具活跃度对比

| 工具 | 热门 Issues 数 | PR 动态 | Release 情况 | 迭代节奏判断 |
|---|---|---|---|---|
| **Claude Code** | 10（另有 50 条全部 Issue 池） | 1 个活跃 PR，修复 hook 规则匹配 | v2.1.225 / v2.1.226 两个维护版 | 稳定高频发版，社区量大但 PR 流量低，属「社区重、官方响应慢」模式 |
| **OpenAI Codex** | 至少 4（信息截断） | 多个安全加固/协议 PR（工作负载身份令牌、gRPC host、异步钩子） | rust-v0.148.0-alpha.4 / alpha.5 连续双发 | 快速迭代期，alpha 版本密集，基础设施优先于社区诉求 |
| **Gemini CLI** | 无数据 | 无数据 | 无数据 | 数据缺失，建议警惕「信息真空」 |
| **GitHub Copilot CLI** | 10 | 0 个公开 PR（24 小时窗口） | v1.0.79-9 单补丁 | 成熟稳定期，发版频率低，但新 Issue 集中爆发（多为回归）、社区反馈速度快 |
| **Kimi Code CLI** | 2（重点筛选后） | 0 | 无 | 早期阶段，Issue 基数小，社区关注点高度聚焦（记忆系统 + 生成安全） |
| **OpenCode** | 10 | 8 个 PR（1 活跃 + 7 因长期无人维护被自动关闭） | 无正式发布 | 社区活跃但维护响应不足，自动清理 PR 是双刃剑 |
| **Qwen Code** | 10 | 10 个 PR（6 新提交 + 2 Open + 2 Closed） | v0.21.8 正式版 + nightly | 高活跃期，既有大量新功能提案又有 CI 自动化闭环，官方响应最积极 |

---

## 3. 共同关注的功能方向

### 3.1 多会话协调与消息队列
- **Claude Code**：用户要求消息队列模式（#50246，184👍）——排队而非打断当前任务，直击人机协作核心痛点。
- **Qwen Code**：提出跨会话消息传递（#8724）与原生多代理协调 RFC（#8718），设计 leader-worker 调度架构，且 #8730 已完成入站门禁实现。
- **OpenCode**：原生会话目标 `/goal` 命令（#27167，128👍）——持久化会话生命周期管理。
- **GitHub Copilot CLI**：ACP 请求支持会话中动态切换 contextTier（#4275），对齐交互式 `/model` 选择器。

**解读**：行业共识正在形成——AI CLI 需要从「单次任务的对话工具」演进为「可编排、可并发的多代理运行时」。

### 3.2 MCP/插件生态稳定性
- **Claude Code**：VS Code 完全不加载 MCP（#19054，已持续 7 个月）、MCP 无界扇出致 macOS 内核崩溃（#64366）。
- **GitHub Copilot CLI**：Enterprise 账号下 MCP OAuth 认证必然失败（#4408）。
- **OpenCode**：TUI 缺少 MCP 服务器管理界面（#38993）、MCP 重复进程致 TasksMax 耗尽（#31554）。
- **Qwen Code**：浏览器控制方案（#8699）探讨绕开 MCP 的替代路径。

**解读**：MCP 从「概念热点」进入「落地阵痛期」。协议成熟度、资源隔离、权限边界三大短板同时暴露，且 Windows/IDE 集成环境问题尤为突出。

### 3.3 成本透明与生成安全
- **Claude Code**：模型悄悄切换三天超额 $1,050（#60093）、未授权 Pro→Max 自动扣费（#82529）；v2.1.225 已新增网关消费限额提示作为回应。
- **Kimi Code CLI**：模型失控单步运行 53 分钟、输出 88K tokens 乱码（#2597），暴露缺少输出上限/中断机制。
- **OpenCode**：中文模型提供商成本追踪恒显 $0.00（#34877）。

**解读**：成本失控正从「轻微不满」升级为「信任危机」。生成护栏（token 上限、异常输出熔断）与费用可视化成为刚需。

### 3.4 平台一致性与会话状态
- **Windows 专属问题**：Claude Code 的 LSP 找不到二进制（#59114）、插件安装 EBUSY（#67595）；Copilot 的技能目录失效（#4401）；OpenCode 的 Ghostty 终端启动缓慢（#14965）。
- **桌面端与 CLI 功能割裂**：Claude Code 桌面端 Dispatch 被禁用（#80058）、内置 CLI ECONNRESET（#84818）。
- **会话状态丢失/串扰**：Copilot resume 后模型重置（#4397）；Claude Code `/clear` 后 session_id 变更导致钩子不重跑；OpenCode 多终端共享同一 SQLite 会话（#31307）。

---

## 4. 差异化定位分析

| 工具 | 核心定位 | 目标用户 | 技术路线特征 | 社区特质 |
|---|---|---|---|---|
| **Claude Code** | 全功能专业级 AI 编码助手 | 重度专业开发者、企业团队 | 多模型网关（Sonnet/Opus）、MCP 大型生态、VS Code/桌面全覆盖 | 全球最大社区（单 Issue 184👍），诉求范围广，对 Anthropic 的计费/稳定性容忍度低 |
| **OpenAI Codex** | 官方 Codex 模型的 Agentic CLI | OpenAI 平台开发者、Rust 技术栈社区 | Rust 实现、gRPC host 服务、工作负载身份令牌、异步钩子 | 迭代快但透明度低（alpha 占位发布），社区集中于子代理配额和本地执行环境问题 |
| **GitHub Copilot CLI** | 嵌入式 GitHub 生态的开发副驾 | Copilot 订阅用户、GitHub Codespaces 用户、企业客户 | 依托 GitHub 账号体系/AGENTS.md 标准、ACP 协议支持、内置 github-mcp-server | 问题数量大但单个热度低，企业场景（Enterprise OAuth、远程控制）与普通用户场景纠缠 |
| **Kimi Code CLI** | 中文友好、记忆优先的轻量 CLI | 中文开发者、Kimi API 用户 | 跨会话记忆系统为最大差异点（虽未实现）、WebBridge 式浏览器控制提案 | 社区尚小，但对「记忆」和「生成安全」有極高一致诉求，可能是下一个爆发点 |
| **OpenCode** | 开源可自托管的中立 CLI | 开源社区、多模型用户（Ollama/LM Studio/本地模型）、终端极客 | Go 实现、SQLite 事件溯源、插件 API、模型自动发现（#6231，205👍 全站最高） | 功能欲望最强（205👍 获赞最高），治理响应弱（PR 长期无人维护被自动关闭） |
| **Qwen Code** | 阿里云模型生态的原生 Agent | Qwen/百炼用户、VS Code 用户、追求 CI 自动化流水线的团队 | autofix/takeover 自动化 CI 闭环、多会话消息门禁、CUA 0.17 Computer Use、daemon/CDP 多端架构 | 官方响应最积极（10+ 新 PR）、自动化治理远胜同行，正在快速从「单工具」向「平台」演进 |

---

## 5. 社区热度与成熟度评估

### 高热度高成熟度：Claude Code
- 社区体量最大（50 条 Issue 池）、功能需求层次最深（从 TUI 交互到网关限额），但 PR 数量常年低位，官方以「周版本」方式回应社区，整体处于**用户高度活跃、管理相对滞后**的成熟期——社区贡献者的参与空间反而有限。

### 高活跃快速迭代：Qwen Code
- 24 小时内 3 个新版本（含 nightly）+ 10 个 PR + 10 个新 Issue，具备罕见的 CI 自动化修复闭环（autofix/takeover），软件工程实践在现代 AI CLI 中领先。正处于**从「工具」到「平台生态」的爬坡期**，值得作为观察「下一代 AI 开发工具标准」的标本。

### 高活跃但治理不足

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截至 2026-08-09）

> 说明：以下 PR 均按仓库给定的“评论数排序”列出，且当前状态均为 `Open`，尚无合并记录。

## 1. 热门 Skills 排行

### 1.1 [#1298 skill-creator：修复 run_eval.py 永远 0% recall](https://github.com/anthropics/skills/pull/1298)
- **功能**：修复 `run_eval.py` 以及依赖它的 `run_loop.py`、`improve_description.py` 全部误报 `recall=0%` 的问题；包含 Windows 流读取、触发检测、并行 worker 等修复。
- **社区热点**：对应 issue #556 的“0% 触发率”被 10+ 次独立复现；skill 描述优化实际是在对噪声做优化，社区关注度极高。
- **状态**：Open

### 1.2 [#514 新增 document-typography Skill](https://github.com/anthropics/skills/pull/514)
- **功能**：为 AI 生成文档增加排版质量控制，重点处理孤儿词、寡段、编号错位等问题。
- **社区热点**：AI 生成文档普遍存在排版缺陷，用户很少主动要求但显著影响交付质量。
- **状态**：Open

### 1.3 [#538 修复 pdf Skill 大小写敏感文件引用](https://github.com/anthropics/skills/pull/538)
- **功能**：修正 `skills/pdf/SKILL.md` 中 8 处大小写不匹配的文件引用（`REFERENCE.md` → `reference.md`、`FORMS.md` → `forms.md`）。
- **社区热点**：在大小写敏感文件系统（Linux/macOS）上 pdf Skill 引用失效，属于基础可用性问题。
- **状态**：Open

### 1.4 [#486 新增 ODT Skill](https://github.com/anthropics/skills/pull/486)
- **功能**：支持 OpenDocument 文本创建、模板填充、读取，以及 ODT 转 HTML。
- **社区热点**：社区对 LibreOffice / ISO 标准文档格式（ODT、ODS、ODF）的自动化处理需求明确。
- **状态**：Open

### 1.5 [#210 改进 frontend-design Skill 的清晰度与可执行性](https://github.com/anthropics/skills/pull/210)
- **功能**：重写 frontend-design skill，使每条指令在单次对话中可被 Claude 实际遵循，避免空泛指导。
- **社区热点**：Skill 指令“可执行性”成为核心讨论点——如何让描述具体到能约束模型行为。
- **状态**：Open

### 1.6 [#83 新增 skill-quality-analyzer 与 skill-security-analyzer](https://github.com/anthropics/skills/pull/83)
- **功能**：新增两个元技能：质量分析器从结构、文档、示例等五维评估 Skill；安全分析器做 Skill 安全审查。
- **社区热点**：社区对 Skill 质量评价体系和供应链安全非常关注。
- **状态**：Open

### 1.7 [#541 修复 docx Skill 中 tracked change w:id 冲突](https://github.com/anthropics/skills/pull/541)
- **功能**：修复 DOCX Skill 添加修订时，`w:id` 与现有书签冲突导致文档损坏的问题。
- **社区热点**：OOXML 中 `w:id` 是共享 ID 空间，简单硬编码 ID 会破坏真实复杂文档。
- **状态**：Open

### 1.8 [#539 skill-creator：对未加引号且含 YAML 特殊字符的 description 给出警告](https://github.com/anthropics/skills/pull/539)
- **功能**：在 `quick_validate.py` 中增加预处理校验，避免 `description` 包含 `:` 等字符时被 YAML 静默截断。
- **社区热点**：YAML 解析失败导致的 Skill 描述损坏是常见隐性故障。
- **状态**：Open

---

## 2. 社区需求趋势

从 Issues 热度和内容看，社区需求集中在以下方向：

- **安全与信任边界**：`#492`（43 条评论）指出社区 Skill 被放在 `anthropic/` namespace 下，冒充官方 Skill，构成信任边界滥用；`#1175` 关注 SharePoint 文档处理时的权限与上下文安全。  
  🔗 https://github.com/anthropics/skills/issues/492

- **组织级 Skill 共享**：`#228`（16 条评论，8 👍）呼吁在 Claude.ai 内直接支持组织级 Skill 库和分享链接，而不是手动下载、发送、上传。  
  🔗 https://github.com/anthropics/skills/issues/228

- **Skill 工具链可靠性**：`#556`（12 条评论，7 👍）和 `#

---

# Claude Code 社区动态日报 — 2026-08-09

## 今日速览

昨日发布 v2.1.225 与 v2.1.226 两个维护版本，重点新增网关消费限额提示与工作区信任机制。社区侧，消息队列模式诉求持续高热（#50246 获 184 👍），多起 MCP 服务器引发系统崩溃与成本失控的 Bug 报告值得关注，反映社区对稳定性与成本透明度的迫切需求。

## 版本发布

### v2.1.226
- **内容**：Bug 修复与可靠性改进。
- **链接**：https://github.com/anthropics/claude-code/releases/tag/v2.1.226

### v2.1.225
- **内容**：
  - Claude Code 使用警告新增网关消费限额支持，当达到限额时，提示信息会显示具体额度、重置时间以及操作者留言（需网关同步升级至 2.1.225）。
  - `claude agents` 新增工作区信任提示，针对不受信任的目录，与现有行为保持一致。
- **链接**：https://github.com/anthropics/claude-code/releases/tag/v2.1.225

## 社区热点 Issues（Top 10）

### 1. 消息队列模式：排队而非打断当前任务
- **Issue**：#50246 | 状态：OPEN
- **作者**：@mozltovcoktail | 创建：2026-04-18 | 更新：2026-08-08
- **热度**：评论 50 | 👍 184
- **摘要**：当 Claude 正在执行任务时，用户只能通过打断来插入新指令。提议新增消息队列模式，将后续需求排队，待当前任务完成后再处理——避免打断导致当前工作偏离轨道。
- **为什么重要**：184 个赞是本期最高，直击人机协作中最常见的中断痛点，可能影响核心交互设计。
- **链接**：https://github.com/anthropics/claude-code/issues/50246

### 2. VS Code 扩展完全不加载 MCP 服务器
- **Issue**：#19054 | 状态：OPEN
- **作者**：@Orbject | 创建：2026-01-18 | 更新：2026-08-08
- **热度**：评论 24 | 👍 26
- **摘要**：Claude Code for VS Code 扩展无法使用任何 MCP 服务器，已确认是最新版本，且并非个例。
- **为什么重要**：IDE 集成是高频使用场景，MCP 完全不可用严重影响插件生态落地，且该问题已持续近 7 个月未解决。
- **链接**：https://github.com/anthropics/claude-code/issues/19054

### 3. MCP 服务器无界扇出导致 macOS 内核崩溃
- **Issue**：#64366 | 状态：CLOSED
- **作者**：@ygbr | 创建：2026-06-01 | 更新：2026-08-08
- **热度**：评论 18 | 👍 0
- **摘要**：Cowork/agent 会话中 MCP 服务器无界扇出，耗尽 RAM 导致 M2 Max / 32GB 设备四次内核崩溃并强制关机。
- **为什么重要**：直接导致系统级崩溃而非应用崩溃，属于严重稳定性缺陷，影响多会话重度用户。
- **链接**：https://github.com/anthropics/claude-code/issues/64366

### 4. 模型未经同意切换到 Opus，三天超额 $1,050
- **Issue**：#60093 | 状态：CLOSED
- **作者**：@brian-christopher-brown | 创建：2026-05-18 | 更新：2026-08-08
- **热度**：评论 10 | 👍 0
- **摘要**：用户声称 5 月 5 日至 7 日三天内产生 $1,050 费用，后端模型在未告知、无 UI 提示的情况下从 Sonnet 切换到 Opus，且伴随 5 次进程失败与 7 个成本放大器。
- **为什么重要**：成本失控 + 无披露的模型切换，触及用户对费用透明度的核心信任，极具警示意义。
- **链接**：https://github.com/anthropics/claude-code/issues/60093

### 5. macOS 桌面应用 Dispatch 功能被禁用，移动端正常
- **Issue**：#80058 | 状态：OPEN
- **作者**：@sejune-oh | 创建：2026-07-22 | 更新：2026-08-08
- **热度**：评论 9 | 👍 1
- **摘要**：Dispatch 功能在 macOS 桌面应用中被禁用，但在移动端可用。
- **为什么重要**：跨平台功能不一致，桌面端是全功能主力端，受限会影响核心工作流。
- **链接**：https://github.com/anthropics/claude-code/issues/80058

### 6. 付费账单显示已支付，账户仍为 Free 计划
- **Issue**：#66558 | 状态：CLOSED
- **作者**：@roshanasingh4 | 创建：2026-06-09 | 更新：2026-08-08
- **热度**：评论 9 | 👍 1
- **摘要**：账单页面显示 Pro 订阅已付费，但账户权限仍停留在 Free 计划，用户请求标记为高优先级计费/权限问题。
- **为什么重要**：付费用户权益无法兑现，属于高影响计费事故，直接影响用户信任和留存。
- **链接**：https://github.com/anthropics/claude-code/issues/66558

### 7. Windows 下 LSP 工具找不到 typescript-language-server
- **Issue**：#59114 | 状态：CLOSED
- **作者**：@ytchenak | 创建：2026-05-14 | 更新：2026-08-08
- **热度**：评论 9 | 👍 3
- **摘要**：LSP 工具报 `ENOENT: uv_spawn 'typescript-language-server'`，即使二进制已全局安装并在 PATH 中。环境为 Windows 11 + Git Bash + nvm/scoop。
- **为什么重要**：Windows 环境 PATH 解析是老问题，影响大量 TS/JS 开发者的日常 LSP 体验。
- **链接**：https://github.com/anthropics/claude-code/issues/59114

### 8. Windows 下 `/plugin install` EBUSY 重命名错误
- **Issue**：#67595 | 状态：CLOSED
- **作者**：@chadj2 | 创建：2026-06-11 | 更新：2026-08-08
- **热度**：评论 6 | 👍 0
- **摘要**：Windows 11 Enterprise 上 `/plugin install` 因 Windows Defender 实时扫描竞争条件触发 `EBUSY rename` 错误，非管理员用户受影响。
- **为什么重要**：企业环境中 Defender 强制开启，插件安装不可用意味着核心扩展能力被阻断。
- **链接**：https://github.com/anthropics/claude-code/issues/67595

### 9. 桌面版内置 CLI 连接 ECONNRESET，npm CLI 正常
- **Issue**：#84818 | 状态：OPEN
- **作者**：@mazengehad | 创建：2026-08-07 | 更新：2026-08-08
- **热度**：评论 1 | 👍 0
- **摘要**：Claude 桌面应用更新至 1.25927.0.0 后，内置启动的 Claude Code 会话反复出现 `ECONNRESET` 错误，而同机 npm CLI 不受影响。
- **为什么重要**：非常新的回归（8 月 5 日更新后出现），桌面端用户是最广泛的使用群体，影响面大。
- **链接**：https://github.com/anthropics/claude-code/issues/84818

### 10. 未经授权的 Pro→Max 自动升级扣费
- **Issue**：#82529 | 状态：OPEN
- **作者**：@ekwkqk12 | 创建：2026-07-30 | 更新：2026-08-08
- **热度**：评论 2 | 👍 0
- **摘要**：用户 Pro 账户在 7 月 29 日被未经授权升级到 Max 计划，产生 ₩327,385 扣费（Invoice #W47FAZS1-0002），用户明确表示未发起此项变更。
- **为什么重要**：涉及未经授权的扣费行为，同时涉及韩国地区用户，可能引发支付合规与信任危机。
- **链接**：https://github.com/anthropics/claude-code/issues/82529

## 重要 PR 进展

### fix(hookify): 匹配 Write 和 prompt 规则
- **PR**：#77492 | 状态：OPEN
- **作者**：@ShiroKSH | 创建：2026-07-14 | 更新：2026-08-08
- **摘要**：
  - 使文件规则检查作为新文本传给 Write 的内容
  - 将简单 prompt 规则映射到当前 UserPromptSubmit 载荷，并保留旧版配置字段
  - 为 Write、Edit 和 prompt 规则增加回归测试覆盖
- **根因**：简单规则被推断为缺失字段，导致规则匹配失效。
- **为什么重要**：这是目前唯一的活跃 PR，修复 hook 规则匹配核心逻辑，直接影响所有使用自定义规则的用户，且长时间未合并值得关注。
- **链接**：https://github.com/anthropics/claude-code/pull/77492

## 功能需求趋势

从全部 50 条 Issue 中提炼出以下高频方向：

- **消息队列与异步交互**：#50246 以 184 👍 高居榜首，用户希望在任务执行中排队消息而非强制打断，说明人机协作的并发模型是核心痛点。
- **MCP 生态稳定性**：多起 MCP 相关 Issue（#64366 内存崩溃、#19054 VS Code 不加载、#70564 无按会话 MCP 白名单、#69953 自定义 MCP 被阻止），覆盖内存、集成、权限配置多个层面，MCP 的成熟度是当前最突出的短板。
- **成本可见性与控制**：#60093 模型悄悄切换导致 $1,050 超额、#82529 未授权升级扣费，用户对成本透明度和计费安全高度敏感。好消息是 v2.1.225 已新增网关消费限额提示，说明官方正在响应。
- **平台一致性**：Windows（LSP、插件安装、EBUSY）与 macOS 桌面版（Dispatch 禁用、ECONNRESET）均有专属问题，跨平台体验一致性亟待提升。
- **会话与状态管理**：Session Bridge 特性请求、`/clear` 后 session_id 变更导致 SessionStart 钩子不重跑等问题，反映用户对长会话状态管理的关注。

## 开发者关注点

- **成本失控是最大信任危机**：三天 $1,050 超额、未经授权的自动升级扣款，表明用户对模型切换的透明度和计费安全高度敏感。建议关注官方后续是否推出更严格的花费上限保护。
- **MCP 服务器稳定性严重影响重度用户**：内存耗尽导致内核崩溃，而非简单的应用报错，说明 MCP 服务器的资源管理存在缺陷，多会话场景下风险成倍放大。
- **Windows 平台问题集中爆发**：LSP 工具找不到二进制、插件安装被 Defender 阻塞——Windows 开发者体验明显滞后于 macOS，建议官方增加 Windows CI 覆盖。
- **桌面应用与 CLI 功能割裂**：Dispatch 在桌面端禁用、桌面内置 CLI 连接失败但 npm CLI 正常，用户希望桌面端与 CLI 保持同等能力与稳定性。
- **TUI 交互细节仍需打磨**：鼠标报告干扰复制粘贴、Ctrl+V 中途失灵、全屏渲染器无法滚动、XML 标签被剥离等小问题高频出现，虽不致命但持续消耗开发者耐心。
- **`/clear` 后钩子行为不一致**：session_id 变更但 SessionStart 不重跑，导致基于会话状态的钩子逻辑失效，属于中等优先级但影响自动化工作流的正确性。

---
*本日报由 AI 技术分析师自动生成，数据截至 2026-08-09。部分 Issue 已关闭但仍在更新窗口内，已如实标注状态。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-08-09）

## 今日速览

昨日 Codex 连续发布了两个 Rust 版本（0.148.0-alpha.4 / alpha.5），核心迭代方向偏向内部基础设施与稳定性。社区讨论集中在三大焦点：**Windows Computer Use 批量故障**（窗口枚举失败、node_repl 上下文被复用）、**子代理生命周期与配额管理**（重新水合状态异常、整周配额一夜耗尽），以及 **MCP/钩子系统在复杂环境下的可靠性问题**。PR 侧则出现了一批安全加固与协议定义工作，包括工作负载身份令牌交换、gRPC code-mode host 服务及异步命令钩子支持。

---

## 版本发布

### rust-v0.148.0-alpha.5
- **发布内容：** Release 0.148.0-alpha.5（仅发布占位说明，详情待补）

### rust-v0.148.0-alpha.4
- **发布内容：** Release 0.148.0-alpha.4（仅发布占位说明，详情待补）

> 这是两版连续发布的内部 alpha 迭代，紧随 0.147.0 系列之后，预计包含钩子系统、身份认证和 gRPC 服务等方面的后续改动（见下方 PR 列表）。

---

## 社区热点 Issues（精选 10 条）

### 1. #23005 — Windows 上文件编辑成功后仍显示 "Oops, an error has occurred"
- **状态：** 已关闭 | 评论：25 | 👍：10
- **链接：** https://github.com/openai/codex/issues/23005
- **核心问题：** 更新后，即使用户的文件编辑任务已完成，应用仍弹出错误提示，严重影响 Windows 端核心工作流体验。25 条评论显示讨论量高，值得关注其修复方案是否彻底。

### 2. #32177 — 附加纯文本日志可触发 "Request blocked" 并"毒化"后续对话
- **状态：** 打开 | 评论：15 | 👍：17
- **链接：** https://github.com/openai/codex/issues/32177
- **核心问题：** 在 Codex App 中向既有会话附加文本日志，会触发安全审查并将整个会话带入拒绝服务状态，后续所有轮次均被阻塞。17 个 👍 表明这是不少用户遇到的真实障碍，涉及会话污染与安全过滤机制的组合缺陷。

### 3. #19694 — Desktop 模型选择器过滤掉了 model_catalog_json 返回的模型
- **状态：** 已关闭 | 评论：15 | 👍：35
- **链接：** https://github.com/openai/codex/issues/19694
- **核心问题：** 通过 model_catalog_json 配置的自定义模型虽然出现在目录中，但被桌面端模型选择器过滤掉，导致自定义模型路由失效。35 个 👍 在列表中最高的，说明大量使用自定义模型配置的用户受影响。

### 4. #34306 — CLI 误判网络安全请求："此内容无法显示"
- **状态：** 打开 | 评论：11 | 👍：7
- **链接：** https://github.com/openai/codex/issues/34306
- **核心问题：** codex-cli 0.144.6 对正常开发请求（疑似涉及安全相关关键字）执行了额外的网络安全审查并拒绝显示内容，且未提供有效绕过方式。这是安全过滤器误报，开发者遭遇此类"

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-08-09

## 今日速览
昨日发布补丁版本 v1.0.79-9，优化了 `/sandbox` 配置对话框的存储位置提示。Issue 方面，社区集中反馈了若干新引入的回归问题：`skill` 工具无法加载 `~/.agents/skills` 下的技能、`/agent` 将 `AGENTS.md` 误判为自定义代理，以及 `permissions.config` 中 `allowed_directories` 完全不生效。此外，关于 npm 安装路径“版本漂移”的讨论值得关注。

## 版本发布
**v1.0.79-9**（2026-08-08）
- **Improved**: `/sandbox` 配置对话框现在会显示沙箱设置在 `settings.json` 中的存储位置，方便用户直接定位和修改。

https://github.com/github/copilot-cli/releases

## 社区热点 Issues
以下为过去 24 小时内更新、最值得关注的 10 个 Issue：

**#4410 [Bug] `/agent` 弹窗将 `.github\agents\AGENTS.md` 误当作自定义 agent**
- 作者指出仓库指引文件 `AGENTS.md` 被 `/agent` 弹窗错误地当作自定义 agent 定义解析，并报出 frontmatter 格式错误，与官方文档描述不符。属于会误导用户的识别逻辑问题。
- 评论 1 条，尚在 triage。
- https://github.com/github/copilot-cli/issues/4410

**#4409 [Bug] `cli_remote_control_enabled: false` 时无任何界面提示，GitHub Mobile 仅返回裸 HTTP 422**
- 当账号 Copilot 权限关闭远程控制时，桌面端可正常修改设置，但 GitHub Mobile 端调用直接失败且无错误说明。暴露了该功能的错误处理与用户引导缺失。
- 0 评论，新提交。
- https://github.com/github/copilot-cli/issues/4409

**#4408 [Bug] github-mcp-server 在 Copilot Enterprise 账号上 OAuth 认证永远失败**
- Enterprise 路由账号下，内置 MCP 服务器的 OAuth 流程无法发现授权服务器元数据，导致 `/mcp` 认证必然失败。
- 0 评论，新提交。
- https://github.com/github/copilot-cli/issues/4408

**#4401 [Regression] `skill` 工具无法找到 `~/.agents/skills` 下的有效技能**
- 用户报告该问题疑似 #2230（已关闭）的不完整修复或回归。技能目录和 `SKILL.md` 均存在，但 `skill` 工具无法发现/调用——影响所有依赖本地技能的自定义 agent 工作流。
- 0 评论，新提交。
- https://github.com/github/copilot-cli/issues/4401

**#4402 [Bug] npm bin/copilot 是加载器而非版本固定：同一路径 101 秒内先后运行 1.0.77 与 1.0.78**
- 全局安装的 `copilot` 命令会在两次调用间自动切换版本，且 `--prefer-version` 虽然可用但官方未记录。对需要可复现构建的 CI/生产环境影响较大。
- 0 评论，新提交。
- https://github.com/github/copilot-cli/issues/4402

**#4405 [Bug] Codespaces 中 Copilot Free 报 “No model available”**
- 免费版账号在 Codespaces 中启动成功，但所有 prompt 立即报 `No model available`，可能与 token 隔离或策略同步延迟有关。影响大量免费用户。
- 0 评论，新提交。
- https://github.com/github/copilot-cli/issues/4405

**#4397 [Bug] `resume` 恢复会话时自动切回默认模型**
- 使用 `--model=gpt-5.6-terr..."` 启动的会话，`resume` 后模型选择被重置为默认值，用户必须手动重新指定。破坏多模型工作流。
- 0 评论，新提交。
- https://github.com/github/copilot-cli/issues/4397

**#4398 [Bug] `permissions.config` 中的 `allowed_directories` 从未加载**
- 用户配置了多个工作区的允许目录，但 `/list-dirs` 完全不显示。目录白名单控制形同虚设，存在安全隐患。
- 0 评论，新提交。
- https://github.com/github/copilot-cli/issues/4398

**#4394 [Feature] 允许禁用/重映射 “Ctrl+C 两次退出” 行为**
- 用户习惯在终端中把 Ctrl+C 用于“取消操作”或“复制文本”，但 Copilot CLI 双击即退出，请求提供配置项。
- 0 评论，新提交。
- https://github.com/github/copilot-cli/issues/4394

**#4275 [Feature] ACP 支持 `contextTier` 作为会话配置项（对齐交互式 `/model` 选择器）**
- 交互式 CLI 支持会话中切换上下文窗口层级，但 ACP（Agent Client Protocol）服务器只能在启动时设定，无法在会话中动态调整。ACP 客户端缺少完整功能对齐。
- 评论 1 条，开放中。
- https://github.com/github/copilot-cli/issues/4275

## 重要 PR 进展
过去 24 小时无公开 PR 更新（新增或合并均为 0）。

## 功能需求趋势
从近期 Issues 中可以提炼出社区最关注的四个功能方向：

1. **配置灵活性与可定制性**：用户希望获得更多可配置项——包括禁用快捷键（#4394）、会话中动态切换上下文层级（#4275）、恢复 sessions 快捷删除（#4395）、以及禁止 banner 重复出现（#4129，已关闭）。
2. **Windows 平台支持完善**：多条 Windows 专属问题（#4219、#4399、#4401）显示 Windows 上的渲染、PowerShell 钩子兼容性和本地技能发现是持续痛点。
3. **本地化支持**：#4407 请求为桌面端与 CLI 添加中文（zh-CN）UI，反映非英语用户群体日益扩大。
4. **会话与模型状态一致性**：多条 issue（#4397 等）指向会话恢复时模型选择丢失、模型策略在 Codespaces 等环境中不可用的问题，用户对“所见即所得”的会话可靠性要求提高。

## 开发者关注点
- **回归问题成高频投诉**：`skill` 工具失效（#4401）、主面板冻结回归（#4222）、`AGENTS.md` 误识别（#4410）等，均指向近期版本引入的已有功能回退——社区对回归修复速度较为敏感。
- **配置项“白名单失效”隐患**：`allowed_directories` 不生效（#4398）与远程控制开关无提示（#4409），均涉及安全/权限边界，用户希望配置能真实生效并给出明确的状态反馈。
- **安装与版本管理困惑**：npm shim 的 loader 行为导致版本在两次调用之间漂移（#4402），暴露出官方安装机制缺乏版本锁定/回滚能力，影响 CI 场景的可复现性。
- **认证与 MCP 集成受阻**：Enterprise 下 MCP OAuth 失败（#4408）、Codespaces 中 Free 账号无模型可用（#4405），这类账号/环境相关的问题量大且影响面广，用户期待更清晰的错误信息和降级策略。

---
*数据统计窗口：2026-08-08（基于 2026-08-09 生成的日报）*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-08-09**

---

## 一、今日速览

- 跨会话记忆系统（Memory System）的功能讨论持续加热，Issue #1283 累计评论达 25 条，成为社区长期关注的核心需求。
- 新增严重稳定性 Bug：模型在一次交互中失控，单步运行 53 分钟、输出约 88K tokens 乱码，引发对生成护栏机制的担忧。

---

## 二、版本发布

过去 24 小时无新版本发布或预发布公告。

---

## 三、社区热点 Issues

### 1. [#1283 Feature Request: Memory System - Persistent context across sessions](https://github.com/MoonshotAI/kimi-cli/issues/1283)
- **作者**: @CatKang | **创建**: 2026-02-27 | **更新**: 2026-08-08 | **评论**: 25
- **核心内容**: 请求实现一套完整的 Memory System，让 Kimi Code CLI 能跨会话记住上下文、项目模式与用户偏好，包括 AI 自动管理的笔记（自动记忆）和用户自定义指令（手动记忆）。
- **为何重要**: 记忆能力直接决定编码助手能否从「单次会话工具」进化为「长期协作伙伴」，是当前 AI 编程工具竞争的关键分水岭。该 Issue 自 2 月提出以来持续有开发者跟进讨论，近期更新热度回升。
- **社区反应**: 25 条评论反映出该需求具有广泛代表性，但至今未被官方采纳，评论中可能包含对实现方案（向量存储、上下文压缩策略等）的具体探讨。

### 2. [#2597 Bug: Runaway garbled generation — 88k tokens of gibberish in one LLM step](https://github.com/MoonshotAI/kimi-cli/issues/2597)
- **作者**: @kdp123 | **创建**: 2026-08-08 | **更新**: 2026-08-08 | **评论**: 0
- **核心内容**: 正常交互会话中，模型发生失控生成：单个 LLM 步骤运行了约 3214 秒（~53分钟），输出 88,114 个 token，内容为多语言乱码、断裂的 Markdown 和无限重复文本。
- **为何重要**: 此类 Runaway Generation 属于严重的生产事故级 Bug，不仅直接阻塞用户工作流，还可能产生巨额 token 成本。该问题暴露了 CLI 在生成层缺少次数限制、异常输出检测和手动终止机制等基础护栏。
- **社区反应**: 刚创建暂无评论，但其严重性预计将快速获得关注。开发者普遍担忧此类问题是否与特定模型参数、上下文窗口溢出或解码策略缺陷有关。

---

## 四、重要 PR 进展

过去 24 小时无合并或更新的 PR。

---

## 五、功能需求趋势

从近期 Issue 与评论内容中提炼出以下社区核心关注方向：

1. **持久化上下文管理（Memory System）**
   - 典型诉求：跨会话保存项目约定、用户偏好、历史决策记录。
   - 社区期望：兼具自动记忆（AI 提炼）与手动记忆（显式指令）两种模式，且存储方式可检索、可控制。
   - 相关 Issue: [#1283](https://github.com/MoonshotAI/kimi-cli/issues/1283)

2. **生成稳定性与安全护栏**
   - 由 #2597 引发的关注：需要限制单次最大生成 token 数、最长执行时长，并支持实时中断。
   - 期待 CLI 在检测到重复/乱码输出时能自动熔断或告警，避免资源和计算成本浪费。
   - 相关 Issue: [#2597](https://github.com/MoonshotAI/kimi-cli/issues/2597)

---

## 六、开发者关注点

1. **上下文丢失的痛点**
   - 开发者在多轮会话或切换项目后，常常需要重新重复说明代码风格、测试命令、技术栈等背景信息。这种重复性劳动破坏了 AI 辅助编码的「连续性」体验，是 Memory System 诉求的根源。

2. **对 runaway 生成的零容忍**
   - 一次 53 分钟的失控生成，意味着用户在此期间无法正常工作。开发者普遍反馈，对于长时间执行的任务：
     - 需要明确的进度指示；
     - 需要可靠的中断/取消机制；
     - 需要输出长度和耗时的硬上限保护。
   - 此类问题若频发，会严重削弱开发者对 CLI 自动化能力的信任度。

---

> 总结：今日社区焦点依旧集中在「强化长期记忆」和「增强输出安全」两个方向。内存系统需求讨论虽长但尚未落地，而失控生成 Bug 再次提醒团队，在下沉新功能前需优先巩固基础稳定性护栏。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-09

## 今日速览
过去 24 小时无新版本发布，社区讨论集中在两大方向：一是 **OpenCode Go 网关 deepseek-v4-flash 模型名前导空格问题**（#41300、#41306、#41314、#41322 四个重复 issue 集中爆发），二是 **会话持久化与数据膨胀**（#27167 会话目标功能获 128 赞、#33356 数据库达 13GB）。此外，多个 PR 因长期无人维护被自动标记关闭，仅 #41335 一个修复 PR 处于活跃状态。

---

## 社区热点 Issues
以下为评论数/影响力最高的 10 个 Issue：

### 1. [FEATURE] 添加原生会话目标 /goal 命令 — #27167
- **标签**: OPEN | 评论 69 | 👍 128
- **作者**: @jorgitin02
- 社区最热功能请求：希望超越自定义 slash 命令，提供原生持久化会话目标/生命周期管理。128 个 👍 表明这是一个广泛需求。
- **链接**: https://github.com/anomalyco/opencode/issues/27167

### 2. 从 OpenAI 兼容提供商端点自动发现模型 — #6231
- **标签**: OPEN | 评论 45 | 👍 205
- **作者**: @ochsec
- 全站获赞最多的 issue（205 👍）。用户需要手动在 `opencode.json` 列出 LM Studio、Ollama、llama.cpp 等本地提供商的模型，这种体验被广泛诟病。
- **链接**: https://github.com/anomalyco/opencode/issues/6231

### 3. [2.0] event 表无限增长，opencode.db 达 13GB+ — #33356
- **标签**: OPEN | 评论 15
- **作者**: @rustyaos
- 事件溯源表从不清理压缩，长期运行实例 DB 已达 13GB，把 22GB 卷撑到 97-99%。这是 2.0 版本的严重数据管理缺陷。
- **链接**: https://github.com/anomalyco/opencode/issues/33356

### 4. [Bug] deepseek-v4-flash 模型名被注入前导空格导致 HTTP 400 — #41306
- **标签**: OPEN | 评论 3
- **作者**: @gugujiao953-ship-it
- 在今天新提交的验证中确认：即使 #41211 声称修复，网关仍返回 400。是当前最活跃的网关 bug（另有 #41300、#41314、#41322 四个相似报告）。
- **链接**: https://github.com/anomalyco/opencode/issues/41306

### 5. 启动缓慢：只在 Ghostty 终端出现 — #14965
- **标签**: OPEN | 评论 19 | 👍 13
- **作者**: @nickkadutskyi
- 从 v1.2.1 起 opencode 在 Ghostty 中启动极慢，但在 Terminal/Alacritty/Kitty 中正常。典型的终端兼容性回归问题。
- **链接**: https://github.com/anomalyco/opencode/issues/14965

### 6. [Bug] 会话因瞬时网络错误失败而非重试 — #30611
- **标签**: OPEN | 评论 6
- **作者**: @literally-dan
- 重试路径只把 `ECONNRESET` 视为可重试，其他瞬时传输错误直接判死。弱网环境下助手会话频繁中断。
- **链接**: https://github.com/anomalyco/opencode/issues/30611

### 7. [Feature] TUI 中增删 MCP 服务器并持久化配置 — #38993
- **标签**: OPEN | 评论 5
- **作者**: @abhirampuranik
- #37712 暴露了 HTTP 运行时 MCP 控制，但 TUI 界面仍缺失管理入口。配置持久化是核心诉求。
- **链接**: https://github.com/anomalyco/opencode/issues/38993

### 8. 同一项目多实例共享同一会话（SQLite 竞争） — #31307
- **标签**: OPEN | 评论 4 | 👍 3
- **作者**: @woei66
- 同一项目目录开两个终端，两个实例显示相同会话内容。交互会相互覆盖，无法并行工作。
- **链接**: https://github.com/anomalyco/opencode/issues/31307

### 9. MCP 服务器启动时产生 2-4 个重复进程导致 TasksMax 耗尽 — #31554
- **标签**: OPEN | 评论 2
- **作者**: @cgartlab
- Linux 上 10 个 MCP 服务器产生 36 个进程，重启不清理，最终触发 `EAGAIN` 错误。影响多 MCP 生产环境。
- **链接**: https://github.com/anomalyco/opencode/issues/31554

### 10. 中文模型提供商成本追踪显示 $0.00 — #34877
- **标签**: OPEN | 评论 2
- **作者**: @hyqf98
- GLM、DeepSeek、Qwen、MiMo 等通过 `@ai-sdk/openai-compatible` 配置后，TUI 始终显示 $0.00，即使已配置 `cost` 字段。
- **链接**: https://github.com/anomalyco/opencode/issues/34877

---

## 重要 PR 进展

### 1. fix(core): 转义字面量通配符并锚定补丁插入 — #41335
- **状态**: OPEN（唯一活跃 PR） | 创建: 08-08
- **作者**: @chirag-gamer
- 修复 #41333：通配符匹配器 `wildcard.ts` 与补丁插入逻辑两处 bug。当前唯一在途修复。
- **链接**: https://github.com/anomalyco/opencode/pull/41335

### 2. feat(observability): 添加 v2 GenAI 追踪 — #35935
- **状态**: CLOSED（automated-pr-cleanup）
- **作者**: @StarpTech
- 通过 OTLP 实现端到端 V2 GenAI 可观测性：每 agent 回合一条 trace，覆盖模型步骤、HTTP/WebSocket 传输、本地/托管工具、重试、压缩、子代理与生命周期失败。
- **链接**: https://github.com/anomalyco/opencode/pull/35935

### 3. feat: 添加基于 browser-use 的浏览器工具 — #35844
- **状态**: CLOSED（automated-pr-cleanup）
- **作者**: @laithrw
- 为 agent 增加内置 `browser` 工具，支持打开页面、点击、执行 JS、提取内容。此前只能通过 Playwright 等 MCP 间接实现。
- **链接**: https://github.com/anomalyco/opencode/pull/35844

### 4. feat(opencode): 添加内置 Pkl LSP 支持 — #35927
- **状态**: CLOSED（automated-pr-cleanup）
- **作者**: @caniko
- 使 OpenCode 原生识别 `.pkl` 文件，并在命令可用时自动启动 `pkl-lsp --stdio`。
- **链接**: https://github.com/anomalyco/opencode/pull/35927

### 5. feat(plugin): 为 v2 插件 API 添加 Tool 域 — #35869
- **状态**: CLOSED（automated-pr-cleanup）
- **作者**: @adm-humanerd
- 新增 `PluginContext.tool.transform()`，使 v2 Effect/Promise 插件可以命令式注册/注销工具，补齐现有 transform 模式缺口。
- **链接**: https://github.com/anomalyco/opencode/pull/35869

### 6. fix: 阻止 headless 运行启动死锁（effect fiber 重入） — #35871
- **状态**: CLOSED（automated-pr-cleanup）
- **作者**: @Xre0uS
- `opencode run` 在负载下约 40% 冷启动会挂起，修复 effect fiber 重入导致的死锁。
- **链接**: https://github.com/anomalyco/opencode/pull/35871

### 7. fix(app): 阻止切换标签时覆盖会话模型 — #35898
- **状态**: CLOSED（automated-pr-cleanup）
- **作者**: @lbklb
- Kobalte Select 在外部控制值变化时误触发 onChange，导致用户选择的模型被默认模型覆盖。修复后切换会话标签不再丢失模型选择。
- **链接**: https://github.com/anomalyco/opencode/pull/35898

### 8. feat(desktop): 通过外部 scheme 深链连接服务器 — #35968
- **状态**: CLOSED（automated-pr-clean

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报

**日期：2026-08-09** | 数据来源：github.com/QwenLM/qwen-code


## 1. 今日速览

v0.21.8 正式发布，恢复了 fork PR 的实时自动修复能力，并为 OpenAI、Gemini、Vertex AI 启用压缩缓存共享。社区讨论焦点集中在多会话协调机制（#8724、#8718）与浏览器控制方案（#8699、#8713）两大新方向，同时大量 autofix/takeover PR 的推进表明 CI 自动化修复流水线正在加速收敛遗留问题。


## 2. 版本发布

### v0.21.8（最新正式版）
- **实时自动修复（autofix）恢复 fork PR 支持**：通过将 review 事件桥接到有凭据的 workflow，解决 fork 来源 PR 无法触发自动修复的问题（[#8676](https://github.com/QwenLM/qwen-code/pull/8676)）
- **压缩缓存共享**：为 OpenAI、Gemini、Vertex AI 后端启用压缩缓存，可降低多会话场景下的重复 token 开销

### v0.21.7-nightly.20260808.4ec0371e6
- 修复 CI 中 autofix takeover 准入被阻塞时未正确暴露的问题（[#8410](https://github.com/QwenLM/qwen-code/pull/8410)）
- 补充 `serve` 子会话并发的文档说明


## 3. 社区热点 Issues

挑选 10 个最受关注或最具讨论价值的 Issue：

### 🔥 跨会话消息传递与多代理协调（新方向，讨论度高）
- **[#8724](https://github.com/QwenLM/qwen-code/issues/8724) Cross-session messaging：同机 Qwen Code 会话互发消息**（评论 4）
  提出 `list_agents` 发现、`send_message` 发送、接收端显式 fail-closed 门禁的方案。评论中关注点集中在安全边界：如何防止未经授权的会话间通信。
- **[#8718](https://github.com/QwenLM/qwen-code/issues/8718) RFC：独立 Qwen 会话的原生协调机制**（评论 4）
  讨论 leader 调度 2-3 个 worker、观察关联状态、收集结构化结果的架构方案。是 #8724 的上位设计文档，被标注 `need-discussion`。

### 🐛 高频 Bug：环境与配置
- **[#8752](https://github.com/QwenLM/qwen-code/issues/8752) VS Code 设置 schema 拒绝已文档化的 prompt hooks**（评论 3）
  生成的 settings schema 无法通过校验，导致 VS Code 用户无法使用核心运行时就支持的 prompt hook 配置。
- **[#8697](https://github.com/QwenLM/qwen-code/issues/8697) `OTEL_METRICS_EXPORTER=otlp` 静默禁用指标导出**（评论 3）
  与其他 OTel 工具共用 collector 时，该环境变量导致 telemetry SDK 启动失败、所有原生 `qwen*` 指标消失，而 trace 正常——问题定位难度高。
- **[#8750](https://github.com/QwenLM/qwen-code/issues/8750) 裸 URL 超链接吞掉 CJK 全角标点**（评论 3）
  CLI 输出中 URL 后紧跟中文全角标点时，终端可点击区域与下划线错误扩展至标点之后，影响中文用户阅读与点击。

### 🛡️ 安全与信任边界
- **[#8627](https://github.com/QwenLM/qwen-code/issues/8627) 显式 `DO_NOT_TRUST` 被祖先 `TRUST_FOLDER` 覆盖**（评论 3）
  信任规则短路求值导致 distrust 永远无法生效，恶意工作区可借信任祖先注入 `qwen serve` bearer token。社区对修复方案讨论积极。

### 🔮 新能力提案
- **[#8699](https://github.com/QwenLM/qwen-code/issues/8699) 提案：Qwen WebBridge——类 Kimi WebBridge 的浏览器控制**（评论 3）
  基于 `qwen serve` + Chrome 扩展做直接浏览器命令桥，MCP 不作为必需路径。评论中讨论了与现有 chrome-devtools MCP 的定位差异。
- **[#8713](https://github.com/QwenLM/qwen-code/issues/8713) 提案：Qwen Computer Use——产品化 CUA 0.17**（评论 2）
  将内置 CUA Driver 0.17 升级为一等公民的 Computer Use 执行循环，目标是补平与 Kimi Computer Use 的差距。

### ⚡ 稳定性与体验
- **[#8678](https://github.com/QwenLM/qwen-code/issues/8678) 大会话恢复超时时应保留当前会话**（评论 2，P1）
  `serve` 恢复大体积会话超时后当前会话不可用。已有 PR #8691 实现超时契约与可观测性。
- **[#8758](https://github.com/QwenLM/qwen-code/issues/8758) 自动会话标题被 hook 上下文主导**（评论 3）
  `UserPromptSubmit` hook 返回的 `additionalContext` 超过 1000 字符时会混入用户消息，导致自动标题描述的是 hook 内容而非用户请求。


## 4. 重要 PR 进展

挑选 10 个功能或修复价值较高的 PR：

### 🛠️ CI/自动化修复流水线
- **[#8765](https://github.com/QwenLM/qwen-code/pull/8765) A/B 确定性门禁拒绝机制**（新）
  确定性拒绝时自动在 `origin/<branch>`（round 提交前基线）重跑失败检查——若基线同样失败则标记为 pre-existing，可节省 18 分钟重跑时间。
- **[#8761](https://github.com/QwenLM/qwen-code/pull/8761) 工作流 label 变更全部走 REST 接口**（新）
  用 `gh pr edit` 在部分场景下无法修改 label，全部替换为 `issues/labels` REST 端点，并添加仓库级 guard 测试防止回归。
- **[#8763](https://github.com/QwenLM/qwen-code/pull/8763) 扩展 loader 环境变量拒绝名单**（新）
  紧接 #8663 合并后的 review 发现了 14 个未处理问题，本 PR 闭环处理其中实质性部分，进一步收窄继承环境变量的泄漏面。

### 🐛 核心修复
- **[#8687](https://github.com/QwenLM/qwen-code/pull/8687) 守护跨工作树 Git 变更操作**（Open）
  识别 `run_shell_command` 中通过 `-C`/`--work-tree`/`--git-dir` 逃逸到会话工作区之外的 Git 仓库操作并拦截，封堵一个模型误操作路径。
- **[#8663](https://github.com/QwenLM/qwen-code/pull/8663) 清除 daemon 子进程中的 loader 环境变量**（CLOSED，autofix/takeover）
  修复 daemon 会话继承启动 shell 的 `NODE_OPTIONS`/`NODE_PATH`/`LD_*`/`BASH_ENV` 等问题，防止跨工作区环境污染。
- **[#8764](https://github.com/QwenLM/qwen-code/pull/8764) 用显式 reader 读取响应体**（新）
  将 `readBoundedBody` 从 `for await` 改为 `getReader()` 循环，规避 `ReadableStream` 在某些运行时缺少 async iterator 的问题，并补齐行为测试。

### ✨ 新功能
- **[#8732](https://github.com/QwenLM/qwen-code/pull/8732) ACP 会话采用 Goal v3 运行时**（Open）
  ACP/Web Shell 会话废弃旧版 Stop-hook 实现，改用 CLI 同款 Goal v3 状态机，支持 create/status/edit/pause/resume/replace/clear 全生命周期。
- **[#8664](https://github.com/QwenLM/qwen-code/pull/8664) 批量 Skill 开关 API**（Open）
  新增 daemon 端点，单次请求最多切换 100 个 Skill 的启用状态，支持按目标报告错误而不影响其他项。
- **[#8739](https://github.com/QwenLM/qwen-code/pull/8739) 双击拖拽词级 / 三击拖拽行级扩展选择**（Open）
  补全 VP 模式文本选择的缺失编辑行为，对齐常规编辑器习惯。

### 🌐 架构整合
- **[#8740](https://github.com/QwenLM/qwen-code/pull/8740) 多客户端共享 Chrome 桥**（Open）
  将 daemon `/cdp` 隧道升级为多客户端模式，所有会话共享一个 Chrome 连接，避免重复拨号。


## 5. 功能需求趋势

从近期 Issue 与 PR 中提炼出四个最受关注的方向：

| 方向 | 代表 Issue/PR | 社区热度 |
|---|---|---|
| **多会话协调与 Agent 间通信** | #8724、#8718、#8730 | 🔥 高。两天内出现设计 RFC + 实现 PR，形成完整提案链 |
| **浏览器控制与 Computer Use** | #8699、#8713、#8740 | 🔥 高。三条路径并行探索（WebBridge、CUA 0.17 产品化、Chrome 桥共享） |
| **Web Shell 统一 UI 战略** | #8092、#8732、#8614 | 持续升温。桌面端转向 Web Shell 复用 + 右侧面板全屏为最新一步 |
| **终端交互体验精细化** | #8750、#8738、#8741 | 稳定增长。CJK 标点、文本选择、阻塞提示等细节打磨 |

值得注意：#8724（消息传递）与 #8718（会话协调 RFC）是当前最热的设计讨论，且 #8730 已完成入站门禁实现，说明多代理编排正在从设想走向落地。


## 6. 开发者关注点

### 🔴 高频痛点：环境变量与工作区隔离
- daemon 子进程继承启动 shell 的 loader 环境变量（`NODE_OPTIONS`、`NODE_PATH`、`BASH_ENV`），导致跨工作区环境污染（[#8653](https://github.com/QwenLM/qwen-code/issues/8653)）
- #8663 合并后 review 又发现 14 个遗留问题，说明该方向根因复杂、修复仍在持续（[#8763](https://github.com/QwenLM/qwen-code/pull/8763)）

### 🟠 高关注：CI 稳定性和自动化修复链路
- 主分支 E2E 测试失败自动建 issue 的机制有效，

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*