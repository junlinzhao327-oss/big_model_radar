# OpenClaw 生态日报 2026-07-13

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-07-12 23:12 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

好的，这是为您生成的 OpenClaw 项目日报。

---

# OpenClaw 项目动态日报 | 2026-07-13

## 今日速览

项目在过去24小时内活动量极高，共计处理了1000条Issue和PR更新，表明社区参与度和维护工作非常活跃。然而，项目健康状况值得关注：出现了两个P0（最高优先级）级别、影响稳定的回归性Bug，分别为工具输出与数据库损坏问题。此外，近300个新Issue被开启，社区对功能改进和问题修复的需求旺盛。总体而言，项目正处在快速迭代与积极维护阶段，但核心稳定性面临挑战。

## 版本发布

今日无新版本发布。

## 项目进展

今日合入了15个Pull Request，主要集中在内部重构、非紧急缺陷修复和CI/CD流程优化上，整体推进了项目的代码质量和工程基建。关键进展包括：

- **内部清理与重构**：
    - [#105720](https://github.com/openclaw/openclaw/pull/105720) 移除了AI提供商内部无用的导出项。
    - [#105580](https://github.com/openclaw/openclaw/pull/105580) 与 [#105579](https://github.com/openclaw/openclaw/pull/105579) 对WhatsApp渠道插件进行了内部逻辑重构，复用了SDK的通用功能，提升了代码可维护性。
- **用户界面修复**：
    - [#105604](https://github.com/openclaw/openclaw/pull/105604) 修复了Web UI中，会话的PR行与输入框宽度不一致的排版问题。
    - [#105594](https://github.com/openclaw/openclaw/pull/105594) 增强了Web UI中“创建PR”行的稳定性，修复了在高负载或限流情况下可能出现的展示问题。
- **Cron Jobs修复**：
    - [#105722](https://github.com/openclaw/openclaw/pull/105722) 修复了在发布流程中，当ClawHub的启动计划为空时可能导致的错误。

## 社区热点

今日社区讨论热度高度集中于几个关键问题，反映出用户对平台稳定性和安全性的迫切诉求。

1.  **跨平台桌面应用支持 (#75)**
    - **详情**: [Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)
    - **热度**: 110条评论，获81个赞，是社区最关注的功能请求。
    - **诉求**: 用户强烈希望在Linux和Windows上也能获得与macOS类似的原生桌面应用体验。此Issue长期处于讨论中，反映了社区对平台扩展性的核心需求。

2.  **严重Bug：工具输出变为不可读的图片附件 (#99241, #104721)**
    - **详情**: [Tool outputs sometimes render as image attachments...](https://github.com/openclaw/openclaw/issues/99241) (22条评论)
    - **详情**: [All tool results return "(see attached image)" literal string...](https://github.com/openclaw/openclaw/issues/104721) (12条评论)
    - **诉求**: 这是社区今天最核心的关注点。两个高度相关的Bug报告指出，在长时间运行或特定工作流中，所有工具（包括文件读取、代码执行）的实际输出会被替换为一个类似“(see attached image)”的占位符字符串，导致AI Agent无法读取关键数据，功能完全失效。此问题被标记为P0，用户情绪强烈。

3.  **严重Bug：网关内存泄漏导致OOM崩溃 (#91588)**
    - **详情**: [Critical: Gateway Memory Leak...](https://github.com/openclaw/openclaw/issues/91588)
    - **诉求**: 用户报告网关进程存在严重内存泄漏，运行2-3天后，内存占用从350MB激增至15.5GB，最终被操作系统OOM killer杀死，导致服务中断和持续重启。这是一个影响生产环境稳定性的P0级Bug。

## Bug 与稳定性

今日Bug类Issue报告活跃，除了P0级别的外，还有多个高优先级问题，项目稳定性承压。

- **P0 (严重):**
    - **所有工具返回占位符字符串 (#104721, #99241)**: 这是一个可能导致所有Agent任务失败的严重回归问题。用户反馈从文件读取到代码执行的所有工具结果都被替换为“(see attached image)”。**暂无对应的 fix PR 被合并。** 但已有提交 [#105717](https://github.com/openclaw/openclaw/pull/105717) 尝试修复“重复生成媒体文件”的问题，可能与此有关联。
    - **CLI启动命令损坏数据库 (#101290)**: 报告指出，在网关运行期间执行健康检查等CLI命令会破坏状态数据库，导致“数据库磁盘映像格式错误”。这是一个严重的回归问题。**暂无对应 fix PR。**

- **P1 (高) & 其他稳定问题:**
    - **网关内存泄漏 (#91588)**: 导致OS OOM崩溃的严重问题，影响持续运行能力。**暂无对应 fix PR。**
    - **会话硬重置循环 (#63216)**: 即使配置了宽松的内存限制，特定会话仍会反复触发上下文溢出重置。**暂无对应 fix PR。**
    - **工具参数静默丢失 (#53408)**: 在长对话后，`write`和`exec`工具的**所有参数**会被静默丢弃，导致工具调用失败。**暂无对应 fix PR。**
    - **PR: Slack附件丢失修复 (#104703)**: 针对Slack渠道附件可能因特定事件类型而丢失的P1级问题，已有一个L级规模的修复PR正在等待审核。
    - **PR: Zalo API请求超时修复 (#104017)**: 修复了Zalo渠道因API无响应导致请求卡死的P2级问题，PR已就绪。

## 功能请求与路线图信号

社区持续提出新功能请求，以下需求反应强烈，可能被纳入未来版本考虑：

- **跨平台桌面应用**: Issue #75 的持续高热度，表明 Windows 和 Linux 桌面应用是社区最期待的功能。这应被列为路线图上的高优先事项。
- **安全增强**:
    - **内存信任标记 (#7707)**: 用户希望根据信息来源（用户、网页、第三方插件）对Agent内存添加信任等级，以防止“记忆投毒”攻击。
    - **遮盖密钥 (#10659)**: 需要让Agent能“使用”API Key但不能明文“看到”它，以防止泄露。
    - **文件系统沙箱 (#7722)**: 通过配置文件限制Agent可访问的文件路径。
- **可用性改进**:
    - **TUI支持多行输入 (#10118)**: 用户希望在终端UI中使用`Shift+Enter`换行，`Enter`发送消息，而非当前一键发送导致无法编写多行命令。
    - **取消子Agent公告 (#8299)**: 用户希望有一个配置项，可以控制子Agent完成任务后是否自动在主聊天中发布总结，目前只能靠模型输出特定关键词来抑制，非常不可靠。

## 用户反馈摘要

- **对稳定性的不满**: 近期多个P0级Bug的爆发，尤其是工具输出完全失效的问题 (#104721), 引发了用户的强烈不满和焦虑，有用户直言“这完全坏了”。这表明当前的开发或测试流程需要在稳定性上投入更多。
- **对功能缺失的渴望**: Issue #75 (Linux/Windows应用) 长期高热度，累积了81个赞，真实反映了用户在跨平台使用上的痛点，他们是真实的潜在用户。
- **对易用性的刚需**: 如TUI多行输入(#10118)等功能请求，虽不复杂，但能显著提升高频用户的日常体验，这类“小痛点”的修复能有效提升社区满意度。

## 待处理积压

以下是一些长期未解决但对项目健康至关重要的问题，建议维护者重点关注：

1.  **A2A会话重复消息 (#39476)**: 2026年3月8日提出的P1级Bug，描述了两个Agent之间通过`sessions_send`通信时可能产生重复消息。虽有PR链接，但状态仍需“实时复现”，表明问题依旧。
2.  **跨执行文件系统读取状态不一致 (#71326)**: 2026年4月25日提出的P1级Bug，描述在连续的`exec`调用中读取同一个文件可能得到不同内容（陈旧数据），怀疑是进程间缓存竞争导致。此问题严重威胁工作流正确性，且已积压多日。
3.  **备份过程被会话清理打断 (#67417)**: 2026年4月15日提出的P2级Bug，描述了`openclaw backup create`命令在运行时，如果网关在清理会话文件，备份会因`ENOENT`错误失败。此问题是用户数据安全的隐患。

---

## 横向生态对比

好的，作为资深技术分析师，现基于您提供的各项目动态，为您生成一份横跨 2026年7月13日的 AI 智能体与个人 AI 助手开源生态的横向对比分析报告。

---

### AI 智能体与个人 AI 助手开源生态横向分析报告 (2026-07-13)

#### 1. 生态全景

当前，AI 智能体开源生态正处于 **“高速迭代、并行竞争”** 的爆发阶段。项目普遍呈现极高的社区活跃度，但发展路径开始出现显著分化。一方面，以 OpenClaw 和 LiteLLM 为代表的项目正面临快速增长带来的 **稳定性挑战**，P0级Bug频发，反映出在快速扩展功能时对核心可靠性的压力。另一方面，以 Pi 和 Hermes Agent 为代表的项目则在 **深度打磨特定场景**，如 TUI 体验和多模型提供者支持。一个清晰的趋势是，**“模型提供者兼容性”** 和 **“MCP/ACP 等互操作协议”** 已成为所有头部项目的必争之地，而安全性（SSRF、凭证泄露）和用户侧的生产环境管理（成本、资源控制）正从“可选”变为“刚需”。

#### 2. 各项目活跃度对比

| 项目 | 24h Issues (新开/关闭) | 24h PRs (新开/合并/关闭) | 今日 Release | 健康度评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | ~1000条更新 (含Issue/PR) | ~15个PR合并 | 无 | **⚠️ 紧急关注**：社区活跃度顶级，但出现2个P0级回归性Bug，核心稳定性承压。 |
| **Hermes Agent** | ~500条更新 (新开/关闭约368个) | ~500条更新 (新开/合并/关闭约67个) | 无 | **⚖️ 高吞吐高积压**：维护者正大规模清理积压，但PR合并瓶颈显著，新功能上线受阻。 |
| **OpenHands SDK** | 12条新开，0条关闭 | 11条新开，2条合并/关闭 | 无 | **✅ 积极迭代**：聚焦少数关键Bug修复和安全增强，项目健康度良好，节奏可控。 |
| **Pi** | 42条新开，大量关闭 | 10条 全部合并/关闭 | 无 | **✅ 高效开发**：维护者响应迅速，所有PR当日合并，闭环效率极高，项目状态健康。 |
| **LiteLLM** | 22条新开，8条关闭 | 112条更新 (83待合并，29合并/关闭) | 2个 | **⚠️ 审慎关注**：活动量极高，但出现CVSS 7.5级SSRF漏洞，且RC版本存在回归问题。 |
| **Temporal** | 低活跃 | 2个PR合并 | 无 | **✅ 平稳维护**：低活跃度，专注于长期Bug修复和版本发布筹备，未出现显著风险。 |

#### 3. OpenClaw 在生态中的定位

*   **定位：个人 AI 助手的“全能型”核心参照。** 相比于其他项目，OpenClaw 的功能覆盖面最广，试图整合 Agent、API 网关、工具链、多平台客户端（Windows/Linux/macOS）于一体，是生态中最具“大一统”野心的项目。
*   **与同类相比的优势：**
    *   **社区规模巨大**：24小时内近1000条更新，热度远超其他项目，这既是动力也是压力。
    *   **功能完整性**：相比Hermes Agent侧重平台连接、OpenHands侧重SDK，OpenClaw提供了一个完整的、开箱即用的个人助手平台，从Web UI到终端，从AI提供商到工具链。
*   **技术路线差异：**
    *   侧重于 **“自建平台”** ，而非常见的路由层（如LiteLLM）或SDK（如OpenHands）。这使得它更容易上手，但也带来了更重的维护负担。
    *   核心架构上，OpenClaw的网关与状态数据库是其特色，但本次报告显示的 **“数据库损坏”** 和 **“内存泄漏”** 两个P0级Bug，恰恰是其架构脆弱性的体现。
*   **社区规模对比：** 从更新量级看，OpenClaw和LiteLLM是第一梯队，其次是Hermes Agent。Pi 和 OpenHands 则属于小而精的社区。OpenClaw的优势在于用户粘性高（如Issue #75持续高热度），但风险在于核心Bug可能瓦解用户信任。

#### 4. 共同关注的技术方向

多个项目不约而同地核心关注以下方向，显示出行业共性需求：

| 共同技术方向 | 涉及项目 | 具体诉求 |
| :--- | :--- | :--- |
| **MCP/ACP 协议支持与增强** | **OpenClaw, OpenHands SDK, LiteLLM** | 所有项目都在讨论如何更好地支持MCP（模型上下文协议）和ACP（Agent通信协议）。如OpenHands要求订阅MCP通知，LiteLLM关注MCP工具权限，OpenClaw的A2A对话重复消息问题也与此相关。**这是行业迈向标准化的核心信号。** |
| **Agent “工具调用” 稳定性** | **OpenClaw, Hermes Agent, Pi, LiteLLM** | 多个P0/P1级Bug均与此相关：OpenClaw的工具输出变为图片、Hermes Agent的Kanban worker协议违规、Pi的工具调用竞争条件、LiteLLM的DeepSeek翻译层错误。**“工具调用”已成为Agent架构最脆弱的环节。** |
| **配额与资源控制** | **OpenHands SDK, LiteLLM** | OpenHands的 `max_concurrent_runs` 失效，LiteLLM的Compresr Guardrail（压缩器护栏）和TTFT超时等需求，都指向了 **生产环境下对成本、并发的控制需求**。 |
| **安全性 (SSRF, 凭证泄露)** | **LiteLLM, OpenClaw** | LiteLLM报告了SSRF漏洞和OAuth开放重定向；OpenClaw社区呼吁“内存信任标记”和“遮盖API Key”。**安全性正从隐形问题变为显性基础设施要求。** |

#### 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | **全栈个人AI助手平台** | 终端用户、希望快速部署个人助手的开发者 | 拥有自己的网关、数据库、Web UI，集成度高，但耦合性强。 |
| **Hermes Agent** | **多平台连接与代理路由** | 希望在不同通讯平台（Telegram, Discord等）运行AI Agent的用户 | 功能上像个“路由器”，擅长连接各种外部服务和API，但对自身核心会话管理（`risk-session-state`）的稳定性有挑战。 |
| **OpenHands SDK** | **企业级Agent开发工具包** | 企业和开发者，需要构建定制化、安全的Agent应用 | 提供底层SDK，强调安全分析器（Security Analyzer）和协议增强（ACP），更适合嵌入到现有系统中。 |
| **Pi** | **终端极客的Coding Agent** | 开发者、主要在终端（TUI/CLI）中工作的技术人员 | 聚焦于最优的终端体验和与OpenAI Codex的深度集成，开发效率极高，但平台开放性不如前两者。 |
| **LiteLLM** | **统一的AI模型/Provider网关** | 企业、开发者，需要管理数十个LLM API路由、计费和访问控制 | 核心能力是路由、翻译、成本控制和安全管理，是生态中的“基础设施”，不提供自己的Agent或UI。 |
| **Temporal** | **可编程工作流引擎** | 需要构建高可靠性、长时间运行的工作流的开发者 | 是一个通用工作流引擎，并非“AI Agent”项目，但它为构建复杂的Agent编排提供了底层基础。 |

#### 6. 社区热度与成熟度

*   **第一梯队（超高热度，快速迭代，但伴随风险）：**
    *   **LiteLLM & OpenClaw**：社区活跃度最高，几乎是“昼夜不息”。但前者因安全漏洞和RC版本回归受到关注，后者因P0级Bug和高积压承压。二者处于 **“功能领先，但伴随稳定性风险”** 的快速迭代阶段。

*   **第二梯队（高热度，高效开发，稳定导向）：**
    *   **Hermes Agent**：虽然PR积压严重，但Issue闭环速度极快（一天关闭368个），表明维护者正在从“粗放增长”转向 **“质量巩固”**。
    *   **Pi**：开发效率是所有项目中最高的，所有PR当日合并，项目健康度极佳。它处于一个 **“小而美、优而快”** 的精益开发阶段。

*   **第三梯队（中等热度，平稳发展）：**
    *   **OpenHands SDK**：活动量适中，专注于特定领域的增强（安全、MCP），项目开发者导向，社区成熟度较高，处于 **“生态化建设”** 阶段。
    *   **Temporal**：作为通用引擎，它不追求Agent功能的高频迭代，而是 **“稳定可靠”** 的系统级维护。

#### 7. 值得关注的趋势信号

1.  **“协议之争”逼近**：MCP/ACP的讨论在各项目涌现（OpenClaw, OpenHands, LiteLLM），这表明行业正在形成底层互操作标准。未来的AI Agent生态将不再局限于单个项目，而是可以像集装箱一样，进行跨平台、跨Agent的协作。**对开发者**：关注MCP标准，其将成为Agent开发的基础。**对决策者**：选型时优先考虑支持标准协议的项目。

2.  **“稳定性”成为最大的用户体验瓶颈**：从OpenClaw的“工具输出全坏”到LiteLLM的“内卷翻译层失败”，再到Pi的“压缩卡死”，**“工具调用”的不可靠性**是今天所有核心项目的一致痛点。**信号**：AI Agent的下一波增长不再是模型本身的能力，而是“工具调用”管道的健壮度。谁能先解决“Agent像黑客一样工作但随机失灵”的问题，谁就能赢得用户。

3.  **“安全”从锦上添花到雪中送炭**：LiteLLM的SSRF漏洞（CVSS 7.5）和OAuth开放重定向（CVSS 6.1）是今天报告的“爆点”。OpenClaw社区对“内存信任标记”和“遮盖API Key”的讨论也表明，当Agent能访问文件、执行代码时，安全问题已不再是理论威胁。**信号**：企业级用户在选择Agent框架时，安全能力将是首要考核项之一。那些提供原生安全机制（如OpenHands SDK的ToolShield）的项目将获得B端市场的青睐。

4.  **“生产环境成本与资源控制”需求显著**：多个项目提出“并发限制失效”（OpenHands）、“提供者过载保护”（LiteLLm的Compresr Guardrail、TTFT超时）。这表明AI Agent已度过“玩具”阶段，进入了真实的成本敏感型生产环境。**信号**：未来LLM网关与Agent平台的融合将成为趋势，LiteLLM与OpenClaw的竞合关系将加剧。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域的开源项目分析师，我将根据您提供的 Hermes Agent GitHub 数据，为您生成 2026-07-13 的项目动态日报。

---

### Hermes Agent 项目日报 (2026-07-13)

**分析师点评**：本次日报基于过去24小时（截至2026年7月12日）的社区活动数据。项目保持着极高的活跃度，Issue 和 PR 更新总数均达到 500 条，但同时也显示出巨大的闭环压力。**大量 Issue 在一天内被关闭（368条），说明项目维护者正在进行大规模的清理和整合**，但仍有大量 PR 处于待合并状态（433条），代码仓库的积压问题依然严峻。

---

### 1. 今日速览

项目整体 **高度活跃，但处于“高吞吐、高积压”状态**。

*   **社区驱动强劲**：用户在功能请求、Bug 报告和外部集成方面保持了强烈的贡献意愿。多个讨论热烈的 Issue 和 PR 反映出用户对 **平台扩展性** (如 Telegram、WeCom)、**模型提供商兼容性** (如 Gemini、Vertex AI、Copilot) 和 **本地化/UI 体验** (如 Windows 支持、桌面字体缩放) 的迫切需求。
*   **维护者响应积极**：短时间内关闭了 368 个 Issue，这表明维护者正在集中精力处理历史积压。许多 Issue 被标记为 `sweeper:implemented-on-main` (已在主分支实现) 或 `sweeper:cannot-reproduce` (无法复现)，证实了这一清理行动。
*   **核心痛点凸显**：“扫荡者（Sweeper）”机制的广泛应用以及许多 PR 被打上 `risk-*` 标签（特别是 `risk-message-delivery` 和 `risk-session-state`），暗示了项目在 **稳定性、会话管理和消息传递可靠性** 方面可能存在一定的技术债务。
*   **合并节奏缓慢**：高达 433 个待合并的 PR 数远超过 67 个已合并/关闭的数量。尽管维护者在关闭 Issue 上效率很高，但代码审查和合并的瓶颈依然显著，新功能和修复的上线速度可能因此受限。

### 2. 版本发布

无新版本发布。

### 3. 项目进展

过去24小时的项目进展主要体现在对已关闭 Issue的解决方案确认和针对具体 Bug 的修复上。虽然合并/关闭的 PR 数量不多（67条），但它们解决了几项关键问题。

*   **核心功能修复**：PR #20266 修复了一个重要的 Bug，即 `title_generator.py` 未能正确处理推理模型（如 Qwen3.5, DeepSeek）的输出，导致会话标题生成泄露模型思考过程。该 PR 直接关联并解决了 Issue #18529 (`[CLOSED] [Bug]: title_generator.py read response.choices[0].message.content directly...`)。
*   **提供商兼容性增强**：PR #20321 修复了企业对版 GitHub Copilot 端点的支持，解决了因缺少自定义头信息导致 400 错误的问题。这直接对应已关闭的 Issue #16551 (`[Bug]: Copilot OAuth client_id prevents copilot_internal token exchange...`)。
*   **社区贡献方向**：包含新平台支持（Mixin Messenger，PR#20308）和多项配置与稳定性改进（如 xAI OAuth 多账户支持 PR#62285、WeCom 流式传输修复 PR#20313）在内的一系列 PR 正在等待合并，显示社区在扩展 Hermes 生态方面有持续投入。

**项目向前迈进的程度**：项目正在快速消化社区反馈，通过关闭大量重复和已解决的 Issue，使项目路线图更清晰。关键 Bug 的修复增强了与特定模型和企业级平台的兼容性，但整体功能进展受限于 PR 合并速度。

### 4. 社区热点

本周社区讨论最热烈的话题集中在 **用户体验** 和 **提供商集成** 两个方面。

*   **桌面应用体验**：Issue #40166 ([链接](https://github.com/NousResearch/hermes-agent/issues/40166)) 要求为桌面应用增加字体大小/缩放控制，获得了 **17个👍** 和 **10条评论**。用户强烈表示标准 macOS 缩放快捷键无效，在 HiDPI 显示屏上无法正常使用。这表明用户对桌面端的原生体验有较高期望。
*   **原生 Google AI 集成**：已关闭的 Issue #12639 ([链接](https://github.com/NousResearch/hermes-agent/issues/12639)) 和 #13484 ([链接](https://github.com/NousResearch/hermes-agent/issues/13484)) 均要求支持原生 Google / Vertex AI 提供商，以绕过 OpenRouter 的限制和费用。这两个 Issue 共获得 **24个👍** 和 **28条评论**，显示用户对直接连接顶级模型提供商的强烈渴望，并且相关功能已在主分支实现。
*   **社区新提案**：开放 Issue #42864 ([链接](https://github.com/NousResearch/hermes-agent/issues/42864)) 提议将 `scope-recall` 作为官方的内存提供者插件，虽评论不多，但作为新生功能探索，值得关注。

### 5. Bug 与稳定性

过去24小时报告和讨论的 Bug 主要围绕 **平台集成、数据一致性和自动化工具**。

*   **【严重】自动化工具稳定性**：Issue #27178 (`[OPEN] [type/bug, comp/cron, P2]`) 报告了一个影响 **Kanban worker** 的 `protocol_violation` 错误。当智能体以文本回复而非按预期调用 `kanban_complete` 时，工作器会退出，且没有重试或降级机制。这直接威胁到自动化工作流的可靠性，目前尚无直接修复 PR。
*   **【中等】网络/Docker 权限问题**：已关闭的 Issue #15290 (`[BUG]: Persistent Permission denied on /opt/data/config.yaml...`) 虽然已解决，但其在 NAS 上部署 Docker 时遇到的持久化权限错误，反映了真实用户在网络存储场景下的核心痛点。
*   **【中等】技能索引退化**：Issue #38240 (`[OPEN] [type/bug, tool/skills, P3]`) 报告了一个持续存在的基础设施问题——技能索引 `degraded`。这会影响 `/docs/skills` 文档页面的正确性，是一个需要监控的技术检测问题。
*   **【低】会话逻辑异常**：已关闭的 Issue #18279 (`[Bug]: Mattermost root threads share one session...`) 指出 Mattermost 平台中，不同顶层帖子被错误共享同一会话，导致对话串扰。该问题虽已修复，但暴露了会话管理设计中可能存在的边界缺陷。

### 6. 功能请求与路线图信号

用户诉求仍然集中在提高 **灵活性**、**扩展平台支持** 和 **优化用户界面**。

*   **桌面临界功能**：**Issue #40166**（桌面应用字体缩放）的讨论热度极高。由于有高度相关的 PR #20223 (TUI/CLI 用户消息高亮) 在等待合并，**可能** 成为桌面体验优化下一阶段的重点。
*   **网关路由灵活化**：**Issue #40173** (Telegram 频道配置文件路由) 要求单个 Telegram 网关能对接不同的 Hermes 专家配置。这反映了用户对 **多智能体/多身份管理** 的需求，与项目正在推进的 `scope-recall` 内存提供者（#42864）思路一致，是走向更复杂 Agent 生态的明确信号。
*   **模型/提供商多元化**：如社区热点所述，对原生 Google/Vertex 支持已完成。一个新兴需求是提供 **模型预设**（如 Issue #20249 建议的跨会话专家按需升级），但这被标记为 `sweeper:not-planned`，说明短期内不是优先事项。

### 7. 用户反馈摘要

从近期活跃的 Issues 中提炼的用户声音：

*   **对平台集成的细节要求高**：用户 @ar-nim 报告 WhatsApp 组消息路由错误，@McoreD 指出 Discord 附件传递不可靠，显示用户对集成平台的功能完整性和准确性有严格的验收标准。
*   **安装配置体验是主要痛点**：多位用户（@kjohn1972, @athuljayaram, @jiezhengj）对 Docker 和 Windows 的安装体验表示不满。特别是 @jiezhengj 在 NAS 上的部署问题，以及 @ttomiczek 强烈指责安装脚本“破坏”了系统 `npm`，表明项目的安装流程对不同系统环境的健壮性有待加强。
*   **渴望避开中间商**：用户 @claubetosilva 和 @prasadus92 的诉求非常一致，即绕过 OpenRouter 直接使用 Gemini 和 Vertex AI，以避免 402 错误和速率限制。这表明用户对代理/中间件的透明度和成本控制有强烈需求。
*   **对问题响应速度有期待**：虽然 Issue #15895 已关闭，但用户 @herbalizer404 报告 Gemini CLI OAuth 的 429 错误，并强调“配额显示正常”，表明用户希望得到超出表面错误信息之外的、更深入的问题诊断。

### 8. 待处理积压

以下为长期开放或对项目健康度有重大影响，但尚未解决或得到明确响应的议题。

*   **待合并 PR 海啸**：**433个待合并的PR** 是项目当前最大的积压。尤其是多个标记为 `risk-message-delivery` 或 `risk-session-state` 的 PR（如 #20313, #20295, #20320），它们直接关系到核心功能的稳定性，应优先审阅和合并。
*   **技能索引异常**：**Issue #38240** (`[OPEN] [skills-index-watchdog] Skills index is stale...`) 技术基础设施的自动探测已连续多日报告状态为 `degraded`，这会影响用户和开发者的正常文档访问，需要维护者介入或检查 CI/CD 工作流。
*   **Kanban Worker 可靠性**：**Issue #27178** (`[OPEN] [Bug]: Kanban worker reports 'protocol_violation'...`) 作为影响自动化工作流稳定性的 `P2` Bug，没有直接关联的修复 PR，应该被列入维护者的近期工作列表中。
*   **桌面缩放需求**：**Issue #40166** (`[OPEN] [Desktop app]: add font size / zoom control`) 作为一个简单但用户体验影响极大的功能请求，获得了很高的社区投票，文档和优先级评估应尽快跟进。

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我将根据您提供的 GitHub 数据，生成一份结构清晰、客观专业的 OpenHands SDK 项目日报。

---

# OpenHands SDK 项目动态日报 — 2026-07-13

## 1. 今日速览

本日项目整体活跃度较高，**Issues 与 PR 的讨论和提交均保持在活跃水平**。过去 24 小时内共处理了 12 条 Issue 和 11 条 PR，但值得注意的是**没有新 Issue 被关闭，也没有新 Release 发布**，表明情况发现多于修复与交付。社区讨论焦点集中在 **Bug 修复（特别是 Agent Server 崩溃问题）** 和 **MCP/ACP 协议的相关增强与兼容性**上。尽管修复工作正在进行中，但项目在稳定性方面仍面临一定挑战，尤其是关于 Agent Server 的崩溃问题已引起社区关注。整体来看，项目处于一个**密集的功能迭代与稳定性加固并行阶段**。

## 2. 版本发布

*本日无新版本发布。*

## 3. 项目进展

今日合并/关闭的 PR 数量较少（2个），但涉及安全和历史数据迁，也值得关注。

- **【已合并】工具级安全分析器 (Security Analyzer)**
  **[PR #2911 - feat(security): add ToolShieldLLMSecurityAnalyzer](https://github.com/OpenHands/software-agent-sdk/pull/2911)**
  - **状态**: 已关闭 (Closed)
  - **摘要**: 该 PR 引入了名为 `ToolShieldLLMSecurityAnalyzer` 的安全分析功能，用于增强 SDK 的工具调用安全性。
  - **影响**: 这是项目安全能力的一次重要升级，为未来更精细化的工具安全控制奠定了基础。

- **【已关闭】修复历史对话数据不一致问题**
  **[PR #4090 - fix: heal history orphaned by pre-#4068 legacy-resume __root__ bug](https://github.com/OpenHands/software-agent-sdk/pull/4090)**
  - **状态**: 已关闭 (Closed)
  - **摘要**: 该 PR 提供了一次性的数据迁移，用于修复因之前某个 Bug 导致的历史对话记录数据孤立问题，确保旧对话可以继续正常运行。

## 4. 社区热点

本日最受关注的议题围绕 **Agent Server 的稳定性** 和 **MCP 配置兼容性** 展开，社区讨论较为深入。

- **最具争议的 Bug：Agent Server 崩溃**
  **[Issue #4096 - [Bug]: agent-server crash / Input should be a valid string...](https://github.com/OpenHands/software-agent-sdk/issues/4096)**
  - **评论**: 1
  - **诉求分析**: 这是一个因 `Pydantic` 类型校验失败导致的 `agent-server` 崩溃问题。问题发生在启用子代理（Sub-agents）并在第二次对话时，表现为 `SecretStr` 类型被错误地传入期望为字符串的位置。用户花了大量时间重现此问题，并称其为“非常棘手的 Bug”，反映了生产环境下的严重稳定性和可用性痛点。

- **备受关注的增强需求：MCP 配置项的持续性改进**
  **[Issue #4052 - fix(settings): restore MCP schema migration](https://github.com/OpenHands/software-agent-sdk/issues/4052)** 及其关联 **[PR #4013 - fix(settings): restore MCP schema migration](https://github.com/OpenHands/software-agent-sdk/pull/4013)**
  - **评论**: 1
  - **诉求分析**: 该议题讨论了 MCP 设置迁移的问题。由于之前的更改，老用户的 MCP 配置可能出现问题。社区呼吁通过正确的数据迁移路径而不是临时兼容 shim 来解决配置平滑过渡问题，体现了对配置兼容性和用户体验的高度关注。

## 5. Bug 与稳定性

今日报告的 Bug 集中在 Agent Server 的运行时错误和配置持久化上。根据严重程度排列如下：

- **【严重】Agent Server 崩溃**
  **[Issue #4096 - [Bug]: agent-server crash / Input should be a valid string...](https://github.com/OpenHands/software-agent-sdk/issues/4096)**
  - **描述**: 启用子代理后，启动第二个对话时，`agent-server` 因 Pydantic 类型校验失败而崩溃。已有修复 PR **#4097** 提出。
  - **修复状态**: 有待合并的 PR **[#4097](https://github.com/OpenHands/software-agent-sdk/pull/4097)**。

- **【严重】并行运行限制失效**
  **[Issue #4063 - bug(agent-server): max_concurrent_runs does not limit native async conversations](https://github.com/OpenHands/software-agent-sdk/issues/4063)**
  - **描述**: `max_concurrent_runs` 配置项无法限制异步（Async）API 的并发会话数，可能导致资源过载。
  - **修复状态**: 暂无关联修复 PR。

- **【中等】MCP 配置迁移问题**
  **[Issue #4052 - fix(settings): restore MCP schema migration](https://github.com/OpenHands/software-agent-sdk/issues/4052)**
  - **描述**: MCP 模式迁移未能正确应用，导致用户原有的 MCP 配置文件出现问题。
  - **修复状态**: 有关联 PR **[#4013](https://github.com/OpenHands/software-agent-sdk/pull/4013)** 和 **[#3503](https://github.com/OpenHands/software-agent-sdk/pull/3503)** 在推进。

- **【中等】历史数据恢复的 Bug**
  **[Issue #4094 - Make filestore cache checks deterministic](https://github.com/OpenHands/software-agent-sdk/issues/4094)**
  - **描述**: 文件存储缓存检查依赖于时间而非确定性结果，导致测试不稳定。
  - **修复状态**: 有关联 PR **[#4088](https://github.com/OpenHands/software-agent-sdk/pull/4088)**。

- **【较低】版本兼容性与弃用警告**
  **[Issue #4093 - ACP 0.11 drops Gemini model state from NewSessionResponse](https://github.com/OpenHands/software-agent-sdk/issues/4093)**
  - **描述**: SDK 对 `agent-client-protocol` 未设置上限，导致新版本（0.11.0）移除不稳定的字段后，与依赖该字段的 Gemini CLI 产生兼容性问题。
  - **修复状态**: 暂无修复 PR，但可能需在依赖版本上增加上限。

## 6. 功能请求与路线图信号

社区在 ACP/MCP 协议支持和代码清理方面提出了明确的增强需求，部分已有相应的 PR 在跟进，可能在下一版本中被纳入。

- **【增强】订阅 MCP 服务器通知**
  **[Issue #4059 - Subscribe to MCP tools/list_changed notifications](https://github.com/OpenHands/software-agent-sdk/issues/4059)**
  - **关联**: 已有关联 PR **[#3894](https://github.com/OpenHands/software-agent-sdk/pull/3894)**。
  - **路线图信号**: 说明 SDK 正在向支持动态、渐进式发现能力的 MCP 服务端演进。

- **【增强】弃用遗留别名并发出警告**
  **[Issue #4058 - Mark deprecated compatibility aliases](https://github.com/OpenHands/software-agent-sdk/issues/4058)**
  - **关联**: 已有关联 PR **[#4004](https://github.com/OpenHands/software-agent-sdk/pull/4004)**。
  - **路线图信号**: 这是一个重要的代码清理和兼容性管理动作，表明项目正逐步清理历史遗留问题，提升代码质量和文档清晰度。

- **【增强】开放 ACP 会话配置**
  **[Issue #4062 - Expose generic ACP session configuration options through Agent Server](https://github.com/OpenHands/software-agent-sdk/issues/4062)**
  - **关联**: 暂无关联 PR。
  - **路线图信号**: 该需求旨在增强 ACP 协议的通用性，允许用户通过 Agent Server 配置更多会话级选项（除了模型选择），这是 ACP 协议功能深化的重要一步。

## 7. 用户反馈摘要

从 Issue 评论中，我们可以提炼出以下几点用户反馈和痛点：

- **痛点：配置与启动异常导致开发停滞**：在 [Issue #4096](https://github.com/OpenHands/software-agent-sdk/issues/4096) 中，用户花费大量时间排查 Agent Server 启动失败问题，反映了配置复杂和错误提示不明确对开发效率的严重影响。
- **痛点：文档与实际功能不符**：在 [Issue #4063](https://github.com/OpenHands/software-agent-sdk/issues/4063) 中，用户发现 `max_concurrent_runs` 的文档说明与实际实现不符，表明文档维护与功能开发存在脱节，影响了用户的正确使用。
- **使用场景：依赖版本管理的挑战**：在 [Issue #4093](https://github.com/OpenHands/software-agent-sdk/issues/4093) 中，用户面临上游库版本变更（ACP 0.11）导致的向下兼容性问题，这体现了开源项目中“版本锁”和依赖管理的典型挑战。

## 8. 待处理积压

以下是一些长期未响应或状态为“陈旧 (Stale)”的重要 Issue/PR，建议维护者团队关注。

- **【陈旧，高价值】与 Claude Code 的功能对标**
  **[Issue #2055 - Feature Parity: Bridge Gap with Claude Code Capabilities](https://github.com/OpenHands/software-agent-sdk/issues/2055)**
  - **状态**: Stale
  - **原因**: 这是项目与业界先进标杆（Claude Code）进行功能对标的长期路线图。虽然近期无评论，但其目标直接关系到项目的核心竞争力和长期发展方向，不应被遗忘。

- **【陈旧，中等价值】Markdown 智能体高级功能**
  **[Issue #2186 - feat(delegation): Advanced Features for Markdown-based Agents](https://github.com/OpenHands/software-agent-sdk/issues/2186)**
  - **状态**: Stale, Help Wanted
  - **原因**: 该 Issue 列出了许多需要社区贡献的高级功能，且已标记“Help Wanted”。社区可以关注，贡献者也可以从这里入手。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 Pi 项目动态日报。

---

# Pi 项目动态日报 ｜ 2026-07-13

### 1. 今日速览

过去24小时 Pi 项目非常活跃，**共处理 42 条 Issues 和 10 个 PR，所有 PR 均已被合并或关闭，展现了高效的开发节奏**。项目维护者与社区紧密协作，快速响应并修复了多个用户反馈的 Bug，尤其是围绕 OpenAI Codex 新模型 `gpt-5.6` 系列的兼容性问题。**虽然今日无新版本发布，但大量代码合入表明下一个版本已进入密集的 bug 修复和功能稳定阶段**。社区讨论集中在模型兼容性、UI/UX 和扩展 API 上，项目整体健康度很高。

### 2. 版本发布

无。

### 3. 项目进展

今日有 10 个 PR 被合并/关闭，项目在以下几个方面取得了重要进展：

- **完善 TUI v2 体验**：`#6580` 为实验性的 TUI v2 模式添加了基于 Ledger 的全历史翻页查看器， **【重要】**。
- **修复核心 TUI 渲染 Bug**：`#6561` 通过禁用终端自动换行，修复了在高密度行（等于终端宽度）时引发的界面错乱与重绘问题，**【影响广泛】**。
- **增强图像支持**：`#6572` 解决了 TUI 模式下用户消息中包含图片块不渲染的问题，并改进了剪贴板图片粘贴的用户体验。
- **修复自定义模型兼容性**：`#6582` 修复了 Amazon Bedrock 提供者忽略 `forceAdaptiveThinking` 配置的问题，**【对高级用户利好】**。
- **修复工具调用竞争条件**：`#6559` 修复了当工具运行时切换 `/tree` 分支导致的工具结果错位问题，提高了代理（Agent）的稳定性，**【关键修复】**。
- **提升 API 扩展性**：`#6556` 将 OpenAI Codex Responses API 子路径通过扩展加载器暴露给第三方扩展，便于开发者在插件中直接使用。
- **其他修复**：`#6577` 修复了数字范围参数被协作为字符串（如 `offset: "380"`）导致的格式化问题；`#5859` 修正了 OpenAI Responses API 系统提示词的处理逻辑。

### 4. 社区热点

今日最受关注的议题集中在 **OpenAI Codex 新模型 `gpt-5.6` 系列的兼容性问题**：

- **#6477 [OPEN]** `[bug] Compaction summary requests omit the session ID, breaking compaction on some OpenAI-Codex models` **【获8个赞，5条评论】**
    - **链接**：https://github.com/earendil-works/pi/issues/6477
    - **分析**：用户报告在使用 OpenAI Codex 的 `gpt-5.6-luna` 等新模型时，任何压缩操作都会失败。核心原因是压缩请求缺少会话 ID（`session_id`），导致 Codex 无法识别模型。该 Issue **引发了大量用户共鸣**（高赞），反映了社区对新模型适配的热切期望。`#6574` 中的讨论也指向了类似原因。
- **#5886 [OPEN]** `[pkg:agent, pkg:coding-agent] AgentSession settlement/continuation and assistant-tail lifecycle bugs` **【获2个赞，6条评论】**
    - **链接**：https://github.com/earendil-works/pi/issues/5886
    - **分析**：这是一个由核心贡献者 `@mitsuhiko` 发起的、关于 Agent 会话生命周期和延续性问题的“母议题”。虽然创建已久，但**今天仍有活跃讨论**，说明修复深层架构性问题仍是社区和开发者关注的焦点。
- **#5463 [OPEN]** `fix(coding-agent): auto-compaction after final turn throws error` **【获5个赞，5条评论】**
    - **链接**：https://github.com/earendil-works/pi/issues/5463
    - **分析**：另一个关于压缩（Compaction）的高关注度 Bug。社区多位成员参与了讨论，共同分析根因，显示了社区协作解决问题的良好氛围。

### 5. Bug 与稳定性

今日报告的 Bug 主要集中在 UI 渲染、模型兼容性和 API 边界情况。

**严重级**:
- **[#6563] TUI drops image blocks from user messages**：TUI 在渲染交互式用户消息时丢弃图片块，导致用户看不到自己发出去的图片。**已有对应 PR #6572 合并修复**。
- **[#6558] Tool result attaches to wrong branch after tree navigation**：工具运行中切换分支会导致结果错位。**已被 PR #6559 修复**。

**关键级**:
- **[#6569] openai-codex: gpt-5.6-luna returns 404 while official Codex works**：用户在 Pi 中使用 `gpt-5.6-luna` 模型时出现 404 错误，但其官方 ChatGPT Codex 可正常使用。**已被关闭，显示为平台侧问题或特定配置问题**。
- **[#6571] assistant message text emitted before a tool call in the same turn never renders in the TUI**：同一轮中，工具调用前的文本不显示，造成用户信息缺失。**【尚未有明确修复方案】**。

**一般级**:
- **[#6555] Compaction/summary llm call should inherit the sessions transport settings.**：压缩调用的传输方式未继承会话设置，导致使用特定模型（如 `gpt-5.6-luna`）时失败。**【尚未有明确修复方案】**。
- **[#6568] openai-completions: Cannot read properties of undefined**：当用户消息内容为空时，序列化过程会崩溃。**已经被关闭，推测为边界情况修复**。
- **[#6574] Example reload-runtime.ts can't work**：官方扩展示例代码无法正常工作，影响开发者体验。**已被标记为 Bug 并关闭**。

### 6. 功能请求与路线图信号

今日提交的功能请求显示了用户对 **更丰富的 TUI 体验**、**更好的扩展 API** 以及 **更多提供者支持** 的兴趣。

- **可能被采纳的信号**:
    - **[#6524] Hide GPT-5.6 reasoning-summary empty placeholders**：建议隐藏某些模型推理摘要中的HTML空占位符，这是一个美化终端的简单且高价值请求，**已被合并后关闭**。
    - **[#6552] Allow extensions to request a deferred canonical reload**：希望扩展能请求“软重启”，而非必须完整的 `reload`。该请求考虑到了交互和RPC模式，**是一个设计严谨的API改进提案**。
    - **[#6579] Send low text verbosity for OpenAI Responses models**：建议为标准 OpenAI Responses 路径默认发送低文本冗余度，以提升响应速度。**已被关闭，可能在下个版本中实施**。

- **路线图信号**:
    - **对 GPT-5.6 系列的适配**：从多个 Issue 和 PR（`#6477`， `#6524`， `#6569`， `#6579`， `#6516`）看出，适配 OpenAI 最新的 `gpt-5.6` 模型系列是 **当前的首要任务**。社区希望尽快解决身份验证、功能兼容性参差不齐等问题。
    - **扩展生态的“稳定性”**：`#6574` 示例代码失效，`#6573` 扩展加载器路径问题，反映出 **扩展开发者体验有待提升**，这是项目走向成熟生态的关键步骤。

### 7. 用户反馈摘要

- **痛点**:
    - “使用 Amazon Bedrock 的 `/tree` 分支摘要功能时，总是报错 'No API key found'，即使我已经配置好环境凭证。” —— `#6324`
    - “每次启动 Pi 后，我自定义的快捷键都不生效，必须执行 `/reload` 才行。” —— `#6459`
    - “我试图在一个扩展里调用 `@earendil-works/pi-ai/providers/all`，结果解析路径错了！” —— `#6573`
    - “使用 `--mode rpc` 时，如果提供者接受请求但不返回JSON，整个代理就挂死了。” —— `#6581`

- **满意点**:
    - **社区互动度高，修复速度快**：许多用户报告的问题在一天或几天内就被修复并合并，如 `#6558`、`#6563` 和 `#6562` 都在当天解决了。这显著提升了用户的参与度和满意度。
    - **对 Codex 模型持续支持受到欢迎**：尽管存在 Bug，但社区对新模型（如 `gpt-5.6`）和 Codex 提供者的支持表现出极高的热情。

### 8. 待处理积压

以下为长期存在且仍有讨论的活跃 Issue，需要维护者重点关注：

- **#5886 [OPEN]** `[pkg:agent, pkg:coding-agent] AgentSession settlement/continuation and assistant-tail lifecycle bugs`。 这是一个架构性的“母议题”，**已经存在近一个月**，涉及 Agent 核心的生命周期管理，解决它可能会修复多个相关Bug。
- **#5463 [OPEN]** `fix(coding-agent): auto-compaction after final turn throws error`。 关于自动压缩的 Bug，**依然处于开放状态**，尽管有大量讨论，但尚未有统一的修复方案。
- **#6324 [OPEN]** `[inprogress] /tree branch summarization throws "No API key found" for ambient-credential providers`。 **已有一些进展**，但对于无 API Key 的提供者，该问题依然待解。
- **#5329 [OPEN]** `Expose when Pi is waiting on user input for host integrations`。 一个对开发符合 I/O 集成非常重要的 API 请求， **已存在超过一个月**，对于构建高级工作流（如与 TUI、IDE 集成）至关重要。

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 (2026-07-13)

## 1. 今日速览

过去 24 小时内，LiteLLM 项目继续保持**极高活跃度**：共处理 30 条 Issue 更新（新开 22，关闭 8），112 条 PR 更新（待合并 83，合并/关闭 29），并发布了两个版本。社区在翻译层（DeepSeek V4、Gemini）、安全（SSRF、OAuth 开放重定向）以及回调/日志稳定性方面反馈密集，项目团队也在紧锣密鼓地推进修复和功能增强。整体健康度良好，但安全漏洞和回归问题需优先关注。

## 2. 版本发布

项目于近期发布了两个版本，均强调 Docker 镜像签名验证：

- **[v1.93.0-rc.1](https://github.com/BerriAI/litellm/releases/tag/v1.93.0-rc.1)**：候选版本，主要变更包含在后续正式版中，目前无破坏性变更说明。
- **[v1.92.0](https://github.com/BerriAI/litellm/releases/tag/v1.92.0)**：正式版，同样包含 Cosign 签名验证。但用户报告称该版本缺失 PR #32339（修复 `fastapi` 可选依赖），导致 `litellm.completion(..., tools=...)` 因缺少 `fastapi` 而崩溃（见 [#32993](https://github.com/BerriAI/litellm/issues/32993)）。**建议升级用户注意检查依赖完整性，或等待后续 patch 版本。**

> 迁移注意事项：两个版本均无已知破坏性变更，但 v1.92.0 用户需确保 `fastapi` 作为可选依赖正确安装（或使用完整安装命令）。v1.93.0-rc.1 为候选版，不建议生产环境直接使用。

## 3. 项目进展

今日共合并/关闭 **29 个 PR**，推动以下关键进展：

- **Bedrock Converse 修复**：解决了空用户消息被 Bedrock 拒绝的问题（PR [#33018](https://github.com/BerriAI/litellm/pull/33018)、[#33020](https://github.com/BerriAI/litellm/pull/33020)），对应 Issue [#33016](https://github.com/BerriAI/litellm/issues/33016)。
- **Fireworks AI 计费修正**：PR [#33017](https://github.com/BerriAI/litellm/pull/33017) 修复了缓存提示 token 计费未使用 `cache_read_input_token_cost` 的问题。
- **日志回调顺序保护**：PR [#33008](https://github.com/BerriAI/litellm/pull/33008) 使用有序集合规避 `set()` 导致回调顺序非确定性问题。
- **代理安全管理**：PR [#33012](https://github.com/BerriAI/litellm/pull/33012) 禁止在请求体中传递 `aws_profile_name`，防止客户端控制 AWS 凭证。
- **UI 和文档**：PR [#29883](https://github.com/BerriAI/litellm/pull/29883) 为批量邀请用户自动创建 API key；PR [#33013](https://github.com/BerriAI/litellm/pull/33013) 改进 PR 模板要求 QA runbook。

此外，以下长期 issue 被关闭，表明相关缺陷已修复或纳入后续规划：UI 仪表盘 MCP 工具列表问题（[#22755](https://github.com/BerriAI/litellm/issues/22755)）、Prometheus 指标重复计数（[#19929](https://github.com/BerriAI/litellm/issues/19929)）、Prisma 重连失败（[#25143](https://github.com/BerriAI/litellm/issues/25143)）、Scheduler 排序异常（[#25157](https://github.com/BerriAI/litellm/issues/25157)）等。

## 4. 社区热点

以下 Issue/PR 引发了最热烈的讨论：

- **[#8842](https://github.com/BerriAI/litellm/issues/8842)**：`CustomLogger` 回调在 Router 的 `acompletion` 中未被触发。共 25 条评论、13 个 👍，创建于 2025-02-26，至今未修复。用户提供了完整可复现示例，核心诉求是自定义日志记录在工作流中的可靠性。

- **[#26395](https://github.com/BerriAI/litellm/issues/26395)**：DeepSeek V4 Pro 多轮对话在第二轮即失败，报错 `BadRequestError`。19 条评论、25 个 👍，直接影响了使用 DeepSeek 的 Claude 兼容模式用户。社区对“翻译层”兼容性高度关注。

- **[#33001](https://github.com/BerriAI/litellm/issues/33001) 和 [#33000](https://github.com/BerriAI/litellm/issues/33000)**：两个安全漏洞报告分别涉及 OAuth 开放重定向（CVSS 6.1）和动态透传 SSRF（CVSS 7.5），提交者 `@Correctover` 提供了详细攻击路径和复现步骤。社区反响强烈，但暂未看到官方修复 PR。

- **[#32992](https://github.com/BerriAI/litellm/issues/32992)**：通过 Codex 使用 LiteLLM 代理 DeepSeek V4 Pro 时出现 tool_call 顺序 400 错误。用户试图解决 Codex 不再支持 `chat/completions` 的问题，反映了对“调用层”兼容性的实际需求。

## 5. Bug 与稳定性

按严重程度排列今日报告的 Bug：

| 严重程度 | Issue | 描述 | 修复 PR |
|----------|-------|------|---------|
| **严重** | [#33001](https://github.com/BerriAI/litellm/issues/33001) | OAuth 开放重定向 (CVSS 6.1) – `MCP_TRUSTED_REDIRECT_ORIGINS` 通配符可被利用 | 暂无 |
| **严重** | [#33000](https://github.com/BerriAI/litellm/issues/33000) | SSRF – `pass_through` 端点未验证目标 URL (CVSS 7.5) | 暂无 |
| **高** | [#26395](https://github.com/BerriAI/litellm/issues/26395) | DeepSeek V4 Pro 多轮对话失败（`reasoning_content` 残留） | 暂无 |
| **高** | [#26444](https://github.com/BerriAI/litellm/issues/26444) | `get_supported_openai_params` 仍报告 Claude Opus 4.7 支持 `temperature`，但 API 已拒绝 | 暂无 |
| **中** | [#32996](https://github.com/BerriAI/litellm/issues/32996) | OTEL 日志事件因 `None` 属性值被 OTLP exporter 静默丢弃 | 暂无 |
| **中** | [#32973](https://github.com/BerriAI/litellm/issues/32973) | 旧版 `thinking` 参数未自动升级为 `adaptive`，导致 Claude 4.6+ 模型 400 错误 | 暂无 |
| **中** | [#33016](https://github.com/BerriAI/litellm/issues/33016) | Bedrock Converse 空用户消息替换仅支持 list 类型，string 类型未处理 | [#33018](https://github.com/BerriAI/litellm/pull/33018) & [#33020](https://github.com/BerriAI/litellm/pull/33020) |
| **低** | [#33003](https://github.com/BerriAI/litellm/issues/33003) | `get_combined_callback_list` 使用 `set()` 破坏回调顺序 | [#33008](https://github.com/BerriAI/litellm/pull/33008) |
| **低** | [#32982](https://github.com/BerriAI/litellm/issues/32982) | soupsieve CVE 修复未传播到外部 PR 目标分支，osv-scan 持续失败 | 暂无 |
| **低** | [#32984](https://github.com/BerriAI/litellm/issues/32984) | `voyage-4-large` 模型缺失定价配置，导致 mode/pricing 为空 | 暂无 |
| **低** | [#32962](https://github.com/BerriAI/litellm/issues/32962) | `validate_environment` 对 zai 模型返回假性全绿（即使 `ZAI_API_KEY` 未设置） | 暂无 |

## 6. 功能请求与路线图信号

今日新增/活跃的功能性需求及对应 PR 信号：

- **Compresr Guardrail** (PR [#33019](https://github.com/BerriAI/litellm/pull/33019))：新增“压缩器”护栏，在请求发送至模型前自动缩减上下文（工具输出、RAG 块、搜索结果），降低 token 消耗。适用于 `/chat/completions`、`/v1/messages` 和 `/v1/responses`。该 PR 处于开放状态，可能纳入 v1.93 或后续版本。

- **TTFT 超时与流式空闲检测** (PR [#30337](https://github.com/BerriAI/litellm/pull/30337))：为 Router 添加首 token 到达时间（TTFT）超时和流式空闲超时，用于检测挂起/卡顿的 Provider。对非流式调用同样适用，是生产环境中提升可用性的重要功能。

- **Tool Permission Guardrail 日志级别优化** (Issue [#32778](https://github.com/BerriAI/litellm/issues/32778))：用户建议将预期的工具权限事件从 `WARNING` 降级，减少日志噪音。此类企业级可观测性需求表明项目在向生产环境强化。

- **Anthropic Claude Code Advisor 集成** (Issue [#25516](https://github.com/BerriAI/litellm/issues/25516))：跟踪 Anthropic Advisor 策略在 Claude Code 中的 rollout。虽标记为“stale”，但 Claude Code 相关功能（如 `claude code` 标签）频繁出现，显示出社区对 Agent/工具使用场景的重视。

- **Skill Hub 源链接硬编码修复** (Issue [#33007](https://github.com/BerriAI/litellm/issues/33007))：仓库默认分支非 `main` 时，Skill Hub UI 中的源链接 404。请求友好性改进。

## 7. 用户反馈摘要

从 Issue 评论和描述中提炼的真实用户痛点与使用场景：

- **痛点：翻译层兼容性不足**  
  - 多位用户使用 DeepSeek V4 Pro 通过 Anthropic 兼容端点调用时，第二轮回话即失败（[#26395](https://github.com/BerriAI/litellm/issues/26395)）；类似问题也出现在 Codex 使用工具调用时（[#32992](https://github.com/BerriAI/litellm/issues/32992)）。用户期望 LiteLLM 能更好地处理 `reasoning_content`、`tool_calls` 的格式转换。

- **场景：企业内部部署与 SSO**  
  - 用户 `@azizbyahia` 描述了 LiteLLM 部署在 oauth2-proxy 后时，自定义 SSO 登录处理器被绕过（[#19856](https://github.com/BerriAI/litellm/issues/19856)）。这反映了企业对统一身份认证和 UI 重定向控制的需求。

- **对可观测性异常的不满**  
  - 多个用户指出 Prometheus 指标重复计数（[#19929](https://github.com/BerriAI/litellm/issues/19929)）和 OTEL 事件静默丢失（[#32996](https://github.com/BerriAI/litellm/issues/32996)）导致监控仪表盘不准确。日志回调顺序被破坏（[#33003](https://github.com/BerriAI/litellm/issues/33003)）也影响了自定义日志工作流。

- **安全意识的提升**  
  - 安全研究员 `@Correctover` 提交了两份详细的安全漏洞报告（[#33001](https://github.com/BerriAI/litellm/issues/33001)、[#33000](https://github.com/BerriAI/litellm/issues/33000)），影响评分 6.1 和 7.5。用户期待官方尽快发布修复版。

- **对模型支持缺位的失望**  
  - 用户 `@akapur99` 发现 `voyage-4-large` 未被收录在价格配置中，导致定价未知（[#32984](https://github.com/BerriAI/litellm/issues/32984)）；类似地，Gemma 4 模型视频输入被拒（[#25291](https://github.com/BerriAI/litellm/issues/25291)）。用户希望模型支持保持更新及时。

## 8. 待处理积压

以下 Issue/PR 长期未获得维护者回应，但社区关注度较高，建议优先处理：

| 类型 | 编号 | 标题 | 创建时间 | 最后更新 | 备注 |
|------|------|------|----------|----------|------|
| Issue | [#8842](https://github.com/BerriAI/litellm/issues/8842) | Router 的 acompletion 不触发 CustomLogger 回调 | 2025-02-26 | 2026-07-12 | 👍13，25 评论，1.5 年未修复 |
| Issue | [#19856](https://github.com/BerriAI/litellm/issues/19856) | oauth2-proxy 后 UI 重定向绕过自定义 SSO 处理器 | 2026-01-27 | 2026-07-12 | 👍3，影响企业部署 |
| Issue | [#22755](https://github.com/BerriAI/litellm/issues/22755) | UI 仪表盘无法列出 MCP 工具

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 Temporal 项目 GitHub 数据，我为您生成了 2026-07-13 的日报。

---

### Temporal 项目动态日报 | 2026-07-13

**分析师点评：** 项目在本日处于低活跃度状态，暂无新版本发布。不过，社区就一项关于错误信息红action的长期遗留问题（Issue #10716）展开了新的讨论，同时一个存在已久的 Bug 修复 PR（PR #8821）被合并，这对工作流稳定性有积极意义。整体来看，项目在维护和清理方面有所推进。

---

#### 1. 今日速览

项目在 2026 年 7 月 12 日至 13 日期间活跃度中等偏低。昨日无新版本发布，但合并了两个关键 PR：一个修复了长期存在的“ContinuedFailure”逻辑 Bug（PR #8821），另一个是为 1.32.0 版本发布做准备的基础分支合并（PR #11023）。社区方面，关于 Nexus handler 错误红action的 Issue（#10716）获得了新的评论，反映出用户对代码质量和安全性的持续关注。

#### 2. 版本发布

无新版本发布。

#### 3. 项目进展

昨日合并的两个 PR 标志着项目在 Bug 修复和版本发布流程上的稳步推进。

- **长期 Bug 修复合并：** #8821 `[CLOSED] Fix ContinuedFailure not cleared on null success payloads` 被合并。该修复解决了一个影响工作流状态的 Bug：当工作流以 `null` payload 成功完成时，`ContinuedFailure`（续传失败）属性未能被正确清除。这可能导致下游逻辑错误判断。此修复增强了工作流完成的健壮性。
  - **影响评估：** 中等。修复了一个可能在特定场景下导致状态错误的逻辑缺陷。
  - **链接：** https://github.com/temporalio/temporal/pull/8821

- **版本发布准备：** #11023 `[CLOSED] 1.32.0: Prepare release branch` 被合并。这是一个由 CI/CD 机器人创建的例行流程 PR，用于覆写治理文件并更新依赖，为即将到来的 1.32.0 版本发布做好了分支准备。这预示着新版本即将发布。
  - **影响评估：** 重大。标志着 1.32.0 版本发布流程的正式开始。
  - **链接：** https://github.com/temporalio/temporal/pull/11023

#### 4. 社区热点

- **#10716 `Clarify scope of "redact certain errors" TODOs in history Nexus handler`**
  - **状态：** OPEN
  - **热度：** 虽仅有 2 条评论，但作为昨日唯一活跃的 Issue，显示社区对一个遗留的、关于信息安全的 TODO 项感兴趣。诉求很明确：希望开发者能明确 `service/history/handler.go` 中两处 TODO 的具体实施范围，即澄清哪些错误在返回给客户端前需要进行敏感信息红action处理。这反映了社区对生产环境中错误信息安全的重视。
  - **链接：** https://github.com/temporalio/temporal/issues/10716

#### 5. Bug 与稳定性

昨日无新增 Bug 报告，但一个已提交 7 个月的重要 Bug 修复被合并：

- **Bug:** `ContinuedFailure` 未在 `null` 结果负载时被清除 (PR #8821)
  - **严重程度：** **高**。该 Bug 会导致工作流状态机状态不一致，可能在特定业务逻辑中引发错误。
  - **修复状态：** **已合并**。修复 PR #8821 已合并入主干，将在下一个版本中发布。
  - **链接：** https://github.com/temporalio/temporal/pull/8821

#### 6. 功能请求与路线图信号

昨日未发现用户直接提出的新功能请求。但结合当日动态，可以识别出以下路线图信号：

- **即将发布的 1.32.0 版本 (信号源: PR #11023):** 项目已开始为新版本准备发布分支，这通常是版本迭代周期结束的信号。虽然本次无具体功能更新日志，但可预期该版本将包含过去一段时间内积累的特性与修复。
  - **链接：** https://github.com/temporalio/temporal/pull/11023

#### 7. 用户反馈摘要

- **对代码质量与安全的关注：** Issue #10716 的讨论表明，用户（或贡献者）正在深入审查 Temporal 的核心代码（`service/history/handler.go`），并关注其生产环境下的安全性。对于 “TODO” 项（尤其是涉及数据安全，如信息红action）被长期搁置感到担忧，希望得到官方的明确澄清和实施承诺。
  - **链接：** https://github.com/temporalio/temporal/issues/10716

#### 8. 待处理积压

- **#10716 [OPEN] Clarify scope of "redact certain errors" TODOs in history Nexus handler**
  - **创建时间：** 2026-06-15
  - **重要性：** **高**。该 Issue 直接指向代码中的 TODO 项，涉及数据安全，且已持续一个月未得到核心维护者的明确回复。虽然是技术债务，但随着 Nexus 功能的成熟，解决这些安全相关的 TODO 应提上日程。
  - **链接：** https://github.com/temporalio/temporal/issues/10716
- **潜在积压项：**
  - **PR #8821** 从创建（2025-12-14）到合并（2026-07-12）经历了约 7 个月，虽然最终被合并，但较长的处理周期也反映出项目在审查和合并长期待处理的 PR 方面可能存在一定的积压或优先级分配问题。
  - **链接：** https://github.com/temporalio/temporal/pull/8821

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*