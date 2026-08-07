# OpenClaw 生态日报 2026-08-07

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-07 01:58 UTC

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

# OpenClaw 项目动态日报 — 2026-08-07

## 1. 今日速览

过去24小时内，OpenClaw 仓库保持极高活跃度：共产生 500 条 Issue 更新（其中新开/活跃 432 条，关闭 68 条）和 500 条 PR 更新（待合并 405 条，合并/关闭 95 条）。P0/P1 级问题仍有多项悬而未决，其中 **Agent 数据库迁移失败（#119263）** 和 **totalTokens 膨胀导致过早压缩（#118772）** 为当前最严重的阻塞性问题；与此同时，A2UI HEAD 响应修复（#117961）等多项 PR 已合入主干。整体健康度中等偏活跃，Bug 修复速度略慢于新问题涌入速度，需关注关键回归的处置进展。


## 2. 版本发布

过去24小时内无新版本发布。需注意，多个 Issue 指向 **2026.7.2 版本存在关键回归**（详见下文 Bug 与稳定性章节），建议维护团队评估是否需要发布补丁版本（2026.7.3）以修复数据库迁移失败（#119263）与 totalTokens 膨胀（#118772）等 P0 级问题。


## 3. 项目进展

过去24小时内合入的 PR 数量为 95 条，以下为几项值得关注的关键变更：

- **[fix(canvas): serve Content-Length on A2UI HEAD responses (#117961)](https://github.com/openclaw/openclaw/pull/117961)** — 已合并（CLOSED）。修复 A2UI 资源服务器响应 HEAD 请求时缺少 `Content-Length` 头的问题，使 HEAD 响应符合 RFC 9110 语义，提升协议兼容性。

- **[fix(gateway): make doctor dreaming timestamp comparators NaN-safe (#118749)](https://github.com/openclaw/openclaw/pull/118749)** — 已合并（CLOSED）。修复 `doctor` 命令中 dreaming 统计比较器在遇到畸形时间戳时的崩溃风险，增强诊断工具的健壮性。

- **[fix(heartbeat): explain target-none skips (#119689)](https://github.com/openclaw/openclaw/pull/119689)** — 已合并（CLOSED）。在保持机器可读的 `reason: "target-none"` 不变的前提下，为运维人员补充可读的跳过原因说明，改善可观测性。

此外，95 条合并/关闭的 PR 中涵盖大量文档修正、小型 Bug 修复和测试加固，显示出项目正处于持续迭代的活跃期。


## 4. 社区热点

| 议题 | 类型 | 评论数 | 👍 | 主题 |
|------|------|--------|-----|------|
| [#75 Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75) | 功能需求 | 116 | 80 | 请求支持 Linux 和 Windows 桌面应用 |
| [#116277 DeepSeek v4 Flash silent reply failure](https://github.com/openclaw/openclaw/issues/116277) | Bug（已关闭） | 114 | 0 | DeepSeek v4 Flash 静默回复失败 |
| [#7707 Memory Trust Tagging by Source](https://github.com/openclaw/openclaw/issues/7707) | 功能需求 | 28 | 0 | 按来源为记忆条目标记信任级别 |
| [#27445 announceTarget option for sub-agent routing](https://github.com/openclaw/openclaw/issues/27445) | 功能需求 | 12 | 5 | 子代理完成通知可路由到父会话 |

**分析：**

- **跨平台支持诉求强烈**：#75（评论 116 条，👍 80 个）是当之无愧的社区焦点。用户对 Linux/Windows 桌面应用的诉求持续高涨，虽已关闭，但反映了桌面端覆盖不足的长期痛点。
- **模型兼容性问题频发**：#116277（评论 114 条）虽已关闭，但 DeepSeek v4 Flash 的静默失败问题引发了大量讨论。同类问题 #88657、#88079 也在持续发酵，表明多模型接入的稳定性仍是用户高度关注的领域。
- **安全与记忆架构受关注**：#7707（评论 28 条）提出的记忆信任标记机制，是用户对 AI 安全（记忆投毒防护）自发提出的解决方案，值得维护团队参考。


## 5. Bug 与稳定性

### 🔴 P0 / 严重阻塞

- **[Agent DB v14→v15 迁移失败：`no such column: entry_valid`，网关拒绝启动 (#119263)](https://github.com/openclaw/openclaw/issues/119263)** — 2026.7.2 版本中从 v14 升级到 v15/v16 schema 时迁移失败，`openclaw doctor --fix` 无法恢复，属发布阻断级回归。无关联 fix PR，严重性极高。

- **[2026.7.1+ embedded-agent-runner sessionEntry.totalTokens 膨胀，导致过早压缩（4-8% 上下文窗口即触发）并造成数据丢失 (#118772)](https://github.com/openclaw/openclaw/issues/118772)** — 回归问题（P0），totalTokens 被多轮工具循环的累计用量错误抬高，导致提前触发压缩造成数据丢失。已有 linked PR，但状态未知。

### 🟠 P1 / 高优先级

- **[聊天回复被“线程切换”拒绝：stale expectedLeafEntryId 未刷新（#115700）](https://github.com/openclaw/openclaw/issues/115700)** — 模型跑完后 `chat.send` 被持续拒绝，影响用户体验。已有 linked PR。
- **[claude-cli 后端：合成“No response requested.”占位符导致 Telegram 回合完全静默（#90789）](https://github.com/openclaw/openclaw/issues/90789)** — 无观测性的消息丢失问题。有 linked PR。
- **[Gateway 冷启动回归 ~2.5x（#119087）](https://github.com/openclaw/openclaw/issues/119087)** — 2026.7.1-beta.1 到 2026.7.2-beta.7 性能显著退化。无 fix PR。
- **[Foreground reply fence 导致并发群聊回复丢失（#92186）](https://github.com/openclaw/openclaw/issues/92186)** — 自动模式下，并发群组消息仅投递最新一条回复，造成回复丢失。已有 linked PR。
- **[chat delta 节流无尾部 flush，导致块滞留（#119557）](https://github.com/openclaw/openclaw/issues/119557)** — 150ms 节流无尾部刷新，蓄积的 chunk 须等下一个事件才被投递，造成输出延迟与丢失。已有 linked PR（#120059 等）。

### 🟡 P2 / 中优先级（代表性）

- [DeepSeek V4 Flash 不完整回合：payloads=0, tools=2, stopReason=stop（#88657）](https://github.com/openclaw/openclaw/issues/88657)
- [WebChat 不渲染 Kimi Code & DeepSeek Reasoner 的 reasoning_content 流（#88079）](https://github.com/openclaw/openclaw/issues/88079)
- [Windows vitest 清理失败：EBUSY unlink agent state DB（#119796）](https://github.com/openclaw/openclaw/issues/119796)
- [LINE 渠道：回复令牌过期 + 缺少推送回退保护导致消息静默丢失（#86012）](https://github.com/openclaw/openclaw/issues/86012)
- [Feishu 流式卡片多个内容投递 Bug 导致最终文本丢失/过期/重复（#77685）](https://github.com/openclaw/openclaw/issues/77685)
- [预压缩（预算触发）被 ~60s 硬上限截断，忽略 `compaction.timeoutSeconds`（#95553）](https://github.com/openclaw/openclaw/issues/95553)

**观察：** 今日无新增 P0 级问题上报，但既有 P0（#119263、#118772）仍未解决，其中 #119263 为升级阻断，建议优先处理。模型兼容性（DeepSeek、Ollama、Bedrock）和消息丢失类问题占比最高。


## 6. 功能请求与路线图信号

| Feature | Issue | 评论 | 👍 | 可能纳入版本 |
|---------|-------|------|-----|-------------|
| Linux/Windows 桌面应用 | [#75](https://github.com/openclaw/openclaw/issues/75) | 116 | 80 | 中期（若团队认可跨平台优先级） |
| 记忆信任标记（Memory Trust Tagging） | [#7707](https://github.com/openclaw/openclaw/issues/7707) | 28 | 0 | 需安全评审，短期可能性低 |
| 子代理 announce 路由选项 | [#27445](https://github.com/openclaw/openclaw/issues/27445) | 12 | 5 | 已有 linked PR，可能进入下一迭代 |
| 每 spawn 的工具限制 | [#15032](https://github.com/openclaw/openclaw/issues/15032) | 7 | 0 | 已有 linked PR，安全相关被高度关注 |
| Slack 模态框支持 | [#88154](https://github.com/openclaw/openclaw/issues/88154) | 7 | 1 | 待产品决策 |
| 自主代理节奏感知限流 | [#45771](https://github.com/openclaw/openclaw/issues/45771) | 6 | 2 | 待产品决策 |
| 代理自触发上下文压缩 | [#6757](https://github.com/openclaw/openclaw/issues/6757) | 6 | 2 | 增强核心体验，较可能 |
| 控制 UI 插件贡献槽位（RFC） | [#71736](https://github.com/openclaw/openclaw/issues/71736) | 9 | 1 | SDK 扩展，中期 |
| agent-scoped usage budgets | [PR #104060](https://github.com/openclaw/openclaw/pull/104060) | — | — | **已在 PR 阶段，预计近期合入** |
| Twilio RCS 渠道 | [PR #105025](https://github.com/openclaw/openclaw/pull/105025) | — | — | **已在 PR 阶段，但需 ⚠️ 兼容性评审** |

说明：**agent-scoped usage budgets（#104060）** 若合入，将为跨所有扩展的 Agent 使用量提供运行时硬性限额保护，属于成本控制类核心能力，是近期重要功能方向；**Twilio RCS（#105025）** 则代表渠道类型的扩展仍在持续推进。


## 7. 用户反馈摘要

- **正向反馈：** #73537 中，用户 Reneb-cafe 明确表示“感谢 OpenClaw，它已成为我们家庭和企业日常流程的一部分”，并建议为 Releases 添加生产就绪稳定性标签——侧面体现了生产环境中对稳定性标识的迫切需求。

- **稳定性焦虑：** 多个用户在升级后遭遇回归：
  - #119263 用户 Wwhin-88 在升级到 2026.7.2 后无法启动网关，且 `doctor --fix` 无法修复。
  - #90595 用户报告“6.1 版本升级后 Cron 运行失败通知在热重载和重试期间反复触发，导致告警疲劳”。
  - #115546 用户报告 CLI 预算压缩在大会话上 100% 失败，且超时远早于配置期限。
  - #119557 用户发现输出被节流卡住，需等待下一事件才被投递。

- **功能诉求：** #75 中用户对 Linux/Windows 客户端的呼声最高，多位用户表达“macOS 可用但工作环境是 Windows/Linux”的痛点。

- **安全关切：** #7707 和 #15032 均源于用户对提示注入/记忆投毒的实际防御需求，有用户在评论中详细描述了构建 DMZ 三区隔离 Web 搜索管道的真实场景；#117445（Feishu 解码为“?”无法回复）与 #117609（嵌入助手阶段长回合单次错误即终止）亦引发较多共鸣。


## 8. 待处理积压

以下为长期未响应或至今仍在等待处理的重要 Issue / PR：

| 编号 | 标题 | 创建时间 | 最后更新 | 天数 | 状态 |
|------|------|----------|----------|------|------|
| [#75](https://github.com/openclaw/openclaw/issues/75) | Linux/Windows Clawdbot Apps | 2026-01-01 | 2026-08-06 | 218天 | 已关闭，但需产品决策 |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | Memory Trust Tagging by Source | 2026-02-03 | 2026-08-06 | 185天 | 需要维护者与安全评审 |
| [#6599](https://github.com/openclaw/openclaw/issues/6599) | `/models` test-fallback 命令 | 2026-02-01 | 2026-08-06 | 187天 | 需要维护者/产品决策 |
| [#15032](https://github.com/openclaw/openclaw/issues/15032) | Per-spawn tool restrictions | 2026-02-12 | 2026-08-07 | 176天 | 需安全评审 + 产品决策 |
| [#6757](https://github.com/openclaw/openclaw/issues/6757) | Agent-triggered 上下文压缩 | 2026-02-02 | 2026-08-06 | 186天 | 需要维护者/产品决策 |
| [#60981](https://github.com/openclaw/openclaw/pull/60981) | PR：Filesystem Access Control (PathGuard) | 2026-04-04 | 2026-08-07 | 125天 | ⏳ 需要真实行为证明 |
| [#65655](https://github.com/openclaw/openclaw/pull/65655) | PR：harden Mattermost slash callback auth | 2026-04-13 | 2026-08-07 | 116天 | ⏳ 需要真实行为证明 |
| [#61519](https://github.com/openclaw/openclaw/pull/61519) | CI: 报告循环依赖 | 2026-04-05 | 2026-08-07 | 124天 | ⏳ 等待作者 |
| [#76631](https://github.com/openclaw/openclaw/pull/76631) | docs(prometheus): 警告 plugins.allow 严格模式 | 2026-05-03 | 2026-08-07 | 96天 | ⏳ 等待作者 |

**给维护者的提醒：**
- 多个 2 月份提出的功能请求已积压近半年，其中 #7707（记忆信任标记）和 #15032（子代理工具限制）属安全类诉求，建议优先给出回应。
- PR 队列中 #60981（PathGuard 文件系统访问控制）与 #65655（Mattermost 认证加固）分别涉及安全边界和渠道安全，建议优先安排评审。
- #119263（数据库迁移失败）为当前发布阻断级问题，建议尽快修复并发布补丁版本。
- #86119（孤儿 node server.js 进程累积）在 Docker 环境下影响资源泄漏，已持续 2.5 个月，建议关注。

---

## 横向生态对比

# AI 智能体开源生态横向对比分析报告

**报告日期**：2026-08-07  
**数据窗口**：过去 24 小时  


## 1. 生态全景

个人 AI 助手/自主智能体开源生态正处于**从功能堆叠向质量治理过渡的关键阶段**。头部项目（OpenClaw、Hermes Agent）保持极高迭代频率，但 P0/P1 级回归问题（数据库迁移失败、上下文膨胀、消息丢失）正在消耗社区信任；腰部项目（NanoBot、IronClaw、CoPaw）面临"用户增长快于稳定性和维护响应"的结构性矛盾，长期积压的 PR 和 Issue 是普遍痛点；与此同时，跨项目共同涌现实质性的技术方向——**跨平台桌面端、多模型容灾、安全加固（记忆投毒防护、密钥隔离、文件系统访问控制）、Agent 间通信（A2A）**——表明生态正在从"单机对话玩具"向"生产级自主智能体基础设施"演进。整体而言，生态活跃度高、创新密度大，但**稳定性与可观测性已成为决定用户留存的核心竞争力**。


## 2. 各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | PR 合并/关闭 | 新版本 | 健康度评估 |
|------|------------|---------|-------------|--------|-----------|
| **OpenClaw** | 500（新开 432） | 500 | 95 | ❌ | 🟡 中等偏活跃 — 2 个 P0 未解决，Bug 修复速度慢于新问题涌入 |
| **Hermes Agent** | 50 | 50 | 4 | ❌ | 🟡 高活跃 — 46 个 PR 积压偏高，god-file 重构进行中，Feishu 审批按钮修复积压过久 |
| **NanoBot** | 9（新开 8） | 17 | 5 | ❌ | 🟢 健康 — 合并节奏稳定，3 个 P0/P1 安全 PR 待合并 |
| **PicoClaw** | 0 | 2 | 1 | ❌ | 🟢 平稳 — 中低活跃度，功能迭代期，#3200 待审 |
| **NanoClaw** | 2 | 14 | 8 | ❌ | 🟢 健康 — 核心维护者响应积极，系统清理积压中 |
| **IronClaw** | 50 | 50 | ~30 | ✅ v1.1.0 | 🟡 高迭代高积压 — P1 runner lease 问题 38 天未解决 |
| **LobsterAI** | 5（新开 2） | 2 | 0 | ❌ | 🔴 维护响应滞后 — 4 个月无 PR 合并，积压集中在 4 月 |
| **CoPaw** | 34（新开 ~17） | 50 | 30 | ❌ | 🟡 高活跃高压力 — 3 个 P0（长会话/MCP 可靠），积极架构治理中 |
| **ZeroClaw** | 31 | 50 | 5 | ❌ | 🟡 高讨论低合并 — v0.8.5 稳定化阶段，SOP 模块 P1 Bug 集中爆发 |
| **NullClaw / TinyClaw / Moltis / ZeptoClaw** | — | — | — | ❌ | ⚪ 无活动 |


## 3. OpenClaw 在生态中的定位

**核心参照系地位稳固。** OpenClaw 在 Issue/PR 绝对数量上（500+/500+）远超其他项目（NanoBot 9/17、PicoClaw 0/2、NanoClaw 2/14），社区规模与开发者生态优势明显。技术路线上，OpenClaw 的特色在于**平台渠道广度**（Telegram、Feishu、LINE、WebChat、Slack、Discord 等全覆盖）与 **A2UI 协议**（自定义 UI 协议，区别于 NanoBot 的 WebSocket 方案与 Hermes 的 Electron 桌面端）。同时，**Claw 命名家族**（OpenClaw、PicoClaw、NanoClaw、NullClaw、IronClaw、TinyClaw、ZeptoClaw、ZeroClaw）已形成事实上的生态集群，但各自独立发展。OpenClaw 的隐忧在于：**庞大的功能面和渠道数带来了成比例的回归风险**（当前 2 个 P0 阻塞问题即为例证），且维护团队对社区安全类需求（#7707 记忆信任标记、#15032 工具限制）响应偏慢，可能为细分场景的竞品（NanoBot 的记忆信任、ZeroClaw 的安全加固）留下差异化空间。


## 4. 共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 | 成熟度信号 |
|----------|---------|---------|-----------|
| **跨平台桌面应用** | OpenClaw（#75, 116 评论/80👍）、Hermes（桌面端回归 #79407）| 用户工作环境为 Win/Linux，macOS-only 覆盖不足；桌面端回归影响可用性 | 需求明确但供给不足 — 头部项目尚未给出明确路线图 |
| **多模型容灾与回退链** | PicoClaw（#3200）、LobsterAI（#1199）、CoPaw（#6659）、Hermes（Grok 对齐）| 主模型不可用/响应异常时自动降级到备用模型；per-model token 配置 | PicoClaw 已实现前端+后端完整链路，LobsterAI PR 悬置 4 个月 |
| **成本控制与使用量透明** | OpenClaw（agent-scoped budgets, PR #104060）、NanoBot（#5266）、Hermes（#77221/#77222）| 运行时硬性限额保护；token 消耗记录与可视化 | OpenClaw 和 Hermes 已进入 PR 阶段，NanoBot 仅停留在 Issue 层面 |
| **记忆安全与信任标记** | OpenClaw（#7707）、NanoBot（#5276）、ZeroClaw（#9328）、Hermes（#79339）| 记忆投毒防护；按来源标记信任级别；外部记忆后端同步可靠性 | OpenClaw 和 NanoBot 停留在需求讨论期，ZeroClaw 已有明确攻击链分析 |
| **Agent 间通信（A2A）** | ZeroClaw（#9106 RFC）| 出站 A2A 客户端（主动调用其他 Agent），当前仅被动响应 | 仅出现在 RFC 阶段，无具体实现信号 |
| **MCP 集成深度优化** | CoPaw（#6732/#6724/#6761）、Hermes（#80652/#62808）、OpenClaw（注册任意 MCP）| 工具调用超时配置；MCP 服务稳定性；stdio 命令白名单安全 | CoPaw 有超时诉求无实现，Hermes 有白名单 PR 待合并 |
| **消息渠道可靠性** | Hermes（Feishu 审批按钮，4 个 Issue 指向 1 个 PR）、IronClaw（Slack 投递 #7157）、CoPaw（#6684 频道重试）、NanoClaw（纯媒体消息丢弃）| 渠道消息丢失/静默失败/投递目标混乱 | 各项目都在单独解决，无跨项目标准；Feishu 修复 PR #10256 在 Hermes 积压已久 |
| **升级安全性（回滚）** | NanoClaw（#3194）、OpenClaw（#119263 DB 迁移失败）、ZeroClaw（#9779）、LobsterAI（#1198）| 升级/迁移失败导致数据丢失或服务不可用 | NanoClaw 已提交事务性升级修复 PR，OpenClaw 无修复 PR，属于高危共性 |


## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 技术架构关键差异 | 核心痛点 |
|------|---------|---------|----------------|---------|
| **OpenClaw** | 全渠道消息平台 + 自主 agent 核心 + A2UI 协议 | 全栈开发者、个人自动化重度用户 | 自研 A2UI 协议、多平台适配、Clawdbot 桌面端 | 功能面广导致回归风险高、P0 修复慢 |
| **Hermes Agent** | 开发者友好的多后端 agent + 桌面端 + 记忆系统 | 开发者、企业内部部署 | 桌面端 Electron、记忆 provider 抽象、God-file 单体架构（重构中） | 单体架构可维护性差（858KB gateway run.py）、PR 积压高 |
| **NanoBot** | 轻量级多渠道机器人 + 沙箱 + WebUI | 个人/小团队快速部署 | Python 系、bwrap 沙箱隔离、WebSocket 实时消息 | 会话模型绑定僵化（无法切换）、MCP 规模小（更轻量） |
| **IronClaw** | 自主例程（Routine）+ 扩展生态（MCP/IronHub） | 从 NearAI 生态入手的开发者 | 双通道投递模型、MCP 注册 + IronHub 深度链接、沙箱配置 | Routine 可靠性（runner lease、无 thread）、GitHub 集成 403 |
| **CoPaw** | 长会话稳定性 + 上下文管理 + 记忆（ReMe） | 依赖自动化长任务的用户 | AgentScope 2.0 生命周期对齐、Scroll 统一上下文协议 | 长会话 P0 Bug 密集、MCP 工具周期性失效 |
| **ZeroClaw** | 企业级安全 + SOP 流程化 + 网关治理 | 企业用户、高安全要求团队 | SOP 引擎、A2A 规划中、工具访问策略（ToolAccessPolicy） | SOP 模块稳定性差、文档与实现脱节、核心安全 Issue 长期未解 |
| **NanoClaw** | 轻量个性化 + 技能动态更新 + Telegram 优化 | 个人用户、Telegram 深度用户 | 技能 pre-flight/凭据分离、事务性升级 | 社区规模小、技能生态待建设 |
| **PicoClaw / LobsterAI** | 极简 + 中文生态 / 本地化、Windows 端 | 特定场景（低资源部署 / Windows 用户） | PicoClaw 轻量部署；LobsterAI PowerShell 内核 | 维护资源有限（LobsterAI 4 个月无合并） |


## 6. 社区热度与成熟度分层

**第一梯队 — 高速迭代（OpenClaw、Hermes Agent、CoPaw、IronClaw）**  
高 Issue/PR 量（每日 50-500 条），功能推进快，但伴随回归风险。其中 **OpenClaw** 和 **CoPaw** 正在经历"功能广度→架构治理"的转型阵痛；**Hermes** 有明确的重构纲领（god-file 分解），战略方向清晰。

**第二梯队 — 质量巩固（NanoBot、NanoClaw、ZeroClaw）**  
NanoBot/NanoClaw 处于稳定的质量打磨期，维护者响应积极，安全类 PR 已排入队列；ZeroClaw 通过 v0.8.5 稳定化 + v0.9.0 规划（安全/网关/A2A）展现明确版本节奏，但 SOP 模块 Bug 爆发正在消耗社区信任。

**第三梯队 — 边缘活跃（PicoClaw、LobsterAI）**  
每日 0-5 条更新，但有实质性的 PR 在推进（PicoClaw #3200 模型回退链）。LobsterAI 存在"用户持续反馈、维护响应滞后"的恶性循环，4 个月积压未处理，社区活跃度与满意度下行风险显著。

**非活跃（NullClaw、TinyClaw、Moltis、ZeptoClaw）**  
过去 24 小时无活动，处于休眠或极低频迭代状态。


## 7. 值得关注的趋势信号

**信号一：可观测性与"静默失败"已超越功能本身成为用户第一诉求。**  
从 OpenClaw（#119557 节流无 flush）、NanoBot（#5266 百万 token 无声消耗）、IronClaw（#5552 泛化错误信息）、CoPaw（#6601 空响应不报错）、ZeroClaw（SOP 配置静默丢弃）到 Hermes（#79339 sync_turn 静默丢失）——**"悄悄失败"正在系统性消耗用户信任**。这对所有 AI 智能体开发者的启示是：任何错误路径都需要显式、可操作的反馈机制，而非静默降级。

**信号二：安全加固从"可选项"变为"基础设施"。**  
记忆投毒防护（OpenClaw #7707）、API 密钥隔离（NanoBot 3 个 P0/P1 安全 PR）、子进程凭据泄漏（Hermes #77164）、MCP stdio 白名单（Hermes PR #62808）、文件系统访问控制（OpenClaw PR #60981）、存储加密（ZeroClaw #1）——安全维度正在从社区自发诉求上升为项目竞争力分水岭。**安全能力强的项目（NanoBot、ZeroClaw）正在获得用户信任溢价。**

**信号三：Agent 间通信（A2A）与互操作性成为下一波浪潮的种子。**  
ZeroClaw 的 A2A RFC、OpenClaw 的 agent-scoped budgets、CoPaw 对 MCP 新规范的支持——它们各自从不同角度（协议、资源隔离、工具调用）指向同一方向：**自主智能体正在从"独立个体"演化为"协作网络"**。开发者应密切关注 A2A 标准进展，这对未来多 Agent 系统架构设计将产生深远影响。

**信号四：多模型容灾能力成为生产部署的刚需。**  
PicoClaw（#3200）、CoPaw（fallback 机制）、LobsterAI（per-model token）、Hermes（Grok 对齐）、OpenClaw（DeepSeek 兼容问题）——多个项目在同一周期内独立涌现多模型容灾需求，说明**单一模型依赖已成为生产环境的最大的单点故障**。对开发者而言，建设模型无关的抽象层和自动降级链路不再是可选项。

**信号五：升级/迁移安全是规模化部署的隐形门槛。**  
NanoClaw #3194（无回滚保障）、OpenClaw #119263（DB 迁移失败阻断启动）、ZeroClaw #9779（文档与实现脱节）、LobsterAI #1198（重启状态不可见）——**升级事故正在成为用户流失的核心原因之一**。维护者应将升级安全（事务性迁移、可回滚、清晰的状态反馈）提升到与功能开发同等的优先级。

---

*报告基于各项目 2026-08-07 公开 GitHub 数据，由 AI 自动生成，仅供技术决策参考。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报

**日期**: 2026-08-07 | **数据窗口**: 过去 24 小时


## 1. 今日速览

NanoBot 项目今日保持高活跃度：24 小时内产生 9 条 Issue 更新和 17 条 PR 更新，其中 8 条新开 Issue 中有 5 条集中在 Matrix 频道行为与 Session 数据一致性问题；PR 方面 5 条已合并/关闭（含 2 条 WebUI 功能 PR 和 1 条 Matrix 兼容性修复），12 条待合并 PR 中有 2 条标注为 P0/P1 优先级（会话数据保护、API Key 泄露修复）。安全与数据完整性是本轮 PR 提交的核心焦点，共 3 条 PR 明确涉及密钥隔离与存储安全。无明显阻塞性问题，项目合并节奏稳定，健康度良好。


## 2. 版本发布

过去 24 小时无新版本发布。但值得关注的是，多条已合并 PR（如 Matrix join 修复、WebUI 交互优化、冷启动性能优化）尚未进入正式 release，建议维护者考虑在近期规划一个 patch 版本。


## 3. 项目进展

今日合并/关闭的 5 条 PR 中，3 条为功能性修复、2 条为 WebUI 改进，从不同维度推进了项目的完善度：

- **[#5248] fix(matrix): 修复 Continuwuity 兼容性**（已合并，P2）— 解决了 nio 库 `Api.join()` 发送空 POST body 导致部分 homeserver（Continuwuity）拒绝请求的问题。该修复直接关联并关闭了 Issue #5247。对于 Matrix 频道用户而言，这意味着从"无法自动入房"到"正常工作的关键修复"，尤其是使用非 Synapse 实现的用户。  
  https://github.com/HKUDS/nanobot/pull/5248

- **[#5261] feat(webui): 侧边栏会话拖拽**（已关闭）— 实现了两重拖拽交互：将侧边栏会话拖入输入框生成结构化提及（@会话），以及拖拽调整会话顺序（类 Codex 插入线）。该 PR 虽未合并，但为 WebUI 交互提供了重要设计参考。  
  https://github.com/HKUDS/nanobot/pull/5261

- **[#5267] fix(webui): 收紧交互动效**（已合并）— 统一 WebUI 过渡动画为 220ms，缩短完成状态保持时长，并确保 reasoning 折叠面板展开/收起时内容不抖动。改善了感知上的响应速度，属于体验打磨型改动。  
  https://github.com/HKUDS/nanobot/pull/5267

- **[#5262] perf(webui): 减少冷启动加载体积**（已合并，P1）— 为生产环境 WebUI 静态资源生成预压缩 gzip 兄弟文件并在网关层协商，同时将 React 共享运行时从 Markdown 渲染、代码高亮、KaTeX 等懒加载块中剥离。附带构建时回归检查，防止体积反弹。对低带宽/高延迟网络环境下的首次加载有明显提升。  
  https://github.com/HKUDS/nanobot/pull/5262

- **[#5259] fix(webui): 临时会话仅存内存**（已合并）— 强化了临时会话（Temporary Chat）的契约：会话状态只存在于进程内存中，不写入 session 历史、WebUI 转录或自动记忆。源于 #5252 的栈上拆分的独立 PR，明确了临时会话的数据边界。  
  https://github.com/HKUDS/nanobot/pull/5259


## 4. 社区热点

今日讨论热度最高的议题集中在 **会话模型切换限制** 和 **子代理导致 cron 任务提前终止** 两个问题上：

- **[#5198] 无法在特定会话中切换模型**（3 条评论）— 用户 whisperity 反馈：Nanobot 始终以配置的默认模型为最高优先级，附加模型仅作 fallback。点击聊天输入框旁的模型标识无法切换（与主流 SaaS AI 不同），`/model` 命令使用其他模型 ID 也似乎无效。该问题已存在一周仍无 PR 关联，可能触及会话模型绑定机制的核心设计。  
  https://github.com/HKUDS/nanobot/issues/5198

- **[#4290] cronjob 遇子代理过早结束**（2 条评论）— 用户 tjc0726 报告：cron 任务派生子代理后，主 agent 在子代理完成后没有机会处理其结果，导致后续工作流失败。该问题自 6 月 10 日提出至今近两个月仍开放，是长期未解决的痛点，涉及异步任务编排的核心逻辑。  
  https://github.com/HKUDS/nanobot/issues/4290

- **[#5276] 会话级临时文件隔离需求**（1 条评论）— whisperity 提出的改进建议——即便启用了 `restrictToWorkspace` 和 bwrap 沙箱，`~/.nanobot/workspace` 仍是所有会话共享的全局读写目录。用户希望在多会话隔离场景下能有更细粒度的控制。  
  https://github.com/HKUDS/nanobot/issues/5276

此外，**Matrix 频道行为** 在今日形成了议题簇：#5274（回复功能未使用）、#5275（thread 应形成独立上下文）、#5247（自动入房已修复）。三者共同指向同一诉求——Matrix 频道的交互模式应向 Discord/Slack 对齐。


## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue/PR | 描述 | 状态 |
|--------|----------|------|------|
| **P0** | [#5271] fix(session): 阻止过期后台任务覆盖会话数据 | `/new` 后，持有旧 Session 引用的后台任务可能在 await 窗口后保存过期数据，覆盖新会话。已提供修复 PR，待合并 | PR 待合并 |
| **P1** | [#5269] fix(providers): API 密钥写入进程级 os.environ | 多 provider 环境下密钥被 gateway 覆盖或首个写入者胜出，导致凭据串用。修复 PR 已提交，待合并 | PR 待合并 |
| **P1** | [#5270] fix(cli): CLI 子进程泄露 API 密钥 | `env=os.environ.copy()` 将全部密钥传递给不可信子进程。修复 PR 已提交，待合并 | PR 待合并 |
| **P2** | [#5273] 会话裁剪丢弃主动频道投递消息 | `retain_recent_legal_suffix` 或 `enforce_file_cap` 裁剪时删除 cron 通知等 `_channel_delivery` 消息，导致用户侧信息缺失。对应修复 PR #5272 已提交 | PR 待合并 |
| **P2** | [#5264] 媒体根目录外附件缺失 media_urls | WebSocket 实时消息有 `media_urls`，但历史端点 `GET /api/sessions/{key}/messages` 不会为 `projects/` 下的附件生成签名 URL，刷新后附件丢失。对应修复 PR #5268 已提交 | PR 待合并 |
| **P2** | [#5265] 工具参数接受 NaN/Infinity 浮点值 | `Tool._cast_value()` 通过 `float()` 接受 `"NaN"` 和 `"Infinity"` 字符串，非法数值可传递至下游工具。修复 PR 已提交 | PR 待合并 |
| — | [#5263] 微信协议投递/流式/登录加固 | 对齐 `@tencent-weixin/openclaw-weixin` 2.4.6 协议头、QR 验证挑战、业务错误解析、重试感知 HTTP 状态处理等 | PR 待合并 |


## 6. 功能请求与路线图信号

| 需求 | 来源 | 对应 PR/状态 | 分析 |
|------|------|-------------|------|
| **Temporary Chat 模式** | Re-bin 的 PR #5252 + #5259 | 功能已基本成型，#5259 已合并 | 多轮对话但持久性为零。若 #5252 合入，将直接对标 ChatGPT 临时对话能力 |
| **会话级文件隔离** | whisperity 的 Issue #5276 | 暂无对应 PR | 涉及会话安全模型，短期内实现可能性较低，但值得纳入路线图讨论 |
| **模型切换交互改进** | whisperity 的 Issue #5198 | 暂无对应 PR | 高频痛点（3 条评论，一周未解决），建议优先处理 |
| **响应式模型预设详情面板** | Re-bin 的 PR #5277 | 待合并 | 宽屏并排编辑，窄屏列表-详情流——纯粹的 WebUI 响应式增强 |
| **共享交互式项目终端** | chengyongru 的 PR #5253 | 待合并，标注 conflict | WebUI 与 agent 共享 PTY 终端（xterm.js），涉及 POSIX/Windows ConPTY 双平台——功能强大但复杂度高 |
| **mst-python 元搜索提供商** | goodtiding5 的 PR #5234 | 待合并 | 聚合 DuckDuckGo/Google/Brave/Bing 等多引擎并用 RRF 融合排序，搜索覆盖面质变 |
| **闲置会话归档供 Dream 处理** | Maaayhan 的 PR #5231 | 待合并 | 解决短会话不产生 `history.jsonl` 导致 Dream 无输入的问题 |


## 7. 用户反馈摘要

- **会话模型切换是真实痛点**（#5198）：用户明确表示"点击模型 blip 无法切换"与"Cloud SaaS AIs 的 UI 不同"，这不是配置问题而是交互设计缺口。用户尝试使用 `/model` 命令也无效，说明该问题的 root cause 在会话状态对模型的绑定逻辑而非 UI 层。  
  https://github.com/HKUDS/nanobot/issues/5198

- **Matrix 回复语义缺失**（#5274/#5275）：用户期望 bot 使用 Matrix 的 reply 功能来回应用户的消息、thread 应形成独立上下文——用户的参照系是 Discord 和 Slack 的成熟实现。当前 Nanobot 在 Matrix 上"总是以顶层消息回复"，在复杂讨论场景中会造成上下文混乱。  
  https://github.com/HKUDS/nanobot/issues/5274  
  https://github.com/HKUDS/nanobot/issues/5275

- **token 消耗透明度不足**（#5266）：用户报告 2 小时内消耗约百万 token 且无明显用户活动，要求"清晰记录每次调用的 token 消耗量与时机"。这不仅是可观测性问题，更可能暗示存在无效循环调用或重试机制缺陷。  
  https://github.com/HKUDS/nanobot/issues/5266

- **cron + 子代理工作流可靠性**（#4290）：主 agent 无法处理子代理结果导致工作流断裂——该 issue 已存在近两个月，至今仍无 PR 关联和官方回应，是社区中积压最久的未响应问题之一。  
  https://github.com/HKUDS/nanobot/issues/4290


## 8. 待处理积压

- **[#4290] cronjob 子代理导致提前结束**（2026-06-10 提出，近 2 个月无响应）— 这是积压最久的未解决 Bug，影响自动化工作流的可靠性，建议优先排查：主 agent 在子代理完成后是否有继续对话的机制。  
  https://github.com/HKUDS/nanobot/issues/4290

- **[#5198] 会话内模型切换不可用**（2026-07-31 提出，一周无 PR 关联）— 高频交互痛点，3 条评论仍无官方回应。建议至少确认该行为是设计如此还是 Bug。  
  https://github.com/HKUDS/nanobot/issues/5198

- **[#5266] token 消耗缺少日志**（2026-08-06 提出）— 百万级 token 消耗在 2 小时内无声发生，可能存在未预期的后台循环。建议优先排查是否与 cron/子代理机制相关。  
  https://github.com/HKUDS/nanobot/issues/5266

- **P0/P1 PR 待合并提醒** — 以下三项涉及数据安全，建议优先审阅合并：  
  1. https://github.com/HKUDS/nanobot/pull/5271 （会话数据被过期任务覆盖）  
  2. https://github.com/HKUDS/nanobot/pull/5269 （API 密钥进程环境串用）  
  3. https://github.com/HKUDS/nanobot/pull/5270 （CLI 子进程密钥泄露）


> **编辑注**：本期日报数据窗口内存在若干 Issue 与 PR 的主题联动（如 #5273 对应 PR #5272、#5264 对应 PR #5268、#5247 对应 PR #5248），说明维护者对 Issue 的响应速度正在加快。但由于今日无 release 发布，各修复尚处于待合并阶段，建议关注后续合入节奏。


</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-07

## 1. 今日速览

过去24小时内，Hermes Agent 仓库保持高度活跃：共产生 50 条 Issue 更新和 50 条 PR 更新，其中有 4 个 PR 被合并/关闭，2 个 Issue 被关闭。当前有 46 个 PR 等待合并，积压量较大。值得关注的是，仓库在 2026-08 月初启动了**全仓库范围的 god-file 分解（sharding）重构 Epic**，多个相关 Issue 和 PR 正在推进，同时存在一批 Feishu（飞书）平台命令审批按钮的系统性 Bug（多个 Issue 指向同一根因，且有修复 PR 等待合并）。无新版本发布。

---

## 2. 版本发布

**无** — 过去 24 小时没有新版本发布。

---

## 3. 项目进展

过去 24 小时共有 4 个 PR 被合并/关闭，亮点如下：

- **PR #80422 [CLOSED]** — `Fireworks user agent`（作者：rob-maron）
  已关闭的针对 Fireworks 提供程序的 user-agent 修复。未合并，可能需要重新提交。
  链接：https://github.com/NousResearch/hermes-agent/pull/80422

- **PR #80702 [CLOSED]** — `fix(desktop): render agent reactions live`（作者：fangliquanflq）
  修复桌面端 agent 消息反应（emoji reactions）无法实时渲染的问题，并将更新路由到运行时的权威会话状态。已关闭（可能已合并）。
  链接：https://github.com/NousResearch/hermes-agent/pull/80702

- **PR #80699 [CLOSED]** — `The desktop's tools reach it on remote and cloud backends too`（作者：OutThisLife）
  修复桌面端工具（浏览器、面板、消息反应等）被 `HERMES_DESKTOP` 环境变量错误限制的问题。已关闭（可能已合并）。
  链接：https://github.com/NousResearch/hermes-agent/pull/80699

项目整体向前推进的方面包括：**桌面端连接稳定性和工具可用性**（远程/云后端现在可以使用桌面工具）、**UI 实时渲染**（agent 消息反应无需刷新即可看到）、以及 **Slack 消息投递可靠性**（PR #76818 处于待合并状态）。

---

## 4. 社区热点

今日讨论最活跃的 Issue 集中在以下三个方向：

### 4.1 全仓库 god-file 分解 Epic（重构）— 社区最热议话题
- **Issue #78647** — `Epic: Shard all 20 god files — repo-wide god-file decomposition`（评论 51 条）
  作者：andrexibiza | 链接：https://github.com/NousResearch/hermes-agent/issues/78647
  这是仓库级的**长期重构纲领**：将所有超过阈值的"上帝文件"拆分为清晰模块，并明确"只拆分，不回归"的硬性政策。该 Epic 衍生出多个子任务（如 #78645 agent/context_compressor.py、#78637 hermes_cli/auth.py、#78792 telegram adapter.py），表明项目正在系统性改善代码可维护性。

### 4.2 Feishu（飞书）平台命令审批按钮 — 多个重复 Issue 汇聚
- **Issue #13924** — `Feishu: Command Approval buttons return "出错了，请稍后再试 code: 220340"`（评论 6 条）
  链接：https://github.com/NousResearch/hermes-agent/issues/13924
- **Issue #25886** — `[Bug]: Feishu/Lark card authorization buttons fail with error 200343`（评论 4 条）
  链接：https://github.com/NousResearch/hermes-agent/issues/25886
- **Issue #38305** — `Feishu error 200340 persists in v0.15.2 - PR #10256 needs merge`（评论 3 条）
  链接：https://github.com/NousResearch/hermes-agent/issues/38305
- **Issue #10073** — `[Feishu Mobile] Command approval card returns error code:200340`（评论 3 条）
  链接：https://github.com/NousResearch/hermes-agent/issues/10073

**分析**：Feishu 平台的审批卡片按钮失效问题从 4 月被报告至今已有 4 个独立 Issue 指向同一/相关根因（`card.data` 解析错误），涉及不同版本（0.8.0、0.15.2、0.17.0）和不同错误码（200340/200343/220340）。社区用户已明确指出 PR #10256 是正确修复但未合并，存在**修复方案悬而未决**的风险。这是目前平台适配层面影响面最大的问题。

### 4.3 插件接口扩展（社区路线图）
- **Issue #64182** — `Tracking: Plugin Interface Expansion — community ideas, July 2026`（评论 27 条）
  作者：teknium1 | 链接：https://github.com/NousResearch/hermes-agent/issues/64182
  该问题聚合了 Discord 社区的插件接口扩展提案，是社区贡献者长期 PR 的参考蓝图。

---

## 5. Bug 与稳定性

### 严重（P1）
- **Telegram 致命断连导致消息投递失效** — Issue #80598（对应 PR #80700）: PR #80700 修复了 Telegram 在 fatal disconnect 后无法自动重连的问题，将可重试平台排队操作提前到断开前，避免重连 watcher 无目标可重试。
  PR: https://github.com/NousResearch/hermes-agent/pull/80700
- **Cron 任务丢失** — Issue #80624（对应 PR #80703）: 修复了 CLI 创建的 cron job 在 gateway 运行期间从 jobs.json 消失的问题。根因是跨进程 flock 降级，而非内存缓存。PR #80703 已在修复中。
  PR: https://github.com/NousResearch/hermes-agent/pull/80703
- **流式响应无总时长上限** — PR #80701: 新增流式响应总生命周期上限（默认 30 分钟），堵住了"滴灌式流"导致响应永不结束的缺口。
  PR: https://github.com/NousResearch/hermes-agent/pull/80701

### 较严重（P2）
- **桌面端底部操作面板消失（0.20.0 回归）** — Issue #79407（评论 8 条，标记 duplicate）: 0.19.0 升级到 0.20.0 后，桌面应用整个底部操作面板消失，应用退化为"仅查看外壳"。标记为 P2。由于被标记为 duplicate，需确认是否已由其他 Issue 跟踪。
  链接：https://github.com/NousResearch/hermes-agent/issues/79407
- **Memory provider sync_turn 回调静默丢失（0.20 回归）** — Issue #79339（评论 5 条）: 升级后 `sync_turn()` 不再被调用，外部记忆后端静默丢失完整的对话回合数据，无任何错误提示。
  链接：https://github.com/NousResearch/hermes-agent/issues/79339
- **`agent_context` 硬编码为 "primary"** — Issue #80646（评论 2 条）: 记忆提供者的上下文区分逻辑（cron/子代理/flush）成为死代码，可能导致上下文串扰。
  链接：https://github.com/NousResearch/hermes-agent/issues/80646
- **MCP stdio 桥接崩溃（args 为 null）** — Issue #80652（评论 2 条）: 当 MCP 配置中 `args: null` 时，桥接以 `TypeError` 崩溃并进入连接-暂停循环。
  链接：https://github.com/NousResearch/hermes-agent/issues/80652
- **Gatekeeper 凭据被丢弃** — Issue #79628（评论 3 条）: 工具配置 `use_gateway: true` 但网关认证失败时，直接报错而不会回退到已有的有效直连凭据。
  链接：https://github.com/NousResearch/hermes-agent/issues/79628

### 一般（P3）
- **Feishu 审批按钮系统性 Bug** — 详见第 4.2 节，多个 P2/P3 Issue 持续开放。
- **child-process 环境变量泄漏** — Issue #77164（评论 4 条）: 环境变量清洗基于名称形状启发式，非凭据形状的已应用密钥会泄漏到子进程。
  链接：https://github.com/NousResearch/hermes-agent/issues/77164
- **/retry 删除已归档的压缩历史** — PR #80695: `rewrite_transcript()` 默认删除了所有会话行（包括 `active=0` 的软归档压缩轮次）。
  PR: https://github.com/NousResearch/hermes-agent/pull/80695
- **桌面端远程会话消息反应不可用** — Issue #80259（评论 2 条）: `HERMES_DESKTOP` 仅在本机设置，导致远程桌面/Cloud 后端下消息反应功能被禁用（对应 PR #80699 已修复）。
- **IMAP/SMTP 登录用户硬编码为 EMAIL_ADDRESS** — Issue #41331（评论 3 条）: 自定义邮件域别名场景下无法单独指定登录用户名。
  链接：https://github.com/NousResearch/hermes-agent/issues/41331

---

## 6. 功能请求与路线图信号

### 明确纳入路线图的信号
- **流式响应总生命周期上限**（PR #80701，P2）: 为流式响应增加默认 30 分钟的总时长上限，防止无限"滴灌"流。已提交 PR，目标明确。
  PR: https://github.com/NousResearch/hermes-agent/pull/80701
- **Telegram 菜单可清除 + agent_passthrough_commands**（PR #80627，P3）: 为 Telegram 平台增加自定义菜单清除能力和代理直通命令（如 `/start`），面向客户服务机器人场景。
  PR: https://github.com/NousResearch/hermes-agent/pull/80627
- **捆绑 `grill-me` 技能**（PR #80708）: 新增对抗性计划面试技能，在编写代码之前通过结构化的一问一答压力测试想法。
  PR: https://github.com/NousResearch/hermes-agent/pull/80708

### 社区呼声较高的功能请求
- **插件接口扩展**（Issue #64182，评论 27 条）: 社区的插件接口扩展蓝图，覆盖社区贡献者长期等待的 PR。
- **桌面端本地 token/成本分析**（Issue #77221，评论 5 条）: 核心已有完整的计量数据（输入/输出 token、成本等），但桌面端无任何展示界面。
  链接：https://github.com/NousResearch/hermes-agent/issues/77221
- **成本分析增强（3 个相关 Issue）**: 包含汇总视图中的 included/estimated/unknown 成本桶（#77223）、按天聚合的 token/成本时间序列（#77222）等。
- **MCP stdio 命令白名单**（PR #62808，P3）: 可选的、默认关闭的 MCP stdio 命令白名单机制，防止任意二进制执行（安全增强）。
  PR: https://github.com/NousResearch/hermes-agent/pull/62808
- **Cron 按任务投递 profile**（Issue #70849，评论 2 条）: 多路复用网关场景下，希望 cron 任务可指定使用的 adapter profile。
  链接：https://github.com/NousResearch/hermes-agent/issues/70849

---

## 7. 用户反馈摘要

- **Feishu 审批按钮（多个 Issue）**：用户反馈在 Feishu 上点击命令审批卡片中的任何按钮（Allow Once/Session/Always/Deny）都会收到错误提示（200340/200343/220340），必须手动输入 `/approve session` 等命令作为替代方案。该问题影响移动端和桌面端，且从 v0.8.0 到 v0.15.2 一直存在，社区对修复 PR 长期未合并表示不满。

- **桌面端面板丢失（Issue #79407）**：用户指出 0.19.0 → 0.20.0 升级后，底部操作面板（含 Command Center、Gateway 控制等）完全消失，应用沦为"仅查看外壳"。这是一个严重影响可用性的回归问题。

- **Memory provider sync_turn 静默丢失（Issue #79339）**：用户反馈升级到 0.20 后，外部记忆后端的 `sync_turn()` 不再被调用，对话回合不再同步到记忆系统，且毫无报错，难以察觉。

- **MCP 配置容错（Issue #80652）**：用户配置 MCP 服务时 args 为 null 导致崩溃并持续循环重连，期望更宽容的配置校验或更明确的错误提示。

- **桌面端远程后端工具缺失（PR #80699）**：用户反馈桌面客户端连接远程网关（非 Electron 启动的后端）后，浏览器面板、消息反应等 6 个工具不可用——原因是它们被 `HERMES_DESKTOP=1` 错误地门控。

- **学习图误标外部技能（Issue #80596）**：用户反馈通过 `npx skills add` 安装的外部技能被学习图标记为"已学习"（use_count 虚增），扭曲了技能使用统计。

---

## 8. 待处理积压

### 高优先级（需尽快关注）
- **Feishu 审批按钮修复 PR #10256** — 已被多个 Issue（#38305、#10073、#13924、#25886）引用为正确修复，但长期未合并。建议维护者尽快审查。
  链接：https://github.com/NousResearch/hermes-agent/pull/10256

- **God-file 分解 Epic（Issue #78647，6 天前创建，51 条评论）** — 全仓库重构的纲领性 Issue，已衍生多个子任务。涉及范围甚广（agent、cli、telegram adapter 等 20 个文件），建议维护者尽快确认资源分配与排期。
  链接：https://github.com/NousResearch/hermes-agent/issues/78647

- **Grok/xAI 功能对齐 campaign（Issue #80424，2 天前创建，9 条评论）** — 提出将 Hermes 的 Grok/xAI 接入面与官方 xAI 开发平台全面对齐（Chat/Responses、推理、流式、Imagine 生图、语音/TTS），范围大且涉及多个子系统，需要决策。
  链接：https://github.com/NousResearch/hermes-agent/issues/80424

### 长期未响应（需关注）
- **Feishu 卡交互问题（Issue #7675，创建于 2026-04-11，已近 4 个月）** — 报告了 Feishu 平台的 3 个问题（卡交互被当作 `/card` 命令、审批按钮无效、流式卡回复支持），近期有更新但状态仍为 OPEN。
  链接：https://github.com/NousResearch/hermes-agent/issues/7675

- **Gateway run.py 拆分（Issue #55138，创建于 2026-06-29）** — gateway/run.py 达 858KB，请求拆分为独立平台路由模块。讨论不多（5 条评论），但代码规模本身说明问题紧迫。
  链接：https://github.com/NousResearch/hermes-agent/issues/55138

- **安全增强：MCP stdio 命令白名单（PR #62808，创建于 2026-07-11，近 1 个月未合并）** — 明确的安全增强（防止任意二进制执行），标记为 P3 但影响安全边界。建议优先审查。
  PR: https://github.com/NousResearch/hermes-agent/pull/62808

- **Shutdown forensics 误报（Issue #61003，创建于 2026-07-08）** — 每次 gateway 启动都报假的 "Stale systemd unit" 警告，影响用户体验。
  链接：https://github.com/NousResearch/hermes-agent/issues/61003

---

**总结**：项目整体处于高活跃状态，重构方向明确（god-file 分解持续推进），桌面端和网关稳定性在快速改善。但需注意 3 个风险点：Feishu 平台审批按钮问题修复积压过久、46 个 PR 待合并积压量偏高、桌面端 0.20 存在回归问题（面板丢失、widget缺失、memory sync_turn 静默失效）。建议优先处理 Feishu 审批按钮修复、桌面端回归、P1 流式响应上限和 cron 任务丢失问题，并关注 PR 合并节奏。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期：2026-08-07** | **数据来源：github.com/sipeed/picoclaw**

---

## 1. 今日速览

PicoClaw 项目今日活跃度处于**中低水平**：过去24小时无新 Issue 提交或关闭，PR 方面有2条更新（1条待合并、1条已关闭）。值得关注的是，编号为 #3200 的 PR 已持续开放超过一个月，近期获得更新，涉及模型默认回退链的可配置化功能，属于 Web UI 和 API 层面的重要增强；另一条 #1349 在本周期内关闭，为 QQ 频道多附件类型支持的功能扩展。过去24小时内无新版本发布。整体来看，项目处于**功能迭代期而非高速活跃期**，核心维护者可能正在集中处理 #3200 的代码审查与合并前准备工作。

---

## 3. 项目进展

**今日合并/关闭 PR:** 1 条

### [PR #1349] feat(qq): 支持解析和回复更多附件类型（已关闭）
- **作者:** aishannon | **创建:** 2026-03-11 | **关闭:** 2026-08-06
- **链接:** https://github.com/sipeed/picoclaw/pull/1349
- **内容摘要:**
  1. 支持解析 QQ 频道 emoji 结构
  2. 支持处理来自 QQ 频道的语音、图片、视频和文件消息
  3. 支持回复本地语音、图片、视频和文件附件（发送前先上传）
  4. 优先使用 Markdown 消息进行回复，失败时降级...

**分析:** 该 PR 经历了近5个月的开发周期后关闭，为 QQ 渠道补齐了多媒体消息处理能力，显著提升了 QQ 生态内的用户体验。考虑到当前渠道类的完整度仍是聊天机器人框架竞争的核心指标，此功能对项目在中文社区中的适用性有实质性帮助。建议维护者在后续 release 中确认此变更是否已包含在主线分支中。

---

## 4. 社区热点

**当前最受关注条目：**

### [PR #3200] feat(models): 添加可配置的默认回退链（OPEN）
- **作者:** lc6464 | **创建:** 2026-07-01 | **最后更新:** 2026-08-06
- **链接:** https://github.com/sipeed/picoclaw/pull/3200
- **关注点:** 开放超过一个月仍保持活跃更新，评论数未显示但持续被更新

**背后的诉求分析:** 该 PR 为模型页面引入"默认回退链"工作流，允许用户设置默认模型、添加备用模型、调整链顺序并持久化到后端 API。这反映了社区对**多模型容灾和灵活切换**的强烈需求——当主模型不可用或响应异常时，用户希望系统能自动降级到备用模型，而不是手动切换。这是生产环境部署中的常见痛点，若被合并，将显著增强 PicoClaw 在真实业务场景中的稳定性。

---

## 5. Bug 与稳定性

**今日无新报告的 Bug、崩溃或回归问题。**

> 注意：过去24小时无新 Issue 提交。需要提醒的是，项目此前可能存在未关闭的稳定性相关 Issue，但不在今日新增范围内。

---

## 6. 功能请求与路线图信号

### 信号一：可配置模型回退链（高优先级信号）
- **来源:** PR #3200（开放中）
- **链接:** https://github.com/sipeed/picoclaw/pull/3200
- **判断:** 该功能涉及 Web UI + 后端 API 的完整链路，且作者持续在更新，大概率会被纳入下一版本。对于多模型策略管理的需求方（如企业用户），这是值得期待的功能。

### 信号二：QQ 渠道多媒体支持（已实现）
- **来源:** PR #1349（已关闭）
- **链接:** https://github.com/sipeed/picoclaw/pull/1349
- **判断:** 功能已完成并关闭，预计会随下一个正式版本发布。对于依赖 QQ 机器人做文件分发、语音交互的社区用户，这是一个重要能力补全。

---

## 7. 用户反馈摘要

今日无新增 Issue 评论可供提炼，基于近期 PR 和 Issue 趋势，用户关注点集中在：

- **多模型管理体验:** 用户期望在 UI 层直接配置模型优先级与降级策略，而不是通过配置文件或代码修改（参考 PR #3200）
- **渠道丰富度:** QQ 渠道从纯文本扩展到多媒体消息，用户对"可发送文件/图片/语音"的需求强烈（参考 PR #1349）

---

## 8. 待处理积压

暂无长期未响应的高优先级 Issue 需要特别提醒。

值得关注的是 **PR #3200** 已开放超过一个月（2026-07-01 至今），建议维护者尽快安排审查或明确回复作者是否准备合并，以避免社区贡献者流失。该 PR 涉及面较广（前端 + 后端），若需调整建议尽早给出具体反馈。

---

*本日报由 AI 分析师自动生成，基于 PicoClaw GitHub 仓库公开数据分析，仅供项目社区参考。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-08-07

## 1. 今日速览

NanoClaw 项目今日保持中等偏上的活跃度，24 小时内共有 2 条 Issue 更新和 14 条 PR 更新，其中 8 条 PR 已合并或关闭，6 条等待合并。值得关注的是，社区焦点从功能添加开始转向**质量加固**：今日核心事件是 `glifocat` 报告了 `/update-nanoclaw` 在无恢复点的情况下误报成功的 bug（#3194），并同步提交了修复 PR #3195。此外，多个长期遗留的 PR（如 #2213、#2644、#2678、#2679、#2873）在今日集中关闭，暗示维护者正在系统性地清理积压。整体项目健康度良好，核心维护者在响应社区反馈方面表现积极。

## 2. 版本发布

过去 24 小时内无新版本发布。


## 3. 项目进展

今日有 8 条 PR 被合并或关闭，涉及多个领域的修复与改进：

**Telegram 媒体消息处理（#2213，已关闭）**
由 ziv-daniel 提交，修复了用户发送无文字说明的图片、视频或文件时消息被静默丢弃的问题。根因是 `chat-sdk-bridge.ts` 中 `onNewMessage` 处理器的正则匹配导致纯媒体消息无法通过验证。此为社区用户长期等待的修复，从 5 月初创建至今历时 3 个月才被合并。

**调度系统三连修复（#2644、#2643、#2678、#2679，均已关闭）**
yairixStudio 提交的系列修复显著增强了调度模块的健壮性：
- #2678：修复永久失败后的重复调度无法重新触发的问题
- #2679：将永久失败的任务通过 agent 主动通知用户，而非仅记录日志
- #2644：修复 Telegram 中回复机器人自身消息时的 `isReplyToBot` 检测
- #2643：修复直接 @提及/DM 时未触发关键词 pattern 的问题

**技能更新机制重构（#2873，已关闭）**
glifocat 将 `pre-flight` 与凭据检查拆分，使 `/update-skills` 可以刷新技能代码而无需重新验证凭据。这为后续 #3195 的事务性升级奠定了基础。

**用户 ID 命名空间修复（#2591，已关闭）**
mmahmed 修复了用户 ID 命名空间方式，将冒号分隔改为渠道类型前缀，避免跨渠道用户 ID 冲突。

**Qodo/Google MCP 技能清理（#3172，已关闭）**
glifocat 移除了依赖于外部未配置 SaaS 服务的 Qodo 和 Google MCP 技能（对应 Issue #3171），降低了新用户开箱即用时的困惑。


## 4. 社区热点

**热点一：Issue #3194 — `/update-nanoclaw` 误报成功（新建，glifocat）**
- 链接：[Issue #3194](https://github.com/nanocoai/nanoclaw/issues/3194)
- 该 Issue 指出升级操作在验证通过前就切换了运行中的代码，回滚点仅保护 Git 而不覆盖 SQLite 数据库、gitignore 配置及外部组件变更，存在四个失败窗口。
- 作者同时提交了对应修复 PR #3195。考虑到作者是核心团队成员，这更像是内部主动暴露并修复问题，而非外部用户踩坑后的反馈。

**热点二：Issue #3171 — Qodo 技能依赖未配置的外部服务（已关闭，glifocat）**
- 链接：[Issue #3171](https://github.com/nanocoai/nanoclaw/issues/3171)
- 该 Issue 指出内置的 `get-qodo-rules` 和 `qodo-pr-resolver` 技能依赖 `~/.qodo/config.json` 中的 API key，但仓库中没有任何配置流程。此问题与 PR #3172 的清理工作形成闭环。

**热点三：PR #3190 — Tavily MCP 搜索工具技能（新建，manisrinivasan2k1）**
- 链接：[PR #3190](https://github.com/nanocoai/nanoclaw/pull/3190)
- 作为 Utility skill 提交，为 NanoClaw 增加 Tavily 搜索能力。这是社区贡献的体现，目前评论较少但值得关注。


## 5. Bug 与稳定性

**严重：升级误报成功且无回滚保障（Issue #3194，修复中）**
- 链接：[Issue #3194](https://github.com/nanocoai/nanoclaw/issues/3194)
- `/update-nanoclaw` 在更新通过验证前即切换运行目录，回滚仅保护 Git，SQLite 数据库、Git-ignored 配置及外部组件变更存在丢失风险。四个失败窗口在 `main` 分支上均存在。
- 已有对应 fix PR：[PR #3195](https://github.com/nanocoai/nanoclaw/pull/3195)，标记为 `core-team`，正在进行事务性升级改造。

**中等：Qodo 技能功能失效（Issue #3171，已关闭）**
- 链接：[Issue #3171](https://github.com/nanocoai/nanoclaw/issues/3171)
- 由外部依赖缺失导致技能欺骗性地拦截正常编码请求。已通过移除技能解决（PR #3172）。

**中等（已修复）：纯媒体消息被静默丢弃（PR #2213，已关闭）**
- 链接：[PR #2213](https://github.com/nanocoai/nanoclaw/pull/2213)
- Telegram 渠道中无文字说明的图片/视频/文件被直接丢弃，用户无法感知。修复已合并。

**中等（已修复）：回复机器人自身消息时无法识别（PR #2644，已关闭）**
- 链接：[PR #2644](https://github.com/nanocoai/nanoclaw/pull/2644)
- Telegram 中回复机器人自身消息时，`isReplyToBot` 无法正确设置为真，导致机器人无法识别用户的直接指令。


## 6. 功能请求与路线图信号

**技能更新机制完善：** PR #2873（拆分 pre-flight 与凭据验证）和 #3195（事务性升级）表明项目正在强化技能的动态更新能力，为更频繁的技能分发铺路。

**Tavily 搜索集成（PR #3190）：** 社区成员提交了 Tavily MCP 工具作为 Utility skill，若被采纳将扩展 NanoClaw 的事实检索能力。

**媒体消息处理增强（PR #2213）：** 合并后，聊天界面在处理图文混排消息时更加可靠，为后续富媒体交互（如 PR #3193 的 Telegram Chat SDK 升级）创造条件。

**OPA 网关绕行（PR #2705，待合并）：** 此 PR 修复了 `use-native-credential-proxy` 技能无法真正绕过 OneCLI 网关的问题，涉及系统集成层面，合并后有助于优化部署场景中的凭据管理体验。


## 7. 用户反馈摘要

- **用户对开箱即用体验敏感**：Issue #3171 表明用户对“内置技能隐含外部服务依赖”这一设计非常不满，认为“nothing sets up”的技能不应出现在默认分发中。维护者已通过移除技能的方式快速解决。
- **升级安全关切强烈**：Issue #3194 对更新流程的批评直接且细致，指出现有回滚策略“protects Git, but not the SQLite database”是明显的设计缺口。核心团队在 24 小时内响应并提交修复，体现了良好的用户信任度。
- **社区对"长期不合并"有耐心但有限度**：PR #2213 从 5 月 3 日创建到 8 月 6 日合并，历时 3 个月。期间用户反复提交新版本触发 CI，最终合并时社区表达了正面反馈但仍存在“为什么这么久”的合理质疑。


## 8. 待处理积压

**PR #2705 — `use-native-credential-proxy` 网关绕行修复（已开放 61 天）**
- 链接：[PR #2705](https://github.com/nanocoai/nanoclaw/pull/2705)
- 创建于 6 月 7 日，至今未合并。修复了技能实装后无法真正生效的问题。此问题影响真实部署场景，建议维护者评估后决定合并或关闭。

**PR #3149 — `groups config add-mount` 的 `--rw` 标志（已开放 9 天）**
- 链接：[PR #3149](https://github.com/nanocoai/nanoclaw/pull/3149)
- 涉及 CLI 功能补全，目前评论为空，等待维护者或社区 review。

**PR #3186 — 技能能力主机接入点（已开放 3 天）**
- 链接：[PR #3186](https://github.com/nanocoai/nanoclaw/pull/3186)
- zvi-fried 提交的重构，为技能拥有的能力添加 host seams。属于架构改进，虽然目前无评论，但对于后续技能生态发展可能具有基础性作用。

---

> 报告生成时间：2026-08-07 | 数据来源：[NanoClaw GitHub 仓库](https://github.com/nanocoai/nanoclaw) | 下次更新：2026-08-08

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-07

## 1. 今日速览

IronClaw 项目昨日保持高强度迭代节奏：24小时内 GitHub 活跃度极高，共产生 50 条 Issue 更新和 50 条 PR 更新，其中新开/活跃 Issue 27 条、待合并 PR 33 条。昨日发布 v1.1.0 稳定版（首个自 1.0.0 以来的正式版本），标志着扩展生态（MCP 注册、IronHub 深度链接、跨渠道文件附件）的阶段性成熟。当前 Issue 积压以 QA bug-bash 为主（P1/P2 级），集中在 Slack 投递、Routine 调度与运行稳定性三大块，项目健康度处于**高迭代、高积压**状态，需关注长期未关闭的 P1 缺陷。


## 2. 版本发布

### ironclaw-v1.1.0（2026-08-06）

**发布要点**：首个自 1.0.0 以来的稳定版本，基于 `1.1.0-rc.1` 并合入其后的修复。核心特性聚焦"扩展触达"：

- 注册任意托管的 MCP 服务器
- 通过 IronHub 深度链接安装
- 持久的文件附件，支持跨渠道传递
- Slack 集成改进（发布说明被截断，未显示完整内容）

**破坏性变更**：发布说明中被截断，未显示破坏性变更说明。建议用户查阅完整 Release Notes 确认。

**迁移注意事项**：文档中未见显式迁移指南。由于涉及 MCP 注册与 Slack 行为变更，建议实例管理员重点验证现有 Slack 投递目标配置与自定义 MCP 集成兼容性。


## 3. 项目进展

**核心推进（昨日合并/关闭）** ：

| PR | 说明 | 影响 |
|---|---|---|
| [#7235](https://github.com/nearai/ironclaw/pull/7235) | **Operator 检查 API 与实时流** — 为运维人员新增诊断快照、提示词检查、工具详情读取与实时诊断流（已关闭，与 Issue #7220 对应） | 为运维可观测性奠定基础 |
| [#7259](https://github.com/nearai/ironclaw/pull/7259) | **修复 docs/ 公开泄漏** — 冻结 `.mintignore` 并添加 CI 门禁，防止内部文档被公开站点访问 | 安全边界加固 |
| [#7289](https://github.com/nearai/ironclaw/pull/7289) | **修复 libSQL FTS 查询** — 解决自然语言召回缺陷（#7275），在生产路径上验证跨对话持久记忆 | 核心记忆功能稳定性修复 |
| [#7303](https://github.com/nearai/ironclaw/pull/7303) | **Docker 镜像安装 curl** — 修复健康检查导致节点状态 error 的问题 | 部署稳定性修复 |

**当前最重要开放 PR**：

- [#7236](https://github.com/nearai/ironclaw/pull/7236) + [#7239](https://github.com/nearai/ironclaw/pull/7239) + [#7277](https://github.com/nearai/ironclaw/pull/7277)：Inspector 调试面板、提示词检查、模型调用统计（XL 级，risk: low）
- [#7157](https://github.com/nearai/ironclaw/pull/7157)：**显式渠道投递工具** — 双通道模型（会话生命周期 + 通知渠道），删除启发式投递逻辑，直击多个 Slack 投递 bug
- [#7300](https://github.com/nearai/ironclaw/pull/7300)：**修复 Slack 个人 DM 投递** — 恢复 OAuth 后个人投递目标，并在工作区不匹配时 fail-closed
- [#7288](https://github.com/nearai/ironclaw/pull/7288)：libSQL FTS 的自然语言安全化（生产缺陷修复）

整体而言，项目正通过 PR #7157 与 #7300 系统性解决 Slack 投递问题；#7220/#7235/#7236 系列则开辟了运维检查（Inspector）新能力线。


## 4. 社区热点

**讨论热度最高**：

- **[#5553](https://github.com/nearai/ironclaw/issues/5553) Approval 通知丢失**（评论 4，P2）：审批通知在通知历史中消失，用户无法追溯需审批的自动化任务。与 #5522 的 retry loop 问题形成呼应，反映**审批流可靠性**是用户核心痛点。
- **[#5702](https://github.com/nearai/ironclaw/issues/5702) GitHub 集成 HTTP 403**（评论 4，P2）：issue 搜索/创建全面失败，属于集成可用性的 P2 阻塞。
- **[#5522](https://github.com/nearai/ironclaw/issues/5522) Reborn 例程缺少 Slack DM 读取能力**（评论 3）：QA 发现能力缺失导致任务失败并进入 `capability_info` 重试循环，暴露 Agent 能力声明与实际执行间的 gap。

**背后诉求**：社区（QA+用户）对**跨渠道通信的可靠性**（Slack 投递、DM 读取）与**运行可见性**（活动面板不更新、日志深链接需两次点击）最为关注。Inspector 系列 PR 是官方对该方向的回应。


## 5. Bug 与稳定性

按严重程度排列：

**P1（严重）** :

| Issue | 问题 | 状态 |
|---|---|---|
| [#5456](https://github.com/nearai/ironclaw/issues/5456) | Routine 运行因 runner lease 过期而失败（90 秒不活动阈值过严，影响多工具例程） | 开放，无 fix PR |
| [#5877](https://github.com/nearai/ironclaw/issues/5877) | Slack 通知发送给错误用户 — 敏感结果投递错误 | **已关闭** |
| [#5504](https://github.com/nearai/ironclaw/issues/5504) | Routine 创建挂起无响应 | **已关闭** |
| [#3533](https://github.com/nearai/ironclaw/issues/3533) | Telegram 无法从 UI 自动设置 | **已关闭** |

**P2（主要）** :

| Issue | 问题 | Fix PR |
|---|---|---|
| [#5836](https://github.com/nearai/ironclaw/issues/5836) | 定时 Routine 每次运行报 "No thread attached"（0% 成功率） | 无直接 fix，待 [#7157](https://github.com/nearai/ironclaw/pull/7157) 可能缓解 |
| [#5701](https://github.com/nearai/ironclaw/issues/5701) | 活动面板隐藏工具详情且不实时更新 | [#7305](https://github.com/nearai/ironclaw/pull/7305) 仅软化失败徽标，非完整修复 |
| [#5834](https://github.com/nearai/ironclaw/issues/5834) | Agent 错误拒绝 Slack 断开请求 | 无 |
| [#5707](https://github.com/nearai/ironclaw/issues/5707) | Routine 创建响应暴露内部实现细节 | 无 |
| [#5522](https://github.com/nearai/ironclaw/issues/5522) | Slack DM 读取能力缺失 + capability_info 重试循环 | 无 |
| [#5552](https://github.com/nearai/ironclaw/issues/5552) | 多工具失败后仅显示泛化 "invalid result" 错误 | 无，与 [#5776](https://github.com/nearai/ironclaw/issues/5776) 同源 |
| [#5508](https://github.com/nearai/ironclaw/issues/5508) | 显示 "无 Slack 投递目标" 但实际已连接 | [#7300](https://github.com/nearai/ironclaw/pull/7300) 待合并 |
| [#5509](https://github.com/nearai/ironclaw/issues/5509) | 聊天创建延迟随历史记录增长 | 无 |
| [#5776](https://github.com/nearai/ironclaw/issues/5776) | 长输出导致模型超时并退化为泛化错误 | 无 |
| [#5702](https://github.com/nearai/ironclaw/issues/5702) | GitHub 集成 403 | 无 |

**P3（轻微）** ：

- [#5510](https://github.com/nearai/ironclaw/issues/5510) 无法删除旧例程、[#5557](https://github.com/nearai/ironclaw/issues/5557) 日志深链接需开两次、[#5704](https://github.com/nearai/ironclaw/issues/5704) 图片预览透明化、[#5705](https://github.com/nearai/ironclaw/issues/5705) 终端图标无法禁用、[#5706](https://github.com/nearai/ironclaw/issues/5706) 侧边栏显示原始线程 ID — 均已被本期关闭。


## 6. 功能请求与路线图信号

**新功能信号**：

| 功能 | 来源 | 状态判断 |
|---|---|---|
| **Inspector / 运维诊断** | [#7220](https://github.com/nearai/ironclaw/issues/7220) + PR #7235/#7236/#7239/#7277 | **已进入实现**，XL 级 PR 序列，或纳入 v1.2 |
| **显式渠道投递工具** | [#7157](https://github.com/nearai/ironclaw/pull/7157) | **已实现**，双通道模型（会话 + 通知），待合并，预计进入 v1.1.x 或 v1.2 |
| **Nostr 签名主机函数** | [#7184](https://github.com/nearai/ironclaw/pull/7184) | 新贡献者提交，为 WASM 工具增加 `nostr-sign-event` 等 3 个函数，XL 级，或进 v1.2 |
| **沙箱配置文件** | [#7214](https://github.com/nearai/ironclaw/pull/7214) | 显式 Docker 与 Railway 用户沙箱配置，明确租户+用户作用域，或进 v1.2 |
| **自定义 MCP 私有注册** | [#7253](https://github.com/nearai/ironclaw/pull/7253) | MCP 注册改为"仅定义、不安装"，强化隐私与可见性控制，或进 v1.2 |

**路线图信号**：Inspector（可观测性）、渠道投递（通信可靠性）、沙箱配置（部署灵活性）构成三条主线。v1.1.0 内的扩展生态 (MCP/深度链接/附件) 已稳定，下一版本大概率聚焦稳定性修复 + Inspector 完善。


## 7. 用户反馈摘要

- **"无法删除旧例程"**（[#5510](https://github.com/nearai/ironclaw/issues/5510)）：用户需"完全重启"才能清除旧例程，且残留例程继续使用旧配置运行，与 Slack 投递问题叠加导致混乱。
- **"Slack 明明已连接，却要求重新连接"**（[#5508](https://github.com/nearai/ironclaw/issues/5508)）：新建例程时提示"无投递目标"，但旧例程仍能正常投递 — 配置可见性与实际状态脱节。
- **"审批通知闪一下就没了"**（[#5553](https://github.com/nearai/ironclaw/issues/5553)）：用户无法可靠追踪待审批事项，影响自动化工作流信任度。
- **"活动面板像黑盒"**（[#5701](https://github.com/nearai/ironclaw/issues/5701)）：运行期间无法实时查看工具调用细节，用户被迫等待运行结束才能排查。
- **"错误信息毫无帮助"**（[#5552](https://github.com/nearai/ironclaw/issues/5552) / [#5776](https://github.com/nearai/ironclaw/issues/5776)）：泛化 "invalid result" 掩盖了真实原因（工具失败、模型超时），用户无法自助定位。
- **正面反馈**：QA 测试环境（railway-staging）持续被用于问题复现，测试覆盖面较广；多数 P3 UI 瑕疵（透明图片、终端图标等）已在本期修复，UI 打磨在持续进行。


## 8. 待处理积压

**长期未关闭的高优先级 Issue**（超过 30 天未解决，P1/P2）：

| Issue | 创建时间 | 持续天数 | 说明 |
|---|---|---|---|
| [#5456](https://github.com/nearai/ironclaw/issues/5456) P1 | 2026-06-30 | 38 天 | Runner lease 过期导致 Routine 系统性失败 — **无 fix PR，需优先处理** |
| [#5508](https://github.com/nearai/ironclaw/issues/5508) P2 | 2026-07-01 | 37 天 | Slack 投递目标不存在但已连接 — [#7300](https://github.com/nearai/ironclaw/pull/7300) 待合并 |
| [#5509](https://github.com/nearai/ironclaw/issues/5509) P2 | 2026-07-01 | 37 天 | 聊天延迟随历史增长 — 前端性能问题，无 fix |
| [#5510](https://github.com/nearai/ironclaw/issues/5510) P3 | 2026-07-01 | 37 天 | 无法删除旧例程 — 功能缺失 |
| [#5702](https://github.com/nearai/ironclaw/issues/5702) P2 | 2026-07-06 | 32 天 | GitHub 集成 403 — 无 fix |
| [#5701](https://github.com/nearai/ironclaw/issues/5701) P2 | 2026-07-06 | 32 天 | 活动面板不更新 — 部分缓解，未根治 |
| [#5836](https://github.com/nearai/ironclaw/issues/5836) P2 | 2026-07-08 | 30 天 | "No thread attached" 系统性失败 — 与 #5507 同源 |

**提醒**：#5456（runner lease）是当前影响面最大的 P1，已积压 38 天。建议维护者将修复该问题纳入 v1.1.x 补丁或 v1.2 必须项，否则 Routine 功能的可靠性将持续受到质疑。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# 🦞 LobsterAI 项目日报 — 2026-08-07

> 数据周期：2026-08-06 ~ 2026-08-07 | 数据来源：GitHub Issues/PRs

---

## 1. 今日速览

过去 24 小时项目活跃度**中等偏低**：新增 5 条 Issue（其中 2 条为本日新开）、2 条 PR 更新（均为待合并），未发布新版本。值得关注的是，今日新开 Issue 全部为**真实用户反馈**（输入框编辑模式、SiliconFlow 模型 ID 兼容性 Bug、PowerShell 内核版本疑问），说明用户正基于实际使用场景提出诉求，社区互动质量较高。但需注意：**3 条 Issue 与 2 条 PR 已挂起超过 4 个月（标记为 stale）**，长期积压问题未得到维护者响应，项目维护活跃度存在隐患。


## 2. 版本发布

**无新版本发布。**

上次版本为 2026.8.5.0（Windows x64），今日 Issue #2443 中用户反馈的 Bug 仍存在于该版本。


## 3. 项目进展

**今日无 PR 被合并或关闭。** 当前有 2 个 PR 处于待合并状态，均已完成开发但存在阻塞因素：

| PR | 内容 | 状态 | 阻塞原因 |
|---|---|---|---|
| [#1197](https://github.com/netease-youdao/LobsterAI/pull/1197) | Agent 管理页面交互优化（删除操作改至侧边栏、UI 改进） | 待合并 | 与主分支存在冲突，需 rebase |
| [#1199](https://github.com/netease-youdao/LobsterAI/pull/1199) | 为模型添加 contextWindow/maxTokens 配置；持久化并在 Cowork/OpenClaw 配置中传播上下文元数据 | 待合并 | 无明确标注阻塞原因 |

**关键观察**：两个 PR 均创建于 2026-04-01，已悬置 4 个月。PR #1199 实现的功能（per-model token 设置）与今日新 Issue #2443（模型 ID 兼容性问题）在模型管理层面存在关联，若该 PR 能合入，可部分改善模型配置体验。

**项目整体进展缓慢**，近 24 小时无代码合并动作。


## 4. 社区热点

**今日社区讨论活跃度为低**，仅 2 条 Issue 收获评论（各 1 条），无高热度讨论。

- **[#1196](https://github.com/netease-youdao/LobsterAI/issues/1196)（强制生成 Agents.md 等 6 个文件）** — 评论者附和了作者诉求，补充了"全局 systemPrompt 添加"的具体应用场景（多项目共用一套 Agent 配置），进一步支撑了需求合理性。该 Issue 自 2026-04-01 以来持续被关注，说明默认文件生成策略确实影响了相当一部分用户的工作流。核心诉求是**自定义性与整洁性**，希望 LobsterAI 不要在每个工作目录强制生成系统文件——用户认为应像 Claude Code 那样支持全局配置文件，或至少将自动生成的文件放入隐藏目录。

- **[#1198](https://github.com/netease-youdao/LobsterAI/issues/1198)（网关重启状态不可见）** — 评论区为该请求增加了业界对标参考：[Zed 编辑器已实现“将 Activity Indicator 放入 Tab 中”的交互模式](https://zed.dev/channels)，可作参考。核心诉求是**操作透明度**——网关重启这类"等待型"操作，需要明确的进度反馈或状态指示，否则用户无法判断操作是否正常进行。同时该 Issue 还暴露了"浏览器已打开但服务不可用"的状态判定问题，可能涉及进程探测逻辑缺陷。


## 5. Bug 与稳定性

今日报告 Bug **1 条**，严重程度评估如下：

| 严重程度 | Issue | 描述 | 影响范围 | Fix PR |
|---|---|---|---|---|
| 🟡 中 | [#2443](https://github.com/netease-youdao/LobsterAI/issues/2443) | **模型 ID 含斜杠的自定义 Provider 无法在界面中使用**（SiliconFlow 用户，模型 ID 如 `deepseek-ai/DeepSeek-V4-Flash`）。添加 Provider 后模型出现在列表中但无法选择/启用，影响所有模型 ID 带斜杠的 OpenAI 兼容服务商 | 特定服务商（SiliconFlow 等） | ❌ 无 |

*另：[#1198](https://github.com/netease-youdao/LobsterAI/issues/1198)（网关重启进度条消失、状态不可见）出现于 4 月，今日仍无 Fix，可能涉及网关状态管理逻辑。*


## 6. 功能请求与路线图信号

今日新功能请求 **1 条**，另有 1 条长期未决的功能增强 PR：

- **[#2444 输入框编辑模式](https://github.com/netease-youdao/LobsterAI/issues/2444)**（本日新开）— 用户苦于长 Prompt 输入换行不便。提出两种方案：① 设置中切换 Enter/Ctrl+Enter 语义；② 输入框提供"编辑模式"开关，进入后输入框展开、回车换行、Ctrl+Enter 发送，可选支持 WYSIWYG Markdown 编辑。**该需求直指日常使用频率最高的交互组件——聊天输入框的可用性问题**，开发成本低（方案 ① 仅需增加一个设置项），建议优先评估。

- **[#1199 Per-model token 设置 PR](https://github.com/netease-youdao/LobsterAI/pull/1199)**（悬置 4 个月）— 实现 per-model 级 `contextWindow` 和 `maxTokens` 配置，持久化到模型列表，并在 Cowork/OpenClaw 配置中传播。该功能是 Model 配置精细化管理的重要一步，且今日新增 Issue #2443（模型 ID 兼容性）也指向模型管理模块，**建议尽快处理 PR 的合并阻塞，或将模型管理列为下个版本重点**。


## 7. 用户反馈摘要

| 来源 | 用户痛点 / 诉求 | 情绪 |
|---|---|---|
| [#1196](https://github.com/netease-youdao/LobsterAI/issues/1196) | "每次选不同工作目录都强制建 6 个文件，太乱了，删了还要重建，而且 agents 里一大堆东西" | 明显不满（×1 附和） |
| [#1198](https://github.com/netease-youdao/LobsterAI/issues/1198) | 网关重启缺乏进度反馈，后续对话全部提示"模型不可用"，无法判断状态 | 困惑、等待 |
| [#2443](https://github.com/netease-youdao/LobsterAI/issues/2443) | 添加 SiliconFlow 后模型无法在界面选择，功能可用但界面不可选 | 中性（Bug 反馈） |
| [#2442](https://github.com/netease-youdao/LobsterAI/issues/2442) | 质疑为何内核仍为 PS 5.1 而非 PS 7.4；自动提问给出推测性自查回答（Node 默认 shell 行为、兼容性兜底），反馈"自问自答"的场景 | 好奇、疑问 |

**值得注意**：Issue #2442 的摘要信息显示，LobsterAI 可能引入了"自动回答"机制（提问后自动附推测性解释）——这可能是新功能，也可能是用户在描述 AI 助手给出的预判答案，值得跟进确认。


## 8. 待处理积压 ⚠️

以下 Issue/PR 长期未响应，建议维护者优先关注：

| 类型 | 编号 | 标题 | 搁置时长 | 优先级建议 |
|---|---|---|---|---|
| PR | [#1199](https://github.com/netease-youdao/LobsterAI/pull/1199) | feat(model): add context window and token settings | 4 个月+ | 🔴 高 — 功能成熟且与当前模型管理诉求相关 |
| PR | [#1197](https://github.com/netease-youdao/LobsterAI/pull/1197) | Agent 管理页面交互优化 | 4 个月+ | 🟡 中 — 需解决分支冲突；UI 体验优化 |
| Issue | [#1198](https://github.com/netease-youdao/LobsterAI/issues/1198) | 网关重启进度丢失 + 状态误判 | 4 个月+ | 🟡 中 — 影响操作透明度，可能涉及状态管理 |
| Issue | [#1196](https://github.com/netease-youdao/LobsterAI/issues/1196) | 强制生成 6 个系统文件 | 4 个月+ | 🟢 待规划 — 社区有明确诉求，但无需紧急处理 |

**积压问题共同特征**：全部来自 4 月，说明 4 月之后维护者对社区输入的响应节奏明显放缓，建议检查项目维护资源分配。


## 📊 项目健康度评估

| 维度 | 评分 | 说明 |
|---|---|---|
| 社区活跃度 | ★★☆☆☆ | 24h 输入 7 条，多为新开，讨论少 |
| 维护响应度 | ★★☆☆☆ | 4 个月未合并 PR、未处理积压 Issue |
| 代码推进速度 | ★☆☆☆☆ | 今日 0 合并 |
| 用户反馈质量 | ★★★★☆ | 新 Issue 均有明确场景与可执行建议 |

**综合结论**：项目处于"用户持续反馈、维护响应滞后"的阶段。社区真实需求（输入框改进、模型配置优化）与已有 PR（#1199）高度吻合，但堵在合并环节。**建议将 PR #1199 与 Issue #2444 纳入同一迭代规划**，一次性解决模型配置与输入体验两块核心诉求。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

好的，我是您的 AI 智能体与个人 AI 助手领域开源项目分析师。以下是根据 CoPaw (github.com/agentscope-ai/CoPaw) 在 2026-08-07 的 GitHub 数据生成的项目动态日报。

---

# CoPaw 项目动态日报 | 2026-08-07

## 1. 今日速览

CoPaw 项目今日活跃度极高，社区反馈密集。过去 24 小时内，Issue 和 PR 的更新总量达到 84 条，显示出强劲的开发迭代速度和用户参与度。Issue 关闭率（17/34）与 PR 合并/关闭率（30/50）均处于健康水平，表明维护团队响应迅速。当前最突出的问题是围绕**长会话稳定性**（上下文窗口超限、空响应、工具调用状态错乱）和 **MCP 工具可靠性**的系列 Bug 报告，这已成为影响用户体验的主要矛盾。同时，多个关于记忆系统（Memory）和模型配置的 PR 正在推进，预示着下一阶段的功能重点。

## 2. 版本发布

- **无新版本发布。**
- **注意**: 多个 Issue 提及 `2.1.0b1` 和 `2.1.0b2` 测试版本，表明下一个重要版本（v2.1.0）正在积极开发中，但尚未正式发布。

## 3. 项目进展

今日合入主分支的关键 PR 显示了项目在稳定性和架构一致性上的投入：

- **[#6530] [已合并] Fix editable per-tool call limit names** ([链接](https://github.com/agentscope-ai/QwenPaw/pull/6530)): 修复了工具调用次数限制名称无法编辑的 UI 问题，并补充了回归测试。
- **[#6744] [已关闭] fix(config): harden agent config persistence on shared filesystems** ([链接](https://github.com/agentscope-ai/QwenPaw/pull/6744)): 增强了在 OSSFS/FUSE 等共享文件系统上 `agent.json` 配置写入的原子性，防止配置损坏。
- **[#6611] [已关闭] refactor(context): align Scroll and memory with AgentScope lifecycle** ([链接](https://github.com/agentscope-ai/QwenPaw/pull/6611)): 这是一次重要的架构重构，将 Scroll 收敛为唯一的上下文协议，并与 AgentScope 2.0 的 Agent 生命周期对齐，旨在从根本上解决状态恢复和自动记忆的不一致问题。

这些合并表明项目正在从“功能堆叠”转向“架构治理”，尤其关注上下文管理和配置持久化，是迈向更稳定 v2.1.0 版本的关键步骤。

## 4. 社区热点

- **[#6684] [已关闭] [Feature]: 增加频道的重试功能** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/6684)): 以 8 条评论成为今日讨论热度最高的 Issue。用户在使用自建 Matrix 时频繁遇到因服务启动竞态导致的连接失败，且无自动恢复机制，需要手动干预。这反映了用户对**Channel 连接健壮性**和**自愈能力**的强烈需求。
- **[#6588] [已关闭] [Bug]: `spawn_subagent` treats empty `batch` placeholders as batch mode** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/6588)): 6 条评论。讨论焦点在于 `spawn_subagent` 在处理空占位符时错误地切换到了批处理模式，导致单任务调用行为异常。这暴露了**参数处理和模式判断逻辑**的兼容性问题。
- **[#6601] [开放] [Bug]: QwenPaw 不报空响应错误** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/6601)): 5 条评论。该问题直指框架层缺陷：在长会话逼近上下文窗口上限时，模型返回空响应但 QwenPaw 不报错，导致会话“假死”。这与 #6700（超大工具输出）、#6726（400 错误）等问题共同构成了**长会话稳定性的核心痛点**。

**诉求分析**：社区热点高度集中在“可靠性”上——连接要可靠、上下文处理要可靠、错误反馈要清晰。用户对于“悄悄失败”或“无响应”的容忍度极低，这应是项目后续优化的首要方向。

## 5. Bug 与稳定性

今日报告的 Bug 可归纳为以下等级，其中 **P0 为高优先级**：

| 严重程度 | Issue | 问题描述 | 是否已有修复 PR |
| :--- | :--- | :--- | :--- |
| **P0** | [#6726](https://github.com/agentscope-ai/QwenPaw/issues/6726) | 长会话大量工具调用后，请求因 `tool` 消息与 `tool_calls` 不匹配而 400 报错，会话中断。 | 无 |
| **P0** | [#6700](https://github.com/agentscope-ai/QwenPaw/issues/6700) | 超大工具输出导致历史会话加载卡死，并可能触发上下文窗口超限。 | 无 |
| **P0** | [#6732](https://github.com/agentscope-ai/QwenPaw/issues/6732) | MCP 工具规律性失效（每隔数小时），需重启容器才能恢复，严重影响自动化。 | 无 |
| **P1** | [#6755](https://github.com/agentscope-ai/QwenPaw/issues/6755) | 跨天会话中模型对“今天”的日期/星期判断错乱，导致日程任务定错日期。 | 无 |
| **P1** | [#6768](https://github.com/agentscope-ai/QwenPaw/issues/6768) | Agent 在完成多步任务后进入死循环，会话被阻塞数小时。 | 无 |
| **P1** | [#6731](https://github.com/agentscope-ai/QwenPaw/issues/6731) | `execute_shell_command` 在模型传入 `sandbox_config` 参数时崩溃（`replace()` 报错）。 | 无 |
| **P2** | [#6756](https://github.com/agentscope-ai/QwenPaw/issues/6756) | `run_tool_batch` 工具在多个 agent 中报错 `No toolkit available in current context`。 | 无 |
| **P2** | [#6775](https://github.com/agentscope-ai/QwenPaw/issues/6775) | Malware Bytes 报毒（疑似误报），已导致用户卸载，需官方澄清以消除信任危机。 | 无 |

**稳定性总结**：今日集中报告的 Bug 指向一个核心问题——**在长会话、多工具、复杂上下文的压力测试下，QwenPaw 的稳定性存在明显短板**。这不仅影响用户体验，更可能对依赖自动化任务的用户造成实际损失（如#6755的错误日程）。这些问题的修复优先级应高于新功能开发。

## 6. 功能请求与路线图信号

结合今日的 Feature Request 和正在审核的 PR，可以窥见 v2.1.0 及未来的功能方向：

- **MCP 能力增强**：
  - **超时配置**: Issue [#6724](https://github.com/agentscope-ai/QwenPaw/issues/6724) 请求为 MCP 工具调用增加可配置的超时时间，防止单个工具卡死整个会话。这与 PR [#6659](https://github.com/agentscope-ai/QwenPaw/pull/6659)（模型 fallback 机制）和 PR [#6723](https://github.com/agentscope-ai/QwenPaw/pull/6723)（能力缓存过期）共同指向提升系统健壮性。
  - **新规范支持**: Issue [#6761](https://github.com/agentscope-ai/QwenPaw/issues/6761) 询问对 MCP 2026-07-28 无状态新规范的支持情况，这是一个重要的前瞻性信号。
- **记忆与上下文系统重构**：
  - **Embedding 配置**: PR [#6772](https://github.com/agentscope-ai/QwenPaw/pull/6772) 和 [#6771](https://github.com/agentscope-ai/QwenPaw/pull/6771) 是重提的 PR，旨在优化 ReMe 记忆的 Embedding 模型配置与验证流程，提升语义检索的质量和配置的易用性。这表明项目正在切实推进“Memory”相关的功能完善。
  - **元数据保持**: PR [#6759](https://github.com/agentscope-ai/QwenPaw/pull/6759) 试图在上下文生命周期中保留工具调用的额外元数据（如 Gemini 的 thought signatures），这意味着未来可能在高级推理模型上提供更好的支持。
- **用户体验细化**：
  - **多语言支持**: Issue [#6765](https://github.com/agentscope-ai/QwenPaw/issues/6765) 请求添加匈牙利语等更多欧盟语言。
  - **交互优化**: Issue [#6728](https://github.com/agentscope-ai/QwenPaw/issues/6728) 请求微信渠道的审批提示支持中文。Issue [#6736](https://github.com/agentscope-ai/QwenPaw/issues/6736) 和 [#6737](https://github.com/agentscope-ai/QwenPaw/issues/6737) 则对自动生成的会话标题提出了改进建议。

**结论**：除稳定性修复外，项目的主要精力正在投向 MCP 的深度集成优化、记忆系统的工程化，以及本地化体验的提升。这些方向符合 AI 助手走向生产环境的关键需求。

## 7. 用户反馈摘要

- **“长会话不可用”是最大的挫败感来源**：用户 `rerbin` 在 [#6601](https://github.com/agentscope-ai/QwenPaw/issues/6601) 中直指框架层缺陷；`bob-geek11` 在 [#6726](https://github.com/agentscope-ai/QwenPaw/issues/6726) 中描述了 20-30 轮工具调用后会话直接 400 失败的场景。这背后是用户对**高复杂度、长周期任务**的强烈需求与当前技术瓶颈之间的矛盾。
- **对“静默失败”零容忍**：多个用户反映问题在无任何错误提示的情况下发生，如 [#6601](https://github.com/agentscope-ai/QwenPaw/issues/6601) 的空响应和 [#6732](https://github.com/agentscope-ai/QwenPaw/issues/6732) 的 MCP 工具失效。用户需要明确的、可操作的状态反馈。
- **功能诉求直指痛点**：用户 `MCQSJ` 在 [#6684](https://github.com/agentscope-ai/QwenPaw/issues/6684) 中提出的“频道重试功能”并非新需求，而是对基础可靠性的呐喊。用户 `tecgic` 在 [#6700](https://github.com/agentscope-ai/QwenPaw/issues/6700) 中提出的“输出截断、历史分页”也是直接针对实际出现的卡死问题。
- **积极互动与热爱**：尽管面临诸多问题，仍有用户（如 `boktoday` 在 [#6775](https://github.com/agentscope-ai/QwenPaw/issues/6775) 中）表达了对项目的喜爱。功能请求（如 [#6765](https://github.com/agentscope-ai/QwenPaw/issues/6765) 的语言支持）也显示出用户群体的多样性。

## 8. 待处理积压

以下 Issue/PR 长期未获明确回应或进展，可能存在沟通或资源分配问题，提醒维护者关注：

- **[#6775] [开放] Malware Bytes 报毒** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/6775)): **创建于 2026-08-07，处于安全与信任的灰色地带**。用户已明确表示“在听到团队回复前将卸载”，尽管是潜在误报，但若不及时官方澄清，将直接损害项目声誉，优先级极高。
- **[#6612] [开放] 与 agentscope 2.0.4.post1 不兼容** ([链接](https://github.com/agentscope-ai/QwenPaw/issues/6612)): 已开放 7 天。这是一个环境依赖问题，可能导致用户因版本冲突无法使用新功能。需确认兼容策略。
- **[#6615] [开放] [PR] 修复损坏的 agent config** ([链接](https://github.com/agentscope-ai/QwenPaw/pull/6615)): 由 `first-time-contributor` 提交，已开放 7 天。该 PR 直接修复 #6612 中提到的配置加载问题，可能因贡献者身份或沟通问题未被及时处理，建议维护者积极回应以避免挫伤社区贡献热情。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，以下是基于ZeroClaw (github.com/zeroclaw-labs/zeroclaw) 2026年8月7日数据生成的日报。

---

# ZeroClaw 项目动态日报 | 2026-08-07

## 1. 今日速览
ZeroClaw 项目今日活跃度极高，尤其是在 Issue 和 PR 的讨论与更新上。过去24小时内，共有31条 Issue 更新和50条 PR 更新，但值得注意的是，**没有新版本发布**，且大部分 PR（45条）仍处于待合并状态。项目当前的焦点集中在 **v0.8.5 稳定版收尾**和 **v0.9.0 重大功能（安全、网关、A2A）的规划**上。社区讨论热度高，涌现出多个关于 **SOP（标准操作程序）功能缺陷**的详细报告，显示该模块虽是新功能但鲁棒性有待加强。

## 2. 版本发布
- 过去24小时内无新版本发布。
- 目前处于 **v0.8.5 有限每周稳定化**阶段（见 Issue #9459），该版本功能冻结已于8月4日结束，每周发布小版本。此外，v0.9.0 的破坏性变更和安全改进工作已在 #7432 跟踪器中规划。

## 3. 项目进展
今日有 **5个PR被合并/关闭**，其中几个是关键修复，推进了核心功能的稳定性和安全性：
- **[PR #9737] `fix(tools): enforce agent policy in pipelines`**：这是一个重要的安全修复，解决了 `execute_pipeline` 绕过每代理工具门控（confused deputy）的问题，通过强制在管道构建时应用代理的 `ToolAccessPolicy` 来修复此漏洞。**（关闭 Issue #7947）**
- **[PR #9329] `refactor(zerocode): derive slash commands from the shared command catalogue`**：这个重构将 ZeroCode 的斜杠命令统一到单一命令描述源，解决了多源不一致的问题。**（关闭 Issue #9172）**
- **[PR #8943] `fix(providers): exclude Nova 2 from Bedrock prompt caching`**：修复了 Bedrock Nova 2 模型因不支持 `cachePoint` 而报错的问题，通过在模型中禁止对该模型启用提示缓存来解决。**（关闭 Issue #8720）**

这些修复解决了从安全漏洞到配置困扰的多个问题，提升了项目的健壮性和用户信任度。

## 4. 社区热点
今日讨论最活跃的 Issue 集中在**RFC（征求意见稿）**和**治理流程**上，显示出社区对项目方向的高度参与：
- **[Issue #6808] RFC: Work Lanes, Board Automation, and Label Cleanup**（19条评论）: 这是一个已持续数月的治理RFC，旨在简化工作流程和标签体系，减少维护者负担，是目前社区讨论最持久的话题之一。
- **[Issue #8692] Maintainer decision queue for RFCs and design issues**（11条评论）: 作为维护者决策队列的跟踪器，反映了社区对 RFC 评审效率的关注，希望加速决策过程。
- **[Issue #9106] RFC: A2A outbound client (A2ATool)**（11条评论）: 社区对实现代理间互操作性（A2A）的**出站**能力呼声很高。当前只能被动接收，无法主动调用其他Agent，这被认为是 Agent 协作的关键缺口。

## 5. Bug 与稳定性
今日报告的 Bug 中，**SOP（标准操作程序）模块**的问题尤为集中，且严重度较高（多为 P1），表明该新功能的稳定性需要立即关注：
- **P1: [Issue #9786] 格式错误的 SOP.toml 被静默丢弃**：`sop list` 不显示，`sop validate` 报告成功，但实际未加载。这会造成用户配置错误但无法察觉，严重误导用户。
- **P1: [Issue #9779] 文档默认的 sops_dir 未被守护进程采用**：如果用户依赖文档中的默认路径，SOP 引擎将永远不会加载，功能“静默失效”。
- **P1: [Issue #9770] cron update 静默丢弃对声明式任务的修改**：修改命令、名称、计划等6个字段会被静默丢弃，存在数据完整性问题。
- **P1: [Issue #9784] 多步骤 SOP 运行中步骤中途被标记为失败**：且无审计事件，Agent 只会在下一步操作时才发现，导致状态不一致。
- **P1: [PR #9002] `fix(gateway): keep agent turns alive after viewer disconnect`**：修复了网关断开后 Agent 线程被错误取消的问题，目前仍开放中。
- **S2 (中等): [Issue #9763] 1Password 非阻塞加载测试的 Flaky 问题**：已由 PR #9764 修复（今日关闭）。

## 6. 功能请求与路线图信号
- **A2A Outbound Client (Agent 间主动交互)**：Issue #9106 作为 RFC 提出，社区强烈希望 Agent 能主动调用其他符合 A2A 标准的 Agent，而不仅仅是被动响应。此功能仍在讨论中，可能会进入 v0.9.0 的规划。
- **实时执行模式 (Live execution)**：PR #9214 实现了 `zeroclaw eval run --mode live`，允许在沙箱中对真实配置的模型提供者运行测试用例。这是一项增强功能，尚在待合并状态。
- **Telegram 群组会话改进**：PR #9772 提出了为共享群组会话添加 `per_user_session` 开关的需求，以解决多用户协作时上下文混乱的问题。
- **cron 任务可用性优化**：多个 Issue（#9672, #9796）指出 CLI 帮助文档中的示例无效，体验不佳，已有相关修复在进行中，但新的问题仍在被发现。

## 7. 用户反馈摘要
- **对安全问题的“零容忍”**：`[Issue #9328] verifiable-intent evaluates constraints without verifying the credential chain` 等安全问题被迅速标记为高风险（risk:high），社区报告者会提供详细的代码位置和攻击链，显示用户对安全非常重视。
- **对文档与实际行为不一致的挫败感**：多个 Issue（如 #9779, #9786）都直接指出“文档说应该有，但实际不工作”，这表明文档和实现之间存在明显脱节，严重影响了用户体验和对自己配置的信任度。
- **对功能缺陷的高容忍与详细反馈**：尽管 SOP 模块 bug 较多，但报告者都提供了**详尽的复现步骤、证据链接**，并且参与了深层代码分析（如 #9783 指出 `finish_run` 接受失败原因但并未记录）。这表明用户是深度使用者，对项目有很高期望并愿意贡献力量。

## 8. 待处理积压
以下是最早提出、讨论度高但目前仍需维护者关注并处理的积压项：
- **[Issue #1] XOR cipher provides no real encryption for stored secrets**：最初于2月14日创建的 CRITICAL 安全漏洞，至今状态为 `needs-author-action`。虽然是非常早期的 Issue，但该漏洞触及核心的静态密钥存储机制，长期未解决已积累多个社区评论，应被优先级重新评估。
- **大型功能 PR 等待审查**：如比较突出的 (PR #9203, #9214, #9222 等） 由 **@IftekharUddin** 提交的系列 **Eval 系统** 功能 PR（已被标记为 `needs-author-action`，但内容详实，风险值高）。这些 PR 旨在建立基线回归测试、LLM评判器等，如果被采纳，将极大提升项目的工程化程度。但它们已开放数周，需维护团队投入更多精力审查，否则可能成为长期滞留的“技术债”。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*