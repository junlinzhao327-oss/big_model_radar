# OpenClaw 生态日报 2026-08-22

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-08-21 22:35 UTC

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



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-22

## 1. 今日速览

过去 24 小时项目活跃度极高：累计 393 条 Issue 更新（其中 335 条新开/活跃、58 条关闭）、500 条 PR 更新（450 条待合并、50 条已合并/关闭），并发布了 v0.20.5 补丁版本（汇总自 v0.20.4 以来的 ~323 个 PR）。今日信号集中在**桌面端与 Windows 平台稳定性**（ZIP 更新删除应用、svchost 蓝屏、gateway 冷启动死亡等一批 P1 问题被集中报告）、**state.db 数据完整性隐患**（无界增长与损坏问题反复出现），以及**大型架构重构**的里程碑落地（god-file 分解 20/20 完成）。项目健康度总体良好，吞吐量可观，但 Windows/桌面端稳定性与数据安全仍是当前最突出的短板。

---

## 2. 版本发布

### Hermes Agent v0.20.5 (`v2026.8.19`)
- **发布日期**：2026-08-19
- **类型**：Patch Release
- **内容**：将自 v0.20.4 以来合并的约 **323 个 PR** 汇总为一个稳定标签，面向下游消费者（Docker 镜像、托管部署、全新安装）。
- **破坏性变更**：补丁版本，无已知破坏性变更；未随数据提供详细迁移说明。
- **迁移注意**：建议下游消费方在升级前关注 v0.20.4 → v0.20.5 之间的 323 个 PR 中涉及 Windows 安装、desktop 更新链路、state.db 处理的相关修改（详见下文 Bug 与稳定性部分）。

发布链接：https://github.com/NousResearch/hermes-agent/releases/tag/v2026.8.19

---

## 3. 项目进展

### 今日完成的重要关闭项

| 项目 | 类别 | 说明 |
|---|---|---|
| [#78647](https://github.com/NousResearch/hermes-agent/issues/78647) 大型 god-file 分解 20/20 完成 | 架构重构 | **Repo-wide god-file sharding epic 完成**。20 个大型文件全部分解为干净模块，落地了 "Extend, don't duplicate" 的共享接口策略。这是项目架构层面的重要里程碑。 |
| [#73082](https://github.com/NousResearch/hermes-agent/issues/73082) 桌面端 Renderer/GPU 空闲 100% CPU | 性能修复 | 空闲状态下 Electron Renderer 与 GPU 进程 50-90% CPU 占用的问题已关闭，应为已修复。 |
| [#53902](https://github.com/NousResearch/hermes-agent/issues/53902) v0.17.0 渲染器 fontations + temporal_rs 循环 | 性能修复 | GPU 98% 占用/13W 功耗的渲染循环问题关闭。 |
| [#38873](https://github.com/NousResearch/hermes-agent/issues/38873) 桌面端远程 gateway 模式回退本地 | 功能修复 | 远程后端就绪后应用不再闪回本地。 |
| [#84185](https://github.com/NousResearch/hermes-agent/issues/84185) Windows 更新后 gateway 静默死亡 | 稳定性修复 | 无日志、无 PID、无退出记录的静默崩溃问题已修复并关闭。 |
| [#23524](https://github.com/NousResearch/hermes-agent/issues/23524) per-cron reasoning effort 覆盖 | 功能落地 | Cron 任务现已支持独立的 reasoning/thinking level 覆盖，不再仅继承全局配置。 |
| [#38053](https://github.com/NousResearch/hermes-agent/issues/38053) macOS launchd 更新后不重启所有 profile gateways | 功能修复 | 多 profile 场景下的更新重启逻辑已补齐。 |
| [#9763](https://github.com/NousResearch/hermes-agent/issues/9763) cron 硬编码 `skip_memory=True` | 功能修复 | 移除了将外部 memory providers（如 mem0）排除在 cron 任务之外的硬编码限制。 |
| [#27649](https://github.com/NousResearch/hermes-agent/issues/27649) 多进程日志写入已轮转文件 | 可观测性修复 | 日志轮转后旧进程继续写入 `.log.1` 的问题已修复。 |

### 今日提交的高质量修复 PR（待合并）

- [#91079](https://github.com/NousResearch/hermes-agent/pull/91079) — Windows 桌面包重建改为**事务性 + 自愈**，针对 #44225/#86443/#90134/#90829 四个关联缺陷，覆盖 zip 回退删除、ESM 路径错误、`get-windows` 损坏等多个问题。
- [#91852](https://github.com/NousResearch/hermes-agent/pull/91852) — macOS 上所有 `state.db` 修复连接启用 fsync 写屏障，并在 schema 手术期间拒绝并发连接，直接治理 #90747 的存量撕裂问题。
- [#89536](https://github.com/NousResearch/hermes-agent/pull/89536) — 为 `gateway.error.log` 接入轮转 writer，解决单文件无限增长至 141MB 的问题。
- [#88674](https://github.com/NousResearch/hermes-agent/pull/88674) — 更新流程中 `git fetch`/`checkout` 失败不再被 `set +e` 吞掉，仓库 stage 会正确失败。

**今日合并/关闭合计**：58 个 Issue + 50 个 PR。项目整体在性能、Windows 稳定性、日志轮转、cron 灵活性等方向都获得了实质推进。

---

## 4. 社区热点

### 讨论最活跃的 Issue/PR

| 排名 | 编号 | 标题 | 评论数 | 分析 |
|---|---|---|---|---|
| 1 | [#78647](https://github.com/NousResearch/hermes-agent/issues/78647) | [COMPLETE] Large-file decomposition: 20/20 done | 77 | 大型重构收官引发广泛关注。社区对 god-file 分解的方向与"永不回退"策略讨论热烈，是架构治理的重要参考案例。 |
| 2 | [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) | [skills-index-watchdog] Skills index is stale or degraded | 71 | 自动化探针持续报告 skills 索引过期（29.8h 超 26h 上限）。讨论量大说明技能生态的指数新鲜度直接影响大量用户。 |
| 3 | [#87093](https://github.com/NousResearch/hermes-agent/issues/87093) | Debian 13.6 安装失败（uv.lock & npm install） | 19 | 新装用户无法完成安装，P1 级别，获得 3 个 👍，社区对此反馈强烈。 |
| 4 | [#73082](https://github.com/NousResearch/hermes-agent/issues/73082) | 桌面端空闲 100% CPU / 高能耗 | 17 | 已关闭（修复）。macOS 用户对电池/发热问题高度敏感。 |
| 5 | [#89675](https://github.com/NousResearch/hermes-agent/issues/89675) | 桌面端更新后所有 profile 会话无法加载 | 16 | 更新回归问题，backend 未携带 `--profile` 导致会话列表为空，2 个 👍。 |

### 背后诉求分析

- **高频词：Windows 安装/更新链路、桌面端稳定性、state.db 数据安全**。排名靠前的议题集中于"更新后坏掉"的场景，说明用户对升级路径的可靠性预期正在提高。
- 自动化探针（sweeper）已渗透到 skills 索引、session state、message delivery 等领域，社区对"机器人盯守"习以为常，但对长期未闭环的探针（如 #66616 开放超一个月）开始表达关注。

---

## 5. Bug 与稳定性

### P1 级（严重）

| Issue | 描述 | 状态 |
|---|---|---|
| [#87093](https://github.com/NousResearch/hermes-agent/issues/87093) | **Debian 13.6 安装失败**：`curl \| bash` 安装脚本在 `uv.lock` / `npm install` 阶段报错，全新系统也无法安装。 | OPEN，暂无 fix PR |
| [#83846](https://github.com/NousResearch/hermes-agent/issues/83846) | **Windows ZIP 回退更新删除已构建桌面应用且不重建**，后续更新报 "Already up to date"。 | OPEN，**fix PR #91079 已提交** |
| [#89614](https://github.com/NousResearch/hermes-agent/issues/89614) | **Windows 下 Hermes 通过 stale-PID `taskkill /F /PID` 误杀 `svchost.exe`**，导致连续 0xEF (CRITICAL_PROCESS_DIED)

</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报

**日期：2026-08-22**
**数据周期：2026-08-21 至 2026-08-22（24小时）**


## 1. 今日速览

过去24小时内，OpenHands SDK 保持**极高活跃度**：共产生 29 条 Issue 更新和 21 条 PR 更新，并连续发布 **v1.43.0 与 v1.43.1** 两个版本。值得关注的是，社区与维护者围绕**并发性能与锁竞争问题**形成了一波集中的报告-修复闭环——#4569（全局生命周期锁）、#4537（任务委托持锁导致 UI 冻结）、#4477（并发负载测试缺口）等 Issue 均已获得对应 PR 或明确修复计划（#4570、#4513），显示出项目对性能回归的高度重视。同时，记忆偏好传播（#4542）、GitLab 克隆 token 注入（#4543）等社区反馈的高优先级 Bug 均在当天获得了修复 PR，整体呈现**响应快、闭环紧**的健康态势。

- Issue 更新：29 条（新开/活跃 17，已关闭 12）
- PR 更新：21 条（待合并 12，已合并/关闭 9）
- 新版本发布：2 个（v1.43.1、v1.43.0）
- 代码健康度：多个高优先级 Bug 在 24 小时内获得修复 PR，并发相关修复集中推进


## 2. 版本发布

### v1.43.1（最新，2026-08-21 发布）

🔗 [Release v1.43.1](https://github.com/OpenHands/software-agent-sdk/releases/tag/v1.43.1) | 发布 PR: [#4572](https://github.com/OpenHands/software-agent-sdk/pull/4572)

**主要变更：**

- **chore(deps):** 将 gitpython 从 3.1.50 升级至 3.1.58（含安全修复），由 Dependabot 提交 [#4545](https://github.com/OpenHands/software-agent-sdk/pull/4545)
- **feat(prompt):** 默认提示词中告知 Agent 本地会话历史（event-history）的存储位置，使 Agent 能够找到之前的本地 OpenHands 对话，由 @neubig 提交 [#4527](https://github.com/OpenHands/software-agent-sdk/pull/4527)
- **fix(sdk):** 修复 workspace 相关的一个问题（Release 说明被截断）

**破坏性变更：** 无

**迁移注意事项：** 提示词变更会改变默认 system prompt 的内容，对依赖特定提示词格式的自动化测试或下游工具可能需要适配。gitpython 升级为 minor 版本跳跃，API 兼容。


### v1.43.0（2026-08-20 发布）

🔗 [Release v1.43.0](https://github.com/OpenHands/software-agent-sdk/releases/tag/v1.43.0) | 发布 PR: [#4553](https://github.com/OpenHands/software-agent-sdk/pull/4553)

**主要变更：**

- **feat(plugin):** 新增 Agent Plugins 清单加载器，支持根目录 `plugin.json` 及闭合 schema，由 @VascoSch92 提交 [#4474](https://github.com/OpenHands/software-agent-sdk/pull/4474)
- **fix(security-scan):** 改进发布版安全扫描评论的生成方式，由 @all-hands-bot 提交

**破坏性变更：** Plugins 清单加载器为新增能力，不影响现有 API。安全扫描评论变更仅影响 CI 输出格式。


## 3. 项目进展

过去 24 小时合并/关闭的 PR 反映了项目在**稳定性修复**和**开发者体验**两个方向的持续投入：

### 已合并/关闭 PR（9 条，部分列出）

| PR | 内容 | 状态归属 |
|---|---|---|
| [#4572](https://github.com/OpenHands/software-agent-sdk/pull/4572) | Release v1.43.1 发布 PR | 已完成发布 |
| [#4527](https://github.com/OpenHands/software-agent-sdk/pull/4527) | feat(prompt): 提示词中告知 Agent 本地会话历史位置 | 已合并到 v1.43.1 |
| [#4497](https://github.com/OpenHands/software-agent-sdk/pull/4497) | fix(sdk): workspace 默认 LLM 从活动配置文件中解析，修复 #4494 | 已关闭（Fixes #4494） |
| [#4479](https://github.com/OpenHands/software-agent-sdk/pull/4479) | feat(tools): 为 FinishTool 新增结构化任务结果预设 | 已合并 |
| [#4567](https://github.com/OpenHands/software-agent-sdk/pull/4567) | fix(sdk): 标准化 Kimi K3 视觉能力元数据 | 已合并 |
| [#4471](https://github.com/OpenHands/software-agent-sdk/pull/4471) | fix(agent): 修复 git/reset 别名导致的可执行文件重复前缀问题 | 已合并（Fixes #4468） |
| [#4545](https://github.com/OpenHands/software-agent-sdk/pull/4545) | chore(deps): gitpython 3.1.50 → 3.1.58 | 已合并到 v1.43.1 |

### 关键进展解读

1. **记忆功能落地**：`#4527` 的合并配合 `#4528` 的关闭，标志着"告知 Agent 本地会话历史"这一功能正式发布，增强了 SDK 的长期记忆能力。关联的 `#4542`（load_memory 偏好传播）已有对应修复 PR `#4566`，预计进入下一版本。

2. **Workspace 安全修复**：`#4497` 修复了"工作区默认 LLM 忽略活动配置文件"的高优先级问题，消除了静默的模型/凭据漂移风险。

3. **工具链完善**：`#4479` 为自动化任务引入了结构化的 `FinishTool` 结果预设，使 Agent 可以显式区分任务"成功"与"不可行"——这也是对用户长期反馈（见 #4106）的落地响应。

4. **并发修复主线**：`#4513`（deadlock 测试）、`#4570`（移除全局锁）共同构成了对并发边界问题的系统性修复。

**整体判断**：项目正从"功能扩张期"转向"稳定性加固期"，短期内修复了大量社区反馈的边界 Bug，且维护者（@neubig 等）直接下场提交修复，推进速度很快。


## 4. 社区热点

今日讨论热度最高的议题集中在**并发性能问题和记忆功能缺陷**上，均获得了维护者快速响应。

### 🔥 热点 1：TaskToolSet 委托持锁导致 UI 冻结

- **Issue:** [#4537 [Bug]: TaskToolSet delegation holds the parent ConversationState lock...](https://github.com/OpenHands/software-agent-sdk/issues/4537) — 2 条评论，1 👍
- **标签:** `bug`, `priority:high`, `delegation`, `performance`
- **核心诉求：** 当 Agent 调用 TaskToolSet 执行子代理任务时，Agent Canvas 的会话列表在任务执行期间完全停止渲染。用户反馈社区报告了类似的跨仓库问题（OpenHands/OpenHands#16720）。
- **关联修复：** 该问题背后的全局 `_lifecycle_lock` 问题已由 `#4569` 正式提出并由 `#4570` PR 修复中。

### 🔥 热点 2：全局 load_memory 偏好被忽略

- **Issue:** [#4542 [Bug]: Global agent_context.load_memory preference is ignored...](https://github.com/OpenHands/software-agent-sdk/issues/4542) — 5 条评论
- **标签:** `bug`, `priority:high`, `memory`, `release-note-required`
- **核心诉求：** `agent_settings.agent_context.load_memory` 是全局用户偏好，但只有在通过 `agent_profile_id` 启动会话时才生效。通过具体 `agent` 或 `agent_settings` 启动时静默丢失该设置，导致持久记忆无法加载。
- **关联修复：** PR [#4566](https://github.com/OpenHands/software-agent-sdk/pull/4566)（fix(agent-server): propagate load_memory preference to all launch paths）当天即提交。

### 🔥 热点 3：全局生命周期锁造成跨会话性能瓶颈

- **Issue:** [#4569 [Bug]: replace global _lifecycle_lock with per-conversation locks...](https://github.com/OpenHands/software-agent-sdk/issues/4569) — 2 条评论
- **标签:** `bug`, `priority:high`, `performance`
- **核心诉求：** 所有会话生命周期操作共享一把全局 `asyncio.Lock`，其中涉及磁盘 I/O 的慢操作会阻塞无关会话，可能造成跨会话"楔住"（wedge）。
- **关联修复：** PR [#4570](https://github.com/OpenHands/software-agent-sdk/pull/4570) 当天即提交，将全局锁替换为每会话锁。

### 💬 值得关注的合作提案

- **AIML API 50/50 收入分成合作**：[Issue #4574](https://github.com/OpenHands/software-agent-sdk/issues/4574) + [PR #4576](https://github.com/OpenHands/software-agent-sdk/pull/4576) 由 @hugoaimlapi 提交，希望作为 LiteLLM 验证提供商集成到 OpenHands 中。这反映了外部商业机构对 OpenHands 生态的重视。


## 5. Bug 与稳定性

### 🔴 高优先级

| Issue | 描述 | 状态 |
|---|---|---|
| [#4537](https://github.com/OpenHands/software-agent-sdk/issues/4537) | TaskToolSet 委托持锁导致 UI 冻结、线程池饱和 | OPEN，已有关联修复方向（#4570） |
| [#4569](https://github.com/OpenHands/software-agent-sdk/issues/4569) | 全局生命周期锁造成跨会话性能瓶颈 | OPEN，修复 PR #4570 已提交 |
| [#4542](https://github.com/OpenHands/software-agent-sdk/issues/4542) | load_memory 全局偏好被忽略 | OPEN，修复 PR #4566 已提交 |
| [#4494](https://github.com/OpenHands/software-agent-sdk/issues/4494) | workspace 默认 LLM 忽略活动配置文件，可能启动无密钥的过期模型 | **已关闭**（由 #4497 修复，已在 v1.43.1 中验证） |

### 🟡 中优先级

| Issue | 描述 | 状态 |
|---|---|---|
| [#4544](https://github.com/OpenHands/software-agent-sdk/issues/4544) | 触发式技能和路径规则在会话压缩（condensation）后静默失效 | OPEN，`ready-for-dev` |
| [#4543](https://github.com/OpenHands/software-agent-sdk/issues/4543) | 无法使用 token 从自托管 GitLab 克隆仓库 | OPEN，修复 PR #4571 已提交 |
| [#4541](https://github.com/OpenHands/software-agent-sdk/issues/4541) | Qwen3-32B 模型 `<think>` 行为异常（标题中出现、截断等） | OPEN |
| [#4540](https://github.com/OpenHands/software-agent-sdk/issues/4540) | Synthetic Provider 下工具调用返回错误的原始语法 | OPEN |
| [#4575](https://github.com/OpenHands/software-agent-sdk/issues/4575) | Agent 终端命令继承服务器进程优先级 | OPEN，修复 PR #4573 已提交 |
| [#4468](https://github.com/OpenHands/software-agent-sdk/issues/4468) | `normalize_tool_call` 重复添加 git 命令前缀 | **已关闭**（由 #4471 修复） |
| [#4500](https://github.com/OpenHands/software-agent-sdk/issues/4500) | 增量视图缓存在压缩后跳过 enforce_properties，导致孤儿 action/obs 对 | **已关闭** |
| [#3645](https://github.com/OpenHands/software-agent-sdk/issues/3645) | DeepSeek 自定义 base_url 被剥离 provider 前缀 | **已关闭**（验证完成） |
| [#4107](https://github.com/OpenHands/software-agent-sdk/issues/4107) | TaskToolSet 未将父级中断传播给活动子代理 | **已关闭** |

### 🟢 低优先级

| Issue | 描述 | 状态 |
|---|---|---|
| [#4156](https://github.com/OpenHands/software-agent-sdk/issues/4156) | Windows 下 uvx 启动 agent-server 报 ModuleNotFoundError | **已关闭** |
| [#2510](https://github.com/OpenHands/software-agent-sdk/issues/2510) | 调研 Dependabot 对 uv workspaces 的支持 | **已关闭**（由 #4144 文档化） |

**分析：** 今日 Bug 报告中约 50% 已获得当日修复 PR，修复效率很高。核心问题集中在**并发模型有缺陷**（全局锁、线程池饱和）和**配置传播不一致**（load_memory、LLM profile）两大类，这属于架构级问题而非边缘 Bug，建议通过 #4477（并发负载测试）建立长期防线。


##

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>

# LiteLLM 项目动态日报 — 2026-08-22

## 1. 今日速览

项目今日保持**极高活跃度**：24小时内更新 Issues 68 条（新开/活跃 54 条，关闭 14 条），PR 更新 304 条（待合并 192 条，合并/关闭 112 条），发布开发版本 v1.99.0-dev.2。当前开发焦点集中在 **MCP 路由与认证修复、模型定价精确性（Azure/DeepSeek/Kimi）、推理能力参数（reasoning_effort）按模型组细分、以及观测性（OTEL spans/日志/回调）增强** 四大方向。同时存在一批长期未关闭的老 Issue（如 #20064、#15519、#17696）持续获得关注，但缺少维护者明确回应。

---

## 2. 版本发布

### v1.99.0-dev.2（开发版）
- **发布时间**：2026-08-21 前后
- **版本性质**：预发布开发版（dev channel）
- **主要内容**：该版本发布说明中仅包含 Docker 镜像 cosign 签名验证的说明，强调所有 LiteLLM Docker 镜像均使用 [commit `0112e53`](https://github.com/BerriAI/litellm/commit/0112e53046018d726492c814b3644b7d376029d0) 引入的同一密钥签名，提醒用户在生产环境验证镜像完整性。
- **破坏性变更**：未在发布说明中声明破坏性变更或迁移注意事项。
- **注意事项**：作为 dev 版本，API 与功能可能不稳定，建议生产环境用户继续使用 main-stable 标签。

---

## 3. 项目进展

今日合并/关闭 112 个 PR 中，以下重要合并体现了项目持续推进的关键方向：

**核心功能合并：**

- **[feat(parallel_ai): add chat + responses LLM provider and full search param support (#36704)](https://github.com/BerriAI/litellm/pull/36704)（已关闭/合并）** — 将 Parallel AI 从仅搜索扩展到 chat + responses 完整 LLM 供应商支持，补齐 search 参数嵌套、按请求定价等能力。这是对多模态/搜索类模型接入的积极补充。
- **[feat(router): per-group supported reasoning efforts via model-map intersection (#37732)](https://github.com/BerriAI/litellm/pull/37732)（已关闭/合并）** — 按模型组自动推导支持的 reasoning_effort 级别，并在各部署之间取交集，解决 GPT/Claude/Kimi 对 reasoning 参数接受度不一致的问题。这是 `v1.99.0` 系列中值得关注的可观测性/能力发现增强。

**修复类合并：**

- **[fix(redis): reset only the failed node on a cluster client timeout, not the whole client (#37863)](https://github.com/BerriAI/litellm/pull/37863)** — 修复 Redis Cluster 单节点超时导致整个客户端连接重置、所有并发请求被阻塞的问题。对高可用部署是重要的稳定性修复。
- **[test(lint): fix PT011/PT012 introduced by #37736, blocking lint on every PR (#37870)](https://github.com/BerriAI/litellm/pull/37870)** — 修复因 #37736 引入的 lint 错误导致的 CI 全树阻塞问题，恢复了所有 PR 的 lint 检查通过能力——这也是今日 PR 合并量恢复正常的先决条件。

**被维护者接手重新提交的外部 PR（重要信号）：**

- **[fix(anthropic_messages): gate sampling params on /v1/messages like /chat/completions (#37868)](https://github.com/BerriAI/litellm/pull/37868)** — 将 #35057（@mihidumh 的 fork 提交）复制到 `litellm_` 分支，以便完整运行 CircleCI。修复 Anthropic Messages 端点对 sampling 参数的限制行为，使其与 /chat/completions 对齐。
- **[fix(pricing): add undated azure aliases for gpt-audio-mini and gpt-realtime-mini (#37867)](https://github.com/BerriAI/litellm/pull/37867)** — 同样复制自外部贡献者 #33291，为 gpt-audio-mini 和 gpt-realtime-mini 补充未标注日期的 Azure 别名。

这四位 PR（#37868、#37867、#37875、#37887 等）被维护者以“保留原作者 commit”方式重新推送，说明项目在**积极吸收外部贡献**，同时通过完整 CI 保证质量。

---

## 4. 社区热点

**今日讨论热度和用户关注度最高的议题：**

- **[#23869 [Bug] adding Custom MCP server 报错（已关闭，17 评论，9 👍）](https://github.com/BerriAI/litellm/issues/23869)** — 用户报告在 UI 中添加自定义 MCP Server 时出现 `Error creating mcp server: Could not find...` 错误。该 Issue 已因 stale 被自动关闭，但 17 条评论和 9 个赞说明 MCP Server 配置是高频痛点，值得维护者关注是否有遗留问题。

- **[#20064 [Feature] support model discovery with custom provider（10 评论，10 👍）](https://github.com/BerriAI/litellm/issues/20064)** — 使用 `model_name: my-custom-service/*` 通配符实现自定义供应商模型自动发现的 Feature Request。10 个 👍 表明这是许多自建模型服务用户的共同诉求。当前长期未获得官方回复，但社区讨论活跃（有 10 条讨论）。

- **[#23005 [Bug] UI very slow in version 1.82.x（10 评论）](https://github.com/BerriAI/litellm/issues/23005)** — 多个用户报告 1.82.x 版本 UI 加载极慢，接口响应迟滞。评论中可能包含复现步骤与性能分析，是版本回归问题的典型代表。

- **[#36192 [Bug] Azure GPT-5.6 Terra/Luna 价格错误（8 评论）](https://github.com/BerriAI/litellm/issues/36192)** — 用户发现 Azure GPT-5.6 Terra/Luna 在 LiteLLM 价格表中沿用 OpenAI 的降价后价格，但 Azure 并未同步降价，导致成本核算错误。这是与费用直接相关的敏感问题，评论区用户关注度高。

---

## 5. Bug 与稳定性

按严重程度从高到低排列：

**🔴 严重（未修复）**

- **[#37611 后台健康检查全量加载数据库表、内存不足与 DB 风暴（3 评论）](https://github.com/BerriAI/litellm/issues/37611)** — 在 `use_shared_health_check: true` + 多 worker 场景下，每个 worker 每轮（默认 15 分钟）都会将整个 `LiteLLM_HealthCheckTable` 无界加载进内存，且 DB 持久化未做 leader 限制。这会造成周期性的内存峰值和数据库压力，规模部署下可能 OOM。**暂无修复 PR**。
- **[#30416 MCP 路由处理中 `_mcp_active_toolset_id` 异步流中断导致上下文状态泄漏（4 评论）](https://github.com/BerriAI/litellm/issues/30416)** — 通过静态源码分析识别出动态 MCP 路由处理中，流中断后可能将 user/session 的 active toolset 状态误串到其他请求，属于并发安全问题。**暂无修复 PR**。

**🟠 中高（有修复或已合并修复）**

- **[#36767 Bedrock Converse 流式输出在 finish_reason 后多输出一个空 chunk（回归，2 评论）](https://github.com/BerriAI/litellm/issues/36767)** — v1.94.0 引入的回归（PR #32255 所致）。这会影响客户端解析稳定性。**暂无明确 fix PR，但与 #36168/#28735 相关**，需进一步确认。
- **[#36358 MCP oauth_delegate + dcr_bridge 模式凭据在上游调用时被丢弃（2 评论，4 👍）](https://github.com/BerriAI/litellm/issues/36358)** — 外部 OAuth 客户端（如 Claude.ai 自定义连接器）在 gateway-DCR 桥接下，上游 MCP 服务器始终收不到 Authorization 头。**暂无修复 PR**。
- **[#37222 OAuth2 client_credentials MCP 服务器运行时收不到 client_id/client_secret（2 评论）](https://github.com/BerriAI/litellm/issues/37222)** — tools/list 100% 失败，token endpoint 返回 400。**暂无修复 PR**。与 #36358 同属 MCP 认证链路问题。

**🟡 中低（有对应修复 PR）**

- **[#37895 [PR] group Codex turns under one session id](https://github.com/BerriAI/litellm/pull/37895)** — 修复 Codex 每次 turn 记录为独立 session 的问题（代码中遗漏了 `codex-tui` user agent 和未加前缀的 `session-id`）。PR 已开放。
- **[#30565 [PR] helm 支持 ServiceMonitor 认证抓取](https://github.com/BerriAI/litellm/pull/30565)** — 修复 ServiceMonitor 缺少 `/metrics` 认证、可能通过 master-key 回退泄露管理员凭据的问题。PR 已开放。

**🟢 低（已有关闭修复）**

- **[#27884 429 错误响应泄露 token 完整哈希（已关闭）](https://github.com/BerriAI/litellm/issues/27884)** — 已修复，限制为不输出完整 SHA-256。
- **[#27900 global_max_parallel_requests 不生效（已关闭）](https://github.com/BerriAI/litellm/issues/27900)** — 已关闭，用户需确认新版本是否修复。
- **[#27924 同一模型别名同时支持 /chat/completions 与 /v1/messages（已关闭）](https://github.com/BerriAI/litellm/issues/27924)** — 已关闭，未有明确结论，可能因 stale 关闭。
- **[#27942 /spend/logs 记录 router 模型而非实际选中模型（已关闭）](https://github.com/BerriAI/litellm/issues/27942)** — 已关闭，未明确解决方案，存在记录偏差风险。

**📊 定价/费用类 Bug（新增集中爆发）**

- **[#37823 azure/us/ 和 azure/eu/ gpt-4o-2024-11-20 缺少 cache_read_input_token_cost（3 评论，新开）](https://github.com/BerriAI/litellm/issues/37823)**
- **[#37631 azure/gpt-5.6* 缺少 cache_creation_input_token_cost，自 v1.97.0 起缓存写入计费为 0（2 评论）](https://github.com/BerriAI/litellm/issues/37631)**

这两个问题直接导致用户成本核算偏差，虽然影响的是“少记”而非“多记”，但会干扰成本归因。值得在下一个补丁版本中修复。

---

## 6. 功能请求与路线图信号

**🔥 高热度功能请求（有对应 PR 或明确路线图）：**

- **[#

</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*