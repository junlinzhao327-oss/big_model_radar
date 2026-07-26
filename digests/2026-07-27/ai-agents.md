# OpenClaw 生态日报 2026-07-27

> Issues: 342 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-26 22:36 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的OpenClaw项目数据，为您生成2026年7月27日的项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-07-27

## 1. 今日速览

项目社区活跃度极高，过去24小时内积累了342条Issue与500条PR的更新，其中PR合并/关闭率（48.6%）略低于新开率，表明评审团队压力较大。**稳定性**仍然是社区讨论的核心焦点，多个P1级别的关键Bug（如会话冲突、消息丢失、崩溃循环）持续有大量讨论，且部分问题已进入长期积压状态。开发团队的精力目前集中在一次大规模的**代码库重构与清理**上（以@steipete和@vincentkoc为主的“机械去重”系列PR），这预示着项目在追求更健康的架构，但短期内频繁的重构也可能引入新的回归风险。今日无新版本发布，但大量紧急修复PR正在排队。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

过去24小时内，项目团队合并/关闭了大量重要PR，主要集中在**代码库清理、关键Bug修复和新功能完整落地**三个方面。

- **核心架构重构**：由维护者@steipete主导的一系列“refactor”PR（如 #113649, #113626, #113648, #113576, #113596 等）被合并，涉及控制UI、Agent原生Hook中继、插件SDK、插件系统安全文件操作等核心模块的机械去重和逻辑拆分。这显著降低了项目的维护成本和后续功能开发的难度。
- **关键Bug修复**：多个影响用户体验的直接Bug被合入主线：
    - **修复终端UI权限问题**：PR #113644 修复了因缺少 `operator.write` 作用域导致TUI无法发送消息的问题。
    - **修复OpenAI HTTP身份验证**：PR #113638 修复了通过OpenAI兼容API调用时，所有者身份丢失导致某些工具权限异常的问题。
    - **修复UI性能问题**：PR #113623 修复了控制UI侧边栏多选归档时每行延迟2秒的性能瓶颈。
    - **修复原生应用重连**：PR #113634 修复了Android/iOS/macOS客户端在重新连接或切换窗口后，无法接收实时会话更新的问题。
    - **修复流式响应假完成**：PR #113629 修复了OpenAI Responses API流式请求在失败后可能无限等待或发送矛盾完成事件的问题。
- **新功能完善**：
    - **Claude Opus 5 完整支持**：PR #113633 合并，标志着对最新Claude Opus 5模型的运行时支持已完整落地，包括回退配置、原生快速模式等。
    - **插件系统增强**：PR #102293 (onepassword插件) 和 PR #112951 (SQLite WAL文件膨胀修复) 的合并，分别增强了密码管理集成和数据存储的健壮性。

**项目整体向前迈进了关键一步**：通过大规模重构提升了代码健康度，并修复了多个直接影响用户日常使用的严重Bug。

## 4. 社区热点

今日社区讨论热度最高的议题仍然集中在**平台扩展痛点**和**核心可靠性问题**上。

1.  **#75 [Linux/Windows Clawdbot Apps]** (评论: 115, 👍: 80)
    - **链接**: [https://github.com/openclaw/openclaw/issues/75](https://github.com/openclaw/openclaw/issues/75)
    - **分析**: 该项目是长期以来的社区焦点，以压倒性的评论和点赞数反映了社区对**跨平台桌面客户端**的强烈渴望。用户不满足于仅限macOS/iOS/Android的方案，追求在所有主流操作系统上获得一致的Agent交互体验。该项目的高热度也表明，社区核心用户希望将OpenClaw打造成一个普适的生产力工具，而不仅仅是开发者的CLI玩具。

2.  **#99241 [Tool outputs render as image attachments]** (评论: 24)
    - **链接**: [https://github.com/openclaw/openclaw/issues/99241](https://github.com/openclaw/openclaw/issues/99241)
    - **分析**: 此问题揭示了在复杂工作流中的一个致命缺陷：Agent无法读取自己的工具输出（因其被渲染为无法解析的图片附件）。这不仅导致任务失败，更暴露了**LLM与外部工具交互时的信息通道脆弱性**，引发了社区对Agent自主性和可靠性的广泛担忧。这是一个高价值的稳定性问题。

3.  **#102020 [Second message fails with reply session initialization conflicted]** (评论: 15)
    - **链接**: [https://github.com/openclaw/openclaw/issues/102020](https://github.com/openclaw/openclaw/issues/102020)
    - **分析**: 会话“第二句话就失败”的问题，直接打击了用户对聊天式AI助手的核心信任。该Bug在跨通道（Signal和Discord）上复现，表明这是一个**底层会话状态管理**的深层问题，而非单一通道的适配问题。社区对此类基础交互的稳定性要求极高。

4.  **#45049 [Agent allows simulated tool calls]** (评论: 7, 👍: 8)
    - **链接**: [https://github.com/openclaw/openclaw/issues/45049](https://github.com/openclaw/openclaw/issues/45049)
    - **分析**: 尽管评论数不多，但极高的点赞数表明这是一个“痛点共识”。用户发现Agent模型频繁通过文字描述“模拟”工具调用，而非实际执行，这让有确定性要求的自动化任务变得不可靠。这反映了社区对**Agent行为可控性和可预测性**的深度关切，是Agent应用走向工业级必须解决的关键问题。

## 5. Bug 与稳定性

今日社区报告的Bug集中在**会话状态损坏**、**消息丢失**、**特定平台/模型的兼容性崩溃**上，严重等级高。

- **P0 (灾难性)**:
    - **#90378**: 升级迁移导致cron任务默认模式变更，引发渠道错误。虽已“修复形状”，但影响范围广。 [链接](https://github.com/openclaw/openclaw/issues/90378)

- **P1 (严重)**:
    - **#99241**: Agent无法读取工具输出（渲染为图片附件），导致任务阻塞。**无修复PR**。 [链接](https://github.com/openclaw/openclaw/issues/99241)
    - **#102020**: 会话第二条消息即失败的“回复初始化冲突”。**无修复PR**。 [链接](https://github.com/openclaw/openclaw/issues/102020)
    - **#86519**: 5.20更新后Agent在Telegram上重复发送相同回复。**无修复PR**。 [链接](https://github.com/openclaw/openclaw/issues/86519)
    - **#94251**: Ollama远程Provider流未消费，导致会话卡死。**有相关PR(#113423可能是相关，但未在列表中)**。 [链接](https://github.com/openclaw/openclaw/issues/94251)
    - **#113315**: Telegram消息在偏移持久化后永久丢失。**无修复PR**。 [链接](https://github.com/openclaw/openclaw/issues/113315)
    - **#113474**: 树莓派5上的网关崩溃循环，引起在线/离线震荡。**无修复PR**。 [链接](https://github.com/openclaw/openclaw/issues/113474)

- **P2 (中等)**:
    - **#106403**: 由于更新时间竞态条件，主会话被静默重置。**无修复PR**。 [链接](https://github.com/openclaw/openclaw/issues/106403)
    - **#111519**: Telegram DM回复在最新测试版后降级。**无修复PR**。 [链接](https://github.com/openclaw/openclaw/issues/111519)
    - **#108473**: 回归：cron工具的Schema破坏了llama.cpp的工具调用功能。**无修复PR**。 [链接](https://github.com/openclaw/openclaw/issues/108473)

## 6. 功能请求与路线图信号

今日社区提出的功能需求显示出向**细粒度控制**和**专业应用场景**演进的趋势。

- **跨平台桌面端 (#75)**: 呼声最高的功能请求，有望成为下一阶段的核心开发目标。**无直接关联PR**。
- **Denylist支持 (#6615)**: 为`exec-approvals`添加黑名单，实现“默认放行，只阻止危险命令”的安全策略，提升了安全管控的灵活性。**有开放的关联PR**。
- **分布式Agent运行时 (#42026)**: 将单体网关拆分为“控制平面”和“运行时”的RFC，这是项目走向规模化、高可用性的必经之路。虽然处于早期阶段，但**今日合并的#113626（拆分Hook Relay）等重构PR正是为此铺路**。
- **按Agent配置记忆梦境 (#67413)**: 允许用户为不同Agent独立配置“记忆梦境”功能，避免全局梦境导致内存溢出。这表明用户对Agent管理提出了更高的粒度要求。**有开放的关联PR**。
- **支持Azure Foundry GPT Realtime Talk (#87325)**: 满足企业用户在特定云平台（Azure）上使用OpenClaw的需求。

## 7. 用户反馈摘要

从今日的Issue评论中，可以提炼出核心用户群体的几种典型声音：

- **“原生客户端是我的刚需”**：Issue #75 及其大量👍表明，用户需要一个像主流聊天软件一样原生的桌面客户端，而不是开一个网页或终端。他们是深度的、日常的Agent用户。
- **“我看不到Agent在做什么，这很可怕”**：Issue #99241 和 #102020 反映出当Agent无法读取自己的输出或在对话初期就失败时，用户感到**失控和沮丧**。这种“黑箱”感削弱了对Agent的信任。
- **“给我更多控制权”**：Issue #6615、#67413、#8299等表明，用户希望摆脱“一刀切”的配置，要求对Agent的行为（如安全策略、执行范围、回复方式）拥有**极细致的调节能力**。
- **“升级带来的破坏比新功能更让我头疼”**：多个Regression报告（如#86519, #111519, #108473）和升级迁移问题（#90378）显示，用户对版本间的兼容性和稳定性高度敏感，一次愉快的升级体验比任何新功能都更重要。

## 8. 待处理积压

以下为长期存在、社区高度关注但尚未取得突破性进展的重要问题，需要维护者给予关注。

- **#75 (Linux/Windows桌面客户端)**: 超过6个月的高需求Issue，至今无实现PR。是项目跨平台战略的最大短板。
- **#42026 (分布式Agent运行时RFC)**: 涉及项目未来架构演进的RFC，需要核心维护团队进行技术决策。
- **#85251 (Codex app-server卡死)**: 一个关键的P1级Bug，Agent运行时完全卡死直到超时回收，对生产环境威胁极大，已标记为“stale”。
- **#85844 (自动更新后缓存过期)**: 导致自动更新后功能异常的问题，影响了无缝升级体验。
- **#98938 (Gateway内存泄漏)**: 长期存在的OOM问题，迫使多账户Matrix网关用户每天重启，严重影响部署稳定性。

---

## 横向生态对比

# 2026-07-27 AI 智能体与个人助手开源生态横向对比分析

---

## 1. 生态全景

当前 AI 智能体/个人助手开源生态呈现 **“爆发式迭代与质量阵痛并存”** 的态势。头部项目（OpenClaw、Hermes）日处理 Issue/PR 超 500 条，社区参与度极高，但大量未合并 PR 与回归缺陷揭示出快速扩张带来的评审瓶颈。与此同时，项目间技术方向趋同——**跨平台客户端、细粒度权限控制、会话稳定性、分布式运行时** 成为多数项目共同攻坚点。LiteLLM 作为模型网关保持高频更新，Temporal 则作为底层编排引擎稳健迈向新版本，形成“前端 Agent + 后端工作流 + 中间件”的立体生态。

---

## 2. 各项目活跃度对比

| 项目 | 过去24h Issues (新开/活跃) | 过去24h PRs (新开/活跃) | 版本发布 | 健康度评估 |
|------|---------------------------|--------------------------|----------|------------|
| **OpenClaw** | 342 | 500 | 无 | ⚠️ 极高活跃，PR 合并率 48.6%，评审压力大；多个 P1 Bug 仍无修复 PR |
| **Hermes Agent** | 500+ | 500+ | 无 | ⚠️ 极高活跃，但大量回归缺陷；桌面端启动崩溃成最大痛点 |
| **OpenHands SDK** | 13 | 13（全部待合并） | 无 | 🟡 中等活跃，核心进展停滞（PR 零合并），积压严重 |
| **Pi** | 约27（关闭数） | 约8（关闭数） | 无 | 🟢 健康，维护者高效清理积压；核心 Bug（CPU 占满、WSL）仍在处理 |
| **LiteLLM** | 57 | 144 | 无 | 🟢 高活跃，合并/关闭 28 个 PR；安全漏洞 CVE 修复滞后 |
| **Temporal** | 1 | 12 | 无（v1.32.0 RC 准备中） | 🟢 稳健，发布分支已就绪；无重大回归 |

> 备注：OpenClaw 与 Hermes 数据包含大量评论/更新，非纯新开；Pi 的 Issue/PR 数主要指关闭项。

---

## 3. OpenClaw 在生态中的定位

- **核心参照项目**：被广泛 fork 与参考，其“机械去重”重构（@steipete 主导）引领代码库健康度提升方向。
- **技术路线**：侧重 **Agent 运行时、插件 SDK、多通道集成**，采用 “单体网关 + 模型适配层” 架构，正在通过重构（如 #113626 拆分 Hook Relay）向 **控制平面与运行时分离** 演进。
- **社区规模**：日处理 Issue/PR 量级与 Hermes 并列第一，但评论含金量更高（Bug 讨论深、功能需求理性）。跨平台桌面端缺失（#75）是最大短板，社区呼声远超 Hermes 同类需求。
- **与同类优势**：
  - 更完善的插件系统（每日合并安全文件操作、onepassword 等）
  - 对 Claude Opus 5、OpenAI Responses API 等模型支持的紧跟速度
  - 代码库重构意愿强烈，长期可维护性优于 Hermes（Hermes 仍处于“填坑”阶段）

---

## 4. 共同关注的技术方向

| 方向 | 涉及项目 | 具体诉求 |
|------|----------|----------|
| **跨平台桌面客户端** | OpenClaw (#75)、Hermes (#71226 等) | 原生 Windows/Linux 桌面端是社区第一梯队刚需 |
| **细粒度权限控制** | OpenClaw (#6615 Denylist)、Hermes (#527 RBAC) | “全有或全无”的二元授权模式无法满足团队协作 |
| **会话状态稳定性** | OpenClaw (#102020 会话冲突)、Hermes (#71480 DB 损坏)、OpenHands (#4192 对话丢失) | 基础会话常因竞态、Schema 损坏、重启而丢失 |
| **工具调用可靠性** | OpenClaw (#99241 工具输出变图片)、Hermes (#45049 模拟调用不规范) | Agent 无法读取自身输出或跳过实际执行，破坏自主性 |
| **TTS/多模态支持** | LiteLLM (#20078 Qwen3-TTS)、OpenHands (#3495 vision 检测) | 语音、图像模态集成仍不稳定 |
| **扩展系统/插件化** | Pi (#7137 pre_response 钩子)、LiteLLM (#34686 CLI 估算) | 允许第三方动态扩展 Agent 行为 |
| **可观测性** | Pi (#7146 Token 用量暴露)、LiteLLM (#34704 Prometheus 按区域归属) | 生产环境对端到端监控的迫切需求 |
| **安全漏洞治理** | LiteLLM (CVE-2026-28684)、Pi (#7090 CVE-2026-14257) | 依赖锁定导致安全修复阻塞 |

---

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent | OpenHands SDK | Pi | LiteLLM | Temporal |
|------|----------|-------------|---------------|----|---------|----------|
| **核心定位** | 全能 Agent 运行时 | 桌面端优先的团队协作 Agent | 开发者 IDE 内嵌 Agent SDK | 轻量级终端 Agent | 模型网关/代理 | 工作流编排引擎 |
| **目标用户** | 开发者/高级用户 | 团队、企业 | 软件开发者 | CLI 重度用户/远程工作者 | MLOps、平台运维 | 后端开发者、SRE |
| **技术架构** | 单体网关+插件 SDK (重构中) | 桌面端+远程网关 | SDK 库 (嵌入 IDE) | Node.js TUI+扩展 | Python 中间件 | Go 运行时+gRPC |
| **今日重点** | 代码重构、Bug 修复 | 桌面崩溃、网关权限 | 文件编辑器修复、并发控制 | TUI 性能、WSL 兼容 | 模型兼容、成本追踪 | VTS、SAA 测试 |
| **社区规模** | 极大（500+ PR/天） | 极大（500+ Issue/天） | 中等（13 PR/天） | 中高 | 高（144 PR/天） | 中（12 PR/天） |
| **核心优势** | 插件生态、重构意愿 | 桌面端集成度 | IDE 原生体验 | 轻量、终端友好 | 模型兼容广度 | 可靠性、分布式能力 |

---

## 6. 社区热度与成熟度分层

| 分层 | 项目 | 特征 |
|------|------|------|
| **🔥 快速迭代阶段（高热度、高 Bug 率）** | OpenClaw、Hermes Agent | 日更新超 500，复现大量回归缺陷；评审瓶颈明显，稳定性较差 |
| **🟢 快速迭代+质量巩固（热度高、回退少）** | LiteLLM、Pi | 活跃度高，但维护者能及时关闭/合并；Bug 修复与功能增强并行 |
| **🟡 质量巩固阶段（中等活跃、专注测试）** | Temporal | 发布准备中，合并以测试基础设施为主；单一 Issue 无重大回归 |
| **⏸️ 停滞风险（PR 零合并）** | OpenHands SDK | 13 个高质量 PR 全部待审 24h+，核心进展空转 |

---

## 7. 值得关注的趋势信号

1. **“轻量化终端 Agent”热度上升**：Pi 项目在处理 TUI 性能、WSL 兼容等细节问题，说明 Agent 正从 Web/桌面向终端环境下沉，适合 DevOps/远程工作场景。
2. **RBAC 与 Denylist 成为安全标配**：OpenClaw 和 Hermes 同时出现细粒度权限需求，反映出 Agent 从“个人玩具”向“团队生产工具”转型中的安全刚需。
3. **模型适配层（LiteLLM）承压加速**：新模型频出（Claude Opus 4.7、Qwen3-TTS、Perplexity 工具调用），LiteLLM 作为中间件必须快速补齐参数映射，否则将拖累上层 Agent 生态。
4. **工作流编排与 Agent 深度融合（Temporal VTS）**：Temporal 的虚拟时间跳过功能使异常测试更加可控，这是 Agent 应用进入生产环境前必须解决的“时间扭曲”难题。
5. **安全漏洞修复滞后成为共同隐患**：多个项目（LiteLLM、Pi）存在已知 CVE 但依赖锁定无法升级，建议开发者订阅项目安全公告并自行评估风险。
6. **开发者对“可观测性”诉求爆发**：Pi 的 Token 用量暴露、LiteLLM 的 Prometheus 成本归属、Temporal 的测试断言工具，说明社区已不满足于“能用”，追求“可度量、可审计”。

**对 AI 智能体开发者的参考建议**：
- 若构建面向团队的生产级 Agent，优先关注 **OpenClaw**（架构前瞻）和 **Hermes**（桌面生态），但需忍受阶段性不稳定。
- 若需快速集成多模型，**LiteLLM** 是最成熟的网关选择，但注意安全修复节奏。
- 若开发 IDE 插件或嵌入式 Agent，**OpenHands SDK** 虽然今日停滞，但其设计理念值得参考。
- 若需要可靠的工作流编排，**Temporal** 是业界标准，v1.32.0 的 VTS 功能将显著提升测试效率。
- **终端 Agent（Pi）** 适合对资源敏感、偏好 CLI 的开发者，但 WSL 支持需尽快完善。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我已根据您提供的 Hermes Agent GitHub 项目数据，为您生成了 2026-07-27 的项目动态日报。

---

### **Hermes Agent 项目动态日报 | 2026-07-27**

#### **1. 今日速览**

今日 Hermes Agent 项目呈现出极高强度的社区活跃度，过去24小时内处理了超过500条 Issue 和 500 条 PR，表明项目正处于大规模迭代与排查的高峰期。尽管未发布新版本，但社区讨论和技术贡献的热度空前。值得注意的是，大量 Issue 集中在桌面客户端（Desktop）的启动崩溃、网关连接及权限管理方面，而 PR 则主要围绕着各类 Bug 修复和内部架构优化。目前项目面临的主要挑战在于如何高效消化庞大的 Issue 积压，并将开放的 PR（383条待合并）平稳地合并入主分支。

- **活跃度评估**：极高。日活跃 Issue/PR 数量远超常规，社区参与热情高涨，但也伴随着大量回归缺陷和稳定性问题，反映出项目快速迭代的阵痛。

#### **2. 版本发布**

- **无新版本发布**：过去24小时内未发现任何新版本发布记录。

#### **3. 项目进展**

在过去24小时内，有数个重要的 PR 被合并，推动项目在稳定性和功能完善上取得进展：

- **桌面端 UI 与用户体验修复**：[@teknium1](https://github.com/teknium1) 的 PR [#72234] 合并了一次全面的仪表盘 QA 修复，解决了标题栏按钮被隐藏、日志颜色异常等六个核心 Bug，这些修复直接提升了用户操作体验。
- **核心会话状态修复**：[@buddhaholic420](https://github.com/buddhaholic420) 的 PR [#72231] 修复了桌面端“停止”操作与持久化中断标记之间的竞态条件，防止了错误的恢复流程。
- **门户组件回归修复**：PR [#45652](https://github.com/NousResearch/hermes-agent/pull/45652) 和 [#31863](https://github.com/NousResearch/hermes-agent/pull/31863) 解决了一个长期存在的回归问题：隐藏的聊天页面（ChatPage）会清空其他所有页面的头部操作按钮，这直接影响 Cron 页面等核心功能的可用性。

**项目评估**：项目在社区驱动下快速修正关键用户体验问题，修复的重点集中在桌面端和仪表盘。但大量未合并的 PR 表明，项目仍处于一个密集的输出阶段，需要加快审阅与合并流程。

#### **4. 社区热点**

本周讨论最热烈的议题主要集中在权限管理和平台集成上，反映了社区对更高程度定制化和专业场景支持的需求。

- **1. 细粒度网关权限控制 (Issue #527)**
  - **链接**: [https://github.com/NousResearch/hermes-agent/issues/527](https://github.com/NousResearch/hermes-agent/issues/527)
  - **分析**: 这是社区呼声最高的功能之一（15条评论，10个赞）。用户[@teknium1](https://github.com/teknium1)指出当前平台只有“全有或全无”的二元授权模型，无法满足企业级团队协作需求。该议题讨论引入RBAC（基于角色的访问控制），让团队可以安全地共享一个Hermes实例。

- **2. 集成新兴平台 Buzz (Issue #68871)**
  - **链接**: [https://github.com/NousResearch/hermes-agent/issues/68871](https://github.com/NousResearch/hermes-agent/issues/68871)
  - **分析**: 该议题获得了13个赞，显示社区对将 Hermes 与新兴的开源协作平台（如Block公司开源的Buzz）集成的强烈兴趣。用户希望 Agent 能融入“AI与人类共处一室”的新型工作空间，这预示着未来 Agent 生态的扩展方向。

- **3. Windows 桌面启动故障 (Issue #71226)**
  - **链接**: [https://github.com/NousResearch/hermes-agent/issues/71226](https://github.com/NousResearch/hermes-agent/issues/71226)
  - **分析**: 这是一个严重影响用户体验的 P1 级 Bug，导致 Windows 11 用户完全无法启动桌面应用。该问题在短时间内获得7条评论，用户被迫陷入重启循环，社区反应强烈。此 Bug 与 Windows 平台问题高度相关，是当前最需要优先解决的核心痛点。

#### **5. Bug 与稳定性**

今日报告的 Bug 频发，以桌面端和网关稳定性问题最为严重。按严重程度排列如下：

- **P1 - 严重 (Critical)**:
    - Windows Desktop 启动循环 (Issue [#71226](https://github.com/NousResearch/hermes-agent/issues/71226))：更新后无法启动，WebSocket连接立即断开。**已有 fix PR #72279 提及，但未直接修复。**
    - Desktop 工作目录设置失效 (Issue [#38855](https://github.com/NousResearch/hermes-agent/issues/38855) - 已关闭)：用户配置的`terminal.cwd`被UI缓存的旧值覆盖。昨日已解决。

- **P2 - 较高 (High)**:
    - 桌面端远程网关连接失败 (Issues [#48434](https://github.com/NousResearch/hermes-agent/issues/48434) - 已关闭, [#71305](https://github.com/NousResearch/hermes-agent/issues/71305) - 已关闭)：Windows和macOS用户均遇到登录认证和连接失败问题，特别是在更新后。昨日已解决。
    - `max_tokens` 设置被静默忽略 (Issue [#60388](https://github.com/NousResearch/hermes-agent/issues/60388))：影响所有使用参考模型或摘要生成器的用户，导致输出无限制，浪费token。
    - Kanban工人协议违规 (Issue [#27178](https://github.com/NousResearch/hermes-agent/issues/27178))：当Agent以文本回复而非API调用结束任务时，系统会产生误报，并且没有自动重试机制。
    - **状态数据库 Schema 损坏 (Issue [#71480](https://github.com/NousResearch/hermes-agent/issues/71480))**: 并发访问时，同时运行的 CLI 和进程可能会导致数据库结构损坏。**暂无有效修复 PR 与之对应。**

- **P3 - 中等 (Medium)**:
    - Kanban数据库索引损坏 (Issue [#34385](https://github.com/NousResearch/hermes-agent/issues/34385))：多进程并发写入导致SQLite数据库损坏。
    - ACP工具完成事件静默丢失 (Issue [#33023](https://github.com/NousResearch/hermes-agent/issues/33023))：客户端（如AionUI）无法得知工具调用已结束，导致界面永远显示“处理中”。

#### **6. 功能请求与路线图信号**

社区在解决现有问题的同时，也向项目提出了富有前瞻性的功能请求，部分已伴有合并请求，显示出快速落地的可能。

- **强路线图信号**：
    - **可插拔审批策略 (PR [#65734](https://github.com/NousResearch/hermes-agent/pull/65734), Issue [#64162](https://github.com/NousResearch/hermes-agent/issues/64162))**：这是一项重要的架构优化，通过`ctx.llm.complete(task=)`将插件的语言模型调用路由到已注册的辅助槽位。这为未来实现更复杂的、安全的工具调用审批工作流做了铺垫。
    - **桌面端国际化 (PR [#71573](https://github.com/NousResearch/hermes-agent/pull/71573))**：首个非英语语言界面（俄语）的PR已经提交，标志着项目在全球化方面迈出一步。
    - **执行策略支持 (PR [#66966](https://github.com/NousResearch/hermes-agent/pull/66966))**：在API模型路由中加入了执行策略，允许针对不同API端点灵活配置工具、推理能力等，将显著提升Gateway的灵活性与安全性。

- **有望进入下一版本**：
    - **macOS TCC 权限持久化 (PR [#68853](https://github.com/NousResearch/hermes-agent/pull/68853))**：该方案旨在解决更新后，Apple TCC权限被重置的问题。由于该问题影响巨大且有明确解决方案，有较大概率被纳入下一个版本。
    - **Jarvis 仪表盘 (PR [#72222](https://github.com/NousResearch/hermes-agent/pull/72222))**：一个集成的AI助手概览面板，可能在未来版本中成为核心功能入口。

#### **7. 用户反馈摘要**

- **痛点与不满**：
    - **更新后兼容性差**：多位Windows和macOS用户在评论中抱怨更新后 Desktop 应用无法启动或连接失败，甚至经历“循环重启”，极大地影响了日常使用。
    - **安全风险担忧**：用户[@ShengjiaCui](https://github.com/ShengjiaCui)报告了一个严重问题：Agent未经用户确认就执行了卸载命令 (`npm uninstall -g openclaw`)，这引发了社区对 Agent 默认行为安全性的广泛讨论和担忧。
    - **复杂配置与无声失败**：多个问题（如`max_tokens`、`kanban`协议）指向配置项虽然可以设置但被静默忽略，导致用户预期行为与实际不符，增加了排查问题的难度。
    - **单点故障与端口冲突**：社区中有人反馈，Agent在追求高度功能集成时，可能因单个组件（如网关）的卡死或一个端口的冲突，导致整个系统崩溃。这种单点故障模式让部分用户在使用时感到脆弱。

- **满意与期待**：
    - **对新集成的期待**：对于 Buzz 集成、Jarvis 仪表盘等提案，社区表达了强烈兴趣并点赞，认可项目在新兴平台和智能化发展方向上的探索。
    - **对精细权限控制的渴望**：社区对#527（网关权限分级）的积极反应表明，用户已不满足于简单的二元授权，渴望更专业、更细粒度的控制能力，以满足团队协作场景。

#### **8. 待处理积压**

以下为影响较大、但缺乏最新回应的关键问题，需提醒维护者关注：

- **架构性 Bug 待处理**：
    - [Issue #34385](https://github.com/NousResearch/hermes-agent/issues/34385): **Kanban DB 索引损坏**。自5月29日起，至今无有效修复PR，这是一个影响核心任务系统的隐蔽Bug。
    - [Issue #43731](https://github.com/NousResearch/hermes-agent/issues/43731): **Honcho 内存迁移重复执行**。受限于简单的检查条件，`migrate_memory_files()` 会在每次新会话中重复运行，造成大量重复数据。问题至今没有修复PR。

- **重要功能请求待决策**：
    - [Issue #527](https://github.com/NousResearch/hermes-agent/issues/527): **RBAC权限层级**。社区高票需求，但维护者尚未明确是否将其纳入路线图（标签`needs-decision`）。此功能对项目的商业化应用至关重要。
    - [Issue #39609](https://github.com/NousResearch/hermes-agent/issues/39609): **Kanban任务状态绕过**。`--initial-status blocked` 功能存在缺陷，1秒后自动转``ready``，绕过人工审批“关卡”，给部署带来严重风险。此Bug也需要维护者尽快决策。

- **长期未修复的兼容性问题**：
    - [Issue #5254](https://github.com/NousResearch/hermes-agent/issues/5254): **LM-Studio 工具调用重复**。使用LM-Studio作为Provider时，工具调用会异常拆分，此问题自4月5日报告以来一直未解决，严重影响本地模型用户的使用体验。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，以下是根据您提供的 OpenHands SDK 项目数据生成的日报。

---

# OpenHands SDK 项目日报 | 2026-07-27

## 1. 今日速览

过去24小时，OpenHands SDK 项目处于 **高活跃度但核心进展停滞** 的状态。Issue 和 PR 的更新数量均为 13 条，显示出社区参与度很高。然而，13 个 PR 全部处于 “待合并” 状态，没有新的合并或关闭，表明项目核心的代码审查和合并流程可能遇到了瓶颈。Bug 修复和功能增强的 PR 大量涌现，主要集中在文件编辑器、LLM 交互、安全性和系统稳定性等关键领域，体现了社区对项目质量的持续关注。值得注意的是，有 7 个长期悬而未决的 “Stale” Issue 被关闭，可能是维护者进行了一轮积压清理。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

由于过去 24 小时没有 PR 被合并，项目核心代码的实际推进处于停滞状态。但大量高质量的 PR 等待合并，预示着下一轮重大更新将非常丰富。

**亟待合并的关键 PR 包括：**

-   **核心系统修复：**
    -   `#4168` 修复了在特定推理模型（如Bedrock）上，由于预算钳制算法导致请求被提供商拒绝的错误。
    -   `#4165` 修复了 `fix(llm)` 模块中因空内容消息导致提示缓存崩溃的 `IndexError` 问题。
    -   `#4108` 修复了任务中断传播到子代理（subagents）的问题，保证了多任务协作的稳定性。
-   **文件编辑与搜索修复：**
    -   `#4163` 修复了在无换行符的末行插入文本时导致内容粘合的数据损坏问题，这对代码编写体验至关重要。
    -   `#4164` 修复了 grep 工具中 `*.{ts,tsx}` 等括号扩展模式无法匹配文件的问题。
-   **安全性与数据持久化：**
    -   `#4175` 修复了终端输出中可能泄露 Git 远程 URL 凭据的安全风险。
    -   `#4166` 修复了 `update_secrets` 方法无法持久化密钥，导致重启后密钥丢失的问题。
-   **新功能与集成：**
    -   `#4154` 为 OpenRouter 提供 API 余额查询端点，方便用户在 UI 中查看信用额度。
    -   `#4222` 修复了反向代理场景下 VSCode URL 生成不正确的问题，改善了部署体验。

## 4. 社区热点

-   **最活跃 Issue: `#2078 [Tracker] Daily Integration Runs`**
    -   **链接：** [https://github.com/OpenHands/software-agent-sdk/issues/2078](https://github.com/OpenHands/software-agent-sdk/issues/2078)
    -   **分析：** 该 Issue 作为日常集成运行的占位符，累积了 148 条评论，是项目长期监控和讨论的热点。虽然不直接反映社区功能诉求，但体现了项目对持续集成和质量控制的重视，是社区开发者持续关注的焦点。

-   **最受关注的 Bug 报告: `#3495 step-3.7-flash: vision support not detected at runtime`**
    -   **链接：** [https://github.com/OpenHands/software-agent-sdk/issues/3495](https://github.com/OpenHands/software-agent-sdk/issues/3495)
    -   **分析：** 该 Issue 获得了 1 个 👍，讨论持续了近两个月。问题核心是 SDK 无法正确识别某些模型的视觉能力（`supports_vision`），导致关键集成测试被跳过。这暴露了 LiteLLM 代理模式下，模型元数据获取机制的脆弱性，直接影响用户在某些模型上的多模态功能体验。

## 5. Bug 与稳定性

以下为过去 24 小时内报告的 Bug，按严重程度排列：

-   **严重 (Data Loss / Core System Crash):**
    -   `#4192 [Bug]: restarting agent-server quickly loses all historical conversations`
        -   **链接：** [https://github.com/OpenHands/software-agent-sdk/issues/4192](https://github.com/OpenHands/software-agent-sdk/issues/4192)
        -   **描述：** 快速重启 agent-server 会导致所有历史对话丢失。
        -   **状态：** 待处理，尚无关联的 fix PR。

-   **高 (Functionality Broken / Feature X-Ray):**
    -   `#3495 step-3.7-flash: vision support not detected at runtime`
        -   **链接：** [https://github.com/OpenHands/software-agent-sdk/issues/3495](https://github.com/OpenHands/software-agent-sdk/issues/3495)
        -   **描述：** SDK 无法检测模型的视觉支持能力，导致图像查看功能测试被跳过。
        -   **状态：** Issue 未关闭，但已有多个关于 LLM 能力的修复 PR (`#4167`, `#4168`) 在等待合并，可能与解决此问题相关。

## 6. 功能请求与路线图信号

-   **用户对余额查询功能的迫切需求：** `#4154` PR 提出为 OpenRouter 用户添加 API 余额查询端点。该 PR 评论虽少，但直击用户痛点——用户希望在 UI 内直接查看剩余额度，无需切换页面或使用命令行。这很可能被纳入下一版本。

-   **工具集管理的标准化呼声：** `#3978` Issue 指出默认工具集定义在三个仓库中有四个副本，缺乏权威性。这反映出随着项目增长，架构治理问题日益突出，社区建议 `create_agent` 作为单一控制点。这是长期项目健康度的重要信号。

-   **对多 Marketplace 支持的探索：** `#2494` Issue 提出支持多个 Marketplace 注册，并允许自动加载。虽然已标记为 Stale，但该需求表明了社区对技能生态系统可扩展性的关注，是未来项目生态繁荣的潜在基石。

## 7. 用户反馈摘要

从 Issues 评论中提炼出的用户痛点：

-   **数据持久化与稳定性是核心焦虑：** Bug `#4192` 和 `#4166` 均涉及到数据丢失问题。用户对“重启丢失对话”、“密钥不保存”这类问题表现出高度不满，这严重影响了工具在长期工作流中的可靠性。
-   **模型兼容性和配置困难：** Bug `#3495` 和 PR `#4167`、`#4168` 的并存，反映了用户在使用非主流模型或特定部署环境（如 LiteLLM, Bedrock）时，面临模型能力识别不准和参数配置冲突的困扰。用户期望更智能、更鲁棒的 LLM 适配层。
-   **安全意识的提升：** 关于 Git 凭据泄露的修复 PR `#4175` 说明用户对 AI 代理操作的透明度和安全性有很高期待。类似 `git remote -v` 这种看似安全的命令，在 AI 环境中也可能成为泄露渠道，用户对此敏感。

## 8. 待处理积压

-   **长期未回应的功能需求：**
    -   `#2494 feat: Support multiple marketplace registrations with auto-load semantics`
        -   **链接：** [https://github.com/OpenHands/software-agent-sdk/issues/2494](https://github.com/OpenHands/software-agent-sdk/issues/2494)
        -   **状态：** 标记为 Stale，自 2026-03-18 创建至今 4 个月。
        -   **建议：** 该 Issue 涉及技能生态的核心扩展能力，建议维护者评估其设计价值并给出反馈，避免扼杀社区创新动力。

-   **积压的“Stale”功能追踪 Issues：**
    -   **列表：** `#2040`, `#2041`, `#2036`, `#2039`, `#2043`, `#2053`, `#2065`
    -   **状态：** 这些 Issue 均在昨日被关闭，大多是 2026-02-13 创建的关于 Claude Code 功能对等的追踪任务。
    -   **分析：** 批量关闭旧追踪 Issue 是积极的信号，可能意味着维护者认为这些长期追踪的功能已不那么紧迫，或已通过其他方式解决。但这需要进一步观察，以确定是否有关键功能（如动态工具发现、任务依赖）再次被提上日程。

-   **大量待审查 PR 积压：**
    -   **状态：** 过去 24 小时内 13 个 PR 无人审核合并。
    -   **建议：** 项目维护者需要加速代码审查和合并流程。大量高质量的 Bug 修复 PR（如 `#4163` 文件编辑器修复）停留在 Draft/Open 状态，使得项目版本稳定性无法释放，也打击了贡献者的积极性。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，我将根据您提供的GitHub数据，生成 **Pi 项目 2026-07-27 的项目动态日报**。

---

### Pi 项目动态日报 | 2026-07-27

**项目名称:** Pi (github.com/earendil-works/pi)
**报告周期:** 2026-07-26 至 2026-07-27

---

#### 1. 今日速览

Pi 项目今日社区活跃度极高，是一个典型的“清理与沉淀日”。虽然无新版本发布，但维护者团队在过去24小时内处理了大量积压的 Issue 和 PR，关闭了27个 Issue 和8个 PR，表明项目正在积极消化社区反馈。社区报告的问题呈现多样化，从核心性能问题到跨平台兼容性细节均有涉及，反映出用户群的扩大和使用场景的深化。值得注意的是，关于 **TUI 性能**、**WSL路径处理** 和 **安全依赖更新** 等问题获得了较高关注。

#### 2. 版本发布

今日无新版本发布。

#### 3. 项目进展

今日项目进展主要体现在对遗留 PR 的合并以及对代码稳定性的修复上。

- **关键 PR 合并/关闭:**
    1.  **[攻击面/兼容性] Set AI_AGENT for child process attribution (#7131)**: 已合并。此 PR 顺应行业趋势，设置 `AI_AGENT=pi` 环境变量，使子进程能够识别启动它的主体是 Pi，增强了与其他开发工具的互操作性。这是个重要的生态信号。
        [链接](https://github.com/earendil-works/pi/pull/7131)
    2.  **[平台修复] 多项跨平台路径修复**: 由社区贡献者 @IKEASven69 提交的多个修复被合并，包括修复 Windows 路径分隔符在 Footer 中显示错误的问题 (#7124)，以及修复核心工具 `write`、`find` 和 `truncateLine` 中的字节计数不准和逻辑错误 (#7122)。这显著提升了 Pi 在 Windows 平台上的使用体验和核心工具的可靠性。
        - [PR #7124](https://github.com/earendil-works/pi/pull/7124)
        - [PR #7122](https://github.com/earendil-works/pi/pull/7122)
    3.  **[用户体验] 显示 SYSTEM.md 上下文状态 (#7120)**: 已合并。此 PR 在启动时增加了一个 Banner，提示用户 `SYSTEM.md` 和 `APPEND_SYSTEM.md` 是否生效，解决了长期存在的“系统提示文件静默生效”的问题，提升了透明度。
        [链接](https://github.com/earendil-works/pi/pull/7120)
    4.  **[稳定性/性能] TUI 缓存优化 (#7129)**: 已合并。针对 TUI 渲染中 `visibleWidth` 缓存抖动问题，将缓存容量从512提升至4096并改用LRU淘汰策略，有助于改善长会话下的终端渲染性能。
        [链接](https://github.com/earendil-works/pi/pull/7129)

- **项目里程碑信号:** 大量 Issue 被归为“[untriaged]”并关闭，这可能是维护团队正在进行大规模的“分类和沉默处理”，为下一阶段的功能开发或重大版本做准备。

#### 4. 社区热点

今日社区讨论主要集中在以下两个热点话题：

1.  **核心性能与架构问题:**
    - **[Issue #6665] TUI pins a full core while streaming (TUI在流式输出时占用完整CPU核心):** 此Issue获得8条评论，是目前**仍在进行中**的最重要Bug。社区深入分析了原因，指出是 `Intl.Segmenter` 未缓存和每次chunk都进行Markdown重建导致的高CPU占用。这直接影响到用户长时间使用TUI的体验，是亟需解决的核心性能瓶颈。
        [链接](https://github.com/earendil-works/pi/issues/6665)
    - **[Issue #4877] Session folder collision (会话文件夹碰撞):** 这是讨论最久的话题，共21条评论。社区指出了会话文件夹命名方式存在缺陷，不同路径可能映射到同一文件夹，可能导致数据冲突。虽然被标记为“小问题”，但用户担忧其潜在的破坏性。
        [链接](https://github.com/earendil-works/pi/issues/4877)

2.  **跨平台与兼容性问题:**
    - **[Issue #7064] WSL absolute windows paths are mishandled (WSL下Windows绝对路径处理错误):** 获5条评论和1个👍。此问题阻碍了WSL用户在文件操作工具（`read`/`write`/`edit`）上的正常使用，属于严重的平台兼容性Bug。社区反响强烈，期待修复。
        [链接](https://github.com/earendil-works/pi/issues/7064)

#### 5. Bug 与稳定性

今日报告的Bug数量较多，按严重程度排列如下：

- **严重 (影响核心功能)**
    1.  **[WSL路径错误] WSL absolute windows paths are mishandled (#7064)**: 核心文件操作工具在WSL下无法正确解析Windows路径，导致功能异常。**无修复PR。**
        [链接](https://github.com/earendil-works/pi/issues/7064)
    2.  **[CPU性能倒退] TUI pins a full core while streaming (#6665)**: 导致CPU满载，影响TUI可用性。**无修复PR，正在排查。**
        [链接](https://github.com/earendil-works/pi/issues/6665)
    3.  **[静默数据丢失] RPC prompt during in-flight compaction: silently dropped (#7150)**: 在会话压缩期间通过RPC提交指令，系统ACK成功但指令丢失，属于静默数据丢失。**无修复PR。**
        [链接](https://github.com/earendil-works/pi/issues/7150)
    4.  **[命令截断] bash tool silently truncates long commands (#7136)**: `bash`工具静默截断长命令，导致部分代码未执行且无报错。**无修复PR。**
        [链接](https://github.com/earendil-works/pi/issues/7136)

- **中等 (影响特定功能/平台)**
    1.  **[未检查的依赖CVE] Regenerate 0.82.x shrinkwrap with brace-expansion 5.0.8+ (#7090)**: 存在已知DoS漏洞的依赖。**无修复PR。**
        [链接](https://github.com/earendil-works/pi/issues/7090)
    2.  **[二进制兼容性] Standalone linux-x64 binary SIGILL on pre-Haswell CPUs (#7149)**: 官方发布的Linux二进制包在旧CPU上崩溃。**无修复PR。**
        [链接](https://github.com/earendil-works/pi/issues/7149)
    3.  **[代理问题] Upgrade Undici to 8.8.0 for correct plain-HTTP proxy forwarding (#7049)**: 使用HTTP代理时连接非HTTPS的MCP/API目标会失败。**无修复PR。**
        [链接](https://github.com/earendil-works/pi/issues/7049)

- **轻微 (用户体验/UI问题)**
    - **多项 TUI 问题**: 包括Kitty终端退格键异常 (#7130)、重命名会话需要按两次Enter (#7126)、tmux下无法显示图片 (#7125)、Windows路径分隔符显示错误 (#7123)。**已有部分修复PR。**

#### 6. 功能请求与路线图信号

今日收到的功能请求指向以下方向，部分已有对应PR：

- **可观测性与开发者体验:**
    - **[Issue #7152] Add a read-only provider/model auth preflight command**: 请求增加非交互式的认证预检命令。`[closed]`
    - **[Issue #7146] Workflow: include token usage in agent_result / run_complete events**: 请求在工作流日志中增加Token用量信息。`[closed]`
    - **[PR #7151] Expose pending stop reason while streaming**: 已提出PR，建议在流式响应中提前暴露“停止原因”，让用户可以判断是否是最终答案。 **状态: OPEN**
        [链接](https://github.com/earendil-works/pi/pull/7151)

- **扩展性与架构演进:**
    - **[Issue #7119 / PR #7118] Expose extension context clear callback**: 用户提出并贡献了代码，允许扩展在不生成摘要的情况下清除会话上下文。**PR已合并。**
        [链接](https://github.com/earendil-works/pi/pull/7118)
    - **[PR #7148] Experimental loadout management**: 由知名贡献者@mitsuhiko提出的实验性功能，允许在会话中动态启用/禁用扩展。**状态: OPEN**
        [链接](https://github.com/earendil-works/pi/pull/7148)
    - **[Issue #7137] Extension hook request: pre_response / before_send_message gate**: 请求增加一个钩子，让扩展可以在AI回复发送给用户前进行拦截、修改或审查。`[closed]`

- **特定模型/提供商支持:**
    - **[Issue #7135] Support OpenAI 5.6 Pro modes**: 请求支持OpenAI Pro模式。`[closed]`
    - **[Issue #7143] Z.AI providers send max_completion_tokens, which Z.AI ignores**: 报告了特定提供商Z.AI的API兼容性问题。`[closed]`

**路线图信号:** 社区对**扩展系统的深化**（如动态加载、回调钩子）和**可观测性**（Token用量、状态预判）的需求非常强烈。@mitsuhiko提出的`/loadout`功能（PR #7148）很可能是下一个重要功能点。

#### 7. 用户反馈摘要

从今日的 Issue 和评论中，可以提炼出以下用户反馈：

- **痛点：WSL体验差。** 用户 @lionkor 报告了核心工具在WSL下无法工作的严重问题，直接影响了日常使用。
    > “When the agent tries to use the `read`, `write` or `edit` tools, it regularly fails...” – [链接](https://github.com/earendil-works/pi/issues/7064)
- **需求：对核心性能不满。** 用户 @axelbaumlisto 对TUI长会话时的CPU占用问题进行了深入分析，体现了高级用户的专业度，也反映出该问题对日常工作的困扰。
    > “Long sessions: the TUI uses ~100% of one core while the model streams.” – [链接](https://github.com/earendil-works/pi/issues/6665)
- **期望：更强大的扩展系统。** 多条Issue和PR（如#7119, #7137）表明，高级用户不满足于现有扩展能力，希望拥有更灵活的会话控制、内容审查和生命周期管理能力。
- **正面反馈：部分修复获得好评。** 关于路径显示和核心工具Bug的修复PR（#7124, #7122）被迅速合并，显示出项目对用户反馈的积极响应。

#### 8. 待处理积压

以下为需要维护者重点关注的历史或高价值未解决问题：

- **[功能请求] [Issue #1086] Add structured output (JSON schema) support (已关闭)**: 这是一项自1月30日提出的功能请求，今日被关闭。它标志着社区对**确定性输出**的长期需求，虽然关闭，但作为路线图参考仍有价值。
    [链接](https://github.com/earendil-works/pi/issues/1086)

- **[高价值Bug] [Issue #6665] TUI pins a full core while streaming**: 这是目前在执行中的、影响最广的性能问题，技术细节已分析透彻，亟需开发团队介入。
    [链接](https://github.com/earendil-works/pi/issues/6665)

- **[重要Bug] [Issue #7064] WSL absolute windows paths are mishandled**: 影响WSL用户核心功能的Bug，目前无修复方案。
    [链接](https://github.com/earendil-works/pi/issues/7064)

- **[安全] [Issue #7090] Regenerate 0.82.x shrinkwrap ... CVE-2026-14257**: 涉及已知安全漏洞的依赖更新，应尽快处理。
    [链接](https://github.com/earendil-works/pi/issues/7090)

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

好的，根据您提供的LiteLLM GitHub数据，以下是为您生成的2026年7月27日项目动态日报。

---

# LiteLLM 项目动态日报 — 2026-07-27

## 1. 今日速览

过去24小时，LiteLLM项目保持高度活跃。共处理57条Issue（新开/活跃42条，关闭15条）和144条PR（待合并116条，已合并/关闭28条），无新版本发布。社区提交的Bug主要集中在Redis限流器性能优化、Anthropic Opus 4.7参数兼容性、Ollama推理参数映射以及MCP工具过滤等问题上。同时，多个涉及预算窗口原子操作、会话预算并发控制、多次调用端到端测试覆盖的修复PR被提交，表明项目在并发安全与成本追踪精度方面有持续投入。整体项目健康度良好，但安全漏洞报告和CVE修复的等待时间较长，需要引起注意。

## 2. 版本发布

无。

## 3. 项目进展

过去24小时关闭/合并了28个PR，推进了以下关键领域：

- **稳定性和正确性**：
    - [#27577](https://github.com/BerriAI/litellm/pull/27577) 修复了Guard主分支工作流，将外部贡献者的PR指引目标从不存在分支改为正确的`litellm_internal_staging`分支。
    - [#29279](https://github.com/BerriAI/litellm/pull/29279) 将ddtrace下限提升至2.19.2，解决了Python 3.13上`/embeddings`端点因字节码重写bug导致的“协程已执行”崩溃。
    - [#25971](https://github.com/BerriAI/litellm/issues/25971) (已关闭) 支持Anthropic Claude Opus 4.7的`task_budget`参数。
    - [#26007](https://github.com/BerriAI/litellm/issues/26007) (已关闭) 更新了Perplexity API以支持工具调用等新特性。
    - [#26053](https://github.com/BerriAI/litellm/issues/26053) (已关闭) 修复了流式文本补全API中`ssl_verify=false`失效的问题。
    - [#34690](https://github.com/BerriAI/litellm/issues/34690) (已关闭) 修复了`tool_calls`条目形状不匹配时被静默丢弃的问题。
    - [#25966](https://github.com/BerriAI/litellm/issues/25966) (已关闭) 修复了当`allow_requests_on_db_unavailable: true`时Datadog APM对每个请求都生成错误跨度的问题。

- **测试与CI**：
    - [#34649](https://github.com/BerriAI/litellm/pull/34649) 新增了大量厂商API策略的端到端测试覆盖。

- **新功能与集成**：
    - [#34697](https://github.com/BerriAI/litellm/pull/34697) 添加了GreenPT作为本地提供者，支持聊天、嵌入和重排序。
    - [#34484](https://github.com/BerriAI/litellm/pull/34484) 添加了Gondala作为OpenAI兼容提供者。

这些合并/关闭项表明项目在修复旧Bug、增强测试套件以及拓展新模型提供者方面持续前进。

## 4. 社区热点

- **#31880 - 速率限制器Redis写优化** (9条评论): [链接](https://github.com/BerriAI/litellm/issues/31880)  
  用户@deepanshululla指出，当前速率限制器在每次LLM调用后都会无条件向Redis写入计数器，即使API密钥、用户或团队没有配置任何速率限制，造成性能浪费。社区对此高度关注，讨论如何在无限制时跳过写操作，反映了生产环境下对性能优化的强烈需求。

- **#26444 - Anthropic Opus 4.7 `temperature`参数兼容性** (6条评论，2个👍): [链接](https://github.com/BerriAI/litellm/issues/26444)  
  用户反馈`get_supported_openai_params`仍然将`temperature`列为Anthropic Claude Opus 4.7的支持参数，而实际该模型已废弃temperature，导致请求被拒绝。此问题已持续数月并拥有2个赞，表明社区对LiteLLM参数映射准确性的关注度较高。

- **#20078 - `/v1/audio/speech`对Qwen3-TTS失败** (6条评论): [链接](https://github.com/BerriAI/litellm/issues/20078)  
  用户@miesgre报告使用LiteLLM代理服务Qwen3-TTS时，`voice`参数被强制要求但会被剥离，导致请求失败。该问题自1月创建，至今仍是开放状态，说明TTS模态的支持还有待完善。

- **#25191 - Bedrock `websearch_interception`智能体循环不触发** (6条评论): [链接](https://github.com/BerriAI/litellm/issues/25191)  
  用户报告在使用AWS Bedrock和`/chat/completions`端点时，`websearch_interception`的智能体循环未触发。该问题涉及Bedrock特有行为，可能影响使用Bedrock作为后端的代理部署。

## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | Bug 描述 | Issue/PR 链接 | 是否有修复 PR |
|----------|---------|----------------|---------------|
| **高** | 安全漏洞CVE-2026-28684：`python-dotenv`钉死在1.0.1导致无法修复 | [#26333](https://github.com/BerriAI/litellm/issues/26333) | 无 |
| **高** | `aiohttp==3.13.3`存在10个CVE，而旧版3.13.5已修复 | [#26190](https://github.com/BerriAI/litellm/issues/26190) | 无 |
| **中** | LLM分类器`NoneType`没有属性`update`导致崩溃 | [#34487](https://github.com/BerriAI/litellm/issues/34487) | 无 |
| **中** | Ollama的`reasoning_effort`映射因使用不可哈希的字典导致崩溃，且错误强制在线程模型上启用`think` | [#34574](https://github.com/BerriAI/litellm/issues/34574) | 无 |
| **中** | `ollama_chat`通过Anthropic适配器流式输出时，工具调用`stop_reason`错误且多出空文本块 | [#34692](https://github.com/BerriAI/litellm/issues/34692) | 无 |
| **中** | Fireworks AI流式响应中`<think>`标签泄漏到`content`而非填充`reasoning_content` | [#26326](https://github.com/BerriAI/litellm/issues/26326) | 无 |
| **低** | `PrismaWrapper.__getattr__`死锁事件循环30秒导致存活检查失败 | [#26192](https://github.com/BerriAI/litellm/issues/26192) | 无 |
| **低** | Admin UI路由器设置在`fallbacks`为字典类型时崩溃 | [#26473](https://github.com/BerriAI/litellm/issues/26473) | 无 |

此外，多个过去24小时内提交的修复PR（如#34741、#34742、#34740等）针对代理中的并发安全问题（TPM限流器、会话预算超支、预算窗口更新原子性等），这些PR待合并，有望在近期解决相关稳定性问题。

## 6. 功能请求与路线图信号

- **#34686 - CLI子命令`litellm cost-estimate`** (3条评论): [链接](https://github.com/BerriAI/litellm/issues/34686)  
  用户希望提供独立的预部署成本估算CLI命令，而不仅限于通过`completion_cost()`函数。如果实现，将提升开发者体验。

- **#34662 - 提供商凭据的周期性可用性计划** (3条评论): [链接](https://github.com/BerriAI/litellm/issues/34662)  
  用户建议允许为提供商凭据定义重复的可用性时间段（如仅工作日可用），用于部署调度。这可能是未来多地域/多时段资源管理的方向。

- **#34704 - Prometheus导出器无法按区域或调用类型归属开销** (1条评论): [链接](https://github.com/BerriAI/litellm/issues/34704)  
  运营团队需要更细粒度的可观测性，以便按区域和调用类型（如Azure OpenAI vs Bedrock）区分支出、延迟和流量。该请求来自Discord讨论，可能被纳入后续监控增强路线图。

- **#34726 - 使`user_api_key_cache`内存大小可配置** (待合并PR): [链接](https://github.com/BerriAI/litellm/pull/34726)  
  PR实现了缓存条目数量的配置化，对于拥有大量活跃虚拟密钥的生产环境尤为重要，有望在近期合并。

- **#29378 - 在fallback查找路径上解析`model_group_alias`** (待合并PR): [链接](https://github.com/BerriAI/litellm/pull/29378)  
  该PR修复了使用模型组别名时fallback失效的问题，表明社区对路由别名和fallback机制的成熟度有较高要求。

## 7. 用户反馈摘要

- **性能与成本**：用户@mangabits在[#34727](https://github.com/BerriAI/litellm/issues/34727)中指出，文档中关于`REDIS_URL`在性能方面不推荐用于生产的警告已经过时，实际性能差异已被修复，建议更新文档。
- **端到端测试**：用户@mubashir1osmani在多个PR中（如#34739、#34649）关注测试套件的可靠性，例如硬编码localhost:4000导致端到端测试失败，通过环境变量解决。
- **兼容性与异常处理**：多位用户（如@jehunt1548、@technobenja、@leftathome）反映了参数映射不准确导致的请求错误，社区对支持新模型版本的及时性有较高期待。
- **安全与依赖**：用户@bhadrim两次报告CVE问题（python-dotenv、aiohttp），强调依赖版本锁定带来的安全风险，希望项目松弛版本约束以允许用户自行升级。

## 8. 待处理积压

- **#24404 - 安全漏洞报告无人审查** (已关闭，stale): [链接](https://github.com/BerriAI/litellm/issues/24404)  
  用户@regaan于3月23日通过huntr提交了4份安全报告，截至7月26日仍无任何审查回复。虽然该Issue已被标记为stale并关闭，但安全问题不容忽视。建议维护者主动联系报告者或通过私有渠道处理。

- **#20078 - `/v1/audio/speech`对Qwen3-TTS失败** (开放超过6个月): [链接](https://github.com/BerriAI/litellm/issues/20078)  
  该Issue自1月30日创建，至今未得到实质性修复或回应，可能影响部分TTS使用场景。建议维护者评估优先级。

- **#26170 - Ollama provider的`api_base`解析顺序与OpenAI不一致** (2条评论): [链接](https://github.com/BerriAI/litellm/issues/26170)  
  用户@aydenious指出LiteLLM中Ollama提供者优先使用全局`litellm.api_base`而非显式传入的`api_base`参数，与其他提供者行为不一致。该问题虽轻微但影响开发体验，可安排修复。

- **#26184 - xAI的`grok-imagine-image`模型在`/images`端点不可用** (2条评论): [链接](https://github.com/BerriAI/litellm/issues/26184)  
  该功能缺失影响图像生成场景，用户已正确定义模型但无法通过端点使用，可能需要检查端点注册逻辑。

---

**数据来源**：GitHub Issues / Pull Requests  
**分析日期**：2026-07-27  
**数据时段**：2026-07-26 至 2026-07-27 (UTC)

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报 | 2026-07-27

---

## 1. 今日速览

- 过去 24 小时内，项目共产生 **12 条 PR 更新**，其中 3 条已合并/关闭，9 条仍在开放审查中；Issues 仅新增 **1 条**，为潜在内存泄漏 Bug。
- 发布分支准备 PR（#11292）已被合并，表明 **v1.32.0 版本即将发布**，社区期待的新功能（如虚拟时间跳过、SAA 声明式测试等）有望随之落地。
- 核心贡献者在虚拟时间跳过（VTS）、活动处理器（SAA）、Nexus HTTP 故障注入等多个方向上持续提交代码，**项目整体活跃度较高**，开发节奏稳健。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

当日合并/关闭的 **3 条 PR** 推动了如下工作：

| PR 编号 | 标题 | 内容摘要 |
|---------|------|----------|
| [#11292](https://github.com/temporalio/temporal/pull/11292) | 1.32.0: Prepare release branch | 自动化的发布分支准备：覆盖治理文件、更新依赖关系。标志 v1.32.0 版本已进入预发布阶段。 |
| [#11149](https://github.com/temporalio/temporal/pull/11149) | SAA: declarative functional tests | 引入 `driveTrace()` 工具，允许用声明式事件序列驱动活动处理器（SAA）的端到端测试，极大降低手动编写测试用例的成本。 |
| [#11286](https://github.com/temporalio/temporal/pull/11286) | Update test shard salt | 自动优化测试分片策略，提升 CI 并行效率。 |

> **整体进展**：测试基础设施持续完善，SAA 回归测试将更全面；v1.32.0 发布在即，路线图功能（如 VTS）的合并窗口逐渐收窄。

---

## 4. 社区热点

当日最受关注的 Issue 为 **#11289**（潜在 Bug），报告了 Frontend/Admin 接口在反复调用 `Add/Remove/List/GetSearchAttributes` 或 `AddOrUpdateRemoteCluster` 时存在未缓存的 gRPC 连接泄漏。虽然尚无评论，但该问题直接影响服务稳定性，已引发核心团队的初步关注。

- **链接**：[#11289](https://github.com/temporalio/temporal/issues/11289)
- **诉求**：修复内存/goroutine 无限增长，要求复用或显式关闭内部 gRPC 连接。

另外，多位贡献者在 **VTS（虚拟时间跳过）** 功能上集中发力，三条相关 PR（#11220、#11259、#11223）均处于开放状态且密集更新，反映出该特性是当前社区开发热点。

---

## 5. Bug 与稳定性

| 严重程度 | Issue # | 标题 | 状态 | 备注 |
|----------|---------|------|------|------|
| **高** | [#11289](https://github.com/temporalio/temporal/issues/11289) | Frontend/Admin SearchAttributes 和 AddOrUpdateRemoteCluster 处理程序每次调用泄漏未缓存的 grpc.ClientConn | OPEN | 暂无 Fix PR，建议尽快修复以避免内存泄漏在生产环境累积。 |

其余 PR 中，[#11290](https://github.com/temporalio/temporal/pull/11290) 针对“已到期的活动调度任务”改用即时队列而非定时器队列，属于性能优化而非回归修复。

---

## 6. 功能请求与路线图信号

### 强烈信号：虚拟时间跳过（VTS）功能接近成熟
- [#11220](https://github.com/temporalio/temporal/pull/11220) 增加 `max skip` 字段、`TimeSkippingInfo` 及快速推进 Poll API；
- [#11259](https://github.com/temporalio/temporal/pull/11259) 增加运行时字段、改进跨 Run 传播行为；
- [#11223](https://github.com/temporalio/temporal/pull/11223) 实现快速推进的 Soft Timeout 和通知机制。

以上三条 PR 均出自同一作者 @feiyang3cat，且均在迭代更新，预计将在 v1.32.0 或后续版本中正式发布。

### 其他新增功能
- **Nexus HTTP 故障注入**（[#11295](https://github.com/temporalio/temporal/pull/11295)）：允许在测试中确定性模拟出站 Nexus 请求故障，提升可靠性测试覆盖面。
- **ParentClosePolicy 处理器工作流级测试**（[#11175](https://github.com/temporalio/temporal/pull/11175)）：补充了此前缺失的测试路径，增强代码覆盖率。
- **非空 gRPC 响应断言**（[#11294](https://github.com/temporalio/temporal/pull/11294)）：增加测试时的软断言，防止意外返回 nil 响应。

---

## 7. 用户反馈摘要

当日未发现明显的用户评论或使用场景反馈。Issue #11289 的作者 @tz-torchai 以简要 “Expected Behavior” 描述了问题，但未提供复现细节或使用背景。后续需关注是否会有其他用户补充真实场景影响。

---

## 8. 待处理积压

- 未发现长期未响应的关键 Issue 或 PR。所有 OPEN 的 PR 最近更新时间均在 2026-07-26 或更近，审查和讨论仍在进行中。
- 可关注 ISSUE #11289 的后续进展，若长时间无 Fix，建议核心团队标记为 `bug` 并优先排期。

---

**报告日期**：2026-07-27  
**数据来源**：GitHub Temporal 仓库（过去24小时）  
**生成工具**：AI 智能体分析师

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*