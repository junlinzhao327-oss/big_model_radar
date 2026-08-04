# AI CLI 工具社区动态日报 2026-08-05

> 生成时间: 2026-08-04 23:28 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告

**日期：2026-08-05**


## 1. 生态全景

AI CLI 工具已从单纯聊天式编码助手演变为具备 **沙箱隔离、插件体系、远程协作、多模型网关** 能力的完整开发基础设施。各工具迭代节奏明显加快（Claude Code、OpenCode、Copilot CLI 均在 24 小时内发布新版本），但 **稳定性问题（Windows 平台、Bash 工具、模型路由故障）仍是社区最大痛点**。与此同时，**会话持久化（记忆/分叉/云同步）和 ACP 协议互操作** 正在成为各工具争夺的下一个核心战场，开发者不再满足于单次会话的代码生成，而是期望 CLI 成为可长期承载复杂工作流的"AI 开发底座"。整体呈现"功能快速膨胀、基础体验仍需夯实"的典型早期生态特征。


## 2. 各工具活跃度对比

| 工具 | 今日 Release | 热点 Issues | 重要 PR | 社区活跃度特征 |
|------|:---:|:---:|:---:|------|
| **Claude Code** | 2（v2.1.222 / v2.1.221） | 10 | 3 | Issues 更新 50 条，老 issue 持续发酵（117 评论） |
| **GitHub Copilot CLI** | 1（v1.0.79-1） | 10 | 2 | 功能迭代稳定，破坏性变更引发关注 |
| **OpenCode** | 2（v1.18.13 / v1.18.12） | 10 | 10 | PR 最活跃，DeepSeek 故障集中爆发 |
| **Qwen Code** | 2（v0.21.5 + nightly） | 10 | 截断，≥1 | 正式版+夜间版双轨迭代 |
| **Kimi Code CLI** | 0 | 4（全部列出） | 3 | 体量最小，但 ACP/记忆方向讨论深入 |
| **OpenAI Codex** | 无数据 | 无数据 | 无数据 | 本日报未披露 |
| **Gemini CLI** | 无数据 | 无数据 | 无数据 | 本日报未披露 |

> 说明：OpenAI Codex 与 Gemini CLI 在本次数据源中无动态记录，下表及分析以其余 5 个工具为主。


## 3. 共同关注的功能方向

### 3.1 会话状态管理（跨工具呼声最高）
| 工具 | 具体诉求 |
|------|---------|
| **Copilot CLI** | 会话分叉/并行分支（25 👍）、云同步跨设备、删除会话命令（13 👍） |
| **Kimi Code CLI** | Memory System 跨会话记忆（#1283，17 评论）、Remote Control 远程控制本地会话（24 👍） |
| **Claude Code** | 后台任务上下文丢失（#83971）、账号切换项目未重置（#83973） |

### 3.2 Windows / WSL2 平台兼容性
| 工具 | 具体问题 |
|------|---------|
| **Claude Code** | 桌面版无法重启（117 评论）、Bash 工具 "unexpected EOF"、VSCode 文本选择回归 |
| **Copilot CLI** | Ctrl+H 误识别（#4328）、原生 Windows 反复崩溃（#4026）、zellij 输入预填异常（#4267） |
| **Kimi Code CLI** | Windows 11 IME 泰文输入重复（#2584） |

### 3.3 ACP 协议生态与互操作性
| 工具 | 具体诉求 |
|------|---------|
| **Kimi Code CLI** | 模型列表不可发现、会话中无法切换模型（#2583）、权限模式切换（#2364）、子进程 AI_AGENT 标记（#2585） |
| **OpenCode** | SSE 事件不完整导致 Codex 客户端解析失败（#40171）、reasoning 字段支持（#35284）、ACP 货币尊重 provider 配置（#39425） |
| **Qwen Code** | JetBrains ACP 任务列表不渲染（#8544） |

### 3.4 安全与隔离边界
| 工具 | 具体关注点 |
|------|-----------|
| **Claude Code** | worktree 隔离漏洞修复、hook 绕过漏洞修复、git 配置污染（#72714） |
| **Copilot CLI** | 沙箱配置重命名致用户静默回退默认值、MCP 服务器被策略解析阻断（#4349） |
| **Qwen Code** | 确定性工具执行边界（#8102）、取消的文件工具仍修改文件系统（#8493）、Provider 警告清理器泄露密码（#8136） |

### 3.5 模型服务稳定性与成本透明度
| 工具 | 具体问题 |
|------|---------|
| **OpenCode** | DeepSeek V4 Flash 空响应/500 错误、模型版本偏差（V3.2 冒充 V4）、Go 套餐用量 API（126 👍） |
| **Claude Code** | 图片处理失败仍计费（#62466）、社区对"无产出却消耗额度"容忍度下降 |
| **Copilot CLI** | ACP 模式未暴露 Token 用量（#4174）、BYOK 流式 reasoning_content 触发重试（#4196） |

### 3.6 自定义主题 / UI 个性化
- **Copilot CLI**：自定义主题支持（23 👍）、OSC 11 背景色适配
- **Claude Code**：RTL 支持（90 👍，最高赞）


## 4. 差异化定位分析

| 维度 | Claude Code | Copilot CLI | OpenCode | Qwen Code | Kimi Code CLI |
|------|------------|-------------|----------|-----------|---------------|
| **功能侧重** | 企业级安全隔离（worktree/hooks）、IDE 深度集成（VSCode Focus view） | 企业治理（组织级 Agent、托管策略、计费实体）、沙箱权限模型 | 多 provider 网关、Go 托管服务、TUI/桌面双端 | 多模型提供商预设、桌面技术栈迁移（Electron→Tauri） | ACP 协议深度、记忆/远程控制愿景 |
| **目标用户** | 团队/企业开发者，重度 VSCode 用户 | 企业内 GitHub 生态用户，需要策略管控的团队 | 追求模型自由度的个人开发者、需要可编程 API 的自动化场景 | 偏好第三方模型（如 Kimi/MiMo）的多模型用户 | 移动端/多设备开发者、ACP 客户端生态的集成者 |
| **技术路线** | 专有闭源，桌面+CLI+插件生态 | 闭源，GitHub 深度绑定，插件自动更新 | 开源，自建 Go 云服务 + 本地 TUI 双路线 | 开源，桌面从 Electron 迁移至 Tauri 提升性能 | 开源，押注 ACP 作为通用协议底座 |
| **当前最热议题** | Windows 桌面稳定性 | 会话管理 + 自定义主题 | DeepSeek 服务可靠性 | 安全信任边界 + 闪屏问题 | 跨会话记忆 + ACP 能力补齐 |


## 5. 社区热度与成熟度

### 成熟度梯队
| 梯队 | 工具 | 判断依据 |
|------|------|---------|
| **成熟稳定型** | **Claude Code** | 版本号 v2.1.x，Issue 讨论深度高（117 评论问题持续 4 个月），功能覆盖安全/IDE/桌面/插件全栈，但 Windows 问题长期未解暴露大版本包袱 |
| | **Copilot CLI** | v1.0.79 已达高版本号，发布节奏稳定，企业功能布局完整（托管策略、计费、组织 Agent），社区讨论更偏向功能增强而非"能不能用" |
| **快速迭代型** | **OpenCode** | 单日 2 个版本 + 10 个 PR，修复速度最快，但 DeepSeek 故障与挂起问题同时爆发，属于"高速扩张伴随质量波动"阶段 |
| | **Qwen Code** | 正式版 + 夜间版双轨，安全边界类深度讨论（#8102 确定性执行边界）显示技术前瞻性强，但社区规模仍较小 |
| **早期探索型** | **Kimi Code CLI** | Issues/PR 数量最少，但聚焦 ACP 协议与长期记忆方向，处于"以少而精的深度议题塑造产品"阶段 |

### 关键观察
- **OpenCode 社区活跃度增速最快**：10 个 PR 覆盖剪贴板、reasoning、挂起、托盘等横跨 TUI/桌面/协议的方向，但其 DeepSeek 故障一日内多帖轰炸，暴露服务型架构的运维短板。
- **Copilot CLI 与 Claude Code 的社区讨论质量最高**：前者集中在企业治理与体验增强，后者集中在安全模型与平台稳定性，均体现出"产品已过可用性门槛、用户开始追求精细化"的特征。
- **Kimi Code CLI 与 Qwen Code 的差异化路线尚未被充分验证**：前者依赖 ACP 生态的成熟度，后者依赖多模型策略能否转化为足够用户基数。


## 6. 值得关注的趋势信号

### 信号一：Windows 平台成为 AI CLI 工具的分水岭
五个工具中有三个今日面临 Windows/WSL2 相关阻断型问题（Claude Code 桌面重启失败、Bash 全挂；Copilot 输入异常与崩溃；Kimi IME 重复）。**Windows 开发者是当前 AI CLI 渗透率最高的增量市场之一**，谁先彻底解决 Windows 稳定性，谁就能收割这一波用户迁移红利。

### 信号二：ACP 正从"边缘协议"走向"事实标准候选"
Kimi Code CLI 的模型发现缺口、OpenCode 的 SSE 事件兼容、Qwen Code 的 JetBrains 渲染问题，本质上都是 **客户端-服务端协议互操作** 的摩擦。当多个工具都围绕 ACP 修补兼容性时，可以判断：**AI CLI 工具正在从"独立终端应用"演变为"可被任意前端驱动的后端服务"**。对开发者的启示是——选择工具时不再是看 UI 好不好用，而是看它的协议层是否开放。

### 信号三：沙箱权限配置的"静默破坏"将引发信任危机
Copilot CLI 在 v1.0.79-1 中重命名 `allowDevToolCaches` 为 `allowDevToolAccess` 且**静默忽略旧键**，导致选择退出的用户悄悄回到默认开启状态。Claude Code 的同类型问题（worktree 配置污染主仓库）也受到重点关注。**安全相关的配置变更必须是显式、可迁移的**——这一原则正在被社区用脚投票验证。

### 信号四：用量透明度成为付费用户的底线诉求
OpenCode 的 Go 套餐用量 API（126 👍）、Copilot 的 ACP Token 用量暴露、Claude Code 的图片处理计费争议，共同指向一个趋势：**AI CLI 工具从"卖订阅"转向"卖信任"**。服务型产品必须提供精准的用量计量 API 和失败不扣费的保障机制，否则用户流失只是时间问题。

### 信号五：模型路由与版本治理是服务型 CLI 的新护城河
OpenCode 的 DeepSeek V4 Flash 事件（空响应 + 模型版本冒用 + 地域托管限制）是一个典型警示：**集成第三方模型的服务必须建立模型版本校验、健康检查、故障快速回退机制**。当用户付费用一个模型 ID，拿到的却是另一个版本的模型时，服务商的公信力受到的损害远大于一次故障。

### 信号六："会话可移植性"正在成为基础需求
从 Copilot 的云同步/会话分叉、Kimi 的 Remote Control（24 👍）到 Claude Code 的上下文丢失投诉，**用户想要的是"一个会话贯穿所有设备、所有时刻"**。这是 AI CLI 从"命令工具"升维为"AI 工作空间"的关键一战，预计未来数月内会有多个工具正式推出会话云同步能力。


**总结**：当前 AI CLI 生态正处于"功能军备竞赛"与"基础体验补课"并存的阶段。技术决策者选型时，应优先评估工具的 **平台兼容性（尤其 Windows）、协议开放性（ACP 支持度）、用量透明度和安全配置的严谨性**；开发者则应密切关注会话管理能力（分叉/同步/记忆）的落地进展——这将决定未来一年 AI 辅助开发的协作范式。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---

# Claude Code 社区动态日报（2026-08-05）

## 今日速览
昨日发布 v2.1.222 与 v2.1.221 两个版本，重点修复了 worktree 隔离安全漏洞、hook 绕过限制，并为 VSCode 带来全新的 Focus view 专注模式。社区方面，Windows 桌面版无法重启的长期问题（117 条评论）仍是最大热点，RTL 语言支持则以 90 个 👍 成为最受期待的功能需求。

## 版本发布
### v2.1.222
- 修复 worktree 隔离会话及其子代理可对主 checkout 执行破坏性 git 命令的问题；隔离机制现适用于所有会话类型的文件编辑与 Bash 操作。
- 修复 PreToolUse 自动允许 hooks 在后台代理任务中绕过工具限制的漏洞。

### v2.1.221
- [VSCode] 新增 **Focus view**：通过聊天菜单切换，可将工具活动隐藏为可展开的逐轮摘要，并附带实时运行工具指示器。快捷键 `Ctrl+Alt+F` 或命令面板 “Claude Code: Toggle Focus view” 触发。
- Linux 新增 `mode: "mask"`，用于沙箱凭证文件。

## 社区热点 Issues
过去 24 小时更新 50 条，以下为最值得关注的 10 条：

1. **[#42776] Claude Code Desktop 在 Windows 上因孤儿进程文件锁无法重启**  
   评论 117 · 👍 51 · 2026-04-02 创建至今仍未解决  
   社区影响最大：Windows 桌面版用户长期受困于重启失败，涉及文件锁与孤儿进程清理，急需官方修复。  
   https://github.com/anthropics/claude-code/issues/42776

2. **[#38005] RTL（从右到左）支持：希伯来语与阿拉伯语**  
   评论 41 · 👍 90  
   高赞功能请求：面向中东语言用户的协作与桌面端渲染需求，社区呼声强烈，但长期处于 open。  
   https://github.com/anthropics/claude-code/issues/38005

3. **[#62466] 反复出现 “Image couldn't be processed” API 错误并消耗使用额度**  
   评论 29 · 👍 20  
   图片处理失败却持续计费，用户反映影响高用量场景，属于成本与稳定性双重问题。  
   https://github.com/anthropics/claude-code/issues/62466

4. **[#61021] VSCode 终端中无法方便地选择文本复制粘贴**  
   评论 15 · 👍 11  
   近期变更引入的易用性回归，影响日常复制路径、代码块等操作，Windows/VSCode 用户反馈集中。  
   https://github.com/anthropics/claude-code/issues/61021

5. **[#83243] Windows 上 Bash 工具连简单命令都报 “unexpected EOF...line 86”**  
   创建于 v2.1.220，最新版仍受影响  
   Bash 工具完全不可用，属于阻断型缺陷，当前评论较少但影响面极大。  
   https://github.com/anthropics/claude-code/issues/83243

6. **[#83971] 后台运行交互会话时，新任务只继承最后一条 prompt，丢失全部上下文**  
   2026-08-04 新提交  
   后台任务无法延续对话状态，导致生成内容与上下文脱节，直接影响异步工作流。  
   https://github.com/anthropics/claude-code/issues/83971

7. **[#83973] 桌面应用切换账号后，已选本地项目/仓库未重置**  
   2026-08-04 新提交  
   账户隔离不彻底，可能在切换团队/账号后意外操作上一账号的项目，存在数据混淆风险。  
   https://github.com/anthropics/claude-code/issues/83973

8. **[#83643] 桌面远程会话插件同步至 `~/.claude/remote/plugins/` 时遗漏 hooks/**  
   插件 hooks 静默失效，技能与命令正常但 hooks 不触发，影响远程自动化与安全检查。  
   https://github.com/anthropics/claude-code/issues/83643

9. **[#83815] 桌面 SSH 连接仅支持密钥的主机时出现死胡同密码提示**  
   sshd 仅支持 publickey，但应用仍弹密码框且永远失败，阻塞远程开发流程。  
   https://github.com/anthropics/claude-code/issues/83815

10. **[#72714] `/worktree` 可能将 `core.hooksPath` 写入主仓库共享 `.git/config`，禁用全局 hooks**  
   配置污染问题：worktree 功能应隔离 git 配置，却影响主 checkout 的 hooks，值得关注。  
    https://github.com/anthropics/claude-code/issues/72714

## 重要 PR 进展
过去 24 小时仅更新 3 个 PR，全部列出：

- **[#83890] Create pylint.yml**  
  新增 GitHub Actions 工作流，疑似为仓库引入 pylint 静态检查（未合并）。  
  https://github.com/anthropics/claude-code/pull/83890

- **[#83374] docs(plugin-dev): 文档化 MessageDisplay 流式语义**  
  为内置 Hook 开发技能补充 `MessageDisplay` 事件的触发说明、事件指南和速查表，完善插件开发文档。  
  https://github.com/anthropics/claude-code/pull/83374

- **[#83738] Fix/83484 symlink path expansion**  
  修复 `claude install` 在某些 Linux 安装中创建指向 `%h` 字面量路径的坏符号链接问题，改为展开 home 目录。  
  https://github.com/anthropics/claude-code/pull/83738

## 功能需求趋势
从过去 24 小时更新的 Issues 中，社区关注的功能方向集中在：

- **桌面端与 Cowork 协作体验**：Windows 重启失败、本地项目选择/账号切换、Cowork 项目删除与归档恢复等。
- **国际化与无障碍**：RTL 语言支持（#38005）是最高赞需求，另有 `area:a11y` 标签。
- **模型行为与代理智能**：多个 issue 反映 agent 对显而易见的缺陷反应迟钝、忽略显式指令、产生虚假对话标记，期待更稳定、更严谨的模型行为。
- **终端与编辑器集成**：VSCode 文本选择、Windows 可配置 shell（#70276）、Focus view 等界面交互改进。
- **安全与隔离**：worktree git 配置污染、Bash 工具注入式注释、远程插件 hooks 同步等安全相关诉求增多。

## 开发者关注点
- **Windows 平台痛点突出**：桌面重启失败、Bash 工具全面故障、PowerShell 硬编码、文本选择回归，Windows 用户占比高且问题迟迟未解决。
- **资源与成本控制**：图片处理错误消耗使用额度、session limit 被非预期消耗，用户对“无产出却计费”的容忍度越来越低。
- **数据安全与会话完整性**：聊天历史丢失、背景任务上下文丢弃、账号切换不重置项目，均涉及数据安全与工作流连续性。
- **远程开发可靠性**：SSH 密钥主机密码死局、远程插件 hooks 不生效，影响多云/远程主机使用场景。
- **新版本回归警惕**：v2.1.220 引入的 Bash 问题引发关注，用户期望官方

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-05** | 数据来源：github.com/github/copilot-cli


## 今日速览

今日发布 **v1.0.79-1**，包含一项破坏性变更：沙箱配置项 `allowDevToolCaches` 重命名为 `allowDevToolAccess`（权限范围扩大至开发工具配置与注册表）。社区最热议题集中在 **自定义主题支持**（23 👍）、**会话分叉**（25 👍）与 **云同步会话**；功能方面，v1.0.78 引入了工具调用耗时显示与插件自动更新机制。另有多个 Windows/WSL2 输入异常、MCP 兼容性及企业计费相关问题值得关注。


## 版本发布

### v1.0.79-1（2026-08-05）

**功能改进**

- ⚠️ **破坏性变更**：沙箱设置 `allowDevToolCaches` 重命名为 `allowDevToolAccess`——现在该设置授予的是开发工具配置与注册表的访问权，而不仅限于缓存。旧键将不再读取且会被静默忽略；现有配置若为 `false`（选择退出），更新后将回退为默认值（启用）。请手动重命名设置项。
- 发布链接：[v1.0.79-1](https://github.com/github/copilot-cli/releases)

### v1.0.78（2026-08-03）

**功能改进**

- **工具耗时显示**：时间线标题现在会展示每个工具调用的耗时，右对齐并实时更新（仅对耗时 ≥5 秒的调用生效）。默认开启，可通过 `/settings showToolDurations` 关闭。
- **插件自动更新**：第一方插件在会话启动时自动更新至最新版本。
- 发布链接：[v1.0.78](https://github.com/github/copilot-cli/releases)


## 社区热点 Issues（Top 10）

### 🔥 1. 自定义主题支持
[#1504](https://github.com/github/copilot-cli/issues/1504) · [OPEN] · 创建于 2026-02-17 · 最后更新 2026-08-04

- 作者：@logar16 ｜ 评论：8 ｜ 👍：23
- 请求在现有基础主题之上支持用户自定义主题（如 JSON 文件），并允许主题分享。`/theme` 命令中可提供自定义选项。社区关注度高，属当前最热门的主题类需求之一。

### 🔥 2. 会话分叉 — 并行分支共享上下文
[#1697](https://github.com/github/copilot-cli/issues/1697) · [OPEN] · 创建于 2026-02-26 · 最后更新 2026-08-04

- 作者：@Bujo0 ｜ 评论：3 ｜ 👍：25
- 面对多步骤任务的分叉点，用户希望将当前会话分支为多个并行会话且共享已有上下文，避免在任务间切换时丢失状态。**今日高赞功能需求之一**。

### 3. 组织级 Agent 不显示
[#1285](https://github.com/github/copilot-cli/issues/1285) · [OPEN] · 创建于 2026-02-04 · 最后更新 2026-08-04

- 作者：@SAhmeti ｜ 评论：7 ｜ 👍：9
- 在 `{org}/.github-private` 仓库按正确模板创建的 Agents 未出现在 CLI / VS Code 工具中。企业用户配置 Agent 时遇到困难，涉及 agents 与 enterprise 两个核心领域。

### 4. Web Search 工具报 MCP 服务器错误
[#2692](https://github.com/github/copilot-cli/issues/2692) · [CLOSED] · 创建于 2026-04-14 · 最后更新 2026-08-04

- 作者：@hellopahe ｜ 评论：6 ｜ 👍：2
- 执行 Web Search 工具时报错：`MCP server 'github-mcp-server': Error: Streamable HTTP error: Error POSTing to endpoint...`。已关闭，但可关注后续与之关联的 MCP 兼容性问题（见 #4370）。

### 5. WSL2 下 Ctrl+H 被误识别为 Ctrl+Backspace
[#4328](https://github.com/github/copilot-cli/issues/4328) · [OPEN] · 创建于 2026-08-01 · 最后更新 2026-08-04

- 作者：@dimbleby ｜ 评论：5 ｜ 👍：0
- `/help` 文档标注 `ctrl+h` 为"删除前一字符"，但在 WSL2 环境下实际表现为"删除前一个整词"。根因指向 Windows Terminal 泄漏的 `WT_SESSION` 环境变量。影响 WSL2 用户的日常输入体验。

### 6. Copilot 计费实体未选中，无法保存记忆
[#4005](https://github.com/github/copilot-cli/issues/4005) · [OPEN] · 创建于 2026-07-02 · 最后更新 2026-08-04

- 作者：@CoolGoose ｜ 评论：4 ｜ 👍：3
- 企业环境中其他功能正常，但保存 memories 时报错 "Copilot billing entity isn't selected"，此前可正常保存。影响企业用户对记忆/上下文功能的依赖。

### 7. 内置 view 工具对存在的文件误报 "Path does not exist"
[#4202](https://github.com/github/copilot-cli/issues/4202) · [OPEN] · 创建于 2026-07-21 · 最后更新 2026-08-04

- 作者：@matanSchaumberg ｜ 评论：4 ｜ 👍：1
- **1.0.72 引入的功能回归**：1.0.73 中内置 `view` 工具对已存在文本文件报 "Path does not exist"，而 1.0.71 正常。作者提供了隔离的复现路径，可追踪至工具调用层。

### 8. 云端同步会话，跨设备连续工作
[#1947](https://github.com/github/copilot-cli/issues/1947) · [CLOSED] · 创建于 2026-03-10 · 最后更新 2026-08-04

- 作者：@robgrame ｜ 评论：4 ｜ 👍：6
- 请求将本地 `~/.copilot/` 中的会话同步上云，解决开发者跨设备切换时无法延续工作上下文的问题。虽已关闭，但反映出社区对"会话可移植性"的强烈期望。

### 9. BYOK 供应商流式响应中 `reasoning_content` 导致 API 报错
[#4196](https://github.com/github/copilot-cli/issues/4196) · [OPEN] · 创建于 2026-07-21 · 最后更新 2026-08-04

- 作者：@aosama ｜ 评论：2 ｜ 👍：0
- 使用 BYOK 供应商时，若流式 completions 增量中含 `reasoning_content` 字段，CLI 会误判为瞬时 API 错误并重试 5 次后失败。影响自定义模型接入的稳定性。

### 10. ACP 服务器未暴露 Token / 上下文使用量
[#4174](https://github.com/github/copilot-cli/issues/4174) · [CLOSED] · 创建于 2026-07-18 · 最后更新 2026-08-04

- 作者：@maxplangg ｜ 评论：2 ｜ 👍：2
- `copilot --acp --stdio / --port` 模式未在任何协议消息中暴露 token 用量、上下文消耗或成本信息，用户无法观测 ACP 模式下的资源消耗。已关闭，但在 BYOK/自托管场景下仍是重要信号。


## 重要 PR 进展

过去 24 小时内 PR 数量较少（2 条），均详细披露如下：

### 🔴 #4366 [OPEN] 安全修复：copilot-cli 基础安全发现处理
- 作者：@vault-chatops[bot] ｜ 更新：2026-08-04 ｜ [查看 PR](https://github.com/github/copilot-cli/pull/4366)
- 由 Vault ChatOps 自动提交的 **安全修复 PR**，针对 `copilot-cli` 应用在 `ci, production` 环境中的 Fundamentals 安全发现进行修复。需要人工审查并替换所有 `<UPDATE_ME>` 占位值后合并，属于**需要尽快处理的安全项**。

### #4355 [OPEN] Merge（无描述）
- 作者：@XavierMP14 ｜ 更新：2026-08-04 ｜ [查看 PR](https://github.com/github/copilot-cli/pull/4355)
- PR 内容暂未提供描述，需要进一步观察其变更内容。


## 功能需求趋势

从近 24 小时活跃的 Issues 中可提炼出以下社区高度关注的功能方向：

### 1. 🎨 主题与个性化
- **自定义主题支持**（[#1504](https://github.com/github/copilot-cli/issues/1504)，23 👍）——允许 JSON 自定义主题并支持分享。
- **OSC 11 背景色适配**（[#3898](https://github.com/github/copilot-cli/issues/3898)）——自定义背景色下前景色对比度问题。

### 2. 🔀 会话管理增强（核心诉求）
- **会话分叉 / 并行分支**（[#1697](https://github.com/github/copilot-cli/issues/1697)，25 👍）——在任务分叉点分支会话并共享上下文。
- **云同步会话**（[#1947](https://github.com/github/copilot-cli/issues/1947)，6 👍）——跨设备连续工作。
- **删除会话命令**（[#2019](https://github.com/github/copilot-cli/issues/2019)，13 👍）——从 `/resume` 历史中删除指定会话。

### 3. 🔌 插件与 MCP 生态
- **插件自动更新**（[#1709](https://github.com/github/copilot-cli/issues/1709)，29 👍）——v1.0.78 已支持第一方插件自动更新，社区仍在关注第三方插件。
- **MCP 兼容性**（[#2692](https://github.com/github/copilot-cli/issues/2692)、[#4370](https://github.com/github/copilot-cli/issues/4370)）——针对 FastMCP 等实现 `server/discover` 方法缺失的处理。

### 4. 🧠 模型与上下文
- **BYOK / 自定义模型端点**（[#4139](https://github.com/github/copilot-cli/issues/4139)，6 👍）——支持接入 Azure OpenAI、Google Cloud AI 等第三方模型。
- **持久化 Token 用量指示器**（[#2532](https://github.com/github/copilot-cli/issues/2532)）——常驻上下文栏展示 Token 消耗。

### 5. 🛡️ 沙箱与权限控制
- **选择性启用工具**（[#4298](https://github.com/github/copilot-cli/issues/4298)，2 👍）——在 settings.json 中白名单化内置工具。
- **OSC 9;4 进度条禁用开关**（[#4352](https://github.com/github/copilot-cli/issues/4352)）——对 kitty 等终端渲染干扰的规避需求。


## 开发者关注点

### ⚠️ 高频痛点

1. **Windows / WSL2 终端输入异常**（多起并发）
   - #4328：Ctrl+H 在 WSL2 下被误判为 Ctrl+Backspace（WT_SESSION 泄漏）
   - #4267：原生 Windows zellij 启动时，输入框预填 DA1 设备属性回复转义序列
   - #4334：会话切换导致 stashed（Ctrl+S）草稿丢失
   - #4026：Windows 原生运行时从 2026-05 起反复崩溃，横跨 4+ 版本

2. **企业环境配置"水土不服"**
   - #1285：组织级 Agents 不显示
   - #4005：计费实体未选中导致记忆功能不可用
   - #4349：托管策略枚举值 `"enable"` 与 CLI 校验器的 `"disable"` 字面量不匹配，**导致所有本地/自定义 MCP 服务器被阻断**

3. **工具回归与兼容性**
   - #4202：v1.0.72 起 `view` 工具对已存在文件误报路径不存在
   - #4361：插件斜杠命令失效，客户端改为发送注定失败的 `session.commands.invoke` RPC
   - #4370：新版 1.0.79-1 对 FastMCP `server/discover` 返回 `-32602` 误判为初始化失败

4. **沙箱/安全设置变更阵痛**
   - v1.0.79-1 将 `allowDevToolCaches` 重命名为 `allowDevToolAccess` 且**静默忽略旧键**，原先选择退出的用户将静默回退到默认开启，存在安全隐患。

### 📌 整体观察

社区当前对 **会话管理（分叉/同步/删除）** 和 **主题个性化** 的功能呼声最高；稳定性方面，**Windows 环境回归** 和 **MCP 生态兼容性** 是过去 24 小时最主要的吐槽来源。建议 Windows + WSL2 用户关注 #4328 与 #4267 的进展；企业用户注意 #4349 可能阻塞 MCP 服务器的策略解析问题。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-08-05）

## 今日速览

过去 24 小时内无新版本发布，但社区动态聚焦于 **ACP 协议生态完善**（模型发现、权限切换）与**跨会话长期能力**（记忆系统、远程控制）两大方向。此外，Windows 平台 IME 输入重复问题的新反馈值得关注。老 Issue 于 8 月 4 日再次更新，显示出社区对 Memory System 与 Remote Control 的持续高热度。

## 版本发布

过去 24 小时无新 Release。

## 社区热点 Issues

以下为过去 24 小时内更新的全部 4 条 Issue（含创建后更新的老 Issue）：

1. **#1283 [Feature Request] Memory System – Persistent context across sessions**  
   - 作者: @CatKang | 创建: 2026-02-27 | 更新: 2026-08-04 | 评论: 17 | 👍: 0  
   - 链接: https://github.com/MoonshotAI/kimi-cli/issues/1283  
   - **重要性**: 该功能请求要实现跨会话的记忆系统（自动记忆项目上下文、AI 笔记 + 用户手动指令），是提升 CLI 长期使用效率的核心需求。  
   - **社区反应**: 17 条评论表明讨论非常活跃，虽创建较早但 8 月 4 日仍在更新，说明用户对持久化上下文的需求长期未得到满足。

2. **#1282 [Feature Request] Remote Control – Continue local sessions from any device**  
   - 作者: @CatKang | 创建: 2026-02-27 | 更新: 2026-08-04 | 评论: 12 | 👍: 24  
   - 链接: https://github.com/MoonshotAI/kimi-cli/issues/1282  
   - **重要性**: 允许用户从手机、平板或浏览器控制本地 CLI 会话，解决“离开办公桌但保留完整本地环境”的连续工作流需求。  
   - **社区反应**: 24 个 👍 是当前 Issue 中支持度最高的一项，说明远程/移动场景在开发者群体中有广泛期待。

3. **#2584 [Bug] Thai（及 IME 类）字符在 Windows 提示输入时重复**  
   - 作者: @mgprona | 创建: 2026-08-04 | 更新: 2026-08-04 | 评论: 0 | 👍: 0  
   - 链接: https://github.com/MoonshotAI/kimi-cli/issues/2584  
   - **重要性**: 在 Windows 11 上使用泰语等 IME 输入法时，提示符中字符会重复，影响非英语用户的正常输入，属于平台兼容性缺陷。  
   - **社区反应**: 刚提交暂无评论，但问题明确、复现步骤清晰，需要维护者及时确认。

4. **#2583 [Feature Request] ACP：广告可用模型并支持会话中途切换模型**  
   - 作者: @tizerluo | 创建: 2026-08-04 | 更新: 2026-08-04 | 评论: 0 | 👍: 0  
   - 链接: https://github.com/MoonshotAI/kimi-cli/issues/2583  
   - **重要性**: 当通过 ACP 客户端（如 Happy Coder 移动应用、Zed）驱动 `kimi acp` 时，客户端无法发现可用模型列表，也无法在会话中切换模型（如 `session/new` 不返回模型列表且无 `current_model_update` 事件）。这是 ACP 集成的重要缺口。  
   - **社区反应**: 刚创建暂无评论，但指出了具体的协议交互缺陷，对移动端/编辑器集成开发者至关重要。

## 重要 PR 进展

以下为过去 24 小时内更新的全部 3 条 PR：

1. **#2200 [fix] shell：为长命令自适应超时**  
   - 作者: @he-yufeng | 创建: 2026-05-08 | 更新: 2026-08-04  
   - 链接: https://github.com/MoonshotAI/kimi-cli/pull/2200  
   - **功能/修复内容**: 自动延长 shell 超时时间，覆盖 `git submodule` 清理、`git clone/fetch`、软件包安装和构建等常见慢命令；普通命令仍保持 60 秒默认值；若调用者已提供更大的显式超时则保留。  
   - **意义**: 解决长时间运行命令被误杀导致任务中断的问题，提升 CLI 在复杂构建场景下的稳定性。

2. **#2585 [feat] CLI：为子进程设置 AI_AGENT 环境变量**  
   - 作者: @complynx | 创建: 2026-08-04 | 更新: 2026-08-04  
   - 链接: https://github.com/MoonshotAI/kimi-cli/pull/2585  
   - **功能/修复内容**: 在 pip/uv 和独立二进制入口启动的子进程中暴露 `AI_AGENT=kimi`；同时保留包装器或编排器显式设置的非空值。覆盖缺失、空白和显式标记三种行为。  
   - **意义**: 为生态工具提供一个统一标记，使下游流程能识别当前由 Kimi CLI 驱动，提升自动化集成能力。

3. **#2364 [feat] ACP：支持权限模式切换**  
   - 作者: @huntharo | 创建: 2026-05-24 | 更新: 2026-08-04  
   - 链接: https://github.com/MoonshotAI/kimi-cli/pull/2364  
   - **功能/修复内容**: 在协议层增加 ACP 权限模式切换，为 Kimi 会话声明 `default` 等权限配置；解决 Issue #1414。PR 依赖 #2363，需按顺序合并。  
   - **意义**: 补全 ACP 交互中的权限控制能力，使客户端能动态选择允许的操作范围，是 ACP 功能走向成熟的关键一步。

## 功能需求趋势

从当前全部活跃 Issue 及 PR 中，可以提炼出以下最受关注的功能方向：

- **ACP 协议生态完善**：能力模型发现（#2583）、权限模式切换（#2364）、子进程身份标记（#2585）都围绕 ACP 生态展开，说明社区希望 Kimi Code CLI 能作为后端被更多客户端无缝驱动。
- **跨会话持久化与设备无缝切换**：Memory System（#1283）和 Remote Control（#1282）代表了用户对“随时随地、长期记忆”工作流的追求，是两大长期高热度需求。
- **平台输入法兼容性**：Windows IME 字符重复 Bug（#2584）反映出非英语开发者对基础输入体验的敏感度。
- **长任务稳定性**：shell 超时自适应（#2200）表明真实场景中长命令执行比 60 秒更常见，需要更智能的超时策略。

## 开发者关注点

- **Windows 输入体验**：泰语等 IME 字符重复是直接影响日常使用的痛点，需要优先修复。
- **ACP 客户端能力不对称**：模型列表不可发现、无法中途切换模型，限制了移动端/编辑器集成场景的使用体验。
- **命令执行中断**：当运行 `git clone`、大型构建等耗时操作时，默认超时设置容易导致任务失败，开发者希望工具能自动识别慢命令并放宽限制。
- **长期服务需求**：Memory System 与 Remote Control 的持续高赞和评论数表明，开发者不满足于 CLI 仅作为临时会话工具，而是希望其成为具备持久上下文、可远程访问的日常开发基础设施。

> 数据说明：本日仅 4 个 Issue 与 3 个 PR 在统计窗口内更新，故全部列出。更多历史 Issue 可访问 [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报（2026-08-05）

## 今日速览

DeepSeek V4 Flash 系列问题集中爆发，成为社区绝对焦点：多个用户报告模型空响应、HTTP 500 错误及模型版本偏差，OpenCode Go 服务稳定性受到质疑。官方已通过 v1.18.12/v1.18.13 两个补丁版本修复 Azure GPT-5.5+ 推理失败、RTL 布局等问题，并有一条针对空响应重试的 PR 正在审查。此外，社区对 Go 套餐用量 API 的需求持续走高（126 👍）。

## 版本发布

### v1.18.13
- **TUI 修复**：GitHub PR 审查上下文现在包含 PR 编号和 URL。
- **Desktop 修复**：修复了多标签页、抽屉、调整大小和标题栏交互中的 RTL（从右到左）布局问题，以及方向性图标的共享 RTL 行为。

### v1.18.12
- **Core 修复**：修复了启用推理时 Azure GPT-5.5+ 补全请求失败的问题（感谢 @frederiknsgo）。
- **Desktop 修复**：减少了粘贴大图片或附件时 composer 的卡顿；项目搜索现在能匹配所有已知最近项目（此前仅匹配前五个）。

## 社区热点 Issues

### 1. DeepSeek V4 Flash 故障系列（#40480 / #40483 / #40460 / #40478 / #40467 等）
- **链接**：[#40480](https://github.com/anomalyco/opencode/issues/40480) | [#40483](https://github.com/anomalyco/opencode/issues/40483) | [#40460](https://github.com/anomalyco/opencode/issues/40460)
- **现象**：DeepSeek V4 Flash Free 在桌面端和 TUI 中均出现「只思考不输出」「完成音效后响应区空白」、HTTP 500 错误。多个用户发帖确认，覆盖 Windows 11 桌面端、CLI 等场景。
- **重要性**：这是当前社区影响面最广的故障，大量免费用户依赖该模型，问题持续一整天未彻底解决。

### 2. OpenCode Go 模型版本偏差（#40409）
- **链接**：[#40409](https://github.com/anomalyco/opencode/issues/40409)
- **现象**：`deepseek-v4-flash` 模型 ID 实际返回的是 V3.2（知识截止 2025-05），并非宣传的 V4 Flash 0731。
- **重要性**：涉及计费与服务质量不匹配，用户质疑 Go 服务的透明性。

### 3. DeepSeek V4 Flash 需中国托管 Opt-in（#39845）
- **链接**：[#39845](https://github.com/anomalyco/opencode/issues/39845)
- **现象**：Go 订阅用户会话中途被要求启用「中国托管模型」才能继续使用 DeepSeek V4 Flash。
- **社区反应**：22 👍、15 评论，用户对订阅服务突然变更模型可用性表示不满。

### 4. Go 套餐用量/余额 API（#16017）
- **链接**：[#16017](https://github.com/anomalyco/opencode/issues/16017)
- **内容**：请求新增公开 API 端点，暴露 Go 订阅计划的用量数据（滚动/周/月窗口），目前仅仪表盘可见。
- **社区反应**：126 👍、29 评论，是近期最受关注的功能请求，说明用户对用量透明化有强烈需求。

### 5. `opencode run` 间歇性挂起（#38723）
- **链接**：[#38723](https://github.com/anomalyco/opencode/issues/38723)
- **现象**：`opencode run` 在初始化阶段有约 56% 概率挂起，无输出、无报错，只能外部超时终止。
- **重要性**：属于核心 CLI 的稳定性问题，影响自动化脚本和 CI 场景。

### 6. Go 服务 SSE 流不完整（#40171）
- **链接**：[#40171](https://github.com/anomalyco/opencode/issues/40171)
- **现象**：`POST /v1/responses` 流式响应缺少 `response.output_item.added` 和 `response.content_part.added` 事件，导致 Codex 风格客户端解析失败。
- **重要性**：暴露了 Go 服务与 OpenAI 协议兼容性的细节缺陷。

### 7. Web 界面不实时刷新（#40502）
- **链接**：[#40502](https://github.com/anomalyco/opencode/issues/40502)
- **现象**：Web 界面新消息不实时出现，必须手动刷新页面。
- **重要性**：基础可用性问题，直接影响 Web 端用户体验。

### 8. Tmux/Kitty 下复制粘贴失效（#36646）
- **链接**：[#36646](https://github.com/anomalyco/opencode/issues/36646)
- **现象**：在 Tmux + Kitty（Linux）中运行 opencode 时，复制-选中功能失效。
- **社区反应**：该 issue 关联了至少 5 个 PR（如 #30472），属于长期存在的 TUI 痛点。

### 9. 桌面端 ECONNREFUSED 127.9.9.9:443（#40525）
- **链接**：[#40525](https://github.com/anomalyco/opencode/issues/40525)
- **现象**：干净安装后桌面应用无法连接本地 API，陷入「Cannot connect to API: connect ECONNREFUSED 127.9.9.9:443」死循环。
- **重要性**：影响新用户首次使用，可能指向安装包或本地服务启动的回归问题。

### 10. macOS 下 Ctrl+D 误退出（#40510）
- **链接**：[#40510](https://github.com/anomalyco/opencode/issues/40510)
- **内容**：请求增加配置项，在 macOS 上 Ctrl+D 退出前二次确认，避免在 Ghostty 等终端中误触。
- **社区反应**：典型的体验优化请求，评论虽少但场景真实。

## 重要 PR 进展

### 1. 修复空响应重试逻辑（#40531）
- **链接**：[#40531](https://github.com/anomalyco/opencode/pull/40531)
- **内容**：检测 provider 尝试以未知原因结束且未产生文本/推理/工具调用的情况，将其路由到现有会话重试策略，避免静默完成空的 assistant 回合。
- **重要性**：直接回应了今日 DeepSeek V4 Flash 空响应问题，如合并将从机制上缓解此类故障。

### 2. Tmux/SSH 剪贴板复制支持（#30472）
- **链接**：[#30472](https://github.com/anomalyco/opencode/pull/30472)
- **内容**：支持在 Tmux `set-clipboard on` 配置下通过 SSH 复制，关闭 #25253、#19982、#36646 等 5 个 issue。
- **重要性**：长期痛点终于有系统性修复方案。

### 3. OpenAI 兼容流式 reasoning 字段（#35284）
- **链接**：[#35284](https://github.com/anomalyco/opencode/pull/35284)
- **内容**：在 OpenAI Chat 流式 delta schema 中增加 `reasoning` 字段支持，修复部分提供商推理内容被丢弃的问题。
- **重要性**：对使用 OpenAI 兼容接口的第三方模型（包括 DeepSeek）兼容性至关重要。

### 4. 挂起工具错误处理（#35268）
- **链接**：[#35268](https://github.com/anomalyco/opencode/pull/35268)
- **内容**：即使 AI SDK 先发出 `tool-error` 再触发 `tool-call` 提升流程，也能正确结算工具错误，保留真实失败原因而非替换为「执行中止」。
- **重要性**：提升工具调用的错误可观测性和可靠性。

### 5. Bash 工具挂起修复（#35245）
- **链接**：[#35245](https://github.com/anomalyco/opencode/pull/35245)
- **内容**：改用 scope teardown 机制而非多个超时来终止产生孙进程的 bash 命令，避免 `close` 事件永不触发导致的无限挂起。
- **重要性**：修复了 #25664 中 bash 工具因孙进程继承 stdio 而死锁的问题。

### 6. 桌面端关闭到托盘（#35259）
- **链接**：[#35259](https://github.com/anomalyco/opencode/pull/35259)
- **内容**：关闭最后一个桌面窗口时隐藏到托盘/Dock 而非退出，让后台任务继续运行。
- **重要性**：提升桌面端后台任务体验，回应了多个相关 feature 请求。

### 7. 日期从 env block 移入用户消息（#35310）
- **链接**：[#35310](https://github.com/anomalyco/opencode/pull/35310)
- **内容**：将系统提示中的「今天日期」从 env block（跨午夜变化会破坏系统提示静态性）移动到用户消息，关闭 #29672 和 #32622。
- **重要性**：优化提示工程稳定性，减少跨日会话的上下文扰动。

### 8. Shell 进度输出紧凑化（#35305）
- **链接**：[#35305](https://github.com/anomalyco/opencode/pull/35305)
- **内容**：将 tqdm 等单行重绘的进度帧折叠为紧凑输出，避免刷爆 TUI 会话记录。
- **重要性**：改善 TUI 下长时间运行命令的可读性。

### 9. Kiro（AWS）Provider 支持（#20491）
- **链接**：[#20491](https://github.com/anomalyco/opencode/pull/20491)
- **内容**：通过 bundled plugin 新增 Kiro（AWS）provider，关闭 #9165 和 #26680。
- **重要性**：扩大官方支持的服务商版图，AWS 用户可直接选用。

### 10. ACP 货币尊重 Provider 配置（#39425）
- **链接**：[#39425](https://github.com/anomalyco/opencode/pull/39425)
- **内容**：修复 ACP `usage_update` 事件硬编码 `currency: "USD"` 的问题，改为尊重 provider 实际货币配置。
- **重要性**：对非美元计费用户（如人民币、欧元）的用量统计有实际意义。

## 功能需求趋势

从近期 Issues 和 PR 中可提炼出以下社区关注方向：

- **模型服务稳定性与透明度**：DeepSeek V4 Flash 系列问题（空响应、错误模型、地域限制）霸榜，用户对模型路由、版本标识和故障恢复的透明性提出更高要求。
- **用量与计费可视化**：#16017 的 Go 套餐用量 API 请求获得 126 👍，与 #40409 的「模型版本/计费不匹配」投诉相互印证，社区强烈希望用量数据可通过 API 获取。
- **剪贴板与终端集成**：Tmux/Kitty/WSL 下的复制粘贴问题长期存在（#36646、#9999），相关 PR（#30472、#35289）持续活跃，是 TUI 体验的老大难。
- **桌面端体验精细化**：RTL 布局修复（v1.18.13）、关闭到托盘（#35259）、Ctrl+D 防误触（#40510）显示社区对桌面应用细节体验的关注。
- **AI 协议兼容性**：SSE 事件完整性（#40171）、reasoning 字段支持（#35284）说明用户正将 OpenCode 作为多客户端的「模型网关」使用，协议一致性成为需求点。

## 开发者关注点

- **DeepSeek V4 Flash 不可用是当前最大痛点**：众多用户报告「thinking 后无输出」「播放完成音但响应区空白」，影响范围覆盖 Windows 桌面端、TUI、CLI 和 Go API，且一天内未根本解决。建议官方优先排查模型路由与流式输出链路。
- **Go 服务计费与质量不符引发信任危机**：#40409 指出模型 ID 返回的模型版本低于宣传值，加上 #39845 的「中国托管」突然要求，用户对订阅服务的稳定性和透明度的信任正在下降。
- **CLI 可靠性问题影响自动化**：`opencode run` 56% 的挂起率（#38723）和 bash 工具死锁（#25664）说明核心执行路径仍有稳定性隐患，对 CI 集成方是硬伤。
- **对官方响应速度的期待**：大量「not working」「stuck thinking」类 issue 在同一天涌入，部分用户表达了失望情绪，社区期待更快的 hotfix 节奏和更清晰的故障状态公告。

---
*数据来源：[github.com/anomalyco/opencode](https://github.com/anomalyco/opencode) | 更新于 2026-08-05*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-05

## 今日速览
- **v0.21.5 正式发布**：为 macOS 用户带来 Electron → Tauri 桌面应用可选迁移桥，并引入工具调用级执行结果跟踪。
- **安全与信任边界成为社区焦点**：Provider 警告清理器密码泄露、hook 执行信任边界漏洞等 Issue 引发高赞讨论。
- **ACP/IDE 集成需求持续攀升**：JetBrains 下任务列表不渲染、reasoning effort 不可配等问题集中反馈。

## 版本发布

### v0.21.5（正式版）
- **macOS 迁移桥（#8392）**：为 macOS 用户提供一次性 opt-in 更新桥，支持从旧版 Electron 桌面应用平滑迁移至新的 Tauri shell。
- **工具调用结果跟踪**：引入细粒度的执行结果追踪能力，便于观测每次工具调用的具体执行结果。

### v0.21.4-nightly.20260804.d6f55a1c9（夜间版）
- 同步包含 Electron → Tauri 桌面桥接变更（#8392）。
- 修复 Web Shell 中表格对话框相关问题。

## 社区热点 Issues（Top 10）

1. **[#8102] 确定性工具执行边界：可信 Agent 运行时的核心提议**  
   作者提出将 LLM 置于信任边界之外，由运行时确定性约束、授权、观测与评估模型动作。17 条评论，社区辩论激烈，被标记为 `need-discussion`。  
   🔗 https://github.com/QwenLM/qwen-code/issues/8102

2. **[#8519] Linux/tmux 下闪屏严重**  
   在 tmux 中使用 Qwen Code 几乎每秒闪屏 1-2 次，11 条评论，Linux 用户痛点明显。  
   🔗 https://github.com/QwenLM/qwen-code/issues/8519

3. **[#8136] Provider 警告清理器泄露密码且截断含端口信息**  
   `sanitizeProviderWarning` 在清洗 URL 时存在两个由同一原因导致的 bug：泄露包含 `@` 的密码，并错误截断含端口号的地址。6 条评论，安全风险较高。  
   🔗 https://github.com/QwenLM/qwen-code/issues/8136

4. **[#8051] 多工作区 daemon 资源使用无上限跟踪**  
   当前仅按工作区/会话数量限制，但请求体字节数、WebSocket 内存等未绑定。9 条评论，关注生产环境稳定性。  
   🔗 https://github.com/QwenLM/qwen-code/issues/8051

5. **[#8356] APIUserAbortError 后本地会话记录丢失**  
   中断后，后续轮次不再写入本地 transcript，影响通过 ACP/Web 桥接的长时间会话。5 条评论。  
   🔗 https://github.com/QwenLM/qwen-code/issues/8356

6. **[#8493] 取消的文件工具仍可修改文件系统**  
   `write_file` 和 `edit` 在异步准备期间收到 abort 后仍会继续执行写入，属于取消语义缺陷。5 条评论。  
   🔗 https://github.com/QwenLM/qwen-code/issues/8493

7. **[#8533] Content[]/Part[] 数组无法安全编码 per-provider 推理回放契约**  
   架构级问题：不同 provider 的 reasoning-replay 需求无法通过现有内容模型表达，4 条评论，`need-discussion`。  
   🔗 https://github.com/QwenLM/qwen-code/issues/8533

8. **[#8452 / #8463] 大小触发微压缩反复使 prompt 缓存失效**  
   默认超 50 万字符后，微压缩会在连续 ToolResult 轮次中反复重写已缓存前缀，严重降低缓存命中率。两条 Issue 合计 5 条评论。  
   🔗 https://github.com/QwenLM/qwen-code/issues/8452 | https://github.com/QwenLM/qwen-code/issues/8463

9. **[#8544] [ACP] JetBrains 中任务列表（plan updates）不渲染**  
   同一 JetBrains ACP 界面下，Claude Code / Codex 均可正常显示任务列表，Qwen Code 无法显示。3 条评论，IDE 集成短板。  
   🔗 https://github.com/QwenLM/qwen-code/issues/8544

10. **[#8539] 扩展 hooks 未被调用**  
   Qwen Code 支持 Claude 扩展，但扩展自带的 hooks（如 ponytail）未被执行，导致部分扩展功能失效。3 条评论。  
   🔗 https://github.com/QwenLM/qwen-code/issues/8539

## 重要 PR 进展（Top 10）

1. **[#8368] 新增 Kimi 与小米 MiMo 提供商预设**  
   在 `/auth` → 第三方提供商中加入 Kimi（Coding Plan / 中国 / 国际

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*