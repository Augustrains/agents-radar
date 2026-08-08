# OpenClaw 生态日报 2026-08-08

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-08 00:41 UTC

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

好的，作为一名 AI 智能体与个人 AI 助手领域开源项目分析师，根据您提供的 OpenClaw 项目 GitHub 数据，我为您生成了 2026-08-08 的项目动态日报。

---

# OpenClaw 项目动态日报 | 2026-08-08

## 1. 今日速览

今日 OpenClaw 项目活跃度极高，呈现出典型的“高吞吐、高压态势”。过去24小时内，Issue 与 PR 更新数量均达到 500 条的上限，表明社区参与度和问题反馈量巨大。项目当前处于紧张的 Bug 修复和稳定性攻坚阶段，大量高优先级（P0/P1）问题集中在**会话状态管理、数据丢失/损坏、内存泄漏及可靠性**方面。值得关注的是，一个名为 **"Code Mode frontier stack"** 的 12 层大型功能分支正在密集提交 PR，预示着重大的架构级功能更新即将落地。虽然今日无新版本发布，但维护者正在通过高频率的 PR 审查和合并来应对积压的 Issue，项目整体处于快速迭代与问题修复并行的活跃期。

## 2. 版本发布

- 无新版本发布。

## 3. 项目进展

尽管没有新版本发布，但今日的 PR 活动揭示了项目在多个关键方向的显著进展：

- **可靠性修复（PR #120087, #120119）**：针对 Slack Enterprise Grid 的消息路由和 QQBot 图片文件名编码问题提交了修复 PR。这些修复直接关系到消息投递的准确性和多媒体文件的完整性，是提升用户体验的关键步骤。
- **"Code Mode" 功能栈推进（PR #119892, #119833, #119813 等）**：由贡献者 `vincentkoc` 主导的一个 **12 层大型功能分支 "Code Mode frontier stack"** 正在密集提交。该栈涵盖从传输层（OpenAI/Anthropic）到可审计跟踪、命令执行核算等底层能力的全面改造。这表明项目正在为一项名为 "Code Mode" 的重大功能进行深度的架构重构和功能扩展，虽然风险较高（多个 PR 标记有兼容性和安全边界风险），但预示着未来强大的新能力。
- **开发者体验优化（PR #120388, #120391）**：Web UI 侧持续改进，包括在侧边栏显示自定义构建的提交年龄，以及修复活动错误高亮在后续执行成功后不消失的 UI 缺陷。

这些进展表明，项目不仅在修修补补，更在通过大型 PR 栈积极构建新功能，展现了良好的长期演进活力。

## 4. 社区热点

- **[#116277] DeepSeek v4 Flash silent reply failure** (128条评论, 已关闭)
  - **链接**: [Issue #116277](https://github.com/openclaw/openclaw/issues/116277)
  - **分析**: 这是今日讨论度最高的问题，被评为 "diamond lobster"。用户报告 DeepSeek v4 Flash 模型在特定情况下静默失败，不生成任何回复。尽管该问题已被关闭，但 128 条评论的讨论量表明“生成失败无反馈”是用户极为关注和恼火的痛点，社区对模型失败的可观测性和降级策略有很高要求。

- **[#91588] Gateway Memory Leak — RSS grows to 15.5GB** (22条评论, 打开中)
  - **链接**: [Issue #91588](https://github.com/openclaw/openclaw/issues/91588)
  - **分析**: 这是一个长期存在的 P0 级问题，网关进程内存泄漏最终导致 OOM 崩溃。22条评论虽不算多，但高投票（👍: 1）和 P0 的严重性使其成为社区焦点。用户对长时间运行后的稳定性表示担忧，这是影响生产环境部署的关键问题。

- **[#101290] CLI Startup Preflight Corrupts Live State DB** (14条评论, 打开中)
  - **链接**: [Issue #101290](https://github.com/openclaw/openclaw/issues/101290)
  - **分析**: 另一个 P0 级数据损坏问题。CLI 的健康检查命令在网关运行时可能损坏实时状态数据库，导致 "database disk image is malformed" 错误。该问题被评为 "diamond lobster"，表明数据安全是社区的底线，此类问题会严重影响用户信任。

## 5. Bug 与稳定性

今日报告的 Bug 主要集中在数据一致性、状态管理和资源泄漏方面，按严重程度排列如下：

- **P0 (严重)**
  - **[#119263] Agent DB v14->v15 migration fails** (6条评论): 数据库迁移失败导致网关无法启动。**已有相关 PR (#119778)**。
  - **[#118772] totalTokens inflation causes premature compaction (data loss)** (6条评论): 令牌计数错误导致对话过早压缩，造成数据丢失。**有相关 PR 跟进**。
  - **[#101290] CLI startup preflight can corrupt the live state DB** (14条评论): 健康检查损坏数据库，**暂无明确 fix PR**。
  - **[#91588] Gateway Memory Leak** (22条评论): 内存泄漏导致 OOM 崩溃，**暂无明确 fix PR**。

- **P1 (高)**
  - **[#119087] Gateway cold start regressed ~2.5x** (9条评论): 冷启动性能回归，影响轻量级容器环境。**暂无明确 fix PR**。
  - **[#116022] /new reuses stable session ID** (9条评论): 新会话无法恢复已废弃的 Codex 绑定。**暂无明确 fix PR**。
  - **[#119411] memory file watcher never reindexes** (5条评论): 内存文件监视器失效，索引停止更新。**暂无明确 fix PR**。
  - **[#117209] AuthProfileStoreUnreadable sticky** (6条评论): 认证状态错误后难以恢复。**暂无明确 fix PR**。

## 6. 功能请求与路线图信号

- **会话与记忆增强**
  - **[#45608] Pre-reset agentic memory flush** (11条评论): 用户希望在会话重置前，像压缩前一样执行记忆清洗，避免上下文丢失。这反映了用户对“无缝体验”的追求。
  - **[#99583] Intelligent Session Auto-Titling** (7条评论): 提议为会话自动生成智能标题，且能随主题变化重命名，提升会话管理效率。

- **平台集成与能力扩展**
  - **[#87325] Support Azure Foundry GPT Realtime Talk** (8条评论): 用户希望增加对 Azure Foundry Realtime 语音的支持，扩展部署选项。
  - **[#81061] Hook: before_route_inbound_message** (7条评论): 请求增加预路由钩子，以便在消息分配到会话前进行拦截，用于频道桥接/代理等高级场景。

- **可观测性与生命周期管理**
  - **[#13219] Per-model usage logging for cost tracking** (7条评论): 用户希望原生支持按模型的使用量日志，以便进行成本核算和模型优化。
  - **[#87362] Emit task flow lifecycle hook events** (5条评论): 建议向插件系统暴露任务流生命周期事件，增强插件的可观测性。

这些请求与正在开发的 **"Code Mode"** 大型功能栈（PR #119892 等）可能没有直接关联，但都指向了**更深层次的可扩展性、可观测性和用户控制力**，很可能成为后续版本的重要方向。

## 7. 用户反馈摘要

- **稳定性是核心痛点**: 多个高热度 Issue（如 #91588, #101290, #118772）都指向了内存泄漏、数据损坏、数据丢失等稳定性问题。用户在使用中面临进程崩溃、会话状态错乱和上下文丢失的困扰，这极大影响了他们对项目“可用于生产环境”的信心。
- **失败通知机制缺失**: Issue #116277 (DeepSeek 静默失败) 和 #90789 (claude-cli 无响应占位符) 揭示了共同的痛点：当 LLM 调用失败或没有输出时，用户端得不到清晰的反馈，而是陷入“沉默”或收到误导性的占位信息。用户强烈需要更可靠的错误传播和降级机制。
- **配置/集成复杂性**: 多个 Issue（如 #119333 Codex 工具暴露不一致, #118161 WhatsApp ack 配置文档错误）反映出配置项、文档和实际行为之间存在偏差，增加了用户的使用和学习成本。

## 8. 待处理积压

以下为长期未解决、可能阻碍用户升级或影响核心体验的重要问题，建议维护者优先关注：

- **[#91588] P0: Gateway Memory Leak** (创建于 2026-06-09): 存在超过两个月，导致生产环境 OOM，但至今无明确修复 PR。
  - **链接**: [Issue #91588](https://github.com/openclaw/openclaw/issues/91588)
- **[#101290] P0: CLI preflight corrupts state DB** (创建于 2026-07-07): 数据损坏类问题，风险极高。虽然后续可能有修复，但持续未关闭，需警惕。
  - **链接**: [Issue #101290](https://github.com/openclaw/openclaw/issues/101290)
- **[#85030] P1: MCP tools not injected into subagent sessions** (创建于 2026-05-21): 功能性缺陷，导致子代理无法使用配置的 MCP 工具，限制了扩展生态。该 Issue 有 10 条评论和 6 个 👍，社区影响面广。
  - **链接**: [Issue #85030](https://github.com/openclaw/openclaw/issues/85030)

---

## 横向生态对比

# 个人 AI 助手/自主智能体开源生态横向对比分析报告

**报告日期**: 2026-08-08  
**分析范围**: OpenClaw、NanoBot、Hermes Agent、PicoClaw、NanoClaw、IronClaw、LobsterAI、CoPaw、ZeroClaw 等 9 个活跃项目


## 一、生态全景

当前个人 AI 助手开源生态正处于**高吞吐、高压力的快速迭代阶段**。头部项目（OpenClaw、Hermes Agent、ZeroClaw、CoPaw）日均 Issue+PR 更新量达 100~1000 条，社区参与度极高，但普遍呈现 PR 合并速度跟不上提交速度的“审查瓶颈”现象。稳定性（数据损坏、内存泄漏、静默失败）是各项目共同的核心痛点，安全问题（会话隔离、密钥泄漏、命令逃逸）关注度显著上升。多项目同步推进大型功能栈（OpenClaw 的 Code Mode、Hermes 的 Kanban 编排、ZeroClaw 的 SOP 引擎、CoPaw 的 ReMe 记忆），显示生态正从“能用”走向“规模化可治理”。


## 二、各项目活跃度对比

| 项目 | Issues 更新 | PR 更新 | Release | 健康度评估 |
|------|------------|---------|---------|-----------|
| **OpenClaw** | 500（达上限） | 500（达上限） | 无 | ⚠️ 极高活跃但问题积压严重；P0 级内存泄漏 2 个月未修复 |
| **Hermes Agent** | 100 | 100 | 无 | ⚠️ 高活跃；4 个 P1 Bug 无修复 PR；Kanban 编排缺陷集中爆发 |
| **ZeroClaw** | 50 | 50 | 无 | ⚠️ 高活跃；10+ P1 问题；安全加固 PR 排队超 13 天 |
| **CoPaw** | 31 | 49 | v2.1.0-beta.2 | ✅ 活跃；Bug 响应快（当日出修复 PR）；Windows 升级问题突出 |
| **IronClaw** | 50 | 50 | 无 | ⚠️ 高活跃；Agent 幻觉问题成系统性风险；文档漂移严重 |
| **NanoBot** | 10 | 21 | 无 | ✅ 健康；PR 合并率 52%（11/21）；安全修复待合入 |
| **NanoClaw** | 0 | 10 | 无 | ✅ 稳定；8 个 PR 待合入，无新 Bug 报告 |
| **PicoClaw** | 4 | 14 | 无 | ⚠️ 中等活跃；12 条 PR 积压，最长等待 38 天 |
| **LobsterAI** | 7 | 7 | v2026.8.7 | ✅ 健康；Bug 反馈到修复 <24 小时 |
| **TinyClaw / NullClaw / Moltis / ZeptoClaw** | — | — | — | 无活动 |


## 三、OpenClaw 在生态中的定位

OpenClaw 是当前生态中**体量最大、社区最活跃**的项目，其 Issue 量（500 条上限）是第二位（Hermes/ZeroClaw）的 5 倍，社区讨论量（如单个 Issue 128 条评论）远超同类。技术路线上，OpenClaw 正向**深度架构重构**推进 —— 12 层 “Code Mode frontier stack” 大型 PR 分支涵盖传输层到命令执行核算，显示出从单体工具向**平台化/框架化**演进的野心。与之相比，同类项目的侧重点各有不同：NanoBot 聚焦 WebUI 和会话记忆优化，ZeroClaw 重安全策略和 SOP 自动化编排，CoPaw 强在多 Agent 协作与跨平台渠道。OpenClaw 的优势在于**社区规模和功能广度**，但这也意味着其稳定性短板（数据损坏、内存泄漏）的影响面更大，治理优先级更迫切。


## 四、共同关注的技术方向

| 技术方向 | 涉及项目 | 具体诉求 |
|---------|---------|---------|
| **稳定性/数据安全** | OpenClaw（内存泄漏 2 个月未修复）、Hermes（压缩丢弃工具链）、ZeroClaw（forbidden_paths 无效、预算失效）、CoPaw（空闲卡死、MCP 失效） | 内存泄漏、数据损坏/丢失、静默失败是跨项目共性痛点，直接影响生产环境可用性 |
| **安全加固** | Hermes（SSRF 防护、Unicode 注入）、NanoBot（会话沙箱隔离）、ZeroClaw（shell 逃逸、密钥泄漏）、PicoClaw（只读挂载） | 会话隔离、敏感文件保护、命令执行边界是安全关注焦点 |
| **会话/记忆管理** | OpenClaw（会话状态、记忆压缩）、NanoBot（归档与裁剪）、Hermes（跨平台上下文共享 #4335）、ZeroClaw（SOP 状态） | 跨会话/跨平台记忆一致性和可恢复性是普遍需求 |
| **成本可观测性** | OpenClaw（per-model 用量日志 #13219）、NanoBot（Token 消耗审计 #5266）、ZeroClaw（cost_usd 恒为 0）、IronClaw（Token 计算错误） | 用户对 Token 消耗透明度和成本控制有强烈诉求 |
| **可观测性/失败通知** | OpenClaw（静默失败 #116277）、LobsterAI（执行无反馈 #2447）、Hermes（工具链丢弃）、NanoClaw（失败文案泛化） | 失败时的明确反馈与可诊断性是用户底线需求 |
| **多渠道一致性** | Hermes（WhatsApp 对齐 #79890）、CoPaw（Telegram/微信）、PicoClaw（钉钉/微信图片）、NanoBot（Telegram/WhatsApp） | 跨渠道功能对齐是社区反复提及的诉求 |


## 五、差异化定位分析

| 项目 | 核心定位 | 目标用户 | 技术架构 |
|------|---------|---------|---------|
| **OpenClaw** | 全功能个人 AI 助手平台 | 开发者/技术爱好者，追求功能广度 | 模块化，支持多 Provider/渠道，大型功能栈持续演进 |
| **Hermes Agent** | 多代理协作与任务编排 | 需要复杂自动化工作流的团队/个人 | Kanban 任务编排、Profiles、Claude Code 集成 |
| **ZeroClaw** | 高安全性的自主智能体框架 | 安全敏感型用户（Raspberry Pi 用户、私有化部署） | Rust 实现，SOP 执行引擎，强大的安全策略体系 |
| **CoPaw** | 开箱即用的多 Agent 协作助手 | 非技术用户/团队协作场景 | 桌面端优先，ReMe 记忆增强，多通道接入 |
| **IronClaw** | 轻量级 Agent 网关 | 需要多渠道互联的用户 | 重工具发现优化、文档自动化验证 |
| **NanoBot** | 轻量可扩展的会话机器人 | 开发者/嵌入式/Web 应用 | 轻架构 + 插件生态，重点在 WebUI 和会话管理 |
| **NanoClaw** | 高扩展性渠道接入方案 | 多渠道渠道服务商/开发者 | ChannelAdapter 架构，Skill 即插即用 |
| **PicoClaw** | 低成本硬件上的 Go 实现 AI 助手 | 嵌入式/极客玩家（Raspberry Pi） | Go 语言，<10MB RAM，sub-second 启动 |
| **LobsterAI** | 桌面端 AI 协作工具 | 桌面用户/知识工作者 | Electron 桌面应用，Cowork 协作功能 |


## 六、社区热度与成熟度

**快速迭代阶段（功能与问题并存，PR 吞吐量大）**：
- **OpenClaw** — 日更新 1000 条，活跃度第一，但 P0 问题积压
- **Hermes Agent** — 日更新 200 条，Kanban 缺陷集中暴露，处于“压力测试期”
- **ZeroClaw** — 日更新 100 条，安全议题热度高，PR 合并率低
- **CoPaw** — v2.1.0-beta，迭代节奏快，功能扩展与回归修复并行
- **IronClaw** — 日更新 100 条，文档治理战役刚启动

**质量巩固阶段（功能稳定、合并率高）**：
- **NanoBot** — 合并率 52%，安全/稳定性问题已出现对应修复 PR
- **LobsterAI** — 每 2 天一个小版本，Bug 响应 <24 小时，健康度最高
- **NanoClaw** — 无新 Bug，PR 待合入 8 条，处于功能累积期

**低活跃/停滞**：
- **PicoClaw** — 中低活跃，PR 积压严重（最长 38 天）
- **NullClaw / TinyClaw / Moltis / ZeptoClaw** — 无活动


## 七、值得关注的趋势信号

### 1. 安全不再是“选配”，而是生存底线
ZeroClaw 的 `forbidden_paths` 失效、Hermes 的 SSRF 防护、NanoBot 的会话沙箱、CoPaw 的 ACL 白名单丢失 —— 安全问题已从个别项目的“加分项”变为跨项目的“必答题”。用户对 Agent 自主执行危险操作（`rm -rf`、shell 逃逸）的容忍度为零。**参考价值**：新项目需将安全策略（隔离、审批、审计）纳入架构设计，而非事后补充。

### 2. “静默失败”是用户流失的第一杀手
OpenClaw 的 DeepSeek 静默失败获得 128 条评论、LobsterAI 的“执行无反馈”、Hermes 的“工具链被丢弃无提示”、NanoClaw 的“失败文案泛化” —— 当 Agent 出错但不告知用户时，用户的信任崩塌最为严重。**参考价值**：失败通知机制、错误日志可读性、降级策略是 UX 的核心组成部分。

### 3. Token 成本可观测性成为刚需
多个项目的用户都开始追问“Token 去哪了”（NanoBot 百万 Token 无感消耗、ZeroClaw cost_usd 恒为 0、IronClaw 计费错误）。当 AI Agent 从“玩具”变为“生产工具”时，成本透明度和预算控制是不可回避的运营需求。**参考价值**：内置按模型/会话/项目的 Token 计量与审计能力将越来越重要。

### 4. 记忆与状态管理是架构分水岭
OpenClaw 的 Code Mode 功能栈（12 层 PR）、CoPaw 的 ReMe 记忆增强、NanoBot 的会话归档、Hermes 的跨平台上下文共享 —— 各头部项目正不约而同地加大对记忆系统的投入。记忆的持久化、跨会话、跨平台一致性将成为下一阶段竞争的关键技术制高点。**参考价值**：架构设计时需早做记忆层的抽象与隔离。

### 5. 多代理协作尚处于“能用但不可控”阶段
Hermes 的 Kanban 编排遭遇系统性缺陷（僵尸进程、任务弹跳、预算耗尽），ZeroClaw 的 SOP 引擎存在卡死和静默失败，OpenClaw 亦面临会话状态管理挑战 —— 多代理自动化的“行为不可预测性”是当前最大的工程挑战。**参考价值**：多代理编排需要内置护栏（预算上限、心跳、超时熔断、审计追踪），否则复杂场景无法可靠落地。

### 6. 桌面端成为兵家必争之地
OpenClaw 有桌面 Web UI、CoPaw 有独立桌面包体（但 Windows 升级问题频发）、Hermes 有 Windows 桌面端（TUI 崩溃、黑屏）、LobsterAI 是纯桌面应用 —— 桌面端体验（安装、升级、复制粘贴、稳定性）是影响用户留存的关键路径，Windows 兼容性问题尤为突出。**参考价值**：桌面端投入需同步覆盖 Windows 安装器、更新机制、安全软件误报处理等“非核心但致命”的细节。

### 7. 硬件低成本化催生新场景
PicoClaw 的目标是“$10 硬件、<10MB RAM、sub-second 启动”，ZeroClaw 社区有大量 Raspberry Pi 用户 —— 低成本硬件上的 AI Agent 正在形成独立的分支场景（家庭自动化、边缘计算），其优化思路（轻量架构、低内存占用）与云端方案截然不同。**参考价值**：设计时考虑分层资源消耗，低配置环境也是潜在用户群。

---

*数据来源：各项目 GitHub 仓库 2026-08-08 公开数据；分析为 AI 自动生成，仅供参考。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-08

---

## 1. 今日速览

过去 24 小时 NanoBot 项目保持高度活跃：共产生 **10 条 Issue 更新**（8 条活跃、2 条已关闭）和 **21 条 PR 更新**（10 条待合并、11 条已合并/关闭），无新版本发布。社区围绕 **会话数据隔离（Session Isolation）** 和 **WebUI/渠道稳定性修复** 两条主线展开密集讨论与开发，安全相关话题（会话历史存放位置、沙箱隔离）成为焦点。值得关注的是，多个涉及底层架构安全的 PR（#5279、#5283）与对应 Issue（#5278、#5276）同日出现，表明维护团队正在系统性地回应社区对隐私和隔离性的关切。整体项目健康度良好，PR 合并效率高（11/21 已合入），但 Token 消耗异常的 Issue（#5266）尚未有对应修复方案，值得重点关注。

---

## 2. 版本发布

无新版本发布。

---

## 3. 项目进展

今日共有 **11 个 PR 被合并或关闭**，覆盖多个模块，核心推进方向如下：

### 🗄️ 会话保留与归档（Session Retention & Archiving）

- **[#5272] fix(session): preserve proactive channel delivery during session retention trimming**（[链接](https://github.com/HKUDS/nanobot/pull/5272)） — 修复 `retain_recent_legal_suffix` 和 `enforce_file_cap` 在裁剪会话历史时误删 `_channel_delivery` 主动消息（如 cron 通知）的问题，解决了对应 Issue #5273。
- **[#5280] fix(memory): archive short idle sessions for Dream**（[链接](https://github.com/HKUDS/nanobot/pull/5280)） — 修复短空闲会话因受保护后缀窗口限制而无法生成 `history.jsonl`、导致 Dream 无法处理的缺陷。
- **[#5231] feat(memory): archive idle sessions for Dream**（[链接](https://github.com/HKUDS/nanobot/pull/5231)） — 合并了为 Dream 归档空闲会话的功能（该 PR 于 8/3 发起，今日合入）。

### 🖥️ WebUI 前端优化

- **[#5277] feat(webui): expand model preset editor inline**（[链接](https://github.com/HKUDS/nanobot/pull/5277)） — WebUI 模型预设编辑器改为行内展开式交互，提升可用性。
- **[#5281] fix(webui): keep activity text crisp while fading edges**（[链接](https://github.com/HKUDS/nanobot/pull/5281)） — 修复活动区域边缘淡出时文字模糊问题，通过渐变遮罩替代合成层。
- **[#5285] fix(webui): preserve newly created topic route**（[链接](https://github.com/HKUDS/nanobot/pull/5285)） — 修复新建会话路由在乐观更新与真实列表确认之间的竞态。
- **[#5284] refactor(webui): remove legacy session messages route**（[链接](https://github.com/HKUDS/nanobot/pull/5284)） — 移除无调用方的旧版 `/api/sessions/{key}/messages` 路由及关联冗余代码。

### 📱 渠道层修复

- **[#5263] fix(weixin): harden protocol delivery, streaming, and login**（[链接](https://github.com/HKUDS/nanobot/pull/5263)） — 微信渠道协议头、投递重试、登录验证等多项加固。
- **[#5287] fix(channels): preserve global progress defaults**（[链接](https://github.com/HKUDS/nanobot/pull/5287)） — 修复渠道未显式覆盖时全局 `sendProgress`/`sendToolHints` 默认值被改变的问题。

### 🧩 其他

- **[#5282] fix: modernize dependency recovery guidance**（[链接](https://github.com/HKUDS/nanobot/pull/5282)） — 文档更新：将 Langfuse/Olostep/WeChat 的直接安装指南替换为 `nanobot plugins enable` 标准命令。
- **[#5268] fix(webui): stage out-of-media-root attachments on history reads**（[链接](https://github.com/HKUDS/nanobot/pull/5268)） — 修复历史记录读取时媒体根目录外附件丢失 `media_urls` 的问题（对应 Issue #5264）。

> **评估**：今日合入 PR 数量可观，且呈"修复一批、重构一批"的节奏。WebUI 和会话记忆模块获得显著打磨，项目正处于**稳定性和体验优化的密集迭代期**。

---

## 4. 社区热点

### 🔥 热点一：Token 消耗异常（高关注度）

**Issue #5266** — [Logs about token consumption (too many tokens are burned)](https://github.com/HKUDS/nanobot/issues/5266) — 作者报告"两小时烧掉约百万 Token 且用户无感知活动"，获得 **10 条评论**，为今日最高。核心诉求：
- 希望系统记录**每次调用的 Token 消耗明细**（时间、调用方、消耗量）
- 要求增加 Token 审计日志能力，以便定位"隐形消耗"

**分析**：该 Issue 反映出生产环境中成本可见性的强烈需求。建议维护者关注与 **可观测性（Observability）** 相关的基础设施建设，这可能是下一阶段的重要功能方向。

---

## 5. Bug 与稳定性

按严重程度排序：

| 严重程度 | Issue/PR | 简述 | 状态 |
|---------|----------|------|------|
| 🔴 高 | [#5266](https://github.com/HKUDS/nanobot/issues/5266) | 大量 Token 被无感知消耗 | ⚠️ 无修复 PR |
| 🟠 中高 | [#5278](https://github.com/HKUDS/nanobot/issues/5278) + [#5279](https://github.com/HKUDS/nanobot/pull/5279) | 会话历史存放在 workspace 内，agent 可越权读取 | ✅ 已有 fix PR（待合并） |
| 🟠 中高 | [#5276](https://github.com/HKUDS/nanobot/issues/5276) + [#5283](https://github.com/HKUDS/nanobot/pull/5283) | 全局 workspace 目录跨会话共享，存在数据泄露风险 | ✅ 已有 fix PR（待合并） |
| 🟡 中 | [#5256](https://github.com/HKUDS/nanobot/issues/5256) | `/goal` 消息导致重复回复数十次，等待用户输入时陷入循环 | ⚠️ 无修复 PR |
| 🟡 中 | [#5149](https://github.com/HKUDS/nanobot/issues/5149) | WhatsApp 渠道无法发送音频消息（可接收） | ⚠️ 无修复 PR |
| 🟢 较低 | [#5264](https://github.com/HKUDS/nanobot/issues/5264) | 历史 API 不返回媒体根目录外文件的 `media_urls` | ✅ 已由 #5268 修复 |
| 🟢 较低 | [#5273](https://github.com/HKUDS/nanobot/issues/5273) | 会话裁剪误删主动推送消息 | ✅ 已由 #5272 修复 |

**安全导向的 PR**：#5279（会话历史外移出 workspace）和 #5283（per-session 沙箱隔离）均标注 security 标签并处于待合并状态，建议维护者**优先评估合入**。

---

## 6. 功能请求与路线图信号

| 功能请求 | 来源 | 信号强度 | 分析 |
|---------|------|---------|------|
| **Token 使用日志/审计** | [#5266](https://github.com/HKUDS/nanobot/issues/5266) | ⭐⭐⭐⭐⭐ | 社区呼声最高，生产级需求明确，预计会进入 roadmap |
| **Telegram Sticker + 主动消息 Reaction** | [#5289](https://github.com/HKUDS/nanobot/issues/5289) | ⭐⭐⭐⭐ | 有 bot 账号提交，功能描述完整，可能作为渠道增强在近期 PR 中出现 |
| **Temporary Chat（临时会话）** | PR [#5252](https://github.com/HKUDS/nanobot/pull/5252) | ⭐⭐⭐⭐ | 已有实现，待合并，WebUI 体验的重要补充 |
| **Per-session 沙箱隔离** | [#5283](https://github.com/HKUDS/nanobot/pull/5283) | ⭐⭐⭐ | 与安全加固方向一致，opt-in 模式，预计将在后续版本默认开启 |
| **Agent Plugins 与 CLI Apps 集成** | PR [#5288](https://github.com/HKUDS/nanobot/pull/5288) | ⭐⭐⭐ | 推动插件生态标准化 |
| **子代理会话记录持久化** | PR [#5291](https://github.com/HKUDS/nanobot/pull/5291) + Issue [#5290](https://github.com/HKUDS/nanobot/issues/5290) | ⭐⭐⭐ | 补足可观测性短板，说明维护者已开始系统性解决"黑盒"问题 |

> 结合已有 PR 判断，**下一版本大概率包含**：per-session 沙箱隔离（#5283）、会话历史外移（#5279）、临时聊天模式（#5252）、子代理记录持久化（#5291）。Token 消耗日志功能目前仅有 Issue，尚未发现对应 PR，可作为路线图参考。

---

## 7. 用户反馈摘要

从今日 Issue 评论和提交内容中，提炼出以下真实声音：

1. **成本敏感度上升**（#5266）：用户在未主动使用的情况下遭遇大量 Token 消耗，对"莫名其妙走量"表示困惑，希望系统提供"透明度"而非仅靠后端监控。
2. **会话隔离诉求强烈**（#5278, #5276）：多用户提到多会话间共享 `~/.nanobot/workspace` 目录存在隐私隐患，"即使开启 bwrap 沙箱，所有会话仍然能读写彼此的临时文件"——这说明安全配置的可感知度不足。
3. **模型切换体验不佳**（#5198）：用户希望像商业 SaaS 一样，在会话中直接切换模型，而非依赖 `/model` 命令或重新配置实例。"UI 上的模型标签没用，点了没有反应"——这是对交互细节的直接批评。
4. **多渠道一致性的期望**（#5149, #5289）：以 WhatsApp 和 Telegram 为代表的渠道功能不完整（音频/贴纸等），用户对渠道间功能一致性有明确期待。
5. **稳定性关注**（#5256）：`/goal` 消息产生几十条重复回复，用户描述为"直到我介入或模型自行识别死循环才算结束"——这种体验对生产环境可用性是致命缺陷。

---

## 8. 待处理积压

以下 Issue/PR 值得维护者重点关注：

| 编号 | 类型 | 简述 | 等待时长 | 优先级建议 |
|------|------|------|---------|-----------|
| [#5198](https://github.com/HKUDS/nanobot/issues/5198) | Issue | 会话内无法切换模型，`/model` 命令无效 | 8 天 | 中 — 直接影响用户体验 |
| [#5256](https://github.com/HKUDS/nanobot/issues/5256) | Issue | `/goal` 重复回复死循环 | 3 天 | 高 — 生产阻塞性 Bug |
| [#5149](https://github.com/HKUDS/nanobot/issues/5149) | Issue | WhatsApp 音频发送失败 | 11 天 | 中 — 渠道功能不完整 |
| [#5156](https://github.com/HKUDS/nanobot/pull/5156) | PR | Telegram 轮询静默停滞后无法恢复 | **10 天** | 高 — 自动化后台进程可能长期无感知失效 |
| [#4276](https://github.com/HKUDS/nanobot/pull/4276) | PR | 模型无关的 computer use 工具集 | **59 天** | 中 — 功能型增强，但积压已久 |

**优先级建议**：

- **#5156** 和 **#5256** 均为"静默失败"型 Bug，在无告警的情况下造成持续影响，建议优先处理；
- **#5198** 是交互体验硬伤，涉及诸多用户日常使用；
- **#4276** 积压近两个月，建议维护者明确接受/拒绝/要求 rebase 的决定，避免 PR 腐烂。

---

*本日报由 AI 自动生成，数据来源于 NanoBot GitHub 仓库公开信息，统计区间：2026-08-07 至 2026-08-08。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-08

## 今日速览

过去24小时内，Hermes Agent 项目保持高度活跃：共产生 100 条 Issues 和 PR 更新，其中新开 Issues 45 条、PR 提交 47 条。**最值得关注的是安全与稳定性方向**——今日提交的 PR 中有 3 条直接涉及安全加固（SSRF 防护、工具结果持久化、隐式 Unicode 注入防护），同时 Kanban 任务编排系统暴露了多个自动化流程缺陷（僵尸进程、任务弹跳、预算耗尽），成为当前最集中的问题域。此外，多平台（Telegram/WhatsApp/Windows）的兼容性与体验问题持续涌入，跨平台会话上下文共享、实时语音、Teams 等前瞻性功能提案也获得了社区关注。无新版本发布，项目处于密集开发迭代阶段。

---

## 版本发布

今日无新版本发布。

## 项目进展

今日有 3 条 PR 被合并或关闭，整体推进有限，但修复方向值得关注：

- **[#74452] [已关闭] fix(tools): Python 3.14 compatibility for DaemonThreadPoolExecutor** — 修复了 Python 3.14 移除 `ThreadPoolExecutor._initializer/_initargs` 后导致的兼容性崩溃，对向新 Python 版本迁移有积极意义。
- **[#81412] [已关闭] Add policy fallback delegation to local Qwen** — 增加策略兜底路由，将受策略限制的任务转发到本地 Qwen 子代理，扩展了模型路由的灵活性。

> ⚠️ 注意：今日关闭的 PR 中有 1 条被标记为 `duplicate`（#74452），可能与已有修复重复。今日**尚未有 PR 被合并进入主分支**，所有功能修复仍在等待审查合入。

## 社区热点

### 讨论热度最高

- **[#4335] Cross-platform session context sharing (CLI ↔ Telegram)** — 12 条评论，3 个 👍。用户要求打通不同平台间的会话上下文，反映多端使用场景下"记忆孤岛"的核心痛点。这是项目长期存在的架构级诉求，涉及网关层会话存储的重新设计。
- **[#79278] Context compression can drop an in-flight tool chain** — 10 条评论。压缩机制在执行中的工具链上触发，导致副作用已完成但结果丢失、智能体重放执行，**对非幂等操作存在安全风险**，是 P1 级别的严重缺陷。
- **[#11349] Discord 文档六处漂移 + `/voice join` 缺失** — 9 条评论。已关闭，但社区对文档与代码一致性的关注可见一斑，同时暴露了 Discord 集成的功能缺口。

### 趋势分析

社区的讨论焦点集中在 **Kanban 自动化编排的可靠性**（#79728、#75444、#80280、#80507、#80512、#79738 等多个高度关联的缺陷）和 **跨平台一致性与同步**（#81405、#79890、#4335）。Telegram 消息投递问题（#79331、#46100、#63485）也反复出现，说明即时通讯平台适配仍是高频痛点。

## Bug 与稳定性

以下按严重程度排序，标注是否已有对应修复 PR：

### P1（严重）

| Issue | 问题描述 | 状态 |
|-------|---------|------|
| [#79278](https://github.com/NousResearch/hermes-agent/issues/79278) | 上下文压缩丢弃进行中的工具链结果，导致非幂等操作被重放 | 无修复 PR |
| [#79624](https://github.com/NousResearch/hermes-agent/issues/79624) | 网关重启时预压缩阶段 exit(1) 崩溃，超大会话直接杀死进程 | 无修复 PR |
| [#65365](https://github.com/NousResearch/hermes-agent/issues/65365) | Anthropic OAuth 连接下，暴露 `memory`/`session_search` 工具 schema 稳定触发 HTTP 400 | 无修复 PR |
| [#81267](https://github.com/NousResearch/hermes-agent/issues/81267) | Cron + 后台 delegate：SessionDB use-after-close 导致子代理日志丢失，完成通知无法路由 | 无修复 PR |

### P2（中等）

| Issue | 问题描述 | 修复 PR |
|-------|---------|--------|
| [#54523](https://github.com/NousResearch/hermes-agent/issues/54523) | Tailscale 远程桌面：异步路由阻塞事件循环 10-25 秒，WS 断流 | 无 |
| [#22418](https://github.com/NousResearch/hermes-agent/issues/22418) | macOS 桌面网关与 CLI `--replace` 冲突，Discord Token 锁死 | 无 |
| [#80569](https://github.com/NousResearch/hermes-agent/issues/80569) | Windows 桌面安装残留重复启动项，更新后可能复活 | 无 |
| [#80968](https://github.com/NousResearch/hermes-agent/issues/80968) | Windows 下 `--tui` 回车即崩溃（已标记 duplicate） | 无 |
| [#81290](https://github.com/NousResearch/hermes-agent/issues/81290) | Windows 副桌面窗口黑屏，无任何诊断日志 | 无 |

### P3（较低，但值得关注）

- Kanban 系列：[#79728](https://github.com/NousResearch/hermes-agent/issues/79728)（自动分解重复工作）、[#75444](https://github.com/NousResearch/hermes-agent/issues/75444)（无限块弹跳）、[#80280](https://github.com/NousResearch/hermes-agent/issues/80280)（超时 worker 遗留进程组存活）、[#80507](https://github.com/NousResearch/hermes-agent/issues/80507)（委托子任务耗尽父任务预算）、[#80512](https://github.com/NousResearch/hermes-agent/issues/80512)（熔断 `gave_up` 后僵尸执行仍完成任务）、[#79738](https://github.com/NousResearch/hermes-agent/issues/79738)（自动分解器重新晋升 review 阻塞任务）
- **[#81411 已有修复 PR](https://github.com/NousResearch/hermes-agent/pull/81411)**：向整个进程组发送终止信号，解决超时/回收时子进程残留问题。
- 桌面端体验：[#79833](https://github.com/NousResearch/hermes-agent/issues/79833)（X/Twitter 卡片卡在 UI 上）、[#80184](https://github.com/NousResearch/hermes-agent/issues/80184)（WSL 安装提示噪音）

> **注意：4 个 P1 级 Bug 均无对应修复 PR，Kanban 稳定性问题已成为系统性风险。**

## 功能请求与路线图信号

### 可能被纳入下一版本的功能

| 功能 | 对应 Issue / PR | 信号强度 |
|------|----------------|---------|
| **`cronjob` 工具增加 `get` action 和 `include_prompt`** | [#18374](https://github.com/NousResearch/hermes-agent/issues/18374) + ([#81408 PR](https://github.com/NousResearch/hermes-agent/pull/81408)) | ⭐⭐⭐ 已有 PR 提交，功能缺失明确 |
| **桌面端安装包一体化** | [#79599 PR](https://github.com/NousResearch/hermes-agent/pull/79599) — 内置 Python/Node/wheelhouse，免首次联网下载 | ⭐⭐⭐ 大型 PR，覆盖安装/更新/通道 |
| **实时语音 Provider 合同** | [#81404 PR](https://github.com/NousResearch/hermes-agent/pull/81404) | ⭐⭐ 基于此前 RFC 与 #70366 的基础 |
| **Cron 失败投递到独立目标** | [#77866 PR](https://github.com/NousResearch/hermes-agent/pull/77866) | ⭐⭐ 已持续活跃 5 天 |
| **跨平台会话上下文共享** | [#4335](https://github.com/NousResearch/hermes-agent/issues/4335) | ⭐⭐ 12 条评论，3 👍，需架构级设计 |
| **Windows `--force-kill` 更新标志** | [#64386 PR](https://github.com/NousResearch/hermes-agent/pull/64386) | ⭐⭐ 解决 Windows 更新时 .pyd 文件锁问题 |

### 值得关注的远期方向

- **[#81405](https://github.com/NousResearch/hermes-agent/issues/81405) 一等公民 Teams** — 多 Profile 持久化协作、快捷聊天、托管工作，定义了多代理协作的下一步形态。结合 Kanban、Profiles 等已有原语，属于路线图级别的提案。
- **[#79890](https://github.com/NousResearch/hermes-agent/issues/79890) WhatsApp 功能对齐战役** — meta-issue 一次性汇总了 WhatsApp 平台的所有功能缺口，推动 WhatsApp Business Cloud API 与桥接后端对齐。

## 用户反馈摘要

从今日 Issues 评论中提炼的真实用户反馈：

### 核心痛点

1. **会话状态一致性与消息可靠性**。反复出现的 `sweeper:risk-session-state` 和 `sweeper:risk-message-delivery` 标签，以及 Telegram 富文本消息丢失、消息批处理被拆散等问题，说明消息投递的零丢失、零重复仍是刚需。用户对"输出被吞"（#80832 评论）和"消息发送了但 UI 不刷新"的容忍度极低。

2. **Windows 平台体验粗糙**。多条 Windows 专属问题（TUI 崩溃、桌面黑屏、启动项残留、WSL 提示噪音），涉及桌面端基本可用性，是影响用户留存的重要短板。

3. **Kanban 自动化流程"行为不可预测"**。用户 SharadKumar 连续提交多个 Kanban 编排缺陷（僵尸进程、重复分派、预算耗尽、状态误判），反映了复杂自动化在真实环境中的失控风险——"`gave_up` 之后任务仍然完成了，这是最可怕的情况"（#80512）。

### 使用场景亮点

- 社区用户积极将 Hermes 嵌入更复杂的多代理协作流程（#81405 提案中"持久化多 Profile 团队 + Quick Chat"的场景），当前在 Kanban 和 Delegation 上的功能积累正在被真实用户探索边界。
- 有用户在尝试用 Hermes 做"第一方调试"——即用 Hermes 管理 Hermes 的开发任务（Kanban 任务含 open PR），这类 dogfooding 行为暴露了大量真实缺陷，也证明了项目的成熟度。

## 待处理积压

以下为长期未响应或可能被忽视的重要项，建议维护者优先关注：

| 编号 | 类型 | 说明 | 过期时间 |
|------|------|------|---------|
| [#4335](https://github.com/NousResearch/hermes-agent/issues/4335) | Feature | 跨平台会话上下文共享（CLI ↔ Telegram），12 条评论、3 👍，已开放 130 天 | 2026-03-31 创建，值得正式回应 |
| [#18374](https://github.com/NousResearch/hermes-agent/issues/18374) | Feature | `cronjob` 工具缺少获取完整 prompt 的能力，5 👍，已开放 99 天 | 已有对应 PR #81408，但被标记为 `duplicate`，需明确处理方式 |
| [#64386](https://github.com/NousResearch/hermes-agent/pull/64386) | PR | Windows `--force-kill` 更新标志，已开放 25 天无进展 | 2026-07-14 创建，解决 Windows 用户更新失败的常见痛点 |
| [#54523](https://github.com/NousResearch/hermes-agent/issues/54523) | Bug | 远程桌面（Tailscale）异步路由阻塞，已开放 40 天，P2 | 2026-06-29 创建，远程使用场景的核心阻塞 |

> **总结**：项目整体活跃度高，社区参与积极，安全与稳定性议题热度上升。但 P1 级缺陷（特别是 #79278 和 #79624）无修复进展，Kanban 编排的系统性缺陷需要一次集中治理。建议维护者优先响应高热度功能提案（#4335、#18374），并对 Kanban 相关 Issues 做一次批量 triage，避免同一根因反复上报。

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期**: 2026-08-08  
**数据来源**: github.com/sipeed/picoclaw  
**统计窗口**: 过去 24 小时


## 1. 今日速览

PicoClaw 过去 24 小时整体活跃度**中高**：共产生 4 条 Issue 更新和 14 条 PR 更新。核心动向集中在 **WhatsApp 渠道修复**（#3320，解决官方客户端 405 拒绝连接问题）、**prefix caching 优化**（#3321，提升推理性能）以及 **exec 工具超时/布尔参数修复**（#3319），均为实质性的代码质量提升。值得关注的是，新提交的 3 个 PR 全部来自社区贡献者（grrowl、MrTreasure），社区活跃度信号积极；但 12 条待合并 PR 中绝大多数为 Dependabot 自动依赖升级（占比约 58%），人工提交的 PR 存在明显的审查积压，最长的等待已超过 5 周（#3200，自 7 月 1 日创建至今未合并），维护吞吐量有待改善。依赖升级 PR 中已有 2 条今日被合并/关闭（#3291、#3289），缓解了部分积压压力。无新版本发布。


## 2. 版本发布

**无新版本发布。** 上次发布节奏需结合历史数据判断，建议关注后续 Release 动态。


## 3. 项目进展

今日合并/关闭了 2 条 PR，均为依赖升级：

- **[PR #3291] [已关闭] build(deps): bump github.com/github/copilot-sdk/go from 0.2.0 to 1.0.8** — 将 GitHub Copilot SDK 从 v0.2.0 升级至 v1.0.8（跨大版本升级），为后续 Copilot 相关功能提供更新的 SDK 基础。[链接](https://github.com/sipeed/picoclaw/pull/3291)
- **[PR #3289] [已关闭] build(deps): bump github.com/pion/rtp from 1.10.2 to 1.10.5** — RTP 库补丁版本升级，提升 WebRTC 相关链路的稳定性。[链接](https://github.com/sipeed/picoclaw/pull/3289)

**等待合并的高价值 PR（今日更新）**：

| PR | 内容 | 等待时长 | 价值评估 |
|---|---|---|---|
| [#3321](https://github.com/sipeed/picoclaw/pull/3321) | 动态上下文移至历史之后，保留 prefix caching | 创建当日 | 可显著降低重复请求的 token 消耗与延迟；对长会话场景影响明显 |
| [#3320](https://github.com/sipeed/picoclaw/pull/3320) | 升级 whatsmeow 修复 WhatsApp 405 掉线 | 创建当日 | 恢复 WhatsApp 渠道可用性，属于功能性修复，影响面明确 |
| [#3319](https://github.com/sipeed/picoclaw/pull/3319) | exec 工具超时参数及布尔参数修复 | 创建当日 | 修正工具行为与 schema 不一致，社区反馈的工具可靠性问题 |
| [#3279](https://github.com/sipeed/picoclaw/pull/3279) | 修复 seahorse 工具调用格式泄漏至 LLM 摘要 | 18 天 | 影响 LLM 输出质量，涉及多模态消息处理链路 |
| [#3283](https://github.com/sipeed/picoclaw/pull/3283) | 钉钉渠道图片消息接入 | 17 天 | 补齐钉钉渠道的多模态能力，扩展了渠道功能边界 |
| [#3271](https://github.com/sipeed/picoclaw/pull/3271) | 9 家 Provider 默认模型名更新至 2026-07 最新 | 19 天 | 防止用户使用已废弃的模型 ID，减少误配置风险 |
| [#3270](https://github.com/sipeed/picoclaw/pull/3270) | 新增 DashScope TTS Provider + 微信语音发送 | 19 天 | 新增 TTS 后端与微信渠道能力，功能覆盖面扩展 |
| [#3200](https://github.com/sipeed/picoclaw/pull/3200) | 可配置模型默认回退链 | 38 天 | 提升模型路由灵活性，对多 Provider 用户有实用价值 |

**总体判断**：非依赖类 PR 均未合并，项目核心功能的推进速度受限于审查效率，8 条功能性 PR 已等待 2~5 周，存在"功能就绪但未上线"的积压现象。


## 4. 社区热点

- **[Issue #3093] 希望支持 SimpleX / Tox / Wire 网关**（6 条评论，1 👍）— 用户明确表达了对端到端加密通信协议的支持诉求。虽然该 Issue 已被标记为 stale 并关闭，但这类需求可能代表隐私敏感型用户群体，值得在路线图讨论中参考。[链接](https://github.com/sipeed/picoclaw/issues/3093)

- **[Issue #3302] MCP Server 支持 OAuth 2.1**（2 条评论）— 引用 #2546 提出为 MCP 服务器增加 OAuth 2.1 认证支持，属于企业级部署场景下的安全增强需求，已被标记为 Nice-to-Have。[链接](https://github.com/sipeed/picoclaw/issues/3302)

- **[Issue #3308] 并发安全与性能优化代码审查报告**（1 条评论）— 社区成员对 SeaHorse、Channel Manager 和 Hooks 的代码审查，指出并发风险、goroutine 泄漏和内存/速度优化空间。该报告的深度表明社区中已有开发者对项目代码进行了深入分析。[链接](https://github.com/sipeed/picoclaw/issues/3308)

- **今日新增 PR #3321 和 #3320**（均为 grrowl 提交）— 两个 PR 分别针对推理性能（prefix caching）和 WhatsApp 渠道可用性，均为明确的、可直接验证的改进，是今日社区贡献的亮点。


## 5. Bug 与稳定性

按严重程度排列：

| 严重程度 | Issue/PR | 描述 | 状态 |
|---|---|---|---|
| **高** | [PR #3320](https://github.com/sipeed/picoclaw/pull/3320) | WhatsApp 渠道持续掉线（Client outdated 405），原生 WhatsApp 通道不可用，无自动重连机制 | 已有修复 PR（待合并） |
| **中** | [PR #3319](https://github.com/sipeed/picoclaw/pull/3319) | `exec` 工具的 `timeout` 参数无效（实际走全局超时）、`background` 和 `pty` 被声明为字符串但实际为布尔 | 已有修复 PR（待合并） |
| **中** | [PR #3279](https://github.com/sipeed/picoclaw/pull/3279) | 工具调用格式泄漏到 LLM 摘要（seahorse `partsToReadableContent`），影响多模态上下文质量 | 已有修复 PR（待合并） |
| **低** | [Issue #3308](https://github.com/sipeed/picoclaw/issues/3308) | 社区代码审查：SeaHorse/Channel Manager/Hooks 存在并发安全隐患、goroutine 泄漏等（属预防性发现，未有线上事故报告） | 无对应修复 PR |

**风险提示**：以上 4 项均有明确修复方案，但受限于 PR 审查积压，尚未合并至主干，线上环境的修复时效存在较大改善空间。


## 6. 功能请求与路线图信号

### 用户新提出的功能请求
- **OAuth 2.1 支持（MCP Servers）** — Issue #3302，企业级认证需求，当前标记为 Nice-to-Have。[链接](https://github.com/sipeed/picoclaw/issues/3302)
- **Telegram / 聊天渠道的会话管理命令** — Issue #3307，要求会话的列出/切换/删除能力，当前仅 Web UI 具备完整会话管理。[链接](https://github.com/sipeed/picoclaw/issues/3307)
- **SimpleX / Tox / Wire 网关支持** — Issue #3093，隐私通信协议扩展（已关闭，但诉求明确）。[链接](https://github.com/sipeed/picoclaw/issues/3093)

### 结合已有 PR 判断可能进入下一版本的功能
- **DashScope TTS + 微信音频发送**（PR #3270）— 功能完整、实现清晰，若通过审查，有望进入下个版本
- **可配置模型默认回退链**（PR #3200）— 已有完整的前后端实现（含 Web UI 拖拽排序），属于直接可用的用户功能
- **钉钉渠道图片消息**（PR #3283）— 完整的渠道能力扩展，覆盖钉钉办公场景的实际需求
- **9 家 Provider 默认模型名更新**（PR #3271）— 属于持续维护类功能，应当尽快合并

**路线图信号**：综合来看，社区对**多模态**（图片/语音）和**多渠道**（钉钉、微信、WhatsApp）的关注度明显上升，预计项目下一阶段将围绕这两个方向持续发力，且已有多个对应 PR 在途，但均因审查积压而进展缓慢。


## 7. 用户反馈摘要

- **对代码质量的积极反馈**：Issue #3308 的作者在代码审查中对项目给予了积极评价，"building a native Go AI assistant that runs on $10 hardware with <10MB RAM and sub-second boot times is seriously awe..."，反映了社区对项目技术路线的认可。[链接](https://github.com/sipeed/picoclaw/issues/3308)

- **对渠道可用性的不满意**：WhatsApp 渠道的持续掉线问题（PR #3320 描述），用户期望消息渠道稳定可靠，当连接被对端拒绝且无自动恢复机制时体验不佳。[链接](https://github.com/sipeed/picoclaw/pull/3320)

- **对隐私/安全通信的需求**：用户（Damian-o2）明确提出需要加密通信协议（SimpleX/tox/Wire）作为网关，暗示当前渠道无法满足部分用户的隐私保护要求。[链接](https://github.com/sipeed/picoclaw/issues/3093)

- **对会话管理跨端一致性的期待**：用户（iamtoricool）指出 Web UI 已有完整会话管理但 Telegram 等渠道无法使用，建议所有渠道功能对齐。[链接](https://github.com/sipeed/picoclaw/issues/3307)


## 8. 待处理积压

以下为长期未获得维护者响应的重要 Issue/PR：

| 项目 | 创建时间 | 等待时长 | 说明 |
|---|---|---|---|
| [PR #3200](https://github.com/sipeed/picoclaw/pull/3200) | 2026-07-01 | **38 天** | 模型默认回退链，含完整前后端实现，文件较多且涉及 UI 变更，一直未获 merge 或评审意见 |
| [PR #3270](https://github.com/sipeed/picoclaw/pull/3270) | 2026-07-20 | **19 天** | DashScope TTS + 微信语音，涉及两个新平台能力 |
| [PR #3271](https://github.com/sipeed/picoclaw/pull/3271) | 2026-07-20 | **19 天** | 9 家 Provider 默认模型名更新至 2026-07 最新，经逐家对照官方文档验证 |
| [PR #3279](https://github.com/sipeed/picoclaw/pull/3279) | 2026-07-21 | **18 天** | 修复工具调用格式泄漏至 LLM 摘要，直接影响输出质量 |
| [PR #3283](https://github.com/sipeed/picoclaw/pull/3283) | 2026-07-22 | **17 天** | 钉钉渠道图片消息支持 |
| [Issue #3308](https://github.com/sipeed/picoclaw/issues/3308) | 2026-07-30 | **9 天** | 社区代码审查报告（并发安全/性能），目前仅有作者自评论 |

**⚠ 维护者提醒**：以上 PR 如功能完善、测试通过，建议优先合并或给出反馈。特别是 PR #3200 已等待 38 天，可能增加后续合并时的冲突解决成本。建议在项目的 Pull Request 审查流程上增加人力投入，合理安排合并优先级，以避免社区贡献者的积极性因长期等待而受挫。


*本日报由 AI 自动生成，数据截止 2026-08-08。以上所有分析均基于 GitHub 公开数据，请以项目实际状态为准。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-08-08

## 1. 今日速览

NanoClaw 项目过去24小时整体活跃度呈**中高水平**：无新 Issue 产生（0开放/0关闭），但 PR 侧十分活跃——共10条更新，其中 8 条仍待合并、2 条已关闭。目前有 4 个 open PR 于8月7日为最新更新，呈现出社区提交持续涌入但合并积压的趋势。核心方向集中在**渠道集成扩展**（Mattermost、Dial）、**技能技能/Skill 生态丰富**（Tavily、AnyDoc）以及**健壮性修复**（挂载只读、消息目的地回填、进度失败展示）。无新版本发布，项目处于功能累积期。

## 3. 项目进展

过去24小时内有 **2 个 PR 关闭**，一为合并，一为关闭（或超驰），对项目推进情况如下：

- **#3197 fix(progress): 失败状态展示具体原因**（由 tier2tech-tian 提交，8月7日关闭）— 修复了 agent-runner 过程卡失败标题只显示“执行系统检查失败”等泛化文案的问题，现可从 `resultSummary` 提取具体失败原因、跳过退出码套话与凭证行，复用脱敏逻辑并做 38 字符单行截断。附带 reducer 单测与飞书卡片 JSON 跨层测试，全量测试 1427 项通过。**这是提升用户可观测性的关键体验修复。**
- **#546 Add Mattermost channel skill (/add-mattermost)**（由 wakqasahmed 提交，8月7日关闭）— 该 PR 针对 pre-v2 `Channel`/`registry.ts` 架构，因 main 分支已迭代至 `ChannelAdapter`/`channel-registry.ts` 而被关闭。**其后续版本 #3199 已以全新实现应对 v2 架构**，此前工作并未白费。

其余 8 条 PR 待合入，包含：

| PR | 类型 | 推动方向 |
|---|---|---|
| #3199 | Feature（渠道集成） | Mattermost 集成适配 v2 ChannelAdapter |
| #3198 | Utility skill | AnyDoc 文档转换技能 |
| #3190 | Utility skill | Tavily MCP 工具技能 |
| #3050 | Feature + Skill | Dial 渠道接入 channel picker 与 wizard |
| #2909 | core-team 功能 | 首次 Agent 模板设置在 setup 向导中 |
| #3145 | 数据库补丁 | 为既有 wirings 回填 channel destinations |
| #2346 | 格式化修复 | 未知斜杠命令降级为普通聊天处理 |
| #3196 | 修复 | 解决挂载只读问题 |

**整体判断**：项目正处于“渠道生态+技能生态+内部健壮性”三轮驱动的稳步推进期，无重大架构变更，但合并通道有所积压（8个待合并）。

## 4. 社区热点

今日热点的核心是 **Mattermost 集成的前后接力**：

- **PR #3199（Open，8月7日更新）** — wakqasahmed 提交 v2 原生 Mattermost 渠道适配，明确声明“Supersedes #546”，针对 `ChannelAdapter`/`channel-registry.ts` 全新实现。这是对旧 PR 的快速跟进，说明贡献者对上游架构变化反应灵敏。
- **PR #546（Closed，8月7日关闭）** — 原 Mattermost 集成方案因架构迁移被关闭，但并非被否定，而是被 #3199 取代。

这两条 PR 形成了“**一条功能的进与退**”的讨论信号：社区对 Mattermost 接入有持续需求（从 #1379 延承），且对 v2 架构表现出了很好的适应力。此外，**#3197 修复了卡片的失败状态展示**，也引发了积极反响（测试全绿、含飞书卡片测试），是“用户痛点→快速修复”的正面案例。

## 5. Bug 与稳定性

基于今日 PR 动态，以下为被活跃处理的稳定性问题，暂无新报告崩溃或回归：

- **[中] 过程卡失败状态泛化**（#3197）— 用户只能看到“执行系统检查失败”而无具体原因。**已有 fix PR，已关闭/合并**，从失败摘要中提取首行有效原因，并限制单行 38 字符避免二次截断。
- **[中] 挂载未以只读方式挂载**（#3196, Open）— 涉及容器化/沙箱场景的挂载安全问题（`mount readonly` 缺失），可能引致运行时写入风险。当前有 fix PR 待合并。
- **[低] SQLite wirings 目的地缺失**（#3145, Open）— 既有 messaging-group wirings 可能缺少 channel destinations，导致消息路由数据不完整。已有第 021 号迁移回填，保留既有本地名，幂等处理。
- **[低] 未知斜杠命令被错误传给 Agent SDK**（#2346, Open）— 导致响应被静默丢弃。修复方案是回退到 `category: 'none'`，防止 SDK 将用户输入误判为 Claude Code 命令。

所有修复均有对应 PR 覆盖，短期无失控风险；**需重点关注 #3196 与 #3145 的合入进度**，以避免安全配置与数据一致性问题积压。

## 6. 功能请求与路线图信号

过去24小时未新增功能请求 Issue，但 PR 中隐含了明确的路线图信号：

- **渠道生态扩展**：Mattermost（#3199）与 Dial（#3050）齐头并进，接入 `ChannelAdapter` 与 `channel-registry` 模型。这表明下一代渠道扩展机制正吸引外部贡献者，且 v2 架构已初步验证其易扩展性。
- **技能（Skill）体系丰富**：Tavily MCP 工具（#3190）、AnyDoc 文档转换（#3198）均为 Utility skill，无源码改动即接入 `.claude/skills/`。社区正在快速铺量基础工具，显示出强烈的“工具即插即用”诉求。
- **Agent 初始化体验升级**：#2909（core-team）引入设置向导（wizard）中创建首 Agent 的模板流程，并支持“首次 Agent 印记”。这可能是 Agent 模板体系（part 2 of 2，part 1 为 #2890）的收尾部分，指向更精细化的初始化自定义。

综合来看，下一版本（或后续 alpha）极可能包含 Mattermost/Dial 渠道、Tavily/AnyDoc 技能，以及 Setup Wizard 的模板化首 Agent 体验。

## 7. 用户反馈摘要

本期无 Issue 评论互动，但从 PR 描述与测试反馈中可提炼以下真实用户痛点：

- **“失败模板文案不可用”**（#3197 提出者）：用户只能看到“执行系统检查失败”之类的泛文案，而底层 `resultSummary` 已含具体错误。修复后期望看到“动作失败：具体原因”，并保持与飞书卡片跨层断言的脱敏一致性，说明用户对错误信息的**可操作性要求较高**。
- **“错误消息被静默丢弃”**（#2346）：当用户输入未知斜杠命令，Agent SDK 可能会误当 Claude Code 命令处理，输出无 `<message>` 块，最终响应被丢弃。用户实际上期望“未知命令≈普通聊天”，而不是整个会话无响应。这是交互预期管理的典型缺口。
- **“写挂载暴露”**（#3196）：容器/沙箱场景中挂载未设为只读，可能造成意外写入与安全风险。#3196 的提交者主动修复此问题，反映了用户对安全默认值的高敏感。

总体用户反馈偏向**可观测性**与**安全默认值**，项目正在响应这些反馈，但反馈入口多经 PR 而非 Issue，维护者需注意 PR 讨论中的隐性用户需求。

## 8. 待处理积压

以下 PR/技能相对长期未合入，需维护者审视推进：

- **#2346 fix(formatter): 未知斜杠命令按普通聊天处理**（2026-05-08 创建，至今 3 个月）— 交互体验修复，直接关乎用户日常输入。**建议尽快评审合入**。
- **#2909 feat(setup): 模板化设置流程与首 Agent 印记**（2026-07-02 创建，1 个多月）— core-team 成员提交，功能完整（含模板加载器 #2890 的 depend），应是路线图正式项，但不知为何停留 open 超一个月。可能需内部对齐测试策略。
- **#3050 feat(setup): Dial 接入 channel picker 与 skills**（2026-07-14 创建，近 4 周）— 功能实现详实，且涉及 wizard 与 `runChannelSkill` 模型。若无冲突，建议与 #2909 一并评审，避免 setup 流程被多个 PR 同时改动而冲突。
- **#3145 fix(db): 回填既有 wirings 目的地**（2026-07-28 创建，约 10 天）— 迁移类低风险修复，仅影响存量数据，合入后可避免后续渠道接入时数据不一致。
- **#3196 Fix/add mount readonly**（2026-08-07 创建，待审）— 安全相关，建议优先安排安全 review。

另外，**#3190（Tavily MCP）与 #3198（AnyDoc）** 均为 Utility skill，生命周期短、影响面小，可进行批量快速评审。若技能合入速度持续高于 Source 变更速率，建议考虑引入“Skill 快速通道”流程。

---

*以上日报基于 2026-08-08 快照数据生成，所有链接均指向 nanocoai/nanoclaw 仓库。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

好的，我是您的 AI 智能体与个人 AI 助手领域开源项目分析师。根据 IronClaw 仓库在 2026-08-08 的 GitHub 数据，我为您生成了以下项目动态日报。

---

## IronClaw 项目动态日报 (2026-08-08)

### 1. 今日速览

IronClaw 项目过去24小时活跃度极高，共有 50 条 Issue 和 50 条 PR 更新，呈现出密集的开发和维护节奏。其中，Issue 关闭率（28%）和 PR 合并率（24%）相对较低，表明项目正处于功能快速迭代期，大量工作积压在待审查和测试阶段。社区关注点集中在**文档与事实严重脱节**、**Agent 状态幻觉（Hallucination）问题**以及**工具发现机制的稳定性**上。值得一提的是，核心贡献者 `serrrfirat` 和 `BenKurrek` 提交了多项大型 PR，旨在系统性解决上述问题，显示出项目健康、积极的发展势头。目前暂无新版本发布。

### 2. 版本发布

无。过去 24 小时内没有新的 Release 版本。

### 3. 项目进展

尽管合并的 PR 数量不多，但今日有多项高价值 PR 被关闭或处于待合并状态，标志着项目在多个关键领域取得了实质性进展。

- **文档与代码一致性 (Doc-Truth) 战役启动**：针对社区广泛抱怨的"文档漂移"问题，维护者 `thisisjoshford` 提交了一个由 5 个 PR 组成的系列（#7375, #7376, #7378, #7379, #7381）。这标志着项目开始系统性解决文档与行为不一致的问题，通过引入 `docs-live` 分支部署、文档事实契约测试等机制，从流程上根除该问题。
- **工具发现机制优化**：PR #7374 和 #7372 聚焦于优化 Reborn 引擎的工具发现（tool disclosure）机制。前者引入了批量工具描述（bulk `tool_describe`）能力，旨在大幅减少模型在发现多个工具时的来回轮询（round-trips），这将直接提升 Agent 的响应速度和效率。
- **关键基础设施审计与加固**：PR #7373 对项目的全部 37 个架构测试门禁文件和约 80 个 CI 脚本进行了全面审计，旨在发现并修复门禁失效（fail-open）的问题，提升 CI/CD 管道的可靠性。
- **核心 Bug 修复**：PR #7365 针对长期存在的"记忆无法跨会话调用"问题（#7185）提出了修复方案，而 PR #7384 则修复了错误地将会话故障报告为 API Key 无效的问题，这些都将显著改善用户体验。

### 4. 社区热点

- **[Issue #7340] 无法将模型设置重置为出厂默认值** (6 条评论)
  - 链接: [nearai/ironclaw Issue #7340](https://github.com/nearai/ironclaw/issues/7340)
  - 分析：这是今日最热门的讨论。用户反馈在更改模型提供商/选择后无法恢复初始配置。这反映了一个常见的 UX 痛点：缺少"恢复默认设置"的逃生舱口。诉求不仅是修复，更是希望能在设置界面提供明确的恢复机制，降低用户误操作后的挫败感。

- **[Issue #6989] Token 计算错误：混合提供商用量与尾部估算** (4 条评论)
  - 链接: [nearai/ironclaw Issue #6989](https://github.com/nearai/ironclaw/issues/6989)
  - 分析：该问题展示了社区对**成本透明度和准确性**的高度关注。Bug 指出模型在估算输入 Token 时，是从内容引用字符串的长度计算，而非引用内容的实际长度，这直接导致用量计费不准确。这不仅是技术bug，更是影响用户信任和成本控制的关键问题。

- **[Issue #7317] 提案：文档真实性验证管道** (3 条评论)
  - 链接: [nearai/ironclaw Issue #7317](https://github.com/nearai/ironclaw/issues/7317)
  - 分析：该提案直接引发了今日的 "Doc-Truth" 系列 PR。它指出了 `origin_gate_matrix` 成为必需字段等破坏性变更未同步更新文档的问题，导致开发者的集成尝试失败。社区的诉求是建立一个**自动化、可验证的文档测试体系**，确保文档与代码行为始终同步，避免误导。

### 5. Bug 与稳定性

过去 24 小时报告了多个 Bug，主要集中在 Agent 行为一致性和基础设施稳定性方面。以下按严重程度排列：

- **严重 (P1) - Agent 状态幻觉与身份混淆**：多条 `bug_bash_P1` Issue 报告此问题，是当前最严重的稳定性风险。Agent 经常在未实际验证的情况下，**虚构**或**错误记忆**用户、频道、自动化的状态，导致错误指令或无效操作。
  - [Issue #7344] Slack 连接 ACTIVE 但助手不识别 (无修复 PR)
  - [Issue #7246] Agent 虚构"自动化正在运行"状态 (无修复 PR)
  - [Issue #7247] Agent 错误声称 GitHub 已连接 (无修复 PR)
  - [Issue #7295] Agent 混淆 Slack 用户身份，将 DM 发送给错误的人 (无修复 PR)
  - 分析：这些高频问题可能源于模型上下文管理缺陷或工具状态查询延迟。虽然暂无直接修复 PR，但它们是项目当前的首要改进方向。

- **严重 (P1) - 基础设施错误**：多条关于 Runner 失联、请求发送失败的 Issue 表明部署环境（Railway）存在不稳定性。
  - [Issue #7298] 请求发送失败/监控系统与运行器失联 (无修复 PR)
  - **[Issue #5456] 例行任务运行因租约过期而失败** - 这是一个长期未解决的 P1 问题，自 6 月 30 日起被标记，至今仍开放，表明这个 90 秒不活动阈值的问题可能根深蒂固。

- **中等问题 - 功能不可用与延迟**:
  - [Issue #7292] CoinGecko 工具安装后无法使用，出现 Runner 心跳错误 (无修复 PR)
  - [Issue #7368] 在 DeepSeek 级别的模型上，频道轮次可能需要几分钟，延迟极高 (无修复 PR)

- **已解决 (过去 24 小时关闭)**：
  - [Issue #6476] Slack `extension_activate` 编码错误导致模型产生幻觉 (已关闭)
  - [Issue #7367] 文档漂移导致模型拒绝操作 (已关闭，为 Doc-Truth 系列 PR 的一部分)
  - [Issue #4874] WebChat v2 在非本地主机 HTTP 环境下报 "Illegal invocation" 错误 (已关闭)

### 6. 功能请求与路线图信号

- **"重置为默认设置" (Issue #7340)**：强烈的用户需求，虽然暂无直接 PR，但属于标准的 UX 改进，很可能在未来版本中作为一个低成本、高收益的小功能被实现。
- **实时的可观测性 (Issue #7369)**：用户请求在 Agent 出错时能捕获追踪信息。PR #7224 的关闭表明**Activity 时间线和轮次导航**功能已实现，这很可能部分满足该需求，并使调试体验大幅改善。
- **文档验证管道 (Issue #7317)**：虽然这是一项工程提案，但社区呼声很高。由它引发的 "Doc-Truth" 系列 PR（见项目进展）将被纳入 v1.2.0 或更早的版本，作为一项重要的工程质量改进。

### 7. 用户反馈摘要

- **对文档的失望**：多名用户和贡献者（如 `cuongdcdev`）在 Issue #7317 中抱怨"破坏性变更没有同步更新文档"，导致迁移和集成过程充满挫败感。这是目前最集中的负面反馈。
- **对 Agent 可靠性的担忧**：大量 QA Bug（如 #7246, #7247, #7295）表明用户对 Agent 的自主判断缺乏信任，因为它经常“一本正经地胡说八道”。用户期望 Agent 在做出声明前先“检查事实”，而不是猜测或虚构。
- **对配置可恢复性的需求**：Issue #7340 的反馈清晰地表明，用户希望有一个"后悔药"。在修改配置后，最好能轻松地回到一个已知的良好状态，而不是在试错中陷入困境。

### 8. 待处理积压

- **[Issue #5456] Routine runs fail with runner lease expiration** (自 2026-06-30 起)
  - 链接: [nearai/ironclaw Issue #5456](https://github.com/nearai/ironclaw/issues/5456)
  - 状态：这是一个高优先级的 P1 Bug，已经积压超过一个月。它严重影响依赖例行任务（Routine）的用户。90 秒的租约过期阈值对多工具工作流来说显然不够，需要维护者优先审视和调整。

- **[Issue #6590] serve fails on Windows** (自 2026-07-23 起)
  - 链接: [nearai/ironclaw Issue #6590](https://github.com/nearai/ironclaw/issues/6590)
  - 状态：一个影响 Windows 用户开发体验的直接阻断性问题。长期未解决可能会将部分潜在贡献者拒之门外。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目动态日报 — 2026-08-08

> 数据来源：github.com/netease-youdao/LobsterAI | 统计周期：过去 24 小时


## 1. 今日速览

项目今日活跃度较高，24 小时内共产生 7 条 Issue 更新和 7 条 PR 更新，并发布了新版本 `2026.8.7`。核心进展集中在 **Cowork 对话搜索**、**Markdown LaTeX 数学公式渲染** 和 **Windows 安装器稳定性修复** 三个方向。值得关注的是，昨日用户报告的 **模型 ID 含斜杠导致的自定义 Provider 无法使用** 问题（#2443）已在 24 小时内收到修复 PR（#2452），体现了项目对社区反馈的快速响应能力。此外，一批 4 月份的陈旧 Issue 被批量关闭，建议维护者关注其中仍未解决的历史问题（见第 8 节）。

- **活跃度**：⭐⭐⭐⭐（中高）
- **响应速度**：Bug 反馈 → 修复 PR 间隔 < 24 小时，优秀
- **项目健康度**：良好，但存在历史 Issue 积压和自动化关闭的争议


## 2. 版本发布

### LobsterAI 2026.8.7（2026-08-07 发布）

**更新内容：**
- ✨ **新增**：Cowork 界面增加标题栏对话搜索功能（PR #2435）
- ✨ **新增**：Markdown 支持 LaTeX 数学公式定界符（PR #2449）
- 🛠️ **修复**：Windows 安装器在 watchdog 退出码为 null 时的异常处理（PR #2446）

**破坏性变更：** 无

**迁移注意事项：** 本次为常规增量更新，无需特殊迁移操作。使用 Cowork 功能的用户升级后可在标题栏直接使用搜索功能；Markdown 渲染现支持 `$...$` 和 `$$...$$` 等 LaTeX 定界符。


## 3. 项目进展

今日共合并/关闭 6 个 PR，主要进展如下：

| PR | 内容 | 影响 |
|---|---|---|
| [#2451](https://github.com/netease-youdao/LobsterAI/pull/2451) | `release/2026.8.5` 合并入 main | 正式发布 8.5 版本，包含对话搜索、数学渲染、IM 分析等多项功能 |
| [#2450](https://github.com/netease-youdao/LobsterAI/pull/2450) | 修复 Windows 上 Cowork 全屏代码工具栏点击失效 | 将全屏浮层移出 Electron 标题栏拖拽区域，解决 Windows 用户实际痛点 |
| [#2449](https://github.com/netease-youdao/LobsterAI/pull/2449) | Markdown LaTeX 数学定界符支持 | 提升技术类用户的文档渲染体验 |
| [#2448](https://github.com/netease-youdao/LobsterAI/pull/2448) | 修复对话搜索相关逻辑 | 完善 Cowork 搜索功能 |
| [#2445](https://github.com/netease-youdao/LobsterAI/pull/2445) | 从 `config.set` 中剥离插件索引管理的键 | 避免插件配置冲突 |
| [#2446](https://github.com/netease-youdao/LobsterAI/pull/2446) | Windows 安装器 watchdog 退出码修复 | 提升 Windows 安装/更新的可靠性 |

**整体评估：** 项目在 Cowork 协作、Markdown 渲染和 Windows 平台稳定性三个方向持续迭代，版本发布节奏稳定（约 2 天一个小版本）。


## 4. 社区热点

**🥇 最热门 Issue：[#2443 - 模型 ID 含斜杠的自定义 Provider 无法在界面中使用](https://github.com/netease-youdao/LobsterAI/issues/2443)**
- 创建于 8 月 6 日，24 小时内获 1 条评论
- **诉求分析：** 用户使用 SiliconFlow 等平台的模型 ID（如 `deepseek-ai/DeepSeek-V4-Flash`）包含斜杠，导致在 UI 中无法正常选择。这类平台在国内开发者中使用广泛，该问题影响面较大
- **响应情况：** 已由 PR #2452 提供修复方案，待合并

**🥈 热门 Issue：[#2447 - 执行没有出结果，也没有错误信息](https://github.com/netease-youdao/LobsterAI/issues/2447)**
- 创建于 8 月 7 日，附截图但无文字描述
- **诉求分析：** 典型的"静默失败"问题，用户无法判断是配置错误还是程序 Bug，这类问题对用户体验伤害较大

**🥉 热门 Issue：[#2444 - 输入框编辑模式功能请求](https://github.com/netease-youdao/LobsterAI/issues/2444)**
- 创建于 8 月 7 日，0 评论但设计完整
- **诉求分析：** 用户详细描述了长 Prompt 输入的痛点（Shift+Enter 换行易误发送），并提两套方案。体现了深度用户对输入体验的精细化需求


## 5. Bug 与稳定性

### 严重程度排序

| 严重程度 | Issue | 描述 | 状态 |
|---|---|---|---|
| 🔴 高 | [#2443](https://github.com/netease-youdao/LobsterAI/issues/2443) | 模型 ID 含斜杠时自定义 Provider 无法在界面使用（SiliconFlow 等） | **已有修复 PR #2452** |
| 🟠 中 | [#2447](https://github.com/netease-youdao/LobsterAI/issues/2447) | 执行无结果无报错，静默失败 | 待排查 |
| 🟡 低 | [#1195](https://github.com/netease-youdao/LobsterAI/issues/1195) | 自建 skill 被安装到 OpenClaw 目录后技能面板不显示（4 月报告，今日被标记 stale） | 长期未解决 |
| 🟡 低 | [#1263](https://github.com/netease-youdao/LobsterAI/issues/1263) | 定时任务 UI 显示重复 + API rate limit 误报（4 月报告，今日关闭） | 已关闭，但根因不明 |

### 关键发现

**7 条 Issue 中，有 4 条是 4 月创建、今日被批量关闭的 stale Issue（#1195、#1263、#1265、#1273）。** 其中：
- #1265（AGENT 绑定独立 IM 机器人和模型）是合理的架构增强需求，被关闭可能令用户失望
- #1273（sql.js WASM 内存崩溃）涉及数据安全，值得关注是否已在内部修复


## 6. 功能请求与路线图信号

| 功能请求 | 来源 | 被纳入下版本的可能性 |
|---|---|---|
| **模型 ID 含斜杠的 Provider 支持**（#2443） | 真实 Bug 反馈 | **高** — 已有修复 PR #2452 |
| **输入框编辑模式**（#2444） | 用户建议，含完整设计 | 中 — 需求合理，非紧急，可能排入后续迭代 |
| **AGENT 绑定独立 IM 机器人和模型**（#1265） | 多 Agent 协作场景 | 低 — 今日被关闭，未见相关 PR |
| **Cowork 对话搜索**（PR #2435） | 项目自主开发 | ✅ 已发布（2026.8.7） |

**路线图信号：** 项目当前发力点明显在 **Cowork 协作体验**（搜索、全屏工具栏修复）和 **兼容性修复**（模型 ID 解析、Windows 安装器）。


## 7. 用户反馈摘要

- **正面反馈：** 无明确正面评价，但快速修复（#2443 当天收到修复 PR）有望提升用户对项目的信任度
- **痛点反馈：**
  - "模型 ID 带斜杠时代理无法配置"（#2443）——国内开发者常用 SiliconFlow，影响面大
  - "执行无结果无错误提示"（#2447）——静默失败比显式报错更令人困惑
  - "输入长 Prompt 换行不便，容易误发送"（#2444）——深度用户的产品体验细节诉求
  - "自建 skill 安装后技能面板无显示"（#1195）——已持续 4 个月未解决，用户可能已流失
- **使用场景洞察：** 用户正在将 LobsterAI 用于**多 Agent 协作**（#1265）和**团队分工**场景，对 Agent 绑定不同模型/机器人有明确需求；同时有用户使用 **WASM 存储且高频写入**（#1273），提示需要关注数据可靠性。


## 8. 待处理积压

| 项目 | 类型 | 创建时间 | 备注 |
|---|---|---|---|
| [#1195](https://github.com/netease-youdao/LobsterAI/issues/1195) 自建 skill 安装后技能面板不显示 | Bug | 2026-04-01 | ⚠️ 已 stale，被标记但未明确解决，建议团队确认是否已在新版本修复 |
| [#1265](https://github.com/netease-youdao/LobsterAI/issues/1265) AGENT 绑定独立 IM 机器人和模型 | 功能需求 | 2026-04-02 | ⚠️ 今日被关闭，但该需求有明确的团队协作场景，建议评估纳入 roadmap |
| [#1273](https://github.com/netease-youdao/LobsterAI/issues/1273) sql.js WASM 内存崩溃及数据库损坏风险 | Bug（数据安全） | 2026-04-02 | ⚠️ 今日被关闭，但涉及数据安全，建议确认是否已修复或已有替代方案 |
| [#2452](https://github.com/netease-youdao/LobsterAI/pull/2452) 修复斜杠模型 ID 的 provider 保留 | PR | 2026-08-07 | 🟡 待合并，建议尽快 review 合入下个版本 |

---

> **分析师总结：** 项目整体处于活跃迭代状态，对社区反馈的响应速度值得肯定。建议维护者关注 4 月份 stale Issue 的关闭是否合理（尤其 #1273 涉及数据安全），并在下个版本合入 #2452 以解决模型 ID 兼容性问题。
>
> *数据截止：2026-08-08 00:00 UTC*

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

# CoPaw 项目动态日报 — 2026-08-08

> 数据来源：[github.com/agentscope-ai/CoPaw](https://github.com/agentscope-ai/CoPaw) | 数据窗口：2026-08-07 ~ 2026-08-08


## 1. 今日速览

过去24小时项目保持**高活跃度**：共产生 31 条 Issue 更新（其中新开/活跃 20 条）和 49 条 PR 更新（其中待合并 27 条），并发布 1 个新版本 `v2.1.0-beta.2`。社区反馈以 **Windows 桌面版稳定性问题**（文本无法选中复制、安装被文件占用阻塞）和 **Telegram/多任务场景下 ACL 白名单丢失** 为两大焦点，两者均已出现对应修复 PR。同时，`doom loop` 类重复调用防护问题在多个相关 Issue 中持续发酵，但核心修复进展仍待观察。整体来看，项目迭代节奏快，社区参与度高，但 **2.0.1 稳定版的若干回归问题（插件市场不可用、MCP 工具失效、空闲卡死）仍是用户迁移的主要阻力**。


## 2. 版本发布

### v2.1.0-beta.2
- **链接**: https://github.com/agentscope-ai/QwenPaw/releases
- **主要更新**:
  - `fix(ci)`: 修复 real-behavior-proof 中 fence-aware section extraction 问题（修复 #6626）— [PR #6653](https://github.com/agentscope-ai/QwenPaw/pull/6653)
  - `fix(checkpoints)`: 修复 web workspace bootstrap 中自动快照恢复问题 — [PR #6](https://github.com/agentscope-ai/QwenPaw/pull/6)

- **破坏性变更与迁移提示**:
  - 无明确的破坏性变更说明。但社区反馈显示 **v2.1.0b2 桌面模式存在文本无法选中复制的问题**（[Issue #6797](https://github.com/agentscope-ai/QwenPaw/issues/6797)），且 **Profile 分类功能出现回归**，自定义 persona 文件无法切换（[Issue #6785](https://github.com/agentscope-ai/QwenPaw/issues/6785)），建议升级前备份 workspace 根目录下的自定义 `.md` 文件。
  - **Windows 用户升级提示**：多位用户反馈从 b1 升级到 b2 时出现 NSIS 安装器报错（“无法打开要写入的文件”），根因与浏览器扩展 NM host 锁文件占用安装目录有关，详见 [Issue #6810](https://github.com/agentscope-ai/QwenPaw/issues/6810)。


## 3. 项目进展

今日无核心 PR 被合并，但以下 **22 条 PR 已关闭/合并**，其中值得关注的有：

| PR | 说明 |
|---|---|
| [PR #4694](https://github.com/agentscope-ai/QwenPaw/pull/4694) `feat(website): downloads UI Refactoring and opt` | 官网下载页 UI 重构完成（5/26 启动，今日关闭） |
| [PR #6564](https://github.com/agentscope-ai/QwenPaw/pull/6564) `fix(memory): flush pending turns before compression (#6555)` | Wait — 此 PR 状态实际为 `[Under Review]`，非合并。特此更正。 |

**实际确认合并/关闭的 PR 中**，多数为自动化机器人操作或低优先级任务。核心进展主要体现在以下 **待合并 PR** 中，它们已获得 review 并接近合入状态：

- [PR #6615](https://github.com/agentscope-ai/QwenPaw/pull/6615) `fix(config): handle corrupted agent config and invalid JSON in load_agent_config` — **Under Review**，修复配置文件损坏导致启动崩溃的问题
- [PR #6617](https://github.com/agentscope-ai/QwenPaw/pull/6617) `fix(providers): honor the Retry-After cap on the streaming retry path` — **Under Review**，流式重试策略修复
- [PR #6623](https://github.com/agentscope-ai/QwenPaw/pull/6623) `fix(acp): prevent final text loss when notifications race the prompt response` — **Under Review**，ACP 协议竞态条件修复
- [PR #6715](https://github.com/agentscope-ai/QwenPaw/pull/6715) `feat(onebot): handle remote inbound voice and image media` — **Under Review**，OneBot 通道支持远程媒体 URL

**今日新增的 8 条 PR 中**，有 5 条为 first-time-contributor 提交，显示社区参与度在提升。其中 [PR #6800](https://github.com/agentscope-ai/QwenPaw/pull/6800) `feat(mailbox)` 提出了一个**完整的智能邮件管理助手**新功能，值得关注。


## 4. 社区热点

### 热点 1: Telegram ACL 白名单丢失（双 Issue + 双 PR）
- [Issue #6786](https://github.com/agentscope-ai/QwenPaw/issues/6786)（OPEN，4 评论）
- [Issue #6787](https://github.com/agentscope-ai/QwenPaw/issues/6787)（CLOSED，重复提交）
- **修复 PR**: [PR #6788](https://github.com/agentscope-ai/QwenPaw/pull/6788) `fix: use shared root profile workspace for ACL store, not per-task workspace`

**分析**：当 multica-daemon 通过 ACP 协议启动新任务时，每个任务使用独立的 workspace，导致 `access_control.json` 变为空白，所有已批准用户被强制下线。**已在当日出现修复 PR**，响应迅速。用户 `niudakok` 连续提交了两个 Issue（其中一个被标记为重复），反映出此问题对其工作流的严重干扰。

### 热点 2: 桌面模式文本无法选中复制
- [Issue #6797](https://github.com/agentscope-ai/QwenPaw/issues/6797)（CLOSED，3 评论）
- **修复 PR**: [PR #6801](https://github.com/agentscope-ai/QwenPaw/pull/6801) `fix(os): restore text selection and copy in OS desktop window content`（根因：`useOsStyles.ts` 设置了 `user-select: none`）
- **修复 PR**: [PR #6802](https://github.com/agentscope-ai/QwenPaw/pull/6802) `fix: restore desktop window text selection`（由另一位贡献者独立修复）

**分析**：v2.1.0b2 引入的回归问题，两位贡献者（`zhijianma` 和 `zhaozhuang521`）几乎同时提交了修复 PR，其中一个 PR 已定位到具体根因。同时用户 `Jasonsun77` 还反馈了桌面模式需要**双击**才能打开应用的问题（[Issue #6790](https://github.com/agentscope-ai/QwenPaw/issues/6790)，已关闭）。

### 热点 3: Doom loop 防护机制失效
- [Issue #6116](https://github.com/agentscope-ai/QwenPaw/issues/6116)（CLOSED，wontfix，8 评论）
- [Issue #6768](https://github.com/agentscope-ai/QwenPaw/issues/6768)（OPEN，need-info，1 评论）
- [Issue #6773](https://github.com/agentscope-ai/QwenPaw/issues/6773)（CLOSED，1 评论）

**分析**：用户 `feng183043996` 在 7 月报告的 doom loop 问题（同一工具重复调用 6 次才触发警示）被标记为 wontfix，但 8 月 6 日又出现了**更严重的变体**（[Issue #6768](https://github.com/agentscope-ai/QwenPaw/issues/6768)）：agent 完成任务后陷入死循环，会话被阻塞数小时。同时 Linux 用户报告 `/goal`、`/mission` 模式下的防护完全无效（[Issue #6773](https://github.com/agentscope-ai/QwenPaw/issues/6773)）。**目前尚无针对性的 fix PR**，建议维护者重新评估 #6116 的 wontfix 决定。


## 5. Bug 与稳定性

### 严重（P0/P1）

| Bug | 影响 | 状态 | 修复 PR |
|---|---|---|---|
| **doom loop 死循环导致会话阻塞数小时** [Issue #6768](https://github.com/agentscope-ai/QwenPaw/issues/6768) | 多步骤任务完成后 agent 进入死循环，用户消息不再被处理 | OPEN（need-info） | ❌ 无 |
| **Windows 安装/更新被文件占用阻塞** [Issue #6810](https://github.com/agentscope-ai/QwenPaw/issues/6810) | b1→b2 升级失败，NSIS 报错“无法打开要写入的文件”（python.exe、VCRUNTIME140.dll 等） | OPEN | ❌ 无（建议先手动杀进程） |
| **MCP 工具规律性失效** [Issue #6732](https://github.com/agentscope-ai/QwenPaw/issues/6732) | 每隔数小时 MCP 工具无法调用，重启 Docker 后恢复 | OPEN | ❌ 无 |
| **2.0.1 空闲卡死** [Issue #6780](https://github.com/agentscope-ai/QwenPaw/issues/6780) | 闲置几十分钟后进程卡死，只能强制重启 | OPEN | ❌ 无 |
| **Agent Kanban 创建 Issue 返回 405** [Issue #6794](https://github.com/agentscope-ai/QwenPaw/issues/6794) | 看板无法创建 Issue，热重载期间 404 | OPEN | ❌ 无 |

### 中等问题（P2）

| Bug | 影响 | 状态 | 修复 PR |
|---|---|---|---|
| **Gemini API 因 $schema 多余字段报错** [Issue #6812](https://github.com/agentscope-ai/QwenPaw/issues/6812) | Google Gemini 模型无法执行 | OPEN | ❌ 无 |
| **OpenAI-compatible 严格提供商拒绝请求** [Issue #6803](https://github.com/agentscope-ai/QwenPaw/issues/6803) | StepFun 等严格校验 content structure 的服务商返回 400 | OPEN | ✅ [PR #6809](https://github.com/agentscope-ai/QwenPaw/pull/6809) |
| **Profile 自定义 persona 文件无法切换（回归）** [Issue #6785](https://github.com/agentscope-ai/QwenPaw/issues/6785) | Files 页面硬编码官方 persona，忽略自定义 .md | OPEN | ✅ [PR #6808](https://github.com/agentscope-ai/QwenPaw/pull/6808) |
| **Malware Bytes 报毒** [Issue #6775](https://github.com/agentscope-ai/QwenPaw/issues/6775) | Windows 桌面版被 Trojan Loader 标记（待确认是否误报） | OPEN | ❌ 无 |
| **OCR/响应续写摘要 ignore disable_thinking** [Issue #6811](https://github.com/agentscope-ai/QwenPaw/issues/6811) | 60 秒取消被误报为 malformed output | OPEN | ❌ 无 |
| **agentscope 2.x 下 auto-title 生成 KeyError** [Issue #6813](https://github.com/agentscope-ai/QwenPaw/issues/6813) | Chat 自动标题生成失败 | OPEN | ❌ 无 |
| **Windows 版 qwenpaw-creator 插件不可用** [Issue #6806](https://github.com/agentscope-ai/QwenPaw/issues/6806)、[Issue #6807](https://github.com/agentscope-ai/QwenPaw/issues/6807) | 模型配置无法保存、视频/图片生成不可用 | OPEN | ❌ 无 |

### 已修复/关闭

- [Issue #6782](https://github.com/agentscope-ai/QwenPaw/issues/6782)（插件市场维护中）— 仍为 OPEN
- [Issue #6619](https://github.com/agentscope-ai/QwenPaw/issues/6619)（ToolCallBlock extra_content 崩溃）— 已关闭
- [Issue #6565](https://github.com/agentscope-ai/QwenPaw/issues/6565)（多行命令换行符被折叠）— 已关闭
- [Issue #6480](https://github.com/agentscope-ai/QwenPaw/issues/6480)（nohup 后台进程卡住）— 已关闭
- [Issue #6796](https://github.com/agentscope-ai/QwenPaw/issues/6796)（b2 无法在新会话中提交）— 已关闭
- [Issue #6789](https://github.com/agentscope-ai/QwenPaw/issues/6789)（GitHub 401 无法解绑）— 已关闭


## 6. 功能请求与路线图信号

### 高优先级信号（已有 PR 或维护者关注）

| 功能 | 来源 | 状态 |
|---|---|---|
| **Telegram ACL 白名单跨任务共享** | [Issue #6786](https://github.com/agentscope-ai/QwenPaw/issues/6786) | ✅ [PR #6788](https://github.com/agentscope-ai/QwenPaw/pull/6788) 修复 |
| **自定义 Profile Markdown 文件显示** | [Issue #6785](https://github.com/agentscope-ai/QwenPaw/issues/6785) | ✅ [PR #6808](https://github.com/agentscope-ai/QwenPaw/pull/6808) 修复 |
| **严格 OpenAI-compatible 提供商兼容** | [Issue #6803](https://github.com/agentscope-ai/QwenPaw/issues/6803) | ✅ [PR #6809](https://github.com/agentscope-ai/QwenPaw/pull/6809) |
| **微信中文审批回复** | [Issue #6728](https://github.com/agentscope-ai/QwenPaw/issues/6728) | ✅ [PR #6804](https://github.com/agentscope-ai/QwenPaw/pull/6804) `feat(wechat): accept Chinese approval replies` |

### 中优先级信号（社区呼声较高，尚无 PR）

| 功能 | 来源 | 分析 |
|---|---|---|
| **增加 Volcengine Agent Plan 和 Xiaomi MiMo 内置 Provider** | [Issue #6490](https://github.com/agentscope-ai/QwenPaw/issues/6490) | 4 条评论，用户 `TinyBai` 提供了完整 API endpoint 信息 |
| **支持 qwen3.8-max-preview 模型** | [Issue #6285](https://github.com/agentscope-ai/QwenPaw/issues/6285) | Aliyun Token Plan 已支持，桌面端硬编码模型列表未更新（仅到 qwen3.7） |
| **Chrome 标签页生命周期可配置** | [Issue #6770](https://github.com/agentscope-ai/QwenPaw/issues/6770) | 用户希望跨响应周期保持浏览器标签 |
| **桌面模式单击打开应用** | [Issue #6790](https://github.com/agentscope-ai/QwenPaw/issues/6790) | 已关闭但需求明确，属于 UX 改进 |
| **智能邮件管理助手** | [PR #6800](https://github.com/agentscope-ai/QwenPaw/pull/6800) | 新贡献者提交的完整功能（多邮箱接收、分类、自动回复） |

### 路线图判断

ReMe 记忆增强配置（[PR #6772](https://github.com/agentscope-ai/QwenPaw/pull/6772)）仍在 review 中，该 PR 引入了 embedding 生命周期管理、Daily Paper 定时简报等能力，若合入将是 v2.1.0 的重要功能增量。整体来看，**v2.1.0 的重点在稳定性修复**（doom loop 防护、配置健壮性、通道兼容性），**v2.2 可能侧重功能扩展**（新 Provider、邮件助手、ReMe 增强）。


## 7. 用户反馈摘要

### 安装/升级体验（不满意）
- **Windows 升级反复失败**（[Issue #6810](https://github.com/agentscope-ai/QwenPaw/issues/6810)）：「v2.1.0b1 自动更新时报错卡死，只能强制退出」「NSIS 连续弹出不止 4 个『无法打开要写入的文件』错误」
- **安全软件误报疑虑**（[Issue #6775](https://github.com/agentscope-ai/QwenPaw/issues/6775)）：用户 `boktoday`（英文用户）表示「I'm uninstalling until I hear back from your team」，对 Malware Bytes 标记 Trojan Loader 表示担忧，并提到 Alibaba 安全漏洞报告页面「way too confusing」

### 稳定性痛点（不满意）
- **空闲卡死**（[Issue #6780](https://github.com/agentscope-ai/QwenPaw/issues/6780)）：「不使用时几十分钟后自己会卡死，只能关闭进程重新启动」
- **MCP 工具失效**（[Issue #6732](https://github.com/agentscope-ai/QwenPaw/issues/6732)）：「每隔一些时间（可能是一个晚上或者几个小时），mcp工具就无效了」「重启 docker 容器后就能恢复」
- **Doom loop 资源浪费**（[Issue #6116](https://github.com/agentscope-ai/QwenPaw/issues/6116)）：「many API calls and tokens have been wasted」

### 功能使用反馈（部分满意）
- **Desktop 模式文本选择**（[Issue #6797](https://github.com/agentscope-ai/QwenPaw/issues/6797)）：「无法选中某句话或者某个词复制，只能点击复制整段话」— 已得到快速响应，双 PR 修复
- **中文审批**（[PR #6804](https://github.com/agentscope-ai/QwenPaw/pull/6804)）：微信用户可以直接回复“允许/拒绝”，改善中文用户使用体验


## 8. 待处理积压

### 长期未响应/需要关注

| 项目 | 创建时间 | 天数 | 说明 |
|---|---|---|---|
| [Issue #6490](https://github.com/agentscope-ai/QwenPaw/issues/6490) `feat: Add Volcengine Agent Plan and Xiaomi MiMo Standard API as built-in providers` | 07-27 | 12 天 | 4 条评论，无维护者回应 |
| [Issue #6285](https://github.com/agentscope-ai/QwenPaw/issues/6285) `feat: qwen3.8-max-preview in Aliyun Token Plan` | 07-20 | 19 天 | 3 条评论，无维护者回应 |
| [PR #6694](https://github.com/agentscope-ai/QwenPaw/pull/6694)（如有） | — | — | — |
| [Issue #6732](https://github.com/agentscope-ai/QwenPaw/issues/6732) `MCP 工具规律性失效` | 08-06 | 2 天 | 高影响力 bug，暂无回应 |
| [Issue #6780](https://github.com/agentscope-ai/QwenPaw/issues/6780) `空闲后卡死` | 08-07 | 1 天 | 暂无回应 |
| [Issue #6768](https://github.com/agentscope-ai/QwenPaw/issues/6768) `doom loop 变体 - 会话阻塞数小时` | 08-06 | 2 天 | 高严重性，无 fix PR |
| [PR #6688](https://github.com/agentscope-ai/QwenPaw/pull/6688) `fix(plugins): isolate bare absolute imports per plugin namespace` | 08-04 | 4 天 | 修复插件安装失败问题（#6683），first-time-contributor，待 review |

### 维护建议

1. **重新评估 #6116 的 wontfix 决定** — #6768 表明 doom loop 问题在复杂任务场景下仍会造成严重故障（阻塞数小时），建议至少补充针对“任务完成后进入死循环”场景的护栏。
2. **对 Windows 安装器增加文件占用检测** — #6810 是 b1→b2 升级的普遍性问题，建议在 NSIS 脚本中预检并提示用户关闭相关进程（尤其是浏览器扩展 NM host）。
3. **及时回应 #6732 和 #6780** — 这两个问题影响 2.0.1 Docker/桌面用户的核心使用体验，且都有“重启后恢复”的特征，可能指向相同的运行时资源回收缺陷。
4. **关注插件生态的 Windows 兼容性** — #6806/#6807 连续两个 qwenpaw-creator 相关问题，均为 Windows 平台，提示插件框架的跨平台测试可能不足。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-08-08

## 1. 今日速览

ZeroClaw 项目过去 24 小时保持了极高的社区活跃度，共计 50 条 Issue 更新与 50 条 PR 更新。其中值得关注的是，今日新增了多个 P1 严重级别 Bug 报告，主要集中在安全策略绕过、预算控制失效和 SOP 执行引擎语义错误等核心领域。值得肯定的是，社区贡献者反应迅速，多个 Bug 在报告当日即有对应修复 PR 提交。此外，PR 队列中堆积了 47 个待合并 PR，其中多涉及安全加固与功能增强，建议维护者优先处理安全相关 PR。项目整体呈现高活跃度、高风险积压并存的态势。

> **趋势观察**: 近期 Issue 集中在 Agent Plugins 标准支持、统一包/能力/配置目录契约、SOP 执行引擎语义修复和安全策略深度加固等方向。其中安全相关 Issue 和 PR 数量显著上升，涉及密钥泄漏、路径逃逸、命令注入等多个维度，说明随着项目用户规模扩大，安全攻防对抗已成为社区关注的核心议题之一，且已催生多个高价值加固 PR。`web_research`/`web_search` 重构系列 PR 也已具雏形，方向明确。


## 2. 版本发布

过去 24 小时内无新版本发布。上一个已知版本为 v0.8.4（预编译 aarch64 版本在社区流传）。


## 3. 项目进展

过去 24 小时仅合入/关闭 3 个 PR，其余 47 个 PR 仍在待合并阶段。重点合并内容包括：

- **[#9836](https://github.com/zeroclaw-labs/zeroclaw/pull/9836) fix(transcription): 使 local_whisper 的 bearer_token 变为可选** — 修复了本地 whisper.cpp 服务（无认证）在缺少 token 时硬失败的问题。该 PR 涉及面极广（ci/docs/core/agent/channel/config/cron/daemon/heartbeat/memory/runtime/service/tool/tests/scripts 等多个模块），疑似为自动化批量修改或分支基准问题，虽已合入但建议维护者留意其改动范围是否超预期。

**尚未合并的关键 PR 预览**（高优先级）：

- **[#9841](https://github.com/zeroclaw-labs/zeroclaw/pull/9841) fix(sop): 驱动 headless SOP 运行并修复 review 发现的五个缺陷** — 续接 #9494，解决 cron 触发的 SOP 在 auto 模式下永远无法执行的问题。**直接对应今日热点 Issue #9805**。
- **[#9839](https://github.com/zeroclaw-labs/zeroclaw/pull/9839) feat(security): 在所有模式下禁止不可逆破坏性命令** — 修复 `allowed_commands: ["*"]` 配合 `block_high_risk_commands: false` 时的短接问题。
- **[#9827](https://github.com/zeroclaw-labs/zeroclaw/pull/9827) fix(security): 阻止 shell 子进程逃逸已验证的隔离环境** — 三个独立的 shell 隔离修复。
- **[#9828](https://github.com/zeroclaw-labs/zeroclaw/pull/9828) feat(tools): agent 面向的配置编写 + operator 审批策略预览** — 替代 `echo > config.toml` 的危险做法。
- **[#9833](https://github.com/zeroclaw-labs/zeroclaw/pull/9833) feat(tools): 新增 web_research delegate，将原始 web_search 限定到子代理** — 对应 Issue #9824 的方案实现。

整体来看，SOP 引擎修复、安全策略加固、工具面精简三条主线正在同步推进，但合入速度远低于提交速度。


## 4. 社区热点

今日讨论最活跃的 Issue 集中在以下几个（除已关闭的 #8933 与 #9246 外）：

- **[#9246](https://github.com/zeroclaw-labs/zeroclaw/issues/9246) RFC: 保留 ZeroCode 所有权迁移期间的 Todo 跟踪器配置** — 12 条评论，已关闭。涉及配置迁移的完整性与向后兼容问题，与 #9013 相关联。
- **[#5937](https://github.com/zeroclaw-labs/zeroclaw/issues/5937) [Feature]: 重构 providers 架构与 reqwest 客户端管理** — 12 条评论，自 4 月 20 日创建以来长期活跃，反映社区对 providers 模块代码重复和配置碎片化的普遍不满。
- **[#8424](https://github.com/zeroclaw-labs/zeroclaw/issues/8424) RFC: 工作区相对 forbidden path 模式与可选 .zeroclawignore** — 10 条评论，与 #9815（forbidden_paths 不可达）直接相关。
- **[#8043](https://github.com/zeroclaw-labs/zeroclaw/issues/8043) RFC: 退役独立 aardvark-sys crate（并入 zeroclaw-hardware）** — 9 条评论，与 #7130（forbid unsafe_code）和 #9832（hardware 编译失败）形成联动。
- **[#9426](https://github.com/zeroclaw-labs/zeroclaw/issues/9426) RFC: 统一集成目录** — 与 #9810（Agent Plugins 加载）和 #9346（包/能力/配置目录契约）并列为生态扩展核心提案。
- **[#8933](https://github.com/zeroclaw-labs/zeroclaw/issues/8933) RFC: 为 OTel 导出增加跨轮次对话关联** — 13 条评论，已关闭，说明该增强已获得接受并可能进入实现阶段。

**核心诉求分析**：社区讨论集中在三大主题 — ① 安全策略的可靠性和可预测性（forbidden_paths 失效、密钥泄漏）；② 架构现代化（providers 统一、aardvark-sys 合并）；③ 标准化集成（Agent Plugins、统一目录契约）。这些讨论共同指向一个核心诉求：**ZeroClaw 作为 AI 智能体框架，正在从"能用"走向"规模化可治理、可扩展、可观测"** — 社区希望有清晰的第三方生态入口和更细粒度的安全控制，同时通过统一架构降低维护成本。


## 5. Bug 与稳定性

### P1 严重级别

| Issue | 描述 | 状态 | 对应修复 |
|-------|------|------|----------|
| [#9815](https://github.com/zeroclaw-labs/zeroclaw/issues/9815) | `forbidden_paths` 对 `allowed_roots` 或 workspace 下的路径**完全无效**（安全策略实质失效） | OPEN, accepted | 待确认 |
| [#9816](https://github.com/zeroclaw-labs/zeroclaw/issues/9816) | Anthropic provider 的 `cost_usd` 恒为 0.0，导致**日/月预算上限永远不会触发** | OPEN, accepted | 待确认 |
| [#9805](https://github.com/zeroclaw-labs/zeroclaw/issues/9805) | SOP auto 模式从 channel/cron 触发后**永远停在第 1 步**，占用并发槽位不释放 | OPEN, accepted | [#9841](https://github.com/zeroclaw-labs/zeroclaw/pull/9841) 已提交 |
| [#9786](https://github.com/zeroclaw-labs/zeroclaw/issues/9786) | 畸形 `SOP.toml` 被**静默丢弃**，`sop list`/`validate` 均无法诊断 | OPEN | 待确认 |
| [#9770](https://github.com/zeroclaw-labs/zeroclaw/issues/9770) | `cron update` **静默丢弃** declarative job 的六列更改 | OPEN, accepted | 待确认 |
| [#9840](https://github.com/zeroclaw-labs/zeroclaw/issues/9840) | 第二个 daemon 启动会 **steal/删除现有 daemon.sock**，使活跃 daemon 失联 | OPEN | 待确认 |
| [#9386](https://github.com/zeroclaw-labs/zeroclaw/issues/9386) | Gemini API key 通过 URL 查询参数传递，错误消息中**密钥泄漏到聊天** | CLOSED (accepted) | 待确认 |

### P2 严重级别

| Issue | 描述 | 状态 |
|-------|------|------|
| [#9708](https://github.com/zeroclaw-labs/zeroclaw/issues/9708) | daemon 服务启动器的 stdout/stderr 日志**无大小/数量限制** | OPEN, in-progress |
| [#9775](https://github.com/zeroclaw-labs/zeroclaw/issues/9775) | OpenRouter streaming 请求**丢弃 `provider_extra`** 配置 | OPEN, in-progress |
| [#9656](https://github.com/zeroclaw-labs/zeroclaw/issues/9656) | Telegram 输入状态指示器在审批等待期间**一直显示"正在输入"** | OPEN, accepted |
| [#9783](https://github.com/zeroclaw-labs/zeroclaw/issues/9783) | `finish_run` 接受失败原因参数但**丢弃该参数** — 失败原因永远不记录 | OPEN |
| [#9784](https://github.com/zeroclaw-labs/zeroclaw/issues/9784) | 多步 SOP 运行在步骤执行中途**被标记失败，且无任何审计事件** | OPEN, needs-repro |
| [#9834](https://github.com/zeroclaw-labs/zeroclaw/issues/9834) | `zeroclaw-runtime` 测试因**进程全局共享状态**间歇性失败 | OPEN |
| [#9832](https://github.com/zeroclaw-labs/zeroclaw/issues/9832) | `--features hardware` 编译失败：`aardvark_sys::AardvarkHandle` 无法解析（aarch64） | OPEN |

### 中低危

| Issue | 描述 | 状态 |
|-------|------|------|
| [#9825](https://github.com/zeroclaw-labs/zeroclaw/issues/9825) | 泄漏检测的熵启发式算法**将公共区块链地址误判为密钥**，导致支付链接无法投递 | OPEN |
| [#9821](https://github.com/zeroclaw-labs/zeroclaw/issues/9821) | Agent 从不调用 cron 工具，总是回退到被策略拦截的 shell "crontab" | OPEN |
| [#9820](https://github.com/zeroclaw-labs/zeroclaw/issues/9820) | 模型（nemotron）输出字面量 `<TOOLCALL>` 伪语法而非真正的函数调用 | OPEN |
| [#9780](https://github.com/zeroclaw-labs/zeroclaw/issues/9780) | cron 触发的 SOP 无法进行任何网络工作（无 HTTP 能力） | OPEN |


## 6. 功能请求与路线图信号

**高确定性 — 已有对应 PR 或 RFC 被接受**：

1. **Agent Plugins 1.0 标准支持**（[#9810](https://github.com/zeroclaw-labs/zeroclaw/issues/9810)）— 加载 `plugin.json + skills/ + mcp.json` 格式的社区插件。与 #9346（统一目录契约）和 #9426（统一集成目录）形成生态扩展矩阵。**方向明确，跨版本可能性高**。
2. **Web 工具面精简**（[#9824](https://github.com/zeroclaw-labs/zeroclaw/issues/9824) + [#9833](https://github.com/zeroclaw-labs/zeroclaw/pull/9833)）— 默认仅保留 `web_fetch` + `web_research` + `http_request`，将原始 `web_search` 收敛到子代理、浏览器自动化改为显式 opt-in。已有 PR 实现。
3. **统一包/能力/配置/运行时状态目录契约**（[#9346](https://github.com/zeroclaw-labs/zeroclaw/issues/9346)）— 产品级统一目录，打通 CLI、网关和插件的插件视图，仍处于 RFC 阶段。
4. **Agent 配置编写能力**（[#9828](https://github.com/zeroclaw-labs/zeroclaw/pull/9828)）— 让 agent 通过受控的 JSON Patch 机制修改配置，而非直接写文件。

**中等确定性 — RFC 讨论中**：

- **跨轮次对话关联的 OTel 导出**（#8933）— 已关闭（accepted），预计进入实现阶段。
- **工作区相对 forbidden path + .zeroclawignore**（[#8424](https://github.com/zeroclaw-labs/zeroclaw/issues/8424)）—与 #9815 的修复直接相关。
- **Herdr agent 状态集成**（[#8337](https://github.com/zeroclaw-labs/zeroclaw/pull/8337)）— 让 Herdr 侧边栏显示 agent 生命周期。

**潜在方向（信号较弱）**：

- **Telegram 工具调用进度显示**（#6663）— `update_draft_progress` 支持。
- **Slack 线程上下文回填**（#6055）— 已关闭，功能已获接受。


## 7. 用户反馈摘要

**来自 Raspberry Pi 用户的真实痛点**（#9820/#9821/#9832，aarch64 平台）：

> 用户 `fabricioartur` 在使用预编译 aarch64 版本 + NVIDIA NIM 模型时连续遇到三个问题：① 模型输出字面量 `<TOOLCALL>` 伪语法而非标准函数调用；② cron 工具从未被 agent 主动调用，总是回退到被策略拦截的 `shell "crontab"`；③ `--features hardware` 编译失败。这些反馈指向一个共同问题：**工具调用协议的模型兼容层在非标准模型上缺乏降级/警示机制**，函数调用的格式假设在不同模型系列间过于脆弱。此外，硬件相关代码在 aarch64 目标上存在明显的条件编译覆盖不足。

> `#9821` 中的 cron 工具调用失败还揭示了一个深层问题：**agent 倾向于使用最直接的 shell 方式而非注册工具**。这可能意味着工具发现的提示词引导不足，或工具调用的奖励/惩罚机制不够明确 — 即使 `cron` 已在 `allowed_tools` 中列出，模型仍选择 shell 方式并被策略拦截。

**安全策略的实际失效案例**（#9815）：

> `bitsbyritik` 报告 `forbidden_paths` 对 workspace 内部文件完全无效，因为 `is_path_allowed` 在 `allowed_roots` 检查处提前返回 `true`。这意味着用户配置的 `.env`、`config.yaml` 等敏感文件保护形同虚设。**该 Issue 与工作区相对 forbidden path RFC（#8424）形成互补，优先级应当拉高。**

**成本控制的核心缺陷**（#9816）：

> `bitsbyritik` 指出 Anthropic provider 的 `cost_usd` 始终为 0.0，预算控制完全失效。这不仅影响账单展示，更严重的是**当用户的预算阈值依赖该数据时，实际不会触发任何告警或限制**，可能导致用户被迫面对意外的超额费用。

**SOP 引擎的可靠性担忧**（#9786/#9805/#9783/#9784）：

> `JordanTheJet` 连续提交了四个 SOP 相关 Bug，覆盖从配置解析（畸形 SOP.toml 静默丢弃）、执行引擎（auto 模式永远卡住）、状态记录（失败原因被丢弃）到审计（无事件标记失败）的全链路问题。此外，`Pratiikpy` 指出 cron 触发的 SOP 缺乏网络能力，使"watch-loop"的使用场景根本无法实现。**SOP 作为 ZeroClaw 的自动化编排核心，目前成熟度仍不足以支撑文档中承诺的复杂场景。**

**Telegram 审批体验问题**（#9656）：

> `ZiBibro` 报告 Telegram 的 typing 指示器在整个审批等待期间持续运行，使用户误以为 agent 仍在工作。这是渠道层 UX 的精细问题，但也反映了 **异步审批流程在渠道层的体验设计仍处于初期阶段**。


## 8. 待处理积压

### 长期未响应/未解决的高价值 Issue

| Issue | 创建时间 | 核心内容 | 备注 |
|-------|----------|----------|------|
| [#5937](https://github.com/zeroclaw-labs/zeroclaw/issues/5937) | 2026-04-20（110 天） | providers 架构统一与 reqwest 客户端管理重构 | 12 条评论，讨论充足但无明确行动者。长期搁置可能加剧架构债务，影响后续 provider 扩展效率 |
| [#7130](https://github.com/zeroclaw-labs/zeroclaw/issues/7130) | 2026-06-03（66 天） | 全工作区 `forbid(unsafe_code)`，仅 aardvark-sys 豁免 | 与 #9832（硬件编译失败）和 #8043（aardvark 并入）直接相关。建议与 #8043 合并推进，避免重复劳动 |
| [#8043](https://github.com/zeroclaw-labs/zeroclaw/issues/8043) | 2026-06-20（49 天） | 退役独立 aardvark-sys crate | RFC 已讨论充分，涉及 workspace 级 `unsafe` 治理（#7130）和硬件编译稳定性（#9832），需 maintainer 决策 |
| [#8424](https://github.com/zeroclaw-labs/zeroclaw/issues/8424) | 2026-06-28（41 天） | 工作区相对 forbidden path + .zeroclawignore | 与 P1 Bug #9815 直接相关 — 用户对安全边界的需求已从问题升级为明确的缺陷报告 |
| [#9346](https://github.com/zeroclaw-labs/zeroclaw/issues/9346) | 2026-07-24（15 天） | 统一包/能力/配置/运行时状态目录契约 | 是 #9810（Agent Plugins）和 #9426（统一集成目录）的架构底座，建议优先对齐路线图 |

### 待合并的关键 PR

| PR | 核心改动 | 关联 Issue | 备注 |
|----|----------|-----------|------|
| [#9841](https://github.com/zeroclaw-labs/zeroclaw/pull/9841) | SOP headless 运行驱动 + 5 个缺陷修复 | #9805, #9786, #9783 | 直接解锁 cron/channel 触发 SOP 的核心场景 |
| [#9839](https://github.com/zeroclaw-labs/zeroclaw/pull/9839) | 所有模式下禁止不可逆破坏性命令 | 安全策略 | 防御 `rm -rf` 类风险，属安全加固 |
| [#9827](https://github.com/zeroclaw-labs/zeroclaw/pull/9827) | 阻止 shell 子进程逃逸已验证的隔离环境 | 安全策略 | 与 #9839 同属 shell 安全加固系列 |
| [#9828](https://github.com/zeroclaw-labs/zeroclaw/pull/9828) | agent 配置编写 + operator 审批 | 安全策略 | 为 agent 提供受控的配置修改路径 |
| [#9833](https://github.com/zeroclaw-labs/zeroclaw/pull/9833) | web_research delegate 工具 | #9824 | 工具面精简的第一步 |
| [#9835](https://github.com/zeroclaw-labs/zeroclaw/pull/9835) | 根包改名为 `zeroclaw` | — | 发布前需完成的清理工作，越早合入越好 |
| [#9384](https://github.com/zeroclaw-labs/zeroclaw/pull/9384) | shell 命令路径参数解析以阻止符号链接逃逸 | 安全策略 | P1 安全修复，已停留 13 天 |

### 维护者行动建议（按优先级）

1. **安全修复优先**：合入 #9839 → #9827 → #9384 → #9838，关闭安全策略绕过的已知路径。
2. **SOP 引擎修复**：合入 #9841（附带 #9494 的 rebase），并跟进 #9786、#9783、#9784 的修复。
3. **成本数据修复**：确认 #9816 的修复方案（Anthropic usage API 的 cost 字段解析问题）。
4. **架构决策**：就 #5937（providers 重构）在 RFC 线程中明确下一步行动者或关闭原因。就 #8043/#7130 给出合并方向。
5. **工具面精简**：合入 #9833 后评估 #9824 的完整方案（含 web_search_tool 下沉和浏览器自动化 opt-in）。

> **项目健康度总结**：社区活跃度极高（50 Issue + 50 PR / 24h），但 PR 合入率偏低（仅 3/50），P1/P2 级别 Bug 存量偏多（约 10+ P1），安全相关修复 PR 排队时间偏长。建议 maintainer 集中一个迭代窗口（sprint）优先处理安全修复与 SOP 引擎修复的合入。整体而言，项目处于社区参与热情高涨、维护者需要加速响应的关键阶段。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*