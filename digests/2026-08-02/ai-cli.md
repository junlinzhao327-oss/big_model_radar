# AI CLI 工具社区动态日报 2026-08-02

> 生成时间: 2026-08-01 23:15 UTC | 覆盖工具: 7 个

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

# Claude Code Skills 社区热点报告（数据截止 2026-08-02）

## 1. 热门 Skills 排行

按社区关注度（评论/讨论活跃度）排序，以下 8 个 PR 最受关注。

| Skill PR | 功能 | 社区讨论热点 | 状态 |
|---------|------|-------------|------|
| [fix(skill-creator): run_eval.py 0% recall bug](https://github.com/anthropics/skills/pull/1298) | 修复 `run_eval.py` 对所有技能描述均报告 0% recall 的严重问题，涉及 Windows 流读取、触发检测和并行 worker | 该问题被多个 issue 引用（#556、#1169），10+ 独立复现，直接导致描述优化循环在噪声上运行；是当前生态最大痛点 | Open |
| [Add document-typography skill](https://github.com/anthropics/skills/pull/514) | 对 AI 生成文档做排版质量控制：孤词换行、段落孤儿、编号错位 | 用户极少主动要求排版，但影响所有 Claude 生成文档；讨论焦点是技能触发时机与是否应默认启用 | Open |
| [fix(pdf): 大小写敏感文件引用](https://github.com/anthropics/skills/pull/538) | 修复 PDF skill 中 `REFERENCE.md` 与 `reference.md` 等 8 处大小写不一致 | 在大小写敏感文件系统（Linux/macOS）上会直接导致 skill 资源加载失败；属于高影响低风险修复 | Open |
| [Add ODT skill](https://github.com/anthropics/skills/pull/486) | 支持创建、填充、读取 OpenDocument 格式（.odt/.ods），并可转换 HTML | 填补了官方文档技能中缺失的 ISO 标准办公格式支持；讨论涉及 LibreOffice 兼容性 | Open |
| [Improve frontend-design skill](https://github.com/anthropics/skills/pull/210) | 重写 `frontend-design` 技能，提升指令可操作性和内部一致性 | 核心争论：技能应像“开发者文档”还是“操作指令清单”；评论普遍认为现有版本太抽象，需要更具体的单轮可执行指导 | Open |
| [Add testing-patterns skill](https://github.com/anthropics/skills/pull/723) | 覆盖完整测试栈：测试哲学、单元测试、React 组件测试、命名约定、边界用例 | 社区对“什么时候不测试”的 Trophy 模型讨论热烈；被认为是目前最全面的测试类技能提案 | Open |
| [Add pyxel skill for retro game development](https://github.com/anthropics/skills/pull/525) | 为 Pyxel 复古游戏引擎和 pyxel-mcp 提供技能，涵盖“编写→运行→捕获→迭代”工作流 | 代表垂直领域 MCP 与 Skills 结合的方向；作者为 Pyxel/MCP 官方开发者，可信度高 | Open |
| [Add color-expert skill](https://github.com/anthropics/skills/pull/1302) | 自包含的颜色专业知识：命名系统（ISCC-NBS、Munsell、RAL）、色彩空间选型（OKLCH/OKLAB/CAM16） | 填补了设计类技能中缺少专业颜色知识的空白；讨论侧重于色彩空间选择的准确性和可维护性 | Open |

> 注：多个 skill-creator 修复 PR（#1099、#1050、#1323、#1261）与 #1298 形成同一热点群，均围绕 Windows 兼容性和触发检测准确率问题，属生态基础设施的集中关注区。

## 2. 社区需求趋势

从 Issues 中可提炼出以下最强烈的需求信号：

- **安全与信任治理**：issue #492（43 评论）指出社区技能被放在 `anthropic/` 命名空间下，造成信任边界滥用风险，用户可能对非官方技能授予过高权限——这是目前影响面最大的治理议题。
- **组织级技能共享**：#228（16 评论）要求支持在组织内直接共享技能库/链接，而不是手动下载、发送、再上传；企业采用的关键阻碍。
- **工具链可靠性**：#556（12 评论）与 #1169 共同指向 `run_eval.py` 触发率恒为 0% 的致命 bug；另有 #1061 汇总 Windows 上的 PATHEXT、编码、select-on-pipes 三类兼容性问题。
- **新技能方向**：#1329（9 评论）提出 `compact-memory` 符号化记忆技能，减少长任务 agent 的上下文开销；#412 提出 `agent-governance`，关注 AI agent 系统的安全治理模式。
- **资源效率**：#1487 报告 `claude-api` 技能一次性注入约 156k tokens，耗尽上下文窗口——社区开始关注“技能体积”对 context 的占用。
- **平台互通**：#29（Bedrock 支持）、#16（将 Skills 暴露为 MCP）显示了跨平台/协议集成的长期需求。

## 3. 高潜力待合并 Skills

以下 PR 评论活跃、尚未合并，但具备近期落地的高可能性：

- [run_eval.py 0% recall 修复](https://github.com/anthropics/skills/pull/1298) — 修复核心工具链致命 bug，多个独立 PR 针对同一问题，且官方已知晓（#556），一旦修正验证通过，合并优先级极高。
- [document-typography](https://github.com/anthropics/skills/pull/514) — 简单实用，影响所有文档类生成，争议小，只需解决触发机制即可推进。
- [testing-patterns](https://github.com/anthropics/skills/pull/723) — 覆盖面广、内容成熟，若能通过瘦身/模块化审查，很可能作为官方 examples 合入。
- [color-expert](https://github.com/anthropics/skills/pull/1302) — 专业性强且自包含，与前端设计等技能协同潜力大；作者维护活跃，吸收反馈后有望合入。
- [self-audit v1.3.0](https://github.com/anthropics/skills/pull/1367) — 面向交付质量的机械验证+四维推理审计，契合社区对 agent 输出可靠性的普遍关注；上线时间较短但迭代快。
- [plan-file-hygiene](https://github.com/anthropics/skills/pull/1479) — 解决 plan 文件生命周期混乱问题，议题 #1417 得到社区认可，属于“小而美”的治理型技能。

## 4. 生态洞察

一句话总结：当前社区最集中的诉求是**修复 skill-creator 工具链本身的可靠性（Windows 兼容、触发评估准确性）**，同时围绕**安全信任边界、组织内共享和上下文效率**建立更成熟的治理机制——说明 Skills 生态正从“收集更多技能”转向“把技能基础设施做扎实”。

---

# Claude Code 社区动态日报 2026-08-02

**数据统计周期**：2026-08-01 至 2026-08-02（GitHub anthropics/claude-code）

## 今日速览

过去 24 小时无新版本发布，但社区围绕认证流程、模型行为可靠性与后台 Agent 任务交付展开激烈讨论。最受关注的 OAuth 登录循环问题（#77966）已有 19 条评论；此外，新的 Claude Max 配额消耗异常报告（#83205）刚提交即获关注，可能与近期服务端限流策略调整有关。

---

## 社区热点 Issues（Top 10）

### 1. OAuth 登录循环：state 参数在重定向后被丢弃
**#77966** · [OPEN] · 评论 19 · 👍 13
> **平台：** Linux / IntelliJ · **标签：** auth
> 用户在 `sign in again to continue` 重定向后，OAuth 流程反复循环，state 参数丢失导致始终无法完成认证。
>
> **社区反应：** 当前评论数最高的 issue，同时影响多个平台，认证链路存在通用性缺陷。
>
> [查看 Issue](https://github.com/anthropics/claude-code/issues/77966)

### 2. Opus 4.8 虚构用户请求并坚持错误任务上下文
**#64260** · [CLOSED] · 评论 13
> **平台：** macOS · **标签：** model
> 模型在无对应输入的情况下，虚构了一条"现在时态"的用户请求，并在整个会话中持续坚持该不存在的任务上下文，属于典型的模型自主行为（autonomous behavior）异常。
>
> **社区反应：** 虽已关闭，但 13 条评论说明开发者对模型"幻觉意图"的高度警惕。
>
> [查看 Issue](https://github.com/anthropics/claude-code/issues/64260)

### 3. 后台 Agent 频繁空闲，不投递最终 SendMessage 报告
**#74113** · [OPEN] · 评论 6 · 👍 5
> **平台：** Windows · **标签：** agents
> 后台 Agent 在完成工作后经常进入空闲状态，最终报告（SendMessage）丢失，需要重新 ping 才能恢复。问题影响自动化流程的可靠性。
>
> **社区反应：** 获得 5 个 👍，Windows 用户受影响明显。
>
> [查看 Issue](https://github.com/anthropics/claude-code/issues/74113)

### 4. Desktop + Bedrock：Haiku 4.5 被发送为裸模型 ID 而非 inference profile
**#65208** · [CLOSED] · 评论 6 · 👍 1
> **平台：** macOS · **标签：** bedrock / cowork / desktop
> 在 Scheduled Task 后续请求中，模型 ID 未被正确映射为 Bedrock inference profile，导致间歇性 400 "invalid model identifier"错误。
>
> **社区反应：** 企业级 Bedrock 用户关注，API 兼容层仍需修正。
>
> [查看 Issue](https://github.com/anthropics/claude-code/issues/65208)

### 5. macOS 桌面应用崩溃循环：CCD bundle 截断 + 渲染器 OOM
**#65624** · [CLOSED] · 评论 5
> **平台：** macOS（Tahoe 26.5.1, arm64）
> 桌面应用在安装时 CCD bundle 仅被截断写入 172MB（预期完整包），随后渲染器在 `/epitaxy` 路由上 OOM，形成启动死循环。
>
> **社区反应：** 安装器与渲染器双重缺陷叠加，属于高危稳定性问题。
>
> [查看 Issue](https://github.com/anthropics/claude-code/issues/65624)

### 6. Worktree 操作默认落在 main 分支而非 worktree 分支
**#66442** · [CLOSED] · 评论 4 · 👍 4
> **平台：** macOS
> 通过 `claude -w` 打开 worktree 后，Claude 仍默认在 main 分支上执行操作，用户必须显式指示才会切换到 worktree 分支，极易造成误提交。
>
> **社区反应：** 获得 4 个 👍，Git 工作流用户反馈强烈。
>
> [查看 Issue](https://github.com/anthropics/claude-code/issues/66442)

### 7. Ultra 工作流自动扩展约 130 个 Agent，触发限流与 IP 封禁
**#69635** · [CLOSED] · 评论 4
> **平台：** macOS · **标签：** cost / agents
> 用户为发起 `/code-review ultra`，Claude 自动扩展了约 130 个子 Agent，远超预期，直接触发服务端 Rate Limit 和 IP Block，造成不可控成本消耗。
>
> **社区反应：** 与成本控制议题高度相关，开发者对自动化扩缩容边界表示担忧。
>
> [查看 Issue](https://github.com/anthropics/claude-code/issues/69635)

### 8. 限流错误导致配额消耗异常跳跃 20%
**#65397** · [CLOSED] · 评论 4
> **平台：** macOS · **标签：** cost / api
> 用户报告：在 3 个 CLI 会话中正常使用时，周配额几乎不动；但一旦遇到 `Server is temporarily limiting requests` 错误，周配额瞬间跳升约 20%。限流本身反而造成了更大的配额消耗。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-02

## 1. 今日速览

今日无新版本发布，社区讨论焦点集中在 GPT-5.6 Sol 的 subagent 模型强制配置问题（#31814，167 👍 / 100 评论）以及 Codex Diff 在 macOS 和 Windows 上均出现的崩溃问题。Windows 平台稳定性（安装失败、进程风暴、sandbox 错误）持续占据大量反馈，同时多智能体 V2 引发的会话数据膨胀（超 100 GiB）成为新的存储隐患。

## 2. 版本发布

过去 24 小时无新的 Codex 版本发布。

## 3. 社区热点 Issues

精选 10 个社区关注度最高或影响最严重的 Issue：

**① GPT-5.6 Sol 无法指定 subagent 模型，强制所有 subagent 均为 Sol 实例**
- [#31814](https://github.com/openai/codex/issues/31814) · CLOSED · 💬 100 · 👍 167
- 模型元数据中 `multi_agent_version = "v2"` 绕过了 `multi_agent_v2` 功能开关，且 `hide_spawn_agent_metadata` 默认值为 `true`，导致用户无法为子代理指定其他模型。这是本月社区共鸣最强烈的配置问题，影响 MultiAgent V2 的灵活使用。

**② Codex Diff 在 macOS VS Code 中崩溃（“Oops, an error has occurred”）**
- [#35058](https://github.com/openai/codex/issues/35058) · OPEN · 💬 44 · 👍 111
- 在任何仓库（包括全新工作区）中打开 Codex Diff 标签页都会报错，环境为 macOS Apple Silicon + VS Code 1.128.0。同类型问题在 Windows 上也有报告（#35481、#36016），Diff 视图故障已成为当前扩展端最普遍的阻断性问题。

**③ VS Code 扩展长时间运行后界面变灰**
- [#8197](https://github.com/openai/codex/issues/8197) · CLOSED · 💬 55 · 👍 19
- 扩展版本 0.5.52，长时间运行后 Codex 面板完全变灰无法交互。该问题跨度较长、影响面广，虽已关闭，但开发者反映的“长任务后 UI 白屏/灰屏”在桌面 App 端仍有再现（#27192）。

**④ Windows 桌面版产生数百个 taskkill/conhost 进程，引发 WMI 风暴和 DWM 降级**
- [#

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-02

## 今日速览

昨日发布 v0.55.0-nightly.20260801.gf47d6c6f7，修复了容量耗尽导致的无限重试和空响应错误信息传播问题。社区讨论热度集中在 subagent 状态误报（MAX_TURNS 被报告为成功）、generalist agent 挂起以及 shell 命令执行后卡死等可靠性问题上；此外一条由 v0.53.0 引入的 `thought_signature` 回归修复 PR 正在推动中。

## 版本发布

**v0.55.0-nightly.20260801.gf47d6c6f7** [查看发布说明](https://github.com/google-gemini/gemini-cli/releases)

- **fix(core)**：将容量耗尽（capacity exhaustion）分类为终止状态，避免重试挂起（[#28599](https://github.com/google-gemini/gemini-cli/pull/28599)）
- **fix(core,cli)**：将 `InvalidStreamError` 的细节传播到 UI，为特定空响应提供明确指引（[#28611](https://github.com/google-gemini/gemini-cli/pull/28611)）

## 社区热点 Issues

### 1. Subagent 在 MAX_TURNS 后被误报为 GOAL 成功（#22323）
[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) · 评论 12 · 👍 2 · P1

`codebase_investigator` 在达到最大轮次后，其自身结果明确显示分析未完成，但最终状态却报告为 `success` / `GOAL`，导致中断被掩盖。该问题直接影响依赖 subagent 结果的自动化流程可信度，社区讨论了多次仍复现。

### 2. Generalist agent 无限期挂起（#21409）
[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) · 评论 8 · 👍 8 · P1

`gemini-cli` 委派给 generalist agent 时无限期挂起，简单操作（如创建文件夹）也会卡住。用户反馈等待一小时后只能手动取消，通过指示模型不要委派给 subagent 可绕开，说明问题出在委派链路本身。

### 3. Shell 命令执行完成后卡在 "Waiting input"（#25166）
[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) · 评论 4 · 👍 3 · P1

在简单 CLI 命令已执行完毕后，UI 仍显示命令活跃并等待用户输入。该问题高频复现，严重干扰日常交互式工作流。

### 4. Browser subagent 在 Wayland 下失败（#21983）
[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) · 评论 4 · 👍 1 · P1

在 Wayland 会话中 `browser_agent` 以 `GOAL` 终止，但实际任务并未完成。Wayland 是主流 Linux 桌面环境，该兼容性问题影响面较大。

### 5. (Sub)agents 自 v0.33.0 起在未授权情况下运行（#22093）
[#22093](https://github.com/google-gemini/gemini-cli/issues/22093) · 评论 3 · P1

用户自动升级到 v0.33.0 后，尽管配置中禁用了 agents，subagent 仍被自动调用。该问题涉及权限边界，与用户对安全性的预期直接冲突。

### 6. 动态内存系统：低信号会话无限重试（#26522）
[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) · 评论 5 · P2

Auto Memory 仅在提取代理成功读取会话后才标记为已处理，低信号会话因跳过读取而反复出现，导致后台任务效率下降。属于内存管道长期存在的设计缺陷。

### 7. Gemini 不会主动使用 custom skills 和 sub-agents（#21968）
[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) · 评论 6 · P2

尽管配置了 `gradle`、`git` 等技能，模型在相关任务中几乎不会自行调用，必须显式指令。这削弱了扩展机制的实际价值。

### 8. 超过 128 个工具时返回 400 错误（#24246）
[#24246](https://github.com/google-gemini/gemini-cli/issues/24246) · 评论 3 · P2

启用大量工具后 API 报 400。社区期望模型能按需动态收窄工具范围，而不是一次性携带全部工具，直接影响了大规模 MCP/工具集场景。

### 9. 内存系统补丁质量与日志问题（#26525）
[#26525](https://github.com/google-gemini/gemini-cli/issues/26525) · 评论 4 · P2

Auto Memory 在将本地转录发送给模型前未能确定性脱敏，且存在过量日志。涉及用户隐私数据流出至模型上下文的风险，社区关注度高。

### 10. `formatTruncatedToolOutput` 负值 bug（#28620）
[#28620](https://github.com/google-gemini/gemini-cli/issues/28620) · 评论 1 · 新

`maxChars` 非正时函数缺少防护，输出被异常放大约 2 倍。属于新发现的边界条件 bug，问题定位清晰、修复成本低。

---

## 重要 PR 进展

### 1. 修复 env 加载时序：设置占位符解析前先加载环境变量（#28597）
[#28597](https://github.com/google-gemini/gemini-cli/pull/28597) · size/l · 2026-07-30 更新

在 settings 生命周期中，原先系统/用户/工作区设置被立即展开并校验，导致 `.env` 中定义的变量无法在占位符解析时被正确引用。该 PR 将环境变量加载前置，修复配置展开的竞态条件。

### 2. 修复 v0.53.0 回归：保留 functionCall 的 `thoughtSignature`（#28607）
[#28607](https://github.com/google-gemini/gemini-cli/pull/28607) · area/agent · 2026-07-31 更新

#28509 引入的 `stripThoughts()` 会在剪裁上下文时移除 `thought_signature`，导致 `API Error 400: Function call is missing a thought_signature`。该修复在剥离 thought parts 时保留签名，是当前最紧迫的回归修复之一。

### 3. 修复 VS Code IDE Companion 资源泄漏（#28526）
[#28526](https://github.com/google-gemini/gemini-cli/pull/28526) · P2 · size/s · 2026-07-24 更新

`activate()` 中括号错位导致 `gemini.diff.accept` 命令和 `onDidChangeWorkspaceFolders` 的 Disposable 未被正确注册，造成事件监听器持续泄漏。该 PR 修复了默认 IDE 集成中的资源管理缺陷。

### 4. 新增 daemon 模式（#21307）
[#21307](https://github.com/google-gemini/gemini-cli/pull/21307) · P2 · area/non-interactive · help wanted · 2026-03-05 更新

为 Unix-like 工具生态新增 daemon 模式与轻量客户端，以支持 shell 工作流和跨会话上下文保留。该 PR 已持续数月，仍在推进中，代表社区对无头模式的需求。

### 5. 将 console.error 替换为 debugLogger（#28613）
[#28613](https://github.com/google-gemini/gemini-cli/pull/28613) · size/xs · 2026-08-01

SDK session 中直接调用 `console.error`，改为项目标准的 `debugLogger`，并移除多余的 ESLint 禁用指令。低风险代码卫生改进。

### 6. 更新 .gitignore 以忽略 .env 和 .ai 文件（#28619）
[#28619](https://github.com/google-gemini/gemini-cli/pull/28619) · P1 · size/m · 2026-08-01

新增对 `.env` 和 `.ai` 文件的忽略规则并补充单元测试，降低敏感配置和 AI 生成文件被误提交的风险。

### 7. 增加 fork 仓库 workflow 审批文档（#28618）
[#28618](https://github.com/google-gemini/gemini-cli/pull/28618) · P1 · size/s · 2026-08-01

补充维护者如何审查和批准来自 fork 的 PR 触发的 workflow 运行，改善外部贡献者的协作流程透明度。

### 8. 连接 GitHub 仓库到 GCP 项目的脚本（#28617）
[#28617](https://github.com/google-gemini/gemini-cli/pull/28617) · P1 · size/s · 2026-08-01

利用 Google Cloud DevTools API 编写脚本，将 GitHub 仓库关联至 GCP 项目，面向基础设施自动化的工具补充。

### 9. 版本提升至 0.55.0-nightly.20260801（#28612）
[#28612](https://github.com/google-gemini/gemini-cli/pull/28612) · size/s · 2026-08-01

按惯例由机器人提交的 nightly 版本号更新。

### 10. Codespace 待处理变更导出（#28616）
[#28616](https://github.com/google-gemini/gemini-cli/pull/28616) · P1 · size/xs · 2026-08-01

由开发者从 Codespace 自动导出的变更，内容待补充，暂无明显功能意义，仅记录社区活跃状态。

---

## 功能需求趋势

- **AI/Agent 评估体系建设**：`Epic #24353`（组件级评估）已有 76 个 behavioral 测试，社区正推动对 6 个支持模型的系统性评估，表明项目从“可用”走向“可验证”阶段。
- **AST 感知的代码库操作**：`Epic #22745` 和 #22746 探索 AST 感知的文件读取/搜索/代码库映射，期望减少 token 消耗、精确定位方法边界。
- **Agent 自我认知与行为控制**：#21432（正确了解自身 CLI 参数/热键）、#22672（阻止破坏性命令如 `git reset`/

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-08-02）

## 今日速览

- 发布 v1.0.78-2，主要优化 Split-view 关闭交互，并修复扩展斜杠命令处理器被多次执行的问题。
- 社区议题集中在 **BYOK 多模型支持**、**大型会话恢复/内存问题** 和 **MCP 服务器懒加载** 上，均获得较高关注。
- 过去 24 小时没有任何 PR 更新，暂无合并/审查进展可汇总。

---

## 版本发布

### v1.0.78-2

- **Improved**
  - Split-view 侧边栏的红色关闭确认文案调整：现在显示 `x again to close`（最后一个会话显示 `x again to exit CLI`），更清楚地提示用户再次按 `x` 才会关闭。
- **Fixed**
  - 扩展斜杠命令在“多个扩展同时存在”的场景下，每个调用只执行一次 handler。原文描述因数据截断未完整显示，核心是修复重复执行问题。

🔗 [GitHub Releases](https://github.com/github/copilot-cli/releases)

---

## 社区热点 Issues

### 1. 支持在 Copilot CLI 中配置多个 BYOK 模型  
**#3282** `[area:models, area:configuration]`  
目前只能通过环境变量配置一个 BYOK 模型，且 TUI 内无法切换模型，用户必须结束会话并重设环境变量。该 Issue 已获得 **19 👍 / 6 评论**，是当前最受关注的功能需求之一。  
🔗 https://github.com/github/copilot-cli/issues/3282

### 2. 自定义 Agent Frontmatter 应支持 Reasoning Effort  
**#2904** `[area:agents, area:models]`  
`.agent.md` 自定义 agent 支持固定 `model`，但无法单独设置 reasoning effort，只能依赖全局 `--effort` 参数。对需要按 agent 精细控制模型推理成本/质量的团队非常重要。获 **16 👍**。  
🔗 https://github.com/github/copilot-cli/issues/2904

### 3. MCP 服务器应支持首次调用时懒加载  
**#2901** `[area:mcp]`  
目前所有 MCP 服务器在 CLI 启动时全部连接，MCP 配置越多启动越慢。社区希望改为“第一次使用某工具时才启动对应服务器”。获 **14 👍**，反映 MCP 重度用户的普遍痛点。  
🔗 https://github.com/github/copilot-cli/issues/2901

### 4. 升级到 1.0.76 后出现 Rust 类型转换崩溃  
**#4305** `[closed]`  
用户升级到 1.0.76 后，几乎任何命令都会报错：`Failed to convert JavaScript value 'Undefined' into rust type 'String'`。虽是 closed，但评论数较多，说明该回归影响了较多用户。  
🔗 https://github.com/github/copilot-cli/issues/4305

### 5. `events.jsonl` 超过 V8 最大字符串长度后会话永久无法恢复  
**#4325** `[area:sessions]`  
长生命周期会话的 `events.jsonl` 增长到一定大小后，CLI 无法再恢复该会话。文件本身没有损坏，但会话不可恢复，属于严重数据可用性问题。  
🔗 https://github.com/github/copilot-cli/issues/4325

### 6. 恢复大型会话时 OOM / 单核 CPU 100% 约 70 分钟  
**#4251** `[area:sessions]`  
A/B 验证显示这是 1.0.74 引入的回归：恢复同一个大会话时，内存约为 1.0.73 的 **3–4 倍**，并导致长时间 CPU 占用。对长期积累会话的重度用户影响很大。  
🔗 https://github.com/github/copilot-cli/issues/4251

### 7. BYOK Responses 流式接口会丢失 `apply_patch` 输入  
**#4327** `[area:models, area:tools]`  
使用 OpenAI-compatible 的 BYOK provider 且 `wireApi: "responses"` 时，模型

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>



</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 · 2026-08-02

数据来源：github.com/anomalyco/opencode

---

## 今日速览

OpenCode 发布 v1.18.11 补丁，修复了 MCP 连接重连循环与推理字段解析问题，同时桌面端外部链接不再被内置拦截。社区层面，围绕「遗留布局去留」「免费额度耗尽」「隐私政策与模型托管透明度」的讨论最为激烈，多个涉及用户控制权与数据主权的 Issue 获得高赞。PR 侧则进入自动化清理期，一批功能型 PR 被关闭，但新提交的核心修复（如 OIDC 格式处理、权限提示清除）仍保持活跃。

---

## 版本发布

### v1.18.11（2026-08-02 发布）

**Core 修复**

- 修复 MCP SSE 连接在服务器返回错误响应后陷入无限重连循环的问题。
- 修复使用交错式思考字段（如 `reasoning_text` 或自定义字段名）的 provider 模型配置解析异常。

**Desktop 修复**

- 外部链接现在改为在系统浏览器中打开，不再被应用内置逻辑拦截。

---

## 社区热点 Issues

### 1. #37012 保留遗留布局选项（Legacy Layout）
- **作者**: @darkine24th
- **评论**: 34 | **👍**: 37
- **状态**: OPEN

老用户对新版 UI 的导航成本提出强烈异议，认为旧布局可在一个主窗口内访问所有功能、支持工作区，而新版本需要层层跳转。这是当前社区反映最集中的 UI 回归问题。

> https://github.com/anomalyco/opencode/issues/37012

### 2. #38801 “exiting loop” 消息导致 TUI 不可用
- **作者**: @josephtingiris
- **评论**: 21 | **👍**: 0
- **状态**: OPEN

用户反馈每当打开 TUI 就被 “exiting loop” 消息打断，尝试设置 `step=80` 等参数仍无法避免。涉及多种 OpenAI 兼容 API，属于影响日常使用的核心稳定性问题。

> https://github.com/anomalyco/opencode/issues/38801

### 3. #33028 子代理在快速 bash 工具调用后无限挂起
- **作者**: @simoesleandro
- **评论**: 8 | **👍**: 5
- **状态**: OPEN

主代理与子代理在执行快速 bash 工具调用后的下一次 LLM 流式请求永远不完成、不超时，只能手动 Esc 或杀进程。已在 `glm-5.2` 和 `minimax-m3` 两个模型上复现，指向流式连接管理缺陷。

> https://github.com/anomalyco/opencode/issues/33028

### 4. #23595 `<system-reminder>` 位置漂移导致缓存失效
- **作者**: @jacekpoplawski
- **评论**: 6 | **👍**: 11
- **状态**: OPEN

`<system-reminder>` 在 prompt 中被反复移动，导致 llama.cpp 的 prompt cache 无法命中，带来大量不必要的重处理时间。社区建议固定 system-reminder 的位置以提升推理性能。

> https://github.com/anomalyco/opencode/issues/23595

### 5. #39875 撤销隐私措辞与 provider 归属删除，且 telemetry 未纳入隐私政策
- **作者**: @Levosilimo
- **评论**: 5 | **👍**: 34
- **状态**: OPEN

Go 订阅用户指出近两周有两次 commit 移除了隐私/数据用途相关的说明文字，且要求补充 telemetry 与数据留存声明。该 Issue 关联了 5 个此前的相关请求，是当前社区对透明度关注度最高的一条。

> https://github.com/anomalyco/opencode/issues/39875

### 6. #39847 模型托管位置需要透明化
- **作者**: @christianhelle
- **评论**: 5 | **👍**: 17
- **状态**: OPEN

用户因官方宣传的 EU 托管模型而付费订阅，但 DeepSeek V4 突然停止工作且无迁移说明。社区要求明确每个模型的实际托管地区，以及服务变更时的通知机制。

> https://github.com/anomalyco/opencode/issues/39847

### 7. #40078 免费额度耗尽提示：Bug 还是条款变更？
- **作者**: @mike2003
- **评论**: 3 | **👍**: 2
- **状态**: OPEN

免费用户周末使用 DeepSeek 时突然遇到 “Free usage exceeded, subscribe to Go” 错误。用户质疑是额度策略临时调整还是 bug，呼吁官方给出明确解释。

> https://github.com/anomalyco/opencode/issues/40078

### 8. #40058 API key 无法附加（已关闭，但评论较多）
- **作者**: @ArsalR
- **评论**: 6 | **👍**: 0
- **状态**: CLOSED

用户报告 Go API key 无法附加到客户端，导致无法正常调用。虽然被关闭，但 6 条评论表明该问题可能影响不止一人，且缺少官方回复。

> https://github.com/anomalyco/opencode/issues/40058

### 9. #35689 DeepSeek 静默停止执行（推理字段被丢弃）
- **作者**: @pragmaxim
- **评论**: 2 | **👍**: 4
- **状态**: OPEN

DeepSeek 模型在使用 thinking 模式时，`interleaved reasoning_content` 字段在 tool call 消息中被丢弃，导致 agent 在任务执行中突然退出循环。属于模型兼容性的关键缺陷。

> https://github.com/anomalyco/opencode/issues/35689

### 10. #17340 会话压缩失败：上下文超限后无法 compact
- **作者**: @he-who-is-not-him
- **评论**: 4 | **👍**: 2
- **状态**: OPEN

会话增长到 145k tokens（模型限制 128k）后，压缩流程报错 “context exceeds model limit even after stripping media”，用户无法手动触发压缩或继续会话。需要更健壮的会话裁剪策略。

> https://github.com/anomalyco/opencode/issues/17340

---

## 重要 PR 进展

### 1. #37889 修复 GitHub OIDC token 格式变化
- **作者**: @chAwater
- **状态**: OPEN

适配 GitHub OIDC token 从 `repo:octocat/my-repo:ref:refs/heads/main` 到新格式的迁移，修复认证失败并增强错误处理。

> https://github.com/anomalyco/opencode/pull/37889

### 2. #34786 文本附件按 MIME 类型读取
- **作者**: @adityachaudhary99
- **状态**: CLOSED（自动清理）

修复将非 `text/plain` 的文本文件以二进制垃圾数据发给模型的问题，`resolveUserPart` 现在对文本类 MIME 做文本解析。

> https://github.com/anomalyco/opencode/pull/34786

### 3. #34785 自定义网关支持 RFC 8628 设备流 OAuth
- **作者**: @fijimunkii
- **状态**: CLOSED（自动清理）

为自定义网关新增通用设备流认证 provider 类型，解决 CLI 环境下第三方网关无法完成 OAuth 交互式登录的问题。

> https://github.com/anomalyco/opencode/pull/34785

### 4. #34764 模型搜索时保留分组
- **作者**: @likeon
- **状态**: CLOSED（自动清理）

新增 `model_picker.group_search_results` 配置，在过滤模型时保留 favorites/最近使用等分组，提升模型选择效率。

> https://github.com/anomalyco/opencode/pull/34764

### 5. #34763 Desktop 支持 prompt-only 新会话 deeplink
- **作者**: @anduimagui
- **状态**: CLOSED（自动清理）

支持 `opencode://new-session?prompt=...` 格式的深度链接，方便从外部直接创建带初始 prompt 的会话。

> https://github.com/anomalyco/opencode/pull/34763

### 6. #40103 Go 使用量图表按请求数排序
- **作者**: @smrdotgg
- **状态**: OPEN

修复 Console Go 用量图表排序问题，将 Kimi K3 调整至 Grok 4.5 上方，使每五小时请求量顺序与视觉顺序一致。

> https://github.com/anomalyco/opencode/pull/40103

### 7. #40100 清除过期的权限请求提示
- **作者**: @miaojixuezhang
- **状态**: OPEN

中断或销毁的权限请求未发布 `permission.replied` 事件，导致 Web/Desktop 端残留过期的权限弹窗。该 PR 补上了事件通知。

> https://github.com/anomalyco/opencode/pull/40100

### 8. #40099 通过父链接完成 prompt 循环
- **作者**: @miaojixuezhang
- **状态**: OPEN

修复 assistant 回复通过 `parentID` 关联用户消息、而非直接比较 ID 时的判断问题，避免因客户端/服务端时钟差异导致的循环错误。

> https://github.com/anomalyco/opencode/pull/40099

### 9. #40083 重构 TUI 标签页脉冲层
- **作者**: @opencode-agent[bot]
- **状态**: OPEN

将镜像的 `outer*` 标签脉冲属性重构为可组合的 primary/edge 层描述，集中管理脉冲状态，保持现有动画时序与 per-cell 渲染循环。

> https://github.com/anomalyco/opencode/pull/40083

### 10. #27554 局域网 provider 自动发现
- **作者**: @androidand
- **状态**: OPEN

为 `/connect` 增加局域网 OpenAI 兼容服务器发现（mDNS 等），并自动拉取模型列表，覆盖本地部署场景的模型接入需求。

> https://github.com/anomalyco/opencode/pull/27554

---

## 功能需求趋势

从过去 24 小时更新的 Issues 中可提炼出以下主要方向：

1. **UI 布局与 TUI 体验**：主张保留 legacy 布局（#37012）、可配置侧边栏（#40086）、可折叠工具输出块（#40096）等，核心诉求是减少导航层级、提升长会话可读性。

2. **隐私与数据主权**：围绕隐私政策、模型托管位置、telemetry 披露的讨论显著集中（#39875 #39847），用户对数据流向与留存期限的知情权诉求强烈。

3. **可靠性改进**：包括子代理挂起（#33028）、无限重试无上限（#21960 #40090）、会话压缩失败（#17340）等稳定性问题，已成为“高频痛点”。

4. **模型兼容性与配置灵活度**：thinking/reasoning 字段解析（#35689 #34282）、图片输入能力（#29740）、模型参数按能力门控等需求持续存在。

5. **订阅与计费透明度**：免费额度虚耗（#40078）、订阅卡住（#40064）、API key 失效（#40058）等计费链路问题浮现，官方需要更清晰的用量管理与异常反馈机制。

---

##

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 · 2026-08-02

## 今日速览

今日发布 v0.21.3 版本，核心围绕 `/review` 命令能力增强。社区最热议的方向是**提示词缓存（Prompt Cache）优化**，多项 issue 与 PR 同时推进，涉及聊天压缩、工具延迟发现等场景的缓存复用。此外，终端 UI/交互类问题（TUI 滚动刷屏、Warp 键位冲突等）也引发了较多讨论。

## 版本发布

### v0.21.3
正式版本发布，结合配套 PR（[#8215](https://github.com/QwenLM/qwen-code/pull/8215)、[#8218](https://github.com/QwenLM/qwen-code/pull/8218)）推断主要包含 `/review` 命令增强：
- **测试计划验证**：审查时校验测试计划的有效性
- **失败归因**：支持衡量失败来源归属，提升代码变更分析准确性
- **多种验证视角**：新增多个验证 lens 用于代码变更评估

### v0.21.2-nightly.20260801.bc382c3ff
- `feat(hooks)`: 生命周期 hook 负载中新增 session source 字段（[#8155](https://github.com/QwenLM/qwen-code/pull/8155)）
- `feat(review)`: 缓存身份校验相关改进

## 社区热点 Issues

### 1. [#176](https://github.com/QwenLM/qwen-code/issues/176) `[CLOSED]` Tool calling does not work with local model qwen3-30b-a3b @Danmoreng · 23 评论 · 7 👍
本地部署 qwen3-30b-a3b 时，模型能生成正确的 tool call 响应，但工具调用不会被执行，且无任何报错信息。该 issue 存活近一年（2025-08 创建），评论数最高，说明本地模型工具链问题是不少用户的核心痛点。

### 2. [#1409](https://github.com/QwenLM/qwen-code/issues/1409) `[CLOSED]` 怎么无法自动读写文件？@shiwanghua · 6 评论
中文用户反馈：AI 输出几行后就结束，无法自动读写文件。此类与核心文件操作能力相关的问题仍有反复出现。

### 3. [#7966](https://github.com/QwenLM/qwen-code/issues/7966) `[CLOSED]` [type/question, scope/session-management, scope/file-operations] 如何获取会话中创建了哪些文件？@ru1yex · 6 评论
用户希望区分工作区中哪些文件由哪个会话产生（直接写入 vs 代码间接生成）。反映会话隔离与文件追踪能力的需求。

### 4. [#5971](https://github.com/QwenLM/qwen-code/issues/5971) `[CLOSED]` TUI 窗口滚动刷屏问题 @EfiveLee · 4 评论 · `welcome-pr`
Linux 环境下（Anolis OS 8.10）长会话大量文本输出时，TUI 窗口从会话开头反复滚动到最新位置，严重影响使用。已标记 `welcome-pr`，适合社区贡献修复。

### 5. [#3804](https://github.com/QwenLM/qwen-code/issues/3804) `[CLOSED]` AskUserQuestion 容易出现 `[API Error: Model stream ended with empty response text.]` @SeoMP · 5 评论
AskUserQuestion 场景下偶发空响应错误。该 issue 从 v0.15.6 持续至今，说明流式响应稳定性仍是薄弱环节。

### 6. [#8279](https://github.com/QwenLM/qwen-code/issues/8279) `[OPEN]` discussion(core): could chat compression reuse the main prompt-cache prefix via a fork? @DragonnZhang · 3 评论
设计讨论：聊天压缩是否有机会通过 fork 方式复用主会话的 prompt-cache 前缀。当前压缩请求与主会话的缓存前缀不一致，导致成本与延迟增加。这是今日 prompt caching 系列讨论的核心设计议题。

### 7. [#8330](https://github.com/QwenLM/qwen-code/issues/8330) `[OPEN]` @ completion tab switching is inaccessible in Warp because Ctrl+Tab switches terminal tabs @DragonnZhang · 3 评论
在 Warp 终端中，`@` 补全的多分类切换使用 Ctrl+Tab，但该快捷键被终端占用，导致无法切换。反映终端键位冲突带来的兼容性问题。

### 8. [#8284](https://github.com/QwenLM/qwen-code/issues/8284) `[OPEN]` feat(telemetry): expose prompt cache hit rate @DragonnZhang · 2 评论
建议将 prompt cache hit rate 作为一等遥测指标输出，方便用户监控缓存命中带来的成本节省。与 caching 方向直接相关。

### 9. [#4777](https://github.com/QwenLM/qwen-code/issues/4777) `[OPEN]` Deferred-tools listing in the system prompt busts prompt cache on every MCP discovery / tool reveal @qqqys · 2 评论
MCP 延迟工具列表被写入缓存的系统提示词，每次工具发现或 ToolSearch reveal 都会破坏 prompt cache，导致缓存频繁失效。这是 caching 方向最具体的技术负债 issue。

### 10. [#8131](https://github.com/QwenLM/qwen-code/issues/8131) `[OPEN]` bug(cli): statusline text cannot be selected in Virtualized History mode @DragonnZhang · 3 评论 · `welcome-pr`
虚拟化历史模式下，状态栏文本无法选中复制，影响用户体验。已标记可直接上手修复。

## 重要 PR 进展

### 1. [#8339](https://github.com/QwenLM/qwen-code/pull/8339) `[OPEN]` fix(core): reuse prompt cache during chat compression @DragonnZhang
聊天压缩时复用主会话的 prompt-cache 前缀（当模型与 provider 支持 Anthropic/DashScope 缓存时）。与 #8279 设计讨论直接对应，是当前 caching 优化的重要落地。

### 2. [#8276](https://github.com/QwenLM/qwen-code/pull/8276) `[OPEN]` fix(core): preserve prompt cache across deferred tool discovery @

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*