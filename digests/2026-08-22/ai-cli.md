# AI CLI 工具社区动态日报 2026-08-22

> 生成时间: 2026-08-21 22:45 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-08-22）

## 1. 生态全景

当前 AI CLI 工具已进入高频迭代与场景分化并存阶段：头部工具保持每日发版节奏，OpenAI Codex 更出现单日 6 个 Rust alpha 版本的高强度更新。社区关注焦点从“能用”转向“用稳”，MCP 生态健壮性、任务生命周期可控性、安全/权限治理成为跨工具共性议题。Windows 平台适配和 BYOK/多模型接入仍是明显短板，直接影响企业级用户采纳。整体看，AI CLI 正从“单点代码助手”演变为融合远程控制、桌面自动化、多 Agent 协作的开发者基础设施。

## 2. 各工具活跃度对比

| 工具 | Issues 动态 | PR 动态 | Release 情况 |
|---|---|---|---|
| **Claude Code** | 约 50 条近期 issue，热点 10 条 | 24h 内无新增/更新 PR | v2.1.239（成本估算溢价、全屏渲染器） |
| **OpenAI Codex** | Top 10 热点 issue（具体总量未披露） | 47 条 PR 更新 | 6 个 Rust alpha 版本 |
| **GitHub Copilot CLI** | 40 条 issue 更新，Top 10 热点 | 24h 内无 PR 更新 | v1.0.81-7（会话恢复、models.list 增强） |
| **Kimi Code CLI** | 1 条 issue | 1 条 PR | 无 |
| **OpenCode** | 热点 issue 如 #785（31 评论/38 👍） | 活跃，具体数量未披露 | v1.18.20、v1.18.21 |
| **Qwen Code** | Top 10 热点 issue | Top 10 PR 进展 | v0.21.14-nightly + 2 项基准测试报告 |
| **Gemini CLI** | 无数据（摘要缺失） | 无数据 | 无数据 |

> 注：Gemini CLI 今日摘要内容为空，本报告无法对其作出分析。

## 3. 共同关注的功能方向

| 方向 | 涉及工具 | 具体诉求 |
|---|---|---|
| **MCP/插件生态稳定性** | Claude Code、OpenAI Codex、Kimi Code、Qwen Code、OpenCode | worktree 下 MCP 不加载、CustomResult 解码失败、MCP 参数被序列化为字符串、启动时 MCP 连接关闭；插件凭证安全与持久化文档 |
| **Windows 平台补齐** | Claude Code、OpenAI Codex、Qwen Code、OpenCode | Auto-Memory 路径失效、捆绑插件因 EFS 加密复制失败、桌面版 MCP 报错、Windows 适配投入 |
| **安全/权限治理** | Claude Code、OpenAI Codex、Qwen Code、Kimi Code | AUP 误报频发；Guardian 审核与沙箱权限细粒度化；CI 代码执行权限边界；权限分类器 fail-open 回归；插件子进程权限边界 |
| **任务生命周期与可观测性** | OpenAI Codex、OpenCode、Kimi Code、Qwen Code | 桌面版任务交接后停止、未知 finish reason 导致会话终止、子代理被 kill 后仍消耗 LLM 配额、subagent 崩溃 |
| **成本/配额透明度** | Claude Code、OpenAI Codex、Kimi Code | 成本估算纳入数据驻留溢价；轮询动作消耗 credits；Pro 配额错配；后台隐形配额消耗 |
| **多模型/多后端接入** | OpenAI Codex、GitHub Copilot CLI、Claude Code、OpenCode | Bedrock 设置能力、BYOK 模型切换、多区域 Vertex AI 支持、本地 provider 接入 |

## 4. 差异化定位分析

| 工具 | 定位与目标用户 | 核心差异化 |
|---|---|---|
| **Claude Code** | 企业级开发者/需要数据驻留与合规的团队 | 多平台推理后端（Bedrock/Vertex/Foundry）、成本估算精细化、严格 AUP 策略 |
| **OpenAI Codex** | 追求前沿 Agent 能力的开发者 | 高频迭代、桌面端 + 移动远程控制、Computer Use/浏览器自动化、Guardian 安全体系 |
| **GitHub Copilot CLI** | GitHub 生态内开发者 | 深度绑定 GitHub Copilot 服务、会话恢复、BYOK/多模型诉求突出但尚未满足 |
| **Kimi Code CLI** | 轻量用户/关注成本控制 | 插件系统轻量，文档化安全最佳实践；目前社区体量小，任务生命周期存在明显 bug |
| **OpenCode** | 开源社区/偏好可定制 CLI 的用户 | 快速补丁节奏、流式模式争议与稳定性修复、MCP 管理可配置性 |
| **Qwen Code** | 中文开发者/Qwen 模型生态用户 | 中文输入法问题关注度高、review 循环与 CI 安全、夜间版发版 + 基准测试验证 |

## 5. 社区热度与成熟度

- **OpenAI Codex** 是当前迭代速度最快的工具：24 小时 47 条 PR、6 个 alpha 版本，社区反馈集中在桌面端和远程控制等新功能，处于“功能扩张期”。
- **Claude Code** 社区基数大、Issue 讨论密集，但 PR 量低；AUP 误报系列 issue 显示出企业级安全策略与开发者体验的矛盾，处于“体验收敛期”。
- **Qwen Code** 开发节奏稳定，每日有 nightly 和完整基准测试报告，安全类议题讨论深度高，属于“快速追赶期”。
- **OpenCode** 虽未披露具体 PR 数，但连续补丁发布并且社区对流式禁用等诉求有 38 👍，属于“活跃开源项目”。
- **GitHub Copilot CLI** 更新量中等，社区集中在 BYOK 和本地模型支持，属于“稳态增强期”。
- **Kimi Code CLI** 24h 内仅 1 Issue / 1 PR，社区热度较低，但仍暴露出任务终止失效这类高影响 bug，属于“早期打磨期”。

## 6. 值得关注的趋势信号

1. **安全治理成为 AI CLI 的核心竞争点。** Claude Code 的 AUP 误报、OpenAI Codex 的 Guardian 审核体系、Qwen Code 的 CI 权限边界讨论均指向同一方向：安全策略必须可解释、可配置、可申诉，而非“一刀切”拦截。
2. **后台 Agent 的资源失控是隐性风险。** Kimi Code 子代理在 kill 后仍调用 LLM、OpenAI Codex 轮询消耗 credits、OpenCode 未知 finish reason 导致提前停止——任务生命周期语义需要标准化，并强制提供“终止即停止”的硬保证。
3. **Windows 支持是普遍短板，也是增量机会。** 多家工具在 Windows 上存在路径、证书、沙箱、插件安装等问题，未来能在该平台提供稳定体验的工具将获得显著差异化优势。
4. **MCP 生态进入“深水区”。** 连接不稳定、参数序列化错误、worktree 下不加载等问题说明 MCP 简单连接已不满足需求，需要引入版本化、作用域隔离、调试诊断等工程能力。
5. **企业级接入与 BYOK 需求上升。** Bedrock 集成、私有 CA 证书、数据驻留成本、多模型切换等诉求表明 AI CLI 正在进入企业采购视野，而不仅是个人开发者玩具。
6. **从“代码补全”到“计算机操作 Agent”正在发生。** OpenAI Codex 的 Browser/Computer Use 配置、远程移动端控制，以及 Claude Code 的全屏渲染器，都预示着 AI CLI 逐步向“操作系统级 Agent”演进，开发者需要重新评估其安全边界。

---

*报告基于 2026-08-22 各工具官方 GitHub 社区摘要整理，Gemini CLI 因数据缺失未纳入对比。*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---

# Claude Code 社区动态日报（2026-08-22）

## 今日速览

- 发布 v2.1.239，为数据驻留工作区加入 1.1× 成本估算溢价，并在 Bedrock、Vertex、Foundry 等平台开放全屏渲染器。
- 最热 issue 为 [#47733](https://github.com/anthropics/claude-code/issues/47733)：用户级 MCP 服务器在 git worktree 会话中无法加载，已获 10 条评论。
- 社区集中反馈 AUP 安全过滤误报（#731xx 系列），涉及漏洞审计、日常代码审查等合法场景，虽多为关闭状态，但反映出的误报问题值得关注。

## 版本发布

**v2.1.239** 已发布，主要变更：

- **成本估算调整**：`/cost`、状态栏及 `--max-budget-usd` 现在将数据驻留工作区的 1.1× 美国-only 推理溢价纳入计算。
- **全屏渲染器**：为 Bedrock、Vertex、Foundry 等此前不支持的平台提供一次性全屏渲染器 offer，新安装将默认启用。

🔗 [Release v2.1.239](https://github.com/anthropics/claude-code/releases)

## 社区热点 Issues

### 1. MCP Worktree 加载缺陷（最高热度）
**#47733** `[OPEN]` 用户级 MCP 服务器在 worktree 会话中不加载
- 作者: @adelaidasofia · 评论: 10 · 👍: 1
- 现象：`~/.claude/settings.json` 中配置的 MCP 在 `claude -w <worktree>` 时失效，手动启动和普通会话正常。
- 社区反应：Mac 用户受影响明显，等待官方 repro，是当前最活跃的 bug 之一。
🔗 https://github.com/anthropics/claude-code/issues/47733

### 2. Windows 上 Auto-Memory 路径失效
**#33619** `[OPEN]` `/memory` 命令在 Windows 无法打开 Auto-Memory 文件夹
- 作者: @lauralex · 评论: 8 · 👍: 2
- 现象：Windows 平台执行 `/memory` 时找不到预期文件夹，功能不可用。
- 社区反应：Windows 用户反馈密集，已有 2 个 👍，期待修复。
🔗 https://github.com/anthropics/claude-code/issues/33619

### 3. Agent 注册表发现不完整
**#82361** `[OPEN]` Agent 工具仅能发现部分 `.claude/agents/*.md` 定义
- 作者: @mTw76 · 评论: 3
- 现象：15 个格式完全相同的 agent 定义文件中，仅 8 个出现在 `subagent_type` 注册表。
- 社区反应：自定义 agent 的开发者关注度较高，可能涉及缓存或加载逻辑缺陷。
🔗 https://github.com/anthropics/claude-code/issues/82361

### 4. CA 证书加载限制导致请求失败
**#72712** `[CLOSED]` 固定加载 10 个系统 CA 证书，忽略 `CLAUDE_CODE_CERT_STORE`
- 作者: @ryansabandal · 评论: 3
- 现象：macOS 环境 `/v1/messages` 请求报 `UNABLE_TO_GET_ISSUER_CERT`，证书配置不生效。
- 社区反应：企业代理/私有 CA 场景下影响严重，虽已关闭，仍是排查热点。
🔗 https://github.com/anthropics/claude-code/issues/72712

### 5. 安全过滤误报：无人机开源项目
**#73126** `[CLOSED]` 反编译自有无人机 App 被误判为 cyber 违规
- 作者: @sworrl · 评论: 4
- 现象：用户构建 FOSS 地面控制站，被服务器端安全过滤器拦截，会话中止。
- 社区反应：误报导致合法开发中断，引发对安全策略误伤的讨论。
🔗 https://github.com/anthropics/claude-code/issues/73126

### 6. AUP 误报：漏洞清扫被阻断
**#73183** `[CLOSED]` 防御性漏洞清扫中因感叹词触发 AUP 阻断
- 作者: @sworrl · 评论: 3
- 现象：用户对自有 Web 应用做漏洞清扫，抱怨语句被安全模型判定为违规。
- 社区反应：`Fable 5` 安全模型对语气敏感，此类误报已非孤例。
🔗 https://github.com/anthropics/claude-code/issues/73183

### 7. AUP 误报：交易机器人部署被标记
**#73172** `[CLOSED]` 部署经过验证的交易机器人升级被 AUP 阻挡
- 作者: @sworrl · 评论: 3
- 现象：已完成合法性验证的部署操作及 3D 仪表盘优化被安全策略拦截。
- 社区反应：安全过滤精准度问题在自动化交易场景下引发争议。
🔗 https://github.com/anthropics/claude-code/issues/73172

### 8. AUP 误报：日常代码审计受阻
**#73168** `[CLOSED]` 审计近期提交与配套服务交互时被阻止
- 作者: @sworrl · 评论: 3
- 现象：常规代码审计操作被安全过滤误判，会话不可恢复。
- 社区反应：开发者对安全模型误伤正常审查工作流感到困扰。
🔗 https://github.com/anthropics/claude-code/issues/73168

### 9. AUP 误报：网站后端安全审计被误杀
**#73211** `[CLOSED]` 自有网站后端基础设施例行安全审计被阻挡
- 作者: @sworrl · 评论: 3
- 现象：普通安全审计请求被服务器端安全策略错误拦截。
- 社区反应：安全审计类合法工作成为误报重灾区，社区期待更精细的策略配置。
🔗 https://github.com/anthropics/claude-code/issues/73211

### 10. AUP 误报：代码质量审计被中断
**#73085** `[CLOSED]` 自有网站仓库代码质量审计被误判为违规
- 作者: @sworrl · 评论: 3
- 现象：例行代码质量检查在半途被安全模型终止。
- 社区反应：大量相似误报印证 `Fable 5` 模型存在系统性误判可能。
🔗 https://github.com/anthropics/claude-code/issues/73085

## 重要 PR 进展

过去 24 小时内无新增或更新的 Pull Request。

## 功能需求趋势

从近 50 条 Issue 中可以提炼出社区重点关注的几个方向：

1. **MCP 配置的健壮性**：用户级与项目级 MCP 应在 worktree、CI 等特殊会话中保持一致的加载行为。
2. **Windows 平台补齐**：路径处理、文件夹操作和文件系统交互需要更完整的 Windows 适配。
3. **自定义 Agent 发现机制**：`subagent_type` 注册表应完整、稳定地装载 `.claude/agents/*.md`，并增加调试/诊断能力。
4. **企业网络与证书处理**：对 `CLAUDE_CODE_CERT_STORE` 等配置应真正生效，支持私有 CA 和代理场景。
5. **安全过滤策略的可控性**：大量误报表明社区需要更透明的策略解释、误报申诉通道，以及针对安全审计类工作的豁免机制。

## 开发者关注点

- **AUP 误报是最突出的痛点**：@sworrl 在 7 月批量提交了 30+ 条相关问题，覆盖漏洞审计、代码审查、开源开发等合规场景，安全模型 `Fable 5` 已造成

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报（2026-08-22）

## 今日速览

- 发布 6 个 Rust 侧新 alpha 版本（0.149.0-alpha.4.1 至 0.150.0-alpha.6），均为高频迭代。
- 社区反馈集中在三大痛点：Windows 平台插件/沙箱故障、Android/iOS 远程控制连接不稳定、ChatGPT Pro 配额异常。
- 共 47 条 PR 于过去 24 小时更新，重点推进 Guardian 安全审核体系、浏览器/计算机使用配置、Amazon Bedrock 接入。

---

## 版本发布

过去 24 小时 Codex Rust 侧发布 6 个版本：

- **rust-v0.150.0-alpha.6** / **rust-v0.150.0-alpha.5** / **rust-v0.150.0-alpha.3** / **rust-v0.150.0-alpha.2**：0.150 系列持续迭代
- **rust-v0.149.0-alpha.7.1** / **rust-v0.149.0-alpha.4.1**：0.149 系列补丁

官方 Release Notes 暂未提供详细变更说明，但结合同日 PR 可推测与沙箱权限管理、Guardian 审核、远程功能重构有关。

---

## 社区热点 Issues（Top 10）

### 1. macOS 桌面版反复生成 Computer Use worker 并 V8 OOM 崩溃
[#38455](https://github.com/openai/codex/issues/38455) · 35 评论 · 15 👍

ChatGPT 桌面版 26.810.41047 在空闲时约 98 秒后崩溃，SIGABRT 经 node::OOMErrorHandler，崩溃时 316 个线程中有 187 个名为 `computer-use`。此前版本 26.730.61639 正常。这是 Computer Use 功能在 macOS 上最严重的稳定性问题。

### 2. 打开已有对话导致 ChatGPT 认证失效并跳转登录
[#39162](https://github.com/openai/codex/issues/39162) · 31 评论 · 22 👍

macOS 版 26.814.41407 打开历史会话时认证 token 失效，被迫重新登录。已知最后一个正常版本为 26.810.52044，属于较严重回归。

### 3. Windows 捆绑插件全部不可用（EFS 加密文件复制失败）
[#25220](https://github.com/openai/codex/issues/25220) · 27 评论 · 4 👍

Windows 11 下所有捆绑插件（Computer Use、Browser、Chrome、LaTeX）不可用，根因是 `copyfile` 无法处理 EFS 加密的 WindowsApps 文件。该问题持续近 3 个月，影响面广。

### 4. 桌面自动化静默回退到 workspace-write 沙箱
[#15310](https://github.com/openai/codex/issues/15310) · 21 评论 · 16 👍

计划任务/自动化任务启动线程时，即使应用配置为 `danger-full-access` 也使用 `workspace-write`，只有用户手动进入聊天界面后才纠正。静默降级存在安全与功能双重隐患。

### 5. 桌面版等待/状态轮询期间反复重新进入模型，消耗 credits
[#35259](https://github.com/openai/codex/issues/35259) · 15 评论 · 8 👍

Ultra/多智能体任务中，仅执行"等待/轮询"动作的 model turns 占总 token 消耗的 19.8%。用户质疑这是否是计费浪费，需优化轮询机制。

### 6. ChatGPT Pro（20x）账户实际获得 Pro 5x 容量
[#38157](https://github.com/openai/codex/issues/38157) · 7 评论 · 5 👍

多个 Pro 账户在 API 中仍标识为 `plan_type: "pro"`，但实际配额与较小的 Pro 5x 档一致。涉及账号计费准确性问题，值得官方核查。

### 7. 桌面版在上下文/任务交接后过早停止
[#33398](https://github.com/openai/codex/issues/33398) · 8 评论 · 6 👍

任务交接后 Codex Desktop 会等待新消息而不是继续执行已进行中的任务，用户需手动发送消息才能恢复。违背智能体连续执行的预期。

### 8. Windows Remote QR 配对成功但 Android 无法建立会话
[#39856](https://github.com/openai/codex/issues/39856) · 8 评论

26.818.31338 版 Windows 主机配对成功，WebSocket 显示 Connected，但 Android 端 `nextConnectionCount=0`，附加请求无法建立。同类问题在 #39947、#39974 中也有报告，说明 Remote 链路存在系统性问题。

### 9. API Key 用户无法使用本地/私有插件市场
[#20621](https://github.com/openai/codex/issues/20621) · 已关闭 · 28 👍

API Key 认证会阻止本地/私有插件市场的管理。该 issue 虽然已关闭，但 28 个 👍 表明 Enterprise/API 用户对此功能诉求强烈。

### 10. MCP tools/call 因 CustomResult 解码失败
[#29002](https://github.com/openai/codex/issues/29002) · 6 评论 · 7 👍

合法的 MCP 工具结果解码为 `CustomResult` 时触发 `Unexpected response type` 错误。Bedrock 提供方环境下可稳定复现，影响 MCP 生态扩展。

---

## 重要 PR 进展（Top 10）

### 1. 实现 Amazon Bedrock 设置（app-server 侧）
[#40007](https://github.com/openai/codex/pull/40007)

新增 `account/bedrock/discover` 与 `account/bedrock/setup` 接口，支持 AWS 配置文件与环境凭据的发现、验证和持久化。Bedrock 接入正在全栈推进。

### 2. 添加 Browser 和 Computer Use 配置
[#40018](https://github.com/openai/codex/pull/40018)

引入类型化的 `browser_use`（历史访问、per-origin 访问、下载/上传、CDP 策略）与 `computer_use`（默认应用访问、macOS bundle ID、Windows AUMID/可执行文件策略）配置。为浏览器/Computer Use 策略化管控打基础。

### 3. 统一 exec 中遵循细粒度沙箱批准
[#40024](https://github.com/openai/codex/pull/40024)

统一 exec 的沙箱升级现在会检查共享的审批策略，`require_escalated` 命令在启用 `sandbox_approval` 时能正确发起提示，未启用时保持拒绝。

### 4. 取消 Guardian 审核及其工具调用
[#40021](https://github.com/openai/codex/pull/40021)

将工具取消 token 传播至 Guardian 审批审核，中断工具时同时中止挂起的审核；对 server 发起的 MCP 审批采用相同取消行为。

### 5. 在异步风险评分中重用 Guardian 审核结果
[#40013](https://github.com/openai/codex/pull/40013)

保留已完成同步 Guardian 允许/拒绝审核的有界证据，作为后续 v2 异步分类器的可信开发者上下文，且与对话记录隔离。

### 6. 升级命令路由至同步 Guardian 审核
[#40005](https://github.com/openai/codex/pull/40005)

`sandbox_permissions=require_escalated` 的命令即使非重试也需经过完整 Guardian 审核，补上一处安全校验盲区。

### 7. 权限更新时保留受管 deny-read 规则
[#40004](https://github.com/openai/codex/pull/40004)

运行时权限更新不得削弱文件系统 `deny_read` 要求——将受管 deny-read 规则独立保留并合并到更新后的配置中，拒绝会削弱规则的配置请求。

### 8. 隐藏不支持模型的 Fast 模式状态
[#39999](https://github.com/openai/codex/pull/39999)

修复了模型不支持 Fast 模式时仍显示"Fast off"的误导性 UI 问题，现在会直接隐藏状态项。

### 9. 为 `/copy` 添加响应目标选择器
[#39997](https://github.com/openai/codex/pull/39997)

`/copy` 现在会打开选择器，可复制整个响应、特定 fenced code block 或 blockquote；代码块按语言标注，显示内容预览并保留原始空白与嵌套引用。

### 10. 强化远程已安装插件缓存协调
[#40015](https://github.com/openai/codex/pull/40015)

远程已安装/已加载插件的快照现在按 active account 隔离，账户切换时丢弃 in-flight 加载；bundle 协调与直接安装/卸载串行化，降低远程插件状态错乱风险。

---

## 功能需求趋势

从近期 Issues/PRs 提炼社区最关注的方向：

1. **浏览器/Computer Use 策略配置**：多条 PR 在引入 per-origin 访问、下载上传策略、AUMID/bundle ID 级控制，说明这两个功能正从"可用"走向"可治理"阶段。
2. **Amazon Bedrock 集成**：既 #37674 缓存控制问题之后，今天出现 app-server 侧 Bedrock 设置能力，官方支持力度明显加大。
3. **Guardian 安全审核体系**：至少 5 条 PR 涉及 Guardian 同步/异步审核、取消传播、deny-read 保留、权限更新合并，安全体系正快速完善。
4. **Remote 远程控制（移动端）**：多条 issue 报告 Android/iOS 配对后无法 attach、连接不稳定，是当前社区反馈量最大的功能方向。
5. **配额/计费透明化**：Pro 配额错配（#38157）、轮询消耗 credits（#35259）、配额异常加速（#38728）等说明用户对用量可观测性与公平性高度敏感。
6. **MCP 生态稳定性**：MCP 工具解码失败（#29002）、OAuth 作用域请求错误（#35253）、subagent 与自定义 provider 不兼容（#17598），MCP 在多 provider 场景下仍待打磨。

---

## 开发者关注点

- **Windows 平台是重灾区**：插件安装（EFS 文件复制失败 #25220、#34764）、沙箱

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 · 2026-08-22

## 今日速览

今日发布 **v1.0.81-7**，重点加入「CLI 崩溃/重启后自动恢复会话」能力，并扩展 `models.list` 的服务端信息展示。Issue 方面，社区对**多 BYOK 模型切换**和 **`/model` 支持本地模型**的呼声最高；同时 `store_memory` 在 v1.0.81 pre-release 中出现回归、MCP BigInt 响应会导致任务中止等 Bug 影响较大。过去 24 小时没有 PR 更新。

---

## 版本发布

### v1.0.81-7

本次为功能增量版本，主要变更：

- **会话恢复**：CLI 启动时会主动询问并恢复上次因崩溃或机器重启而遗留的会话，无需再手动逐个终端重开。
- **`models.list` 增强**：每个模型的响应中现在会包含服务端发布的 `infoMessages` / `warningMessages`。
- **新增 `copilot app` 命令**：新增应用入口命令（原始 release notes 文本截断，具体目标页面待完整发布说明确认）。

---

## 社区热点 Issues

以下从过去 24 小时更新的 40 条 Issue 中选出 10 条最值得关注：

1. **多 BYOK 模型能力** — [#3282](https://github.com/github/copilot-cli/issues/3282)  
   8 条评论 / 26 👍。当前 BYOK 只能通过环境变量配置单个模型，TUI 内无法切换，必须终止会话后重新设置。是当前最高频的模型能力诉求之一。

2. **`/model` 支持 BYOK/本地 provider 切换** — [#3709](https://github.com/github/copilot-cli

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报（2026-08-22）

## 今日速览

过去 24 小时内 Kimi Code CLI 无新版本发布。社区最值得关注的是 **#2615** 号 Bug 报告：后台子代理在任务被标记为 `timed_out`/`killed` 后仍持续调用 LLM，导致配额消耗不可见且无法通过 `TaskStop` 终止。与此同时，**#2614** 号 PR 为插件系统补充了安全与持久化数据文档，回应了社区对插件安全边界的关注。

## 版本发布

过去 24 小时内无新版本发布。

## 社区热点 Issues

> 注：过去 24 小时内仅有 1 条 Issue 更新，以下为全部内容。

### #2615 [Bug] 后台子代理在 TaskStop/超时标记终止后仍持续调用 LLM
- **作者**: @pc9527zxx  
- **创建**: 2026-08-21 | **状态**: OPEN | **评论**: 0 | **👍**: 0  
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2615  

**摘要**: 后台子代理在其任务和元数据已被标记为 `timed_out` 或 `killed` 后，仍持续发出 LLM 请求。任务从活动任务跟踪中消失，导致配额消耗不可见，且 `TaskStop` 无法再将其终止，用户只能通过强制结束整个进程来止损。

**重要性**: 该 Issue 直指任务生命周期管理的核心漏洞——终态判定与资源回收的原子性缺失。若子代理失去控制，用户可能面临不可控的 API 费用。虽然该 Issue 发布不足 24 小时、暂无社区评论，但问题性质严重，预计后续讨论热度会明显上升。

## 重要 PR 进展

> 注：过去 24 小时内仅有 1 条 PR 更新，以下为全部内容。

### #2614 docs(plugins): 文档化插件安全与持久化数据
- **作者**: @QIANLING-0831  
- **创建**: 2026-08-20 | **更新**: 2026-08-21 | **状态**: OPEN  
- **链接**: https://github.com/MoonshotAI/kimi-cli/pull/2614  

**功能/内容**: 完善插件系统文档，明确以下几点：
- 插件工具以本地子进程方式运行，拥有当前用户的文件与网络访问权限；
- `inject` 注入的凭证应妥善处理，避免记录或提交到版本库；
- 重装插件会替换其安装目录，需注意数据持久化策略；
- 建议将插件数据与程序安装目录分离存放。

**重要性**: 插件系统的权限模型与数据安全是开发者采用插件机制的核心顾虑。该 PR 补充的安全说明有助于降低使用风险，也为插件作者提供了明确的最佳实践指引。

## 功能需求趋势

基于当前有限的 Issue/PR 样本，可观察到以下需求方向：

1. **任务生命周期与资源回收**（#2615）：子代理在超时/终止后的行为必须与终态标记严格一致，不允许继续产生资源消耗。
2. **配额与成本可见性**（#2615）：后台任务引发的 LLM 调用需要被完整追踪，用户需要能随时发现"隐形消耗"。
3. **插件安全机制**（#2614）：随着插件工具以本地子进程运行，权限边界、凭证存储和数据持久化正在成为重点完善方向。

## 开发者关注点

- **任务终止的确定性**：一旦任务被标记为 `timed_out` 或 `killed`，所有相关子任务与资源占用应立即终止，不应存在"终止后仍在运行"的例外。
- **后台任务的可观测性**：后台子代理的每次 LLM 调用都应为用户所见，避免出现跟踪系统之外的黑盒消耗。
- **`TaskStop` 的强制力**：用户期望 `TaskStop` 对终态标记的任务仍然有效，当前行为与直觉预期不一致，是明确的功能缺陷。
- **插件凭证安全**：使用 `inject` 注入密钥等敏感信息时，开发者需要清晰的防泄漏指引，避免因不当日志或误提交导致凭证泄露。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报（2026-08-22）

## 1. 今日速览

过去 24 小时，OpenCode 连续发布了 v1.18.20 与 v1.18.21 两个补丁版本，重点修复了网络错误重试、未知 finish reason 导致会话提前结束等稳定性问题。社区侧最受关注的议题是「是否支持禁用流式模式」（#785，31 评论 / 38 👍）以及多个会话静默停止/随机停止的报告。PR 活跃度高，核心稳定性、MCP 可管理性和 Windows 平台适配是当下开发主力方向。

## 2. 版本发布

### v1.18.21
**Core Bugfixes**
- 当模型返回未知 finish reason 时，继续响应而不是提前停止（与 #41469 相关）
- Vertex AI `eu` / `us` 多区域 Gemini 请求改走 REP 端点

**Desktop Bugfixes**
- 文件搜索加载期间保持已有搜索结果可见

### v1.18.20
**Core Bugfixes**
- 失败的 subagent 工具调用以可恢复的 `task_id` 形式呈现
- 对 `finish_reason: network_error` 的响应自动重试
- 扩展对 `network-error` / `network_error` 等网络错误变体的重试
- 展示可

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-22

## 今日速览

- 发布 v0.21.14 nightly 版本，重点改进 review 循环的反馈机制（明确告知作者未收敛原因）并修复 CI 回退逻辑；同时 SWE-bench Verified 与 Terminal-Bench 完整基准测试成功通过。
- 社区安全讨论热度上升：#9556 围绕「CI 是否应继续以调用用户身份执行代码」引发 7 条评论；#9089 的 PAT 凭证与不受信任分支代码共享主机问题进入修复阶段。
- 兼容性修复落地：针对 Ubuntu 22.04 Git 2.34.1 与 Qwen Code 要求 Git ≥2.37 的冲突，PR #9690 已提供安全的匿名降级方案，问题 #8993 随之关闭。

## 版本发布

### v0.21.14-nightly.20260821.9f2342d323
- **feat(review)**：当 review 循环无法收敛时，直接向作者说明原因，减少反复试错。
- **fix(ci)**：停止回退 nightly CI（避免回退引发的不稳定）。

### dsw-eas-tb-smoke-20260821-r1（SWE + Terminal-Bench 冒烟测试）
- **状态**：SUCCEEDED
- 覆盖 1 个 SWE-bench Verified 用例 + 1 个 Terminal-Bench 用例，用于验证发布触发的 DSW Harbor 执行链路与 GitHub Release 回写。

### dsw-eas-full-20260821-r1（完整基准测试）
- **状态**：SUCCEEDED
- SWE-bench Verified **500 个用例** + Terminal-Bench 2.0 **89 个用例**全部完成，包含验证器支持的结果与轨迹回写。

---

## 社区热点 Issues（Top 10）

### 1. #9556 [安全/CI-CD] 是否继续以调用用户身份授予代码执行权限
- **评论 7** | 作者 @wenshao | 更新 2026-08-21
- **为什么重要**：围绕 #9221 历经 20 轮 review 后，所有未解决发现都指向「代码以 review 自身用户身份执行」这一前置事实。该权限并非 #9221 引入，而是更早阶段授予，涉及 CI 安全边界设计。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9556)

### 2. #5180 [Bug/多代理] 子代理任务执行一半崩溃
- **评论 7** | 作者 @wunan067830-west | 更新 2026-08-21
- **为什么重要**：用户以主会话派发任务，subagent 执行中途崩溃，影响复杂多代理流程稳定性。会话长达 12 小时的分析数据为定位提供了充分线索。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/5180)

### 3. #8993 [已关闭] Git 2.37 要求 vs Ubuntu 22.04 仅提供 2.34.1
- **评论 6** | 作者 @callmeYe | 更新 2026-08-21
- **为什么重要**：公共 Git 扩展安装强制 Git ≥2.37，但 Ubuntu 22.04 LTS 官方源仍为 2.34.1，导致大量用户无法正常安装扩展。已由 PR #9690 修复并闭环。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/8993)

### 4. #5966 [Bug/UI] 中文输入法完全失效且不定期 UI 错误
- **评论 6** | 作者 @aspnmy | 更新 2026-08-21
- **为什么重要**：中文用户核心痛点，输入法失效严重影响日常使用，且界面上无报错、难以定位。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/5966)

### 5. #9089 [已关闭] PAT 作业与不受信任分支代码共享主机
- **评论 6** | 作者 @wenshao | 更新 2026-08-21
- **为什么重要**：autofix 流水线中持有 PAT 的作业与不受信任的分支代码运行在同一主机，存在凭据泄露风险，需 runner 级隔离。属于安全关键议题。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9089)

### 6. #9693 [Bug/Windows/MCP] 桌面版启动时报 MCP -32000 Connection closed
- **评论 4** | 作者 @Gui8092 | 更新 2026-08-21
- **为什么重要**：Windows 上即使未激活 MCP，Qwen Desktop 也会抛出 STDIO 传输连接关闭错误，影响所有 Windows 用户。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9693)

### 7. #9639 [安全] 自动模式权限分类器在提供商不稳定时故障开放
- **评论 3** | 作者 @Gauss2024 | 更新 2026-08-21
- **为什么重要**：分类器降级为「fail-open」，在模型提供商不稳定期间可能放行未授权操作，是 #7331 的回归，涉及安全底线。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9639)

### 8. #2862 [Bug] 启用 checkpointing 后启动卡在 "Initializing..."
- **评论 3** | 作者 @za-songguo | 更新 2026-08-21
- **为什么重要**：基础功能可用性问题。开启检查点功能即无法启动，必须强制退出，影响依赖该功能的用户。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/2862)

### 9. #379 [Bug/MCP] 复杂工具参数被序列化为 JSON 字符串而非原生类型
- **评论 3** | 作者 @luanweslley77 | 更新 2026-08-21
- **为什么重要**：MCP stdio 客户端将列表/对象参数序列化为字符串，违反 JSON-RPC 通信规范，导致复杂工具调用异常，属于 MCP 互操作老问题。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/379)

### 10. #9487 [Bug/Web Shell] 长任务期间加载指示器状态不一致
- **评论 3** | 作者 @yiliang114 | 更新 2026-08-21
- **为什么重要**：To Do 面板 spinner 持续转动，但会话加载指示器提前消失，前端状态管理缺陷影响长任务的可观察性。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9487)

---

## 重要 PR 进展（Top 10）

### 1. #9690 fix(core): 支持旧 Git 下的公共 GitHub 扩展安装
- **作者 @yiliang114** | 更新 2026-08-21
- **内容**：系统 Git 低于 2.37 时，通过解析 GitHub ref 为不可变 commit，再经现有公共下载通道安全拉取，而非放宽 Git 传输限制。直接解决 #8993。
- [查看 PR](https://github.com/QwenLM/qwen-code/pull/9690)

###

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*