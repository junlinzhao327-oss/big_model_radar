# AI 官方内容追踪报告 2026-09-12

> 今日更新 | 新增内容: 232 篇 | 生成时间: 2026-09-11 22:35 UTC

数据来源:
- Anthropic: [anthropic.com](https://www.anthropic.com) — 新增 14 篇（sitemap 共 443 条）
- OpenAI: [openai.com](https://openai.com) — 新增 218 篇（sitemap 共 959 条）

---

# AI 官方内容追踪报告  
**追踪日期：2026-09-12｜增量范围：Anthropic 14 篇、OpenAI 218 条**

> **数据说明与核验提示**  
> 1. Anthropic 本次 14 篇内容正文可提取，但其中多篇为历史研究/报告的官网索引更新，原文日期跨度从 2024 到 2026。下文同时标注“官网索引更新日”和“原文日期”。  
> 2. OpenAI 本次 218 条新内容正文均无法提取，且重复率很高，很多为 `/index`、`/news` 导航页。因此 OpenAI 部分只能基于标题、URL、分类和发布节奏做“标题级信号分析”，**不能视为已核验的正式公告全文**。  
> 3. 下文对 OpenAI 的判断均加“标题显示/若属实则”限定，建议后续以官网正文和 release note 复核。

---

## 1. 今日速览

1. **Anthropic 今日增量明显偏向“社会影响、经济测量、安全红队与政策叙事”**：最值得关注的是 Frontier Red Team 关于 AI 在战术情报 targeting 和常规武器开发中的能力评估，以及 Claude Corps、Economic Index、AI Fluency、Claude 价值跨模型/语言差异等研究集中出现。  
2. **OpenAI 今日抓取量异常庞大，达 218 条，但正文缺失、重复严重**。标题层面显示其内容矩阵覆盖 GPT-5、GPT-5.4/5.5/5.6、GPT-6 Astra、GPT Live、Rosalind、Aardvark、Daybreak、Codex Security、ChatGPT Health/金融/广告/Atlas、Agents API、数据驻留、零留存、年龄预测、Lockdown Mode 等，产品与安全合规并行扩张。  
3. **竞争态势上，OpenAI 更像在定义“模型代际 + 超级 App + 企业平台 + 开发者生态”的节奏**；Anthropic 则继续强化“可信 AI、社会经济影响、独立研究、国家安全与军事滥用评估”的差异化议题领导权。  
4. **安全与合规成为双方共同高频主题**：Anthropic 关注军事/情报 targeting、越狱、可解释性；OpenAI 标题密集出现网络安全、生物防御、青少年安全、年龄预测、家长控制、Bug Bounty、供应链攻击、数据主权与零数据留存。  
5. **对开发者和企业的直接影响**：代理 API/SDK、Codex Security、GPT Live/语音、ChatGPT Apps、企业数据驻留、零留存、广告商业化、健康/金融/教育垂直化，都会改变集成方式、合规边界和模型选型周期。

---

## 2. Anthropic / Claude 内容精选

### 2.1 News / 政策与有益部署

#### 1. Introducing Claude Corps  
- **官网索引更新：2026-09-11；原文日期：2026-06-11**  
- Anthropic 推出国家 fellowship 项目 Claude Corps，计划培训 1,000 名早期职业人士，匹配美国非营利组织，全职工作一年，初始承诺 1.5 亿美元。  
- 这是 Anthropic 将“AI 红利广泛分享”落到政策与劳动力市场干预层面的动作，与 AI 对就业冲击的政策框架配套。  
- 战略上，它把 Claude 生态从模型/API 扩展到“人才、非营利、社区部署”。  
- 链接：[Introducing Claude Corps](https://www.anthropic.com/news/claude-corps)

### 2.2 Frontier Red Team / 安全与军事风险

#### 2. Measuring AI capabilities in intelligence targeting and conventional weapons  
- **官网索引更新：2026-09-11；原文日期：2026-09-10**  
- Anthropic Frontier Red Team 发布新评估，衡量模型在战术情报 targeting（如根据碎片信息定位人员）和常规武器开发（如无人机打击移动目标）中的能力。  
- 文中指出，部分军事/情报任务上，模型已能做到历史上只有稀缺、高度训练的人类专家才能完成的事情；PRC 开源权重模型虽落后前沿，但仍展现出识别/ targeting 对手和提升武器性能的令人担忧能力。  
- Anthropic 同时强调平台侧分类器等安全措施的必要性，用于阻断此类滥用。  
- 这是本次增量中最具战略敏感性的研究：AI 安全评估正从网络安全、生物风险扩展到常规军事与情报 kill chain。  
- 链接：[Measuring AI capabilities in intelligence targeting and conventional weapons](https://www.anthropic.com/research/intelligence-targeting-conventional-weapons-capabilities)

### 2.3 Societal Impacts / 社会影响、价值、教育与独立研究

#### 3. How Claude’s values vary by model and language  
- **官网索引更新：2026-09-11；原文日期：2026-07-13**  
- 研究将 Claude 对话中 3,000 多个价值压缩为少数“价值轴”，例如情感温暖 vs 严谨，以测量不同模型和语言下 Claude 表达价值的差异。  
- 这是 Anthropic 对“Claude 宪法无法覆盖所有日常价值判断”的实证回应，试图把价值对齐从原则文本推进到可测量维度。  
- 对多语言产品、全球合规和区域价值观差异有直接影响。  
- 链接：[How Claude’s values vary by model and language](https://www.anthropic.com/research/claude-values-models-languages)

#### 4. Enabling independent research on how people use Claude  
- **官网索引更新：2026-09-11；原文日期：2026-08-26**  
- Anthropic 分享外部研究者访问聚合真实 Claude 使用数据的试点结果，三家研究机构通过 Anthropic Insights 设计研究，Anthropic 代为收集数据，研究者独立分析。  
- 文中指出，当前真实 AI 使用数据集中在少数实验室，公共数据集又偏向休闲使用，不足以支撑独立研究。  
- 这延续了 Anthropic 在“隐私保护 + 外部研究开放”上的治理叙事，也可能影响未来 AI 经济、社会影响研究的证据标准。  
- 链接：[Enabling independent research on how people use Claude](https://www.anthropic.com/research/enabling-independent-research)

#### 5. Anthropic Education Report: The AI Fluency Index  
- **官网索引更新：2026-09-11；原文日期：2026-02-23**  
- AI Fluency Index 通过数千个匿名 Claude.ai 对话，测量 11 类可观察行为，判断用户是否在发展“AI 协作能力”。  
- 初步发现，最常见的 AI fluency 表现是“增强型”：把 AI 当作思考伙伴，而非单纯委托工具。  
- 该指标把教育研究从“使用率”推进到“使用质量”，对教育产品、企业培训和 AI 素养政策有参考价值。  
- 链接：[Anthropic Education Report: The AI Fluency Index](https://www.anthropic.com/research/AI-fluency-index)

#### 6. Education Report: How educators use Claude  
- **官网索引更新：2026-09-11；原文日期：2025-08-27**  
- 分析约 74,000 条高等教育专业人士的匿名 Claude.ai 对话，并与东北大学合作访谈教师。  
- 教师用 Claude 开发课程材料、写基金申请、学术 advising、招生和财务规划等行政任务，也用 Artifacts 创建化学模拟、自动评分 rubric、数据看板。  
- 核心信号：教育场景中，AI 先自动化“苦差事”，而非直接替代教学判断。  
- 链接：[Education Report: How educators use Claude](https://www.anthropic.com/research/anthropic-education-report-how-educators-use-claude)

### 2.4 Anthropic Economic Index 系列

#### 7. Introducing the Anthropic Economic Index  
- **官网索引更新：2026-09-11；原文日期：2025-02-10**  
- Anthropic 启动 Economic Index，基于数百万匿名 Claude.ai 对话分析 AI 对劳动市场影响，并开源数据集。  
- 初期发现：使用集中在软件开发和技术写作；约 36% 职业至少四分之一任务出现 AI 使用，约 4% 职业在四分之三任务中使用；57% 为增强，43% 为自动化。  
- 这是 Anthropic 建立“AI 经济影响公共数据基础设施”的起点。  
- 链接：[Introducing the Anthropic Economic Index](https://www.anthropic.com/research/the-anthropic-economic-index)

#### 8. Anthropic Economic Index: Insights from Claude 3.7 Sonnet  
- **官网索引更新：2026-09-11；原文日期：2025-03-27**  
- 报告观察到 Claude 3.7 Sonnet 发布后，编码、教育、科学、医疗使用份额上升；extended thinking 主要用于技术任务。  
- 首次按任务和职业发布 augmentation/automation 分解，例如 copywriter/editor 更多任务迭代，translator/interpreter 更偏 directive。  
- 这说明 Anthropic 将模型能力变化与职业任务结构变化直接挂钩。  
- 链接：[Anthropic Economic Index: Insights from Claude 3.7 Sonnet](https://www.anthropic.com/research/anthropic-economic-index-insights-from-claude-sonnet-3-7)

#### 9. Anthropic Economic Index: AI’s impact on software development  
- **官网索引更新：2026-09-11；原文日期：2025-04-28**  
- 分析 50 万条编码相关交互，比较 Claude.ai 与 Claude Code。  
- Claude Code 中 79% 对话被识别为 automation，而 Claude.ai 仅 49%；说明专用编码 agent 更偏向直接执行任务。  
- 这对理解 agent 产品对软件工程工作流的替代/增强边界非常关键。  
- 链接：[Anthropic Economic Index: AI’s impact on software development](https://www.anthropic.com/research/impact-software-development)

#### 10. Economic Index: AI’s role in the US and global economy  
- **官网索引更新：2026-09-11；原文日期：2025-09-15**  
- 第三份经济指数报告扩展到美国各州和全球国家差异，提供美国州级 AI 使用首次详细评估。  
- 软件工程几乎在各地领先，但区域偏好明显：马萨诸塞更偏科研，巴西更偏翻译和语言学习，夏威夷偏旅行规划。  
- 信号：AI 采用不是均匀扩散，而是与地方经济结构强相关。  
- 链接：[Economic Index: AI’s role in the US and global economy](https://www.anthropic.com/research/economic-index-geography)

#### 11. Economic Index: New building blocks for AI use  
- **官网索引更新：2026-09-11；原文日期：2026-01-15**  
- 第四份报告提出“economic primitives”：任务复杂度、技能水平、用途（工作/教育/个人）、AI 自主性、成功。  
- 这些基础测量作为 AI 经济影响的领先指标，可支持更复杂的工作变化分析。  
- 这代表 Anthropic 正把 Economic Index 从描述性统计升级为可复用测量框架。  
- 链接：[Economic Index: New building blocks for AI use](https://www.anthropic.com/research/economic-index-primitives)

#### 12. Anthropic Economic Index report: Cadences  
- **官网索引更新：2026-09-11；原文日期：2026-06-26**  
- 报告指出 Claude Code 和 Cowork 使 Claude 会话越来越多是长时 agentic 任务，传统聊天记录不再能完整反映使用方式。  
- 方法论更新包括更高比例采样、小时级使用模式、新输出分类器，并区分 chat、Cowork、1P API。  
- 还纳入 2026 年 4 月启动的 Anthropic Economic Index Survey，研究用户对 AI 改变工作与机会的感知。  
- 链接：[Anthropic Economic Index report: Cadences](https://www.anthropic.com/research/economic-index-june-2026-report)

### 2.5 Alignment / Interpretability

#### 13. Many-shot jailbreaking  
- **官网索引更新：2026-09-11；原文日期：2024-04-02**  
- Anthropic 研究“many-shot jailbreaking”：利用长上下文窗口，通过大量特定配置文本迫使 LLM 输出潜在有害响应。  
- 该技术对 Anthropic 和其他公司模型均有效，Anthropic 提前通知其他开发者并部署缓解措施。  
- 这是长上下文能力带来新型安全漏洞的早期标志性研究。  
- 链接：[Many-shot jailbreaking](https://

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*