# AI 开源趋势日报 2026-08-18

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-08-17 22:44 UTC

---

# AI 开源趋势日报 2026-08-18

## 一、今日速览

- **AI 安全赛道集中爆发**：AI 渗透测试工具 strix（+656）与 Anthropic-Cybersecurity-Skills（+156）同时登榜，智能体安全技能标准化趋势明确。
- **AI 内容生成热度持续**：MoneyPrinterTurbo 以今日 +1,275 stars 领跑 Trending，一键短视频自动化仍是社区最热应用场景之一。
- **Agent 记忆与上下文工程成新焦点**：ai-memory、claude-mem、headroom 等项目密集出现，长期记忆、上下文压缩正成为 Agent 生产级落地的核心瓶颈。
- **本地推理与硬件适配受关注**：llmfit（+239）、omlx（+96）登榜，Apple Silicon 和个人硬件上的模型运行体验成为新热点。
- **RAG/向量数据库生态依旧繁荣**：RAGFlow、AnythingLLM、Milvus 等在主题搜索中保持极高活跃度，检索增强仍是 AI 应用基础设施主力。

## 二、各维度热门项目

### 🔧 AI 基础工具

- [ollama/ollama](https://github.com/ollama/ollama) ⭐178,806 — 本地 LLM 运行的事实标准，已支持 Kimi、GLM、DeepSeek、Qwen 等最新模型。
- [huggingface/transformers](https://github.com/huggingface/transformers) ⭐164,195 — 模型定义与训练/推理的核心框架，文本、视觉、音频多模态全覆盖。
- [langchain-ai/langchain](https://github.com/langchain-ai/langchain) ⭐144,414 — Agent 工程化平台，Tool Calling 与 MCP 生态集成的枢纽。
- [vllm-project/vllm](https://github.com/vllm-project/vllm) ⭐89,275 — 高吞吐 LLM 推理与服务引擎，生产环境部署标配。
- [AlexsJones/llmfit](https://github.com/AlexsJones/llmfit) 今日 +239 — 一条命令匹配数百模型与你的硬件配置，解决"哪個模型跑得动"的选型痛点。
- [jundot/omlx](https://github.com/jundot/omlx) 今日 +96 — 面向 Apple Silicon 的 LLM 推理服务器，支持连续批处理与 SSD 缓存，macOS 菜单栏管理。
- [0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig) ⭐8,300 — Rust 原生 LLM 应用开发框架，模块化构建可扩展的 Agent 应用。

### 🤖 AI 智能体/工作流

- [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) ⭐186,655 — 开放式自主 Agent 平台，持续迭代的 AI 自动化先驱。
- [langgenius/dify](https://github.com/langgenius/dify) ⭐152,721 — 可视化构建 Agentic Workflow 与 RAG 管线，企业级私有化部署首选之一。
- [browser-use/browser-use](https://github.com/browser-use/browser-use) ⭐109,524 — 让 AI Agent 操作浏览器的核心库，网页自动化任务的事实标准。
- [shareAI-lab/learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) ⭐74,487 — 从零构建类 Claude Code 的 Agent Harness，"Bash is all you need"教学仓库。
- [akitaonrails/ai-memory](https://github.com/akitaonrails/ai-memory) 今日 +207 — 为 CLI 编码 Agent 提供长期记忆，支持跨 Agent 厂商无缝切换。
- [usestrix/strix](https://github.com/usestrix/strix) 今日 +656 — 开源 AI 渗透测试工具，自动发现并修复应用漏洞，AI 安全方向的黑马。
- [mukul975/Anthropic-Cybersecurity-Skills](https://github.com/mukul975/Anthropic-Cybersecurity-Skills) 今日 +156 — 817 个结构化网络安全技能，映射 MITRE ATT&CK、NIST CSF 2.0 等 6 大框架，兼容 20+ 平台。
- [esengine/DeepSeek-Reasonix](https://github.com/esengine/DeepSeek-Reasonix) ⭐34,682 — DeepSeek 原生的终端 AI 编码 Agent，针对 prefix-cache 稳定性优化，可常驻运行。

### 📦 AI 应用

- [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) ⭐105,904（今日 +1,275）— 输入主题一键生成高清短视频，AI 内容自动化最热项目。
- [santifer/career-ops](https://github.com/santifer/career-ops) ⭐64,576（今日 +147）— 开源 AI 求职助手：扫描职位、A-F 评分、定制简历、跟踪申请，本地 CLI 运行。
- [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) ⭐72,530 — 让 AI Agent 读取 Twitter/Reddit/YouTube/小红书等全网信息，零 API 费用。
- [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) ⭐63,165 — LLM 驱动的多市场股票智能分析系统，支持零成本定时运行。
- [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) ⭐47,489 — AI 一键生成原生 PowerPoint，支持动画、图表、音频旁白与自定义模板。
- [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) ⭐50,661 — 智能聊天 + 自主 Agent，统一接入前沿 LLM 的 AI 生产力工作台。

### 🧠 大模型/训练

- [tensorflow/tensorflow](https://github.com/tensorflow/tensorflow) ⭐196,989 — 经典 ML 框架，生态成熟、工业部署广泛。
- [pytorch/pytorch](https://github.com/pytorch/pytorch) ⭐102,439 — 动态神经网络框架，AI 研究与训练的事实标准。
- [microsoft/ML-For-Beginners](https://github.com/microsoft/ML-For-Beginners) ⭐89,459 — 12 周经典 ML 课程，入门必读的社区常青树。
- [open-compass/opencompass](https://github.com/open-compass/opencompass) ⭐7,310 — LLM 评测平台，支持 100+ 数据集、主流模型全面评估。
- [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) ⭐4,497 — 面向系统工程师的微型 LLM 推理系统教程，在 Apple Silicon 上从零实现 vLLM + Qwen。
- [thinkwee/AgentsMeetRL](https://github.com/thinkwee/AgentsMeetRL) ⭐1,784 — Agentic RL 优质资源清单，强化学习驱动 Agent 的前沿方向。

### 🔍 RAG/知识库

- [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) ⭐107,490 — 将代码库、文档、SQL Schema 转为可查询知识图谱，无需向量库。
- [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) ⭐91,008 — 跨会话持久上下文，AI 压缩会话记忆并在未来会话注入，支持 Claude Code、Codex 等。
- [infiniflow/ragflow](https://github.com/infiniflow/ragflow) ⭐88,678 — 领先的 RAG 引擎，融合 Agent 能力构建 LLM 上下文层。
- [Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm) ⭐64,834 — Local-first 全能 AI 工作台，内置 RAG 与 Agent，强调数据自主。
- [mem0ai/mem0](https://github.com/mem0ai/mem0) ⭐63,465 — 通用 AI Agent 记忆层，跨会话持久化用户与上下文信息。
- [run-llama/ll

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*