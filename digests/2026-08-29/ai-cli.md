# AI CLI 工具社区动态日报 2026-08-29

> 生成时间: 2026-08-29 03:44 UTC | 覆盖工具: 7 个

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

# Claude Code Skills 社区热点报告（数据截至 2026-08-29）

## 1. 热门 Skills 排行（Top PR）

> 以下 PR 均处于 **Open** 状态，按社区关注度排序（基于评论活跃度及关联 Issue）。

- **#1298 — skill-creator：修复 run_eval.py 评估器全面失效问题**  
  [链接](https://github.com/anthropics/skills/pull/1298)  
  **功能**：修复 `skill-creator` 中评估脚本 `run_eval.py` 始终报告 0% recall 的核心缺陷，使描述优化循环不再基于噪音运行。  
  **社区热点**：关联 Issue #556（12 条评论），多用户独立复现，Windows 流读取、触发检测及并行 worker 问题均有讨论，是当前技能开发工具链最紧迫的修复。

- **#514 — 新增 document-typography：AI 生成文档的排版质检**  
  [链接](https://github.com/anthropics/skills/pull/514)  
  **功能**：解决 AI 生成文档中的孤字、孤行、段落标题滞留页尾、编号错位等排版问题。  
  **社区热点**：涉及几乎所有 AI 生成文档的通用痛点，用户对“Claude 生成的文档是否需要排版约束”有较高共鸣。

- **#1628 — 新增 Hivemind：零成本多智能体编排技能**  
  [链接](https://github.com/anthropics/skills/pull/1628)  
  **功能**：让 Claude Code 将机械性工作委托给免费模型驱动的 opencode 无头 worker，Claude 保持规划/审查/合并职责。  
  **社区热点**：围绕成本优化与上下文稀缺性展开，代表社区对“昂贵模型上下文是稀缺资源”这一理念的探索。

- **#1607 — 更新 claude-api：标记四个已退役模型 ID**  
  [链接](https://github.com/anthropics/skills/pull/1607)  
  **功能**：将 `claude-opus-4-1` 等四个已退役模型从“Legacy/Deprecated”列表更正为 retired。  
  **社区热点**：模型生命周期与技能文档同步问题，用户关注官方技能是否及时反映 API 变更。

- **#538 — 修复 pdf 技能：SKILL.md 中大小写敏感的文件引用**  
  [链接](https://github.com/anthropics/skills/pull/538)  
  **功能**：修复 `skills/pdf/SKILL.md` 中 8 处 `REFERENCE.md`/`FORMS.md` 大小写错误，避免大小写敏感系统（Linux）下资源不可用。  
  **社区热点**：跨平台兼容性，尤其影响 Linux/macOS 用户。

- **#486 — 新增 ODT 技能：OpenDocument 创建/填充/解析/转 HTML**  
  [链接](https://github.com/anthropics/skills/pull/486)  
  **功能**：覆盖 `.odt`/`.ods` 文件的创建、模板填充、读取及格式转换。  
  **社区热点**：开源/ISO 标准文档格式支持，与 LibreOffice 生态联动，办公场景需求明显。

- **#210 — 改进 frontend-design 技能的可执行性**  
  [链接](https://github.com/anthropics/skills/pull/210)  
  **功能**：重构前端设计技能的指令，使每条指引都可在单次对话中被 Claude 实际执行，并提高行为引导精度。  
  **社区热点**：用户对“技能指令是否真正可操作”的讨论，反映出对技能质量本身的关注。

- **#525 — 新增 Pyxel 技能：复古游戏开发**  
  [链接](https://github.com/anthropics/skills/pull/525)  
  **功能**：为 pyxel-mcp 添加技能，支持 Python 编写像素风/8-bit 游戏（write → run_and_capture → inspect → iterate）。  
  **社区热点**：游戏开发与 MCP 结合，社区对创意类技能兴趣较高。

## 2. 社区需求趋势（来自 Issues）

- **安全与信任边界**（#492，43 条评论）：社区最担忧社区技能被放在 `anthropic/` 命名空间下导致用户误认为官方技能，进而授予过高权限。这是当前最强烈的生态治理诉求。
- **技能共享与协作**（#228，16 条评论）：用户希望在企业组织内直接共享技能，而非通过下载/手动上传，指向正式的 Skill 分享库/链接机制。
- **技能开发工具可靠性**（#556，12 条评论；#202，8 条评论）：`skill-creator` 的评估脚本无法触发技能、描述优化无效，说明社区需要一个可量化、可信任的 Skill 质量验证工具链。
- **去重与插件管理**（#189，6 条评论）：`document-skills` 和 `example-skills` 插件内容重复，导致上下文窗口浪费，要求更清晰的包划分。
- **上下文窗口效率**（#1487，4 条评论）：内置 `claude-api` 技能单次注入约 15.6 万 tokens，暴露大型技能对上下文的冲击，社区开始关注“技能体积”与按需加载。
- **办公文档兼容性**（#12，4 条评论）：docx/ooxml 技能在处理 Word 文档时引入额外空白导致文件损坏，需要对 Office 文档格式做更严格的约束。

## 3. 高潜力待合并 Skills（活跃但未合并的 PR）

- **#1298 skill-creator 评估修复** — 直接解除 #556 阻塞，是当前影响面最广的 bugfix，大概率优先合并。
- **#514 document-typography** — 普适性强的文档质量检测技能，需求明确，实现独立。
- **#1628 Hivemind** — 概念新颖且带有完整实现，若维护者认可“省钱但可控”的多智能体方向，有较高合并概率。
- **#538 / #541 / #539（同作者系列修复）** — 针对 pdf、docx、skill-creator 的三个轻量精准修复（大小写、w:id 冲突、YAML 引号），技术风险低，容易被 maintainer 采纳。
- **#1602 多问题综合修复** — 覆盖 mcp-builder 序列化、评估指标、编码和脚本稳定性，与 #1390 问题对应，属于工具链可靠性补强。
- **#525 Pyxel** — 成熟的游戏开发技能，作者即 pyxel-mcp 维护者，生态完整度高。

## 4. Skills 生态洞察

**当前社区最集中的诉求是：将 Skill 从“个人脚本”升级为“受信、可靠、可共享的基础设施”——一边要求修复评估工具并获得质量反馈，一边呼吁解决安全命名空间、去重和共享机制。**

---

# Claude Code 社区动态日报（2026-08-29）

## 今日速览

今日核心动态有三：发布 v2.1.251，新增模型切换钩子事件以及前台子代理 tool calls 到 Remote Con 的实时流式同步；Issue 侧 Windows 桌面端稳定性问题集中爆发，包括窗口置顶、静默更新后无法启动、更新重启破坏运行会话；社区同时持续要求“当前模型可见”和“用量可视化”，并新增了 MCP 无重试、Windows exec 钩子参数丢失等可靠性反馈。

## 版本发布

### v2.1.251

- 新增 `PreModelSwitch` / `PostModelSwitch` 钩子事件，支持对模型切换进行 block、confirm 或 annotate。
- `SessionStart` 恢复钩子现在会收到会话陈旧度（staleness）以及预估重新缓存成本。
- 前台子代理的 tool calls 与结果现在可以实时流式同步到 Remote Con。

## 社区热点 Issues（10 条）

1. [#85891 Claude Desktop (Windows 11) 窗口始终置顶，且无设置可关闭](https://github.com/anthropics/claude-code/issues/85891)  
   41 评论、90 👍。Windows 端高频问题，虽被标记 invalid 但讨论仍非常活跃，并有同类 #88093 跟进。

2. [#53247 Windows 上 Claude Desktop 崩溃后遗留 Silo/Job Object，只能注销或重启恢复](https://github.com/anthropics/claude-code/issues/53247)  
   30 评论、19 👍。涉及 HRESULT 0x80070020 与 AppModel-Runtime 事件，Windows 平台严重稳定性缺陷。

3. [#61682 GitHub connector 显示 Connected 但 Cowork 中不暴露任何工具](https://github.com/anthropics/claude-code/issues/61682)  
   27 评论、24 👍。连接状态与实际工具可用性不一致，直接影响 Cowork 工作流。

4. [#13340 global/local settings.json 中的 allow 权限未被 Claude Code 遵守](https://github.com/anthropics/claude-code/issues/13340)  
   26 评论、51 👍。权限配置失效属于安全敏感问题，社区关注度很高。

5. [#89680 Windows 桌面端静默更新留下孤儿进程，新版本无法启动，报 0x80070020](https://github.com/anthropics/claude-code/issues/89680)  
   与 #53247 具有相似根因特征，说明 Windows 上的自动更新机制存在系统性问题。

6. [#90172 桌面端静默重启更新破坏运行中会话，提示 “Can’t reach your computer”](https://github.com/anthropics/claude-code/issues/90172)  
   报告详细列出 8 个相互关联的缺陷，直指“为更新悄悄重启”会杀死用户的远程/后台会话。

7. [#74349 VSCode 扩展无法在界面中看到当前活跃模型](https://github.com/anthropics/claude-code/issues/74349)  
   CLI 有 statusLine 和 `/status`，但 VSCode 扩展缺少等效能力，影响多模型切换体验。

8. [#80261 桌面应用主界面应显示用量限制 / 持续用量指示器](https://github.com/anthropics/claude-code/issues/80261)  
   13 👍。Pro/Max 用户对周配额消耗可见性诉求强，关联 #83092、#80732。

9. [#90494 MCP server 晚于 Claude Code 启动就永远不会被连接，且无重试；/mcp reconnect 报 “No token data found”](https://github.com/anthropics/claude-code/issues/90494)  
   最新提交。Claude Code 在进程启动时一次性解析 MCP server，失败缓存终身有效，属于 MCP 可靠性关键问题。

10. [#90495 Windows 上 exec 形式 hook 的 args 被丢弃，仍被路由到 bash.exe 导致 eval_stdin 崩溃](https://github.com/anthropics/claude-code/issues/90495)  
    最新提交。Windows 下 hooks 行为不一致，影响自定义自动化与安全钩子。

## 重要 PR 进展

过去 24 小时仅 1 条 PR 更新，暂无其他合并或新 PR 数据：

- [#87079 fix(security-guidance): make ** glob patterns match zero-depth paths](https://github.com/anthropics/claude-code/pull/87079)  
  修复 `**` 在安全规则匹配中无法匹配零深度路径的问题。原因：`_glob_match` 委托给 `fnmatch` 后，裸 `*` 已能跨 `/`，导致 `**/*.ts` 要求字面 `/`，从而静默漏掉顶层文件的 security-patterns.json 规则覆盖。对安全规则来说，这是“静默失效”的隐患。

## 功能需求趋势

- **当前模型可见性**：多个 Issue 要求 CLI、TUI、VSCode 扩展持续展示当前活跃模型（Sonnet/Opus/Haiku 等），参见 #74349、#75047。
- **用量可视化**：社区期望在主界面或状态栏显示订阅计划用量

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-08-29）

## 今日速览

昨日密集发布 6 个 `rust-v0.151.0-alpha` 系列版本，迭代节奏明显加快。Windows 桌面应用成为社区关注焦点：#40752 更新后无法启动持续发酵（85 评论，51 👍），另有多个 Windows 专属崩溃与浏览器控制问题被高频反馈。底层架构 PR 集中在模型目录来源、执行器钩子、终端查询响应等方向，官方正系统性加固 code-mode 与浏览器自动化的稳定性。

## 版本发布

过去 24 小时发布了 6 个 alpha 版本（具体变更内容暂未披露）：

- [rust-v0.151.0-alpha.12](https://github.com/openai/codex/releases/tag/rust-v0.151.0-alpha.12)
- [rust-v0.151.0-alpha.11](https://github.com/openai/codex/releases/tag/rust-v0.151.0-alpha.11)
- [rust-v0.151.0-alpha.10](https://github.com/openai/codex/releases/tag/rust-v0.151.0-alpha.10)
- [rust-v0.151.0-alpha.9](https://github.com/openai/codex/releases/tag/rust-v0.151.0-alpha.9)
- [rust-v0.151.0-alpha.8](https://github.com/openai/codex/releases/tag/rust-v0.151.0-alpha.8)
- [rust-v0.151.0-alpha.7.1](https://github.com/openai/codex/releases/tag/rust-v0.151.0-alpha.7.1)

密集的 alpha 发布节奏表明开发团队正在快速修复问题并推进新功能落地。

## 社区热点 Issues

以下 10 个 Issue 为过去 24 小时社区关注度最高、影响面最广的问题：

**1. [Windows] 桌面应用更新后无法启动（“Unable to locate Codex CLI” & spawn EINVAL）**
- 85 评论，51 👍，持续发酵中
- Windows 11 用户升级至 v26.820.60940 后应用完全不可用，报错指向 CLI 定位失败及 `.cmd` 包装器 spawn 错误
- https://github.com/openai/codex/issues/40752

**2. 请求增加“禁用‘Ran N commands’折叠”选项**
- 43 评论，65 👍，高赞功能需求
- 用户希望 TUI 中始终完整显示已执行命令，而非默认折叠为摘要行
- https://github.com/openai/codex/issues/39903

**3. [Windows] code-mode host 握手阶段退出导致 GPT-5.6 异常**
- 36 评论，影响 ChatGPT Pro 20x 用户
- 本地命令执行通道在初始化握手时异常退出（`code-mode host exited during handshake`），导致无法自动读取目录
- https://github.com/openai/codex/issues/41049

**4. GPT-5.6 串行化独立 Code Mode 调用；显式批处理可降低 27-45% 权重消耗**
- 29 评论，40 👍
- 用户实测发现模型频繁串行调用工具而非并行批处理，显著浪费配额；社区对成本优化高度敏感
- https://github.com/openai/codex/issues/35050

**5. [Windows] Computer Use 无法获取 Chrome URL（即使在新标签页）**
- 26 评论，影响浏览器自动化核心流程
- https://github.com/openai/codex/issues/25271

**6. [Windows][WSL] 集成终端在 PTY/WSL 启动前静默失败**
- 23 评论，底部和侧边面板均无法打开（该 issue 已被关闭）
- https://github.com/openai/codex/issues/37104

**7. [Windows] 宠物覆盖层点击区域与显示位置随时间不同步**
- 20 评论，桌面应用细节体验问题
- https://github.com/openai/codex/issues/34227

**8. 高级账户安全（Advanced Account Security）导致应用登录-退出无限循环**
- 12 评论，认证流程严重故障
- 用户在启用安全增强后 Codex 应用完全不可用
- https://github.com/openai/codex/issues/40611

**9. macOS：Chrome 标签可声明但所有真实页面操作被策略验证拒绝**
- 12 评论，macOS 浏览器自动化功能受阻
- https://github.com/openai/codex/issues/39280

**10. Computer Use 辅助进程在每次点击后 SIGTRAP 崩溃（get_app_state 成功之后）**
- 8 评论，Windows/macOS 均有报告
- `SkyComputerUseService` 在获取应用状态后首次 UI 操作即崩溃，是当前最严重的稳定性问题之一
- https://github.com/openai/codex/issues/41326

## 重要 PR 进展

以下 10 个 PR 反映了官方正在推进的底层架构改进与稳定性修复：

**1. 从模型目录获取异步用户消息描述**
- 为 `send_user_message_async` 改用活动模型的目录描述，支持中途切换模型，未配置时回退内置描述
- https://github.com/openai/codex/pull/41461

**2. 从模型目录获取主动式多智能体指令**
- Ultra 推理模式使用目录中的 proactive 消息，增强多智能体场景下的模式引导
- https://github.com/openai/codex/pull/41457

**3. 执行器插件钩子支持应用目标**
- 允许受信任的 Browser 插件的 `Stop`/`SubagentStop` 钩子按应用策略执行，并携带可信路由元数据
- https://github.com/openai/codex/pull/41456

**4. 连续执行主机失败后阻止目标**
- 同一目标累计 3 次执行失败自动标记为 blocked，成功则重置计数，避免无限重试
- https://github.com/openai/codex/pull/41454

**5. 上报 code-mode 主机请求耗时**
- 统一测量 execute/wait/terminate 请求的墙钟时间，为性能诊断提供更准确的数据
- https://github.com/openai/codex/pull/41452

**6. 澄清默认协作模式中的问题处理**
- 允许 `request_user_input` 用于可选的、能提升工作质量的问题；必需输入（审批等）仍走原有流程
- https://github.com/openai/codex/pull/41448

**7

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-08-29）

> 数据来源：[github.com/github/copilot-cli](https://github.com/github/copilot-cli)

## 1. 今日速览

今日发布 **v1.0.82-1**，主要修复了认证失败时只提示 `/login`、无法看到具体错误（如 `401 Bad credentials`）的问题。社区讨论热度集中在 **TUI/运行时稳定性**（FileWatch 死循环导致 13GB 日志）与 **MCP 生态兼容性**（Atlassian OAuth 回归、chroma-mcp 被 v1.0.81 破坏）。企业用户持续反馈 **GHEC data residency 下 `copilot -p` 的 401 端点路由问题**。

## 2. 版本发布

### v1.0.82-1
- **Fixed**：认证失败时显示具体的失败原因（例如 `401 Bad credentials`），而不是仅提示登录 `/login`。

---

## 3. 社区热点 Issues

以下为过去 24 小时更新中最值得关注的 10 个 Issue：

### 1. [Runaway FileWatch host-event loop freezes TUI and grows debug log to 13 GB (#4612

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报
**日期：2026-08-29** | 数据源：[github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

---

## 今日速览

今日社区动态聚焦于**安全与稳定性**：一项关于 MCP 工具调用可绕过内置文件保护的安全问题（#2625）已于昨日关闭；同时用户反馈了严重的配额计费异常（#2626），称缓存读取计费存在超 10 倍放大。PR 方面仅有一条依赖安全更新（#2622），无需发布新版本。

---

## 社区热点 Issues

> 注：当日无新 Release。过去 24 小时内更新的 Issues 共 7 条，以下全部列出。

### 1. 🔒 安全漏洞：MCP 工具调用绕过内置 secret-file 防护（已关闭）
- **#2625** | 作者：@zhaoxingxing06 | 更新：2026-08-28 | 评论：1 | 👍：0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2625
- **摘要**: 内置文件读取工具会拒绝敏感文件（`.env`、SSH 密钥等），但 MCP 工具调用不受此内容级守卫限制。在自动批准权限模式下，MCP 调用可直接跳过审批提示，攻击者可利用恶意 MCP 服务器读取任意文件。
- **重要性**: 这是当前最严重的安全风险，涉及 MCP 生态的信任边界。Issue 在创建当天即被关闭，说明维护者已介入处理，但社区仍期待详细的修复方案说明。

### 2. ⚠️ 配额消耗异常：cache_read 每次对话都被计费，cache_creation 恒为 0（开放中）
- **#2626** | 作者：@ahmadyaseen35-coder | 更新：2026-08-29 | 评论：0 | 👍：0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2626
- **摘要**: 付费年费用户在 2026-08-28 晚间仅轻度使用，5 小时配额窗口就消耗了约 40%。检查 CLI 日志后发现 `cache_read` 在每轮对话都被计费，而 `cache_creation` 始终为 0，疑似计费逻辑异常。
- **重要性**: 直接影响用户付费体验，涉及配额计算准确性。若问题属实，可能导致用户被超额扣费，是当前**最紧迫的计费问题**。该 Issue 刚创建，社区关注度待发酵。

### 3. 🐛 Plan mode 死循环：反复执行 Bash echo / ReadFile 而不写计划（开放中）
- **#2623** | 作者：@zheng001001001 | 更新：2026-08-28 | 评论：1 | 👍：0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2623
- **摘要**: 在 Plan mode 下，模型（k3）完成探索后不执行写计划或 ExitPlanMode，而是死循环重复调用 `Bash echo <任意字符>` 和 ReadFile。影响版本 0.38.0，Linux 平台 + uv 部署。
- **重要性**: 这是核心工作流（Plan mode）的稳定性问题，会严重打断开发效率。目前仅有 1 条评论，社区需要更多复现信息来帮助定位。

### 4. 🛡️ Notion Remote MCP 凭据仅保存在当前会话（已关闭）
- **#1211** | 作者：@ghost | 更新：2026-08-28 | 评论：3 | 👍：0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/1211
- **摘要**: v1.12.0 中，运行 `kimi mcp auth n`（Notion Remote MCP 认证）后，凭据不会跨会话持久化，每次启动都要重新认证。
- **重要性**: 影响 MCP 的实际使用体验。该 Issue 从 2 月报告至 8 月底才被关闭，说明 MCP 认证持久化是一个长期待解决的问题。

### 5. 🎯 功能请求：JetBrains AI Assistant 通过 ACP 调用 kimi 无法识别文件（已关闭）
- **#1272** | 作者：@yuweni99 | 更新：2026-08-28 | 评论：1 | 👍：0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/1272
- **摘要**: 在 JetBrains AI Assistant 中通过 ACP 调用 kimi，拖拽添加的文件无法被识别，用户需在提示词中写完整文件路径或文件名才能处理。
- **重要性**: IDE 集成是开发者使用 CLI 的重要入口，此问题直接影响 JetBrains 用户的工作流。从 2 月创建到 8 月底关闭，周期较长。

### 6. 📄 文档改进：openai_legacy 托管 /v1 示例补充（开放中）
- **#2624** | 作者：@cursor[bot] | 更新：2026-08-28 | 评论：0 | 👍：0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2624
- **摘要**: providers 文档页已覆盖 `openai_legacy` 的 Chat Completions 宿主。建议补充三个易错细节：`type` 必须为 `openai_legacy` 而非 `openai_responses`，以及正确的 wire 协议示例。
- **重要性**: 文档准确性能减少用户接入第三方宿主时的报错，属于开发者体验优化。

### 7. 🧩 功能请求：原生 git-ai 集成，支持 AI 代码溯源（已关闭）
- **#1279** | 作者：@deshes | 更新：2026-08-28 | 评论：0 | 👍：0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/1279
- **摘要**: 建议原生支持 [git-ai](https://git-ai.com) 标准，让开发者可以在 `git blame` 中直接看到哪些代码来自 Kimi、哪些是人工编辑。
- **重要性**: 代码溯源与合规审计是 AI 代码工具在团队协作中的关键需求。该请求从 2 月 27 日创建到 8 月 28 日关闭，可能已被列入路线图，但社区期待更多细节。

---

## 重要 PR 进展

> 过去 24 小时内更新的 PR 共 1 条，无多个 PR 可挑选。

### 🔧 依赖安全修复：升级 asyncssh 至 2.23.1（开放中）
- **#2622** | 作者：@katsugtgz | 更新时间：2026-08-28 | 评论：无 | 👍：0
- **链接**: https://github.com/MoonshotAI/kimi-cli/pull/2622
- **摘要**: 将 `pykaos` 工作区包中的 `asyncssh` 从 2.21.1 升级至 2.23.1，旨在修复两个安全通告（GHSA-2wxc-x7rj-hg8f 和 GHSA-qr67-gv47-xwwh）。PR 中附带了版本锁定证据（`pyproject.toml` 和 `uv.lock` 均指向旧版本）。
- **重要性**: 安全相关依赖升级，虽然核心 CLI 用户未必直接受 `pykaos` 影响，但表明维护者正在积极处理供应链安全问题。不过该 PR 目前无评论，评审进度待观察。

---

## 功能需求趋势

从过去 24 小时活跃的 Issues 中，可以提炼出以下社区关注方向：

1. **MCP 安全加固与体验优化**
   - 安全问题：MCP 工具调用绕过 secret-file 守卫（#2625）
   - 体验问题：MCP 凭据跨会话持久化（#1211）
   - **趋势解读**：MCP 生态正在快速普及，但权限边界和凭据管理尚未成熟，社区对安全机制和易用性的诉求最为强烈。

2. **IDE 集成深化**
   - JetBrains AI Assistant 通过 ACP 调用的文件识别问题（#1272）
   - **趋势解读**：CLI 工具正逐步嵌入 IDE 工作流，但文件上下文传递、路径识别等细节仍有缺口。

3. **配额与计费透明度**
   - 配额异常消耗：cache_read 计费放大（#2626）
   - **趋势解读**：随着用户规模扩大，计费精确性和配额消耗的可解释性成为信任基础，社区对异常计费的容忍度正在降低。

4. **代码溯源与合规**
   - 原生 git-ai 集成请求（#1279）
   - **趋势解读**：企业级用户开始关注 AI 生成代码的可追溯性，希望将 AI 协作深度嵌入版本控制生态。

5. **核心模式稳定性**
   - Plan mode 探索后死循环（#2623）
   - **趋势解读**：模型行为（如 k3）在特定模式下的会话管理稳定性问题，直接影响开发效率，是高优先级反馈方向。

---

## 开发者关注点

- **安全盲区**: MCP 工具调用不受内容级文件访问限制，在 auto-approve 模式下可读取敏感文件。这是一个架构层面的权限模型问题，开发者提醒：**在修复前谨慎使用自动批准模式，并审查 MCP 服务器的可信度**。
- **计费担忧**: 异常配额消耗让用户产生「计费不透明」的不安情绪。受影响用户在 Issue 中提供了 CLI 日志数据，建议**关注官方回应及修复进度**。
- **工作流卡顿**: Plan mode 死循环问题在 0.38.0 + k3 模型下复现，涉及 Linux 环境。社区需要更多用户提供复现信息来协助定位。
- **IDE 集成的小摩擦**: JetBrains 用户遇到的文件识别问题，虽然已关闭，但「拖拽传文件」这一交互需要额外写路径才能生效，反映出 ACP 适配层仍有提升空间。
- **依赖安全同步**: pykaos 包中的 asyncssh 旧版本存在已知安全漏洞，PR #2622 依赖社区推动合并。**建议有 Kaos 子包使用场景的开发者注意升级版本**。

---
*本日报基于 GitHub 公开数据自动生成，仅供参考。Issue/PR 状态以官方仓库为准。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

## OpenCode 社区动态日报 — 2026-08-29

### 📌 今日速览

今日发布 v1.18.24 / v1.18.25 两个补丁版本，重点修复 Azure 认证与 Bedrock 推理缓存问题。社区最热 Issue 为 GPT 模型响应延迟问题（119 评论），同时 PR 侧密集出现针对 AI 提供商兼容性和性能优化的贡献，整体社区活跃度较高。

---

### 📦 版本发布

**v1.18.25** — [查看 Release](https://github.com/anomalyco/opencode/releases/tag/v1.18.25)
- **Core 修复**：修复 Azure 认证，Azure CLI 登录不再需要依赖 Bun。

**v1.18.24** — [查看 Release](https://github.com/anomalyco/opencode/releases/tag/v1.18.24)
- **Core 修复**：Bedrock 推理响应不再被缓存为不可重放的空消息。
- **Core 改进**：
  - Azure 提供商可通过 Azure CLI 使用 Microsoft Entra ID 登录，无需 API Key。
  - V1 版本现已支持读取 V2 配置字段，兼容更新后的配置文件。

> 这两个版本主要围绕云厂商（Azure/Bedrock）的认证链路与数据缓存可靠性做下沉修复，建议 Azure 与 Bedrock 用户及时升级。

---

### 🔥 社区热点 Issues

过去 24 小时共更新 50 条 Issue，以下为最值得关注的 10 条：

1. **[#29079] GPT 模型响应延迟过高** — ⭐ 119 评论 / 52 👍（已关闭）
   GPT 模型有时几秒内响应，有时需要数分钟，即使是非常简单的命令（如更新 graphify）。这是目前社区讨论最激烈的 Issue。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/29079)

2. **[#42700] TUI 每次启动泄漏 ~21MB .so 文件至 /tmp** — 7 评论（打开）
   TUI 每次启动向临时目录释放约 21MB 的 .so 文件且从不清理，多次启动后 tmpfs 被填满，导致 TUI 无法启动并报 OpenTUI 库加载错误。涉及 opencode 0.0.0-next-17444。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/42700)

3. **[#22792] 本地 vLLM + Qwen3-Coder 触发无限压缩循环** — 6 评论 / 3 👍（已关闭）
   通过 `@ai-sdk/openai-compatible` 连接本地 vLLM 后端并用 Qwen3-Coder-30B 时，输入“你好”等简单内容也会触发病态的反复压缩摘要循环。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/22792)

4. **[#29397] Opencode Zen 全模型变慢、Esc 中断失效** — 6 评论 / 7 👍（已关闭）
   一段时间以来所有模型都需要数分钟甚至永不完成响应，期间按 Esc 两次也无法中断。影响面较大。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/29397)

5. **[#46059] AI 陷入纯文本推理循环，不执行工具** — 2 评论（打开）
   模型反复在聊天中输出“Let me grep...”等文本意图，而不是真正调用工具，形成死循环。这是 8 月 29 日新报告的 Issue，值得关注。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/46059)

6. **[#38570] 额度计算异常：消耗 47% 但实际仅用 $1.50** — 5 评论（打开）
   5 小时额度显示已消耗 47%，但实际消费仅 $1.50，百分比与消费金额严重不符。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/38570)

7. **[#34223] Web UI 文件树开关被误隐藏** — 5 评论（已关闭）
   通过 `opencode web` 打开网页版时，无法开启文件树。“Show file tree”开关被错误地放在 `desktop()` 条件之后。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/34223)

8. **[#5750] 工具调用 ID Bug** — 14 评论 / 3 👍（已关闭）
   上传 2 张图片加短消息后触发错误。历史较久（12 月创建）但评论仍持续。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/5750)

9. **[#17427] 功能请求：工作区删除脚本** — 5 评论（已关闭）
   用户希望在打开新工作区时能自动创建专用测试数据库，需要工作区生命周期删除脚本支持。
   [查看 Issue](https://github.com/anomalyco/opencode/issues/17427)

10. **[#15680] 功能请求：向插件暴露 worktree 生命周期事件** — 4 评论 / 3 👍（已关闭）
    当前插件完全感知不到 worktree 的创建/删除/重置操作，希望补充事件机制。
    [查看 Issue](https://github.com/anomalyco/opencode/issues/15680)

---

### 🔧 重要 PR 进展

过去 24 小时共有 50 条 PR 更新，以下为 10 个关键 PR：

1. **[#36068] 支持 Ollama 的 `reasoning` 字段（OpenAI 兼容端点）** — 已关闭
   Ollama 的 `/v1/chat/completions` 使用 `reasoning` 字段输出推理内容，而非 DeepSeek 惯例的 `reasoning_content`，此前该内容被 Schema 静默丢弃。此修复对本地 Ollama 用户很重要。
   [查看 PR](https://github.com/anomalyco/opencode/pull/36068)

2. **[#46051] 修复 `PartUpdated` 事件反复 `structuredClone` 的性能问题** — 已关闭
   修复 #35107。`Session.updatePart` 在每次事件发布时对 part 做深拷贝，流式输出时 part 最大可达 488KB，93K 次事件造成严重的分配开销。此 PR 移除了不必要的克隆操作。
   [查看 PR](https://github.com/anomalyco/opencode/pull/46051)

3. **[#46044] 降低会话切换延迟** — 已关闭
   修复打开未访问会话时约半秒空白转录的问题。针对 v2 目标，涉及 bug fix 与重构。
   [查看 PR](https://github.com/anomalyco/opencode/pull/46044)

4. **[#46015] 确保 SSE 断开时释放流（Bun 平台）** — 已关闭
   关闭 #36311。修复 Bun 环境下客户端断开后 `ServerResponse.close` 不触发导致的 CPU 占用问题。
   [查看 PR](https://github.com/anomalyco/opencode/pull/46015)

5. **[#46074] Backport Effect-TS 上游修复：清理无效 location** — 打开
   临时将 Effect-TS 上游修复移植到当前固定的 Effect 版本，避免无效 location 导致的异常。
   [查看 PR](https://github.com/anomalyco/opencode/pull/46074)

6.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-08-29）

## 今日速览

- 发布正式版 **v0.22.3** 和夜间版 **v0.22.3-nightly.20260829**，带来 Channels 命名会话、daemon 扩展安装路径校验以及 CUA 驱动预编译二进制更新。
- 社区聚焦 Web Shell 稳定性：多个 UI/交互 bug（无限渲染循环、会话切换卡死、编辑索引错位）被集中报告，相关修复 PR 已陆续提交。
- 核心修复方向包括：HTTP 413 自动压缩恢复、本地 llama-server 兼容性、Agent Team 清理可靠性，以及 review/CI 流程的大量自动化/容错增强。

---

## 版本发布

### v0.22.3（正式版）

- **Channels 命名会话**：支持按 owner 管理最多 8 个持久任务会话（[#10198](https://github.com/QwenLM/qwen-code/pull/10198)）。
- **daemon Extension 安装**：允许绝对本地路径，拒绝相对路径。
- **cua-driver-rs v0.20.2**：更新 Qwen CUA Driver 预编译二进制——macOS 提供已签名/公证的通用二进制和 `QwenCuaDriver.app`；Linux/Windows 提供 x86_64 + arm64 版本；同时发布 `@qwen-co` 相关 npm 包。

### v0.22.3-nightly.20260829.e5cb60ad48

- `feat(web-shell):` 在分支选择器操作旁显示 git 状态提示（[#10397](https://github.com/QwenLM/qwen-code/pull/10397)）。
- `feat(review):` 引入针对 review 的流式状态输出增强（详见 PR #10397 相关变更）。

---

## 社区热点 Issues

### 1. 0.22.1 中 edit/write_file 在配置 permissions.allow 后静默消失（#10075）
**状态：已关闭 | P1 | 评论 4**

配置 allowlist 后，未被覆盖的工具会从会话中完全消失，导致 `tool_search` 找不到工具。社区强烈建议发布前增加冒烟测试，该问题已关闭但值得关注。

🔗 https://github.com/QwenLM/qwen-code/issues/10075

### 2. Anthropic 通道缺少 OpenAI 通道已有的流安全保护（#9005）
**状态：进行中 | P1 | 评论 8**

`anthropicContentGenerator` 在流式响应处理上缺少 OpenAI 侧已具备的保护机制，可能与 SDK 版本过旧有关，影响使用 Anthropic 兼容模型的稳定性。

🔗 https://github.com/QwenLM/qwen-code/issues/9005

### 3. Bailian 个人 Token Plan 模型列表不同步，图像/视频生成失败（#8432）
**状态：OPEN | P2 | 评论 5 | 👍 1**

`/auth` 中内置的阿里云百炼 Token Plan 模型列表与实际控制台不一致，导致相关模型的 image/video 生成功能不可用。已标记 ready-for-human，等待维护者更新模型清单。

🔗 https://github.com/QwenLM/qwen-code/issues/8432

### 4. 自动压缩无法从 HTTP 413 错误中恢复（#10380）
**状态：OPEN | P2 | 评论 3**

当 OpenAI-compatible 网关前有请求体大小限制时，长会话会因 413 永久卡死。该问题直接催生了修复 PR #10408，属于核心健壮性缺陷。

🔗 https://github.com/QwenLM/qwen-code/issues/10380

### 5. VS Code 插件 closeDiff 未执行 showDiff 的路径解析（#10372）
**状态：OPEN | P2 | 评论 4**

`closeDiff` 跳过了 `showDiff` 中的 workspace-relative 路径解析，导致在特定工作区布局下 diff 关闭失败。属于 VS Code 集成细节 bug，已附上定位分析与后续修复建议。

🔗 https://github.com/QwenLM/qwen-code/issues/10372

### 6. 新版本导致本地 llama-server 推理崩溃：grammar 解析失败（#10435）
**状态：OPEN | P2 | 评论 3**

v0.22.3 在本地 llama-server 上执行代码 review 时报错 `[API Error: 400 Failed to initialize samplers: failed to parse grammar]`，其他 harness 不受影响。影响本地模型用户，需要兼容性修复。

🔗 https://github.com/QwenLM/qwen-code/issues/10435

### 7. Web Shell 在 daemon 不可达时无限 re-render 循环（#10406）
**状态：OPEN | P2 | 评论 3**

`connection.error` 持续存在，内联 `onError` 导致 effect 每次渲染都重新触发，最终无限循环。由 PR #9811 引入，需重构错误处理回调。

🔗 https://github.com/QwenLM/qwen-code/issues/10406

### 8. Agent Team：team_delete 在文件系统清理失败后仍报告成功（#10210）
**状态：OPEN | P2 | 评论 4**

静态检查发现 `deleteTeamDirs()` 中的 `fs.rm` 操作被 `Promise.allSettled` 包裹，失败时不会向上抛出，导致用户看到“删除成功”但残留文件。多智能体功能可靠性隐患。

🔗 https://github.com/QwenLM/qwen-code/issues/10210

### 9. review 过滤器可被 include 指令绕过隐藏 repo 本地过滤规则（#10441）
**状态：OPEN | P2 | 评论 3 | ready-for-agent**

`localFilterCommands` 使用 `git config --file` 读取配置，不会展开 `include.path`/`includeIf`，因此攻击者可通过 include 指令隐藏本地过滤规则，形成安全盲区。已提出按源文件解析的修复方向。

🔗 https://github.com/QwenLM/qwen-code/issues/10441

### 10. 无 .git 文件夹禁止 git 操作，对 submodule 不合理（#10448）
**状态：OPEN | P3 | 评论 2**

最近版本强制要求存在 `.git` 才能执行 git 操作，但在 submodule 场景下工作目录没有 `.git` 却仍可执行 git 命令。用户建议移除简单目录检查，改为实际调用 git 命令验证。

🔗 https://github.com/QwenLM/qwen-code/issues/10448

---

## 重要 PR 进展

### 1. feat(cli): OpenTUI 迁移第 4 批——对话框、命令与会话回退（#10383）
OpenTUI 迁移计划持续推进，本批包含 19 个对话框模块（auth、extensions、MCP、memory-status 等）以及命令路由基础设施，是 CLI UI 全面重构的重要一步。

🔗 https://github.com/QwenLM/qwen-code/pull/10383

### 2. fix(core): HTTP 413 通过一次性压缩恢复模型请求（#10408）
针对 #10380 的修复：当网关因请求体超限返回 413 时，自动触发与 token 溢出相同的 reactive 压缩路径，避免长会话永久不可用。

🔗 https://github.com/QwenLM/qwen-code/pull/10408

### 3. feat(web-shell): 脏工作区也可更新项目（#10390）
“Update Project”不再因未提交变更而中止，而是提供冲突解决面板，支持 stash/checkout 等两种前进方式，提升 Web Shell 的 git 操作体验。

🔗 https://github.com/QwenLM/qwen-code/pull/10390

### 4. feat(review): 在任何 agent 运行前预构建 review worktree（#10423）
CI 上的 review 流程现在会在 agent 启动前完成工作区安装和编译，显著减少后续 agent 等待构建的时间，提升 review 自动化效率。

🔗 https://github.com/QwenLM/qwen-code/pull/10423

### 5. fix(web-shell): 消息编辑在 transcript 窗口不完整时 fail closed（#10419）
修复了编辑消息时使用窗口内局部索引而非会话全局索引的问题，避免重新生成快照定位错误。

🔗 https://github.com/QwenLM/qwen-code/pull/10419

### 6. feat(core): 绑定通过 `gh pr create` 创建的 PR 到当前会话（#9739）
补全 session↔PR 绑定机制：现在 agent 在 shell 中直接运行 `gh pr create` 创建的 PR 也能自动绑定到会话，并带有 live/completed 两条检测路径。

🔗 https://github.com/QwenLM/qwen-code/pull/9739

### 7. fix(cli): 会话启动时显示活动定时任务（#10053）
交互式会话启动时若存在有效的定时任务，会显示 `N active scheduled task(s). Run /loop list to inspect.`，支持新会话和恢复会话。

🔗 https://github.com/QwenLM/qwen-code/pull/10053

### 8. feat(cli): 将已完成的 read/search 工具批次折叠进思考行（#9503）
当模型思考后立即执行信息收集工具，TUI 不再分别渲染“思考 9s”和“搜索了 alpha, beta”两行，而是合并为一行更紧凑的摘要，提升转录可读性。

🔗 https://github.com/QwenLM/qwen-code/pull/9503

### 9. fix(core): heredoc 主体不参与权限规则拆分（#9417）
修复权限匹配中 heredoc 被错误拆分的问题，让 `Bash(python *)` 等规则能正确匹配 Python heredoc 为一条命令，同时规避歧义和注入风险。

🔗 https://github.com/QwenLM/qwen-code/pull/9417

### 10. feat(channels): 用 sessionRotation 限制会话生命周期（#8927）
新增 per-channel `sessionRotation` 选项，支持 `maxTurns` 与 `maxAge` 两种界限，超限后下条消息自动使用新会话，适合长期运行且需要定期清理上下文的场景。

🔗 https://github.com/QwenLM/qwen-code/pull/8927

---

## 功能需求趋势

- **Web Shell 交互完善**：持续集中修复 git 状态展示、会话切换、消息编辑、侧栏工作区概览、MCP Apps 渲染等问题，Web Shell 正成为与原生 CLI 并重的核心界面。
- **多智能体（

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*