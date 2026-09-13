# AI CLI 工具社区动态日报 2026-09-13

> 生成时间: 2026-09-13 00:03 UTC | 覆盖工具: 7 个

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
**数据源**：github.com/anthropics/skills | **截止**：2026-09-13

> ⚠️ **数据说明**：本批 PR 数据的评论数全部为 `undefined`，无法直接按评论排序。因此以下 PR 排名改用复合信号：**关联 Issue 讨论热度 + 更新时效性 + 影响面**。Issues 部分评论数完整，可直接排序。

---

## 1. 热门 Skills 排行（Top 8 PR）

| # | PR / Skill | 功能 | 社区讨论热点 | 状态 |
|---|---|---|---|---|
| 1 | [#1298](https://github.com/anthropics/skills/pull/1298) skill-creator 评估修复 | 修复 `run_eval.py` 恒返回 0% recall；将 eval artifact 装为真 skill；修 Windows 流读取/触发检测/并行 worker | 直指社区最热技术 Issue [#556](https://github.com/anthropics/skills/issues/556)（12 评论 / 7 👍，10+ 独立复现）——"描述优化循环正在对噪声做优化" | OPEN（09-12 更新，最新活跃） |
| 2 | [#514](https://github.com/anthropics/skills/pull/514) document-typography | 生成文档的排版质控：孤词换行、寡行标题、编号错位 | 覆盖**所有** Claude 生成文档，但用户从不主动要求 → 属"默认质量"型需求 | OPEN（自 2026-03 停滞） |
| 3 | [#83](https://github.com/anthropics/skills/pull/83) skill-quality / skill-security-analyzer | 元技能：五维质量评估 + 安全分析，上架 marketplace | 同时呼应两大议题——安全信任（#492）与 skill 质量规范（#202） | OPEN（2025-11 创建，最长寿 PR 之一） |
| 4 | [#1742](https://github.com/anthropics/skills/pull/1742) mcp-builder 兼容修复 | 适配 `mcp>=2.0.0`：`streamablehttp_client` → `streamable_http_client`，headers 改走 `create_mcp_http_client` | Fixes #1668，新生态破坏性变更 | OPEN（09-08 新建） |
| 5 | [#1367](https://github.com/anthropics/skills/pull/1367) self-audit | 交付前审计：机械文件验证 + 四维推理质量门（v1.3.0） | 与 Issue [#1385](https://github.com/anthropics/skills/issues/1385) 推理质量门管线提案同源 | OPEN |
| 6 | [#1628](https://github.com/anthropics/skills/pull/1628) Hivemind | 零成本多智能体编排：Claude Code 只做规划/审查/合并，机械活下放 headless opencode 免费模型 | "稀缺资源不是智能而是贵模型的上下文" | OPEN |
| 7 | [#1615](https://github.com/anthropics/skills/pull/1615) scnet-hpc | SCNet 超算集群运维：profile SSH + Slurm 作业生成、分区/内存/加速器指引 | 垂直领域（HPC）深度集成 | OPEN |
| 8 | [#1602](https://github.com/anthropics/skills/pull/1602) 稳定性合集 | 修复 evaluation 序列化、benchmark 指标、编码、脚本稳定性 | 对应 Issue [#1390](https://github.com/anthropics/skills/issues/1390)（evaluation.py 对所有真实 MCP server 伪造报错、评分 0/N） | OPEN |

**其他值得关注**：`#1607` 标记四个退役模型 ID（时效维护）、`#1734` docx 孤立批注检测（09-06 新建）、`#1724` 评测默认模型升级至 claude-sonnet-5、`#486` ODT 格式支持、`#210` frontend-design 可执行性改写。

---

## 2. 社区需求趋势（Issues 提炼）

**① 安全与信任边界（最高热度）**
- [#492](https://github.com/anthropics/skills/issues/492)（**43 评论**）社区 skill 冒用 `anthropic/` 命名空间，构成信任边界滥用——本批数据中讨论量绝对第一
- [#1175](https://github.com/anthropics/skills/issues/1175) 在 SKILL.md 内硬编码 SharePoint 访问控制的风险
- 映射到 PR：`#83` skill-security-analyzer

**② 工具链可靠性与跨平台（数量最多）**
- [#556](https://github.com/anthropics/skills/issues/556)（12 评论 / 7 👍）`run_eval.py` 触发率恒 0%
- [#1390](https://github.com/anthropics/skills/issues/1390) mcp-builder 评测静默伪造错误
- [#1487](https://github.com/anthropics/skills/issues/1487) claude-api 单次工具调用注入 ~156k token，直接打爆上下文
- [#1362](https://github.com/anthropics/skills/issues/1362) web-artifacts-builder 在 pnpm ≥10.1 构建失败
- [#62](https://github.com/anthropics/skills/issues/62)（10 评论）用户自建 skill 集体消失
- 对应 PR 簇：`#1298` / `#1099` / `#1050`（Windows 兼容）、`#538` / `#541` / `#539`

**③ 分发与协作机制**
- [#228](https://github.com/anthropics/skills/issues/228)（16 评论 / **8 👍，点赞最高**）组织内 skill 共享：目前只能下载 .skill 文件走 Slack 手动上传
- [#189](https://github.com/anthropics/skills/issues/189)（**9 👍**）document-skills 与 example-skills 内容重复，污染上下文窗口
- [#16](https://github.com/anthropics/skills/issues/16) 把 Skills 暴露为 MCP，标准化调用接口

**④ 元技能与质量治理**
- [#202](https://github.com/anthropics/skills/issues/202)（CLOSED）skill-creator 写作风格像开发者文档而非操作性 skill，token 效率低
- [#1385](https://github.com/anthropics/skills/issues/1385) 三段式推理质量门管线

**⑤ 文档格式与领域扩展**
- 格式：ODT/ODS、typography、docx 批注 → `#486` / `#514` / `#1734`
- 记忆压缩：[#1329](https://github.com/anthropics/skills/issues/1329) compact-memory（符号化 agent 状态）
- 平台：[#29](https://github.com/anthropics/skills/issues/29) AWS Bedrock 支持

---

## 3. 高潜力待合并 Skills

按落地概率排序：

1. **`#1298` skill-creator 评估链路修复** — 更新日期最新（09-12），锚定最高复现量 Issue #556，是解锁整个 description 优化闭环的前置条件。⚠️ **冲突风险**：`#1099`、`#1050` 修复同一 Windows 子进程缺陷，维护者需择优或合并。
2. **`#1742` mcp-builder mcp>=2 适配** — 破坏性依赖变更，不改则 mcp-builder 在新版本下整体不可用，属高优先级低争议修复。
3. **`#1724` 评测默认模型升级** — 单点改动、零风险，仅是 claude-3-7-sonnet 快照的时效更正。
4. **`#1602` 稳定性合集** — 一个 PR 打包多类缺陷（序列化/指标/编码），覆盖 #1390 等活跃 Issue。
5. **`#1367` self-audit** — 与 #1385 提案、#202 对 skill-creator 的批评方向一致，若质量治理成为主线则可顺势落地。
6. **`#514` document-typography** — 需求普适性强，但自 3 月起无更新，可能因维护者优先级而搁置。
7. **`#83` 双元技能（质量/安全分析器）** — 与评论量最高的 #492 安全议题高度契合，是最"政治正确"的候选，但已挂起 10 个月，落地取决于维护者对 marketplace 准入的态度。
8. **垂直集成三件套** `#1615`（HPC）/ `#1628`（多智能体）/ `#1627`（Buffer API）— 质量参差、审查成本高，属长尾候选。

---

## 4. Skills 生态洞察

> **社区当前最集中的诉求，不是"再造更多 Skill"，而是把现有 Skill 变成可信赖的基础设施——评估链路必须真实有效（#556/#1298/#1390）、命名空间必须可信（#492，43 评论居首）、工具链必须跨平台可复现（Windows/pnpm/Bedrock）、Skill 必须能在组织内分发（#228），否则再多的 Skill 也只是堆积在不可

---

# Claude Code 社区动态日报 · 2026-09-13

数据来源：github.com/anthropics/claude-code

---

## 一、今日速览

1. **v2.1.270 紧急补丁发布**，修复 2.1.269 引入的只读 git 命令误触发权限申请的回归问题。
2. **Windows 桌面端致命崩溃 Issue（#80444）以 111 条评论继续霸榜**，成为当前社区最严重的未解决问题；会话连续性与 Cowork/云端会话的 GitHub 集成失败紧随其后。
3. 过去 24 小时共 50 条 Issue 更新，但**大量长期 Issue 被标记 `stale` 集中关闭**，成本/限额类问题与数据丢失类问题仍在持续发酵。

---

## 二、版本发布

### v2.1.270

- **修复**：会话运行一段时间后，Bash 中的只读 git 命令（如 `git status`、`git log`）会意外弹出权限申请。该问题为 2.1.269 引入的回归。
- 链接：https://github.com/anthropics/claude-code/releases

> 评价：这是一次典型的"回归修复型"小版本，说明官方在快速收敛 2.1.269 的副作用，但频繁的权限/交互回归也在消耗用户信任。

---

## 三、社区热点 Issues（10 条）

### 1. [#80444](https://github.com/anthropics/claude-code/issues/80444) — Windows 桌面端 GPU 进程致命崩溃（111 评论 / 👍17）
**OPEN** · `area:desktop` · `Windows`
内嵌 Browser 标签页触发 GPU 进程崩溃（0x060C201E），导致 MSIX 包彻底无法启动（`appxState=2`），必须走系统"修复"流程才能恢复。已在两块 NVIDIA 驱动版本上复现。**评论数远超其他 Issue，是当前社区情绪最集中的爆发点**——崩溃直接让应用不可用，且恢复路径对普通用户不友好。

### 2. [#11455](https://github.com/anthropics/claude-code/issues/11455) — 会话交接 / 连续性支持（31 评论 / 👍25）
**OPEN** · `enhancement`
自 2025-11 提出的长期功能需求，要求 CLI 支持跨会话的上下文交接。**点赞数全榜最高**，说明这是被压抑最久的核心诉求：开发者不愿意每次重新交代项目背景。长期未落地也是社区反复顶帖的原因。

### 3. [#84581](https://github.com/anthropics/claude-code/issues/84581) — Cowork 云会话无法访问任何 GitHub 仓库（8 评论 / 👍5）
**OPEN**
git 代理指示 Agent 调用一个**根本不存在的 `add_repo` 工具**，导致云端会话完全无法拉取仓库。这是一个"提示词/工具定义与服务端实现不一致"的典型问题，影响 Cowork 云会话的可用性。

### 4. [#93894](https://github.com/anthropics/claude-code/issues/93894) — Fable 5.1 高强度 code-review 一次耗尽整月会话预算（2 评论）
**OPEN** · `area:cost` · `area:skills`
$100/月档位下，单次高 effort 的代码审查就会打满会话预算且任务未完成。作者直接对比 OpenAI 同档位的限制策略。**成本模型透明度正在成为订阅用户的头号抱怨**。

### 5. [#88731](https://github.com/anthropics/claude-code/issues/88731) — `claude remote-control` 启动的会话缺失 Artifact 工具（2 评论 / 👍2）
**OPEN** · `area:tools` · `area:agent-sdk`
同一台机器、同一账号下，`claude --remote-control` 正常而 server 模式启动的会话没有 Artifact 工具。这是**远程控制/服务端模式下工具集不一致**的问题，对自动化与 CI 场景影响明显。

### 6. [#91805](https://github.com/anthropics/claude-code/issues/91805) — 已安装 GitHub App 但仓库选择器为空（3 评论）
**OPEN** · `area:claude-code-web` · `area:integrations`
Claude Code Web 的仓库选择器无法列出任何仓库。与 #84581、#86828 构成同一主题簇：**云端/Web 侧的 GitHub 接入链路存在系统性缺陷**。

### 7. [#82624](https://github.com/anthropics/claude-code/issues/82624) — Web 版 git stop hook 双重误判，且给出的修复建议会导致死循环（4 评论）
**OPEN** · `area:hooks`
仓库状态本已正确却拦截 Agent 回合，更严重的是它建议的 `amend` 补救方案会**改写历史且永远无法收敛**（因为又会触发新的判定）。这是一个"错误建议比错误本身更危险"的案例。

### 8. [#93124](https://github.com/anthropics/claude-code/issues/93124) — WSL 下 Claude in Chrome 完全不可用（1 评论）
**OPEN** · `platform:wsl` · `area:browser-extension`
Windows + WSL2 场景中，桌面端会强制把 Agent 拉进 WSL 运行，而 CLI 检测到 WSL 后又直接禁用浏览器工具，形成**无法绕过的死锁**。相关需求 [#79655](https://github.com/anthropics/claude-code/issues/79655)（WSLg 原生 Chrome 支持）同样在等待。

### 9. [#93910](https://github.com/anthropics/claude-code/issues/93910) — Cowork：Progress 面板中未完成任务应跨会话持久化（2 评论）
**OPEN** · `area:cowork`
用户希望任务列表不随会话关闭而丢失。与 #11455 同属"**状态持久化**"诉求，反映多会话/长任务工作流正在成为主流用法。

### 10. [#79427](https://github.com/anthropics/claude-code/issues/79427) — 共享 daemon 将 `ANTHROPIC_AUTH_TOKEN` 泄漏至后续所有会话（已关闭）
**CLOSED** · `area:auth` · `area:security` · `high-priority`
首个启动共享 `claude daemon` 的会话所携带的认证环境变量，会被机器上**之后所有 daemon 会话静默继承**，造成错误的账号认证与计费。虽已关闭，但属于安全/计费级别的严重问题，值得回查版本修复情况。

> **其他值得留意的已关闭项**：#86280（macOS 更新后 Cowork 项目全丢，且 `cleanupPeriodDays=30` 默认值静默删除会话记录——**默认值导致数据丢失**）、#86857（工作区信任对话框不弹出，静默禁用 statusLine 等受信功能）、#85348 / #85352 / #85369（三起 `cyber` 安全过滤器误杀，均以 `stale` 关闭）。

---

## 四、重要 PR 进展

> 过去 24 小时仅有 **3 条 PR 更新**，其中 2 条来自同一位贡献者 @poteat，集中在下游 mods 生态，**没有来自官方的核心功能 PR**。

1. [#93452](https://github.com/anthropics/claude-code/pull/93452) **CLOSED** — `mods/diff`：让 mod 的 `/diff` 面板与内置 diff 面板视觉对齐。包含 hunk 渲染走引擎 code 元素、关闭按钮、行距与空状态位置、窄终端换行处理，并限制仓库探测并发为 1。降低了 mod 与内置 UI 的割裂感。
2. [#93912](https://github.com/anthropics/claude-code/pull/93912) **CLOSED** — `mods`：为 diff、sec-default、telemetry 补齐单元测试，并针对插件声明做类型检查。测试在 mod 实际运行环境中执行（注入引擎的 `$` 与 hooks 模块的 `on`，可按需注册 `mock.clock`/`mock.store`/`mock.env`），由 `claude plugin test <dir>` 驱动。**这是插件/mod 生态工具链走向可测试化的重要一步。**
3. [#61716](https://github.com/anthropics/claude-code/pull/61716) **OPEN**（自 2026-05-23 起长期挂起）— 文档补充：上下文溢出被误报为"用量限额"的排查说明。指出 `/compact` 以 "Extra usage required for 1M context" 失败后，错误被映射到了错误的提示文案上。关联 #50321。

---

## 五、功能需求趋势

从本期 Issue 集合可提炼出以下社区关注方向：

| 方向 | 代表 Issue | 说明 |
|---|---|---|
| **会话连续性 / 状态持久化** | #11455、#93910、#86280 | 跨会话交接、任务面板持久化、上下文不丢失，是点赞最高、跨度最长的需求簇 |
| **成本与配额透明度** | #93894、#77469、#74165、#87007、#84750 | 限额提示与实际恢复时间不符、token 异常消耗、订阅档位性价比争议 |
| **云端 / Web / Cowork 的集成可靠性** | #84581、#91805、#86828 | GitHub App、仓库选择器、git 代理工具名不一致，云端链路问题集中爆发 |
| **平台与运行时覆盖（Windows / WSL）** | #80444、#93124、#79655、#78189 | 桌面端稳定性、WSL 下浏览器工具不可用、Windows 控制台窗口闪烁 |
| **多 Agent / 后台会话 UX（Agent View / FleetView）** | #82192、#83996、#83013、#80119 | 后台任务被误杀、误标完成、`/exit` 行为异常、pin 排序诉求 |
| **安全与信任边界** | #79427、#86857 | daemon 环境变量泄漏、信任对话框失效导致功能静默降级 |
| **MCP / 工具链一致性** | #74329、#88731、#71711 | MCP 重连后工具被错误注销、不同启动模式下工具集不一致 |

---

## 六、开发者关注点

1. **交互回归正在消耗信任。** 今日的 v2.1.270 又是在修上一版引入的权限提示回归（只读 git 命令被误要求授权）。类似 #86857（信任对话框不弹）、#83996（光标在行首按左键就切屏并杀死后台 Agent）都属于"小交互引发大破坏"，建议官方加强 TUI/权限链路的回归测试覆盖。

2. **限额提示不可信，直接影响工作安排。** 多条 Issue（#77469、#74165、#87007）反映"提示 5:40pm 重置，实际 2:00pm 就恢复"，导致用户白等数小时。这类文案错误比功能缺失更伤用户，因为它直接误导排期。

3. **默认配置造成静默数据丢失。** #86280 指出 `cleanupPeriodDays=30` 默认值会删除会话记录，叠加 macOS 重启后 Cowork 项目目录被重建为空。开发者希望**破坏性默认值应显式提示或提供恢复手段**。

4. **Stale 机器人式关闭引发不满。** 本期大量 Issue（含三起安全过滤器误杀、statusline 回归、工作区信任失效）以 `stale` 关闭而非"已修复"关闭，社区担心问题被"清理"而非"解决"。建议公开 stale 策略与复现入口。

5. **多会话 / 多 Agent 已成为默认工作方式。** 后台任务、远程控制、FleetView、Cowork 四套并行会话机制并存，但彼此的**工具集、状态、退出语义互不一致**（#88731、#82192、#86864），是当前最需要统一抽象的地方。

6. **云会话的 GitHub 接入是重灾区。** #84581（不存在的 `add_repo` 工具）、#91805（仓库列表为空）、#86828（网络策略被覆盖）指向同一链路的多个断点，对把 Claude Code 用于团队协作的开发者影响最大。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报

**日期：2026-09-13** ｜ 数据来源：github.com/openai/codex

---

## 一、今日速览

1. **无新版本发布**，社区讨论全面转向配额计量异常与桌面端稳定性问题，跨报告跟踪帖 #41220 已累积 40 条评论，成为当前最大焦点。
2. **Windows / iPad 桌面端体验问题集中爆发**，涉及远程会话冻结、沙箱安装失败、应用启动失败、任务中断等多个层面。
3. **PR 侧以体验打磨为主**：TUI 流式渲染、Recap 逻辑、命令中心用量展示等由 `copyberry[bot]` 批量提交，同时出现多账号 Profile 切换、连接器缓存重构等基础设施级改动。

---

## 二、版本发布

过去 24 小时内无新 Release。

---

## 三、社区热点 Issues（精选 10 条）

### 1. #41220 配额异常消耗与计量不一致【跨报告跟踪帖】
- 作者 @FromAriel ｜ 评论 40 ｜ 👍 14 ｜ 2026-08-27 创建，持续更新
- https://github.com/openai/codex/issues/41220
- **为什么重要**：这是官方仓库内少见的"元级"跟踪帖，把大量"订阅配额/购买额度消耗速度远超基线"的分散报告收敛为同一症状族，并指出用量在会话中途突然变化。40 条评论与 14 个赞说明问题覆盖面广、持续时间长。
- **社区反应**：讨论已从个别用户抱怨上升为系统性计量可信度问题，是本轮权限/计费类争议的核心节点。

### 2. #34349 请求彻底关闭 Pets 功能
- 作者 @lazyanubis ｜ 评论 11 ｜ 👍 **48（今日最高）** ｜ 2026-07-20 创建
- https://github.com/openai/codex/issues/34349
- **为什么重要**：用户要求不仅能关闭 Pets，还要从侧边栏彻底移除 "Show Pet" 入口。48 个赞是本批数据中最高，反映出相当一部分开发者对应用中"非生产力功能"占用 UI 空间的容忍度很低。
- **社区反应**：典型的"功能可选化"诉求，与专业工具定位的期待直接相关。

### 3. #45073 5 小时配额在 26 分钟内被消耗约 86%
- 作者 @brolabitalia ｜ 评论 3 ｜ 2026-09-12 创建（当日新报）
- https://github.com/openai/codex/issues/45073
- **为什么重要**：仅 2 次 prompt 就消耗近 86% 的 5 小时窗口，环境为 Windows + codex-cli 0.154.0 + gpt-5.6-sol medium fast。作为 #41220 之外新增的具体复现案例，数据点非常尖锐。
- **社区反应**：新开报告，正处于等待官方回应的早期阶段。

### 4. #45132 app-server 客户端无法使用 Luna Reserve
- 作者 @liuxing7954 ｜ 评论 2 ｜ 2026-09-12
- https://github.com/openai/codex/issues/45132
- **为什么重要**：`supportsLunaReserve` 能力位已存在，但协议层缺少 accept/redeem 动作，属于典型的"能力暴露不完整"导致的集成阻塞，直接影响第三方 app-server 客户端。
- **社区反应**：与 #41220 的额度议题形成呼应，指向配额体系在协议层的不一致。

### 5. #41695 iPad 应用访问远程 Codex 会话时频繁冻结
- 作者 @jpagan ｜ 评论 8 ｜ 2026-08-30 创建
- https://github.com/openai/codex/issues/41695
- **为什么重要**：iPad App 1.2026.230 + Pro 20x 订阅 + iPadOS 27 Beta 5，属于高付费用户的核心移动场景受阻。评论数在移动端问题中最高。
- **社区反应**：与 #36946（macOS 无法启用 Remote Control）共同构成"远程能力不可用"的问题簇。

### 6. #36946 macOS 端 Remote Control 无法启用
- 作者 @ziqinickhan ｜ 评论 6 ｜ 👍 8 ｜ 2026-08-04 创建
- https://github.com/openai/codex/issues/36946
- https://github.com/openai/codex/issues/36946
- **为什么重要**：Plus 用户在 macOS 上无法开启远程控制，且长期未解决（已开放一个多月）。8 个赞表明影响面不止个例。
- **社区反应**：与 iPad 冻结问题合并看，跨设备远程工作流是当前体验短板。

### 7. #43938 Codex 工具 IPC 解码失败（企业版 / Linux）
- 作者 @lucas-armadin ｜ 评论 6 ｜ 2026-09-08 创建
- https://github.com/openai/codex/issues/43938
- **为什么重要**：每次工具调用都以 `failed to decode code-mode ...` 失败，等于工具链在 enterprise + Linux 环境下完全不可用，是阻断级缺陷。
- **社区反应**：与同期 #44379（缺少 `code_mode_host_duration_ns` 字段，已关闭）指向同一工具调用序列化层，疑似版本回归。

### 8. #44444 codex-cli 0.154.0：选中 Astra 时光标在输入行内跳动
- 作者 @janthmueller ｜ 评论 6 ｜ 👍 5 ｜ 2026-09-10 创建
- https://github.com/openai/codex/issues/44444
- **为什么重要**：TUI 交互细节直接影响日常输入效率；且与今日 PR #45137（移除 Astra 闪烁动画）形成同一主题的两面——Astra 的终端呈现正在成为摩擦点。
- **社区反应**：5 个赞在 CLI 类问题中属较高，说明可复现性较好。

### 9. #45126 `codex resume <session-name>` 在会话跨多页时必然失败
- 作者 @DRanger666 ｜ 评论 2 ｜ 2026-09-12
- https://github.com/openai/codex/issues/45126
- **为什么重要**：分页查询逻辑缺陷导致按名称恢复会话不可用，属于"数据都在但取不回来"的典型工程 bug，随着会话数量增长影响会放大。
- **社区反应**：新报，属可精确定位的高价值缺陷报告。

### 10. #42025 会话历史消失：durable-rollout 投影拒绝 `token_count` 事件
- 作者 @lost-pass-key ｜ 评论 3 ｜ 2026-09-01 创建
- https://github.com/openai/codex/issues/42025
- **为什么重要**：Pro 用户的会话历史因投影层拒绝 `token_count` 事件而丢失，属于不可逆的数据问题；同时暴露 rollout 投影的容错策略过严。
- **社区反应**：与 #39471（Windows 线程归档全部失败）共同反映本地会话存储层脆弱。

**其他值得快速关注**：#45134（Windows 应用 26.908.4834.0 无法定位 CLI 组件启动失败）、#45095（Astra 推理质量明显下降）、#45117（`~/package.json` 为空导致 Linux GUI 启动崩溃）、#44169（Windows Edge 标签页发现失败）。

---

## 四、重要 PR 进展（精选 10 条）

> 注：本批 PR 状态多数标记为 `CLOSED`，其中包含已合并的改动。

### 1. #45137 移除 TUI 输入框中的 Astra 闪烁动画
- 作者 @copyberry[bot] ｜ https://github.com/openai/codex/pull/45137
- 移除选中 Astra 时的动画星形效果，以及相关的输入、终端焦点、模型选择挂钩，保留草稿文本与实时语音快照的测试覆盖。
- **意义**：直接回应 TUI 中 Astra 相关视觉干扰（参见 issue #44444）。

### 2. #45135 在换行到达前预览流式散文内容
- 作者 @copyberry[bot] ｜ https://github.com/openai/codex/pull/45135
- 修复"未终止的长单行响应在流式过程中不可见"的问题，为 agent 消息与建议计划提供实时预览。
- **意义**：直接影响长输出的可感知延迟体验。

### 3. #45124 为异步用户消息引入特性开关
- 作者 @copyberry[bot] ｜ https://github.com/openai/codex/pull/45124
- 新增默认关闭的 `send_message_to_user_async` 开关，使根 agent 在模型目录未支持时也能使用该工具，子 agent 保持不可用。
- **意义**：为多 agent / 主动消息能力铺路，采用渐进式放开策略。

### 4. #45094 基于内容而非序列化信封估算历史 token
- 作者 @copyberry[bot] ｜ https://github.com/openai/codex/pull/45094
- 原逻辑把消息 ID、metadata、JSON 转义都计入估算，导致 token 数虚高；改为按 content 逐项估算。
- **意义**：与配额争议直接相关——估算精度影响用户对"用量是否异常"的判断。

### 5. #45090 Recap 中保留会话上下文并分离下一步动作
- 作者 @copyberry[bot] ｜ https://github.com/openai/codex/pull/45090
- 原 recap prompt 限制在 900 字节，难以容纳已完成进度、未决事项与近期修正；本次放宽并区分"已完成"与"待处理"。
- **意义**：长会话上下文管理的核心改进。

### 6. #45089 延后自动 Recap 并压缩其 TUI 布局
- 作者 @copyberry[bot] ｜ https://github.com/openai/codex/pull/45089
- 自动 recap 延迟从 3 分钟提高到 30 分钟，标题与分隔线改为斜体 `↳ Recap:` 布局，保留换行与 Unicode，并处理 URL 折行。
- **意义**：减少高频打扰，同时降低终端刷屏。

### 7. #45108 手动重命名后取消待执行的线程标题生成
- 作者 @copyberry[bot] ｜ https://github.com/openai/codex/pull/45108
- 修复手动命名后标题生成请求仍在后台运行、进度指示仍可见的问题。
- **意义**：消除状态不一致带来的困惑。

### 8. #25383 [2/2] app-server 账号会话生命周期（多账号 Profile 切换）
- 作者 @dhruvgupta-oai ｜ https://github.com/openai/codex/pull/25383
- 新增 `accountSession/login/start`、`add`、`list`、`switch`、`logout` 路由，为桌面端多账号切换提供 Rust 侧实现。
- **意义**：企业/多身份用户的关键基础设施，跨越数月终于落地。

### 9. #31471 将 Apps 缓存逻辑抽取为 ConnectorRuntimeManager
- 作者 @mzeng-openai ｜ https://github.com/openai/codex/pull/31471
- 把 Codex Apps 工具缓存封装

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-09-13** ｜ 数据来源：github.com/google-gemini/gemini-cli

---

## 一、今日速览

1. **新 nightly 版本发布**：`v0.61.0-nightly.20260912.g9c1b0a610` 重点修补了两类安全风险——通过构建文件修改与不可信 flags 触发的**间接提示注入**，以及沙箱文件系统边界的加固。
2. **Agent 稳定性仍是社区最大痛点**：评论数最高的 Issue 集中在子代理（subagent）行为异常——MAX_TURNS 中断被误报为 `GOAL success`、通用 Agent 无限挂起、浏览器子代理在 Wayland 下失败。
3. **PR 侧出现一批安全与配置一致性修复**：MCP 策略运行时强制、shell wrapper 剥离、checkpoint 校验、显式模型选择不被覆写等，显示维护者正系统性收敛"策略与实现不一致"类缺陷。

---

## 二、版本发布

### v0.61.0-nightly.20260912.g9c1b0a610

- **fix(core)**：防止通过构建文件修改与不可信 flags 造成的间接提示注入（PR #29250）
- **fix(sandbox)**：加固文件系统边界，隔离运行时状态，将宿主目录挂载替换为净化后的配置文件（PR #29214）

> 本次发布延续了近期"安全优先"的路线，两条改动都直接对应外部输入可能被模型当作指令执行的攻击面。
> 链接：https://github.com/google-gemini/gemini-cli/releases

---

## 三、社区热点 Issues（按关注度筛选 10 条）

### 1. 子代理 MAX_TURNS 中断被报告为 GOAL 成功 ⭐️最重要
**#22323** ｜ P1 ｜ 13 条评论 ｜ 👍 2 ｜ 已挂起近 6 个月
`codebase_investigator` 子代理在触达最大轮次、尚未完成任何分析的情况下，仍返回 `status: "success"` 与 `Termination Reason: "GOAL"`。这是典型的**静默失败**，会让调用方误判任务已完成，直接污染上层编排逻辑。
链接：https://github.com/google-gemini/gemini-cli/issues/22323

### 2. 通用 Agent 无限挂起（社区点赞最高）
**#21409** ｜ P1 ｜ 8 条评论 ｜ 👍 8
只要 Gemini CLI 把任务转交给 generalist agent，就会永久卡住，连"创建文件夹"这类简单操作也不例外，最长等待 1 小时。用户绕过方式是显式禁止调用子代理——这从侧面说明子代理调度链路存在结构性问题。
链接：https://github.com/google-gemini/gemini-cli/issues/21409

### 3. 零依赖 OS 沙箱 + 执行后意图路由
**#19873** ｜ P2 ｜ 9 条评论 ｜ 👍 1
提议充分利用 Gemini 3 模型"原生 bash 用户"的偏好（链式使用 `grep`/`cat`/`sed`/`awk`），在**不牺牲安全与 UX**的前提下提供零依赖操作系统级沙箱，并配合执行后意图路由。这是对模型能力取向与安全边界之间张力的系统性回应。
链接：https://github.com/google-gemini/gemini-cli/issues/19873

### 4. AST 感知的文件读取、搜索与代码库映射
**#22745** ｜ P2 ｜ 7 条评论
EPIC 类跟踪议题，评估 AST 感知能力能否：① 单次工具调用精准读取方法边界，减少错位读取与 token 噪声；② 支持结构化导航。这是当前**上下文效率优化**方向的关键探索。
链接：https://github.com/google-gemini/gemini-cli/issues/22745

### 5. Gemini 不主动使用 skills 与子代理
**#21968** ｜ P2 ｜ 6 条评论
用户反馈：即便配置了描述清晰的 `gradle`、`git` 技能，模型在明显相关场景下也几乎不会自行调用，必须显式指令。这削弱了 skills/subagent 体系的实际价值。
链接：https://github.com/google-gemini/gemini-cli/issues/21968

### 6. ACP 会话文件使用 agent 生成的 sessionId，session/load 失败
**#29288** ｜ P1 ｜ 4 条评论 ｜ 新近提交（09-11）
在 Zed 1.19.2+ 作为 ACP 客户端时，客户端与 agent 为同一会话生成不同 sessionId，导致 `session/load` 报 "Invalid session identifier"，会话永远无法恢复。影响 IDE 集成体验。
链接：https://github.com/google-gemini/gemini-cli/issues/29288

### 7. Shell 命令执行完成后仍卡在 "Waiting input"
**#25166** ｜ P1 ｜ 4 条评论 ｜ 👍 3
简单 CLI 命令明明已执行完毕，界面却持续显示命令活跃并等待用户输入，阻塞后续流程。属于高频且影响日常使用的核心缺陷。
链接：https://github.com/google-gemini/gemini-cli/issues/25166

### 8. 浏览器子代理在 Wayland 下失败
**#21983** ｜ P1 ｜ 4 条评论 ｜ 👍 1
Wayland 环境下 browser subagent 直接失败并输出 `Termination Reason: GOAL`，与 #22323 同属"终止原因语义失真"的问题簇。
链接：https://github.com/google-gemini/gemini-cli/issues/21983

### 9. Auto Memory 需要确定性脱敏并减少日志
**#26525** ｜ P2 ｜ 5 条评论
Auto Memory 会读取本地 transcript 并发送给后台提取代理，而**脱敏发生在内容已进入模型上下文之后**；此外服务还会记录既有 skill 内容。属于数据泄漏风险面。
链接：https://github.com/google-gemini/gemini-cli/issues/26525

### 10. 工具数超过 128 个时触发 400 错误
**#24246** ｜ P2 ｜ 3 条评论
工具数量过多时模型请求直接返回 400。随着 MCP 生态扩张，工具规模管理（作用域裁剪、按需加载）将越来越关键。
链接：https://github.com/google-gemini/gemini-cli/issues/24246

---

## 四、重要 PR 进展（10 条）

| PR | 状态 | 内容 |
|---|---|---|
| **#29214** | CLOSED | **fix(sandbox)**：加固沙箱文件系统边界，隔离运行时状态，用净化配置文件替代宿主目录挂载，路径敏感检查统一走 realpath。已进入本次 nightly。 |
| **#29292** | OPEN | **fix(checkpoint)**：`loadCheckpoint()` 现在校验 `history` 必须为数组，修复 `{"history": null}` 之类损坏文件导致的 `/resume` 崩溃（Fixes #29194）。 |
| **#29294** | OPEN | **fix(cli)**：解决后台命令执行期间快速输入引发的终端闪烁与撕裂，根因是 ink reconciler 周期内 stdout 争用与光标焦点问题。 |
| **#29287** | CLOSED | **feat(policy)**：把 `--yolo` 原生映射为通配策略 `allowedTools: ["*"]`，移除 `ApprovalMode.YOLO` 这一独立状态，统一审批模型。 |
| **#29208** | OPEN | **fix(core)**：`agents.json` 结构损坏（null/标量/数组）时回退为空，避免 `isAcknowledged`/`acknowledge` 抛 TypeError 或静默丢弃确认（Fixes #29207）。 |
| **#29205** | OPEN | **fix(cli)**：MCP prompt 响应文本直接提交，不再做 JSON 编码，保留服务器返回的引号与换行原貌。 |
| **#29200** | OPEN | **fix(core)**：MCP 策略在运行时一致执行——服务名匹配改为大小写不敏感 + 去空白；显式空 `mcp.allowed` 列表

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-09-13）

数据窗口：过去 24 小时  
数据来源：github.com/MoonshotAI/kimi-cli

## 1. 今日速览

过去 24 小时无新 Release、无 PR 更新，社区动态集中在 Issue 侧：共 3 条 Issue 更新。唯一仍为 OPEN 的是 Web UI 队列面板新增 Steer（⚡）按钮的功能请求，获得 2 个赞和 1 条评论；另两条旧 bug 被关闭，但均无公开评论，关闭原因不明确。

## 2. 版本发布

无。过去 24 小时无新 Release。

## 3. 社区热点 Issues

说明：过去 24 小时仅 3 条 Issue 更新，无法按要求列出 10 条。以下为全部条目，按关注度排序。

### 3.1 #2370 [OPEN][enhancement] Feature Request: Add Steer (⚡) button to Web UI queue panel

- 作者：@2986787982dsx-ui
- 创建：2026-05-26；更新：2026-09-12
- 状态：OPEN；评论：1；👍：2
- 为什么重要：在 `kimi web`（Windows PowerShell）中，当 AI 正在运行时按 Enter 发送后续消息，消息只会进入队列，缺少立即“引导/打断”模型的快捷操作。新增 Steer 按钮可提升 Web UI 的实时交互控制力。
- 社区反应：本时段唯一获得正向反馈的功能请求，2 个赞说明队列控制是实际痛点。
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2370

### 3.2 #1409 [CLOSED][bug] kimi cli web mode keeps refreshing and connects different port

- 作者：@LSTM-Kirigaya
- 创建：2026-03-11；更新：2026-09-12
- 状态：CLOSED；评论：0；👍：0
- 为什么重要：报告在 v1.20.0、Darwin arm64 上使用 `/web` 时，网页反复刷新并连接不同端口，影响 Web 模式可用性和开发流。
- 社区反应：无评论、无点赞；已关闭，但数据中未体现关闭原因。
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1409

### 3.3 #1404 [CLOSED][bug] Reckless behaviour

- 作者：@acorello
- 创建：2026-03-11；更新：2026-09-12
- 状态：CLOSED；评论：0；👍：0
- 为什么重要：用户使用 v1.19.0、kimi.ai、kimi-for-coding 时，要求 Kimi 制定并展示计划，但遇到“不谨慎行为”。这关系到 Agent 自主执行边界、计划确认和权限护栏。
- 社区反应：无评论、无点赞；已关闭，具体解决或关闭原因未公开。
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1404

## 4. 重要 PR 进展

过去 24 小时无 PR 更新，共 0 条，无法列出 10 条。

## 5. 功能需求趋势

从本批 Issue 可提炼出以下方向：

- **Web UI 交互精细化**：用户希望在 AI 运行过程中对队列消息进行“Steer/引导”，而不是只能排队等待。
- **Web 模式稳定性与连接可靠性**：端口漂移、页面反复刷新是影响 `/web` 使用体验的典型问题。
- **Agent 行为安全与计划确认**：围绕模型“计划—执行”过程的谨慎性、确认机制和权限控制存在关注。
- **跨平台体验一致性**：Windows PowerShell 与 macOS Darwin arm64 均有反馈，说明 Web/CLI 体验需覆盖多平台。

## 6. 开发者关注点

- **队列消息缺少即时控制**：AI 运行时 Enter 仅入队，期望有 Steer 按钮快速引导或打断。
- **`/web` 模式连接不稳定**：刷新和端口变化会打断工作流，开发者需要更可靠的 Web 会话管理。
- **模型自主行为需更可控**：计划任务中的 “Reckless” 反馈指向对确认、护栏和可回滚性的需求。
- **关闭 Issue 缺少解释**：两条 CLOSED Issue 均无评论，社区难以判断是修复、重复还是过期关闭；建议维护者补充关闭原因或关联版本/PR。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 · 2026-09-13

> 数据来源：github.com/anomalyco/opencode ｜ 统计窗口：过去 24 小时（截至 2026-09-12 的更新）

---

## 一、今日速览

过去 24 小时**无新版本发布**，社区讨论几乎被"剪贴板复制粘贴失效"这一条主线占据——相关 Issue 已累计 **200+ 条评论**，是当前项目最高热度话题。与此同时，**opencode2（V2）** 的稳定性与性能问题密集浮现：当天新开/更新的 PR 覆盖了 session 错误透出、slash 技能参数丢失、Desktop sidecar 崩溃重启、事件写入放大等多个方向。整体看，社区诉求正从"能跑起来"转向**跨终端/IDE 环境的可靠性**与**错误可见性**。

---

## 二、版本发布

无新版本发布（过去 24 小时内）。

---

## 三、社区热点 Issues（TOP 10）

### 1. #4283 Copy To Clipboard is not working —— 131 评论 / 👍123
[链接](https://github.com/anomalyco/opencode/issues/4283)
从 2025-11 持续至今的"元老级"问题：选中响应文本后无法复制到系统剪贴板。它是全仓**评论数与点赞数双第一**的 Issue，说明这并非边缘场景，而是直接影响日常使用的核心体验。社区情绪已从"报 bug"转向"为什么一年了还没修"。

### 2. #13984 can not copy and paste in opencode CLI —— 57 评论 / 👍32
[链接](https://github.com/anomalyco/opencode/issues/13984)
CLI 中右上角提示"copied to clipboard"，但 Ctrl+V 粘贴无内容。核心痛点是**UI 反馈与实际行为不一致**——这种"假成功"比直接报错更消耗用户信任。

### 3. #41470 "Copied to clipboard" doesn't work（VS Code Server / Docker） —— 22 评论
[链接](https://github.com/anomalyco/opencode/issues/41470)
在 Docker 化的 VS Code Server 环境中复现，v1.18.14。指向**远程/容器环境下剪贴板桥接缺失**，与 #26459 属于同一根因家族。

### 4. #26459 Clipboard copy fails in web-based VSCode terminals —— 14 评论
[链接](https://github.com/anomalyco/opencode/issues/26459)
覆盖 code-server、GitHub Codespaces、VS Code Remote SSH、Gitpod 等场景。该 Issue 的价值在于**把问题从"某个终端有问题"抽象为"Web 化终端环境普遍不支持"**，为后续统一修复提供了范围界定。

### 5. #26602 Desktop 5-minute Headers Timeout Error with slow local providers —— 12 评论
[链接](https://github.com/anomalyco/opencode/issues/26602)
Desktop 端在 5 分钟后强制中断本地 OpenAI 兼容 provider 请求，即使配置 `"timeout": false` 或设置更大超时值也无效。配置项被静默忽略，对使用本地大模型的用户是**硬性阻塞**。

### 6. #36761 [bug, core, 2.0] V2 subagent 工具未向模型暴露合法 subagent ID —— 7 评论
[链接](https://github.com/anomalyco/opencode/issues/36761)
V2 的 `subagent` 工具既不下发已配置的 ID，也不提供发现（discovery）操作，导致模型只能"猜"ID，委托调用在执行期失败。这是 **V2 架构层面的工具契约缺陷**，作者为 @kitlangton，关注度较高。

### 7. #47258 SSE 事件流在标签页后台化后不恢复 —— 3 评论
[链接](https://github.com/anomalyco/opencode/issues/47258)
`server-sdk.tsx` 中 `pagehide` 无条件调用 `stop()`，但 `pageshow` 仅在 `event.persisted === true` 时重启，需手动刷新页面。属于**小而具体的状态机 bug**，定位清晰、易修复。

### 8. #48715 Desktop sidecar 反复崩溃（0xC0000409）+ 图片数错误卡死会话 —— 1 评论
[链接](https://github.com/anomalyco/opencode/issues/48715)
Windows 11 / 48GB 内存环境下，服务端 sidecar 因内存压力反复崩溃；同时"Too many images in request"错误会让 session 永久不可用。作者附带了 3 个 debug bundle，**证据充分、可复现性强**。

### 9. #48675 `opencode run` 零 chunk 流式停滞：无超时、无重试、无退出 —— 1 评论
[链接](https://github.com/anomalyco/opencode/issues/48675)
三个并行 headless worker 在 17 秒内相继挂死，日志最后一行停留在 stream open。对 **CI/自动化场景**是致命的：进程既不退出也不报错。

### 10. #39628 [FEATURE] 从手机/第二设备远程批准权限请求 —— 4 评论
[链接](https://github.com/anomalyco/opencode/issues/39628)
长会话频繁阻塞在权限提示（文件编辑、bash、MCP 调用）上。这是本轮 Issue 中**最具产品化想象力的需求**，指向"agent 长时间无人值守运行"这一核心使用场景。

> 另注：**#31087（SSE 事件流无界内存增长）已关闭**，长会话导致 worker 内存膨胀至无响应的问题有了结论，可视为今日少数正面信号。[链接](https://github.com/anomalyco/opencode/issues/31087)

---

## 四、重要 PR 进展（TOP 10）

### 1. #48734 fix(server): surface session creation errors
[链接](https://github.com/anomalyco/opencode/pull/48734)
V2 session 创建时数据库写入失败只返回空 500，TUI 又用通用错误覆盖了客户端信息。本 PR 让错误真正透出，直接对应 #39775。

### 2. #48733 fix(tui): preserve slash skill arguments
[链接](https://github.com/anomalyco/opencode/pull/48733)
修复通过 slash 自动补全调用 skill 时，**技能名后的尾随文本被丢弃**的问题（Closes #48720）。修复方式是把尾随文本作为普通用户 prompt 提交并附带 skill。

### 3. #48732 fix(tui): finalize streamed markdown responses
[链接](https://github.com/anomalyco/opencode/pull/48732)
助手消息结束后 OpenTUI 的 Markdown 渲染器仍停留在 streaming 模式，导致渲染异常。属于典型的"流式收尾"缺陷。

### 4. #48730 fix(core): keep locations with running terminals out of eviction
[链接](https://github.com/anomalyco/opencode/pull/48730)
`LocationActivity` 在最后一个持久化 session 事件 60 分钟后驱逐 location；但终端不产生 session 事件，导致**有活跃终端的 location 被误驱逐**。长会话用户值得关注。

### 5. #48729 fix(session): keep todo list current for non-Claude models
[链接](https://github.com/anomalyco/opencode/pull/48729)
非 Anthropic 提示词路径下的模型从未收到更新 todo 的指令，导致任务完成后条目仍停留在 `in_progress`。已在 Qwen3 + OpenAI 兼容 provider 上复现。这是**跨模型一致性**的重要修复。

### 6. #48716 fix(desktop): respawn crashed sidecar; classify image-count errors as overflow
[链接](https://github.com/anomalyco/opencode/pull/48716)
针对 #48715 的双重修复：sidecar 崩溃后自动重启；把图片数超限归类为 overflow 而非"毒化"整个会话。

### 7. #48638 fix(core): eliminate durable event write amplification from turn diffs
[链接](https://github.com/anomalyco/opencode/pull/48638)
`SessionSummary.summarize` 把整轮 git patch 文本挂到 user 消息的 `summary.diffs` 上并被 fork，造成持久化事件的**写入放大**。属于性能与存储层面的深度修复。

### 8. #48724 fix(desktop): migrate mac beta to stable installer
[链接](https://github.com/anomalyco/opencode/pull/48724)
让 macOS Beta 用户转向当前签名的 Stable DMG，而不是让 Squirrel.Mac 去替换一个 bundle identifier 不同的应用；同时统一了外部安装器在更新状态、原生弹窗、设置、崩溃恢复与标题栏中的呈现。

### 9. #43298 fix(app): keep prompt submit visible on narrow displays
[链接](https://github.com/anomalyco/opencode/pull/43298)
窄视口下 prompt 控件会溢出并遮挡提交按钮，导致点击被误接收。移动端/小窗口用户的实用修复，自 8-18 挂起至今仍在推进。

### 10. #46165 fix(app): keep archived sessions open in their tabs
[链接](https://github.com/anomalyco/opencode/pull/46165)
当前"归档"实际充当了导航命令，会把会话从标签页中踢出。本 PR 让归档只写 `time.archived`，不改变导航状态（Closes #35058）。

> 另有几个值得留意的动向：**#48712**（TUI 通过 kitty graphics 渲染 LaTeX 数学块，已关闭）、**#48731**（TUI i18n）、**#47783**（波斯语 README 翻译）、**#48722/#48726**（生态页新增 lintlang 插件与 BYOT 项目）。

---

## 五、功能需求趋势

从本次 50 条 Issue + 50 条 PR 的分布看，社区关注方向集中在以下五条：

| 方向 | 典型信号 | 说明 |
|---|---|---|
| **剪贴板 / 复制粘贴** | #4283、#13984、#41470、#26459、#35258、#39588、#44056、#47165、#44740 | 本次数据中占比最高的一类，横跨 TUI、VS Code 扩展、Desktop、Windows/macOS/Linux 与 Web 终端 |
| **IDE / 远程环境集成** | #41470、#26459、#39588、#32985 | VS Code Server、Codespaces、code-server、Remote SSH、GNU Screen、tmux 等非标准终端环境适配 |
| **V2（opencode2）迁移与打磨** | #36761、#48636、#43845、#48720、#48718 | subagent ID 暴露、Ctrl+C 丢弃草稿、每项目目录重复拉起 MCP 进程、slash 参数丢失、`-s` 无 ID 时打开选择器 |
| **性能与资源占用** | #31087（已关）、#48638、#42150、#43845 | SSE 内存增长、持久化写入放大、文本增量累积 O(N²) → O(N)、MCP 进程数爆炸 |
| **模型与 Provider 兼容** | #48728、#48687、#48721、#48729 | NVIDIA API key 认证失败、DeepSeek 4.1 Flash 配额计算错误、多段式 model key（含 `/`）报错不透明、非 Claude 模型 todo 不更新 |

值得额外注意的两个"小而明确"的需求：
- **#48661** Desktop 双击 Review/Context 标签最大化面板（JetBrains 风格），60 天自动关闭后被重新创建，说明**确有持续需求**。
- **#39628** 移动端/第二设备远程批准权限请求。

---

## 六、开发者关注点

综合 Issue 与 PR 的措辞，开发者反馈中最集中的痛点可归纳为四类：

**1. 静默失败与"假成功"——当前最大的信任消耗点**
剪贴板提示"已复制"但实际为空（#4283/#13984/#41470）；subagent 流错误被包装成 `<task_result></task_result>` 的"成功空结果"（#38866）；session 创建失败返回空 500（#48734）；

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-09-13）

数据来源：github.com/QwenLM/qwen-code

## 1. 今日速览

- v0.23.3 nightly 发布，主要移除 DingTalk 过时后台响应聚合及 channels 相关能力（breaking change）。
- 社区最热问题是 TUI 在多个后台

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*