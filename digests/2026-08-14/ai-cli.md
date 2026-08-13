# AI CLI 工具社区动态日报 2026-08-14

> 生成时间: 2026-08-13 23:07 UTC | 覆盖工具: 7 个

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
**数据截止：2026-08-14 | 数据源：github.com/anthropics/skills**

---

## 一、热门 Skills 排行（按评论/关注度 Top 8）

> 说明：Top 50 PR 全部处于 **Open** 状态，暂无 merged/draft；以下按仓库列表关注度排序。

| # | Skill / PR | 类型 | 功能与讨论热点 | 状态 |
|---|-----------|------|---------------|------|
| 1 | **skill-creator 评估链路修复** [#1298](https://github.com/anthropics/skills/pull/1298) | 工具链缺陷修复 | `run_eval.py` 恒定报 `recall=0%`，导致描述优化循环在噪声上运行（关联 #556 及 10+ 复现）；涉及 Windows 流读取、触发检测、并行 worker 修复 | Open |
| 2 | **document-typography 文档排版** [#514](https://github.com/anthropics/skills/pull/514) | 新 Skill | AI 生成文档的孤词换行、寡段标题悬挂、编号错位等排版质量校验，社区认为"所有文档都受影响" | Open |
| 3 | **pdf 大小写引用修复** [#538](https://github.com/anthropics/skills/pull/538) | 工具链缺陷修复 | SKILL.md 中 `REFERENCE.md`→`reference.md` 等 8 处大小写不匹配，导致大小写敏感文件系统（Linux/macOS）引用失效 | Open |
| 4 | **ODT 办公文档技能** [#486](https://github.com/anthropics/skills/pull/486) | 新 Skill | OpenDocument 格式（.odt/.ods）创建、模板填充、ODT→HTML 转换，覆盖 LibreOffice/ISO 标准场景 | Open |
| 5 | **frontend-design 技能重构** [#210](https://github.com/anthropics/skills/pull/210) | 技能改进 | 提升指令可执行性与内部一致性，确保每条指令可在单次会话内被 Claude 实际遵循 | Open |
| 6 | **skill-quality / skill-security 分析器** [#83](https://github.com/anthropics/skills/pull/83) | 新元技能 | 双元技能：质量分析器（结构/文档 20%、示例、资源等五维评分）+ 安全分析器 | Open |
| 7 | **docx 修订 ID 冲突修复** [#541](https://github.com/anthropics/skills/pull/541) | 工具链缺陷修复 | OOXML `w:id` 为书签/修订/批注共享 ID 空间，硬编码低 ID 导致文档损坏（document corruption） | Open |
| 8 | **skill-creator YAML 预校验** [#539](https://github.com/anthropics/skills/pull/539) | 工具链缺陷修复 | 检测未加引号 description 中的 `:`，防止 YAML 静默截断/

---

# Claude Code 社区动态日报（2026-08-14）

## 今日速览

- 发布 v2.1.231，修复 MCP OAuth 登录时针对 Slack 等预注册 OAuth 客户端的重定向 URI 不匹配问题。
- 社区讨论焦点集中在模型行为控制（如强制停止冗长注释、尊重代词偏好）以及大量文档过时/缺失问题。
- 过去 24 小时仅 2 个 PR 更新，均为小型维护性变更（文档修正与 CI 安全加固）。

---

## 版本发布

### v2.1.231
- **修复**：MCP OAuth 登录时，针对使用预注册 OAuth 客户端（如 Slack）的服务器，修复了因重定向 URI 不匹配导致的登录失败问题。
- 链接：[v2.1.231 Release](https://github.com/anthropics/claude-code/releases)

---

## 社区热点 Issues

以下从过去 24 小时更新最活跃的 30 条 Issues 中挑选 10 条，重点关注模型行为、平台稳定性及高频文档问题。

### 1. [MODEL] Claude 覆盖用户显式代词并默认男性偏见
- **#52477** | 开放中 | 评论 12 | 👍 4
- 用户在 memory 中明确指定代词，Claude 仍覆写为男性默认，引发对 AI 偏见和指令遵循的担忧。
- 链接：[#52477](https://github.com/anthropics/claude-code/issues/52477)

### 2. [MODEL] Claude 默认输出冗长代码注释，无视停止指令
- **#65961** | 开放中 | 评论 11 | 👍 110
- 大量开发者反馈模型持续生成冗余注释，即使明确要求停止。110 个 👍 表明该问题具有普遍性。
- 链接：[#65961](https://github.com/anthropics/claude-code/issues/65961)

### 3. [BUG] Windows 11 上 Dispatch 永久卡死，无法重置到 QR 码配对状态
- **#67682** | 开放中 | 评论 5
- 移动端显示 "Can't reach your desktop" / "Asleep"，桌面端 Dispatch 无法恢复，影响 Cowork 远程使用。
- 链接：[#67682](https://github.com/anthropics/claude-code/issues/67682)

### 4. [BUG] 桌面应用切换账号后会话历史丢失（macOS）
- **#48511** | 已关闭 | 评论 4 | 👍 5
- 在 Cowork 模式和本地 Code 模式下，切换账号后历史会话全部消失，社区认为是数据持久化缺陷。
- 链接：[#48511](https://github.com/anthropics/claude-code/issues/48511)

### 5. [DOCS] 设置文档仍将 `/config` 配置指向 `~/.claude.json`，实际应为 `~/.claude/settings.json`
- **#52601** | 已关闭 | 评论 7
- 文档路径错误导致用户按旧指引配置无效，属于高频踩坑点。
- 链接：[#52601](https://github.com/anthropics/claude-code/issues/52601)

### 6. [DOCS] Worktree 文档遗漏 `/tui` 和 `/update` 的会话中命令行为
- **#51376** | 已关闭 | 评论 6
- 并行 git worktree 会话中执行命令的实际行为与文档描述不符，社区希望补充说明。
- 链接：[#51376](https://github.com/anthropics/claude-code/issues/51376)

### 7. [DOCS] 认证文档遗漏 `CLAUDE_CODE_OAUTH_TOKEN` 已设置时 `/login` 的行为
- **#52203** | 已关闭 | 评论 5
- 认证优先级和凭据管理说明不完整，开发者对 token 切换时的预期行为产生困惑。
- 链接：[#52203](https://github.com/anthropics/claude-code/issues/52203)

### 8. [DOCS] 托管插件市场限制文档遗漏 `blockedMarketplaces` 配置条目
- **#52611** | 已关闭 | 评论 5
- `blockedMarketplaces` 是实际存在的 managed setting，但文档未给出明确示例，导致配置困难。
- 链接：[#52611](https://github.com/anthropics/claude-code/issues/52611)

### 9. [DOCS] MCP 文档遗漏远程服务器 header 的环境变量展开覆盖情况
- **#52619** | 已关闭 | 评论 5
- `.mcp.json` 中远程服务器 `headers` 的 env var 展开规则未说明，影响自定义认证配置。
- 链接：[#52619](https://github.com/anthropics/claude-code/issues/52619)

### 10. [DOCS] 插件市场文档缺少“无法识别的源格式”行为说明
- **#53076** | 已关闭 | 评论 5
- 插件安装失败时对错误源格式的处理未文档化，增加排查成本。
- 链接：[#53076](https://github.com/anthropics/claude-code/issues/53076)

---

## 重要 PR 进展

当前仅 2 个 PR 在过去 24 小时有更新，以下全部列出。

### 1. 修复 CHANGELOG.md 中的重复单词
- **#86537** | 开放中
- 修正 v1.0.124 条目中 `CLAUDE_BASH_NO_LOGIN` 相关描述的 "to to" 拼写错误，纯文档变更。
- 链接：[#86537](https://github.com/anthropics/claude-code/pull/86537)

### 2. CI：对剩余 actions/checkout 和 actions/github-script 进行 SHA 固定
- **#60280** | 已关闭
- 继 #56784 后，对 6 个工作流中多个第三方 Action 进行 SHA 锁定（如 `actions/checkout@v4` 固定为 v4.3.1 对应 SHA），提升供应链安全。
- 链接：[#60280](https://github.com/anthropics/claude-code/pull/60280)

---

## 功能需求趋势

从过去 24 小时 Issues 中可提炼出以下社区关注方向：

1. **文档完善与准确性（占比最高）**
   大量 Issue（约 20+ 条）集中反映文档路径错误、缺失行为说明或描述滞后，尤其是配置、认证、MCP、插件市场等模块。

2. **模型指令遵循与个性化**
   - 用户希望 Claude 能严格遵守“停止冗长注释”等命令。
   - 对代词、身份等用户自定义信息的尊重度成为关注点。

3. **MCP 生态稳定性与易用性**
   - OAuth 认证流程（如预注册客户端、redirect URI）被版本更新专项修复。
   - 远程 MCP 服务器的 headers 动态配置与环境变量扩展需要更清晰的支持。

4. **桌面端与移动端协同体验**
   - Dispatch（远程控制）在 Windows 上的稳定性问题。
   - 桌面应用多账号之间的会话持久化与隔离。

5. **CI/CD 安全加固（PR 侧）**
   社区贡献者主动推动 GitHub Actions 的 SHA 固定，体现对供应链安全的重视。

---

## 开发者关注点

- **模型行为失控**：最突出的痛点是 Claude 无视“不要写注释”等指令，持续输出冗长注释；此外存在覆盖用户代词、默认男性偏见的案例，直接影响信任度。
- **文档滞后影响配置效率**：大量文档 Issue 指向配置路径、命令行为和认证优先级等关键信息失真，开发者需要自行追源码验证，成本极高。
- **跨平台可靠性不足**：Windows 下 Dispatch 卡死无法恢复，macOS 桌面端切换账号丢失历史会话，均属于阻塞性数据或功能问题。
- **MCP 认证流程复杂**：尽管本次版本修复了 OAuth redirect URI 问题，但开发者仍希望文档提供完整的恢复和自定义认证指引，尤其是环境变量展开和 `/mcp` 重连流程。

---
*数据来源：GitHub anthropics/claude-code，采集时间 2026-08-14。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报

**日期：2026-08-14** | 数据来源：github.com/openai/codex

---

## 今日速览

过去 24 小时内，Codex 仓库持续高频迭代：**三个 Rust alpha 版本（0.148.0-alpha.11~13）相继推送**，同时 50+ 个 Issue 和 PR 获得更新。社区讨论热度集中在 **Windows 沙箱稳定性**、**gpt-5.6-luna 新模型兼容性**（获得 36 👍）以及 **Chats 存储目录可配置化**（获得 35 👍）三大话题上。此外，大量由 `copyberry[bot]` 提交的 PR 涵盖了 MCP OAuth 配置、线程回滚、Guardian 安全增强等方向，反映出项目正在系统性地加固安全与沙箱基础设施。

---

## 版本发布

过去 24 小时推送了 **3 个 Rust alpha 版本**，均为小版本迭代：

- **rust-v0.148.0-alpha.13** — 最新 alpha 版本
- **rust-v0.148.0-alpha.12**
- **rust-v0.148.0-alpha.11**

目前仓库未附详细更新说明，建议关注后续 release notes。从同日 PR 看，可能涉及 Windows 沙箱清单嵌入、模型退役时间暴露等内核改动。

---

## 社区热点 Issues（TOP 10）

### 1. 让 "Chats" 目录可配置（#19909）
**👍 35 | 💬 17 | 状态：Open**

用户要求将 `~/Documents/Codex` 默认聊天存储目录改为可配置，因为 `~/Documents` 常被 iCloud Drive 同步，不适合存放代码项目。

🔗 https://github.com/openai/codex/issues/19909

### 2. spawn_agent 拒绝 gpt-5.6-luna（#34700）
**👍 36 | 💬 15 | 状态：Open**

Windows 版 Codex App 26.715.9868.0 / CLI 0.145.0 在启用 multi_agent_v2 后，`spawn_agent` 会拒绝新模型 `gpt-5.6-luna`，提示未知模型。新模型推送与 Agent 体系的兼容性问题引发广泛关注。

🔗 https://github.com/openai/codex/issues/34700

### 3. TUI 支持 Markdown 数学公式渲染（#18906）
**👍 22 | 💬 15 | 状态：Open**

用户希望在终端 UI 中渲染行内和块级 LaTeX 数学公式，便于在 Codex 中查看技术文档和论文内容。

🔗 https://github.com/openai/codex/issues/18906

### 4. Windows 沙箱无法启动 MSIX 版 pwsh（#35871）
**👍 3 | 💬 13 | 状态：Open**

当解析到的 shell 是 Microsoft Store（MSIX）版 PowerShell 7 时，沙箱 `CreateProcessAsUserW` 返回错误 5（拒绝访问）。Windows 拒绝在沙箱受限令牌下启动打包应用。

🔗 https://github.com/openai/codex/issues/35871

### 5. 桌面版重启后子代理状态错乱（#37563）
**👍 4 | 💬 12 | 状态：Open**

Codex Desktop 26.803.41515 应用重启后，已终止的子代理会话被错误恢复为 "Working" 状态。虽然实际任务已结束，但 UI 上仍显示运行中。

🔗 https://github.com/openai/codex/issues/37563

### 6. macOS App 启动时 OOM 崩溃（#36523）
**👍 1 | 💬 6 | 状态：Open（P0）**

自 2026-07-31 起，macOS 版 Codex/ChatGPT 在启动时因 `external-agent-import` 解析 Claude Desktop 目录中 1.73 GB 数据导致 V8 堆内存溢出崩溃。26 小时内出现 26 次崩溃报告。

🔗 https://github.com/openai/codex/issues/36523

### 7. browser.tabs.finalize() 静默终止整个应用（#35210）
**👍 0 | 💬 12 | 状态：Open**

Windows 上 Codex Desktop 调用 `browser.tabs.finalize()` 时，整个应用静默退出，无任何错误提示。影响内置浏览器自动化场景。

🔗 https://github.com/openai/codex/issues/35210

### 8. 远程 MCP 应提取 scopes_supported（#15643）
**👍 14 | 💬 7 | 状态：Open**

远程 MCP 认证中，`scopes_supported` 应从受保护资源元数据文档中提取，而非依赖静态配置。涉及 OAuth 流程的规范兼容性问题。

🔗 https://github.com/openai/codex/issues/

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-14** | 数据来源：[github/copilot-cli](https://github.com/github/copilot-cli)

---

## 1. 今日速览

v1.0.80-0 发布，新增 `--enable-mcp-server` 运行级 MCP 开关与共享会话多客户端标识；Issue 侧呈现两极化：MCP OAuth/远程连接类问题集中涌现（新增 6+ 条），同时模型推理 effort 配置相关的老 Issue（#2904、#4345）继续保持热度。值得注意的还有多起子代理模型覆盖被静默忽略的报告。

---

## 2. 版本发布

### [v1.0.80-0](https://github.com/github/copilot-cli/releases)

**新增功能：**

- **`--enable-mcp-server`**：在当前运行中重新启用设置里已禁用的 MCP 服务器，便于临时按需启用。
- **共享会话可见性增强**：在 `--ahp`（agent host protocol）模式下，加入的会话行会显示 `2 clients`（或更多）标识其他客户端已连接；`Sessions` 标签页中亦有相应展示（详情见 changelog）。

---

## 3. 社区热点 Issues（共 27 条更新，精选 10 条）

### 🔥 高热度

#### [#2904 Custom Agent YAML Frontmatter Should Support Reasoning Effort](https://github.com/github/copilot-cli/issues/2904)
- **状态**：OPEN | 作者：@brian-kelley-intel | 👍 20 | 💬 6 | 更新：08-13
- **要点**：自定义 `.agent.md` 可以通过 `model` 字段固定模型，但无法设置 per-agent 的 reasoning effort（目前仅全局 `--effort` 可用）。
- **价值**：20👍 的长期需求，社区呼声最高的配置能力缺口之一。

#### [#2133 Custom agent frontmatter `model` 字段拒绝数组语法](https://github.com/github/copilot-cli/issues/2133)
- **状态**：OPEN | 作者：@deyil | 👍 7 | 💬 4 | 更新：08-13
- **要点**：VS Code Copilot Chat 支持 `model: [a, b]` 数组语法，但 CLI 解析失败，导致 agent 加载报错。
- **价值**：跨工具兼容性问题，影响同时使用 VS Code 与 CLI 的开发者。

### 🐛 MCP 与远程连接（今日爆发区）

#### [#4480 Atlassian MCP OAuth 失败："Incompatible authorization server" — 1.0.79 回归](https://github.com/github/copilot-cli/issues/4480)
- **状态**：OPEN [triage] | 作者：@jfrost-fabric | 更新：08-13
- **要点**：从 1.0.71 升级到 1.0.79 后，连接 Atlassian 远程 MCP（`mcp.atlassian.com`）在 OAuth 发现阶段报 `Incompatible authorization server` 错误。
- **价值**：明确指向版本的回归，需紧急排查。

#### [#4472 远程 MCP token 刷新并发导致工具调用取消](https://github.com/github/copilot-cli/issues/4472)
- **状态**：OPEN [triage] | 作者：@jmtt89 | 更新：08-13
- **要点**：同一 OAuth 保护的 MCP 服务器并发调用时，若 token 过期，每个调用会独立触发刷新并各自创建新的 rmcp 服务实例，导致正在进行的调用因 "transport closed" 失败。
- **价值**：并发场景下的经典竞态问题，影响所有 OAuth 远程 MCP。

#### [#4346 MCP registry 策略 403 阻止 CI 中使用非默认 MCP 服务器](https://github.com/github/copilot-cli/issues/4346)
- **状态**：CLOSED | 作者：@ben-ogp | 👍 3 | 更新：08-13
- **要点**：GitHub Actions 中使用 `GITHUB_TOKEN`（PAT-less 方式）认证时，MCP registry 策略读取返回 403，非默认 MCP 服务器全部被阻断。
- **价值**：影响 CI/CD 自动化的核心场景，已关闭但值得追踪修复方案。

### 🤖 模型与子代理行为

#### [#4345 claude-haiku-4.5 不支持 'medium' reasoning effort](https://github.com/github/copilot-cli/issues/4345)
- **状态**：CLOSED | 作者：@indeherb | 👍 4 | 💬 5 | 更新：08-13
- **要点**：`copilot_cli_opus_medium_effort_default` 与 `copilot_cli_gpt_5_4_mini_for_explore` 同时启用时，子代理执行反复报错：`Reasoning effort 'medium' is not supported for model 'claude-haiku-4.5'`。
- **价值**：与今日新增的 [#4473](https://github.com/github/copilot-cli/issues/4473) 高度重复，说明该问题影响面广，官方虽已关闭但可能未根治。

#### [#4462 显式 code-review 子代理模型覆盖被忽略](https://github.com/github/copilot-cli/issues/4462)
- **状态**：OPEN | 作者：@mattheusbr | 更新：08-13
- **要点**：内置 `code-review` agent 配置为 `gpt-5.6-luna`，但 CLI 实际以 `gpt-5.6-sol` 启动——配置值被静默忽略。
- **价值**：模型覆盖失效问题并非个例（与 #3565、#3954 同类），开发者对"静默降级"行为非常敏感。

#### [#3954 `explore` 工具硬编码 gpt-5.4-mini，忽略自定义/DeepSeek 配置](https://github.com/github/copilot-cli/issues/3954)
- **状态**：OPEN | 作者：@Aferrara3 | 👍 3 | 更新：08-13
- **要点**：升级到 v1.0.65 后，`explore` 工具无视自定义模型端点（如 DeepSeek），强行传 `gpt-5.4-mini` 导致错误。
- **价值**：自定义模型用户的硬阻塞，与 #4462 共同反映"模型选择逻辑"的系统性缺陷。

### 📝 会话管理

#### [#4477 停止操作导致会话与提示词丢失](https://github.com/github/copilot-cli/issues/4477)
- **状态**：OPEN [triage] | 作者：@daveroama | 更新：08-13
- **要点**：用户点击停止按钮中断执行时，整个会话——包括原始提示词和修改内容——被删除，且多次复现。
- **价值**：数据丢失类严重 Bug，直接影响日常使用信心。

#### [#4474 长时间运行的 General Chat 超时后静默归档且无恢复 UI](https://github.com/github/copilot-cli/issues/4474)
- **状态**：OPEN [triage] | 作者：@VincentLi0728 | 更新：08-13
- **要点**：会话恢复超时（60秒）后，原会话被静默归档，侧边栏消失且无任何恢复入口，同时自动创建替代会话。
- **价值**：会话生命周期管理缺陷，用户会话可能"凭空消失"。

---

## 4. 重要 PR 进展

> 过去 24 小时内仅 1 个 PR 更新。

### [#4476 docs: 文档化 custom-agent effort frontmatter（Option A）](https://github.com/github/copilot-cli/pull/4476)
- **状态**：CLOSED | 作者：@romanstetsenko | 创建/更新：08-13
- **内容**：为长期 Issue #2904 的 **Option A** 方案编写文档——在自定义 agent 的 frontmatter 中新增独立的 `effort` 字段（与 `model` 平行）。README 新增 "Custom Agents" 参考章节，涵盖现有字段（`name`、`description`、`model`）及新提案。
- **分析**：虽然是 docs-only PR，但它将 #2904 的方案讨论推进到文档落地阶段，意味着官方可能在后续版本实现该配置。

---

## 5. 功能需求趋势

从全部 Issues 中提炼的社区关注方向：

| 方向 | 相关 Issues | 热度 |
|------|-------------|------|
| **MCP 生态成熟度**（OAuth 流程、远程容错、并发刷新、策略认证） | #4480, #4472, #4463, #4464, #4466, #4478, #4346 | 🔥🔥🔥 最高 |
| **模型/推理能力精细控制**（per-agent effort、模型覆盖不生效） | #2904, #4473, #4462, #3954, #3565, #2133 | 🔥🔥🔥 高 |
| **会话管理增强**（列出运行中会话、恢复 UI、状态可见性） | #4470, #4474, #4467, #4468, #4477 | 🔥🔥 中高 |
| **权限系统体验**（允许目录、hook 提示、持久化） | #4482, #4237, #4469 | 🔥🔥 中 |
| **插件/市场机制**（自动更新、技能状态展示） | #4465, #4471 | 🔥 中 |

**明确的需求信号：**

- `#4470` 提出了类似 Claude Code `claude agents --json` 的"列出所有运行中会话及状态"的 API，社区希望构建外部监控面板。
- `#4475` 请求澄清启动消息中 "No copilot-instructions.md found" 的措辞，避免用户误以为全局配置缺失。

---

## 6. 开发者关注点

**痛点 Top 5：**

1. **模型选择逻辑"不听话"**：多个报告（#4462、#3954、#3565）指向同一问题——CLI 在子代理调度时忽略显式模型配置，或静默降级到其他模型，且无任何日志提示。开发者对"静默"行为尤为不满。

2. **MCP OAuth 流程脆弱**：#4480（Atlassian 回归）、#4464（Entra scope 错误导致频繁交互登录）、#4463（Windows socket 10013）——远程 MCP 认证环节问题密度最高，且涉及不同厂商/平台。

3. **MCP 服务器容错不足**：#4466 指出一次瞬时 5xx 即导致整个会话内该服务器被永久标记失败，无重试/退避机制；#4472 的并发 token 刷新竞态同样缺乏保护。

4. **会话数据安全**：#4477 的"停止即丢会话"和 #4474 的"静默归档"都是数据丢失性质的问题，优先级应高于功能优化。

5. **权限提示的"粘性"**：#4482 发现 `allowed_directories` 配置对 shell 命令不生效（`/add-dir` 反而可以）；#4469 报告已批准的目录访问请求在每次会话恢复时重复弹出，且无法彻底消除。

**总体观察**：本周社区议题从"功能建议"转向"稳定性和信任度"——特别是 MCP 与模型调度两个核心链路的可靠性问题。v1.0.80-0 的 `--enable-mcp-server` 表明团队正在快速响应 MCP 配置灵活性需求，但远端 OAuth 与进程生命周期管理的系统性修复仍是当务之急。

---

*本日报基于 2026-08-13 至 2026-08-14 的公开 GitHub 数据自动整理，仅供参考。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# 2026-08-14 Kimi Code CLI 社区动态日报

## 今日速览
过去24小时，Kimi Code CLI 无新版本发布、无新PR合并，但有3个Issue保持活跃更新。其中，#1283 Memory System 功能需求获得38条评论，社区关注度最高；另有2个严重Bug（ACP流式响应静默挂死、单步生成88k乱码token）引发开发者担忧。整体来看，社区对「跨会话持久记忆」的呼声强烈，而流式传输可靠性与生成稳定性问题亟待官方回应。

## 版本发布
昨日无新版本发布。

## 社区热点 Issues
以下按关注度排序，列出当前值得关注的3个活跃 Issue（过去24小时内更新）。

### 1. [#1283 Feature Request: Memory System - Persistent context across sessions](https://github.com/MoonshotAI/kimi-cli/issues/1283)
- **作者**: @CatKang | 创建: 2026-02-27 | 更新: 2026-08-13 | 评论: 38
- **内容摘要**: 请求实现一套完整的**记忆系统**，使 Kimi Code CLI 能够跨会话记住上下文、项目模式与用户偏好。提案包含：
  - 自动记忆（AI 管理的笔记）
  - 手动记忆（用户通过 `c` 指令自定义持久化规则）
- **重要性**: 这是当前社区呼声最高的功能需求（38条评论），且 Issue 已存在近半年，仍保持活跃讨论。它直击 CLI 工具在长时间任务中「上下文丢失」的核心痛点，一旦实现将显著提升实际工作流效率。

### 2. [#2598 Bug: ACP/print 流式响应静默挂死](https://github.com/MoonshotAI/kimi-cli/issues/2598)
- **作者**: @ai-agent-workbench | 创建: 2026-08-09 | 更新: 2026-08-13 | 评论: 1
- **内容摘要**: 在 `kimi acp` 模式下，流式对话偶发「内容全部发送完毕后连接挂死」：
  - 客户端能收到完整答复，但 `[DONE]`/finish 帧始终不来
  - 无错误、无超时，且 CLI **没有流式空闲超时配置项**
  - 用户发送下一条消息时，挂死轮被静默顶替，已流式答复**从未写入** `wire.jsonl`
  - 官方 `config.toml` 文档确认无兜底机制；0.31.1 仅覆盖 Esc 场景
- **重要性**: ACP 模式是自动化工作流的关键接口，静默挂死且数据落盘缺失会直接导致下游链路数据丢失。该 Issue 暴露了超时机制与异常恢复的架构性缺陷，对依赖 ACP 做集成的开发者影响较大。

### 3. [#2597 Bug: 单步生成失控 — 88k tokens 乱码](https://github.com/MoonshotAI/kimi-cli/issues/2597)
- **作者**: @kdp123 | 创建: 2026-08-08 | 更新: 2026-08-13 | 评论: 1
- **内容摘要**: 正常交互会话中，模型出现**失控生成**：
  - 单个 LLM step 运行 **3214 秒（约53分钟）**
  - 输出 **88,114 个 token**，内容为无意义的乱码（随机多语言片段、损坏的 Markdown、无限重复）
- **重要性**: 单步生成 88k tokens 是极端的资源浪费（时间与费用），且严重影响用户体验。该 Bug 可能涉及解码参数异常或模型侧故障，若高频发生，将动摇用户对 CLI 稳定性的信任。

## 重要 PR 进展
过去24小时内无新 PR 更新或合并。

## 功能需求趋势
鉴于昨日活跃数据有限，以下趋势基于当前活跃 Issue 及历史上下文提炼：

- **跨会话持久记忆（Memory System）**：这是目前社区第一诉求。开发者希望 CLI 能像 Cursor 等产品一样记住项目模式和用户偏好，减少重复说明。相关讨论已持续近半年，热度未减。
- **流式传输可靠性**：`#2598` 反映的正是流式场景下的「悬挂」问题——无空闲超时、无异常兜底。社区期待官方提供可配置的流式超时时间，并保证输出完整落盘（`wire.jsonl`）。
- **生成质量护栏**：`#2597` 暴露了 LLM 单步生成失控的风险。开发者希望增加「最大 token 数硬限制」和「重复内容检测」等保护机制。

## 开发者关注点
- **可靠性 > 新功能**：3个活跃 Issue 中有2个是严重 Bug，且都关乎基础可用性（挂死、乱码）。社区现阶段更关注「稳定性和可观测性」，而非单纯堆叠新特性。
- **可观测性缺口**：流式挂死时无日志、无超时；失控生成时无中断手段。开发者期望 CLI 提供更透明的运行状态（如 step 进度、token 消耗预警）和干预入口。
- **数据完整性**：`wire.jsonl` 是调试和审计的关键凭据，但挂死轮的数据不落盘。开发者希望任何流式响应（即使异常终止）都能被完整持久化。
- **长周期 Bug 响应**：`#1283` 已存在 5 个多月，讨论活跃但未见官方排期说明。社区希望官方对高频需求给予明确的「planned/not planned」回复，以降低沟通成本。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报（2026-08-14）

## 今日速览

昨日发布 v1.18.18 补丁版本，修复了 Kimi 系统提示词选择错误及 xAI 模型高推理强度的问题；社区层面，关于保留旧版布局的讨论持续升温（#37012，37 评论/41 赞），而多项安全相关议题（升级脚本完整性、SSRF、上下文裁剪）同日密集出现，值得关注。

## 版本发布

**v1.18.18**（过去 24 小时）

Core:
- 修复官方 Moonshot 和 Kimi Provider 的 Kimi 系统提示词选择错误
- 修复 xAI 模型的 xhigh reasoning effort 问题

## 社区热点 Issues

1. **[#37012 保留旧版布局选项（FEATURE）](https://github.com/anomalyco/opencode/issues/37012)** — 37 评论 / 41 👍
   用户呼吁在新版中保留旧布局，指出旧版从主窗口可直接访问几乎所有功能，无需在应用内多次导航；同时强调工作区（workspace）能力的重要性。社区反响强烈，是目前最受关注的功能请求。

2. **[#41470 剪贴板复制在 VSCode Server 中失效](https://github.com/anomalyco/opencode/issues/41470)** — 15 评论
   在 Docker 环境下的 VSCode Server 中使用 OpenCode 时，显示 "Copied to clipboard" 但实际并未写入系统剪贴板，文本无法粘贴到其他应用。影响远程开发场景。

3. **[#25630 plugin provider.models() 钩子回归（REGRESSION）](https://github.com/anomalyco/opencode/issues/25630)** — 15 评论
   PR #25167 合并后，插件 `provider.models()` 钩子无法再为自定义 provider 填充模型。影响所有通过插件扩展模型列表的用户。

4. **[#6719 新增 /reload 命令（FEATURE）](https://github.com/anomalyco/opencode/issues/6719)** — 15 评论 / 77 👍
   请求新增 `/reload` 命令，用于重新加载全局和项目级 `opencode.jsonc` 配置文件及 `.opencode/` 目录内容。是社区点赞数最高的功能请求之一。

5. **[#18694 TypeScript LSP 无法处理子目录 package.json](https://github.com/anomalyco/opencode/issues/18694)** — 7 评论
   在 Go + React TypeScript 混合项目中，若 `package.json` 和 `node_modules` 位于 `/web` 子目录，从仓库根目录运行 OpenCode 时不会启用 TS 语言服务。多语言项目结构的常见痛点。

6. **[#42083 GitHub Copilot Provider 模型显示为零](https://github.com/anomalyco/opencode/issues/42083)** — 5 评论
   opencode 1.18.15 中 `github-copilot` provider 登录成功但模型选择器不显示任何模型，`opencode models` 返回 "Provider not found"，Copilot 用户无法使用。

7. **[#26091 LLM 响应头被丢弃，插件无法访问路由元数据](https://github.com/anomalyco/opencode/issues/26091)** — 4 评论
   使用 LiteLLM 代理的自动路由器（如复杂度路由、语义路由）时，实际选择的模型信息在 HTTP 响应头（如 `x-litellm-model-api-base`）中返回，但这些头部被 OpenCode 丢弃，导致插件无法感知实际路由结果。

8. **[#42434 安全：opencode upgrade curl|bash 无完整性校验](https://github.com/anomalyco/opencode/issues/42434)** — 3 评论
   `opencode upgrade` 直接获取远程脚本并管道到 bash 执行，无任何完整性验证（curl|bash 模式），存在供应链/TOCTOU 攻击风险，属于中危安全问题。

9. **[#42437 安全：上下文裁剪静默丢弃指令性内容](https://github.com/anomalyco/opencode/issues/42437)** — 2 评论
   上下文压缩（session/compaction）在静默丢弃包含指令或约束的内容时，可能导致模型的约束被绕过。被标记为中高危安全问题。

10. **[#42260 opencode2 破坏 V1 数据库共存](https://github.com/anomalyco/opencode/issues/42260)** — 2 评论
    opencode2 迁移数据库 schema 后，opencode 1.x 的 `/move` 命令损坏，会话被困在 worktree 中。影响同时使用 V1 和 V2 的用户。

## 重要 PR 进展

1. **[#42433 保留 response model 元数据](https://github.com/anomalyco/opencode/pull/42433)**
   修复 #42420：保存 AI SDK 返回的结构化模型 ID，使客户端能看到实际响应的模型而非仅请求别名。与 #26091 相关但范围更窄。

2. **[#42424 模型 fallback 链（NEW FEATURE）](https://github.com/anomalyco/opencode/pull/42424)**
   关闭 #10287：当主模型重试耗尽后，自动按配置尝试 fallback 模型，避免因单个模型持续故障导致任务失败。

3. **[#42425 agent_memory 表与 memory-tools 插件](https://github.com/anomalyco/opencode/pull/42425)**
   关闭 #41998：新增 `agent_memory` 表和 `memory-tools` 插件，支持通过 Supabase 云端备份/恢复 OpenCode AgentMemory。

4. **[#42427 插件自动更新与临时残留清理](https://github.com/anomalyco/opencode/pull/42427)**
   关闭 #16608：修复插件 `@latest` 自动更新卡住的问题，直接通过 registry.npmjs.org 获取 dist-tags.latest，并在 npm install 后清理临时残留文件。

5. **[#42428 Kimi K2.6（k2p6）模型检测修复](https://github.com/anomalyco/opencode/pull/42428)**
   关闭 #23933：新增 `kimi-for-coding` 自定义 handler，修复多个代码路径无法正确处理 Kimi K2.6 模型 ID 的问题。

6. **[#42430 插件 config 钩子在 skill 发现前执行](https://github.com/anomalyco/opencode/pull/42430)**
   关闭 #28646：确保插件 `config()` 钩子（如 superpowers）对 `config.skills.paths` 的修改在 skill 发现流程前生效。

7. **[#42431 MCP 连接重试应对并行竞争条件](https://github.com/anomalyco/opencode/pull/42431)**
   关闭 #41996：修复 `concurrency: "unbounded"` 下并行启动 MCP server 时的间歇性 "Connection closed" 错误。

8. **[#42429 WSL 模式下 MCP 命令包装](https://github.com/anomalyco/opencode/pull/42429)**
   关闭 #28159：修复 Windows 桌面版开启 WSL 模式后，MCP local 命令引用 Linux 可执行文件但在 Windows sidecar 环境找不到的问题。

9. **[#42422 健康检查指数退避重试](https://github.com/anomalyco/opencode/pull/42422)**
   关闭 #24142：桌面版健康检查在慢速机器上可能因服务端尚未就绪而失败，增加指数退避重试逻辑。

10. **[#38790 新布局工作区 Flow（BETA）](https://github.com/anomalyco/opencode/pull/38790)**
    为优化后的新版布局添加工作区选择流程：支持本地仓库、新建隔离工作区、或已有工作区三种会话启动方式，并增强 composer 的上下文感知。

## 功能需求趋势

- **布局与 UI 定制**：旧布局保留诉求强烈（#37012），同时有 TUI 右侧边栏显示后台 subagent 活动（#42369）、会话内输出风格切换器（#42414）等新提议。
- **安全加固**：多个安全问题同日被提出——升级脚本完整性验证（#42434）、webfetch 的 SSRF 防护（#42435）、上下文裁剪的指令完整性风险（#42437）。安全已成为社区关注焦点。
- **模型与 Provider 支持**：GitHub Copilot 集成故障（#42083）、Kimi K2.6 模型检测修复（#42428）、xAI 推理强度修复（v1.18.18），模型生态的稳定支持持续受到关注。
- **插件系统可靠性**：插件 `provider.models()` 钩子回归（#25630）、插件依赖漂移（#30526）、手动插件更新命令（#18544）等，插件机制的健壮性是长期议题。
- **会话与上下文管理**：`/reload` 命令（#6719）、V1/V2 数据库共存（#42260）、上下文裁剪策略（#42437）、标题生成污染（#42386）等，反映用户对会话生命周期控制的需求。

## 开发者关注点

- **VSCode Server 环境剪贴板失效**（#41470）：远程开发是重要使用场景，此问题直接影响开发效率。
- **插件回归风险**：#25630 的 `provider.models()` 回归说明核心改动容易影响插件生态，开发者希望有更完善的兼容性保障。
- **配置与模型发现体验**：GitHub Copilot 集成异常（#42083）、子目录语言服务识别（#18694）等问题，暴露出多语言、多 provider 场景下的体验短板。
- **任务卡死与超时控制**：Task 工具超时可配置（#36755）、无限重试循环问题（#29143），开发者期待更可控的任务执行机制。
- **数据库迁移兼容性**：opencode2 破坏 V1 数据库（#42260），提示在引入重大变更时需考虑旧版本共存路径，这也是阻碍用户升级的潜在因素。
- **上下文质量**：内存 MCP 注入污染会话标题（#23114、#42386）和上下文裁剪丢弃指令（#42437），直接影响模型输出的正确性，需要更精细的控制策略。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 2026-08-14

## 今日速览

过去 24 小时内 Qwen Code 发布两版更新：正式版 v0.21.11 落地了 Agent Plugins v1 和原生多代理 `/coordinate` 命令，预览版 v0.21.12-preview.1 则带来 Web Shell 的工作区文件上传等修复。社区讨论焦点集中在本周多代理（fleet）路线图的密集推进、Windows 平台两个 P1 级回归（CLI 粘贴失效、桌面版弹出终端）、以及 Google Vertex AI 认证在 headless 场景下的稳定问题。此外，v0.21.11 的 SWE-bench Verified 结果被标记为 QUARANTINED（500 题完成 0 解决），需要关注后续说明。

## 版本发布

### v0.21.12-preview.1（预览版）
- **fix(web-shell): preserve standalone session target** — 修复 Web Shell 独立会话目标丢失的问题（[#9038](https://github.com/QwenLM/qwen-code/pull/9038)）
- **feat(web-shell): support workspace file uploads** — Web Shell 支持向工作区上传文件

### v0.21.11（正式版）
- **Agent Plugins v1** — 新增插件机制，可扩展 Agent 能力（[#8834](https://github.com/QwenLM/qwen-code/pull/8834)）
- **原生多代理工作流** — 通过 `/coordinate` 命令实现带有只读 teammate 的多代理协作（[#8804](https://github.com/QwenLM/qwen-code/pull/8804)）
- **SWE-bench Verified 状态：QUARANTINED** — 500/500 完成，0 resolved，结果被隔离待查（non-production E2E 验证，非正式发布阻断）

---

## 社区热点 Issues（10 个）

### 1. RFC: Native coordination for independent Qwen sessions（#8718）⭐️ 多代理路线图核心
- **作者**: @yiliang114 | 评论 9 | [链接](https://github.com/QwenLM/qwen-code/issues/8718)
- **动态**: 已 CLOSED，但作为多代理工作总纲，衍生了 #8840-#8843 等 8 个阶段任务，v0.21.11 的 `/coordinate` 是其首批落地成果。社区关注度高，讨论围绕 leader 如何在保持交互的同时调度多个 worker 并收集结构化结果。

### 2. fix(serve): Preserve current session when large restore times out（#8678）🟡 P1
- **作者**: @doudouOUC | 评论 8 | [链接](https://github.com/QwenLM/qwen-code/issues/8678)
- **动态**: P1 级会话管理 bug。PR1（#8691）已合入实现 timeout 契约和安全恢复，但当前 issue 仍 OPEN，剩余工作涉及大 session 恢复超时后的现场保留。社区重点关注恢复过程的可观测性和数据安全。

### 3. Gemini 2.5 models unusable on Vertex AI: thinkingLevel always sent（#9019）
- **作者**: @axiom-of-choice | 评论 5 | [链接](https://github.com/QwenLM/qwen-code/issues/9019)
- **动态**: 通过 `vertex-ai` 认证的 Gemini 2.5 请求全部失败，因为请求总是携带 `thinking_level` 参数（包括 UNSPECIFIED 占位符），该模型不支持。影响所有使用 Gemini 2.5 + Vertex AI 的用户，社区给出了复现步骤，等待修复。

### 4. Keyless Vertex AI is not inferred from environment（#9025）
- **作者**: @axiom-of-choice | 评论 5 | [链接](https://github.com/QwenLM/qwen-code/issues/9025)
- **动态**: 纯环境变量配置的 keyless Vertex AI（ADC）无法被 `getAuthTypeFromEnv` 识别，导致 headless 运行在启动时退出。与 #9019

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*