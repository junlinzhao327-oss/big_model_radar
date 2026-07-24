# AI CLI 工具社区动态日报 2026-07-25

> 生成时间: 2026-07-24 23:28 UTC | 覆盖工具: 7 个

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

好的，作为专注于 AI 开发工具生态的资深技术分析师，我已基于您提供的 2026 年 7 月 25 日各主流 AI CLI 工具的社区动态数据，为您生成以下横向对比分析报告。

---

### AI CLI 工具生态横向对比分析报告 (2026-07-25)

**报告日期**: 2026-07-25
**分析师**: AI 开发工具生态资深技术分析师

---

#### 1. 生态全景

当前 AI CLI 工具生态呈现出 **“百家争鸣、双核驱动”** 的竞争态势。以 **Claude Code** 和 **OpenAI Codex** 为代表的头部产品正通过引入更强的基础模型（如 Opus 5、GPT-5.5）加速功能迭代，但也因此引发了用户对模型行为控制权和付费价值的深刻反思。与此同时，**Gemini CLI**、**Copilot CLI** 和 **Qwen Code** 等追赶者则在特定领域（如 Agent 自省、GitHub 生态集成、Web Shell 体验）深耕，力求差异化突围。一个显著的共性是，**Windows 平台的稳定性、长对话中的上下文管理、以及 MCP 协议的标准化集成，已经取代模型能力本身，成为社区抱怨和期待的核心焦点**，标志着行业正从“模型能力竞赛”转向“产品体验与可靠性竞赛”。

#### 2. 各工具活跃度对比

| 工具名称 | 今日新/更新 Issues (Top 10参考) | 今日新/更新 PRs | 版本发布情况 | 社区整体活跃度 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | 10个 | 2个 | v2.1.219 | 中高（核心Bug讨论激烈，但PR贡献低迷） |
| **OpenAI Codex** | 10个 | 10个 | 3个 (Rust alpha) | 高（大量严重Bug反馈，基础设施迭代快） |
| **Gemini CLI** | 50个 (含更新) | 25个 (含更新) | 无 | 极高（社区活跃度最高，开发团队投入大） |
| **Copilot CLI** | 10个 | 0个 | v1.0.75 | 中（回归问题频发，社区反馈集中在老问题） |
| **Kimi Code CLI** | 6个 | 3个 | 无 | 低（社区规模较小，问题方向较分散） |
| **OpenCode** | 10个 | 10个 | v1.18.5 | 高（高赞功能需求+稳定性报告，PR关注安全） |
| **Qwen Code** | 31个 | 50个 | v0.21.0 | 极高（PR贡献量最大，生态扩展迅速） |

**结论**: **Gemini CLI** 和 **Qwen Code** 是今日社区最活跃、开发最频繁的工具，显示出强劲的追赶势头。**OpenAI Codex** 和 **OpenCode** 的活跃度也很高，但前者偏向应对 Bug 浪潮，后者则兼备功能演进和稳定性修复。**Claude Code** 和 **Copilot CLI** 在 PR 贡献上表现疲软，可能影响了社区的参与意愿。

#### 3. 共同关注的功能方向

多个工具的社区不约而同地指向了以下几个核心痛点：

- **Agent 行为控制与可配置性**:
    - **Claude Code**: 用户抗议 `AgentTool` 强制提示无法关闭。
    - **OpenAI Codex**: 用户希望自定义模型行为，避免网络过滤器误报。
    - **Gemini CLI**: 代理误报任务成功、挂起、忽略用户配置，社区呼吁更强的行为约束。
    - **Copilot CLI**: plan-mode 权限混乱，用户期望自定义规则。

- **长对话可靠性与上下文管理**:
    - **Claude Code**: `CLAUDE.md` 指令衰减、上下文丢失问题反复出现。
    - **OpenAI Codex**: 上下文压缩无效、session 恢复 OOM，引发额度浪费和性能问题。
    - **Copilot CLI**: 5MB 请求体限制、大 session 恢复时 OOM。
    - **Gemini CLI**: 自动内存对低信号会话无限重试。

- **跨平台兼容性（Windows 为首）**:
    - **OpenAI Codex**: Windows 桌面应用崩溃、Git 进程失控、WSL 误判。
    - **Copilot CLI**: Windows React/Ink 无限渲染循环、子进程问题。
    - **Qwen Code**: Windows 输入法光标偏差、WSL 渲染重复。
    - **Kimi Code CLI**: Windows 下方向键无法使用。

- **支付与订阅体验**:
    - **Claude Code**: 付费后自动作废、充值失败，长时间未解决。
    - **OpenAI Codex**: Pro 用户额度消耗异常，付费价值感下降。

- **MCP（Model Context Protocol）集成兼容性**:
    - **OpenAI Codex**: 修复 MCP 认证、配置刷新等问题。
    - **Gemini CLI**: 修复 MCP OAuth 令牌刷新失败。
    - **OpenCode**: 修复 MCP OAuth 安全问题、自动重连。
    - **Qwen Code**: 用户反馈 MCP 服务器工具列举超时、VSCode 集成失败。

#### 4. 差异化定位分析

| 工具名称 | 功能侧重 | 目标用户 | 技术路线特点 |
| :--- | :--- | :--- | :--- |
| **Claude Code** | 强大的模型能力（Opus 5）、深度代码理解 | 追求极致代码生成能力的高级开发者 | 深度绑定 Anthropic 模型，强调模型本身的能力天花板。 |
| **OpenAI Codex** | IDE深度集成、企业级功能（MCP、多代理） | 深度依赖微软/OpenAI生态的开发者 | 强调与VS Code、Xcode的集成，后台服务化（MCP），企业化。 |
| **Gemini CLI** | 系统级Agent、评测与安全性、Linux生态 | 高级用户、开源社区贡献者、安全研究者 | 注重 Agent 的自省、评测和安全，采用Rust构建底层，社区驱动。 |
| **Copilot CLI** | GitHub生态深度绑定、命令行专家 | 重度使用GitHub、习惯命令行的开发者 | 强调与 `gh` 命令的协同，聚焦于 `shell` 和 `plan-mode` 的交互。 |
| **Kimi Code CLI** | 跨设备协作、Agent能力外延、国产化 | 国产化需求、探索 Agent 实践的用户 | 特色功能如 Remote Control 讨论热，关注 Agent 在非纯代码场景的应用。 |
| **OpenCode** | 多Provider支持、P2P MCP、高定制性 | 追求灵活性、自行搭建工作流的资深开发者 | 支持多种AI模型提供商，在MCP安全、Provider配置上投入大。 |
| **Qwen Code** | 开源生态、Web Shell体验、中文社区 | 开源社区、中文开发者、WebIDE用户 | 创新Web Shell交互，社区PR贡献活跃，频道扩展（钉钉、微信）有中国特色。 |

#### 5. 社区热度与成熟度

- **快速迭代期**: **Gemini CLI** (极高 PR/Issue，开发团队投入大，但稳定性问题多)、**Qwen Code** (PR贡献惊人，功能迭代快，社区参与积极)。
- **成熟稳进期**: **OpenAI Codex** (迭代频繁，但多为基础设施和修复，显示产品已进入精细化打磨阶段)。
- **生态分化期**: **Claude Code** (社区讨论热度高，但 PR 贡献低迷，官方与社区互动不够顺畅，生态增长遇瓶颈)。
- **深度绑定期**: **Copilot CLI** (版本更新慢，新特性少，社区反馈以回归和老问题为主，增长趋于平缓)。
- **新兴探索期**: **Kimi Code CLI** (社区规模小，功能需求方向明确但用户基础尚在建立，潜力待释放)。
- **挑战者层**: **OpenCode** (社区活跃，功能讨论深入，尤其在安全和定制化方面，是高阶用户喜爱的“小而美”选项)。

#### 6. 值得关注的趋势信号

1.  **Agent 行为控制权是下一个“护城河”**：用户不再满足于模型有多强，而是更关注“我能不能管住它”。谁能在提供强大能力的同时，给予用户更精细、更透明的行为配置（而不是强加规则），谁就能赢得高阶开发者的信任。**Claude Code** 的 `AgentTool` 争议就是最好的反面教材。

2.  **“Windows 体验”等于“产品基础分”**：多个主流工具在 Windows 上遭遇严重稳定性问题，这已经成为巨大的差异化负分项。在跨平台开发日益普遍的今天，忽视 Windows 体验将直接流失大量主流开发者。

3.  **MCP 协议仍是“半成品”**：多个工具都暴露了 MCP 集成的不稳定性、认证安全性、可发现性等问题。虽然 MCP 是行业共识的未来方向，但离“即插即用”的成熟状态还有距离，这为工具厂商提供了巨大的差异化优化空间。

4.  **“付费但不值”的声音正在积聚**：Pro/Plus 等高端套餐的额度消耗计算不透明、不合理，成为社区公愤。这提示产品方需要重新审视定价模型和额度消耗逻辑，向用户提供更清晰的成本预期和价值感知，否则可能面临用户流失或降级。

5.  **Web Shell 和可视化正成为 CLI 的“第二增长曲线”**：Qwen Code 的 Web Shell 创新（如 Git 可视化面板、工作区选择器）引起了社区广泛关注。这表明纯文本交互的 CLI 正在向更丰富的图形化、Web 化界面演进，以降低使用门槛，吸引更多非硬核用户。

**对开发者的建议**:
- **选择工具前，先评估你的平台和场景**：如果你重度使用 Windows，**OpenAI Codex** 和 **Copilot CLI** 可能会带来较多困扰，而 **Gemini CLI** 和 **Qwen Code** 在适配性上可能更胜一筹。
- **关注 Agent 的可控性**：优先选择在指令遵循、行为配置上提供更高透明度的工具。
- **警惕“付费陷阱”**：选择公开、清晰的额度和定价模型的工具，并关注社区对“额度虚高”的抱怨。
- **拥抱 MCP，但保持耐心**：MCP 是未来，但当前集成挑战较大，需要时间成熟。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，这是根据您提供的 `anthropics/skills` 仓库数据（截止 2026-07-25）生成的 Claude Code Skills 社区热点分析报告。

---

## Claude Code Skills 社区热点报告 (2026-07-25)

### 1. 热门 Skills 排行

根据 PR 的评论活跃度和功能影响，以下 8 个 Skills 是社区当前关注的焦点：

- **功能**: 彻底修复技能创建器核心脚本 `run_eval.py` 在评估时始终报告 0% 召回率的致命 Bug。该修复涉及 Windows 兼容性、触发检测逻辑等多个方面，是当前社区开发最活跃的 PR。
- **社区讨论热点**: 该问题严重阻碍了技能创建与自动优化流程（关联 Issue #556, #1169, #1061），多个开发者报告了独立复现。PR #1298 试图一次性修复所有根因，社区高度关注其合并进展。
- **当前状态**: **Open**
- **链接**: https://github.com/anthropics/skills/pull/1298

- **功能**: 新增“文档排版”技能，专门处理 AI 生成文档中的孤词、孤行、标题孤立等排版问题。
- **社区讨论热点**: 该技能定位精准，解决了 AI 生成文档中普遍存在的“能用但不完美”的视觉痛点。社区认为这是一个对输出质量有显著提升的实用技能。
- **当前状态**: **Open**
- **链接**: https://github.com/anthropics/skills/pull/514

- **功能**: 新增对 ODT（OpenDocument）格式的全面支持，包括创建、填充模板和解析为 HTML。
- **社区讨论热点**: 填补了官方技能集中在 DOCX/PDF 方面的缺口，满足了使用 LibreOffice 等开源办公套件的用户需求。讨论集中在 ODT 模板的复杂性和与现有文档技能集的集成上。
- **当前状态**: **Open**
- **链接**: https://github.com/anthropics/skills/pull/486

- **功能**: 重构并优化了前端设计技能，旨在提供更清晰、可操作、内部一致的指导，确保 Claude 能在一个会话内有效执行。
- **社区讨论热点**: 社区普遍认为原版技能过于理论化，可操作性差。此 PR 代表了对“高质量技能定义”的追求，即如何让技能指令更具体、更易于AI遵循。
- **当前状态**: **Open**
- **链接**: https://github.com/anthropics/skills/pull/210

- **功能**: 新增“自我审计”技能，在交付前对 AI 输出进行机械文件验证和四维度推理质量审计。
- **社区讨论热点**: 该技能设计新颖，试图解决 AI 输出的幻觉和逻辑错误问题。社区对其“通用性”和“四维度评估标准”的有效性展开了热烈讨论，认为这是一项具有前瞻性的元技能。
- **当前状态**: **Open**
- **链接**: https://github.com/anthropics/skills/pull/1367

- **功能**: 修复技能创建器脚本在 Windows 下的运行崩溃问题，主要涉及子进程管道读取和编码。
- **社区讨论热点**: 这是众多 Windows 兼容性问题中的一个（另有 PR #1050, #1099），凸显了社区中 Windows 用户群体的活跃度以及官方工具对非 Unix 平台支持的不足。该 PR 被视为解决此系列问题的关键一步。
- **当前状态**: **Open**
- **链接**: https://github.com/anthropics/skills/pull/1099

- **功能**: 新增“颜色专家”技能，覆盖 ISCC-NBS、Munsell 等多种颜色命名系统和 OKLCH、OKLAB 等色彩空间，提供色彩知识的专业知识。
- **社区讨论热点**: 这是一个高度专业化、领域知识密集型的技能。社区肯定其内容的丰富度，并讨论如何将其与 UI/UX 或数据可视化等其他技能协同使用。
- **当前状态**: **Open**
- **链接**: https://github.com/anthropics/skills/pull/1302

- **功能**: 新增面向 Pyxel 复古游戏引擎的游戏开发技能，涵盖从编写代码到运行、捕捉画面、迭代的完整工作流。
- **社区讨论热点**: 代表了一种新的技能类别：结合外部 MCP 工具。社区关注点在于技能如何与 MCP 服务器高效协作，以及在“写-运行-调试”循环中的具体实现方式。
- **当前状态**: **Open**
- **链接**: https://github.com/anthropics/skills/pull/525

### 2. 社区需求趋势

从 Issues 中可以看出，社区最期待的新 Skill 方向主要围绕以下几个核心诉求：

- **安全与信任**: 社区成员@aliksir 提出的 Issue #492（已获 43 条评论）指出，社区技能在官方命名空间下分发可能导致信任边界滥用和权限提升风险，这已成为最受关注的安全议题。
- **组织级协作**: Issue #228（获 14 条评论）强烈呼吁官方提供组织级别的技能共享与分发机制，目前需要通过 Slack/Teams 手动分享 `.skill` 文件的方式效率低下。
- **工具链与平台兼容性**: 大量 Issues（如 #556, #1169）指向技能创建和评估工具（`run_eval.py`）的稳定性问题。同时，对 Windows 平台的兼容性抱怨集中爆发（#1061），表明社区生态正从纯 Unix 环境快速扩展。
- **特定领域专精**: 除了上述 Skils 排行中的具体方向，还有对**代理治理（Agent Governance）**（#412）、**紧凑记忆管理（Compact Memory）**（#1329）等前沿概念的技能提案，显示出社区对 Claude 作为智能代理能力的深入探索需求。
- **基础体验修复**: 技能突然消失（#62）、页面重定向错误（#184）等问题，表明社区对 Skils 管理、安装和配置的基础体验仍有较高期待。

### 3. 高潜力待合并 Skills

以下 PR 评论活跃、功能完整且已形成初步共识，有望在近期合并入主分支：

- **自我审计技能 (Self-Audit - PR #1367)**: 作为一项极具创新性的元技能，其“先机械验证、后逻辑审计”的设计受到社区广泛好评，若能解决部分争议点，有望被官方采纳为一项标准实践。
- **测试模式技能 (Testing-Patterns - PR #723)**: 覆盖了从单元测试到 E2E 测试的完整堆栈，内容专业、实用性强，对于希望提升代码质量的开发者非常有价值。
- **颜色专家技能 (Color-Expert - PR #1302)**: 知识体系完整，定位清晰，是专业化技能的典范，适用于设计、数据可视化等多个领域，合并可能性较高。
- **像素游戏开发技能 (Pyxel - PR #525)**: 展示了 Skill 与外部 MCP 工具的深度集成，具有示范意义，且作者是 Pyxel 引擎的原作者，权威性强。

### 4. Skills 生态洞察

> **一句话总结：社区当下最集中的诉求并非新增技能功能，而是解决基础工具链的稳定性（尤其是 Windows 兼容性）和评估流程的可靠性，同时迫切要求官方建立社区贡献的安全信任与组织级共享机制。**

---

---

好的，这是 2026 年 7 月 25 日的 Claude Code 社区动态日报。

---

# Claude Code 社区动态日报 | 2026-07-25

## 今日速览

**Claude Code 发布 v2.1.219，默认模型升级为 Claude Opus 5，带来 1M 上下文窗口和全新定价，但新模型引入的强制行为引发社区争议。** 支付问题依然是社区的最大痛点，一个长达两个月的“付款后自动作废”Bug 高居热度榜首，同时多位日本用户反映 API 充值失败。此外，核心指令遵循衰减、上下文丢失等长期顽疾再次被推上风口浪尖。

## 版本发布

**v2.1.219** 已于昨日发布，主要更新内容如下：
- **新模型支持**: 正式支持 Claude Opus 5 (`claude-opus-5`)，现为默认的 Opus 模型。提供 **1M** 上下文窗口，定价模式更改为快速模式，价格为输入 $10/Mtok，输出 $50/Mtok。
- **安全增强**: 新增 `sandbox.network.strictAllowlist` 设置，可拒绝沙盒命令访问未在白名单中的主机，无需用户确认。
- **新 Hook 事件**: 新增 `DirectoryAdded` 钩子，可在添加目录后触发。

## 社区热点 Issues

1.  **[#55982] 订阅计划升级支付持续失败** — 热度最高 Issue，长达 2 个月未解决。用户在升级计划时，支付意图在确认完成前被系统`void_invoice`，导致付款被立即作废。尽管有 25 个 👍，但官方仅标记为无效，社区反应强烈。
    - 链接: https://github.com/anthropics/claude-code/issues/55982

2.  **[#18467] 个人仓库在 Claude Web 中不可见** — 影响广泛，67 个 👍。用户只能看到组织下的仓库，个人账户创建的仓库无法被 Claude Code 访问，严重限制了许多独立开发者和小团队的使用。
    - 链接: https://github.com/anthropics/claude-code/issues/18467

3.  **[#80055] 日本用户购买 API 积分失败** — 新出现的支付问题。信用卡授权可通过，但最终购买流程返回“Payment failed”，涉及多张信用卡，包括新发行的卡片。
    - 链接: https://github.com/anthropics/claude-code/issues/80055

4.  **[#80873] CLAUDE.md 指令在对话中期“衰减”** — 核心功能 Bug。用户反馈 CLAUDE.md 中的规则在对话 5-10 轮后开始被模型忽略，即便规则仍在系统提示中。这触及了长对话中模型行为一致性的核心痛点。
    - 链接: https://github.com/anthropics/claude-code/issues/80873

5.  **[#80988] v2.1.219 强制注入 `AgentTool` 禁用提示** — 新版本引入的争议性变更。系统为 Opus 5 模型专门注入一条指令，警告“若非用户主动请求，不要调用 AgentTool”，且**无法通过配置关闭**，这被认为是对用户代理策略的无声覆盖。
    - 链接: https://github.com/anthropics/claude-code/issues/80988

6.  **[#52420] 请求自定义对话结束语动词** — 功能建议，获得 16 个 👍。众多用户希望能在 `settings.json` 中配置 `settings.json` 的结束行动词（如“cogitated for 12s”），目前是硬编码的随机列表。
    - 链接: https://github.com/anthropics/claude-code/issues/52420

7.  **[#74662] 桌面版需要多账户会话支持** — 桌面端用户在切换账户后，无法访问另一账户下的本地会话历史，严重影响了多账户（个人+工作）用户的日常工作流程。
    - 链接: https://github.com/anthropics/claude-code/issues/74662

8.  **[#80989] 桌面版 Code 标签页限制 Opus 5 上下文为 400K** — 新 Bug。尽管 Opus 5 支持 1M 上下文，但同一账户下，桌面版 Code 标签页的上限仅为 400K，而另一台机器（或 Web 端）则能正常使用 1M 上下文。
    - 链接: https://github.com/anthropics/claude-code/issues/80989

9.  **[#81015] `setup-token` 缺乏只读用量权限** — 开发者工具缺陷。`claude setup-token` 生成的令牌缺少 `user:profile` 权限，导致无法通过 `/usage` 命令查看用量，只能用于发送推理请求。
    - 链接: https://github.com/anthropics/claude-code/issues/81015

10. **[#81013 / #81014 / #81012] 服务器端 Rate Limiting 错误** — 多位用户（疑似同一人）在同一时间段内报告了服务器端速率限制错误，提示非客户端用量问题，而是服务器端主动拒绝请求（HTTP 429）。可能暗示后端服务遇到了瓶颈。
    - 链接: https://github.com/anthropics/claude-code/issues/81013

## 重要 PR 进展

当日仅收到 **2 个** Pull Requests 更新，社区贡献活动较为平淡。

1.  **[#80883] 尝试添加“上下文安全网”插件** — 社区提出的解决方案，旨在通过插件形式来缓解自动压缩导致的关键上下文丢失问题，作为一种非官方的恢复手段。
    - 链接: https://github.com/anthropics/claude-code/pull/80883

2.  **[#41611] 补充缺失的源代码引用** — 一项持续数月的文档/代码贡献，为 Claude Code 添加一个此前遗漏的源文件。目前已开放近 4 个月。
    - 链接: https://github.com/anthropics/claude-code/pull/41611

*(注：得益于官方近期大量关闭旧 Issue，当日 Issue 活跃度有所下降。PR 数量极少，社区贡献热度处于低位。)*

## 功能需求趋势

从过去 24 小时的反馈来看，社区最关注的功能方向是：

- **支付与订阅优化**: 支付失败问题仍是最急迫的需求。无论是计划升级还是 API 积分购买，流程的稳定性和成功率亟待提升。
- **模型行为可配置性**: 社区要求对模型行为有更强的控制权，例如自定义结束语动词，以及不希望被强制注入与自身工作流冲突的提示（如 `AgentTool` 规则）。
- **上下文与状态持久性**: 用户对 `CLAUDE.md` 指令衰减、会话历史丢失、自动压缩导致上下文丢失等问题表现出强烈不满，希望有更可靠的状态管理机制。
- **多账户与账户灵活性**: 随着工作场景的复杂化，用户对于在桌面端无缝切换和管理多个账户的需求日益增长。
- **文档完善**: 大量已关闭的 Issue 显示，社区持续在推动官方文档的完善，特别是 WSL、Windows 平台、MCP 连接器等高级或小众特性的文档补全。

## 开发者关注点

- **Opus 5 的“暗箱”行为**: 新模型带来的默认强制规则让人担忧，开发者希望 Anthropic 能提供透明的配置选项，而非无声覆盖用户习惯。
- **长对话失效瓶颈**: 无论是指令衰减还是上下文丢失，都在证明 Claude Code 在处理超长会话时，其内部的状态管理机制尚不稳固，这是影响高级用户采用的核心障碍。
- **跨平台体验不一致**: 桌面版与 CLI 之间的功能差异（如上下文窗口大小），以及 Windows 与 macOS 平台的特有 Bug，说明跨平台体验的打磨仍需投入。
- **API 基础设施稳定性**: 服务器端的 429 错误提示后端压力，对于依赖 API 的企业用户和重度开发者来说，这是一个潜在的稳定性风险信号。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

好的，作为专注于AI开发工具的技术分析师，我已根据您提供的 GitHub 数据，为您整理出 2026 年 7 月 25 日的 OpenAI Codex 社区动态日报。

---

### OpenAI Codex 社区动态日报 | 2026-07-25

#### 1. 今日速览

今日社区动态高度紧张，Windows 平台的稳定性问题成为绝对焦点，多个严重 Bug（如应用启动后无法使用、Git 进程失控）引发开发者广泛讨论。与此同时，项目组在后台基础设施上迭代频繁，发布了三个 Rust 版本的 alpha 更新，并合并了大量关于 MCP（Model Context Protocol）协议和内部架构优化的 PR。

#### 2. 版本发布

今日发布了三个连续版本的 Rust 编译器/工具链 alpha 更新，版本号从 `0.146.0-alpha.6` 递增至 `0.146.0-alpha.8`。从更新日志来看，这几个版本未包含显著的新功能或修复公告，可能侧重于内部依赖更新或小范围测试。

-   `rust-v0.146.0-alpha.8` | [发布链接](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.8)
-   `rust-v0.146.0-alpha.7` | [发布链接](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.7)
-   `rust-v0.146.0-alpha.6` | [发布链接](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.6)

#### 3. 社区热点 Issues

以下是从今日更新中筛选出的 10 个最值得关注的 Issue，其严重性、社区讨论热度或新出现的 Bug 特征均较为突出。

1.  **\[BUG\] Windows Codex Desktop 添加第二个项目文件夹后无法启动**
    -   **重要性**: **严重性极高**。影响 Windows 用户的核心使用流程，导致应用完全不可用。
    -   **社区反应**: 创建当日即有 18 条评论，5 个赞，表明多个用户遭遇此问题。
    -   **链接**: [Issue #35057](https://github.com/openai/codex/issues/35057)

2.  **\[BUG\] Pro 用户每周使用额度消耗异常快**
    -   **重要性**: **核心付费用户痛点**。直接关系到高价值用户的服务体验和付费意愿，已持续存在 3 个月。
    -   **社区反应**: 评论数高达 33 条，获得 29 个赞，社区反馈非常激烈。
    -   **链接**: [Issue #19585](https://github.com/openai/codex/issues/19585)

3.  **\[BUG\] Windows 上 Git 进程失控，导致高 CPU 和磁盘占用**
    -   **重要性**: **平台关键问题**。多个 Issue 指向同一类问题，表明这是一个系统性的 Windows 性能缺陷。
    -   **社区反应**: 13条评论，11个赞（Issue #20933）及 14条评论，24个赞（Issue #22085），开发者普遍反馈系统卡顿。
    -   **链接**: [Issue #20933](https://github.com/openai/codex/issues/20933) | [Issue #22085](https://github.com/openai/codex/issues/22085)

4.  **\[BUG\] 应用在 macOS 上每次启动都静默创建空文件夹**
    -   **重要性**: **用户体验问题**。虽不影响功能，但行为不符合预期，会打扰用户文件管理。
    -   **社区反应**: 20条评论，39个赞，是今日获赞最多的问题，说明用户对此类“不干净”的行为容忍度很低。
    -   **链接**: [Issue #20880](https://github.com/openai/codex/issues/20880)

5.  **\[BUG\] Xcode 27 Beta 登录失败，特定账户需邮箱 OTP 验证**
    -   **重要性**: **IDE 集成问题**。阻碍了使用最新 Beta 版 Xcode 的开发者。
    -   **社区反应**: 18条评论，11个赞，且问题描述清晰，影响了 Pro 用户。
    -   **链接**: [Issue #28078](https://github.com/openai/codex/issues/28078)

6.  **\[BUG\] VS Code 扩展在 Windows 多根工作区崩溃**
    -   **重要性**: **开发者工具稳定性**。影响使用复杂项目配置的高级用户。
    -   **社区反应**: 创建当日即有 5 条评论，影响范围明确。
    -   **链接**: [Issue #35073](https://github.com/openai/codex/issues/35073)

7.  **\[BUG\] 上下文压缩完成后仍占用 80% 容量，导致频繁重复压缩**
    -   **重要性**: **性能与资源浪费**。核心机制失效，可能导致更大的额度消耗和更差的体验，与 Issue #19585 可能有关联。
    -   **社区反应**: 14条评论，社区对机制本身有深入讨论。
    -   **链接**: [Issue #35032](https://github.com/openai/codex/issues/35032)

8.  **\[BUG\] Windows WSL 仓库被误判为“非 Git”**
    -   **重要性**: **平台兼容性问题**。影响大量在 WSL 环境下工作的 Windows 开发者。
    -   **社区反应**: 发布当日即获 3 个赞，显示其普遍性。
    -   **链接**: [Issue #35119](https://github.com/openai/codex/issues/35119)

9.  **\[BUG\] Codex CLI 网络安全过滤器误报**
    -   **重要性**: **功能可用性**。会错误拦截正常请求，影响工作效率。
    -   **社区反应**: 有持续讨论，开发者正在寻找绕过方法。
    -   **链接**: [Issue #33810](https://github.com/openai/codex/issues/33810)

10. **\[BUG\] 自定义模型 (非OpenAI) 在 MultiAgentV2 中无法理解加密任务**
    -   **重要性**: **高级特性缺陷**。影响自定义模型集成的核心功能，使得多代理协作不可用。
    -   **社区反应**: 5 条评论，2 个赞，开发者社区对此类高级功能的稳定性关注度很高。
    -   **链接**: [Issue #34833](https://github.com/openai/codex/issues/34833)

---

#### 4. 重要 PR 进展

今日 PR 合并频繁，主要集中在 MCP（Model Context Protocol）的完善、线程管理和新企业计划支持等后台基础设施上。

1.  **\[CLOSED\] 支持可配置的插件 MCP 端点**
    -   **重要性**: 提升 MCP 部署灵活性，允许开发者为插件服务指定独立端点。
    -   **链接**: [PR #31307](https://github.com/openai/codex/pull/31307)

2.  **\[CLOSED\] 协调 MCP 工具刷新**
    -   **重要性**: 解决并发刷新导致状态不同步的问题，提升 MCP 工具集的稳定性。
    -   **链接**: [PR #31310](https://github.com/openai/codex/pull/31310)

3.  **\[CLOSED\] 暴露工作区插件发布能力**
    -   **重要性**: 为客户端提供判断插件是否可发布到工作区的元数据，为未来的插件生态管理奠定基础。
    -   **链接**: [PR #35254](https://github.com/openai/codex/pull/35254)

4.  **\[CLOSED\] 支持分页线程的临时分支**
    -   **重要性**: 增强了分页线程功能，允许创建临时分支进行预览或实验，是重要的功能增强。
    -   **链接**: [PR #35251](https://github.com/openai/codex/pull/35251)

5.  **\[CLOSED\] 通过运行时 HTTP 客户端路由 MCP 认证发现**
    -   **重要性**: 修复 MCP 认证发现可能忽略代理配置的问题，提高了网络兼容性。
    -   **链接**: [PR #35239](https://github.com/openai/codex/pull/35239)

6.  **\[CLOSED\] 支持 `ent26` 企业计划**
    -   **重要性**: 新增对最新企业版订阅计划的后端支持，是商业化产品迭代的一部分。
    -   **链接**: [PR #35238](https://github.com/openai/codex/pull/35238)

7.  **\[CLOSED\] 避免为 Hook 转录持久化非本地线程**
    -   **重要性**: 修复了在特定情况下（Hook）可能错误持久化线程数据的问题。
    -   **链接**: [PR #35221](https://github.com/openai/codex/pull/35221)

8.  **\[CLOSED\] 跨线程独立刷新 MCP 配置**
    -   **重要性**: 优化了 MCP 配置更新逻辑，避免一个线程的失败影响其他线程。
    -   **链接**: [PR #35216](https://github.com/openai/codex/pull/35216)

9.  **\[CLOSED\] 启用显式执行器技能的资源读取**
    -   **重要性**: 修复了显式调用的技能可能无法读取其引用资源的问题，完善了技能系统的可靠性。
    -   **链接**: [PR #35198](https://github.com/openai/codex/pull/35198)

10. **\[CLOSED\] 在元数据压力下压缩主机技能路径**
    -   **重要性**: 优化技能目录的存储效率，防止绝对路径前缀浪费空间，间接提升技能加载性能。
    -   **链接**: [PR #35172](https://github.com/openai/codex/pull/35172)

---

#### 5. 功能需求趋势

从今日的 Issues 中可以看出社区的关注点正集中在以下几个方向：

-   **平台稳定性（尤其是 Windows）**：这是当前最突出的问题。大量 Issue 指向 Windows 桌面应用在启动、Git 集成、WSL 兼容性和整体性能上存在严重问题。
-   **资源消耗与额度管理**：Pro 用户的额度消耗异常和上下文压缩机制的缺陷，反映了用户对成本控制和资源利用效率的高度敏感。
-   **IDE 集成生态的成熟度**：Xcode 和 VS Code 扩展的登录、认证、多根工作区兼容性等问题表明，社区对与主流 IDE 的无缝集成有很高的期待。
-   **模型与代理能力的精细化控制**：自定义模型在多代理场景下的不兼容、安全过滤器的误报，说明用户正在探索更复杂的使用模式，对系统的健壮性要求更高。
-   **自动化和不需要的副作用**：应用自动创建文件夹、频繁自动更新等非功能性行为，引发了用户的普遍反感，表明用户期待一个更“干净”的工具。

#### 6. 开发者关注点

总结今日的开发者反馈，高频痛点如下：

-   **Windows 平台体验极差**：Git 进程疯狂启动是今日的“明星 Bug”，导致 CPU 和磁盘 I/O 飙升，严重影响开发机性能。此外，应用在 Windows 上频繁出现 “Oops” 错误和无法启动的问题，正在动摇 Windows 用户的使用信心。
-   **付费价值感下降**：Pro 用户（$200/月）的额度“无预警”快速消耗，尤其在使用 GPT-5.5 时，这种“用了却感觉用不起”的体验是最大的付费意愿杀手。
-   **核心机制可靠性不足**：上下文自动压缩功能看似成功实则无效，导致额度被浪费。网络安全过滤、响应流处理等机制存在漏洞，影响了功能的可用性和信任度。
-   **版本更新过于频繁且不稳定**：应用更新频繁，但更新后往往会引入新的问题（如项目丢失、登录失败），开发者开始产生“更新焦虑”。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 (2026-07-25)

> 数据来源：github.com/google-gemini/gemini-cli | 统计周期：过去24小时

---

## 今日速览

昨日社区活跃度较高，**未发布新版本**，但 **50 个 Issue 和 25 个 PR 获得更新**。最受关注的三条动态是：① **子代理在达到最大轮次后误报“Goal 成功”**（#22323），掩盖了中断原因；② **通用代理 (/generalist) 持续挂起** 问题仍未解决；③ 团队持续推进 **Caretaker Agent 评测框架**（PR #28530/#28532）和多项安全修复（HTTPS 强制、MCP OAuth 刷新等）。

---

## 社区热点 Issues（Top 10）

以下为过去 24 小时内更新、评论数最多或优先级最高的 Issue，反映当前社区的主要痛点。

1. **#22323 – 子代理达到最大轮次后误报 Goal 成功**  
   > 代码调查子代理因达到 `MAX_TURNS` 而中断，但其终止原因仍标记为 `GOAL`，导致用户误以为任务已完成。  
   > **优先级 P1**，评论 12，👍 2。涉及 agent 的成果报告准确性。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/issues/22323)

2. **#21409 – 通用代理持续挂起**  
   > 当 Gemini CLI 将任务委派给通用代理时，进程无限期挂起（简单创建文件夹操作也需等待 1 小时）。用户需手动禁止使用子代理才能绕过。  
   > **优先级 P1**，评论 8，👍 8。严重影响日常使用。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/issues/21409)

3. **#19873 – 利用模型的 Bash 倾向：零依赖 OS 沙箱与执行后意图路由**  
   > 建议让 Gemini 的原生 POSIX 工具链在安全沙箱中执行，同时保留后执行意图判断。  
   > **优先级 P2**，评论 8，涉及安全与模型能力最大化的长期需求。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/issues/19873)

4. **#24353 – 组件级评估**  
   > 追踪“行为评估”测试的完善，目前已生成 76 个测试，需覆盖更多组件。  
   > **优先级 P1**，评论 7，开发团队重点投入方向。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/issues/24353)

5. **#22745 – AST 感知的文件读取、搜索与映射研究**  
   > 探索通过抽象语法树精准读取方法边界、减少无效轮次、降低 Token 开销。  
   > **优先级 P2**，评论 7，有望提升代码库分析和编辑效率。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/issues/22745)

6. **#21968 – Gemini 不主动使用自定义技能和子代理**  
   > 用户反馈即使已有相关技能（如 Gradle、Git），Gemini 仍倾向自行执行命令，除非明确指示。  
   > **优先级 P2**，评论 6，用户体验痛点。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/issues/21968)

7. **#25166 – Shell 命令执行完成后仍显示“等待输入”**  
   > 极简单的命令（如 `ls`）执行完毕后，Gemini 仍认为命令活跃并挂起。  
   > **优先级 P1**，评论 4，👍 3，高频 Bug。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/issues/25166)

8. **#21983 – 浏览器子代理在 Wayland 下失败**  
   > 使用 Wayland 显示服务时，浏览器代理无法正常启动并报错。  
   > **优先级 P1**，评论 4，👍 1，Linux 用户的兼容性障碍。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/issues/21983)

9. **#26522 – 自动内存对低信号会话无限重试**  
   > 当提取代理判断某个会话“低信号”而跳过读取时，该会话不会被标记为已处理，导致后续无限次重试。  
   > **优先级 P2**，评论 5，影响内存系统效率。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/issues/26522)

10. **#22672 – 代理应阻止或劝阻破坏性行为**  
    > 模型有时会使用 `git reset --force`、`rm -rf` 等危险命令，建议在用户确认前先提示风险。  
    > **优先级 P2**，评论 3，👍 1，安全相关，社区呼声较高。  
    > [查看详情](https://github.com/google-gemini/gemini-cli/issues/22672)

---

## 重要 PR 进展（Top 10）

以下为过去 24 小时更新的 Pull Request，包含新功能、安全修复与核心改进。

1. **#28530 – feat(caretaker-evals): 添加分类评测框架与裁判运行器**  
   > 引入 LLM-as-a-Judge 评估流程，支持并行 Git Worktree 基准测试，用于 Caretaker Agent 的 Issue 分类管线。  
   > 标签：size/l，打开状态。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/pull/28530)

2. **#28532 – feat(caretaker-evals): 本地 golden issue 收集与 Firestore 同步工具**  
   > 提供 CLI 工具用于组装测试用例并同步至 Cloud Firestore，依赖 #28530。  
   > 标签：size/l，打开状态。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/pull/28532)

3. **#28531 – fix(a2a-server): 规范化 CRLF 换行符为 LF**  
   > 修复在 Windows 下 Gemini Code Assist 侧边栏 diff 视图无法高亮变更的问题。  
   > 标签：size/m，打开状态。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/pull/28531)

4. **#28509 – fix(core): 禁用上下文管理时过滤内省（thought）片段**  
   > 防止 Gemini 2.x 等模型的思维过程泄漏到历史记录中，导致重复推理块。  
   > 标签：size/m，已合并。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/pull/28509)

5. **#28523 – fix(core): 密钥链中强制显式标签长度与校验**  
   > 确保文件凭据存储使用标准 128-bit 标签长度并处理格式错误的数据。  
   > 标签：size/m，打开状态。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/pull/28523)

6. **#28517 – fix(core): 对 GoogleCredentialsAuthProvider 强制使用 HTTPS**  
   > 禁止通过明文 HTTP 传输 ADC 身份令牌，防止凭证泄漏。  
   > 标签：size/m，已合并。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/pull/28517)

7. **#28529 – feat(caretaker): 添加 Caretaker Agent GCP 部署脚本**  
   > 支持一键部署 Ingestion Service、Triage Worker Job 和 Egress Service 至 Cloud Run。  
   > 标签：size/m，打开状态。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/pull/28529)

8. **#28481 – fix(core): 使用存储的客户端 ID 刷新 MCP OAuth 令牌**  
   > 修复通过 HTTP 动态注册的 MCP 服务器在令牌刷新时因客户端 ID 丢失而失败的问题。  
   > 标签：security，size/m，打开状态。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/pull/28481)

9. **#28435 – feat(pr-generator-core): 环境配置解析器、命令执行器及 GitHub REST API 客户端**  
   > 为 Gemini CLI SSR 管线提供基础模块，支持子进程执行与结构化日志。  
   > 标签：size/l，打开状态。  
   > [查看详情](https://github.com/google-gemini/gemini-cli/pull/28435)

10. **#28526 – fix(vscode-ide-companion): 停止泄漏 disposables**  
    > 修复 `gemini.diff.accept` 命令和 `onDidChangeWorkspaceFolders` 事件监听器未正确注册导致的内存泄漏。  
    > 标签：core，size/s，打开状态。  
    > [查看详情](https://github.com/google-gemini/gemini-cli/pull/28526)

---

## 功能需求趋势

从过去 24 小时的 Issue 和 PR 中可以提炼出以下社区最关注的功能方向：

- **Agent 可靠性与自省**：用户期望代理能更准确报告执行状态（#22323）、更主动使用技能（#21968）、避免挂起（#21409）和内存无限重试（#26522）。
- **安全加固**：围绕凭证传输（强制 HTTPS #28517）、密钥存储长度校验（#28523）、OAuth 令牌刷新（#28481）、破坏性命令防护（#22672）等，安全修复呈批量涌现。
- **评测与质量保障**：组件级评估（#24353）、Caretaker Agent 分类评测框架（#28530/#28532）、AST 感知的代码理解（#22745）等项目显示开发团队在系统性提升 Agent 效果。
- **跨平台与 IDE 集成**：Wayland 兼容性（#21983）、Windows CRLF 问题（#28531）、VS Code 插件内存泄漏（#28526）表明社区对多桌面环境支持有较高需求。
- **沙箱与执行安全**：零依赖 OS 沙箱（#19873）持续被提及，期望能在不牺牲用户安全的情况下充分发挥模型的 Bash 能力。

---

## 开发者关注点

综合社区反馈，以下为高频痛点或急需解决的问题：

- **子 / 通用代理挂起与误报**：多个 P1 Bug 直指代理核心行为，用户被迫禁用子代理或手动干预。
- **Shell 命令执行卡死**：简单命令完成后仍显示“等待输入”，直接影响 CLI 基础流程。
- **浏览器代理在 Wayland 环境下不可用**：部分 Linux 发行版用户无法使用浏览器子代理。
- **自动内存低效与安全隐患**：无限重试低信号会话，且提取过程中先发送内容后再要求模型脱敏，存在隐私风险。
- **忽略自定义配置**：symlink 代理不被识别（#20079）、Browser Agent 忽略 `settings.json` 中的 `maxTurns`（#22267）。
- **MCP OAuth 刷新失败**：动态注册的服务器令牌刷新时会删除已有凭据，需反复重新认证。

---

*日报由 AI 自动生成，基于 github.com/google-gemini/gemini-cli 公开数据，仅供参考。*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 | 2026-07-25

## 今日速览

昨日发布了 **v1.0.75**，新增对 **Claude Opus 5** 的支持，进一步拓展了模型选择。社区反馈集中在 **plan-mode权限回归**（#4188）、**超大session恢复OOM**（#4251）以及 **插件系统持久化**（#4247）等关键问题，稳定性和可靠性成为开发者关注焦点。

---

## 版本发布

### v1.0.75（2026-07-24）
- **新增**：支持 **Claude Opus 5** 模型，用户可在 CLI 中调用该模型进行交互。

---

## 社区热点 Issues（Top 10）

1. **#1128 - [Feature Request] 添加 `awaitingUserInput` hook 类型**  
   👍 28 | 💬 5 | 开放中  
   **为何重要**：当前缺少“等待用户输入”的 hook，导致自动化流程无法准确感知 agent 状态。属于 **themeing/accessibility** 领域，社区需求强烈。  
   [查看](https://github.com/github/copilot-cli/issues/1128)

2. **#4188 - [Regression] plan-mode 拦截 shell 命令**  
   👍 3 | 💬 4 | 开放中  
   **为何重要**：plan 模式本应允许只读命令（如 `gh api`），但新版错误地阻止了这些操作，影响 CI/CD 和开发流程。  
   [查看](https://github.com/github/copilot-cli/issues/4188)

3. **#4163 - [Bug] 子进程僵尸累积（Linux）**  
   👍 3 | 💬 3 | 已关闭  
   **为何重要**：子进程未被正确回收，导致 PID 下僵尸进程堆积，影响系统资源。已修复（关闭），值得关注修复内容。  
   [查看](https://github.com/github/copilot-cli/issues/4163)

4. **#4183 - [Bug] 自动压缩无法阻止 CAPI 5MB 失败**  
   👍 10 | 💬 3 | 开放中  
   **为何重要**：长会话即使未超 token 限制，也可能因序列化请求体超 5MB 而永久卡死。属于 **context-memory** 核心机制缺陷。  
   [查看](https://github.com/github/copilot-cli/issues/4183)

5. **#3773 - [Bug] 浅色主题下文本对比度低**  
   👍 3 | 💬 3 | 开放中  
   **为何重要**：影响大量使用浅色主题的开发者的可读性，属于 **theming-accessibility**，长期存在未修复。  
   [查看](https://github.com/github/copilot-cli/issues/3773)

6. **#4251 - [Regression] 恢复大 session 时 OOM/单核 100% 达 70 分钟（v1.0.74）**  
   👍 0 | 💬 0 | 新提交  
   **为何重要**：性能严重退化，社区反馈 v1.0.73 正常，v1.0.74 内存暴涨 3-4 倍，属于 **triage** 紧急问题。  
   [查看](https://github.com/github/copilot-cli/issues/4251)

7. **#4247 - [Bug] plugin marketplace add 报告成功但未持久化**  
   👍 0 | 💬 0 | 新提交  
   **为何重要**：插件市场注册流程存在数据丢失，`list` 和后续操作找不到已添加的 marketplace，破坏插件生态。  
   [查看](https://github.com/github/copilot-cli/issues/4247)

8. **#4246 - [Bug] archive_session 超时导致工作区残留**  
   👍 0 | 💬 0 | 新提交  
   **为何重要**：大仓库工作区清理超时（60秒），残留不可恢复的 session 和磁盘占用，影响磁盘空间和分支复用。  
   [查看](https://github.com/github/copilot-cli/issues/4246)

9. **#4222 - [Regression] React/Ink 无限渲染循环回归（Windows）**  
   👍 0 | 💬 1 | 开放中  
   **为何重要**：v1.0.72+ 再次出现“主面板冻结/无输出”问题，曾修复于 #2802 后又复发，严重影响 Windows 用户。  
   [查看](https://github.com/github/copilot-cli/issues/4222)

10. **#4235 - [Regression] Ctrl+C 不再中断 agent 运行**  
  👍 0 | 💬 1 | 已关闭  
  **为何重要**：键盘中断失效，属于 **input-keyboard** 基本交互回归，虽已关闭但需关注修复策略。  
  [查看](https://github.com/github/copilot-cli/issues/4235)

---

## 重要 PR 进展

本阶段无新 PR 提交或更新（过去 24 小时内 PR 数据为 0）。

---

## 功能需求趋势

从近期的 Issues 中可以提炼出以下社区重点关注的功能方向：

- **计划模式下命令权限精细化**：多个 issue（#4188、#4220）反映 plan-mode 对只读命令的误判，要求支持更灵活的权限白名单或用户自定义规则。
- **上下文窗口与内存管理**： #4183 的 5MB 限制、#4251 的 OOM 问题，显示用户对长会话稳定性的渴求，需要更好的自动压缩、分片或离线持久化机制。
- **插件系统与 MCP 集成改进**：#4247 的持久化失败、#2247 的路径错误、#4234 的工作目录问题，说明插件安装、注册和运行时环境仍需打磨。
- **平台兼容性修复**：持续收到 Windows 终端渲染 (#4222)、Linux 复制剪贴板 (#4236) 以及原生进程管理 (#4163) 的投诉。
- **AI 模型扩展**：v1.0.75 添加 Claude Opus 5 支持，暗示社区期待更灵活的模型切换，同时 issue #4231 要求更智能的指令注入。

---

## 开发者关注点

综合社区反馈，当前开发者的主要痛点和高频需求包括：

1. **回归问题频发**：plan-mode 权限、Ctrl+C 中断、Windows 渲染循环等老问题反复出现，开发者对版本间的兼容性表示担忧。
2. **大型项目支持不足**：长 session 恢复 OOM、5MB 请求体限制、archive_session 超时，严重影响有大量工具调用的开发者。
3. **UI/UX 缺陷**：主题对比度 (#3773)、MCP 标签渲染一行一个字符 (#4238)、密码遮蔽浪费 token (#4241) 等细节问题削弱使用体验。
4. **调试与反馈缺失**：项目 session 隐藏失败原因 (#4144)、拒绝消息静默丢失 (#4237)，使得排查问题困难。
5. **文档与配置期望**：希望工作树更可配置 (#3675)、支持更多的 glob 模式 (#4231)、以及 SSH 别名识别 (#4248)。

---

*数据来源：GitHub `github/copilot-cli` 仓库，截至 2026-07-25 08:00 UTC。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 | 2026-07-25

## 今日速览
昨日（7月24日）Kimi CLI 无新版本发布，但社区活跃度回升：6个 Issues 获得更新，其中 **登录失败（#2556）** 和 **Windows 方向键无法使用（#2521）** 成为新痛点；同时一则关于 **A股量化 + AI Agent 实践（#2555）** 的讨论引发社区关注。3个 Pull Requests 也有进展，其中企业代理 SSL 支持（#762）和 MCP 日志路由修复（#1637）是长期未合并的老 PR 再次被推动。

---

## 社区热点 Issues

### 1. [#2556] kimi login fails（新上报）
**作者**: @moodmosaic | **创建**: 2026-07-24 | **评论**: 0 | **👍**: 0  
**摘要**: 用户刚购买 Vivace 订阅后，`kimi login` 在 Linux ARM64 上失败，怀疑是 OAuth 流程异常。  
**重要性**: 直接影响付费用户使用，需优先定位。  
[查看详情](https://github.com/MoonshotAI/kimi-cli/issues/2556)

### 2. [#2521] Windows 方向键无法选择选项
**作者**: @RambleRainbow | **创建**: 2026-07-20 | **更新**: 2026-07-24 | **评论**: 1 | **👍**: 0  
**摘要**: Windows 环境下的 `herdr`（推测为 Herder 或类似 TUI）中，使用方向键无法正常选择菜单项。  
**重要性**: 跨平台体验的关键问题，尤其影响 Windows 开发者。  
[查看详情](https://github.com/MoonshotAI/kimi-cli/issues/2521)

### 3. [#2326] VS Code Kimi Freezes
**作者**: @pctablet505 | **创建**: 2026-05-19 | **更新**: 2026-07-24 | **评论**: 3 | **👍**: 0  
**摘要**: VS Code 扩展频繁卡死，使用 kimi 2.6 模型时尤为明显，且存在其他多个问题。  
**重要性**: 已有超过2个月未解决，影响 IDE 集成体验。  
[查看详情](https://github.com/MoonshotAI/kimi-cli/issues/2326)

### 4. [#1282] 远程控制功能需求
**作者**: @CatKang | **创建**: 2026-02-27 | **更新**: 2026-07-24 | **评论**: 7 | **👍**: 16  
**摘要**: 用户希望能在手机/平板上继续本地 Kimi CLI 会话（类似 Remote Control），实现无缝切换。  
**重要性**: 获得16个👍，是近期需求最高的 Feature Request。  
[查看详情](https://github.com/MoonshotAI/kimi-cli/issues/1282)

### 5. [#1070] 登录失败：网络不可达（已关闭）
**作者**: @notedit | **创建**: 2026-02-09 | **更新**: 2026-07-24 | **评论**: 7 | **👍**: 0  
**摘要**: 因 `auth.kimi.com:443` 网络不可达导致登录失败，最终关闭（可能已修复）。  
**重要性**: 虽已关闭，但表明企业网络/代理问题仍是常见痛点。  
[查看详情](https://github.com/MoonshotAI/kimi-cli/issues/1070)

### 6. [#2555] 讨论：A股量化 + AI Agent 实践
**作者**: @yupeng012 | **创建**: 2026-07-24 | **评论**: 0 | **👍**: 0  
**摘要**: 用户分享基于 Hermes Agent 框架在 A 股市场的自主进化 Agent 实践，核心强调真实 PnL 反馈闭环和参数驱动。  
**重要性**: 虽非直接 Bug，但展示了 Kimi Agent 思路的金融应用潜力，可能启发 CLI 的 Agent 能力扩展。  
[查看详情](https://github.com/MoonshotAI/kimi-cli/issues/2555)

---

## 重要 PR 进展

### 1. [#762] fix: respect SSL_CERT_FILE env var for corporate proxy support
**作者**: @aaraujodata | **更新**: 2026-07-24 | **评论**: 0 | **👍**: 0  
**摘要**: 增加对 `SSL_CERT_FILE` 环境变量的支持，允许企业代理环境下使用 Kimi CLI 而不被 SSL 错误拦截。该 PR 自1月创建，昨日再次更新。  
**影响**: 解决企业用户长期痛点，但尚未合并。  
[查看详情](https://github.com/MoonshotAI/kimi-cli/pull/762)

### 2. [#1637] fix: route MCP server log notifications to loguru instead of TUI
**作者**: @he-yufeng | **更新**: 2026-07-24 | **评论**: 0 | **👍**: 0  
**摘要**: 将 MCP 服务器的日志通知从 TUI 界面中分离到 loguru（独立日志库），防止日志干扰交互界面。  
**影响**: 明显改善使用 MCP 工具（如 SearXNG）时的 TUI 整洁度。  
[查看详情](https://github.com/MoonshotAI/kimi-cli/pull/1637)

### 3. [#2554] fix(tools): count StrReplaceFile replacements against running content
**作者**: @ayaangazali | **更新**: 2026-07-23 | **评论**: 0 | **👍**: 0  
**摘要**: 修复 `StrReplaceFile` 工具的成功计数逻辑——之前统计的是原始内容中的匹配数，现在按实际替换后的运行内容计数。  
**影响**: 提升文件编辑工具的一致性。  
[查看详情](https://github.com/MoonshotAI/kimi-cli/pull/2554)

---

## 功能需求趋势
从所有 Issues 中可提炼出三大社区关注方向：

1. **跨设备协作** – #1282 远程控制功能获得最高支持，表明用户渴望在不同设备上延续对话。  
2. **企业级网络兼容** – #1070（已关闭）和 #762（PR）均指向 SSL 证书/代理问题，企业环境使用仍是短板。  
3. **Agent 能力外延** – #2555 的量化 Agent 讨论，以及 #1282 中提到的“继续本地会话”，均暗示用户希望 Kimi CLI 具备更强的自主任务延续和调度能力。

---

## 开发者关注点
- **登录体验脆弱**：新版 #2556 登录失败问题（ARM64平台、OAuth）值得警惕，尤其在刚完成订阅付费后。  
- **Windows 平台 TUI 兼容性**：方向键失效（#2521）提示开发者优先排查终端渲染库（如 Herder）的跨平台适配。  
- **IDE 集成稳定性**：#2326 VS Code 扩展卡死已存在两月，社区反馈有多个子问题，建议团队优先修复。  
- **MCP 工具集成防干扰**：PR #1637 的思路受到关注，开发者普遍希望 MCP 背景日志不要污染主界面。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-07-25

## 📋 今日速览

v1.18.5 补丁发布，重点修复了 Claude 自适应思考、OpenAI 响应处理、grep 符号链接路径保留等核心问题。社区方面，一个高赞（188👍）的「自动发现 OpenAI 兼容 Provider 模型」需求成为讨论焦点，同时多起关于 Agent 无故停止、任务挂起及 TUI 崩溃的稳定性报告引发广泛关注。PR 侧涌现一批自动化清理合并，涉及 MCP OAuth 安全加固、Provider 配置扁平化重构等基础设施改进。

---

## 🚀 版本发布：v1.18.5

- **核心修复**
  - 改进 Claude 自适应思考（Adaptive Thinking）处理，覆盖更多响应形状
  - 规避 OpenAI Responses 阶段处理可能导致的对话中断
  - 搜索时保留 grep 符号链接路径（感谢 @remixz）
  - 保留 Mistral 推理历史跨轮次连贯性
  - 稳定 Mistral 整体交互

---

## 🔥 社区热点 Issues（10 条）

1. **[#6231] Auto-discover models from OpenAI-compatible provider endpoints**  
   - 用户需手动在 `opencode.json` 中列出本地 provider（如 LM Studio、Ollama）的所有模型，频繁变动时极其繁琐。提议自动探测模型列表。
   - 188👍 / 32 条评论 | [GitHub](https://github.com/anomalyco/opencode/issues/6231)

2. **[#38195] 401 AuthError: Request blocked by upstream provider**  
   - Go 订阅用户在所有 Go 模型中遭遇 401 错误，免费模型正常。涉及 Desktop 和 Hermes 等多端复现。严重影响付费用户。
   - 17👍 / 21 条评论 | [GitHub](https://github.com/anomalyco/opencode/issues/38195)

3. **[#24316] Progress halts with qwen 3.6 35b-a3b with naked tool call**  
   - 使用 Qwen 3.6 模型时，代理输出裸 `<tool_call>` 后停止响应，需手动干预。可能涉及 llama.cpp 或 OpenCode 本身。
   - 2👍 / 19 条评论 | [GitHub](https://github.com/anomalyco/opencode/issues/24316)

4. **[#31932] [FEATURE]: Cross-project session list / picker for TUI**  
   - 当前 `/sessions` 局限在当前项目，跨仓库工作时无法统一管理会话。提议在 TUI 中增加全局会话选择器。
   - 5👍 / 13 条评论 | [GitHub](https://github.com/anomalyco/opencode/issues/31932)

5. **[#25038] Long-running shell commands hang even after “BUILD SUCCESSFUL”**  
   - Gradle 等长时命令执行完毕后，OpenCode 进程不再响应，界面卡死。Android 构建场景常见。
   - 9👍 / 11 条评论 | [GitHub](https://github.com/anomalyco/opencode/issues/25038)

6. **[#25130] opencode jumping into a difference language**  
   - 使用 Big Pickle 模型时，回复突然切换为其他语言（非中文/英文），影响使用体验。
   - 0👍 / 10 条评论 | [GitHub](https://github.com/anomalyco/opencode/issues/25130)

7. **[#6479] opencode reads agents.md from parent directories**  
   - 启动时意外读取上级目录的 `agents.md`，可能导致配置污染。版本 1.0.208 中已存在。
   - 0👍 / 10 条评论 | [GitHub](https://github.com/anomalyco/opencode/issues/6479)

8. **[#18654] [FEATURE]: To be able to remove or change email in OpenCode Zen**  
   - 用户更改 GitHub 邮箱后，OpenCode Zen 中出现重复用户，且无法编辑/删除已有邮箱。账户管理缺陷。
   - 12👍 / 6 条评论 | [GitHub](https://github.com/anomalyco/opencode/issues/18654)

9. **[#38749] agent keeps stopping abruptly**  
   - Agent 在任务执行中频繁无端停止，需要手动输入“continue”继续。影响生产效率。
   - 0👍 / 4 条评论 | [GitHub](https://github.com/anomalyco/opencode/issues/38749)

10. **[#38690] [2.0] TUI crash: undefined is not an object (evaluating 'f.part.state.content[0]')**  
    - TUI 会话索引页渲染时内核崩溃，错误指向 `part.state.content` 为空。影响部分用户正常使用。
    - 0👍 / 4 条评论（已关闭）| [GitHub](https://github.com/anomalyco/opencode/issues/38690)

---

## 🔧 重要 PR 进展（10 条）

1. **[#35195] fix(session): preserve agent and model on async prompt without explicit fields**  
   - 修复异步提示（async prompt）时丢失 agent 和 model 选择的问题，确保配置一致性。
   - [GitHub](https://github.com/anomalyco/opencode/pull/35195)

2. **[#33725] fix(opencode): secure manual MCP OAuth callback**  
   - 增强 MCP 手动 OAuth 回调安全：要求 state 参数并原子校验/消费，防止重放攻击。
   - [GitHub](https://github.com/anomalyco/opencode/pull/33725)

3. **[#33724] fix(opencode): reconnect closed remote MCP clients**  
   - 支持在传输层 `onclose` 后自动重连远程 MCP 客户端，采用有界指数退避与世代隔离机制。
   - [GitHub](https://github.com/anomalyco/opencode/pull/33724)

4. **[#33722] fix(mcp): isolate OAuth request headers**  
   - 将 MCP 配置的请求头限制在资源请求和同源元数据发现中，防止泄漏至跨域中间件。
   - [GitHub](https://github.com/anomalyco/opencode/pull/33722)

5. **[#33715] fix(mcp): make oauth callback startup atomic**  
   - OAuth 回调监听器直接绑定 `127.0.0.1`，避免先探测再绑定的竞争条件，修复 `EADDRINUSE` 问题。
   - [GitHub](https://github.com/anomalyco/opencode/pull/33715)

6. **[#33700] fix(tui): expand pasted text placeholders literally**  
   - TUI 中粘贴文本占位符（如 `[Pasted ~N lines]`）之前替换失败，现在正确展开原始内容。
   - [GitHub](https://github.com/anomalyco/opencode/pull/33700)

7. **[#33697] refactor(schema): flatten provider identity**  
   - 重构 schema，将 `AISDK | Native` 联合类型统一为扁平 `package` 标识，简化 provider 配置覆盖逻辑。
   - [GitHub](https://github.com/anomalyco/opencode/pull/33697)

8. **[#33689] feat(llm): add native provider packages**  
   - 实现统一的 `model(id, settings)` provider 包合约，覆盖 OpenAI、Anthropic、Amazon Bedrock 等模块。
   - [GitHub](https://github.com/anomalyco/opencode/pull/33689)

9. **[#33684] fix(session): finalize assistant finish on aborted tool input**  
   - 修复流被中断后（`tool-input-start` 后无 `tool-call`），`halt()` 未正确完成 assistant 消息报错的问题。
   - [GitHub](https://github.com/anomalyco/opencode/pull/33684)

10. **[#33680] fix(acp): omit directory paths from ToolCallLocation**  
    - 修复 ACP 协议中 shell/grep 等工具的输出包含目录路径的问题，使其符合 `ToolCallLocation.path` 规范。
    - [GitHub](https://github.com/anomalyco/opencode/pull/33680)

---

## 📊 功能需求趋势

- **自动模型发现**：用户强烈期望 OpenCode 能自动探测本地 OpenAI 兼容 Provider 的模型列表，减少手动配置开销（#6231，188👍）。
- **跨项目会话管理**：多仓库开发场景缺乏统一的会话查看/切换界面，提议在 TUI 中新增全局会话选择器（#31932）。
- **UI/UX 增强**：要求显示每次工具调用的耗时与回合时长（#38666），以及改善粘贴文件路径行为（#34006）。
- **新模型/Provider 支持**：社区积极寻求集成 GPT-5.6 系列（#38722）、Crof AI（#24636）、Ling 3.0 Flash 等模型。
- **实验性功能**：`research` 命令提案（#35496）希望将实验循环作为一等公民，支持自动化假设→测量→日志→保留/丢弃。

---

## 🧑‍💻 开发者关注点

- **Agent 稳定性**：多起报告称 Agent 无故停止、需要不断输入“continue”才能继续执行（#38749、#38731、#38766），成为当前最影响效率的痛点。
- **认证与网络错误**：付费用户遭遇 401 AuthError（#38195）、“Upstream request failed”（#37231）等，指向上游 Provider 的认证或网络问题。
- **长命令挂起**：Gradle/构建类长时命令执行后 OpenCode 僵死（#25038），社区呼吁改善子进程退出检测。
- **TUI / Desktop 崩溃**：版本 2.0 预览版 TUI 因 `content[0]` 为空崩溃（#38690），Desktop 端也报告频繁闪退（#38736）。
- **模型配置继承**：背景子代理通知后手动选择的模型被静默重置为默认（#38770），以及 agent 读取父目录的 `agents.md` 文件（#6479），均反映配置管理不够严谨。
- **Windows 兼容性**：子进程启动时控制台窗口闪烁（#38715），以及路径粘贴行为不一致（#34006），Windows 用户的使用体验有待提升。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 (2026-07-25)

---

## 1. 今日速览

- **v0.21.0 正式发布**，新增 Web Shell Composer 工具栏的工作区选择器（切换/添加工作区），标志着 Web 客户端交互体验的一次重要升级。
- **DSW SWE-bench 全量测试管道持续迭代**，多个 POC 版本（Run 2/3/4 及异步模式）在隔离环境中完成 500 例评测，当前结果被标记为“QUARANTINED”，社区 CI 验证正趋于成熟。
- **社区活跃度攀升**：过去 24 小时新增 31 条 Issue 和 50 条 PR，涉及 MCP 集成、TUI 渲染、冷启动性能、子代理模型选择等多个方向，P2 级 Bug 密集涌现。

---

## 2. 版本发布

### 🚀 v0.21.0 (正式版)

- **发布说明**: [Release v0.21.0](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.0)
- **主要变更**:
  - `feat(web-shell):` 在 Composer 工具栏中添加工作区选择器按钮，支持下拉切换/新增工作区 ([#7390](https://github.com/QwenLM/qwen-code/issues/7390)).
- **破坏性变更**: 无

### 🌙 夜间版 & 试验版本

| 标记 | 说明 |
|------|------|
| `v0.20.1-nightly.20260724.7d17c44a3` | 包含 daemon 指标初始化顺序测试及性能优化。 |
| `dsw-swe-full-poc-20260724-*` (共 4 个) | 针对 PR #7656 的隔离 SWE-bench 验证管道输出（500 例全部完成），结果均为 “QUARANTINED”，非正式发布。 |
| `dsw-swe-full-async-poc-20260724-*` (共 3 个) | 异步全量 POC，部分结果显著不同（一次仅 12 resolved / 8 unresolved），显示异步模式下评测一致性仍需打磨。 |

---

## 3. 社区热点 Issues (Top 10)

1. **#5800** – [Bug: CLI TUI 静态模式下长回复最后一行被覆盖](https://github.com/QwenLM/qwen-code/issues/5800)
   - **缘由**: 当助手回复高度超过终端时，完成瞬间最后一行消失。影响所有使用默认 Static 渲染的用户。
   - **社区**: 7 条评论，作者 @MikeWang0316tw 详细描述了复现步骤，已标注 `welcome-pr`。

2. **#7485** – [Bug: `qwen resume` 后出现大面积空白](https://github.com/QwenLM/qwen-code/issues/7485)
   - **缘由**: 恢复会话后最后一条消息与输入提示之间出现大片空白。
   - **社区**: 6 条评论，已关闭（疑似修复中），但仍值得关注 TUI 布局稳定性。

3. **#7147** – [Bug: MCP 服务器无法获取工具和资源列表](https://github.com/QwenLM/qwen-code/issues/7147)
   - **缘由**: 使用 Fastmail MCP 服务器时认证通过但工具列举超时，导致 MCP 功能完全失效。
   - **社区**: 6 条评论，用户 @imrehg 提供了详细日志，已关闭但问题可能仍影响其他 MCP 服务。

4. **#7684** – [Bug: macOS 下 Command 模式多行 statusline 输入法候选框位置错误](https://github.com/QwenLM/qwen-code/issues/7684)
   - **缘由**: 状态栏多行时输入法光标远离实际位置，严重影响中文输入体验。
   - **社区**: 5 条评论，附带截图，标注 `scope/macos`，对 Mac 用户至关重要。

5. **#7264** – [增强: 冷启动延迟跟踪 – ACP 惰性加载候选](https://github.com/QwenLM/qwen-code/issues/7264)
   - **缘由**: 基于 esbuild 审计发现 ACP 子进程静态导入 17.24 MiB / 2420 模块，全部在 `initialize` 前解析，导致冷启动延迟。
   - **社区**: 5 条评论，已标记 `priority/P2`，开发者 @doudouOUC 提供了详细分析。

6. **#7631** – [Bug: AcpBridge xterm.js 解析错误](https://github.com/QwenLM/qwen-code/issues/7631)
   - **缘由**: 微信频道终端出现大量 `[AcpBridge] xterm.js: Parsing error`，终端交互被破坏。
   - **社区**: 5 条评论，用户 @Varorbc 提供了详细错误栈，对 WeChat 渠道影响大。

7. **#7687** – [功能请求: DingTalk 频道支持出站图片发送](https://github.com/QwenLM/qwen-code/issues/7687)
   - **缘由**: 目前 agent 无法将本地图片（截图、图表）通过钉钉频道发送，只能返回文件路径。
   - **社区**: 4 条评论，作者 @qqqys 提出明确的实现方案，`priority/P3`。

8. **#6835** – [Bug: `/insight` 报告 UTC vs 本地时间不一致](https://github.com/QwenLM/qwen-code/issues/6835)
   - **缘由**: 热力图、连续天数、活跃小时等统计基础不统一，导致非 UTC 用户数据错误。
   - **社区**: 4 条评论，作者 @chinesepowered 提供详细分析，标注 `need-discussion`。

9. **#4252** – [功能请求: `/stats` 增加生成时间指标 (TPS / TTFT)](https://github.com/QwenLM/qwen-code/issues/4252)
   - **缘由**: 用户希望了解实时生成性能（Tokens Per Second, Time-To-First-Token），便于优化选路。
   - **社区**: 4 条评论，自 5 月 17 日起持续活跃，近期仍有更新。

10. **#7697** – [Bug: VSCode 扩展中无法连接 Unity MCP，而 Claude Code 可以](https://github.com/QwenLM/qwen-code/issues/7697)
    - **缘由**: 用户尝试在 VSCode 中使用 Unity MCP 失败，但同一环境下的 Claude Code 正常。
    - **社区**: 3 条评论，涉及跨平台集成兼容性，`status/need-information`。

---

## 4. 重要 PR 进展 (Top 10)

1. **[#7656] – CI: 添加隔离的 DSW SWE-bench 发布管道**  
   - 作者 @DennisYu07，全新异步流水线：GitHub Release → DSW 分发 → PostgreSQL 队列 → 10 台 Harbor 执行器 → SWE 评分 → OSS → 原 Release 更新。
   - 这是 SWE-bench 验证自动化的基础设施基石，今日多个 POC 版本均源于此。

2. **[#7695] – fix(web-shell): 启用工作树会话的 Changes/History 对话框**  
   - 作者 @wenshao，修复 Web Shell 中 git 相关对话框对工作树（worktree）的禁用问题，现支持 `/diff`、`/log` 等功能。

3. **[#7680] – perf(web-shell): git 分支状态缓存，实现即时绘制**  
   - 作者 @wenshao，daemon 侧增加 per-workspace 缓存，使 git branch chip 在 Web Shell 中几乎瞬间展示。

4. **[#7669] – fix(core): 为后台 shell 添加状态 sidecar**  
   - 作者 @ComplexSimply，解决后台命令输出文件为空时模型错误重启的问题：在输出文件旁生成 `.status` JSON 文件，记录 PID、exit code 等。

5. **[#7692] – feat(review): 审核前检测 head 漂移并封顶 verdict**  
   - 作者 @wenshao，`presubmit` 新增检测 PR head 在审核过程中是否前进，若前进则标记为 `DRIFTED`，避免基于过时代码做出错误判断。

6. **[#7632] – feat(channels): GitHub 通知轮询适配器 (notification-as-wakeup)**  
   - 作者 @OrbitZore，支持通过 GitHub API 轮询通知并响应 @mention，实现频道级的 Issue/PR 评论交互。

7. **[#7683] – feat(web-shell): 添加只读 GitHub Pull Requests 面板**  
   - 作者 @wenshao，在 Git 对话框中增加 PR 列表标签页，显示标题、分支、审核状态、CI 图标等，并支持 `/prs` 斜杠命令。

8. **[#7678] – fix(core): 允许读取已保存的 plan 文件无需确认**  
   - 作者 @zjunothing，将 `~/.qwen/plans` 目录添加至免权限读取根路径，优化计划文件读取流程。

9. **[#7651] – perf(core): 系统提示重排：易变 auto-memory 段放最后**  
   - 作者 @DragonnZhang，参照 Hermes Agent 三层布局（稳定→上下文→易变），将自动记忆指令始终置于提示末尾，改善模型注意力。

10. **[#7694] – fix(acp): 每轮 prompt 结束后清理 review worktree 租约**  
    - 作者 @wenshao，修复取消审核后残留工作树和分支的问题，通过服务端 sweep 确保 `qwen-review/pr-<n>` 被清理。

---

## 5. 功能需求趋势

从近 24 小时 Issue/PR 中提炼出社区最关注的五大方向：

1. **MCP / 外部工具集成**  
   - 代表 Issue: #7147 (Fastmail MCP 超时), #7697 (Unity MCP 与 VSCode 兼容), #7631 (xterm.js 解析错误)。  
   - 趋势: 用户希望 Qwen Code 能与更多第三方 MCP 服务器无缝协作，暴露的集成 bug 成为近期修复焦点。

2. **Web Shell / 图形化交互增强**  
   - 代表 PR: #7695 (工作树对话框), #7680 (git chip 缓存), #7683 (PR 面板), #7390 (工作区选择器)。  
   - 趋势: 团队正大力提升 Web Shell 的 Git 可视化和会话管理能力，对标 IDE 级体验。

3. **多 Agent / 子代理能力**  
   - 代表 Issue: #7685 (子代理模型等级选择), #7679 (QWEN.md 禁令被覆盖)。  
   - 趋势: 用户希望精细控制子代理的模型规格、工具权限，同时避免不必要的自动 spawn。

4. **频道扩展 (DingTalk, WeChat, GitHub)**  
   - 代表 Issue: #7687 (钉钉出站图片), #7590 (微信频道无法使用), PR #7632 (GitHub 轮询适配器)。  
   - 趋势: 社区期待更多通讯渠道的深度集成，尤其是图片/文件传输、事件驱动。

5. **性能与资源管理**  
   - 代表 Issue: #7264 (冷启动惰性加载), #4252 (生成时间指标), #7658 (流限时重试延迟硬编码)。  
   - 趋势: 开发者和用户共同关注系统资源占用、启动延迟、API 限流处理的可配置性。

---

## 6. 开发者关注点

| 痛点/高频需求 | 涉及 Issue | 描述 |
|---------------|------------|------|
| **TUI 渲染兼容性** | #5800 (末行覆盖), #7485 (resume 空白), #7684 (输入法光标), #7634 (WSL 重复渲染) | 不同终端环境下的渲染 bug 频发，尤其是 macOS 输入法、WSL、Windows Terminal。 |
| **MCP 连接稳定性** | #7147, #7697 | 认证后超时、不同 MCP 服务器兼容性问题，需要统一错误处理框架。 |
| **后台任务监控** | #7626 (后台 shell 空文件导致误判), #7669 (sidecar 方案) | 后台长时间运行命令的输出缓冲问题，模型因空文件误认为任务已完成。 |
| **配置灵活性** | #7658 (重试延迟不可配置), #7679 (QWEN.md 被覆盖) | 用户希望覆盖硬编码行为（如限流等待）、以及系统提示优先级控制。 |
| **多平台差异** | #7684 (macOS), #7634 (WSL), #7697 (VSCode) | 不同操作系统/编辑器上表现不一致，统一性需提升。 |
| **插件/扩展 ID 冲突** | #7676 (同一仓库扩展 ID 唯一性) | 两个来自同一仓库的插件因 ID 相同导致冲突，现 PR #7676 已修复。 |

---

*数据来源: [github.com/QwenLM/qwen-code](https://github.com/QwenLM/qwen-code) | 生成时间: 2026-07-25T00:00 UTC+8*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*