# AI CLI 工具社区动态日报 2026-08-03

> 生成时间: 2026-08-02 22:35 UTC | 覆盖工具: 7 个

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

**数据截止**: 2026-08-03 | **数据源**: [anthropics/skills](https://github.com/anthropics/skills)

---

## 1. 热门 Skills 排行

> 按 PR 评论数排序。当前榜单呈现明显分化：**skill-creator 工具链修复**与**新 Skill 提交**各占半壁江山，且所有高热度 PR 均处于 Open 状态，官方合并节奏偏慢。

### ① skill-creator 评估脚本全面修复
- **PR**: [#1298](https://github.com/anthropics/skills/pull/1298)（@MartinCajiao，2026-06-10）
- **功能**: 修复 `run_eval.py` 对所有 skill 描述恒报 `recall=0%` 的致命缺陷——将评估 artifact 安装为真实 skill，并修复 Windows 流读取、触发检测和并行 worker 问题
- **讨论热点**: 该问题已累计 10+ 独立复现（见 Issue #556），意味着描述优化循环一直在"对着噪声调参"；PR 同时波及 `run_loop.py` 和 `improve_description.py`，是当前生态最核心的阻塞项
- **状态**: Open

### ② document-typography（文档排版质量）
- **PR**: [#514](https://github.com/anthropics/skills/pull/514)（@PGTBoos，2026-03-04）
- **功能**: 针对 AI 生成文档的排版质检：孤行换行（1-6 个词溢出到下一行）、孤立标题滞留页底、编号错位
- **讨论热点**: "用户很少主动要求好的排版，但每个 Claude 生成的文档都会受影响"——直击生成文档的隐性体验痛点
- **状态**: Open

### ③ odt（OpenDocument 支持）
- **PR**: [#486](https://github.com/anthropics/skills/pull/486)（@GitHubNewbie0，2026-03-01）
- **功能**: OpenDocument 格式（.odt/.ods）创建、模板填充、ODT→HTML 解析转换
- **讨论热点**: 填补开源/ISO 标准办公格式的空白，与既有 docx/pdf skill 形成互补，是企业文档工作流的关键拼图
- **状态**: Open

### ④ frontend-design 改进
- **PR**: [#210](https://github.com/anthropics/skills/pull/210)（@justinwetch，2026-01-05）
- **功能**: 重写 frontend-design skill，确保每条指令可在单次对话内被执行，指导具体到足以约束行为
- **讨论热点**: 核心

---



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报

**日期：2026-08-03**


## 今日速览

过去 24 小时 Codex 仓库无新版本发布，社区热度集中在桌面应用（Desktop）与 CLI 的稳定性反馈上。Linux 桌面版支持（#11023）与提问自动解析可配置化（#28969）持续占据讨论榜前列。PR 侧聚焦内部基础设施修复，包括 MCP 目录项上限提升至 2048、SQLite 线程元数据保护，以及 Agent 插件的可移植安装支持。


## 版本发布

过去 24 小时无新版本发布。


## 社区热点 Issues

### 1. Codex 桌面应用 Linux 版支持 [#11023](https://github.com/openai/codex/issues/11023)
- **作者** @Suhaibinator | **评论** 197 | **👍** 905
- 社区中呼声最高的功能请求。用户因 macOS 端存在的电源消耗问题（#10432）转向 Linux 桌面环境，期望官方提供 Linux 版桌面应用。该 issue 获得近千点赞，反映出对跨平台桌面客户端的强烈需求。

### 2. 新增设置：禁用 60 秒问题自动解析 [#28969](https://github.com/openai/codex/issues/28969)
- **作者** @antoyo | **评论** 66 | **👍** 187
- 在 codex-cli 0.141.0 中，Codex 会在 60 秒后自动解析（resolve）用户的提问，用户希望增加开关以禁用此行为。社区反响积极，认为该超时机制在实际使用中过于激进。

### 3. Codex 桌面版会话超出最近 50 条后静默消失 [#21128](https://github.com/openai/codex/issues/21128)
- **作者** @thughy | **评论** 31 | **👍** 20
- 当项目会话超出全局最近 50 条窗口后，会从桌面应用 UI 中消失，影响项目记忆的连续性，用户认为这不是边缘 case，而是工作流设计缺陷。

### 4. Computer Use Chrome 扩展无法从商店下载：有无离线安装包？ [#21700](https://github.com/openai/codex/issues/21700)
- **作者** @DevDengChao | **评论** 27 | **👍** 24
- 桌面版 Computer Use 依赖的 Chrome 扩展在 Chrome Web Store 页面显示 error，用户请求离线安装包。该问题阻塞了 Windows 端浏览器自动化能力的落地。

### 5. OneDrive 降级导致 Work/Codex 流式请求反复断开 [#35420](https://github.com/openai/codex/issues/35420)
- **作者** @hiroki-tamba-research | **评论** 26 | **👍** 0
- Windows 下当工作区由 OneDrive 支持且 OneDrive 处于降级状态时，ChatGPT Work/Codex 的流式请求反复出现 stream disconnected 错误。已产出两个 request ID 供排查。

### 6. elevated_windows_sandbox 导致所有命令失败（CreateProcessAsUserW failed: 5） [#10090](https://github.com/openai/codex/issues/10090)
- **作者** @i4TsU | **评论** 22 | **👍** 7
- 启用 elevated Windows 沙箱后所有 agent 命令均无输出，日志揭示 CreateProcessAsUserW 权限错误（错误码 5），导致 Business 订阅用户无法在 Windows 上使用沙箱功能。

### 7. Windows 10 22H2 下 Computer Use 截图失败 [#25178](https://github.com/openai/codex/issues/25178)
- **作者** @Define1165250535 | **评论** 21 | **👍** 12
- 在 Windows 10 22H2 上，Computer Use 已经可以列出窗口、激活窗口和读取辅助功能文本，但任何调用 get_window_state 请求截图的操作都会因 `SetIsBorderRequired failed: 0x80004002`（接口不支持）而失败。

### 8. 子代理导致 Codex 磁盘用量爆炸 [#34061](https://github.com/openai/codex/issues/34061)
- **作者** @jezell | **评论** 17 | **👍** 1
- 在 codex-cli 0.144.6 + gpt-5.6 环境下，多子代理工作负载产生异常磁盘占用。用户反馈磁盘空间被大量消耗，与子代理会话历史或临时数据的保留策略有关。

### 9. Pro20x 订阅使用量表现异常 [#29968](https://github.com/openai/codex/issues/29968)
- **作者** @NAXXcode | **评论** 16 | **👍** 15
- Pro20x 订阅用户反映其额度消耗模式与 Plus 计划几乎一致，疑似订阅等级识别或计费逻辑存在错误。

### 10. Codex 桌面版在等待/状态轮询期间反复进入模型并消耗大量额度 [#35259](https://github.com/openai/codex/issues/35259)
- **作者** @dimasyankauskas | **评论** 10 | **👍** 2
- 在 Ultra 与多智能体工作流中，桌面版反复调用模型仅用于轮询 agent 状态；在一次重置后的 49% 额度窗口中，仅轮询类 turn 就占了原始 token 消耗的 19.8%。

**其余值得关注的 issue：**
- [#34021](https://github.com/openai/codex/issues/34021) 新消息队列请求被忽略（8 条评论）
- [#27880](https://github.com/openai/codex/issues/27880) macOS 桌面版频繁崩溃：CrBrowserMain EXC_BREAKPOINT、Renderer SIGABRT（6 条评论）
- [#32309](https://github.com/openai/codex/issues/32309) 大上下文恢复 + 高频代码模式轮询放大 token 消耗（6 条评论）
- [#34863](https://github.com/openai/codex/issues/34863) app-server 占用 27 GB 内存/36 GB swap，单 rollout JSONL 膨胀至 10.2 GB（5 条评论）


## 重要 PR 进展

### 1. [已关闭] 暴露登录完成通知中的引导提示 [#36635](https://github.com/openai/codex/pull/36635)
- **作者** @copyberry[bot] | 创建 2026-08-02 | 已合并
- 允许在 OAuth 状态中接受白名单 `.onboarding_entrypoint=life_sciences` 后缀，同时继续拒绝未知后缀；登录服务器返回解析后的回调元数据。

### 2. [已关闭] 目标变更期间保留 SQLite 线程元数据 [#36632](https://github.com/openai/codex/pull/36632)
- **作者** @copyberry[bot] | 创建 2026-08-02 | 已合并
- 修复设置或清除线程目标时，重新索引 rollout 可能覆盖 SQLite 侧线程元数据（含预览）的问题。当 SQLite 已引用同一事件时跳过 rollout 重新对账。

### 3. [代码评审中] 限制 executor 控制的 HTTP 响应缓冲 [#31781](https://github.com/openai/codex/pull/31781)
- **作者** @jif-oai | 创建 2026-07-09
- 此前流式 HTTP 响应的缓冲仅按帧数限制（256 帧），但单帧可达 JSON-RPC 消息上限。现在对不可信 exec-server 的响应数据量增加字节级上限，缓解内存压力。

### 4. [待合并] 自动更新 models.json [#31817](https://github.com/openai/codex/pull/31817)
- **作者** @github-actions[bot] | 创建 2026-07-09
- 由 CI 自动提交的模型列表更新，通常伴随新模型加入或模型参数变更。

### 5. [已关闭] 安装流程支持便携式 Agent 插件 [#36544](https://github.com/openai/codex/pull/36544)
- **作者** @copyberry[bot] | 创建 2026-08-02 | 已合并
- Agent 插件使用 schema 声明的 `plugin.json` 作为根，且可能包含不符合目录安全版本格式的点分名称或版本号。此次修复使打包和安装路径不再依赖旧版 manifest 布局，支持更灵活的插件命名与安装。

### 6. [已关闭] 将 MCP 目录项上限提升至 2048 [#36534](https://github.com/openai/codex/pull/36534)
- **作者** @copyberry[bot] | 创建 2026-08-01 | 已合并
- 分页 MCP 工具/资源/资源模板发现请求的收集上限从 1024 提升至 2048，缓解大型 MCP 生态下工具被截断的问题。


## 功能需求趋势

从近期 Issue 与 PR 中可以提炼出以下社区功能诉求方向：

- **跨平台桌面客户端扩展**：Linux 桌面版支持（#11023）、SSH 远程工作区一等公民支持（#21509）获大量关注，说明开发者希望桌面应用摆脱单一操作系统绑定并支持远程开发场景。
- **IDE 工作区隔离**：VS Code 扩展会话按项目/工作区隔离的需求再次出现（#33779），与此前关闭的 #3550 诉求一致且热度不减。
- **细粒度策略配置**：用户期望更多开关控制 CLI 行为，如禁用 60 秒自动解析（#28969）、`approvals_reviewer` 不应静默覆盖 `--sandbox` 显式级别（#36570）。
- **额度与用量透明度**：订阅额度异常（#29968、#29895）、轮询消耗占比过高（#35259）等问题本质上都指向用户对额度消耗机制透明度的强烈需求。
- **大型 MCP 生态支持**：MCP 目录项上限从 1024 扩展到 2048（#36534），反映真实项目中 MCP server 规模已超出原有假设。


## 开发者关注点

- **稳定性的老生常谈**：多个 issue 指向崩溃、内存膨胀与沙箱兼容性问题。尤其是 Windows 端，`elevated_windows_sandbox` 权限失败（#10090）、Chrome 扩展缺失（#21700）、截图接口不支持（#25178）构成了“Windows 上桌面/沙箱/浏览器自动化不可用”的组合痛点。
- **远程 workspace 的传输效率**：OneDrive 降级导致流式断连（#35420）、远程 SSH 线程 hydration 阻塞队列（#36189）和多 GB rollout 会话唤醒时突发 ~71 Mbps 上行（#33796），都指向远端与本地数据同步机制存在设计短板。
- **成本控制与配额消耗**：开发者对“非生产性”模型调用非常敏感——高频率轮询、意外多轮重入、等待/status 检查消耗高额 token，已影响用户对代理的信任。反馈 ID 被大量附上，说明用户希望官方据此调优计费与轮询策略。
- **本地数据量膨胀**：超过 10 GB 的 JSONL rollout、27 GB app-server 内存占用（#34863）、子代理磁盘爆炸（#34061）、侧边栏因元数据包含完整记录而卡死（#32371），反映出数据序列化与存储策略需要重新设计。

---

*本日报基于 GitHub 公开数据自动整理，部分 issue 状态与内容以仓库实际为准。*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>



</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-08-03）

## 1. 今日速览

昨日发布 v0.21.3-nightly 版本，重点补全 TUI 键盘快捷键文档并推进核心历史分页修复。社区讨论聚焦于 **daemon 多工作区资源管控**、**OpenAI SDK 取消请求误判** 以及 **进程识别问题**，同时大量安全与稳定性修复 PR 涌入（hook 信任边界、ASR 地址守卫等），整体呈现「安全加固 + 基础设施

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*