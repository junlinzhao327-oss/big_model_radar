# AI CLI 工具社区动态日报 2026-08-24

> 生成时间: 2026-08-23 22:42 UTC | 覆盖工具: 7 个

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

# Claude Code Skills 社区热点报告（数据截至 2026-08-24）

> 说明：PR 评论数字段在本次数据快照中缺失，以下排名基于仓库自身「按评论数排序」的呈现顺序；所有热门 PR 当前状态均为 Open（无 merged/draft）。

---

## 1. 热门 Skills 排行（Top 8 PR）

**#1298 skill-creator 评估修复** — ❝run_eval.py 永远报 0% recall❞
修复 `run_eval.py` 在所有测试查询下触发率恒为 0% 的严重问题（对应 issue #556，已有 10+ 独立复现），涉及 Windows 流读取、触发检测、并行 worker。该问题导致 skill-creator 的优化闭环「对着噪声调参」，是整个生态最痛的工程债。  
状态：Open  
https://github.com/anthropics/skills/pull/1298

**#514 document-typography 技能（文档排版质检）**
防止 AI 生成文档的典型排版缺陷：孤行（1–6 词溢出到下一行）、寡段（标题滞留在页底）、编号错位。通用性强，适配所有 Claude 生成的办公文档。  
状态：Open  
https://github.com/anthropics/skills/pull/514

**#538 pdf 技能大小写引用修复**
修正 `skills/pdf/SKILL.md` 中 8 处大小写不一致的引用（`REFERENCE.md`→`reference.md`、`FORMS.md`→`forms.md`），在大小写敏感文件系统上会导致技能引用直接失效。讨论聚焦「官方技能也应通过社区 review 保证跨平台可用性」。  
状态：Open  
https://github.com/anthropics/skills/pull/538

**#486 ODT 技能（OpenDocument 文本创建与转换）**
覆盖 .odt/.ods 文件的创建、模板填充、ODT→HTML 解析，触发词包括 ODT/ODS/ODF/OpenDocument/LibreOffice。回应了办公文档开源格式的社区刚需。  
状态：

---

# Claude Code 社区动态日报 — 2026-08-24

## 今日速览

v2.1.241 发布，仅包含常规 bug 修复与可靠性改进。社区热度高度集中于 #77136——用户集中反馈 Claude 4.7+ 及 Fable 模型输出出现“修辞性口头禅”与上下文连贯性退化，成为当前最受关注的产品质量问题。PR 侧活动低迷，24 小时内仅有 1 个文档 PR，无新功能合入。

## 版本发布

### v2.1.241
- 内容：Bug fixes and reliability improvements
- 说明：补丁版本，无新增功能，官方未披露具体修复项。建议关注更新后是否有回归反馈。

## 社区热点 Issues

挑选了 10 个当前讨论价值最高的 Issue：

### 1. 模型文风退化：#77136
👉 [github.com/anthropics/claude-code/issues/77136](https://github.com/anthropics/claude-code/issues/77136)
- 状态：OPEN ｜ 评论 89 ｜ 👍 351
- 核心：用户反映 Claude 4.7/4.8/5.0 与 Fable 默认倾向输出重复的修辞套话（“口头禅”），即便给定明确风格指令，仍难以产出连贯散文。
- 分析：这是目前社区声量最大的单点 Issue，点赞数远超其他问题，说明模型输出质量已成为大量用户的核心痛点，而非个别使用习惯问题。

### 2. Windows 文件编码损坏：#7134
👉 [github.com/anthropics/claude-code/issues/7134](https://github.com/anthropics/claude-code/issues/7134)
- 状态：OPEN ｜ 评论 27 ｜ 👍 23
- 核心：Claude Code 读写文件时不尊重原始编码，导致 Windows-1252 等非 UTF-8 文件被破坏。
- 分析：从 2025 年 9 月持续至今仍未解决的长尾 bug，Windows 中文本地化用户受影响较大，但关注度相对有限。

### 3. Fable 5 文本块被摘要为 thinking 块：#74558
👉 [github.com/anthropics/claude-code/issues/74558](https://github.com/anthropics/claude-code/issues/74558)
- 状态：OPEN ｜ 评论 9 ｜ 👍 8
- 核心：Fable 5 在对话中段偶尔将完整 assistant 文本块作为“摘要式 thinking 块”交付，导致界面显示“静默”但 token 仍在消耗。
- 分析：包含完整 repro 与 JSONL 证据，直接影响 Fable 5 用户的可观察性和调试体验。

### 4. 桌面浏览器面板阻断内网资源：#87472
👉 [github.com/anthropics/claude-code/issues/87472](https://github.com/anthropics/claude-code/issues/87472)
- 状态：OPEN（新建于 8-17）｜ 评论 3
- 核心：桌面应用内置浏览器面板加载私有网段（RFC1918）Web 应用时，所有子资源被 net::ERR_BLOCKED_BY_CLIENT 拦截，页面渲染空白。
- 分析：较新的沙箱/权限问题，影响企业用户在内网环境使用 Claude 桌面端浏览器组件。

### 5. 跨会话 SendMessage 在 Windows 静默失败：#87501
👉 [github.com/anthropics/claude-code/issues/87501](https://github.com/anthropics/claude-code/issues/87501)
- 状态：OPEN ｜ 评论 2
- 核心：macOS 发送方向原生 Windows 会话通过 Remote Control 发 SendMessage，返回 success:true 但消息实际未被对方会话接收。
- 分析：多会话协作（Cowork）刚起步，此类跨平台消息可靠性问题会直接打击该功能的信任度。

### 6. Plan Mode 并行子代理触发 400 错误：#80881
👉 [github.com/anthropics/claude-code/issues/80881](https://github.com/anthropics/claude-code/issues/80881)
- 状态：OPEN ｜ 评论 1
- 核心：在 Plan Mode 下启动多个并行 background subagents 时，API 返回 400 “system content must contain at least one block”。
- 分析：涉及规划模式与并行执行边界组合，属于 API 层面的参数构造缺陷，对使用 Agent 编排复杂任务的用户有阻塞性影响。

### 7. 多会话协调原语设计讨论：#48965
👉 [github.com/anthropics/claude-code/issues/48965](https://github.com/anthropics/claude-code/issues/48965)
- 状态：CLOSED（stale）｜ 评论 11
- 核心：用户提出一套完整的跨会话协作原语（消息传递、会话注册表、压缩抗性状态、共享任务板），用于“一个 PM + N 个 worker”的协调模式。
- 分析：虽被 stale 关闭，但反映了社区对 Claude Code 从单人工具走向多智能体编排平台的明确诉求，且与当前 SendMessage 功能方向匹配。

### 8. NotebookRead 工具缺失：#60844
👉 [github.com/anthropics/claude-code/issues/60844](https://github.com/anthropics/claude-code/issues/60844)
- 状态：CLOSED（stale）｜ 评论 5
- 核心：请求新增 NotebookRead 工具高效读取 Jupyter notebook 单元；现有 Read 工具常因文件过大（含输出）被阻塞。
- 分析：数据科学与 Notebook 工作流用户的实际需求，因长期未获响应被自动关闭，但仍有一定代表性。

### 9. 记忆失效问题：#73024
👉 [github.com/anthropics/claude-code/issues/73024](https://github.com/anthropics/claude-code/issues/73024)
- 状态：CLOSED ｜ 评论 4
- 核心：用户反馈 Claude Code “什么都不记得”，跨会话记忆几乎为零。
- 分析：标题极具传播性，但未提供足够复现信息，最终被关闭。记忆功能仍是用户感知最强烈的短板之一。

### 10. 嵌套仓库无法从 @repo 选择器访问：#72482
👉 [github.com/anthropics/claude-code/issues/72482](https://github.com/anthropics/claude-code/issues/72482)
- 状态：CLOSED ｜ 评论 3 ｜ 👍 2
- 核心：在父目录打开 Claude Agents 时，@repo 选择器无法发现嵌套在多层子文件夹中的 git 仓库。
- 分析：社区普遍使用单根目录聚合多个项目的工作流，此问题直接影响 repo 发现效率。

## 重要 PR 进展

过去 24 小时 PR 活动极少，数据集中仅 1 个 PR 有更新：

### #83374 docs(plugin-dev): document MessageDisplay streaming semantics
👉 [github.com/anthropics/claude-code/pull/83374](https://github.com/anthropics/claude-code/pull/83374)
- 作者：@iCodeCraft
- 核心：为内置的 Hook 开发技能补充 MessageDisplay 事件说明。当前文档缺失该事件在 trigger 描述、事件指南及速查表中的条目，本次 PR 将其完整补入。
- 分析：非功能性改动，但说明插件/ Hook 开发文档存在信息盲区；同时折射出当前主线开发重心不在文档完善上。

> 提示：过去 24 小时无功能性 PR 合入或更新，v2.1.241 为主要交付物。

## 功能需求趋势

从近期 Issue 中提炼出社区最关注的几个方向：

1. **跨会话 / 多智能体协作生态**（#48965、#87501、#73617）
   用户不再满足于单会话，而是期望“PM + worker”模式、会话间消息可靠传递、远程控制时的授权输入等能力成为一等公民。

2. **Fable 5 模型行为可控性**（#74558、#73603、#73604、#73599）
   大量 Fable 5 相关报告集中在安全分类器误报和模型回退上，社区希望有更透明的降级机制和更宽松的守卫策略。

3. **Windows 平台体验补齐**（#7134、#73590、#73613）
   编码处理、配置文件持久化、插件隔离等 Windows 专属问题的修复优先级，预期会随用户占比提升而上升。

4. **专用读取工具与 Notebook 支持**（#60844）
   数据类用户希望 Claude Code 提供针对 Jupyter 等富文档格式的高效读取工具，而非依赖 Python 脚本或勉强使用通用 Read。

5. **桌面端浏览器面板与沙箱精细化**（#87472、#73593）
   内置浏览器的网络访问边界、LAN 访问策略、窗口焦点管理成为桌面端体验的新关注点。

## 开发者关注点

1. **输出质量下降 + token 消耗并存**：#77136 的 351 👍 说明“写不好”已成为比“写不出”更严重的体验衰退；而 #74558 与 #73601 进一步揭示“文本转 thinking 块”和“子代理死循环”会在用户不知情时大量消耗 token。

2. **成本可见性不足**：#73615 中 session 显示 $60、实际扣费 $300 的差异报告，指向动态工作流成本归因不透明的问题，已影响用户对大额任务投入的信心。

3. **配置与状态脆弱性**：#73590 中 Windows 下 `~/.claude.json` 反复损坏并静默清空 mcpServers；#73565 中 bridge 重启导致环境 ID 变化、所有定时任务被自动禁用——这两个问题都会让 Agent 的长期自治运行“悄悄失能”。

4. **安全过滤误伤的挫败感**：多个并发 Issue（#73599、#73604、#73594）反映 Fable 5 将合法开发行为（如 Amiga 模拟器开发、hermes skill 编写）判定为违规，触发降级或中断，开发者普遍将其视为“假阳性带来的强制打断”，而非安全防护的有效性。

5. **长时间自主运行的稳定性欠缺**：#73561 中 wakeup 驱动的 8 小时监控会话出现“助理文本渲染不一致”；#73601 中恢复的子代理在 3 小时内烧掉约 1000 万 token 且零输出，这类问题会直接动摇用户对 Agent 后台自治运行的信任。

---

> 本日报基于 GitHub 公开数据整理，信息截至 2026-08-24。Issue 状态、评论数、点赞数均为数据抓取时快照，后续可能发生变化。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-24

## 今日速览

昨日无新版本发布，社区讨论热度集中在 Windows 平台稳定性（性能卡顿、沙箱权限）及 GPT-5.6 Sol 模型行为差异（上下文窗口缩减、originator 区分）。PR 方面则有大量关于内容分类与注解（ContentItemKind）系统的内部一致性修复合并，以及一个 MongoDB 线程存储的实验性 PR 仍在推进。

## 社区热点 Issues

1. **[#20214] Codex App 在 Windows 11 Pro 上频繁卡顿/不流畅**  
   108 条评论、87👍，是本日最热 issue。用户反馈在系统资源充足（Ryzen 5 5600 + 32GB RAM）的情况下，从 Microsoft Store 安装的 Codex App 仍频繁卡顿，社区正在讨论是否与 GPU 加速或合成器相关。  
   https://github.com/openai/codex/issues/20214

2. **[#39392] gpt-5.6-sol 触发 `unsupported prompt_cache_retention` 导致中止**  
   39 条评论、37👍。最新版桌面端（26.814.41407）搭配 gpt-5.6-sol 时，app-server 在请求中携带了不受支持的 `prompt_cache_retention` 参数，导致任务直接中止。用户猜测是模型端尚未支持该参数。  
   https://github.com/openai/codex/issues/39392

3. **[#38350] 循环定时任务在成功运行后自动禁用**  
   34 条评论。ChatGPT Work 网页端的计划任务会无故从 enabled 变为 paused，且无需用户任何操作。一次出现四个不相关任务同时被禁用，疑似状态管理回归。  
   https://github.com/openai/codex/issues/38350

4. **[#25178] Windows 10 Computer Use 截图功能失败**  
   29 条评论、16👍。`get_window_state` 截图调用被底层 `SetIsBorderRequired` 接口拒绝（0x80004002），但窗口激活、键盘输入、可访问性文本均正常，定位为 Windows 桌面会话截图权限缺陷。  
   https://github.com/openai/codex/issues/25178

5. **[#25928] VS Code / Cursor 插件提交的 Prompt 随机消失**  
   28 条评论、18👍。Cursor 环境下 Prompt 提交后未进入队列即消失，用户必须重新提交多次才能成功。该 issue 已被标记为多个相关问题的汇聚点（duplicate target）。  
   https://github.com/openai/codex/issues/25928

6. **[#39903] 增加选项禁用“Ran N commands”折叠显示**  
   12 条评论、27👍。TUI 自动折叠已执行命令，用户希望增加配置项始终展开显示。点赞较高，属于社区呼声强烈的体验类改进。  
   https://github.com/openai/codex/issues/39903

7. **[#33192] Windows 10 DWM Composition 句柄在任务结束后持续累积**  
   12 条评论、10👍。有 terminal 工具调用的任务会使 DWM 句柄数持续增长，一次 5 次调用的实验增加 22 个句柄且不释放，长时间使用时可能伴随图形性能下降。  
   https://github.com/openai/codex/issues/33192

8. **[#34619] 请求恢复 GPT-5.6 Sol 的 372k Codex 上下文窗口**  
   6 条评论、23👍。用户发现上下文窗口从 372k 缩减，要求恢复或提供 opt-in 设置。此问题与 #40258 联动，社区对模型上下文策略透明度提出质疑。  
   https://github.com/openai/codex/issues/34619

9. **[#40258] GPT-5.6 Sol 模型目录按 `originator` 头区分：编码端仅获 272K**  
   同账号下 `/backend-api/codex/models` 响应因 `originator` 头不同而返回不同上下文窗口（编码端 272K vs 其他 872K）。此 issue 揭示了模型能力在客户端侧的隐性分层，影响开发者对大上下文任务的规划。  
   https://github.com/openai/codex/issues/40258

10. **[#30105] macOS 桌面端因并发 sqlite 访问启动失败**  
    5 条评论。当 IDE 扩展的 app-server 持有 `logs_2.sqlite` 时，桌面端无法初始化本地数据库并弹出阻塞式错误对话框，且非损坏、非空间问题，属于锁机制缺陷。  
    https://github.com/openai/codex/issues/30105

## 重要 PR 进展

1. **[#31175] [OPEN] 添加 MongoDB 线程存储与会话迁移支持**  
    唯一处于 OPEN 状态的 PR。通过 `experimental_thread_store = { type = "mongodb", ... }` 引入实验性 MongoDB 后端，并提供 `codex sessions migrate-to-mongo` 迁移命令（含进度、警告、验证与命名空间清理）。面向大规模会话管理的企业级能力。  
    https://github.com/openai/codex/pull/31175

2. **[#40281] 图像准备期间保留内容 kind 元数据**  
    在图像预处理改写消息内容时，确保位置性 `content-item-kind` 元数据与重写后的内容保持一致，避免内容错位。  
    https://github.com/openai/codex/pull/40281

3. **[#40280] 远程压缩时对保留图像进行预算控制**  
    新增 `compaction_image_budget` 特性，让图像按 token 计入保留消息预算，防止图像密集型历史超出预算边界。  
    https://github.com/openai/codex/pull/40280

4. **[#40277] 省略不支持的媒体时保留注解**  
    将无法处理的图像/音频输入渲染为 `images.unsupported` 与 `audio.unsupported` 的上下文片段，保持其注解可见。  
    https://github.com/openai/codex/pull/40277

5. **[#40275] 对额外生成的上下文片段进行分类**  
    为压缩摘要、Guardian 批准操作、子代理通知等注入统一的 `content_item_kind` 分类（如 `compaction.summary`、`guardian.approved`），增强调试与过滤能力。  
    https://github.com/openai/codex/pull/40275

6. **[#40271] 模型切换回滚时保留内容注解**  
    修复将模型切换指令回滚为原始内容时，开发者片段元数据丢失的问题，并补充了回归测试。  
    https://github.com/openai/codex/pull/40271

7. **[#40266] 过滤分叉 agent 历史时保留内容注解**  
    在子代理生成所需的父历史准备过程中，开发者消息内容与 `content_item_kinds` 保持对齐。  
    https://github.com/openai/codex/pull/40266

8. **[#40264] 截断消息时保留内容元数据**  
    重建截断消息时避免 passthrough 元数据丢失，同时保持位置分类与剩余条目同步。  
    https://github.com/openai/codex/pull/40264

9. **[#40196] 为用户输入与上下文片段注解内容 kind**  
    为用户文本、图像、音频分别分配 `user.text`、`user.image`、`user.audio` kind，并保持原始顺序。  
    https://github.com/openai/codex/pull/40196

10. **[#40186] 将独立记忆请求识别为记忆整合**  
    将 `thread_source` 设为 `memory_consolidation`，并在请求头与嵌套 `client_metadata` 中验证，改善遥测与调试可观测性。  
    https://github.com/openai/codex/pull/40186

## 功能需求趋势

- **会话/分支可靠性**：多个 issue（#37719、#38552、#39823、#36551）反映会话恢复在高频场景下不稳定，涉及“active writer 冲突”、“Conversation interrupted”、“resume 超时”等；开发者希望 Codex 支持更健壮的会话持久化与恢复机制。
- **模型上下文透明化**：用户对 GPT-5.6 Sol 上下文窗口缩减（#34619）以及按客户端类型差异化授予上下文大小（#40258）敏感，社区更倾向于显式、一致的上下文限制配置。
- **Windows 平台深度适配**：从卡顿（#20214、#33192）到沙箱/文件权限（#33806、#34294）、Computer Use 截图（#25178）再到 Chrome 控制（#40228），Windows 用户反馈量远超其他平台，成为当前最大的社区痛点。
- **自动化与监控工作流**：#32993 提出长期任务的自愈监控；#38350 暴露定时任务状态管理缺陷，显示用户在将 Codex 运用于无人值守场景时对可靠性的关注。
- **上下文内容可观测性**：PR 中大量新增 `ContentItemKind` 分类、注解保留、图像预算控制，说明团队正在系统化提升对上下文内容的可追踪性与可审计性。

## 开发者关注点

- **Windows 性能问题集中爆发**：卡顿、DWM 句柄泄漏、截图接口失败、沙箱权限冲突，Windows 端体验明显落后于 macOS，开发者希望获得同等的功能稳定性和性能。
- **会话数据完整性风险**：历史记录损坏（#23126）、SQLite 并发访问失败（#30105）、事件丢失导致会话污染（#38234），用户对本地数据安全与可迁移性的担忧逐渐上升。
- **模型端与客户端的参数兼容性**：`prompt_cache_retention` 这类模型端不支持参数被直接传递，反映出客户端需要更完善的模型能力探测，仅靠版本号判断不够可靠。
- **任务自动化的状态失控**：定时任务被意外暂停、会话恢复产生重复上下文（#39951），开发者担心自动化任务在无人值守时出现状态漂移而无人察觉。
- **输入丢失与排队机制**：IDE 插件 Prompt 随机消失仍未彻底解决，高频用户受影响严重，期望官方在输入队列持久化、错误可见性层面有明确改进。

> 引用链接均可在 https://github.com/openai/codex 下访问。本日报基于 2026-08-23 至 2026-08-24 期间的公开数据自动整理，如有遗漏，以 GitHub 实际页面

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>



</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报（2026-08-24）

## 今日速览
昨日发布 v1.0.81-8，新增 Grok 4.6 xhigh 推理支持，并优化了本地插件的实时加载机制——编辑插件后 `/restart` 即可生效，无需手动 `/plugin update`。Issue 方面，企业认证问题（#2306）持续近 5 个月仍未根治，同时上下文压缩导致数据丢失（#4572）、Windows 下 VS Code 文件锁导致插件安装失败（#4570）等新问题浮出水面。PR 活动较为冷清，24 小时内仅有 1 条提交。

## 版本发布：v1.0.81-8
- **新增**：为 Grok 4.6 添加 `xhigh` 推理努力级别支持。
- **改进**：
  - 目录源的本地插件现在从其真实目录实时加载，编辑后通过 `/restart` 或新会话即可生效，无需 `/plugin update`。
  - 技能与自定义代理的可发现性提升。

链接：https://github.com/github/copilot-cli/releases

## 社区热点 Issues（Top 10）

### 1. 企业策略认证反复失败（#2306）
- **作者**：@stewartadvt | 更新：2026-08-23 | 评论：9 | 👍：3
- **要点**：每周出现数次 "You are not authorized to use this Copilot feature” 错误，过一段时间又自动消失。持续近 5 个月，是企业用户的一大痛点。
- 链接：https://github.com/github/copilot-cli/issues/2306

### 2. v1.0.81 预发布版 `store_memory` 失败（#4535）
- **作者**：@DavidTeju | 更新：2026-08-23 | 评论：5
- **要点**：`store_memory` 在 1.0.81 预发布版中持续报错 `Instance id is required`——原生记忆写入器被调用时缺少必需的实例 ID，上下文记忆功能不可用。
- 链接：https://github.com/github/copilot-cli/issues/4535

### 3. 后台压缩丢失并行工具结果，触发 HTTP 400（#4572）
- **作者**：@koboldul | 更新：2026-08-23 | 评论：1
- **要点**：长上下文 GPT-5.6-sol 会话在自动后台压缩后立即报 `CAPIError: 400 No tool output found`。工具实际执行成功，但 JSONL 事件流中结果丢失，会话可能损坏。
- 链接：https://github.com/github/copilot-cli/issues/4572

### 4. Windows：VS Code 运行时插件安装/更新失败（#4570）
- **作者**：@DDKinger | 更新：2026-08-23 | 评论：1
- **要点**：只要有 VS Code 在运行，`copilot plugin install/update` 就报 `Access is denied (os error 5)`，影响所有插件；关闭 VS Code 即恢复。疑似文件锁或权限冲突。
- 链接：https://github.com/github/copilot-cli/issues/4570

### 5. 代理反复确认但不执行工具动作（#4566）
- **作者**：@kloudkon | 更新：2026-08-23 | 评论：1 | 👍：1
- **要点**：GPT-5.3-codex 在 1.0.80 中反复

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>



</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>



</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-24

## 今日速览

昨日发布 v0.22.0-nightly.20260823 版本，包含一个 Web Shell 工作目录传递的修复。社区讨论聚焦于权限配置不生效（工具 schema 未按 allowlist 过滤）、/review 工具链的持续打磨以及安全加固（PAT 隔离、容器化执行），多个 autofix/takeover 标记的 PR 正在推进中。

## 版本发布

**v0.22.0-nightly.20260823.1007bcacfc**
- fix(web-shell): 从 overview 面板打开会话时正确传递 session workspace cwd
- 链接: https://github.com/QwenLM/qwen-code/releases

## 社区热点 Issues

挑选 10 个最值得关注的问题：

1. **【提议】新增直接外部上下文提供者配置** — #7585（评论 13）
   提议为 Qwen Code 增加私有 monorepo 集成的直连外部上下文提供者配置文件，支持按需与自动召回两种互斥模式。社区讨论热度最高，体现用户对多仓共享上下文的需求。
   https://github.com/QwenLM/qwen-code/issues/7585

2. **【Bug】流式响应 19 chunks 后无活动，120s 超时** — #5975（评论 11）
   v0.19.3 升级后频繁出现 `No stream activity for 120000ms after 19 chunks`，此前版本无此问题。影响核心编码体验，社区反馈多，标注 welcome-pr。
   https://github.com/QwenLM/qwen-code/issues/5975

3. **【Bug】Windows 终端中文输入拼音显示不清** — #8625（评论 8）
   Windows 终端中中文输入法拼音渲染模糊，影响日常使用。社区有 8 条评论，期待 UI 渲染层修复。
   https://github.com/QwenLM/qwen-code/issues/8625

4. **【安全】PAT 任务与不可信分支代码共用主机，需 runner 级隔离** — #9089（评论 7，已关闭）
   审查 PR #8961 时发现 autofix 的 PAT 承载任务与不可信代码共享主机，需 runner 级隔离。安全问题重视度高，已关闭说明已有处理方案。
   https://github.com/QwenLM/qwen-code/issues/9089

5. **【Bug】/review 预检查重叠匹配仅支持精确行，多行范围与语义重复被漏检** — #9219（评论 5）
   手动审查 PR #9204 时发现重叠检测仅按 (path, line) 精确匹配，多行 range 和语义重复的 comment 被误判为无冲突。影响 review 质量。
   https://github.com/QwenLM/qwen-code/issues/9219

6. **【Bug】permissions.allow 不限制发送给模型的工具 schema** — #9827（评论 4）
   设置 `permissions.allow` 后，实际 API 请求仍包含完整内置工具集。权限白名单形同虚设，存在安全隐患。
   https://github.com/QwenLM/qwen-code/issues/9827

7. **【Bug】Vertex AI 无法使用 ADC 认证** — #9016（评论 4，已关闭）
   Vertex AI 认证强制要求 API key，且任何 key 值都会导致 ADC 被禁用。影响 GCP 用户。
   https://github.com/QwenLM/qwen-code/issues/9016

8. **【Bug】原生斜杠命令间歇性从 Skill-tool 表面消失** — #9821（评论 3）
   `commands/*.md` 原生斜杠命令仅 50% 概率注册成功，调用报 "not found"，版本 0.21.8+ 受影响，非确定性复现。
   https://github.com/QwenLM/qwen-code/issues/9821

9. **【Bug】DaemonClient 工作区文件辅助方法在相对 base URL 下报 "Invalid URL"** — #9816（评论 2）
   #9734 修复了 `readWorkspaceFileBytes`，但同类六个方法仍使用 `new URL(...)` 绝对路径构造，Web Shell 相对路径 `/daemon` 下抛错。
   https://github.com/QwenLM/qwen-code/issues/9816

10. **【疑问】与 craft-agents-oss 的关系？界面相似且会话共享** — #9831（评论 2）
    用户质疑 Qwen Code 与 craft-agents-oss 外观几乎一致、会话互通，希望官方说明关系。社区对项目独立性较关注。
    https://github.com/QwenLM/qwen-code/issues/9831

## 重要 PR 进展

挑选 10 个值得关注的 PR：

1. **【修复】嵌套子代理审批挂起** — #9793（fix(core)）
   修复后台 Agent 或 fork 启动的嵌套子代理中的工具审批既不展示也不自动拒绝、永久挂起的问题。
   https://github.com/QwenLM/qwen-code/pull/9793

2. **【安全】review 在容器内执行被审仓库命令** — #9723
   将 review 对仓库自身命令的执行放入容器边界，由操作者显式配置策略。
   https://github.com/QwenLM/qwen-code/pull/9723

3. **【增强】延迟的 review 建议可在 PR 页外恢复** — #9761
   /review 收敛机制下移出 inline 的 Suggestion 可在审查后通过工具恢复，标记 autofix/needs-human。
   https://github.com/QwenLM/qwen-code/pull/9761

4. **【增强】per-file 内容评审结论跨 rebase 保留** — #9661
   将 per-file 评审结论打包并随 rebase 迁移，避免因 PR 栈关闭导致评审内容丢失。
   https://github.com/QwenLM/qwen-code/pull/9661

5. **【增强】覆盖率变为密封分类账本** — #9768
   /review 的 chunk 覆盖率带身份与原因说明，区分"已读取"与"已发布"的差异量。
   https://github.com/QwenLM/qwen-code/pull/9768

6. **【增强】review findings 以类型化契约上报** — #9794
   新增 `report_findings` 核心工具，/review 以结构化数据而非 Markdown 向客户端传递结果。
   https://github.com/QwenLM/qwen-code/pull/9794

7. **【集成】VS Code Companion 采用 WebShell transcript 作为默认时间线** — #9719
   VS Code 插件统一使用 WebShell 会话渲染器，取代原有 ACP 原始通知展示。
   https://github.com/QwenLM/qwen-code/pull/9719

8. **【新渠道】新增钉钉工作频道** — #9394
   内置 DingTalk Workspace 频道，支持私聊、@提及、钉钉文档通知与待办。
   https://github.com/QwenLM/qwen-code/pull/9394

9. **【修复】提供商感知的推理控制** — #9590
   为 DeepSeek V4、GLM 5.2、Kimi 等模型提供适配的 WebShell 推理控制选项。
   https://github.com/QwenLM/qwen-code/pull/9590

10. **【新功能】系统提示添加输出风格层** — #9565
    新增会话级 output style：可选用简洁、主动、解释型等风格，由模型在系统提示中执行。
    https://github.com/QwenLM/qwen-code/pull/9565

## 功能需求趋势

从昨日 Issues 与 PRs 中提炼社区关注方向：

- **外部上下文与多渠道集成**: 外部上下文提供者配置（#7585）、钉钉工作频道（#9394）、Telegram bot 完善（#5907）
- **权限与安全**: permissions.allow 真正限制 API 请求中的工具 schema（#9827）、review 的容器化执行（#9723）、PAT 任务 runner 隔离（#9089）
- **/review 工具链加固**: 重叠匹配精度（#9219）、覆盖率账本（#9768）、findings 类型化契约（#9794）、deferred suggestions 可恢复（#9761）
- **认证与云服务**: Vertex AI ADC 认证修复（#9016）
- **终端与 UI 体验**: Windows 中文输入显示（#8625）、TUI 渲染层迁移至 OpenTUI（#8662）、VP 内容底部对齐（#9305）
- **会话与后台任务管理**: 后台 Agent 恢复机制（#8586）、session 生命周期绑定 `sessionRotation`（#8927）
- **SDK 与 Web Shell 可嵌入性**: 异步提交准备（#9802）、DaemonClient 相对 URL 修复（#9816）

## 开发者关注点

- **权限配置形同虚设**: `permissions.allow` 只影响 CLI 展示，实际发往模型的仍是全量工具集（#9827），这是一个亟待修复的安全盲区
- **流式响应超时问题影响大**: v0.19.3 起频繁出现 stream 无活动 120 秒后报错，阻塞日常编码流程（#5975）
- **中文输入显示缺陷**: Windows 终端拼音渲染不清，中文用户反馈强烈（#8625）
- **认证痛点**: Vertex AI 不支持 ADC，被迫使用 API key 反而引发 401（#9016）
- **异步竞态类问题增多**: 斜杠命令注册竞态（#9821）、相对 base URL 下 DaemonClient 抛错（#9816），说明并发路径下兼容性不足
- **社区对项目独立性敏感**: 与 craft-agents-oss 高度相似引发用户质疑（#9831），官方可能需要澄清项目定位
- **Review 工具虽有迭代但仍有缺口**: 多行重复检测、跨 rebase 结论保留、异步上报等问题在持续完善中，说明 /review 已是重度使用的核心功能

</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*