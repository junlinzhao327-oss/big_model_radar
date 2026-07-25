# AI 开源趋势日报 2026-07-26

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-07-25 23:16 UTC

---

# AI 开源趋势日报（2026-07-26）

---

## 1. 今日速览

- **Agent 工具链持续爆发**：今日 Trending 榜中近半数项目与 AI Agent 相关，从专用浏览器（`ego-lite`）到技能框架（`superpowers`、`skills`）再到性能优化系统（`ECC`），社区正围绕 Agent 构建完整基础设施。
- **阿里巴巴开源企业级代码审查工具**：`alibaba/open-code-review` 首次登榜，融合 LLM Agent 与确定性管线的混合架构，首日即获 439 星，表明企业级 AI 工具需求旺盛。
- **金融垂直领域模型与工具涌现**：`shiyu-coder/Kronos` 发布金融市场基础模型，`palmier-io/palmier-pro` 打造 AI 原生视频编辑器——AI 正在快速渗透高价值行业。
- **RAG 生态成熟度继续提升**：`dify`、`RAGFlow`、`anything-llm` 等主流项目保持高热度，同时新项目如 `turbovec`（向量索引）和 `LEANN`（极省存储）展示了技术迭代方向。

---

## 2. 各维度热门项目

### 🔧 AI 基础工具 (框架 / SDK / 推理引擎 / 开发工具 / CLI)

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [andrewyng/aisuite](https://github.com/andrewyng/aisuite) | 0 (+75 today) | 吴恩达出品，统一接口对接多个生成式 AI 提供商，降低切换成本。 |
| [alibaba/open-code-review](https://github.com/alibaba/open-code-review) | 0 (+439 today) | 阿里开源的混合架构代码审查工具，LLM Agent + 确定性规则，已在内部大规模验证。 |
| [citrolabs/ego-lite](https://github.com/citrolabs/ego-lite) | 0 (+986 today) | 专为 AI Agent 设计的极速浏览器，可将已登录会话共享给 Codex、Claude Code 等。 |
| [RyanCodrai/turbovec](https://github.com/RyanCodrai/turbovec) | 0 (+89 today) | Rust 实现的向量索引库，基于 TurboQuant 量化，Python 绑定，主打轻量高性能。 |
| [obra/superpowers](https://github.com/obra/superpowers) | 0 (+507 today) | Agent 技能开发框架与方法论，帮助开发者用标准模式构建可复用 Agent 能力。 |
| [ollama/ollama](https://github.com/ollama/ollama) | ⭐176,883 | 本地运行大模型的一站式工具，支持主流开源模型，社区生态最活跃。 |
| [huggingface/transformers](https://github.com/huggingface/transformers) | ⭐162,975 | 业界标准模型库，支持文本、视觉、音频多模态，训练与推理全覆盖。 |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | ⭐87,147 | 高性能 LLM 推理引擎，内存优化设计，已成为部署首选。 |

### 🤖 AI 智能体 / 工作流 (Agent 框架 / 自动化 / 多智能体)

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | ⭐233,286 (+364 today) | Agent 性能优化系统，面向 Claude Code、Codex 等 CLI 工具，集成技能、记忆、安全。 |
| [mattpocock/skills](https://github.com/mattpocock/skills) | 0 (+1,743 today) | 知名工程师的 Agent 技能集合，直接 `.agents` 目录发布，可快速复用。 |
| [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) | 0 (+574 today) | Claude 技能精选列表，涵盖工具、资源和自定义工作流，拓展 Claude 能力边界。 |
| [anthropics/claude-cookbooks](https://github.com/anthropics/claude-cookbooks) | 0 (+144 today) | 官方 Claude 使用示例集合，展示创意且高效的 Agent 调用方式。 |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | ⭐220,436 | 可成长 Agent 框架，强调与用户的长期交互与自我进化。 |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | ⭐185,684 | 早期 Agent 先驱，持续迭代，提供通用自主任务执行能力。 |
| [browser-use/browser-use](https://github.com/browser-use/browser-use) | ⭐106,761 | 让 AI Agent 能像人类一样操作网页，自动化在线任务。 |
| [CopilotKit/CopilotKit](https://github.com/CopilotKit/CopilotKit) | ⭐36,276 | 前端 Agent 栈，支持 React / Angular / 移动端等，构建生成式 UI。 |

### 📦 AI 应用 (具体产品 / 垂直场景解决方案)

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [shiyu-coder/Kronos](https://github.com/shiyu-coder/Kronos) | 0 (+319 today) | 专为金融市场语言训练的基础模型，探索 AI 在量化交易中的能力。 |
| [OtterMind/Chat2DB](https://github.com/OtterMind/Chat2DB) | 0 (+364 today) | AI 驱动的数据库客户端，支持多种数据库，自然语言查询生成 SQL。 |
| [palmier-io/palmier-pro](https://github.com/palmier-io/palmier-pro) | 0 (+346 today) | macOS 原生 AI 视频编辑器，集成 AI 辅助剪辑、特效生成。 |
| [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) | ⭐99,280 | 一键生成高清短视频，AI 大模型 + 自动化工作流，内容创作利器。 |
| [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) | ⭐58,795 | LLM 驱动的多市场股票智能分析系统，支持定时运行与自动推送。 |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | ⭐48,984 | 全能 AI 生产力工作室，集成智能对话、自主 Agent 与 300+ 助手。 |

### 🧠 大模型 / 训练 (模型 / 训练框架 / 微调 / 评估)

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [Lordog/dive-into-llms](https://github.com/Lordog/dive-into-llms) | 0 (+405 today) | 《动手学大模型》编程实践教程，适合从零开始系统学习 LLM。 |
| [jingyaogong/minimind](https://github.com/jingyaogong/minimind) | ⭐53,841 | 2 小时从零训练 64M 参数小 LLM 的教程，降低大模型学习门槛。 |
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | ⭐7,236 | 综合性 LLM 评估平台，支持 100+ 评测集与主流模型。 |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | ⭐4,407 | 面向系统工程师的 LLM 推理服务课程，在 Apple Silicon 上构建迷你 vLLM。 |

### 🔍 RAG / 知识库 (向量数据库 / 检索增强 / 知识管理)

| 项目 | Stars | 一句话说明 |
|------|-------|------------|
| [langgenius/dify](https://github.com/langgenius/dify) | ⭐150,239 | 领先的 RAG + Agent 构建平台，支持可视化工作流与企业级部署。 |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | ⭐85,990 | 深度 RAG 引擎，融合 Agent 能力，为 LLM 提供优质上下文层。 |
| [Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm) | ⭐63,836 | 本地优先的全能 Agent 体验，支持文档管理、多模型切换。 |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | ⭐61,676 | 通用 AI 记忆层，为 Agent 提供持久化上下文管理。 |
| [StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN) | ⭐12,728 | 极省存储的 RAG 方案，降低 97% 存储成本，论文发表于 MLSys2026。 |
| [VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex) | ⭐34,555 | 无向量推理的 RAG 方案，基于文档索引与逻辑推理。 |
| [milvus-io/milvus](https://github.com/milvus-io/milvus) | ⭐45,382 | 高性能云原生向量数据库，支撑大规模向量 ANN 搜索。 |
| [qdrant/qdrant](https://github.com/qdrant/qdrant) | ⭐33,585 | 下一代向量搜索引擎，高性能 + 云原生，提供云服务。 |

---

## 3. 趋势信号分析

**Agent 生态加速成熟：** 今日 Trending 榜中有 5 个以上项目直接服务于 Agent 开发与运行（`ego-lite`、`superpowers`、`skills`、`ECC`、`awesome-claude-skills`），合计获星超过 4,600。社区已从“Agent 能做什么”转向“如何高效开发、部署和优化 Agent”。`mattpocock/skills` 日增 1,743 星，表明顶级工程师开始公开分享自己的 Agent 工作流，极有可能成为 Agent 技能的“标准包管理器”雏形。

**“AI Agent 浏览器”概念首次登榜：** `citrolabs/ego-lite` 提出“为 AI Agent 重新设计浏览器”，解决 Agent 自动化中 cookie、session 共享等痛点，首日近千星，预示 Agent 专用基础设施赛道打开。

**企业级 AI 工具开源化：** `alibaba/open-code-review` 展示了大型科技公司内部工具开源的意愿，其“确定性规则 + LLM Agent”的混合架构可能成为行业代码审查的新范式。

**金融与创作垂直场景受追捧：** `Kronos`（金融基础模型）和 `palmier-pro`（AI 视频编辑器）同时上榜，结合此前 `MoneyPrinterTurbo` 的热度，可见 AI 正从通用助手走向行业深度应用，尤其是高价值、数据密集领域。

**RAG 存储效率成为新焦点：** `LEANN` 在 MLSys2026 发表后获 12.7k 星，提出极端存储节省方案；`turbovec` 通过量化降低向量索引资源消耗。社区在关注性能的同时，开始更重视成本与隐私（本地部署）。

---

## 4. 社区关注热点

- **⭐ `mattpocock/skills` — 日增 1,743 星**：TypeScript 类型专家 Matt Pocock 公开自己的 Agent 技能目录，可能成为 Agent 技能社区的“Recipe”模板，建议开发者关注其文件结构与管理方式。
- **⭐ `citrolabs/ego-lite` — 日增 986 星**：AI Agent 专用浏览器，解决网页自动化中的状态共享难题，与 `browser-use` 互补，有望成为 Agent 核心组件。
- **⭐ `alibaba/open-code-review` — 日增 439 星**：企业级代码审查开源方案，展示 LLM 与确定性规则结合的最佳实践，适合希望提升开发流程的团队研究。
- **⭐ `StarTrail-org/LEANN` — 总量 12.7k 星**：97% 存储节省的 RAG 方案，为资源受限设备（手机、边缘端）上运行 RAG 提供了新思路，值得关注其技术细节。
- **⭐ `andrewyng/aisuite` — 吴恩达新项目**：虽然今日新增仅 75 星，但出自 AI 权威之手，统一接口降低多 Provider 切换成本，有望成为 LLM 应用的“标准适配层”，早期参与者有优势。

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*