# AI 开源趋势日报 2026-07-12

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-11 23:14 UTC

---

# AI 开源趋势日报 | 2026-07-12

## 今日速览

1. **Agent 技能生态爆发**：`superpowers`、`stitch-skills`、`claude-code-templates` 等项目今日新增 stars 迅猛，社区正从单一 Agent 工具转向跨平台、可复用的 Agent 技能/ skill 标准。
2. **MCP 服务器成为 Agent 基础组件**：`DesktopCommanderMCP` 单日暴涨 900 stars，说明开发者对将 Claude 等 AI 代理连接到终端、文件系统的需求极强，MCP 协议正在快速落地。
3. **向量数据库与记忆层持续升温**：`mem0`、`cognee`、`memvid` 等项目 stars 居高不下，AI 长期记忆和多模态知识管理成为 RAG 之后的新增长点。
4. **AI 辅助绘图/文档生成落地**：`next-ai-draw-io` 和 `PPT-Master` 等应用级工具证明 AI 从对话走向具体生产力场景的趋势明显。
5. **大模型生态链日益完整**：从基础框架（transformers、vllm）到训练（stable-pretraining）再到评估（opencompass），全栈工具链日趋成熟。

---

## 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

- **[ollama/ollama](https://github.com/ollama/ollama)** ⭐175,936  
  本地运行大模型的最简方式，已支持 Kimi、GLM、DeepSeek 等最新模型，是本地 AI 开发的首选入口。

- **[huggingface/transformers](https://github.com/huggingface/transformers)** ⭐162,503  
  业界标准模型库，支持文本、视觉、音频多模态，今日持续活跃。

- **[vllm-project/vllm](https://github.com/vllm-project/vllm)** ⭐85,988  
  高性能 LLM 推理引擎，吞吐和内存优化领先，生产部署标配。

- **[langchain4j/langchain4j](https://github.com/langchain4j/langchain4j)** ⭐12,574 [topic:vector-db]  
  Java 生态的 LLM 开发框架，原生支持 MCP、Agent 和 RAG，与 Spring Boot/Quarkus 深度集成。

- **[0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig)** ⭐7,895 [topic:llm-model]  
  Rust 语言实现的模块化 LLM 应用框架，兼具性能和类型安全。

- **[davila7/claude-code-templates](https://github.com/davila7/claude-code-templates)** ⭐0 (+230 today) [Trending]  
  Claude Code 的 CLI 配置与监控工具，让开发者轻松管理 Agent 行为模板。

- **[obra/superpowers](https://github.com/obra/superpowers)** ⭐0 (+737 today) [Trending]  
  一套 Agent 技能框架与软件开发方法论，强调可复用、可组合的技能单元，今日爆火。

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐213,275 [topic:ai-agent]  
  自增长式 AI Agent 框架，强调持续进化和自我改进。

- **[langgenius/dify](https://github.com/langgenius/dify)** ⭐148,521 [topic:rag]  
  生产级 Agentic Workflow 开发平台，支持拖拽编排、RAG、插件，企业级首选。

- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** ⭐185,478 [topic:llm]  
  最早的自主 AI Agent 项目，持续迭代，已成为多智能体协作的参考实现。

- **[browser-use/browser-use](https://github.com/browser-use/browser-use)** ⭐104,262 [topic:llm]  
  让 AI 代理操控浏览器的标准库，自动化网页操作与数据采集。

- **[CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit)** ⭐35,923 [topic:ai-agent]  
  前端 Agent 交互栈，支持 React、Angular、移动端，提供 AG-UI 协议。

- **[HKUDS/nanobot](https://github.com/HKUDS/nanobot)** ⭐45,263 [topic:ai-agent]  
  轻量级开源 Agent，支持工具调用、聊天和工作流编排，一行安装即用。

- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐48,452 [topic:ai-agent]  
  AI 生产力工作室：智能聊天、自主代理、300+ 助手，统一接入前沿 LLM。

- **[wonderwhy-er/DesktopCommanderMCP](https://github.com/wonderwhy-er/DesktopCommanderMCP)** ⭐0 (+900 today) [Trending]  
  MCP 服务器，为 Claude 提供终端控制、文件搜索与 diff 编辑能力，今日新增 stars 最高。

### 📦 AI 应用（具体应用产品、垂直场景解决方案）

- **[DayuanJiang/next-ai-draw-io](https://github.com/DayuanJiang/next-ai-draw-io)** ⭐0 (+74 today) [Trending]  
  用自然语言生成和编辑 draw.io 图表，AI 辅助可视化新玩法。

- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** ⭐38,399 [topic:ai-agent]  
  从任意文档一键生成原生可编辑 PowerPoint，支持动画、图表、演说备注，AI 办公利器。

- **[TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents)** ⭐92,365 [topic:llm]  
  多智能体 LLM 金融交易框架，让 AI 代理协同分析市场并执行交易。

- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** ⭐56,681 [topic:ai-agent]  
  LLM 驱动的多市场股票智能分析系统，零成本定时运行，适合个人投资者。

- **[openai/plugins](https://github.com/openai/plugins)** ⭐0 (+75 today) [Trending]  
  OpenAI 官方插件示例（JavaScript），虽非新项目，但今日仍获关注，反映插件生态活力。

- **[acon96/home-llm](https://github.com/acon96/home-llm)** ⭐1,377 [topic:llm-model]  
  本地 LLM 控制智能家居的 Home Assistant 集成，用自然语言管理家庭设备。

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

- **[rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch)** ⭐98,932 [topic:llm]  
  手把手指南：用 PyTorch 从零实现 ChatGPT 类 LLM，教育价值极高。

- **[tensorflow/tensorflow](https://github.com/tensorflow/tensorflow)** ⭐196,297 [topic:ml]  
  传统深度学习框架，持续维护并支持最新硬件加速。

- **[pytorch/pytorch](https://github.com/pytorch/pytorch)** ⭐101,752 [topic:ml]  
  动态神经网络框架，AI 研究/工业界的事实标准。

- **[ultralytics/ultralytics](https://github.com/ultralytics/ultralytics)** ⭐59,357 [topic:ml]  
  YOLO 系列最全实现，支持检测、分割、姿态估计，目标检测领域标杆。

- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** ⭐7,184 [topic:llm-model]  
  全面 LLM 评测平台，覆盖 100+ 数据集，模型能力对比利器。

- **[galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining)** ⭐283 [topic:llm-model]  
  可靠、最小化的预训练库，面向基础模型和世界模型，适合高阶研究者。

- **[starpig1129/DATAGEN](https://github.com/starpig1129/DATAGEN)** ⭐1,768 [topic:llm-model]  
  多智能体研究助手，自动完成假设生成、数据分析、报告撰写。

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

- **[open-webui/open-webui](https://github.com/open-webui/open-webui)** ⭐145,086 [topic:rag]  
  用户友好的 AI 界面（支持 Ollama、OpenAI API），内置 RAG 能力，本地部署首选。

- **[langchain-ai/langchain](https://github.com/langchain-ai/langchain)** ⭐141,545 [topic:rag]  
  最流行的 Agent/RAG 开发框架，生态最丰富，持续领跑。

- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** ⭐45,197 [topic:vector-db]  
  云原生高性能向量数据库，支持 ANN 搜索，企业级 RAG 标配。

- **[qdrant/qdrant](https://github.com/qdrant/qdrant)** ⭐33,160 [topic:vector-db]  
  高可扩展向量数据库，支持云原生部署，AI 搜索领域明星项目。

- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** ⭐60,626 [topic:rag]  
  通用 AI Agent 记忆层，为智能体提供跨会话持久记忆，RAG 进化方向。

- **[topoteretes/cognee](https://github.com/topoteretes/cognee)** ⭐27,583 [topic:vector-db]  
  开源 AI 记忆平台，基于知识图谱实现 Agent 长期记忆，自托管方案。

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐84,828 [topic:rag]  
  领先的开源 RAG 引擎，融合 Agent 能力与上下文管理，支持多模态。

- **[meilisearch/meilisearch](https://github.com/meilisearch/meilisearch)** ⭐58,507 [topic:vector-db]  
  闪电般快速的搜索引擎，内置 AI 混合搜索，适合网站/应用集成。

---

## 趋势信号分析

### 🔥 爆发性关注：Agent 技能标准化与 MCP 生态

今日 Trending 榜单中，`DesktopCommanderMCP` 以 **+900 stars** 登顶、`superpowers` 以 **+737 stars** 紧随其后，`stitch-skills` 和 `claude-code-templates` 也表现抢眼。这标志着 AI Agent 正从“单一工具”向“可组合技能（Skills）”和“统一协议（MCP）”转型。社区不再满足于单个聊天机器人，而是希望用标准化的技能单元（文件操作、终端控制、浏览器交互）搭建自定义工作流。`superpowers` 甚至提出了一整套软件开发方法论，强调“技能即模块”，可能重塑 AI 辅助编程的范式。

### 🆕 新兴方向首次登榜：AI 辅助绘图与文档生成

`next-ai-draw-io` 和 `ppt-master`（主题搜索中高星）等应用级项目首次获得显著关注。前者用自然语言直接操作 draw.io 图表，后者将文档一键转化为原生 PowerPoint。这反映出 AI 正从“代码生成”向“视觉/文档生产力”扩展，多模态输出能力开始落地。

### 🧠 与行业事件的关联

- 近期 Anthropic 持续更新 Claude Code，推动 MCP 协议标准化，直接催生了 `DesktopCommanderMCP` 等生态组件的流行。
- OpenAI 发布 ChatGPT 插件规范更新，带动 `openai/plugins` 重新获得关注。
- 多家模型厂商（DeepSeek、Qwen、Gemma）密集发布新版本，`ollama` 迅速集成，持续刺激本地推理需求。
- RAG 领域竞争加剧，传统向量数据库（Milvus、Qdrant）与新兴记忆层（mem0、cognee）并行发展，后者更强调 Agent 的长期上下文记忆。

---

## 社区关注热点

- **⭐ `wonderwhy-er/DesktopCommanderMCP`** — 今日 stars 增速第一，MCP 服务器 + 终端控制，让 Claude 真正拥有本地操作能力。
- **⭐ `obra/superpowers`** — 提出 Agent 技能框架与软件工程方法论，有望成为下一代 AI 辅助开发的最佳实践。
- **⭐ `mem0/mem0`** — 通用记忆层，解决 Agent 跨会话遗忘问题，与 RAG 互补，是迈向真正智能体的关键组件。
- **⭐ `dayuanjiang/next-ai-draw-io`** — 用自然语言画图，低代码可视化场景潜力大，适合产品经理、设计师快速原型。
- **⭐ `CherryHQ/cherry-studio`** — 统一接入 300+ 助手，集成 Agent 功能，面向日常生产力提升，适合不想折腾多个工具的开发者。

---

*数据来源：GitHub Trending (2026-07-12) + GitHub Search API (topic: rag, vector-db, ai-agent, llm, llm-model, ml)*

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*