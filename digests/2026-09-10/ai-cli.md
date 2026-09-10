# AI CLI 工具社区动态日报 2026-09-10

> 生成时间: 2026-09-10 00:19 UTC | 覆盖工具: 7 个

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



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-09-10）

## 今日速览

过去 24 小时仓库活跃度较低：**无新版本发布**，共 **4 条 Issue 更新**、**1 条 PR 更新**。重点风险集中在 **macOS 设备码登录流程 HTTP 500 故障**（#2638）与 **Windows Terminal 下阿拉伯语 RTL 文本渲染错乱**（#2639）；此外两个存量需求（VSCode `@` 文件排序、Kimi Web 选中引用）同日关闭。PR 侧唯一动态是 fetch 模块去重修复的收尾。

## 社区热点 Issues

> 过去 24 小时内更新的 Issue 共 4 条，全部列出。数据量偏少，未做二次筛选。

### #2638 [OPEN] /login 设备认证在浏览器批准后返回 HTTP 500（CLI v0.42.0，macOS）
- 作者：@milesbuckton | 创建：2026-09-09 | 评论：0 | 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2638
- **摘要**：macOS 上执行 `/login`，浏览器中批准设备码后，CLI 收到 HTTP 500；VS Code 扩展同样可复现，账号为免费计划。严重影响新设备认证与登录态恢复。
- **重要性**：这是最接近“阻断性故障”的问题。认证路径直接卡住用户上手流程，且横跨 CLI 与 VS Code 扩展。当前 0 评论，说明刚提交尚未获维护者响应，需持续跟进。

### #2639 [OPEN] Windows Terminal 上阿拉伯语（RTL）文本字符反转
- 作者：@lyesmke-png | 创建：2026-09-09 | 评论：0 | 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2639
- **摘要**：在交互式提示符中输入阿拉伯语时，字符显示顺序完全反转；当 AI 回复中混排阿拉伯语与拉丁文/数字时，同样出现渲染顺序错乱。
- **重要性**：暴露终端渲染层对双向文本（bidi）支持的缺失，影响阿拉伯语用户及所有使用 RTL 脚本做混合语言开发的场景。虽非核心代码逻辑 bug，但属于全球化体验欠债。

### #1270 [CLOSED] VSCode 扩展：敲入 `@` 后应优先显示已经打开的文件
- 作者：@ljyfree | 创建：2026-02-27 | 更新：2026-09-09 | 评论：1 | 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/1270
- **摘要**：版本 v0.4.3 下，在对话框中输入 `@` 选择上下文文件时，应把 VSCode 当前打开的文件排在候选列表最前，因为用户大概率要针对这些文件做分析与操作。
- **重要性**：这是一条典型的 IDE 集成体验反馈，从 2 月一直开到 9 月 9 日才关闭，生命周期较长，说明该需求优先级不高或需要跨扩展协作完成。虽然关闭，但上下文候选排序的策略仍值得产品侧借鉴。

### #2601 [CLOSED] Kimi Web：支持对 AI 回复任意选中内容进行“引用并追问”
- 作者：@topit | 创建：2026-08-11 | 更新：2026-09-09 | 评论：0 | 👍：0
- 链接：https://github.com/MoonshotAI/kimi-cli/issues/2601
- **摘要**：希望用户可以选择 AI 回复中的某段文本

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-09-10

> 数据来源：github.com/QwenLM/qwen-code | 涵盖过去 24 小时 Releases、Issues 与 PR 动态


## 一、今日速览

昨日发布正式版 **v0.23.2**（新增 Web Shell 分屏会话导航改进）以及 SDK TypeScript v0.1.11（捆绑 CLI 0.23.2）；值得关注的是，**Windows 平台 conhost.exe（ConPTY）进程泄漏问题**连续收到多项 P1 级 Issue 与针对性修复 PR，成为社区焦点之一。此外，**VS Code 扩展升级导致会话历史丢失（#11489）**再次凸显了版本升级数据兼容方面的社区痛点。


## 二、版本发布

### v0.23.2（正式版）
- **核心变更**（仅 1 项 Feature）：
  - `feat(web-shell)`：优化分屏会话导航体验，改进 split-view 下会话切换逻辑（PR [#11250](https://github.com/QwenLM/qwen-code/pull/11250) by @wensha）
- **Breaking Changes**：无
- 另含 nightly 版本 `v0.23.2-nightly.20260909.2e212144d3`，包含一项 goal 相关 bug 修复：checkpoint 超支时重试而非 stall（[#11365](https://github.com/QwenLM/qwen-code/pull/11365)）

### sdk-typescript-v0.1.11
- 捆绑 CLI 版本：0.23.2（同时发布 v0.1.11 对应 CLI 0.23.1 的说明）
- 面向 TypeScript SDK 用户，CLI 从源码构建

### cua-driver-rs-v0.20.5
- Qwen CUA Driver 预编译二进制发布
  - **macOS**：经 codesign + notarization 的通用二进制，含 `QwenCuaDriver.app`
  - **Linux**：x86_64 + arm64（glibc 2.31 起），未签名
  - **Windows**：x86_64 + arm64，未签名 UIAccess worker + 原生 SDK payload


## 三、社区热点 Issues（Top 10）

### 1. [P1/Windows] qwen-cli 泄漏 headless conhost.exe ConPTY 进程 — 12 小时积累 347 个进程 / ~2.8 GB [#11303](https://github.com/QwenLM/qwen-code/issues/11303)
- **作者**: @Andrea-Bruno | 评论: 12
- 单个 qwen-cli（VS Code Companion 内嵌实例）在 Windows 上运行 ~12 小时后产生 347 个 `conhost.exe` 子进程，占用 ~2.8 GB 内存且从未释放。社区讨论热度最高，已拆分出独立的依赖侧问题 #11352 跟踪。

### 2. [P1] daemon 回收后后台 shell 输出与唤醒通知被静默丢弃，会话卡死 [#11119](https://github.com/QwenLM/qwen-code/issues/11119)
- **作者**: @yiliang114 | 评论: 10
- `qwen serve` 托管会话中，由 `run_shell_command` 启动的后台 CI 轮询循环持续产生输出，但所在 turn 结束后输出被静默丢弃，最终会话被卡死。涉及 daemon 生命周期中的会话状态移交。

### 3. [P1] 扩展更新丢失全部会话历史（v0.21.x → v0.23.x）[#11489](https://github.com/QwenLM/qwen-code/issues/11489)
- **作者**: @alper-cevik | 评论: 4
- VS Code Companion 从 v0.21.11 升级至 0.23.1 后，侧边栏中所有会话记录消失。数据仍在 `state.vscdb`，但新版本不再读取。P1 + `status/need-information`，涉及升级路径数据兼容问题。

### 4. [P1] Windows 上 node-pty 在 shell 自然退出时泄漏 ConPTY host（conhost.exe）— blocked [#11352](https://github.com/QwenLM/qwen-code/issues/11352)
- **作者**: @yiliang114 | 评论: 4
- 从 #11303 中拆分出的依赖侧（`@lydell/node-pty`）问题：baton 在 onExit 前被擦除，导致 JS 侧无法调用 `ClosePseudoConsole`。当前被 pinned 依赖版本阻塞，等待上游修复。

### 5. [P1] TUI 静默退出：多后台代理完成时触发 React #185 [#11500](https://github.com/QwenLM/qwen-code/issues/11500)
- **作者**: @zaalipro | 评论: 3
- 多个后台子代理在短时间内相继完成时，Ink `useBoxMetrics` 布局监听器产生 setState 循环，进程直接跌落回 shell，未渲染错误。恢复后 CLI 提示“Previous session appears...”。

### 6. [P2] 被 deny 的工具"全盘否认" — 模式匹配误导模型 [#11405](https://github.com/QwenLM/qwen-code/issues/11405)（已关闭）
- **作者**: @nihil-pro | 评论: 3
- 当工具因具体 pattern（如 `Bash(npm view *)`）被拒后，错误信息过于严格，模型误认为该工具被完全禁用，不再尝试任何形式的调用。

### 7. [P3/feature] 支持远程文件夹工作流 — 客户端连接远程 daemon [#11475](https://github.com/QwenLM/qwen-code/issues/11475)
- **作者**: @yiliang114 | 评论: 3
- 请求在现有远程 Web Shell 基础上，构建“本地客户端 + 远程 daemon/工作区/代理执行”的开发模式，让 `qwen serve` 成为真正的远程开发后端。

### 8. [P3/讨论] 评估引入嵌入式 SQLite 用于 Session/Prompt 索引与持久化 [#11433](https://github.com/QwenLM/qwen-code/issues/11433)
- **作者**: @chiga0 | 评论: 3
- 针对长对话、大量 session、精确 prompt 查询、transcript 回放等场景，提议评估以 SQLite 作为索引存储，替代现有文件扫描机制。属 roadmap/session-management 下的设计讨论。

### 9. [P2] `.mcp.json` 中 `${VAR}` 占位符未展开，密钥以字面量发送 [#11499](https://github.com/QwenLM/qwen-code/issues/11499)
- **作者**: @stdray | 评论: 2
- 项目 `.mcp.json` 使用 `"Authorization": "Bearer ${MY_TOKEN}"` 格式时，环境变量未被替换，服务端收到的是字面量 `${MY_TOKEN}` 而非密钥值。涉及 MCP 配置的变量展开功能缺失。

### 10. [P1/讨论] Windows Daemon guard 拒绝工作区自身仓库（.git 为 junction/symlink）[#11503](https://github.com/QwenLM/qwen-code/issues/11503)
- **作者**: @Andrea-Bruno | 评论: 3
- 当仓库 `.git` 目录是 NTFS junction 或指向其他卷的 symlink 时，daemon guard 会拒绝所有 git 命令（包括只读的 `git status`/`git log`）。Andrea-Bruno 同时提出替代架构建议 #11504。


## 四、重要 PR 进展（Top 10）

### 1. [修复] Windows 通过内置 ConPTY 托管 shell PTY，避免 conhost.exe 孤儿化 [#11497](https://github.com/QwenLM/qwen-code/pull/11497)
- **作者**: @yiliang114（昨天新开）
- 修复方向：所有 shell 命令强制 node-pty 加载 `conpty.dll`（而非 Windows 内置 ConPTY 后端）。实测 30 条命令后不再遗留孤儿 conhost 进程，直接面向 #11303/#11352 的 P1 问题。

### 2. [功能] Web Shell 可在任务详情面板直接查看 Shell 与 Monitor 输出 [#10906](https://github.com/QwenLM/qwen-code/pull/10906)
- **作者**: @BZ-D
- Monitor stdout/stderr 与现有 Shell 捕获一并持久化，daemon 暴露限定于 live-session-owner 的 sanitized tail 端点。

### 3. [功能] Web Shell Goal 提案支持“所属轮次结束后的启动” [#11360](https://github.com/QwenLM/qwen-code/pull/11360)
- **作者**: @qqqys
- Web Shell 可在 Allow/Reject 面板中展示拟定的 Goal；批准后在该用户轮次正常结束后启动第一个工作轮。是 #11284 之后的第二个切片。

### 4. [功能] daemon 管理的会话注册入 registry，支持 peer 消息 [#11488](https://github.com/QwenLM/qwen-code/pull/11488)
- **作者**: @qqqys
- `qwen serve` 驱动的会话会出现在 `qwen sessions ps` 和另一会话的 `list_agents` 中，可按名称寻址，模型可通过 `send_message` 触达终端。为多会话协作铺路。

### 5. [功能] Web Shell 定时任务按模型和分组路由 [#11396](https://github.com/QwenLM/qwen-code/pull/11396)
- **作者**: @qqqys
- 定时任务可选择配置的模型和新建/已有 session group；路由随 durable task 持久化，同时作用于定时触发与手动 Run。

### 6. [文档] LSP 指南对齐当前行为 [#11506](https://github.com/QwenLM/qwen-code/pull/11506)
- **作者**: @harjothkhara（昨天新开）
- 更新配置、workspace trust、超时、sandbox、server 选择、诊断与文档同步行为；修正 `character` 为可选参数（默认取第一个）。

### 7. [重构] rewind 映射锚定到稳定 prompt identity 而非位置序号 [#9466](https://github.com/QwenLM/qwen-code/pull/9466)
- **作者**: @yiliang114
- 使 rewind 在 session 恢复（含 headless `-p --rewind`）等 turn 重排场景下也能正确解析目标 prompt；目前 PR 创建已超三周仍在推进。

### 8. [功能] 将 rewind 搜索的 DashScope 客户端拆为后端接口并展示页面标题 [#11490](https://github.com/QwenLM/qwen-code/pull/11490)
- **作者**: @qqqys
- 搜索结果现携带网页标题；模型被要求以 `Sources:` 块输出 `- <title> — <url>` 形式的来源列表；DashScope 搜索客户端下沉至 backend interface。

### 9. [修复] 上游无 HTTP 状态的错误应重试而非终止本轮 [#11291](https://github.com/QwenLM/qwen-code/pull/11291)
- **作者**: @wenshao
- 网关向已返回 200 的 SSE 流中推入 error 对象时，OpenAI SDK 抛出的错误不带 status。该 PR 让 retry 路径识别此类上游失败并恢复，而不是结束当前 turn。

### 10. [性能] transcript 渲染器内嵌 CSS 拆分为版本化静态资源 [#11485](https://github.com/QwenLM/qwen-code/pull/11485)
- **作者**: @yiliang114
- 导出文档通过带 nonce 的 `<link>` 从 unpkg 并行加载 `export-transcript-document.css`，配合 SRI 完整性校验，不再将样式内嵌于 JS。与 #11096/#11100 系列问题配套。

---

**其他值得关注**：
- **#9983**（@wenshao）审查沙箱：将 host-trusted state（lease 文件等）移出容器读写挂载面，防止 host git 解析错误；
- **#10455**（@qwen-code-dev-bot）：输出语言文件不可写时 CLI 启动崩溃的修复，目前 `autofix/needs-human`；
- **#11001**（@qwen-code-dev-bot）：交互式 PTY 会话测试清理时等待进程真正退出，修复测试竞态。


## 五、功能需求趋势

从全部 Issues 中提炼出社区关注度最高的功能方向：

### 🔥 方向一：Windows 平台进程生命周期治理（本周最热）
- conhost.exe/ConPTY 进程泄漏是当前社区反馈最集中、严重度最高的问题（#11303、#11352，均为 P1）
- 关联问题：daemon 对 junction/symlink 仓库的误杀（#11503）
- PR 侧已有多路修复（#11497），但部分依赖上游 node-pty（blocked）

### 🔥 方向二：Daemon / 远程开发模式（持续升温）
- 远程文件夹支持（#11475）：连接远程 daemon、管理远程 workspace/session
- 后台任务可靠性（#11119）：session runtime 回收时不得丢失后台任务输出
- daemon-managed session 需要与本地 session 完全对等的可发现性与通信能力（PR #11488）
- daemon 模式相关 issue 已形成专项标签组，文档也在补全（#11399）

### 🔥 方向三：会话数据可移植性与持久化
- VS Code 扩展升级丢历史（#11489）是 P1 事件
- Web Shell transcript 与 session 索引缓存存在规模瓶颈：64 MiB 字节预算导致热会话永远不被缓存（#11493）；SQLite 方案讨论已开启（#11433）
- export-transcript 仍需彻底移除 daemon runtime 耦合（#11100）

### 方向四：MCP 生态完善
- `${VAR}` 占位符不展开（#11499）直接影响密钥配置安全性
- MCP 相关 bug 反馈虽零散，但都是配置/协议实现层面的具体缺口

### 方向五：模型推理与工具使用语义精细化
- denial 语义过强误导模型“全盘弃用”工具（#11405）
- 上游无状态错误应触发 retry 而非结束 turn（PR #11291）
- 不同模型间切换导致会话不可用（#9452）等
- provider-configured reasoning 边界情况跟踪（#11328）


## 六、开发者关注点

### ✔️ 最集中的痛点：Windows 进程泄漏
被多次以独立 issue/PR 跟踪，说明影响真实，复现明确（12h/347 进程/2.8GB）。核心阻塞在 `@lydell/node-pty` 依赖，社区有拆分、绕行、自托管 ConPTY 多线并进。

### ✔️ 升级/数据兼容恐慌
Extension v0.21.x → v0.23.x 后会话历史消失，说明用户对会话数据持久化的信任可能被破坏，且问题发生在“数据还在但新版不读”的状态，容易引发数据安全担忧。

### ✔️ 后台任务的透明性与可观测性
后台 shell 输出在 daemon 回收后丢失、TUI 在多个后台代理完成时静默崩溃（#11500）、后台任务 spinner 不显示（#11385）——社区在做 heavy background automation，而目前 UI/会话生命周期并没有为此做好支撑。

### ✔️ 安全机制需要粒度而非“一刀切”
- Deny 规则的错误信息过于绝对，模型无法区分

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*