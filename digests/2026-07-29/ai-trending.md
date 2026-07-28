# AI 开源趋势日报 2026-07-29

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-28 22:35 UTC

---

# AI 开源趋势日报（2026-07-29）

## 1. 今日速览

今日 GitHub 上 AI 领域热点密集：**AI 智能体（Agent）** 生态持续爆发，微软发布官方级治理工具包，多个“Claude Code 技能”类项目斩获高星；**语音 / 视频多模态 Agent** 成为新风口，Hugging Face 推出本地语音代理，个人开发者“让 Claude 看视频”项目一日涨星近千；**AI 统一接口**（Andrew Ng 的 aisuite）和**自托管 AI 伴侣**（moeru-ai/airi）也受到社区追捧，反映出开发者对易用、可本地运行的工具链需求旺盛。

---

## 2. 各维度热门项目

### 🔧 AI 基础工具
| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [andrewyng/aisuite](https://github.com/andrewyng/aisuite) | ⭐ 92 (today) | Andrew Ng 出品的多生成式 AI 提供商统一接口，简化 LLM 调用。 |
| [ollama/ollama](https://github.com/ollama/ollama) | 177,128 | 本地运行 Kimi、DeepSeek、Qwen 等主流模型的 CLI 工具，AI 开发者标配。 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | 163,072 | 🤗 模型定义框架，支持文本/视觉/音频/多模态推理与训练。 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | 142,817 | Agent 工程平台，提供 LLM 应用构建的标准抽象层。 |
| [firecrawl/firecrawl](https://github.com/firecrawl/firecrawl) | 157,494 | 专为 AI Agent 设计的网页搜索与抓取 API，今日新增 430+ ⭐。 |
| [open-webui/open-webui](https://github.com/open-webui/open-webui) | 147,109 | 用户友好的 AI 界面，支持 Ollama/OpenAI API，可自托管。 |
| [microsoft/agent-governance-toolkit](https://github.com/microsoft/agent-governance-toolkit) | 17 (today) | 微软官方 AI Agent 治理工具包：策略执行、零信任身份、沙箱执行、可靠性工程。 |

### 🤖 AI 智能体 / 工作流
| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 185,742 | “人人可用的 AI”愿景下的 Agent 框架，支持自主任务执行。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 107,126 | 让 AI Agent 自动操作浏览器，在线任务自动化利器。 |
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | 234,745 (+692 today) | Agent 性能优化系统，为 Claude Code/Codex/Cursor 等提供技能、记忆、安全框架。 |
| [moeru-ai/airi](https://github.com/moeru-ai/airi) | +796 today | 自托管 Grok 伴侣，支持实时语音聊天、Minecraft/Factorio 游玩，类 Neuro-sama 风格。 |
| [langgenius/dify](https://github.com/langgenius/dify) | 150,578 | 可视化 Agent 工作流与 RAG 管道构建平台，支持多模型与团队协作。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 61,944 | 通用 AI Agent 记忆层，跨会话持久化上下文。 |
| [bradautomates/claude-video](https://github.com/bradautomates/claude-video) | +989 today | 让 Claude 能“看视频”——自动下载、抽帧、转录并交付给 AI 分析的 CLI 工具。 |

### 📦 AI 应用
| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [huggingface/speech-to-speech](https://github.com/huggingface/speech-to-speech) | +177 today | 基于开源模型构建本地语音代理（语音对话/语音交互）。 |
| [virgiliojr94/book-to-skill](https://github.com/virgiliojr94/book-to-skill) | +366 today | 将技术 PDF 转化为 Claude Code 技能，实现边工作边参考。 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 49,091 | AI 生产力工作室，集成智能聊天、自主 Agent 和 300+ 助手预设。 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | 41,624 | AI 根据文档或主题自动生成原生 PowerPoint，含动画、图表与音频旁白。 |
| [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | 99,740 | 利用 AI 大模型一键生成高清短视频，适合内容创作者。 |
| [HKUDS/Vibe-Trading](https://github.com/HKUDS/Vibe-Trading) | 28,323 | 个人级 AI 交易 Agent，自动分析市场并执行策略。 |

### 🧠 大模型 / 训练
| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | 100,055 | 从零实现 ChatGPT 类 LLM 的经典教程与代码。 |
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) | 53,946 | 2小时从 0 训练 64M 参数小模型，门槛极低。 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | 4,421 | 面向系统工程师的 LLM 推理服务课程：在 Apple Silicon 上构建微型 vLLM。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,241 | 支持 100+ 数据集的 LLM 评估平台。 |
| [Picovoice/picollm](https://github.com/Picovoice/picollm) | 315 | 设备端 LLM 推理引擎，基于 X-Bit 量化，适合边缘部署。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 221,879 | “与你一同成长的 Agent”，支持技能学习与持续演进。 |

### 🔍 RAG / 知识库
| 项目 | Stars | 一句话说明 |
|------|-------|-----------|
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 86,263 | 领先的开源 RAG 引擎，融合 Agent 能力，为 LLM 提供优质上下文层。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 45,404 | 高性能云原生向量数据库，支持大规模 ANN 搜索。 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | 33,631 | 高可用向量数据库与搜索引擎，AI 应用的检索基础设施。 |
| [weaviate/weaviate](https://github.com/weaviate/weaviate) | 16,655 | 开源向量数据库，支持向量+结构化过滤，云原生容错。 |
| [lancedb/lancedb](https://github.com/lancedb/lancedb) | 11,016 | 嵌入式多模态检索库，开发者友好、存储高效。 |
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | 97,729 | 将代码库/文档/SQL 模式转为可查询知识图谱，无需向量存储。 |

---

## 3. 趋势信号分析

**🔥 爆发性关注领域：AI Agent 的“技能与记忆”生态。** 今日 Trending 榜上有 3 个项目（ECC、book-to-skill、claude-video）直接为 Claude Code 及其他 CLI Agent 提供“技能注入”能力，涨星速度极快（ECC +692、book-to-skill +366、claude-video +989）。这表明开发者社区正从使用现成 Agent 转向 **定制化 Agent 技能**，将特定知识、工具、多模态能力以轻量插件形式注入 Agent。

**🎙️ 语音/视频多模态 Agent 首次高频登榜。** Hugging Face 的 `speech-to-speech` 和 `bradautomates/claude-video` 分别代表了语音对话和视频理解两个方向。前者展示了本地运行语音代理的可行性，后者则暴露了“让老模型看懂视频”的灵活方案，两者共同指向 **Agent 从纯文本走向多感官交互** 的趋势。

**🏭 治理与安全开始成为正式议题。** 微软发布的 `agent-governance-toolkit` 覆盖了 OWASP Agentic Top 10 中的全部 10 项风险，这是首个来自头部厂商的 Agent 治理级开源项目，预示着企业级 Agent 落地的安全合规需求正在加速标准化。

---

## 4. 社区关注热点

- **⭐ [affaan-m/ECC](https://github.com/affaan-m/ECC)（+692 today）**：Agent 技能/记忆/安全一体化框架，已被 234K 星关注，是今日增长最快的 AI 智能体生态项目。值得深入研究其“研究优先”的架构设计。
- **🎬 [bradautomates/claude-video](https://github.com/bradautomates/claude-video)（+989 today）**：用极简方式让 Claude 处理视频，开源方案可直接复用，适合需要多模态 Agent 的场景。
- **🗣️ [huggingface/speech-to-speech](https://github.com/huggingface/speech-to-speech)（+177 today）**：实现端到端语音代理的官方入门项目，搭配 Ollama 可快速搭建本地语音助手。
- **📚 [virgiliojr94/book-to-skill](https://github.com/virgiliojr94/book-to-skill)（+366 today）**：将技术书籍变成 Agent 可用的技能，为开发者提供“知识即代码”的实用模式。
- **🛡️ [microsoft/agent-governance-toolkit](https://github.com/microsoft/agent-governance-toolkit)（+17 today）**：虽然今日涨星不多，但作为微软官方推出的 Agent 安全治理项目，对生产环境部署有长远参考价值。

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*