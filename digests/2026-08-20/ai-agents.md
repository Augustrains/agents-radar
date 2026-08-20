# OpenClaw 生态日报 2026-08-20

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-20 00:30 UTC

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

# OpenClaw 项目动态日报 — 2026-08-20

## 1. 今日速览

OpenClaw 项目今日保持高强度运转，过去 24 小时共产生 500 条 Issue 更新与 500 条 PR 更新，社区活跃度处于高位。Issue 侧以"会话状态丢失"和"消息丢失"类问题最为集中，多个 P1 级 bug 长期滞留（如 #44925、#62505）。PR 侧修复节奏明显加快，今日有 93 条 PR 被合并或关闭，合并率 18.6%，其中 7 条由维护者（steipete、jesse-merhi、joshavant）提交并在 24 小时内完成合并，显示维护团队正对积压问题展开集中清理。值得关注的是，多个关键修复（#126205、#125002、#119784）仍处于"等待作者"状态，合并周期较长。新版本发布为 0，项目处于 v2026.8.1-beta.2 的发布验证阶段（#125626）。

## 2. 版本发布

过去 24 小时无新版本发布。当前处于 **v2026.8.1-beta.2** 的社区验证阶段，验证跟踪 Issue 为 [#125626](https://github.com/openclaw/openclaw/issues/125626)，已有 13 条评论，测试者需通过 release-validation skill 提交反馈。另有一条与 beta 验证直接相关的修复已合入：[#126354](https://github.com/openclaw/openclaw/pull/126354) 修复了从 2026.7.2-beta.4 升级时 Doctor 误报成功但 Gateway 启动仍被拒的问题。

## 3. 项目进展

今日有 93 条 PR 被合并/关闭，以下为本日完成的关键变更：

**已合并（CLOSED）— 值得关注：**

- **[#126354](https://github.com/openclaw/openclaw/pull/126354) — fix(state): restore upgrades from 2026.7.2-beta.4 agent state** — 修复 beta 升级路径中 schema 不匹配问题，直接服务于当前 beta 验证。
- **[#126483](https://github.com/openclaw/openclaw/pull/126483) — fix(cron): honor failure alert thresholds** — 修复自动化任务失败告警频率失控问题。实测案例中一条 60 秒周期的监控在事故期间发出了 21 条告警。该 PR 从提交到合并仅用 1 天，响应迅速。
- **[#120900](https://github.com/openclaw/openclaw/pull/120900) — feat(ui): review install policy warnings** — 为 Control UI 增加安装策略警告的审核功能，管理员可查看警告并决定是否继续安装。这与此前合入的 [#116489](https://github.com/openclaw/openclaw/pull/116489)（安全安装策略框架）形成完整闭环。
- **[#116489](https://github.com/openclaw/openclaw/pull/116489) — feat(security): require acknowledgement for install policy warnings** — 外部 `security.installPolicy` 命令现在可返回 `warn`，交互式 CLI 安装将要求操作者输入确切的插件名以确认风险。这是安全边界的重要加固。

**仍开放但已具备合并条件（👀 ready for maintainer look）：**

- **[#126485](https://github.com/openclaw/openclaw/pull/126485) — fix(skills): keep workshop revisions atomic** — 修复 Skill Workshop 修订中断时 SQLite 记录与文件不一致的问题，由 steipete 提交。
- **[#126492](https://github.com/openclaw/openclaw/pull/126492) — fix: preserve GPT-5.6 Max and Ultra through Codex** — 修复通过 Codex 使用 GPT-5.6 Max/Ultra 时推理强度被静默降级的问题。
- **[#126487](https://github.com/openclaw/openclaw/pull/126487) — fix(memory-wiki): persist ChatGPT import run record before compiling the vault** — P0 级修复：编译失败时回滚记录丢失导致数据一致性风险。

**整体判断**：项目正在从"报告问题"阶段转向"集中修复"阶段。安全加固（安装策略确认、Claude CLI OAuth 恢复 #125471）和消息投递可靠性（#126205）是当前最高优先级的两个方向。

## 4. 社区热点

今日讨论热度最高的议题反映了两大核心诉求：**Realtime 语音的资源管理** 和 **会话状态持久化**。

| Issue/PR | 评论数 | 核心诉求 |
|---|---|---|
| [#116201](https://github.com/openclaw/openclaw/issues/116201) — Realtime voice work can retain unbounded provider and consult state | 60 | ⭐ 今日最热。Realtime 语音会话缺少硬性资源上限，慢速/卡住的 provider 可导致 superseded consult work、provider frames 和 pre-ready audio 无限累积。这直接关系到生产成本和稳定性，已被标记为 diamond lobster 级问题。 |
| [#44925](https://github.com/openclaw/openclaw/issues/44925) — Subagent completion silently lost | 26 | Subagent 任务完成通知失败（E31、E42、E45 错误）时结果静默丢失。无重试、无通知、无自动重启。该 Issue 已持续 5 个月，社区强烈关注。 |
| [#77598](https://github.com/openclaw/openclaw/issues/77598) — Track live dev agent behavior and trajectory | 22 | Pash 的 dev agent 24 小时观察记录，社区对 agent 自主行为的持续关注。 |
| [#62505](https://github.com/openclaw/openclaw/issues/62505) — Coding Agent never completes anything | 15 | 回归 bug：2026.4.2 及更早版本正常，之后 coding agent 完全停止工作。已持续 4 个月+，用户失望情绪明显，被标记为 diamond lobster。 |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) — "Cannot convert undefined or null to object" w/ google-vertex | 14 | 2026.3.2 版本引入的回归，影响 gemini-3.1-pro-preview，3 👍。 |
| [#108435](https://github.com/openclaw/openclaw/issues/108435) — Gateway fails to start after update to 2026.7.1 | 14 | P0 级启动失败，影响 systemd/ollama/手动启动所有方式。3 👍。 |

**分析**：社区热度集中在两个关键词 — **"静默丢失"** 和 **"回归"**。用户对 OpenClaw 的期望已经超过"能用就行"，而是要求在生产环境中的可靠性。特别是 #44925 和 #62505 已经持续数月，用户耐心正在消耗。

## 5. Bug 与稳定性

按严重程度排序的本日活跃 bug：

### 🔴 P0 — 阻断/崩溃

| Issue | 描述 | 状态 |
|---|---|---|
| [#108435](https://github.com/openclaw/openclaw/issues/108435) | 升级到 2026.7.1 后 Gateway 无法启动（所有启动方式） | 3 👍，已有 14 评论，**无 fix PR** |
| [#70903](https://github.com/openclaw/openclaw/issues/70903) | Provider 冷却状态持久化在文件中，充值后仍被锁定数小时 | P0，stale，**无 fix PR** |

### 🟠 P1 — 重要功能受损

| Issue | 描述 | 状态 |
|---|---|---|
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | Subagent 完成结果静默丢失 | 持续 5 个月，needs-maintainer-review，无 fix |
| [#62505](https://github.com/openclaw/openclaw/issues/62505) | Coding Agent 完全不工作（4.2 之后回归） | 持续 4 个月+，fix-shape-clear，可排队修复 |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | google-vertex 模型 "undefined or null" 错误 | 持续 5 个月+，需 live-repro |
| [#40001](https://github.com/openclaw/openclaw/issues/40001) | write 工具无追加模式，cron 会话覆盖共享文件 | 数据丢失风险，needs-product-decision |
| [#119796](https://github.com/openclaw/openclaw/issues/119796) | Windows vitest teardown EBUSY 锁文件 | 已 linked-pr-open |
| [#83959](https://github.com/openclaw/openclaw/issues/83959) | Codex app-server 启动重试耗尽 | linked-pr-open |
| [#125679](https://github.com/openclaw/openclaw/issues/125679) | Matrix 初始同步无限重启（回归，bisect 到 #125302） | CLOSED（已解决），platinum hermit |
| [#114211](https://github.com/openclaw/openclaw/issues/114211) | Matrix 房间 agent 循环 + 过期会话重放 | diamond lobster，需产品决策 |
| [#116512](https://github.com/openclaw/openclaw/issues/116512) | Telegram 进度模式下首条评论重复显示 | diamond lobster，source-repro |
| [#123273](https://github.com/openclaw/openclaw/issues/123273) | 非默认 agent 图片附件被拒绝 | diamond lobster，**已有 PR #126490 尝试解决** |
| [#92633](https://github.com/openclaw/openclaw/issues/92633) | memory_search corpus=all 超时 | diamond lobster |
| [#115546](https://github.com/openclaw/openclaw/issues/115546) | CLI-budget 压缩超时提前触发，100% 失败 | diamond lobster |
| [#106704](https://github.com/openclaw/openclaw/issues/106704) | sessions_yield 首轮静默终止子任务 | diamond lobster |

### 🟡 P2 — 一般问题

| Issue | 描述 | 状态 |
|---|---|---|
| [#88657](https://github.com/openclaw/openclaw/issues/88657) | DeepSeek V4 Flash 不完整回合 | 5.27/5.28 引入回归 |
| [#94939](https://github.com/openclaw/openclaw/issues/94939) | 6.x 迁移致 conversation-store SQLite 为空 | 已 linked-pr-open |
| [#114234](https://github.com/openclaw/openclaw/issues/114234) | usage-cost 刷新锁容器内 PID 复用 | 已 linked-pr-open |
| [#114612](https://github.com/openclaw/openclaw/issues/114612) | memory SQLite 无保留策略，磁盘将满 | 需产品决策 |
| [#120735](https://github.com/openclaw/openclaw/issues/120735) | Telegram 贴纸不可见/不可用 | 已 linked-pr-open |
| [#119401](https://github.com/openclaw/openclaw/issues/119401) | DM 中 NO_REPLY 抑制无视 silentReply 策略 | 需产品决策 |

**今日亮点修复**：

- **[#126483](https://github.com/openclaw/openclaw/pull/126483)** 修复 cron 失败告警风暴（已合并）
- **[#126354](https://github.com/openclaw/openclaw/pull/126354)** 修复 beta 升级 schema 不匹配（已合并）
- **[#126487](https://github.com/openclaw/openclaw/pull/126487)** 修复 wiki 导入失败时回滚记录丢失（P0，待合并）
- **[#126205](https://github.com/openclaw/openclaw/pull/126205)** 修复 durable delivery 后首条回复行为丢失（待合并）

## 6. 功能请求与路线图信号

以下功能需求在今日活跃的 Issue/PR 中具备较高实现可能性：

| 需求 | 来源 | 信号强度 |
|---|---|---|
| **write 工具追加模式** | [#40001](https://github.com/openclaw/openclaw/issues/40001) | 高 — 数据丢失风险，diamond lobster，社区 14 评论持续追踪 |
| **Subagent 优雅超时（预警告）** | [#6625](https://github.com/openclaw/openclaw/issues/6625) | 中高 — 已有明确提案（超时前 N 秒注入系统消息），持续 6 个月+ |
| **多槽位记忆架构** | [#60572](https://github.com/openclaw/openclaw/issues/60572) | 中 — 需要产品决策，3 👍 |
| **OpenRouter 使用成本暴露** | [#9016](https://github.com/openclaw/openclaw/issues/9016) | 中 — 用户希望 agent 能感知每次请求成本。**已有关联 PR [#92649](https://github.com/openclaw/openclaw/pull/92649)（Kimi 配额展示）** 正在扩展 provider 使用量管线，可能覆盖此需求。 |
| **Anthropic advisor tool 支持** | [#63930](https://github.com/openclaw/openclaw/issues/63930) | 中 — 涉及 server-side tool 通用支持，技术影响面较大 |
| **模型切换时上下文过大静默失败** | [#58957](https://github.com/openclaw/openclaw/issues/58957) | 中 — 影响模型切换体验，已有 2 👍 |
| **Onboarding 集成记忆配置** | [#16670](https://github.com/openclaw/openclaw/issues/16670) | 中 — 新人上手关键路径 |

**判断**：`write` 工具追加模式（#40001）是当前最有可能被纳入下一版本的功能改动 — 它直接影响数据安全，被标记为 diamond lobster，且有清晰的解决方案（增加 append 选项或引入独立工具）。

## 7. 用户反馈摘要

**最强烈的痛点：**

1. **"静默失败"是用户最大的挫败感来源。** #44925 中用户详细描述了三种不同的 subagent 失败模式（E31、E42、E45），全部表现为"结果消失但无任何提示"。评论区中用户表达了"完全无法信任 agent 的完成状态"的失望。同样，#62505 中用户描述 coding agent "只给出模糊的状态更新然后道歉"。

2. **模型切换的摩擦。** #120563 用户发现使用 Ollama 自定义 provider 时，对话历史根本不发送给模型 — "每个 turn 都是固定大小上下文"，这直接导致多轮对话质量崩溃。#88657 中 DeepSeek V4 Flash 在 5.27/5.28 突然不完整输出，用户只能停留在旧版本。

3. **记忆/状态的脆弱性。** #40001 用户指出 cron 隔离会话直接覆盖共享记忆文件的灾难性后果。用户称 "multiple sessions silently clobber each other's memory"。同时在 [#90361](https://github.com/openclaw/openclaw/issues/90361) 中，用户报告 memory_search 间歇性返回 "index metadata is missing"，虽然已本地热修复，但表明持久层仍有竞态问题。

4. **回归频率偏高。** 从 #62505（coding agent 回归）、#38327（google-vertex 回归）、#108435（Gateway 启动回归）、到 #125679（Matrix sync 回归），用户多次强调 "worked before, now fails"。这种模式消耗信任。

**正面反馈：**

- 维护者对 #119796（Windows EBUSY）和 #114234（容器 PID 复用）等平台特定问题有响应且有 linked PR。
- #120900 和 #116489 的安装策略确认机制获得了社区认可 — 用户对精确到输入插件名才确认的设计表示赞赏。
- #92649（Kimi 配额展示）的持续更新表明维护者重视第三方 provider 集成体验。

## 8. 待处理积压

以下为长期未解决且需要维护者关注的关键项：

| 项目 | 持续时间 | 严重度 | 状态 |
|---|---|---|---|
| [#44925](https://github.com/openclaw/openclaw/issues/44925) — Subagent 结果静默丢失 | 5 个月+（3/13 开放） | P1，diamond lobster | needs-maintainer-review；无 fix PR |
| [#62505](https://github.com/openclaw/openclaw/issues/62505) — Coding Agent 回归失效 | 4 个月+（4/7 开放） | P1，diamond lobster | fix-shape-clear，可排队修复 |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) — google-vertex 错误 | 5 个月+（3/6 开放） | P1，platinum hermit | 需 live-repro；无 fix |
| [#70903](https://github.com/openclaw/openclaw/issues/70903) — Provider 冷却永久锁定 | 4 个月+（4/24 开放） | P0，diamond lobster | stale；需产品决策 |
| [#40001](https://github.com/openclaw/openclaw/issues/40001) — write 工具无追加模式 | 5 个月+（3/8 开放） | P1，diamond lobster | 需产品决策；无 fix |
| [#16670](https://github.com/openclaw/openclaw/issues/16670) — Onboarding 缺少记忆配置 | 6 个月+（2/15 开放） | P2 | 需产品决策 |
| [#43374](https://github.com/openclaw/openclaw/issues/43374) — 多 agent 并发 LLM 超时 | 5 个月+（3/11 开放） | P3 | 需用户补充信息 |
| [#9016](https://github.com/openclaw/openclaw/issues/9016) — OpenRouter 成本暴露 | 6 个月+（2/4 开放） | P3 | 需产品决策；#92649 可能部分覆盖 |
| [#122846](https://github.com/openclaw/openclaw/pull/122846) — 工具调用块上限 | ⏳ 8/12 开放 | 直接影响 CLI 稳定性 | 大型 PR（覆盖几乎所有 channel/extensions），需仔细 review |

**给维护者的话**：今日数据最值得关注的是长期 P1/P0 问题（#44925、#62505、#70903）持续数月无实质进展，同时新问题持续涌入。建议将 #44925 的"失败通知机制"作为基础设施优先建设 — 它会影响所有 subagent 工作流。另外 note 到 #62505 已标记 fix-shape-clear，排队等待修复，但排队已超过 4 个月。修复回归问题的优先级应高于新功能开发。

---

## 横向生态对比

# 个人 AI 助手/自主智能体开源生态横向对比分析报告

**报告日期**: 2026-08-20  
**数据窗口**: 2026-08-19 至 2026-08-20  
**覆盖项目**: OpenClaw、NanoBot、Hermes Agent、PicoClaw、NanoClaw、NullClaw、IronClaw、LobsterAI、TinyClaw、Moltis、CoPaw、ZeptoClaw、ZeroClaw


## 1. 生态全景

个人 AI 助手/自主智能体开源生态正处于**从"功能堆叠"向"生产级可靠性"转型的关键阶段**。头部项目（OpenClaw、IronClaw、ZeroClaw）保持高强度迭代，日均 PR 更新量达 50-500 条，但共性痛点是**"静默失败"和"回归 bug"**——Subagent 结果丢失、上下文超限无提示、更新后功能失效等问题的反复出现，正在消耗用户对"自主智能体"的信任。与此同时，多通道整合（Telegram、Discord、Slack、WhatsApp）成为差异化竞争焦点，安全加固（安装策略确认、OAuth 凭据管理、漏洞修复）被普遍提升至 P0/P1 优先级。生态整体呈现**"头部活跃、腰部分化、尾部沉寂"**的格局，而**沙箱持久化、会话状态管理和跨平台一致性**是各项目共同的技术攻坚方向。


## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | 合并/关闭 PR | Release | 健康度 | 活跃度分级 |
|------|------------|---------|-------------|---------|--------|-----------|
| **OpenClaw** | 500 | 500 | 93 (18.6%) | 无（v2026.8.1-beta.2 验证中） | 🟡 集中修复期，长期 P1 积压 | 🔥 极高 |
| **ZeroClaw** | 42 | 50 | 2 (4%) | 无（v0.8.4 → v0.9.0 过渡） | 🟡 评审积压，合并率低 | 🔥 高 |
| **IronClaw** | 14 | 38 | 多项核心合并 | ✅ **v1.3.0 稳定版** | 🟢 健康上升期 | 🔥 高 |
| **NanoClaw** | 3 | 34 | 25 (73.5%) | 无 | 🟢 快速迭代期 | 🔥 高 |
| **NanoBot** | 5 | 24 | 8 (33%) | 无 | 🟢 响应迅速，但待合并积压 | 中高 |
| **Hermes Agent** | 50 | 50 | 8 (16%) | 无 | 🟡 维护者带宽不足 | 中高 |
| **Moltis** | 3 关闭 | 5 合并 + 5 待审 | 5 | ✅ **20260818.10** | 🟢 响应快，无积压 | 中 |
| **LobsterAI** | 6（均 stale） | 8（均合并/关闭） | 8 | 无 | 🟡 历史债务消化期，新功能放缓 | 中 |
| **CoPaw** | 63 条清理 | — | 无合并 | 无 | 🟡 稳定修复推进，无版本发布 | 中 |
| **PicoClaw** | 0 新开 | 2 合并 | 2 | 无 | 🟡 2 个 stale PR 需关注 | 低 |
| **NullClaw** | 0 | 1（待合并） | 0 | 无 | 🟡 平静期，响应偏慢 | 低 |
| **TinyClaw** | 无活动 | 无活动 | 0 | 无 | ⚪ 沉寂 | 无 |
| **ZeptoClaw** | 无活动 | 无活动 | 0 | 无 | ⚪ 沉寂 | 无 |


## 3. OpenClaw 在生态中的定位

### 优势

- **社区规模断层领先**：500 条 Issue + 500 条 PR 的日更新量，是第二梯队（ZeroClaw 92 条、Hermes 100 条）的 5-10 倍，已形成自我强化的社区飞轮。
- **维护团队响应机制成熟**：93 条 PR 日合并量 + 维护者（steipete 等人）24 小时内完成 7 条合并，远超 Hermes（8 条合并但多为机器人）和 ZeroClaw（2 条）。
- **安全与可靠性双线推进**：安装策略确认机制（#116489/#120900）和消息投递可靠性（#126205）是当前最高优先级，显示出对生产环境的认真态度。

### 技术路线差异

| 对比维度 | OpenClaw | Hermes Agent | IronClaw | ZeroClaw |
|---------|----------|---------------|----------|----------|
| **架构哲学** | 单体 + 部署器（node 节点模式） | 多运行时（Desktop/CLI/Webhook） | 模块化 + 沙箱优先 | 轻量核心 + 外部集成 |
| **沙箱/隔离** | 容器化部署 + Doctor 验证 | 进程级隔离（Windows 存在风险） | **持久化沙箱 + Docker Exec（~40ms）** | 未提及 |
| **安全加固** | 安装策略确认、OAuth 恢复 | 更新机制脆弱（update 破坏安装） | CI 全面限界、漏洞修复 | 安全加固（webhook 认证、凭据日志） |
| **平台支持** | 跨平台 + Doctor 诊断 | Windows 稳定性短板 | CI 稳定，测试完善 | Windows CI 缺口（74 测试失败） |
| **扩展方式** | Skill + 插件 | 提交 "salvage" PR 清理积压 | storybook + 设计系统 | WASM 插件架构（RFC） |

### 社区规模对比

| 项目 | 日 Issue 量 | 日 PR 量 | 合并率 | 长期积压（P1+ 超 3 个月） |
|------|-----------|---------|--------|--------------------------|
| **OpenClaw** | 500 | 500 | 18.6% | 5 个（#44925、#62505、#38327、#70903、#40001） |
| **Hermes** | 50 | 50 | 16% | 多个（#89614、#83529、#66616） |
| **ZeroClaw** | 42 | 50 | 4% | 多个（#9290、#7462、#9487） |
| **IronClaw** | 14 | 38 | ~50%+ | 无（新 Issue 快速对接） |
| **NanoClaw** | 3 | 34 | 73.5% | 无 |

**判断**：OpenClaw 在社区规模和响应速度上确立了明显领先地位，但**长期积压的 P1 bug（5 个）**说明其规模化后的问题消化能力尚未跟上增长速度。IronClaw 和 NanoClaw 的合并效率（50%+）反而值得 OpenClaw 借鉴。


## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---------|---------|---------|
| **会话/状态持久化** | OpenClaw（#44925、#62505）、NanoBot（#5271、#5403）、ZeroClaw（#9487/#9600）、CoPaw（#2723） | Subagent 结果丢失、会话数据被覆盖、统一会话所有权归属——"静默失败"成为跨项目的头号痛点 |
| **沙箱/容器优化** | IronClaw（#7732）、CoPaw（#6847 杀软误报）、ZeroClaw（隐含） | 容器创建耗时从秒级降至毫秒级（IronClaw #7741），杀毒软件误拦截需修复 |
| **跨平台一致性** | OpenClaw（#108435 Gateway 启动）、Hermes（#89614 Windows 蓝屏、#90134 构建失败）、ZeroClaw（#7462 Windows 测试失败、#9290 安装器）、NanoBot（#5444 Docker OAuth） | Windows 平台体验碎片化严重，macOS/Linux 作为默认开发环境导致 Windows 用户长期承压 |
| **安全加固** | OpenClaw（#116489/#120900 安装策略确认）、Moltis（#1216 vault 暴力破解 CWE-306）、ZeroClaw（#9976 凭据日志泄露）、NanoBot（#5444 OAuth 凭据管理） | 认证绕过、凭据泄露、暴力破解是普遍安全短板 |
| **模型调用可靠性** | OpenClaw（#38327 google-vertex 回归、#88657 DeepSeek 不完整输出）、CoPaw（#6515 新 provider）、NanoBot（#2493 LANGSMITH 回归）、ZeroClaw（#9447 不完整响应分类） | 模型 provider 适配层不稳定，新版本引入回归是普遍问题 |
| **记忆/上下文管理** | OpenClaw（#40001 write 工具追加模式、#60572 多槽位记忆）、NanoBot（#5441 记忆游标阻塞、#5403 token 估算）、CoPaw（#6624 记忆压缩不触发）、ZeroClaw（#9745 知识图谱隔离） | 记忆系统的稳定性和安全性正在成为核心竞争力 |


## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构 | 差异化标签 |
|------|---------|---------|---------|-----------|
| **OpenClaw** | 全功能个人 AI 助手（多通道、技能、自动化） | 个人开发者、重度用户 | 单体 + 部署器 + Skill 生态 | **生态之王**，功能最全、社区最大 |
| **IronClaw** | 编码智能体 + 沙箱优先 | 开发者、企业级工作流 | 持久化沙箱 + 统一编码工具契约 | **沙箱与 CI/CD 最佳实践**，发布节奏稳健 |
| **NanoClaw** | 多通道安装工具 | 快速部署者、非技术用户 | Bash 安装脚本 + 通道适配器 | **最低上手门槛**，安装即用 |
| **NanoBot** | 轻量 AI 助手（TUI/WebUI） | 轻量用户、个人使用 | 模块化、TUI 优先 | **极简主义**，关注记忆优化 |
| **Hermes Agent** | 多运行时（Desktop/CLI） | 桌面用户、Windows 用户 | 多前端 + Webhook 集成 | **Desktop 体验**，但 Windows 稳定性待加强 |
| **Moltis** | 容器化部署 + WhatsApp 集成 | 自托管用户 | 多后端容器（Apple Container 等） | **容器适配深度**，安全加固响应快 |
| **ZeroClaw** | 运行时 + SOP 引擎 + WASM | 高级开发者、企业 | 轻量核心 + 外部集成 + Rust | **架构先进性**，WASM 插件路线 |
| **CoPaw** | 编码智能体（Python 优先） | Python 开发者、国内用户 | 本地模型支持（RTX 3080 流畅跑 4B） | **本地模型友好**，但文件操作安全隐患 |
| **LobsterAI** | 企业级管理（IM 斜杠命令） | 企业/团队用户 | 全渠道接入 + 权限审批 | **IM 集成优先**，但沟通效率低下 |
| **PicoClaw** | 轻量单二进制 | 嵌入式/极简用户 | 单二进制分发 | 活跃度低，需关注 |
| **NullClaw / TinyClaw / ZeptoClaw** | — | — | — | **休眠状态** |


## 6. 社区热度与成熟度分层

### 第一层：快速迭代期（高活跃度、功能扩展快）

| 项目 | 特征 | 风险 |
|------|------|------|
| **OpenClaw** | 日均 1000 条事件，93 条 PR 合并，多个功能线并行 | P1 bug 积压持续 5 个月，用户耐心消耗 |
| **IronClaw** | v1.3.0 稳定发布，三大史诗级功能推进中 | 社区规模较小，新贡献者 PR 等待长 |
| **NanoClaw** | 合并率 73.5%，多条功能线同日完成合并 | 长期无版本发布，功能合入但用户无法使用 |

### 第二层：质量巩固期（活跃度中高、转向稳定性）

| 项目 | 特征 | 风险 |
|------|------|------|
| **ZeroClaw** | 规模大但合并率仅 4%，评审积压 | RFC 决策拖延可能导致 v0.9.0 延期 |
| **Hermes Agent** | 社区自主 "salvage" PR 补充核心维护者不足 | "更新即毁"问题削弱信任 |
| **NanoBot** | 响应迅速，但 16 条待合并 PR 堆积 | conflict 标记的 P1 修复长时间无进展 |
| **Moltis** | 无积压，安全修复快 | 需关注长期功能规划 |

### 第三层：平台期（活跃度低、等待新版本或方向决策）

| 项目 | 特征 |
|------|------|
| **LobsterAI** | 集中清理历史 PR/Issue，新功能停止，4 个月以上积压未闭环 |
| **CoPaw** | 稳定性修复推进中，但无版本发布，用户安全性担忧 |
| **PicoClaw** | 今日 2 PR 关闭，2 个 stale PR 待维护者响应 |

### 第四层：沉寂期

| 项目 | 特征 |
|------|------|
| **NullClaw / TinyClaw / ZeptoClaw** | 无代码合并、无版本发布，社区活跃度极低（NullClaw 仅 1 条文档修复 PR 待合并） |


## 7. 值得关注的趋势信号

### 趋势 1：沙箱从"隔离"走向"高性能复用"

**信号**：IronClaw 将容器创建耗时从 1-2.5s 降至 ~40ms（#7741），从"逐命令创建/销毁"演进为"per-user 持久化"（#7732）。

**参考价值**：对于所有依赖容器化隔离的项目，**容器复用 + 持久化工作区**是下一阶段提升开发体验的关键突破口。OpenClaw 的 Doctor 和部署器也可以借鉴这一模式。

### 趋势 2：会话状态管理成为核心架构争议

**信号**：OpenClaw（#44925 "Subagent 结果静默丢失" 持续 5 个月）、ZeroClaw（RFC #9487 "会话所有权归属运行时还是传输层"）、NanoBot（#5271 "会话数据被后台任务覆盖"）三大项目同时聚焦会话状态。

**参考价值**：会话持久化的**失败可见性**（失败时用户需要知道）和**所有权边界**（谁拥有、谁可写）是两个待解决的根本问题。率先建立可靠会话契约的项目将获得结构性优势。

### 趋势 3：工具调用权限精细化管理成为安全标配

**信号**：OpenClaw（#116489/#120900 安装策略确认）、CoPaw（权限审批弹窗语法高亮）、Moltis（vault 认证 CWE-306 修复）同步强调工具调用/安全边界的用户可见性。

**参考价值**：**"有界授权"（bounded permission）+ "明确确认"（explicit acknowledgment）**正在成为智能体框架安全设计的最低标准。新项目应从一开始就内置这一模式。

### 趋势 4：Windows 平台成为信任分水岭

**信号**：Hermes（蓝屏 #89614）、ZeroClaw（74 个测试失败 #7462）、OpenClaw（Gateway 启动回归 #108435）、NanoBot（Docker OAuth #5444）四线同时暴露 Windows 兼容性缺陷。

**参考价值**：多数项目 CI 仅覆盖 Linux，Windows 用户实际上在"裸奔"。**将 Windows CI 纳入测试矩阵** + **对 Windows 特有 API 做隔离处理**应成为所有项目的必修课。

### 趋势 5：社区从"提 Bug"转向"主动治理"

**信号**：Hermes 的 meta-issue（#84834 Webhook Feature Package）、ZeroClaw 的 anti-slop 清理 tracker（#10118，307 个候选修复）、IronClaw 的 /cleanup 制度——社区贡献者开始系统化组织跨切片的修复/治理计划。

**参考价值**：当项目规模达到一定程度后，**社区驱动的治理框架（meta-issue、tracker、salvage PR）** 将成为维持项目健康的关键基础设施。

### 趋势 6：本地模型 + 个人硬件成为差异化场景

**信号**：CoPaw 用户反馈 4B 模型在 RTX 3080 上流畅运行；OpenClaw 支持 Ollama/自定义 provider；NanoBot 优化本地上下文压缩 token 消耗。

**参考价值**：**本地优先（local-first）** 正在从极客偏好演变为隐私敏感用户的真实需求。支持 local model + 私有化部署可能是下一波用户增长点。

---

*报告生成时间：2026-08-20 | 数据来源：各项目 GitHub 仓库公开 Issue/PR 数据*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-20

## 1. 今日速览

NanoBot 项目近 24 小时保持高活跃度：共收到 5 条新 Issue（全部处于开放状态）、24 条 PR 动态（待合并 16 条、已合并/关闭 8 条），无新版本发布。社区反馈集中于 **OpenAI Codex OAuth 在 Docker 环境下的认证失败**（Issue #5444）及 **LANGSMITH 集成回归**（Issue #2493）两大问题，均有对应修复 PR 在途。此外，**Dream 记忆游标异常阻塞**（Issue #5441）和 **socks:// 代理兼容性**（Issue #5425）两条 Bug 也获得了针对性修复方案。项目整体响应速度较快，多数新报告 Issue 在 24 小时内即有 PR 对接，项目健康度良好，但待合并 PR 积累较多（16 条），需关注合并节奏。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

近 24 小时共 8 条 PR 被合并或关闭，展示了多个关键领域的推进：

| PR | 标题 | 类型 | 状态 | 要点 |
|---|---|---|---|---|
| [#5443](https://github.com/HKUDS/nanobot/pull/5443) | fix(tui): expose /exit in command menu | Bug修复 | 已关闭 | TUI 界面 `/exit` 命令加入斜杠命令菜单，完善 CLI 用户体验 |
| [#5440](https://github.com/HKUDS/nanobot/pull/5440) | perf(memory): reuse conversation prefix for local compaction | 性能优化 | 已关闭 | 本地压缩复用模型上下文前缀，降低记忆压缩对 token 的重复消耗 |
| [#5438](https://github.com/HKUDS/nanobot/pull/5438) | fix(webui): return promptly after Ctrl-C | Bug修复 | 已关闭 | WebUI 在 Ctrl-C 后的退出延迟问题修复，提升交互响应 |
| [#5341](https://github.com/HKUDS/nanobot/pull/5341) | fix(skills): make weather workflow Windows-safe | 兼容性 | 已关闭 | 天气技能工作流替换裸 `curl`，修复 Windows PowerShell 下 `Invoke-WebRequest` 别名问题 |
| [#4527](https://github.com/HKUDS/nanobot/pull/4527) | Add ask_clarification tool | 新功能 | 已关闭 | 新增内置 `ask_clarification` 工具，支持智能体主动向用户提问澄清 |
| [#4282](https://github.com/HKUDS/nanobot/pull/4282) | feat: add file management features to settings view | 新功能 | 已关闭 | 设置视图新增文件浏览与管理功能，用户可直接在界面查看/修改 Agent 生成的文件 |

**核心进展总结**：`ask_clarification` 工具的合入意味着智能体在遇到歧义时不再盲目猜测，而是可以直接询问用户，这对**多轮对话体验和任务完成准确率**是重要提升。同时，`perf(memory)` 的优化对**长会话场景下的 token 消耗**有明显帮助。

## 4. 社区热点

| 条目 | 类型 | 链接 | 热度与诉求 |
|---|---|---|---|
| **#2493 LANGSMITH is not working (anymore) after latest update** | Issue | [链接](https://github.com/HKUDS/nanobot/issues/2493) | **7 条评论**，1 👍。这是跨度最长（2026-03-25 创建）且近 24 小时仍在更新的 Issue。核心矛盾点在移除了 `litellm_provider.py` 后，langchain.com 的集成被破坏。用户明确表示"Any ideas how to fix this?"，期待官方给出替代方案 |
| **#5446 fix(cli): route OpenAI Codex OAuth storage through nanobot's data dir** | PR | [链接](https://github.com/HKUDS/nanobot/pull/5446) | **与 #5444 Bug 直接关联**，修复 Docker 下 OAuth 凭据因写入非托管目录导致 `PermissionError` 的问题。社区对 Docker 场景下的认证稳定性诉求强烈 |
| **#5441 Dream: a single recovered tool error permanently blocks the memory cursor** | Issue | [链接](https://github.com/HKUDS/nanobot/pull/5441) | 描述了一个典型的"**单点故障放大为系统性阻塞**"问题：一次工具错误被模型恢复后，整个 Dream 运行仍被判定失败，导致记忆游标不推进，后续每次运行重复处理同一批次，造成编辑重复。**对应修复 PR #5442 已提交**，社区反应积极 |
| **#5425 Support legacy socks:// proxy URLs** | Issue | [链接](https://github.com/HKUDS/nanobot/issues/5425) | 自定义 OpenAI-compatible 提供商在使用 `socks://` 别名时代理解析失败。**与 PR #5439 直接对应**，但 #5439 明确拒绝了 `socks://` 的兼容（仅支持标准 `socks5://`），该 Issue 是否会被采纳为 roadmap 需要关注 |

## 5. Bug 与稳定性

| 严重程度 | Issue / PR | 描述 | 状态 |
|---|---|---|---|
| **P1 高** | [#5444](https://github.com/HKUDS/nanobot/issues/5444) — Failed to login OpenAI via OAuth in Docker | Docker 环境下 OpenAI OAuth 登录失败，授权码交换 token 阶段报错 | **已有 PR #5446 和 #5445**，分别从 CLI 层和 Docker 层双管齐下修复 |
| **P1 高** | [#5403](https://github.com/HKUDS/nanobot/pull/5403) — fix(memory): use API-reported prompt tokens to trigger consolidation | 本地 tiktoken 估算低估 30-50%，导致上下文超限也不触发合并 | **PR 待合并**，修复已提交但未合入 |
| **P1 高** | [#5271](https://github.com/HKUDS/nanobot/pull/5271) — fix(session): prevent stale background task saves from overwriting session data | `/new` 或生命周期替换后，过期后台任务保存可能覆盖新会话数据 | **PR 待合并**，标记为 conflict，需要手动解决冲突 |
| **P2 中** | [#5441](https://github.com/HKUDS/nanobot/issues/5441) — Dream cursor permanently blocked by recovered tool error | 单次可恢复的工具错误导致整个 Dream 运行判定失败，游标永久阻塞，重复处理同一批次 | **已有 PR #5442** |
| **P2 中** | [#5425](https://github.com/HKUDS/nanobot/issues/5425) — socks:// proxy URLs not supported | `socks://` 别名无法被自定义 OpenAI-compatible provider 解析 | **PR #5439 仅支持 `socks5://`，拒绝 `socks://`**，需要维护者决策 |
| **P2 中** | [#2493](https://github.com/HKUDS/nanobot/issues/2493) — LANGSMITH integration regression | 移除 `litellm_provider.py` 后 langchain.com 集成失效 | **无对应 PR**，开放超过 5 个月，期望官方给出替代方案 |

## 6. 功能请求与路线图信号

| 功能请求 | 来源 | 对应 PR | 纳入下一版本可能性 |
|---|---|---|---|
| **ask_clarification 工具** | [#4527](https://github.com/HKUDS/nanobot/pull/4527) | 已合并 | ✅ 已进入主分支 |
| **Settings 页文件管理** | [#4282](https://github.com/HKUDS/nanobot/pull/4282) | 已合并 | ✅ 已进入主分支 |
| **支持手动专属调用技能（disable-model-invocation）** | [#5405](https://github.com/HKUDS/nanobot/pull/5405) | 待合并，有冲突 | ⏳ 高（对应部署/发布等副作用操作的使用场景） |
| **WebUI 会话后跟进建议** | [#5408](https://github.com/HKUDS/nanobot/pull/5408) | 待合并 | ⏳ 中高（对齐 DeerFlow 交互模式） |
| **nano_timer 核心工具** | [#4853](https://github.com/HKUDS/nanobot/pull/4853) | 待合并，有冲突 | ⏳ 中（依赖时间感知的智能体场景） |
| **基于 x402 的付费 MCP 安全扫描集成** | [#5447](https://github.com/HKUDS/nanobot/issues/5447) | 无 | ❌ 低（需治理评估，商业化服务接入需谨慎） |

## 7. 用户反馈摘要

- **Docker 环境痛点集中**（Issue #5444、PR #5445、#5446）：多个用户报告 OAuth 凭据无法在容器内持久化或写入非托管目录导致权限错误。用户期待容器场景下"开箱即用"体验，目前通过 XDG 数据目录重定向缓解，但需要文档明确持久化方案。
- **记忆系统稳定性关注度上升**（Issue #5441、PR #5442、#5403）：Dream 记忆游标阻塞导致重复处理的问题，以及 token 估算不准导致的合并延迟，直接影响了需要长期运行场景的用户体验。修复方案（使用 API 报告的 token 计数触发合并、恢复游标推进条件）已提交，用户关注度较高。
- **LANGSMITH 集成回归引发"供应链焦虑"**（Issue #2493）：有用户明确表示"迁移到 langchain.com 是因为更好的生态"，当前回归让部分用户对 NanoBot 的集成稳定性产生疑虑。建议维护者评估替代方案。
- **对 PR 合并速度的不满信号**：多条标记为 `conflict` 的 PR 已停留约 1-2 周（如 #5271、#5403、#4853），涉及 P0/P1 级别 bug 修复，用户可能感受到"修复已提交但迟迟不生效"的落差。

## 8. 待处理积压

| 类型 | 条目 | 链接 | 滞留时间 | 风险 |
|---|---|---|---|---|
| **P1 Bug 修复（有冲突）** | [#5271](https://github.com/HKUDS/nanobot/pull/5271) — Stale background task overwrites session | PR | 14 天 | 会话数据静默丢失风险持续存在，建议尽快解决冲突 |
| **P1 Bug 修复（有冲突）** | [#5403](https://github.com/HKUDS/nanobot/pull/5403) — API-reported token count for consolidation | PR | 4 天 | 长对话用户面临上下文超限后合并失效的问题 |
| **P1 功能（有冲突）** | [#4853](https://github.com/HKUDS/nanobot/pull/4853) — nano_timer core tool | PR | 43 天 | 时间感知能力缺失，且冲突已影响合并评估，建议维护者尽快裁决 |
| **P0 Bug 修复（有冲突）** | [#5271](https://github.com/HKUDS/nanobot/pull/5271) — 已注明，更高优先级 | PR | 14 天 | 同上 |
| **开放 Issue（2026-03-25 起）** | [#2493](https://github.com/HKUDS/nanobot/issues/2493) — LANGSMITH regression | Issue | ~5 个月 | 无修复 PR，集成用户流失风险 |
| **开放 Issue（2026-08-19 起，待维护者回应）** | [#5447](https://github.com/HKUDS/nanobot/issues/5447) — Paid security-scan MCP integration (x402) | Issue | 1 天 | 商业化服务接入需明确立场，避免社区期望错位 |

---

**报告生成时间**: 2026-08-20 | **数据来源**: HKUDS/nanobot GitHub 仓库

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-20

## 1. 今日速览

Hermes Agent 在过去 24 小时保持中等偏高的活跃度：50 条 Issue 更新（82% 为新增或活跃）、50 条 PR 更新（84% 待合并），但值得注意的是**零新版本发布**，且超过 40 个 PR 仍处于待合并状态，积压明显。当日最突出的风险信号来自 Windows 平台：一条 **P0 级崩溃报告**（#89614）称 Hermes 通过 stale PID 误杀 `svchost.exe` 导致系统蓝屏，与多条 Windows 相关的安装/更新/构建问题叠加，表明该平台的稳定性仍是当前最紧迫的短板。与此同时，社区出现了大量由不同作者提交的 "salvage" PR（捡拾修复），如修复 `/whoami` 命令失效（#90381）、修复技能加载时自我冲突的警告刷屏（#90387）等，显示出核心维护者资源分散、社区贡献者主动补充修复的积极分工模式。项目整体处于**功能扩展与稳定性修补并进、但发布节奏偏慢**的阶段。

## 2. 版本发布

过去 24 小时内无新版本发布。

## 3. 项目进展

今日**合并/关闭的 PR 共 8 条**，其中值得注意的包括：

- **[PR #90382 — feat(agent): emit bounded activation receipts](https://github.com/NousResearch/hermes-agent/pull/90382)（已关闭）**：为 agent 激活事件引入有界收据机制，但该 PR 由 Amp-Thread-ID 标注，且合并状态为 closed 而非 merged，疑似因格式问题被关闭，未实际落地。
- **[PR #90384 — fmt(js): `npm run fix` auto-fix](https://github.com/NousResearch/hermes-agent/pull/90384)（已关闭）**：机器人自动提交的代码格式化修复，已自动合并。

**真正推进项目实质进展的主要力量来自今日新提交的 PR 队列**，它们虽然尚未合并，但很大程度上代表了项目修复和功能的方向：

- **[PR #90389 — fix(cli): `hermes -z` 不再静默丢弃 `-s/--skills`](https://github.com/NousResearch/hermes-agent/pull/90389)**：修复 oneshot 模式下技能参数无法加载的回归问题。
- **[PR #90387 — fix(skills): 消除启动时 69 条自我冲突警告](https://github.com/NousResearch/hermes-agent/pull/90387)（salvage #74960）**：修复技能扫描时的自我碰撞误报，并让技能命令映射原子发布。
- **[PR #90381 — fix(cli): `/whoami` 在经典 CLI 中不再报 Unknown command](https://github.com/NousResearch/hermes-agent/pull/90381)（salvage #26047）**。
- **[PR #90370 — fix(desktop): 删除已归档会话不再留下"幽灵行"](https://github.com/NousResearch/hermes-agent/pull/90370)**：修复归档会话删除后残留 UI 异常。

此外，多条大型功能 PR 仍在积压中等待审查，包括 **Zulip 平台集成（#3335）**、**Claude Agent SDK 作为一等运行时（#65982）**、**Desktop 管理的 Computer Use 桥接（#61507）** 和 **通用 voice_server 网关平台（#27040）**——它们的持续积压表明核心维护者的审查带宽已成为项目发展的主要瓶颈。

## 4. 社区热点

### 最热 Issue 🔥

- **[#66616 — Skills index is stale or degraded (degraded)](https://github.com/NousResearch/hermes-agent/issues/66616)（60 条评论）**
  自动巡检发现 Skills 索引已过时 29.8 小时（上限 26 小时）。虽然这是一个自动化探针报告的问题，但获得了**60 条评论**的高热度，说明社区对文档与技能索引的可用性有较高关注度。此问题已持续超过一个月（7/18 创建），仍未被关闭，是项目"健康度"的重要负面信号。

- **[#84834 — Webhook Feature Package — graph-gated repair (meta-issue)](https://github.com/NousResearch/hermes-agent/issues/84834)（19 条评论）**
  由社区核心贡献者 `andrexibiza` 发起的一项系统性、跨 Webhook 表面的修复/治理计划，覆盖 5×2×3=30 个组合维度，包括入口、执行、投递、配置、管理 UI、部署与文档。此类 meta-issue 已形成社区推动项目治理的一种固定模式。

- **[#89564 — Discord Feature Parity & Alignment Campaign (API v10) (meta-issue)](https://github.com/NousResearch/hermes-agent/issues/79564)（8 条评论）**
  针对 Discord API v10 对齐的系统性计划，与今日新增的 **[PR #90383 — Discord 智能多路复用大厅路由](https://github.com/NousResearch/hermes-agent/pull/90383)** 形成呼应，表明社区正在按计划推进 Discord 能力的完整覆盖。

**热点诉求分析**：社区的核心诉求集中在两方面——（1）对项目管理透明度和治理节奏的期待，体现在 meta-issue 的兴起；（2）对既有功能缺陷（Windows、会话状态、配置解析等）快速修复的迫切需求，体现在多条带 `P1/P2` 级别的 bug 报告与即时提交的 fix PR 并存。

## 5. Bug 与稳定性

### 🔴 P0 / 严重

- **[#89614 — [Windows] Hermes 通过 stale-PID `taskkill /F /PID` 误杀 `svchost.exe` → 反复 0xEF 蓝屏](https://github.com/NousResearch/hermes-agent/issues/89614)（P1 标记，实为系统级崩溃）**
  Windows 11 上 Hermes Desktop 在进程清理时因 PID 已被系统复用而误杀 `svchost.exe`，导致 **CRITICAL_PROCESS_DIED 蓝屏循环**。这是极高严重度的安全问题（可导致系统无法启动），目前无关联 fix PR。**建议维护者立即响应。**

### 🟠 P1 / 高

- **[#83529 — `hermes update` 直接破坏安装](https://github.com/NousResearch/hermes-agent/issues/83529)（6 条评论）**
  用户在 Debian Trixie 上执行 `hermes update` 后安装彻底损坏。无关联 fix PR。该问题已存在 10 天（8/10 创建），仍未解决。

### 🟡 P2 / 中

- **[#90299 — 误报 "TERMINAL_CWD found in .env" 弃用警告（每次启动都出现）](https://github.com/NousResearch/hermes-agent/issues/90299)** — `.env` 未设置该变量仍报错，属逻辑判断缺陷。
- **[#90159 — `hermes update` 将 `mcp` 升级到 2.0.0，绕过 1.28.1 锁版，静默禁用所有 HTTP/SSE MCP 服务器](https://github.com/NousResearch/hermes-agent/issues/90159)** — 依赖管理存在严重缺陷。
- **[#84064 — `hermes config set/unset` 无法处理含字面量点号的 provider key](https://github.com/NousResearch/hermes-agent/issues/84064)（更新于今日）** — 路径解析无转义机制。
- **[#90134 — Windows 上 `hermes desktop` 构建失败（blockmap.js）](https://github.com/NousResearch/hermes-agent/issues/90134)** — 已有 [PR #90046](https://github.com/NousResearch/hermes-agent/pull/90046) 部分关联修复（进程扫描编码问题），但构建失败本身仍未直接解决。

### 🔵 已关闭 / 有修复

- **[#89897 — Codex 工具后续请求向 gpt-5.6-sol 发送不支持的 prompt_cache_retention（P0，已关闭）](https://github.com/NousResearch/hermes-agent/issues/89897)** — 今日已关闭，修复速度值得肯定。
- **[#70058 — GLM API 拒绝 "ultra" reasoning_effort（已关闭）](https://github.com/NousResearch/hermes-agent/issues/70058)** — 与 #74295 同期关闭，相关 reasoning_effort 系列问题正在收尾。
- **[#89503 — Cron 任务 per-job 模型覆盖对非 Anthropic provider 失效（已关闭）](https://github.com/NousResearch/hermes-agent/issues/89503)**

## 6. 功能请求与路线图信号

### 可能纳入下一版本的功能

- **[PR #90313 — 新装即用的无密钥 Web 搜索（Parallel + Exa 免费层）](https://github.com/NousResearch/hermes-agent/pull/90313)** — 零配置即可使用 `web_search` / `web_extract`，对齐 opencode 的默认搜索路径。若被采纳，将显著降低新用户上手门槛。
- **[PR #90385 — Webhook 会话完成后移交消息平台（Discord）](https://github.com/NousResearch/hermes-agent/pull/90385)** — 配合 #84834 Webhook Feature Package 的系统性修复计划。
- **[PR #90383 — Discord 智能多路复用大厅路由](https://github.com/NousResearch/hermes-agent/pull/90383)** — 与 #79564 Discord 对齐战役互为助力。
- **[Issue #89995 — 将 Bot Mode 群聊房间暴露到 Web 仪表盘与网关](https://github.com/NousResearch/hermes-agent/issues/89995)** — 当前群聊仅限 Desktop，用户生态正在向"远程优先"方向推进此能力。
- **[PR #90380 — Computer Use 可插拔后端提供者（容器/沙箱/远程桌面）](https://github.com/NousResearch/hermes-agent/pull/90380)** — 解耦 Computer Use 运行时的关键架构分拆，为 #61507 扫清障碍。
- **[PR #90388 — `hermes sessions unhide` 子命令与 `--include-hidden` 列表选项](https://github.com/NousResearch/hermes-agent/pull/90388)** — 为 `hidden` 会话标志提供恢复和管理手段，配 #89901 的修复。

### 值得关注的架构演进信号

- **[Issue #90144 — "Proof scope must equal mutation scope"](https://github.com/NousResearch/hermes-agent/issues/90144)** — 系统性归纳了多类"狭义证明授权广义变更"的缺陷，可能是未来防御性重构的纲领性文档。

## 7. 用户反馈摘要

- **更新即毁灭的恐惧**：`hermes update - destroys hermes`（#83529）和 `hermes update 覆盖 mcp 锁版`（#90159）这类问题严重削弱了用户对更新机制的基本信任，这在开源工具的日常使用中影响很大，属于 P1 级体验问题。
- **Windows 用户的挫败感持续累积**：从蓝屏（#89614）、文件树卡死（#90229）、构建失败（#90134）到安装恢复死循环（#79539），Windows 平台问题呈现"多点开花"的态势，用户正在应对一系列相互关联的稳定性问题。
- **"能量和创造力"被技能索引问题拖累**：#66616 的高评论数侧面反映社区对 `/docs/skills` 索引的依赖程度较高，持续 30 小时的延迟会直接影响用户的实际使用体验。
- **社区主动捡拾修复**：多条以 "salvage"（捡拾）命名的 PR（#90389、#90387、#90381、#90370）显示社区开发者正在代替核心维护者推进积压修复，但也意味着核心维护团队的响应速度已经难以跟上 issue 产生的节奏。

## 8. 待处理积压

以下条目需维护者重点关注：

- **[#66616 — Skills 索引持续陈旧（60 条评论，已开放 33 天）](https://github.com/NousResearch/hermes-agent/issues/66616)** — 自动化探针反复报告失败，可能是 CI/CD 管道配置存在系统性缺陷。
- **[#83529 — `hermes update` 破坏安装（开放 10 天，P1，无 fix PR）](https://github.com/NousResearch/hermes-agent/issues/83529)** — 这是一个直接影响核心功能链路的严重问题，应作为最优先修复项之一。
- **[#79564 — Discord Feature Parity & Alignment Campaign 元问题（开放 15 天）](https://github.com/NousResearch/hermes-agent/issues/79564)** 与 **[#84834 — Webhook Feature Package 元问题（开放 8 天）](https://github.com/NousResearch/hermes-agent/issues/84834)** — 两套系统性治理方案均需维护者给出评审意见。
- 待合并功能性 PR 中积压最久的包括：**Zulip 平台集成（#3335，已开放 147 天）**、**Claude Agent SDK 作为一等运行时（#65982，35 天）**、**Computer Use 桥接（#61507，42 天）**、**voice_server 网关平台（#27040，96 天）**——这些均是对项目生态有显著扩展价值的贡献，长时间的等待可能消磨贡献者的积极性。
- **[#79614 — Windows 进程误杀导致蓝屏（P1，无 fix PR）](https://github.com/NousResearch/hermes-agent/issues/89614)** — 该问题涉及系统级稳定性，建议维护者第一时间优先响应。

---

*本日报基于 2026-08-20 GitHub 数据自动生成，所有数据均来源于 [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) 仓库公开 Issue 与 PR。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期：2026-08-20** | **数据窗口：2026-08-19 00:00 - 2026-08-20 00:00 UTC**


## 1. 今日速览

PicoClaw 项目过去24小时整体活跃度**中等偏上**，核心动能为 PR 合并/关闭（2条）与关闭积压 Issue（1条）。当前有 **3 个 PR 处于开放状态**，其中 2 个已标记为 stale 超两周，需维护者关注。特别值得注意：**PR #3341（Telegram 交互命令 UX 改进）与 PR #3200（模型回退链）均于今日关闭**，但合并状态需确认——前者为功能增强，后者为搁置超 6 周的 PR 终局。并无新版本发布，也无新 Issue 开启，表明项目处于**功能收尾而非需求爆发期**。短期风险在于：2 个 stale PR（#3316、#3315）尚未获得维护者响应，可能成为社区不满的隐患。


## 2. 版本发布

**无新版本发布。**


## 3. 项目进展

今日关闭/合并了 2 个 PR，分别标志着**功能落地**与**长尾清理**：

| PR | 标题 | 状态 | 影响 |
|----|------|------|------|
| [#3341](https://github.com/sipeed/picoclaw/pull/3341) | feat(telegram): add interactive command UX and formatted ephemeral fallback | **CLOSED** | 为 Telegram 通道引入交互式命令 UX，简化 `/memory` 等子命令认知负担；优化 `/help` 输出冗长问题；为结构化内容提供格式化临时消息回退 |
| [#3200](https://github.com/sipeed/picoclaw/pull/3200) | feat(models): add configurable default fallback chain | **CLOSED** | 为 Web UI 模型页新增默认回退链配置（默认模型 + 后备模型 + 排序 + 持久化），经 6 周搁置后关闭 |

**解读**：PR #3341 的关闭是今日最实质的进展——Telegram 通道交互体验将显著改善，用户不再需要记忆复杂子命令语法。PR #3200 关闭时间较长（创建于 7/1），建议维护者确认是已合并还是放弃，若放弃需给出理由以安抚贡献者。


## 4. 社区热点

今日无高热度讨论（所有 Issues/PR 评论数 ≤ 4）。**唯一有实质讨论的 Issue #1305**（4 条评论）成为自然焦点：

- **[Issue #1305](https://github.com/sipeed/picoclaw/issues/1305)（已关闭）**：`new banner print to STDOUT, break completion flow`
  - **核心矛盾**：上游 PR #1008 引入的 banner 输出污染了 STDOUT，直接破坏了 `picoclaw completion zsh > _picoclaw` 等 shell 补全工作流——生成的文件头部被 banner 污染，导致补全失效。
  - **用户诉求**：CLI 工具必须严格区分标准输出与标准错误，banner 应输出到 STDERR 或受 `--quiet` 控制。该项目 Issue 于 **3 月创建、今日关闭**，修复周期约 5 个月，社区耐心已被消耗。

> 其他 PR（#3329、#3316、#3315）均无评论，无社区讨论热度。


## 5. Bug 与稳定性

今日共 1 条 Bug 相关更新，**已解决**：

| 严重程度 | Issue | 问题描述 | 状态 |
|---------|-------|---------|------|
| 🟡 中 | [#1305](https://github.com/sipeed/picoclaw/issues/1305) | banner 输出到 STDOUT 污染 shell 补全脚本 | ✅ 已关闭（2026-08-19） |

**稳定性观察**：今日无新 Bug 报告，无崩溃或回归问题。但需警惕 banner 问题的修复方式——建议维护者在 Release 说明中明确说明是否已将 banner 迁移至 STDERR，避免用户升级后行为变化产生困惑。


## 6. 功能请求与路线图信号

**无新功能请求**。但开放 PR 中蕴含明确的路线图信号：

| 信号 | PR | 方向 |
|------|-----|------|
| **Telegram 话题支持** | [#3315](https://github.com/sipeed/picoclaw/pull/3315) | 修复私人机器人聊天中的话题消息识别（`IsTopicMessage` 而非仅依赖 `Chat.IsForum`）——对启用话题模式的私聊场景是刚需 |
| **路由代理上下文管理** | [#3316](https://github.com/sipeed/picoclaw/pull/3316) | 修复路由代理不记忆历史、不触发自动压缩的严重逻辑缺陷——直接影响 Discord 频道路由场景下的多轮对话体验 |
| **LINE 配置校验** | [#3329](https://github.com/sipeed/picoclaw/pull/3329) | 对声明了但从未被读取的 `webhook_host` / `webhook_port` 配置项给出警告（而非静默播种）——消除配置误导 |

**预判**：热线图所示，**Telegram 话题支持 + 路由代理上下文管理** 如果被合并，将进入下一版本（v0.x）。但两者均已 stale（>14 天无更新），需维护者明确回应。


## 7. 用户反馈摘要

基于今日非活跃 Issue 的既有评论（#1305），提炼真实用户痛点：

- **痛点在 CLI 工具边界**：用户明确反馈“**补全脚本被污染**”，暴露出 shell 集成（zsh/bash/fish 补全）对 stdout 纯净性的强依赖。核心诉求：*一切非主输出内容（banner、日志）必须走 stderr*。[Issue #1305 评论](https://github.com/sipeed/picoclaw/issues/1305)
- **修复周期过长**：Issue 3 月提出、8 月修复，**5 个月延迟**对 CLI 工具用户极其不友好——期间用户可能已经放弃使用补全功能或被其他工具吸引。


## 8. 待处理积压

以下条目需维护者重点关注：

| 类型 | 编号 | 标题 | 创建日期 | 搁置天数 | 建议 |
|------|------|------|---------|---------|------|
| 🔴 PR | [#3316](https://github.com/sipeed/picoclaw/pull/3316) | fix: routed-agent context management not respecting history, summarization, compression, and seahorse bootstrap | 2026-08-03 | **17 天（stale）** | 核心 Context 管理修复，阻塞多轮路由对话体验。建议尽快 review 并测试 |
| 🔴 PR | [#3315](https://github.com/sipeed/picoclaw/pull/3315) | Support topics in private bot chats | 2026-08-03 | **17 天（stale）** | 影响 Telegram 私聊话题场景，实现清晰但需确认测试覆盖 |
| 🟡 Issue | [#1305](https://github.com/sipeed/picoclaw/issues/1305) 关联 | 确认修复是否已进入 release | 2026-03-10 | 已关闭但需验证 | 建议补充回归测试，防止 banner 问题复发 |
| 🟡 PR | [#3200](https://github.com/sipeed/picoclaw/pull/3200) | feat(models): add configurable default fallback chain | 2026-07-01 | 50 天后关闭 | 确认是否合并；若放弃请在贡献者沟通渠道说明原因 |

> **对维护者的提醒**：2 个 stale PR（#3316、#3315）已超 2 周未收到任何维护者评论。长距离搁置将导致贡献者流失风险，建议在 48 小时内至少给出**明确的时间承诺或 review 反馈**。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-08-20

## 1. 今日速览

过去 24 小时 NanoClaw 项目保持高度活跃：**34 条 PR 更新**（其中 25 条已合并/关闭），远超近期均值，合并节奏明显加快；**3 条新 Issue** 全部与安装/运行时稳定性相关，且均由同一用户 (glifocat) 提交，指向非交互式安装和 Node 新版本兼容两个真实痛点。值得注意的信号是：**Telegram 群组连接、Slack agents 分离、Cursor Agent SDK 接入**三条功能线在同一天内集中推进并完成合并，表明项目正处在多通道/多 Provider 能力扩张的密集交付期。当前无新版本发布，9 个 PR 仍在待合并队列中。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日共合并/关闭 25 个 PR，主要集中在以下几条功能线：

### 3.1 Slack 通道重构与 agents 特性拆分（#3357、#3358）
- **[#3357] setup: --slack-agents installs the whole Slack agents feature** — `bash nanoclaw.sh` 默认安装基础 Slack 体验（单 bot + DM/频道聊天），`--slack-agents` 标志则安装完整 agents 特性（子 bot、a2a 房间、canvas、DM onboarding）。
- **[#3358] slack: split the payload — base adapter in /add-slack, agents feature in /slack-agent-flow** — 与 #3357 配套，将 Slack 通道负载沿标志边界拆分，并将 agents 负载适配到 trunk 的异步中央数据库。

### 3.2 Telegram 群组连接流程（#3351、#3352）
- **[#3351] feat(telegram): add approved group connection picker** — 新增 `/connect_group` DM 命令，基于 Telegram 原生群组选择器，通过 NanoClaw 既有的审批通道流入群组连接流程，并以群组级欢迎/引导对话作为起点。
- **[#3352] docs(telegram): document approved group connection flow** — 配套文档，指导 `/add-telegram` 安装并验证群组连接行为测试。

### 3.3 Provisioning 与审批基础设施加固（#3339、#3340、#3341、#3344、#3345）
- **[#3339] fix(setup): fail closed when a stored sign-in cannot be verified** — 修复"未经验证的凭据被当作已通过"的漏洞（认证失败应关闭而非放行）。
- **[#3340] fix(approvals): record the delivering instance on pending_approvals** — 为 `pending_approvals` 增加 `instance` 列，确保 OneCLI 凭据卡片由拥有 DM 的同一 bot 身份发送/编辑。
- **[#3341] fix(provisioning): derive the Slack service from the credential's issuer** — 修复安装令牌由 account 服务签发、在 Slack 服务消费时未配对验证的问题。
- **[#3344] feat(provisioning): optional request-origin metadata on app creation** — 增加 4 个可选的来源元数据字段（请求者、创建工具、客户端等）。
- **[#3345] feat(setup): forward optional client metadata on Slack service requests** — 在 Slack 服务请求中透传 `client_version` 等可选元数据。

### 3.4 其他关键合并
- **[#3025] fix(container): raise the agent SDK's 32000 output-token cap** — 提升 agent SDK 的 32000 输出 token 上限（该 PR 自 7 月 12 日起挂起超一个月，今日终于合并）。

> **评估**：今日合并在"多通道能力扩展"和"基础设施加固"两个维度均有实质推进，尤其是 Slack 功能拆分和 Telegram 群组连接两项，均属用户可感知的功能增量。项目整体处于快速迭代期。

---

## 4. 社区热点

今日无单个 Issue/PR 出现大量评论互动（所有新增 Issue 评论数均为 0），但以下 PR 值得关注：

### 4.1 Dial 通道两条 PR 合并前的最后冲刺（#3041、#3050）
- **[#3041] feat(channels): add Dial channel adapter (SMS + AI voice calls)**（OPEN，7/14 创建）
- **[#3050] feat(setup): add Dial to the channel picker + wizard/skills**（OPEN，7/14 创建）

这两条 PR 自 7 月 14 日发起，已持续 37 天未合并，是当前开放时间最长的功能 PR。同一天提交的 **Issue #3353（Dial 短信送达状态误报）** 直接指向该通道适配器的一个逻辑缺陷，可能成为这两条 PR 最终合并前的最后阻塞项。

### 4.2 Cursor Agent SDK 集成（#3355、#3356）
- **[#3355] feat(setup): add /add-cursor agent provider skill**（OPEN）
- **[#3356] feat(providers): add Cursor Agent SDK payload**（OPEN）

同一位作者 (zvi-fried) 在同一天提交了 provider 负载和 setup skill 两条 PR，与另一条已合并的 **#3349 (agent mailbox seam and registry)** 构成完整的 Cursor Agent 接入方案。

> **分析**：Dial（SMS/AI 通话）和 Cursor（AI 编程助手 Provider）是当前社区贡献者最集中的两条新方向，反映出用户对"多通道触达"和"与主流 AI 编程工具打通"的需求正在上升。

---

## 5. Bug 与稳定性

### 5.1 严重度：高

**[#3359] Node 26 兼容性：better-sqlite3 11.10.0 无法编译**
- 作者: glifocat | [链接](https://github.com/nanocoai/nanoclaw/issues/3359)
- 现象：macOS arm64 + Homebrew Node 26.7.0 环境下，`bash nanoclaw.sh` 通过 Node 检查后在 bootstrap 阶段因 `deps_failed` 中止，better-sqlite3 编译失败。
- 根因：`check_node` 仅有下限检查（`[ "$major" -ge 20 ]`），未验证上限或已知不兼容的版本。
- **已有 fix PR：[#3360] support current Node runtimes**（OPEN）— 升级 better-sqlite3 至 13.0.3，并将 Node 最低版本提升至 22。

### 5.2 严重度：中

**[#3354] Setup 留下 0 字节通道文件 + onecli 检查在 PATH 修复前运行**
- 作者: glifocat | [链接](https://github.com/nanocoai/nanoclaw/issues/3354)
- 现象：非登录 SSH 会话（无交互 shell、`~/.local/bin` 不在 PATH）下安装时出现两个问题：`git show <ref>:<path> > <file>` 失败留下 0 字节文件；onecli 检查在自己的 PATH 修复逻辑之前执行。
- 根因：setup 假定交互式登录 shell 环境。
- **无对应 fix PR**，但 [#3249]（PR: Fix, core-team, 8/14 创建）可能部分覆盖此问题（处理已超出支持范围的 Node）。

### 5.3 严重度：中

**[#3353] Dial 通道：运营商拒绝后短信仍被记录为已送达**
- 作者: glifocat | [链接](https://github.com/nanocoai/nanoclaw/issues/3353)
- 现象：Dial 适配器在运营商接受发送时即记录为已送达；若运营商后续拒绝（如远端号码无效），`delivered` 行的 `status` 保持 `'delivered'`，重试预算不会被消耗，agent 和 owner 均不会被通知。
- 影响：用户可能永远不知道短信实际未送达。
- **无对应 fix PR**，需在 Dial 适配器中补充送达回执处理逻辑。

> **汇总**：3 个新 Bug 中有 1 个已有关联修复 PR（#3360），其余 2 个待讨论。当前无崩溃级回归报告。

---

## 6. 功能请求与路线图信号

### 6.1 明确信号：Node 运行时支持范围调整
- Issue #3359 + PR #3360 构成明确的信号：NanoClaw 需要更新 Node.js 版本策略（最低版本升至 22，同时支持最新的 Node 26）。此 PR 已在队列中，预期近期合并。

### 6.2 开发中的新功能

| 功能 | PR/Issue | 状态 | 信号强度 |
|------|----------|------|----------|
| Cursor Agent SDK 接入 | #3355、#3356 | OPEN（提交于 8/19） | 高 — 同一作者同天提交配套两条 PR |
| Agent mailbox seam + registry | #3349 | OPEN（8/19 提交） | 高 — 可能作为新 provider 接入的基础设施 |
| Dial 通道正式落地 | #3041、#3050 | OPEN（7/14 提交，已 37 天） | 高 — 社区持续关注，Issue #3353 暴露了落地前的最后缺陷 |
| Slack agents 特性 flag 化 | #3357、#3358 | ✅ 已合并 | 已完成 |

### 6.3 路线图推断
结合已合并的 PR (#3349、#3351、#3357、#3358) 和待合并的 PR (#3355、#3356、#3360、#3362)，下一版本大概率包含：**Node 22+ 支持、Cursor Agent Provider、代理邮箱注册表（mailbox registry）** 三项能力。

---

## 7. 用户反馈摘要

### 7.1 真实用户痛点

1. **Node 新版本兼容性延迟**（#3359）：用户在全新 macOS 机器上首次安装即失败。反馈显示 Homebrew 已默认安装 Node 26，而项目仅检查最低版本——这暴露了一个核心体验问题：**通过版本检查但实际无法安装**比直接提示"不支持"更令人困惑。

2. **非交互式安装场景考虑不足**（#3354）：用户明确标注了"non-login/headless install"，说明 CI/CD 或远程机器部署是真实使用场景。0 字节残留文件虽然不会导致崩溃，但会让后续排查成本升高。

3. **短信送达状态的准确性**（#3353）：用户（可能是 Dial 通道的早期采用者）希望获得真实的送达确认，而非"运营商接受即已送达"。对于需要短信通知关键事件（如审批、告警）的场景，误报送达可能导致严重后果。

### 7.2 满意点

- 所有 3 个 Issue 均在提交当天或次日获得响应，维护者响应速度良好。
- 修复 PR（如 #3360、#3249）与 Issue 的时间关联性强，用户能快速找到解决办法。
- Telegram 群组连接和 Slack agents 拆分的合并表明项目正在认真听取社区对多通道/多工作区场景的需求。

---

## 8. 待处理积压

### 8.1 长期挂起的重要 PR（>30 天）

| PR | 主题 | 挂起天数 | 阻塞原因推测 |
|----|------|----------|--------------|
| [#3041](https://github.com/nanocoai/nanoclaw/issues/3041) | Dial channel adapter (SMS + AI voice calls) | 37 天 | Issue #3353 暴露了送达状态逻辑缺陷，可能需要先修复再合并 |
| [#3050](https://github.com/nanocoai/nanoclaw/issues/3050) | Dial 加入 channel picker + wizard | 37 天 | 依赖 #3041 合并 |
| [#3025](https://github.com/nanocoai/nanoclaw/issues/3025) | 提升 agent SDK 输出 token 上限 | 39 天 | ⚠️ 今日已合并（8/19 更新），积压解除 |

### 8.2 建议关注

- **#3050 与 #3041**：这两条 Dial PR 与今日新提交的 Issue #3353 高度关联。建议维护者评估是否在合并前为 Dial 适配器补充送达状态回执逻辑，否则上线后可能随安装量增加产生更多误报反馈。
- **#3249 (fix(setup): handle existing Node outside supported range)**：与 #3359/#3354 相关，但该 PR 只处理 Node 版本范围外的情况，未覆盖非交互式 shell 的 PATH 问题。建议将 #3354 中提及的两个 bug 拆分为独立议题并分配所有者。

---

## 项目健康度评估

| 维度 | 状态 | 说明 |
|------|------|------|
| 活跃度 | 🟢 高 | 日均 30+ PR 更新，多条功能线同时推进 |
| 合并效率 | 🟢 高 | 25/34 的 PR 在当日完成合并，且包含多个核心特性 |
| 响应速度 | 🟢 良好 | 新 Issue 当天即有 PR 跟进（#3359 → #3360） |
| Bug 密度 | 🟡 中等 | 3 个新 Bug，1 个已有修复 PR，2 个待处理 |
| 长尾积压 | 🟡 需关注 | 2 条 PR 已挂起超 37 天（Dial 通道） |
| 版本管理 | 🟡 无发布 | 大量功能已合并但未发布，社区可能等待新版本 |

> **核心洞察**：NanoClaw 正在经历一轮"多通道扩展 + 基础设施加固"并行的活跃开发周期，但长时间未发布新版本（今日无 Release）可能让外部用户无法及时获得上述修复和功能。若维持当前合并速度，建议在 Dial 通道和 Node 22+ 支持合并后尽快打一个版本。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报

**日期：2026-08-20** | **数据来源：GitHub (github.com/nullclaw/nullclaw)**

---

## 1. 今日速览

过去 24 小时内，NullClaw 项目整体活跃度处于**低位**：无新增或关闭的 Issue，无新版本发布，仅有 1 条 PR 处于待合并状态。唯一值得关注的动作是社区成员 FaintFlower 提交的 PR #989，针对 README 星标历史图表因依赖受限的 GitHub API 而失效的问题，提出了切换到替代数据源（star-history.dera.page）的修复方案。该修复尚未被合并，表明维护者响应节奏偏缓。项目今日无代码合并、无功能进展，整体处于**平静等待期**。

---

## 2. 版本发布

今日无新版本发布（最新 Releases：无）。无更新内容、无破坏性变更、无迁移注意事项。

---

## 3. 项目进展

今日**无任何 PR 被合并或关闭**。唯一的待合并 PR 为：

- **[#989 [OPEN] fix: restore broken star history chart](https://github.com/nullclaw/nullclaw/pull/989)** — 作者: FaintFlower，创建于 2026-08-19，当前 0 评论、0 👍。

该 PR 修复 README 中因 GitHub stargazer API 访问受限而失效的星标历史图表，改用无需 Token 的 star-history.dera.page 作为数据源，并已验证图表 URL 可用性。**尽管修复范围较小（文档/展示层面），但它属于社区自发维护行为，若被合并将提升项目可读性和对外展示质量。** 项目核心代码今日无任何推进，进展停滞。

---

## 4. 社区热点

今日无高互动、高评论的 Issue 或 PR。唯一存在的 PR #989 评论数为 undefined（即无评论），👍 数为 0。**无热点话题、无激烈讨论**。社区整体处于安静状态，说明用户当前关注度不高，或多数问题已在前期解决。

---

## 5. Bug 与稳定性

今日无一新增 Bug 报告、崩溃或回归问题。唯一与稳定性相关的信息来自 PR #989 的摘要说明：

- **问题描述**：README 中的星标历史图表因依赖 GitHub stargazer API（存在访问限制）而无法正常渲染。
- **严重程度**：低（不影响代码功能，仅影响项目展示页）。
- **修复 PR**：已有 PR #989 待合并，若合并可彻底解决。

**结论：无严重稳定性威胁。**

---

## 6. 功能请求与路线图信号

今日无新功能请求。基于现有 PR #989，可以捕捉到一个**间接信号**：社区对项目对外展示（README 图表）的可用性有期待，且倾向于采用**无需认证、去中心化的替代方案**（如 star-history.dera.page）。这可能暗示用户对 GitHub API 依赖的敏感度在上升。**该改动一旦合并，可能为后续 README 中其他图表类组件引入更轻量的数据源策略提供参考。**

---

## 7. 用户反馈摘要

由于今日无 Issue 活动、无 PR 评论，**无法提炼用户痛点、使用场景或满意度反馈**。唯一可获取的“反馈”来自 PR #989 作者的描述，间接反映了用户在浏览项目 README 时对图表可用性的需求。建议维护者关注后续合并后的用户反馈，以评估该修复是否被接受。

---

## 8. 待处理积压

当前无长期未响应的 Issue 或 PR 被标记。但需注意：**PR #989 已创建 1 天，仍处于未合并状态，且无任何维护者评论**。若持续无响应，可能演变为积压项。建议维护者：

- 尽快审阅 PR #989 并给出合并/修改意见（原因为该项目唯一的开放 PR）。
- 关注是否存在其他早期未关闭的 Issue（当前数据未显示），避免历史遗留问题被忽视。

---

> **综合评估**：项目今日活跃度低（1 PR、0 Issue、0 Release），无核心代码进展，但社区有一个小规模文档修复贡献待处理。项目健康度**短期呈平稳偏冷**，维护者响应速度将是未来用户留存的观察点。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-20

> 数据窗口：2026-08-19 至 2026-08-20（基于 GitHub 活动数据）

---

## 1. 今日速览

IronClaw 于昨日晚间正式发布 **v1.3.0 稳定版**，标志着近两周 RC 验证周期的收官。项目活跃度处于高位：过去 24 小时内有 **38 条 PR 更新**（22 条待合并）和 **14 条 Issue 更新**（9 条活跃），核心贡献者 serrrfirat 与 henrypark133 在沙箱持久化、能力响应规范化、CI 稳定性三条战线上均有实质推进。值得关注的是，多个 PR 已形成清晰的 stack 依赖关系（如 #7752 → #7755、#7686 → #7692 → #7711），显示团队正按计划执行跨切片的功能落地。v1.3.0 的发布为 v1.4.0 的史诗级功能（持久化沙箱、OOBE 引导、设计系统）铺平了道路，项目整体处于**健康活跃上升期**。

---

## 2. 版本发布 — ironclaw-v1.3.0

- **发布时间**：2026-08-19
- **发布类型**：稳定版（由 1.3.0-rc.2 晋升，PR #7754）
- **Release Notes 要点**：
  - 继承了 RC2 中已验证的升级路径和容器修复
  - 修复了从 1.2 升级时 `activation_state` 字段导致的 crash-loop 问题——升级过程现在能正确接受并保留该扩展字段
- **破坏性变更**：无（明确标注 "no production behavior"）
- **迁移注意事项**：从 1.2 直接升级至 1.3.0 的用户将自动获得 `activation_state` 字段的兼容性修复，无需手动干预
- 🔗 [Release 页面](https://github.com/nearai/ironclaw/releases) | [晋升 PR #7754](https://github.com/nearai/ironclaw/pull/7754)

---

## 3. 项目进展

### 3.1 已合并/关闭的重要 PR

| PR | 标题 | 影响 |
|---|---|---|
| [#7754](https://github.com/nearai/ironclaw/pull/7754) | chore(release): promote 1.3.0-rc.2 to 1.3.0 | v1.3.0 稳定版发布 |
| [#7741](https://github.com/nearai/ironclaw/pull/7741) | feat(sandbox): per-thread persistent container with Docker Exec (#7732 Step 1) | 容器创建耗时从 1–2.5s 降至 ~40ms，解决多 SSO 用户场景下的逐命令 churn 问题 |
| [#7491](https://github.com/nearai/ironclaw/pull/7491) | feat(coding): omp core-tool contract + engines + benchmark arm | 统一编码工具面为 6 个裸名称（read/write/edit/glob/grep/bash），移除旧工具面和派生命名 |
| [#6994](https://github.com/nearai/ironclaw/pull/6994) | feat(webui): OOBE automation-tasks prototype | 首次运行引导原型落地（carousel、inline cards、agent-mode pill），全部功能由 off-by-default 标志控制 |
| [#7686](https://github.com/nearai/ironclaw/pull/7686) | refactor(runtime): centralize capability outcome processing | 能力结果处理收敛至单一 `capability_response_processor`，行为保持不变的架构重构 |
| [#7756](https://github.com/nearai/ironclaw/pull/7756) | fix(ci): bound every unbounded CI operation | 修复 merge queue 反复超时问题——所有 stall 均源于无界 `apt-get` 操作，已全面限界（69 次运行、1,193 个 job 普查） |

### 3.2 项目推进评估

v1.4.0 的三大史诗（#7732 持久化沙箱、#7044 渠道优先进驻、#7038 设计系统）均有实质进展。特别是**持久化沙箱**已从设计阶段进入实现：PR #7741 先按线程维度实现容器复用，随后 PR #7751 将其升级为按用户维度（~40ms 的 Docker Exec），并配套 Issue #7732 的 epic 跟踪。**能力响应规范化**栈（#7686 → #7692 → #7711）已完成第一层合并，第二、三层待审。CI 稳定性修复（#7756）直接解决了 merge queue 反复 dequeuing 的顽疾，预计将显著提升后续合入效率。

---

## 4. 社区热点

### 热点 1：Persistent per-user sandbox 史诗（#7732）
- **链接**：[Issue #7732](https://github.com/nearai/ironclaw/issues/7732)
- **讨论热度**：7 条评论
- **动态**：昨天还是 open 状态的 epic，今天已有两个 Step 1 PR（#7741 已合并、#7751 待审）。用户对持久化沙箱的诉求强烈——当前实现每个 shell 命令都创建/销毁容器，`/workspace` 跨命令丢失。这是本地开发体验的核心痛点，社区关注度高。

### 热点 2：本地 MCP 服务器无传输通道（#5998）
- **链接**：[Issue #5998](https://github.com/nearai/ironclaw/issues/5998)
- **讨论热度**：1 条评论（但已开放 40 天）
- **动态**：stdio 被拒、loopback HTTP 被 deny，本地 MCP 服务器完全无法接入。昨日有一位新贡献者（jpdevries）提交了 PR #7757 试图修复该问题，允许 hosted MCP 使用字面 loopback IP。这是一个从 Issue 到 PR 的完整社区驱动闭环。

### 热点 3：能力响应规范化栈（#7686 → #7692 → #7711）
- **链接**：[PR #7692](https://github.com/nearai/ironclaw/pull/7692) | [PR #7711](https://github.com/nearai/ironclaw/pull/7711)
- **讨论热度**：三层 stack，核心贡献者 henrypark133 主导
- **动态**：第一层（#7686）已合并，第二层（#7692）待审，第三层（#7711）已提交并 supersede #7703。社区对 provider 认证失败的"类型化、有界、一致可见"的处理方式有较高期待，这直接关系到多模型提供方的接入体验。

---

## 5. Bug 与稳定性

### 5.1 严重级

| 严重度 | Issue | 描述 | 状态 |
|---|---|---|---|
| 🔴 高 | [#7748](https://github.com/nearai/ironclaw/issues/7748) | "IronClaw got confused and stopped working"——用户报告核心功能失效 | 无 fix PR，待复现和诊断 |
| 🟡 中 | [#7745](https://github.com/nearai/ironclaw/issues/7745) | Copilot MCP 扩展安装失败：`auth_required` 错误、目录存在重复条目、token 类型不明确 | 无 fix PR |
| 🟡 中 | [#7744](https://github.com/nearai/ironclaw/issues/7744) | Cron 任务管理 UI 缺少编辑和测试/触发按钮 | 无 fix PR |

### 5.2 已修复或已合入修复

| 问题 | 修复 PR | 说明 |
|---|---|---|
| CI merge queue 反复超时 | [#7756](https://github.com/nearai/ironclaw/pull/7756) | 所有 stall 均为无界 `apt-get`，已全面限界 |
| 1.2 → 1.3 升级 crash-loop | v1.3.0 Release | `activation_state` 字段兼容性修复 |
| 每次 shell 命令创建/销毁容器（性能问题） | [#7741](https://github.com/nearai/ironclaw/pull/7741) | 容器复用 + Docker Exec，耗时从 1–2.5s 降至 ~40ms |

### 5.3 故障分类报告

- **链接**：[Issue #7736](https://github.com/nearai/ironclaw/issues/7736)
- **内容**：pinchbench 套件中 169 个非通过项的分析表明，分数下降主要源于**模型能力限制而非 harness bug**（Qwen3.8-27 在特定轨迹上的表现），为基准测试的可信度提供了数据支撑。

---

## 6. 功能请求与路线图信号

### 可能进入 v1.4.0 的信号

| 功能 | 来源 | 信号 |
|---|---|---|
| **持久化 per-user 沙箱** | [#7732](https://github.com/nearai/ironclaw/issues/7732) + [#7751](https://github.com/nearai/ironclaw/pull/7751) | Epic 明确标记 v1.4.0，Step 1 PR 已提交，按用户复用的容器方案已实现 |
| **子代理激活溯源与自主唤醒** | [#7752](https://github.com/nearai/ironclaw/pull/7752) | 已添加 `ActivationProvenance` 类型和 `activate()` 原语，无生产行为变更——是 v1.4.0 后台子代理功能的基础层 |
| **OOBE 渠道优先进驻** | [#7044](https://github.com/nearai/ironclaw/issues/7044) | Epic 已关闭，后端 wiring（#6993）和前端原型（#6994）均已合入，v1.4.0 目标明确 |
| **Storybook + 设计系统** | [#7038](https://github.com/nearai/ironclaw/issues/7038) | Phase 1 PR（#7750）已提交，文档包（#7257）待审 |
| **本地 MCP 服务器支持** | [#5998](https://github.com/nearai/ironclaw/issues/5998) + [#7757](https://github.com/nearai/ironclaw/pull/7757) | 新贡献者提交了修复 PR，社区驱动的功能补全 |
| **自动化创建预检** | [#7742](https://github.com/nearai/ironclaw/issues/7742) + [#7743](https://github.com/nearai/ironclaw/pull/7743) | 新增 `ready`/`needs_setup`/`needs_input` 协议，区分"编写未来运行"与"现在就执行" |

### 路线图信号解读

v1.4.0 的功能面已逐渐明朗：**持久化沙箱 + 渠道优先进驻 + 设计系统**为三大支柱。值得留意的是 #7742（automations 预检）和 #7650（基于运行时证据的结果判定）的组合，暗示 IronClaw 正在构建更可靠的自动化执行评估体系。此外，`/cleanup` 驱动的技术债清理（#7755）也已成为常态化的代码卫生实践。

---

## 7. 用户反馈摘要

### 7.1 核心痛点

| 痛点 | 来源 | 用户原声/场景 |
|---|---|---|
| **沙箱命令开销大** | [#7732](https://github.com/nearai/ironclaw/issues/7732) | "local Docker creates and removes a container for every shell command"——每个命令都要等容器起停 |
| **本地 MCP 完全不可用** | [#5998](https://github.com/nearai/ironclaw/issues/5998) | "leaves no transport for a local MCP server of any kind"——stdio 被拒、loopback HTTP 被 deny |
| **Slack 连接提示不够私密** | [#7681](https://github.com/nearai/ironclaw/issues/7681) | 在共享频道中连接提示对所有成员可见，且需要手动往返操作 |
| **Copilot MCP 安装体验差** | [#7745](https://github.com/nearai/ironclaw/issues/7745) | 目录中两个 Copilot 条目、`auth_required` 错误、token 类型不明确 |
| **Cron 任务管理功能缺失** | [#7744](https://github.com/nearai/ironclaw/issues/7744) | 只能查看 cron job 的状态，无法编辑或手动触发 |

### 7.2 满意信号

- v1.3.0 发布后未出现回归报告
- CI 稳定性修复（#7756）的普查方法论获得了社区的认可
- OOBE 原型（#6994）的 off-by-default 设计获得了"低风险引入"的评价

---

## 8. 待处理积压

### 8.1 长期未响应的重要 Issue

| Issue | 开放时长 | 优先级 | 说明 |
|---|---|---|---|
| [#5998](https://github.com/nearai/ironclaw/issues/5998) — 本地 MCP 服务器无传输通道 | 40 天 | P1 | **已有修复 PR #7757**（新贡献者），建议维护者优先评审以鼓励社区贡献 |
| [#7255](https://github.com/nearai/ironclaw/pull/7255) — APDD 治理框架评估 | 15 天 | 中 | 文档型 PR，无障碍，建议合并 |

### 8.2 长时间未合并的重要 PR

| PR | 开放时长 | 说明 |
|---|---|---|
| [#7456](https://github.com/nearai/ironclaw/pull/7456) — 持久化存储与 profile 无关化 | 10 天 | 涉及 sandbox/ci/docs/dependencies 多 scope，risk: medium，建议关注 |
| [#7650](https://github.com/nearai/ironclaw/pull/7650) — 从运行时证据推导运行结果 | 6 天 | 与 #7742 形成功能互补，两者可能合并评审 |
| [#7516](https://github.com/nearai/ironclaw/pull/7516) — IronHub agent link 的操作界面 | 8 天 | 新贡献者（neo-sky），涉及 secrets 管理，建议维护者提供反馈 |

### 8.3 贡献者健康度提醒

- **新贡献者 PR 积压**：#7757（jpdevries）、#7516（neo-sky）均来自非核心贡献者，保持较长时间的未评审状态可能影响社区参与积极性。
- **PR #7749**（`/benchmark` 触发测试）本质上是 QA 基础设施的一部分，建议尽快处理以释放基准测试能力。

---

## 附：项目健康度评分

| 维度 | 评分（5 分制） | 说明 |
|---|---|---|
| 活跃度 | ⭐⭐⭐⭐⭐ | 24h 内 38 PR + 14 Issue，核心贡献者持续输出 |
| 发布节奏 | ⭐⭐⭐⭐ | v1.3.0 按计划稳定，RC 流程有效 |
| 社区参与 | ⭐⭐⭐ | 活跃但有 2 个新贡献者 PR 待评审 |
| Bug 响应速度 | ⭐⭐⭐ | #7748 待诊断，#7745/#7744 无响应 |
| 技术债管理 | ⭐⭐⭐⭐ | `/cleanup` 制度 + 能力响应规范化栈系统化推进 |
| 文档质量 | ⭐⭐⭐⭐⭐ | APDD 治理框架、设计系统提案、OOBE 设计文档齐备 |

---

*本日报由 AI 分析师自动生成，数据截至 2026-08-20。所有链接均指向 GitHub 原始数据。*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 2026-08-20

## 1. 今日速览

LobsterAI 项目在过去 24 小时内保持温和活跃度：**6 条 Issue 和 8 条 PR 产生更新**，其中 PR 全部为已合并/关闭状态（含 2 条今日新建的 Windows 安装器修复 PR），但**无新版本发布**。当前 6 条活跃 Issue 均创建于 2026-04-08 并带有 `[stale]` 标记，说明社区反馈存在 **4 个月以上未闭环的积压问题**，主要涉及断连后无响应、文件上传识别、网关重启和产品文案错误等。值得关注的是，今日合并的 8 条 PR 中有 6 条也带 `[stale]` 标记（创建于 4 月），表明维护者正在集中清理历史积压 PR——这些修复涵盖定时任务状态丢失、SSE 竞态条件、IM 斜杠命令、图片缩略图等多项功能和稳定性改进。综合来看，项目处于**维护者集中消化历史债务、新功能迭代暂时放缓**的阶段。

## 2. 版本发布

**无新版本发布。**

> 所有合并的 8 条 PR 均尚未随 Release 发布，值得用户关注后续版本更新。

## 3. 项目进展

今日合并/关闭了 8 条 PR，涵盖功能新增、Bug 修复、安装器与文档改进等多个维度。以下按重要程度梳理：

| PR | 类型 | 关键内容 |
|----|------|----------|
| [#1576](https://github.com/netease-youdao/LobsterAI/pull/1576) | **Bug 修复** | 修复 SSE 流监听器被旧请求异步 abort 回调错误清理的竞态条件：快速停止后立即发新消息时，共享 `cleanupFunctions` 数组导致新请求监听器被误删，流式数据静默丢失 |
| [#1570](https://github.com/netease-youdao/LobsterAI/pull/1570) | **Bug 修复** | 修复定时任务编辑时被强制重新启用：`handleSubmit` 中 `enabled` 字段硬编码为 `true`，导致编辑已禁用任务后保存即被重新开启 |
| [#1573](https://github.com/netease-youdao/LobsterAI/pull/1573) | **新功能** | 为 IM 渠道（Telegram/钉钉/飞书/Discord/QQ/微信等）新增斜杠命令支持：`/help`、`/status`、`/new`、`/compact` 等，用户无需打开桌面端即可控制会话 |
| [#1580](https://github.com/netease-youdao/LobsterAI/pull/1580) | **体验改进** | 输入框图片附件从纯图标+文件名改为 64×64 缩略图预览（`object-cover`），删除按钮 hover 显示，提升上传确认效率 |
| [#1578](https://github.com/netease-youdao/LobsterAI/pull/1578) | **安全增强** | 权限审批弹窗中的 Bash 命令增加语法高亮，帮助用户快速识别 `rm -rf`、`--force` 等危险片段 |
| [#1582](https://github.com/netease-youdao/LobsterAI/pull/1582) | **Bug 修复** | Windows 平台 setup-python：检测旧版本残留的 `__main__.py` 并覆盖，解决 pip 递归调用错误 |
| [#2511](https://github.com/netease-youdao/LobsterAI/pull/2511) | **Windows 安装器** | 支持 upload-first 两遍式 Web 安装流程，复用已上传的 NOS 负载并校验 SHA-256，确保 stub 通过不使已上传的 payload 失效 |
| [#2512](https://github.com/netease-youdao/LobsterAI/pull/2512) | **Windows 安装器** | 隐藏 dictbind 双击静默通道的插件 Banner，保留其他静默安装路径的原有行为，更新安装器设计规范 |

**总结：** 今日合并内容集中在 **稳定性修复**（SSE 竞态、定时任务状态）和 **用户体验优化**（IM 斜杠命令、权限弹窗语法高亮、图片缩略图）两大主线，兼顾 Windows 安装器细节打磨，项目整体迈出了扎实的一步。

## 4. 社区热点

今日活跃 Issue 均创建于 2026-04-08 并带有 `[stale]` 标记，虽无爆发式热度，但部分问题已积累一定评论：

- **#1569** [提问后不运行，也不显示任何信息](https://github.com/netease-youdao/LobsterAI/issues/1569)（5 条评论）：用户展示了大段截图，反馈提问后系统完全无响应、无任何输出。这是严重的功能性障碍，牵涉用户体验核心链路。

- **#1566** [最新版本无论输入什么都回复相同内容](https://github.com/netease-youdao/LobsterAI/issues/1566)（2 条评论）：版本 2026.4.3 中，模型对任意输入均回复相同内容，已附日志文件。高度疑似上下文处理或会话状态管理缺陷。

- **#1561** [模型无法获取上传的文件](https://github.com/netease-youdao/LobsterAI/issues/1561)（2 条评论）：用户明确指出**新版本回归**——此前上传文件会置于 project 目录供模型引用，新版本模型完全感知不到上传文件。

**分析：** 这三条讨论集中在 4 月报告的功能性 Bug，至今仍未见对应修复 PR 合入，是社区信任度的关键风险点。建议维护者优先排查并回应。

## 5. Bug 与稳定性

今日报告的 Bug 均来自 4 月遗留 Issue，按严重程度排列：

| 严重程度 | Issue | 描述 | 是否有 fix PR |
|----------|-------|------|---------------|
| **P0（完全不可用）** | [#1566](https://github.com/netease-youdao/LobsterAI/issues/1566) | 最新版本任何输入均回复相同内容，模型失去对话能力 | ❌ 无 |
| **P0（完全不可用）** | [#1569](https://github.com/netease-youdao/LobsterAI/issues/1569) | 提问后不运行也不显示信息，疑似静默崩溃 | ❌ 无 |
| **P1（功能回归）** | [#1561](https://github.com/netease-youdao/LobsterAI/issues/1561) | 新版本模型无法获取上传文件（此前可用） | ❌ 无 |
| **P1（稳定性）** | [#1551](https://github.com/netease-youdao/LobsterAI/issues/1551) | 网络切换导致网关反复重启，恢复原网络后正常 | ❌ 无 |
| **P2（体验）** | [#1563](https://github.com/netease-youdao/LobsterAI/issues/1563) | 流量包服务条款页面存在明显文字错误 | ❌ 无 |

> ⚠️ **值得注意：** 6 条活跃 Issue 中 **5 条为 Bug/稳定性问题，且 0 条拥有修复 PR**。今日虽合并了多项历史修复 PR，但均未覆盖上述已报告的在线问题。项目的**用户侧稳定性修复存在明显缺口**。

## 6. 功能请求与路线图信号

- **#1567** [输入框添加快捷操作按钮：停止当前话题、压缩上下文](https://github.com/netease-youdao/LobsterAI/issues/1567)：用户建议除停止按钮外，增加上下文压缩的快速入口，并提供 `/help` 等恢复指令。

  💡 **路线图信号：** 该需求与今日已合并的 PR #1573（IM 渠道斜杠命令，含 `/compact` 强制压缩上下文）高度呼应——桌面端输入框大概率会在后续版本中跟进类似能力。

- **#1573**（已合并 PR）为 IM 渠道新增 斜杠命令（`/help`、`/status`、`/new`、`/compact`、`/stop`），未来可能进一步覆盖桌面端交互。

  **预测：** 上下文压缩与快速会话重置正成为用户高频诉求，下一版本有望在桌面端提供同类快捷操作。

## 7. 用户反馈摘要

- **上下文过长/后端 Bug 导致会话卡死，缺乏快速恢复手段**（#1567）：用户建议提供强制中断或上下文压缩按钮，"出问题后可以进一步操作"，表达了对会话失控场景的强烈焦虑。
- **上传文件不可见**（#1561）：用户明确指出"这个是新版本才有的 bug"，透露对版本回退质量的失望情绪。
- **网络切换导致网关反复重启**（#1551）：真实使用场景中 网络环境动态变化 是常态，此问题影响移动办公场景的可靠性。
- **服务条款含错别字**（#1563）：虽是低严重度文案问题，但用户专门截图上报告，反映对项目专业度和文档质量的期待。
- **无响应/回复重复**（#1569、#1566）：两位用户以图形化截图和日志附件详尽描述，说明对顺利完成任务的渴望与当前体验的反差。

## 8. 待处理积压

以下 Issue 长期未获响应或缺少修复 PR，建议维护者优先关注：

1. **[P0] #1566** — 模型回复内容完全相同（4个月+ 未修复，影响核心可用性）
2. **[P0] #1569** — 提问后无任何响应（4个月+ 未修复，影响核心可用性）
3. **[P1] #1561** — 上传文件无法被模型识别（功能回归，影响文件协作场景）
4. **[P1] #1551** — 网络变化导致网关反复重启（稳定性风险）
5. **[P2] #1563** — 服务条款页面存在文字错误（文档质量问题）

> 📌 另外，6 条 PR（#1570、#1573、#1576、#1578、#1580、#1582）虽已合入，但均带 `[stale]` 标记，说明从提报到合并经历了 **4 个月以上延迟**。建议维护者评估 Issue/PR 积压处理机制，缩短反馈闭环周期。

---

*数据来源：[LobsterAI GitHub 仓库](https://github.com/netease-youdao/LobsterAI)*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目日报 — 2026-08-20

## 今日速览

过去24小时项目活跃度较高，共关闭3个问题、合并5个PR，并有1个新版本发布（20260818.10）。值得关注的是，今日多条PR集中于**Apple Container后端的稳定性修复**（资源限制未生效、状态解析错误）和**OpenAI Responses API路由逻辑的统一**（GPT-5.6 Luna支持），显示出维护者对运行时基础可靠性的重视。此外，今日新开的5个待合并PR覆盖了WhatsApp集成、HTTP认证加固与cron调度修复，社区贡献者参与度高。安全方面，HTTP vault解锁端点存在未授权暴力破解风险（CWE-306），相关修复PR已提交待合并，建议尽快跟进。

- 最新版本：20260818.10
- 新增待合并PR：5个（其中4个为今日创建）
- 关闭PR/Issue：各5个/3个，无长期遗留


## 版本发布

**20260818.10** 于昨日发布（2026-08-18）。结合今日合并的PR推断，该版本核心变更包括：内置OpenAI端点（含GPT-5.6系列）完整迁移至Responses API路由；Apple Container后端适配1.x版本状态字段并支持资源限制传入；修复WhatsApp客户端回复提及判定等。**破坏性变更**：不再对同时使用工具与reasoning的请求回退Chat Completions（对官方端点生效，自建兼容端点不受影响）；Apple Container在1.x下建议显式声明`--cpus`，否则将报错退出。升级后建议核对官方OpenAI端点的调用行为是否与预期一致，并确认Apple Container运行前已正确传入资源配额。


## 项目进展

今日合并/关闭的PR聚焦于三条主线：**Apple Container后端稳定化**（#1214、#1215）、**OpenAI Responses路由统一**（#1198、#1212）、**GPT-5.6系列支持**（#1213）。这些变更共同消除了此前围绕`OPENAI_BASE_URL`自定义配置时的路由不确定性，并将Apple Container的适配从状态读取到资源限制完整打通；同时新增了Luna模型的确定性reasoning回归测试，为后续模型迭代提供保障。**安全性方面**，#1216对vault解锁/恢复端点强制要求认证，直接修复CWE-306漏洞——此前任何未认证远程调用者均可暴力破解vault密码，修复后该接口不再位于`/api/auth/`白名单豁免范围。**协议层面**，#1217/@#1218 修正了WhatsApp集成中回复提及与push name的两个行为问题，使bot在群聊中的交互语义更符合用户直觉。整体来看，项目在容器适配、路由一致性与安全加固上均有实质推进。

值得留意的是，**#1219**将#1170引入的hardcoded deny-all工具策略改为可配置上限，这使得非操作员turn能按需放行工具调用，属于对既有限制的修正而非新增能力，预期将减少社区在sharing场景下的灵活性抱怨。


## 社区热点

今日讨论热度主要集中在 #1185（Apple Container 1.x沙箱状态误判），该Issue在3条评论后由PR #1214修复并关闭。社区对“容器明明在运行但Moltis认为未启动”的反馈直接驱动了状态解析重构，说明**容器适配的兼容性问题是当前用户最大痛点**。此外，两条来自vikng-dev的WhatsApp相关PR(#1217、#1218)虽评论不多，但均为**提升群聊交互体验**的直接反馈：例如用户直接回复bot的消息被丢弃、以及push name被硬编码为“Moltis”导致自定义名称失效。这些改动指向同一个诉求——**让集成层行为完全符合主流IM的用户习惯**。GPT-5.6 Luna相关Issue (#1181)在今日因PR #1213合并而关闭，回应了用户对特定模型可用性的关切。


## Bug 与稳定性

今日无新增Bug报告，3个既有Bug均被关闭，其中2个（#1185、#1188）与Apple Container直接相关，涉及1.x状态解析与资源限制传递；第3个（#1181）为GPT-5.6 Luna路由问题。以下为严重程度排序：

- **高危（安全）**：HTTP vault解锁与恢复端点缺乏认证（CWE-306），未认证攻击者可暴力破解密码——修复PR #1216已提交，待合并
- **中危（功能缺失）**：Apple Container资源限制（内存/CPU/pids_max）未生效——修复PR #1215已合并
- **中危（兼容性）**：Apple Container 1.x状态解析失败导致误判运行状态——修复PR #1214已合并
- **低危（易用性）**：GPT-5.6 Luna路由失败——修复PR #1213已合并


## 功能请求与路线图信号

今日无新增功能请求，但开放PR中透露了明确的路线图：通过公开audience的tool ceiling配置（#1219）增强自定义策略能力；将`heartbeat.active_hours`纳入调度器判断（#1208，待合并）以便支持定时任务在特定时段运行。此外WhatsApp的push name配置化（#1218）也为自定义bot身份提供了基础。


## 用户反馈摘要

- **“容器明明在运行却显示未启动”**（#1185）：Apple Container 1.x状态字段由标量改为嵌套对象，导致误判。修复后用户体验将实质改善
- **直接回复bot消息被忽略**（#1217）：在`mention_mode = "mention"`的群组中，回复bot的消息被丢弃。修复已在PR中，等待合并
- **push name被硬编码为“Moltis”**（#1218）：即使配置名为“Ada”，群聊中仍显示“Moltis”。修复后自定义身份将生效
- **Vault认证缺失**（#1216）：vault解锁与恢复端点无需认证，可被暴力破解


## 待处理积压

当前无超过48小时未响应的bug报告或PR。5个开放PR均已获得维护者关注，其中#1208（cron active_hours）已存在2天，等待进一步审查。Moltis的维护响应速度保持在高水准，社区无需担心长期搁置问题。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，我是你的 AI 智能体与个人 AI 助手领域开源项目分析师。根据 CoPaw 在 2026-08-20 的 GitHub 数据，我为你生成了以下项目动态日报。

---

# CoPaw 开源项目动态日报 — 2026-08-20

## 1. 今日速览

今日 CoPaw 项目活跃度**中等偏高**，核心体现在大量历史遗留 Issue 和 PR 被集中清理（累计 63 条关闭/合并），这有助于减轻维护负担。虽然新版本发布数为零，但项目在稳定性修复上取得了关键进展，尤其是针对 LLM 流式响应卡死（#7102）和杀毒软件误报（#6847）等用户痛点提交了专门的修复 PR。开发者在积极响应用户反馈，并推进多用户 Hub、会话级多项目目录等新功能，显示出强劲的迭代动力。社区方面，用户对安全性的担忧（文件被清空、杀软拦截）和功能易用性（如一键更新）的诉求较为突出。

## 2. 版本发布

今日无新版本发布。

## 3. 项目进展

今日虽无重要 PR 合并，但提交了一批高价值修复，表明项目正从“功能堆叠”转向“稳定性打磨”阶段。主要进展集中在以下几个方面：

- **稳定性修复**：
    - **修复 LLM 流式卡死** ([PR #7150](https://github.com/agentscope-ai/QwenPaw/pull/7150)): 针对 Issue #7102 用户反馈的“模型冻结超过10分钟”问题，引入了“语义流看门狗”机制，可检测并自动恢复停滞的 LLM 流，避免任务无限期挂起。
    - **修复杀毒软件误报** ([PR #6986](https://github.com/agentscope-ai/QwenPaw/pull/6986)): 针对 Issue #6847 用户反馈的“被杀软强制关停”问题，对沙盒环境进行了修复，以减少安全软件的误拦截。
- **功能增强**：
    - **自托管多用户 Hub** ([PR #7112](https://github.com/agentscope-ai/QwenPaw/pull/7112)): 新增了可选的 `qwenpaw hub` 命令，支持在本地或 Docker 中运行多用户控制平面，为团队协作和云端部署提供了基础。
    - **会话级多项目目录** ([PR #6976](https://github.com/agentscope-ai/QwenPaw/pull/6976)): 允许一个会话绑定多个项目目录，并支持主目录设置（用于文件工具的相对路径和Shell命令的默认 cwd），提升了代码库管理能力。
- **生态与集成**：
    - **新增 Volcengine 和 MiMo V2.5 模型提供商** ([PR #6515](https://github.com/agentscope-ai/QwenPaw/pull/6515)): 扩展了模型市场选择，并更新了相关模型目录。
    - **修复 provider 工具参数类型强制转换问题** ([PR #6936](https://github.com/agentscope-ai/QwenPaw/pull/6936)): 解决了模型将字符串类型参数作为 JSON 数字输出导致的校验失败问题。
- **平台体验**：
    - **远程图片冻结机制** ([PR #7146](https://github.com/agentscope-ai/QwenPaw/pull/7146)): 修复了 `view_image` 工具中远程 URL 可能破坏后续对话的问题，通过下载并持久化图片来增强稳定性与安全性。
    - **显示实际回复完成时间** ([PR #6938](https://github.com/agentscope-ai/QwenPaw/pull/6938)): 修复了聊天历史中显示不准确的回复时间戳问题，提升用户体验。

## 4. 社区热点

今日社区讨论热度较分散，但最引人注目的依然是历史遗留问题：

- **#2884 [已关闭] 用户个人目录被清空** ([Issue #2884](https://github.com/agentscope-ai/QwenPaw/issues/2884)): 该问题拥有27条评论，虽已关闭，但严重性极高。用户反馈安装后个人目录内容几乎被清空，软件被删除。这引发了社区对 CoPaw 文件操作安全和潜在漏洞的担忧。分析认为，这可能是极端情况下的误操作或安全缺陷，但**必须**作为最高优先级的安全事件进行复盘和长期跟进。

- **#2301 [已关闭] 关于更新的建议** ([Issue #2301](https://github.com/agentscope-ai/QwenPaw/issues/2301)): 该建议帖获得了10条评论，用户提出了多达6条具体的功能建议，包括一键更新、将 `/approve` 改为按钮形式、模型自动切换、内置反思机制、跨平台同步（网页端与手机端）以及集成更多国内模型服务（智普、美团）。这反映了用户对**易用性**和**移动端体验**的强烈诉求。

## 5. Bug 与稳定性

今日无新增 Bug 报告，但关闭了多项遗留问题。目前最值得关注的稳定性风险如下：

- **严重级**:
    - **LLM 流式响应卡死（冻结）** ([Issue #7102](https://github.com/agentscope-ai/QwenPaw/issues/7102)): 用户反馈模型在执行任务时冻结超过10分钟无响应。**已有对应修复 PR (#7150)**。
    - **被杀毒软件拦截/关停** ([Issue #6847](https://github.com/agentscope-ai/QwenPaw/issues/6847)): 用户反馈 QwenPaw 任务执行频繁被杀软拦截。**已有对应修复 PR (#6986)**。
- **中级**:
    - **ReactAgent 执行工具时出现 `__aiter__` TypeError** ([Issue #7034](https://github.com/agentscope-ai/QwenPaw/issues/7034)): 并发执行或流式处理时可能触发异步迭代器类型错误，该问题已关闭，但需确认修复是否合入。
    - **新版本嫩无法触发记忆压缩** ([Issue #6624](https://github.com/agentscope-ai/QwenPaw/issues/6624)): 2.0版本中自动压缩（Scroll）未触发 `summarize_when_compact` 记忆流程，而手动 `/compact` 可以，疑似设计或缺陷。该问题已关闭，建议留意后续版本行为。

## 6. 功能请求与路线图信号

结合今日开放的新功能 PR，可以预见 CoPaw 未来的演进方向：

- **多用户与协作**：`qwenpaw hub` 自托管多用户 PR 的提交，明确了 CoPaw 走向团队协作和云部署的路线。这将对标 OpenClaw 的 node 节点模式，或直接实现云端与桌面的互通（Issue #2493）。
- **平台化与扩展性**：`会话级多项目目录` 和 `新增 Volcengine、MiMo 模型提供商` 的 PR，体现了 CoPaw 正努力成为一个更强大、更通用的 AI 开发与执行平台。
- **稳定与安全**：一系列针对流式卡死、SSRF、沙盒安全的修复 PR，表明项目组正将**稳定性**和**安全性**作为下一阶段的核心目标。

## 7. 用户反馈摘要

今日的用户反馈呈现出明显的两极分化：

- **满意的方面**：
    - **本地模型运行流畅**：用户 ([tianheng2017](https://github.com/agentscope-ai/QwenPaw/issues/2776)) 反馈 `copaw-flash` 4B模型在RTX 3080上运行流畅，输出 token 速度快。
    - **功能构想有共鸣**：关于深度执行（#3074）和多智能体（#2035）的讨论，说明用户对 CoPaw 的 Agent 能力抱有较高期待。

- **不满的方面**：
    - **稳定性与可靠性是最大痛点**：任务中断（#2377）、任务消失（#2723）、流式冻结（#7102）等问题严重影响了用户体验。
    - **易用性有待提升**：一键更新（#2301）、将 `/approve` 改为按钮（#2301）、移动端页面适配（#2856）等呼声很高。
    - **安全信任危机**：目录被清空（#2884）和被杀软拦截（#6847）的问题，极大地损害了用户对 CoPaw 的信任。

## 8. 待处理积压

以下问题虽非今日新增，但长期未获官方回复，可能存在被忽略的风险：

- **重要**：
    - **多平台协同** ([Issue #2493](https://github.com/agentscope-ai/QwenPaw/issues/2493)): 用户询问云端部署的 CoPaw 与 Windows 端如何协同/互通。该诉求与目前的多用户 Hub 策略相关，建议明确规划或回复。
    - **支持公司私有模型网关** ([Issue #2296](https://github.com/agentscope-ai/QwenPaw/issues/2296)): 企业用户希望对接非 OpenAI 格式的私有 LLM 网关。这是 B 端落地的重要需求，建议在路线图中予以考虑。

- **一般**：
    - **浏览器自动化能力差** ([Issue #3261](https://github.com/agentscope-ai/QwenPaw/issues/3261)): 用户反馈浏览器自动化容易触发反爬机制，且无法复用登录状态。该问题对 RPA 类应用场景至关重要。
    - **支持云手机或 Harness Agents** ([Issue #3260](https://github.com/agentscope-ai/QwenPaw/issues/3260)): 用户期待 CoPaw 支持 ACP/Codex 或集成更强大的 Harness 编排能力。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-08-20

> 开源 AI 智能体与个人助手框架 | github.com/zeroclaw-labs/zeroclaw


## 1. 今日速览

过去 24 小时项目保持高活跃度：共产生 42 条 Issue 动态（41 开/1 关）与 50 条 PR 动态（48 待合并/2 已合并关闭），无新版本发布。讨论重心集中在**运行时会话持久化契约归属**（#9487/#9600）、**Rust 反模式技术债清理**（#10118，307 个候选修复项）、以及 **CI 基础设施改进**（Windows 测试失败 #7462、缓存优化 #7108）三大方向。值得注意的是，贡献者 **JordanTheJet** 在 8 月 19 日密集提交了 8 个 PR，覆盖 panic 消除、dead-code 清理、unsafe 审计等代码质量硬仗，并与 NiuBlibing、IftekharUddin 形成多线推进的态势。虽然合并率偏低（48 条 PR 待合并），但这与项目严格执行 risk 分级评审和 maintainer-review 机制相符，整体**项目活跃度：高**，并行工作流清晰。


## 2. 版本发布

**无新版本发布。**

最新公开版本仍为 v0.8.4（#9376），项目正处于 v0.9.0 功能冻结前的密集 RFC 评审期。


## 3. 项目进展

今日无 PR 被合并，有 2 条 PR 动态为关闭/合并状态：

- **#10145 — `chore: withdrawn`**（作者 JordanTheJet）：作者主动撤回，无功能影响。
- **#10067 — `[Bug]: tool-result truncation is a fixed 50,000 chars`**（Issue #10067 已关闭）：该 Bug 经重新界定后关闭，确认原始 1MB 报告有误，实际为 50,000 字符固定截断且对结构化输出按字节截断的问题，本次关闭意味着修复已完成（相关代码改动已在之前合入）。

待合并队列中值得关注的 PR 有：

| PR | 标题 | 风险 | 等待时长 | 意义 |
|---|---|---|---|---|
| #9447 | `fix(anthropic): classify incomplete terminal responses` (XL) | high | ~24 天 | 避免不完整响应被当作完成回复，影响 Anthropic 通道可靠性 |
| #9745 | `fix(memory): add per-agent attribution and scoping to the knowledge graph` (XL) | high | ~16 天 | 修复知识图谱跨 Agent 数据泄露，属安全关键修复 |
| #9744 | `refactor(gateway): require authenticated webhook ingress` (XL) | high | ~16 天 | 三个 webhook 通道（WhatsApp/Linq/Nextcloud Talk）认证失败即拒绝，安全加固 |
| #9320 | `fix(cron): bound agent job runs with wall-clock timeout` (XL) | high | ~28 天 | 修复 cron 任务无限期锁死问题 |
| #9504 | `fix(runtime): show a terminal notice when a turn ends on context exhaustion` | high | ~23 天 | 提升上下文耗尽场景的用户可见性 |
| #9981 | `feat(runtime): report the active shell dialect in system prompt` (XL) | high | 已标记 `do-not-merge` | Windows 下区分 cmd/PowerShell，解决跨平台指令误判 |

**项目整体进度**：多线推进但合并通道存在积压，近 20 个大中型 PR 处于待评审状态，若维持当前节奏，v0.9.0 的发布可能面临延期风险。


## 4. 社区热点

今日讨论最密集的议题并非新开 Issue，而是进入最后评审阶段的几个存量 RFC：

- **[#9487 — RFC: Runtime-owned conversation sessions and transport surface adapters](https://github.com/zeroclaw-labs/zeroclaw/issues/9487)**（20 评论，+8月19日）
  讨论围绕会话生命周期归属权展开：运行时是否应统一持有会话状态、各传输层（Web/Matrix/ACP 等）只做适配。这是当前**最核心的架构争议**，尚需维护者拍板。

- **[#7462 — [Bug]: 74 test failures on Windows](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)**（18 评论，持续 70 天）
  项目在 Windows 11 简体中文环境（代码页 936）下有 74 个测试失败，而 CI 只跑 Linux，长期未暴露。多位用户跟帖确认复现，**跨平台测试覆盖缺失**已成为社区信任度隐患。

- **[#10118 — [Tracker]: Rust anti-slop policy debt remediation](https://github.com/zeroclaw-labs/zeroclaw/issues/10118)**（16 评论，当天新建）
  由 JordanTheJet 发起的清理 tracker：307 个违反 anti-slop 策略的候选点（202 个生产 panic、105 个其余问题）。这在 24 小时内迅速获得 16 条评论，说明社区对**代码质量基础设施**的关注度很高。配套的 #10134/#10129/#10123/#10124 等 PR 即为其第一批落地。


## 5. Bug 与稳定性

| 严重度 | Issue | 状态 | 关联 PR |
|---|---|---|---|
| **S0 安全** | [#9976 — `bug(provider): stop logging Anthropic credential fragments`](https://github.com/zeroclaw-labs/zeroclaw/issues/9976) — debug 日志泄露凭据头尾 8+4 字符 | in-progress | — |
| **S1 阻断** | [#10066 — `[Bug]: SOP engine promotes and runs later steps before recording a step's output-schema rejection`](https://github.com/zeroclaw-labs/zeroclaw/issues/10066) — SOP 步骤顺序执行失败但后续步骤真实运行（p0） | accepted | — |
| **S1 阻断** | [#9290 — `[Bug]: Windows desktop installer fails at launch with missing TaskDialogIndirect`](https://github.com/zeroclaw-labs/zeroclaw/issues/9290) — Windows 桌面版无法启动（p1，已挂 28 天） | accepted, help wanted | — |
| **S2 降级** | [#10106 — `[Bug]: Exact proxy selectors reject supported transcription services`](https://github.com/zeroclaw-labs/zeroclaw/issues/10106) — 配置代理选择器不识别 5 个转录服务 key | accepted | — |
| **S2 降级** | [#10045 — `[Bug]: Persisted image markers can retain temporary source paths`](https://github.com/zeroclaw-labs/zeroclaw/issues/10045) — 图片标记残留临时路径导致反复告警 | in-progress | — |
| **S2 降级** | [#7462 — `[Bug]: 74 test failures on Windows`](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) — Windows 测试全挂 | accepted | — |
| **S3 轻微** | [#10103 — `[Bug]: ZeroCode Health status values misalign in French and Spanish`](https://github.com/zeroclaw-labs/zeroclaw/issues/10103) — 标签宽度固定 11 但法语/西语为 13 格 | open | — |

**正面信号**：`#10134 (fix(runtime): keep agent dispatch panic-free)` 和 `#10129 (fix(tools): replace panic-prone assumptions)` 分别清除了 17 和 21 个 panic/invariant 隐患，配合 `#10124` 对 25 处 unsafe 平台的审计，Rust 代码质量在系统性改善。


## 6. 功能请求与路线图信号

- **Session 可用性抱怨 → 会话持久化重构**：[#10141 — `[Feature]: Please make sessions usable`](https://github.com/zeroclaw-labs/zeroclaw/issues/10141) 用户表达了对会话管理的强烈不满（复制、切换、恢复都困难）。这与 #9487/#9600 的会话持久化契约重构高度相关，且 PR #9739 已实现多会话面板（multi-session panes with agent sidebar），预计 v0.9.0 会重点改善该体验。

- **WASM 插件架构**：[#10076 — `[RFC]: Comprehensive WASM plugin architecture`](https://github.com/zeroclaw-labs/zeroclaw/issues/10076) 提出 hook/backend/capability 三层的「一切皆插件」方案。与既有 `runtime:wasm` 标签的 #9126（验证 typed instance config）形成呼应，可能是 v0.10 级规划。

- **SOP 权限契约**：[#9598 — `RFC: Define the SOP capability permission contract`](https://github.com/zeroclaw-labs/zeroclaw/issues/9598) 处于 Rev 3，配合 PR #9476（已验证的取消控制）和 #9694（只读 SOP 面板），SOP 功能正在快速收敛为 v0.9.0 的正式能力。

- **CI/工程质量**：#7108（缓存与关键路径优化）、#9330（AI 辅助 PR 预评审）、#9990（PR 风险分级校准）三条线共同指向**提升评审效率和开发者体验**，属基础设施投入。


## 7. 用户反馈摘要

- **会话管理是最大痛点**（#10141）：用户 `klonuo` 直言"进入之前的会话非常痛苦"，表达了对会话复制、切换、持久化的强烈需求。值得关注的是——该 Issue 没有任何标签（未 triage），反映出**新用户反馈的处理通道可能存在延迟**。

- **Windows 生态支持不足**（#7462/#9290）：同为 Windows 用户，一位报告 74 个测试失败（开发者视角），另一位直接无法启动桌面应用（终端用户视角）。当前 CI 仅覆盖 Linux 是核心问题。

- **安全透明度获认可**：虽然 Anthropic 凭据日志问题（#9976）严重度很高，但社区对项目快速响应持正面态度——该问题从报告（8月13日）到 in-progress 仅数小时，且 SECURITY.md 过时问题（#10074）也被社区成员主动发现并申报。

- **配置体验矛盾**：#9828 PR 允许 AI 代理在运营商审批下编写配置（取代原始的 shell echo），而 #10106 暴露了精确代理选择器无法识别转录服务的配置死角。前者是主动设计，后者是被动遗漏。


## 8. 待处理积压

| 类型 | 编号 | 标题 | 等待时长 | 备注 |
|---|---|---|---|---|
| **P1 Bug** | [#9290](https://github.com/zeroclaw-labs/zeroclaw/issues/9290) | Windows 桌面版启动失败（缺 TaskDialogIndirect） | **28 天** | 已有 `help wanted` 标记，但无 assignee |
| **P1 Bug** | [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) | Windows 74 个测试失败 | **70 天** | 持续活跃讨论中，需要 CI 矩阵扩展决策 |
| **RFC** | [#9487](https://github.com/zeroclaw-labs/zeroclaw/issues/9487) | 运行时持有会话 + 传输适配层 | 23 天 | 20 评论，等待 maintainer 拍板；与 #9600 tracker 绑定 |
| **RFC** | [#6165](https://github.com/zeroclaw-labs/zeroclaw/issues/6165) | 轻量化核心，外部集成替代内置 | **115 天** | 架构方向性讨论，涉及核心边界重新划分 |
| **PR XL** | [#9320](https://github.com/zeroclaw-labs/zeroclaw/pull/9320) | cron 任务 wall-clock 超时 | **28 天** | P1 修复，XL 规模，需 maintainer review |
| **PR XL** | [#9447](https://github.com/zeroclaw-labs/zeroclaw/pull/9447) | Anthropic 不完整响应分类 | 24 天 | 同样 P1，标 `needs-author-action`，等待作者更新 |

> **维护者提醒**：#9487 作为当前最核心的架构 RFC 已进入 20+ 评论阶段，其决策将影响 #9488/#9600/#9702 等多个关联工作流。此外，#9290 是唯一长期未分配的 P1 桌面端问题，建议尽快指派。


## 附：健康度指标

| 指标 | 今日值 | 趋势/备注 |
|---|---|---|
| 事件总吞吐 | 92 条（42 Issues + 50 PRs） | 高活跃度 |
| 合并率 | 2/50（4%） | 偏低，存在评审积压 |
| P0/P1 未关闭 Bug | 2（#10066, #9976） | 均已有方向，无阻塞性 |
| 待处理 RFC（≥30 天） | 4 个 | 需要 maintainer 决策 |
| 新贡献者活跃度 | 1 个新作者（ggettert, PR #10150） | 社区吸引力良好 |
| 代码质量投入 | 4 个 PR 清理 300+ 隐患 | 系统性改善中 |

---

*本日报基于 2026-08-19 至 2026-08-20 的 GitHub 公开数据自动生成，所有链接均为仓库真实地址。*

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*