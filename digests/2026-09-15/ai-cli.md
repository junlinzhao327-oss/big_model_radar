# AI CLI 工具社区动态日报 2026-09-15

> 生成时间: 2026-09-15 00:42 UTC | 覆盖工具: 7 个

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

# Claude Code 社区动态日报（2026-09-15）

## 1. 今日速览

今日社区焦点仍集中在**成本与配额信任**：Max 计划限额异常消耗 Issue 已累积 851 条评论、476 个 👍，同时 Opus 5 xhigh 的 thinking/token 异常膨胀报告继续发酵。扩展体系方面，Mods / function hooks 讨论保持高热，社区期待 Claude Code 进一步开放 hooks、plugins 与 subagent 控制能力。平台侧，Windows Cowork/Plan9、Linux sandbox 和 Windows 桌面 PowerShell 延迟等问题构成新的

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 · 2026-09-15

数据来源：[github.com/openai/codex](https://github.com/openai/codex)

---

## 1. 今日速览

- 24 小时内连发 **3 个 `rust-v0.155.0-alpha` 预发布版本**（alpha.5 / alpha.4 / alpha.2.4），迭代节奏密集，但 Release Notes 未附带任何变更说明。
- 社区热度高度集中在 **Windows 桌面端与 Computer Use 稳定性**：截图接口调用失败（[#25178](https://github.com/openai/codex/issues/25178)）以 59 条评论、25 个赞稳居榜首，且已持续三个多月未闭环。
- 工程侧主线是 **沙箱与后台服务架构**：当日 20 条高活跃 PR 中过半围绕 Windows 沙箱账号注册、daemon 安装解耦与 Unix socket 权限修复。

---

## 2. 版本发布

过去

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 · 2026-09-15

> 数据来源：[github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)

---

## 一、今日速览

今日仓库保持 nightly 节奏推进，唯一新版本为 `v0.61.0-nightly.20260914`，无重大功能变更。社区讨论热度集中在**子代理（Subagent）可靠性**与**安全加固**两条主线：一方面多起 P1 级 bug 指向 agent 挂起、错误上报成功、shell 交互卡死；另一方面，企业策略目录权限校验、沙箱扩展递归上限、A2A 日志凭据泄漏等修复 PR 密集提交。

---

## 二、版本发布

**v0.61.0-nightly.20260914.g9c1b0a610**

- 由机器人提交的自动化 nightly 版本号递增（对应 PR [#29321](https://github.com/google-gemini/gemini-cli/pull/29321)），无单独变更说明。
- Full Changelog：https://github.com/google-gemini/gemini-cli/compare/v0.61.0-nightly.20260913.g9c1b0a610...v0.61.0-nightly.20260914.g9c1b0a610

---

## 三、社区热点 Issues（Top 10）

**1. [#22323](https://github.com/google-gemini/gemini-cli/issues/22323) [P1] Subagent 达到 MAX_TURNS 后被上报为 GOAL 成功**（13 条评论）
`codebase_investigator` 子代理在未完成任何分析、已触发最大轮次限制的情况下，仍返回 `status: "success"` 与 `Termination Reason: "GOAL"`。这会掩盖中断事实，让上层 agent 和用户误以为任务成功——属于**结果可信度**层面的严重问题，是今日评论数最高的 Issue。

**2. [#21409](https://github.com/google-gemini/gemini-cli/issues/21409) [P1] Generalist agent 无限挂起**（8 条评论，👍 8）
一旦 CLI 委派给 generalist agent，即使只是"创建文件夹"这类简单操作也会永久卡住，用户等待长达一小时。禁用子代理委派可规避，说明问题出在**委派链路的调度/回收**上。这是今日点赞数最高的 Issue，社区共鸣强烈。

**3. [#25166](https://github.com/google-gemini/gemini-cli/issues/25166) [P1] Shell 命令执行完成后仍卡在 "Waiting input"**（4 条评论，👍 3）
极具迷惑性：命令实际已结束，但 TUI 仍显示命令活跃并"等待用户输入"。对于不读取 stdin 的简单命令也会复现，属于**终端交互状态机**的经典缺陷。

**4. [#21968](https://github.com/google-gemini/gemini-cli/issues/21968) [P2] Gemini 不主动使用 skills 与 sub-agents**（6 条评论）
用户反馈：即使配置了 `gradle`、`git` 等描述清晰的 skill，模型也几乎不会自主调用，只有显式指令才触发。这直接削弱了自定义 skills / 子代理生态的价值，指向**工具选择策略（tool routing）**需要增强。

**5. [#22745](https://github.com/google-gemini/gemini-cli/issues/22745) [P2] AST 感知的文件读取、搜索与代码库映射评估**（7 条评论）
一个 EPIC 级议题：用 AST 感知工具精确读取方法边界，减少错位读取带来的轮次浪费与 token 噪声。这是**上下文效率**方向的重要探索，与 [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)、[#19561](https://github.com/google-gemini/gemini-cli/issues/19561)（Tactful Extraction）形成完整的技术线索。

**6. [#19873](https://github.com/google-gemini/gemini-cli/issues/19873) [P2] 零依赖 OS 沙箱 + 执行后意图路由**（9 条评论）
核心论点：Gemini 3 模型天生擅长以 bash 方式工作（`grep`/`sed`/`awk` 链式操作），现有权限模型却限制了这种原生能力。提议通过零依赖 OS 沙箱释放模型能力，同时不牺牲安全与体验。评论数第二高，是**架构级**讨论。

**7. [#26525](https://github.com/google-gemini/gemini-cli/issues/26525) [P2] Auto Memory 需要确定性脱敏并减少日志**（5 条评论）
Auto Memory 会把本地会话转录内容发送给后台提取模型，脱敏仅在提示词中要求、发生在内容**已进入模型上下文之后**，服务还会记录既有 skill 信息。与 [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)、[#26523](https://github.com/google-gemini/gemini-cli/issues/26523)、[#26516](https://github.com/google-gemini/gemini-cli/issues/26516) 同属 Memory 系统系列问题，隐私风险明确。

**8. [#24246](https://github.com/google-gemini/gemini-cli/issues/24246) [P2] 工具数量超过 128 个时触发 400 错误**（3 条评论）
标题写 128、正文写 400，说明阈值边界本身就不清晰。对于启用大量 MCP server / extensions 的重度用户，这会导致直接不可用，需要 agent 更智能地收敛工具范围。

**9. [#21983](https://github.com/google-gemini/gemini-cli/issues/21983) [P1] Browser subagent 在 Wayland 下失败**（4 条评论）
Linux Wayland 环境下浏览器子代理直接报 `Termination Reason: GOAL` 结束但无实际产出。Linux 桌面用户的**平台兼容性**诉求，长期未解决。

**10. [#22672](https://github.com/google-gemini/gemini-cli/issues/22672) [P2] Agent 应停止/劝阻破坏性行为**（3 条评论）
在复杂 git 操作、分支管理、数据库维护等场景，模型会随手使用 `git reset`、`--force` 等危险命令。这是**安全护栏**类需求，与沙箱、权限策略议题互相呼应。

> 其他值得留意的更新：[#21335](https://github.com/google-gemini/gemini-cli/issues/21335) `/compress` 在会话恢复后不持久；[#22598](https://github.com/google-gemini/gemini-cli/issues/22598) 希望 `/chat share` 能导出子代理轨迹；[#20079](https://github.com/google-gemini/gemini-cli/issues/20079) `~/.gemini/agents/` 下符号链接不被识别；[#22465](https://github.com/google-gemini/gemini-cli/issues/22465) 创建 Vite 应用时卡在交互式提示。

---

## 四、重要 PR 进展（Top 10）

**1. [#29335](https://github.com/google-gemini/gemini-cli/pull/29335) [P1][core] 修复 AgentLoopContext 属性在对象展开中丢失**
`Config` 类此前用原型 getter 实现 `AgentLoopContext` 接口，对象展开后这些属性会全部丢失。这是影响 agent 循环上下文完整性的基础性修复，优先级 P1。

**2. [#29332](https://github.com/google-gemini/gemini-cli/pull/29332) [P2][core] 限制单次调用可扩展沙箱的次数**
当工具每次返回 `sandbox_expansion_required` 时，`_execute` 会无计数地递归自调用，进程会因堆内存耗尽而报 `FATAL ERROR: Ineffective mark-compacts near heap limit` 直接崩溃。这是**拒绝服务级别的稳定性修复**。

**3. [#29328](https://github.com/google-gemini/gemini-cli/pull/29328) [P1][security] A2A Server 遵守 LOG_LEVEL 且不将凭据写入日志**
`LOG_LEVEL` 虽被加入 `allowedServerKeys` 允许列表，logger 却硬编码 `level: 'info'`，配置形同虚设；同时日志中会输出凭据。安全级别 P1。

**4. [#29327](https://github.com/google-gemini/gemini-cli/pull/29327) [P2][agent] SDK 的 AgentShellOptions env 与 timeoutSeconds 生效**
`SdkAgentShell.exec` 接收 3 个字段却忽略其中 2 个：`env` 从未传入进程，`timeoutSeconds` 完全不起约束作用，`exec('sleep 30', { timeoutSeconds: 1 })` 会足足等满 30 秒。SDK 用户的直接痛点。

**5. [#29333](https://github.com/google-gemini/gemini-cli/pull/29333) [P2][enterprise] 校验"按约定发现"的策略目录权限**
`filterSecurePolicyDirectories` 原本只对系统策略目录做 `isDirectorySecure` 检查，用户级与工作区级目录被读取却未经权限校验——没有任何显式声明的目录只能依赖自身权限来担保安全。企业场景的关键加固。

**6. [#29336](https://github.com/google-gemini/gemini-cli/pull/29336) [P2][enterprise] 保护非系统策略目录免遭写权限风险**（Fixes [#29311](https://github.com/google-gemini/gemini-cli/issues/29311)）
把 `isDirectorySecure` 校验从"仅系统级"扩展到全部层级，并支持 POSIX/Windows 下的当前用户所有权判定。

**7. [#29329](https://github.com/google-gemini/gemini-cli/pull/29329) [P2][cli] 截断后暂停 stdin，并在放弃时明确告知**
指出 `process.stdin.destroy()` 在截断后**不可逆**——销毁后的 stdin 在进程余下生命周期内无法再读取，后续读取者会拿到空内容。改为暂停而非销毁，是更稳妥的 I/O 处理方式，与 [#25166](https://github.com/google-gemini/gemini-cli/issues/25166) 的 "Waiting input" 卡死问题同源。

**8. [#29330](https://github.com/google-gemini/gemini-cli/pull/29330) [P2][cli] 保留用户在 logger 响应前键入的内容，并只读取一次**
修复 `setCurrentSessionMessages` updater 内部调用 `setPastSessionMessages` 的 React 纯度违规，同时排查出两个非理论性的输入丢失问题。

**9. [#29323](https://github.com/google-gemini/gemini-cli/pull

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-09-15）

## 1. 今日速览

过去 24 小时内，Copilot CLI 连续发布 **v1.0.84-6** 和 **v1.0.84-7**，重点引入 `/config` 侧边栏配置、`/sandbox` 网络规则，并修复 Claude 模型 thinking 模式与 `/clear` 会话钩子问题。社区 Issues 活跃，**MCP 协议兼容性、新模型工具限制、沙箱与企业策略、会话稳定性**成为高频主题；过去 24 小时无 Pull Request 更新。

## 2. 版本发布

### v1.0.84-7
链接：https://github.com/github/copilot-cli/releases  
- **Fixed**：修复发送给 Claude 模型的 thinking shape，被归类为 adaptive-only 的模型现在保持 adaptive，不再失败；当 thinking 禁用时，推理努力改为降低，并封顶为 high。  
- **Fixed**：当 `/clear` 关闭会话时，运行 `sessionEnd` hooks。

### v1.0.84-6
链接：https://github.com/github/copilot-cli/releases  
- **Added**：新增 `/config`，可在 CLI 中打开侧边栏配置界面。  
- **Added**：新增 `/sandbox` 网络主机允许/拒绝规则，且不会替换已配置的上游代理。  
- **Improved**：将托管 Edit 和 Write 规则应用于可识别的原生 shell 重定向及支持的就地 `sed` 操作。

## 3. 社区热点 Issues

以下挑选 10 个过去 24 小时内更新、最值得关注的 Issue：

1. **#4525 [CLOSED] [area:mcp] 1.0.81-1 在成功的现代 `server/discover` 后发送 legacy `initialize`，导致 -32022**  
   链接：https://github.com/github/copilot-cli/issues/4525  
   重要性：MCP 初始化协议兼容性直接阻塞 stdio server 连接，影响使用 Python MCP SDK 2.0.0 双时代运行器的用户。社区反应：7 条评论、3 个 👍，已关闭，说明官方修复响应较快。

2. **#4725 [OPEN] [area:platform-linux] 频繁 JavaScript heap out of memory**  
   链接：https://github.com/github/copilot-cli/issues/4725  
   重要性：Linux 平台下 CLI 每隔几分钟因堆内存耗尽崩溃，严重影响长时间任务稳定性。社区反应：5 条评论、1 个 👍，属于高优先级稳定性问题。

3. **#4505 [OPEN] [area:sessions, area:networking] 恢复会话后连接项 ID 过期，所有提示失败**  
   链接：https://github.com/github/copilot-cli/issues/4505  
   重要性：恢复已有会话后持续报 `CAPIError: 400 input item ID does not belong to this connection`，且 `/fork` 也无法恢复，直接中断工作流。社区反应：4 条评论、3 个 👍。

4. **#4549 [OPEN] [triage] [Windows] 每条 shell 命令都会弹出可见 PowerShell 控制台窗口**  
   链接：https://github.com/github/copilot-cli/issues/4549  
   重要性：Windows 下每次执行 shell 命令都会闪烁并抢占焦点，严重影响日常使用体验。社区反应：2 条评论、1 个 👍。

5. **#4556 [OPEN] [area:plugins, area:configuration] 服务端管理的 `extraKnownMarketplaces` 被获取但从未注册市场**  
   链接：https://github.com/github/copilot-cli/issues/4556  
   重要性：企业侧下发的插件市场配置无法生效，`copilot plugin marketplace list` 只显示默认市场，影响插件生态推广。社区反应：2 条评论、2 个 👍。

6. **#3572 [OPEN] [area:agents, area:enterprise] 工作目录无 GitHub 托管仓库时，组织级自定义代理不可见**  
   链接：https://github.com/github/copilot-cli/issues/3572  
   重要性：企业组织在 `.github-private` 中定义的自定义代理，必须从包含该组织 GitHub 远程仓库的目录启动才可见，限制了企业代理的普适性。社区反应：2 条评论、3 个 👍。

7. **#4846 [OPEN] [triage] 启用“允许开发工具访问”后，沙箱策略对某些命令被忽略**  
   链接：https://github.com/github/copilot-cli/issues/4846  
   重要性：沙箱文件系统策略在 `python` 等命令下被绕过，属于安全边界问题。社区反应：新 Issue，暂无评论，但安全影响高。

8. **#4844 [OPEN] [triage] `--yolo` 启动标志被预认证 fail-closed 绕过上限吞掉，策略解析后未重新应用**  
   链接：https://github.com/github/copilot-cli/issues/4844  
   重要性：交互启动时，预认证窗口应用 fail-closed 姿态会禁用 bypass 权限模式，导致 `--yolo` / `--allow-all` 失效，涉及权限策略一致性。社区反应：新 Issue，暂无评论。

9. **#4836 [OPEN] [triage] Grok 4.5：351 个工具时返回 HTTP 400，而非报告 350 工具限制**  
   链接：https://github.com/github/copilot-cli/issues/4836  
   重要性：新模型 Grok 4.5 对工具数量有 350 上限，但 CLI 未提前检查或给出清晰错误，导致请求直接失败。社区反应：新 Issue，暂无评论，反映新模型适配痛点。

10. **#4834 [OPEN] [triage] 支持 MCP 2026-07-28 多轮往返请求（`input_required`）**  
    链接：https://github.com/github/copilot-cli/issues/4834  
    重要性：Copilot 当前不支持 MCP 2026-07

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-09-15）

数据源：github.com/MoonshotAI/kimi-cli  
今日数据：Releases 0；Issues 更新 3；PR 更新 0。

## 1. 今日速览
过去 24 小时无新版本、无 PR 更新。社区动态集中在 3 个 Issue：`kimi web` 的 CJK 输入法回车误发送问题、Kimi Work 对 Agent 回复的可视化批注需求，以及已关闭的多 Agent 并发/API 限流疑问。整体看，国际化输入体验、Agent 审阅协作和配额透明度是今日焦点。

## 2. 版本发布
过去 24 小时无新 Release。

## 3. 社区热点 Issues
> 今日数据仅返回 3 条 Issue，无法凑足 10 条；以下为全部更新内容，按关注价值排列。

### 1. #2643 [OPEN] [kimi web] Enter pressed during IME composition is treated as 'send message'
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2643
- 作者：@wangjin1982 | 创建/更新：2026-09-14 | 评论：0 | 👍：0
- 重要性：这是影响中文、日文、韩文用户的输入法兼容性 bug。在 `kimi web` 输入框组词时按回车，本意是确认拼音/字母上屏，却被误判为发送消息，容易导致未完成内容被直接发出。
- 社区反应：目前暂无评论和点赞，但属于高影响本地化交互问题，建议优先修复。

### 2. #2642 [OPEN] 功能需求：Kimi Work 会话内支持对 Agent 回复的可视化批注与审阅反馈
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2642
- 作者：@Zhywleo | 创建/更新：2026-09-14 | 评论：0 | 👍：0
- 重要性：社区希望 Kimi Work 支持对 Agent 的任意回复，尤其是计划、报告、方案类长回复，进行逐段可视化批注，并将批注结果以结构化形式返回给 Agent 用于修订，而不是只能靠输入框文字描述修改意见。
- 社区反应：暂无评论，但该需求指向 Agent 工作流从“生成”走向“审阅—反馈—修订”的闭环，可能影响 Kimi Work / Kimi Code 的产品交互设计。

### 3. #1383 [CLOSED] [bug] 为什么说的会员权益是支持多 agent 但是我两个小龙虾同时思考就会出现限制
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1383
- 作者：@asecret | 创建：2026-03-10 | 更新：2026-09-14 | 评论：6 | 👍：0
- 重要性：用户反馈 Kimi Code CLI 1.15.0 在 Allegretto 订阅下，通过 openclaw 使用 API 时，两个 Agent 同时持续对话会触发限制，疑似与 API rate limit 或并发配额有关。该问题触及会员权益、多 Agent 支持和实际限流策略的一致性。
- 社区反应：共 6 条评论，已有一定讨论，当前已关闭。

## 4. 重要 PR 进展
过去 24 小时无 PR 更新，暂无可总结的功能或修复内容。

## 5. 功能需求趋势
从今日 Issues 中可提炼出以下方向：

1. **多 Agent 并发与配额透明度**  
   用户关注会员权益与实际并发限制是否一致，尤其是多 Agent 同时运行时的 API rate limit 表现。  
   参考：https://github.com/MoonshotAI/kimi-cli/issues/1383

2. **本地化输入体验与 IME 兼容**  
   `kimi web` 需要正确处理 CJK 输入法组合状态，避免 Enter 键在组词期间被误判为发送。  
   参考：https://github.com/MoonshotAI/kimi-cli/issues/2643

3. **Agent 回复审阅与结构化反馈**  
   社区希望从纯文本反馈升级为逐段可视化批注，并让批注结果结构化回流给 Agent，用于自动修订。  
   参考：https://github.com/MoonshotAI/kimi-cli/issues/2642

4. **Kimi Work / Kimi Code 协作闭环**  
   需求涉及长回复审阅、方案修订和反馈渠道整合，说明用户期待更成熟的 Agent 协作界面。

## 6. 开发者关注点
- **多 Agent 场景下的限流与权益边界**：用户不清楚何时会触发限制，也不清楚订阅权益与 API 限流之间的关系，建议在文档和错误提示中明确。
- **IME 组合输入处理**：Web 输入框需正确监听 `compositionstart` / `compositionend`，避免组词状态下 Enter 误发送。
- **长回复审阅缺少结构化交互**：只能靠输入框文字描述修改意见，效率低且难以对应到具体段落。
- **国际化与可访问性**：中文、日文、韩文用户的基础输入体验应纳入核心回归测试。
- **配额与错误反馈可观测性**：当多 Agent 并发触发限制时，应给出清晰原因、当前配额和建议操作。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 · 2026-09-15

数据来源：[github.com/anomalyco/opencode](https://github.com/anomalyco/opencode)

---

## 1. 今日速览

今日发布 **v1.18.31**，重点修复 ACP 会话在加载、恢复与 fork 时的 model/effort/mode/reasoning 边界丢失问题，并在启动阶段暴露远程配置认证错误。社区侧，**V2 新布局的反弹持续发酵**，多个请求恢复旧版侧边栏/经典布局的 Issue 集中涌现；同时 `SystemPrompt.environment` 崩溃回归、DeepSeek V4.1 Flash 与 Muse Spark 等模型/网关异常，成为影响日常使用的高优先级问题。

---

## 2. 版本发布

### v1.18.31

**Core · Bugfix**
- 修复会话加载、resume 与 fork 时丢失的 ACP 会话 model、effort、mode 及 reasoning chunk 边界信息（@JacobNWolf）。这对依赖长会话续跑与分支实验的用户尤为关键。

**TUI · Bugfix**
- 启动时展示远程配置认证错误，并以失败状态码退出，避免静默失败导致的误判。

**Extensions · Improvements**
- 官方发布说明中该段落被截断（原文仅 "### Improvemen"），建议关注后续完整 changelog。

链接：https://github.com/anomalyco/opencode/releases

---

## 3. 社区热点 Issues

1. **[#13984](https://github.com/anomalyco/opencode/issues/13984) 无法复制粘贴（59 评论 / 32 👍，OPEN）**
   CLI 中提示 "copied to clipboard"，但 `Ctrl+V` 无内容。这是评论数最高的长期未决问题，跨平台剪贴板集成缺陷持续消耗用户信任，社区反复催促修复。

2. **[#17318](https://github.com/anomalyco/opencode/issues/17318) SSE read timed out（48 评论 / 37 👍，CLOSED）**
   文件写入或 brainstorming/planning 技能链式调用时出现 SSE 超时。今日关闭，说明根因已定位或由新版本缓解，是长任务稳定性讨论的代表案例。

3. **[#48741](https://github.com/anomalyco/opencode/issues/48741) Muse Spark 图片/工具调用触发 Zen 关键错误（26 评论）**
   报错 `reasoning encrypted_content was not issued to this caller`，涉及 Zen 网关上的推理内容回传逻辑。对应修复 PR #48908 已在推进，属于高优先级 provider 兼容问题。

4. **[#48882](https://github.com/anomalyco/opencode/issues/48882) 请求恢复带常驻左侧栏的旧版 UI（14 评论 / 20 👍，OPEN）**
   直指 #20242 的侧边栏改版取消经典双栏布局。这是本轮 UI 争议中支持度最高的诉求之一，反映新布局对既有工作流的破坏。

5. **[#5391](https://github.com/anomalyco/opencode/issues/5391) 每个 provider 支持多套认证配置（13 评论 / 41 👍，OPEN）**
   从 2025 年 12 月延续至今的高票功能请求，用户需要在同一 provider 下切换不同账号/密钥（工作与个人、多租户场景），呼声稳定但迟迟未落地。

6. **[#26602](https://github.com/anomalyco/opencode/issues/26602) Desktop 对慢速本地 provider 固定 5 分钟 Headers Timeout（13 评论，OPEN）**
   即使配置 `"timeout": false` 仍被 abort。与 #49044（客户端 SDK 硬编码 300s undici headers timeout）同源，暴露超时参数未贯通到调用链的问题。

7. **[#49041](https://github.com/anomalyco/opencode/issues/49041) DeepSeek V4.1 Flash 不可用（9 评论，OPEN）**
   模型无响应、界面无限转圈，而 DeepSeek V4 Pro 正常，问题在一小时内集中出现。典型的 provider 侧抖动，但缺少降级提示与快速切换体验。

8. **[#48372](https://github.com/anomalyco/opencode/issues/48372) / [#48803](https://github.com/anomalyco/opencode/issues/48803) `SystemPrompt.environment` 崩溃回归（各 5 评论，19 👍 / 5 👍）**
   v1.18.30 起每次 prompt 都以 `TypeError: undefined is not an object (evaluating 'a.name')` 失败，v1.18.20 正常。已通过 A/B 对比确认是版本回归，影响面为"全量请求不可用"，严重度极高。

9. **[#31137](https://github.com/anomalyco/opencode/issues/31137) Web UI 新布局下 "Auto-accept permissions" 按钮被禁用（9 评论 / 9 👍，OPEN）**
   经典布局正常、新

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 · 2026-09-15

> 数据来源：[github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)

---

## 今日速览

TUI 稳定性成为今日社区最集中的焦点：多个 P1 级 Issue 同时指向 Ink `useBoxMetrics` 布局监听器引发的 React #185 崩溃，已有对应修复 PR 提交。与此同时，daemon/ACP 权限模型暴露出一组安全与隔离问题（跨会话权限阻塞、审批模式被忽略），社区讨论热度明显上升。平台侧，Windows 扩展 EPERM、Web Terminal PTY 缺失、VSCode Remote-SSH 等跨环境兼容缺陷集中爆发。

---

## 版本发布

**v0.23.4（正式版）**
- 发布说明较为简略，Highlights 指向完整变更列表。
- **Breaking Change**：移除 channels 中可配置的 message-prefix 过滤。符合条件的消息不再需要前缀，直接遵循常规的 sender / group / mention / pairing 策略。（[#11571](https://github.com/QwenLM/qwen-code/pull/11571)）
- 链接：https://github.com/QwenLM/qwen-code/releases

**v0.23.4-nightly.20260914.f024b37689**
- 夜间构建，包含 Windows inode 门控测试记录与非跳过处理等改动。（[PR #11853](https://github.com/QwenLM/qwen-code/pull/11853)）

**cua-driver-rs v0.20.7 / v0.20.8**
- Qwen CUA Driver 预编译二进制发布（vendored 于 `packages/cua-driver`）。
- macOS：已签名 + 公证的 universal binary + `QwenCuaDriver.app`
- Linux：未签名（x86_64 + arm64，glibc 2.31 下限）
- Windows：未签名 UIAccess worker + 原生 SDK payload（x86_64 + arm64）

---

## 社区热点 Issues

1. **[#11500](https://github.com/QwenLM/qwen-code/issues/11500) [OPEN][P1] 多个后台 agent 完成时 TUI 静默退出（React #185）** · 13 条评论
   多个后台子 agent 密集完成时，Ink 的 `useBoxMetrics` 布局监听器触发 `setState` 无限循环，进程无任何错误提示直接退回 shell，恢复会话还会提示"上次会话异常"。这是当前评论数最高的 Issue，直接命中交互式 TUI 的核心可用性。

2. **[#11590](https://github.com/QwenLM/qwen-code/issues/11590) [CLOSED][P1] 非 Qwen 厂商模型不兼容——自动插入 metadata 导致 400** · 8 条评论
   DashScope OpenAI 兼容端点作为聚合网关时，Qwen Code 在请求

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*