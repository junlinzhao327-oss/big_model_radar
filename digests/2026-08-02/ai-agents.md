# OpenClaw 生态日报 2026-08-02

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-01 23:15 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告



---

## 横向生态对比

# 开源 AI 智能体生态横向对比分析报告（2026-08-02）

## 1. 生态全景

个人 AI 助手与自主智能体开源生态正经历从"能跑"到"可信、可控、可治理"的转型。Hermes Agent 与 LiteLLM 的密集迭代表明核心工具层仍在快速扩张功能边界，而 OpenHands SDK 与 Temporal 的动向则显示安全加固、企业级治理和稳定性打磨已提升至与功能开发同等重要的地位。社区对 A2A 协议互操作、token 成本优化、模型自动路由、插件生命周期治理等横切议题的关注高度一致，反映出生态正从单一工具孤岛走向互联互通的企业级基础设施。整体判断：生态处于高活跃度的功能爆发期，同时治理与安全标准正在同步建立。

## 2. 各项目活跃度对比

| 项目 | Issues 动态 | PR 动态 | Release | 健康度评估 |
|---|---|---|---|---|
| **OpenClaw**（核心参照） | 今日无动态数据 | 今日无动态数据 | — | 数据缺失，无法评估 |
| **Hermes Agent** | 442 条更新（新开/活跃 321，关闭 121） | 500 条更新（待合并 391，合并/关闭 109） | 无新版本 | 极高活跃，密集迭代，维护者响应快；但更新器相关 P1 bug 集中暴露，需关注质量稳定性 |
| **OpenHands SDK** | 4 条活跃（全部开放） | 13 条更新（待合并 11，合并/关闭 2） | **v1.40.0**（含 secrets 持久化安全修复） | 健康活跃，安全加固与模型兼容性并进；Issue 侧偏冷，社区讨论热度集中于治理议题 |
| **Pi** | 今日无动态数据 | 今日无动态数据 | — | 数据缺失，无法评估 |
| **LiteLLM** | 39 条更新（新开/活跃 32，关闭 7） | 177 条更新（待合并 124，合并/关闭 53） | **v1.95.0-rc.3**（cosign 签名） | 高强度迭代，PTU 计费/Rust 迁移等多线推进；124 条待合并 PR 积压值得注意 |
| **Temporal** | 1 条更新（历史 bug 关闭） | 13 条更新（待合并 7，关闭/合并 6） | 1.32.0 发布分支准备中 | 中等活跃，以回归修复和发布准备为主，稳定性导向明显 |

## 3. OpenClaw 在生态中的定位

今日摘要未包含 OpenClaw 的社区动态，无法进行数据化的竞品对比。但从其"核心参照"的角色设定及生态格局推断，OpenClaw 大概率定位为个人 AI 助手的基础框架层，与 Hermes Agent（用户终端型）、OpenHands SDK（软件自主智能体开发型）、LiteLLM（网关路由型）形成互补而非直接竞争。若 OpenClaw 保持"参照系"地位，其技术路线可能强调架构简洁性、协议标准化与插件生态开放性；社区规模需补充数据后评估。建议后续跟踪时优先补齐该项目的 Issue/PR/Release 数据，以便完成横向定量对比。

## 4. 共同关注的技术方向

| 方向 | 涉及项目 | 具体诉求 |
|---|---|---|
| **企业级治理与安全** | OpenHands SDK、LiteLLM、Hermes Agent | OpenHands #4273 要求治理层（文件访问控制、命令白名单、成本预算、审计）；LiteLLM 修复 IDOR 漏洞、secrets 持久化问题；Hermes 修复 Discord 门控隔离性破坏 |
| **Token 成本优化** | Hermes Agent、LiteLLM、OpenHands SDK | Hermes #4379 实测 73% API 调用为固定开销；PR #76458 提出 per-turn 请求预算；LiteLLM 并行推进 PTU 计费与 auto-router 成本可视化；OpenHands #3442 智能模型选择以降低多模型使用成本 |
| **MCP / A2A 协议互操作** | Hermes Agent、LiteLLM | Hermes #514 讨论 A2A 与 MCP 互补关系；LiteLLM 出现 4 个 MCP 相关 issue，集成问题集中爆发 |
| **模型兼容性与自动路由** | OpenHands SDK、LiteLLM、Hermes Agent | OpenHands 适配 Claude Opus 5；LiteLLM 探索 Markov 决策路由策略；Hermes 讨论 Ollama 原生 API 集成 |
| **更新机制与客户端可靠性** | Hermes Agent、Temporal | Hermes macOS 更新器连环故障（4 个 P1/P2 bug 今日关闭）；Temporal 定位 CI 大规模失败根因 |
| **插件/钩子生命周期治理** | Hermes Agent、OpenHands SDK | Hermes #64231 要求统一钩子验收标准；OpenHands PR #4327 扩展 hooks.json 发现路径 |

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|---|---|---|---|
| **OpenClaw** | 核心参照，定位未明确 | — | 数据不足 |
| **Hermes Agent** | 全渠道个人 AI 助手（Telegram/WhatsApp/Discord/桌面端），强调对话体验与多 Provider 接入 | 个人用户与爱好者，追求开箱即用 | 网关-适配器架构，插件系统，技能（Skills）机制；迭代速度快但更新器稳定性和配置隔离性偏弱 |
| **OpenHands SDK** | 软件自主智能体开发框架，Agent Canvas 可视化，强调可编程性与企业集成 | 开发者、企业 R&D 团队 | SDK 形态，社区治理机制（hooks），命令行/画布双交互；Issue 基数小但语义清晰，适合二次开发 |
| **LiteLLM** | AI 网关/代理层，聚焦模型路由、统一计费、可观测性与安全 | 平台工程师、SRE、企业 AI 基础设施团队 | 代理架构，100+ Provider 适配，PTU/预算/审计体系；高吞吐场景下性能焦虑推动 Rust 迁移计划 |
| **Temporal** | 持久化工作流编排引擎，保障分布式任务可靠执行 | 后端/平台工程师 | 事件溯源 + 确定性执行模型，CRDT/HSM 状态管理；非智能体专用，但构成 Agent 任务编排的可信底座 |

## 6. 社区热度与成熟度

- **快速迭代阶段（功能扩张为主）**：**Hermes Agent**（442 Issues / 500 PR，日更量级相当于 LiteLLM 的近 3 倍）、**LiteLLM**（177 PR / 39 Issues，多线并行开发，RC 版本频发）。两者共同特征是功能需求旺盛、版本节奏快、但存在一定的质量债（Hermes 更新器 bug 集中，LiteLLM 待合并 PR 积压）。
- **质量巩固阶段（稳定与安全优先）**：**OpenHands SDK**（单版本发布 + 多项安全修复 + 合并少量 PR，问题导向明确）、**Temporal**（活跃度中等，聚焦回归修复与发布分支准备，CI 稳定性为当前重点）。
- **数据不足**：OpenClaw、Pi 今日无动态，无法判定成熟度。

## 7. 值得关注的趋势信号

1. **安全与治理正在成为 AI 智能体采用的前置条件**。OpenHands 将治理层列为最高热度需求，LiteLLM 一日内合入 IDOR 安全修复，Hermes 出现多租户隔离性 bug——三线共振表明企业级用户不再接受"先跑起来再说"，可审计、可管控、可隔离是进入生产环境的门票。

2. **Token 成本优化从经验主义走向数据驱动**。Hermes #4379 用真实监控数据量化固定开销占比（73%），并直接催生预算控制提案；LiteLLM 的 PTU 计费与成本仪表盘也在同步落地。对开发者而言，构建 AI 应用时应将 token 计量与预算控制内建为第一公民能力，而非事后补救。

3. **MCP 与 A2A 的协议分层正在形成共识**。Hermes 社区讨论明确"MCP 管工具，A2A 管智能体"，LiteLLM 的 MCP 集成问题集中爆发说明网关层需要为 MCP 流量提供专属治理。标准之争尚未结束，但"工具协议 + 智能体协议"分层已成为主流心智模型。

4. **客户端更新机制是个人 AI 助手用户信任的隐性杀手**。Hermes 今日一次性关闭 3 个 P1 级更新器 bug，用户对自动更新的信心明显受损。桌面端/移动端 AI 助手的 OTA 可靠性，将直接影响产品口碑与留存。

5. **模型路由从静态配置走向动态策略**。OpenHands 的"智能模型选择"、LiteLLM 的 Markov 路由策略、Hermes 的 per-turn 模型覆盖特性，共同指向同一目标：将模型选择交给系统而非用户。这背后是模型种类爆炸与成本/质量权衡复杂化的必然结果，也预示着"模型路由层"将成为 AI 基础设施的独立品类。

---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-02

## 今日速览

过去24小时项目活跃度极高：**442条Issue更新**（新开/活跃321条，关闭121条）与**500条PR更新**（待合并391条，已合并/关闭109条）均维持在高位，无新版本发布。社区讨论热度集中在A2A协议支持（#514，25评论/28👍）、token开销分析（#4379，20评论）与Ollama原生API集成优化（#4505，15评论/4👍）三大议题；桌面端（Desktop）安装/更新链路出现集中式Bug报告，至少5个P1/P2级问题指向更新器逻辑缺陷，但对应的修复PR已同步上线；插件生命周期治理（#64231）与xAI会话卡死（#69078）是当前最受关注的架构性议题。整体来看项目处于密集迭代期，社区参与度高，维护者响应速度快。

---

## 项目进展

今日无新版本发布，但**109个PR已合并/关闭**，其中多个修复落地值得关注：

- **[#59175] [已关闭]** 修复Codex后台审查技能的读-写竞态问题：要求先调用 `skill_view` 读取完整SKILL.md后再添加支持文件，加强技能执行的顺序约束 [链接](https://github.com/NousResearch/hermes-agent/pull/59175)
- **[#46260] [已关闭]** Windows 10安装器在"desktop"阶段npm install失败的P2级Bug已被标记为已在main分支实现（sweeper:implemented-on-main），Windows平台安装体验得到修复 [链接](https://github.com/NousResearch/hermes-agent/issues/46260)
- **[#74836] [已关闭]** macOS应用内更新被残留二进制永久破坏的P1级问题已完成修复，`resolveUpdaterBinary()` 增加版本门控 [链接](https://github.com/NousResearch/hermes-agent/issues/74836)
- **[#74532] [已关闭]** Codex辅助适配器错误地迭代已完成Responses对象的问题已关闭，涉及OpenAI流式响应兼容性 [链接](https://github.com/NousResearch/hermes-agent/issues/74532)
- **[#74531] [已关闭]** macOS应用内更新"另一个更新正在运行"死循环的P1级问题已关闭，属于更新器自身不退出导致 [链接](https://github.com/NousResearch/hermes-agent/issues/74531)
- **[#74570] [已关闭]** 桌面端pin/unpin被`pullRemotePins`竞态静默回滚的问题已修复 [链接](https://github.com/NousResearch/hermes-agent/issues/74570)
- **[#73298] [已关闭]** 预检token估算对thinking模型计数偏差导致压缩提前至真实用量的~27%即触发，P1级问题已修复 [链接](https://github.com/NousResearch/hermes-agent/issues/73298)
- **[#72348] [已关闭]** Discord适配器allow/deny门控为进程级共享、破坏per-profile隔离的安全问题已关闭 [链接](https://github.com/NousResearch/hermes-agent/issues/72348)
- **[#74942] [已关闭]** 更新器PID检查误判自身为"另一个实例"的P1级问题已修复 [链接](https://github.com/NousResearch/hermes-agent/issues/74942)
- **[#5012] [已关闭]** `delegate_task` 接受provider/model参数的特性已完成（按标签推断为已合并/关闭） [链接](https://github.com/NousResearch/hermes-agent/issues/5012)

**新提交的重要PR**（今日创建）：

- **[#76459]** 修复Windows上系统Node优先于Hermes托管Node的路径优先级问题，涉及Desktop后端与安装器 [链接](https://github.com/NousResearch/hermes-agent/pull/76459)
- **[#76460]** 修复工具执行器在硬中断时未发出工具结果、导致消息角色交替异常的问题 [链接](https://github.com/NousResearch/hermes-agent/pull/76460)
- **[#76458]** 为每个用户turn增加物理主Agent提供方请求预算（默认关闭） [链接](https://github.com/NousResearch/hermes-agent/pull/76458)
- **[#76461]** 支持自定义systemd单元名称，提供稳定的网关服务单元配置 [链接](https://github.com/NousResearch/hermes-agent/pull/76461)

---

## 社区热点

### 1. A2A（Agent-to-Agent）协议支持 — 25评论 / 28👍
**[#514]** 讨论Google的A2A开放标准（Apache 2.0，Linux基金会）与MCP的互补关系：MCP回答"我能用哪些工具"，A2A回答"谁能帮我"。提议实现远程Agent发现、通信与互操作 [链接](https://github.com/NousResearch/hermes-agent/issues/514)

### 2. Token开销分析：73%的API调用为固定开销 — 20评论
**[#4379]** 用户 @Bichev 构建了监控仪表盘，分析6份会话转储后发现在Telegram+WhatsApp+Cron网关部署中，**每次API调用有73%（约13.9K tokens）是固定开销**。引发对token使用效率的广泛讨论 [链接](https://github.com/NousResearch/hermes-agent/issues/4379)

### 3. Ollama集成优化：原生 /api/chat 与 OpenAI兼容端点之争 — 15评论 / 4👍
**[#4505]** 提议使用Ollama原生端点的优势对比：真正的delta流式传输、更好的性能。涉及P2级，需决策 [链接](https://github.com/NousResearch/hermes-agent/issues/4505)

### 4. 插件生命周期事件目录与钩子分类 — 15评论
**[#64231]** 要求定义统一的钩子验收标准，并一次性批处理10多个待处理的 `VALID_HOOKS` 添加PR，避免各自为政或腐烂 [链接](https://github.com/NousResearch/hermes-agent/issues/64231)

### 5. xAI grok-4.5 'Invalid PNG image' 400会话永久损坏 — 13评论
**[#69078]** 网关会话因历史中包含原生视觉工具结果，对xAI的**所有**API调用（包括纯文本）持续报400错误，且重启无效，唯一恢复方法是删除会话 [链接](https://github.com/NousResearch/hermes-agent/issues/69078)

---

## Bug 与稳定性

### P1级

- **[#74836] [已修复]** macOS应用内更新被残留 `~/.hermes/hermes-setup` 永久破坏，`resolveUpdaterBinary()` 无版本门控 [链接](https://github.com/NousResearch/hermes-agent/issues/74836) — 对应修复已关闭
- **[#74531] [已修复]** macOS更新器死循环"另一个更新正在运行"，更新器自身不退出 [链接](https://github.com/NousResearch/hermes-agent/issues/74531) — 已关闭，标记为重复
- **[#74942] [已修复]** 更新器PID检查误判自身为其他实例 [链接](https://github.com/NousResearch/hermes-agent/issues/74942) — 已关闭
- **[#73298] [已修复]** 预检token估算按chars/4计数reasoning_details，导致压缩在真实用量27%即触发 [链接](https://github.com/NousResearch/hermes-agent/issues/73298) — 已关闭
- **[#37968] [开放]** Cron任务网关审批受环境污染，CVSS v3.1评分6.3 / v4.0评分7.0，需要隔离 [链接](https://github.com/NousResearch/hermes-agent/issues/37968)

### P2级

- **[#69078] [开放]** xAI grok-4.5 'Invalid PNG image' 400永久卡死会话，无恢复机制 [链接](https://github.com/NousResearch/hermes-agent/issues/69078)
- **[#69551] [已关闭]** 桌面SSH远程模式在非默认profile下token路径校验错位 [链接](https://github.com/NousResearch/hermes-agent/issues/69551)
- **[#75670] [开放]** TUI更新后node_modules完整性未校验导致启动失败 [链接](https://github.com/NousResearch/hermes-agent/issues/75670)
- **[#65274] [开放]** Windows桌面端项目级新会话回退到home目录cwd [链接](https://github.com/NousResearch/hermes-agent/issues/65274)
- **[#52010] [开放]** macOS桌面更新后文件全盘访问权限被撤销 [链接](https://github.com/NousResearch/hermes-agent/issues/52010)

### P3级

- **[#53819] [开放]** Kanban DB在高并发工作负载下因未序列化写入而损坏 [链接](https://github.com/NousResearch/hermes-agent/issues/53819)
- **[#2788] [开放]** Cron任务从不执行或失败时无日志信息 [链接](https://github.com/NousResearch/hermes-agent/issues/2788)
- **[#66616] [开放]** Skills索引过期（29.8h > 26h限制）导致文档站降级 [链接](https://github.com/NousResearch/hermes-agent/issues/66616)
- **[#49529] [开放]** PyPI 0.17.0 wheel安装存在venv入口点误报与可选技能缺失 [链接](https://github.com/NousResearch/hermes-agent/issues/49529)

---

## 功能请求与路线图信号

- **A2A协议支持**（#514，28👍）：开放标准互操作方向，可能与MCP形成互补生态，具有较高路线图优先级 [链接](https://github.com/NousResearch/hermes-agent/issues/514)
- **Mistral作为LLM提供商**（#20859，24👍）：用户基数大于部分已支持提供商，语音模型已集成，LLM接入难度估计不高 [链接](https://github.com/NousResearch/hermes-agent/issues/20859)
- **可配置推理温度**（#17565，13👍）：当前温度硬编码导致严重幻觉问题 [链接](https://github.com/NousResearch/hermes-agent/issues/17565)
- **delegate_task 支持按任务覆盖模型**（#5012/#18591）：已关闭#5012，但#18591标记为重复，说明已解决 [链接](https://github.com/NousResearch/hermes-agent/issues/18591)
- **MLX Whisper本地STT支持**（#3491）：Apple Silicon原生语音转文字，避免faster-whisper绕行 [链接](https://github.com/NousResearch/hermes-agent/issues/3491)
- **俄语本地化**（#40347、#52137）：v2翻译已完成99% UI字符串，并附PR [链接](https://github.com/NousResearch/hermes-agent/issues/40347) [链接](https://github.com/NousResearch/hermes-agent/issues/52137)
- **桌面端reasoning面板保持展开选项**（#53617）：当前自动折叠影响思考模型的体验 [链接](https://github.com/NousResearch/hermes-agent/issues/53617)
- **每个turn的provider请求预算**（PR #76458）：直接回应#4379的token开销讨论 [链接](https://github.com/NousResearch/hermes-agent/pull/76458)

---

## 用户反馈摘要

- **Token开销是真实痛点**：用户在 #4379 中通过数据指出大部分API调用成本为固定开销，呼吁优化系统提示和上下文管理；该讨论催生了 #76458 的预算控制提案 [链接](https://github.com/NousResearch/hermes-agent/issues/4379)
- **更新机制信任度受损**：macOS用户集中反映更新器连环故障（#74836、#74531、#74942、#52010），关闭窗口、权限撤销、死循环等问题叠加，影响用户对自动更新的信心
- **配置隔离性问题**：多profile场景下的全局

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目日报 — 2026-08-02

## 1. 今日速览

过去 24 小时项目保持高活跃度：发布新版本 v1.40.0，共 13 条 PR 更新（11 条待合并、2 条已关闭/合并），4 条 Issue 活跃（均为开放状态，无关闭）。最显著的进展是 v1.40.0 发布，其中包含一项关键安全修复（secrets 不再持久化到 workspace）；同时 Claude Opus 5 模型支持已通过 PR 修复并关闭。社区讨论集中在大模型治理（#4273）和智能模型选择（#3442）两个议题上，企业级功能诉求明显。整体看，项目在安全加固、模型兼容性和开发者体验三个方向均有实质推进，开发管线畅通。

## 2. 版本发布

### v1.40.0
- 发布时间：2026-08-01
- 发布 PR：[#4324](https://github.com/OpenHands/software-agent-sdk/pull/4324)
- 行为兼容性说明（Behavioral compatibility notes）：

  > **#3990** fix(agent-server): keep secrets out of workspace persistence — [@enyst](https://github.com/OpenHands/software-agent-sdk/pull/3990)

  该修复确保 agent-server 不再将 secrets（如 API 密钥）写入 workspace 持久化存储，属于安全加固类变更。对于依赖旧行为（从持久化中恢复 secrets）的用户，升级后需注意 secrets 需通过安全渠道重新注入。
- 其余变更：未发布明确的变更日志条目。
- 迁移注意事项：暂无已知破坏性变更；建议部署在共享/多租户环境的企业用户，升级后检查现有 workspace 持久化中是否残留历史 secrets 并予清理。

## 3. 项目进展

今日合并/关闭的 PR 共 2 条，实质性推进了以下方面：

- **[#4326](https://github.com/OpenHands/software-agent-sdk/pull/4326) fix(acp): surface Claude Opus 5 in Claude Code model picker**（已关闭/合并）
  修复 Agent Canvas 的 Claude Code 模型选择器仍显示 Opus 4.8 的问题，正式支持 2026-07-24 GA 的 Claude Opus 5。该修复保证了模型选择器与最新模型供应同步，避免用户手动配置。

- **[#4324](https://github.com/OpenHands/software-agent-sdk/pull/4324) Release v1.40.0**（已关闭/合并）
  v1.40.0 发布流程完成，携带上述安全修复（#3990）。

此外，11 条 PR 处于待合并状态，涵盖 **安全检测增强（#3944）、ruff 规则重构（#4281）、多个 bug 修复（#4163/#4164/#4166/#4168）、hooks.json 发现路径扩展（#4327）** 等，预示下一版本将集中落地一批正确性修复和功能改进。

## 4. 社区热点

今日讨论最活跃的议题是 **企业级治理能力**，其次是 **智能模型选择**：

- **[#4273 Governance layer for agent actions](https://github.com/OpenHands/software-agent-sdk/issues/4273)** — 12 条评论，热度最高
  由 @nagasatish007 提出，要求为 agent 行为增加治理层：文件访问控制、命令白名单、成本预算、结构化审计证据。适用场景明确指向企业共享开发基础设施、合规行业和多租户平台。12 条评论说明社区对其设计边界、实现路径有较大讨论空间。

- **[#3442 Intelligent Model Selection](https://github.com/OpenHands/software-agent-sdk/issues/3442)** — 9 条评论，👍 1
  虽被标记 Stale 但仍保有讨论热度。用户希望系统自动为任务路由到最佳模型，而非手动比较各模型的成本、性能与能力。背后诉求是降低普通用户使用多模型时的认知负担。

两个热门议题均指向同一信号：**OpenHands 正在从个人开发者工具走向企业级平台，社区对可治理性、自动化运维能力的需求在快速增长**。

## 5. Bug 与稳定性

今日活跃的 Bug 类 PR 共 5 条（均待合并），按严重程度排列如下：

| 严重程度 | 问题 | 修复 PR | 状态 |
|---|---|---|---|
| **高（安全）** | `/vscode/url` 端点接受未验证的 `workspace_dir` 参数，存在路径穿越/未授权访问风险（Medium 级别，文件 `vscode_router.py:L31`） | [#4282](https://github.com/OpenHands/software-agent-sdk/pull/4282) | 待合并 |
| **高（数据安全）** | `update_secrets` 仅原地修改 registry 而未持久化，导致 secrets（含构造函数注入的）在重启后丢失 | [#4166](https://github.com/OpenHands/software-agent-sdk/pull/4166) | 待合并 |
| **中（数据损坏）** | `file_editor` 在文件末行无换行符时执行 insert，新文本会粘贴到末行尾部，破坏原有末行内容 | [#4163](https://github.com/OpenHands/software-agent-sdk/pull/4163) | 待合并 |
| **中（功能失效）** | `grep` 的 include 过滤不识别 brace 展开（如 `*.{ts,tsx}`），导致该类型模式静默匹配不到任何文件 | [#4164](https://github.com/OpenHands/software-agent-sdk/pull/4164) | 待合并 |
| **中（请求被拒）** | Bedrock 联合预算裁剪逻辑只降低 `max_tokens` 而未同步裁剪 `thinking.budget_tokens`，导致请求被 provider 拒绝 | [#4168](https://github.com/OpenHands/software-agent-sdk/pull/4168) | 待合并 |

此外，v1.40.0 已合入 #3990 修复 secrets 持久化问题，与 #4166 形成互补（前者解决写入侧，后者解决更新侧）。上述修复若随下一版本合并，将显著提升文件编辑和搜索功能的稳定性。

## 6. 功能请求与路线图信号

- **[#4273 治理层（Governance layer）](https://github.com/OpenHands/software-agent-sdk/issues/4273)** — 新开 8 天，评论 12 条。这是当前社区呼声最高的功能请求，涵盖访问控制、命令白名单、成本预算与审计。结合项目近期多项安全 PR（#3944、#4282），治理/安全方向很可能进入优先路线图。

- **[#3442 智能模型选择](https://github.com/OpenHands/software-agent-sdk/issues/3442)** — 被标记 Stale，但评论仍有 9 条。需求真实存在，但因长期未获维护者响应而降温。若后续被纳入路线图，可能以"模型路由/推荐"模块形式出现。

- **[#4327 hooks.json 发现路径扩展到 .agents/](https://github.com/OpenHands/software-agent-sdk/pull/4327)** — 新 PR，将 hooks 配置位置从 `.openhands/hooks` 联合到 `.agents/hooks`，统一项目级扩展加载路径。该改动与现有 skills/plugins/subagents 的目录约定一致，属"一致性改进"，大概率会被合入。

- **[#3944 AST-backed shell 命令名解析](https://github.com/OpenHands/software-agent-sdk/pull/3944)** — 安全检测增强（#2721 Phase 2b），用 AST 解析替代正则匹配，封堵 shell 检测的三种绕过方式。属于既定

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目日报 — 2026-08-02

## 今日速览

过去 24 小时 LiteLLM 项目保持高强度迭代：共产生 39 条 Issue 更新（新开/活跃 32，关闭 7）与 177 条 PR 更新（待合并 124，合并/关闭 53），并发布 1 个 RC 版本。从 PR 流向看，PTU 计费、可观测性（OTEL/回调）、MCP 集成与 Rust 迁移四条线并行推进，团队内部提交占比极高显示出明确的版本节奏控制。Issue 侧以 MCP、花费追踪/计费和流式响应稳定性三类问题最为集中。整体健康度良好，但 124 条待合并 PR 的积压规模值得关注。

---

## 版本发布

### v1.95.0-rc.3
- **发布时间**：2026-08-02（RC 候选版）
- **核心内容**：延续 v1.95.0 系列，本次为第三个 RC 候选。重点强调所有 Docker 镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 签名，并可通过公开密钥验证完整性。
- **迁移注意事项**：RC 版本不保证 API 兼容性，生产环境建议等待正式版发布后再升级。近期主版本迭代频繁（v1.91+ 引入了 `aiohttp>=3.14.1` 约束，相关连接池问题见下文 Bug 区），升级时需特别关注依赖变更。

---

## 项目进展

### 今日已合并/关闭的重要 PR

| PR | 内容 | 意义 |
|---|---|---|
| [#35518](https://github.com/BerriAI/litellm/pull/35518) | 将 `pydantic-settings` 移入基础依赖 | 修复 `pip install litellm` 后直接 `import` 失败的严重问题 |
| [#35487](https://github.com/BerriAI/litellm/pull/35487) | 终端批次检索时注册托管文件 ID | 修复原始 `file-*` ID 绕过 `/v1/files` 所有权 ACL 的 IDOR 安全漏洞 |
| [#35504](https://github.com/BerriAI/litellm/pull/35504) | 移除 `classifier_tier_rubric` 覆写机制 | 简化复杂度路由配置，与上下文窗口特性解耦 |
| [#35500](https://github.com/BerriAI/litellm/pull/35500) | Admin UI 暴露 assistant-turn 分类器开关 | 使 #35471 新增的复杂度路由配置可在界面操作，不再仅限 YAML |
| [#35505](https://github.com/BerriAI/litellm/pull/35505) | 修复 `_delete_deployment` 测试断言 | 适配 #35400 的返回值变更，修复 staging 失败 |

### 当前推进中的关键方向（未合并 PR）

- **PTU 计费闭环**：`#35343`（每日按活跃小时摊分 PTU 固定成本）、`#35391`（读取路径汇总 PTU 固定成本）、`#35393`（UI 模型表单增加 PTU 配置项）三件套形成完整闭环，PTU 计费功能接近可用状态。
- **可观测性增强**：`#35514` 在认证时解析请求的 trace 目的地并携带在 server-only context 中；`#35516` 在 `/team/info` 和 `/organization/info` 中披露 `resolved_logging_exporters`。
- **团队回调修复**：`#35520` 修复 `disable_logging` 报成功但实际仍在记录的问题；`#35512` 修复 `GET /team/{team_id}/callback` 永远返回空列表的问题。
- **成本优化仪表盘**：`#35521`/`#35522` 在成本优化仪表盘中加入 auto-router 净节省统计，修正冷缓存场景下成本低估的问题。
- **Rust 迁移基建**：`#35519` 在 CI 中固定 Rust 工具链版本，消除依赖漂移带来的编译不确定性。

**综合评估**：今日合并的 PR 以修复为主（依赖、安全、测试、配置继承），而大规模功能增量（PTU、OTEL 目的地解析、UI 改进）正处于密集提交的待合并状态。项目健康度良好，安全修复（#35487）响应迅速。

---

## 社区热点

### 1. [Dark Mode 功能请求（#10177）](https://github.com/BerriAI/litellm/issues/10177) — 69 👍 / 60 评论
创建于 2025-04-20，至今已持续活跃 15 个月，今日仍有更新。作者原话 *"I'm going blind"* 引发大量共鸣，是 UI 体验类需求中呼声最高的一项，长期占据 Issue 热榜。**诉求分析**：Admin 面板的使用频率高、使用时间长，深色主题不仅是美观问题，更是可访问性诉求。

### 2. [LiteLLM Rust 迁移（#31263）](https://github.com/BerriAI/litellm/issues/31263) — 16 👍 / 17 评论
官方发起的父级追踪 Issue，目标是实现 sub-1ms 开销的 AI 网关。已发布博客并开放 Beta 测试者报名。**诉求分析**：社区对性能和资源占用有持续焦虑，Rust 迁移是 LiteLLM 面对企业级高并发场景的长期战略布局。

### 3. [Markov 决策过程路由策略（#31555）](https://github.com/BerriAI/litellm/issues/31555) — 0 👍 / 10 评论
提出基于马尔可夫决策过程的自适应 Token 成本套利路由策略。评论数高但点赞为 0，说明讨论热度存在但社区支持度尚不明确。**诉求分析**：大型用户对多供应商成本优化的诉求正在从静态规则走向动态决策。

---

## Bug 与稳定性

按严重程度排序：

### 严重（安全/数据完整性）

1. **[IDOR 漏洞：批处理文件 ID 泄漏（#35487，已修复）](https://github.com/BerriAI/litellm/pull/35487)**
   终端批次检索时泄漏原始 `file-*` ID，绕过 `/v1/files` 所有权 ACL，任意已认证 key 可读取其他用户的批处理文件。**已有 fix PR 并已合并。**

2. **[项目花费完全未追踪（#33871，OPEN）](https://github.com/BerriAI/litellm/issues/33871)**
   项目预算/软预算/预算时长虽已暴露且请求经过预算检查，但正常请求路径从不写项目级花费记录，导致项目预算和告警从不触发。**暂无 fix PR。**

3. **[disable_end_user_cost_tracking 不生效（#27038，OPEN）](https://github.com/BerriAI/litellm/issues/27038)**
   设置 `disable_end_user_cost_tracking: true` 后，`SpendLogs.end_user` 仍被填充，`DailyEndUserSpend` 表仍被写入。**暂无 fix PR。**

### 中等（功能失效/回归）

4. **[Azure 异步处理器吞掉 CancelledError（#35329，OPEN）](https://github.com/BerriAI/litellm/issues/35329)**
   `asyncio.CancelledError` 被捕获并转成 `AzureOpenAIError(500)`，导致客户端取消操作被误报为服务端错误，且 Router 回退逻辑会继续跑完。**暂无 fix PR。**

5. **[aiohttp 3.14.x 连接池中毒（#33820，已关闭）](https://github.com/BerriAI/litellm/issues/33820)**
   从 v1.91.0 起，`aiohttp>=3.14.1` 导致跨供应商出现间歇性 `Connection timed out`。该 issue 今日已关闭，推测已通过版本约束或依赖调整解决，建议关注具体修复版本。

6. **[SSRF 覆盖项删除后不重置（#35502，OPEN）](https://github.com/BerriAI/litellm/issues/35502)**
   从 DB 配置中移除 `user_url_allowed_hosts` 等 SSRF 键后，重启前仍生效——同步逻辑只应用 key 的增改、不处理删除。**暂无 fix PR。**

### 轻微（特定场景）

7. **[MCP 会话上限按 API key 分桶（#35383，OPEN）](https://github.com/BerriAI/litellm/issues/35383)** — 共享 key 下所有用户共用一个 100 并发会话上限，单个用户可能阻塞其他人。**暂无 fix PR。**

8. **[OpenAI 直通部署花费日志中 model 字段不一致（#35472，OPEN）](https://github.com/BerriAI/litellm/issues/35472)** — `openai/<upstream-model>` 直通部署中部分日志行丢失模型标识，导致按模型分组的花费视图不准确。**暂无 fix PR。**

---

## 功能请求与路线图信号

| 功能请求 | Issue/PR | 信号强度 | 判断依据 |
|---|---|---|---|
| **Dark Mode** | [#10177](https://github.com/BerriAI/litellm/issues/10177) | 强（69 👍） | 长期高赞未实现，但 UI 改进类 PR（#35523、#35522）近期持续增多，可能进入排期 |
| **Rust 迁移** | [#31263](https://github.com/BerriAI/litellm/issues/31263) | 强（官方立项） | 已有 Beta 报名表和博客，CI 基建（#35519）今日已开始落地 |
| **PTU 计费** | PR #35343/#35391/#35393 | 强（已在实现） | 今日 3 个 PR 并行推进，即将合入主干 |
| **OpenAI Workload Identity Federation** | [#31649](https://github.com/BerriAI/litellm/issues/31649) | 弱（已关闭/重复） | 被标记为 duplicate，可能已有替代实现 |
| **Markov 路由策略** | [#31555](https://github.com/BerriAI/litellm/issues/31555) | 中（讨论热、点赞少） | 10 条讨论但 0 赞，社区兴趣分化，短期进入路线图概率低 |
| **auto-router 成本可视化** | PR #35521/#35522 | 强（已在实现） | 与成本优化仪表盘直接相关，待合并 |

**路线图信号总结**：近期主线集中在 **成本可观测性**（PTU + auto-router 节省）和 **企业级可管理性**（OTEL 目的地披露、团队回调可编程化）两大方向。Rust 迁移是中长期结构性投资。

---

## 用户反馈摘要

从今日活跃的 Issue 评论中提炼的真实用户声音：

1. **新手引导不足**：[#35469](https://github.com/BerriAI/litellm/issues/35469) 用户按照教程在命令行输入 `litellm` 后遇到错误，「istellm not opening in command prompt」——教程与实际 CLI 行为不匹配，反映出官方文档/快速上手对新用户仍有摩擦。

2. **配置覆盖问题困扰老用户**：[#32736](https://github.com/BerriAI/litellm/issues/32736) 用户明确表示「Price-Reload overrides my explicit definitions in the Proxy-Config.model_list」，即价格自动刷新机制覆盖用户显式配置，需要更可控的优先级逻辑。

3. **流式响应可靠性是刚需**：[#27144](https://github.com/BerriAI/litellm/issues/27144) 使用 `gpt-5.3-codex-spark` 流式响应时，如果模型直接发出 `response.function_call_arguments.done` 而省略增量 delta，函数调用参数会完全丢失。这类边缘 case 直接影响生产环境的 agent 应用。

4. **MCP 集成问题集中爆发**：今日 4 个 MCP 相关 Issue（#353

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>

# Temporal 项目动态日报（2026-08-02）

## 1. 今日速览

过去 24 小时内，Temporal 仓库整体活跃度中等偏高：Issue 侧仅 1 条更新，且是历史 bug 被关闭，无新增 issue；PR 侧共 13 条动态，其中 7 条处于待合并状态，6 条关闭/合入。核心进展集中在 Standalone Activity 默认能力开启、S3 visibility 查询兼容、Worker API 限流归属调整，以及 1.32.0 发布分支准备。稳定性方面，一条 CI 大规模失败问题的根因已被定位到 `logger.Fatal` 误用。仓库暂无新版本发布，但 release 准备 PR 已出现，说明一个新版本正在路上。

## 3. 项目进展

从 PR 关闭/合入情况来看，项目在以下方向有明确推进：

- **Standalone Activity Start Delay 默认开启**  
  PR #11378 已关闭：`Enable standalone activity start delay by default`，并移除了不必要的测试覆盖。这是 standalone activity 向 GA 迈进的关键一步。  
  https://github.com/temporalio/temporal/pull/11378

- **S3 visibility 查询支持 WorkflowType**  
  PR #11383 已关闭：S3 visibility archiver 查询解析器开始接受 `WorkflowType`，同时保留 `WorkflowTypeName` 作为兼容别名，并统一为 `workflowType` 字段。改善了归档工作流查询的一致性和可用性。  
  https://github.com/temporalio/temporal/pull/11383

- **Worker API 限流归属调整**  
  PR #11366 已关闭：将 `ListWorkers`、`DescribeWorker`、`CountWorkers` 从 visibility 限流器迁移到通用 API 限流器，并统一为 P3 优先级，因为这些 API 实际由 matching 服务而非 visibility 服务提供。  
  https://github.com/temporalio/temporal/pull/11366

- **1.32.0 发布分支准备**  
  PR #11392 已关闭：由 CI bot 发起，用于覆盖 governance 文件并更新依赖，说明 1.32.0 发布流程已经启动。  
  https://github.com/temporalio/temporal/pull/11392

- **稳定性回滚**  
  PR #11387 已关闭：将导致 `TestNamespaceDeploymentsLimit` 在共享测试 namespace 下不稳定的 MaxDeployments 行为变更回滚，并重新禁用该 functional test，以恢复主干稳定性。  
  https://github.com/temporalio/temporal/pull/11387

整体来看，当前主干正在为 1.32.0 累积功能与稳定性改动，同时围绕 standalone activity、visibility 查询兼容性、API 治理三线并进。

## 4. 社区热点

今日评论最集中的是 Issue #7821：

- **#7821**：`[bug] workflow list takes different query for hot and archived`  
  该 issue 创建于 2025-05-28，持续到 2026-08-01 被关闭，共获得 2 条评论。核心诉求是：用户希望用同一条 `temporal workflow list -q 'WorkflowType = "MyWorkflowType"'` 查询热工作流和归档工作流，但归档查询需要额外加 `--arch...` 参数且语法不统一。  
  https://github.com/temporalio/temporal/issues/7821

虽然该 issue 已关闭，但背后反映的是 CLI 查询语义在 hot 与 archived 两条路径上不一致，容易让自动化脚本在跨状态复用查询条件时出错。

## 5. Bug 与稳定性

- **CI 大规模失败：`logger.Fatal` 导致测试进程退出**  
  PR #11390（WIP）针对 GitHub Actions 上的 `Functional test (cass_es, shard0)` 失败做了根因分析：`execSchemaVersionQuery` 中的 `logger.Fatal` 会直接终止测试二进制，进而引发 736+ 个级联失败；同时 `WorkflowTypeEncodingSuite` 为每个 subtest 创建一个 `NewEnv`，导致集群 lease 压力上升。该 WIP PR 已关闭，修复项并未完整完成，因此应视为调查结论而非最终修复。  
  https://github.com/temporalio/temporal/pull/11390

- **回归修复：CHASM 与 HSM 路由行为**  
  PR #11381 待合并：将 `cherryPickHSMEvent` 对 `hsm.ErrStateMachineNotFound` 的处理恢复为可跳过，避免事件被错误路由到 CHASM 树。这是一行行为变更，用于修复 #10986 引入的回归。  
  https://github.com/temporalio/temporal/pull/11381

- **matching GC 潜在 flaky 测试**  
  PR #11389 待合并：作者在无关 PR 的测试中注意到 GC 与 ack 竞态问题，且坦言“改动太深，不打算轻易碰逻辑”，可能选择

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*