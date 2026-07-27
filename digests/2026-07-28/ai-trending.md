# AI 开源趋势日报 2026-07-28

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-27 22:36 UTC

---

# AI 开源趋势日报 (2026-07-28)

## 今日速览

今日 GitHub 热门趋势呈现 **AI 智能体能力深化**与**垂直领域基础模型**两大主线。`bradautomates/claude-video` 让 Claude 获得视频感知能力，`mvanhorn/last30days-skill` 则是多功能研究型 Agent skill，两者均获得数百新增 star；阿里开源的 `alibaba/open-code-review` 以混合 LLM + 确定性管道做代码审查，上线即近千 star；金融领域基础模型 `shiyu-coder/Kronos` 首日上榜。AI 主题搜索中，RAG 与 Agent 框架类项目（Dify、RAGFlow、browser-use）继续高歌猛进，说明社区正加速从“能用”走向“好用”的 AI 基础设施构建。

## 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

1. **[huggingface/transformers](https://github.com/huggingface/transformers)** ⭐ 163,046  
   🤗 Transformers: 定义模型的标准框架，支持文本、视觉、音频等任务的推理与训练，仍是 LLM 开发最核心的依赖。

2. **[ollama/ollama](https://github.com/ollama/ollama)** ⭐ 177,024  
   一键本地运行各种开源 LLM（Kimi、DeepSeek、Qwen 等），降低个人使用门槛，持续活跃。

3. **[alibaba/open-code-review](https://github.com/alibaba/open-code-review)** ⭐ 0 (+980 today)  
   阿里开源的混合架构代码审查工具，结合确定性规则流水线与 LLM Agent，内置 NPE、SQL 注入等规则，生产级可用。

4. **[shiyu-coder/Kronos](https://github.com/shiyu-coder/Kronos)** ⭐ 0 (+442 today)  
   金融市场的 Foundation Model，专为量化分析与交易语言设计，标志着垂直领域模型正走入开源视野。

5. **[The-Pocket/PocketFlow](https://github.com/The-Pocket/PocketFlow)** ⭐ 11,049  
   仅 100 行核心代码的 LLM 框架，强调“让 Agent 构建 Agent”，适合快速原型与教学。

6. **[samchon/nestia](https://github.com/samchon/nestia)** ⭐ 2,172 (topic: llm-model)  
   NestJS 辅助工具 + AI 聊天机器人开发，打通后端与 LLM 的集成。

### 🤖 AI 智能体 / 工作流（Agent 框架、自动化、多智能体）

1. **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** ⭐ 221,396  
   “与你一起成长的 Agent”，提供持续学习与自适应能力，社区热度极高。

2. **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** ⭐ 185,719  
   自动驾驶式 AI Agent 先驱，持续迭代为多工具、长任务执行平台。

3. **[browser-use/browser-use](https://github.com/browser-use/browser-use)** ⭐ 107,022  
   让 AI Agent 像人类一样操控浏览器，自动化在线任务，成为网页自动化新范式。

4. **[bradautomates/claude-video](https://github.com/bradautomates/claude-video)** ⭐ 0 (+412 today)  
   给 Claude“装上眼睛”——下载视频、抽帧、转录后交给 Claude 分析，扩展多模态 Agent 能力。

5. **[mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill)** ⭐ 0 (+221 today)  
   一个 Agent skill，跨 Reddit、X、YouTube 等多平台搜索并合成总结，体现 Agent 复合检索能力。

6. **[moeru-ai/airi](https://github.com/moeru-ai/airi)** ⭐ 0 (+554 today)  
   自托管的“Grok 伴侣”，支持实时语音聊天、Minecraft 操控等，尝试将 AI 融入虚拟世界交互。

7. **[FlowiseAI/Flowise](https://github.com/FlowiseAI/Flowise)** ⭐ 54,970  
   可视化构建 AI Agents，无需代码即可搭建 RAG、Agent 工作流，降低创新门槛。

### 📦 AI 应用（具体应用产品、垂直场景解决方案）

1. **[harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo)** ⭐ 99,554  
   利用 AI 大模型自动生成高清短视频，一键式“视频工厂”，创作者经济驱动。

2. **[PaddlePaddle/PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR)** ⭐ 86,358 (topic: rag)  
   轻量级 OCR 工具，将 PDF/图片转为结构化数据，打通 LLM 与文档之间的桥梁。

3. **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** ⭐ 49,048 (topic: ai-agent)  
   AI 生产力工作室，集成智能对话、自主 Agent 和 300+ 预设助手，统一管理多种 LLM。

4. **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** ⭐ 41,412 (topic: ai-agent)  
   AI 根据文档或主题生成原生 PowerPoint，支持动画、图表、语音旁白，办公场景利器。

5. **[pbakaus/impeccable](https://github.com/pbakaus/impeccable)** ⭐ 0 (+849 today)  
   面向 AI 的设计语言系统，旨在提升 AI 在 UI/UX 方面的表现，今日增量最高。

### 🧠 大模型 / 训练（模型权重、训练框架、微调、评估）

1. **[rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch)** ⭐ 99,977  
   从零实现一个 ChatGPT 类 LLM 的教程，PyTorch 逐行实现，技术教育标杆。

2. **[jingyaogong/minimind](https://github.com/jingyaogong/minimind)** ⭐ 53,906 (topic: llm-model)  
   2 小时从零训练 64M 参数的小 LLM，极大降低学习与实验成本。

3. **[open-compass/opencompass](https://github.com/open-compass/opencompass)** ⭐ 7,240 (topic: llm-model)  
   全面的 LLM 评估平台，支持 100+ 数据集和多款模型，为模型选型提供客观基准。

4. **[Picovoice/picollm](https://github.com/Picovoice/picollm)** ⭐ 315 (topic: llm-model)  
   端侧 LLM 推理引擎，采用 X-Bit 量化，适合嵌入式与移动设备。

### 🔍 RAG / 知识库（向量数据库、检索增强、知识管理）

1. **[langgenius/dify](https://github.com/langgenius/dify)** ⭐ 150,451 (topic: rag)  
   一站式 RAG + Agent 工作流平台，支持多种模型和工具，从原型到生产无需重构。

2. **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** ⭐ 86,160 (topic: rag)  
   领先开源 RAG 引擎，融合 Agent 能力，为 LLM 提供高质量上下文层。

3. **[milvus-io/milvus](https://github.com/milvus-io/milvus)** ⭐ 45,391 (topic: rag)  
   高性能云原生向量数据库，支撑大规模 ANN 搜索，RAG 系统的核心基础设施。

4. **[qdrant/qdrant](https://github.com/qdrant/qdrant)** ⭐ 33,613 (topic: vector-db)  
   另一主流向量数据库，以 Rust 实现高吞吐、低延迟，提供云服务。

5. **[mem0ai/mem0](https://github.com/mem0ai/mem0)** ⭐ 61,858 (topic: rag)  
   AI Agent 的通用记忆层，让 Agent 拥有跨会话的长期记忆，补齐 RAG 之外的上下文短板。

6. **[siyuan-note/siyuan](https://github.com/siyuan-note/siyuan)** ⭐ 45,457 (topic: ai-agent)  
   隐私优先的个人知识管理系统，支持 AI 集成，用作本地知识库与 Agent 的储存后端。

7. **[topoteretes/cognee](https://github.com/topoteretes/cognee)** ⭐ 29,463 (topic: vector-db)  
   开源 AI 记忆平台，通过自托管知识图谱引擎赋予 Agent 持久记忆。

## 趋势信号分析

1. **AI 智能体的“感官”正在扩展**：`claude-video` 和 `last30days-skill` 表明，社区不再满足于纯文本 Agent，而是赋予其视频理解、跨平台检索等复合能力，这预示着多模态 Agent skill 将进入爆发期。

2. **垂直领域基础模型开始登台**：`Kronos`（金融）首次出现在 Trending 榜单，说明 LLM 正在从通用向金融、医疗、法律等垂直细分渗透。这类模型往往结合领域语言（如交易指令、报表数据）做预训练，价值远高于通用模型。

3. **代码审查 + AI 成为企业级新热点**：阿里巴巴开源的 `open-code-review` 上线即收获 980+ star，以“确定性流水线 + LLM Agent”混合架构提供精准的行级评论，代表企业将 AI 嵌入 DevOps 的新范式。

4. **RAG 基础设施趋于成熟**：Dify、RAGFlow 等项目 star 数持续增长，同时向量数据库（Milvus、Qdrant、LanceDB）竞争白热化，RAG 已从“概念验证”进入“规模化部署”阶段。

5. **混合推理与记忆层受追捧**：`mem0`、`cognee` 等专门为 Agent 设计的记忆系统获得数万 star，表明社区认识到长程任务中上下文管理的重要性，未来“记忆即服务”可能成为 AI 中间件的新赛道。

## 社区关注热点

- **bradautomates/claude-video** 🎥 — 让 Claude 处理视频输入，复用现有的 LLM 能力到多模态，对视频分析、内容审核等场景有直接价值。今日新增 412 star，值得一试。
- **alibaba/open-code-review** 🔍 — 开源、免费、生产验证的 AI 代码审查工具，内置 NPE、线程安全等规则集，适合团队提升代码质量。今日新增 980 star，增速惊人。
- **PocketFlow** 🧩 — 仅有 100 行核心代码的 LLM 框架，适合想理解 Agent 原理的开发者，也适合快速构建轻量级 Agent。
- **opencompass** 📊 — 模型评估平台，支持 100+ 数据集，对于需要选型或测试自有模型的团队是必备工具。近期更新频繁，值得关注。
- **mem0 + cognee** 🧠 — 两个专注 AI 记忆层的项目均在快速增长，它们为 Agent 提供长期上下文，有望成为 RAG 之后的下一个必备组件。建议集成到自己的 Agent 项目中验证效果。

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*