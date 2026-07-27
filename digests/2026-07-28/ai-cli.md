# AI CLI 工具社区动态日报 2026-07-28

> 生成时间: 2026-07-27 23:30 UTC | 覆盖工具: 7 个

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

# AI CLI 工具生态横向对比分析报告（2026-07-28）

---

## 1. 生态全景

当前 AI CLI 工具整体处于“功能爆发与稳定性修补并行”的阶段。所有主流工具均在加速推出新模型、多代理架构及 IDE 集成，但用户对**计费透明度、Windows 平台兼容性、Agent 行为可靠性**的投诉急剧上升。社区参与度极高，高频 Bug 和功能请求集中在配额管理、权限安全、子代理生命周期控制及插件系统健壮性上。同时，MCP（Model Context Protocol）生态正在成为各工具竞相适配的核心接口，但安全漏洞和兼容性挑战也随之暴露。

---

## 2. 各工具活跃度对比

| 工具 | 热点 Issues（选取数） | PR（实质更新数） | 版本 Release（24h内） | 社区评论总量（估算） | 核心关注领域 |
|------|-------------------|----------------|-----------------------|------------------|--------------|
| **Claude Code** | 10 | 5 | 0 | 约 90 条 | 计费混乱、Windows崩溃、权限控制 |
| **OpenAI Codex** | 10 | 10 | 2（alpha.12, .13） | 约 120 条 | 配额重置失效、子代理超额、多账户需求 |
| **Gemini CLI** | 10 | 10 | 1（nightly） | 约 70 条 | Agent 假成功/挂起、MCP OAuth、沙箱安全 |
| **Copilot CLI** | 10（实际列出10个） | 8 | 1（v1.0.76-0） | 约 40 条 | plan-mode回归、僵尸进程、Autopilot持久化 |
| **Kimi Code CLI** | 4 | 4 | 0 | 约 11 条 | Windows编码崩溃、VSCode弹窗/钩子GC |
| **OpenCode** | 10 | 10 | 2（v1.18.6/7） | 约 70 条 | UI冻结、粘贴展开、用量追踪、Agent循环 |
| **Qwen Code** | 10 | 10 | 4（2 nightly + 2预发布） | 约 50 条 | MCP授权绕过、长上下文ECONNRESET、E2E CI失败 |

**简评**：OpenAI Codex 与 Claude Code 讨论热度最高，Gemini CLI 和 OpenCode 修复节奏快，Kimi Code 社区最小但关键 Bug 正在被快速修复。

---

## 3. 共同关注的功能方向

| 共同方向 | 涉及工具 | 具体诉求 |
|----------|---------|---------|
| **计费/配额透明度与可靠性** | Claude Code, OpenAI Codex, Qwen Code | 显示可用模型与实际套餐是否一致；Reset 机制无效；子代理超额消耗；429 静默重试导致预算耗尽 |
| **Windows 平台稳定性** | Claude Code, OpenAI Codex, Gemini CLI, Kimi Code | 桌面应用崩溃（GPU进程退出）；输入延迟；MSIX注册失败；编码问题（GBK/UTF-8）；后台服务不可卸载 |
| **MCP 安全与兼容** | Claude Code, Gemini CLI, OpenCode, Qwen Code | MCP 工具绕过用户授权（#7768/#7769）；OAuth令牌刷新失败；工具 Schema 归一化；拒绝列表过滤 |
| **子代理/Agent 可靠性** | Claude Code, OpenAI Codex, Gemini CLI, OpenCode, Qwen Code | 子代理假成功（MAX_TURNS误报）、挂起、过度消耗资源、无法与用户交互（#7835）、工具调用循环 |
| **IDE 集成（VS Code）稳定性** | Claude Code, OpenAI Codex, Kimi Code, Qwen Code | Diff 崩溃、审批弹窗不渲染、连接失败、路径不可点击 |
| **权限与安全控制** | Claude Code, Qwen Code, OpenCode | 域级别浏览器权限割裂、AI 读取敏感文件、分支保护绕过、Electron 安全配置强化 |

---

## 4. 差异化定位分析

| 工具 | 功能侧重 | 目标用户 | 技术路线特点 |
|------|----------|---------|-------------|
| **Claude Code** | 模型策略与计费一体化体验；插件系统扩展性 | 重度付费用户、团队协作场景 | 强调 Max 计划与模型（Fable 5）深度绑定；Cowork 后台服务；丰富的插件钩子系统 |
| **OpenAI Codex** | 多代理编排（子代理、spawn_agent）；配额精细化控制 | 自动化开发者、CI/CD 集成者 | 强 Rust 客户端；多架构配置（V1/V2 兼容）；ACP 非交互模式 |
| **Gemini CLI** | Agent 安全沙箱（macOS Seatbelt、零依赖OS沙箱）；模型原生 Bash 亲和 | 安全敏感型开发者、Linux 用户 | 深度整合 Gemini 3 模型原生能力；组件级自动化评估（EPIC #24353） |
| **Copilot CLI** | Autopilot 模式与 Git 工作流深度绑定；计划/执行分离 | GitHub 生态用户、日常 CLI 辅助 | 与 GitHub Copilot 订阅强关联；plan-mode 只读设计；MCP 工具缓存优化 |
| **Kimi Code CLI** | VSCode 扩展体验；中文环境兼容性 | 国内开发者、VSCode 重度用户 | 专注于解决 Windows 中文编码、扩展弹窗渲染、钩子生命周期；Moonshot API 定制 |
| **OpenCode** | 桌面端 TUI 与项目会话管理；粘贴交互增强 | 桌面端重度用户、项目管理场景 | 原生桌面应用（Electron）；项目路径与会话持久化；统一用量追踪诉求 |
| **Qwen Code** | 长上下文稳定性；安全漏洞快速修复；Web Shell 集成 | 高负载代码生成用户、安全研究社区 | SWE-bench 高认证率（75.2%）；Goal v3 状态持久化；GitHub 通知分发 |

---

## 5. 社区热度与成熟度

- **最活跃（高热度+高频更新）**：**OpenAI Codex** 与 **Claude Code**。两者均拥有大量付费用户，Bug 报告和功能请求质量高，开发节奏快（Codex 每日 alpha 发布；Claude Code 社区自主提交修复 PR）。
- **中等活跃（修复与开发并进）**：**Gemini CLI**、**OpenCode**、**Qwen Code**。Gemini 正在系统级加固（沙箱、MCP 安全）；OpenCode 桌面端稳定性修复集中；Qwen 安全漏洞被快速关闭（#7768 已修复）但 CI 稳定性堪忧。
- **相对稳定但仍有痛点**：**Copilot CLI**。Release 周期较长（v1.0.76-0），社区反馈集中在计划模式回归和 Autopilot 持久化，整体成熟度较高但功能迭代速度偏慢。
- **快速起步阶段**：**Kimi Code CLI**。社区规模小，但 PR 和 Issue 质量高（编码兼容、扩展弹窗），正在解决早期用户的核心阻塞问题，潜力可期。

**成熟度排序（主观）**：Copilot CLI > Claude Code > OpenAI Codex > Gemini CLI > OpenCode > Qwen Code > Kimi Code CLI。

---

## 6. 值得关注的趋势信号

1. **计费与配额管理成为用户体验的“卡点”**  
   Claude Code 的 Fable 5 计费显示混乱、Codex 的 Reset 失效、Qwen 的 429 静默重试——这些事件表明，随着模型复杂性增加，**“我能用哪个模型？会花多少钱？”** 已成为用户最迫切的透明性需求。开发者应要求工具提供实时、可靠的计量面板，并区分瞬时限流与永久配额耗尽。

2. **Windows 平台正在拖累 AI CLI 的普及**  
   几乎所有工具都报告了 Windows 专属的崩溃、输入延迟、编码问题、后台服务无法关闭等 Bug。Windows 用户占比极高，但产品测试和适配明显滞后。**跨平台一致性是下一阶段竞争关键**，尤其是中文环境下的编码兼容性（Kimi 的修复预示了这点）。

3. **Agent 自主性与安全护栏的矛盾激化**  
   - Qwen Code 的 MCP 授权绕过（#7768/#7769）  
   - Claude Code 的浏览器权限割裂（#78315）  
   - Gemini CLI 的子代理假成功（#22323）  
   - Copilot CLI 的 plan-mode 回归（#4188）  

   这些事件揭示了一个深层问题：**用户既希望 Agent 高效自动执行，又恐惧其越权**。未来会出现更细粒度的“域级别权限模型”和“沙箱内执行审计”，MCP 协议本身也需要增加强制授权层。

4. **长上下文场景下的网络与稳定性挑战**  
   Qwen Code 的 ECONNRESET（#7831）、Gemini CLI 的自动记忆无限重试（#26522）、OpenAI Codex 的子代理磁盘飙升（#34061）——当会话超 150k tokens 时，网络中断、内存泄漏、重试逻辑缺陷集中爆发。**上下文压缩、分页加载、断线重试**将成为必备能力。

5. **多账户与认证持久性需求从“希望”变为“刚需”**  
   OpenAI Codex 的 #20500（多账户支持）获 90👍，Claude Code 的 #70115（认证路由失败）长期存在。随着用户将 AI CLI 嵌入工作流，**一个工具绑定多个身份（个人/企业）** 以及 **单点登录（SSO）的稳定集成** 将决定其企业级可用性。

6. **IDE 扩展的可靠性正在赶超 CLI 原生体验**  
   VS Code 扩展的 Diff 崩溃（Codex #35058）、审批弹窗不渲染（Kimi #2563）、连接失败（Qwen #6414）——当 IDE 集成成为主要使用方式时，其稳定性直接影响用户忠诚度。**CLI 与 IDE 扩展功能对等且互不依赖** 是不可逆的趋势。

7. **安全报告的“白帽化”**  
   Qwen Code 的安全漏洞由第三方研究者 @rishavkumar-thecoder 报告并附带了完整 PoC，随后被快速关闭。这表明**独立安全研究者正在成为 AI CLI 质量保障的重要力量**，工具方应建立漏洞赏金或致谢机制。

---

**总结**：AI CLI 工具已从“尝鲜期”进入“实用期”，用户对稳定、透明、安全的诉求远超新功能速度。能在计费一致性、Windows 兼容性、Agent 权限审计上率先突破的工具，将赢得下一阶段的核心用户群。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截止 2026-07-28）

## 1. 热门 Skills 排行

### 🥇 #1298 — fix(skill-creator): run_eval.py 修复（评论数最高）
- **功能**：修复 `run_eval.py` 始终报告 recall=0% 的核心缺陷，包含 Windows 流读取、触发检测和并行 worker 修复
- **讨论热点**：社区对此高度关注（关联 #556、#1169 等多个 issue），因为描述优化循环长期在噪声上运行，严重影响所有 skill 开发者的工作效率
- **状态**：⚠️ Open（6月23日最后更新）
- **链接**：https://github.com/anthropics/skills/pull/1298

### 🥈 #514 — Add document-typography skill（文档排版质量）
- **功能**：检测 AI 生成文档中的孤字换行、寡妇段落、编号错位等排版问题，覆盖 Claude 生成的每一份文档
- **讨论热点**：社区认同这是高频痛点——用户很少主动要求排版优化，但问题普遍存在
- **状态**：⚠️ Open（3月13日最后更新）
- **链接**：https://github.com/anthropics/skills/pull/514

### 🥉 #486 — Add ODT skill（OpenDocument 格式支持）
- **功能**：支持 .odt/.ods 文件的创建、填充、读取和 HTML 转换，适配 LibreOffice 及 ISO 标准格式
- **讨论热点**：社区对办公文档格式的支持需求强烈，尤其是开源生态用户
- **状态**：⚠️ Open（4月14日最后更新）
- **链接**：https://github.com/anthropics/skills/pull/486

### #1367 — feat(skills): add self-audit（自我审计 v1.3.0）
- **功能**：交付前机械文件验证 + 四维推理质量审计（按损害严重性排序），声称通用适配任何项目/模型
- **讨论热点**：关注 AI 输出质量控制，社区在 #1385 中进一步提出三阶段质量门流水线提案
- **状态**：⚠️ Open（7月2日最后更新）
- **链接**：https://github.com/anthropics/skills/pull/1367

### #723 — Add testing-patterns skill（测试模式）
- **功能**：覆盖完整测试栈——测试奖杯模型、AAA 模式、React 组件测试、命名约定
- **讨论热点**：社区对结构化测试指导需求明确，尤其是"测什么 vs 不测什么"的决策边界
- **状态**：⚠️ Open（4月21日最后更新）
- **链接**：https://github.com/anthropics/skills/pull/723

### #525 — Add pyxel skill（复古游戏开发）
- **功能**：为 Pyxel 复古游戏引擎添加 MCP 服务器集成，支持编写→运行→迭代的工作流
- **讨论热点**：社区对创造性/娱乐性 skill 持积极态度，但讨论相对温和
- **状态**：⚠️ Open（7月15日最后更新，最新活跃）
- **链接**：https://github.com/anthropics/skills/pull/525

### #1479 — Add plan-file-hygiene skill（规划文件卫生）
- **功能**：解决规划制品积累无生命周期的问题（关联 #1417），管理代理规划文件的生命周期
- **讨论热点**：社区在 issue 中已明确定义问题框架，协作氛围积极
- **状态**：⚠️ Open（7月27日最后更新，最新 PR）
- **链接**：https://github.com/anthropics/skills/pull/1479

---

## 2. 社区需求趋势

从热门 Issues 中提炼的五大需求方向：

| 需求方向 | 代表 Issue | 核心诉求 |
|---------|-----------|---------|
| **🔒 安全与信任治理** | #492（43评论） | 社区 skill 在 `anthropic/` 命名空间下的信任边界滥用，要求改进分发机制 |
| **🏢 企业级协作** | #228（16评论） | 组织内 skill 共享需手动下载/上传，缺少直接分享链接或共享库 |
| **🛠 skill-creator 工具链稳定** | #556（12评论）、#1061、#1169 | 触发检测失败、Windows 兼容性、UTF-8 编码——构成开发体验最大瓶颈 |
| **📦 去重与管理** | #189（6评论） | `document-skills` 和 `example-skills` 安装重复内容，浪费上下文窗口 |
| **📐 上下文窗口优化** | #1487（4评论） | `claude-api` skill 单次注入 ~156k tokens，耗尽上下文，需懒加载或分片 |

**额外关注**：#1329 提出的 compact-memory（符号化记忆压缩）代表社区对长会话上下文优化的新需求方向。

---

## 3. 高潜力待合并 Skills

以下 PR 评论活跃、功能完整且社区期待度高，有较大概率在近期落地：

### 🏆 #514 — document-typography（文档排版质量）
- **社区价值**：直接影响所有 Claude 生成文档的终端用户体验
- **成熟度**：功能定义清晰、触发条件明确，无重大争议
- **落地概率**：⭐⭐⭐⭐
- **链接**：https://github.com/anthropics/skills/pull/514

### 🏆 #486 — ODT skill（OpenDocument 格式）
- **社区价值**：填补办公文档生态的明显空白，覆盖 LibreOffice 等开源工具链用户
- **成熟度**：功能范围定义完整（创建+填充+读取+转换），讨论焦点在技术实现细节
- **落地概率**：⭐⭐⭐
- **链接**：https://github.com/anthropics/skills/pull/486

### 🏆 #1367 — self-audit（自我审计 v1.3.0）
- **社区价值**：AI 输出质量控制是跨领域通用需求，#1385 提案正在推进第二、第三阶段
- **成熟度**：已有明确版本号和功能分层，但尚待 merge 审查
- **落地概率**：⭐⭐⭐
- **链接**：https://github.com/anthropics/skills/pull/1367

### 🏆 #1479 — plan-file-hygiene（规划文件卫生）
- **社区价值**：直击长会话代理的规划制品堆积问题，与 compact-memory 形成互补
- **成熟度**：最新的 PR（7月25日），协作氛围好，但尚需时间审查
- **落地概率**：⭐⭐⭐
- **链接**：https://github.com/anthropics/skills/pull/1479

### 🏆 #723 — testing-patterns（测试模式）
- **社区价值**：填补 Claude Code 测试指导的结构化空白，被开发者的高频场景
- **成熟度**：内容覆盖面广但尚处于早期讨论阶段
- **落地概率**：⭐⭐
- **链接**：https://github.com/anthropics/skills/pull/723

---

## 4. Skills 生态洞察

**当前社区最集中的诉求是：提升 skill-creator 工具链的稳定性和跨平台兼容性（Windows 支持、触发检测、UTF-8 编码），同时拓展 skill 生态的覆盖范围（排版质量、办公格式、质量审计）和组织协作能力（共享、安全治理）。** 本质上，社区正在经历从"技能实验期"向"生产化部署期"的过渡——人们不再满足于创建技能，而是要求它们可靠运行、可团队共享、可质量控制。

---

好的，这是根据您提供的 GitHub 数据生成的 2026 年 7 月 28 日 Claude Code 社区动态日报。

---

# Claude Code 社区动态日报 | 2026-07-28

## 📰 今日速览

1.  **Fable 5 计费混乱持续发酵**：围绕新模型 Fable 5 在 Max 计划下的计费问题成为社区最热焦点，用户反馈最多的问题在于平台错误地将其标记为“需消耗使用积分”，即便用户已订阅最高等级的 Max 套餐。
2.  **Windows 桌面端稳定性告急**：多个关于 Claude Desktop 在 Windows 系统上崩溃的 Bug 报告涌现，其中浏览器面板（Browser Pane）的闪退问题影响广泛，GPU 进程持续异常退出。
3.  **多项关键 Bug 修复 PR 提交**：社区贡献者针对 DevContainer 防火墙、插件路径引用和文档链接等关键问题提交了修复 PR，显示出社区在提升产品稳定性和易用性方面的积极参与。

## 🐛 社区热点 Issues

> 从过去 24 小时更新的高热度 Issues 中，我们选取了 10 个最值得关注的动态。

1.  **[#79337]** **Fable 5 在 Max 计划中错误提示“需要积分”** 🟠热议中
    - **摘要**：自 Fable 5 成为 Max 计划的标准配置后，部分 Max 用户在使用时被错误地提示“需要消耗使用积分”，并强制降级到 Opus 4.8。该问题严重影响了付费用户的权益，社区反响强烈。
    - **作者**：@otnixX | 评论：47 | 👍：16
    - **链接**：[查看 Issue](https://github.com/anthropics/claude-code/issues/79337)

2.  **[#81703]** **7月17日计费事故：计划内额度被错误扣除积分** 🆕
    - **摘要**：用户反馈在 Anthropic 确认的 7月17日计费系统故障中，其 Max 计划的免费额度被错误地计入了付费积分，并产生了高达 $704.71 的争议费用。社区期待官方对此事件进行妥善处理。
    - **作者**：@COOLak | 评论：5 | 👍：0
    - **链接**：[查看 Issue](https://github.com/anthropics/claude-code/issues/81703)

3.  **[#81275]** **Windows 桌面版打开浏览器面板导致应用崩溃** 🆕
    - **摘要**：Claude Desktop for Windows 的最新 MSIX 版本（）在打开内置浏览器面板时，会因 Chromium GPU 进程崩溃（退出代码 `101457950`）而导致整个应用闪退。该问题在 Intel、NVIDIA 甚至软件渲染模式下均会复现。
    - **作者**：@oleksiiskrypka | 评论：5 | 👍：0
    - **链接**：[查看 Issue](https://github.com/anthropics/claude-code/issues/81275)

4.  **[#57371]** **要求提供禁用 Cowork 后台服务的方法** 🟠热议中
    - **摘要**：许多 Windows 用户因不使用 Cowork 功能，但 Claude Desktop 会强制后台启动 `CoworkVMService` 服务而困扰。社区强烈希望官方提供一个开关，允许用户禁用此项功能以节省系统资源。
    - **作者**：@itutar | 评论：15 | 👍：39
    - **链接**：[查看 Issue](https://github.com/anthropics/claude-code/issues/57371)

5.  **[#78315]** **浏览器“读取工具”不遵循“允许的站点”白名单** 🟠热议中
    - **摘要**：用户反映，在 Desktop 浏览器面板中，导航到“允许的站点”列表中的域名后，读取页面内容、屏幕截图等后续操作仍被提示“需要每次授权”，与导航行为不一致，严重影响了使用流程。
    - **作者**：@strickdd | 评论：6 | 👍：3
    - **链接**：[查看 Issue](https://github.com/anthropics/claude-code/issues/78315)

6.  **[#76002]** **VS Code 扩展中“AskUserQuestion”对话框无法用回车提交** 🟠热议中
    - **摘要**：在 VS Code 的 Claude Code 扩展中，当 AI 发起一个问题，用户选择“其他”并输入文本后，按回车键无法提交，必须手动点击“提交”按钮，这是一个破坏操作流畅性的交互 Bug。
    - **作者**：@James9688 | 评论：1 | 👍：0
    - **链接**：[查看 Issue](https://github.com/anthropics/claude-code/issues/76002)

7.  **[#54418]** **macOS 上无法使用 `/advisor` 命令**
    - **摘要**：macOS 用户报告名为 `advisor` 的内置功能或命令无法使用，该问题自4月起存在，近期再次被标记为活跃。这表明部分核心功能在特定平台上可能存在兼容性或实现问题。
    - **作者**：@zxjrc3mrmr | 评论：7 | 👍：2
    - **链接**：[查看 Issue](https://github.com/anthropics/claude-code/issues/54418)

8.  **[#70700]** **Windows Server 2025 更新破坏 MSIX 注册** 🟠热议中
    - **摘要**：一个特定的 Windows Server 2025 累积更新（KB5094125）导致 Claude Desktop 的 MSIX 包部署状态异常，即便显示部署成功，实际应用仍处于“需要修复”状态。这指向了与 Windows 底层包管理系统的不兼容问题。
    - **作者**：@erngab | 评论：4 | 👍：0
    - **链接**：[查看 Issue](https://github.com/anthropics/claude-code/issues/70700)

9.  **[#66488]** **工具搜索排名错误导致 Claude 找不到工具** 🟠热议中
    - **摘要**：一个关键的 Bug，当用户拥有大量工具（如 MCP 服务器）时，Claude 的工具检索排名算法出现错误，即使工具名称完全匹配，Claude 也可能无法找到并调用它，严重削弱了其 Agent 能力。
    - **作者**：@opcode81 | 评论：5 | 👍：6
    - **链接**：[查看 Issue](https://github.com/anthropics/claude-code/issues/66488)

10. **[#70115]** **Max 订阅用户反复遭遇认证路由失败** 🟠热议中
    - **摘要**：付费的 Max 用户反映，反复出现通过 Magic Link 或 OAuth 登录后，被错误地导向“创建账户”页面，导致无法在网页、桌面和 CLI 上正常使用。该问题已被用户标记为长期存在的后端认证路由故障。
    - **作者**：@0xiao7 | 评论：2 | 👍：0
    - **链接**：[查看 Issue](https://github.com/anthropics/claude-code/issues/70115)

## 🔧 重要 PR 进展

> 以下是在过去 24 小时内提交或更新的 5 个重要 PR。

1.  **[#81673]** **修复：DevContainer 防火墙设置因 DNS 解析失败而中断**
    - **摘要**：修复了 `init-firewall.sh` 脚本在配置防火墙时，如果允许列表中的某个域名无法解析（如 `statsig.anthropic.com`），整个脚本会因 `set -e` 机制报错退出，导致防火墙规则不完整的 Bug。该 PR 确保了单个域名解析失败不会阻断整体配置。
    - **作者**：@ozdemirsarman
    - **链接**：[查看 PR](https://github.com/anthropics/claude-code/pull/81673)

2.  **[#81672]** **修复：hookify 插件安装路径依赖问题**
    - **摘要**：修复了 `hookify` 插件的导入机制，使其不依赖于插件目录被命名为 `hookify`。此前，如果插件通过市场安装（目录名可能不同），会导致导入失败。此 PR 解决了插件包与目录名的解耦问题。
    - **作者**：@ozdemirsarman
    - **链接**：[查看 PR](https://github.com/anthropics/claude-code/pull/81672)

3.  **[#81670]** **修复：插件钩子命令因路径包含空格而失效**
    - **摘要**：修复了两个相关的 Bug：一是 `hooks.json` 中的命令未对 `${CLAUDE_PLUGIN_ROOT}` 变量进行引号包裹，导致插件路径包含空格时命令执行失败；二是为 hookify 示例添加了正确的路径前缀。这是一个提升插件系统稳定性的重要修复。
    - **作者**：@ozdemirsarman
    - **链接**：[查看 PR](https://github.com/anthropics/claude-code/pull/81670)

4.  **[#81576]** **文档：修复 plugins/README.md 中关于 security-guidance 插件描述**
    - **摘要**：社区贡献者发现 `plugins/README.md` 对 `security-guidance` 插件的描述不准确。实际插件的钩子数量和监控的模式数量与文档中的描述都不相符，此 PR 对文档进行了修正，提高了文档的准确性。
    - **作者**：@Woohyeon-Hong
    - **链接**：[查看 PR](https://github.com/anthropics/claude-code/pull/81576)

5.  **[#81500]** **修复：AWS 网关示例中的 404 文档链接**
    - **摘要**：修复了 `examples/gateway/aws` 目录下所有指向 `code.claude.com` 的文档链接，这些链接目前均返回 404 错误。此 PR 确保了示例的可用性和引导性。
    - **作者**：@yazansalhi
    - **链接**：[查看 PR](https://github.com/anthropics/claude-code/pull/81500)

## 💡 功能需求趋势

从近期的 Issues 和讨论中，可以提炼出以下几个社区最关注的功能方向：

1.  **模型策略与计费透明度**：围绕新模型（如 Fable 5）的计费显示不一致问题十分突出。社区强烈要求“显示可用模型与计费策略”的功能，确保 UI 层、计费层和模型层的信息完全同步，避免误导用户。
2.  **IDE 集成优化 (VS Code)**：VS Code 扩展的用户体验正在成为焦点。需求包括修复对话框交互（如回车提交）、提升“AskUserQuestion”等消息类型的响应速度，以及与 VS Code 原生功能的深度集成。
3.  **权限与安全控制**：用户对 AI Agent 的自主权限越来越关注。社区希望提供更细粒度的控制，例如：可配置的“域级别”浏览器权限（区分导航与读取操作）、阻止 AI 读取敏感文件（如 shell 配置文件）的明确指令、以及防止 AI 绕过分支保护等安全措施。
4.  **插件系统与扩展性**：随着插件生态的发展，社区对插件系统的健壮性提出了更高要求。趋势是改进插件安装路径（不再依赖固定目录名）、增强路径引用的鲁棒性（处理空格、特殊字符）、以及提供更清晰的文档来指导插件开发和使用。
5.  **桌面端稳定性和资源控制**：Windows 和 Mac 桌面客户端的稳定性 Bug 报告频发。用户强烈期望官方能“修复应用崩溃问题”，尤其是与内嵌浏览器、GPU 进程相关的问题，并提供关闭非必要后台服务（如 Cowork）的能力。

## 🧑‍💻 开发者关注点

总结开发者在社区反馈中的几个关键痛点和高频需求：

*   **计费显示混乱**：用户无法信任 `/model` 命令显示的计费信息，它与实际使用情况不符。开发者需要一个可靠且统一的界面来了解“我有哪些模型可用？”以及“这个模型是否在我的套餐内？”。
*   **权限设置的割裂感**：用户对一个域名的权限设置（如“允许”）无法在所有操作上生效。开发者希望权限模型是完整且一致的，而不是需要为同一个域名在不同操作（如导航 vs. 读取）上重复授权。
*   **跨平台兼容性问题**：Windows 用户面临更多的平台特定 Bug，例如 MSIX 注册失败、桌面应用崩溃、后台服务不可卸载等。这表明产品在 Windows 平台的测试和适配仍需加强。
*   **认证持久性不足**：付费用户频繁遭遇“登出”或被导向“注册”页面，导致需要反复登录。认证令牌的持久性和后台服务的稳定性是影响高粘性用户的关键因素。
*   **AI 自主行为的不可预测性**：用户担心 AI Agent 会忽略显式指令（如“不要读取我的 shell 配置”）或执行未经授权的敏感操作（如合并代码）。社区呼吁更强的“安全护栏”和更明确的自主操作边界。
*   **插件安装的脆弱性**：当插件目录路径包含空格或非标准名称时，插件会失效。这暴露了插件系统在处理基础文件系统特性时的不足，开发者期望一个更健壮的安装和加载机制。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

好的，以下是基于您提供的 GitHub 数据生成的 2026-07-28 OpenAI Codex 社区动态日报。

---

# OpenAI Codex 社区动态日报 | 2026-07-28

## 📰 今日速览

昨日 Codex 团队发布了两个针对 Rust 客户端的 Alpha 版本，主要修复了 Windows 平台下的进程中断与执行延迟问题。社区方面，关于 **配额/速率限制** 的投诉持续升温，多个高热度 Issue 指出 Reset 机制不生效以及子代理过度消耗配额的问题。此外，多账户支持与 VS Code 扩展的 Diff 崩溃问题依旧是社区呼声最高的两大待办事项。

## 🚀 版本发布

-   **rust-v0.146.0-alpha.13**: 最新 Rust 客户端 alpha 版本。本次发布紧随前一版本，很可能包含了对 `0.146.0-alpha.12` 中已知问题的紧急修复。
    -   [查看 Release](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.13)

-   **rust-v0.146.0-alpha.12**: 昨日的 Rust 客户端 alpha 版本。结合今日合并的 PR 来看，该版本可能已启动对 Windows 非 TTY 进程中断、执行延迟优化等底层问题的修复工作。
    -   [查看 Release](https://github.com/openai/codex/releases/tag/rust-v0.146.0-alpha.12)

## 🔥 社区热点 Issues

1.  **[#31606] Reset 机制存在严重 Bug，导致配额浪费与功能失效**
    -   **热度**: 👍 61 | 💬 52
    -   **状态**: 开放中
    -   **重要性**: **极高**。用户报告执行 Reset 后，不仅未能恢复状态，反而白白消耗了宝贵的 Reset 次数。这直接影响了用户对 Codex 核心配额管理机制的信任，是整个社区最关心的问题。
    -   [查看详情](https://github.com/openai/codex/issues/31606)

2.  **[#35058] VS Code 扩展中的 Codex Diff 功能完全崩溃，无法使用**
    -   **热度**: 👍 48 | 💬 20
    -   **状态**: 开放中
    -   **重要性**: **极高**。Codex Diff 是开发者进行代码审查和更改预览的核心功能。该问题导致 macOS 上的 VS Code 用户完全无法使用此功能，严重阻碍了工作流，是社区中呼声极高的待修复 Bug。
    -   [查看详情](https://github.com/openai/codex/issues/35058)

3.  **[#32683] Windows 版桌面应用在“浏览器使用”功能中频繁崩溃**
    -   **热度**: 👍 8 | 💬 27
    -   **状态**: 开放中
    -   **重要性**: **高**。此问题涉及核心功能“Computer Use”中的浏览器操作，崩溃发生在 `chrome.dll` 中，影响范围大，对 Windows 用户的使用体验有显著负面影响。
    -   [查看详情](https://github.com/openai/codex/issues/32683)

4.  **[#20500] 社区强烈要求为同一应用连接多个账户**
    -   **热度**: 👍 90 | 💬 20
    -   **状态**: 开放中
    -   **重要性**: **高**。这是目前社区投票最高的功能请求。用户希望在一个 Codex 工作会话中，能同时访问和管理多个不同账号（如个人 Gmail、企业 Gmail），而无需反复切换全局账户。
    -   [查看详情](https://github.com/openai/codex/issues/20500)

5.  **[#35097] 子代理模型兼容性问题：`gpt-5.6-luna` 被新代理架构拒绝**
    -   **热度**: 👍 5 | 💬 3
    -   **状态**: 开放中
    -   **重要性**: **高**。该问题揭示了Codex在代理系统版本兼容性上的缺陷。当一个模型被标记为旧版 (V1) 时，新版 (V2) 的 `spawn_agent` 指令会直接拒绝它，尽管该模型可能依然能良好运行，限制了用户的选择。
    -   [查看详情](https://github.com/openai/codex/issues/35097)

6.  **[#35463] Codex 子代理一夜之间耗尽整周配额，使用量统计存在严重 Bug**
    -   **热度**: 👍 0 | 💬 3
    -   **状态**: 开放中
    -   **重要性**: **高**。与 #31606 类似，此问题同样指向了配额管理的核心缺陷。子代理超额消耗配额导致用户第二天无法使用，这是一个严重的“成本失控”Bug，对 Pro 用户影响巨大。
    -   [查看详情](https://github.com/openai/codex/issues/35463)

7.  **[#34061] 子代理功能导致 Codex 客户端磁盘空间使用异常飙升**
    -   **热度**: 👍 1 | 💬 14
    -   **状态**: 开放中
    -   **重要性**: **中**。用户反馈子代理在运行时会生成大量临时的日志或缓存数据，迅速耗尽磁盘空间。这是一个性能与存储管理的关键问题，影响长时间、复杂的开发任务。
    -   [查看详情](https://github.com/openai/codex/issues/34061)

8.  **[#34450] Windows 版应用输入延迟和界面卡顿严重**
    -   **热度**: 👍 1 | 💬 3
    -   **状态**: 开放中
    -   **重要性**: **中**。用户报告在 Windows 上启动应用和输入时体验极差，严重影响日常使用。这表明桌面应用的性能优化，尤其是在 Windows 平台，仍有很大的提升空间。
    -   [查看详情](https://github.com/openai/codex/issues/34450)

9.  **[#35352] Windows 桌面应用因嵌入式浏览器 GPU 进程崩溃而意外退出**
    -   **热度**: 👍 0 | 💬 12
    -   **状态**: 开放中
    -   **重要性**: **中**。该问题描述了应用在基于 GPU 的渲染失败后，未能优雅地降级或恢复，而是直接崩溃退出。这是典型的鲁棒性问题，影响了核心功能的可用性。
    -   [查看详情](https://github.com/openai/codex/issues/35352)

10. **[#24268] Windows + WSL 混合环境下插件缓存路径解析错误**
    -   **热度**: 👍 3 | 💬 10
    -   **状态**: 开放中
    -   **重要性**: **中**。对于大量使用 WSL 进行开发的 Windows 用户，此 Bug 导致插件无法正常加载。这是一个较为隐蔽的环境兼容性问题，但随着 WSL 用户的增多，其影响范围不容忽视。
    -   [查看详情](https://github.com/openai/codex/issues/24268)

## 🛠️ 重要 PR 进展

1.  **[#35670] 提升 Windows 下执行命令的最小等待时间至 10 秒**
    -   **重要性**: **高**。这是一个针对 Windows 平台的性能修复。通过提高 `exec` 操作的 yield 时间下限，旨在减少在慢速系统上不必要的上下文切换和资源争用，从而提升响应稳定性。
    -   [查看详情](https://github.com/openai/codex/pull/35670)

2.  **[#35655] 修复 Windows 非 TTY 进程的中断问题**
    -   **重要性**: **高**。此 PR 修复了一个关键的终端兼容性问题。此前，在 Windows 上未绑定终端 (non-TTY) 的执行会话无法通过 `Ctrl-C` 中断，导致用户无法停止失控的进程。此修复是 `v0.146.0-alpha.12` 发布的重要依据。
    -   [查看详情](https://github.com/openai/codex/pull/35655)

3.  **[#35656] 维护多代理设置在不同配置表示形式间的兼容性**
    -   **重要性**: **高**。这是一个架构层面的修复。它确保了以布尔值 (V1) 和结构化表 (V2) 两种方式保存的 `multi_agent` 配置在系统升级或配置合并时不会相互覆盖或丢失，保证了代理功能的无缝过渡。
    -   [查看详情](https://github.com/openai/codex/pull/35656)

4.  **[#35649] TUI 输入在终端焦点返回时不再丢失**
    -   **重要性**: **高**。此 PR 修复了一个影响终端界面的长期Bug。当终端窗口失去焦点再返回时，用户输入的字符可能被丢弃。此修复通过缓存启动时的调色板信息，避免了焦点事件阻塞输入循环，提升了 TUI 的使用流畅度。
    -   [查看详情](https://github.com/openai/codex/pull/35649)

5.  **[#35661] 优化开发者指令中的技能优先级排序**
    -   **重要性**: **中**。此 PR 调整了系统提示词 (prompt) 的结构，将 `host_skills`（宿主技能）部分放在权限指令之前。这能确保模型更优先地关注和执行特定的宿主环境能力，优化了指令的理解与执行效率。
    -   [查看详情](https://github.com/openai/codex/pull/35661)

6.  **[#35623] 独立解析 Claude 和 Cursor 的会话记录**
    -   **重要性**: **中**。这项改进增强了导入外部工具 (Claude、Cursor) 会话的兼容性。通过分离解析逻辑，可以更准确地处理不同工具的特定上下文记录 (如 Cursor 的 `<cursor_commands>` 标签)，提升会话导入的质量和准确性。
    -   [查看详情](https://github.com/openai/codex/pull/35623)

7.  **[#35644] 增强线程恢复的健壮性：即使部分文件丢失也能继续**
    -   **重要性**: **中**。此 PR 提升了 Codex 在恢复会话时的容错能力。当某些滚动的历史文件无法找到时，应用将跳过这些文件，并继续从数据库中恢复其他有效线程，而不是直接失败，提升了数据恢复的成功率。
    -   [查看详情](https://github.com/openai/codex/pull/35644)

8.  **[#35621] 优化 `exec` 恢复时的 Token 消耗**
    -   **重要性**: **中**。此 PR 在恢复 `exec` 指令执行后的会话时，通过 `excludeTurns` 参数避免了重复计算已消耗的 Token。这对于 Pro 等按量计费用户来说，是一项重要的成本优化。
    -   [查看详情](https://github.com/openai/codex/pull/35621)

9.  **[#35668] 暴露网络代理配置接口**
    -   **重要性**: **中**。此 PR 将内部网络代理的规范 (spec) 构造函数公开，使得外部组件或插件可以更容易地集成或覆盖 Codex 的网络代理策略，增强了系统的可扩展性。
    -   [查看详情](https://github.com/openai/codex/pull/35668)

10. **[#35671] 根据认证模式动态路由插件**
    -   **重要性**: **中**。此 PR 允许 Codex 为不同认证来源（如 ChatGPT 账户、API Key 或远程服务）提供不同的推荐插件列表。这为构建更精细、更安全的插件生态系统奠定了基础。
    -   [查看详情](https://github.com/openai/codex/pull/35671)

## 📊 功能需求趋势

1.  **多账户管理 (Multi-Account Support)**: 社区中最强烈的声音。以 Issue #20500 和 #30418 为代表，用户希望在一个 Codex 会话中同时操作多个不同平台的账号（如 Gmail, GitHub）。这已成为阻碍许多工作流自动化的最大瓶颈。
2.  **配额与成本控制优化 (Quota & Cost Control)**: #31606 和 #35463 事件表明，用户对 Reset 不生效、子代理超额消耗等配额管理问题极为敏感。这不仅是 Bug，更是对用户体验和信任度的重大打击。
3.  **性能与稳定性 (Performance & Stability)**: Windows 平台的崩溃 (#32683, #35352)、输入延迟 (#34450) 以及子代理的磁盘占用 (#34061) 是当前性能优化的核心痛点。社区期望 Codex 能有更低的资源消耗和更稳定的运行表现。
4.  **IDE 集成深度 (IDE Integration)**: VS Code 扩展的 Codex Diff 崩溃 (#35058) 引发了大量关注。这表明开发者对在 IDE 中嵌入的 Codex 功能（如 Diff、代码解释）有着很高的稳定性和可用性要求。
5.  **MCP 与身份验证 (MCP & Auth)**: #35006 号 Issue 提出了为 MCP (Model Context Protocol) 构建可靠的企业 SSO OAuth 生命周期的需求，显示了 Codex 正在向更复杂、更正式的企业级应用场景演进。

## 👁️ 开发者关注点

-   **Windows 用户的“被抛弃感”**: 大量高热度 Bug (如崩溃、输入延迟、沙箱问题) 都集中在 Windows 平台。开发者对 Windows 版本的稳定性和性能优化表达了强烈不满，这是当前最需要关注的痛点。
-   **配额系统的信任危机**: Reset 失败 (#31606) 和子代理超额消耗 (#35463) 直接触动了用户的“钱包”。开发者急需官方解释和修复，以重建对配额管理系统的信任。
-   **功能有效性与 Bug 修复的优先级**: 社区普遍认为，相比于增加新功能，修复“Reset 不生效”、“Diff 崩溃”这类让核心功能不可用的 Bug 应优先处理。用户希望得到的是“能用”且“稳定”的产品。
-   **对复杂系统的“黑盒”担忧**: #35097 号 Issue (子代理模型兼容性问题) 揭示了内部系统架构变更可能对用户已习惯的功能产生影响。开发者希望能有更清晰的变更日志和降级/兼容方案，而不是“无法使用”这种硬性限制。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

好的，这是根据您提供的 GitHub 数据生成的 2026 年 7 月 28 日 Gemini CLI 社区动态日报。

---

# Gemini CLI 社区动态日报 — 2026-07-28

## 今日速览

尽管 `v0.54.0-nightly` 例行发布，但社区焦点集中在 Agent 可靠性上。多个高优先级的 Bug 报告指出，子代理在达到最大执行轮次时错误地报告任务成功，甚至发生“挂起”或无视用户配置自主运行的情况。安全与稳定性方面，本周有多项重要 PR 试图修复 macOS 下的沙箱启动崩溃、MCP OAuth 令牌刷新失败以及 HTTP 认证头冲突等问题。

## 版本发布

- **v0.54.0-nightly.20260727.g3818efbbf**: 最新的夜间构建版本已发布。
  - **Changelog**: https://github.com/google-gemini/gemini-cli/compare/v0.54.0-nightly.20260726.g3818efbbf...v0.54.0-nightly.20260727.g3818efbbf

## 社区热点 Issues（Top 10）

1.  **[Subagent recovery after MAX_TURNS is reported as GOAL success, hiding interruption] (https://github.com/google-gemini/gemini-cli/issues/22323)**
    - **重要性**: **核心 Bug**。子代理在达到最大交互轮次后，本应被识别为中断，却错误地报告为“成功”和“达成目标”。这会严重误导用户，隐藏任务失败的真相。
    - **社区反应**: 评论数达 12 条，开发者正在积极讨论根因和修复方案，属于 P1 优先级的 Bug。

2.  **[Generalist agent hangs] (https://github.com/google-gemini/gemini-cli/issues/21409)**
    - **重要性**: **阻塞性 Bug**。当 CLI 调用通用（Generalist）子代理时，整个任务会“挂起”无响应，包括创建文件夹这样的简单操作。这导致核心功能无法使用。
    - **社区反应**: 获得 8 个 👍，评论 8 条。用户反馈需要手动指定“不使用子代理”才能规避，是影响用户体验的关键问题。

3.  **[Leverage model's bash affinity via Zero-Dependency OS Sandboxing & Post-Execution Intent Routing] (https://github.com/google-gemini/gemini-cli/issues/19873)**
    - **重要性**: **前瞻性特性**。提出利用 Gemini 3 模型原生擅长 Bash 操作的特点，通过“零依赖”的沙箱机制来增强安全性和意图路由。这是社区对 AI 安全执行环境的深度思考。
    - **社区反应**: P2 优先级，获得 8 条评论，说明社区对原生 Bash 能力和安全沙箱的结合很感兴趣。

4.  **[Robust component level evals](https://github.com/google-gemini/gemini-cli/issues/24353)**
    - **重要性**: **质量保障基石**。这是一个 EPIC，旨在建立组件级别的自动化评估体系，确保 Agent 的每个组成部分（如代码搜索、浏览器操作）都能得到独立、可靠的测试。
    - **社区反应**: P1 优先级，有 7 条评论。表明团队正在系统性地提升 Agent 质量，这是长期健康的信号。

5.  **[Assess the impact of AST-aware file reads, search, and mapping] (https://github.com/google-gemini/gemini-cli/issues/22745)**
    - **重要性**: **技术趋势**。探讨引入抽象语法树感知的文件读取和搜索能力。这能极大提高代码理解的精度，减少 API 调用次数和 Token 消耗，是 Agent 能力进化的关键方向。
    - **社区反应**: P2 优先级，评论 7 条，点赞 1 个，社区认同其在减少噪音和精确导航方面的潜力。

6.  **[Gemini does not use skills and sub-agents enough] (https://github.com/google-gemini/gemini-cli/issues/21968)**
    - **重要性**: **智能调度缺陷**。模型明明有自定义技能和子代理可用，却很少主动调用。用户反馈即使任务高度相关，模型也需要显式指令才会使用。这表明模型的元认知和工具选择能力需要大幅提升。
    - **社区反应**: P2 Bug，6 条评论。这是一个有关“智能”度的核心痛点，直接关系到工具的实用性。

7.  **[Stop Auto Memory from retrying low-signal sessions indefinitely] (https://github.com/google-gemini/gemini-cli/issues/26522)**
    - **重要性**: **资源与逻辑问题**。自动记忆功能会无限重试处理低质量会话，导致资源浪费和处理循环卡死。这暴露了后台 Agent 处理逻辑的健壮性不足。
    - **社区反应**: P2 Bug，5 条评论。社区担忧此问题会导致后台任务处理堆积和性能下降。

8.  **[Shell command execution gets stuck with "Waiting input" after command completes] (https://github.com/google-gemini/gemini-cli/issues/25166)**
    - **重要性**: **常见体验问题**。Shell 命令执行完毕后，CLI 却显示仍在“等待输入”并卡死。这严重破坏了工作流的连续性和对自动化脚本的信任。
    - **社区反应**: P1 重要 Bug，获得 3 个 👍，4 条评论，表明这是个高频复现且令人沮丧的问题。

9.  **[Model frequently creates tmp scripts in random spots] (https://github.com/google-gemini/gemini-cli/issues/23571)**
    - **重要性**: **工作流污染**。模型倾向于在项目各处创建临时脚本，造成工作区混乱，影响版本管理和代码整洁度。
    - **社区反应**: P2 Bug，3 条评论。这是一个典型的“聪明但乱来”的问题，开发者希望模型行为更规范。

10. **[Browser subagent fails in wayland] (https://github.com/google-gemini/gemini-cli/issues/21983)**
    - **重要性**: **兼容性问题**。浏览器子代理在 Wayland 显示服务器上故障，直接影响了 Linux 用户的体验。
    - **社区反应**: P1 优先级，4 条评论。这是 Linux 平台用户面临的典型痛点，影响面较广。

## 重要 PR 进展（Top 10）

1.  **[fix(cli): fall back to embedded macOS seatbelt profiles if missing] (https://github.com/google-gemini/gemini-cli/pull/28551)**
    - **功能**: **关键修复**。解决 macOS 沙箱模式下，因缺少 Seatbelt 配置文件导致 CLI 启动崩溃的严重问题。通过内嵌配置文件作为后备方案，保证了核心功能可用。
    - **状态**: 新提交，Open。

2.  **[fix(core): refresh MCP OAuth tokens with the stored client ID] (https://github.com/google-gemini/gemini-cli/pull/28481)**
    - **功能**: **安全修复**。修复了 MCP OAuth 令牌刷新失败的问题，该问题会导致已配置的 MCP 服务器需要反复重新认证。
    - **状态**: 已更新，Open。

3.  **[fix(cli): add gemini-3.5-flash to model selector for all users] (https://github.com/google-gemini/gemini-cli/pull/28485)**
    - **功能**: **新模型支持**。允许所有用户在模型选择器中选用 `gemini-3.5-flash` 和 `gemini-3.6-flash` 新模型，解决了部分用户无法选择新模型的限制。
    - **状态**: 已更新，Open。

4.  **[fix(core): enforce explicit tag length and validation in file keychain] (https://github.com/google-gemini/gemini-cli/pull/28523)**
    - **功能**: **安全加固**。为基于文件的安全凭证存储（File Keychain）强制执行明确的认证标签长度和验证逻辑，提高加密存储的健壮性和跨运行时兼容性。
    - **状态**: 已合并/关闭。

5.  **[fix(mcp): disclose that Plan Mode read-only status is a server claim] (https://github.com/google-gemini/gemini-cli/pull/28549)**
    - **功能**: **安全透明性**。Plan Mode 的只读状态依赖于 MCP 服务器自身的声明。此 PR 修复了 CLI 不进行验证的问题，并改进了相关信息披露，防止恶意服务器绕过限制。
    - **状态**: 新提交，Open。

6.  **[fix(core): strip Authorization header when using GEMINI_API_KEY auth] (https://github.com/google-gemini/gemini-cli/pull/28546)**
    - **功能**: **关键修复**。当用户通过 `GEMINI_API_KEY` 环境变量认证时，会清除请求中可能存在的冲突 `Authorization` 头，防止 Google API 返回 401 认证错误。
    - **状态**: 新提交，Open。

7.  **[fix(core): deep-merge user model config over defaults] (https://github.com/google-gemini/gemini-cli/pull/28364)**
    - **功能**: **配置修复**。修复了用户配置不能正确与默认配置进行深层合并的问题，确保用户对模型的参数设置（如 `generateContentConfig`）能生效。
    - **状态**: 已合并/关闭。

8.  **[fix(auth): use native fetch for OAuth token exchange to avoid "Premature close"] (https://github.com/google-gemini/gemini-cli/pull/28446)**
    - **功能**: **Bug修复**。解决在特定 VPS 环境下，使用非原生 HTTP 库进行 OAuth 令牌交换时导致的“连接意外关闭”问题，改用 Node.js 原生 `fetch` 提高兼容性。
    - **状态**: 已更新，Open。

9.  **[docs(get-started): add Windows PowerShell troubleshooting for gemini command] (https://github.com/google-gemini/gemini-cli/pull/28447)**
    - **功能**: **文档改进**。为 Windows PowerShell 用户提供了安装后无法运行 `gemini` 命令的故障排查指南，降低平台门槛。
    - **状态**: 已更新，Open。

10. **[fix(core): prevent AbortSignal listener leak in ShellExecutionService] (https://github.com/google-gemini/gemini-cli/pull/28363)**
    - **功能**: **稳定性修复**。修复了 Shell 执行服务中的 `AbortSignal` 监听器泄露问题，防止长会话中出现内存泄漏，提升 CLI 的长期运行稳定性。
    - **状态**: 已合并/关闭。

## 功能需求趋势

1. **Agent 行为增强与可靠性**：社区最关注的点。包括子代理的错误恢复（#22323）、智能调度（#21968）、避免挂起（#21409）、更安全的命令执行（#19873）以及行为评估体系的建立（#24353）。
2. **安全加固**：安全相关的 PR 和 Issue 显著增多。例如 MCP OAuth 令牌管理、认证头冲突修复、沙箱模式兼容性、文件密钥存储的加密加固等，说明随着功能增加，安全审计和修复成为重点。
3. **新模型与平台支持**：社区对引入 `gemini-3.5-flash` 等新模型有明确需求（#28485），同时对 Windows、Wayland、特定 VPS 环境等非主流平台的兼容性问题有持续反馈。
4. **上下文与记忆管理**：自动记忆功能的逻辑缺陷（#26522, #26525）和持久化问题引起关注，社区希望记忆系统能更智能、更节约资源。
5. **开发者工具与可观测性**：希望改进 Agent 行为的报告和调试能力，例如 `/bug` 报告包含子代理上下文（#21763）、子代理执行轨迹可视化（#22598）。

## 开发者关注点

- **可靠性痛点**：**子代理假成功**和**通用代理挂起**是两个最令开发者头疼的问题，直接破坏了自动化工作流的信任。
- **智能性不足**：模型**不主动使用自定义技能和子代理**，被批评为“不知变通”，严重限制了工具的可扩展性和高级定制能力。
- **稳定性问题**：**Shell 命令执行后卡死**、**创建临时脚本污染目录**等是高频出现的稳定性吐槽，影响日常开发体验。
- **兼容性挑战**：Linux 下的 **Wayland 兼容性**、Windows 下的 **PowerShell 使用** 以及 headless VPS 的 **OAuth 认证**问题，表明跨平台支持仍有待改进。
- **性能开销**：自动记忆功能的**无限重试**和 Agent 的**过度消耗 Token**（例如不使用 AST 工具而导致多次读取文件），是开发者关注的长远性能优化方向。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 | 2026-07-28

## 今日速览

今日发布 **v1.0.76-0**，重点改进了 MCP 工具缓存加载速度并让 Autopilot 模式在任务完成后默认保持选中。社区中 **plan-mode 回归**（阻止 shell 命令）和 **子进程僵尸泄漏** 成为焦点，同时多项关于 ACP 非交互模式、Windows 终端渲染、`glob` 工具假阴性的新问题被提出。开发者对 **持久化 Autopilot 模式** 和 **非 Git VCS 支持** 的需求依然强烈。

## 版本发布

**v1.0.76-0** ([查看详情](https://github.com/github/copilot-cli/releases/tag/v1.0.76-0))

**改进**
- MCP 工具从定义域快照加载更快，支持进程级和每服务器缓存退出。
- Autopilot 在任务完成后默认保持选中；如需返回交互模式，设置 `stayInAutopilot` 为 `false`。

**修复**
- 恢复“当……时的早期警告”（原文不完整，推测为恢复某些场景下的 warning）。

---

## 社区热点 Issues

以下精选 10 个当前最受关注或最具讨论价值的问题，按重要性排序。

### 1. [#4188] plan-mode 回归：阻止 shell 命令
- **状态**：OPEN | **评论**：6 | **点赞**：3
- **重要原因**：`gh` 等命令行工具被 plan-mode 阻止，破坏了原有规划流程，属于严重回归。
- 🔗 https://github.com/github/copilot-cli/issues/4188

### 2. [#2792] [已关闭] 自动切换规划与执行模型
- **状态**：CLOSED | **评论**：5 | **点赞**：16
- **重要原因**：虽已关闭，但社区高票支持，表明对 **不同阶段使用不同模型** 的强烈需求（如规划用 GPT-4o、执行用更快模型）。
- 🔗 https://github.com/github/copilot-cli/issues/2792

### 3. [#4163] [已关闭] 子进程未收割导致僵尸进程堆积
- **状态**：CLOSED | **评论**：5 | **点赞**：3
- **重要原因**：Linux 上每 21 分钟产生 8 个僵尸进程，影响系统稳定性，已在 1.0.76 修复（具体修复未在 Release 中说明）。
- 🔗 https://github.com/github/copilot-cli/issues/4163

### 4. [#4183] [已关闭] 自动压缩无法防止 CAPI 5MB 请求体限制
- **状态**：CLOSED | **评论**：4 | **点赞**：10
- **重要原因**：长会话虽未达到 token 上限，但序列化后超过 5MB 导致模型调用永久失败，自动压缩无效。
- 🔗 https://github.com/github/copilot-cli/issues/4183

### 5. [#1381] Rewind 功能强制依赖 Git，不支持 jj/hg 等其他 VCS
- **状态**：OPEN | **评论**：3 | **点赞**：9
- **重要原因**：大量非 Git 用户无法使用 Rewind，而 VS Code 中不依赖 Git，CLI 应支持更灵活的回退机制。
- 🔗 https://github.com/github/copilot-cli/issues/1381

### 6. [#1730] 插件 hook `sessionStart` 未触发
- **状态**：OPEN | **评论**：6 | **点赞**：3
- **重要原因**：`.github/hooks/` 下的 `sessionStart` 钩子在 v0.0.420 后失效，影响插件生态自动化。
- 🔗 https://github.com/github/copilot-cli/issues/1730

### 7. [#4233] ACP 模式缺少 `usage_update` 事件
- **状态**：OPEN | **评论**：2 | **点赞**：2
- **重要原因**：ACP 客户端无法获取上下文窗口和 AI credits 用量指示，与交互模式功能不对等。
- 🔗 https://github.com/github/copilot-cli/issues/4233

### 8. [#4161] 切换回 Autopilot 模式后 `task_complete` 不可用
- **状态**：OPEN | **评论**：2 | **点赞**：3
- **重要原因**：声称在 v1.0.4 已修复的回归再次出现，影响多任务自动化流程。
- 🔗 https://github.com/github/copilot-cli/issues/4161

### 9. [#4266] 退出命令不显示会话概览屏
- **状态**：OPEN | **评论**：1 | **点赞**：0
- **重要原因**：`/exit` 或 Ctrl+C 后本应显示会话摘要，现直接消失，疑似竞态条件。
- 🔗 https://github.com/github/copilot-cli/issues/4266

### 10. [#4271] `glob` 工具多段模式假阴性
- **状态**：OPEN | **评论**：0 | **点赞**：0
- **重要原因**：任何包含路径分隔符的模式（如 `2026/07/*.md`）除非以 `**/` 开头，否则返回无匹配，影响文件搜索可靠性。
- 🔗 https://github.com/github/copilot-cli/issues/4271

---

## 重要 PR 进展

以下 10 个 PR 在过去 24 小时内均有更新（部分为长期未合并但持续活跃的贡献）。由于社区中存在较多测试/垃圾提交，仅列出具有实质内容的 PR。

### 1. [#1609] 更新 PAT 添加权限的文档路径
- **内容**：修正文档中 `Copilot Requests` 权限在 PAT UI 下的位置说明，帮助用户避免遗漏。
- 🔗 https://github.com/github/copilot-cli/pull/1609

### 2. [#1598] 修复 install.sh 临时目录泄漏
- **内容**：为 `install.sh` 添加 `trap` 清理临时目录，防止 `set -e` 意外退出时残留 `/tmp` 文件。
- 🔗 https://github.com/github/copilot-cli/pull/1598

### 3. [#1333] 修正文档语法和 Markdown 格式
- **内容**：补充缺失冠词，删除多余空行，无功能变化。
- 🔗 https://github.com/github/copilot-cli/pull/1333

### 4. [#1116] 修正 0x 模型不减少配额的误导文档
- **内容**：README 此前暗示 0x 模型也会减少配额，实际使用中 0x 模型不消耗配额，现已更正。
- 🔗 https://github.com/github/copilot-cli/pull/1116

### 5. [#988] 修复 brew 安装命令前缀缺失
- **内容**：README 中 `brew install copilot-cli` 缺少 `github/gh` tap 前缀，导致安装失败。
- 🔗 https://github.com/github/copilot-cli/pull/988

### 6. [#4030] 添加 Jekyll 部署的 GitHub Actions Workflow
- **内容**：为项目添加自动构建并部署 Jekyll 站点到 GitHub Pages 的 CI 工作流。
- 🔗 https://github.com/github/copilot-cli/pull/4030

### 7. [#3928] 添加 .gitignore 和设置配置
- **内容**：新增 `.gitignore` 及默认设置配置文件，提升项目初始化体验。
- 🔗 https://github.com/github/copilot-cli/pull/3928

### 8. [#2800] 添加初始 devcontainer 配置
- **内容**：增加开发容器配置，方便远程开发或容器化开发环境（PR 质量存疑，但主题有价值）。
- 🔗 https://github.com/github/copilot-cli/p

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 | 2026-07-28

## 今日速览

过去 24 小时，Kimi Code CLI 社区主要聚焦于 **Windows 环境兼容性修复** 与 **VSCode 扩展稳定性改进**。两项关键的 UnicodeEncodeError 修复 PR 已提交，解决了 Git Bash 和 Web 模式下的中文编码崩溃问题。同时，VSCode 扩展中审批弹窗间歇性不渲染以及钩子函数被 GC 提前回收的 bug 被详细报告，正在推动修复。

---

## 社区热点 Issues

> 以下为过去 24 小时内更新的全部 Issues（共 4 条），均已附上链接。

### #1070 [已关闭] 登录失败：无法连接到 auth.kimi.com:443（网络不可达）  
- **作者**：@notedit  
- **状态**：已关闭，最后更新 2026-07-27  
- **评论数**：8  
- **重要性**：该问题影响用户使用 `/login` 命令完成身份认证，根源是网络不可达，推测为特定网络环境或代理配置导致。社区有 8 条讨论，说明有一定用户遇到此问题。尽管已关闭，仍可作为网络诊断参考。  
- [查看详情](https://github.com/MoonshotAI/kimi-cli/issues/1070)

### #2317 [开放] [VSCode 扩展] Plan 模式下的文件路径在聊天 WebView 中不可点击  
- **作者**：@vlad-at-work  
- **状态**：OPEN，最后更新 2026-07-27  
- **评论数**：3  
- **重要性**：影响了 VSCode 扩展的日常使用体验——用户无法通过点击路径快速跳转到对应文件。评论数 3，社区关注度中等，但属于交互细节的常见需求。  
- [查看详情](https://github.com/MoonshotAI/kimi-cli/issues/2317)

### #2564 [开放] 修复钩子函数：PostToolUse / PostToolUseFailure 任务在完成前被 GC 回收  
- **作者**：@belenov-maker  
- **状态**：OPEN，最后更新 2026-07-27  
- **评论数**：0（新提）  
- **重要性**：这是一个 **根本性 bug**——用户注册的自定义钩子（如 post-tool-use）可能因 GC 过早回收子进程而无法执行，导致钩子行为非确定性。该问题深入引擎层（`kimi_cli/soul/toolse...`），对依赖钩子做自动化的开发者影响较大。虽无评论，但描述详尽并给出根因，预计会迅速引起维护者注意。  
- [查看详情](https://github.com/MoonshotAI/kimi-cli/issues/2564)

### #2563 [开放] [VSCode 扩展] 审批弹窗（ExitPlanMode / 工具权限）间歇性不渲染，导致无限等待或 600 秒静默超时  
- **作者**：@edpa2019  
- **状态**：OPEN，最后更新 2026-07-27  
- **评论数**：0（新提）  
- **重要性**：高优先级！VSCode 扩展中审批弹窗不显示会让用户操作完全卡死，直到 10 分钟超时。作者提供了详细的版本信息（Extension 0.6.4, darwin-arm64），有助于快速复现。该问题直接影响用户对扩展的基本信任。  
- [查看详情](https://github.com/MoonshotAI/kimi-cli/issues/2563)

---

## 重要 PR 进展

> 以下为过去 24 小时内提交或更新的全部 Pull Requests（共 4 条）。

### #2539 [开放] fix(mcp): 为 Moonshot API 规范化工具名称  
- **作者**：@lihailong00  
- **最后更新**：2026-07-27  
- **摘要**：为 MCP 工具名称生成稳定的 Moonshot 兼容别名，同时保留原始名称用于上游路由；修正了 MCP schema 中缺失的根 `object` 类型，并分发 `anyOf`/`required` 结构。  
- **意义**：提升 MCP 工具在 Moonshot API 下的兼容性，修复了因 schema 不完整导致的调用失败。  
- [查看详情](https://github.com/MoonshotAI/kimi-cli/pull/2539)

### #2562 [开放] fix(llm): 允许禁用 prompt cache key  
- **作者**：@lihailong00  
- **最后更新**：2026-07-27  
- **摘要**：在 `kimi` 提供者配置中新增 `prompt_cache_key` 布尔设置，设为 false 时可省略会话派生的 `prompt_cache_key` 请求字段；保留默认行为并更新中英文文档。  
- **意义**：满足需要禁用提示缓存的场景（如调试、节约 token），提升配置灵活性。  
- [查看详情](https://github.com/MoonshotAI/kimi-cli/pull/2562)

### #2561 [开放] 修复启动时因 stdio 使用非 UTF-8 编码导致的 UnicodeEncodeError  
- **作者**：@LHMQ878  
- **最后更新**：2026-07-27  
- **摘要**：修复 Windows 下从 Git Bash 启动 `kimi` 时因 GBK 编码无法编码 `▐` 字符导致的崩溃，该字符来自欢迎横幅。  
- **意义**：解决 Windows（尤其是中文 locale）用户长期以来的启动阻塞问题。  
- [查看详情](https://github.com/MoonshotAI/kimi-cli/pull/2561)

### #2560 [开放] 修复 Web 模式下横幅输出时 stdout 非 UTF-8 导致的 UnicodeEncodeError  
- **作者**：@LHMQ878  
- **最后更新**：2026-07-27  
- **摘要**：修正 `kimi web` 在 Windows 中文环境（codepage 936/GBK）下重定向 stdout 时因 `➜` 等字符编码失败而崩溃的问题。  
- **意义**：与 #2561 互补，覆盖 Web 服务启动场景，进一步消除 Windows 下的编码障碍。  
- [查看详情](https://github.com/MoonshotAI/kimi-cli/pull/2560)

---

## 功能需求趋势

从近期 Issues 和 PR 可以提炼出社区当前最关注的三个方向：

1. **跨平台编码兼容性**  
   - Windows 下 GBK/非 UTF-8 环境依然是主要痛点。两项 PR (#2561, #2560) 集中修复 CLI 和 Web 模式的 UnicodeEncodeError。  
   - **趋势**：用户希望官方彻底解决 Windows 中文 locale 下的稳定性，预计后续还会对日志输出、文件路径等做类似加固。

2. **VSCode 扩展的交互稳定性**  
   - Issues #2317（路径不可点击）和 #2563（审批弹窗不渲染）表明扩展的 UI 渲染和事件处理存在并发竞态或时机问题。  
   - **趋势**：随着更多用户通过 VSCode 使用 Kimi，扩展的可靠性已成为社区核心诉求，未来可能引入更紧密的 WebView 状态同步机制。

3. **钩子/自动化的确定性执行**  
   - Issue #2564（钩子被 GC 提前回收）提示了后台任务生命周期管理的缺陷。  
   - **趋势**：高级用户希望钩子系统稳定可预测，以支撑复杂的 CI/CD 或本地自动化流程。可能推动引擎层引入引用保持或任务队列。

---

## 开发者关注点

综合昨日动态，开发者反馈最突出的痛点如下：

| 痛点 | 对应 Issue/PR | 受影响场景 |
|------|---------------|------------|
| **Windows 下 CLI 直接崩溃** | #2561, #2560 | Git Bash / CMD / PowerShell 启动 `kimi` 或 `kimi web` |
| **VSCode 扩展审批弹窗无法显示，导致操作卡死** | #2563 | 任何需要确认工具权限或退出 Plan 模式的操作 |
| **自定义钩子执行随机缺失** | #2564 | 依赖 `PostToolUse`/`PostToolUseFailure` 进行日志记录、通知等自动化任务 |
| **MCP 工具在 Moonshot API 下调用失败** | #2539 | 使用第三方 MCP 服务并通过 Moonshot API 路由的场景 |
| **提示缓存无法按需关闭** | #2562 | 调试或需要精确控制每个请求上下文的开发场景 |

> 建议关注以上问题的开发者查看对应条目，社区维护团队正积极处理，尤其是涉及 Windows 编码的两项 PR 已进入审查阶段。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 | 2026-07-28

## 📌 今日速览
- 发布 **v1.18.7 / v1.18.6** 两个补丁版本，修复 macOS 全屏标题栏、项目选择器滚动、分支缓存冲突及 MCP 兼容性问题。
- 社区最热 Issue 仍是 **#8501 粘贴文本展开**（👍219），反映用户对输入控制力的强烈需求；**#9281 统一用量追踪** 讨论活跃，签名集成场景呼声渐高。
- 多个 UI 冻结/崩溃报告（#38844、#38979、#39162）在 v1.18.7 中已部分修复，但 AutoScroller 插件依赖问题仍待解决。

---

## 📦 版本发布

### v1.18.7（最新）
**Desktop 修复**
- 移除 macOS 全屏下多余的标题栏内边距。
- 修复当影子命令被移除后命令面板条目错误重现的问题。
- 为项目选择器下拉菜单添加滚动支持（感谢 @david1gp 贡献）。

### v1.18.6
**Core 修复**
- 修复分支专属仓库缓存：刷新一个引用不再导致另一个分支的 checkout 被移动。

**Desktop 改进与修复**
- 改进与新版客户端 API 的兼容性（目录、项目、会话、终端流程）。
- 修复旧版 MCP 兼容问题。

> 社区贡献者：2 人

---

## 🔥 社区热点 Issues（Top 10）

### 1. #8501 [FEATURE] 允许展开粘贴文本
- **热度**：👍219 · 💬30 · 创建 2026-01-14
- **摘要**：当前粘贴文本会被自动摘要，但用户希望编辑或查看原文，需要可展开/折叠的交互。
- **链接**：https://github.com/anomalyco/opencode/issues/8501

### 2. #9281 [FEATURE] 添加统一用量跟踪 `/usage`
- **热度**：👍31 · 💬11 · 创建 2026-01-18
- **摘要**：OAuth 登录后无法查看用量/速率限制，建议提供内置的 `/usage` 命令统一展示各 provider 用量。
- **链接**：https://github.com/anomalyco/opencode/issues/9281

### 3. #29703 [FEATURE] 更改项目文件夹路径时不丢失会话历史
- **热度**：👍13 · 💬9 · 创建 2026-05-28
- **摘要**：重命名或移动目录后，OpenCode 因路径绑定而丢失历史，用户希望支持路径变更时的会话迁移。
- **链接**：https://github.com/anomalyco/opencode/issues/29703

### 4. #34063 [FEATURE] 分离「复制选中文本」与「鼠标」设置
- **热度**：👍2 · 💬6 · 创建 2026-06-26
- **摘要**：`mouse: true` 时选中文本自动复制，`false` 时无法滚动。建议增加独立 `copy_on_select` 选项。
- **链接**：https://github.com/anomalyco/opencode/issues/34063

### 5. #28596 [BUG] 重复工具调用循环
- **热度**：👍0 · 💬5 · 创建 2026-05-21
- **摘要**：Agent 进入无限循环，重复调用同一工具且参数相同，需要手动中断。希望加入重试检测或循环上限。
- **链接**：https://github.com/anomalyco/opencode/issues/28596

### 6. #38844 [BUG] 关闭按钮无响应（UI 卡死）
- **热度**：👍0 · 💬5 · 创建 2026-07-25
- **摘要**：在项目主页点击关闭按钮后屏幕冻结，无法进行任何操作。v1.18.5 复现，怀疑与渲染器相关。
- **链接**：https://github.com/anomalyco/opencode/issues/38844

### 7. #24760 [BUG] 鼠标滚轮应滚动整个聊天视图
- **热度**：👍2 · 💬4 · 创建 2026-04-28
- **摘要**：输入框内滚动时只遍历输入历史，期望改为滚动整个聊天区域，符合常规聊天工具行为。
- **链接**：https://github.com/anomalyco/opencode/issues/24760

### 8. #38979 [BUG] macOS 上关闭项目后桌面 UI 冻结
- **热度**：👍0 · 💬4 · 创建 2026-07-26
- **摘要**：通过 "..." → "Close" 关闭项目后，整个 UI 无响应（鼠标悬停仍有高亮，但点击无效）。渲染进程未崩溃。
- **链接**：https://github.com/anomalyco/opencode/issues/38979

### 9. #39162 [BUG] Desktop 1.18.7 渲染器崩溃：AutoScroller 依赖 Scroller
- **热度**：👍0 · 💬3 · 创建 2026-07-27
- **摘要**：打开含有可排序/拖拽列表的 Settings 页面时，报错 `AutoScroller plugin depends on Scroller plugin`，窗口显示错误页。
- **链接**：https://github.com/anomalyco/opencode/issues/39162

### 10. #34040 [BUG] TUI 自动补全不列出配置引用中的文件
- **热度**：👍2 · 💬4 · 创建 2026-06-26
- **摘要**：引用别名指向外部目录时，输入 `@home` 后自动补全只显示别名本身，无法展开下级文件列表。
- **链接**：https://github.com/anomalyco/opencode/issues/34040

---

## 🔧 重要 PR 进展（Top 10）

### 1. #39203 [contributor] refactor(core): 使用 RcMap 管理 Watcher 生命周期
- **类型**：重构 · **状态**：OPEN
- **摘要**：使 Watcher 获取过程可中断，解决原生订阅超时（10s）期间无法取消/关闭的问题，提升稳定性。
- **链接**：https://github.com/anomalyco/opencode/pull/39203

### 2. #29831 fix(core): 在进程退出时解析 spawn 完成（修复 Windows 孤儿进程挂起）
- **类型**：修复 · **状态**：OPEN
- **摘要**：后台进程启动后，父 shell 退出但子进程输出仍打开导致 Agent 等待。PR 通过检测退出并延迟收集剩余输出来解决。
- **链接**：https://github.com/anomalyco/opencode/pull/29831

### 3. #38534 feat(tui): 发射 Toast 挂载事件
- **类型**：新特性 · **状态**：OPEN
- **摘要**：为服务器插件新增 `tui.toast.mount` 生命周期事件，TUI 挂载 Toast 后通知服务端，便于插件做联动。
- **链接**：https://github.com/anomalyco/opencode/pull/38534

### 4. #37625 [contributor] fix(provider): 对 Kimi 工具 schema 做归一化处理
- **类型**：修复 · **状态**：OPEN
- **摘要**：对自定义或 MCP 工具 schema 做兼容层转换，避免因不兼容字段导致整个 Prompt 被 Kimi 拒绝。
- **链接**：https://github.com/anomalyco/opencode/pull/37625

### 5. #38060 fix(opencode): 从 provider 请求中排除被拒绝的 MCP 工具
- **类型**：修复 · **状态**：OPEN
- **摘要**：全局 `tools` 配置中使用 `"mymcp_*": false` 禁用的工具仍被发送给 provider，PR 实现拒绝列表过滤。
- **链接**：https://github.com/anomalyco/opencode/pull/38060

### 6. #34256 fix(server): 在实例查找前拒绝外部目录提示
- **类型**：修复 · **状态**：CLOSED
- **摘要**：防止恶意/错误的目录提示被用于实例路由，增强多项目时的安全性。
- **链接**：https://github.com/anomalyco/opencode/pull/34256

### 7. #34253 fix(app): 解析沙箱项目编辑
- **类型**：修复 · **状态**：CLOSED
- **摘要**：根据 project ID、worktree 或沙箱成员关系匹配项目元数据后再执行编辑，加入回归测试，修复沙箱目录无法编辑的问题。
- **链接**：https://github.com/anomalyco/opencode/pull/34253

### 8. #34246 feat(tui): 添加 `tool_output_expanded_default` 选项
- **类型**：新特性 · **状态**：CLOSED
- **摘要**：新增 TUI 配置，默认为 `false`；设为 `true` 后所有工具输出默认展开，方便查看详情。
- **链接**：https://github.com/anomalyco/opencode/pull/34246

### 9. #34234 fix: 保留附件文件路径
- **类型**：修复 · **状态**：CLOSED
- **摘要**：将附件的源路径作为元数据保留，同时保持 Prompt 请求体在本地/HTTP/WebSocket 间可移植，便于后续引用。
- **链接**：https://github.com/anomalyco/opencode/pull/34234

### 10. #34227 fix(console): 处理部分 Zen 退款
- **类型**：修复 · **状态**：CLOSED
- **摘要**：修正 Stripe `charge.refunded` webhook 逻辑：只扣除实际退款金额（而非原充值额），并防止重复扣减。
- **链接**：https://github.com/anomalyco/opencode/pull/34227

---

## 📈 功能需求趋势

从近 24 小时更新的大量 Issues 中，社区最关注以下方向：

| 趋势方向 | 代表 Issue | 热度 |
|----------|------------|------|
| **输入交互增强** | 粘贴文本展开（#8501）、鼠标与复制分离（#34063）、聊天滚动行为（#24760） | 🔥🔥🔥 |
| **会话与项目管理** | 路径变更不丢历史（#29703）、存档/归档功能（PR #34210）、沙箱项目编辑（#34253） | 🔥🔥 |
| **用量与计费透明** | 统一用量追踪（#9281）、支付激活问题（#33264, #39133） | 🔥🔥 |
| **MCP / Provider 兼容性** | 拒绝工具过滤（#38060）、Kimi schema 归一化（#37625）、环境变量字段歧义（#39135） | 🔥🔥 |
| **UI 稳定性** | 桌面端冻结/崩溃（#38844, #38979, #39162）、TUI 自动补全（#34040） | 🔥🔥 |

---

## 🧑‍💻 开发者关注点

- **UI 冻结/崩溃高发**：macOS 关闭项目后锁定（#38979）、Windows 同样复现（#38885）、设置页 AutoScroller 依赖错误（#39162）。建议团队优先排查渲染进程生命周期管理。
- **Agent 循环与子代理失败**：#28596 工具调用无限循环、#39196 子代理失败后无 task_id 导致父级无法恢复——核心 Agent 编排稳定性仍是痛点。
- **全局技能不可用**：#32181 用户自定义全局技能注册后无法被模型使用，影响插件生态。
- **TUI 多服务器分支混乱**：#39181 多个 TUI 连接到同一 `opencode serve` 时显示其他项目的分支名，影响开发体验。
- **支付与订阅问题**：#33264 信用卡被拒、#39133 付款后订阅未激活，财务系统与用户通知需完善。

如需进一步追踪某类问题或 PR 并入情况，请随时告知。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 | 2026-07-28

## 今日速览
- 🚀 **夜间版 v0.21.0-nightly 发布**，修复了 CLI 时间显示本地化及 autofix 重构问题；同时 SWE-bench Verified 基准结果显示 **75.2% resolv率（376/500）**，但处于 QUARANTINED 状态。
- 🔒 **两起严重安全漏洞被报告并关闭**：MCP 工具调用绕过用户授权（#7768）和 SSE 会话创建可重试被拒工具（#7769），影响桌面端和 MCP 集成。
- ⚠️ **E2E 测试链式失败**：过去 24 小时内超过 15 个提交触发了主分支 CI 失败（#7860、#7859 等），开发团队已发起 PR 试图对重复失败进行去重（#7792）。

---

## 版本发布
### v0.21.0-nightly.20260727.c003e1718
> **更新内容：**
> - `fix(cli): measure insight days and hours in local time everywhere` — 修正 CLI 中洞察统计的时区问题，确保所有时间显示遵循本地时间。
> - `refactor(autofix): ext` — 对 autofix 模块进行扩展性重构，为后续自动化修复能力铺路。
> - 链接：[Release notes](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.0-nightly.20260727.c003e1718)

### dsw-manual-poc-20260727-1 / -2（非生产基准预发布）
> - 基于 `v0.20.0-nightly.20260722.b98306b7e`。
> - 附带 SWE-bench Verified 结果：500/500 完成，376 解决，116 未解决，1 个执行错误。
> - 链接：[dsw-manual-poc-20260727-1](https://github.com/QwenLM/qwen-code/releases/tag/dsw-manual-poc-20260727-1) | [dsw-manual-poc-20260727-2](https://github.com/QwenLM/qwen-code/releases/tag/dsw-manual-poc-20260727-2)

---

## 社区热点 Issues（10 条）

### 1. [Security] MCP tool denial bypassed when a new SSE session is created (#7769)
- **优先级 P1**，6 条评论。当用户拒绝某个 MCP 工具调用后，AI 代理可创建新 SSE 会话并重试被拒工具，导致授权机制被绕过。
- [Issue #7769](https://github.com/QwenLM/qwen-code/issues/7769)

### 2. [Security] Desktop IPC bridge `mcp_client_tool_call` executes MCP tools without enforcing user authorization (#7768)
- **优先级 P1**，6 条评论。桌面端渲染进程通过 `window.electronAPI` 可直接调用 MCP 服务，无需用户授权，存在权限提升风险。
- [Issue #7768](https://github.com/QwenLM/qwen-code/issues/7768)

### 3. [Security Hardening] Qwen Desktop BrowserWindow uses insecure Electron webPreferences (#7772)
- **优先级 P3**，4 条评论。桌面窗口启用了不安全选项（如 `sandbox: false`），建议加强 Electron 安全配置。
- [Issue #7772](https://github.com/QwenLM/qwen-code/issues/7772)

### 4. VS Code 扩展无法连接 Qwen Agent (#6414 / #7056)
- 两个 Issue 均已被关闭，但社区反映强烈（各 6 条评论）。`Failed to connect to Qwen agent` 问题在 0.19.11 和 0.21.0 版本中反复出现，涉及 ACP 进程异常退出。
- [#6414](https://github.com/QwenLM/qwen-code/issues/6414) | [#7056](https://github.com/QwenLM/qwen-code/issues/7056)

### 5. Feature Request: Skill Context Lifecycle Management (#6762)
- **优先级 P2**，5 条评论。建议为 SKILL.md 上下文添加生命周期管理，支持卸载、压缩或分页，避免长期会话中上下文无限膨胀。
- [Issue #6762](https://github.com/QwenLM/qwen-code/issues/6762)

### 6. YOLO mode: mid-stream socket close is not retried (#7832)
- **优先级 P1**，3 条评论。YOLO 模式下生成大代码（>500 行）时 SSL 连接断开无重试，导致任务彻底失败。DashScope 网关约 3-5 分钟后关闭连接。
- [Issue #7832](https://github.com/QwenLM/qwen-code/issues/7832)

### 7. Repeated ECONNRESET on streaming responses when context exceeds ~150k tokens (#7831)
- **优先级 P2**，3 条评论。长会话上下文超过 150k tokens 后，流式响应频繁触发 ECONNRESET，影响持续对话体验。
- [Issue #7831](https://github.com/QwenLM/qwen-code/issues/7831)

### 8. Sub agent asks user questions but user has no way to answer (#7835)
- **优先级 P2**，3 条评论。子代理向用户提问时，主代理未收集并转发，导致子代理永久等待。需增强子代理交互机制。
- [Issue #7835](https://github.com/QwenLM/qwen-code/issues/7835)

### 9. Quota-exhausted 429s retry silently and surface no error to the user (#7841)
- **优先级 P2**，3 条评论。API 返回 429（配额耗尽）时被错误视为瞬时限流，导致静默重试直到预算耗尽，用户无感知。
- [Issue #7841](https://github.com/QwenLM/qwen-code/issues/7841)

### 10. Git branch display in footer becomes stale after branch switch (#7828)
- **优先级 P3**，3 条评论。Web Shell 中切换 Git 分支后，底部按钮显示的分支名未及时更新，影响开发体验。
- [Issue #7828](https://github.com/QwenLM/qwen-code/issues/7828)

---

## 重要 PR 进展（10 条）

### 1. feat(web-shell): honor voice hold mode (#7839)
- 为 Web Shell 添加语音「按住说话」模式，支持按压力度控制录音启停，优化语音交互体验。
- [PR #7839](https://github.com/QwenLM/qwen-code/pull/7839)

### 2. feat(web-shell): add git branch picker, commit dialog, and create PR flow (#7731)
- 引入 IntelliJ 风格的分支选择器、提交对话框和创建 PR 流程，大幅提升 Git 操作效率。
- [PR #7731](https://github.com/QwenLM/qwen-code/pull/7731)

### 3. feat(ci): Deduplicate E2E failure issues by commenting on existing issue (#7792)
- 修改主分支 CI 逻辑，对重复的 E2E 测试失败不再新建 Issue，改为在已有 Issue 追加评论，减少噪音。
- [PR #7792](https://github.com/QwenLM/qwen-code/pull/7792)

### 4. fix(core): fast-fail permanent quota-exhaustion 429s instead of silent retry (#7842)
- 针对配额永久耗尽的 429 响应，立即报错并提示用户，而非静默重试整个预算。
- [PR #7842](https://github.com/QwenLM/qwen-code/pull/7842)

### 5. feat(core): persist and replay Goal v3 state (#7815)
- 实现 Goal v3 的持久化转录与回放基础，记录生命周期快照，且内部提示不干扰用户可见的回放边界。
- [PR #7815](https://github.com/QwenLM/qwen-code/pull/7815)

### 6. feat(web-shell): add native Live Voice (#7859)
- 为 macOS 提供原生 Live Voice 体验，支持双击 Command 键启动无项目语音对话，需安装 Qwen Live Host。
- [PR #7859](https://github.com/QwenLM/qwen-code/pull/7859)

### 7. feat(web-shell): add native workspace folder picker (#7849)
- 在 Web Shell 的添加工作区对话框中支持原生文件夹选择器，提升用户路径输入体验。
- [PR #7849](https://github.com/QwenLM/qwen-code/pull/7849)

### 8. fix(cli): do not count a partial trailing line when re-opening a split fence (#7875)
- 修复代码块分割场景下尾部未完成行被误计为完整行的问题，确保 `start-line` 指向正确源代码行。
- [PR #7875](https://github.com/QwenLM/qwen-code/pull/7875)

### 9. fix(safe-mode): preserve caller-supplied top-tier MCP servers (#7827)
- 修复 `--safe-mode` 无条件丢弃通过 ACP `session/new` 或 `--mcp-config` 传入的 MCP 服务器的 bug。
- [PR #7827](https://github.com/QwenLM/qwen-code/pull/7827)

### 10. feat(channels): dispatch GitHub notifications by reason (#7826)
- 路由 GitHub 通知按 `notification.reason` 分发，确保提及、审查请求、指派等不同场景生成正确的 agent 输入。
- [PR #7826](https://github.com/QwenLM/qwen-code/pull/7826)

---

## 功能需求趋势

从近期 Issues 和 PR 中可以提炼出以下社区关注方向：

| 方向 | 说明 | 代表性 Issue/PR |
|------|------|-----------------|
| **MCP 安全与授权** | 用户希望 MCP 工具调用有严格的用户确认机制，防止绕过。 | #7768, #7769, #7772 |
| **IDE/VSCode 连接稳定性** | 反复出现的 ACP 进程退出、连接失败问题影响开发日常。 | #6414, #7056, #7697 |
| **长上下文支持** | 超过 150k tokens 后的 ECONNRESET、Socket 断开问题急需解决。 | #7831, #7832 |
| **上下文生命周期管理** | 用户希望 SKILL.md 等信息能卸载或压缩，而非永久占用 token。 | #6762 |
| **子代理交互** | 子代理询问用户时缺乏转发机制，导致死锁。 | #7835 |
| **配额与错误提示** | 429 状态码应区分瞬时限流和永久耗尽，给用户明确反馈。 | #7841, #7842 |
| **终端用户体验** | 虚拟视口模式、Kitty 键盘协议、信号处理等 CLI 体验优化。 | #7779, #7781 |
| **Git 集成** | 分支选择器、提交对话框、PR 创建等 UI 增强正在快速迭代。 | #7731, #7828 |

---

## 开发者关注点

- **连接问题仍是首要痛点**：多个 Issue 报告 VS Code 扩展无法连接 Qwen Agent，问题跨版本复现，社区希望提供更清晰的错误诊断和重试机制。
- **安全加固刻不容缓**：MCP 工具绕过授权、渲染进程直接调用 MCP 服务等漏洞被研究者报告（@rishavkumar-thecoder），需尽快修复并合入安全配置基线。
- **CI 稳定性需提升**：过去 24 小时内超过 15 次 E2E 测试失败，产生大量重复 Issue 干扰社区讨论。团队已发起去重 PR，但仍需关注根本原因。
- **大上下文交互体验不足**：长会话中网络断开和 API 超时问题突出，开发者建议实现断线重试、上下文压缩或分页加载。
- **子代理能力边界**：子代理无法与用户通信导致永久等待，社区期望设计更完善的子代理交互协议，或明确禁止子代理提问。
- **配额管理缺乏透明度**：429 静默重试浪费 token 且用户无感知，建议将配额耗尽信息直接透传至界面。

---

*数据来源：GitHub QwenLM/qwen-code 仓库，更新时间 2026-07-28。*

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*