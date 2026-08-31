# OpenClaw 生态日报 2026-09-01

> Issues: 448 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-31 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

## 📋 OpenClaw 项目动态日报 — 2026-09-01

---

### 1. 今日速览

过去 24 小时项目活跃度极高：共 448 条 Issue 更新（新开/活跃 202，关闭 246），500 条 PR 更新（待合并 233，已合并/关闭 267），并有 1 个新版本 v2026.8.1 发布。Issue 关闭率（54.9%）与 PR 合并率（53.4%）均超过五成，说明项目维护节奏和问题上报/解决循环运转顺畅。然而，**v2026.8.1 刚发布即出现多起升级回归报告**，涉及 Gateway 无法启动、配置迁移将 secrets 替换为字面量 `__OPENCLAW_REDACTED__`、cron 任务被错误隔离等严重问题，已有多位用户建议撤回该版本——项目正处于一个活跃但升级稳定性受挑战的窗口期。此外，长期未修复的严重内存泄漏（#91588）和 P0 安全漏洞（#108395）仍是社区情绪的两大关键痛点。

---

### 2. 版本发布

**v2026.8.1（stable）** — [Release Notes](https://docs.openclaw.ai/releases/2026.8.1) | 提交 `ea80657`，发布于 2026-08-31。

官方更新帮助：若自动更新失败，请使用本地编码 harness 帮助完成更新、诊断迁移错误，并验证 Gateway 正确启动；更新前务必备份配置和状态。

**但本次发布在当日即收到多个升级回归报告，集中在迁移与启动路径：**

| 问题 | 严重度 | 链接 |
|---|---|---|
| 2026.7.1-2 → 2026.8.1 升级后 Gateway 无法启动，`doctor --fix` 不执行 config-key 迁移，需约 12 步手动修复 | P1 | [#133984](https://github.com/openclaw/openclaw/issues/133984) |
| 2026.8.1 升级 crash-loop 导致 Gateway 无法启动，`doctor --fix` 被 `ExecApprovalsMigrationRequiredError` 阻塞 | P1 | [#133813](https://github.com/openclaw/openclaw/issues/133813) |
| 配置迁移将 discord token / provider apiKeys 等**全部内联 secrets** 替换为字面量 `__OPENCLAW_REDACTED__` | P0 | [#134169](https://github.com/openclaw/openclaw/issues/134169) |
| 调度器迁移将合法 cron jobs 误隔离为 `invalid-schedule`，静默丢失活跃库存 | P1 | [#133347](

---

## 横向生态对比

## 个人 AI 助手 / 自主智能体开源生态横向对比报告（2026-09-01）

> 说明：本次采集到完整社区动态的为 **OpenClaw**，其余项目（Hermes Agent、OpenHands SDK、Pi、LiteLLM、Temporal）在数据源中未返回可解析的当日动态。因此，数据类对比仅呈现 OpenClaw 实况；其余项目从公开定位和生态角色进行定性分析，并已在表中如实标注。

---

### 1. 生态全景

当前个人 AI 助手 / 自主智能体生态已进入“快速迭代但稳定性承压”的阶段。以 OpenClaw 为参照，头部项目单日可产生近千次 Issue/PR 交互，维护节奏快、社区反馈活跃；但高频发布伴随升级回归，说明项目正经历从“功能扩张”向“工程质量”过渡的阵痛。生态内部呈现明显分层：既有面向终端用户的完整 Agent 服务框架（OpenClaw），也有面向开发者的 SDK（OpenHands SDK）、模型网关（LiteLLM）、通用工作流编排（Temporal）和研究型 Agent 项目（Hermes Agent），共同构成从模型访问、任务编排到应用交付的全栈图谱。基础设施的安全与稳定，尤其是 secrets 管理、配置迁移和长期任务可靠性，正成为制约生态进一步落地的关键瓶颈。

---

### 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | Release | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw** | 448（新开/活跃 202，关闭 246） | 500（待合并 233，已合并/关闭 267） | v2026.8.1 stable，发布当日即现回归 | 活跃度极高，但升级稳定性风险突出；内存泄漏 #91588 与 P0 安全漏洞 #108395 长期未决 |
| **Hermes Agent** | 数据未返回 | 数据未返回 | 数据未返回 | 无法评估（定性分析见下文） |
| **OpenHands SDK** | 数据未返回 | 数据未返回 | 数据未返回 | 无法评估（定性分析见下文） |
| **Pi** | 数据未返回 | 数据未返回 | 数据未返回 | 无法评估（定性分析见下文） |
| **LiteLLM** | 数据未返回 | 数据未返回 | 数据未返回 | 无法评估（定性分析见下文） |
| **Temporal** | 数据未返回 | 数据未返回 | 数据未返回 | 无法评估（定性分析见下文） |

OpenClaw 当日 Issue 关闭率 54.9%、PR 合并率 53.4%，社区维护闭环高效；但新版本 v2026.8.1 引发的多起回归（Gateway 启动失败、secrets 被替换为字面量、cron 任务被错误隔离）表明发布质量把控仍需加强。

---

### 3. OpenClaw 在生态中的定位

- **生态角色**：核心参照项目，定位是**可自托管的个人 AI 助手网关**，集成多消息渠道（Discord、provider API keys）、配置迁移、cron 调度与自动诊断（`doctor --fix`），更接近“开箱即用的个人 AI 中台”。
- **相对优势**：社区规模与迭代速度在同类中领先——单日 448 条 Issue、500 条 PR，说明用户基数大、反馈链路完整；同时具备内置升级辅助 harness 与迁移诊断工具，有意识在降低运维门槛。
- **技术路线差异**：相比 Hermes Agent 偏研究探索、OpenHands SDK 偏代码执行、Pi 偏轻量个人入口，OpenClaw 采用**重量级网关架构**，把通道接入、调度、配置管理、升级流程都收进官方边界内。这带来一体化体验，也导致升级路径复杂，当前回归问题正集中于此。
- **社区规模对比**：从数据密度看，OpenClaw 的 Issue/PR 量级在个人 AI 助手赛道属于头部；LiteLLM、Temporal 虽在各自领域使用面同样广泛，但本次采样中未能获得可对比数据。

---

### 4. 共同关注的技术方向

虽然只有 OpenClaw 有当日数据，但其暴露的问题在 Agent 基础设施中具有普遍共性，值得所有项目关注：

1. **配置与状态迁移的向后兼容性**（涉及：OpenClaw，以及依赖持久化状态的 Temporal、具有丰富配置面的 LiteLLM）  
   OpenClaw 升级中 config-key 迁移未执行、`doctor --fix` 被 `ExecApprovalsMigrationRequiredError` 阻塞（#133813/#133984），用户需手工 12 步修复——迁移工具链必须覆盖更多真实环境。

2. **Secrets 全生命周期管理**（涉及：OpenClaw，以及作为模型网关的 LiteLLM）  
   #134169 升级时把 discord token、provider apiKeys 内联 secrets 全部替换为字面量 `__OPENCLAW_REDACTED__`，属 P0 级数据事故。AI Agent 常需持有大量密钥，如何在迁移、回滚、日志中保持机密性，是生态级命题。

3. **长时间运行的任务调度可靠性**（涉及：OpenClaw，核心与 Temporal 直接共用问题域）  
   调度器迁移将合法 cron jobs 静默隔离为 `invalid-schedule`（#133347），导致活跃任务库存丢失。Agent 自动化依赖持久任务编排，调度的“静默失败”比报错更危险。

4. **自诊断/自愈工具的有效性**（涉及：OpenClaw，以及任何依赖 `doctor` 类工具的项目）  
   在迁移和启动路径上，`doctor --fix` 多次失效，说明自动化诊断需覆盖版本差异和数据库迁移场景，而非仅做静态检查。

5. **长期运行资源治理**（涉及：OpenClaw，对 OpenHands SDK、Pi 等长期驻留进程同样关键）  
   内存泄漏 #91588 长期未修复，叠加 P0 安全漏洞 #108395 未关闭，反映社区对“活跃功能”的投入已压倒核心稳定性债务。

---

### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构特征 |
|---|---|---|---|
| **OpenClaw** | 个人 AI 助手全栈网关：多通道、调度、配置、升级运维 | 自托管个人用户、小型团队 | 重量级网关 + 本地配置 + 内置迁移/诊断 harness |
| **Hermes Agent** | 前沿模型驱动的 Agent 行为研究与实验 | AI 研究者、实验开发者 | 更依赖模型能力，架构偏研究和可探查 |
| **OpenHands SDK** | 软件工程场景的 Agent 开发套件 | 构建 Coding Agent 的开发者 | 围绕代码执行、文件操作、沙箱环境提供 SDK |
| **Pi** | 轻量个人 AI 入口 | 追求简单、低依赖的个体用户 | 轻量、极简，可能偏本地优先 |
| **LiteLLM** | 统一 LLM 网关与 Provider 抽象 | 需要接入多家模型的开发者/团队 | 代理层，侧重 API 标准化、密钥路由、成本管理 |
| **Temporal** |

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*