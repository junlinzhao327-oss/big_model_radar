# AI CLI 工具社区动态日报 2026-08-18

> 生成时间: 2026-08-17 22:44 UTC | 覆盖工具: 7 个

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
**数据来源**: anthropics/skills 仓库 | **数据截止**: 2026-08-18

---

## 1. 热门 Skills 排行（按社区关注度）

所有 PR 目前均为 open 状态，此处按评论活跃度排序。

### 🥇 #1298 — skill-creator 评估管线修复（关注度最高）
修复 `run_eval.py` 对任何技能描述均报告 `recall=0%` 的系统性故障——根因是评估产物未作为真实 skill 安装，导致整个描述优化循环在噪声上运行（关联 issue #556，被 10+ 用户独立复现）。同时修复了 Windows 管道读取、触发检测及并行 worker 问题。
- **讨论热点**: skill-creator 工具链可靠性；Windows 兼容性；优化循环"优化空气"的严重性
- **状态**: Open
- 🔗 https://github.com/anthropics/skills/pull/1298

### 🥈 #514 — document-typography 文档排版质量检查
新增技能，用于纠正 AI 生成文档中的排版缺陷：孤行文字（1-6 个词溢出到下一行）、孤立段落标题（页底悬空）、编号对齐错乱。直击 Claude 生成文档的普遍痛点。
- **讨论热点**: 印刷级排版标准是否应纳入 Claude Code 默认行为
- **状态**: Open
- 🔗 https://github.com/anthropics/skills/pull/514

### 🥉 #568 — ServiceNow 企业平台技能
覆盖面极广的 ServiceNow 综合技能：ITSM、ITOM、ITAM/SAM、FSM、HRSD、SPM、漏洞响应、安全事件响应、IntegrationHub 等，定位是"平台级助手"而非窄脚本工具。持续迭代至 2026-08-12。
- **讨论热点**: 大型企业平台技能的边界与维护成本；广覆盖 vs 深度
- **状态**: Open（近期仍有更新，落地概率高）
- 🔗 https://github.com/anthropics/skills/pull/568

### #723 — testing-patterns 测试模式技能
覆盖完整测试技术栈：Testing Trophy 模型、单元测试 AAA 模式、React 组件测试（Testing Library）、边界用例、测试命名规范等。
- **讨论热点**: 测试金字塔/奖杯模型的最佳实践标准化
- **状态**: Open
- 🔗 https://github.com/anthropics/skills/pull/723

### #1367 — self-audit 推理质量门禁技能
机械验证 + 四维度推理审计：先验证所有声明输出的文件真实存在，再按损害严重性优先级执行推理质量审计。设计为通用技能，适配任意项目/技术栈/模型。
- **讨论热点**: AI 输出的交付前质量门禁模式；机械验证与推理审计如何分工
- **状态**: Open
- 🔗 https://github.com/anthropics/skills/pull/1367

### #525 — pyxel 复古游戏开发技能
为 pyxel-mcp 新增的技能，触发词涵盖 retro/pixel-art/8-bit 游戏开发，工作流为 write → run_and_capture → inspect → iterate 循环。
- **讨论热点**: MCP server 与 Skills 的组合玩法；游戏开发迭代闭环
- **状态**: Open
- 🔗 https://github.com/anthropics/skills/pull/525

### #83 — skill-quality-analyzer / skill-security-analyzer 元技能
两个"元技能"：质量分析器从结构/文档（20%）、安全性、可维护性等五维度评测 Skills；安全分析器负责权限风险审查。定位是"审查技能的技能"。
- **讨论热点**: 技能质量量化评估框架；社区技能安全审核
- **状态**: Open
- 🔗 https://github.com/anthropics/skills/pull/83

### #486 — ODT 文档技能
支持 OpenDocument 格式（.odt/.ods）的创建、模板填充、读取及转 HTML，触发词覆盖 ODF/LibreOffice/ISO 标准文档。
- **讨论热点**: 开源办公格式支持是否应与 docx 技能平权
- **状态**: Open
- 🔗 https://github.com/anthropics/skills/pull/486

---

## 2. 社区需求趋势（从 Issues 提炼）

### 📌 趋势一：Skill 工具链可靠性是当前最痛点
- **#556**（12 评论, 7👍）`run_eval.py` 在所有查询上 0% 触发率——评估工具基本不可用
- **#202** skill-creator 写得像开发者文档而非可操作技能，教育式语气严重损害 token 效率
- **#1487** `claude-api` 技能单次调用注入 ~156k tokens，直接耗尽上下文窗口
- **#62** 用户自建 12 个技能全部消失且报错——技能持久化稳定性堪忧

### 📌 趋势二：安全与信任边界
- **#492**（43 评论, 2👍，最高评论量）社区技能混入 `anthropic/` 命名空间，冒充官方技能，形成信任边界滥用漏洞——用户可能向非官方技能授予过高权限。这是当前**社区情绪最激烈**的议题。

### 📌 趋势三：组织级协作与共享
- **#228**（16 评论, 8👍）要求在 Claude.ai 内实现组织级技能库，替代"下载 .skill 文件→Slack 传输→手动导入"的原始流程。点赞数全场最高，代表企业用户的迫切需求。

### 📌 趋势四：新技能方向集中在 AI Agent 治理与上下文效率
- **#412** agent-governance：AI Agent 系统的安全治理模式（策略执行、威胁检测、信任评分、审计追踪）
- **#1329** compact-memory：符号化记法压缩长驻代理的状态记忆，降低上下文开销
- **#1385** 推理质量门流水线：任务前校准 → 对抗性审查 → 交付验证
- **#16** 将 Skills 暴露为 MCP 接口，统一 AI 软件 API 协议

### 📌 趋势五：Office/OpenDocument 文档格式稳定性
- **#12** docx 技能在添加注释时引入多余空白导致文档损坏（LibreOffice 也无法打开）
- **#1362** web-artifacts-builder 在 pnpm ≥10.1 下无法构建

---

## 3. 高潜力待合并 Skills

| PR | Skill | 潜力判断 |
|---|---|---|
| [#568](https://github.com/anthropics/skills/pull/568) ServiceNow | 企业级综合技能，持续更新至 8 月，覆盖 10+ 模块，有望成为 enterprise 场景标杆 | ⭐⭐⭐ |
| [#723](https://github.com/anthropics/skills/pull/723) testing-patterns | 测试是开发者刚需，内容体系完整，合并门槛低 | ⭐⭐⭐ |
| [#1367](https://github.com/anthropics/skills/pull/1367) self-audit | 与 #1385 提案呼应，质量门禁是 AI 交付的通用诉求 | ⭐⭐ |
| [#525](https://github.com/anthropics/skills/pull/525) pyxel | 有真实 MCP 生态支撑，游戏开发场景独特且可验证 | ⭐⭐ |
| [#514](https://github.com/anthropics/skills/pull/514) document-typography | 直击 AI 文档排版通病，需求普遍，但需评估与 docx 技能的职责划分 | ⭐⭐ |
| [#83](https://github.com/anthropics/skills/pull/83) quality/security analyzer | 元技能概念领先，但五维度评分框架需社区达成共识后才会被采纳 | ⭐⭐ |

---

## 4. Skills 生态洞察

**一句话总结**: 当前社区最集中的诉求是**"自我诊断与质量保障"**——三分之一的活跃讨论围绕 skill 评估工具失效（#556/#1298/#1099/#1050）、技能名空间安全（#492）、上下文窗口滥用（#1487）等基础设施问题，说明社区已从"能加技能"阶段进入"技能可度量、可信任、可治理"阶段；同时企业级平台技能（ServiceNow、SAP）与 AI Agent 治理技能是下一批最受期待的新方向。

---

# Claude Code 社区动态日报 — 2026-08-18

## 1. 今日速览

- **v2.1.234 发布**：新增 `CLAUDE_CODE_PROJECT_DIR_NAME` 环境变量与 `selection:clear` 键绑定动作。
- **内存崩溃类问题集中爆发**：#87238 和 #87319 分别报告了 11.6GB 与 10.8GB 的 RSS 泄漏并触发 OOM kill，成为今日最受关注的稳定性议题。
- **高票功能需求持续发酵**：#33978（内置用量分析命令）以 👍10 / 20 评论稳居社区呼声榜首。

## 2. 版本发布

### v2.1.234
- **新增 `CLAUDE_CODE_PROJECT_DIR_NAME` 环境变量**：为每个会话分配独立配置目录的宿主环境，可为项目转录目录指定短名称。
- **新增 `selection:clear` 键绑定动作**：支持将按键绑定到清除应用内选区。

🔗 [查看 Release 详情](https://github.com/anthropics/claude-code/releases)

## 3. 社区热点 Issues（10 条）

### 🔥 高热度 / 高影响

**#33978 [OPEN] 内置用量分析命令（claude usage）— 整合 10+ 个未关闭 Issue**
👍 10 | 💬 20 评论
社区长期呼吁的 Token 用量可视化功能，作者整理并关联了十余个同类请求，属于高频需求"众望所归"型 Issue。
🔗 https://github.com/anthropics/claude-code/issues/33978

**#68065 [CLOSED] 后台 Agent 通知路由到错误的 Agent ID（2.1.172+）**
👍 4 | 💬 5 评论 | 已有复现
顺序启动两个后台 agent 时，第二个的完成通知被错误路由到第一个的 task ID，影响多 agent 协作的可观测性，社区点赞较高。
🔗 https://github.com/anthropics/claude-code/issues/68065

### 🐛 内存泄漏 / OOM（今日最突出痛点）

**#87238 [CLOSED] 每次工具调用的辅助进程泄漏至 11.6GB 匿名 RSS 并被 OOM 杀死**
🆕 8月17日提交 | 💬 3 评论
交互使用中，临时辅助进程（comm 显示为 `claude.exe`）约 2 分钟膨胀到 11.6GB，触及容器 12GB cgroup 上限被杀。
🔗 https://github.com/anthropics/claude-code/issues/87238

**#87319 [CLOSED] 后台 Bash 运行器进程在命令完成后持续泄漏内存（v2.1.226 和 v2.1.233）**
🆕 8月17日提交 | 💬 1 评论
Debian 12 / LXC 环境下，后台命令执行完仍 100% CPU 并泄漏至 10.8GB OOM，且两个版本均复现，疑似回归。
🔗 https://github.com/anthropics/claude-code/issues/87319

**#82179 [OPEN] Bash 工具 grep shim 灾难性回溯 — 20KB 文件触发 6.6GB RSS / OOM**
💬 4 评论 | 已复现
`grep` 被替换为 claude 二进制的 ugrep 模拟，`-o` 与有界量词组合时发生灾难性回溯，小文件即可拖垮系统。
🔗 https://github.com/anthropics/claude-code/issues/82179

### 🖥️ 渲染 / UI / IDE 集成

**#87185 [OPEN] 消息首 500 字符内无 Markdown 结构则整条消息以原始 Markdown 渲染**
💬 1 评论 | 已复现
定位到"整条消息偶发显示为原始 Markdown"的根因：Claude Code 仅扫描前 ~500 字符决定是否渲染，首个 Markdown 结构出现更晚时会误判。
🔗 https://github.com/anthropics/claude-code/issues/87185

**#69087 [OPEN] MCP 引导表单在 TUI 全屏模式下被裁剪、不可滚动，操作按钮超出视口**
👍 2 | 💬 3 评论 | macOS
全屏终端中 MCP 表单确认按钮不可见，直接影响使用 MCP 工具的流畅度。
🔗 https://github.com/anthropics/claude-code/issues/69087

**#78461 [OPEN] VSCode 映射网络驱动器工作区 Local 会话列表为空**
💬 2 评论 | Windows 11
`Z:\` 映射到 SMB 共享时，原生 realpath 与写入路径不一致，导致本地会话不显示，终端 `claude --resume` 却正常。
🔗 https://github.com/anthropics/claude-code/issues/78461

### 🧠 模型行为

**#86261 [OPEN] 模型接受显式完成条件，复述后仍提前停止 — 5 个会话重复出现**
👍 1 | 💬 2 评论
作者提供了跨会话的重复证据，说明模型在明确接受结束条件后仍执行不完整，属于指令遵循类的精细报告。
🔗 https://github.com/anthropics/claude-code/issues/86261

### 🔧 其他

**#65710 [CLOSED] Claude Code 提交被错误归属到无关 GitHub 用户**
👍 2 | 💬 4 评论 | Bedrock/macOS
`claude-code@anthropic.com` 的提交关联到了错误的 GitHub 用户，涉及 Git 身份解析问题，社区关注度高。
🔗 https://github.com/anthropics/claude-code/issues/65710

## 4. 重要 PR 进展（10 条）

**#72451 [CLOSED] 从 init-firewall.sh 移除 statsig.anthropic.com**
`statsig.anthropic.com` 已不再解析，导致 devcontainer 启动时防火墙初始化失败。修复移除该失效域名。
🔗 https://github.com/anthropics/claude-code/pull/72451

**#79131 [OPEN] validate-settings.sh 无匹配小写 frontmatter 键时不再中止**
`set -euo pipefail` 下 grep 返回 1 直接退出且无诊断信息，修复后跳过不匹配的键并正常执行。
🔗 https://github.com/anthropics/claude-code/pull/79131

**#87395 [CLOSED] ralph-wiggum 插件：使用 disable-model-invocation 阻止模型自我调用 /ralph-loop**
原 frontmatter 键 `hide-from-slash-command-tool` 不受支持，模型可自行触发循环。改用 `disable-model-invocation` 正确禁用。
🔗 https://github.com/anthropics/claude-code/pull/87395

**#30692 [CLOSED] 新增容器隔离示例（含 guard hook）**
提供 Podman/Docker 容器运行 Claude Code 的完整示例，内置 PreToolUse 钩子拦截强推、硬重置、`rm -rf` 等危险 Git 操作。
🔗 https://github.com/anthropics/claude-code/pull/30692

**#29284 [CLOSED] 文档：明确 excludedCommands 需 `:*` 后缀**
`"docker"` 只匹配裸命令，需 `"docker:*"` 才能匹配带参数的命令。补充示例与 README 说明。
🔗 https://github.com/anthropics/claude-code/pull/29284

**#84004 [CLOSED] 插件开发：限制 frontmatter 解析范围**
原 `sed` 范围表达式会在后续 `---` 处重新开始，导致正文中的分隔线被误解析。改为仅解析开头 YAML 块并校验闭合标记。
🔗 https://github.com/anthropics/claude-code/pull/84004

**#84003 [CLOSED] 脚本：顶层失败正确传播退出码**
原 `.catch(console.error)` 吞掉启动与 API 错误，修复后保留日志并返回失败状态。
🔗 https://github.com/anthropics/claude-code/pull/84003

**#83999 [CLOSED] 脚本：校验 gh 包装器的标志值**
修复 `gh issue list --limit` 这类缺值命令被透传绕过校验的问题，拒绝不完整参数。
🔗 https://github.com/anthropics/claude-code/pull/83999

**#83995 [CLOSED] 脚本：校验 --add-label / --remove-label 选项值**
未传值时 `set -u` 触发内部 `$2: unbound variable`，且可能吞掉后续选项。修复后显式报错。
🔗 https://github.com/anthropics/claude-code/pull/83995

**#83992 [CLOSED] 插件开发：断言 Hook 期望的决策结果**
为 `test-hook.sh` 增加 `--expect allow|deny|ask`，避免"运行了但放行了本应拒绝的操作"这一假阳性。
🔗 https://github.com/anthropics/claude-code/pull/83992

## 5. 功能需求趋势

- **成本与用量可见性**：#33978（内置 `claude usage` 命令）集中表达了社区对 Token 消耗透明化的强烈诉求，关联 10+ 个同类 Issue，是当前第一梯队功能期望。
- **内存稳定与泄漏治理**：多个 OOM 报告（#87238、#87319、#82179）表明社区对内存占用极度敏感，尤其是长时间会话与后台任务场景。
- **子 Agent 可控性**：围绕子 Agent 的 token 浪费（#71423）、通知路由（#68065）与控制能力，社区希望更细粒度的监督与限制手段。
- **IDE 与平台集成成熟度**：VSCode 扩展的多个问题（#63580、#72261、#78461）显示桌面与 IDE 场景是使用重地，集成质量直接影响口碑。
- **Markdown 渲染与 TUI 交互细节**：#87185 的根因定位与 #69087 的表单裁剪，说明社区开始深入打磨终端交互细节。

## 6. 开发者关注点

- **内存泄漏与 OOM kill 是最突出痛点**：连续多起 GB 级内存泄漏（#87238、#87319、#82179）跨 Linux/macOS/Windows 平台出现，且部分在多个版本中复现，开发者期待官方尽快定位修复。
- **模型指令遵循可靠性**：多个 Issue（#86261、#72480、#72486）反映模型"接受条件但执行不到位"或"需要对抗式验证"，开发者对输出可信度有疑虑。
- **Token 消耗与费用失控**：#71423（低效子 Agent 索要退款）与 #67323（自动模式死循环）显示，意外的高额 API 费用会直接损害用户信任。
- **Windows 平台问题集中**：OAuth 证书（#71766）、VSCode 扩展（#63580）、网络驱动器（#78461）等多条 Windows 专属 bug，平台打磨有待加强。
- **后台任务与 Agent 编排可观测性**：任务状态残留（#60095）、通知错路（#68065）等问题影响多 Agent 工作流的信任度与调试效率。

---
*本日报由 GitHub 公开数据自动生成，仅供技术交流参考。*
*数据窗口：2026-08-17 至 2026-08-18*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-18

> 数据来源：github.com/openai/codex | 统计窗口：过去 24 小时

---

## 1. 今日速览

昨日社区共产生 50 条 Issue 更新与 50 条 PR 动态，最热议题集中在 **MCP（Model Context Protocol）进程生命周期管理** 与 **Windows/macOS 桌面端稳定性回归** 两大方向。全新 alpha 版本 `rust-v0.148.0-alpha.21` 已发布；同时一条关于「允许用户关闭 60 秒自动继续问题」的配置建议获得了 **195 个 👍 与 78 条评论**，成为目前社区最受关注的 Issue。此外，官方连续提交了 20+ 个关闭状态的内部 PR，覆盖 TUI 导航加固、Windows 沙箱安全、MCP 策略对齐等底层修复，预示着近期将有一波集中性质量更新。

---

## 2. 版本发布

### rust-v0.148.0-alpha.21
- 版本号：`0.148.0-alpha.21`
- 说明：Rust 版 Codex CLI 的又一 alpha 迭代，目前官方未附带详细变更日志，但从同期 PR 推断，此版本可能已包含部分 TUI 与 MCP 生命周期修复。
- 链接：https://github.com/openai/codex/releases

---

## 3. 社区热点 Issues（10 条）

### 🔥 #28969 — 建议增加「禁用 60 秒自动继续问题」的配置项
- **作者**：@antoyo | 评论 78 | 👍 195
- **概要**：用户希望 Codex CLI 在向用户提问后不再默认 60 秒自动继续，而是允许手动配置等待策略，避免在复杂任务中被自动跳过关键决策点。
- **重要性**：当前评论数与点赞数均为近期最高，直接反映 CLI 交互控制力不足这一普遍痛点。
- 链接：https://github.com/openai/codex/issues/28969

### 🔥 #17265 — 路由式 MCP OAuth Token 不会自动刷新
- **作者**：@infoseekAI | 评论 31 | 👍 57
- **概要**：`~/.codex/.credentials.json` 中虽保存了 `refresh_token`，但 access token 过期后 Codex 不会自动更新，导致 MCP 工具调用持续失败。
- **重要性**：MCP 是 Codex 生态的核心扩展机制，token 过期问题会直接中断所有依赖远程鉴权的工具链。
- 链接：https://github.com/openai/codex/issues/17265

### 🔥 #24990 — ChatGPT 登录流程无法访问 Codex
- **作者**：@D4Vinci-CDM | 评论 26 | 👍 22
- **概要**：已订阅 ChatGPT Plus 的用户无法通过宣传中的 ChatGPT 登录入口使用 Codex CLI；`codex login` 与 `--device-auth` 均被重定向到 `auth.openai.com/add-phone`，疑似账号绑定逻辑缺陷。
- **重要性**：登录是使用产品的第一道门槛，说明 Plus 订阅与 Codex 之间的账号打通仍有兼容性问题。
- 链接：https://github.com/openai/codex/issues/24990

### 🔥 #34268 — Multi-agent V2 全量历史 Fork 导致会话存储暴涨超 100 GiB
- **作者**：@gonzalolarralde | 评论 9 | 👍 6
- **概要**：使用 Ultra 推理 + Multi-agent V2 的长会话在 `$CODEX_HOME/sessions` 下产生了约 110 GiB 的本地数据，存储增长呈乘法级而非线性，疑似历史压缩快照与内联图片被重复复制。
- **重要性**：对重度用户而言是严重的本地磁盘耗尽隐患，同时可能引发桌面端卡顿与崩溃。
- 链接：https://github.com/openai/codex/issues/34268

### 🔥 #37403 — macOS 桌面端更新后无法恢复远程控制/CLI 线程
- **作者**：@xkun1 | 评论 21 | 👍 17
- **概要**：8 月 7 日更新 ChatGPT Desktop 后，「手机远程控制 Mac 上的 Codex CLI 线程」「白天在桌面端继续同一线程」的工作流报错 `already has an active writer`，属回归性缺陷。
- **重要性**：远程接管是桌面端核心协同场景，该回归直接影响跨设备开发者工作流。
- 链接：https://github.com/openai/codex/issues/37403

### 🔥 #25744 — macOS 版累积 Computer Use/MCP 辅助进程与僵尸子进程
- **作者**：@quasa0 | 评论 19 | 👍 3
- **概要**：长时间运行后 Codex 会累积大量 Computer Use/MCP helper 进程与 unreaped zombie 子进程，导致 HID 延迟、WindowServer/TCC 阻塞。
- **重要性**：与 #38754（Windows 版同类问题）呼应，说明进程生命周期管理是多平台普遍缺陷。
- 链接：https://github.com/openai/codex/issues/25744

### 🔥 #11011 — 线程切换非常缓慢
- **作者**：@ImanYZ | 评论 23 | 👍 19
- **概要**：桌面端在一次夜间更新后，切换线程/对话变得卡顿且无响应，尤其在会话历史较长时。
- **重要性**：高频基础操作性能退化，直接影响日常使用体验，评论中多位用户确认可复现。
- 链接：https://github.com/openai/codex/issues/11011

### 🔥 #38350 — 周期性定时任务在成功执行后自行暂停
- **作者**：@montao | 评论 4 | 👍 0
- **概要**：ChatGPT Work 网页版中，用户未做任何操作，多个周期性 Scheduled Task 在成功运行后自动从 enabled 变为 paused。
- **重要性**：自动化任务是 Agent 场景的重要入口，无授权自禁用将破坏用户对定时任务的信任。
- 链接：https://github.com/openai/codex/issues/38350

### 🔥 #38754 — Windows 版单任务内反复拉起 stdio MCP 服务且不回收
- **作者**：@youngraison | 评论 7 | 👍 2
- **概要**：Codex Windows 应用在**单个任务内**的每次 new turn 都会重新 spawn 本地 stdio MCP 服务器，进程不被 reaping，导致资源占用持续上升。
- **重要性**：MCP 进程泄漏不仅影响性能，还可能触发 Windows 安全软件误报或句柄耗尽。
- 链接：https://github.com/openai/codex/issues/38754

### 🔥 #39059 — GPT-5.6 Codex 将代码任务演变为自我强化验证层
- **作者**：@squarepots | 评论 3 | 👍 0
- **概要**：在成熟生产代码库上，GPT-5.6 Codex 倾向于生成大量自证式的验证与治理层代码，而非直接完成业务改动，导致 PR 膨胀。
- **重要性**：代表用户对模型行为（model behavior）的反馈，提示官方需要校准模型在既有大型代码库上的最少侵入原则。
- 链接：https://github.com/openai/codex/issues/39059

---

## 4. 重要 PR 进展（10 条）

### #39092 [OPEN] — 新增「向已存在会话排队发消息」命令
- **内容**：新增 `codex queue --thread <THREAD> --message <TEXT>`，基于 `thread/queue/add` app-server API，支持按 UUID 或名称解析活跃会话并投递消息。
- **意义**：为脚本化/自动化方式向现有 Codex 会话发指令提供了原生 CLI 入口。
- 链接：https://github.com/openai/codex/pull/39092

### #39091 [OPEN] — codex-otel OTLP HTTP 导出器支持代理
- **内容**：将 OTLP/HTTP 的 logs/traces/metrics 与 Statsig exporter 全部切换到 `codex-http-client` 的 proxy-aware 传输层，同时保留企业 CA 与 TLS 配置。
- **意义**：解决企业代理环境下遥测数据无法上报的问题，对安全合规部署至关重要。
- 链接：https://github.com/openai/codex/pull/39091

### #39088 [CLOSED] — 加固 TUI 子代理导航
- **内容**：统一使用 `/subagents` 作为子代理选择入口（移除 `/agent` 别名）；子代理线程可安全重入，不覆盖原设置；通知与审批请求仅路由到活跃线程。
- **意义**：降低多子代理协同时的上下文串扰与误操作风险。
- 链接：https://github.com/openai/codex/pull/39088

### #39083 [CLOSED] — 加固 Windows

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 (2026-08-18)

## 今日速览
昨日发布 v0.56.0-nightly 版本，修复了 SSR Agent 的 tsconfig 配置问题。社区讨论高度聚焦于 Agent 子系统的稳定性和可靠性，其中子代理在达到最大轮次后被错误报告为成功（#22323）以及 Generalist agent 永久挂起（#21409）是最受关注的两个缺陷。此外，多线程的“SSR Agent”自动修复 PR 已针对这些高优 bug 提交了对应补丁，其中修复 #22323 的 PR（#28815）已被合并。

## 版本发布

### v0.56.0-nightly.20260817.g9a15c45fb
- 发布内容：本次更新为 `packages/cli/tsconfig` 添加 `composite` 标志，修复了 SSR Agent 在构建过程中遇到的问题（PR [#28813](https://github.com/google-gemini/gemini-cli/pull/28813)）。
- 完整变更日志：[v0.56.0-nightly.20260816...v0.56.0-nightly.20260817](https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260816.g2a87e7be1...v0.56.0-nightly.2)

## 社区热点 Issues
> 以下挑选了过去 24 小时内评论数最多、优先级最高（p0/p1）及用户反馈强烈（👍 较多）的 10 个 Issue。

### 1. 子代理达到 MAX_TURNS 后恢复被错误报告为 GOAL 成功 — [#22323](https://github.com/google-gemini/gemini-cli/issues/22323)
- **标签**：p1, kind/bug, area/agent, status/need-retesting
- **热度**：评论 12 | 👍 2 | 维护者锁定讨论
- **要点**：`codebase_investigator` 子代理实际已达最大轮次限制，未能进行任何分析，但其恢复流程却将其终止原因改写为 `GOAL` 并标记为成功。这导致用户无法感知到任务被中断，存在误导性。
- **点评**：该 Issue 已获得对应修复 PR（#28815），并进入待复测状态，是当前 Agent 可靠性改进的核心问题之一。

### 2. Generalist agent 无限期挂起 — [#21409](https://github.com/google-gemini/gemini-cli/issues/21409)
- **标签**：p1, kind/bug, area/agent, status/need-retesting
- **热度**：评论 8 | 👍 8 | 维护者锁定讨论
- **要点**：当 Gemini CLI 将任务委派给 Generalist agent 时，即使是简单的"创建文件夹"操作也会永久挂起（用户最长等待 1 小时）。明确指示模型不要委派给子代理可绕过此问题。
- **点评**：8 个 👍 表明这是影响面较广的高频问题，社区反应强烈。

### 3. 组件级评估（Component Level Evaluations）— [#24353](https://github.com/google-gemini/gemini-cli/issues/24353)
- **标签**：p1, area/agent, aiq/eval_infra, kind/customer-issue
- **热度**：评论 7 | 维护者锁定讨论
- **要点**：作为 #15300 的后续 EPIC，该 Issue 规划了行为评估测试的规模化演进。目前已生成 76 个行为评估测试，并为 6 个受支持的 Gemini 模型运行，目标是构建更稳健的组件级评估体系。
- **点评**：这并非用户报告的 bug，而是维护者内部的质量保障基建，反映了项目对回归测试的重视。

### 4. 评估 AST 感知文件读取、搜索与代码库映射的影响 — [#22745](https://github.com/google-gemini/gemini-cli/issues/22745)
- **标签**：p2, area/agent, kind/feature, workstream-rollup
- **热度**：评论 7 | 👍 1 | 维护者锁定讨论
- **要点**：该 EPIC 探索是否引入 AST 感知工具，以实现更精确的方法边界读取（降低 token 噪声）、更智能的代码搜索和代码库映射，提高多轮交互效率。
- **点评**：代表了社区对 agent 代码理解能力的下一阶段演进方向。

### 5. Gemini 未充分自主使用 skills 和 sub-agents — [#21968](https://github.com/google-gemini/gemini-cli/issues/21968)
- **标签**：p2, kind/bug, area/agent, status/need-retesting
- **热度**：评论 6 | 维护者锁定讨论
- **要点**：用户反馈 Gemini 几乎不会主动调用自定义 skills 和 sub-agents，即使已有 "gradle"/"git" 等描述清晰的技能，也需显式指令才会使用。
- **点评**：自主调用决策能力的不足，直接影响了用户对 Agent 自动化能力的体验。

### 6. Auto Memory 对低信号会话无限重试 — [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)
- **标签**：p2, kind/bug, area/agent
- **热度**：评论 5 | 维护者锁定讨论
- **要点**：Auto Memory 仅当提取 agent 成功读取 transcript 后才标记会话为已处理。若 agent 判断会话低信号而跳过，该会话会被反复重试直至超时，造成资源浪费。
- **点评**：反映了后台 agent 任务调度逻辑中的边界条件缺陷。

### 7. Shell 命令执行完成后卡在 "Waiting input" — [#25166](https://github.com/google-gemini/gemini-cli/issues/25166)
- **标签**：p1, area/core, kind/bug, effort/medium
- **热度**：评论 4 | 👍 3 | 维护者锁定讨论
- **要点**：执行已完成的简单 CLI 命令后，Gemini 偶发挂起，界面仍显示命令运行中并等待用户输入。该问题可复现于不会请求输入的最小化命令。
- **点评**：终端交互状态机存在缺陷，3 个 👍 表明影响较多用户。

### 8. 增强 browser_agent 韧性：自动会话接管与锁恢复 — [#22232](https://github.com/google-gemini/gemini-cli/issues/22232)
- **标签**：p3, kind/feature, area/agent, kind/customer-issue
- **热度**：评论 4 |

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-18** ｜ 数据来源：[github.com/github/copilot-cli](https://github.com/github/copilot-cli)

---

## 1. 今日速览

过去 24 小时无新版本 Release，社区热度主要集中在一个长期未决的键盘输入问题（#1481）与多个 MCP OAuth 兼容性回归上。与此同时，非交互模式（`copilot -p`）与交互模式行为不一致、长会话稳定性问题开始密集浮现。

---

## 2. 社区热点 Issues（精选 10 条）

过去 24 小时共 28 条 Issue 更新，以下为最值得关注的 10 条：

### 🔥 高热度 & 高影响

**#1481 — [CLOSED] SHIFT+ENTER 应换行，却执行了 prompt**
- 作者：@mithunshanbhag ｜ 评论：28 ｜ 👍：17
- 影响：所有 CLI 用户的输入习惯，讨论热度最高
- 社区反馈：多数聊天应用以 `SHIFT+ENTER` 换行，Copilot CLI 反其道而行之，用户普遍认为是“Mildly annoying”
- 链接：https://github.com/github/copilot-cli/issues/1481

**#4390 — 组织已启用的模型（Claude Sonnet 5/Opus 5、Kimi K3）在模型目录中缺失**
- 作者：@Rogn ｜ 评论：8 ｜ 👍：7
- 影响：Copilot Business 组织客户无法在 CLI 中选用已由管理员启用的 Anthropic 和 Kimi 模型
- 链接：https://github.com/github/copilot-cli/issues/4390

**#4480 — Atlassian MCP OAuth 失败（1.0.79 较 1.0.71 回归）**
- 作者：@jfrost-fabric ｜ 评论：5 ｜ 👍：6
- 影响：`Incompatible authorization server (RFC 8414 §3.3)`，远程 MCP 服务在 1.0.79 无法完成 OAuth 发现，属于升级后的行为回归
- 链接：https://github.com/github/copilot-cli/issues/4480

**#4509 — `--no-alt-screen` 被静默移除，alt-screen 无法避开且表现异常**
- 作者：@bounis ｜ 评论：0 ｜ 👍：1
- 影响：自 3 月以来已有 #1799、#2334 等多个 issue 反馈 alt-screen 问题，如今唯一的规避手段也被无声删除，用户质疑程度较高
- 链接：https://github.com/github/copilot-cli/issues/4509

**#4506 — 内存压力 watchdog 在 23% 上下文占用时强制压缩，仅回收 0.003% token，随后循环直至 OOM**
- 作者：@jay-tau ｜ 评论：0 ｜ 👍：0
- 影响：长会话场景下的严重稳定性缺陷，压缩逻辑未将上下文实时使用率纳入判断
- 链接：https://github.com/github/copilot-cli/issues/4506

### 🔧 功能缺陷 & Bug

**#4505 — 恢复会话后所有 prompt 报错：`input item ID does not belong to this connection`**
- 作者：@Adamkadaban ｜ 评论：0 ｜ 👍：0
- 影响：远程/本地恢复的会话无法继续使用，且 `/fork` 不能恢复
- 链接：https://github.com/github/copilot-cli/issues/4505

**#4504 — `account.getQuota` 将请求时间戳误作为 `resetDate` 返回**
- 作者：@chrisjq ｜ 评论：0 ｜ 👍：0
- 影响：使用 JSON-RPC（`--server`）的开发者会拿到错误的配额重置时间，影响自动化逻辑
- 链接：https://github.com/github/copilot-cli/issues/4504

**#4507 — 仓库级 `enabledPlugins` 在非交互模式（`copilot -p`）被忽略**
- 作者：@RezaJooyandeh ｜ 评论：1 ｜ 👍：0
- 影响：同一份 `.github/copilot/settings.json` 配置，交互模式生效、非交互模式不生效，造成流水线中的插件行为不一致
- 链接：https://github.com/github/copilot-cli/issues/4507

**#4508 — 自定义指令（`.github/instructions/`）无法在会话中途热重载**
- 作者：@micsh ｜ 评论：0 ｜ 👍：0
- 影响：跨天/跨 compaction 的长会话永远使用旧版指令，200+ 次 compaction 仍不重新加载
- 链接：https://github.com/github/copilot-cli/issues/4508

**#4512 — MCP 注册表策略拉取失败时，本地自定义 stdio MCP server 被一并阻止**
- 作者：@dochollidayxx ｜ 评论：0 ｜ 👍：0
- 影响：安全策略 `fail closed` 的设计对用户本地手动定义的 stdio MCP 服务过于严格，缺乏逃生通道
- 链接：https://github.com/github

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-08-18

> 数据源：github.com/MoonshotAI/kimi-cli | 仅统计过去 24 小时更新

## 今日速览
过去 24 小时仓库整体活动较少：无新 Release、无 Issue 更新，仅 1 条 PR 出现状态变化。PR #864 提出新增 `--starting-prompt / -s` 标志，允许用户启动 CLI 时直接传入初始 prompt，避免“先启动、再退出、带参重启”的低效流程。该功能如果落地，将显著优化脚本化调用与快速交互体验。

## 版本发布
本期无新版本发布。查看历史 Releases：[GitHub Releases](https://github.com/MoonshotAI/kimi-cli/releases)

## 社区热点 Issues
**过去 24 小时无 Issue 更新。**

不过，今日 PR #864 关联了两个重要 Issue，可作为近期社区关注点的参考：
- [#887](https://github.com/MoonshotAI/kimi-cli/issues/887)：被 PR #864 标记为“Closes”，即该 PR 要解决的核心需求——启动时直接指定 prompt。
- [#785](https://github.com/MoonshotAI/kimi-cli/issues/785#issuecomment-3837789973)：PR 作者提到该 Issue 中有“相关的简单讨论”，可能与启动行为或提示词模式有关。

> 由于缺乏过去 24 小时的 Issue 动态，无法给出 10 个热点 Issue 排行。可关注上方关联 Issue 以了解功能背景。

## 重要 PR 进展

**过去 24 小时有更新的 PR 共 1 条，且为 Closed 状态。**

### #864 [CLOSED] feat: --starting-prompt flag to prompt without exit
- 作者：[@stebbins](https://github.com/stebbins)
- 创建：2026-02-02 ｜ 更新：2026-08-17 ｜ 👍 0 ｜ 评论数未披露
- 链接：[PR #864](https://github.com/MoonshotAI/kimi-cli/pull/864)

**功能内容：**
- 新增 `--starting-prompt` / `-s` 命令标志。
- 作用：启动 CLI 后直接进入 prompt 模式，无需先启动再退出，即可在命令行中预设初始提问或指令。

**说明：** 当前 PR 状态为 **CLOSED**，并非 merged。可能已被维护者关闭或需要进一步修改。但该需求本身值得关注，尤其对自动化工作流和快速启动场景有实际价值。

## 功能需求趋势
从今日唯一的 PR 及其关联 Issue 可以观察到一条清晰的社区需求线索：

> **“启动时即进入指定 prompt 场景”**

这一趋势反映出用户希望减少“启动 CLI → 进入默认界面 → 退出 → 配置参数 → 再次启动”的重复操作，进一步向“一条命令完成上下文初始化”演进。未来可能衍生以下方向：
- 支持通过环境变量或配置文件预设 prompt；
- 支持 `kimi -s "翻译以下内容"` 这类快速任务调用；
- 扩展为 `--starting-prompt` 与其他执行标志（如 `--execute`、`--no-stream`）的组合使用。

## 开发者关注点
- **启动流程效率**：开发者对 CLI 的启动参数灵活性有明确诉求，希望通过 `-s` 直接进入工作状态。
- **脚本友好性**：新增 flag 对 CI/CD 集成、Shell 别名、批处理任务等场景非常友好，说明社区正在把 KCLI 当作可嵌入的工具链组件使用。
- **Issue 关联性**：PR 同时提及 #887 和 #785，表明这两个 Issue 所讨论的问题与启动交互相关，后续值得持续跟踪维护者对关闭理由的说明。

---

*注：本日报严格基于数据源“过去 24 小时”的实际动态生成。由于活跃数据较少，部分栏目内容相应精简，以真实反映仓库状态。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-18

## 今日速览

过去24小时内无新版本发布，但社区围绕 **Windows 平台兼容性**（ARM64 TUI 崩溃、路径与权限配置）、**服务端点退役与配额问题** 以及 **MCP 工具连接但不可用** 等话题展开了密集讨论。PR 方面，大量历史 PR 被 `automated-pr-cleanup` 流程标记为已关闭，但其中包含 `/workflow` 命令、`session loop` 等有意义的功能提案，核心 2.0 的远程工作区生命周期等基建 PR 仍在推进。

## 版本发布

过去 24 小时内无新版本 Release。

## 社区热点 Issues

以下为评论数最多、社区关注度最高的 10 个 Issue：

1. **[#19130] Windows ARM64 原生：OpenTUI 使用 bun:ffi dlopen TinyCC 初始化失败**
   - 评论 18 · 👍 12 · 创建于 2026-03-25，本周持续更新
   - Windows 11 ARM64 上原生 ARM64 二进制可运行非交互命令，但 TUI 无法初始化。社区关注度高，长期未闭环。
   - https://github.com/anomalyco/opencode/issues/19130

2. **[#43105] [2.0] BUG：endpoint 错误 — Legacy inference endpoint retired（410）**
   - 评论 15 · 创建于 2026-08-17
   - 用户尝试使用 `https://opencode.ai/inference/v1` 作为 endpoint，所有 CLI 均提示 410 Gone：旧推理端点已退役。OpenCode 2.0（Beta）行为不一致，引发对新旧端点迁移的困惑。
   - https://github.com/anomalyco/opencode/issues/43105

3. **[#7801] [FEATURE]：Plan Mode + Question tool 可自动切换到 Build Mode**
   - 评论 11 · 👍 32 · 创建于 2026-01-11
   - Plan Mode 已就绪，但需要用户手动切换模式。该提案获得 32 个 👍，是社区最期待的工作流增强之一。
   - https://github.com/anomalyco/opencode/issues/7801

4. **[#22861] Bug：Big Pickle 提前停止响应**
   - 评论 10 · 👍 3 · 创建于 2026-04-16
   - Big Pickle 在描述功能实现方案时在同一位置连续两次提前停止，无法继续。用户报告可稳定复现。
   - https://github.com/anomalyco/opencode/issues/22861

5. **[#40243] ChatGPT OAuth 拒绝 EU 工作区的 GPT-5.6 模型，而官方 Codex CLI 可正常使用**
   - 评论 9 · 👍 4 · 创建于 2026-08-03
   - EU 数据/推理驻留工作区通过 OAuth 调用 GPT-5.6 失败，官方 Codex CLI 同环境成功。涉及 OAuth 与 OpenAI 区域策略兼容性问题。
   - https://github.com/anomalyco/opencode/issues/40243

6. **[#33027] [BUG] MCP 工具已连接但未暴露给 Agent**
   - 评论 8 · 👍 3 · 创建于 2026-06-19
   - MCP server `pdfrag` 成功连接并可通过 `tools/list` 暴露 6 个工具，但 Agent 的工具列表中不显示。MCP 协议正常，疑似工具注册/转发逻辑缺陷。
   - https://github.com/anomalyco/opencode/issues/33027

7. **[#24153] [FEATURE]：为已归档会话添加取消归档/恢复功能**
   - 评论 8 · 👍 11 · 创建于 2026-04-24
   - 归档会话目前是单向操作，归档后仅以灰色显示，无法恢复。获得 11 个 👍，会话管理体验的重要缺口。
   - https://github.com/anomalyco/opencode/issues/24153

8. **[#36681] [Bug] Windows 路径引用及外部目录权限配置不生效**
   - 评论 7 · 创建于 2026-07-13
   - 尝试在配置中使用 Windows 路径时失败，且官方文档缺少 Windows 路径处理说明。Windows 用户配置 `external_directory` 权限时受阻。
   - https://github.com/anomalyco/opencode/issues/36681

9. **[#42995] Quota 问题：收费 $3.02 即达 5 小时 Quota（$12）上限**
   - 评论 4 · 👍 3 · 创建于 2026-08-17
   - 用量显示费用仅 $3.02，但 5 小时配额（$12）已耗尽。Quota 计量与实际费用不符，影响用户正常使用。
   - https://github.com/anomalyco/opencode/issues/42995

10. **[#43054] 除 hy3-free / deepseek flash free 外其他模型均报 Forbidden: `{model: big-pickle}`**
    - 评论 3 · 👍 1 · 创建于 2026-08-17
    - 几乎所有模型（除两个免费模型）在请求时返回 Forbidden，错误体指向 `big-pickle`。疑似网关路由/模型白名单配置问题。
    - https://github.com/anomalyco/opencode/issues/43054

## 重要 PR 进展

过去 24 小时内多数 PR 被 `automated-pr-cleanup` 自动关闭，以下为功能意义较大或修复关键问题的 10 个 PR：

1. **[#37504] feat(opencode): 新增 session loop 命令（/loop & /proactive）**
   - 新增内置 `/loop` 命令及 `/proactive` 别名，帮助会话循环执行。原 PR #23575 因久未更新产生冲突，本次为更新版。
   - https://github.com/anomalyco/opencode/pull/37504

2. **[#37499] feat: 新增 /workflow 斜杠命令，支持多步骤 YAML 流水线**
   - 允许用户在 `.opencode/workflows/` 下通过 YAML 定义多步骤流水线，并通过 `/workflow` 触发。面向复杂任务编排的新功能。
   - https://github.com/anomalyco/opencode/pull/37499

3. **[#37477] fix: session list 不再启动完整实例**
   - `session list` 之前仅查询数据库也会启动完整实例，拖慢启动，且可能引发不必要的副作用。本轮修复显著优化了该命令的性能。
   - https://github.com/anomalyco/opencode/pull/37477

4. **[#37494] fix(snapshot): `info/exclude` 写入失败时优雅处理，而非 `orDie` 崩溃**
   - 当快照 gitdir 因 UID 不匹配等原因触发 `EACCES` 时，`Snapshot.sync` 不再直接崩溃。修复 #37493 报告的文件系统权限异常崩溃。
   - https://github.com/anomalyco/opencode/pull/37494

5. **[#37472] fix(opencode): 从无效工具输出中剥离 provider 控制 token**
   - 部分 OpenAI 兼容 provider 返回的 tool arguments 包含 `<|tool_call_begin|>` 等原始控制 token，本 PR 在解析前将其剥离。修复 #37297。
   - https://github.com/anomalyco/opencode/pull/37472

6. **[#37453] fix(session): fork 会话时清空 reasoning 状态**
   - Fork 会话会继承 OpenAI reasoning 的 `itemId` 和 `reasoningEncryptedContent`，导致部分 Responses 兼容接口报错。修复 #37444。
   - https://github.com/anomalyco/opencode/pull/37453

7. **[#37438] fix(task): 忽略无效 task_id 而非崩溃**
   - 此前 `task` 遇到模型生成的非法 UUID 时会抛出 “Expected a string starting with...” 崩溃，现改为忽略该无效 ID。修复 #37440。
   - https://github.com/anomalyco/opencode/pull/37438

8. **[#37437] feat(core): 新增远程工作区生命周期 seam（2.0 基建）**
   - 为集中执行的 V2 Sessions 引入 provider-neutral 的工作区生命周期与环境 seam（create/connect/suspend/reconcile/delete），支撑托管 Workspaces 场景，未触碰 server host checkout。
   - https://github.com/anomalyco/opencode/pull/37437

9. **[#37460] fix(tui): 修复 `truncateMiddle` 在 maxLength 为 1 或 2 时的越界问题**
   - `truncateMiddle("abcdefghij", 1)` 此前会返回超出 maxLength 的字符串。修复 #37458。
   - https://github.com/anomalyco/opencode/pull/37460

10. **[#37457] feat(i18n): 新增高棉语（kh）本地化词典**
    - 为界面补充高棉语本地化支持，覆盖核心 UI 文案，并同步了相关文档。
    - https://github.com/anomalyco/opencode/pull/37457

> 补充：#37467 文档类 PR 将 opencode-lightpanda 插件加入生态页面；#37452 将 my-opencode-deepseek-config 示例加入生态页面跨 18 种语言。均为社区生态扩充，供参考。

## 功能需求趋势

从近期 Issue 与 PR 中可提炼出以下社区关注方向：

1. **Windows 平台体验补齐（高频）**
   - ARM64 原生 TUI、路径引用、cmdlet 权限、npm 全局安装、grep/ripgrep 提取、MSIX PowerShell 兼容性等，Windows 成为当前 BUG 最密集的平台。
2. **会话生命周期管理增强**
   - 归档恢复（#24153）、超大文本

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*