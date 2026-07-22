# OpenClaw 生态日报 2026-07-23

> Issues: 401 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-22 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目日报 — 2026-07-23

## 1. 今日速览

过去 24 小时内，OpenClaw 项目保持着极高的社区活跃度，共新增或更新 401 条 Issue（其中新开/活跃 252 条，关闭 149 条），PR 处理量达 500 条（待合并 318 条，已合并/关闭 182 条）。核心贡献者 @steipete 集中提交了超过 20 个重构与功能 PR，涉及代理模型归一化、UI 侧边栏组件提取、会话可见性管理、日志文件分离等，代码库清理与架构整合明显加速。同时，多个高优先级 Bug（P0/P1）仍在持续讨论，暂无新版本发布，但项目正向更健壮的模块化方向稳步推进。

> 本期数据来源：GitHub 时间窗口 2026-07-22 00:00 UTC – 2026-07-23 00:00 UTC

---

## 2. 版本发布

**无新版本发布。**  
（上一版本仍为 2026.7.1 或 2026.7.2，具体请查阅 Releases 页面。）

---

## 3. 项目进展｜今日合并/关闭的重要 PR

以下为今日已合并或关闭的核心 PR，涉及性能修复、安全策略、UI 重构和测试优化：

- **[fix(sessions): gateway becomes unusable when there are many sessions](https://github.com/openclaw/openclaw/pull/112273)**（#112273，OPEN 但标记为待合并？）  
  → **说明**：修复大会话数（~4900）导致网关事件循环阻塞 35–59 秒的问题，是今日最直接提升稳定性的改进。

- **[fix(msteams): reset sessions on app removal lifecycle](https://github.com/openclaw/openclaw/pull/104690)**（#104690，OPEN）  
  → 修复 Teams 应用删除后重新添加仍保留旧会话历史的安全隐患（关联 #99054），方案已获得 maintainer 初步审查。

- **[fix(gateway): isolate wizard exits from shared process](https://github.com/openclaw/openclaw/pull/110382)**（#110382，OPEN）  
  → 隔离设置向导退出行为，防止远程调用误关闭网关主进程（关联 #110545），已标记为“ready for maintainer look”。

- **[fix(context-engine): bound deferred turn maintenance with a per-task timeout](https://github.com/openclaw/openclaw/pull/97175)**（#97175，OPEN）  
  → 为上下文引擎的延迟维护任务增加超时保护，避免因锁竞争导致后续用户消息无限等待。

- **[fix(memory-core): keep live reindex of reset/deleted session archives](https://github.com/openclaw/openclaw/pull/96132)**（#96132，CLOSED）  
  → 修复重置/删除会话后，记忆索引无法实时更新的问题（需重启网关才能找回历史）。现已在 live 模式下正确重建索引。

- **[refactor(agents): consolidate model normalization](https://github.com/openclaw/openclaw/pull/112772)**（#112772，OPEN）  
  → 将代理模型引用归一化逻辑整合到一处，消除代码重复，简化审核路径。

- **[refactor: remove stale E2E proof scripts](https://github.com/openclaw/openclaw/pull/112776)**（#112776，CLOSED）  
  → 清理 8 个无调用者的 E2E 测试脚本，减少 2529 行死代码维护负担。

- **[refactor(ui): sidebar cleanups — shared tooltips, one idle-import helper, cross-tab outbox bridge](https://github.com/openclaw/openclaw/pull/112780)**（#112780，CLOSED）  
  → 统一侧边栏工具提示、优化空闲导入、增加跨标签发送箱桥接。

- **[test(ui): collapse chat-send request mock boilerplate](https://github.com/openclaw/openclaw/pull/112783)**（#112783，CLOSED）  
  → 将 ~156 个 chat-send 测试中的重复模拟代码抽取为单一定义，提升可维护性。

**总计**：今日关闭/合并 PR 约 30+ 项，除上述重点外还包括日志文件分离（#112777）、会议插件粘合代码抽取（#112785）、CLI 测试装置合并（#112779）等。整体架构整洁度与测试效率显著提升。

---

## 4. 社区热点

今日讨论最活跃的 Issue 与 PR 反映了用户对性能、安全性和跨渠道一致性的强烈关注：

| 编号 | 标题 | 评论数 | 👍 | 摘要 |
|------|------|--------|-----|------|
| [#85333](https://github.com/openclaw/openclaw/issues/85333) | `openclaw doctor --fix` 4-5x slower on 2026.5.20 vs 2026.5.19 | **17** | 1 | 会话快照路径遍历导致性能瓶颈，从 55s 骤升至 229s+。讨论核心是 `doctor --fix` 的路径解析算法需优化。 |
| [#13583](https://github.com/openclaw/openclaw/issues/13583) | Pre-response enforcement hooks (hard gates) for mandatory tool-call | **16** | 2 | 社区要求“硬门控”强制工具调用策略，用于金融、安全等高保证场景。对“软提示”不可靠的共识强烈。 |
| [#91009](https://github.com/openclaw/openclaw/issues/91009) | Codex PreToolUse native hook relay spawns CPU-bound processes | **15** | 2 | Codex 集成中的 PreToolUse 事件产生大量短生命周期进程，每进程耗 100%+ CPU，导致 RPC 网关阻塞。已有多个 linked PR 在讨论。 |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | Masked Secrets – Prevent Agent from Accessing Raw API Keys | **15** | 4 | 安全核心诉求：让代理能使用密钥但不能读取明文。点赞最高。提案已有明确 shape，但需产品决策和安全性审查。 |
| [#96857](https://github.com/openclaw/openclaw/issues/96857) | Normal tool text outputs degrade to “(see attached image)” placeholders | **13** | 4 | 代理上下文中的工具输出被替换为占位符，使代理对部分命令输出“失明”，影响多步骤自动工作流。用户对此非常不满。 |
| [#92043](https://github.com/openclaw/openclaw/issues/92043) | 180s compaction timeout blocks legitimately-long compactions | **12** | 3 | 压缩超时从 900s 降为 180s 后，对长历史 / 慢模型用户造成循环失败。用户要求部分进度重用。 |

**分析**：性能回归（#85333、#91009、#92043）和安全强化（#13583、#10659）成为今日绝对热点。用户对“软规则”的不信任感增强，并希望 OpenClaw 能提供机械强制机制。

---

## 5. Bug 与稳定性

以下按严重程度列出今日最受关注的 Bug（含已有 fix PR 的）：

### P0 / 发布阻断

- **[Bug]: update to openclaw 2026.7.1: gateway fails to start](https://github.com/openclaw/openclaw/issues/108435)**  
  **严重程度**：P0，发布阻断  
  **摘要**：2026.7.1 版本在 systemd、Ollama、手动启动下均无法启动，报错 `gateway did not start on 127.0.0.1:18789`。  
  **状态**：未关联 fix PR，需要 maintainer 紧急介入。

- **[Bug]: cron tool schema incompatible with llama.cpp grammar-constrained tool calling](https://github.com/openclaw/openclaw/issues/108580)**  
  **严重程度**：P1（新回归）  
  **摘要**：2026.7.1 中 cron 工具 schema 新增字段导致 llama.cpp 语法约束解析失败，每个聊天请求都崩溃。  
  **状态**：已有 linked PR，但未合并。

### P1 / 重要回归

- **[Bug]: 180s compaction timeout is a single wall clock with no partial-progress reuse](https://github.com/openclaw/openclaw/issues/92043)**  
  → 压缩超时设计问题，可复现失败循环。尚未有 fix，讨论中有建议引入阶段性 checkpoint。

- **[Bug]: Normal tool text outputs degrade to “(see attached image)” placeholders](https://github.com/openclaw/openclaw/issues/96857)**  
  → 代理“失明”问题，影响自动化脚本。无关联 fix，社区在排查根因。

- **[Bug]: Codex PreToolUse native hook relay spawns CPU-bound processes](https://github.com/openclaw/openclaw/issues/91009)**  
  → 已有 linked open PR（#91009 自身为 Issue，但多个 PR 尝试修复），尚需 maintainer 最终审查。

- **[Bug]: Model fallback chain not triggered on provider-wide quota exhaustion](https://github.com/openclaw/openclaw/issues/85103)**  
  → 在上周被关闭，但今天并未重新打开，可能已修复或等待验证。需要关注验证结果。

### P2 / 中优先级

- **[Bug]: Gateway memory growth due to repeated file read errors](https://github.com/openclaw/openclaw/issues/87314)**  
  → 内存每天增长 ~60MB，源自定时任务中的 `tools.read failed` 错误。需改进错误处理或释放。

- **[Bug]: exec tool silently corrupts 2>&1 / 2>/dev/null shell redirect arguments](https://github.com/openclaw/openclaw/issues/87980)**  
  → 阻止使用 shell 重定向，影响所有 `gh` 命令集成工作流。社区无 workaround。

---

## 6. 功能请求与路线图信号

今天讨论了多项未来发展方向，部分已有实现 PR：

| Issue | 摘要 | 是否已有 PR | 可能纳入版本 |
|-------|------|-------------|--------------|
| [#13583](https://github.com/openclaw/openclaw/issues/13583) | Pre-response enforcement hooks（硬门控） | 无 | 远期（需产品决策 + 安全审查） |
| [#10659](https://github.com/openclaw/openclaw/issues/10659) | Masked secrets（密钥屏蔽） | 无 | 远期 |
| [#9912](https://github.com/openclaw/openclaw/issues/9912) | maxTurns / maxToolCalls 配置项 | 无 | 中期 |
| [#10142](https://github.com/openclaw/openclaw/issues/10142) | session:end 内部钩子事件 | 有 linked PR | 近期（已有 `session:end` hook PR 草稿） |
| [#38568](https://github.com/openclaw/openclaw/issues/38568) | 在系统提示中注入上下文窗口占比 | 无 | 远期，但社区点赞高 |
| [#112787](https://github.com/openclaw/openclaw/pull/112787) | 会话可见性状态、成员管理、服务器强制参与 | PR 已提交 | **近期**（由 @steipete 提交，正在审查） |
| [#112773](https://github.com/openclaw/openclaw/pull/112773) | 可移植代理策略设置（Claw manifest） | PR 已提交 | 近期（与 #111391 配合） |

**信号**：用户对“硬策略”（强制钩子、密钥屏蔽、maxTurns）的呼声持续高涨，表明社区从简单演示走向生产级部署。同时，会话可见性与协作管理（#112787）可能是下一版本的重点功能。

---

## 7. 用户反馈摘要

从今日 Issues 评论中提炼的真实用户痛点与场景：

1. **性能退化不可接受**  
   > “Same command went from 55 seconds to over 229 seconds.”（#85333）  
   → 用户 @samson1357924 在 VPS 上经历 4 倍慢化，强烈要求回归或优化。

2. **硬门控是刚需**  
   > “Soft rules are not acceptable: the agent must be mechanically prevented from emitting a final answer.”（#13583）  
   → 金融/安全用户 @JamieMolty 表示软提示无法满足合规要求。

3. **密钥安全处于最优先**  
   > “Prevents accidental leaks and protects against prompt injection.”（#10659）  
   → @jmkritt 指出当前代理可看见所有 API 密钥，是巨大安全隐患。

4. **跨渠道一致性差**  
   > “/status works on Telegram but intermittently no response on LINE.”（#94626）  
   → @samson1357924 抱怨 LINE 渠道状态不稳定，且回复令牌过期竞争条件。

5. **子代理输出错误送达**  
   > “Subagent run completion delivered to chat user as raw worker output.”（#90840）  
   → @longjie521 发现嵌套代理的原始输出被直接推送到 QQ 聊天，暴露内部逻辑。

6. **社区对快速修复的期待**  
   > “Rollback to 2026.5.12 stabilizes.”（#83968）  
   → 多个用户提到降级作为临时方案，但希望 mainline 尽快修复。

---

## 8. 待处理积压｜长期未响应的重要 Issue

以下 Issue 标记为 `stale` 但严重性高（P1/P2），且长时间没有 maintainer 响应或进展：

| Issue | 标题 | 创建时间 | 最后更新时间 | 备注 |
|-------|------|----------|-------------|------|
| [#85333](https://github.com/openclaw/openclaw/issues/85333) | `doctor --fix` 4-5x slower | 2026-05-22 | 2026-07-22 | 17 评论，无 fix PR，需 maintainer 确认路径优化方案。 |
| [#39807](https://github.com/openclaw/openclaw/issues/39807) | Billing 402 causes infinite retry death spiral | 2026-03-08 | 2026-07-22 | 已有 linked PR，但 4 个月未合并，影响所有 inline-apiKey 用户。 |
| [#41199](https://github.com/openclaw/openclaw/issues/41199) | Agent-to-Agent 通信工具参数冲突 | 2026-03-09 | 2026-07-22 | 系统级问题，导致 LLM 重复添加冲突参数，7 条评论但无实际进展。 |
| [#65538](https://github.com/openclaw/openclaw/issues/65538) | 屏幕阅读器在流式输出时每 token 播报 | 2026-04-12 | 2026-07-22 | 无障碍 Bug，7 评论，无 linked PR，需产品决策。 |
| [#74021](https://github.com/openclaw/openclaw/issues/74021) | 原生推理模型 reasoning 字段处理 | 2026-04-29 | 2026-07-22 | 此问题已关闭但可能未完全解决，影响基准测试准确性。 |
| [#77802](https://github.com/openclaw/openclaw/issues/77802) | `doctor --fix` 原子失败导致修复无法持久化 | 2026-05-05 | 2026-07-22 | 已关闭但仅通过 PR #77804 修复部分场景，仍有用户报告残留问题。 |

**建议**：Project maintainers 可优先处理 #85333（性能最直观）、#39807（无限重试浪费配额）、#41199（阻断 Agent-to-Agent

---

## 横向生态对比

好的，作为一名资深技术分析师，基于您提供的2026-07-23各项目动态摘要，我为您生成以下横向对比分析报告。

---

### **个人AI助手与自主智能体开源生态横向对比分析报告 (2026-07-23)**

#### **1. 生态全景**

当前，个人AI助手与自主智能体开源生态正经历从“功能可用”向“生产可靠”的关键跃迁。社区活跃度极高，头部项目日均处理数百条Issue和PR，表明开发者正大规模涌入。然而，生态内部分化明显：**核心基础设施层**（如代理网关、会话管理、工具链）正快速走向模块化和标准化，以解决性能和安全等“硬骨头”；**应用体验层**（如桌面端、跨平台集成）则面临兼容性与一致性的巨大挑战。整体上，社区对**机械化的安全门控、跨会话持久记忆、以及高性能低延迟的运行时**提出了前所未有的刚性需求，标志着AI智能体正从实验沙盒走向严肃的业务场景。

#### **2. 各项目活跃度对比**

下表汇总了各项目在2026-07-23这一天的核心数据，以便直观对比。

| 项目名称 | 活跃 Issues | 新PR总数 | 版本发布 | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 252 | 500 | 无 | **高 (但存在P0风险)**：代码重构力度大，模块化加速，但P0级启动失败Bug急需解决。 |
| **Hermes Agent** | 266 | 500 | 无 | **高 (有严重风险)**：Issue解决效率高，但数个P1级Bug影响生产，如Agent死锁、会话损坏。 |
| **OpenHands SDK** | 17 | 48 | 无 | **高 (稳固)**：Bug修复迅速，功能合并稳健，虽有P1级问题，但已有沟通和修复进行中。 |
| **Pi** | 70 | 30 | 无 | **高 (精益求精)**：维护者和贡献者效率极高，大部分问题当天关闭，专注TUI和本地模型体验。 |
| **LiteLLM** | 44 | 217 | 2个预发布版 | **极高 (迭代冲刺)**：高强度开发同时面临严重Bug，计费缓存和预算绕过问题威胁核心功能。 |
| **Temporal** | 0 | 64 | 无 | **中 (工程导向)**：核心架构推进强劲（CHASM, VTS），但用户侧（Issues）活跃度极低，社区互动需加强。 |

#### **3. OpenClaw 在生态中的定位**

OpenClaw 在该生态中扮演着 **“AI智能体操作系统”** 的角色，其核心差异化优势在于：
*   **架构领先性**：正如日报所示，其代码库正经历大规模重构，以实现代理模型归一化、UI组件化和会话管理标准化。这种底层的架构整合，是其他项目（如Pi、Hermes Agent）尚未系统性推进的。
*   **深度跨渠道集成**：OpenClaw修复了Teams、LINE等渠道的具体Bug，表明其目标是构建一个覆盖广泛、行为一致的跨平台代理底座，而非单纯优化某一端体验。
*   **安全与治理先行**：社区对“硬门控”（#13583）和“密钥屏蔽”（#10659）的强烈需求，以及对应的具体方案讨论，显示了其在生产级安全策略上的前瞻性。

**与同类对比**：相较于**Hermes Agent**（更侧重Codex和桌面端即时体验）、**Pi**（专注TUI与开发者本地工具链），**OpenClaw**的社区规模更大（日均处理约400+ Issue/500+ PR），讨论的问题更为系统和底层。更类似于一个基础框架，而其他项目更像在此框架之上或与之并行的特定应用或开发工具。

#### **4. 共同关注的技术方向**

多个项目不约而同地涌现出相似的技术需求，揭示了行业的核心痛点：

1.  **安全的工具调用与执行门控**：（涉及**OpenClaw**，#13583硬门控；**Hermes Agent**，#68915 worker死锁；**OpenHands SDK**，#4157 LLM安全分析器自评绕过）—— 社区普遍不再信任“软提示”，要求强制性的机械隔离和审计机制。
2.  **跨会话持久记忆与上下文管理**：（涉及**Hermes Agent**，#8457、#27013；**OpenHands SDK**，#4178已合并；**OpenClaw**，#96857上下文占位符问题）—— 用户不满于Agent重启后“失忆”，要求持久化的、可检索的长期记忆，以支撑连续工作流。
3.  **核心性能和稳定性回归**：（涉及**OpenClaw**，#85333 doctor命令慢4倍、#92043压缩超时；**Pi**，#6911 SDK重试缺陷、#6918持续崩溃；**LiteLLM**，#14457流中断计费缺失）—— 性能退化是影响用户信任度的最大敌人，超过半数的热点讨论与此相关。
4.  **敏感信息（API密钥）的安全遮蔽**：（涉及**OpenClaw**，#10659；**OpenHands SDK**，#4191已修复；**Hermes Agent**，#69449桌面端明文存储）—— 这是一个共识性刚需，防止提示注入和意外泄露。
5.  **多渠道/多模型兼容性与行为一致性**：（涉及**OpenClaw**，#94626 LINE渠道不稳定；**Hermes Agent**，#13834 Codex兼容性、#20859支持Mistral；**Pi**，#6768 Copilot Enterprise问题）—— 用户希望同一个Agent在不同平台和模型上表现出一致、可靠的体验。

#### **5. 差异化定位分析**

| 维度 | OpenClaw | Hermes Agent | OpenHands SDK | Pi | LiteLLM | Temporal |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **功能侧重** | Agent **操作系统/运行时** | Codex & 桌面端 **Agent应用** | Agent **开发SDK/基建工具** | 终端开发者 **TUI Coding Agent** | **LLM 代理/网关** (计费路由) | **工作流/活动引擎** (微服务编排) |
| **目标用户** | 希望自建、定制Agent平台的组织 | 追求极致编码体验的个人开发者 | 希望将Agent能力嵌入自己应用的开发者 | 偏好命令行、深度使用本地模型的工程师 | 需要为LLM调用做集中管理和计费的团队 | 构建可靠、可扩展分布式应用的开发者 |
| **技术架构** | 模块化、微服务导向、重视跨渠道 | 集成度较高、专注于特定（Codex/桌面）交互 | SDK为核心，嵌入宿主应用，支持多种协议 | 高度插件化、组件化，聚焦TUI交互 | 无状态代理，核心是模型路由和计费引擎 | 分布式、持久化、强一致性的工作流引擎 |
| **核心挑战** | 模块化整合的稳定性与性能 | 跨平台一致性与生产级可靠性 | SDK的灵活性与使用复杂度平衡 | TUI交互范式的普适性 | 分布式缓存一致性及计费准确性 | 架构迁移（CHASM）对现有用户的平滑过渡 |

#### **6. 社区热度与成熟度**

*   **第一梯队（高活跃、快速迭代）**：**OpenClaw** 和 **LiteLLM**。两者日均处理数百条PR，社区讨论极为活跃。OpenClaw正经历架构重塑，LiteLLM则在疯狂补功能和修Bug。它们代表了生态中最前沿和最具活力的部分，但同时也伴随着较多的回归和稳定性风险。
*   **第二梯队（高活跃、稳健推进）**：**Hermes Agent** 和 **OpenHands SDK**。同样活跃，但代码合并节奏更稳健，问题处理效率高。两者都聚焦于解决实际痛（Codex兼容、SDK集成），社区反馈也更具建设性。
*   **第三梯队（专注、精耕细作）**：**Pi** 和 **Temporal**。
    *   **Pi**：社区规模相对较小，但贡献者和维护者质量极高，修复速度惊人。虽有小众，但在其领域（本地/TUI编码Agent）内已建立起坚实的口碑。
    *   **Temporal**：社区参与度低，更像一个自上而下的工程驱动项目。其进展体现在核心架构（CHASM, VTS）的推进，而非广泛吸纳社区反馈，成熟度和可靠性最高，但离普通AI开发者较远。

#### **7. 值得关注的趋势信号**

1.  **“从软到硬”的安全理念转变**：社区不再满足于通过提示词约束Agent行为，而是要求**机械化的强制机制**（硬门控、密钥遮蔽、工具调用审计）。这是AI智能体走向企业级合规的必经之路。
2.  **“会话记忆”成为标配**：多个项目同时将跨会话持久记忆作为最高优先级的功能需求或已着手实现。**“记不住”是当前Agent体验的最大断层**，这一问题的解决将极大提升Agent的实用性和自主性。
3.  **性能即信仰**：无论是OpenClaw的启动失败，还是LiteLLM的缓存Bug，都展示了性能退化对社区信任的毁灭性打击。**微小的性能倒退（如医生命令慢4倍）也可能引发大规模用户反弹**，性能基准测试和回归预防将成为项目的关键竞争力。
4.  **从“接入模型”到“管理模型”**：LiteLLM的火爆揭示了AI应用中一个新的核心品类：**LLM网关与代理**。当模型数量爆炸，如何统一管理API、路由、计费、安全和限流，成为一个巨大的市场机会。
5.  **“多功能自治”与“确定性编排”并存**：OpenClaw/Hermes Agent追求更自动、更灵活的Agent，而Temporal则强调确定性、可靠的工作流编排。这反映了两种不同的哲学：**让Agent随机应变 vs. 让系统按计划执行**。未来的复杂AI系统很可能需要两者结合，在灵活性和确定性之间找到平衡。

**给开发者的建议**：如果你在构建一个**平台级或基础设施级**的AI智能体，密切关注OpenClaw的架构变化和LiteLLM的安全模型。如果你在开发**面向开发者的工具**，Pi和Hermes Agent的思路和用户反馈非常有价值。而对于需要**健壮后端逻辑**的复杂应用，Temporal的确定性工作流引擎是值得考虑的关键组件。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-07-23

---

## 1. 今日速览

过去 24 小时内，Hermes Agent 仓库共产生 **356 条 Issue 更新**（其中新开/活跃 266 条，已关闭 90 条）和 **500 条 PR 更新**（待合并 347 条，已合并/关闭 153 条），数据量处于近期高位，项目整体活跃度 **极高**。社区围绕 Codex 兼容性、会话持久化、桌面端 Bug 等话题讨论热烈，多个 P1/P2 级 Bug 报告涌现，但同时也有大量修复补丁在快速迭代。无新版本发布，但主干分支已吸纳多项改进，版本发布窗口临近。

---

## 2. 版本发布

今日 **无新版本发布**。最新稳定版仍为 **v0.19.0**（2026-07-07），请关注后续动态。

---

## 3. 项目进展

今日合并/关闭的 PR 以自动化格式修复和低风险改动为主，主要进展体现在 **大量 Issue 的关闭** 上，表明部分长期积压问题已得到解决：

- **PR #69651**（已合并）— 自动化 JS 格式修复 `npm run fix`，无功能影响。
- **Issue #18733**（已关闭）— 实现 **按模型/按提供方设置压缩阈值** 的 feature request，对应方案已合并入主分支。
- **Issue #44456**（已关闭）— 修复桌面端 `/compress` 命令未正确路由到 slash.exec 的 Bug，阻止压缩功能失效。
- **Issue #47685**（已关闭）— 解决 Z.AI GLM-5.2 在系统提示包含“Hermes Agent”时返回 429 的异常行为，推测为上游策略误解，已通过调整提示词方式规避。
- **Issue #27683**（已关闭）— 修复 web_tools.py 缺少插件初始化导致网页工具静默失败的问题，`_ensure_plugins_discovered()` 补丁已合入 `main`。
- **Issue #27579**（已关闭）— 实现 **空闲触发式上下文压缩**，避免用户输入后才延迟压缩，提升交互体验。

以上关闭表明项目在 **内存/会话管理、多平台兼容性、工具可靠性** 等核心领域持续前进。此外，多个开放性 PR（如 #69630 `fix(agent): recover from dropped tool calls`、#69141 `fix(checkpoints): never auto-delete orphans`）正在等待审查，有望在下一轮合并中落地。

---

## 4. 社区热点

今日讨论最热烈、关注度最高的话题如下：

| Issue/PR | 类型 | 主题 | 评论数 | 👍数 | 分析 |
|----------|------|------|--------|------|------|
| [#13834](https://github.com/NousResearch/hermes-agent/issues/13834) | 开放 Bug | Hermes `openai-codex` 在同机器上失败，而官方 Codex CLI 正常 | 18 | 3 | 核心诉求：Hermes 的 Codex 实现与官方客户端行为不一致，影响日常编码工作流。用户期待 Hermes 能完全替代官方 CLI。 |
| [#8457](https://github.com/NousResearch/hermes-agent/issues/8457) | 开放 Feature | 持久化会话内存 + 跨会话搜索与自动压缩 | 14 | 0 | 长期需求，用户希望 Agent 记忆不随网关重启丢失，且能跨会话检索。已有 `MemoryManager` 但未实现持久化。 |
| [#47349](https://github.com/NousResearch/hermes-agent/issues/47349) | 开放 Feature | 可配置内存后端：禁用 `memory.md`，仅用 honcho/fact_store | 14 | 1 | 对硬编码内存系统的不满，要求灵活选用不同存储方案。 |
| [#18733](https://github.com/NousResearch/hermes-agent/issues/18733) | **已关闭** Feature | 按模型/按提供方覆盖压缩阈值 | 12 | 4 | 获得较高赞同，最终被合并，社区需求得到响应。 |
| [#44456](https://github.com/NousResearch/hermes-agent/issues/44456) | **已关闭** Bug | 桌面端 `/compress` 返回错误“not a quick/plugin/skill command: compress” | 11 | 1 | 影响用户体验的关键命令失效，今日被修复。 |
| [#67600](https://github.com/NousResearch/hermes-agent/issues/67600) | 开放 Bug | 桌面端默认 profile 的会话侧边栏为空 | 10 | 0 | 命名 profile 正常，默认 profile 无会话列表，严重影响入门用户。 |
| [#20859](https://github.com/NousResearch/hermes-agent/issues/20859) | 开放 Feature | 支持 Mistral 作为 LLM 提供方 | 7 | **23** | 获得最高👍数，社区对支持 Mistral 的呼声极高，但项目组尚未明确纳入路线图。 |

**总结**：社区当前最关心的是 **Codex 兼容性、内存持久化、配置灵活性**，以及 **桌面端稳定性**。`#20859` 表示用户希望尽快接入 Mistral 模型。

---

## 5. Bug 与稳定性

今日报告的 Bug 中，按严重性排列如下：

| 严重等级 | Issue | 主题 | 状态 | Fix PR |
|----------|-------|------|------|--------|
| **P1** | [#68915](https://github.com/NousResearch/hermes-agent/issues/68915) | Worker 因为 shell `&` 后台化服务器而永久死锁（orphaned subshell holds stdout pipe open） | 开放 | 暂无 |
| **P1** | [#69078](https://github.com/NousResearch/hermes-agent/issues/69078) | xAI grok-4.5 无效 PNG 图片导致会话永久损坏（400错误） | 开放 | 暂无 |
| **P2** | [#67600](https://github.com/NousResearch/hermes-agent/issues/67600) | 桌面端默认 profile 会话侧边栏为空（后端正常） | 开放 | 暂无 |
| **P2** | [#69078](https://github.com/NousResearch/hermes-agent/issues/69078) | 同上，注意该 Issue 也涉及 xAI 400 错误 |
| **P2** | [#62936](https://github.com/NousResearch/hermes-agent/issues/62936) | Telegram >15MB 上传总是超时，`TELEGRAM_HTTP_WRITE_TIMEOUT` 无效 | 开放 | 暂无 |
| **P2** | [#27013](https://github.com/NousResearch/hermes-agent/issues/27013) | 会话重启后 Agent 丢失项目上下文，开始幻觉 | 开放 | 暂无 |
| **P2** | [#11113](https://github.com/NousResearch/hermes-agent/issues/11113) | MCP 熔断器将工具级错误（如 DNS 失败）误判为服务器故障，触发误熔断 | 开放 | 暂无 |
| **P2** | [#69449](https://github.com/NousResearch/hermes-agent/issues/69449) | 桌面端自定义端点 API 密钥以明文存储在 `config.yaml`（安全风险） | 开放 | 暂无 |
| **P2** | [#14091](https://github.com/NousResearch/hermes-agent/issues/14091) | SSH 会话未传递环境变量 | 开放 | 暂无 |
| **P2** | [#27683](https://github.com/NousResearch/hermes-agent/issues/27683) | web_tools.py 缺少插件初始化（**已关闭，已修复**） | **已修复** | 已合并至 main |
| **P2** | [#47685](https://github.com/NousResearch/hermes-agent/issues/47685) | Z.AI 系统提示包含“Hermes Agent”导致 429（**已关闭，已修复**） | **已修复** | 已于上游调整 |
| **P2** | [#44456](https://github.com/NousResearch/hermes-agent/issues/44456) | 桌面端 `/compress` 失败（**已关闭，已修复**） | **已修复** | 已合并至 main |

此外，今日有 **多条 P1/P2 级 PR 提交修复**，正在等待合并，如：
- PR #69630：修复 provider (copilot) 返回空 `tool_calls` 时 Agent 无法恢复的问题。
- PR #69141：防止无人值守启动时误删检查点孤儿数据。
- PR #69508：加强桌面端项目和会话隔离。

**稳定性评估**：虽然活跃修复数量多，但仍有数个 P1 级 Bug 严重影响生产环境使用（Worker 死锁、xAI 会话损坏），需要维护者优先处理。

---

## 6. 功能请求与路线图信号

今日用户提出的新功能需求以及可能被纳入下个版本的信号：

| Issue | 主题 | 类型 | 热度 | 纳入可能性 |
|-------|------|------|------|------------|
| [#8457](https://github.com/NousResearch/hermes-agent/issues/8457) | 持久化会话内存 + 跨会话搜索 | Feature | 14评论，长期未决 | **高** – 已有 `MemoryManager` 设计，且多个相关 issue 关联（#47349, #27013等），预计会被纳入 v0.20。 |
| [#47349](https://github.com/NousResearch/hermes-agent/issues/47349) | 可配置内存后端（禁用 memory.md） | Feature | 14评论 | 中 – 与前一条关联，但需要更多架构讨论。 |
| [#4335](https://github.com/NousResearch/hermes-agent/issues/4335) | 跨平台会话上下文共享（CLI ↔ Telegram） | Feature | 8评论，自3月开放 | 中 – 属于长期路线图“统一会话”，但实现复杂度高。 |
| [#23524](https://github.com/NousResearch/hermes-agent/issues/23524) | 支持按 cron 任务覆盖推理 effort | Feature | 7评论 | 高 – 近期有 PR 涉及 cron 改进，可能一并处理。 |
| [#12238](https://github.com/NousResearch/hermes-agent/issues/12238) | 内置自动备份与版本控制 | Feature | 5评论，👍19 | 中 – 用户呼声高，但未看到原型代码。 |
| [#7489](https://github.com/NousResearch/hermes-agent/issues/7489) | RPM 预判限流（利用 x-ratelimit 头） | Feature | 5评论，👍5 | 低 – 架构影响较大，可能先作为插件。 |
| [#64900](https://github.com/NousResearch/hermes-agent/issues/64900) | 允许插件扩展 `send_message` 的平台特定字段 | Feature | 5评论 | 低 – 属于插件能力拓展，可能推迟。 |
| [#20859](https://github.com/NousResearch/hermes-agent/issues/20859) | 支持 Mistral 作为 LLM 提供方 | Feature | 7评论，👍23 | **高** – 社区最高点赞请求，Mistral 已与 Hermes 工具链有部分集成（语音），LLM 接入预计很快被提上日程。 |

同时，今日 PR #65076 为 Bedrock 添加了 GPT-5.6 系列模型支持，PR #44987 添加了阿拉伯语/ RTL 支持，显示项目在本地化和云服务集成上持续投入。

---

## 7. 用户反馈摘要

从今日评论中提炼的真实用户声音：

1. **Codex 使用体验不一致**（#13834）：用户 `@army-u8` 抱怨“same machine, same network, official Codex CLI works but Hermes doesn't”，直接表达对替代方案可靠性的质疑。期望 Hermes 能无缝替代官方客户端。

2. **内存丢失导致 Agent 幻觉**（#27013）：用户 `@HECer` 描述“会话重启后 Agent 忘记项目，甚至认为自己在做别的项目”，会严重误导用户，对协作场景影响极大。

3. **桌面端基础功能受阻**（#44456 与 #67600）：多个用户报告桌面端 `/compress` 和侧边栏为空，影响日常使用。`@mahersabbagh80` 强调“error returned before any compression code runs”，说明命令调度层存在缺陷。

4. **安全担忧**（#69449）：用户 `@asorry75` 发现 API 密钥明文存储，表示“security concern”，要求至少使用系统密钥链或加密。

5. **对硬件/平台兼容性的期待**：PR #69646 的作者 `@lo-phare` 提出为 Tirith 工具添加 Windows 二进制支持，暗示部分用户正在 Windows 上尝试运行 Hermes，但平台支持仍有缺口。

6. **对新模型支持的迫切需求**（#20859 的 23 个 👍 和 #65076 的 Bedrock GPT-5.6 支持）表明用户希望第一时间使用最新大模型。

7. **Telegram 生产环境问题**（#62936、#69314）：用户 `@KShad10` 报告大文件上传始终失败，`@ashanzzz` 报告代理后的 Telegram 网关陷入死循环，说明 Telegram 通道在生产环境中的稳定性仍需加强。

---

## 8. 待处理积压

以下 Issue/PR 长期未响应或处于重要决策点，需要维护者关注：

| 编号 | 主题 | 创建时间 | 最后更新 | 状态 | 备注 |
|------|------|----------|----------|------|------|
| [#4335](https://github.com/NousResearch/hermes-agent/issues/4335) | 跨平台会话上下文共享 | 2026-03-31 | 2026-07-22 | 开放，`needs-decision` | 虽然评论活跃，但缺乏维护者回应。 |
| [#8457](https://github.com/NousResearch/hermes-agent/issues/8457) | 持久化会话内存 | 2026-04-12 | 2026-07-22 | 开放 | 自4月提出，至今没有具体实现计划。 |
| [#12238](https://github.com/NousResearch/hermes-agent/issues/12238) | 内置自动备份与版本控制 | 2026-04-18 | 2026-07-22 | 开放，👍19 | 用户呼声较高，但无分配标签。 |
| [#7489](https://github.com/NousResearch/hermes-agent/issues/7489) | RPM 预判限流 | 2026-04-11 | 2026-07-22 | 开放，`P3` | 优秀提案，长期被忽视。 |
| [#140

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

**日期：2026-07-23**  
**数据覆盖时段：2026-07-22 UTC 至 2026-07-23 UTC**  
**数据来源：OpenHands SDK GitHub 仓库 (github.com/OpenHands/software-agent-sdk)**

---

## 今日速览

过去 24 小时项目保持**高活跃度**：共处理 27 条 Issue（17 条活跃 / 10 条关闭）和 48 条 PR（34 条待合并 / 14 条合并或关闭）。虽无新版本发布，但多项关键修复和功能 PR 已完成合并，包括 MCP 订阅、Windows PowerShell 多行命令、秘密遮蔽及跨会话持久记忆等。社区讨论集中在安全分析器信任模型、ACP 协议兼容性以及异步并发限制等痛点。整体项目健康状态良好，代码合并节奏稳健。

---

## 版本发布

无新版本发布（最新 Release 仍为 v1.36.1）。

---

## 项目进展

今日合并 / 关闭的重要 PR 展示了 SDK 在多个维度的推进：

- **MCP 渐进式发现支持**：PR [#3894](https://github.com/OpenHands/software-agent-sdk/pull/3894)（已合并）实现订阅 `tools/list_changed` 通知，使 SDK 能动态加载 MCP 服务器新工具。
- **Windows 终端修复**：PR [#4155](https://github.com/OpenHands/software-agent-sdk/pull/4155)（已合并）修复了 `WindowsTerminal` 无法提交多行 PowerShell 命令的 Bug，解决了 PS1 元数据执行超时问题。
- **MCP 设置迁移恢复**：PR [#4013](https://github.com/OpenHands/software-agent-sdk/pull/4013)（已合并）恢复了 MCP schema 的持久化迁移逻辑，避免旧设置加载失败。
- **持久化跨会话记忆**：PR [#4178](https://github.com/OpenHands/software-agent-sdk/pull/4178)（已合并）引入了可选的持久记忆功能，通过 `MEMORY.md` 在会话间传递学习内容。
- **秘密遮蔽修复**：PR [#4191](https://github.com/OpenHands/software-agent-sdk/pull/4191)（已合并）确保所有注册的秘密（无论是否被命令引用）均在终端输出中被遮蔽，防止泄露。
- **Codex 凭证持久化**：PR [#4124](https://github.com/OpenHands/software-agent-sdk/pull/4124)（已合并）修复了云托管的 ChatGPT 订阅凭证在后端不能正确刷新的问题。
- **市场技能自动加载**：PR [#4176](https://github.com/OpenHands/software-agent-sdk/pull/4176)（已合并）使独立市场技能在云端 / OHE 环境中能自动加载。
- **发布流程动态**：PR [#4123](https://github.com/OpenHands/software-agent-sdk/pull/4123)（Release v1.37.0）因检查项尚未完成被关闭，随后重新发起 PR [#4196](https://github.com/OpenHands/software-agent-sdk/pull/4196)（仍为 Draft，待集成测试）。

这些变更涵盖了终端兼容性、MCP 协议演进、安全加固、用户记忆、市场集成等多个领域，项目整体向前迈进了约 **14 个已合并 PR** 的规模。

---

## 社区热点

今日讨论最活跃的议题（按评论数排序）：

| 议题 | 评论数 | 核心痛点 |
|------|--------|----------|
| [#2078 Daily Integration Runs](https://github.com/OpenHands/software-agent-sdk/issues/2078) | 144 | 每日集成运行结果占位，持续跟踪回归 |
| [#2186 Markdown-based Agents 高级功能](https://github.com/OpenHands/software-agent-sdk/issues/2186) | 13 | Markdown Agent 缺少高级特性（已完成部分） |
| [#4019 ACP profiles 注入重复技能](https://github.com/OpenHands/software-agent-sdk/issues/4019) | 11 | ACP 配置导致项目技能重复加载 |
| [#3950 Daily Examples Run 结果](https://github.com/OpenHands/software-agent-sdk/issues/3950) | 11 | 每日示例脚本运行跟踪 |
| [#3992 弱模型因内容-工具调用不对称处理而终止](https://github.com/OpenHands/software-agent-sdk/issues/3992) | 8 | 响应分发器对无工具调用内容的不对称处理使弱模型无限循环或提前结束 |
| [#4063 max_concurrent_runs 未限制原生异步对话](https://github.com/OpenHands/software-agent-sdk/issues/4063) | 8 | 并发限制仅作用于同步回退，异步路径可无限制并发 |

**分析**：社区讨论集中在**稳定性**（并发控制、弱模型兼容）和**配置正确性**（ACP 重复注入、MCP 设置迁移）上。其中 #3992 引起较多共鸣，因为影响面广——任何产生纯文本响应的模型都会触发异常。此外 #4063 反映异步架构下的资源竞争隐患，维护者已标记 `needs-triage`。

---

## Bug 与稳定性

今日报告的 Bug（按严重程度排列，附修复状态）：

| 严重度 | Issue | 问题描述 | 修复 PR |
|--------|-------|----------|---------|
| **严重** | [#4158 switch_profile 半应用](https://github.com/OpenHands/software-agent-sdk/issues/4158) | ACP 对话中途切换 profile 只更新状态文件，在线会话仍使用旧 agent | 无 |
| **严重** | [#4192 快速重启丢失历史对话](https://github.com/OpenHands/software-agent-sdk/issues/4192) | agent-server 重启后若上次对话在 60s 内则被忽略，不加载进历史 | 无 |
| **高** | [#4080 单个未注册事件类型导致整段对话无法加载](https://github.com/OpenHands/software-agent-sdk/issues/4080) | 反序列化失败的 observation 导致整条 conversation 404，应降级为单个事件丢弃 | 无 |
| **高** | [#4093 ACP 0.11 删除了 Gemini 模型状态字段](https://github.com/OpenHands/software-agent-sdk/issues/4093) | 新版 ACP SDK 移除 `NewSessionResponse.models`，导致 Gemini CLI 报错 | 无 |
| **中** | [#4063 异步并发未受限制](https://github.com/OpenHands/software-agent-sdk/issues/4063) | `max_concurrent_runs` 仅控制同步路径，异步 `EventService.run()` 可无限并发 | 无 |
| **中** | [#4157 LLM 安全分析器信任模型自评估](https://github.com/OpenHands/software-agent-sdk/issues/4157) | `security_analyzer: llm` 下任何自评为 LOW 的动作自动执行，可绕过确认 | 无 |
| **低** | [#4189 可视化器中并行工具调用指标重复](https://github.com/OpenHands/software-agent-sdk/issues/4189) | 同一次 LLM 请求的多个工具调用共享同一个 `llm_response_id`，导致指标重复显示 | [#4193](https://github.com/OpenHands/software-agent-sdk/pull/4193)（已提交） |
| **低** | [#4182 布尔 MCP schema 仍会导致崩溃](https://github.com/OpenHands/software-agent-sdk/issues/4182) | `items: true` 等布尔值未处理，导致 `_process_schema_node` 崩溃 | 已关闭（#4182 自身即关闭） |
| **低** | [#4184 MCP 运行时工具绕过 `filter_tools_regex`](https://github.com/OpenHands/software-agent-sdk/issues/4184) | 运行时物化的 MCP 工具不受 Agent 的正则过滤控制 | 无 |
| **低** | [#4190 秘密不在终端输出中遮蔽](https://github.com/OpenHands/software-agent-sdk/issues/4190) | 若命令文本未引用秘密名称，则输出中的秘密值不遮蔽 | [#4191](https://github.com/OpenHands/software-agent-sdk/pull/4191)（已修复，已合并） |

此外今日已关闭的 Bug：  
- [#4052 MCP schema 迁移未正确应用](https://github.com/OpenHands/software-agent-sdk/issues/4052)（已修复，#4013 合并）  
- [#4133 PowerShell 多行命令超时](https://github.com/OpenHands/software-agent-sdk/issues/4133)（已修复，#4155 合并）  
- [#3412 Laminar 包装器 `throw()` 错误](https://github.com/OpenHands/software-agent-sdk/issues/3412)（已关闭，可能已修复）

**总结**：今日 Bug 修复密集，但仍有多个严重问题（#4158、#4192、#4080、#4093）未分配修复 PR，需维护者优先处理。安全相关 #4157 风险较高，建议尽快提供修复方案。

---

## 功能请求与路线图信号

今日提出的新功能需求：

| Issue | 功能描述 | 关联 PR |
|-------|----------|---------|
| [#4195 外部容器判定作为 agent 观察](https://github.com/OpenHands/software-agent-sdk/issues/4195) | 提供可选的 seam，将外部沙箱的 containment 结果注入为 agent observation | 无 |
| [#4187 服务端持有对话与远程执行工作区](https://github.com/OpenHands/software-agent-sdk/issues/4187) | 支持远程工作区下的 server-owned 对话，解耦对话放置与工作区类型 | 无 |
| [#4199 title LLM profile 作为用户级设置](https://github.com/OpenHands/software-agent-sdk/issues/4199) | 将标题生成 LLM profile 从请求级上移到用户级持久设置 | 无 |
| [#2755 HookType.PROMPT 基于 LLM 的钩子评估](https://github.com/OpenHands/software-agent-sdk/issues/2755) | 实现 prompt-based hook，允许 LLM 自我评估钩子条件 | [#4160](https://github.com/OpenHands/software-agent-sdk/pull/4160)（已提交，Draft） |
| [#3950 Daily Examples 持续集成增强](https://github.com/OpenHands/software-agent-sdk/issues/3950) | 每日示例运行结果跟踪（已有配套 workflow） | 无 |
| [#2055 Claude Code 功能对等](https://github.com/OpenHands/software-agent-sdk/issues/2055) | 主跟踪 Issue，已在多个子 Issue 中推进 | 今日关闭（可能已完成大多数目标） |

**路线图信号**：  
- **持久记忆**（#2037 已关闭，#4178 已合并）标志着 SDK 终于具备了跨会话自动学习能力，是行为倡议路线图中的重要里程碑。  
- **MCP 渐进式发现**（#3894 已合并）为开放 MCP 生态铺平了道路。  
- 社区对**用户级配置持久化**（#4199）和**解耦对话与工作区**（#4187）的呼声较高，预计可能进入 v1.38 规划。

---

## 用户反馈摘要

从 Issue 评论中提炼的真实用户痛点与场景：

- **#3992 弱模型无限终止**：用户 @Rkaplounov 反映：“使用本地小模型时，只要 LLM 返回纯文本（无

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，这是根据您提供的 Pi 项目 GitHub 数据生成的 2026-07-23 项目动态日报。

---

## Pi 项目动态日报 | 2026-07-23

### 1. 今日速览

过去24小时，Pi 项目整体持续高活跃度，社区贡献者和维护者均保持了极高的工作效率。**共处理了70条 Issues 和30条 PR**，其中大部分问题已关闭（61个 Issues，22个 PR），显示了强大的问题解决和代码合并能力。社区对 **OpenRouter OAuth集成、CP-1252 编码支持、Agnai 和 Chub 数据迁移**等新功能反响热烈，同时关于 **Copilot Enterprise 的兼容性、SDK 重试机制、以及 TUI 外部编辑器性能**的问题也引发了深度讨论。项目在修复关键 Bug 和推进新功能方面均取得显著进展。

### 2. 版本发布

*无新版本发布。*

### 3. 项目进展

今日合并了大量 PR，项目在多条线路上取得进展：
- **稳定性与 Bug 修复**：
    - **PR #6958**: 修复了 TUI 崩溃日志硬编码路径的问题，现在会写入配置的 `PI_CODING_AGENT_DIR` 目录。
    - **PR #6903**: 重构了外部编辑器的启动逻辑，通过写入临时子目录而非直接在 `/tmp` 下创建文件，显著加快了 `Ctrl+G` 编辑器的启动速度。
    - **PR #6964**: 修复了 Windows 上 npm 包引入的依赖扩展显示绝对路径的问题。
    - **PR #6955**: 处理了 OpenAI WebSocket 的 `previous_response_not_found` 错误，会清除缓存并建立新连接，提升连接稳定性。
- **新功能与增强**：
    - **PR #6927**: **合并了 OpenRouter OAuth 支持**，用户现在可以通过 OAuth 流程授权使用 OpenRouter API 密钥。
    - **PR #6960**: 新增了对 StepFun 系列模型（`stepfun`, `stepfun-ai` 等）的本地提供商支持。
    - **PR #6916**: 引入了 `AgentHarnessTool` 抽象，允许外部工具在执行时获取应用特定的上下文（如 `ExecutionEnvironment`），为更复杂的代理生态系统奠定基础。
    - **PR #6967**: 将当前 Pi 会话元数据（如 session ID, provider, model）暴露给 bash 工具执行的子进程，方便脚本和扩展使用。
- **其他**：
    - **PR #6976**: 修复了 TUI 启动基准测试因缺少 TTY 而失败的问题。

### 4. 社区热点

- **[#6768] Copilot Enterprise 无法使用上下文压缩**: 该问题获得了 **8个 👍**，成为今日社区最受关注的痛点。用户报告使用 Copilot Enterprise 许可进行上下文压缩会导致 OpenAI (421 Misdirected Request) 和 Anthropic 模型均失败。这反映了企业级用户对特定提供商支持的迫切需求。
    - 链接: [https://github.com/earendil-works/pi/issues/6768](https://github.com/earendil-works/pi/issues/6768)
- **[#6922] 默认模型为 llama.cpp 时启动失败**: 该问题获得 **7个 👍**，显示本地模型部署用户对配置便捷性的强烈不满。当用户设置 `llama.cpp` 为默认提供商后，Pi 会因找不到模型而提示“No models available”并退出，这是一个关键的用户体验阻断。
    - 链接: [https://github.com/earendil-works/pi/issues/6922](https://github.com/earendil-works/pi/issues/6922)
- **[#6879] 自动上下文压缩不触发**: 用户报告在长达2小时的代理轮次中，上下文使用量超过100%后，自动压缩并未触发，直到API因超出限制而报错。这暴露了在长时间运行的任务中资源管理逻辑的缺陷，需求是确保压缩能在达到限制前主动触发。
    - 链接: [https://github.com/earendil-works/pi/issues/6879](https://github.com/earendil-works/pi/issues/6879)

### 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 状态 / Fix PR |
| :--- | :--- | :--- | :--- |
| **严重** | [#6911] | OpenAI/Anthropic SDK 重试机制存在缺陷：会完整等待 `Retry-After` 头信息（可能长达数天），且无法被 `AbortSignal` 中断。 | **已修复** (PR #6980) |
| **严重** | [#6918] | Pi v0.81.0 持续崩溃，错误为 `TypeError: streamFunction is not a function`，影响核心的 `streamAssistantResponse` 流程。 | 待排查 |
| **严重** | [#6920] | 输入 `/` 触发自动补全时崩溃，错误为 `TypeError: value.startsWith is not a function`，可能是提供商返回非字符串值导致。 | 待排查 |
| **高** | [#6879] | 自动压缩功能在上下文超过100%后仍不触发，直至API报错。 | 待修复 |
| **高** | [#6476] (回归) | v0.80.6 版本中，为自托管 OpenAI 兼容提供商设置的 `httpIdleTimeoutMs` 参数不再生效，导致请求被错误地提前超时。 | 已关闭 |
| **中** | [#6686] | Pi 会自动登出 GitHub，该问题在另一 Issue #2725 中已报告，但仍在 v0.80.7 重现。 | 待修复 |
| **中** | [#6817] | Windows 上 `find` 工具对包含路径分隔符的模式（如 `src/**/*.ts`）返回“无结果”。 | 待修复 |
| **中** | [#6957] | `aws-bedrock` 提供商在存在 `AWS_*` 环境变量时，会忽略配置文件中指定的 profile。 | 待修复 |
| **低** | [#6652] | TUI 崩溃日志路径硬编码为 `~/.pi/agent/pi-crash.log`，忽略 `PI_CODING_AGENT_DIR` 设置。 | **已修复** (PR #6958) |
| **低** | [#6774] | 当 `os.tmpdir()` 目录文件过多时，外部编辑器启动缓慢。 | **已修复** (PR #6903) |

### 6. 功能请求与路线图信号

- **隐藏环境变量 (Feature Request #6923)**: 用户希望增加一个标志或命令来对 Pi 隐藏全局环境变量（如 API 密钥），以便在使用不同工具时拥有更细致的控制。该需求反映了用户在安全隔离和隐私方面的考量。
    - 链接: [https://github.com/earendil-works/pi/issues/6923](https://github.com/earendil-works/pi/issues/6923)
- **添加安装说明到 README (Feature Request #6907)**: 新用户/贡献者迫切希望 README 中包含清晰的安装指南，以降低入门门槛。这通常是项目发展初期到成熟期过渡时社区最基础也最强烈的需求。
    - 链接: [https://github.com/earendil-works/pi/issues/6907](https://github.com/earendil-works/pi/issues/6907)
- **OpenRouter OAuth 支持 (PR #6927)**: 今日已合并，标志着 Pi 正式支持 OpenRouter 的标准 OAuth 授权流程，极大地方便了该平台的用户。
    - 链接: [https://github.com/earendil-works/pi/pull/6927](https://github.com/earendil-works/pi/pull/6927)
- **提供工具调用事件 (Feature/PR #6971 & #6703)**: 有 PR 尝试通过 `bash_execution_update` 事件在工具执行期间提供更细粒度的通知，以便客户端（如 Emacs）能够更好地处理并行执行和展示状态。这预示着对更丰富、更实时的事件系统的需求在增长。
    - 链接: [https://github.com/earendil-works/pi/pull/6971](https://github.com/earendil-works/pi/pull/6971)

### 7. 用户反馈摘要

- **对回归问题敏感**: 用户 `@hoho51` 在 [#6476] 中详细报告了 `httpIdleTimeoutMs` 在 v0.80.6 的回归，并明确指出在 v0.80.3 工作正常。这种精确的版本回溯反馈对排查问题非常有价值。
- **长期问题未解决导致挫败感**: 用户 `@bachya` 在 [#6686] 中明确指出“GitHub 自动登出”是之前已报告的 [#2725] 的延续，至今仍存影响。这表明用户对复发性、未被彻底修复的问题感到不满。
- **工作流受阻**: 用户 `@MojangPlsFix` 在 [#6768] 中因使用 Copilot Enterprise 而无法进行上下文压缩，直接导致其工作流程中断。这凸显了 Pi 在特定企业级环境下的适配性问题。
- **对细节和定制的追求**: 用户 `@IstPlayer` 在 [#6459] 中报告自定义键绑定在初始会话中不生效，需要 `/reload`。用户 `@possibilities` 在 [#6774] 中请求优化 `os.tmpdir()` 的使用方式以避免性能瓶颈。这些反馈都指向用户正深度使用 Pi，并对工具链的细节和效率有较高要求。

### 8. 待处理积压

- **[#2557] `tool_call` “edit”在冲突编辑时仍然执行，且扩展无法检测冲突**: 此 Issue 自 3月24日 创建以来长期未获得根本性修复，虽然有一个 PR (#5144) 但未被合并。这是一个涉及核心编辑安全和扩展生态系统的关键问题，维护者应重新评估其重要性。
    - 链接: [https://github.com/earendil-works/pi/issues/2557](https://github.com/earendil-works/pi/issues/2557)
- **[#6479] 子文件夹中的技能不可用**: 用户报告将技能安装在子文件夹（如 `~/.agents/skills/third-party`）后 Pi 无法识别。问题创建于7月10日，目前评论数较少，可能被忽视。这会影响社区分享和结构化技能管理的需求。
    - 链接: [https://github.com/earendil-works/pi/issues/6479](https://github.com/earendil-works/pi/issues/6479)

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-07-23

---

## 1. 今日速览

过去 24 小时内，LiteLLM 项目保持极高活跃度：共处理 **50 条 Issue**（新开/活跃 44 条，关闭 6 条）和 **217 个 PR**（待合并 143 个，已合并/关闭 74 个）。两个预发布版本（`v1.95.0-dev.1` 和 `v1.94.0-rc.3`）同步推出，持续迭代 Proxy、UI、SDK 及多模型集成。重大方向（如 Rust 迁移）的讨论持续升温，同时社区反馈了大量生产环境中的计费、缓存、UI 可用性等稳定性问题，修复 PR 跟进迅速。项目整体处于高强度开发与质量巩固并行阶段。

---

## 2. 版本发布

过去 24 小时发布了两个新版本：

- **v1.95.0-dev.1** — 开发版，包含 Docker 镜像签名验证功能，为后续正式版做准备。
- **v1.94.0-rc.3** — 候选版，同样强化了镜像安全性验证。

> 两个版本均为预发布版，未提及破坏性变更或迁移注意事项。建议生产环境用户继续使用已稳定的正式版（如 v1.94.x），开发测试可试用 dev/rc 分支。

---

## 3. 项目进展（重要合并/关闭 PR）

过去 24 小时内共合并/关闭 74 个 PR，以下为具有代表性的推进：

| PR | 状态 | 类型 | 摘要 |
|----|------|------|------|
| [#34185](https://github.com/BerriAI/litellm/pull/34185) | ✅ 已合并 | 修复 | 团队成员添加变为原子操作，防止并发添加导致成员丢失 |
| [#34181](https://github.com/BerriAI/litellm/pull/34181) | ✅ 已合并 | 修复 | SCIM PATCH 路径解析兼容性，当 value 省略时正确提取 membership id |
| [#34305](https://github.com/BerriAI/litellm/pull/34305) | ✅ 已合并 | 修复 | UI 日志设置中移除误导性的 `os.environ` 提示（该语法已不再支持） |
| [#33284](https://github.com/BerriAI/litellm/pull/33284) | 🟡 待合并 | 依赖 | GitHub Actions 依赖一站式更新（19 个包），提升 CI 安全性 |
| [#34304](https://github.com/BerriAI/litellm/pull/34304) | 🟢 新建 | 重构 | 将旧用量页面从 Tremor 迁移至 shadcn，主题统一化 |
| [#34303](https://github.com/BerriAI/litellm/pull/34303) | 🟢 新建 | 重构 | Playground 页面从 antd/Tremor 迁移至 shadcn，修复水平溢出 |
| [#34311](https://github.com/BerriAI/litellm/pull/34311) | 🟢 新建 | 修复 | 解决 `model_group_alias` 导致预路由钩子 400 错误 |
| [#34312](https://github.com/BerriAI/litellm/pull/34312) | 🟢 新建 | 修复 | Bedrock 跨区域推理配置前缀在 `count_tokens` 中保留 |
| [#34307](https://github.com/BerriAI/litellm/pull/34307) | 🟢 新建 | 修复 | 挂起请求 Slack 告警正确读取 Key/Team 别名 |
| [#34046](https://github.com/BerriAI/litellm/pull/34046) | 🟢 新建 | 修复 | OpenAI 缓存写入 token 映射，修复计费遗漏 |

> **项目整体向前迈进了多少**：79 个 PR（合并+关闭）和 44 个活跃 Issue 表明团队同时交付修复、重构和新功能。UI 向 shadcn 的统一迁移进入攻坚期，多路由 alias 兼容性问题得到解决，Bedrock 和 OpenAI 的计费/缓存边缘 case 被填补。Rust 迁移虽无 PR 落地，但主 Issue 持续吸纳社区反馈。

---

## 4. 社区热点

| Issue/PR | 链接 | 评论数 | 热度分析 |
|----------|------|--------|----------|
| [#31263](https://github.com/BerriAI/litellm/issues/31263) Rust 迁移主议题 | [🔗](https://github.com/BerriAI/litellm/issues/31263) | 16 评论，14 👍 | 社区对性能提升（<1ms 开销）高度期待，已开放 Beta 申请，路线图信号明确 |
| [#361](https://github.com/BerriAI/litellm/issues/361) 愿望列表（已关闭） | [🔗](https://github.com/BerriAI/litellm/issues/361) | 472 评论 | 历史遗留帖，但仍是社区需求汇总地，可作未来功能决策参考 |
| [#14457](https://github.com/BerriAI/litellm/issues/14457) 流中断丢失用量数据 | [🔗](https://github.com/BerriAI/litellm/issues/14457) | 7 评论，3 👍 | 影响计费准确性的高优 bug，社区讨论强烈要求修复 |
| [#19858](https://github.com/BerriAI/litellm/issues/19858) Claude 工具调用损坏 | [🔗](https://github.com/BerriAI/litellm/issues/19858) | 5 评论 | 影响 Claude Sonnet 4.5 + Kilo Code 等工具链，用户急切等待修复 |

**背后诉求**：性能（Rust 迁移）、计费完整性（流中断、缓存计费）、多模型兼容性（Claude、Bedrock）是目前社区最关注的三大方向。

---

## 5. Bug 与稳定性（按严重程度排列）

| 严重度 | Issue | 描述 | fix PR 状态 |
|--------|-------|------|-------------|
| 🔴 致命 | [#34217](https://github.com/BerriAI/litellm/issues/34217) | `/team/delete` 未清理虚拟键缓存，导致已删除团伙的键仍可通过认证 | 无 |
| 🔴 致命 | [#34238](https://github.com/BerriAI/litellm/issues/34238) | 终端用户预算因 Redis 计数器过期后回退到过时逐节点费用，可被绕过 | [#34298](https://github.com/BerriAI/litellm/pull/34298) (新建) |
| 🟠 高 | [#14457](https://github.com/BerriAI/litellm/issues/14457) | 客户端断流导致用量数据丢失，计费缺口 | 无 |
| 🟠 高 | [#34299](https://github.com/BerriAI/litellm/issues/34299) | Redis 缓存写入吞异常，断路器永不打开 | 无 |
| 🟠 高 | [#34309](https://github.com/BerriAI/litellm/issues/34309) | OpenAI Responses API 缓存成本字段始终为 null | 无 |
| 🟡 中 | [#34271](https://github.com/BerriAI/litellm/issues/34271) | 挂起请求 Slack 告警始终显示空白别名 | [#34307](https://github.com/BerriAI/litellm/pull/34307) (新建) |
| 🟡 中 | [#34272](https://github.com/BerriAI/litellm/issues/34272) | Bedrock CountTokens 剥离跨区域前缀，导致 400 | [#34312](https://github.com/BerriAI/litellm/pull/34312) (新建) |
| 🟡 中 | [#31301](https://github.com/BerriAI/litellm/issues/31301) | OpenAI 5.x 推理模型温度验证缺失 | [#34301](https://github.com/BerriAI/litellm/issues/34301) (新报告) |
| 🟡 中 | [#29397](https://github.com/BerriAI/litellm/issues/29397) | AdaptiveRouter 重启后崩溃 “gammavariate: alpha and beta must be > 0.0” | 无 |
| 🟢 低 | [#34281](https://github.com/BerriAI/litellm/issues/34281) | 健康检查在主机离线时硬失败，应优雅降级 | 无 |

**总评**：计费/预算绕过和缓存一致性问题最为紧急，团队已提交多个修复 PR；UI 相关问题也有并行修复。稳定性整体可控但需警惕 Redis 类分布式问题。

---

## 6. 功能请求与路线图信号

| 请求 | 链接 | 潜在纳入版本 |
|------|------|--------------|
| **Rust 迁移**—子 1ms 代理 | [#31263](https://github.com/BerriAI/litellm/issues/31263) | 中长期路线图（已有 Beta 表单） |
| **Bedrock 会话标签**（CUR 2.0 成本归属） | [#34069](https://github.com/BerriAI/litellm/issues/34069) | 可能 v1.95.0+，已有社区贡献 |
| **Bedrock AgentCore 网页搜索**作为原生搜索提供者 | [#31819](https://github.com/BerriAI/litellm/issues/31819) | 路线图候选，反馈积极 |
| **UI 预算/多窗口/权限增强**（多 Issue 合并） | [#34294](https://github.com/BerriAI/litellm/issues/34294), [#34295](https://github.com/BerriAI/litellm/issues/34295), [#34297](https://github.com/BerriAI/litellm/issues/34297) | 已有多项 UI 重构 PR 并行，预计下一版本覆盖 |
| **日志页面按标签过滤** | [#23559](https://github.com/BerriAI/litellm/issues/23559) (已关闭，标记增强) | 虽已关闭，功能可能已合并至新 UI |

**路线图信号**：项目重心正在从 Python 接口层向上迁移至 Rust 内核，同时 UI 现代化（shadcn）和计费/预算体系完备性是短期冲刺方向。

---

## 7. 用户反馈摘要

从今日活跃 Issue 评论中提炼：

1. **用量/计费痛点**：多位用户反映流中断导致用量丢失、缓存成本字段为空、Bedrock 计费歧义，影响生产账单。@jasonpnnl 称“创造计费缺口、配额跟踪不完整”。
2. **Claude 工具调用损坏**：@tapir 表示 “Roo Code 和 Kilo Code 完全无法使用”，说明集成工具链依赖严重。
3. **预算绕过**：@FenterChen 报告 Redis 计数器过期后预算可被绕过，引发安全担忧。
4. **UI 可用性**：多位用户指出创建/编辑键时预算字段无法正确设置（#33253, #34294 等），管理员无法完成简单操作。
5. **Rust 迁移期待**：用户 @ishaan-berri 提交 Issue 并发布博客，社区 14 个点赞显示对性能改善的强烈需求。

**满意点**：修复 PR 跟进速度快（如 #34307 当日即提供修复），团队对关键 bug 响应积极。

---

## 8. 待处理积压

以下 Issue/PR 长期未获维护者响应，需引起注意：

| 项目 | 链接 | 状态 | 距上次更新 |
|------|------|------|------------|
| **Rust 迁移主 Issue** | [#31263](https://github.com/BerriAI/litellm/issues/31263) | 开放 | 2026-07-22 (活跃讨论) |
| **流失量数据丢失** | [#14457](https://github.com/BerriAI/litellm/issues/14457) | 开放 | 2026-07-22 (去年 9 月提出，仍无 fix PR) |
| **Claude 工具调用损坏** | [#19858](https://github.com/BerriAI/litellm/issues/19858) | 开放 | 2026-07-22 (今年 1 月提出，已标记 stale) |
| **AdaptiveRouter 重启崩溃** | [#29397](https://github.com/BerriAI/litellm/issues/29397) | 开放 | 2026-07-22 (6 周前提出，无 fix PR) |
| **Redis 缓存设置忽略环境变量** | [#26233](https://github.com/BerriAI/litellm/issues/26233) | 开放 | 2026-07-22 (3 个月前提出) |
| **PR: 添加 Azure passwordless 数据存储认证** | [#30633](https://github.com/BerriAI/litellm/pull/30633) | 开放 | 2026-06-17 (停更 36 天，急需评审) |

**提醒**：上述 Issue 涉及计费丢失、稳定性崩溃、核心模型兼容性，建议维护者优先分配资源，避免社区信任度下降。

---

> **日报生成时间**：2026-07-23 05:00 UTC  
> **数据源**：GitHub BerriAI/litellm 实时 API  
> **分析师**：AI 智能体（开源项目分析助手）

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 — 2026-07-23

## 1. 今日速览

- **Issues** 活跃度极低：过去24小时无新议题、无关闭。社区反馈环节近乎静默。  
- **PR** 活跃度较高：共处理64条，其中25条已合并/关闭，39条仍在审查。核心开发集中在 **CHASM Nexus 操作**、**Standalone Activity (SAA) 功能对等**、**Virtual Time Skipping (VTS)** 以及 **Scheduler 稳定性** 上。  
- **版本发布**：无。  
- **健康度评估**：工程推进强劲，但用户侧参与度不足，建议关注 Issues 渠道的冷启动。

## 2. 版本发布

无

## 3. 项目进展

今日合并/关闭的 PR 中，对项目主线有实际推进的包括：

- **[#11221] Fix flaky partition scaling functional tests**  
  修复分区缩放测试的偶发失败，通过调整 `ShrinkRatio` 和 `ShrinkDelta` 确保场景可靠性。  
  → [PR链接](https://github.com/temporalio/temporal/pull/11221)

- **[#11218] Disable standalone activity start delay dynamic config default value**  
  将 SAA 启动延迟动态配置默认值重设为关闭状态，直到正式 GA 再启用。  
  → [PR链接](https://github.com/temporalio/temporal/pull/11218)

- **[#11217] Fix standalone activity token validation during rolling upgrades**  
  修复混合版本滚动升级中 standalone activity 任务令牌验证问题，保证兼容性。  
  → [PR链接](https://github.com/temporalio/temporal/pull/11217)

- **[#11215] Fix PostgreSQL test database teardown with active connections**  
  增强测试数据库清理逻辑，强制终止残留连接后再删除库，提高 CI 稳定性。  
  → [PR链接](https://github.com/temporalio/temporal/pull/11215)

- **[#11132] Dynamic partitioning: refactor client**  
  重构匹配客户端，简化分区解析与转发逻辑，无功能性破坏，但为后续优化奠定基础。  
  → [PR链接](https://github.com/temporalio/temporal/pull/11132)

- **[#11201] [Scheduler] Cap V2 RecentActions in Memo at 5 items**  
  将 V2 调度器 Memo 中记录的动作数限制为 5（与 V1 一致），避免可视化存储膨胀。  
  → [PR链接](https://github.com/temporalio/temporal/pull/11201)

- **[#11028] Add run fallback to CHASM Nexus operation completion**  
  完善 CHASM 异步 Nexus 操作完成的跨运行回退机制，实现与 HSM 完成处理器的功能对等。  
  → [PR链接](https://github.com/temporalio/temporal/pull/11028)

**小结**：Standalone Activity 功能进入稳定化阶段，多个修复/配置调整合并；CHASM Nexus 继续填补功能缺口；Scheduler 和分区测试的可靠性得到增强。项目整体向前迈进约 **7 个关键修复/功能点**。

## 4. 社区热点

今日虽无高评论量议题，但以下 PR 涉及核心架构变更，值得关注：

- **CHASM Nexus 操作系列**（#10950、#11035、#11139）  
  持续推动 Nexus 操作的 CHASM 实现，包括百分比灰度、令牌转换、测试覆盖。表明 Temporal 团队正在将 Nexus 能力从 HSM 向新架构 CHASM 迁移，可能影响未来部署配置。  
  → #10950: [PR链接](https://github.com/temporalio/temporal/pull/10950)  
  → #11035: [PR链接](https://github.com/temporalio/temporal/pull/11035)  
  → #11139: [PR链接](https://github.com/temporalio/temporal/pull/11139)

- **Virtual Time Skipping (VTS)**（#11223、#11220）  
  新增轮询超时、最大跳过次数、描述接口等，为工作流时间操纵提供更细粒度控制。这一功能面向测试/调试场景，有望提升开发体验。  
  → #11223: [PR链接](https://github.com/temporalio/temporal/pull/11223)  
  → #11220: [PR链接](https://github.com/temporalio/temporal/pull/11220)

- **SAA 功能对等**（#11199、#11191、#11214、#11216）  
  多项 PR 分别解决 SAA 手动完成、暂停时重试预算耗尽、更新重试策略丢失 `non_retryable_error_types` 等问题，体现对独立活动完整性的重视。  
  → #11199: [PR链接](https://github.com/temporalio/temporal/pull/11199)  
  → #11191: [PR链接](https://github.com/temporalio/temporal/pull/11191)

**分析**：社区目前聚焦于“功能对等”与“架构迁移”，未出现激烈讨论，但功能密度高。建议维护者主动在 Issues 中征求反馈，避免闭门造车。

## 5. Bug 与稳定性

### 已修复（严重级别中等）
| 问题 | 严重性 | 状态 | 说明 |
|------|--------|------|------|
| 分区缩放测试不稳定 | 中 | 已合并 #11221 | 测试环境偶发失败，通过调参彻底修复 |
| PostgreSQL 测试库清理失败 | 中 | 已合并 #11215 | 残留活动连接导致测试数据库删除失败，CI 反复重试 |
| 滚动升级中 SAA 令牌验证 | 高 | 已合并 #11217 | 混合版本下令牌验证错误，可能导致任务丢死 |
| Standalone Activity 默认延迟配置导致未预期行为 | 低 | 已合并 #11218 | 回滚默认值，避免 GA 前意外启用 |

### 待修复（未合并）
- **WFA 重试策略更新丢失字段**（#11214）  
  问题描述：通过 `UpdateActivityOptions`/`UpdateActivityExecutionOptions` 更新重试策略时，`NonRetryableErrorTypes` 被丢弃。  
  → [PR链接](https://github.com/temporalio/temporal/pull/11214) 当前为 OPEN 状态。

- **暂停期间重试预算耗尽未正确终止 WFA**（#11191）  
  问题描述：WFA 在暂停状态下最后重试未正确终止，导致活动状态不收敛。  
  → [PR链接](https://github.com/temporalio/temporal/pull/11191) 当前为 OPEN 状态。

**建议**：上述两个 Bug 均与 Standalone Activity 用户体验直接相关，建议加速评审合并。

## 6. 功能请求与路线图信号

从今日 PR 可识别出以下路线图重点：

- **CHASM Nexus 操作百分比灰度**（#10950）  
  新增 `nexusoperation.chasmWorkflowOperationsRolloutPercentage` 动态配置，允许命名空间级别灰度 CHASM。预计纳入下一正式版本。

- **Scheduler V1 版本钳制**（#10817）  
  引入 `worker.schedulerV1VersionCeiling`，用于限制 V1 调度器工作流的版本，以支持向后兼容。这是一项长期兼容性设计。

- **VTS 完善**（#11223、#11220）  
  包括轮询完成、最大跳过次数、描述接口。属于之前发布的 VTS 功能的补全，可能成为 2.1 或 2.2 的一部分。

- **Standalone Activity Operator Commands 开关**（#11216）  
  新增 `history.enableStandaloneActivityOperatorCommands`（默认 false），为后续 Operator 命令提供安全开关。

- **Backfill 资源预留**（#11161）  
  解决 Scheduler backfill 时因缓冲区分配不均导致的进度停滞问题，提升大规模调度可靠性。

**判断**：以上功能均非破坏性变更，预计随下一个 Minor 版本发布。其中 CHASM 灰度、VTS 可能影响用户生产运维方式，官方建议提前关注文档预告。

## 7. 用户反馈摘要

**今日无新增用户 Issues**，因此无直接用户反馈可提炼。但从 PR 描述可间接看出：

- 用户/开发者对 **Standalone Activity** 的“功能对等”要求迫切，包括手动完成、暂停-重试行为、更新参数完整性等。
- **CHASM 迁移** 进度较快，但用户可能担心迁移风险，因此团队采用百分比灰度与动态配置控制。
- **测试稳定性** 依然是开发阶段的痛点，多个 PR 专门修复测试用例，暗示 CI 环境偶发失败影响了信心。

建议维护者在后续版本发布前发起社区调查，收集用户对 CHASM 和 VTS 的实际使用意愿。

## 8. 待处理积压

以下 Issue/PR 创建较早且仍处于开放状态，需提醒维护者关注：

- **[#10817] add workflow version clamp to the V1 scheduler's recorded version**  
  创建于 2026-06-23，已超过 30 天未合并。功能设计较为保守，但可能影响调度器版本兼容性策略。  
  → [PR链接](https://github.com/temporalio/temporal/pull/10817)

- **[#10950] Add intra-namespace percentage rollout for CHASM Nexus operation creation**  
  创建于 2026-07-07，涉及灰度方案，虽持续有更新但尚未合并。若纳入下一个迭代应加速评审。  
  → [PR链接](https://github.com/temporalio/temporal/pull/10950)

- **[#11199] activity-parity: allow SAA to be manually completed by ID**  
  创建于 2026-07-21，是社区关注的 SAA 功能点，目前评论数为 0，可能缺乏 reviewer 关注。  
  → [PR链接](https://github.com/temporalio/temporal/pull/11199)

**建议**：对超过 2 周未移动的开放 PR 重新分配 reviewer 或设置预期合并时间点。

---

**生成时间**：2026-07-23  
**数据来源**：GitHub – temporalio/temporal  
**分析范围**：过去 24 小时（2026-07-22 至 2026-07-23）

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*