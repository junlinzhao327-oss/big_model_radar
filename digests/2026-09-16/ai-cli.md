# AI CLI 工具社区动态日报 2026-09-16

> 生成时间: 2026-09-15 22:35 UTC | 覆盖工具: 7 个

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

# AI CLI 工具社区动态横向对比分析报告  
**数据日期：2026-09-16｜样本：Claude Code、OpenAI Codex、Gemini CLI、GitHub Copilot CLI、Kimi Code CLI、OpenCode、Qwen Code**

> 数据口径说明：以下基于各工具当日社区摘要。OpenAI Codex 数据源为空，未纳入有效对比；部分工具摘要截断，Issue/PR 数量按“可见范围”标注。

---

## 1. 生态全景

当前 AI CLI 工具已从“终端聊天 + 代码补全”进入 **Agent 编排平台化竞争**阶段：子代理、工作流、持久状态、上下文压缩、成本归因成为共同演进方向。与此同时，社区反馈重心明显从“功能有没有”转向“能不能稳定跑、失败是否诚实、成本是否可控”。平台一致性、长会话内存、OAuth/MCP 认证链路和企业网关可观测性，正在成为规模采纳的主要瓶颈。头部工具版本迭代仍快，但回归与静默失败正在快速消耗用户信任。

---

## 2. 各工具活跃度对比

| 工具 | Issues 动态 | PR 动态 | Release 情况 | 今日关键词 |
|---|---|---|---|---|
| **Claude Code** | 过去 24h 更新约 50 条，筛选出 10+ 热点 | 1 条 | v2.1.273、v2.1.272 | 网关 Header、Windows 回归、Agent 编排、MCP 认证 |
| **OpenAI Codex** | 无数据 | 无数据 | 无数据 | 数据缺失，无法评估 |
| **Gemini CLI** | 过去 24h 更新约 50 条，Top 10 热点 | Top 10 | v0.60.0、v0.61.0-preview.0、nightly | 子代理挂起、MAX_TURNS 误报、AST、PTY 泄漏、OAuth |
| **GitHub Copilot CLI** | 10 条热点 | 0 条 | v1.0.84-7/8/9 | 长会话 OOM、

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（截止 2026-09-16）

> 数据口径：PR 评论数字段在原始数据中为 `undefined`，因此“热门 PR”按仓库给出的排序（即按评论数排序后的前 20）取前 8，并结合更新活跃度与关联 Issue 判断。以下 PR 状态均为 **OPEN**。

## 1. 热门 Skills 排行（PR）

1. **#1298 skill-creator 触发评估修复**  
   功能：隔离 trigger evals，处理 Windows 下 subprocess pipe 问题，避免运行时失败被误判为“未触发”。  
   讨论热点：触发评估误报、跨平台兼容、负例误通过。  
   状态：OPEN，2026-09-15 更新。  
   https://github.com/anthropics/skills/pull/1298

2. **#1703 新增 md2video-audio skill**  
   功能：将 Markdown 通过 Marp 转为演示幻灯片，再编译为带类真人语音的 MP4 视频，零成本方案。  
   讨论热点：多模态内容生成、文档到视频的自动化工作流。  
   状态：OPEN，2026-09-15 更新。  
   https://github.com/anthropics/skills/pull/1703

3. **#1742 mcp-builder 适配 MCP SDK v2**  
   功能：支持 `mcp>=2.0.0` 中 `streamable_http_client` 重命名，以及通过 `create_mcp_http_client` 配置自定义 headers。  
   讨论热点：MCP 生态升级兼容性，关联 Issue #1668。  
   状态：OPEN，2026-09-13 更新。  
   https://github.com/anthropics/skills/pull/1742

4. **#1734 检测 DOCX 孤立评论**  
   功能：检测 Word 文档中失去锚点的 orphaned comments。  
   讨论热点：Office 文档质量、评论清理与文档完整性。  
   状态：OPEN，2026-09-11 更新。  
   https://github.com/anthropics/skills/pull/1734

5. **#514 新增 document-typography skill**  
   功能：对 AI 生成文档做排版质控，处理孤词换行、孤行段落、编号错位等常见问题。  
   讨论热点：AI 生成文档的专业排版与可交付质量。  
   状态：OPEN，2026-03-13 更新。  
   https://github.com/anthropics/skills/pull/514

6. **#1615 新增 scnet-hpc skill**  
   功能：通过 profile 化 SSH 与 Slurm 工作流操作 SCNet HPC 集群。  
   讨论热点：垂直科研/HPC 场景、集群发现与作业生成。  
   状态：OPEN，2026-08-24 更新。  
   https://github.com/anthropics/skills/pull/1615

7. **#538 修复 PDF skill 文件引用大小写**  
   功能：修正 `SKILL.md` 中 `REFERENCE.md`、`FORMS.md` 等大小写错误，避免在大小写敏感系统上失效。  
   讨论热点：跨平台文件引用、Linux/macOS 兼容性。  
   状态：OPEN，2026-04-29 更新。  
   https://github.com/anthropics/skills/pull/538

8. **#525 新增 Pyxel 复古游戏开发 skill**  
   功能：指导 Claude 创建、调试、验证 Python 复古游戏，支持确定性无头运行与逐帧检查。  
   讨论热点：游戏开发、可验证生成、状态检查。  
   状态：OPEN，2026-09-15 更新。  
   https://github.com/anthropics/skills/pull/525

## 2. 社区需求趋势

- **安全与信任边界**：最热 Issue #492 关注社区 Skill 使用 `anthropic/` 命名空间冒充官方 Skill，社区期待官方命名空间隔离、权限边界与签名/认证机制。  
  https://github.com/anthropics/skills/issues/492

- **组织内共享与分发**：Issue #228 希望 Claude.ai 支持组织级 Skill 共享库或分享链接，减少手动上传 `.skill` 文件的低效流程。  
  https://github.com/anthropics/skills/issues/228

- **评估与触发可靠性**：Issue #556 指出 `run_eval.py` 触发率为 0%，#1487 则暴露 `claude-api` 单次注入约 156k tokens。社区需要可靠的 Skill 触发测试、评估指标和上下文预算控制。

---

# Claude Code 社区动态日报（2026-09-16）

数据来源：github.com/anthropics/claude-code

---

## 一、今日速览

今日社区的主要动向有两条主线：一是 **v2.1.273 为 LLM 网关新增了一组请求元数据 Header**，标志着 Claude Code 在企业网关/代理场景下的可观测性建设继续推进；二是 **Windows 平台问题集中爆发**，Cowork 本地设备桥接修复失效、Atlassian Rovo MCP 组件渲染异常等多个回归问题同日更新，而一个已有近 190 条评论的 Windows 桌面重启缺陷仍处于僵持状态。此外，过去 24 小时内大量 8 月初提交的 Issue 被以 `stale` 标签批量关闭，社区对自动清理机制的讨论值得留意。

---

## 二、版本发布

### v2.1.273
核心更新是**面向 LLM 网关的请求提示 Header 扩展**，为网关侧做请求分类、成本归因和上下文压缩追踪提供了数据基础：

- 新增请求头：`x-claude-code-request-class`、`x-claude-code-agent-type`、`x-claude-code-prev-tool-durations`、`x-claude-code-compaction`、`x-claude-code-context-compacted`
- 需通过环境变量 `CLAUDE_CODE_GATEWAY_HINT_HEADERS=1` 显式开启
- 同时新增了一类通知（release note 内容在此处截断）

**解读**：`agent-type` 与 `request-class` 的组合，意味着企业可以在网关层区分主 Agent / 子 Agent / 后台任务流量；`context-compacted` 类 Header 则让网关能感知上下文压缩事件，对做成本分摊、延迟归因的团队价值较大。默认关闭说明 Anthropic 对隐私与额外开销保持谨慎。

### v2.1.272
仅包含「Bug 修复与可靠性改进」，无详细说明。

---

## 三、社区热点 Issues

> 说明：过去 24 小时内更新的 50 条 Issue 中，绝大多数为 8 月初提交、当日被 `stale` 批量关闭的历史需求。以下筛选出真正具有讨论价值或代表新问题的条目。

### 1. 桌面端 Windows 重启失败（悬而未决的最大热点）
- **#42776** · OPEN · 标签 `invalid` · 👍88 · 💬188
- 现象：孤儿进程持有文件锁，导致 Claude Code Desktop 在 Windows 上无法重新启动
- **为什么重要**：这是当前社区讨论量最高的 Issue，且被标记为 `invalid` 却持续活跃近半年（创建于 4 月 2 日），说明用户认为这是真实缺陷但标签判定存在争议。近 190 条评论反映出长期未被解决带来的情绪积累，是 Windows 桌面端信任度的核心隐患。
- 链接：https://github.com/anthropics/claude-code/issues/42776

### 2. Cowork 本地设备桥接在 Windows 上被 9/8 更新打断
- **#94266** · OPEN · `bug, platform:windows, area:cowork` · 👍0 · 💬1
- 现象：`device_bash` / `device_stage_files` 在 2026-09-08 更新后失效，多台机器上文件与网络访问被阻断
- **为什么重要**：典型的版本回归，且直接导致功能不可用（而非体验下降）。与上一条叠加，形成「Windows 平台可靠性」这一集中风险面。
- 链接：https://github.com/anthropics/claude-code/issues/94266

### 3. 自主化 Agent 架构提案（被关闭但值得重读）
- **#56913** · CLOSED · `enhancement, area:agents, stale` · 💬49
- 提案：以「分层 Opus 大脑 + Sonnet 执行工人 + 持久化状态」构建真正可长期运行的自治 Claude Code（流水线、ML 训练、构建自动化、监控、内容工作流）
- **为什么重要**：49 条评论显示这是社区对 Claude Code 未来形态最深入的讨论。虽然以 `stale` 关闭，但其提出的编排/持久状态/成本分层问题，与今日 v2.1.273 新增 `agent-type` Header 的方向形成呼应。
- 链接：https://github.com/anthropics/claude-code/issues/56913

### 4. claude_design MCP 的 OAuth 发现被 Cloudflare 挑战页打断
- **#72673** · CLOSED · `bug, has repro, platform:macos, area:auth, area:mcp`
- 现象：授权 `claude_design` MCP 时报 `Failed to parse JSON`，因为 AS metadata 端点返回了 Cloudflare HTML 挑战页，OAuth 窗口从未打开
- **为什么重要**：暴露了 MCP 授权链路对中间层（WAF/CDN）返回非 JSON 响应的容错缺失，是 MCP 生态接入第三方服务时的典型阻塞点。
- 链接：https://github.com/anthropics/claude-code/issues/72673

### 5. 自定义 API Key 提示硬编码 `sk-ant-` 前缀
- **#86983** · CLOSED · `bug, area:tui, area:auth, reproduced`
- 现象：无论实际值为何，检测提示都渲染固定的 `sk-ant-` 前缀
- **为什么重要**：对使用自建网关、第三方兼容端点或自定义 Key 格式的用户造成误导，属于典型的「假设 Anthropic 官方形态」的硬编码问题。
- 链接：https://github.com/anthropics/claude-code/issues/86983

### 6. Atlassian Rovo MCP 组件渲染过亮
- **#93369** · OPEN · `bug, regression, area:mcp, area:ui, area:desktop`
- 现象：Jira 搜索结果等 MCP Widget 在 Windows 桌面端渲染异常明亮，「昨天还正常」
- **为什么重要**：MCP Widget 是 Claude Code 从「命令行工具」向「富交互客户端」演进的关键，样式回归会直接影响企业用户在 IDE/桌面场景下的可用性。
- 链接：https://github.com/anthropics/claude-code/issues/93369

### 7. `persistHookOutput` 10K 阈值需要可配置
- **#84022** · CLOSED · `area:hooks`
- 现象：自 v2.1.89 引入的 10,000 字符硬编码阈值，迫使长期记忆类插件把 SessionStart 输出拆成 N 条 hook 命令来绕开限制
- **为什么重要**：Hooks 是社区扩展 Claude Code 的主要入口，硬编码上限直接限制了插件架构设计，这类「应可配置」的诉求在 Issue 列表中反复出现。
- 链接：https://github.com/anthropics/claude-code/issues/84022

### 8. 子 Agent 扇出成本与 Workflow 脚本能力缺口
- **#83873** · CLOSED · `area:agents`
- 提案：为 Workflow 脚本增加 shell 执行原语，用于确定性操作
- **为什么重要**：作者基于一次真实的 instrumented workflow 运行，从 `subagents/workflows/<runId>/agent-*.jsonl` 中汇总 usage 计算成本——这是社区开始**量化多 Agent 成本**的标志性案例。
- 链接：https://github.com/anthropics/claude-code/issues/83873

### 9. VS Code 扩展未捕获集成终端选中内容
- **#86683** · CLOSED · `enhancement, area:ide, platform:vscode` · 👍1
- 现象：在集成终端面板中选中报错/命令输出，不会被纳入 `ide_selection` 上下文，仅编辑器标签页生效
- **为什么重要**：调试场景下「复制报错进对话」是最高频操作之一，缺失该能力让 IDE 集成的上下文注入不完整。
- 链接：https://github.com/anthropics/claude-code/issues/86683

### 10. 远程控制需要「无会话机器」的冷启动能力
- **#83912** · CLOSED · `area:core`
- 提案：「My Devices」支持对一台当前没有任何会话运行的机器发起 Remote Control 会话
- **为什么重要**：现有的先有会话、才能远控的循环依赖，实质限制了「从手机随时唤起家中/办公机上的 Claude Code」这一核心使用场景。
- 链接：https://github.com/anthropics/claude-code/issues/83912

**其他值得扫一眼的条目**
- **#84192** 用纯 Rust 重写以消除 CPU 尖峰与终端闪烁（社区对 TUI 性能的极端表达）
- **#84047** Web UI 中显示每个运行中 Agent 的模型与 effort 级别
- **#83988** 桌面端窗口 1 秒出现、却空白长达 117 秒且无进度提示
- **#86780** 权限确认支持 `y` / `n` 而不仅是 `1` / `2`（Linux 用户习惯）
- **#84532** Apps Gateway 使用容器服务账号凭据做 Google Group OIDC 查询

---

## 四、重要 PR 进展

> **数据说明**：过去 24 小时内更新的 Pull Request 仅有 **1 条**，无法按「10 个重要 PR」的口径展开。以下为该 PR 详情，并附同期 Issue 中反映的合并/关闭信号作为补充。

### #94594 · CLOSED · `diff` mod 的 Git 调用时机修正
- 作者：@poteat ｜ 提交并关闭于 2026-09-15
- **内容**：`mods/diff` 原本在 `session.start` 钩子中固定仓库状态——执行一次 `git rev-parse`，再加上覆盖整个工作树的 `git status --porcelain -z --untracked-files=all`，且两者均被 `await`。由于引擎会阻塞首个 prompt 直到 `session.start` 完成，在超大仓库中会造成明显的启动延迟。
- **修复方向**：改为「在内置面板本应运行 Git 的时机才运行，绝不在会话启动时运行」。
- **为什么重要**：这属于**启动路径上的性能优化**，与社区长期抱怨的 TUI 卡顿、桌面端空窗期问题（#83988、#84192）指向同一根源——初始化阶段做了过多同步 I/O。
- 链接：https://github.com/anthropics/claude-code/pull/94594

**补充观察**：今日大量 Issue 集中从 OPEN 转为 CLOSED（多为 `stale` 自动关闭，少数为 `invalid`），但数据源中未体现对应的修复 PR，说明这批关闭主要来自清理策略而非实际交付。

---

## 五、功能需求趋势

从今日 50 条 Issue 的标签分布与内容看，社区关注方向高度集中：

| 方向 | 代表 Issue | 趋势判断 |
|---|---|---|
| **Windows / 桌面端可靠性** | #42776、#94266、#93369、#83988 | 当前**最突出**的痛点区，回归问题密集，用户对「更新后功能失效」容忍度快速下降 |
| **Agent 编排与自治化** | #56913、#83873、#84047 | 从「结对编程」转向「长期运行编排器」的诉求明确，成本分层、子 Agent 可见性、Workflow 原语是三个具体抓手 |
| **IDE 集成深化** | #86683、#86658 | 需求从「能用」转向「上下文注入无死角 + 交互细节对齐」（终端选区、代码块一键复制） |
| **MCP 生态健壮性** | #72673、#86705、#83894 | 集中在三处：OAuth 对非 JSON 响应的容错、连接器参数透传缺失、需要用户交互的工具在 Routines 中静默失败 |
| **TUI / UX 细节打磨** | #86669、#86780、#84030、#83903 | 主题中途切换、y/n 应答、side-chat 合并、prompt suggestion 可引导——属于日常高频交互层 |
| **企业认证与网关** | #84532、#83870 | OIDC 凭据来源、组织级策略（CVP）覆盖范围，反映企业部署正在规模化 |
| **Hooks / 可配置性** | #84022、#83907 | 反对硬编码阈值，要求按仓库/通道粒度配置 |
| **性能** | #84192、#83988 | 表达激烈但方向一致：启动耗时、CPU 空转、终端闪烁 |

---

## 六、开发者关注点

**1. 平台一致性债务正在累积**
Windows 同时出现在最高热度 Issue（#42776）和最新回归 Issue（#94266、#93369）中。用户的措辞已从「建议」转向「功能被阻断」，这是信任度下降的信号。同时桌面端、TUI、IDE 扩展三套界面下的行为差异（如代码块复制、选区上下文）也在持续制造不一致体验。

**2. 「硬编码假设」是高频摩擦源**
`sk-ant-` 前缀（#86983）、10K hook 输出阈值（#84022）、`session.start` 中的全量 git status（#94594）——三者本质相同：代码假设了一个特定的 Key 格式、输出规模或仓库体积。`has repro` / `reproduced` 标签频繁出现，说明这类问题容易复现且用户定位成本低，适合作为快速修复批次。

**3

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 · 2026-09-16

---

## 一、今日速览

今日 Gemini CLI 正式发布 **v0.60.0 稳定版**，同时推进 v0.61.0 预览/夜间构建。社区侧高度聚焦于 **Agent 可靠性**：通用子代理挂起、MAX_TURNS 被误报为成功、Shell 执行卡死等 P1 问题持续获得高热度讨论。PR 端则以核心稳定性修复为主，涵盖 UI 渲染越界、PTY 资源泄漏、OAuth 凭证刷新等关键缺陷。

---

## 二、版本发布

| 版本 | 类型 | 要点 |
|---|---|---|
| **v0.60.0** | 稳定版 | 修复 `web fetch` 工具的目标校验与连接路由；在 MCP OAuth 流程中强制执行 RFC 9207 issuer 识别 |
| **v0.61.0-preview.0** | 预览版 | 包含 v0.60.0-preview.0 changelog 与 v0.59 changelog 汇总 |
| **v0.61.0-nightly.20260915.g9c1b0a610** | 夜间构建 | 例行自动化版本推进 |

- v0.60.0: https://github.com/google-gemini/gemini-cli/releases
- 相关 Changelog PR: [#29345](https://github.com/google-gemini/gemini-cli/pull/29345) / [#29344](https://github.com/google-gemini/gemini-cli/pull/29344)

---

## 三、社区热点 Issues（Top 10）

1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) [P1] 子代理 MAX_TURNS 中断被误报为 GOAL 成功** — 评论 13 条，本周最热。`codebase_investigator` 在未完成任何分析、触达最大回合限制后仍返回 `status: "success"`，掩盖了真实的执行中断。这直接影响 Agent 结果的可信度，属于「静默失败」类严重缺陷。

2. **[#19873](https://github.com/google-gemini/gemini-cli/issues/19873) [P2] 零依赖 OS 沙箱 + 执行后意图路由** — 评论 9 条。核心思路：Gemini 3 原生擅长以 bash 方式链式调用 `grep`/`sed`/`awk`，希望通过沙箱化释放这一能力而不牺牲安全性，是架构级增强方向。

3. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) [P1] 通用代理（generalist agent）永久挂起** — 👍8，社区共鸣最强。连创建文件夹这类简单操作都会挂起，用户曾等待一小时；禁用子代理委派可绕过。是当前用户体验的最大阻塞点之一。

4. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) [P2] 评估 AST 感知的文件读取、搜索与代码库映射** — 评论 7 条。EPIC 级调研，目标是用 AST 精确识别方法边界、减少误读与 token 噪音，属于下一代代码导航基础设施。

5. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) [P2] Gemini 主动使用 skills / sub-agents 的比例过低** — 评论 6 条。用户反馈即使存在 "gradle"、"git" 等自定义技能，模型也几乎不会主动调用，凸显 Agent 自主性调优的迫切性。

6. **[#26525](https://github.com/google-gemini/gemini-cli/issues/26525) [P2] Auto Memory 需确定性脱敏并降低日志量** — 评论 5 条。目前敏感信息在进入模型上下文**之后**才被要求脱敏，且技能内容可能被写入日志，存在隐私风险。

7. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) [P1] Shell 命令执行完毕后卡在 "Waiting input"** — 👍3。命令早已结束却仍显示等待输入，属于高频复现的终端交互缺陷。

8. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) [P1] Wayland 环境下 browser 子代理失败** — Linux 桌面用户的核心阻塞，与浏览器代理的跨平台适配相关。

9. **[#22267](https://github.com/google-gemini/gemini-cli/issues/22267) [P2] Browser Agent 忽略 settings.json 覆盖（如 maxTurns）** — `AgentRegistry` 虽能正确合并配置，但浏览器代理完全无视全局/项目级配置，破坏用户配置预期。

10. **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246) [P2] 工具数量超过 128 个时触发 400 错误** — 随着 MCP 工具生态膨胀，工具作用域裁剪（tool scoping）成为必须解决的问题。

> 其他值得关注：[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) Auto Memory 无限重试低信号会话 / [#22672](https://github.com/google-gemini/gemini-cli/issues/22672) 代理应主动阻止破坏性命令 / [#21335](https://github.com/google-gemini/gemini-cli/issues/21335) `/compress` 在会话恢复后不持久。

---

## 四、重要 PR 进展（Top 10）

1. **[#29347](https://github.com/google-gemini/gemini-cli/pull/29347) [P1] 修复边框渲染中的负维度崩溃** — 对 `renderBorder` 及字符串重复逻辑加防，避免 `RangeError: Invalid count value: -1`，并对 `ToolConfirmationMessage`、`DiffRenderer` 等组件做防御性钳制。

2. **[#29339](https://github.com/google-gemini/gemini-cli/pull/29339) [P1] OAuth 刷新令牌保留与凭证删除幂等化** — 修复 GH-21691，解决刷新后 `refresh_token` 丢失导致的「重新认证死循环」。

3. **[#29335](https://github.com/google-gemini/gemini-cli/pull/29335) [P1] 确保对象展开保留 AgentLoopContext 属性** — 修复 `Config` 类原型 getter 在对象展开时属性丢失的问题，防止 Agent 循环上下文断层。

4. **[#29343](https://github.com/google-gemini/gemini-cli/pull/29343) 抑制请求取消时的未捕获 AbortError 日志** — 修复 Node 23+ 下取消查询/流时由 `node-fetch` 事件监听器抛出的 `AbortError` 导致的硬崩溃。

5. **[#29340](https://github.com/google-gemini/gemini-cli/pull/29340) 改进 PTY 文件描述符清理与执行生命周期管理** — POSIX 平台下确保 PTY 会话与后台 Shell 执行结束时完整释放资源，缓解长期运行后的 fd 泄漏。

6. **[#29342](https://github.com/google-gemini/gemini-cli/pull/29342) [P2] 避免嵌套的输入历史状态更新** — 重构 `useInputHistoryStore`，规避 React StrictMode 双调用引发的问题（Closes #29313）。

7. **[#29333](https://github.com/google-gemini/gemini-cli/pull/29333) [P2] 校验约定发现策略目录的权限** — 企业安全方向：原 `filterSecurePolicyDirectories` 仅检查系统策略目录，现扩展至用户目录与工作区目录。

8. **[#29341](https://github.com/google-gemini/gemini-cli/pull/29341) [P1] MCP 工具调用标题格式化为结构化签名** — 统一 ACP payload 与核心工具接口中 MCP/已发现工具的表示，隔离命令与解释说明。

9. **[#29304](https://github.com/google-gemini/gemini-cli/pull/29304) 截断时避免拆分 UTF-16 代理对** — 修复 `sanitizeForDisplay` 在 emoji 边界截断产生孤立代理字符的问题。

10. **[#29242](https://github.com/google-gemini/gemini-cli/pull/29242) [P2] 修正 401 子串误判为认证错误** — 原逻辑 `message.includes('401')` 会命中端口号 `4012`、行号等，错误触发重新认证/登出流程。

> 依赖维护：[#29137](https://github.com/google-gemini/gemini-cli/pull/29137) npm 依赖组 77 项升级（含 `simple-git`、`@modelcontextprotocol/sdk`）。

---

## 五、功能需求趋势

从本批 50 条 Issue 提炼，社区关注方向集中在以下六类：

| 方向 | 代表 Issue | 说明 |
|---|---|---|
| **Agent / 子代理可靠性** | #22323、#21409、#21968 | 挂起、回合限制误报、技能与子代理不被主动调用，是当前最高优先级主线 |
| **安全与沙箱** | #19873、#26525、#22672、#29333 | 从 OS 级沙箱、确定性脱敏到破坏性命令拦截，安全边界持续加固 |
| **代码库理解（AST / 上下文效率）** | #22745、#22746、#19561 | AST 感知读取与「外科手术式」token 节省，目标是降低基线 token 与误读 |
| **浏览器代理（Browser Agent）** | #22232、#21983、#22267 | 跨平台（Wayland）、会话锁恢复、配置覆盖生效 |
| **记忆与上下文持久化** | #26522、#26523、#26516、#21335 | Auto Memory 质量、`/compress` 持久化、会话恢复 |
| **工具生态扩展性** | #24246 | 工具数量突破 128 后的 400 错误，需智能裁剪工具作用域 |

此外，**平台/UI 体验**（#21924 终端 resize 闪烁、#22466 `\n` 转义、#22465 vite 交互式提示卡死）仍是稳定的长尾需求池。

---

## 六、开发者关注点

1. **「静默失败」比崩溃更可怕**：#22323 中 Agent 明明被回合上限截断却报告成功，开发者最需要的是**失败状态的诚实上报**，否则上层自动化流程会基于错误信号继续执行。

2. **挂起类问题占据体验投诉榜首**：通用代理挂起（#21409，等待一小时）、Shell 执行完成后卡在 "Waiting input"（#25166）、vite 交互提示卡死（#22465）——三者共同指向**子进程/交互式终端的生命周期管理**缺陷，与今日 PR #29340（PTY fd 清理）方向一致。

3. **Agent 自主性调优呼声高**：模型不主动调用 skills 与 sub-agents（#21968），需要更明确的触发策略或提示层设计，而非依赖用户显式指令。

4. **跨平台稳定性仍是痛点**：Wayland 浏览器代理失败（#21983）、Node 23+ 的 AbortError 崩溃（#29343），说明新运行时与 Linux 桌面环境适配需持续投入。

5. **凭证与认证流程脆弱**：OAuth refresh token 丢失导致重认证死循环（#29339 对应 #21691），叠加 `401` 子串误判（#29242），二者共同构成认证链路的可靠性风险。

6. **安全默认值诉求上升**：从 Auto Memory 脱敏时序（#26525）到策略目录权限校验（#29333），开发者期望**安全机制前置**，而非事后补救。

---

*数据来源：github.com/google-gemini/gemini-cli ｜ 统计窗口：2026-09

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报
**日期：2026-09-16** | 数据来源：github.com/github/copilot-cli

---

## 1. 今日速览

今日 Copilot CLI 连发三个补丁版本（v1.0.84-7/8/9），核心围绕 **上下文管理开关、会话历史扫描性能、Claude 模型 thinking 行为修复** 展开，其中 v1.0.84-9 明确以“扫描更快但线程与内存占用上升”为代价换取大历史会话体验。Issue 侧热度集中在**长会话/恢复场景的 OOM 崩溃**与**子代理工作流延迟**，同时两个高赞长期需求（Vim 模式、VS Code Chat 集成）在昨日被关闭，标志性意义较大。过去 24 小时无 PR 更新。

---

## 2. 版本发布

过去 24 小时内共发布 3 个版本：

### v1.0.84-9
- **Added**：新增 `/settings` 选项，可选择性为 agent 与 subagent 启用**上下文管理工具**。
- **Improved**：大幅降低大型本地会话历史的元数据扫描时间，代价是线程数与内存占用上升（这一点与当前社区 OOM 反馈直接相关，值得关注）。
- **Fixed**：`End` 与 `Ctrl+E` 现在会将光标移动到**折行后的真实行尾**，修复长命令编辑错位问题。

### v1.0.84-8
- **Added**：`transcriptView` 设为 `"concise"` 时，将工具活动聚合为**可展开的工作摘要**，降低长会话的视觉噪音。
- **Improved**：支持从 `/factories` 对话框**暂停与恢复 Agent Factory 运行**。
- **Fixed**：登录、切换账号、登出后模型列表现在会正确刷新。

### v1.0.84-7
- **Fixed**：修正发送给被判定为 `adaptive-only` 的 Claude 模型的 thinking 参数——保持 adaptive 而不再报错；关闭 thinking 时改为降低 reasoning effort，并将其上限锁定为 high。
- **Fixed**：当 `/clear` 关闭会话时，正确触发 `sessionEnd` 钩子。

> 关联提示：v1.0.84-8 曾引入 macOS Terminal 交互键盘无响应问题（#4855），该 Issue 已于昨日关闭，建议仍使用 -8 的用户升级至 -9。

---

## 3. 社区热点 Issues（10 条）

1. **#4664 [OPEN] 恢复长期会话时 JavaScript heap OOM 崩溃**（8 条评论）
   会话在 resume 阶段、用户尚未开始工作前即因 V8 堆耗尽崩溃，堆达到约 4GB 上限。这是当前最集中的稳定性问题之一，与今日 v1.0.84-9 的内存权衡高度相关。
   https://github.com/github/copilot-cli/issues/4664

2. **#13 [CLOSED] CLI 应支持 vi/vim 输入模式**（13 条评论，👍76）
   社区呼声最高的交互体验需求：为模态编辑器用户提供键驱导航与编辑。历时一年后关闭，是本项目交互能力演进的一个标志性节点。
   https://github.com/github/copilot-cli/issues/13

3. **#54 [CLOSED] 与 VS Code Copilot Chat 能力全面打通**（13 条评论，👍20）
   诉求是让 CLI 成为已有 VS Code Copilot Chat 配置的批处理/终端前端，复用项目上下文与设置。关闭意味着该方向的整合路径已明确或有替代方案。
   https://github.com/github/copilot-cli/issues/54

4. **#4725 [OPEN] Linux 上频繁 JavaScript heap out of memory**（6 条评论）
   每几分钟即触发一次 Mark-Compact 失败，属高频阻断型崩溃，且平台集中在 Linux，影响 CI/容器场景。
   https://github.com/github/copilot-cli/issues/4725

5. **#4849 [OPEN] 降低 subagent 工作流的延迟与评审循环开销**（5 条评论）
   指出子代理驱动的实现与评审流程“每一轮往返动辄数分钟”，小型改动也变得昂贵。随着多代理能力成为卖点，性能已成为采纳瓶颈。
   https://github.com/github/copilot-cli/issues/4849

6. **#4251 [OPEN] 1.0.74 起恢复大型会话的 OOM 回归（内存约为 1.0.73 的 3–4 倍）**（4 条评论）
   通过同机同会话的 A/B 对比将回归精确定位到 1.0.74，并附带 RSS 数据，是质量最高的性能回归报告之一。
   https://github.com/github/copilot-cli/issues/4251

7. **#4699 [OPEN] 长 `--resume` 会话 OOM，且崩溃转储被写入用户 cwd**（4 条评论，👍5）
   除崩溃本身外，Node 诊断报告污染当前工作目录，对仓库整洁与 CI 环境造成二次影响，属易修复但影响面广的问题。
   https://github.com/github/copilot-cli/issues/4699

8. **#4807 [OPEN] 空闲 CLI 进入 `FileWatch` 事件风暴，占用 2 个 CPU 核心并写下 33GB 日志**（2 条评论）
   进程在无操作状态下持续 35 小时以上高 CPU 运行，日志膨胀至 33GB，指向文件监听与调试日志的失控路径，资源风险极高。
   https://github.com/github/copilot-cli/issues/4807

9. **#1148 [OPEN] Windows 上 Copilot CLI 将所有编辑文件改为 CRLF**（7 条评论，👍8）
   跨平台换行符破坏问题，对以 LF 为规范的仓库（如 vcpkg 生态）会污染 diff、影响提交评审，属长期未决的平台兼容痛点。
   https://github.com/github/copilot-cli/issues/1148

10. **#2734 [OPEN] 支持插件自动更新（全部或按插件）**（3 条评论，👍13）
    插件市场更新目前需手动检查与应用，用户易长期运行带 bug 的旧版本。这是插件生态成熟度最直接的诉求。
    https://github.com/github/copilot-cli/issues/2734

> 其他值得留意：#4438（`disable-model-invocation: true` 导致 skill 完全不可调用）、#4780（压缩阶段 OOM 使会话永久无法恢复）、#4783（企业策略需为 CLI 沙箱单独划定 yolo 权限范围）、#4800/#4793（CIMD OAuth 回调用临时端口导致登录失败）、#4862/#4863（OTel span 缺失响应标识、SIGINT 后仍上报成功）。

---

## 4. 重要 PR 进展

**过去 24 小时内无 PR 更新（0 条）**，因此本期不列出 PR 条目。

结合现象判断：该仓库的外部 PR 流当前较为封闭，功能与修复主要通过版本发布通道直接交付（今日三个补丁版本即为佐证）。若需跟踪贡献方向，建议关注 Releases 变更日志与 Issues 中的 `triage` 标签状态流转。

---

## 5. 功能需求趋势

综合本期全部 Issues，社区关注方向可归纳为六条主线：

| 方向 | 代表 Issue | 核心诉求 |
|---|---|---|
| **长会话内存与上下文管理** | #4664 #4725 #4251 #4699 #4780 #4506 #4639 | OOM 崩溃、压缩失败、内存看门狗误触发；v1.0.84-9 的 `/settings` 上下文工具开关正是对该方向的回应 |
| **Agent / 子代理工作流** | #4849 #4850 #4438 #3954 | 降低启动与交接延迟、避免后台子代理假死、修复 skill 调用可达性与模型硬编码 |
| **交互与终端体验** | #13（已关闭）#4865 #4855 | Vim 键位、`transcriptView` 简洁视图、以聊天而非表单方式提问、光标与键盘输入正确性 |
| **IDE 与生态集成** |

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-09-16）

> 数据来源：github.com/MoonshotAI/kimi-cli  
> 统计范围：过去 24 小时更新

## 1. 今日速览

今日无新 Release、无 PR 更新，社区动态集中在 Issues。最值得关注的是付费用户报告配额异常消耗：`cache_read` 被每轮计费，而 `cache_creation` 始终为 0，疑似造成 >10x 放大。其余更新涉及 macOS 剪贴板兼容、Kimi Work 会话标题日期前缀，以及第三方项目 PicoClaw 接入需求。

## 2. 版本发布

过去 24 小时无新 Release。

## 3. 社区热点 Issues

> 今日仅有 4 条 Issue 更新，以下为全部条目；无法按 10 条筛选。

1. **#2626 [OPEN] 配额异常消耗：cache_read 每轮计费，cache_creation 始终为 0（>10x 放大）**  
   - 作者：@ahmadyaseen35-coder  
   - 创建：2026-08-29；更新：2026-09-15；评论：2；👍：0  
   - 为什么重要：年付订阅用户报告 5 小时配额窗口在轻度使用下数分钟内损失约 40%，怀疑缓存计费逻辑异常，可能造成显著成本放大。该问题

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 · 2026-09-16

数据来源：github.com/anomalyco/opencode

---

## 一、今日速览

今日无新版本发布，社区注意力集中在 **1.18.30 版本的严重回归**上：`SystemPrompt.environment` 抛出的 `TypeError: undefined is not an object (evaluating 'a.name')` 导致所有 prompt 直接崩溃，至少三个独立 Issue 在同时发酵，合计获得 50+ 👍。与此同时，长期高票需求（可点击链接、Plan Mode 自动切换）持续升温，配置与数据库 schema 不一致、输出 token 被静默截断等"隐性限制"类问题成为开发者新的不满焦点。

---

## 二、版本发布

过去 24 小时无新 Release。当前用户侧反馈主要围绕 **1.18.30** 的回归问题展开（详见下文 Issue 部分）。

---

## 三、社区热点 Issues（10 条）

**1. [#48645](https://github.com/anomalyco/opencode/issues/48645) — 1.18.30 回归：每条 prompt 都在 `SystemPrompt.environment` 崩溃**（8 评论 / 15 👍）
最严重的当日问题。升级到 1.18.30 后任意新会话的第一条消息即报 `Failed to send prompt. Unexpected server error`，1.18.18 正常。用户提供了明确的版本回退证据链，属于典型的阻断性回归。

**2. [#48372](https://github.com/anomalyco/opencode/issues/48372) — 同一崩溃的 TUI + `opencode run` 双路径复现**（6 评论 / 23 👍）
本日 👍 数最高的 Issue，明确覆盖 CLI 与 TUI 两条入口。与 #48645、#49158 构成同一根因的三重报告，说明影响面远超单一平台。

**3. [#49158](https://github.com/anomalyco/opencode/issues/49158) — 堆栈几乎完全一致的重复报告**（6 评论 / 16 👍）
带有 `chunk-y88jw4qv.js:50:13096` 的完整堆栈，可作为定位 `a.name` 空引用的直接线索。三个 Issue 同日报到，社区情绪偏急躁。

**4. [#29363](https://github.com/anomalyco/opencode/issues/29363) — `limit.output` 被静默限制在 32k**（20 评论 / 21 👍）
当日评论数最多的 Issue。即使用户把 `limit.output` 设为 384000（DeepSeek）或 128000（GPT/Claude），每步输出仍被硬编码截断在 32,000 token，唯一出口是实验性环境变量 `OPENCODE_EXPERIMENTAL_OUTPUT_TOKEN_MAX`。核心争议在于"静默截断 + 实验性开关"的组合对生产用户极不友好。

**5. [#1168](https://github.com/anomalyco/opencode/issues/1168) — 让链接可 Ctrl+左键点击打开**（12 评论 / 133 👍）
全场 👍 数最高的 Issue，从 2025-07 一直挂到现在。这是一个极低实现成本、极高感知收益的终端交互体验缺口，高票长期未落地本身也是社区关注点。

**6. [#7801](https://github.com/anomalyco/opencode/issues/7801) — Plan Mode 下 Question 工具应答后自动切 Build 模式**（12 评论 / 34 👍）
Plan Mode 与 Build Mode 的流转仍需人工干预，用户希望 Question 工具的确认动作能驱动模式自动切换。反映社区对"工作流状态机"体验的期待。

**7. [#45278](https://github.com/anomalyco/opencode/issues/45278) — 订阅续费被拒付，银行侧确认无异常**（19 评论 / 5 👍）
评论数第二高，属商业/支付链路问题。卡片连续三个月正常扣款后突然被拒，银行无风控拦截，影响付费用户留存，需与支付服务商联合排查。

**8. [#30611](https://github.com/anomalyco/opencode/issues/30611) — 瞬时网络错误直接中断会话，不进入重试**（10 评论 / 1 👍）
重试策略只把 `ECONNRESET` 视为可重试，其他瞬时传输故障被归类为硬错误。对移动网络/弱网环境用户影响显著。

**9. [#45989](https://github.com/anomalyco/opencode/issues/45989) — 触发限流后进入 3 秒无限重试且无日志**（9 评论）
UI 不显示真实退避/重置时间，后端也没有任何错误或网络事件日志，形成"黑盒死循环"。可观测性缺失是主要诟病点。

**10. [#35403](https://github.com/anomalyco/opencode/issues/35403) — 插件版本落后导致 `no such column: replacement_seq`**（6 评论 / 4 👍）
根因是共享 SQLite 中 `__drizzle_migrations` 只记录了 21 条迁移而 CLI 已应用 38 条，任何先打开数据库的运行时都会把 schema 推进，导致其他进程崩溃。属于多运行时共享存储的架构性风险（已有对应 PR，见下）。

> 其他值得留意：#49222（TUI 启动即占用 6.5–7GB RSS）、#42263（PDF 附件无大小上限 base64 全量驻留导致 OOM）、#48069（Bedrock GPT-6 Astra 读取图片后 400）、#35283（`reasoning` 字段的推理内容被丢弃）。

---

## 四、重要 PR 进展（10 条）

**1. [#49225](https://github.com/anomalyco/opencode/pull/49225) — schema 超前运行时快速失败**（OPEN）
直接修复 #35403 / #49177 / #38471：当共享 SQLite schema 版本高于当前运行时，主动 fail fast 而非静默崩溃。是解决"CLI / Desktop / 插件三方共享一个 db 文件"混乱的关键一步。

**2. [#44725](https://github.com/anomalyco/opencode/pull/44725) — v2 分支恢复 `OPENCODE_DISABLE_CLAUDE_CODE`**（OPEN）
v1 中该开关用于阻止 OpenCode 读取 `~/.claude` 的 prompt 与 skills，v2 只声明未实现。对在意配置隔离与隐私边界的用户是重要回归修复。

**3. [#49235](https://github.com/anomalyco/opencode/pull/49235) — 向 code mode 脚本暴露 `fetch`**（OPEN）
让 `execute` 工具运行的脚本可以调用 `globalThis.fetch`。基于 #49196 的宿主函数机制实现，未引入新运行时类型，扩展了脚本化工具的能力边界且保持实现轻量。

**4. [#49236](https://github.com/anomalyco/opencode/pull/49236) — 桌面端测试重心收缩至漏斗与性能**（OPEN）
删除 395 个测试文件中的 335 个（约 85%），保留全部 benchmark、时间线稳定性检查与 profiling 工具。这是一次颇具争议的测试策略调整，值得关注后续是否出现回归盲区。

**5. [#47607](https://github.com/anomalyco/opencode/pull/47607) — 优化 Levenshtein 距离计算并限制编辑锁**（OPEN）
把 `src/tool/edit.ts` 中 (n+1)×(m+1) 的全矩阵分配改为双行滚动数组，降低大文件编辑时的内存与时间开销。

**6. [#49185](https://github.com/anomalyco/opencode/pull/49185) — 修复连续拖拽文件只插入第一个 `@path`**（OPEN）
v2 输入框中第二次及以后的拖拽会被静默忽略，属于交互一致性 bug，修复成本低、体验收益直接。

**7. [#49111](https://github.com/anomalyco/opencode/pull/49111) — 时间线图片支持在附件浮层中预览**（已关闭）
支持点击/Enter/Space 打开 agent 消息与 Read 结果中的图片，并带缩放光标。属于渲染与可访问性层面的体验补强。

**8. [#48735](https://github.com/anomalyco/opencode/pull/48735) — 会话标题占位符与标签页文案统一**（已关闭）
未命名会话标题统一使用本地化的 "Session"，并同步父/子标题与删除弹窗，属国际化一致性清理。

**9. [#42812](https://github.com/anomalyco/opencode/pull/42812) — Go 订阅信用卡结账强制 3DS 验证**（已关闭）
针对生产环境欺诈团伙利用唯一 Stripe 客户与支付方式 ID 批量创建 Go 订阅的行为，要求新卡结账走 3D Secure；Alipay/UPI 路径不变。与今日 #45278 的拒付问题可能相关。

**10. [#42762](https://github.com/anomalyco/opencode/pull/42762) — 提升并发会话吞吐（refactor）**（已关闭）
基于 6 条真实 Session 历史构建确定性 benchmark，度量并发会话的完整值事件推断与吞吐表现，是性能方向的基础性工作。

> 另注：今日有大批 2026-08-15 创建、带 `automated-pr-cleanup` 标签的 PR 被集中关闭（#42819、#42809、#42808、#42807、#42796、#42789、#42786、#42777、#42761、#42751 等），提示维护者正在进行一轮存量 PR 清理，其中包含乐观提交、乐观会话创建、子文件夹浏览、流式传输诊断保留等有价值的改动，社区需关注是否会被重新提交。

---

## 五、功能需求趋势

从本期全部 Issue 中可提炼出四个清晰方向：

1. **工作流状态机与模式自动化** — Plan Mode / Build Mode 的自动切换（#7801）、达到 `finish_reason: "length"` 后自动续写（#17471），用户希望减少手动衔接。
2. **终端/编辑器级交互体验对齐** — 可点击链接（#1168，133 👍）、图片预览、附件浮层等，本质是把 TUI 体验向现代 IDE 靠拢。
3. **安全与合规工具链** — `/security-review` 扫描 diff 中的密钥与硬编码凭证（#41913）、PII/Secret 正则脱敏并在送模型前替换占位符（#3056），安全左移诉求开始成型。
4. **平台与生态扩展** — AARCH32/ARM32 支持（#44783，Termux armv7l / 树莓派 32 位）、远程 MCP OAuth 对 RFC 9728 `resource_metadata` 的正确处理（#44790）、以及第三方桌面应用（如 Lift）能否在用户自有登录下托管 `opencode serve` 的策略问题（#49207）。

---

## 六、开发者关注点

- **版本回归质量**：1.18.30 让所有 prompt 直接崩溃，且同日出现三份独立报告（#48645 / #48372 / #49158），说明发布前的基础冒烟覆盖存在明显缺口，用户开始自发整理"可用版本号"作为规避手段。
- **静默限制与隐式行为**：`limit.output` 被静默截断至 32k（#29363）、`reasoning` 字段被丢弃（#35283）、限流后无日志无限重试（#45989）——共同指向"系统替用户做决定但不告知"的问题模式。
- **多运行时共享状态的脆弱性**：CLI、Desktop、插件共用一个 SQLite，迁移版本漂移会导致 `no such column` 类崩溃（#35403、#49177、#38471），社区期待更严格的 schema 版本协商机制。
- **资源占用与内存安全**：TUI 空项目启动即占 6.5–7GB RSS（#49222）、PDF 附件无上限 base64 全量驻留并每轮重编码（#42263），内存问题已从"性能优化"升级为"可用性阻塞"。
- **弱网与容错策略**：重试白名单过窄（#30611）与限流退避黑盒（#45989）叠加，使网络波动场景下的会话稳定性成为高频痛点。
- **商业化链路的信任成本**：支付被拒（#45278）配合 PR #42812 的 3DS 反欺诈变更，提示计费与风控策略调整需要更透明的用户沟通。

---

*本日报由 GitHub 数据自动整理，链接均指向 anomalyco/opencode 仓库。*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-09-16）

---

## 1. 今日速览

过去 24 小时社区焦点集中在**稳定性与宿主集成**上：TUI 因 React #185 静默崩溃（#11500，15 条评论）持续发酵，ACP/daemon 通道在异常输入下被撕裂并导致全会话 404（#11908）成为新的 P1 风险。同时，围绕 Web Shell / Desktop 的**设置未生效**问题（主题、语言）与 **MiniMax / OpenAI Responses 等第三方网关的工具参数序列化兼容性**，已分别有对应 PR（#11961、#11842）跟进修复。版本侧发布 `cua-driver-rs v0.20.9`，为 CUA Driver 补齐 macOS 签名公证与多平台预编译二进制。

---

## 2. 版本发布

### cua-driver-rs v0.20.9
Qwen CUA Driver 预编译二进制，以 vendored 形式置于 `packages/cua-driver`。

- **macOS**：已签名 + 公证的 universal binary，附 `QwenCuaDriver.app`
- **Linux**：未签名（x86_64 + arm64，glibc 2.31 下限）
- **Windows**：未签名 UIAccess worker + 原生 SDK payload（x86_64 + arm64）

> 关注点：Windows/Linux 产物仍为未签名，与 #11952 中「桌面端是否必须代码签名才能发布」的讨论直接相关。

---

## 3. 社区热点 Issues（Top 10）

### ① [#11500](https://github.com/QwenLM/qwen-code/issues/11500) — TUI 静默退出（未捕获 React #185）｜P1 · 15 评论
多个后台 subagent 相继完成时，交互式 TUI 抛出 **Minified React error #185（Maximum update depth exceeded）** 后直接掉回 shell，无任何错误渲染；恢复会话时 CLI 提示 "Previous session appears…"。根因指向 Ink `useBoxMetrics` 的 layout-listener setState 循环。**这是本轮评论最多的 Issue，且属于"崩溃无提示"这一类最伤体验的缺陷**，后续已有加固 PR/Issue（#11858）。

### ② [#11908](https://github.com/QwenLM/qwen-code/issues/11908) — 超大 `available_commands_update` 撕裂 ACP 通道｜P1
会话启动通知超过 `MAX_JSON_NODES`(10 000) 后，ACP bridge 判定为 `ndjson_invalid_message`，fail-closed 拆除通道、`SIGKILL` 子进程并丢弃会话，**此后所有请求返回 404 `No session with id`**。一次超限输入永久废掉整个会话，影响 `qwen serve` / ACP 全链路，是 daemon 侧最值得优先处理的问题。

### ③ [#11895](https://github.com/QwenLM/qwen-code/issues/11895) — `/review` 维度 agent 读错工作树｜P1
同仓库 PR 评审时，`/review` 通过 `working_dir: "<worktreePath>"` 约束 agent，但该约束只对**相对路径**生效；agent brief 只给了 diff 的绝对路径，导致维度 agent读取主 checkout 而非 PR worktree。**直接影响 AI 代码评审结论的正确性**，属于自研工作流的核心可信度问题。

### ④ [#11834](https://github.com/QwenLM/qwen-code/issues/11834) — MiniMax 报 400「function parameters is empty」｜P1
用户输入「你好」即触发 `API Error: 400 invalid params, function parameters is empty (2013)`（0.23.3）。与 #11956 同源：无参数工具在 OpenAI 兼容序列化层被写成 `null`，严格网关直接拒绝整条请求。已由 PR [#11842](https://github.com/QwenLM/qwen-code/pull/11842) 提供修复方向。

### ⑤ [#11887](https://github.com/QwenLM/qwen-code/issues/11887) — `--acp` 忽略审批模式，工具自动执行｜P2（

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*