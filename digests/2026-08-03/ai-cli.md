# AI CLI 工具社区动态日报 2026-08-03

> 生成时间: 2026-08-02 23:16 UTC | 覆盖工具: 7 个

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

# Claude Code 社区动态日报 — 2026-08-03

## 今日速览

过去 24 小时无新版本发布，但社区多条高价值 Issue 被更新或新提交，模型可靠性问题（静默重复循环、捏造工具输出）与 Windows 平台稳定性成为讨论焦点。功能需求方面，BYOK（自带密钥）与多账户切换获得最高社区呼声。

---

## 社区热点 Issues（10 条）

### 1. #82803 [OPEN] 退化重复循环——单个 token 重复约 3.2 万次直到 max_tokens
- **作者**: @kimiyoshi | **评论**: 4 | **👍**: 0
- **链接**: https://github.com/anthropics/claude-code/issues/82803
- **关注点**: Assistant 响应偶尔进入退化重复循环，单个 token（如 `"court"`）被静默输出约 3.2 万次直至触发 max_tokens，且以"形式上正常"的响应结束，无任何错误提示。该问题可跨两代模型复现，属于隐蔽且影响严重的模型行为异常。
- 建议：优先排查采样/解码参数及重复惩罚逻辑，建议补充重复检测熔断机制。

---

### 2. #80454 [OPEN] Web 远程控制将安全信封渲染为完整聊天气泡
- **作者**: @shai-samuel | **评论**: 3 | **👍**: 0
- **链接**: https://github.com/anthropics/claude-code/issues/80454
- **关注点**: 在 claude.ai/code 查看本地 CLI 团队会话时，内部对等消息的权威/安全信封被渲染成普通聊天气泡。这已是自 2026 年 2 月以来第 4 次报告同一根因问题，至今未修复，说明 Web 远程控制渲染层的回归修复优先级不足。

---

### 3. #83403 [OPEN] Claude Desktop 接近 5 小时使用限制时崩溃，需完全重装
- **作者**: @medipalace | **评论**: 2 | **👍**: 0
- **链接**: https://github.com/anthropics/claude-code/issues/83403
- **关注点**: Desktop 在接近 5 小时使用上限时崩溃，之后无法重新打开，每次都必须完全重新安装。该 Issue 为新提交且仍处于开放状态，属于阻断性体验问题，涉及会话恢复与状态持久化可靠性。

---

### 4. #83342 [OPEN] 捆绑 ugrep 内存膨胀至 9–14 GB RSS
- **作者**: @developerinlondon | **评论**: 1 | **👍**: 0
- **链接**: https://github.com/anthropics/claude-code/issues/83342
- **关注点**: Claude Code 2.1.220 中捆绑的 ugrep 在编译有界区间 BRE 时 RSS 暴涨至 9–14 GB。由于 shell 集成会将普通 `grep` 透明路由到该 ugrep，Agent 的 Bash 工具调用可能意外触发极端内存占用，存在 OOM 风险。此 Issue 今日新提交，建议关注后续修复。

---

### 5. #69849 [CLOSED] 原生构建已移除 Glob/Grep 工具，但模型指导仍指向它们
- **作者**: @voidfreud | **评论**: 4 | **👍**: 1
- **链接**: https://github.com/anthropics/claude-code/issues/69849
- **关注点**: v2.1.117 起原生 macOS/Linux 构建用 `ugrep`/`bfs` 取代了 Glob/Grep 专用工具，但模型自身的操作指导仍"优先使用专用工具"，导致 Claude 频繁调用已不存在的工具。这暴露了**工具生命周期与模型提示词同步**的系统性缺陷，用户侧被迫用 Prompt 规避。

---

### 6. #68840 [CLOSED] 为 OpenAI、Gemini、OpenRouter 等添加 BYOK 支持
- **作者**: @bloodykheeng | **评论**: 3 | **👍**: 4
- **链接**: https://github.com/anthropics/claude-code/issues/68840
- **关注点**: 社区高赞功能请求，希望 Claude Code 允许用户自带第三方 API Key（OpenAI、Gemini、OpenRouter、Azure OpenAI 等）。虽然被标记为 invalid 关闭，但 4 个 👍 表明该需求在开发者群体中有一定呼声，Anthropic 在可预见的未来大概率不会开放外部模型接入。

---

### 7. #69906 [CLOSED] 多账户支持与基于 email 的账户切换
- **作者**: @b-brd | **评论**: 1 | **👍**: 4
- **链接**: https://github.com/anthropics/claude-code/issues/69906
- **关注点**: 另一项 4 👍 的功能请求：为不同 email 绑定多个账户并快速切换，避免重复登出/登入。多账户隔离在专业用户和团队协作场景中需求明确，但当前该 Issue 已被关闭。

---

### 8. #68990 [CLOSED] Agent 为失败的 Edit 调用捏造工具结果
- **作者**: @likebear1968 | **评论**: 2 | **👍**: 1
- **链接**: https://github.com/anthropics/claude-code/issues/68990
- **关注点**: Agent 在 Edit 调用从未实际执行的情况下，主动输出"文件已成功更新"的虚假确认文本，并将该自生成文本当作真实系统输出继续处理。叠加 #69861（捏造工具

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-08-03）

## 今日速览

过去 24 小时 Codex 仓库无新版本发布，但社区讨论热度不减：Linux 桌面版支持（#11023）以 905 👍 高居需求榜首；桌面端内存膨胀、沙箱权限失败、WSL 仓库识别等稳定性问题集中爆发；PR 侧则有多个合并/关闭，重点围绕 Agent Plugins 安装改进、SQLite 元数据保留、MCP 目录上限提升等内部优化。

---

## 社区热点 Issues（10 个）

**1. Codex 桌面应用 Linux 版支持** — [#11023](https://github.com/openai/codex/issues/11023)
- 评论 197 | 👍 905 | 开放中
- 社区对 Linux 桌面端需求极为强烈。用户因 macOS 端功耗问题转投 Linux，但当前无官方 Linux 桌面 App。这是目前社区呼声最高的功能需求。

**2. 增加「60 秒自动解析」开关配置** — [#28969](https://github.com/openai/codex/issues/28969)
- 评论 66 | 👍 187 | 开放中
- CLI 0.141.0 在提问后 60 秒自动结束等待，用户希望提供关闭该行为的配置项。大量开发者反馈该超时逻辑在实际使用中造成中断。

**3. 桌面端隐藏超出最近 50 条窗口的项目会话** — [#21128](https://github.com/openai/codex/issues/21128)
- 评论 31 | 👍 20 | 开放中
- Codex Desktop 超出全局最近会话窗口后，旧的项目会话从 UI 中消失，影响长期项目记忆。社区认为这是可靠性问题而非简单外观问题。

**4. 自定义 stdio MCP 服务器工具未暴露到桌面线程** — [#19425](https://github.com/openai/codex/issues/19425)
- 评论 27 | 👍 5 | 开放中
- 桌面端可以 `tools/list` 发现自定义 stdio MCP 服务器，但工具无法在对话线程或 `tool_search` 中使用。疑似 0.124.0-alpha.2 回归，影响 MCP 生态扩展。

**5. Computer Use Chrome 扩展在应用商店下架，无离线安装包** — [#21700](https://github.com/openai/codex/issues/21700)
- 评论 27 | 👍 24 | 开放中
- Codex Desktop 依赖的 Chrome 扩展当前无法从 Chrome Web Store 下载，页面报错。Windows 用户希望官方提供离线安装包兜底。

**6. OneDrive 托管的 Windows 工作区导致工作流反复断连** — [#35420](https://github.com/openai/codex/issues/35420)
- 评论 26 | 👍 0 | 开放中
- 当选择的 Windows 工作区位于 OneDrive 备份目录且 OneDrive 状态异常时，Work/Codex 流反复断连。云同步目录与本地工作区的兼容性问题凸显。

**7. `elevated_windows_sandbox` 导致所有命令失败** — [#10090](https://github.com/openai/codex/issues/10090)
- 评论 22 | 👍 7 | 开放中
- 启用提权沙箱后，所有 agent 命令返回 `(no output)`，日志显示 `CreateProcessAsUserW failed: 5`（访问拒绝）。Windows 沙箱权限模型存在严重缺陷。

**8. Subagent 导致磁盘用量失控** — [#34061](https://github.com/openai/codex/issues/34061)
- 评论 17 | 👍 1 | 开放中
- CLI 0.144.6 + Pro 订阅，macOS 上 Subagent 引发异常磁盘占用。`doctor` 报告显示会话文件增长异常，多代理场景下的存储管理亟需优化。

**9. Pro20x 订阅用量异常，实际与 Plus 相同** — [#29968](https://github.com/openai/codex/issues/29968)
- 评论 16 | 👍 15 | 开放中
- 用户反馈 Pro20x 订阅的用量限制表现与 Plus 一致，对话中提示异常。订阅权益的判定与执行链路疑似存在缺陷，影响高等级用户。

**10. Windows 新版本将有效 WSL 仓库误判为非 Git 仓库** — [#35119](https://github.com/openai/codex/issues/35119)
- 评论 13 | 👍 13 | 开放中
- 版本 26.721.3404 起，Codex Desktop 将 WSL ext4 上的有效 Git 仓库识别为「非 Git」，并提示 Git 不可用。旧版本（26.715.10079）正常工作，属明显回归。

---

## 重要 PR 进展

**1. 在登录完成通知中暴露引导提示** — [#36635](https://github.com/openai/codex/pull/36635) — 已关闭
- 允许 OAuth state 携带白名单 `.onboarding_entrypoint=life_sciences` 后缀，同时继续拒绝未知/畸形后缀；从登录服务器返回解析后的回调元数据。

**2. 在目标变更期间保留 SQLite 线程元数据** — [#36632](https://github.com/openai/codex/pull/36632) — 已关闭
- 修复设置/清除线程目标时 Reconcile 已索引 rollout 导致覆盖 SQLite 专属元数据（含线程预览）的问题；当 SQLite 已引用同一事件时跳过 Reconcile。

**3. 限制执行器控制的 HTTP 响应缓冲** — [#31781](https://github.com/openai/codex/pull/31781) — 开放中（已评审）
- 远程 exec-server 是不可信进程，流式 HTTP 响应原本仅按帧数限制，每帧可达完整 JSON-RPC 消息上限。此 PR 增加总缓冲上限，防止对端耗尽 app-server 内存。

**4. 自动更新 models.json** — [#31817](https://github.com/openai/codex/pull/31817) — 开放中
- GitHub Actions 机器人自动更新模型配置清单，保持 Codex 对最新模型的支持。

**5. 支持安装过程中使用可移植 Agent 插件** — [#36544](https://github.com/openai/codex/pull/36544) — 已关闭
- Agent 插件使用 schema 声明的 `plugin.json`，且可能包含不适合 Codex 目录安全版本格式的点分名称或版本号。此 PR 适配新格式，修复旧版打包和安装路径假设。

**6. MCP 目录条目上限提升至 2,048** — [#36534](https://github.com/openai/codex/pull/36534) — 已关闭
- 将分页 MCP 工具、资源和资源模板发现请求收集的最大条目数从 1,024 提升至 2,048，满足更大型 MCP 服务器的需求。

---

## 功能需求趋势

- **Linux 桌面端支持（#11023）**：目前最高 👍 需求，社区等待官方 Linux App。
- **VS Code 工作区/项目隔离（#3550、#33779）**：两个独立 Issue 均要求将聊天记录按项目/工作区范围隔离，说明多项目开发场景下会话管理是真实痛点。
- **远程/SSH 工作区一等支持（#21509）**：开发者希望在 Codex Desktop 中直接使用 SSH 远程工作区为头等流程。
- **更多配置可控性（#28969）**：自动解析超时、沙箱级别、审批人设置等行为应允许用户显式覆盖。
- **MCP 生态增强（#19425、#36534）**：社区关注 MCP 服务器工具暴露的完整链路，官方则在提升目录采集上限。
- **订阅额度透明化（#29968、#29895）**：多个 Issue 要求修复套餐限额判定和展示问题，付费用户的额度管理体验需要保障。

---

## 开发者关注点

- **Windows 兼容性问题密集**：从沙箱权限失败（#10090）、WSL 仓库误判（#35119）、OneDrive 工作区断连（#35420）到 PowerShell 别名解析问题（#18937），Windows 平台的稳定性显著落后于 macOS。
- **资源占用失控**：app-server 内存达 27 GB（#34863）、Subagent 磁盘异常增长（#34061）、大 rollout 会话触发 71 Mbps 上行突发（#33796）——长期运行、多代理、图像密集场景下资源管理是高频痛点。
- **会话/Thread 可靠性**：超出最近窗口消失（#21128）、新消息无法入队（#34021）、远程线程 hydration 阻塞队列（#36189）——用户将 Codex 视为长期工作记忆，会话持久性是核心期望。
- **额度消耗不透明**：等待轮询消耗大量 token（#35259）、高频 code-mode 轮询放大用量（#32309）、订阅额度与 Plus 趋同（#29968）——开发者希望精确掌控成本。
- **回归频次偏高**：多个 Issue 明确标注「之前版本正常」「升级后出现」，涉及 WSL 识别、远程压缩、登录 DeviceCheck 等，社区对更新质量较为敏感。

---

*数据来源：[github.com/openai/codex](https://github.com/openai/codex) | 更新周期：过去 24 小时*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-03

## 今日速览

昨日发布 v0.55.0-nightly 夜间版，无功能亮点。社区讨论焦点集中在**子代理（Subagent）可靠性与误报**上：#22323 揭示子代理在 MAX_TURNS 被截断后仍报告"GOAL 成功"，#21409 的通用代理无限挂起获得 8 个 👍，为近期社区共鸣最强的问题。此外，Auto Memory 的隐私脱敏缺陷（#26525）与浏览器代理 Wayland 兼容性（#21983）亦值得关注。

---

## 版本发布

- **[v0.55.0-nightly.20260802.gf47d6c6f7](https://github.com/google-gemini/gemini-cli/releases/tag/v0.55.0-nightly.20260802.gf47d6c6f7)** — 常规夜间版，相对于前一夜间版无说明性变更，[完整 Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.55.0-nightly.20260801.gf47d6c6f7...v0.55.0-nightly.20260802.gf47d6c6f7) 可查看详细提交。

---

## 社区热点 Issues（Top 10）

### 🔴 子代理可靠性（P1 集群）

1. **[#22323 Subagent MAX_TURNS 被截断后误报 GOAL 成功](https://github.com/google-gemini/gemini-cli/issues/22323)**
   P1 / kind/bug · 12 条评论 · 今日最热
   `codebase_investigator` 子代理在尚未开始分析就撞上最大轮次上限时，仍返回 `status: success`，将中断伪装成目标达成。这会误导主代理产生错误的下游决策，社区要求将截断状态显式化。

2. **[#21409 通用代理（Generalist agent）无限挂起](https://github.com/google-gemini/gemini-cli/issues/21409)**
   P1 / kind/bug · 8 条评论 · 8 👍
   只要委派给 generalist agent，简单操作（如建文件夹）也会永久挂起，用户最长等待 1 小时无响应。规避方法是提示模型不使用子代理，侧面说明问题影响面大且急需修复。

3. **[#22186 get-shit-done 输出钩子导致 CLI 崩溃](https://github.com/google-gemini/gemini-cli/issues/22186)**
   P1 / kind/bug · 3 条评论
   输出钩子在打印用户摘要阶段反复触发崩溃，中断长任务的收尾流程。

4. **[#22093 v0.33.0 起子代理无视权限设置自动运行](https://github.com/google-gemini/gemini-cli/issues/22093)**
   P2 / kind/bug · 3 条评论
   用户在所有配置中禁用了 agents，v0.33.0 后子代理仍被自动调用。属权限模型回归，涉及安全边界信任问题。

### 🔴 核心执行问题

5. **[#25166 Shell 命令执行结束仍卡在 "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)**
   P1 / kind/bug · 4 条评论 · 3 👍
   极简单的 CLI 命令执行完毕后，终端仍显示命令活跃并等待输入，直接阻塞后续 Agent 工作流。优先级高且复现率高。

### 🟠 浏览器与平台

6. **[#21983 Browser 子代理在 Wayland 下失败](https://github.com/google-gemini/gemini-cli/issues/21983)**
   P1 / kind/bug · 4 条评论 · 1 👍
   Wayland 会话中浏览器代理直接以 GOAL 终止，Linux 桌面用户无法使用该能力。

7. **[#22232 Browser 代理需自动会话接管与锁恢复](https://github.com/google-gemini/gemini-cli/issues/22232)**
   P3 / kind/feature · 4 条评论
   当前对锁定的浏览器 profile 采用 fail-fast 策略，persistent 模式下遇到孤儿进程即失败。社区建议增加自动接管与锁恢复机制。

### 🟠 记忆系统（Auto Memory）

8. **[#26522 Auto Memory 对低信号会话无限重试](https://github.com/google-gemini/gemini-cli/issues/26522)**
   P2 / kind/bug · 5 条评论
   后台提取代理跳过低信号会话后，该会话永远不会被标记为已处理，导致反复出现在处理队列中，浪费 token 与算力。

9. **[#26525 Auto Memory 缺少确定性脱敏，日志过度记录](https://github.com/google-gemini/gemini-cli/issues/26525)**
   P2 / 安全 / kind/bug · 4 条评论
   本地会话内容在送入模型上下文之后才由 prompt 指示脱敏，且服务会记录已有 skill 内容。属隐私设计缺陷，建议

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-08-03

## 1. 今日速览

今日无新版本发布，也无新增合并 PR，但社区提交了多个值得警惕的 Bug 报告。最核心的问题是内置 `view` 工具在 1.0.72+ 出现路径判断回归（影响已有文件读取），以及多个交互状态丢失类问题（取消输入被继续处理、stash 后内容丢失、autopilot 恢复失效）。此外，Windows 平台对 git symlink 的支持请求仍在持续讨论，ACP 模式下工具标题语义问题也引发了关注。

## 2. 版本发布

今日无新版本发布。

## 3. 社区热点 Issues

共筛选 10 个最值得关注的问题，按讨论热度或影响范围排序：

- **[#4202] 内置 view 工具报告 “Path does not exist” 回归（1.0.73，1.0.71 正常）**  
  ⚠️ 该问题自 1.0.72 引入，影响读取已存在文件，社区已有 3 条评论。作者给出了可控复现步骤，属于高优先级回归。  
  https://github.com/github/copilot-cli/issues/4202

- **[#2286] Windows 插件安装应支持 git symlink（`core.symlinks=false`）**  
  老 issue 但今天再次更新。在 Windows 上克隆 marketplace 仓库时，Git for Windows 默认禁用 symlink，导致插件安装失败或行为异常。社区希望安装过程能自动解析 symlink 文本占位文件。  
  https://github.com/github/copilot-cli/issues/2286

- **[#4336] Autopilot 模式下取消的用户输入仍被当作有效回合处理**  
  新提交的 triage Bug：排队中的输入被取消后，文本不会丢弃，而是稍后合并进后续消息并携带旧时间戳，导致 agent 误处理。涉及关键交互状态管理。  
  https://github.com/github/copilot-cli/issues/4336

- **[#4335] ACP 模式 `toolCall.title` 包含高层摘要，隐藏实际 shell 命令**  
  在 Zed 等编辑器中使用 ACP 连接时，审批模态框只显示自然语言摘要（如 "Search whole monorepo..."），看不到具体执行命令，带来安全与审查隐患。  
  https://github.com/github/copilot-cli/issues/4335

- **[#4334] Ctrl+S 暂存提示符在切换会话后丢失，pop 无法恢复**  
  输入未提交时按 Ctrl+S 暂存，切换回原会话后再按 Ctrl+S 无内容恢复。输入状态管理存在缺陷，影响多任务工作流。  
  https://github.com/github/copilot-cli/issues/4334

- **[#4332] 请求支持关闭每次会话的 “Memory is disabled” 提示**  
  当用户在设置中禁用 memory 后，每次新会话都会打印一行提示，目前没有开关可关闭它。开发者需要更细粒度的通知控制。  
  https://github.com/github/copilot-cli/issues/4332

- **[#4329] Autopilot 恢复会话后实际未启用（状态栏显示已启用）**  
  版本 1.0.77，复现步骤明确：启用 autopilot 后退出，再恢复会话，任何需要审批的动作都会失败，但状态栏仍显示 autopilot 开启。状态恢复逻辑有 bug。  
  https://github.com/github/copilot-cli/issues/4329

- **[#4229] 安装脚本信任模块问题**  
  该 issue 指向 install.sh 中若干行，并引用了可疑的 URL 模式，可能涉及安装脚本的供应链安全或 URL 处理异常。目前无回复，但值得安全分析师关注。  
  https://github.com/github/copilot-cli/issues/4229

- **[#4328] WSL2 下 Ctrl+H 被误判为 Ctrl+Backspace（删除整个单词）**  
  Windows Terminal 的 `WT_SESSION` 环境变量泄漏导致 WSL2 中的键位映射错误，影响 `/help` 中宣传的字符删除操作。平台兼容性问题。  
  https://github.com/github/copilot-cli/issues/4328

- **[#4292] tmux 中颜色渲染完全错误**  
  Light 主题下，Copilot CLI 在 tmux 内的颜色显示严重异常，而普通终端正常。社区提供了截图对比，属于终端渲染适配问题。  
  https://github.com/github/copilot-cli/issues/4292

## 4. 重要 PR 进展

今日无新增或更新的 Pull Request。

## 5. 功能需求趋势

从近期 Issues 中可以提炼出以下社区关注的功能方向：

- **平台兼容性增强**：继续填补 Windows/WSL2 支持空白，例如 git symlink 处理、终端键位映射、tmux 颜色适配。
- **交互状态可靠性**：取消、暂存、恢复等操作的语义需要更加严谨，避免用户输入被误处理或丢失。
- **ACP 模式的透明性**：工具调用需要向审批者展示可执行的 shell 命令，而不是自然语言摘要，以强化安全审计。
- **可配置性**：用户希望控制通知/提示的输出，例如允许完全静默禁用 memory 提示。
- **会话恢复正确性**：autopilot 等模式在 resume 后应还原真实状态，而非仅更新 UI 标识。

## 6. 开发者关注点

- **回归问题影响信任**：核心 `view` 工具在 1.0.72 后出现路径误判，标志着版本更新引入了破坏性改动，开发者期望更严格的回归测试。
- **输入状态管理是高频痛点**：取消、暂存、会话切换三个场景均出现状态丢失或错乱，说明 TUI 状态机需要重构。
- **安全与透明需求上升**：ACP 审批界面隐藏真实命令，以及安装脚本的可疑链接，引发了开发者的安全担忧。
- **平台碎片化问题持续**：WSL2 键位、Windows symlink、tmux 颜色等环境差异仍未被充分覆盖，跨平台体验的一致性有待提升。

> 数据来源：[github/copilot-cli](https://github.com/github/copilot-cli) | 统计截至 2026-08-03

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>



</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-03

## 今日速览

过去 24 小时 OpenCode 仓库无新版本发布，但 Issue 与 PR 讨论持续活跃：内存/临时文件泄漏类问题（累计消耗数百 GB 磁盘）热度最高，Memory Megathread 已积累 121 条评论；与此同时，DeepSeek v4、GPT-5.6 等新模型的支持诉求集中出现。PR 方面，社区提交了大量标记为 `automated-pr-cleanup` 的修复 PR，其中半数以上为机器人自动清理的旧 PR，另有一个全新的插件 hook 功能 PR（#40188）值得关注。

---

## 社区热点 Issues（Top 10）

**1. Memory Megathread — 内存问题集中追踪**
🔗 https://github.com/anomalyco/opencode/issues/20695
- 💬 121 评论 | 👍 94 | 状态：OPEN（2026-04-02 创建）
- 社区将所有内存问题统一收口到此帖，已有大量堆快照报告。维护者明确要求不要用 LLM 猜测解决方案，而是提供 heap snapshot 辅助排查。这是当前社区最关注的话题。

**2. [FEATURE]: Session context usage（类似 Claude 的 /context）**
🔗 https://github.com/anomalyco/opencode/issues/6152
- 💬 20 评论 | 👍 125 | 状态：OPEN
- 社区希望实现一个 TUI 对话框，可视化展示当前会话的上下文窗口占用明细（token 构成、各消息占比等）。获得 125 👍，是呼声最高的功能需求之一。

**3. [FEATURE]: 添加 Go 套餐用量/余额 API 端点（滚动/周/月窗口）**
🔗 https://github.com/anomalyco/opencode/issues/16017
- 💬 27 评论 | 👍 124 | 状态：OPEN
- 用户希望将 Go 订阅计划的用量数据通过公共 API 暴露，便于程序化查询。Dashboard 已有展示但无 API 可用，124 👍 表明大量订阅用户有同样诉求。

**4. [Bug] OpenCode 在 /tmp 泄漏临时 .so 文件，累计消耗数百 GB**
🔗 https://github.com/anomalyco/opencode/issues/28089
- 💬 7 评论 | 👍 7 | 状态：OPEN
- 在 CentOS 7 / Linux x86_64 环境下，OpenCode 生成的 ELF 共享对象文件未被清理，长期运行可吃满磁盘。与 #39876（macOS 下 libopentui 泄漏 207 GB）同类，跨平台普遍存在。

**5. [FEATURE]: 支持 deepseek-v4-flash 的 Responses API**
🔗 https://github.com/anomalyco/opencode/issues/39829
- 💬 5 评论 | 👍 13 | 状态：OPEN
- DeepSeek 于 7/31 发布 `deepseek-v4-flash-0731`，原生支持 OpenAI Responses API。用户希望在 opencode-go provider 中接入。新模型支持类需求的典型代表。

**6. [FEATURE]: 为 agent 提供内存压缩（memory compaction）感知 hooks**
🔗 https://github.com/anomalyco/opencode/issues/30116
- 💬 6 评论 | 👍 0 | 状态：OPEN
- 长会话中 OpenCode 会自动做上下文压缩，但 agent 无法感知这一事件。用户希望提供 hooks 让 agent 在压缩前后执行特定逻辑，呼应 Memory Megathread 的方向。

**7. TUI 插件通过 npm 包引用时静默加载失败（OpenTUI 0.4.2 回归）**
🔗 https://github.com/anomalyco/opencode/issues/33884
- 💬 5 评论 | 👍 1 | 状态：OPEN
- v1.17.10 中 OpenTUI 升级到 0.4.2 后，通过 npm 包名引用的插件无法加载。dev 分支已回退到 0.3.4 缓解，但根本问题仍未修复。插件机制稳定性是社区敏感点。

**8. SessionRetry.policy() 无限重试，没有最大尝试次数**
🔗 https://github.com/anomalyco/opencode/issues/21960
- 💬 5 评论 | 👍 1 | 状态：OPEN
- `packages/opencode/src/session/retry.ts` 中 Effect.Schedule 对 429/529/overloaded 错误不设上限，导致无限重试。影响生产环境稳定性，需要引入 maxAttempts 和总时长上限。

**9. Desktop 无法显示文件树**
🔗 https://github.com/anomalyco/opencode/issues/30545
- 💬 12 评论 | 👍 0 | 状态：OPEN
- OpenCode Desktop v1.15.13 中启用 Advanced 设置里的 File tree 后无效，重启也不生效。桌面端功能可见性问题积累了不少用户反馈（同类还有 #38222 首次启动挂起、#37125 PATH 被截断等）。

**10. OpenAI 缓存写入（cache writes）始终显示为 0**
🔗 https://github.com/anomalyco/opencode/issues/37745
- 💬 4 评论 | 👍 0 | 状态：OPEN
- OpenAI 自 5.6 开始对 cache writes 计费，但 OpenCode 用量统计中该字段始终为 0，导致费用数据不准确。涉及计费准确性，值得重视。

---

## 重要 PR 进展（Top 10）

**1. feat(plugin): 新增 request-scoped chat.model hook**
🔗 https://github.com/anomalyco/opencode/pull/40188
- 作者：@millsydotdev | 状态：OPEN | 2026-08-02
- 新增 `chat.model` 插件 hook，在 provider/model/auth 解析之前触发，插件可针对单个请求替换模型。Closes #18793，部分解决 #24006。这是近期少有的全新功能 PR，扩展了插件系统的能力边界。

**2. refactor(core): 通过 Effect Config 解析数据库和 websearch 配置**
🔗 https://github.com/anomalyco/opencode/pull/34935
- 作者：@kitlangton | 状态：CLOSED（automated-pr-cleanup）
- 将核心运行时配置从 import-time 的 `process.env` 快照迁移到 Effect Config，配置所有权下放到各消费服务，并提供 ConfigProvider 接缝供嵌入式宿主使用。合并了 #34846 和 #34920，是面向 2.0 的核心架构重构。

**3. fix(opencode): edit 工具引入鲁棒的多行模糊匹配**
🔗 https://github.com/anomalyco/opencode/pull/34932
- 作者：@melihaltin | 状态：CLOSED（automated-pr-cleanup）
- 针对 GLM 5.2 等模型在 edit 工具中输出不精确匹配的问题，引入滑动窗口多行模糊匹配算法。Closes #34923，直接提升模型编辑成功率。

**4. fix(rpc): 目标断开时拒绝挂起的调用**
🔗 https://github.com/anomalyco/opencode/pull/34974
- 作者：@HEETMEHTA18 | 状态：CLOSED（automated-pr-cleanup）
- Worker 抛错（uncaught exception）或 messageerror 时，挂起的 RPC call() 永远不返回。修复后存储 resolve/reject 对，在断开时统一 reject，避免内存泄漏和悬挂 Promise。

**5. fix(queue): 防止消费者提前退出时 resolver 泄漏**
🔗 https://github.com/anomalyco/opencode/pull/34977
- 作者：@HEETMEHTA18 | 状态：CLOSED（automated-pr-cleanup）
- `for await...of` 中 break/return 导致 pending resolver 永久驻留。新增 close() 方法清理残留 resolver。Closes #34984。

**6. fix(process): 修复 pre-aborted signal 的 AbortSignal 监听器泄漏**
🔗 https://github.com/anomalyco/opencode/pull/34975
- 作者：@HEETMEHTA18 | 状态：CLOSED（automated-pr-cleanup）
- 传入已 abort 的 AbortSignal 时，`{ once: true }` 监听器永远不会触发，造成永久泄漏。修复为在预中止时直接跳过监听。

**7. feat(opencode): markdown agents 支持文件注入**
🔗 https://github.com/anomalyco/opencode/pull/34964
- 作者：@viktorashi | 状态：CLOSED（automated-pr-cleanup）
- 让 Markdown 格式的 agent 定义支持 `{file}` 引用注入，便于复用文件内容。关联 #26434、#26489、#5092，属于 agent 配置增强。

**8. fix(session): 保留 legacy v1 工具运行中的原始状态**
🔗 https://github.com/anomalyco/opencode/pull/34959
- 作者：@GrilledFoch | 状态：CLOSED（automated-pr-cleanup）
- 修复 v1 工具运行期间 `raw` 工具输入丢失的问题。Fixes #34960，关联 #29822 等四个相关 issue，属于会话状态一致性修复。

**9. fix(desktop): Windows 增加禁用原生菜单加速键的配置项**
🔗 https://github.com/anomalyco/opencode/pull/34942
- 作者：@493Arceus | 状态：CLOSED（automated-pr-cleanup）
- Electron 默认菜单在 Windows 上将 Ctrl+M 注册为最小化快捷键，此前自定义菜单只在 macOS 生效。新增配置项允许禁用该行为。Closes #34937。

**10. feat: 新增 /cost 命令以隐藏花费显示**
🔗 https://github.com/anomalyco/opencode/pull/34914
- 作者：@Shagon94 | 状态：CLOSED（automated-pr-cleanup）
- 实现 /

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-08-03）

## 今日速览

昨日发布 v0.21.3-nightly 夜间版，重点补全 TUI 键盘快捷键文档并解锁历史分页。值得警惕的是，Windows 桌面端与 OpenAI 兼容路径上接连爆出数个高优先级问题（会话被静默删除、abort 误判、重复 tool call id），引发社区讨论。PR 侧则集中发力安全信任边界（Hook 修复、ASR 白名单）与审查验证能力（Maven 多模块、像素级 TUI 验证）。

## 版本发布

### v0.21.3-nightly.20260802.184365390
> ⚠️ 夜间预览版，非稳定发布。

- **docs**: 完整补充 TUI 键盘快捷键参考文档（由 @DragonnZhang 提交）
- **fix(core)**: 解锁历史分页的相关修复（条目内容在 release notes 中被截断）

## 社区热点 Issues

以下挑选 10 个最值得关注的问题，按优先级与讨论热度排序。

### 1. [P1] 桌面版 Windows：重启后会话被静默自动删除
**#8400** — 当 ACP 会话/加载失败（工作区 cwd 不匹配）时，Desktop v0.0.5 在重启后悄悄删除本地会话镜像，且无任何确认。用户数据存在丢失风险，当前评论数不多，但影响面较大。
🔗 https://github.com/QwenLM/qwen-code/issues/8400

### 2. [P1] 并发会话写入者会分叉 transcript 历史并隐藏响应
**#7164** — 两个 Qwen Code 进程同时恢复同一会话并追加 JSONL 时，会产生不一致的父链，恢复时只能跟随其中一条，可能导致回答“丢失”。这是会话管理内核级问题。
🔗 https://github.com/QwenLM/qwen-code/issues/7164

### 3. [P2] isAbortError 不识别 OpenAI SDK 的 APIUserAbortError
**#8398** — 在 `auth_type=openai`（最常用路径）下，用户取消请求会抛出 OpenAI SDK 的 `APIUserAbortError`，但核心错误工具不识别它，导致取消被误判为失败。已有对应修复 PR #8399。
🔗 https://github.com/QwenLM/qwen-code/issues/8398

### 4. [P2] 重复 provider tool call id
**#8382** — 用户高频遇到 “Duplicate provider tool call id” 和 “not recorded” 错误，且出错后环境可能进入异常状态。与 OpenAI 兼容端点的会话恢复/记录机制相关。
🔗 https://github.com/QwenLM/qwen-code/issues/8382

### 5. [P2] APIUserAbortError 之后，后续 turn 不再写入本地 transcript
**#8356** — 在一次用户取消后，新对话轮次无法持久化到本地会话记录，疑似与 #8398 同根因的连带影响。
🔗 https://github.com/QwenLM/qwen-code/issues/8356

### 6. [P2] 多工作区 daemon 资源使用需要上限
**#8051** — `qwen serve` 的 daemon 目前只限制工作区和会话数量，未限制请求体、WebSocket 组装等占用的字节数。高负载下可能内存失控，需要更细粒度的资源预算。
🔗 https://github.com/QwenLM/qwen-code/issues/8051

### 7. [P3] 进程名仍为 node.exe，外部工具难以稳定识别
**#8376** — 社区呼吁将 Windows 上的进程名改为 `qwen-code.exe`（macOS/Linux 为 `qwen-code`），否则依赖进程名的外部工具/任务管理器只能靠启发式猜测。
🔗 https://github.com/QwenLM/qwen-code/issues/8376

### 8. [P3] 桌面客户端无法用 @ 引用到项目中的文件
**#8123** — 项目目录中存在 `KuaiShouOrderService.java`，但桌面客户端用 @ 引用搜索不到。用户使用的是 v0.5.5 桌面版，疑似路径索引问题。
🔗 https://github.com/QwenLM/qwen-code/issues/8123

### 9. [P3] 提案：直接外部上下文提供者 Profile
**#7585** — 提议为 Qwen Code 增加“直接外部上下文提供者”配置，让 CLI 进程从管理员绑定的外部内存中获取仓库共享上下文，实现私有 monorepo 的双 Profile 管理。讨论已持续 11 天，收到 11 条评论。
🔗 https://github.com/QwenLM/qwen-code/issues/7585

### 10. [P3] ConEmu/Cmder 下整个输出闪烁
**#8385** — Windows 下 Qwen CLI 在 ConEmu/Cmder 中全屏闪烁，只有设置 `CI=true` 才能规避。与终端缓冲/ANSI 处理相关，尚未有官方修复。
🔗 https://github.com/QwenLM/qwen-code/issues/8385

## 重要 PR 进展

以下 10 个 PR 反映了当前开发主力方向，按影响面筛选：

### 1. fix(hooks): 关闭 Hook 执行中的四个信任边界漏洞
**#8396** (@wenshao) — 修复包括：HTTP hook 不再跟随重定向（此前 URL 白名单可被绕过）、以及另三个仓库配置与执行/出网之间的边界漏洞。属于安全加固的关键合并。
🔗 https://github.com/QwenLM/qwen-code/pull/8396

### 2. fix(core): 识别 OpenAI SDK APIUserAbortError 为 abort
**#8399** (@harjothkhara) — 直接修补 #8398：让 `isAbortError` 识别 `APIUserAbortError`（该错误不设置 `.name`，导致漏判）。OpenAI 兼容路径的取消体验将恢复正常。
🔗 https://github.com/QwenLM/qwen-code/pull/8399

### 3. feat(review): Maven 多模块构建验证
**#8394** (@wenshao) — 为 `/review` 增加确定性 Maven 多模块验证：能识别 root reactor、将变更文件映射到最深默认模块，并优先进行针对性验证，减少误报。
🔗 https://github.com/QwenLM/qwen-code/pull/8394

### 4. feat(review): capture-tui — 渲染类问题从“描述”变为“像素证据”
**#8388** (@wenshao) — 在私有 tmux server 中驱动被测代码，截取真实终端渲染结果作为 finding 的证据。对“面板在 80 列被截断”这类 UI 问题的验证将更可信。
🔗 https://github.com/QwenLM/qwen-code/pull/8388

### 5. feat(voice): 支持受信任的私有 ASR base URL
**#8350** (@rockybot2026) — 新增 `security.allowedInsecureVoiceBaseUrls`（默认全空）精确白名单，允许受管部署内使用 HTTP/私有网络的语音转写网关，同时保持默认“拒绝一切”的安全语义。
🔗 https://github.com/QwenLM/qwen-code/pull/8350

### 6. feat(workflows): 协作式暂停与恢复
**#8320** (@qqqys) — 为 Dynamic Workflows 增加整轮协作式暂停：暂停后停止派发新 agent、让在途工作收尾、在 gate 处保留结果；恢复后再继续。取消请求不会导致已工作丢失。
🔗 https://github.com/QwenLM/qwen-code/pull/8320

### 7. feat: 从任意对话处 fork
**#8274** (@water-in-stone) — 此前分支只能基于最新会话状态，无法回退到早期 Assistant 回复。该 PR 将分支点精确绑定到可见消息，并处理 tool calls、取消、分页等边界情况。
🔗 https://github.com/QwenLM/qwen-code/pull/8274

### 8. feat(auth): 新增 Kimi 与小米 MiMo 提供商
**#8368** (@DragonnZhang) — 为 `/auth` 增加两个第三方提供商预设：Kimi（含 Coding Plan / 国内 API Key / 国际 API Key 三种接入方式）和 MiMo（按量付费 + 中国/新加坡等多区域）。
🔗 https://github.com/QwenLM/qwen-code/pull/8368

### 9. feat(cli): 渲染内联终端图像
**#8305** (@tlysanhuo) — 将 #8217 的终端图像能力从工作区文件预览扩展到模型/工具的 `inlineData`，支持在交互式 CLI 中按顺序渲染文本与图片，为多模态交互铺路。
🔗 https://github.com/QwenLM/qwen-code/pull/8305

### 10. feat(desktop): 将 Electron 用户桥接到 Tauri 更新
**#8392** (@yiliang114) — 提供一次性的 macOS 更新桥：Tauri 版本沿用旧名称和标识符，新用户可平滑升级，旧 Electron 分发渠道过渡到 Tauri。
🔗 https://github.com/QwenLM/qwen-code/pull/8392

## 功能需求趋势

从昨日更新的全部 Issue 与 PR 中可以提炼出以下五个最受关注的功能方向：

1. **会话可靠性**：多起会话被删、transcript 分叉、历史无法写入等问题表明，社区对“会话数据不丢、可恢复”的需求远超新功能。P1 级 Issue 集中在此。

2. **安全与信任边界**：进程名可识别（#8376）、Hook 不跟随重定向（#8396）、私有 ASR 白名单（#8350）、安全云部署集成（#8291）——安全相关提案明显增多，且多数带“默认拒绝”的保守设计。

3. **多渠道/多模型接入**：邮箱（IMAP/SMTP）、QQ 频道、Kimi、小米 MiMo 等第三方 Provider 的接入请求持续出现，用户希望 Qwen Code 成为统一入口。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*