# AI CLI 工具社区动态日报 2026-09-12

> 生成时间: 2026-09-12 00:22 UTC | 覆盖工具: 7 个

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

数据截止：2026-09-12  
说明：PR 评论数在给定数据中显示为 `undefined`，因此 PR 排行依据原列表“按评论数排序”的先后，并结合关联 Issue 评论数与更新时间判断热度。以下 PR 状态均为 **OPEN**。

## 1. 热门 Skills 排行（PR）

1. **#1298 fix(skill-creator): run_eval.py always reports 0% recall**  
   功能：修复 `run_eval.py` 始终报告 0% recall 的核心评测 bug，并修复 Windows 流读取、触发检测、并行 worker。  
   热点：直连 Issue #556，10+ 独立复现；描述优化循环正在“优化噪声”，属于 Skill 质量基建问题。  
   状态：OPEN  
   链接：https://github.com/anthropics/skills/pull/1298

2. **

---

# Claude Code 社区动态日报 · 2026-09-12

> 数据来源：github.com/anthropics/claude-code

---

## 一、今日速览

过去 24 小时社区焦点集中在**网络/沙箱与桌面端稳定性**：Cowork 与 Desktop 出现多条"出口网络全断、代理 403、VM 不挂载文件夹"的回归报告，其中 #93507 明确指出回归始于 2026-09-10 23:15 UTC。同时，一条 4 月就提交的 Windows 桌面重启失败问题（#42776）评论数已飙至 178、获 88 赞，成为仓库内讨论热度最高的长期未决 Issue。版本侧，v2.1.269 带来了插件评测工具 `claude plugin eval` 与输出风格切换 `/output-style`，是今日唯一实质性功能增量。

---

## 二、版本发布

### v2.1.269

- **`claude plugin eval`**：可对插件运行其自带 eval 套件，针对 Claude Code 产出**可评分、可复现**的结果，并输出 JSON + HTML 报告（`claude plugin eval --help`）。
- **`/output-style [name]`**：列出并切换输出风格，支持通过 Remote Control 操作，以及在 cloud 等环境中使用。

**意义**：`plugin eval` 把插件质量从"能跑"推进到"可度量"，对插件生态的工程化是重要一步；`/output-style` 则延续了近期对 UI/交互可配置性的投入。

---

## 三、社区热点 Issues（精选 10 条）

### 1. [#42776](https://github.com/anthropics/claude-code/issues/42776) — Windows Desktop 重启失败（孤儿进程文件锁）· 178 评论 / 88 👍
状态 OPEN，带 `invalid` 标签，创建于 2026-04-02，至今仍在更新。**仓库内评论数最高的 Issue**：应用退出后残留孤儿进程持有文件锁，导致 Relaunch 失败。标记为 `invalid` 却持续获得大量讨论与点赞，说明用户对官方判定存在明显分歧，也反映桌面端生命周期管理的长期顽疾。

### 2. [#11897](https://github.com/anthropics/claude-code/issues/11897) — Web 端 .NET SDK 二进制下载被代理拦截 · 21 评论 / 25 👍
即使用户已开启 "All domains" 网络访问，代理仍拦截二进制下载。**沙箱 egress 策略与实际放行范围不一致**的典型样本，从 2025-11-18 拖到现在仍未解决，踩坑者持续追加复现。

### 3. [#59736](https://github.com/anthropics/claude-code/issues/59736) — Desktop 第三方 Code 会话重启后从 UI 消失（已关闭）· 15 评论
JSONL 转录文件仍在磁盘，但会话不再出现在界面中。问题已 CLOSED，可作为**会话持久化与 UI 状态解耦**的参考案例。

### 4. [#93507](https://github.com/anthropics/claude-code/issues/93507) — Cowork macOS 沙箱 VM 无网络路由，代理全域名 403 · 9 评论
带 `regression` + `has repro`，明确指出**回归始于 2026-09-10 23:15 UTC**：VM 只起 loopback，云出口代理对每个域名返回 403。这是今天最"新鲜"且影响面最大的回归，与 #93494 同属 Cowork 网络问题簇，建议优先关注。

### 5. [#25947](https://github.com/anthropics/claude-code/issues/25947) — 项目记忆文件应存于项目本地 `.claude/` · 9 评论 / 39 👍
现状是全局路径 `~/.claude/projects/<encoded-path>/memory/MEMORY.md`，用户希望改为 `<project-root>/.claude/memory/MEMORY.md`。**高赞的功能需求**，与 #93743 的路径 slug 冲突问题互相印证：全局存储模型正在暴露规模化后的隔离性缺陷。

### 6. [#93221](https://github.com/anthropics/claude-code/issues/93221) — Windows 连接文件夹从未挂载进 VM · 8 评论
宿主侧报告 Plan9 共享添加成功，guest 侧完全看不到。**静默失败**最伤体验，且与 #93507/#93494 共同指向 VM/沙箱层。

### 7. [#57034](https://github.com/anthropics/claude-code/issues/57034) — 支持 VS Code 浏览器共享 API 以验证 Web UI · 6 评论 / 41 👍
VS Code 新增"与 agent 共享浏览器标签页"能力，作者希望 Claude 也能读取 DOM、截图、console 来验证 Web UI 改动。**点赞/评论比极高**，是 IDE 集成方向最具共识的诉求。

### 8. [#81620](https://github.com/anthropics/claude-code/issues/81620) — `advisor` 工具使 context 用量翻倍，~50% 即触发 auto-compact · 5 评论
`advisor` 转发转录的 prompt 被累加进同一个 `usage` 块，Claude Code 误判为真实上下文占用。直接导致**长会话被提前压缩、有效窗口腰斩**，属高影响的计量类 bug。

### 9. [#93494](https://github.com/anthropics/claude-code/issues/93494) — Cowork macOS 会话中途全部出站网络丢失 · 5 评论 / 4 👍
桌面工作区与云容器**双端同时断网**，文件访问不受影响。与 #93507 组合看，Cowork 网络栈这 48 小时内出现系统性退化。

### 10. [#89992](https://github.com/anthropics/claude-code/issues/89992) — Windows MSIX 自动更新终止运行中的应用 · 5 评论
"Another program is currently using this file"——新包已暂存但无法完成替换，因为运行中的 app 持有文件锁。**更新机制与运行实例互斥**，与 #42776 同源，是 Windows 桌面版的共性架构问题。

**其他值得留意**：#82184（项目规则被当作建议、hooks 自我中和、compaction 丢弃治理）、#93667（IDE 选择指示器从 footer 回退到内联，v2.1.268 行为变更引发反弹）、#93087（Stdio MCP 服务在会话结束时成为孤儿进程）、#93743（非 ASCII 路径被折叠为 `-`，韩文等目录发生存储冲突）、#77310（每小时 PR 自检无成本上限，4 天耗尽额度，已关闭）。

---

## 四、重要 PR 进展

**说明**：过去 24 小时内，该仓库仅有 **1 条** PR 发生更新，无法凑满 10 条。以下为完整清单，不做虚构补充。

### [#42205](https://github.com/anthropics/claude-code/pull/42205) — `fix(hookify): normalize tool matcher parsing`（CLOSED）
- **问题**：形如 `Edit | Write`（分隔符两侧带空格）的 matcher 因未 trim 而匹配失败。
- **改动**：求值前先 trim matcher；对每个 OR 分段做规范化。
- **价值**：修的是 hook 匹配的"空格敏感"隐式陷阱，属小而确定的正确性修复。该 PR 创建于 2026-04-01、于 9-11 关闭，处理周期较长。

---

## 五、功能需求趋势

从今日全部 Issue 标签与内容归纳，社区诉求集中在以下方向：

| 方向 | 代表 Issue | 核心诉求 |
|---|---|---|
| **IDE 深度集成** | #57034、#93667、#86576 | 浏览器共享 API、选择指示器位置可配、Code 标签页可用性 |
| **项目级存储隔离** | #25947、#93743、#93722 | 记忆文件本地化、路径 slug 编码正确性、worktree 跟随配置 |
| **沙箱 / 网络策略** | #93507、#93494、#11897、#93221 | VM 路由、egress 代理一致、文件夹挂载 |
| **上下文与成本治理** | #81620、#77310、#82184 | usage 计量准确、自检循环限流、compaction 不丢治理信息 |
| **权限粒度** | #80846 | Plan mode 只读命令自动批准 |
| **进程/资源生命周期** | #93087、#93679、#42776、#89992 | MCP 孤儿进程、渲染器内存无界、文件锁互斥 |
| **平台一致性** | #92210、#93707、#78146 | Deep link 语义、macOS 本地网络权限、Windows 环境变量膨胀 |

可以看出一条主线：**功能在变强（插件 eval、输出风格、Remote Control），但平台层的可靠性与隔离性正在成为主要瓶颈**。

---

## 六、开发者关注点

1. **长会话的"慢性中毒"**：`CLAUDE_ENV_FILE` 在每次 compact 后继续追加、Bash 前导块无去重无截断（#78146）；Design 渲染器内存增长至 2–4GB 被杀（#93679）。这类问题不阻断首发，但会在数小时后集中爆发。

2. **沙箱承诺与事实不符**：多个 Issue 都出现同一模式——界面显示"已允许/已添加成功"，实际网络或挂载完全不可用（#11897、#93221、#93507）。**静默失败 + 错误成功回执**是最高的信任成本。

3. **Windows 桌面端质量落差**：重启、更新、Code 标签页、VM 挂载，四条独立问题都落在 Windows。加上 #42776 被标 `invalid` 却获 178 条评论，用户与官方在问题定性上的张力值得注意。

4. **计量可信度**：`advisor` 让 usage 翻倍触发 auto-compact（#81620），usage 不一致提示甚至直接阻断工作（#86677，已关闭）。**计量不准 = 用户无法规划额度**。

5. **项目治理规则缺乏强制力**：项目规则被当作建议、hooks 在 compaction 后被中和、auto-memory 优先级高于项目指令（#82184）。对团队协作场景，这是"写了规则但不生效"的根因。

6. **存储模型需要从全局走向项目化**：全局记忆路径（#25947）、非 ASCII 路径 slug 碰撞（#93743）、worktree 不继承 connector 禁用列表（#93722）——三者在不同层面暴露同一件事：`~/.claude/` 的扁平全局模型已跟不上多项目、多 worktree、多语言目录的实践。

---

*日报生成时间：2026-09-12 · 基于 GitHub 公开数据自动汇总*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 · 2026-09-12

数据来源：[github.com/openai/codex](https://github.com/openai/codex)

---

## 一、今日速览

今日 Codex 仓库仍处于高强度迭代期，24 小时内连发 7 个 Rust alpha 版本（0.155.0-alpha.3.x 系列一天内推进 4 个小版本）。社区侧，Windows 桌面端稳定性问题集中爆发——发送按钮卡死（#40968，36 条评论）、会话历史反复丢失、推理强度被重置等多条 Issue 持续发酵；同时 macOS 26.908.31748 出现白屏回归（#44743）。PR 侧则显示 TUI 语音对话正式转正、人格（Personality）选择被全面退役、多账号 Profile 切换能力落地。

---

## 二、版本发布

过去 24 小时共发布 7 个 Rust 通道版本，均为 alpha 预发布，无 changelog：

| 版本 | 说明 |
|---|---|
| [rust-v0.155.0-alpha.3.10](https://github.com/openai/codex/releases) | 0.155.0 分支最新推进 |
| [rust-v0.155.0-alpha.3.9](https://github.com/openai/codex/releases) | |
| [rust-v0.155.0-alpha.3.8](https://github.com/openai/codex/releases) | |
| [rust-v0.155.0-alpha.3.7](https://github.com/openai/codex/releases) | |
| [rust-v0.155.0-alpha.3](https://github.com/openai/codex/releases) | 0.155.0 迭代基线 |
| [rust-v0.155.0-alpha.2.3](https://github.com/openai/codex/releases) | |
| [rust-v0.154.0-alpha.6.2](https://github.com/openai/codex/releases) | 0.154.0 分支补丁 |

**观察**：版本号在小版本内部以「.7/.8/.9/.10」粒度高频推进，反映 CI 驱动的持续交付节奏。值得注意的是，Issue #44743 报告 `0.154.0-alpha.6.1` 对应的桌面端构建出现白屏崩溃，回滚到 26.901.51231（codex-cli 0.153.4）后恢复正常——alpha 通道当前不建议生产使用。

---

## 三、社区热点 Issues

### 1. #40968 Windows 桌面端发送按钮无限转圈，提示词无法提交 ⭐36 评论
[链接](https://github.com/openai/codex/issues/40968) · OPEN · 标签：`bug, windows-os, app, session`

Windows 11（build 26200.0）Pro x5 用户反馈，在 ChatGPT 桌面端中发送后续消息时按钮持续转圈、prompt 永不提交。该 Issue 自 8 月 26 日创建以来累计 36 条评论，是当前社区讨论度最高的问题，且 9 月 11 日仍有更新，说明尚未修复。**这是 Windows 桌面端「无法使用」级别的主干功能阻断。**

### 2. #18693 超大会话历史导致桌面端全局性能崩塌 ⭐20 评论 / 👍9
[链接](https://github.com/openai/codex/issues/18693) · OPEN · 标签：`bug, app, session, performance`

问题远超「线程切换慢」：当 Profile 中存在少量超大本地会话历史时，输入、会话内滚动、线程列表滚动、UI 更新、线程切换全面劣化，甚至随机退出。自 2026-04-20 挂起至今近 5 个月仍在更新，属于**长期未解决的结构性性能债务**，高赞（9）说明影响面广。

### 3. #44743 macOS 26.908.31748 白屏崩溃：renderer 抛 "r is not a function" ⭐8 评论 / 👍4
[链接](https://github.com/openai/codex/issues/44743) · OPEN · 标签：`bug, app`

新版 macOS 应用在线状态下渲染进程因 `authed-route ↔ app-primary` 循环导入直接抛异常，导致白屏；回滚到旧版本即恢复。这是**新版引入的回归缺陷**，且用户已明确定位到循环依赖根因，修复路径清晰。同时 #44720（31 条评论，已关闭）与 #44824（6 条评论）均围绕 “ChatGPT hit a snag” 弹窗异常，建议合并观察。

### 4. #44035 会话历史丢失：read_thread 陈旧、rollout 保留更新消息 ⭐8 评论 / 👍3
[链接](https://github.com/openai/codex/issues/44035) · OPEN · 标签：`bug, windows-os, app, app

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报（2026-09-12）

## 今日速览

昨日 Gemini CLI 发布 `v0.61.0-nightly.20260911.ged2ac40df` 夜间版本。社区侧最显著的变化是**安全与沙箱相关 PR 集中落地**：多个针对文件系统隔离、间接提示注入、路径穿越和 Windows sandbox 的修复同时推进。Issues 侧则以 **Agent/Subagent 可靠性**为主线，`subagent` 状态误报、generalist agent 挂起、browser agent 兼容性等 P1 问题持续占据讨论热度。

---

## 版本发布

**v0.61.0-nightly.20260911.ged2ac40df**

- 由 `gemini-cli-robot` 自动提交的夜间版本提升（对应 PR #29285）。
- Changelog：https://github.com/google-gemini/gemini-cli/compare/v0.61.0-nightly.20260910.ged2ac40df...v0.61.0-nightly.20260911.ged2ac40df

---

## 社区热点 Issues

1. **[#22323] Subagent 达到 MAX_TURNS 却被上报为 GOAL 成功**（P1 / bug / agent，13 评论，👍2）
   `codebase_investigator` 子代理在未完成任何分析、仅因耗尽最大轮次而中断时，仍返回 `status: "success"` 与 `Termination Reason: "GOAL"`。这类"假成功"会掩盖真实中断，对上游自动化流程危害极大，是当前讨论量最高的 Issue。
   https://github.com/google-gemini/gemini-cli/issues/22323

2. **[#21409] Generalist agent 永久挂起**（P1 / bug / agent，8 评论，👍8）
   只要 CLI 委派给 generalist agent，简单操作（如创建文件夹）就会无限挂起，用户最长等待一小时。规避方式是不使用子代理，说明委派链路存在阻塞。点赞数为当前列表最高，用户感知强烈。
   https://github.com/google-gemini/gemini-cli/issues/21409

3. **[#19873] 通过零依赖 OS 沙箱 + 执行后意图路由释放模型的 bash 亲和性**（P2 / enhancement / effort-large，9 评论）
   提出利用 Gemini 3 原生擅长 POSIX 工具链（grep/cat/sed/awk）的特性，在不牺牲安全与 UX 的前提下扩大 bash 使用面。这是 agent 执行能力演进方向的纲领性讨论。
   https://github.com/google-gemini/gemini-cli/issues/19873

4. **[#22745] 评估 AST-aware 文件读取、搜索与代码库映射的影响**（P2 / EPIC，7 评论）
   探索以 AST 感知方式精确读取方法边界、降低误读轮次与 token 噪声。与 #22746 联动，是提升 codebase_investigator 精度的关键方向。
   https://github.com/google-gemini/gemini-cli/issues/22745

5. **[#21968] Gemini 几乎不会主动使用 skills 和 sub-agents**（P2 / bug，6 评论）
   用户反馈即便已配置 gradle、git 等 skill 与子代理，模型也不会在相关场景自动调用，只有显式指令才生效。该问题直接影响可扩展生态的实用价值。
   https://github.com/google-gemini/gemini-cli/issues/21968

6. **[#26525] 为 Auto Memory 增加确定性脱敏并减少日志输出**（P2 / security / bug，5 评论）
   Auto Memory 会把本地会话内容送给后台抽取代理，当前仅在 prompt 层要求模型脱敏，等于敏感内容已进入模型上下文。属于记忆系统的隐私红线问题，与 #26516/#26522/#26523 同属一组。
   https://github.com/google-gemini/gemini-cli/issues/26525

7. **[#25166] Shell 命令执行完毕后仍卡在 "Waiting input"**（P1 / core / bug，4 评论，👍3）
   简单 CLI 命令已结束，界面却仍显示命令活跃并等待用户输入，是高频可复现的交互阻塞问题。
   https://github.com/google-gemini/gemini-cli/issues/25166

8. **[#21983] Browser subagent 在 Wayland 下失败**（P1 / agent/browser，4 评论）
   在 Wayland 环境启动 browser subagent 失败并直接给出 `Termination Reason: GOAL`，与 #22323 一样暴露了终止原因上报不可信的问题，同时反映 Linux 桌面兼容性缺口。
   https://github.com/google-gemini/gemini-cli/issues/21983

9. **[#24246] 工具数量超过 128 个时触发 400 错误**（P2 / bug，3 评论）
   当可用工具规模膨胀时，请求直接被模型端拒绝。这限制了 MCP/自定义工具生态的扩展上限，需要更智能的工具裁剪策略。
   https://github.com/google-gemini/gemini-cli/issues/24246

10. **[#22672] Agent 应停止/劝阻破坏性行为**（P2 / customer-issue，3 评论，👍1）
    在复杂 git 操作、分支管理、数据库维护等场景，模型倾向使用 `git reset`、`--force` 等危险命令而非更安全的替代方案。这与今日多个安全 PR 形成呼应。
    https://github.com/google-gemini/gemini-cli/issues/22672

---

## 重要 PR 进展

1. **[#29282] fix(auth): 登录后立即持久化 OAuth 凭据**（OPEN，P2 / security）
   修复此前仅在 OAuth 客户端刷新 token 时才落盘的问题，避免用户完成浏览器/设备码登录后仍被重复要求登录。
   https://github.com/google-gemini/gemini-cli/pull/29282

2. **[#29283] fix(sandbox): 改进文件系统隔离并隔离运行时状态**（CLOSED）
   收紧 Docker/Podman/runsc/LXC 与 macOS Seatbelt 下的挂载边界，改为只读配置访问 + 临时运行时写入。
   https://github.com/google-gemini/gemini-cli/pull/29283
   （同类前序工作：[#29214]）https://github.com/google-gemini/gemini-cli/pull/29214

3. **[#29250] fix(core): 阻止通过构建文件修改与不可信参数实现的间接提示注入**（CLOSED，size/xl）
   在受限工作区模式下强化工作区边界校验，重构 `shell`、`edit`、`write_file` 等内置执行路径。属于安全面较大的改动。
   https://github.com/google-gemini/gemini-cli/pull/29250

4. **[#29287] feat(policy): 将 --yolo 映射为 allowedTools 通配策略**（CLOSED，size/xl）
   把 `--yolo` 原生映射为 `allowedTools: ["*"]`，移除独立的 `ApprovalMode.YOLO` 状态及其 UI 旁路，统一审批模型，为后续策略化权限管理铺路。
   https://github.com/google-gemini/gemini-cli/pull/29287

5. **[#29184] fix(core): 在 Windows sandbox 中校验 git 参数，阻断静默 `git diff --output`**（OPEN，P1 / security）
   Windows 下所有 `git status|log|diff|show|branch` 都被视为只读且无需确认，导致 `git diff --output=<path>` 可静默截断任意文件。
   https://github.com/google-gemini/gemini-cli/pull/29184

6. **[#29192] fix(checkpoint): 将 legacy raw tag 路径限制在 checkpoints 目录内**（OPEN，P1 / security）
   修复 `/chat delete <tag>` 配合 `../` tag 可删除 checkpoints 目录外文件的路径穿越漏洞。
   https://github.com/google-gemini/gemini-cli/pull/291

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-09-12）

## 1. 今日速览
- Copilot CLI 发布 **v1.0.84-5**，新增 session/memory 导入命令，并改进 Shell 补全生成机制。
- 过去 24 小时 Issues 更新 33 条，Pull Requests 更新 0 条；社区焦点集中在 **MCP 认证与生命周期、权限疲劳、Windows/WSL 稳定性、长期会话可靠性**。
- 社区信号最强的 Issue 是 **#4095 Windows 插件更新被 VS Code 占用句柄阻塞**，获得 21 个 👍，说明插件/IDE 协同工作流痛点突出。

---

## 2. 版本发布

### v1.0.84-5
链接：https://github.com/github/copilot-cli/releases/tag/v1.0.84-5

**Added**
- 新增 session 和 memory import 命令，支持 semantic JSONL interchange format，便于会话与记忆数据导入/交换。

**Improved**
- Shell 补全由 CLI 解析所用的同一套 grammar 生成：`copilot <TAB>` 会同时提供 root flags 和子命令，各子命令只展示自身选项。
- 注：Release note 中 Improved 列表存在截断，`Command` 后续内容在数据中不完整。

---

## 3. 社区热点 Issues（Top 10）

1. **#4095 [OPEN] Windows 插件更新失败：“Access is denied (os error 5)”**
   - 链接：https://github.com/github/copilot-cli/issues/4095
   - 重要性：VS Code 运行时，Copilot 扩展持有已安装插件的 watcher 句柄，导致 `copilot plugin update` 在 Windows 上失败。影响插件生态和 IDE 协同。
   - 社区反应：评论 2，👍 21，是今日点赞最高的 Issue，说明 Windows 插件更新是强痛点。

2. **#4438 [OPEN] `disable-model-invocation: true` 使 skill 不可达，而非仅手动调用**
   - 链接：https://github.com/github/copilot-cli/issues/4438
   - 重要性：项目 skill 在 `skill list` 中可见，但显式调用时报 `Skill not found`，破坏 skill/agent 系统的预期语义。
   - 社区反应：评论 5，👍 7，是今日讨论最活跃的 Issue 之一。

3. **#4699 [OPEN] 长 `--resume` 会话 OOM 崩溃，诊断文件写入用户 cwd**
   - 链接：https://github.com/github/copilot-cli/issues/4699
   - 重要性：长时间恢复会话触发 V8 heap OOM，约 14 小时崩溃 3 次；同时 crash

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-09-12）

数据来源：github.com/MoonshotAI/kimi-cli  
统计窗口：过去24小时（2026-09-11 至 2026-09-12）

## 1. 今日速览

过去24小时，MoonshotAI/kimi-cli 无新 Release、无 PR 更新，社区活跃度较低。最值得关注的是 #2640：Linux/WSL2 下 Kimi CLI 0.42.0 出现随机硬死锁，SIGTERM/SIGQUIT 无法终止，并会拖死 SSH 会话。另有一条长期 Issue #1388（CentOS 7.9 下 MCP 连接失败）被关闭，但无评论说明关闭原因。

## 2. 版本发布

过去24小时无新 Releases。

## 3. 社区热点 Issues

过去24小时仅有 2 条 Issue 更新，无法凑足 10 条；以下为全部更新条目。

### 1）[OPEN] #2640 Linux/WSL2 下 kimi CLI 0.42.0 随机硬死锁
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2640
- 作者：@jinruyan02
- 创建/更新：2026-09-11
- 状态：OPEN
- 平台/版本：Linux/WSL2，Kimi CLI 0.42.0，Kimi Code，模型 kimi-for-coding
- 重要性：高。问题涉及长时间运行后 TUI 偶发卡死、无响应，且 SIGTERM/SIGQUIT 无法终止进程，最终拖死 SSH 会话。这直接影响远程开发与终端工作流的可用性。
- 社区反应：评论 0，点赞 0。暂无维护者或社区成员参与讨论。

### 2）[CLOSED] #1388 CentOS 7.9 下 kimicode terminal 无法使用，MCP 连接失败
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1388
- 作者：@supsmile
- 创建：2026-03-10；更新：2026-09-11
- 状态：CLOSED
- 平台/版本：CentOS 7.9，kimi version 1.17.0，通过 /login 使用，模型 kimi-for-coding
- 重要性：中。问题为 MCP 服务器连接失败导致终端不可用，影响旧版 Linux 发行版与 MCP 集成场景。
- 社区反应：评论 0，点赞 0。Issue 已被关闭，但数据中未说明具体修复方式或关闭原因。

## 4. 重要 PR 进展

过去24小时无 PR 更新，暂无进展可汇总。

## 5. 功能需求趋势

本期没有新功能需求提案，社区反馈集中在基础可用性与兼容性问题上：

- **跨平台稳定性**：Linux/WSL2、CentOS 7.9 等环境均出现阻断性问题。
- **终端/TUI 健壮性**：长时间运行后 TUI 卡死、无响应。
- **进程与信号处理**：SIGTERM/SIGQUIT 无法终止进程，影响自动化与远程会话管理。
- **MCP 集成可靠性**：MCP server 连接失败会直接导致 CLI 不可用。
- **旧系统/旧版本兼容性**：CentOS 7.9 等环境仍被开发者使用，需要兼容或明确支持边界。
- **错误诊断信息**：MCP 连接失败等错误缺少足够上下文，不利于快速定位。

注：本期样本仅 2 条 Issue，趋势判断置信度有限。

## 6. 开发者关注点

- **Linux/WSL2 下的硬死锁最严重**：随机卡死、无法优雅终止、拖死 SSH，属于高优先级稳定性问题。  
  链接：https://github.com/MoonshotAI/kimi-cli/issues/2640
- **信号处理需要加强**：SIGTERM/SIGQUIT 应能可靠终止 CLI，避免必须强制杀进程或重启终端。
- **MCP 连接失败影响可用性**：在 CentOS 7.9 等旧环境中，MCP connect failed 会直接阻断使用。  
  链接：https://github.com/MoonshotAI/kimi-cli/issues/1388
- **旧系统支持边界需明确**：CentOS 7.9、旧版 kimi 等组合是否仍被支持，建议在文档或发布说明中说明。
- **社区互动偏低**：两条 Issue 均为 0 评论、0 点赞，维护者分诊与用户复现信息补充可能不足。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报｜2026-09-12

---

## 一、今日速览

过去 24 小时无新版本发布，社区讨论集中在 **2.0 beta 的稳定性与发布流水线修复**：子代理无限循环、TUI 崩溃、会话错误静默等 bug 持续发酵，同时团队密集提交了一批 2.0 发布相关修复（Docker 产物路径、Windows CLI 签名、Node CLI 排除）。**OpenCode Go 订阅支付/额度问题**依旧是最热议题（#37790，18 条评论），叠加 DeepSeek 提示缓存命中率接近 0 的反馈，计费透明度与成本控制成为社区共同关注点。

---

## 二、版本发布

过去 24 小时内无新 Release。

---

## 三、社区热点 Issues（精选 10 条）

**1. [#37790](https://github.com/anomalyco/opencode/issues/37790) [OPEN] OpenCode Go 订阅付款成功但工作区仍显示"余额不足"（18 评论）**
社区当前热度最高的 Issue。用户通过 Stripe 成功支付 OpenCode Go 订阅后，工作区依然报 `Insufficient balance`，导致付费功能不可用。这是直接影响付费用户转化的严重计费链路问题，持续近两个月仍未关闭。

**2. [#27110](https://github.com/anomalyco/opencode/issues/27110) [OPEN] 希望增加限制并行子代理最大数量的设置（32 👍）**
全时段最高点赞量的功能需求。本地模型受上下文/显存限制，并行子代理会导致 OOM 和任务拖慢。社区呼声极高，反映出对**资源可控性**的强烈诉求。

**3. [#45442](https://github.com/anomalyco/opencode/issues/45442) [OPEN] [2.0] 子代理无限循环：50 分钟内 364 次相同工具调用，无循环保护，token 失控燃烧（8 评论）**
2.0 目前最严重的稳定性/成本问题之一。后台 `general` 子代理对同一 pattern/path 重复发起 364 次 `grep`，持续约 50 分钟，缺乏循环检测与熔断机制，直接烧掉大量 token。与 #27110 共同指向**自主代理的成本安全阀缺失**。

**4. [#48330](https://github.com/anomalyco/opencode/issues/48330) [OPEN] [2.0] Copilot Legacy Plan（按请求计费）被单次 prompt 全部耗尽（6 评论）**
用户 1500 次/月的 Copilot 配额在 opencode2 的一个会话中被全部消耗并触发 429，而 v1 无此问题。这是 2.0 请求合并/重试逻辑导致的**配额计量异常**，对订阅用户影响直接。

**5. [#40993](https://github.com/anomalyco/opencode/issues/40993) [OPEN] [FEATURE] 支持 Agent Plugins 标准（agent-plugins.org）（12 👍）**
跨厂商

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 · 2026-09-12

> 数据来源：[github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)

---

## 一、今日速览

今日社区焦点集中在**平台稳定性与数据安全**两条主线上：Windows 平台的 MCP 连接、PTY 资源泄漏问题持续发酵，同时多条 P1 级 Issue 指向遥测/日志中的敏感内容未脱敏。PR 侧则有一批高质量改动落地中，包括 Linux 内核级沙箱（bwrap）、Playwright 浏览器 SDK、后台 Agent 看门狗超时等，会话生命周期与 worktree 清理相关的工作也在密集推进。

---

## 二、版本发布

**v0.23.3-nightly.20260911.aaa6a32aae**（nightly 构建）

- `refactor(dingtalk)`：移除已废弃的后台响应聚合逻辑（[#11570](https://github.com/QwenLM/qwen-code/pull/11570)）
- `feat(channels)!`：channels 模块出现破坏性变更（Release Notes 中该条目信息被截断，建议关注后续正式版本说明）

> 该版本为 nightly 预发布，建议生产环境等待对应 stable 版本。

---

## 三、社区热点 Issues（精选 10 条）

### 1. [P1] TUI 在多个后台 Agent 完成时静默崩溃 — React #185
[#11500](https://github.com/QwenLM/qwen-code/issues/11500) · OPEN · 6 条评论

多个后台子 Agent 接连完成时，Ink 的 `useBoxMetrics` 布局监听器触发 `setState` 循环，导致未捕获的 React #185（Maximum update depth exceeded），TUI 直接退出到 shell，且无错误渲染、会话恢复报错。这是目前评论数最高的 Issue，影响交互式终端核心体验，需要渲染层修复。

### 2. [P1] Windows web-terminal PTY 泄漏 conhost.exe
[#11352](https://github.com/QwenLM/qwen-code/issues/11352) · OPEN · 6 条评论

Web 终端 PTY 在自然退出时遗留 `conhost.exe --headless` 进程。作者已将范围缩小至 web-terminal 部分（shell 侧已由 [#11497](https://github.com/QwenLM/qwen-code/pull/11497) 通过 `useConptyDll: true` 修复），剩余部分待处理。Windows 进程管理是长期痛点。

### 3. [P1] vscode-ide-companion 0.23.1 在 Remote-SSH 下 webview 卡加载
[#11556](https://github.com/QwenLM/qwen-code/issues/11556) · OPEN · 5 条评论

VSCode 客户端为 linux-x64，Remote-SSH 服务端为 linux-arm64 时，扩展 Webview 永久卡在加载状态。跨架构远程开发是主流工作流，此问题直接阻断 IDE 集成在远程场景下的使用。

### 4. [P2] Windows 上 MCP 未启用也报 -32000 Connection closed
[#9693](https://github.com/QwenLM/qwen-code/issues/9693) · OPEN · 6 条评论

即使 MCP 未激活，Qwen Desktop 在 Windows 启动时仍对 STDIO 传输的 MCP server 报 `McpError: MCP error -32000: Connection closed`，官方 filesystem / sequential-thinking server 均可复现。与已关闭的 [#4218](https://github.com/QwenLM/qwen-code/issues/4218)（UI 显示已连接但模型无工具）属同一类 Windows MCP 问题簇。

### 5. [P1] 依赖 CVE 审计仓库级失败
[#10850](https://github.com/QwenLM/qwen-code/issues/10850) · OPEN · 5 条评论

`Dependency CVE audit` CI 作业自 9 月 2 日起在整个仓库范围失败，`npm audit --omit=dev` 报告 4 个漏洞（1 low / 2 moderate / 1 high，涉及 fast-uri、qs、uuid）。属于供应链安全门禁问题，优先级高。

### 6. [P1] hooks 合约需对齐 Claude Code
[#11610](https://github.com/QwenLM/qwen-code/issues/11610) · OPEN · 3 条评论

qwen-code 的 hooks 引擎在结构上已与 Claude Code 持平，但在若干契约细节上不一致：纯文本 stdout、`stop_hook_active`、超时单位、matcher、通用输入等。对于从 Claude Code 迁移的用户，这是兼容性关键项，且已引发设计层面讨论。

### 7. [P1] 遥测上传未脱敏的原始工具错误文本
[#11198](https://github.com/QwenLM/qwen-code/issues/11198) · OPEN · 3 条评论

默认开启的使用统计通道将原始工具错误文本上传至 RUM 端点，未做任何脱敏，shell 命令行（可能含 URL 凭据、Bearer token）是主要泄漏向量。同一天还有 [#11667](https://github.com/QwenLM/qwen-code/issues/11667)（Responses 调试日志含请求体前缀）与 [#11666](https://github.com/QwenLM/qwen-code/issues/11666)（`logPrompts=false` 失效）两条相关 Issue，形成安全/隐私问题集中区。

### 8. [P2] `logPrompts=false` 依然导出 API 请求内容
[#11666](

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*