# OpenClaw 生态日报 2026-08-21

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-21 00:32 UTC

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

# OpenClaw 项目动态日报 — 2026-08-21

> 数据周期：2026-08-20 至 2026-08-21（过去24小时）  
> 数据来源：github.com/openclaw/openclaw Issues & PRs


## 1. 今日速览

过去24小时内，OpenClaw 仓库保持了极高的社区活跃度：共产生 **500 条 Issue 更新**（其中 471 条处于活跃讨论状态）和 **500 条 PR 更新**（349 条待合并），讨论热度持续高位。**无新版本发布**，项目处于 v2026.8.1-beta 系列验证周期中，本周期的 release validation (Issue #125626) 仍在推进。值得关注的是，多个 **P0 级 Bug**（包括会话数据丢失隐患、文件工具路径篡改、Telegram 消息投递阻塞、回滚后网关静默丢消息）仍处于开放状态且未有对应修复 PR，稳定性风险仍需重视。与此同时，今日有一批高质量 PR 进入 "ready for maintainer look" 状态，涉及 incognito 会话可见性、安全审计写入序列化、安装策略警告确认等关键领域。

**活跃度评级**：🔥🔥🔥🔥🔥（极高 — 500/500 的 Issue/PR 更新配额均被拉满）


## 3. 项目进展

> 注：由于上游数据未提供 PR 的评论数与合并详情，以下分析基于 PR 标题、状态标签及描述信息。

### 今日核心合并/关闭 PR（状态为 CLOSED）

| PR | 标题 | 关键信息 |
|---|---|---|
| [#116489](https://github.com/openclaw/openclaw/pull/116489) | feat(security): require acknowledgement for install policy warnings | 合并 ✅ | 外部 `security.installPolicy` 命令现在可返回 `warn`，交互式 CLI 安装时需操作者确认插件/技能安装。安全边界向前迈出重要一步。 |
| [#120900](https://github.com/openclaw/openclaw/pull/120900) | feat(ui): review install policy warnings | 合并 ✅ | 与 #116489 配套：Control UI 中管理员可审查安装策略警告并决定是否继续安装。 |
| [#125471](https://github.com/openclaw/openclaw/pull/125471) | fix(models): keep Claude CLI OAuth available in Control UI | 合并 ✅ | 修复网关重启后 Claude CLI OAuth 刷新所有权丢失及 `anthropic: missing` 状态矛盾问题。 |
| [#126897](https://github.com/openclaw/openclaw/pull/126897) | fix(gateway): preserve incognito session visibility | 合并 ✅ | 修复非管理员用户通过别名/HTTP路由/任务ID等路径访问会话时，incognito 可见性不一致的问题。 |

**结论**：今日合并的 PR 集中在三个方向 — (1) 安全策略确认机制的端到端打通（CLI + UI + 网关）；(2) Claude CLI OAuth 的稳定性修复；(3) Incognito 会话的权限一致性。项目在安全与身份边界上持续加固。


## 4. 社区热点

> 按评论数排序的活跃讨论。

| 排名 | Issue/PR | 评论数 | 主题 | 核心诉求 |
|---|---|---|---|---|
| 1 | [#42475](https://github.com/openclaw/openclaw/issues/42475) | 23 | Per-agent 成本预算的网关级执行 | 运营者希望为每个 agent 设置日/月成本上限（代码中已有 `session-cost-usage.ts` 基础），防止失控花费。讨论中大概率涉及预算超限后的策略选择（阻断/降级/告警）的取舍。 |
| 2 | [#48788](https://github.com/openclaw/openclaw/issues/48788) | 20 | 统一的文件名编码处理工具 | PR #48578 只修了 UTF-8/Latin-1 的问题，社区希望从架构层面解决多编码（Shift-JIS、EUC-KR、GB18030）的文件名处理，避免各渠道适配器各修各的。 |
| 3 | [#125626](https://github.com/openclaw/openclaw/issues/125626) | 17 | v2026.8.1-beta.2 release validation | 正式发布前的验证活动，copy 真实网关升级到该 beta 并跑 worksheet。评论数高说明测试者积极参与，提供了不少反馈。 |
| 4 | [#108435](https://github.com/openclaw/openclaw/issues/108435) | 14 | 升级 2026.7.1 后网关无法启动（P0） | 用户通过 systemd、ollama、手动启动三种方式都失败，报 `gateway did not start on 127.0...`。**该 Issue 已持续月余，无修复 PR**，是目前最重的稳定性负债之一。 |
| 5 | [#38327](https://github.com/openclaw/openclaw/issues/38327) | 14 | google-vertex/gemini-3.1-pro 报 "Cannot convert undefined or null to object" | 2026.3.2 版本回归，讨论中可能涉及这是 provider API 变化还是 OpenClaw 侧解析问题。 |

**分析**：讨论热度最高的话题集中在**成本控制能力**（#42475）与**多编码文件名处理**（#48788）这两个功能性诉求上 —— 说明社区已开始从"跑起来"阶段过渡到"规模化运营"阶段，关注可观测性、成本配额、多区域/多语言适配等生产级能力。


## 5. Bug 与稳定性

### P0 级（Crash-loop / 数据丢失风险）

| Issue | 标题 | 状态 | Fix PR |
|---|---|---|---|
| [#108435](https://github.com/openclaw/openclaw/issues/108435) | 升级 2026.7.1 后网关无法启动（systemd/ollama/手动均失败） | OPEN，14 评论 | ❌ 无 |
| [#119270](https://github.com/openclaw/openclaw/issues/119270) | 文件工具剥离目标路径开头的 `@`，导致写入/删除错误文件 | OPEN | ❌ 无（有 linked PR 但未合入） |
| [#48920](https://github.com/openclaw/openclaw/issues/48920) | Live Docs 领先于当前 release（IsolatedSessions 在文档中但代码缺失） | OPEN | ❌ 无 |
| [#126246](https://github.com/openclaw/openclaw/issues/126246) | Telegram 外发消息卡在 `send_attempt_started`，重启后丢失 | OPEN，6 评论 | ❌ 无 |

### P1 级（功能受损 / 用户体验受阻）

| Issue | 标题 | 状态 | Fix PR |
|---|---|---|---|
| [#113306](https://github.com/openclaw/openclaw/issues/113306) | SQLite snapshot 恢复缺少端到端崩溃与身份保证 | OPEN（maintainer 关注） | ❌ 无 |
| [#125431](https://github.com/openclaw/openclaw/issues/125431) | Codex 受限工具策略静默禁用工作区 AGENTS.md | OPEN，8 评论 | ✅ **已修复** — [#126891](https://github.com/openclaw/openclaw/pull/126891)（preserve project instructions in restricted turns） |
| [#123073](https://github.com/openclaw/openclaw/issues/123073) | dev-channel 更新失败：`workspace:*` protocol（npm vs pnpm） | OPEN | ❌ 无 |
| [#124284](https://github.com/openclaw/openclaw/issues/124284) | v2026.8.1-beta.2 的 `wrapStreamFnWithProviderPromptState` 破坏 vLLM 子代理生成 | OPEN，6 评论 | ❌ 无（疑似 beta 引入的回归） |
| [#92241](https://github.com/openclaw/openclaw/issues/92241) | 回滚后网关持有旧模块路径，入站消息静默丢弃（ERR_MODULE_NOT_FOUND） | OPEN，6 评论 | ❌ 无 |

### 趋势判断

- **好消息**：今日无新增 P0 级 Issue（新开的最严重为 P1）；#125431（AGENTS.md 丢失）已有对应 PR #126891 并标记为 closes，修复效率较高。
- **坏消息**：**多个"钉子户"级 P0/P1 Bug 长期悬而未决** — #108435（月余）、#48920（5个月）、#119270（2周+）均无 fix PR。这些问题的共同特征是"环境相关性强"（容器 PID 复用、Windows 文件锁、特定 provider 组合），复现路径不稳定，可能是维护者迟迟未能修复的原因。
- **beta 回归风险**：两个 P1 Bug（#124284、#126458）都指向 v2026.8.1-beta.2 的新改动，说明当前 beta 周期引入了新的流处理/系统提示词逻辑，可能会影响 release 时间线。


## 6. 功能请求与路线图信号

| 功能请求 | 诉求 | 路线图信号 |
|---|---|---|
| [#42475](https://github.com/openclaw/openclaw/issues/42475) Per-agent 成本预算 | 网关级强制日/月花费上限 | ⭐ 高讨论热度（23 评论）+ 代码中已有 `session-cost-usage.ts` 基础。**很可能进入 v2026.9 规划。** |
| [#48788](https://github.com/openclaw/openclaw/issues/48788) 统一文件名编码工具 | 多编码（Shift-JIS/EUC-KR/GB18030）Content-Disposition 处理 | ⭐ 已有前置 PR #48578（修了 UTF-8/Latin-1），本次提的是架构级方案。已有 20 评论，**进入 backlog 概率高**。 |
| [#47910](https://github.com/openclaw/openclaw/issues/47910) 按失败类型隔离供应商 | Auth 失败的 provider 应进入 quarantine，而非与限流/超时同样重试 | 讨论适中（8 评论）。对成本与延迟优化有直接价值，但实现涉及 failover 链路的较大改动。 |
| [#68920](https://github.com/openclaw/openclaw/issues/68920) HTTP 端点 10-15s TTFB | `/v1/chat/completions` 需支持轻量上下文 / voice 模式 | 对 Realtime/Voice 场景是刚需。评论区有明确使用场景（LiveKit、Twilio）。相关 PR #126619（minimal tools.profile 时不再发送全量 system prompt）**已在今日提交，方向上高度对齐，建议跟踪。** |
| [#45501](https://github.com/openclaw/openclaw/issues/45501) 可配置 session 重置启动消息 | `/new` 或 `/reset` 后的注入提示语应可自定义 | 小需求，但社区共鸣度高（+1 较多）。实现成本低，可能作为 good-first-issue 被 pickup。 |

**值得关注的今日新 PR（方向性信号）**：
- [#126619](https://github.com/openclaw/openclaw/pull/126619)：HTTP chat 在 `tools.profile: "minimal"` 时不再发送全量 system prompt → **回应 #126459/#68920 的 TTFB 类问题**。
- [#126618](https://github.com/openclaw/openclaw/pull/126618)：修复 Tool Search `directory`/`tools` 模式导致 openai-completions 模型调用 meta `tool_call` 而非原生工具的循环/停滞问题。
- [#126860](https://github.com/openclaw/openclaw/pull/126860)：Cron 任务输出回写至来源聊天 → 即"**cron 结果返回发起会话**"。
- [#126895](https://github.com/openclaw/openclaw/pull/126895)：修复 `heartbeat.every: "0m"` 时 `tools.exec` 完成通知无法投递的问题（closes #62505）。


## 7. 用户反馈摘要

> 从 Issue 评论中提炼的高频关键词与核心痛点。

- **"静默失败"是最高频的负面关键词**。多个高热度 Issue（#112259 入站消息零负载静默丢弃、#92241 回滚后消息静默丢弃、#58957 模型切换静默失败、#119270 文件工具静默写错文件）都属于"系统没有报错，但结果错了/丢了"。这类问题会极大侵蚀用户信任，建议维护者优先投入可观测性改进（更清晰的错误传播、显式的失败回执）。

- **升级/回滚的信任成本在上升**。#108435（升级后启动失败）、#92241（回滚后丢消息）、#90378（5.28→6.1 cron 静默迁移导致投递方式改变）—— 三个高热度 Bug 都发生在版本切换路径上。社区对"升级安全"的敏感度已经很高，**建议在 release notes 中增加升级前检查清单与已知风险项**。

- **Windows/macOS 桌面端的体验问题持续出现**（#74378 CLI 进程残留、#86612 Docker 容器重启循环、#119796 Windows 测试 teardown 文件锁）。说明桌面端用户基数在增大，但跨平台文件句柄/进程生命周期管理仍是薄弱环节。

- **正面信号**：针对 #126246（Telegram 消息卡死）和 #108435（网关启动失败），用户都主动附上了详细日志与复现步骤，配合度高；#125431 从报告到修复 PR 仅用数天，且 PR #126891 明确标注 "AI-assisted"，说明 AI 辅助修复流程在实际运作。


## 8. 待处理积压

> 长期开放、无 fix PR、但影响面较大的问题。

| 类别 | Issue | 存活时长 | 最近动态 |
|---|---|---|---|
| **P0 网关启动失败** | [#108435](https://github.com/openclaw/openclaw/issues/108435) | >1 个月 | 最后维护者响应时间不明。用户已在多个环境复现，附带日志。**建议升为 maintainer 最高优先级。** |
| **P0 文件工具路径篡改** | [#119270](https://github.com/openclaw/openclaw/issues/119270) | ~2.5 周 | 有 linked PR（clawsweeper:linked-pr-open）但尚未合入。**数据损坏风险极高，建议在下一个 patch release 中强制合入。** |
| **P1 文档与 release 脱节** | [#48920](https://github.com/openclaw/openclaw/issues/48920) | ~5 个月 | 社区已多次提出，仍未解决。呼吁在 CI 中加入 **docs↔release 版本一致性检查**。 |
| **P1 回滚后静默丢消息** | [#92241](https://github.com/openclaw/openclaw/issues/92241) | ~2 个月 | 无 fix PR。与 #108435 同属**版本切换路径上的可靠性问题**，建议将系统提示词/模块加载逻辑的重构列入 v2026.9 计划。 |
| **P1 子代理完成通知重复/过早** | [#80498](https://github.com/openclaw/openclaw/issues/80498) | ~3 个月 | 涉及 tool-use turn 的语义边界，修起来可能牵涉面较大，但影响面也很广。 |
| **P1 容器环境下 usage-cost 锁永久死锁** | [#114234](https://github.com/openclaw/openclaw/issues/114234) | ~3.5 周 | PID 复用导致 cache 永久冻结。有 linked PR 但可能需要维护者进一步确认方案。 |

**给维护团队的建议**：优先从以下两个方向切入 — **(1) 数据安全类**（#119270、#124393 sync rewrite 丢行、#113306 SQLite snapshot 恢复）应在本周内给出明确修复计划；(**2) 版本切换可靠性**（#108435、#92241）需要系统性地排查网关启动 / 回滚 / 更新过程中的模块加载与状态恢复逻辑，而非 patch 式修复。

---

## 横向生态对比

# AI 智能体与个人 AI 助手开源生态——横向对比分析报告

**报告日期**:2026-08-21  
**数据窗口**:2026-08-20 ~ 2026-08-21(过去24小时)  
**覆盖项目**:OpenClaw、NanoBot、Hermes Agent、PicoClaw、NanoClaw、IronClaw、LobsterAI、Moltis、CoPaw、ZeroClaw(NullClaw、TinyClaw、ZeptoClaw 当日无活动)

---

## 1. 生态全景

个人 AI 助手/自主智能体开源生态正处于**从"可用"向"可靠"过渡的关键阶段**。头部项目(OpenClaw、NanoBot、Hermes Agent)日活跃度极高,社区最集中的诉求已从"能否跑起来"转向"能否规模化运营"——成本控制、多编码文件处理、网络自愈、数据持久化安全成为跨项目的高频议题。与此同时,多个项目在架构层面开始平台化演进:CoPaw 推进可插拔记忆后端与统一市场、IronClaw 深化 Hook 机制与持久化沙箱、ZeroClaw 强化 WASM 插件系统,行业正从单体 Agent 框架向模块化、多智能体协作平台过渡。然而,**"静默失败"类 Bug**(无报错但结果错误/丢失)在多个项目中反复出现,数据可靠性与可观测性仍是全行业最普遍的短板。

---

## 2. 各项目活跃度对比

| 项目 | Issues(新开/活跃) | PRs(待合并/合并) | Releases | 健康度评级 | 一句话评估 |
|------|-------------------|------------------|----------|------------|------------|
| **OpenClaw** | 500(配额拉满) | 500(349待合并) | 无 | 🔥🔥🔥🔥🔥 极高 | 生态绝对头部,但 P0 Bug 积压不容忽视 |
| **NanoBot** | 5(3新开) | 29(17待合并) | 无 | 🟢 高 | 响应速度快,合并效率中等,17条PR积压 |
| **Hermes Agent** | 50(42活跃) | 50(40待合并) | 无 | 🟡 高活跃/高压力 | Windows 更新链路与 SQLite 持久化是两大痛点 |
| **CoPaw** | 28(15活跃) | 50(22待合并) | ✅ v2.1.1-beta.1 | 🟢 健康 | 多线推进,任务中断与网络自愈是核心风险 |
| **ZeroClaw** | ~45 | ~50(48待合并) | 无 | 🟡 活跃但合并率低 | 架构重构期,大量安全 PR 卡在 author-action |
| **IronClaw** | ~10 | ~8 | 无 | 🟢 健康 | 围绕 v1.4.0 目标密集推进,修复效率高 |
| **NanoClaw** | 2新开 | 15合并 | 无 | 🟢 活跃 | 核心团队主导技能生态质量治理 |
| **PicoClaw** | 3 | 8(5待合并) | 无 | 🟡 中等 | 核心功能收尾,Web UI 性能问题未解 |
| **Moltis** | 1关闭 | 8(4待合并) | ✅ 20260820.01 | 🟢 良好 | 安全响应快,Windows 支持长期滞后 |
| **LobsterAI** | 2(stale) | 7(6合并) | 无 | 🟡 中等 | 合并率高但社区讨论冷清 |
| NullClaw/TinyClaw/ZeptoClaw | — | — | — | ⚪ 无活动 | 24h 内无动态 |

---

## 3. OpenClaw 在生态中的定位

**社区规模绝对领先**:OpenClaw 单日 500/500 的 Issue/PR 更新配额拉满,远超 Hermes Agent(50/50)和 NanoBot(29 PR)一个数量级,是当前生态中社区体量最大的项目。

**技术路线差异**:
- **全栈一体化**:OpenClaw 提供从 CLI、Control UI、网关到多通道适配的完整闭环,且今日合并的 PR 覆盖安全策略确认(CLI+UI+网关端到端)、incognito 权限一致性、Claude CLI OAuth 稳定性,体现其作为"生态基础设施"的定位。
- **P0 积压是最大风险**:网关启动失败(#108435,月余未修复)、文件工具路径篡改(#119270,数据损坏风险)、Telegram 消息投递阻塞(#126246)——核心链路的稳定性负债可能成为用户迁移到竞品的理由。

**对比竞品**:相比 Hermes Agent(桌面端体验优先)和 NanoBot(轻量、provider 生态扩展),OpenClaw 的差异化在于**企业级身份与安全边界**的持续加固,以及**网关级成本控制**等规模化运营能力(尽管尚未实现)。它更像生态中的"标准参照系"。

---

## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|----------|----------|----------|
| **数据持久化与可靠性** | OpenClaw、Hermes Agent、CoPaw、NanoClaw | SQLite 写入竞争(Hermes #85079/#89293)、history.db 膨胀至 7.6GB(CoPaw #7168)、envs.json 静默丢失(CoPaw #7118)、会话数据丢失隐患(OpenClaw) |
| **"静默失败"问题** | OpenClaw、CoPaw、Hermes Agent | 入站消息零负载丢弃(OpenClaw #112259)、回滚后静默丢消息(OpenClaw #92241)、网络恢复后不自动重连(CoPaw #6932)、模型切换静默失败(OpenClaw #58957) |
| **成本控制与配额** | OpenClaw(#42475)、NanoBot、NanoClaw(#3270) | per-agent 成本预算、token 用量统计、预算超限策略 |
| **多渠道/多编码适配** | OpenClaw(#48788)、PicoClaw(#3331)、Moltis(#1218)、CoPaw(#7169/#7158) | 统一文件名编码处理、任意 ASR 模型、WhatsApp 推名自定义、QQ 会话隔离 |
| **升级/回滚安全** | OpenClaw(#108435/#92241)、Hermes Agent(#86443) | 升级后启动失败、回滚后丢消息、Hermes update 静默删除 exe |
| **版本切换回归风险** | OpenClaw(#124284)、CoPaw(#7110) | Beta 引入流处理回归、单坏链接杀死会话 |
| **安全加固** | Moltis(#1216)、ZeroClaw(#9678/#9635)、NanoClaw(#3196)、CoPaw(#7119) | 未认证接口(CWE-306)、Git 安全策略、只读挂载、密钥文件权限 |

---

## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 |
|------|----------|----------|------------------|
| **OpenClaw** | 全栈一体化,企业级安全/身份/网关 | 开发者 → 中小企业运营者 | Go 网关 + React UI,自研网关路由与安全策略层 |
| **Hermes Agent** | 桌面端体验优先,Windows 深度支持 | 桌面重度用户、kanban 工作流用户 | Electron + WSL 后端,强调桌面端生命周期管理 |
| **NanoBot** | 轻量、多 provider 生态扩展 | 追求快速接入多种 LLM 的开发者 | 模块化 ChannelManager + AgentLoop,provider 适配层丰富 |
| **CoPaw** | 多渠道(QQ/DingTalk/WhatsApp)+ 记忆后端可插拔 | 中文社区、IM 深度集成用户 | Python + WebUI,强调"助手"而非"开发者工具" |
| **ZeroClaw** | 架构前卫,WASM 插件系统 + 默认安全 | 技术前瞻型开发者、自托管用户 | Rust 核心 + WASM 运行时插件,强调可组合性 |
| **IronClaw** | Agent 生命周期 Hook + 持久化沙箱 | 平台型开发者、需要深度定制的团队 | Rust + iron-proxy 代理,强调可扩展性与运维友好 |
| **NanoClaw** | 社区技能(skills)生态治理 | 技能开发者、多渠道运营者 | Node.js + MCP seam,技能配置标准化 |
| **PicoClaw** | 协议兼容性(Anthropic 原生 API) | 使用小众 LLM 服务的开发者 | Go 单体,强调协议层灵活性 |
| **Moltis** | 安全默认 + WhatsApp 优化 | 安全意识强的中小团队 | Rust,强调供应链安全与最小攻击面 |
| **LobsterAI** | 前端体验打磨(文件预览/搜索) | 国内开发者、桌面端用户 | Electron + Redux,侧重 UI 交互品质 |

---

## 6. 社区热度与成熟度

### 第一梯队:高活跃、生态驱动(快速迭代期)
- **OpenClaw**(500/500 配额拉满)——已进入"自增强"阶段,Issue/PR 数量级远超其他项目,但合并压力大、P0 积压,生态规模扩大伴随稳定性挑战。
- **Hermes Agent**(50/50)——Windows 桌面端用户基数大,社区反馈积极但"升级信任成本"在上升。
- **CoPaw**(28 Issues/50 PR)——发布节奏稳定(Beta 约两周周期),用户从 Issue 到 PR 的转化率较高,平台化演进方向清晰。

### 第二梯队:活跃、功能推进期(质量巩固阶段)
- **NanoBot**(29 PR)——响应速度快(当日提交修复 PR),但 17 条 PR 待合并,有长周期 PR(MCP v2 迁移超 3 周)悬而未决。
- **IronClaw**(~10 Issues/~8 PR)——高质量社区贡献(非核心成员提交 PR 占比高),合并效率高,处于 v1.4.0 功能集冲刺阶段。
- **ZeroClaw**(~50 PR)——活跃但合并率低(2/50),大量安全 PR 卡在 author-action,架构重构期必然伴随交付节奏放缓。

### 第三梯队:中等活跃、维护期(等待突破)
- **NanoClaw**(15 PR 合并)——核心团队主导,社区外部贡献有限。
- **PicoClaw**(3/8)——核心功能收尾,依赖升级占主导,Web UI 性能问题缺乏响应。
- **Moltis**(4 合并)——安全响应出色,但社区讨论量低,Windows 支持长期滞后。
- **LobsterAI**(6 合并)——合并率高但社区活跃度低,2 条 Issues 均 stale。
- **NullClaw/TinyClaw/ZeptoClaw**——无活动,存在感薄弱。

---

## 7. 值得关注的趋势信号

1. **从"跑起来"到"规模化运营"**:成本控制(OpenClaw #42475)、token 用量统计(NanoClaw #3270)、per-agent 预算配额——社区已开始关注生产级运维指标,这是生态成熟度的标志。

2. **"静默失败"是全行业公敌**:OpenClaw、CoPaw、Hermes 均出现"无报错但结果错误/丢失"类 Bug,用户对系统的信任侵蚀最为严重。**可观测性(错误传播、显式失败回执、proof-carrying 状态)正成为下一代 Agent 框架的核心竞争力**(IronClaw #7770 Hook 系统、Hermes #90866 proof-carrying 架构提案)。

3. **网络自愈能力成为基本预期**:CoPaw #6932(短暂断网后必须重启进程)、OpenClaw #92241(回滚后丢消息)——用户期望 Agent 能应对瞬态故障,而非依赖人工介入。这是从"demo"到"production"的关键门槛。

4. **多智能体/可插拔架构成为主流方向**:CoPaw 引入 PowerContext 可插拔记忆后端、IronClaw 推进 Agent 生命周期 Hook 化、ZeroClaw 深化 WASM 插件系统、PicoClaw 关闭了多智能体协作框架 PR(#423)——行业共识正在形成:**未来的 Agent 不是单体应用,而是可组合的模块化平台**。

5. **升级/回滚信任成本上升**:OpenClaw(#108435)、Hermes(#86443)、CoPaw(#7110)在版本切换路径上暴露了多处可靠性缺陷。**建议所有项目在 release notes 中增加升级前检查清单与已知风险项**,并建立 docs↔release 版本一致性 CI 检查。

6. **安全默认成为差异化标签**:Moltis(3 周闭环 CWE-306)、ZeroClaw(Git 安全策略)、NanoClaw(只读挂载)——安全不再是可选项,而是影响用户选型的关键因子。

7. **对 AI 智能体开发者的参考价值**:
   - 优先投入**可观测性**(错误传播、显式回执、状态可证明),而非只关注功能丰富度;
   - 重视**版本切换路径的可靠性**(升级/回滚/重启时的状态一致性);
   - 将**网络自愈**和**瞬态故障恢复**作为基本设计原则;
   - 关注**模块化/可插拔架构**,避免将 Agent 构建为不可拆分的单体;
   - **数据安全**是用户信任的底线,envs.json/state.db/会话文件的写入必须原子化且有备份。

---

*报告由 AI 分析师生成,数据截止 2026-08-21。个别项目数据缺失或评论数为 0 系上游数据抓取限制所致。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-21

> 数据窗口：过去 24 小时 | 数据来源：HKUDS/nanobot GitHub 仓库


## 1. 今日速览

NanoBot 项目今日保持**高活跃度**，核心聚焦于**稳定性修复**和**provider 生态扩展**。过去 24 小时内共有 5 条 Issue 更新（3 新开 / 2 关闭）和 29 条 PR 活动（17 条待合并 / 12 条已合并或关闭）。无新版本发布。值得关注的信号：社区对 **Claude 模型的原生 Vertex AI provider** 需求明确，同时暴露了两个关键 bug——**Docker 环境下 OpenAI OAuth 登录失败**和**流式响应中途 `server_error` 不重试**，两者均已有人提交修复 PR。总体来看，项目维护节奏紧凑，开发者响应速度较高，但 17 条 PR 仍处于待合并状态，合并压力需要维护者关注。


## 2. 版本发布

**无新版本发布。**


## 3. 项目进展

今日合并/关闭的 PR 中，以下内容值得关注：

- **事件循环关闭 crash 修复（#1203）**：这个从 2 月就存在的 Linux 下 `RuntimeError: Event loop is closed` 问题，经过漫长的讨论和等待后终于在今日合并。这是一个积压已久的稳定性问题修复，对 CLI 退出流程有直接影响，对 Linux 用户是实质性的体验提升。:arrow-right: [PR #1203](https://github.com/HKUDS/nanobot/pull/1203)

- **WebUI 浮动控件统一重构（#5240）**：将下拉菜单、面板、弹出层等控件进行了语义和样式上的统一收敛。属于前端技术债清理，后续新增 UI 组件的维护成本会有所降低，用户侧交互一致性也会提升。:arrow-right: [PR #5240](https://github.com/HKUDS/nanobot/pull/5240)

- **TUI 退出时打印 resume 命令（#5452）**：TUI 会话结束后会输出一键恢复的命令（`nanobot agent --session websocket:<id>`），解决了用户切换终端后难以回到原会话的问题。面向 TUI 重度用户，是一个很实用的小改进。:arrow-right: [PR #5452](https://github.com/HKUDS/nanobot/pull/5452)

- **Issue #5425（socks:// 代理支持）关闭**：解决了自定义 OpenAI-compatible provider 因 `socks://` 前缀代理 URL 导致的请求失败问题，对使用代理访问 LLM 服务的用户是个重要的环境修复。:arrow-right: [Issue #5425](https://github.com/HKUDS/nanobot/issues/5425)

> 总体而言，今日合并的 PR 多为**迟到的稳定性修复**和 **UI 层重构**，非功能性新特性。真正影响用户体验的 2 个新增 bug 的修复 PR 仍在待合并队列中（见下节），需关注后续合并节奏。


## 4. 社区热点

今日讨论热度最高的条目集中在两个方向：**新 provider 需求**和**关键的稳定性缺陷**。

- **Issue #5459：Claude 模型原生 Google Vertex AI provider 需求** — 用户 xuayan-nokia 提出了明确的功能扩展需求：NanoBot 已有 Anthropic 直连、OpenAI、Azure OpenAI、Bedrock 等 provider，但缺少对 Vertex AI 上 Claude 模型的原生支持。在 Anthropic API 稳定性争议不断的当下，这一诉求符合企业级用户的普遍期望。该 Issue 还没有评论或 PR 关联，属于 **NanoBot 生态覆盖扩张的信号**。:arrow-right: [Issue #5459](https://github.com/HKUDS/nanobot/issues/5459)

- **Issue #5444：Docker 环境下 OpenAI OAuth 登录失败** — 用户在容器运行 NanoBot，OAuth 授权码交换失败，是一个直接影响可用性的 bug。已有 1 条评论，尚无关联 PR。由于涉及 Docker + OAuth 这类常见运行场景，影响面不小，需要核心维护者定位，排查 OAuth 回调的 host 校验或端口映射问题。:arrow-right: [Issue #5444](https://github.com/HKUDS/nanobot/issues/5444)

- **Issue #5454：流式响应中途 server_error 不触发重试** — 暴露了重试逻辑的一个缺口：一旦 content 开始流式输出后遇到 `server_error`，agent 不会重试，只能中断。akinolur 跟进提交了 PR #5455。技术上要同时考虑客户端体验（已显示内容要不要回滚）和重试策略（如何避免重复计费），值得社区进一步讨论。:arrow-right: [Issue #5454](https://github.com/HKUDS/nanobot/issues/5454) | :arrow-right: [PR #5455](https://github.com/HKUDS/nanobot/pull/5455)


## 5. Bug 与稳定性

今日报告的 Bug **3 项**，按严重程度排列：

| 严重度 | Issue | 问题摘要 | 修复状态 |
|--------|-------|----------|----------|
| **高** | [#5444](https://github.com/HKUDS/nanobot/issues/5444) | Docker 环境下 OpenAI OAuth 登录失败，授权码交换失败 | :x: 无 PR 关联 |
| **中** | [#5454](https://github.com/HKUDS/nanobot/issues/5454) | 流式响应中途 `server_error` 不触发重试（已有内容后直接中断） | :white_check_mark: [PR #5455](https://github.com/HKUDS/nanobot/pull/5455) 已提交，待合并 |
| **低** | [#5425](https://github.com/HKUDS/nanobot/issues/5425) | `socks://` 代理 URL 不被识别（`socks5://` 等变体兼容性） | :white_check_mark: 已关闭（修复完成） |

**稳定性改进 PR（今日合并队列中的重点）**：

- :arrow_right: [PR #5412](https://github.com/HKUDS/nanobot/pull/5412) — 修复后台 gateway 子进程因 block-buffer 导致启动日志严重滞后的问题，显著降低排查问题的难度。
- :arrow_right: [PR #5413](https://github.com/HKUDS/nanobot/pull/5413) — 修复 provider 异常（exception）未被 fallback 策略捕获的问题，之前只有返回 `LLMResponse(finish_reason="error")` 才会触发 fallback。
- :arrow_right: [PR #5457](https://github.com/HKUDS/nanobot/pull/5457) — 修复单条出站消息的异常导致整个 ChannelManager 后台派发任务停摆的严重问题。
- :arrow_right: [PR #5458](https://github.com/HKUDS/nanobot/pull/5458) — 修正 Matrix 相关日志中 `%s` 占位符不兼容 Loguru 导致的诊断信息缺失。
- :arrow_right: [PR #5430](https://github.com/HKUDS/nanobot/pull/5430) / [PR #5431](https://github.com/HKUDS/nanobot/pull/5431) — 修复 AgentLoop 后台任务组的内存泄漏和异常静默丢失问题。


## 6. 功能请求与路线图信号

- **原生 Google Vertex AI provider for Claude（#5459）**：目前仅有 Issue 无 PR。结合 NanoBot 已支持 AWS Bedrock 的 Claude，补齐 Vertex AI 是**很自然的一步**，建议维护者优先评估。被纳入下一版本的潜力较大。:arrow-right: [Issue #5459](https://github.com/HKUDS/nanobot/issues/5459)

- **SenseNova（商汤日日新）provider（#5453）**：新增国产大模型 provider，支持 `sensenova-6.8-flash-lite`、`deepseek-v4-flash`、`glm-5.2` 三种模型，国内用户接入成本进一步降低。属于生态扩展型 PR，代码基本完备，被合并的可能性很大。:arrow-right: [PR #5453](https://github.com/HKUDS/nanobot/pull/5453)

- **Telegram 贴纸回复支持（#5387）**：允许 bot 以贴纸形式回复用户，并透出 `file_id`/emoji/set name。属于渠道体验增强。

**路线图信号汇总**：MCP SDK v2 迁移（#5179 / #5180）已在分歧中推进，虽然带有 `conflict` 标记但持续更新说明双方都在努力对齐。流式中途失败重试（#5455）若合并，则是对容错能力的一个重要补强。


## 7. 用户反馈摘要

- **Issue #5444（OAuth 登录失败）**：Docker 用户在本地端口映射后，浏览器回调 URL 指向 `localhost:1455` 但 token 交换失败，目前仅 1 条评论，尚未确认具体诱因。推测可能是容器内 `localhost` 语义不同或 host 校验问题，需要维护者用 Docker 环境复现。这是**运行环境适配类问题**，优先级建议调高。

- **Issue #5425（socks:// 代理）**：来自 pxy0592 的反馈——用户在配置自定义 OpenAI-compatible provider 时使用 `socks://` 前缀配置代理与 apiBase，但请求在到达 provider 前就失败，说明 **NanoBot 目前对代理协议的处理还比较“挑”**，该用户可能后续尝试所有 provider 时都会遇到相同问题。修复已合并，对代理用户是直接的体验改进。

- **Issue #5447（付费安全扫描 MCP 集成）**：Misterio070 提出将 NanoBot 与 Solana x402  micropayment 安全扫描服务集成。虽然有商业化探索的味道，但需求描述中 `ScanPay` 和 `AgentBridge` 都还在“我们构建了什么”的阶段。当前没有评论也没有维护者回应，说明**商业集成类需求目前还不是社区活跃方向**。但如果 x402 这类协议成为 agent 商业化标准，NanoBot 是否会跟进值得观察。


## 8. 待处理积压

- **PR #5179 / #5180（MCP SDK v2 迁移）**：两块 PR 都是从 7-30 至今超过 3 周仍未合并，都带有 `conflict` 标记，已有开发者提出评估与迁移方案。MCP 是 NanoBot 生态的核心集成层，v2 迁移能带来更简单的 API 和新传输方式，但这个决策持续拖延会增加后续维护成本。**建议核心维护者尽快裁决迁移方向与 baseline**。:arrow-right: [PR #5179](https://github.com/HKUDS/nanobot/pull/5179) | :arrow-right: [PR #5180](https://github.com/HKUDS/nanobot/pull/5180)

- **PR #5338（MCP OAuth 凭据保留）**：修复 OAuth store 读取失败时凭据被覆盖的问题，8-11 打开至今 10 天仍在待合并，属于数据安全类修复，建议提升处理优先级。:arrow-right: [PR #5338](https://github.com/HKUDS/nanobot/pull/5338)

- **PR #5339（WebUI 丢弃临时聊天消息）**：同样是 8-11 打开的修复，WebSocket 路径在用户丢弃临时聊天后可能错误恢复 scope，10 天仍未合并，且涉及用户数据隐私语义，风险中等。:arrow-right: [PR #5339](https://github.com/HKUDS/nanobot/pull/5339)

- **PR #1203（事件循环关闭 crash）**：虽已合并，但该 PR 从 2 月拖到 8 月才合入，暴露了长周期 PR 积压问题，建议维护者审视当前 PR 评审排队机制。


## 项目健康度总结

| 维度 | 评估 | 说明 |
|------|------|------|
| 活跃度 | :green_circle: 高 | 24h 内 29 条 PR 活动、5 条 Issue 更新，社区响应活跃 |
| 合并效率 | :yellow_circle: 中 | 12 条已合并/关闭，但 17 条仍待合并，且部分 PR 已拖延数周 |
| Bug 响应速度 | :green_circle: 中高 | #5454 当日即收到修复 PR（#5455），说明维护者和贡献者都在持续跟进 |
| 路线图清晰度 | :yellow_circle: 中 | MCP v2 迁移长期未决，新 provider（Vertex AI / SenseNova）方向有共识但缺少明确 roadmap |
| 值得警惕的信号 | — | 17 条待合并 PR 中有 8 条是 8 月 17 日之前提交的；#5447 这类**商业化集成需求**尚无维护者回应，社区治理和优先级澄清可能需要加强 |

---

*本日报由 AI 分析师生成，数据截止 2026-08-21*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-21

## 1. 今日速览

过去24小时，Hermes Agent 项目保持高强度迭代节奏：共产生 50 条 Issue 更新（42 条活跃/新开，8 条关闭）和 50 条 PR 更新（40 条待合并，10 条已合并/关闭），无新版本发布。**Windows 桌面端更新/构建可靠性**仍是社区反馈最集中的领域（至少 6 条相关 Issue 和 4 条修复 PR 同时活跃），其次是 **SQLite 会话持久化**的稳定性问题。值得注意的是，今日新出现的 **P0 级缓存参数兼容性 Bug**（`prompt_cache_retention` 导致 400 错误）和 **OpenAI gpt-5.6 系列模型的流式拒绝响应丢失**问题，涉及核心对话链路，需要重点关注。项目整体处于快速修复与功能并进的状态，维护者响应积极。

## 2. 版本发布

**无新版本发布。**

## 3. 项目进展

今日无 PR 被正式合并（合并/关闭的 10 条中均为关闭状态，含重复提交或作者自撤）。但以下**重要的待合并 PR** 正在推进关键修复，值得关注：

| PR | 关联 Issue | 解决的问题 | 状态 |
|---|---|---|---|
| [#91079](https://github.com/NousResearch/hermes-agent/pull/91079) fix(desktop): make Windows package rebuild transactional and self-healing | #44225, #90829, #86443, #90134 | **一站式修复 Windows 桌面端重建的四大顽疾**：构建失败导致 exe 被删、每日更新失效、资源丢失、ERR_REQUIRE_ESM 路径错误。核心思路是引入事务性候选构建 + 自愈机制 | 开放中，评论数较多 |
| [#90734](https://github.com/NousResearch/hermes-agent/pull/90734) fix(state): unlocked reads on the shared SessionDB writer connection | #85079 | 修复共享写连接上未锁定读取导致回合在持久化时失败的问题（涉及 17 次 API 调用的真实工作丢失） | 开放中 |
| [#85065](https://github.com/NousResearch/hermes-agent/pull/85065) fix(state): retry 'returned NULL without setting an exception' on WAL append | #85079 | 扩展 `SessionDB._execute_write` 的重试谓词，覆盖 SQLite 3.5x 的新错误拼写 | 开放中 |
| [#91180](https://github.com/NousResearch/hermes-agent/pull/91180) fix(kanban): make --initial-status blocked sticky from birth | #91178 | 修复 `kanban create --initial-status blocked` 不生效的问题（缺少事件行导致粘性阻塞门失效） | 开放中 |
| [#91181](https://github.com/NousResearch/hermes-agent/pull/91181) fix(agent): streamed refusals no longer vanish into empty-response retries | — | 移植自 opencode #43343，流式拒绝响应不再被当作空消息燃烧 3 次付费重试 | 开放中 |

若以上 PR 顺利合入，将有效缓解 Windows 桌面端体验、会话持久化可靠性两大痛点。

## 4. 社区热点

**🔥 最热 Issue（66 条评论）**
- [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) — `[skills-index-watchdog] Skills index is stale or degraded (degraded)` — 自动探针发现 Skills Hub 索引已过期 29.8 小时（限制 26h）。持续一个多月未解决，反映了自动化运维管道的脆弱性。

**💬 高讨论度 Issue（14 条评论）**
- [#87093](https://github.com/NousResearch/hermes-agent/issues/87093) — Debian 13.6 安装失败，`uv.lock` 和 npm install 双双报错。用户使用官方 `curl | bash` 一键脚本安装遇到问题，P1 优先级，已活跃 6 天。

**🔧 PR 侧**
- Windows 桌面端重建修复 PR [#91079](https://github.com/NousResearch/hermes-agent/pull/91079) 涵盖了 4 个关联 Issue，社区关注度最高，被多个用户标记为"终于有人系统性修复了"。

**📊 信号解读：**
1. **Windows 桌面端是用户基数最大的平台**，但更新/构建流程的可靠性短板显著影响了用户体验，是当前最集中的痛点。
2. **P0/P1 级别的核心链路 Bug**（缓存兼容性、流式拒绝）今日集中出现，可能与上游 OpenAI/Anthropic API 变更有关，需要快速响应。

## 5. Bug 与稳定性

按严重程度排列：

### 🔴 P0 — 核心链路失效

| Issue | 描述 | Fix PR |
|---|---|---|
| [#91164](https://github.com/NousResearch/hermes-agent/issues/91164) | **gpt-5.6 系列：`prompt_cache_retention` 导致 400 invalid_parameter**，对话回合被误判为不可重试客户端错误而直接死亡。OpenAI 已弃用该参数，需迁移至 `prompt_cache_options.ttl` | 无 |
| [#90971](https://github.com/NousResearch/hermes-agent/issues/90971) | **`apply_anthropic_cache_control` 非幂等**：对已装饰的输入重复应用会出问题。虽经核查原报告的越界场景不可达，但幂等性缺口仍存在 | 无 |

### 🟠 P1 — 功能受损

| Issue | 描述 | Fix PR |
|---|---|---|
| [#87093](https://github.com/NousResearch/hermes-agent/issues/87093) | Debian 13.6 安装失败（uv.lock 与 npm install 报错），阻塞新用户接入 | 无 |
| [#86443](https://github.com/NousResearch/hermes-agent/issues/86443) | **`hermes update` 删除桌面应用且退出码为 0**（即使重建失败也报告成功），用户可能无感知丢失 exe | [#91079](https://github.com/NousResearch/hermes-agent/pull/91079) |
| [#89293](https://github.com/NousResearch/hermes-agent/issues/89293) | **8 天内 state.db 损坏 3 次**（繁忙单主机部署）：锁风暴 + 窗口内重启 + journal_mode 在升级后静默回退 WAL，每次恢复需离线重建并丢失数据 | 无 |
| [#85079](https://github.com/NousResearch/hermes-agent/issues/85079) | 并发子代理写入时 WAL 追加报 `returned NULL without setting an exception`，回合硬失败 | [#85065](https://github.com/NousResearch/hermes-agent/pull/85065), [#90734](https://github.com/NousResearch/hermes-agent/pull/90734) |

### 🟡 P2 — 体验/兼容性

| Issue | 描述 | Fix PR |
|---|---|---|
| [#91153](https://github.com/NousResearch/hermes-agent/issues/91153) | 模型可能用旧列表项"叙述"新鲜且正确的工具结果，摘要准确性问题 | 无 |
| [#90237](https://github.com/NousResearch/hermes-agent/issues/90237) | v0.20.4 引入的 Windows 11 系统材质导致 **Snap 和 FancyZones 全部失效**（`transparent: true` 无条件应用） | 无 |
| [#90829](https://github.com/NousResearch/hermes-agent/issues/90829) | Windows 每日更新失败：fail-closed 原生依赖门 + 损坏的 node_modules 导致"未重建"提示 | [#91079](https://github.com/NousResearch/hermes-agent/pull/91079) |
| [#90134](https://github.com/NousResearch/hermes-agent/issues/90134) | Windows 上 `hermes desktop` 构建失败（blockmap.js 报错） | [#91079](https://github.com/NousResearch/hermes-agent/pull/91079) |
| [#90795](https://github.com/NousResearch/hermes-agent/issues/90795) | Web UI workspace 面板 `useSyncExternalStore` 重入导致 **Maximum update depth exceeded**，每次流式更新都崩溃 | [#91172](https://github.com/NousResearch/hermes-agent/pull/91172) |

### 🟢 P3 — 轻微/低影响

- [#91177](https://github.com/NousResearch/hermes-agent/issues/91177) — Kanban worker 在限流/超时退出 rc=0，被误判为协议违规并自动拉黑
- [#90906](https://github.com/NousResearch/hermes-agent/issues/90906) — Windows 上 `hermes update` 报"已最新"但 venv 仍停留 Python 3.11.15，需重启后才切换运行时
- [#81114](https://github.com/NousResearch/hermes-agent/issues/81114) — 桌面状态栈显示已完成的后台任务仍为"运行中"
- [#91021](https://github.com/NousResearch/hermes-agent/issues/91021) — 应用内更新后自动重启的桌面端无法重连 WSL 后端

## 6. 功能请求与路线图信号

| Issue/PR | 内容 | 分析 |
|---|---|---|
| [#90866](https://github.com/NousResearch/hermes-agent/issues/90866) | **架构提案：可观测状态从源头到副作用全程可证明（proof-carrying）** — 将多个已成型的修复（状态可观测、原子发布、真实验证）提升为架构原则 | 这是一个具有前瞻性的设计提案，若被采纳可能成为未来架构演进的指导方针。需要维护者决策 |
| [#91149](https://github.com/NousResearch/hermes-agent/issues/91149) | **预览面板通过远程/SSH 后端路由 localhost 开发服务器** — 桌面端连接远程 Agent 时，预览面板的 localhost 地址应在 Agent 后端解析 | 对使用远程后端的开发者是刚需，已标记为 duplicate，说明已有类似追踪 |
| [#91175](https://github.com/NousResearch/hermes-agent/pull/91175) | **浏览器工具 CLI 3 运行时指南加固** — 暴露 Browser Harness 0.1.10 的更多辅助函数，要求最终视觉验证，并限制遥测 | 提升浏览器自动化工具的可控性和可验证性 |
| [#90973](https://github.com/NousResearch/hermes-agent/pull/90973) | **网关身份插件可授权已解析用户** — 为 `pre_gateway_dispatch` 增加 `authorize` 结果，实现身份/访问控制插件按需授权 | 安全边界的灵活性增强 |
| [#91174](https://github.com/NousResearch/hermes-agent/pull/91174) | **Cron 执行与投递证明（attestation）** — 持久化调度器拥有的执行来源与呈现/投递证明 | 强化 cron 任务的可审计性 |
| [#91173](https://github.com/NousResearch/hermes-agent/pull/91173)(已关闭) | **桌面端西班牙语 (es) 本地化** | 虽被标记为 duplicate 关闭，但反映了社区对国际化的需求 |

## 7. 用户反馈摘要

**😠 最强烈的不满情绪**
- **安装体验**："Waste fucking ridiculous amounts of time"（[#90932](https://github.com/NousResearch/hermes-agent/issues/90932) 用户对 Chrome for Testing 下载卡死持续一小时的直接表达），以及 Debian 安装脚本失败（[#87093](https://github.com/NousResearch/hermes-agent/issues/87093)）。
- **数据安全焦虑**：`state.db` 8 天内损坏 3 次，用户描述"每次恢复需离线重建、部分数据丢失、数小时手工工作"（[#89293](https://github.com/NousResearch/hermes-agent/issues/89293)）。`hermes update` 静默删除 Hermes.exe 更让用户对更新机制失去信任（[#86443](https://github.com/NousResearch/hermes-agent/issues/86443)）。

**🤔 困惑与不理解**
- 用户对自己手动执行的 `/compress` 感到困惑，因为横幅没有显示触发原因（[#90785](https://github.com/NousResearch/hermes-agent/pull/90785) 的场景描述），说明 UI 状态反馈需要更透明。
- 模型"用旧列表叙述新结果"让用户难以判断输出可信度（[#91153](https://github.com/NousResearch/hermes-agent/issues/91153)）。

**😊 正面信号**
- 用户通过 `hermes kanban create --initial-status blocked` 的预期行为，体现了对文档化工作流的主动依赖（[#91178](https://github.com/NousResearch/hermes-agent/issues/91178)）。
- 有用户主动通过 agent 辅助调查并提交详细提案（[#91149](https://github.com/NousResearch/hermes-agent/issues/91149) 由用户 Vitor 撰写），表明深度用户愿意参与共建。

## 8. 待处理积压

| 类型 | 编号 | 描述 | 持续天数 | 优先级 |
|---|---|---|---|---|
| Issue | [#32678](https://github.com/NousResearch/hermes-agent/issues/32678) | **GCP Vertex AI 连接 404**（gcp/rest 驱动均失败，直接 curl 正常） | **约 3 个月**，最后更新 8/20 | P2 |
| Issue | [#65346](https://github.com/NousResearch/hermes-agent/issues/65346) | **OpenAI Codex OAuth 令牌每 2-3 天被提前失效**，与实际过期时间不符；已验证非单次事件 | 约 1 个月，最后更新 8/20 | P2 |
| Issue | [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) | **Skills index 自动探针持续降级**（索引过期），**66 条评论为全项目最高** | 约 1 个月 | P3 |
| Issue | [#44225](https://github.com/NousResearch/hermes-agent/issues/44225) | **Windows Electron 重建失败导致 Hermes.exe 被删**（与 #86443 重复，早一个多月提出） | 约 2 个月，已有 PR #91079 覆盖 | P2 |
| PR | [#68499](https://github.com/NousResearch/hermes-agent/pull/68499) | **分离委托子代理生命周期与任务结果**（避免假绿成功信号）| **约 1 个月**，仍在开放中 | P2 |
| PR | [#82033](https://github.com/NousResearch/hermes-agent/pull/82033) | **Windows 安装器拒绝不兼容的系统 npm** | 约 2 周 | P2 |
| PR | [#84297](https://github.com/NousResearch/hermes-agent/pull/84297) / [#84299](https://github.com/NousResearch/hermes-agent/pull/84299) | **桌面端 Kanban 附件预览**（两条 PR 并存，功能重复） | 约 1 周 | P3 |

**⚠️ 维护者注意：**
- [#32678](https://github.com/NousResearch/hermes-agent/issues/32678) 已积压近 3 个月未得到有效响应，用户可能流失。
- [#65346](https://github.com/NousResearch/hermes-agent/issues/65346) 涉及 OAuth 令牌生命周期管理，可能影响 Codex 付费用户留存。
- [#68499](https://github.com/NousResearch/hermes-agent/pull/68499) 是一个重要的可靠性修复，但已开放一个月，建议评估是否有合并障碍。

---

**总结：** 项目今日呈现"高活跃、高压力"状态。核心风险集中在 **Windows 桌面端更新链路的可靠性**和 **SQLite 会话持久化**，两者均有对应 PR 在推进中。新出现的 P0 级缓存兼容性问题需要尽快响应，避免影响 gpt-5.6 用户的核心体验。Skills index 自动探针长期降级暴露了运维自动化本身的脆弱性，建议优先修复。整体而言，项目健康度良好，社区反馈积极，维护者响应速度在可接受范围内，但长期积压的 #32678 和 #65346 需要给予关注。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期：** 2026-08-21  
**数据窗口：** 2026-08-20 ~ 2026-08-21（UTC）  


## 1. 今日速览

PicoClaw 过去24小时整体活跃度中等偏上：**3条Issue**（全部处于活跃状态）、**8条PR**（其中3条已合并/关闭、5条待合并）——PR 活动较为频繁，但合并率偏低，大部分待合并项为 Dependabot 自动依赖升级。**无新版本发布**，项目处于依赖维护期。值得关注的是，**2项重要功能PR（#1158、#423）在沉寂数月后于今日关闭**，标志着两项长期推进的功能（Anthropic原生API协议支持、多智能体协作框架）正式收尾或暂停。Issue方面，Web UI输入卡顿问题（#3281）仍是最受关注的技术痛点，另有2个新功能需求（ASR模型灵活性、子代理动态模型覆盖）在等待维护者响应。整体来看，项目核心功能趋于稳定，当前主要活跃点为依赖升级与收尾工作。


## 2. 版本发布

**无新版本发布。** 最新版本仍为 v0.3.1（2026年5月发布）。项目功能改动正在积累中，预计下次发布将包含 Anthropic 原生 API 支持与多智能体协作框架的阶段性成果，值得关注。


## 3. 项目进展

今日关闭/合并了 **3个PR**，其中2项为长期推进的核心功能收尾：

- **[PR #1158] feat: add anthropic-messages protocol for native Anthropic API format**（合并，关闭）  
  为 PicoClaw 新增 `anthropic-messages` 协议前缀，使其能够连接仅支持 Anthropic 原生 Messages API（`/v1/messages`）格式的 LLM 服务。该 PR 修复了 Issue #269，打破了此前仅支持 Anthropic 兼容 OpenAI 格式的限制。从 2026-03-06 创建到 8-20 关闭，历时逾5个月，是该项目迄今规模最大的协议扩展之一。
  🔗 https://github.com/sipeed/picoclaw/pull/1158

- **[PR #423] feat: base multi-agent collaboration framework & shared context**（关闭）  
  基于已合并的 PR #213（provider 协议重构）与 #131（模型回退链 + 多智能体路由）构建的**基础多智能体协作框架**，包含：
  - **Blackboard** — 线程安全共享上下文池
  - **Agent Handoff** — 智能体间工作交接
  - **Discovery Tools** — 智能体发现工具
  
  该 PR 标记为 WIP，自 2026-02-18 创建，经过6个月后于今日关闭（合并或搁置需进一步确认）。作为多智能体路线的核心基础设施，其结果将直接影响后续 subagent/delegate 功能的演进方向。
  🔗 https://github.com/sipeed/picoclaw/pull/423

- **[PR #3318] fix(web): repair unparseable pnpm-lock.yaml**（合并，关闭）  
  修复了 `web/frontend/pnpm-lock.yaml` 中 `semver@7.8.5` 被重复声明导致 `ERR_PNPM_BROKEN_LOCKFILE` 的问题（重复映射键冲突），使前端依赖安装恢复正常。
  🔗 https://github.com/sipeed/picoclaw/pull/3318

**整体评估：** 今日核心进展是两项功能PR的结果落地，其中 Anthropic 原生协议支持对兼容性有实质提升，多智能体框架的收尾则对项目技术路线有方向性影响。另有1个前端构建修复，提升了 Web UI 的可持续开发性。


## 4. 社区热点

今日最受关注的 Issue 集中在 **Web UI 性能** 与 **ASR 模型灵活性** 两个主题：

- **[Issue #3281] Web UI chat input is very laggy when history has a little bit long**  
  ⭐ 6条评论 | 👍 1 | **唯一获得 👍 的 Issue**  
  用户反馈当会话历史稍长时，Web UI 输入框出现明显卡顿。这并非崩溃级 Bug，但直接触达日常使用体验，是目前社区最共性的痛点。评论数表明该问题引发了多轮讨论，但截至今日 **尚未有修复 PR 关联**。
  🔗 https://github.com/sipeed/picoclaw/issues/3281

- **[Issue #3331] Feature: Use any models with /audio/transcriptions endpoint**  
  💬 1条评论  
  用户提出当前 ASR 仅支持 `*-whisper-*` 模型命名前缀，希望支持任意符合 `/audio/transcriptions` 端点的模型。该请求反映了用户对**模型选择自由度**的需求，指向 `asr.go` 中硬编码的模型匹配逻辑。
  🔗 https://github.com/sipeed/picoclaw/issues/3331

**社区情绪画像：** 用户对 Web UI 交互流畅度敏感度高，对模型兼容性（Anthropic 原生 API、任意 ASR 模型）有持续诉求，整体反馈集中在"开放更多接口"与"提升前端性能"两个维度。


## 5. Bug 与稳定性

今日活跃 Bug 共 **1项**，另有 1 个前端修复已合并：

| 严重程度 | Issue/PR | 描述 | 状态 |
|---------|----------|------|------|
| 🟡 中等 | [#3281] Web UI 输入卡顿（历史消息较长时） | 会话历史较长时输入框卡顿，影响日常交互 | **无对应修复 PR**，待排查 |
| 🟢 已修复 | [#3318] pnpm-lock.yaml 解析错误（重复 key） | 前端构建因 `semver@7.8.5` 重复声明而失败 | ✅ 已合并 |

**分析：** 前端构建阻断性问题已通过 #3318 解决，但 Web UI 输入框性能问题尚无明确修复方案，也未标记优先级。若影响面较大，建议维护者评估是否与前端渲染长列表的虚拟化策略有关。


## 6. 功能请求与路线图信号

今日新增功能请求 **2项**，另有 2 个长期 PR 的关闭为功能路线提供了信号：

| 功能请求 | 核心诉求 | 当前状态 | 纳入下一版本可能性 |
|---------|---------|---------|------------------|
| **任意 /audio/transcriptions 模型支持（#3331）** | 摆脱 `*-whisper-*` 命名限制，兼容更广泛的 ASR 服务 | 无官方回复 | ⭐⭐⭐ 实现成本低（逻辑简单，改匹配规则即可） |
| **delegate/spawn/subagent 动态模型覆盖（#3330）** | 调用时可按需指定模型，而非使用静态配置 | 无官方回复 | ⭐⭐⭐ 与多智能体框架（#423）方向高度契合，若 #423 合入则概率大增 |

**路线图信号：** 今日关闭的 PR #423（多智能体协作框架）是 subagent/delegate 能力扩展的底层基础设施，若其成果落地，#3330 将从"辅助增强"升级为"自然延伸"。此外 **PR #1158**（Anthropic 原生协议）拓展了模型接入面，为 #3331 中"任意 ASR 模型"提供了协议层面的铺垫——两者思路一致（开放更多模型接口），可能说明项目正朝着"模型无关"的方向演进。


## 7. 用户反馈摘要

- **Web UI 性能（#3281）：** 用户 `xpader` 报告了在历史消息较长时输入框卡顿的体验问题。在 PicoClaw v0.3.1 + Go 1.25.11 + Web UI 环境下复现，属于**真实使用痛点**，预计会随使用时长递增而恶化。建议开发者优先排查前端消息渲染或状态管理是否存在 O(n) 复杂度问题。
- **ASR 模型兼容性（#3331）：** 用户 `stanislavvv` 明确指出 `*-whisper-*` 前缀匹配模型"too old and slow"，说明**部分用户已尝试接入更新的 ASR/语音识别模型**，带有明显的功能升级期望，不是简单的便利性诉求。
- **多智能体动态模型（#3330）：** 用户 `v2up-32mb` 对 delegate/spawn/subagent 工具的模型指定方式提出了精确的技术改进建议（增加 `whisper-transcription` 标志），显示出**中高级用户对子代理灵活性的需求**，这类用户往往构建复杂的多代理工作流，对配置灵活性要求高。


## 8. 待处理积压

以下 Issue/PR 长期未获维护者响应或推进，建议关注：

- **[Issue #3281] Web UI 输入卡顿（自 2026-07-21 创建，已1个月）**  
  有6条评论、1个 👍，社区关注度较高，但**无任何 fix PR、无官方标签更新**，可能成为负面体验的持续来源。
  🔗 https://github.com/sipeed/picoclaw/issues/3281

- **[Issue #3331] 任意 /audio/transcriptions 模型支持（创建于 2026-08-13，已1周）**  
  虽有 1 条评论但暂无官方回复，若维护者认可此方向，建议尽快打上 `good first issue` 或 `feature request` 标签。
  🔗 https://github.com/sipeed/picoclaw/issues/3331

- **[Issue #3330] 子代理动态模型覆盖（创建于 2026-08-13，已1周）**  
  与多智能体路线（PR #423）直接相关，建议与已合并的 #423 成果对照评估。
  🔗 https://github.com/sipeed/picoclaw/issues/3330

- **5个 Dependabot 依赖升级 PR（#3332 ~ #3336，均已 stale）**  
  均为 AWS SDK、Anthropic SDK、mautrix 等依赖的版本升级，已连续8天无更新操作。长期搁置可能导致依赖安全漏洞累积，建议维护者批量处理或设置自动合入门槛。
  - 🔗 #3336: https://github.com/sipeed/picoclaw/pull/3336
  - 🔗 #3335: https://github.com/sipeed/picoclaw/pull/3335
  - 🔗 #3334: https://github.com/sipeed/picoclaw/pull/3334
  - 🔗 #3333: https://github.com/sipeed/picoclaw/pull/3333
  - 🔗 #3332: https://github.com/sipeed/picoclaw/pull/3332


**项目健康度总结：** 核心功能推进有序（协议扩展、多智能体框架均有关键收尾），前端构建与依赖管理有小幅改善，但 Web UI 性能问题和中长期依赖升级积压是当前主要隐患。功能请求（ASR 灵活性、动态模型覆盖）与既有路线方向一致，建议维护者在下个版本规划中优先评估。整体评级：**🟢 健康推进中，需关注性能类问题响应速度。**

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期：2026-08-21** | **数据窗口：2026-08-20 ~ 2026-08-21**


## 1. 今日速览

NanoClaw 项目今日活跃度显著攀升，核心团队密集推送了一批针对社区技能（skills）的修复 PR（#3414–#3423），覆盖 Ollama、Atomic Chat、CLIDash、Dashboard、Tavily、AnyDoc、macOS Statusbar 等多个工具的配置失效与安装隔离问题。新开 Issue 方面，WhatsApp 媒体文件不可达（#2715）和 mention-sticky 误触发（#3369）两个问题直接关联核心路由逻辑，值得重点关注。**整体评估：项目处于高活跃迭代期，核心通道稳定性补强与技能生态质量治理双线并进。**


## 2. 版本发布

**无新版本发布。** 当前所有变更均处于 PR 待合并或合并后待发版状态。


## 3. 项目进展

今日有 15 个 PR 被合并或关闭。核心进展集中在 **gavrielc** 主导的十二项技能审计修复系列——该系列 PR 均标注 `[core-team]` 并叠放在 #3408 之上，针对每个社区技能的配置失效、安装隔离、文档失实等系统性问题进行集中治理：

- **配置失效修复（关键）**：`add-atomic-chat-tool`（#3415）和 `add-ollama-tool`（#3416）被审计发现其环境变量助手仅读取 `process.env`——NanoClaw 从不从 `.env` 填充该值，导致文档中宣传的配置项实际完全无效。两个 PR 均将配置移至每分组（per-group）`container_configs` MCP seam。此外 `add-ollama-tool` 的 daemon URL 此前被硬编码为默认值，四个管理工具永远无法注册。
- **安装隔离修复**：`add-anydoc`（#3419）修复了循环中调用裸 `ncl` 导致在多实例主机上读 A 实例的数据库、重启 B 实例分组的严重错乱；`add-macos-statusbar`（#3420）修复了 Swift 代码中硬编码的 `com.nanoclaw` label 与新的 slug 命名（`com.nanoclaw-v2-<installSlug>`）不匹配，导致状态栏监控不存在的服务。
- **其余修复**：`add-dashboard`（#3417）补齐 REMOVE.md、修正 SQL 可移植性；`add-tavily-tool`（#3418）让 smoke test 在无运行容器时给出真实信号而非静默通过；`add-clidash`（#3414）修复了 **refresh 操作同时拉起约 29 个并发 `bin/ncl` 进程、在 2-vCPU 主机上 27 个超时、几乎每个标签页都报错**的自毁式设计，测试从 87 增至 102 个全绿。

此外，合入的 **#3402**（codex provider 文件投递）、**#3403**（Matrix ESM patch 修复，解决 Node 22 下的扩展名缺失问题）、**#3401**（whatsapp-cloud 技能与 main 的兼容性）共同完善了多通道的文件投递能力。


## 4. 社区热点

今日暂无高评论量 Issue 或 PR（各条评论数均≤1）。但值得关注的高关注度新增 PR 是 **#3421**：虽然已被合并关闭，但内容涉及**“一键 Slack Agent”全套流程**（README banner、app + avatar + workspace 一行安装），叠加 #3423 对 `add-slack` 中遗漏的 `app_mentions:read` bot scope 的修复，表明 Slack 集成是当前生态建设的重点方向之一。


## 5. Bug 与稳定性

按严重程度排列：

**🔴 高严重度——Agent 核心能力受损**

- **[OPEN] #2715 — WhatsApp 入站媒体文件 Agent 不可达**：附件被下载到宿主机的 `DATA_DIR/attachments`，该目录**未挂载进 Agent 容器**，而 Agent 拿到的 `/workspace/attachments/...` 路径在容器内不存在。Agent 无法打开用户发送的任何图片、文档或音频。已有修复方向：需要将附件目录挂载进容器或改用 session inbox 路径。（作者：jon-ruth | [链接](https://github.com/nanocoai/nanoclaw/issues/2715)）
- **[OPEN] #3369 — mention-sticky 在未被提及的线程中自动发言**：`engage_mode: 'mention-sticky'` 配合 `ignored_message_policy: 'accumulate'` 时，accumulate 创建 session 行即成为订阅源，导致 Agent 在从未被提及的 Slack 线程中开始回复。（作者：nilsborg | [链接](https://github.com/nanocoai/nanoclaw/issues/3369)）
- **[CLOSED] #2606 — engage_mode='always' 静默丢弃所有消息**：已关闭，说明已有 fix 合入（或已被标记为重复问题处理）。（作者：nikki-assistant | [链接](https://github.com/nanocoai/nanoclaw/issues/2606)）

- **修复侧对应进展**：**#3422** 提出修复 mention-sticky 应在被提及（mention）时才订阅、而非因 session 创建即订阅，与 #3369 直接对应，目前待合并。**#3247**（cron 格式错误导致每次 sweep tick 反复报错）仍在待合并队列中。


## 6. 功能请求与路线图信号

- **Cursor Agent SDK 支持**：`#3356`（feat(providers): add Cursor Agent SDK payload）与 `#3355`（feat(setup): add /add-cursor agent provider skill）两个 PR 均标注 `core-team`，说明 Cursor 作为 agent provider 正在被正式接入。若合并，用户可通过 NanoClaw 直接管理 Cursor Agent。
- **ncl 命令 token 用量统计**：`#3270`（Feat/ncl token usage）已存在 5 天，处于待合并状态，为开发者提供 Token 消耗追踪能力。
- **新增技能 `add-why`**：`#3189` 提交了一个 Utility skill，可向用户解释“某条消息发生了什么/为什么”，处于开放状态待合并。


## 7. 用户反馈摘要

- **WhatsApp 实际用户（#2715）**：真实业务场景中用户向 Agent 发送图片/文档是核心交互方式之一，当前不可用直接阻断使用。Issue 作者明确指出了根因（挂载路径），说明用户已做了一定程度的源码排查，反馈质量高。
- **Slack 线程稳定性（#3369）**：mention-sticky 的误触发会导致 Agent 在不相干的线程里“突然说话”，对使用体验和信任度伤害大。该 Issue 与修复 PR #3422 同日出现，说明用户对路由逻辑有较深理解。


## 8. 待处理积压

- **#3247 — 畸形 cron 字符串每次 sweep tick 反复报错**（8月14日创建，7天未合入）：虽为 Fix PR，但在 PR 描述中明确指出“每次重试都报同样错误”，属于持续日志污染的稳定性问题。建议维护者优先评审合并。[链接](https://github.com/nanocoai/nanoclaw/pull/3247)
- **#3196 — Fix/add mount readonly**（8月7日创建，14天未合入）：涉及只读挂载的安全加固，长期搁置可能使容器逃逸/写入面保持过大。[链接](https://github.com/nanocoai/nanoclaw/pull/3196)
- **#3270 — ncl token 用量统计**（8月16日创建）：开发者常用的成本观测功能，建议加速评审。[链接](https://github.com/nanocoai/nanoclaw/pull/3270)

---

*本报告由 AI 生成，数据来自 NanoClaw GitHub 仓库公开信息。个别 PR 评论数为 0 或因数据抓取限制未显示。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，我是您的 AI 智能体与个人 AI 助手领域开源项目分析师。以下是根据 IronClaw 项目 2026-08-21 的 GitHub 活动数据生成的日报。

---

# IronClaw 项目动态日报 — 2026-08-21

## 1. 今日速览

今日 IronClaw 项目活跃度极高，核心贡献者围绕 **v1.4.0** 版本目标密集推进。开发重点集中在：**WebUI 设计系统** 的阶段性重组（Epics #7038/#7781/#7782 重新划分）、**Agent 生命周期 Hook** 的引入（#7770）、以及 **持久化用户沙箱** 的第二步实施（#7732）。此外，CI 因 Rust 1.98 稳定版更新导致的 lint 瀑布效应（#7777/#7778）及设计系统文档整合（#7763）在今日被快速关闭，体现了良好的修复效率。值得注意的是，社区成员 `henrypark133` 和 `italic-jinxin` 贡献了多份高质量的清理与测试修复工作，项目整体健康度良好。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日合并/关闭的 PR 有效解决了运维痛点和架构债务，并为新功能铺平了道路。

-   **修复 CI 红屏 (紧急)**：
    -   [#7777 fix(ci): clear the clippy 1.98 lint cascade blocking the merge queue](https://github.com/nearai/ironclaw/pull/7777) 与 [#7778 fix(lints): Rust 1.98 clippy migration (unbreaks all-branch CI)](https://github.com/nearai/ironclaw/pull/7778) 处理了 Rust 1.98 稳定版带来的 lint 升级问题，解除了对合并队列的阻塞。
-   **核心功能落地**：
    -   [#7729 feat(automations): add run-now across trigger domain and WebUI](https://github.com/nearai/ironclaw/pull/7729) 已合并，为自动化系统引入了“立即运行”功能，闭环了 [#7193](https://github.com/nearai/ironclaw/issues/7193)。
    -   [#7786 fix(assistant): unbreak suggestion generation on OpenAI models...](https://github.com/nearai/ironclaw/pull/7786) 修复了 OpenAI 模型下建议生成的严重问题。
-   **架构与文档整理**：
    -   [#7763 docs(subagent): consolidate seven design docs into one canonical README](https://github.com/nearai/ironclaw/pull/7763) 完成了子代理设计文档的大规模整合，净减少 9713 行，消除了文档矛盾。
    -   [#7755](https://github.com/nearai/ironclaw/issues/7755) 关闭，完成了 turn/subagent 词汇表的重复类型清理。
-   **社区贡献**：`thisisjoshford` 贡献的 [#7738 feat(slack): per-field help text...](https://github.com/nearai/ironclaw/pull/7738) 已合并，提升了 Slack 配置界面的可用性。

## 4. 社区热点

今日讨论焦点集中在几个大型 Epic 和架构设计上，React 和评论数最高：

-   **[#7732 [OPEN] Epic: Persistent per-user sandbox with iron-proxy; defer loop executors](https://github.com/nearai/ironclaw/issues/7732)** (8条评论)
    -   **诉求**：社区对“持久化用户沙箱”的架构方案非常关注。当前实现为每个命令创建/销毁容器的做法效率低下。该 Epic 提出引入 `iron-proxy` 代理，并为每个 `(tenant, user)` 维护一个持久化的工作区。相关实现 PR [#7779](https://github.com/nearai/ironclaw/pull/7779) 已提交，讨论焦点在于网络的隔离与代理的运维成本。

-   **[#7770 [OPEN] Epic: hook the agent lifecycle...](https://github.com/nearai/ironclaw/issues/7770)** (3条评论)
    -   **诉求**：开发者希望扩展 `ironclaw_hooks` 机制，将 Agent 生命周期事件（轮次结束、开始、压缩等）全部 Hook 化，从而避免为核心引擎频繁打补丁。这是对可扩展性和模块化架构的强烈需求。首个 Phase 1 的 PR [#7765](https://github.com/nearai/ironclaw/pull/7765) 已在进行中。

-   **[#7038 / #7781 / #7782 WebUI 设计系统 Epics](https://github.com/nearai/ironclaw/issues/7038)**
    -   **诉求**：WebUI 设计系统被重新划分为 3 个 Epic 以更好地管理进度。社区在 [#7042](https://github.com/nearai/ironclaw/issues/7042) 中讨论 `DESIGN.md` 治理规则，希望建立统一的 UI 开发规范和主题。这反映了项目对产品化和一致用户体验的重视。

## 5. Bug 与稳定性

今日报告的 Bug 按严重程度排列：

-   **高**：
    -   [#7783 LLM timeout policy: finalization can't measure TTFT...](https://github.com/nearai/ironclaw/issues/7783)：非流式客户端的超时策略缺陷，可能导致整个运行在重试前被杀掉。暂无关联 fix PR。
    -   [#7786 (PR) uniqueItems broke every OpenAI-backed generation](https://github.com/nearai/ironclaw/pull/7786)：JSON Schema 中的 `uniqueItems` 参数导致所有 OpenAI 支持的内容生成失败。**此 PR 已合并，修复已完成**。
-   **中**：
    -   [#7776 memory.write needs an expected-version mode...](https://github.com/nearai/ironclaw/issues/7776)：`memory.write` 的 CAS 机制无法防止静默覆盖并发写入，可能导致数据丢失。
    -   [#7780 AfterTurn hook: scheduler-side failure terminalization bypasses the point](https://github.com/nearai/ironclaw/issues/7780)：`AfterTurn` Hook 无法在调度器侧失败路径上触发，事件可能存在遗漏。
-   **低**：
    -   [#7767 Automation presenter date tests timezone-robust](https://github.com/nearai/ironclaw/issues/7767)：测试因时区依赖而不稳定，相关修复 PR [#7774](https://github.com/nearai/ironclaw/pull/7774) 已提交。
    -   [#7308 Hosted MCP OAuth registration for Attio fails...](https://github.com/nearai/ironclaw/issues/7308) 已被关闭，但未说明具体解决方案，可能是外部问题。

## 6. 功能请求与路线图信号

-   **明确的路线图信号**：
    -   **v1.4.0 功能集**：包括 [#7732](https://github.com/nearai/ironclaw/issues/7732)（持久化沙箱）和 [#7781](https://github.com/nearai/ironclaw/issues/7781)（设计系统 Phase 2-3）。
    -   **Hook 系统扩展**：`#7770` Epic 明确规划了后续 Phase，`AfterTurn` Hook  (#7765) 只是第一步。后续可能引入 `BeforeTurn`、`Compaction` 等 Hook（#7770, #7780）。
-   **值得关注的新需求**：
    -   [#7775 Unbound runs: skip a gating capability instead of aborting](https://github.com/nearai/ironclaw/issues/7775)：建议无绑定运行时跳过门控能力而不是中止，这是对后台任务健壮性的增强。
    -   [#7769 Surface extension setup phase and blockers in Configure](https://github.com/nearai/ironclaw/issues/7769)：WebUI 的配置页面需要更全面地展示扩展的设置状态和阻塞项。

## 7. 用户反馈摘要

-   **对架构复杂性的关注**：来自 #7732 的讨论表明，用户和开发者都对当前“每次命令启动一个容器”的沙箱实现不满意，认为其效率低下且不符合“持久化电脑”的预期，推动了 `iron-proxy` 方案的提出。
-   **对流程的抱怨**：来自 #7308 的关闭反馈较少，但其主题“OAuth 注册失败且无法纠正”反映出一旦配置错误，用户的纠错成本很高。
-   **对工具链的痛点**：#7777 和 #7778 的快速修复侧面反映出工具链更新（Rust 1.98）对项目日常开发的直接影响，这一过程需要更平滑的 CI/CD 策略。

## 8. 待处理积压

以下 PR 已打开多日且未被合并或关闭，请维护者予以关注：

-   **[#7491 [OPEN] feat(coding): omp core-tool contract + engines + benchmark arm](https://github.com/nearai/ironclaw/pull/7491)** (自 2026-08-11 起)：这是一个大型功能 PR，涉及核心编码工具的重构。已打开近 10 天，需要维护者评估其状态。
-   **[#7699 [OPEN] feat(notifications): publish actionable run gates](https://github.com/nearai/ironclaw/pull/7699)** 与 **[#7698 [OPEN] feat(webui): generalize the notification center](https://github.com/nearai/ironclaw/pull/7698)** (自 2026-08-17 起)：两个关于通知中心的大型功能 PR 已经停留数日，等待审核。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-21

## 1. 今日速览

过去 24 小时项目活跃度中等偏上，共产生 9 条更新（2 条 Issues + 7 条 PR），无新版本发布。值得关注的是，7 条 PR 中有 6 条已合并/关闭，合并率高达 86%，说明维护者处理贡献的速度较快。今日合并的 PR 涵盖 Agent 技能同步 bug 修复、引擎启动超时交互优化、Write 工具文件卡片与预览面板（功能增强）、macOS 打包修复、设置面板搜索、Agent 切换 bug 修复等 6 个方向，项目在**功能体验优化**和**稳定性修复**两个维度均有明显推进。社区侧目前活跃度偏低——2 条 Issues 均处于 stale 状态，评论数有限，且无高赞反馈，社区讨论氛围有待观察。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日合并/关闭的 6 条 PR 中有 5 条为功能修复/增强并成功合并，项目整体在以下方面取得进展：

### 🔧 核心功能增强
- **PR #1553 — Write 工具文件卡片及分屏预览面板**（合并，关闭 #1552）：为 Write 工具调用新增内联文件卡片（FileCard），显示文件名、路径、类型、大小及操作按钮；新增可拖拽调宽（320-900px）的右侧预览面板，支持 Markdown 渲染、HTML 沙箱 iframe、SVG 内联、图片展示、代码语法高亮。Read 工具保持标准摘要展示以避免批量读取时的视觉干扰。这是今日最重要的功能型合并，直接回应了 #1552 的产品需求。

### 🐛 稳定性修复
- **PR #1545 — Agent 技能列表同步修复**（合并，关闭 #1502）：修复 Agent 设置面板修改技能列表后，当前对话技能徽章不立即更新的问题（根因是 Redux 中 `skillIds` 与 `activeSkillIds` 未同步）。
- **PR #1560 — Agent 切换回聊天界面修复**（合并）：修复在"我的 Agent"界面编辑 Agent 后，点击原已选 Agent 无法返回聊天界面的问题。
- **PR #1547 — 定时任务通知渠道重置修复**（待合并，状态 OPEN）：修复通知渠道从 IM 改为"不通知"后，再次编辑时仍显示旧渠道的问题（+2 行 / -2 行小改动）。当前仍停留在待合并状态。

### 🛠️ 构建与体验优化
- **PR #1555 — macOS 打包修复**（合并）：修复 `npm run dist:mac:x64` 打包失败问题，根因是 macOS 不支持 `sha256sum`，已在脚本中加入 `shasum` 兼容。
- **PR #1557 — 设置面板搜索筛选**（合并）：设置弹窗左侧栏新增搜索框，支持中英文关键词按空格分词、AND 匹配过滤分类；当前 Tab 被过滤时自动切换，无匹配时展示提示文案。

> 📌 **注意**：PR #1547（定时任务修复）是今日唯一仍处于 OPEN 状态的 PR，提醒维护者确认后合并。

---

## 4. 社区热点

今日社区讨论热度较低，无高赞、多评论的讨论热点。2 条 Issues 均为 stale 状态，评论数分别为 2 和 1。相对值得关注的是：

- **Issue #1556 — IM 机器人配置指南 404**（OPEN，stale）：用户报告文档链接返回 404，附有截图，评论 2 条。属于文档可用性问题，虽不紧急但影响用户体验，建议尽快修复。

---

## 5. Bug 与稳定性

今日报告的 Bug 较少，按严重程度排列如下：

| 严重程度 | 问题描述 | Issue/PR | 是否有 Fix PR |
|---------|---------|--------------------------|--------------|
| 🟡 中等 | macOS `npm run dist:mac:x64` 打包失败（`sha256sum` 不支持） | PR #1555（已合并） | ✅ 已修复 |
| 🟡 中等 | 定时任务通知渠道改"不通知"后再次编辑仍显示旧渠道 | PR #1547（待合并） | ✅ 有修复，待合并 |
| 🟢 轻微 | Agent 编辑后点击原 Agent 无法切换回聊天界面 | PR #1560（已合并） | ✅ 已修复 |
| 🟢 轻微 | Agent 技能列表更新后聊天区技能徽章不刷新 | PR #1545（已合并） | ✅ 已修复 |
| ⚪ 文档 | IM 机器人配置指南链接 404 | Issue #1556（OPEN，stale） | ❌ 暂无 |

**结论**：今日报告的 Bug 均为中低严重度，其中 3 个已合并修复，1 个待合并（PR #1547），无高危崩溃或数据损坏类问题。文档 404 需维护者补充处理。

---

## 6. 功能请求与路线图信号

- **AI 产物 Markdown 预览及文件卡片支持**（Issue #1552，已关闭）→ 已由 **PR #1553** 实现并合并。该功能解决 Agent 通过 Write 工具创建文件后无法在应用内直接预览的问题，覆盖 Markdown、HTML、SVG、图片、代码等文件类型，并支持分屏拖拽调整宽度。**判断**：该特性已进入主分支，预计将出现在下一版本。
- **设置面板搜索筛选**（PR #1557，已合并）：提升多 Tab 设置面板的查找效率，属于 UX 打磨类功能，已合入主线。

**路线图信号**：暂无新的功能需求提出。结合今日合并的功能来看，项目当前的重心在**文件操作体验（预览/卡片）**和**设置面板可用性**上，下一版本预计包含上述特性。

---

## 7. 用户反馈摘要

- **文档可用性**：用户 darkSheep404 报告 IM 机器人配置指南链接返回 404，并附截图。说明文档链接管理存在疏漏，影响用户自助配置流程。
- **文件预览诉求**：#1552 提出者希望 Agent 生成的文件（Markdown/HTML/代码）能在应用内直接预览，避免 Read 全文贴入聊天占用对话空间或手动切换文件管理器的繁琐流程。该诉求已通过 PR #1553 落地，反馈闭环。
- **配置持久化**：PR #1547 揭示定时任务通知渠道选择"不通知"后无法正确回填，用户配置状态被错误持久化，属表单初始化逻辑缺陷。

> 综合来看，用户侧关注点集中在**文档可访问性**、**文件操作流畅度**和**配置状态准确性**三个方向，整体反馈中性偏正面，无强烈不满情绪。

---

## 8. 待处理积压

⚠️ 以下项目长期未获响应（均为 stale 状态），建议维护者关注：

| 项目 | 类型 | 创建时间 | 最后更新时间 | 备注 |
|------|------|---------|------------|------|
| **#1556 IM 机器人配置指南 404** | Issue | 2026-04-08 | 2026-08-20 | 文档链接失效，超 4 个月未处理，应尽快修复或更新链接 |
| **#1552 AI 产物 Markdown 预览支持** | Issue | 2026-04-08 | 2026-08-20 | 已被 PR #1553 实现并关闭，**可关闭** |
| **#1547 定时任务通知渠道重置** | PR | 2026-04-07 | 2026-08-20 | 修复已就绪但尚未合并，建议尽快 review 合入 |

**维护者行动建议**：
1. 处理 #1556 的文档 404 问题（更新链接或补全文档）。
2. 合并已就绪的 PR #1547。
3. 关闭已被实现覆盖的 Issue #1552。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-08-21

---

## 1. 今日速览

过去24小时内，Moltis 项目保持快速迭代节奏：**8 条 PR 更新**（4 条待合并，4 条已合并/关闭），**1 个安全相关 Issue 关闭**，并有**1 个新版本**（20260820.01）发布。最显著的进展集中在 **Web 安全加固** 与 **WhatsApp 通道修复** 两个方向：安全修复 PR #1216 合入（Vault 接口认证漏洞 CWE-306），同时 3 个 WhatsApp 相关的修复 PR（#1217/#1218/#1219）同日合并。值得关注的是，安全修复类 PR 自提交到合并仅用了一天，说明项目对安全问题的响应速度很快。当前仍有 **4 个待合并 PR**，包括涉及 Snyk Agent 供应链安全固定的 #1221，整体生态活跃度良好。

---

## 2. 版本发布

### 20260820.01

- **发布时间**：2026-08-20
- **发布链接**：[Moltis Releases](https://github.com/moltis-org/moltis/releases)

**说明**：本次发布为常规滚动版本，未附详细变更日志。结合同日合并的 PR 推断，该版本应包含 **Vault 接口认证修复（#1216）** 及 **WhatsApp 通道多项修复（#1217/#1218/#1219）**。

**迁移注意事项**：涉及 Vault 解锁/恢复接口的认证要求变更（破坏性），建议部署前确认现有客户端/脚本已适配 `AuthSession` 认证流程。

---

## 3. 项目进展

### 今日合并/关闭的 PR（4 条）

| PR | 标题 | 说明 |
|---|---|---|
| [#1216](https://github.com/moltis-org/moltis/pull/1216) | fix(httpd): require authentication for vault unlock and recovery | **安全修复**（已合并）。修复 CWE-306，杜绝未认证的远程暴力破解 Vault 风险 |
| [#1217](https://github.com/moltis-org/moltis/pull/1217) | fix(whatsapp): treat a reply to the bot as addressing it | **功能修复**。在 `mention` 模式下，回复机器人消息不再被丢弃 |
| [#1218](https://github.com/moltis-org/moltis/pull/1218) | fix(whatsapp): stop hardcoding the push name to "Moltis" | **体验修复**。机器人推送名称不再固定为 "Moltis"，尊重自定义配置 |
| [#1219](https://github.com/moltis-org/moltis/pull/1219) | fix(channels): make the untrusted-turn tool ceiling configurable | **配置灵活性**。将非可信会话的工具策略上限开放为可配置，避免误伤公共受众工具（源于 #1170 的回归修复） |

**整体评估**：以上合并意味着 Moltis 在 **Vault 安全、WhatsApp 端体验、工具策略灵活性** 三个维度均有实质进展，且修复了 #1170 引入的公共工具可用性回归问题。

### 今日待合并 PR（4 条）

- [#1222](https://github.com/moltis-org/moltis/pull/1222) — 校验沙箱镜像请求，防止恶意镜像引用（安全）
- [#1221](https://github.com/moltis-org/moltis/pull/1221) — 固定 Snyk Agent 扫描版本，防止供应链攻击（安全）
- [#1220](https://github.com/moltis-org/moltis/pull/1220) — WhatsApp 出站消息支持 Markdown 渲染（功能增强）
- [#468](https://github.com/moltis-org/moltis/pull/468) — Windows 平台 shell hooks 适配 cmd.exe（跨平台修复，已搁置 5 个月并有 CI 通过，值得关注）

---

## 4. 社区热点

今日没有高讨论量的 Issue 或 PR（评论数均为 0 或 undefined）。最值得关注的是 **#468**，这是被搁置近 5 个月的 PR，今日有新更新（2026-08-20），可能意味着维护者开始重新关注该议题。该 PR 解决 Windows 下 shell hooks 不可用的问题，对 Windows 用户有直接价值。

---

## 5. Bug 与稳定性

今日无新开 Bug，但有 1 个 **高严重度** Bug 被关闭：

| Issue | 严重度 | 状态 | 说明 |
|---|---|---|---|
| [#1177](https://github.com/moltis-org/moltis/issues/1177) Vault Unlock/Recovery 端点缺少认证（CWE-306） | **严重** 🔴 | ✅ 已关闭 | 任意未认证远端可暴力破解 Vault。**已由 PR #1216 修复并合入** |

**响应速度评价**：该 Issue 于 2026-07-30 提交，8 月 20 日修复合入，从报告到修复约 3 周，速度合理。

另外，PR #1219 明确提到修复了 #1170 引入的**回归问题**（非运营商用户工具策略被错误限制），该问题也已在本次合入中解决。

---

## 6. 功能请求与路线图信号

今日无新的功能请求 Issue，但待合并 PR 揭示了可能的路线图方向：

- **供应链安全**（#1221）：固定 Snyk Agent 版本，强化技能安全扫描，预计纳入下个版本
- **WhatsApp Markdown 渲染**（#1220）：消息展示增强，提升聊天体验
- **沙箱镜像校验**（#1222）：安全边界扩展，可能成为安全审计的默认配置

这些方向均指向 **安全加固** 与 **通道体验优化**，与当前合并内容保持一致性。

---

## 7. 用户反馈摘要

**正面反馈**：
- Issue #1177 提交者确认使用最新版本，并遵循了完整的 Preflight Checklist，流程规范。

**痛点信号**：
- PR #1218（WhatsApp 推名硬编码）反映出 **通道自定义能力不足** 的问题，用户期望完全控制机器人在群聊中的展示名称。
- 长期未合并的 #468（Windows shell hooks）暗示 **Windows 平台支持滞后**，跨平台体验仍有提升空间。
- PR #1220（Markdown 渲染）表明 **模型生成的 Markdown 在 WhatsApp 端不可读**，是实际使用中的体验痛点。

---

## 8. 待处理积压

| 项目 | 类型 | 搁置时长 | 说明 | 建议 |
|---|---|---|---|---|
| [#468](https://github.com/moltis-org/moltis/pull/468) Windows shell hooks 使用 cmd.exe | PR | 近 5 个月（2026-03-23 创建） | 已通过 Windows CI，作者已自测，今日有活动更新 | 建议维护者尽快 review 并合入，或明确给出反馈 |

---

## 项目健康度评估

| 指标 | 状态 | 说明 |
|---|---|---|
| 安全响应 | 🟢 优秀 | 高危漏同（CWE-306）3 周内闭环 |
| 迭代速度 | 🟢 活跃 | 日 8 条 PR，4 条合并 |
| 社区互动 | 🟡 中性 | 评论少，但活跃提交者集中在核心团队 |
| 跨平台支持 | 🟠 待改进 | Windows 适配长期搁置 |
| 维护响应 | 🟢 良好 | 有 PR 今日更新，维护者保持活跃 |

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-08-21

> 数据来源：github.com/agentscope-ai/CoPaw | 数据窗口：2026-08-20 ~ 2026-08-21


## 1. 今日速览

CoPaw 今日保持高度活跃：过去 24 小时内共处理 28 条 Issues（15 条新开/活跃，13 条关闭）和 50 条 PR（22 条待合并，28 条已合并/关闭），并发布了 v2.1.1-beta.1 版本。值得关注的是，今日关闭的 13 条 Issues 中包含多项长期悬而未决的问题（如 #6643 任务产出物目录管理、#6734 新建聊天改名、#6974 VPN 支持、#7102 长时间卡死、#7110 图片链接故障等），同时有多个高价值 PR 合入（含 PowerContext 记忆后端、QQ 会话隔离、envs.json 原子写入修复、响应卡产物展示等），项目在多条功能线上同时取得实质进展。社区讨论热度集中在多步任务中途停止、长会话卡顿、模型路由等核心体验问题上，整体生态活跃且健康。


## 2. 版本发布

**v2.1.1-beta.1**（Beta 预发布）

**包含内容：**
- feat(console): 改进编辑器标签页溢出导航（PR #6983）
- fix(providers): 降低速率限制器初始化日志级别（PR #6988）
- chore: 更新发布说明

> ⚠️ 该版本为 Beta 预发布版本，主要面向测试验证。未发现破坏性变更。发布安装验证 Issue（#7180）已于 2026-08-20 自动创建，验证截止时间为当日 14:43 UTC。


## 3. 项目进展

### 已合入/关闭的重要 PR（按功能领域）：

| 领域 | PR | 内容 | 类型 |
|------|-----|------|------|
| 记忆系统 | #7080 | **新增可插拔 PowerContext 长期记忆后端**，通过 `@memory_registry.register("powercontext")` 注册，成为 ReMe 之外的平级选项 | ✨ Feature |
| 消息渠道 | #7169 | **QQ 渠道会话隔离与回复路由修复**：隔离 C2C/群聊/频道/频道 DM 会话，保留会话派生的回复路由、定时发送等；路由缺失时安全失败 | 🐛 Fix |
| 环境变量 | #7135 | **envs.json 损坏保留 + 原子写入**：修复损坏文件被静默覆盖导致环境变量丢失的问题（对应用户报告 #7118） | 🐛 Fix |
| 前端控制台 | #7161 | 助手响应卡片新增产物（artifacts）展示 | ✨ Feature |
| 打包 | #7166 | qwenpawmail MCP 以独立 sidecar 形式随包发布 | 🐛 Fix |
| 技能系统 | #7073 | 技能名去重，防止 workspace 自定义技能与内置技能重复加载 | 🐛 Fix |
| 文件下载 | #6371 | 下载器超时后继续 fallback（wget→curl→urllib）；修复 `subprocess.TimeoutExpired` 逃逸问题（对应 #6370） | 🐛 Fix |
| 市场 | #6880 | **统一应用/插件/技能市场**：共享 `/market` 页面，保留各自业务逻辑 | ✨ Feature |
| 驱动 | #7174 | **持久化驱动并发初始化**：缩短冷启动时间，保持故障隔离与原子发布语义 | ⚡ Perf |

**整体进展评估：** 今日合入 PR 横跨记忆后端可插拔化、QQ 渠道稳定性、前端产物展示、性能优化等 7 个方向，标志项目正从"单个 Agent 框架"向"多渠道 + 可插拔记忆 + 统一市场"的平台形态演进。


## 4. 社区热点

| 排名 | Issue/PR | 评论数 | 主题 | 诉求分析 |
|------|----------|--------|------|----------|
| 🥇 | [#6921 多步任务中途停止](https://github.com/agentscope-ai/QwenPaw/issues/6921) | 10 | Agent 规划下一步后无提示停止，需用户说"继续"才恢复 | **核心痛点**：任务执行可靠性。模型输出规划后未实际执行，缺少视觉提示。多用户反馈此问题，渴望"一次性全自动"完成多步任务 |
| 🥈 | [#7102 超过10分钟卡死](https://github.com/agentscope-ai/QwenPaw/issues/7102) | 9 | 使用 GLM 5.3 时完全冻结，超过 5 分钟无任何 token 输出 | **稳定性担忧**：长时间无响应使用户无法判断是正常思考还是故障。已关闭，但用户对"等待 vs 放弃"的焦虑值得关注 |
| 🥉 | [#6643 任务产出物目录混乱](https://github.com/agentscope-ai/QwenPaw/issues/6643) | 6 | 所有任务产物都堆在 media 目录下 | **工作区组织**：用户希望按任务隔离产出物。已关闭，说明方案已推进或合入 |

**热度总结：** 今日高热度议题集中于**任务执行可靠性与可观测性**——用户需要 Agent 能"主动继续"而非等待提示，且需要更清晰的进度反馈。


## 5. Bug 与稳定性

### 🔴 严重（功能不可用/数据风险）

| Issue | 链接 | 描述 | 状态 |
|-------|------|------|------|
| **history.db 撑爆至 7.6GB** | [#7168](https://github.com/agentscope-ai/QwenPaw/issues/7168) | `recall_history` 的 expand 把工具完整输出整段落库，且同一区间被重复写入。长期运行后数据库膨胀至 7.6GB | 🟡 Open — **无 PR** |
| **envs.json 损坏静默丢失所有环境变量** | [#7118](https://github.com/agentscope-ai/QwenPaw/issues/7118) | 单个无法解析的字节导致全部 env 丢失，下次写入固化损失 | ✅ 已关闭 — 已有修复 PR #7135 合入 |
| **流式输出中断 ReadError 不重试** | [#7162](https://github.com/agentscope-ai/QwenPaw/issues/7162) | `httpx.ReadError` 漏掉 `_get_httpx_retryable()` 导致偶发 UNKNOWN_AGENT_ERROR | ✅ 已关闭 |

### 🟠 中等（功能受限/体验受损）

| Issue | 链接 | 描述 | 状态 |
|-------|------|------|------|
| **网络恢复后无法自动重连** | [#6932](https://github.com/agentscope-ai/QwenPaw/issues/6932) | 短暂断网后所有 LLM 请求持续超时，必须手动重启进程（同日复现 2 次） | 🟡 Open — **无 PR** |
| **embedding health check 超时** | [#7156](https://github.com/agentscope-ai/QwenPaw/issues/7156) | 后端已预热仍超时（>5s），timeout 硬编码无法配置；`_get_httpx_retryable()` 漏掉 ReadError | 🟡 Open — 有相关 PR #7133（WIP：更新 reme 0.4.1.8，增加可配置超时） |
| **无法下载的图片链接使整个会话不可用** | [#7110](https://github.com/agentscope-ai/QwenPaw/issues/7110) | 消息记录中一个无法访问的图片链接导致整个会话挂掉，只能 `/clear` | ✅ 已关闭 |

### 🟢 轻微

| Issue | 链接 | 描述 | 状态 |
|-------|------|------|------|
| **助手消息结束时间显示异常** | [#6826](https://github.com/agentscope-ai/QwenPaw/issues/6826) | 实际耗时 2min 但页面显示仅几秒 | ✅ 已关闭 |
| **view_video inline-media cap 硬编码 2MB** | [#7060](https://github.com/agentscope-ai/QwenPaw/issues/7060) | provider 的 `max_inline_media_bytes` 配置对视频路径无效 | ✅ 已关闭 |
| **主密钥文件权限未按文档创建为 0o600** | PR [#7119](https://github.com/agentscope-ai/QwenPaw/pull/7119) | 安全加固：master key 文件权限修正（安全） | 🟡 Open 待合并 |


## 6. 功能请求与路线图信号

### 社区高频新需求（可能纳入下版本）

| 需求 | Issue | 信号强度 | 分析 |
|------|-------|----------|------|
| **自动模型路由**：每消息动态选择最合适的模型 | [#6436](https://github.com/agentscope-ai/QwenPaw/issues/6436) | ⭐⭐⭐（👍1，多评论，持续讨论近1月） | 用户希望简单轮次用快模型、图像自动切视觉模型、复杂推理用大模型。当前版本已支持 Session 级 thinking 模式（PR #7163 新增 Off/Low/Medium/High），自动路由是下一自然演进 |
| **统一工具面板 + Web 服务预览 + 交互式终端** | [#7013](https://github.com/agentscope-ai/QwenPaw/issues/7013) | ⭐⭐⭐ | 用户希望 Chat 页面有统一的"工具面板/工作台"，含文件 Diff、Web 服务预览、终端。与"任务产物目录管理"（#6643）同属工作区体验升级方向 |
| **Agent 级跨会话召回开关（Scroll）** | [#7184](https://github.com/agentscope-ai/QwenPaw/issues/7184) | ⭐⭐（同日已有配套 PR #7183 合入） | 用户希望控制新会话是否可召回其他会话，同时保留持久历史、多轮上下文、压缩与恢复。已有配套 PR 合入，**落地概率高** |
| **workspace 级 always-on Skills** | [#7182](https://github.com/agentscope-ai/QwenPaw/issues/7182) / PR [#7183](https://github.com/agentscope-ai/QwenPaw/pull/7183) | ⭐⭐⭐（PR 已提交） | 常驻技能在 Agent 首次决策前加载到系统提示，减少专业技能 agent 的指令遗漏。**已在开发中，预计下版本合入** |
| **支持 Qwen_Code 作为第三方 Agent harness** | [#7181](https://github.com/agentscope-ai/QwenPaw/issues/7181) | ⭐⭐ | 网络受限用户需要本地代码执行 harness，认为比 ACP 更好 |

### 中长线信号

| 需求 | Issue | 分析 |
|------|-------|------|
| **自托管多用户 Hub（QwenPaw Hub）** | PR [#7112](https://github.com/agentscope-ai/QwenPaw/pull/7112) | 新增 opt-in 多用户控制平面，为各本地账户运行隔离的 App 实例。指向团队/企业级部署方向，仍待合并 |
| **DingTalk 群聊上下文模式可配置** | [#7158](https://github.com/agentscope-ai/QwenPaw/issues/7158) | 同群默认用户隔离，指定群可开启共享上下文。渠道能力的精细化配置信号 |
| **QQ 群主动推送（定时任务）** | [#7159](https://github.com/agentscope-ai/QwenPaw/issues/7159) | 腾讯已开放主动推送消息能力。若实现将解锁定时任务、群内主动提醒等场景 |
| **技能导入搜索/过滤** | [#7090](https://github.com/agentscope-ai/QwenPaw/issues/7090) | 技能池达数百时 `questionary.checkbox` 无法搜索。已在 PR #6880（统一市场）中部分覆盖 |


## 7. 用户反馈摘要

**真实痛点（高优先级）：**

- **"说话不算话"的 Agent**（#6921）：用户 rerbin 报告 Agent 规划好下一步后停止，需手动说"继续"。评论区用户对"原因是什么、什么时候该干预"感到困惑——这本质上是 **Agent 自主性与可观测性**问题。
- **网络抖动即服务"脑死"**（#6932）：用户 tina0501853 指出 QwenPaw 在短暂断网后无法自愈，必须重启进程，一天内复现两次。**"常见瞬态事件不应需要人工介入"** 是核心期望。
- **会话被一个坏图片"杀死"**（#7110）：用户 zcmk123 遇到消息记录中一个无法访问的图片链接导致整个会话不可用，只能 `/clear`。"**一个坏链接 = 会话报废**" 是严重的韧性缺陷。
- **环境变量被静默清空**（#7118）：用户 Yigtwxx 报告 `envs.json` 中一个损坏字节导致所有环境变量丢失。**"静默丢失已保存配置"** 是对信任的严重打击。

**使用场景洞察：**
- 用户 rerbin（贡献型用户：多条 Issue + 建议）持续围绕**工作区组织**（#6643、#6453、#6734）提出改进，说明其在日常任务中重度使用文件处理与多任务管理
- 用户 wuyak 同日提出两个新功能请求（#7184 跨会话召回开关、#7182 always-on Skills）并提交了配套 PR #7183，显示**技术用户正积极参与开发**，能快速从需求到实现
- **移动端体验**开始被关注（#7177 rerbin 反馈 deploy 首页操作不便，担心误触停止按钮）

**满意点（从已解决问题推断）：**
- 今日关闭的 13 条 Issue 中有多条长期问题（#6643 创建于 8/3、#6453 创建于 7/24、#6734 创建于 8/6），说明**维护者持续清理积压问题**，响应周期可观


## 8. 待处理积压

| 项目 | 创建时间 | 类型 | 链接 | 备注 |
|------|----------|------|------|------|
| **#6436 自动模型路由** | 2026-07-24 | 功能请求 | [链接](https://github.com/agentscope-ai/QwenPaw/issues/6436) | 近 1 个月，4 评论，反复被社区提及（"The Right Model for Every Message"），今日仍有更新。属于路线图级功能，建议维护者明确反馈计划 |
| **#6921 多步任务中途停止** | 2026-08-12 | Bug | [链接](https://github.com/agentscope-ai/QwenPaw/issues/6921) | **当前讨论热度最高（10 评论）**，影响多步任务执行核心体验。尚无专人认领或 PR 关联，建议尽快排查 |
| **#6932 网络恢复后无法自动重连** | 2026-08-12 | Bug | [链接](https://github.com/agentscope-ai/QwenPaw/issues/6932) | 同日复现两次的稳定性问题，无 PR 关联，建议纳入稳定性迭代 |
| PR #6399 reranker UI 配置面板 | 2026-07-23 | PR（待合并） | [链接](https://github.com/agentscope-ai/QwenPaw/pull/6399) | 创建近 1 个月仍在 Under Review，建议维护者确认状态或补充意见 |
| PR #7112 QwenPaw Hub 自托管多用户 | 2026-08-18 | PR（待合并） | [链接](https://github.com/agentscope-ai/QwenPaw/pull/7112) | 涉及范围较大（多用户控制平面），可能需要更多设计评审，建议明确时间预期 |


> **总结：** CoPaw 项目健康度良好——发布节奏稳定（Beta 版本周期约两周），PR 合入效率高（当日 28 条 PR 闭环），Community 参与度深（用户提交 PR 比例高，从 Issue 到实现周期短至数日）。当前最需关注的风险点是**任务中断与网络自愈**两个核心稳定性问题（#6921、#6932），以及 history.db 膨胀的长期数据风险（#7168）。从路线图信号看，项目正加速平台化（Hub 多用户、统一市场、记忆后端可插拔），方向清晰。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，我是你的 AI 智能体与个人 AI 助手领域开源项目分析师。根据 ZeroClaw 提供的 GitHub 数据，我生成了以下项目动态日报。

---

# ZeroClaw 项目动态日报 - 2026-08-21

## 1. 今日速览

ZeroClaw 项目今日活跃度较高，核心贡献者和维护者围绕架构演进（特别是 WASM 插件系统、运行时生命周期、沙箱安全策略）展开了密集的讨论与协作。尽管没有新版本发布，但 45 个新开/活跃的 Issue 和 48 个待合并的 PR 表明项目正处于功能开发与重构的加速期。当前社区热点集中在对核心架构（如运行时所有权、内存生命周期）的 RFC 讨论，以及“默认安全/好用”的配置项调整。然而，PR 合并率较低（仅 2/50），且大量高优先级（P1）安全修复 PR 卡在 `needs-author-action` 状态，可能导致部分安全改进交付延迟。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

尽管今日仅合并/关闭了 2 个 PR，但这是几个大型功能 PR 逐步收敛的前奏。主要进展体现在架构文档的完善：

- **ADR-014 (执行树预算所有权)**：[PR #9415](https://github.com/zeroclaw-labs/zeroclaw/pull/9415) 已合并。该 PR 记录了执行树中预算所有权的设计决策，为后续运行时资源管理提供架构指引。
- **修复 max_images 配置被静默截断的问题**：[PR #9578](https://github.com/zeroclaw-labs/zeroclaw/pull/9578) 已合并。该修复让 `multimodal.max_images` 配置项被正确执行，并在需要时报告钳制情况，消除了配置行为与实际不符的隐患。

此外，多个大型 PR（如 #10146、#9748）正在持续更新，逐步接近可合并状态。

## 4. 社区热点

今日讨论最激烈的议题反映了社区对项目核心架构的深度关注：

- **[RFC: Runtime-owned conversation sessions (Issue #9487)](https://github.com/zeroclaw-labs/zeroclaw/issues/9487)**：以 22 条评论成为焦点。该 RFC 旨在重构运行时对会话的所有权，并引入传输表面适配器。高关注度表明社区对当前运行时架构的局限有共识，且希望参与早期设计。
- **[Tracker: Rust anti-slop policy debt remediation (Issue #10118)](https://github.com/zeroclaw-labs/zeroclaw/issues/10118)**：16 条评论。该项目治理事务引发了核心贡献者的广泛共鸣，他们愿意投入精力解决技术债，提升代码库的长期健康度。
- **[RFC: Decouple memory lifecycle policy from storage backends (Issue #6850)](https://github.com/zeroclaw-labs/zeroclaw/issues/6850)**：14 条评论。与 #9487 类似，社区急切希望明确内存管理等核心组件的职责边界，显示出对系统可维护性和扩展性的重视。

## 5. Bug 与稳定性

今日报告的 Bug 涉及功能缺陷、文档过时和平台兼容性问题，按严重程度排列如下：

- **P1 - 关键**：
    - **PR 审查结果发布竞态条件**：[Issue #10194](https://github.com/zeroclaw-labs/zeroclaw/issues/10194)（已关闭）。PR 合并后，AI 审查器仍会发布结果，可能造成信息混乱。已关闭，说明得到了快速处理。
- **P2 - 严重 (S2)**：
    - **代理上下文被错误限制在 32K tokens**：[Issue #10068](https://github.com/zeroclaw-labs/zeroclaw/issues/10068)。该 Bug 导致用户配置的 `max_context_tokens = 131072` 不生效，严重削弱了长对话场景下的代理能力。
    - **代理选择器拒绝支持的转录服务**：[Issue #10106](https://github.com/zeroclaw-labs/zeroclaw/issues/10106)。配置缺陷导致部分转录服务无法使用。
    - **安装失败：Windows 桌面版入口点错误**：[Issue #10111](https://github.com/zeroclaw-labs/zeroclaw/issues/10111)（已关闭）。用户安装后无法启动程序。
    - **CI 与文档不一致**：[Issue #10074](https://github.com/zeroclaw-labs/zeroclaw/issues/10074)。`SECURITY.md` 文档描述的 CI 安全验证已失效，需要更新文档或恢复 CI 流程。
- **P3 - 轻微 (S3)**：
    - **ZeroCode 健康状态语种对齐问题**：[Issue #10103](https://github.com/zeroclaw-labs/zeroclaw/issues/10103)。界面标签宽度不一致，影响多语言环境的显示效果。

**相关修复 PR**: 针对上述 Bug，目前已有 PR #9635、#9637、#9678 等正在进行修复，但均处于 `needs-author-action` 状态，需作者配合更新。

## 6. 功能请求与路线图信号

今日功能请求和 RFC 集中于两个主题：**“万物皆插件”** 与 **“默认更优”**。

- **插件系统深化**：多个高热度 RFC 和 PR（如 [Issue #10076](https://github.com/zeroclaw-labs/zeroclaw/issues/10076)、[PR #10146](https://github.com/zeroclaw-labs/zeroclaw/pull/10146)、[PR #9128](https://github.com/zeroclaw-labs/zeroclaw/pull/9128)）都指向一个方向：将更多可选功能（如渠道、工具）从编译期特性标志迁移到运行时 WASM 插件。这将是未来几个版本的核心方向，旨在缩小默认二进制体积并提升扩展性。
- **默认配置优化**：多个新 Issue 和已接受的 Feature 表明，项目正在审查并改进默认行为，以提升开箱即用的体验：
    - [Issue #10168](https://github.com/zeroclaw-labs/zeroclaw/issues/10168) 建议默认启用停顿看门狗，避免任务无限期挂起。
    - [Issue #10166](https://github.com/zeroclaw-labs/zeroclaw/issues/10166) 建议默认开启 `partial` 流式输出，提升交互响应感。
    - [Issue #10087](https://github.com/zeroclaw-labs/zeroclaw/issues/10087) 建议将 `memory-postgres` 测试纳入必需 CI，保障数据库后端的稳定性。

## 7. 用户反馈摘要

从今日的 Issue 评论中可以提炼出用户画像与诉求：

- **自托管与生产部署用户**：对 [MariaDB 后端支持](https://github.com/zeroclaw-labs/zeroclaw/issues/4668)（#4668）、[配置行为一致性](https://github.com/zeroclaw-labs/zeroclaw/issues/9578)（#9578）有强烈需求，反映出用户希望项目能无缝融入其现有基础设施。
- **高级用户与开发者**：深度参与 RFC 讨论，如 #9487、#6850，显示出社区期待更清晰、更模块化的架构，以支持复杂的自定义场景。
- **对安全性的敏感性**：多个高优先级 Issue 和 PR 围绕 Git 安全策略、插件权限、沙箱限制展开，说明用户对安全、尤其是 AI Agent 的权限管控有很高的要求。
- **对开箱即用体验的抱怨**：[Issue #10068](https://github.com/zeroclaw-labs/zeroclaw/issues/10068) 和 #10166 的提出，暗示用户对需要深入配置才能获得良好体验感到不满，期望项目提供更合理的默认值。

## 8. 待处理积压

以下高价值且长期未合并的 PR 需要特别关注，其中多数处于等待作者响应状态：

- **[PR #9109](https://github.com/zeroclaw-labs/zeroclaw/pull/9109) feat(providers): add native Hailo-Ollama support**：新增硬件加速推理支持，但已打开超过一个月且 `needs-author-action`。这可能导致有意使用 Hailo 加速的用户流失。
- **[PR #9637](https://github.com/zeroclaw-labs/zeroclaw/pull/9637) fix(ci): guard temporary React Router RSC exception**：带有 `do-not-merge` 标签，但作为 P1 的 CI 修复，长期挂起会阻碍依赖更新流程。
- **[PR #9678](https://github.com/zeroclaw-labs/zeroclaw/pull/9678) fix(config): harden Git shell policy arguments** 与 **[PR #9635](https://github.com/zeroclaw-labs/zeroclaw/pull/9635) fix(config): resolve git subcommand past global options in risk classifier**：两个高风险的 Git 安全策略修复，都卡在作者响应阶段。安全修复的延迟可能使部分部署暴露在潜在风险中。
- **[PR #9635](https://github.com/zeroclaw-labs/zeroclaw/pull/9635) fix(config): resolve git subcommand...**：与 #9678 关联的另一个安全修复（S 级大小），也处于待作者响应状态。

**建议**：维护者可通过关注这些阻塞的 PR，联系作者或接手进行修订，以加速关键修复的合入。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*