# AI CLI 工具社区动态日报 2026-08-15

> 生成时间: 2026-08-14 22:44 UTC | 覆盖工具: 7 个

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



---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告

> 数据来源：github.com/anthropics/skills | 截止 2026-08-15

---

## 一、热门 Skills 排行（按社区关注度 TOP 8）

### 1. skill-creator 评测循环修复 — `#1298` ⚠️ 最热 PR
**功能**：修复 `run_eval.py` 对所有 skill description 一律报告 `recall=0%` 的严重缺陷；同时修复 Windows 流读取、触发检测和并行 worker 问题。
**社区讨论热点**：该问题被 10+ 独立复现（关联 Issue #556，#1169），是描述优化循环"对着噪声调优"的根因。大量 skill 作者因评测数据失真而无法判断描述质量。
**状态**：OPEN
🔗 https://github.com/anthropics/skills/pull/1298

---

### 2. document-typography 文档排版技能 — `#514`
**功能**：针对 AI 生成文档的排版质量控制：孤儿词换行（1-6 词溢出到下一行）、段落孤立在页底、编号错位等普遍问题。
**社区讨论热点**：切中"用户很少主动要求、但每个 Claude 生成的文档都会遇到"的隐性痛点，属于高感知度体验改进。
**状态**：OPEN
🔗 https://github.com/anthropics/skills/pull/514

---

### 3. pdf 技能大小写引用修复 — `#538`
**功能**：修复 `skills/pdf/SKILL.md` 中 8 处大小写不匹配（`REFERENCE.md` → `reference.md`，`FORMS.md` → `forms.md`），解决大小写敏感文件系统上的文档加载失败。
**社区讨论热点**：看似微小但直接影响技能可用性，反映官方文档技能在跨平台兼容性上的疏漏。
**状态**：OPEN
🔗 https://github.com/anthropics/skills/pull/538

---

### 4. ODT 技能（OpenDocument 格式支持）— `#486`
**功能**：新增 ODT/ODS 文件的创建、模板填充、读取及 ODT→HTML 转换能力，填补开源文档格式空白。
**社区讨论热点**：与 LibreOffice/ISO 标准生态对齐，面向政企/开源办公场景的需求明确。
**状态**：OPEN
🔗 https://github.com/anthropics/skills/pull/486

---

### 5. frontend-design 技能重构 — `#210`
**功能**：修订前端设计技能，提升指令清晰度、可执行性和内部一致性，确保每条指令可在单次对话中落地。
**社区讨论热点**：关注 skill 描述从"给人看的文档"转变为"给 Claude 的可执行指令"。
**状态**：OPEN
🔗 https://github.com/anthropics/skills/pull/210

---

### 6. 元技能：skill-quality-analyzer + skill-security-analyzer — `#83`
**功能**：新增两个 meta skill——质量分析器（结构/文档/示例/资源五维评估）与安全分析器，为 Skill 生态自身提供质检能力。
**社区讨论热点**：对应社区对 Skill 质量和安全性的焦虑（见 Issue #492），属于"生态自举"方向。
**状态**：OPEN
🔗 https://github.com/anthropics/skills/pull/83

---

### 7. docx 修订模式 ID 冲突修复 — `#541`
**功能**：修复 DOCX 技能在有书签的文档中添加修订时 `w:id` 冲突导致的文档损坏（OOXML 中书签/修订共用一个 ID 空间）。
**社区讨论热点**：直接回应用户遇到的 Word 文档不可读问题（Issue #12），技术深度高。
**状态**：OPEN
🔗 https://github.com/anthropics/skills/pull/541

---

### 8. self-audit 推理质量门控技能 — `#1367`
**功能**：交付前先做机械性文件核验，再按损害严重度优先级执行四维推理审计，宣称通用适配任何项目/技术栈/模型（v1.3.0）。
**社区讨论热点**：与 #1385 提案形成"质量门控流水线"体系，反映社区对 AI 输出可靠性治理的需求上升。
**状态**：OPEN
🔗 https://github.com/anthropics/skills/pull/1367

---

## 二、社区需求趋势（来自 Issues）

| 趋势方向 | 代表 Issue | 热度信号 |
|---------|-----------|---------|
| **安全与信任边界** | #492：社区技能伪装在 `anthropic/` 命名空间下，形成信任边界滥用漏洞 | 43 评论，最热 Issue |
| **组织级协作共享** | #228：Claude.ai 内 org-wide 技能库/共享链接需求 | 16 评论，👍8 |
| **Skill 工具链可靠性** | #556：`run_eval.py` 0% 触发率；#1169：优化循环 recall=0% | 12+3 评论，高赞 |
| **上下文窗口优化** | #1487：`claude-api` 技能单次注入 ~156k tokens 挤爆上下文 | 4 评论，新锐话题 |
| **记忆与状态压缩** | #1329：compact-memory 技能——符号化紧凑 agent 状态 | 9 评论 |
| **重复/冲突管理** | #189：document-skills 与 example-skills 安装后内容重复 | 6 评论，👍9 高赞 |
| **质量治理与安全治理** | #412：agent-governance 安全模式；#1385：推理质量门控流水线 | 6+4 评论 |
| **平台扩展** | #29：AWS Bedrock 支持；#16：Skills 以 MCP 形式暴露 | 各 4 评论 |

**核心结论**：社区的注意力正从"增加更多技能"转向 **"让技能生态可信、可共享、不爆上下文"**——安全命名空间、评测工具正确性、上下文效率是三大核心诉求。

---

## 三、高潜力待合并 Skills（近期可能落地）

| PR | Skill | 落地潜力信号 |
|----|-------|------------|
| `#1298` | skill-creator 修复 | 直接修复最热 Issue（#556/#1169），多位作者独立复现，合并优先级最高 |
| `#568` | ServiceNow 平台技能 | 覆盖 ITSM/ITOM/SecOps/ITAM 等 10+ 模块，**最近更新 2026-08-12**，作者持续维护 |
| `#1367` | self-audit 质量门控 | 与 #1385 提案联动，发布仅 4 天即获得高讨论度 |
| `#723` | testing-patterns | 覆盖单元测试/React 组件测试/测试哲学全栈，属高频刚需 |
| `#525` | pyxel 复古游戏开发 | 关联知名 MCP 项目（kitao/pyxel），作者即项目作者，生态黏性强 |
| `#83` | skill 质量+安全分析器 | 回应生态治理需求，若与 #492 安全 Issue 挂钩将被加速 |
| `#486` | ODT 文档技能 | 填补开源文档格式空白，与政企迁移场景强相关 |
| `#1479` | plan-file-hygiene | 解决规划产物无生命周期管理的真实痛点，社区提名后落地 |

🔗 全部 PR 列表见：https://github.com/anthropics/skills/pulls

---

## 四、Skills 生态洞察（一句话总结）

**社区当前最集中的诉求不是"更多技能"，而是让 Skill 开发生态本身变得可靠、安全和高效——修复评测工具失真（recall=0%）、杜绝命名空间信任滥用、遏制上下文膨胀，正在

---



</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>



</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-15

## 今日速览

昨日发布 v0.56.0-nightly.20260814，核心方向是**容量错误静默重试机制**与 E2E 测试稳定性。Issue 侧，**Subagent 恢复逻辑误报成功**（#22323，12 条评论）成为社区最热话题，已由 SSR Agent 自动提交修复 PR #28815。此外，一批由 SSR Agent 驱动的自动化 PR 集中合入，系统性修复了 TUI 挂起、PTY 泄漏、消息总线静默失败等历史顽疾。

---

## 版本发布

**v0.56.0-nightly.20260814.gc0d192452**

- **test(e2e)**：稳定 slow runners 上的 file-system-interactive 测试（PR #28793）
- **fix(core)**：为容量错误（capacity errors）实现**上下文感知静默重试**与可用性 TTL 机制（PR #28761）

> 说明：Nightly 版本，重点观察重试逻辑对生产环境 429/容量错误的改善效果。

---

## 社区热点 Issues（Top 10）

### 1. Subagent 达到 MAX_TURNS 后被误报为 GOAL 成功 — #22323
**P1 | 12 评论 | 2 👍 | 已有修复 PR #28815**

`codebase_investigator` 子代理在触发最大轮次限制后，仍被报告为 `status: "success"`、`Termination Reason: "GOAL"`，掩盖了实际的中断。开发者认为这是**错误归因**，会误导上层决策。今日 SSR Agent 已提交修复（#28815），保留原始终止原因。

📎 [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22323)

---

### 2. Generalist Agent 永久挂起 — #21409
**P1 | 8 评论 | 8 👍**

当 CLI 委派任务给 generalist agent 时，执行会永久挂起（用户等待长达 1 小时）。**简单操作如创建文件夹也会触发**。社区用户表示“禁止委派 subagent”可绕过，说明问题出在委派与恢复机制本身。

📎 [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21409)

---

### 3. Shell 命令执行完成后卡在 "Waiting input" — #25166
**P1 | 4 评论 | 3 👍**

简单 CLI 命令执行完毕后，终端仍显示命令活动并停留在“Awaiting user input”，**命令实际早已结束**。严重影响自动化流水线，且复现率高。

📎 [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/25166)

---

### 4. Browser Subagent 在 Wayland 环境下失败 — #21983
**P1 | 4 评论 | 1 👍**

浏览器子代理在 Wayland 会话中无法正常工作，终止原因仅显示 `GOAL` 但无详细诊断信息。图形环境适配问题仍需社区提供更多日志。

📎 [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21983)

---

### 5. get-shit-done 输出 Hook 导致崩溃 — #22186
**P1 | 3 评论**

当 get-shit-done 输出接近完成（打印用户摘要）时，Gemini CLI 反复崩溃。属于 **hook 执行阶段的稳定性缺陷**，优先级高但评论较少，可能影响面有限。

📎 [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22186)

---

### 6. Gemini 不主动使用 Skills 与 Subagents — #21968
**P2 | 6 评论**

用户反馈，即使配置了 `gradle`、`git` 等自定义 skills，Gemini CLI 在相关场景下**几乎从不主动调用**，只有显式指令才会触发。这直接削弱了 skills/subagents 功能的价值。

📎 [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/21968)

---

### 7. Auto Memory 无限重试低信号会话 — #26522
**P2 | 5 评论**

后台提取代理遇到低信号会话（读取后判定无价值）时，会将该会话标记为未处理，导致**同一会话被反复重试**，浪费算力与 token。

📎 [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/26522)

---

### 8. v0.33.0 起 Subagents 未经许可运行 — #22093
**P2 | 3 评论**

升级后，尽管所有配置中 `agents mode` 均为 disabled，generalist 等子代理仍被自动调用。用户质疑权限控制是否失效，**涉及配置兼容性**。

📎 [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/22093)

---

### 9. 超过 128 个工具时出现 400 错误 — #24246
**P2 | 3 评论**

CLI 在启用大量工具（用户环境超 400 个）时直接报 400 错误。开发者期望按场景**限制工具集范围**，而非将所有工具一次性注入上下文。

📎 [查看 Issue](https://github.com/google-gemini/gemini-cli/issues/24246)

---

### 10. Agent 应主动避免破坏性行为 — #22672
**P2 | 3 评论 | 1 👍**

模型在复杂 git 操作和数据库维护等场景下，可能使用

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>



</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报 — 2026-08-15

> 数据来源：[github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

## 今日速览

过去 24 小时，Kimi Code CLI 仓库无新版本发布、无新 PR 更新，但有 4 条 Issue 持续活跃。其中，**跨会话记忆系统**（#1283）以 39 条评论成为社区讨论热度最高的需求，同时远程控制/多设备会话交接（#2269）也获得用户关注。此外，一条关于 **Windows 下 Shell 工具增强** 的旧 Issue（#1136）虽已关闭但仍在更新，值得留意。

---

## 社区热点 Issues

> 过去 24 小时内共 4 条 Issue 更新，已全部收录。按关注度排序如下：

### 1. [#1283] Feature Request: Memory System - Persistent context across sessions（增强：记忆系统 - 跨会话持久上下文）
- **作者**: @CatKang | **创建**: 2026-02-27 | **更新**: 2026-08-14 | **评论**: 39 | **👍**: 0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/1283
- **重要性**: 这是目前仓库中讨论最热烈的一条 Issue（39 条评论遥遥领先），用户期待一个完整的记忆系统，涵盖**自动记忆**(AI 托管的笔记)和**手动记忆**(用户定义的指令)两种模式，以便在不同会话间保留项目模式与用户偏好。高评论量说明社区对该功能存在长期且迫切的需求。
- **社区反应**: 用户围绕记忆的存储形式、隐私边界、与 `agent.md` 的关系等话题展开了密集讨论，但尚未形成明确结论。

### 2. [#2269] Feature Request: Remote Control / Multi-Device Session Handoff（功能请求：远程控制 / 多设备会话交接）
- **作者**: @lucianalima777 | **创建**: 2026-05-13 | **更新**: 2026-08-14 | **评论**: 6 | **👍**: 1
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2269
- **重要性**: 用户希望能在笔记本、网页、手机等多设备之间无缝切换或远程控制同一会话，属于跨环境工作流的核心诉求。对于在本地与远程机器间频繁切换的开发者，这个能力能显著提升效率。
- **社区反应**: 已有 6 条评论，讨论集中于实现方案（如云端会话同步）与安全风险。

### 3. [#1478] 能否优化记忆层？而且我也没在参考文档里看到和记忆有关的东西？搞大项目的时候很痛苦。
- **作者**: @hahy36 | **创建**: 2026-03-17 | **更新**: 2026-08-14 | **评论**: 2 | **👍**: 0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/1478
- **重要性**: 用户明确表达了对当前记忆层的不满：在官方参考文档中找不到与记忆相关的说明（仅看到 `agent.md`），导致大型项目管理非常痛苦。该 Issue 引用了 OpenClaw 的记忆目录结构（SOUL.md / USER.md / MEMORY.md 等）作为参考，是 #1283 的互补视角——**记忆不光是"要有"，更要有文档和透明机制**。
- **社区反应**: 评论较少，但问题指向明确，与 #1283 形成共振，共同构成了记忆主题的"功能+文档"双重诉求。

### 4. [#1136] [CLOSED] feat(shell): enhance shell tool with version-aware PowerShell context
- **作者**: @QIN2DIM | **创建**: 2026-02-13 | **更新**: 2026-08-14 | **评论**: 0 | **👍**: 0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/1136
- **重要性**: 虽然是已关闭的 Issue 且无评论，但 2026-08-14 仍在更新。该建议指出，在 **Kimi K2.5 (SGLang)** 测试中，Shell 工具在 Windows 上的命令生成存在歧义等关键问题（尤其在 pass-1 阶段），需要针对 PowerShell 版本做上下文感知的增强。这暴露了 Windows 平台的兼容性短板。
- **社区反应**: 无评论，但被重新更新可能意味着相关 PR 或关联工作正在推进。

---

## 重要 PR 进展

过去 24 小时内无 PR 更新或合并。

---

## 功能需求趋势

从近期活跃的 Issues 中，可以提炼出社区最关注的三个功能方向：

| 方向 | 代表性 Issue | 热度 |
|------|-------------|------|
| **🧠 跨会话记忆系统** | #1283、#1478 | 高（41 条评论合计） |
| **🌐 多设备远程协作** | #2269 | 中（6 条评论） |
| **🪟 Windows Shell 体验优化** | #1136 | 低（0 条评论，但已关闭仍被更新） |

其中，**记忆系统** 是当前绝对的主题焦点，且存在两条互补诉求：
- **#1283** 侧重于"新增功能"——希望系统化地引入自动/手动记忆；
- **#1478** 侧重于"完善文档"——希望提供记忆机制的权威参考文档。

两者合并来看，社区想要的是一个**有文档、有结构、可手动干预**的记忆系统，可类比 Claude Code 的 `CLAUDE.md` 或 OpenClaw 的目录式记忆管理。

---

## 开发者关注点

- **大型项目记忆痛感强烈**：用户在大项目中反复丢失上下文，且官方文档仅提及 `agent.md`，缺少系统化的记忆层说明（#1478）。
- **记忆系统的双轨需求**：既要有 AI 自动维护的记忆笔记，也要有用户可显式定义的手动指令，两者需要清晰共存（#1283）。
- **跨设备工作流衔接缺失**：部分用户在多设备（如本地笔记本 + 远程服务器）环境中工作，希望可以在设备间接力或远程控制会话（#2269）。
- **Windows 平台存在命令生成的可靠性问题**：在 K2.5 模型的初始命令生成阶段，PowerShell 环境下的行为有歧义，影响 Agent 在 Windows 上的执行效率（#1136）。

---

## 小结

过去一天 Kimi Code CLI 开发节奏相对平静，但社区对**记忆系统**的讨论热度正在上升。建议关注 #1283 的进展——如果官方在后续版本中引入记忆层机制或补充相关文档，将直接回应一个高浓度的社区诉求。同时，Windows 用户的 Shell 工具体验也是潜在需要投入的方向。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报

**日期：2026-08-15** | 数据来源：[github.com/anomalyco/opencode](https://github.com/anomalyco/opencode)


## 今日速览

昨日（8月14日）出现了一次**严重故障**：ID 生成器的 48 位时间戳在 `2026-08-14 12:39:55 UTC` 发生回绕，导致大量既有会话（尤其桌面端）停止响应，引发多个重复 Issue（[#42608](https://github.com/anomalyco/opencode/issues/42608)、[#42605](https://github.com/anomalyco/opencode/issues/42605)、[#42594](https://github.com/anomalyco/opencode/issues/42594) 等），目前该 Issue 已关闭，但影响仍在社区发酵。同时，社区最大的长期关注点仍是内存问题（“Memory Megathread”已有 131 条评论、98 个 👍），且一个大型 PR（[#42660](https://github.com/anomalyco/opencode/pull/42660)）带来了自定义 OpenAI 兼容提供商的**动态模型发现**功能，有望解决多个历史顽疾。


## 社区热点 Issues

### 🔴 故障与严重问题

1. **[#42608] 48 位 ID 时间戳回绕卡死所有历史会话**（已关闭，👍 3）
   2026-08-14 12:39:55 UTC 起，该 Bug 导致所有早于此时间创建的会话静默停止处理提示词，用户输入 prompt 完全无响应，影响面覆盖桌面端与 CLI。核心原因定位在 `packages/opencode/src/id/id.ts`，是当天社区最严重的事件。
   https://github.com/anomalyco/opencode/issues/42608

2. **[#20695] 内存问题集中讨论帖**（131 评论 / 👍 98）
   这是社区最活跃的 Issue，旨在集中收集堆快照以排查内存泄漏。维护者明确要求**不要运行 LLM 来瞎猜解决方案**（“PLEASE DO NOT RUN YOUR LLM AND SUGGEST SOLUTIONS IT IS ALWAYS WRONG”），呼吁用户按文档提供手动堆快照。关注度最高，已持续 4 个月。
   https://github.com/anomalyco/opencode/issues/20695

3. **[#36997] 桌面版 v1.18.1 新布局隐藏代理切换 UI**（12 评论 / 👍 6）
   新布局设计下，Plan/Build 代理切换指示器被隐藏，Tab 键也失效，用户无法确认当前代理模式，属高影响 UI 回归。
   https://github.com/anomalyco/opencode/issues/36997

4. **[#42657] 多子代理会话 TUI 严重卡顿**（新，2 评论）
   2-4 个并发子代理时，TUI 渲染线程 CPU 占用高达 97%，输入延迟 1-3 秒，在 Warp、Windows Terminal、WezTerm 中均复现。
   https://github.com/anomalyco/opencode/issues/42657

5. **[#42215] 新会话持续收到 429 限流**（👍 2）
   用户反馈即使过了 24 小时配额窗口，免费模型仍报告“Free Usage Exceeded”，付费用户也被限流，直接影响 Zen API 使用体验。
   https://github.com/anomalyco/opencode/issues/42215

6. **[#42605] 会话保持打开但代理不再响应后续提示**（新）
   与 #42608 同源（时间戳回绕），但此问题发生在回绕时间点之后，说明修复可能不完整，需持续关注——代理完成任务后，新消息无法被处理。
   https://github.com/anomalyco/opencode/issues/42605

### 💡 功能与兼容性

7. **[#27553] 自动发现 OpenAI 兼容提供商的模型列表**（👍 4）
   用户希望自动调用 `/v1/models` 端点发现模型，避免手动在 `opencode.json` 中逐一配置。这与 PR #42660 直接相关，是该 PR 关闭的 6 个 Issue 之一。
   https://github.com/anomalyco/opencode/issues/27553

8. **[#41518] gpt-5.6-luna 经 OpenCode Go 中继返回 403 区域限制**
   通过 `opencode.ai` 的 OpenCode Go 中继访问 `gpt-5.6-luna` 时报 403 “模型不可用”，疑似上游区域策略问题。
   https://github.com/anomalyco/opencode/issues/41518

9. **[#25000] DeepSeek V4 Pro 多轮工具调用时 `reasoning_content` 报错**
   经 `opencode.ai/zen/go/v1` 使用 DeepSeek V4 Pro 时，多轮工具调用间歇性报“The `reasoning_content` in the thinking mode must be passed back to the API”，根源是其与 OpenAI 兼容协议的不一致。
   https://github.com/anomalyco/opencode/issues/25000

10. **[#37489] 切换模式/压缩期间上下文缓存失效导致性能下降**
    连接本地推理引擎（vLLM/Ollama）时，模式切换或 context 压缩会触发缓存失效，导致大量重复 prefill，显著降低响应速度。
    https://github.com/anomalyco/opencode/issues/37489

### 其他值得关注

- **[#42635]** TUI 系统主题在终端复用器（herdr）中不刷新调色板，需手动触发 `\e[?997` 报告。https://github.com/anomalyco/opencode/issues/42635
- **[#41909]** 请求新增 `/approve on|off` 滑杆命令，运行时切换权限审批模式。https://github.com/anomalyco/opencode/issues/41909
- **[#33966]** 请求将 `OAUTH_CALLBACK_HOST` 配置化（当前被 PR #30022 硬编码为 127.0.0.1）。https://github.com/anomalyco/opencode/issues/33966
- **[#41120]** Kimi 模型（kimi-k3 / kimi-k2.7-code）的 Anthropic 路由工具调用报 400。https://github.com/anomalyco/opencode/issues/41120


## 重要 PR 进展

### 功能上新

1. **[#42660] 为自定义提供商添加动态模型发现**（新，OPEN）
   通过调用 OpenAI 兼容提供商的 `/v1/models` 自动拉取模型列表，**一次性关闭 6 个相关 Issue**（#13891、#29308、#28999、#25624、#23327、#26863）。实践了社区呼声最高的需求之一。
   https://github.com/anomalyco/opencode/pull/42660

2. **[#36869] 每工具执行超时 + 中止 + 会话恢复**
   为内置和 MCP 工具提供可配置超时（默认与可调），超时后中止工具调用并恢复会话循环，避免工具挂起导致代理无响应。关联 #20096、#34888 等 5 个 Issue。
   https://github.com/anomalyco/opencode/pull/36869

### 核心修复

3. **[#36943] 修复：被中断的会话保持停止状态**
   通过 durable admission sequence 隔离被中断的会话，抑制中断前已准入的 prompt 唤醒，同时保留真正的新 prompt。解决“中断后旧 prompt 复活”的竞态问题。
   https://github.com/anomalyco/opencode/pull/36943

4. **[#36861] 从 openai 兼容元数据中恢复缓存 token**
   自定义 baseURL 提供商可能通过 provider metadata 上报缓存 token（如 `prompt_tokens_details`），该 PR 确保这些 token 被正确计入会话缓存统计。
   https://github.com/anomalyco/opencode/pull/36861

5. **[#36898] 处理后代权限请求**
   修复 headless `opencode run` 只响应根会话权限请求的问题——Task 子会话请求权限时不再被阻塞，自动化场景更可靠。
   https://github.com/anomalyco/opencode/pull/36898

6. **[#36862] 按协议验证 `openExternal` URL**
   修复 Electron 桌面端 `shell.openExternal` 接受任意 URL 的安全漏洞，阻止 `file://`、`javascript:` 等危险协议。关闭 #30613。
   https://github.com/anomalyco/opencode/pull/36862

### 性能与稳定性

7. **[#36851] 数据库自动 vacuum + 定期维护**
   避免 SQLite 文件膨胀，提升长时间使用后的查询性能。关闭 #31526。
   https://github.com/anomalyco/opencode/pull/36851

8. **[#36853] 降低会话切换时的响应式级联开销**
   重构减少 session 切换时大量 reactive 更新带来的 UI 卡顿/闪烁，是桌面端流畅度的重要优化。
   https://github.com/anomalyco/opencode/pull/36853

9. **[#36916] 排队并发子代理问题**
   按请求 ID 对全根会话树的待处理问题排序，确保当前活动请求保持选中状态，修复多子代理并发提问时的 UI 错乱。
   https://github.com/anomalyco/opencode/pull/36916

### 其他

- **[#42656]** 将 worktree 路由移出 `experimental` 命名空间，API 规范化。https://github

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报
**2026-08-15** | 数据来源：[QwenLM/qwen-code](https://github.com/QwenLM/qwen-code)

---

## 今日速览

昨日发布了 **v0.21.12** 正式版，重点引入 Web Shell 工作区文件拖拽上传能力，并针对 autofix 审查流程加入 diff 增长制动器。社区侧最受关注的是 **#8957 图片加载崩溃回归问题**（12 条评论）与 **#9002 Python SDK 参数校验不一致** 的讨论；同时 **#9127 会话级媒体引用端到端支持** PR 展示出社区对多模态能力的强烈需求。

---

## 版本发布

### v0.21.12（正式版）
- **Web Shell 文件上传**：支持在工作区通过拖拽或 `@` 文件面板上传文件，并带有进度跟踪（[#8874](https://github.com/QwenLM/qwen-code/pull/8874)）
- **autofix 审查改进**：实现 diff 增长制动器（diff growth brake），限制自动修复过程中的扩散

### v0.21.12-preview.4 / preview.3
- `fix(web-shell)`: 保留独立会话目标（[#9038](https://github.com/QwenLM/qwen-code/pull/9038)）
- `feat(web-shell)`: 支持工作区文件上传

### 端到端验证基准
- `dsw-eas-tb-e2e-20260814-r6`：完整验证通过，SWE-bench Verified 500、Terminal-Bench 2.0 89

---

## 社区热点 Issues

### 1. [Regression] Qwen Code 自 0.21.2 起加载图片即崩溃
- **#8957** | `[P2/bug/core]` | 评论 12 · 更新 08-14
- 自 0.21.1 后，读取图片时 Qwen Code 立即崩溃，影响核心功能。目前标签为 `need-information`，社区等待维护者进一步确认。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/8957)

### 2. 大会话恢复超时时无法保留当前会话
- **#8678** | `[P1/bug/core]` | 评论 9 · 已关闭
- 维护者已确定该问题为“部分解决并被取代”，包含请求级恢复超时、附件身份隔离等多项验收标准。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/8678)

### 3. 多工作区 daemon 资源使用无上限
- **#8051** | `[P2/feature-request/performance]` | 评论 9
- 仅按数量限制工作区和会话，无法约束请求体、WebSocket 组装等字节级资源占用，社区持续关注生产环境稳定性。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/8051)

### 4. core + CLI 架构审查：12 项结构性问题清单
- **#4063** | `[type/enhancement]` | 评论 8 · 👍 1
- 核心类型系统被 `@google/genai` 绑架，136 个文件直接依赖该包。P0 级架构问题引发社区对可维护性的广泛讨论。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/4063)

### 5. Python SDK 拒绝 `permission_mode="auto"`
- **#9002** | `[P3/bug/SDK]` | 评论 6
- SDK 客户端校验只允许 `default/plan/auto-edit/yolo`，与 CLI 支持的 `auto` 不一致，导致 API 无法使用该参数。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9002)

### 6. `/compress` 后状态栏上下文占比不刷新
- **#6806** | `[P2/bug/UI]` | 评论 5
- 压缩后 footer 显示仍停留在压缩前的 token 占比，需要下一次模型请求才更新。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/6806)

### 7. 只读 Shell 分类器可被命令替换绕过
- **#8582** | `[P1/security]` | 评论 5 · 已关闭
- AST 分类器与运行时替换门禁均可绕过（利用行延续或 `${var@P}`），存在任意代码执行风险，已修复。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/8582)

### 8. ACP 子进程报错 `Unknown argument: acp`
- **#8871** | `[P2/bug/ACP]` | 评论 5
- `qwen serve --http-bridge=true` 下子进程无法解析 `--acp` 标志，导致 token 认证失败。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/8871)

### 9. 长会话内存无限增长
- **#2128** | `[P1/enhancement/memory]` | 评论 4
- UI History 数组无上限累积，数十小时会话后内存持续增长不释放，是长期运行用户的核心痛点。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/2128)

### 10. `utils/` 目录循环依赖重构
- **#9146** | `[P2/refactor]` | 评论 4
- 51 个文件的 107 个向上导入使目录图成环，社区建议将 `utils/` 变为叶子层。
- [查看 Issue](https://github.com/QwenLM/qwen-code/issues/9146)

---

## 重要 PR 进展

### 1. Web Shell 采用 Goal v3 控制平面
- **#9087** | `feat(web-shell)` | @qqqys
- 在首条消息前即可创建/编辑/暂停/恢复/替换/清除 Goal，无需路由命令给模型，并提供紧凑展示行。
- [查看 PR](https://github.com/QwenLM/qwen-code/pull/9087)

### 2. 会话媒体引用端到端支持
- **#9127** | `feat(session-media)` | @ytahdn
- 图片上传一次后以媒体 ID + 元数据贯穿 daemon/ACP bridge/SDK/Web Shell，支持提示提交、中途队列、注入消息回显与对账快照。
- [查看 PR](https://github.com/QwenLM/qwen-code/pull/9127)

### 3. 新增 Kimi 与小米 MiMo 服务提供商
- **#8368** | `feat(auth)` | @DragonnZhang
- `/auth` 第三方提供商新增 Kimi（Coding Plan / 中国 / 国际 API Key）与小米 MiMo（按量付费 + 中国/新加坡/国际区域）。
- [查看 PR](https://github.com/QwenLM/qwen-code/pull/8368)

### 4. 隐私安全的工具结果边界诊断
- **#9039** | `feat(core)` | @doudouOUC
- 添加隐私安全的工具结果边界诊断能力，

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*