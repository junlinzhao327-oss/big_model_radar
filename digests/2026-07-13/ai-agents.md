# OpenClaw 生态日报 2026-07-13

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-12 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 | 2026-07-13

---

## 今日速览

过去 24 小时内，OpenClaw 社区保持极高活跃度：共处理 500 条 Issue 更新（新开/活跃 297 条，关闭 203 条）和 500 条 PR 更新（待合并 347 条，已合并/关闭 153 条）。合并/关闭的 PR 主要集中在备份快照、UI 输入维护、CI 稳定性及会话状态修复等方向。无新版本发布，但大量待合并 PR 表明开发输出充沛，合并瓶颈值得关注。社区讨论热度最高的 Issue 是跨平台桌面应用支持（#75），已获 110 条评论与 81 个点赞。

---

## 版本发布

今日无新版本发布。

---

## 项目进展

今日有 9 个重要 PR 被合并/关闭（标记为 `CLOSED`），涵盖功能增强、缺陷修复和技术债务清理：

- **备份功能强化**：`feat(backup): add verified SQLite snapshots`（#105718）与 `Add SQLite snapshot artifacts under backup`（#94805）合并，为备份命令添加了可验证的 SQLite 快照能力，可创建、验证、恢复和列出快照，直接回应多次报告的状态库损坏问题（如 #101290、#71689）。
- **UI 修复**：`fix(ui): prevent New Session input loss during creation`（#105702）修复了创建新会话时用户编辑可能被静默丢弃的问题；`fix(ci): stabilize terminal lifecycle waits`（#105714）解决了 CI 中的终端生命周期超时失败。
- **代码清理**：`chore(ui): drop dead config-form search exports`（#105713）和 `refactor(ui): trim private search exports`（#105705）移除了无用的导出，保持代码库健康。
- **配置重构**：`refactor(config): retire flat streaming keys from the last six channel schemas via doctor migration`（#105709）对 Signal、IRC、WhatsApp 等六个频道的扁平流式键配置进行了统一迁移。
- **会话稳定性**：`fix: include archived transcript lineage in session usage detail`（#92610）修复了会话用量统计未包含归档转录音的问题。`fix: stop Claude tool heartbeats from hiding stuck sessions`（#96198）解决了 Claude 工具心跳导致卡死会话被误判为正常的问题。

这些合并在备份可靠性、用户交互和会话基础架构上带来了可衡量的前进。

---

## 社区热点

过去 24 小时讨论最活跃的 Issue/PR：

- **#75 – Linux/Windows Clawdbot Apps**（评论 110 👍81）：自 2026 年 1 月提出，至今仍是最受关注的需求。用户要求补齐 macOS/iOS/Android 之外的桌面端支持，呼声极高，但还未进入产品决策阶段。
- **#99241 – 工具输出渲染为图片附件**（评论 22 👍2）：在长时间运行的 ANSI 重工作流中，工具结果被压缩为 `(see attached image)` 占位符，导致 agent 无法读取原始 stdout/stderr 文本，严重阻碍调试。
- **#91588 – 网关内存泄漏**（评论 19 👍1）：RSS 从 350MB 增长至 15.5GB 导致 OOM 崩溃，持续多天影响生产部署，被标记为 P0。
- **#102175 – 嵌入提示缓存跨边界失效**（评论 16 👍1）：长会话中 prompt-cache 复用因房间事件、策略、响应边界切换而丢失，影响成本与性能。
- **#65161 – 心跳隔离模式异常**（评论 15 👍1）：2026.4.10 版本后心跳调度停滞、事件错误标记、状态写入缺失。

社区焦点集中在三类诉求：**跨平台支持**（#75）、**工具输出可读性**（#99241）和**基础稳定性**（#91588 等）。

---

## Bug 与稳定性

以下为今日报告或仍处于活跃状态的关键 Bug，按严重程度排列。若已有关联 fix PR 则标注。

| 严重性 | Issue | 摘要 | 状态 |
|--------|-------|------|------|
| P0 | #91588 | 网关内存泄漏：RSS 持续增长至 15.5GB 导致 OOM 崩溃 | 无 fix PR |
| P0 | #104721 | **所有工具结果返回 `(see attached image)` 字面字符串**，而非实际输出；严重回归 | 无 fix PR |
| P0 | #101290 | CLI 启动前健康检查命令可导致 SQLite 损坏（"database disk image is malformed"） | 关联 #94805（快照工具） |
| P1 | #63216 | 同一会话键反复硬重置，即使 `reserveTokensFloor` 已调高 | 无 fix PR |
| P1 | #53408 | 长对话后 `write`/`exec` 工具参数静默丢失 | 无 fix PR |
| P1 | #89228 | 隔离 cron 会话中 `exec` 间歇不可用（曾在 4.1 修复，现回归） | 关联 PR（标记 `linked-pr-open`） |
| P1 | #94939 | 6.x 迁移后频道会话存储 SQLite 为空（0 字节），导致 MS Teams 主动发送失败 | 已关联 PR |
| P1 | #47910 | 提供者故障类回退未区分鉴权失败 vs 限速，浪费重试 | 有 `fix-shape-clear` |
| P1 | #91009 | Codex PreToolUse 钩子 spawn CPU 高峰期进程，阻塞网关 RPC | 关联 PR |
| P1 | #39476 | A2A `sessions_send` 双向调用导致消息重复 | 关联 PR |
| P1 | #90639 | 保护模式允许会话增长至上限导致 "Something went wrong" 且无法在 Slack 内恢复 | 无 fix PR |

今日没有新报告 P0/P1 Bug，上述多数为长期问题。值得警惕的是 #104721（全部工具输出被替换为占位符）是严重回归，需紧急响应。

---

## 功能请求与路线图信号

用户提出的新功能需求（来自最新 Issues 及 PR 中的意图）表明以下方向可能会被纳入下一版本：

1. **安全加固**：
   - `Feature Request: Memory Trust Tagging by Source`（#7707）：对记忆条目按来源打信任标签，防记忆中毒。
   - `Feature Request: Masked Secrets`（#10659）：agent 可使用 API 密钥但不能读取明文。
   - `Denylist support for exec-approvals`（#6615）：拒绝列表，允许“除 X 外全部通过”。
   - 今日合并的 `fix(security): add estimate-before-decode guard to base64 paths`（#105323）和已打开的 `fix(github-copilot): reject unvalidated OAuth enterprise domain`（#105584）表明安全修复持续活跃。

2. **模型与提供者改进**：
   - `Dynamic model discovery`（#10687）：OpenRouter 等快速变更目录的自动模型发现。
   - `Trigger model fallback on context length exceeded`（#9986）：上下文超限时触发回退，而非冻结。

3. **会话与工具增强**：
   - `Webhook hook sessions reuse existing session`（#11665）：实现多轮对话，已有 PR 关联。
   - `Config option to suppress sub-agent announce`（#8299）：避免子 agent 自动发布摘要。
   - `maxTurns/maxToolCalls config option`（#9912）：限制 agent 工具调用迭代次数，防止失控。
   - `Ralph Loop per-agent configuration`（#6890）：允许 agent 定义默认 Ralph 迭代次数。

4. **用户体验**：
   - `Shift+Enter for newline in TUI`（#10118）：已获 4 赞，高频需求。
   - `Accessibility: disable emojis in TUI`（#9637）：屏幕阅读器兼容性。
   - `Per-model generation timeout`（#8724）：解决 Google 模型无限思考循环。

路线图信号：**安全、记忆管理、模型回退**正在成为下一阶段的重点。备份快照功能（已合并）则回应了长期来的数据损毁投诉。

---

## 用户反馈摘要

从 Issues 评论中提炼的真实用户痛点与使用感受：

- **稳定性是最大不满**：“gateway 每几天 OOM 一次，生产环境无法使用”（#91588）；“所有工具输出都变成图片占位符，完全不可用”（#104721）；“写文件工具在 15 轮对话后参数全丢”（#53408）。
- **跨平台缺口阻碍采用**：“我们有 macOS/iOS/Android 应用，但 Linux 和 Windows 用户被排除在外” (#75)。该 Issue 已获 81 个赞，是社区最强烈的单一需求。
- **工具可见性差**：“agent 看不到自己的输出，只能看到 `(see attached image)`，调试如同盲人摸象”（#99241）。
- **配置灵活性不足**：“没有 maxTurns 限制，模型可能无限循环工具调用”（#9912）；“fallback 只处理 API 错误，上下文超限却不触发”（#9986）。
- **部分满意改善**：SQLite 快照功能获正面反馈（#94805 关联 #101290），用户表示“至少现在能看到备份是否有效了”。UI 创建会话丢失修复（#105702）得到积极评论。

---

## 待处理积压

以下 Issue/PR 长期未得到回应或停滞，提醒维护者优先关注：

| 编号 | 标题 | 创建时间 | 最后更新 | 标签 | 备注 |
|------|------|----------|----------|------|------|
| #75 | Linux/Windows Clawdbot Apps | 2026-01-01 | 2026-07-12 | enhancement, P2 | 110 评论，81 赞，需产品决策 |
| #91588 | Gateway Memory Leak (P0) | 2026-06-09 | 2026-07-12 | P0, clawsweeper:no-new-fix-pr | 无 fix PR，严重危害生产 |
| #63216 | Repeated hard resets on same session | 2026-04-08 | 2026-07-12 | stale, P1 | 3 赞，需实时复现 |
| #65161 | Heartbeat isolated mode regression | 2026-04-12 | 2026-07-12 | stale, P1 | 15 评论，需产品决策 |
| #69822 | feat(session-message-events) socket.drain | 2026-04-21 | 2026-07-12 | 等待作者 | 已停滞 3 个月，需跟进 PR |

此外，P0 问题 #104721（全部工具输出变占位符）虽创建于 2026-07-11，但至今无任何 fix PR 或 maintainer 响应，急需排查。

---

---

## 横向生态对比

好的，作为AI智能体与个人AI助手开源生态的资深技术分析师，我将基于您提供的各项目2026-07-13动态摘要，为您呈现一份横向对比分析报告。

---

## 个人AI助手开源生态横向对比分析日报（2026-07-13）

### 1. 生态全景

当前个人AI助手/自主智能体开源生态整体处于**从“功能可用”向“生产可靠”与“体验精致”过渡的关键阶段**。一方面，核心项目如 OpenClaw 和 Hermes Agent 的社区贡献极其活跃（日均数百条Issues/PRs），大量功能请求和Bug修复并行推进，但合并/发布瓶颈明显，暴露出规模化管理挑战。另一方面，用户诉求高度集中：**稳定性（内存泄漏、工具输出吞没）、多模态支持（图像渲染、视频输入）、模型回退/流控**以及**跨平台桌面端**成为普遍痛点。此外，安全加固（SSRF、敏感信息泄露、信任标签）和协议标准化（MCP/ACP）正成为多方共同押注的方向，预示着下一阶段的技术竞赛将围绕**生态互操作性**与**企业级可靠性**展开。

---

### 2. 各项目活跃度对比

| 项目 | 今日Issues更新数 (新开+活跃 / 关闭) | 今日PR更新数 (待合并 / 已合并+关闭) | 版本发布 | 健康度评估 |
|------|--------------------------------------|---------------------------------------|----------|------------|
| **OpenClaw** | 297 / 203 | 347 / 153 | 无 | **黄灯**（极高吞吐但合并瓶颈明显；P0级内存泄漏与工具输出回归未修复） |
| **Hermes Agent** | 134 / 366 | 443 / 57 | 无 | **绿灯**（修复效率极高，大量旧Issue标记为已合并；但存在“npm劫持”严重安装问题） |
| **OpenHands SDK** | (数据未明确分量，共约数十条) | (2个关键PR合并，多个修复PR进行中) | 无 | **绿灯**（安全防线增强，历史数据修复；但关键Bug如SecretStr解析、并发配置失效已有快速响应） |
| **Pi** | 31个关闭 / 数据未提供新开数 | 9个关闭 / 少量开放 | 无 | **绿灯**（核心维护者修复效率高，TUI与模型适配快速响应） |
| **LiteLLM** | 23 / 9 (新开23，关闭9) | 34 / 34 (更新总计118，84待合并) | 3个 (v1.91~1.93rc) | **黄灯**（高频发布但存在发布版本缺失补丁的问题；模型适配滞后，安全漏洞待修补） |
| **Temporal** | 1 / 0 | 1 / 2 (1个合并，1个自动化) | 无 | **绿灯**（项目成熟，开发节奏平稳；唯一Issue为代码清理，无新Bug报告） |

*注：健康度评估基于Bug严重性、响应速度、合并效率综合判断。绿灯表示短期风险较低；黄灯表示存在需紧急关注的问题或瓶颈。*

---

### 3. OpenClaw 在生态中的定位

- **核心优势**：作为生态中**社区规模最大、功能最全面**的通用Agent框架（参照项目），其功能覆盖面（CLI/UI/MCP/备份/会话管理）远超其他项目。今日合并的SQLite快照功能直接呼应了长期的数据损毁投诉，表明项目在**数据面可靠性**上持续投入。
- **技术路线差异**：与Hermes Agent更强调“Agent原生协议”和“看板工人”等自动化工作流不同，OpenClaw更像一个**全栈集成平台**，从底层存储到上层UI一应俱全，但这也导致其**包体积和复杂度**显著高于Pi等轻量级项目。
- **社区规模对比**：OpenClaw的每日Issues/PR总数（1000条）是Hermes Agent（1000条）类似强度，但比Pi（约40条）、OpenHands SDK（约20条）和LiteLLM（150条）高出一个数量级。这也带来了最严重的**合并瓶颈**：347个PR等待合并，远高于其他项目（Hermes的443个待合并状态类似，但其关闭率更高）。
- **风险亮点**：跨平台桌面支持（#75）获81赞，是生态中最强烈的单一用户需求，但长期未进入产品决策，可能成为对手（如Pi的TUI v2）抢占用户的抓手。

---

### 4. 共同关注的技术方向（多项目涌现）

| 技术方向 | 涉及项目 | 具体诉求 |
|----------|----------|----------|
| **模型兼容性与回退** | OpenClaw, LiteLLM, Pi, Hermes Agent | 主流模型（DeepSeek V4、Claude Opus 4.7/4.8、GPT-5.6、Gemma 4）的多轮对话失败、参数不兼容、上下文超限回退缺失；原生支持Google/Vertex AI热度极高。 |
| **安全加固** | OpenClaw, OpenHands SDK, LiteLLM | 记忆信任标签（#7707）、Base64路径guard、OAuth域校验；SSRF漏洞（CVSS 7.5）、OAuth Open Redirect；SDK内置LLM安全分析器。 |
| **工具输出可视化与可读性** | OpenClaw, Pi | 工具结果被压缩为“（see attached image）”占位符（P0回归）；TUI中用户图像不渲染。 |
| **会话与记忆管理** | OpenClaw, Hermes Agent, OpenHands SDK | 会话历史校验、记忆来源信任标签、MCP tools/list_changed订阅、Scope-recall独立记忆插件。 |
| **平台兼容性与桌面端** | OpenClaw, Pi, Hermes Agent | Linux/Windows桌面应用缺失（81赞）；macOS桌面字体控制；Docker部署体验差。 |
| **配置灵活性与日志降噪** | OpenClaw, LiteLLM, Temporal | maxTurns/toolCalls限制、工具权限拦截日志降级、错误脱敏范围明确。 |

---

### 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent | OpenHands SDK | Pi | LiteLLM | Temporal |
|------|----------|--------------|---------------|----|---------|----------|
| **功能侧重** | 全栈通用Agent平台 | Agent协议+看板工人自动化 | 面向开发者的Agent SDK库 | 终端UI体验极致优化 | LLM代理网关/成本控制 | 工作流编排引擎（非Agent） |
| **目标用户** | 开发者/团队/生产部署 | 高级用户/自动化运维 | 解决方案架构师/SDK集成方 | 命令行重度用户/终端爱好者 | 企业运维/路由/成本管理 | 后端微服务/分布式工作流开发者 |
| **技术架构** | 单体+MCP插件+CLI/UI | Agent原生协议+看板工人隔离 | 纯Python SDK，依赖Pydantic | 轻量级Rust CLI，TUI v2 | Python Proxy+Router，FastAPI | Go服务端，gRPC，强一致性 |
| **核心弱点** | PR合并瓶颈、跨平台缺失 | 安装体验差（npm劫持）、仪表盘UI差 | 配置兼容性（SecretStr）、文档不足 | 多模态支持滞后（用户图像不显示） | 模型适配滞后、版本遗漏补丁、安全漏洞 | 功能迭代慢、Nexus组件仍不成熟 |

---

### 6. 社区热度与成熟度

- **快速迭代阶段（高频变动，稳定性欠佳）**：**OpenClaw、Hermes Agent、LiteLLM**。日均上百条Issues/PRs，新功能与Bug并存，社区活跃但生产用户需谨慎评估。其中OpenClaw和LiteLLM存在P0级未修复问题（内存泄漏、工具回归），风险最高。Hermes Agent虽修复效率高，但安装体验问题（npm劫持）可能劝退新用户。
- **质量巩固阶段（中等活跃，注重核心体验）**：**Pi、OpenHands SDK**。Issues/PRs数量适宜，维护者响应迅速，Bug修复精准。Pi聚焦TUI和模型兼容性，OpenHands SDK聚焦安全与协议标准化，两者均无重大未解决问题。
- **成熟稳定阶段（低变动，路线明确）**：**Temporal**。每日仅少量活动，项目已进入企业级工作流领域的成熟期，功能迭代节奏慢但可靠性高，适合作为基础设施。

---

### 7. 值得关注的趋势信号（对AI智能体开发者的参考）

1. **“安全左移”正成为标配**：从LLM安全分析器到SSRF修复、记忆信任标签，安全不再只是外围配置，而是嵌入Agent框架核心。开发者应优先采用内置安全机制的框架，避免后期补丁带来的架构冲突。
2. **多模态与模型兼容性是最大竞争分水岭**：工具输出吞没、图像不渲染、推理内容字段错误等问题直接导致Agent“失明”。下一阶段，谁能最快速适配新模型（如DeepSeek V4、GPT-5.6）并保持多模态交互的透明度，谁就能赢得用户心智。
3. **协议标准化（MCP/ACP）从“可选”走向“必须”**：OpenHands SDK和Hermes Agent均在推进MCP工具变更通知、ACP会话配置增强。开发者应优先选择原生支持MCP/ACP的项目，以降低集成成本和未来迁移风险。
4. **Token成本与上下文压缩成为企业刚需**：LiteLLM的Compresr护栏、TTFT超时检测，以及各项目对模型回退的诉求，反映出企业对“可控成本”和“稳定延迟”的极致追求。具备成本监控、上下文压缩功能的网关或SDK将获得更强壁垒。
5. **跨平台桌面端仍是生态真空带**：OpenClaw的#75获81赞却无行动，Pi的TUI v2全屏查看器正在突破终端体验上限。开发者若能在Windows/Linux桌面端提供原生、低门槛的Agent交互，有望快速获取被主流项目忽视的用户群体。

---
**总结**：当前AI智能体生态正处于“百家争鸣向协议兼容、安全可控、体验精细”过渡的关键窗口。OpenClaw和Hermes Agent作为社区双雄，规模与风险并存；Pi、OpenHands SDK以专注度取胜；LiteLLM与Temporal则在各自细分领域稳固占据。开发者应依据自身对稳定性、功能丰富度、平台偏好的需求，选择最匹配的项目深度参与。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 Hermes Agent 数据，为您生成 2026年7月13日的项目动态日报。

---

### Hermes Agent 项目动态日报 | 2026-07-13

---

### 1. 今日速览

今日项目活跃度极高，社区贡献和问题处理均非常积极。过去24小时内，共有 **500条** Issues和 **500条** PRs 被更新，其中 **366条** Issues 和 **57条** PRs 被关闭或合并，显示出项目维护者对社区反馈的响应速度和处理能力依然强劲。今日无新版本发布，但大量针对特定Bug的修复和新功能PR已提交。值得注意的是，自动化工具（如“sweeper”）在问题处理中发挥了重要作用，许多旧Issue被标记为“implemented-on-main”，表明修复已经完成。社区讨论热点集中在 Dashboard 界面的可读性、对 Google 原生/Vertex AI 提供商的支持以及桌面端的用户体验上。

### 2. 版本发布

**无**

---

### 3. 项目进展

尽管没有新的 Release，但项目在多个方面取得了实质性进展，主要关注于错误修复、平台兼容性和用户体验优化。

-   **关键修复已合并至主分支**：大量的旧 Issue 被关闭并标记为 “sweeper:implemented-on-main”，表明以下问题可能已在最新代码中解决：
    - **平台支持**：`#17753` (Windows系统读取本地文件失败)、`#15290` (NAS Docker环境权限问题)、`#18646` (WhatsApp群组消息路由错误)、`#9756` (微信多账号支持) 等问题已被关闭。
    - **Provider 稳定性**：`#15551` (自定义端点不执行命令)、`#20244` (Gemini HTTP 500错误)、`#16551` (Copilot OAuth令牌交换问题)、`#18529` (会话标题泄露思维链信息) 等问题已被修复。
    - **功能增强**：`#12639` 和 `#13484` (原生 Google Vertex AI 提供商支持)、`#10644` (添加 Brave Search 搜索后端)、`#19559` (MCP客户端重连机制) 等新功能已合并。
-   **重要PR提交**：多个重要的修复性 PR 在今日被提交，显示出社区对项目稳定性的持续贡献。
    - `#63421` [OPEN]: 修复了分离式看板工人跨进程审批的问题。
    - `#63431` [OPEN]: 修复了 Matrix 网关关闭时可能出现的数据库损坏问题。
    - `#63433` [OPEN]: 修复了内容策展人（Curator）提示中缺少明确指令导致工作流失败的问题。

**总体评价**：项目正在高效地消化前期的社区反馈，将大量积压的 Bug 和新功能请求转化为实际代码，项目成熟度和稳定性得到进一步提升。

---

### 4. 社区热点

今日社区讨论集中在以下两个核心议题上，反映了用户对 **“界面可用性”** 和 **“AI提供商自由度”** 的强烈诉求。

1.  **[Feature]: Improved Themes for Dashboard - currently hard to read (#18080)**
    -   **热度**: 评论 28 | 👍 50
    -   **链接**: [Issue #18080](https://github.com/NousResearch/hermes-agent/issues/18080)
    -   **诉求分析**: 该 Issue 获得的点赞数最高（50个），表明大量用户对 Dashboard 的默认主题感到不满，认为其字体、颜色对比度差，难以阅读。这虽然是一个长期存在的 Issue（创建于4月30日），但今日被关闭，说明项目方已经或即将对主题进行改进。用户对产品视觉体验的期望正成为重要关注点。

2.  **[Subtext] Google / Vertex AI 原生支持**
    -   **热度**: `#12639` (评论15, 👍10), `#13484` (评论13, 👍14)
    -   **链接**: [Issue #12639](https://github.com/NousResearch/hermes-agent/issues/12639), [Issue #13484](https://github.com/NousResearch/hermes-agent/issues/13484)
    -   **诉求分析**: 多个高赞 Issue 都指向对 Google Gemini 原生 API 和 Vertex AI 的支持。用户受够了通过 OpenRouter 等第三方路由时遇到的 402 错误和速率限制。他们希望直接与 Google 服务对接以获得更稳定的连接、更低的延迟和更好的配额管理。这表明用户对 AI 模型的接入稳定性和成本控制有很高的要求。

---

### 5. Bug 与稳定性

今日报告中，一些较严重或影响范围广的 Bug 已经或正在被修复。

-   **严重**:
    -   **npm全局安装被劫持 (#18357)**: Setup脚本会将自身的npm安装到 `~/.hermes/node` 并替换系统 npm，导致其他软件安装失败。用户形容这是“破坏计算机完整性的行为”。目前该Issue仍为 **OPEN** 状态，需要高度关注。
        -   [Issue #18357](https://github.com/NousResearch/hermes-agent/issues/18357)
-   **中等**:
    -   **看板工人协议违规 (#27178)**: 当 agent 以文本回复结束对话而非调用 `kanban_complete` 时，看板工人会报告 `protocol_violation`。该Issue仍为 **OPEN** 状态。
        -   [Issue #27178](https://github.com/NousResearch/hermes-agent/issues/27178)
    -   **TUI网关重启后挂起**：对应修复已提交 PR `#63437`。
        -   [PR #63437](https://github.com/NousResearch/hermes-agent/pull/63437)
-   **低/已修复**:
    -   **桌面端字体/缩放控制 (#40166)**: 用户希望在macOS桌面应用上调整字体大小，享受原生缩放快捷键。该Issue仍为 **OPEN** 状态。
        -   [Issue #40166](https://github.com/NousResearch/hermes-agent/issues/40166)
    -   **Mattermost频道会话冲突 (#18279)**: 不同线程的顶层帖子会合并到同一个会话中。该问题已通过关闭的Issue标记为已修复。
    -   **Discord附件传递不可靠 (#11860)**: 文件附件无法可靠地传入Agent上下文。该问题已标记为已修复。
    -   **看板工人历史记录解析失败 (#63430)**: `kanban_show` 命令在遇到 `ended_at = NULL` 的记录时会崩溃。对应修复 PR 已提交。
        -   [PR #63430](https://github.com/nousresearch/hermes-agent/pull/63430)
    -   **标题生成泄露思维链 (#18529)**: 使用“思考”模型时，会话标题会包含模型的内部推理过程。该问题已标记为已修复。
    -   **Matrix 加密处理器关闭顺序问题 (#63431)**: 可能导致数据库损坏。对应修复 PR 已提交。
        -   [PR #63431](https://github.com/nousresearch/hermes-agent/pull/63431)

---

### 6. 功能请求与路线图信号

-   **高可能性**:
    -   **原生 Google / Vertex AI 提供商**: 多个高赞 Issue (#12639, #13484) 和 PR 推动此功能，预计会很快进入主线或下一个版本。这可能是路线图上最明确的信号。
    -   **音视频功能增强**:
        -   **WebUI TTS音频播放**: PR `#16717` 为 WebUI 添加了浏览器端 TTS 音频播放功能，目前仍为 **OPEN** 状态，很可能继续推进。
        -   **TTS/STT插件指南**: PR `#63432` 提供了详细的 TTS 和语音转文字（STT）提供者插件开发指南，表明项目在鼓励社区构建语音能力。
-   **社区呼声高，待评估**:
    -   **Scope-recall 独立记忆提供者插件 (#42864)**: 用户提出了一种新的记忆管理插件，强调当前轮次召回和可审计本地存储。这反映了社区对更精细、更透明记忆管理方案的需求。
        -   [Issue #42864](https://github.com/NousResearch/hermes-agent/issues/42864)
    -   **模型预设与专家按需升级 (#20249)**: 用户希望在会话中能够根据任务复杂度自动切换模型（如从 Flash 升级到 Opus）。这是一个高级功能，虽已被标记为 “not-planned”，但反映了高端用户对最优成本/性能平衡的追求。
        -   [Issue #20249](https://github.com/NousResearch/hermes-agent/issues/20249)
-   **长期可能**:
    -   **Slovak (sk) 本地化**: PR `#63426` 添加了斯洛伐克语支持，项目国际化进程在稳步推进。

---

### 7. 用户反馈摘要

-   **满意之处**:
    -   **功能响应迅速**：用户对于 Brave Search 搜索的加入 (👍23) 和 Google Vertex AI 的支持有强烈需求，并被快速响应。
    -   **插件系统潜力**：社区通过 PR `#20303`（Mixin Network消息工具）展示了对插件系统的利用，生态系统正在萌芽。
-   **不满意/待改进**:
    -   **安装与配置体验**：`#18357`（npm劫持）、`#15290`（Docker权限）、`#12188`（Docker文档不足）等 Issue 尖锐地指出，项目的安装和配置过程对用户非常不友好，甚至被形容为“破坏性”。**这是项目成长中最需要迫切改善的环节之一**。
    -   **界面可用性**：至少有 50 名用户通过点赞 `#18080` 来表达对 Dashboard 可读性的不满。
    -   **特定Provider稳定性**：用户对 Gemini (`#15895`, `#20244`) 和 Copilot (`#16551`) 等特定提供商的连接问题感到困惑和沮丧。
    -   **Docker体验**：`#14448` 中用户直言“你的 Docker 用户体验太糟糕了”，指出了用户ID不匹配、文件挂载不清晰等具体问题。

---

### 8. 待处理积压

以下为已存在一段时间、未被打上 `implemented-on-main` 标签、且尚未关闭的关键 Issue 和 PR，建议维护者关注：

1.  **`#18357` (严重): Setup脚本破坏系统npm**
    -   **状态**: OPEN
    -   **原因**: 此问题严重且用户反馈激烈，可能涉及复杂的安装/升级流程修改，需要谨慎处理，但优先级应最高。
    -   [Issue #18357](https://github.com/NousResearch/hermes-agent/issues/18357)

2.  **`#40166` (持续关注): 桌面端应用缺少字体控制**
    -   **状态**: OPEN
    -   **原因**: 获得了 17 个赞，是持续的用户痛点。修复相对独立，可能适合社区贡献者。
    -   [Issue #40166](https://github.com/NousResearch/hermes-agent/issues/40166)

3.  **`#16717` (长期PR): WebUI TTS音频播放**
    -   **状态**: OPEN
    -   **原因**: 该 PR 创建于 4月27日，是一个较大的功能增强，但似乎一直未被合并。可能需要解决与现有架构的兼容性问题或等待 code review。
    -   [PR #16717](https://github.com/NousResearch/hermes-agent/pull/16717)

4.  **`#20295` (长期PR): 修复空对话历史处理**
    -   **状态**: OPEN
    -   **原因**: 一个关于 API 端点的关键 Bug 修复，创建于 5月5日，至今未被合并。这可能影响所有通过 API 发起的会话。
    -   [PR #20295](https://github.com/NousResearch/hermes-agent/pull/20295)

5.  **`#50164` (长期PR): 添加内存上下文验证**
    -   **状态**: OPEN
    -   **原因**: 一个重要的测试和验证 PR，旨在提升 Agent 长期记忆的可靠性。创建已超三周，但仍未合并。
    -   [PR #50164](https://github.com/NousResearch/hermes-agent/pull/50164)

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 OpenHands SDK (software-agent-sdk) GitHub 数据，为您生成一份结构清晰的 2026-07-13 项目动态日报。

---

## OpenHands SDK 项目日报 (2026-07-13)

**数据统计周期**：2026-07-12 至 2026-07-13

### 1. 今日速览

项目今日活跃度极高，Issues 和 PR 更新频繁，主要集中在核心架构稳定性与 MCP/ACP 协议兼容性上。社区反馈的 `SecretStr` 解析错误和 `max_concurrent_runs` 配置失效等关键 Bug 已迅速得到修复 PR 响应，体现了项目团队对用户反馈的及时跟进。此外，多项关于 MCP 增强和 ACP 会话管理的功能提议正在被积极讨论，显示出项目正向更成熟、标准化的协议支持方向迈进。

### 2. 版本发布

本日无新版本发布。

### 3. 项目进展

过去24小时内，有2个重要 PR 被关闭或合并，对项目稳定性有显著提升：

- **[已合并] 安全功能增强**：`feat(security): add ToolShieldLLMSecurityAnalyzer` ([#2911](https://github.com/OpenHands/software-agent-sdk/pull/2911)) 被合并。此 PR 实现了一个基于 LLM 的安全分析器，加强了对 Agent 行为安全性的检测能力，是项目安全防线的重要补充。
- **[已关闭] 历史数据修复**：`fix: heal history orphaned by pre-#4068 legacy-resume __root__ bug` ([#4090](https://github.com/OpenHands/software-agent-sdk/pull/4090)) 被关闭。该 PR 提出并解决了一个在特定旧版本中可能导致会话历史数据损坏的深层 Bug，提升了历史记录的可靠性。

此外，多个正在推进的 Bug 修复 PR (如 [#4097](https://github.com/OpenHands/software-agent-sdk/pull/4097)、[#4095](https://github.com/OpenHands/software-agent-sdk/pull/4095)) 也表明团队正在集中力量解决稳定性问题。项目整体正朝着更健壮、更安全的方向稳步前进。

### 4. 社区热点

今日讨论最活跃的 Issue 是：

- **持续集成运行状态追踪**：`[tracker] [Tracker] Daily Integration Runs` ([#2078](https://github.com/OpenHands/software-agent-sdk/issues/2078))，该 Issue 作为每日集成运行的占位符，拥有高达 **135** 条评论。虽然这是一个长期存在的机器人维护帖，但其高评论量反映了社区对项目整体质量与自动化集成测试流程的高度关注。

### 5. Bug 与稳定性

今日报告的 Bug 问题较多，且集中在接口兼容性和关键功能失效上，按严重程度排列如下：

- **高危：`SecretStr` 反序列化错误导致连接失败**：Bug [#4096](https://github.com/OpenHands/software-agent-sdk/issues/4096) 报告了 OpenHands 前端无法连接到 agent-server，原因是 Pydantic 在解析 JSON 时，`SecretStr` 类型的字段出现校验错误。**已存在修复 PR**：[#4097](https://github.com/OpenHands/software-agent-sdk/pull/4097) 已针对此问题提交，进展迅速。
- **高危：`max_concurrent_runs` 配置失效**：Bug [#4063](https://github.com/OpenHands/software-agent-sdk/issues/4063) 指出，该配置项仅对同步执行生效，而对使用 `EventService` 的异步并发执行无效，导致并发限制功能形同虚设，是严重的功能缺陷。
- **中危：MCP Schema 迁移未正确应用**：Bug [#4052](https://github.com/OpenHands/software-agent-sdk/issues/4052) 报告了用户存在旧 MCP 配置时，Schema 迁移未能正确执行，导致设置项出错。关联修复 PR：[#4013](https://github.com/OpenHands/software-agent-sdk/pull/4013) 正在进行中。
- **中危：ACP 0.11 版本兼容性问题**：Bug [#4093](https://github.com/OpenHands/software-agent-sdk/issues/4093) 指出，未设置版本上限的 `agent-client-protocol` 依赖在升级到 0.11.0 后，由于该版本移除了某些字段，导致与 Gemini CLI 等上游工具出现兼容性问题。**暂无关联修复 PR**。
- **一般：空流式响应未触发重试**：Bug [#4095](https://github.com/OpenHands/software-agent-sdk/pull/4095) 针对一个内部 Issue [#4077](https://github.com/OpenHands/software-agent-sdk/issues/4077) 提出了修复，解决了当 LLM 返回空流式响应时，SDK 未能触发重试机制的问题。

### 6. 功能请求与路线图信号

今日用户和开发者的功能请求主要集中在增强 MCP 和 ACP 协议的深度集成上，这些很可能是未来版本的重点：

- **增强 ACP 会话配置能力**：Issue [#4062](https://github.com/OpenHands/software-agent-sdk/issues/4062) 建议，Agent Server 应支持 ACP Agent 广告的所有会话级 `configOptions`，并能接收 `session/set_config_option` 更新，而不仅限于 `model` 选项。这是一个向 ACP 标准看齐的重要信号。
- **订阅 MCP `tools/list_changed` 通知**：Issue [#4059](https://github.com/OpenHands/software-agent-sdk/issues/4059) 请求支持订阅 MCP 服务器的工具变更通知，以便动态刷新可用工具列表。关联 PR：[#3894](https://github.com/OpenHands/software-agent-sdk/pull/3894) 正在实现此功能。
- **标记过时的兼容性别名**：Issue [#4058](https://github.com/OpenHands/software-agent-sdk/issues/4058) 要求对弃用的字段和别名发出 SDK 弃用警告，并生成对应的 Schema 标记。这是一个提升开发者体验和代码健壮性的举措。关联 PR：[#4004](https://github.com/OpenHands/software-agent-sdk/pull/4004)。

以上功能请求均有明确对应的 PR 在推进，表明它们有很高的可能性被纳入下一版本迭代。

### 7. 用户反馈摘要

从今日 Issues 的讨论中，我们可以提炼出以下用户痛点：

- **配置复杂性与兼容性问题**：一位用户 (kripper) 在 [#4096](https://github.com/OpenHands/software-agent-sdk/issues/4096) 中提到，为了绕过连接错误，他不得不从配置中手动移除非 LLM 提供商的 MCP 配置。这表明当前配置的依赖和解析逻辑对用户不够友好，尤其是在混合使用不同 MCP 服务时。
- **版本依赖风险**：用户 (smolpaws) 在 [#4093](https://github.com/OpenHands/software-agent-sdk/issues/4093) 中明确指出，由于依赖 `agent-client-protocol` 未设置版本上限，当上游库发布不向后兼容的版本时，项目会立即受损。这体现了用户对依赖管理的敏感性和对稳定性的高要求。
- **文档与实际行为不符**：用户 (neubig) 在 [#4063](https://github.com/OpenHands/software-agent-sdk/issues/4063) 中指出了配置项 `max_concurrent_runs` 文档与实际行为不一致的问题，这属于可用性问题，影响了用户对系统行为的预期管理。

### 8. 待处理积压

以下为长期未关闭或未获得更新，但仍对项目健康度有潜在影响的重要 Issue/PR，提醒维护者关注：

- **长期功能对等追踪**：Issue `Feature Parity: Bridge Gap with Claude Code Capabilities` ([#2055](https://github.com/OpenHands/software-agent-sdk/issues/2055))，自 2026-02-13 创建，作为与 Claude Code 功能对等的 Master 追踪 Issue。此 Issue 跨度极大，长期未关闭，建议定期评估各子 Issue 的进展。
- **非活跃的增强请求**：Issue `feat(delegation): Advanced Features for Markdown-based Agents` ([#2186](https://github.com/OpenHands/software-agent-sdk/issues/2186))，自 2026-02-23 起处于 `Stale` 状态。虽然已标记为 “Help Wanted”，但近期无新进展。该项目对于扩展 Agent 的协作能力很有价值，若仍为未来路线图考虑，建议定期更新状态，保持社区关注度。
- **等待时间较长的 PR**：`feat: add public from_persisted() entry point to AgentSettingsBase` ([#3503](https://github.com/OpenHands/software-agent-sdk/pull/3503)) 从 2026-06-04 开始，至今仍为 “Open” 状态。这是一个提供公共 API 接口的增强功能，有望简化设置迁移流程，建议维护者评估其合规性与合并计划。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我将根据您提供的 Pi 项目数据，生成一份客观、数据驱动的项目动态日报。

---

### Pi 项目动态日报 | 2026-07-13

#### 1. 今日速览

过去24小时内，Pi 项目的核心维护者展现了极高的修复效率，共关闭了31个 Issue 和9个 PR，重点关注了终端用户界面（TUI）的渲染问题和 OpenAI Codex 新模型（如 GPT-5.6 系列）的兼容性适配。社区活跃度处于中高水平，主要围绕 Codex 模型集成的新增问题以及 TUI 的交互体验缺陷展开讨论。尽管没有新版本发布，但大量合并的修复和功能 PR 表明项目正稳步向更高稳定性和更广的模型支持迈进。

#### 2. 版本发布

**无新版本发布。**

#### 3. 项目进展

今日项目修复与功能推进主要聚焦于终端用户体验优化和特定 Provider 的兼容性修复，核心 Agent 稳定性也有小幅提升。

- **TUI 渲染与交互修复**：这是今天的重点。处理了因终端自动换行引起的界面错位问题 ([PR #6561](https://github.com/earendil-works/pi/pull/6561))，并修复了用户消息中图像块在交互界面不显示的问题，同时优化了剪贴板图片的粘贴流程 ([PR #6572](https://github.com/earendil-works/pi/pull/6572))。阻止了在 Agent 运行中通过 `/tree` 切换分支导致的工具结果错乱问题 ([PR #6559](https://github.com/earendil-works/pi/pull/6559))。
- **Provider 兼容性**：修复了 AWS Bedrock 忽略 `forceAdaptiveThinking` 配置的问题 ([PR #6582](https://github.com/earendil-works/pi/pull/6582))。同时，合并了一个为 Z.AI 平台提供自定义 Provider 支持的功能性 PR ([PR #6565](https://github.com/earendil-works/pi/pull/6565))，并开放了一部分 OpenAI Codex API 供扩展使用 ([PR #6556](https://github.com/earendil-works/pi/pull/6556))。
- **Agent 稳定性**：修复了一个解析工具参数时可能因字符串格式引发的错误，提升了 Agent 工具调用的鲁棒性 ([PR #6577](https://github.com/earendil-works/pi/pull/6577))。
- **待合并亮点**：目前唯一处于开放状态的 PR #6580 引入了 TUI v2 的全屏历史记录查看器，这是一个值得关注的新功能。

#### 4. 社区热点

今日讨论焦点集中在两个领域：一是 GPT-5.6 系列模型的兼容性问题，二是 TUI 的人机交互体验。

- **GPT-5.6 Model 404 错误 (`#6569`)**：用户报告通过 Pi 使用 `gpt-5.6-luna` 时返回 404 错误，但官方 Codex 应用却能正常工作，引发了对 Pi 中 Codex Provider 请求格式的讨论。
  [链接](https://github.com/earendil-works/pi/issues/6569)
- **TUI 图像显示问题 (`#6563`)**：用户发现 TUI 会丢弃用户消息中的图片，导致模型能“看到”图片但用户界面上看不到，破坏了人机对话的上下文一致性。该讨论收到了 4 条评论，热度较高。
  [链接](https://github.com/earendil-works/pi/issues/6563)
- **OpenAI Codex 模型压缩失败 (`#6477`)**：用户反映在 Codex 的 GPT-5.6 模型上压缩失败，社区分析了失败原因是压缩请求中缺失了会话ID。此 Issue 获得了 8 个赞，反映了用户对主流新模型的强烈使用需求。
  [链接](https://github.com/earendil-works/pi/issues/6477)

#### 5. Bug 与稳定性

今日报告的 Bug 主要集中在 TUI 渲染和新模型适配，大部分已有对应的修复 PR。

- **严重 (有修复 PR)**：
    - **[TUI] 用户消息中的图像不显示 (`#6563`)**：模型接收了图片，但对话记录中不显示。**已有修复 PR #6572**。
      [Issue](https://github.com/earendil-works/pi/issues/6563) | [PR](https://github.com/earendil-works/pi/pull/6572)
    - **/tree 切换导致工具结果错乱 (`#6558`)**：在工具运行中切换分支会导致结果挂载到错误分支。**已有修复 PR #6559**。
      [Issue](https://github.com/earendil-works/pi/issues/6558) | [PR](https://github.com/earendil-works/pi/pull/6559)
- **中等 (有修复 PR)**：
    - **OpenAI Codex GPT-5.6 模型返回 404 (`#6569`)**：特定模型因 API 请求格式不匹配导致连接失败。
      [Issue](https://github.com/earendil-works/pi/issues/6569)
    - **TUI 自动换行导致界面错乱 (`#6562`)**：精准匹配终端宽度的行会导致光标追踪错误。**已有修复 PR #6561**。
      [Issue](https://github.com/earendil-works/pi/issues/6562) | [PR](https://github.com/earendil-works/pi/pull/6561)
    - **Bedrock 忽略 `forceAdaptiveThinking` (`#6212`，修复在 #6582)**：针对特定模型的配置项被忽略。
      [PR](https://github.com/earendil-works/pi/pull/6582)
- **低严重度**：
    - **Extension 路径重写错误 (`#6573`)**：扩展加载器错误重写了provider子路径。
      [Issue](https://github.com/earendil-works/pi/issues/6573)
    - **RPC 模式无限挂起 (`#6581`)**：当 Provider 接受请求但不返回 JSON 时，RPC 模式会陷入僵局。
      [Issue](https://github.com/earendil-works/pi/issues/6581)

#### 6. 功能请求与路线图信号

今日的功能请求信号显示出社区对 **扩展性** 和 **Provider 灵活性** 的强烈需求。

- **潜在入线功能**：
    - **支持非 OAuth Token 的自定义 Codex API (`#6564`)**：允许用户为 `openai-codex-responses` provider 设置自定义 `baseUrl` 时使用任意 API Key，这为接入第三方兼容服务打开了大门。社区对此关注度高，有明确的使用场景。
      [链接](https://github.com/earendil-works/pi/issues/6564)
    - **Extension 的延迟重载 API (`#6552`)**：请求增加 `ExtensionContext.requestReload()` 方法，让扩展能够安全地请求运行时重载。这体现了社区在构建复杂扩展时对生命周期管理的需求。
      [链接](https://github.com/earendil-works/pi/issues/6552)
- **路线图信号**：TUI v2 的持续迭代是当前明显的路线图信号，特别是 PR #6580 提出的全屏历史记录查看器，预示着 TUI v2 正从基础渲染走向一个功能更丰富的终端用户界面。
  [PR](https://github.com/earendil-works/pi/pull/6580)

#### 7. 用户反馈摘要

- **对多模态支持的迫切需求**：用户 `@AMagicPear` 在 Issue [#6563](https://github.com/earendil-works/pi/issues/6563) 中指出了 TUI 中图像支持的缺失。这并非一个简单的“能不能用”的问题，而是一个关键的用户体验问题：当模型能理解和引用图片时，用户界面上的不一致会严重破坏信任和协作流畅性。
- **对“零日”模型兼容性的期待**：用户 `@valtterimelkko` 和 `@DmitroGO` 分别遇到了 GPT-5.6 系列模型在 Pi 上的部署问题。这反映出用户期望 Pi 作为顶尖的 AI 代理，能够无缝适配最新的、甚至是刚发布的 AI 模型。配置困难或请求格式不匹配很容易成为用户流失的点。
- **对“非 OpenAI”Provider 生态的焦虑**：用户 `@yuval-shimoni-cyera` 在 Issue [#6324](https://github.com/earendil-works/pi/issues/6324) 中反馈，依赖 AWS Bedrock 等环境凭证的 Provider 在使用 `/tree` 分支摘要时因缺失 API Key 而报错。这表明在支持多元化、自托管 Provider 的同时，需要对不同的认证模式进行更精细的处理，避免功能降级。

#### 8. 待处理积压

- **Agent Session 生命周期 Bug (`#5886`)**：由核心维护者 `@mitsuhiko` 创建的 meta issue，讨论了 Agent 结算、继续和会话生命周期中的一系列 bug。该 Issue 已开放近一个月，拥有 2 个赞和 6 条评论。其复杂性和持续的开着状态暗示这是一个需要大规模重构的难题，对 Agent 的长期稳定性至关重要。
  [链接](https://github.com/earendil-works/pi/issues/5886)
- **Extension API 会话替换 (`#5952`)**：用户 `@llblab` 请求暴露一个安全的 Extension API 用于会话替换。该 Issue 讨论了 Session 的生命周期管理，对构建复杂扩展的用户非常重要。虽然已经被标记为 `[no-action]` 关闭，但其背后的核心诉求(安全的会话管理API)仍是痛点，可能需要重新考虑设计。
  [链接](https://github.com/earendil-works/pi/issues/5952)

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

好的，各位关注 LiteLLM 项目的朋友们，早上好！这里是 2026-07-13 的项目动态日报。

---

### LiteLLM 项目日报 | 2026-07-13

---

### 1. 今日速览

今日项目活跃度极高。过去24小时内，共产生 **32 条 Issue 更新** 和 **118 条 PR 更新**。其中，新开/活跃的 Issue 达 23 条，有 84 个 PR 仍在等待合并，表明社区贡献与项目维护工作量巨大。安全审计与模型适配是今日的焦点，社区提交了多项关于 **SSRF** 和 **Open Redirect** 的安全漏洞报告，同时主流模型（如 **DeepSeek V4**、**Claude Opus 4.7/4.8**、**Gemma 4**）的兼容性问题也被密集反馈。尽管发布节奏较快（3个新版本），但大量待处理的 PR 和高关注度的 Bug 表明，项目当前可能在快速迭代与稳定性之间寻求平衡。

---

### 2. 版本发布

昨日共发布了 **3 个新版本**，全部为 Patch 或 Release Candidate 版本：

- **[v1.93.0-rc.1](https://github.com/BerriAI/litellm/releases/tag/v1.93.0-rc.1)**、**[v1.92.0](https://github.com/BerriAI/litellm/releases/tag/v1.92.0)**、**[v1.91.3](https://github.com/BerriAI/litellm/releases/tag/v1.91.3)**
- **主要说明**：这三个版本的核心说明均为 Docker 镜像签名验证（Cosign）流程文档，内部特性变更等详细内容未在 Release Notes 中展开。生产环境部署的用户建议关注后续完整的 Changelog。
- **注意事项**：有 Issue [#32993](https://github.com/BerriAI/litellm/issues/32993) 报告称 **v1.92.0 版本可能缺少了关键的补丁 #32339**，导致在没有安装 FastAPI 的 SDK 环境中，调用 `completion(..., tools=[...])` 会报 `ModuleNotFoundError`。**建议使用 SDK 而非 Proxy 功能的用户谨慎升级至 v1.92.0，或确保环境完整。**

---

### 3. 项目进展

尽管大多数 PR 仍在等待合并，但昨日仍有关键进展：

- **MCP (Model Context Protocol) 优化**：PR [#29883](https://github.com/BerriAI/litellm/pull/29883) 修复了批量邀请用户时无法自动创建 API Key 的问题，提升了管理界面的可用性。
- **安全与合规**：PR [#33012](https://github.com/BerriAI/litellm/pull/33012) 禁止了请求体中携带 `aws_profile_name` 参数，这是一项应对内部安全审计发现的重要加固措施，防止客户端滥用 AWS Profile 配置。
- **稳定性修复**：多个针对特定模型 Bug 的修复 PR 已提交，包括 Bedrock Converse 的空用户消息处理 ([#33020](https://github.com/BerriAI/litellm/pull/33020))、Fireworks AI 的缓存计费逻辑 ([#33017](https://github.com/BerriAI/litellm/pull/33017)) 等，虽未合并，但表明修复工作已在进行中。
- **CI/CD 改进**：PR [#33011](https://github.com/BerriAI/litellm/pull/33011) 尝试恢复自动化的 PR 分类和审查流程，旨在提高社区 PR 的处理效率。

---

### 4. 社区热点

- **#8842 [Bug] 路由器的异步补全 (acompletion) 不触发自定义日志回调**：此 Issue 虽古老，但讨论热度极高（25条评论，13个👍）。核心用户群体强烈关切 **异步调用下的回调一致性**，这是构建复杂监控和审计系统的关键痛点，长期未解决可能影响用户对系统可靠性的信心。
    - [Issue 链接](https://github.com/BerriAI/litellm/issues/8842)

- **#26395 [Bug] DeepSeek V4 Pro 多轮对话失败**：19条评论，25个👍，是近期最高赞的 Bug。用户在使用热门模型 DeepSeek V4 Pro 进行多轮对话时，从第二轮开始就会因 `reasoning_content` 字段问题导致失败。这表明 **LiteLLM 在处理新兴模型特性（如推理内容）时存在兼容性缺陷**，是当前优先度极高的待解决问题。
    - [Issue 链接](https://github.com/BerriAI/litellm/issues/26395)

- **#33001 与 #33000 [Security] OAuth Open Redirect 与 SSRF 漏洞**：昨日新提交的两个高危/中危安全漏洞，作者均为 `Correctover`。这反映了社区安全研究者对 LiteLLM 的积极审计。SSRF 漏洞（CVSS 7.5）可能被用于攻击内部网络，需要项目组高度重视并快速响应。
    - [Issue 链接 - OAuth](https://github.com/BerriAI/litellm/issues/33001) | [Issue 链接 - SSRF](https://github.com/BerriAI/litellm/issues/33000)

---

### 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 有无修复 PR |
| :--- | :--- | :--- | :--- |
| **高** | [#26395](https://github.com/BerriAI/litellm/issues/26395) | **DeepSeek V4 Pro 多轮对话失败**：热门模型核心功能不可用。 | 有相关PR【如[#32992](https://github.com/BerriAI/litellm/issues/32992)】 |
| **高** | [#32992](https://github.com/BerriAI/litellm/issues/32992) | 通过 LiteLLM 路由 DeepSeek V4 Pro 给 Codex 时出现400错误。 | 无 |
| **中** | [#26444](https://github.com/BerriAI/litellm/issues/26444) | 对 Claude Opus 4.7 仍报告支持 `temperature` 参数，导致请求被拒。 | 无 |
| **中** | [#32993](https://github.com/BerriAI/litellm/issues/32993) | **v1.92.0 发布版本缺少关键补丁**，导致 SDK 中使用 Tools 功能报错。 | 无 |
| **中** | [#25291](https://github.com/BerriAI/litellm/issues/25291) | Gemma 4 模型通过 Google AI Studio 发送视频时被拒。 | 无 |
| **低** | [#33003](https://github.com/BerriAI/litellm/issues/33003) | `get_combined_callback_list` 使用 `set` 去重，破坏了回调的执行顺序。 | 已提交 [#33008](https://github.com/BerriAI/litellm/pull/33008) |

---

### 6. 功能请求与路线图信号

- **Compresr 上下文压缩护栏**：PR [#33019](https://github.com/BerriAI/litellm/pull/33019) 提出了一个名为 `Compresr` 的新型护栏（Guardrail），旨在请求到达模型前压缩臃肿的上下文（如工具输出、RAG 块），以节省 Token。这直接回应了**降低应用成本和优化长上下文性能**的普遍需求，可能成为企业用户接受度高的功能。
- **工具权限护栏日志降噪**：Issue [#32778](https://github.com/BerriAI/litellm/pull/32778) 请求将预期内的工具权限拦截事件从 `WARNING` 级别降级，**减少监控日志噪音**。这反映了运维人员对精细化管理日志的渴求。
- **TTFT 超时检测**：PR [#30337](https://github.com/BerriAI/litellm/pull/30337) 为路由器增加了 `ttft_timeout` (首Token时间) 超时功能。这是**增强代理弹性和预防“挂起”提供者**的重要功能，对于保障生产环境的稳定性有重要意义。

---

### 7. 用户反馈摘要

- **痛点聚焦**：**DeepSeek V4 Pro 的集成问题**是当前用户反馈的最强音，多篇 Issue 指向其多轮对话和工具调用兼容性，严重影响了用户使用该热门模型的体验。
- **环境适配诉求**：用户普遍要求 LiteLLM 能够跟上各大模型厂商的最新变化，例如 Claude Opus 4.7 的 `temperature` 参数弃用、Gemma 4 的视频处理、Ollama 流式工具调用等，但当前版本在这些方面存在滞后。
- **运维复杂性**：多个 Issue 反映了用户在复杂部署环境中的痛点，如 **oauth2-proxy 集成** ([#19856](https://github.com/BerriAI/litellm/issues/19856))、**Prometheus 指标翻倍** ([#19929](https://github.com/BerriAI/litellm/issues/19929)) 等，表明部署和运维的复杂性仍在。

---

### 8. 待处理积压

以下 Issue 和 PR 长期未得到有效响应，可能值得维护团队关注：

- **长期未解决的重大 Bug**：
    - [#8842](https://github.com/BerriAI/litellm/issues/8842): `acompletion` 不触发回调（自2025年2月）。
    - [#26395](https://github.com/BerriAI/litellm/issues/26395): DeepSeek V4 Pro 多轮对话失败（自2026年4月）。
- **积压的社区贡献 PR**：
    - [#25029](https://github.com/BerriAI/litellm/pull/25029)：修复超时分析中的硬编码 provider（自2026年4月）。
    - [#25040](https://github.com/BerriAI/litellm/pull/25040)：隔离并限制重试元数据（自2026年4月）。
    - [#25030](https://github.com/BerriAI/litellm/pull/25030)：修复 Web 搜索 `extra_headers` 传播（自2026年4月）。
- **需要关注的稳定性问题**：
    - [#32996](https://github.com/BerriAI/litellm/issues/32996): OTEL 日志事件因 `NoneType` 被静默丢弃。

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 | 2026-07-13

---

## 📌 今日速览
- 过去24小时内项目活跃度一般，仅出现 **1 个新 Issue** 和 **3 个 PR 更新**，无新版本发布。
- 一个长期待审的 PR (#8821) 终于被关闭合并，修复了空 payload 下 `ContinuedFailure` 未清除的缺陷；另一个自动化 PR (#11023) 完成了 `1.32.0` 发布分支的准备。
- 社区讨论集中在 Nexus 相关功能的完善：一个需澄清错误脱敏范围的 Issue 持续获得关注，一个新的 PR (#11022) 正在为 NexusTask token 添加队列类型字段，以区分内部与用户调用。
- 项目整体健康度良好，短期无显著波动，但长期未解决的 Issue (#10716) 仍提醒维护者关注代码中的 TODO 清理。

---

## 🚀 版本发布
**无**（过去24小时无新 Releases）

---

## 📈 项目进展

### 已合并/关闭的 PR

1. **[#8821] Fix ContinuedFailure not cleared on null success payloads** (已关闭)  
   - **影响范围**：工作流执行引擎  
   - **修复内容**：当工作流以空 `payload` 成功完成时，`ContinuedFailure` 字段未能正确清除，导致后续重试或状态查询异常。该 PR 确保只要 `workflow completed successfully` 都清除该字段，无论 `result` 是否为 `nil`。  
   - **意义**：消除一处隐蔽的状态残留 bug，提升工作流重试与终止判断的鲁棒性。  
   - 链接：https://github.com/temporalio/temporal/pull/8821

2. **[#11023] 1.32.0: Prepare release branch** (已关闭)  
   - **性质**：持续集成/发布流程  
   - **内容**：由机器人自动创建，用于覆盖治理文件并更新依赖，标志 `1.32.0` 版本的发布分支已就绪。  
   - **意义**：表明下一正式版本即将发布，相关功能将进入稳定阶段。  
   - 链接：https://github.com/temporalio/temporal/pull/11023

**总结**：过去24小时项目清理了一个遗留 PR 并完成了新版本的发布分支准备工作，整体进度向前迈出一步，但无重大功能合并。

---

## 🔥 社区热点

### 最活跃 Issue：**#10716** – Clarify scope of "redact certain errors" TODOs in history Nexus handler  
- **背景**：`service/history/handler.go` 中 `StartNexusOperation` 和 `CancelNexusOperation` 的 fallback 路径下有两处 TODO 注释，要求“redact certain errors”。  
- **诉求**：发起者希望明确到底哪些错误需要脱敏、脱敏规则如何实现，以及是否应该现在完成而非仅留 TODO。  
- **讨论热度**：自创建以来已有 2 条评论，最后更新于 2026-07-12（即昨日）。虽无大量回复，但该 Issue 指向核心安全/日志脱敏机制，对生产运维至关重要。  
- 链接：https://github.com/temporalio/temporal/issues/10716

### 待合并 PR：**#11022** – Add task queue kind to NexusTask token  
- **原因**：当前 `RespondNexusTaskCompleted`/`Failed` 中硬编码 `TASK_QUEUE_KIND_NORMAL`，无法区分内部 Nexus 调用与用户调用。该 PR 通过向 token 增加 `TaskQueueKind` 字段，使前端能将正确类型传递给 matching 服务。  
- **关联**：源于 Issue #10141，属于 Nexus 功能与匹配层集成的重要改进。  
- 链接：https://github.com/temporalio/temporal/pull/11022

---

## 🐛 Bug 与稳定性

**无全新 Bug 报告**。  
- 唯一与 Bug 相关的 PR #8821（已合并）属于修复历史回归问题： `ContinuedFailure` 在空 payload 场景下未清除。该问题严重程度中等，可能引起用户误判工作流失败原因，已通过合并解决。

---

## 🧪 功能请求与路线图信号

| 请求/PR | 类型 | 描述 | 可能纳入版本 |
|---------|------|------|-------------|
| #11022 | 功能增强 | 向 NexusTask token 添加 `TaskQueueKind`，区分内部与用户 Nexus 调用 | 可能随 Nexus 功能完整化纳入下一版本（1.32.0 或后续） |
| #10716 | 代码清理/安全 | 明确 Nexus handler 中错误脱敏 TODO 的实现范围 | 尚无 PR 关联，属于长期技术债 |

此外，自动生成的发布分支 PR #11023 暗示 1.32.0 即将发布，预计会包含近期合并的多项改进（如 #8821 的修复及 #11022 如果能在分支合并窗口前完成）。

---

## 💬 用户反馈摘要

**来自 Issue #10716 的评论**：
- 用户 @NasitSony 认为这两个“TODO: redact certain errors”的上下文过于模糊，未说明哪些错误需要脱敏、脱敏策略是什么。在安全审计场景下，直接暴露原始错误可能泄露内部实现细节（如数据库错误、网络错误等）。
- 尚无其他用户明确回应，但该类 TODO 积压容易导致后续疏忽，维护者应尽快制定规范或直接修复。

---

## 🗄 待处理积压

### 长期未响应的 Issue
- **#10716** – 自 2026-06-15 创建，至今已近一个月，仅有 2 条评论，无 assigned 人员，无 PR 关联。维护者应评估是否将其列入 Sprint 或标注为“help wanted”。  
  链接：https://github.com/temporalio/temporal/issues/10716

### 待审核 PR
- **#11022** – 创建于 2026-07-11，目前状态为 OPEN，无评论。由于涉及 proto 变更（NexusTask token），需等待核心维护者 review。建议尽快安排，以免错过 1.32.0 发布窗口。  
  链接：https://github.com/temporalio/temporal/pull/11022

---

*报告生成时间：2026-07-13 UTC | 数据来源：GitHub temporalio/temporal 仓库公开活动*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*