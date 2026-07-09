# AI 开源趋势日报 2026-07-09

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-09 01:52 UTC

---

# AI 开源趋势日报（2026-07-09）

## 1. 今日速览

- **Agent 基础设施爆发**：腾讯云连推 `TencentDB-Agent-Memory`（本地长期记忆）和 `CubeSandbox`（安全沙箱），同时 `agent-skills`、`superpowers` 等技能框架获得大量关注，AI Agent 的“内存/技能/安全”三大基础组件正在快速成型。
- **Office 场景 AI 化加速**：`OfficeCLI` 首日涨星 1717，成为今天最亮眼的新项目；`bradautomates/claude-video` 让 AI 能“看”视频，办公与多媒体自动化的落地路径愈发清晰。
- **提示词泄露与反思**：`system_prompts_leaks` 今日新增 1218 星，社区对闭源模型的 prompt 工程反向分析热情高涨，也侧面反映 AI 安全与透明性议题升温。
- **向量数据库轻量化趋势**：阿里 `zvec` 以“进程内、超快”定位出现，配合 `lancedb`、`orama` 等嵌入式方案，向量检索正从云端下沉到本地边缘。

## 2. 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

| 项目 | Stars | 说明 |
|------|-------|------|
| [ollama/ollama](https://github.com/ollama/ollama) | 175k | 本地运行大模型的极简 CLI，已支持 Kimi、GLM、DeepSeek 等最新模型，是个人开发者首选推理入口。 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | 162k | 业界标准模型定义与推理框架，支持文本/视觉/语音/多模态，今日仍为最活跃的 AI 库之一。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 85k | 高吞吐、内存高效的 LLM 推理引擎，是生产部署的首选，持续优化 PagedAttention 等核心技术。 |
| [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | 141k | Agent 工程平台，今日仍是最广泛使用的 Agent 编排框架之一。 |
| [wonderwhy-er/DesktopCommanderMCP](https://github.com/wonderwhy-er/DesktopCommanderMCP) | ⭐28 today | MCP 服务器，为 Claude 提供终端控制、文件搜索与 diff 编辑能力，是 Agent 与本地系统交互的关键桥梁。 |
| [TencentCloud/CubeSandbox](https://github.com/TencentCloud/CubeSandbox) | ⭐564 today | 为 AI Agent 设计的即时、并发、轻量沙箱，提供安全隔离的执行环境，底层用 Rust 实现。 |

### 🤖 AI 智能体/工作流（Agent 框架、多智能体、自动化）

| 项目 | Stars | 说明 |
|------|-------|------|
| [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | ⭐1297 today | 生产级 AI 编码 Agent 技能集合，让 Agent 具备工程化能力，今日热榜第一。 |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 185k | 经典自主 Agent 框架，持续进化，是 Agent 生态的基石项目。 |
| [langgenius/dify](https://github.com/langgenius/dify) | 148k | 生产级 Agentic 工作流开发平台，低代码可视化，适合快速构建复杂 Agent。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | 103k | 让 AI Agent 能像人一样操作浏览器，自动化在线任务，Web 交互 Agent 的标杆。 |
| [mvanhorn/last30days-skill](https://github.com/mvanhorn/last30days-skill) | ⭐352 today | AI Agent 技能：自动检索 Reddit、X、YouTube、HN 等多平台内容并合成摘要，实效信息获取利器。 |
| [obra/superpowers](https://github.com/obra/superpowers) | ⭐1116 today | Agent 技能框架与软件开发方法论，强调“结构化技能”范式，今日热度极高。 |

### 📦 AI 应用（具体产品、垂直场景解决方案）

| 项目 | Stars | 说明 |
|------|-------|------|
| [iOfficeAI/OfficeCLI](https://github.com/iOfficeAI/OfficeCLI) | ⭐1717 today | 专为 AI Agent 设计的 Office 套件（Word/Excel/PPT），单二进制，无需安装 Office，今日涨星最多。 |
| [bradautomates/claude-video](https://github.com/bradautomates/claude-video) | ⭐951 today | 让 Claude 能“观看”视频：下载、抽帧、转录后交给 LLM 分析，视频理解应用创新。 |
| [ruvnet/RuView](https://github.com/ruvnet/RuView) | ⭐799 today | 用 WiFi 信号实现实时空间感知、生命体征监测，无需摄像头，隐私友好的环境智能产品。 |
| [Shubhamsaboo/awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps) | 116k | 100+ 可直接运行的 AI Agent 和 RAG 应用合集，是学习与复用的宝藏库。 |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | 91k | 多智能体 LLM 金融交易框架，AI 辅助量化交易的热门项目。 |

### 🧠 大模型/训练（模型权重、训练框架、微调、提示词资源）

| 项目 | Stars | 说明 |
|------|-------|------|
| [asgeirtj/system_prompts_leaks](https://github.com/asgeirtj/system_prompts_leaks) | ⭐1218 today | 收集并公开了 Anthropic、OpenAI、Google、xAI 等多家公司最新模型的系统提示词，是 prompt 工程和模型行为研究的直接素材。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7k | 大模型评测平台，支持 100+ 数据集，是评估模型能力的关键工具。 |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | 281 | 可靠的预训练库，注重稳定性与可扩展性，适合研究和生产预训练。 |
| [chrisliu298/awesome-llm-unlearning](https://github.com/chrisliu298/awesome-llm-unlearning) | 607 | LLM 机器遗忘（unlearning）的资源汇总，安全合规方向的前沿主题。 |

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 说明 |
|------|-------|------|
| [alibaba/zvec](https://github.com/alibaba/zvec) | ⭐395 today | 轻量级进程内向量数据库，C++ 实现，极速检索，适合嵌入到本地应用。 |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 84k | 领先的开源 RAG 引擎，融合 Agent 能力，提供上下文层，企业级部署常见选择。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | 45k | 云原生向量数据库，高性能 ANN 搜索，支撑大规模 RAG 系统。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 60k | AI Agent 的通用记忆层，跨会话持久化上下文，解决 Agent 长期记忆痛点。 |
| [TencentCloud/TencentDB-Agent-Memory](https://github.com/TencentCloud/TencentDB-Agent-Memory) | ⭐318 today | 四层渐进式本地长期记忆方案，零外部 API，专为 Agent 设计，今日登榜。 |
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | 80k | 将代码、SQL、文档等自动转化为可查询的知识图谱，赋能 RAG 的知识结构化。 |

## 3. 趋势信号分析

今日 GitHub 热榜呈现三个鲜明趋势：

1. **Agent 基础设施“三件套”日臻成熟**。  
   `TencentDB-Agent-Memory`（记忆）、`CubeSandbox`（安全沙箱）、`agent-skills`（技能库）三者同日登榜，标志着社区对 Agent 生产化所需的**持久记忆、安全执行、可组合能力**三大组件形成共识。这种“基建化”倾向将降低开发复杂 Agent 的门槛。

2. **办公与多媒体自动化场景迎来“AI 原生工具”**。  
   `OfficeCLI` 一天涨星 1717，成为今日增速最快的项目。它让 Agent 无需传统 Office 就能原生读写文档，深挖办公自动化长尾需求。同时 `claude-video` 将视频理解简化为“下载→抽帧→转录→LLM 分析”的标准化流水线，视频 Agent 赛道开始爆发。

3. **向量数据库“嵌入式、轻量化”趋势凸显**。  
   阿里 `zvec` 主打“进程内、超快”，配合 `lancedb`、`orama` 等方案，向量检索正从独立的分布式服务向单进程嵌入演进。这适应了边缘计算、个人 AI 助手等低延迟、轻部署场景，也与 RAG 本地落地的需求吻合。

4. **提示词逆向工程热度不减**。  
   `system_prompts_leaks` 今日新增 1218 星，反映出开发者对“黑盒模型内部引导”的强烈好奇。此举虽存在法律风险，但客观上推动了 AI 透明性讨论，也间接暴露了各大模型 prompt 竞争的白热化。

## 4. 社区关注热点

- **📦 iOfficeAI/OfficeCLI**：首个为 AI Agent 打造的 Office 原生套件，单二进制部署即可读写 Word/Excel/PPT，有望成为 Agent 办公自动化的事实标准。
- **🎯 bradautomates/claude-video**：使 LLM 具备视频感知能力的轻量方案，适合自媒体分析、监控摘要、教育视频处理等场景。
- **🧠 TencentDB-Agent-Memory**：四层本地记忆机制（无外部 API），是解决 Agent 跨会话遗忘问题的实用方案，值得关注其与 langchain/mem0 的对比。
- **🔐 TencentCloud/CubeSandbox**：Agent 沙箱安全方案，使用 Rust 实现高性能并发隔离，对于运行不可信工具的 Agent 应用至关重要。
- **⚡ alibaba/zvec**：进程内向量数据库，性能极快，适合嵌入式场景（移动端、IoT），可能颠覆现有云端向量数据库的部署模式。

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*