# OpenClaw 生态日报 2026-09-12

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-11 22:35 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-09-12

## 1. 今日速览

过去 24 小时 OpenClaw 保持极高活跃度：Issues 更新 500 条（新开/活跃 277、已关闭 223），PR 更新 500 条（待合并 285、已合并/关闭 215），并发布新版本 **v2026.9.4**。版本核心能力是“兼容失败更新的回滚与恢复”，但该版本同时暴露出 release blocker：#144742 指出 2026.9.4 未包含 #144208，导致保留的 version-1 handoff lease 行会让每次配置写入失败。今日社区讨论高度集中在**升级迁移可靠性、Gateway 事件循环阻塞、会话状态/消息丢失、子进程泄漏**四大方向。维护者提交了大量修复型 PR，项目在积极收敛，但 P0/P1 积压仍较密集，升级路径稳定性是当前最大风险。

---

## 2. 版本发布

### v2026.9.4 — openclaw 2026.9.4

**更新亮点：**
- **兼容失败更新后的恢复能力**：在 schema 和配置检查证明回滚安全时，保留上一版本包，并用先前配置与服务恢复。相关改动 #140339。
- **数据库迁移仍要求验证过的预更新备份**：回滚能力不替代迁移备份，升级前必须保留可验证备份。

**已知严重问题与迁移注意事项：**
- **v2026.9.4 未包含 #144208**，已迁移的全局 handoff lease 存储中若存在 version-1 保留行，`withConfigWriteLock` → `assertSourceUnborrowed` → `readRetainedSources` 会扫描并失败，导致每次配置写入失败。该问题被标记为 P0 / release blocker。  
  链接：https://github.com/openclaw/openclaw/issues/144742
- **2026.9.2 → 2026.9.4 管理更新可能失败**：在 candidate-Doctor 的 runtime-verification 步骤因 #144742 / #144208 拒绝，随后回滚到已迁移的 9.4 状态。  
  链接：https://github.com/openclaw/openclaw/issues/145192
- **npm 全局安装更新失败但回滚恢复**：用户从 2026.9.3 升级到 2026.9.4 时在 `global install swap` 步骤确定性失败，回滚恢复了包树，但报告“recovery is unverified”。该 Issue 已关闭。  
  链接：https://github.com/openclaw/openclaw/issues/144712
- **git/dev 安装的 Codex 插件风险**：Doctor 可能用 npm 刷新 Codex 插件，导致重建的 bundled plugin 被遮蔽，缺失 native-hook-relay export。  
  链接：https://github.com/openclaw/openclaw/issues/145266
- **Windows dev 通道更新**：candidate snapshot 阶段可能因 malformed canary path 失败，报 `runtime-verification-failed`。  
  链接：https://github.com/openclaw/openclaw/issues/144581

**迁移建议：**
1. 升级前必须完成并验证数据库备份。
2. 从 2026.9.2 / 2026.9.3 升级时，预留 candidate-Doctor 失败后的回滚与手工 triage 时间。
3. git/dev 安装用户需关注 Codex 插件是否被 npm 刷新覆盖，必要时使用 host-rebuilt Codex。
4. Windows 用户避免在 dev 通道直接依赖 candidate snapshot 流程。

---

## 3. 项目进展

今日 PR 列表中展示的评论最多条目大多仍为 OPEN，但维护者和贡献者提交了大量修复型 PR，重点推进以下方向：

| 进展方向 | 关键 PR / Issue | 说明 |
|---|---|---|
| 更新与回滚修复 | [#145044](https://github.com/openclaw/openclaw/pull/145044) | 修复 unattended update repair 在 candidate 状态较新时失败的问题 |
| Codex 插件版本偏斜 | [#145356](https://github.com/openclaw/openclaw/pull/145356)、[#145298](https://github.com/openclaw/openclaw/pull/145298) | 让 git 安装保留重建的 bundled plugin，避免 Doctor 从 npm 刷新造成 SDK 符号不匹配 |
| cron reaper 性能 | [#142591](https://github.com/openclaw/openclaw/pull/142591) | 以只读方式列出 run sessions，避免同步 `PRAGMA integrity_check` 阻塞事件循环，对应 #142476 |
| Doctor 凭据重命名 | [#145136](https://github.com/openclaw/openclaw/pull/145136) | 保留被重命名 auth profile 的消费者，避免模型引用和账户选择指向已删除 ID |
| 模型凭据绑定 | [#144768](https://github.com/openclaw/openclaw/pull/144768) | 要求 provider-bound credentials，涉及安全边界和 auth-provider |
| Gateway 升级与 Node prefix | [#145335](https://github.com/openclaw/openclaw/pull/145335) | 修复 nvm 切换 Node 后受管 Gateway 仍使用旧全局安装的问题 |
| Logbook SQLite 异步化 | [#144982](https://github.com/openclaw/openclaw/pull/144982) | 将 SQLite 操作迁移到 owned workers，减少 Gateway 事件循环阻塞 |
| UI 诊断保留 | [#144844](https://github.com/openclaw/openclaw/pull/144844)（已关闭） | 保留自动构建失败的有用诊断信息，避免只显示 `Control UI build failed: }` |

**已关闭的重要 Issue：**
- [#144712](https://github.com/openclaw/openclaw/issues/144

---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>



</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>

# Pi 项目动态日报

**报告日期：2026-09-12** ｜ 数据窗口：过去 24 小时
**项目：** [earendil-works/pi](https://github.com/earendil-works/pi)

---

## 1. 今日速览

- 项目维持**高活跃度**：24 小时内 52 条 Issue 更新（新开/活跃 17、已关闭 35），23 条 PR 更新（待合并 8、已合并/关闭 15），**关闭量约为新增量的 2 倍**，积压正在被有效消化。
- **核心团队动作显著**：mitsuhiko 主导的「对话中途系统消息」分层重构（#9116、#9117）双双关闭合并，是本次窗口内最重要的架构级推进。
- 稳定性修复密集落地：压缩逻辑误触发（#9478）、Bedrock token 计量（#9489）、fd/rg 版本解析限流（#8708）等多个长尾 Bug 被修复。
- **Windows 平台仍是最大痛点来源**：从 shell 路径发现（#9490、#9501）到 CJK 输入法（#9497），社区讨论热度最高的 Issue（#7547，62 条评论）也聚焦 Windows 支持策略。
- 无新版本发布；当前主线版本仍为 **v0.85.1**，下一个版本预计将整合上述多项修复。

---

## 2. 版本发布

本周期**无新版本发布**。

---

## 3. 项目进展

### 已合并 / 关闭的重点 PR

| PR | 标题 | 意义 |
|---|---|---|
| [#9116](https://github.com/earendil-works/pi/pull/9116) | feat(ai): add mid-conversation system messages | **架构级变更**：为 pi-ai 引入对话中途 system role，解决扩展/工具集变更时只能重写顶层 prompt 的问题 |
| [#9117](https://github.com/earendil-works/pi/pull/9117) | feat(coding-agent): deliver prompt and tool changes as system message deltas | 承接 #9116，将 prompt / tool loadout 变更改为系统消息增量下发，减少上下文重复并提升缓存命中 |
| [#9483](https://github.com/earendil-works/pi/pull/9483) | Make tool cwd resolution opt-in via customCwd with ctx.cwd fallback | 在 #8627 引发兼容性反馈后迅速修正，改为显式 `customCwd` 选择加入，兼顾扩展生态兼容 |
| [#9468](https://github.com/earendil-works/pi/pull/9468) | feat(coding-agent): deferred extension reload | 扩展重载改为「回合稳定后合并执行」，避免中途重载导致的运行态不一致 |
| [#9478](https://github.com/earendil-works/pi/pull/9478) | fix(coding-agent): cap per-message chars in compaction token estimate | 修复 6.6MB 工具结果导致压缩误触发（关联 #9476） |
| [#9489](https://github.com/earendil-works/pi/pull/9489) | fix(bedrock-converse): normalize gross usage.input to net per model family | 统一 Bedrock 各模型族的 input token 口径（Fixes #8752） |
| [#8708](https://github.com/earendil-works/pi/pull/8708) | fix(coding-agent): resolve fd/rg release versions without the GitHub API | 规避匿名 API 配额（60 次/小时）对共享出口 IP 的限流（Fixes #8594） |
| [#8616](https://github.com/earendil-works/pi/pull/8616) | fix(coding-agent): scan past non-EXIF APP1 segments | 修复 XMP 在 EXIF 之前的 JPEG 无法转换（Fixes #8571） |
| [#9467](https://github.com/earendil-works/pi/pull/9467) | fix(ai): classify setup-phase aborts as "aborted" in lazyStream | 消除误报的硬错误提示 |

### 整体推进评估

本周期合并集中在三个方向：**(1) 上下文与缓存架构**（#9116/#9117）、**(2) 扩展生态健壮性**（#9468/#9483）、**(3) 长尾稳定性修复**。其中 #9116/#9117 是 #8998 拆分计划的第二层，意味着一次较大的 prompt 管理重构已基本落地主干，后续可能影响扩展作者对 `system` 消息的假设，值得关注。

---

## 4. 社区热点

| Issue | 评论 | 👍 | 焦点 |
|---|---|---|---|
| [#7547](https://github.com/earendil-works/pi/issues/7547) `[Windows]` 如何在 Windows 上使用 Pi？ | **62** | 2 | 社区自发汇总 Windows 运行方式与问题，核心诉求是**收敛支持矩阵**（哪些进核心、哪些外包给扩展） |
| [#9323](https://github.com/earendil-works/pi/issues/9323) 改进 fireworks 专用配置 | 14 | 0 | 某内部函数的配置缺乏文档与通用性 |
| [#5323](https://github.com/earendil-works/pi/issues/5323) 改进 Vertex + GCP metadata server 支持 | 9 | 2 | `is Vertex authed?` 使用同步 `existsSync`，在 GCP metadata server 场景下失效 |
| [#7321](https://github.com/earendil-works/pi/issues/7321) Termux 多行粘贴损坏 | 5 | 1 | 非 bracketed-paste 终端兼容性 |
| [#6108](https://github.com/earendil-works/pi/issues/6108) `/reload` 重复执行扩展依赖副作用 | 5 | 0 | 扩展热重载语义 |
| [#8810](https://github.com/earendil-works/pi/issues/8810) 扩展注册的 provider 默认值被忽略 | 5 | 1 | 与 #9116/#9117 的 prompt 重构方向相关 |

**背后诉求分析：**
- **平台支持策略需要定调**：#7547 62 条评论表明 Windows 用户基数大但路径分散，维护者需要明确「核心支持 vs 扩展承载」的边界（且该讨论已直接催生 PR #9501）。
- **扩展作者需要更稳定的 API 契约**：#8810、#6108、#7658、#6930 四条均围绕扩展能力边界，说明扩展生态正在增长但底层接口尚未定型。
- **云厂商适配质量参差**：#5323（Vertex）、#9331（Bedrock）、#9494（Antigravity 429）显示各 provider 适配仍有盲区。

---

## 5. Bug 与稳定性

### 🔴 严重

| Issue | 描述 | Fix 状态 |
|---|---|---|
| [#9410](https://github.com/earendil-works/pi/issues/9410) | 大上下文会话中按 Escape 中断流式输出，TUI 冻结约 60 秒（v0.85.1，~465k token） | ❌ 无 PR |
| [#9265](https://github.com/earendil-works/pi/issues/9265) | openai-completions 流式 handler 每次 delta 重新解析全部 tool-call JSON，复杂度 O(n²)，单线程守护进程下阻塞事件循环 | ❌ 无 PR |
| [#9500](https://github.com/earendil-works/pi/issues/9500) | pi 0.85.1 SIGILL (ILL_ILLOPN) 崩溃，疑似 bundled addon `fs-native-extensions` | 已关闭（自关闭，证据已补全，建议复审） |

### 🟠 高

| Issue | 描述 | Fix 状态 |
|---|---|---|
| [#9331](https://github.com/earendil-works/pi/issues/9331) | Bedrock 下 OpenAI reasoning effort 从未真正下发，thinking level 无效 | ❌ 无 PR |
| [#8810](https://github.com/earendil-works/pi/issues/8810) | 扩展注册的 provider 间歇性忽略 `defaultProvider`/`defaultModel` | ❌ 无 PR，与 #9116/#9117 方向相关 |
| [#6108](https://github.com/earendil-works/pi/issues/6108) | release 二进制在 `/reload` 时重跑扩展依赖模块副作用 | ❌ 无 PR（#9468 改进了重载时序，但未直接覆盖此因） |
| [#9323](https://github.com/earendil-works/pi/issues/9323) | fireworks 专用配置缺乏泛化 | ❌ 无 PR |

### 🟡 中

| Issue | 描述 | Fix 状态 |
|---|---|---|
| [#8371](https://github.com/earendil-works/pi/issues/8371) | compaction 输入无上界，超上下文会话无法被压缩 | 已关闭（no-action） |
| [#8318](https://github.com/earendil-works/pi/issues/8318) | 同回合 read+edit 同文件时 read 报「1 行 EOF」（`fs.writeFile` 竞态） | 已关闭（no-action） |
| [#7321](https://github.com/earendil-works/pi/issues/7321) | Termux 等终端多行粘贴被首个 `\r` 提前提交 | ❌ 无 PR |
| [#9045](https://github.com/earendil-works/pi/issues/9045) | 非法 `--mode` 值被静默忽略，无 diagnostic | ❌ 无 PR |
| [#9497](https://github.com/earendil-works/pi/issues/9497) | Windows CJK 输入法严重卡顿、候选窗不显示 | 已关闭（临时方案：`showHardwareCursor`） |
| [#9480](https://github.com/earendil-works/pi/issues/9480) | MCP 重连后不刷新 `tools/list`，OAuth 解锁的工具不可见 | 已关闭 |
| [#9502](https://github.com/earendil-works/pi/issues/9502) | `build:offline` 因 Google `TOO_MANY_TOOL_CALLS` finish reason 类型未覆盖而失败 | 已关闭 |
| [#9499](https://github.com/earendil-works/pi/issues/9499) | `pi update --extensions` 在 npm 12 下因 EALLOWREMOTE 失败 | 已关闭 |

### 🟢 低 / 已闭环

- [#9490](https://github.com/earendil-works/pi/issues/9490) `findPowerShell` 硬编码 `C:\` — **已有对应 PR [#9501](https://github.com/earendil-works/pi/pull/9501)（OPEN）**
- [#9205](https://github.com/earendil-works/pi/issues/9205) 示例脚本传入不存在的 `--no-extension` 标志（应为 `--no-extensions`）
- [#9473](https://github.com/earendil-works/pi/issues/9473) TUI 标题内 inline code 丢失 heading 粗体/下划线
- [#9494](https://github.com/earendil-works/pi/issues/9494) Antigravity 429 但配额充足
- [#9498](https://github.com/earendil-works/pi/issues/9498) 误提交（rogue agent），已关闭

> **稳定性小结：** 未发现明确的安全漏洞。性能类 Bug（#9410、#9265）均无对应 PR，属于当前最大风险敞口，建议优先排期。

---

## 6. 功能请求与路线图信号

| 需求 | 状态 | 纳入下一版本的可能性 |
|---|---|---|
| [#7658](https://github.com/earendil-works/pi/issues/7658) 扩展持久化 API-key 凭据（`auth.json`）的编程接口 | OPEN，4 评论 | **中** — 扩展生态刚需，但涉及凭据安全需谨慎设计 |
| [#6930](https://github.com/earendil-works/pi/issues/6930) 将 `renderPage` / `oauthSuccessHtml` / `oauthErrorHtml` 公开 | OPEN，4 评论 | **中高** — 纯 HTML 渲染函数，无逻辑风险，实现成本极低 |
| [#9496](https://github.com/earendil-works/pi/issues/9496) 增加内联图片开关快捷键（类比 Ctrl+T / Ctrl+O） | CLOSED | **高** — 已有明确 action id 模式，属体验补全 |
| [#9469](https://github.com/earendil-works/pi/issues/9469) 非阻塞事件导出扩展（webhook / MQ） | CLOSED | 低 — 更适合作为社区扩展而非核心 |
| [#9475](https://github.com/earendil-works/pi/issues/9475) 启动与会话恢复性能优化（5 个独立分支） | CLOSED | **中高** — 提交者已备好分支，等待批准即可拆分为 PR |
| [#9403](https://github.com/earendil-works/pi/issues/9403) 后台子进程保留 `-e` 选择与 `--no-extensions` 策略 | CLOSED | 中 —

</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报

**报告日期：2026-09-12** ｜ 数据源：github.com/BerriAI/litellm

---

## 一、今日速览

- **开发吞吐量维持高位**：24 小时内 PR 更新 309 条（待合并 195 / 已合并或关闭 114），Issues 更新 59 条（新开或活跃 46 / 已关闭 13），PR:Issue 更新比约 **5.2:1**，工程侧动能远强于问题侧。
- **审查积压压力上升**：待合并 PR（195）是已合并/关闭数（114）的 **1.7 倍**，且抽样展示的 20 条 PR 中 18 条仍处 OPEN 状态，维护者审查队列存在明显堆积。
- **安全与凭据治理成为今日主线**：从长期未结的供应链投毒事件（#24518）、默认主密钥 `sk-1234` 治理（#40758 / #40789）、秘密脱敏覆盖缺口（#40190）到代理级 ReDoS 崩溃（#32353），形成一条覆盖"默认配置—秘密处理—运行时防护"的加固链条。
- **无功能性版本发布**：唯一新版本 `v1.102.0-dev.2` 仅为 Docker 镜像签名验证说明，不涉及功能变更或破坏性更新。
- **积压清理明显**：今日关闭的 13 条 Issue 中至少 8 条为已修复缺陷（MCP OAuth、OTel 规范化、多说话人转录、PG 绑定变量超限等），表明旧账正在被系统性收敛。

---

## 二、版本发布

### v1.102.0-dev.2（开发版）

- 链接：https://github.com/BerriAI/litellm/releases
- **性质**：`-dev` 后缀标记的开发构建，**不建议用于生产环境**。
- **内容**：发布说明仅涵盖 Docker 镜像签名验证流程——所有 LiteLLM 镜像均使用 [cosign](https://docs.sigstore.dev/cosign/overview/) 签名，密钥沿用 commit `0112e53` 中引入的同一把密钥。
- **破坏性变更**：无。
- **迁移注意事项**：若使用 `ghcr.io/berriai/litellm` 镜像，建议在 CI/CD

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*