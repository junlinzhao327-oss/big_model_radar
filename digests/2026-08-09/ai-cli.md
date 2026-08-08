# AI CLI 工具社区动态日报 2026-08-09

> 生成时间: 2026-08-08 22:51 UTC | 覆盖工具: 7 个

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

## AI CLI 工具横向对比分析报告（2026-08-09）

### 1. 生态全景

当前 AI CLI 工具已从"可用"进入"信得过、用得稳"的竞争阶段：头部工具（Claude Code、GitHub Copilot CLI）保持高频版本迭代，社区反馈的核心矛盾由功能不足转向稳定性、成本透明度和跨平台一致性；开源工具（OpenCode、Kimi Code）正在通过差异化功能（插件体系、记忆系统、本地模型）寻求突破。MCP 生态的爆发式增长同时带来了资源失控、配置失效、认证失败等系统性风险，成为所有工具共同面临的成长阵痛。整体来看，市场呈现"功能同质化与场景细分并存"的态势。

---

### 2. 各工具活跃度对比

| 工具 | 活跃 Issues（当日） | 重要 PR | Release 情况 | 备注 |
|---|---|---|---|---|
| **Claude Code** | 10 条（含 Top10 全量） | 未提及 | **v2.1.225、v2.1.226**，新增网关限额提示与工作区信任机制 | 版本迭代最频繁 |
| **GitHub Copilot CLI** | 10 条（含 Top10 全量） | 无新增 | **v1.0.79-9**，仅改进 `/sandbox` 配置提示 | 补丁型小步快跑 |
| **OpenCode** | 10 条（另有当日 4 个同类 bug 集中爆发） | **8 个** | 无新版本 | 社区活跃度最高 |
| **Kimi Code** | 2 条（全量） | 无 | 无 | 社区体量较小 |
| **OpenAI Codex** | 无数据 | 无数据 | 无数据 | 摘要未收录 |
| **Gemini CLI** | 无数据 | 无数据 | 无数据 | 摘要未收录 |
| **Qwen Code** | 无数据 | 无数据 | 无数据 | 摘要未收录 |

---

### 3. 共同关注的功能方向

**① 非侵入式协作与消息队列**
Claude Code 最热需求（#50246，184👍）——在任务执行期间排队追加指令而非打断当前工作。这反映出长时间运行 agent 任务已成为常态，用户迫切需要"旁路沟通"能力。

**② 远程控制与跨设备接管**
Claude Code #29006（119👍）希望在 Desktop 端控制 CLI 会话；Copilot CLI #4409 则暴露了远程控制开关静默失效问题。远程/无头工作流正在从"极客偏好"变为"标准诉求"。

**③ 会话状态持久化与模型一致性**
Copilot CLI #4397：`/resume` 后模型被重置；Kimi Code #1283（25 评论）：跨会话记忆系统；Claude Code #60093：模型被静默切换导致 $1,050 超额收费——用户对"会话是可靠上下文载体"的信任正在被动摇。

**④ MCP 生态稳定性**
Claude Code 遭遇 MCP 服务器内存失控致 macOS 内核崩溃（#64366）、VS Code 集成不加载 MCP（#19054）；OpenCode 插件静默失效导致 MCP 与 hook 消失（#41234）；Copilot CLI 企业版 MCP 认证失败（#4408）。MCP 已从"加分项"变成"必须兜底的基础设施"。

**⑤ 配置项可发现性与真实性**
Copilot CLI 的 `allowed_directories` 不加载（#4398）、远程控制开关失效（#4409）、`banner` 不生效——配置"写入无反馈"问题引发开发者强烈不满。《配置要么明确报错、要么真正生效》成为跨项目共识。

---

### 4. 差异化定位分析

| 工具 | 核心定位 | 差异化特征 | 目标用户 |
|---|---|---|---|
| **Claude Code** | 功能全面的重型 agent CLI | 网关限额、工作区信任等企业级治理机制；功能广度领先（桌面、IDE、移动端全覆盖），但复杂度与成本失控风险并存 | 企业中高强度使用者，多设备协同开发者 |
| **Copilot CLI** | GitHub 生态深度绑定的官方 CLI | 与 GitHub Enterprise、远程控制、社 region 功能深度联动；Windows 平台适配明显滞后（渲染循环崩溃、toast 崩溃） | GitHub 重度用户、企业组织 |
| **OpenCode** | 开源可扩展的插件化 agent 平台 | v2 插件 API（Tool 域）、本地模型优先（OpenAI 兼容端点自动发现，205👍）、SQLite 会话模型；社区驱动，技术选型偏 Rust/Go 栈 | 开源开发者、本地模型爱好者、高度定制需求者 |
| **Kimi Code** | 轻量聚焦的上下文管理工具 | 主推 Memory System 跨会话记忆，体量尚小，但切入点是差异化场景（持久化上下文） | 追求简单、注重上下文连续性的个人开发者 |

---

### 5. 社区热度与成熟度

**最活跃：OpenCode**。单日 4 个同源 bug 集中上报 + 8 个 PR，最高需求 205👍（模型自动发现），证明其社区参与度高且迭代节奏快。但"事件表膨胀 13GB"（#33356）等基础设施问题也说明其成熟度仍在爬坡。

**最受瞩目：Claude Code**。双版本连发 + 184👍 的头部需求，社区规模大、声量大。但 MCP 崩溃、费用异常等重大事故频发，反映出功能扩张速度与稳定性保障之间存在明显张力。

**最稳定但承压：Copilot CLI**。版本更新较克制，但 10 个高影响 issue 中 7 个是 bug 或回归，且 Windows 问题占比高，社区耐心正在消耗。

**最早期：Kimi Code**。活跃 issue 仅 2 条，尚处于用户需求探索期；单次生成 88k 乱码 token 的严重 bug（#2597）需要快速止血以建立信任。

---

### 6. 值得关注的趋势信号

**① 稳定性与资源安全正成为核心购买理由**。Claude Code 的 MCP 内存崩溃、OpenCode 的 13GB 数据库膨胀、Kimi 的 token 失控——工具不仅需要"会干活"，更需要"不闯祸"。开发者在选型时应重点考察资源上限、进程隔离和故障恢复能力。

**② 成本可见性将决定企业级取舍**。Claude Code #60093 的模型静默切换与 $1,050 超额收费，打开了"成本透明"这一敏感话题。能提供实时费用披露、模型锁定、限额告警的工具将获得企业信任溢价。

**③ 远程与多设备协同成为刚需**。Claude Code 和 Copilot CLI 的远程控制 issue 共同指向一个趋势：开发者希望从手机/平板接管桌面端的 agent 任务。支持无头模式、远程 API、会话镜像的能力将成为下一代 CLI 的标配。

**④ 配置系统需要"确定性"**。多个工具出现"配置写了但没生效""静默失败"的问题，开发者已经厌倦了黑盒式配置。未来 CLI 应当提供配置校验、生效状态回显和诊断命令，而不是默默忽略错误。

**⑤ 本地/私有模型支持是差异化突破口**。OpenCode 的模型自动发现需求拿到 205👍，表明有一大批用户正在尝试用 Ollama、LM Studio 等本地模型替代云端 API。这对数据敏感型公司和成本敏感型个人开发者尤其有吸引力。

**⑥ Windows 平台是被忽视的蓝海**。Copilot CLI 的 10 个高影响 issue 中近半与 Windows 相关，Claude Code 的 macOS 崩溃问题也反映出跨平台测试不足。给 Windows/macOS 提供一等公民支持，是赢得开发者口碑的确定性机会。

---

**给决策者的建议**：
- 评估工具时，稳定性指标（崩溃率、资源失控风险）应优先于功能数量；
- 关注各工具对 MCP 资源上限、配置诊断、成本告警的官方响应速度；
- 多设备/远程工作流团队，优先选择原生支持无头模式与远程控制的工具；
- 有私有化或成本控制需求的团队，可重点关注 OpenCode 等开源方案。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---

# Claude Code 社区动态日报（2026-08-09）

## 今日速览

今日连续发布 v2.1.225、v2.1.226 两个版本，核心变化是新增网关消费限额提示与 `claude agents` 工作区信任机制。社区热度方面，**消息队列模式**（#50246）以 184 👍 成为最受期待的功能请求；同时，MCP 服务器资源失控导致 macOS 内核崩溃的报告（#64366）为稳定性问题敲响警钟。成本透明度与跨平台一致性仍是开发者投诉的高频区。

---

## 版本发布

### v2.1.226
- **内容**：Bug 修复与可靠性改进。

### v2.1.225
- **新增**：网关消费限额支持——Claude Code 的用量警告新增 spend-limit 提示；达到限额时，消息会显示具体额度上限、重置时间及操作者自定义消息（需网关同步升级至 2.1.225）。
- **新增**：`claude agents` 针对不受信任目录增加工作区信任提示，与主 CLI 行为对齐。

---

## 社区热点 Issues（Top 10）

### 1. [Feature Request] 消息队列模式 — 成为最热功能呼声
- **Issue**: [#50246](https://github.com/anthropics/claude-code/issues/50246)
- **状态**: OPEN | 👍 184 | 💬 50
- **要点**: 当 Claude 正在执行任务时，用户无法追加后续想法而不打断当前工作。提议新增消息队列模式，将新消息排队而不是抢占。
- **分析**: 50 条评论、184 赞高居榜首，说明“非侵入式协作”是当前工作流最大的痛点。该功能若落地，将显著改善长任务场景下的用户体验。

### 2. [Feature Request] 在 Claude Desktop 中远程控制 Claude Code 会话
- **Issue**: [#29006](https://github.com/anthropics/claude-code/issues/29006)
- **状态**: OPEN | 👍 119 | 💬 36
- **要点**: 用户希望能在 Claude Desktop App 中远程连接并控制正在运行的 Claude Code 会话，实现移动端/桌面端跨设备接管。
- **分析**: 反映多设备、多端协同的强烈需求，与远程/无头工作流趋势一致。

### 3. [BUG] VS Code 集成完全不加载 MCP 服务器
- **Issue**: [#19054](https://github.com/anthropics/claude-code/issues/19054)
- **状态**: OPEN | 👍 26 | 💬 24
- **要点**: 在 Claude Code For VS Code 中，MCP 服务器配置完全不生效，导致 IDE 内工具调用缺失。
- **分析**: 已持续数月仍为 OPEN，IDE 集成与 MCP 的兼容性是高频痛点，影响面较大。

### 4. [BUG] MCP 服务器无界扇出导致 macOS 内核崩溃
- **Issue**: [#64366](https://github.com/anthropics/claude-code/issues/64366)
- **状态**: CLOSED (stale) | 💬 18
- **要点**: Cowork/agent 会话中，MCP 服务器被无限扇出，耗尽 32GB 内存并导致 macOS 内核崩溃（4 次 panic + 强制关机）。M2 Max 设备同样中招。
- **分析**: 虽已关闭并标记 stale，但暴露出 MCP 缺少资源上限管控的严重问题，与 #70564（远程 runner 无条件加载所有插件）互为印证。

### 5. [BUG] 模型被静默切换至 Opus，3 天超额收费 $1,050
- **Issue**: [#60093](https://github.com/anthropics/claude-code/issues/60093)
- **状态**: CLOSED (stale) | 💬 10
- **要点**: 用户声称后台模型在无通知、无 UI 披露的情况下从 Sonnet 切为 Opus，叠加 5 次进程故障与 7 个成本放大器，5 月 5-7 日产生约 $1,050 超额费用。
- **分析**: 成本透明度和模型选择可见性问题引发强烈信任危机，是财务类 issue 中最具代表性的一例。

### 6. [Feature Request] 开发历史默认不写入代码注释 / docstrings
- **Issue**: [#85130](https://github.com/anthropics/claude-code/issues/85130)
- **状态**: OPEN（2026-08-08 新开）| 👍 0 | 💬 1
- **要点**: 建议 Claude Code 默认不要将开发历史以注释/docstring 形式写入代码中，开发记录应保留在 git 而非源码文件里。
- **分析**: 新开 issue，反映开发者对代码整洁度与 git 作为唯一事实来源的诉求。

### 7. [BUG] Claude Code Desktop 内置 CLI 持续 ECONNRESET
- **Issue**: [#84818](https://github.com/anthropics/claude-code/issues/84818)
- **状态**: OPEN（2026-08-07 新开）| 💬 1
- **要点**: 桌面应用更新至 1.25927.0.0 后，从 Desktop 启动的 Claude Code 会话反复出现 `ECONNRESET`，而同机 npm CLI 运行正常。
- **分析**: 新出现的集成 bug，影响 Desktop 内置 CLI 的重度用户；CLI 与 Desktop 行为不一致值得跟进。

### 8. [BUG] macOS Desktop 应用禁用 Dispatch，移动端正常
- **Issue**: [#80058](https://github.com/anthropics/claude-code/issues/80058)
- **状态**: OPEN | 👍 1 | 💬 9
- **要点**: Dispatch 功能在 macOS Desktop 端被禁用，但移动端可用，跨端功能不一致。
- **分析**: 平台功能差异导致工作流割裂，用户希望桌面端补齐能力。

### 9. [BUG] 账单显示已付费，但账户仍停留在 Free 计划
- **Issue**: [#66558](https://github.com/anthropics/claude-code/issues/66558)
- **状态**: CLOSED (stale) | 👍 1 | 💬 9
- **要点**:

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-08-09

## 1. 今日速览

昨日发布补丁版 **v1.0.79-9**，仅包含 `/sandbox` 配置对话框的存储位置提示改进。Issue 方面，Windows 平台的渲染循环与通知崩溃两大回归问题仍持续引发关注，同时社区密集提交了一系列 triage 新问题，涉及 skill 工具回归、npm 安装版本漂移、配置项不生效等。PR 方面则暂无新进展。

## 2. 版本发布

**v1.0.79-9** — 小幅改进  
- `/sandbox` 配置对话框现在会显示沙箱设置实际存储于 `settings.json` 中的位置，便于用户手动修改与排查。

https://github.com/github/copilot-cli/releases/tag/v1.0.79-9

## 3. 社区热点 Issues

以下为过去 24 小时内更新中最值得关注的 10 个 Issue：

1. **Windows 主面板冻结——无限 React/Ink 渲染循环回归**  
   [#4222](https://github.com/github/copilot-cli/issues/4222) — `[area:platform-windows, area:terminal-rendering]`  
   早前已在 #2802 修复的渲染循环问题在 v1.0.72+ 重新出现，表现为主视图间歇性冻结、输出被吞、`/resume` 后内容才恢复。严重影响 Windows 下 VS Code 集成终端的日常使用，虽已标记 closed，但开发者仍需关注新版本是否真正修复。

2. **Windows 启用 `notifications` 后 `copilot.exe` 反复崩溃**  
   [#4219](https://github.com/github/copilot-cli/issues/4219) — `[area:platform-windows]`  
   原生访问冲突导致硬崩溃，发生在系统通知（toast）路径。Windows 用户启用通知功能后无法稳定运行，属高影响稳定性问题。

3. **`--add-dir` 导致 Claude 子代理调度返回 400 cache_control 块超限**  
   [#4185](https://github.com/github/copilot-cli/issues/4185) — `[area:agents, area:models]`  
   只要启动时带一个或多个 `--add-dir` 参数，所有 Anthropic 模型的子代理调度都会因超过 4 个 `cache_control` 块而上限失败，核心工作流被阻断。

4. **skill 工具无法找到 `~/.agents/skills` 下已安装技能（回归）**  
   [#4401](https://github.com/github/copilot-cli/issues/4401) — `[area:platform-windows, area:tools]`  
   新提交的 triage 问题：`skill` 工具找不到有效的本地技能目录，社区怀疑与已关闭的 #2230 相关，属于修复不完整或新回归。

5. **`/resume` 恢复会话后自动切回默认模型**  
   [#4397](https://github.com/github/copilot-cli/issues/4397) — `[area:sessions, area:models]`  
   使用 `--model` 指定模型创建的会话，在被恢复后不再保留原模型设定，而是退回默认模型。这与已发布的 `contextTier` 配置诉求叠加，反映出用户对模型会话一致性的明确期望。

6. **`permissions.config` 中的 `allowed_directories` 从未被加载**  
   [#4398](https://github.com/github/copilot-cli/issues/4398) — `[area:permissions, area:configuration]`  
   配置了多个工作区目录白名单，但 `/list-dirs` 中完全看不到。配置项静默失效，用户无法按预期限制文件访问范围。

7. **npm 全局安装的 `bin/copilot` 是加载器而非版本固定**  
   [#4402](https://github.com/github/copilot-cli/issues/4402) — `[area:installation]`  
   同一路径的 `copilot` 命令在 101 秒内先后运行了 1.0.77 和 1.0.78 两个版本，而 npm 包本身未变。`--prefer-version` 可绕过但无文档说明，给 CI 与生产环境带来不确定性。

8. **`/agent` 弹窗将 `.github\agents\AGENTS.md` 误认为自定义代理**  
   [#4410](https://github.com/github/copilot-cli/issues/4410) — `[triage]`  
   文档明确的仓库说明文件 `AGENTS.md` 被 `/agent` 当作自定义 agent 定义解析，并报出 frontmatter 格式错误，属于工具链识别逻辑干扰。

9. **远程控制开关静默失效——`cli_remote_control_enabled=false` 时无任何提示**  
   [#4409](https://github.com/github/copilot-cli/issues/4409) — `[triage]`  
   当账户 entitlement 禁用远程控制时，桌面端与 GitHub Mobile 均无提示，设置项可随意修改但实际不生效，Mobile 端仅返回裸 HTTP 422。体验割裂且难以排查。

10. **Copilot Enterprise 路由下 `/mcp` 的 `github-mcp-server` 认证永远失败**  
    [#4408](https://github.com/github/copilot-cli/issues/4408) — `[triage]`  
    企业账号触发 OAuth 后发现企业 MCP 主机通告了跨源 resource identifier，导致授权元数据发现失败，阻断企业用户使用内置 MCP 服务器。

## 4. 重要 PR 进展

过去 24 小时内无新增或更新的 Pull Requests。当前社区焦点集中在 Issue 反馈与回归修复上，期待后续版本对齐这些高优问题。

## 5. 功能需求趋势

从各 Issue 中可提炼出以下社区关注的功能方向：

- **Windows 平台稳定性**：渲染循环、原生崩溃、PowerShell 下 `.claude/settings.local.json` hooks 中 `||`、`&&` 等运算符无法执行，均反映出 Windows 一等公民体验仍是薄弱环节。
- **会话与模型一致性**：期望 `resume` 保留模型/上下文窗口设置，并希望 ACP 层也开放 `contextTier` 配置（#4275），使非交互场景与交互模式对齐。
- **配置系统完善**：`banner: "once"` 不生效（#4129）、`allowed_directories` 不加载（#4398）、`Ctrl+C` 行为不可重映射（#4394）、快速删除会话操作被移除（#4395）等，说明用户希望配置项都真正可依赖、可发现。
- **Agent/Skill 生态增强**：包括为自定义 agent 增加 `skill` 工具别名（#4209）、修正 `AGENTS.md` 误识别（#4410）、修复 skill 工具对 `~/.agents/skills` 的查找回归（#4401）。
- **企业/账户场景**：企业版 MCP 认证、`cli_remote_control_enabled` 状态可见性、Copilot Free 在 Codespaces 中提示“No model available”（#4405），是企业与免费用户正在遭遇的现实障碍。
- **本地化**：#4407 提出为桌面应用及 CLI 添加中文（zh-CN）UI，显示社区对多语言界面的需求开始浮现。

## 6. 开发者关注点

- **Windows 是主要痛点平台**：多个高影响 bug（渲染循环、toast 崩溃、PowerShell 钩子不兼容）都集中在 Windows；用户期望官方优先修复并增加平台回归测试。
- **配置项“假可用”问题突出**：部分配置看似支持但实际不加载或静默失效（`allowed_directories`、`banner`、远程控制开关），开发者希望配置要么明确报错、要么真正生效，不接受“写入无反馈”的状态。
- **模型会话保留是刚需**：resume 后模型切换、递归恢复时上下文窗口丢失等，会让依赖特定模型的用户感到“会话被重置”。
- **安装机制引发信任问题**：npm loader 在同一路径上飘移版本，开发者担心 CI 可复现性和生产稳定性，要求官方文档明确 `--prefer-version` 用法或直接固定版本。
- **工具链混淆成本高**：AGENTS.md 被当作 agent、skill 工具找不到本地技能、`--add-dir` 破坏 Claude 子代理，这些“生态位”问题容易浪费大量排查时间，社区反应积极。

---

*本日报根据 GitHub 公开数据自动整理，仅供社区参考。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-08-09

## 今日速览

过去 24 小时社区动态集中在两条 Issue 上：#1283「内存系统」功能请求持续发酵，累计 25 条评论成为当前最热议题；昨日新上报的 #2597 严重 Bug（单次 LLM 生成 88k 乱码 token）拉响稳定性警报。期间无新版本发布，PR 活动亦无更新。

## 版本发布

过去 24 小时内无新版本发布，暂无 Release 更新可汇总。

## 社区热点 Issues

数据窗口内活跃 Issue 共 2 条（本期全量覆盖），以下逐一分析：

### 1. #1283 — 功能请求：内存系统，跨会话持久化上下文
- **作者**：@CatKang | 创建 2026-02-27 | 更新 2026-08-08
- **评论**：25
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/1283

**核心诉求**：实现系统化 Memory System，让 CLI 能跨会话记住项目上下文、代码模式与用户偏好，具体包含自动记忆（AI 管理的笔记）与手动记忆

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-09

## 今日速览

过去 24 小时无新版本发布，但社区并不平静：**OpenCode Go 网关的 `deepseek-v4-flash` 模型名前导空格问题**在一天内集中爆发了 4 个相关 Issue（#41300、#41306、#41314、#41322），且此前标记修复的 #41211 被证实未生效；功能需求端，**原生会话目标 `/goal`（#27167）和 OpenAI 兼容端点模型自动发现（#6231）**仍是热度最高的两个诉求，分别获得 128 与 205 个 👍。PR 侧则以自动化清理为主，另有两个新提交的开源 PR（fish 补全、通配符转义）值得关注。

## 社区热点 Issues（Top 10）

1. **#27167 [FEATURE] 原生会话目标 `/goal`** — 69 评论 / 128 👍
   自定义斜杠命令已有，但缺少持久化的会话目标与生命周期管理，社区呼声极高。
   https://github.com/anomalyco/opencode/issues/27167

2. **#6231 OpenAI 兼容端点模型自动发现** — 45 评论 / 205 👍
   LM Studio / Ollama / llama.cpp 等本地 provider 需要手动罗列模型，模型频繁变动维护成本高，是本地模型用户的最大痛点。
   https://github.com/anomalyco/opencode/issues/6231

3. **#33356 [2.0] `event` 表无界增长，opencode.db 达 13GB+** — 15 评论 / 4 👍
   事件溯源表从不清理，长时间实例使 SQLite 膨胀至 13GB 并几乎占满磁盘，需引入保留策略或压缩机制。
   https://github.com/anomalyco/opencode/issues/33356

4. **#14965 启动缓慢（Ghostty 特定）** — 19 评论 / 13 👍
   1.2.1 版本后在 Ghostty 中启动明显变慢，其他终端正常，疑似终端探测或 PTY 初始化回归。
   https://github.com/anomalyco/opencode/issues/14965

5. **#41300 [Bug] `deepseek-v4-flash` 模型名前带前导空格** — 4 评论 / 1 👍
   Console Go 报错显示 `you passed  deepseek-v4-flash`（多了空格），OpenCode Desktop v1.18.15 + Windows 11 复现。
   https://github.com/anomalyco/opencode/issues/41300

6. **#41306 [Bug] #41211 修复未生效：网关仍转发前导空格** — 3 评论
   用户于 2026-08-09 用有效 key 实测 `https://opencode.ai/zen/go/v1/chat/completions` 仍返回 HTTP 400，根因指向网关两侧的模型名处理。
   https://github.com/anomalyco/opencode/issues/41306

7. **#31307 同一项目多实例共享同一 SQLite 会话** — 4 评论 / 3 👍
   两个终端同时运行 opencode，会话内容互相串扰，需要按进程隔离或实现会话锁定。
   https://github.com/anomalyco/opencode/issues/31307

8. **#30611 瞬时网络错误直接中断会话，不触发重试** — 6 评论 / 1 👍
   重试路径仅识别 `ECONNRESET`，其他瞬时错误（如 DNS 抖动、连接重置）被算作硬失败，建议扩大可重试错误类型。
   https://github.com/anomalyco/opencode/issues/30611

9. **#38932 向输入框粘贴长文本导致桌面端挂死** — 5 评论
   粘贴约 5000 字符以上时 Desktop 应用完全无响应，疑似渲染或状态更新未做分片处理。
   https://github.com/anomalyco/opencode/issues/38932

10. **#41234 插件含一个非函数命名导出即整体静默失效** — 2 评论
    插件中混入非函数导出会使整个插件被跳过，且无任何用户可见错误，注册的 MCP 与 hook 全部消失，调试成本极高。
    https://github.com/anomalyco/opencode/issues/41234

## 重要 PR 进展（Top 10）

1. **#41336 fish shell 补全支持** — 新增 `completion` 子命令，按 shell 参数输出 bash/zsh/fish 补全脚本，解决 #41232 中 fish 拿到 bash 语法的问题。
   https://github.com/anomalyco/opencode/pull/41336

2. **#41335 转义字面量通配符并锚定 patch 插入位置** — 修复 #41333，统一 `packages/core/src/util/wildcard.ts` 与旧版逻辑的匹配行为。
   https://github.com/anomalyco/opencode/pull/41335

3. **#35898 防止切换标签页时覆盖会话模型** — Kobalte Select 在外部受控值变化时误触发 onChange，导致用户手动选择的模型被 agent 默认值覆盖，修复后所有会话选择得以保留。
   https://github.com/anomalyco/opencode/pull/35898

4. **#35857 初始消息页大小从 2 增至 20** — 大幅减少加载历史会话时的翻页次数，改善长会话的滚动体验。
   https://github.com/anomalyco/opencode/pull/35857

5. **#35871 修复 headless run 启动死锁** — Effect fiber 重入导致 `opencode run` 在冷启动高负载时约 40% 概率挂起，已加回归测试。
   https://github.com/anomalyco/opencode/pull/35871

6. **#35877 转发本地 MCP 服务器 stderr 到错误诊断** — 此前 stderr 管道无人读取，MCP 服务端输出错误时完全不可见，现接入诊断面板。
   https://github.com/anomalyco/opencode/pull/35877

7. **#35869 v2 插件 API 新增 Tool 域** — 为 Effect / Promise 插件提供 `PluginContext.tool.transform()` 命令式注册与注销工具的能力，补齐与 v1 的差距。
   https://github.com/anomalyco/opencode/pull/35869

8. **#35926 恢复 agent 环境标记注入** — 在 legacy shell 与 V2 bash 进程边界统一注入 `OPENCODE=1` 与 `AGENT=1`，保持环境变量继承

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*