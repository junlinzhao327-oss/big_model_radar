# AI CLI 工具社区动态日报 2026-08-08

> 生成时间: 2026-08-07 22:35 UTC | 覆盖工具: 7 个

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

# AI CLI 工具横向对比分析报告（2026-08-08）

## 1. 生态全景

AI CLI 工具已从单一对话式编程助手演进为多Agent协作、多端接入、可编程扩展的完整开发平台。头部工具均保持高频迭代节奏——Gemini CLI 单日发布 3 个版本，Claude Code 与 Qwen Code 均有正式版新功能落地（自托管运行环境、移除任务轮数上限）。安全与稳定性问题开始取代基础功能缺失，成为社区最集中的反馈方向：子代理挂起/误报、SSRF 漏洞、编码损坏、计费争议等高频出现——行业正从"能做"迈向"可靠、安全、可控"。同时，商业化路径明显分化：SaaS 订阅制（OpenCode Go、Claude Team/Enterprise）与开放生态整合（Qwen 接入 Kimi/MiMo、多模型聚合）并进。

## 2. 各工具活跃度对比

| 工具 | Issues（精选/总数） | PR 数 | Release 数 | 备注 |
|---|---|---|---|---|
| **Claude Code** | 10 个精选 | 3 个 | 1 个（v2.1.224） | 头条 issue 达 191 👍 / 73 评论，社区参与度最高 |
| **Gemini CLI** | 10 个精选 | 10 个 | 3 个（stable/preview/nightly） | 含 2 项安全修复（SSRF CVSS 8.6、Node 20→22） |
| **OpenCode** | 10 个精选 | 10 个 | 1 个（v1.18.15） | 话题集中在 Go 订阅服务稳定性与计费 |
| **Qwen Code** | 10 个精选 | 10 个 | 2 个（正式版 + nightly） | 含 Kimi/MiMo 认证、飞书集成、浏览器控制等大型功能 |
| **Kimi Code CLI** | 2 个（全部） | 2 个（跟进修复） | 0 个 | 样本量较小，但两个 issue 均属高危（编码损坏、误删目录） |
| **OpenAI Codex** | — | — | — | 本期无社区动态数据 |
| **GitHub Copilot CLI** | — | — | — | 本期无社区动态数据 |

## 3. 共同关注的功能方向

**① 长时任务与会话连续性**（热度最高）
- Claude Code：`#13354` 要求会话达上限后自动继续，191 👍 为全榜最高。
- Qwen Code：v0.21.7 移除 Goals 50 轮上限，支持跨轮恢复执行。
- Gemini CLI：子代理 MAX_TURNS 后误报成功（#22323）、通用代理无限挂起（#21409）。
- 共性诉求：Agent 应能自主管理长任务生命周期，而非在上下文边界中断等待人工干预。

**② 安全边界与权限管控**
- Gemini CLI：修复 SSRF 绕过（#28725，CVSS 8.6）、沙箱升级 Node 22（#28726）、子代理绕过权限配置（#22093）。
- Kimi Code：yolo 模式 `rm -rf` 误删工作区外真实目录（#2596）。
- Claude Code：插件脚本 YAML 注入与符号链接凭据覆写防护（#84711）、bash 自动审批 allowlist 文档缺失（#31675）、安全审查误报（#70458）。
- 共性诉求：工具的每一步文件系统操作和命令执行都必须在明确边界内进行，安全机制不能误伤正常开发流。

**③ 多端与远程运行体验**
- Claude Code：新增 `self-hosted-runner`，将自有机器/容器变为 Web/移动/桌面端会话运行环境。
- Qwen Code：围绕 Web Shell 构建桌面应用（#8092）、修复 Desktop Windows 崩溃、Chrome WebBridge 直接浏览器控制。
- Gemini CLI：修复 IDE 连接目录不匹配（#28729）。
- 共性诉求：CLI 不再局限于本地终端，而是向桌面应用、IDE、移动端、远端容器等多入口形态延伸。

**④ 模型接入透明度与兼容性**
- OpenCode：deepseek-v4-flash 实际返回 V3.2（#40409，High 严重级别）、`reasoning_content` 回传报错（#24334）。
- Claude Code：Fable 5 文本渲染回归（#81853）。
- Gemini CLI：新增 3.6 Flash 与 3.5 Flash-Lite 模型配置（#28673）。
- 共性诉求：模型版本标识透明、推理格式兼容稳定，并对新模型能力差异有明确预期管理。

**⑤ 可观测性与运维标准化**
- Qwen Code：遥测对齐 OpenTelemetry 会话生命周期（#8616）、增加运行时/客户端归因（#8660）。
- Claude Code：Analytics 数据停滞引发社区对服务健康度的质疑（#64503）。
- OpenCode：Go 计划用量计费与实际消耗不符（#41146）。
- 共性诉求：用户要求用量可查、配额可预期、遥测数据标准化且可审计。

## 4. 差异化定位分析

| 工具 | 功能侧重 | 目标用户 | 技术路线 |
|---|---|---|---|
| **Claude Code** | 企业级能力最完整：

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)



---

# Claude Code 社区动态日报 — 2026-08-08

## 今日速览

Claude Code 发布 v2.1.224，新增 `self-hosted-runner` 自托管环境能力与 `archive` 插件源，将 Claude Code 会话运行环境扩展至用户自有机器。社区方面，Issue #13354（会话限制后继续）以 191 👍 / 73 评论持续霸榜，是当前社区最强烈的功能诉求；Fable 5 文本渲染 bug 与 KVM 环境 100% CPU 问题成为今日最受关注的新增缺陷。

## 版本发布

### v2.1.224
- 新增自托管环境：`claude self-hosted-runner` 可将自有机器或容器转化为 Claude Code Web/移动/桌面会话的运行环境（Team 与 Enterprise 套餐可用）
- 新增 `archive` 插件源：支持通过 HTTPS 从 zip 包安装插件，无需经过 git

https://github.com/anthropics/claude-code/releases/tag/v2.1.224

## 社区热点 Issues（10 个精选）

### 1. [FEATURE] 会话达到限制后自动继续 — #13354
**🔥 191 👍 / 73 评论 | OPEN | 作者 @massyn**

社区热度最高的长期需求：当会话达到上下文限制时，用户希望 Claude Code 能自动开启新会话并继续当前任务，而不是中断等待手动操作。

https://github.com/anthropics/claude-code/issues/13354

### 2. [BUG] Fable 5 文本与工具调用同响应时文本不显示 — #81853
**3 👍 / 5 评论 | OPEN | 作者 @rhv-resideo**

使用 `claude-fable-5` 模型时，同时包含文本和工具调用的响应在终端中只显示工具调用，文本部分在正常视图中消失（Ctrl+O 转录详情中仍可看到）。同一设置在 Opus 4.8 下工作正常。

https://github.com/anthropics/claude-code/issues/81853

### 3. [BUG] Claude Code ≥2.1.205 在 KVM 虚拟机 100% CPU 死锁 — #77208
**0 👍 / 3 评论 | OPEN | 作者 @joos81**

kvm64 通用 CPU 模型的 KVM 客户机上，Claude Code 从 2.1.205 起即使执行 `--version` 也会 100% CPU 运行且无任何输出，同时导致 Linux 桌面 beta 的 Code 标签页静默失效。影响 CI 环境与虚拟化部署。

https://github.com/anthropics/claude-code/issues/77208

### 4. [BUG] Claude Code Analytics 自 5 月 12 日起未更新 — #64503
**6 👍 / 5 评论 | CLOSED | 作者 @bdavj**

官方分析页面数据停滞，社区对数据透明性和服务可观测性表达关注。已关闭，但反映了用户对官方运营指标可见性的需求。

https://github.com/anthropics/claude-code/issues/64503

### 5. [BUG] iOS App 打开 Remote Control 会话硬崩溃 — #70165
**2 👍 / 10 评论 | CLOSED | 作者 @atrusniak-ruz**

iOS 1.260618.0 在打开远程控制会话时主线程 Swift KeyPath 元数据栈溢出导致崩溃，涉及移动端与桌面端联动场景稳定性。

https://github.com/anthropics/claude-code/issues/70165

### 6. [FEATURE] BeforeModel / AfterModel Hook 拦截 LLM 请求与响应 — #21531
**3 👍 / 9 评论 | CLOSED | 作者 @coygeek**

提议在模型调用前后增加 Hook 拦截点，用于成本控制、安全审计与请求/响应改写。该需求涉及 core/security/cost 多个核心区域，说明社区对细粒度管控能力的关注。

https://github.com/anthropics/claude-code/issues/21531

### 7. [RFC] 异步/事件驱动通信成为 Claude Code 代理的一等能力 — #55981
**0 👍 / 5 评论 | CLOSED | 作者 @abaumanndev**

以 RFC 形式提出将异步事件驱动通信作为 agent 底层能力，跳出当前同步调用框架。虽然关闭，但代表社区对 agent 架构演进方向的探索。

https://github.com/anthropics/claude-code/issues/55981

### 8. [DOCS] bash 自动审批 allowlist 枚举缺失 — #31675
**4 👍 / 6 评论 | CLOSED | 作者 @coygeek**

`settings.md` 中 `autoAllowBashIfSandboxed` 仅引用 sandbox 配置，但未列出完整的 bash 自动批准 allowlist 枚举规则。权限配置文档不清晰会直接导致用户安全配置困难。

https://github.com/anthropics/claude-code/issues/31675

### 9. [BUG] 安全审查误报正常指令 — #70458
**0 👍 / 4 评论 | CLOSED | 作者 @MrJoy**

模型将“跳过读取某文件夹”这类正常指令误判为违反使用条款，社区认为当前安全审查过于敏感，影响实际开发效率。

https://github.com/anthropics/claude-code/issues/70458

### 10. [ENHANCEMENT] Code 标签页批量删除会话 — #70409
**0 👍 / 2 评论 | CLOSED | 作者 @dicksonsam**

桌面应用 Code 标签页无法批量选择/删除服务端会话，且未提交过提示词的空会话也会被持久化。多端同步场景下的会话管理体验问题。

https://github.com/anthropics/claude-code/issues/70409

## 重要 PR 进展

过去 24 小时内共 3 个 PR，全部列出如下：

### 1. docs: 修复 bash_command_validator_example.py 过期 hooks 文档链接 — #84854
**OPEN | 作者 @cassiacarollinee-ship-it**

示例脚本仍链接到旧的 `docs.anthropic.com` 域名，仓库中其他 46 处链接均已迁移至 `code.claude.com`。属文档一致性清理。

https://github.com/anthropics/claude-code/pull/84854

### 2. fix(hookify): 强制规则评估作用域与安全文件读取 — #84747
**OPEN | 作者 @alifakbxr**

修复 `hookify` 插件两处安全逻辑缺陷：`load_rules()` 在 `event` 为 None 时绕过事件过滤器，导致 `Read`、`Browser` 等未映射工具触发所有作用域规则；同时加固文件读取安全边界。

https://github.com/anthropics/claude-code/pull/84747

### 3. fix(security): 插件脚本 YAML 注入与符号链接凭据覆写防护 — #84711
**OPEN | 作者 @alifakbxr**

修复 #76580。新增防御性检查，防止 YAML 注入攻击与通过符号链接覆写凭据文件，属插件供应链安全加固。

https://github.com/anthropics/claude-code/pull/84711

## 功能需求趋势

从当前 Issues 中可提炼出社区五大关注方向：

1. **会话连续性与长任务管理**：以 #13354（会话限制继续）为代表，用户强烈需要长时任务的无人值守处理能力，是目前绝对热度第一的诉求。
2. **Hook 与扩展机制深化**：BeforeModel/AfterModel 拦截、异步事件驱动一等能力等需求表明，社区不再满足于现有工具级 Hook，而是追求模型调用级和架构级的可编程性。
3. **Web/桌面/移动多端体验打磨**：iOS Remote Control 崩溃、Code 标签页会话管理、bridge session 重连文档过时等，反映多端同步场景正在成为用户日常使用的重要组成部分。
4. **权限与安全管控精细化**：bash 自动审批 allowlist 枚举、`--mcp-config` 受策略约束的文档澄清、插件供应链安全修复，说明企业级安全配置和插件生态安全是用户重点关注方向。
5. **文档同步严重滞后**：约 20 条由 @coygeek 提交的文档类 Issue（hooks 工具名列表不全、`awsAuthRefresh` 超时未记录、Agent SDK `activeForm` 过时等）均被标记 stale 关闭，社区对文档更新速度有明确不满。

## 开发者关注点

- **新模型 Fable 5 引入的渲染回归**（#81853 文本不显示）是当前最受关注的新模型问题，开发者对 Opus 4.8 正常而 Fable 5 异常的兼容性差异较为敏感。
- **虚拟化环境稳定性**：#77208 的 KVM 100% CPU 死锁对 CI/CD 场景影响严重，且 2.1.205 起引入的回归已持续近一个月未获官方回应，相关开发者反馈强烈。
- **安全审查误报干扰正常开发流**（#70458）：安全机制过于激进会打断开发节奏，社区希望 Anthropic 在安全与可用性之间取得更好平衡。
- **文档过期而非功能缺失**：大量 stale 文档 Issue 的核心诉求并非新功能，而是功能已变但文档未更新的问题。开发者希望文档能与版本发布同步迭代。
- **官方数据透明度**：Analytics 面板长时间不更新引发社区对服务健康度的猜测，开发者希望获取更可靠的官方运行状态信号。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-08

## 今日速览

昨日 Gemini CLI 发布了 3 个版本（v0.54.4 稳定版补丁、v0.55.0-preview.2 和 v0.56.0-nightly），其中 v0.54.4 为稳定分支的精选修复。社区方面，子代理在达到 MAX_TURNS 后误报 GOAL 成功的问题（#22323）和通用代理持续挂起（#21409）仍是开发者关注焦点。此外，两项安全相关 PR 于昨日提交：web-fetch 工具的 SSRF 漏洞修复（CVSS 8.6）与沙箱 Dockerfile 升级至 Node 22。

---

## 版本发布

### v0.54.4（稳定版补丁）
- 通过 cherry-pick 将 56f9688 提交应用到 v0.54.0 分支，修复了特定问题并发布为 v0.54.1 版本，随后版本号提升至 0.54.2
- 适合生产环境使用者更新

🔗 https://github.com/google-gemini/gemini-cli/releases

### v0.55.0-preview.2
- 对 v0.55.0-preview.1 分支进行精选修复（cherry-pick 2139b12），创建补丁版本 v0.55.0-preview.2
- 包含变更日志更新

🔗 https://github.com/google-gemini/gemini-cli/releases

### v0.56.0-nightly.20260807.gd5c9a97dc
- 更新变更日志至 v0.55.0-preview.1 和 v0.54
- 版本号提升至 0.56.0-nightly.20260806

🔗 https://github.com/google-gemini/gemini-cli/releases

---

## 社区热点 Issues（10 个）

### 1. 子代理 MAX_TURNS 后被误报为 GOAL 成功 ⭐ P1
**#22323** | 评论: 12 | 👍: 2

`codebase_investigator` 子代理在达到最大轮次限制后仍返回 `status: "success"`，实际上并未执行任何分析。导致用户收到误导性的成功反馈，掩盖了真正的中断原因。社区已讨论近 5 个月，处于 need-retesting 状态。

🔗 https://github.com/google-gemini/gemini-cli/issues/22323

### 2. 通用代理（Generalist agent）无限挂起 ⭐ P1
**#21409** | 评论: 8 | 👍: 8

当 Gemini CLI 委派任务给通用代理时，即使创建文件夹等简单操作也可能无限期挂起（最长等待 1 小时）。用户通过指示模型不委派给子代理可暂时绕过。拥有 8 个 👍，是社区影响面较大的问题。

🔗 https://github.com/google-gemini/gemini-cli/issues/21409

### 3. Shell 命令执行完成后卡在 "Waiting input" ⭐ P1
**#25166** | 评论: 4 | 👍: 3

Gemini 执行简单 CLI 命令后频繁卡住，显示命令仍在执行并等待用户输入，但进程实际已完成。影响日常开发效率，被标记为 effort/medium，社区有 3 个 👍。

🔗 https://github.com/google-gemini/gemini-cli/issues/25166

### 4. 浏览器子代理在 Wayland 环境下失败 ⭐ P1
**#21983** | 评论: 4 | 👍: 1

Browser subagent 在 Wayland 显示服务器下无法正常工作，返回 GOAL 终止原因但实际失败。影响 Linux 用户群体。

🔗 https://github.com/google-gemini/gemini-cli/issues/21983

### 5. get-shit-done 输出钩子导致崩溃 ⭐ P1
**#22186** | 评论: 3

当 get-shit-done 模式输出接近完成（打印用户摘要）时，反复崩溃。处于 need-information 状态，可能是钩子与终端渲染层的竞争条件。

🔗 https://github.com/google-gemini/gemini-cli/issues/22186

### 6. Gemini 不会主动使用 skills 和 sub-agents
**#21968** | 评论: 6

用户反馈 Gemini 不会主动调用自定义 skills 和子代理，即使提供了详细描述（如 gradle、git skills），只有在显式指示时才会使用。影响自动化效率。

🔗 https://github.com/google-gemini/gemini-cli/issues/21968

### 7. 组件级行为评估体系（EPIC）⭐ P1
**#24353** | 评论: 7

跟踪行为评估测试体系的后续进展——目前已有 76 个评估测试覆盖 6 个支持的 Gemini 模型，目标是建立更健壮的组件级评估能力。这是维护者关注的长期质量基础设施。

🔗 https://github.com/google-gemini/gemini-cli/issues/24353

### 8. 超过 128 个工具时出现 400 错误
**#24246** | 评论: 3

当可用工具数量过多（>128）时，Gemini CLI 遇到 400 错误。用户期望代理能更智能地限制工具范围。

🔗 https://github.com/google-gemini/gemini-cli/issues/24246

### 9. Auto Memory 对低信号会话的无限重试
**#26522** | 评论: 5

Auto Memory 仅当提取代理成功使用 `read_file` 读取会话记录后才将其标记为已处理。如果代理判断会话信号低而决定不读取，该会话将保持未处理状态，可能被无限重试。

🔗 https://github.com/google-gemini/gemini-cli/issues/26522

### 10. 子代理在 v0.33.0 后绕过权限设置运行
**#22093** | 评论: 3

自 v0.33.0 起，即使用户在所有配置中禁用了 agents 模式，子代理（如 generalist）仍会被自动调用。用户预期禁用后不应启用子代理。

🔗 https://github.com/google-gemini/gemini-cli/issues/22093

---

## 重要 PR 进展（10 个）

### 1. 修复 web-fetch 的 SSRF 漏洞（DNS 解析绕过）🔥 安全
**#28725** | priority/p1, area/security

修复 CVSS 8.6 的 SSRF 漏洞。恶意用户可通过自定义域名指向私有/回环 IP（如 `169.254.169.254`）绕过 DNS 保护。属于关键安全修复。

🔗 https://github.com/google-gemini/gemini-cli/pull/28725

### 2. 沙箱 Dockerfile 升级至 Node 22-slim 🔥 安全
**#28726** | priority/p1, area/security

将沙箱及所有 Cloud Run Dockerfile 从 `node:20-slim` 升级至 `node:22-slim`。Node 20 已至 EOL，不再接收安全修复（如近期 CVE 仅修复于 Node 22/24/26）。

🔗 https://github.com/google-gemini/gemini-cli/pull/28726

### 3. 新增 Gemini 3.6 Flash 和 3.5 Flash-Lite 模型配置
**#28673** | priority/p2, size/l

为核心包添加 Gemini 3.6 Flash 与 3.5 Flash-Lite 的模型配置，包括模型解析、能力配置（thinking、multimodalToolUse）、别名和 Code 相关能力。

🔗 https://github.com/google-gemini/gemini-cli/pull/28673

### 4. 修复虚假模型容量耗尽报错与配额映射
**#28730** | size/m

解决 CLI 中虚假的模型容量耗尽错误信息，修正核心包中客户端模型配额查找映射，并确保 "Keep trying" 选项在瞬时容量激增时保留在 UI 中。

🔗 https://github.com/google-gemini/gemini-cli/pull/28730

### 5. 修复 IDE 连接中的目录不匹配问题
**#28729** | size/m

解决在 Cider 或任何 VS Code fork/远程工作区（使用虚拟/不同 FUSE 或目录路径）下，Gemini CLI 无法连接到 IDE 扩展的问题。

🔗 https://github.com/google-gemini/gemini-cli/pull/28729

### 6. 修复设置加载顺序竞态条件
**#28597** | priority/p2, size/l

修复设置生命周期中的加载顺序竞态：之前系统/用户/工作区设置文件在启动时被立即解析并展开 `process.env`，但本地 `.env` 文件尚未加载，导致占位符解析失败。

🔗 https://github.com/google-gemini/gemini-cli/pull/28597

### 7. 防止 diff hunk 标记被误认为 @file 引用
**#28581** | priority/p2, area/core+agent

修复联合 diff hunk 标记被错误解释为 `@file` 引用的问题，消除大 diff 提示中每次 hunk 的递归工作区搜索，防止 `minimatch`/`path-scurry` 在大 diff 场景下的堆增长。

🔗 https://github.com/google-gemini/gemini-cli/pull/28581

### 8. Caretaker Agent：Cloud Run 评测运行器入口
**#28727** | size/m

新增 Cloud Run Job 入口、GCS 产物同步助手及容器定义，用于在 Google Cloud Run 上执行 Caretaker 分诊评估套件。

🔗 https://github.com/google-gemini/gemini-cli/pull/28727

### 9. Caretaker Agent：发布 ready-for-code Pub/Sub 事件
**#28588** | size/m

在 issue 成功分诊（`status: "TRIAGED"`）后发布事件负载（含 `github_metadata` 和 `workable_spec`），通知下游自动化工作流（如代码生成）。

🔗 https://github.com/google-gemini/gemini-cli/pull/28588

### 10. Caretaker Triage：提示词爬山优化与编排器更新
**#28524** | size/m

整合 3 周的提示词爬山和评估调优结果，引入专门的 `code_explorer` 技能，并从评估中取得显著的质量提升。

🔗 https://github.com/google-gemini/gemini-cli/pull/28524

---

## 功能需求趋势

从过去 24 小时的 Issues 和 PR 中可提炼出以下社区关注方向：

### 1. 子代理系统可靠性与可控性
- **误报/伪成功**: 子代理在到达 MAX_TURNS 后被误报为 GOAL 成功（#22323）
- **挂起/卡死**: 通用代理无限挂起（#21409）、浏览器代理在 Wayland 失败（#21983）
- **绕过权限设置**: 子代理在用户禁用后仍被自动调用（#22093）
- 这是当前社区反馈最集中的领域

### 2. AST 感知的代码理解
- **#22745**: EPIC 跟踪 AST 感知文件读取/搜索/代码库映射的可行性研究
- **#22746**: 探索使用 AST 感知 CLI 工具进行代码库映射
- 方向为减少 token 消耗、提高代码定位精确度

### 3. Auto Memory 系统的稳定性与安全性
- **#26522**: 低信号会话无限重试问题
- **#26525**: 增加确定性脱敏并减少日志
- **#26523**: 无效内存补丁的表面化/隔离
- 记忆系统仍在早期阶段，安全性和稳定性是重点

### 4. 安全加固
- SSRF 修复（#28725）
- Node 20 → 22 升级（#28726）
- 社区对安全漏洞反应迅速，维护者也在积极修复

### 5. 新模型支持
- Gemini 3.6 Flash 与 3.5 Flash-Lite 的配置 PR（#28673），社区在期待更强模型的集成

### 6. 代理"自我意识"能力
- **#21432**: Agent 应准确了解自身的 CLI 标志、快捷键和自执行方式，能做自己的专家指南

---

## 开发者关注点

### 高频痛点

**1. 子代理稳定性是最大痛点**
- 多个 P1 级 bug 集中在子代理的挂起、误报和不遵守配置上。开发者对子代理的可靠性有明显的信任危机。

**2. 终端渲染与 Shell 交互问题频发**
- Shell 命令执行后卡死（#25166）、终端 resize 闪烁（#21924）、外部编辑器退出后渲染损坏（#24935）。终端体验类的 bug 反复出现，说明这一块的工程质量仍需打磨。

**3. 代理对工具和技能的利用率不足**
- Gemini 不主动使用自定义 skills（#21968）、模型在随机位置创建临时脚本（#23571）、工具数量过多时报 400（#24246）。开发者期望代理能更智能地选择工具。

**4. 破坏性行为的抑制需求**
- **#22672**: 代理使用 `git reset` 或 `--force` 等危险命令时，应更偏好安全替代方案，尤其在数据库等关键资源维护场景。这一需求有客户 issue 标签，说明已有真实用户受到影响。

### 值得注意的信号
- 大量问题被标记为 `🔒 maintainer only` + `workstream-rollup`，说明维护团队正在系统性地追踪和推进这些问题，子代理和记忆系统是当前的两大重点投入方向。
- 昨天集中合并了多个 Caretaker Agent（机器人运维）的 PR，该内部工具的基建正在快速完善中，对普通用户不可见但会提升未来的 issue 响应效率。

---

*本日报由 AI 技术分析师自动生成，数据来源：[github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-08-08

数据来源：github.com/MoonshotAI/kimi-cli

## 今日速览

今日无新版本发布。开发社区提交了 2 条重要 issue：#2591 暴露了 `StrReplaceFile` 编辑非 UTF-8 文件时会造成字节级损坏，并已催生两个修复 PR（#2594、#2595）同日跟进；#2596 则报告了 yolo 权限模式下 agent 误删工作区外真实目录的严重安全事件。两条 issue 分别指向文件数据完整性与命令执行安全边界，值得所有用户关注。

## 社区热点 Issues

> 本期数据窗口内仅 2 条活跃 issue，以下全部列出。

### #2591 StrReplaceFile 损坏编辑区域外的非 UTF-8 字节
- 作者：@shoemoney | 创建：2026-08-05 | 更新：2026-08-07 | 评论：3
- 链接：[https://github.com/MoonshotAI/kimi-cli/issues/2591](https://github.com/MoonshotAI/kimi-cli/issues/2591)

**摘要**：`StrReplaceFile` 在实现上使用 `errors="replace"` 解码整个文件，以字符串形式编辑后整体写回。任何不在编辑区域内的非法 UTF-8 字节——例如 GBK/GB2312 编码的中文注释、或二进制文件片段——都会被替换为 U+FFFD（`EF BF BD`），造成不可逆损坏。

**为什么重要**：国内有大量存量项目使用 GBK/GB2312 编码，这类文件只要被 `StrReplaceFile` 触碰，即使编辑位置与编码问题无关，整个文件也会被改写损坏。该 issue 创建后迅速催生两个修复 PR（#2594、#2595），说明维护者与社区都已确认这是高危缺陷。

### #2596 Agent 在执行 rm -rf 时误删工作区外真实目录
- 作者：@iMaxTomas | 创建：2026-08-07 | 更新：2026-08-07 | 评论：0
- 链接：[https://github.com/MoonshotAI/kimi-cli/issues/2596](https://github.com/MoonshotAI/kimi-cli/issues/2596)

**摘要**：在 yolo 权限模式下，用户要求 agent 清理它之前创建的 symlink `~/.pi/agent/sessions`。但该 symlink 创建时实际已失败（`ln -sfn` 落在了已存在的真实目录上），agent 未察觉，后续清理时对该路径执行 `rm -rf`，导致目录内用户会话数据被全部删除。

**为什么重要**：这是对 agent 文件系统操作

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报（2026-08-08）

## 今日速览

OpenCode Go 订阅服务成为社区热议焦点：#38257（Go 返回 401 上游拦截，45 条评论）和 #41146（Go 套餐被超额扣费）等事件持续发酵，用户对服务稳定性和计费准确性提出质疑。此外，DeepSeek V4 Flash 模型标识错误问题（#40409）引发对模型服务透明度的讨论。版本方面，v1.18.15 发布，修复了消息排序、回滚/分叉操作及截断清理等核心问题。

## 版本发布

**v1.18.15** 主要修复三项核心缺陷：
- 即使导入的或旧版消息 ID 乱序，也能保持消息时间顺序正确
- 回滚（revert）和分叉（fork）操作现在基于真实消息时间线而非消息 ID 排序
- 截断清理（truncation cleanup）通过文件时间戳更可靠地移除过期文件

## 社区热点 Issues

1. **[#38257] OpenCode Go 上游返回 401，chat/completions 被阻止**（45 评论，👍 11）
   OpenCode Go 订阅用户在调用 chat/completions 时全部收到 `401 Request blocked by upstream provider`，但 /v1/models 接口正常。用户认为是服务端问题，受影响的 Go 订阅用户众多。创建于 7 月 22 日，至今仍处于 OPEN 状态。
   https://github.com/anomalyco/opencode/issues/38257

2. **[#5359] 部分模型无法读取粘贴的图片**（18 评论）
   从 v1.0.137 开始，粘贴图片后 OpenCode 持续报告无法读取图片，v1.0.134 正常。涉及 LiteLLM + Vertex AI 后端，是较早的回归 bug，开发者长期受影响。
   https://github.com/anomalyco/opencode/issues/5359

3. **[#23153] 功能请求：支持加密货币支付 Go 订阅**（17 评论，👍 37）
   社区呼吁为 OpenCode Go 订阅增加加密支付方式。该请求是本期 issue 中获赞最多的功能请求，反映出对支付方式多样化的期待。
   https://github.com/anomalyco/opencode/issues/23153

4. **[#14332] Amazon Bedrock Opus 4.6 压缩失败**（16 评论，👍 8）
   压缩时报错：最新 assistant 消息中的 `thinking`/`redacted_thinking` 块不可修改，导致压缩操作失败。涉及 Bedrock 特有的 reasoning 内容处理问题。
   https://github.com/anomalyco/opencode/issues/14332

5. **[#40409] OpenCode Go 的 deepseek-v4-flash 实际不是 DeepSeek V4 Flash**（14 评论）
   用户购买的是 deepseek-v4-flash 0731，但实际返回的模型自称 V3.2、知识截止 2025-05。被标记为 High 严重级别，涉及计费与服务质量不符问题，已关闭。
   https://github.com/anomalyco/opencode/issues/40409

6. **[#6560] Windows/PowerShell 下 OpenCode 无法粘贴**（13 评论，👍 2）
   Windows 11 Pro 的 PowerShell 中打开 OpenCode 后右键粘贴和 Ctrl+V 均无效，只能输入文字。虽然已关闭，但该问题自 1 月起存在，Windows 用户受影响大。
   https://github.com/anomalyco/opencode/issues/6560

7. **[#24334] DeepSeek 思考模式报错：reasoning_content 必须回传**（10 评论，👍 2）
   使用 DeepSeek 模型 thinking 模式时，API 要求将 `reasoning_content` 原样回传，否则返回 400。反映 DeepSeek 特殊 reasoning 格式的兼容性问题。
   https://github.com/anomalyco/opencode/issues/24334

8. **[#8565] 功能请求：屏幕阅读器无障碍模式**（10 评论，👍 3）
   当前 TUI 的 Emoji、动画和 Unicode 字符对屏幕阅读器用户极不友好，社区请求增加无障碍模式，是重要的可访问性改进需求。
   https://github.com/anomalyco/opencode/issues/8565

9. **[#41146] Go 计划超额扣费：周限额在约 $7.50 时耗尽**（2 评论）
   用户使用 $10/月的 Go 计划，Usage 面板仅显示消费 $7.50 时周配额已达 100% 被阻断。与宣称的 $30 周限额严重不符，用户对计费系统准确性存疑。已关闭。
   https://github.com/anomalyco/opencode/issues/41146

10. **[#39376] 通过 prompt_skills 快捷键选择技能会清空输入草稿**（4 评论，👍 1）
    当输入框已有草稿文本时，使用 Ctrl+P 选择技能会立即调用 skill 工具并清空现有草稿。多技能工作流中被误操作的用户会丢失正在编辑的文本。
    https://github.com/anomalyco/opencode/issues/39376

## 重要 PR 进展

1. **[#35743] 修复：chunkTimeout 未应用于非 SSE 流式协议**
   原实现仅对 `text/event-stream` 响应生效，导致 AWS Bedrock（`application/vnd.amazon.eventstream`）等 EventStream 协议完全绕过 chunk 超时监控。
   https://github.com/anomalyco/opencode/pull/35743

2. **[#35796] 修复：清除 TUI 过期工具准备状态**
   为终端服务器投影被过期 pending 状态覆盖的问题添加回归测试；在刷新观察到完成的 assistant 消息时优先采用服务器投影，保留真实的活动状态。
   https://github.com/anomalyco/opencode/pull/35796

3. **[#35787] 功能：Bedrock provider 连接时提示选择区域**
   为 Bedrock 接入增加 AWS 区域提示，显著改善 Desktop 用户的连接体验。关闭 #28834。
   https://github.com/anomalyco/opencode/pull/35787

4. **[#35785] 重构：将 Code Mode 服务化**
   将 Code Mode 重构为 Location 作用域服务，支持嵌套的规范化工具源；通过 Effect 插件上下文注册，MCP 的注册和启用逻辑迁移到 Code Mode 域内。
   https://github.com/anomalyco/opencode/pull/35785

5. **[#35780] 功能：从 TUI 附加 MCP 资源**
   增加浏览器安全的 MCP 附件 URI（携带 server/resource 标识），在 Location 作用域的 Core 中解析 MCP 文本/blob 内容，并保留精确的重试语义和 MIME 嗅探。
   https://github.com/anomalyco/opencode/pull/35780

6. **[#35764] 功能：添加 planner/worker/reviewer 工作流**
   新增可选 `workflow` 配置，支持规划者（planner）、执行者（worker）和审查者（reviewer）分工协作的工作流模式。
   https://github.com/anomalyco/opencode/pull/35764

7. **[#35727] 修复：grep 精确文件路径搜索范围过大**
   当 grep 收到精确文件路径时，现在将文件名传给 ripgrep 适配器而非搜索整个路径，避免不必要的全库搜索。关闭 #35726。
   https://github.com/anomalyco/opencode/pull/35727

8. **[#35721] 修复：MCP remembered 资源读取范围扩大**
   read_mcp_resource 已要求精确资源模式，但 remember/always 选项使用了过宽的通配符。修复后确保记住的资源读取严格限定在原始精确模式内。关闭 #35720。
   https://github.com/anomalyco/opencode/pull/35721

9. **[#35715] 修复：Windows 文件监听路径反斜杠问题**
   `@parcel/watcher` 在 Windows 下发出原生反斜杠路径，现已规范化为正斜杠后再发布更新事件。关闭 #35329。
   https://github.com/anomalyco/opencode/pull/35715

10. **[#35699] 修复：超大行导致 grep 中止**
    当匹配行超过 64KiB（如压缩 bundle、base64、大数据行）时，grep 直接中止整个搜索，现在改为跳过超限行继续搜索。关闭 #35523。
    https://github.com/anomalyco/opencode/pull/35699

## 功能需求趋势

- **付费方式扩展**：社区对 OpenCode Go 的付费方式有明确诉求，加密货币支付获得 37 个 👍（#23153）。
- **可访问性与键盘操作**：屏幕阅读器支持（#8565）、Windows 粘贴问题（#6560）持续受关注。
- **模型透明性与兼容性**：DeepSeek/V4 Flash 模型标识与实际不符（#40409、#40607）、reasoning_content 格式兼容（#24334）、图片理解回归（#5359）等模型相关问题频繁出现。
- **会话与消息管理**：技能选择清空输入草稿（#39376）、回复生成期间新消息排队（#41106）、运行时为子代理覆盖模型（#17595）等会话/消息体验优化需求上升。
- **自定义与扩展能力**：Skill 子文件夹组织（#38853）、跳过 npm 安装的环境变量（#37888）、按会话配置工具可用性等（PR #35691），持续提升可扩展性。
- **故障排查能力**：Copilot 配额查看插件（PR #35769）等开发辅助工具被引入；部分 issue 也反映了开发者对用量统计透明度的诉求。

## 开发者关注点

- **OpenCode Go 服务的稳定性和计费准确性是当前最大痛点**：401 上游阻断（#38257）与周配额在消费约 $7.50 时即耗尽的计费问题（#41146）直接影响付费用户的核心使用。
- **模型服务标识与实际不符引发信任危机**：deepseek-v4-flash 返回 V3.x 的问题（#40409）被标记为“计费/质量不匹配”，官方 DeepSeek API 也存在同样问题（#40607）。
- **TUI 桌面体验问题高频出现**：Windows 粘贴失效（#6560）、新布局下 git 分支不可见（#41105）、通知权限不请求（#37120）、从源码非仓库目录运行时黑屏（#40231）等，桌面和终端体验完善空间较大。
- **安全与隐私防护意识增强**：有用户因本地 session 删除后无法执行 /unshare，紧急请求从远端服务器删除分享链接（#41124），期望增强分享数据生命周期管理。
- **Copilot 集成体验待优化**：OAuth 登录后模型不显示（#41088）、每次会话都被要求重新认证（#40183）等，与 Copilot 的联动体验存在明显问题。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报（2026-08-08）

## 今日速览

今日最大的变化是 **Qwen Code v0.21.7 正式发布**，移除了 Goals 功能的 50 轮对话限制，并支持在交互式 CLI 中渲染内联终端图片。社区方面，**桌面端（Desktop）在 Windows 平台的启动崩溃**（#8615）和**终端中文输入显示问题**（#8625）成为开发者反馈最集中的两个 bug，同时 **Web Shell 桌面化**（#8092）与 **Kimi/MiMo 第三方认证支持**（#8368）等方向获得了持续关注。

## 版本发布

### v0.21.7（正式版）
- **移除 Goals 50 轮上限**：任务现在可以跨过旧有的 50 轮边界，恢复后继续执行（[#8421](https://github.com/QwenLM/qwen-code/pull/8421)）
- **内联终端图片渲染**：交互式 CLI 支持渲染模型输出的内联终端图片（具体支持对象被截断，推测为 Kimi 或某终端协议）

### v0.21.7-nightly.20260807.fca8f3c1f
- `fix(ci): surface blocked autofix takeover admission`（[#8410](https://github.com/QwenLM/qwen-code/pull/8410)），修复 CI 中 autofix takeover 被阻塞时无提示的问题

---

## 社区热点 Issues（10 个）

### 1. #3203 Qwen OAuth 免费额度策略调整（150 条评论）
[链接](https://github.com/QwenLM/qwen-code/issues/3203)  
社区讨论最激烈的一个 issue。提议将每日免费配额从 1000 次请求降至 100 次，并在 2026 年 8 月 20 日完全关闭免费入口。该 issue 虽已关闭，但长期占据讨论榜，反映大量用户依赖免费额度。CLOSED 状态但仍有 150 条评论，说明争议较大。

### 2. #8615 [Desktop 0.1.0 / Windows] 启动时崩溃：EISDIR lstat 'C:'（5 条评论）
[链接](https://github.com/QwenLM/qwen-code/issues/8615)  
Desktop 版 v0.1.0 在 Windows 上打开工作区时崩溃，打包的 Node.js v22.20.0 报 `EISDIR lstat 'C:'` 错误。P1 优先级、已关闭。是桌面端刚推出不久的关键平台 bug。

### 3. #8625 Windows 终端输入中文时显示拼音看不清（6 条评论）
[链接](https://github.com/QwenLM/qwen-code/issues/8625)  
Windows 终端中输入中文时，候选拼音和文字混在一起看不清，影响使用。**欢迎 PR**。这是中文用户高频反馈的输入法兼容问题。

### 4. #8092 围绕 Web Shell 构建低维护成本的桌面应用（5 条评论）
[链接](https://github.com/QwenLM/qwen-code/issues/8092)  
社区提议复用 Web Shell 作为桌面端主界面，避免维护两套独立 UI。这反映了对桌面端体验和降低维护成本的双重诉求。Open 状态，仍在讨论中。

### 5. #8562 tmux 中闪屏（5 条评论）
[链接](https://github.com/QwenLM/qwen-code/issues/8562)  
通过 iTerm2 + SSH 连接 Ubuntu 服务器，在 tmux 分屏中对话时屏幕闪烁。用户用 Qwen 3.8 Max 排查后认为与 Qwen Code 版本有关。同类问题在 web 终端场景也有报告（#8659），指向了 TUI 渲染兼容性。

### 6. #8660 为遥测添加运行时和客户端归因（5 条评论）
[链接](https://github.com/QwenLM/qwen-code/issues/8660)  
希望为 usage-statistics 添加稳定的运行环境和客户端来源信息。当前只有 `channel` 字段区分入口，VS Code 扩展和 CLI 的遥测数据无法准确归因。体现了可观测性需求的前沿化。

### 7. #8550 `qwen mcp list` 在 SSE 服务器慢速/无响应时无限挂起（4 条评论）
[链接](https://github.com/QwenLM/qwen-code/issues/8550)  
当 MCP 服务器使用 SSE 传输但连接建立后不发送 `endpoint` 事件时，`qwen mcp list` 永久阻塞。已关闭并标记为 ready-for-agent，说明已有修复方案或正在修复。

### 8. #8593 Desktop 中 Markdown 链接点击无效（4 条评论）
[链接](https://github.com/QwenLM/qwen-code/issues/8593)  
Desktop 中 assistant 消息里的 Markdown 链接显示为可点击样式，但点击后既不开浏览器也不出现内置浏览器面板，静默失败。P2，已关闭，是一个明显的桌面端交互缺失。

### 9. #6565 "糟糕！连接到 Qwen Coder 时出现问题。Internal Error"（10 条评论）
[链接](https://github.com/QwenLM/qwen-code/issues/6565)  
多语言界面下偶发 `Internal Error` 连接问题。虽然已关闭（状态为需要更多信息），但评论数高，说明不少用户遇到过。可能与认证或网络状态有关。

### 10. #7118 Windows 独立安装程序在 PowerShell 无法解析 Get-FileHash 时失败（4 条评论 / 3 👍）
[链接](https://github.com/QwenLM/qwen-code/issues/7118)  
SHA-256 校验步骤在 PowerShell 环境异常时直接失败，导致安装中断。社区反馈有 3 个 👍，欢迎 PR。Windows 安装体验的常见痛点。

---

## 重要 PR 进展（10 个）

### 1. #8614 feat(web-shell): 右侧 artifact 面板支持全屏视图
[链接](https://github.com/QwenLM/qwen-code/pull/8614)  
为 Web Shell 右侧 tab 面板添加展开/折叠按钮，支持全屏查看 artifacts、subagents、review changes 等。提升桌面化 UI 的使用体验。

### 2. #8675 feat(web-shell): 模型级推理控制
[链接](https://github.com/QwenLM/qwen-code/pull/8675)  
内置模型推理控制注册表，端到端应用于 Core、ACP、daemon、SDK 和 WebShell，支持 Thinking 和 Effort 控制及默认值。首个精确注册模型为 `qwen3.*` 系列，为后续模型差异化配置铺路。

### 3. #8368 feat(auth): 新增 Kimi 和 小米 MiMo 认证提供商
[链接](https://github.com/QwenLM/qwen-code/pull/8368)  
`/auth` 第三方提供商新增 Kimi（Coding Plan / API Key 中国 / API Key 国际）和小米 MiMo（按量付费，含中国/新加坡等区域）。进一步丰富多模型生态接入。

### 4. #8616 feat(telemetry): 对齐 OpenTelemetry 会话生命周期
[链接](https://github.com/QwenLM/qwen-code/pull/8616)  
为每个活跃会话发出标准 `session.start` / `session.end` LogRecord，包含 `event.name` 和 `session.id`；恢复持久会话时附带 `session.previous_id`。向标准可观测性协议靠拢。

### 5. #8578 feat(channels): 飞书富交互 ask-user 问题卡片
[链接](https://github.com/QwenLM/qwen-code/pull/8578)  
飞书渠道新增 Card V2 格式的 `ask_user_question` 交互，支持单选/多选表单并关联回调。提升飞书集成在企业场景中的可用性。

### 6. #8394 feat(review): Maven 多模块验证
[链接](https://github.com/QwenLM/qwen-code/pull/8394)  
`/review` 新增确定性 Maven 多模块验证：识别 root reactor、将变更文件映射到最深层默认模块、优先验证受影响模块。面向 Java 生态的重型项目。

### 7. #8588 feat(serve): 暴露活跃工作状态
[链接](https://github.com/QwenLM/qwen-code/pull/8588)  
`GET /health?deep=1` 新增 `activeWork`、`activeWorkReporting`、`activeWorkStaleMs` 字段。便于外部系统监控 daemon 当前是否有未决任务或运行中的后台 Agent。

### 8. #8682 feat(serve): 可轮询的 turn 状态端点
[链接](https://github.com/QwenLM/qwen-code/pull/8682)  
daemon HTTP API 新增 `GET /session/:sessionId/turns/:promptId` 和 `GET /session/:sessionId/turns/current`，支持轮询会话 turn 的生命周期和结果，方便外部客户端对接。

### 9. #8708 perf(review): 为 finder 和 auditor 简报添加软工具调用预算
[链接](https://github.com/QwenLM/qwen-code/pull/8708)  
`agentToolBudget` 以 `clamp(30 + effective/20, 30, 60)` 计算软上限，确保任何调用方无法无限放大工具调用量，是可审查性/资源控制的性能优化。

### 10. #8707 feat(chrome): Qwen WebBridge 直接浏览器控制
[链接](https://github.com/QwenLM/qwen-code/pull/8707)  
从 `qwen serve` 到 Qwen Chrome 扩展及用户真实 Chromium profile 的直接浏览器控制路径，兼容 Kimi WebBridge 的 `/command` 和 `/status` 端点，实现 17 种操作。浏览器自动化生态向前一步。

---

## 功能需求趋势

### 1. Desktop/Web Shell 一体化与交互增强
- 要求以 Web Shell 为核心构建桌面应用，降低维护成本（#8092）
- 桌面端补全链接点击（#8593）、面板全屏（#8614）、Composer 工具栏增强（#6699、#6701）等交互细节

### 2. 第三方模型与认证提供商扩展
- PR #8368 新增 Kimi、小米 MiMo；社区对多模型接入保持高度兴趣
- OAuth 免费额度策略引发长时间讨论（#3203），说明模型获取成本是社区关注的核心话题

### 3. 可观测性标准化：OTel 对齐、溯源归因
- 遥测数据需要对齐 OpenTelemetry 会话生命周期（#8616）
- 增加运行时和客户端归因（#8660）
- `OTEL_METRICS_EXPORTER=otlp` 环境变量导致指标静默失效（#8697）引发了社区反馈

### 4. 浏览器自动化能力（WebBridge）
- 提议通过 HTTP 桥接 `qwen serve` 与 Chrome 扩展，提供类似 Kimi WebBridge 的 17 种操作（#8699、#8707）
- 社区希望浏览器控制不依赖 MCP，降低使用门槛

### 5. 多模态与长时任务可靠性（omni-exp 实验）
- Omni 多模态接入实验总纲（#8197）和 S3 投递可靠性设计（#8185）仍在推进，优先离线缓存与恢复，目标“用户无感重传”

### 6. 多语言/本地化社区支持
- 请求新增韩语文档站点（#8551），中文、日文等多语言 issue 频繁出现，说明用户已形成国际化社区

---

## 开发者关注点

### 1. 终端兼容性问题是最大痛点
- **中文输入显示**：Windows 终端拼音不可辨识（#8625）
- **闪烁/撕裂**：tmux 分屏闪烁（#8562）、Alibaba Workbench 等 web 终端闪烁（#8659）
- **鼠标操作回归**：PuTTY 下中键选择/复制失效（#8672）
- 这些问题的共性是指向 TUI 渲染层对终端能力检测（如 `COLORTERM`、TERM）和 Virtualized History 模式的兼容性需要加强

### 2. Windows 平台稳定性亟待改善
- 桌面版启动崩溃 `EISDIR lstat 'C:'`（#8615）
- 独立安装程序在 PowerShell 异常时失败（#7118）
- 客户端版本为 0.21.5 时即出现终端显示问题（#8625），说明全链路在 Windows 的测试覆盖不足

### 3. M

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*