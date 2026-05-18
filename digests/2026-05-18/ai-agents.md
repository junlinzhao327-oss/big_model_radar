# OpenClaw 生态日报 2026-05-18

> Issues: 500 | PRs: 500 | 覆盖项目: 12 个 | 生成时间: 2026-05-18 01:56 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Zeroclaw](https://github.com/zeroclaw-labs/zeroclaw)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyclaw)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [EasyClaw](https://github.com/gaoyangz77/easyclaw)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报（2026-05-18）

---

## 1. 今日速览

OpenClaw 社区活跃度持续高位运行，过去24小时内共产生 **500条 Issues 更新**（新开/活跃：472，已关闭：28）和 **500条 PR 更新**（待合并：448，已合并/关闭：52），显示出强劲的开发与问题反馈节奏。项目在 **Mac 应用体验优化、安全审计机制增强、多平台支持扩展** 等方面取得实质性进展。同时，围绕 **API 密钥泄露防护、会话状态稳定性、跨通道消息路由可靠性** 的讨论热度居高不下，反映出用户对生产环境可用性与安全性的高度关注。

---

## 2. 版本发布

### 新版本：`v2026.5.16-beta.6`（最新）、`v2026.5.16-beta.5`、`v2026.5.16-beta.4`

#### 主要更新内容：
- **Mac 应用设置页全面重构**：采用统一卡片布局，优化导航缓存机制，清理权限、语音、技能、定时任务、执行与调试面板的视觉与交互一致性，并改善侧边栏间距稳定性。
- **技能命名规范化**：将本地 Codex 关闭审查技能及其辅助组件重命名为 `autoreview`，提升语义清晰度。
- **安全审计增强**（v2026.5.16-beta.4）：引入 `security.audit.suppressions` 配置项，允许开发者标记“已知可接受”的安全审计发现项，使其从活跃摘要中隐藏但仍保留在 JSON 输出中并附带抑制说明（#76949，感谢 @100menotu001）。
- **子代理标签化**：为委托执行的子代理添加明确标签，提升调试与追踪能力。

> ⚠️ **无破坏性变更**，但建议用户检查自定义技能是否依赖旧版 Codex 审查相关命名。

---

## 3. 项目进展

今日合并/关闭的重要 PR 聚焦于 **稳定性修复与基础设施加固**：

- **#83350（已合并）**：修复旧版包升级路径中的配置元数据写入问题，避免候选版本 `doctor` 检查期间配置损坏（@giodl73-repo）。
- **#83314（已合并）**：修正迁移预览中隐藏配置冲突计数不准确的问题，确保敏感项统计可见性（@giodl73-repo）。
- **#83310（已合并）**：强制要求 `update --timeout` 参数必须为完整正整数，拒绝 `1.5` 或 `10abc` 等非法格式，提升 CLI 健壮性（@giodl73-repo）。
- **#82966（已合并）**：修复 `resolveFreshSessionTotalTokens` 在数据过期时错误返回 `undefined` 的问题，解决 `/context` 命令与控制台上下文计量器频繁显示“不可用”的异常（@njuboy11）。

此外，多个高优先级 PR 进入深度审查阶段，如 #79925（上下文压力感知续接机制）、#81729（移除系统事件信任元数据）等，预示下一阶段将强化自主代理调度能力与安全性隔离。

---

## 4. 社区热点

### 🔥 高讨论度 Issues（附链接）：

| Issue | 评论数 | 核心诉求 |
|------|--------|--------|
| [#75 Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75) | 104 | 强烈呼吁补齐 Linux 与 Windows 原生客户端，实现与 macOS 同等功能覆盖 |
| [#25592 工具调用间文本泄露至消息通道](https://github.com/openclaw/openclaw/issues/25592) | 26 | 内部处理输出（如错误日志、确认语）不应作为用户可见消息发送，属严重 UX 缺陷 |
| [#9443 请求预编译 Android APK 发布](https://github.com/openclaw/openclaw/issues/9443) | 24 | 用户希望 GitHub Releases 提供可直接安装的 APK，而非仅源码 |
| [#10659 屏蔽式密钥管理（Masked Secrets）](https://github.com/openclaw/openclaw/issues/10659) | 12 | 防止代理直接读取原始 API 密钥，防范提示注入攻击导致凭证泄露 |

> 📌 分析：用户需求集中于 **跨平台可访问性** 与 **敏感信息保护机制**，反映出 OpenClaw 正从开发者工具向企业级协作平台演进。

---

## 5. Bug 与稳定性

### 🔴 高严重性 Bug（按优先级排序）：

| Issue | 类型 | 状态 | 说明 |
|------|------|------|------|
| [#43661 会话在压缩超时时无限挂起并重复发消息](https://github.com/openclaw/openclaw/issues/43661) | P1 / 消息丢失 / 死循环 | 🔧 有相关 PR #81621 | 压缩失败触发静默重试循环，需紧急修复 |
| [#44905 Discord 泄露内部工具调用痕迹](https://github.com/openclaw/openclaw/issues/44905) | P1 / 安全风险 / 消息污染 | ⏳ 无 fix PR | `NO_REPLY`、`to=functions` 等调试信息外泄 |
| [#22676 SIGUSR1 重启时信号守护进程竞争条件](https://github.com/openclaw/openclaw/issues/22676) | P1 / 崩溃循环 | ⏳ 无 fix PR | 旧进程未退出即启动新实例，导致端口/文件锁冲突 |
| [#45494 Cron 作业在 LLM API 持续故障时静默超时](https://github.com/openclaw/openclaw/issues/45494) | P1 / 数据丢失 | ⏳ 无 fix PR | 应快速失败而非耗尽 180s 超时窗口 |

> ✅ 已有关键修复推进：#81621 正解决子代理提前完成导致的会话状态漂移问题。

---

## 6. 功能请求与路线图信号

### 🚀 高潜力功能（已有 PR 或强烈社区呼声）：

| 功能 | 关联 Issue/PR | 状态 |
|------|---------------|------|
| **Webhook 多轮会话支持**（sessionKey 复用） | [#11665](https://github.com/openclaw/openclaw/issues/11665) | 🔄 长期未解，需维护者决策 |
| **技能级模型路由**（per-skill model field） | [#43260](https://github.com/openclaw/openclaw/issues/43260) | 💡 明确需求，适合中低复杂度模型分流 |
| **预响应强制钩子**（硬网关规则） | [#13583](https://github.com/openclaw/openclaw/issues/13583) | ⚠️ 高价值但需安全评审 |
| **Telegram Business Bot 支持** | [#20786](https://github.com/openclaw/openclaw/issues/20786) | 👍 5 点赞，企业场景刚需 |
| **MathJax/LaTeX 渲染支持** | [#42840](https://github.com/openclaw/openclaw/issues/42840) | 🎯 科学计算用户强烈需求 |

> 📊 判断：**技能级模型路由** 与 **Telegram Business 支持** 最可能纳入下一版本，因实现成本可控且需求明确。

---

## 7. 用户反馈摘要

### 💬 真实用户声音提炼：

- **痛点**：
  - “Android 只有源码，每次都要自己编译，太麻烦了”（#9443）
  - “代理突然在 Slack 里发一堆 `to=functions.memory_search`，吓我一跳”（#44905）
  - “内存管理完全乱套，我和同事的存储方式都不一样”（#43747）
  - “API 密钥明文存在 `.env` 里，根本不敢上生产”（#11829）

- **满意点**：
  - Mac 设置页 redesign 获普遍好评，“终于不像 beta 软件了”
  - 安全审计抑制功能被赞“专业级合规支持”

- **使用场景**：
  - 企业用户通过 Cron + Webhook 实现日报自动生成（#11665）
  - 开发者用 Browser Tool 做跨站点自动化注册测试（#44431）

---

## 8. 待处理积压

### ⏳ 长期未响应重要事项（需维护者关注）：

| Issue/PR | 创建日期 | 标签 | 说明 |
|----------|----------|------|------|
| [#75 Linux/Windows 客户端缺失](https://github.com/openclaw/openclaw/issues/75) | 2026-01-01 | `P2` + `help wanted` | 超 4 个月未分配，影响生态完整性 |
| [#23096 Bitwarden/Vaultwarden 密钥集成](https://github.com/openclaw/openclaw/pull/23096) | 2026-02-22 | `stale` | 安全增强型 PR，停滞近 3 个月 |
| [#19482 仅在新工作区生成 HEARTBEAT.md](https://github.com/openclaw/openclaw/pull/19482) | 2026-02-17 | `needs-real-behavior-proof` | 小但重要的 UX 修复，长期 pending |
| [#63919 编码工具接入 HTTP /tools/invoke API](https://github.com/openclaw/openclaw/pull/63919) | 2026-04-09 | `needs-real-behavior-proof` | 文档承诺功能未实现，易引发用户困惑 |

> 🔔 **建议**：优先 review #23096（密钥管理）与 #63919（API 一致性），二者均涉及核心安全与功能完整性。

--- 

**报告生成时间**：2026-05-18  
**数据来源**：OpenClaw GitHub Repository（github.com/openclaw/openclaw）

---

## 横向生态对比

# 个人 AI 助手/自主智能体开源生态横向对比分析报告  
**报告时间：2026-05-18**

---

## 1. 生态全景

当前个人 AI 助手与自主智能体开源生态呈现**高活跃度、强分化、快迭代**的态势。核心项目如 OpenClaw、Zeroclaw、NanoClaw 等日均产生数百条 Issues 与 PR，反映出开发者对生产级可用性与安全性的迫切需求。跨平台支持（Linux/Windows/Android）、密钥安全治理、多模型兼容性及 MCP 工具链集成成为全行业共性痛点。同时，项目间技术路线显著分化：部分聚焦轻量化边缘部署（如 PicoClaw），部分押注企业级多代理架构（如 Zeroclaw v0.8.0），另一些则深耕垂直场景集成（如 IronClaw 的 Web3 签名、CoPaw 的钉钉/微信通道）。

---

## 2. 各项目活跃度对比

| 项目 | Issues 更新数 | PR 更新数 | 新版本发布 | 健康度评估 |
|------|---------------|-----------|-------------|-------------|
| **OpenClaw** | 500 | 500 | ✅ v2026.5.16-beta.6 | ⭐⭐⭐⭐⭐（高活跃，强修复力） |
| **NanoBot** | 8 | 18 | ❌ | ⭐⭐⭐⭐☆（稳健迭代，部署优化中） |
| **Zeroclaw** | 20 | 50 | ❌ | ⭐⭐⭐⭐☆（高修复密度，v0.8.0 在即） |
| **PicoClaw** | 12 | 9 | ✅ nightly | ⭐⭐⭐☆☆（用户驱动，边缘场景聚焦） |
| **NanoClaw** | 10 | 21 | ❌ | ⭐⭐⭐⭐☆（CLI/容器修复高效） |
| **IronClaw** | 9 | 46 | ❌ | ⭐⭐⭐☆☆（架构重构期，回归 Bug 多） |
| **LobsterAI** | 0 | 9 | ❌ | ⭐⭐⭐☆☆（低 Issue，PR 持续优化） |
| **Moltis** | 2 | 5 | ✅ 20260517.03 | ⭐⭐⭐⭐☆（远程访问扩展成功） |
| **CoPaw** | 19 | 13 | ❌ | ⭐⭐☆☆☆（高 Bug 密度，稳定性承压） |
| **TinyClaw / ZeptoClaw / EasyClaw** | 0 | 0 | ❌ | ⭐☆☆☆☆（无近期活动） |

> 注：健康度综合考量活跃度、Bug 响应速度、版本节奏与社区反馈质量。

---

## 3. OpenClaw 在生态中的定位

OpenClaw 是当前生态中**唯一实现全功能覆盖 + 高频发布 + 企业级安全特性**的核心参照项目。其优势体现在：
- **社区规模**：单日 500+ Issues/PR，远超同类（次高为 Zeroclaw 的 70 条），反映广泛采用；
- **技术路线**：坚持“渐进式稳定”策略，beta 版本每周迭代，同时引入安全审计抑制、子代理标签化等生产级特性；
- **差异化**：相比 NanoBot 侧重部署简化、PicoClaw 专注边缘设备，OpenClaw 明确面向**多平台企业协作场景**，提供 Mac 设置页重构、跨通道消息路由等完整 UX 解决方案。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|--------|--------|--------|
| **跨平台客户端支持** | OpenClaw (#75)、PicoClaw (#28)、NanoBot (#3876) | 补齐 Linux/Windows 原生应用；Android APK 预编译发布；WebUI 远程访问 |
| **API 密钥安全防护** | OpenClaw (#10659)、IronClaw (Gmail token 泄露)、NanoClaw (#2520) | 屏蔽式密钥管理；日志脱敏；防提示注入泄露 |
| **多模型推理兼容** | Zeroclaw (#6059, #6672)、Moltis (#1007)、LobsterAI (#762) | 支持 DeepSeek/Qwen/Gemma 的 `reasoning_content` 结构化输出；自动检测 API 格式 |
| **MCP 工具链稳定性** | NanoClaw (#2208)、CoPaw (#3640)、OpenClaw (#25592) | 避免工具调用泄露至用户消息；支持 HTTP/SSE 传输；防止会话状态漂移 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|------|--------|--------|----------------|
| **OpenClaw** | 企业级多代理协作 | 团队开发者、运维人员 | 统一配置中心 + 安全审计层 + 多通道路由 |
| **Zeroclaw** | 多代理运行时 + 自主认知 | 高级开发者、AI 研究员 | v0.8.0 多代理调度 + Dream Mode 记忆整理 |
| **PicoClaw** | 边缘设备本地推理 | 个人用户、Termux/Android 开发者 | 轻量级 MCP 集成 + LM Studio 易连接 |
| **IronClaw** | Web3 + TEE 安全代理 | 区块链开发者、隐私敏感用户 | Reborn 架构 + WASM 多链签名 |
| **CoPaw** | 国内 IM 通道集成 | 中国企业用户 | 钉钉/微信/飞书深度适配 + 技能市场 |
| **Moltis** | 远程协作 + 外部代理持久化 | 分布式团队 | NetBird/Cloudflare Tunnel 集成 + ACP 会话保持 |

---

## 6. 社区热度与成熟度

- **快速迭代阶段**：OpenClaw、Zeroclaw、NanoClaw —— 日均 PR >20，Bug 修复周期 <24h，功能发布密集；
- **质量巩固阶段**：NanoBot、LobsterAI、Moltis —— 聚焦性能优化（SQLite 异步写入）、文档对齐、部署可靠性；
- **架构转型期**：IronClaw（Reborn 重构）、CoPaw（安全测试覆盖）—— 功能冻结倾向明显，优先解决回归问题；
- **边缘创新点**：PicoClaw（SiliconFlow 原生支持）、Moltis（Gemma 推理标签）—— 探索国产模型与新兴协议适配。

---

## 7. 值得关注的趋势信号

1. **安全合规成为准入壁垒**：  
   OpenClaw 的 `security.audit.suppressions`、CoPaw 的 RCE 漏洞报告、NanoClaw 的日志泄露问题，表明**生产环境部署必须内置安全审计与密钥隔离机制**。

2. **“配置即代码”（Configuration-as-Code）兴起**：  
   IronClaw #3036、OpenClaw 技能命名规范化、Zeroclaw 配置一致性修复，显示项目正从“UI 配置”向**可编程、版本化配置**演进。

3. **国产模型生态加速整合**：  
   PicoClaw（SiliconFlow）、Zeroclaw（DeepSeek/Kimi）、LobsterAI（自动格式检测）均加强中文模型支持，**非 OpenAI 兼容接口的适配能力将成为竞争力关键**。

4. **MCP 协议向分布式扩展**：  
   NanoClaw 的 HTTP/SSE 支持、Moltis 的外部代理会话持久化，预示**工具调用将从本地 Stdio 走向云原生微服务架构**。

> **对开发者的建议**：优先选择具备活跃安全响应机制（如 OpenClaw）、明确跨平台路线图（如 Zeroclaw）、且支持多模型推理结构化的项目；在集成第三方工具时，务必评估其日志安全与密钥管理实现。

---  
**分析师备注**：生态整体向“企业级可用”迈进，但稳定性与安全性仍是最大瓶颈。建议开发者关注 OpenClaw 与 Zeroclaw 的下一版本发布，二者将定义 2026 下半年个人 AI 助手的技术基线。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报（2026-05-18）

---

## 1. 今日速览

NanoBot 社区活跃度维持高位，过去24小时内共产生 **8条 Issues 更新** 和 **18条 PR 更新**，其中 **9个 PR 被合并/关闭**，表明开发节奏紧凑且协作高效。尽管无新版本发布，但多个关键功能优化与 Bug 修复已落地，涵盖 WebUI、CLI、Docker 部署、内存管理及模型支持等核心模块。社区对部署文档一致性与 WebUI 可访问性问题的关注显著上升，反映出用户向生产环境迁移的实际需求增强。

---

## 2. 版本发布

**无新版本发布**。当前最新稳定版本仍为 `v0.2.0`，建议用户关注即将发布的 `v0.2.1` 或 nightly 构建以获取近期修复。

---

## 3. 项目进展

今日共 **9个 PR 被合并或关闭**，推动多项关键改进：

- **WebUI 与 CLI 体验优化**：  
  - [#3877](https://github.com/HKUDS/nanobot/pull/3877) 优化流式响应渲染与长会话同步，提升 WebUI 响应性能；  
  - [#3878](https://github.com/HKUDS/nanobot/pull/3878) 修复 CLI 中推理 token 逐行输出问题，改善可读性。

- **系统稳定性增强**：  
  - [#3881](https://github.com/HKUDS/nanobot/pull/3881) 解决 AutoCompact 与 Consolidator 并发写入 session 导致的竞态条件，避免数据损坏风险。

- **部署与文档一致性修复**：  
  - [#3874](https://github.com/HKUDS/nanobot/pull/3874) 对齐 `docker run` 示例与 `docker-compose.yml` 配置；  
  - [#3875](https://github.com/HKUDS/nanobot/pull/3875) 补充 WebUI Docker 配置要求与 bwrap 安全标志说明，解决 #3873 报告的多项部署障碍。

- **构建与兼容性修复**：  
  - [#3870](https://github.com/HKUDS/nanobot/pull/3870)、[#3872](https://github.com/HKUDS/nanobot/pull/3872) 修复 Docker 构建失败问题，确保容器化部署可行性。

- **国际化与错误处理**：  
  - [#3864](https://github.com/HKUDS/nanobot/pull/3864) 将中文“访问量过大”识别为可重试的瞬态错误，提升中国用户 LLM 调用稳定性。

> 整体来看，项目在 **用户体验、系统健壮性、部署可靠性** 三方面取得实质性进展。

---

## 4. 社区热点

**最活跃 Issue：[#3790](https://github.com/HKUDS/nanobot/issues/3790)**（WebUI 会话内容显示错乱）  
- **评论数：14**，**👍：0**，持续 4 天未解决  
- 用户反馈升级至 `0.1.5.post3.2026.05.13` 后，WebUI 打印内容错乱，需手动刷新恢复。  
- **背后诉求**：WebUI 实时性体验受损，影响日常使用，亟需前端渲染逻辑修复。

**高关注度功能请求：[#3876](https://github.com/HKUDS/nanobot/issues/3876)**（WebUI bootstrap 仅限 localhost 访问）  
- 用户指出 Docker 部署下 WebUI 完全不可达，因 `/webui/bootstrap` 拒绝非本地连接。  
- **信号**：强烈需求支持远程访问，可能推动下一版网络策略重构。

---

## 5. Bug 与稳定性

按严重程度排序：

| 严重性 | Issue | 描述 | 是否有 Fix PR |
|--------|------|------|----------------|
| ⚠️ 高 | [#3857](https://github.com/HKUDS/nanobot/issues/3857) | Bootstrap 失败，HTTP 500 错误，网关运行但前端无法访问 | ❌ 无（但 #3875 部分缓解） |
| ⚠️ 高 | [#3790](https://github.com/HKUDS/nanobot/issues/3790) | WebUI 会话内容显示错乱，需刷新恢复 | ❌ 无（#3877 已优化流式渲染，可能间接缓解） |
| ⚠️ 中 | [#3884](https://github.com/HKUDS/nanobot/issues/3884) | WebUI 对话在首次响应后自动关闭 | ❌ 无 |
| ⚠️ 中 | [#3863](https://github.com/HKUDS/nanobot/issues/3863) | 微信登录失败，提示“版本过低”（即使已更新） | ❌ 无（#3882 已关闭，协议升级待合并） |
| ⚠️ 低 | [#3873](https://github.com/HKUDS/nanobot/issues/3873) | Docker 部署文档与实际配置不一致 | ✅ 已修复（#3874、#3875） |

> 建议优先处理 #3857 和 #3790，二者直接影响核心功能可用性。

---

## 6. 功能请求与路线图信号

以下功能请求具备高采纳可能性，已有对应 PR 或明确技术路径：

- **Dream 系统作业全局开关**（[#3885](https://github.com/HKUDS/nanobot/issues/3885)）  
  → 用户希望禁用记忆整理后台任务，PR 尚未提交但设计清晰，易实现。

- **BM25-lite 技能路由**（[#3865](https://github.com/HKUDS/nanobot/pull/3865)）  
  → 减少系统提示 token 消耗达 60%，性能优化显著，已进入 review 阶段。

- **MiniMax 图像生成支持**（[#3879](https://github.com/HKUDS/nanobot/pull/3879)）  
  → 扩展多模态能力，适配中国主流 AI 服务商，符合生态趋势。

- **CLI 模型配置管理命令**（[#3883](https://github.com/HKUDS/nanobot/pull/3883)）  
  → 提升运维效率，降低配置门槛，实用性高。

> 预计上述功能将纳入 **v0.2.1 或 v0.3.0** 版本。

---

## 7. 用户反馈摘要

- **痛点**：  
  - Docker 部署流程复杂，文档与实际脱节（#3873）；  
  - WebUI 在容器内无法远程访问（#3876）；  
  - 微信渠道协议陈旧，登录失败（#3863）；  
  - 多轮对话中技能内容丢失（#3847 提及）。

- **满意点**：  
  - CLI 推理 token 显示优化后更清晰（#3878 合并后）；  
  - 长任务目标状态同步至 WebUI 提升可观测性（#3788）。

- **使用场景**：  
  用户多用于 **Linux 服务器部署 + WebUI 远程管理**，强调稳定性与可维护性，对“开箱即用”体验要求高。

---

## 8. 待处理积压

| 类型 | 编号 | 标题 | 创建时间 | 状态 | 提醒 |
|------|------|------|----------|------|------|
| Issue | [#3790](https://github.com/HKUDS/nanobot/issues/3790) | WebUI 会话内容显示错乱 | 2026-05-14 | OPEN | 高优先级，影响核心体验，需前端团队介入 |
| Issue | [#3863](https://github.com/HKUDS/nanobot/issues/3863) | 微信不能 Login | 2026-05-16 | OPEN | 协议升级 PR (#3882) 已关闭但未合并，需跟进 |
| PR | [#3847](https://github.com/HKUDS/nanobot/pull/3847) | 引入 skill_load 工具防止技能内容丢失 | 2026-05-15 | OPEN | 关键功能，长期未 review，建议加速处理 |
| PR | [#2060](https://github.com/HKUDS/nanobot/pull/2060) | Shell 工具支持可配置路径白名单 | 2026-03-15 | OPEN | 积压超 2 个月，安全相关，应评估合并 |

> 建议维护者优先处理 **#3790** 与 **#3847**，二者分别代表用户体验与功能完整性的关键瓶颈。

---  
*数据截止：2026-05-18 00:00 UTC*  
*来源：NanoBot GitHub Repository (HKUDS/nanobot)*

</details>

<details>
<summary><strong>Zeroclaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# Zeroclaw 项目动态日报（2026-05-18）

---

## 1. 今日速览

Zeroclaw 项目在2026年5月18日继续保持高活跃度，社区与核心团队协同推进多项关键修复与架构演进。过去24小时内共产生 **20条 Issues 更新**（16条新开/活跃，4条关闭）和 **50条 PR 更新**（40条待合并，10条已合并/关闭），显示出强烈的开发动能和问题响应速度。尽管无新版本发布，但多个高风险 Bug 已定位并提交修复 PR，尤其在 **provider 兼容性、cron 调度一致性、内存初始化稳定性** 等核心模块取得实质性进展。项目整体处于 **高迭代、高修复密度** 的健康状态，为 v0.8.0 多代理运行时版本的推进奠定基础。

---

## 2. 版本发布

**无新版本发布**。  
当前主干分支正聚焦于 v0.8.0 版本的集成测试与关键缺陷修复（见 PR #6398），预计将在近期进入 Beta 阶段。

---

## 3. 项目进展

今日有 **10个 PR 被合并或关闭**，重点推进了以下方向：

- **关键 Bug 修复**：
  - 修复了 Windows 平台下 cron 任务因硬编码 `sh` 导致的“program not found”错误（#6705 → 已关闭），相关修复 PR #6740、#6741 已提交，统一时区处理逻辑。
  - 解决了 Matrix 通道中 tool-call 协议数据泄漏至用户可见消息的问题（#6734），修复中。
  - 修复了 SQLite 内存模块在并发启动时的 schema 初始化失败问题（#6431 → 已关闭）。

- **CI/CD 与工具链稳定性**：
  - 修复了自 #6396 以来从未成功运行的 `pr-title` 工作流（#6751），通过替换 `amannn/action-semantic-pull-request` 为内联正则检查（PR #6752）实现快速绕过权限限制。
  - 优化了 Windows 快照 TTL 配置，避免轮询间隔短于缓存有效期导致的竞态（PR #6750）。

- **配置与运行时健壮性**：
  - 修复了 OpenAI provider 忽略 `timeout_secs` 配置而硬编码 120s 超时的问题（#6723）。
  - 修复了 `MemoryConfig.rerank_enabled` 字段声明但未消费的问题（#6722）。

> 整体项目在 **跨平台兼容性、配置一致性、CI 可靠性** 方面迈出关键步伐，为后续多代理架构上线扫清障碍。

---

## 4. 社区热点

### 🔥 最活跃 Issue：#6059 — DeepSeek-V4 API 格式不兼容（9条评论，4👍）
- **链接**：https://github.com/zeroclaw-labs/zeroclaw/issues/6059
- **分析**：用户报告在使用 DeepSeek-V4-Pro/Flash 模型时，因“thinking mode”导致 `reasoning_content` 缺失而触发 400 错误。该问题影响 S2 级别功能降级，且涉及主流大模型厂商兼容性，**反映出项目对非标准 OpenAI 兼容接口的适配能力不足**。维护者已标记为 `in-progress`，预计将推动 provider 层抽象改进。

### 🔥 高优先级回归：#6672 — Xiaomi 模型 reasoning_content 未在工具调用循环中回传（S0 严重性）
- **链接**：https://github.com/zeroclaw-labs/zeroclaw/issues/6672
- **分析**：在 agentic tool-call 多轮交互中，`reasoning_content` 丢失导致后续轮次无法获取完整上下文，属数据完整性风险。此问题暴露了 **thinking mode 在多轮对话中的状态管理缺陷**，亟需修复。

---

## 5. Bug 与稳定性

| 严重程度 | Issue | 描述 | 修复状态 |
|--------|------|------|--------|
| **S0** | #6672 | reasoning_content 在工具调用循环中丢失 | 🔧 修复中（in-progress） |
| **S1** | #6705 | Windows 上 cron 因硬编码 `sh` 失败 | ✅ 已关闭，修复 PR #6740/#6741 |
| **S1** | #5600 | kimi-code provider 流式调用报错（thinking 启用但 reasoning_content 缺失） | 🔧 修复中 |
| **S2** | #6059 | DeepSeek-V4 API 格式不兼容 | 🔧 修复中 |
| **S2** | #6734 | Qwen 3.6 tool-call 数据泄漏至 Matrix 消息 | 🔧 修复中 |
| **S2** | #6733 | Matrix 流式草稿状态仅按 room 键控，导致并发冲突 | 🔧 修复中 |

> 当前无未响应的崩溃级（S0）问题，所有高风险 Bug 均已进入处理流程。

---

## 6. 功能请求与路线图信号

- **Dream Mode 内存 consolidation 功能**（PR #6693）进入开发阶段，支持周期性本地记忆整理与可选 LLM 反思，**预示 v0.8.0 将向“自主认知演进”方向演进**。
- **技能管理 UX 改进**（#6253）被标记为 `accepted`，结合 PR #6667 引入 background review fork 机制，**表明项目正强化技能生态的可维护性与作者体验**。
- **移除 skill audit 中 remote-markdown-link 拦截**（#6714）提议获关注，反映社区对 **降低第三方技能集成门槛** 的强烈需求。
- **官方文档网站构建**（#5994）已关闭，但内容需求明确，预计将作为 v0.8.0 发布配套资源推进。

> 综合判断：**v0.8.0 将聚焦“多代理运行时 + 技能生态成熟度 + 配置一致性”三大支柱**。

---

## 7. 用户反馈摘要

- **痛点**：
  - “使用 DeepSeek-V4 时频繁报错，thinking 模式根本无法启用”（#6059）
  - “Windows 上 cron 完全不可用，文档没提需要 Git Bash”（#6705）
  - “Matrix 消息里突然冒出 JSON 工具调用数据，体验很差”（#6734）
- **满意点**：
  - “v0.8.0 的 multi-agent 设计终于让复杂工作流跑起来了”（PR #6398 评论）
  - “skill_manage 工具让技能调试效率提升很多”（PR #6667 反馈）
- **使用场景**：
  - 企业级自动化（cron + MCP 工具链）
  - 多模型混合推理（DeepSeek/Qwen/OpenAI 切换）
  - 跨平台部署（Windows/Linux/macOS 服务化）

---

## 8. 待处理积压

| Issue/PR | 类型 | 创建时间 | 状态 | 提醒 |
|--------|------|--------|------|------|
| #6074 | Issue | 2026-04-24 | `in-progress` | **审计类任务积压**：需恢复 153 个被误回滚的提交，涉及功能与修复，建议分配资源专项处理 |
| #6253 | Issue | 2026-05-01 | `accepted` | **技能 UX 路线图协调器**：虽被接受，但缺乏明确 milestone 和 owner，易成“僵尸 tracker” |
| #6398 | PR | 2026-05-05 | `open` | **v0.8.0 主干 PR**：已开放近两周，需核心维护者尽快 review 并决策合并节奏，避免阻塞下游 |

> 建议维护者优先处理 #6074 和 #6398，二者分别代表**历史债务清理**与**未来版本基石**，对项目健康度影响深远。

---  
**数据来源**：Zeroclaw GitHub 仓库（截至 2026-05-18 23:59 UTC）  
**分析师备注**：项目处于快速迭代期，建议加强自动化测试覆盖（尤其 provider 兼容性矩阵）以支撑多模型生态扩展。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报（2026-05-18）

---

## 1. 今日速览

PicoClaw 社区活跃度保持高位，过去24小时内共产生 **12条 Issues 更新** 和 **9条 PR 更新**，涵盖功能增强、Bug 修复与文档优化。项目发布了一个 nightly 版本（`v0.2.8-nightly.20260518.0df050ff`），反映持续集成节奏稳定。社区对 **SiliconFlow 原生支持** 和 **工具策略细粒度控制** 的需求显著上升，同时多个长期 Bug 被关闭，表明核心稳定性正在改善。整体项目处于积极迭代与用户驱动演进的健康状态。

---

## 2. 版本发布

### 🔧 Nightly Build: `v0.2.8-nightly.20260518.0df050ff`
- **类型**：自动化 nightly 构建（非稳定版）
- **说明**：本次构建基于 main 分支最新提交，包含近期合并的功能与修复，但可能存在未暴露的回归问题。
- **变更范围**：见 [Full Changelog](https://github.com/sipeed/picoclaw/compare/v0.2.8...main)，主要包括：
  - 新增 SiliconFlow 提供商支持（#2885）
  - 聊天界面详情可见性选择器（#2886）
  - `load_image` 工具配置逻辑修复（#2888）
  - 文档更新（微信二维码修正，#2889）
- **⚠️ 注意**：此为开发预览版，不建议生产环境使用；用户若测试新功能请备份配置。

---

## 3. 项目进展

今日共 **3个 PR 被合并/关闭**，推动多项关键改进：

| PR | 类型 | 进展说明 |
|----|------|--------|
| [#2889](https://github.com/sipeed/picoclaw/pull/2889) | 文档更新 | 修正微信二维码，提升社区沟通渠道准确性 |
| [#2833](https://github.com/sipeed/picoclaw/pull/2833) | 功能增强 | 实现 Web/API 层真实连通性验证，提升 MCP 服务器连接可靠性 |
| [#2462](https://github.com/sipeed/picoclaw/pull/2462) | Bug 修复 | 修复 Codex 流式输出异常及 Telegram 重复重试问题，增强多通道稳定性 |

此外，两个重要功能 PR（[#2885](https://github.com/sipeed/picoclaw/pull/2885)、[#2886](https://github.com/sipeed/picoclaw/pull/2886)）虽未合并但已开放，预示下一版本将显著提升用户体验与提供商兼容性。

---

## 4. 社区热点

### 🔥 最活跃 Issue：[#28](https://github.com/sipeed/picoclaw/issues/28) —— *Feat Request: LM Studio Easy Connect*
- **评论数**：19 | **👍 反应数**：2
- **诉求分析**：用户强烈希望简化 LM Studio 的接入流程，尤其在 Android 设备上部署困难。该需求反映 PicoClaw 在**边缘设备与本地推理集成**方面的使用场景扩展，属于“易用性”与“本地 AI 生态兼容”交叉痛点。
- **潜在影响**：若实现，将大幅降低非技术用户使用本地模型的门槛。

### 🔥 高关注度 PR：[#2885](https://github.com/sipeed/picoclaw/pull/2885) —— *Add SiliconFlow provider support*
- **背景**：用户 @myourscom 在 Issue [#2884](https://github.com/sipeed/picoclaw/issues/2884) 中提出 SiliconFlow 仅能通过 OpenAI 兼容模式接入，配置繁琐。
- **进展**：已有完整 PR 提交，实现 SiliconFlow 作为一级提供商，支持原生 API 配置。
- **意义**：响应中文 AI 开发者对国产模型平台（如 SiliconFlow）的深度集成需求，增强项目在中国市场的适用性。

---

## 5. Bug 与稳定性

| Issue | 严重程度 | 状态 | 是否有 Fix PR |
|------|--------|------|-------------|
| [#1042](https://github.com/sipeed/picoclaw/issues/1042) —— `exec` 工具路径误判 | ⚠️ 中 | Open | ❌ 无（但逻辑问题明确） |
| [#2887](https://github.com/sipeed/picoclaw/issues/2887) —— RISC-V `.deb` 包无法使用 OpenAI 模型 | ⚠️ 中 | Open | ❌ 无（平台兼容性问题） |
| [#2878](https://github.com/sipeed/picoclaw/issues/2878) —— `load_image` 无法通过 `config.json` 配置 | ✅ 低 | Open | ✅ 有（[#2888](https://github.com/sipeed/picoclaw/pull/2888) 已提交修复） |
| [#2839](https://github.com/sipeed/picoclaw/issues/2839) —— 最终回复错误编辑占位消息 | ⚠️ 中 | Open | ❌ 无（影响多通道 UX） |

> **注**：[#2749](https://github.com/sipeed/picoclaw/issues/2749)、[#2745](https://github.com/sipeed/picoclaw/issues/2745)、[#1297](https://github.com/sipeed/picoclaw/issues/1297) 等 Bug 已于今日关闭，显示核心路径稳定性提升。

---

## 6. 功能请求与路线图信号

以下功能请求具备高采纳可能性，已有对应 PR 或明确技术路径：

| 功能请求 | Issue | 对应 PR | 采纳可能性 |
|--------|------|--------|----------|
| SiliconFlow 原生支持 | [#2884](https://github.com/sipeed/picoclaw/issues/2884) | [#2885](https://github.com/sipeed/picoclaw/pull/2885) | ⭐⭐⭐⭐☆（PR 已就绪） |
| AGENT.md 前端工具策略过滤 | [#2837](https://github.com/sipeed/picoclaw/issues/2837) | [#2838](https://github.com/sipeed/picoclaw/pull/2838) | ⭐⭐⭐☆☆（设计清晰，待 review） |
| 聊天详情可见性控制 | — | [#2886](https://github.com/sipeed/picoclaw/pull/2886) | ⭐⭐⭐⭐☆（UI/UX 改进，低风险） |
| LM Studio 易连接 | [#28](https://github.com/sipeed/picoclaw/issues/28) | — | ⭐⭐☆☆☆（需架构调整，暂无 PR） |

> **预测**：SiliconFlow 支持与聊天 UI 改进极可能进入 v0.2.9 正式版。

---

## 7. 用户反馈摘要

- **痛点**：
  - 非技术用户在 Android/Termux 环境部署困难（#28）
  - 国产模型平台（如 SiliconFlow）配置不便，依赖 OpenAI 兼容层（#2884）
  - 多通道下消息渲染不一致，如 Telegram 占位符被错误编辑（#2839）
  - RISC-V 架构支持薄弱，.deb 包功能异常（#2887）

- **满意点**：
  - 社区响应迅速，多个历史 Bug 被关闭（如 #1297、#2745）
  - MCP 服务器 OAuth 支持提案（#2546）获认可，体现对安全集成的重视
  - 工具安全 guard 机制虽有问题，但用户认可其设计初衷（#1042）

- **使用场景**：
  - 本地 AI 代理（LM Studio + Android）
  - 国产云模型接入（SiliconFlow）
  - 多通道部署（Discord/Telegram/OneBot）
  - 多代理协作与工具权限隔离（#2837）

---

## 8. 待处理积压

以下 Issue/PR 长期未响应，建议维护者优先关注：

| 编号 | 类型 | 积压时长 | 建议动作 |
|------|------|--------|--------|
| [#28](https://github.com/sipeed/picoclaw/issues/28) | Enhancement | >3个月 | 评估 LM Studio 集成可行性，或提供配置指南 |
| [#1042](https://github.com/sipeed/picoclaw/issues/1042) | Bug | >2个月 | 审查 `guardCommand` 正则逻辑，避免误拦截合法命令 |
| [#2837](https://github.com/sipeed/picoclaw/issues/2837) | Feature | >1个月 | 推动 [#2838](https://github.com/sipeed/picoclaw/pull/2838) 进入 review 流程 |
| [#2839](https://github.com/sipeed/picoclaw/issues/2839) | Bug | >1周 | 分析 steering-chain 回复渲染逻辑，修复占位符污染 |

> 💡 **维护建议**：对标记为 `stale` 的 Issue（如 #2837、#2839）应主动沟通，避免社区贡献者流失。

--- 

**报告生成时间**：2026-05-18  
**数据来源**：PicoClaw GitHub Repository (github.com/sipeed/picoclaw)

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报（2026-05-18）

---

## 1. 今日速览

NanoClaw 社区活跃度显著上升，过去24小时内共产生 **10条 Issues 更新**（8条新开/活跃，2条关闭）和 **21条 PR 更新**（11条待合并，10条已合并/关闭），显示出高强度开发与问题响应节奏。尽管无新版本发布，但多个关键 Bug 修复已进入合并阶段，涵盖 CLI、容器权限、Signal 附件处理等核心模块。项目整体处于**高修复密度、快速迭代**状态，技术债清理与稳定性提升是当前重点。

---

## 2. 版本发布

**无新版本发布**。最新 Release 仍为历史版本，团队聚焦于底层 Bug 修复与架构优化，暂未推进正式版本迭代。

---

## 3. 项目进展

今日共 **10个 PR 被合并或关闭**，推动多项关键修复落地：

- **CLI 组管理稳定性增强**：  
  [#2526](https://github.com/nanocoai/nanoclaw/pull/2526) 修复了 `ncl groups delete` 因外键约束失败的问题，通过级联删除依赖行实现完整清理；  
  [#2510](https://github.com/nanocoai/nanoclaw/pull/2510) 解决了审批流程中添加目标后接收方 `inbound.db` 未同步的问题，确保消息路由可达。

- **容器安全与权限修复**：  
  [#2527](https://github.com/nanocoai/nanoclaw/pull/2527) 将主机补充组（supplementary groups）映射至 agent 容器，解决组权限文件访问失败问题（v2 移植）。

- **消息通道兼容性改进**：  
  [#2523](https://github.com/nanocoai/nanoclaw/pull/2523) 修复 Telegram 上 approval cards 无法送达的问题，统一 `transformOutboundText` 在 `ask_question` 和 `card` 路径的应用；  
  [#2529](https://github.com/nanocoai/nanoclaw/pull/2529) 实现 Signal 图像/PDF 附件 base64 内联传输，解决 agent 容器内无法访问主机路径的问题。

- **日志安全与监控增强**：  
  [#2521](https://github.com/nanocoai/nanoclaw/pull/2521) 在 XML 消息属性中增加 `from-channel` 和 `from-type`，提升多通道监控仪表盘的可视化能力。

> 整体来看，项目在**CLI 可靠性、跨容器通信、通道兼容性**三大方向取得实质性进展。

---

## 4. 社区热点

### 🔥 高关注度 Issue：双重消息投递（#2404）
- **链接**: [#2404](https://github.com/nanocoai/nanoclaw/issues/2404)  
- **讨论焦点**：当 agent 同时使用 `send_message` MCP 工具和 `<message>` 块时，消息被重复投递。  
- **背后诉求**：用户期望 MCP 工具与原生消息块行为一致，避免因架构分层（MCP 子进程 vs 主轮询循环）导致语义重复。此问题暴露了**跨进程消息协调机制缺失**，需设计统一输出管道。

### 💬 高互动 PR：MCP 多传输支持（#2208）
- **链接**: [#2208](https://github.com/nanocoai/nanoclaw/pull/2208)  
- **状态**：长期开放，近期更新  
- **意义**：支持 HTTP 和 SSE 作为 MCP 服务器传输层，突破 Stdio 限制，为远程工具调用铺路。社区对扩展性需求强烈，但需评估与现有会话管理的兼容性。

---

## 5. Bug 与稳定性

按严重程度排序：

| 严重性 | Issue | 描述 | 是否有 Fix PR |
|--------|------|------|----------------|
| 🔴 High | [#2525](https://github.com/nanocoai/nanoclaw/issues/2525) | `ncl groups delete` 因外键约束失败，无法删除非空组 | ✅ [#2526](https://github.com/nanocoai/nanoclaw/pull/2526) 已合并 |
| 🔴 High | [#2465](https://github.com/nanocoai/nanoclaw/issues/2465) | 审批流程添加目标后接收方 `inbound.db` 未更新 | ✅ [#2510](https://github.com/nanocoai/nanoclaw/pull/2510) 已合并 |
| 🟠 Medium | [#2528](https://github.com/nanocoai/nanoclaw/issues/2528) | Signal 图像/PDF 附件在 agent 容器中不可访问 | ✅ [#2529](https://github.com/nanocoai/nanoclaw/pull/2529) 已提交 |
| 🟠 Medium | [#2520](https://github.com/nanocoai/nanoclaw/issues/2520) | `nanoclaw.log` 泄露 Signal 协议私钥缓冲区 | ❌ 无 PR，需过滤日志输出 |
| 🟡 Low | [#2386](https://github.com/nanocoai/nanoclaw/issues/2386) | `ncl groups create` 生成违反 OneCLI 规则的 UUID | ❌ 无 PR，需改用合规标识符生成逻辑 |

> 注：[#2512](https://github.com/nanocoai/nanoclaw/issues/2512)（PostgreSQL 容器通信失败）已关闭，疑似环境问题。

---

## 6. 功能请求与路线图信号

- **CalDAV 工具集成**：  
  [#2530](https://github.com/nanocoai/nanoclaw/pull/2530) 提出 `/add-caldav-tool` 技能，支持日历同步，反映用户对**个人生产力集成**的需求上升。
  
- **CLI 模式替代 Agent SDK**：  
  [#2470](https://github.com/nanocoai/nanoclaw/pull/2470) 实现 `useCliMode` 配置，绕过 Agent SDK 使用交互式配额，暗示平台正探索**成本控制与配额优化**路径。

- **MCP 协议扩展**：  
  [#2208](https://github.com/nanocoai/nanoclaw/pull/2208) 对 HTTP/SSE 的支持表明项目正向**分布式工具调用架构**演进，可能为未来云原生部署做准备。

> 综合判断：**CLI 增强、MCP 协议扩展、个人工具集成**将成为下一阶段重点方向。

---

## 7. 用户反馈摘要

- **痛点**：
  - 多通道用户抱怨附件无法访问（Signal）、卡片消息丢失（Telegram），影响核心通信体验。
  - CLI 工具链不稳定，`groups create/delete` 存在数据一致性问题，导致部署失败。
  - 日志泄露敏感密钥引发安全担忧，尤其在自托管场景。

- **满意点**：
  - 快速响应：如 [#2525] 从报告到修复仅1天。
  - 多通道支持完善（Telegram/Discord/Signal/WhatsApp），用户赞赏跨平台能力。
  - 文档驱动开发（如 Finance Plan 3 系列 PR 附带详细 spec），提升可预测性。

---

## 8. 待处理积压

| Issue/PR | 类型 | 积压时长 | 说明 |
|--------|------|--------|------|
| [#2404](https://github.com/nanocoai/nanoclaw/issues/2404) | Bug | 8天 | 双重消息投递，影响 MCP 工具可信度，需架构级修复 |
| [#2386](https://github.com/nanocoai/nanoclaw/issues/2386) | Bug | 8天 | UUID 生成违反 OneCLI 规则，阻碍自动化部署 |
| [#2208](https://github.com/nanocoai/nanoclaw/pull/2208) | Feature | 15天 | MCP HTTP/SSE 支持，长期开放，需维护者 review |
| [#2520](https://github.com/nanocoai/nanoclaw/issues/2520) | Security | 1天 | 日志泄露密钥，需紧急处理 |

> ⚠️ 建议优先处理 **#2404（消息重复）** 和 **#2520（密钥泄露）**，二者分别影响功能正确性与安全性，属高优先级积压。

--- 

**报告生成时间**: 2026-05-18  
**数据来源**: GitHub Repository `nanocoai/nanoclaw`

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报（2026-05-18）

---

## 1. 今日速览

IronClaw 项目在过去24小时内保持**高活跃度**，共产生 **46 条 PR 更新**（含 14 条已合并/关闭）与 **9 条新 Issue**，无新版本发布。核心开发聚焦于 **Reborn 架构演进** 与 **工具链集成能力增强**，同时暴露出 v0.28.2 版本中多个影响用户体验的回归性 Bug。社区反馈集中指向 Gmail 工具授权流程与 TEE 代理配置界面异常，需优先修复。

---

## 2. 版本发布

**无新版本发布**。当前最新稳定版本仍为 v0.28.2，但该版本已引发多个关键回归问题（见第5节）。

---

## 3. 项目进展

今日有 **14 条 PR 被合并或关闭**，主要推动以下方向：

- **Reborn 架构深化**：  
  - [`#3695`](https://github.com/nearai/ironclaw/pull/3695)（已合并）完成 `ironclaw_reborn_composition` 作为统一组合根的改造，并交付可独立运行的 `ironclaw-reborn` 二进制文件，为后续配置即代码（#3036）打下基础。  
  - [`#3703`](https://github.com/nearai/ironclaw/pull/3703) 和 [`#3704`](https://github.com/nearai/ironclaw/pull/3704) 分别重构运行时接口以支持未来蓝图配置，并实现 TOML + JSON 配置文件启动机制，提升运维友好性。  
  - [`#3722`](https://github.com/nearai/ironclaw/pull/3722) 修复 provider 工具调用元数据在 Reborn 循环中的丢失问题，保障多轮对话一致性。

- **WebUI 与产品工作流增强**：  
  - [`#3721`](https://github.com/nearai/ironclaw/pull/3721) 引入运行 profile 对个人上下文的策略控制，支持更细粒度的隐私管理。  
  - [`#3725`](https://github.com/nearai/ironclaw/pull/3725) 绑定 WebUI 线程至调用者作用域，防止隐式线程创建导致的状态混乱。  
  - [`#3735`](https://github.com/nearai/ironclaw/pull/3735) 在 `RebornServicesApi` 暴露 `get_run_state` 方法，解耦前端路由与底层运行时依赖。

- **文档与测试完善**：  
  - [`#3723`](https://github.com/nearai/ironclaw/pull/3723)（已合并）清理过时规划文档，替换为基于 CLAUDE.md 的轻量级开发指南，提升新贡献者上手效率。

> 整体来看，项目正从“功能堆叠”向“架构稳定+可运维性”阶段过渡，Reborn 分支成为核心演进主线。

---

## 4. 社区热点

**最热讨论集中于 Gmail 工具链的授权与安装逻辑缺陷**，由 @sunglow666 连续提交 6 个高相关性 Bug Issue（[#3731](https://github.com/nearai/ironclaw/issues/3731) 至 [#3736](https://github.com/nearai/ironclaw/issues/3736)），揭示以下核心矛盾：

- 用户期望：一次授权后应持久生效，UI 应准确反映工具状态。
- 实际表现：重复提示安装、无效 token 显示成功、页面刷新后状态错乱、TEE 与非 TEE 环境行为不一致。

这些 Issue 虽暂无评论，但**问题密度高、复现路径清晰**，且涉及核心第三方集成能力，极可能影响用户信任度。维护者需紧急响应。

此外，**IronHub 工具动态安装功能**（[#3737](https://github.com/nearai/ironclaw/pull/3737)）作为新特性 PR 引发关注，支持 CLI 与运行时 agent 自主安装技能，标志着平台向“动态扩展生态”迈出关键一步。

---

## 5. Bug 与稳定性

以下为今日报告的 **高优先级回归性 Bug**（均基于 v0.28.2）：

| 严重程度 | Issue | 描述 | 是否有 Fix PR |
|--------|------|------|-------------|
| 🔴 **高** | [#3734](https://github.com/nearai/ironclaw/issues/3734) | 非 TEE 代理中推理提供商配置页缺失 API Key 输入与“获取模型”按钮（v0.28.1 正常） | ❌ 无 |
| 🔴 **高** | [#3736](https://github.com/nearai/ironclaw/issues/3736) | TEE 代理中为未配置凭证的提供商错误显示“Use”按钮，误导用户 | ❌ 无 |
| 🟠 **中** | [#3733](https://github.com/nearai/ironclaw/issues/3733) | 提交无效 Gmail token 后显示“激活成功” toast，实则未生效 | ❌ 无 |
| 🟠 **中** | [#3731](https://github.com/nearai/ironclaw/issues/3731) | Gmail 已安装但仍重复提示 `tool_install(gmail)` | ❌ 无 |
| 🟠 **中** | [#3729](https://github.com/nearai/ironclaw/issues/3729) | 拒绝 `tool_install` 后刷新页面错误显示为成功 | ❌ 无 |

> ⚠️ 所有问题均无对应修复 PR，建议维护团队优先分配资源处理 #3734 与 #3736，因其直接影响核心推理功能可用性。

---

## 6. 功能请求与路线图信号

- **IronHub 动态工具安装**（[#3737](https://github.com/nearai/ironclaw/pull/3737)）已进入开发阶段，表明“运行时技能市场”将成为下一阶段重点，契合 #3036 “Configuration-as-Code” 的长期愿景。
- **WASM 凭证签名支持**（[#3256](https://github.com/nearai/ironclaw/pull/3256)）引入 HMAC、EIP-712、NEP-413、Solana 等多链签名能力，反映项目正积极拓展 Web3 集成场景。
- **钩子框架（hooks）系列 PR**（[#3573](https://github.com/nearai/ironclaw/pull/3573) 及后续）虽多为草案，但释放出“可插拔安全策略引擎”的信号，未来可能支持自定义审批流与审计钩子。

---

## 7. 用户反馈摘要

从 Issues 内容提炼真实用户痛点：

- **配置体验割裂**：TEE 与非 TEE 环境 UI 行为不一致（#3734 vs #3736），导致运维困惑。
- **状态反馈不可信**：前端 toast 提示与实际后端状态脱节（#3733、#3729），削弱用户对系统的信任。
- **授权流程冗余**：Gmail 工具需多次确认安装，违背“一次授权，长期可用”的直觉（#3731、#3728）。
- **文档滞后于代码**：开发者抱怨旧版规划文档与当前架构不符（#3723 被主动清理印证此点）。

> 用户核心诉求：**一致性、可预测性、减少认知负担**。

---

## 8. 待处理积压

- **长期未决 E2E 测试失败**：[#3447](https://github.com/nearai/ironclaw/issues/3447)（自 2026-05-10 起 nightly E2E 持续失败）虽为 bot 报告，但超一周未修复，可能掩盖深层集成问题，建议排查 CI 环境或测试用例稳定性。
- **Reborn 组合根拆分跟踪**：[#3726](https://github.com/nearai/ironclaw/issues/3726) 提出对 `ironclaw_reborn_composition` 职责分离的审查需求，虽关联已合并 PR #3695，但仍需确认是否完全达成设计目标。

> 建议维护者优先处理 #3447，避免 nightly 失败演变为“狼来了”效应，影响发布信心。

--- 

**报告生成时间**：2026-05-18  
**数据来源**：GitHub IronClaw 仓库公开数据

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报（2026-05-18）

---

## 1. 今日速览

过去24小时内，LobsterAI 项目整体活跃度**中等偏低**：无新 Issue 提交，无新版本发布，但 Pull Request 更新频繁，共 9 条 PR 发生变动（7 条待合并，2 条已关闭）。社区贡献持续聚焦于**用户体验优化、性能提升与可观测性增强**，反映出项目处于功能迭代与稳定性打磨阶段。尽管无即时合并动作，多个长期 PR 正逐步接近可合入状态，技术债清理与架构优化并行推进。

---

## 2. 版本发布

**无新版本发布**。  
当前最新 Release 仍为历史版本，团队未在24小时内推送正式更新。

---

## 3. 项目进展

今日有 **2 条 PR 被关闭/合并**，标志着关键优化落地：

- **#812 [CLOSED] perf(sqlite): debounce save() 并缓存 getConfig() 减少主线程阻塞**  
  ✅ 已解决 Issue #562 中 SQLite 同步写入阻塞 Electron 主线程的问题。通过引入 `save()` 防抖机制（500ms 合并写入）与异步文件写入（`fs.promises.writeFile`），显著降低 streaming 场景下的 UI 卡顿。同时缓存 `getConfig()` 结果，减少重复序列化开销。  
  🔗 [PR #812](https://github.com/netease-youdao/LobsterAI/pull/812)

- **#871 [CLOSED] feat(skills): 新增 skill 执行统计展示**  
  ✅ 在 SkillsManager 中集成 Skill 调用频次、成功率等统计分析功能，基于 OpenClaw 会话 JSONL 日志解析实现，并以弹窗形式可视化展示，提升用户对自动化技能使用效率的洞察能力。  
  🔗 [PR #871](https://github.com/netease-youdao/LobsterAI/pull/871)

> 这两项合并显著提升了系统性能与运维可观测性，是近期核心优化成果。

---

## 4. 社区热点

**无高互动 Issue 或 PR**。  
过去24小时所有 PR 均无新评论、点赞或讨论，社区讨论热度较低。但值得注意的是，以下 PR 虽标记为 `[stale]`，仍持续更新，表明作者仍在积极维护：

- **#762 feat(settings): 自定义模型 API 格式新增"自动检测"选项**  
  旨在降低用户配置门槛，尤其对非技术用户友好。若合入将极大改善多模型接入体验。  
  🔗 [PR #762](https://github.com/netease-youdao/LobsterAI/pull/762)

- **#768 feat(observability): add Opik observability integration via OpenClaw plugin**  
  引入可扩展的可观测性框架，为后续集成 LangFuse/LangSmith 打下基础，属中长期架构演进关键步骤。  
  🔗 [PR #768](https://github.com/netease-youdao/LobsterAI/pull/768)

> 尽管无即时互动，这些 PR 代表用户核心诉求：**易用性提升**与**生产环境可观测能力**。

---

## 5. Bug 与稳定性

**无新 Bug 报告**。  
过去24小时无新 Issue 提交，说明当前版本运行相对稳定。但以下已关闭 PR 对应的问题曾影响用户体验：

- **#788 fix(scheduled-task): deduplicate tasks before migration to prevent duplicates on restart**  
  修复了 SQLite → OpenClaw 迁移过程中因网关错误导致任务重复创建的问题（关联 Issue #775），避免应用重启后出现冗余定时任务。  
  🔗 [PR #788](https://github.com/netease-youdao/LobsterAI/pull/788)

> 该修复提升了任务调度系统的健壮性，属中等严重程度稳定性问题。

---

## 6. 功能请求与路线图信号

从待合并 PR 可识别以下**高优先级功能方向**，极可能纳入下一版本：

| 功能方向 | 代表 PR | 用户价值 |
|--------|--------|--------|
| **模型配置智能化** | #762（API 格式自动检测） | 降低多模型接入复杂度，减少配置错误 |
| **可观测性增强** | #768（Opik 集成） | 支持 LLM 应用监控、追踪与评估，面向企业级用户 |
| **UI/UX 优化** | #771（附件缩略图预览）、#783（输入框截断修复） | 提升协作场景下的视觉反馈与交互流畅度 |
| **性能优化** | #770（MarkdownContent 防重渲染）、#812（SQLite 异步写入） | 改善 streaming 响应速度与主线程阻塞 |

> 其中 **#762 与 #768** 最具战略意义，分别对应“开箱即用”体验与“生产就绪”能力，预计为下一版本重点。

---

## 7. 用户反馈摘要

**无直接用户评论数据**（过去24小时无新 Issue）。  
但从 PR 描述可反推用户痛点：

- **配置复杂**：用户难以判断 DeepSeek、智谱等模型应选 Anthropic 还是 OpenAI 兼容格式（#762 背景说明）。
- **协作体验待优化**：附件仅显示文件名缺乏预览，输入框在移动端易被截断（#771、#783）。
- **性能敏感**：streaming 过程中频繁写入导致界面卡顿，已被 #812 有效缓解。

> 用户核心诉求集中于：**降低使用门槛、提升响应速度、增强视觉反馈**。

---

## 8. 待处理积压

以下 **长期未合入但高价值 PR** 需维护者重点关注：

- **#762 [OPEN][stale] feat(settings): 自定义模型 API 格式新增"自动检测"选项**  
  创建超 50 天，持续更新，解决真实用户配置痛点，建议优先 review。  
  🔗 [PR #762](https://github.com/netease-youdao/LobsterAI/pull/762)

- **#768 [OPEN][stale] feat(observability): add Opik observability integration**  
  架构级扩展，为未来监控体系奠基，适合在稳定版本周期内合入。  
  🔗 [PR #768](https://github.com/netease-youdao/LobsterAI/pull/768)

- **#770 [OPEN][stale] perf(renderer): wrap MarkdownContent with React.memo**  
  简单但有效的性能优化，无破坏性变更，建议快速合入。  
  🔗 [PR #770](https://github.com/netease-youdao/LobsterAI/pull/770)

> 建议维护团队在本周内对上述 PR 进行代码审查与测试，避免优质贡献因 stale 状态流失。

---

**项目健康度评估**：⭐⭐⭐⭐☆（4/5）  
- 优势：性能优化成果显著，架构扩展性增强，社区贡献活跃  
- 风险：部分高价值 PR 长期 pending，需加强维护响应速度  
- 建议：建立 stale PR 定期 review 机制，加速功能落地

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyclaw">TinyAGI/tinyclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报（2026-05-18）

---

## 1. 今日速览  
Moltis 项目在过去24小时内保持中等活跃度，共产生 **2个新 Issue** 和 **5个 PR 更新**，其中 **3个 PR 已合并/关闭**，**1个新版本发布**。社区贡献者 @gmoigneu 和 @penso 主导了核心功能迭代与稳定性修复，涉及内存管理、外部代理会话持久化及远程访问扩展。整体开发节奏稳健，重点聚焦于底层架构优化与多模型兼容性提升。

---

## 2. 版本发布  
✅ **新版本 `20260517.03` 已发布**（[Release 链接](https://github.com/moltis-org/moltis/releases/tag/20260517.03)）  
本次发布为增量更新，主要整合了以下关键改进：
- **新增 NetBird 与 Cloudflare Tunnel 远程访问支持**（源自 PR #1002），扩展了除 Tailscale/ngrok 外的私有网络接入选项；
- **引入持久化外部代理会话机制**（源自 PR #566），支持 ACP、Codex CLI 及 Claude Code 的跨轮次会话保持；
- **修复 QMD 子进程泄漏问题**（源自 PR #1009），提升长时间运行稳定性。  
⚠️ **无破坏性变更**，但建议用户在启用 NetBird 或 Cloudflare Tunnel 前确认本地 CLI 工具已安装并配置权限。

---

## 3. 项目进展  
今日合并/关闭的 PR 显著推进了系统健壮性与功能边界：

- **#1002 [CLOSED] feat(remote-access): add NetBird and Cloudflare Tunnel support**  
  → 实现多云隧道集成，增强部署灵活性，尤其利好企业级私有环境用户。[链接](https://github.com/moltis-org/moltis/pull/1002)

- **#566 [CLOSED] feat(external-agents): add persistent agent sessions**  
  → 解决外部 AI 代理（如 Claude Code）会话中断问题，提升长对话连贯性，是 ACP 架构的重要里程碑。[链接](https://github.com/moltis-org/moltis/pull/566)

- **#1008 [CLOSED] Add NetBird and Cloudflare Tunnel to onboarding**  
  → 完善新手引导流程，降低新用户接入门槛，提升产品易用性。[链接](https://github.com/moltis-org/moltis/pull/1008)

> 综合评估：项目在“远程协作”与“多代理协同”两大方向取得实质性进展，架构成熟度进一步提升。

---

## 4. 社区热点  
当前无高评论或高反应 Issue/PR，但 **两个新报 Bug（#1006、#1007）均由核心贡献者 @maop 提交**，表明内部测试正在深入边缘场景：
- #1007 涉及 Gemma-4 模型推理标签解析异常，可能影响高级推理工作流用户体验；
- #1006 揭示配置系统在自动压缩时丢失默认值，属隐蔽性配置风险。  
虽暂无社区广泛讨论，但两者均标记为 `[bug]`，需优先验证是否影响生产环境。

---

## 5. Bug 与稳定性  
按严重程度排序如下：

🔴 **高优先级**  
- **#1007 [OPEN] gemma-4-31b-it reasoning tags 被当作纯文本处理**  
  → 导致 `<thought>` 块无法正确渲染为推理区块，破坏结构化输出体验。**尚无 fix PR**。[链接](https://github.com/moltis-org/moltis/issues/1007)

🟠 **中优先级**  
- **#1006 [OPEN] VoiceCoquiTtsConfig 默认值在 auto-compact 后消失**  
  → 配置“隐形”可能引发语音合成功能静默失败。**尚无 fix PR**，但类似问题曾在 QMD 模块修复（见 PR #1009）。[链接](https://github.com/moltis-org/moltis/issues/1006)

> 建议维护团队在下一热修复版本中优先处理 #1006，因其影响基础功能可靠性。

---

## 6. 功能请求与路线图信号  
尽管无显式“feature request”标签 Issue，但从 PR 可推断未来重点方向：

- **内存系统增强**：PR #1010 提议支持嵌套子文件夹与集合感知写入，反映用户对**结构化记忆管理**的强烈需求，极可能纳入 v2.1 路线图。[链接](https://github.com/moltis-org/moltis/pull/1010)
- **多模型推理兼容**：#1007 暗示需扩展 reasoning tag 解析器以支持非 OpenAI 模型（如 Gemma），预示**多厂商 LLM 适配**将成为下一阶段重点。

---

## 7. 用户反馈摘要  
本期 Issues 未提供详细用户评论，但从提交内容可提炼关键痛点：

- **模型兼容性不足**：Gemma-4 等新兴开源模型的结构化输出未被正确识别，限制高级用户使用场景；
- **配置透明度缺失**：auto-compact 行为未明确提示默认值变更，导致“配置消失”类困惑，反映**配置系统 UX 需优化**；
- **远程访问多样性需求**：NetBird/Cloudflare Tunnel 的快速集成（PR #1002/#1008）印证企业对**非 Tailscale 方案**的迫切需求。

---

## 8. 待处理积压  
经扫描，以下事项需维护者关注：

- **#1010 [OPEN] feat(memory): allow nested subfolders and collection-aware writes**  
  → 已开放近24小时，无评论。该 PR 对记忆系统有结构性影响，建议尽快 review 以避免分支漂移。[链接](https://github.com/moltis-org/moltis/pull/1010)

- **#1009 [OPEN] fix(qmd): kill child process when run_with_timeout expires**  
  → 虽为关键稳定性修复，但尚未合并。鉴于其解决子进程泄漏问题，**建议优先合入主分支**。[链接](https://github.com/moltis-org/moltis/pull/1009)

> 提醒：两个开放 PR 均出自活跃贡献者 @gmoigneu，技术价值明确，延迟合并可能影响后续开发节奏。

---  
**报告生成时间**: 2026-05-18  
**数据来源**: GitHub moltis-org/moltis 公开仓库

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报（2026-05-18）

---

## 1. 今日速览

过去24小时内，CoPaw 社区活跃度较高，共产生 **19条 Issues 更新**（17条新开/活跃，2条关闭）和 **13条 PR 更新**（12条待合并，1条已合并），显示出较强的开发参与度与问题反馈频率。尽管无新版本发布，但核心功能优化、测试覆盖提升及安全增强持续推进。值得注意的是，多个高优先级 Bug 报告集中爆发，涉及聊天无响应、上下文压缩失败、RCE 漏洞等关键路径问题，需紧急关注。

---

## 2. 版本发布

**无新版本发布**。当前最新稳定版本仍为 v1.1.7，建议用户关注即将发布的修复版本以解决近期集中报告的稳定性问题。

---

## 3. 项目进展

今日仅 **1个 PR 被合并**（#4466），但该 PR 意义重大：
- **#4466 [CLOSED] test(security): Phase 0-1 unit tests, 481 tests, 89% coverage**  
  ✅ 完成安全模块（`tool_guard` + `skill_scanner`）的全面单元测试覆盖，修复测试收集错误，并建立共享测试基础设施。  
  🔗 https://github.com/agentscope-ai/QwenPaw/pull/4466  
  此合并为后续 CI 硬门禁（L1 gate）打下基础，显著提升系统安全性保障能力。

此外，多个重要 PR 仍处于“Under Review”状态，包括 Tauri 桌面端支持（#3813）、xAI Grok 集成（#4444）等，表明团队正聚焦于架构扩展与生态集成。

---

## 4. 社区热点

### 🔥 最活跃 Issue：#2291 — “Help Wanted: Open Tasks — Come Contribute!”
- **评论数：61** | **👍：0** | 最后更新：2026-05-17  
- 🔗 https://github.com/agentscope-ai/QwenPaw/issues/2291  
- **分析**：作为长期开放任务看板，该 Issue 持续吸引贡献者认领 P0-P2 级任务，反映社区对结构化协作机制的高度依赖。维护者 @cuiyuebing 需加强任务状态同步，避免重复劳动。

### 💬 高频问题聚焦：聊天无响应（#4453、#4469）
- 两 Issue 合计 **13条评论**，均描述“发送消息后卡在三个点加载状态”，且重启、重装、切换模型均无效。  
- 日志指向 `RuntimeError: Event loop stopped before Future completed`，暗示异步通信层存在死锁或资源泄漏。  
- 🔗 #4453: https://github.com/agentscope-ai/QwenPaw/issues/4453  
- 🔗 #4469: https://github.com/agentscope-ai/QwenPaw/issues/4469  

---

## 5. Bug 与稳定性

按严重程度排序：

| 严重等级 | Issue | 描述 | 是否有 Fix PR |
|--------|------|------|-------------|
| ⚠️ **高危** | #4470 | 插件接口存在未授权远程代码执行（RCE）漏洞 | ❌ 无 |
| 🚨 **严重** | #4453 / #4469 | 聊天窗口完全无响应，Event loop 异常 | ❌ 无（疑似 WeChat 通道问题） |
| 🚨 **严重** | #4447 | 上下文压缩频繁失败（“missing ## header”） | ❌ 无 |
| 🚨 **严重** | #4454 | `/mission` 命令导致 Console 完全冻结 | ❌ 无 |
| ⚠️ **中危** | #3640 | MCP client TaskGroup 异常致 Agent 假死 | ❌ 无（4月报告，持续未解） |
| ⚠️ **中危** | #3854 | chromadb Rust binding 引发 SIGSEGV 进程崩溃 | ❌ 无（Linux + Python 3.13 特定环境） |

> 💡 建议：优先处理 RCE 漏洞（#4470）和聊天无响应问题，二者直接影响用户核心体验与系统安全。

---

## 6. 功能请求与路线图信号

以下功能请求已获得初步实现或积极讨论，有望纳入下一版本：

- **多技能路径配置支持**（#4455）→ 已由 @xielevi 提出，适配 SkillHub 等外部工具集成需求。  
  🔗 https://github.com/agentscope-ai/QwenPaw/issues/4455

- **CLI 彩色输出与 Typer 迁移**（#4472）→ 提升开发者体验，利用现代 Python 类型注解。  
  🔗 https://github.com/agentscope-ai/QwenPaw/issues/4472

- **上下文 Token 估算优化**（#4463）→ 已通过 PR #4465 实现缓存机制，减少重复计算。  
  🔗 https://github.com/agentscope-ai/QwenPaw/pull/4465

- **E2E 测试体系构建**（#4457 ~ #4461）→ 正在迁移 `python_e2e` 至主仓，为前端质量保驾护航。  
  🔗 https://github.com/agentscope-ai/QwenPaw/pull/4464

---

## 7. 用户反馈摘要

从 Issues 评论提炼关键用户声音：

- **痛点**：
  - “重装 Docker、清空配置、回退版本都没用，就是不能聊天”（#4469）→ 表明问题非本地环境所致，属系统性缺陷。
  - “执行任务后钉钉/微信没响应，但 console 还能用”（#3640）→ 多通道隔离失效，核心通信模块异常。
  - “chromadb 崩溃 45 次，根本没法用”（#3854）→ 第三方依赖稳定性成瓶颈。

- **满意点**：
  - 对内置技能（如 #4471 的 HTML 视频演示技能）表示欢迎，认为“降低了 demo 制作门槛”。
  - 对 Token 使用可视化（#4433）给予正面评价：“终于知道上下文占多少了”。

---

## 8. 待处理积压

以下长期未响应 Issue/PR 需维护者重点关注：

| 编号 | 类型 | 创建时间 | 状态 | 说明 |
|------|------|--------|------|------|
| #2684 | Issue | 2026-03-31 | OPEN | Ubuntu 安装启动失败，DeprecationWarning 提示 websockets.legacy 已弃用，可能影响新用户入门。 |
| #3640 | Issue | 2026-04-21 | OPEN | MCP client 导致 Agent 假死，4月底报告至今无进展，影响生产可用性。 |
| #3854 | Issue | 2026-04-27 | OPEN | chromadb 段错误致进程崩溃，Linux 用户高频反馈，需评估是否切换向量数据库或提供 fallback。 |
| #2771 | PR | 2026-04-01 | OPEN | 限制 mlx-lm 仅 Apple Silicon 使用，防止跨平台安装错误，属基础兼容性修复。 |

> 📌 **行动建议**：@cuiyuebing 及核心团队应在本周内对上述积压项进行 triage，明确修复优先级或关闭理由。

--- 

**总结**：CoPaw 正处于功能快速迭代与稳定性挑战并存的阶段。社区贡献活跃，但核心通信链路与安全漏洞亟待修复。建议下一版本聚焦“稳定性优先”，暂停非关键新功能合并，集中资源解决高影响 Bug。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>EasyClaw</strong> — <a href="https://github.com/gaoyangz77/easyclaw">gaoyangz77/easyclaw</a></summary>

过去24小时无活动。

</details>

---
*本日报由 [Big Model Radar](https://github.com/gsscsd/big_model_radar) 自动生成。*