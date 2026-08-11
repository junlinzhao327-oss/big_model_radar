# AI CLI 工具社区动态日报 2026-08-12

> 生成时间: 2026-08-11 23:07 UTC | 覆盖工具: 7 个

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

**报告日期**: 2026-08-12
**数据来源**: 当日社区动态摘要（覆盖 7 个主流工具，其中 3 个有完整数据）

---

## 1. 生态全景

AI CLI 工具已从"能跑通 Agent 流程"进入**稳定性与精细化治理**阶段：头部玩家（Codex、Qwen Code）以近乎每日发布的速度迭代，但高频发布伴随的回归问题（OOM、资源泄漏、沙箱权限）正在消耗用户信任。与此同时，跨会话记忆（Memory System）成为社区最强烈的共性诉求，而推理强度（Reasoning Effort）配置、MCP/ACP 协议治理则被多个项目同步推进，预示着 AI CLI 正从"单次任务工具"演化为"可精细管控的长期开发基础设施"。值得注意的是，7 个主流工具中仅 3 个在本次摘要中有实质动态，工具间的活跃度与社区声量差距明显拉大。

---

## 2. 各工具活跃度对比

> 注：Claude Code、Gemini CLI、GitHub Copilot CLI、OpenCode 在本日摘要中无实质数据，仅列出已知状态，不做推测。

| 工具 | 热点 Issues | PR 进展 | Release（24h） | 数据完整性 |
|------|------------|---------|----------------|-----------|
| **OpenAI Codex** | 10（含 2 个已关闭） | 10（全部 OPEN） | 2 个 pre-release（rust-v0.148.0-alpha.7 / alpha.8） | ✅ 完整 |
| **Qwen Code** | 10（1 个 P1） | 5+（摘要截断） | 3 个（v0.21.10、nightly、live-host-v0.1.1） | ⚠️ 较完整 |
| **Kimi Code CLI** | 5（全部 OPEN） | 8（7 关闭 / 1 活跃） | 0 | ✅ 完整 |
| **Claude Code** | — 无数据 — | — 无数据 — | — 无数据 — | ❌ 缺失 |
| **Gemini CLI** | — 无数据 — | — 无数据 — | 昨日发布 v（被截断） | ❌ 缺失 |
| **GitHub Copilot CLI** | — 无数据 — | — 无数据 — | — 无数据 — | ❌ 缺失 |
| **OpenCode** | — 无数据 — | — 无数据 — | — 无数据 — | ❌ 缺失 |

**核心发现**：OpenAI Codex 在 Issue 热度和 PR 活跃度上均领先（10+10），且保持每日双 pre-release 的高频节奏；Qwen Code 发布频次同样密集（含 nightly），但 PR 摘要被截断，完整度仅次于 Codex；Kimi Code 相对平静——单日 0 Release，唯一活跃 PR 是连续 25 天未合并的 #2509。

---

## 3. 共同关注的功能方向

### 3.1 推理强度 / 思考预算配置（Reasoning Effort）
| 工具 | 具体表现 |
|------|---------|
| **Kimi** | PR #2509 新增 `/effort` 命令，可配置 thinking effort（持续 25 天未合入） |
| **Qwen Code** | v0.21.10 新增 ACP 会话级推理强度配置（Default→Max） |
| **Codex** | 安全拦截 issue 中出现 `gpt-5.6-sol-xhigh` 模型，暗示模型级 effort 档位已存在 |

**共性诉求**：用户不满足于"只能选模型"，要求对推理预算做显式控制，以平衡成本与输出质量。

### 3.2 跨会话记忆与上下文管理
| 工具 | 具体表现 |
|------|---------|
| **Kimi** | #1283（34 评论）与 #1478 双 issue 直指记忆系统缺失，是当前最强单项需求 |
| **Codex** | #37421（Esc-Esc 回溯失效，25 👍）与 #11907（会话同步一致性） |

**共性诉求**：大项目开发中上下文丢失是最高频痛点，`agent.md` 这类文件式方案只能算 workaround，社区期待系统级持久记忆。

### 3.3 MCP/ACP 协议治理
| 工具 | 具体表现 |
|------|---------|
| **Codex** | PR #38081 统一 MCP 审批流程（`ReviewDecision`）、#38052 支持 MCP OAuth 客户端注册 |
| **Qwen Code** | v0.21.10 做 ACP 推理强度会话配置；#8182 关注 daemon 向 ACP 子进程授权内存过大 |
| **Kimi** | 多个 ACP 相关 PR（#2057、#1393）合入，完善 ACP Python 实现 |

**共性诉求**：协议层正在经历"从小规模使用到企业级治理"的升级——审批、认证、资源隔离是共同课题。

### 3.4 资源泄漏与长会话稳定性
| 工具 | 具体表现 |
|------|---------|
| **Codex** | MCP 管道 FD 泄漏→EMFILE（#26984）、macOS OOM 崩溃（#36523）、Windows 磁盘 400GiB 膨胀（#35470） |
| **Qwen Code** | daemon 向每个子进程授权 50% 宿主内存→多进程 OOM 风险（#8182） |

**共性诉求**：长时运行的 Agent 会话暴露了操作系统级资源治理短板，文件描述符、内存、磁盘的释放与上限控制成为信任门槛。

### 3.5 Windows 平台兼容性
| 工具 | 具体表现 |
|------|---------|
| **Codex** | Windows 沙箱嵌套 Git 仓库支持（#38080）、根目录 ACL 授权（#38064） |
| **Kimi** | #2600 PowerShell 7 非 C 盘启动路径 Bug |
| **Qwen Code** | #8644 Windows 盘符冒号被 URL 编码、#8901 macOS iTerm 闪屏（终端兼容） |

**共性诉求**：Windows 仍是缺陷密度最高的平台，沙箱权限、路径解析、终端渲染三方面问题最为集中。

---

## 4. 差异化定位分析

| 维度 | OpenAI Codex | Qwen Code | Kimi Code CLI |
|------|-------------|-----------|---------------|
| **技术栈** | Rust 核心 | TypeScript/Node + daemon 架构 | Python |
| **产品形态** | CLI + 桌面端 + iOS，全平台矩阵 | CLI + VS Code 扩展 + Web Shell | 纯 CLI（Python 包） |
| **目标用户** | Pro/Max 订阅的高强度用户，重远程与多端协作 | 自动化/无头场景（stream-json）、多工作区开发者 | 大项目开发者，追求轻量 CLI + ACP 生态 |
| **迭代风格** | 高频激进（日双 pre-release），基础设施优先（沙箱、MCP、认证） | 稳步推进（版本 + nightly），重视 UI 体验与 daemon 稳定性 | 社区驱动但核心团队资源有限，PR 吸收慢（25 天未合并） |
| **当前短板** | 桌面端回归频繁（OOM、远程控制失效）、Windows 沙箱缺陷密度高 | P1 会话恢复超时、OpenAI 兼容 API 错误误报成功（误导自动化） | 记忆系统长期缺位、0 新 Release、新功能迭代放缓 |
| **独特亮点** | MCP 审批治理最完善（跨会话持久化策略）；Linux 桌面诉求达 950 👍（生态引力强） | OpenTUI 全新渲染后端（无闪烁 + 鼠标支持）；守护跨 worktree Git 变更，安全设计深入 | 社区提的 ACP/Python 修复 PR 批量合入（7/8），印证开源协作有效 |

---

## 5. 社区热度与成熟

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告

**数据范围**：github.com/anthropics/skills ｜ 截至 2026-08-12

---

## 1. 热门 Skills 排行

按评论/关注度排序，选取 Top 8（当前全部为 Open 状态）：

### 🥇 #1298　skill-creator 评估循环修复（recall 恒为 0%）
- **功能**：修复 `run_eval.py` 在全部查询下都报 recall=0% 的严重 bug——该脚本被 `run_loop.py` 和 `improve_description.py` 消费，导致描述优化循环在「对着噪声优化」。同时修复 Windows 流读取、触发检测与并行 worker 问题。
- **社区热点**：仓库最热 PR，直接回应 #556（12 条评论、7 👍，大量独立复现）。`skill-creator` 工具链不可用已成为开发者核心痛点。
- **状态**：Open（2026-06-10 创建，06-23 更新）
- 🔗 https://github.com/anthropics/skills/pull/1298

### 🥈 #514　document-typography 技能（文档排版质量控制）
- **功能**：新增文档排版技能，防止 AI 生成文档中的孤词换行（orphan）、孤行段落标题（widow）及编号错位三类典型排版问题。
- **社区热点**：讨论聚焦于「Claude 生成的每份文档都会遇到、但用户很少主动要求」的隐性质量问题，属于高普适性技能。
- **状态**：Open（2026-03-04 创建）
- 🔗 https://github.com/anthropics/skills/pull/514

### 🥉 #538　pdf 技能：修复 SKILL.md 大小写敏感引用
- **功能**：修复 `skills/pdf/SKILL.md` 中 8 处大小写不匹配（`REFERENCE.md` → `reference.md`、`FORMS.md` → `forms.md`），该问题在大小写敏感文件系统（Linux/macOS）上会直接导致引用失效。
- **社区热点**：虽为小修复，但戳中跨平台可移植性的普遍痛点；同作者另有 docx 与 skill-creator 相关修复（#541、#539），形成系列贡献。
- **状态**：Open（2026-03-06 创建，04-29 更新）
- 🔗 https://github.com/anthropics/skills/pull/538

### #486　ODT 技能（OpenDocument 创建/填充/转 HTML）
- **功能**：新增 `.odt/.ods` 文件的创建、模板填充、读取与转 HTML 能力，覆盖 LibreOffice 及 ISO 标准格式需求。
- **社区热点**：讨论围绕「开源/ISO 标准格式」在企业文档场景的落地价值，是文档类技能方向的重要补充。
- **状态**：Open（2026-03-01 创建，04-14 更新）
- 🔗 https://github.com/anthropics/skills/pull/486

### #210　frontend-design 技能可执行性优化
- **功能**：重构 frontend-design 技能，目标是将每条指令收敛为「Claude 能在单次对话中真正执行」的动作，提升内部一致性与行为引导力。
- **社区热点**：反映社区对 Skill 质量的深层反思——技能文档不宜像开发者文档，而

---



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-12

## 今日速览
- 发布两个 Rust 预发布版本（0.148.0-alpha.7 / alpha.8），持续推进 CLI 核心与桌面端联动修复。
- macOS 桌面端回归问题集中爆发：OOM 崩溃、远程控制线程失效、子进程泄漏等成为最热门 bug 类别。
- 社区对 Linux 桌面应用支持的需求持续高涨（950 👍 / 207 条评论），成为当前最具影响力的 Feature Request。

## 版本发布
过去 24 小时发布两个预发布版本，未附详细变更说明，但版本号为 rust-v0.148.0-alpha.8 和 rust-v0.148.0-alpha.7（对应 codex-cli 0.148.0 系列）。建议关注后续 release notes 以确认修复内容。

- [rust-v0.148.0-alpha.8](https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.8)
- [rust-v0.148.0-alpha.7](https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.7)

## 社区热点 Issues（Top 10）

### 1. Codex 桌面版 Linux 支持 [#11023](https://github.com/openai/codex/issues/11023)
- 状态：CLOSED | 评论 207 | 👍 950
- 受 macOS 端 bug 影响，用户强烈希望在 Linux 桌面使用 Codex App。这是社区最关注的单一 issue，已获得近千赞。

### 2. 新增“禁用 60 秒问题自动解析”设置 [#28969](https://github.com/openai/codex/issues/28969)
- 状态：OPEN | 评论 69 | 👍 192
- 用户希望控制 CLI 中问题在 60 秒后自动关闭的行为，目前该行为在长时间任务（如多文件分析）中会打断流程。

### 3. App 每次启动静默创建空的 `~/Documents/Codex` 文件夹 [#20880](https://github.com/openai/codex/issues/20880)
- 状态：OPEN | 评论 22 | 👍 42
- 即使未开启任何项目，app 每次启动都会在 Documents 目录生成空文件夹。用户要求彻底移除该副作用，或提供关闭入口。

### 4. MCP stdio 服务器管道 FD 泄漏 + 孤儿进程 → 累积 EMFILE [#26984](https://github.com/openai/codex/issues/26984)
- 状态：OPEN | 评论 18 | 👍 4
- 长时间运行 codex-cli 会话后，MCP stdio 服务器不断泄漏管道文件描述符并产生孤儿进程，最终导致 “Too many open files”（os error 24）。影响 Pro 用户的长会话稳定性。

### 5. App 子代理卡片关闭后仍卡在 UI [#23930](https://github.com/openai/codex/issues/23930)
- 状态：OPEN | 评论 16 | 👍 4
- 子代理关闭后其卡片仍残留在界面中，即使 close/readback 确认已无 live agent。属于桌面端 UI 状态同步缺陷。

### 6. macOS 桌面端无法恢复远程控制 / CLI 线程（回归） [#37403](https://github.com/openai/codex/issues/37403)
- 状态：OPEN | 评论 9 | 👍 9
- 8 月 7 日更新后，桌面端打开手机端已在跑的远程 CLI 线程时出现 “already has an active writer” 错误，打断 off-hours 工作流。

### 7. [P0][回归] macOS App 启动时 OOM 崩溃：解析 Claude Desktop 1.73 GB 历史数据 [#36523](https://github.com/openai/codex/issues/36523)
- 状态：OPEN | 评论 5 | 👍 1
- `external-agent-import` 在每次启动时扫描 Claude Desktop 约 1.73 GB 数据，导致 V8 heap OOM。机器此前零崩溃，更新后 26 小时内崩溃 26 次。

### 8. Windows 上复制图片 150,000 次，消耗 400 GiB 磁盘空间 [#35470](https://github.com/openai/codex/issues/35470)
- 状态：OPEN | 评论 4 | 👍 0
- CLI 0.145.0 在 Windows 上因图像文件重复复制导致磁盘空间被严重占用，属于文件操作逻辑严重缺陷。

### 9. CLI 0.147.0 Esc-Esc 回溯无法找到已选提示词 [#37421](https://github.com/openai/codex/issues/37421)
- 状态：CLOSED | 评论 4 | 👍 25
- 在持久化线程中使用 Esc-Esc 回溯时无法定位先前选中的 prompt。虽已关闭，但 25 个 👍 表明该功能在 Max 订阅用户中关注度较高。

### 10. 安全请求被拦截：“This content can't be shown” [#34306](https://github.com/openai/codex/issues/34306)
- 状态：OPEN | 评论 13 | 👍 8
- 使用 gpt-5.6-sol-xhigh 时，部分网络安全相关的合法请求被内容安全策略误拦截，且无明确原因展示。

## 重要 PR 进展（Top 10）

### 1. 允许空输入启动新回合 [#38084](https://github.com/openai/codex/pull/38084)
允许在 `Op::UserInput` 无消息项时直接启动一个回合，利用环境上下文生成内容；仍拒绝空输入用于持久化会话。

### 2. 统一 MCP 工具审批流程：`ReviewDecision` [#38081](https://github.com/openai/codex/pull/38081)
新增跨会话持久化的 MCP 审批策略，并将 MCP 审批响应统一走 `ReviewDecision` 类型，保留拒绝原因与超时逻辑。

### 3. Windows 沙箱支持嵌套 Git 仓库 [#38080](https://github.com/openai/codex/pull/38080)
允许沙箱内访问嵌套 Git 仓库。此前 Git 会拒绝沙箱用户操作主用户拥有的仓库，此次对 worktree 根目录及 `/*` 通配符授权。

### 4. TUI 历史记录遵循渲染宽度 [#38075](https://github.com/openai/codex/pull/38075)
新聊天控件按当前终端宽度初始化；按活动渲染模式及环境预留空间判断历史单元可见性，并调整 diff 摘要饱和逻辑。

### 5. Windows 沙箱授予 Codex 应用根目录读取/执行权限 [#38064](https://github.com/openai/codex/pull/38064)
将 read/execute ACL 应用到 Codex 应用根目录并支持继承，同时继续单独处理托管运行时缓存。

### 6. Azure Responses 请求禁用存储 [#38060](https://github.com/openai/codex/pull/38060)
所有 Responses 请求统一设置 `store=false`，包括 Azure 渠道；移除 provider 级存储检查，简化请求构建。

### 7. 配置驱动的外部认证 [#38054](https://github.com/openai/codex/pull/38054)
新增 host-owned 外部认证源，runtime 账户 API 无法替换/清除/登出该源；凭证保存在进程本地，不写入 auth storage。

### 8. MCP OAuth 客户端注册方式可选 [#38052](https://github.com/openai/codex/pull/38052)
为 `codex mcp add` 与 `codex mcp login` 增加 `--oauth-client-registration`（`auto` / `dcr`），协议 schema 同步更新。

### 9. CI 改为针对 PR 合并提交运行 [#38051](https://github.com/openai/codex/pull/38051)
移除显式 PR head ref，让 GitHub Actions 默认 check out synthetic merge commit，避免主分支新变更导致的冲突漏检。

### 10. gRPC 代码模式回调转发至会话委托 [#38072](https://github.com/openai/codex/pull/38072)
每个 gRPC code-mode 会话订阅嵌套工具调用，并将工具/通知回调转发至 delegate；通过 host 完成工具调用并限制超限结果。

## 功能需求趋势
- 🔒 **Linux 桌面 App 支持**（#11023）：仍是社区第一大诉求，与 macOS 端可靠性问题叠加后需求更强烈。
- ⚙️ **可配置的自动行为**（#28969）：用户要求对 CLI 自动解析、自动关闭等行为提供显式开关。
- 🖼️ **CLI 图片粘贴**（#19143）：前端调试场景高频需求，目前仅桌面/TUI 部分支持。
- 🌐 **远程连接与认证增强**（#22857）：SSH 远程主机的密钥认证体验是跨端（Desktop/iOS/CLI）共同痛点。
- 🗂️ **会话同步与手动刷新**（#11907）：归档恢复、跨端（VS Code/CLI/App）同步仍存在一致性问题。

## 开发者关注点
- **资源泄漏问题突出**：MCP 管道 FD 泄漏、子代理内存泄漏、Desktop 子进程残留是三类高频反馈，涉及 CLI 与 App 双端。
- **Windows 沙箱权限**：嵌套 Git 仓库、`apply_patch` 停顿、WindowsApps launcher 拒绝访问等多条 issue 表明 Windows 路径仍有较高缺陷密度。
- **性能回归**：OOM 崩溃（1.73GB 导入）、400GB 磁盘占用、50MB 级超长 JSONL 处理慢等极端性能问题拉低信任度。
- **模型与配置兼容**：自定义 API-key 模式下模型被隐藏、`gpt-5.6-luna` 未知模型错误、multi-agent 不支持普通 API 提供商等问题显示“自带密钥”场景仍是二等公民。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报（2026-08-12）

## 今日速览

昨日 Gemini CLI 发布 v

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-08-12）

## 今日速览
过去 24 小时无新版本发布，但社区围绕 **记忆系统（Memory System）** 的讨论持续升温，多个 Issue 集中反映大项目场景下上下文管理痛点；同时 8 个 PR 中有 7 个为历史 PR 被批量关闭，仅 1 个新 PR（#2509）仍在活跃推进，聚焦推理强度配置功能。

## 社区热点 Issues
（全部 5 条，按更新热度排序）

### 1. [#1283 🚀 记忆系统 · 跨会话持久上下文](https://github.com/MoonshotAI/kimi-cli/issues/1283)
- **作者**: @CatKang | 创建: 2026-02-27 | 评论: 34 | 👍: 0
- **为什么重要**: 这是目前社区呼声最高的增强请求，已持续近半年，34 条评论说明开发者对“跨会话记忆”需求强烈。该 Issue 提出实现自动记忆（AI 管理笔记）和手动记忆（用户自定义指令）的完整方案，直击大项目开发中上下文丢失的痛点。
- **社区反应**: 评论活跃，许多用户分享了当前使用 workaround（如维护 `agent.md`），并期待官方支持。

### 2. [#1478 优化记忆层，大项目开发很痛苦](https://github.com/MoonshotAI/kimi-cli/issues/1478)
- **作者**: @hahy36 | 创建: 2026-03-17 | 更新: 2026-08-11 | 评论: 1
- **为什么重要**: 与 #1283 呼应，直接质疑记忆层实现，并指出文档中仅提及 `agent.md`，缺乏系统性的长期记忆方案。用户还引用了其他工具（如 openclaw）的记忆文件结构作参考，对 Kimi CLI 的改进具有直接参考价值。
- **社区反应**: 评论数虽少，但问题具有普遍性，说明官方文档对记忆功能的说明不充分。

### 3. [#2601 引用回复：在 AI 回复中任意选择文本进行评论](https://github.com/MoonshotAI/kimi-cli/issues/2601)
- **作者**: @topit | 创建: 2026-08-11 | 更新: 2026-08-11 | 评论: 0
- **为什么重要**: 虽然是针对 Kimi Web 的功能请求，但反映了用户对交互精细化的需求——希望像 GitHub 代码评论一样对 AI 回复的段落、代码块、计划步骤进行定点追问。该功能若实现，将大幅提升协作式编程体验。
- **社区反应**: 新 Issue，尚无评论，但需求描述详细，具有代表性。

### 4. [#2600 Windows PowerShell 7 默认 D 盘启动找不到路径](https://github.com/MoonshotAI/kimi-cli/issues/2600)
- **作者**: @RooKichenn | 创建: 2026-08-11 | 更新: 2026-08-11 | 评论: 0
- **为什么重要**: 明确的环境兼容性 Bug，影响 Windows 用户在使用 PowerShell 7 且默认工作目录不在 C 盘时启动 kimi code 失败。报错包含了版本（0.33）和模型信息，便于复现。
- **社区反应**: 新 Issue，待官方确认。

### 5. [#2599 CLI 规划任务出现“验尸”字样](https://github.com/MoonshotAI/kimi-cli/issues/2599)
- **作者**: @KING0177 | 创建: 2026-08-11 | 更新: 2026-08-11 | 评论: 0
- **为什么重要**: 模型输出措辞异常，可能是由于中文翻译/模型生成导致不恰当术语（"Autopsy"），影响用户体验。虽然严重性不高，但反映出模型对中文上下文中专业术语的把握仍需优化。
- **社区反应**: 新 Issue，截图显示界面问题，等待官方回应。

## 重要 PR 进展
（全部 8 个，按活跃度/相关性排序）

### 1. [🚧 #2509 feat(kimi): 可配置思考强度与 /effort 命令](https://github.com/MoonshotAI/kimi-cli/pull/2509)
- **作者**: @n-WN | 创建: 2026-07-18 | 更新: 2026-08-11 | 状态: OPEN
- **内容**: 实现可配置的思考强度（thinking effort），新增 `/effort` 命令，关联 issue #2501，并兼容旧版 `reasoning_effort` 参数。这是目前唯一活跃的 PR，说明官方正在推进推理能力的精细控制。
- **关注点**: 该功能直接影响 API 使用成本和输出质量，社区期待已久。

### 2. [✅ #2057 fix(acp): 用 RuntimeError 替换 assert 语句](https://github.com/MoonshotAI/kimi-cli/pull/2057)
- **作者**: @hobostay | 创建: 2026-04-24 | 更新: 2026-08-11 | 状态: CLOSED
- **内容**: 修复 `acp/session.py` 中 5 个 assert 在 Python 优化模式（`-O`）下失效的安全隐患，改为正确的 `RuntimeError` 异常。
- **重要性**: 提升生产环境的健壮性，属于基础质量改进。

### 3. [✅ #2056 fix(wire): 消除 WireFile.append_record 的 TOCTOU 竞态条件](https://github.com/MoonshotAI/kimi-cli/pull/2056)
- **作者**: @hobostay | 创建: 2026-04-24 | 更新: 2026-08-11 | 状态: CLOSED
- **内容**: 修复 `WireFile.append_record` 中检查文件存在与获取 size 之间的竞态窗口，避免文件被删除时崩溃。
- **重要性**: 提升文件写入可靠性，潜在避免数据丢失。

### 4. [✅ #2055 fix(agentspec): 使用 AgentSpecError 替代 assert](https://github.com/MoonshotAI/kimi-cli/pull/2055)
- **作者**: @hobostay | 创建: 2026-04-24 | 更新: 2026-08-11 | 状态: CLOSED
- **内容**: 将 agentspec 中的断言改为显式异常，防止 `-O` 优化禁用检查。
- **重要性**: 同上，提高代码防御性。

### 5. [✅ #1328 修复文件工具和 UI 反馈的若干小问题](https://github.com/MoonshotAI/kimi-cli/pull/1328)
- **作者**: @hobostay | 创建: 2026-03-03 | 更新: 2026-08-11 | 状态: CLOSED
- **内容**: 修复 StrReplaceFile 替换计数错误、UI 反馈等问题，提升文件编辑工具的准确性。
- **重要性**: 改善日常编码操作体验。

### 6. [✅ #1082 fix(pyinstaller): 过滤不存在的 dateparser 缓存文件](https://github.com/MoonshotAI/kimi-cli/pull/1082)
- **作者**: @hobostay | 创建: 2026-02-10 | 更新: 2026-08-11 | 状态: CLOSED
- **内容**: 修复 PyInstaller 打包时因 dateparser 缓存文件不存在而失败的问题。
- **重要性**: 解决 CI/新环境中的构建问题。

### 7. [✅ #1077 fix: 移除 WriteFile 工具中冗余的 mode 校验](https://github.com/MoonshotAI/kimi-cli/pull/1077)
- **作者**: @hobostay | 创建: 2026-02-10 | 更新: 2026-08-11 | 状态: CLOSED
- **内容**: 删除 WriteFile 中重复的 mode 参数验证逻辑，简化代码。
- **重要性**: 代码整洁性改进。

### 8. [✅ #1393 fix(acp): 将 shell 命令通过终端参数路由](https://github.com/MoonshotAI/kimi-cli/pull/1393)
- **作者**: @hanhan3344 | 创建: 2026-03-10 | 更新: 2026-08-11 | 状态: CLOSED
- **内容**: 修复 ACP Shell 终端执行时命令和参数传递方式，新增 bash 和 PowerShell 的回归测试。
- **重要性**: 增强跨平台终端执行兼容性。

## 功能需求趋势
从当前 Issues 中可提炼出以下社区最关注的功能方向：

1. **记忆系统**（#1283, #1478）：跨会话持久化上下文、自动/手动记忆管理是当下最强需求，尤其影响大型项目开发效率。
2. **交互式评论/引用**（#2601）：期望对 AI 回复进行定点引用和追问，类似代码评审的交互模式。
3. **运行时配置与模型控制**（#2509 PR）：可配置思考强度、`/effort` 命令等，体现对模型行为精细控制的诉求。
4. **跨平台与环境兼容性**（#2600）：Windows PowerShell 路径处理问题，说明多平台支持仍是关注重点。

## 开发者关注点
- **记忆层缺失或文档不足**：用户反映大项目开发中上下文丢失严重，且除 `agent.md` 外未见系统记忆方案，希望官方提供明确的长期记忆机制。
- **中文模型输出措辞**：计划中出现“验尸”等不当术语，提示模型在中文专业场景下需要优化生成质量。
- **环境配置灵活性**：Windows 下非 C 盘启动路径导致的失败，要求 CLI 能适配常见的 PowerShell 工作目录设置。
- **PR 大量关闭**：今日 8 个 PR 中 7 个被关闭（多数为合入），仅 1 个活跃，侧面反映项目正在持续吸收功能并推进，但新功能迭代速度可能受制于核心团队资源。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 · 2026-08-12

## 今日速览

v0.21.10 正式发布，带来 ACP 推理强度（reasoning effort）会话级配置和 Web Shell 图片预览能力；会话恢复超时（#8678）与 OpenAI 兼容 API 错误误报成功（#8920）是今日最受关注的两大问题。社区需求持续聚焦会话管理可靠性、daemon 资源保护、多平台终端体验与集成渠道扩展。

## 版本发布

**v0.21.10**
- 新增 ACP 会话配置，支持将推理强度从 Default 调整至 Max（[#8526](https://github.com/QwenLM/qwen-code/pull/8526)）
- Web Shell 中点击已上传或粘贴的图片，现可在 artifact 中打开预览

**v0.21.9-nightly.20260811**
- 内存相关测试：覆盖上下文刷新标记（context refresh marker）在多次轮次间的传递（[#8809](https://github.com/QwenLM/qwen-code/pull/8809)）

**live-host-v0.1.1**
- 修复 CLI 在选定沙箱运行时的探测逻辑（[#7734](https://github.com/QwenLM/qwen-code/pull/7734)）
- 修复 autofix 中 scan-and-pick 的序列化问题

## 社区热点 Issues

**故障与回归**

1. **大型会话恢复超时导致当前会话丢失**（[#8678](https://github.com/QwenLM/qwen-code/issues/8678)）· P1，7 条评论
   核心会话管理问题：当 restore 超时时，当前工作会话未被保留。PR1 已合入（#8691）实现超时契约与可观测性，社区高度关注后续进展。

2. **stream-json 模式将 OpenAI API 错误误报为成功**（[#8920](https://github.com/QwenLM/qwen-code/issues/8920)）· P2，4 条评论
   无头模式下，API 错误被包装为"成功"结果且进程退出码为 0，对自动化调用方造成严重误导，被多名用户标记为高影响。

3. **Windows 聊天中点击文件链接失败——盘符冒号被 URL 编码**（[#8644](https://github.com/QwenLM/qwen-code/issues/8644)）· P2，4 条评论
   VS Code 扩展中 `file:///d%3A/...` 无法打开文件，Windows 用户日常路径跳转受阻。

4. **0.21.2 起图片加载即崩溃**（[#8957](https://github.com/QwenLM/qwen-code/issues/8957)）· P2，3 条评论
   用户反馈 0.21.1 是最后一个可正常加载图片的版本，正在等待复测信息。

5. **macOS iTerm 下选择命令后闪屏**（[#8901](https://github.com/QwenLM/qwen-code/issues/8901)）· P2，4 条评论
   每次确认执行命令回车后出现闪屏，影响 iTerm 用户日常交互，需补充客户端环境信息。

**配置与资源**

6. **`npm update` 后报告 2 个高危漏洞**（[#8944](https://github.com/QwenLM/qwen-code/issues/8944)）· P2，3 条评论
   自 0.21.0 起每次更新均出现高危漏洞提示，社区关注依赖供应链安全。

7. **daemon 向每个 ACP 子进程授权 50% 宿主内存**（[#8182](https://github.com/QwenLM/qwen-code/issues/8182)）· P2，4 条评论
   内存上限按宿主内存而非子进程数均分计算，多 ACP 子进程场景下存在 OOM 风险。

8. **Shell 忽略 `tools.truncateToolOutputThreshold` 配置**（[#8922](https://github.com/QwenLM/qwen-code/issues/8922)）· P2，3 条评论
   文档声明该配置适用于 Shell，但实际 Shell 仍使用固定 30,000 字符预算，配置不生效。

9. **Provider 更新提示承诺模型切换但实际不再执行**（[#8948](https://github.com/QwenLM/qwen-code/issues/8948)）· P2，3 条评论
   自 #8889 后更新流程无条件移除 `modelSelection`，但确认提示仍告知用户"将切换模型"，存在误导。

10. **multi-workspace 模式冷加载/恢复可能使用错误的运行时存储**（[#8909](https://github.com/QwenLM/qwen-code/issues/8909)）· P2，3 条评论
   `POST /session/:id/load|resume` 未在正确的 ambient storage 上下文中执行 restore，多工作区下可能恢复出错。

## 重要 PR 进展

1. **OpenTUI 渲染器后端（react track）**（[#8677](https://github.com/QwenLM/qwen-code/pull/8677)）
   全新 TUI 渲染架构，主打无闪烁、一流的鼠标支持，是 CLI 交互体验的一次大版本升级。

2. **传播 daemon 会话列表取消信号**（[#8954](https://github.com/QwenLM/qwen-code/pull/8954)）
   会话列表读取支持请求取消，且不影响 #8892 引入的目录缓存，REST 与 ACP 调用者可独立取消。

3. **守护跨 worktree Git 变更**（[#8687](https://github.com/QwenLM/qwen-code/pull/8687)）
   内置宿主机侧防护：识别 `-C`/`--work-tree`/`--git-dir` 跳转，阻止模型发布的 Git 命令逃逸会话目录。

4. **修复 Qwen 3.8 推理预算冲突**（[#8525](https://github.com/QwenLM/qwen-code/pull/8525)）
   解决 DashScope 请求同时携带 `reasoning_

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*