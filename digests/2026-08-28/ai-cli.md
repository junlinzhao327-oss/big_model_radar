# AI CLI 工具社区动态日报 2026-08-28

> 生成时间: 2026-08-28 04:05 UTC | 覆盖工具: 7 个

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

# Claude Code Skills 社区热点报告（数据截止 2026-08-28）

## 1. 热门 Skills 排行

### 🥇 #1298 — skill-creator 评估脚本修复（评论热度第一）
- **功能**：修复 `run_eval.py` 对所有 Skill 描述均报告 `recall=0%` 的致命缺陷（关联 Issue #556，已有 10+ 独立复现）。该脚本是 `run_loop.py` 和 `improve_description.py` 的信号源，当前整个描述优化循环都在"对着噪声优化"。
- **社区讨论焦点**：评估管线可信度、Windows 兼容性（流读取、触发检测、并行 worker）。
- **状态**：OPEN（作者 @MartinCajiao，2026-06 创建，持续更新）
- 链接：https://github.com/anthropics/skills/pull/1298

### 🥈 #514 — document-typography 文档排版质量技能
- **功能**：治理 AI 生成文档中的孤词换行（1~6 个单词溢出到下一行）、标题悬挂页底（widow paragraphs）、编号对齐错乱等排版问题，覆盖 Claude 生成的几乎所有文档类型。
- **社区讨论焦点**：用户很少主动要求排版质量，但对交付观感影响最直接，属于"刚需但此前无人做"的方向。
- **状态**：OPEN（作者 @PGTBoos，2026-03 创建）
- 链接：https://github.com/anthropics/skills/pull/514

### 🥉 #1628 — Hivemind 零成本多智能体编排技能
- **功能**：让 Claude Code 将机械性工作委托给运行免费模型的无头 opencode worker，Claude 仅承担规划、审查和合并角色。核心理念："昂贵的模型上下文才是稀缺资源，而非智能本身。"
- **社区讨论焦点**：多智能体成本优化范式、任务分配边界。
- **状态**：OPEN（作者 @Hanishchow，2026-08 创建，更新活跃）
- 链接：https://github.com/anthropics/skills/pull/1628

### #486 — ODT 文档技能
- **功能**：支持 OpenDocument 格式（.odt/.ods）的创建、模板填充、读取及 ODT→HTML 转换，覆盖 LibreOffice 等开源/ISO 标准办公场景。
- **社区讨论焦点**：office 文档技能矩阵（docx/pdf/pptx 已有）的补全，开源文档标准的支持需求。
- **状态**：OPEN（作者 @GitHubNewbie0，2026-03 创建，4 月有更新）
- 链接：https://github.com/anthropics/skills/pull/486

### #210 — frontend-design 技能可操作性重构
- **功能**：重写 frontend-design 技能，目标是让每一条指令都能被 Claude 在单次对话中实际执行，指导足够具体以真正改变模型行为。
- **社区讨论焦点**：现有技能"写得像面向人类的文档而非面向模型的操作指令"这一普遍问题（与 Issue #202 对 skill-creator 的批评同源）。
- **状态**：OPEN（作者 @justinwetch，2026-01 创建）
- 链接：https://github.com/anthropics/skills/pull/210

### #723 — testing-patterns 测试模式技能
- **功能**：覆盖完整测试栈——Testing Trophy 模型、单元测试（AAA 模式、纯函数、边界用例）、React 组件测试（Testing Library）、测试哲学与"不该测什么"。
- **社区讨论焦点**：测试生成是编码 Agent 最高频使用场景之一，社区对结构化测试方法论需求明确。
- **状态**：OPEN（作者 @4444J99，2026-03 创建）
- 链接：https://github.com/anthropics/skills/pull/723

### #568 — ServiceNow 全平台技能（评论活跃度持续攀升）
- **功能**：覆盖 ServiceNow 平台级能力——ITSM、ITOM、ITAM/SAM Pro、FSM、HRSD、SPM/PPM、漏洞响应、安全事件响应、IntegrationHub 等。定位为平台助手而非窄脚本工具。
- **社区讨论焦点**：企业级平台技能的广度与深度权衡；从 3 月创建至今持续迭代（8 月仍有更新），显示社区对垂直领域技能的兴趣。
- **状态**：OPEN（作者 @Vanka07，2026-03 创建）
- 链接：https://github.com/anthropics/skills/pull/568

---

## 2. 社区需求趋势（来自 Issues）

### 🔴 安全信任边界（热度最高，43 评论）
**#492**：社区技能在 `anthropic/` 命名空间下分发，冒充官方技能，构成信任边界漏洞——用户可能为"以为是官方的"社区技能授予高权限。这是当前社区最强烈的安全关切。
https://github.com/anthropics/skills/issues/492

### 🟠 组织级分享与协作
**#228**（16 评论，👍 8）：要求支持组织内直接分享技能，替代当前"下载 .skill 文件→Slack/Teams 发送→手动上传"的原始流程。企业采用的关键阻塞点。
https://github.com/anthropics/skills/issues/228

### 🟠 评估/工具链可靠性
**#556**（12 评论，👍 7）：`run_eval.py` 对任何查询都是 0% 触发率——技能评估工具本身不可用，直接动摇整个技能优化流程的可信度。
https://github.com/anthropics/skills/issues/556

### 🟡 技能管理与去重
- **#62**（10 评论）：用户技能无故消失且报错。
- **#189**（6 评论，👍 9）：`document-skills` 与 `example-skills` 插件安装完全相同的技能，导致上下文窗口重复占用。

### 🟡 上下文窗口效率
- **#1487**：`claude-api` 技能单次调用即注入约 156k tokens，直接耗尽上下文窗口。
- **#1329**：compact-memory 技能提案——用符号化记法压缩 Agent 长时记忆的上下文占用。

### 🟡 治理与安全模式
**#412**（已关闭但呼声明确）：agent-governance 技能提案——策略执行、威胁检测、信任评分、审计追踪，目前技能集合缺少安全治理维度。

### 🟢 平台互操作
- **#16**：将 Skills 暴露为 MCP 协议的诉求。
- **#29**：AWS Bedrock 上的使用支持。

---

## 3. 高潜力待合并 Skills（评论活跃尚未合并）

| PR | Skill | 亮点 | 状态 |
|---|---|---|---|
| #514 | document-typography | 解决 AI 文档排版顽疾，普适性强 | OPEN，持续讨论 |
| #486 | ODT | 补全 office 文档技能矩阵的 ISO 标准缺口 | OPEN |
| #723 | testing-patterns | 测试是编码 Agent 最高频场景 | OPEN |
| #568 | ServiceNow | 企业级平台广度罕见，8 月仍在迭代 | OPEN |
| #1628 | Hivemind | 多智能体成本优化，范式新颖 | OPEN（8 月新提） |
| #525 | pyxel | 复古游戏开发（配套 MCP server），垂直场景明确 | OPEN |
| #83 | skill-quality-analyzer + skill-security-analyzer | 元技能——评估技能质量与安全性，呼应 #492 安全关切 | OPEN |
| #1367 | self-audit | 交付前机械验证 + 四维推理质量门禁 | OPEN（v1.3.0） |

合并概率判断：**#514（排版）与 #723（测试）** 普适性最强、与现有技能集合无冲突，落地概率最高；**#83（质量/安全分析器）** 若与 #492 安全议题形成呼应，有可能被官方优先吸收为基础设施型技能。

---

## 4. Skills 生态洞察

> 社区当前最集中的诉求并非"更多新技能"，而是**技能生态的信任与质量基础设施**——可用的评估工具链（#556/#1298）、安全的命名空间与权限边界（#492）、上下文窗口效率（#1487/#1329）以及组织级分享机制（#228），这四项决定了 Skills 能否从"个人玩具"走向"团队/企业级生产工具"。

---

# Claude Code 社区动态日报 — 2026-08-28

## 1. 今日速览

昨日发布两个补丁版本：**v2.1.250** 聚焦可靠性修复，**v2.1.248** 引入全新的 `--restricted` 受限模式（移除命令执行、代码运行与 WebFetch 等内置工具），面向高风险自动化场景提供更强的安全边界。社区端，**Max 订阅用户即时触发用量限制**（#16157，1491 条评论）持续发酵，成为当前最受关注的老大难问题；同时，多个 Windows 桌面应用更新后无法启动的报告（#73107/#89680/#89648）显示该平台稳定性是近期主要痛点。

## 2. 版本发布

### v2.1.250
- 仅含 Bug 修复与可靠性改进，无新功能说明。
- 建议所有用户尽快升级。

### v2.1.248
- 新增 `--restricted` 标志（或设置环境变量 `CLAUDE_CODE_RESTRICTED=1`）：
  - 移除所有可执行命令/代码的内置工具，以及 `WebFetch`（除非在 `--tools` 中显式列出）；
  - 文件工具仅限工作目录内操作；
  - 拒绝 `bypassPermissions`；
  - 忽略用户、项目及本地设置文件。
- 适用于需在不可信目录或 CI 环境中强制降权运行的场景。

## 3. 社区热点 Issues（Top 10）

### ① Max 订阅用户即时触发用量限制
[#16157](https://github.com/anthropics/claude-code/issues/16157) · 开放中 · 👍 693 · 💬 1491  
创建于 1 月，至今仍是最热 Issue。大量 Max 订阅用户反馈在几乎未使用的情况下立即撞上使用上限，涉及 macOS、API 成本核算等多个模块。社区持续施压，Anthropic 尚未给出明确修复时间表。

### ② Claude 4.7/4.8/5.0/Fable 输出陷入修辞套话
[#77136](https://github.com/anthropics/claude-code/issues/77136) · 开放中 · 👍 394 · 💬 108  
开发者反映即便给出明确文体指令，最新模型仍频繁产生“canned rhetorical tics”，连贯散文生成能力退化。该问题直接影响写作类工作流，获大量共鸣。

### ③ 支持同一 Connector 的多个账户（Claude Code Web）
[#27302](https://github.com/anthropics/claude-code/issues/27302) · 开放中 · 👍 361 · 💬 238  
企业用户要求在同一 Connector 下切换不同身份账户，当前只能使用单一账户，阻碍团队协作场景。属于高票功能请求。

### ④ 认证重定向循环：老用户被强制引导至 Onboarding
[#36797](https://github.com/anthropics/claude-code/issues/36797) · 开放中 · 👍 15 · 💬 34  
已有订阅的存量账户在登录时被重定向至 `claude.ai/onboarding`，无法进入主界面。类似报告还有 #74236，疑似认证服务端回归。

### ⑤ Windows 桌面端跨会话消息静默丢失（回归）
[#86298](https://github.com/anthropics/claude-code/issues/86298) · 已关闭 · 👍 1 · 💬 25  
消息被挂起等待一个 UI 从未弹出的审批，约 5 分钟后过期遗失。自桌面应用 1.28929.0 起回归，已关闭但社区仍有讨论。

### ⑥ TUI 多行输入框方向键行为回归
[#63670](https://github.com/anthropics/claude-code/issues/63670) · 开放中 · 👍 11 · 💬 19  
当提示文本软换行超过一行时，Up/Down 仍触发历史命令导航而非光标行间移动。影响全平台，自约 2.1.15 引入。

### ⑦ MCP 连接器拒绝个人 Microsoft 账户
[#53408](https://github.com/anthropics/claude-code/issues/53408) · 开放中 · 👍 23 · 💬 13  
内置 Microsoft 365 MCP 连接器无法登录 Hotmail/Outlook.com/Live 个人账户，OAuth 流程在微软侧被拦截，仅工作/学校账户可用。

### ⑧ Code 标签页污染 transcript JSONL 导致 API 400
[#90002](https://github.com/anthropics/claude-code/issues/90002) · 开放中 · 👍 0 · 💬 10  
昨日新上报：Windows 平台 Code 标签页将 UI 渲染元数据（start/stop_timestamp、flags）写入 transcript JSONL，引发不可恢复的 API 400，即使全量清理后仍复发。

### ⑨ Linux 版 2.1.243 启动即 SIGSEGV
[#89390](https://github.com/anthropics/claude-code/issues/89390) · 开放中 · 👍 12 · 💬 5  
Linux x86_64 上 2.1.243 在启动阶段空指针崩溃，连 `claude --version` 都无法执行；回滚至 2.1.241 恢复正常，疑似发布包缺陷。

### ⑩ Windows 桌面升级后 AppX 容器被占用，无法启动
[#73107](https://github.com/anthropics/claude-code/issues/73107) · 开放中 · 👍 2 · 💬 8  
升级后启动报 `0x80070020`（文件占用），根因为旧版 AppX 容器被一个孤立的高权限 Claude Code 子进程钉住。同类报告 #89680、#89648 也于本周集中出现。

## 4. 重要 PR 进展

> 过去 24 小时内仅 1 条 PR 更新。

### 更新 frontend-design skill
[#69226](https://github.com/anthropics/claude-code/pull/69226) · 已关闭 · 作者 @williamqian12  
对 frontend-design skill 做了若干改进，并将插件版本升至 1.1.0，使已安装副本能自动拉到更新。无社区评论。

## 5. 功能需求趋势

| 方向 | 代表 Issue | 社区热度 |
|---|---|---|
| **多账户/身份体系** | #27302 同一 Connector 多账号切换 | 👍 361 |
| **跨会话连续性** | #89645 持久化定时任务、Claude 自有记忆、外部唤醒触发 | 新提，讨论中 |
| **模型输出质量** | #77136 模型修辞套话、散文连贯性退化 | 👍 394 |
| **安全受限模式** | v2.1.248 `--restricted`；#79575 标志冲突；#77508 沙箱兼容性 | 官方已响应 |
| **认证流程可靠性** | #36797、#74236 登录重定向循环 | 💬 36+，重复上报 |
| **Windows 桌面稳定性** | #73107、#89680、#89648 更新后无法启动 | 3 个独立复现，高优先 |
| **TUI / 终端交互优化** | #63670 多行输入导航回归 | 👍 11，影响全平台 |
| **MCP 生态兼容性** | #53408 个人 Microsoft 账户被拒 | 👍 23 |

## 6. 开发者关注点

- **用量计费透明度**：#16157 表明 Max 订阅用量计算存在明显缺陷，社区强烈要求公开用量核算细节并提供实时反馈，这是当前积怨最深的问题。
- **Windows 桌面应用质量**：一周内出现多条“更新后无法启动”的高质量根因分析（AppX 容器被孤儿进程抢占），开发者普遍认为这与静默自动更新策略相关，期望提供手动回滚渠道。
- **认证流程反复**：多起“老用户被导向 Onboarding”的独立报告，说明认证服务端存在系统性回归，影响存量用户信任。
- **受限/沙箱模式的可用性**：官方虽快速推出 `--restricted`，但社区在沙箱兼容性（Gradle/JVM loopback 被阻断）与标志组合（如 `--append-system-prompt-file` 意外阻止 `/fork`）上仍有不少抱怨。
- **模型行为退化**：不止一位用户对比 4.x/5.x 与旧版本输出，认为推理链变长但文风趋于模板化。此为高频反馈，建议 Anthropic 在模型更新中引入风格稳定性测试。

---

*日报数据来源：github.com/anthropics/claude-code，采集时间 2026-08-28。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-28

## 今日速览

今日社区动态集中在 **Agent 子代理可靠性** 与 **安全加固** 两大方向。多个高优先级 bug（如子代理 max turns 误报成功、通用代理挂起）持续获得维护者关注并进入重测流程；安全方面，围绕 MCP 配置损坏导致的安全失效、扩展环境变量注入等问题的修复 PR 密集推进。此外，夜间版 v0.59.0-nightly.20260828 已自动发布。

## 版本发布

**v0.59.0-nightly.20260828.g3c311beac**（nightly）
- 自动版本更新，无重大功能变更
- 完整变更日志：[查看详情](https://github.com/google-gemini/gemini-cli/compare/v0.59.0-nightly.20260827.g3c311beac...v0.59.0-nightly.20260828.g3c311beac)

## 社区热点 Issues（10 个）

1. **Subagent recovery after MAX_TURNS 被误报为成功** — [#22323](https://github.com/google-gemini/gemini-cli/issues/22323)（💬13 | P1）
   `codebase_investigator` 子代理明明达到了最大轮次限制、尚未执行任何分析，却报告 `status: "success"` 和 `Termination Reason: "GOAL"`。该问题掩盖了真实的执行中断，误导用户判断。社区评论 13 条，热度最高，已进入 need-retesting 阶段。

2. **通用代理（Generalist agent）无限挂起** — [#21409](https://github.com/google-gemini/gemini-cli/issues/21409)（💬8 | P1 | 👍8）
   用户报告当 CLI 将任务委派给通用代理时会无限期挂起（等待长达一小时）。简单的文件夹创建操作也会触发。当前唯一的 workaround 是指示模型不要使用子代理。该问题获得 8 个 👍，是社区受影响面较大的 P1 问题。

3. **启用 bash 亲和力：零依赖 OS 沙盒与执行后意图路由** — [#19873](https://github.com/google-gemini/gemini-cli/issues/19873)（💬8 | P2）
   Gemini 3 模型天然具备 bash 使用能力，该 issue 提议通过零依赖沙盒方案让模型充分发挥原生 bash 能力，同时保障用户安全。讨论热度高，代表了 Agent 能力演进的重要方向。

4. **评估 AST 感知的文件读取/搜索/代码库映射的价值** — [#22745](https://github.com/google-gemini/gemini-cli/issues/22745)（💬7 | P2）
   该 EPIC 追踪一系列关于 AST 感知工具是否有价值的调研，希望通过精确读取方法边界来减少 token 噪声和调用次数。这反映了社区对 token 效率和上下文优化的持续关注。

5. **Gemini 不够主动使用 skills 和子代理** — [#21968](https://github.com/google-gemini/gemini-cli/issues/21968)（💬6 | P2）
   用户反馈即使用户自定义了 gradle、git 等 skill 并附上了清晰描述，Gemini 依然几乎不会主动调用，只有在明确指令下才会使用。这暴露了模型在工具选择主动性上的明显短板。

6. **Shell 命令执行完成后卡在 "Waiting input"** — [#25166](https://github.com/google-gemini/gemini-cli/issues/25166)（💬4 | P1 | 👍3）
   一个 P1 级别 core 问题：简单的 CLI 命令执行完成后，终端仍显示命令活跃并等待用户输入，导致流程卡死。获得 3 个 👍，是影响日常开发效率的高频痛点。

7. **browser 子代理在 Wayland 环境下失败** — [#21983](https://github.com/google-gemini/gemini-cli/issues/21983)（💬4 | P1）
   Linux Wayland 显示服务器下 browser subagent 运行失败，终止原因为 GOAL。属于浏览器代理的兼容性问题，影响 Linux 用户群体。

8. **Auto Memory 无限重试低信号会话** — [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)（💬5 | P2）
   当提取代理判定某会话低信号并跳过时，该会话不会被标记为已处理，会被反复重新呈现。反映了自动记忆机制在索引管理上的缺陷。

9. **Auto Memory 的确定性脱敏与日志精简** — [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)（💬4 | P2 | 安全）
   Auto Memory 在将本地转录发送给模型前，脱敏行为发生在内容已进入模型上下文之后，存在安全隐患。社区对隐私和敏感信息处理表达了明确关切。

10. **扩展更新可绕过用户同意并注入环境变量** — PR [#28863](https://github.com/google-gemini/gemini-cli/pull/28863) 关联（💬 安全相关）
    该 PR 修复了扩展更新可能绕过用户同意检查，并向 MCP server 进程注入未经授权的环境变量的问题。涉及安全边界，值得用户关注。

## 重要 PR 进展（10 个）

1. **扩展环境变更需用户同意 + 环境变量消毒** — [#28863](https://github.com/google-gemini/gemini-cli/pull/28863)
   将 MCP server 环境配置纳入同意字符串生成，并过滤自定义环境变量中可改变运行时行为的条目，修复安全绕过问题。

2. **read_file 内容路由至 FileSystemService** — [#29110](https://github.com/google-gemini/gemini-cli/pull/29110)
   修复 `read_file` 直接读本地磁盘而忽略 `FileSystemService` 注入的问题。此前 ACP 客户端可声明 `fs.readTextFile` 能力但实际被绕过，破坏权限模型一致性。

3. **工作区信任失败关闭 + 受限模式过滤 mcpServers** — [#29099](https://github.com/google-gemini/gemini-cli/pull/29099)
   在非信任或受限环境下强制执行失败关闭的工作区信任解析，并过滤仓库定义的 `mcpServers`，防止服务启动期间发生意外进程执行。

4. **SSE 最终事件在 EOF 时不再丢失** — [#29106](https://github.com/google-gemini/gemini-cli/pull/29106)
   修复 SSE 解析器在流结束缺少尾部空行时静默丢弃最终缓冲事件的问题，避免丢失 `finishReason` 和 usage 元数据。

5. **stripShellWrapper 处理多行转义引号** — [#27467](https://github.com/google-gemini/gemini-cli/pull/27467)（已关闭）
   改用 shell-quote 解析，正确提取和反转义包含转义引号的多行命令（如 `bash -c "hg commit -m \"title\n\nbody\""`）。

6. **MCP enablement 配置损坏不再视为空配置** — [#28787](https://github.com/google-gemini/gemini-cli/pull/28787)（已关闭）
   修复 JSON 解析失败时被折叠为空对象 `{}` 的 bug，防止所有 MCP server 意外恢复默认启用状态。

7. **修复 MCP enablement 配置损坏导致的安全失效与数据丢失** — [#28794](https://github.com/google-gemini/gemini-cli/pull/28794)（已关闭）
   `readConfig()` 在 JSON 解析失败时返回 `{}`，导致 fail-open 和潜在的数据丢失，现已修复。

8. **Slash 命令自动补全增加 [Skill] 标签** — [#29104](https://github.com/google-gemini/gemini-cli/pull/29104)
   为 skill 驱动的斜杠命令在 `/` 自动补全菜单和 `/help` 中添加 `[Skill]` 标签，与现有 `[MCP]`、`[Agent]` 视觉风格保持一致，提升可发现性。

9. **on-retry 提示注入 contents 以保留前缀缓存** — [#28914](https://github.com/google-gemini/gemini-cli/pull/28914)
   将重试 nudge 从 `systemInstruction` 移至 `contents` 末尾，保留静态提示前缀缓存，并确保模型在生成前立即看到恢复提示。

10. **frontmatter 解析器剥离引号并处理块标量** — [#29006](https://github.com/google-gemini/gemini-cli/pull/29006)（已关闭）
    修复 YAML 解析失败回退到简单解析时，name 和 description 保留引号的问题；同时优雅处理 `|` 和 `>` 块标量指示符。

## 功能需求趋势

从今日 50 条活跃 Issues 中可提炼出以下社区重点关注方向：

- **Agent/子代理行为可靠性（最高优先级）**：大量 P1/P2 issue 集中在子代理误报成功、挂起、不支持 Wayland、忽略配置覆盖等可靠性问题上，约占活跃 issue 的 60% 以上
- **安全加固**：围绕 MCP 配置损坏的 fail-open 风险、扩展环境变量注入、Auto Memory 的敏感信息处理，形成了完整的安全修复链条
- **Token 效率与上下文优化**：AST 感知文件读取、Tactful Extraction（精准读取避免 context firehose）、持久化任务追踪替代 in-context todo，构成"减少 token 浪费"的解决方案矩阵
- **模型主动性与工具使用**：社区持续反馈模型不主动使用 skills/子代理，且倾向于创建临时脚本而非直接编辑文件，指向工具调用策略的改进需求
- **终端体验与性能**：Shell 命令卡死、终端 resize 闪烁高刷等问题，核心体验的稳定性成为关注点

## 开发者关注点

- **误报与状态失真**：#22323 中 max turns 被上报为成功，这类"假阳性"完成信号比直接报错更具危害性，开发者担心会破坏对 Agent 完成状态的信任
- **挂起与无限等待**：通用代理挂起、shell 命令完成后等待输入等"卡死"类问题，直接打断开发流程，开发者对此容忍度最低
- **配置与安全边界**：开发者高度关注 MCP 配置损坏导致的"意外启用"和扩展环境变量注入风险，期望安全的默认行为是 fail-closed 而非 fail-open
- **子代理可见性**：多个 issue（如 `bugreport` 不含子代理上下文、subagent 轨迹无法通过 `/chat share` 分享）反映开发者希望获得更完整的执行追踪能力
- **工具调用的智能性**：开发者希望模型能更聪明地在合适时机使用合适的工具（如主动调用已配置的 skill、避免创建零散临时文件），减少人工介入和清理成本

---
*数据截止 2026-08-28，涵盖 50 条活跃 Issues 和 16 条活跃 PRs。*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>



</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

⚠️ 摘要生成失败。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-28

## 今日速览

昨日发布 `v0.22.2-nightly`，修复了 WebShell 会话差异恢复与钉钉富文本保留问题。社区方面，最热门的讨论集中在 API 流式超时（#5975，13 条评论）与 TUI 渲染层迁移方案（#8662，10 条评论）两个长期痛点。此外，多 Agent 与 MCP 工具链相关的 PR 密集推进，成为当前开发主线。

## 版本发布

**v0.22.2-nightly.20260828.7357136dd1**

- `fix(web-shell)`: 恢复已保存的会话差异（@ytahdn，[#10093](https://github.com/QwenLM/qwen-code/pull/10093)）
- `fix(channels)`: 保留钉钉富文本多格式内容（详见 [Release 页面](https://github.com/QwenLM/qwen-code/releases)）

## 社区热点 Issues

### 1. API 流式超时问题持续发酵 — [#5975](https://github.com/QwenLM/qwen-code/issues/5975)
`[P2/bug]` 13 条评论 · 1 👍 · 状态：待分类
> 升级到 v0.19.3 后频繁出现 "No stream activity for 120000ms after 19 chunks" 错误，此前必定先显示 "Thought for 2s" 再没有输出。这是一个跨版本长期未解决的稳定性问题，被标记为 `welcome-pr`。

### 2. TUI 渲染层迁移跟踪 — [#8662](https://github.com/QwenLM/qwen-code/issues/8662)
`[P3/enhancement]` 10 条评论 · 状态：等待反馈
> 当前基于 ink 7 + React 19 的 TUI 存在闪烁等结构性问题。社区提议迁移到 OpenTUI，并已形成跟踪 issue。配套设计文档 PR #10343 已提交，属于影响深远的架构级改动。

### 3. 自定义模型供应商（Moonshot）无法对话 — [#10227](https://github.com/QwenLM/qwen-code/issues/10227)
`[P2/bug]` 6 条评论 · 状态：需补充信息
> 报错 `tools.function.parameters is not a valid moonshot flavored json schema`，说明 Qwen Code 生成的工具参数 schema 与 Moonshot 方言不兼容。第三方供应商兼容性仍是高频痛点。

### 4. LM Studio 本地模型解析语法失败 — [#10065](https://github.com/QwenLM/qwen-code/issues/10065)
`[P2/bug]` 6 条评论 · 状态：待人工处理
> 即使关闭全部 MCP/工具，Qwen Code 请求本地 LM Studio 模型仍报 "failed to parse grammar"。本地模型用户受影响较大。

### 5. E2E 测试在部分 runner 上挂起 — [#10272](https://github.com/QwenLM/qwen-code/issues/10272)
`[P1/bug]` 5 条评论 · 已关闭
> `external-context-mem0` 测试套件在 macOS 和 ecs-qwen 池上卡在 "Connecting to MCP servers"，ubuntu 则通过。属于 CI 基础设施层面的平台差异问题。

### 6. 升级 0.22 后本地命令执行与文件编辑失败 — [#10147](https://github.com/QwenLM/qwen-code/issues/10147)
`[P2/bug]` 3 条评论 · 状态：需补充信息
> 用户反馈 0.22 版本完全丧失本地命令执行和文件编辑能力，并建议增加禁止自动升级的开关。属于高影响回归类问题。

### 7. 推理过程渲染错乱 — [#9475](https://github.com/QwenLM/qwen-code/issues/9475)
`[P2/bug]` 4 条评论 · 状态：待分类
> 工具调用输出 stuck 在底部而推理内容从顶部刷新，插入点随机，最终输出前界面完全混乱。与 #8662 的 TUI 迁移直接相关。

### 8. Ollama 工具调用后用户消息丢失 — [#9438](https://github.com/QwenLM/qwen-code/issues/9438)
`[P1/bug]` 4 条评论 · 已关闭
> 工具调用后的 follow-up 请求丢失 `role: "user"` 消息，导致 Ollama 返回 500 错误。已修复，但作为 P1 回归问题值得关注。

### 9. Release provenance 安全缺陷 — [#10336](https://github.com/QwenLM/qwen-code/issues/10336)
`[P1/bug/security]` 2 条评论 · 状态：待人工处理
> npm 发布产物的 provenance 记录的是分发上下文而非实际构建树 hash，导致发布产物无法与 tag 源码验证关联。供应链安全问题，需尽快处理。

### 10. hooks 触发事件增强 — [#10348](https://github.com/QwenLM/qwen-code/issues/10348)
`[P3/feature-request]` 4 条评论 · 新建
> 希望在智能体发起提问（如 YOLO 模式）时也能触发 hooks 事件，以便后台任务通过飞书/桌面推送提醒。反映了对 hooks 事件覆盖面的扩展诉求。

## 重要 PR 进展

### 1. [fix(core)] 退出后保留 fire-and-forget hooks — [#10288](https://github.com/QwenLM/qwen-code/pull/10288)
> 让 `MessageDisplay`、`StopFailure`、`SessionDelete` 等输出忽略型 hooks 在进程退出后仍能完整执行，避免输入/截止时间/进程树监督信息丢失。通过 mode-0600 临时文件实现安全落地。

### 2. [fix(daemon)] 取消超时会话初始化 — [#10268](https://github.com/QwenLM/qwen-code/pull/10268)
> 将已有的会话初始化预算变为端到端权威：ACP new-session 请求携带绝对截止时间，子进程将取消传播至 Gemini 启动与 SessionStart hooks。

### 3. [feat(web-shell)] 持久化推理努力级别 — [#10011](https://github.com/QwenLM/qwen-code/pull/10011)
> WebShell 中调整的 reasoning effort 实时更新活跃会话，并持久化为全局 `model.reasoningEffort` 默认值，daemon 重启后仍生效。

### 4. [

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*