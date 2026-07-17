# AI CLI 工具社区动态日报 2026-07-18

> 生成时间: 2026-07-17 23:11 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-07-18）

## 1. 生态全景

当前AI CLI工具整体处于**功能快速迭代与稳定性博弈**的关键阶段。一方面，各工具持续发布新版本（Claude Code v2.1.212、Codex Rust SDK 三个alpha、Copilot CLI v1.0.72-1、Qwen Code nightly），核心能力逐渐分化：会话管理、多代理协作、MCP协议集成成为标配。另一方面，社区反馈暴露了大量**基础设施层面的缺陷**——安全分类器误报、子代理无限循环、Windows兼容性崩溃、MCP连接故障——这些问题的频发使得开发者对工具的信任度产生波动。**“可用性”正在取代“功能丰富度”，成为当前社区最关注的维度。**

## 2. 各工具活跃度对比

| 工具 | 热议Issues数 | 重要PR数 | 版本发布 | 社区活跃度评估 |
|------|-------------|---------|---------|--------------|
| Claude Code | 10（精选） | 10（精选） | v2.1.212 | ★★★★★ 极高，讨论深入，抱怨集中 |
| OpenAI Codex | 10（精选） | 10 | 3个Rust SDK alpha | ★★★★★ 极高，LSP集成获425赞 |
| Gemini CLI | 10 | 10（含合并） | 无 | ★★★★☆ 高，P1级Bug密集修复 |
| GitHub Copilot CLI | 10 | 0 | v1.0.72-1 | ★★★☆☆ 中，问题多但修复慢 |
| OpenCode | 10 | 10 | 无 | ★★★★☆ 高，功能需求强烈 |
| Qwen Code | 10 | 10 | v0.19.11-nightly | ★★★★☆ 高，多工作区讨论持续 |
| Kimi Code | 4 | 0 | 无 | ★★☆☆☆ 低，社区氛围冷清 |

**说明**：Issues/PR数为各日报中精选的热点数量，非当日全部总量，但能反映社区聚焦的广度与深度。

## 3. 共同关注的功能方向

以下需求横跨多个工具，表明行业级痛点：

| 方向 | 涉及工具 | 具体诉求 |
|------|---------|----------|
| **安全策略可控性** | Claude Code、Gemini CLI、Copilot CLI | Claude Code 的 Fable 5 误报率极高（甚至对“hello”触发降级），社区强烈要求用户可配置/关闭；Gemini 修复变量注入绕过；Copilot 计划模式错误拦截只读命令、危险命令无权限检查 |
| **模型切换与回退** | Claude Code、Kimi Code、OpenCode | Claude Code 因安全审查强制降级到 Opus 4.8；Kimi Code 用户要求切回 K2.5 以避免 K2.6 思维链过重；OpenCode 社区要求自动发现 OpenAI-compatible 模型 |
| **会话持久化与断线重连** | Claude Code、Copilot CLI、OpenCode、Gemini CLI | Claude Code SSH 断线后进程终止（获29赞）；Copilot 附件过大导致会话永久卡死；OpenCode 桌面版需要 SSH 远程连接；Gemini 子代理恢复后状态丢失 |
| **MCP 协议稳定性** | Claude Code、Qwen Code、Gemini CLI | Claude Code 的 Streamable-HTTP 连接器报“不可用”；Qwen Code 链式 MCP 调用静默失败；Gemini 将 MCP 连接集中化管理以提高可靠性 |
| **Windows 平台兼容性** | 几乎全部 | Claude Code 屏幕闪烁；Copilot 插件安装权限拒绝、交互模式变白；Kimi Code install.ps1 在 PS 5.1 崩溃；Qwen Code Docker 沙箱 cwd 无效；OpenCode WSL 路径损坏 |
| **子代理 / 多代理可靠性** | Claude Code、Gemini CLI、Copilot CLI、Qwen Code | 代理复制导致双倍Token消耗、无限循环、消息队列丢失、最大轮次误报成功等 |

## 4. 差异化定位分析

| 工具 | 核心优势 / 技术路线 | 目标用户 | 独特短板 |
|------|-------------------|---------|---------|
| **Claude Code** | 会话管理创新（`/fork`、`/subtask`）、多代理协作、安全审查强介入 | 企业级开发者、需要严格合规的团队 | Fable 5 过度防御引发大量信任危机 |
| **OpenAI Codex** | Rust SDK Alpha 密集迭代、LSP 集成呼声最高、与 OpenAI 生态深度绑定 | 追求最新模型与 API 能力的开发者 | Windows 性能问题严重（15秒挂起循环）、速率限制显示混乱 |
| **Gemini CLI** | 自动 PR 生成管道、AST 感知工具探索、macOS 安全策略加固 | 内部工具链重度用户、需要自定义 agent 能力 | 通用 agent 无限挂起、shell 命令卡死、Wayland 兼容性差 |
| **GitHub Copilot CLI** | 与 GitHub 生态无缝集成、语音模式、插件系统扩展 | 日常使用 GitHub 的开发者 | 插件安装全平台权限问题、计划模式误判、Telemetry 缺失 |
| **Kimi Code** | 强调多模态（K2.6 思维链）、Wind 插件针对金融量化 | 中文开发者、特定行业（金融） | 模型切换不可逆、内网依赖暴露、社区极小 |
| **OpenCode** | opencode2 (next) 版本激进重构、自动模型发现、SSH 远程连接 | 希望高度自定义和本地化的开发者 | 新版兼容性问题（模型不可用、插件崩溃）、数据库升级报错 |
| **Qwen Code** | 多工作区守护进程、Web Shell 增强（Git 状态芯片）、多模态路由 | 需要远程/多工作区管理的 DevOps 用户 | Windows Docker 沙箱故障、CI 频繁失败 |

## 5. 社区热度与成熟度

- **最活跃 / 成熟度较高（社区规模大、讨论深入）：**  
  **Claude Code** 与 **OpenAI Codex** 是当前最热的两极，前者因安全策略争议而话题度高，后者因 LSP 集成和版本发布节奏而吸引大量反馈。两者均积累了成规模的吐槽与功能建议，表明用户基数大、使用频率高。

- **快速迭代 / 技术探索期：**  
  **Gemini CLI** 和 **Qwen Code** 处于“高修复、高功能产出”阶段，P1 级 Bug 与重要 PR 密集合并，社区参与度中等但质量较高。**OpenCode** 则在 next 版本上激进重构，兼容性阵痛明显，但功能需求方向明确。

- **发展较慢 / 社区规模小：**  
  **Kimi Code** 仅 4 个活跃 Issue 且无 PR，更新停滞，模型切换诉求三个月未解决，社区活跃度远低于其他工具。**Copilot CLI** 虽然背靠 GitHub 生态，但过去 24 小时无 PR 更新，且核心功能（语音、插件）存在阻塞级问题，修复速度低于预期。

## 6. 值得关注的趋势信号

### (1) 安全与信任成为第一优先级
Claude Code 的 Fable 5 误报事件暴露了“AI 安全对 AI 开发工具的反噬”——过度防御导致开发者无法正常工作，且申诉闭环失效（人工介入为零）。这传递出一个重要信号：**安全策略必须可解释、可配置、可绕过**，否则将严重损害用户信任。Gemini 和 Copilot 也在同步修补安全漏洞，行业正在探索“安全与效率的平衡点”。

### (2) 模型切换灵活性是刚需
用户不再被动接受“最新即最好”。Kimi Code 用户要求回退 K2.5，Claude Code 用户对强制降级 Opus 4.8 不满，OpenCode 社区希望自动发现所有可用模型。这说明**模型质量并非单调递增**，开发者需要根据任务特性选择模型（如创造类 vs 精确类），工具应提供“模型超市”而非“单一推送”。

### (3) Windows 平台仍是第二等公民
几乎所有工具在 Windows 上都出现了从性能到兼容性的严重问题：CPU 占用、进程挂起、权限拒绝、渲染异常。对于企业开发者（尤其是 Windows 用户占多数的组织），这些痛点足以成为选型否决因素。**跨平台一致性将成为 AI 工具下一轮竞争的关键胜负手。**

### (4) 子代理/多代理系统的可靠性亟待提升
无限循环、消息重复、中断误报、资源泄漏——这些在多工具中反复出现。多代理协作是当前 AI 工具的核心卖点，但基础设施的脆弱性让“自动化”变成“事故多发区”。社区反馈表明，**用户宁愿功能少一点，也要稳定多一点**。

### (5) 远程开发与持久化连接需求爆发
SSH 断线重连（Claude Code、Copilot）、桌面版远程连接（OpenCode）、会话恢复（Gemini）——随着更多开发者将 AI 工具用于后台或远端服务器，**会话持久化**正在从“nice-to-have”升级为“must-have”。这同时也意味着对 Token 消耗、上下文管理的更高要求。

---

**总结**：2026 年中期的 AI CLI 工具生态，正从“功能堆叠”转向“稳定信任”阶段。安全策略、模型选择、跨平台兼容、多代理可靠性是当前最紧迫的“基础设施债”。后发工具（如 Qwen Code、OpenCode）通过差异化定位（多工作区、SSH、自动发现）获得增长机会，但若无法快速解决基础稳定性问题，将在与 Claude Code、Codex 的竞争中掉队。对于开发者而言，选型时应优先考察工具的**安全可控性、平台覆盖度、子代理稳定性**，而非单一功能亮点。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（截至 2026‑07‑18）

---

## 1. 热门 Skills 排行

以下 PR 按社区讨论热度（评论数）排列，涵盖新技能与关键修复。

### ① `skill-creator` 评估系统修复（#1298）
- **功能**：修复 `run_eval.py` 始终报告 `recall=0%` 的核心 bug，包括 Windows 流读取、触发检测、并行 worker 等问题。
- **讨论热点**：社区长期受困于技能优化循环“对噪声优化”，该 PR 是多份独立报告（#556 等）的汇集解决方案，评论密度极高。
- **状态**：🔴 Open  
  https://github.com/anthropics/skills/pull/1298

### ② 文档排版技能 `document-typography`（#514）
- **功能**：防止 AI 生成文档中的孤字换行、寡妇段落、编号错位等常见排版问题。
- **讨论热点**：用户认为此类问题影响所有文档生成，属于高频刚需；评审关注技能描述的通用性与触发准确性。
- **状态**：🔴 Open  
  https://github.com/anthropics/skills/pull/514

### ③ ODT 文档技能（#486）
- **功能**：支持创建、填充、读取及转换 ODF 格式文件（.odt/.ods），包括模板填充与转 HTML。
- **讨论热点**：LibreOffice 用户群强烈需求；社区讨论集中在如何与已有 DOCX 技能协同、模板引擎选择。
- **状态**：🔴 Open  
  https://github.com/anthropics/skills/pull/486

### ④ 前端设计技能改进（#210）
- **功能**：重写 `frontend-design` 技能的描述与指令，使其更清晰、可执行，避免歧义。
- **讨论热点**：原有技能“像开发者文档而非操作指令”，社区对技能写法的“实用性”标准争论激烈。
- **状态**：🔴 Open  
  https://github.com/anthropics/skills/pull/210

### ⑤ 元技能：质量分析器 & 安全分析器（#83）
- **功能**：新增两个 meta skill——从结构、安全、合规等维度评估 Claude Skills 质量。
- **讨论热点**：社区对技能质量缺乏客观度量表示欢迎；同时担忧安全分析器可能越权访问敏感信息。
- **状态**：🔴 Open  
  https://github.com/anthropics/skills/pull/83

### ⑥ Pyxel 复古游戏开发技能（#525）
- **功能**：集成 `pyxel-mcp` MCP 服务器，支持像素/8-bit 游戏开发循环（写→运行→截图→迭代）。
- **讨论热点**：创意编码社区活跃，作者 @kitao 是 Pyxel 引擎原开发者，PR 关注度持续增长。
- **状态**：🔴 Open  
  https://github.com/anthropics/skills/pull/525

### ⑦ 测试模式技能 `testing-patterns`（#723）
- **功能**：覆盖单元测试、React 组件测试、E2E 测试等全栈模式，强调“测试奖杯”理念与抗反模式。
- **讨论热点**：测试是 AI 辅助开发的核心场景，社区期待官方提供权威测试指南而非零散社区方案。
- **状态**：🔴 Open  
  https://github.com/anthropics/skills/pull/723

### ⑧ 自我审计技能 `self-audit`（#1367）
- **功能**：在 AI 输出交付前进行机械文件验证 + 四维推理质量门（按严重性排序）。
- **讨论热点**：社区对“输出质量可验证”有强烈需求，部分用户质疑审计步骤对上下文预算的影响。
- **状态**：🔴 Open  
  https://github.com/anthropics/skills/pull/1367

---

## 2. 社区需求趋势

从 Issues 热帖提炼的 5 大方向：

| 方向 | 代表性 Issue | 核心诉求 |
|------|-------------|---------|
| **技能创建工具链稳定性** | #556（recall=0%）、#1169、#1061（Windows 兼容） | 修复 `run_eval.py` 和 `run_loop.py` 的跨平台触发检测、编码、子进程问题；改善 `skill-creator` 文档与最佳实践（#202） |
| **组织级技能共享与分发** | #228 | 支持在组织内直接共享 `.skill` 文件或创建共享库，避免手动 Slack/上传 |
| **技能安全与信任边界** | #492 | 社区技能冒充官方技能的风险，要求 Anthropic 引入签名或认证机制 |
| **新领域技能需求** | #1329（compact-memory）、#412（agent-governance）、#16（MCP 暴露）、#1385（推理质量门） | 长期会话记忆优化、代理安全管控、MCP 协议暴露、输出质量审计 |
| **平台兼容性** | #29（Bedrock）、#184（agentskills.io 重定向） | 支持 AWS Bedrock 等非 Claude 客户端运行 Skills；修复官方参考站点可靠性 |

---

## 3. 高潜力待合并 Skills

以下 PR 讨论活跃且尚未合并，因解决社区核心痛点或填补新领域空白，预计近期可能落地：

| PR | 名称 | 关键价值 | 当前状态 | 链接 |
|----|------|---------|---------|------|
| #1298 | skill-creator: fix run_eval recall=0% | 直接影响所有技能优化效果，社区多次复现 | 🔴 Open | [链接](https://github.com/anthropics/skills/pull/1298) |
| #514 | document-typography | 解决高频文档排版问题，官方文档类技能空白 | 🔴 Open | [链接](https://github.com/anthropics/skills/pull/514) |
| #486 | ODT 技能 | 填补 LibreOffice/ODF 生态缺失，需求明确 | 🔴 Open | [链接](https://github.com/anthropics/skills/pull/486) |
| #723 | testing-patterns | 全栈测试指南，社区期待官方标准 | 🔴 Open | [链接](https://github.com/anthropics/skills/pull/723) |
| #83 | skill-quality-analyzer | 技能质量度量可推动生态健康发展 | 🔴 Open | [链接](https://github.com/anthropics/skills/pull/83) |
| #1367 | self-audit (推理质量门) | 输出质量保障，适配多种项目与模型 | 🔴 Open | [链接](https://github.com/anthropics/skills/pull/1367) |
| #525 | pyxel 游戏开发 | 创意编码社区标杆，作者为官方维护者 | 🔴 Open | [链接](https://github.com/anthropics/skills/pull/525) |

> 注：多个 `skill-creator` 修复 PR（#539、#1050、#1099、#362、#361）也受广泛关注，但因功能重叠，合并时可能优先整合。

---

## 4. Skills 生态洞察

**当前社区最集中的诉求是：稳定且跨平台兼容的技能创建与评估工具链，同时期待官方提供可信分发渠道、新领域技能（文档/测试/游戏）及输出质量保障机制。**  

整体而言，社区已从“尝试构建单个技能”转向“使技能生态可规模化、可信任、可度量”，`run_eval` 相关 bug 的持续高关注度正是这一转变的集中体现。

---

# Claude Code 社区动态日报 | 2026-07-18

## 📌 今日速览

Claude Code 昨日发布 v2.1.212 版本，核心更新了 `/fork` 与 `/subtask` 命令，会话管理更加灵活。社区最集中的反馈围绕 **Fable 5 安全分类器误报** 与 **MCP 连接兼容性**问题，多起 Issue 指向“安全审查违规”“模型无故降级到 Opus 4.8”等高频场景，开发者对安全策略的过度响应表达了强烈不满。另有多个 PR 聚焦插件安全加固和 Terraform 集成范例修复。

---

## 🚀 版本发布：v2.1.212

- **`/fork` 命令重构**：不再启动会话内子代理，而是将当前对话复制进一个新的**后台会话**（在 `claude agents` 中显示为单独一行），原有 `/fork` 的子代理行为已转移至 `/subtask` 命令
- **`claude auto-mode reset` 命令**：新增重置自动模式配置至默认状态的命令，执行前会要求确认

---

## 🔥 社区热点 Issues（10条精选）

1. **#78193 | MCP Streamable-HTTP 连接器触发“客户端服务器能力不可用”致命提示**
   - 作者：@realstephenreed-commits | 评论：10 | 👍：4
   - 描述：启用远程 Streamable-HTTP MCP 连接器（如 Atlassian 远程连接器）时，频繁出现 `Client server capabilities not available` 的 toast 提示，问题定位在客户传输层而非服务端
   - [查看详情](https://github.com/anthropics/claude-code/issues/78193)

2. **#49790 | 建议：Claude Desktop SSH 远程会话应支持断线重连/恢复**
   - 作者：@pwh9882 | 评论：8 | 👍：29
   - 描述：当 SSH 远程客户端断开（主动退出、网络断线、合盖），远程服务器上的 Claude Code 进程随之终止，无法断线重连恢复会话。该需求获得社区极高支持
   - [查看详情](https://github.com/anthropics/claude-code/issues/49790)

3. **#56805 | 桌面应用：Windows 屏幕闪烁与鼠标延迟**
   - 作者：@sigma4x | 评论：9 | 👍：0
   - 描述：Claude Desktop App 在 Windows 平台持续出现屏幕闪烁和鼠标延迟问题，已关闭但讨论热度未减
   - [查看详情](https://github.com/anthropics/claude-code/issues/56805)

4. **#78688 | Fable 5 → Opus 4.8 的中途切换导致后台代理重复生成（双倍 Token 消耗）**
   - 作者：@Sahil170595 | 评论：1 | 👍：0
   - 描述：Fable 5 安全分类器误报后强制切换到 Opus 4.8 时，不会感知已在运行的代理，导致**重新生成重复代理**，造成双倍 Token 消耗
   - [查看详情](https://github.com/anthropics/claude-code/issues/78688)

5. **#66657 | Fable 5 安全分类器对“hello”触发 model_refusal_fallback——误判的是静态请求头部，而非用户消息**
   - 作者：@famulare | 评论：5 | 👍：2
   - 描述：在第一轮对话中，哪怕仅输入 `hello`，Fable 5 都会因静态请求 preamble 而误触发安全回退至 Opus 4.8
   - [查看详情](https://github.com/anthropics/claude-code/issues/66657)

6. **#66595 | 安全审查中 Fable 5 自动切换至 Opus，干扰已授权的安全测试**
   - 作者：@sin99xx | 评论：3 | 👍：0
   - 描述：在合法、已授权范围内的安全测试过程中，Fable 5 安全分类器仍进行错误的模型切换，影响正常安全审计工作流
   - [查看详情](https://github.com/anthropics/claude-code/issues/66595)

7. **#78663 | 安全审查管道全天崩溃全记录：5次误报+申诉被拒+自动回复无人工干预**
   - 作者：@2tbmz9y2xt-lang | 评论：1 | 👍：0
   - 描述：该用户详细记录了自己在一天内遇到的完整安全管道失败闭环：5 次自主代码审查被误报拒绝、申诉文案被安全策略判定为违规、最终提交到 `usersafety@` 邮箱后只收到 5 轮自动回复（零人工介入），暴露安全策略的“反馈闭环失效”
   - [查看详情](https://github.com/anthropics/claude-code/issues/78663)

8. **#72174 | Windows TUI 显示异常：`├─── ✂ ─── 1 lines hidden ─────────────────────┤`**
   - 作者：@fschwiet | 评论：2 | 👍：3
   - 描述：Windows 终端界面中，行隐藏标记出现渲染异常，虽不影响核心功能但降低了可读性
   - [查看详情](https://github.com/anthropics/claude-code/issues/72174)

9. **#78338 | 后台代理丢失已排队的 SendMessages 并跳过完成通知**
   - 作者：@kerneltoast | 评论：1 | 👍：0
   - 描述：Linux 平台上后台 Agent 丢失已排队的消息，且不发送完成通知，该 bug 是在分析自身受影响的会话时由 Claude（Fable 5）自行发现并报告的
   - [查看详情](https://github.com/anthropics/claude-code/issues/78338)

10. **#78070 | AskUserQuestion 预览截断且无法展开**
    - 作者：@kustrun | 评论：1 | 👍：0
    - 描述：当模型调用 `AskUserQuestion` 工具并附带多行预览内容时，右侧预览框高度不足导致内容截断，仅显示 `N lines hidden` 却无法展开或滚动查看，影响用户对选项的判断
    - [查看详情](https://github.com/anthropics/claude-code/issues/78070)

---

## 🔧 重要 PR 进展（10条精选）

1. **#78532 | GCP Terraform 示例：可选内部 ALB + PG16 Cloud SQL 版本兼容修复**
   - 作者：@gabrielparanthoen-cmd
   - 摘要：修复新部署 PG16 实例时因默认 `ENTERPRISE_PLUS` Edition 拒绝共享核心规格而失败的问题；同时加入可选的内部 ALB 支持
   - [查看详情](https://github.com/anthropics/claude-code/pull/78532)

2. **#76581 | 插件脚本安全加固：YAML 注入、路径遍历与符号链接保护**
   - 作者：@1837620622
   - 摘要：修复官方插件脚本中 YAML frontmatter 逃逸、路径穿越及基于符号链接的凭据覆盖风险
   - [查看详情](https://github.com/anthropics/claude-code/pull/76581)

3. **#78446 | 修复 plugin-dev 缺少 `.claude-plugin/plugin.json` 清单**
   - 作者：@Atishyy27
   - 摘要：`plugins/plugin-dev/` 是仓库中唯一缺少 manifest 的插件目录，补全以保持一致性
   - [查看详情](https://github.com/anthropics/claude-code/pull/78446)

4. **#78445 | 文档修正：插件描述和版本与实际行为不一致**
   - 作者：@Atishyy27
   - 摘要：发现三处插件索引 / marketplace 元数据与插件实际功能矛盾，逐一对照源码修正
   - [查看详情](https://github.com/anthropics/claude-code/pull/78445)

5. **#78441 | DevContainer 脚本修复：通过 $LASTEXITCODE 检测原生命令失败**
   - 作者：@Atishyy27
   - 摘要：PowerShell 脚本中 `try/catch` 无法捕获原生命令（`docker`/`podman`/`devcontainer`）的非零退出码，改用 `$LASTEXITCODE` 判断正确
   - [查看详情](https://github.com/anthropics/claude-code/pull/78441)

6. **#78425 | 代码审查插件：禁止模型/子代理自动触发 review**
   - 作者：@ZaunEkko
   - 摘要：明确将 `/code-review` 标记为手动调用，阻止模型和子代理以编程方式重新进入多代理审查工作流
   - [查看详情](https://github.com/anthropics/claude-code/pull/78425)

7. **#77427 | PR Review Toolkit：将 code-reviewer 限制为 Leaf Agent**
   - 作者：@ZaunEkko
   - 摘要：限制 `pr-review-toolkit` 的代码审查器只能使用仓库检查工具，禁止其调用额外代理或审查工作流，防止 Agent 无限递归
   - [查看详情](https://github.com/anthropics/claude-code/pull/77427)

8. **#78371 | ralph-wiggum 插件安全加固：限制迭代、防止自动推送/发布**
   - 作者：@kazukinakai
   - 摘要：为 ralph-wiggum 循环插件添加安全防护——限制迭代次数、防止无人值守时自动推送/合并/发布，保留本地实验可用性
   - [查看详情](https://github.com/anthropics/claude-code/pull/78371)

---

## 🧠 功能需求趋势

从过去 24 小时更新的 Issues 中提炼出 5 大社区关注方向：

1. **会话持久化与恢复**（#49790、#66666）
   - SSH 远程会话断线重连 / 恢复是当前呼声最高的功能需求（👍29 支持），同样包括 `--remote-control` 模式下模型选择不能继承的问题

2. **Fable 5 安全分类器智能性**（#66657、#66595、#78688、#78663、#66668 等多条）
   - 连续提交的 Issue 显示 Fable 5 误报率极高，甚至对 `hello`、合法的安全审查、开源项目中的 CSRF/HMAC 防护代码都进行拦截，社区强烈要求降低误报率、允许用户主动配置或关闭

3. **MCP 协议兼容性与稳定性**（#78193）
   - Streamable-HTTP MCP 连接器的兼容性问题是当前技术层面的关键瓶颈

4. **TUI/终端用户体验改进**（#72174、#78070、#66689）
   - Windows 终端渲染问题、预览内容截断无法展开、“Thinking”文本颜色渲染异常

5. **VSCode IDE 集成与 Windows 平台兼容性**（#60045、#56805、#72174）
   - VSCode 扩展首次启动超时、Windows 全局渲染问题持续存在

6. **资源与成本管理优化**（#78688、#66698）
   - 代理复制、无效 API 调用导致的 Token 浪费引发开发者对成本控制的担忧

---

## 💡 开发者关注点（痛点 / 高频需求）

1. **⚠️ Fable 5 安全策略“过度防御”已成社区最大痛点**：大量 Issue 反映 Fable 5 对合法代码安全审查、渗透测试、个人项目进行误报拦截，强制降级到旧模型 Opus 4.8，且用户无法自主关闭此机制

2. **⚠️ 安全管道的“反馈闭环缺失”**（#78663）：用户在安全审查被拒后的申诉过程几乎“无路可走”——申诉文案本身可能被判定违规、`usersafety@` 只返回自动回复，完全没有人工介入机制

3. **⚠️ 代理复制与消息丢失**（#78688、#78338）：Fable 5 模型切换时生成重复代理导致 Token 浪费，后台 Agent 存在消息队列丢失、完成通知不发送等影响工作流可靠性的问题

4. **⚠️ MCP 连接、远程会话等基础设施稳定性**：Streamable-HTTP 协议兼容性（405 错误）、SSH 会话无法断线恢复、DevContainer 脚本中命令退出码判断错误等问题直接影响日常开发流水线

5. **⚠️ 选择器/预览/渲染等小处体验仍需打磨**：`AskUserQuestion` 预览截断、Windows 终端行隐藏显示异常、TTY 缓冲不足等虽非致命 bug，但高频场景下对开发者体验的累积影响不容小觑

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

好的，作为专注于 AI 开发工具的技术分析师，我已根据您提供的 GitHub 数据，为您生成了 2026 年 7 月 18 日的 OpenAI Codex 社区动态日报。

---

# OpenAI Codex 社区动态日报 | 2026-07-18

## 今日速览

今日 Codex 项目发布节奏密集，连续推出了三个 Rust SDK 的 Alpha 版本，但核心社区的焦点集中在 **Windows 桌面应用的严重性能问题** 和 **应用挂起** 上。与此同时，**LSP 集成** 和 **速率限制显示异常** 成为社区呼声最高的两个议题。

## 版本发布

昨日共发布 3 个版本，均为 Rust SDK 的 Alpha 迭代：
- **rust-v0.145.0-alpha.20**: 2026-07-17 发布
- **rust-v0.145.0-alpha.22**: 2026-07-18 发布
- **rust-v0.145.0-alpha.23**: 2026-07-18 发布
> 官方未提供详细更新日志，主要涉及 Rust SDK 的持续迭代。

## 社区热点 Issues

1.  **LSP 集成需求高企** [#8745](https://github.com/openai/codex/issues/8745)
    - **重要性**: 社区最热议题，获得了 425 个 👍 和 58 条评论。用户强烈希望在 Codex CLI 中内置语言服务器协议（LSP）支持，实现自动检测和安装，利用诊断和符号智能生成更精准的代码。
    - **社区反应**: 广泛支持，是当前社区最渴望的功能增强之一。

2.  **Windows 桌面应用性能与进程问题** [#33884](https://github.com/openai/codex/issues/33884)
    - **重要性**: 新报告的严重问题，描述 Codex 在 Windows 上进入周期性约 15 秒挂起、约 10 秒响应的循环，严重影响使用。
    - **社区反应**: 问题刚提出即获得 3 条评论，表明用户对 Windows 平台稳定性的关注度极高。

3.  **Windows 应用启动后“无响应”** [#33780](https://github.com/openai/codex/issues/33780)
    - **重要性**: 核心 Bug，应用启动时因 HID 设备枚举阻塞导致主进程挂起。这表明了应用启动流程中的底层兼容性问题。
    - **社区反应**: 已有 18 条评论，开发者正在积极排查。

4.  **Linux 用户被排除在计费重置机制外** [#27915](https://github.com/openai/codex/issues/27915)
    - **重要性**: 虽然已关闭，但获得了 41 个 👍 和 17 条评论。问题指出新的速率限制重置机制仅限桌面应用用户使用，导致 Linux CLI 用户无法享受此权益。
    - **社区反应**: 引发了关于平台公平性的大讨论，最终问题虽然关闭，但核心矛盾未完全解决。

5.  **Windows 应用缺失“控制其他设备”功能** [#28919](https://github.com/openai/codex/issues/28919)
    - **重要性**: Codex 的远程控制功能在 Windows 平台上缺失关键设置入口，影响了跨设备协作体验。
    - **社区反应**: 16 条评论，23 个 👍，表明远程控制是重要功能。

6.  **Plus 账号“5 小时”速率限制显示消失** [#32791](https://github.com/openai/codex/issues/32791)
    - **重要性**: 多位用户报告 Plus 订阅下，原有的 5 小时用量限制消失，仅显示周限制，引发了关于计费策略变更的担忧。
    - **社区反应**: 多起类似报告，如 #32707、#32635、#32840，形成一个话题集群，正在影响用户信心。

7.  **应用内浏览器插件启动失败** [#25247](https://github.com/openai/codex/issues/25247)
    - **重要性**: 桌面应用内置浏览器自动化功能在启动时因安全信任问题失败，阻碍了依赖该功能的工作流。
    - **社区反应**: 14 条评论，开发者已在跟踪。

8.  **CLI 子代理选择器无交互能力** [#30813](https://github.com/openai/codex/issues/30813)
    - **重要性**: TUI 中 `/agent` 命令能列出子代理，但无法选择或切换，这是一个影响多代理工作流的明显可用性缺陷。
    - **社区反应**: 13 条评论，6 个 👍，反馈集中于操作便利性。

9.  **Windows 应用启动触发高 CPU 占用** [#29499](https://github.com/openai/codex/issues/29499)
    - **重要性**: 与 #33875 类似，启动 Codex 后 WMI Provider Host 占用大量 CPU。这是一个反复出现的性能痛点。
    - **社区反应**: 该问题与 #33875、#32562 等共同构成了 Windows 平台性能问题的“热区”。

10. **RTL/LTR 双向文本渲染错误** [#26250](https://github.com/openai/codex/issues/26250)
    - **重要性**: 涉及国际化/本地化基础能力，对于阿拉伯语等 RTL 语言的用户至关重要。
    - **社区反应**: 9 条评论，对使用混合文本的开发者有直接影响。

## 重要 PR 进展

1.  **TUI 选择器支持路径代理** [#33922](https://github.com/openai/codex/pull/33922)
    - **内容**: 修复了 TUI 代理选择器无法选择路径代理的问题，提升了多代理管理的可用性。

2.  **允许稳定版 Python SDK 发布** [#33919](https://github.com/openai/codex/pull/33919)
    - **内容**: 修正了发布工作流，使其支持稳定版标签，为 Python SDK 的正式版发布扫清障碍。

3.  **允许通过共享更新发布插件** [#33908](https://github.com/openai/codex/pull/33908)
    - **内容**: 新增 `LISTED` 状态，允许插件作者通过共享更新机制公开发布插件，简化了分发流程。

4.  **分页线程的搜索功能** [#33907](https://github.com/openai/codex/pull/33907)
    - **内容**: 新增 `thread/searchOccurrences` 方法，支持在长对话线程中进行大小写不敏感的文本搜索，提升了内容检索效率。

5.  **远程执行器的代理启动** [#33906](https://github.com/openai/codex/pull/33906)
    - **内容**: 实现了在远程执行器上启动托管网络代理，这对远程开发环境中的网络功能至关重要。

6.  **批量读取持久化历史记录** [#33905](https://github.com/openai/codex/pull/33905)
    - **内容**: 将反向搜索中的历史记录读取方式从单条改为批量，显著优化了深度搜索的性能。

7.  **实时对话 V3 的路由切换** [#33903](https://github.com/openai/codex/pull/33903)
    - **内容**: 为实时对话 V3 版本增加了多种响应通道路由模式（thinking, commentary, bemTags），为更复杂的交互模式奠定基础。

8.  **支持 ChatGPT 品牌桌面应用构建** [#33901](https://github.com/openai/codex/pull/33901)
    - **内容**: 使得桌面应用可以基于 Codex 或 ChatGPT 品牌构建，CLI 可并行发现两者，适应产品线调整。

9.  **线程 MCP 连接集中化** [#33889](https://github.com/openai/codex/pull/33889)
    - **内容**: 将线程的 MCP (Model Context Protocol) 连接管理集中到 `McpRuntime` 中，提高了连接管理的原子性和可靠性。

10. **合作模式状态持久化与恢复** [#33876](https://github.com/openai/codex/pull/33876)
    - **内容**: 将合作模式状态持久化到 World State 中，使得对话恢复后能保持之前的协作模式状态。

## 功能需求趋势

1.  **IDE 集成与智能增强**: LSP 集成（#8745）需求排名第一，表明社区的核心诉求已从简单代码生成转向深度 IDE 体验。
2.  **多平台体验一致性**: 关于 Linux 计费（#27915）、Windows 性能（#33780, #33884, #29499）和远程控制缺失（#28919）的反馈，显示出用户对各平台功能对等和稳定性的强烈预期。
3.  **基础体验优化**: 父工作区多仓库支持（#26338）、禁用定时自动解决问题（#29702）、RTL/LTR 文本渲染（#26250）等需求，体现了社区对日常开发体验精细化打磨的诉求。
4.  **上下文管理增强**: 关于 Thread Context Pins（#26889）的设计讨论，反映出用户对长对话中关键信息持久化和有效管理的需求增长。
5.  **速率限制透明化**: 多个 Issue 报告速率限制显示异常，用户对计费策略和用量状态的高度敏感，要求信息准确、透明。

## 开发者关注点

- **Windows 平台性能是头号痛点**: 应用周期性卡死、启动时挂起、高 CPU 占用等一系列问题，成为了 Windows 用户最大的噩梦，严重阻碍了日常使用。
- **速率限制与计费问题引发焦虑**: “5小时限制消失”的集体报告（#32791 系列）非常罕见，这给用户带来了不确定性，需要官方尽快澄清和修复。
- **子代理（Sub-agent）的交互有待改进**: 无论是无法选择子代理（#30813），还是子代理超时问题（#24951），都表明多代理工作流的管理和控制界面还不够成熟。
- **远程能力的平台差异**: Windows 上缺失的“控制其他设备”是一个明显的功能“坑”，损害了跨设备协作的流畅性。

---
**精选热评**:
> 来自 Issue [#8745](https://github.com/openai/codex/issues/8745)
> “We need Codex CLI to use LSP diagnostics and symbol intelligence to produce more accurate code.” - 社区开发者对 LSP 集成的渴望，表达了用 AI 工具提升代码质量的朴素愿望。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# 2026-07-18 Gemini CLI 社区动态日报

## 今日速览

社区聚焦于子代理行为异常与安全加固，多个 P1 级别的 Bug 和 PR 在昨日密集更新。核心 agent 的无限 ReAct 循环和变量注入绕过问题已通过合并 PR 修复，同时一个自动 PR 生成管道的系列 PR 开始引入，显示了项目在 CI/CD 集成方向的新探索。另外，AST 感知文件读取和记忆系统质量改进依然是长期工作流中的热点。

---

## 社区热点 Issues

1. **[#22323] Subagent recovery after MAX_TURNS 被错误报告为 GOAL 成功**  
   - **优先级**: P1, Bug | **评论**: 11 | **👍**: 2  
   - **重要性**: 子代理在达到最大轮次后返回 `status: success` 和 `Termination Reason: "GOAL"`，掩盖了真实的中断原因，导致用户和自动化流程误判，严重损害了 agent 行为可观测性。  
   - **链接**: https://github.com/google-gemini/gemini-cli/issues/22323

2. **[#24353] Robust component level evaluations**  
   - **优先级**: P1 | **评论**: 7 | **👍**: 0  
   - **重要性**: 该 Epic 追踪组件级评估体系的建设，旨在从 behavioral eval 扩展至更细粒度的测试，是提升 agent 质量保证的基础设施。  
   - **链接**: https://github.com/google-gemini/gemini-cli/issues/24353

3. **[#22745] Assess the impact of AST-aware file reads, search, and mapping**  
   - **优先级**: P2 | **评论**: 7 | **👍**: 1  
   - **重要性**: 探索 AST 感知工具是否能减少 token 消耗、降低误读轮次，对 agent 效率和成本有直接影响，社区关注度高。  
   - **链接**: https://github.com/google-gemini/gemini-cli/issues/22745

4. **[#21409] Generalist agent hangs**  
   - **优先级**: P1, Bug | **评论**: 7 | **👍**: 8  
   - **重要性**: 通用代理在简单任务（如创建文件夹）时无限挂起，用户需要手动禁止使用子代理才能绕过，是当前最影响日常使用的 Bug 之一。  
   - **链接**: https://github.com/google-gemini/gemini-cli/issues/21409

5. **[#21968] Gemini does not use skills and sub-agents enough**  
   - **优先级**: P2, Bug | **评论**: 6 | **👍**: 0  
   - **重要性**: 用户反馈 Gemini 不会主动使用自定义 skill 和子代理，除非明确指令，导致高级功能利用率低，反映 agent 自主决策能力的不足。  
   - **链接**: https://github.com/google-gemini/gemini-cli/issues/21968

6. **[#26522] Stop Auto Memory from retrying low-signal sessions indefinitely**  
   - **优先级**: P2, Bug | **评论**: 5 | **👍**: 0  
   - **重要性**: Auto Memory 对低信息量对话反复重试，浪费资源且可能无限循环，影响后台服务的稳定性。  
   - **链接**: https://github.com/google-gemini/gemini-cli/issues/26522

7. **[#25166] Shell command execution gets stuck with "Waiting input" after command completes**  
   - **优先级**: P1, Bug | **评论**: 4 | **👍**: 3  
   - **重要性**: 简单 shell 命令执行完成后仍显示“等待输入”导致代理卡住，影响交互流畅性，属于高频复现问题。  
   - **链接**: https://github.com/google-gemini/gemini-cli/issues/25166

8. **[#21983] Browser subagent fails in Wayland**  
   - **优先级**: P1, Bug | **评论**: 4 | **👍**: 1  
   - **重要性**: Wayland 环境下浏览器子代理无法正常工作，阻碍 Linux 用户使用图形化 agent 功能。  
   - **链接**: https://github.com/google-gemini/gemini-cli/issues/21983

9. **[#21000] Experiment with using native file tools for creating and maintaining the task tracker**  
   - **优先级**: P3 | **评论**: 4 | **👍**: 0  
   - **重要性**: 提议使用原生文件工具管理任务追踪器，减少对 sub-agent 的依赖，可降低系统复杂度和失败率。  
   - **链接**: https://github.com/google-gemini/gemini-cli/issues/21000

10. **[#20079] Symlink in agents folder not recognized as an agent**  
    - **优先级**: P2, Bug | **评论**: 4 | **👍**: 0  
    - **重要性**: 用户希望使用符号链接管理 agent 配置文件，但当前不被识别，限制了自定义配置的灵活性。  
    - **链接**: https://github.com/google-gemini/gemini-cli/issues/20079

---

## 重要 PR 进展

1. **[#28429] fix(core): mitigate infinite ReAct loops and prompt injection loops**  
   - **状态**: 已合并 (CLOSED) | **优先级**: P1 | **大小**: M, XL  
   - **内容**: 引入每用户请求最多 15 轮的递归推理限制，并增强工具调用循环检测，防止恶意 workspace 文件导致无限循环或配额耗尽。  
   - **链接**: https://github.com/google-gemini/gemini-cli/pull/28429

2. **[#28403] fix(core): block $VAR and ${VAR} variable expansion bypass**  
   - **状态**: 开放 (OPEN) | **优先级**: P1 | **大小**: M, L  
   - **内容**: 修复了 `detectBashSubstitution()` 和 `detectPowerShellSubstitution()` 对变量扩展模式的遗漏，防止安全绕过（GHSA-wpqr-6v78-jr5g）。  
   - **链接**: https://github.com/google-gemini/gemini-cli/pull/28403

3. **[#28424] refactor(cli): align macOS permissive Seatbelt profiles with deny-default model**  
   - **状态**: 已合并 (CLOSED) | **优先级**: P1 | **大小**: L  
   - **内容**: 更新 macOS `permissive-open` 和 `permissive-proxied` 安全策略为 `(deny default)` + 显式白名单，使宽松模式默认拒绝并提升安全性。  
   - **链接**: https://github.com/google-gemini/gemini-cli/pull/28424

4. **[#28386] fix(vscode): track activation disposables**  
   - **状态**: 开放 (OPEN) | **优先级**: P2 | **大小**: M  
   - **内容**: 修复 VS Code 插件激活路径中因括号包裹导致的 disposables 追踪遗漏问题，确保资源正确释放。  
   - **链接**: https://github.com/google-gemini/gemini-cli/pull/28386

5. **[#28345] feat(caretaker-triage): implement LLM triage orchestrator and container build**  
   - **状态**: 已合并 (CLOSED) | **大小**: L  
   - **内容**: 引入基于 Antigravity SDK 的 LLM 分类编排器，用于自动对 issue 进行 triage，并构建 Cloud Run Job 容器。  
   - **链接**: https://github.com/google-gemini/gemini-cli/pull/28345

6. **[#28275] fix(core): make direct GCP telemetry exporters optional**  
   - **状态**: 已合并 (CLOSED) | **优先级**: P3 | **大小**: XL  
   - **内容**: 将 Google Cloud 遥测导出器从核心运行时依赖中移除，改为可选，减少核心包的依赖负担。  
   - **链接**: https://github.com/google-gemini/gemini-cli/pull/28275

7. **[#28435] feat(pr-generator-core): add environment config parser, command executor, GitHub REST API client**  
   - **状态**: 开放 (OPEN) | **大小**: L  
   - **内容**: 自动 PR 生成管道的基础模块，包含配置解析、子进程执行和 GitHub API 集成。  
   - **链接**: https://github.com/google-gemini/gemini-cli/pull/28435

8. **[#28434] feat(pr-generator-agent): implement Antigravity agent runner and prompt templates**  
   - **状态**: 开放 (OPEN) | **大小**: L  
   - **内容**: 提供 headless AI agent 的系统提示模板和运行器，用于迭代式代码生成与质量门控。  
   - **链接**: https://github.com/google-gemini/gemini-cli/pull/28434

9. **[#28433] feat(pr-generator-orchestrator): implement iterative bug-fixing state machine and container worker entrypoint**  
   - **状态**: 开放 (OPEN) | **大小**: L, XL  
   - **内容**: 实现 Firestore 并发锁定、AI agent 编码与评估的循环状态机、ESLint 分析、diff 大小验证等。  
   - **链接**: https://github.com/google-gemini/gemini-cli/pull/28433

10. **[#28346] Fix trust dialog disclosure for runnable hooks**  
    - **状态**: 开放 (OPEN) | **优先级**: P1 | **大小**: M  
    - **内容**: 修复文件夹信任对话框可能暴露实际可执行钩子之外的非钩子条目，增强安全提示信息。  
    - **链接**: https://github.com/google-gemini/gemini-cli/pull/28346

---

## 功能需求趋势

- **Agent 行为诊断与可观测性**：社区迫切希望子代理能如实报告中断原因（如 MAX_TURNS），并能在 `/chat share` 中查看子代理轨迹，以便调试和评估。
- **AST 感知工具链**：多个 Issue 探讨使用 AST 解析来优化文件读取、代码搜索和代码库映射，旨在减少 token 消耗和提升 agent 效率。
- **安全加固**：变量注入绕过、信任对话框信息泄露、macOS Seatbelt 策略对齐等安全相关 PR 占据高优先级，表明项目正系统性地提升安全基线。
- **Auto Memory 与记忆系统优化**：针对记忆提取的无限重试、低信号会话处理、补丁验证等问题，社区期望更稳定且资源友好的记忆管理。
- **自动化 CI/CD 集成**：一连串 `pr-generator-*` 系列 PR 显示团队正在构建从 Issue 到 PR 的自动代码生成管道，涵盖 Firestore 并发控制、LLM 分类、ESLint 检测等组件。

---

## 开发者关注点

1. **无限循环与卡死问题**：`generalist agent hangs`（#21409）和 `shell command stuck`（#25166）是高频痛点，影响日常开发效率，用户不得不手动限制 agent 行为。
2. **子代理自主性不足**：Gemini 不会主动使用用户定义的 skill 和子代理（#21968），需要明确指令，削弱了自定义扩展的价值。
3. **配置兼容性问题**：浏览器子代理在 Wayland 上失效（#21983）、symlink agent 不被识别（#20079）、settings.json 中 maxTurns 对 browser agent 无效（#22267）等配置相关 Bug 反馈集中。
4. **资源与性能**：高 turn 限制导致大量 token 消耗和 API 配额快速耗尽，`Auto Memory` 在低信号会话上的无限重试进一步浪费资源。
5. **安全与信任**：变量注入绕过、信任对话框泄露、文件权限 TOCTOU 问题等安全修复正在密集进行，开发者对 agent 的沙箱安全信任度仍需加强。

---

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

好的，以下是为您生成的 **GitHub Copilot CLI 社区动态日报（2026-07-18）**。

---

# GitHub Copilot CLI 社区动态日报

**日期：2026-07-18** | 数据来源：github.com/github/copilot-cli

---

## 1. 今日速览

昨日发布了 **v1.0.72-1** 小版本，主要扩展了插件子命令和终端显示优化。社区 Issues 数量激增（23 条），其中 **语音模式全模型静默失败**（#4024）、**Windows 插件安装权限拒绝**（#4151）和 **计划模式过度拦截只读命令**（#4160）是讨论热度最高的 Bug；此外，多个用户反馈了僵尸进程泄漏、Telemetry 缺失、Gemini 模型返回 400 错误等影响稳定性的问题。

---

## 2. 版本发布

### v1.0.72-1

- **Added**
  - 新增 `--plugin`、`--mcp`、`--skill` 三个标志位，支持插件相关变更操作
  - `copilot plugins remove --skill` 增加技能移除能力
- **Improved**
  - 展开紧凑编辑行时，显示完整文件路径
  - 计划审批菜单（plan-approval menu）在不同模型下行为保持一致
  - `/add-dir` 目录保持可见

---

## 3. 社区热点 Issues（精选 10 条）

1. **[#4024] Voice mode: 所有内置 ASR 模型静默失败**  
   🏷️ `area:models`  
   **为什么重要**：语音模式记录音频正常，但所有三个支持模型（`nemotron-3.5-asr-streaming-0.6b` 等）均返回空转录，属于核心功能完全失效。12 条评论，社区关注度高。  
   [👉 查看详情](https://github.com/github/copilot-cli/issues/4024)

2. **[#3767] 附件过大导致会话永久卡死（已关闭）**  
   🏷️ `area:sessions, area:context-memory`  
   **为什么重要**：附件超过 CAPI 5MB 限制后，错误提示后会话无法恢复。虽已关闭，但揭示了无恢复路径的设计缺陷。  
   [👉 查看详情](https://github.com/github/copilot-cli/issues/3767)

3. **[#3762] `contextTier` 配置项完全无效**  
   🏷️ `area:context-memory, area:configuration`  
   **为什么重要**：即便在配置中设置`contextTier`，主会话和子 agent 仍使用默认模型；必须手动通过模型选择器切换后才生效。配置不生效会让用户困惑。  
   [👉 查看详情](https://github.com/github/copilot-cli/issues/3762)

4. **[#4151] Windows 上插件安装 100% 失败（权限拒绝）**  
   🏷️ `area:platform-windows, area:plugins`  
   **为什么重要**：`copilot plugin install` 在 Windows 11 上从任何来源（市场、GitHub、本地目录）均报 `Access is denied (os error 5)`，严重影响插件生态在 Windows 上的可用性。  
   [👉 查看详情](https://github.com/github/copilot-cli/issues/4151)

5. **[#4160] 计划模式过度拦截只读 Shell 命令**  
   🏷️ `triage`  
   **为什么重要**：基于关键词启发式的分类器错误地将大量只读命令（如 `git log --oneline`）判定为“可能修改工作区”并拦截，频繁打断工作流。3 条评论，用户反馈强烈。  
   [👉 查看详情](https://github.com/github/copilot-cli/issues/4160)

6. **[#4163] Copilot CLI 1.0.71 不清理子进程，僵尸进程累积**  
   🏷️ `triage`  
   **为什么重要**：子进程（约 2 个/分钟）成为僵尸进程，长期运行会耗尽系统进程表。影响服务器和长时间使用场景的稳定性。  
   [👉 查看详情](https://github.com/github/copilot-cli/issues/4163)

7. **[#4169] `copilot -p` 模式下不发送 OTEL Telemetry**  
   🏷️ `triage`  
   **为什么重要**：即使服务端配置启用了 Telemetry，使用 `-p`（管道）模式时完全无数据上报，导致无法在 IDE 中查看 CLI 会话的可观测性数据。  
   [👉 查看详情](https://github.com/github/copilot-cli/issues/4169)

8. **[#4155] Gemini 模型在 Copilot CLI 中返回 400 Bad Request**  
   🏷️ `area:models`  
   **为什么重要**：尝试使用 `gemini-3.1-pro-preview` 和 `gemini-3.5-flash` 发送纯文本提示时，全部失败。新模型兼容性问题需尽快修复。  
   [👉 查看详情](https://github.com/github/copilot-cli/issues/4155)

9. **[#4156] `git branch -D`（强制删除分支）被错误分类为“无需权限”**  
   🏷️ `area:permissions, area:tools`  
   **为什么重要**：`git push --delete` 会触发权限请求，但 `git branch -D` 却静默执行，属于安全漏洞。用户可通过 `/diagnose` 确认分类错误。  
   [👉 查看详情](https://github.com/github/copilot-cli/issues/4156)

10. **[#4159] 交互模式在 Windows Terminal 中提交后变空白**  
    🏷️ `area:platform-windows, area:terminal-rendering`  
    **为什么重要**：交互模式首次正常显示，提交任何提示后 UI 完全空白，而 `-p` 模式正常工作。影响绝大多数 Windows 用户的日常使用。  
    [👉 查看详情](https://github.com/github/copilot-cli/issues/4159)

---

## 4. 重要 PR 进展

过去 24 小时内无 Pull Request 更新。

---

## 5. 功能需求趋势

从近期 Issue 中提炼出社区最关注的几个功能方向：

- **权限精细化控制**  
  多个 Issue（#4150、#4156、#4157）要求：支持带空格的命令自动批准、路径前缀白名单、文件/网络权限更细粒度划分。

- **多账户 / 默认用户管理**  
  #4166 要求允许设置默认用户，避免频繁在个人和工作账户之间手工切换。

- **终端交互体验改进**  
  #4152 提出添加 `j/k` 导航快捷键（类 Vim）；#4154 抱怨最近更新使 TUI 无法选择文本。

- **本地模型 / 信用限制优化**  
  #4167 希望允许 `-max-ai-credits=0` 以在使用本地模型时彻底禁用远程信用消耗；#4168 希望关闭低信用警告。

- **定时任务与日程提示**  
  #4137 反映定时提示不触发，社区期待该功能稳定可用。

- **语音模式修复需求**  
  #4024 暴露语音模式全面失效，语音输入作为 Beta 功能急需修复。

---

## 6. 开发者关注点（痛点与高频需求）

1. **配置不生效**：`contextTier` 完全无效，用户需手动切换模型才能启用长上下文。
2. **会话卡死无恢复**：附件过大（#3767）或僵尸进程累积（#4163）后，会话无法恢复，需要手动重启。
3. **Windows 兼容性差**：插件安装全失败（#4151）、交互模式变白（#4159）、`--resume` 挂起（#4165），Windows 成为第二等公民。
4. **权限误判**：计划模式拦截只读命令（#4160），同时危险命令（`git branch -D`）却不要求权限（#4156），双重矛盾。
5. **复制粘贴污染**：选中提示输入框时复制会附带左边框字符（#4116），影响粘贴后的内容纯净度。
6. **模型兼容性**：Gemini 模型 400 错误（#4155）、语音模型全静默（#4024），新模型接入质量不稳定。
7. **可观测性缺失**：`copilot -p` 不发送 Telemetry（#4169），导致无法在 IDE 中追踪 CLI 会话状态。

---

*本日报基于 GitHub 公开数据自动生成，仅供社区参考。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 | 2026-07-18

## 1. 今日速览

过去24小时内，Kimi Code CLI 社区共有4个活跃 Issue，无新 Release 或 Pull Request。其中，**模型切换的诉求持续发酵（#1925）**，用户呼吁能够回退至 K2.5 以避免 K2.6 的“思维链过重”问题；**Wind 数据插件因依赖指向内网而完全不可用（#2505）** 成为新的阻塞性 Bug；此外，Windows PowerShell 5.1 安装脚本崩溃（#2504）和 TUI 中 Markdown 换行字词截断（#2379）也获得了关注。

## 2. 版本发布

*（无）*

## 3. 社区热点 Issues

> 因过去24小时内活跃的 Issue 只有4条，以下全量列出，按新近程度排序。

### #1925 [增强] 希望支持在 K2.5 与 K2.6 模型间切换  
- **作者**: @herrbasan  
- **创建**: 2026-04-17｜**更新**: 2026-07-17｜**评论**: 13  
- **摘要**: 用户强烈要求允许手动切换到 Kimi K2.5 模型（含旧版系统提示），认为 K2.6 的“思维链”压制了创造性并增加幻觉，且丧失了模型原有的“人格”。该 Issue 已持续活跃近3个月，13条评论反映了不少用户的共鸣。  
- 🔗 https://github.com/MoonshotAI/kimi-cli/issues/1925

### #2505 [Bug] Wind 插件取数失败：agent-gw-pysdk 依赖安装指引指向公网不可达的内网地址  
- **作者**: @Steven-DD  
- **创建/更新**: 2026-07-17｜**评论**: 1  
- **摘要**: Kimi Work 桌面端的 `wind-allskill` 插件所有取数调用均返回 `NETWORK_ERROR`，根因是依赖 `agent-gw-pysdk` 未随插件安装，而官方安装指引指向 Moonshot 内网 Git 服务器 `dev.msh.team`，公网用户无法解析。该 Bug 导致 Wind 插件功能完全不可用，对金融量化开发者影响较大。  
- 🔗 https://github.com/MoonshotAI/kimi-cli/issues/2505

### #2379 [Bug] TUI 中 Markdown 列表项换行时字符被截断  
- **作者**: @bdragan  
- **创建**: 2026-05-27｜**更新**: 2026-07-17｜**评论**: 1  
- **摘要**: 在 Linux 系统（Kimi Code CLI v1.45.0，使用 K2.6 模型）的文本界面（TUI）中，渲染 Markdown 列表时，项目符号后的单词在换行处会被截断，严重影响可读性。社区建议修复文本换行算法。  
- 🔗 https://github.com/MoonshotAI/kimi-cli/issues/2379

### #2504 [Bug] install.ps1 在 Windows PowerShell 5.1 中因 IndexOutOfRangeException 崩溃  
- **作者**: @lyp1938  
- **创建/更新**: 2026-07-17｜**评论**: 0  
- **摘要**: 使用官方安装命令 `irm https://code.kimi.com/kimi-code/install.ps1 | iex` 在 Windows PowerShell 5.1 上安装 v0.26.0 时，`Invoke-WebRequest` 抛出索引越界异常，安装失败。该问题影响大量仍在使用 Win10/11 自带 PowerShell 5.1 的开发者。  
- 🔗 https://github.com/MoonshotAI/kimi-cli/issues/2504

## 4. 重要 PR 进展

*（无）*

## 5. 功能需求趋势

基于近期活跃 Issue，社区最关注以下方向：

| 需求方向 | 代表 Issue | 说明 |
|--------|------------|------|
| **模型选择与回退** | #1925 | 用户希望 CLI 能支持切换至旧版模型（如 K2.5），以保留个性化和低幻觉输出，避免 K2.6 的过度思维链。该诉求持续数月，讨论热度最高。 |
| **插件生态与内网依赖** | #2505 | Wind 插件依赖指向内部 Git 服务器，暴露了第三方插件安装机制对公网用户的不友好，急需提供镜像或公网包版本。 |
| **终端交互体验** | #2379 | Markdown 列表的换行渲染 Bug 被用户标记为“长时间未修复”，反映出 TUI 稳定性仍需打磨。 |
| **跨平台安装兼容性** | #2504 | Windows PowerShell 5.1 安装脚本崩溃，提示 CLI 对旧版 PowerShell 的支持存在漏洞，影响企业用户首次部署体验。 |

## 6. 开发者关注点

- **模型行为不可控**：多名用户反映 K2.6 的“思维链”过重，导致输出质量下降（创造力被压制、幻觉增加），且无法通过 API 参数完全关闭。官方若持续不提供模型切换选项，可能流失追求个性化输出的开发者。
- **插件依赖不可达**：Wind 插件的依赖安装指引指向内网地址属于明显的产品遗漏（QA 未覆盖公网环境），导致依赖安装环节永久卡死。开发者建议：在未解决前，应在插件文档中标注“仅限内部使用”，或提供备用 PyPI 源。
- **Windows 安装坑**：`install.ps1` 在 PowerShell 5.1 崩溃，且无错误回退提示。当前版本 0.26.0 与主流企业环境不兼容，建议紧急修复或添加 PowerShell 版本检测逻辑。
- **UI 细节粗糙**：Markdown 换行截断虽非功能阻塞，但长期存在（自 5 月底）说明 TUI 渲染引擎存在结构性缺陷，可能影响 CLI 作为“Code”工具的专业形象。

---

*数据截止 2026-07-18 09:00 UTC，由 AI 自动生成。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 2026-07-18 OpenCode 社区动态日报。

---

## OpenCode 社区动态日报 | 2026-07-18

### 今日速览

今日社区焦点集中在 **opencode2 (next) 版本** 的兼容性问题，用户报告了多个关于自定义 OpenAI-compatible 提供商、插件加载和配置覆盖的严重 Bug。同时，**自动发现模型** 和 **SSH 远程连接** 这两大功能需求持续获得高热度讨论，社区对用户体验和远程开发能力的期待非常高。

### 社区热点 Issues

1.  **[#6231] 自动发现 OpenAI-compatible 提供商中的模型**
    - **重要性**: **极高**。用户手动配置模型列表繁琐且易错，特别是对于本地模型经常变更的提供商。该需求获得了 181 个赞，是当前社区最强烈的呼声之一。
    - **社区反应**: 讨论热烈，已有 21 条评论，用户普遍支持并要求尽快实现。
    - **链接**: https://github.com/anomalyco/opencode/issues/6231

2.  **[#7790] [功能] OpenCode 桌面版支持基于 SSH 的远程连接**
    - **重要性**: **极高**。该功能被视为将桌面版从“完全无用”变为“可用”的关键特性，获得 73 个赞。
    - **社区反应**: 15 条评论中有非常具体的实现讨论，表明用户对此有迫切需求。
    - **链接**: https://github.com/anomalyco/opencode/issues/7790

3.  **[#37012] [功能] : 保留旧版布局选项**
    - **重要性**: 高。新版 UI 的改动引发了部分用户的强烈不满，他们怀念旧版布局的易用性和高效率，特别是工作区功能。
    - **社区反应**: 13 条评论详细阐述了旧版布局的优势，社区分歧明显，开发团队面临 UI 设计平衡的挑战。
    - **链接**: https://github.com/anomalyco/opencode/issues/37012

4.  **[#31119] [Bug] 数据库错误: no such column: name**
    - **重要性**: **高**。这是一个严重的回归 Bug，导致用户无法正常使用应用，影响了从旧版本升级的用户。
    - **社区反应**: 13 条评论，用户反馈了具体的复现步骤和版本信息，开发团队需紧急修复以恢复用户信任。
    - **链接**: https://github.com/anomalyco/opencode/issues/31119

5.  **[#31041] Zen API 对 CORS 预检请求 (OPTIONS) 返回 404**
    - **重要性**: **高**。此 Bug 完全阻止了所有浏览器端（Web）客户端调用 Zen API，严重影响了 API 的可用性。
    - **社区反应**: 10 条评论，社区已提供详细的错误信息和证据，问题明确，亟待解决。
    - **链接**: https://github.com/anomalyco/opencode/issues/31041

6.  **[#33998] [OpenCode Go] GLM-5.2 提示缓存间歇性失效**
    - **重要性**: **高**。此问题导致模型性能下降和成本增加，影响了通过 `opencode-go` 网关使用 GLM-5.2 的用户体验。
    - **社区反应**: 10 条评论，用户通过严谨的测试（36 次 API 调用）验证了问题存在，对网关的稳定性提出了质疑。
    - **链接**: https://github.com/anomalyco/opencode/issues/33998

7.  **[#5305] [功能]: 为即时 TUI 命令添加插件钩子**
    - **重要性**: **高**。该功能能极大提升插件的交互能力，允许插件绕过 agent 直接执行命令，扩展了 OpenCode 的自动化可能性。
    - **社区反应**: 19 条评论，讨论深入，表明用户对插件生态系统的强大功能有很高期待。
    - **链接**: https://github.com/anomalyco/opencode/issues/5305

8.  **[#37531] opencode2: 即使 API 正常工作，也提示“模型不可用”**
    - **重要性**: **高**。这是 `opencode2 (next)` 中一个关键的兼容性 Bug，直接影响用户在新版本中的基础使用体验。
    - **社区反应**: 3 条评论，已确认问题存在，是阻碍用户迁移至 next 版本的主要障碍之一。
    - **链接**: https://github.com/anomalyco/opencode/issues/37531

9.  **[#37553] [opencode2] OpenAI-compatible 解析器丢失 stream 中的 reasoning 内容**
    - **重要性**: **中等**。该问题导致部分提供商（如 vLLM）的“推理”过程无法显示，虽然最终回复正常，但削弱了功能的完整性和透明度。
    - **社区反应**: 2 条评论，问题描述清晰，对使用 vLLM 等特定提供商的用户影响较大。
    - **链接**: https://github.com/anomalyco/opencode/issues/37553

10. **[#37533] opencode2: 插件列表崩溃且未从配置加载**
    - **重要性**: **中等**。这是 opencode2 插件系统的基本功能缺陷，导致用户无法管理和使用已有的插件配置。
    - **社区反应**: 2 条评论，已明确是 chdir 路径问题，需要尽快修复以完善 opencode2 的插件生态。
    - **链接**: https://github.com/anomalyco/opencode/issues/37533

### 重要 PR 进展

1.  **[#37573] feat(plugin): 暴露活动的监听器 URL**
    - **内容**: 向插件提供其当前绑定的服务器监听地址 (`listenerUrl`)，增强了插件与外部服务交互的灵活性。
    - **重要性**: 对插件开发者非常有价值，是完善插件生态的重要一步。
    - **链接**: https://github.com/anomalyco/opencode/pull/37573

2.  **[#37572] fix(cli): 通过端口绑定选举托管服务**
    - **内容**: 用端口绑定的机制替换原有的 `ProcessLock`，并使用助记端口，以更可靠的方式实现对 `latest`、`local` 等托管服务的选举，解决端口冲突导致的启动问题。
    - **重要性**: 解决了多实例服务管理中的一个根本问题，提升了服务启动的稳定性。
    - **链接**: https://github.com/anomalyco/opencode/pull/37572

3.  **[#37571] fix(tui): 单独打包解析器 worker**
    - **内容**: 修复了一个构建 Bug，通过虚拟入口点编译 TUI 解析器 worker，避免了与 `OpenTUI 0.4.5` 版本的构建冲突。
    - **重要性**: 修复了`#37556`问题，确保 TUI 解析器能正常构建和工作。
    - **链接**: https://github.com/anomalyco/opencode/pull/37571

4.  **[#37477] fix: 不加载完整实例来显示会话列表**
    - **内容**: 优化了 `session list` 命令，使其不再需要加载整个应用实例来查询数据库，大幅提升了列表的加载速度。
    - **重要性**: 解决了 `#37435` 问题，改善了用户日常操作（如查看/切换会话）的体验。
    - **链接**: https://github.com/anomalyco/opencode/pull/37477

5.  **[#36710] fix(core): 限制事件日志压缩范围**
    - **内容**: 为事件日志压缩功能增加了受控能力，包括只读状态报告和显式的 `--apply` 参数，防止意外压缩数据。
    - **重要性**: 解决了 `#33356`，为重要的数据维护功能增加了安全性和可控性。
    - **链接**: https://github.com/anomalyco/opencode/pull/36710

6.  **[#32743] feat(session): 原生会话目标与 `/goal` 命令**
    - **内容**: 引入持久化的每个会话目标，并支持通过 `/goal` 命令进行管理（激活、暂停、完成），使 Agent 能够自主学习并追求目标。
    - **重要性**: 一个引人注目的新特性，将大大增强会话的自主性和任务管理能力。
    - **链接**: https://github.com/anomalyco/opencode/pull/32743

7.  **[#32741] fix(lsp): 允许自定义服务器配置 languageId**
    - **内容**: 为 `opencode.json` 中配置的自定义 LSP 服务器增加了可选的 `languageId` 字段，解决了此类服务器（如 R 语言服务器）无法正常工作的问题。
    - **重要性**: 对使用特定语言 LSP 的开发者来说是一个重要的修复，提升了 IDE 集成的质量。
    - **链接**: https://github.com/anomalyco/opencode/pull/32741

8.  **[#32728] feat(app): 添加实验性浏览器语音输入**
    - **内容**: 为 Web 提示框添加了实验性的语音输入功能，用户可以通过浏览器进行语音交互。
    - **重要性**: 探索新的交互方式，为未来可能的多模态交互奠定了基础。
    - **链接**: https://github.com/anomalyco/opencode/pull/32728

9.  **[#37567] docs: 将 Agent Sessions 添加到生态系统 → 项目**
    - **内容**: 在生态文档中新增了一个第三方 macOS 应用 Agent Sessions，用于读取和管理 OpenCode 的本地会话历史。
    - **重要性**: 展示了社区围绕 OpenCode 构建工具的能力，有助于生态繁荣。
    - **链接**: https://github.com/anomalyco/opencode/pull/37567

10. **[#32738] fix(shell): 仅在存在编辑/写入工具时才在 bash 工具描述中提及它们**
    - **内容**: 优化了 bash 工具的提示信息，对于只读 Agent，不再错误地提示“使用 Edit/Write 编辑文件”，避免误导模型。
    - **重要性**: 修复了 `#32704`，这是一个高质量的改进，能有效提升模型在特定场景下的决策准确性。
    - **链接**: https://github.com/anomalyco/opencode/pull/32738

### 功能需求趋势

- **无缝模型集成**: 社区对 **自动发现本地和第三方模型** 的需求极为强烈（`#6231`），这反映了用户对配置简化与即插即用体验的追求。同时，对 `opencode2` 与 **各种 OpenAI-compatible 提供商** 的兼容性修复需求也非常紧迫。
- **远程开发体验**: **SSH 远程连接** 是桌面版最迫切需要的能力（`#7790`、`#33273`），表明用户期望 OpenCode 能够融入其现有的云端或服务器开发工作流。
- **UI/UX 的灵活性与稳定性**: 新版 UI 的改动引发了 **保留旧版布局** 的呼声（`#37012`），用户希望有选择权。同时，**“Ctrl+P”快捷键失灵** (`#37165`) 和 **IME（输入法）兼容性** (`#37167`) 等问题表明，基础的键盘交互流畅性是社区的痛点。
- **扩展性与自动化**: **插件系统**的增强是关键需求，包括 **即时 TUI 命令钩子** (`#5305`) 和 **暴露 listener URL** 给插件 (`#37573`)，这表明社区希望构建更强大、更自动化的插件。

### 开发者关注点

- **升级与迁移阵痛**: 从旧版升级到新版（尤其是 1.16.2 版本）时出现的 **数据库错误** (`#31119`)，以及迁移到 `opencode2` (`next`) 版本时出现的 **模型不可用** (`#37531`)、**插件加载失败** (`#37533`) 等兼容性问题，是当前开发者的主要痛点。
- **WSL 环境兼容性**: Windows 开发者在使用 WSL 时，路径处理不当会导致 **数据库损坏和服务崩溃** (`#36902`)，这是一个持续存在的系统性问题，严重影响 WSL 用户的使用。
- **成本与性能透明性**: 开发者对 **费用统计不准确**（如 Kimi K3 显示 $0.01）(`#37524`) 和 **提示缓存失效** (`#33998`) 等问题非常敏感，因为他们直接关系到模型的使用成本和响应性能。
- **核心功能缺陷**: **Subagent 无限挂起** (`#33028`)、**工具调用 Schema 错误** (`#34652`)、**上下文限制被忽略** (`#31020`) 等关键功能的 Bug 影响了开发者的实际工作流和信任感。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 (2026-07-18)

## 今日速览
- **版本发布**：v0.19.11-nightly.20260717 发布，聚焦 daemon 冷启动追踪与多工作区所有权加固。  
- **社区热点**：多工作区支持（RFC #6378）持续热烈讨论，本周已产出多项 implement PR；性能优化方向（#4748）与自动内存召回（#7040）同样备受关注。  
- **重要动态**：Web Shell 迎来 Git 状态芯片、目录自动补全、分屏持久化等多项 UX 增强；CLI 端则修复了任务面板残留、拼写错误等多个小问题。  

---

## 版本发布

### [v0.19.11-nightly.20260717](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.11-nightly.20260717.f8e6e8931)
- **feat(daemon)**: 追踪冷启动的首次会话 (Trace cold first-session startup)  
- **fix(serve)**: 加固多工作区所有权 (Harden multi-workspace ownership)  

---

## 社区热点 Issues

### 1. [#6378 - RFC: Support multiple workspaces in one qwen serve daemon](https://github.com/QwenLM/qwen-code/issues/6378)  
- **标签**：P2, feature-request, daemon, session-management  
- **摘要**：提议让一个 `qwen serve` 守护进程同时管理多个工作区，同时保持现有单工作区行为兼容。  
- **社区反应**：评论数最高(29)，引发多轮设计讨论，已产出多个子 Issue 和 PR（#7015, #7070, #7069 等），是目前最热的核心功能需求。

### 2. [#4748 - Optimize daemon cold start and qwen serve fast-path latency](https://github.com/QwenLM/qwen-code/issues/4748)  
- **标签**：enhancement, daemon, performance  
- **摘要**：原始基准显示 daemon 冷启动+首次会话耗时约 2.5s，纯 CLI 仅 0.7s，需优化剩余差距。  
- **社区反应**：6条评论，社区持续关注启动延迟对开发者体验的影响。

### 3. [#7040 - RFC: Reliable auto-memory recall — timing, quality, and telemetry](https://github.com/QwenLM/qwen-code/issues/7040)  
- **标签**：P2, feature-request, memory, roadmap  
- **摘要**：缩小范围后的自动内存召回路线图，仅包含三个独立可审查的改进点，不影响企业级记忆治理。  
- **社区反应**：6条评论，核心内存维护者已介入，讨论集中在召回时机与质量。

### 4. [#7051 - VS Code侧边插件报错](https://github.com/QwenLM/qwen-code/issues/7051)  
- **标签**：bug, integration, vscode  
- **摘要**：VS Code 中 Qwen ACP 进程因 Electron 参数传递错误退出，导致无法连接。  
- **社区反应**：6条评论，已标记为 `need-information`，用户积极提供复现环境。

### 5. [#6809 - Ctrl+S diff preview garbled for multi-line edits in permission dialog](https://github.com/QwenLM/qwen-code/issues/6809)  
- **标签**：bug, ui, rendering  
- **摘要**：多行编辑时，权限确认对话框的 Ctrl+S 差异预览出现行拼接混乱。  
- **社区反应**：4条评论，已关闭但修复方式待确认。

### 6. [#7096 - Main CI failed: E2E Tests](https://github.com/QwenLM/qwen-code/issues/7096)  
- **标签**：bug, ready-for-agent  
- **摘要**：主分支 E2E 测试 CI 失败，自动创建 Issue 并分配 agent 修复。  
- **社区反应**：4条评论，自动机器人频繁触发，显示 CI 稳定性仍需加强。

### 7. [#7044 - 升级就报错](https://github.com/QwenLM/qwen-code/issues/7044)  
- **标签**：bug, cli, core, installation  
- **摘要**：用户升级到 v0.19.11 后启动即报错。  
- **社区反应**：4条评论，欢迎 PR 贡献修复。

### 8. [#6806 - Status line context usage percentage does not refresh after /compress](https://github.com/QwenLM/qwen-code/issues/6806)  
- **标签**：bug, ui, rendering  
- **摘要**：执行 `/compress` 后状态栏令牌占用百分比不更新，需等到下一次模型请求。  
- **社区反应**：3条评论，欢迎 PR 修复。

### 9. [#6992 - Chained MCP calls fail silently with "Server configuration not found"](https://github.com/QwenLM/qwen-code/issues/6992)  
- **标签**：bug, mcp, windows  
- **摘要**：Windows 上连续调用两个不同 MCP 时，第二个静默失败且权限 UI 卡死。  
- **社区反应**：3条评论，属于 MCP 权限处理的严重问题。

### 10. [#7139 - Windows: Docker sandbox passes invalid workspace cwd to ACP shell tools](https://github.com/QwenLM/qwen-code/issues/7139)  
- **标签**：P1, bug, windows, sandbox  
- **摘要**：Windows 11 上 `qwen serve` 启动 Docker 沙箱后，shell 工具因工作目录无效而失败。  
- **社区反应**：刚创建（1条评论），但优先级为 P1，需紧急处理。

---

## 重要 PR 进展

### 1. [#7054 - feat(web-shell): git status chip, visual working-tree diff, and sidebar git status](https://github.com/QwenLM/qwen-code/pull/7054)  
- **功能**：为 Web Shell 添加 Git 状态芯片、工作树差异可视化以及侧边栏 Git 状态，使浏览器端会话 UI 具备基本 Git 意识。  
- **状态**：OPEN，评论0，但代码量大，影响面广。

### 2. [#6842 - fix(memory): resolve root symlinks in isAllowedMemoryPath before creation](https://github.com/QwenLM/qwen-code/pull/6842)  
- **修复**：解决在符号链接基目录下写入记忆时因路径比较不一致而被错误阻止的问题。  
- **状态**：OPEN，涉及内存系统关键路径。

### 3. [#7033 - fix(review): report what the transcripts prove; build the roster in one call](https://github.com/QwenLM/qwen-code/pull/7033)  
- **修复**：改进 `/review` 技能的报告准确性，避免输出未经证明的声明；同时优化一次调用构建名单。  
- **状态**：OPEN，通过实际 PR 狗粮测试发现并修复。

### 4. [#7062 - fix(cli): hide sticky task panel when agent is idle](https://github.com/QwenLM/qwen-code/pull/7062)  
- **修复**：对应 Issue #7061，代理完成任务后固定任务面板不再残留“正在运行”图标。  
- **状态**：CLOSED，已合入。

### 5. [#6739 - feat(browser-ext): add alpha readiness diagnostics](https://github.com/QwenLM/qwen-code/pull/6739)  
- **功能**：完善 Chrome 扩展的 alpha 就绪状态，包括守护进程和浏览器自动化诊断、运行时 MCP 状态、确定性打包等。  
- **状态**：OPEN，跨组件集成度较高。

### 6. [#7045 - feat: support full-turn multimodal routing for image prompts](https://github.com/QwenLM/qwen-code/pull/7045)  
- **功能**：当主模型为纯文本且配置了视觉回退模型时，将包含图片的完整轮次路由到支持视觉和 agent 能力的模型。  
- **状态**：OPEN，多模态能力重要增强。

### 7. [#7132 - fix(cli): correct misspelled handleUpdateRecieved -> handleUpdateReceived](https://github.com/QwenLM/qwen-code/pull/7132)  
- **修复**：修正自动更新处理函数中的拼写错误。  
- **状态**：CLOSED，小型代码整洁修复。

### 8. [#6931 - fix(cli): tighten VP-mode controls footprint and fix shell tool indicator overlap](https://github.com/QwenLM/qwen-code/pull/6931)  
- **修复**：修复视口模式下五个渲染问题，包括任务面板与子代理列表溢出、shell 工具指示器重叠等。  
- **状态**：OPEN，针对高密度终端的 UX 改进。

### 9. [#6945 - feat(cli): add daemon Todo stop guard](https://github.com/QwenLM/qwen-code/pull/6945)  
- **功能**：为 daemon/ACP 模式添加可选的 Todo 停止防护，允许在任务未完成时自动继续最多两次。  
- **状态**：OPEN，提升自动化工作流连续性。

### 10. [#6984 - feat(agents): support per-model sub-agent concurrency limits](https://github.com/QwenLM/qwen-code/pull/6984)  
- **功能**：新增 `agents.maxParallelAgentsByModel` 配置，可按模型 ID 限制并发后台子代理数量。  
- **状态**：OPEN，增强代理系统的资源控制能力。

---

## 功能需求趋势

从所有新/更新 Issue 中提炼的社区关注方向：

1. **多工作区支持** – RFC #6378 引发持续设计讨论，并衍生出会话所有权、API 端点等多个子功能需求。  
2. **守护进程性能优化** – 冷启动延迟（#4748）、内存召回时机（#7040）是性能热点。  
3. **MCP 权限与稳定性** – 链式 MCP 调用失败（#6992）、权限 UI 卡死等问题表明需要更健壮的 MCP 处理框架。  
4. **Web Shell 增强** – 文件夹选择器（#7102）、终端历史持久化（#7117）、分屏持久化（#7136）、Git 集成（#7054）等，Web UI 正在快速迭代。  
5. **VS Code 集成修复** – 插件侧边栏报错（#7051）、ACP 启动依赖问题（#7101）显示跨平台 Electron 兼容性需要加强。  
6. **Windows 平台兼容** – Docker 沙箱工作目录无效（#7139）、MCP 权限问题等，Windows 用户反馈增多。  
7. **CLI 交互改进** – Ctrl+C 退出后终端乱码（#6776）、取消提示恢复输入（#7138）、状态栏刷新等问题体现用户对基础交互体验的高要求。

---

## 开发者关注点

- **升级稳定性**：多个用户报告升级后无法启动（#7044），建议关注版本迁移测试。  
- **CI 可靠性**：3 次主分支 E2E 测试失败自动创建 Issue（#7096, #7111, #7086），需排查测试环境波动或代码回归。  
- **多模态路由**：图像提示的完整轮次路由（#7045）是社区期待的杀手功能，但实现复杂度高，需注意回退模型声明规范。  
- **自动修复机器人**：`autofix` 相关 PR 和 Issue 增多，bot 的 PR 注释双语化（#7137）值得关注，将提升非英语贡献者的参与度。  
- **子代理模型选择**：子代理运行后模型记录（#7099）、并发限制（#6984）等功能表明社区对代理的可控性和可观测性需求上升。

---

*数据时间范围：2026-07-17 ~ 2026-07-18（UTC）*  
*报告自动生成，如有遗漏或错误，请参考原始 GitHub 仓库。*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*