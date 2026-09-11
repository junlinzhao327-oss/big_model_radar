# AI 开源趋势日报 2026-09-11

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-09-11 00:15 UTC

---

# AI 开源趋势日报 · 2026-09-11

---

## 一、今日速览

今日最强烈的信号是 **"Agent Skills" 正在成为独立的分发单元**：`i-have-adhd`（+3882）、`superpowers`（+732）、`diagram-design`（+1294）、`vercel-labs/skills` 四个"技能包"同日登榜，说明社区正围绕 Claude Code / Codex 等编码 Agent 形成插件化生态。第二条主线是 **token 成本与本地化的军备竞赛**：`llmfit` 做硬件选型、`colibri` 用纯 C 流式加载 MoE、`OmniRoute` 做 352 provider 免费网关、`caveman`/`headroom` 做上下文压缩，几乎覆盖了推理降本的全链条。第三条主线是 **记忆层替代纯向量 RAG**：`graphify`、`claude-mem`、`llm_wiki`、`PageIndex` 集体主张"无向量 / 知识图谱 / 持久记忆"，RAG 架构正在被重新定义。此外，垂直场景 Agent 开始密集落地（交易、求职、PPT、课堂）。

---

## 二、各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、CLI）

| 项目 | Stars | 为什么值得关注 |
|---|---|---|
| [vercel-labs/skills](https://github.com/vercel-labs/skills) | 今日 +122 | 官方出品的开放 Agent Skills 工具（`npx skills`），可能成为跨 Agent 技能分发的标准入口。 |
| [AlexsJones/llmfit](https://github.com/AlexsJones/llmfit) | 今日 +258 | 一条命令回答"我这台机器能跑哪个模型"，覆盖数百模型与厂商，本地部署的第一道选择题。 |
| [diegosouzapw/OmniRoute](https://github.com/diegosouzapw/OmniRoute) | 今日 +626 | 免费 MIT AI 网关，单端点接入 352 家 provider / 1200+ 模型，配额感知自动降级 + token 压缩。 |
| [JustVugg/colibri](https://github.com/JustVugg/colibri) | 今日 +98 | 纯 C、零依赖，专家权重从磁盘流式加载，在消费级硬件上跑前沿 MoE——低成本推理的代表作。 |
| [Tencent/teamai-cli](https://github.com/Tencent/teamai-cli) | 今日 +841 | "让每个团队 AI Native"的命令行工具，大厂在团队级 AI 工作流上的标准化尝试。 |
| [ollama/ollama](https://github.com/ollama/ollama) | ⭐180,596 | 本地模型运行的事实标准，已把 Kimi-K2.6、GLM-5.2、MiniMax、gpt-oss 等纳入支持。 |
| [apache/casbin-gateway](https://github.com/apache/casbin-gateway) | ⭐623 | Apache 旗下的 AI & MCP 安全网关，填补 MCP 时代的权限治理空白。 |
| [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) | ⭐8,586 | Rust 生态的模块化 LLM 应用框架，面向高并发/低开销的生产场景。 |

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 为什么值得关注 |
|---|---|---|
| [obra/superpowers](https://github.com/obra/superpowers) | 今日 +732 | Agentic Skills 框架 + 软件开发方法论，把"怎么让 Agent 干活"沉淀成可复用范式。 |
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | ⭐255,889 | Agent Harness 性能优化系统，涵盖技能、直觉、记忆、安全，跨 Claude Code / Codex / Cursor 通用。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | ⭐244,211 | "与你一同成长的 Agent"，Nous 官方智能体栈，强调持续演化而非一次性任务。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | ⭐114,081 | 让 Agent 操作浏览器的主流方案，仍是 Web 自动化 Agent 的默认选项。 |
| [JuliusBrussee/caveman](https://github.com/JuliusBrussee/caveman) | ⭐104,742 | 用"原始人语"砍掉 65% token 的 Claude Code 技能，是 token 压缩思路的爆款表达。 |
| [vastsa/PI-Desktop](https://github.com/vastsa/PI-Desktop) | 今日 +624 | Electron + Rust 本地优先编码 Agent 桌面端，支持用户自装插件，主打数据不出本机。 |
| [HKUDS/nanobot](https://github.com/HKUDS/nanobot) | ⭐47,993 | 超轻量自托管个人 Agent 框架，一个 Python 包搞定 WebUI / 记忆 / MCP / 多智能体。 |
| [esengine/DeepSeek-Reasonix](https://github.com/esengine/DeepSeek-Reasonix) | ⭐35,497 | DeepSeek 原生终端编码 Agent，围绕 prefix-cache 稳定性做工程优化，适合长时间常驻。 |

### 📦 AI 应用（具体产品、垂直场景）

| 项目 | Stars | 为什么值得关注 |
|---|---|---|
| [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd) | 今日 +3882（榜首）| 让编码 Agent 别把答案埋在废话里的技能，今日 Trending 第一，反映开发者对"输出可用性"的强烈不满。 |
| [cathrynlavery/diagram-design](https://github.com/cathrynlavery/diagram-design) | 今日 +1294 | 38 种编辑级图表类型，自包含 HTML+SVG，明确反对"Mermaid 味"的图表生成。 |
| [freestylefly/awesome-gpt-image-2](https://github.com/freestylefly/awesome-gpt-image-2) | 今日 +962 | GPT Image 2/2.5 提示词与案例库，530+ 案例、20+ 工业模板，"Prompt as Code"的工程化尝试。 |
| [THU-MAIC/OpenMAIC](https://github.com/THU-MAIC/OpenMAIC) | 今日 +837 | 清华团队的多智能体互动课堂，一键生成沉浸式多 Agent 教学体验，教育场景的标杆 Demo。 |
| [alsk1992/CloddsBot](https://github.com/alsk1992/CloddsBot) | 今日 +277 | 自主 AI 交易 Agent，横跨 Polymarket / Kalshi / Binance / 5 条 EVM 链，含机器对机器支付协议。 |
| [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | ⭐122,233 | 关键词一键生成高清短视频的自动化工作流，内容生产 Agent 的常青项目。 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | ⭐53,541 | 直接输出原生 PowerPoint（形状/动画/图表/配音），而非图片拼贴，办公自动化 Agent 的刚需方向。 |
| [career-ops-hq/career-ops](https://github.com/career-ops-hq/career-ops) | ⭐71,140 | 在本地编码 CLI 里跑完整求职流程：扫岗、评分、改简历、投递跟踪。 |

### 🧠 大模型/训练（模型权重、训练框架、微调）

| 项目 | Stars | 为什么值得关注 |
|---|---|---|
| [huggingface/transformers](https://github.com/huggingface/transformers) | ⭐165,090 | 模型定义框架的默认答案，文本/视觉/音频/多模态统一入口。 |
| [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | ⭐104,713 | 从零用 PyTorch 实现类 ChatGPT 模型，仍是理解 LLM 内部机制的最佳教学路径。 |
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | ⭐102,913 | 训练侧基础设施，无需多言。 |
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) | ⭐60,546 | 2 小时从零训出 64M 参数 LLM，小模型自训练的入门标杆。 |
| [ultralytics/ultralytics](https://github.com/ultralytics/ultralytics) | ⭐61,484 | YOLO26 / YOLO11 系列，视觉模型工程化的主力军。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | ⭐7,414 | 覆盖 100+ 数据集的 LLM 评测平台，模型选型阶段的客观标尺。 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | ⭐4,557 | 在 Apple Silicon 上手写 tiny-vLLM + Qwen，面向系统工程师理解推理栈。 |
| [ridgerchu/matmulfreellm](https://github.com/ridgerchu/matmulfreellm) | ⭐3,090 | MatMul-free LM 实现，探索抛弃矩阵乘法的替代架构。 |

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 为什么值得关注 |
|---|---|---|
| [nashsu/llm_wiki](https://github.com/nashsu/llm_wiki) | 今日 +142 | 用增量构建的持久 Wiki 替代每次从零检索的传统 RAG，知识库范式转向的代表。 |
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | ⭐116,718 | 把代码库+文档+SQL+PDF 转成可查询知识图谱，本地确定性 AST 解析，明确"不用向量库"。 |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | ⭐93,642 | 跨会话持久上下文，自动压缩并回注相关记忆，兼容 Claude Code / Codex / Copilot 等。 |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | ⭐90,465 | 融合 RAG 与 Agent 能力的上下文引擎，企业级 RAG 的成熟选项。 |
| [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom) | ⭐71,370 | 在进入 LLM 前压缩工具输出、日志与 RAG chunk，JSON 场景省 60–95% token。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | ⭐65,077 | 生产可用的 Agent 记忆层，drop-in 式接入，记忆基础设施的事实标准之一。 |
| [VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex) | ⭐35,619 | 无向量、基于推理的文档索引，直指向量检索在长文档上的语义割裂问题。 |
| [StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN) | ⭐12,933 | MLSys 2026 最佳论文，省 97% 存储在个人设备上跑完全私有 RAG。 |

---

## 三、趋势信号分析

**第一，Agent 的竞争焦点从"模型能力"转向"技能与脚手架"。** 今日 Trending 前四名中有三个是给编码 Agent 加装能力的技能包（`i-have-adhd`、`diagram-design`、`superpowers`），加上 Vercel 官方的 `npx skills`，一个类似 npm 的 Agent 技能分发层正在成形——谁能定义技能规范，谁就掌握下一代开发者入口。

**第二，token 经济学成为独立赛道。** 压缩（caveman、headroom）、路由（OmniRoute、LLM-API-Key-Proxy）、硬件适配（llmfit、colibri）、前缀缓存优化（DeepSeek-Reasonix）同日出现，说明当模型能力趋于同质，**单位任务成本**成了工程竞争的主战场。

**第三，RAG 正在"去向量化"。** graphify、PageIndex、llm_wiki 均明确以知识图谱或推理式索引替代向量检索，配合 claude-mem / mem0 的持久记忆层，行业正从"检索片段"走向"维护一份持续演化的知识状态"。这与近期 GLM-5.2、Kimi-K2.6、MiniMax、gpt-oss 等长上下文模型密集发布直接相关：上下文变长后，如何**组织**上下文比如何**检索**它更关键。

---

## 四、社区关注热点

- **Agent Skills 规范之争（vercel-labs/skills vs obra/superpowers）**：一方是平台方的轻量分发工具，一方是重型方法论框架，短期内会并存，但技能格式的标准化窗口已经打开，值得提前押注。
- **上下文压缩中间件（headroom / caveman）**：不改模型、不改业务代码就能省 20–95% token，是所有 Agent 团队能立刻落地的 ROI 项目。
- **持久记忆层（claude-mem / mem0 / cognee）**：跨会话记忆是当前 Agent 体验最大的断点，也是从"玩具"走向"日常工具"的关键，建议在自建 Agent 时优先评估。
- **本地低门槛推理（colibri / llmfit / LEANN）**：纯 C 跑 MoE、97% 存储节省的私有 RAG，说明"消费级硬件跑前沿模型"已从口号进入工程实践，隐私敏感场景值得重点关注。
- **垂直 Agent 的赚钱样本（CloddsBot / career-ops / ppt-master）**：交易、求职、PPT 三个高价值场景同日活跃，验证了"Agent + 具体工作流 + 可衡量产出"比通用助手更容易获得真实用户。

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*