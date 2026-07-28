# OpenClaw 生态日报 2026-07-29

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-28 23:27 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我根据您提供的 OpenClaw 项目 GitHub 数据，为您生成了 2026-07-29 的项目动态日报。

---

## OpenClaw 项目日报 | 2026-07-29

### 今日速览

今日 OpenClaw 项目活跃度极高，24小时内处理了500条 Issue 和 500 条 PR，社区参与度旺盛。新发布的 `v2026.7.2-beta.5` 是一剂“强心针”，深度聚焦于状态安全与数据恢复，标志着项目在核心系统可靠性上迈出了坚实一步。然而，大量与“会话状态”、“崩溃循环”和“消息丢失”相关的高优先级问题仍处于开放状态，显示出项目在应对复杂生产环境时仍面临严峻挑战。总体而言，项目处于快速迭代与核心稳定性攻坚并行的关键阶段。

### 版本发布

- **[v2026.7.2-beta.5](https://github.com/openclaw/openclaw/releases/tag/v2026.7.2-beta.5)**
  - **亮点：**
    - **状态安全与恢复：** 此版本是功能与稳定性的大更新，引入了多重数据保护机制，包括：隔离存储（在数据库损坏时保护持久化数据）、崩溃可恢复的 SQLite 快照、崩溃持久的文件系统发布、拒绝导致数据丢失的模式升级，以及回滚写入者的快照恢复。这显著增强了系统在面对意外崩溃或数据损坏时的韧性。
  - **破坏性变更与迁移建议：** 由于涉及底层状态管理和数据持久化的重构，建议用户在升级后运行 `openclaw doctor --fix` 命令，以确保所有遗留状态和插件索引都能正确迁移到新的安全隔离存储中。请密切关注 Issue [#90213](https://github.com/openclaw/openclaw/issues/90213) 中报告的迁移警告问题，开发者已有相关的修复行为。

### 项目进展

今日项目合并/关闭了大量PR，核心开发团队和社区贡献者协同推进了多项关键修复和性能优化：

- **核心代理与通讯渠道：**
  - **[PR #115434](https://github.com/openclaw/openclaw/pull/115434) (合并):** 修复了 Telegram 私聊回复在网关重启后丢失的问题，直接解决了 Issue [#111519](https://github.com/openclaw/openclaw/issues/111519) 中报告的回归 Bug。
  - **[PR #115426](https://github.com/openclaw/openclaw/pull/115426) (合并):** 修复了插件提供者元数据解析可能导致代理轮次事件循环阻塞的性能问题。
  - **[PR #115349](https://github.com/openclaw/openclaw/pull/115349) (合并):** 为修复特定 Telegram 时序问题提供了精确的测试证明。
  - **[PR #115319](https://github.com/openclaw/openclaw/pull/115319) (开放):** 修复了 `agent exec --json` 命令中，代理执行超时时错误地报告为“异常”而非“超时”的问题。

- **性能与UI优化：**
  - **[PR #115403](https://github.com/openclaw/openclaw/pull/115403) (合并):** 优化了 Codex 应用的性能。通过采用“stale-while-revalidate”策略和跳过热启动客户端解析，显著减少了目录加载的延迟。
  - **[PR #115407](https://github.com/openclaw/openclaw/pull/115407) (合并):** 改进了多代理网关下的 Control UI 交互，将其他代理创建的会话组显示为“空标题”，避免了加载状态的混淆。

- **工具与配置：**
  - **[PR #115246](https://github.com/openclaw/openclaw/pull/115246) (开放):** 为浏览器下载请求增强了策略控制。
  - **[PR #115286](https://github.com/openclaw/openclaw/pull/115286) (开放):** 修复了 `agents.defaults.mediaLocalRoots` 配置项被错误地拒绝的问题。

**总体进展：** 项目在修复回归 Bug（尤其是消息传递可靠性）、提升 UI 交互体验和解决关键性能瓶颈方面取得了显著进展。`v2026.7.2-beta.5` 的发布更是在底层稳定性上进行了重大投入。

### 社区热点

- **[Issue #75](https://github.com/openclaw/openclaw/issues/75)：Linux/Windows 原生应用开发** 以 **115条评论** 和 **80个👍** 高居热点榜首。社区对跨平台原生应用的需求极为强烈，尤其是桌面端用户。该项目已持续活跃超过半年，是社区最期待的功能之一。
- **[Issue #91588](https://github.com/openclaw/openclaw/issues/91588)：关键性网关内存泄漏** 引起了社区的广泛关注。该问题详细描述了网关进程内存（RSS）从启动时的 350MB 在数天内飙升至 15.5GB 并导致系统 OOM 杀手将进程杀死，触发崩溃循环。这是一个严重影响生产环境稳定性的 P0 级别 Bug。
- **[Issue #10659](https://github.com/openclaw/openclaw/issues/10659)：掩码密钥系统** 和 **[Issue #7707](https://github.com/openclaw/openclaw/issues/7707)：内存信任标签** 都反映了社区对**安全性的高度关注**。用户希望引入更细粒度的安全策略，防止代理因提示注入等原因泄露敏感信息（如 API 密钥）或被恶意内容污染记忆。

**诉求分析：** 社区热点清晰地指向三大核心诉求：
1.  **跨平台与原生体验：** 强烈要求提供与 macOS/iOS 同等的原生 Windows/Linux 应用。
2.  **生产级稳定性：** 内存泄漏、消息丢失、崩溃循环等问题是当前用户面临的最主要痛点。
3.  **安全与信任：** 随着代理功能的增强，用户对其访问敏感信息和执行危险操作的安全边界提出了更高要求。

### Bug 与稳定性

今日报告的 Bug 中，稳定性问题依然是主旋律，尤其是“会话状态”和“崩溃循环”相关的问题。

**严重程度排序：**

| 严重等级 | Issue | 摘要 | 是否有修复 PR |
| :--- | :--- | :--- | :--- |
| **P0 (紧急)** | [#91588](https://github.com/openclaw/openclaw/issues/91588) | 关键内存泄漏：RSS从350MB增长至15.5GB，导致OOM崩溃循环 | 否 |
| **P0 (紧急)** | [#114895](https://github.com/openclaw/openclaw/issues/114895) | `edit` 和 `apply_patch` 工具会静默破坏非 UTF-8 文件内容 | 否 (已关闭) |
| **P1 (高)** | [#113434](https://github.com/openclaw/openclaw/issues/113434) | 会话 `reset` 重用失效的 Session ID，导致数组扫描耗尽网关内存并崩溃 | 否 |
| **P1 (高)** | [#115326](https://github.com/openclaw/openclaw/issues/115326) | 崩溃-回路断路器在网关重启后永久抑制 Discord/WhatsApp 频道，且恢复方法失效 | 否 |
| **P1 (高)** | [#108075](https://github.com/openclaw/openclaw/issues/108075) | [回归] `2026.7.1` 版本中，LLM 请求因提供者拒绝可架构或工具载荷而失败 | 否 (已关闭) |
| **P1 (高)** | [#114137](https://github.com/openclaw/openclaw/issues/114137) | [回归] 信号频道间歇性地将最终文本持久化到记录，但从未交付给用户 | 否 |
| **P1 (高)** | [#115001](https://github.com/openclaw/openclaw/issues/115001) | 混合记忆搜索返回虚假的 1.0 相似度评分 | 否 |

**观察：** 许多高优先级 Bug 的根因都指向了 `v2026.7.x` 系列版本引入的新变化。尽管新版本在稳定性方面做了改进（如 beta.5），但新的回归问题依然层出不穷，说明测试覆盖，尤其是集成和压力测试，仍需加强。

### 功能请求与路线图信号

今日的功能请求呈现出对**安全、可观测性和模型管理**的强烈需求：

- **安全增强类：**
  - **[Issue #7707](https://github.com/openclaw/openclaw/issues/7707)**: 内存信任标签，建议为不同来源的记忆内容标注信任级别，防止提示注入攻击。这是下一阶段安全策略的重要方向。
  - **[Issue #10659](https://github.com/openclaw/openclaw/issues/10659)**: 掩码密钥系统，让代理能使用 API 密钥但无法查看或泄露。此功能的实现将对企业级应用至关重要。
  - **[Issue #7722](https://github.com/openclaw/openclaw/issues/7722)**: 文件系统沙箱配置，提供更精细的文件访问控制。
  - **[Issue #39979](https://github.com/openclaw/openclaw/issues/39979)**: 路径作用域的 RWX 权限，取代当前的二进制级别执行白名单。

- **模型与代理管理类：**
  - **[Issue #10687](https://github.com/openclaw/openclaw/issues/10687)**: 完全动态的模型发现，特别是针对 OpenRouter 这种模型目录快速变化的提供商。这与项目支持多模型提供商的愿景一致。
  - **[Issue #9986](https://github.com/openclaw/openclaw/issues/9986)**: 在上下文长度超限时触发模型回退，解决了当前回退逻辑仅针对 API 错误，忽略了上下文溢出的场景。
  - **[Issue #9912](https://github.com/openclaw/openclaw/issues/9912)**: 新增 `maxTurns/maxToolCalls` 配置，用于限制代理的无限迭代，是防止代理失控和消耗费用的关键工具。

- **与已有PR的关联：** 功能请求中体现的“文件访问控制”和“工具权限管理”与当前开放中的 [PR #115277](https://github.com/openclaw/openclaw/pull/115277) 及 [PR #115286](https://github.com/openclaw/openclaw/pull/115286) 方向一致，说明这些功能很可能已经在路线图中。特别是 [PR #115277](https://github.com/openclaw/openclaw/pull/115277) 正在优化 `toolsAllow` 的通配符匹配，这是实现细粒度权限管理的基础。

### 用户反馈摘要

从今日的 Issue 评论和报告中，可以提炼出以下用户痛点：

- **稳定性是最大痛点：** 用户反映“我的网关在运行2-3天后总是会由于OOM被杀死”（#91588），“更新到最新版后，我的Telegram机器人不回消息了”（#115326），这些反馈直指系统在生产环境中的不可靠。
- **迁移过程不顺畅：** 用户报告“升级后遗留状态迁移警告总是出现，即使运行了doctor --fix也没用”（#90213），这表明新版本的平滑过渡体验有待提升。
- **对安全风险的担忧：** 多位用户主动提出“我担心我的API密钥被模型误用或泄露”（#10659），“我想阻止代理访问我的重要系统目录”（#7722），表明用户对代理安全性的信任度还有待加强。
- **对跨平台支持的期待：** Issue #75 中积累了大量评论，用户表达了“我们真的很需要原生的Windows/Linux客户端，而不是用命令行或WebUI凑合”的强烈诉求。

**用户满意点：** 尽管问题很多，但用户仍然积极提交高质量的Issue报告和功能建议，并且如#73537中所述“OpenClaw 已经真正成为我们日常工作的一部分”，这显示了核心用户对项目潜力的认可和依赖。

### 待处理积压

以下是一些长期存在或未获得足够响应的重要问题，提醒维护者关注：

1.  **跨平台开发计划 (P2, 开放超6个月):** **[Issue #75](https://github.com/openclaw/openclaw/issues/75)**。尽管社区呼声极高，但官方尚未给出明确的开发时间线。这是提升项目用户基数的关键窗口。
2.  **文件系统沙箱配置 (P2, 开放近6个月):** **[Issue #7722](https://github.com/openclaw/openclaw/issues/7722)**。该功能请求对于企业级用户和安全敏感用户至关重要，且与当前多个开放PR的改进方向一致，但尚未获得官方维护者的明确回复。
3.  **Exec-Approvals的拒绝列表支持 (P2, 开放近6个月):** **[Issue #6615](https://github.com/openclaw/openclaw/issues/6615)**。这是一个高赞的功能需求，能够提供更灵活的执行策略，但目前没有对应的修复PR或维护者明确表态。
4.  **语音通话管道流式化 (P2, 开放近6个月):** **[Issue #8355](https://github.com/openclaw/openclaw/issues/8355)**。用户希望实现句子级别的流式 TTS 以降低延迟，提升语音通话体验。该需求对产品竞争力有显著提升，但优先级似乎不高。
5.  **代理触发的上下文压缩 (P2, 开放近6个月):** **[Issue #6757](https://github.com/openclaw/openclaw/issues/6757)**。由代理自动提出的功能请求，旨在提供“自压缩”工具以管理长对话上下文。这可以视为对当前`/compact`命令用户路径的优化，值得评估。

---

## 横向生态对比

# 横向对比分析报告：AI 智能体与个人AI助手开源生态（2026-07-29）

## 1. 生态全景

个人 AI 助手与自主智能体开源生态正进入“功能快速膨胀与核心可靠性攻坚并行”的成熟期。六大项目在 24 小时内合计产生超过 650 条 Issue 更新与 876 条 PR 活动，社区参与度极高。虽然各项目在目标用户、技术侧重点上有所分化，但无不将**状态持久化、安全治理、跨平台兼容性与 Provider 生态扩展**作为当前迭代的核心突破口。同时，**内存泄漏、会话丢失、升级迁移缺陷**等稳定性问题仍是最普遍的社区痛点，表明整个生态尚未完全跨越“可用→可靠”的门槛。

## 2. 各项目活跃度对比

| 项目 | 24h Issue 更新 | 24h PR 更新 | 今日发布 | 健康度评估 |
|------|----------------|-------------|----------|------------|
| **OpenClaw** | 500条（新开/活跃） | 500条（新开/待合） | ✅ v2026.7.2-beta.5 | 高活跃，但大量P0/P1 Bug开放，处于“快速迭代+稳定性攻坚”并行期 |
| **Hermes Agent** | 500条 | 500条（合并151） | ❌ 无 | 极高社区参与，合并率30%，维护压力大，多项核心功能缺陷待修 |
| **OpenHands SDK** | 21条（新开14） | 50条（合并3） | ✅ v1.38.0 | 中高活跃，PR合并率仅6%，审核瓶颈明显，安全与MCP方向进展快 |
| **Pi** | 73条（新开18） | 25条（合并18） | ❌ 无 | 高活跃，合并率72%，修复效率高，但Copilot Enterprise等关键Bug积压 |
| **LiteLLM** | 77条（新开61） | 253条（合并57） | ✅ v1.94.0 | 极高活跃，合并率22%，商业化驱动明显，路由与Provider兼容性优先 |
| **Temporal** | 1条（非新开） | 48条（合并17） | ❌ 无 | 中等活跃（工作流引擎属性），PR合并率35%，聚焦复制流隔离与CHASM |

## 3. OpenClaw 在生态中的定位

- **参照级地位**：GitHub 日均 Issue/PR 量居生态之首，社区规模最大，且官方将其作为“核心参照”项目。
- **技术路线差异**：相比 Hermes Agent 和 Pi 偏重“通用 Agent 平台”，OpenClaw 更强调**底层状态安全与数据恢复**（隔离存储、SQLite 崩溃可恢复快照），这是其独特的防御性设计哲学。
- **优势**：状态管理成熟度最高，beta.5 版本引入了多重数据保护机制；社区对“跨平台原生应用”呼声极强（Issue #75 获 115 评论），表明用户基础深厚且期待桌面端体验。
- **弱点**：回归 Bug 频发（Telegram 消息丢失、内存泄漏等），版本升级迁移警告长期得不到解决，影响生产环境信任度。
- **社区规模对比**：OpenClaw 的 Issue 数量（500）远超 OpenHands（21）和 Temporal（1），与 Hermes（500）相当但合并率更高；LiteLLM 虽也有大量 PR，但侧重商用代理网关，与 OpenClaw 面向通用 Agent 的定位不完全重叠。

## 4. 共同关注的技术方向

| 技术主题 | 涉及项目 | 具体诉求 |
|----------|----------|----------|
| **状态/会话持久化与恢复** | OpenClaw（隔离存储）、Hermes（跨会话内存 #8457）、Pi（自动压缩不触发 #6879） | 多轮对话的长期记忆、崩溃后恢复、会话上下文压缩 |
| **安全与权限治理** | OpenClaw（掩码密钥 #10659）、Hermes（多级权限模型 #527）、OpenHands（治理层 #4273）、Pi（文件沙箱 #7722） | 细粒度 RBAC、API Key 保护、提示注入防御、文件访问控制 |
| **跨平台与原生体验** | OpenClaw（Windows/Linux 原生应用 #75）、Pi（WSL 路径错误 #7064）、Hermes（macOS 桌面 SSH 崩溃 #69551） | 桌面原生客户端、WSL/容器环境适配、SSH 远程模式 |
| **Provider/模型兼容性** | LiteLLM（Gemini 缓存 #34872、Vertex AI 500 #34914）、OpenHands（deepseek 缺少参数 #4248）、Pi（Kimi K3 路由 #7230） | 模型回退、Provider 特定参数适配、本地模型（Ollama、llama.cpp）支持 |
| **内存泄漏与稳定性** | OpenClaw（网关内存泄漏 #91588）、Pi（TUI 重渲染 #7194）、LiteLLM（i_dict 并发崩溃 #34471） | OOM 崩溃、goroutine 泄漏、高并发下数据结构竞争 |
| **可观测性与监控** | Temporial（队列积压指标 #11255）、LiteLLM（OTEL 属性类型 #24057）、OpenClaw（性能延迟优化） | Prometheus 指标、OpenTelemetry 集成、延迟/成本追踪 |
| **MCP/工具集成规范** | OpenHands（MCP CRUD 端点 #4294）、LiteLLM（MCP OAuth #34985）、Hermes（技能集 fork #2823） | 原子化操作、OAuth 认证、子代理隔离执行 |

## 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent | OpenHands SDK | Pi | LiteLLM | Temporal |
|------|----------|--------------|---------------|----|---------|----------|
| **功能侧重** | 通用 Agent 框架+状态安全 | 自主智能体+多环境集成 | SDK/工具链+Agent Canvas | 终端个人助手+本地模型优先 | 代理网关+模型路由+成本管理 | 工作流引擎+分布式编排 |
| **目标用户** | 开发者/企业用户（生产级 Agent） | 高级开发者/研究者 | SDK 开发/企业集成 | 个人开发者/CLI 用户 | 平台运维/API 管理者 | 后端工程师/数据管道 |
| **技术架构** | 插件化、隔离存储、SQLite 快照 | 沙箱、技能集、跨平台桥接 | 微服务+ACP 协议 | 终端 TUI+扩展系统+SQLite 搜索 | REST API+路由器+Provider 抽象 | 强一致性复制+CHASM |
| **部署形态** | 自托管/桌面端待开发 | 自托管（Python 3.14 兼容） | Docker/K8s + SDK | CLI/TUI + tmux/SSH | Docker/Helm/Cloud | 分布式集群 |
| **社区成熟度** | 高活跃，但稳定性不够 | 高活跃，合并率低 | 中活跃，审核瓶颈 | 中高活跃，修复效率高 | 极高活跃，商业化驱动 | 中等活跃，工程严谨 |

## 6. 社区热度与成熟度分层

### 第一梯队：极速迭代期（Issue/PR 日产出 >200）
- **OpenClaw、Hermes、LiteLLM**：社区参与量巨大，新功能与 Bug 报告同步激增。特点是高产但“快而不稳”，回归 Bug 频发，大量 PR 积压（LiteLLM 196 待合、Hermes 349 待合）。适合愿意尝鲜的开发者，但生产环境需谨慎。

### 第二梯队：稳步推进期（日产出 20-100）
- **Pi、OpenHands**：活跃度适中，合并率较高（Pi 72%），修复效率好。社区反馈集中在核心功能缺陷（如 Pi 的 Copilot 压缩、OpenHands 的 MCP 治理）。适合中小团队或个人使用。

### 第三梯队：成熟巩固期（日产出 <20）
- **Temporal**：作为工作流引擎，其社区节奏较慢，但代码质量高、测试覆盖广。PR 集中在复制流隔离、CHASM 等长期架构改进，不追求功能堆叠，工程稳健性第一。适合对可靠性和一致性要求极高的用户。

## 7. 值得关注的趋势信号

1. **企业级治理需求爆发**：Hermes（多级权限）、OpenHands（治理层）、OpenClaw（掩码密钥）同时出现，表明用户正推动 Agent 从“个人玩具”走向“企业级协同工具”，要求 RBAC、审计、成本预算等能力。**建议开发者优先实现细粒度权限模型与安全沙箱**。

2. **本地模型生态成熟加速**：Pi 的 `llama.cpp` 默认模型问题、LiteLLM 的 Ollama/Vertex 集成、OpenHands 的超时不可配置，共同指向用户对**自托管/边缘部署**的强烈偏好，同时暴露了主流框架对本地 Provider 支持的不完善。这是早期差异化机会。

3. **MCP 协议成为事实标准**：OpenHands 和 LiteLLM 均围绕 MCP 进行 CRUD 端点、OAuth 集成、原子化操作设计，MCP 正从“新兴协议”演变为 Agent 工具调用的基础构件。**所有 Agent 框架应尽快对齐 MCP 规范**。

4. **可观测性成为稳定性基石**：LiteLLM 的 OTEL 类型错误、Temporal 的队列积压指标、OpenClaw 的性能优化 PR，反映社区不再满足于“能运行”，而是要求“能监控、能诊断”。**建议将 Prometheus/OpenTelemetry 集成纳入每个项目的 MVP**。

5. **会话记忆从缓存走向永久存储**：Hermes（跨会话持久化内存）、OpenClaw（崩溃可恢复快照）、Pi（SQLite 全文搜索索引）不再将记忆视为临时上下文，而是持久化知识库。**设计 Agent 时需考虑向量索引、增量压缩与长期回滚能力**。

6. **供应链安全受关注**：LiteLLM v1.94.0 引入 cosign 镜像签名、OpenHands CI 修复目录泄露（#4208），安全左移趋势明显。**所有提供 Docker 镜像的项目应尽快引入签名验证机制**。

7. **WSL/跨平台兼容性成隐形门槛**：Pi 的 WSL 路径错误获 10 条评论、Hermes 的 macOS SSH 崩溃、OpenClaw 的 Windows 原生应用等待已久——Windows 用户是巨大的被忽视群体。**支持 WSL 2 路径映射与原生 Windows 可执行文件可快速拉新用户**。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，以下是根据您提供的 Hermes Agent 项目数据生成的 2026-07-29 项目动态日报。

---

# Hermes Agent 项目动态日报 (2026-07-29)

**分析师:** AI 智能体与个人 AI 助手领域开源项目分析师
**数据源:** GitHub (github.com/NousResearch/hermes-agent)
**报告周期:** 2026-07-28 至 2026-07-29

### 1. 今日速览

今日项目社区活跃度极高，24小时内产生了大量提交和讨论。**关键数据**：Issues 更新达500条，PR 更新同样为500条，但无新版本发布。这反映出项目正处于一个**密集的社区反馈与协作开发期**，Bug 修复与功能提案的讨论并行，开发者响应积极，但大量 PR 尚未合并（349/500），也提示项目维护进度面临一定压力。

### 2. 版本发布

**无新版本发布。** 今日无正式发布。项目当前开发状态处于多个大型修复和功能 PR 等待审核或合并的阶段，距离下一个稳定版本可能还需一段时间。

### 3. 项目进展

今日虽然没有新版本发布，但合并/关闭了151个 PR，有力地推动了项目进程。其中重要的进展包括：

- **桌面应用稳定性提升**:
    - [#73688 **CLOSED**](https://github.com/NousResearch/hermes-agent/pull/73688): 修复了 Discord 语音通道首次加入时产生 STT 幻觉的问题，通过 PCM 活动门控过滤静音/舒适噪音数据。
    - [#58641 **CLOSED**](https://github.com/NousResearch/hermes-agent/pull/58641): 实现了 CloakBrowser 的原生后端集成，增强浏览器工具的私有页面保护。
    - [#52188 **CLOSED**](https://github.com/NousResearch/hermes-agent/pull/52188) 和 [#48884 **CLOSED**](https://github.com/NousResearch/hermes-agent/pull/48884): 修复了 LM Studio 集成时的上下文窗口处理问题，确保 Agent 能正确识别和利用本地模型的上下文能力。

- **跨平台与兼容性修复**:
    - [#58596](https://github.com/NousResearch/hermes-agent/issues/58596) 的讨论和 [#68992](https://github.com/NousResearch/hermes-agent/pull/68992) 的提交，标志着项目方开始主动解决对 **Python 3.14 的兼容性问题**。`DaemonThreadPoolExecutor` 的修复对于所有使用多线程协作 (如 `delegate_task`, 技能集) 的功能至关重要。

项目整体在**解决桌面端体验、修复特定 Provider 集成错误以及预研新平台兼容性**方面取得了明显进展。

### 4. 社区热点

今日讨论最热烈的议题集中在**权限控制、Agent 核心能力和平台集成**三大方向：

1.  **多级权限模型 (Gateway Permission Tiers)** [#527](https://github.com/NousResearch/hermes-agent/issues/527)
    - **讨论热度**: 16条评论，持续活跃中 (创建于3月)。
    - **诉求分析**: 用户 `@teknium1` 提出的这一功能需求反映了**企业级和个人高级用户的强烈治理需求**。目前的“全有或全无”授权模型对于多用户环境（如企业团队使用 Discord/Telegram 机器人）极不友好，社区呼吁实现精细化的 RBAC 控制。

2.  **跨会话持久化内存 (Persistent Session Memory)** [#8457](https://github.com/NousResearch/hermes-agent/issues/8457)
    - **讨论热度**: 15条评论。
    - **诉求分析**: 这是社区对 Agent 智能体长期记忆能力最核心的诉求之一。用户 `@sephmartin` 提出了一个非常完整的方案，涵盖了会话搜索、自动压缩等关键点。这表**用户已经不满足于单次对话的上下文，而是期望 Agent 能成为真正的“长期伙伴”**。

3.  **全新平台集成 (Buzz & Claude订阅)**
    - **Buzz 集成** [#68871](https://github.com/NousResearch/hermes-agent/issues/68871): 17条评论，反响热烈。用户正在积极探索将 Agent 接入新兴的“AI 原生协作空间”（如 Block 开源的 Buzz），**显示出 Agent 从“聊天机器人”向“工作区成员”演进的趋势**。
    - **Claude 订阅模式** [#25267](https://github.com/NousResearch/hermes-agent/issues/25267): 13条评论，获得44个👍，是今日获赞最高的议题。这反映了**用户对使用成本的高度敏感**。许多 Claude 订阅用户希望无缝地在 Hermes Agent 中使用现有订阅，避免双重付费。这是一个重要的用户留存障碍。

### 5. Bug 与稳定性

今日报告的 Bug 数量较多 (408个活跃/新开)，涉及范围广泛，以下是按严重程度排列的关键问题：

- **严重**:
    - **Desktop SSH 远程模式因 Profile 路径解析错误而崩溃** [#69551](https://github.com/NousResearch/hermes-agent/issues/69551): **P2级别**。当使用非默认 Profile 时，Token 路径验证逻辑错误，导致远程桌面连接完全不可用。这是一个严重的回归问题，对使用多 Profile 的用户影响巨大。
    - **Session 重置导致上下文丢失 (Auto-reset discards context)** [#12857](https://github.com/NousResearch/hermes-agent/issues/12857): **P2级别**。这直接破坏了 Agent 的长期对话能力，是核心功能缺陷，虽有7条评论但尚未被关闭。

- **中高**:
    - **Qwen 模型思维链上下文丢失 (prior-turn reasoning stripped)** [#56004](https://github.com/NousResearch/hermes-agent/issues/56004): **P2级别，5个👍**。对于使用 Qwen 系列模型的用户，这是破坏性体验，多轮对话中模型“思考过程”的缺失会影响回答的连贯性和质量。
    - **Gemini 503 错误无 Provider 回退** [#25822](https://github.com/NousResearch/hermes-agent/issues/25822): **P2级别**。依赖云服务的 Agent 必须要有稳定的容错机制。此 Bug 会导致 Agent 在 Gemini 服务不稳定时完全失效。
    - **`hermes update` 操作导致浏览器依赖丢失** [#43564](https://github.com/NousResearch/hermes-agent/issues/43564): **P2级别**。安装/更新流程中的 Bug 会直接破坏核心功能（浏览器工具），用户满意度会因此下降。

- **已有修复 PR**:
    - **Python 3.14 兼容性问题** [#58596](https://github.com/NousResearch/hermes-agent/issues/58596): 没有直接对应的 PR 修复，但 [PR #68992](https://github.com/NousResearch/hermes-agent/pull/68992) 在修复类似的内存问题，表明开发者正在处理此方向的问题。
    - **桌面端连续语音收听中断** [#73690](https://github.com/NousResearch/hermes-agent/pull/73690): 相关 PR 已被提交，旨在恢复播放后的麦克风状态。

### 6. 功能请求与路线图信号

今日的功能请求为项目未来的演进方向提供了明确信号：

1.  **迈向通用 Agent 平台**:
    - **Buzz 集成 (Issue #68871)** 和 **Claude 订阅模式 (Issue #25267)** 都表明用户希望 Hermes Agent 成为一个“通用接入层”，连接到各种主流或新兴平台，而不是局限在某个特定生态中。
    - **Kanban 看板集成桌面端 (Issue #41222)**: 15个👍。用户希望将强大的工作流功能和桌面聊天界面深度融合，提升日常使用的便捷性。

2.  **强化核心记忆与工作流能力**:
    - **跨会话记忆 (Issue #8457)** 和 **Topic-Aware 压缩 (Issue #62595)**: 这表明社区对 Agent 自主管理记忆的智能化程度有更高要求，不仅需要记住，还要能高效组织和检索。
    - **文件传输 (send_file tool) (Issue #466)**: 这是一个基础但关键的功能补全。Sandbox 环境与用户的文件交互是实现真正“有用”的 Agent 的必备能力。

3.  **潜在的下一版本特性**:
    - 结合已有 PR，**角色基础访问控制 (RBAC, Issue #527)** 和 **持久化会话内存 (Issue #8457)** 可能是社区呼声最高、基础架构影响最大的功能，有较大概率被纳入下一版本计划。`@ValentinSergief` 提交的多个关于修复 Session 和 Cron 的 PR (如 #48525, #43233) 也在为更强和更稳定的会话能力打下基础。

### 7. 用户反馈摘要

从今日的 Issue 评论中提炼出如下用户体验：

- **痛点集中**:
    - **配置复杂性**: 多个用户抱怨存在“两个独立的超时配置键” (Issue #25859)，导致难以排查 CLI 无故自动决策的问题。
    - **权限与安全**: 用户对 Agent 自动修改 Skill 文件感到不安 (Issue #64926)，期望通过配置使其只读。同时，对 Sandbox 内外文件传输的不便表示困扰 (Issue #466)。
    - **平台兼容性**: macOS 用户的桌面端 SSH 远程模式崩溃 (Issue #69551) 以及权限被重置 (Issue #49110) 是明确的痛点。Windows 用户则面临更新时 Node 依赖丢失的问题 (Issue #43564)。

- **使用场景**:
    - **高级用户**正在尝试将 Hermes Agent 集成到更复杂的工作流中，如使用 Cron 进行定时任务，并期待内存和看板功能能深度融合 (Issue #41222, #45769)。
    - **企业用户**开始关注治理问题，如多用户权限控制 (Issue #527)。
    - **研究者/开发者**在使用最新模型 (如 Qwen3.6) 时遇到了特定 Provider 的兼容性问题 (Issue #56004)。

- **满意之处**:
    - 社区对开发者响应问题的积极性表示认可，例如 [PR #45769](https://github.com/NousResearch/hermes-agent/pull/45769) 对应 Issue #45768 的高效修复。
    - 对于 Buzz 集成这类前瞻性功能提议，社区投票和评论非常活跃，显示了用户对项目创新方向的期待和兴趣。

### 8. 待处理积压

以下是一些长期未解决但对项目健康度或用户体验影响较大的 Issue/PR，建议维护团队关注：

- **长期未解决的核心功能缺陷**:
    - **WhatsApp 桥接在 macOS 上不可用** (Issue [#2975](https://github.com/NousResearch/hermes-agent/issues/2975)): 创建于2026年3月25日，至今已4个月，仅检查 PATH 的方式限制了 macOS 用户的使用。建议引入更通用的 Node.js 查找逻辑。
    - **OpenRouter 模型响应极慢 (2分钟)** (Issue [#4291](https://github.com/NousResearch/hermes-agent/issues/4291)): 创建于2026年3月31日，严重影响了依赖此服务用户的体验。尽管可能需要 OpenRouter 端配合，但作为集成方，增加诊断信息或添加超时/重试机制可能是有益的第一步。

- **需要决策的重要 PR**:
    - **多项由 @ValentinSergief 提交的包含 `needs-decision` 标签的修复 PR**，例如关于Cron session 渲染 (PR #43233)、session 压缩行删除 (PR #48525) 等。这些 PR 影响面较广 (blast-moderate)，需要核心维护者决策并合并，以解决多个已报告的痛点。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目日报 — 2026-07-29

数据区间：2026-07-28 00:00 UTC – 2026-07-29 00:00 UTC  
数据来源：[OpenHands/software-agent-sdk](https://github.com/OpenHands/software-agent-sdk)

---

## 1. 今日速览

过去 24 小时项目保持**高活跃度**：共处理 21 条 Issue（新开/活跃 14 条，关闭 7 条）、50 条 PR（待合并 47 条，合并/关闭 3 条），并发布了 v1.38.0 版本。PR 提交量较大，但合并率偏低（仅 6%），反映出社区贡献积极但审核流程可能成为瓶颈。Issue 关闭数量正常，其中包含多个自动化追踪器和测试性 Issue。安全、MCP 治理和模型路由是今日社区讨论的焦点。

---

## 2. 版本发布

### [v1.38.0](https://github.com/OpenHands/software-agent-sdk/releases/tag/v1.38.0)

**变更内容：**
- `docs(examples)` 在确认预览中展示 LLM action 摘要（PR [#4218](https://github.com/OpenHands/software-agent-sdk/pull/4218)）
- `feat` 在 agent-settings schema 中暴露 `agent_context.load_memory`（PR [#4205](https://github.com/OpenHands/software-agent-sdk/pull/4205)）

**破坏性变更：** 无  
**迁移注意事项：** 无特殊需要，建议关注 `load_memory` 字段的新增用途。

---

## 3. 项目进展

### 已合并/关闭的重要 PR（共 3 条）

由于数据仅展示评论数最多的 20 条 PR，今日合并的 3 条 PR 未在列表中详细列出。但从 Issue 关闭情况可推断，以下工作已取得进展：

- **多个自动化追踪器关闭**：`#2078`（Daily Integration Runs）和 `#3950`（Daily Examples Run Results）按计划关闭，表明 CI/CD 运行稳定。
- **测试性 Issue 关闭**：`#4286`（测试 bug）和 `#4285`（自动化验证 bug）被关闭，说明维护团队正在清理非阻塞问题。
- **功能关闭**：`#2494`（多 marketplace 注册支持）已关闭，该功能可能在更早的版本中已落地。

### 项目整体推进

- **MCP 相关功能加速**：PR [#4294](https://github.com/OpenHands/software-agent-sdk/pull/4294) 新增 MCP 设置 CRUD 端点，配套 Issue [#4293](https://github.com/OpenHands/software-agent-sdk/issues/4293) 开始设计原子化操作，这是 Agent Canvas 重构的重要一步。
- **安全加固**：PR [#4282](https://github.com/OpenHands/software-agent-sdk/pull/4282) 修复了 VSCode URL 端点未校验 workspace 目录的安全问题（中等严重性），已提交待合并。
- **性能与稳定性**：PR [#3997](https://github.com/OpenHands/software-agent-sdk/pull/3997) 增加了可配置的 `content_response_policy`，解决 LLM 无工具调用时的响应问题；PR [#3698](https://github.com/OpenHands/software-agent-sdk/pull/3698) 持久化子 agent 任务索引，支持跨进程恢复。

---

## 4. 社区热点

### 讨论最活跃的 Issue

| Issue | 标题 | 评论数 | 标签 | 链接 |
|-------|------|--------|------|------|
| #2078 | [Tracker] Daily Integration Runs | 152 | closed | [查看](https://github.com/OpenHands/software-agent-sdk/issues/2078) |
| #4248 | [Bug] Missing required parameters for function 'execute_bash': {'security_risk'} | 10 | bug, needs-triage | [查看](https://github.com/OpenHands/software-agent-sdk/issues/4248) |
| #4273 | [Feature] Governance layer for agent actions | 8 | enhancement, needs-triage | [查看](https://github.com/OpenHands/software-agent-sdk/issues/4273) |

**分析：**

- **#4248** 是今日被讨论最多的实际 bug。用户使用 `deepseek-reasoner` 模型时，`execute_bash` 函数缺少 `security_risk` 参数，导致调用失败。该问题暴露了模型适配中的参数兼容性问题，社区对此高度关注。
- **#4273** 提出的“治理层”概念（文件访问控制、命令白名单、成本预算、审计证据）获得了较多讨论，反映了企业级用户对安全管控的强烈需求。该功能若实现，将显著提升 OpenHands 在合规场景的可用性。

### 值得关注的 PR

PR [#3953](https://github.com/OpenHands/software-agent-sdk/pull/3953)（修复 subscription validator 组合）虽未标注评论数，但从描述看是关键的序列化修复；PR [#2823](https://github.com/OpenHands/software-agent-sdk/pull/2823)（添加 `context=fork` 实现子 agent 隔离执行）已暂停 3 个月，仍被社区持续更新，说明是热门需求。

---

## 5. Bug 与稳定性

按严重程度排列（优先级从高到低）：

### 高优先级

- **#4208** [priority:high] — `check-pr-artifacts` 工作流因 `.pr/` 目录泄露到 main 分支，且在 fork PR 上因 403 硬失败。  
  当前状态：**无关联 fix PR**，已有 1 个 👍。  
  链接：[#4208](https://github.com/OpenHands/software-agent-sdk/issues/4208)

- **#4255** — 使用 Ollama 时任务超过 300 秒自动被 kill，UI 和 `settings.json` 无法修改超时。  
  当前状态：**开放中，无 fix PR**。5 条评论。  
  链接：[#4255](https://github.com/OpenHands/software-agent-sdk/issues/4255)

- **#4256** — agent-server Docker 镜像中 browser-use 启动 Chromium 未带 `--no-sandbox`，导致 `BrowserLaunchEvent` 超时和“Root CDP client not initialized”。  
  当前状态：**开放中，无 fix PR**。4 条评论。  
  链接：[#4256](https://github.com/OpenHands/software-agent-sdk/issues/4256)

### 中优先级

- **#4285** [priority:medium] — SDK session 重试在首次网络错误后停止，用户需手动重启。  
  当前状态：**已关闭**（自动化验证 Issue，实际修复可能在其他 PR 中）。  
  链接：[#4285](https://github.com/OpenHands/software-agent-sdk/issues/4285)

- **#4248** — `execute_bash` 缺少 `security_risk` 参数（如上文）。  
  当前状态：**开放中，needs-triage**。10 条评论。  
  链接：[#4248](https://github.com/OpenHands/software-agent-sdk/issues/4248)

### 低优先级

- **#4286** [priority:low] — 测试 bug（已关闭）。  
- **#3753** (Stale) — iframe 吸附导致 DOM 提取失败。  
- **#3759** (Stale) — `is_git_url()` 不支持 `ssh://` 协议。  
- **#4253** — OpenHands 内置浏览器损坏，无法测试 Web 应用。

**总结：** 今日无严重影响生产的崩溃性 bug，但超时未修、Docker 启动失败、CI 硬失败等问题持续存在，建议优先处理 #4208 和 #4256。

---

## 6. 功能请求与路线图信号

### 可能纳入下一版本的功能

- **MCP 原子化 CRUD 操作** — Issue [#4293](https://github.com/OpenHands/software-agent-sdk/issues/4293) 与 PR [#4294](https://github.com/OpenHands/software-agent-sdk/pull/4294) 已对齐，旨在避免客户端手动构造 `PATCH /api/settings` payload。设计已完成，预计很快合并。
- **缓存 TTL 可达 1 小时** — Issue [#4292](https://github.com/OpenHands/software-agent-sdk/issues/4292) 指出 `_apply_prompt_caching` 只能设置 5 分钟 TTL，用户希望扩展至 1 小时以提升性能。虽无直接 PR，但属于低风险优化。
- **治理层** — Issue [#4273](https://github.com/OpenHands/software-agent-sdk/issues/4273) 得到 8 条评论，是企业部署的核心诉求。目前无关联 PR，但架构设计文档 [#4288](https://github.com/OpenHands/software-agent-sdk/issues/4288) 已发布，预计进入设计阶段。

### 长期路线图信号

- **ACP 协议清理** — Issue [#3771](https://github.com/OpenHands/software-agent-sdk/issues/3771) 计划废弃 `session/new` 的 `_meta` 模型选择路径，统一使用 `set_session_model`；Issue [#3772](https://github.com/OpenHands/software-agent-sdk/issues/3772) 要求升级 provider CLI（Claude 0.30→0.46 等）。这两项均对模型兼容性有影响。
- **技能系统增强** — Issue [#2053](https://github.com/OpenHands/software-agent-sdk/issues/2053)（Skills Epic）仍在推动子 agent 执行、模型路由等能力，但标记为 Stale，进度可能放缓。

---

## 7. 用户反馈摘要

从 Issue 评论中提炼的真实痛点和使用场景：

| 用户痛点 | 涉及 Issue | 评论摘录 / 描述 |
|---------|------------|----------------|
| Ollama 超时不可配置 | [#4255](https://github.com/OpenHands/software-agent-sdk/issues/4255) | “Changing the timeout in the UI or in the `settings.json` file does not actually apply.” |
| 缺少 `security_risk` 参数导致 deepseek 模型不可用 | [#4248](https://github.com/OpenHands/software-agent-sdk/issues/4248) | `Missing required parameters for function 'execute_bash': {'security_risk'}` |
| 浏览器功能严重损坏 | [#4253](https://github.com/OpenHands/software-agent-sdk/issues/4253) | “WebApp Development requires you to check out the real behaviour of your apps in browser. Currently OpenHands WebUI's built-in browser tab is very flaky and broken.” |
| iframe 导致 DOM 完全失效 | [#3753](https://github.com/OpenHands/software-agent-sdk/issues/3753) | “Since virtually every real page has such iframes, this matches the 'fails on every real page' pattern.” |
| SSH URL 协议不被识别 | [#3759](https://github.com/OpenHands/software-agent-sdk/issues/3759) | `ssh://` URL 在 `parse_extension_source` 中解析失败，错误信息误导。 |

**满意之处：** 未发现正面反馈，但 Issue 数量相对于 PR 数量（21:50）说明社区积极贡献，整体满意度可能较高。

---

## 8. 待处理积压

以下 Issue 或 PR 长期未更新或未响应，建议维护者关注：

### 长期未响应的 Issues（标记为 Stale）

| Issue | 标题 | 创建时间 | 最后更新 | 链接 |
|-------|------|----------|----------|------|
| #2053 | [Epic] Skills: Execution isolation, model routing & enhanced capabilities | 2026-02-13 | 2026-07-28（仍活跃） | [查看](https://github.com/OpenHands/software-agent-sdk/issues/2053) |
| #3753 | [Bug] browser-use iframe 导致 DOM 提取失败 | 2026-06-16 | 2026-07-28 | [查看](https://github.com/OpenHands/software-agent-sdk/issues/3753) |
| #3759 | [Bug] is_git_url() 不支持 ssh:// | 2026-06-16 | 2026-07-28 | [查看](https://github.com/OpenHands/software-agent-sdk/issues/3759) |
| #3771 | ACP: deprecate session/new `_meta` path | 2026-06-17 | 2026-07-28 | [查看](https://github.com/OpenHands/software-agent-sdk/issues/3771) |
| #3772 | ACP: bump provider CLIs | 2026-06-17 | 2026-07-28 | [查看](https://github.com/OpenHands/software-agent-sdk/issues/3772) |

### 长期未合并的 PR（创建超过 2 个月）

| PR | 标题 | 创建时间 | 最后更新 | 链接 |
|----|------|----------|----------|------|
| #2823 | feat(skills): add context=fork for isolated subagent execution | 2026-04-14 | 2026-07-28 | [查看](https://github.com/OpenHands/software-agent-sdk/pull/2823) |
| #2848 | refactor: Centralize MCP utils in `openhands.sdk.mcp` | 2026-04-16 | 2026-07-28 | [查看](https://github.com/OpenHands/software-agent-sdk/pull/2848) |
| #3029 | feat(sdk): introduce SnapshotReplayAgent for deterministic conversation | 2026-05-01 | 2026-07-28 | [查看](https://github.com/OpenHands/software-agent-sdk/pull/3029) |
| #3262 | perf(hooks): persistent hook runner | 2026-05-14 | 2026-07-28

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

## Pi 项目动态日报 — 2026-07-29

---

### 1. 今日速览

过去 24 小时项目保持高活跃度：共处理 73 条 Issue（其中新开或活跃 18 条，关闭 55 条），处理 25 个 PR（其中已合并或关闭 18 个，待合并 7 个）。社区关注点集中于**Copilot Enterprise 压缩失败**、**WSL 路径处理错误**、**自动压缩不触发**等核心稳定性问题，同时有多项功能改进 PR 被合并（如 Undici 升级、Kimi K3 路由、Apiário 提供商等）。项目整体处于快速迭代与问题修复并行阶段，无新版本发布。

---

### 3. 项目进展

**今日合并/关闭的重要 PR**（按功能领域分类）：

| 领域 | PR | 简述 | 状态 |
|------|----|------|------|
| 网络与代理 | [#7225](https://github.com/earendil-works/pi/pull/7225) `fix: update undici from 8.5.0 to 8.8.0` | 修复 HTTP_PROXY 被忽略的问题，解决 #7049 | 已合并 |
| 新提供商 | [#7240](https://github.com/earendil-works/pi/pull/7240) `feat(ai): add Apiário as built-in provider` | 新增巴西开发者聚合 API Apiário 提供商 | 已合并 |
| 模型支持 | [#7230](https://github.com/earendil-works/pi/pull/7230) `fix(ai): route Fireworks Kimi K3 through openai-completions` | 为 Fireworks 上的 Kimi K3 添加特殊路由，关闭 #7199 | 已合并 |
| 提供商修复 | [#7174](https://github.com/earendil-works/pi/pull/7174) `fix(ai): send max_tokens for Z.AI providers` | 修复 Z.AI 忽略 `max_completion_tokens` 的问题，改用 `max_tokens` | 已合并 |
| 扩展与资源 | [#7218](https://github.com/earendil-works/pi/pull/7218) `fix(coding-agent): preserve resource metadata after extension resource reloads` | 修复扩展资源重载后元数据丢失，关闭 #6968 | 已合并 |
| 安装清理 | [#7210](https://github.com/earendil-works/pi/pull/7210) `fix(coding-agent): clean up failed git installs` | 失败安装后清理残留文件，关闭 #7189 | 已合并 |
| 模型选择器 | [#7211](https://github.com/earendil-works/pi/pull/7211) `fix(coding-agent): reset model selector selection to top row when filtering` | 修复 `/model` 过滤时高亮不移动的问题 | 已合并 |
| 扩展事件 | [#7214](https://github.com/earendil-works/pi/pull/7214) `fix: rpc bash no longer bypass user_bash` | 修复 RPC 模式下 `bash` 绕过 `user_bash` 扩展事件，关闭 #7063 | 已合并 |
| 构建修复 | [#7206](https://github.com/earendil-works/pi/pull/7206) `fix(coding-agent): build-check-test` | 修复 `npm run check` 因提交 `04b1525` 被破坏的问题 | 已合并 |

此外，多个 **open** 的 PR 正在推进重要功能：

- [#7245](https://github.com/earendil-works/pi/pull/7245) `feat(tui): inline images under tmux via sixel`：在 tmux 内支持 Sixel 内联图像。
- [#7231](https://github.com/earendil-works/pi/pull/7231) `Markdown api`：为扩展提供 Markdown 渲染 API（关闭 #6747）。
- [#5262](https://github.com/earendil-works/pi/pull/5262) `feat(ai): add Anthropic Vertex provider`：新增 Google Cloud Vertex AI 上的 Anthropic Claude 提供商。
- [#7243](https://github.com/earendil-works/pi/pull/7243) `fix(ai): update TypeBox nullable array validation`：升级 TypeBox 到 1.3.7，修复 nullable 数组的 JSON Schema 验证。
- [#7216](https://github.com/earendil-works/pi/pull/7216) `fix: formatting of delta content blocks`：修复 `openai-completions` 流式响应中数组内容被序列化为 `[object Object]` 的 bug（部分修复 #7062）。
- [#7221](https://github.com/earendil-works/pi/pull/7221) `fix(coding-agent): stop loading AGENTS.md twice in nested git worktrees`：避免嵌套 git worktree 中重复加载上下文文件。
- [#7163](https://github.com/earendil-works/pi/pull/7163) `feat: search index sqlite`：为 SQLite session 仓库添加全文搜索索引。

**项目整体向前迈进**：在网络代理兼容性、新提供商支持、多个稳定性修复上均有产出，同时扩展系统（Markdown API）和 TUI 增强（tmux Sixel、搜索索引）正在开发中。

---

### 4. 社区热点

**讨论最活跃的 Issues**（评论数 ≥5）：

1. **[#6768](https://github.com/earendil-works/pi/issues/6768) [OPEN] Compaction using Copilot Enterprise not possible**  
   - 评论 16，👍 13。用户报告使用 Copilot Enterprise 许可证进行上下文压缩时，OpenAI 端点返回 421 错误，Anthropic 模型也失败。该问题持续 12 天，尚未有公开修复 PR，社区呼声很高。

2. **[#6747](https://github.com/earendil-works/pi/issues/6747) [OPEN] An API for enhancing agent message markdown**  
   - 评论 11，👍 2。用户希望允许扩展在不修改 LLM 原始内容的情况下改变 agent 消息的 Markdown 展示，当前已有对应 PR [#7231](https://github.com/earendil-works/pi/pull/7231) 处于开放状态，社区关注度高。

3. **[#7064](https://github.com/earendil-works/pi/issues/7064) [OPEN] WSL absolute windows paths are mishandled**  
   - 评论 10，👍 1。WSL2 用户报告路径处理错误导致 `read`/`write`/`edit` 工具失败。属于 Windows+WSL 环境的核心 Bug，影响面广。

4. **[#6922](https://github.com/earendil-works/pi/issues/6922) [CLOSED] Default model cannot be a llama.cpp model**  
   - 评论 7，👍 13。当默认提供商为 `llama.cpp` 时，启动显示 "No models available"。该问题已被关闭（可能是通过 PR 修复或标记为设计限制），但点赞众多，说明本地模型支持需求强烈。

**分析**：社区当前最关心的两大方向是 **Copilot Enterprise 兼容性** 和 **本地模型（llama.cpp）** 的默认配置问题。WSL 路径处理也是高频痛点，尤其是使用 Pi 作为远程开发工具的用户。

---

### 5. Bug 与稳定性

**按严重程度排列：**

| 严重程度 | Issue | 简述 | 是否有 Fix PR |
|----------|-------|------|--------------|
| **Critical** | [#6768](https://github.com/earendil-works/pi/issues/6768) | Copilot Enterprise 压缩完全不可用，导致功能阻塞 | 无 |
| **High** | [#7064](https://github.com/earendil-works/pi/issues/7064) | WSL 下绝对 Windows 路径处理错误，工具调用频繁失败 | 无 |
| **High** | [#6879](https://github.com/earendil-works/pi/issues/6879) | 自动压缩在上下文超过 100% 后不触发，直到 API 拒绝请求 | 无 |
| **High** | [#7020](https://github.com/earendil-works/pi/issues/7020) | 压缩后 agent 有时没有继续执行 | 无 |
| **High** | [#7194](https://github.com/earendil-works/pi/issues/7194) | TUI 每 1 秒全量重渲染，当活动工具卡片移出视口时 | 无 |
| **Medium** | [#7049](https://github.com/earendil-works/pi/issues/7049) | HTTP_PROXY 代理未正确转发（已修复，PR #7225 合并） | ✅ [#7225](https://github.com/earendil-works/pi/pull/7225) |
| **Medium** | [#7161](https://github.com/earendil-works/pi/issues/7161) | Anthropic 路径不发送 `x-client-request-id`，导致代理无法分组会话 | 无 |
| **Medium** | [#7133](https://github.com/earendil-works/pi/issues/7113) | `/login` 输入 API Key 后 TUI 死锁（模型目录不可达） | 无 |
| **Low** | [#7126](https://github.com/earendil-works/pi/issues/7126) | Ctrl+R 重命名会话需按两次 Enter | 无 |
| **Low** | [#7195](https://github.com/earendil-works/pi/issues/7195) | 扩展目录为符号链接时不加载（已关闭） | 无 |

**新出现的 Bug 信号**：今日新增 [#7187](https://github.com/earendil-works/pi/issues/7187)（第三方包清单 typo 导致核心包解析静默崩溃，影响所有用户的聊天和定时任务）、[#7161](https://github.com/earendil-works/pi/issues/7161)（缺少请求 ID 导致代理路由异常）。多个压缩相关的问题（#6879、#7020）表明当前压缩系统在长时间会话中仍需完善。

---

### 6. 功能请求与路线图信号

| 需求 | Issue/PR | 简述 | 可能被纳入下一版本 |
|------|----------|------|-------------------|
| Markdown 渲染 API | [#6747](https://github.com/earendil-works/pi/issues/6747) + [#7231](https://github.com/earendil-works/pi/pull/7231) | 允许扩展重写 agent 消息的 Markdown 展示，不影响发送给 LLM 的内容 | ✅ 已有 PR，高可能性 |
| tmux Sixel 内联图像 | [#7245](https://github.com/earendil-works/pi/pull/7245) | 在 tmux 会话中支持 Sixel 图像显示 | ✅ PR 开放中 |
| Anthropic Vertex AI 提供商 | [#5262](https://github.com/earendil-works/pi/pull/5262) | 增加 Google Cloud Vertex AI 上的 Claude 支持 | 待合并（已有 2 个月） |
| 搜索索引（SQLite FTS5） | [#7163](https://github.com/earendil-works/pi/pull/7163) | 为 SQLite 会话添加全文搜索能力 | ✅ PR 开放中 |
| 改进本地模型连接体验 | [#6305](https://github.com/earendil-works/pi/issues/6305)（已关闭） | 新手友好方式连接本地模型服务器（自动发现或手动输入 URL） | 可能被重新讨论 |
| 上下文文件重复去重 | [#7171](https://github.com/earendil-works/pi/issues/7171)（已关闭） | 去重 cwd→root 遍历中字节相同的 AGENTS.md/CLAUDE.md | 设计信号，已有 PR #7221 部分解决 |

**路线图信号**：项目正在逐步扩展提供商生态（Apiário、Anthropic Vertex），同时提升扩展能力和 TUI 交互（Markdown API、tmux 图像、搜索）。压缩系统的稳定性和 WSL 兼容性是当前最突出的短板。

---

### 7. 用户反馈摘要

**正面 / 满意**：
- 用户对快速修复 `HTTP_PROXY` 问题表示认可（#7049 → #7225 当日合并）。
- 社区对新增 Apiário 提供商（#7240）普遍欢迎，尤其是巴西开发者。
- 关于扩展符号链接问题（#7195）被快速关闭，表明维护者注意到了 dotfiles 用户的需求。

**痛点 / 不满意**：
- **Copilot Enterprise 用户**：压缩功能完全无法使用，且已持续 12 天无修复，多位用户表达不满。
- **WSL 用户**：路径问题导致核心文件工具不可用，破坏开发流程（#7064）。
- **长会话用户**：自动压缩机制不可靠（#6879、#7020），需要手动干预或等待 API 拒绝。
- **代理/网关用户**：Anthropic 缺少 `x-client-request-id` 导致无法在多账户代理下工作（#7161）。
- **Z.AI 用户**：`max_completion_tokens` 被忽略导致长时间输出被截断（#7143 已被 #7174 修复，但之前受影响用户已报告）。

**典型使用场景**：
- 远程沙箱环境（#7194）中 TUI 的频繁重绘导致性能问题，用户通过原始 PTY 字节流转发接入 Pi。
- 使用 `pi -p --no-session` 编写测试脚本的用户遭遇临时 session 目录残留（#6924，已关闭）。
- 在 Windows 11 上使用 GitHub Copilot 提供商时，`edit` 工具在不同模型下生成无效工具调用（#6150，已关闭）。

---

### 8. 待处理积压

**长期未响应的重要 Issue/PR**（超过 7 天未获得维护者关注或回复）：

| 编号 | 类型 | 标题 | 创建时间 | 最后维护者回应 |
|------|------|------|----------|----------------|
| [#6768](https://github.com/earendil-works/pi/issues/6768) | Issue | Copilot Enterprise 压缩失败 | 2026-07-17 | 无（用户自行多次补充信息，👍 13） |
| [#5262](https://github.com/earendil-works/pi/pull/5262) | PR | featch(ai): add Anthropic Vertex provider | 2026-05-31 | 无（已搁置近 2 个月） |
| [#6879](https://github.com/earendil-works/pi/issues/6879) | Issue | 自动压缩超过 100% 不触发 | 2026-07-20 | 无（👍 3） |
| [#7064](https://github.com/earendil-works/pi/issues/7064) | Issue | WSL 绝对路径错误 | 2026-07-24 | 无（👍 1） |
| [#7161](https://github.com/earendil-works/pi/issues/7161) | Issue | Anthropic 不收发 `x-client-request-id` | 2026-07-27 | 无 |
| [#7194](https://github.com/earendil-works/pi/issues/7194) | Issue | TUI 每秒全量重渲染 | 2026-07-27 | 无 |

**提醒**：上述积压问题（尤其是 #6768 和 #6879）涉及核心功能稳定性，建议维护者优先分配资源。此外，PR #5262（Vertex 提供商）尽管功能完整，但长时间无人审查，可能阻塞依赖该功能的用户。

---

*数据来源：Pi GitHub 仓库，统计时间窗口 2026-07-28 至 2026-07-29。*

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-07-29

**数据截止时间：2026-07-28 24:00 (UTC+8)**  
**数据来源：** [LiteLLM GitHub](https://github.com/BerriAI/litellm)

---

## 今日速览

- **活跃度极高**：过去 24 小时共产生 **77 条 Issue 更新**（新开/活跃 61，关闭 16）和 **253 条 PR 更新**（待合并 196，合并/关闭 57），社区与开发团队工作节奏紧凑。
- **版本发布**：**v1.94.0** 今日发布，主要加强 Docker 镜像签名验证，提升供应链安全。
- **关键修复落地**：多个长期悬而未决的 Bug 和回归问题被合入（如 router 策略路由注册表未清空、SCIM 嵌套组幻影用户、Helm 依赖失效等），项目整体稳定性持续推进。
- **社区反馈密集**：Gemini 缓存、OAuth 发现、流式回调丢数据等高频问题被集中报告，部分已有修复 PR 在审。

---

## 版本发布

### v1.94.0
- **发布链接：** [v1.94.0 Release](https://github.com/BerriAI/litellm/releases/tag/v1.94.0)
- **主要变化：**
  - 所有 LiteLLM Docker 镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 签名，用户可验证镜像完整性（签名密钥由 commit `0112e53` 引入）。
  - 其他更新详见 Release 页面（目前公开信息仅包含签名说明，推测内含多项 Bug 修复与小幅增强）。
- **破坏性变更/迁移注意事项：** 无明确标记。使用 Docker 部署的用户建议更新至该版本以利用镜像签名验证能力；若使用 Helm Chart 或非 root 镜像，注意同步更新（Helm 依赖的 Postgres/Redis 镜像已迁移至 `bitnamilegacy` 仓库）。

---

## 项目进展（今日合并/关闭的重要 PR）

| PR | 标题 | 状态 | 说明 |
|----|------|------|------|
| [#33289](https://github.com/BerriAI/litellm/pull/33289) | fix(router): evict strategy-router registries in upsert/delete_deployment (DB-sync path) | 已合并 (CLOSED) | 修复 DB 同步路径下自动路由/复杂路由模型注册表不随增删操作清空的长期 Bug，该问题曾导致模型从 `/v1/models` 永久消失。 |
| [#34963](https://github.com/BerriAI/litellm/pull/34963) | fix(helm): pin bundled postgres and redis to the bitnamilegacy images | 已合并 (CLOSED) | 解决 Helm Chart 安装时因 Bitnami 镜像仓库迁移导致 Postgres/Redis 拉取失败的问题。 |
| [#34962](https://github.com/BerriAI/litellm/pull/34962) | fix(aiohttp): keep keep-alive connector config when a session is rebuilt | 已合并 (CLOSED) | 修复 `AIOHTTP_SO_KEEPALIVE` 环境变量在 aiohttp session 重建后失效的问题，避免 keepalive 超时意外缩短。 |
| [#34966](https://github.com/BerriAI/litellm/pull/34966) | feat(prometheus): add service_tier label to latency and spend metrics | 已合并 (CLOSED) | 为 Prometheus 延迟和花费指标添加 `service_tier` 标签，支持按服务层级（如 flex/priority）拆分监控。 |
| [#34864](https://github.com/BerriAI/litellm/pull/34864) | [run-ci] chore(ci): promote internal staging to main | 已合并 (CLOSED) | 内部 CI 管道代码合入主分支，提升发布流程自动化程度。 |
| [#34779](https://github.com/BerriAI/litellm/pull/34779) | fix(complexity_router): escalate a session pin when a turn scores higher | 待合并 (OPEN) | 修复复杂路由 session 亲和性导致低分轮次锁死在高阶模型的缺陷，允许根据后续轮次评分自动升级。 |

**整体进展：** 今日合并/关闭 57 个 PR，其中多个是与代理稳定性、路由正确性、部署体验相关的核心修复。v1.94.0 的发布标志着安全基线提升，而 `complexity_router` 的 session 升级逻辑有望在下一版本中改善多轮对话的成本效率。

---

## 社区热点（讨论最活跃、评论最多的 Issues）

### 1. [#361](https://github.com/BerriAI/litellm/issues/361) — 🎅 I WISH LITELLM HAD... (已关闭，474 评论)
- **热度：** 累计 474 条评论，虽已关闭但作为功能 wishlist 持续被引用。
- **诉求分析：** 用户在此集中提出希望 LiteLLM 支持的功能，覆盖多供应商兼容性、路由策略、监控集成等。当前版本已实现其中部分功能，但仍有大量请求等待落地。该 Issue 可作为路线图参考的长期数据库。

### 2. [#11549](https://github.com/BerriAI/litellm/issues/11549) — [Bug]: Vertex AI gemini-2.5-pro-preview 返回空字符串 (已关闭，11 评论，4 👍)
- **影响范围：** 从 v1.72.1 升级到 v1.72.2 后，Vertex AI 所有模型返回空内容，属于严重回归。用户被迫回滚或修改配置。
- **当前状态：** 已关闭，说明已修复（可能合入后续版本）。社区对此类回归问题反应激烈，建议维护者加强回归测试。

### 3. [#23976](https://github.com/BerriAI/litellm/issues/23976) — [Bug]: Upgrade from v1.82.0-stable to v1.82.3-stable (未关闭，10 评论)
- **诉求：** 多实例部署用户报告从 `v1.82.0-stable` 升级到 `v1.82.3-stable` 出现问题，具体症状未详细说明，但标注了 `stale`。标记为 stale 后仍未获得维护者响应，社区关注度下降。

### 4. [#22998](https://github.com/BerriAI/litellm/issues/22998) — [Bug]: litellm_proxy_extras 迁移记录为已执行但列未创建 (未关闭，7 评论，4 👍)
- **严重性：** 升级后 `/v2/login` 返回 500，`/v1/mcp/server` 返回空数组，原因是数据库列未实际创建。影响生产环境认证和 MCP 功能。用户给出了详细的迁移文件分析和建议修复。
- **社区期待：** 较高优先级，建议维护者尽快审查并合入修复。

---

## Bug 与稳定性（按严重程度排列）

| 严重程度 | Issue / PR | 标题 | 状态 | 影响 | 备注 |
|----------|------------|------|------|------|------|
| 严重 | [#22998](https://github.com/BerriAI/litellm/issues/22998) | 迁移列缺失，500 错误 | OPEN | 认证、MCP 功能不可用，生产环境受阻 | 社区贡献了分析，尚无修复 PR |
| 严重 | [#26147](https://github.com/BerriAI/litellm/issues/26147) | `/ui/chat` 中 response_id 找不到 | OPEN | vLLM 后端的 Playground 可用但 UI 聊天失败 | 从 1.82.3-stable 开始，疑似回归 |
| 高 | [#24057](https://github.com/BerriAI/litellm/issues/24057) | OTEL 属性 `gen_ai.prompt` 类型无效 | OPEN | 每次请求触发 SDK 警告/错误，影响可观测性 | 已有社区讨论，建议修复 |
| 高 | [#34872](https://github.com/BerriAI/litellm/issues/34872) | Gemini 上下文缓存使用自定义 api_base 时 URL 与 auth header 错误 | OPEN | 使用自定义 endpoint 的缓存功能完全失效 | 3 个 👍，影响较多用户 |
| 高 | [#34953](https://github.com/BerriAI/litellm/issues/34953) | Streaming `/v1/messages` 丢失所有 success callback (成本追踪丢失) | CLOSED (已修复) | 流式响应时成本追踪静默丢失 | 已修复，但用户需升级至包含修复的版本 |
| 中 | [#34985](https://github.com/BerriAI/litellm/issues/34985) | MCP OAuth 发现持久化导致 issuer 锚定，一次失败后 `/authorize` 中断 | OPEN | 交互式 OAuth2 MCP 服务认证断裂 | 已有 PR [#34990](https://github.com/BerriAI/litellm/pull/34990) 修复 |
| 中 | [#34914](https://github.com/BerriAI/litellm/issues/34914) | `service_tier` 参数被 Vertex AI v1 API 500 拒绝 | OPEN | 所有 tier 值均被拒绝，影响成本优化 | 无进展 |
| 中 | [#34471](https://github.com/BerriAI/litellm/issues/34471) | `safe_deep_copy` 在高并发下崩溃 | OPEN | 并发突变导致 `dictionary changed size` | 影响多线程 SDK 使用 |

**稳定性小结：** 今日报告了多个高影响 Bug，其中数据库迁移缺陷、UI 聊天回归、Gemini 缓存、成本追踪丢失等问题直接影响生产使用。可喜的是 #34953 已修复，MCP OAuth 和 Helm 等部署相关的 Bug 也已合入。建议优先处理 #22998 和 #26147。

---

## 功能请求与路线图信号

| 功能 | Issue / PR | 说明 | 可能纳入下一版本的迹象 |
|------|------------|------|------------------------|
| **Langfuse v4 SDK & OTel 集成** | [#33383](https://github.com/BerriAI/litellm/issues/33383) | 由 Langfuse 团队提交，要求升级以支持 v4 实时 ingestion | 关联 PR 尚未出现，但属外部合作请求 |
| **Kimi K3、Inkling、Tinker 平台原生支持** | [#33921](https://github.com/BerriAI/litellm/issues/33921) | 用户需要直接使用这三个新模型 | 暂无关联 PR |
| **Provider 配额池与包级路由** | [#31823](https://github.com/BerriAI/litellm/issues/31823) | 希望在路由器中支持供应商级别配额池 | 1 个 👍，暂无 PR，但复杂性较高 |
| **Claude Gateway 支持** | [#34924](https://github.com/BerriAI/litellm/issues/34924) | 近期 Anthropic 发布的 Claude Apps Gateway | 1 个 👍，可能与 #30508 重复，社区兴趣初显 |
| **Session payload 捕获与缓存预热** | PR [#35010](https://github.com/BerriAI/litellm/pull/35010)、[#35014](https://github.com/BerriAI/litellm/pull/35014) | 复杂路由场景下，提前预热 prompt 缓存以减少冷启动成本 | **已提交 PR**，说明正在内部开发，很可能在 v1.95.x 中引入 |
| **用户附加元数据到工具调用** | [#23692](https://github.com/BerriAI/litellm/issues/23692) | 允许用户对每个 tool_call / mcp_call 添加自定义 metadata | stale 状态，暂无进展 |

**路线图信号：** 团队正积极推进 `complexity_router` 的缓存预热和 session 升级逻辑，这是提升多轮对话成本效率的重要方向。外部厂商集成（Langfuse、Claude Gateway）呼声渐高，但尚未看到对应的开发 PR。

---

## 用户反馈摘要

- **数据库迁移问题使多个用户陷入 500 错误**（#22998）：用户 `madhu19991` 反馈升级后 `/v2/login` 直接 500，经过两天排查发现列未创建，手动补全后恢复。用户对升级流程的可靠性提出质疑。
- **UI 聊天功能无法用于 vLLM 模型**（#26147）：用户 `escon1004` 表示 Playground 正常但独立 UI 页面返回 `Response not found`，需要手动构造请求，体验割裂。用户希望团队优先修复 UI 与常用后端的兼容性。
- **OpenTelemetry 集成不稳定**（#24057、#24516）：用户 `metalshank

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

**Temporal 项目动态日报 | 2026-07-29**

---

## 1. 今日速览

过去 24 小时内，Temporal 核心仓库维持中等活跃度：收到 1 条 Issue 更新（非新开，为已有增强请求的持续讨论），PR 活动密集（共 48 条更新，其中 17 条已合并/关闭，31 条待合并）。项目主要围绕 **Worker 回调（CHASM）**、**独立活动（SAA）稳定性**、**任务队列调度优化** 及 **复制流隔离** 等方向推进，同时修复了若干 goroutine 泄漏和边缘 case 的 DLQ 问题。无新版本发布。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日合并/关闭了 17 个 PR，其中对项目功能有实质性推进的关键合并包括：

- **#11320 – fix(saa): RESET_REQUESTED(keepPaused=true) maps to runState=PAUSED**  
  修复独立活动（SAA）在 `keep_paused=true` 重置时的状态转换错误，保证暂停意图不被覆盖。  
  [PR #11320](https://github.com/temporalio/temporal/pull/11320)

- **#11335 – Remove system.enableNamespaceHandoverWait dynamic config**  
  清理已废弃的动态配置项，简化命名空间交接拦截器代码。  
  [PR #11335](https://github.com/temporalio/temporal/pull/11335)

- **#11337 – Qian/namespace migration benchmark**  
  新增命名空间迁移基准测试工具，为后续复制队列替换做准备。  
  [PR #11337](https://github.com/temporalio/temporal/pull/11337)

- **#10881 – add namespace replication chasm component**  
  合并长线分支 `feature/namespace-replication` 的核心组件——基于 CHASM 的命名空间复制引擎，为替换当前复制队列打下基础。  
  [PR #10881](https://github.com/temporalio/temporal/pull/10881)

此外，多个仍在进行中的 PR（如 #11255 新增队列积压时间指标、#11268 恢复共享连接缓存、#11290 使用即时队列处理已到期任务）表明项目在 **可观测性** 和 **执行延迟优化** 上持续投入。

---

## 4. 社区热点

今日最受关注的 Issue 仍是 **#4795**（Schedules – 允许用户自定义 workflow ID，而非自动附加时间戳）。该 Issue 创建于 2023 年，积累了 7 条评论和 17 个 👍，最新更新时间为 2026-07-28，说明社区对该功能的呼声仍然强烈，值得维护团队评估下一版本的纳入优先级。  
[Issue #4795](https://github.com/temporalio/temporal/issues/4795)

PR 方面，评论数未见突出（数据未提供具体数字），但以下 PR 涉及核心稳定性改进，获得较多关注：

- **#11322 – Fix goroutine leaks**（修复泄漏测试中的所有 TODO，仅保留 sqlite 设计性泄漏）  
- **#11336 – Resend missing CAN successor instead of DLQ on non-current branch**（修复版本验证边缘 case 导致的 DLQ 问题）

---

## 5. Bug 与稳定性

今日修复/发现的 Bug 按严重程度排列：

| 严重程度 | 问题描述 | 状态 | 链接 |
|----------|----------|------|------|
| **高** | 独立活动 SAA 在 `keep_paused=true` 重置时状态错误丢失暂停意图 | 已修复（#11320 已合并） | [PR #11320](https://github.com/temporalio/temporal/pull/11320) |
| **高** | 非当前分支上 CAN 后继任务缺失导致不当 DLQ | 修复中（#11336 待合并） | [PR #11336](https://github.com/temporalio/temporal/pull/11336) |
| **中** | 多个 goroutine 泄漏（测试框架中发现的 TODO 项） | 已修复（#11322 已合并） | [PR #11322](https://github.com/temporalio/temporal/pull/11322) |
| **中** | 调度器重试可能超过 catchup 截止时间执行过期动作 | 修复中（#11316 待合并） | [PR #11316](https://github.com/temporalio/temporal/pull/11316) |
| **低** | 已到期侧效应任务错误进入定时队列而非即时队列 | 修复中（#11290 待合并） | [PR #11290](https://github.com/temporalio/temporal/pull/11290) |

项目稳定性持续提升，尤其在独立活动、调度器边界和副本一致性问题上有显著进展。

---

## 6. 功能请求与路线图信号

本期值得关注的功能请求：

- **Schedules – 自定义 Workflow ID**（#4795）：用户希望调度创建的执行使用用户定义的 workflow ID，而非自动附加时间戳。该功能已被标记为 `enhancement`，结合社区呼声（17 👍）和长期未关闭状态，很可能在下一里程碑被排入计划。  
  [Issue #4795](https://github.com/temporalio/temporal/issues/4795)

- **Query-backed Nexus Operations**（#11274）：为 Nexus 操作添加工作流查询支持，属于“以 Nexus 暴露所有 Temporal 原语”系列的一部分。PR 中提及“SDK Ergonomics”，表明这是提升开发者体验的路线图项目。  
  [PR #11274](https://github.com/temporalio/temporal/pull/11274)

- **Worker 回调（CHASM）进度**：多个 PR（#11338、#11139、#11312）不断丰富 Worker 回调功能，包括持久化回调终端状态、取消时正确返回 CanceledError、解除 Nexus 测试跳过等。该特性已接近全功能状态。  
  [PR #11338](https://github.com/temporalio/temporal/pull/11338)  
  [PR #11139](https://github.com/temporalio/temporal/pull/11139)  
  [PR #11312](https://github.com/temporalio/temporal/pull/11312)

---

## 7. 用户反馈摘要

从 Issue #4795 的评论中可提炼出用户核心痛点：

- **可靠性/可预测性**：部分用户使用 Schedules 执行幂等或基于业务标识的工作流，当前自动生成的时间戳式 workflow ID 破坏了“用户定义即 final”的直觉，导致回调或外部系统跟踪困难。
- **对简单场景的过度设计**：用户认为“一个执行一个唯一 ID”应为可选行为，默认应允许用户定义裸 workflow ID。

未发现其他明显的负面反馈。项目整体在稳定性（泄漏修复、DLQ 减少）和可扩展性（复制隔离、CHASM 回调）上获得正向社区期待。

---

## 8. 待处理积压

| 类别 | 编号 | 标题摘要 | 活跃度（👍/评论） | 最后更新 | 建议 |
|------|------|----------|------------------|----------|------|
| 功能增强 | #4795 | Schedules – 自定义 workflow ID | 17 👍 / 7 评论 | 2026-07-28 | 已近 3 年未合并，社区需求明确，建议进入下一版本评估 |
| 待合并 PR | #11199 | activity-parity: 允许按 ID 手动完成 SAA（从 Scheduled 状态） | 0 👍 / 未评论 | 2026-07-28 | 功能仅完成部分测试，需补充单元/集成测试后合并 |
| 待合并 PR | #11274 | 支持 Query-backed Nexus Operations | 0 👍 / 未评论 | 2026-07-28 | 属于 SDK 易用性路线图，代码量大，建议加速 review |
| 待合并 PR | #11263 | 复制流队列扫描添加预读缓冲区（系列 PR 第 1 部分） | 0 👍 / 未评论 | 2026-07-28 | 依赖后续 4 个 PR，需整体协调合并节奏 |

> 注：所有活跃 PR 均已包含在“最新 Pull Requests”列表中，维护者可优先关注 #11274、#11263 及 #4795 的路线图排期。

---
*日报数据来源：GitHub 仓库 temporalio/temporal，统计时间截至 2026-07-28 23:59 UTC。*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*