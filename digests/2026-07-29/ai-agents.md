# OpenClaw 生态日报 2026-07-29

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-28 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 OpenClaw 项目数据，生成 2026-07-29 的项目动态日报。

---

### **OpenClaw 项目日报 | 2026 年 7 月 29 日**

**数据周期：** 2026-07-28 00:00 UTC - 2026-07-29 00:00 UTC (基于数据概览)

---

#### **1. 今日速览**

- **项目总体活跃度：极高 (🔥)。** 过去24小时内，项目维护了惊人的活动节奏，处理了 500 个 Issue 和 500 个 PR，反映了社区与核心团队的极高参与度。
- **核心焦点：稳定性与 Beta 版冲刺。** 大量高优先级（P0/P1）的 Bug 和回归问题（特别是在最新的 Beta 版本 `2026.7.2-beta.5` 中）被密集报告、讨论和修复，表明团队正在全力打磨 `2026.7.2` 稳定版。
- **发布新 Beta 版。** 发布了 `v2026.7.2-beta.5`，重点强化了数据持久化与状态安全，这是一个对生产环境至关重要的更新。
- **修复进展迅速。** 针对多个严重问题（如 Web UI/终端会话不同步、Gateway 内存泄漏、子代理交付问题）的修复 PR 已被提交或在当天关闭，显示了高效的问题响应和闭环能力。

#### **2. 版本发布: v2026.7.2-beta.5**

- **发布时间:** 2026-07-28
- **核心更新: 状态安全与恢复 (State safety and recovery)**
  - **隔离存储 (Quarantine Store):** 引入了“隔离存储”机制，用于保护持久化数据免受主数据库损坏的影响。这是一项关键的企业级特性，可防止因单点故障导致数据全损。
  - **崩溃可恢复的快照 (Crash-recoverable SQLite snapshots):** SQLite 快照现在具备崩溃恢复能力，提高了数据写入的健壮性。
  - **崩溃持久化的文件发布 (Crash-durable filesystem publication):** 文件系统发布操作也增强了持久化保证。
  - **升级保护 (Schema-upgrade data-loss rejection):** 拒绝可能导致数据丢失的 Schema 升级，防止因版本不兼容而意外损毁数据。
  - **回滚保护 (Rollback-writer snapshot recovery):** 支持通过回滚写入器快照进行恢复，为用户提供了兜底方案。
- **破坏性变更/迁移注意:** 该版本未提及明确的破坏性变更，但强烈建议所有 Beta 测试者在升级前备份关键状态。新增的“隔离存储”等机制可能需要用户关注其存储路径和资源占用。

#### **3. 项目进展**

- **核心架构统一:** **PR #115429** (合并中) 修复了 Web UI 和终端终端共享同一个聊天会话时状态不一致的问题，这是一项核心体验的修复，解决了历史记录、回复、隐私等多个痛点。
- **关键 Bug 修复:**
  - **PR #115427** (已关闭) 修复了无效插件安装可能过早占用生命周期的漏洞，提高了插件管理的健壮性。
  - **PR #115416 / #115417** (已关闭) 清理了过时的进程取消路径和重复的 Cron 关闭路径（技术债务清理），提升了代码质量和 Gateway 稳定性。
  - **PR #115327** (合并中) 修复了 `agent exec --json` 命令输出被诊断日志污染的问题，对自动化脚本用户至关重要。
- **新功能推进:**
  - **PR #115323** (合并中) 新增了 `memory.list` RPC 方法，允许客户端应用枚举 Agent 持久化到记忆中的内容。这是实现记忆管理 UI 的基础。
  - **PR #115419** (已关闭) 在 Control UI 中增加了“记忆搜索”标签，将新 RPC 转化为用户可见的功能，填补了 Agent 记忆管理的关键空白。
  - **PR #115425** (合并中) 修复了 Control UI 中 Provider 排序问题，确保用户看到的模型顺序是经过排名优化的。

#### **4. 社区热点**

今日社区讨论高度集中于**稳定性、安全性和特定通道的故障**问题。

- **🔥 [Issue #75: Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)**
  - **热度:** 115 条评论，80 👍
  - **分析:** 这是社区最强烈的呼声之一。尽管框架在 macOS/iOS/Android 已有原生应用，但 Linux 和 Windows 用户长期无法获得同等体验。这已成为一个影响用户基础和生态扩展的关键诉求。

- **⚠️ [Issue #91588: Gateway 内存泄漏](https://github.com/openclaw/openclaw/issues/91588)**
  - **热度:** 20 条评论，P0 优先级
  - **分析:** 进程内存从 350MB 暴涨至 15.5GB 并导致 OOM 崩溃，这是一个严重的稳定性回归。社区表达了强烈不满，因为该问题会彻底中断服务。作为 *铂金级*、P0 问题，它毫无疑问是开发团队当前的核心关注点。

- **🔑 [Issue #10659: 掩码秘密 (Masked Secrets)](https://github.com/openclaw/openclaw/issues/10659)**
  - **热度:** 14 条评论，4 👍
  - **分析:** 社区不仅关心功能，也开始重视安全。该请求要求 Agent 只能“使用”API Key 而无法“读取”API Key，以防范提示注入攻击。这反映出用户对开放 Agent 安全性的深层担忧。

#### **5. Bug 与稳定性**

以下为今日报告或活跃的、按严重性排列的高影响问题：

- **P0 (致命):**
  - **[Issue #91588] 网关内存泄漏 (OOM 崩溃):** RSS 增长至 15.5GB 导致进程反复崩溃。**当前无 Fix PR**，是最高优待解决问题。
  - **[Issue #114895] 编辑非 UTF-8 文件时静默数据损坏:** `edit`/`apply_patch` 工具会静默地将非 UTF-8 字节替换为 UTF-8 字节，导致文件被无声损坏。**已关闭**，应已有修复。

- **P1 (严重):**
  - **[Issue #113434] Codex 会话 ID 复用导致内存耗尽:** 在 `2026.7.2-beta.4` 中出现，会话 ID 复用导致扫描操作耗尽 RAM。**当前无 Fix PR。**
  - **[Issue #115326] Crash-loop 断路器永久抑制 Discord/WhatsApp:** 文档中提到的恢复方法失败，导致通道被永久上锁。**当前无 Fix PR。**
  - **[Issue #115001] 混合记忆搜索返回虚假的高分结果:** 搜索相关性算法缺陷，返回错误的匹配内容。**当前无 Fix PR。**
  - **[Issue #102755] 项目在 Windows/WSL 上启动挂起:** 二次构建时挂起，开发者标记为“Beta release blocker”。**当前无 Fix PR。**

- **P2 (中等 - 包含多个回归):**
  - **[Issue #74378] Windows 上 CLI 进程残留:** `openclaw version` 等命令执行后，`node.exe` 进程不被终止。**当前无 Fix PR。**
  - **[Issue #108075] Provider 拒绝请求 Schema:** `2026.7.1` 版本回归，请求被 LLM Provider 拒绝。**已关闭。**
  - **[Issue #111519] Telegram DM 回复丢失/滞后:** `2026.7.2-beta.3` 回归，DM 回复无法实时送达。**当前无 Fix PR。**

#### **6. 功能请求与路线图信号**

- **下一代安全策略:**
  - **[Issue #10659]: 掩码秘密 (Masked Secrets)** — 社区对 Agent 安全提出了更高要求。
  - **[Issue #6615]: exec-approvals 添加黑名单支持** — 社区希望有更灵活的“除了X之外都允许”策略。
  - **[Issue #7722]: 文件系统沙箱配置** — 需求文档十分详细，社区强烈希望限制 Agent 的文件系统访问范围。
  - **[Feature #39979]: 基于路径的 RWX 权限** — 这是一个更彻底的方案，目标是用类似 Unix DAC 的权限模型替换当前的二值化 exec 白名单。**此功能与 PR #104681 (权限系统重构) 有显著关联，预示着下一代安全模型正在开发中。**

- **Agent 能力增强:**
  - **[Issue #9986]: 触发上下文溢出时的模型回退** — 用户期望当主模型上下文耗尽时能自动切换到备用模型，而不是报错。
  - **[Issue #6757]: Agent 触发的自压缩工具** — Agent 感觉上下文过长时能主动请求压缩，而不是被动依赖用户指令。
  - **[Issue #8355]: 语音通话的流式 TTS 管道** — 用户期望实时合成语音，而不是等待完整响应。
  - **[Issue #10687]: 动态模型发现** — 用户希望 OpenClaw 能自动发现 OpenRouter 等平台的新模型，无需手动更新目录。

#### **7. 用户反馈摘要**

- **对核心能力的肯定:** 尽管问题众多，仍有用户（如 *Reneb-cafe* 在 Issue #73537 中）表达了感谢，称 OpenClaw 已成为家庭和业务助手的核心。这反映了项目对早期用户的巨大价值。
- **对稳定性的焦虑:** 大量用户因内测版本的频繁崩溃和数据问题感到沮丧。*petercheng*（#91588）和 *virtualwolfnz*（#113434）等用户报告的问题直接导致了服务中断。用户*robingutsche*（#115326）报告了官方恢复文档都无效的情况，加剧了不信任感。
- **对 Linux/Windows 支持的渴望:** Issue #75 的超高评论和点赞数证明了这是社区最大、最普遍的痛点。
- **迭代频率压力:** 从用户报告的版本号（如 `v2026.5.5`, `v2026.6.10`, `v2026.7.2-beta.4`）可以看出迭代速度极快。这对积极部署的用户意味着需要频繁应对升级带来的回归问题。

#### **8. 待处理积压**

- **[Issue #73537] 为发布版本添加生产就绪标签:** 由用户 *Reneb-cafe* 提出，该 Issue 已表明稳定版和测试版界限模糊是社区的主要痛点。虽然标签看似简单，但其背后代表着发布流程和版本管理策略的重大改进。
- **[Issue #74378] Windows 上 CLI 进程残留:** 一个长期存在且影响 Windows 用户基础体验的 P2 Bug，评论数不多但影响范围广，未被当前“修复浪潮”覆盖。
- **[Issue #10687] 动态模型发现:** 随着 LLM 模型更新速度加快，此功能请求的评论数不多，但代表了项目的长期演进方向，可能会随着 OpenRouter 等平台的流行而重要性提升。

---

## 横向生态对比

好的，作为专注于 AI 智能体与个人 AI 助手开源生态的资深技术分析师，我已根据您提供的五个核心项目在 2026 年 7 月 29 日的社区动态，为您整理出以下横向对比分析报告。

---

### **个人 AI 智能体开源生态横向对比分析报告 (2026-07-29)**

**报告日期：** 2026 年 7 月 29 日
**分析对象：** OpenClaw, Hermes Agent, OpenHands SDK, Pi, LiteLLM, Temporal

---

#### **1. 生态全景**

当前，个人 AI 智能体与自主智能体开源生态正处于 **“大规模工程化冲刺”** 阶段。项目不再聚焦于概念验证，而是全力解决 **企业级部署、生产稳定性、跨平台体验和安全性** 等痛点。一方面，以 OpenClaw 和 LiteLLM 为代表的基础设施层项目在狂热修复 Bug、发布密集版本，打磨产品健壮性；另一方面，以 Hermes Agent 和 Pi 为代表的客户端项目则积极探索新平台集成与用户体验，而 Temporal 作为底层工作流引擎，正通过重构（CHASM）和功能增强为上层智能体的复杂编排提供更坚实的基础。**社区的共同焦虑点已从“如何实现”转向“如何用好且不出错”**。

#### **2. 各项目活跃度对比**

| 项目名称 | 周期内 Issue 更新数 | 周期内 PR 活动数 | 新版本发布 | 项目健康度评估 | 活跃度评级 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 | 500 | `v2026.7.2-beta.5` | **极高** (🔥)，但面临严重的稳定性危机和社区信任挑战 | 🔥 危机式活跃 |
| **LiteLLM** | 78 | 253 | `v1.94.0` | **高**，PR 提交远高于合并，功能迭代速度快，但积压问题多 | 🚀 高速迭代 |
| **Hermes Agent** | 500 | 500 | 无 | **高**，社区活跃，桌面端修复取得进展，但维护压力巨大 | 🚀 活跃开发 |
| **Pi** | 73 (18新开) | 25 | 无 | **良好**，Bug 修复与兼容性提升扎实，社区讨论有深度 | ✅ 稳健推进 |
| **Temporal** | 未明确(热点2条) | 49 | 无 | **优秀**，PR 活动密集，核心架构（CHASM）推进稳健，方向清晰 | ✅ 高质量开发 |
| **OpenHands SDK** | 21 | 50 | `v1.38.0` | **良好**，发布新版本，注重安全与治理，建设性社区反馈 | ✅ 稳健发展 |

#### **3. OpenClaw 在生态中的定位**

与同类项目相比，OpenClaw 定位于 **全能型个人 AI 助手框架**，试图提供从底层智能体到上层原生应用的完整体验。

- **优势：**
    - **生态广度：** 拥有 macOS/iOS/Android 原生应用，覆盖移动和桌面场景（尽管 Linux/Windows 缺失是最大软肋）。
    - **功能深度：** 强大的 Provider 集成、插件系统和丰富的工具链（如记忆、RPC 等），功能完整性远超单一客户端。
    - **社区规模：** 极高的 Issue 和 PR 活跃度表明其社区规模巨大，用户基础广泛。
- **技术路线差异：**
    - 相较于 **Hermes Agent** 和 **Pi**（更侧重客户端体验），OpenClaw 更**高度耦合全栈**，试图自成生态。这带来了集成问题（如 Gateway 内存泄漏）和发布压力。
    - 相较于 **LiteLLM**（专注 API 网关与模型路由），OpenClaw 是**所有功能的“综合体”**，复杂度更高，稳定性更易受影响。
    - 相较于 **OpenHands SDK**（专注 Agent 行为治理的 SDK），OpenClaw 是一个**成熟的“开箱即用”产品**，但缺乏企业级安全治理抽象层。
- **社区规模对比：** OpenClaw 的社区活跃度（Issue/PR 双 500）远超其他项目，但其健康度评估为“危机式活跃”，说明其规模带来的 Bug 反馈压力巨大，维护团队可能处于**被动应对状态**。

#### **4. 共同关注的技术方向**

以下方向在多个项目中同时被提及或推进，代表行业共性需求：

1.  **企业级安全与治理（OpenClaw, Hermes Agent, OpenHands SDK, LiteLLM）**：这是最强烈的信号。具体诉求包括：
    - **细粒度权限控制 (RBAC):** Hermes Agent #527, OpenClaw #10659 (掩码秘密), #7722 (沙箱), #39979 (路径权限)。
    - **审计与成本控制:** OpenHands SDK #4273 (治理层)。
    - **预算隔离:** LiteLLM #26239 (预算记录错误)。

2.  **记忆与状态的持久化管理（OpenClaw, Hermes Agent, Pi）**：用户不再满足于简单的消息记录，能力需求明显深化：
    - **跨会话搜索与检索:** OpenClaw `memory.list` RPC, Hermes Agent #8457。
    - **自动压缩与上下文管理:** Hermes Agent #8457, OpenClaw #9986/#6757。
    - **会话状态恢复:** OpenClaw `v2026.7.2-beta.5` 核心主题，Hermes Agent #12857。

3.  **平台兼容性与跨桌面体验（OpenClaw, Hermes Agent, Pi）**：
    - **桌面端原生应用:** OpenClaw #75 (Linux/Windows App) 是社区最强烈呼声；Hermes Agent 全面修复 macOS TCC 权限问题。
    - **WSL2 支持:** Pi #7064 报告了 WSL 路径处理问题，反映 Linux/Windows 混合开发场景的痛点。
    - **SSH 远程模式:** Hermes Agent #69551 报告桌面端 SSH 模式在非默认 profile 下崩溃。

#### **5. 差异化定位分析**

| 对比维度 | OpenClaw | Hermes Agent | Pi | LiteLLM | OpenHands SDK | Temporal |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **功能侧重** | 全栈个人 AI 助手 (客户端+框架) | 跨平台桌面 AI 客户端 | 终端 AI 搭档 (TUI 优化) | LLM API 网关与路由 | Agent 行为治理 SDK (企业级) | 分布式工作流编排引擎 |
| **目标用户** | 追求一体化体验的个人/发烧友 | macOS/Linux 开发者 | 重度终端用户, WSL2 用户 | 企业 AI 应用团队, 平台工程 | 构建 Agent 平台的企业开发者 | 构建复杂工作流的开发者 |
| **技术架构** | 整体式 + 插件 | 原生客户端 (Electron?) | TUI + 扩展 | Python 中间件 | SDK/Framework | Go 核心引擎 |
| **最大风险** | 稳定性失控，版本迭代过快导致 Bug 爆炸 | 社区维护压力大，长期问题积压 | 企业级 Copilot 兼容性受阻 | 数据库迁移/计费等核心企业功能 Bug | 作为 SDK 的生态独立性和易用性 | Schedules 功能缺少灵活控制 |
| **核心卖点** | “开箱即用”的 Agent 体验 | “美且完善”的桌面 GUI | “高效且极客”的 TUI | “可靠且可扩展”的企业网关 | “安全可控”的 Agent 构建工具 | “可靠且强大”的工作流引擎 |

#### **6. 社区热度与成熟度**

- **疯狂迭代/修复期（危机感强）：** **OpenClaw**。尽管社区活跃度最高，但严重 Bug 和稳定性问题密集爆发，版本迭代速度过快，产品处于“功能驱动”向“质量驱动”的艰难转型期。
- **高速迭代/功能扩张期：** **Hermes Agent** 和 **LiteLLM**。两者社区活跃，Issue/PR 数量高，但在积极扩展功能（新平台集成、MCP OAuth）的同时，也积累了较多关键缺陷。特点是 PR 提交数远超合并数，有一定“消化不良”风险。
- **稳健推进/质量巩固期：** **Pi**、**OpenHands SDK** 和 **Temporal**。这些项目 Issue 和 PR 活动量相对可控，修复的落地率高，发展方向清晰。Temporal 展示了最优的开发质量，Pi 和 OpenHands SDK 则在扎实地解决社区反馈的具体问题。

#### **7. 值得关注的趋势信号**

1.  **“安全中间件”成为刚需：** OpenHands SDK 明确提出“治理层”概念，OpenClaw、Hermes Agent 和 LiteLLM 也从不同角度回应安全需求。这意味着未来 AI 智能体应用将需要标准化的、与平台无关的**安全与合规抽象层**，类似于 Web 开发的 API 网关或身份提供商。

2.  **从“会话”到“记忆库”的能力跃迁：** OpenClaw 推出 `memory.list` RPC，Hermes Agent 寻求“跨会话检索”，标志着智能体正在从“一次性对话”演进为**具备长期知识库和记忆管理能力的“知识体”**。这将是下一代差异化的核心。

3.  **企业级集成的“最后一公里”问题凸显：** LiteLLM 的 Claude Gateway 支持请求、Pi 的 Copilot Enterprise 兼容性问题，都表明 AI 智能体工具与企业现有的 IT 基础设施（如 SSO、计费系统、企业版 SaaS）的无缝集成，是阻碍大规模部署的关键障碍。

4.  **底层基础设施的“隐形重构”：** Temporal 的 CHASM 项目正在进行大规模架构重构，这虽不直接体现在前端，但预示着上层智能体应用的**复杂编排、大规模状态管理和持久化将迎来更健壮的基石**。对于构建高可用 Agent 系统的开发者来说，关注 Temporal 的演进是长期战略。

---
**给 AI 智能体开发者的建议：**
- **选型思考：** 若追求快速体验和社区支持，OpenClaw 是首选，但需警惕其波动性。若构建企业级平台，LiteLLM + OpenHands SDK 组合提供了一个更可控、可治理的路径。而 Pi 是 TUI 重度用户的最佳选择。
- **关注核心矛盾：** 将更多精力投入在**记忆管理、安全治理、模型路由**等通用模块上，而非从零构建基础 Agent 能力。提前规划您应用的“安全中间件”和“长期记忆存储”方案。
- **短期避险：** 在 OpenClaw 和 Hermes Agent 当前的高速迭代期，建议锁定一个相对稳定的 Beta 版本，避免跟随每日更新，以降低回归风险。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是基于 Hermes Agent (github.com/NousResearch/hermes-agent) 在 2026-07-28 至 2026-07-29 间的数据生成的每日项目动态。

---

# Hermes Agent 项目动态日报 — 2026-07-29

## 今日速览

Hermes Agent 社区在 2026 年 7 月 28 日处于**高度活跃**但**维护压力较大**的状态。过去 24 小时内，项目共产生 500 条 Issue 更新和 500 条 PR 更新，社区讨论热度极高，但待合并的 PR（353 条）与待解决的活跃 Issue（410 条）数量居高不下。当前社区讨论焦点集中在**会话状态持久性、权限管理、桌面端体验**以及**新兴平台集成（如 Buzz）** 上。虽然无新版本发布，但多个影响桌面端 macOS 用户体验的关键 Bug 的修复 PR 已成功合并，是今日最积极的进展。

## 项目进展

今日项目核心进展体现在对**macOS 桌面端体验**的持续优化上，多个修复 PR 成功合并。

### 已合并/关闭的重要 PR
- **[#73675] fix(desktop): match Edit Models row hover to the model picker**  
  **贡献者:** @OutThisLife  
  **状态:** 已合并  
  **摘要:** 修复了桌面端模型选择弹窗内，模型行缺少悬停反馈的 UI 不一致问题。  
  **链接:** https://github.com/NousResearch/hermes-agent/pull/73675

- **[#73670] fix(desktop): overlay scrollbars on conversation code blocks**  
  **贡献者:** @OutThisLife  
  **状态:** 已合并  
  **摘要:** 修复了桌面端对话代码块中滚动条样式问题，使其回归更现代的悬浮式滚动条，优化了视觉体验。  
  **链接:** https://github.com/NousResearch/hermes-agent/pull/73670

- **一系列 macOS 桌面签名与权限修复 PR**
  今日有 5 个旨在解决 macOS 桌面端 TCC 权限在更新后丢失问题的 PR 被合并。这标志着社区对一个长期困扰用户的问题发起了集中攻关并取得了成果。
  - [#38752] Preserve Developer ID signatures in Desktop relaunch fixup ( @twe-cloud )
  - [#63857] fix(installer): preserve macOS entitlements during ad-hoc re-signing ( @cipry0200 )
  - [#67357] fix: keep macOS TCC permission grants across desktop self-updates ( @gvago )
  - [#61763] fix(desktop): preserve macOS TCC identity across rebuilds ( @caseyanthony )
  - [#68853] fix(desktop): preserve macOS TCC permissions across updates ( @natebransc )

**项目评估:** 尽管合并推进了体验修复，但 353 个待合并的 PR 和 410 个活跃 Issue 反映出项目维护能力可能暂时落后于社区贡献的热情与 Bug 报告速度。项目正向提升桌面端稳定性和用户体验的方向坚实迈进。

## 社区热点

今日讨论热度最高、响应最多的议题集中于**权限管理、会话持久化和新功能集成**，反映了社区对核心能力拓展的强烈诉求。

1.  **[{Feature}] Add messenger support for Buzz** ([#68871](https://github.com/NousResearch/hermes-agent/issues/68871))
    -   **热度:** 17 条评论，16 个 👍
    -   **诉求:** 社区对集成 Block 公司新开源的工作区消息协议 **Buzz** 表现出浓厚兴趣。Buzz 允许人类与 AI 代理在同一个房间中协作，用户希望 Hermes Agent 能够原生支持加入 Buzz 工作区。
    -   **展望:** 该 Issue 标记为 `needs-decision`，显示出高社区关注度，可能成为下一阶段集成的重要候选。

2.  **[{Feature}] Gateway Permission Tiers — RBAC for Messenger** ([#527](https://github.com/NousResearch/hermes-agent/issues/527))
    -   **热度:** 16 条评论，10 个 👍
    -   **诉求:** 这是一个持续数月的长期热门议题。用户强烈要求摒弃当前的“全有或全无”的 Gateway 授权模式，引入细粒度的角色权限（如 Owner/Admin/User/Guest）。这是支持企业级多用户场景的关键需求。
    -   **展望:** 作为 P2 级别的功能请求，此需求是路线图上的重点工程。

3.  **[{Feature}] Persistent Session Memory with Cross-Session Search & Auto-Compression** ([#8457](https://github.com/NousResearch/hermes-agent/issues/8457))
    -   **热度:** 15 条评论
    -   **诉求:** 用户高度期望一项更高级的持久记忆功能。功能需求从简单的“重启后记忆不丢失”扩展到了“跨会话检索”和“自动压缩”。这显示了用户对 Agent 长期记忆能力和智能化程度的更高要求。

## Bug 与稳定性

过去 24 小时内报告的 Bug 集中在**会话管理、配置错误和平台兼容性**上。

### 严重 Bug
1.  **Desktop SSH remote mode broken with non-default profile** ([#69551](https://github.com/NousResearch/hermes-agent/issues/69551))
    -   **严重级别:** P2
    -   **描述:** 当用户切换为非默认 profile 时，桌面版的 SSH 远程模式完全失效。这是由于 `token-path` 验证路径与客户端硬编码路径不一致导致的。
    -   **状态:** 待处理。

2.  **Preflight token estimate miscounts on thinking models** ([#73298](https://github.com/NousResearch/hermes-agent/issues/73298))
    -   **严重级别:** P2
    -   **描述:** 在“思考/推理”模型（如 Kimi K3）上，自动压缩功能会在真实 token 使用量仅为阈值 27% 时就被错误触发，导致会话过早压缩。
    -   **状态:** 新报告，待处理。建议维护者关注此模型兼容性问题。

3.  **Session auto-reset discards context** ([#12857](https://github.com/NousResearch/hermes-agent/issues/12857))
    -   **严重级别:** P2
    -   **描述:** 会话重置后，尽管上下文被保存，但新会话没有继承父会话的 ID，导致新会话历史完全空白。这是一个影响会话连续性的核心 Bug。
    -   **状态:** 持续开放中，已有详细的复现步骤与分析。

### 稳定性相关问题
- **DaemonThreadPoolExecutor crashes on Python 3.14** ([#58596](https://github.com/NousResearch/hermes-agent/issues/58596)): 一个关键的兼容性 Bug，将阻塞所有并发功能，影响用户向新 Python 版本的迁移。
- **Desktop GUI: prompt.submit sends to wrong session** ([#72971](https://github.com/NousResearch/hermes-agent/issues/72971)): 用户反馈在切换会话时，消息可能被发送到错误的对话中，严重影响了桌面版的多会话体验。

## 功能请求与路线图信号

除了上述热点社区反馈，今日还有以下几类功能请求，可能暗示了未来的发展方向：
- **OpenAI 兼容图像生成:** Issue [#13798](https://github.com/NousResearch/hermes-agent/issues/13798) 要求增加通用 OpenAI 兼容的图像生成提供商，显示社区不想被单一提供商（FAL.ai）绑定，期望更高的灵活性。
- **Kanban Board 集成桌面端:** Issue [#41222](https://github.com/NousResearch/hermes-agent/issues/41222) 要求将 Kanban Board 功能直接集成到桌面应用中，以消除在 CLI 和 GUI 之间切换的障碍。该 Issue 有 15 个 👍 标记，需求旺盛。
- **Claude Agent SDK 订阅集成:** Issue [#25267](https://github.com/NousResearch/hermes-agent/issues/25267) 获得 44 个 👍 标记，是当日“点赞”榜首。用户痛点明确：已订阅 Claude 的用户不愿意为了使用 Hermes 而再支付 API 费用。

**结合 PR 预判:** 今日有一项旨在支持多 Telegram 账户的 PR [#67455](https://github.com/NousResearch/hermes-agent/pull/67455) 处于开放状态，并且长期 feature PR [#27208](https://github.com/NousResearch/hermes-agent/pull/27208)（添加 `agent_loop_stopped` 插件钩子）仍在等待合并决策。这预示着插件系统和多平台账户管理将是接下来的迭代重点。

## 用户反馈摘要

从热门 Issue 和评论中可以提炼出用户的几个核心痛点和使用场景：
- **反馈痛点:**
  - **“我已经付费了”**: 使用 Claude 订阅的用户对二次付费感到困扰（#25267），希望 Hermes 能利用其现有订阅。
  - **“设置复杂，改啥坏啥”**: macOS 用户对更新后所有权限丢失的体验感到沮丧，虽然有修复 PR，但问题已衍变为多个重复 Issue（见已合并 PR 列表）。
  - **“不知道自己是谁”**: 细粒度权限管理的缺失（#527）让拥有多用户场景的用户感到不安和不便。
- **反馈期望:**
  - 用户不仅希望 Agent 有记忆，还希望**能检索**和**自动总结**（#8457）。
  - 用户期望**低摩擦、体验一致**的跨平台使用体验，例如桌面、CLI 与 Kanban 板的无缝衔接（#41222）。
  - 社区对**开源生态集成**表现出开放性，例如对 Buzz 项目（#68871）的快速响应。

## 待处理积压

以下为长期未得到回应或解决的关键 Issue，建议维护团队优先审阅：
- **#527** (Feature: Gateway Permission Tiers — RBAC): 自 3 月起开放，至今未合入任何相关 PR，是社区反馈最强烈的长期诉求之一。
- **#8457** (Feature: Persistent Session Memory): 自 4 月开放，代表了用户对 Agent“记忆”这一核心能力的进阶期望。
- **#25267** (Feature: Claude Agent SDK model provider): 自 5 月开放，拥有社区最高点赞数，涉及商业模式和用户体验的痛点，其决策将影响大量 Claude 用户。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

好的，以下是为您生成的 OpenHands SDK 项目动态日报。

---

# OpenHands SDK 项目日报 - 2026-07-29

## 今日速览

今日项目整体活跃度很高，共处理了21条 Issue 和50条 PR。核心亮点是发布了 v1.38.0 版本，重点更新了 LLM 操作摘要展示和 Agent 设置架构。社区讨论集中在企业级治理功能、关键 Bug 修复以及安全性增强上。尽管 PR 合并率较低（8/50），但项目在架构优化和功能扩展方面表现出了强劲的发展势头，代码库的健康度与创新性均处于高位。

## 版本发布

- **[v1.38.0]** 于今日发布。该版本包含两项关键更新：
    - **功能增强**: 在确认预览中增加了 LLM 操作摘要的展示 ([PR #4218](https://github.com/OpenHands/software-agent-sdk/pull/4218))，提升了用户对 Agent 行为的可视化理解。
    - **架构演进**: 在 agent-settings 的 schema 中公开了 `agent_context.load_memory` 接口 ([PR #4205](https://github.com/OpenHands/software-agent-sdk/pull/4205))，这为后续更精细的 Agent 状态管理和定制化行为控制铺平了道路。
    - **迁移注意事项**: 本次发布无重大破坏性变更，但开发者若使用了自定义的 `agent-settings`，可能需要检查是否兼容新引入的 `load_memory` 字段。

## 项目进展

今日，项目在安全性、开发者体验和稳定性方面取得了实质性的整合进展。主要亮点包括：
- **安全性增强**: 通过引入 [PR #4282](https://github.com/OpenHands/software-agent-sdk/pull/4282)（修复 VSCode URL 中未经验证的工作区路径）和持续推进 [PR #3944](https://github.com/OpenHands/software-agent-sdk/pull/3944)（基于 AST 的 shell 命令解析），项目的安全边界得到了加强。
- **开发者体验优化**: [PR #4295](https://github.com/OpenHands/software-agent-sdk/pull/4295) 测试了拒绝持久化设置的未版本化形状更改，这有助于防止配置回滚问题，增强了稳定性。
- **服务端能力增强**: [PR #4294](https://github.com/OpenHands/software-agent-sdk/pull/4294) 新增了 MCP 设置的 CRUD 端点，为更完善的 Agent Server API 管理奠定了基础。
- **基础设施维护**: 合并了 [PR #3951](https://github.com/OpenHands/software-agent-sdk/pull/3951)，对集成测试跟踪器进行了轮转，避免了 GitHub Issue 页面因评论过多而无法打开的尴尬，维护了社区沟通渠道的顺畅。

## 社区热点

今日社区讨论热度较高，主要围绕几个关键议题：

1.  **企业级治理与安全性**：
    - **[Issue #4273 - Feature: 治理层]** 引发了广泛讨论。该提案要求为 agent 行为添加文件访问控制、命令白名单、成本预算和结构化审计证据。这表明随着项目向企业级部署迈进，用户对安全、合规和可审计性的需求变得非常迫切。这将是项目下一阶段发展的核心方向之一。
    - **[Issue #4288 - Design: 引用凭证和安全的运行时交付]** 作为一份架构设计文档被提出，讨论了在运行时安全地传递凭证的问题。这直接关系到企业用户的数据安全和合规要求。

2.  **关键 Bug 修复需求**：
    - **[Issue #4248 - Bug: execute_bash 缺少参数 'security_risk']** 该问题报告了与 DeepSeek 模型交互时，`execute_bash` 函数因缺少参数而报错。这可能是由于模型返回的安全风险评估与 SDK 预期不匹配导致的，影响了特定模型（如 deepseek-reasoner）的正常使用。
    - **[Issue #4255 - Bug: Ollama 5分钟超时]** 和 **[Issue #4256 - Bug: Docker 容器中 Chromium 启动失败]** 分别反映了用户在本地开发和云端部署时遇到的具体障碍，表明在不同环境下的一致性和可靠性仍有改进空间。

3.  **功能性诉求**:
    - **[Issue #4293 - Enhancement: 添加原子 MCP 服务器创建、修补和删除端点]** 和 [#4292 - Enhancement: 1小时缓存 TTL](#) 反映了社区对更精细、更强大的 API 和性能优化方案的持续追求。

## Bug 与稳定性

今日报告的 Bug 按严重程度排列如下：

- **高优先级（HIGH）**:
    - **[Issue #4208] check-pr-artifacts 工作流错误**: `.pr/` 目录意外侵入主分支，且工作流在 fork 的 PR 上因 403 错误硬性失败。这对 CI/CD 流程有直接影响。
    - **已有修复 PR**: 暂无直接关联的修复 PR。但该问题的提出本身已构成警告。
- **中优先级（MEDIUM）**:
    - **[Issue #4248] execute_bash 缺少参数**: 影响特定模型的使用，属于功能阻断性 Bug。
        - **修复状态**: 暂无关联 PR。
    - **[Issue #4255] Ollama 5分钟超时**: UI 和设置文件中的超时配置不生效，影响用户体验。
        - **修复状态**: 暂无关联 PR。
    - **[Issue #4285] (自动化测试) 会话重试过早停止**: 这是一个由 Bot 创建的测试 Issue，用于验证[问题分类自动化流程](#)。但其描述指出了 SDK 在处理短暂网络错误时的一个真实逻辑缺陷。
- **低优先级（LOW）**:
    - **[Issue #4286]** 测试 Bug。
    - **[Issue #3753] browser-use 与 iframe 的兼容性问题** 仍然处于开放状态，可能影响复杂的网页抓取和自动化场景。
    - **[Issue #4253] WebApp 浏览器功能断裂** 影响了开发者测试自身应用的能力。

## 功能请求与路线图信号

用户提出的新功能请求显示出清晰的企业级需求和性能优化倾向，这些很可能会被纳入下一版本的考虑范围：

- **核心架构（高优先级）**:
    - **[Issue #4273] 治理层**: 该项目是企业级部署的基石，势在必行。
    - **[Issue #4288] 引用凭证设计**: 该设计文档的提出，表明核心团队已经开始着手解决身份验证和安全凭证管理的架构问题。
- **API 增强**:
    - **[Issue #4293] 原子 MCP 端点**: 与已提交的 [PR #4294](https://github.com/OpenHands/software-agent-sdk/pull/4294)（MCP 设置 CRUD）直接对应，预计将很快实现并集成。
- **性能优化**:
    - **[Issue #4292] 1小时缓存 TTL**: 用户希望突破当前5分钟的硬编码限制，以获得更好的 LLM 调用性能。这为项目提供了明确的性能优化方向。

## 用户反馈摘要

从今日的 Issues 互动中，可以提炼出以下真实的用户痛点和使用场景：

1.  **企业部署的困境**: 多位用户提到了在企业共享基础设施、受监管行业或多租户平台中部署时的担忧。
    > `Issue #4273` 提出者描述道：“当在企业环境（共享开发基础设施、受监管行业、多租户平台）中部署 OpenHands 时，自动化... 存在风险。”
2.  **特定配置的挫败感**: 用户报告了尝试自定义超时或连接本地模型（如 Ollama）时的失败体验。
    > `Issue #4255` 用户抱怨：“更改 UI 或 `settings.json` 中的超时无效。” 这表明配置系统的健壮性和一致性有待提高。
3.  **开发工作流的阻碍**: 开发者指出，内置的 WebApp 和浏览器功能存在问题，阻碍了他们正常的软件开发测试流程。
    > `Issue #4253` 用户直言：“WebApp 开发要求你在浏览器中检查应用的真是行为。目前…非常不稳定。”

## 待处理积压

以下为长期未响应或对项目健康度有潜在影响的重要 Issue/PR，提请维护者关注：

1.  **[Issue #4248] - execute_bash 缺少参数**: 该问题已存在3个月，且由不同用户持续讨论，影响特定 LLM 模型的可用性，建议优先处理。
    - [链接](https://github.com/OpenHands/software-agent-sdk/issues/4248)
2.  **[Issue #2053] - Skills Epic**: 作为一项功能增强的史诗级 Issue，自2月以来一直开放，虽然状态标记为“陈旧的”，但其描述的“技能执行隔离、模型路由和增强能力”是项目长期路线图中的关键组成部分，需要持续规划和推进。
    - [链接](https://github.com/OpenHands/software-agent-sdk/issues/2053)
3.  **高评论量的 Issue**:
    - **[#2078](https://github.com/OpenHands/software-agent-sdk/issues/2078)**: 拥有152条评论，虽为追踪Issue，但评论数之高反映了社区对集成运行状况的密切关注。建议维护者关注其内部讨论，或许有可提取的共性反馈。
    - **[#3950](https://github.com/OpenHands/software-agent-sdk/issues/3950)**: 同样作为示例运行的追踪Issue，15条评论也值得快速审视。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目日报 (2026-07-29)

---

## 1. 今日速览

过去24小时内，Pi 项目保持高活跃度：共处理 **73 条 Issue**（其中新开/活跃 18 条，关闭 55 条），**25 条 PR**（其中已合并/关闭 18 条，待合并 7 条）。无新版本发布。社区讨论集中在 **Copilot Enterprise 兼容性、WSL 路径处理、UI 重绘性能** 等关键问题。代码库方面，多个重要的 bug 修复（Undici 升级、Kimi K3 支持、Z.AI max_tokens 修复）已完成合并，项目稳定性与兼容性稳步提升。

---

## 2. 版本发布

无新版本发布（最新 Release 为之前版本，今日无变动）。

---

## 3. 项目进展

今日合并/关闭的重要 PR 及对应的功能推进：

| PR | 描述 | 状态 | 推进内容 |
|---|---|---|---|
| [#7218](https://github.com/earendil-works/pi/pull/7218) | fix(coding-agent): preserve resource metadata after extension resource reloads | ✅ 已合并 | 修复扩展资源重载后元数据丢失问题 |
| [#7240](https://github.com/earendil-works/pi/pull/7240) | feat(ai): add Apiário as built-in provider | ✅ 已合并 | 新增巴西聚合 API 提供商 Apiário，支持 BRL 结算 |
| [#7236](https://github.com/earendil-works/pi/pull/7236) | feat(tui): pin chat input and support mouse caret | ✅ 已合并 | TUI 输入栏固定、鼠标光标支持、视图同步改进 |
| [#7230](https://github.com/earendil-works/pi/pull/7230) | fix(ai): route Fireworks Kimi K3 through openai-completions | ✅ 已合并 | 解决 Kimi K3 模型在 Fireworks 上不可选的问题 |
| [#7225](https://github.com/earendil-works/pi/pull/7225) | fix: update undici from 8.5.0 to 8.8.0 | ✅ 已合并 | 修复 HTTP_PROXY 环境变量被忽略的问题 |
| [#7206](https://github.com/earendil-works/pi/pull/7206) | fix(coding-agent): build-check-test | ✅ 已合并 | 修复 npm run check 构建错误 |
| [#7210](https://github.com/earendil-works/pi/pull/7210) | fix(coding-agent): clean up failed git installs | ✅ 已合并 | 清理安装失败时的残留文件 |
| [#7211](https://github.com/earendil-works/pi/pull/7211) | fix(coding-agent): reset model selector selection to top row when filtering | ✅ 已合并 | 修复模型选择器筛选时高亮不归位的问题 |
| [#7214](https://github.com/earendil-works/pi/pull/7214) | fix: rpc bash no longer bypass user_bash | ✅ 已合并 | 修复 RPC 模式 bash 绕过 user_bash 扩展钩子的问题 |
| [#7215](https://github.com/earendil-works/pi/pull/7215) | fix(coding-agent): include scoped models in TUI extension context | ✅ 已合并 | 修复 CI 构建中的 TS 类型错误 |
| [#7174](https://github.com/earendil-works/pi/pull/7174) | fix(ai): send max_tokens for Z.AI providers | ✅ 已合并 | 修复 Z.AI 忽略 max_completion_tokens 导致长推理被截断 |
| [#7224](https://github.com/earendil-works/pi/pull/7224) | Preserve structured metadata for Amazon Bedrock provider errors | ✅ 已关闭 | 保留 Bedrock 错误的结构化元数据（已合并） |

**总结**：今日合并/关闭 18 条 PR，覆盖 **代理（Provider）支持扩展、代理层兼容性修复、TUI 交互改进、HTTP 代理修复** 等多个方向，项目在跨平台稳定性和功能丰富度上均有实质进展。

---

## 4. 社区热点

以下 Issue/PR 在评论数、讨论深度或反应票数上最为突出，反映用户核心诉求与痛点：

1. **[#6768] [OPEN] [bug] Compaction using Copilot Enterprise not possible**  
   [链接](https://github.com/earendil-works/pi/issues/6768)  
   - **评论 16 | 👍 13**  
   - 用户在使用 Copilot Enterprise 许可证进行上下文压缩时遇到 421 错误，OpenAI 和 Anthropic 模型均失败。社区讨论高度集中，多名用户反馈同样问题。目前无明确 fix PR，属于高优先级 bug。

2. **[#4609] [CLOSED] Rewrite pi in Rust**  
   [链接](https://github.com/earendil-works/pi/issues/4609)  
   - **评论 12 | 👍 13**  
   - 讨论重写 Pi 为 Rust 的可行性，虽然已关闭（标为“closed-because-weekend”？），但社区投票高，反映了对性能或资源占用的潜在需求。

3. **[#6747] [OPEN] [inprogress] An API for enhancing agent message markdown**  
   [链接](https://github.com/earendil-works/pi/issues/6747)  
   - **评论 11 | 👍 2**  
   - 用户希望扩展能修改 agent 消息的显示表示而不影响 LLM 内容，已有对应 PR [#7231](https://github.com/earendil-works/pi/pull/7231)（open），属于功能请求与实现并行的热点。

4. **[#7064] [OPEN] [bug] WSL absolute windows paths are mishandled**  
   [链接](https://github.com/earendil-works/pi/issues/7064)  
   - **评论 10 | 👍 1**  
   - WSL2 用户报告 read/write/edit 工具因路径处理错误而回退到命令行工具，影响日常使用。社区反馈积极，尚未有 fix PR。

5. **[#6922] [CLOSED] [bug] Default model cannot be a llama.cpp model**  
   [链接](https://github.com/earendil-works/pi/issues/6922)  
   - **评论 7 | 👍 13**  
   - 启动时若默认模型为 llama.cpp 模型显示“No models available”，导致退出。虽然已关闭，但高票显示本地模型用户痛点，值得关注后续。

**分析**：社区热度集中在 **企业级 Copilot 兼容性、WSL 用户体验、扩展能力** 等方面，用户对 **稳定性和本地模型支持** 有较高期待。

---

## 5. Bug 与稳定性

以下为过去24小时内报告的 Bug，按严重程度排列，并标注是否有修复 PR：

### 严重（阻碍正常工作）
- **[#6768] Compaction using Copilot Enterprise not possible**  
  ⚠️ 无 fix PR，高优先级。  
  [链接](https://github.com/earendil-works/pi/issues/6768)

- **[#7064] WSL absolute windows paths are mishandled**  
  ⚠️ 无 fix PR。  
  [链接](https://github.com/earendil-works/pi/issues/7064)

- **[#6879] auto-compaction never triggers after context grows past 100% until provider overflow**  
  ⚠️ 无 fix PR，需检查后确认。  
  [链接](https://github.com/earendil-works/pi/issues/6879)

- **[#7020] Sometimes Pi doesn't continue after compaction**  
  ⚠️ 无 fix PR。  
  [链接](https://github.com/earendil-works/pi/issues/7020)

### 中等（影响特定场景）
- **[#7194] Pi does a full re-render every 1s when an active tool card scrolls outside the viewport**  
  ⚠️ 无 fix PR，但可能与 [#7236 PR](https://github.com/earendil-works/pi/pull/7236)（视图改进）相关。  
  [链接](https://github.com/earendil-works/pi/issues/7194)

- **[#7187] Silent crash caused by inconsistent error handling and schema validation**  
  ⚠️ 无 fix PR，第三方包 manifest 错误可能导致永久崩溃。  
  [链接](https://github.com/earendil-works/pi/issues/7187)

- **[#7113] TUI freezes after entering an API key in /login when the pi.dev model catalog is unreachable**  
  ⚠️ 无 fix PR。  
  [链接](https://github.com/earendil-works/pi/issues/7113)

### 较低（已有修复或临时方案）
- **[#7062] fix(openai-completions): handle array content and missing finish_reason**  
  ✅ 已有 [PR #7216](https://github.com/earendil-works/pi/pull/7216) 部分修复。  
  [链接](https://github.com/earendil-works/pi/issues/7062)

- **[#7049] Upgrade Undici to 8.8.0 for correct plain-HTTP proxy forwarding**  
  ✅ 已通过 [PR #7225](https://github.com/earendil-works/pi/pull/7225) 修复。  
  [链接](https://github.com/earendil-works/pi/issues/7049)

- **[#7195] Extensions don't load if directory is a symlink**  
  ⚠️ 无 fix PR，但社区给出了临时方案（不使用符号链接）。  
  [链接](https://github.com/earendil-works/pi/issues/7195)

**总体**：今日修复了 **Undici 代理、Z.AI max_tokens、Kimi K3 路由、资源元数据保留** 等多项稳定性问题，但仍有不少严重 bug 待处理。

---

## 6. 功能请求与路线图信号

### 已有关联 PR 的请求（大概率进入下一版本）
- **[#6747] API for enhancing agent message markdown** → PR [#7231](https://github.com/earendil-works/pi/pull/7231)（open）  
- **[#7199] support Kimi K3 on Fireworks** → PR [#7230](https://github.com/earendil-works/pi/pull/7230)（已合并）  
- **[#7003] Update TypeBox after multi-type keyword guard fix** → PR [#7243](https://github.com/earendil-works/pi/pull/7243)（open）  
- **[#7062] fix(openai-completions): handle array content** → PR [#7216](https://github.com/earendil-works/pi/pull/7216)（open，部分）  

### 暂无 PR 但呼声较高的请求
- **[#6305] Newbie friendly way connect to local models server**  
  [链接](https://github.com/earendil-works/pi/issues/6305)  
  用户希望提供自动发现本地模型服务器 URL 的机制，属于易用性改进，可能有路线图价值。
- **[#7126] Rename session via Ctrl+R needs Enter pressed twice**  
  [链接](https://github.com/earendil-works/pi/issues/7126)  
  交互细节优化，评论较少但属于日常体验改进。
- **[#7237] Bound bash output archives and contain temp-storage failures**  
  [链接](https://github.com/earendil-works/pi/issues/7237)  
  功能请求：限制 bash 输出归档大小并处理临时存储失败，属于健壮性改进。

---

## 7. 用户反馈摘要

从过去24小时的 Issues 评论中提炼真实用户痛点与使用场景：

- **Copilot Enterprise 用户受阻**：多名使用 Copilot Enterprise 许可证的用户反映压缩（compaction）完全失效，错误代码 421“Misdirected Request”，导致无法继续工作。他们希望快速排除此问题，否则无法在生产环境中使用 Pi。
- **WSL2 文件路径问题**：WSL 用户反馈 read/write/edit 工具频繁失败，退化为全量写入命令行工具，大幅降低效率。用户希望 Pi 能正确处理 `/mnt/c/` 等 Windows 绝对路径。
- **本地模型启动失败**：使用 llama.cpp 作为默认模型的用户遇到“No models available”错误，不得不手动切换提供商，新手容易困惑。
- **UI 重绘耗资源**：远程沙箱用户观察到 Pi 每秒全量重绘屏幕（当活动工具卡片滚动出视口时），导致带宽和 CPU 浪费，影响多人协作体验。
- **扩展符号链接支持**：用户将扩展目录设为符号链接以同步点文件，但 Pi 无法识别，只能通过非符号链接方式绕开。

**积极反馈**：社区对 **Kimi K3 快速适配**、**Undici 代理修复** 以及 **Apiário 巴西提供商** 的加入表示欢迎，说明项目对区域用户和代理兼容性关注度提升。

---

## 8. 待处理积压

以下为长期未响应或待合并的重要 Issue/PR，建议维护者优先关注：

1. **[#5262] feat(ai): add Anthropic Vertex provider**  
   [链接](https://github.com/earendil-works/pi/pull/5262)  
   - **创建于 2026

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是根据您提供的GitHub数据生成的LiteLLM项目动态日报（2026-07-29）。

---

# LiteLLM 项目日报 (2026-07-29)

## 1. 今日速览

今日LiteLLM项目整体活跃度极高，社区讨论与开发提交均十分活跃。过去24小时内，**Issues更新78条**，**PR更新高达253条**，显示出项目维护团队与社区在功能迭代和问题修复上均投入了大量精力。新提交的PR数量（200个待合并）远超已处理数量（53个），表明项目正处于快速开发和功能集成的阶段。新版本 `v1.94.0` 已发布，但本次发布说明主要侧重于Docker镜像签名验证，未提及大量功能性更新，可能是一次侧重于基础设施层维护的发布。

## 2. 版本发布

### v1.94.0
- **发布说明**: 本次发布核心为强化软件供应链安全，所有LiteLLM Docker镜像现已支持使用Cosign进行签名验证。用户可通过提供的验证指南确保所拉取的Docker镜像是官方签发、未经篡改的。
- **破坏性变更**: 无
- **迁移注意事项**: 对于使用Docker镜像的用户，建议更新CI/CD流程以集成镜像签名验证，保障部署安全。此次升级理论上对现有功能无影响。

## 3. 项目进展

今日有53个PR被合并或关闭，`固定` 和 `更新日志` 类型的PR占据了主要部分，显示项目在持续进行整体性修复与版本管理。

**重点功能/修复推进**:
- **MCP OAuth 修复与优化**: #34985 (已报告bug) 和 #34997 (已合并) 分别解决了MCP OAuth流程中的状态持久化问题和SCIM嵌套组管理问题，提升了企业集成的稳定性。
- **Gemini 兼容性修复**: #34816 (新PR) 提议为配置JSON生成模式文件以提高可维护性；#34779 (新PR) 修复了多轮对话中Gemini `thoughtSignature` 的处理逻辑，确保了与Gemini API的兼容性。
- **Router与UI增强**: #35009 (新PR) 和 #35002 (新PR) 分别对UI中的“Router Settings”导航和团队模型过滤逻辑进行了优化，提升了用户体验和配置效率。

## 4. 社区热点

今日讨论最活跃的Issues主要围绕业务关键路径上的Bug和功能缺失。

1.  **数据库迁移失败的深层问题** (Issue #22998): 此问题已持续数月，今日仍有7条评论。用户报告在升级 `v1.81.14-stable` 时，`litellm_proxy_extras` 的数据库迁移记录已标记为“已应用”，但实际列并未创建，导致登录API返回500错误。该问题严重影响了升级流程的可靠性，社区对此高度关注，迫切需要一个修复或更优雅的降级/回滚机制。
    - [问题链接](https://github.com/BerriAI/litellm/issues/22998)

2.  **代理/UI 聊天页面无法使用** (Issue #26147): 用户反馈在使用 `vLLM` 模型时，`/ui/chat` 页面无法显示聊天记录，提示“Response not found”。此问题已存在数月，直接影响了UI管理面板的可用性，成为社区一大痛点。
    - [问题链接](https://github.com/BerriAI/litellm/issues/26147)

3.  **预算记录错误** (Issue #26239): 用户报告团队密钥的消耗会错误地计入用户个人预算，导致在调用个人密钥时出现 `BudgetExceededError`。这是一个关键的多租户计费bug，对需要精细成本核算的团队影响巨大。
    - [问题链接](https://github.com/BerriAI/litellm/issues/26239)

## 5. Bug 与稳定性

今日报告的新Bug和回归问题主要集中在集成兼容性、数据一致性和配置解析上。

| 严重程度 | Bug 描述 | 是否有 Fix PR | 链接 |
| :--- | :--- | :--- | :--- |
| **严重** | **Gemini上下文缓存使用自定义`api_base`时URL错误**: 用户反映当Gemini上下文缓存使用自定义`api_base`时，缓存请求的URL和Auth Header均不正确，导致缓存失效或API失败。会影响所有使用自定义端点部署Gemini的用户。 | 尚无 | [Issue #34872](https://github.com/BerriAI/litellm/issues/34872) |
| **高** | **Gemini 429限流错误被错误映射为`BadRequestError`**: SDK在解析Vertex AI的异常时，未加区分的`"403" in error_str`字符串匹配逻辑导致429限流错误被错误识别为400请求错误，导致代理层无法正确触发重试逻辑。 | 尚无 | [Issue #34954](https://github.com/BerriAI/litellm/issues/34954) |
| **高** | **MCP OAuth重定向问题**: 持久化的`issuer`配置在元数据获取失败时会导致`/authorize`端点永久性故障。 | 尚未直接覆盖 | [Issue #34985](https://github.com/BerriAI/litellm/issues/34985) |
| **普通** | **Vertex AI原生`service_tier`参数被拒绝**: 发送`service_tier`参数到`vertex_ai/`模型时，被Vertex AI返回400错误。 | 尚无 | [Issue #34914](https://github.com/BerriAI/litellm/issues/34914) |
| **普通** | **`core_helpers.py` / `safe_json_dumps.py`并发访问崩溃**: 在高并发下，`safe_deep_copy`和`safe_dumps`函数因“dictionary changed size during iteration”错误而崩溃。 | 尚无 | [Issue #34471](https://github.com/BerriAI/litellm/issues/34471) |

## 6. 功能请求与路线图信号

今日社区提出了一些值得关注的功能请求，部分已有关联PR，可能成为未来版本的核心特色。

1.  **升级Langfuse集成以支持SDK v4 (Issue #33383)**: Langfuse官方团队提出，希望LiteLLM升级其集成以支持Langfuse SDK v4的OTel ingestion路径。该请求获得6个👍，优先级较高，对确保可观测性集成持续可用至关重要。
    - [Issue链接](https://github.com/BerriAI/litellm/issues/33383)

2.  **支持Claude Gateway (Issue #34924)**: 用户请求支持Anthropic新发布的Claude Apps Gateway，这可能涉及到复杂的反向代理或中间件集成。
    - [Issue链接](https://github.com/BerriAI/litellm/issues/34924)

3.  **Session内自动升级 (PR #34779 & #35010)**: 两个紧密相关的PR旨在解决多模态路由（Complexity Router）中的“session亲和性”问题。当前的实现会将整个会话锁定在首轮请求的模型上，导致后续更复杂的问题无法自动升级到更强模型，除非用户手动触发关键词。PR #34779 提出了基于分数自动升级的机制，而 #35010 引入了会话内多模型缓存预热的“捕获面”，预示着项目在智能路由和成本优化方向上的重要演进。

## 7. 用户反馈摘要

从今日的Issue评论中可以提炼出以下用户痛点和期望：
- **升级体验糟糕**: 多位用户反馈数据库迁移问题 (#22998) 导致升级后服务不可用，抱怨“升级过程不应该变得如此复杂和不可预测”。
- **UI功能不完善**: 用户对 `/ui` 面板的不满持续存在，包括模型列表过滤不准确 (#25222) 和聊天记录丢失 (#26147)。用户期望UI能提供与API同等功能，真实反映代理状态。
- **预算与计费难题**: 企业用户对团队预算与个人预算混淆的问题 (#26239) 表示“这是管理多团队时的噩梦”，迫切需要清晰的成本归属和隔离机制。
- **对新技术支持的期待**: 对于 `Claude Gateway` 和 `Langfuse SDK v4` 的支持请求，社区表达了“顺滑集成”的强烈期望，用户认为这是作为智能网关的核心能力。

## 8. 待处理积压

以下为长期未响应或状态为 `[stale]` 的重要Issue和PR，需要维护团队重点关注。

1.  **数据库迁移失败 (Issue #22998)**: 自3月提出，状态为 `[stale]`，是阻碍用户从 `v1.81.x` 升级到新版本的最大路障。
    - [链接](https://github.com/BerriAI/litellm/issues/22998)

2.  **UI聊天页面404 (Issue #26147)**: 自4月提出，状态为 `[stale]`，严重影响了管理面板的用户体验。
    - [链接](https://github.com/BerriAI/litellm/issues/26147)

3.  **团队预算记录错误 (Issue #26239)**: 自4月提出，是多租户场景下的关键计费Bug。
    - [链接](https://github.com/BerriAI/litellm/issues/26239)

4.  **OpenTelemetry集成崩溃 (Issue #24516)**: 自3月提出，状态为 `[stale]`。用户在使用Usage AI Chat时，OTel成功日志记录路径会因 `response_obj` 非字典类型而崩溃，导致链路追踪数据丢失。
    - [链接](https://github.com/BerriAI/litellm/issues/24516)

5.  **允许非管理员访问`/key/update` 的 `key_type` preset (PR #35006)**: 该PR旨在允许更灵活的角色管理，但仍在待合并状态，其进展将反映项目对细粒度权限控制的支持力度。
    - [链接](https://github.com/BerriAI/litellm/pull/35006)

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我已根据您提供的 Temporal 项目 GitHub 数据，生成以下项目动态日报。

---

### Temporal 项目动态日报 #2026-07-29

**报告周期：** 2026-07-28 UTC 至 2026-07-29 UTC
**数据来源：** github.com/temporalio/temporal

---

#### 1. 今日速览

昨日，Temporal 项目呈现极高的活跃度，尤其是 Pull Request (PR) 提交与处理数量（49条）异常亮眼，远高于近期平均水平，表明项目正处于密集开发和交付阶段。核心方向聚焦于 **CHASM**（下一代架构组件）、**Nexus Operations**、**Schedules**（调度器）和 **Standalone Activities** 等功能模块的深度开发与稳定性修复。与此同时，有 2 个关于 Schedules 的增强型 Issue 持续获得社区关注，社区对编排精细度的需求依然强烈。

- **活跃度评估：** 🚀 **极高**（PR 活动远超日常水平，核心功能开发与重构同步进行）

---

#### 2. 版本发布

无新版本发布。

---

#### 3. 项目进展

昨日有 21 个 PR 被合并或关闭，推动了一批重要的功能和修复落地：

- **CHASM 核心组件推进**：
    - [#11335 Remove system.enableNamespaceHandoverWait dynamic config](https://github.com/temporalio/temporal/pull/11335): 移除了命名空间交接的旧版动态配置，标志着该功能的网关逻辑向新架构（CHASM）的演进迈出坚实一步。
    - [#10881 add namespace replication chasm component](https://github.com/temporalio/temporal/pull/10881): 新增了用于命名空间复制的 CHASM 组件，为未来替换旧的复制队列做准备。
- **功能与可观测性增强**：
    - [#11333 Add dynamic config to flip skip persistence optimization (CHASM)](https://github.com/temporalio/temporal/pull/11333): 为 CHASM 引入了一项关键的持久化优化（跳过无变更节点的持久化），并提供了动态配置开关以控制其启用，兼顾了性能与稳定性。
    - [#11255 Add immediate queue backlog age metric](https://github.com/temporalio/temporal/pull/11255): 新增了即时队列的“备份时长”指标，增强了系统的可观测性，帮助运维人员更精确地监控任务积压情况。
- **清理与技术债务**：
    - [#11334 Remove addsearchattributes workflow](https://github.com/temporalio/temporal/pull/11334): 移除了一个旧的、不再必要的 `addsearchattributes` 工作流，完成了对 Search Attributes API 治理架构的优化收尾。
- **BUG 修复**：
    - [#11320 fix(saa): RESET_REQUESTED(keepPaused=true) maps to runState=PAUSED](https://github.com/temporalio/temporal/pull/11320): 修复了 Standalone Activity 在特定重置场景下的状态机转换问题，确保了暂停状态的正确保留。此项修复对 SAA 功能的可靠性至关重要。

**项目总体向前迈进的幅度的评估：** 多个关于 CHASM 和 Schedules 的 PR 进入待合并或已合并状态，表明项目正稳步从新架构设计过渡到实现与优化阶段。尤其是 CHASM 的成熟度在快速提升。

---

#### 4. 社区热点

昨日社区讨论热度最高的主题集中在 **Schedules** 功能上：

1.  **Issue #4795: [enhancement, schedules] 允许工作流ID “原样” 执行**
    - **链接：** [https://github.com/temporalio/temporal/issues/4795](https://github.com/temporalio/temporal/issues/4795)
    - **热度：** 👍 17 | 评论 7
    - **分析：** 这是目前 Schedules 相关最受关注的 Issue。核心诉求是用户希望在 Schedules 触发执行时，能够完全控制工作流 ID，而不是被框架自动添加时间戳。这反映了用户在处理幂等性、重复数据删除以及与外部系统集成时，对 Workflow ID 的确定性有强烈需求。尽管创建时间较早（2023年），但至今仍有活跃讨论，表明这是一个长期未解决的痛点。

2.  **Issue #5005: [enhancement, schedules] 允许 Backfill 时覆盖搜索属性**
    - **链接：** [https://github.com/temporalio/temporal/issues/5005](https://github.com/temporalio/temporal/issues/5005)
    - **热度：** 👍 1 | 评论 0
    - **分析：** 用户提出的一个具体增强请求，希望在进行 Schedules 的 Backfill（回填）操作时，能够为这些回填的执行设置自定义的搜索属性，以便在 UI 中轻松区分哪些是常规调度，哪些是回填任务。这体现了用户在运营和审计层面，对大规模调度任务的可管理性和可追踪性的需求。

---

#### 5. Bug 与稳定性

昨日没有新提交的 Bug 报告 Issue。然而，在已合并的 PR 中，包含了对稳定性的重要修复：

- **Goroutine 泄漏修复**：
    - **PR 链接：** [#11322 Fix the goroutine leaks tracked in the leak regression test](https://github.com/temporalio/temporal/pull/11322) (待合并)
    - **严重程度：** 🔴 高
    - **分析：** 该 PR 旨在修复回归测试中检测到的所有已知 Goroutine 泄漏，这是一个非常积极但也是高风险的信号。它表明项目团队正在通过自动化测试主动排查并解决内存泄漏问题，对长期运行的服务稳定性至关重要。该 PR 本身正在等待合并，它是对现有稳定性问题的直接回应。

- **调度任务重试逻辑修复**：
    - **PR 链接：** [#11316 Prevent scheduler retries past catchup deadline](https://github.com/temporalio/temporal/pull/11316) (待合并)
    - **严重程度：** 🟡 中
    - **分析：** 该 PR 修复了一个边缘场景：当调度器在回填任务时，如果重试次数过多导致超过截止时间，原先的逻辑可能导致非预期的行为。此修复确保了任务会在过期后被正确丢弃和记录，避免了潜在的执行混乱。

---

#### 6. 功能请求与路线图信号

结合社区 Issue 和项目开发中的 PR，可以推测以下方向可能被纳入下个版本：

- **Schedules 功能深化**：社区强烈要求 (#4795, #5005) 与 PR 活动（#11311, #11316）共同指向 Schedules 是当前开发重点。未来版本极有可能增强 Backfill 的可控性和用户对 Workflow ID 的自定义能力。
- **CHASM 架构成熟化**：大量 CHASM 相关 PR 的涌现（如 #11333, #11263, #11139）强烈表明，Temporal 的下一代架构（CHASM）正从概念验证进入功能完善和生产化阶段。Chasm replication, Nexus operations on CHASM, 以及与 SQL/Nexus 相关的稳定性测试是当前焦点。
- **Standalone Activity (SAA) 的完善**：多项 PR (#11320, #11321) 专注于修复 SAA 的状态机、重试状态暴露等问题，表明该功能正在快速迭代以提升稳定性和可观测性，目标是使其达到与 Workflow Activity 同等的水准。

---

#### 7. 用户反馈摘要

- **正面反馈 (隐含)**：社区对 Schedules 功能的持续关注和投入（大量评论和👍）实际上反映了对该功能的认可和依赖，用户期望它在现有基础上做得更好、更灵活。
- **核心痛点（来自 Issues）**：
    - **Workflow ID 控制缺失 (#4795)**：用户对于无法完全控制调度执行的 Workflow ID 感到困扰，这在需要与外部系统集成或进行精确幂等控制的场景下是个明显的障碍。
    - **Backfill 可观察性差 (#5005)**：用户无法通过搜索属性区分正常调度和回填任务，导致运维和排查困难。这暴露了当前 Schedules 在运营层面的一个短板。

---

#### 8. 待处理积压

- **[Issue #4795] Schedules - add option for execution workflowid to be "as-is"**
    - **链接：** [https://github.com/temporalio/temporal/issues/4795](https://github.com/temporalio/temporal/issues/4795)
    - **状况：** 该 Issue 已开放近 3 年，获得了 17 个 👍 和 7 条评论，是 Schedules 功能用户呼声最高的增强请求之一。尽管项目团队可能在内部进行了一些工作，但至今未有明确的公开进展或关联 PR。鉴于当前 Schedules 正处在密集开发期，维护者应考虑给出一个更明确的回复或更新路线图状态，以回馈社区的热情。

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*