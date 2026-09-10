# AI CLI 工具社区动态日报 2026-09-11

> 生成时间: 2026-09-10 22:36 UTC | 覆盖工具: 7 个

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
数据截止：2026-09-11  
说明：PR 列表中的评论数在给定数据中显示为 `undefined`，因此下文“热门 Skills”按关联 Issue 热度、影响面与时效性综合排序；所列 PR 截至数据均显示为 **OPEN**。

---

## 1. 热门 Skills 排行（PR）

| 排名 | Skill / PR | 功能与讨论热点 | 状态 |
|---|---|---|---|
| 1 | [#1298 skill-creator: run_eval.py always reports 0% recall](https://github.com/anthropics/skills/pull/1298) | 修复 skill-creator 评估链路：`run_eval.py` 长期报告 `recall=0%`，导致描述优化循环在噪声上优化。关联 [#556](https://github.com/anthropics/skills/issues/556)，有 12 条评论、7 👍，并牵出 Windows 流读取、触发检测、并行 worker 等问题。 | OPEN |
| 2 | [#514 Add document-typography skill](https://github.com/anthropics/skills/pull/514) | 为 AI 生成文档做排版质控：孤词换行、寡行段落、标题落底、编号错位等。属于高频文档输出场景的“最后一公里”质量提升。 | OPEN |
| 3 | [#83 Add skill-quality-analyzer and skill-security-analyzer](https://github.com/anthropics/skills/pull/83) | 增加两个元技能：从结构、文档、示例等五维评估 Skill 质量，并做安全分析。与安全信任议题 [#492](https://github.com/anthropics/skills/issues/492) 高度呼应。 | OPEN |
| 4 | [#1367 Add self-audit — mechanical verification + reasoning quality gate](https://github.com/anthropics/skills/pull/1367) | 交付前自审计：先机械验证文件/输出，再做四维推理质量门禁。关联 [#1385](https://github.com/anthropics/skills/issues/1385)，代表社区对“质量门禁流水线”的兴趣。 | OPEN |
| 5 | [#1628 Add Hivemind: Zero-Cost Multi-Agent Orchestration Skill](https://github.com/anthropics/skills/pull/1628) | 让 Claude Code 作为规划/审查/合并者，把机械工作委派给免费模型上的 headless opencode worker。热点是成本优化与多智能体编排。 | OPEN |
| 6 | [#1627 Add buffer-api Agent Skill](https://github.com/anthropics/skills/pull/1627) | 通过 Buffer GraphQL API 管理社交内容排期，面向 Claude、Cursor、Codex 等多 agent 的可移植 Skill。反映 SaaS 集成类 Skill 需求。 | OPEN |
| 7 | [#1742 fix(mcp-builder): support mcp>=2 streamable_http_client](https://github.com/anthropics/skills/pull/1742) | 修复 `mcp-builder` 对 `mcp>=2.0.0` 的兼容性：`streamablehttp_client` 重命名、自定义 header 配置方式变化。关联 MCP 工具链稳定性。 | OPEN |
| 8 | [#1607 Update claude-api skill: mark four retired model IDs](https://github.com/anthropics/skills/pull/1607) | 更新 `claude-api` 技能中的模型退役信息，修复过期模型 ID 仍在“活跃/弃用”分类中的问题。属于官方技能内容维护类热点。 | OPEN |

补充：文档类修复也非常密集，如 [#1734 检测孤立的 docx 评论](https://github.com/anthropics/skills/pull/1734)、[#538 修正 PDF 文件引用大小写](https://github.com/anthropics/skills/pull/538)、[#541 修复 docx tracked change id 冲突](https://github.com/anthropics/skills/pull/541)、[#539 校验 YAML 特殊字符](https://github.com/anthropics/skills/pull/539)。

---

## 2. 社区需求趋势（来自 Issues）

1. **安全、信任边界与命名空间治理**  
   [#492](https://github.com/anthropics/skills/issues/492) 以 43 条评论成为最高热 Issue：社区技能以 `anthropic/` 命名空间分发，可能被误认为官方技能，造成权限授予风险。相关诉求包括技能签名、来源标识、权限透明和官方审核。  
   相关：[#412 agent-governance](https://github.com/anthropics/skills/issues/412)、[#1175 SharePoint 权限与上下文安全](https://github.com/anthropics/skills/issues/1175)。

2. **组织级共享、分发与去重**  
   [#228](https://github.com/anthropics/skills/issues/228) 希望 Claude.ai 支持组织内 Skill 共享库/直链，而不是手动下载 `.skill` 再上传。  
   [#189](https://github.com/anthropics/skills/issues/189) 指出 `document-skills` 与 `example-skills` 内容重复，造成上下文窗口浪费。  
   相关：[#16 将 Skills 暴露为 MCP](https://github.com/anthropics/skills/issues/16)。

3. **skill-creator 与评估工具链可靠性**  
   [#556](https://github.com/anthropics/skills/issues/556) 反馈 `run_eval.py` 下 `claude -p` 从不触发技能，触发率 0%。  
   [#202](https://github.com/anthropics/skills/issues/202) 认为 `skill-creator` 更像开发文档而非可执行技能，token 效率低。  
   趋势：社区需要可复现评测、Windows 兼容、触发检测、描述优化闭环。

4. **上下文窗口与 token 效率**  
   [#1487](https://github.com/anthropics/skills/issues/1487) 指出 `claude-api` 技能单次工具调用急切注入约 156k tokens，几乎耗尽上下文。  
   [#1329](https://github.com/anthropics/skills/issues/1329) 提议 `compact-memory`，用符号化表示压缩 agent 状态。  
   趋势：Skill 需要懒加载、分段加载、token 预算和记忆压缩。

5. **文档/办公自动化与格式兼容**  
   PR 侧集中出现 typography、ODT、PDF、DOCX 评论/修订/编号/大小写问题；Issue 侧也有 SPO 文档处理安全讨论。  
   趋势：社区希望 Skills 能稳定处理 docx、pdf、odt、comments、tracked changes 等真实办公格式。

6. **MCP、API

---

# Claude Code 社区动态日报 · 2026-09-11

> 数据来源：github.com/anthropics/claude-code

---

## 一、今日速览

今日社区最热的焦点是 **Windows 平台 Cowork（协作）功能大面积故障**——#92984 报告在安装 KB5124008 更新后所有 Plan9 共享挂载失败，单条 Issue 已积累 79 条评论与 40 个赞，卸载该 KB 可临时规避。与此同时，**模型质量与计费/配额类问题仍是长期痛点**：Gen 5 模型（Fable 5 / Opus 5 / Sonnet 5）的性能回退报告持续发酵，多条关于配额异常消耗、自动充值误扣的旧 Issue 在今日集中被标记为 `stale` 并关闭。版本侧发布 v2.1.268，主要为网关定价同步与网关配置启动校验。

---

## 二、版本发布

### v2.1.268

- **网关定价同步**：在 `gateway.yaml` 中设置 `pricing:` 后，已登录的 Claude Code 客户端会通过托管设置（managed settings）接收相同费率，使 `/cost` 输出与遥测数据和企业侧花费计量表保持一致，解决了此前成本显示不匹配的问题。
- **网关启动告警**：当 `access_control.allow_cidrs` 为空时将新增启动警告，避免因访问控制未配置导致的隐性暴露风险。

---

## 三、社区热点 Issues（10 项）

**1. [#92984](https://github.com/anthropics/claude-code/issues/92984) — Cowork (Windows)：KB5124008 更新后所有 Plan9 共享挂载失败**
`OPEN` · 79 评论 · 👍40 · 今日最热
Windows 更新 KB5124008（26200.9445）后，所有 Plan9 共享均报 `Plan9 mount failed: invalid argument`，卸载该 KB 即可恢复。这是本期评论数最多、点赞最高的 Issue，说明影响面广且已定位到明确的触发条件（OS 更新与挂载机制的兼容性回归），运维和 Windows 开发者受影响最直接。

**2. [#83510](https://github.com/anthropics/claude-code/issues/83510) — Gen 5 模型可测量的质量回退**
`OPEN` · 13 评论 · 👍21
作者给出可复现的量化数据：胡言乱语检测能力下降、输出冗长度约 2 倍、以及在未充分披露的情况下从 Fable 5 回退到 Opus 4.8。这是模型行为层面最有分量的一份报告，附带测量方法，社区共鸣度高，直接关系付费用户的产出质量预期。

**3. [#47327](https://github.com/anthropics/claude-code/issues/47327) — Cowork 标签页在 Windows 11 Pro 上被判定为 "unsupported"**
`CLOSED (stale)` · 25 评论 · 👍3
自 2026 年 3 月持续至今的平台兼容问题，最终以 stale 关闭而非修复。它和 #92984 一起说明 **Cowork 在 Windows 上的稳定性是长期结构性短板**，而非单次事故。

**4. [#68773](https://github.com/anthropics/claude-code/issues/68773) — 自动充值循环误扣 29 次、共 $661，客服无法升级到人工**
`CLOSED (stale)` · 8 评论
消费级计划用户在 6 月 4–13 日被自动充值连续扣款 29 次，总额 $661.08，而应用内显示的周用量远未接近上限。客服承认故障但无法升级处理。属于**可信度破坏力最强的一类问题**，stale 关闭但无明确修复说明，容易积累用户不信任。

**5. [#80750](https://github.com/anthropics/claude-code/issues/80750) — 计划额度未用尽却消耗额外额度；开启 extra usage 后 5 小时窗口不再启动**
`CLOSED (stale)` · 👍3
揭示了配额逻辑的内部冲突：额外用量开关会阻塞正常计划窗口的计时。属于会直接影响成本与使用节奏的计费语义缺陷。

**6. [#86033](https://github.com/anthropics/claude-code/issues/86033) — 5 小时配额消耗量自 2026-08-08 起跃升约 15–20 倍**
`CLOSED (stale)` · 多实例场景
从"偶发且自愈"变为"持续高消耗"，多实例并行使用时尤为明显。与 #80750 相互印证，说明**配额计量模型在多会话/多实例下可能存在系统性偏差**。

**7. [#86225](https://github.com/anthropics/claude-code/issues/86225) — Claude Code 未经确认将用户个人信息发布到公开 Issue**
`CLOSED (stale)` · `area:tools` `area:security`
在起草公开评论时，Claude Code 把用户 Windows 账户名（来自其先前生成的工作材料）写进了公开发布内容。这不是模型能力问题而是**工具侧的隐私边界缺失**：涉及 `area:tools` 与 `area:security` 双重标签，对任何在企业仓库中使用该工具的人都构成直接风险。

**8. [#85400](https://github.com/anthropics/claude-code/issues/85400) — `--max-budget-usd` 在零 API 成本、额度充足时仍终止 Max 订阅运行**
`CLOSED (stale)`
CLI 在通过 Claude.ai Max 订阅鉴权（无 API 凭证）的情况下，仍以 `Exceeded USD budget (1)` 终止运行。说明**订阅模式与 API 计费模式的预算校验路径没有正确区分**，影响 CI/脚本化调用。

**9. [#85874](https://github.com/anthropics/claude-code/issues/85874) — 代理声明的动作从未执行，且失败静默无提示**
`CLOSED (stale)` · `area:model` `area:agents`
代理明确表示将要派发/运行某个动作，随后并未执行，也没有任何信号暴露。作者特意区分了它与 #85308（把推理当成观测）和 #85092（违反自身规则）——这是**承诺型行为的静默失败**，在编排型长会话中极难排查。

**10. [#86015](https://github.com/anthropics/claude-code/issues/86015) — 后台 Bash 任务运行时，Cron/loop 作业永不触发（仅 stream-json 客户端）**
`CLOSED (stale)` · 含复现 · 👍2
在 VS Code 扩展与桌面 App 上，只要有 harness 跟踪的后台 Bash 任务在跑，`CronCreate` / `/loop` 创建的定时作业就不会投递；同样复现在终端 CLI 下则正常。这是**客户端传输方式相关的调度器缺陷**，对依赖 `/loop` 做自动化的用户是硬阻断。

> 补充关注：安全策略误判类问题今日集中出现——[#86071](https://github.com/anthropics/claude-code/issues/86071)（安全研究请求被拦）、[#86195](https://github.com/anthropics/claude-code/issues/86195)（WiFi RTSP 扫描脚本触发使用政策）、[#86065](https://github.com/anthropics/claude-code/issues/86065)（对自有代码库的防御性审计被重路由离开 Fable 5）。三者共同指向**安全护栏对合法防御性/授权场景的误伤**，是安全从业者群体的高频抱怨点。

---

## 四、重要 PR 进展

> 说明：过去 24 小时内仓库仅有 **3 条 PR** 有更新（2 条 OPEN、1 条 CLOSED），无法凑足 10 条。以下为全部条目，并补充观察。

**1. [#93452](https://github.com/anthropics/claude-code/pull/93452) — `mods/diff`：对齐内置 `/diff` 面板**
`OPEN` · @poteat
让 `/diff` 扩展模块的面板与内置 diff 面板视觉与行为一致：hunk 通过引擎的 code element 渲染、采用内置的关闭 ✕、统一行距与空状态位置、窄终端下的重绘提示线，并确保同一时刻只进行一个仓库探测。属于**插件 API 成熟度提升**的典型工作——第三方模块开始向官方 UI 标准收敛。

**2. [#93244](https://github.com/anthropics/claude-code/pull/93244) — `mods`：API 重命名、遥测修复与 diff 后端接缝**
`CLOSED` · @poteat
跟进插件 API 的命名整理（`isFocused`、`tool`），收紧遥测行为（逐行上报、每行独立读取分析开关、任何第三方 provider 一律不上报），并为 diff 模块引入后端接缝，以 git 作为内置后端，为其他版本控制系统留出扩展位。对**插件生态的可扩展性与数据合规**都有直接价值。

**3. [#89404](https://github.com/anthropics/claude-code/pull/89404) — `validate-agent.sh`：不再在首个警告处中止，并停止误报合法 agent**
`OPEN` · @bcherny
修复公开 Issue #83803。`plugin-dev` skill 的校验脚本在自身 agent 文件上就会失败，三个根因均与 `set -euo pipefail` 的交互有关：其一，`((warning_count++))` 在计数为 0 时算术表达式返回非零，导致脚本在第一处警告即中止；其二，会错误标记合法 agent。这是**开发者工具链自身的可靠性修复**。

**观察**：本期 PR 数量偏少，且作者高度集中（poteat 两条、bcherny 一条），与当日 50 条 Issue 更新的流量形成鲜明对比——社区能量主要集中在问题反馈而非代码贡献，插件/模块 API 是最活跃的贡献方向。

---

## 五、功能需求趋势

综合本期全部 Issues，社区关注方向可归纳为六类：

| 方向 | 代表性 Issue | 说明 |
|---|---|---|
| **Windows 平台稳定性** | #92984、#47327 | 问题密度最高、讨论最热，涵盖 Cowork 挂载、标签页兼容、剪贴板、deep link、taskkill 闪窗等 |
| **计费与配额透明化** | #68773、#80750、#86033、#85400 | 用户要求成本可解释：额外用量与计划窗口的关系、订阅与 API 预算校验的区分、多实例计量准确性 |
| **模型质量与回退披露** | #83510、#85874 | 要求可量化的质量保证，以及模型降级/切换的显式告知 |
| **安全策略误伤** | #86071、#86195、#86065 | 防御性安全审计、授权渗透测试、自有资产扫描被护栏阻断 |
| **Agent 编排可靠性** | #85874、#86015、#86070 | 承诺动作静默丢失、定时任务不触发、teammate 系统提示自相矛盾 |
| **插件/模块生态** | PR #93452、#93244 | 插件 API 命名规范、遥测合规、后端可插拔 |

---

## 六、开发者关注点

1. **平台一致性缺口明显**：Windows 相关问题占据了今日讨论的绝对头部，且不乏持续数月（#47327 自 3 月起）最后以 `stale` 关闭而非修复的案例。开发者对"长期挂起后被自动关闭"的处理方式表达出明显不满。
2. **计费黑箱感强**：从 $661 误扣款到 15–20 倍配额消耗，再到订阅模式下 `--max-budget-usd` 误拦截，多个独立报告指向同一诉求——**用户需要能自行验证的计量口径**，当前 `/cost` 与实际扣费之间的信任已经受损。v2.1.268 的网关定价同步正是朝这个方向的补救。
3. **静默失败是最难排查的痛**：无论是代理宣称执行未执行（#85874）、Cron 作业不投递（#86015），还是 teammate 结果丢失（#86070），共同特征是**无错误、无日志、无提示**。开发者反复强调"缺少可观测性"比"功能缺失"更难接受。
4. **安全护栏与安全从业者的冲突**：三期内的多条报告显示，CVP 认证组织、对自有代码库的防御性审计、授权范围内的网络设备发现，均可能被策略拦截或被重路由到能力较弱的模型。这类用户恰恰是最深度、最忠诚的使用者。
5. **`stale` 自动关闭正在消耗社区信任**：今日展示的 30 条 Issue 中，绝大多数为 `CLOSED` + `stale`，其中包含 #68773 这类涉及实际金钱损失、且客服承认故障的问题。缺乏修复说明的批量关闭，容易让报告者认为反馈渠道失效。
6. **插件生态是当前最健康的贡献面**：在整体 PR 稀薄的情况下，mods/diff 与 plugin-dev 工具链的改进仍在持续推进，且已经出现"向内置功能对齐 UI 标准"和"为第三方后端留接缝"这类架构级动作，值得关注后续插件 API 的正式稳定化。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 · 2026-09-11

> 数据来源：github.com/openai/codex ｜ 统计窗口：过去 24 小时

---

## 1. 今日速览

- **配额（rate limit）异常成为今日绝对焦点**：多个 Pro/Max 用户报告额度在一夜之间从 73%／45% 直接归零，单条 Issue 已累积 26 条评论、16 个 👍，是当前社区情绪最集中的问题。
- **Python SDK 0.154.0 发布**，新增 `max` / `ultra` 两档 reasoning effort 取值；同时 Rust 侧进入 0.155.0 alpha 周期。
- **TUI 体验类需求持续升温**：隐藏工具调用输出（34 👍）、关闭 Astra「星光」动画（whimsy）、Calm 模式等多条 Issue 同时活跃，显示用户对"视觉噪声"的容忍度正在下降。

---

## 2. 版本发布

**python-v0.154.0**（Python SDK）
- 安装：`pip install --upgrade openai-codex==0.154.0`（需 Python 3.10+），配套运行时 `openai-codex-cli-bin==0.154.0`。
- 新增 `max` 与 `ultra` 两个 reasoning-effort 档位（[#39662](https://github.com/openai/codex/pull/39662)）——与社区中出现的 `gpt-6-astra ultra fast` 模型标识相呼应，说明"更高推理强度"正在成为正式能力。
- 同步 API 新增 `ExternalMessage` 类型。

**rust-v0.155.0-alpha.1 / alpha.2**
- 仅发布版本号，changelog 未附具体内容，属于常态 alpha 迭代。

**voice-cygwin-108b38cf67cbb731**（非用户包）
- 面向 native Windows voice 发布的 CI 专用构建产物：103 个固定版本 Cygwin 二进制包 + 83 个对应源码归档 + 离线安装器签名索引。
- 官方明确说明：**不包含在 Codex 用户包中**，仅用于可复现的离线构建。

---

## 3. 社区热点 Issues（精选 10 条）

| # | Issue | 关注理由 | 社区反应 |
|---|---|---|---|
| 1 | [#44199](https://github.com/openai/codex/issues/44199) **Usage went from ~73% to 0% instantly（$200/mo Pro 计划）** | 额度凭空清零，直接触及计费与配额可信度。App 版本 26.901.51231、Pro x20 | 26 评论 · 16 👍（今日最热） |
| 2 | [#42765](https://github.com/openai/codex/issues/42765) **Weekly limit 从 ~45% 掉到 0%，期间未运行任何会话** | 与 #44199 互相印证，说明并非个例，且已提供 CEST 时间线证据 | 12 评论 · 1 👍 |
| 3 | [#44382](https://github.com/openai/codex/issues/44382) **反复出现 "Selected model is at capacity"，Codex 不可用** | Pro 20x 用户在 v0.154.0 + `gpt-6-astra ultra fast` 上被容量错误阻塞，属于可用性级别故障 | 11 评论 · 5 👍 |
| 4 | [#18396](https://github.com/openai/codex/issues/18396) **TUI 增加隐藏工具调用/输出的能力** | 长期未满足的高赞需求：每条命令后终端被工具输出刷屏，影响阅读与专注 | 13 评论 · **34 👍** |
| 5 | [#34349](https://github.com/openai/codex/issues/34349) **允许完全禁用 Pets 并从侧边栏移除入口** | 今日 👍 最高的需求（43），反映用户对非核心装饰性功能的抵触 | 9 评论 · **43 👍** |
| 6 | [#41535](https://github.com/openai/codex/issues/41535) **[Windows] 桌面宠物变点击穿透、无法拖动** | 与 #34349 形成对照：既有人想关掉，也有人因它被破坏而困扰，Windows 桌面宠物实现稳定性存疑 | 10 评论 · 8 👍 |
| 7 | [#22705](https://github.com/openai/codex/issues/22705) **iOS 移动端 thread 打开后消息水合失败（CodexClientError error 11）** | 跨端（Mac 桌面 + iOS）会话同步链路问题，且涉及本地存在多版本 CLI 的复杂环境 | 7 评论 · 8 👍 |
| 8 | [#44609](https://github.com/openai/codex/issues/44609) **rollout writer 序号复用导致 durable history 投影永久卡死** | 高质量技术报告：`thread_settings_applied` 紧跟非持久化 `token_count` 时复用相同 ordinal，触发投影器停滞 | 4 评论 · 0 👍（技术价值高） |
| 9 | [#43855](https://github.com/openai/codex/issues/43855) **Codex 在上下文压缩（compaction）后停止工作** | 长会话核心路径的可靠性问题，Windows + gpt-6-astra 复现 | 5 评论 · 1 👍 |
| 10 | [#44477](https://github.com/openai/codex/issues/44477) **`gpt-5.5` 在 Codex 后端路由返回 404，但同账号在 ChatGPT App 可用** | 典型的模型路由/后端一致性缺陷，Max $200 用户可复现，指向 Codex 后端与主产品的能力不对齐 | 4 评论 · 1 👍 |

**其他值得留意的活跃条目**：`#44599`（macOS/iPhone 同一任务显示不同 active turn，app-server 状态去同步）、`#44612`（更新后 WSL 反复重启、Codex 无法使用）、`#44140`（Windows 更新后 Chrome/Edge 控制报请求头策略错误）、`#44398`（kitty 下 Astra 星光动画阻挡鼠标选中文本）、`#44561`（请求默认关闭 whimsy 特效）、`#7953`（MCP 工具选择/过滤/分组，已 CLOSED）。

---

## 4. 重要 PR 进展（精选 10 条）

> 说明：本批次 PR 均为 `CLOSED` 状态、作者为 `copyberry[bot]`，且未附评论数据，应视为 09-10 集中批量关闭/合并的一批内部提交。

1. [#44661](https://github.com/openai/codex/pull/44661) **追踪工具调用接收、结果就绪与 code-mode 派发**
   拆分 trace 里程碑，暴露"工具结果早于采样循环收集"以及 code-mode cell 跨 turn 存活的时序问题，并把嵌套调用关联回派发它的 turn——对 agent 可观测性意义重大。
2. [#44659](https://github.com/openai/codex/pull/44659) **在委派 agent 工作中保留 turn trigger**
   将 `turn_trigger` 沿 agent 派生与后续消息链路传播，确保多 agent 委派场景下的用量归因仍能追溯到发起 turn（composer 输入 / 定时自动化）。
3. [#44658](https://github.com/openai/codex/pull/44658) **让 Windows 沙箱私有桌面在 helper 退出后存活**
   短生命周期沙箱 wrapper 退出会带走私有桌面，导致跨文件系统 helper 请求无法复用；改为在调用进程中选择并缓存私有桌面。
4. [#44656](https://github.com/openai/codex/pull/44656) **将 turn 指标归因到该 turn 实际使用的模型**
   修复模型切换后遥测被错标的问题；同时支持一个 turn 内包含 compaction 与多模型响应的情况。
5. [#44655](https://github.com/openai/codex/pull/44655) **在运行时能力层面遵循 thread 级 plugin 排除**
   将 `disabled_plugin_ids` 应用到 plugin skills、推荐、hooks 与 MCP servers，且不污染共享插件状态；选择变更在下一个任务开始时生效。
6. [#44650](https://github.com/openai/codex/pull/44650) **强制受管（managed）模型 provider 的选择与定义**
   在 managed requirements 中支持 `model_provider` / `model_providers`，强制选择覆盖本地与会话配置——面向企业集中管控的关键能力。
7. [#44639](https://github.com/openai/codex/pull/44639) **为 Windows 离线沙箱阻断非 loopback 入站流量**
   此前离线沙箱防火墙仅覆盖出站，补齐入站规则，缩小离线用户侧攻击面。
8. [#44636](https://github.com/openai/codex/pull/44636) **通过 OIDC 从 503 响应中恢复 OAuth 元数据发现**
   当 issuer 的 OAuth 元数据端点返回 503 时，回退到同一 issuer 的 OIDC 元数据，避免 MCP 启动时过期 OAuth token 无法刷新。
9. [#44629](https://github.com/openai/codex/pull/44629) **MCP OAuth 登录支持手工回调输入**
   新增 `codex mcp login <name> --no-browser`，允许粘贴完整回调 URL，解决浏览器无法访问回调页时的授权阻塞。
10. [#44622](https://github.com/openai/codex/pull/44622) **新增 `/voice settings` 选择后续会话语音**
    TUI 此前没有语音选择器，realtime 启动请求也不带

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报（2026-09-11）

---

## 一、今日速览

今日社区焦点集中在**安全加固**与**Agent 可靠性**两条主线：一方面，a2a-server 被发现 HTTP API 完全不校验鉴权且使用硬编码凭据（#29001），推动多个沙箱/路径穿越/提示注入修复 PR 集中涌现；另一方面，子代理 MAX_TURNS 被误报为成功（#22323）、generalist agent 永久挂起（#21409）等 P1 缺陷持续占据讨论热度。此外，nightly 版本正常迭代至 `v0.61.0-nightly.20260910`。

---

## 二、版本发布

**v0.61.0-nightly.20260910.ged2ac40df**
- 由自动化机器人发布的每日 nightly 构建（对应 PR #29268 版本号提升）。
- 与前一 nightly 的完整变更对比：https://github.com/google-gemini/gemini-cli/compare/v0.61.0-nightly.20260909.ged2ac40df...v0.61.0-nightly.20260910.ged2ac40df
- 说明：过去 24 小时内**无稳定版发布**，正式功能进展主要体现在 PR 队列中。

---

## 三、社区热点 Issues（10 个）

1. **[P1] 子代理 MAX_TURNS 中断被误报为 GOAL 成功** — #22323（13 条评论）
   `codebase_investigator` 在达到最大轮次限制、尚未完成任何分析时，仍返回 `status: "success"` 与 `Termination Reason: "GOAL"`，掩盖了中断事实。这是今日讨论量最高的问题，直接关系到用户能否信任 agent 的执行结果。
   https://github.com/google-gemini/gemini-cli/issues/22323

2. **[P1] Generalist Agent 永久挂起** — #21409（8 条评论，👍8）
   一旦 CLI 移交 generalist agent 就会无限阻塞（如创建文件夹这类简单操作，等待一小时也不返回）；禁用子代理可绕开。高 👍 数说明影响面广，是当前最影响可用性的问题之一。
   https://github.com/google-gemini/gemini-cli/issues/21409

3. **[P2] 零依赖 OS 沙箱 + 执行后意图路由** — #19873（9 条评论）
   提议充分利用 Gemini 3 原生 bash 亲和力（grep/sed/awk 链式探索代码库），同时通过沙箱保障安全与 UX。这是一条带有战略性的架构提案。
   https://github.com/google-gemini/gemini-cli/issues/19873

4. **[P2][安全] a2a-server HTTP API 从不鉴权，且仅比对硬编码凭据** — #29001
   npm 包 `@google/gemini-cli-a2a-server` 对外宣称 bearer/basic 安全方案，实际所有端点不校验鉴权，且唯一校验逻辑与 `'valid-token'`、`'admin:password'` 硬编码值比对。属于严重安全披露，值得优先跟进。
   https://github.com/google-gemini/gemini-cli/issues/29001

5. **[P1] Shell 命令执行完成后卡在 "Waiting input"** — #25166（👍3）
   简单 CLI 命令已执行完毕，界面仍显示命令活跃并等待用户输入。这是长期存在的交互状态机缺陷，会持续吞掉用户会话。
   https://github.com/google-gemini/gemini-cli/issues/25166

6. **[P2] Gemini 主动使用 skills 与子代理的频率过低** — #21968
   用户反馈：除非显式指令，模型几乎不会自主调用自定义 skill 或子代理，即使任务高度相关。这削弱了 agent 体系的设计价值。
   https://github.com/google-gemini/gemini-cli/issues/21968

7. **[P2] AST 感知的文件读取、搜索与代码库映射评估（EPIC）** — #22745（7 条评论）
   探讨以 AST 感知工具精确读取方法边界、减少错位读取与 token 噪音，并提升代码库导航能力。配套子任务 #22746 建议从 tilth / glyph 入手。
   https://github.com/google-gemini/gemini-cli/issues/22745

8. **[P2][安全] Auto Memory 需要确定性脱敏并减少日志** — #26525
   本地 transcript 在被脱敏前就已进入模型上下文；服务端还会记录已有 skill 内容。涉及隐私与合规，属于 Auto Memory 系列问题的核心。
   https://github.com/google-gemini/gemini-cli/issues/26525

9. **[P2] 工具数量超过 128 个时触发 400 错误** — #24246
   当可用工具过多时请求直接失败，用户期望 agent 能更智能地裁剪工具范围。随着 MCP 生态扩张，该问题会愈发普遍。
   https://github.com/google-gemini/gemini-cli/issues/24246

10. **[P1] 会话中途 401 UNAUTHENTICATED（ACCESS_TOKEN_TYPE_UNSUPPORTED）** — #29275（今日新建）
    原本运行正常的会话突然报 401，而 API Key 经其他脚本验证正常。与今日 OAuth 凭据持久化 PR #29282 可能同源，属于今日新增的高优先级反馈。
    https://github.com/google-gemini/gemini-cli/issues/29275

> 其他值得留意：#22672（agent 应避免 `git reset`/`--force` 等破坏性操作）、#21335（`/compress` 结果不落盘，恢复会话后失效）、#21983（Wayland 下 browser 子代理失败）、#23571（模型在随机目录留下临时脚本）。

---

## 四、重要 PR 进展（10 个）

1. **#29282 fix(auth): 登录后立即持久化 OAuth 凭据**（OPEN）
   此前初始 OAuth 凭据只在客户端 `tokens` 流程中落盘，导致 CLI 重复要求 Google 登录；该 PR 在浏览器/用户码登录成功后立即写入，有望缓解今日 #29275 这类会话中途鉴权失败。
   https://github.com/google-gemini/gemini-cli/pull/29282

2. **#29214 fix(sandbox): 强化文件系统边界并隔离运行时状态**（OPEN，size/l+）
   将沙箱运行时状态与宿主配置目录隔离，用净化后的配置文件替代宿主目录挂载，并在路径敏感性检查中统一使用 realpath（含不存在路径的回退处理）。
   https://github.com/google-gemini/gemini-cli/pull/29214

3. **#29250 fix(core): 阻断通过构建文件修改与不可信参数的间接提示注入**（OPEN，size/xl）
   在受限工作区模式下强化边界校验，重点覆盖构建配置文件与外部命令参数，并重构 `shell`/`edit`/`write_file` 等内置执行路径。
   https://github.com/google-gemini/gemini-cli/pull/29250

4. **#29249 fix(core): 修复 get_internal_docs 路径守卫的同级前缀绕过**（OPEN，P1）
   原实现使用字符串前缀比较且无路径分量边界，任何以 docs 目录名开头的同级目录都会被读取并把内容返回给模型。属典型目录穿越类漏洞。
   https://github.com/google-gemini/gemini-cli/pull/29249

5. **#29116 fix(core): 缓解 NTFS 8.3 短文件名（SFN）路径问题**（CLOSED）
   针对 Windows 短名（如 `git~1`、`vscode~1`）在路径归一化与 AllowedPathChecker 中的绕过进行加固，关闭了 NTFS 下的路径穿越与黑名单规避通道。
   https://github.com/google-gemini/gemini-cli/pull/29116

6. **#29134 fix(cli): 保护当前会话不被删除**（OPEN，P2，修复 #29133）
   在 `--list-sessions` / `--delete-session` 流程中传递活动会话 ID，仅按文件名短 ID 后缀匹配，避免误删正在使用的会话，并补充回归测试。
   https://github.com/google-gemini/gemini-cli/pull/29134

7. **#29200 fix(core): 运行时一致地执行 MCP 策略**（OPEN，P2）
   对齐 MCP 运行时策略与 CLI 的大小写不敏感/去空格匹配规则；将显式空的 `mcp.allowed` 列表视为 fail-closed，而非放开所有服务器；区分"未配置白名单"与"显式空白名单"。
   https://github.com/google-gemini/gemini-cli/pull/29200

8. **#29278 / #29277 fix(core): expandEnvVars 哨兵键与调用方环境变量冲突**（OPEN，P2）
   两个独立提交修复同一缺陷：当调用方环境恰好含有 `__GCLI_EXPAND_TARGET__` 时，函数会返回该值而不展开输入。修复方式是选用不冲突的临时键。
   https://github.com/google-gemini/gemini-cli/pull/29278 ｜ https://github.com/google-gemini/gemini-cli/pull/29277

9. **#29094 / #29095 依赖安全升级：simple-git 3.28.0→3.32.3、shell-quote 1.8.3→1.8.4**（CLOSED）
   分别修复 CVE-2026-28292 与 CVE-2026-9277，两者均被 trivy 标记为 CRITICAL。
   https://github.com/google-gemini/gemini-cli/pull/29094 ｜ https://github.com/google-gemini/gemini-cli/pull/29095

10. **#29098 fix(cli): 保持 useInputHistoryStore 状态更新函数纯净**（CLOSED，P1/P2）
    原实现把 `setPastSessionMessages()` 与带副作用的 `recalculateHistory()` 放在 state updater 内部，React 严格模式下会重复调用，导致历史记录异常。
    https://github.com/google-gemini/gemini-cli/pull/29098

> 附注：#29268 为 nightly 版本号自动提升；#29271、#29272、#29274 等 PR 标题为 "refactor: simplify project structure"、"SECURITY.md"、"NB-gemini"，内容与摘要几乎为空但标记 P1，质量存疑，建议维护者谨慎处理。

---

## 五、功能需求趋势

1. **Agent 编排与自主体能力**：如何让模型**主动**使用 skill / 子代理（#21968）、子代理执行状态可信（#22323）、子代理轨迹可查看与分享（#22598、#21763）、以及避免 destructive 操作（#22672）。
2. **安全与沙箱化**：本轮最密集的方向——OS 级沙箱（#19873）、提示注入防护（#29250）、路径穿越与短文件名绕过（#29249、#29116）、MCP 策略统一（#29200）、a2a-server 鉴权（#29001）。
3. **Memory / Auto Memory 质量与隐私**：脱敏时点（#26525）、低信号会话反复重试（#26522）、非法补丁静默丢弃（#26523）、整体质量跟踪（#26516）。
4. **代码理解能力升级**：AST 感知的读取/搜索/代码库映射（#22745、#22746），目标是降低轮次浪费与 token 噪音。
5. **工具规模治理**：工具数量上限导致 400（#24246），随 MCP 生态膨胀，工具裁剪与作用域管理将成为刚需。
6. **终端体验与跨平台**：resize 闪烁与性能（#21924）、`\n` 转义行为错误（#22466）、Wayland 下浏览器子代理（#21983）、NTFS 路径（#29116）。
7. **会话与状态持久化**：`/compress` 不落盘（#21335）、会话删除保护（#29134）、OAuth 凭据持久化（#29282）。

---

## 六、开发者关注点

- **"卡住"是最高频的挫败来源**：generalist agent 无限挂起（#21409）、shell 命令完成后仍显示等待输入（#25166）、vite 交互式提示卡死（#22465）。三者的共性是没有可靠的超时/状态收敛机制。
- **状态与结果不可信**：达到 MAX_TURNS 却报 GOAL 成功（#22323）、browser 子代理在 Wayland 报 GOAL 但实际失败（#21983）。开发者需要的是**可区分"失败/中断/成功"**的明确语义，而非统一绿灯。
- **鉴权链路脆弱**：会话中途 401（#29275）+ OAuth 凭据未及时持久化（#29282），说明凭据生命周期管理仍是薄弱环节。
- **安全默认值不足**：a2a-server 硬编码凭据、沙箱边界、路径守卫绕过等集中爆发，社区期望"安全是默认而非可选"。
- **子代理被"雪藏"**：skill 与子代理很难被自主触发（#21968），叠加 MAX_TURNS 恢复问题，使多代理架构的收益难以兑现。
- **工作区污染**：模型在随机目录生成临时脚本（#23571），影响干净

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-09-11

## 1. 今日速览
- `v1.0.84-4` 发布，插件、指令与 LSP 相关命令进一步拆分，并增加 JSON 输出与插件启用/禁用能力。
- 社区侧 OOM/内存泄漏、MCP 认证与生命周期兼容性、Windows 插件更新权限成为今日高热度问题。
- 高票 Vim 输入模式 Issue 已关闭；桌面应用多会话、组织级 Agent、会话恢复与资源泄漏仍待解决。

## 2. 版本发布
**v1.0.84-4**  
- 新增 `copilot instruction list` 和 `copilot lsp list`，替代 `copilot plugins list --kind instruction` 与 `--kind lsp`。  
- 为 `copilot plugin list`、`copilot plugin marketplace list`、`copilot plugin marketplace browse` 增加 `--json`。  
- 为 `copilot plugin` 增加 `enable` 和 `disable`。  
- 链接：[GitHub Copilot CLI Releases](https://github.com/github/copilot-cli/releases)

## 3. 社区热点 Issues（挑选 10 个）
1. **[CLOSED] #13 CLI input should have a vi/vim input mode**  
   12 评论、76 👍。高票输入体验需求已关闭，社区长期关注 CLI 内是否支持 Vim 模态编辑。  
   https://github.com/github/copilot-cli/issues/13

2. **[OPEN] #4742 Desktop app 1.1.15: cannot create a second Local session while one is running**  
   11 评论、5 👍。桌面应用会话管理回归：同一项目已有活跃 Local 会话时无法新建第二个分支会话，影响并行开发。  
   https://github.com/github/copilot-cli/issues/4742

3. **[OPEN] #1285 Organisation level Agent not showing up**  
   9 评论、11 👍。组织级 `.github-private` 中定义的 Agent 未在 CLI/VS Code 中显示，影响企业级 Agent 推广。  
   https://github.com/github/copilot-cli/issues/1285

4. **[OPEN] #4095 Windows: plugin update fails with "Access is denied (os error 5)" while VS Code is running**  
   3 评论、21 👍。高赞 Windows 插件更新失败问题，疑似 VS Code Copilot 扩展持有已安装插件句柄。  
   https://github.com/github/copilot-cli/issues/4095

5. **[OPEN] #4686 Node.js OOM crash after ~37 min — 31,965 leaked async libuv handles**  
   严重稳定性问题：SEA 忽略 `NODE_OPTIONS`，长会话泄漏大量 libuv handle 后堆内存耗尽。  
   https://github.com/github/copilot-cli/issues/4686

6. **[OPEN

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报
**日期：2026-09-11** ｜ 数据源：github.com/MoonshotAI/kimi-cli

---

## 1. 今日速览

过去 24 小时社区数据处于低位：**无新版本发布、无 PR 更新**，仅 1 条 Issue 产生活动。唯一动态是一条认证链路的阻塞性缺陷——`/login` 设备码授权在浏览器端批准成功后，CLI 侧仍收到 HTTP 500（#2638），且该问题在 VS Code 扩展中同样可复现，指向共享的认证后端而非单一客户端。总体而言，今天是"低噪声、单点高优先级"的一天。

---

## 2. 版本发布

过去 24 小时内无新 Release。当前社区反馈所基于的最新版本为 **CLI v0.42.0**。

---

## 3. 社区热点 Issues

> 说明：过去 24 小时内更新的 Issue 共 **1 条**，不足 10 条筛选基数，以下为全量呈现，不做凑数扩展。

### #2638 [OPEN] `/login` 设备授权在浏览器批准成功后返回 HTTP 500
- **链接**：https://github.com/MoonshotAI/kimi-cli/issues/2638
- **作者**：@milesbuckton ｜ **创建**：2026-09-09 ｜ **更新**：2026-09-10 ｜ **评论**：1 ｜ **👍**：0

**为什么重要**

1. **命中认证主路径，属阻塞级缺陷**。设备码（Device Code）授权是 CLI 首次使用与令牌过期后的必经入口。一旦该流程在"浏览器已批准"之后失败，用户处于**无法通过任何自助手段进入产品**的状态，影响面覆盖全部新用户与需要重新登录的老用户。
2. **跨客户端复现，指向服务端**。报告者明确指出问题同样在 **VS Code 扩展**中复现。这基本排除了 CLI 单一端的本地实现问题，更可能是设备码轮询/换取令牌的**后端接口**或共享认证 SDK 出现异常——对 MoonshotAI 而言，这比单端 bug 的修复优先级更高。
3. **HTTP 500 而非 4xx，属于非预期失败**。500 意味着服务端未按业务语义处理该请求（例如未正确返回"授权待完成/已过期"的明确状态），这既影响用户可诊断性，也提示服务端缺少针对设备码状态的健壮分支处理。
4. **报告质量高，便于定位**。Issue 中提供了版本、OS、账户层级（free plan / Adagio tier）、完整复现步骤，并给出了实际设备码样例（`WGBT-C3BW`、`QLE2-MYVL`），对复现与关联服务端日志有直接价值。

**社区反应**

目前仅 1 条评论、0 个 👍，讨论热度低。考虑到该 Issue 创建于 09-09、09-10 有更新，且尚未标记为已修复，**属于"低热度但高严重度"类型**——这类问题通常热度增长滞后（用户卡在登录页时未必会来提 Issue），建议维护方主动介入而非等待 👍 累积。

**当前状态**：OPEN，未观察到修复版本。

---

## 4. 重要 PR 进展

过去 24 小时内**无 PR 更新**（新增、合并、评论均无），本期无可汇总内容。

值得留意的是，Issue #2638 目前尚无与之关联的修复 PR，认证主路径的修复进度处于"已报告、未动工"阶段。

---

## 5. 功能需求趋势

受限于本期样本量（1 条 Issue，且为缺陷报告而非功能需求），**无法从数据中提炼出具备统计意义的需求趋势**。为避免误导，此处不做趋势推断。

仅从该单条数据可观察到的方向性信号：

- **认证与身份体系的稳定性**仍是社区最底层的关注点。CLI 与 IDE 扩展共用认证链路，意味着任何认证侧回归都会同时冲击两条产品线。
- **多端一致性（CLI ↔ VS Code 扩展）**：报告者自发跨端验证，反映用户已把 Kimi 的 CLI 与 IDE 插件视为同一套工具的两种入口，对两端行为一致性的期望较高。

后续如需形成趋势判断，建议累积至少 15–20 条 Issue 样本后再做归纳。

---

## 6. 开发者关注点

基于本期唯一有效样本，开发者反馈的核心痛点可归纳为：

1. **登录即被阻断，且缺乏可自救路径**。`/login` 是工具链的第一道门，此处返回 500 会让用户既无法使用产品，也拿不到可操作的错误信息（不知道是重试、清缓存还是等待服务恢复）。
2. **服务端错误语义不清晰**。设备码流程中，"用户已批准但客户端轮询仍失败"这一状态本应被明确区分（如返回待处理、超时或授权冲突），而非统一落到 500。建议在错误响应中附带可追踪的 request-id，便于用户提 Issue 时直接关联服务端日志。
3. **免费层级用户同样受影响且易被忽视**。报告者使用 free plan（Adagio tier），这类用户在反馈链路上的声音通常更弱，但其基数可能更大，认证故障对其是 100% 的阻断。
4. **跨端问题缺少统一的故障通报渠道**。CLI 与 VS Code 扩展同时故障时，用户难以判断是本地环境问题还是服务端故障，建议补充状态页或客户端内的服务健康提示。

**建议跟进动作**：优先复现 #2638 并确认是否与 09-09 前后的认证服务变更相关；若确认为服务端问题，建议在 Issue 中公开说明影响范围与临时绕过方案（如 Token 缓存复用或备用登录方式）。

---

*本期数据量偏少，日报以如实呈现为主，未对 10 条 Issue / 10 条 PR 的选取要求做补充填充。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报（2026-09-11）

## 1. 今日速览

今日无新版本发布。社区讨论高度集中在 **2.0 数据库事件表无界增长**（单实例达 13GB+）与 **subagent 无限循环燃烧 token** 两大严重问题上。支付/订阅失败、免费模型额度限制、TUI/桌面端功能需求（垂直标签、Token 用量显示）持续发酵。PR 方面，TUI 递归分组树、GenAI 可观测性追踪、可配置标签位置等改进值得关注。

---

## 2. 版本发布

过去 24 小时无新 Releases。

---

## 3. 社区热点 Issues（精选 10 条）

### ① 免费模型 "free usage exceed" 引发大量讨论
- **#15585 [CLOSED]** | 评论 55 | 👍 17
- 用户使用免费模型 Big Pickle 进行两个大型会话（约 6 小时）后触发 “free usage exceed”。社区对免费额度限制的透明度和合理性提出质疑。
- 🔗 https://github.com/anomalyco/opencode/issues/15585

### ② 2.0 事件表无界增长，数据库达 13GB+
- **#33356 [OPEN]** | 评论 30 | 👍 9
- `opencode.db` 中 `event` 表从不修剪/压缩，长期实例达到 ~13GB，填满 22GB 卷至 97–99%。这是当前最严重的生产级存储问题。
- 🔗 https://github.com/anomalyco/opencode/issues/33356

### ③ 加密支付 Go 订阅（高赞需求）
- **#23153 [OPEN]** | 评论 21 | 👍 50
- 请求支持加密货币支付 OpenCode Go，社区反响强烈，反映出传统支付渠道的不便。
- 🔗 https://github.com/anomalyco/opencode/issues/23153

### ④ 垂直标签页需求
- **#36942 [OPEN]** | 评论 15 | 👍 31
- 新 UI 强制水平标签，超过 5 个会话标题难以查看。希望支持垂直标签以提升多会话管理效率。
- 🔗 https://github.com/anomalyco/opencode/issues/36942

### ⑤ TUI 显示 Token 使用信息（高赞）
- **#13003 [OPEN]** | 评论 13 | 👍 53
- 目前 Token 使用（输入/输出/剩余预算）仅在内部跟踪，TUI 不显示。开发者需要实时了解消耗情况。
- 🔗 https://github.com/anomalyco/opencode/issues/13003

### ⑥ 支付被拒：卡和银行均无问题
- **#45278 [OPEN]** | 评论 13 | 👍 2
- 用户订阅续费时支付方式突然被拒，同一张卡已成功使用约三个月，银行确认无异常。类似支付问题近期频发。
- 🔗 https://github.com/anomalyco/opencode/issues/45278

### ⑦ Subagent 无限循环：364 次相同工具调用，燃烧 token 约 50 分钟
- **#45442 [OPEN]** | 评论 6 | 👍 1
- 后台 `general` subagent 进入无限循环，反复执行相同 grep 命令，无循环保护机制，导致不可控的 token 消耗。
- 🔗 https://github.com/anomalyco/opencode/issues/45442

### ⑧ 事件表存储完整消息快照导致磁盘暴涨（社区工具已出现）
- **#41175 [OPEN]** | 评论 5 | 👍 4
- `event` 表在每次流式更新时存储完整消息副本（非增量），占数据库约 90% 体积。社区已有开发者提供清理工具。
- 🔗 https://github.com/anomalyco/opencode/issues/41175

### ⑨ `opencode run --format json` 将自动压缩内部信息作为普通文本事件输出
- **#42238 [OPEN]** | 评论 4 | 👍 0
- 自动压缩发生时，内部摘要和合成用户续写提示被当作普通 `type: "text"` JSONL 事件输出，下游消费者无法区分，影响自动化集成。
- 🔗 https://github.com/anomalyco/opencode/issues/42238

### ⑩ 2.0 插件 API 事件订阅不工作，上下文钩子无法注入模型提示
- **#44788 [OPEN]** | 评论 4 | 👍 1
- 在 beta 18050 中，`ctx.event.subscribe` 注册成功但收不到任何事件，`ctx.session.hook("context")` 也无法将上下文注入模型提示，严重阻碍插件生态开发。
- 🔗 https://github.com/anomalyco/opencode/issues/44788

---

## 4. 重要 PR 进展（精选 10 条）

### ① 修复编译提示中的文件系统循环
- **#48397 [OPEN]** | @kernel-oops
- 关联 #44946，在 Bun 升级之外检查编译提示准备中的文件系统循环问题，避免运行时异常。
- 🔗 https://github.com/anomalyco/opencode/pull/48397

### ② TUI 增加递归分组树
- **#48394 [OPEN]** | @jlongster
- 在 v2 上新增纯分组引擎，支持可配置嵌套路径（activity -> exploration/reasoning 等），为后续会话投影做准备。
- 🔗 https://github.com/anomalyco/opencode/pull/48394

### ③ TUI 递归会话分组树
- **#48395 [OPEN]** | @jlongster
- 实现通用的递归分组树，支持有序关联接缝合并和深度优先拆分，缓存叶子总数以优化转录预算。
- 🔗 https://github.com/anomalyco/opencode/pull/48395

### ④ 添加 V2 GenAI 可观测性追踪
- **#35935 [CLOSED]** | @StarpTech
- 通过 OTLP 实现端到端 V2 GenAI 可观测性，记录每个 agent 回合、模型步骤、HTTP/WebSocket 传输、本地工具、重试、压缩、subagent 等，并附 Dash0 配置文档。
- 🔗 https://github.com/anomalyco/opencode/pull/35935

### ⑤ 容忍缺失的 workspace 名称
- **#41610 [CLOSED]** | @opencode-agent[bot]
- 检测旧版 `workspace` 表是否包含 `name` 列后再重建，修复 `no such column: name` 错误，并增加回归测试。
- 🔗 https://github.com/anomalyco/opencode/pull/41610

### ⑥ 回滚后保留压缩结果
- **#41604 [CLOSED]** | @opencode-agent[bot]
- 在允许手动压缩前提交暂存的会话回滚，防止下一次提示在旧回滚边界截断已完成的压缩。
- 🔗 https://github.com/anomalyco/opencode/pull/41604

### ⑦ 拒绝空问题数组，避免会话挂起
- **#41597 [CLOSED]** | @ousamabenyounes
- 修复 `question` 工具接受空 `questions` 数组后无限等待的问题，现在会直接拒绝。
- 🔗 https://github.com/anomalyco/opencode/pull/41597

### ⑧ 压缩时遵循 agent variant 配置
- **#41594 [CLOSED]** | @ousamabenyounes
- 修复 `agent.compaction.variant` 配置无效的问题，不再硬编码继承父用户消息的 variant。
- 🔗 https://github.com/anomalyco/opencode/pull/41594

### ⑨ 防止大段粘贴导致界面卡顿
- **#41579 [CLOSED]** | @vanthunder
- V2 编辑器中大段多行粘贴不再通过 `execCommand("insertText")` 路由，避免 Chromium 创建大量 DOM 导致卡死。
- 🔗 https://github.com/anomalyco/opencode/pull/41579

### ⑩ 支持可配置标签位置（上/下/左/右）
- **#41575 [CLOSED]** | @kitlangton
- V2 TUI 标签可通过设置放置在顶部、底部、左侧或右侧，侧边保留 42 列垂直侧栏，终端过窄时回退顶部。直接响应 #36942 垂直标签需求。
- 🔗 https://github.com/anomalyco/opencode/pull/41575

---

## 5. 功能需求趋势

从近期 Issues 中可提炼出以下社区最关注的方向：

- **UI/UX 改进**：垂直标签（#36942）、TUI 显示 Token 用量（#13003）、桌面端麦克风按钮（#37742）、Markdown 正确渲染（#38828）、可配置标签位置（PR #41575）。
- **支付与订阅**：加密货币支付（#23153）、支付失败/无法续费（#45278、#43400、#48374）、账户删除（#48360）。
- **性能与存储**：事件表无界增长（#33356、#41175）、磁盘空间耗尽（#48384）、subagent 无限循环（#45442）。
- **插件与扩展性**：插件 API 事件订阅失效（#44788）、GenAI 可观测性追踪（PR

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*