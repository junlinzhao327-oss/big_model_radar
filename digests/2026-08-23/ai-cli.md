# AI CLI 工具社区动态日报 2026-08-23

> 生成时间: 2026-08-22 22:35 UTC | 覆盖工具: 7 个

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



---

# Claude Code 社区动态日报 — 2026-08-23

## 今日速览

- 发布补丁版本 **v2.1.240**，仅包含 bug 修复与可靠性改进，无新增功能。
- 社区最热话题仍是 **#27302**（多 Connector 账户支持），已积累 234 条评论、357 个 👍，高居榜首且仍在持续讨论。
- 多个与 **Hook 系统行为不一致** 相关的 Issue 活跃（Windows 不触发、subagent 跳过、插件禁用后仍执行），成为开发者反馈最集中的方向。

---

## 版本发布

### v2.1.240
- 仅包含 bug 修复和可靠性改进（Bug fixes and reliability improvements），无详细变更日志。

---

## 社区热点 Issues（10 个）

### 1. 🔥 支持多 Connector 账户（同一 Connector、不同账户） — #27302
**状态**: OPEN | 评论 234 | 👍 357
社区呼声最高的功能请求。用户希望在 Claude Code 中同时使用同一个 Connector（如 GitHub、Google）下的多个不同账户，当前只能使用单一账户，严重阻碍了多身份工作流。
https://github.com/anthropics/claude-code/issues/27302

### 2. 后台 agent 会话快速终止、attach 时崩溃循环、丢失任务记录 — #75037
**状态**: OPEN | 评论 9
`claude --bg` / `claude agents` 工作流在 macOS 上暴露三个独立问题：后台会话快速终止、worker 在 attach 时反复崩溃、后台任务完成记录丢失。对依赖无人值守 agent 的自动化团队影响巨大。
https://github.com/anthropics/claude-code/issues/75037

### 3. 2.1.238 回归：交互式会话 thinking 只存签名空壳 — #88383
**状态**: OPEN | 评论 3 | 👍 1
从 2.1.238 开始，交互式 CLI 会话把 thinking 块持久化为 `thinking: ""` 空内容 + 签名的"空壳"，与 #87947 记录的 print 模式问题同形。影响 session 回放、审查与记忆恢复。
https://github.com/anthropics/claude-code/issues/88383

### 4. [最新版本] Windows 上 PreToolUse hooks 完全不触发（v2.1.240） — #88896
**状态**: OPEN | 评论 1
刚发布的 v2.1.240 中，Windows 平台 `.claude/settings.json` 里配置的 `PreToolUse` hooks 从不触发，所有工具调用（Bash、PowerShell、Edit、Write）均绕行；而 `SessionStart`、`Stop`、`SessionEnd` 等 hooks 正常。Windows 用户的安全与合规链被直接击穿。
https://github.com/anthropics/claude-code/issues/88896

### 5. PreToolUse hooks 对 subagent 静默跳过 — #69260
**状态**: CLOSED（needs-info）| 评论 6 | 👍 2
主 agent 的 `PreToolUse` hooks 正常，但在 `Agent` 工具派生的 subagent 中被完全静默跳过，命令重写、安全检查和 instrumentation 只覆盖部分实际工具调用。与 #86405、#88896 构成 Hook 覆盖缺失的连环报告。
https://github.com/anthropics/claude-code/issues/69260

### 6. 静态 ask 规则获批后，同模式命令不再触发 PreToolUse hook — #62437
**状态**: CLOSED | 评论 7
当某条命令模式获得 session 级批准后，后续相同模式的调用不再经过 `PreToolUse` hook。说明"批准记忆"的优先级高于 hook 执行，绕过了 hook 链中的安全/审计逻辑。
https://github.com/anthropics/claude-code/issues/62437

### 7. 提交归属硬编码 "Claude Opus 4.7 (1M context)" — #66506
**状态**: CLOSED（stale）| 评论 2 | 👍 1
系统提示将 `Co-Authored-By: Claude Opus 4.7 (1M context)` 硬编码进 commit trailer，即使用户切换到 Sonnet 等其他模型仍错误署名。社区质疑模型的自我认知与元数据真实性。
https://github.com/anthropics/claude-code/issues/66506

### 8. skill 与 MCP 服务器同名导致静默丢服务 — #85827
**状态**: CLOSED | 评论 2
当 `.claude/skills/<name>/` 的 skill 与 `~/.claude.json` 中注册的 MCP 服务器同名时，harness 在启动时静默不加载该 MCP 服务器，无错误、无警告。命名冲突应该被检测并提示，而不是静默吞掉。
https://github.com/anthropics/claude-code/issues/85827

### 9. 项目 slug 路径段重复导致记忆静默分裂 — #86525
**状态**: CLOSED | 评论 2
项目路径 `/Projects/companyname/companyname-ios` 生成的 slug 中 `companyname` 出现两次，但写入路径与读取路径不一致，导致同一个 session 的内存 key 错位、记忆静默分裂且无法召回。
https://github.com/anthropics/claude-code/issues/86525

### 10. 禁用插件的 PostToolUse hook 仍每次执行 — #85893
**状态**: CLOSED | 评论 2
插件被禁用后，其 `PostToolUse` hook 仍在每次 Edit/Write 时执行，但 `/hooks` 列表中已不显示。这不仅让用户"以为禁用了"而产生误判，更构成安全与隐私风险。
https://github.com/anthropics/claude-code/issues/85893

---

## 重要 PR 进展

过去 24 小时内 **无公开 PR 更新**（共 0 条）。仓库当前处于补丁修复窗口期，团队重心在 v2.1.240 的稳定性修复上，预计后续会有针对 Hook 与后台 agent 问题的修复 PR 合入。

---

## 功能需求趋势

从本期 Issue 中可提炼出社区最集中的六个功能方向：

1. **安全过滤器可配置化** — 大量反馈（#61646、#72909、#73409、#73432、#73439 等）指向同一个诉求：本地开发、学术研究、授权安全测试等合法场景频繁被 safeguard 误报，希望支持按项目/领域关闭或调低敏感度。该类 Issue 多为 stale/closed，说明官方尚未正面回应。

2. **多账户 / 多身份支持** — #27302 是当之无愧的榜首，用户对 Connector 多账户的诉求已远超一般 feature request，几乎成为企业使用的硬门槛。

3. **Hook 系统全链路一致性** — subagent 不触发（#69260、#86405）、Windows 不触发（#88896）、批准记忆绕过 hook（#62437）、禁用插件仍执行（#85893）——四个不同角度揭示同一问题：hook 语义在子代理、跨平台、权限记录、插件生命周期上都不一致。

4. **后台 / 异步任务可靠性** — #75037 暴露的崩溃循环与任务记录丢失，反映 `claude --bg` 在长时间运行场景下仍不成熟。

5. **插件生命周期管理** — 禁用状态未被彻底执行（#85893），插件与内置功能（skills、MCP）的命名冲突静默失败（#85827），说明插件运行时边界需要更严格的隔离与校验。

6. **元数据/会话完整性** — thinking 空壳回归（#88383）、UUID 复用（#86188）、slug 读写不一致（#86525）、提交署名硬编码（#66506）：session 的持久化与身份追踪成为高频回归区。

---

## 开发者关注点

**Hook 相关（最高频痛点）**
- `PreToolUse` 在 subagent 与 Windows 上静默失效，安全拦截出现巨大盲区。
- Session 批准记忆会绕过 hook 链，导致"已批准过一次，后续完全裸奔"。
- 禁用插件后 hook 仍执行，用户对被禁用的能力失去信任。

**安全误报正在伤害正常开发**
- 多个用户报告在合法工程、学术研究、甚至 BJJ 教学博客上遭遇 safeguard 拦截，且无清晰豁免机制。反馈中可见沮丧情绪，"Fable 5 has no use" 等表述已出现在 Issues 中。

**新版本回归频繁**
- 2.1.238 引入 thinking 空壳，2.1.212→2.1.214 引入 `CLAUDE_CODE_TASK_LIST_ID` 被覆盖（#79495），2.1.240 引入 Windows hooks 失效。连续三次小版本均带回归，开发者已开始对"升级需谨慎"形成共识。

**静默失败是比报错更痛的体验**
- MCP 服务器因同名冲突被静默丢弃、记忆因 slug 不一致静默分裂、UUID 被静默复用——多个 issue 都指向同一个结论：宁可显式报错，也不要无痕的坏行为。

---

*本日报基于 GitHub anthropics/claude-code 仓库公开数据自动整理，数据截止 2026-08-23。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-23

## 今日速览

- 过去 24 小时发布 3 个 Rust 核心库 alpha 版本（0.150.0-alpha.7 / alpha.6 / 0.149.0-alpha.7.2），均属迭代性预发布，无重大功能变更说明。
- 认证与会话稳定性成为社区头号痛点：macOS、Windows、CLI 和 VS Code 扩展均出现打开历史会话后触发 401、登录循环甚至账号被注销的问题，多个 Issue 评论数持续上升。
- 性能问题依旧显著：#25719 中 Codex Desktop for macOS 导致系统级进程 `syspolicyd` / `trustd` CPU 与内存失控，以 394 👍 高居社区关注榜榜首。

## 版本发布

过去 24 小时共发布 3 个 Rust crate 版本（均为 alpha 预发布，无详细变更日志）：

| 版本 | 说明 |
|---|---|
| [rust-v0.150.0-alpha.7](https://github.com/openai/codex) | 0.150.0 系列第 7 个 alpha |
| [rust-v0.149.0-alpha.7.2](https://github.com/openai/codex) | 0.149.0 系列补丁 alpha |
| [rust-v0.150.0-alpha.6](https://github.com/openai/codex) | 0.150.0 系列第 6 个 alpha |

三个版本均聚焦 Rust 核心库的迭代，建议关注 0.150.0-alpha 系列的稳定性改进。

## 社区热点 Issues

### 1. Codex Desktop for macOS 触发 syspolicyd/trustd 资源失控 🔥
[#25719](https://github.com/openai/codex/issues/25719) — 评论 85 | 👍 394

macOS 上 Codex Desktop 反复触发系统级 `syspolicyd` / `trustd` 进程 CPU 和内存跑满。这是当前社区反馈最强烈的问题，👍 数远超其他 Issue，说明大量 macOS 用户受到影响。

### 2. macOS 打开已有对话使 ChatGPT 认证失效
[#39162](https://github.com/openai/codex/issues/39162) — 评论 37 | 👍 26

在版本 26.814.41407 中，打开一个既有会话会导致 ChatGPT 认证被无效化并重定向到登录页。用户反馈上一版本 26.810.52044 正常，疑似回归问题。

### 3. ChatGPT Desktop 反复生成 Computer Use 进程并以 V8 OOM 崩溃
[#38455](https://github.com/openai/codex

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-23

## 今日速览

昨日发布了 v0.56.0 夜间版，修复了 macOS Seatbelt 沙箱对 Docker 容器运行时的隔离缺口（首次贡献者 @josebalius）。与此同时，社区围绕 Subagent 可靠性、（Auto Memory）记忆系统质量与安全以及沙箱逃逸防护的讨论持续升温，多个 P1 级 bug 正在等待重测。

## 版本发布

**v0.56.0-nightly.20260822.g5411f113c**（2026-08-22 发布）

- 修复：macOS Seatbelt 沙箱现已隔离 Docker 和容器运行时的 Unix Domain Socket、CLI 二进制、Mach/XPC 服务查找及 POSIX 共享内存，以阻止通过容器 Hypervisor 文件系统挂载（如 Docker Desktop VirtioFS）实现沙箱逃逸。
- 新增贡献者：@josebalius（首个 PR 即修复安全关键问题）

🔗 https://github.com/google-gemini/gemini-cli/releases/tag/v0.56.0-nightly.20260822.g5411f113c

## 社区热点 Issues

1. **Subagent 在 MAX_TURNS 后被误报为 GOAL 成功**（#22323，P1，13 评论）
   `codebase_investigator` 子代理在达到最大轮次、未做任何分析时仍报告 `status: "success"` / `Termination Reason: "GOAL"`，掩盖了真实的中断原因。社区认为这个错误状态传递会误导开发者对 Agent 实际行为的判断。
   🔗 https://github.com/google-gemini/gemini-cli/issues/22323

2. **Generalist Agent 无限挂起**（#21409，P1，8 评论，8 👍）
   用户反映一旦委托给 generalist agent（仅创建文件夹这种简单操作），就会永久挂起（最长等待 1 小时）。手动在提示中禁止使用 subagent 可回避该问题，说明根因在 Agent 调度层而非模型能力。
   🔗 https://github.com/google-gemini/gemini-cli/issues/21409

3. **零依赖 OS 沙箱与执行后意图路由**（#19873，P2，8 评论）
   提议充分利用 Gemini 3 模型的原生 bash 能力——通过 OS 级沙箱（非 Docker）安全地让模型使用 `grep/sed/awk` 等 POSIX 工具，并在执行后进行意图路由，兼顾安全与模型偏好。
   🔗 https://github.com/google-gemini/gemini-cli/issues/19873

4. **AST 感知文件读取/搜索/代码映射的评估**（#22745，P2，7 评论）
   EPIC 级 issue，探索利用 AST 感知工具实现方法级精确读取、减少 token 噪声与轮次错位。评论区关注其对大型代码库上下文占用的实质改善。
   🔗 https://github.com/google-gemini/gemini-cli/issues/22745

5. **Gemini 不会主动使用 skills 和 sub-agents**（#21968，P2，6 评论）
   用户发现即使定义了 `gradle`/`git` 等技能，模型仍倾向于直接执行命令而非调用技能，必须显式指示才会使用，大幅削弱了自定义技能的实用价值。
   🔗 https://github.com/google-gemini/gemini-cli/issues/21968

6. **Auto Memory 对低信号会话无限重试**（#26522，P2，5 评论）
   后台提取代理一旦判断某会话“低信号”而不读取，该会话会永远留在待处理索引中，造成反复空转。社区建议增加处理状态标记（如“跳过/低信号”）。
   🔗 https://github.com/google-gemini/gemini-cli/issues/26522

7. **Auto Memory 缺少确定性脱敏且日志过多**（#26525，P2，4 评论，安全）
   当前提取提示词要求模型脱敏，但敏感内容在进入模型上下文之前未被确定性去除；且服务会记录已有技能等内容，存在泄露风险。
   🔗 https://github.com/google-gemini/gemini-cli/issues/26525

8. **Shell 命令执行后卡在 "Waiting input"**（#25166，P1，4 评论，3 👍）
   极为简单的 CLI 命令在已完成后仍显示活动状态，界面停留在“等待输入”，需要手动干预。影响自动化流程的稳定性。
   🔗 https://github.com/google-gemini/gemini-cli/issues/25166

9. **Browser Agent 在 Wayland 环境下失败**（#21983，P1，4 评论，1 👍）
   browser subagent 在 Wayland 会话中直接以 GOAL 终止。评论指出这可能与 Chromium 沙箱/显示协议兼容性有关，Wayland 用户无法使用浏览器子代理。
   🔗 https://github.com/google-gemini/gemini-cli/issues/21983

10. **Browser Agent 忽略 settings.json 覆盖（如 maxTurns）**（#22267，P2，3 评论）
    `AgentRegistry` 在初始化时正确合并了设置，但 Browser Agent 运行期完全不读取这些覆盖项，导致用户无法通过配置调整其行为。
    🔗 https://github.com/google-gemini/gemini-cli/issues/22267

## 重要 PR 进展

1. **修复 $VAR/${VAR} 变量展开绕过安全门**（#28902，P1，安全）
   补全 `detectBashSubstitution()` 和 `detectPowerShellSubstitution()` 的不完整检查，防止变量展开模式绕过 GHSA-wpqr-6v78-jr5g 的安全限制，并加固了自动化去重工作流。这是当前最值得关注的安全加固 PR。
   🔗 https://github.com/google-gemini/gemini-cli/pull/28902

2. **macOS Seatbelt 隔离 Docker/容器运行时资源**（#28935，已合并）
   在 Seatbelt 配置中显式拒绝访问容器运行时 daemon 的 UNIX Socket、CLI 二进制、Mach/XPC 服务及 POSIX 共享内存。对应 v0.56.0-nightly.20260822 发布。
   🔗 https://github.com/google-gemini/gemini-cli/pull/28935

3. **修复静态刷新误清终端回滚**（#28967，P2，新增）
   在非备用缓冲区模式下调用 `refreshStatic()` 时不再使用 `clearTerminal`，避免 GNOME Terminal、xterm、Alacritty 等模拟器上的滚动历史被意外清除。
   🔗 https://github.com/google-gemini/gemini-cli/pull/28967

4. **修正 excludeTools 文档（两处）**（#28966 / #28963，P1）
   文档示例中 `run_shell_command(rm -rf *)` 这类写法实际永远不会匹配——`excludeTools` 是按完整工具名精确匹配的。两个 PR 均修正文档并指向 policy 引擎做命令级拦截。
   🔗 https://github.com/google-gemini/gemini-cli/pull/28966 · https://github.com/google-gemini/gemini-cli/pull/28963

5. **修复 write policy 中安全检查器注册失败**（#28961，新增）
   将 `packages/core/src/policy/policies/write.toml` 中的安全检查器声明对齐为标准顶层 `[[safety_checker]]` 表数组，确保 `AllowedPathChecker` 能被正确注册并应用于 write_file/replace 工具。
   🔗 https://github.com/google-gemini/gemini-cli/pull/28961

6. **A2A 服务器: 修复取消后状态损坏**（#28940，large）
   修复 A2A 服务器在请求中止/取消后，后续用户提示会立即崩溃报 `Execution aborted` 的状态污染 bug，目标是彻底解决 Google Cloud Assistant 执行停止问题。
   🔗 https://github.com/google-gemini/gemini-cli/pull/28940

7. **扩展程序环境变更需用户同意 + 环境变量消毒**（#28863，medium）
   在扩展更新时，将 MCP 服务器环境配置纳入生成的同意字符串，并对自定义环境变量做消毒，防止运行时关键变量被注入到子进程。首次合入需要 issue 关联。
   🔗 https://github.com/google-gemini/gemini-cli/pull/28863

8. **A2A 服务器 501 后缺 return 导致崩溃**（#27754，P1，help wanted）
   `GET /tasks/metadata` 在返回 501 后缺少 `return`，代码继续执行导致 `ERR_HTTP_HEADERS_SENT` 崩溃，加一行即修复。
   🔗 https://github.com/google-gemini/gemini-cli/pull/27754

9. **修复 401 子串误判认证失败**（#28827，P2）
   `isAuthenticationError` 的 fallback 逻辑会错误匹配任何包含 `401` 的值（如端口号、退出码）。现在仅在消息开头或 HTTP 状态上下文位置识别 401，避免误报。
   🔗 https://github.com/google-gemini/gemini-cli/pull/28827

10. **保留工具/媒体空文本轮次**（#28892，medium，已关闭）
    优化 `isValidContent` 校验逻辑，允许模型轮次中带空 `text: ''` 但含工具请求/响应或多模态媒体的内容保留在历史中，防止上下文丢失。
    🔗 https://github.com/google-gemini/gemini-cli/pull/28892

## 功能需求趋势

- **从“上下文内任务追踪”转向持久化文件任务**：多个 issue（#18836、#21000）推动以真实文件为基础的 CRUD 任务跟踪（ToDo），替代依赖对话上下文的 `WriteToDo`，以对抗 context rot 和 token 膨胀。
- **AST 感知的代码理解**：社区期待引入 AST 感知工具（如 tilth/glyph）实现方法级精确读取和代码库映射，降低大文件读入的 token 开销并提升导航精度（#22745、#22746）。
- **更强的沙箱与安全策略**：除 macOS Seatbelt 修复外，大量 PR 针对变量展开绕过、危险 git 命令、生产资源保护等场景进行加固（#28902、#22672）；同时有人提议零依赖 OS 沙箱方案以减少对 Docker 的依赖（#19873）。
- **Auto Memory 系统精细化治理**：对低信号会话的处理、确定性脱敏、无效补丁隔离/上抛等改进被集中提出（#26522、#26523、#26525、#26516），表明记忆系统正从“能用”走向“可控、可审计”。
- **Browser Agent 的健壮性提升**：用户期望包括 Wayland 兼容、会话接管/锁 recovery、遵守 settings.json 覆盖（#21983、#22232、#22267）。

## 开发者关注点

- **Subagent 状态报告不可信**：MAX_TURNS 被打断却上报 GOAL 成功（#22323），以及 bugreport 不包含子代理内部上下文（#21763），都削弱了开发者对 Agent 系统的信任，修复优先级很高。
- **技能/子代理采用率低**：多个开发者反馈模型默认几乎不使用自定义 skills 和 sub-agents，必须显式指示，影响自动化脚本的可复用性（#21968、#21432）。
- **终端交互卡顿类问题频发**：命令执行完仍显示 “Waiting input”（#25166）、终端 resize 时闪烁与性能差（#21924）、输出 hook 导致崩溃（#22186）——这些都是高频日常使用中的痛点。
- **模型产生临时脚本/文件过多**：模型被限制 shell 后转而在多个目录生成临时脚本，造成工作区清理困难，开发者期望更可预测的写入行为（#23571）。
- **安全策略的“度”需要精细平衡**：既要防止破坏性命令（git reset、--force 等），又要避免过度限制影响效率；社区期望有更细粒度的策略配置而非一刀切（#22672、#21432）。

---
*本日报基于 GitHub 公开数据整理，数据抓取时间范围为 2026-08-22 全天。*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-08-23

## 今日速览

过去 24 小时内无新版本发布。社区最集中的诉求围绕**跨会话记忆系统**展开（#1283、#1478 持续活跃），而企业代理 SSL 证书问题（#760）已关闭。PR 方面，一个修复文件编辑时非 UTF-8 字节损坏的关键补丁（#2594）已被合并。

## 社区热点 Issues

过去 24 小时内共有 3 条 Issue 更新（均为老 issue 的近期活跃）：

### 1. #1283 功能请求：记忆系统（跨会话持久上下文）— OPEN
- **作者**：@CatKang | **创建**：2026-02-27 | **更新**：2026-08-22 | **评论**：40 | 👍：0
- **摘要**：请求实现综合性的 **Memory System**，让 Kimi Code CLI 跨会话记住项目上下文、代码模式与用户偏好，包括 AI 自动管理的笔记和用户手动定义的指令。
- **分析**：40 条评论表明该需求在社区中呼声极高，且已持续活跃近半年。这是当前 CLI 编码工具的核心竞争点，直接影响 Agent 在大型项目中的可用性。
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1283

### 2. #1478 能否优化记忆层？参考文档中未提及相关实现 — OPEN
- **作者**：@hahy36 | **创建**：2026-03-17 | **更新**：2026-08-22 | **评论**：3 | 👍：0
- **摘要**：开发者反映在大型项目中因缺少记忆层而“很痛苦”，且参考文档中仅见 `agent.md`，未提及记忆机制。同时引用了 `~/.openclaw/workspace/` 下的 `SOUL.md`、`USER.md`、`MEMORY.md` 等文件结构作为替代方案参考。
- **分析**：与 #1283 形成互补，不仅指出问题，还提供了具体的业界参考实现。文档缺失与功能缺失同时被提上议程。
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1478

### 3. #760 企业代理（Zscaler）下 SSL 证书验证失败 — CLOSED
- **作者**：@aaraujodata | **创建**：2026-01-28 | **更新**：2026-08-22 | **评论**：3 | 👍：0
- **摘要**：在 Zscaler 等企业代理后运行 `/login` 命令时，因 `[SSL: CERTIFICATE_VERIFY_FAILED]` 无法获取本地证书链导致登录失败。
- **分析**：该问题已关闭，意味着解决方案或替代配置已落地。企业网络兼容性是 CLI 工具进入大型组织的必备条件，值得关注其修复方式。
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/760

## 重要 PR 进展

过去 24 小时内共有 2 条 PR 更新：

### 1. #2614 文档：插件安全与持久化数据说明 — OPEN
- **作者**：@QIANLING-0831 | **创建**：2026-08-20 | **更新**：2026-08-22
- **摘要**：纯文档更新，澄清插件契约范围：根目录 `plugin.json`、基于命令的工具、`inject` 机制，以及安装路径 `~/.kimi/plugins/`。不涉及独立插件的行为描述或变更。
- **意义**：为插件开发者建立安全边界共识，明确哪些数据可被插件持久化，降低生态滥用风险。
- 链接：https://github.com/MoonshotAI/kimi-cli/pull/2614

### 2. #2594 修复：StrReplaceFile 编辑时保留非 UTF-8 字节 — CLOSED
- **作者**：@686f6c61 | **创建**：2026-08-06 | **更新**：2026-08-22
- **摘要**：修复 `StrReplaceFile` 用 `errors="replace"` 解码整个

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-08-23）

## 今日速览

今日发布正式版 v0.22.0，重点修复 Web Shell 在大转录场景下的 OOM 崩溃。审查工作流继续成为迭代核心：新版本让 Review 循环在不稳定时引用具体文件，同时社区围绕“代理运行时可信边界”的讨论热度最高（#8102，17 条评论），安全与权限控制成为当前最受关注的主题。此外，多个与会话恢复相关的 Bug 集中浮出水面，提示会话管理健壮性仍是用户痛点。

---

## 版本发布

### [v0.22.0](https://github.com/QwenLM/qwen-code/releases/tag/v0.22.0)
- **Web Shell 防 OOM**：通过限制转录保留量并修剪过大的重放，避免长时间运行导致内存溢出（[#9303](https://github.com/QwenLM/qwen-code/pull/9303)）。
- **Review 循环可解释性**：在审查不稳定时，现在会引用具体文件以及反复出现的 finding，帮助作者理解问题根因。

### v0.21.14-nightly.20260822.7a4566cb3b
- feat(review)：告诉作者 Review 循环无法收敛的原因（[#9461](https://github.com/QwenLM/qwen-code/pull/9461)）。
- fix(ci)：修复 fallback 流程相关 CI 问题。

---

## 社区热点 Issues（精选 10 条）

### 1. 确定性工具执行边界：可信代理运行时提案（#8102）
**标签**：P3 / feature-request / core / security  
**评论**：17 | **[链接](https://github.com/QwenLM/qwen-code/issues/8102)**

> 提案核心：将 LLM 排除在信任边界之外，让运行时能确定性地约束、授权、观察和评估模型产生的动作。这是当前社区讨论最激烈的话题，17 条评论说明开发者对 Agent 安全运行的关注度很高。

### 2. /review 发布时收敛建议：遥测、诊断与发布面（#9278）
**标签**：P2 / in-progress / design  
**评论**：9 | **[链接](https://github.com/QwenLM/qwen-code/issues/9278)**

> 设计文档详细分析了“评审→修复→引入新缺陷→更大 diff”的失控回路，并提出发布时收敛建议的完整方案。Review 工作流正在向高度指标化、可量化的方向演进。

### 3. 审查流水线是否应继续以调用者身份执行代码？（#9556）
**标签**：security / ci-cd / need-discussion  
**评论**：8 | **[链接](https://github.com/QwenLM/qwen-code/issues/9556)**

> 多次 Review 轮次的未解决 finding 都指向同一个前提：代码以审查者身份在工作树中执行。该问题质疑这一权限模型是否正确，是安全相关的关键讨论。

### 4. OOM 问题：1T 内存服务器仍崩溃（#9198）
**标签**：P2 / bug / performance / memory-usage  
**评论**：5 | **[链接](https://github.com/QwenLM/qwen-code/issues/9198)**

> 用户反馈：连续运行一周多后 OOM，即使服务器有 1T 内存也未能幸免。伴随会话崩溃，tmux 按键错乱。与今日发布的 Web Shell OOM 修复直接相关，但问题可能超出 Web Shell 范围。

### 5. 循环检测误报：验证循环导致无人值守回合不可恢复（#9733）
**标签**：P2 / bug / core  
**评论**：4 | **[链接](https://github.com/QwenLM/qwen-code/issues/9733)**

> 在长时间脚本化自动化运行中，循环检测对“写脚本→运行→编辑→重跑验证”这类合法序列误报并终止回合，且终止后无法无人值守恢复。这对 Agent 自主运行场景是严重阻塞。

### 6. CI 依赖 CVE 审计全面失败（#9699）
**标签**：P1 / bug / security / ci-cd / ready-for-human  
**评论**：4 | **[链接](https://github.com/QwenLM/qwen-code/issues/9699)**

> 自 2026-08-21 起，所有 PR 的 `npm audit` 步骤均失败，报告 8 个漏洞（1 高、6 中、1 低）。虽然不直接阻塞合并，但已污染所有 PR 的 CI 信号。

### 7. 自动会话标题逐字回显系统提示示例（#9706）
**标签**：P2 / bug / session-management  
**评论**：4 | **[链接](https://github.com/QwenLM/qwen-code/issues/9706)**

> 自动生成的会话标题会直接回显提示词模板里的示例字面量：“Fix login button on mobile”。已在多个不相关会话中复现，影响用户体验与后续检索。

### 8. 恢复会话显示“Tool result missing from saved history”（#9573）
**标签**：P1 / bug / session-management / need-retesting  
**评论**：4 | **[链接](https://github.com/QwenLM/qwen-code/issues/9573)**

> 恢复会话后，本应正常完成的工具调用被标记为失败，显示占位符。这直接影响会话恢复的可信度，是 P1 级 Bug。

### 9. Node REPL：以独立 MCP server 交付（#9333）
**标签**：P2 / feature-request / core / tools / status/ready-for-human  
**评论**：3 | **[链接](https://github.com/QwenLM/qwen-code/issues/9333)**

> 重要形态变更：持久化 Node REPL 不再作为内置 core 工具，而是交付为独立 MCP server（`@qwen-code/node-repl-mcp`），通过 stdio 暴露工具。这是路线图第三阶段的前置依赖。

### 10. Computer Use Skill 实现（#9335）
**标签**：P2 / feature-request / computer-use / ready-for-human  
**评论**：3 | **[链接](https://github.com/QwenLM/qwen-code/issues/9335)**

> 基于 #9333 的 Node REPL 调用 Computer Use SDK，并用确定性测试和模型在环基准验证。代表了 Qwen Code 向“模型自主操作计算机”方向迈进的意图。

---

## 重要 PR 进展（精选 10 条）

### 1. 在容器中执行被审查仓库的命令（#9723）
**[链接](https://github.com/QwenLM/qwen-code/pull/9723)**

> 直接响应 #9556：将审查过程中对“被审查仓库自身命令”的执行放入容器边界，并把该策略交给操作者配置而非由环境决定。安全模型的重大变更。

### 2. VS Code 配套采用 WebShell 转录作为默认时间线（#9719）
**[链接](https://github.com/QwenLM/qwen-code/pull/9719)**

> 将共享 WebShell 转录渲染器作为 VS Code 配套的对话时间线。原始 ACP session/update 通知经 SDK 转录 reducer 桥接，使配套扩展获得与 Web Shell 一致的转录体验。

### 3. CLI utils 叶子层依赖方向强制（#9737）
**[链接](https://github.com/QwenLM/qwen-code/pull/9737)**

> 让 `packages/cli/src/utils/` 成为真正的叶子层：此前该目录被所有 CLI 目录依赖，却反向导入 `config`、`ui`、`i18n` 等。本次用机制强制修正依赖方向，是 #9146 的 CLI 部分。

### 4. 降级平衡的内联思考块而非使回合失败（#9607）
**[链接](https://github.com/QwenLM/qwen-code/pull/9607)**

> 针对

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*