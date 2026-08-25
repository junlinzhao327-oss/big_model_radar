# AI CLI 工具社区动态日报 2026-08-26

> 生成时间: 2026-08-25 22:35 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-08-26）

> 数据来源：各工具 GitHub 仓库社区动态日报；统计周期为 2026-08-25 24:00 UTC 前 24 小时。Claude Code 与 Copilot CLI 当日无数据收录，Codex 简报被截断，相关结论请在完整数据可用后复核。

---

## 1. 生态全景

AI CLI 工具已从"单模型封装"演进为**分层竞争**：头部玩家（Gemini、Qwen、OpenCode）以"日更版本 + 高频安全修复 + 生态协议对接"为常态，技术栈也呈现 Rust（Codex）、TypeScript/Node（Gemini、OpenCode）、跨语言混合（Qwen）多路线并行的格局。子代理/多智能体协调成为各工具共同攻坚的核心战场，但可靠性问题（挂起、误报成功、协调混乱）仍在消耗大量用户信任。与此同时，**安全加固正在成为版本发布的高频主题**——SSRF 防护、环境变量注入拦截、权限白名单有效性验证在多仓库同步出现，说明 AI CLI 已进入企业级安全审视期。整体判断：功能竞赛已从"模型能力"转向"工程可靠性 + 生态兼容性"。

---

## 2. 各工具活跃度对比

| 工具 | 版本发布 | 热点 Issue 数* | 重要 PR 数* | 社区活跃信号 |
|---|---|---|---|---|
| **Gemini CLI** | 🔥 4 个：v0.57.0 正式版 + v0.58.0-preview.0 + v0.57.0-preview.1 + nightly | 10（含 3 个 P1） | 10（含 2 个安全修复） | 发布节奏最稳，正式/preview/nightly 多轨并行 |
| **OpenCode** | 1 个：v1.18.23 补丁 | 10（多个 Issue 互相关联印证） | 10（3 个已合入） | 社区反馈量大，Issue 间关联性强，用户参与度高 |
| **Qwen Code** | 1 个：v0.22.0-nightly | 10（含 1 个 P0、1 个 P1） | 10（9 个 OPEN） | 多代理编排与审核管线是当前迭代焦点 |
| **Kimi Code** | 0 | 2（均更新） | 0 | 明显低谷期，但暴露的问题严重度高 |
| **OpenAI Codex** | 提到"三个 Rust 版本"（详情截断） | 数据截断 | 数据截断 | 有动作，但无法定量评估 |
| **Claude Code** | 无数据 | 无数据 | 无数据 | — |
| **Copilot CLI** | 无数据 | 无数据 | 无数据 | — |

\* 注：为日报筛选后的"热点/重要"条目数，非 GitHub 全量 Issue/PR 计数。

**活跃度排序**：Gemini CLI ≈ Qwen Code ≈ OpenCode ≫ Kimi Code，Codex 待补全数据。

---

## 3. 共同关注的功能方向

| 方向 | 涉及工具 | 具体诉求 |
|---|---|---|
| **多智能体/子代理协调可靠性** | Gemini、Qwen | Gemini：Generalist agent 无限挂起、子代理 MAX_TURNS 误报 GOAL 成功；Qwen：多后台代理重复工作、提前宣布完成、send_message 无交互。二者高度同构，说明行业级难题尚未有解 |
| **工具执行结果真实性** | Kimi、Gemini、OpenCode | Kimi：Edit/Write 虚报成功不写盘；Gemini：Shell 命令卡 "Waiting input"、Browser 子代理假完成；OpenCode：多问题工具调用静默失败。伪成功是比报错更危险的失效模式 |
| **安全与权限边界** | Gemini、Qwen、OpenCode | Gemini：MCP OAuth SSRF 防护、扩展环境变量注入拦截、移除不安全 diff.external 覆盖；Qwen：permissions.allow 白名单不生效、Windows 符号链接校验失效；OpenCode：工具参数修复需先通过 schema 校验防注入 |
| **上下文生命周期管理** | Gemini、Qwen、Kimi | Gemini：Auto Memory 无限重试低信号会话、脱敏时机滞后；Qwen：SKILL.md 永久驻留无法卸载；Kimi：上下文压缩后误恢复已删除任务。长会话下的上下文"垃圾回收"成为普遍痛点 |
| **模型服务商兼容性** | OpenCode、Qwen | OpenCode：Cloudflare AI Gateway、Azure CLI、DeepSeek reasoning 字段、Ox Alpha Free 故障；Qwen：DeepSeek 视觉模型丢图、OpenAI-compatible 的 effort 参数钳制缺失 |
| **平台/系统兼容性** | OpenCode、Gemini、Qwen | OpenCode：macOS x64 illegal instruction、CJK IME 输入异常、Windows 代理断连；Gemini：Wayland 下浏览器子代理失败；Qwen：OOM 后终端按键紊乱。全球化用户底座带来的长尾问题仍在消耗维护精力 |

---

## 4. 差异化定位分析

| 工具 | 定位 | 技术路线特征 | 典型用户 |
|---|---|---|---|
| **Gemini CLI** | **企业级稳定性优先** | 多轨发布体系（stable/preview/nightly）成熟；安全修复密度高；深度绑定 Cloud Workstations、VS Code IDE 等 Google 生态；A2A 协议支持 | 依赖 Google Cloud 的企业开发者、关注合规与安全的生产环境用户 |
| **OpenCode** | **模型服务商"万能适配器"** | 对长尾模型服务商（Cloudflare、Azure、Vertex、DeepSeek、OpenAI-compatible）的适配最激进；桌面端 + TUI 双形态；社区功能请求驱动（i18n、搜索、触摸） | 多模型切换的资深开发者、桌面端重度用户、非英美地区开发者 |
| **Qwen Code** | **多智能体编排先锋** | 明确的多代理 roadmap（/review 子代理化 P0、advisor 独立模型、后台代理协调）；自研 TUI 架构迁移（ink → OpenTUI）；定时任务/loop 等运维化功能；阿里系模型深度联动 | 使用 Qwen 模型生态的开发者、需要复杂自动化工作流（CI/CD、定时任务）的团队 |
| **Kimi Code** | **Moonshot 生态补充** | 迭代节奏较缓，当前阶段核心矛盾是基础可靠性（文件写入、上下文恢复）而非新功能 | Kimi 模型偏好者、轻量使用场景 |
| **OpenAI Codex** | （数据截断，仅确认 Rust 技术栈有活跃迭代） | Rust 基金会带来性能与分发优势，具体方向待数据补充 | — |

**一句话总结差异**：Gemini 在"稳"上投入最深，OpenCode 在"广"上最激进，Qwen 在"多"（多智能体）上走得最远。

---

## 5. 社区热度与成熟度

- **最活跃梯队**：**Gemini CLI**（版本发布频率最高、P1 问题社区讨论充分、PR 安全主题密集）、**OpenCode**（Issue 讨论量大且用户愿意反复补充复现细节，如 Ox Alpha Free 系列 4 个 Issue 互相印证）、**Qwen Code**（P0/P1 议题清晰、PR 覆盖从核心逻辑到 CI 细节，且社区贡献者活跃——10 个 PR 中 7 个来自非官方账号）。
- **相对沉默**：**Kimi Code** 今日仅 2 个 Issue 更新、0 PR，但两个问题（假写入、上下文误恢复）都直击信任根基，属于"低活跃、高隐患"状态。
- **成熟度特征**：Gemini 已进入"安全审计常态化"阶段（SSRF、注入、依赖批量升级均出现在同日 PR 中），是七款工具中最接近企业级软件成熟度的；OpenCode 与 Qwen 处于"功能快速扩展但稳定性追赶中"——OpenCode 有持续半年的 x64 兼容问题未解、Qwen 有权限白名单失效这类安全有效性缺陷；Kimi 尚在可靠性补课期。

---

## 6. 值得关注的趋势信号

1. **"伪成功"正在成为 AI CLI 的头号信任杀手**。Kimi 的"返回成功但不写盘"、Gemini 子代理的"MAX_TURNS 误报 GOAL 成功"、OpenCode 的"工具调用静默失败"，本质都是**状态汇报与真实世界不一致**。开发者对这类 bug 的容忍度极低（Kimi 问题 1 天内获 2 条评论、Gemini P1 的 13 条讨论），可以预期**结果校验/回读验证机制**将成为下一代 AI CLI 的标配能力。

2. **安全边界从前端鉴权扩展到"AI 供应链"**。Gemini 同日三连发（MCP OAuth SSRF 防护、扩展环境变量注入净化、移除 unsafe diff.external 覆盖）+ Qwen 暴露 permissions.allow 形同虚设，指向一个核心趋势：CLI 工具正在成为企业数据面的一部分，**对 MCP 服务器、扩展、环境变量等第三方输入的安全审计**将是下一阶段竞争焦点。

3. **多智能体协作的"工程化"需求开始显性化**。Gemini 的挂起/误报与 Qwen 的协调缺陷在 24 小时内同时成为头条，且 Qwen 已提出 95k token 污染主会话的量化证据（/review 场景）。这说明**子代理不是简单的"调用另一个模型"**，隔离上下文、任务生命周期管理、结果真实性校验都需要系统级设计——这是当前最值得投入研发的方向。

4. **模型服务商兼容性 = 新的用户获取渠道**。OpenCode 因 Ox Alpha Free 故障连续多日收到用户不满、为 DeepSeek 做专属字段适配，Qwen 为 OpenAI-compatible 的 effort 参数做钳制修复——**"能插多少家模型"正在成为 CLI 工具获客的差异化武器**，长尾模型兼容不再是 PR 里的边角工作，而是直接影响社区口碑的一线战场。

5. **自由开源社区对桌面端与输入体验的诉求升温**。OpenCode 的消息搜索（👍8）、IME 修复（👍2）、触摸滚动等 Issue 持续获得关注，Qwen 与 Gemini 也在 IDE 连接与 WebShell 投入修复——**AI CLI 正从"纯终端玩具"向"桌面级生产力工具"延展**，这对 TUI/IDE 集成、渲染层架构（如 ink→OpenTUI）提出了更高要求。

6. **长时间运行稳定性成为硬指标**。Qwen 的 1T 内存 OOM、OpenCode 的 266GB 自动更新器缓存泄漏、Gemini 的会话无限挂起，都发生在"长周期驻留"场景。随着 agent 从"交互式工具"走向"后台自动化服务"，**内存管理、更新机制、会话持久化**的健壮性将直接决定产品能否进入生产环境。

---

*报告完。如需针对某一工具展开深度分析、或对某两个工具做逐项对比，可基于原始日报数据继续加工。*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-08-26）

## 1. 今日速览

过去 24 小时，Codex 发布了三个 Rust

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-08-26** | 数据更新至 2026-08-25 24:00 UTC

---

## 1. 今日速览

昨日发布了 v0.57.0 正式版及多个 preview/nightly 版本，核心修复集中在符号链接处理、Cloud Workstations OAuth 流程和 A2A 服务器稳定性。社区讨论热度最高的是 **Generalist agent 挂起** 和 **子代理达到 MAX_TURNS 后误报 GOAL 成功** 这两个 P1 级可靠性问题；与此同时，**MCP OAuth SSRF 防护**、**扩展环境变量注入** 等安全修复也吸引了大量关注。

---

## 2. 版本发布

### 🚀 v0.57.0（正式版）
- **修复**：Cloud Workstations 动态解析代理重定向 URI，解决 OAuth 流程失败问题（[#28688](https://github.com/google-gemini/gemini-cli/pull/28688)）
- **修复**：解决 IDE 连接中的目录不匹配吞掉问题

### 🔧 v0.58.0-preview.0
- **修复**：ignore 路径处理中一致的符号链接评估（[#28915](https://github.com/google-gemini/gemini-cli/pull/28915)）
- **重构**：core 模块代码结构优化

### 🌙 v0.56.0-nightly.20260825.g812f7a2bc
- **修复**：a2a-server 在新消息轮次中清除过期取消错误（[#28940](https://github.com/google-gemini/gemini-cli/pull/28940)）
- **修复**：在写策略配置中声明顶层安全检查器

### 🔄 v0.57.0-preview.1
- 将 commit `812f7a2` cherry-pick 到 release 分支，修补 v0.57.0-preview.0（[#29024](https://github.com/google-gemini/gemini-cli/pull/29024)）

---

## 3. 社区热点 Issues（TOP 10）

### #1 🔥 [P1] 子代理 MAX_TURNS 恢复被误报为 GOAL 成功（13条评论）
**#22323** | 作者：@matei-anghel | 👍 2
`codebase_investigator` 子代理报告 `status: "success"`，但实际已触发最大轮次限制，未做任何分析。该问题会**掩盖真实的性能瓶颈和中断原因**，影响代理可靠性评估。
🔗 https://github.com/google-gemini/gemini-cli/issues/22323

### #2 🔥 [P1] Generalist agent 无限期挂起（8条评论，👍 8）
**#21409** | 作者：@turmanticant
最简单的文件夹创建操作也会导致通用代理挂起长达一小时，迫使开发者取消任务。社区对这个问题关注度高，是当前**影响日常使用最严重的 bug** 之一。
🔗 https://github.com/google-gemini/gemini-cli/issues/21409

### #3 ⚡ 利用模型 bash 亲和力：零依赖 OS 沙箱与事后意图路由（8条评论）
**#19873** | 作者：@abhipatel12 | 👍 1
由于 Gemini 3 模型天然擅长链式使用 POSIX 工具，提案建议在保证安全的前提下，采用**零依赖 OS 沙箱**方式释放模型的 bash 能力，并引入事后意图路由来防止破坏性命令。
🔗 https://github.com/google-gemini/gemini-cli/issues/19873

### #4 ⚡ AST 感知的文件读取/搜索/映射影响评估（7条评论）
**#22745** | 作者：@gundermanc | 👍 1
该 EPIC 追踪一系列关于 AST 感知工具的调研：通过单次工具调用精确读取方法边界，可**减少 token 噪音和多轮对齐读取**，有望显著提升代码库导航效率。
🔗 https://github.com/google-gemini/gemini-cli/issues/22745

### #5 💬 Gemini 不主动使用 skills 和子代理（6条评论）
**#21968** | 作者：@rnett
有开发者反馈，即使配置了 gradle/git 等自定义 skills，Gemini 在相关场景下**几乎不会主动使用**，只有显式指令才会触发。这削弱了自定义扩展的实际价值。
🔗 https://github.com/google-gemini/gemini-cli/issues/21968

### #6 💬 Auto Memory 无限重试低信号会话（5条评论）
**#26522** | 作者：@SandyTao520
背景提取代理若不读取低信号会话，该会话会**永远保持在未处理状态**并被反复推荐。需要一个上限来避免无限重试的空转开销。
🔗 https://github.com/google-gemini/gemini-cli/issues/26522

### #7 🔒 Auto Memory 需确定性脱敏并减少日志（4条评论）
**#26525** | 作者：@SandyTao520
Auto Memory 将本地转录发送给模型时，脱敏发生在内容进入上下文**之后**，且服务可能记录现有技能内容。社区呼吁在输入端做确定性 redaction。
🔗 https://github.com/google-gemini/gemini-cli/issues/26525

### #8 🔥 [P1] Shell 命令执行卡在 "Waiting input"（4条评论，👍 3）
**#25166** | 作者：@rnett
简单的 CLI 命令执行完毕后，终端仍显示 "Awaiting user input" 并永久挂起。该问题**高频复现**，严重干扰自动化工作流。
🔗 https://github.com/google-gemini/gemini-cli/issues/25166

### #9 💬 Browser Agent 需要自动会话接管与锁恢复（4条评论）
**#22232** | 作者：@hsm207
`BrowserManager.ts` 在遇到锁定的浏览器配置时采用 fail-fast 策略，建议改为自动接管失效会话，提升持久化浏览器模式下的鲁棒性。
🔗 https://github.com/google-gemini/gemini-cli/issues/22232

### #10 🔥 [P1] Browser 子代理在 Wayland 下失败（4条评论）
**#21983** | 作者：@sigmaSd | 👍 1
浏览器子代理在 Wayland 会话中以 `GOAL` 终止但实际并未完成任务，疑似 Wayland 兼容性问题，影响 Linux 用户的核心体验。
🔗 https://github.com/google-gemini/gemini-cli/issues/21983

---

## 4. 重要 PR 进展（TOP 10）

### 🔧 IDE 连接稳定性
**#29088** `fix(vscode-ide-companion): resolve stop() with an MCP stream open`
修复 `IdeServer.stop()` 因 MCP 长连接而永不 resolve 的问题，解决 VS Code 扩展 deactivate 阻塞。
🔗 https://github.com/google-gemini/gemini-cli/pull/29088

### 🔧 扩展并发安装竞态
**#29087** `fix(cli): prevent concurrent extension install races`
利用 `proper-lockfile` 防止多个 Gemini CLI 进程同时安装/更新同一扩展造成文件交错写入。
🔗 https://github.com/google-gemini/gemini-cli/pull/29087

### 🔒 MCP OAuth SSRF 防护
**#29081** `fix(core): prevent SSRF in MCP OAuth metadata discovery and authentication`
强制 HTTPS（loopback 除外）、校验资源来源匹配，符合 RFC 9728/8414 安全约束，修复 OAuth 发现与令牌交换中的 SSRF 风险。
🔗 https://github.com/google-gemini/gemini-cli/pull/29081

### 🔧 AbortSignal 正确透传
**#29089** `fix(core): forward abortSignal to retryWithBackoff in BaseLlmClient`
修复 `SessionSummaryService`、聊天压缩等场景下 abortSignal 未传入重试逻辑的问题，确保取消操作及时生效。
🔗 https://github.com/google-gemini/gemini-cli/pull/29089

### 🔧 混合行尾检测修复
**#28983** `fix(core): detect mixed line endings instead of flagging CRLF on a single match`
原逻辑只要出现一个 `\r\n` 就判定整个文件为 CRLF，现改为正确识别混合行尾，避免不必要的全文件重写。
🔗 https://github.com/google-gemini/gemini-cli/pull/28983

### 🔒 移除不安全的 diff.external 覆盖
**#28930** `fix(core): drop unsafe diff.external override`
撤销通过空字符串禁用外部 diff 工具的 hack（git 不支持该写法），改用安全的替代方案，修复潜在命令注入面。
🔗 https://github.com/google-gemini/gemini-cli/pull/28930

### 🔒 扩展环境变量注入防护
**#28863** `fix(extensions): prompt for consent on environment changes and sanitize runtime-altering environment variables`
将 MCP 服务器环境配置纳入 consent 字符串，并净化可改变运行时行为的环境变量，防止扩展绕过用户同意注入恶意环境。
🔗 https://github.com/google-gemini/gemini-cli/pull/28863

### 📦 76 个 npm 依赖批量升级
**#28984** `chore(deps): bump the npm-dependencies group across 1 directory with 76 updates`
包含 `simple-git`（3.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-08-26

## 今日速览

过去 24 小时内，Kimi Code CLI 仓库无新版本发布、无 PR 更新，但有两个 Issue 出现重要动态：一个涉及 0.38.0 版本在 macOS 上 `Edit`/`Write` 工具虚报成功但不写盘（严重可靠性问题），另一个是较早的上下文压缩 Bug 在昨日获得新回复，可能与任务恢复逻辑有关。今日社区热点集中在文件操作可靠性与上下文管理两方面。

## 社区热点 Issues

过去 24 小时更新/新增的 Issue 共 2 个，全部列出：

### 1. [#2617] Edit/Write tools report success but never write to disk (0.38.0, macOS)  
- **作者**: @tizerluo | 创建: 2026-08-25 | 更新: 2026-08-25  
- **评论**: 2 | 👍: 0  
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2617

**为什么重要**：该 Issue 描述了一个 100% 可复现的严重缺陷——`Edit` 和 `Write` 工具返回成功消息，但实际没有写入磁盘。这会导致开发者误以为文件已保存，影响核心工作流，属于高危可靠性问题。社区已在 1 天内产生 2 条评论，说明关注度较高。目前状态为 Open，且关联到 0.38.0 版本，建议优先处理。

### 2. [#2523] Context compaction bug — Kimi Code reopens an already completed and deleted task  
- **作者**: @Frogzter | 创建: 2026-07-20 | 更新: 2026-08-25  
- **评论**: 1 | 👍: 0  
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2523

**为什么重要**：这是个跨版本问题（用户报告时为 v0.6.3，昨日被更新，可能仍在复现）。它涉及上下文压缩后，CLI 错误地重新打开一个已完成且已删除的任务，导致工作区状态混乱。任务恢复逻辑与上下文压缩的交互值得关注，尤其是长时间会话下的稳定性问题。

## 重要 PR 进展

过去 24 小时内无 Pull Request 新增或更新。

## 功能需求趋势

由于今日仅更新 2 个 Issue，功能需求趋势主要从这两条反馈中提炼：

- **文件写入可靠性**：开发者对“工具返回成功但实际磁盘未变更”的容忍度极低。社区期望文件操作具备明确的原子性保障或校验机制，必要时给出失败警告而非伪成功。
- **上下文管理与任务恢复**：上下文压缩不应破坏任务生命周期。开发者希望压缩过程能正确区分已完成任务和活跃任务，避免错误恢复已删除的工作上下文。

## 开发者关注点

当前开发者反馈中的痛点集中体现为：  
1. **工具行为透明性**：`Edit`/`Write` 等修改类工具需要真实反映操作结果，不能“假成功”，否则会引发连锁错误。  
2. **会话长期稳定性**：在长会话或上下文压缩场景下，任务状态保持和恢复需要更谨慎，当前实现存在误判风险（同时覆盖了 macOS 与 Windows 平台上的不同表现）。

> 注：以上分析基于 2026-08-26 抓取的 GitHub 数据（仅含 2 个更新 Issue），如需更全面的趋势，建议结合更多历史 Issue 数据。完整仓库地址：https://github.com/MoonshotAI/kimi-cli

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-26

## 今日速览

昨日 OpenCode 发布 v1.18.23 补丁，修复了 Cloudflare AI Gateway 对第三方提供方（尤其是 Anthropic 模型）的路由问题。社区最热话题集中在 **Ox Alpha Free 模型的 "Endpoint is unavailable" 错误**（多个 Issue 互相印证，疑似服务端故障）以及桌面端长期存在的稳定性问题（TUI 卡死、会话永久卡住、自动更新器异常）。此外，多语言支持和消息搜索等社区功能请求持续获得高赞。

---

## 版本发布

### v1.18.23
- **核心修复**：修复 Cloudflare AI Gateway 对第三方提供方的路由逻辑，使非 Workers 模型可通过网关 REST API 正常工作（@superhighfives）
- **Anthropic 适配**：修复 Anthropic 模型经 Cloudflare AI Gateway 时，将 `claude-haiku-4.5` 这类带点的模型 ID 转换为 Anthropic 所需的短横线格式

---

## 社区热点 Issues（Top 10）

### 1. Ox Alpha Free 模型 "Endpoint is unavailable" 故障（系列报告）
- **#44300** — [Zen API: x-preview-f-free / ox-alpha-free 含 tools 请求全部失败](https://github.com/anomalyco/opencode/issues/44300) （评论 13，👍 5）
  自 8/23 起，任何包含 `tools` 数组的请求都会失败，已在 Zen Console 和 Go 两条路由上复现。疑似服务端问题。
- **#44850** — [Ox Alpha Free 在使用工具时报错](https://github.com/anomalyco/opencode/issues/44850) （评论 7，👍 2）
  普通对话正常，一旦 OpenCode 调用工具即报 "Endpoint is unavailable"，影响实际开发工作流。
- **#44742** — [Closed: 使用 Ox Alpha Free 时的报错](https://github.com/anomalyco/opencode/issues/44742) （评论 3）
  用户多次尝试仍无法解决，已关闭但问题未根治。

**为什么重要**：免费模型是社区获取新用户的重要入口，连续多日未修复已引起多位用户不满（#45084 被标记 needs:compliance）。

### 2. [#8345 — zsh: illegal hardware instruction opencode](https://github.com/anomalyco/opencode/issues/8345)（评论 23，👍 7）
- **状态**：OPEN（创建于 2026-01-14，仍在更新）
- **摘要**：macOS x64 上运行 opencode-desktop-darwin-x64 时报 `illegal hardware instruction`。
- **为何重要**：这是历史最久、评论最多的 Issue 之一，暴露出 x64 Darwin 构建的系统兼容性问题，至今未解决。

### 3. [#19143 — [Feature] 桌面端实现消息搜索（Cmd+F / Ctrl+F）](https://github.com/anomalyco/opencode/issues/19143)（评论 9，👍 8）
- **状态**：OPEN
- **摘要**：桌面 App 中无法在长会话内快速定位信息，请求支持消息搜索。
- **为何重要**：高赞功能请求，直接关系到桌面端日常使用效率。

### 4. [#12405 — Error: Connection reset by server](https://github.com/anomalyco/opencode/issues/12405)（评论 19）
- **状态**：CLOSED
- **摘要**：Windows 10 + 代理环境下，接入 GLM-4.7 模型后执行 init 命令即报错。
- **为何重要**：代理/网络兼容性问题影响面广，关闭可能意味着已修复，但仍是代理用户的常见痛点参考。

### 5. [#35434 — 多问题工具调用在 TUI 中静默失败（v1.17.13 回归）](https://github.com/anomalyco/opencode/issues/35434)（评论 7）
- **状态**：CLOSED
- **摘要**：`question` 工具在传入 2 个以上问题时，按回车无效，无 reply/reject 事件发出。单问题调用正常。
- **为何重要**：这是一个明确的回归 bug，涉及与 TUI 交互核心路径。

### 6. [#43277 — 会话永久卡死，重启无法恢复](https://github.com/anomalyco/opencode/issues/43277)（评论 5）
- **状态**：OPEN
- **摘要**：多个会话在使用中永久卡死，状态跨重启保留，无法通过重启 opencode server 恢复。
- **为何重要**：会话持久化状态损坏问题，严重影响用户长期工作流。

### 7. [#7712 — [Feature] 支持编辑上下文删除消息](https://github.com/anomalyco/opencode/issues/7712)（👍 12，评论 4）
- **状态**：CLOSED
- **摘要**：用户希望能在死胡同中通过编辑上下文（删除消息）来挽回对话，而不是新开会话。
- **为何重要**：12 个赞在功能请求中属于高热度，反映用户在长会话中模型方向跑偏时的真实需求。

### 8. [#45053 — opencode-go/muse-spark-1.2-contributor 无限挂起](https://github.com/anomalyco/opencode/issues/45053)（评论 3）
- **状态**：OPEN
- **摘要**：该模型接受请求后无输出、无错误、无完成，同一订阅下其他模型正常，疑似服务端问题。

### 9. [#45087 — 自动更新器每 10 分钟重装，吃掉 266 GB](https://github.com/anomalyco/opencode/issues/45087)（评论 2）
- **状态**：OPEN
- **摘要**：`opencode2 serve --service` 的更新循环不断重新下载 beta 包，导致 `~/.npm/_cacache` 积累了 266 GB 数据。
- **为何重要**：极端异常的资源消耗，服务端进程长期运行时可能被触发，影响面极大。

### 10. [#39632 — v2 输入框中 IME 首字输入异常](https://github.com/anomalyco/opencode/issues/39632)（评论 3，👍 2）
- **状态**：OPEN
- **摘要**：新 prompt 输入框首字符无法停留在组合态，而是直接提交为纯文本；旧 UI 正常。
- **为何重要**：对中日韩用户（CJK）输入法用户是关键的可用性 bug。

---

## 重要 PR 进展（Top 10）

### 1. [#45085 — fix(ai): send responses instructions at top level](https://github.com/anomalyco/opencode/pull/45085)（CLOSED）
- **内容**：将 Responses API 的 `instructions` 移到标准顶层字段，移除冗余的 provider-option 路径，统一 `request.system` 为唯一来源。
- **意义**：简化 AI 请求路径，避免指令重复/冲突。

### 2. [#44971 — feat(tui): add persistent session terminals](https://github.com/anomalyco/opencode/pull/44971)（OPEN）
- **内容**：TUI 新增持久化终端，主界面左侧为会话、右侧为选中的终端，通过会话级状态管理成员。
- **意义**：大幅改善 TUI 中终端与代码编辑的协作体验。

### 3. [#45086 — feat(core): support Azure CLI authentication](https://github.com/anomalyco/opencode/pull/45086)（OPEN）
- **内容**：V2 Azure provider 支持通过 Azure CLI 现有登录会话获取 Microsoft Entra ID 认证。
- **意义**：简化 Azure 企业用户接入流程，无需手动配置 API key。

### 4. [#45081 — fix(ai): accept responses calls without item ids](https://github.com/anomalyco/opencode/pull/45081)（CLOSED）
- **内容**：允许 Responses `function_call` 输出项缺少 provider item ID 时使用 `call_id` 兜底。
- **意义**：修复部分模型或网关返回格式不完整时的兼容性问题。

### 5. [#43498 — fix(ai): preserve Vertex Anthropic tool continuations](https://github.com/anomalyco/opencode/pull/43498)（CLOSED）
- **内容**：修复 Vertex 上 Claude 工具连续调用时，因本地工具结果后紧跟原生 system 消息导致 HTTP 404 的问题。
- **意义**：保障 GCP Vertex 用户的 Anthropic 工具调用可靠性。

### 6. [#45079 — feat(opencode): support Azure CLI authentication（v1 版本）](https://github.com/anomalyco/opencode/pull/45079)（OPEN）
- **内容**：与 #45086 类似，为现有 Azure provider 增加 Azure CLI 认证支持，同时保留 API key 流程。

### 7. [#44423 — fix(app): scroll project picker with touch](https://github.com/anomalyco/opencode/pull/44423)（OPEN）
- **内容**：项目选择器支持触摸滚动，修复 Shadow DOM 内拖拽滚动失效的问题。
- **意义**：改善触屏设备/平板上的桌面端使用体验。

### 8. [#45075 — fix(ai): require reasoning fields for deepseek assistants](https://github.com/anomalyco/opencode/pull/45075)（CLOSED）
- **内容**：新增 `requireReasoning` 兼容选项，根据 DeepSeek 模型 ID/provider/端点自动推断是否需要 reasoning 字段。
- **意义**：适配 DeepSeek 模型的特殊推理要求，避免请求被拒。

### 9. [#45002 — feat(core): repair malformed tool arguments before validation](https://github.com/anomalyco/opencode/pull/45002)（OPEN）
- **内容**：内部插件在 schema 校验前对畸形工具参数做保守修复：移除可选非空 null、类型转换、解析字符串化容器等。
- **意义**：提升对宽松 LLM 输出的容忍度，减少工具调用失败率。

### 10. [#38896 — feat(opencode): expose POST /question/ask for plugins and SDK](https://github.com/anomalyco/opencode/pull/38896)（CLOSED）
- **内容**：插件和 SDK 已有 reply 能力，但无法主动发起提问；此 PR 新增 `POST /question/ask` 端点。
- **意义**：补齐插件交互闭环，支持更丰富的工作流自动化。

---

## 功能需求趋势

从 Issue 和 PR 中可提炼出社区最关注的几个方向：

1. **模型服务商兼容性（最高优先级）**：大量 Issue 集中在 Ox Alpha Free 服务故障、Cloudflare AI Gateway、Azure Vertex 接入、DeepSeek 特殊字段适配。社区既关心**免费模型的可用性**，也关注**企业级云服务（Azure/Vertex）的顺滑接入**。
2. **桌面端体验完善**：消息搜索（#19143）、MCP 服务器可视化配置（#40335）、项目删除/编辑（#37280、#44994）、触摸支持（#44423）等，说明桌面端在快速迭代但功能覆盖仍有明显缺口。
3. **TUI 生产力优化**：持久化终端（#44971）、可编辑上下文/删除消息（#7712）、`--resume` 会话选择器（#38878）是提升终端用户体验的代表性需求。
4. **多语言与国际化**：Hebrew（#42447）、Italian（#38841）等多个语言贡献 PR，社区全球化活跃。
5. **会话状态恢复与稳定性**：会话永久卡死（#43277）、TUI 冻结（#35494）、渲染器 ResizeObserver 死循环（#43355）表明会话生命周期管理是稳定性短板。

---

## 开发者关注点

- **"Endpoint is unavailable" 高频出现**：涉及 Ox Alpha Free 模型和 opencode-go 订阅的多个 Issue 反复出现此错误（#44300、#44850、#45020、#45084 等），用户普遍反馈"没有明确解决方案、只能等待"，服务状态透明度和修复速度是当前社区的最大不满点。
- **macOS x64 / Linux 系统兼容性**：#8345（illegal hardware instruction）从 1 月持续至今未解决，x64 Darwin 用户受影响；#35494 报告 Debian 13 XFCE 下 TUI 空白屏只能 kill -9。
- **代理与网络环境适配**：#12405 等 Issue 显示 Windows + 代理场景下连接失败是常见问题，影响中国大陆等多地域开发者。
- **I18n 输入法（IME）问题**：#39632 反映 v2 prompt 输入框 IME 组合态被破坏，直接影响 CJK 用户基础输入体验，开发者期望尽快修复。
- **自动更新机制可信度**：#45087 的 266 GB 事件引发对后台更新循环设计的质疑，长时间运行的官方服务进程反而成为磁盘杀手，社区希望引入更新频率限制或版本比较去重。
- **多系统消息格式仍不兼容**：#45055 指出即便在 1.18.23 中，OpenCode 仍会向 OpenAI 兼容后端发送多个 `system` 角色片段，导致 SGLang/Qwen 严格模板下每轮 agent 调用失败——模型兼容适配任重道远。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-26

## 今日速览

今日发布 v0.22.0-nightly 版本，包含 web-shell 相关工作区路径传递修复。社区讨论热度集中在多智能体协调缺陷（#8097）、`/effort max` 导致会话锁死的高优先级 bug（#9459）、以及 TUI 架构迁移方案（#8662）；同时新增了 DAP 调试协议集成的功能请求（#10051），显示社区对调试能力的关注正在上升。P0 级 `/review` 子代理化改造（#9784）进入讨论视野。

## 版本发布

**v0.22.0-nightly.20260825.22bb5e8b9f** — 过去 24 小时发布

- `fix(web-shell)`: 从 overview panel 打开会话时正确传递 session workspace cwd（PR #9730 相关）
- `fix(web-shell)`: 另一项修复内容条目被截断，完整信息需查看 release notes

🔗 [查看 Release](https://github.com/QwenLM/qwen-code/releases/tag/v0.22.0-nightly.20260825.22bb5e8b9f)

## 社区热点 Issues（10 个）

### 1. `/effort max` 锁死会话 — OpenAI-compatible 提供商全挂
**#9459** · [priority/P1, type/bug] · 💬 10 评论
UI 提供 `/effort max` 选项，但 OpenAI-compatible provider 全部拒绝该值，`clampReasoningEffort()` 未对 `'max'` 做钳制。一旦设置，**会话内后续每个请求都会 400 失败**，直到手动改回 tier。这是当前最高优先级 bug，影响所有使用第三方兼容 API 的用户。
🔗 https://github.com/QwenLM/qwen-code/issues/9459

### 2. `/review` 全流程子代理化改造
**#9784** · [priority/P0, enhancement, roadmap/multi-agent] · 💬 3 评论
完整 `/review high` 运行会在用户主会话中注入约 95k token 的 SKILL.md 并累积 14+ 个代理返回结果，既影响正确性也污染主对话。提议将整个管线放入 fork 子代理上下文执行（前置条件：#9782）。P0 优先级说明团队已重视此问题。
🔗 https://github.com/QwenLM/qwen-code/issues/9784

### 3. 后台代理协调缺陷：重复工作、提前完成、send_message 无交互
**#8097** · [priority/P2, type/bug, roadmap/multi-agent] · 💬 8 评论
同时运行多个后台 Explore 子代理并用 `send_message` 进行中通信时出现三类协调失败：父代理重复子代理工作、子代理提前宣布完成、`send_message` 无法交互。来自社区的多代理协作核心痛点，反映了真实使用场景下的协调机制缺口。
🔗 https://github.com/QwenLM/qwen-code/issues/8097

### 4. Skill 上下文生命周期管理
**#6762** · [priority/P2, feature-request, roadmap/context-performance] · 💬 6 评论
SKILL.md 内容作为工具结果加载进对话历史后**永远驻留**，无法卸载、压缩或过期。社区请求引入机制来管理 skill 体在模型上下文中的生命周期，与 #9309（压缩结果不正确）共同指向上下文管理方向的强烈需求。
🔗 https://github.com/QwenLM/qwen-code/issues/6762

### 5. 长时间运行后 OOM（内存 1T 仍溢出）
**#9198** · [priority/P2, type/bug, 状态: need-information] · 💬 6 评论
用户跑了一周多未退出，服务器 1T 内存仍 OOM，且 OOM 后 tmux 终端按键全部紊乱（复制/粘贴异常）。用户明确指出"qwen 独有问题，kimi code 正常"，对终端交互稳定性有较高期待。
🔗 https://github.com/QwenLM/qwen-code/issues/9198

### 6. DeepSeek 视觉模型静默丢弃图片内容
**#10027** · [priority/P2, type/bug] · 💬 4 评论 · 已关闭
使用 `deepseek-v4-flash-vision-exp` 时，通过 `read_file` 读到的图片（`image_url` 内容）被静默替换为 `[Unsupported content type: image_url]` 占位符。多模型兼容性问题，社区对新模型接入的验证速度有要求。
🔗 https://github.com/QwenLM/qwen-code/issues/10027

### 7. `permissions.allow` 不限制发送给模型的工具集
**#9827** · [priority/P2, type/bug, category/tools] · 💬 4 评论 · 已关闭
设置 `permissions.allow` 白名单后，CLI 的 `/tools` 显示是过滤了，但**实际发往 API 的请求仍包含完整内置工具集**，导致白名单形同虚设。涉及权限模型的安全有效性问题，属核心信任边界。
🔗 https://github.com/QwenLM/qwen-code/issues/9827

### 8. TUI 渲染层从 ink 迁移到 OpenTUI
**#8662** · [priority/P3, enhancement, roadmap/terminal-ux] · 💬 5 评论
当前 TUI 基于 ink 7 + React 19，带着约 1037 行补丁和一个自定义虚拟视口模式，存在闪烁/渲染结构性问题。社区发起迁移到 OpenTUI 的跟踪讨论，属于终端体验的架构级改进方向。
🔗 https://github.com/QwenLM/qwen-code/issues/8662

### 9. 原生 DAP（Debug Adapter Protocol）集成
**#10051** · [priority/P3, feature-request, type/tools] · 💬 4 评论
社区请求为 Qwen Code 添加一等 DAP 支持，让代理能编程式地与调试器交互，而非仅依赖终端输出和源码分析。这是一个全新的、面向调试场景的能力扩展。
🔗 https://github.com/QwenLM/qwen-code/issues/10051

### 10. Windows 下 `@` 文件读取安全加固缺陷
**#8227** · [priority/P2, type/bug, category/security] · 💬 5 评论 · 欢迎 PR
PR #7206 对 `@` 引用文件读取做了符号链接/TOCTOU 防护，但 Windows 上 `O_NOFOLLOW` 不存在，dev/ino 身份校验可能无效且未经过测试。安全关键路径上的平台差异问题。
🔗 https://github.com/QwenLM/qwen-code/issues/8227

## 重要 PR 进展（10 个）

### 1. `feat(cli)`: 为无项目任务添加独立会话
**#9978** · @doudouOUC · 状态: OPEN
为 projectless 任务提供 standalone sessions，使用户不依赖特定项目目录即可启动独立会话，提升 CLI 在零散任务场景中的可用性。
🔗 https://github.com/QwenLM/qwen-code/pull/9978

### 2. `feat(review)`: 新增 prose-execution 审计与 counter-frame 审计
**#9717** · @wenshao · 状态: OPEN · [autofix/takeover]
当 diff 涉及指令类文件（SKILL.md、`.claude/agents/`、`.qwen/agents/` 等）时，执行散文执行审计和反向框架审计，补齐 #9655 事故复盘中的缺口。
🔗 https://github.com/QwenLM/qwen-code/pull/9717

### 3. `fix(ci)`: 脚本测试间让出事件循环，避免 vitest RPC 超时
**#10050** · @qwen-code-dev-bot · 状态: OPEN
为 script-test setup 添加一行全局钩子：每个测试前让出事件循环到真实定时器。autofix 套件 219 个测试、约 66s 同步 `spawnSync` 测试导致 vitest worker 事件循环阻塞并超时。
🔗 https://github.com/QwenLM/qwen-code/pull/10050

### 4. `feat(skills)`: 扩展技能注册表 key 按扩展名加命名空间
**#10049** · @nerdalytics · 状态: OPEN · [review/self-reported]
扩展提供的技能注册 key 从裸名称改为 `<extension>:<name>` 格式，Skill 工具查找、`<available_skills>` 上下文块、斜杠命令注册、`skills.disabled` 匹配统一走同一注册表解析，避免命名冲突。
🔗 https://github.com/QwenLM/qwen-code/pull/10049

### 5. `fix(core)`: 三个运行生命周期缺陷
**#9974** · @qqqys · 状态: OPEN · [autofix/takeover]
修复工作流运行生命周期中三个独立缺陷：取消工作流真正结束、失败状态正确传播等。每个修复独立可回退，共享同一文件冲突面所以打包提交。
🔗 https://github.com/QwenLM/qwen-code/pull/9974

### 6. `feat`: 添加原生 advisor 工具
**#9636** · @ZijianZhang989 · 状态: OPEN
当配置了独立的 Advisor 模型时，执行器可调用无参 `advisor {}` 工具获取独立第二意见，并将审查结果作为工具结果继续执行原任务。可配置模型入口，属于多模型协作方向的实用增强。
🔗 https://github.com/QwenLM/qwen-code/pull/9636

### 7. `fix(cli)`: 会话启动时显示活动定时任务
**#10053** · @yiliang114 · 状态: OPEN
交互式会话启动时输出 `N active scheduled task(s). Run /loop list to inspect.` 警告。直接回应 #5823 中"cron 任务静默触发、无可见性"的痛点。
🔗 https://github.com/QwenLM/qwen-code/pull/10053

### 8. `feat(web-shell)`: 持久化 reasoning effort
**#10011** · @callmeYe · 状态: OPEN
WebShell 推理设置现在立即更新活动会话，并将相同值持久化为全局 `model.reasoningEffort` 默认值，重启守护进程后依然生效，同时修复 #10006 中懒加载会话无法配置推理模式的问题。
🔗 https://github.com/QwenLM/qwen-code/pull/10011

### 9. `feat(core)`: 信任 generated-scripts 根目录用于工作流 scriptPath 加载
**#9987** · @qq

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*