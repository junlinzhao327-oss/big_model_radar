# OpenClaw 生态日报 2026-09-04

> Issues: 500 | PRs: 500 | 覆盖项目: 6 个 | 生成时间: 2026-09-04 00:10 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- [OpenHands SDK](https://github.com/OpenHands/software-agent-sdk)
- [Pi](https://github.com/earendil-works/pi)
- [LiteLLM](https://github.com/BerriAI/litellm)
- [Temporal](https://github.com/temporalio/temporal)

---

## OpenClaw 项目深度报告



---

## 横向生态对比



---

## 同赛道项目详细报告

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/NousResearch/hermes-agent">NousResearch/hermes-agent</a></summary>



</details>

<details>
<summary><strong>OpenHands SDK</strong> — <a href="https://github.com/OpenHands/software-agent-sdk">OpenHands/software-agent-sdk</a></summary>

# OpenHands SDK 项目动态日报（2026-09-04）

## 今日速览

过去 24 小时仓库活跃度处于高位：**21 条 Issue 更新**（新开/活跃 17 条、关闭 4 条），**43 条 PR 更新**（待合并 33 条、关闭/合并 10 条），无新版本发布。本日核心是**质量修复与 ACP 提供商整合收尾**：LLM 成本核算（#4817/#4836/#4848）、状态持久化（#4810/#4813）、WebSocket ESM 兼容（#4764/#4846/#4799）、Agent Canvas 云端 405（#4854/#4855）均有关键 PR 推进；Kimi Code（#4714）与 Pi（#4419）两个内置 ACP 提供商 PR 落地关闭。整体判断：项目处于**密集 PR 合并后的验证/修复周期**，而非新功能发布冲刺期，维护者响应速度快，但 LLM 成本、测试稳定性等系统性问题仍需持续关注。

---

## 项目进展

本日关闭/合并的关键 PR（10 条）与 Issue（4 条）显示项目在以下方向向前迈进：

1. **ACP 内置提供商扩展落地**
   - [#4714 feat(acp): add Kimi Code, plus the hardening the other provider PRs share](https://github.com/OpenHands/software-agent-sdk/pull/4714)：Kimi Code CLI 以 ACP 提供商形式内置，关闭了对应的 [Feature 请求 #4716](https://github.com/OpenHands/software-agent-sdk/issues/4716)。
   - [#4419 feat(sdk): register Pi as a built-in ACP provider](https://github.com/OpenHands/software-agent-sdk/pull/4419)：由维护者接手 rebase 到 #4832 的 install catalog 后合并，Pi 的 adapter+engine 拆分成为该 catalog 的首个落地案例。

2. **流式传输架构（Streaming）阶段性完成**
   - [#4681 Streaming step 3+4: /sockets/session/{id} — envelope wire, cursor, paged replay, byte-budget admission](https://github.com/OpenHands/software-agent-sdk/issues/4681) 关闭：server 端 `/sockets/session/{conversation_id}` 已随 #4807 落地，为客户端侧 [#4763](https://github.com/OpenHands/software-agent-sdk/issues/4763) 扫清了阻塞项。

3. **基础健壮性修复**
   - [#4114 fix(sdk): degrade per event when a stored event cannot be deserialized](https://github.com/OpenHands/software-agent-sdk/pull/4114)：存储事件反序列化失败时按单条降级处理，避免单条坏数据拖垮整个 event 加载流程。
   - [#4844 ci(typescript-client): run integration tests against the branch's agent-server](https://github.com/OpenHands/software-agent-sdk/pull/4844)：TypeScript

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/earendil-works/pi">earendil-works/pi</a></summary>



</details>

<details>
<summary><strong>LiteLLM</strong> — <a href="https://github.com/BerriAI/litellm">BerriAI/litellm</a></summary>



</details>

<details>
<summary><strong>Temporal</strong> — <a href="https://github.com/temporalio/temporal">temporalio/temporal</a></summary>



</details>

---
*本日报由 [Big Model Radar](https://github.com/junlinzhao327-oss/big_model_radar) 自动生成。*