# AI CLI 工具社区动态日报 2026-08-20

> 生成时间: 2026-08-19 22:45 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-08-20）

## 1. 生态全景

AI CLI 工具已全面进入"可靠性打磨"阶段：不再是基础对话能力的比拼，而是

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告

**数据截至 2026-08-20 | 来源：github.com/anthropics/skills**

---

## 1. 热门 Skills 排行

> 以下 PR 均处于 **Open** 状态（TOP 列表内尚无 merged）。按社区讨论热度排序。

**① skill-creator 评估链路修复（#1298）** — [链接](https://github.com/anthropics/skills/pull/1298)
- 修复 `run_eval.py` 对所有技能描述一律报告 `recall=0%` 的严重缺陷，导致描述优化循环在噪声上做梯度下降；同时修复 Windows 流读取、触发检测与并行 worker 问题。
- 讨论热点：直接响应 Issue #556（10+ 独立复现），是当前 skill-creator 工具链最大的可靠性痛点的集中修复。

**② document-typography 排版质检技能（#514）** — [链接](https://github.com/anthropics/skills/pull/514)
- 对 AI 生成文档做排版质量控制：孤词换行（1–6 词溢出到下一行）、段首孤儿标题、编号错位——均为 Claude 生成文档的普遍问题。
- 讨论热点：覆盖所有走文档生成的用户场景，通用性强，社区讨论关注度高。

**③ ODT 文档处理技能（#486）** — [链接](https://github.com/anthropics/skills/pull/486)
- 支持 OpenDocument 格式（.odt/.ods）的创建、模板填充、解析转

---



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-20

## 今日速览

- 昨日发布 `rust-v0.149.0-alpha.1` 与 `rust-v0.149.0-alpha.2` 两个预发布版本，目前尚未披露详细变更日志。
- Windows 平台问题集中爆发：归档失败（`\\?\` 路径前缀）、更新后无法重启、认证意外丢失、浏览器插件初始化失败等成为社区最热议题。
- 安全加固成为 PR 主线：**停止将 Git 命令视为固有安全操作**、**隔离自动插件 Git 操作**等多项安全修复陆续合入，回应了近期针对仓库配置劫持的担忧。

## 版本发布

### rust-v0.149.0-alpha.1 / rust-v0.149.0-alpha.2
- 8 月 19 日连续发布两个 alpha 预发布版本（`0.149.0-alpha.1` → `0.149.0-alpha.2`）。
- 官方目前仅标注 "Release 0.149.0-alpha.x"，尚未公布具体变更内容。从当日合入的 PR 来看，可能涉及 Git 安全策略调整、Guardian v2 架构整合以及异步用户消息功能开关移除等改动。

## 社区热点 Issues

1. **[#39136] Codex 内置浏览器插件初始化失败：Trusted RPC 依赖不在可信代码路径内**
   - 作者：@Double-hhd ｜ 更新：2026-08-19 ｜ 💬 77 ｜ 👍 41
   - 当前社区最热 issue。Windows 桌面版内置浏览器插件无法初始化，Trusted RPC 依赖校验失败。41 个 👍 和 77 条评论说明大量 Windows 用户受影响，且存在多种触发场景。
   - https://github.com/openai/codex/issues/39136

2. **[#38455] ChatGPT Desktop 反复生成 Computer Use 工作进程并导致 V8 OOM 崩溃（macOS）**
   - 作者：@flannick ｜ 更新：2026-08-19 ｜ 💬 30 ｜ 👍 12
   - 空闲状态下 98 秒后自动崩溃，崩溃前生成 187 个 computer-use 命名线程。32GB RAM 的 Apple Silicon 机器也无法幸免，明显是异常进程泄漏，属于影响较大的稳定性问题。
   - https://github.com/openai/codex/issues/38455

3. **[#34301] GPT Sol/Terra 线程无法生成 Luna 子代理（Windows）**
   - 作者：@QuinnISHE ｜ 更新：2026-08-19 ｜ 💬 10 ｜ 👍 34
   - 34 个 👍 在仅 10 条评论的情况下显得格外突出，说明很多用户遇到了相同问题但不一定都参与讨论。Luna Multi Agent 版本不匹配导致子代理功能在 Windows 上完全不可用。
   - https://github.com/openai/codex/issues/34301

4. **[#27117] Windows 独立更新从 pwsh 继承 PSModulePath，导致 Get-FileHash 失败**
   - 作者：@BlueOcean223 ｜ 更新：2026-08-19 ｜ 💬 17 ｜ 👍 13
   - 更新流程从 PowerShell 7 启动后会继承 `PSModulePath` 到 `powershell.exe`，造成哈希校验失败、更新中断。属于 Windows 更新链路的典型环境变量污染问题，影响所有 pwsh 用户。
   - https://github.com/openai/codex/issues/27117

5. **[#33493] 本地压缩 v2 保留无界 input_image 载荷，导致反复自动压缩**
   - 作者：@snrui ｜ 更新：2026-08-19 ｜ 💬 17 ｜ 👍 4
   - 长线程 + 大量图片场景下，压缩后 input_image 未被清理，上下文反复触发自动压缩。直接影响图像密集型工作流，并伴随 token 消耗翻倍。
   - https://github.com/openai/codex/issues/33493

6. **[#39189] Windows 26.814：打开已有线程后个人 Pro 账户被登出**
   - 作者：@ll10020163 ｜ 更新：2026-08-19 ｜ 💬 9 ｜ 👍 2
   - 触发条件：workspace-only 设置返回 401 后，个人账户直接掉登录。认证状态与 workspace 配置耦合，属于比较隐蔽的账户状态管理缺陷。
   - https://github.com/openai/codex/issues/39189

7. **[#11298] “Yes, and don't ask again” 权限记忆功能失效**
   - 作者：@BlueBlazin ｜ 更新：2026-08-19 ｜ 💬 10 ｜ 👍 18
   - 老 issue 但持续获得关注。用户反复确认“不再询问”后，Codex 依然弹出权限确认。沙箱权限规则未正确持久化，属于日常使用频率最高的痛点之一。
   - https://github.com/openai/codex/issues/11298

8. **[#29797] Windows 桌面版运行 git log / 读取项目文件时报 helper_unknown_error**
   - 作者：@jrtigers ｜ 更新：2026-08-19 ｜ 💬 14 ｜ 👍 0
   - 看似集中在 Windows 沙箱辅助进程上：`setup refresh` 阶段反复失败，导致基础代码阅读能力不可用。虽然 👍 不多，但 14 条评论说明影响范围不小。
   - https://github.com/openai/codex/issues/29797

9. **[#39209] Windows 归档失败：rollout 路径使用 `\\?\` 前缀时外部路径规范化失效**
   - 作者：@RuriLothlorien ｜ 更新：2026-08-19 ｜ 💬 12 ｜ 👍 2
   - 与 #39150、#39161 同属一个根因系列：Windows 扩展长度路径前缀导致归档操作 `os error 2`。文件明明存在却无法归档，说明路径规范化在 `\\?\` 前缀下没有生效，影响多个版本。
   - https://github.com/openai/codex/issues/39209

10. **[#39531] [Windows] Chrome 扩展 Native Host 过期，浏览器控制只能只读**
    - 作者：@HumpyAngel ｜ 更新：2026-08-19 ｜ 💬 2 ｜ 👍 0
    - 新提交 issue：扩展能读取标签页标题/URL/可见文本，但点击、输入、导航等操作全部失败，提示 native host 过期。浏览器自动化能力在 Windows 上处于半可用状态。
    - https://github.com/openai/codex/issues/39531

## 重要 PR 进展

1. **[#39524] 停止将 Git 命令视为固有安全操作**
   - 仓库配置可让只读 Git 命令执行 helpers（如 `core.fsmonitor`、`core.pager` 等），因此 Git 参数本身不足以建立信任。从 Unix 和 Windows 的 known-safe 列表中移除 Git 命令，属于安全边界的重要收紧。
   - https://github.com/openai/codex/pull/39524

2. **[#39520] 隔离自动插件 Git 操作**
   - 后台 marketplace/插件刷新可能继承项目仓库的 Git 配置，导致远程地址被重定向或自动执行 Git helpers。本次修改将插件刷新操作与项目级配置隔离。
   - https://github.com/openai/codex/pull/39520

3. **[#39410] 刷新过期的 AWS Bedrock 凭证**
   - 为 Bedrock 会话增加 `aws.auth_refresh` provider 配置，支持通过外部 `aws` 命令刷新过期凭证，并带可配置超时。解决长会话中途凭证失效需要重建会话的问题。
   - https://github.com/openai/codex/pull/39410

4. **[#39452] 移除异步用户消息功能门**
   - `send_user_message_async` 不再受功能开关限制，只要模型支持即可暴露给 root agents。同时保留 `send_async_message` 作为兼容性 flag，避免破坏现有配置。
   - https://github.com/openai/codex/pull/39452

5. **[#39404] 支持旧版系统 Bubblewrap 的 FD 挂载**
   - 系统 Bubblewrap 缺少 `--ro-bind-fd` 时，检测后回退到旧

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-20

## 今日速览

昨日发布 v0.57.0-preview.0（修复 OAuth 代理与 IDE 连接问题）及稳定版 v0.56.0。社区讨论焦点集中在 subagent 可靠性（误报成功、挂起）、模型不主动复用自定义 skills/subagents 以及 Auto Memory 系统的效率与安全性上。PR 方面最值得注意的是添加了 Gemini 3.7 Flash / 3.6 Flash 模型配置支持，以及多项针对 Whisper、沙箱和符号链接处理的修复。

---

## 版本发布

### v0.57.0-preview.0
- **fix(core)**：为 OAuth 流程动态解析 Cloud Workstations 代理重定向 URI（[#28688](https://github.com/google-gemini/gemini-cli/pull/28688)，@amelidev）
- **fix(core)**：解决 IDE 连接中被吞掉的目录不匹配问题
- 完整链接：[v0.57.0-preview.0](https://github.com/google-gemini/gemini-cli/releases/tag/v0.57.0-preview.0)

### v0.56.0（稳定版）
- 自 v0.55.1 以来的累计变更，完整 Changelog：[v0.55.1...v0.56.0](https://github.com/google-gemini/gemini-cli/compare/v0.55.1...v0.56.0)

### v0.56.0-nightly.20260819.g571851b10
- 添加 Vertex AI locations 文档链接（修复 #28050，[@joneba-google](https://github.com/google-gemini/gemini-cli/pull/28865)）
- 在 agents 模式禁用时阻止 subagents 运行（修复 #22093）

---

## 社区热点 Issues

### 1. Subagent 在 MAX_TURNS 后误报 GOAL 成功 ⭐ P1
[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — `codebase_investigator` 子代理在达到最大轮次限制、未做任何分析的情况下，仍报告 `status: "success"` 和 `Termination Reason: "GOAL"`，掩盖了实际的中断。**12 条评论**，社区高度关注。这直接关系到代理结果的可信度，是调试和自动化场景中的关键可靠性问题。

### 2. Generalist agent 无限期挂起 ⭐ P1
[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — 当 `gemini-cli` 委托给 generalist agent 时，即使是简单的文件夹创建操作也会永久挂起（用户最长等待 1 小时）。指示模型不要 defer 给子代理即可解决。**8 条评论、8 👍**，是最多开发者遇到的痛点之一。

### 3. 零依赖 OS 沙箱与后执行意图路由
[#19873](https://github.com/google-gemini/gemini-cli/issues/19873) — 提议利用 Gemini 3 模型原生的 bash 亲和力（POSIX 工具链），通过零依赖沙箱在保持安全的同时充分发挥模型能力。**8 条评论**，属于 P2 enhancement，但反映了社区对"模型以自然方式工作 vs 安全限制"之间平衡的关切。

### 4. 组件级评估体系 ⭐ P1
[#24353](https://github.com/google-gemini/gemini-cli/issues/24353) — 在已有 76 个行为评估测试的基础上，构建组件级评估体系，覆盖 6 个受支持的 Gemini 模型配置。**7 条评论**。这是工程化的重大方向，意味着 Gemini CLI 正在从功能开发走向系统化质量保障。

### 5. AST 感知文件读取的研究 ⭐ P2
[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) — 一系列调研：AST 感知的文件读取、搜索和代码库映射是否值得做。潜在收益包括单次工具调用即可精确读取方法边界、减少 tokens 浪费。**7 条评论**。与 #22746（AST 感知 CLI 工具映射代码库）联动，属于长期投资方向。

### 6. 模型不会主动使用自定义 skills 和 subagents
[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — 用户反馈即便有描述清晰的 gradle/git 等自定义 skills/subagents，Gemini 几乎从不主动触发，必须显式指令才会用。**6 条评论**。这验证了许多开发者的体感——如果用不上用户配置的工具，agent 框架的价值就大打折扣。

### 7. Auto Memory 对低信号会话无限重试
[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) — 只有当提取代理成功读取 transcript 时，候选会话才被标记为已处理；若代理认为低信号而不读，该会话会被反复重新呈现。**5 条评论**。属于内存系统的效率缺陷，可能造成后台资源浪费。

### 8. Shell 命令执行卡在 "Waiting input" ⭐ P1
[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — 简单 CLI 命令执行完成后，界面仍显示命令处于活动状态并提示"等待用户输入"。**4 条评论、3 👍**，P1 优先级。这是交互体验方面的明显 bug，频繁出现。

### 9. symlink agent 文件不被识别
[#20079](https://github.com/google-gemini/gemini-cli/issues/20079) — `~/.gemini/agents/filename.md` 是符号链接时不会被识别为 agent。**4 条评论**。对使用 dotfiles 管理工具（如 chezmoi、GNU Stow）的用户影响较大。

### 10. ctrl+o 展开 subagents 时滚动卡顿（新）
[#28921](https://github.com/google-gemini/gemini-cli/issues/28921) — 使用 ctrl+o 展开多代理任务视图时，终端快速滚动抖动，文字完全不可读。**1 条评论**，昨日刚创建，属于较新的 UI 问题。

---

## 重要 PR 进展

### 1. 添加 Gemini 3.7 Flash / 3.6 Flash / 3.5 Flash-Lite 模型配置 ⭐
[#28910](https://github.com/google-gemini/gemini-cli/pull/28910) — 在 `packages/core` 和 `packages/cli` 中完整配置并支持 Gemini 3.7 Flash、3.6 Flash 和 3.5 Flash-Lite 的模型解析与选择。**当前最大性的功能性 PR**，意味着轻量级模型阵营即将全面可用。（注意：该 PR 已被关闭，可能因流程或合并原因）

### 2. 恢复暂停的 stdin 流（终端能力检测后）
[#28889](https://github.com/google-gemini/gemini-cli/pull/28889) — 修复 `detectCapabilities()` 临时挂载 `data` 监听器后，未恢复 stdin 为暂停模式的问题（修复 #28799）。**P1 优先级**，解决了终端会话中的输入流异常。

### 3. 扩展更新需明确征求环境变更同意
[#28863](https://github.com/google-gemini/gemini-cli/pull/28863) — 将 MCP 服务器环境配置纳入同意字符串，并过滤可能改变运行时行为的环境变量，防止扩展在用户不知情的情况下注入环境变量。**安全相关的重要加固**。

### 4. 重试 nudge 注入保持前缀缓存
[#28914](https://github.com/google-gemini/gemini-cli/pull/28914) — 将 on-retry nudge 从 `systemInstruction` 移到 `contents` 末尾（用户轮次后缀），既保持静态前缀缓存，又让模型在生成前立即看到恢复提示。**性能与行为正确性的双重优化**（修复 #28909）。

### 5. Whisper 转录 stdout 分块缓冲修复
[#28916](https://github.com/google-gemini/gemini-cli/pull/28916) — 在 `WhisperTranscriptionProvider` 中引入行缓冲，解决跨 `data` 事件被拆分的带时间戳转录行被丢弃的问题（修复 #28648）。**本地语音模式的稳定性修复**。

### 6. Whisper 模型下载的失败原子性
[#28917](https://github.com/google-gemini/gemini-cli/pull/28917) — `downloadModel()` 写入临时文件，尊重背压、处理流错误、校验长度、失败时清理、最后原子重命名。防止中断/失败导致模型文件损坏（修复 #28644）。**质量工程的正规化动作**。

### 7. 符号链接一致性：.geminiignore / .gitignore 路径处理
[#28915](https://github.com/google-gemini/gemini-cli/pull/28915) — 确保忽略规则同时基于字面路径和真实路径（resolved canonical path）求值，消除符号链接导致的工具行为不一致。**对 monorepo/多仓库开发尤为关键**。

### 8. GCS 轨迹记录与产物保留
[#28922](https://github.com/google-gemini/gemini-cli/pull/28922) — 为代理执行（编码、评估、修复循环）实现 GCS 轨迹记录器与 debug 产物存储。**服务生产与评估场景的可观测性基础设施**，便于事后分析和调试。

### 9. 允许重命名当前聊天会话
[#28907](https://github.com/google-gemini/gemini-cli/pull/28907) — 新增 `/chat rename <title>` 和 `/resume rename <title>` 命令，复用现有 `ChatRecordingService.saveSummary()` 存储路径。**

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报
**2026-08-20**

---

## 1. 今日速览

过去 24 小时内，Copilot CLI 密集发布 3 个补丁版本（v1.0.81-2 → v1.0.81-4），官方仅标注 "Fixes and changes"。社区讨论热度集中在两大方向：**沙箱强制启用与权限配置冲突**（#4522、#4521）和 **MCP OAuth 认证回归**（#4480、#4490）。此外，GHEC 数据驻留租户在非交互模式下出现 401 认证失败（#4527），影响企业用户。

---

## 2. 版本发布

| 版本 | 说明 |
|---|---|
| [v1.0.81-4](https://github.com/github/copilot-cli/releases/tag/v1.0.81-4) | Fixes and changes |
| [v1.0.81-3](https://github.com/github/copilot-cli/releases/tag/v1.0.81-3) | Fixes and changes |
| [v1.0.81-2](https://github.com/github/copilot-cli/releases/tag/v1.0.81-2) | Fixes and changes |

24 小时内连续发布 3 个补丁版本，说明上游正在快速修复 1.0.81 系列引入的回归问题。结合 Issue 区反馈，沙箱与 MCP 相关修复大概率包含其中。建议开发者关注 changelog 更新。

---

## 3. 社区热点 Issues

### 🔥 沙箱（Sandbox）问题集中爆发

**[#4522] Copilot CLI 1.0.81 在托管策略未决时强制启用沙箱，忽略 `sandbox.enabled=false`** — [链接](https://github.com/github/copilot-cli/issues/4522)
- 作者：@dfederm | 👍 7 | 评论 2
- **为什么重要**：用户显式禁用沙箱，但 CLI 在服务器托管策略"临时未决"状态下仍强制启用。这是当前沙箱争议中最尖锐的配置覆盖问题，可能导致企业环境中的意外行为。
- **社区反应**：👍 数量高，说明多人遇到相同问题；讨论集中在策略轮询机制应尊重本地配置。

**[#4521] 沙箱无法被禁用** — [链接](https://github.com/github/copilot-cli/issues/4521)
- 作者：@hahahahahaiyiwen | 👍 4 | 评论 2
- **为什么重要**：配置界面显示"沙箱已禁用"，但运行时状态仍显示"已启用"，配置与实际执行行为不一致。疑似 1.0.81 的沙箱状态同步缺陷。
- **社区反应**：与 #4522 互相印证，沙箱配置在 1.0.81 中存在普遍的状态判定问题。

**[#4524] [已关闭] 沙箱导致 Copilot 无法使用 git** — [链接](https://github.com/github/copilot-cli/issues/4524)
- 作者：@logar16 | 评论 3
- **为什么重要**：即使用户启用了整个工作目录和 `~/.copilot`，沙箱仍阻止 git 命令执行。该问题已关闭，说明可能是快速修复或重复问题，但暴露了沙箱权限模型对 git 操作的过度限制。

**[#4516] JVM 进程不遵循沙箱 RW 路径授权** — [链接](https://github.com/github/copilot-cli/issues/4516)
- 作者：@pavsindelar | 评论 0
- **为什么重要**：通过 `/sandbox` 配置的路径 RW 许可（如 `~/.m2/repository`）在 JVM/Java 进程中无效，Maven、javac 等工具仍报 `Operation not permitted`。沙箱对 JVM 子进程的隔离机制存在缺陷，影响 Java 生态开发者。
- **社区反应**：暂无评论，属于新提交的细分问题。

### 🔥 MCP 生态：OAuth 与协议兼容性

**[#4480] Atlassian MCP OAuth 失败："Incompatible authorization server"（1.0.79 回归）** — [链接](https://github.com/github/copilot-cli/issues/4480)
- 作者：@jfrost-fabric | 👍 6 | 评论 6
- **为什么重要**：1.0.79 起连接 Atlassian 远程 MCP 服务器时，OAuth 发现流程报 RFC 8414 §3.3 错误。1.0.71 可用，明显是回归。MCP 远程服务器用户受影响。
- **社区反应**：6 条讨论，社区在对比 1.0.71 与 1.0.79 的 OAuth 元数据获取逻辑差异。

**[#4490] Atlassian MCP OAuth 在 1.0.80 中仍然损坏** — [链接](https://github.com/github/copilot-cli/issues/4490)
- 作者：@ChandrasekarCK | 评论 4
- **为什么重要**：#4480 的姊妹 Issue，确认 1.0.80 未修复该回归。两个 Issue 合并看，MCP OAuth 发现逻辑已连续两个版本异常。

**[#4525] 1.0.81-1 在 `server/discover` 成功后发送旧版 `initialize`，导致 -32022** — [链接](https://github.com/github/copilot-cli/issues/4525)
- 作者：@dmbutko | 评论 1
- **为什么重要**：与 Python MCP SDK 2.0.0 双协议运行器交互时，CLI 先发出现代 `server/discover` 探测，随后又发送旧版 `initialize`，被服务器拒绝。协议协商逻辑存在"双轨发送"bug。
- **社区反应**：技术细节讨论中，涉及 MCP 协议版本协商的时序问题。

**[#4526] MCP 强制重新认证对非微软 OAuth 服务器附加 `prompt=select_account`** — [链接](https://github.com/github/copilot-cli/issues/4526)
- 作者：@shulkx | 评论 0
- **为什么重要**：非微软 OIDC 服务器不识别 `select_account` prompt，强制重认证流程被破坏。说明 CLI 在 OAuth 参数处理上写死了微软特定逻辑。

### 💡 其他重要问题

**[#2082] Linux 上 Ctrl+Shift+C 无法复制到剪贴板（自 v1.0.4 起）** — [链接](https://github.com/github/copilot-cli/issues/2082)
- 作者：@MasonMcV | 👍 12 | 评论 24 | 创建于 2026-03-16
- **为什么重要**：这是**历时最久、讨论最激烈**的 Issue 之一。Ubuntu 24.04 下几乎全部终端都支持 `ctrl+shift+c` 复制，但 Copilot CLI 自 v1.0.4 起失效。虽然新增了 `ctrl+c` 和右键复制，但用户对标准快捷键回归极为不满。

**[#4390] [已关闭] 启用的组织模型未出现在目录中（Claude Sonnet 5/Opus 5、Kimi K3）** — [链接](https://github.com/github/copilot-cli/issues/4390)
- 作者：@Rogn | 👍 7 | 评论 15
- **为什么重要**：Copilot Business 组织显式启用的模型（Anthropic、Kimi 系列）在 CLI 目录中不可用，选择 `claude-sonnet-5` 报 "This model is disabled"。问题已关闭，但 15 条评论说明企业模型目录同步机制曾深度影响用户。

**[#4527] GHEC 数据驻留租户在 `copilot -p` 时 401，交互模式正常** — [链接](https://github.com/github/copilot-cli/issues/4527)
- 作者：@AvitalLivshits | 评论 0
- **为什么重要**：企业用户使用 GHEC 数据驻留（`<tenant

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-08-20

## 1. 今日速览

今日社区相对平静：过去 24 小时内无新版本发布、无活跃 PR。但一条关于 **ACP 会话中 Grep/Glob 工具被系统阻止** 的 Issue 被关闭，反映了当前 ACP 模式在工具进程隔离策略上的关键限制，值得 ACP 客户端（如 Zed）用户关注。

## 2. 版本发布

无新版本发布。当前最新版本为 kimi-code CLI 0.37.1。

## 3. 社区热点 Issues

> 说明：过去 24 小时仅有 1 条更新 Issue，以下为全部内容。由于数据量不足，未达 10 条标准，特此说明。

### #2609 [已关闭] ACP 模式下 Grep/Glob 被阻止："ACP runtime only supports interactive Bash tool processes"

- **作者**: @SolomonFang
- **状态**: 已关闭（创建 2026-08-19，更新 2026-08-19），0 评论，0 👍
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2609
- **摘要**: 在 macOS 上通过 Zed 使用 `kimi acp` 启动 ACP 会话时，内置 `Grep` 和 `Glob` 工具始终报错 `ACP runtime only supports interactive Bash tool processes`。`Read` 工具正常工作，但搜索类工具完全不可用，严重影响基于 ACP 的代理式编码体验。
- **重要性**: 该 Issue 触及 ACP（Agent Client Protocol）运行时对非交互式 Bash 进程的限制。虽然已被关闭，但问题本身可能代表当前架构下搜索类工具的刚性约束，对重度依赖 Grep/Glob 进行代码导航的用户影响显著。关闭原因未在摘要中说明，社区后续是否提出替代方案有待观察。

## 4. 重要 PR 进展

过去 24 小时内无活跃 PR。

## 5. 功能需求趋势

基于当前唯一 Issue，社区关注点集中在以下方向：

- **ACP 工具链完整性**：用户期望在 ACP 会话中，Grep/Glob 等静态搜索工具与 Read 工具一样可靠可用。目前策略性限制导致工具间能力不对等，可能驱使其在未来的 ACP 运行环境中引入更细粒度的进程权限模型。

## 6. 开发者关注点

- **工具可用性一致性**：开发者对同一协议下不同内置工具的支持程度存在差异非常敏感，此类不一致会直接影响代理工作流的自动化程度。
- **错误提示可操作性**：当前错误信息虽明确，但未提供绕过或降级方案。开发者希望获得更友好的指引，例如回退到 bash 命令或调整配置的明确建议。

---
*注：因今日数据量极少，以上报告已如实反映信息全貌，未做任何虚构扩充。建议持续关注 #2609 是否被重新讨论或引发后续架构调整。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-20

## 今日速览

今日社区最集中的声音指向 **OpenCode Go 订阅计费不透明与配额异常消耗**，多位用户报告本地统计与实际扣费严重不符，成为当前最尖锐的信任危机；同时，provider 流中断被静默记录为正常完成（#37852）以 56 个 👍 稳居热榜，直接影响结果可靠性。V2 分支的 TUI/客户端体验改进（粘贴、乐观渲染、命令附件化）贡献了今日最活跃的 PR 流。

## 社区热点 Issues（10 个）

1. **[#37852] Provider 流中断被静默记录为正常停止**（👍 56 · 评论 19）
   流中断时无 finish reason/usage，却以 `finish=unknown` 结束并空手退出 agent 循环，无任何错误抛出。Subagent 因此返回空结果且无迹可查。社区高赞表明此问题触及 "AI 结果可信性" 底线。
   https://github.com/anomalyco/opencode/issues/37852

2. **[#41976] Go 订阅：$60 月配额 6 天耗尽，本地仅记录 $14.80**（评论 4）
   缓存读取计费不可见、未文档化，本地费用计量器与仪表盘严重不一致。已影响付费用户的信任，且并非孤例（见 #43416、#43424、#43409、#43387）。
   https://github.com/anomalyco/opencode/issues/41976

3. **[#3028] 一键为所有 agent 切换模型**（评论 15）
   用户期望切换模型时默认同时作用于 PLAN+BUILD/所有 agent，目前需逐模式手动切换、极易遗漏。已在 2025 年提出但持续活跃，说明该功能是真实高频诉求。
   https://github.com/anomalyco/opencode/issues/3028

4. **[#25848] 会话手动重命名**（评论 13）
   请求支持 `/rename` 或 `opencode session rename` 方式重命名会话，便于多会话管理。需求发布时间早（5 月）、至今未实现，社区仍在跟进。
   https://github.com/anomalyco/opencode/issues/25848

5. **[#9296] Plan 模式交接 Build 时错误保留 plan agent 的模型配置**（👍 11 · 评论 8）
   已配置不同模型（如 plan 用 GTP-5.2、build 用 opus-4.5），交接后 build 仍沿用 plan 模型，打破用户预期。触发对 agent 模型继承语义的讨论。
   https://github.com/anomalyco/opencode/issues/9296

6. **[#43367] gpt-5.6-sol-fast subagent 因注入 `prompt_cache_retention` 失败**（👍 10 · 评论 2）
   三种 review subagent 在工具执行后全部中断，原因是 OpenCode 发送了模型不支持的选项。Variant `max` 场景下兼容性风险暴露。
   https://github.com/anomalyco/opencode/issues/43367

7. **[#39876] libopentui 临时文件占用 207 GiB**（评论 3）
   约 5.9 万个 `libopentui.dylib` 拷贝残留在 `$TMPDIR`，几近撑爆磁盘。属于资源管理类 bug，但影响面大、易触发。
   https://github.com/anomalyco/opencode/issues/39876

8. **[#43295] Web UI V2 输入区控件遮挡发送按钮**（评论 4）
   窄屏下 agent/model/variant 选择器与发送按钮重叠，点按发送可能误开选择器。新 UI 的响应式适配 bug。
   https://github.com/anomalyco/opencode/issues/43295

9. **[#36604] TUI detach 后权限/提问 prompt 丢失，会话卡死**（评论 3）
   Agent 在后台等待回复，但 reattach 后界面无任何提示、输入看似空闲。tmux 工作流用户的直接影响。
   https://github.com/anomalyco/opencode/issues/36604

10. **[#40253] Deepseek V4 FLASH (New) 在 OpenCode Go 不可用**（评论 6）
    连续三天报错，提示模型仅限中国大陆托管并需 opt-in。属于模型可用性争议，影响 Go 订阅用户的模型选择空间。
    https://github.com/anomalyco/opencode/issues/40253

---

## 重要 PR 进展（10 个）

1. **[#43535] 修复插件工具 schema 误校验、branded ID 输入与 TUI 默认模型显示**
   解决从另一 agent 会话驱动 opencode 时 `session.create` 合法输入被拒（虚假的 `Expected a value with a length of at least 1`）、品牌化 ID 校验失败和默认模型显示错误三个 bug。
   https://github.com/anomalyco/opencode/pull/43535

2. **[#43520] 客户端乐观 prompt 提交（client-minted 幂等 ID）**
   Prompt 发送全局幂等化，输入即渲染，无需新增端点。大幅改善高延迟网络下的输入响应体验。
   https://github.com/anomalyco/opencode/pull/43520

3. **[#43528] 在 TUI 中以附件形式渲染斜杠命令**
   此前提交 `/mycmd hello` 后只保存展开文本，模型内容是对的但 UI 暴露模板细节。改为将命令作为一等附件渲染，语义更清晰。
   https://github.com/anomalyco/opencode/pull/43528

4. **[#43498] 修复 Vertex Anthropic 工具延续性（tool continuation）丢失**
   Vertex 在工具结果后遇到原生 system message 会返回 404，PR 针对该特定序列调整消息组织方式。
   https://github.com/anomalyco/opencode/pull/43498

5. **[#43479] 隔离 Gemini function-response turn**
   阻止 Gemini 系统更新被合并进包含函数响应的 user turn，满足 Gemini 对 function response 的独立 turn 要求。
   https://github.com/anomalyco/opencode/pull/43479

6. **[#42811] 会话 viewed/unread 状态核心化**
   将 unread 状态从各 TUI 本地 tab 文件提升为 Session 层事实，解决多客户端状态不一致。
   https://github.com/anomalyco/opencode/pull/42811

7. **[#43522] 消除 V2 CI 不稳定竞态**
   修复过去两天测试运行和本地压力测试中可复现的 CI 竞态：TUI 插件重复激活、CLI 子进程测试受开发者真实配置干扰等。
   https://github.com/anomalyco/opencode/pull/43522

8. **[#37813] Code Mode 进度更新批量化（100ms coalescing）**
   将累积的 child-call 元数据每 100ms 合并发布，替代每次 start/end 都触发一次发布，降低 TUI 与后端的更新压力。
   https://github.com/anomalyco/opencode/pull/37813

9. **[#37809] 修复 console `/auth/authorize` 开放重定向（CWE-601）**
   对 `continue` 参数进行校验，防止构造恶意 URL 实施钓鱼跳转。安全类修复。
   https://github.com/anomalyco/opencode/pull/37809

10. **[#37752] 序列化 v2 session 回滚**
    防止 session runner 在回滚暂存期间恢复执行，并在新 prompt 接入前提交已暂存回滚。修复回滚与恢复并发时的状态错乱。
    https://github.com/anomalyco/opencode/pull/37752

---

## 功能需求趋势

- **会话管理增强**：会话重命名（#25848）、viewed/unread 状态（#42811）、桌面端支持 Tab/Shift+Tab 切换 agent（#41742）与 Review 模式快捷键（#43408）——社区期待更完善的会话与交互控制，而非仅聊天功能。
- **计费透明性**：Go 订阅配额消耗不透明、缓存读取计费未展示（#41976、#43424、#43409、#43387、#43416）——用户需要实时可见的计费细节与一致性。
- **多模型/多 agent 配置体验**：一键切换所有 agent 模型（#3028）、plan→build 模型交接语义修正（#9296）——减少配置心智负担。
- **TUI 可用性打磨**：Ctrl+V 粘贴到 "Type your own answer"（#43516）、diff 半页滚动自定义（#43267）、detach 后 prompt 保持（#36604）——深挖终端交互细节。
- **MCP 稳定性**：V2 空闲后 Atlassian/GitHub rate limit（#43530）、本地 MCP 命令崩溃导致服务 crash-loop（#43257）——MCP 生态的可靠性问题开始显现。

## 开发者关注点

- **计费信任危机（Go 订阅）**：至少 5 个 issue 指向同一问题——本地 usage 统计与云端配额扣除差异巨大，缓存读取计费 "隐形"，用户无法信任成本数据。
- **静默失败不可接受**：#37852 高赞排第一，流中断不报错、subagent 返回空结果——比报错更危险，开发者明确要求 "要么有文本，要么有错误"。
- **桌面端与 TUI 功能差距**：审查不显示（#43485）、快捷键冲突（#43408）、缺少声音/通知提醒

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*