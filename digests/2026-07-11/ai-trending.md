# AI 开源趋势日报 2026-07-11

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-10 22:36 UTC

---

# AI 开源趋势日报 · 2026-07-11

## 一、今日速览

今日 GitHub AI 开源生态呈现三大热点：**Agent Skills 标准** 成为社区爆发点，`addyosmani/agent-skills`、`mattpocock/skills`、`obra/superpowers` 三个项目同时冲上 Trending，合计新增近 3,700 stars，标志着“AI 编程代理技能文件”正在形成事实标准。**AI Agent 的持久记忆层** 继续获得关注，腾讯开源的 `TencentDB-Agent-Memory` 以 4 级渐进式流水线提供全本地长时记忆，新增 134 stars。**专为 AI 代理设计的办公套件** `iOfficeAI/OfficeCLI` 单日新增 1,210 stars，显示垂直场景 Agent 工具需求旺盛。此外，主题搜索中大量 AI Agent 类项目（如 hermes-agent、career-ops、Agent-Reach）均以数十万 star 成为社区中坚力量，RAG 与向量数据库生态持续繁荣，`llama_index`、`ragflow`、`mem0` 等项目保持高热度。

---

## 二、各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、CLI）

| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|-----------|
| [ollama/ollama](https://github.com/ollama/ollama) | ⭐175,889 | 本地运行新一代开源模型（Kimi、GLM、DeepSeek等）的一站式 CLI 工具，LLM 入门必选。 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | ⭐162,457 | 业界标准模型框架，支持文本、视觉、音频、多模态模型的推理与训练。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | ⭐85,926 | 高吞吐、低内存的 LLM 推理引擎，生产级部署首选。 |
| [TencentCloud/TencentDB-Agent-Memory](https://github.com/TencentCloud/TencentDB-Agent-Memory) | ⭐0 (+134 today) | 全本地、零外部依赖的 AI Agent 长时记忆层，4 级渐进式流水线设计。 |
| [davila7/claude-code-templates](https://github.com/davila7/claude-code-templates) | ⭐0 (+104 today) | 为 Claude Code 提供配置与监控的 CLI，降低 Agent 使用门槛。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | ⭐7,184 | 覆盖 100+ 数据集的大模型评估平台，支持 Llama3、Mistral、Qwen 等。 |
| [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) | ⭐7,886 | Rust 生态的模块化 LLM 应用框架，支持可扩展的 Agent 构建。 |

### 🤖 AI 智能体 / 工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|-----------|
| [langgenius/dify](https://github.com/langgenius/dify) | ⭐148,432 | 生产级 Agent 工作流开发平台，支持可视化编排与多模型接入。 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | ⭐80,365 | AI 驱动软件开发助手，可自主完成编码、测试、部署任务。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | ⭐104,129 | 让 AI Agent 像人类一样操控浏览器，实现网页自动化。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | ⭐212,735 | “与你一起成长的智能体”，强调长期记忆与自适应能力。 |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | ⭐92,217 | 多 Agent 金融交易框架，集成 LLM 进行市场分析与决策。 |
| [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | ⭐0 (+1,114 today) | 为 AI 编程代理提供的生产级工程技能集合，今日 Trending 榜首。 |
| [obra/superpowers](https://github.com/obra/superpowers) | ⭐0 (+969 today) | Agentic Skills 框架与软件开发方法论，与 Claude Code 深度集成。 |
| [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills) | ⭐0 (+101 today) | Google 推出的 Agent Skills 库，兼容 Stitch MCP 与多款 coding agent。 |

### 📦 AI 应用（具体应用产品、垂直场景）

| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|-----------|
| [iOfficeAI/OfficeCLI](https://github.com/iOfficeAI/OfficeCLI) | ⭐0 (+1,210 today) | 专为 AI Agent 设计的 Office 套件（Word/Excel/PPT），单二进制、无需安装。 |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | ⭐148,891 | 可扩展的网页抓取与交互 API，为 LLM 提供实时网页数据。 |
| [santifer/career-ops](https://github.com/santifer/career-ops) | ⭐59,549 | 开源 AI 求职助手：扫描职位、评分、定制简历，本地运行。 |
| [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) | ⭐54,442 | 让 AI Agent 访问全互联网（Twitter、Reddit、B站等），零 API 费用。 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | ⭐48,417 | AI 生产力工作室，集成智能聊天、自主代理与 300+ 助手模板。 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | ⭐38,233 | 从任意文档自动生成可编辑的 PowerPoint，支持原生动画与图表。 |
| [asgeirtj/system_prompts_leaks](https://github.com/asgeirtj/system_prompts_leaks) | ⭐55,798 | 收集并更新主流模型（Claude、GPT、Gemini 等）的系统提示词，逆向工程最佳实践。 |

### 🧠 大模型 / 训练（模型权重、训练框架、微调工具）

| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|-----------|
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | ⭐283 | 可靠、简洁、可扩展的基础模型预训练库，支持世界模型。 |
| [testtimescaling/testtimescaling.github.io](https://github.com/testtimescaling/testtimescaling.github.io) | ⭐107 | 关于大模型测试时扩展（test-time scaling）的综述与资源仓库。 |
| [chrisliu298/awesome-llm-unlearning](https://github.com/chrisliu298/awesome-llm-unlearning) | ⭐608 | 大模型机器遗忘的研究资源汇总，帮助开发者实现模型“忘记”特定知识。 |
| [liguge/Awesome-large-language-model-for-PHM](https://github.com/liguge/Awesome-large-language-model-for-Prognostics-and-health-management) | ⭐125 | 将 LLM 应用于预测性维护与故障诊断的论文与工具集合。 |

### 🔍 RAG / 知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars（今日新增） | 一句话说明 |
|------|-------------------|-----------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | ⭐84,777 | 领先的开源 RAG 引擎，融合 Agent 能力，为 LLM 提供高质上下文层。 |
| [run-llama/llama_index](https://github.com/run-llama/llama_index) | ⭐50,773 | 文档解析与 OCR 领域的语义索引框架，支撑多模态 RAG。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | ⭐60,568 | 面向 AI Agent 的通用记忆层，实现跨会话持久化。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | ⭐45,176 | 高性能云原生向量数据库，支撑大规模 ANN 搜索。 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | ⭐33,136 | 下一代 AI 的高性能向量搜索引擎，提供云端服务。 |
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | ⭐81,913 | 将代码、SQL、文档、图像等转化为可查询的知识图谱，支持多种 coding agent。 |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | ⭐86,764 | 跨会话上下文持久化工具，自动压缩并注入相关历史给 Agent。 |
| [meilisearch/meilisearch](https://github.com/meilisearch/meilisearch) | ⭐58,488 | AI 驱动的混合搜索引擎，为网站和应用提供闪电级搜索。 |

---

## 三、趋势信号分析

**1. “Agent Skills” 标准正在成为新基建**  
今日 Trending 榜单上，三个与 Agent Skills 直接相关的项目（`agent-skills`、`skills`、`superpowers`）合计新增超过 3,700 stars，同时 Google 推出 `stitch-skills`，表明业界正围绕“AI 编程代理可复用的技能文件”形成共识。这类项目提供结构化指令（如 .claude 目录），使 Agent 能快速掌握特定工程实践（测试、日志、安全等）。这类似于早期的“插件生态”，但更轻量、更贴近 Agent 交互范式。

**2. 垂直场景 Agent 工具爆发**  
`OfficeCLI` 的 1,210 单日 stars 表明，AI 代理不再满足于通用编程，开始冲击商业办公软件。类似地，`career-ops`（求职）、`ppt-master`（演示文稿）、`daily_stock_analysis`（股票分析）等项目均获得数万 stars，显示开发者正在快速填充“Agent + 具体行业”的空白。

**3. 记忆与上下文工程成为关键**  
`TencentDB-Agent-Memory`、`mem0`、`claude-mem`、`cognee`、`memvid` 等项目密集涌现，说明社区已意识到当前 Agent 的“无状态”短板。长时记忆、知识图谱、上下文压缩等技术正从实验走向实用，并开始出现“记忆即服务”的轻量方案。

**4. 多 Agent 协作从概念走向实践**  
`TradingAgents`（多 Agent 金融交易）、`DATAGEN`（多 Agent 研究助手）、`hermes-agent`（自适应增长）等项目的 star 数快速攀升，表明单一 Agent 的能力天花板正被多 Agent 协作突破。Agent 通信、任务编排、角色分配等方向将迎来更多创新。

---

## 四、社区关注热点

- **⭐ Agent Skills 生态**：关注 `addyosmani/agent-skills` 和 `obra/superpowers`，它们可能成为类似 VSCode 扩展市场的 Agent 技能分发平台。建议开发者尝试将自己的最佳实践封装为 .claude 技能文件。
- **🛠️ 全本地 Office Agent**：`iOfficeAI/OfficeCLI` 是首个完全脱离 OA 系统的 Agent 办公方案，单二进制、零依赖，适合集成到 CI/CD 或 Agent 工作流中。
- **🧠 持久记忆层选型**：`TencentDB-Agent-Memory`（4 级流水线）与 `mem0`（通用 API）分别代表企业级和轻量级两条路径，值得对比测试。
- **🔗 知识图谱型 RAG**：`Graphify-Labs/graphify` 将文件夹代码、文档、图像转化为可查询知识图谱，解决了传统 RAG 的碎片化问题，且适配多种 coding agent。
- **📈 金融多 Agent**：`TauricResearch/TradingAgents` 在 LLM 金融决策领域 star 数极高，其开源的多 Agent 协作模式可复用到其他复杂决策场景（如供应链、医疗诊断）。

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*