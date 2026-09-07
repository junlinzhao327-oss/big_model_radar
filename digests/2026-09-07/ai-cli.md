# AI CLI 工具社区动态日报 2026-09-07

> 生成时间: 2026-09-07 00:03 UTC | 覆盖工具: 7 个

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

# Kimi Code CLI 社区动态日报（2026-09-07）

## 今日速览

过去 24 小时内，Kimi Code CLI 无新版本发布；共有 5 个 Issue 和 1 个 PR 发生更新。最受关注的是 #1282「远程控制本地会话」功能请求（👍 32），以及 #2252 希望对标 Codex/Claude Code 增加 `/goal` 命令并支持将 coding plan 导入 Codex。PR 方面，#2513 正在修复 Moonshot API 工具调用参数双重编码导致的校验失败问题。

## 社区热点 Issues

过去 24 小时共更新 5 个 Issue，以下全部收录。

- [#1282 [enhancement] Remote Control - Continue local sessions from any device](https://github.com/MoonshotAI/kimi-cli/issues/1282)  
  作者 @CatKang | 开放中 | 👍 32 | 评论 13  
  **亮点**：建议增加「远程控制」能力，让用户从手机、平板或任意浏览器继续本地 Kimi Code CLI 会话，保持完整本地环境的同时实现跨设备工作流无缝衔接。这是当前社区关注度最高的需求，32 个 👍 说明用户对「随时离开工位、又不中断编码上下文」的场景有较强刚需。

- [#2252 [enhancement] 希望增加 /goal 命令并允许 coding plan 导入到 Codex 中使用](https://github.com/MoonshotAI/kimi-cli/issues/2252)  
  作者 @DuskLin | 已关闭 | 👍 2 | 评论 9  
  **亮点**：用户希望参考 Codex 的 `/goal` 命令，并指出 Claude Code 在 138 版本已跟进该功能；同时认为 Kimi coding plan 不支持导入 Codex 难以理解。该 Issue 已关闭但仍有讨论，反映社区对「跨 AI 编程工具互操作」和「任务目标管理」的需求。

- [#1284 [bug] Does not launch in Zed IDE ACP panel in Windows](https://github.com/MoonshotAI/kimi-cli/issues/1284)  
  作者 @prashanth057 | 已关闭 | 👍 0 | 评论 1  
  **关注点**：在 Windows 平台（版本 1.14.0）中，Kimi Code CLI 无法在 Zed IDE 的 ACP 面板中启动。涉及 IDE 集成、Windows 平台兼容性，虽然是已关闭 Issue，但仍在近期被更新，说明该问题对 Zed + Windows 用户有持续影响。

- [#1350 [bug] 频繁出现 Authorization failed, please check your login status](https://github.com/MoonshotAI/kimi-cli/issues/1350)  
  作者 @dapeng1162 | 已关闭 | 👍 0 | 评论 0  
  **关注点**：在 Debian 12 上使用 `/login` 登录后，使用 `kimi-for-coding` 模型时频繁出现 `Authorization failed`。认证稳定性直接影响日常开发，值得官方持续关注；0 条评论也说明该问题可能仍未获得充分反馈处理。

- [#1349 [bug] shell prompt no longer shows cwd/git branch; request configurable display](https://github.com/MoonshotAI/kimi-cli/issues/1349)  
  作者 @Sirfetch-d | 已关闭 | 👍 0 | 评论 0  
  **关注点**：近期版本中 shell prompt 不再显示当前工作目录（cwd）和 git 分支，只显示 `✨ / 💫 / $` 等符号，导致交互式编码时难以确认上下文。用户希望恢复或提供可配置显示选项，这属于 CLI 使用体验的关键细节。

## 重要 PR 进展

过去 24 小时更新的 PR 共 1 条，已收录。

- [#2513 fix(kosong): recursively decode double-encoded tool-call arguments](https://github.com/MoonshotAI/kimi-cli/pull/2513)  
  作者 @nitishagar | 开放中 | 更新于 2026-09-06  
  **内容**：Moonshot API 返回的 `function.arguments` 中，嵌套数组/对象值可能以 JSON 字符串形式出现（即双重编码）。单次 `json.loads` 后类似 `todos` 的值仍是字符串，进而导致 Pydantic 校验失败（`Input should be a valid list`）。该 PR 新增共享的 `decode_tool_arguments` 工具函数进行递归解码，以正确处理嵌套结构。该修复对工具调用稳定性较为关键，尤其是依赖结构化参数的编码场景。

## 功能需求趋势

从本期更新的 Issues 中可以看出几个方向：

1. **远程控制与跨设备工作流**（#1282）：用户希望打破本地终端会话的设备绑定，支持手机、平板、浏览器远程接入。这是当前呼声最高、点赞最多的功能方向。
2. **跨 AI 工具生态互操作**（#2252）：社区希望 Kimi CLI 能与 Codex、Claude Code 等主流 agent 生态兼容，如补齐 `/goal` 命令，并允许 coding plan 导入其他平台。
3. **终端交互信息可配置性**（#1349）：用户对 shell prompt 的信息密度敏感，期望保留 `cwd`、git branch 等关键上下文，并提供自定义能力。
4. **IDE 集成完善**（#1284）：Zed + Windows 等特定组合下仍存在启动问题，开发者希望 Kimi Code CLI 在主流 IDE 的 ACP/插件面板中稳定运行。
5. **认证/登录稳定性**（#1350）：跨 Linux 环境下出现频繁 `Authorization failed`，认证链路可靠性是阻塞日常使用的心智痛点。

## 开发者关注点

- **认证失败高频出现**（#1350）：用户使用 `/login` 后仍频繁掉登录态，浪费大量时间在重新认证上，且反馈响应不足。
- **跨平台兼容仍显不足**（#1284）：Windows 下 Zed IDE 无法启动 ACP 面板，说明官方在非主流开发环境上的适配仍需投入。
- **上游 API 数据解析异常需快速兜底**（#2513）：工具参数双重编码会导致结构化调用失败，开发者希望 CLI 侧能透明地兼容这类服务端边界情况。
- **对标竞品功能成为一种诉求**（#2252）：社区会以 Codex / Claude Code 的功能为基准，反向要求 Kimi CLI 补齐规划、导入/导出等能力。
- **远程无缝续跑需求明显**（#1282）：本地会话与远程设备之间的连续工作流，已成为 Coding Agent 工具的重要使用场景，开发者期待尽早落地。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-09-07

## 今日速览

昨日共发布 3 个版本（含 1 个 preview 与 2 个 nightly），核心工作集中在 Web Shell 动态工作流可视化；社区最热议题聚焦于导出文件体积优化、工具调度取消竞态，以及一个 P1 级遥测隐私泄露问题（可追溯至文本上传至 RUM 时未脱敏）。此外，CI 可靠性问题持续攀升，多起 release workflow 超时/失败引发关注。


## 版本发布

### v0.23.1-preview.1
> Release notes generated using configuration in .github/release.yml at release/v0.23.1-preview.1

**What's Changed**
- **feat(web-shell):** visualize and manage dynamic workflow runs by [@qqqys](https://github.com/qqqys) ([#10594](https://github.com/QwenLM/qwen-code/pull/10594))
- **perf(web-shell):** derive the session workflow project

> ⚠️ 该版本的 release workflow 发生失败——失败任务：`integration_docker`。详见 issue [#11185](https://github.com/QwenLM/qwen-code/issues/11185)

### v0.23.0-nightly.20260906.92a8a8d179 / v0.23.0-nightly.20260905.0c945a6136

两个 nightly 的变更内容相同（指向同一 PR 集）：
- **feat(web-shell):** visualize and manage dynamic workflow runs ([#10594](https://github.com/QwenLM/qwen-code/pull/10594))
- **perf(web-shell):** derive the session workflow project。

---

## 社区热点 Issues（10 条）

### 🔥 P1 安全/隐私类

**1. Usage-statistics telemetry 向 RUM 上传未脱敏的工具错误文本** ⭐ 重点关注
- **Issue:** [#11198](https://github.com/QwenLM/qwen-code/issues/11198)（`P1` / `security` / `data-privacy` / `credential-security`）
- **为什么重要：** 默认开启的使用统计通道将工具错误的原始文本（含 shell 命令行）不由分说地上传至 RUM 端点。该问题在 `main` 分支上已存在，范围比先前 #10916 中标记的单个字段更大。对使用私有环境或涉及敏感命令的开发者来说，这属于数据泄露级别的隐患。

**2. skill 的 PreToolUse hook 在 `--continue` 后失效**
- **Issue:** [#11180](https://github.com/QwenLM/qwen-code/issues/11180)（`P1` / `security` / `hooks-events`）
- **为什么重要：** skill 的 SKILL.md 中声明的 `PreToolUse` 安全门在普通会话中可正常工作，但在 `--continue` 恢复会话后则不再执行，而 skill 的指令仍保留在上下文中——意味着“安全门可能被静默跳过”，安全语义被打破。与 [#11067](https://github.com/QwenLM/qwen-code/issues/11067)（`/<skill-name>` 启动时不运行 PreToolUse）属于同类问题，指向 hooks 生命周期管理的系统缺陷。

### 🐞 工具调度 / 取消竞态

**3. 已取消的工具请求仍会阻塞在无关的活动批次之后**
- **Issue:** [#11146](https://github.com/QwenLM/qwen-code/issues/11146)（`P2` / `core` / `tools`）
- **为什么重要：** `CoreToolScheduler.schedule()` 在调度器正在运行或正在收尾一个批次时，会将已 abort 的请求也排入队列，且该请求会一直等待与该请求无关的活动批次完成后才会被清理。会导致取消操作无法及时生效。

**4. CLI 常规排队工具取消时跳过了完成清理（completion cleanup）**
- **Issue:** [#11162](https://github.com/QwenLM/qwen-code/issues/11162)（`P2` / `cli` / `tools`）
- **为什么重要：** 常规交互调度分支在 `CoreToolScheduler` 因信号中断拒绝一个排队请求时会静默返回，阻止调用方的完成处理器（completion handler）执行。与 #11146 同根，会影响工具调用的资源释放。

### 📦 导出架构 / 体积优化

**5. mermaid (~6 MB) 仍被打进导出的 transcript 渲染器**
- **Issue:** [#11091](https://github.com/QwenLM/qwen-code/issues/11091)（`P2` / `build-system` / `web-shell` / 已关闭）
- **为什么重要：** #9812 合并后导出的 HTML 不再内联渲染器，但 `@qwen-code/qwen-code` 的 `export-transcript-document.js` 中仍将 mermaid（约 6 MB）整体打入。该 issue 关联 #11038 / #11031，是导出瘦身系列的后续收尾。社区评论 7 条，显示对产物体积优化有较高关注度。

**6. 导出的 transcript 入口仍携带 daemon hook 运行时**
- **Issue:** [#11100](https://github.com/QwenLM/qwen-code/issues/11100)（`P2` / `build-system` / `web-shell`）
- **为什么重要：** `@qwen-code/web-shell/transcript` 虽然是只读 transcript 入口，但其静态值导入图中仍通过三个真实渲染的组件可达 `daemon-react-sdk`。即只读导出文档依旧带着完整的 daemon React 运行时，与 #11031 的优化目标背道而驰。

### ⚙️ CI / 工程效率

**7. release.yml 重复执行已有工作，一步 20 分钟的检查形同虚设**
- **Issue:** [#1109](https://github.com/QwenLM/qwen-code/issues/11109)（`P2` / `ci-cd` / `github-actions`）
- **为什么重要：** 昨日两次 release 运行超时（[33957952281](https://github.com/QwenLM/qwen-code/actions/runs/33957952281)、[33963757913](https://github.com/QwenLM/qwen-code/actions/runs/33963757913)）。release.yml 大量时间在重复同一 run 已完成的工作，且其中一步耗时 20 分钟的检查“什么也没有验证”，是纯工程浪费。评论中有较多讨论，是 CI 可靠性的集中代表。

**8. web-shell E2E Smoke 是 ECS 池中唯一仍用固定超时的任务**
- **Issue:** [#11209](https://github.com/QwenLM/qwen-code/issues/11209)（`P2` / `ci-cd` / 已关闭）
- **为什么重要：** 与其他三个已接入动态预算的任务不同，`web-shell E2E Smoke` 仍使用 `timeout-minutes: 20`，导致在 PR 完全不涉及待测代码时也因资源争抢被杀掉并报告为 `cancelled`。直接拖慢了 CI 的反馈速度。

### 🎨 架构级追踪

**9. 将 TUI 渲染层从 ink 迁移至 OpenTUI（tracking）**
- **Issue:** [#8662](https://github.com/QwenLM/qwen-code/issues/8662)（`P3` / `ui` / `terminal-ux` / 评论 30 条）
- **为什么重要：** 这是当前社区评论最多的 issue。qwen-code 现有 TUI 基于 **ink 7 + React 19**，带有一个 1037 行的重度补丁渲染器（`patches/ink+7.0.3.patch`）和自研 Virtual Viewport 模式，引发了闪烁等一系列结构性难题。30 条评论说明该话题在开发者社区关注度高、讨论充分，是中期重要的架构演进方向。

### 🤖 自动化 / Bot 生态

**10. Fleet Shepherd Dashboard（自动维护）**
- **Issue:** [#7167](https://github.com/QwenLM/qwen-code/issues/7167)（`ci-cd`）
- **为什么重要：** 该 issue 为 Fleet Shepherd 工作流自动维护的机器人舰队看板，每日更新。从数据中可看到 bot PR 状态（如 #11134 处于 idle），用于追踪自动化生产的 PR 的实时健康度。


## 重要 PR 进展（10 条）

**1. feat(serve): scope extensions to workspace runtimes**
- **PR:** [#11086](https://github.com/QwenLM/qwen-code/pull/11086)（`autofix/takeover` / 更新时间 09-07）
- **内容：** 将全局扩展目录通过各 workspace 选定的 runtime 提供；协调扩展状态到活跃的 workspace runtime，暴露 workspace 限定的 daemon/SDK 访问，并更新扩展管理、composer add 菜单及 `@` 引用。
- **点评：** 属于服务端扩展体系的重要架构调整，更新时间为今日，值得关注。

**2. fix(vscode): canonicalize workspace paths**
- **PR:** [#11201](https://github.com/QwenLM/qwen-code/pull/11201)（更新时间 09-07）
- **内容：** 在启动 Web Shell daemon、持久化活跃 session key、引导嵌入式 shell 及导出 session 前，对 VS Code workspace 路径做规范化。例如 macOS 上 `/tmp` 是指向 `/private/tmp` 的符号链接，可能导致路径不一致问题。
- **点评：** 修复跨平台路径解析不一致，影响所有 macOS 用户，实用价值高。

**3. feat(web-shell): add a context usage tab to the right sidebar**
- **PR:** [#11177](https://github.com/QwenLM/qwen-code/pull/11177)（更新时间 09-07）
- **内容：** 在 Web Shell 右侧边栏新增 Context Usage 入口，与现有 Token Usage 并列；通过 opt-in 的 header action（stacked-layers 图标）打开会话级别的 `context_usage` 面板，展示实时 context-window 占用情况。
- **点评：** 上下文占用可视化是开发者长期诉求，此 PR 直接补上了可观测性短板。

**4. fix(cli): prevent dialog clipping in short terminals**
- **PR:** [#9040](https://github.com/QwenLM/qwen-code/pull/9040)（`review/self-reported` / 更新时间 09-07）
- **内容：** 防止 `/statusline` 与 `/skills` 配置对话框在终端高度受限时渲染出界。`/statusline` 在低于 16 行时使用可选择的紧凑布局；`/skills` 仅在存在高度预算时限制锁定行。
- **点评：** 小屏/小终端用户的高频痛点修复，等待 review 的时间较长。

**5. feat(core): auto-retry transient network errors (EOF) where Ctrl+Y is unavailable**
- **PR:** [#10347](https://github.com/QwenLM/qwen-code/pull/10347)（`review/self-reported` / `autofix/needs-human`）
- **内容：** 将实际为底层网络错误的 4xx（如 `400 network error ... EOF`、peer 在请求中途关闭连接）分类为可重试的传输错误，使现有有界自动重试生效——此前这类错误被当作快速失败的客户端错误。
- **点评：** 对使用不稳定网络的开发者极有价值，自动重试可显著减少手动干预。

**6. fix(ci): retry the transient all-green macOS E2E shard death once**
- **PR:** [#11134](https://github.com/QwenLM/qwen-code/pull/11134)（`review/self-reported` / `autofix/needs-human`）
- **内容：** macOS E2E 新增与 Linux `sandbox:none` 相同的单次预算门控重试机制：shard 命令进入 `run_shard()`，仅在失败后执行第二次，且受剩余 job 预算限制。
- **点评：** 直接缓解 macOS CI 偶发全绿死亡的痛点，提升 CI 可信度。

**7. feat(dingtalk): show dynamic lifecycle tags**
- **PR:** [#10504](https://github.com/QwenLM/qwen-code/pull/10504)（`autofix/takeover` / `review/self-reported`）
- **内容：** 为钉钉集成添加本地化的生命周期反馈，不暴露原始工具输入/输出/推理；turn 活跃期间，源消息保持 `👀` 并附加 Thinking、Reading、Searching、Running、Editing、Retrying 等状态反应。
- **点评：** 对钉钉重度用户是直观体验提升；不泄露原始内容的设计很到位。

**8. feat(core): preserve prompt cache for deferred tools**
- **PR:** [#10410](https://github.com/QwenLM/qwen-code/pull/10410)（`autofix/takeover`）
- **内容：** 用稳定的两步桥替代延迟工具的 schema 揭示：`tool_search` 允许模型在声明工具列表不变的情况下查看延迟工具 schema；`tool_call` 负责校验并调用该延迟工具。
- **点评：** 可节省大量 prompt 缓存重算成本，对带延迟工具的长会话有直接收益。

**9. fix(cli): guard channel pidfiles against PID reuse**
- **PR:** [#10687](https://github.com/QwenLM/qwen-code/pull/10687)（`autofix/takeover` / `review/self-reported`）
- **内容：** Channel 服务的 pidfile 现在持久化 Linux process-start token，并在读取、信号或等待该进程时进行校验。PID 被回收但进程仍在运行的情况被视为过期，不会向新进程误发信号；standalone 与 `qwen serve` 共享同一套实现。
- **点评：** 守护进程管理中的经典坑，修复方式严谨，值得肯定。

**10. refactor(daemon): decouple extension activation refresh**
- **PR:** [#10991](https://github.com/QwenLM/qwen-code/pull/10991)（`autofix/takeover`）
- **内容：** 扩展激活操作在激活策略持久化完成后即算完成，不再直接刷新所有活跃会话；新增 `extension_activation_explicit_refresh` capability 以区分新旧 daemon 的契约差异。Web Shell 相应适配。
- **点评：** 斩断扩展激活与全局刷新的耦合，提升扩展激活性能与稳定性。


## 功能需求趋势

从全部 issue 中可提炼出如下社区聚焦方向：

1. **数据导出体积与架构（Export Data Redesign）：** 围绕 #11031、#11091、#11100 组成的系列工作，目标是将单个导出 HTML 从 19.5 MB 级别压缩到可接受范围，此方向是当前 Web Shell 最活跃的工程主题。
2. **TUI 架构现代化：** #8662 提出的 ink → OpenTUI 迁移（30 条评论）代表底层渲染层的重构意愿，与 dialog 裁剪（#9040）等终端体验优化共同支撑 roadmap/terminal-ux。
3. **安全与隐私加固：** 包括 telemetry 脱敏（#11198）、PreToolUse hook 一致性问题（#11180、#11067）、本地文件桥信任边界（#11169）等，security 类 P1/P2 issue 密度在上升。
4. **工具调用与任务调度的可靠性：** 多条 issue（#11146、#11162）指向 tool scheduler 的取消竞态与资源清理行为；同时 #10347 在尝试让网络层瞬时错误自动重试。社区对 agent 工具层的健壮性容忍度正在降低。
5. **CI/CD 稳定性与效率：** release.yml 重复劳动（#11109）、E2E 超时误杀（#11209）、macOS 偶发死亡（#11134）等多点开花，反映

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*