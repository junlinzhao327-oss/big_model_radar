# AI CLI 工具社区动态日报 2026-09-14

> 生成时间: 2026-09-13 22:35 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-09-14）

> 数据边界：本期仅 Claude Code、GitHub Copilot CLI、Kimi Code CLI、OpenCode 有有效摘要；OpenAI Codex、Qwen Code 无数据，Gemini CLI 摘要生成失败。以下结论基于 4 个有效样本。

## 1. 生态全景

AI CLI 正从“代码问答/补全”快速转向“多 Agent 运行时”。竞争焦点已不只是模型能力，而是 Agent 可观测性、可中断性、权限控制与 token 成本治理。MCP 成为工具集成的核心入口，但配置加载、schema 兼容和错误可诊断性仍很脆弱。跨平台稳定性与版本升级体验，正在成为开发者信任度的分水岭。社区对“强制迁移 UI”“静默失效”“升级即崩溃”异常敏感，说明工具已进入生产工作流。

## 2. 各工具活跃度对比

| 工具 | Release | Issues 更新/列示 | PR 更新/列示 | 今日关键信号 |
|---|---:|---:|---:|---|
| Claude Code | 0 | 列示 10（含 OPEN/CLOSED，非全量） | 5 | 高票 IDE 集成：#15942 VS 2026 获 437👍；Windows 进程锁、Keychain token 清空、多会话消息丢失 |
| GitHub Copilot CLI | 0 | 5（全量） | 2（均为 Dependabot，已关闭） | v1.0.83 回归：Workspace `.mcp.json` 未加载、Linux Voice ONNX 崩溃；subagent 击穿 prompt caching |
| Kimi Code CLI | 0 | 0 | 1（OPEN，文档类） | 仅 OpenAI 兼容 Provider 配置澄清；Issues 零更新，社区极低活跃 |
| OpenCode | 0 | 列示 10 热点 + 其他 | 50（均 CLOSED，多为自动清理） | v1.18.30 prompt 崩溃回归；新版布局强制迁移反弹；Muse Spark `encrypted_content` 报错 |
| Gemini CLI | — | 摘要失败 | — | 数据不可用 |
| OpenAI Codex | — | 无数据 | — | 数据不可用 |
| Qwen Code | — | 无数据 | — | 数据不可用 |

## 3. 共同关注的功能方向

| 方向 | 涉及工具 | 具体诉求 |
|---|---|---|
| Agent 可观测与可控 | Copilot、OpenCode、Claude | Copilot #2254 要后台子代理进度流；OpenCode #36423 要取消后台 subagent；Claude 多会话消息丢失、跨会话通信可靠性 |
| 成本与 token 透明度 | Copilot、OpenCode、Claude | Copilot #4829 prompt caching 失效导致 token 倍增；OpenCode token 计数覆盖、tokens/秒、配额

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---

# Claude Code 社区动态日报（2026-09-14）

> 数据来源：github.com/anthropics/claude-code  
> 统计范围：过去 24 小时内更新（截至 2026-09-13）

## 1. 今日速览

过去 24 小时无新 Release。社区讨论主要集中在 Windows 桌面端进程锁、Visual Studio 2026 集成、VS Code 自动附加设置等开放需求上，其中 VS 2026 集成 Issue 已获得 437 个 👍。PR 侧更新较少，仅 5 条，主要涉及插件/模组测试布局、`validate-agent.sh` 修复与 CLI 构建基础设施。

## 2. 版本发布

无新版本发布。

## 3. 社区热点 Issues

以下挑选 10 个最值得关注的 Issue，包含开放高热度问题与近期关闭但仍反映关键痛点的条目。

1. **#42776 [OPEN] Windows 桌面端因孤儿进程文件锁无法重启**  
   评论 182，👍 88。Windows 桌面端长期未解决的可靠性问题，影响重启与更新流程。  
   https://github.com/anthropics/claude-code/issues/42776

2. **#15942 [OPEN] 支持 Visual Studio 2026 集成**  
   评论 152，👍 437。当前最高票功能请求之一，反映 Windows/.NET 开发者对官方 IDE 集成的强烈需求。  
   https://github.com/anthropics/claude-code/issues/15942

3. **#24726 [OPEN] VS Code 扩展增加“禁用自动附加打开文件/选区”设置**  
   评论 73，👍 237。社区希望更精细地控制上下文注入，避免自动附加带来的隐私与上下文污染问题。  
   https://github.com/anthropics/claude-code/issues/24726

4. **#88094 [OPEN] Windows TUI 远程控制默认开启**  
   评论 10，👍 10。默认行为与安全预期冲突，涉及远程控制是否应默认启用。  
   https://github.com/anthropics/claude-code/issues/88094

5. **#76026 [CLOSED] Sonnet 5 将 `UserPromptSubmit` 误判为提示注入并拒绝执行**  
   涉及 `area:model`、`area:hooks`、AWS Bedrock，已标记 stale/reproduced。模型安全策略与 hooks 兼容性问题值得持续关注。  
   https://github.com/anthropics/claude-code/issues/76026

6. **#74699 [CLOSED] iTerm2 下 CLI 作为守护子会话启动，阻塞 Agents 面板/会话切换**  
   macOS 终端与 Agent View 集成问题，影响多会话工作流。  
   https://github.com/anthropics/claude-code/issues/74699

7. **#86370 [CLOSED] 跨会话消息自 2.1.227 起静默丢失**  
   发送方显示成功，目标会话却收不到消息。多会话/Agent 通信可靠性问题，对自动化工作流影响较大。  
   https://github.com/anthropics/claude-code/issues/86370

8. **#84331 [CLOSED] macOS CLI 登录循环：Keychain 凭据 token 被清空**  
   `claudeAiOauth` 与 MCP OAuth 条目中的 accessToken/refreshToken 为空，导致登录循环，属于认证持久化严重问题。  
   https://github.com/anthropics/claude-code/issues/84331

9. **#85749 [CLOSED] Claude Code Web：同一容器内消息在两个并发会话间交替，UI 无提示**  
   Web 端会话隔离与 UI 状态同步问题，影响多日复用容器的可信度。  
   https://github.com/anthropics/claude-code/issues/85749

10. **#73886 [CLOSED] 自定义 `fileSuggestion` 命令用数组索引作为评分，导致 MCP 资源排序异常**  
    涉及 TUI、MCP 与文件建议排序核心逻辑，且已有复现，属于工具链细节但影响明显。  
    https://github.com/anthropics/claude-code/issues/73886

## 4. 重要 PR 进展

过去 24 小时仅有 5 条 PR 更新，以下为全部条目。

1. **#79148 [OPEN] 为示例规则文件名添加必需的 `hookify.` 前缀**  
   修复 hookify 加载器只识别 `.claude/hookify.*.local.md`，而示例文件缺少前缀导致规则被静默忽略的问题。  
   https://github.com/anthropics/claude-code/pull/79148

2. **#89404 [OPEN] 修复 `validate-agent.sh` 在首个警告处中止并误报有效 Agent**  
   解决 `set -euo pipefail` 与 `((warning_count++))` 交互导致的提前退出，关联公开 Issue #83803。  
   https://github.com/anthropics/claude-code/pull/89404

3. **#41621 [CLOSED] 添加缺失的 CLI 构建基础设施与打包配置**  
   包含从 TypeScript 源码打包为单可执行文件的构建文档与 esbuild 配置，已关闭但涉及 CLI 构建链路。  
   https://github.com/anthropics/claude-code/pull/41621

4. **#93951 [OPEN] 将 diff、sec-default、telemetry 三个模组的测试移至模组旁**  
   行为测试迁移到 `mods/<mod>/tests/`，按单元组织，并由 `claude plugin test` 运行，改善插件测试结构。  
   https://github.com/anthropics/claude-code/pull/93951

5. **#93932 [CLOSED] 修正 telemetry 模组 `types` 路径为 `./` 相对路径**  
   修复 `plugin.json` 中唯一的裸相对路径，使其符合 manifest schema 对 `types` 的要求。  
   https://github.com/anthropics/claude-code/pull/93932

## 5. 功能需求趋势

从近期 Issues 可提炼出以下社区关注方向：

- **IDE 集成深化**：Visual Studio 2026 集成、VS Code 自动附加开关、IDE 扩展行为一致性。
- **Windows 平台稳定性**：桌面端重启失败、远程控制默认开启、网络 ECONNRESET、安装/更新异常。
- **多会话与 Agent 通信**：跨会话消息丢失、iTerm2 子会话阻塞、Web 端并发会话串流。
- **模型行为与 Hooks 兼容**：Sonnet 5 误判提示注入、`AskUserQuestion` 触发错误通知类型、Skill 指令与工具调用批处理顺序。
- **认证、更新与打包**：macOS Keychain token 清空、Homebrew/apt 更新提示误报、自动更新静默失败。
- **成本与用量透明度**：prompt-cache token 异常增长、用量百分比单次跳变过大。
- **MCP 与工具链细节**：MCP 资源排序、文件建议评分、LSP 诊断过期。
- **无障碍与可配置性**：屏幕阅读器模式开关、TUI/CLI 配置项细化。

## 6. 开发者关注点

开发者反馈中的高频痛点集中在：

- **Windows 桌面端进程与文件锁**：孤儿进程导致无法重启，影响日常使用与升级。
- **IDE 上下文控制**：VS Code 自动附加打开文件/选区缺乏关闭选项，用户希望显式控制。
- **官方 IDE 覆盖不足**：Visual Studio 2026 支持请求票数极高，说明非 VS Code 用户群体需求强烈。
- **多会话可靠性**：跨会话消息静默丢失、Web 会话串流、macOS 子会话阻塞，均影响 Agent 工作流可信度。
- **认证与更新机制**：macOS Keychain token 清空、包管理器更新提示误报、自动更新静默失败，属于基础体验问题。
- **模型安全策略副作用**：Sonnet 5 对 `UserPromptSubmit` 的误判可能破坏 hooks 与自动化流程。
- **成本可解释性**：token 缓存增长与用量百分比跳变让开发者难以预估费用。
- **MCP/工具排序与诊断准确性**：排序错误、LSP 过期诊断等问题虽小，但直接影响编码辅助体验。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

⚠️ 摘要生成失败。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-09-14** ｜ 数据来源：github.com/github/copilot-cli

> 数据说明：过去 24 小时内无新版本发布，Issues 更新 5 条、PR 更新 2 条。本期按重要性**全量列出**，未凑数虚构条目。

---

## 1. 今日速览

- 过去 24 小时**无新 Release**，社区焦点集中在 v1.0.83 暴露的两处回归问题：**Voice 模式在 Linux 上崩溃**、**Workspace 级 `.mcp.json` 完全未被加载**。
- Agent 子代理（subagent）的可观测性与资源消耗成为持续热点：一条新提交的 Bug 指出 subagent 单轮长工具链调用**击穿 prompt caching 并导致 token 消耗倍增**。
- 仓库维护侧仅有两笔 Dependabot 依赖升级（GitHub Actions），无功能性代码变更。

---

## 2. 版本发布

过去 24 小时无新版本发布。当前社区讨论主要围绕 **v1.0.83** 的已知问题展开（详见下方 Issues）。

---

## 3. 社区热点 Issues

（本期实际更新仅 5 条，全部列出）

### 1. #4832 — Workspace `.mcp.json` 在 CLI 1.0.83 中完全未加载 🔴 新增
- **链接**：https://github.com/github/copilot-cli/issues/4832
- **状态**：OPEN / triage ｜ 作者 @ryan-knopp-elanco ｜ 创建 2026-09-13
- **要点**：仓库根目录的 `.mcp.json` 被完全忽略，`copilot mcp list` 只输出 `User servers:`，从不出现 `Workspace` 分组。作者强调**这不是显示问题**——服务端根本没有被启动，会话日志中也无任何相关记录。
- **为何重要**：MCP 是 CLI 与外部工具/数据源集成的核心能力，Workspace 级配置失效会直接导致「团队共享的项目级 MCP 配置」这一主要使用场景不可用，属于影响面较大的回归。

### 2. #4833 — Voice 模式在 Linux 上触发 ONNX Runtime 断言并崩溃 🔴 新增
- **链接**：https://github.com/github/copilot-cli/issues/4833
- **状态**：OPEN / triage ｜ 作者 @r-o-x ｜ 创建 2026-09-13 ｜ 评论 0
- **要点**：启用语音输入后，CLI 以 signal 6（`SIGABRT`）中止并 dump core，崩溃发生在本地 Nemotron 语音模型处理音频时；环境为 Manjaro Linux / x64、CLI 1.0.83。
- **为何重要**：本地推理栈（ONNX Runtime）的断言失败属于**硬崩溃**，无优雅降级路径，且目前零评论、暂无维护者响应，风险等级高。

### 3. #4829 — Subagent 单轮长工具链击穿 prompt caching，token 消耗成倍放大 🟠 新提交
- **链接**：https://github.com/github/copilot-cli/issues/4829
- **状态**：OPEN / triage ｜ 作者 @gcapnias ｜ 创建 2026-09-12，更新 2026-09-13 ｜ 评论 1
- **要点**：环境为 CLI v1.0.83 / Windows 11 + PowerShell / 主模型 Gemini 3.8 Flash。当子代理（经 `task` 工具的自定义 agent）在**单个 turn 内执行数百次工具调用**时，agent harness 会导致 prompt caching 失效，成本与延迟同步膨胀。
- **为何重要**：同时命中「成本」与「性能」两个最敏感的开发者痛点，且随着自治型多 agent 工作流普及，这是架构级而非边角问题，值得优先跟进。

### 4. #2254 — 为后台子代理提供实时进度流式输出 🟡 长期需求
- **链接**：https://github.com/github/copilot-cli/issues/2254
- **状态**：OPEN / area:agents ｜ 作者 @Ghislain89 ｜ 创建 2026-03-24，更新 2026-09-13
- **要点**：在多阶段编排型 agent（plan → implement → deliver → review）场景下，`/tasks` 仅显示工具调用计数，缺少细粒度进度信息。请求增加更丰富的后台子代理可观测性。
- **为何重要**：创建已近半年仍在活跃更新，说明这是**长期未被满足的结构性需求**；与 #4829 同属「agent 运行时黑盒」问题域，指向同一产品缺口。

### 5. #2147 — CAIP 400：`input item ID does not belong to this connection` ✅ 已关闭
- **链接**：https://github.com/github/copilot-cli/issues/2147
- **状态**：CLOSED ｜ 作者 @crgarcia12 ｜ 创建 2026-03-18，更新 2026-09-12 ｜ 评论 7 ｜ 👍 1
- **要点**：WebSocket 会话报 `CAPIError: 400`，模型为 gpt-5.4（xhigh）。历经近 6 个月、7 条评论后关闭。
- **为何重要**：本批次唯一关闭项，涉及长连接会话状态管理；其解决路径对理解 #4829 中 subagent 会话/缓存问题有参考价值。

---

## 4. 重要 PR 进展

（本期实际更新仅 2 条，全部列出）

### 1. #4827 — `actions/stale` 9.1.0 → 11.0.0 ✅ 已关闭
- **链接**：https://github.com/github/copilot-cli/pull/4827
- **类型**：dependencies, github_actions ｜ 作者 @dependabot[bot] ｜ 更新 2026-09-13
- **内容**：升级仓库自动关闭陈旧 Issue/PR 的 action，跨两个大版本（含行为变更说明）。属 CI/仓库治理维护，不影响 CLI 运行时行为。

### 2. #4828 — `actions/github-script` 7.1.0 → 9.0.0 ✅ 已关闭
- **链接**：https://github.com/github/copilot-cli/pull/4828
- **类型**：dependencies, github_actions ｜ 作者 @dependabot[bot] ｜ 更新 2026-09-13
- **内容**：升级工作流脚本执行 action 至 v9 主版本。同样属维护性依赖更新。

> 说明：两笔 PR 均为 Dependabot 自动提交且已关闭，过去 24 小时内**没有功能特性或 Bug 修复类 PR 合入**。

---

## 5. 功能需求趋势

从本期 Issues 可提炼出三条主线：

| 方向 | 代表 Issue | 社区诉求 |
|---|---|---|
| **Agent 可观测性** | #2254、#4829 | 后台/子代理目前是黑盒：既看不到细粒度进度，也无法解释为何单轮长工具链会击穿缓存、成倍放大 token |
| **MCP 配置与集成** | #4832 | 需要可靠的分层配置（User / Workspace / Repo）加载机制，项目级共享配置是团队落地的关键 |
| **多模态与本地推理稳定性** | #4833 | 本地语音模型（Nemotron / ONNX Runtime）需要跨平台健壮性，Linux 上不应 hard crash |

其余观察：本期无新模型支持类需求提出；性能与成本问题（#4829）取代单纯的编辑器/IDE 集成话题，成为 agent 时代的新焦点。

---

## 6. 开发者关注点

- **成本失控风险**：prompt caching 在长工具链子代理场景下失效，直接造成 token 爆炸式增长——开发者已经开始关注「agent 自治程度」与「账单」之间的权衡。
- **配置加载的确定性**：Workspace `.mcp.json` 静默失效（无报错、无日志）比显式失败更伤，开发者需要**可诊断性**而非沉默降级。
- **跨平台健壮性**：Linux 桌面环境的语音功能崩溃说明本地推理栈的边界测试仍不充分，非 macOS/Windows 用户处于次要支持地位。
- **可观测性缺口**：`/tasks` 只给工具调用计数、子代理执行过程不可见，使得调试多阶段 agent 工作流极为困难。
- **维护节奏**：24 小时内零 Release、零功能性 PR，仅依赖升级，但同期新增 3 条 Issue（其中 2 条为硬性回归/Bug），**Issue 流入速度高于修复速度**，值得关注。

---

*本日报基于 2026-09-12 至 2026-09-13 的公开 GitHub 数据生成。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-09-14** ｜ 数据来源：github.com/MoonshotAI/kimi-cli

---

## 1. 今日速览

今日仓库整体处于低活跃状态：**无新版本发布，Issues 在过去 24 小时内零更新**，仅有 **1 条 PR 处于开放状态**。唯一动态是文档类 PR #2641，聚焦于澄清 OpenAI 兼容 Provider 的配置方式（base URL 与模型 ID），并说明环境变量对配置字段的覆盖优先级。今日社区无功能性代码变更进入评审流程。

---

## 2. 版本发布

过去 24 小时内无新 Release，本节省略。

---

## 3. 社区热点 Issues

**过去 24 小时内 Issues 更新数为 0 条，无可用数据。**

> 说明：本期无法按"挑选 10 个最值得关注的 Issue"输出。为避免生成虚假条目，此处不做臆测性填充。如需历史 Issue 盘点，建议扩大数据窗口（如近 7 天或 30 天）。

---

## 4. 重要 PR 进展

过去 24 小时内共 1 条 PR 更新，实际可分析条目为 1 条（非 10 条）。

### PR #2641 — docs(providers): clarify OpenAI-compatible configuration
- **状态**：OPEN ｜ **作者**：@QIU-Guanzong
- **创建/更新**：2026-09-13 ｜ **评论**：暂无 ｜ **👍**：0
- **链接**：https://github.com/MoonshotAI/kimi-cli/pull/2641

**内容摘要：**
1. 澄清自定义 OpenAI 兼容 Provider 需要提供 **API 根路径形式的 base URL**，以及**服务端实际接受的 model ID**——这两点是接入第三方兼容服务时最常见的配置误区。
2. 明确当 `OPENAI_BASE_URL` 与 `OPENAI_API_KEY` **非空**时，会**覆盖** Provider 中对应字段，且该行为对 `openai_legacy` 与 `openai_responses` 两种模式**同时生效**。
3. 保持英文与中文文档同步更新（摘要在此处截断）。

**为什么值得关注：**
这是典型的"降低接入摩擦"型文档改进。OpenAI 兼容层是 Kimi Code CLI 对接自建推理服务、第三方网关、企业内网模型的关键入口，而 base URL 该填 `/v1` 还是根域名、环境变量与配置文件谁优先，长期是用户踩坑高发区。该 PR 把隐式行为显式化，可显著减少同类支持类 Issue。

**社区反应：** 目前尚无评论与点赞，处于待评审状态，需维护者确认文档描述与实际实现是否完全一致。

---

## 5. 功能需求趋势

今日 Issues 数据为空，**无法从 Issue 语料中提炼功能方向**。仅能从唯一 PR 的主题做有限观察：

- **模型接入与兼容性配置**是当前被明确打磨的方向：OpenAI 兼容 Provider 的配置语义（base URL、model ID、环境变量优先级）正在被文档化，说明多 Provider / 私有化部署场景的实际使用量已足以催生系统性文档需求。
- 文档国际化（中英同步）被视为一等公民，反映社区用户构成的中英双语特征。

> 建议：若要形成有统计意义的需求趋势，需拉取更长周期的 Issue 数据（如按 label、reaction 数、评论数排序）。

---

## 6. 开发者关注点

同样受限于当日数据量，仅能给出**基于单条数据的谨慎推论**：

- **配置歧义是接入阶段的主要摩擦点**：base URL 语义、model ID 取值、环境变量与配置文件的覆盖关系，属于"看一眼文档就能省一次 debug"的典型痛点。
- **`openai_legacy` 与 `openai_responses` 双模式并存**，意味着用户在选择接入方式时需要更清晰的对照说明，二者行为差异应成为后续文档与错误提示的重点。
- 该 PR 尚无社区互动，暂无法判断是否存在更广泛的同类抱怨；建议维护者关注合并后是否出现相关补充反馈。

---

## 数据说明

本期数据窗口内样本量极小（Releases 0、Issues 0、PR 1），报告第 3、5、6 部分无法按要求提供 10 条量级的清单。本日报坚持**不为凑数而生成虚构条目**，如需完整趋势分析，请提供更长统计周期或补充数据源。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 · 2026-09-14

---

## 一、今日速览

今日无新版本发布，社区动态主要集中在**稳定性回归**与**UI 强制迁移**两大议题上：v1.18.30 出现导致所有 prompt 崩溃的 `TypeError` 严重回归（#48645、#48803），同时大量用户集中反馈"新版布局强制生效且无法回退"（#48835、#48837、#48866）。此外，Zen 平台 `Muse Spark` 系列模型因 `encrypted_content` 报错持续影响多用户（#48741、#48805、#48864），成为当日的另一个焦点。PR 侧则是一批 8 月中旬提交的 PR 集中进入 `automated-pr-cleanup` 清理并关闭。

---

## 二、版本发布

过去 24 小时内无新 Release。

---

## 三、社区热点 Issues（10 项）

### 1. #4283 复制到剪贴板功能失效（长期未解决）
- 评论 **133**，👍 **124**，为社区互动量最高的 Issue
- 自 2025-11 起持续存在，v1.0.62 复现，选中回复文本无法复制
- 重要性：基础交互功能长期失效，是当前社区情绪最集中的"老账"
- https://github.com/anomalyco/opencode/issues/4283

### 2. #23153 [FEATURE] 支持加密货币支付 OpenCode Go
- 评论 22，👍 **51**
- 用户请求为 Go 订阅增加 crypto 支付入口，反映出付费习惯多元化的诉求
- https://github.com/anomalyco/opencode/issues/23153

### 3. #48741 [2.0] Muse Spark 系列在图片输入 / 工具调用时出现 Zen 严重错误
- 评论 21，当日创建即高热
- 报错：`reasoning encrypted_content was not issued to this caller`，影响 Zen 上全部 Muse Spark 模型
- 版本：0.0.0-beta-18050
- https://github.com/anomalyco/opencode/issues/48741

### 4. #43277 会话永久卡死，且重启系统也无法恢复
- 评论 14
- 多个 session 在使用中进入"拒绝新消息"状态，**重启服务甚至重启系统均无法清除**
- 重要性：属于数据/状态层持久性 Bug，破坏性高
- https://github.com/anomalyco/opencode/issues/43277

### 5. #48645 / #48803 v1.18.30 全量 prompt 崩溃回归
- 两独立报告（评论 4 / 3），错误为 `SystemPrompt.environment` 中 `a.name` 的 `TypeError`
- 全新会话、第一条消息即失败；A/B 验证 1.18.18、1.18.20 正常
- 重要性：**升级即不可用**，属最高优先级回归，且已有两人独立复现
- https://github.com/anomalyco/opencode/issues/48645
- https://github.com/anomalyco/opencode/issues/48803

### 6. #48835 / #48837 / #48866 新版布局强制迁移引发强烈反弹
- #48835：旧布局被移除，但新布局**不支持多 worktree**
- #48837：V2 界面破坏 20+ 会话的多项目 / 多 Agent 工作流，作者称"摧毁生产力"
- #48866：用户长期锁定 1.17.x 规避新布局，仍被自动升级强制切换
- 重要性：开发者工作流核心体验受损，是当日声量最大的产品决策争议
- https://github.com/anomalyco/opencode/issues/48835
- https://github.com/anomalyco/opencode/issues/48837
- https://github.com/anomalyco/opencode/issues/48866

### 7. #36423 [2.0] 后台 subagent 缺少取消能力
- 评论 5，👍 4
- v2 中 `subagent` 可启动并返回 sessionID，但**没有任何方式取消运行中的后台子代理**
- 重要性：长任务失控时代价高，是 Agent 编排能力的关键缺口
- https://github.com/anomalyco/opencode/issues/36423

### 8. #48073 Gemini 拒绝含 nullable array schema 的 MCP 工具
- 评论 2
- `@sylphx/pdf-reader-mcp` 启用后，Gemini 对**所有函数声明**做前置校验，单个不兼容 schema 导致全部请求 400
- 重要性：MCP 生态与模型侧 schema 兼容性的典型阻塞问题
- https://github.com/anomalyco/opencode/issues/48073

### 9. #34442 Windows Desktop 离线安装包损坏：未内置 ripgrep
- 评论 3，👍 4
- 无网络环境下 `grep`、`glob`、`skill` 三个内置工具及 `customize-opencode` 技能全部失效
- 重要性：企业内网 / 离线场景的"开箱即坏"，影响面广
- https://github.com/anomalyco/opencode/issues/34442

### 10. #48848 Snapshot Git 事务跨进程竞态，残留 index.lock 永久卡死快照
- 评论 2，基于最新 `dev`（`95daf90`）
- 同一 worktree 内多进程 snapshot 操作互相竞争，一次 stale `index.lock` 即导致快照永久不可用
- 重要性：直指快照机制的核心并发缺陷
- https://github.com/anomalyco/opencode/issues/48848

> 其他值得留意：#47458（V2 插件工具静默丢弃 HTTPS/file 附件）、#42324（多步工具调用 token 计数被覆盖而非累加）、#37353（Windows+WSL 下全局状态 JSON 损坏导致白屏）、#38529（会话列表混入无关非 git 目录）。

---

## 四、重要 PR 进展（10 项）

> 今日更新的 50 个 PR 均为 **CLOSED**，绝大多数由 `[automated-pr-cleanup]` 流程在 9-13 批量关闭（创建于 2026-08-13）。以下为其中技术价值较高的条目。

| # | PR | 内容 |
|---|---|---|
| 1 | [#48341](https://github.com/anomalyco/opencode/pull/48341) | **docs: 修正 v2 formatter 文档** — V2 格式化与配置页仍称格式化"未实现"，实际 #39564 已落地 |
| 2 | [#42372](https://github.com/anomalyco/opencode/pull/42372) | **上下文指示器显示 tokens/秒** — 在会话头部进度圈旁增加吞吐速率，轻量 UX 增强 |
| 3 | [#42365](https://github.com/anomalyco/opencode/pull/42365) | **docs(go): Grok 4.5 改用 Responses 端点** — 同步更新 `@ai-sdk/openai` 依赖 |
| 4 | [#42364](https://github.com/anomalyco/opencode/pull/42364) | **fix(desktop): 打包版忽略 renderer override** — 打包应用中禁用 `ELECTRON_RENDERER_URL`，统一受信来源校验 |
| 5 | [#42355](https://github.com/anomalyco/opencode/pull/42355) | **fix(config): 容忍缺失的 file 变量** — `{file:...}` 缺失时回落为空串，而非启动失败（Closes #15033） |
| 6 | [#42340](https://github.com/anomalyco/opencode/pull/42340) | **fix(cli): `run` 配额耗尽时不再静默挂起** — 此前 `opencode run` 会无限休眠、无输出（Closes #40747） |
| 7 | [#42326](https://github.com/anomalyco/opencode/pull/42326) | **fix(opencode): 累加而非覆盖 step tokens** — 修复 `processor.ts` 在 `step-finish` 覆盖 token 计数（Closes #42324） |
| 8 | [#42317](https://github.com/anomalyco/opencode/pull/42317) | **fix(opencode): system prompt 加入 Agent 身份** — 模型此前不知道自己以哪个 Agent 运行（Fixes #42125） |
| 9 | [#42310](https://github.com/anomalyco/opencode/pull/42310) | **fix(opencode): auto 权限级联到子 Agent 会话** — `opencode run` 生成子 Agent 时权限请求归属子会话，此前仅过滤根会话（Fixes #41730） |
| 10 | [#42296](https://github.com/anomalyco/opencode/pull/42296) | **fix(opencode): 移除签名 reasoning 块之间的空文本分隔符** — 避免 Anthropic 因 assistant 消息被修改而拒绝签名 thinking 块（Closes #41738） |

其他已关闭修复：#42319（snapshot 私有 Git index 损坏自恢复）、#42309（配置解析错误指向原始文本）、#42303（工具参数截断提示）、#42297（prompt 编辑器重建后光标错位）、#42331（目录级 auto-accept 设置）、#42327（直达 session 路由注册项目）。

---

## 五、功能需求趋势

综合过去 24 小时全部 Issues，社区关注方向可归纳为五类：

1. **UI/UX 迁移与工作流连续性（最强声量）**
   新布局强制生效、旧布局彻底移除，但新布局缺失 MCP 开关（#46426）、不支持多 worktree（#48835）、无法承载 20+ 会话的多项目/多 Agent 场景（#48837）。用户诉求明确：**要么保留回退开关，要么补齐新布局能力**。

2. **模型/Provider 兼容性与多模型支持**
   Muse Spark 的 `encrypted_content` 报错（#48741、#48805、#48864）呈批量出现；Gemini 与 MCP 工具 schema 校验冲突（#48073）。此外 Grok 4.5 responses 端点落地（#42365）显示模型接入仍在快速扩张。

3. **Agent 编排与可控性**
   后台 subagent 无法取消（#36423）、权限未级联到子会话、Agent 身份未注入 system prompt——社区正在从"能跑"转向要求**可观测、可中断、可授权**。

4. **付费与商业化**
   Crypto 支付（#23153，👍 51）、Go 订阅配额耗尽时的 CLI 行为异常（#42340），说明付费链路是被主动关注的区域。

5. **平台健壮性（Windows / 离线 / 并发）**
   离线缺 ripgrep（#34442）、WSL+Windows 状态库分裂（#37353）、snapshot 跨进程竞态（#48848）、非 git 项目 session 路径为绝对路径导致列表不显示（#48762）。

---

## 六、开发者关注点（痛点与高频需求）

- **升级即故障的恐惧感**：v1.18.30 的 `SystemPrompt.environment` `TypeError` 让"升级后第一条消息就崩"，且用户需靠版本 A/B 对比自行定位（#48645、#48803）。配合"1.17.x 仍被自动升级到新布局"（#48866），**版本可控性与回滚机制**已成为信任级问题。

- **状态层持久化缺陷**：会话永久卡死（#43277）、全局状态 JSON 损坏导致白屏（#37353）、`session.path` 绝对路径导致会话不可见（#48762）、snapshot 残留 `index.lock` 永久锁死（#48848）——多位报告者都强调"重启无效"，指向数据模型与并发设计而非临时故障。

- **基础交互的长期欠账**：剪贴板复制（#4283，133 评论 / 124 👍）与 V2 代码块复制按钮失效（#48839）同时存在，说明复制链路在多个渲染路径上都有缺口。

- **多项目 / 多 Agent 重度用户被边缘化**：所有关于新布局的抗议（#48835、#48837）都来自同时运行数十个会话的进阶用户，他们要求的是**多 worktree、会话分组与并发可见性**，而非视觉刷新。

- **统计与账务准确性**：token 计数被覆盖（#42324）、tokens/秒 缺失（#42372）、配额耗尽时静默挂起（#42340）——用量透明度直接影响成本判断，是付费用户与团队采用的关键。

- **MCP 生态的 schema 兼容**：一个第三方 MCP server 的不兼容 schema 就能让 Gemini 全军覆没（#48073），社区期待在声明层面做校验与降级，而非整体失败。

---

*数据来源：[github.com/anomalyco/opencode](https://github.com/anomalyco/opencode) · 统计窗口：2026-09-13 → 2026-09-14*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*