# AI CLI 工具社区动态日报 2026-08-25

> 生成时间: 2026-08-24 22:47 UTC | 覆盖工具: 7 个

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

**数据来源**: github.com/anthropics/skills | **数据截止**: 2026-08-25

---

## 一、热门 Skills 排行

以下 PR 按社区讨论热度（评论数）排序，当前全部处于 **Open** 状态，尚无 merge 记录。

| # | Skill / PR | 功能 | 社区讨论热点 | 状态 |
|---|---|---|---|---|
| 1 | **#1298** skill-creator 评测修复<br>[@MartinCajiao](https://github.com/MartinCajiao) | 修复 `run_eval.py` 对所有 skill 报告 0% recall 的严重缺陷，包含 Windows 流读取、触发检测、并行 worker 三项修复 | 关联 issue #556（12 评论、7 👍），已被 10+ 用户独立复现。核心争议是：描述优化循环一直在"对噪声做优化"，整个 skill-creator 评测信号可信度存疑 | **Open** |
| 2 | **#514** document-typography<br>[@PGTBoos](https://github.com/PGTBoos) | 为 AI 生成文档提供排版质量控制：孤词折行、孤行段落（标题滞留页底）、编号错位等 | 讨论集中在"AI 生成的文档普遍存在排版问题，但用户极少主动提出"，属于高频刚需场景 | **Open** |
| 3 | **#1615** scnet-hpc<br>[@lql341](https://github.com/lql341) | 通过 profile 化 SSH + Slurm 工作流操作 SCNet HPC 集群，覆盖分区、内存、模块与加速器配置 | 关注点：HPC 场景下 skill 如何安全封装 SSH 凭据与集群配置 | **Open** |
| 4 | **#538** pdf 大小写引用修复<br>[@Lubrsy706](https://github.com/Lubrsy706) | 修复 `skills/pdf/SKILL.md` 中 8 处 `REFERENCE.md`/`FORMS.md` 与真实小写文件名不一致的问题 | 评论聚焦于 case-sensitive 文件系统（Linux/CI）下文档型 skill 的可靠性；同作者还提交了 #539、#541 两个 skill-creator/docx 修复，形成系列贡献 | **Open** |
| 5 | **#486** ODT skill<br>[@GitHubNewbie0](https://github.com/GitHubNewbie0) | 支持 OpenDocument 格式（.odt/.ods）的创建、模板填充、ODT 转 HTML | 讨论点：开源/ISO 标准格式支持是 LibreOffice 用户的核心诉求，触发词设计是否合理 | **Open** |
| 6 | **#210** frontend-design 修订<br>[@justinwetch](https://github.com/justinwetch) | 重写 frontend-design skill，提升指令清晰度、可执行性与内部一致性 | 中心议题：如何让 skill 指令"在单次对话内可被 Claude 真正执行"，而非停留在抽象原则 | **Open** |
| 7 | **#83** skill-quality-analyzer 与 skill-security-analyzer<br>[@eovidiu](https://github.com/eovidiu) | 两个 meta skill：从结构/文档/示例等五维评估 skill 质量；从安全维度审计 skill 风险 | 高讨论度源于与 #492 安全 issue 的呼应——社区对 skill 信任边界高度关注 | **Open** |
| 8 | **#541** docx w:id 冲突修复<br>[@Lubrsy706](https://github.com/Lubrsy706) | 修复 DOCX skill 在添加

---

# Claude Code 社区动态日报 — 2026-08-25

## 今日速览

今日无新版本发布，但社区动态密集：**Linux 版 v2.1.242 被曝启动即崩溃的严重回归**（可能是 mimalloc 符号导出问题），引发高度关注；**跨机器多智能体协作**的长期功能请求（#28300）讨论量持续走高，已达 44 条评论；此外，**模型生成的 ugrep 正则耗尽 13.6GB 内存**的资源滥用问题也引起社区对工具安全边界的讨论。

## 社区热点 Issues

以下为过去 24 小时内更新、值得关注的 10 个 Issue：

### 1. v2.1.242 Linux 启动即崩溃（严重回归）
- **#89334** · [链接](https://github.com/anthropics/claude-code/issues/89334) · ✅ 3 👍
- v2.1.242（Linux x64 原生安装）在 `main` 之前即段错误，连 `claude --version` 都无法执行。作者定位到根因：v2.1.242 首次将捆绑的 mimalloc 导出为版本化 glibc 分配器符号，而 mimalloc 的 `free` 缺少 NULL 检查，与 glibc `newlocale` 的 `free(NULL)` 调用冲突；v2.1.241 不受影响。由于是启动即崩，影响面极广，社区评价：此回归绝对紧急，应优先热修复。

### 2. Bundled ugrep 无内存限制，可被模型生成的 regex 打爆
- **#86238** · [链接](https://github.com/anthropics/claude-code/issues/86238) · ✅ 2 👍
- `Grep` 工具将 Claude Code 二进制重新 exec 为 `ugrep`，但既不设 `RLIMIT_AS`/`RLIMIT_CPU`，也没有 wall-clock 超时。实测一个病态模式消耗了 **13.6 GB 内存**并严重拖垮宿主机。这揭示了一个安全边界问题：当模型自主生成搜索模式时，缺少防护机制可能导致资源耗尽。

### 3. 跨机器多智能体协作（Agent-to-Agent 协议）
- **#28300** · [链接](https://github.com/anthropics/claude-code/issues/28300) · 44 评论
- 自 2 月提出后讨论热度持续，是当前评论数最高的开放 Issue。核心诉求是让不同机器上的 Claude Code 实例能通过标准协议相互发现、通信与协作。与之相关的 #89338（跨会话 peer 地址在 session resume 后失效）也在今日被提出，表明多实例协调已成为社区高频场景。

### 4. Claude Desktop 排序失效 Bug
- **#56060** · [链接](https://github.com/anthropics/claude-code/issues/56060) · 13 👍
- 在按项目分组（Group by: Project）时，排序方式（Sort by: Recency）完全不生效。在 5 月提出、已积累了 15 条评论和 13 个赞，是当前点赞数最高的 Issue。用户期待桌面端会话管理逻辑能尽快修复。

### 5. Claude Desktop MSIX 在 Intel 集显上崩溃
- **#83028** · [链接](https://github.com/anthropics/claude-code/issues/83028) · 13 评论
- Windows MSIX 版本在 Intel 集成 GPU 上使用浏览器面板时必现崩溃，无任何 workaround。创建于 8 月 1 日，已持续近一个月，评论数仍在增长，反映桌面端稳定性的迫切问题。

### 6. 子代理结果路由至根 Teammate 而非发起者
- **#69212** · [链接](https://github.com/anthropics/claude-code/issues/69212) · ✅ 3 👍
- 当 teammate agent 再派生子代理时，子代理的结果没有回到派生的 teammate，而是错误路由到根 teammate。这个问题影响多代理协作的上下文隔离，评论中获得 3 个 👍，说明不少用户遇到了类似的多层代理场景。

### 7. Max20x 计划周刊限额异常跳变
- **#69430** · [链接](https://github.com/anthropics/claude-code/issues/69430) · ✅ 6 👍
- 用户报告「Max20x 计划周刊上限在不到一小时内从 ~50% 跳到 100%」，在 VS Code 和 macOS 上均有复现，并已关闭（可能已修复）。该 Issue 获得了 6 个 👍，说明成本/额度透明性是用户高度敏感的话题。

### 8. 使用策略分类器对安全术语误报
- **#61625** · [链接](https://github.com/anthropics/claude-code/issues/61625) · ✅ 2 👍
- 模型在生成安全相关术语（如 "Black Hat briefings"）时被 Use Policy 分类器误判为违规并拦截。开发者生成安全内容并非恶意，但会被策略系统误伤，说明安全检测与开发者合法需求间的平衡仍需打磨。

### 9. php-lsp 插件（intelephense）忽略项目级配置
- **#83470** · [链接](https://github.com/anthropics/claude-code/issues/83470)
- PHP 语言服务器插件不读取 `intelephense.config.json` 中的 `environment.includePaths` 等项目级设置，导致 LSP 无法正确处理项目环境。该问题已复现，属于插件生态的集成质量问题。

### 10. 请求正式支持 GitHub Virtual Filesystem（VFS）
- **#83696** · [链接](https://github.com/anthropics/claude-code/issues/83696) · ✅ 1 👍
- 用户希望在 Claude Code 及其 VS Code 扩展中正式支持 `vscode-vfs://` 等虚拟/远程工作区。目前打开 VFS 工作区时不仅无法优雅降级，某些情况下甚至会导致崩溃。随着远程开发普及，这一需求预计会持续升温。

## 重要 PR 进展

过去 24 小时内 PR 更新较少，共计 3 条，无合并更新，以下为全部内容：

### 1. Add Claude apps gateway on AWS example deployment assets
- **#79898** · [链接](https://github.com/anthropics/claude-code/pull/79898) · 已关闭（未合并）
- 为 Claude Apps Gateway 的 AWS 部署提供参考资产，基于 Amazon Bedrock，与现有 `examples/gateway/gcp` 对照，位于 `examples/gateway/aws/`。附带教程文档即将发布在 code.claude.com/docs。该 PR 说明 Anthropic 正在完善 AWS 上的官方部署指南。

### 2. Create pylint.yml
- **#83890** · [链接](https://github.com/anthropics/claude-code/pull/83890) · 开放中
- PR 内容为空，仅添加了一个 pylint CI 工作流文件。推测是社区贡献者为仓库引入 Python 静态检查（可能用于示例代码或工具脚本），目前缺乏描述信息，关注度有限。

### 3. docs: clarify plugin MCP configuration scope
- **#75252** · [链接](https://github.com/anthropics/claude-code/pull/75252) · 已关闭（未合并）
- 文档澄清：插件内的 `mcpServers` 配置仅用于插件自带的 MCP server 定义，与用户级 `~/.claude.json` 中的 MCP allow/deny 列表相互独立。该 PR 从 #74857 重新打开（原仓库被删），说明社区对插件 MCP 配置的作用域存在普遍困惑，文档澄清很有必要。

## 功能需求趋势

从近期 Issues 中可以提炼出以下社区关注的功能方向：

1. **多智能体协作（Multi-agent / Multi-session）**：跨机器 Agent-to-Agent 协议（#28300）、跨会话消息传递与稳定寻址（#89338）等，表明用户正在把 Claude Code 当作分布式协作系统使用，而不仅是单会话工具。

2. **桌面端体验与稳定性**：排序失效（#56060）、Intel GPU 崩溃（#83028）、会话状态指示不准确（#73662）、分屏快捷键缺失（#73679）等占比较高，说明桌面端已从「可用」迈向「好用」的精细化阶段。

3. **资源使用与安全边界**：ugrep 无资源限制（#86238）、插件/技能自动更新防偏离（#73681）、PreResponse hook 约束输出等，反映用户开始关注 Agent 在自主运行时的资源消耗可控性与安全防护。

4. **IDE 与远程开发集成**：GitHub VFS 支持（#83696）、跨平台 CLI 可靠性（Windows `!` 命令静默失败 #73671）等，说明用户希望在更多开发环境中无缝使用。

5. **成本与配额透明度**：周刊限额异常跳变（#69430）、模型意外升级导致费用变化（#73672）等引发讨论，用户希望用量记录更加透明可审计。

## 开发者关注点

综合 Issue 反馈，开发者目前最头痛的高频问题包括：

- **多会话同目录工作区冲突**：同一仓库多个 Claude Code 会话可能静默切换彼此的分支（#60295），导致协作场景下心智模型失效。
- **环境变量与认证被忽略**：`CLAUDE_CODE_OAUTH_TOKEN` 在首次运行时被 onboarding 流程覆盖（#73403），自动化/CI 场景受影响。
- **模型不听指令/走捷径**：多条反馈（#87445、#87418）抱怨 Agent 「凭习惯行事」而没有基于当前规则重新评估指令，且有「需要复现」（needs-repro）标签，说明此类问题尚难稳定复现。
- **自动更新的副作用**：自动引入 MCP 连接器（#73682）、插件更新时机不合理（#73681）等，让用户觉得「Claude 自作主张」，希望有更明确的控制权。
- **Hook 机制的语义问题**：Stop hook 匹配「整个对话历史」而非「当前状态」（#73674），可能阻止正常收尾；同时缺少 PreResponse hook（#73669）来在输出前拦截不符合约束的内容。

如需跟踪上述任一 Issue 的进展，可直接点击对应链接跳转 GitHub。本日报数据截至 2026-08-24 日 UTC。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-25

## 1. 今日速览

今日社区热度集中在桌面端**认证稳定性问题**：多个 Issue 报告 macOS/Windows 桌面 App 在恢复会话时反复登出或直接失效，其中 #39162 已积累 51 条评论，成为当前最受关注的问题。代码层面，昨日密集合并了 20+ 个由 copyberry[bot] 提交的 PR，覆盖 Multi-Agent V2 子代理所有权、Guardian v2 审查范围、Windows 沙箱 ACL 修复等方向，系统稳定性与内部架构治理仍是当前迭代主轴。

## 2. 版本发布

过去 24 小时共发布 3 个版本，均无详细变更说明：

- [rust-v0.150.0-alpha.8](https://github.com/openai/codex/releases/tag/rust-v0.150.0-alpha.8)：0.150.0-alpha.8
- [rust-v0.149.1](https://github.com/openai/codex/releases/tag/rust-v0.149.1)：完整变更日志见 [compare/rust-v0.149.0...rust-v0.149.1](https://github.com/openai/codex/compare/rust-v0.149.0...rust-v0.149.1)
- [rust-v0.149.0-alpha.4.3](https://github.com/openai/codex/releases/tag/rust-v0.149.0-alpha.4.3)：0.149.0-alpha.4.3

> 注：三个版本均缺少详细的变更说明，建议关注发布链接中的 tag 对比获取更多信息。

## 3. 社区热点 Issues

以下 10 个 Issue 评论数或关注度最高，反映了当前用户最迫切的痛点：

**1. [macOS 打开历史会话导致 ChatGPT 认证失效并跳转登录页](https://github.com/openai/codex/issues/39162)** — 51 评论 / 31 👍
评论数最高的 Issue。macOS 桌面端（build 6720）打开既有会话后，ChatGPT 认证被意外失效，用户被强制登出。自 8/18 创建以来持续发酵，多个用户确认复现。

**2. [gpt-5.6-luna 被标记为 MultiAgent V1，导致 V2 spawn_agent 拒绝使用](https://github.com/openai/codex/issues/35097)** — 29 评论 / 51 👍
👍 数最高。模型 `gpt-5.6-luna` 的 MultiAgent 版本标记为 V1，与 V2 的 spawn_agent 机制不兼容，开发者被迫回退到较低版本。已持续一个月仍未修复，社区关注度高。

**3. [分页历史记录丢失有效的扁平化 rollout 记录并重复使用序号](https://github.com/openai/codex/issues/35746)** — 25 评论
CLI 在分页加载历史时出现 `RolloutLine` 解码不一致，导致记录丢失和序号错乱。影响 `0.146.0-alpha.10.1` 及之后版本。

**4. [Windows/WSL 集成终端在 PTY 启动前静默失败，侧边栏无法打开](https://github.com/openai/codex/issues/37104)** — 19 评论 / 9 👍
Windows 桌面版在 WSL 环境下集成终端静默失败，同时底部/侧边面板无法打开。Windows 用户高频反馈问题。

**5. [App 中近期 Thread 历史被清空，但 CLI 中仍存在](https://github.com/openai/codex/issues/17354)** — 14 评论 / 7 👍
桌面 App 丢失最近 2-3 个月的会话历史，但 CLI 侧数据完好，暗示 App 层的数据同步或存储存在严重缺陷。

**6. [自动压缩（auto compaction）应暴露给 agent](https://github.com/openai/codex/issues/21777)** — 9 评论 / 9 👍
用户希望在长任务运行中主动感知并控制上下文压缩，而不是让压缩在后台静默发生。

**7. [config.toml 自动迁移生成不兼容的 permissions 配置，--strict-config 解析失败](https://github.com/openai/codex/issues/40339)** — 5 评论
CLI 0.149.1 自动迁移生成的 `default_permissions = "protect-env"` 块无法通过 `--strict-config` 校验，且 `sandbox_workspace_write.network_access` 被静默忽略。属于高危配置兼容性问题，升级用户需谨慎。

**8. [macOS 线程恢复导致登出：refresh token 未持久化到 auth.json，新登录在 76 秒内失效](https://github.com/openai/codex/issues/40267)** — 6 评论
与 #39162 高度相关的认证问题，OAuth refresh 流程存在缺陷，新登录也会在极短时间内再次失效。

**9. [MCP tools/list_changed 通知不触发延迟工具缓存失效或重新拉取](https://github.com/openai/codex/issues/33266)** — 5 评论 / 4 👍
启用 `tool_search_always_defer_mcp_tools` 后，MCP 服务器通知不会导致缓存失效，动态工具列表无法更新。

**10. [Hooks: PostToolUse 载荷缺失失败信号，PostToolUseFailure 从不触发](https://github.com/openai/codex/issues/34289)** — 6 评论
CLI hooks 系统中 `PostToolUse` 无法区分工具调用成功与否，而 `PostToolUseFailure` 事件虽然存在于二进制中但从未触发，导致基于 hooks 的自动化流程不可靠。

## 4. 重要 PR 进展

以下 10 个 PR 反映了代码库当前的核心演进方向（全部由 copyberry[bot] 于 8/24 提交并关闭）：

**1. [导出 turn 成本为 OTEL 指标](https://github.com/openai/codex/pull/40488)**
新增 `codex.turn.cost_microusd` 计数器，携带 turn/conversation/中断/速度/推理力度等维度，为成本观测提供标准化指标。

**2. [将 agent role 加载逻辑抽离为独立 crate](https://github.com/openai/codex/pull/40487)**
新增 `codex-agent-roles` crate，统一 agent role 的类型、解析、发现、校验与分层加载逻辑，减少 `codex-core` 的耦合。

**3. [为 turn 和工具分析添加根 turn ID](https://github.com/openai/codex/pull/40486)**
新增 `root_turn_id` 字段，用于将子代理（subagent）活动关联到顶层触发 turn，同时避免 steering 导致关联过期。

**4. [子环境中凭据别名代理（credential brokering）](https://github.com/openai/codex/pull/40484)**
使子环境可以继承父环境中被过滤的凭据提供者变量，并支持在更长的环境变量值中替换匹配的凭据。

**5. [支持 Amazon Bedrock 的托管 AWS 访问密钥](https://github.com/openai/codex/pull/40481)**
新增实验性 `amazonBedrockAccessKeys` 登录流程，凭据持久化至 auth store，用于 SigV4 签名的 Bedrock 请求。

**6. [新增仅计算机使用的 Guardian v2 审查范围](https://github.com/openai/codex/pull/40480)**
新增 `features.guardianv2.review_scope.computer_use_only`，将异步分类和快速审批限制在浏览器/计算机使用工具上，其余工具保留同步审批路径。

**7. [Multi-Agent V2 子代理通过父代理重新加载](https://github.com/openai/codex/pull/40477)**
修复子代理直接恢复时可能使用调用方设置而非父代理当前权限的问题，统一以父代理为权威来源。

**8. [请求 Windows 沙箱 ACL 更新时的读控制权限](https://github.com/openai/codex/pull/40475)**
修复 `SetSecurityInfo` 拒绝仅含 `WRITE_DAC` 的目录句柄的问题，新增 `READ_CONTROL` 权限并补充回归测试。

**9. [在支持的终端中将 Markdown 链接渲染为可点击标签](https://github.com/openai/codex/pull/40471)**
在支持超链接的终端中以青色下划线渲染链接标签，隐藏重复的目标地址；未知终端保留完整 URL。

**10. [批量执行沙箱能力根发现](https://github.com/openai/codex/pull/40443)**
同一沙箱上下文下的多个根目录可在一次沙箱辅助调用中完成能力发现，失败时回退到逐根发现。

## 5. 功能需求趋势

从今日 Issues 观察，社区最关注的功能方向包括：

- **认证与会话稳定性**：macOS/Windows 桌面端反复登出、refresh token 未持久化、更新后历史记录丢失等认证/会话问题呈集中爆发态势，是高优先级痛点。
- **Windows 平台体验全面修复**：WSL 终端失败、浏览器自动化不可用、鼠标卡顿、MSIX 自动更新器死循环、内核崩溃等问题，显示出 Windows 平台存在系统性质量问题。
- **Multi-Agent V2 生态兼容**：模型版本标记冲突（#35097）、子代理所有权控制（PR #40477、#40464）等，表明 Agent 架构的版本管理仍处于快速演进和不稳定期。
- **Hooks 与 MCP 机制完善**：Hook 失败信号缺失（#34289）、MCP 缓存失效（#33266）、MCP Stop hook 失败时 fail-open 等，自动化扩展能力是深度用户的核心诉求。
- **上下文管理可见性**：用户希望将自动压缩（compaction）暴露给 agent 主动控制（#21777）。

## 6. 开发者关注点

- **升级有风险，迁移需谨慎**：`config.toml` 自动迁移生成不兼容配置（#40339）导致 `--strict-config` 解析失败，这是升级到 0.149.1 后需要立即检查的配置兼容性隐患。
- **"应用有、CLI 正常"的割裂体验**：多个 Issue（#17354、#26157、#33771、#35135）均指向桌面 App 在更新或项目重建后丢失会话/历史记录，而 CLI 数据完好，说明 App 层的数据持久化与迁移逻辑存在问题。
- **桌面端认证是最大的信任危机**：#39162、#39218、#40267 三个独立问题都指向"打开会话导致登出"，且新登录也很快失效。对于依赖桌面端的用户，这已经影响到了基本可用性。
- **Hook 生态期待"诚实"的信号**：开发者在构建自动化工作流时，需要可靠的工具调用成功/失败信号以及对应的失败回调，当前 `PostToolUseFailure` 形同虚设，限制了 hooks 的使用场景。
- **MCP 集成仍有暗坑**：动态工具列表变更无法刷新、MCP 服务器不可用时 Stop hook 意外放行，MCP 相关的边界情况处理尚不够健壮。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-25

## 今日速览

昨日发布 v0.56.0 系列新夜间版，功能迭代持续进行。社区讨论热度集中在 Agent 子代理的可靠性问题（如超时误报成功、工具使用不充分）以及安全相关的环境变量处理。此外，多份 PR 聚焦于 Git 环境变量清洗与 CLI 文档补全，显示项目在安全加固与开发者体验两方面同步推进。

---

## 版本发布

**v0.56.0-nightly.20260824.g5411f113c** — 常规夜间更新，无显著特性说明。完整变更见：
https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260823.g5411f113c...v0.56.0-nightly.20260824.g5411f113c

---

## 社区热点 Issues

挑选评论数最多、讨论最活跃的 10 个 Issue：

**1. 子代理达到 MAX_TURNS 被误报为 GOAL 成功**（#22323，评论 13）
`codebase_investigator` 子代理在超时未做分析时仍返回 `status: success`，掩盖了真实的中断原因，影响对 Agent 行为的判断。社区讨论热烈，属于高优先级 P1 缺陷。
https://github.com/google-gemini/gemini-cli/issues/22323

**2. Gemini 不主动使用 skills 和 sub-agents**（#21968，评论 6）
用户报告即使有合适的自定义技能（如 gradle/git），模型也很少主动调用，只在明确指令下才使用，限制了 Agent 的自动化潜力。
https://github.com/google-gemini/gemini-cli/issues/21968

**3. Auto Memory 对低信号会话无限重试**（#26522，评论 5）
后台提取代理跳过低价值会话后，这些会话不会被标记为已处理，导致反复出现在待处理队列中，浪费资源。
https://github.com/google-gemini/gemini-cli/issues/26522

**4. Shell 命令执行完仍卡在 "Waiting input"**（#25166，评论 4，👍 3）
用户反复遇到简单 CLI 命令结束后界面仍挂起的问题，严重影响交互体验。P1 优先级，社区呼声较高。
https://github.com/google-gemini/gemini-cli/issues/25166

**5. 浏览器子代理在 Wayland 下失败**（#21983，评论 4）
浏览器子代理在 Wayland 环境无法正常工作，属于 P1 缺陷，影响 Linux 用户的使用。
https://github.com/google-gemini/gemini-cli/issues/21983

**6. 工具数量超限导致 400 错误**（#24246，评论 3）
当可用工具超过 400 个时 CLI 报错，用户期望 Agent 能按需“裁剪”工具范围而非直接失败。
https://github.com/google-gemini/gemini-cli/issues/24246

**7. 模型随意在随机位置创建临时脚本**（#23571，评论 3）
模型被限制 shell 执行后，转而把编辑脚本写到各种目录，给工作区清理带来负担。
https://github.com/google-gemini/gemini-cli/issues/23571

**8. Agent 应避免破坏性行为**（#22672，评论 3）
处理复杂 Git 操作或数据库维护时，模型有时使用 `git reset`、`--force` 等危险命令，社区希望能有安全护栏。
https://github.com/google-gemini/gemini-cli/issues/22672

**9. 浏览器 Agent 忽略 settings.json 配置覆盖**（#22267，评论 3）
`AgentRegistry` 虽正确读取了设置，但 `BrowserManager` 未使用，导致 `maxTurns` 等配置不生效。
https://github.com/google-gemini/gemini-cli/issues/22267

**10. bug 报告缺少子代理上下文**（#21763，评论 2）
`/bug` 生成的报告只包含主会话信息，没有子代理内部日志，排障困难。
https://github.com/google-gemini/gemini-cli/issues/21763

---

## 重要 PR 进展

**1. 修复：保留 ask_user 问题到文本历史**（#29022，OPEN）
新增 `ui.keepAskUserQuestionsInHistory` 配置，恢复会话时能追溯此前问答选择，提升可追溯性。
https://github.com/google-gemini/gemini-cli/pull/29022

**2. 修复：write 策略中顶层安全检查器声明**（#28961，CLOSED）
将 `AllowedPathChecker` 改为标准顶层 `[[safety_checker]]` 写法，确保 `write_file`/`replace` 能正确注册安全策略。
https://github.com/google-gemini/gemini-cli/pull/28961

**3. 安全：扩展程序环境变更需用户同意并清除危险变量**（#28863，OPEN）
MCP server 启动时注入的额外环境变量不再绕过用户确认，同时过滤可能改变运行时行为的敏感变量。
https://github.com/google-gemini/gemini-cli/pull/28863

**4. 安全：保持 GIT_CONFIG_* 三元组内部一致性**（#28938，OPEN）
修复消毒处理导致成对 Git 配置被拆散后无法解析的问题，防止敏感 Git 配置在 Shell 执行中被还原。
https://github.com/google-gemini/gemini-cli/pull/28938

**5. 优化：重试提示注入以保留前缀缓存**（#28914，OPEN）
将 on-retry nudge 消息从 `systemInstruction` 移到 `contents` 尾部，显著提高缓存命中率，减少 API 请求量。
https://github.com/google-gemini/gemini-cli/pull/28914

**6. 修复：避免持久化“响应被中断”占位文本**（#28939，OPEN）
修复后，中断后的占位符不再作为模型消息保存，防止模型后续重复输出该串文本。
https://github.com/google-gemini/gemini-cli/pull/28939

**7. 修复：symlink/junction 技能目录去重**（#29017，OPEN）
解决 `.gemini` 与 `.agents` 通过软链接或 Windows junction 指向同一目录时技能被重复加载的问题。
https://github.com/google-gemini/gemini-cli/pull/29017

**8. 安全：清除 getSafeGitEnv 中影响执行的 GIT_* 变量**（#29008，OPEN）
修复 `.env` 中其他 GIT_* 变量（如 `GIT_EDITOR`、`GIT_SSH_COMMAND`）未过滤即参与 Git 操作的安全隐患。
https://github.com/google-gemini/gemini-cli/pull/29008

**9. 文档：补全缺失的 CLI 标志**（#29013，OPEN）
为 `--policy`、`--session-id`、`--raw-output` 等 6 个已注册但未文档化的标志补充说明。
https://github.com/google-gemini/gemini-cli/pull/29013

**10. 文档：修正环境变量重编辑设置键名**（#29009，OPEN）
文档中的配置键名与 schema 不一致，已修正并补充实际启用的键。
https://github.com/google-gemini/gemini-cli/pull/29009

---

## 功能需求趋势

- **Agent 自主性与可控性**：社区最关注如何让主 Agent 更智能地使用 skills/sub-agents（#21968），同时希望子代理可以后台运行、能并行协作（#22600/22602/22741）。
- **安全与隐私加固**：Auto Memory 的日志脱敏与确定性重编辑（#26525）、子代理无提示读本地文件（#26526）以及环境变量注入防护是近期安全焦点。
- **AST 感知工具探索**：多个 Issue 在调研用 AST 感知的读取和搜索工具来减少 token 消耗、提升代码定位精度（#22745/22746/22747），可能对未来代码库导航能力产生重要影响。
- **记忆系统改进**：Auto Memory 在处理低信号会话、无效 patch 时存在行为缺陷（#26516/26522/26523），社区对后台记忆系统的稳定性提出更高要求。
- **终端体验优化**：终端 resize 闪烁、高刷渲染（#21924）与交互卡死（#25166）的问题被反复提及，体验优化需求迫切。

---

## 开发者关注点

- **误报与假象成功**：子代理在任务中断或被截断时仍返回 GOAL 成功，导致用户对整个 Agent 的信任度下降（#22323）。
- **上下文不透明**：bug 报告、`/chat share` 缺少子代理的轨迹记录，用户难以及时定位问题根因（#21763、#22598）。
- **Shell 交互可靠性**：命令执行完仍提示 “Waiting input”、创建 vite 应用卡在交互式提示（#22465），这类基础交互故障直接影响可用性。
- **破坏性命令风险**：Git 与数据库相关操作中，模型倾向使用 `--force`/`reset` 等危险指令，社区普遍希望能有安全护栏或确认机制（#22672）。
- **配置被静默忽略**：浏览器 Agent 不识别 `settings.json` 中的 `maxTurns` 等覆盖配置，用户对配置失效感到困扰（#22267）。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-08-25）

> 基于 GitHub 上 github/copilot-cli 截至 2026-08-24 的公开动态整理。

## 今日速览

昨日发布 v1.0.81-9 小版本，主要改进 `/model` 选择器中的模型数据保留警告。社区讨论热度集中在 **MCP OAuth 认证问题**（Atlassian、Entra ID 等持续受影响）和 **CLI 在 code review 场景下频繁返回 400 错误**。功能需求方面，多轮 `/ask`、交互模式工具白名单、`/fork` 新终端等呼声较高。

## 版本发布

- **v1.0.81-9**
  - 改进：`/model` 选择器中展示模型数据保留警告，并附带相关链接。

## 社区热点 Issues

以下挑选 10 个过去 24 小时内最值得关注的 Issue：

- [#1274 CLI constantly getting 400 errors for invalid request body](https://github.com/github/copilot-cli/issues/1274)  
  作者对 diff 文件执行 code review 时，约 95% 的请求返回 400 错误。已提供 debug logs，问题可能出在客户端请求构造或服务端校验。  
  **社区反应**：27 评论 / 11 👍，是当前讨论度最高的 bug。

- [#1973 Feature Request: Tool whitelist for Interactive Mode](https://github.com/github/copilot-cli/issues/1973)  
  希望为交互模式提供细粒度工具白名单，而不是只能手动逐个批准或使用 `--allow-all` 放行所有操作（包括危险操作）。  
  **社区反应**：12 评论 / 27 👍，是近期最受关注的功能请求。

- [#4490 Atlassian MCP OAuth authentication broken in 1.0.80 (RFC 8414 §3.3 regression)](https://github.com/github/copilot-cli/issues/4490)  
  1.0.80 中 Atlassian MCP 的 OAuth 认证因 RFC 8414 issuer 不匹配而失败，1.0.78 正常。该 issue 虽已关闭，但 [#4584](https://github.com/github/copilot-cli/issues/4584) 指出 1.0.81 prerelease 中仍存在类似问题。

- [#4582 MCP OAuth authorize request omits 'scope' parameter for Entra ID servers with static oauthClientId, causing AADSTS900144](https://github.com/github/copilot-cli/issues/4582)  
  针对使用静态 `oauthClientId` 的 Entra ID MCP 服务器，authorize 请求缺少 `scope` 参数，导致 AADSTS900144 错误。  
  **社区反应**：新 issue，已获 2 条评论，MCP OAuth 问题仍在扩散。

- [#4421 MCP initialize handshake has a fixed, non-configurable 60s budget with no retry](https://github.com/github/copilot-cli/issues/4421)  
  MCP `initialize` 握手硬编码 60 秒超时且无重试，npx 启动的 stdio 服务器约 29% 会话会失败且无法恢复。  
  **社区反应**：2 评论，属于影响 MCP 生态可靠性的系统性缺陷。

- [#4566 Agent repeatedly acknowledges work without executing tool actions](https://github.com/github/copilot-cli/issues/4566)  
  在 gpt-5.3-codex 下，Agent 多次口头确认任务已开始，但不实际执行任何 tool 调用。  
  **社区反应**：2 评论 / 1 👍，模型行为异常类问题逐渐增多。

- [#4568 --cloud owner picker hangs, reconnect crashes, and task polling reaches 429](https://github.com/github/copilot-cli/issues/4568)  
  `copilot --cloud` 在无仓库上下文时卡在 “Loading available owners...”，有仓库上下文时云任务超时，并伴随重连崩溃和 polling 429。  
  **社区反应**：1 评论，cloud 模式的可用性问题值得关注。

- [#3255 Stale inuse.<pid>.lock files left behind on unclean exit (SIGKILL / crashes)](https://github.com/github/copilot-cli/issues/3255)  
  进程被 SIGKILL 或崩溃后，`~/.copilot/session-state/<uuid>/` 下残留 `inuse.<pid>.lock` 文件，导致后续会话无法恢复。  
  **社区反应**：1 评论，属于长期存在的会话状态管理缺陷。

- [#4570 Windows: plugin install/update fails with "Access is denied. (os error 5)" while VS Code is running](https://github.com/github/copilot-cli/issues/4570)  
  Windows 上只要 VS Code 正在运行，`copilot plugin install/update` 就会因文件锁失败；关闭 VS Code 后正常。  
  **社区反应**：1 评论，对 Windows 用户影响明显。

- [#4572 Background compaction can lose a completed parallel GPT tool result and cause HTTP 400](https://github.com/github/copilot-cli/issues/4572)  
  1.0.80 中，后台上下文压缩可能导致并行 GPT tool 调用结果丢失，并触发 `400 No tool output found for function call` 错误。  
  **社区反应**：1 评论，长会话场景下的稳定性隐患。

## 重要 PR 进展

过去 24 小时内仅检测到 1 条 PR 更新，且非实质代码改动：

- [#4573 Rename README.md to README.mdmain](https://github.com/github/copilot-cli/pull/4573)  
  作者 @phuongnam467 将 `README.md` 重命名为 `README.mdmain`，无描述信息，疑似低质量/测试 PR。  
  **状态**：OPEN，未合并，社区应谨慎对待。

目前没有看到合并或实质性功能修复的 PR 进展。

## 功能需求趋势

从近日 Issues 可以提炼出以下社区关注方向：

- **交互式会话能力扩展**：  
  - 多轮 `/ask`：允许在 `/ask` 内追问澄清 [#4577](https://github.com/github/copilot-cli/issues/4577)、[#4579](https://github.com/github/copilot-cli/issues/4579)  
  - `/fork` 支持打开新终端并行操作，或提供 `copilot --fork` 启动参数 [#4578](https://github.com/github/copilot-cli/issues/4578)、[#4580](https://github.com/github/copilot-cli/issues/4580)  
  - 交互模式工具白名单，避免 `allow-all` 一放全放 [#1973](https://github.com/github/copilot-cli/issues/1973)

- **MCP 与认证修复**：OAuth 兼容性、scope 传参、握手超时重试等是当前最集中的痛点，涉及 Atlassian、Entra ID、github-mcp-server 等多个方向。

- **Token 成本与效率**：  
  [#4588](https://github.com/github/copilot-cli/issues/4588) 指出非 Anthropic 模型上 Tool Search/MCP tool deferral 未生效，导致一个 `"hi"` 提示词消耗 21.6k input tokens，社区开始关注 token 成本控制。

- **状态栏与可观测性**：请求显示原始 token 数、路径和分支支持尾部对齐截断等 UI 细节 [#4589](https://github.com/github/copilot-cli/issues/4589)、[#4591](https://github.com/github/copilot-cli/issues/4591)。

- **富媒体支持**：PDF 上传分析 [#4583](https://github.com/github/copilot-cli/issues/4583)、开发资产图片生成 [#4581](https://github.com/github/copilot-cli/issues/4581) 等新能力开始被提出。

## 开发者关注点

- **MCP OAuth 认证是多发故障区**：#4490 关闭后，仍有 #4584、#4582 等新问题出现，涉及 RFC 8414、Entra ID scope、跨域 resource identifier 等多种原因，社区对回归和修复延迟不满。
- **400 错误影响核心工作流**：#1274 的 code review 场景和 #4572 的上下文压缩场景都会触发 400，说明请求构造与上下文管理仍有稳定性风险。
- **权限控制不够灵活**：交互模式只有“逐次批准”和“全部放行”两个极端，缺少中间态白名单机制。
- **Agent 行为可靠性**：Agent 口头答应但不执行 tool 调用，以及 MCP 握手超时无重试，都在削弱开发者对 agentic 工作流的信任。
- **Windows 平台体验问题**：VS Code 运行时插件安装/更新失败，是近期较典型的平台兼容性反馈。
- **Cloud 模式不成熟**：owner picker 卡死、重连崩溃、429 轮询等问题频繁，云开发模式仍需打磨。

---

以上为 2026-08-25 GitHub Copilot CLI 社区动态日报。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-08-25**


## 今日速览

今日社区焦点集中在**用量计费机制**的争议上：Issue #1994 高赞质疑官方的“按请求次数”宣传与实际“按 Token 消耗”扣费不符，引发 8 条讨论。代码安全方面，PR #2595 提出修复非 UTF-8 文件被 `StrReplaceFile` 静默损坏的严重问题。过去 24 小时无新版本发布。


## 版本发布

过去 24 小时内无新版本发布。


## 社区热点 Issues

**说明**：过去 24 小时内仅 1 个既有 Issue 获得更新，且无新增 Issue，以下为本期唯一热点。

### 1. kimiCode 用量计算有问题 / There is a problem with kimiCode usage calculation (#1994)
- **作者**: @wanghonghust
- **创建**: 2026-04-22 | **更新**: 2026-08-24
- **评论**: 8 | **👍**: 7
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/1994

**为什么重要**：
- **计费模型与宣传不一致**：用户指出实际扣费按 **Token 数**计算，而非官方宣传中隐含的 API 请求次数。该用户订阅会员后，仅 2 个任务就耗尽 2 小时额度，官方说明中“每 5 小时可支持约 300-1200 次请求”的说法与实际严重不符。
- **K2.6 思维链过长**：用户将矛头指向 K2.6 生成的思维链（CoT）过长，导致 Token 快速耗尽，大幅降低会员套餐的实际可用次数。
- **社区共鸣**：7 个 👍 说明不少用户对此有同感；8 条评论中社区正在争论“请求次数 vs Token 消耗”的合理性，以及对 UI 展示 & 用量明细透明化的诉求。


## 重要 PR 进展

**说明**：过去 24 小时内仅 1 个 PR 获得更新。

### 1. fix(StrReplaceFile): refuse to edit files that are not valid UTF-8 (#2595)
- **作者**: @shoemoney
- **创建**: 2026-08-06 | **更新**: 2026-08-24
- **评论**: 无 | **👍**: 0
- **链接**: https://github.com/MoonshotAI/kimi-cli/pull/2595
- **关联 Issue**: #2591

**功能/修复内容**：
- 当前 `StrReplaceFile` 实现使用 `errors="replace"` 解码整个文件 → 执行字符串替换 → 将完整字符串写回。
- 问题在于：文件中任意位置的**非 UTF-8 字节**（即使远离编辑区域）都会被替换为 `U+FFFD` 并写回，导致二进制文件或非 UTF-8 编码文件（如 GBK）被**静默破坏**。
- 修复后：工具将**拒绝编辑非有效 UTF-8 文件**，避免数据损坏，而非在用户无感知的情况下修改文件内容。

**重要性**：
- 这是典型的数据安全修复，直接关系到用户源码与资源文件的完整性，尤其对多编码环境下的中文开发者尤为重要。
- 虽然当前 👍 为 0，但该修复的价值在于“防患于未然”，可避免严重的文件损坏事故。


## 功能需求趋势

基于今日仅有的 1 条 Issue 与 1 条 PR 更新，提炼出以下社区关注方向：

- **计费透明度**：用户对“按 Token 计费”的机制理解成本较高，期望提供清晰的用量明细，以及更直观的“每次请求预估消耗”展示。
- **思维链（CoT）可配置**：针对 K2.6 思维链过长导致的 Token 消耗问题，社区需要“快速/简洁模式”、可调 CoT 长度、或按任务类型动态控制 Token 上限。
- **文件编码健壮性**：CLI 工具在编辑文件时必须能安全处理非 UTF-8 内容，这关系到工具在复杂项目中的可用性与信任度。


## 开发者关注点

- **Token 消耗过快，实际可用次数远低于预期**：2 小时配额仅支撑 2 次任务，严重冲击开发者的实际工作效率和订阅价值。
- **宣传与事实有落差**：官方关于“300-1200 次请求/5 小时”的说明存在误导，容易让用户误以为按次数计费，期待用更准确、透明的口径描述配额机制。
- **文件编辑安全不可妥协**：开发者不希望 CLI 在替换字符串时“殃及池鱼”——非 UTF-8 字节应在被明确拒绝或提示，而非被莫名替换为乱码。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 · 2026-08-25

## 今日速览

昨日发布 `v0.22.0-nightly.20260824.3a1f86d805` 与 `cua-driver-rs v0.20.0` 预编译二进制；社区围绕流式超时中断、MCP 重连"假成功"、Anthropic 流保护缺失等稳定性问题展开密集讨论，50 条活跃 Issue 中有 12 条于昨日新开。PR 侧核心进展集中在 Anthropic 流看门狗、HTTP MCP 恢复、多智能体循环检测与跨平台 CI 修复。

---

## 版本发布

### v0.22.0-nightly.20260824.3a1f86d805
- **fix(web-shell)**：从 overview panel 打开会话时正确传递 workspace cwd（PR [#9730](https://github.com/QwenLM/qwen-code/pull/9730)）
- 另有两个 gh-attach 资产上传流水线动作（`pr-9806-verification-assets`、`gh-attach-assets`），无功能性变更

### cua-driver-rs v0.20.0
Qwen CUA Driver 预编译二进制（vendored under `packages/cua-driver`）：
- **macOS**：codesigned + notarized 通用二进制及 `QwenCuaDriver.app`
- **Linux**：未签名（x86_64 + arm64，glibc 2.31 基线）
- **Windows**：未签名（x86_64 + arm64）
- 同一工作流同时发布 Node.js 版本

---

## 社区热点 Issues（10 个）

**1. [API Error: No stream activity for 120000ms after 19 chunks](https://github.com/QwenLM/qwen-code/issues/5975)**
12 条评论 · P2 · bug · 核心/集成/性能/延迟
自 v0.19.3 起频繁出现的流式中断问题：`Thought for 2s` 后无输出直至超时。评论数居首，是当前社区最集中的稳定性痛点，欢迎 PR。

**2. [refactor: core + cli 架构 Review — 12 项结构性问题清单](https://github.com/QwenLM/qwen-code/issues/4063)**
9 条评论 · in-progress · enhancement
对 `packages/core` 与 `packages/cli` 的全面架构审查，P0 级问题包括核心类型系统被 `@google/genai` 绑架——**136 个文件**直接 import 该包。是核心架构治理的重要讨论帖。

**3. [Bug: qwen mcp reconnect reports success but MCP tools remain unavailable](https://github.com/QwenLM/qwen-code/issues/9944)**
4 条评论 · P2 · bug · MCP
HTTP transport MCP 服务器重启后生成新 `mcp-session-id`，`qwen mcp reconnect --all` 报告成功但工具调用返回 `Tool not found`。直接影响 MCP 生态可用性，昨日新开。

**4. [design(core): make derived Config context ownership explicit](https://github.com/QwenLM/qwen-code/issues/8083)**
6 条评论 · P1 · enhancement · 核心架构
子代理、scoped memory agents、审批模式覆盖等多条生产路径依赖 `Object.create(base)` 原型委托派生 `Config`，状态所有权不明确。架构改进方向，已 in-progress。

**5. [The Anthropic wire is missing stream-safety protections the OpenAI wire already has](https://github.com/QwenLM/qwen-code/issues/9005)**
4 条评论 · P1 · bug · 内容生成
`anthropicContentGenerator` 缺少 OpenAI wire 已具备的空闲/生命周期看门狗，长时间无帧或持续 `thinking_delta` 低内容帧会导致流悬挂。与 #5975 同源，已有对应修复 PR #9945。

**6. [Migrate TUI rendering layer from ink to OpenTUI](https://github.com/QwenLM/qwen-code/issues/8662)**
4 条评论 · P3 · enhancement · UI/终端
当前基于 ink 7 + React 19 + 约 1037 行自定义 patch 的渲染层存在闪烁问题，且对鼠标支持不够，提议迁移至 OpenTUI。roadmap/terminal-ux 方向。

**7. [Artifact updatedAt stays stale; write_file intermediates linger as missing](https://github.com/QwenLM/qwen-code/issues/9927)**
4 条评论 · P2 · bug · 会话管理
Artifact 的 `updatedAt` 仅在注册字段变化时更新，内容更新不触发；且 `write_file` 中间状态残留在会话中。影响 WebShell 与桌面端内容同步准确性。

**8. [Hide skill commands from top-level slash completion](https://github.com/QwenLM/qwen-code/issues/9942)**
4 条评论 · P3 · feature-request · UI/命令
大量已安装 skill 使 `/` 补全菜单拥挤不堪，内置命令难以查找。社区建议 skill 命令不应自动出现在顶级补全中，需 discussion。

**9. [Team shutdown requests overload the teammate message channel and reject ordinary reports](https://github.com/QwenLM/qwen-code/issues/9510)**
3 条评论 · P2 · bug · 多智能体
扩展 Agent Team 会话中，teammate 的普通报告被误判为 shutdown 请求并被拒绝（`Only the team leader can request shutdowns`）。多智能体协作的关键消息通道问题，已 closed（有修复）。

**10. [bug(core): Kimi rejects built-in tool schemas with uniqueItems](https://github.com/QwenLM/qwen-code/issues/9865)**
2 条评论 · P1 · bug · 模型兼容性
`update_goal.evidenceRefs` 与 `todo_write.blockedBy` 内建 schema 中的 `uniqueItems: true` 导致 DashScope OpenAI 兼容端点对 `kimi-k3` 直接 HTTP 400。新模型适配的兼容性隐患。

---

## 重要 PR 进展（10 个）

**1. [fix(core): guard Anthropic streams with idle and lifetime watchdogs](https://github.com/QwenLM/qwen-code/pull/9945)**
将 OpenAI wire 的空闲超时 + 非重置生命周期上限接入 Anthropic 生成器，静默流或持续低内容帧将按错误中断。直接回应 #9005，是当前流稳定性的关键修复。

**2. [fix(mcp): recover restarted HTTP MCP servers in-session and in CLI](https://github.com/QwenLM/qwen-code/pull/9962)**
修复 HTTP（Streamable HTTP）MCP 服务器重启后工具不可用的四层缺陷——会话内失败调用自动修复连接、CLI 重连不再"假成功"，对应 #9944。

**3. [fix(core): make loop detection result-aware for task_list polls](https://github.com/QwenLM/qwen-code/pull/9492)**
对 `task_list` 这类有状态读工具，相同参数不代表相同结果（其他 teammate 可变更共享任务板），循环检测现按结果感知判断，避免多智能体协作中的误判。

**4. [fix: repair the Windows and macOS test lane failures](https://github.com/QwenLM/qwen-code/pull/9728)**
修复导致 Windows/macOS CI 红线的测试失败，涵盖产品修复、测试夹具修复与 CI harness 修复三部分，为恢复两个平台 lane（#9370）铺路。

**5. [feat(web-shell): unblock git update on dirty working tree](https://github.com/QwenLM/qwen-code/pull/9769)**
WebShell 的 "Update Project" 不再因未提交变更而死路：pull 受阻时提供冲突解决方案面板，而非单行错误提示。

**6. [feat: support provider-aware reasoning controls](https://github.com/QwenLM/qwen-code/pull/9590)**
为 DeepSeek V4、GLM 5.2、Kimi 提供 WebShell 推理控制——按文档路由匹配切换型、标准 effort 分层、强制思考三种模式，请求适配器相应调整。

**7. [feat(daemon

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*