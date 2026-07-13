# AI 开源趋势日报 2026-07-14

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-13 23:17 UTC

---

# AI 开源趋势日报 (2026-07-14)

## 今日速览

今日 GitHub 热门榜上 AI 项目占据六席，其中交易智能体 Vibe-Trading、AI 编程助手 Graphify 和 LLM 应用合集 awesome-llm-apps 收获千余 stars，社区对可落地、可复用的 Agent 工具需求旺盛。主题搜索数据中，AI Agent 和 RAG 生态继续膨胀，Hermes Agent、OpenHands、CherryStudio 等平台级项目 star 数已突破十万级别。值得注意的是，面向 AI Agent 的记忆层、知识图谱与持久化上下文（如 mem0、Graphify、claude-mem）成为新热点，标志着从 “对话能力” 向 “长期记忆与知识管理” 的纵深演进。

---

## 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|------------|
| [tensorflow/tensorflow](https://github.com/tensorflow/tensorflow) | 196,300 | — | 经典深度学习框架，仍是工业级训练和推理的基石。 |
| [pytorch/pytorch](https://github.com/pytorch/pytorch) | 101,791 | — | 动态神经网络框架，研究社区首选，GPU 加速训练标配。 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | 162,573 | — | 模型定义与推理框架，支持文本、视觉、多模态 SOTA 模型。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 86,162 | — | 高吞吐 LLM 推理引擎，内存优化显著，生产部署首选。 |
| [ollama/ollama](https://github.com/ollama/ollama) | 176,060 | — | 本地运行大模型的一站式工具，支持 Kimi、DeepSeek、Qwen 等最新模型。 |
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | 145,310 | — | 用户友好 AI 界面，兼容 Ollama 与 OpenAI API，快速搭建私有聊天平台。 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | 141,694 | — | Agent 与 LLM 应用编排框架，行业标准，社区生态最丰富。 |

### 🤖 AI 智能体 / 工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|------------|
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 214,248 | — | 开源 Agent 框架，强调可成长性，今日热度极高。 |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 185,511 | — | 自动智能体先驱，使命是让每个人都能使用和构建 AI。 |
| [OpenHands/OpenHands](https://github.com/OpenHands/OpenHands) | 80,671 | — | AI 驱动的开发助手，可自主执行编码任务。 |
| [HKUDS/Vibe-Trading](https://github.com/HKUDS/Vibe-Trading) | — | **+1,148 today** | 个人交易 Agent，今日 Trending 榜首，AI 量化交易新宠。 |
| [moeru-ai/airi](https://github.com/moeru-ai/airi) | — | **+57 today** | 自托管 Grok 伴侣，支持实时语音、游戏操作，类似 Neuro-sama 的开源实现。 |
| [esengine/DeepSeek-Reasonix](https://github.com/esengine/DeepSeek-Reasonix) | 26,868 | — | 深度求索原生的终端编码 Agent，专为前缀缓存稳定性设计。 |
| [jackwener/OpenCLI](https://github.com/jackwener/OpenCLI) | 26,597 | — | 将任意网站转化为 CLI 工具，供 AI Agent 在已登录浏览器中使用。 |

### 📦 AI 应用（具体应用产品、垂直场景解决方案）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|------------|
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 48,521 | — | AI 生产力工作室，内置智能聊天、自主 Agent 和 300+ 助手。 |
| [Shubhamsaboo/awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps) | 119,545 | **+1,006 today** | 100+ 可运行的 AI Agent 与 RAG 应用集合，克隆即用。 |
| [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) | — | **+260 today** | 专为 Claude Code 等 AI Agent 设计的营销技能集（CRO、SEO、文案）。 |
| [Nutlope/hallmark](https://github.com/Nutlope/hallmark) | — | **+802 today** | 反 AI 低质设计的 CSS 技能包，用于 Claude Code、Cursor 等编码助手，提升生成内容的视觉质量。 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | 38,759 | — | AI 根据任意文档生成可编辑的 PowerPoint，保留原生图表、语音备注。 |
| [OpenBB-finance/OpenBB](https://github.com/OpenBB-finance/OpenBB) | 70,531 | — | 面向分析师、量化人员和 AI Agent 的开放数据平台。 |

### 🧠 大模型 / 训练（模型权重、训练框架、微调工具）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|------------|
| [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | 99,035 | — | 从零实现类 ChatGPT 大模型的教育级代码教程（PyTorch）。 |
| [ultralytics/ultralytics](https://github.com/ultralytics/ultralytics) | 59,448 | — | YOLO 系列目标检测框架，持续迭代至 v26，支持多任务。 |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | 285 | — | 可靠、最小化、可扩展的基础模型预训练库，新兴项目值得关注。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,186 | — | LLM 评估平台，覆盖 100+ 数据集，支持主流模型。 |
| [starpig1129/DATAGEN](https://github.com/starpig1129/DATAGEN) | 1,769 | — | 多智能体研究助手，自动生成假设、分析数据、撰写报告。 |

### 🔍 RAG / 知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 今日新增 | 一句话说明 |
|------|-------|----------|------------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 84,964 | — | 领先的开源 RAG 引擎，融合 Agent 能力，提供优质上下文层。 |
| [HKUDS/LightRAG](https://github.com/HKUDS/LightRAG) | 37,633 | — | 简单快速的 RAG 方案，EMNLP 2025 论文配套实现。 |
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | 84,621 | **+1,028 today** | AI 编程助手技能，将代码/文档/数据转化为可查询的知识图谱，今日热度极高。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 60,748 | — | AI Agent 的通用记忆层，实现跨会话持久化。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 45,210 | — | 高性能云原生向量数据库，专为 ANN 搜索构建。 |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | 87,109 | — | 捕获 Agent 会话、压缩并注入上下文，实现跨 session 记忆。 |
| [topoteretes/cognee](https://github.com/topoteretes/cognee) | 27,768 | — | 开源 AI 记忆平台，自托管知识图谱引擎，为 Agent 提供长期记忆。 |

---

## 趋势信号分析

从今日数据中可提炼出三大趋势信号：

1. **AI Agent 生态进入“商业化落地”阶段**  
   今日 Trending 中 Vibe-Trading（交易 Agent）和 awesome-llm-apps（可运行应用集）均获得超千次日增星，说明社区不再满足于框架演示，而是渴望可直接获取价值的“即用型” Agent。同时 marketing skills、hallmark 等面向特定行业（营销、UI 设计）的技能包崛起，标志着 Agent 能力正从通用向垂直领域下沉。

2. **记忆与知识管理成为下一代 Agent 的关键基础设施**  
   主题搜索中 mem0（60k+ stars）、claude-mem（87k+）、cognee（27k+）、Graphify（今日新增 1,028）等项目集体爆发，且均围绕“跨会话记忆”、“知识图谱构建”、“上下文压缩”等能力。这暗示当前 LLM 单次交互能力已趋成熟，开发者焦点转向如何让 Agent 拥有长期记忆和结构化知识，以支撑真正的自主工作流。

3. **向量数据库与 RAG 引擎持续迭代，但侧重“轻量级”与“多模态”方向**  
   Milvus、Qdrant 等传统向量库仍占主流，但 lancedb（嵌入式检索库，10k+ stars）、alibaba/zvec（轻量级进程内向量库，14k+）等轻量化方案开始获得关注。同时 PageIndex（无向量 RAG）和 headroom（压缩 token 工具）等创新项目出现，表明 RAG 技术正从“单纯向量检索”走向更智能、更经济的上下文处理。

---

## 社区关注热点

- **🌐 Vibe-Trading** — 今日 Trending 榜首，展示 AI Agent 在金融量化领域的实际应用潜力，适合想探索自动化交易的开源开发者。
- **📊 Graphify** — 将任意代码/文档/视频转化为知识图谱，同时支持 Claude Code 等多款编码助手，是连接“代码知识”与“RAG”的桥梁，值得深入体验。
- **🧠 mem0 / claude-mem** — 两大记忆层项目竞争激烈，mem0 通用性强，claude-mem 专为 AI 编码场景优化，选择哪个将影响 Agent 长期任务的设计模式。
- **🎨 hallmark** — 反 AI 低质设计的 CSS 技能包，针对 AGI 编码工具输出粗糙 UI 的痛点，开源社区首次出现专门“美化”AI 生成结果的工具，可能开启新品类。
- **🛠 awesome-llm-apps** — 100+ 可运行的 Agent 与 RAG 应用，覆盖电商、客服、教育等场景，是快速构建原型的最佳资源库，适合所有 AI 应用开发者。

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*