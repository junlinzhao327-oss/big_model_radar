# AI CLI 工具社区动态日报 2026-08-11

> 生成时间: 2026-08-10 23:00 UTC | 覆盖工具: 7 个

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

> **数据说明**：本次日报采集窗口内，Claude Code、OpenAI Codex、GitHub Copilot CLI、OpenCode 四个仓库未捕获到活跃社区动态，以下分析基于 Gemini CLI、Qwen Code、Kimi Code CLI 三个仓库的实际数据。

---

## 1. 生态全景

AI CLI 工具正从"单次对话式编码助手"向**多智能体编排平台**演进：Gemini CLI 的 subagent 机制与 Qwen Code 的 Fleet 多会话架构同时成为社区讨论焦点，子代理稳定性、状态误报等问题开始暴露，说明该方向已从概念走向规模化落地。同时，**跨会话记忆**（Kimi #1283）与**上下文持久化**正在取代基础代码补全，成为新一代差异化能力。安全层面不再是"事后修补"，SSRF 防护、OS 级沙箱、OAuth 凭据管理已进入核心迭代管线。整体呈现**功能架构复杂化、可靠性要求工程化、生态集成多元化**三大趋势。

---

## 2. 各工具活跃度对比

| 工具 | 活跃 Issues | 活跃 PRs | 版本发布 | 整体活跃度 |
|---|---|---|---|---|
| **Gemini CLI** | 10 个高热度 Issue（5 个 P1） | 7 个重要 PR（4 个 P1） | v0.56.0-nightly（8/10） | 🔥🔥🔥🔥 极高，多线并行 |
| **Qwen Code** | 9 个热门 Issue（3 个 P1） | ≥3 个 PR（#8661/#8691/#8838） | v0.21.9 + nightly | 🔥🔥🔥🔥 高，架构级 RFC 推进 |
| **Kimi Code CLI** | 1 个活跃 Issue（#1283） | 0 | 无 | 🔥 低，社区讨论集中但低频 |
| Claude Code | 未捕获 | 未捕获 | 未捕获 | 数据缺失 |
| OpenAI Codex | 未捕获 | 未捕获 | 未捕获 | 数据缺失 |
| GitHub Copilot CLI | 未捕获 | 未捕获 | 未捕获 | 数据缺失 |
| OpenCode | 未捕获 | 未捕获 | 未捕获 | 数据缺失 |

**关键指标解读**：
- **Gemini CLI 处于 Bug 密集修复期**：10 个热门 Issue 中 P1 占一半，且集中在子代理、终端交互、沙箱等核心路径，nightly 高频发版（8/10 与 8/9 连续迭代）。
- **Qwen Code 处于架构扩展期**：v0.21.9 正式发布带来 Qoder 插件生态能力，Fleet RFC（#8718）被拆分为 4 个实施阶段推进，属于"建设性"活跃。
- **Kimi Code CLI 处于需求沉淀期**：无代码产出，但 #1283 累计 31 条评论持续发酵，社区在深度讨论记忆系统的产品形态。

---

## 3. 共同关注的功能方向

### 方向一：多智能体 / 子代理编排（Gemini × Qwen）
| 工具 | 具体诉求 |
|---|---|
| Gemini | #22323 子代理超时后**误报成功**（MAX_TURNS → "GOAL"）；#21409 generalist agent 无限挂起；#21968 子代理与 skills 不被主动调用 |
| Qwen | #8718 Fleet 架构 RFC：Leader 派发 2~3 个 worker 并收集结构化结果，拆分为 1A/1B/2/3 四阶段 |

**共性痛点**：智能体协作的**可观测性**（状态上报真实性）、**调度稳定性**（挂起、死循环）和**主动性问题**（模型不主动委派），是当前所有多智能体方案的第一道坎。

### 方向二：跨会话记忆 / 上下文持久化（Kimi × Gemini）
| 工具 | 具体诉求 |
|---|---|
| Kimi | #1283 构建 Memory System：自动记忆 + 手动记忆双路径，31 条评论成为仓库最热议题 |
| Gemini | #26522 Auto Memory 对低价值 session 无限重试，说明**已有记忆机制但缺乏管理策略** |

**共性痛点**：记忆的**可干预性**（用户能否编辑/删除）与**存储边界**（本地 / 云端 / 版本控制）仍是未决问题，Kimi 在需求讨论阶段，Gemini 已进入工程化修复。

### 方向三：安全与权限控制（Gemini 主线，Qwen 侧翼）
- Gemini：#28557 SSRF 漏洞修复（异步 DNS 解析防内网探测）、#28734 macOS Seatbelt 沙箱崩溃、#22093 子代理绕过权限设置擅自运行。
- Qwen：#8863 "Update all" 静默覆盖 `model.name`/`baseUrl`，属于配置安全类问题。

**共性趋势**：安全已从"外部网络攻击面"扩展至**客户端内部信任链**——子代理权限隔离、配置防误写、沙箱兜底。

### 方向四：终端 UI / 环境兼容性（Gemini × Qwen）
- Gemini：#25166 命令执行后卡 "Waiting input"、#21983 Wayland 环境浏览器子代理失败。
- Qwen：#8124 启动横幅首行丢失（Windows）、#8557 Warp 终端缩小窗口 scrollback 重复输出（macOS）。

**共性痛点**：跨平台终端适配（Wayland/Warp/Windows）是 CLI 工具的长期负债，各厂商均在补齐。

---

## 4. 差异化定位分析

| 维度 | Gemini CLI | Qwen Code | Kimi Code CLI |
|---|---|---|---|
| **核心价值主张** | 安全、可靠的企业级编码代理 | 可扩展的开放编码平台 | 轻量、能"记住"你的编码伙伴 |
| **架构重心** | Subagent 多级代理 + OS 沙箱 + MCP 生态 | Fleet 多会话编排 + Qoder 插件系统 + serve 模式 | （尚不明确，memory 为当前主线） |
| **技术路线特征** | **防御纵深**：AST 感知（#22745）、零依赖沙箱提案（#19873）、异步 DNS 防 SSRF——倾向底层安全能力自建 | **生态开放**：插件可来自目录/Git/npm/URL 任意来源，ACP 子进程支持外部自动化调用 | **产品克制**：无频繁发版，集中打磨单点体验 |
| **目标用户** | 企业/安全敏感型团队，深度依赖 MCP 与自定义 agent 配置的用户 | 需要多模型切换、内网网关、插件定制的开发者与自动化集成方 | 追求会话连续性与低配置成本的个人开发者 |
| **当前阶段** | Bug 扫尾 + 安全加固期 | 架构升维 + 生态扩张期 | 需求探索 + 形态打磨期 |

---

## 5. 社区热度与成熟度

### 社区热度排序
1. **Gemini CLI**——评论互动最密集（Top Issue #22323 单日 12 条评论），8 个 👍 出现在 #21409，P1 问题响应迅速，社区反馈闭环快。
2. **Qwen Code**——10 个热门 Issue 覆盖架构/UI/性能/CI 多领域，RFC #8718 引发分阶段落地讨论，社区参与层次较高（含架构设计讨论）。
3. **Kimi Code CLI**——单一 Issue 长期累计 31 条评论但单日增量有限，属于"高深度、低广度"讨论形态。

### 成熟度判断
- **Gemini CLI**：**快速迭代期（0.x nightly）**，但功能广度和深度已接近生产级；当前主要风险是 P1 Bug 密度偏高（核心路径 5 个 P1 同时在修），适合尝鲜型团队，生产落地需关注子代理稳定性修复进度。
- **Qwen Code**：**健康成长期**，v0.21.x 稳定发版 + RFC 推动大功能前进，P1 Bug 多为回归问题（#8863 是 #5819 回归），说明已有用户基数并形成测试反馈循环。
- **Kimi Code CLI**：**发展早期**，活跃度最低，但 Memory System 一旦落地可能形成独特卖点；当前生态规模和迭代速度尚不足以支撑企业级评估。

---

## 6. 值得关注的趋势信号

### 信号一：子代理可靠性 = 下一代 CLI 的生死线
Gemini #22323 暴露的问题极具代表性：**子代理超时却上报成功**，会导致主代理基于错误状态做决策，产生连锁的隐蔽错误。随着多智能体方案（Fleet、subagent）进入主流，**状态真实性与执行可观测性**将成为用户选择工具的核心评估项。开发者应关注各工具对"中断/失败/降级"语义的透明化程度。

### 信号二：Memory System 将从"加分项"变为"标配"
Kimi #1283 的热度（31 评论 + 持续 6 个月）与 Gemini Auto Memory 的工程化修复共同表明：**会话状态持久化已成为共识需求**。下一阶段竞争点在于记忆的**可编辑性、检索效率与多项目隔离**，而非简单的"是否拥有"。对开发者的参考价值：选择工具时评估其记忆机制是否透明可控（能否一键清除、是否本地存储）。

### 信号三：安全能力正从"外围"移入"内核"
Gemini 的 SSRF 修复（异步 DNS 校验绕过验证）、沙箱崩溃修复、子代理权限绕过三件事同时发生，标志着一线工具已开始为**不可信代码执行**场景做实质准备。叠加 Qwen #8863 的配置静默覆盖问题，"配置可信、执行可控"正在成为基础要求。引入 AI CLI 到生产环境前，建议优先核查其沙箱模型与权限边界。

### 信号四：插件生态是下一轮竞争的差异化战场
Qwen 的 Qoder 插件支持目录/压缩包/Git/URL/npm 五种来源安装，明显是在对标 IDE 插件市场的分发体验；Gemini 则以 MCP OAuth 修复（#28481）和 IDE 连接目录修复（#28729）夯实集成底座。**谁的插件分发链路更顺、认证体验更平滑，谁就能锁定更多企业用户**。

### 信号五：开发环境碎片化仍在吞噬工具投入
从 Wayland（#21983）、Warp（#8557）、Windows 首行渲染（#8124）、Cloud Workstations OAuth（#28688）到远程 VS Code fork（#28729），大量 P1/P2 精力被环境适配消耗。这是 CLI 工具的**结构性成本**，短期内难以消除。对团队决策者的启示：优先在主流统一环境下验证工具，

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



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-11

## 今日速览
过去 24 小时，Gemini CLI 发布 v0.56.0 nightly 版本，社区讨论热度集中在**子代理（Subagent）稳定性**问题上——`MAX_TURNS` 被误报为成功、generalist agent 无限挂起等 bug 持续发酵。安全方面有多项重要 PR 推进，包括 SSRF 漏洞修复、macOS 沙箱崩溃修复及 MCP OAuth token 刷新修复。

---

## 版本发布

**v0.56.0-nightly.20260810.gcf22ac7e8** 已于 8 月 10 日发布。具体变更内容未随 release notes 提供，可查看 [完整 Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260809.gcf22ac7e8...v0.56.0-nightly.20260810.gcf22ac7e8) 了解详情。值得留意的是，仓库中已有自动化版本 bump PR（#28758）在同步推进。

---

## 社区热点 Issues

以下为过去 24 小时内更新最活跃、社区关注度最高的 10 个 Issue：

### 1. Subagent 在 MAX_TURNS 后误报为 GOAL 成功
[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — **12 条评论** | P1 | kind/bug
`codebase_investigator` 子代理在达到最大轮次限制后，仍返回 `status: "success"` + `Termination Reason: "GOAL"`，**掩盖了实际的执行中断**。这会导致主代理误以为子任务顺利完成，属于隐蔽的可靠性问题，社区评论最活跃。

### 2. Generalist agent 无限挂起
[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — **8 条评论，8 👍** | P1 | kind/bug
用户报告只要 Gemini CLI 将任务委托给 generalist agent 就会永久挂起，连创建文件夹这类简单操作也无法完成，有用户等待长达一小时。通过指示模型不要使用子代理可绕过。8 个 👍 表明影响面较大。

### 3. Shell 命令执行后卡在 "Waiting input"
[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — **4 条评论，3 👍** | P1 | kind/bug
简单的 CLI 命令执行完毕后，界面仍显示命令活动并停留在“等待用户输入”状态。这是终端交互类核心 bug，多用户重复遇到。

### 4. Gemini 不会主动使用 skills 和子代理
[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — **6 条评论** | P2 | kind/bug
用户反馈 Gemini 几乎从不主动调用自定义 skills 和子代理，即使任务高度相关。只有在用户明确指示时才会使用，导致自定义技能形同虚设。

### 5. Auto Memory 无限重试低价值 session
[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) — **5 条评论** | P2 | kind/bug
Auto Memory 后台提取 agent 遇到低信号 session 时，会跳过处理但不记录结果，导致这些 session 反复出现并无限占用重试资源。

### 6. Browser 子代理在 Wayland 环境失败
[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — **4 条评论** | P1 | agent/browser
浏览器子代理在 Wayland 显示服务器环境下启动失败，影响面涉及 Linux 用户群体。

### 7. 零依赖 OS 沙箱 + 执行后意图路由
[#19873](https://github.com/google-gemini/gemini-cli/issues/19873) — **8 条评论** | P2 | kind/enhancement
提案建议利用 Gemini 模型原生擅长 bash 的特点，通过零依赖 OS 级沙箱 + 执行后意图路由来替代当前 shell 调用方案，目标是兼顾模型能力与用户安全。属于较大的架构级 enhancement。

### 8. AST 感知的文件读取/搜索/代码库映射评估
[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) — **7 条评论** | P2 | kind/feature
跟踪一系列调研，评估 AST 感知工具能否减少 token 噪音、精确读取方法边界、提升代码库探索效率。有望优化未来核心 agent 的代码理解能力。

### 9. 子代理绕过权限设置擅自运行
[#22093](https://github.com/google-gemini/gemini-cli/issues/22093) — **3 条评论** | P2 | kind/bug
用户升级到 v0.33.0 后，即使在所有配置中禁用了 agents 模式，子代理仍会被自动触发执行。对权限控制有严格要求的用户构成安全隐患，需要尽快修复。

### 10. `~/.gemini/agents/` 中的 symlink 不被识别
[#20079](https://github.com/google-gemini/gemini-cli/issues/20079) — **4 条评论** | P2 | kind/bug
如果自定义 agent 文件（`filename.md`）是符号链接，则不会被识别为有效 agent。影响使用 dotfiles 管理工具维护配置的用户，问题虽小但困扰真实用户群体。

---

## 重要 PR 进展

以下为过去 24 小时内更新的 10 个重要 PR：

### 1. 修复 MCP OAuth token 刷新时删除已存凭据
[#28481](https://github.com/google-gemini/gemini-cli/pull/28481) — **P1** | 已关闭
对于通过 OAuth discovery + 动态客户端注册配置的 MCP 服务器，token 刷新在发起网络请求前即失败，且失败会删除已保存的凭据，导致每次都需要重新认证。此 PR 修复了该问题。

### 2. 修复 web-fetch 的 SSRF 漏洞（异步 DNS 解析）
[#28557](https://github.com/google-gemini/gemini-cli/pull/28557) — **P1** | 开放
修复 SSRF：`isBlockedHost` 原先仅检查字面 IP，恶意域名解析到内网地址（如 `169.254.169.254`）即可绕过验证。改用已有的 `isPrivateIpAsync` 进行异步 DNS 解析后校验，杜绝内网探测风险。

### 3. 修复 macOS Seatbelt 沙箱导致启动崩溃
[#28734](https://github.com/google-gemini/gemini-cli/pull/28734) — **P1** | 开放
当 macOS Seatbelt 沙箱启用且 CWD 位于 Git 仓库内时，`resolveToRealPath` 遇到 `EACCES` 错误未捕获导致 CLI 启动崩溃。补上了这一异常场景的错误处理。

### 4. 修复模型容量耗尽误报 + quota 查询映射
[#28730](https://github.com/google-gemini/gemini-cli/pull/28730) — 开放
解决 CLI 中模型容量耗尽（capacity exhaustion）错误误报的问题，修正 core 包中客户端侧模型 quota 查询映射，并确保 UI 中的“Keep trying”选项在瞬时容量高峰时保留。

### 5. Cloud Workstations 中 OAuth 重定向 URI 动态解析
[#28688](https://github.com/google-gemini/gemini-cli/pull/28688) — **P3** | 开放
修复 Google Cloud Workstations VM 中 OAuth 2.0 流程失败的问题：原先静态配置回环地址 `localhost`，在浏览器与开发环境分离的 Workstations 场景下重定向失败。改为动态解析代理地址。

### 6. IDE 连接目录不匹配修复
[#28729](https://github.com/google-gemini/gemini-cli/pull/28729) — 开放
修复在 Cider 或 VS Code fork/远程工作区中使用虚拟目录路径时，Gemini CLI 无法连接 IDE companion extension 的问题。此前端口文件存在但 workspace 路径不匹配时错误被静默吞掉。

### 7. 修复 boolean thought parts 泄漏为 `[Thought: true]`
[#28624](https://github.com/google-gemini/gemini-cli/pull/28624) — **P2** | 开放

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-08-11

> 数据来源：github.com/MoonshotAI/kimi-cli  
> 统计窗口：2026-08-10 至 2026-08-11（约 24 小时）

## 今日速览

过去 24 小时内，Kimi Code CLI 仓库无新版本发布、无 Pull Request 更新，社区活动集中在 Issue 讨论上。最值得关注的是 `#1283` 关于 **持久化 Memory System（跨会话记忆）** 的功能请求——该 Issue 自 2 月创建以来持续讨论，昨日新增更新，已积累 31 条评论，可见社区对“会话记忆”能力的诉求强烈且讨论热度长期不减。

## 社区热点 Issues

> 注：本期统计窗口内仅有 1 个 Issue 发生更新，故只做单点深度分析。

### #1283 [enhancement] Memory System - Persistent context across sessions

- **作者**: @CatKang  
- **创建时间**: 2026-02-27  
- **更新时间**: 2026-08-10  
- **评论数**: 31 | 👍 0  
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/1283  
- **状态**: Open

**核心诉求**：实现一套完整的 Memory System，使 Kimi Code CLI 能跨会话记住项目上下文、代码风格约定、用户偏好等信息。该机制包含两条路径：

1. **自动记忆（AI-managed）**——由 AI 在对话过程中自动沉淀笔记，学习用户习惯；
2. **手动记忆（User-defined）**——用户通过显式指令或配置文件，固化团队规范、项目约束等内容。

**为什么值得关注**：这是当前 AI 编程助手的核心痛点之一——默认无状态的会话机制，导致每次新开 session 都要重新交代项目背景，也切断了用户 Agent 学习长期协作模式的可能性。31 条评论说明开发者对“自动记忆与手动记忆如何协同”“记忆存储位置与隐私边界”“记忆内容如何在命令行中被高效检索/引用”等实现细节有较高讨论热情。

## 功能需求趋势

> 因本期 Issue 样本有限，以下趋势主要结合 `#1283` 的高热度讨论及 AI CLI 工具领域整体发展路径进行研判。

- **跨会话长期记忆**：开发者希望 CLI 工具不只是“一次性对话交互”，而是能记住项目进展、用户偏好和历史决策，形成可持续累积的上下文资产。
- **记忆的分类管理**：从 `#1283` 的讨论可看出，社区对“AI 自动记录的隐式记忆”与“用户/团队显式定义的结构化记忆”均有需求，且期待二者通过某种机制融合（例如自动记忆可沉淀为一个独立文件，并支持用户人工修正）。
- **上下文能力的“工程化”**：Memory System 背后是对上下文窗口利用效率的更高要求——如何筛选、压缩、持久化上下文，未来可能成为 AI CLI 的核心差异化能力。
- **团队协作场景萌芽**：手动记忆的描述涉及“project patterns / user preferences”，已有评论进一步讨论记忆文件纳入版本控制、供团队共享的可能性。

## 开发者关注点

- **会话上下文丢失**：每次新开 session 后，AI 完全丢失此前积累的代码风格偏好、项目结构信息和用户操作习惯，需要反复重复上下文，体验割裂。
- **记忆的“可干预性”**：开发者希望既能自动沉淀记忆，又能手动编辑/删除记忆内容，避免 AI 记下错误或过时的信息，同时需要清晰的记忆管理界面（即使是 CLI 命令）。
- **隐私与存储边界**：31 条评论中隐含着对“记忆存到哪里”的担忧——纯本地文件、云端同步或 `.kimi/` 目录内管理模式，各方存在不同诉求。
- **实用主义优先**：点赞数不高（👍 0）而评论数较多，说明该需求关注度高但方案争议较大，社区更期待一个轻量、可自托管、兼容现有 Git 工作流的实现，而非重量级外部存储依赖。

---

**数据说明**：本期统计窗口内，该仓库无新 Release、无 PR 更新，仅 1 个 Issue 活跃，因此日报聚焦于该 Issue 的深度分析。完整历史 Issue / PR 可访问 [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli) 主页查看。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-11

## 今日速览

- **v0.21.9 正式发布**：新增 Qoder 插件多来源安装（目录/压缩包/Git/URL/npm）和 Local Control 二维码配对，插件生态接入门槛进一步降低。
- **多智能体「Fleet」架构正式公开**：RFC #8718 提出原生多会话协调路径，并拆分为 1A、1B、2、3 四个实施阶段，社区讨论活跃。
- **两个 P1 级会话/配置 Bug 集中曝光**：rewind 索引错配（#8885）与 built-in provider 更新静默改写模型配置（#8863），成为开发者最关心的稳定性问题。

---

## 版本发布

### v0.21.9
- **Qoder 插件安装能力增强**：支持从目录、归档文件、Git 仓库、URL 和 npm 包安装 Qoder 插件，并自动加载系统提示词（[#8661](https://github.com/QwenLM/qwen-code/pull/8661)）。
- **Local Control 配对**：新增二维码配对方式，简化局域网内设备连接流程。

### v0.21.8-nightly.20260810.55e20db328
- 核心层支持 Qoder 插件扩展（[#8661](https://github.com/QwenLM/qwen-code/pull/8661)）。
- CI 改进：自动将 issue 分配给对应的 area owners。

---

## 社区热点 Issues（Top 10）

### 1. RFC: 原生协调独立 Qwen 会话 — [#8718](https://github.com/QwenLM/qwen-code/issues/8718)
- **类型**：Feature Request（P2）｜ 8 条评论
- **要点**：提出多会话协作的 RFC——Leader 可派发 2~3 个独立 worker 并保持自身交互，观察运行时/任务状态、收集结构化结果。这是 Fleet 架构的纲领性 issue。
- **关注理由**：被拆分为 #8840、#8841、#8843 等多个实施阶段，社区对多智能体方向关注度极高。

### 2. fix(session): 对齐 rewind 索引与自动 user-role 历史条目 — [#8885](https://github.com/QwenLM/qwen-code/issues/8885)
- **类型**：Bug（P1，core/session-management）｜ 3 条评论
- **要点**：PR #8838 暴露了模型侧 Content history（含 cron、后台通知、stop continuation 等自动 user 条目）与 ChatRecordingService turn 边界之间的索引空间不一致，可能导致 rewind 行为错乱。
- **关注理由**：P1 严重级别，直接影响会话回退正确性，属于核心数据一致性问题。

### 3. fix(serve): 大体积 restore 超时时保留当前会话 — [#8678](https://github.com/QwenLM/qwen-code/issues/8678)
- **类型**：Bug（P1，session-management/latency/memory）｜ 3 条评论
- **要点**：会话恢复超时可能导致当前会话被破坏，PR1 已合并（#8691），剩余部分继续跟进。
- **关注理由**：P1 + 超时场景下的用户体验与数据安全，与会话管理稳定性直接相关。

### 4. bug(providers): built-in provider 更新静默覆盖 model.name / baseUrl — [#8863](https://github.com/QwenLM/qwen-code/issues/8863)
- **类型**：Bug（P1，#5819 回归，已关闭）｜ 2 条评论
- **要点**：选择 “Update all” 后，settings.json 中指向其他 provider 的 `model.name` 被改写为该 provider 内置第一个模型，`model.baseUrl` 被清空。使用自建代理/内网网关的用户受影响。
- **关注理由**：配置静默丢失风险极高，P1 回归问题，涉及多厂商模型切换场景。

### 5. Startup banner 首次绘制缺失顶部行 — [#8124](https://github.com/QwenLM/qwen-code/issues/8124)
- **类型**：Bug（P2，UI/rendering/Windows）｜ 10 条评论
- **要点**：TUI 启动横幅（ASCII logo + provider 信息）首次绘制时可能丢失前 3 行，与 pending provider 更新相关，非覆盖问题。
- **关注理由**：评论数最高，Windows 与渲染相关，且已标记 `welcome-pr`，社区修复意愿强。

### 6. 缩小终端窗口导致 scrollback 重复输出 — [#8557](https://github.com/QwenLM/qwen-code/issues/8557)
- **类型**：Bug（P3，UI/rendering/macOS）｜ 8 条评论
- **要点**：macOS Warp 终端下，缩小窗口宽度会触发 transcript 块重复打印到 scrollback，同一内容叠加出现。
- **关注理由**：典型终端兼容性问题，影响日常使用；评论与截图丰富，便于复现与修复。

### 7. ACP 子进程报 “Unknown argument: acp” — [#8871](https://github.com/QwenLM/qwen-code/issues/8871)
- **类型**：Bug（P2，CLI/daemon）｜ 4 条评论
- **要点**：`qwen serve --http-bridge=true`（默认）生成的 ACP 子进程无法解析 `--acp` 参数，导致 token 认证失败（401）。
- **关注理由**：serve 模式下的 ACP 集成链路断裂，直接影响自动化调用方。

### 8. OpenAI API 日志无界增长（~95 GB / 34 万文件）— [#8860](https://github.com/QwenLM/qwen-code/issues/8860)
- **类型**：Bug（P2，performance/logging）｜ 2 条评论
- **要点**：`model.enableOpenAILogging` 开启后，每次调用写一个 JSON 文件到 `logs/openai`，无轮转或保留策略，两个月可累积约 95 GB。
- **关注理由**：存储占用问题严重，生产环境长期运行可能拖垮磁盘，亟需日志管理策略。

### 9. Autofix 推送与 review-pr 形成互相取消的循环 — [#8888](https://github.com/QwenLM/qwen-code/issues/8888)
- **类型**：Bug（P2，GitHub Actions）｜ 3 条

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*