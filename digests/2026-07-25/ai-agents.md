# OpenClaw 生态日报 2026-07-25

> Issues: 450 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-24 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 OpenClaw 项目 GitHub 数据，以下是为您生成的 2026-07-25 项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-07-25

## 1. 今日速览

今日 OpenClaw 项目的 Issue 与 PR 流量均处于 **极高活跃度** 水平（450 条 Issue 更新，500 条 PR 更新），揭示出项目进入密集的修复与功能开发周期。尽管无新版本发布，但社区与维护者的投入度明显，有 **324 个 PR 被合并或关闭**，表明项目正加速解决积压问题并推进关键功能。值得关注的是，多个高优级（P0/P1）议题正在激烈讨论，集中在会话恢复、数据丢失和核心架构重构上，项目健康度处于 **高投入、高挑战** 状态。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日合并与关闭的 PR 数量庞大（324 条），尽管详细列表未完全展示，但从已关闭的 PR 中可观察到项目在以下关键方向取得显著进展：

- **安全性强化**：PR [#113307](https://github.com/openclaw/openclaw/pull/113307) 被合并，为安装脚本增加了执行前的完整性校验，防止下载破坏或恶意脚本执行，解决了隐患排查，提升了供应链安全性。
- **质量控制与测试覆盖**：PR [#113426](https://github.com/openclaw/openclaw/pull/113426) 被合并，作为修复程序回滚到 `release/2026.7.2` 版本，以确保在 QA 测试中能准确追踪 `sessions_spawn` 功能的执行情况，说明项目正在加强版本发布的测试验证流程。
- **架构与稳定性修复**：PR [#113418](https://github.com/openclaw/openclaw/pull/113418) 被合并，强制整个项目只使用单一的 SQLite 数据库连接边界，从根本上解决了因多连接实例导致的 `deep-Windows-path` 问题，这是一项重要的架构规范化举措，有助于避免潜在的数据库状态不一致和跨平台兼容问题。

这些合并表明，项目除了解决用户报告的 Bug，也在积极推进内部架构清理和开发规范的落地。

## 4. 社区热点

今日讨论最活跃的议题集中在**会话流程的脆弱性**和**关键功能的回归**上。

- **会话初始化与恢复**: Issue [#102020](https://github.com/openclaw/openclaw/issues/102020) (16 条评论) 报告了跨频道场景下第二条消息即失败的问题，涉及 `reply session initialization conflicted`。这直接影响了核心交互体验。
- **核心功能回归**: Issue [#98528](https://github.com/openclaw/openclaw/issues/98528) (6 条评论，Closed) 是一个 P1 级别的回归 Bug，报告了在 2026.6.11 版本后，`exec`, `web_fetch` 等关键工具在每轮对话中首次调用后即输出为空。该问题已被关闭，推测已有修复方案。另一个回归问题 [#111519](https://github.com/openclaw/openclaw/issues/111519) 报告了 Telegram DM 在 `2026.7.2-beta.3` 版本后回复回退。
- **架构统一讨论**: Issue [#110950](https://github.com/openclaw/openclaw/issues/110950) (10 条评论，Closed) 提出了“万物皆 Cron”的愿景，建议将心跳、监控和调度自动化统一为 Cron 作业。此建议虽已关闭，但其高讨论度反映了社区对简化复杂配置模型的渴望。

**诉求分析**: 社区的核心诉求集中在 **可靠性和可预测性**。用户对会话突然中断、工具调用失败或消息丢失等稳定性问题容忍度低，同时对简化复杂的配置和自动化体系存在强烈意愿。

## 5. Bug 与稳定性

今日报告的 Bug 和稳定性问题众多且严重，主要集中在会话状态、数据丢失和渠道集成问题上。以下为按严重程度排列的核心问题：

- **[P0] 升级数据迁移问题**: Issue [#90378](https://github.com/openclaw/openclaw/issues/90378) 报告从 2026.5.28 升级到 6.1 时，Cron 存储从 JSON 静默迁移到 SQLite，导致新工作默认行为变更，可能引起渠道错误。这是一个影响广泛的数据迁移问题，需尽快提供清晰的升级指南或修复。
- **[P1] 会话初始化失败**: Issue [#102020](https://github.com/openclaw/openclaw/issues/102020) (16 条评论) 为最新的严重 Bug，导致跨频道会话无法连续工作，是当前影响最大的会话问题。
- **[P1] 历史思考块签名错误**: Issue [#94228](https://github.com/openclaw/openclaw/issues/94228) 指出在 Anthropic 原生路径下，回放长时间运行的 `thinking` 块会导致整个工具使用线程永久损坏。此问题有链入的开放 PR，表明有修复在途。
- **[P1] 超时导致永久性恢复失败**: Issue [#92043](https://github.com/openclaw/openclaw/issues/92043) 报告 180s 的压缩超时是单次时间限制，导致合法长任务在每次恢复时都失败，形成死循环（`recovery-stuck`）。
- **[P1] 主 Agent 被持久化工作区状态阻塞**: Issue [#111498](https://github.com/openclaw/openclaw/issues/111498) 报告了在 Anthropic 认证恢复后，主 Agent 被一个遗留的工作区状态迁移阻塞，无法响应，是一个严重的可用性问题。

此外，还有大量 P1/P2 的 Bug 涉及 Telegram 频道黑洞、子 Agent 持久占用、Ollama 流式传输问题等，稳定性挑战严峻。

## 6. 功能请求与路线图信号

今日用户提出的功能请求显示出对 **动态、可配置和平台化** 的追求：

- **动态模型发现**: Issue [#10687](https://github.com/openclaw/openclaw/issues/10687) 要求为 OpenRouter 等快速迭代的提供商实现全动态模型发现，取代当前的静态模型目录，这预计会成为提升用户选择灵活性的重要方向。
- **文件系统沙箱**: Issue [#7722](https://github.com/openclaw/openclaw/issues/7722) 要求对工具的文件访问进行配置化沙箱（`tools.fileAccess`），这是对安全性的重要提升，反映社区对角色权限和权限最小化的关注。
- **新渠道集成**: PR [#113419](https://github.com/openclaw/openclaw/pull/113419) 提议增加 Buzz 频道插件，这是一个基于 NIP-29 协议的新去中心化通信渠道。这表明项目在持续拓展第三方集成能力。同时，PR [#112714](https://github.com/openclaw/openclaw/pull/112714) 在推进 iMessage 渠道的原生审批机制。

从已提交的 PR 看，下一个版本的路线图可能侧重于 **核心运行时重构**（如 PR [#113421](https://github.com/openclaw/openclaw/pull/113421) 的 `readiness` 框架和 [#112678](https://github.com/openclaw/openclaw/pull/112678) 的 Agent 加载逻辑优化）、**标准化托管**（[#113422](https://github.com/openclaw/openclaw/pull/113422)）以及 **本地化支持**（[#113427](https://github.com/openclaw/openclaw/pull/113427)）。

## 7. 用户反馈摘要

从今日的 Issue 评论中，可以提炼出以下真实用户反馈：

- **挫败感与不信任**: 用户面对“已恢复的会话”实为“运行中不可用”的欺骗性状态（如 Issue [#98435](https://github.com/openclaw/openclaw/issues/98435) 和 [#92043](https://github.com/openclaw/openclaw/issues/92043) 中的 `recovery-stuck` 标签），表达了对系统状态报告不透明的挫败感。
- **核心功能退化焦虑**: 多位用户（如 Issue [#98528](https://github.com/openclaw/openclaw/issues/98528), [#111519](https://github.com/openclaw/openclaw/issues/111519), [#112906](https://github.com/openclaw/openclaw/issues/112906)）报告了在新版本中“之前工作的功能”出现回退，这种“修复一个，破坏另一个”的模式会导致用户对升级时机产生焦虑。
- **性能与资源消耗**: 在多会话场景下，用户反馈事件循环停滞（[#112273](https://github.com/openclaw/openclaw/pull/112273)）和 Context 体积超标（[#67419](https://github.com/openclaw/openclaw/issues/67419)）问题突出，表明项目在资源管理和性能优化上仍有较大压力。
- **安全与权限控制**: 用户对安全性的需求日益增加，不再满足于全或无的权限模型，强烈要求细粒度控制（如 Issue [#7722](https://github.com/openclaw/openclaw/issues/7722) 的文件沙箱和 [#12219](https://github.com/openclaw/openclaw/issues/12219) 的技能权限声明）。

## 8. 待处理积压

以下为长期未解决或进展缓慢的高影响 Issue，需要维护者关注：

- **文件系统沙箱 (P2, 5个月)**: Issue [#7722](https://github.com/openclaw/openclaw/issues/7722) 讨论深入，需求明确，但状态仍为 `needs-maintainer-review`，无解决方案在途。
- **动态模型发现 (P2, 5个月)**: Issue [#10687](https://github.com/openclaw/openclaw/issues/10687) 被标记为 platinum hermit 高影响等级，但同样卡在 `needs-product-decision` 阶段，无明确推进。
- **会话上下文膨胀 (P2, 3个月)**: Issue [#67419](https://github.com/openclaw/openclaw/issues/67419) 指出每次轮次都会重新注入引导文件，浪费 20-30% Tokens。这既影响速度也影响成本，需作为性能优化事项进行审视。
- **技能权限声明标准 (P2, 5个月)**: Issue [#12219](https://github.com/openclaw/openclaw/issues/12219) 作为安全问题的高影响力提案，自 2 月以来无进展，是提升平台安全性的关键短板。
- **Cron 超时需快速失败 (P1, 4个月)**: Issue [#45494](https://github.com/openclaw/openclaw/issues/45494) 指出 Cron 任务在 LLM API 持续错误时不会快速失败，会耗尽超时窗口，应作为运维质量提升的重点。

这些遗留积压问题，特别是 7722 和 10687，代表了用户对平台安全性和灵活性的长期诉求，其解决将显著提升 OpenClaw 的用户满意度与生态系统成熟度。

---

## 横向生态对比

# AI 智能体/个人助手开源生态横向对比分析报告（2026-07-25）

---

## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态正经历 **高速迭代与社区密集反馈的“爆发期”**。各项目在会话可靠性、安全加固、工具调用标准化方面面临共同挑战，同时纷纷向 **远程客户端模式、结构化输出、MCP/ACP 协议集成** 方向演进。生态整体从“单机实验”向 **服务化、平台化、企业级** 过渡，用户对稳定性、安全性和跨平台兼容性的要求显著提升。大量回归 Bug 和功能断裂表明，社区规模和功能复杂度已超过基础设施的质量保障能力，行业正进入“功能补全”与“质量巩固”并行的关键阶段。

---

## 2. 各项目活跃度对比

| 项目 | Issue 更新 | PR 更新 | 今日 Release | 健康度评估 |
|------|-----------|--------|-------------|------------|
| **OpenClaw** | 450 | 500 | 无 | 高投入高挑战，会话稳定性严重，大量回归 Bug |
| **Hermes Agent** | 440+ | 500+ | 无 | 极高活跃，Desktop 客户端是最大痛点，Windows 支持不足 |
| **OpenHands SDK** | 21 | 50 | v1.37.1 补丁 | 安全加固显著，协议兼容性隐忧 |
| **Pi** | 77 | 23 | v0.82.0 | 功能推进快（Constrained sampling），但 Copilot 压缩等严重 Bug 未修 |
| **LiteLLM** | 85 | 187 | v1.95.0-dev.2 | 基础设施发力（Rust 网关、MCP），TPM 限速回归顽固 |
| **Temporal** | 1 | 43 | 无 | 稳定演进，技术债务清理（V2 调度器、依赖升级） |

**结论**：OpenClaw 与 Hermes Agent 规模最大但稳定性承压；Pi 和 LiteLLM 版本节奏积极但存在高危缺陷；Temporal 最成熟稳健。

---

## 3. OpenClaw 在生态中的定位

- **优势**：社区规模最大（单日 450+ Issue / 500+ PR），功能覆盖最广（多渠道、Cron、技能、会话管理），是通用 AI 智能体框架的 **“参照实现”**。今日合并 324 个 PR，展示极强迭代能力。
- **技术路线**：强调整合统一配置、自托管全功能运行，与 Pi 的轻量 TUI 和 Hermes 的桌面客户端形成差异化。
- **短板**：**会话恢复死循环、数据迁移 Bug、工具调用回归** 等问题频发，用户普遍反映“修复一个，破坏另一个”。相比之下，OpenHands SDK 和 Temporal 的稳定性表现更优。
- **社区规模**：OpenClaw 与 Hermes Agent 处于第一梯队（日活跃度 ~500），Pi 和 LiteLLM 为第二梯队（~100），OpenHands SDK 和 Temporal 为成熟稳定梯队（<50）。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---------|---------|----------|
| **会话恢复与可靠性** | OpenClaw、Hermes Agent、Pi | 跨频道会话失败（#102020）、Telegram 网关挂死（#67498）、Copilot 压缩 421 错误（#6768）、Gemini 工具 ID 丢失（#7047） |
| **安全加固** | 全部 6 个项目 | API 密钥泄露（OpenHands #4216）、安装脚本完整性校验（OpenClaw #113307）、Windows 签名（Hermes #50210）、Temporal 供应链签名、LiteLLM 扫描失败 |
| **结构化输出与工具调用格式标准化** | OpenHands SDK、Pi、LiteLLM | Pydantic 响应 schema（#4206）、OpenAI `required` 数组归一化（#7050）、MCP 路由上下文泄漏（LiteLLM #30416） |
| **远程/瘦客户端模式** | Hermes Agent、OpenClaw | Desktop 仅连接远程服务器（#38602），社区强烈希望 Agent 服务化集中部署 |
| **协议生态成熟（MCP/ACP）** | OpenHands SDK、LiteLLM、Pi | ACP 技能重复（#4019）、MCP 版本断开（#4093）、MCP OAuth RFC 8707 兼容（LiteLLM #34265） |

---

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent | OpenHands SDK | Pi | LiteLLM | Temporal |
|------|----------|-------------|--------------|-----|---------|----------|
| **功能侧重** | 全能 AI 助手（多通道、自动化、技能） | 桌面优先 + 隐私（Telegram/Matrix） | 开发者 SDK（事件、结构化输出、文件系统） | 轻量 TUI、多提供商兼容、本地推理 | 模型网关/代理（限速、路由、计费、MCP） | 工作流编排引擎（调度、持久化、故障注入） |
| **目标用户** | 个人开发者/团队，自托管 | 个人用户，重视桌面体验 | 应用开发者，构建 Agent 应用 | 终端用户，偏好 CLI/TUI | 平台运维，统一 API 管理 | 后端/SRE，构建可靠分布式工作流 |
| **技术架构** | 单体 + 插件（SQLite、Cron） | 桌面客户端 + 后端代理 | 库式 SDK（Python） | 模块化 TUI + 核心引擎（Rust/Go） | 中间件代理（Python + Rust 网关） | 分布式服务（Go、gRPC） |

**关键差异**：Pi 和 LiteLLM 更专注 **模型兼容性与推理**，而 OpenClaw 与 Hermes 更关注 **用户交互与自动化**。OpenHands SDK 是唯一暴露底层 API 给开发者的项目。

---

## 6. 社区热度与成熟度分层

- **快速迭代阶段（功能爆发、稳定性波动）**：OpenClaw、Hermes Agent、LiteLLM  
  三者日 PR 量 >100，新功能密集合并（Constrained sampling、V2 调度器、Rust 网关），但伴随大量回归 Bug（TPM 限速不生效、会话恢复死锁），用户升级焦虑明显。

- **质量巩固阶段（版本节奏适中、修复为主）**：OpenHands SDK、Pi  
  版本更新谨慎（补丁或 minor），重点关注安全漏洞和协议兼容性。Pi 虽发布 v0.82.0 大功能，但仍有 Copilot 压缩等严重 Bug 未修，处于过渡。

- **成熟稳健阶段（技术债务清理、架构演进）**：Temporal  
  无新版本但 43 个 PR 密集合并，侧重内部架构（移除旧配置、依赖升级、可编程故障注入），社区讨论更偏向设计决策，而非紧急 Bug。

---

## 7. 值得关注的趋势信号

1. **从“全功能一体机”到“远程 Agent 服务”**  
   Hermes Agent 的 Desktop 瘦客户端请求（#38602）和 OpenClaw 的远程管理讨论，预示用户不再满足于本地运行完整 Agent，而是希望将核心逻辑部署在服务器，仅通过轻量界面访问。这对资源受限环境和企业级部署至关重要。

2. **工具调用精确化成为刚需**  
   Pi 的 `Constrained Sampling` 和 OpenHands SDK 的 `response_schema` 同时落地，表明开发者要求 Agent 输出严格可预测的 JSON 格式，以对接下游系统。模型必须支持 JSON Schema 约束，否则无法稳定使用。

3. **安全事件倒逼生态升级**  
   多项目暴露 API 密钥直接打包（OpenHands）、安装脚本无校验（OpenClaw）、模型自评绕过安全分析（#4157）等严重漏洞。供应链安全（cosign 签名、CLI 完整性校验）成为标配。

4. **协议生态（MCP/ACP）快速成熟但兼容性阵痛**  
   LiteLLM、OpenHands SDK、Pi 同时集成 MCP/ACP，但出现版本断开、技能重复、OAuth 不标准等问题。预计未来 3 个月将涌现更多协议统一规范（如 OpenAI 的 strict mode 与 MCP 的融合）。

5. **性能与资源管理成新瓶颈**  
   OpenClaw 上下文膨胀（#67419 浪费 20-30% tokens）、LiteLLM 事件循环阻塞（114MB 错误响应）、Pi TUI 渲染优化，暴露基础性能不足。开发者需关注事件循环监控、会话压缩策略和内存限制机制。

**对 AI 智能体开发者的建议**：  
- 优先采用支持结构化约束的框架（Pi、OpenHands SDK）以提升工具调用可靠性。  
- 部署时务必隔离 API 密钥和文件系统（参考 OpenClaw #7722 沙箱、OpenHands #4217 修复）。  
- 关注协议版本锁定（ACP >=0.10.1 兼容性问题），使用 LTS 版本避免升级断裂。  
- 考虑部署架构向远程 Agent 服务演进，提升灵活性与可管理性。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为AI智能体与个人AI助手领域的开源项目分析师，我将根据您提供的数据，为您生成 Hermes Agent 项目的 2026-07-25 项目动态日报。

***

### Hermes Agent 项目动态日报 | 2026年7月25日

**数据覆盖区间：** 2026-07-24 至 2026-07-25

---

#### 1. 今日速览

今日项目活跃度极高，社区参与度火爆。过去24小时内，共产生了超过440条Issue和500条PR，虽然大部分为开放状态，但合并/关闭数量也超过200项，表明项目处理能力与社区热情同步高涨。**Desktop客户端的稳定性与连接问题是当前社区最关注的焦点**，同时多个Gateway层面的Bug修复和平台兼容性改进正在并行推进。整体来看，项目处于高速迭代与社区大规模反馈的密集期，健康度较高，但新Bug的涌入速度也值得关注。

---

#### 2. 版本发布

无新版本发布。

---

#### 3. 项目进展

今日合并/关闭的PR反映了项目在平台兼容性、稳定性及功能完善方面的持续努力。

*   **Kanban流程规则化**：PR [#67057](https://github.com/NousResearch/hermes-agent/pull/67057) 被合并，该修复限制了Kanban板自动分解功能，确保其仅在被授权的板上执行。这增强了工作流定制的灵活性，避免了不必要的自动操作。
*   **Docker后端清理修复**：PR [#62312](https://github.com/NousResearch/hermes-agent/pull/62312) 成功合并，解决了在Docker环境中，临时探针容器未能被正确清理的问题。此举可有效防止资源泄漏，提升Docker后端的可靠性。
*   **CLI多平台兼容性增强**：PR [#48838](https://github.com/NousResearch/hermes-agent/pull/48838) 被合并，它修复了在Windows上因命令输出解码问题导致的CLI工具崩溃。这标志着项目在跨平台（尤其是Windows）的健壮性上又向前迈进了一步。
*   **重要安全修复**：PR [#71049](https://github.com/NousResearch/hermes-agent/pull/71049) 和 PR [#71048](https://github.com/NousResearch/hermes-agent/pull/71048) 分别对Windows上的Auth存储安全性和Discord消息转发规范化进行了修复，提升了关键功能的安全性和一致性。

这些合并的PR表明，项目正在**积极修复已知的稳定性问题，并着力提升对Windows生态的支持水平。**

---

#### 4. 社区热点

*   **[Feature]: Desktop Client-Only Installation** (Issue [#38602](https://github.com/NousResearch/hermes-agent/issues/38602))
    *   **热度：** 13条评论，53个👍
    *   **诉求：** 用户希望Hermes Desktop App能够作为只连接远程服务器的“瘦客户端”来运行，而不是强制在本地引导一个完整的Hermes Agent运行时。
    *   **分析：** 这是当前社区最响亮的呼声之一。用户希望将计算资源和数据管理集中在服务器端，Desktop仅作为一个轻量级交互界面。这反映出用户群体正在从单机个人使用转向**Agent即服务**的远程管理模式，是项目向企业级或高级用户演进的关键信号。

*   **[Bug]: Matrix E2EE device verification fails** (Issue [#6174](https://github.com/NousResearch/hermes-agent/issues/6174))
    *   **热度：** 10条评论，4个👍 (已关闭)
    *   **诉求：** 用户在启用端到端加密（E2EE）的Matrix聊天中，Hermes Bot无法完成设备验证，导致所有加密消息无法解密。
    *   **分析：** 该Bug虽已关闭，但获得了大量讨论。E2EE是注重隐私的用户的基本需求。尽管已关闭，但侧面反映出用户对**安全通信**的强烈需求，以及项目在复杂加密协议上的处理仍存在挑战。

*   **[Bug]: Latest session does not switch after navigating to Plugins/Artifacts tab and back** (Issue [#66875](https://github.com/NousResearch/hermes-agent/issues/66875))
    *   **热度：** 8条评论
    *   **诉求：** 在Desktop App中，当用户切换到“插件/工件”等非聊天标签页再返回时，点击列表中的最新会话无法正确切换，用户体验出现断裂。
    *   **分析：** 这是一个典型的桌面端UI/UX交互Bug，直接影响了用户的工作流。高回复量说明这个问题影响面广，且容易复现，对Desktop的日常使用造成了显著困扰。

---

#### 5. Bug 与稳定性

按严重程度排列今日值得关注的新增及活跃Bug：

*   **P1级（紧急）：**
    *   **Telegram网关连接挂起** (Issue [#67498](https://github.com/NousResearch/hermes-agent/issues/67498))：Telegram网关注册后始终卡在“正在连接”状态，即使在应用已知的IP回退方案后依然无效。这是一个严重影响Telegram平台用户使用体验的阻塞性问题。
    *   **Windows App签名问题** (Issue [#50210](https://github.com/NousResearch/hermes-agent/issues/50210))：Windows桌面客户端安装后，主程序`Hermes.exe`未签名，被Windows 11的Smart App Control拦截，导致App不可用。这会直接劝退大量Windows用户。

*   **P2级（重要）：**
    *   **桌面端UI/UX Bug** (Issues [#63047](https://github.com/NousResearch/hermes-agent/issues/63047), [#66875](https://github.com/NousResearch/hermes-agent/issues/66875), [#49978](https://github.com/NousResearch/hermes-agent/issues/49978))：多篇报告指出Desktop App在交互（会话切换、输入响应、长对话后冻结）上存在问题，严重降低使用体验。其中Issue [#63047](https://github.com/NousResearch/hermes-agent/issues/63047) 描述的情况尤为严重（UI完全冻结）。
    *   **技能整理导致Cron任务失效** (Issue [#26326](https://github.com/NousResearch/hermes-agent/issues/26326))：自动化技能管理功能在合并或删除技能时，未能同步更新引用这些技能的Cron任务，导致定时任务失效。这是一个数据一致性问题，影响自动化的可靠性。
    *   **成本显示功能存在缺陷** (Issue [#67762](https://github.com/NousResearch/hermes-agent/issues/67762))：会话成本估算值在网关注册后会被重置为$0，这对于任何依赖此数据进行费用跟踪或显示的功能都是阻塞性的。
    *   **远程连接功能缺陷** (Issue [#69551](https://github.com/NousResearch/hermes-agent/issues/69551))：在非默认Profile下，Desktop的SSH远程模式完全失效，原因是路径验证存在逻辑错误。这影响了高级用户的远程管理能力。

*   **已有Fix PR的Bug:**
    *   Issue [#70538](https://github.com/NousResearch/hermes-agent/issues/70538) 描述的Desktop E2E测试超时问题，虽然是一个CI问题，但其Blocking性质直接影响开发效率。
    *   PR [#71043](https://github.com/NousResearch/hermes-agent/pull/71043) 和 PR [#71001](https://github.com/NousResearch/hermes-agent/pull/71001) 分别针对会话清理和压缩轮转的数据丢失问题提出了修复方案，目前为OPEN状态，值得关注。

---

#### 6. 功能请求与路线图信号

*   **强烈信号：Desktop远程客户端模式**
    *   Issues [#38602](https://github.com/NousResearch/hermes-agent/issues/38602) 和 [#36970](https://github.com/NousResearch/hermes-agent/issues/36970) 清晰地表达了用户对“Desktop作为纯远程客户端”的需求。这很可能被提升为下一个版本的核心Feature。

*   **数据备份与版本控制**
    *   Issue [#12238](https://github.com/NousResearch/hermes-agent/issues/12238) 获得了19个👍，要求为Agent数据（记忆、技能等）增加自动备份和版本控制功能。这表明用户对**Agent数据资产化管理**的需求日益增长，希望避免因误操作或故障导致数据丢失。

*   **Context管理机制的标准化**
    *   Issue [#36765](https://github.com/NousResearch/hermes-agent/issues/36765) 和 [#513](https://github.com/NousResearch/hermes-agent/issues/513) 都在讨论Context Engine（上下文引擎）的架构。它们提出应区分“选择/路由”和“压缩”两个概念，并借鉴Kilocode实现更高效的两阶段处理。这暗示社区认为当前的上下文压缩策略有优化空间，是项目技术演进的重要方向。

*   **Cursor SDK集成**
    *   Issue [#30640](https://github.com/NousResearch/hermes-agent/issues/30640) 提出了将Cursor Composer作为`cursor_agent`工具整合到Hermes中。这是一个连接AI Agent与代码生成工具的**杀手级功能**，如果实现，将极大扩展Hermes在开发者社区的吸引力。

---

#### 7. 用户反馈摘要

*   **痛点集中于Desktop App**：用户对Desktop App的稳定性、交互方式（如只能作为本地全功能客户端）存在普遍不满。反馈中频繁出现“无响应”、“连接失败”、“UI冻结”等负面词汇，Desktop的体验是当前用户主要的挫败来源。
*   **对远程连接模式的强烈渴望**：用户不再满足于在本机上运行完整的Hermes Agent。他们希望将核心Agent部署在服务器/远程机器上，而Desktop只作为一个无处不在的双向交互终端。这是向“Agent农场”或“中心化Agent服务”模式演进的核心信号。
*   **平台兼容性问题**：特别是Windows和中文Windows用户，面临着App签名、编码崩溃等“硬伤”问题，导致基础功能不可用。这表明项目在平台测试，特别是非POSIX系统上的覆盖度仍有欠缺。
*   **对AI工作流的深度要求**：用户正在将Hermes Agent应用于更复杂、更自动化的场景。他们不仅需要简单的聊天，还需要**稳定可靠的自动化（Cron）**、**可控的技能管理**以及**成本可见性**。这些高级功能的Bug往往比普通聊天Bug影响更大。
*   **隐私与安全性是刚需**：Matrix E2EE问题的长期讨论表明，社区中存在一批高度重视通信隐私的用户。他们期望Hermes Agent在安全层面达到企业级水准。

---

#### 8. 待处理积压

以下长期存在的问题和PR，对项目健康度有潜在影响，需维护团队关注：

*   **紧急问题：**
    *   **Telegram网关的严重问题**： [#67498](https://github.com/NousResearch/hermes-agent/issues/67498) (P1) 和 [#692814](https://github.com/NousResearch/hermes-agent/issues/692814) (P3, 连接泄漏问题) 均涉及Telegram网关，且持续多日未有结论。这严重影响了Telegram用户群体的使用。
    *   **Windows平台兼容性“硬伤”**：[#50210](https://github.com/NousResearch/hermes-agent/issues/50210) (P1, 签名问题) 和 [#53428](https://github.com/NousResearch/hermes-agent/issues/53428) (P2, 中文系统编码问题) 是Windows用户的两大入门级障碍，长期未彻底解决将损害项目在Windows生态的推广。

*   **长期未决但重要的功能请求与Bug：**
    *   **数据备份/版本控制** [#12238](https://github.com/NousResearch/hermes-agent/issues/12238) 作为高赞功能请求，应被纳入路线图讨论。
    *   **Cron任务与技能引用的数据一致性问题** [#26326](https://github.com/NousResearch/hermes-agent/issues/26326) 是一个典型的架构设计问题，长期存在会影响用户对自动化功能的信任。
    *   **技能仓库“污染”问题** [#17345](https://github.com/NousResearch/hermes-agent/issues/17345) 需要核心开发者介入，澄清或修复不同Hermes相关项目（如OpenClaw）之间潜在的配置文件/技能库干扰问题。

*   **悬而未决的PR**：
    *   PR [#39382](https://github.com/NousResearch/hermes-agent/pull/39382) 关于暴露ElevenLabs TTS配置，已存在超过一个月，仍在等待合并。如果功能本身无问题，合并此类高价值PR将充实项目功能，提升用户满意度。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是基于2026年7月25日数据生成的OpenHands SDK项目日报。

---

# OpenHands SDK 项目动态日报 | 2026-07-25

---

## 1. 今日速览

今日项目活跃度**极高**，24小时内产生了21条Issue更新和50条PR活动，社区参与热情旺盛。核心进展与隐患并存：**v1.37.1补丁版本**已发布，修复了代理服务器的关键安全配置；社区在**结构化输出**和**凭证安全**两大方向上有显著推进。然而，严重的**安全漏洞报告（如轨迹下载泄露API密钥、模型自评风险等级）** 和**与第三方协议（ACP）的兼容性问题**成为当前最需关注的稳定性风险点。尽管项目整体向前迈进，但合并/关闭的PR数量（5条）相对于庞大的待处理队列（45条）提示了潜在的合并瓶颈。

## 2. 版本发布

**新版本：v1.37.1**
- **发布链接**: [v1.37.1](https://github.com/OpenHands/software-agent-sdk/releases/tag/v1.37.1)
- **发布时间**: 2026-07-24
- **关键更新**: 这是一个补丁版本，主要修复了代理服务器（agent-server）的一个安全配置问题。
- **重要变更与迁移注意**:
    - **[安全/配置]**: PR [#4180](https://github.com/OpenHands/software-agent-sdk/pull/4180) 修复了当没有配置Session API密钥时，`agent-server` 默认绑定到 `0.0.0.0`（所有网络接口）的问题。现在，若无密钥，它将默认只绑定到 `127.0.0.1`（本地回环），从而防止未经授权的网络访问。
    - **迁移注意**: 如果您的部署依赖于无密钥情况下从外部IP访问 `agent-server`，升级到此版本后需要显式配置 `bind_host` 和 API密钥。建议所有用户尽快升级以确保安全。

## 3. 项目进展

今日合并/关闭的5个PR（包括1个Release PR）和多个重要Issue的关闭，推动了项目在以下几个关键领域取得了实质性进展：

- **核心安全加固**:
    - **[已关闭 - #4217](https://github.com/OpenHands/software-agent-sdk/pull/4217)**: 修复了“轨迹下载”API (`download-trajectory`) 泄露LLM和Condenser API密钥的严重问题。
    - **[已关闭 - #4198](https://github.com/OpenHands/software-agent-sdk/pull/4198)**: 通过要求在冷启动前重新激活凭证，增强了凭证安全性。
- **结构化输出功能落地**:
    - **[已关闭 - #4206](https://github.com/OpenHands/software-agent-sdk/issues/4206)**: 关于实现结构化输出的讨论（`response_schema`）已关闭，相关的功能实现 PR [#4207](https://github.com/OpenHands/software-agent-sdk/pull/4207) 已被提出并等待合并。这是一个期待已久的特性，允许用户为工具调用定义Pydantic模型，以获得严格格式化的响应。
- **事件系统健壮性**:
    - **[已关闭 - #4089](https://github.com/OpenHands/software-agent-sdk/pull/4089)**: 修复了事件图可能因未知父事件而形成循环的问题，通过在追加时拒绝未知父事件来确保数据完整性。
- **用户体验改进**:
    - **[已关闭/合并 - #4211](https://github.com/OpenHands/software-agent-sdk/pull/4211)**: 改进了示例中的确认提示，使其显示LLM提供的可读动作摘要，而非原始的Action模型转储。

## 4. 社区热点

1.  **#2078 [Tracker] Daily Integration Runs (146评论)**
    链接: https://github.com/OpenHands/software-agent-sdk/issues/2078
    这是一个每日集成运行的长期追踪Issue，长期以来一直是社区讨论和集成状态报告的中心。今日仍有更新，说明集成测试持续运行，且社区持续关注其状态。

2.  **#4019 [Bug] ACP profiles inject workspace project skills that duplicate what the ACP CLI already ingests (12评论)**
    链接: https://github.com/OpenHands/software-agent-sdk/issues/4019
    此问题引发了关于ACP（Agent Communication Protocol）交互中技能（skills）重复加载的深入讨论。社区开发者指出，当通过ACP CLI配置时，代理会自动加载一次项目技能，而SDK的ACP配置文件会再次注入，导致技能在LLM上下文中重复出现，浪费token并可能引发冲突。这反映了协议集成中的细微语义冲突问题。

3.  **#3267 [Bug] DeepSeek v4-pro/v4-flash compatibility issues (10评论)**
    链接: https://github.com/OpenHands/software-agent-sdk/issues/3267
    随着DeepSeek新版本模型的推出，社区用户详细报告了模型列表获取、提供者路由逻辑以及`reasoning_content`处理上的兼容性问题。这表明社区对最新、最前沿模型的支持有强烈需求，也暴露了LLM提供商抽象层的潜在不灵活之处。

## 5. Bug 与稳定性

以下问题按严重程度排列，标注了修复进展：

- **【严重-安全】#4216 [已关闭]**: **轨迹下载泄露LLM & Condenser API密钥**。漏洞细节令人担忧，直接打包原始会话目录而未做任何掩码处理。**此Bug已有对应FIX PR #4217并已合并**。
    - 链接: https://github.com/OpenHands/software-agent-sdk/issues/4216
- **【严重-安全/信任】#4157 [开放]**: **LLMSecurityAnalyzer信任模型自评风险等级**。配置`security_analyzer: llm`后，只要模型自己将某个动作评为“低风险”，就会自动执行，绕过了人工确认。这构成了巨大的安全隐患，因为模型可能低估自己的错误行动。
    - 链接: https://github.com/OpenHands/software-agent-sdk/issues/4157
- **【高-数据完整】#4080 [开放]**: **单一未注册事件类型导致整个对话加载失败**。如果一个事件序列化失败（如`observation.kind`未注册），整个对话将被静默丢弃。这个Bug会导致用户数据丢失，严重影响可靠性。**暂无关联的FIX PR**。
    - 链接: https://github.com/OpenHands/software-agent-sdk/issues/4080
- **【高-兼容性】#4093 [开放]**: **ACP 0.11 删除Gemini模型状态**。SDK声明了宽松的ACP依赖（`>=0.10.1`），导致引入下位不兼容的版本，破坏了与Gemini CLI的集成。这提示需要更严格的依赖管理和向下兼容性测试。
    - 链接: https://github.com/OpenHands/software-agent-sdk/issues/4093
- **【中-性能】#4063 [开放]**: **`max_concurrent_runs`不限制原生异步对话**。配置参数失效，异步事件驱动（EventService）的对话可以无限并发，可能导致服务器资源耗尽。
    - 链接: https://github.com/OpenHands/software-agent-sdk/issues/4063

## 6. 功能请求与路线图信号

- **结构化输出（Strong Signal）**: Issue #4206 已关闭，且实现PR #4207 已在队列中。这很可能成为下一个版本的核心新功能之一。它满足了开发者对Agent输出确定性、可解析性的强烈需求。
    - 链接: https://github.com/OpenHands/software-agent-sdk/issues/4206
- **支持标题生成LLM偏好（Moderate Signal）**: Issue #4199 提出，SDK虽已支持`title_llm_profile`，但UI（Canvas和OpenHands应用）缺乏持久化设置此偏好的能力。这是一个典型的“SDK能力已经就绪，但上层UI未集成”的断点，表明项目在功能落地的全链路一致性上需要加强。
    - 链接: https://github.com/OpenHands/software-agent-sdk/issues/4199
- **智能模型选择（Weak Signal）**: Issue #3442 关于自动路由任务到最佳模型的提议在之前获得了一些关注（1个👍），但已标记为过时（Stale）。这可能意味着社区更倾向于手动配置的灵活性，或者此功能实现复杂度超出预期。
    - 链接: https://github.com/OpenHands/software-agent-sdk/issues/3442

## 7. 用户反馈摘要

从今日的Issue评论中，可以提炼出以下用户和开发者的核心痛点与场景：

- **安全是第一要务**: 多个高优先级Bug（#4216, #4157）直指安全领域的核心担忧。用户明确指出，API密钥泄露和模型自我评估风险是不可接受的，这严重影响了项目在安全敏感场景（如企业级、金融级）下的采用。
- **协议兼容性之痛**: 用户在使用ACP等集成协议时遇到了“部分应用 (#4158)”、“版本断裂 (#4093)”等问题。这表明，虽然拥抱开放生态（如ACP）是正确方向，但多版本、多实现的兼容性管理和测试已成为一个亟待解决的工程挑战。
- **对“半成品”功能的不满**: 从#4199（标题生成LLM偏好未在UI落地）和#4158（切换Profile未完全生效）可以看出，用户对功能仅在SDK层级实现而感到困惑和不满。他们期望的是开箱即用、端到端流畅的体验。

## 8. 待处理积压

以下为长期未合并或未回应的关键PR，建议维护团队关注：

- **PR #1821 - feat: add LSP server runtime support**: 已开放 **6个月**。此PR为代理提供代码智能能力（如跳转到定义），对开发者用户场景至关重要。其长期积压可能成为新贡献者的阻碍。
    - 链接: https://github.com/OpenHands/software-agent-sdk/pull/1821
- **PR #2371 - feat: add per-MCP server graceful degradation**: 已开放 **4.5个月**。此PR解决了一个非常实际的痛点：单个MCP服务器故障不应导致整个Conversation启动失败。提议的优雅降级策略对系统健壮性提升明显。
    - 链接: https://github.com/OpenHands/software-agent-sdk/pull/2371
- **PR #3954 - fix(sdk): mark corrective nudge as environment event**: 已开放 **3周**。此PR修正了事件系统中一个分类错误，对数据分析和审计日志的准确性有重要意义。
    - 链接: https://github.com/OpenHands/software-agent-sdk/pull/3954

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目日报 — 2026-07-25

## 1. 今日速览

过去 24 小时内，Pi 项目保持高活跃度：共处理 77 条 Issue 更新（其中 17 条新开/活跃，60 条关闭），23 条 PR 更新（10 条待合并，13 条已合并/关闭），并发布了 **v0.82.0** 版本。主要进展集中在 **工具调用约束采样（Constrained tool sampling）** 的功能落地、多个热门 Bug 的修复（如 `wl-copy` 退出码检查、模型配置热重载、OpenAI 工具模式 `required` 数组归一化），以及 TUI 渲染性能的大幅优化。社区反馈聚焦于 **Copilot Enterprise 压缩失败**、**Gemini 3.x 工具 ID 丢失** 以及 **llama.cpp 默认模型启动问题**，其中大部分已有对应的修复 PR 或正在处理中。

## 2. 版本发布：v0.82.0

- **发布链接**：https://github.com/earendil-works/pi/releases/tag/v0.82.0
- **核心新特性**：**Constrained tool sampling** — 工具定义现在可以指定偏好或强制要求使用严格 JSON Schema 采样，或使用 OpenAI Lark/regex 文法。模型能力元数据会自动阻止对不支持的请求发送此类约束，确保向后兼容。此特性主要面向需要精确工具调用格式的 OpenAI 兼容提供商（如 DeepSeek、Databricks）以及使用自定义推理引擎的用户。
- **破坏性变更与迁移注意**：未明确声明破坏性变更。但若用户自定义了 `tool_choice` 或 `tool_schema` 的 JSON Schema 序列化逻辑，建议检查是否与新的 `constrainedSampling` 字段冲突。默认情况下，行为保持不变。

## 3. 项目进展

今日合并的 13 个 PR 覆盖了多个重要维度的修复与增强：

| PR 编号 | 标题 | 类型 | 关键进展 |
|--------|------|------|----------|
| [#7082](https://github.com/earendil-works/pi/pull/7082) | perf(tui): O(viewport) transcript rendering | 性能优化 | 引入视口窗口化和容器记忆化，使大日志（5000+ 行）的 TUI 渲染复杂度降为 O(视口高度)，显著缓解输入延迟。 |
| [#7009](https://github.com/earendil-works/pi/pull/7009) | fix: await wl-copy exit code and fall through to xclip on failure | Bug 修复 | 确保 `wl-copy` 退出码被检查，失败时自动回退到 `xclip` / OSC 52，解决沙箱环境下 `/copy` 假成功问题 (#6872)。 |
| [#7036](https://github.com/earendil-works/pi/pull/7036) | fix(coding-agent): reload model config in picker | Bug 修复 | 使 `ModelRuntime.refresh()` 在刷新前重新加载 `models.json`，修复 `model` 命令无法立即感知配置文件修改的回归 (#6999)。 |
| [#7050](https://github.com/earendil-works/pi/pull/7050) | Normalize OpenAI tool schema required arrays | Bug 修复 | 修正 DeepSeek 等严格 OpenAI 兼容提供商因 JSON Schema 中 `required` 为 `null` 而拒绝工具调用的问题。 |
| [#7055](https://github.com/earendil-works/pi/pull/7055) | fix(ai,agent,coding-agent): prevent retry on tool validation errors | Bug 修复 | 当 LLM 输出畸形工具参数时，阻止代理层重试（原错误信息含 "429" 导致误触重试逻辑）。 |
| [#7081](https://github.com/earendil-works/pi/pull/7081) | feat(ai): support Claude Opus 5 on Bedrock | 功能支持 | 为 Bedrock 上的 Claude Opus 5 配置自适应思维（adaptive thinking），并修复错误信息过于详细的问题。 |
| [#7046](https://github.com/earendil-works/pi/pull/7046) | feat: add provider-neutral prompt cache contracts | 基础架构 | 引入供应商无关的提示缓存合约，为后续跨提供商缓存管理奠定基础。 |

此外，仍有 10 个 PR 处于待合并状态，其中值得关注的有：
- [#7085](https://github.com/earendil-works/pi/pull/7085) feat(coding-agent): add vitest eval harness（添加评估测试框架）
- [#7032](https://github.com/earendil-works/pi/pull/7032) fix(coding-agent): expose unavailable scoped models（暴露不可用的作用域模型）
- [#6216](https://github.com/earendil-works/pi/pull/6216) feat: Add Amazon Bedrock Mantle OpenAI Responses provider（新提供商）
- [#7072](https://github.com/earendil-works/pi/pull/7072) fix(coding-agent): cache llama.cpp model catalog（修复缓存导致的启动问题）

## 4. 社区热点

以下 Issues / PRs 在今日获得最多评论和反应，反映了社区的核心关切：

### #6768 [Bug] Copilot Enterprise 无法进行压缩
- **链接**：https://github.com/earendil-works/pi/issues/6768  
- **12 评论 / 11 👍**  
- **诉求**：用户使用 Copilot Enterprise 许可证进行上下文压缩时，OpenAI API 返回 421 错误，Anthropic 模型也失败。该问题已持续一周（创建于 07-17），至今未分配或标注 `inprogress`，社区呼吁尽快修复。

### #6686 [Bug] Pi 自动登出 GitHub（重复问题）
- **链接**：https://github.com/earendil-works/pi/issues/6686  
- **12 评论 / 0 👍**  
- **背景**：该问题曾被报告过（#2725），现在 v0.80.7 仍复现。用户确认在 macOS 和 Linux 上独立安装均会遇到。社区诉求是彻底解决 OAuth token 失效问题，而不是仅通过环境变量绕过。

### #6922 [Bug] 默认模型为 llama.cpp 时启动显示 “No models available”
- **链接**：https://github.com/earendil-works/pi/issues/6922  
- **6 评论 / 10 👍**  
- **诉求**：用户希望将 llama.cpp 设置为默认提供商和模型，但 Pi 启动时因异步加载未完成而报错。已有 PR #7072 修复缓存问题，但用户仍希望默认模型能在初始化时直接应用。

### #7047 [Bug] Gemini 3.x 工具调用 ID 被剥离
- **链接**：https://github.com/earendil-works/pi/issues/7047  
- **4 评论 / 1 👍**  
- **诉求**：多轮工具对话中，`functionCall` 和 `functionResponse` 的 `id` 字段丢失，导致 Gemini 3.x 模型后续调用失败。用户认为这是一个严重的回归，需优先修复。

## 5. Bug 与稳定性

根据今日数据，报告了以下 Bug，按严重程度排列：

| 严重程度 | 编号及摘要 | 是否已有 Fix PR | 备注 |
|----------|------------|----------------|------|
| **严重** | [#6768](https://github.com/earendil-works/pi/issues/6768) Copilot Enterprise 压缩失败（421 错误） | ❌ 无 | 影响企业用户，已持续 8 天无进展 |
| **严重** | [#7047](https://github.com/earendil-works/pi/issues/7047) Gemini 3.x 工具调用 ID 丢失 | ❌ 无 | 多轮工具对话完全不可用 |
| **严重** | [#7067](https://github.com/earendil-works/pi/issues/7067) 模型切换中断会话（GPT 返回 HTML 错误 / Qwen `thinking` 400） | ❌ 无 | 三种不同故障模式，影响通用性 |
| **中等** | [#6948](https://github.com/earendil-works/pi/issues/6948) llama.cpp 默认模型/提供商未在启动时应用（竞态条件） | ✅ [#7072](https://github.com/earendil-works/pi/pull/7072) | 待合并中，预计可解决 |
| **中等** | [#6922](https://github.com/earendil-works/pi/issues/6922) llama.cpp 默认模型导致启动提示无可用模型 | ✅ [#7072](https://github.com/earendil-works/pi/pull/7072) | 同上 |
| **中等** | [#7020](https://github.com/earendil-works/pi/issues/7020) 压缩后有时不继续对话 | ❌ 无 | 用户报告在长会话协调器中频繁出现 |
| **中等** | [#7048](https://github.com/earendil-works/pi/issues/7048) 压缩摘要因 token 上限被截断（`stopReason: 'length'` 未检查） | ❌ 无 | 导致摘要不完整 |
| **中等** | [#6996](https://github.com/earendil-works/pi/issues/6996) Gemini 3.x 因缺少 `thought_signature` 工具调用失败 | ❌ 无 | 与 #7047 相关但现象不同 |
| **低** | [#6998](https://github.com/earendil-works/pi/issues/6998) 阿里云提供的 DeepSeek 应使用 `thinkingFormat: qwen` | ❌ 无 | 配置错误，生成模型映射需修正 |
| **低** | [#6872](https://github.com/earendil-works/pi/issues/6872) `/copy` 假成功（`wl-copy` 退出码未检查） | ✅ [#7009](https://github.com/earendil-works/pi/pull/7009) | 已合并 |
| **低** | [#7035](https://github.com/earendil-works/pi/issues/7035) 大型 `grep` 操作导致间歇性崩溃 | ❌ 无 | 仅在 DeepSeek v4 环境复现，建议提供更多日志 |
| **低** | [#6849](https://github.com/earendil-works/pi/issues/6849) HTML 导出在 Chrome 中空白（递归溢出） | ❌ 无 | 深层嵌套会话（2847 层）导出失败 |

**稳定性总结**：今日修复了 `wl-copy` 假成功、模型配置热重载、OpenAI 工具模式 `required` 归一化等几个影响面较广的 Bug。但仍有多个严重 Bug（特别是 Copilot Enterprise 压缩、Gemini 工具 ID 丢失）未分配或等待修复，需维护者优先关注。

## 6. 功能请求与路线图信号

社区今日提出的新功能需求（以 OPEN 且评论较多为准）：

| Issue 编号 | 功能请求 | 关联 PR | 可能纳入版本 |
|------------|---------|---------|--------------|
| [#7038](https://github.com/earendil-works/pi/issues/7038) | 在 TUI 编辑器中添加标准键盘文本选择（Windows 用户诉病） | 无 | 短期：社区呼声高，但实现复杂（需处理非 Vim 模式） |
| [#7040](https://github.com/earendil-works/pi/issues/7040) | 模型：按提供商作用域刷新 API（用于 `letta-code` 等调用方） | 无 | 短期：已有讨论，但 PR 尚未创建；可能进入 v0.83 |
| [#7026](https://github.com/earendil-works/pi/issues/7026) | `openai-completions`：允许通过 `compat` 覆盖发送 `prompt_cache_key` 给网关路由的 OpenAI 模型 | 无 | 短期：仅需修改条件判断，适合热修复 |
| [#7010](https://github.com/earendil-works/pi/issues/7010) | 自动归一化 OpenAI 兼容提供商的可选对象工具模式（与 #7050 类似） | ✅ [#7050](https://github.com/earendil-works/pi/pull/7050) | 已合并 |
| [#6881](https://github.com/earendil-works/pi/pull/6881) | 使用提供商报告的成本（PR：`feat(ai): use provider-reported cost`） | 待合并 | 中期：将为成本核算提供更准确数据 |

另外，已关闭的 #6886（支持 Anthropic 服务端 Fable-to-Opus 回退）被标记为 `no-action`，可能未被采纳；#3442（WebSocket 传输）已关闭，说明功能已在某版本中实现或因其他原因拒绝。

**路线图信号**：项目正逐步增强对多元推理引擎的支持（Constrained Sampling、Claude Opus 5 on Bedrock、Mantle Provider），同时优化开发者体验（缓存、测试治理）。TUI 性能优化是当前重点。

## 7. 用户反馈摘要

从今日 Issues 评论中提炼真实用户声音：

- **痛点**：
  - **Copilot Enterprise 用户无法压缩**（#6768）：*“If you compact context with PI using a Copilot Enterprise License you

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是为您生成的 LiteLLM 项目动态日报。

---

# LiteLLM 项目动态日报 | 2026-07-25

## 今日速览

过去24小时内，LiteLLM 项目保持了极高的活跃度，共计收到 85 条 Issues 和 187 条 PR 更新。项目发布了新的开发版本 `v1.95.0-dev.2`，重点在于基础设施与架构演进。社区讨论焦点集中在 **TPM/RPM 限速、MCP（Model Context Protocol）稳定性、以及 Claude Code 集成兼容性** 等关键痛点上。尽管合并率（24%）相对待合并数量偏低，但大量的功能 PR（特别是围绕 Rust 网关、MCP 及 UI 重构）表明项目正积极进行下一阶段的能力建设。

## 版本发布

### v1.95.0-dev.2
- **链接**: [Release v1.95.0-dev.2](https://github.com/BerriAI/litellm/releases/tag/v1.95.0-dev.2)
- **详情**: 该版本主要是一个开发里程碑版本，重点在于验证 Docker 镜像的签名机制。项目已采用 [cosign](https://docs.sigstore.dev/cosign/overview/) 对所有镜像进行签名，每个版本均使用同一密钥。
- **影响分析**:
    - **破坏性变更**: 此版本为预发布版本，无明确破坏性变更。用户在生产环境中应谨慎使用 `-dev` 标签。
    - **迁移注意事项**: 无。
    - **项目意义**: 此举是提升软件供应链安全的重要一步，确保用户下载的镜像是未被篡改的官方版本，对于企业级部署至关重要。

## 项目进展

今日合并/关闭的 PR 主要围绕功能修复和稳定性提升，关键进展如下：

- **核心功能修复**:
    - **[PR #34046] 修复 OpenAI 缓存写入计费**: 解决了 GPT-5 等模型在提示缓存创建时的 token 计费问题，确保 `cache_write_tokens` 被正确追踪并按缓存写入费率计费。
    - **[PR #34473] 修复 Vertex AI 批处理响应**: 处理了 Vertex AI 返回显式 `outputInfo: null` 时导致的崩溃问题，提升了批处理 API 的健壮性。
- **可观测性增强**:
    - **[PR #34537] 修复 MCP 工具调用的链路追踪**: 解决了 OpenTelemetry 追踪中，同一个 MCP 工具调用被拆分成两个不连续追踪段的问题，现在整个调用流程会锚定在同一个追踪中，便于排查。
- **生态集成**:
    - **[PR #34563] Rust 网关支持 Bedrock**: 为 Rust 实现的 `/v1/messages` 端点增加了对 Bedrock Anthropic 的原生调用支持，使得 Claude Code 用户可以通过高性能的 Rust 网关来路由 Bedrock 请求。
- **技术债清理**:
    - **[PR #33284] 依赖更新**: 批量更新了 19 个 GitHub Actions 依赖项，有助于提升 CI/CD 管道安全性与稳定性。

## 社区热点

今日讨论最热烈的问题反映了用户在生产环境中遇到的真实挑战：

1.  **#24677 虚拟键的 TPM 限速 Bug** (`👍: 4`, `评论: 15`)
    - **链接**: [Issue #24677](https://github.com/BerriAI/litellm/issues/24677)
    - **诉求**: 用户报告虚拟 API 键（virtual keys）的“每分钟 Token 数（TPM）”限速逻辑不正确。该问题曾在 v1.80.0 中被报告并标记为已解决，但在 v1.82.3 中依然存在。这是一个**严重且顽固的回归问题**，直接影响用户对多租户场景下的资源控制与计费准确性。

2.  **#8513 支持通过环境变量设置货币单位** (`👍: 1`, `评论: 19`)
    - **链接**: [Issue #8513](https://github.com/BerriAI/litellm/issues/8513)
    - **诉求**: 这是一个存在已久的 Feature Request，用户强烈要求能够通过环境变量修改 UI 中显示的货币符号（目前硬编码为 `$`）。在全球化部署的背景下，这反映了用户对**多区域、多币种本地化支持**的迫切需求。

3.  **#25296 SMTP 配置崩溃与重启** (`评论: 11`)
    - **链接**: [Issue #25296](https://github.com/BerriAI/litellm/issues/25296)
    - **诉求**: 用户在配置 SMTP 邮件服务时，点击测试按钮导致 LiteLLM 崩溃，重启后不断报出 `nacl.exceptions.ValueError: The nonce must be exactly 24 bytes long` 错误。这暴露出配置加密模块存在严重的稳定性问题，可能导致服务完全不可用。

## Bug 与稳定性

以下为今日报告的高严重度 Bug，按影响范围排列：

- **严重: TPM/RPM 限速逻辑回归** `[bug, proxy]`
    - **Issue**: [#24677](https://github.com/BerriAI/litellm/issues/24677)
    - **描述**: 虚拟键的 TPM 限制不生效，影响多租户资源控制。**尚无明确修复 PR。**

- **严重: MCP 路由上下文泄漏** `[bug, proxy]`
    - **Issue**: [#30416](https://github.com/BerriAI/litellm/issues/30416)
    - **描述**: 静态代码分析发现，在异步流中断场景下，MCP 路由中存在潜在的 `_mcp_active_toolset_id` 状态泄漏，可能导致错误的工具调用。

- **严重: 无限读取上游错误体导致事件循环阻塞** `[bug, proxy]`
    - **Issue**: [#34031](https://github.com/BerriAI/litellm/issues/34031)
    - **描述**: 代理在读取上游 API 错误响应体时未做大小限制。一个 114MB 的错误响应体导致代理进程内存膨胀和事件循环停滞。这是一个潜在的性能攻击面。

- **中等: MCP HTTP 客户端不转发会话 ID** `[bug, proxy]`
    - **Issue**: [#25128](https://github.com/BerriAI/litellm/issues/25128)
    - **描述**: HTTP MCP 代理客户端未将 `mcp-session-id` 转发给上游有状态服务器，导致工具列表永远无法正常加载。

- **中等: 安全扫描 (osv-scan) 在 Fork PR 中持续失败** `[Bug]`
    - **Issue**: [#34530](https://github.com/BerriAI/litellm/issues/34530)
    - **描述**: `gitpython` 和 `postcss` 等依赖的安全扫描在 Fork 仓库的 PR 中持续失败，堵塞了外部贡献者的代码提交流程。

## 功能请求与路线图信号

今日涌现的功能请求揭示了未来版本可能的演进方向：

1.  **MCP 生态深化**:
    - **[PR #34550](https://github.com/BerriAI/litellm/pull/34550)**: 新增 `gcp_service_account` 认证类型，为 GCP 托管的 MCP 服务器提供原生认证，解决了 GKE 用户需要部署旁路代理的痛点。
    - **[PR #34265](https://github.com/BerriAI/litellm/pull/34265)**: 在 MCP 的 OAuth 流程中遵循 RFC 8707 标准，支持发送 `resource` 参数，以兼容更严格的授权服务器。
    - **信号**: 项目正在积极增强 MCP 的认证和协议标准兼容性，这对构建安全、复杂的 Agentic 应用至关重要。

2.  **路由策略精细化**:
    - **[Issue #31876](https://github.com/BerriAI/litellm/issues/31876)**: 用户提出了一个关键功能：为**每个部署**独立配置 `allowed_fails` 熔断策略，而非当前全局统一的策略。这能更精细地管理不同类型模型（如实验性与生产性模型）的容错率。

3.  **门禁（Guardrail）扩展**:
    - **[Issue #19779](https://github.com/BerriAI/litellm/issues/19779)**: 用户提议为自定义门禁（Guardrail）添加“故障开放”模式。当前，如果门禁服务挂了，所有请求都会被阻塞（故障关闭），这在高可用场景下是不可接受的。

## 用户反馈摘要

从今日的 Issues 和评论中，可以清晰感受到用户的核心痛点：

- **“回归噩梦”**: Issue #24677 的评论揭示了用户对**功能回归**的强烈不满。一个在旧版本已被修复的 TPM 限速问题，在新版本中再次出现，动摇了用户对版本稳定性的信心。
- **“我在用，但它在崩”**: Issue #25296 的用户描述了配置 SMTP 时整个服务崩溃的体验，这与 #34281 中“健康检查不优雅”的反馈类似，反映用户对**后端服务鲁棒性和容错能力**的期望越来越高。
- **“试图新玩法，却被卡住”**: 多个关于 `Claude Code` + `Bedrock`/`Axure AI Foundry` 的 Bug（如 #26413, #26240, #27091）和 `web_search` 无法触发（如 #25191, #26252）的反馈，显示用户正**积极探索高级和混合部署场景**，但遭遇了兼容性阻碍。他们需要更稳定、更透明的“胶水”来连接各种尖端模型和工具。
- **“被审计锁死”**: Issue #34099 的反馈指出，`internal_user` 角色无法在 UI 上看到自己的请求日志，这在大企业审计场景下是**无法接受的痛点**。

## 待处理积压

以下是一些长期未响应或未解决但非常关键的 Issue，提醒维护者关注：

1.  **#14052 [P0] [Bug]: x-litellm-tags 路由不生效** (`opened: 2025-08-29`)
    - **链接**: [Issue #14052](https://github.com/BerriAI/litellm/issues/14052)
    - **原因**: 严重影响基于标签的模型路由和容错逻辑，被标记为 `P0` 和 `blocking use cases`。虽有讨论但尚未解决。

2.  **#14635 [Bug]: Timeout 错误信息显示“None 秒”** (`opened: 2025-09-17`)
    - **链接**: [Issue #14635](https://github.com/BerriAI/litellm/issues/14635)
    - **原因**: 这是一个非常低级的 UI/UX Bug，但影响面广（所有 SDK 用户），且`👍: 9`表明用户很在意。虽然看起来是小事，但“`None 秒`”的提示毫无调试价值。

3.  **#24152 [Bug]: Key 级别的模型 RPM/TPM 限制未触发 Fallback** (`opened: 2026-03-19`)
    - **链接**: [Issue #24152](https://github.com/BerriAI/litellm/issues/24152)
    - **原因**: 与今日最热 Issue #24677 密切相关，都是在处理细粒度限速与容错机制之间的互动关系。如果 #24677 解决了限速问题，此功能可能成为新版本的逻辑延伸。

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

好的，这是为您生成的 Temporal 项目 2026-07-25 动态日报。

---

## Temporal 项目日报 (2026-07-25)

### 1. 今日速览

过去24小时，Temporal 项目处于**非常活跃**的状态。尽管Issue更新较少（仅1条），但Pull Request活动量巨大，高达43条，其中17条已被成功合并或关闭。合并的PR涵盖了从核心功能优化（如移除旧版动态配置、修复调度器Bug）到依赖升级（SDK、API版本）等多个方面，表明项目在积极清理技术债务、提升稳定性的同时，也在持续推进新功能（如V2调度器、可编程故障注入）。社区关于是否应从正式Docker镜像中移除已废弃的 `tctl` 工具，引发了值得关注的讨论。

### 2. 版本发布
*(无)*

### 3. 项目进展

今日有17个PR被合并或关闭，以下为关键进展：

- **架构清理与稳定性提升**：
    - **移除旧版配置**：PR [#11133](https://github.com/temporalio/temporal/pull/11133) 被合并，移除了 `matching.enableMigration` 动态配置项，强制执行新的匹配逻辑。这表明该特性已成为默认行为，代码得到清理。
    - **修复并发安全问题**：PR [#11258](https://github.com/temporalio/temporal/pull/11258) 修复了在记录慢命名空间回调时的并发map崩溃问题，提升了系统在高并发下的稳定性。
    - **修复指标统计**：PR [#11247](https://github.com/temporalio/temporal/pull/11247) 被合并，修复了活动（Activity）在暂停（paused）状态下 `StartToClose` 延迟指标计算错误的问题，确保监控数据准确。

- **依赖项与API升级**：
    - **SDK和API版本更新**：项目集中升级了底层依赖，包括合并/关闭了 `upgrade SDK to v1.46.0` ([#11266](https://github.com/temporalio/temporal/pull/11266))、`upgrade SDK to v1.44.0` ([#11267](https://github.com/temporalio/temporal/pull/11267)) 和 `Update to API v1.63.4` ([#11264](https://github.com/temporalio/temporal/pull/11264))，紧跟社区最新发布。
    - **内部通信库升级**：PR [#11265](https://github.com/temporalio/temporal/pull/11265) 更新了 `ringpop-go` 和 `tchannel-go` 依赖，修复了内部的成员变更和错误处理问题。

- **功能修复与优化**：
    - **修复调度器Bug**：PR [#11162](https://github.com/temporalio/temporal/pull/11162) 修复了V2调度器在回填（backfill）时，因仅考虑容量限制而跳过部分时间范围的问题。
    - **限制内存使用**：PR [#11151](https://github.com/temporalio/temporal/pull/11151) 被合并，为分页的 `RespondWorkflowTaskCompleted` 请求添加了进程级和命名空间级的内存限制，防止单个错误请求耗尽系统资源。
    - **Nexus更新并发修复**：PR [#11254](https://github.com/temporalio/temporal/pull/11254) 修复了并发Nexus更新时，重复的更新请求可能导致调用者挂起的问题。

### 4. 社区热点

今日最受关注的讨论围绕 Issue [#11260](https://github.com/temporalio/temporal/issues/11260) 展开：

- **议题**：是否应该在Temporal Server 1.29.7的Docker镜像中继续包含已废弃且不再维护的 `tctl` 二进制文件？
- **诉求**：用户 `@haiping3` 指出 `tctl` 已废弃且仓库不再维护，继续包含不仅增加镜像体积，还可能给新用户造成困惑。
- **分析**：这是一个关于“代码清理”与“向下兼容”之间的经典博弈。一方面，移除废弃组件是健康项目应有的姿态；另一方面，可能仍有部分用户依赖Docker镜像中的 `tctl`。这需要项目维护者明确决策并给出合理解释。

### 5. Bug 与稳定性

| 严重程度 | 问题描述 | 状态 | 链接 |
| :--- | :--- | :--- | :--- |
| **高** | **并发Nexus更新导致调用者挂起**：当对同一个更新ID发起重复请求时，如果原始请求仍在“已受理”状态，新的回调可能不会被正确挂载，导致后续流程卡死。 | 已有修复PR [#11254](https://github.com/temporalio/temporal/pull/11254) | [Issue详情](https://github.com/temporalio/temporal/issues/11254) |
| **中** | **记录慢命名空间回调时可能发生并发map崩溃**：日志格式化操作本身未加锁，在高并发下可能触发 `fatal error: concurrent map iteration and map write`。 | 已有修复PR [#11258](https://github.com/temporalio/temporal/pull/11258) | [Issue详情](https://github.com/temporalio/temporal/issues/11258) |
| **中** | **复制应用时当前执行记录丢失可能导致任务无法处理**：当复制任务应用到一个“当前执行记录”已丢失的工作流时，系统会将其标记为坏消息（poison-pill）而无法处理。 | 已有修复PR [#11257](https://github.com/temporalio/temporal/pull/11257) | [Issue详情](https://github.com/temporalio/temporal/issues/11257) |
| **低** | **活动暂停时 `StartToClose` 延迟指标错误**：被暂停的活动不应记录 `StartToClose` 时间，因为此时尚无工作线程持有该活动，记录的指标具有误导性。 | 已合修复，`CLOSED` ([#11247](https://github.com/temporalio/temporal/pull/11247)) | [Issue详情](https://github.com/temporalio/temporal/issues/11247) |

### 6. 功能请求与路线图信号

今日的PR中透露了部分未来路线图的信号：

- **V2调度器（CHASM）持续完善**：多个PR（如 [#11271](https://github.com/temporalio/temporal/pull/11271)、[#11240](https://github.com/temporalio/temporal/pull/11240)、[#11223](https://github.com/temporalio/temporal/pull/11223)）专注于全新的CHASM V2调度器，涉及非正数Catchup窗口的处理、使用确定性UUIDv5生成请求ID、以及轮询时间跳跃完成状态等。这表明V2调度器正在从基础功能向生产级健壮性演进。
- **加强测试和可观测性**：PR [#9076](https://github.com/temporalio/temporal/pull/9076) 和 PR [#11269](https://github.com/temporalio/temporal/pull/11269) 提出了“可编程的gRPC故障注入”和“可编程的持久化故障注入”，旨在为回归测试提供更强大的工具，模拟各种棘手的错误场景。
- **代码架构重构**：PR [#11272](https://github.com/temporalio/temporal/pull/11272)（移动links_converter）和 PR [#11268](https://github.com/temporalio/temporal/pull/11268)（恢复并安全重构共享的内部连接缓存）体现了团队持续进行的小范围代码重构和优化。
- **时间跳跃（Time Skipping）功能**：PR [#11259](https://github.com/temporalio/temporal/pull/11259) 和 [#11223](https://github.com/temporalio/temporal/pull/11223) 为VTS（版本化时间跳跃）功能增加了运行时状态查询和轮询完成通知的API，这是为开发者提供更精细控制测试时间能力的信号。

### 7. 用户反馈摘要

- **关于废弃工具**：用户在 Issue [#11260](https://github.com/temporalio/temporal/issues/11260) 中对项目持续携带已废弃工具表达了**明确的不满和困惑**，认为这与清理代码库的目标相悖，并希望项目能对此决策给出合理解释。

### 8. 待处理积压

- **PR [#9076](https://github.com/temporalio/temporal/pull/9076)**：这是一个重要的**可编程gRPC故障注入**功能，自2026年1月19日开始，已持续开放超过6个月。虽然今日有更新，但尚未合并。该功能对于社区开发者和SRE进行混沌工程测试非常有价值，建议维护者关注其合并进度。

---

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*