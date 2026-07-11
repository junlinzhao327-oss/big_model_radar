# AI 开源趋势日报 2026-07-12

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-11 22:35 UTC

---

# AI 开源趋势日报 2026-07-12

## 今日速览

今日 GitHub Trending 榜单中，AI 相关项目占 7/24，其中 **DesktopCommanderMCP**（+900 stars）和 **superpowers**（+737 stars）表现最为突出，展现出社区对 Agent 终端控制与技能框架的强烈兴趣。主题搜索方面，RAG 与 AI Agent 依旧是绝对热点，langgenius/dify、open-webui、langchain 等头部项目 star 数持续攀升，同时向量数据库（Milvus、Qdrant）和记忆层（mem0、cognee）等基础设施不断完善。值得注意的是，**Claude 生态**（claude-code-templates、claude-cookbooks、stitch-skills）在今日热榜中集中出现，预示 MCP（Model Context Protocol）标准化正在加速。

## 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

- **ollama/ollama** ⭐175,936  
  本地运行大模型的命令行工具，现已支持 Kimi、GLM、DeepSeek 等新模型，是 AI 开发者的标配推理引擎。  
  https://github.com/ollama/ollama

- **vllm-project/vllm** ⭐85,988  
  高吞吐、低延迟的 LLM 推理与服务引擎，适配多模型，生产级部署首选。  
  https://github.com/vllm-project/vllm

- **huggingface/transformers** ⭐162,503  
  模型定义与微调框架，支持文本、视觉、音频等多模态模型，保持绝对领先。  
  https://github.com/huggingface/transformers

- **firecrawl/firecrawl** ⭐149,354  
  面向 AI Agent 的网页抓取与交互 API，支持大规模数据获取，是 RAG 和 Agent 的数据入口。  
  https://github.com/firecrawl/firecrawl

- **davila7/claude-code-templates** ⭐0 (+230 today)  
  Claude Code 的配置与监控 CLI 工具，简化开发者对 Claude 编码环境的自动化管理。  
  https://github.com/davila7/claude-code-templates

- **openai/plugins** ⭐0 (+75 today)  
  OpenAI 官方插件库，为 ChatGPT 等应用扩展能力，虽增速放缓但仍是生态参考标杆。  
  https://github.com/openai/plugins

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

- **langgenius/dify** ⭐148,520  
  生产级 Agentic 工作流开发平台，可视化编排 + 内置 RAG 与工具调用，企业首选。  
  https://github.com/langgenius/dify

- **langchain-ai/langchain** ⭐141,545  
  代理工程平台，提供统一接口构建复杂 Agent 应用，生态最广。  
  https://github.com/langchain-ai/langchain

- **FlowiseAI/Flowise** ⭐54,536  
  低代码 AI Agent 构建工具，拖拽式设计，适合快速原型开发。  
  https://github.com/FlowiseAI/Flowise

- **wonderwhy-er/DesktopCommanderMCP** ⭐0 (+900 today)  
  为 Claude 提供终端控制、文件搜索和差异编辑能力的 MCP 服务器，今日新增最高，Agent 实操性工具。  
  https://github.com/wonderwhy-er/DesktopCommanderMCP

- **obra/superpowers** ⭐0 (+737 today)  
  Agent 技能框架与软件开发方法论，主张通过结构化技能定义提升 Agent 生产力，社区热议。  
  https://github.com/obra/superpowers

- **google-labs-code/stitch-skills** ⭐0 (+338 today)  
  Stitch MCP 服务器的 Agent 技能库，遵循开放标准，兼容 Claude Code、Gemini CLI 等多 Agent。  
  https://github.com/google-labs-code/stitch-skills

- **Significant-Gravitas/AutoGPT** ⭐185,478  
  自主 AI Agent 先驱项目，持续迭代任务规划与执行能力。  
  https://github.com/Significant-Gravitas/AutoGPT

### 📦 AI 应用（具体应用产品、垂直场景解决方案）

- **open-webui/open-webui** ⭐145,085  
  用户友好的 AI 交互界面，支持 Ollama、OpenAI API，本地部署首选。  
  https://github.com/open-webui/open-webui

- **Mintplex-Labs/anything-llm** ⭐63,128  
  本地优先的全能 AI Agent 应用，内置文档管理、Agent 技能、知识库。  
  https://github.com/Mintplex-Labs/anything-llm

- **CherryHQ/cherry-studio** ⭐48,452  
  多功能 AI 生产力工作室，集成智能对话、自主 Agent 和 300+ 助手。  
  https://github.com/CherryHQ/cherry-studio

- **DayuanJiang/next-ai-draw-io** ⭐0 (+74 today)  
  基于 Next.js 的 AI 辅助绘图应用，通过自然语言命令创建和修改 draw.io 图表，新颖应用场景。  
  https://github.com/DayuanJiang/next-ai-draw-io

- **anthropics/claude-cookbooks** ⭐0 (+322 today)  
  Claude 官方使用教程集合（Jupyter Notebook），展示创意用法，适合开发者学习。  
  https://github.com/anthropics/claude-cookbooks

- **TauricResearch/TradingAgents** ⭐92,360  
  多 Agent 金融交易框架，结合 LLM 进行市场分析与策略执行，垂直领域标杆。  
  https://github.com/TauricResearch/TradingAgents

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

- **pytorch/pytorch** ⭐101,752  
  动态神经网络框架，GPU 加速训练，深度学习基础库。  
  https://github.com/pytorch/pytorch

- **tensorflow/tensorflow** ⭐196,297  
  端到端机器学习框架，覆盖训练到部署全流程。  
  https://github.com/tensorflow/tensorflow

- **ultralytics/ultralytics** ⭐59,357  
  YOLO 系列目标检测训练框架，支持分类、分割、姿态估计，边缘部署友好。  
  https://github.com/ultralytics/ultralytics

- **rasbt/LLMs-from-scratch** ⭐98,932  
  从零实现 ChatGPT 类 LLM 的教程与代码，最佳学习资源之一。  
  https://github.com/rasbt/LLMs-from-scratch

- **open-compass/opencompass** ⭐7,184  
  大模型评测平台，覆盖 100+ 数据集，评估工具标准化。  
  https://github.com/open-compass/opencompass

- **galilai-group/stable-pretraining** ⭐283  
  可靠、最小化的基础模型预训练库，面向研究者，今日关注度提升。  
  https://github.com/galilai-group/stable-pretraining

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

- **infiniflow/ragflow** ⭐84,827  
  顶级开源 RAG 引擎，融合 Agent 能力，提供上下文层简化 LLM 接入。  
  https://github.com/infiniflow/ragflow

- **milvus-io/milvus** ⭐45,197  
  高性能云原生向量数据库，支持大规模 ANN 搜索，RAG 基础设施。  
  https://github.com/milvus-io/milvus

- **qdrant/qdrant** ⭐33,160  
  高性能向量搜索引擎，支持边缘与云，适用于生成式 AI 应用。  
  https://github.com/qdrant/qdrant

- **mem0ai/mem0** ⭐60,624  
  通用 AI Agent 记忆层，为会话提供持久化上下文，替代复杂 RAG 管道。  
  https://github.com/mem0ai/mem0

- **weaviate/weaviate** ⭐16,572  
  对象与向量混合存储数据库，支持结构化过滤与向量搜索，多云部署。  
  https://github.com/weaviate/weaviate

- **lancedb/lancedb** ⭐10,866  
  嵌入式多模态检索库，开发者友好的轻量级 RAG 方案。  
  https://github.com/lancedb/lancedb

- **tesseract-ocr/tesseract** ⭐75,248  
  经典 OCR 引擎，虽非 RAG 核心但常与知识提取流程集成。  
  https://github.com/tesseract-ocr/tesseract

## 趋势信号分析

今日热榜中最显著的信号是 **MCP 生态的爆发**：`DesktopCommanderMCP` 和 `stitch-skills` 均围绕 Model Context Protocol 构建，分别提供终端控制和标准化技能库，单日新增合计超 1200 stars。这表明社区正在从“调 API”转向“让 Agent 真正操作电脑”——Agent 的“手脚”（终端、文件系统、浏览器）成为刚需。与此同时，`superpowers` 提出的“技能框架+方法论”代表了一种系统化提升 Agent 可靠性的方向，可能推动 Agent 开发从玩具走向工程。

另一趋势是 **Claude 生态的强化**：`claude-code-templates`、`claude-cookbooks` 以及 `antigravity`（Gemini CLI）的并入，显示出多平台兼容性（Stitch、OpenCode 等）正被重视。与此对应，`openai/plugins` 虽增速放缓，但仍是标准竞争者。整体来看，**Agent 的可操作性**（终端、文件、浏览器控制）是今日最火的方向，预计未来一周将有更多类似 MCP 服务器涌现。

**新兴技术栈方面**：`mem0`（记忆层）和 `cognee`（知识图谱记忆）等“持久化上下文”项目热度持续，标志着长程 Agent 记忆从理论走向实用。此外，向量数据库赛道虽成熟，但 `VectifyAI/PageIndex` 提出的“无向量 RAG”模式值得关注。

## 社区关注热点

- **DesktopCommanderMCP** — 目前最热门的 MCP 服务端，让 Claude 能直接执行 shell 命令、搜索文件并 diff 编辑，适合开发自动化与运维场景。  
  https://github.com/wonderwhy-er/DesktopCommanderMCP

- **superpowers** — 提出 Agent 开发方法论与技能框架，强调“结构优于 prompt”，适合团队构建标准化 Agent 开发流程。  
  https://github.com/obra/superpowers

- **claude-cookbooks** — 官方教程集，包含多种创造性用法（如多轮对话、工具调用），快速上手 Claude 新特性。  
  https://github.com/anthropics/claude-cookbooks

- **mem0** — 通用记忆层，让 Agent 跨会话保持用户偏好与历史记忆，解决 RAG 片段丢失问题。  
  https://github.com/mem0ai/mem0

- **stitch-skills** — 开放标准 Agent 技能库，可同时适配 Claude Code、Gemini CLI、Cursor 等，生态兼容性值得跟进。  
  https://github.com/google-labs-code/stitch-skills

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*