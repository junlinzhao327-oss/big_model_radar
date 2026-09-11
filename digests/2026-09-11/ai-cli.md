# AI CLI 工具社区动态日报 2026-09-11

> 生成时间: 2026-09-11 00:15 UTC | 覆盖工具: 7 个

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

# Claude Code 社区动态日报

**日期：2026-09-11** | 数据来源：github.com/anthropics/claude-code

---

## 一、今日速览

今日社区最热的焦点是 **Cowork（Windows）沙箱全面故障**——一次 Windows 系统更新（KB5124008）导致 Plan9 共享挂载失败，至少 5 个独立 Issue 在 24 小时内更新，社区情绪强烈。与此同时，**Function Hooks 插件能力提案（#91870）持续高热**，官方已在 Issue 中承诺「以周为单位」交付。版本方面，v2.1.268 发布，聚焦网关计费一致性与配置校验。

---

## 二、版本发布

### v2.1.268

- **网关计费对齐**：在 `gateway.yaml` 中设置 `pricing:` 后，已登录的 Claude Code 客户端可通过托管设置获得与网关一致的费率，使 `/cost` 与遥测数据与官方支出计量器保持一致。
- **网关启动告警**：当 `access_control.allow_cidrs` 为空时，网关启动阶段会给出警告提示（原文摘要被截断）。

> 该版本延续了近期对**企业级网关/成本治理**的投入，与社区对成本透明的高频诉求方向一致。

---

## 三、社区热点 Issues（Top 10）

### 1. #91870 — Function Hooks：让插件强大 10 倍 🔥
- 状态：OPEN | 评论 **158** | 👍 **91** | 标签：`enhancement`, `area:hooks`, `area:plugins`
- 作者 @poteat（也是今日 PR 的主要贡献者）
- **为何重要**：这是当前社区呼声最高的功能需求。官方在 9/9 的社区更新中明确承诺「以周为单位（in weeks）交付 function hooks」，并感谢社区高质量反馈。
- 链接：https://github.com/anthropics/claude-code/issues/91870

### 2. #42776 — Windows 桌面端因孤儿进程文件锁无法重启
- 状态：OPEN（标记 `invalid`）| 评论 **170** | 👍 **82**
- **为何重要**：全站评论数最高、跨 5 个月仍未解决的长期问题。孤儿进程导致文件锁，桌面端重启失败，直接影响 Windows 用户日常使用。
- 链接：https://github.com/anthropics/claude-code/issues/42776

### 3. #92984 — Windows 更新 KB5124008 后 Cowork Plan9 共享全部失败 ⚠️
- 状态：OPEN | 评论 **81** | 👍 **40** | 标签：`bug`, `has repro`, `platform:windows`, `area:cowork`
- **为何重要**：`Plan9 mount failed: invalid argument`，卸载该 KB 即可恢复。这是今日 Cowork Windows 集群故障的**核心源头 Issue**，复现路径明确，影响面大。
- 链接：https://github.com/anthropics/claude-code/issues/92984

> 关联同源问题：#93118、#93221、#93071（均为 Windows Cowork / Plan9 / sandbox-helper 挂载失败）

### 4. #30112 — Cowork 网络出口白名单失效，自定义域名被 403
- 状态：OPEN | 评论 **57** | 👍 **54** | 标签：`area:desktop`
- **为何重要**：企业用户在受限网络下无法放行自定义域名，`blocked-by-allowlist` 403 直接阻断业务。与 #34690（代理 JWT 未反映白名单设置）互为关联问题。
- 链接：https://github.com/anthropics/claude-code/issues/30112

### 5. #76248 — 云端/Cowork 会话 git 代理阻断所有 push
- 状态：OPEN | 评论 **34** | 👍 **14** | 标签：`bug`, `has repro`, `area:cowork`
- **为何重要**：自 2026-07-10 起，即使自带 fine-grained PAT，也无法推送到「会话授权仓库集」之外的仓库，疑似 `CCR_TEST_GITPROXY` 灰度引入。**云会话推送被完全阻断**是团队协作场景的严重回归。
- 链接：https://github.com/anthropics/claude-code/issues/76248

### 6. #12953 — 鼠标滚轮滚动的是输入历史而非聊天历史
- 状态：OPEN | 评论 **22** | 👍 **21** | 标签：`bug`, `area:tui`, `platform:windows`
- **为何重要**：一个从 2025-12 存活至今的 TUI 交互体验问题，长期高赞说明它持续困扰日常使用。
- 链接：https://github.com/anthropics/claude-code/issues/12953

### 7. #83510 — Claude 第 5 代模型质量可测量回归
- 状态：OPEN | 评论 **13** | 👍 **21** | 标签：`MODEL`
- **为何重要**：报告称 Fable 5 / Opus 5 / Sonnet 5 在**胡言乱语检测能力下降、啰嗦度约 2 倍、静默降级**（Fable 5 → Opus 4.8）方面存在可复现的量化问题。属于模型层面的高价值反馈。
- 链接：https://github.com/anthropics/claude-code/issues/83510

### 8. #92183 — 桌面端禁用 SendMessage，子代理无法被唤醒或续跑
- 状态：OPEN | 评论 **6** | 👍 **18** | 标签：`area:agents`, `area:desktop`, `platform:macos`
- **为何重要**：Agent 工具能成功启动子代理，但无法消息化已运行/已完成子代理，**多代理工作流被桌面端权限限制卡死**，与 #82565（子代理递归膨胀）同属 agent 体系问题。
- 链接：https://github.com/anthropics/claude-code/issues/92183

### 9. #83048 — [SEV-1] `budget.spent()` 低于实际消耗 72 倍
- 状态：OPEN | 评论 **4** | 标签：成本控制
- **为何重要**：用户报告 4 小时内耗尽每周预算，而 API 上报仅显示约 3–4% 消耗。**成本计量失灵**对重度 Max 用户是直接经济损失，同族的 #86033、#80750 已被 stale 关闭，问题仍被社区认为未根除。
- 链接：https://github.com/anthropics/claude-code/issues/83048

### 10. #93490 — `--resume` 提示缓存不命中（Fable 5.1）
- 状态：OPEN（9/10 新增）| 评论 **2** | 标签：`area:cost`, `area:core`, `performance`
- **为何重要**：作者精确指认根因——**会话启动上下文消息以纯字符串而非 content blocks 重放**，导致静态前缀之后缓存全部失效。与 #91971、#83913 构成「提示缓存失效三连」，是当前成本异常的主要技术线索。
- 链接：https://github.com/anthropics/claude-code/issues/93490

---

## 四、重要 PR 进展

> ⚠️ 过去 24 小时内仅 **3 个 PR** 有更新，以下为全部条目。

### 1. #93452 — `mods/diff`：对齐内置 /diff 面板（OPEN）
- 作者 @poteat
- 让 diff 模块的界面与内置面板保持一致：hunk 通过引擎 code 元素绘制、内置关闭按钮 ✕、行距与空状态位置、窄终端 resize 线，并限制同一时间只进行一次仓库探测。
- 链接：https://github.com/anthropics/claude-code/pull/93452

### 2. #93244 — `mods`：API 重命名、遥测修复、diff 后端 seam（CLOSED）
- 作者 @poteat
- 跟随插件 API 的命名规范化（`isFocused`、`tool`），收紧遥测（逐行发送、按行读取分析开关、第三方 provider 不上报任何数据），并为 diff 模块引入后端 seam，git 作为内置后端以支持其他版本控制。
- 链接：https://github.com/anthropics/claude-code/pull/93244

### 3. #89404 — `validate-agent.sh`：不再在首个警告处中止（OPEN）
- 作者 @bcherny
- 修复 `set -euo pipefail` 与 `((warning_count++))` 的交互问题，解决 plugin-dev skill 的 `validate-agent.sh` 在自身 agent 文件上失败、并误报合法 agent 的问题（关联 #83803）。
- 链接：https://github

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报
**日期：2026-09-11** | 数据来源：github.com/openai/codex

---

## 一、今日速览

Python SDK 0.154.0 正式发布，新增 `max` / `ultra` 两档推理强度枚举值，同步 API 引入 `ExternalMessage`。社区侧，**配额异常消耗**仍是最大争议点——跨报告汇总追踪帖 #41220 已累积 35 条评论；同时"Selected model is at capacity"容量报错在 GPT-5/GPT-6 多模型上持续扩散。当日 20 条 PR 集中落地，主题聚焦沙箱安全边界、权限路径解析与 MCP OAuth 可靠性。

---

## 二、版本发布

###

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报（2026-09-11）

> 数据来源：[github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)

---

## 一、今日速览

今日社区最受关注的是**企业 Workspace 账号认证失败**问题（#29101，42 条评论），已升级为 P1 并持续发酵。安全面动作密集，多个沙箱隔离、路径遍历与提示注入防护 PR 集中更新。Agent 可靠性仍是长期主线——子代理虚假上报成功、通用代理挂起、Skills/子代理调用率低等问题持续被维护者跟踪。

---

## 二、版本发布

**v0.61.0-nightly.20260910.ged2ac40df** 已发布，为常规 nightly 构建，版本提升 PR 见 [#29268](https://github.com/google-gemini/gemini-cli/pull/29268)。

- Changelog: [对比链接](https://github.com/google-gemini/gemini-cli/compare/v0.61.0-nightly.20260909.ged2ac40df...v0.61.0-nightly.20260910.ged2ac40df)

---

## 三、社区热点 Issues

1. **[#29101](https://github.com/google-gemini/gemini-cli/issues/29101) 企业 Workspace 账号认证失败（P1 / 42 评论）**
   原本正常工作的 Google Workspace 账号 + Cloud Project ID 配置突然失效，直接阻断企业用户使用，是目前评论数最高、优先级最紧急的问题。

2. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) 子代理达到 MAX_TURNS 却上报"GOAL 成功"（P1 / 13 评论）**
   `codebase_investigator` 在未完成任何分析前触发轮次上限，却返回 `status: "success"` 与 `Termination Reason: GOAL`，把中断伪装成成功。这类"静默失败"会严重污染上层 Agent 的决策与评估。

3. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) 通用代理（Generalist Agent）无限挂起（P1 / 8 👍）**
   即使是创建文件夹这类简单操作，一旦委派给通用代理便永久卡住，禁用于代理可绕开。点赞数最高，说明影响面广。

4. **[#19873](https://github.com/google-gemini/gemini-cli/issues/19873) 借助零依赖 OS 沙箱 + 执行后意图路由释放模型的 bash 能力（P2）**
   维护者提案：Gemini 3 本质是"原生 bash 用户"，应通过沙箱而非限制工具来兼顾安全与能力，代表官方在 Agent 执行模型上的方向性思考。

5. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) AST 感知的文件读取 / 搜索 / 代码库映射评估（P2）**
   EPIC 级议题，目标是减少错位读取带来的无效轮次与 token 噪声，与 [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)（AST 感知 CLI 工具）联动。

6. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) Gemini 很少主动使用 Skills 与子代理（P2）**
   用户反馈即使技能描述高度相关，模型也不会自主调用，必须显式指令。这直接影响自定义技能生态的可用性。

7. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) Shell 命令执行完成后仍卡在"Waiting input"（P1 / 3 👍）**
   简单命令执行完毕后界面继续显示"等待用户输入"，属于高频卡死体验问题，复现稳定。

8. **[#26525](https://github.com/google-gemini/gemini-cli/issues/26525) Auto Memory 需要确定性脱敏并削减日志（P2）**
   Auto Memory 会把本地会话内容送入后台提取模型，脱敏发生在内容已进入上下文之后；同系列还有 [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)（低信号会话无限重试）、[#26523](https://github.com/google-gemini/gemini-cli/issues/26523)（非法 patch 静默跳过），构成记忆系统的安全/质量组合议题。

9. **[#24246](https://github.com/google-gemini/gemini-cli/issues/24246) 工具数量超过 128 个时触发 400 错误（P2）**
   大量 MCP/Skills 接入场景下的硬性瓶颈，期望 Agent 能智能裁剪工具作用域。

10. **[#22672](https://github.com/google-gemini/gemini-cli/issues/22672) Agent 应阻止/劝阻破坏性行为（P2）**
    复杂 git 操作中模型可能使用 `git reset` 或 `--force`，而更安全的替代方案是存在的，涉及数据库等资源修改时的风险提示也不足。

> 其他值得留意：[#21983](https://github.com/google-gemini/gemini-cli/issues/21983)（browser subagent 在 Wayland 下失败，P1）、[#21335](https://github.com/google-gemini/gemini-cli/issues/21335)（`/compress` 结果不跨会话持久化）、[#19561](https://github.com/google-gemini/gemini-cli/issues/19561)（Tactful Extraction 精准读取以节省 token）。

---

## 四、重要 PR 进展

1. **[#29282](https://github.com/google-gemini/gemini-cli/pull/29282) fix(auth): 登录后立即持久化 OAuth 凭据**
   修复浏览器/用户码登录完成后凭据未落盘、导致重复要求登录的问题。与当日最热的认证 Issue 高度相关，值得重点跟踪。

2. **[#29283](https://github.com/google-gemini/gemini-cli/pull/29283) fix(sandbox): 改进文件系统隔离并隔离运行时状态**
   覆盖 Docker、Podman、runsc、LXC 与 macOS Seatbelt，配置访问改为只读，运行时写入临时化，是沙箱安全面的核心改动。

3. **[#29214](https://github.com/google-gemini/gemini-cli/pull/29214) fix(sandbox): 加固文件系统边界**
   用净化后的配置文件替代宿主机目录挂载，统一 realpath 解析并处理不存在路径的降级逻辑。

4. **[#29250](https://github.com/google-gemini/gemini-cli/pull/29250) fix(core): 阻断经由构建文件篡改与不可信参数的间接提示注入**
   在受限工作区模式下校验构建配置与外部命令参数，重构 `shell`、`edit`、`write_file` 等内置执行路径。

5. **[#29249](https://github.com/google-gemini/gemini-cli/pull/29249) fix(core): 修复 `get_internal_docs` 路径守卫的同级前缀绕过（P1）**
   原实现使用字符串前缀比较，缺少路径分隔边界，任何以 docs 目录名开头的同级目录都能被读取并回传给模型。

6. **[#29200](https://github.com/google-gemini/gemini-cli/pull/29200) fix(core): 运行时统一执行 MCP 策略**
   服务名匹配改为大小写不敏感 + 去空格；显式空 `mcp.allowed` 列表改为 fail-closed，而不再放行全部服务。

7. **[#29134](https://github.com/google-gemini/gemini-cli/pull/29134) fix(cli): 防止误删当前会话（P2）**
   为 `--list-sessions` / `--delete-session` 传入活动会话 ID，并以文件名后缀精确匹配避免误判，附带回归测试。

8. **[#29277](https://github.com/google-gemini/gemini-cli/pull/29277) / [#29278](https://github.com/google-gemini/gemini-cli/pull/29278) fix(core): 消除 `expandEnvVars()` 哨兵键冲突**
   两个独立提交修复同一问题：调用方环境若恰含 `__GCLI_EXPAND_TARGET__`，环境变量展开会返回错误值。现改为选择无冲突的临时键。

9. **[#29094](https://github.com/google-gemini/gemini-cli/pull/29094) 升级 simple-git 至 3.32.3（CVE-2026-28292，严重）**
   Trivy 扫描出的 CRITICAL 级依赖漏洞修复，属于必须尽快合并的安全更新。

10. **[#29116](https://github.com/google-gemini/gemini-cli/pull/29116) fix(core): 缓解 NTFS 8.3 短文件名路径穿越**
    Windows 下 `git~1`、`env~1` 等短名可绕过路径规范化与 `AllowedPathChecker` 黑名单，该 PR 已关闭但问题本身值得持续关注。

> 其他：[#29098](https://github.com/google-gemini/gemini-cli/pull/29098) 修复 `useInputHistoryStore` 状态更新器非纯函数问题；[#29097](https://github.com/google-gemini/gemini-cli/pull/29097) 修复仓库名解析误删非尾部 `.git`（如 `blog.github.io` 被解析成 `hub.io`）。

---

## 五、功能需求趋势

- **Agent 可靠性与自省**：子代理生命周期可见性（[#22598](https://github.com/google-gemini/gemini-cli/issues/22598) `/chat share`）、中断状态正确上报（[#22323](https://github.com/google-gemini/gemini-cli/issues/22323)）、`/bug` 报告包含子代理上下文（[#21763](https://github.com/google-gemini/gemini-cli/issues/21763)）构成一组明确的"可观测性"需求。
- **沙箱与执行安全**：从 prompt injection、路径穿越到破坏性命令防护，安全议题在 Issue 与 PR 两端同时升温，是当前迭代密度最高的方向。
- **上下文与 token 效率**：AST 感知读取/搜索/映射（[#22745](https://github.com/google-gemini/gemini-cli/issues/22745)、[#22746](https://github.com/google-gemini/gemini-cli/issues/22746)、[#19561](https://github.com/google-gemini/gemini-cli/issues/19561)）加上 `/compress` 持久化（[#21335](https://github.com/google-gemini/gemini-cli/issues/21335)），指向降低每轮基线开销的长期目标。
- **企业级部署能力**：Workspace 认证、MCP 策略一致性、非交互模式，是 enterprise 标签下的持续诉求。
- **Auto Memory 质量治理**：脱敏时机、无效 patch 隔离、低信号会话防重试，形成一个小而完整的子方向。
- **终端体验与跨平台**：终端 resize 闪烁（[#21924

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报
**日期：2026-09-11** ｜ 数据源：github.com/github/copilot-cli

---

## 1. 今日速览

今日社区最受关注的是一条被关闭的长期高票需求——**vim/vi 输入模式**（#13，76 👍，12 条评论），历时近一年终于 CLOSED。与此同时，**内存与资源泄漏成为压倒性痛点**：过去 24 小时内至少有 4 条 OOM/句柄泄漏类 Issue 在活跃更新，其中一条记录到单进程 221% CPU 持续 35 小时、写出 33 GB 日志。版本侧发布 v1.0.84-4，主要围绕插件/指令/LSP 的命令行接口做了一次重构与 `--json` 输出补全。

---

## 2. 版本发布

### v1.0.84-4

**Added**
- 新增 `copilot instruction list` 与 `copilot lsp list` 子命令，取代原先的 `copilot plugins list --kind instruction` 与 `--kind lsp`（命令语义更清晰，`instruction`/`lsp` 从 plugin 命名空间中独立出来）。
- 为 `copilot plugin list`、`copilot plugin marketplace list`、`copilot plugin marketplace browse` 增加 `--json` 输出，便于脚本化与 CI 集成。
- `copilot plugin` 新增 `enable` / `disable` 操作，插件可临时停用而无需卸载。

**观察**：本次更新延续了近期「可编程化 + 插件体系细化」的方向，`--json` 的铺开说明 CLI 正在被更多自动化流程（Agent、CI、企业内部工具链）消费。

---

## 3. 社区热点 Issues

> 过去 24 小时共 37 条 Issue 更新，以下为评论数最多、最值得关注的 10 条。

### ① #13 [CLOSED] CLI 应支持 vi/vim 输入模式
- 链接：https://github.com/github/copilot-cli/issues/13
- 作者 @RyanHecht ｜ 12 评论 ｜ **76 👍（今日最高）**
- **为何重要**：这是本仓库最长时间被顶的功能请求之一（2025-09 创建）。核心诉求是让熟悉模态编辑器的用户在交互输入区获得键盘驱动的导航与编辑体验。今日以 CLOSED 状态出现，意味着维护方已给出结论（实现或明确不做），对长期关注者是一个信号性事件。

### ② #4807 Idle 状态下进入 FileWatch 事件风暴：占用 2 个 CPU 核、写出 33+ GB 日志
- 链接：https://github.com/github/copilot-cli/issues/4807
- 作者 @nayato ｜ 0 评论 ｜ 0 👍（新报）
- **为何重要**：由 Agency 启动的空闲 CLI 进程持续 35 小时占用约 **221% CPU**，并将被拒绝的 file-watch 事件无限追加到 debug 日志，最终日志膨胀到 33 GB。这是典型的资源泄漏型严重缺陷，对长驻/后台运行场景影响极大。

### ③ #4686 Node.js OOM 崩溃：约 37 分钟后泄漏 31,965 个 libuv 异步句柄
- 链接：https://github.com/github/copilot-cli/issues/4686
- 作者 @Marcus-Lindbloom ｜ 3 评论 ｜ 0 👍
- **为何重要**：版本 1.0.82，Linux x86_64，SEA 内嵌 Node v24.20.0。问题明确指出 SEA 模式下 `NODE_OPTIONS` 被忽略，导致用户无法通过常规手段调大堆上限。句柄泄漏计数具体、可复现，是定位内存问题的关键线索。

### ④ #4725 Linux 上频繁出现 JavaScript heap out of memory
- 链接：https://github.com/github/copilot-cli/issues/4725
- 作者 @jbulow ｜ 3 评论 ｜ 1 👍
- **为何重要**：与 #4686 形成印证——每隔几分钟即崩溃，堆在约 4 GB 处反复触发 Mark-Compact 后分配失败。说明内存问题并非单一平台个案，而是 Linux 用户群体的普遍现象。

### ⑤ #4780 Session compaction OOM 且永不完成，会话永久无法恢复
- 链接：https://github.com/github/copilot-cli/issues/4780
- 作者 @simukka ｜ 1 评论 ｜ 3 👍
- **为何重要**：触及上下文压缩这一核心机制。一旦触发阈值就进入不可逆的崩溃循环：`session.compaction_start` 发出后压缩永不完成，进程以堆溢出死亡，此后每次 `--resume` 都会重新进入同一循环——**会话数据事实上被锁死**。属于数据可用性级别的缺陷。

### ⑥ #4699 长时间 `--resume` 会话 OOM，且崩溃转储被写入用户当前工作目录
- 链接：https://github.com/github/copilot-cli/issues/4699
- 作者 @pedoch ｜ 2 评论 ｜ 5 👍
- **为何重要**：14 小时内崩溃 3 次，均在 4 GiB 堆上限。除 OOM 本身外，**诊断报告落盘到 cwd** 是另一层问题：会污染用户仓库（可能被误提交），也暴露了诊断产物路径设计不合理。

### ⑦ #4742 [triage] 桌面端 1.1.15：已有 Local 会话运行时无法创建第二个会话
- 链接：https://github.com/github/copilot-cli/issues/4742
- 作者 @DannyBe99 ｜ 11 评论 ｜ 5 👍（今日评论最多）
- **为何重要**：报错 "This project already has an active Local workspace" 在 1.1.15 自动更新后出现，属于明显的版本回归。11 条评论说明影响面较广，且直接阻断了并行会话这一常用工作流。

### ⑧ #4095 Windows 下插件更新失败："Access is denied (os error 5)"
- 链接：https://github.com/github/copilot-cli/issues/4095
- 作者 @FBakkensen ｜ 3 评论 ｜ **21 👍（今日第二高）**
- **为何重要**：git fetch/checkout 成功但安装阶段被拒绝，根因指向 VS Code 中 Copilot 扩展持有 `installed-plugins` 的 watcher 句柄。这是**跨产品（CLI × VS Code）资源争用**问题，点赞数说明 Windows 开发者受阻严重。

### ⑨ #4795 [triage] Atlassian MCP OAuth 失败：回调 URL 与注册的 33418 端口不匹配
- 链接：https://github.com/github/copilot-cli/issues/4795
- 作者 @rhodla02 ｜ 2 评论 ｜ 2 👍
- **为何重要**：CLI 使用随机端口做 OAuth 回调，而 Atlassian MCP 服务端注册的是固定端口 33418，导致鉴权必然失败。在 1.0.83 与 1.0.84-3 上均可复现，说明 MCP 生态接入的**回调地址协商机制**尚未标准化。

### ⑩ #4809 [triage] 原生 MCP 连接器在 initialize 前发送非标准 `server/discover`，违反 MCP 生命周期规范
- 链接：https://github.com/github/copilot-cli/issues/4809
- 作者 @jacob-schmier-sndk ｜ 0 评论 ｜ 0 👍（新报）
- **为何重要**：当本地 stdio MCP 服务端没有缓存工具快照时，CLI 会在 `initialize` 握手之前发送私有 `server/discover` 请求。这会**直接搞崩严格遵循规范的第三方 MCP 服务端**。对生态兼容性影响深远，是规范一致性问题而非单纯 bug。

**其他值得收藏的条目**：#4803（`/ask` / `/btw` 答案变空白）、#4805（崩溃遗留的陈旧 `inuse.<pid>.lock` 使会话不可复活）、#4252 / #4067（`settings.json` 中 `model` 字段不生效，且退出时会用启动时快照覆盖文件，形成自噬式陈旧默认值）、#4804（沙箱导出的 `GH_TOKEN` 静默使用无关的缓存 PAT）。

---

## 4. 重要 PR 进展

> 说明：过去 24 小时本仓库仅有 **2 条** PR 更新，远少于 Issues 的活跃度，故无法凑足 10 条，以下如实列出全部。

### ① #4808 [OPEN] Pin GitHub Actions to commit SHAs
- 链接：https://github.com/github/copilot-cli/pull/4808
- 作者 @github-security-bot ｜ 2026-09-10
- **内容**：将 `github/copilot-cli` 中所有 GitHub Actions 的 `uses:` 引用固定到不可变 commit SHA。统计：改动 4 个文件、扫描 3 个文件、发现 3 处引用、全部完成固化、0 跳过 / 0 警告 / 0 错误。
- **意义**：供应链安全加固。以 SHA 替代可变 tag 可防止上游 Action 被篡改或强制推送后影响本仓库 CI 流水线，属于现代 CI 的基线实践。

### ② #4786 [CLOSED] Revise notice regarding third-party services
- 链接：https://github.com/github/copilot-cli/pull/4786
- 作者 @nkasuku ｜ 2026-09-10 关闭
- **内容**：修订第三方服务相关声明章节，澄清访问要求与条款。
- **意义**：合规与法务文本更新，非功能性变更，但对涉及 MCP 等外部服务接入的用户有参考价值。

**观察**：PR 流量极低（2 条）而 Issue 流量极高（37 条更新），且两条 PR 均非功能开发——侧面反映当前阶段社区主要在做「报障」，而非「贡献代码」。

---

## 5. 功能需求趋势

从今日全部 Issues 中可提炼出以下方向：

| 方向 | 代表 Issue | 热度信号 |
|---|---|---|
| **内存与资源管理** | #4686、#4725、#4780、#4699、#4807 | 数量最多、最活跃，涵盖堆 OOM、libuv 句柄泄漏、file-watch 事件风暴、CPU 满载 |
| **MCP 生态集成与规范兼容** | #4795、#4809、#4731 | OAuth 回调、生命周期握手、工具列表刷新三条链路均有问题 |
| **会话生命周期可靠性** | #4805、#4755、#4780 | 陈旧锁、队列卡死（idle/运行双非态）、压缩失败后不可恢复 |
| **键盘与终端交互体验** | #13、#2199、#3260、#3534 | vim 模式（76 👍）与 Ctrl+Backspace（7 👍）是高频编辑器体验诉求；复制粘贴在 SSH+tmux / WSL2 ARM64 下失效 |
| **插件体系与可编程接口** | v1.0.84-4、#4095、#3589 | 新增 `enable`/`disable` 与 `--json`，同时 Windows 句柄争用、多 hook 上下文只注入最后一条 |
| **认证与多身份管理** | #367、#4804、#4796 | 多账号切换、沙箱凭据选择不可见、EMU 场景下 Entra 鉴权失败 |
| **模型配置一致性** | #4067、#4252 | `settings.json` 的 `model` 不生效 + 退出时回写覆盖 |
| **自动化/非交互场景** | #4810、#4799 | 定时自动化受本地分支状态阻塞；更新失败后重复下载不复用已下包 |

---

## 6. 开发者关注点（痛点总结）

1. **稳定性压倒一切：OOM 是当前第一号问题。**
   今日最活跃的话题集中在堆内存耗尽与句柄泄漏。#4686 给出的数字极具诊断价值（37 分钟 / 31,965 个泄漏句柄），#4807 的 33 GB 日志与 221% CPU 则说明进程在空闲状态下仍在做无效功。**共性根因指向长期驻留进程的资源回收**，涉及 SEA 打包下 `NODE_OPTIONS` 失效这一额外障碍。

2. **会话可信度：崩溃之后的「不可恢复」比崩溃本身更伤。**
   #4780（compaction 后永久不可 resume）、#4805（陈旧 `inuse.<pid>.lock` 不回收）、#4755（队列消息落到 turn 结束点导致永久卡死）三条独立路径都指向同一个体验：**用户的会话资产可能毫无征兆地变成废纸**。对重度使用者（长 `--resume` 会话、数小时连续工作）这是留存级风险。

3. **跨平台是持续失血点。**
   Windows 侧：插件更新被 OS 级文件占用阻断（#4095，21 👍）；WSL2 ARM64 侧：`clip.exe` 引号处理导致 `/copy` 失败（#3534）；远程侧：SSH + tmux + Windows Server 组合下复制粘贴全面失效（#3260）。三个平台组合各自有独立故障，说明终端层与剪贴板/文件系统的适配缺乏统一抽象。

4. **MCP 的「规范一致性」正在成为新的信任门槛。**
   #4809（握手前发私有请求会搞崩合规服务端）、#4795（回调端口协商）、#4731（超时后向已放弃的服务端派发刷新，导致工具被永久剥离）显示：**CLI 的 MCP 客户端行为一旦偏离规范，代价由生态承担**。第三方服务提供方对兼容性的耐心正在被消耗。

5. **配置与凭据的「静默行为」侵蚀信任。**
   #4067 / #4252 构成一对反直觉组合：启动不读 `settings.json` 的 `model`，退出却把内存里的旧值写回去——用户的编辑被反复静默回滚。类似地，#4804 中沙箱导出的 `GH_TOKEN` 并非当前 `gh` 活跃会话，且**没有任何可见性提示**。开发者反复强调的关键词是「no visibility into which credential is chosen」。

6. **编辑器级体验的需求已积累到临界点。**
   #13 的 76 👍 是本仓库当前最高票，结合 #2199（Ctrl+Backspace）与两条剪贴板 Issue，可以判断：CLI 的交互输入层仍被视作「够用

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-09-11** ｜ 数据来源：github.com/MoonshotAI/kimi-cli

---

## 1. 今日速览

过去 24 小时内，kimi-cli 仓库整体处于低活跃状态：**无新版本发布、无 PR 更新**，仅有 **1 条 Issue 被更新**。唯一动态是 v0.42.0 上 `/login` 设备授权流程在浏览器批准成功后仍返回 HTTP 500 的登录阻塞问题（#2638），该问题同时在 VS Code 扩展中复现，属于影响面较广的认证链路故障。

> **数据说明**：本日有效数据量极小（1 条 Issue / 0 条 PR），因此「社区热点 Issues」与「重要 PR 进展」无法按 10 条规模呈现。为避免虚构信息，以下仅对真实存在的条目做深度分析，并说明数据缺口。

---

## 2. 版本发布

**无。** 过去 24 小时内没有新的 Release，当前社区反馈的问题集中在最近版本 **v0.42.0**。

---

## 3. 社区热点 Issues（共 1 条，全部列出）

### 🔴 #2638 — `/login` 设备授权在浏览器批准成功后返回 HTTP 500

- **作者**：@milesbuckton
- **状态**：OPEN ｜ 创建：2026-09-09 ｜ 更新：2026-09-10 ｜ 评论：1 ｜ 👍：0
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2638

**问题描述**

| 维度 | 信息 |
|---|---|
| CLI 版本 | 0.42.0 |
| 操作系统 | macOS |
| 账户类型 | Free plan（Adagio tier） |
| 复现范围 | CLI 与 VS Code 扩展均可复现 |

**复现路径**
1. 在 CLI 中执行 `/login`；
2. 浏览器打开并展示设备码（如 `WGBT-C3BW`、`QLE2-MYVL`）；
3. 在浏览器中使用正确账号完成授权确认；
4. **授权成功后 CLI 侧仍返回 HTTP 500**，登录流程中断。

**为什么这条 Issue 值得关注**

1. **阻塞级故障**：`/login` 是新用户接触产品的第一个必经环节，500 错误意味着完全无法进入使用流程，属于 P0 级别体验问题。
2. **跨端一致复现**：CLI 与 VS Code 扩展同时命中同一错误，说明问题大概率位于**服务端设备授权 / token 兑换接口**或共享的认证 SDK 层，而非单一客户端实现缺陷，影响面超出单个产品形态。
3. **版本相关性明确**：报告者明确锁定 v0.42.0，为回归排查（regression bisect）提供了清晰起点。
4. **设备码流程本身有迹可循**：浏览器端已给出设备码且授权成功，说明「授权确认」环节正常，「token 兑换 / 轮询确认」环节失败——这一分界信息对定位服务端 5xx 极有价值。

**社区反应**

目前评论数仅 1、点赞 0，社区声量尚未起来，属于**早期发现阶段**。考虑到该问题直接阻断登录，若未在短时间内修复，预计后续会有重复报告（duplicate）与升级讨论。建议维护者在 Issue 中补充请求 ID / trace-id 采集指引，以加速定位。

---

## 4. 重要 PR 进展

**无。** 过去 24 小时内没有任何 Pull Request 被创建或更新。这意味着：

- 上述登录故障目前**尚无公开的修复 PR**；
- 仓库当前处于代码变更的空窗期，可能是版本发布后的稳定期，或维护工作尚未同步到公开 PR 流程。

---

## 5. 功能需求趋势

由于本日仅有 1 条 Issue，无法形成统计意义上的趋势。但从该条数据仍可提炼出以下方向性信号：

1. **认证与登录链路稳定性**
   设备码（device code）授权是 CLI 类工具面向无 GUI 场景的标准方案，其端到端可靠性直接决定首次使用转化率。当前 5xx 说明该链路的服务端容错与错误语义仍有改进空间。

2. **多端一致性（CLI ↔ IDE 扩展）**
   同一问题在 CLI 与 VS Code 扩展中同时复现，反映出社区对「一次修复、多端生效」的共享认证层有实际需求。IDE 集成仍是需要持续投入的方向。

3. **错误可观测性与诊断能力**
   HTTP 500 属于最不具信息量的失败形态。开发者需要的是可操作的错误上下文（trace-id、失败阶段标识、可重试提示），而非一个裸状态码。

---

## 6. 开发者关注点

综合本日数据，开发者反馈中的核心痛点可归纳为：

| 痛点 | 具体表现 | 影响 |
|---|---|---|
| **登录流程不可用** | 授权成功后仍 500，无降级路径 | 完全阻塞使用，无法自愈 |
| **错误信息不透明** | 仅返回 HTTP 500，无失败阶段或 trace 信息 | 用户无法自助排查，只能提 Issue |
| **跨端缺陷扩散** | CLI 与 VS Code 扩展同时受影响 | 修复成本与影响半径同步放大 |
| **缺少重试/回退机制** | 未提及失败后自动重试或备用授权方式 | 网络抖动或服务端瞬时故障即导致失败 |
| **免费层体验风险** | 报告者为 Free plan（Adagio tier） | 若与配额/权限校验相关，可能影响新用户留存 |

**给维护者的建议**

1. 优先确认 v0.42.0 是否引入了认证相关的服务端或 SDK 变更，并公开回滚/热修计划；
2. 在设备授权轮询失败时返回结构化错误（含错误码与 trace-id），替代裸 500；
3. 为 `/login` 增加幂等重试与明确的失败提示，降低用户重复触发造成的噪声 Issue。

---

**明日关注**：#2638 是否获得维护者回应或关联修复 PR；若仓库继续无 PR 活动，可关注是否临近下一次版本发布窗口。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 | 2026-09-11

> 数据来源：github.com/anomalyco/opencode


## 一、今日速览

过去 24 小时无新版本发布，社区讨论热度集中在**存储膨胀与性能问题**——`event` 表无限增长导致 `opencode.db` 达到 13GB+ 的 Issue 持续升温。与此同时，**支付与订阅问题集中爆发**（加密货币支付、支付被拒、免费额度超限），成为社区情绪最集中的方向。PR 方面，TUI 递归分组树、托管提供商策略、Anthropic thinking 块修复等值得关注。


## 二、版本发布

无新版本发布。


## 三、社区热点 Issues（10 个）

### 1. #15585 [CLOSED] 免费模型用量超限
- **重要性**：55 条评论、17 个赞，为当前讨论最热烈的 Issue。用户使用免费模型 Big Pickle 进行长时间会话后遭遇 "free usage exceed" 错误。
- **社区反应**：大量用户确认遇到同类问题，讨论集中在免费额度机制是否透明、是否存在隐藏限制。
- 🔗 https://github.com/anomalyco/opencode/issues/15585

### 2. #33356 [OPEN] event 表无限增长，opencode.db 达 13GB+
- **重要性**：30 条评论、9 个赞。长期运行实例中事件溯源表从未被修剪或压缩，两个实例各达约 13GB，占满 22GB 卷的 97–99%。
- **社区反应**：当前最严重的性能问题之一，开发者呼吁加入保留策略、上限与压缩机制。
- 🔗 https://github.com/anomalyco/opencode/issues/33356

### 3. #23153 [OPEN] 支持加密货币支付 Go 订阅
- **重要性**：21 条评论、50 个赞，是点赞最高的功能需求之一。
- **社区反应**：高赞表明支付方式多样化是社区强烈诉求。
- 🔗 https://github.com/anomalyco/opencode/issues/23153

### 4. #36942 [OPEN] 垂直标签页
- **重要性**：15 条评论、31 个赞。新 UI 强制水平标签，超过 5 个会话标题就难以查看。
- **社区反应**：UI/UX 改进需求突出，尤其针对多会话管理场景。
- 🔗 https://github.com/anomalyco/opencode/issues/36942

### 5. #13003 [OPEN] TUI 显示 Token 用量信息
- **重要性**：13 条评论、53 个赞，点赞数最高。Token 用量（输入/输出/剩余预算）内部有追踪但未在 TUI 显示。
- **社区反应**：成本透明度是开发者非常关心的功能。
- 🔗 https://github.com/anomalyco/opencode/issues/13003

### 6. #45278 [OPEN] 支付被拒（信用卡/银行无异常）
- **重要性**：13 条评论。同一张卡正常使用约 3 个月后突然被拒，银行确认无问题。
- **社区反应**：与 #43400、#48374 等支付问题形成集群，支付稳定性引发担忧。
- 🔗 https://github.com/anomalyco/opencode/issues/45278

### 7. #41358 [OPEN] 自动压缩后代理失去任务目标
- **重要性**：8 条评论。Windows 桌面端长会话中，上下文自动压缩后代理未停止确认即继续执行，且忘记原始任务目标。
- **社区反应**：上下文压缩可靠性问题，影响长任务场景。
- 🔗 https://github.com/anomalyco/opencode/issues/41358

### 8. #41175 [OPEN] event 表存储完整消息快照导致存储过大
- **重要性**：5 条评论、4 个赞。与 #33356 相呼应，指出 event 表存储的是每个流式更新的完整消息副本而非增量，占数据库约 90%。
- **社区反应**：社区已有工具尝试缓解，但根因仍需官方修复。
- 🔗 https://github.com/anomalyco/opencode/issues/41175

### 9. #44788 [OPEN] V2 插件 event.subscribe 不传递事件
- **重要性**：4 条评论。V2 插件 API 无法通过任何文档机制将上下文注入会话模型提示，event.subscribe 注册正常但零事件。
- **社区反应**：V2 插件系统可靠性问题，影响插件生态建设。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报
**日期：2026-09-11** ｜ 数据来源：[github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)

---

## 一、今日速览

v0.23.3 正式版在经历一次发布流程失败后完成修复并发布，同时 TypeScript SDK 0.1.12 与 Desktop 0.3.0 同步跟进。社区今日焦点集中在三条 P1 级问题上：VS Code 扩展 0.23.x 的会话历史回归、非 Qwen 模型因 `metadata` 字段被 DashScope 网关拒收 400、以及 Windows 平台 MCP STDIO 持续报 `-32000 Connection closed`。架构层面，可信 agent 运行时提案（#8102）讨论持续升温，桌面端"弃 Electron 转 Tauri/Web Shell"的路线之争也在推进。

---

## 二、版本发布

### 1. v0.23.3（正式版）
- 主要变更：`feat(core): expand Kimi, Qwen and DeepSeek reasoning presets`（[#11349](https://github.com/QwenLM/qwen-code/pull/11349)）
- 发布过程中 `quality` 环节失败（[#11580](https://github.com/QwenLM/qwen-code/issues/11580)），已由 [#11588](https://github.com/QwenLM/qwen-code/pull/11588) 修复 CI 重放时间线余量问题。
- 无已知破坏性变更。

### 2. v0.23.3-nightly.20260910.c46cb85cf2
- `refactor(dingtalk): remove obsolete background response aggregation`（[#11570](https://github.com/QwenLM/qwen-code/pull/11570)）
- `feat(channels)!` 系列变更（PR 文本被截断，标记为 breaking，建议升级前查看完整变更列表）。

### 3. sdk-typescript-v0.1.12
- 打包 CLI 版本 0.23.3。
- ⚠️ 注意：Release 说明中同时出现了 "bundles CLI version: 0.23.3" 与 "0.23.2" 两处不一致描述，集成方需自行核对。

### 4. desktop-v0.3.0 / desktop-v0.3.0-preview.0
- 正式版：调度化桌面打包 CI（[#11519](https://github.com/QwenLM/qwen-code/pull/11519)）、修复 bridge 中挂起的权限请求。
- 预览版明确提示：`desktop-latest` 更新源仍指向 `0.2.2`，现有安装不会自动升级，需手动安装体验。

---

## 三、社区热点 Issues

### 1. [#8102](https://github.com/QwenLM/qwen-code/issues/8102) — 可信 agent 运行时的确定性工具执行边界（18 条评论）
P3 / core+security。提案将语言模型置于信任边界之外，由运行时对模型产出的动作做确定性的约束、授权、观测与评估。这是本周期评论数最高的架构级讨论，

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*