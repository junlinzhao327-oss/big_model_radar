# AI 开源趋势日报 2026-07-10

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-09 22:35 UTC

---

# AI 开源趋势日报（2026-07-10）

---

## 今日速览

- **AI Agent 生态爆发**：围绕 Claude Code 的 MCP 服务器、技能库和办公 CLI 工具集中登榜，`ai-job-search` 单日暴涨 3728 stars，成为今日最大黑马。
- **办公自动化与求职赛道崛起**：`OfficeCLI`（+1923 stars）专为 AI 代理打造 Office 套件，`ai-job-search` 实现全流程求职自动化，垂直场景应用进入加速期。
- **轻量本地模型受追捧**：`pocket-tts`（+273 stars）在 CPU 上运行的 TTS 模型和 `DesktopCommanderMCP`（+185 stars）的终端控制工具，体现了“小而美”的本地化趋势。
- **AI 系统透明度需求高涨**：`system_prompts_leaks` 已获 55k+ stars，持续收集各家大模型系统提示词，反映社区对模型行为透明度的强烈关注。
- **RAG 与向量生态持续壮大**：`ragflow`、`mem0`、`graphify` 等项目均在 7 天内获得高活跃度，知识管理与检索增强仍是 AI 基础设施的核心方向。

---

## 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐85,835  
  高吞吐、内存高效的 LLM 推理引擎，支撑大量生产级部署。

- **[ollama/ollama](https://github.com/ollama/ollama)** ⭐175,821  
  本地运行大模型的终极工具，支持 Kimi、DeepSeek、Qwen 等主流模型。

- **[unclecode/crawl4ai](https://github.com/unclecode/crawl4ai)** ⭐0（今日 +195）  
  LLM 友好的开源网页爬虫与抓取工具，专为 RAG 和 Agent 数据采集设计。

- **[kyutai-labs/pocket-tts](https://github.com/kyutai-labs/pocket-tts)** ⭐0（今日 +273）  
  轻量级 TTS 模型，可在普通 CPU 上实时运行，适合本地语音合成应用。

- **[wonderwhy-er/DesktopCommanderMCP](https://github.com/wonderwhy-er/DesktopCommanderMCP)** ⭐0（今日 +185）  
  为 Claude 提供的 MCP 服务器，赋予其终端控制、文件搜索和差异编辑能力。

- **[open-webui/open-webui](https://github.com/open-webui/open-webui)** ⭐144,865  
  用户友好的 AI 界面，支持 Ollama、OpenAI API，快速搭建个人 AI 工作台。

- **[firecrawl/firecrawl](https://github.com/firecrawl/firecrawl)** ⭐148,400  
  大规模网页搜索、抓取与交互 API，是 LLM 获取网络数据的基础设施。

---

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** ⭐185,445  
  最知名的自主 Agent 项目，近期持续迭代，使命是让 AI 人人可用。

- **[OpenHands/OpenHands](https://github.com/OpenHands/OpenHands)** ⭐80,237  
  AI 驱动的软件开发助手，可自主完成编码、调试、部署等任务。

- **[vxcontrol/pentagi](https://github.com/vxcontrol/pentagi)** ⭐0（今日 +543）  
  全自主 AI Agent 系统，能够执行复杂的渗透测试任务，安全领域 Agent 新星。

- **[addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)** ⭐0（今日 +2,582）  
  生产级工程技能库，为 AI 编码代理提供专业能力，今日涨幅惊人。

- **[langchain-ai/langchain](https://github.com/langchain-ai/langchain)** ⭐141,405  
  Agent 工程平台，提供构建 LLM 应用的统一框架和工具链。

- **[browser-use/browser-use](https://github.com/browser-use/browser-use)** ⭐103,967  
  让 AI 代理像人类一样操作浏览器，自动化 Web 任务。

- **[langgenius/dify](https://github.com/langgenius/dify)** ⭐148,327  
  生产级 Agentic 工作流开发平台，可视化编排 AI 应用。

---

### 📦 AI 应用（具体产品、垂直场景解决方案）

- **[MadsLorentzen/ai-job-search](https://github.com/MadsLorentzen/ai-job-search)** ⭐0（今日 +3,728）  
  基于 Claude Code 的 AI 求职框架，自动评估岗位、优化简历、准备面试——今日最热项目。

- **[iOfficeAI/OfficeCLI](https://github.com/iOfficeAI/OfficeCLI)** ⭐0（今日 +1,923）  
  专为 AI 代理设计的 Office 命令行套件，无需安装 Office 即可读写 Word/Excel/PPT。

- **[bradautomates/claude-video](https://github.com/bradautomates/claude-video)** ⭐0（今日 +727）  
  让 Claude 能“看”视频：下载、抽帧、转录，全交给 Claude 分析。

- **[TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents)** ⭐92,047  
  多智能体 LLM 金融交易框架，用 AI 代理执行量化策略。

- **[santifer/career-ops](https://github.com/santifer/career-ops)** ⭐59,359  
  开源 AI 求职工具：扫描职位、评分、定制简历，本地运行于 AI 编码 CLI。

- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐48,369  
  AI 生产力工作室，集成智能对话、自主代理和 300+ 预置助手。

- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** ⭐38,014  
  从文档一键生成可编辑的 PowerPoint，支持动画、图表和语音旁白。

---

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

- **[huggingface/transformers](https://github.com/huggingface/transformers)** ⭐162,418  
  🤗 Transformers 系列，涵盖文本、视觉、音频等多模态模型，是模型生态核心。

- **[ultralytics/ultralytics](https://github.com/ultralytics/ultralytics)** ⭐59,298  
  YOLO26/YOLO11 系列目标检测模型，持续迭代最新的视觉 AI 方案。

- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** ⭐281  
  可靠、最小化、可扩展的基础模型预训练库，专注世界模型训练。

- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** ⭐7,180  
  LLM 评估平台，支持 100+ 数据集和主流模型，是模型评测的标配工具。

- **[starpig1129/DATAGEN](https://github.com/starpig1129/DATAGEN)** ⭐1,766  
  AI 驱动的多智能体研究助手，自动生成假设、分析数据、撰写报告。

- **[acon96/home-llm](https://github.com/acon96/home-llm)** ⭐1,375  
  将本地 LLM 集成到 Home Assistant，实现智能家居的本地化语音控制。

---

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐84,699  
  领先的 RAG 引擎，融合 Agent 能力，为 LLM 提供高质量上下文层。

- **[run-llama/llama_index](https://github.com/run-llama/llama_index)** ⭐50,751  
  文档代理与 OCR 平台，LlamaIndex 是 RAG 项目的事实标准之一。

- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** ⭐45,154  
  高性能云原生向量数据库，支持大规模 ANN 搜索。

- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** ⭐60,493  
  通用 AI 代理记忆层，持久化跨会话的长期记忆。

- **[Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify)** ⭐81,236  
  将代码、文档、数据库模式等转换为可查询的知识图谱，增强 RAG 推理。

- **[weaviate/weaviate](https://github.com/weaviate/weaviate)** ⭐16,549  
  云原生向量数据库，支持向量搜索与结构化过滤的混合查询。

- **[Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm)** ⭐63,009  
  本地优先的全能 LLM 工具，集 RAG、Agent、文档管理于一身。

---

## 趋势信号分析

从今日热榜来看，**AI Agent 工具链正在经历一场“基础设施化”浪潮**。`agent-skills`（+2,582 stars）和 `VoltAgent/awesome-design-md`（+1,233 stars）的爆发，标志着社区从“使用 Agent”转向“为 Agent 编写可复用的技能与设计规范”——这类似于早期前端生态的组件化演进。同时，`DesktopCommanderMCP` 和 `OfficeCLI` 的登榜，说明 MCP（Model Context Protocol）协议正在成为连接 Agent 与操作系统的标准桥梁。

**垂直场景应用出现“杀手级”案例**：`ai-job-search` 单日近 4000 stars，首次将 AI Agent 与求职全流程深度绑定，验证了“Agent + 高频刚需”模式的爆发力。`pentagi` 在网络安全领域的渗透测试 Agent 也获得 543 stars，表明安全自动化成为 Agent 落地的新锐方向。

**值得注意的新兴技术栈**：`pocket-tts` 作为 CPU 可运行的 TTS 模型，配合 `Ollama`、`vLLM` 等本地推理引擎，正推动“AI 边缘化”趋势。`system_prompts_leaks` 的持续增长（55k stars）则反映了社区对模型行为透明度和对“提示词工程”逆向工程的浓厚兴趣。

**与行业事件的关联**：近期 Anthropic 发布 Claude 的 MCP 协议和 Cookbook 更新，直接带动了周边生态（如 `claude-cookbooks` +347 stars）。OpenAI 的 GPT 5.5 系列传闻和 Google Gemini 3.5 的迭代，也间接推动了 `system_prompts_leaks` 这类对比分析项目的人气。

---

## 社区关注热点

- **🎯 `ai-job-search`**：以 3728 单日 stars 登顶，集简历优化、岗位匹配、面试准备于一体，是 AI Agent 在就业场景的最佳实践。**理由**：高频刚需 + Claude Code 深度集成，推荐有求职需求的开发者体验。

- **🧩 `agent-skills`**：生产级 Agent 技能库，帮助开发者快速为 Agent 注入专业能力。**理由**：类似“NPM 包 for Agent”，可能成为 Agent 生态的关键基础设施，值得关注其后续发展。

- **🔧 `OfficeCLI`**：首个为 AI 代理设计的 Office 命令行工具，无需 Office 安装即可操作文档。**理由**：办公自动化是 Agent 落地的最大场景之一，该项目或成为 RPA 替代品。

- **🕵️ `system_prompts_leaks`**：持续更新各主流模型系统提示词，已积累 55k stars。**理由**：对于理解模型行为、优化提示词工程、甚至安全审计都有极高参考价值。

- **🌐 `Graphify-Labs/graphify`**：将代码、文档、数据库等转化为知识图谱，增强 RAG 推理能力。**理由**：知识图谱 + RAG 是提升 LLM 精准度的前沿方向，该项目已获 81k stars，值得深入探索。

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*