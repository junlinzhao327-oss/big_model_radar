# AI CLI 工具社区动态日报 2026-08-08

> 生成时间: 2026-08-07 22:59 UTC | 覆盖工具: 7 个

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

**数据窗口：2026-08-08** ｜ 覆盖：Claude Code / OpenAI Codex / Gemini CLI / GitHub Copilot CLI / Kimi Code / OpenCode / Qwen Code

---

## 1. 生态全景

AI CLI 工具已从"单点对话助手"全面转向"可编程、可托管、可扩展的 Agent 运行平台"。当日市场呈三大特征：**一是版本迭代极快**，Codex（正式版 + 2 alpha）、Copilot（3 补丁）、Qwen（正式 + nightly）在 24 小时内密集发版；**二是跨工具共性痛点高度重合**——会话恢复、权限边界、MCP 稳定性、Windows 兼容性在几乎每个仓库的 Issues 中同时出现；**三是企业级能力成为新增量**，self-hosted runner、企业沙箱策略、多模型接入等基础设施功能陆续落地。整体上，工具间的竞争正从模型能力比拼转向工程成熟度与生态完整性的较量。

---

## 2. 各工具活跃度对比

| 工具 | 今日 Issues | 今日 PRs | Releases | 活跃定性 |
|---|---|---|---|---|
| **Claude Code** | 10 条精选（#13354 达 191👍） | 3 条 | v2.1.224（新增 self-hosted runner、archive 插件源） | 高赞集中，企业功能发布 |
| **OpenAI Codex** | 10 条精选（1 条新提交） | 10 条 | rust-v0.147.0 正式版 + 2 个 alpha | 高频迭代，架构层 PR 密集 |
| **Gemini CLI** | 10 条精选（含 2 个 P1 严重 bug） | 1 条 | 3 个维护版（nightly/preview.2/patch） | 讨论深入但节奏平稳 |
| **GitHub Copilot CLI** | 30 条更新（8 条新增） | 0 | v1.0.79-6 / -7 / -8 | 回归问题集中爆发 |
| **Kimi Code** | 2 条（1 个数据损坏级 bug） | 3 条 | 无 | 低活跃但问题严重 |
| **OpenCode** | 10 条精选（数据截断） | 未披露 | v1.18.15（纯 bugfix） | 服务争议主导讨论 |
| **Qwen Code** | 39 条更新 | 50 条更新（10 条精选） | v0.21.7 正式版 + nightly | 当日最活跃仓库 |

---

## 3. 共同关注的功能方向

### 3.1 会话生命周期管理（呼声最强）
| 工具 | 具体诉求 |
|---|---|
| **Claude Code** | #13354 会话数上限后继续运行（191👍，全场最高）；#84625 后台任务被静默杀 |
| **OpenAI Codex** | #14599 全局 trust_level 避免重复审批（57👍） |
| **Qwen Code** | v0.21.7 移除 Goals 的 50 轮对话上限 |
| **Copilot CLI** | #4397 恢复会话时模型被静默重置；#4251 恢复大会话 OOM |
| **Gemini CLI** | #22323 子代理 MAX_TURNS 后目标状态被误报为成功 |

**结论**：长时间运行、断点续跑、后台任务可靠性是全体用户的基础刚需，工具间尚未形成统一解决方案。

### 3.2 权限控制与安全边界
| 工具 | 具体诉求 |
|---|---|
| **Kimi Code** | #2596 在 yolo 模式下误删工作区外数据；#2591 文件编辑破坏非 UTF-8 字节 |
| **Copilot CLI** | #4398 `allowed_directories` 配置被静默忽略 |
| **Gemini CLI** | #22093 禁用 agents 后仍被子代理自动调用 |
| **Qwen Code** | #8706 修复工作区信任边界（已提交 PR） |
| **Claude Code** | #70458 安全检查对无害内容误报 |

### 3.3 MCP 生态稳定性
- **Claude Code**：#70386 丢弃 `Mcp-Session-Id` 导致会话型 MCP 失败
- **OpenAI Codex**：#12491 子进程未回收致 1300+ 僵尸进程 / 37GB 内存泄漏
- **Copilot CLI**：#4392 认证后 MCP 客户端重建留下孤儿进程
- **Qwen Code**：#8550 SSE 服务器无响应导致 `qwen mcp list` 无限挂起

### 3.4 Windows / 终端兼容性
- **Codex**：Windows 沙箱提权失败（#10090）、Computer Use 崩溃（#37043）
- **Copilot CLI**：剪贴板静默失败（#3622）、OneDrive 权限循环（#1409）
- **Qwen Code**：中文输入拼音显示不清（#8625）、安装包 SHA 校验失败（#7118）
- **Gemini CLI**：Wayland 下 Browser 子代理失败（#21983）

### 3.5 插件 / 技能 / 多模型扩展
- **Claude Code**：新增 `archive` 插件源；社区关注插件安装的供应链安全（#84939）
- **Codex**：便携式 Agent 插件跨目录搜索；LiteLLM 自定义 provider 回归（#37425）
- **Copilot CLI**：skills 子文件夹需求（23👍）；`skill` 工具找不到有效技能（#4401）
- **Qwen Code**：接入 Kimi、小米 MiMo 三方提供商（#8368）
- **OpenCode**：用户呼吁加密货币支付（37👍），多提供商订阅模式下出现 401 故障（#38257，45 条评论）

---

## 4.

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截止 2026-08-08）

**数据源**：github.com/anthropics/skills（Top 50 PRs / Top 50 Issues 采样分析）

---

### 1. 热门 Skills 排行

以下 Skills 为当前社区讨论热度最高（按评论数/关注度排序）且尚未合并的核心 PR：

- **#1298 fix(skill-creator)：run_eval.py 触发率恒为 0% 的根因修复**
  - **功能**：修复 `run_eval.py` 因未将 eval artifact 安装为真实 skill、Windows 流读取错误、并行 worker 等问题，导致所有查询 recall=0% 的严重缺陷。
  - **讨论热点**：该问题直接导致 `run_loop.py` 和 `improve_description.py` 在错误的噪声上进行优化，是 `skill-creator` 生态中最致命的缺陷之一。
  - **状态**：OPEN（2026-06-23 更新）
  - https://github.com/anthropics/skills/pull/1298

- **#514 Add document-typography skill（文档排版质量控制）**
  - **功能**：检测 AI 生成文档中的孤词折行（1-6 个词溢出到下一行）、孤行标题（标题位于页底）以及编号不对齐等排版问题。
  - **讨论热点**：直击 Claude 生成文档的通病，社区认可度较高，具备通用跨格式价值。
  - **状态**：OPEN（2026-03-13 更新）
  - https://github.com/anthropics/skills/pull/514

- **#486 Add ODT skill（OpenDocument 文本创建与转换）**
  - **功能**：支持创建、填充、读取和转换 OpenDocument 格式（.odt/.ods），并能将 ODT 解析为 HTML。
  - **讨论热点**：弥补了官方 Skill 集合中缺失的 LibreOffice/ISO 标准格式支持，推动开源办公套件的互操作性。
  - **状态**：OPEN（2026-04-14 更新）
  - https://github.com/anthropics/skills/pull/486

- **#723 feat: add testing-patterns skill（全栈测试模式指南）**
  - **功能**：覆盖 Testing Trophy 测试哲学、单元测试、React 组件测试（Testing Library）、边界测试等完整测试栈。
  - **讨论热点**：社区对"如何让 Claude 生成高质量测试"的需求旺盛，普适性强，长期维护价值高。
  - **状态**：OPEN（2026-04-21 更新）
  - https://github.com/anthropics/skills/pull/723

- **#1367 feat(skills): add self-audit — 机械验证 + 四维推理质量门控（v1.3.0）**
  - **功能**：在交付前先进行机械文件验证，再按损坏严重程度对推理过程进行四维审查，通用性强，不依赖特定技术栈。
  - **讨论热点**：回应了社区对 AI 输出质量控制和"自检"机制的长期诉求，版本迭代频繁，方案成熟度较高。
  - **状态**：OPEN（2026-07-02 更新）
  - https://github.com/anthropics/skills/pull/1367

- **#1302 Add color-expert skill（色彩专家知识库）**
  - **功能**：内置 ISCC-NBS、Munsell、XKCD、RAL 等色彩命名系统，以及 OKLCH/OKLAB 等色彩空间适用场景对照表。
  - **讨论热点**：由知名开源作者 @meodai 提交，高度自包含，覆盖设计师与前端开发者的高频色彩查询需求。
  - **状态**：OPEN（2026-07-21 更新）
  - https://github.com/anthropics/skills/pull/1302

- **#525 Add pyxel skill（复古像素游戏开发）**
  - **功能**：基于作者自研的 pyxel-mcp 服务器，支持编写 → 运行捕获 → 检查 → 迭代的完整复古 8-bit 游戏开发工作流。
  - **讨论热点**：作为 MCP 与 Skills 结合的典型案例，作者持续活跃更新（2026-07-15），垂直领域穿透力强。
  - **状态**：OPEN（2026-07-15 更新）
  - https://github.com/anthropics/skills/pull/525

---

### 2. 社区需求趋势

- **开发工具链稳定性（最高优先级痛点）**
  - [#556](https://github.com/anthropics/skills/issues/556) 与 [#1169](https://github.com/anthropics/skills/issues/1169)：`run_eval.py` 在所有查询下 0% 触发率，导致 skill 描述优化流程完全失效。社区反复提交复现报告（10+ 独立复现），是当前最大的单点故障。
  - [#202](https://github.com/anthropics/skills/issues/202)：要求将 `skill-creator` 从"人类可读的教科书"重写为"可操作指令"，提升 token 效率。

- **安全与信任边界（高评论量，风险最高）**
  - [#492](https://github.com/anthropics/skills/issues/492)：社区技能被分发在 `anthropic/` 命名空间下，伪装成官方技能，形成信任边界漏洞。42 条评论表明该问题引发开发者警惕与治理讨论。

- **组织级共享与分发**
  - [#228](https://github.com/anthropics/skills/issues/228)：要求实现组织内技能库直连分发，替代 Slack/Teams 手动传输 .skill 文件的低效方案（👍 8 个）。
  - [#189](https://github.com/anthropics/skills/issues/189)：`document-skills` 与 `example-skills` 插件安装了重复内容，造成上下文窗口冗余（👍 9 个）。

- **上下文窗口与性能优化**
  - [#1487](https://github.com/anthropics/skills/issues/1487)：核心 `claude-api` 技能一次性注入约 156k tokens，直接耗尽上下文窗口。这暴露了技能"越强大越臃肿"的设计悖论，社区开始关注技能体积管控。

- **新领域技能提案（前沿方向）**
  - [#1329](https://github.com/anthropics/skills/issues/1329)（compact-memory）：用符号化记号压缩 agent 的长期记忆。
  - [#412](https://github.com/anthropics/skills/issues/412)（agent-governance）：AI 代理系统的策略执行、威胁检测与审计。
  - [#1385](https://github.com/anthropics/skills/issues/1385)（Reasoning Quality Gate Pipeline）：预任务校准 → 对抗性审查 → 交付验证的三阶段流水线。

---

###

---

# Claude Code 社区动态日报 — 2026-08-08

## 今日速览

Claude Code 发布 v2.1.224，引入 `claude self-hosted-runner` 让 Team/Enterprise 用户可将自有机器或容器纳为远程会话运行环境，同时新增 `archive` 插件源。社区方面，关于“会话数上限后续跑”的 #13354 以 191 👍 持续保持最高热度，Fable 5 系列的模型行为问题与后台任务静默杀掉成为新的讨论焦点。

## 版本发布

### v2.1.224
- **新增** `claude self-hosted-runner`：支持将自有机器/容器作为 Claude Code Web、移动端和桌面端会话的运行环境（Team 和 Enterprise 计划）。
- **新增** `archive` 插件源：支持从 HTTPS 上的 zip 包安装插件，无需依赖 Git 仓库。

## 社区热点 Issues

### 1. [FEATURE] Continue when the session limit reached — #13354
- **作者**: @massyn | 评论 73 | 👍 191
- **为什么重要**: 会话数到达上限后无法继续工作，是大量长会话用户的刚需痛点。该 Issue 的 👍 数远超其他所有 Issue，是目前社区呼声最高的功能请求。
- **链接**: https://github.com/anthropics/claude-code/issues/13354

### 2. [BUG] Fable 5: text in a response that also contains tool calls is never displayed — #81853
- **作者**: @rhv-resideo | 评论 5 | 👍 3
- **为什么重要**: 新模型 Fable 5 在同时包含文本与工具调用的响应中，主视图不显示文本部分（文本仅在 Ctrl+O 详细记录中可见）。该问题直接影响日常使用体验，且涉及新模型回归。
- **链接**: https://github.com/anthropics/claude-code/issues/81853

### 3. [BUG] Claude Code ≥ 2.1.205 livelocks at 100% CPU with no output on KVM guests with kvm64 — #77208
- **作者**: @joos81 | 评论 3 | 👍 0
- **为什么重要**: 在 KVM 虚拟化环境（kvm64 CPU 模型）中，≥2.1.205 版本即使执行 `--version` 也会 100% CPU 空转且无输出，同时导致 Linux 桌面版 Code 标签页静默故障。对云主机/虚拟化用户影响严重。
- **链接**: https://github.com/anthropics/claude-code/issues/77208

### 4. [DOCS] Plugin installation silently runs `bun install`/`npm ci` — #84939
- **作者**: @rymalia | 评论 1 | 👍 0
- **为什么重要**: 在 v2.1.224 上复验：安装插件时会自动执行依赖安装（bun.lock 存在时），该行为完全未在文档中说明。无锁文件时静默跳过、有 yarn.lock 时静默跳过，行为不一致且存在供应链安全隐忧。
- **链接**: https://github.com/anthropics/claude-code/issues/84939

### 5. [BUG] Background Bash tasks killed mid-run silently — #84625
- **作者**: @mattmeyer-ia | 评论 1 | 👍 0
- **为什么重要**: `run_in_background: true` 的后台任务在运行中被静默杀掉，无 OOM、无用户操作、无报错。作者在 2026-07-28 至 08-06 期间观察到约 10 次。长时间后台任务的可靠性是自动化工作流的关键。
- **链接**: https://github.com/anthropics/claude-code/issues/84625

### 6. [BUG] Remote Control: stale environments cannot be deleted, ghost sessions cause permanent 404 — #77372
- **作者**: @makeitnotable | 评论 3 | 👍 1
- **为什么重要**: 远程控制模式下 stale 环境无法删除，新环境注册后仍出现 404（会话 ID 不同但同样失败）。直接影响自托管 runner（v2.1.224 新增功能）的稳定性。
- **链接**: https://github.com/anthropics/claude-code/issues/77372

### 7. [FEATURE] Post-mortem: weekend three of Fable getting nothing done — #79247
- **作者**: @ThatDragonOverThere | 评论 1 | 👍 0
- **为什么重要**: 用户详述 19 天来 Fable 模型声称完成了 12 步流水线，实际 46 个日期中仅 1 个到达第 2 步。虽是情绪化贴文，但代表部分开发者对新模型的可靠性质疑，值得关注。
- **链接**: https://github.com/anthropics/claude-code/issues/79247

### 8. [FEATURE] BeforeModel and AfterModel Hooks for LLM Request/Response Interception — #21531
- **作者**: @coygeek | 评论 9 | 👍 3
- **为什么重要**: 请求在发送给模型前后缺少统一的拦截/审计点。该需求涉及成本控制、安全审计、可观测性等场景，在 hooks 体系中属于高频诉求。
- **链接**: https://github.com/anthropics/claude-code/issues/21531

### 9. [BUG] Safety check flagging clearly harmless content — #70458
- **作者**: @MrJoy | 评论 4 | 👍 0
- **为什么重要**: 安全检测对明显无害的指令（如“不要读取某文件夹”）误报，且作者认为该检查过于激进。类似反馈在多模型中反复出现，并影响正常开发效率。
- **链接**: https://github.com/anthropics/claude-code/issues/70458

### 10. [BUG] HTTP MCP client drops Mcp-Session-Id header — #70386
- **作者**: @shpp-abelokon | 评论 2 | 👍 0
- **为什么重要**: 对接 Streamable HTTP 会话模型的 MCP 服务器时，客户端未回传 `Mcp-Session-Id`，导致 tools/list 失败。该问题涉及 mcp-grafana、mcp-go 等常用服务器，影响 MCP 生态集成。
- **链接**: https://github.com/anthropics/claude-code/issues/70386

## 重要 PR 进展

当前仅有 3 条 PR 在 24 小时内更新，全部列出如下：

### 1. docs: fix stale hooks documentation link in bash_command_validator_example.py — #84854
- **作者**: @cassiacarollinee-ship-it
- **摘要**: 将示例脚本中指向旧 `docs.anthropic.com` 的链接更新为新的 `code.claude.com` 地址。仓库内其余 46 处链接均已更新。
- **链接**: https://github.com/anthropics/claude-code/pull/84854

### 2. fix(hookify): enforce proper rule evaluation scope and secure file read — #84747
- **作者**: @alifakbxr
- **摘要**: 修复 hookify 插件中 `load_rules()` 在 `event` 为 `None` 时绕过事件过滤的问题，确保 `Read`、`Browser` 等工具只触发 `all` 范围规则。
- **链接**: https://github.com/anthropics/claude-code/pull/84747

### 3. fix(security): address yaml injection and symlink credential overwrites in plugin scripts — #84711
- **作者**: @alifakbxr
- **摘要**: 修复 #76580，增加防御性检查，防止 YAML 注入和通过符号链接覆盖凭据文件。
- **链接**: https://github.com/anthropics/claude-code/pull/84711

## 功能需求趋势

综合全部 Issues，社区当前最关注的方向：

1. **会话持续性与恢复**（#13354、#84625、#77372）：会话数限制后续跑、后台任务不静默退出、远程会话无残留，反映出用户对长时间/无人值守工作流的强烈依赖。
2. **远程控制与自托管基础设施**：self-hosted runner 的发布带来新期待，配套的 remote control bug（stale 环境、404）被快速报告。
3. **插件机制完善**：`archive` 插件源的引入后，社区开始关注插件安装行为的透明度（自动 bun/npm 安装）与插件安全性（#84711、#84747）。
4. **可观测性与拦截能力**：BeforeModel/AfterModel 钩子、会话审计、成本控制仍是长期高频诉求。
5. **MCP 生态标准化**：HTTP MCP 会话头处理、二进制输出等细节问题不断浮现，说明 MCP 集成场景正在扩大。
6. **新模型支持质量**：Fable 5 系列的文本渲染、错误率等行为问题成为近期新增讨论热点。

## 开发者关注点

- **静默失败最令人困扰**：后台任务被杀、KVM 中 100% CPU 空转、MCP tools/list 失败等均无显式报错，开发者需要长时间轮询才能发现。缺少错误可见性是本周重点吐槽对象。
- **文档滞后于功能**：大量标题带 `[DOCS]` 的 Issue（coygeek 等维护者批量提交）指向文档缺失或与行为不一致，特别是 hooks 工具名列表、插件依赖安装、MCP 二进制输出等新能力。
- **Fable 5 的信任危机**：多个 Issue 反映 Fable 5 在工具调用、文本显示、长流程执行上的不稳定，社区对“新模型是否真的可用”存在明显分歧。
- **远程控制的边缘场景**：Windows 文件锁导致 relaunch 失败、iOS 无响应、桌面版浏览器崩溃等问题集中出现，多平台一致性仍待加强。
- **安全与误报的平衡**：安全检测误报与插件安全问题同时被讨论，社区希望更可配置的检测粒度而非一刀切拦截。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-08

## 今日速览

昨日发布正式版 `rust-v0.147.0`，核心新增便携式 Agent 插件安装/跨目录搜索、对话持久化分段浏览两大能力，并伴随两个 0.148.0 alpha 版本的快速迭代。社区方面，Windows 平台的沙箱、Computer Use 及 MCP 子进程生命周期问题持续发酵，多个高赞 Issue 等待官方响应；同时 v0.147.0 已出现 LiteLLM 流式请求回归反馈。

## 版本发布

### rust-v0.147.0 正式版
- **便携式 Agent 插件**：支持安装便携插件，并可在本地、个人、工作区及远程插件目录中跨范围搜索（#36544, #36409, #36919, #36796）。
- **对话管理增强**：支持将对话组织为持久化、手动排序的分段；浏览超长对话记录时可增量加载（#35722, #36007, #36380, #36948）。

### rust-v0.148.0-alpha.1 / alpha.2
- 两个快速迭代的 alpha 版本，暂无详细变更日志，主要同步主线修复。

## 社区热点 Issues

*以下按关注度与讨论热度综合排序（数据截至 2026-08-07）*

### 1. OAuth 认证失败：issuer 校验错误 — #31573
- **热度**：👍 74 | 评论 34 | 状态：OPEN
- **要点**：Codex CLI 0.143.0 在 OAuth 认证流程中，issuer 校验失败，影响免费版用户登录。
- **链接**：https://github.com/openai/codex/issues/31573

### 2. 请求新增 trust_level = "trusted" 全局配置 — #14599
- **热度**：👍 57 | 评论 16 | 状态：OPEN
- **要点**：项目首次打开需手动审批，反复打扰。社区希望提供全局信任配置，避免重复授权提示。
- **链接**：https://github.com/openai/codex/issues/14599

### 3. VS Code 的 Codex Diff 视图报错 — #35481
- **热度**：👍 54 | 评论 26 | 状态：CLOSED
- **要点**：Windows 平台上打开 Codex Diff 视图时显示 “Oops, an error has occurred”，内容无法加载，已关闭（疑似已修复或重复）。
- **链接**：https://github.com/openai/codex/issues/35481

### 4. Codex 响应速度过慢 — #21527
- **热度**：评论 41 | 👍 18 | 状态：OPEN
- **要点**：用户抱怨 VS Code 插件与 Codex App 模型响应均极慢，涉及 26.429.61741 版本，属于持续性能痛点。
- **链接**：https://github.com/openai/codex/issues/21527

### 5. MCP 子进程未被回收：1300+ 僵尸进程、37GB 内存泄漏 — #12491
- **热度**：评论 38 | 👍 5 | 状态：CLOSED
- **要点**：Codex.app GUI 包装的 MCP 子进程在任务完成后不退出，造成大量僵尸进程与严重内存泄漏（codex-cli 0.98.0）。
- **链接**：https://github.com/openai/codex/issues/12491

### 6. Windows 沙箱 `elevated_windows_sandbox` 导致所有命令失败 — #10090
- **热度**：评论 24 | 👍 7 | 状态：OPEN
- **要点**：沙箱提权后所有 agent 命令均报 `(no output)`，日志显示 `CreateProcessAsUserW failed: 5`（权限错误），影响 Business 订阅用户。
- **链接**：https://github.com/openai/codex/issues/10090

### 7. Windows Computer Use 在 EnumWindows 处失败 — #37043
- **热度**：评论 17 | 👍 3 | 状态：OPEN
- **要点**：Computer Use 插件的 `sky.list_apps()` / `list_windows()` 报 `0x80070003`，重启无效；Windows 平台功能不可用。
- **链接**：https://github.com/openai/codex/issues/37043

### 8. VS Code 扩展停止自动包含 IDE 上下文 — #31553
- **热度**：评论 16 | 👍 12 | 状态：OPEN
- **要点**：远程容器（.vscode-server）场景下，扩展更新后不再自动附带 IDE 上下文（文件、选中代码等），破坏工作流。
- **链接**：https://github.com/openai/codex/issues/31553

### 9. Windows 桌面端无法在 ChatGPT Project 中创建本地 Work 对话 — #34499
- **热度**：评论 15 | 👍 6 | 状态：OPEN
- **要点**：在 ChatGPT Project 内尝试创建新的 Work 会话失败（Windows 26.715.61943），项目/会话集成存在缺陷。
- **链接**：https://github.com/openai/codex/issues/34499

### 10. v0.147.0 与 LiteLLM provider 流式请求回归 — #37425 ⭐ 新
- **热度**：评论 4 | 👍 2 | 状态：OPEN（24 小时内创建）
- **要点**：升级至 v0.147.0 后，自定义 LiteLLM provider 的 streaming 请求持续失败；属于刚发布版本的快速回归反馈，值得跟进。
- **链接**：https://github.com/openai/codex/issues/37425

## 重要 PR 进展

*以下 PR 均于 24 小时内更新，多数来自自动化机器人（copyberry[bot]），以架构重构与稳定性修复为主。*

### 1. 工具命名空间清单纳入 turn 元数据 — #37492
- 为 Responses Lite 增加可选的 `tool_namespaces_info` 元数据，描述模型可见函数的命名空间、直接/延迟暴露方式及 Code Mode 属性，提升可观测性。
- https://github.com/openai/codex/pull/37492

### 2. MCP 事件发现与订阅机制 — #37494
- 新增 `McpResourceClient::list_events`，支持可取消的 `events/stream` 订阅，将运行时生命周期事件路由至请求方，拓展 MCP 协议能力。
- https://github.com/openai/codex/pull/37494

### 3. 连接失败时保持响应流存活 — #37485
- 将 HTTP 连接失败与其他网络错误区分；采样请求按 5–60 秒指数退避重试，并在 UI 展示 `Reconnecting...` 状态，减少流式响应中断。
- https://github.com/openai/codex/pull/37485

### 4. 进程终止时保留子进程等待器 — #37498
- 修复终止阶段 abort 子 waiter 导致 PTY 子进程未被 reap、会话丢失退出码的问题；改为 detach 等待器。
- https://github.com/openai/codex/pull/37498

### 5. 远程进程沙箱委托给执行器 — #37480
- 远程 `exec_command` 不再通过宿主机解析工作目录与权限，转而保留 executor 原生配置，使远程沙箱行为与本地一致。
- https://github.com/openai/codex/pull/37480

### 6. 中断 turn 时同步中断 code-mode 单元格 — #37483
- 新增默认关闭的 `code_mode_interrupt` 特性：turn 被中断时，终止其遗留的所有活跃 code-mode 任务，避免后台残留执行。
- https://github.com/openai/codex/pull/37483

### 7. 上下文压力下为技能定位器添加别名 — #37489
- 对 executor/orchestrator/host 的技能定位器引入源感知根别名（`e`/`o`/`r`），压缩元数据开销，确保长标识符不挤占技能上下文预算。
- https://github.com/openai/codex/pull/37489

### 8. 限制诊断日志中的 payload 追踪 — #37497
- 将 HTTP、SSE、WebSocket 的请求/响应体诊断限制为 `DEBUG` 级，防止高频大 payload 冲垮 SQLite 日志库与环形缓冲。
- https://github.com/openai/codex/pull/37497

### 9. 为 code-mode WebSocket 禁用 Nagle 算法 — #37504
- 对远程会话 WebSocket 启用 `TCP_NODELAY`，消除小包缓冲带来的延迟，优化交互式请求/响应时延。
- https://github.com/openai/codex/pull/37504

### 10. 响应元数据中加入沙箱模式 — #37507
- 在常规、预热、压缩与分离内存服务的 turn 元数据中增加 `sandbox_mode` 字段，并保留该 key 以防客户端覆盖。
- https://github.com/openai/codex/pull/37507

## 功能需求趋势

从近 24 小时更新的全部 Issues 中，社区最关注以下功能方向：

| 方向 | 代表性 Issues | 热度信号 |
|---|---|---|
| **Windows 平台支持** | #10090、#37043、#37415、#34499、#35718 | 高频 bug，涉及沙箱、Computer Use、桌面应用、权限模型 |
| **MCP 生态成熟度** | #12491、#31573、#35486、#35253、#37453 | OAuth 流程、传输稳定性、子进程生命周期、作用域语义 |
| **性能与资源占用** | #21527、#12491、#36523、#35799、#37397 | 响应慢、内存泄漏、启动 OOM、UI 卡顿 |
| **会话管理灵活度** | #14599、#21839、#34499、#34300、#26875 | 信任配置、项目/工作区集成、会话恢复审批、侧边栏排序 |
| **上下文长度扩展** | #28852 | 社区明确呼吁 GPT-5.5 在 Codex 中放开 1M 有效上下文 |

## 开发者关注点

- **Windows 沙箱与权限是最大痛点**：`CreateProcessAsUserW failed: 5` 问题横跨多个版本（#10090、#13965、#14211），且新出现的 WindowsApps ACL 问题（#37415）和 NUL 填充状态文件导致沙箱永久损坏（#35718）表明 Windows 路径仍是稳定性洼地。
- **MCP 稳定性直接影响生产使用**：从僵尸进程内存泄漏（#12491）到 OAuth/传输层故障（#31573、#35486），再到新提交的历史 subagent 线程重复拉起 MCP 栈（#37453），插件生态的可靠性亟待加强。
- **升级需谨慎**：v0.147.0 刚发布即出现 LiteLLM 流式回归（#37425），建议依赖自定义 provider 的团队暂缓升级；可在官方修复后再跟进。
- **桌面端体验欠佳**：后台预取导致 OOM 崩溃（#36523、#35799）、打开本地线程卡顿 5 秒（#37397）、静默消耗周限额（#37445）等新问题集中出现，桌面 App 的资源管理策略需要系统性改进。
- **希望减少重复确认**：`trust_level` 全局配置请求（#14599）获得 57 👍，充分说明开发者希望 Codex 在安全与效率之间提供更灵活的信任机制。

---
*日报数据来源：github.com/openai/codex · 统计窗口：2026-08-07 至 2026-08-08*

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报（2026-08-08）

## 今日速览

昨日发布 3 个版本（含 1 个 patch 和 1 个 preview 修复），但均无重大用户可见变更。社区讨论热度集中在子代理（Subagent）可靠性问题（如 #22323 误报成功、#21409 通用代理挂起）和 Auto Memory 系统的隐私/质量控制。PR 侧亮点是安全加固：一项 SSRF 高危漏洞修复（#28725）和沙箱运行时升级（#28726）同日合并（或待合并）。

## 版本发布

昨日发布 3 个版本，全部为维护性更新：

- **[v0.56.0-nightly.20260807.gd5c9a97dc](https://github.com/google-gemini/gemini-cli/releases/tag/v0.56.0-nightly.20260807.gd5c9a97dc)** — 夜间构建，包含上游 changelog 同步与版本号更新，无独立功能变更。完整的 changelog 指向 v0.55.0-preview.1。
- **[v0.55.0-preview.2](https://github.com/google-gemini/gemini-cli/releases/tag/v0.55.0-preview.2)** — 对 preview.1 的 cherry-pick 补丁，用于修复特定问题。
- **[v0.54.4](https://github.com/google-gemini/gemini-cli/releases/tag/v0.54.4)** — 对 v0.54.0 的 cherry-pick 补丁，含两个修复提交。

## 社区热点 Issues

以下为过去 24 小时更新最频繁、讨论度最高的 Issue：

1. **[#22323 Subagent 达到 MAX_TURNS 后被误报为 GOAL 成功](https://github.com/google-gemini/gemini-cli/issues/22323)** — 🔴 P1 严重 Bug，12 条评论。`codebase_investigator` 子代理在未做任何分析就触发最大轮次限制时，仍向主会话报告 `status: "success"` 和 `"GOAL"`，导致主代理误判任务完成。这是 Agent 信任链路中的高危缺陷。

2. **[#21409 Generalist agent 无限挂起](https://github.com/google-gemini/gemini-cli/issues/21409)** — 🔴 P1，8 条评论，👍 8。创建文件夹等简单操作在委派给 generalist agent 后永久挂起，最长等待一小时未返回。用户通过指示模型不要使用子代理可绕过，说明问题与子代理调度策略直接相关。

3. **[#25166 Shell 命令执行完后卡在 "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)** — 🔴 P1，4 条评论，👍 3。简单的 CLI 命令执行完毕后，终端仍显示命令活跃并等待输入。核心团队已标记为 effort/medium，可能需要状态机层面的修复。

4. **[#21983 Browser 子代理在 Wayland 下失败](https://github.com/google-gemini/gemini-cli/issues/21983)** — 🔴 P1，4 条评论。浏览器子代理在 Wayland 会话中无法正常工作，影响 Linux 用户群体。已进入 need-retesting 阶段。

5. **[#22093 v0.33.0 后子代理未经许可被调用](https://github.com/google-gemini/gemini-cli/issues/22093)** — P2，3 条评论。用户明确在配置中禁用了 agents 模式，但升级到 v0.33.0 后 generalist 等子代理仍被自动调用，属于权限配置失效问题，涉及信任边界。

6. **[#26522 Auto Memory 无限重试低信号会话](https://github.com/google-gemini/gemini-cli/issues/26522)** — P2，5 条评论。Auto Memory 的后台提取代理如果判定某会话为低信号而不读取，该会话不会被标记为已处理，导致在同一批会话上无限循环重试，浪费 token。

7. **[#26525 Auto Memory 确定性脱敏缺失](https://github.com/google-gemini/gemini-cli/issues/26525)** — P2，4 条评论，安全相关。Auto Memory 将本地 transcript 内容发送给模型时才提示脱敏，此时内容已进入模型上下文。且后台服务可能记录现有技能内容，存在隐私风险。

8. **[#20079 ~/.gemini/agents/ 下的符号链接不被识别为 agent](https://github.com/google-gemini/gemini-cli/issues/20079)** — P2，4 条评论。用户通过 symlink 管理自定义 agents 配置时无法生效，影响配置管理的灵活性。标记为 status/need-information。

9. **[#22745 调研 AST 感知的文件读取/搜索/代码库映射的价值](https://github.com/google-gemini/gemini-cli/issues/22745)** — P2，7 条评论，方向性 EPIC。评估 AST 工具能否精确读取方法边界、减少 token 噪声、提升导航效率。对长期代智能体上下文管理有重大意义。

10. **[#28713 Caretaker Agent 原型收尾](https://github.com/google-gemini/gemini-cli/issues/28713)** — P2，4 条评论。核心团队的自动化 triage 代理进入收尾阶段，列出待合入的 PR 清单（Firestore schema、Cloud Workflows、Pub/Sub 事件等），反映项目正在加强自治运维能力。

## 重要 PR 进展

1. **[#28673 新增 Gemini 3.6 Flash 和 3.5 Flash-Lite 模型配置](https://github.com/google-gemini/gemini-cli/pull/28673)** — P2，size/l。在 `packages/core` 中注册新模型的基础定义、别名、能力

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-08**  
**数据来源：** [github/copilot-cli](https://github.com/github/copilot-cli)

---

## 1. 今日速览

过去 24 小时密集发布了 3 个补丁版本（v1.0.79-6 至 v1.0.79-8），重点引入企业策略控制、`kimi-k3` 模型支持，并修复了会话历史加载失败导致的时间线空白问题。社区方面，共有 30 条 Issue 更新，其中 8 条为新提交，集中在 Windows 兼容性、权限配置不生效、会话恢复回归三大方向，另有 2 条 Issue 被关闭。

---

## 2. 版本发布

### v1.0.79-8
- **新增**：支持企业 `allow-auto-only` 策略——在完全禁止 `allow-all` 的企业环境中，`/allow-all auto` 仍可自动工作
- **新增**：企业托管沙箱策略可强制执行代理 URL，同时凭据仍由用户控制
- **改进**：`/sandbox` 配置对话框对 `git`、`gh` 等选项进行分组，界面更清晰

### v1.0.79-7
- **新增**：Agent 插件规范支持在 `com.github.copilot/extensions/` 目录下发布扩展
- **新增**：支持 `kimi-k3` 模型
- **新增**：可将 `--plan` 与 `--mode autopilot` 组合使用——先规划后自动实施，无需中间审批
- **改进**：用户多选提示的交互体验优化

### v1.0.79-6
- **修复**：罕见的内部延迟不再在交互式 UI 上叠加打印诊断警告
- **修复**：会话历史加载失败不再导致时间线永久空白——此前失败被静默丢弃，整个会话 transcript 保持空白且无日志输出

---

## 3. 社区热点 Issues（10 个精选）

### 🚨 高优先级回归 / Bug

**#2494 - `copilot login` 自动确认钥匙串提示（回归）**  
`v1.0.16` 起，当系统钥匙串不可用时，CLI 不再等待用户 `y/N` 输入，而是自动代替用户确认，导致认证流程异常结束。4 月创建至今仍在活跃讨论，已有 11 条评论。  
🔗 [github.com/github/copilot-cli/issues/2494](https://github.com/github/copilot-cli/issues/2494)

**#4251 - 恢复大型会话 OOM / 单核 CPU 占用约 70 分钟（1.0.74 回归）**  
1.0.74 版本恢复长期大型会话时内存占用飙升至 3-4 倍，并出现接近 70 分钟的单核 CPU 满载。作者通过 A/B 测试将问题精确隔离到版本变更，社区反馈影响面较大。  
🔗 [github.com/github/copilot-cli/issues/4251](https://github.com/github/copilot-cli/issues/4251)

**#4397 - 恢复会话时模型自动切换回默认模型**  
使用 `copilot --yolo --model=gpt-5.6-terr...` 创建会话后，`resume` 恢复时会话模型被静默重置为默认值，破坏多模型工作流。  
🔗 [github.com/github/copilot-cli/issues/4397](https://github.com/github/copilot-cli/issues/4397)

**#4401 - `skill` 工具无法找到 `~/.agents/skills` 中的有效技能（回归）**  
即使技能目录和 `SKILL.md` 均存在，`skill` 工具仍无法调用。社区认为与已关闭的 #2230 未完全修复有关，需紧急排查。  
🔗 [github.com/github/copilot-cli/issues/4401](https://github.com/github/copilot-cli/issues/4401)

### 🖥️ Windows 平台问题

**#3622 - Windows 上复制到剪贴板静默失败**  
复制操作无任何错误提示，但粘贴时仍为旧内容。1.0.48 中正常，现回归，影响 Windows 用户日常操作。  
🔗 [github.com/github/copilot-cli/issues/3622](https://github.com/github/copilot-cli/issues/3622)

**#1409 - `add-dir` 标志将路径中的破折号转为下划线，导致 OneDrive 权限循环**  
Windows 上 OneDrive 目录路径包含破折号时，权限授予路径与真实路径不匹配，触发无限权限请求。  
🔗 [github.com/github/copilot-cli/issues/1409](https://github.com/github/copilot-cli/issues/1409)

### 🧩 功能与体验

**#1632 - 支持 skills 子文件夹以更好地组织**  
目前 skills 目录只能扁平存放，超过 10 个技能后难以管理。获得 **23 个 👍**，社区需求强烈。  
🔗 [github.com/github/copilot-cli/issues/1632](https://github.com/github/copilot-cli/issues/1632)

**#4311 - transcript 渲染为空白行，直至 `children` 或终端宽度变化**  
交互模式下 transcript 底部区域空白，滚动可见内容但无法触发重绘，`/resume` 也无法恢复。涉及测量行缓存失效问题。  
🔗 [github.com/github/copilot-cli/issues/4311](https://github.com/github/copilot-cli/issues/4311)

### ⚙️ 配置与进程管理

**#4398 - `permissions.config` 中的 `allowed_directories` 从未被加载**  
用户配置了多个工作区的 `allowed_directories`，但 `/list-dirs` 从未显示，配置被静默忽略。权限系统可靠性受质疑。  
🔗 [github.com/github/copilot-cli/issues/4398](https://github.com/github/copilot-cli/issues/4398)

**#4392 - 认证后 MCP 客户端重建，遗留孤儿 stdio 子进程**  
启动时生成的 MCP stdio 子进程在认证完成后被整体重建，但第一代进程未被回收，造成进程泄漏。新提交即获关注。  
🔗 [github.com/github/copilot-cli/issues/4392](https://github.com/github/copilot-cli/issues/4392)

---

## 4. 重要 PR 进展

过去 24 小时内无 PR 更新或合并。

---

## 5. 功能需求趋势

从全部 30 条 Issue 中提炼出以下社区关注的五大方向：

| 方向 | 代表 Issue | 热度/影响 |
|------|-----------|----------|
| **权限系统可用性** | #4398、#4388、#4386 | 配置不生效、模式切换卡死、提示缺乏触发原因说明——权限系统成为最集中的吐槽点 |
| **Windows 平台体验修复** | #3622、#4391、#4384、#4399 | 剪贴板失败、代码页清屏、终端标题被改写、PowerShell hooks 运算符兼容——Windows 用户的日常操作受影响面广 |
| **会话管理增强** | #4397、#4395、#4251 | 恢复会话模型被重置、恢复大会话 OOM、快速删除操作被移除——会话生命周期管理需完善 |
| **终端交互与输入优化** | #4387、#4394、#4311 | Tab 应触发补全而非切换面板、Ctrl+C 双击退出需可配置、渲染空白刷新机制有缺陷 |
| **模型与技能生态扩展** | #4345、#4401、#1632 | 新模型支持持续推进，但技能路由存在回归，社区对技能组织方式有明确改进诉求 |

---

## 6. 开发者关注点

### 🔴 高频痛点

1. **回归问题密集**  
   登录流程（#2494）、会话恢复性能（#4251）、技能查找（#4401）、剪贴板（#3622）均出现回归，开发者对新版本稳定性信心受到影响。

2. **权限配置行为不一致**  
   `allowed_directories` 不加载（#4398）、权限模式切换不生效（#4388）、触发规则不透明（#4386）——权限系统需要从“能用”走向“可信赖”。

3. **Windows 生态“二等公民”感受明显**  
   多个 Windows 专属问题（代码页、终端标题、PowerShell 运算符）在短期内密集上报，侧面反映 Windows 用户基数增大且对体验要求提高。

4. **进程与后台任务管理缺失**  
   MCP 孤儿进程（#4392）、后台任务完成状态误判（#4385），让用户担心长期运行时的资源消耗与任务可靠性。

5. **快捷操作习惯被破坏**  
   Tab 补全行为改变（#4387）、Ctrl+C 双击退出不可配置（#4394）、会话快速删除入口消失（#4395）——细节交互回退引发大量反馈。

### 📌 社区情绪

- 新功能（`--plan` + `autopilot`、`kimi-k3`、企业策略）获得积极评价
- 但对“修复一个 bug 引入另一个 bug”的回归循环感到沮丧，部分 Issue 评论区已出现 A/B 版本对比等精细排查方法，社区自服务意识增强

---

*本日报由 AI 自动生成，数据截取时间为 2026-08-08。所有链接可点击直达 GitHub Issue 页面。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-08-08

## 今日速览

今日社区焦点集中在文件编辑安全与 Agent 权限控制两大方向：`StrReplaceFile` 在编辑非 UTF-8 文件时可能破坏无关字节的问题引发讨论，两个修复 PR 已提交；另有用户报告 Agent 在 yolo 权限模式下误删工作区外目录，凸显权限边界审核的紧迫性。交互体验方面，Shift+Enter 换行快捷键 PR 已关闭，后续可关注合并状态。

---

## 版本发布

过去 24 小时无新版本发布。

---

## 社区热点 Issues

> 说明：过去 24 小时内更新的 Issue 共 2 条，以下全部列出。

### 1. StrReplaceFile 破坏编辑区域外的不可解码字节
- **Issue**: [#2591](https://github.com/MoonshotAI/kimi-cli/issues/2591)
- **作者**: @shoemoney | 创建: 2026-08-05 | 更新: 2026-08-07
- **评论**: 3 | 👍: 0 | 状态: OPEN
- **内容摘要**: `StrReplaceFile` 使用 `errors="replace"` 解码整个文件，随后将编辑后的字符串整体写回。文件中任何非 UTF-8 字节（即使远离编辑区域）都会被替换为 U+FFFD 并写入磁盘（`EF BF BD`），导致文件长度与内容被永久改变。
- **重要性**: 这是数据损坏级别的严重 bug，影响任何包含二进制或非 UTF-8 内容的项目文件。社区已有 3 条评论且两个修复 PR 跟进，说明开发者高度重视。

### 2. Agent 在 yolo 权限模式下误删工作区外用户数据
- **Issue**: [#2596](https://github.com/MoonshotAI/kimi-cli/issues/2596)
- **作者**: @iMaxTomas | 创建: 2026-08-07 | 更新: 2026-08-07
- **评论**: 0 | 👍: 0 | 状态: OPEN
- **内容摘要**: 会话期间，Agent（yolo 权限模式）被要求清理它创建的符号链接 `~/.pi/agent/sessions`，但实际执行了 `rm -rf` 删除该路径下的真实目录，导致用户会话数据被清除。此前符号链接创建已失败（目标目录已存在），Agent 未注意到该错误。
- **重要性**: 直接暴露了权限模式对文件系统破坏性操作的边界控制不足，属于安全类高优先级问题。当前无评论，可能尚未被官方/社区关注，值得扩散。

---

## 重要 PR 进展

> 说明：过去 24 小时内更新的 PR 共 3 条，以下全部列出。

### 1. fix(tools): preserve non-UTF-8 bytes in StrReplaceFile edits
- **PR**: [#2594](https://github.com/MoonshotAI/kimi-cli/pull/2594)
- **作者**: @686f6c61 | 创建: 2026-08-06 | 更新: 2026-08-07
- **状态**: OPEN
- **内容摘要**: 修复 `StrReplaceFile` 对非 UTF-8 文件的破坏问题。方案改为在原始字节缓冲区上执行 `old`/`new` 的 UTF-8 字节子串替换，避免整体解码再编码造成的无关字节损坏。
- **技术亮点**: 以字节粒度操作替换逻辑，从根本上规避解码误差，是较彻底的修复思路。

### 2. fix(StrReplaceFile): refuse to edit files that are not valid UTF-8
- **PR**: [#2595](https://github.com/MoonshotAI/kimi-cli/pull/2595)
- **作者**: @shoemoney | 创建: 2026-08-06 | 更新: 2026-08-07
- **状态**: OPEN
- **内容摘要**: 同样针对 Issue #2591，采取保守策略：当文件不是合法 UTF-8 时直接拒绝编辑，防止数据被破坏。与 #2594 形成两种方案的对比。
- **权衡点**: 简单安全但可能阻塞对二进制文件的合法编辑需求，需权衡灵活性与安全性。

### 3. feat(shell): support Shift+Enter for inserting newlines
- **PR**: [#2255](https://github.com/MoonshotAI/kimi-cli/pull/2255)
- **作者**: @donbeave | 创建: 2026-05-13 | 更新: 2026-08-06
- **状态**: CLOSED
- **内容摘要**: 为交互式提示符新增 Shift+Enter 换行快捷键，与现有 Ctrl-J、Alt-Enter 并存。关联 #2254，同时引用 #2010、#2121、#1585、#1574 等历史需求。
- **解读**: PR 已关闭，可能已合并或未合并，但 Shift+Enter 作为主流终端交互习惯，此前已有多个相关 Issue 请求，说明该功能是社区长期痛点，建议关注合并后的使用反馈。

---

## 功能需求趋势

基于当前 Issue 与 PR 内容，社区关注点主要集中在以下方向：

- **文件编辑安全性**：`StrReplaceFile` 对非 UTF-8 文件的处理成为焦点，开发者希望这类工具函数能在字节层面工作，避免隐式解码破坏文件完整性。
- **权限边界管控**：Agent 误删操作引发对权限模式（尤其是 yolo 模式）的反思，社区可能需要更精细的路径白名单或危险操作确认机制。
- **交互体验优化**：Shift+Enter 换行等终端交互细节持续被需求，说明用户对 CLI 的日常使用舒适度有较高要求。

---

## 开发者关注点

- **数据无损是底线**：多个反馈围绕“工具函数不应偷偷修改文件内容”，开发者期望编辑操作严格限定在指定范围内，即使文件包含非法编码也能安全跳过。
- **Agent 操作可审计性**：yolo 模式下的 `rm -rf` 误删暴露了权限模式的粗粒度问题，社区需要更透明的操作日志或可回滚机制。
- **问题响应速度**：#2591 在两天内获得两个修复 PR，体现社区对严重 bug 的快速行动意愿；但 #2596 尚无人评论，建议核心维护者优先排查，避免安全类问题积累。

---
*本日报由自动化工具生成，数据截至 2026-08-08 00:00 UTC。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-08

## 今日速览

- **v1.18.15 发布**：纯 Bugfix 版本，修复消息排序、fork/revert 时间线一致性以及截断清理逻辑。
- **OpenCode Go 服务争议升温**：订阅用户遭遇 `401 Request blocked by upstream provider`（#38257）与“周配额耗尽但实际消费未达上限”的计费异常（#41146、#41102），成为社区最热议题。
- **社区功能需求集中爆发**：加密货币支付（👍37）、运行时子代理模型切换、技能子文件夹组织等呼声最高；PR 侧则以 App 层 UI 修复与跨提供商协议兼容性改进为主。

---

## 版本发布

### v1.18.15
纯 Bugfix 版本，核心修复三处：
1. **消息排序修正**：即使导入或遗留消息 ID 乱序，时间线仍按真实时间顺序展示。
2. **Revert/Fork 动作修正**：不再依赖消息 ID 排序，改用真实消息时间线作为依据。
3. **截断清理可靠性提升**：按文件时间戳更稳定地删除过期文件。

> 无新功能加入，建议受上述问题影响的用户升级。

---

## 社区热点 Issues（Top 10）

### 1. OpenCode Go 返回 401，`chat/completions` 全线受阻
- **Issue**: [#38257](https://github.com/anomalyco/opencode/issues/38257) | 状态: OPEN | 评论: 45 | 👍: 11
- **要点**: 自 7 月 22 日起，OpenCode Go 订阅调用 `chat/completions` 全部返回 `401 Request blocked by upstream provider`，而 `/v1/models` 正常。影响所有 Go 订阅模型。
- **社区反应**: 已有 45 条评论，持续 17 天未解决，是目前社区最关注的服务级故障。

### 2. [FEATURE] 支持加密货币支付 Go 订阅
- **Issue**: [#23153](https://github.com/anomalyco/opencode/issues/23153) | 状态: OPEN | 评论: 17 | 👍: 37
- **要点**: 社区强烈希望增加加密货币作为 OpenCode Go 的支付方式。
- **社区反应**: 当前全 Issue 列表👍数最高，但尚未收到官方回应。

### 3. 部分模型无法读取粘贴的图片（回归）
- **Issue**: [#5359](https://github.com/anomalyco/opencode/issues/5359) | 状态: OPEN | 评论: 18
- **要点**: v1.0.137 之后，粘贴图片会提示“无法读取图像”；v1.0.134 正常。涉及 LiteLLM + Vertex AI 后端链路。
- **社区反应**: 持续 8 个月未修复，影响面较广。

### 4. Amazon Bedrock Opus 4

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-08-08）

## 今日速览

正式版 v0.21.7 发布，核心变化为移除 Goals 功能的 50 轮对话上限，并支持在交互式 CLI 中渲染模型输出的终端内联图片。社区侧，自动化修复流程（autofix/takeover）正在推动多个 Web Shell 与认证相关 PR 合入，同时 Windows 平台的终端显示与桌面端稳定性问题成为今日最集中的反馈方向。

## 版本发布

### v0.21.7（正式版）
- **核心亮点**：
  - **移除 Goals 的 50 轮限制**（[#8421](https://github.com/QwenLM/qwen-code/pull/8421)）：任务可在超过原有边界后继续恢复执行。
  - **终端内联图片渲染**：交互式 CLI 支持直接展示模型输出的内联终端图片，适合 Ki 系列等多模态场景。

### v0.21.7-nightly.20260807.fca8f3c1f
- 仅包含一个 CI 修复：`fix(ci): surface blocked autofix takeover admission`（[#8410](https://github.com/QwenLM/qwen-code/pull/8410)），用于暴露被阻塞的 autofix 接管准入问题。

## 社区热点 Issues

过去 24 小时更新的 39 条 Issue 中，精选以下 10 条最值得关注：

1. **[#3203] Qwen OAuth 免费层政策调整**（150 条评论 · 已关闭）
   https://github.com/QwenLM/qwen-code/issues/3203
   提议将免费额度从 1000 次/天降至 100 次/天并逐步关闭免费入口。评论数远超其他 Issue，社区对价格策略变化极为敏感，虽已关闭但讨论热度最高。

2. **[#8625] Windows 终端中文输入时拼音显示不清**（6 条评论 · 开放）
   https://github.com/QwenLM/qwen-code/issues/8625
   中文输入法场景下终端渲染问题，直接影响中文用户日常使用，附有截图和客户端版本信息（0.21.5），是典型的 UI 渲染 bug。

3. **[#8615] Windows 桌面版 0.1.0 启动崩溃：EISDIR lstat 'C:'**（5 条评论 · 已关闭 · P1）
   https://github.com/QwenLM/qwen-code/issues/8615
   Windows 桌面版打开工作区时崩溃，属于 P1 级别平台阻断问题，已关闭说明已定位或修复。

4. **[#8562] tmux 中屏幕闪烁（iTerm2 SSH → Ubuntu → tmux）**（5 条评论 · 开放）
   https://github.com/QwenLM/qwen-code/issues/8562
   用户借助 Qwen 3.8 Max 排查后指向 Qwen Code 版本问题。涉及 TUI 渲染，影响远程开发典型场景。

5. **[#8660] 为使用遥测添加运行时和客户端归属**（5 条评论 · 已关闭）
   https://github.com/QwenLM/qwen-code/issues/8660
   当前的 `properties.channel` 无法区分 VS Code 扩展和 CLI 等入口，社区希望增加稳定的运行时归属字段，可观测性需求明确。

6. **[#8092] 围绕 Web Shell 构建低维护成本的桌面应用**（5 条评论 · 开放）
   https://github.com/QwenLM/qwen-code/issues/8092
   提出复用 Web Shell 作为桌面端 UI，而非维护独立桌面实现，反映社区对桌面端维护成本与体验统一的关注。

7. **[#8593] 桌面版 Markdown 链接点击无响应**（4 条评论 · 已关闭）
   https://github.com/QwenLM/qwen-code/issues/8593
   样式正常但点击不触发任何浏览器打开或错误提示，属桌面端交互短板，已关闭推测已进入修复流程。

8. **[#8550] `qwen mcp list` 在 SSE 服务器上无限挂起**（4 条评论 · 已关闭）
   https://github.com/QwenLM/qwen-code/issues/8550
   当 MCP 服务器使用 SSE 传输且不发送 `endpoint` 时，命令永久阻塞而非超时。影响 MCP 生态稳定性，已标记 ready-for-agent。

9. **[#7118] Windows 独立安装包因 Get-FileHash 失败**（4 条评论 · 3 👍 · 开放）
   https://github.com/QwenLM/qwen-code/issues/7118
   PowerShell 的 `Get-FileHash` 解析失败导致 SHA-256 校验报错，安装中断。已影响真实用户并获得社区点赞，Windows 安装路径的老问题。

10. **[#8695] Context 使用率默认重复显示（状态栏+页脚）**（3 条评论 · 开放）
    https://github.com/QwenLM/qwen-code/issues/8695
    当内置状态栏开启时，上下文窗口使用率在状态栏与页脚同时出现，UI 冗余且占用空间，属于轻微但明确的 UI/UX 问题。

## 重要 PR 进展

过去 24 小时更新的 50 条 PR 中，精选以下 10 条：

1. **[#8707] Qwen WebBridge 直接浏览器控制**（Qwen WebBridge）
   https://github.com/QwenLM/qwen-code/pull/8707
   添加从 `qwen serve` 到 Chrome 扩展的直连浏览器控制路径，兼容 Kimi WebBridge 的 `/command` 与 `/status` 端点，支持 17 种操作。

2. **[#8675] 模型特定推理控制（thinking/effort）**（端到端注册）
   https://github.com/QwenLM/qwen-code/pull/8675
   在 Core、ACP、daemon、SDK 和 WebShell 中端到端支持模型推理控制（Thinking/Effort 可选档位），首个注册模型为 `qwen3.*`。

3. **[#8394] `/review` 添加 Maven 多模块验证**
   https://github.com/QwenLM/qwen-code/pull/8394
   让 `review build-test` 识别根 Maven reactor，把变更文件映射到最深层默认模块，并支持常用 Maven 参数透传。

4. **[#8368] 为 `/auth` 添加 Kimi 和小米 MiMo 提供商**
   https://github.com/QwenLM/qwen-code/pull/8368
   Kimi 提供 Coding Plan / API Key（中国/国际）三种接入方式；小米 MiMo 支持按量付费及中国、新加坡等区域。

5. **[#8693] 修复 integration-tests 从无法类型检查到 0 错误**
   https://github.com/QwenLM/qwen-code/pull/8693
   `tsconfig.json` 中 `compilerOptions.paths` 含 `"//"` 文档键导致 tsc 直接中止；修复后目录从“完全无法检查”变成 0 错误，并修复了暴露出的所有问题（对应 Issue #8692）。

6. **[#8687] 守护跨 worktree 的 Git 变更**
   https://github.com/QwenLM/qwen-code/pull/8687
   内置主机侧防护，识别 `run_shell_command` 中通过 `-C` / `--work-tree` / `--git-dir` 的仓库迁移，阻止逃逸会话工作区的变更操作。

7. **[#8708] 为 review 工具加入软性工具调用预算**
   https://github.com/QwenLM/qwen-code/pull/8708
   在 review 计划中引入 `agentToolBudget`，公式为 `clamp(30 + effective/20, 30, 60)`，作为 finder 与 auditor 简报中的软上限。

8. **[#8588] `qwen serve` 暴露活动工作状态**
   https://github.com/QwenLM/qwen-code/pull/8588
   在 `GET /health?deep=1` 中新增 `activeWork`、`activeWorkReporting`、`activeWorkStaleMs` 三个字段，便于外部监控真实工作负载。

9. **[#8706] 修复：尊重可信环境边界（对应 #8643）**
   https://github.com/QwenLM/qwen-code/pull/8706
   按项目分别评估工作区信任状态，用户级 `.env` 文件保持无条件加载，同时保留显式 `workspaceTrusted` 覆盖。

10. **[#8613] Web Shell 的 tmux 交互式终端子代理**
    https://github.com/QwenLM/qwen-code/pull/8613
    让 Agent 在 daemon 主机的 tmux 会话中运行 REPL、TUI 等交互式 CLI，Web Shell 侧提供实时终端视图，支持作为后台任务驱动。

## 功能需求趋势

从过去 24 小时更新的 Issues/PRs 中，社区最关注的功能方向：

- **浏览器与本地设备控制**：#8699（Kimi WebBridge 风格直接浏览器控制）、#8595（手机 QR 码配对访问本地会话）、#8707（WebBridge 实现落地）——延续“外部设备/工具操控本地 Agent”的需求主线。
- **多模态与 Omni 实验**：#8197（Omni 多模态接入实验 Roadmap）、#8185（S3 投递可靠性的缓存与恢复）——omni-experiment 分支持续推进，且社区对可靠性细节（TTL、凭证缓存）有明确诉求。
- **Web Shell 作为统一 UI 载体**：#8092（用 Web Shell 构建低维护桌面应用）、#6699/#6701（composer 工具栏重设计）——Web Shell 被社区视为桌面端维护成本问题的解法。
- **可观测性与遥测完善**：#8660（运行时/客户端归属）、#8616（会话生命周期对齐 OTel）、#8697（OTEL 环境变量兼容）——企业用户对 OpenTelemetry 标准化的需求日益突出。
- **第三方模型/提供商接入**：#8368（Kimi、小米 MiMo）、#8675（模型推理控制注册表）——平台开放性与多模型支持成为明确方向。
- **文档国际化**：#8551（添加韩语）——社区自发贡献多语言支持，反映项目国际化吸引力。

## 开发者关注点

- **Windows 平台问题高频出现**：中文输入拼音显示不清（#8625）、安装包 SHA-256 校验失败（#7118）、桌面版启动崩溃 EISDIR（#8615）、PuTTY 中键选择回归（#8672）——Windows 上的终端渲染、安装流程与桌面端稳定性是最集中的痛点。
- **TUI 在特殊终端环境下的兼容性**：tmux 闪屏（#8562）、Web 终端全屏重绘闪烁/撕裂（#8659）、PuTTY 鼠标行为回归（#8672）——远程/Web 终端用户对虚拟化历史模式（useTerminalBuffer）的默认开启效果反馈较多。
- **MCP 生态稳定性**：SSE 服务器无响应导致 `qwen mcp list` 无限挂起（#8550），即使已关闭也说明 MCP 健康检查与超时机制需要更稳健。
- **桌面端交互细节缺失**：Markdown 链接点击无反应（#8593）、“Local Control”手机访问（#8595）等桌面体验需求被反复提起。
- **配置与多工具共存问题**：`OTEL_METRICS_EXPORTER=otlp

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*