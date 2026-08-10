# AI CLI 工具社区动态日报 2026-08-11

> 生成时间: 2026-08-10 22:36 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-08-11）

> **数据范围说明**：本报告基于 2026-08-11 各工具 GitHub 社区动态日报生成。其中 GitHub Copilot CLI、OpenCode 当日无有效数据披露，Gemini CLI 的 PR 数量未完整列出，以下分析均以可获得数据为准。

---

## 1. 生态全景

当前 AI CLI 工具正处于**密集迭代与能力深水区**并行的阶段：一方面 Qwen Code、OpenAI Codex 保持高频发版与大量 PR 合入，新功能快速落地；另一方面，各工具不约而同地暴露出**安全策略误报、子代理可靠性、跨平台稳定性**等"第二层"问题——基础能力已不再是瓶颈，精细化、可靠性、可配置性成为社区核心诉求。值得注意的共性信号是：**多智能体编排**（Claude Code、Gemini CLI、Qwen Code）与**跨会话上下文持久化**（Kimi Code、Gemini CLI）正成为下一代体验的竞争焦点，而 Windows/Wayland 等桌面端体验仍是全行业短板。整体来看，AI CLI 正从"单次会话的编码助手"向"可信赖的长期开发协作者"演进。

---

## 2. 各工具活跃度对比

| 工具 | 当日热点 Issues | 当日重要 PR | Release | 当日最突出信号 |
|---|---|---|---|---|
| **Claude Code** | 10 个（另有约 28 条误报 Issue 被关闭） | 4 条 | 0 | 安全过滤器误报引发社区集中反弹（205 👍 的 VS Code 功能请求居首） |
| **OpenAI Codex** | 10 个 | 10 条（含 9 条已合并） | 2 个 alpha | Windows 平台稳定性问题集中爆发（#20214 达 92 评论/81 👍） |
| **Gemini CLI** | 约 9+ 个（列表未完整） | 未完整披露（提及安全类、eval 工具链类 PR） | 1 个 nightly | 子代理"谎报 GOAL 成功"与挂起问题成讨论焦点 |
| **Qwen Code** | 10 个 | 10 条 | 1 个正式版（v0.21.9） | 多智能体 Fleet 架构进入密集实施阶段，同时大量渲染修复合入 |
| **Kimi Code CLI** | 1 个（#1283，31 评论） | 0 | 0 | Memory System 提案持续讨论近半年，跨会话记忆诉求强烈 |
| **GitHub Copilot CLI** | 数据未提供 | 数据未提供 | 数据未提供 | — |
| **OpenCode** | 数据未提供 | 数据未提供 | 数据未提供 | — |

从数据密度看，**Claude Code 与 OpenAI Codex 是社区讨论量最大的两个工具**；**Qwen Code 是当日唯一发布正式版且 PR 数量达两位数的工具**，处于明显的功能扩张期；**Gemini CLI 的问题聚焦度极高**，子代理成为绝对关键词；**Kimi Code 活跃度低，但唯一的热点 Issue 具有战略意义**。

---

## 3. 共同关注的功能方向

### 3.1 安全策略精准度与沙箱兼容性（涉及工具最多的议题）
- **Claude Code**：约 28 条安全误报 Issue，覆盖 CVE 自查、RustDesk 远程管理、阅读开源源码、甚至撰写误报反馈标题本身，均被 AUP 过滤器拦截。
- **OpenAI Codex**：沙箱安装破坏 AppData ACL（#15777）、apply_patch 在沙箱内失败（#30009）、Windows 沙箱级别与网络策略不一致（#37875）。
- **Gemini CLI**：出现 SSRF 修复、沙箱崩溃修复等高优先级安全类 PR。
- **核心诉求**：安全策略需要区分"防御性安全任务"与"恶意行为"，沙箱不能阻断正常开发工作流（如 `git clone` 导致 pip 安装失败）。

### 3.2 上下文窗口与跨会话记忆管理
- **Kimi Code**：#1283 提出完整的 Memory System，涵盖自动记忆（AI 维护项目笔记/偏好）与手动记忆（用户配置文件），评论 31 条，持续半年。
- **Claude Code**：#24726 要求禁用 VS Code 扩展自动附加文件/选区，防止上下文膨胀，获 205 👍。
- **OpenAI Codex**：#34619 要求恢复 GPT-5.6 Sol 的 372k 上下文窗口或提供 opt-in，获 18 👍——超长上下文是重度用户刚需。
- **Gemini CLI**：Auto Memory 系统出现重试风暴、脱敏不足等质量问题。

### 3.3 多智能体/子代理可靠性
- **Gemini CLI**：#22323 子代理在 MAX_TURNS 后误报 GOAL 成功；#21409 generalist 代理永久挂起（8 👍 为当日最高赞）。
- **Qwen Code**：Fleet 多智能体架构进入 Stage 1A/1B 实施，但 #8885 已暴露 rewind 索引错位等会话一致性问题。
- **OpenAI Codex**：#37563 重启后已关闭的子代理被恢复为 Working 状态。
- **核心诉求**：子代理的状态报告必须可信，"谎报成功"会直接破坏外部自动化流程。

### 3.4 桌面端与跨平台稳定性
- **OpenAI Codex**：Top 30 Issue 中近 1/3 与 Windows 相关，涵盖卡顿、WSL Git 识别失败、Computer Use 崩溃等。
- **Claude Code**：macOS Advisor 触发时 "No response from API"（95 👍）、Windows Intel GPU 崩溃。
- **Gemini CLI**：#21983 浏览器子代理在 Wayland 下直接失败。
- **Qwen Code**：macOS 终端窗口缩放导致滚动区重复打印（#8557），桌面端回归缺口修复（#8896）。

### 3.5 MCP 与生态集成
- **OpenAI Codex**：当日 10 条 PR 中过半与 MCP 相关——OAuth 凭据读取加速、表单输入支持、插件所有权暴露。
- **Qwen Code**：WebBridge 直接控制 Chrome 扩展，Kimi 与小米 MiMo 提供商接入。
- **Claude Code**：社区插件提交（entroly 上下文管理）与 security-guidance 模型引用更新。

---

## 4. 差异化定位分析

| 工具 | 功能侧重 | 目标用户 | 技术路线特征 |
|---|---|---|---|
| **Claude Code** | 全功能 IDE 集成、安全策略、代码审查 | 企业级开发者、安全敏感团队 | 大而全的成熟路线，社区体量大，当前主要矛盾是安全过滤器的"精准度"而非功能缺失；VS Code 扩展精细控制是用户最期待的方向 |
| **OpenAI Codex** | Windows 兼容、MCP 生态、Computer Use、模型灵活配置 | 微软生态开发者、通过云/桌面端协作的团队 | 快速补课路线：大量 PR 集中在 Windows 沙箱修复与 MCP 基础设施打磨；Rust 工具链 alpha 高频迭代（当日 2 个版本），engineering 气息强 |
| **Gemini CLI** | 子代理体系、Auto Memory、eval 基础设施 | 研究型/自动化工作流使用者 | 架构探索激进（零依赖 OS 沙箱、意图路由为 P2

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---

# Claude Code 社区动态日报（2026-08-11）

## 今日速览

昨日无新版本发布，社区焦点集中在两件事：一是 VS Code 扩展禁用"自动附加文件/选区"的功能请求持续发酵（205 👍 / 66 评论，高居榜首）；二是用户 @sworrl 批量提交的约 28 条安全策略误报 Issue 已陆续被标记为重复并关闭，但大量误报案例本身反映了安全过滤器对防御性安全任务的过度拦截问题，值得官方关注。

---

## 社区热点 Issues（10 个）

### 1. VS Code 扩展：增加禁用自动附加文件/选区的设置
- **Issue**: [#24726](https://github.com/anthropics/claude-code/issues/24726)
- **状态**: OPEN | **评论**: 66 | **👍**: 205
- **要点**: 用户希望 VS Code 扩展侧边栏不要自动将当前打开文件或选区附加到对话上下文。该请求自今年 2 月提出，至今仍有大量开发者跟进，评论区积累了丰富的使用场景讨论，是目前社区呼声最高的功能增强请求。

### 2. macOS 上触发 Advisor 时出现 "No response from API" 错误
- **Issue**: [#69238](https://github.com/anthropics/claude-code/issues/69238)
- **状态**: OPEN | **评论**: 61 | **👍**: 95
- **要点**: 使用 Sonnet 作为基础模型时，触发 Advisor（Opus 4.8）后 API 无响应，并反复重试（提示检查网络）。该问题影响 macOS + TUI 用户，复现路径清晰，评论中大量用户确认遇到相同问题，是当前最受关注的稳定性 Bug。

### 3. Claude Desktop MSIX 在 Intel 集成 GPU 上崩溃
- **Issue**: [#83028](https://github.com/anthropics/claude-code/issues/83028)
- **状态**: OPEN | **评论**: 4 | **👍**: 0
- **要点**: 浏览器窗格使用过程中，Windows 上 Intel 集成 GPU 环境下的 MSIX 包崩溃，可稳定复现且无绕过方案。属于较新的 Windows 端兼容性问题。

### 4. 远程执行沙箱阻止 git clone 导致 pip 安装失败
- **Issue**: [#71230](https://github.com/anthropics/claude-code/issues/71230)
- **状态**: CLOSED | **评论**: 3
- **要点**: Claude Code Web 的远程执行沙箱阻止了对 github.com 的 `git clone`，导致 `git+https://` 依赖的 pip install 失败。属于沙箱网络策略与开发工作流冲突的典型问题，影响使用远程沙箱模式安装 GitHub 依赖的开发者。

### 5. 会话恢复问候语被网络安全策略误拦截
- **Issue**: [#71123](https://github.com/anthropics/claude-code/issues/71123)
- **状态**: CLOSED | **评论**: 3
- **要点**: 在已授权的安全技术工作会话中，仅发送 "HELLO!?" 进行恢复续接即触发了 AUP 违规拦截。误报系列中的一个代表案例——安全术语的上下文误判已影响正常会话流程。

### 6. Cloud IAM 租户安全审计被误拦截
- **Issue**: [#71241](https://github.com/anthropics/claude-code/issues/71241)
- **状态**: CLOSED | **评论**: 3
- **要点**: 管理员对自有云身份租户进行防御性审计（枚举管理员角色、应用凭据、OAuth 授权），被网络安全过滤器判定为违规。防御性安全运维成为误报重灾区。

### 7. 设置 RustDesk 远程桌面会话被误判为网络安全风险
- **Issue**: [#71076](https://github.com/anthropics/claude-code/issues/71076)
- **状态**: CLOSED | **评论**: 3
- **要点**: 对自有受管端点建立远程桌面会话进行故障恢复，被安全分类器硬拦截并返回 API 错误，且"不允许模型评估请求"直接阻断。反映了分类器的二元判定方式对日常 IT 管理工作的副作用。

### 8. ClAudit 误报：阅读开源远程桌面工具源码被拦截
- **Issue**: [#71060](https://github.com/anthropics/claude-code/issues/71060)
- **状态**: CLOSED | **评论**: 3
- **要点**: 请求阅读并解释知名开源远程桌面应用的源代码，被网络安全过滤器以"模式匹配"方式拦截。纯软件工程任务因术语表触发拦截，误报面较广。

### 9. 起草 GitHub Issue 标题本身被网络安全策略拦截
- **Issue**: [#71070](https://github.com/anthropics/claude-code/issues/71070)
- **状态**: CLOSED | **评论**: 3
- **要点**: 用户为提交"网络安全误报"反馈而撰写 Issue 标题时，该标题再次被安全过滤器拦截，形成"反馈误报本身也是误报"的循环。该案例被社区认为是过滤器上下文理解局限性的典型写照。

### 10. CVE 与攻击面防御性自查被误拦截
- **Issue**: [#71229](https://github.com/anthropics/claude-code/issues/71229)
- **状态**: CLOSED | **评论**: 3
- **要点**: 在自身基础设施遭受攻击期间进行防御性 CVE 审计（盘点已知漏洞组件、生成修复清单）被安全策略阻止。误报已从"普通术语"延伸至"正当防御行为"，对安全运维场景造成实际干扰。

> 说明：@sworrl 在 6 月 25 日前后批量提交了约 28 条同类误报 Issue（#71056 ~ #71247），均为安全策略/ AUP 误拦截的重复报告。虽然多数已被标记为 duplicate 并关闭，但其数量集中反映了当前安全过滤器的误报问题在安全工程从业者中影响广泛。

---

## 重要 PR 进展（共 4 条）

由于数据源中近 24 小时活跃的 PR 共 4 条，以下全部列出：

### 1. `/code-review` 命令增加 GitHub/GitLab 自动检测与 GitLab 支持
- **PR**: [#34951](https://github.com/anthropics/claude-code/pull/34951)
- **状态**: OPEN | 更新于 2026-08-10
- **内容**: 为 `/code-review` 命令增加多平台支持，基于远程 URL 自动检测 GitHub 与 GitLab（含自托管实例），复用现有逻辑，消除平台分支重复代码。对应 Issue #26932。

### 2. 新增社区插件：entroly-context 预算感知上下文管理
- **PR**: [#85464](https://github.com/anthropics/claude-code/pull/85464)
- **状态**: CLOSED | 更新于 2026-08-10
- **内容**: 提交一个社区插件，当代码库超出上下文窗口时，基于 [Entroly](https://github.com/juyterman1000/entroly) 提供预算感知的上下文选择策略。该 PR 已关闭，作者未来可能调整后重新提交。

### 3. 文档：在 commit 命令文档中强制使用 Task 工具并补充模型元数据
- **PR**: [#9262](https://github.com/anthropics/claude-code/pull/9262)
- **状态**: CLOSED | 更新于 2026-08-10
- **内容**: 文档更新，将 `claude-3-5-haiku-latest` 模型信息补充到 commit 命令文档，并强调 commit 工作流中应使用 Task 工具以保证上下文隔离。该 PR 仅涉及文档变更，已于本周期关闭。

### 4. security-guidance 插件模型引用更新：Opus 4.7/Sonnet 4.6 → Opus 5/Sonnet 5
- **PR**: [#85409](https://github.com/anthropics/claude-code/pull/85409)
- **状态**: OPEN | 更新于 2026-08-10
- **内容**: `security-guidance` 插件 README 与 hook 代码中仍引用已过时的模型版本（默认审查模型 Opus 4.7、回退模型 Sonnet 4.6）。该 PR 将默认模型统一更新为当前最新的 Opus 5 / Sonnet 5，涉及 `llm.py` 中 `SECURITY_REVIEW_MODEL` 等相关配置。

---

## 功能需求趋势

从当前活跃 Issues 中可以提炼出以下社区关注方向：

1. **IDE 集成可控性**（#24726）：开发者希望更精细地控制 VS Code 扩展的上下文附加行为，避免自动附加带来的令牌浪费和上下文污染。
2. **安全策略精准度**：大量误报 Issue 表明，当前安全过滤器对"防御性安全任务""远程工具管理"等正常操作存在过度拦截。社区期待更精准的分类逻辑或更宽松的白名单机制。
3. **跨平台稳定性**：macOS 上 Advisor 触发时的无响应（#69238）与 Windows Intel GPU 崩溃（#83028）说明多平台稳定性仍有待加强。
4. **远程沙箱网络能力**：沙箱阻止 `git clone` 的案例（#71230）暴露了远程沙箱模式对 GitHub 依赖安装的限制，开发者希望沙箱策略能更好地兼容常见开发工作流。
5. **新模型支持同步**：PR #85409 显示社区插件仍在跟进 Opus 5 / Sonnet 5 的迁移，官方模型更新后生态需要及时同步。

---

## 开发者关注点

- **安全过滤器误报是当前最大痛点**：约 28 条误报 Issue 覆盖了安全审计、CVE 自查、远程桌面管理、会话恢复问候语、甚至"撰写误报反馈标题"等场景。误报不仅打断工作流，还会产生 API 硬错误强制阻断，用户无法通过调整提示绕行，需申请豁免才能继续——这对合法安全从业者造成了实质性打扰。
- **上下文自动附加行为有待优化**：VS Code 扩展的自动附加设计在大型项目中会导致上下文膨胀，开发者希望获得明确的开关控制。
- **Sandbox 与日常开发工具的兼容性**：远程沙箱对 `git clone` 的限制直接导致依赖安装失败，沙箱策略需与 pip、npm 等生态的开发习惯对齐。
- **错误恢复体验不佳**：macOS 上 API 无响应后仅提示"检查网络"并进入长时间重试（2m 25s），缺乏诊断信息，用户难以自行排查。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-11

## 今日速览

Windows 平台稳定性问题仍是社区最集中的痛点，#20214（Windows 应用卡顿）已累计 92 条评论和 81 个赞，成为近期影响面最大的 Issue。PR 方面主要围绕 Windows 沙箱修复、MCP OAuth 性能优化与 apply_patch 输入校验展开，多个修复直接对应社区高频反馈。版本层面今日发布了两个 Rust alpha 迭代版（0.148.0-alpha.6 / 0.147.0-alpha.6.6），无重大功能变更。


## 版本发布

过去 24 小时发布了两个预发布版本，均在 Rust 工具链迭代线上：

- **rust-v0.148.0-alpha.6**（0.148.0-alpha.6）：最新 alpha 版发布，无额外变更说明。
- **rust-v0.147.0-alpha.6.6**（0.147.0-alpha.6.6）：0.147 系列的小版本迭代。

链接：https://github.com/openai/codex/releases


## 社区热点 Issues

**① Codex App 在 Windows 11 Pro 上频繁卡顿/停滞**（#20214，92 评论 / 81 👍）  
反映 App 在系统资源充足（Ryzen 5 5600 / 32GB RAM）的情况下仍频繁卡顿。自 4 月底创建以来持续获得关注，是社区讨论度最高的 Windows 性能问题。  
https://github.com/openai/codex/issues/20214

**② apply_patch 在 Windows 沙箱环境中失败**（#30009，33 评论 / 11 👍）  
Windows 下文件编辑通过 apply_patch 调用时报沙箱相关错误，涉及工具调用链路的平台兼容性，当前仍处于开放状态。  
https://github.com/openai/codex/issues/30009

**③ SQLite WAL 写入过多，TRACE 日志忽略 RUST_LOG 配置**（#17320，30 评论 / 39 👍）  
流式输出期间产生大量 SQLite WAL 写入，理想情况下应通过 RUST_LOG 控制跟踪日志但未生效。问题指向日志系统配置不当造成的性能开销。  
https://github.com/openai/codex/issues/17320

**④ Codex 沙箱安装破坏 AppData 的 ACL 权限**（#15777，27 评论 / 2 👍）  
Windows 10 上安装 Codex 沙箱导致 AppData 访问控制列表（ACL）损坏，属于安装器/沙箱的权限管理缺陷。  
https://github.com/openai/codex/issues/15777

**⑤ Windows + WSL 仓库被误判为非 Git 仓库，提示 Git 不可用**（#35119，19 评论 / 16 👍）  
26.721.3404 版本将 WSL ext4 上的有效仓库识别为“非 Git”，上一正常版本为 26.715.10079，应为回归性 bug。  
https://github.com/openai/codex/issues/35119

**⑥ Windows Computer Use 复用过期 node_repl 执行上下文**（#37013，17 评论 / 4 👍）  
`@oai/sky` 调用在首次 JS 执行完成后，下一次调用仍复用同一传输通道，导致执行失败。这是 Computer Use 在 Windows 的一个确定性 bug。  
https://github.com/openai/codex/issues/37013

**⑦ Windows Computer Use 窗口发现失败，报 0x80070003**（#37383，13 评论 / 4 👍）  
应用/窗口发现阶段直接报“路径不存在”错误，阻塞整个 Computer Use 流程。  
https://github.com/openai/codex/issues/37383

**⑧ Codex Cloud 停止识别 Git remote，只引用 work 工作区**（#12498，11 评论 / 7 👍）  
云端会话在正常使用中突然丢失仓库 remote 配置，行为不可预测且无手动恢复手段。  
https://github.com/openai/codex/issues/12498

**⑨ 重启后已关闭的子代理被恢复为 Working 状态**（#37563，9 评论 / 4 👍）  
Codex Desktop 26.803.41515 在启动时将已完成/已中止的子代理回放为“Working”，持久化状态与实际不符，干扰会话恢复和 UI 展示。  
https://github.com/openai/codex/issues/37563

**⑩ 恢复 GPT-5.6 Sol 的 372k Codex 上下文窗口或提供 opt-in 设置**（#34619，5 评论 / 18 👍）  
虽然评论数不高，但 18 个 👍 说明该功能诉求在社区中有显著共识，属于高频需求。  
https://github.com/openai/codex/issues/34619


## 重要 PR 进展

**① 拒绝 apply_patch 中的重复解析路径**（#37867，已合并）  
如果补丁中多个操作解析到同一文件（如 `duplicate.txt` 与 `./duplicate.txt`），将直接拒绝。这是对 Windows apply_patch 相关问题（#30009 等）的输入校验加固。  
https://github.com/openai/codex/pull/37867

**② 忽略 Windows 上的 Unix 套接字代理设置**（#37889，已合并）  
Unix 套接字代理权限仅适用于 macOS，但此前 Windows 配置了该设置会把代理监听器错误地限制在 loopback 并发警告。  
https://github.com/openai/codex/pull/37889

**③ 遵守已配置的 Windows 沙箱级别管理网络**（#37875，已合并）  
托管网络此前会隐式选择提权的 Windows 沙箱后端，即使沙箱配置的是受限 token。现在完全由 `WindowsSandboxLevel` 决定后端选择。

**④ 加速 MCP OAuth 凭据读取**（#37860，已合并）  
运行时刷新 MCP 连接身份时，不再因其他进程持有 OAuth 凭据存储锁而阻塞异步执行器，改为无等待探测并保留最近一次匹配快照。  
https://github.com/openai/codex/pull/37860

**⑤ 支持 MCP 表单输入（full-access 用户线程）**（#37864，已合并）  
即使工具权限被自动批准，标准 MCP 表单仍可能需要用户输入。该 PR 识别 `openai/standard-form-input` 扩展并显示非审批类型的表单提示。  
https://github.com/openai/codex/pull/37864

**⑥ 拦截 exec 审批统一走共享 review 流程**（#37851，已合并）  
zsh fork 拦截到的 Unix `execve` 审批现在会进入共享审批管线，包括权限钩子、Guardian review、用户提示和遥测，同时解析活动 turn 与其 auto-review 设置。  
https://github.com/openai/codex/pull/37851

**⑦ MCP OAuth 凭据竞争回归测试**（#37866，已合并）  
覆盖文件/密钥存储被锁时的非阻塞凭据探测场景，包括保留匹配快照、锁释放后恢复等，延伸了 streamable HTTP OAuth round trip 测试。  
https://github.com/openai/codex/pull/37866

**⑧ 从响应元数据读取安全缓冲（safety buffering）**（#37882，已合并）  
解析类型化的 `response.metadata` SSE 事件中的安全缓冲数据；保留现有顶层 `safety_buffering` 字段作为权威值（即使为 null 或格式错误）。  
https://github.com/openai/codex/pull/37882

**⑨ 解析 Code Mode 工具 schema 中的本地 MCP $ref 引用**（#31901，开放中）  
支持在渲染 TypeScript 工具声明时解析本地 JSON Pointer `$ref`，包括 `#/$defs/...` 和 `#/definitions/...`，并保留兄弟描述信息。  
https://github.com/openai/codex/pull/31901

**⑩ 暴露 MCP 服务器状态中的插件所有权**（#37850，已合并）  
`mcpServerStatus/list` 结果新增 `pluginId` 字段，可区分插件贡献的 MCP 服务器与其他来源，协议 schema、TypeScript 绑定同步更新。  
https://github.com/openai/codex/pull/37850

此外还有几项值得留意的内部重构：`copyberry` 机器人批量提交了持久化历史类型抽取（#37871）、Goal token 预算配置化（#37878）、Statsig 指标排除（#37874）。`hefuc-oai` 的 5/5 系列 PR（#31286-#31315）完成了 legacy enterprise-managed bundle 通道的迁移清理。


## 功能需求趋势

从今日活跃 Issue 可以提炼出以下社区最关注的功能方向：

- **Windows 平台体验修复**：Top 30 Issue 中近 1/3 与 Windows 相关，涵盖 WSL 仓库识别、沙箱 ACL、网络代理、Computer Use 稳定性等，说明 Windows 已是 Codex 的重要使用平台，但体验仍不够成熟。
- **Computer Use 功能稳定性**：Windows 端连续出现 node_repl 上下文复用、应用/窗口发现失败等多个阻断性问题，且影响 Pro 订阅用户。
- **上下文窗口与模型能力配置**：#34619 要求恢复 GPT-5.6 Sol 的 372k 上下文窗口或提供 opt-in 开关，表明超长上下文是重度用户的核心诉求。
- **MCP 集成体验**：大量 PR 集中在 MCP OAuth 读取性能、表单输入支持、插件所有权暴露，MCP 相关功能正在快速迭代中。
- **性能与资源占用**：SQLite WAL 写入、DWM 句柄累积、Node 进程内存膨胀等性能类 Issue 反复出现，资源效率是普遍关注点。
- **子代理与会话状态管理**：子代理在重启后状态错误、嵌套 exec 会话“假完成”等状态一致性问题开始进入社区视野。


## 开发者关注点

- **Windows 稳定性是最集中的痛点**：#20214（App 卡顿，81 👍）、#35119（WSL Git 识别，16 👍）、#30009（apply_patch 沙箱失败，11 👍）均指向 Windows 用户的实际体验问题，且多个问题在 Windows 10/11 不同版本上都有复现。
- **沙箱相关权限问题反复出现**：安装时破坏 ACL、沙箱级别与网络策略不一致、apply_patch 在沙箱内失败等，涉及安装器、CLI、App 三层。
- **高资源消耗与长期运行的可靠性**：SQLite 频繁写入、主进程 CPU 100% 不释放、海量 Node 进程耗尽内存等，说明长期会话场景下仍有严重资源管理缺陷。
- **上下文窗口被缩减引发不满**：GPT-5.6 Sol 的 372k 上下文窗口被移除，用户明确要求恢复或提供配置项，这属于功能回退引发的社区反弹。
- **状态一致性问题呈上升趋势**：子代理恢复状态错误、活动线程排序错乱、嵌套会话结束后模型误报完成等，说明桌面端的持久化与状态同步仍不够可靠。
- **连接器/MCP 认证流程存在缺陷**：Linear 连接器授权后循环重认证、MCP 凭据锁竞争造成阻塞等问题，直接影响自动化工作流的使用。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-11

## 今日速览

昨日仅发布一个自动化 nightly 版本（v0.56.0-nightly.20260810），无重大功能更新。社区讨论集中在**子代理可靠性**（误报成功、挂起、绕过权限）与**Auto Memory 系统**的一批质量问题（重试风暴、脱敏不足）上，安全类 PR（SSRF 修复、沙箱崩溃修复）有较高优先级。此外，eval 工具链的两项增强 PR 值得关注，表明官方正在强化评估基础设施。

## 版本发布

- **[v0.56.0-nightly.20260810.gcf22ac7e8](https://github.com/google-gemini/gemini-cli/releases/tag/v0.56.0-nightly.20260810.gcf22ac7e8)**：常规自动化 nightly 构建，无独立变更说明，完整 diff 见 [Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260809.gcf22ac7e8...v0.56.0-nightly.20260810.gcf22ac7e8)（含当天合并的部分依赖与修复 PR，详见下文说明）。

## 社区热点 Issues

1. **[#22323 Subagent 在 MAX_TURNS 后被误报为 GOAL 成功](https://github.com/google-gemini/gemini-cli/issues/22323)** [p1/bug] | 12 评论
  `codebase_investigator` 子代理明明已触发最大轮次中断，却向外报告 `Termination Reason: "GOAL"` 和 `status: "success"`，会误导外部自动化流程。评论数居首，社区对"子代理谎报成功"问题反馈强烈。
2. **[#21409 Generalist 代理无限挂起](https://github.com/google-gemini/gemini-cli/issues/21409)** [p1/bug] | 8 评论、8 👍（最高赞）
  用户表示只要委托给 generalist 代理就会永久挂起（建文件夹这类简单任务也能等 1 小时），唯一规避手段是提示词禁止委派。影响面大，呼声最高。
3. **[#25166 Shell 命令执行完成后卡在 "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)** [p1/bug] | 4 评论、3 👍
  简单的 CLI 命令完成后界面仍显示挂起状态，频繁复现且非交互式命令也会触发，直接影响日常使用体验。
4. **[#21983 浏览器子代理在 Wayland 下失败](https://github.com/google-gemini/gemini-cli/issues/21983)** [p1/bug] | 4 评论、1 👍
  Linux Wayland 环境下 browser subagent 启动即失败（Termination Reason: GOAL，但实际未完成任何操作），Linux 桌面用户受影响。
5. **[#22186 get-shit-done 输出钩子在收尾时崩溃](https://github.com/google-gemini/gemini-cli/issues/22186)** [p1/bug] | 3 评论
  输出摘要打印阶段反复导致 CLI 崩溃，属于阻断性稳定性问题。
6. **[#24353 组件级评估体系（EPIC）](https://github.com/google-gemini/gemini-cli/issues/24353)** [p1] | 7 评论
  在已有 76 个行为评估测试、覆盖 6 个模型的基础上，推进更细粒度的组件级评估。反映官方对可评测性的投入方向。
7. **[#19873 零依赖 OS 沙箱 + 执行后意图路由](https://github.com/google-gemini/gemini-cli/issues/19873)** [p2/enhancement] | 8 评论
  主张利用 Gemini 3 模型"原生 bash 倾向"，在不牺牲安全/UX 的前提下让模型自由使用 POSIX 工具链。代表社区对 Agent 能力上限的探索方向。
8. **[#22745 AST 感知的文件读取/搜索/代码库映射评估（EPIC）](https://github.com/google-gemini/gemini-cli/issues/22745)** [p2] | 7 评论
  调研是否值得引入 AST 感知工具来减少 token 噪声、精确读取方法边界。若落地可显著改善大仓库场景效率。
9. **[#26522 Auto Memory

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-08-

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

> **数据说明**：本次日报基于采集窗口内（2026-08-10 至 2026-08-11）GitHub 数据生成，期间活跃数据量较少：Release 0 个、PR 更新 0 个、Issue 更新 1 个。为保证信息真实，下文仅列出实际可查证的内容。

---

## 1. 今日速览

过去 24 小时内，Kimi Code CLI 无新版本发布，也无 PR 变动；社区讨论集中在 Issue **#1283（Memory System）**——该提案已持续讨论近半年、累计 31 条评论，是目前最受关注的功能诉求。它反映了开发者对**跨会话持久化上下文**的强烈需求，值得官方关注。

## 2. 社区热点 Issues

> 说明：采集窗口内仅 1 个 Issue 发生更新，无法凑足 10 个，故只列出该议题。

### #1283 [OPEN] Feature Request: Memory System - Persistent context across sessions
- **作者**：@CatKang
- **创建**：2026-02-27 | **更新**：2026-08-10 | **评论数**：31 | 👍：0
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/1283
- **核心内容**：提议为 Kimi Code CLI 实现一套完整的**记忆系统（Memory System）**，支持跨会话保留上下文，包括：
  - **自动记忆（Automatic Memory）**：由 AI 管理维护的项目笔记、项目模式、用户偏好；
  - **手动记忆（Manual Memory）**：用户自定义的指令与规则（例如通过配置文件持久化）。
- **为什么重要**：该 Issue 从 2 月创建至今活跃近半年，评论达 31 条，说明“会话隔离/上下文丢失”是大量用户在长周期开发中的真实痛点。能持久记住项目约定、编码规范与个人偏好，将显著减少重复上下文注入，提升 CLI 作为日常开发助手的实用性。
- **社区反应**：讨论热度高，但 👍 数为 0，说明关注者以“深度用户”为主（更倾向评论交流而非投票）；建议后续跟踪官方是否有设计文档或 roadmap 回应。

## 3. 重要 PR 进展

过去 24 小时内**无 PR 更新**，暂无进展可汇报。

## 4. 功能需求趋势

> 说明：由于采集样本仅 1 个 Issue，以下趋势为**有限样本下的初步判断**，建议扩大时间窗口后做更全面分析。

- **持久化记忆 / 上下文管理**：以 #1283 为代表，社区最核心的诉求是让 CLI 具备跨会话记忆能力，覆盖**项目模式、用户偏好、历史决策**的长期保存。这表明当前工具在“单次会话内强、跨会话弱”的使用体验上存在明显短板。
- 其他常见趋势（如 IDE 集成、新模型支持、性能优化等）在本次采样中未出现，需更多数据验证。

## 5. 开发者关注点

- **跨会话连续性不足**：开发者需要反复向 CLI 描述项目背景、编码规范与偏好，缺乏记忆导致上下文断裂，这是当前最集中的痛点。
- **自动与手动记忆的平衡**：用户既希望 AI 能主动沉淀笔记（自动记忆），又要求保留手动定义指令的控制权（手动记忆），反映出社区对“AI 自主性”与“用户可控性”并重的期望。
- 由于数据量有限，上述结论主要源自 #1283 的讨论；若需提取更完整的开发者痛点清单，建议结合更长周期（如近 30 天）的 Issues 与 PR 做综合聚类分析。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-11

## 今日速览

**v0.21.9 正式发布**，新增 Qoder 插件原生支持（可从目录/压缩包/Git 仓库/URL/npm 安装），并开启 Local Control 二维码配对功能。社区侧，多智能体 Fleet 架构进入密集实施阶段（Stage 1A/1B 同步推进），同时大量终端渲染与桌面端回归问题的修复正在合入。

---

## 版本发布

### v0.21.9
- **核心新功能**：支持从目录、压缩包、Git 仓库、URL 及 npm 包安装 Qoder 插件，并自动加载系统提示词（[#8661](https://github.com/QwenLM/qwen-code/pull/8661)）
- **Local Control**：新增二维码配对方式，简化局域网设备连接
- 另含 0.21.8-nightly 分支的多项修复与 CI 改进

---

## 社区热点 Issues

### 1. [#8124](https://github.com/QwenLM/qwen-code/issues/8124) — 启动横幅首次渲染丢失顶部几行（P2/UI）
- **说明**：TUI 启动横幅（ASCII logo + 版本/Provider 信息）首次绘制时偶尔缺少顶部 ~3 行，与待处理的 provider 更新存在相关性。
- **关注度**：10 条评论，跨 Windows/渲染链路，属用户可见度较高的老问题（创建于 7/30，至今未闭环）。

### 2. [#8718](https://github.com/QwenLM/qwen-code/issues/8718) — RFC：多个独立 Qwen 会话的原生协调机制（P2/多智能体）
- **说明**：提出实验性的多会话协调路径——leader 可在保持交互的同时派发 2-3 个 worker，观察运行状态并收集结构化结果。这是 Fleet 架构的纲领性 issue。
- **关注度**：8 条评论，roadmap 标注 multi-agent 与 background-automation，社区讨论活跃。

### 3. [#8557](https://github.com/QwenLM/qwen-code/issues/8557) — 终端窗口缩小导致滚动区重复打印（P3/UI/macOS）
- **说明**：macOS + Warp 下缩小终端宽度时，已打印的 transcript 块被重复渲染进 scrollback，内容重复堆叠。
- **关注度**：8 条评论，已拆分出多个子问题（见 #8849、#8831），是当前渲染修复的重点战场。

### 4. [#8863](https://github.com/QwenLM/qwen-code/issues/8863) — Provider 更新静默改写 model.name 与 baseUrl（P1/严重回归）
- **说明**：选择 “Update all” 后，若当前模型属于其他 provider（如自建代理），`settings.json` 中的 `model.name` 会被换成内置列表第一个模型，`model.baseUrl` 被清空——#5819 回归。
- **关注度**：P1 级别，直接影响用户模型配置安全，2 条评论但已关闭（修复已合入）。

### 5. [#8885](https://github.com/QwenLM/qwen-code/issues/8885) — rewind 索引与自动 user-role 历史条目错位（P1/会话管理）
- **说明**：PR #8838 暴露了模型侧历史（含 cron/后台通知/停止续写等自动条目）与 ChatRecordingService 轮次边界之间的索引不匹配，可能导致回退（rewind）行为错乱。
- **关注度**：P1 高优，daemon 与会话管理核心区域，3 条评论持续跟进。

### 6. [#8841](https://github.com/QwenLM/qwen-code/issues/8841) — 受监督的 teammate 运行时（Fleet Stage 1B，P2）
- **说明**：Fleet 架构的 MVP 阶段，将 in-process 预览升级为完整舰队运行时，依赖 Stage 1A（#8840）。
- **关注度**：roadmap/multi-agent 的核心环节，与 #8718、#8840 构成完整实施路径。

### 7. [#8871](https://github.com/QwenLM/qwen-code/issues/8871) — ACP 子进程报 “Unknown argument: acp”（P2/CLI）
- **说明**：`qwen serve --http-bridge=true` 主进程以 `--acp` 参数派生子进程，但子进程无法解析该参数，导致 Token 认证失败（401）。
- **关注度**：4 条评论，直接阻断 ACP 模式使用，需紧急修复。

### 8. [#8888](https://github.com/QwenLM/qwen-code/issues/8888) — Autofix 推送取消 in-progress review-pr 形成死循环（P2/CI）
- **说明**：在机器人作者 PR 上，autofix 工作流与 review-pr 工作流互相触发取消，形成自我强化的循环。
- **关注度**：3 条评论，社区开发者 yiliang114 报告，属 CI 基础设施稳定性问题。

### 9. [#8837](https://github.com/QwenLM/qwen-code/issues/8837) — ACP 自动计划任务未出现在恢复的 transcript 中（P2/会话恢复）
- **说明**：会话冷启动后，从 transcript 恢复时调度任务提示词丢失，虽然实时消息与 assistant 结果均已持久化。
- **关注度**：与 #8885 同源相关，3 条评论，直接影响后台自动化场景的可恢复性。

### 10. [#8898](https://github.com/QwenLM/qwen-code/issues/8898) — API 错误：历史中出现重复工具调用（P2）
- **说明**：持续提示 “Repetitive tool calls detected”，相同 tool call 跨多轮重复触发，阻碍会话继续。
- **关注度**：3 条评论，已关闭（标记 need-information），但影响实际对话体验，值得持续观察。

---

## 重要 PR 进展

### 1. [#8896](https://github.com/QwenLM/qwen-code/pull/8896) — 修复 Desktop 0.1.1 回归缺口
- **内容**：修复三个桌面端回归：按住录音释放时捕获中断（React 未提交中间状态）、SSE 正常结束时误报重连错误、macOS 发布构建配置恢复。

### 2. [#8838](https://github.com/QwenLM/qwen-code/pull/8838) — 持久化计划执行的 cron 提示词
- **内容**：自动触发的计划任务现通过既有 cron-message 契约在模型轮次前写入会话记录，保持与实时 ACP 回显一致的文本。修复 #8837 的根因。

### 3. [#8882](https://github.com/QwenLM/qwen-code/pull/8882) — 跨会话切换事务化（WebUI）
- **内容**：现代 WebUI 的 load/resume 切换变为事务性——目标会话在隔离的 staging store 中完整恢复后才成为可见 owner，避免半加载状态污染当前会话。

### 4. [#8831](https://github.com/QwenLM/qwen-code/pull/8831) — 消除 banner 重复与 resize/wake 拖拽闪烁
- **内容**：修复 #8557 系列渲染问题：宽度缩小时旧宽度的行数导致 reflow 后顶部 banner 被孤立，后续每帧重绘不断堆叠副本。现已在宽度变化时正确清屏。

### 5. [#8707](https://github.com/QwenLM/qwen-code/pull/8707) — Qwen WebBridge：浏览器直接控制
- **内容**：从 `qwen serve` 直接控制 Qwen Chrome 扩展与真实 Chromium 配置，实现 Kimi WebBridge 兼容的 `/command` 与 `/status` 端点，覆盖 17 种动作面。

### 6. [#8728](https://github.com/QwenLM/qwen-code/pull/8728) — 实时会话注册表与 `qwen sessions ps`
- **内容**：每个运行中的交互会话在 `~/.qwen/sessions/<pid>.json` 登记，退出时清理。不改变会话行为，为后续进程管理打基础（#8724 第一步）。

### 7. [#8848](https://github.com/QwenLM/qwen-code/pull/8848) — Web Shell Channel 策略与工作区管理重构
- **内容**：为每个可管理适配器暴露共享的私信、群访问、会话路由与工作区所有权控制；支持全局选择 sender/group 策略、管理 allowlist，并统一连接状态展示。对应 #8845。

### 8. [#8874](https://github.com/QwenLM/qwen-code/pull/8874) — Web Shell 工作区文件上传
- **内容**：Composer 支持拖拽上传，文件在 `@` 面板中可选择 “Upload file” 入口；支持顺序上传、进度显示、取消、冲突自动重命名及内联预览。

### 9. [#8866](https://github.com/QwenLM/qwen-code/pull/8866) — 桌面端支持企业局域网地址
- **内容**：允许 Desktop Local Control 使用 OS 选定的物理接口默认路由（即使企业网络分配非 RFC1918 地址），入站连接仍限制在所选接口的子网内。

### 10. [#8368](https://github.com/QwenLM/qwen-code/pull/8368) — 新增 Kimi 与小米 MiMo 提供商
- **内容**：`/auth` 中新增第三方 provider 预设——Kimi 支持 Coding Plan、API Key（中国）、API Key（国际）三种接入方式；小米 MiMo 支持按量付费与中国/新加坡等区域 endpoint。

---

## 功能需求趋势

1. **多智能体 Fleet 架构快速推进**：`#8718`（RFC）、`#8840`（Stage 1A）、`#8841`（Stage 1B）、`#8843`（Stage 3）同批创建并互相依赖，显示 Qwen Code 正系统化构建“leader 调度多个 worker”的原生多会话能力，覆盖契约定义、进程生命周期、终端 attach 与清理。

2. **Web Shell 能力大幅扩展**：Channel 访问策略重构（#8845/#8848）、Git diff 与分支切换（#8467）、工作区文件上传（#8874）、SSE 重连体验优化（#8887）——Web 端正从“聊天界面”走向完整开发工作台。

3. **桌面端与 Local Control 生态补全**：企业 LAN 地址支持（#8866）、回归修复（#8896）、二维码配对（v0.21.9），Local Control 在真实企业网络环境中的可用性成重点。

4. **Provider 配置安全与弹性**：内置 provider 更新覆盖用户自定义模型（#8863 已修复）、更新提示重复出现（#8504），社区对“配置不被静默改写”有强烈诉求。

5. **CI/自动化基础设施稳定性**：Autofix 与 review-pr 互相取消（#8888）、CI E2E 多次失败（#8847、#8870），社区开始关注机器人维护链路的自愈能力。

---

## 开发者关注点

- **终端渲染正确性**：banner 首次绘制缺失（#8124）、缩放闪烁（#8557/#8831）、web 终端撕裂（#8659）、输入框偏移（#8849）——TUI 基础体验仍是高频反馈区。
- **配置与数据安全**：provider 更新改写模型配置（#8863）、`.env` 从非信任上级目录加载（#8643）——信任边界与配置持久化最受关注。
- **会话恢复可靠性**：ACL 计划任务缺失（#8837）、rewind 索引错位（#8885）、恢复超时保护（#8678）——长时间运行与后台自动化的用户基数在增长，对恢复一致性提出了更高要求。
- **日志无界增长**：OpenAI API 日志两个月积累 ~95GB/34 万文件（#8860），无轮转无保留期，生产环境长时间运行存在磁盘风险。
- **CLI 细节打磨**：`--approval-mode`/`--auth-type` 被接受但不出现在 `--help`（#8897）；`/clear` 被后台任务阻塞时提示语无法指导用户行动（#8741）——开发者对命令行的自我描述性和可操作性有较高期待。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*