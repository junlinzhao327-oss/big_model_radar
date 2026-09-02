# AI CLI 工具社区动态日报 2026-09-02

> 生成时间: 2026-09-02 00:19 UTC | 覆盖工具: 7 个

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
**数据截至 2026-09-02** | 来源：github.com/anthropics/skills | 说明：以下 PR 均处于 **OPEN 状态**（暂无 merged），按评论活跃度排序。

---

## 一、热门 Skills 排行（Top 7）

### 1. skill-creator 评估工具链修复 — PR #1298
- **功能**：修复 `run_eval.py` 对任何 skill 描述均报告 `recall=0%` 的问题，并改进 Windows 流读取、触发检测与并行处理。
- **讨论热点**：社区最高关注度 PR，直接对应 issue #556（10+ 独立复现

---

# Claude Code 社区动态日报 — 2026-09-02

---

## 今日速览

- **双版本发布**：v2.1.258 修复 macOS 12 启动回归与远程会话报错；v2.1.257 引入新旗舰模型 Claude Fable 5.1 并新增时间格式/时区设置。
- **社区焦点**：vim 模式光标形状增强以 42 👍 成为今日最高赞需求；MCP draft-07 schema 兼容性问题（41 评论）已由官方修复关闭。
- **批量处理**：7 月集中提交的 cyber 安全误报系列（约 20 条）全部标记为重复并关闭，社区对误报打断合法工作流的投诉值得持续关注。

---

## 版本发布

### v2.1.258（最新）
- **修复**：macOS 12 (Monterey) 启动失败——2.1.255 引入的回归问题。
- **修复**：远程/定时会话在重新发送权限批准后报 "user messages must have non-empty content" 错误。

### v2.1.257
- **新模型**：Claude Fable 5.1（`claude-fable-5-1`），成为默认 Fable 模型。1M 上下文窗口，定价 $10/$50 每百万 tokens（缓存读取 $0.25/Mtok）。
- **新设置**：新增 `timeFormat`（12/24 小时、UTC、strftime 模式）与 `timeZone`，可自定义回合结束时钟与转录显示格式。

---

## 社区热点 Issues

### 1. [已关闭] MCP draft-07 schema 被客户端完全拒绝
- **作者**: @amitfin | 评论 41 | 👍 13
- **问题**: 声明 draft-07 outputSchema 的 MCP server 在分派前就被客户端以 "unsupported dialect" 拒绝，完全不可用。
- **价值**: 反映 MCP 生态对 JSON Schema 版本兼容的高要求，41 条评论表明影响面广，已修复关闭。
- 🔗 https://github.com/anthropics/claude-code/issues/86142

### 2. [开放] GitHub 连接器显示已连接但不暴露任何工具（Windows）
- **作者**: @ranilyons-ctrl | 评论 31 | 👍 24
- **问题**: Windows 11 桌面应用中 GitHub connector 状态为 "Connected"，但 Cowork 中看不到任何工具。
- **价值**: 31 条讨论 + 24 👍，Windows 桌面集成稳定性是社区强烈关注的方向。
- 🔗 https://github.com/anthropics/claude-code/issues/61682

### 3. [开放] vim 模式光标形状跟随模式切换
- **作者**: @halvorlinder | 评论 5 | 👍 42
- **请求**: vim 模式下 Insert 用细线光标、Normal 用方块光标。
- **价值**: 仅 5 条评论却收获 42 👍，说明编辑器体验细节对重度用户极为重要，属低成本高价值改进。
- 🔗 https://github.com/anthropics/claude-code/issues/32469

### 4. [已关闭] Windows 桌面版自动更新后消息内容全部丢失
- **作者**: @guan64 | 评论 15 | 👍 9
- **问题**: 更新后侧边栏有会话记录但消息正文缺失，JSONL 文件未持久化。
- **价值**: 数据丢失属严重事故，15 条评论讨论回滚与恢复方案，已关闭修复。
- 🔗 https://github.com/anthropics/claude-code/issues/53717

### 5. [开放] Bedrock 上 getContextUsage 按条目计费
- **作者**: @dafzthomas | 评论 3 | 👍 0
- **问题**: 在 Bedrock application-inference-profile 上 `CountTokens` 被拒，回退到 `messages.create`（max_tokens=1）读取 input_tokens，且每个上下文条目执行一次，造成大量按量计费。
- **价值**: 新近上报的成本类问题，对 Bedrock 企业用户有直接财务影响。
- 🔗 https://github.com/anthropics/claude-code/issues/86628

### 6-10. cyber 安全误报系列（代表性选取）
以下 5 条仅为该系列中较有代表性的样本。该系列由单一用户从 7 月 6 日起持续上报，累计约 20 条，全部标记为 duplicate 并关闭。共同特征是：合法开发/调试场景被服务器端 cyber 安全过滤器误判为网络安全威胁，触发后会话中止（session-halted），且部分触发点为用户表达沮丧情绪（如 "YOU F••• SHGIT!"）。

| Issue | 请求 ID | 场景 |
|---|---|---|
| #75792 | req_011Ccq4qQMX8h4JMButvzEf9 | 硬件调试被误判 |
| #75555 | req_011Ccoxy1X7DHomS8UsFWMYM | 个人 Android 设备 APK 静态分析 |
| #75364 | req_011CcoAjdGB9Xs5QVtMUc2Sj | Frida 内存检查被拦截 |
| #74985 | req_011CcmaeFCn4WG9c7dEoQGde | 情绪化表达触发了阻断 |
| #74987 | req_011Ccmaec6suGp85f5t5sGxa | 无实质 cyber 内容的按键噪声 |

- **社区关注点**：误报阻断合法工作流、对用户情绪化语言过度敏感、批量提交后官方关闭但未见系统性修复声明。
- 🔗 https://github.com/anthropics/claude-code/issues/75792
- 🔗 https://github.com/anthropics/claude-code/issues/75555
- 🔗 https://github.com/anthropics/claude-code/issues/75364
- 🔗 https://github.com/anthropics/claude-code/issues/74985
- 🔗 https://github.com/anthropics/claude-code/issues/74987

---

## 重要 PR 进展

过去 24 小时内仅有 1 条 PR 更新，不存在 10 条待选 PR。当前活跃度为低点，可能是版本发布后维护期。

### [已关闭] ralph-wiggum 插件安全加固
- **作者**: @kazukinakai | 创建 2026-07-17 | 更新 2026-09-01
- **内容**: 
  - 限制循环最大迭代次数（bounded iterations），防止无限循环
  - 新增 push/publish 操作保护，避免无人值守循环自动发布半成品
  - 修复 stop-hook 机制，确保中断逻辑可靠触发
- **价值**: Ralph 循环默认无限迭代且无发布保护，存在严重安全风险。该 PR 保留本地实验能力的同时加装安全护栏，社区插件治理迈出一步。
- 🔗 https://github.com/anthropics/claude-code/pull/78371

---

## 功能需求趋势

从近期 Issues 中提炼的社区主要功能方向：

1. **编辑器深度体验**（👍 42）
   - vim 模式光标形状随模式切换（#32469），反映终端 UI 细节打磨需求

2. **MCP 生态兼容性**（👍 13 + 系列问题）
   - JSON Schema dialect 完整支持（#86142）
   - 连接器工具在桌面端的可见性/可用性（#61682）

3. **安全过滤器精度**（系列 20+ 条）
   - 误报率降低、对用户情绪表达的容错、授权工作流白名单

4. **平台稳定性与数据安全**
   - macOS 回归问题（v2.1.255→v2.1.258 来回修复）
   - Windows 数据持久化完整性（#53717）

5. **成本可观测性**
   - 云上推理按量计费的透明化（#86628），用户希望在跳过 CountTokens 时有明确提示或批量处理

---

## 开发者关注点

1. **MCP 标准兼容是头号问题**：draft-07 schema 被拒、连接器工具不显示，两起高讨论量 Issue 均涉及 MCP 生态互操作性，开发者期待 Anthropic 更激进的兼容策略。

2. **误报阻断工作流是最集中的投诉**：cyber 系列 20 余条 issue 中，用户反复强调"个人设备""授权调试""合法研究"等关键词，且对"因情绪化表达触发阻断"表示强烈不满。建议 Anthropic 公开误报处理流程与修复时间线。

3. **平台回归令人警觉**：macOS 12 启动回归说明测试矩阵覆盖不足；Windows 数据丢失引发了社区对桌面应用持久化机制的信任危机。

4. **计费透明化需求浮现**：新上报的 Bedrock 按上下文条目付费问题（#86628）虽评论不多，但属于"静默扣费"类问题，可能在更多企业用户关注后升级。

5. **社区插件生态处于早期**：唯一活跃 PR 为插件安全加固，表明官方插件体系已出现但在工程成熟度上仍需努力。

---

*日报数据来源：github.com/anthropics/claude-code · 数据窗口：2026-08-31 至 2026-09-02*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-09-02

## 今日速览

昨日 Gemini CLI 密集发版：正式版 v0.58.0 与预览版 v0.59.0-preview.0 先后发布，主线聚焦 symlink 路径处理与 ignore 规则修复。社区侧对 subagent 可靠性的质疑持续升温——`MAX_TURNS` 被误报为成功、generalist agent 无限挂起等问题讨论激烈。PR 侧则集中出现一批安全加固类提交，包括硬编码 API key 清理、配置文件权限校验、OAuth issuer 验证等，显示项目正加强对供应链与运行时安全的治理。

## 版本发布

过去 24 小时共发布 3 个版本：

- **v0.58.0（正式版）**：主要包含 symlink 评估一致性修复（`ensure consistent symlink evaluation in ignore path handling`），解决 workspace 通过 symlink 访问时 ignore 规则失效的问题。
- **v0.59.0-preview.0**：紧随 v0.58.0 发布，包含核心逻辑修复（`fix(core): prevent ...`，详情待 changelog 补全），另有版本号 bump。
- **v0.59.0-nightly.20260901.g0bd1d4397**：日常夜间构建，无独立变更说明。

发布关联 PR：[v0.58.0 Changelog](https://github.com/google-gemini/gemini-cli/pull/29161)、[v0.59.0-preview.0 Changelog](https://github.com/google-gemini/gemini-cli/pull/29159)、[版本号 bump 至 0.60.0-nightly](https://github.com/google-gemini/gemini-cli/pull/29162)

## 社区热点 Issues

以下 10 个 Issue 为昨日讨论最热烈或影响面最广的问题：

1. **[Subagent 达到 MAX_TURNS 却被报告为 GOAL 成功，中断被隐藏](https://github.com/google-gemini/gemini-cli/issues/22323)**
   `codebase_investigator` 明明因达到最大轮次而停止分析，却对外报告 `status: "success"` / `Termination Reason: "GOAL"`，严重误导用户判断。13 条评论，社区反应强烈，属于 P1 级别 bug。

2. **[Generalist agent 无限挂起](https://github.com/google-gemini/gemini-cli/issues/21409)**
   只要模型决定委派给 generalist agent 就永久卡住，连建文件夹这种简单操作也会挂起，用户最长等待 1 小时。8 个 👍 为近期最高，P1 且需重新测试。

3. **[Gemini 不主动使用 skills 和 sub-agents](https://github.com/google-gemini/gemini-cli/issues/21968)**
   用户反馈即使提供了 gradle、git 等自定义 skill，模型在相关场景下也不会主动调用，只有显式指令才生效。直接影响用户自定义工作流的价值。

4. **[Shell 命令执行完成后卡在 "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)**
   极简 CLI 命令执行完毕后终端仍显示等待输入，且命令状态一直保持 active。属于 P1 高频复现问题，影响日常使用体验。

5. **[零依赖 OS 沙箱与执行后意图路由（bash affinity）](https://github.com/google-gemini/gemini-cli/issues/19873)**
   提议利用 Gemini 3 模型原生 bash 能力，在 sandbox 中安全执行 POSIX 工具链，并增加执行后意图路由。属于设计层面的 enhancement，9 条评论持续讨论中。

6. **[AST-aware 文件读取/搜索/代码库映射影响评估](https://github.com/google-gemini/gemini-cli/issues/22745)**
   EPIC 级 issue，探索用 AST 感知工具减少 token 消耗、精确读取方法边界、减少对齐偏差。与开发者普遍关注的成本与上下文窗口效率直接相关。

7. **[Auto Memory 确定性脱敏与日志减少](https://github.com/google-gemini/gemini-cli/issues/26525)**
   指出 Auto Memory 在提取前即将 transcript 内容送入模型上下文，脱敏发生在"内容已进上下文之后"，且服务可能记录已有技能，属于安全缺陷。

8. **[超过 128 个工具时遭遇 400 错误](https://github.com/google-gemini/gemini-cli/issues/24246)**
   当可用工具数量过多时 API 直接报错，用户期望模型能更智能地裁剪可用工具范围。对深度定制 MCP 工具的用户影响明显。

9. **[~/.gemini/agents 下 symlink 文件不被识别为 agent](https://github.com/google-gemini/gemini-cli/issues/20079)**
   通过 symlink 管理 agent 定义文件的用户无法正常加载，与昨日版本修复的 symlink ignore 问题属于同一技术债务区域。

10. **[Browser subagent 在 Wayland 下失败](https://github.com/google-gemini/gemini-cli/issues/21983)**
   浏览器子代理在 Wayland 会话中直接失败，Termination Reason 为 GOAL。Linux 桌面用户受影响较大，P1 且需重新测试。

## 重要 PR 进展

以下 10 个 PR 反映了当前代码库的活跃开发方向：

1. **[系统级配置路径的严格权限与所有权检查](https://github.com/google-gemini/gemini-cli/pull/29115)**
   在 Windows 和 POSIX 上加载系统级配置前强制执行文件所有权与 ACL 验证，防止恶意配置注入。安全加固方向的重要一步。

2. **[Git 仓库内认证崩溃修复（macOS Seatbelt）](https://github.com/google-gemini/gemini-cli/pull/29163)**
   修复在受限权限环境下（如 macOS Seatbelt）启动 Gemini CLI 时的崩溃问题，根因与 `useGitBranchName` hook 读取 `.git` 失败有关。P1 安全修复。

3. **[清理 chrome-devtools-mcp 中硬编码的 Google CrUX API key](https://github.com/google-gemini/gemini-cli/pull/29158)**
   从编译产物中移除硬编码 API key，避免敏感凭证暴露在 npm 包和文件系统镜像中。

4. **[Skill 优先级与激活状态大小写不敏感处理](https://github.com/google-gemini/gemini-cli/pull/29151)**
   修复 `SkillManager` 中因 skill 名称大小写不同导致的工作区覆盖内置/扩展 skill 失效问题，对使用混合大小写命名的用户很关键。

5. **[Shell 执行不再清空用户 git config](https://github.com/google-gemini/gemini-cli/pull/29156)**
   回退此前将 `GIT_CONFIG_GLOBAL` / `GIT_CONFIG_SYSTEM` 指向 `/dev/null` 的行为，恢复 shell 命令中 `user.name`、`user.email` 等真实配置可用。

6. **[isEmpty() 对 BOM 编码内容的正确解码](https://github.com/google-gemini/gemini-cli/pull/29155)**
   修复 UTF-16/UTF-32 编码的空白 plan 文件因 NUL 字符被误判为非空的问题，涉及 `validatePlanContent` 等路径。

7. **[MCP OAuth 流程实现 RFC 9207 issuer 校验](https://github.com/google-gemini/gemini-cli/pull/29117)**
   在 OAuth 授权响应中增加 `iss` 参数校验，防止 token 路由到非预期服务器，提升 MCP 安全基线。

8. **[SSE 流结束事件不再静默丢失](https://github.com/google-gemini/gemini-cli/pull/29106)**
   修复 stream 结束时无尾随空行（如代理截断）导致 `finishReason`/usage 元数据丢失的问题，改善错误可诊断性。

9. **[symlink 工作区根的 glob 结果保留](https://github.com/google-gemini/gemini-cli/pull/28975)**
   修复 macOS 下 `/tmp` 指向 `/private/tmp` 等 symlink 场景导致 glob 误报 "No files found" 的问题（issue #28416），影响面广。

10. **[NTFS 8.3 短文件名路径绕过缓解](https://github.com/google-gemini/gemini-cli/pull/29116)**
   在路径归一化和 AllowedPathChecker 中处理 `git~1`、`env~1` 等 Windows 短名，封堵 NTFS 上的路径遍历与 blocklist 绕过风险。

另有 [#29120 增强 WebFetch 目标校验与连接路由](https://github.com/google-gemini/gemini-cli/pull/29120)（DNS 异步解析 + Undici 连接绑定）和 [#29115 扩展环境变量变更需用户同意](https://github.com/google-gemini/gemini-cli/pull/28863) 也值得关注。

## 功能需求趋势

从近期 Issues 与 PR 中可提炼出以下社区最关注的方向：

- **Subagent 可靠性治理**：误报成功、挂起、不主动使用技能——三类问题共同指向 subagent 的决策透明度与生命周期管理仍是最大痛点。
- **安全与合规加固**：Auto Memory 脱敏时机、硬编码密钥清理、配置文件权限校验、OAuth issuer 验证，安全类提交占比显著上升。
- **Token 效率优化**：AST-aware 文件读取、Tactful Extraction 分层搜索、按工具数量裁剪等提议，反映用户对上下文成本的高度敏感。
- **跨平台文件系统兼容**：symlink（macOS `/tmp`）、NTFS 8.3 短名、Windows junction——平台差异导致的路径问题持续涌现。
- **浏览器 Agent 体验**：Wayland 支持、settings.json 覆盖、持久化会话锁恢复，浏览器子代理的稳定性仍是 Linux/远程开发用户的关注重点。

## 开发者关注点

- **Subagent 行为不可信**：`MAX_TURNS` 被包装成成功、generalist agent 挂起、不主动调用技能，开发者普遍感觉"模型能力很强但 agent 编排不可控"。
- **Shell 交互卡顿**："Waiting input" 是高频关键词，简单命令执行后 hang 住严重影响自动化流程。
- **内存/记忆系统隐患**：Auto Memory 存在低信号会话无限重试、无效 patch 静默跳过、脱敏滞后等一揽子问题（见 [#26516 汇总](https://github.com/google-gemini/gemini-cli/issues/26516)），安全与资源双重风险。
- **配置可见性与还原**：shell 执行强制清空 git config 引发反弹（PR #29156），说明开发者对"工具擅自改动环境"高度敏感，期望保持用户配置的原样传递。
- **文档与 CLI 一致性**：存在 6 个已注册但未文档化的 CLI 标志（`--policy`、`--session-id` 等），社区对"Agent 应准确了解自身能力"的呼声持续（issue #21432）。

---
*数据来源：[github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli) | 统计窗口：2026-08-31 至 2026-09-02*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-09-02）

> 数据来源：github.com/MoonshotAI/kimi-cli

## 1. 今日速览

- Kimi CLI 发布 v1.50.0，包含 anthropic-beta 空 header 修复、kosong 依赖升级，以及 shell 弃用感知更新流程，开始引导一键迁移到 Kimi Code。
- 两个历史 Issue 关闭：一个关于“执行任务时无法预输入下一个任务 prompt”，另一个关于“Task 子任务调用偶发卡住”。
- 社区 PR 主要围绕版本发布、插件安全文档、skills 列表能力和迁移流程，整体显示项目正加速向统一品牌 **Kimi Code** 收敛。

## 2. 版本发布

### v1.50.0

- **fix(kosong): omit empty anthropic-beta header**  
  在没有声明 beta 特性时，不再发送空的 `anthropic-beta` header，减少 API 请求噪音。  
  [#2580](https://github.com/MoonshotAI/kimi-cli/pull/2580)

- **chore(release): bump kosong to 0.56.0**  
  依赖 kosong 升级到 0.56.0。  
  [#2581](https://github.com/MoonshotAI/kimi-cli/pull/2581)

- **feat(shell): deprecation-aware update flow**  
  CLI 会读取 CDN 上的迁移公告，检测到 kimi-cli 已弃用后，引导用户一键迁移到 Kimi Code。  
  [#2630](https://github.com/MoonshotAI/kimi-cli/pull/2630)

- **chore(release): bump kimi-cli to 1.50.0**  
  完成 1.50.0 版本号同步、release notes 更新，并同步 `packages/kimi-code` wrapper 依赖。  
  [#2632](https://github.com/MoonshotAI/kimi-cli/pull/2632)

## 3. 社区热点 Issues

> 本期数据窗口内仅有 2 个 Issue 更新，以下全部列出。

### #1287 [CLOSED] 执行当前任务时，无法同时编写下一个任务的 prompt

- 作者：@XiaoPengYouCode  
- 创建：2026-02-28｜更新：2026-09-01｜评论：1｜👍：0  
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1287

**摘要**：在执行一个任务时，下一个任务的 prompt 输入框保持锁定/不可访问，用户无法提前准备后续任务内容，影响连续任务编排效率。

**重要性**：这是任务批处理场景下的常见诉求。用户希望 CLI 支持并行预输入或任务队列机制；该 Issue 已关闭，但评论区讨论值得关注。

### #1292 [CLOSED] 调用 Task 时有时会卡住

- 作者：@Wolido  
- 版本：kimi 1.16.0｜平台：Darwin 25.3.0 arm64  
- 创建：2026-03-01｜更新：2026-09-01｜评论：0｜👍：0  
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1292

**摘要**：多个 Task 子任务并行/连续调用时，某个子任务会偶发卡住，且没有明显报错。

**重要性**：Task 执行稳定性直接影响自动化流程可靠性。虽然已经关闭，但这类偶发阻塞问题通常是高优先级修复对象。

## 4. 重要 PR 进展

> 本期共 4 个 PR 更新，以下全部列出。

### #2614 [OPEN] docs(plugins): document security and persistent data

- 作者：@QIANLING-0831  
- 更新：2026-09-01  
- 链接：https://github.com/MoonshotAI/kimi-cli/pull/2614

**说明**：文档型 PR，明确 `plugin.json`、`command` 工具、`inject`、`~/.kimi/plugins/` 目录的插件

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-09-02

## 1. 今日速览

OpenCode 发布 v1.18.26 补丁版本，重点修复 Claude 5 会话与 Bedrock GPT-5.6 模型的兼容性问题。社区层面，#4283「复制到剪贴板失效」以 128 条评论成为最热 Issue，持续近一年仍未解决；而 #6231「OpenAI 兼容 Provider 模型自动发现」以 225 个 👍 成为社区最渴求的功能。PR 侧，Windows 桌面端沙箱权限修复、托管更新机制、插件 API 扩展（表单/事件流/webhooks/权限断言）是当前开发主线。

## 2. 版本发布

**v1.18.26** 发布（核心更新）：

- **Claude 5 sessions**：现在可容忍过期的 thinking blocks，提示或工具变更后不再直接失败。
- **Bedrock GPT-5.6 模型**：支持 `none` reasoning effort 选项。
- **Bedrock**：reasoning 与 replay 处理逻辑更可靠（感谢 @pengzh1）。
- **工具调用**：时间戳记录保持精确。

🔗 https://github.com/anomalyco/opencode/releases

## 3. 社区热点 Issues

### #4283 Copy To Clipboard is not working（复制到剪贴板失效）
**128 评论 · 119 👍 · 创建于 2025-11-13 · OPEN**

用户选中回复文本后无法复制到剪贴板，自 v1.0.62 起报告，持续近一年仍为 OPEN，是当前社区抱怨最集中的问题之一。

🔗 https://github.com/anomalyco/opencode/issues/4283

### #6231 Auto-discover models from OpenAI-compatible provider endpoints
**47 评论 · 225 👍 · OPEN**

LM Studio、Ollama、llama.cpp 等本地 Provider 要求用户手动在 `opencode.json` 中列出所有模型，模型经常变动导致管理繁琐且易错。这是目前 👍 数最高的 Issue，社区对自动发现呼声极强。

🔗 https://github.com/anomalyco/opencode/issues/6231

### #3688 System Theme no longer works after v1.0.0
**38 评论 · 20 👍 · CLOSED**

v1.0.0 后 System 主题选项消失，配置为 `system` 也不再生效。虽是已关闭的 bug，但说明主题功能在 1.0 重构中出现了回归。

🔗 https://github.com/anomalyco/opencode/issues/3688

### #10490 [Feature Request] Add config option to disable copy-on-select behavior
**18 评论 · 32 👍 · OPEN**

OpenCode 实现了 XTerm/GPM 风格的「选中即复制」，用户希望能在 `opencode.json` 中配置关闭。与 #4283 同属剪贴板交互体验问题。

🔗 https://github.com/anomalyco/opencode/issues/10490

### #19466 opencode is using CPU for doing nothing!
**16 评论 · 16 👍 · OPEN**

等待 API 限流重试（`retrying in 18m 12s`）时，opencode 在 i9-14900 上仍占用约 50% 单核 CPU，用户质疑后台空转的轮询/重试实现过于低效。

🔗 https://github.com/anomalyco/opencode/issues/19466

### #7006 `permission.ask` plugin hook is defined but not triggered
**14 评论 · 24 👍 · OPEN**

插件开发者按文档实现 `permission.ask` Hook 后从未被触发。新权限系统（PR #6319）的插件扩展点存在文档与实现脱节的问题，直接影响社区插件开发生态。

🔗 https://github.com/anomalyco/opencode/issues/7006

### #38723 `opencode run` intermittently hangs during init — no session created, no output, no error (~56% failure rate)
**8 评论 · 2 👍 · OPEN**

`opencode run` 在创建会话前间歇性挂起：进程存活但零 stdout、零错误，日志停留在 `message=init`，只能靠外部超时终止，失败率约 56%。这是 CLI 核心路径的严重可靠性问题。

🔗 https://github.com/anomalyco/opencode/issues/38723

### #25570 [FEATURE]: Support Multiple Skills in a Single Prompt
**8 评论 · 22 👍 · OPEN**

当前单个 Prompt 无法同时调用多个 Skills，多框架工作流不得不拆分多次请求。社区希望支持一次指定多个 Skill 的能力。

🔗 https://github.com/anomalyco/opencode/issues/25570

### #18011 LM Studio shows only 3/9 models in opencode models lmstudio
**7 评论 · 5 👍 · OPEN**

LM Studio autodiscovery 不完整，`/v1/models` 返回 9 个模型但 opencode 只显示 3 个。即使配置 API key 也一样。说明 OpenAI 兼容 Provider 的模型发现逻辑存在兼容性缺陷。

🔗 https://github.com/anomalyco/opencode/issues/18011

### #1515 Feature request: cli tab completions for bash, fish, and zsh
**11 评论 · 33 👍 · CLOSED**

社区希望提供 `source <(opencode completions $SHELL)` 式 shell 补全。虽已关闭，但 33 个 👍 表明 CLI 集成体验仍是用户关心的方向。

🔗 https://github.com/anomalyco/opencode/issues/1515

## 4. 重要 PR 进展

### #46696 fix(desktop): grant Windows sandbox access during installation
**OPEN · @Hona**

修复 Windows 上 NSIS 安装后缺少 `ALL RESTRICTED APPLICATION PACKAGES` 读取/执行权限导致的 Electron 启动失败问题，涉及安装包 ACL 设置。

🔗 https://github.com/anomalyco/opencode/pull/46696

### #46695 fix(app): keep sync failures out of location recovery
**OPEN · @Hona**

连接与工作区同步失败时保持编辑区和草稿可见，失败读操作原地重试；重连后刷新会话，只有确认 `LocationNotFoundError` 才进行目录恢复。改善弱网环境的错误体验。

🔗 https://github.com/anomalyco/opencode/pull/46695

### #46694 fix(app): preserve worktree creation title and busy state
**OPEN · @Hona**

创建 worktree 期间保持会话标题可见，并在桌面标签页、后台标签页、移动端标题栏/抽屉中正确显示 busy 指示器。修复状态切换时的 UI 空窗。

🔗 https://github.com/anomalyco/opencode/pull/46694

### #46485 [contributor] feat(cli): apply managed updates when idle and wire up ui
**OPEN · @jlongster**

托管模式下跳过 TUI 启动更新检查，改为监听服务端 Session 执行结束事件，待无活跃会话时静默安装更新。避免更新打断用户工作流。

🔗 https://github.com/anomalyco/opencode/pull/46485

### #46558 refactor(app): drive persisted state with Effect Schema
**OPEN · @Brendonovich**

将 Web/Desktop 共 30 个持久化消费者（设置、编辑器、终端、布局、服务器状态等）迁移到 Effect Schema，统一类型约束并移除隐式默认值。

🔗 https://github.com/anomalyco/opencode/pull/46558

### #46690 feat(plugin): expose session forms, session list, and global event stream
**OPEN · @mblakele**

面向 Telegram Bot 类插件场景，向插件 API 暴露会话表单（session forms）、会话列表和全局事件流，显著扩展插件可驱动的 UI 与数据能力。

🔗 https://github.com/anomalyco/opencode/pull/46690

### #46687 feat(core): add async session webhooks
**OPEN · @R44VC0RP**

为 v2 prompt 请求增加可选 `callbackUrl`，用于移动端通知和无法维持 SSE 连接的外部集成。补齐异步会话集成的重要拼图。

🔗 https://github.com/anomalyco/opencode/pull/46687

### #46531 feat(browser): add a public-API browser plugin
**OPEN · @Hona**

新增实验性 `browser` 工具插件，完全基于公开插件接口实现，并通过 `@opencode-ai/schema/browser` 共享浏览器安全契约。

🔗 https://github.com/anomalyco/opencode/pull/46531

### #46530 feat(plugin): expose permission assertions
**OPEN · @Hona**

为 Effect 与 Promise 插件新增 `ctx.permission.assert(input)` 方法，复用现有权限引擎，不新增 HTTP 端点。浏览器插件的 URL 权限检查即基于此实现。

🔗 https://github.com/anomalyco/opencode/pull/46530

### #40142 fix(opencode): surface

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-09-02

## 今日速览

过去 24 小时，Qwen Code 社区核心动态集中在 **TUI 渲染层迁移（ink → OpenTUI）** 的持续发酵、**0.22.3 版本引入的 llama.cpp grammar 解析回归**（约 12 条相关评论），以及 **`permissions.allow` 行为变更引发的权限模型讨论**。同时，**cua-driver-rs v0.20.3** 发布了新的预构建二进制（含 macOS 已签名公证版本）。Web Shell 与会话管理相关的 PR 和 Issue 数量显著上升，成为当前社区建设的重点方向。

---

## 版本发布

### cua-driver-rs v0.20.3
- **地址**: [GitHub Releases](https://github.com/QwenLM/qwen-code/releases)
- **内容**: Qwen CUA Driver 预构建二进制更新（vendored under `packages/cua-driver`）。
- **平台支持**:
  - **macOS**: 已代码签名 + 公证的 universal binary + `QwenCuaDriver.app`
  - **Linux**: 未签名（x86_64 + arm64, glibc 2.31 floor）
  - **Windows**: 未签名 UIAccess worker + 原生 SDK payload（x86_64 + arm64）

---

## 社区热点 Issues（精选 10 条）

### 1. TUI 渲染层迁移跟踪（高热度）
- **#8662** | [OPEN] [TUI migration from ink to OpenTUI](https://github.com/QwenLM/qwen-code/issues/8662)
- 评论数：16 | 作者：@chiga0
- **要点**: 当前 TUI 基于 ink 7 + React 19，携带约 1037 行 patch。Issue 列举了结构性 flicker 等难以在 ink 内修复的问题。社区讨论热度最高，但值得注意的是 👍 为 0，属于开发者主导的重构跟踪，用户侧声量尚不明显。

### 2. llama.cpp 400 "failed to parse grammar"（已关闭）
- **#10520** | [CLOSED] [toolSearch threshold > 0 导致 llama.cpp 400](https://github.com/QwenLM/qwen-code/issues/10520)
- 评论数：7 | 作者：@SLP-DEV1
- **要点**: 0.22.3 中，`tools.toolSearch.threshold = 10` 配合本地 llama.cpp 时，每次请求都 400 失败；threshold 0 则正常。涉及 MCP 工具与本地推理服务的兼容性，直接影响本地模型用户。

### 3. permissions.allow 语义变化（P1）
- **#10218** | [OPEN] [permissions.allow 0.22.1 起未覆盖工具直接禁用](https://github.com/QwenLM/qwen-code/issues/10218)
- 评论数：5 | 作者：@pandazhangS
- **要点**: 0.21.1 及之前 `allow` 为“自动批准列表”；0.22.1 起变为“注册表白名单”，未覆盖的工具被直接禁用且不会询问。这是权限模型的行为 breaking change，且文档未说明。目前标记为 `need-retesting`，表明维护者已开始复现确认。

### 4. llama-server 同样报错（0.22.3 回归）
- **#10530** | [OPEN] [400 Failed to initialize samplers in 0.22.3](https://github.com/QwenLM/qwen-code/issues/10530)
- 评论数：5 | 作者：@tonydiep
- **要点**: 与 #10520 类似，但用户使用的是 Qwen 3.8 27b / 3.6 35b 在 llama-server 上。Gemma 模型正常，Pi / OpenCode 无此问题。明确指向 0.22.3 引入的回归，上一版本正常。

### 5. serve: ACP NDJSON 通道队列饱和
- **#10162** | [OPEN] [Degrade gracefully when ACP NDJSON channel queue saturates](https://github.com/QwenLM/qwen-code/issues/10162)
- 评论数：5 | 作者：@yiliang114
- **要点**: `qwen serve` 在队列溢出时直接拆掉整个 channel（fail-closed），生产环境中触发过。社区期望是优雅降级而不是整体拆除。是 daemon 稳定性方向的关键问题。

### 6. serve: 会话恢复丢失已持久化消息
- **#10710** | [OPEN] [Reloading killed session hides persisted assistant messages](https://github.com/QwenLM/qwen-code/issues/10710)
- 评论数：4 | 作者：@yiliang114
- **要点**: 当 prompt 回合被中断（如 #10162 的 teardown），虽然输出已持久化到 channel 历史，但 reload 后不显示。是会话一致性的数据丢失类 bug，影响对 daemon 工作流的信任。

### 7. tools.eager 条目导致 PermissionManager 崩溃（P1）
- **#10400** | [OPEN] [tools.eager entry named after Object.prototype key crashes](https://github.com/QwenLM/qwen-code/issues/10400)
- 评论数：4 | 作者：@yiliang114
- **要点**: 若 `tools.eager` 配置项名为 `constructor`、`__proto__` 等 Object.prototype 键，初始化直接崩溃。是权限系统重构（#10098）引入的边界问题，P1 严重级别，目前等待修复。

### 8. Web Shell 会话级 turn 导航（已进入实现）
- **#10750** | [OPEN] [feat(web-shell): add session-wide turn navigation](https://github.com/QwenLM/qwen-code/issues/10750)
- 评论数：3 | 创建于 2026-09-01，更新于 09-02，状态 `in-progress`
- **要点**: 希望实现 Codex 风格的会话全局 turn 导航侧栏，无需下载整个 transcript 即可跳转。开发效率高——Issue 创建后就由 @doudouOUC 提交了 PR #10751，是 Web Shell 体验升级的关键方向。

### 9. CI 测试确定性失败（P1）
- **#10734** | [OPEN] [1000 ms CPU budget is wall-clock applied to CPU-time metric](https://github.com/QwenLM/qwen-code/issues/10734)
- 评论数：2 | 作者：@TianYuan1024
- **要点**: `shellAstParser.test.ts` 将 `process.cpuUsage()` 与字面量 `1000 ms` 比较，单位错配导致 GitHub-hosted runner 上必然失败。开发基础设施问题，会阻塞合并和发布流程。

### 10. standalone channels 未应用 approvalMode（P1）
- **#10714** | [OPEN] [apply approvalMode to standalone sessions](https://github.com/QwenLM/qwen-code/issues/10714)
- 评论数：2 | 作者：@qqqys
- **要点**: `channels.<name>.approvalMode` 被解析但未应用于 standalone ACP 会话，权限配置形同虚设。已标记 `status/ready-for-agent`。

---

## 重要 PR 进展（精选 10 条）

### 1. Web Shell 会话 turn 导航协议（Phase 1）
- **#10751** | [OPEN] [feat(serve): add session turn navigation protocol](https://github.com/QwenLM/qwen-code/pull/10751)
- 作者：@doudouOUC
- **要点**: 为 #10750 提供 daemon/SDK 契约：有界的持久 turn 稀疏索引、签名工作区快照、分页元数据，支持在不加载完整 transcript 的情况下跳转。

### 2. Web Shell 加载独立会话模型目录
- **#10719** | [OPEN] [fix(web-shell): Load models for fresh standalone sessions](https://github.com/QwenLM/qwen-code/pull/10719)
- 作者：@doudouOUC
- **要点**: 为 Web Shell 增加 capability-gated 的 standalone options endpoint，由内部 Conversations 运行时驱动，并在 TypeScript SDK 侧校验响应。

### 3. Workspace-scoped MCP 管理
- **#10679** | [OPEN] [feat(serve): add workspace-scoped MCP management](https://github.com/QwenLM/qwen-code/pull/10679)
- 作者：@ytahdn
- **要点**: MCP 配置写入在 runtime 冷启动时保持持久，reload / reconnect / approval / auth / tools 等操作均路由到选定的 workspace runtime。这是服务端多 workspace 隔离的重要一步。

### 4. Workspace-scoped Skills 运行时
- **#10697** | [OPEN] [feat(serve): add workspace-scoped Skills runtime](https://github.com/QwenLM/qwen-code/pull/10697)
- 作者：@ytahdn
- **要点**: 将 Skills 管理迁移到 workspace 独立 runtime，分离持久配置与运行时发现，并通过 revision / epoch 元数据追踪就绪状态，配置变更后自动 reconcile 活动会话。

### 5. Channel 对话支持 BTW 侧问
- **#10713** | [OPEN] [feat(channels): add BTW side questions to Channel conversations](https://github.com/QwenLM/qwen-code/pull/10713)
- 作者：@qqqys
- **要点**: 在 Channel 对话中支持 `/btw <question>`：校验文本输入与会话授权，即时确认请求（带 correlation ID），侧问不进入主对话历史。

### 6. Review 流程内容过滤器修复
- **#10421** | [OPEN] [fix(review): screen content filters before the probe tree's restore](https://github.com/QwenLM/qwen-code/pull/10421)
- 作者：@wenshao
- **要点**: `scratch-tree` 会拒绝在仓库定义了 `filter.<name>.smudge` 时创建/重置树（本地 config）。本 PR 在探针树恢复前先检查内容过滤器，避免 checkout 触发外部过滤器。

### 7. 隐藏不可用的外部编辑器选项
- **#10746** | [OPEN] [fix(cli): hide unavailable external editor option](https://github.com/QwenLM/qwen-code/pull/10746)
- 作者：@SLP-DEV1
- **要点**: 在执行编辑确认时，若配置的 `preferredEditor` 不可用或不在 PATH 中，则不再显示“Modify with external editor”选项，并补充回归测试。

### 8. 保留斜杠命令附件
- **#10730** | [OPEN] [fix(web-shell): preserve slash command attachments](https://github.com/QwenLM/qwen-code/pull/10730)
- 作者：@ytahdn
- **要点**: 修复技能、自定义命令、MCP prompt、workflow 等展开时图片/文件附件被丢弃的问题；内置控制命令仍丢弃附件，别名命令与 canonical 分类一致。

### 9. 瞬态网络错误自动重试
- **#10347** | [OPEN] [feat(core): auto-retry transient network errors (EOF)](https://github.com/QwenLM/qwen-code/pull/10347)
- 作者：@qwen-code-dev-bot
- **要点**: 将“4xx 但底层实际是网络中断”（如 `400 network error ... EOF`）分类为可重试的传输错误，进入现有 bounded auto-retry。此前这类错误被视为 fail-fast，在 channel 场景下会导致立即失败。

### 10. 输出语言文件不可写时的启动崩溃
- **#10455** | [OPEN] [fix(cli): don't crash startup when the output-language file is unwritable](https://github.com/QwenLM/qwen-code/pull/10455)
- 作者：@qwen-code-dev-bot
- **要点**: CLI 每次启动会写入 advisory output-language 规则文件。当全局配置目录为只读（read-only home、root 遗留文件）时，未防护的写入直接抛出。本 PR 让启动不再崩溃。

---

## 功能需求趋势

从过去 24 小时的 Issues 看，社区最关注的功能方向为：

1. **终端用户体验重构（roadmap/terminal-ux）**
   - #8662（TUI → OpenTUI）、#10728（OpenTUI 迁移后续项）、#10745（外部编辑器优化）、#10749（滚动行为）。
   - 说明终端 UI 的稳定性与交互细节是当前最集中的投入方向。

2. **Web Shell 与会话管理**
   - #10750（turn 导航）、#10261（会话内容搜索）、#10717（结构化任务标题）、#10710（会话恢复消息丢失）。
   - session 粒度的管理与恢复能力成为 Web Shell 发展的核心路径。

3. **通道 / 渠道集成（Channels）**
   - #10711/#10713（/btw 侧问）、#10714（approvalMode 应用）、#233

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*