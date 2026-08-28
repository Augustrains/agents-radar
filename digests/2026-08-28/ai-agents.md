# OpenClaw 生态日报 2026-08-28

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-28 07:19 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyagi)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw 项目深度报告

# OpenClaw 项目动态日报 — 2026-08-28

## 1. 今日速览

今日 OpenClaw 仓库保持高活跃度：过去 24 小时内有 500 条 Issue 更新（341 条活跃/新开，159 条关闭）和 500 条 PR 更新（336 条待合并，164 条已合并/关闭），但无新版本发布。当前最突出的信号集中在三个方面：**cron 投递可靠性**（#131603、#131610 同时针对延迟执行结果丢弃和重试耗尽通知提出修复）、**网关稳定性与资源泄漏**（#125344 报告 embedding 进程和 codex app-server 无 TTL 泄漏；#131456 修复嵌套 writer 竞态）、以及 **渠道层回归**（#131564 发现五个渠道插件存在 schema 同步问题，#131150 报告 Slack 多账户重启后 DM 静默丢失）。多个高优级 Issue（P0/P1）已在等待维护者产品决策，整体项目健康度中等偏上，但需警惕长期未决的稳定性问题。

---

## 2. 版本发布

**无新版本发布。**
当前最新版本为 [v2026.8.1-beta.3](https://github.com/openclaw/openclaw/releases/tag/v2026.8.1-beta.3)（截止 2026-08-28 仍处于 beta 验证阶段，#125626 中维护者 Patrick-Erichsen 持续在收集反馈）。过去 24 小时无预发布或正式版本产出。

---

## 3. 项目进展

过去 24 小时共合并/关闭 164 个 PR，以下为值得关注的重要变更：

**渠道兼容性修复**
- [#126424 [已关闭] fix(gateway): keep conversation delivery within agent bindings](https://github.com/openclaw/openclaw/pull/126424) — 修复多 agent 操作者使用对话工具时消息可能逃逸出 agent 绑定的问题，涉及 Discord、Telegram、Slack、Matrix 等多个渠道，XL 量级。
- [#112811 [已关闭] feat(msteams): support multiple bot accounts](https://github.com/openclaw/openclaw/pull/112811) — 支持单个网关配置多个 Microsoft Teams 机器人身份，解决此前只能运行一个 Teams-visible agent 的限制（关联 #71058）。

**UI 与用户体验**
- [#128995 [已关闭] feat: make full session actions available from chat header](https://github.com/openclaw/openclaw/pull/128995) — 从聊天头部即可进行 pin、未读标记、图标设置、复制 session ID 等完整操作。
- [#123535 [已关闭] fix(ui): avoid session catalog refresh storms](https://github.com/openclaw/openclaw/pull/123535) — 修复侧边栏会话目录在浏览器窗口聚焦时触发冗余全量刷新的问题。
- [#131174 [已关闭] fix(ui): retry stale dashboard final history](https://github.com/openclaw/openclaw/pull/131174) — 修复 Dashboard 在终态到达前收到陈旧快照时历史记录缺失的竞态。

**安全与配置**
- [#116489 [已关闭] feat(security): require acknowledgement for install policy warnings](https://github.com/openclaw/openclaw/pull/116489) — 安装策略现可返回 `warn` 状态，要求操作者确认后才能继续安装可疑插件或技能。

**CLI 与模型管理**
- [#128223 [已关闭] fix(cli): resolve alias targets from the write snapshot](https://github.com/openclaw/openclaw/pull/128223) — 修复 `openclaw models aliases add` 在解析别名目标时可能读到过期快照的问题。
- [#125471 [已关闭] fix(models): keep Claude CLI OAuth available in Control UI](https://github.com/openclaw/openclaw/pull/125471) — 修复网关重启后 Claude CLI OAuth 丢失刷新所有权、在 Control UI 中不可用的问题。

**发布流程**
- [#128371 [已关闭] fix(release): authorize focused beta evidence](https://github.com/openclaw/openclaw/pull/128371) — 解决 beta.3 发布阻塞：当冻结候选仅更改了已审核的 Slack 测试且失败的历史叶子已重跑成功后，发布器不再要求全量 Release Validation 通过。

---

## 4. 社区热点

**#42475 — 网关级别的 per-agent 成本预算**（23 评论）
> [Feature]: Per-agent cost budget enforcement at the gateway level  
> https://github.com/openclaw/openclaw/issues/42475

需求：在网关层为每个 agent 设置每日/每月成本上限，在调用模型前拦截以防止失控支出。评论数今日榜首，持续获得关注。来自企业/运维用户的强诉求——需要更细粒度的成本治理。

**#125626 — 2026.8.1 beta 反馈收集**（22 评论）
> OpenClaw 2026.8.1 beta feedback  
> https://github.com/openclaw/openclaw/issues/125626

维护者持续在 beta 期内收集反馈，评论活跃说明社区积极参与 beta 验证。

**#91009 — Codex PreToolUse hook 导致 CPU 占满 / 网关 RPC 阻塞**（21 评论，P0）
> Codex PreToolUse native hook relay spawns CPU-bound openclaw-hooks processes  
> https://github.com/openclaw/openclaw/issues/91009

P0 级严重问题，每个 `openclaw-hooks` 进程占用 ~100%+ CPU，直接拖垮网关 RPC。从 6 月至今仍未解决，社区持续施压。

**#48003 — Steer 模式无法在 turn 中途注入消息**（20 评论）
> Steer mode does not inject messages mid-turn for main sessions  
> https://github.com/openclaw/openclaw/issues/48003

核心功能缺陷：`messages.queue.mode: "steer"` 要等当前 turn 结束后才能注入消息，违背了"中途转向"的设计意图。社区关注度高。

---

## 5. Bug 与稳定性

按严重程度排列：

**P0 紧急**
- [#91009](https://github.com/openclaw/openclaw/issues/91009) — Codex PreToolUse hook 产生的进程占满 CPU、阻塞网关 RPC。**已有 linked PR，但 6 月至今未合入。** 无 fix PR。

**P1 高风险**
- [#125344](https://github.com/openclaw/openclaw/issues/125344) — memory-core 本地 embedding 进程和 codex app-server 无空闲 TTL 持续泄漏，蚕食网关 cgroup。**无 fix PR。**
- [#131150](https://github.com/openclaw/openclaw/issues/131150) — Slack 19 账户 socket 模式下，网关重启后所有账户 DM 静默丢弃（`prepareSlackMessage` 返回 null）。**无 fix PR。** 2026.8.1 回归。
- [#129314](https://github.com/openclaw/openclaw/issues/129314) — 隐藏的 runtime context 消息偶尔作为独立可见 turn 被发送给用户，暴露内部元数据。**无 fix PR。**
- [#100941](https://github.com/openclaw/openclaw/issues/100941) — 并行 tool fan-out 下网关丢弃 WebSocket 连接（1006），报"Gateway crashed"误导性错误。**无 fix PR。**
- [#87744](https://github.com/openclaw/openclaw/issues/87744) — Codex 支持的 Telegram turn 反复超时无法到达 `turn/completed`。**无 fix PR。**
- [#86215](https://github.com/openclaw/openclaw/issues/86215) — Codex OAuth 刷新失败可让 agent 卡死数小时，无清晰告警、无 profile 轮换。**无 fix PR。**

**P2 中等（已有修复）**
- [#131113](https://github.com/openclaw/openclaw/issues/131113) — 嵌套 writer drain 违反 FIFO 约束。已有 [PR #131456](https://github.com/openclaw/openclaw/pull/131456) 修复，待审核。
- [#131491](https://github.com/openclaw/openclaw/issues/131491) — cron 单次任务延迟超过 3 小时后执行结果被丢弃。已有 [PR #131603](https://github.com/openclaw/openclaw/pull/131603) 提供带延迟标注的投递方案。
- [#131490](https://github.com/openclaw/openclaw/issues/131490) — cron 重试耗尽后静默禁用且不通知属主。已有 [PR #131610](https://github.com/openclaw/openclaw/pull/131610) 修复。

**P1/P2 已关闭（今日合入修复）**
- [#92057](https://github.com/openclaw/openclaw/issues/92057) — 多会话/多 agent 负载下网关超时（已关闭）。
- [#106760](https://github.com/openclaw/openclaw/issues/106760) — Telegram pre-tool-call 文本在多个 content block 时被静默擦除（已关闭）。
- [#106914](https://github.com/openclaw/openclaw/issues/106914) — `models list` 因 sonnet-5 无 cost 数据崩溃（已关闭）。
- [#103884](https://github.com/openclaw/openclaw/issues/103884) — GPT-5.6 Sol 在 Codex 运行时被拒（已关闭）。
- [#116010](https://github.com/openclaw/openclaw/issues/116010) — 所有持久会话被限制在 128k 上下文（已关闭）。

---

## 6. 功能请求与路线图信号

**可能进入下一版本的功能（已有对应 PR）**
- **多 Teams 机器人支持** — [#71058](https://github.com/openclaw/openclaw/issues/71058) 已有 [PR #112811](https://github.com/openclaw/openclaw/pull/112811)（已关闭/已合入），从"无法实现"进入"已交付"状态。
- **Standing-grant 审批** — [#129526](https://github.com/openclaw/openclaw/issues/129526) 已有 [PR #131602](https://github.com/openclaw/openclaw/pull/131602)（新开待审），补齐撤回/列表/期限配置能力。
- **浏览器工具扩展** — 已有 [PR #131592](https://github.com/openclaw/openclaw/pull/131592) 新增 agent 请求/文本/模拟 + 缩略图卡片，拓展 browser 插件能力面。

**社区高票但无进展**
- [#42840](https://github.com/openclaw/openclaw/issues/42840) — Control UI 支持 MathJax/LaTeX（👍10，10 评论）。用户急需数学公式渲染，当前显示为原始 LaTeX。
- [#28300](https://github.com/openclaw/openclaw/issues/28300) — 主题定制系统（👍5，6 评论）。预设主题 + 自定义主题工作室。

**路线图信号（RFC 阶段）**
- [#71736](https://github.com/openclaw/openclaw/issues/71736) — Control UI 插件贡献槽（1 评论后关闭）。
- [#71712](https://github.com/openclaw/openclaw/issues/71712) — Agent 可调度的 cron API + 不可伪造来源证明。

---

## 7. 用户反馈摘要

**核心痛点**
- **长会话可靠性**：多个用户反映长时间对话后工具参数被静默丢弃（#53408）、上下文被错误截断（#116010），严重侵蚀信任感。
- **消息静默丢失**：Slack DM 重启后丢失（#131150）、Telegram 多 content block 文本被擦除（#106760）、Codex 的 turn 永不完成（#87744）——“静默”是用户最反感的关键词。
- **资源管理失控**：CPU 占满（#91009）、进程无 TTL 泄漏（#125344），单机部署用户尤感切肤之痛。
- **恢复假象**：`recovered=1` 但 MCP loopback 未重连（#98435）、网关报告正常但 WebSocket 已断（#100941），用户被误导性状态困扰。

**满意度信号**
- Cron 修复 PR（#131603/#131610）获得积极关注，用户期待已久的"延迟结果不丢"和"失败通知"终于有人处理。
- 多 Teams bot 支持落地（#112811）解决了运营多品牌团队的用户的长期困扰。

**呼声最高的诉求**
- 网关级 per-agent 成本预算（#42475，23 评论）——运维用户已不再满足于事后审计。
- 会话排序逻辑透明化（#51028，7 评论）——用户无法理解会话为何置顶，需要按"有意义活动"而非最后消息排序。

---

## 8. 待处理积压

**长期未响应的高优先级 Issue（按创建时间排序）**

| Issue | 创建 | 标签 | 状态 |
|-------|------|------|------|
| [#7338 Agent Attestation Headers](https://github.com/openclaw/openclaw/issues/7338) | 2026-02-02 | security, needs-security-review | 等待安全评审 |
| [#40982 3 分钟 watchdog 上限](https://github.com/openclaw/openclaw/issues/40982) | 2026-03-09 | P1, diamond lobster | 有 linked PR，待合入 |
| [#41165 Telegram DM 路由污染](https://github.com/openclaw/openclaw/issues/41165) | 2026-03-09 | P1, diamond lobster | 有 linked PR，待合入 |
| [#53008 Memory compaction 阻塞主通道](https://github.com/openclaw/openclaw/issues/53008) | 2026-03-23 | P1, diamond lobster | 等待产品决策 |
| [#91009 Codex hook CPU 100%](https://github.com/openclaw/openclaw/issues/91009) | 2026-06-06 | **P0**, platinum hermit | 有 linked PR，长期未合入 |
| [#84393 Codex 基础 prompt 注入](https://github.com/openclaw/openclaw/issues/84393) | 2026-05-20 | P1, security, platinum hermit | 等待安全评审 + 产品决策 |

**提醒**：#91009 是当前唯一 P0 且已存在 linked PR 但长期未合入的问题，建议维护者优先处理。

---

*本报告基于 GitHub 公开数据自动生成，仅供参考。*

---

## 横向生态对比

# 2026-08-28 开源 AI 智能体生态横向分析报告

---

## 1. 生态全景

个人 AI 助手/自主智能体开源生态正经历从"功能可用"到"架构可信"的关键跃迁：**稳定性、成本治理与安全边界**成为各项目社区反馈的共同焦点，而**记忆系统重构、Provider 契约标准化、渠道消息一致性**则是头部项目不约而同投入的主战场。以 OpenClaw 为首的头部项目已进入**平台化阶段**（网关架构、渠道矩阵、企业级治理诉求），中坚力量（NanoBot、IronClaw、ZeroClaw）正密集推进模块化重构与架构演进，而 PicoClaw、Moltis 等项目则以精细维护和小步快跑维持稳定输出。值得警惕的是，**静默失败类 Bug**（消息丢失、工具调用异常、认证失效无告警）已连续多日出现在各项目的高严重度问题榜单上，成为侵蚀用户信任感的最大系统性风险。

---

## 2. 各项目活跃度对比

| 项目 | Issues（活跃/新开） | PR 更新 | Release | 合并率 | 健康度 | 活跃阶段 |
|------|---------------------|---------|---------|--------|--------|----------|
| **OpenClaw** | 341 | 500 | 无（v2026.8.1-beta.3 验证中） | 33% (164/500) | 🟡 中等偏上 | 平台化运维期 |
| **NanoBot** | 2 | 24 | 无 | 37.5% (9/24) | 🟢 良好 | 架构重构期 |
| **Hermes Agent** | 50 | 50 | **v0.20.6** (8/27) | 12% (6/50) | 🟡 高活跃/高Bug密度 | 功能扩张期 |
| **PicoClaw** | 3 | 7 | 无 | 86% (6/7) | 🟢 稳定维护 | 稳定维护期 |
| **NanoClaw** | 11 (10新) | 50 | 无 | 8% (4/50) | 🟡 快节奏/稳定性承压 | 高速迭代期 |
| **NullClaw** | — | — | — | — | ⚪ 无活动 | 休眠 |
| **IronClaw** | 25 (新增) | 48 | 无 | 65% (31/48) | 🟢 良好 | 记忆系统攻坚期 |
| **LobsterAI** | 2 (新增) | 13 | **2026.8.26** | **100%** (13/13) | 🟢 健康 | 稳定迭代期 |
| **TinyClaw** | — | — | — | — | ⚪ 无活动 | 休眠 |
| **Moltis** | 0 | 2 | **20260827.01** | **100%** (2/2) | 🟢 健康（活跃度偏低） | 存量消化期 |
| **CoPaw** | 15 (新开) | 50 | 无 | 50% (25/50) | 🟢 良好 | 2.2.0 冲刺期 |
| **ZeptoClaw** | — | — | — | — | ⚪ 无活动 | 休眠 |
| **ZeroClaw** | 26 | 50 | 无（v0.8.5 截止 8/30） | 4% (2/50) | 🟡 良好但 PR 积压 | 架构演进期 |

---

## 3. OpenClaw 在生态中的定位

**生态地位：绝对头部，平台级枢纽。** OpenClaw 单日 Issue/PR 活动量（500+500）即超过其余所有活跃项目之和，社区规模与维护者投入（Patrick-Erichsen 等常驻维护者）断崖式领先。

**核心优势：**
- **渠道矩阵最完整**：Discord/Telegram/Slack/Matrix/MSTeams 等全渠道覆盖，且持续扩展（今日新增多 Teams 机器人支持），已验证大规模消息中间层的工程能力
- **企业级治理先行**：per-agent 成本预算（#42475，23 评论）虽未落地，但已是生态中唯一被系统性讨论的网关级成本治理方案
- **版本节奏稳健**：beta 验证流程（#125626 反馈收集）体现了对稳定性的重视，而非盲目追逐特性数量

**技术路线差异：**
- 与 Hermes Agent 的"激进功能扩张"路线不同，OpenClaw 侧重**网关可靠性 + 渠道兼容性**的平台型路线，修复重点集中在消息不丢失、路由不逃逸、进程不泄漏等基础设施问题
- 与 NanoClaw 的"快速试错"路线不同，OpenClaw 对 P0/P1 问题有更严谨的验证链路（如 #128371 放宽发布门禁的前提是"已审核的 Slack 测试且失败历史叶子已重跑成功"）

**空间与风险：**
- **最大风险是 P0/P1 积压**：#91009（Codex hook CPU 100%）从 6 月至今未合入，已有 linked PR 却长期搁置；#125344（进程泄漏）、#131150（Slack DM 丢失）均无 fix PR。这与其平台级定位形成反差，可能被竞品在稳定性维度追赶
- 长期未决的"静默失败"类问题（#129314 隐藏消息泄漏、#100941 误导性错误）侵蚀企业用户信任，成本治理诉求（#42475）若持续不落地，可能促使大客户转向自建

---

## 4. 共同关注的技术方向

| 方向 | 涉及项目 | 具体诉求 |
|------|---------|----------|
| **记忆/上下文管理重构** | IronClaw（史诗 #7276 拆解 8 Issue）、NanoBot（#5570/#5571 默认行为变更）、Hermes（压缩策略缺陷 #84718/#96775）、OpenClaw（#125344 泄漏） | 从"被动注入"到"主动召回"的架构转向；记忆归档与 provider 状态解耦；压缩摘要停滞回退链；进程/资源的确定性生命周期 |
| **Provider/模型契约标准化** | OpenClaw（别名解析、OAuth 刷新）、NanoClaw（7 个契约 PR 并行）、IronClaw（#7940 MCP OAuth 参数）、ZeroClaw（#9809 多模型支持）、Moltis（#1232 OpenAI-safe Schema） | 工具定义 Schema 的 OpenAI 兼容性；OAuth 令牌刷新所有权；多模型/多端点承载同一凭据；provider 配置校验统一化 |
| **渠道消息一致性** | NanoClaw（Discord 附件丢弃 #2888、Telegram Markdown #3569）、OpenClaw（Slack DM 丢失 #131150、Telegram 文本擦除 #106760）、NanoBot（飞书多卡片 #5567）、ZeroClaw（Telegram 线程碎片化 #10237） | 附件传递在 URL-only 适配器中的完整性；长消息/多 content block 不丢失；渠道消息合并策略统一化；重连/重启后状态不丢 |
| **成本治理与配额** | OpenClaw（#42475 per-agent 预算）、LobsterAI（#2562 扣费异常）、ZeroClaw（#9809 多模型成本优化） | 网关级调用拦截；细粒度配额；计费链路透明化 |
| **安装器/启动性能** | CoPaw（#7360/#7363/#7367 启动 30s-4min）、LobsterAI（#2561 升级删数据）、Hermes（#60323 macOS 启动超时） | 依赖懒加载；增量更新；非阻塞安装；数据目录保护 |
| **上下文窗口管理** | OpenClaw（#116010 128k 限制，已关闭）、IronClaw（#7954 累计压缩屏障）、Hermes（#39691 工具输出压缩） | 长会话下上下文膨胀控制；压缩策略保留指令/推理依据；Per-token 成本与延迟优化 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构特征 |
|------|---------|---------|-------------|
| **OpenClaw** | 全渠道消息网关 + 多 Agent 协调 | 企业/运维/重度多平台用户 | 网关-渠道解耦架构，Agent bindings 隔离，大型 PR 严谨验证 |
| **Hermes Agent** | 功能广度优先，桌面端+群聊+实时语音 | 追求新特性的个人开发者 | 快速迭代，滚动 Release（~525 PR/版本），社区驱动特性决策 |
| **NanoBot** | 轻量级、高性能、渠道聚焦（飞书/国内生态） | 国内开发者、轻部署场景 | 单核心维护者主导，模块化解耦重构（内存/Agent Runner/Provider 路由），注重默认行为合理性 |
| **IronClaw** | 记忆系统 + 自动化工作流 | 研究型/自动化重度用户 | 记忆多阶段落地（学习路由/适配器/审查），上下文压缩屏障，CI 集中化 |
| **ZeroClaw** | 架构深度演进 + 安全治理 | 关注前沿架构的贡献者/早期采用者 | RFC 驱动的决策机制（决策队列 #8692），WASM 插件、会话架构重构、沙箱策略 |
| **CoPaw (QwenPaw)** | 桌面端 + Web 控制台 + 多渠道 | 中文用户、桌面优先（Windows） | 同步调用问题突出，性能优化 + 移动端预研（React Native），Hub 多租户路线图 |
| **NanoClaw** | Provider 多样化（Codex/OpenCode/Gemini） | 需要灵活模型后端的开发者 | provider 契约标准化为重，通道适配层（chat-sdk-bridge）为当前主要短板 |
| **LobsterAI** | 桌面应用 + 安装器体验 | 中文桌面用户、非技术用户 | Electron 类桌面架构，发布节奏稳定，Install 安全为当前焦点 |
| **PicoClaw** | 轻量、极致简约 | 极简主义用户 | 低频繁迭代，依赖自动更新占主，IRC 等长尾渠道支持 |
| **Moltis** | 沙箱安全 + 工具生态兼容 | 安全敏感型部署 | 沙箱镜像验证、OpenAI 工具 Schema 兼容、多租户权限细分 |
| **休眠项目** (NullClaw/TinyClaw/ZeptoClaw) | — | — | 24h 无任何活动，可能已停止维护 |

---

## 6. 社区热度与成熟度分层

### 🟢 第一梯队：快速迭代期（高活跃 + 高功能产出）
- **OpenClaw** — 平台级活跃度，但 P0/P1 积压与 beta 验证周期拉长，处于"重压下的平台演进"阶段
- **Hermes Agent** — 以 ~525 PR/版本的速度滚动推进，功能扩张激进，Bug 密度同步上升
- **NanoClaw** — 核心团队密集重构（7 个契约 PR 并行），但通道适配稳定性（附件/按钮/依赖锁）尚未跟上前端速度
- **CoPaw** — 2.2.0 冲刺期，安全响应迅速（当日开 Issue 当日合修复），性能问题集中爆发

### 🟡 第二梯队：质量巩固期（中高活跃 + 架构纵深）
- **IronClaw** — 记忆系统多阶段拆解展现强执行力，上下文管理、CI 基础设施同步升级，Windows 支持仍是短板
- **ZeroClaw** — RFC 驱动的深度架构演进，响应速度快（3 天修 Bug），但 PR 合并漏斗瓶颈明显（50 条仅合 2 条）
- **NanoBot** — 单核心维护者主导的密集重构，方向清晰但外部贡献者响应节奏需平衡

### 🔵 第三梯队：稳定维护期（低活跃 + 精细打磨）
- **LobsterAI** — PR 合并率 100%，发布节奏稳定，但新 Issue 输入偏低
- **PicoClaw** — 依赖自动更新占主导，社区功能请求推进缓慢
- **Moltis** — 队列干净无积压，但新输入停滞，活跃度有回落趋势

### ⚪ 休眠状态
- **NullClaw / TinyClaw / ZeptoClaw** — 24h 无任何活动

---

## 7. 值得关注的趋势信号

### 信号一：记忆系统从"被动注入"走向"主动召回"（已在多项目主力推进）
NanoBot #5571 默认不再将 MEMORY.md 注入系统提示词，改为按需工具调用；IronClaw 记忆系统 8 个 Issue 拆解落地（学习路由/适配器/审查）；Hermes 压缩策略修复保留指令问题。**开发者启示**：context 预算是新的性能边界，主动召回将替代全量注入成为记忆设计的默认范式。

### 信号二："静默失败"成为信任危机的头号杀手
跨项目的高严重度 Bug 高度集中在**无告警的失败**——Slack DM 静默丢失（OpenClaw #131150）、agent 静默停止响应（NanoClaw #3568）、消息被静默丢弃（CoPaw #5344）、恢复后 MCP 未重连但显示 recovered=1（OpenClaw #98435）。**开发者启示**：在智能体产品设计中，"不撒谎"（明确的失败状态 + 可恢复路径）比"不失败"更重要。

### 信号三：Provider 契约标准化成为多项目的一致选择
NanoClaw 核心团队一次性推进 7 个契约 PR；Moltis 修复 OpenAI 严格 Schema 兼容；OpenClaw 多 Teams 支持落地；ZeroClaw 多模型子表（#9809）被标记为高需求。**开发者启示**：单一 Provider 绑定正在成为过去，模型/端点/凭据三位一体的可配置模型是共同方向。

### 信号四：成本治理从"事后审计"到"事前拦截"
OpenClaw #42475（网关级 per-agent 预算，23 评论）是社区呼声最高的未落地功能；LobsterAI #2562 扣费异常引发用户激烈反应；ZeroClaw 多模型支持被期待的隐含动机即是成本优化。**开发者启示**：成本控制将嵌入智能体基础设施（LLM 网关、路由层），而非停留在账单侧。

### 信号五：安装/升级流程的数据安全成为用户信任底线
LobsterAI #2561（升级删除项目文件夹，2000 credits 损失）和 CoPaw 启动性能问题，均指向客户端应用的生命周期管理缺陷。**开发者启示**：对于发布桌面应用的项目，"升级不动用户数据"是基本底线，启动路径上的依赖懒加载是基本要求。

### 信号六：中国用户生态需求在头部项目中加速显性化
Hermes 同日内一关一开两条中国用户 Issue（#46839 关闭、#96858 新开），后者已论证"国内镜像对项目本身的价值"；NanoBot 飞书渠道诉求（#5567）直指国内协作工具生态。**开发者启示**：面向中文市场的渠道（飞书/企业微信）与网络基础设施优化（镜像/代理），正从"nice-to-have"变为"中国用户留存的关键因子"。

---

*报告生成时间：2026-08-28 | 基于上述 13 个开源项目的 GitHub 公开数据*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报

**日期：** 2026-08-28  
**数据窗口：** 2026-08-27 ~ 2026-08-28  

---

## 1. 今日速览

NanoBot 项目在过去 24 小时内保持**高活跃度**，PR 更新达 24 条，其中 9 条已合并/关闭，15 条待处理，显示核心维护团队（chengyongru 主导，KDB-Wind、BearMett 等积极参与）正在进行一轮**密集的内部重构与优化**。重点方向集中在**内存管理重构**（#5565/#5575/#5571）、**Agent Runner 架构边界梳理**（#5568/#5569/#5574）以及 **MCP OAuth 令牌刷新**（#5573）。Issues 方面仅 2 条新开，无新版本发布，整体项目呈现出**"架构调整期"的典型特征**——代码变动频繁但对外用户可见的新功能较少。飞书渠道的多消息整合问题（#5567）是今日最值得关注的用户侧诉求。

---

## 2. 版本发布

**无新版本发布。** 项目正处在重构密集期，多个 PR 标题带 `refactor` 前缀，预期下一个版本可能包含显著的行为变更（如内存 recall 默认行为、并发限制默认值等），建议使用者关注合并状态。

---

## 3. 项目进展

今日共 9 条 PR 被合并/关闭，核心进展如下：

- **[#5575] refactor(memory): remove consolidation ratio**（[链接](https://github.com/HKUDS/nanobot/pull/5575)）  
  移除 `consolidationRatio` 配置，代之以确定性存档策略（保留最近 8 条消息+回溯到用户轮次）。**简化了内存压缩逻辑，提升可预测性**，是内存管理重构系列的重要一环。

- **[#5565] refactor(memory): decouple archival from provider state**（[链接](https://github.com/HKUDS/nanobot/pull/5565)）  
  提取 `MemoryArchiver` 组件，将记忆归档与 SessionManager 解耦，同时保持 provider 续跑状态跨 token 触发和空闲归档的一致性。引入 `last_archived` 新语义名以兼容 `last_consolidated`。**架构层面为后续记忆插件化铺路。**

- **[#5572] fix(agent): default request concurrency to unlimited**（[链接](https://github.com/HKUDS/nanobot/pull/5572)）  
  当 `NANOBOT_MAX_CONCURRENT_REQUESTS` 未设置时，默认并发限制改为**无限**。修复了 WebUI 多 tab 场景下互相阻塞的问题，是**面向用户体验的重要默认行为修正**。

- **[#5574] refactor(providers): make fallback attempts explicit**（[链接](https://github.com/HKUDS/nanobot/pull/5574)）  
  引入不可变的 `ProviderAttempt` 路由，在执行前解析具体 provider/model/transport/context window/重试策略。将隐式 fallback 逻辑显式化，降低后续维护复杂度。

- **[#5569] refactor(agent): extract tool execution boundary**（[链接](https://github.com/HKUDS/nanobot/pull/5569)）  
  将工具调用准备、执行、批处理、错误观察与安全分类从 `AgentRunner` 中剥离为功能性边界模块，让 `AgentRunner` 专注于 ReAct 阶段控制。

**综合判断**：项目核心架构正在经历一轮有序的模块化重构，内存管理、Agent 执行链路、Provider 路由三大方向同步推进，整体健康度良好，但合并后的回归风险需密切关注。

---

## 4. 社区热点

今日最受关注的议题集中在 Issues 区：

- **[#5567] Feat: 飞书渠道应整合多轮回复为单条流式卡片消息**（[链接](https://github.com/HKUDS/nanobot/issues/5567)）  
  获 2 条评论，是目前 Issues 中唯一有讨论的条目。用户 `yrxeva` 明确指出飞书渠道存在"一用户消息 → N 条 agent 回复"的体验割裂问题：流式输出使用 `send_delta()`、工具提示用 `send()`、最终输出再次 `send()`，导致卡片消息多条并存。**诉求本质是对话语义完整性**——用户期望保持 1:1 的消息对应关系，这与 ChatGPT/Claude 等主流产品的交互范式一致。

- **[#5564] fix(session): prevent path traversal in session file handling**（[链接](https://github.com/HKUDS/nanobot/issues/5564)）  
  由 arena-ai-coding-agent[bot] 自动提交，属于**安全扫描发现**。无评论，但路径穿越漏洞（session ID 未验证直接拼接文件路径）属于**中高危安全风险**，建议维护者优先处理。

**PR 侧分析**：虽然 24 条 PR 均显示 0 评论，但 chengyongru 连续提交 7 条关联重构 PR（#5568→#5575），其内部协作密度极高，架构方向呈现高度一致性。

---

## 5. Bug 与稳定性

| 严重程度 | Issue/PR | 描述 | 状态 |
|---------|----------|------|------|
| **中高** | [#5564](https://github.com/HKUDS/nanobot/issues/5564) | Session 文件路径穿越漏洞，恶意 session ID 可读取任意文件 | 无 fix PR，待处理 |
| **中高** | [#5573](https://github.com/HKUDS/nanobot/pull/5573) | MCP OAuth 令牌过期后无法自动刷新（含 gateway 重启场景） | 已有 fix PR，待合并 |
| **中** | [#5382](https://github.com/HKUDS/nanobot/pull/5382) | Windows 平台 `os.replace()` 偶发 `[WinError 5]` 导致 gateway 崩溃（已在日志中确认两次） | 已有 fix PR，带 `conflict` 标记，待处理 |
| **中** | [#5483](https://github.com/HKUDS/nanobot/pull/5483) | 延迟消息可能重新创建已删除的 session | 已有 fix PR，待合并 |
| **中** | [#5339](https://github.com/HKUDS/nanobot/pull/5339) | WebUI 临时聊天被丢弃后消息仍可能被持久化 | 已有 fix PR，待合并 |
| **中** | [#5338](https://github.com/HKUDS/nanobot/pull/5338) | MCP OAuth 存储读失败被误判为空存储，可能覆盖其他服务器凭据 | 已有 fix PR（draft），待推进 |
| **低** | [#4346](https://github.com/HKUDS/nanobot/pull/4346) | 图片被剥离时泄漏本地路径而非标记为不可查看（已关闭，可能被搁置） | 已关闭 |

**关键风险**：Windows 平台崩溃（#5382）和 MCP 凭据覆盖（#5338）两条 PR 均超过 2 周未合并且带 `conflict` 标记，建议维护者优先处理冲突。

---

## 6. 功能请求与路线图信号

- **飞书渠道单卡片消息**（[#5567](https://github.com/HKUDS/nanobot/issues/5567)）  
  用户明确要求 `用户发一条 → agent 回一条` 的流式卡片。考虑到飞书是国内协作工具的头部产品，**该功能对国内用户获取具有战略意义**。当前已有 CardKit 流式卡片实现基础，建议结合「工具调用阶段可否并入主卡片」的方案评估可行性。

- **每 spawn 独立模型预设**（[#5561](https://github.com/HKUDS/nanobot/pull/5561)，Resolves #4231）  
  通过 `spawnPresets` 允许列表实现每个 spawn 独立模型配置，是 #4291 的替代实现。作者明确引用了此前 PR 评审中的设计方向。**该功能将显著提升多模型管理灵活性**，适合纳入下一版本规划。

- **记忆系统改造三连**（[#5570](https://github.com/HKUDS/nanobot/pull/5570) + [#5571](https://github.com/HKUDS/nanobot/pull/5571)）  
  - `#5570`：引入可插拔的 `MemoryBackend`（`ingest`/`recall` 接口），首个后端为现有 `MemoryStore`  
  - `#5571`：**默认**不再将 `MEMORY.md`、`history.jsonl`、归档摘要注入系统提示词，改为按需调用 `recall_memory` 工具  
  **这是一个重要的默认行为变更**——长期记忆从"被动注入"转为"主动召回"。对 token 消耗和上下文清洁度是显著提升，但用户需要时间适应。

- **Session 焦点持久化**（[#5537](https://github.com/HKUDS/nanobot/pull/5537)，Fixes #3292）  
  为 `my` 工具增加 session 级 `focus` 值，支持跨轮次、跨重启保留一条简短的连续性提示。适合希望 agent 记住"当前在做什么"的场景。

---

## 7. 用户反馈摘要

基于今日 Issues 评论的定性分析：

- **飞书渠道体验割裂**（[#5567](https://github.com/HKUDS/nanobot/issues/5567)）：用户 `yrxeva` 描述的场景非常典型——工具提示、进度消息、最终输出分多条发送，在城市 IM 场景下会打断对话节奏。用户对「流式卡片已有实现」但工具阶段不并入表示不解，说明 **渠道消息合并策略需要统一化设计**，而非各渠道自扫门前雪。

- **安全类自动报告增加**（[#5564](https://github.com/HKUDS/nanobot/issues/5564)）：由 AI agent 自动提交的安全发现说明项目已被扫描工具覆盖，对开源项目是好事；但同时也提醒维护者需要建立**漏洞响应机制**。

- **从 PR 讨论中捕获的信号**：#5561 作者提到设计方向来自 #4291 的评审讨论（credit 给 @aiguozhi123456 和 @chengyongru），说明社区对设计方案的 contributive 迭代流程正在发挥作用，且外部开发者（@BearMett）有动力参与替代实现。

---

## 8. 待处理积压

以下为长期未响应或存在阻塞的重要条目，建议维护者关注：

| 条目 | 天数（约） | 阻塞原因 / 风险 | 建议 |
|------|-----------|----------------|------|
| [#5382](https://github.com/HKUDS/nanobot/pull/5382) Windows 平台归档崩溃修复 | 15 天 | 带 `conflict` 标记，但崩溃已在生产日志中复现两次 | **优先处理冲突并合并**；若无法及时合并，建议至少合入 `os.replace` 的 try-except 兜底 |
| [#5396](https://github.com/HKUDS/nanobot/pull/5396) 收窄 Pyright 文件级抑制 | 14 天 | 涉及 9 个工具模块，改动面广，带 `conflict` 标记 | 考虑拆分为小 PR 或邀请作者 rebase |
| [#4346](https://github.com/HKUDS/nanobot/pull/4346) 图片剥离时泄漏路径 | 74 天 | 已关闭但问题描述为安全/隐私泄露，不应被搁置 | 确认是否已由其他 PR 覆盖；若未修复，建议重新打开 |
| [#5338](https://github.com/HKUDS/nanobot/pull/5338) MCP OAuth 凭据覆盖风险 | 17 天 | Draft 状态，涉及跨服务器凭据安全问题 | 主动联系作者推动完成 |
| [#5483](https://github.com/HKUDS/nanobot/pull/5483) 延迟消息重建已删除会话 | 6 天 | 已有完整实现与测试，停在待审状态 | 无明显阻塞，建议安排评审 |
| [#5537](https://github.com/HKUDS/nanobot/pull/5537) Session focus 持久化 | 3 天 | 功能明确（Fix #3292），实现完整 | 建议纳入下一版本讨论 |

---

**总结**：NanoBot 当前处于**架构优化与基础设施加固**阶段，核心维护者 chengyongru 正在快速、有节奏地推进重构，方向清晰。但需注意三点：① 多条长期积压 PR 的冲突维护成本在上升；② 安全相关问题（#5564/#5338）不见得能等；③ 飞书渠道反馈表明非技术用户对「消息合并」这类体验细节有明确期待。项目健康度总体良好，但需**在重构节奏与外部贡献者响应之间找到平衡**。

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-28

---

## 1. 今日速览

项目今日活跃度处于**高位**：24小时内产生50条Issue更新（98%为新增/活跃）与50条PR更新（88%待合并），并发布v0.20.6补丁版本（滚动纳入约525个PR）。社区讨论高度集中在**会话恢复可靠性**（#93888、#96877、#79001）与**上下文压缩策略缺陷**（#84718、#96775、#96949）两大主题，Bug类Issue占比显著偏高。值得注意的是，**中国用户相关的两条Issue**（#46839关闭、#96858新开）同日获得关注，显示国内社区需求正在积累。项目整体"高活跃、高讨论、高Bug密度"——工程推进速度可观，但稳定性和兼容性问题仍是主要短板。

---

## 2. 版本发布

### v0.20.6 (v2026.8.27)

- **发布日期**: 2026年8月27日
- **性质**: Patch Release，面向下游消费者（Docker镜像、托管部署、新安装）的稳定标签
- **内容**: 滚动纳入自v0.20.5以来合并的约525个PR
- **破坏性变更**: 无明确说明，作为patch release定位，预期无破坏性变更
- **迁移注意事项**: 属于稳定标签发布，建议下游消费者及时跟进以纳入累积修复

> 链接: [Hermes Agent v0.20.6 Release](https://github.com/NousResearch/hermes-agent/releases)

---

## 3. 项目进展

今日合并/关闭的PR共6条（含自动关闭），值得关注的有：

- **PR #96634 (已合并)** — `fix(compression): retry a stalled summary on the fallback chain`
  修复了上下文压缩摘要停滞时辅助客户端异常路径回退失效的问题。该PR为P1优先级bug修复（#78981），是今日合并的最重要修复，直接影响长会话体验。合并后已有后续PR #96949跟进解决其遗留的所有权问题。

- **PR #96951 (已合并/自动)** — `fmt(js): npm run fix` 自动代码格式化PR，由机器人`hermes-seaeye[bot]`自动生成并合并

- **PR #96945 (已关闭)** — `perf(compression): add guarded fast summary lane`
  **被标记为 duplicate 并关闭**（同主题的 #93634 仍在评估中），说明压缩快速通道方案尚未收敛，实现路径存在分歧

- **PR #93634 (已关闭)** — `perf(compression): add guarded fast summary lane`
  同样被关闭（非合并），与 #96945 构成重复提交，项目采用了保留先来者的策略

值得注意：**今日合并数量极少（实质修复仅1个）**，大量PR仍处于等待评审状态，44条待合并PR的积压可能成为瓶颈。

---

## 4. 社区热点

| 排名 | Issue/PR | 评论数 | 核心诉求 |
|-------|----------|--------|----------|
| 1 | [#66616 Skills index is stale or degraded](https://github.com/NousResearch/hermes-agent/issues/66616) | 110 | 自动化新鲜度探针持续报警——Skills Hub索引延迟超限（29.8h vs 26h限制），且该问题已持续**41天**，社区耐心消耗严重 |
| 2 | [#93888 Desktop sends local runtime ID to Remote Gateway](https://github.com/NousResearch/hermes-agent/issues/93888) | 14 | P1级Bug：Desktop连接远程Gateway时发送错误的本地运行时ID，导致**已存会话完全无法恢复**，用户被卡死 |
| 3 | [#39691 Compress tool output with headroom-ai](https://github.com/NousResearch/hermes-agent/issues/39691) | 12 (👍 17) | 社区高赞功能需求：当前压缩仅限会话级LLM调用摘要，缺少工具输出层面的细粒度压缩方案 |
| 4 | [#60323 Desktop boot timeout on macOS](https://github.com/NousResearch/hermes-agent/issues/60323) | 11 | macOS桌面端启动超时：虽日志显示后端已就绪但前端仍等待至90000ms，等待队列推进缓慢 |
| 5 | [#77111 RealtimeVoiceProvider ABC](https://github.com/NousResearch/hermes-agent/issues/77111) | 9 | 四个并发duplex-voice PR竞争同一集成点，社区建议按AGENTS.md规则设计ABC接口而非逐个合并 |

**热点趋势分析**：
- **两个P1级会话恢复Bug连续上榜**（#93888、#79001）、一个P2级MCP握手失败（#96877），说明远程/多端场景下的**会话一致性问题**已经成为社区最大痛点。
- Skills索引陈旧问题已追踪**41天**仍处于"degraded"状态——自动化监控系统有效，但修复效率不足。
- 值得注意的"隐性热点"是**两条中国用户相关Issue**（#46839关闭、#96858新开），话题涉及安装网络问题和镜像/更新渠道建议，后者已明确论证项目收益，是一条高质量建议。

---

## 5. Bug 与稳定性

按严重程度排列：

### 🔴 P1 严重

| Issue | 问题 | 状态 |
|--------|------|------|
| [#93888 Desktop远程会话恢复失败](https://github.com/NousResearch/hermes-agent/issues/93888) | Desktop发送本地运行时ID至远程Gateway，已存会话无法恢复，用户被永久卡死 | **无fix PR**，评论14条，仍在讨论 |
| [#84718 压缩丢弃策略保留指令](https://github.com/NousResearch/hermes-agent/issues/84718) | 上下文压缩保留todo列表但丢弃技能指令和推理依据，导致agent盲目执行过期任务 | **无fix PR** |
| [#96775 压缩停滞重入同一策略](https://github.com/NousResearch/hermes-agent/issues/96775) | 中断的预压缩没有持久化backoff，重新进入相同失败策略。**已有对应修复PR #96634合并，但仅覆盖特定路径** | 部分修复（#96634已合并） |

### 🟠 P2 中等

| Issue | 问题 | 状态 |
|--------|------|------|
| [#96877 MCP握手失败](https://github.com/NousResearch/hermes-agent/issues/96877) | MCP客户端发送不支持的`sampling.tools`字段导致Zoho服务器拒绝整个握手 | **无fix PR** |
| [#60323 macOS桌面启动超时](https://github.com/NousResearch/hermes-agent/issues/60323) | 后端就绪但前端超时，等待90000ms后失败 | **无fix PR** |
| [#96902 Copilot grok-4.6 400错误](https://github.com/NousResearch/hermes-agent/issues/96902) | GitHub Copilot provider上设置grok-4.6即失败，标记为duplicate | **无fix PR** |
| [#83992 Python 3.14兼容性](https://github.com/NousResearch/hermes-agent/issues/83992) | `DaemonThreadPoolExecutor`使用了Python 3.14删除的属性。**已有PR #90201修复** | PR #90201待合并 |
| [#96924 视觉恢复使用过期provider](https://github.com/NousResearch/hermes-agent/issues/96924) | 跨provider回退恢复后辅助视觉检测使用过期provider，发送图片到错误端点 | **无fix PR** |

### 🟡 P3 较低

| Issue | 问题 | 状态 |
|--------|------|------|
| [#66616 Skills索引陈旧](https://github.com/NousResearch/hermes-agent/issues/66616) | 索引29.8小时未更新超限，持续41天未解决 | **无fix PR** |
| [#75130 技能提议队列膨胀](https://github.com/NousResearch/hermes-agent/issues/75130) | 8天内357条提案、21%无效，`write_approval`使队列自失效 | **无fix PR** |
| [#96800 AMD RDNA4渲染缓慢](https://github.com/NousResearch/hermes-agent/issues/96800) | Electron在AMD新GPU + Wayland下渲染极慢，需手动传GPU flags绕过 | **无fix PR，有workaround** |

---

## 6. 功能请求与路线图信号

### 高潜力（已有实现/接近实现）

- **PR #96919 — Bot模式：自主群聊中Bot间文件传递**
  Bot创建的报告、截图、补丁等文件无法传给下一个Bot，只能粘贴文本。功能完整、涉及面广（CLI/gateway/tools/TUI/desktop），是Group Chat多智能体协作的重要拼图。

- **PR #96952 — iOS WebKit会话行可点击**
  修复web dashboard在iOS上无法打开会话的问题，已有根因分析，预计可快速合入。

- **PR #96950 — 飞书DM会话文档工具修复**
  启用飞书文档/云盘工具在私聊场景下的客户端回退。

- **PR #96944 — Cron按调用时解析profile路径**
  修复多profile场景下cron使用冻结路径导致写错文件的问题。

### 需关注的方向性需求

- **#39691（👍17）— headroom-ai工具输出压缩**: 社区高赞，属于上下文压缩方向的延伸功能。当前 #96945/#93634 的"fast summary lane"方案尚未收敛，此类需求可能被推迟。

- **#96858 — 国内镜像/更新渠道建议**: 新开Issue（2评论/2👍），从项目推广价值角度论述。结合 #46839 的关闭，中国用户访问问题**尚未有系统性解决方案**，建议维护者认真评估。

- **#96937 — 波兰语支持**: 已完成约3450行翻译（覆盖所有41个section），属于低成本高确定性需求，可直接合入。

- **#77111 — RealtimeVoiceProvider ABC**: 涉及4个竞争PR，若按项目AGENTS.md规则推进ABC抽象设计，将是一个跨语音提供商的架构级改进。

---

## 7. 用户反馈摘要

**主要痛点**：

1. **会话恢复失败是最核心的不满来源**（#93888）："*Desktop can get permanently stuck on 'Restore failed — Session not found'*"——用户存储在远程Gateway的会话完全无法打开，直接破坏核心工作流。

2. **压缩策略破坏任务执行**（#84718）："*agent keeps executing a task item long after the context that would let it question that item is gone*"——压缩后agent失去技能指令和推理依据，但todo仍在，导致盲目执行。用户反馈"preserves the imperative but destroys the policy"，精确描述了这一诡异行为。

3. **Settings/环境兼容性困扰中国用户**（#46839）："*安装程序不会走梯子，只会默默被墙*"——网络问题被关闭时用户已尝试多种方案。新Issue #96858建议者进一步指出"*不只是为了我们国内用户方便，我认为它对 Hermes 本身也很有价值*"，将诉求上升至项目推广层面。

4. **Mac桌面启动偶发超时**（#60323）："*Timed out waiting for Hermes backend port announcement (90000ms)*"——即使日志已显示端口公告，前端仍超时；等待时间长达90秒，体验严重受损。

**积极信号**：
- #96937 波兰语用户已主动完成全部翻译内容（约3450行），展现出较高的社区参与热情。
- #96800 用户提供精确的环境描述和已验证的workaround（`ELECTRON_EXTRA_LAUNCH_ARGS`），便于后续针对性修复。

---

## 8. 待处理积压

### 长期未解决（需维护者关注）

| 条目 | 创建时间 | 持续天数 | 类型 | 优先级 | 备注 |
|--------|----------|----------|------|--------|------|
| [#66616 Skills索引陈旧](https://github.com/NousResearch/hermes-agent/issues/66616) | 2026-07-18 | 41天 | Bug | P3 | 110条评论，社区持续关注，自动化监控已多次报警但修复未落地 |
| [#60323 macOS桌面启动超时](https://github.com/NousResearch/hermes-agent/issues/60323) | 2026-07-07 | 52天 | Bug | P1 | 11条评论，长期未解决 |
| [#46839 中国用户网络问题](https://github.com/NousResearch/hermes-agent/issues/46839) | 2026-06-15 | 74天 | 支持 | — | **今日被关闭**，实际上未提供系统解决方案；#96858新开同类话题 |
| [#33638 项目级内存过滤](https://github.com/NousResearch/hermes-agent/issues/33638) | 2026-05-28 | 92天 | Feature | P3 | MEMORY.md按需过滤，3+个月无进展 |

### 待合并关键PR

- **PR #90201** — Python 3.14 `daemon_pool` 兼容性修复（对应P2 bug #83992），等待合并
- **PR #83870** — Gateway multiplex上下文文件按profile隔离，收到多个risk标签（session-state/message-delivery/compatibility），涉及面较大需仔细评审
- **PR #92526** — Cron保留profile密钥作用域，涉及多profile凭据安全，建议优先评审

---

*报告生成时间：2026-08-28 | 数据来源：[Hermes Agent GitHub](https://github.com/NousResearch/hermes-agent) | 统计周期：过去24小时*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期：** 2026-08-28  
**数据窗口：** 过去 24 小时

---

## 1. 今日速览

PicoClaw 在过去的 24 小时内保持温和活跃度：共产生 3 条 Issue 更新和 7 条 PR 更新，无新版本发布。值得关注的是，社区依赖升级 PR 批量关闭（5 个 dependabot PR 因 stale 标记被清理），同时有一条新的 UI 性能修复 PR 提交，以及一条关于 IRC 长消息支持的 Feature 请求仍在持续讨论中。整体来看，项目处于稳定维护期，核心开发节奏放缓，但社区仍在对细节体验和新功能提出改进建议。

**活跃度评估：** 中等偏低——主要活动来自自动化依赖更新和零星的人工贡献。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日共关闭/合并 6 个 PR，其中最有意义的是：

| PR | 标题 | 状态 | 说明 |
|---|---|---|---|
| [#1555](https://github.com/sipeed/picoclaw/pull/1555) | fix: merge PR #1390 #1389 #1383 #1381 | 已关闭 | 合并了 4 个遗留 PR 的修复，涵盖多项历史累积的 bug 修复，建议维护者在 release notes 中确认具体包含哪些变更 |

其余 5 个关闭的 PR 均为 **dependabot 自动化依赖升级**（见下表），皆为 stale 自动关闭：

| PR | 依赖 | 版本变更 |
|---|---|---|
| [#3336](https://github.com/sipeed/picoclaw/pull/3336) | aws-sdk-go-v2/service/bedrockruntime | 1.53.3 → 1.57.1 |
| [#3335](https://github.com/sipeed/picoclaw/pull/3335) | aws-sdk-go-v2/config | 1.32.25 → 1.32.35 |
| [#3334](https://github.com/sipeed/picoclaw/pull/3334) | anthropic-sdk-go | 1.55.1 → 1.62.0 |
| [#3333](https://github.com/sipeed/picoclaw/pull/3333) | maunium.net/go/mautrix | 0.27.0 → 0.29.0 |
| [#3332](https://github.com/sipeed/picoclaw/pull/3332) | aws-sdk-go-v2 | 1.42.0 → 1.43.4 |

> ⚠️ **值得注意：** 这 5 个依赖升级 PR 均为 8 月 13 日创建、8 月 27 日因 stale 关闭，说明维护者**未在两周内及时合并或处理**。其中 anthropic-sdk-go 和 mautrix 均为重要依赖，建议维护团队尽快手动跟进这些升级，确保不落后于上游修复。

**新增 PR（待合并）：**

- **[#3347](https://github.com/sipeed/picoclaw/pull/3347) [OPEN] fix laggy interface** — 贡献者 iMilnb 修复了 Web UI 在聊天区域文本较多时的卡顿问题，并已在桌面和移动端（Brave 浏览器）测试通过。作者自述非 TS/Node 专业人员，修复经过 AI 辅助分析。这是今日唯一的非自动化人工 PR，建议维护者优先 review。

---

## 4. 社区热点

### 最热 Issue：#3287 — IRC 长消息支持

- **链接：** [sipeed/picoclaw Issue #3287](https://github.com/sipeed/picoclaw/issues/3287)
- **状态：** Open（已持续讨论 37 天，8 条评论）
- **诉求：** PicoClaw 需要将 IRCv3 协议中超过 512 字节被拆分的消息视为一条完整消息。IRC 默认限制 512 字节，超长消息会被客户端自动拆分，导致 PicoClaw 将其误判为多条独立消息。
- **分析：** 这是一个涉及 IRC 协议细节的实战问题，反馈者来自真实使用场景。虽然评论数不算高（8条），但持续讨论一个月仍未关闭说明维护者可能对 IRC 适配的优先级不高，或该功能涉及底层重构需要更多时间评估。

---

## 5. Bug 与稳定性

今日**无新 bug 报告**。唯一与稳定性相关的信息来自新 PR：

- **[#3347](https://github.com/sipeed/picoclaw/pull/3347)**（待合并）：修复 Web UI 聊天区域文本量过大时界面卡顿（laggy）的问题。严重程度：中等——影响长对话场景的可用性，但已有修复提交。

---

## 6. 功能请求与路线图信号

今日活跃的 Feature 请求共 3 条（1 条 Open，2 条新关闭为 stale）：

| Issue | 标题 | 状态 | 信号强度 |
|---|---|---|---|
| [#3287](https://github.com/sipeed/picoclaw/issues/3287) | Better support long messages in IRC | **Open** | 高 — 持续讨论中，真实使用痛点 |
| [#3331](https://github.com/sipeed/picoclaw/issues/3331) | 支持任意 `/audio/transcriptions` 端点模型（不限于 `*-whisper-*`） | 已关闭（stale） | 中 — 反映当前 ASR 模型选择过于受限，用户希望扩展兼容性 |
| [#3330](https://github.com/sipeed/picoclaw/issues/3330) | delegate/spawn/subagent 工具支持调用时动态指定模型 | 已关闭（stale） | 中 — 用户希望子任务可覆盖默认模型配置，提升灵活性 |

> 📌 **路线图判断：** #3287（IRC 长消息）仍保持 Open，说明可能被纳入后续版本考虑；#3330 和 #3331 虽被 stale 关闭，但其诉求（模型灵活配置）与生态趋势一致，建议维护者评估是否以较小改动（如配置项扩展）来满足。综合来看，**模型可配置性和协议兼容性**是当前社区最关注的两大方向。

---

## 7. 用户反馈摘要

从今日活跃 Issue 评论中可提炼：

- **IRC 长消息痛点（#3287）：** 用户实际部署中遇到 IRC 消息被拆分为多条、导致 PicoClaw 逻辑混乱的问题，影响对话连贯性。这是协议层面的硬限制，需要框架级支持。
- **ASR 模型选择受限（#3331）：** 用户反映当前仅支持 `*-whisper-*` 命名的模型，但 newer 或自部署的语音转写模型（符合 OpenAI `/audio/transcriptions` 接口）无法被识别，导致被迫使用老旧/缓慢的模型。
- **子任务模型固定（#3330）：** 用户期望在 `delegate` / `spawn` / `subagent` 工具中灵活指定模型，当前静态配置无法满足不同子任务对模型能力/成本的不同需求。

**总体感受：** 社区用户多为技术型深度使用者，对协议细节（IRC）、模型生态兼容性和灵活配置有较高期待。

---

## 8. 待处理积压

以下项需维护者关注：

| 类型 | 编号 | 摘要 | 积压时长 | 建议 |
|---|---|---|---|---|
| **PR（依赖）** | [#3336](https://github.com/sipeed/picoclaw/pull/3336) | bedrockruntime SDK 升级至 1.57.1 | 2 周+（已 stale 关闭） | 手动跟进，确认兼容性后合并 |
| **PR（依赖）** | [#3334](https://github.com/sipeed/picoclaw/pull/3334) | anthropic-sdk-go 升级至 1.62.0 | 2 周+（已 stale 关闭） | **高优先级** — 涉及 Anthropic API 兼容，建议尽快手动 merge |
| **PR（依赖）** | [#3333](https://github.com/sipeed/picoclaw/pull/3333) | mautrix 升级至 0.29.0 | 2 周+（已 stale 关闭） | 高优先级 — Matrix 协议库，建议跟进新特性与修复 |
| **Issue** | [#3287](https://github.com/sipeed/picoclaw/issues/3287) | IRC 长消息支持 | Open 37 天 | 建议给出是否纳入路线图的明确回复，避免用户等待 |
| **Issue** | [#3330](https://github.com/sipeed/picoclaw/issues/3330) | 子代理动态模型覆盖 | 已 stale 关闭 | 如接受该功能方向，请 reopen 并规划实现 |

---

*本日报由 AI 生成，数据来自 PicoClaw GitHub 仓库公开信息。*  
*项目地址：github.com/sipeed/picoclaw*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期：2026-08-28** | **数据窗口：过去 24 小时** | **数据源：github.com/qwibitai/nanoclaw**


## 1. 今日速览

NanoClaw 在过去 24 小时保持高度活跃：**11 条 Issue 更新（10 新开/活跃，1 关闭）与 50 条 PR 更新（46 待合并，4 已合并/关闭）**，呈现出典型的开源项目高速迭代状态。值得关注的是，**核心团队（core-team）成员 zvi-fried 与 amit-shafnir 密集提交了一批 provider 层重构 PR**（#3581-#3593），指向项目正在系统性地推进 provider 契约标准化工作。社区反馈方面，**Discord 通道的附件丢失（#2888）与按钮参数损坏（#3456）两个高严重度 Bug 仍在发酵**，且 Telegram 通道存在依赖锁定导致的 Markdown 解析缺陷（#3569），稳定性问题仍需团队优先关注。整体而言，项目功能开发节奏迅猛，但通道适配层的稳定性短板已开始显现。


## 2. 版本发布

**无新版本发布。**

过去 24 小时内未检测到任何 Releases。结合 PR 积压情况（46 个待合并），上游可能正在为一次较大规模的合并做准备，建议关注 `providers` 分支上的一系列重构 PR 动向。


## 3. 项目进展

### 3.1 已合并/关闭 PR（4 条）

**★ 高价值合并：Codex Provider 错误处理修复**

> **PR #3594** — _[Fix] fix(tasks): account errored task turns as FAILED runs instead of dropping them_ · 作者：chiptoe-svg
> 🔗 https://nanocoai/nanoclaw PR #3594

该 PR 修复了 **#3223**——此前定时任务执行出错与"正常运行但未发消息"无法区分，导致任务失败被静默吞掉。修复方案将错误信息以 `chat` 消息形式写入，并复制触发方路由字段。**该修复对依赖定时任务的可观测性有实质提升**，任务失败不再对系统不可见。

其余 3 条合并/关闭的 PR 数据未完整回传（数据采样限制），建议查看 GitHub 页面获取详情。

### 3.2 正在进行中的大型重构方向

核心团队（zvi-fried）正在推进 **provider 层契约标准化** 的系列重构，今日活跃 PR 包括：

| PR | 内容 | 状态 |
|---|---|---|
| #3584 | 实现 codex provider 契约 | 开放 |
| #3585 | 声明 host provider 契约 | 开放 |
| #3586 | 声明 setup provider 契约 + 安装验证器 | 开放 |
| #3588 | 实现 opencode provider 契约 | 开放 |
| #3591 | 从核心权威源渲染 provider 指令 | 开放 |
| #3592 | 核心拥有的 tone/speed 推理属性 | 开放 |
| #3593 | 将核心 tone/speed 映射到 personality/service tier | 开放 |

**信号解读：** 这一系列 PR 表明 NanoClaw 正在从"各 provider 各自为政"向 **"核心定义契约，provider 负责实现"** 的架构演化。方向正确，但 7 个 PR 并行推进也带来合并冲突风险，建议维护者规划合并顺序。

> 🔗 参考：[PR #3584](https://nanocoai/nanoclaw PR #3584) · [#3585](https://nanocoai/nanoclaw PR #3585) · [#3586](https://nanocoai/nanoclaw PR #3586) · [#3588](https://nanocoai/nanoclaw PR #3588) · [#3591](https://nanocoai/nanoclaw PR #3591) · [#3592](https://nanocoai/nanoclaw PR #3592) · [#3593](https://nanocoai/nanoclaw PR #3593)


## 4. 社区热点

### 热点一：Discord 按钮 `value` 参数损坏（高严重度）

> **Issue #3456** — _chat-sdk-bridge: redundant Button 'value' param corrupts Discord approval custom_id_
> 👥 5 条评论 | 🔗 https://nanocoai/nanoclaw Issue #3456

**核心诉求：** 用户在 Discord 上发起 approval/ask_question 卡片时，**每次点击都解析到错误选项**，功能完全不可用。根因是 `createChatSdkBridge` 的 `ask_question` 卡片构建器中，每个选项按钮同时设置了 `id` 和 `value` 两个参数，导致 Discord 的 `custom_id` 被污染。

**社区反应：** 该 Issue 虽创建于 8/23，但到昨天（8/27）仍持续收到新评论，说明有多个用户受此问题困扰。**严重度高，覆盖面为所有 Discord 用户。**

### 热点二：附件/图片在 URL-only 通道中被丢弃

> **Issue #2888** — _Discord (and likely other url-only chat-sdk adapters) drop image/file attachments_
> 👥 2 条评论 | 🔗 https://nanocoai/nanoclaw Issue #2888

**核心诉求：** Discord 用户发送图片/截图/文件时，agent 只收到元数据（`{type, name, mimeType, size}`），**内容永远不会被下载**。Telegram 正常工作。用户 `eagansilverpathmarketing` 明确表示根因在 `messageToInbound` 只调用 `att.fetchData`，但适配器只提供了 `url`。

**社区反应：** 该 Issue 已存在近两个月（6/30 创建），期间 #3572 提出过类似问题又被关闭，说明修复进展缓慢，**社区耐心正在消耗**。

### 热点三：注册表技能 `nc:copy` 列表漂移

> **Issue #3579** — _registry skills: prevent nc:copy lists from drifting from channels/providers_
> 👥 0 条评论（新开） | 🔗 https://nanocoai/nanoclaw Issue #3579

**核心诉求：** 用户 `glifocat` 指出，注册表支撑的 channel/provider 技能可能与实际安装内容**静默漂移**——实现文件在长期存在的 `channels`/`providers` 分支上，而 `nc:copy` 配方在 `main` 分支上，两者之间缺少一致性校验。

**信号：** 虽然是新开 Issue，但这也是 glifocat 今日报告的第三个问题（另见 #3529、#3532），**说明该用户在深度使用后系统性暴露了项目维护方面的短板**。


## 5. Bug 与稳定性

按严重程度降序排列：

| 严重度 | Issue | 描述 | 状态 |
|---|---|---|---|
| 🔴 高 | [#3456](https://nanocoai/nanoclaw Issue #3456) | Discord approval 卡片按钮 `value` 参数损坏 `custom_id`，每次点击解析到错误选项 | 无 fix PR |
| 🔴 高 | [#2888](https://nanocoai/nanoclaw Issue #2888) | Discord 及类似 URL-only 适配器丢弃图片/文件附件，agent 只见文件名 | **#3572 曾报告后被关闭**，无有效修复 |
| 🟠 中高 | [#3569](https://nanocoai/nanoclaw Issue #3569) | Telegram 固定在 `@chat-adapter/telegram@4.29.0`，上游 4.32.0 已修复 MarkdownV2 奇数下划线 URL 不投递的问题 | 无 fix PR |
| 🟠 中高 | [#3568](https://nanocoai/nanoclaw Issue #3568) | 待处理 `system` 行耗尽入站队列，agent 静默停止响应（`maxMessagesPerPrompt` 默认 10） | 无 fix PR |
| 🟠 中 | [#3576](https://nanocoai/nanoclaw Issue #3576) | 限流回合在 `deliverErrorResult` 无 backoff/dedup，重复重试产生重复错误通知 | 无 fix PR |
| 🟡 中低 | [#3575](https://nanocoai/nanoclaw Issue #3575) | WhatsApp 单张超 2000px 图片导致整个 SDK 会话持续失败，需手动 `/clear` | 用户自带 fix 建议 |

**观察：** 今日 6 个 Bug 类 Issue 中 **5 个尚无对应 fix PR**，且 #2888 的修复尝试（#3572）被关闭后问题仍然存在。**稳定性缺口集中在通道适配层，建议团队将附件处理列为 P0 技术债。** **#3575 值得注意——用户直接给出了具体修复建议（长边缩至 2000px），是低门槛的 PR 切入点。**


## 6. 功能请求与路线图信号

### 6.1 明确的社区功能需求

| Issue | 需求 | 信号强度 |
|---|---|---|
| [#3577](https://nanocoai/nanoclaw Issue #3577) | **自动接入唯一可用的 agent-group**，而非每次 @-提及都弹"选择 agent"选择器 | ★★★ 用户明确描述使用场景痛点 |
| [#3532](https://nanocoai/nanoclaw Issue #3532) | **`add-*-tool` 的作用域应对后创建的 agent 生效**（当前新 group 默认获得工具，绕过权限控制） | ★★★ 安全/权限边界问题 |
| [#3529](https://nanocoai/nanoclaw Issue #3529) | **update-nanoclaw 技能刷新应跳过本地自建适配器**，或提供 opt-out | ★★☆ 影响自定义扩展的用户 |

### 6.2 路线图信号（来自 PR 侧） 

- **Provider 契约标准化**（zvi-fried 系列 PR）：核心定义、provider 实现的架构方向已非常明确
- **Gemini Provider 支持**（PR #2136，farooqu）：从 4 月底开放至今仍在等待合并，**该 PR 可能被上述重构所阻塞，建议维护者明确其与契约重构的关系**
- **OpenCode 本地 LLM 支持**（PR #1995，TeeJS）：`/add-local-llama` 技能瞄准本地 Ollama/llama.cpp 等场景，需求潜力大

> 🔗 参考：[PR #2136](https://nanocoai/nanoclaw PR #2136) · [PR #1995](https://nanocoai/nanoclaw PR #1995) · [PR #1994](https://nanocoai/nanoclaw PR #1994)


## 7. 用户反馈摘要

### 真实用户痛点

| 场景 | 用户反馈 | 来源 |
|---|---|---|
| Discord 审批流 | "every click resolves to the wrong option"——每次点击都解析到错误选项 | [#3456](https://nanocoai/nanoclaw Issue #3456) |
| Discord 附件 | "agent receives only attachment metadata — never the content" | [#2888](https://nanocoai/nanoclaw Issue #2888) |
| Telegram 链接 | "URLs with an odd number of underscores never deliver"——奇数下划线计数导致消息永远不投递 | [#3569](https://nanocoai/nanoclaw Issue #3569) |
| WhatsApp 大图 | "one big photo... agent looks dead, and it stays dead for hours"——大图导致数小时不可用 | [#3575](https://nanocoai/nanoclaw Issue #3575) |
| 入站静默失活 | "agent silently stops responding"——无任何错误提示 | [#3568](https://nanocoai/nanoclaw Issue #3568) |
| 更新流程破坏本地扩展 | "My own adapter blocks the update" / "local adapters fail validation or get overwritten" | [#3529](https://nanocoai/nanoclaw Issue #3529) |

### 满意度信号

负面信号占主导，但均为**功能性 Bug 而非设计理念分歧**。用户在指出问题时通常提供详细根因分析（#3575 附 API 错误原文，#3456 附代码定位），说明社区质量高、参与深度好。正面信号方面，核心团队的 provider 契约重构 PR 密集且标注 `core-team`，表明**内部开发资源投入充足，项目商业化/平台化方向明确**。


## 8. 待处理积压

### 8.1 长期未响应/未合并的重要 PR

| PR | 内容 | 等待时长 | 风险 |
|---|---|---|---|
| [#2136](https://nanocoai/nanoclaw PR #2136) | **Google Gemini Provider 支持** | 122 天（4/29 创建） | Gemini 用户持续流失 |
| [#1995](https://nanocoai/nanoclaw PR #1995) | OpenCode 自定义 npm + 无认证 + 本地 LLM | 127 天（4/24 创建） | 与 #2136 同属 provider 扩展，可能被契约重构阻塞 |
| [#1994](https://nanocoai/nanoclaw PR #1994) | 按 group 路由自定义 OpenAI 兼容端点 | 127 天（4/24 创建） | 同上 |
| [#2878](https://nanocoai/nanoclaw PR #2878) | Codex 静态 OpenAI secret 重连（core-team） | 62 天（6/28 创建） | 认证流程缺陷持续影响生产 |

### 8.2 长期未关闭的高严重度 Issue

| Issue | 内容 | 存活时长 | 状态 |
|---|---|---|---|
| [#2888](https://nanocoai/nanoclaw Issue #2888) | Discord 丢弃附件 | 60 天 | 修复尝试被关闭，问题仍在 |

### 8.3 维护者行动建议

1. **优先合并 #2878（Codex 认证修复）**——core-team 标记、62 天未合，直接影响生产环境可靠性
2. **明确 #2136（Gemini）与 provider 契约重构的关系**——若重构不兼容，应关闭并指导作者适配；若兼容，应给出合并时间表
3. **对 #2888（附件丢弃）给出官方回应**——该问题已两次被报告、一次修复被关闭，社区需要明确的处理计划


## 附：项目健康度评价

| 维度 | 评价 | 说明 |
|---|---|---|
| **活跃度** | 🟢 极高 | 24h 内 11 Issues + 50 PRs，核心团队持续投入 |
| **开发节奏** | 🟢 快 | 大量 Feature/Refactor 并行推进 |
| **稳定性** | 🟡 中 | 6 个 Bug 类 Issue 集中爆发，5 个无 fix PR |
| **社区健康度** | 🟢 良好 | 用户反馈质量高，提供根因分析；但高严重度 Bug 修复周期过长 |
| **技术债** | 🟡 需关注 | 通道适配层（chat-sdk-bridge）问题集中，附件处理、Telegram 依赖锁定等均为长期欠账 |
| **风险信号** | ⚠️ | PR 积压 46 个待合并 + 7 个契约重构并行，合并冲突概率高；gemini/本地 LLM 等外部贡献 PR 长期积压可能挫伤贡献者积极性 |

---

*本报告由 AI 分析师自动生成，基于 2026-08-28 的 GitHub 公开数据。数据采样限制：部分 PR 评论数未完整回传（显示为 undefined），已合并 PR 详情需以 GitHub 实际记录为准。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-28

---

## 1. 今日速览

项目活跃度 **高**：过去24小时新增/活跃 Issue 25 条、关闭 8 条；PR 更新 48 条（其中 31 条已合并/关闭，17 条待合并）。核心方向聚焦于 **记忆系统（memory）多阶段落地**（#7947–#7953 八个相关 Issue 同步推进）、**Gmail/MCP 工具输出规范化**（#7960/#7963/#7964/#7968）以及 **CI 基础设施集中化**（#7943/#7967）。无新版本发布，但 PR #7954（累计压缩上下文屏障）与 #7907（内存写入 CAS 保护）已合入，标志着上下文管理和数据一致性进入新阶段。值得关注的是，**深层记忆持久化** 与 **学习路由** 作为史诗级功能（#7864/#7276）正在密集拆解落地。

---

## 2. 版本发布

过去24小时无新版本发布。

---

## 3. 项目进展

**今日合并/关闭的关键 PR：**

| PR | 标题 | 影响 |
|---|---|---|
| [#7954](https://github.com/nearai/ironclaw/pull/7954) | feat(threads): add cumulative compaction context barrier | 压缩输出从独立范围摘要升级为**累计上下文屏障**，跨循环运行折叠最新持久化屏障，大幅降低长对话的上下文膨胀问题 |
| [#7907](https://github.com/nearai/ironclaw/pull/7907) | fix(memory): reject stale full-document rewrites | 为 `memory.write` 增加 `expected_content_hash` 校验，解决并发覆写问题（对应 [#7776](https://github.com/nearai/ironclaw/issues/7776)） |
| [#7944](https://github.com/nearai/ironclaw/pull/7944) | feat(gmail): surface semantic message output | Gmail 消息在 producer 边界即完成 base64url 解码、HTML→Markdown 转换、语义头筛选，为修复 #7891 的性能问题奠定基础 |
| [#7941](https://github.com/nearai/ironclaw/pull/7941) | fix(slack): admit broadcast mention via app_mention exemption | 修复 Slack"同时发送到频道"（`thread_broadcast`）被错误忽略的问题 |
| [#7943](https://github.com/nearai/ironclaw/pull/7943) | ci: compile integration batches once | 集成测试批次合并为单次编译+单次执行，CI 效率显著提升 |
| [#7893](https://github.com/nearai/ironclaw/issues/7893)（已关闭） | feat(memory): per-automation lessons file | 自动化运行间经验持久化，配套实现已合入 |

**整体判断：** 项目在 **上下文管理** 和 **记忆系统** 两条主线取得实质性进展，Gmail 扩展的语义输出为后续性能修复合入铺路。CI 基础设施的集中化表明项目正进入规模化工程阶段。

---

## 4. 社区热点

**🔥 最热 Issue：[#7891](https://github.com/nearai/ironclaw/issues/7891) — Gmail 扩展导致单轮 19.7 秒推理延迟（10 条评论）**

两个 `gmail.get_message` 调用仅耗时 274ms/290ms，但模型推理却消耗了 19.2 秒——原因是 49KB 原始 MIME 头未经投影被直接推入 prompt。社区讨论聚焦于 **扩展输出投影机制** 和 **24 KiB 盲目截断策略** 的合理性。该问题的修复路径已清晰：PR #7944 的语义输出 + [#7960](https://github.com/nearai/ironclaw/issues/7960)（HTML 复杂度限制）双重保障。

**💬 值得关注：[#7824](https://github.com/nearai/ironclaw/issues/7824) — 上下文压缩屏障（4 条评论）**

PinchBench 数据显示完整历史回放导致 input tokens 从 55.1M 暴增至 227.7M（成本 $2.52→$10.31），社区对 Pi 风格的压缩屏障方案讨论升温。PR #7954 已合入第一版实现。

**👥 新涌现：[#7856](https://github.com/nearai/ironclaw/issues/7856) — MCP 工具发现静默跳过 camelCase 名称**

用户 `Kampouse` 报告托管 MCP 发现机制要求工具名直接可作为标识符，导致 camelCase 工具被静默丢弃。该问题与 #7891 同样指向 **工具目录健全性**，预计后续会有修复 PR。

---

## 5. Bug 与稳定性

| 严重度 | Issue | 描述 | 状态 |
|---|---|---|---|
| **高** | [#7891](https://github.com/nearai/ironclaw/issues/7891) | Gmail MIME 头未投影导致单轮推理 19.7 秒 | 修复中（#7944 已合入 + #7960 待合入） |
| **中** | [#6590](https://github.com/nearai/ironclaw/issues/6590) | Windows 下 `serve` 失败："workspace root must not overlap default skill root /skills"（3 条评论） | 待处理，评论建议需要路径规范化 |
| **中** | [#7936](https://github.com/nearai/ironclaw/issues/7936) | Nightly Reborn Playwright（陈旧 landing-copy fixtures + attachment 流程）与 Postgres stress API 503 就绪门禁失败 | 已定位根因，待修复 |
| **中** | [#7940](https://github.com/nearai/ironclaw/issues/7940) | MCP OAuth 缺少顶层 `resource` 参数；始终使用已弃用的 DCR 而非 CIMD | 待处理 |
| **低** | [#7956](https://github.com/nearai/ironclaw/issues/7956) | Telegram 未配对用户 `/start` 显示命令清单而非配对提示 | 待处理 |
| **低** | [#7955](https://github.com/nearai/ironclaw/issues/7955) | Telegram 个人账户链接在未配置 api_id/api_hash 时显示通用错误 | 待处理，建议给出配置指引 |

**稳定性观察：** #7936 暴露了 Nightly 管线的脆弱性（陈旧 fixtures + 503 门禁），已作为独立 Issue 跟踪。无崩溃级回归报告。

---

## 6. 功能请求与路线图信号

**🧠 记忆系统（史诗 [#7276](https://github.com/nearai/ironclaw/issues/7276)，今日拆解 8 个 Issue）：**

| Issue | 内容 | 判断 |
|---|---|---|
| [#7947](https://github.com/nearai/ironclaw/issues/7947) | 共享学习路由、设置、持久化候选存储 | 已出对应 PR #7958（待合并） |
| [#7948](https://github.com/nearai/ironclaw/issues/7948) | 稳定的 commit/feedback/forget 能力 | 规划中 |
| [#7949](https://github.com/nearai/ironclaw/issues/7949) | 确定性准入 + 自动/审批晋升 | 规划中 |
| [#7950](https://github.com/nearai/ironclaw/issues/7950) | native/mem0/Mnesis 学习能力适配器 | 规划中 |
| [#7951](https://github.com/nearai/ironclaw/issues/7951) | 有界主动召回 | 规划中 |
| [#7952](https://github.com/nearai/ironclaw/issues/7952) | 学习审查路由至技能蒸馏 | 规划中 |
| [#7953](https://github.com/nearai/ironclaw/issues/7953) | 可观测性、评估、provider 迁移门禁 | 规划中 |

**🎙️ 其他信号：**
- **[#7867](https://github.com/nearai/ironclaw/issues/7867) — WebUI 语音输入**：用户明确表示 Slack/Telegram 均支持语音而 Web 端缺失，属于渠道一致性缺口，预计会进入后续迭代
- **[#7938](https://github.com/nearai/ironclaw/issues/7938) — 大线程工件下载流式化**：当前在服务端内存中多次序列化+完整解析，效率低下，属架构优化项
- **[#7903](https://github.com/nearai/ironclaw/issues/7903) — 持久化 per-user 沙箱执行器决策 spike**：已在 PR #7908 中推进 spike 实现
- **[#7939](https://github.com/nearai/ironclaw/issues/7939) — 从废弃 PR 中回收仍有价值的工作**：10 个过期 PR 包含可能有用的需求/测试，维护者可优先审查

---

## 7. 用户反馈摘要

**😊 正面信号：**
- 记忆系统从 Issue 到 PR 的快速落地获得社区认可（#7276 系列 Issue 均由核心贡献者提出，响应迅速）
- Slack 广播提及修复（#7941）解决了实际用户场景

**😠 痛点集中：**
- **性能敏感**（#7891）：用户对扩展输出未经投影即入 prompt 表示不满，49KB 无关注入导致 19 秒推理浪费是"不可接受的"
- **配置可发现性**（#7920）：学习技能提取功能依赖未文档化的环境变量 `IRONCLAW_SKILL_LEARNING_MODEL`，缺失时静默禁用，用户无法从产品界面发现或启用
- **错误提示质量**（#7955）：配置缺失时用户看到的是通用的"Something went wrong"而非明确的配置指引，增加排查成本
- **工具收录可靠性**（#7856）：camelCase 工具被静默跳过，用户无法感知，排查困难

**📊 数据支撑：**
- #7891 提供了完整的性能数据（274ms 工具调用 vs 19.2s 推理），社区讨论认可数据驱动的分析方式
- #7824 引用 PinchBench 对比数据（227.7M vs 55.1M tokens），为压缩屏障提供了量化论证

---

## 8. 待处理积压

**⚠️ 需维护者关注：**

| 项目 | 创建时间 | 持续天数 | 说明 |
|---|---|---|---|
| [#6590](https://github.com/nearai/ironclaw/issues/6590) Windows serve 失败 | 2026-07-23 | **36 天** | 长期未响应，Windows 本地开发被阻塞，社区有 3 条评论建议但无官方回应 |
| [#5671](https://github.com/nearai/ironclaw/issues/5671) LeakDetector 每次 JSON 字符串重建 | 2026-07-06 | **53 天** | 性能优化项，`redact_output` 递归遍历中每次调用都重建检测器，虽已关闭但值得确认修复是否彻底 |
| [#4491](https://github.com/nearai/ironclaw/issues/4491) Slack AI 流式进度 | 2026-06-05 | **84 天** | 明确的短期补丁方案已被接受，但长期流式方案未推进 |
| [#7856](https://github.com/nearai/ironclaw/issues/7856) MCP camelCase 工具跳过 | 2026-08-24 | 4 天 | 用户报告后无回应 |

**📋 今日关闭：**
- [#3278](https://github.com/nearai/ironclaw/issues/3278) MissionService 与 TurnCoordinator 集成定义 — 跟踪器清理完成
- [#7776](https://github.com/nearai/ironclaw/issues/7776) memory.write 并发覆写 — 由 #7907 修复
- [#7876](https://github.com/nearai/ironclaw/issues/7876) 通知生产者生命周期加固 — 已合入

---

**总结：** IronClaw 今日呈现 **高活跃度、强执行力** 的状态。记忆系统多阶段拆解推进展示了清晰的路线图执行力，上下文管理与 Gmail 性能问题在同一周期内修复+优化并举。需关注 Windows 本地开发阻塞问题（36 天未响应）和 MCP 工具发现的静默失败，这两项直接影响外部开发者和用户体验。整体项目健康度良好，核心架构（上下文、记忆、CI）正在经历系统性升级。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-28

> 项目健康度评估：**健康** | 综合活跃度：**高** | 关键信号：**发布周期稳定，PR 合并率 100%，Bug 响应及时**


## 1. 今日速览

过去 24 小时 LobsterAI 保持了高强度的迭代节奏：13 条 PR 全部完成合并/关闭，无滞留待合并项，且已关闭的 5 条 Issue 均为长期遗留的 stale 问题（3 月底创建），说明维护团队在持续清理技术债务。新版本 **2026.8.26** 于 8 月 26 日发布，主要修复 Windows 安装器的静默安装行为。当前最值得关注的信号是：**两条新开的 Issue（#2561、#2562）均指向安装器在升级时可能删除用户项目文件夹、以及模型调用扣费异常的问题，涉及用户数据安全与资费敏感度，建议优先跟进。** 整体来看，项目发布节奏稳定、PR 流程高效，处于健康活跃状态。


## 2. 版本发布

### LobsterAI 2026.8.26（8 月 26 日发布）

**更新内容：**
- `fix(installer)`: 支持静默上传优先的 Web 构建（PR #2511）
- `fix(installer)`: 为 dictbind 静默安装包隐藏横幅（PR #2512）

**破坏性变更：** 无明确破坏性变更。但结合今日 Issue #2561 反馈，**安装器升级时若项目文件夹位于安装目录内，可能被整体删除（用户报告损失约 2000 credits）**。若您将项目目录放在 LobsterAI 安装根目录下，**升级前建议先备份或迁移至独立路径**。开发团队已注意到该问题，修复补丁预计在后续版本中推出。


## 3. 项目进展

今日共合并/关闭 13 条 PR，按功能领域归纳如下：

| 领域 | PR 数 | 关键变更 |
|------|-------|----------|
| UI/渲染层（renderer） | 6 | 模型列表可折叠分组、侧边栏横幅计划、资料库缩略图渲染优化、登录 CTA 彩虹动画等 |
| 安装器/构建（installer/build） | 3 | Windows 安装器静默安装行为修正、截断载荷加固 |
| 核心逻辑（main） | 2 | 应用更新保留就绪状态、横幅同步调度 |
| 文档与测试（docs/test） | 2 | 早前提交（#1163、#1165）的 Stale 合并，含定时任务交互优化与 75 个 Vitest 单元测试 |

**本日最重要的 PR：**
- **#2568** (`feat: collapse more models and sync sidebar banner schedules`) — 将可选模型归入默认折叠的“更多模型”区，同时引入服务器同步横幅调度（含客户端版本门控、本地过期、缓存处理与刷新恢复）。功能面向用户体验优化，对侧边栏信息架构影响较大。
- **#2566** (`fix: win installer truncated payload hardening`) — 针对 Windows 安装器载荷截断的加固，与今日新 Issue #2561（升级删除工程）属于同一风险域。
- **#2565** (`fix(library): 优化列表查询切换与重新加载状态`) — 消除列表切换时的闪烁与重复骨架屏，修复旧查询结果污染当前列表的并发问题。


## 4. 社区热点

今日最活跃的讨论集中在两条新 Issue 上，均为用户 `dreamsdesign` 在同一天提出，评论互动频繁：

### 🔥 Issue #2561 — installer 升级时删除整个项目文件夹
- **链接：** https://github.com/netease-youdao/LobsterAI/issues/2561
- **创建时间：** 2026-08-27（1 条评论）
- **内容：** 用户反馈升级时安装器会“nuke and wipe”整个项目文件夹（若其位于安装目录内），损失约 2000 credits。
- **诉求分析：** 这是典型的数据安全敏感问题，与安装器路径处理和升级清理逻辑相关。用户语气强烈，涉及实际资产损失，建议优先响应。

### 🔥 Issue #2562 — 敏感词触发高额扣费
- **链接：** https://github.com/netease-youdao/LobsterAI/issues/2562
- **创建时间：** 2026-08-27（暂无评论）
- **内容：** 用户声称输入脏话被扣约 200 credits/次，总计损失约 800 credits，且与 DeepSeek 无关。
- **诉求分析：** 用户对模型的计费机制与内容审核逻辑产生疑虑。这可能是侧边栏模型（如 DeepSeek 之外的自定义模型）的计费统计异常，或是 Prompt 注入导致的额外调用。该问题直接关联用户资费，**建议核查计费链路与内容过滤是否产生额外 API 调用**。

### 历史 Issue 的陈旧关闭
今日关闭的 5 条 Issue（#1179、#1162、#1173、#1174、#1180）均为 3 月 31 日创建，被标记为 `[stale]` 后统一关闭。其中 **#1173（卸载后程序仍可运行）** 与 **#1180（修改自建 agent 触发网关反复重启）** 曾涉及敏感稳定性问题，虽关闭但值得复盘修复有效性。


## 5. Bug 与稳定性

| 严重程度 | Issue/PR | 描述 | 状态 |
|----------|----------|------|------|
| 🔴 严重 | [#2561](https://github.com/netease-youdao/LobsterAI/issues/2561) | 升级时若项目文件夹在安装目录内会被整体删除 | **待修复**，尚无直接 fix PR；相关加固 PR #2566 已合并 |
| 🔴 严重 | [#2562](https://github.com/netease-youdao/LobsterAI/issues/2562) | 敏感词触发模型扣费约 200 credits/次 | **待排查**，暂无 fix PR |
| 🟠 中等 | [#1180](https://github.com/netease-youdao/LobsterAI/issues/1180)（已关闭） | 修改自建 agent 图标触发网关反复重启 | 已关闭（stale），3 月问题，建议验证当前版本是否仍可复现 |
| 🟡 轻微 | [#1173](https://github.com/netease-youdao/LobsterAI/issues/1173)（已关闭） | 卸载后程序窗口仍可运行并发送消息 | 已关闭（stale），仍建议排查卸载清理逻辑 |

**今日已合并的稳定性修复：**
- **#2551** — `fix: app update preserve ready state`（应用更新时保留就绪状态，防止更新流程状态丢失）
- **#2566** — Windows 安装器截断载荷加固（与 #2561 风险域一致，但未必直接解决路径删除问题）


## 6. 功能请求与路线图信号

| 功能需求 | 来源 | 状态 | 路线图判断 |
|----------|------|------|------------|
| 支持多个自定义模型提供商 | Issue [#1174](https://github.com/netease-youdao/LobsterAI/issues/1174)（已关闭） | 3 月提出，被 stale 关闭 | 结合今日 PR #2568 的“模型折叠”改动，**模型管理是近期重点**。多提供商支持虽未直接出现于 PR，但折叠交互表明列表在增长，有可能在后续迭代中加入。 |
| 侧边栏横幅计划（**服务端同步**） | PR [#2568](https://github.com/netease-youdao/LobsterAI/pull/2568) 已合并 | 已完成 | 表明团队在推进运营位配置的服务端化，对商业化/功能推广是利好信号 |
| 资料库缩略图渲染与资源管理 | PR [#2559](https://github.com/netease-youdao/LobsterAI/pull/2559) 已合并 | 已完成 | 资料库体验持续优化，后续可能涉及更丰富的文件类型支持 |
| 登录 CTA 彩虹动画 | PR [#2558](https://github.com/netease-youdao/LobsterAI/pull/2558) 已合并 | 已完成 | 登录转化率是当前优化方向之一，暗示商业化推进 |

**结论：** 今日无新功能请求，但可判断**模型管理、资料库、侧边栏运营位**是当前产品迭代的三个核心方向。


## 7. 用户反馈摘要

来自今日活跃 Issue 和评论的真实用户声音：

| 用户 | 反馈 | 情感倾向 | 分析 |
|------|------|----------|------|
| `dreamsdesign` | “升级过程中清除了整个项目文件夹，浪费了约 2000 credits” | 😠 愤怒/焦虑 | 对数据安全的极度不信任，可能导致用户流失。核心诉求是**安装器应默认保护用户数据目录** |
| `dreamsdesign` | “说了几个脏话就扣了 800 credits，跟 DeepSeek 没关系” | 😠 愤怒/困惑 | 对计费透明度和敏感词触发机制有疑虑，核心诉求是**检查是否存在异常计费** |
| `syrphid` | “3.31 强制沙箱找不到关闭按钮，回滚 3.30 正常” | 😕 困扰 | 沙箱策略变更缺少可见的用户控制入口，安全与易用性需平衡 |
| `773780238` | “卸载之后程序还能运行，是不是留后门？” | 😡 极度不信任 | 卸载残留进程触发严重信任危机，建议立即核查并公开说明 |

**共性痛点：** 用户对**数据安全、计费透明度、卸载/升级行为的可控性**极为敏感。建议团队在后续版本中强化安装/卸载流程的用户可见性与数据保护承诺。


## 8. 待处理积压

| 项目 | 类型 | 创建时间 | 备注 |
|------|------|----------|------|
| [#2561](https://github.com/netease-youdao/LobsterAI/issues/2561) 升级删除项目文件夹 | Issue | 2026-08-27 | 高优先级，涉及数据安全，需尽快 assign 并给出修复时间表 |
| [#2562](https://github.com/netease-youdao/LobsterAI/issues/2562) 敏感词扣费异常 | Issue | 2026-08-27 | 高优先级，涉及计费正确性，需尽快排查 |
| [#1179](https://github.com/netease-youdao/LobsterAI/issues/1179) 沙箱强制开启 | Issue（已关闭） | 2026-03-31 | 已被 stale 关闭，但用户曾明确反馈困扰，建议在新版本中重新评估沙箱的用户可控性 |
| [#1173](https://github.com/netease-youdao/LobsterAI/issues/1173) 卸载残留进程 | Issue（已关闭） | 2026-03-31 | 涉及用户信任，建议验证当前版本是否已修复 |

**维护者行动建议：**
1. 对 #2561、#2562 分配负责人，24 小时内给出初步响应
2. 在安装器中增加“检测到项目文件夹位于安装目录”时的警告或自动迁移流程
3. 对已 stale 关闭但风险等级较高的 Issue（#1173、#1180）进行回归验证，确认修复有效性后更新文档


*以上日报基于 2026-08-28 GitHub 数据自动生成。所有链接均可点击直达原始 Issue/PR。*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-08-28

## 1. 今日速览

过去24小时内，Moltis 项目整体活跃度处于**中等偏低**水平：无新增或活跃 Issue，2 条 PR 均从前几日创建进入合并/关闭流程（无待合并项）。**1 个新版本 20260827.01 于昨日发布**，但未附带独立的 Release Notes，推测为常规滚动更新。当前 PR 队列已完全清空，说明维护团队正在消化存量工作，但新输入（Issue）趋于停滞，值得关注后续是否存在开发节奏放缓或集中冲刺阶段。

## 2. 版本发布

**新版本：20260827.01**（发布日期：2026-08-27）
- **链接**：https://github.com/moltis-org/moltis/releases/tag/20260827.01
- 未附带独立 Release Notes 的滚动版本。结合同期合并的 PR 推断，该版本应包含下述两项修复（Web 沙箱镜像验证加固 + OpenAI 工具 Schema 兼容性修复）。
- **破坏性变更**：未声明，推测无重大破坏。
- **迁移注意事项**：`#1232` 涉及工具定义 Schema 变更，如自建客户端依赖 MCP 环境变量字段结构，建议验证兼容性。

## 3. 项目进展

今日 2 条 PR 完成合并/关闭，均属**修复性质**，分别解决安全验证与外部工具兼容性问题：

- **PR #1222** — `fix(web): validate sandbox image requests`（作者：tsauvajon）
  - **链接**：https://github.com/moltis-org/moltis/pull/1222
  - **内容**：为沙箱镜像引用与包名引入验证机制；将包检查和镜像构建操作限制为操作员管理员；保留密码、通行密钥及受信回环标识的完整管理权限。
  - **价值**：显著降低沙箱逃逸与未授权镜像拉取风险，属于安全加固类关键修复。

- **PR #1232** — `fix(tools): make object schemas OpenAI-safe`（作者：IlyaBizyaev）
  - **链接**：https://github.com/moltis-org/moltis/pull/1232
  - **内容**：OpenAI 严格工具 Schema 将对象关闭为 `additionalProperties=false`，导致未指定的 patch/map Schema 迫使 Codex 发送 null/空值。此 PR 显式声明 webhook 补丁字段，将 MCP 环境变量表示为固定键值对。
  - **价值**：解决了与 Codex 等 OpenAI 工具链集成时的数据丢失问题，提升外部生态兼容性。

## 4. 社区热点

今日无高热度讨论。两条今日关闭的 PR 均获得 0 评论、0 点赞，社区讨论沉淀较少。合并前 PR 从创建到合并分别耗时 7 天（#1222）和 5 天（#1232），节奏合理，但反映出当前社区活跃贡献者集中于少数核心维护者（两位 PR 作者均为常规贡献者）。

## 5. Bug 与稳定性

- **中等级（已修复）**：沙箱镜像请求未经校验即可被使用 — 可能被利用拉取恶意镜像或构造非法容器配置（PR #1222，已合并）。
- **低等级（已修复）**：OpenAI 严格模式下对象 Schema 未声明字段导致 Codex 发送 null/空值，破坏部分工具调用数据完整性（PR #1232，已合并）。属功能缺陷而非崩溃/回归。

无其他新增 Bug 报告。

## 6. 功能请求与路线图信号

今日无新增功能请求 Issue。但从 PR #1222 的权限模型调整可识别出**架构层面信号**：对操作员（operator）权限的细分（镜像构建与包检查）暗示 Moltis 正在加强多租户/细粒度权限治理，未来版本可能进一步扩展管理角色；PR #1232 中对 MCP 环境变量的固定键值对表示，则是为规范化生态接口所做的铺垫。两者均可视为**后续长期演进方向**（安全管控 + 工具生态标准化），但暂无明确新功能提案。

## 7. 用户反馈摘要

无新 Issue/评论产出。结合 PR 上下文可间接推断用户痛点：
- 部分部署者使用非管理员身份执行镜像构建时遇到阻碍（促成 #1222 中"限制为操作员管理员"的权限收缩）。
- 使用 Codex/OpenAI 工具链的开发者反馈工具调用数据异常（空值提交），根因追溯至 Schema 定义过宽（#1232）。

总体而言，当前反馈以工程侧修正为主，尚未出现大规模用户体验或功能缺失抱怨。

## 8. 待处理积压

- **PR 队列**：当前为 0 项待合并，无积压。
- **Issue 队列**：无未关闭遗留项。
- 整体队列健康，无长期未响应的任务。但需注意连续两日无新 Issue 进入，建议对外释放信号（如推进路线图讨论或发布贡献指南），维持社区输入活跃度。

---

**项目健康度评估**：⭐️⭐️⭐️⭐️☆（4/5）
安全修复与生态兼容性双线并进，队列干净整洁，版本持续滚动向前。唯社区讨论度与新 Issue 输入偏低，活跃度有回落迹象，建议关注下一周输入趋势。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-08-28

## 1. 今日速览

CoPaw 项目今日活跃度处于**高位**：过去24小时共有 31 条 Issue 更新（新开/活跃 15 条，关闭 16 条）和 50 条 PR 更新（待合并 25 条，已合并/关闭 25 条），合并/关闭率 50%，项目维护节奏紧凑。多租户版 QwenPaw Hub（2.2.0）的路线图讨论（#7318）以 10 条评论成为社区焦点，移动端原生体验的预研 PR（#7378）也已开出。与此同时，**桌面端启动耗时过长**和**渠道模块导入开销过大**成为今日最集中的 Bug 反馈主题，多个 Issue（#7360、#7363、#7367、#7023）均指向启动路径上的性能瓶颈，项目组已有多项优化 PR（#7372、#7361）在推进中。值得注意的是，文件保护未生效（#7362）的修复 PR 已在今日合并，安全类问题的响应速度值得肯定。

## 2. 版本发布

过去 24 小时无新版本发布。

## 3. 项目进展

今日合并/关闭了 25 条 PR，其中以下合并值得重点关注：

- **#7375 [`fix(governance): enforce File Guard paths in active policy evaluation`](https://github.com/agentscope-ai/QwenPaw/pull/7375)（已合并）** — 修复 File Guard 仅被旧版 `ToolGuardEngine` 消费、而正常 Agent 工具调用走 `GovernancePolicy` 新路径导致保护失效的问题（修复 #7362）。
- **#7374 [`feat(console): auto-fold assistant process messages`](https://github.com/agentscope-ai/QwenPaw/pull/7374)（已合并）** — 控制台自动分组折叠推理与工具调用过程消息，改善流式输出时的可读性。
- **#7349 [`feat(tools): propagate console stop cancellation to agent tools`](https://github.com/agentscope-ai/QwenPaw/pull/7349)（已合并）** — 将控制台的停止操作正确传递到 Coordinator 管理的工具任务，修复取消后工具状态未正确记录的问题。
- **#7368 [`fix(security): keep file guard active in off mode`](https://github.com/agentscope-ai/QwenPaw/pull/7368)（已合并）** — 统一工具执行安全相关的 UI 文案并规范化各模式描述，同步中英日等多语言。
- **#7337 [`fix(providers): separate model output capabilities from request limits`](https://github.com/agentscope-ai/QwenPaw/pull/7337)（已合并）** — 修复自动发现的模型输出能力被误当作请求级 `max_tokens` 上限的问题。

此外，`agentscope` 依赖已通过 #7373 升级至 2.0.7.post1。整体来看，项目今日在**安全治理、工具取消语义、控制台可读性、Provider 配置**四个方面均有关键修复落地，2.2.0 的发布准备（#7348 release notes PR）也在同步进行中。

## 4. 社区热点

- **[#7318 [OPEN] QwenPaw Hub 多租户版 2.2.0 路线图讨论](https://github.com/agentscope-ai/QwenPaw/issues/7318)（10 条评论）** — 社区对多用户访问和管理员管理的诉求由来已久（可追溯到 #2324），此 Issue 是项目方主动发起的路线图征询，标志着 QwenPaw 从个人助手向团队协作工具演进的关键一步。
- **[#2814 [CLOSED] 多智能体聊天中 callee agent 运行中历史为空](https://github.com/agentscope-ai/QwenPaw/issues/2814)（7 条评论）** — 一个从 4 月持续到今日的 Bug 最终关闭，涉及多智能体流式对话期间聊天历史的可见性问题。
- **[#7298 [OPEN] 桌面端/Docker 携带 OpenSSL 3.0.x TLS 栈，被运营商 DPI 重置握手](https://github.com/agentscope-ai/QwenPaw/issues/7298)（7 条评论）** — 指出了打包产物中 Python 3.11/OpenSSL 3.0.x 的 TLS 兼容性问题，影响部分运营商网络环境下的连接稳定性。
- **[#4770 [CLOSED] 左侧会话界面列顺序调整](https://github.com/agentscope-ai/QwenPaw/issues/4770)（6 条评论）** — 用户要求将"更新时间"列移到可见位置，将 ID/session ID 右移或隐藏，该 Issue 今日关闭，但需确认是否已在 UI 中落地。

社区核心诉求集中于 **UI/UX 细节打磨**（列顺序、文件分类展示、图标一致性）和**部署/多用户能力**（Hub、移动端）。

## 5. Bug 与稳定性

按严重程度排列：

### 高严重度

- **[#7362 [CLOSED] 文件保护未生效](https://github.com/agentscope-ai/QwenPaw/issues/7362)** — 用户开启文件保护后仍可读取 `/etc/passwd`。**已有修复 PR #7375 今日合并**，安全风险已解除。
- **[#7363 [OPEN] 同步调用阻塞事件循环且 timeout 失效（Desktop 2.1.1b1）](https://github.com/agentscope-ai/QwenPaw/issues/7363)** — Windows 桌面端启动期间 118–135 秒无响应、发送消息时约 126 秒阻塞。该 Issue 今日新开，暂无对应 PR。
- **[#5344 [CLOSED] `/api/console/chat` 返回 200 但静默丢弃消息（agent 忙时）](https://github.com/agentscope-ai/QwenPaw/issues/5344)** — 今日关闭，预计对应 PR #7299（拒绝冲突的聊天 payload）已合并或待合并。
- **[#7296 [CLOSED] OpenAI Responses 多轮对话 400 "Referenced reasoning item not found"](https://github.com/agentscope-ai/QwenPaw/issues/7296)** — 无状态上游（OpenCode Zen/Go Muse Spark）多轮失败，今日关闭，未核实修复方式。

### 中严重度

- **[#7367 [OPEN] 仅启用 console 渠道仍需 30–45 秒启动 —— 无条件导入全部 18 个渠道模块](https://github.com/agentscope-ai/QwenPaw/issues/7367)** — 根因是 `_load_builtin_channels()` 全量导入重型 SDK（lark_oapi 单个约 18.5 秒）。建议按需懒加载。
- **[#7360 [OPEN] QwenPaw Desktop 启动耗时约 4 分钟（V2.2.0b1）](https://github.com/agentscope-ai/QwenPaw/issues/7360)** — 用户附带了完整的 `qwenpaw-logs.zip`，需要核心团队分析定位。
- **[#7023 [OPEN] Desktop 启动在关键路径上阻塞约 60 秒安装 Playwright Chromium](https://github.com/agentscope-ai/QwenPaw/issues/7023)** — 无跳过/懒加载选项，影响每次启动体验。

### 低严重度 / 边界情况

- **[#7312 [OPEN] Windows 上 `execute_shell_command` 因继承 stdin 管道而挂起](https://github.com/agentscope-ai/QwenPaw/issues/7312)** — 子进程缺少 `stdin=DEVNULL`。
- **[#7370 [OPEN] 企业微信渠道发送 base64 data URI 图片报 OSError [Errno 36] File name too long](https://github.com/agentscope-ai/QwenPaw/issues/7370)** — 返回"Internal error"。
- **[#7364 [OPEN] Zero-downtime reload 复用已关闭的 memory_manager 并跳过 start()](https://github.com/agentscope-ai/QwenPaw/issues/7364)** — 导致 memory_search 永久不可用，影响 2.2.0b1。
- **[#7302 [OPEN] 关闭工具/思考过程显示后钉钉渠道仍发送空消息并触发未读提醒](https://github.com/agentscope-ai/QwenPaw/issues/7302)** — 影响消息渠道的用户体验。

## 6. 功能请求与路线图信号

- **QwenPaw 移动端原生体验（PR #7378，DO NOT MERGE）** — 以 Expo/React Native 实现 Android/iOS 客户端，复用现有后端服务。虽标记为不可合入，但表明项目方已开始移动端预研。
- **每次会话模型覆盖（PR #5992 进行中，首贡献者）** — 同一 Agent 可在不同会话中使用不同 LLM，`/model` 命令按会话生效，默认关闭以保持现有行为。
- **`React` 循环中工具返回内容裁剪（Issue #7316）** — 用户提议设计一个工具让 LLM 判断并删除/简化无效工具返回以优化上下文。与 PR #7331（bound oversized single-line tool results）方向一致，后者从硬性截断角度切入，可能在 2.2.0 中部分落地。
- **桌面端工作区产出物快捷访问按钮（Issue #6083，今日关闭）** — 一键直达工作区目录或最近产出物，改善非技术用户工作流。
- **Web 控制台文件上传按分类路由（Issue #7322）** — 当前在"知识库/日记/档案"分类下上传文件，实际落在工作区根目录。已有 PR #7351 修复该问题的上传路由与 Profile 文件隔离。
- **部署管理升级可视化（Issue #7366，今日关闭）** — 用户要求 platform.agentscope.io/deploy 增加可升级版本号，避免升级黑盒。

## 7. 用户反馈摘要

- **启动性能是最大痛点：** 多名用户在今日集中反馈桌面端启动耗时过长——从 30–45 秒（#7367）到 247 秒（#7360）、118–135 秒（#7363）不等。HDD/NAS 用户更新一次需约 1.5 小时（#6380），建议增量更新。核心团队需要在 2.2.0 发布前优先解决启动关键路径上的性能瓶颈，尤其是 Channel 模块的全量导入和 Playwright Chromium 的同步安装。
- **文件管理逻辑让用户困惑：** 在 Web 控制台选择不同分类上传文件，却全部落在工作区根目录（#7322），用户质疑这是 Bug 还是设计如此——这实际是上传路由未按当前选中分类正确分发的问题。
- **安全功能需要"真正生效"：** 开启文件保护后仍可读取系统敏感文件（#7362），以及关闭工具信息显示后钉钉仍收到空消息（#7302），均反映了用户对安全/隐私控制功能的信任度问题——设置项必须与实际行为一致。
- **移动端输入体验欠缺：** 安卓 Chrome 等浏览器下对话框无法换行，因为输入法回车被绑定为提交（#7355），建议在移动端将提交按钮独立出来。
- **多租户/团队功能持续被期待：** QwenPaw Hub 讨论（#7318）表明社区对团队使用场景有真实需求，建议在路线图中明确优先级。

## 8. 待处理积压

以下 Issue/PR 长期未获得维护者响应或修复进展，建议重点关注：

- **[#6380 [OPEN] 更新流程对机械硬盘用户不友好，耗时约1.5小时](https://github.com/agentscope-ai/QwenPaw/issues/6380)**（自 2026-07-23 至今，仅 2 条评论）— 用户建议增量更新、依赖缓存优化、编译步骤后置。
- **[#7023 [OPEN] Desktop 启动阻塞约 60s 安装 Playwright Chromium，无跳过/懒加载选项](https://github.com/agentscope-ai/QwenPaw/issues/7023)**（自 2026-08-14，2 条评论）— 与今日反馈的启动性能问题直接相关，建议纳入 2.2.0 修复范围。
- **[#7312 [OPEN] Windows 上 `execute_shell_command` 因继承 stdin 管道挂起](https://github.com/agentscope-ai/QwenPaw/issues/7312)**（自 2026-08-26，2 条评论）— Windows 环境下的稳定性问题，修复成本可能较低（补 `stdin=DEVNULL`），建议尽快安排。
- **[#6874 [OPEN] MCP 工具调用超时可配置化（PR）](https://github.com/agentscope-ai/QwenPaw/pull/6874)**（自 2026-08-10 至今仍在审核中）— 功能完整且对应关闭 #6724，已等待半月有余，建议维护者推进 review。
- **[#7057 [OPEN] 子进程 PATH 增加用户级 bin 目录（PR）](https://github.com/agentscope-ai/QwenPaw/pull/7057)**（自 2026-08-15，标记 ready-for-human-review）— 解决 systemd/Docker 环境下用户安装的 CLI 不可用的问题，属于部署场景的高频需求，建议尽快进入正式 review 流程。

---

**项目健康度评估：** 今日合并/关闭 PR 数量与新增 Issue 数量基本持平，安全类 Bug 响应迅速（当日开 Issue 当日合修复 PR），核心维护者参与度高。但桌面端启动性能的持续反馈与多日未动的积压 PR 仍需引起注意——建议在 2.2.0 发布前对启动关键路径进行一轮系统性优化（Channel 懒加载、Playwright 异步安装、同步调用事件循环解耦）。项目整体处在 2.1.x 向 2.2.0 过渡的活跃迭代期，社区参与度与版本演进节奏均处于健康水平。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-08-28


## 今日速览

ZeroClaw 在过去 24 小时保持高活跃度：**29 条 Issues 更新**（26 条活跃、3 条关闭）和 **50 条 PR 更新**（48 条待合并、2 条已合并/关闭）表明社区贡献强劲，但大量的 `needs-author-action`（需要作者行动）和 `stale-candidate`（过期候选）标签暗示了一批 PR 处于等待作者回应的停滞状态。值得注意的是，活跃的 Issue 几乎都集中在高层级架构 RFC 上——session 持久化、附件架构、WASM 插件运行时等——说明项目正经历深度架构演进期。此外，本周六 8 月 30 日将是 v0.8.5 稳定版发布线的截止日期（见 #9459），届时可能需要一次集中合并冲刺。整体项目健康度良好，但 PR 合并率（2/50）偏低，需要维护者加强跟进。

> **标记说明**：#开头为 Issue，PR #开头为 Pull Request。所有链接均为 `https://github.com/zeroclaw-labs/zeroclaw/issues/{编号}` 或 `/pull/{编号}`。


## 项目进展

今日有 **2 个 PR 被合并/关闭**，均为小型修复：

- **[PR #10413] test(channels): keep Telegram photo upload test offline** — 将 Telegram 照片上传测试从真实网络请求改为本地 Wiremock 端点，消除测试对网络的依赖，提升 CI 稳定性。
- **[PR #10416] fix(runtime): detect context overflow through error causes** — 修复 `is_context_window_exceeded` 仅检查外层错误字符串的问题，改为遍历完整 `anyhow::Error` 来源链。该修复解决了 #10329 号报告的核心问题（resilient wrapper 截断导致 loop-level 恢复永不触发）。

  → [#10329][i10329] 由 [@Project516][uProject516] 于 8 月 25 日报告的 Bug 在 **3 天** 内得到修复，响应速度优秀。

此外，大量 PR 正在排队等待合并（48 条），其中包括多项高价值功能（详见下文"社区热点"与"待处理积压"部分）。今日活跃 PR 中值得关注的新增内容包括：

- **[PR #10411] feat(channels): serialize same session messages** — 修复 [#10408][i10408] 报告的问题（同一会话中并行运行导致重复工作和回复），新消息将等待进行中的轮次完成而非启动并发运行。
- **[PR #10415] fix(providers): attribute reliable stream errors to served model** — 针对 [#10326][i10326]，流式错误现在报告实际发送到上游的模型，而非请求的模型。
- **[PR #10402] feat(tools): add Serply web search provider** — 新增 Serply 作为 `web_search_tool` 的 provider，扩展搜索后端选项。
- **[PR #10399] fix(ci): typecheck generated dashboard contract** — 在 CI 中自动生成 OpenAPI client 后再做 TypeScript 类型检查，响应 #10306 对 web/ 类型检查门禁的诉求。


## 社区热点

### 1. 核心架构讨论：RFC #9487 — 运行时所有权 session

> [Issue #9487][i9487] | 评论 27 条 | 由 [@NiuBlibing][uNiuBlibing] 创建 | 已更新 8 月 28 日

过去 24 小时最活跃的 Issue，讨论 Runtime-owned conversation sessions 和传输层适配器的 RFC。该 RFC 与 #9488（附件架构）、#9600（session 持久化合同所有权）和 #6850（内存生命周期与存储后端解耦）相互关联，构成了一个"会话架构深度重构"主题组。评论者正在讨论持久化合同的所有权边界和分层顺序。

**背景分析**：这一组 RFC（#9487/#9488/#9600）构成了 ZeroClaw v0.9 架构方向的核心。四个独立工作流同时触碰会话持久化合同（见 #9600 tracker），说明项目正在快速扩展 channel 和 ACP 支持，但需要明确的架构所有权来防止碎片化。24 小时内仍在持续评论，表明讨论尚在激烈进行中。

### 2. 架构决策追踪：#8692 — RFC 决策队列

> [Issue #8692][i8692] | 评论 14 条 | 由 [@Audacity88][uAudacity88] 创建 | 已更新 8 月 28 日

维护者决策队列 tracker，用于跟踪所有需要维护者批准的 RFC 和设计问题。今天仍有多条 RFC 在此队列中等待决策，包括 #9487、#9488、#8396 等。这是项目架构演进的"指挥中心"。

### 3. 多模型支持：#9809 — 每个 Provider Profile 支持多模型

> [PR #9809][p9809] | 由 [@NiuBlibing][uNiuBlibing] 创建 | 仅主贡献者

大型功能 PR（size:XL），为 provider 配置增加 `[providers.models.<family>.<alias>.models.<model_alias>]` 子表，使单一凭证 + 端点可承载多个模型。该 PR 已标记为 `stale-candidate`（过期候选），需要作者的关注和更新。用户对更灵活模型配置的诉求强烈，且当前活跃的 Telegram 安全模型选择器（#9997）也依赖类似能力。


## Bug 与稳定性

### 严重级别 S1 — 工作流受阻

- **[#10063][i10063] Anthropic-backed compatible gateways reject image_url blocks inside tool results**（已接受）
  - 自定义 OpenAI-compatible provider 在工具返回图片时会失败，而直接附加到用户消息则正常。
  - **状态**：已接受，但尚无对应 fix PR。

### 严重级别 S2 — 降级行为

- **[#10324][i10324] cron manual trigger 和 run-history 读取存在 check-then-act 竞态**（P1，已接受）
  - 操作者在 agent 重命名的窄窗口内可能绕过跨 agent 边界。虽然 filed at S2 而非 S0，但这是 #9947 的后续。
  - **状态**：已接受，尚无 fix PR。
- **[#10408][i10408] 同一 session 中第二条消息触发并行 agent 运行**（新报告）
  - 当前行为：用户发送新消息时，旧轮次仍在处理中，会导致重复工作和重复回复。
  - **状态**：已有对应 fix PR #10411（仍在讨论中）。
- **[#10186][i10186] Terminal fallback 文本绕过实时交付缝** — 两条终端回退路径绕过了部分实时交付合同。
- **[#10237][i10237] Telegram 回复线程将对话记忆碎片化为每个线程独立历史桶** — 多轮上下文丢失。
- **[#10286][i10286] 恢复的 ZeroCode 记录在历史裁剪后省略持久化轮次**。
- **[#10329][i10329] Resilient wrapper 截断遮蔽了上下文溢出恢复** — **今日已关闭**，由 PR #10416 修复。

### 严重级别 S3 — 轻微问题

- **[#10326][i10326] Reliable streaming 错误报告请求模型而非实际提供的固定模型** — 已有对应 fix PR #10415。
- **[#10076][i10076] WASM 插件运行时架构 RFC** — 新的 RFC 提出可组合的 WASM 插件运行时架构，标志着插件系统进入更深层次的设计阶段。

### 已关闭

- **[#8720][i8720] [Support]: Disable cachePoint for Bedrock Nova 2 Lite** — 已关闭，未提供解决方案。
- **[#10264][i10264] Quickstart CLI 验证测试的 locale 无关性** — 已关闭，任务完成。
- **[#10329][i10329] Resilient wrapper 上下文溢出恢复被遮蔽** — 已关闭，由 PR #10416 修复。


## 功能请求与路线图信号

### 今日新功能请求

- **[#10419][i10419] Stream agent-loop tokens from POST /webhook (SSE)** — 当 `stream: true` 且 `Accept: text/event-stream` 时，`POST /webhook` 应通过 SSE 流式传输 cumulative assistant tokens，而非返回单个 JSON。**这指向 Hosted Path A workers 的使用场景，对部署在受限环境中的用户很有价值。**
- **[#10421][i10421] Paginate persisted ACP transcript restoration in ZeroCode** — 在上周合并 PR #10380 之后，将持久化 Code/ACP 记录分页加载，保持 ZeroCode 渲染有界。
- **[#10405][i10405] [Tracker]: Implement session-scoped prompt attachments (#9998)** — 实现已接受的 #9998 功能，覆盖持久化聊天会话、ACP 会话、提示词修改工具、审批、编辑、生命周期清理和文档。

### 下一版本（v0.8.5，8 月 30 日截止）可能纳入的信号

- **多模型支持**（PR #9809）—— 高需求，但需作者更新
- **Telegram 安全模型选择器**（PR #9997）—— 当前标记为 `blocked`/`needs-author-action`
- **Web 搜索 Serply provider**（PR #10402）—— 新的功能，代码相对独立，合并风险低
- **TypeScript 类型检查门禁**（#10306）—— 已接受任务，且有对应 PR #10399
- **ZeroCode 输入保持响应**（PR #10374）—— 修复连接重连时 TUI 冻结问题
- **ZeroCode 配置元数据本地化**（PR #10378）—— 基于稳定的 group/section 标识符翻译

### 长期路线图信号

- **会话架构深度重构**（#9487/#9488/#9600）—— Runtime 所有权的会话、统一附件架构、持久化合同分层。是 v0.9 的核心方向，建议用户关注这些 RFC 的进展。
- **细粒度沙箱策略**（#6996）—— 文件系统和网络限制，影响部署在共享/多租户环境的用户。
- **桌面计算机使用支持**（#6909）—— 桌面屏幕交互与输入控制，值得关注的部署能力扩展。


## 用户反馈摘要

- **Sandbox 权限漂移**（#6996）：用户报告应用程序层路径准入与操作系统沙箱后端（Bubblewrap/Landlock/Seatbelt）之间在策略上漂移，导致权限配置混乱。维护者已接管并正在修订。
- **ZeroCode 记录恢复不一致**（#10286、#10380）：用户在 ZeroCode 中恢复历史记录时，发现持久化轮次在历史裁剪后缺失。该问题已通过 PR #10380 修复（恢复完整的持久化 ACP 记录），但仍有后续改进需求（分页加载）。
- **Telegram 线程记忆碎片化**（#10237）：用户报告 Telegram 回复线程将对话记忆拆分为每个线程独立的历史桶，导致多轮上下文丢失。目前尚无 fix。
- **CI 误导错误**（#10306）：用户反馈 `npm run build` / `tsc -b` 在 `web/` 目录下会打印 75 条令人困惑的错误。维护者已接受整改任务。
- **AI 辅助 PR 审查**（#9330）：关于 AI 辅助 PR 审查的 RFC 被多次修订，正在吸收生产环境中的 `pr-review-pilot` 经验。该项目正在慎重权衡 AI 审查与人工审批的边界。


## 待处理积压

### 需维护者关注的 RFC（在 #8692 决策队列中）

| Issue | 标题 | 等待时长 | 评论数 | 风险 |
|-------|------|----------|--------|------|
| [#9487][i9487] | Runtime-owned conversation sessions | 31 天 | 27 | 高 |
| [#9488][i9488] | Unified attachment architecture | 31 天 | 21 | 高 |
| [#6850][i6850] | Decouple memory lifecycle policy | 98 天 | 20 | 高 |
| [#8396][i8396] | Wire protocol first-class in provider | 62 天 | 15 | 高 |
| [#6996][i6996] | Granular sandbox policy | 92 天 | 13 | 高 |
| [#6909][i6909] | Computer-use desktop interaction | 95 天 | 11 | 高 |
| [#9975][i9975] | Web bundle/daemon compatibility | 15 天 | 7 | 高 |
| [#7822][i7822] | WASM plugin observer subscriptions | 73 天 | 7 | 高 |

### 长期未响应的关键 PR（stale-candidate / needs-author-action）

- **[PR #9809][p9809] 多模型支持**（8 月 7 日创建，21 天未更新）— 高需求功能，等待作者回应维护者反馈。
- **[PR #9724][p9724] always_ask 在 Full autonomy 下的修复**（8 月 4 日创建，24 天未更新）— 安全相关，风险：高。
- **[PR #9753][p9753] risk-profile allowed_tools 区分 absent vs empty**（8 月 4 日创建，24 天未更新）— 安全相关，风险：高。
- **[PR #9826][p9826] CLI 拒绝在 agent 的 shell 中运行**（8 月 7 日创建，21 天未更新）— 安全关键，风险：高。
- **[PR #9283][p9283] web_fetch 解压缩响应**（8 月 23 日创建，36 天未更新）— 功能修复，风险：高。

### 被阻塞的 PR

- **[PR #9997][p9997] Telegram 安全模型选择器** — 标记为 `blocked`/`needs-author-action`，该功能依赖 multi-model 支持（#9809）的落地，若 #9809 无法及时合并将阻塞此 PR。


## 项目健康度评估

| 指标 | 状态 |
|------|------|
| **Issues 响应速度** | ✅ 优秀 — #10329 在 3 天内被修复，多数新 Bug 在 24 小时内获得维护者回应 |
| **PR 合并率** | ⚠️ 偏低 — 过去 24 小时内 50 条 PR 仅 2 条被合并/关闭，需关注漏斗瓶颈 |
| **架构讨论活跃度** | ✅ 高 — 会话架构、WASM 插件、沙箱策略等核心主题持续吸引高参与度讨论 |
| **发布进度** | 🎯 v0.8.5 稳定版截止线为 8 月 30 日，当前为关键冲刺期 |
| **安全修复及时性** | ✅ 良好 — 安全相关 Bug（#10324、#10409）均已接受并被积极跟进 |
| **PR 积压风险** | ⚠️ 高 — 大量 `stale-candidate` PR（如 #9809、#9724、#9753）等待作者更新和维护者回复 |

**关注建议**：对于部署生产环境的用户，建议关注 #10324（cron 竞态）和 #10063（Anthropic 图片工具结果失败）的修复进展；对于参与社区开发的人员，建议关注 #9487/#9488/#9600 的会话架构讨论——这在未来将成为核心的架构决策方向，对上游和集成工作都会产生影响。目前主仓库的 `master` 分支已纳入 TypeScript 类型检查门禁（#10399），对 web/ 改动需要特别注意。

[i9487]: https://github.com/zeroclaw-labs/zeroclaw/issues/9487
[i9488]: https://github.com/zeroclaw-labs/zeroclaw/issues/9488
[i6850]: https://github.com/zeroclaw-labs/zeroclaw/issues/6850
[i8396]: https://github.com/zeroclaw-labs/zeroclaw/issues/8396
[i8692]: https://github.com/zeroclaw-labs/zeroclaw/issues/8692
[i9600]: https://github.com/zeroclaw-labs/zeroclaw/issues/9600
[i6996]: https://github.com/zeroclaw-labs/zeroclaw/issues/6996
[i6909]: https://github.com/zeroclaw-labs/zeroclaw/issues/6909
[i9975]: https://github.com/zeroclaw-labs/zeroclaw/issues/9975
[i7822]: https://github.com/zeroclaw-labs/zeroclaw/issues/7822
[i9330]: https://github.com/zeroclaw-labs/zeroclaw/issues/9330
[i8720]: https://github.com/zeroclaw-labs/zeroclaw/issues/8720
[i10076]: https://github.com/zeroclaw-labs/zeroclaw/issues/10076
[i10306]: https://github.com/zeroclaw-labs/zeroclaw/issues/10306
[i10329]: https://github.com/zeroclaw-labs/zeroclaw/issues/10329
[i10237]: https://github.com/zeroclaw-labs/zeroclaw/issues/10237
[i10186]: https://github.com/zeroclaw-labs/zeroclaw/issues/10186
[i10324]: https://github.com/zeroclaw-labs/zeroclaw/issues/10324
[i10286]: https://github.com/zeroclaw-labs/zeroclaw/issues/10286
[i10419]: https://github.com/zeroclaw-labs/zeroclaw/issues/10419
[i10326]: https://github.com/zeroclaw-labs/zeroclaw/issues/10326
[i10408]: https://github.com/zeroclaw-labs/zeroclaw/issues/10408
[i10244]: https://github.com/zeroclaw-labs/zeroclaw/issues/10244
[i10405]: https://github.com/zeroclaw-labs/zeroclaw/issues/10405
[i10063]: https://github.com/zeroclaw-labs/zeroclaw/issues/10063
[i9459]: https://github.com/zeroclaw-labs/zeroclaw/issues/9459
[i10421]: https://github.com/zeroclaw-labs/zeroclaw/issues/10421
[i10409]: https://github.com/zeroclaw-labs/zeroclaw/issues/10409
[i10264]: https://github.com/zeroclaw-labs/zeroclaw/issues/10264

[p9997]: https://github.com/zeroclaw-labs/zeroclaw/pull/9997
[p10350]: https://github.com/zeroclaw-labs/zeroclaw/pull/10350
[p10378]: https://github.com/zeroclaw-labs/zeroclaw/pull/10378
[p10064]: https://github.com/zeroclaw-labs/zeroclaw/pull/10064
[p9753]: https://github.com/zeroclaw-labs/zeroclaw/pull/9753
[p9724]: https://github.com/zeroclaw-labs/zeroclaw/pull/9724
[p10005]: https://github.com/zeroclaw-labs/zeroclaw/pull/10005
[p9809]: https://github.com/zeroclaw-labs/zeroclaw/pull/9809
[p9379]: https://github.com/zeroclaw-labs/zeroclaw/pull/9379
[p9283]: https://github.com/zeroclaw-labs/zeroclaw/pull/9283
[p9378]: https://github.com/zeroclaw-labs/zeroclaw/pull/9378
[p10402]: https://github.com/zeroclaw-labs/zeroclaw/pull/10402
[p10380]: https://github.com/zeroclaw-labs/zeroclaw/pull/10380
[p10413]: https://github.com/zeroclaw-labs/zeroclaw/pull/10413
[p10411]: https://github.com/zeroclaw-labs/zeroclaw/pull/10411
[p10374]: https://github.com/zeroclaw-labs/zeroclaw/pull/10374
[p10415]: https://github.com/zeroclaw-labs/zeroclaw/pull/10415
[p10416]: https://github.com/zeroclaw-labs/zeroclaw/pull/10416
[p9826]: https://github.com/zeroclaw-labs/zeroclaw/pull/9826
[p10399]: https://github.com/zeroclaw-labs/zeroclaw/pull/10399

[uNiuBlibing]: https://github.com/NiuBlibing
[uProject516]: https://github.com/Project516
[uAudacity88]: https://github.com/Audacity88

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*