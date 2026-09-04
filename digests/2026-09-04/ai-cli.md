# AI CLI 工具社区动态日报 2026-09-04

> 生成时间: 2026-09-04 00:10 UTC | 覆盖工具: 7 个

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

# OpenAI Codex 社区动态日报（2026-09-04）

## 今日速览

昨日 Codex 团队密集合入了 GPT-6-Astra 模型目录、macOS 沙箱加固、Vim 模式修复等一批 PR，并发布 rust-v0.153.2 补丁。社区侧 Windows 平台问题持续高热，Computer Use 截图失败、WSL 项目创建失败、桌面宠物点击穿透等 Issue 讨论最为活跃。

## 版本发布

昨日共发布 3 个稳定版补丁及 3 个 alpha 版本，主要内容集中在 GPT-6-Astra 模型目录支持与 Vim 模式功能增强。

- **rust-v0.153.2**：修正 GPT-6-Astra Fast tier 描述文本，由 “1.5x speed” 更正为 “2x speed, increased usage”，仅影响展示文字，不改变请求行为。 [查看详情](https://github.com/openai/codex/compare/rust-v0.153.1...rust-v0.153.2)
- **rust-v0.153.1**：支持通过 API 配置 GPT-6-Astra，无需更改默认模型，且不会显示在模型选择器中。 [查看详情](https://github.com/openai/codex/compare/rust-v0.153.0...rust-v0.153.1)
- **rust-v0.153.0**：Vim 模式新增 `u` 撤销与 `Ctrl+R` 重做，完整保留草稿内容（含粘贴内容和附件）；插件 CLI 支持列表、安装与删除等操作。 [查看详情](https://github.com/openai/codex/compare/rust-v0.152.0...rust-v0.153.0)
- **rust-v0.154.0-alpha.1 / alpha.2 / rust-v0.153.0-alpha.5.1**：三个 alpha 版本发布，无详细更新说明。 [详情](https://github.com/openai/codex/releases)

## 社区热点 Issues

以下为过去 24 小时更新最活跃或影响力最高的 10 个 Issue。

1. **[#25178] Windows Computer Use 截图失败：SetIsBorderRequired 接口不兼容**（评论 38，👍 17）
   Windows 10 22H2 上 Computer Use 无法执行截图，错误为 `SetIsBorderRequired failed: 不支持此接口 (0x80004002)`。作为评论数最高的 Issue，说明 Windows 桌面端功能在旧系统上的兼容性仍是重要短板。 [链接](https://github.com/openai/codex/issues/25178)

2. **[#35746] 分页历史记录丢失有效 rollout 数据并重用序号**（评论 35）
   分页 rollout 历史解码不一致，会丢弃有效的 flattened rollout 记录并复用重复序号，影响会话历史的完整性与可信度。 [链接](https://github.com/openai/codex/issues/35746)

3. **[#34061] Subagents 导致 Codex 磁盘占用异常飙升**（评论 24，👍 5）
   用户报告 0.144.6 版本在 macOS 上使用 subagents 时磁盘占用急剧增加，Pro 订阅、gpt-5.6 模型环境复现。 [链接](https://github.com/openai/codex/issues/34061)

4. **[#41463] Windows + WSL 下无法创建项目：AbsolutePathBuf 缺少根路径**（评论 22，👍 12）
   Codex Desktop 在 Windows 配合 WSL2 使用时创建项目失败，路径反序列化缺少 base path。👍 数较高，反映 WSL 用户群体对此痛点高度关注。 [链接](https://github.com/openai/codex/issues/41463)

5. **[#41220] [Meta] Codex 用量/配额异常消耗追踪**（评论 18，👍 9）
   多个用户报告订阅配额或购买的 credits 消耗速度远超往日水平，与本地 token 使用证据不符。该 Issue 作为 cross-report 汇总帖出现，具有系统性风险特征。 [链接](https://github.com/openai/codex/issues/41220)

6. **[#17318] 无法更改模型和 reasoning effort**（评论 19，👍 30）
   macOS Codex 桌面版在部分情况下无法切换模型或调整推理强度。👍 30 为当前 Issue 中最高，说明这是高频困扰用户的设置问题。 [链接](https://github.com/openai/codex/issues/17318)

7. **[#35458] 桌面端截图重复持久化导致 ~/.codex/sessions 膨胀至 165 GiB**（评论 15）
   Compaction 时截图被全量重复保存并被 subagent fork 继承，95% 为 base64 图片数据。触目惊心的存储浪费案例，是典型的上下文管理缺陷。 [链接](https://github.com/openai/codex/issues/35458)

8. **[#41513] Windows 桌面宠物（Pets）点击穿透无法拖拽**（评论 21，👍 8）
   内置宠物 Codey 和自定义宠物均出现点击穿透现象。Windows 宠物功能短时间内出现多个相似 report（另一条 #41960 评论 9 / 👍 10），判定为较普遍的新功能回归。 [链接](https://github.com/openai/codex/issues/41513)

9. **[#40782] macOS 更新后全局 UI 文字变细且模糊**（评论 14，👍 4）
   26.820.60940 版本更新后出现文字渲染异常，中文界面下更明显。UI 渲染回归直接影响日常使用体验。 [链接](https://github.com/openai/codex/issues/40782)

10. **[#38944] MCP OAuth 因 issuer 不匹配被阻断，建议支持 per-server issuer 覆盖**（评论 8，👍 9）
    远程 MCP 服务器返回的 authorization-server metadata 与实际 issuer 不一致时无法完成 OAuth。属于企业级 MCP 应用的关键阻塞。 [链接](https://github.com/openai/codex/issues/38944)

## 重要 PR 进展

以下 10 个 PR 反映了 Codex 在模型支持、安全加固和 TUI 体验方面的核心变化。

1. **[#42607] Add GPT-6-Astra to bundled model catalog**
   将隐藏的 `gpt-6-astra` 模型加入内置模型目录，包含推理等级、工具能力、上下文限制、agent 指令与审查策略，并重新排序已有模型优先级。 [链接](https://github.com/openai/codex/pull/42607)

2. **[#42619] Add GPT-6-Astra to Amazon Bedrock catalogs**
   将 `openai.gpt-6-astra` 加入 Bedrock 模型目录，包含 global 与 US cross-region 变体，保留内置元数据的同时应用 Bedrock 特定能力标识。 [链接](https://github.com/openai/codex/pull/42619)

3. **[#42590] Harden the macOS sandbox against terminal input injection**
   沙箱命令继承用户 controlling terminal，子进程可用 `TIOCSTI` 向 Codex 退出后的未沙箱 shell 注入输入。通过追加 `file-ioctl` 限制进行加固。 [链接](https://github.com/openai/codex/pull/42590)

4. **[#42606] Support trusted headers for remote exec WebSockets**
   为远程 exec-server WebSocket 握手添加可信 HTTP 头支持，跨会话重连保留请求头，同时对敏感值进行脱敏。 [链接](https://github.com/openai/codex/pull/42606)

5. **[#42623] Bound Noise handshakes by the exec server initialization timeout**
   将 Noise 握手与 JSON-RPC `initialize` 请求超时统一到配置的初始化超时时间内，提升远程执行环境的稳定性。 [链接](https://github.com/openai/codex/pull/42623)

6. **[#42598] Report MCP tool discovery errors in server status**
   修复空工具列表无法区分“成功返回空目录”与“服务器启动失败”的问题，在 `mcpServerStatus/list` 中新增 `toolsError` 字段。 [链接](https://github.com/openai/codex/pull/42598)

7. **[#42584] Recover Vim escape input in legacy terminals**
   解决旧终端将 `Alt+字符` 与 `Esc` 后跟字符编码相同的问题，避免 Vim insert/replace 模式下指令状态错乱。 [链接](https://github.com/openai/codex/pull/42584)

8. **[#42609] Condense TUI startup warnings**
   将配置、技能、sandbox、MCP 启动诊断合并为会话头下方的单一摘要（含 MCP 与登录计数），完整告警保留在 transcript 中，简化启动界面。 [链接](https://github.com/openai/codex/pull/42609)

9. **[#42588] Require Guardian review for incompatible compaction checkpoints**
   当 parental compaction 的 producer hash 与当前 scoring model 不匹配时，禁止复用异步评分结果，必须重新进行 Guardian 审查，防止跨模型安全审查绕过。 [链接](https://github.com/openai/codex/pull/42588)

10. **[#42577] Preserve target-native paths in command approvals**
    命令审批请求改为传递所选 executor 的 `PathUri` 而非 host-native 路径，避免远程/沙箱环境中路径语义错误。 [链接](https://github.com/openai/codex/pull/42577)

## 功能需求趋势

从近期 Issues 和 PR 可以提炼出四个方向的社区诉求：

- **新模型支持（GPT-6-Astra 落地）**：模型目录、Bedrock 接入、API 隐藏配置、Fast tier 描述等多个 PR 和 release 同步推进，说明新模型上线前的收尾正在密集进行。开发者期待的是无缝的模型切换体验。
- **Windows 平台功能完善**：Computer Use、Pets、WSL 集成、桌面空白等问题集中在 Windows 侧，说明 Codex 桌面端的 Windows 版本在功能完整性上与 macOS 存在明显差距，且系统版本兼容性覆盖不足。
- **MCP 生态可靠性**：OAuth issuer 校验失败、工具装载不全、发现错误不可见等 Issue 频出，开发者对 MCP 的诉求已从“能否接入”转向“接入后是否稳定、可诊断”。
- **数据与配额透明度**：配额异常消耗、会话历史不一致、磁盘占用失控等问题本质上反映同一个需求——开发者希望 Codex 的用量记录、历史数据和本地存储行为透明可预期。

## 开发者关注点

高频痛点集中在以下方面：

- **桌面端稳定性**：Windows 上宠物点击穿透（#41513、#41960）、空白窗口（#42547）、崩溃（#41581）等多条独立报告相互印证，桌面端功能在发布前缺乏充分的 Windows 真机测试。相关讨论：[#41513](https://github.com/openai/codex/issues/41513)、[#41960](https://github.com/openai/codex/issues/41960)
- **存储与磁盘空间**：~/.codex/sessions 膨胀至 165 GiB（#35458）、subagent 磁盘占用飙升（#34061），用户担心无限增长的本地数据会拖垮开发机。
- **配额/用量异常**：多人反馈配额消耗速度与本地记录不一致（#41220），该问题直接关系用户成本，情绪反应通常最激烈。
- **会话历史与数据一致性**：分页历史记录丢失、重复序号、ghost 会话

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-09-04

## 1. 今日速览

过去 24 小时无新版本发布，社区动态集中于**安全加固 PR 密集提交**与**核心稳定性问题持续发酵**。多个高优先级 PR（如路径穿越修复 #29192、NTFS 短文件名绕过 #29116）直指文件系统边界校验漏洞；与此同时，Subagent 误报成功（#22323）与 Generalist agent 挂起（#21409）等 P1 级 Bug 仍是开发者吐槽焦点。

---

## 2. 版本发布

过去 24 小时无新 Release。

---

## 3. 社区热点 Issues

### ① Subagent 达到 MAX_TURNS 后被误报为 GOAL 成功
**#22323** | P1, Bug | 评论 13 | 👍 2
`codebase_investigator` 子代理在尚未开始分析时就因 max turn 被中断，却向主会话报告 `status: "success"` / `Termination Reason: "GOAL"`，**掩盖了真实的中断原因**。社区担心这会导致用户对子代理结果产生错误信任，尤其在自动化流水线中可能造成隐性故障。链接：https://github.com/google-gemini/gemini-cli/issues/22323

### ② Generalist agent 无限挂起
**#21409** | P1, Bug | 评论 8 | 👍 8
多个用户反馈 Gemini CLI 在委派 generalist agent 时永久挂起，连简单的“创建文件夹”都无法完成。workaround 是手动指示模型不要委派子代理——但这令 sub-agent 机制形同虚设。链接：https://github.com/google-gemini/gemini-cli/issues/21409

### ③ 零依赖 OS 沙箱 + 意图路由（模型原生的 bash 亲和力）
**#19873** | P2, Enhancement | 评论 9 | 👍 1
议题提出 Gemini 3 模型本质上是“原生 bash 用户”，建议通过零依赖 OS 沙箱在保证安全的前提下释放模型链式调用 `grep`/`cat`/`sed`/`awk` 的能力，并在命令执行后加入意图路由。讨论度高，涉及 CLI 安全模型和 UX 的深层次取舍。链接：https://github.com/google-gemini/gemini-cli/issues/19873

### ④ Shell 命令执行结束后卡在 “Waiting input”
**#25166** | P1, Bug | 评论 4 | 👍 3
极其简单的 CLI 命令执行完成后，Gemini CLI 仍显示命令激活并“等待用户输入”。用户需要反复中断，严重影响交互体验。此 issue 与 agent 挂起问题（#21409）互为印证，指向 shell 交互层存在系统性缺陷。链接：https://github.com/google-gemini/gemini-cli/issues/25166

### ⑤ Gemini 不会主动使用 skills 与 sub-agents
**#21968** | P2, Bug | 评论 6
用户报告 Gemini **几乎从不主动**调用自定义 skills 与 sub-agents，即使任务高度相关且技能描述明确（如 gradle/git skill），只有在显式指令下才会使用。这限制了 Gemini CLI 的可扩展性价值。链接：https://github.com/google-gemini/gemini-cli/issues/21968

### ⑥ AST 感知的文件读取/搜索/代码库映射（EPIC）
**#22745** | P2, Feature | 评论 7
跟踪多项调查：是否值得引入 AST 感知工具来实现“一次调用精确读取方法边界”、降低 token 噪声并改善代码库导航。属长期优化方向，社区关注其能否显著降低上下文占用。链接：https://github.com/google-gemini/gemini-cli/issues/22745

### ⑦ >128 个工具时遭遇 400 错误
**#24246** | P2, Bug | 评论 3
当启用的工具数量超过限制时，Gemini CLI 直接遇 400 错误，而非优雅降级或动态收敛工具范围。对重度 MCP 用户影响明显。链接：https://github.com/google-gemini/gemini-cli/issues/24246

### ⑧ Auto Memory 日志泄露与确定性脱敏
**#26525** | P2, Bug, 安全 | 评论 5
Auto Memory 将本地 transcripts 发给提取模型后才提示其脱敏 secrets——敏感内容在提示词生效前就已进入模型上下文。此外服务可能记录已有 skill 的完整内容。安全研究者关注此数据流设计缺陷。链接：https://github.com/google-gemini/gemini-cli/issues/26525

### ⑨ agents 目录下 symlink 文件不被识别
**#20079** | P2, Bug | 评论 4
`~/.gemini/agents/` 下通过 symlink 指向的自定义 agent 无法被识别，用户希望支持 symlink 以方便管理多个 agent 定义文件。虽是使用细节，但涉及 agent 加载机制的文件解析策略。链接：https://github.com/google-gemini/gemini-cli/issues/20079

### ⑩ Browser Agent 在 Wayland 下失败
**#21983** | P1, Bug | 评论 4 | 👍 1
Browser subagent 在 Wayland 会话中启动后立即以 `Termination Reason: GOAL` 退出，未能执行任何实际操作。Linux 桌面用户受影响；配合 #22267（Browser Agent 忽略 settings.json 覆盖）可以看到浏览器代理的配置与兼容性整体欠佳。链接：https://github.com/google-gemini/gemini-cli/issues/21983

---

## 4. 重要 PR 进展

### ① 系统级配置文件权限与 ACL 强制校验
**#29115** | size/xl | @jesussamuel-byte
在 Windows/POSIX 上加载系统级配置前增加文件所有权与 ACL 验证，防止低权限用户通过篡改全局配置实现提权。属于纵深防御安全加固。链接：https://github.com/google-gemini/gemini-cli/pull/29115

### ② 修复 NTFS 8.3 短文件名绕过路径检查
**#29116** | size/l | @urielefrenvirtusa
Windows 上 `git~1`、`node_m~1` 等短文件名可绕过路径规范化与 AllowedPathChecker 安全引擎。此 PR 在路径归一化和安全检查层同时处理 SFN。链接：https://github.com/google-gemini/gemini-cli/pull/29116

### ③ 遏制 `/chat delete <tag>` 路径穿越
**#29192** | P1, 安全 | size/m | @soroush5
`../` 形式的 tag 可导致删除 checkpoints 目录之外的文件。修复在 legacy raw-tag 回退路径中补充了未验证 tag 的边界检查。链接：https://github.com/google-gemini/gemini-cli/pull/29192

### ④ 增强工作区边界检查与符号链接解析
**#29170** | size/xl | @jesussamuel-byte
跨 POSIX/Windows 强化命令安全启发式、文件发现服务与目录列举工具中的工作区逃逸检测和 symlink 解析一致性。链接：https://github.com/google-gemini/gemini-cli/pull/29170

### ⑤ 修复 Windows 沙箱中 `git diff --output` 静默截断文件
**#29184** | size/m | @PakCyberbot
Windows 上 `git status/log/diff/show/branch` 一律被视为只读、免确认。`git diff --output=<path>` 可借此静默打开并截断任意文件。修复为对 git 参数进行校验。链接：https://github.com/google-gemini/gemini-cli/pull/29184

### ⑥ 修复 shell 沙箱拒绝启发式中的 exitCode 空值检查
**#29186** | P1, 安全 | size/s | @chelsealong
`ExecutionResult.exitCode` 类型为 `number | null`，原判断 `!== undefined && !== 0` 无法捕捉 `null`，导致“沙箱拒绝”后的安全回溯逻辑失效。修复关联 #29043。链接：https://github.com/google-gemini/gemini-cli/pull/29186

### ⑦ `read-many-files` 精确匹配二进制资源包含/排除
**#29188** | P1, Core | size/m | @chelsealong
原先用 `String.includes()` 判断 include pattern 是否匹配文件 stem/extension，目录名片段与文件名文本重叠时会造成误判。修复改为精确匹配。链接：https://github.com/google-gemini/gemini-cli/pull/29188

### ⑧ LLM prompt 模板占位符替换的安全修复
**#29187** | P2, Core | size/m | @chelsealong
三处 prompt 模板用 `String.replace` 填充 `{placeholder}`，用户可控内容中的 `$&` 等序列会触发 ECMA-262 GetSubstitution 特殊语义。改为 `safeLiteralReplace`，修复 #29044。链接：https://github.com/google-gemini/gemini-cli/pull/29187

### ⑨ checkpoint 非数组 history 崩溃降级
**#29195** | P2, Core | size/s | @soroush5
合法 JSON 但 `history` 非数组的 checkpoint 文件会使 `/resume` 崩溃并抛原始 `TypeError`。修复后与不可解析文件一样降级为空 checkpoint。链接：https://github.com/google-gemini/gemini-cli/pull/29195

### ⑩ 防止后台 Git 操作劫持 stdin
**#29148** | P2, Extensions | size/m | @DavidAPierce
后台扩展更新检查（`git.listRemote`）或 clone 操作未禁用交互提示，私有仓库在凭据/口令挑战时 Git 会阻塞读取 stdin，劫持用户终端输入。修复 #23480。链接：https://github.com/google-gemini/gemini-cli/pull/29148

---

## 5. 功能需求趋势

从近期 Issue 中可以提炼出以下几个社区高度关注的功能方向：

- **Agent 执行可靠性**：Generalist agent 挂起（#21409）、Subagent 误报成功（#22323）、shell 命令卡死（#25166）等共同指向 agent 执行状态机需要重构——社区期望有明确的超时降级、可观测性和错误传播机制。
- **安全边界与沙箱模型**：大量 PR 围绕路径穿越、NTFS 短文件名、符号链接逃逸、git 参数注入等问题展开，说明社区对 CLI 作为“本地 agent 执行环境”的安全隔离要求正快速提升。
- **上下文效率与记忆管理**：Auto Memory 的一系列 Bug（#26525、#26522、#26523）与 AST 感知读取探索（#22745、#22746）表明，token 成本的敏感性和上下文质量已成为重度用户的核心痛点。
- **模型自主调用扩展能力**：#21968（不使用 skills/sub-agents）和 #21432（agent 不自知 CLI 命令）反映出社区期望模型在“何时委派/何时使用工具”上更加主动、智能。
- **浏览器代理成熟度**：Wayland 失败（#21983）、忽略 `settings.json`（#22267）、会话锁恢复（#22232）等说明 browser_agent 在 Linux 下的兼容性和配置一致性有待加强。

---

## 6. 开发者关注点

- **频繁挂起与“已成功”错觉**：无论主 agent（#21409）还是 subagent（#22323），“卡死但报告成功”的组合最令开发者困扰——在无人值守的自动化场景中，这类静默故障比显式报错危害更大。
- **安全修复的密集度暗示攻防压力**：仅本周就有 5+ 个安全相关 PR（路径遍历、SFN 绕过、提权校验、凭据暴露 CrUX key 等），说明 Gemini CLI 的安全面在被安全社区积极审视。对开发者而言，**及时升级**比以往更重要。
- **工具数量与上下文窗口的现实瓶颈**：超过 128/400 个工具即触发 400 错误（#24246），而大量 MCP 扩展会快速推高工具数量——社区期待更聪明的工具动态裁剪机制。原始链接：https://github.com/google-gemini/gemini-cli/issues/24246
- **自定义 agent/skill 的可发现性与主动性不足**：模型不会主动使用用户配置的 skills/agents（#21968），即使这些扩展正是用户选择 Gemini CLI 的重要原因。开发者希望“配置了就要用得上”，而非每次显式指令。
- **终端体验细节仍待打磨**：命令结束后错误显示 “Waiting input”（#25166）、resize 闪烁（#21924）、`\n` 转义错误（#22466）等交互层问题高频出现,对日常使用体验拖累明显。

---

> 报告基于 github.com/google-gemini/gemini-cli 公开数据整理，数据采集时间 2026-09-04。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-09-04）

## 今日速览

今日发布 **v1.0.83-4**，重点为 MCP OAuth 登录引入 Client ID Metadata Document（CIMD）支持，并优化了大 session 恢复时的输入响应速度。社区讨论集中在 MCP 兼容性、模型配置错误、长会话稳定性及 Windows 企业环境问题，其中 #4525（MCP 初始化协议冲突）和 #3442（远程会话未启用）关注度最高。过去 24 小时无新增 PR，项目以高频小版本发布快速回应用户反馈。

---

## 版本发布：v1.0.83-4

- **Added**：为 MCP OAuth 登录添加 Client ID Metadata Document（CIMD）支持。
- **Improved**：CLI 默认不再弹出“中断会话恢复”提示；恢复大型会话时输入提示响应更快。
- **Fixed**：沙箱化文件工具现读取与开发者工具一致的配置（发布说明原文截断，完整内容以官方 Release 为准）。

📦 完整发布记录见 [GitHub Releases](https://github.com/github/copilot-cli/releases)

---

## 社区热点 Issues（按关注度精选 10 条）

1. **[area:mcp] #4525：1.0.81-1 在成功执行现代 `server/discover` 后仍发送旧版 `initialize`，导致 -32022**  
   影响使用 Python MCP SDK 2.0.0 双协议运行时的 stdio MCP server，初始化流程不兼容。  
   评论 6 · 👍 3 · 状态 OPEN  
   <https://github.com/github/copilot-cli/issues/4525>

2. **[area:sessions, enterprise] #3442：v1.0.51 提示“Remote sessions are not enabled”**  
   用户更新后无法启用远程会话，需组织管理员开启。企业部署反馈较多，共获得 10 个 👍。  
   评论 6 · 👍 10 · 状态 CLOSED  
   <https://github.com/github/copilot-cli/issues/3442>

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 · 2026-09-04

> 数据来源：github.com/MoonshotAI/kimi-cli  
> 统计区间：2026-09-03 更新动态（截至 2026-09-04 晨间）

## 今日速览

- 1.17+ 版本的 ACP 认证逻辑引发争议：新 Issue #2633 指出自定义 Provider 被强制要求 Kimi 账户 OAuth token，是当前最尖锐的未解决问题。
- 停滞近三个半月的 PR #2332（token 预算动态化）更新并关闭，涉及对硬编码 `max_tokens=32000` 的修复，值得关注最终去向。
- 多个 2026 年 3 月的功能需求（undo / web UI 增强 / 自动化能力等）在 9 月 3 日被批量关闭，官方或迎来一轮 Issue 清理与路线图收敛。

## 版本发布

过去 24 小时无新版本发布。

## 社区热点 Issues

过去 24 小时更新的 Issue 共 7 条，本期全部收录。

### 新增 / 未解决

**#2633 [OPEN] ACP auth gate (1.17+) blocks custom providers that don't need a Kimi account**  
作者: @billc8128 | 👍 0 | 💬 0  
https://github.com/MoonshotAI/kimi-cli/issues/2633

> 自 1.17.0 起，ACP server 对 `session/new`、`session/load`、`session/resume`、`session/prompt` 无条件执行 `_check_auth`，强制要求持久化的 Kimi 账户 OAuth token。作者指出这阻断了不需要 Kimi 账户的自定义 Provider（如本地模型、第三方网关）的正常使用。

**为什么重要：** 1.17+

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-09-04

## 1. 今日速览

今日无新版本发布，社区焦点集中在**高 CPU 占用回归（#30086）**与**模型调用后卡死/挂起类问题**上，多个相关 Issue 仍在高频更新。PR 侧，Windows 终端 Ctrl+C 中断修复（#47163）与桌面命令面板响应问题修复（#47164）已合入，浏览器插件 API（#46531）、Snowflake Cortex 原生认证（#47156）等新功能仍在推进中。

---

## 2. 版本发布

过去 24 小时无新版本 Release。

---

## 3. 社区热点 Issues

### 3.1 High CPU usage in newer versions of OpenCode
- **作者**: @DenisSilent · 更新: 2026-09-03 · 评论 49 · 👍 26
- **链接**: https://github.com/anomalyco/opencode/issues/30086
- **关注点**: 近期更新后 CPU 占用飙升，用户从可并行 10+ 会话降至 3 个即卡顿。社区讨论热度最高，强烈影响日常使用。

### 3.2 SSE error with #44944 — broken
- **作者**: @Artyomkun · 更新: 2026-09-03 · 评论 9
- **链接**: https://github.com/anomalyco/opencode/issues/47047
- **关注点**: Big Pickle 模型在生成过程中陷入死循环，1.18.26/1.18.27 均可复现，疑似与 #44944 变更相关，属较新的严重回归。

### 3.3 stuck in busy forever after toolcall
- **作者**: @yope · 更新: 2026-09-04 · 评论 6 · 👍 2
- **链接**: https://github.com/anomalyco/opencode/issues/40468
- **关注点**: 工具调用成功后 TUI 永久卡在 busy 状态，双 Esc 无法中断，日志停留在 loop 步骤。开发者普遍关心的核心稳定性问题。

### 3.4 [web] How to unarchive in opencode-desktop
- **作者**: @leavor · 更新: 2026-09-03 · 评论 20 · 👍 34
- **链接**: https://github.com/anomalyco/opencode/issues/12393
- **关注点**: 用户误操作归档后无法找回会话，桌面端缺少归档恢复入口。虽为提问，但 34 个 👍 说明这是一项高共识的 UX 缺陷。

### 3.5 Discrepancy between different opencode go usage dashboard
- **作者**: @PiouPiou82 · 更新: 2026-09-03 · 评论 11
- **链接**: https://github.com/anomalyco/opencode/issues/38255
- **关注点**: 月度限额仪表盘与粒度用量仪表盘数据不一致，导致模型提前被停止服务。影响用户对计费系统的信任。

### 3.6 Payment Declined After 3 Months Despite No Issue With Card or Bank
- **作者**: @haumannsvante · 更新: 2026-09-03 · 评论 9 · 👍 2
- **链接**: https://github.com/anomalyco/opencode/issues/45278
- **关注点**: 连续正常扣费三个月后突然支付失败，银行侧确认卡片无问题。支付链路稳定性直接影响订阅用户留存。

### 3.7 opencode Worker subprocess crashes with SIGILL on Intel i5-7200U
- **作者**: @oovaa · 更新: 2026-09-03 · 评论 5
- **链接**: https://github.com/anomalyco/opencode/issues/36280
- **关注点**: 老款 Intel CPU（Kaby Lake）上出现非法指令崩溃，崩溃处理链递归触发，甚至尝试分配 28 GB 内存导致系统冻结。兼容性风险较高。

### 3.8 [FEATURE]: System prompt mode switcher (Default/Light)
- **作者**: @kshnkvn · 更新: 2026-09-03 · 评论 5 · 👍 7
- **链接**: https://github.com/anomalyco/opencode/issues/15457
- **关注点**: 系统提示词过重，小模型/低端硬件场景需要轻量模式切换。属于长期存在的功能诉求。

### 3.9 [FEATURE]: Support for MCP Support Client ID Metadata Document (CIMD)
- **作者**: @jonesbusy · 更新: 2026-09-03 · 评论 4 · 👍 11
- **链接**: https://github.com/anomalyco/opencode/issues/25961
- **关注点**: 希望支持 Keycloak 等授权服务器的 Client ID Metadata Document，完善 MCP 企业级鉴权场景。功能票中点赞数较高。

### 3.10 [FEATURE]: Clarify Build scope — rename to All Access and add picker
- **作者**: @Fe2-O3 · 更新: 2026-09-03 · 评论 5
- **链接**: https://github.com/anomalyco/opencode/issues/46549
- **关注点**: “Build”命名易被误解为构建命令，社区建议改为 “All Access” 并增加选择器。产品命名与范围表达问题。

---

## 4. 重要 PR 进展

### 4.1 fix(core): restore Ctrl+C in Windows terminals
- **作者**: @Hona · 已关闭
- **链接**: https://github.com/anomalyco/opencode/pull/47163
- **内容**: 清除 Bun PTY 后端继承的 Ctrl+C-ignore 属性，恢复 Windows 桌面/Web 终端的 Ctrl+C 中断能力。修复 Windows 用户核心交互问题。

### 4.2 fix(tui): resolve keyboard deadlock in question mode
- **作者**: @maharshi365 · 已关闭
- **链接**: https://github.com/anomalyco/opencode/pull/36550
- **内容**: 修复 QuestionPrompt 组件中两个 useBindings 互斥条件导致的键盘死锁，Closes #36382 与 #30517。

### 4.3 feat(cli): restore automatic update policy
- **作者**: @jlongster · 打开中
- **链接**: https://github.com/anomalyco/opencode/pull/47161
- **内容**: 恢复 `update: "auto"` 自动更新策略，兼容旧版 `autoupdate: true`，支持后台轮询和免重启安装更新。

### 4.4 fix(desktop): keep command palette responsive and scoped
- **作者**: @Hona · 已关闭
- **链接**: https://github.com/anomalyco/opencode/pull/47164
- **内容**: 命令面板改为同步匹配内置命令，异步追加文件和会话结果，避免重置键盘选择；同时修复命令重复注册与作用域越界问题。

### 4.5 feat(browser): add a public-API browser plugin
- **作者**: @Hona · 打开中
- **链接**: https://github.com/anomalyco/opencode/pull/46531
- **内容**: 新增 @opencode-ai/plugin-browser，提供 44 个 Code Mode 方法：标签页、交互、快照、文件、诊断、性能分析

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*