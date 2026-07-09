# AI 开源趋势日报 2026-07-10

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-09 23:40 UTC

---

# AI 开源趋势日报（2026-07-10）

## 今日速览

- **AI Agent 与 Claude 生态爆发**：多个专为 Claude / Claude Code 设计的工具登顶 Trending，如 `ai-job-search`（今日 +3728⭐）、`agent-skills`（+2582⭐）、`DesktopCommanderMCP`，显示社区正围绕 Anthropic 的 Claude 生态构建大量生产力套件。
- **“Agent 工作流”基础设施成主流**：`OfficeCLI`、`crawl4ai`、`claude-video` 等项目专注于让 AI Agent 能独立操作办公文档、抓取网页、理解视频，Agent 的“超能力”正在快速商品化。
- **提示词工程向“反向工程”延伸**：`system_prompts_leaks` 以 +1135⭐ 冲上热榜，社区对主流闭源模型的系统提示拆解需求旺盛，暗示提示词审计与安全研究成为新热点。
- **端侧推理与 TTS 持续升温**：`pocket-tts`（CPU 可运行的高质量 TTS）印证了小型化、本地化 AI 模型的趋势；同时 `vllm`、`picollm` 等推理框架在主题搜索中保持高星。
- **知识库 / RAG 赛道稳健扩张**：`anything-llm`（63k⭐）、`llama_index`（50k⭐）、`ragflow`（84k⭐）等经典项目持续迭代，新项目 `LEANN`（12k⭐）以 97% 存储节省的极端优化切入边缘设备。

---

## 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

| 项目 | Stars | 说明 |
|------|-------|------|
| [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) | +2582 today | 生产级 AI 编码 Agent 技能库，使 agent 具备工程级能力，开箱即用。 |
| [iOfficeAI/OfficeCLI](https://github.com/iOfficeAI/OfficeCLI) | +1923 today | 首个专为 AI Agent 设计的 Office 自动化 CLI，单文件无依赖，无需安装 Office。 |
| [unclecode/crawl4ai](https://github.com/unclecode/crawl4ai) | ⭐ +195 today | LLM 友好的开源网络爬虫/抓取库，支持结构化输出，方便 RAG 与 agent 直接使用。 |
| [wonderwhy-er/DesktopCommanderMCP](https://github.com/wonderwhy-er/DesktopCommanderMCP) | +185 today | 为 Claude 提供的 MCP 服务器，赋予终端控制、文件搜索与差异编辑能力，是 agent 扩展关键组件。 |
| [anthropics/claude-cookbooks](https://github.com/anthropics/claude-cookbooks) | +347 today | 官方 Claude 使用指南与 Jupyter 示例，涵盖多模态、函数调用等实用场景。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | ⭐ 85,836 | 高吞吐、内存高效的 LLM 推理引擎，已成为生产部署标配，近期持续优化多模态支持。 |
| [Picovoice/picollm](https://github.com/Picovoice/picollm) | ⭐ 315 | 端侧 LLM 推理库，采用 X-Bit 量化，可在树莓派等设备上运行，适合边缘 AI 场景。 |

### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

| 项目 | Stars | 说明 |
|------|-------|------|
| [vxcontrol/pentagi](https://github.com/vxcontrol/pentagi) | +543 today | 全自主 AI Agent 系统，可独立完成渗透测试任务，代表 Agent 在安全领域的深度应用。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | ⭐ 212,189 | 自进化 Agent 框架，支持长期记忆与技能学习，社区热度极高。 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | ⭐ 48,372 | 集成智能聊天、自主 Agent 与 300+ 预设助手的 AI 生产力工作室，统一接口接入主流 LLM。 |
| [zhayujie/CowAgent](https://github.com/zhayujie/CowAgent) | ⭐ 45,898 | 开源超级 AI 助手与 Agent 框架（原 chatgpt-on-wechat），支持多模型、工具调用与记忆演化。 |
| [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit) | ⭐ 35,880 | 前端 Agent 与生成式 UI 开发栈，支持 React、Angular 等框架，推动 Agent 交互 UI 化。 |
| [langgenius/dify](https://github.com/langgenius/dify) | ⭐ 148,332 | 生产级 Agent 工作流开发平台，低代码编排复杂流程，已成为企业级 RAG/Agent 首选。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | ⭐ 103,970 | 让 AI Agent 拥有浏览器操作能力，自动化网页任务，是 Agent 实现“数字劳动”的关键基础设施。 |

### 📦 AI 应用（具体产品、垂直场景解决方案）

| 项目 | Stars | 说明 |
|------|-------|------|
| [MadsLorentzen/ai-job-search](https://github.com/MadsLorentzen/ai-job-search) | +3728 today | AI 求职框架：自动评估岗位、定制简历、写求职信、模拟面试，全流程自动化。 |
| [bradautomates/claude-video](https://github.com/bradautomates/claude-video) | +727 today | 让 Claude 能“观看”任意视频：自动下载、抽帧、转录并交给 Claude 分析。 |
| [kyutai-labs/pocket-tts](https://github.com/kyutai-labs/pocket-tts) | +273 today | 在 CPU 上即可运行的高质量文本转语音模型，适合本地离线部署。 |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | ⭐ 38,017 | 根据文档自动生成可编辑的 PowerPoint，支持原生图表、动画及语音旁白，AI 办公又一力作。 |
| [TauricResearch/TradingAgents](https://github.com/TauricResearch/TradingAgents) | ⭐ 92,050 | 多 Agent LLM 金融交易框架，模拟不同策略 Agent 协作交易，代表 AI 在量化金融的前沿。 |
| [Shubhamsaboo/awesome-llm-apps](https://github.com/Shubhamsaboo/awesome-llm-apps) | ⭐ 117,060 | 100+ 可运行的 AI Agent & RAG 应用集合，新手快速上手的宝藏仓库。 |

### 🧠 大模型/训练（模型权重、训练框架、微调工具）

| 项目 | Stars | 说明 |
|------|-------|------|
| [ollama/ollama](https://github.com/ollama/ollama) | ⭐ 175,826 | 本地运行 LLM 的标杆工具，现已支持 Kimi、GLM、DeepSeek 等多款国产模型，持续带动本地推理。 |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | ⭐ 185,445 | 早期自主 Agent 标杆，虽热度略降，但仍是理解 Agent 架构的经典参考。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | ⭐ 7,180 | 大规模 LLM 评测平台，支持 100+ 模型，是选型与基准测试的权威工具。 |
| [galilai-group/stable-pretraining](https://github.com/galilai-group/stable-pretraining) | ⭐ 281 | 轻量、可靠的基础模型预训练库，面向世界模型与大规模预训练，适合研究者。 |
| [asgeirtj/system_prompts_leaks](https://github.com/asgeirtj/system_prompts_leaks) | +1135 today, ⭐ 55,124 | 系统性提取并公开主流 AI 产品（Claude、ChatGPT、Gemini 等）的系统提示词，用于模型行为研究与安全审计。 |

### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

| 项目 | Stars | 说明 |
|------|-------|------|
| [Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm) | ⭐ 63,011 | 本地优先的全能 LLM 代理，支持文档索引、多模型切换，是个人/团队私有 RAG 首选。 |
| [run-llama/llama_index](https://github.com/run-llama/llama_index) | ⭐ 50,751 | 领先的文档 Agent 与 OCR 平台，提供 RAG 全链路能力。 |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | ⭐ 84,699 | 融合 RAG 与 Agent 能力的高性能引擎，提供企业级检索增强生成。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | ⭐ 45,154 | 云原生高性能向量数据库，支撑大规模 ANN 搜索。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | ⭐ 60,497 | 通用 AI Agent 记忆层，实现跨会话持久化上下文，与 RAG 互补。 |
| [StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN) | ⭐ 12,662 | MLsys2026 论文项目：97% 存储节省的私有 RAG，可在个人设备上运行。 |
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | ⭐ 81,260 | 将代码、文档、视频等任意文件夹转化为可查询知识图谱，赋能 coding agent。 |

---

## 趋势信号分析

1. **Agent 生态重心从“对话”转向“工具执行”**：今日热榜上，`OfficeCLI`、`DesktopCommanderMCP`、`crawl4ai` 等不再是单纯的聊天机器人，而是让 Agent 直接操作操作系统、Office 软件、浏览器的底层工具。这标志着 AI Agent 正从“建议者”进化为“执行者”，对自动化办公、测试、渗透等场景有颠覆性影响。

2. **Claude 生态一枝独秀**：在 Trending 中，6/11 的 AI 项目直接或间接基于 Claude（`ai-job-search`、`agent-skills`、`DesktopCommanderMCP`、`claude-cookbooks`、`claude-video`、`system_prompts_leaks`）。这暗示 Anthropic 的 Claude 模型和 Claude Code 工具链正成为社区创新的主要承载平台，其开放的 API 和 MCP 协议吸引大量开发者。

3. **系统提示词泄漏成新安全研究热点**：`system_prompts_leaks` 仓库今日新增超 1000⭐，且总星数已超 5.5 万，说明业界对模型行为审计、提示词注入防御的需求急升。这一方向可能催生新的安全工具链。

4. **端侧 AI 与 TTS 走向实用**：`pocket-tts` 在 CPU 上运行，`picollm` 面向边缘设备，`LEANN` 主打本地存储节省——小模型+本地化成为降低推理成本、保障隐私的主流方案，且技术成熟度已达到产品级。

5. **招聘与金融两大垂直场景被 AI 重塑**：`ai-job-search`（求职）和 `TradingAgents`（金融交易）分别刷新热度，说明 AI 不再是泛化工具，而是聚焦高价值业务流程的自动化。尤其是求职场景，AI 全流程介入（评估→简历→面试）正在改变求职方式。

---

## 社区关注热点

- **🤖 Claude Code 生态工具链**：`ai-job-search`、`DesktopCommanderMCP`、`claude-video` 展示了如何扩展 Claude Code 的能力边界，推荐开发者关注 MCP 协议的应用开发。
- **📋 系统提示词泄露与安全**：`system_prompts_leaks` 揭示了模型内部行为，不仅是逆向工程，更可帮助开发者和企业理解自家产品的提示词设计风险，建议安全团队重点跟进。
- **⚡ 轻量化 RAG 与边缘推理**：`pocket-tts` 与 `LEANN` 代表“低资源高回报”的技术趋势，适合在手机、笔记本甚至 IoT 设备上部署 AI 应用，是普惠 AI 的关键路径。
- **💼 AI 驱动的办公自动化**：`OfficeCLI` 和 `ppt-master` 展示了 AI 直接操作 Word / Excel / PowerPoint 的能力，这比传统宏/VBA 更智能灵活，将极大提升办公效率。
- **🔗 多 Agent 协作框架崛起**：`TradingAgents`、`pentagi` 以及 `CherryHQ` 都在探索多 Agent 协同完成复杂任务，建议关注如何设计 Agent 间通信、信任与任务分解的架构模式。

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*