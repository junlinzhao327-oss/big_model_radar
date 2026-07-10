# AI 开源趋势日报 2026-07-11

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-10 23:17 UTC

---

# 📊 AI 开源趋势日报 | 2026-07-11

---

## 1. 今日速览

- **Agent Skills 生态大爆发**：`addyosmani/agent-skills`、`mattpocock/skills`、`obra/superpowers` 三个技能库项目同时冲上 Trending 榜，合计今日斩获超 3,700 stars，标志着“AI 编码 agent 技能”正向标准化、工业化迈进。
- **MCP 协议持续渗透**：`DesktopCommanderMCP` 为 Claude 提供终端控制，`stitch-skills` 推出兼容 MCP 的技能库，腾讯云 `TencentDB-Agent-Memory` 则用本地 4 级流水线实现 Agent 长期记忆，大厂与社区合力填充 MCP 生态。
- **AI 办公自动化新星**：`iOfficeAI/OfficeCLI` 今日新增 1,210 stars，专为 AI 代理读写 Office 文件而生，单二进制、无需 Office 安装，直接对标传统办公软件。
- **多智能体金融交易框架**：`TauricResearch/TradingAgents` 以 9.2 万 stars 成为 RAG 主题下的黑马，LLM 驱动的多智能体量化交易系统获得社区高度认可。
- **向量数据库与记忆层竞争白热化**：`mem0`、`cognee`、`memvid` 等轻量级记忆层项目崛起，与 `milvus`、`qdrant` 等传统向量 DB 形成差异化竞争。

---

## 2. 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、CLI）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [ollama/ollama](https://github.com/ollama/ollama) | 175,891 | 本地运行大模型的一站式工具，现已支持 Kimi、GLM、DeepSeek 等最新模型。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 85,928 | 高吞吐、低延迟的 LLM 推理引擎，生产级部署首选。 |
| [wonderwhy-er/DesktopCommanderMCP](https://github.com/wonderwhy-er/DesktopCommanderMCP) | 0 (+349 today) | 为 Claude 提供终端控制、文件搜索和 diff 编辑能力的 MCP 服务器，今日新星。 |
| [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | 0 (+1,114 today) | 生产级工程技能库，为 AI 编码 agent 注入真实开发经验，今日爆火。 |
| [mattpocock/skills](https://github.com/mattpocock/skills) | 0 (+1,663 today) | 直接从 `.claude` 目录提取的实战技能，社区贡献量极高。 |
| [obra/superpowers](https://github.com/obra/superpowers) | 0 (+969 today) | 一套 agentic skills 框架+软件开发方法论，强调可复用的 agent 技能。 |
| [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills) | 0 (+101 today) | Google 实验室出品，兼容 MCP 服务器的标准化 Agent Skills 库。 |
| [TencentCloud/TencentDB-Agent-Memory](https://github.com/TencentCloud/TencentDB-Agent-Memory) | 0 (+134 today) | 腾讯云推出的本地长期记忆方案，4 级渐进式管道，零外部 API 依赖。 |

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 185,452 | 经典自主 agent 框架，愿景是“人人可用的 AI”。 |
| [langgenius/dify](https://github.com/langgenius/dify) | 148,434 | 生产级 agentic 工作流开发平台，支持可视化编排。 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | 141,483 | Agent 工程的核心框架，生态最成熟。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 104,129 | 让 AI agent 像人一样操作浏览器，自动化在线任务。 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | 80,370 | AI 驱动的软件开发 agent，可自动修复代码、提交 PR。 |
| [FlowiseAI/Flowise](https://github.com/FlowiseAI/Flowise) | 54,506 | 可视化拖拽构建 AI Agent 和 RAG 流程，零代码友好。 |
| [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit) | 35,910 | 前端 Agent 与生成式 UI 栈，支持 React、Angular、移动端等。 |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | 92,220 | 多智能体 LLM 金融交易框架，近期社区热捧。 |

### 📦 AI 应用（具体产品、垂直场景解决方案）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [iOfficeAI/OfficeCLI](https://github.com/iOfficeAI/OfficeCLI) | 0 (+1,210 today) | 专为 AI agent 设计的 Office 读写工具，单二进制、无需安装 Office。 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 48,417 | AI 生产力工作室，集成智能对话、自主 agent 和 300+ 预设助手。 |
| [ScrapeGraphAI/Scrapegraph-ai](https://github.com/ScrapeGraphAI/Scrapegraph-ai) | 28,251 | AI 驱动的网页爬虫，用自然语言指定抓取规则。 |
| [deepfakes/faceswap](https://github.com/deepfakes/faceswap) | 55,336 | 经典深度学习换脸应用，长期活跃。 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | 38,235 | AI 从文档自动生成可编辑 PPT，支持原生形状、动画、图表。 |
| [netdata/netdata](https://github.com/netdata/netdata) | 79,586 | AI 加持的全栈可观测性平台，可自动检测异常。 |
| [tesseract-ocr/tesseract](https://github.com/tesseract-ocr/tesseract) | 75,234 | 开源 OCR 引擎，被大量 AI 应用集成。 |

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [huggingface/transformers](https://github.com/huggingface/transformers) | 162,457 | 模型定义与训练的 Hugging Face 生态核心库。 |
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | 101,719 | 深度学习框架，AI 研究基石。 |
| [tensorflow/tensorflow](https://github.com/tensorflow/tensorflow) | 196,276 | 谷歌开源机器学习框架，依然广泛使用。 |
| [ultralytics/ultralytics](https://github.com/ultralytics/ultralytics) | 59,332 | YOLO 系列最新版，目标检测/分割/分类一站式。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 212,749 | 能持续学习的 agent（含模型能力），社区星数惊人。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,184 | 100+ 数据集上评估 LLM，支持主流模型。 |

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 84,777 | 领先的开源 RAG 引擎，融合 Agent 能力与上下文层。 |
| [Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm) | 63,080 | 本地优先的 RAG + Agent 体验，支持多种 LLM。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 60,569 | 通用记忆层，让 AI Agent 跨会话记住用户偏好。 |
| [run-llama/llama_index](https://github.com/run-llama/llama_index) | 50,773 | 文档 agent 和 OCR 平台，RAG 领域的明星。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 45,176 | 高性能云原生向量数据库，大规模 ANN 搜索。 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | 33,137 | 极速向量数据库，支持云服务。 |
| [topoteretes/cognee](https://github.com/topoteretes/cognee) | 27,551 | 开源 AI 记忆平台，用知识图谱实现持久长期记忆。 |
| [memvid/memvid](https://github.com/memvid/memvid) | 15,739 | 无服务器单文件记忆层，替代复杂 RAG 管道。 |

---

## 3. 趋势信号分析

- **“Agent Skills” 品类异军突起**：今日三大技能库项目（`mattpocock/skills`、`addyosmani/agent-skills`、`obra/superpowers`）合计新增超 3,700 stars，表明社区已经从“构建 agent”转向“为 agent 提供高质量技能”。技能标准化（如 `stitch-skills` 遵循 Agent Skills 开放标准）正在成为新的技术栈层。
- **MCP 协议成为 Agent 工具互联的默认接口**：`DesktopCommanderMCP`（终端控制）、`TencentDB-Agent-Memory`（记忆）、`stitch-skills`（技能库）均基于 MCP，大厂（腾讯、Google）与独立开发者一致拥抱该协议，未来 agent 的“工具生态”将围绕 MCP 组装。
- **AI 办公自动化赛道涌现新玩家**：`OfficeCLI` 今日新增 1,210 stars，直接挑战传统 Office 自动化方案；`ppt-master` 也已积累 38k stars。这印证了“AI agent 需要原生能力操作办公文档”的刚需，也预示着低代码/无代码平台与 AI agent 的融合趋势。
- **长期记忆（Memory Layer）成为 Agent 基础设施标配**：从 `mem0`（60k stars）到 `TencentDB-Agent-Memory`，再到 `memvid`、`cognee`，记忆层项目密集出现。社区不再满足于单次对话，而是追求跨会话、跨工具的持久上下文，这一方向可能成为 2026 年 AI 基础设施的关键增长点。
- **多智能体金融量化框架获得高关注**：`TauricResearch/TradingAgents` 以 92k stars 位居 RAG 主题榜前列，说明 LLM 在垂直金融领域的应用（如量化交易、市场分析）正从概念走向工程化实践。

---

## 4. 社区关注热点

- 🔥 **`mattpocock/skills`** – 今日新增 stars 最多的项目（+1,663），直接公开了作者在 `~/.claude` 中积累的实战技能，是学习如何为 Claude Code 编写高质量技能的极佳参考。
- ⚡ **`iOfficeAI/OfficeCLI`** – AI agent 读写 Office 文件的利器，免费开源、单二进制、无需安装 Office，非常适合自动化办公场景。
- 🧩 **`google-labs-code/stitch-skills`** – Google 官方出品的 Agent Skills 库，兼容 MCP 服务器，标准化程度高，预示未来 agent 技能将像 npm 包一样可复用。
- 💾 **`TencentCloud/TencentDB-Agent-Memory`** – 腾讯云开源，4 级渐进式流水线实现本地长期记忆，零外部 API 依赖，对隐私敏感的应用场景极具吸引力。
- 🚀 **`TauricResearch/TradingAgents`** – 多智能体 LLM 金融交易框架，社区认可度极高，可关注其架构如何协调多个 agent 进行市场分析、策略执行。

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*