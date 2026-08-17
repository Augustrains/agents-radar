# OpenClaw 生态日报 2026-08-17

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-17 00:29 UTC

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

# OpenClaw 项目动态日报
**日期：2026-08-17**

---

## 1. 今日速览

过去24小时内，OpenClaw 项目保持高活跃度：共新增/更新 500 条 Issues（关闭 37 条）和 500 条 PR（合并/关闭 82 条），并发布了 1 个新 Release（PR #124528 的 Gateway profile 证据归档）。**值得关注的是，大量长期存在的问题（如 #44925、#48003、#121058）仍未解决，且在持续获得新评论，表明社区对消息丢失、会话状态损坏等可靠性问题的关注度极高。** 今日合并的 PR（如 #120398、#120900）主要聚焦于进程管理和安全策略确认，但核心的 session-state 和 message-loss 类问题尚未看到决定性的修复 PR 被合并。项目整体处于功能开发与稳定性修复并行的快节奏阶段。


## 2. 版本发布

### pr-124528-profiles
- **链接**: 查看 Release 详情（项目 Releases 页面）
- **内容**: 此 Release 包含 PR #124528 的 Gateway CPU profile 证据归档，从受限的三节点、十二并发轮次 Gateway 测试环境中捕获。归档中包含用于事件循环热点比较的"修复前"与"精确修复后"Gateway profile。
- **性质**: 证据归档，非功能更新，无破坏性变更。


## 3. 项目进展

今日合并/关闭的重要 PR 显示了项目在以下几个方向的推进：

- **进程管理修复（Linux 专属）**: [#120398](https://github.com/openclaw/openclaw/pull/120398) 已关闭。此 PR 修复了服务管理的工具子进程在 Linux 上未被分离的问题（关联 Issue #120386），解决了工具子进程在命令超时后不被终止的缺陷。但 Issue #120386 在 macOS/launchd 上的复现仍未解决。
- **安全策略确认机制**: [#120900](https://github.com/openclaw/openclaw/pull/120900) 已关闭。为 Control UI 增加了安装策略警告的审查功能，允许管理员在 UI 中查看并确认安装策略警告后继续插件安装。同时 [#116489](https://github.com/openclaw/openclaw/pull/116489) 也已关闭，实现外部 `security.installPolicy` 命令返回 `warn` 状态，要求操作员确认。
- **消息发送修复**: [#119681](https://github.com/openclaw/openclaw/pull/119681) 已关闭。修复了 Cron agentTurn 运行中 HEARTBEAT_OK 被附加到发送负载的问题。
- **诊断工具修复**: [#124929](https://github.com/openclaw/openclaw/pull/124929) 已关闭。修复了 `openclaw doctor --fix` 在全新安装时误报共享认证迁移的问题。

**项目整体向前迈进的步伐**：在安全性和进程管理方面有具体进展，但大量 P1 级别的可靠性问题（尤其是消息丢失和会话状态损坏）仍在积压。


## 4. 社区热点

今日讨论最活跃的 Issues 集中在**消息丢失与会话状态完整性**这一核心痛点：

- **[#121058](https://github.com/openclaw/openclaw/issues/121058) [P1, impact:message-loss] Silent reply failures still recurring after #116277 closed — no queued reply payload**（97 条评论，已关闭）：社区反馈 #116277 关闭后，静默回复失败仍在发生。监控 cron 持续记录到新案例。这引起了大量讨论，最终被关闭，但**用户侧对修复效果的不信任感十分强烈**。
- **[#44925](https://github.com/openclaw/openclaw/issues/44925) [P1, impact:message-loss, data-loss, session-state] Subagent completion silently lost — no retry, no notification, no auto-restart on timeout**（31 条评论）：子代理任务编排存在多种静默丢失结果的方式，包括完成通知失败、超时无自动重启等。
- **[#42475](https://github.com/openclaw/openclaw/issues/42475) [P2] Per-agent cost budget enforcement at the gateway level**（26 条评论）：用户希望网关层面执行单代理成本预算，防止失控支出。

此外，[#48003](https://github.com/openclaw/openclaw/issues/48003)（Steer 模式不注入消息，21 条评论）也获得了较高关注。

**诉求分析**：社区对"消息确定性交付"和"状态可恢复性"的诉求非常集中。多个高热度 Issue 都指向同一个根因：**系统在异常或边界情况下会静默丢弃消息或状态，且缺乏有效的重试、通知和恢复机制**。用户对 #116277 关闭后问题仍复现表示强烈不满，这可能是信任度下降的信号。


## 5. Bug 与稳定性

### 严重（P1，影响消息/状态完整性）

| Issue | 问题 | 状态 |
|-------|------|------|
| [#121058](https://github.com/openclaw/openclaw/issues/121058) | 静默回复失败在 #116277 关闭后仍复现 | 已关闭（评论 97），但用户反馈问题未解决 |
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | 子代理完成结果静默丢失，无重试/通知/自动重启 | 打开（31 评论），无 fix PR |
| [#96834](https://github.com/openclaw/openclaw/issues/96834) | WhatsApp 1:1 入站图片导致消息通道阻塞约 3 分钟 | 打开（15 评论），无 fix PR |
| [#87744](https://github.com/openclaw/openclaw/issues/87744) | Codex 驱动的 Telegram 轮次反复超时（2026.5.27 版本） | 打开（17 评论），无 fix PR |
| [#115908](https://github.com/openclaw/openclaw/issues/115908) | 会话转录投影在持续写入下可能活锁，阻塞主线程 | 打开（14 评论），无 fix PR |
| [#112423](https://github.com/openclaw/openclaw/issues/112423) | 大型 SQLite 转录清理阻塞网关事件循环 | 打开（11 评论），无 fix PR |
| [#50093](https://github.com/openclaw/openclaw/issues/50093) | WhatsApp 重连后错过消息不回溯 | 打开（12 评论），无 fix PR |
| [#53408](https://github.com/openclaw/openclaw/issues/53408) | 长对话后 write/exec 工具参数静默丢失 | 打开（11 评论），无 fix PR |

### 中等级别（P2，影响功能或体验）

| Issue | 问题 | 状态 |
|-------|------|------|
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | 2026.3.2 版本 google-vertex/gemini-3.1-pro-preview 报 "Cannot convert undefined or null to object" | 打开（14 评论），无 fix PR |
| [#74586](https://github.com/openclaw/openclaw/issues/74586) | AM 嵌入式运行中止 memory_search 工具调用，误报超时 | 打开（14 评论），无 fix PR |
| [#114612](https://github.com/openclaw/openclaw/issues/114612) | memory_index_chunks 和 memory_embedding_cache 表无保留策略，磁盘将被写满 | 打开（9 评论），无 fix PR |
| [#46786](https://github.com/openclaw/openclaw/issues/46786) | tools.elevated.enabled: true 破坏 exec 路由逻辑，所有调用路由到网关主机 | 打开（8 评论），无 fix PR |

### 已有 fix PR 的问题

- [#120398](https://github.com/openclaw/openclaw/pull/120398) 修复 #120386（Linux 上服务管理的工具子进程未分离）。
- [#123877](https://github.com/openclaw/openclaw/pull/123877)（打开，等待维护者查看）修复卡住会话恢复时应尊重提供方超时。

**稳定性观察**：今日新报告的严重 Bug 数量不多，但**长期存在的 P1 问题数量庞大且持续获得关注**。尤其值得注意的是，多个 P1 问题（如 #44925）同时带有 `impact:message-loss`、`impact:session-state` 和 `impact:data-loss` 标签，说明一个根因可能引发多类故障。此外，多个内存/数据库增长类问题（如 #114612）开始引起注意，可能成为未来的稳定性隐患。


## 6. 功能请求与路线图信号

### 高热度/高优先级功能请求

- **[#42475](https://github.com/openclaw/openclaw/issues/42475) 网关级单代理成本预算执行**（26 评论，P2）：用户希望防止失控支出。虽然目前没有直接关联的 fix PR，但已有 PR #124864 除了引入机器选择外，也包含成本/预算相关的 gateway 增强。值得注意的是，该功能在社区中呼声较高，可能是企业用户的核心诉求。
- **[#22438](https://github.com/openclaw/openclaw/issues/22438) 分层引导文件加载**（19 评论，P2）：用户希望按需加载引导文件，避免浪费上下文窗口。
- **[#87561](https://github.com/openclaw/openclaw/issues/87561) 定义跨渠道的持久最终回退交付语义**（11 评论，P1）：这是一个维护者标记的 Issue，旨在统一解决多个渠道静默丢消息的问题。这可能是项目未来的核心改进方向。
- **[#45508](https://github.com/openclaw/openclaw/issues/45508) 支持自托管 TTS/STT 提供方**（8 评论，P2）：用户希望 WebChat 的语音功能走网关配置而非浏览器 API。
- **[#88154](https://github.com/openclaw/openclaw/issues/88154) Slack Modal 支持**（8 评论，P2）：用户希望 Slack 集成支持原生模态框。
- **[#6757](https://github.com/openclaw/openclaw/issues/6757) Agent 触发的上下文压缩**（9 评论，P2）：代理自主触发 compact，减少人工干预。

### 可能被纳入下一版本的功能

- **会话持久性与可见性增强**：PR [#124925](https://github.com/openclaw/openclaw/pull/124925) "keep durable work visible and auto-archive stale sessions" 可能解决 #22438 的部分诉求。
- **外发消息交付审计**：PR [#123709](https://github.com/openclaw/openclaw/pull/123709) 为外发消息提供精确的交付解释，可追溯性增强，间接回应了 message-loss 类问题。

### 值得关注的尝试性 PR

- **会话权限模式（Beta 性质）**：[#124909](https://github.com/openclaw/openclaw/pull/124909) 引入会话级权限模式和 worktree 作用域默认值。此 PR 试图将全局的、基于配置的权限模型改为按会话切换，当前标记为 `⏳ waiting on author`，尚未合并。这是一个较大的架构调整，可能需要较长时间打磨。


## 7. 用户反馈摘要

- **对"静默失败"的强烈不满**：Issue #121058 的讨论中，用户明确表达了" #116277 关闭了，但问题还在"的挫败感。监控 cron 持续记录到新案例，说明修复没有真正解决问题。这种"修复后又复发"的情况严重影响了用户信任。
- **对超时和重试机制的诉求**：多个 Issue（#87744、#44925、#117609、#45494）都涉及超时后无重试或错误分类问题。用户希望系统能快速失败而不是长时间等待，或者能在瞬态错误后自动重试。
- **对配置灵活性的需求**：用户在多个 Issue 中要求更多可配置选项，如 #45501 可配置的会话启动消息、#45565 将生命周期警告路由到专用频道、#95553 希望允许配置或禁用预检压缩的超时。
- **对渠道特定功能的缺失感**：WhatsApp(#50093)、Slack(#88154)、Feishu(#48786) 等渠道各有功能缺失或 Bug 反馈，表明多渠道支持仍需打磨。
- **对 GitHub Actions 更新的关注**：一个自动化的依赖更新 PR（#117712）请求被标记为 `⏳ waiting on author`，原因是 Dependabot 正在 rebase，这可能只是例行维护，但用户也在持续跟进。


## 8. 待处理积压

以下问题长期未解决且影响重大，**建议维护者优先关注**：

### 高优先级长期未解决 Issue

- **[#44925](https://github.com/openclaw/openclaw/issues/44925) 子代理完成结果静默丢失**（31 评论，2026-03-13 创建，5 个月未解决）：这是一个核心可靠性问题，同时标记 `impact:message-loss`、`impact:data-loss`、`impact:session-state`，且被评为 `diamond lobster`。有多个关联但未闭合的子问题。
- **[#48003](https://github.com/openclaw/openclaw/issues/48003) Steer 模式不注入消息**（21 评论，2026-03-16 创建，5 个月未解决）：影响核心交互体验。
- **[#87744](https://github.com/openclaw/openclaw/issues/87744) Codex 驱动的 Telegram 轮次反复超时**（17 评论，2026-05-28 创建）。
- **[#38327](https://github.com/openclaw/openclaw/issues/38327) Gemini 3.1 Pro 回归 Bug**（14 评论，2026-03-06 创建）。
- **[#96834](https://github.com/openclaw/openclaw/issues/96834) WhatsApp 入站图片阻塞**（15 评论，2026-06-25 创建）。

### 长期未响应的 PR

- **[#104703](https://github.com/openclaw/openclaw/pull/104703) Slack 丢弃 message_changed 事件中的附件**（2026-07-11 创建，标记为 `stale` 和 `needs proof`）：影响 Slack 渠道的消息完整性，但已超过一个月没有新进展。
- **[#105617](https://github.com/openclaw/openclaw/pull/105617) 精确轮次能力投影报告**（2026-07-12 创建，标记 `needs proof`）：一个有价值的功能，但长期未获得维护者反馈。

**健康度总评**：项目活跃度极高，但**可靠性债务正在累积**。大量 P1 问题长期存在且没有明确的 fix PR，尤其是围绕消息传递和会话状态的问题，已成为社区最主要的痛点。建议项目维护者将资源集中于解决这些"diamond lobster"级别的核心可靠性问题，并考虑对 #121058 这类"修复后复发"的问题进行根因复盘。

---

## 横向生态对比

# AI 智能体开源生态横向分析报告

**报告日期：2026-08-17**


## 1. 生态全景

个人 AI 助手与自主智能体开源生态正处于**从功能扩张转向可靠性加固与平台化演进**的关键转折期。"消息确定性交付"和"状态可恢复性"已成为跨项目的第一技术债——OpenClaw 的静默丢消息（#121058）、NanoBot 的 token 估算失灵（#5402）、NanoClaw 的上下文积压（#3254）均指向同一类问题。与此同时，安全加固（SSRF 防护、白名单绕过、日志脱敏）在多个项目中密集落地，**安全不再是附加项而是准入门槛**。第三，生态开始分化：OpenClaw/ZeoClaw 向"平台+协议"演进（Chat Completions 兼容层、附件统一架构），而 NanoClaw/CoPaw 则在"多会话多代理协同"的纵深方向上加速。


## 2. 各项目活跃度对比

| 项目 | Issues（新增/关闭） | PRs（更新/合并关闭） | Release | 健康度 | 核心状态 |
|------|---------------------|----------------------|---------|--------|----------|
| **OpenClaw** | 500+/37 | 500+/82 | ✅ pr-124528-profiles | 🟡 高活跃，可靠性债务累积 | 功能与稳定性并行，P1 积压严重 |
| **NanoBot** | 11/4 | 500/1 | — | 🟡 活跃但 PR 积压 499 条 | 19 条 `[conflict]` PR 超 5 个月 |
| **Hermes Agent** | — | 50/2 | ✅ v0.20.2（397 PR 聚合） | 🟢 健康，平台工程化 | 安全隔离与多配置文件治理 |
| **PicoClaw** | 3/— | 5/— | — | 🟡 中等，SSRF 修复悬置 | 安全修复系列待合并 |
| **NanoClaw** | 1/1 | 32/13 | — | 🟢 高产收敛 | 多会话架构推进，零用户投诉 |
| **NullClaw** | — | — | — | ⚪ 无活动 | — |
| **IronClaw** | 1/— | 9/2 | — | 🟢 小步快跑 | 依赖更新为主，1 个 UX 修复 |
| **LobsterAI** | 7/3 | 17/9 | — | 🟢 安全加固密集 | 3 项安全修复合入 |
| **TinyClaw** | — | — | — | ⚪ 无活动 | — |
| **Moltis** | 2/3 | 17/16 | — | 🟡 CI 红色需清理 | 安全+新功能，外部贡献者活跃 |
| **CoPaw** | 9/3 | 9/0 | — | 🟢 提交密集，待合并积压 | 7 个新 PR 待 review |
| **ZeptoClaw** | — | — | — | ⚪ 无活动 | — |
| **ZeroClaw** | 48/2 | 50/4 | — | 🟡 高活跃，测试基础设施不稳 | 安全加固里程碑 + RFC 治理 |


## 3. OpenClaw 在生态中的定位

**优势**：
- **社区规模断层领先**：日增 500+ Issues/PRs，远超第二梯队（NanoBot 500 条 PR 但大量为积压，Hermes 50 条），活跃度一个数量级优势。
- **生态辐射力强**：多条 PR 从 openclaw 移植至其他项目（如 Hermes 的 `ironclaw`、`nanoclaw` 移植修复），实为生态的"上游"。
- **基础设施投入超前**：Gateway profile 证据归档（pr-124528）、精确轮次能力投影报告（#105617）等手段说明其在可观测性上投资领先。

**技术路线差异**：
- OpenClaw 是**全功能单体**：渠道、代理编排、记忆、安全策略一体，走"大而全"路线，但因此可靠性问题面广。
- 对比 NanoClaw 的**轻量多代理协同**（A 系列 PR 编号显示有清晰架构演进路线图）、Hermes 的**平台工程化**（多配置文件、Windows 全量支持）、ZeroClaw 的**安全/协议标准化**（ADR-013 出口加固、Chat Completions 兼容层）。

**社区信任风险**：用户对 #116277 修复后问题复现表达强烈不满，这类"修复又复发"正在侵蚀信任度，是 OpenClaw 当前最大隐患。


## 4. 共同关注的技术方向

| 方向 | 涉及项目 | 具体诉求 |
|------|----------|----------|
| **消息确定性交付** | OpenClaw（#121058）、NanoClaw（#3255）、Hermes（#87694）、IronClaw（#7681） | 静默丢消息、投递错乱、无重试/通知机制、"修复后复发" |
| **Token 成本透明与管控** | NanoBot（#5266/#5402/#5377）、OpenClaw（#42475）、CoPaw（#7003） | token 审计日志、估算准确性、网关级成本预算 |
| **会话/上下文保真度** | NanoBot（#2463）、OpenClaw（#44925）、CoPaw（#7065）、NanoClaw（#3254） | prompt 前缀保留、子代理结果不丢、上下文不因整合而丢失 |
| **多配置/多代理隔离** | Hermes（#87722/#87723）、NanoClaw（#3255）、OpenClaw | 密钥作用域逃逸、Session 隔离、多 bot 共室场景 |
| **安全加固** | PicoClaw（SSRF 系列）、LobsterAI（3 项安全 PR）、Moltis（2 项安全 PR）、NanoBot（#5305）、ZeroClaw（#9580） | SSRF、白名单绕过、日志脱敏、IPC 越权、出口策略 |
| **统一协议/API 兼容层** | ZeroClaw（#8603）、CoPaw（#6302）、NanoBot（#5104） | 暴露 OpenAI Chat Completions 以接入 Open WebUI、Continue.dev 等生态 |


## 5. 差异化定位分析

| 项目 | 功能侧重 | 目标用户 | 核心架构特征 |
|------|----------|----------|-------------|
| **OpenClaw** | 全功能、多渠道、生态上游 | 个人开发者到企业 | 单体 + 可插拔渠道；可靠性债务重但迭代极快 |
| **NanoBot** | Python 优先、技能（Skills）管理 | Python 技术用户 | basedpyright 严格模式，PR 审查严格导致积压 |
| **Hermes Agent** | 跨平台桌面体验、视觉/OCR 能力 | Windows 用户、桌面重度用户 | 多配置文件 + 桌面端原生体验，平台工程化 |
| **NanoClaw** | 多会话多代理协同 | 多 bot 生产环境运维者 | 对话投递流水线重构，A 系列编号显示清晰路线图 |
| **PicoClaw** | 嵌入式/资源受限场景 | 嵌入式开发者 | 轻量，资源占用敏感 |
| **IronClaw** | Rust 原生、多渠道网关 | DevOps 场景 | Rust 全栈，依赖自动更新为主 |
| **LobsterAI** | 办公场景集成、IM 协作 | 企业办公用户 | Electron 桌面端 + 企业认证（OAuth2、IPC 安全） |
| **Moltis** | 持久化连接器、CalDAV/Gmail | 知识工作者 | Rust + Tauri 类架构，安全优先（配对签名、zip 防护） |
| **CoPaw** | 数据分析/办公场景、原生桌面 | 数据分析师、办公人群 | 分析工作区 + 持久化会话，DataPaw 原生应用在途 |
| **ZeroClaw** | 安全标准化、治理流程化 | 安全敏感的企业用户 | 基于 RFC 治理，ADR（架构决策记录），出口策略三步走 |


## 6. 社区热度与成熟度

| 阶段 | 项目 | 特征 |
|------|------|------|
| **超活跃/平台型** | OpenClaw、ZeroClaw | 日增 50-500 条活动，功能与安全并行推进，但可靠性/测试稳定性是硬约束 |
| **快速迭代/功能型** | NanoClaw、CoPaw、Hermes Agent | 日增 10-50 条活动，架构演进清晰（NanoClaw 的 A 系列，CoPaw 的原生桌面），社区贡献者占比高 |
| **稳定巩固/维护型** | LobsterAI、Moltis、IronClaw | 安全修复与依赖更新为主，外部贡献者参与度高，但新功能节奏放缓 |
| **收缩/低活跃** | NanoBot、PicoClaw | 活跃但 PR 积压严重（NanoBot 499 条待合并），NanoBot 存在 PR 冲突超 5 个月无人处理的情况 |
| **休眠** | NullClaw、TinyClaw、ZeptoClaw | 24 小时零活动 |


## 7. 值得关注的趋势信号

1. **"平台化"是下一个竞争制高点**：ZeroClaw 的 Chat Completions 兼容层（#8603，22 评论）与统一附件架构（#9488）表明顶层玩家正在从"渠道网关"升级为"标准 API 服务器"。OpenClaw 若不能在协议标准化上跟进，其生态位可能被细分项目侵蚀。

2. **可靠性债务成为规模化瓶颈**：OpenClaw 的 #121058（静默丢消息"修复后复发"）和 NanoClaw 的 #3255（多 bot 投递错乱）都指向一个事实——在多会话、多代理、多通道的复杂环境下，**消息确定性交付不再是"锦上添花"而是"可用性底线"**。建议所有 AI 智能体项目的架构师将事件溯源、幂等投递、审计日志列为 P0 级基础设施。

3. **安全投资从"功能"变为"合规"**：LobsterAI、Moltis、PicoClaw、ZeroClaw 四家同一天合并/提交安全修复（日志脱敏、SSRF 防护、出口策略），且多为外部贡献者主动提交（"我想用 Moltis，但在用之前得先修几个安全问题"）。对开发者意味着：**安全修复是获得社区信任和贡献者的最佳途径之一**。

4. **Token 成本透明化将成标配**：NanoBot 的百万 token 消耗投诉（#5266）、OpenClaw 的网关级成本预算（#42475）、CoPaw 的 ViBo 记忆压缩（#7003）三个独立诉求同时出现。模型推理成本仍是用户最大的焦虑点，提供细粒度、可预期的 token 审计能力将成为差异化竞争力。

5. **治理机制开始专业化**：ZeroClaw 的维护者决策队列（#8692）和工作泳道 RFC（#6808）是生态中最前沿的治理实践——将"谁来决定、何时决定"透明化。这对大型开源 AI 项目有直接借鉴意义，能有效缓解"提案石沉大海"的社区不满。

6. **本地模型生态的"最后一公里"未打通**：Hermes 的 Ollama MCP 工具调用"被编造"（#87027）和流式输出 1.5 秒取消（#87697）、NanoBot 的 gemini-3-flash-preview 回归（#2185）暴露了本地模型在工具调用和流式输出的兼容性短板。这将随本地模型使用率提升而愈发成为痛点。

---

*报告基于 2026-08-17 各项目 GitHub 公开数据生成，供技术决策者与开发者参考。*

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报 — 2026-08-17

---

## 1. 今日速览

NanoBot 项目今日保持**高度活跃**状态。过去24小时内共产生 15 条 Issue 更新和 500 条 PR 更新，其中新增/活跃 Issue 11 条、关闭 4 条，PR 池中仍有 499 条待合并。值得关注的是，**安全漏洞（#5305）已确认关闭**，表明维护团队对安全问题响应迅速；但 PR 积压数量庞大（499 条待合并），合并效率仍是项目当前的主要瓶颈。讨论焦点集中在**token 消耗监控与整合机制**（#5266、#5402、#5377）、**上下文管理**（#2463）以及 **MCP 生态扩展**（#5251、#5298）等方向。今日无新版本发布，项目处于功能迭代与修复并行的阶段。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日 PR 合并/关闭数量极少（仅 1 条），但有一项值得关注的变化：

| PR | 状态 | 说明 |
|---|---|---|
| [#4329](https://github.com/HKUDS/nanobot/pull/4329) feat(cli): add native TypeScript terminal UI | **已关闭** | 该 PR 曾被误标为合并（head 短暂出现在 main 分支上），main 已立即恢复，变更内容未进入主分支。替代 PR [#5406](https://github.com/HKUDS/nanobot/pull/5406) 已由 Re-bin 重新提交，携带完整提交历史及跨终端测试修复。 |

**项目推进评估**：由于今日合并数量极少（仅 1 条关闭），主分支在功能层面实质推进有限。但 PR #5406 的重新提交意味着 TypeScript 终端 UI 这一重要功能仍有望在后续合入。此外，500 条 PR 更新中绝大多数（499 条）仍处于待合并状态，其中大量 PR 标注了 `[conflict]` 标记（见第 8 部分），可能需要维护者优先处理冲突解决。

---

## 4. 社区热点

今日讨论最活跃的 Issue/PR 如下：

**#2463 [Architectural issue] prompt 前缀不保留** — 15 条评论
🔗 https://github.com/HKUDS/nanobot/issues/2463

> 社区讨论了 nanobot 持久化会话历史与实际发送给模型的 prompt 前缀不一致的架构性问题。该 Issue 自 3 月提出至今，讨论热度持续，表明**会话上下文保真度**是社区长期关注的核心架构议题，直接影响与 OpenAI 等 Provider 的兼容性。

**#5266 [enhancement] token 消耗日志** — 14 条评论
🔗 https://github.com/HKUDS/nanobot/issues/5266

> 用户反馈 nanobot 在无明显用户活动的情况下，2 小时内消耗了约百万级 token。该问题获得大量共鸣，反映出**token 成本透明度**已成为用户的核心诉求之一，特别是对于长期运行、后台自动触发的场景。

**#2185 [regression] gemini-3-flash-preview 升级后不可用** — 9 条评论
🔗 https://github.com/HKUDS/nanobot/issues/2185

> 升级到 0.1.4post5 后 gemini-3-flash-preview 模型调用异常。该 Issue 从 3 月持续至今，虽然已关闭，但 9 条评论说明用户对**版本升级的兼容性**高度敏感。

**#4864 [bug] complete_goal 工具死循环** — 6 条评论（👍 1）
🔗 https://github.com/HKUDS/nanobot/issues/4864

> 工具参数序列化变更导致 gateway 将 recap 参数解析为裸字符串而非 JSON 对象，引发死循环。该问题获得了社区关注，可能影响使用 goal-completion 工作流的用户。

---

## 5. Bug 与稳定性

按严重程度排列：

### 🔴 严重 — 安全漏洞（已修复）

**#5305 [Security] `exec.allowPatterns` 白名单绕过 → 链式 shell 命令执行** — **已关闭**
🔗 https://github.com/HKUDS/nanobot/issues/5305

> 攻击者可通过 OpenAI 兼容 API 绕过 `exec.allowPatterns` 白名单，执行额外的 shell 命令段。该漏洞已确认关闭，说明修复已合入或通过其他方式解决。**建议维护者在下一个版本发布说明中明确披露此安全修复。**

### 🟠 中等 — 功能异常

**#5402 [bug] token 整合永不触发 — tiktoken 估算系统性低估** — OPEN
🔗 https://github.com/HKUDS/nanobot/issues/5402

> tiktoken（或 Provider 特定计数器）对 prompt token 的估算持续低于 API 实际返回的 token 数，导致 consolidation 机制永远无法触发。这可能造成**上下文无限增长**，进而引发成本飙升（与 #5266 呼应）。

**#5377 [bug] consolidation 截断输入但推进完整批次游标** — OPEN
🔗 https://github.com/HKUDS/nanobot/issues/5377

> `Consolidator.archive()` 将格式化会话截断至模型输入 token 预算，但其调用方仍将 `Session.last_consolidated` 推进到完整批次，导致被截断的消息永久丢失。这属于**数据完整性问题**，可能造成对话上下文意外丢失。

**#4864 [bug] complete_goal 工具死循环** — OPEN
🔗 https://github.com/HKUDS/nanobot/issues/4864

> 工具参数序列化方式变更导致 `complete_goal` 期望的 JSON 对象参数被解析为裸字符串，工具反复报错形成死循环。**该问题与近期 gateway 更新相关，建议优先排查。**

**#5373 [bug] Cron 调度器在持久化失败后永久死亡** — **已关闭**
🔗 https://github.com/HKUDS/nanobot/issues/5373

> `CronService._on_timer` 中单次持久化失败（磁盘满、权限变更、文件锁）即导致异常逃逸，且 `_arm_timer()` 位于 `try/finally` 之外，调度器不再调度下一次任务。**该问题虽已关闭，但“静默死亡”类故障值得后续添加监控告警。**

### 🟡 低 — 回归问题

**#2185 [regression] gemini-3-flash-preview 升级后不可用** — **已关闭**
🔗 https://github.com/HKUDS/nanobot/issues/2185

> 升级 0.1.4post5 后 gemini-3-flash-preview 无法通过 Ollama endpoint 调用。该问题已关闭，但用户可能需要手动更新配置才能恢复。

---

## 6. 功能请求与路线图信号

| Issue/PR | 功能描述 | 是否已有对应 PR | 纳入下一版本可能性 |
|---|---|---|---|
| [#5404](https://github.com/HKUDS/nanobot/issues/5404) [enhancement] 技能增加 `disable-model-invocation` 配置 | 允许将技能设为“仅用户可用”，限制模型自主调用，参考 PI、Cursor 等工具的做法 | 暂无 | 中 — 与主流编码助手的功能对齐趋势一致 |
| [#5251](https://github.com/HKUDS/nanobot/issues/5251) [enhancement] WebUI 支持 MCP Apps 宿主 | 通过 `io.modelcontextprotocol/ui` 扩展，将 MCP 调用结果以交互式 UI 组件呈现，而非仅文本/图片 | 暂无 | 中 — MCP 生态演进的自然延伸 |
| [#5298](https://github.com/HKUDS/nanobot/issues/5298) [enhancement] MCP schema 预算控制 | 当 MCP 工具集过大时，动态裁剪传给模型的 tool schema，控制上下文成本 | 暂无 | 中高 — 与社区对 token 成本的高度关注直接相关 |
| [#4467](https://github.com/HKUDS/nanobot/issues/4467) [enhancement] Dream 应更新已有技能而非每次新建副本 | 用户维护的工作区技能应被 Dream 增量更新，而非创建重复文件 | 暂无 | 中 — 影响技能管理体验 |
| [#5289](https://github.com/HKUDS/nanobot/issues/5289) [feat] Telegram 支持贴纸与消息反应 | 支持发送贴纸、接收/回复入站贴纸，并允许 agent 主动添加消息反应 | 暂无 | 低 — 属于渠道功能增强 |
| [#5161](https://github.com/HKUDS/nanobot/issues/5161) [refactor] 缩小文件级 Pyright 抑制范围 | 在 BasedPyright strict 模式下的代码质量持续改进 | 暂无 | 中 — 代码健康度工程 |
| [#5358](https://github.com/HKUDS/nanobot/pull/5358) [feat] WebUI 会话协作（mention 提及） | 通过稳定 `@name` 支持会话间互相提及与协作 | **已有 PR** | 高 — 功能完整，等待 review |
| [#5406](https://github.com/HKUDS/nanobot/pull/5406) [feat] TypeScript 终端 UI | 原生 TS/OpenTUI 终端客户端，Python gateway 为后端 | **已有 PR** | 高 — 替代 #4329 的完整提交 |

**路线图信号**：token 成本控制（#5266、#5402、#5298）、MCP 深度集成（#5251、#5298）、以及技能管理增强（#4467、#5404）是当前社区关注度最集中的三大方向，预计将影响后续版本的优先级排序。

---

## 7. 用户反馈摘要

从今日活跃的 Issue 评论中提炼的关键用户声音：

| 用户诉求 | 来源 | 情绪倾向 |
|---|---|---|
| **Token 消耗不透明**：“2 小时内烧掉百万 token 且用户无感知”——用户需要细粒度的 token 审计日志（调用时间、来源、消耗量） | [#5266](https://github.com/HKUDS/nanobot/issues/5266) | 不满 — 成本焦虑 |
| **Token 估算系统不可靠**：tiktoken 估算与实际 API 计数偏差过大，导致自动整合机制失效 | [#5402](https://github.com/HKUDS/nanobot/issues/5402) | 困惑 — 系统行为不可预期 |
| **上下文丢失风险**：整合过程中的截断行为导致消息永久丢失，用户对数据完整性表示担忧 | [#5377](https://github.com/HKUDS/nanobot/issues/5377) | 担忧 — 数据安全 |
| **技能迭代体验差**：Dream 每次运行都创建新的技能副本，用户手动维护的技能会被“淹没” | [#4467](https://github.com/HKUDS/nanobot/issues/4467) | 沮丧 — 工作流受阻 |
| **技能控制粒度不足**：用户希望某些技能只能被人类显式触发，防止模型“自作主张”调用 | [#5404](https://github.com/HKUDS/nanobot/issues/5404) | 期待 — 对齐行业实践 |
| **线程上下文隔离**（Matrix 渠道）：用户希望“回复线程”能像 Discord/Slack 一样形成独立上下文，而非与主房间消息混杂 | [#5275](https://github.com/HKUDS/nanobot/issues/5275) | 期待 — 跨渠道体验一致性 |

---

## 8. 待处理积压

以下为长期未响应或存在合并冲突的 PR/Issue，建议维护者优先关注：

### ⚠️ 长期存在的 PR（距今已 >5 个月，全部标注 `[conflict]`）

| PR | 内容 | 距今天数 | 说明 |
|---|---|---|---|
| [#1306](https://github.com/HKUDS/nanobot/pull/1306) | Discord 语音/音频 + TTS 回复 | ~170 天 | 功能性增强，但长期冲突未解决 |
| [#1205](https://github.com/HKUDS/nanobot/pull/1205) | KV cache 复用与 batch prompt rollover | ~173 天 | 性能优化，含实验数据对比 |
| [#1195](https://github.com/HKUDS/nanobot/pull/1195) | Telegram forum threads 支持 | ~173 天 | 渠道功能增强 |
| [#1149](https://github.com/HKUDS/nanobot/pull/1149) | PromptGuard 提示注入检测 | ~173 天 | **安全相关**，建议优先解决冲突 |
| [#1147](https://github.com/HKUDS/nanobot/pull/1147) | Telegram 群聊消息前缀显示发送者名 | ~174 天 | 简单功能，冲突应易于解决 |
| [#1128](https://github.com/HKUDS/nanobot/pull/1128) | 163.com IMAP 连接修复 | ~174 天 | 特定 Provider 兼容性修复 |
| [#1073](https://github.com/HKUDS/nanobot/pull/1073) | 保存配置时保留未知键 | ~175 天 | 数据丢失问题修复（#1023 Bug 2） |
| [#1072](https://github.com/HKUDS/nanobot/pull/1072) | 捕获工具执行中的 CancelledError | ~175 天 | 进程崩溃修复 |
| [#1066](https://github.com/HKUDS/nanobot/pull/1066) | Release 自动发布 + Docker 镜像 CI | ~175 天 | 基础设施改进 |
| [#1053](https://github.com/HKUDS/nanobot/pull/1053) | 消息工具传播渠道路由元数据 | ~175 天 | 线程回复路由修复 |
| [#1037](https://github.com/HKUDS/nanobot/pull/1037) | 系统提示中时间信息移至末尾（优化 KV cache 命中） | ~175 天 | 性能优化 |
| [#1034](https://github.com/HKUDS/nanobot/pull/1034) | Z.ai Coding Plan 配置文档 | ~175 天 | 文档改进 |
| [#1032](https://github.com/HKUDS/nanobot/pull/1032) | Subagent 控制平面 MVP（list/kill） | ~175 天 | 功能增强，对应 #1006 |
| [#1026](https://github.com/HKUDS/nanobot/pull/1026) | 处理完媒体文件后删除，防止磁盘无限增长 | ~175 天 | 运维稳定性 |
| [#1025](https://github.com/HKUDS/nanobot/pull/1025) | OAuth token 持久化 + 保留未知配置字段 | ~175 天 | 对应 #1023 两个 Bug 修复 |
| [#1024](https://github.com/HKUDS/nanobot/pull/1024) | Subagent 配置文件化（含 227 行测试） | ~176 天 | 功能增强 |
| [#1015](https://github.com/HKUDS/nanobot/pull/1015) | Subagent spawn 支持指定模型 | ~176 天 | 功能增强，成本路由 |

### ⚠️ 长期未关闭的 Issue

| Issue | 内容 | 创建时间 | 评论数 |
|---|---|---|---|
| [#2463](https://github.com/HKUDS/nanobot/issues/2463) | Prompt 前缀不保留的架构问题 | 2026-03-25 | 15 |
| [#4864](https://github.com/HKUDS/nanobot/issues/4864) | complete_goal 工具死循环 | 2026-07-09 | 6 |

### 📌 维护者行动建议

1. **优先处理 `[conflict]` 标记的 18 个 PR**：这些 PR 大多数提交于 2-3 月，距今已超过 5 个月，代码冲突累积严重，建议安排一次集中的 conflict resolution 工作坊。
2. **尽快 review PR #5406（TypeScript 终端 UI）**：作为 #4329 的替代品，该 PR 承载了社区对终端体验改进的期望，且已在开放 1 天内获得关注。
3. **考虑为 #5266、#5402、#5377 建立 token 消耗与整合机制的工作组**：这三个 Issue 相互关联，核心问题都是 token 管理的可观测性和准确性，建议从架构层面统一解决。

---

*本日报基于 2026-08-17 的 GitHub 数据自动生成。项目总体健康度：⚠️ 活跃但 PR 积压严重，安全问题响应及时，token 管理与上下文保真度是当前最大技术债。*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目日报 — 2026-08-17

## 1. 今日速览

项目今日保持高活跃度：24小时内更新了50条Issue和50条PR，社区快速迭代节奏明显。新发布的 v0.20.2 补丁版本将约397个自上一版本以来的PR合入稳定发行渠道，保证了Docker镜像、托管部署和全新安装的同步演进。值得关注的是，过去24小时的新Issue呈现出明显的"平台工程化"特征——Windows平台的更新/安装流程、多配置文件网关的安全性隔离、以及桌面应用稳定性问题集中爆发，反映出项目在用户规模扩大后正面临真实世界的多样性挑战。48个PR待合并也表明维护者审查队列存在一定积压。

---

## 2. 版本发布

### Hermes Agent v0.20.2 (v2026.8.16)

**发布日期：** 2026年8月16日

这是一个补丁版本，将自 v0.20.1 以来合并的约397个PR聚合为一个稳定的标签发布，面向下游消费者（Docker镜像、托管部署、全新安装）。

**包含内容：**
- 自 v0.20.1 以来的约397个已合并PR的聚合
- 涵盖Bug修复、功能增强、性能优化等多方面变更

**破坏性变更：** 补丁版本预期不包含破坏性变更，但建议查阅具体PR详情确认与自身配置相关的变更。

**迁移注意事项：** 无特殊迁移步骤，常规更新即可。

---

## 3. 项目进展

过去24小时内合并/关闭的PR共2个，虽然数量不多，但项目整体V0.20.2的发布已将该周期所有重要变更推送到稳定渠道。以下是值得关注的待合并PR，它们代表了项目下一阶段的方向：

### 关键推进方向

| 方向 | PR | 说明 |
|------|-----|------|
| **视觉能力强化** | [#88031](https://github.com/NousResearch/hermes-agent/pull/88031) | 修复openai-api视觉路径：原生视觉模型不再被静默降级到辅助文本模型，视觉拒绝时fail-closed |
| **OCR工具链** | [#87712](https://github.com/NousResearch/hermes-agent/pull/87712) | 新增`vision_ocr`工具，为辅助视觉路径提供OCR grounding，支持PaddleOCR-VL等轻量CPU模型 |
| **Devin ACP集成** | [#88027](https://github.com/NousResearch/hermes-agent/pull/88027) | 将Devin (Cognition)作为一级Hermes provider暴露，支持`devin-acp`、`devin`、`cognition`、`swe`等别名 |
| **生成式UI** | [#88024](https://github.com/NousResearch/hermes-agent/pull/88024) | 插件注册`::directives`后，agent可在聊天中渲染实时内联UI组件 |
| **日志可靠性** | [#88026](https://github.com/NousResearch/hermes-agent/pull/88026) | `hermes logs -f`在日志轮转后自动重新打开新文件，不再静默断开 |
| **会话搜索增强** | [#88030](https://github.com/NousResearch/hermes-agent/pull/88030) | 当精确FTS5匹配无结果时，OR-relaxed重试可恢复释义型多词查询的召回 |
| **Cron任务上限** | [#45809](https://github.com/NousResearch/hermes-agent/pull/45809) | 为cron作业添加per-job的`max_turns`和wall-clock超时上限 |
| **网关消息策略** | [#88028](https://github.com/NousResearch/hermes-agent/pull/88028) | 新增`unauthorized_dm_behavior: decline`选项，对未授权DM发送一次礼貌拒绝而非配对码 |

---

## 4. 社区热点

### 最热门 Issue

**[#66616 - Skills index is stale or degraded](https://github.com/NousResearch/hermes-agent/issues/66616)**（45条评论）
- 自动化新鲜度探针报告索引已29.8小时未更新（限制为26h）
- 这是一个由`nousbot-eng`提交的自动化监控告警，已存在约30天
- 45条评论的高互动量表明该问题持续发酵，社区对Skills Hub的可用性关注度高

### 热门Issue背后的诉求分析

| Issue | 核心诉求 |
|-------|----------|
| [#53480 - Updater should guard against interrupting active Desktop agent sessions](https://github.com/NousResearch/hermes-agent/issues/53480) | 用户希望更新流程不打断正在运行的agent会话，需要检测活跃工作并阻塞/延迟/强制确认 |
| [#87027 - Local/custom provider (Ollama)： agent never emits real tool_calls for MCP tools](https://github.com/NousResearch/hermes-agent/issues/87027) | 本地Ollama模型对MCP工具的调用路径存在严重缺陷——模型"编造"工具结果而非真正调用，或返回空内容 |
| [#87818 - computer_use capture： `question` param is dropped on auxiliary.vision path](https://github.com/NousResearch/hermes-agent/issues/87818) | 辅助视觉路径丢掉了用户传入的自定义`question`参数，硬编码为通用提示词 |

### 最受关注的新PR

**[#88027 - Expose and wire Devin ACP as a first-class Hermes provider](https://github.com/NousResearch/hermes-agent/pull/88027)**（P4，需决策）
- 将Devin ACP作为一级provider接入，这反映了社区对SWE-bench类自动化工具的强烈需求
- 标注`needs-decision`，可能需要维护者对集成方向做出明确选择

---

## 5. Bug 与稳定性

### P1 级别

**[#87694 - autostash produces orphan commit with full working tree snapshot — breaks all subsequent updates](https://github.com/NousResearch/hermes-agent/issues/87694)**
- **影响：** `hermes update`的autostash机制可能产生**孤儿提交**——HEAD与origin/main分叉后，所有后续更新将失败
- **严重性：** 极高，直接影响用户更新能力
- **状态：** 待修复，已有1条评论

### P2 级别（未关联fix PR）

| Issue | 问题 | 影响面 |
|-------|------|--------|
| [#87703](https://github.com/NousResearch/hermes-agent/issues/87703) | Windows: `hermes update`在cua-driver刷新时因UAC提示不可见而挂起约11分钟 | Windows平台更新流程 |
| [#87856](https://github.com/NousResearch/hermes-agent/issues/87856) | `API_SERVER_ENABLED=false`无效，服务器仍然启动（因API_SERVER_KEY总是存在） | 配置可信度 |
| [#87857](https://github.com/NousResearch/hermes-agent/issues/87857) | Desktop renderer崩溃循环："Duplicate key toolCallId" → 空白窗口 | Desktop稳定 |
| [#87724](https://github.com/NousResearch/hermes-agent/issues/87724) | computer_use变更在headless dispatch中无审批回调时fail-open | **安全边界** |
| [#87722](https://github.com/NousResearch/hermes-agent/issues/87722) | 多配置文件cron投递可逃逸密钥作用域，使用默认配置文件的凭据 | **安全边界** |
| [#87723](https://github.com/NousResearch/hermes-agent/issues/87723) | 多配置文件网关共享默认配置文件的SessionStore/SessionDB | 数据隔离 |
| [#87726](https://github.com/NousResearch/hermes-agent/issues/87726) | MCP审批响应无法解析权威网关审批 | **安全/一致性** |
| [#87697](https://github.com/NousResearch/hermes-agent/issues/87697) | Hermes Client在~1.5s后取消本地LLM流（触发`<unused49>` token循环） | 本地Ollama用户 |

### 已有修复PR关联的Bug

| Issue | 对应PR | 状态 |
|-------|--------|------|
| vision_analyze静默降级 | [#88031](https://github.com/NousResearch/hermes-agent/pull/88031) | 待合并 |
| TUI技能密钥提示路由到错误的会话 | [#68271](https://github.com/NousResearch/hermes-agent/pull/68271) | 待合并 |
| 桌面自然语言操作丢失工具名 | [#88029](https://github.com/NousResearch/hermes-agent/pull/88029) | 待合并 |
| 集成终端路由不遵循活跃配置文件 | [#85241](https://github.com/NousResearch/hermes-agent/pull/85241) | 待合并 |

---

## 6. 功能请求与路线图信号

### 热门功能请求

| 功能 | 来源 | 状态 |
|------|------|------|
| **会话标题重新生成机制** | [#47803](https://github.com/NousResearch/hermes-agent/issues/47803) (P3，2评论，1👍) | 开放中，已有1个多月历史 |
| **Cron作业per-job上限** | [PR #45809](https://github.com/NousResearch/hermes-agent/pull/45809) | 待合并，直接满足用户对cron可控性的需求 |
| **Devin ACP集成** | [PR #88027](https://github.com/NousResearch/hermes-agent/pull/88027) | 待决策，社区对SWE类工具的接入有明确期待 |
| **插件实时内联UI** | [PR #88024](https://github.com/NousResearch/hermes-agent/pull/88024) | 待合并，为agent构建插件化交互提供新范式 |
| **vision_ocr工具** | [PR #87712](https://github.com/NousResearch/hermes-agent/pull/87712) | 待合并，满足CPU快速OCR识别需求 |
| **Grok Imagine Image 2.0** | [PR #87711](https://github.com/NousResearch/hermes-agent/pull/87711) | 待合并，扩展xAI图像目录 |
| **config append命令** | [PR #87734](https://github.com/NousResearch/hermes-agent/pull/87734) | 待合并，安全附加列表配置值 |

### 路线图判断

- **配置文件管理**正在向更安全、更灵活的方向演进（config append、多配置文件隔离修复），预计下一版本将重点关注多租户/多配置文件场景的稳定性和安全性
- **视觉能力**是当前开发重点：原生视觉路由修复、OCR工具、Grok Imagine 2.0 —— 多个PR同时发力
- **插件生态**出现新的想象力（生成式UI、ACP集成），但P3/P4的优先级偏低，可能还需要社区更多正反馈

---

## 7. 用户反馈摘要

### 真实用户痛点

1. **Windows更新体验糟糕**（→ 多条Issue）：
   - [#87703](https://github.com/NousResearch/hermes-agent/issues/87703)：更新挂起11分钟且无反馈
   - [#87772](https://github.com/NousResearch/hermes-agent/issues/87772)：桌面更新停滞10-17分钟，无法恢复
   - [#87828](https://github.com/NousResearch/hermes-agent/issues/87828)：健康检查在Defender行为监控下被SIGTERM
   - [#87789](https://github.com/NousResearch/hermes-agent/issues/87789)：Smart App Control阻止（os error 4551）在日志中不透明，用户缺乏可见性

2. **Ollama等本地模型体验不稳定**：
   - [#87027](https://github.com/NousResearch/hermes-agent/issues/87027)：MCP工具调用被"编造"而非真实执行
   - [#87697](https://github.com/NousResearch/hermes-agent/issues/87697)：流式输出在~1.5秒被取消

3. **桌面端副作用Bug**：
   - [#86601](https://github.com/NousResearch/hermes-agent/issues/86601) / [#87823](https://github.com/NousResearch/hermes-agent/issues/87823)：自动TTS重复朗读同一回复
   - [#87716](https://github.com/NousResearch/hermes-agent/issues/87716)：删除会话后行残留2-4秒
   - [#87759](https://github.com/NousResearch/hermes-agent/issues/87759)：两个独立会话交替消失

### 用户满意度信号

- 积极的方面：社区有用户自发为项目生态做贡献，例如 [#88021](https://github.com/NousResearch/hermes-agent/pull/88021) 添加ClawMetry（一个零配置的本地仪表盘）到Community列表
- 多个PR从其他开源项目（openclaw、ironclaw、nanoclaw等）移植修复，说明社区生态之间存在横向学习与协作

---

## 8. 待处理积压

### 重要但未响应的Issue

| Issue | 创建时间 | 积压天数 | 标签 | 为什么值得关注 |
|-------|---------|---------|------|---------------|
| [#47803](https://github.com/NousResearch/hermes-agent/issues/47803) | 06-17 | ~61天 | P3 | 会话标题重生成是Desktop用户明确提出的体验提升需求 |
| [#53480](https://github.com/NousResearch/hermes-agent/issues/53480) | 06-27 | ~51天 | P2 | 更新打断活跃agent会话，涉及数据安全 |
| [#70233](https://github.com/NousResearch/hermes-agent/issues/70233) | 07-23 | ~25天 | P2 | Groq reasoning_details泄漏导致后续请求失败 |
| [#66616](https://github.com/NousResearch/hermes-agent/issues/66616) | 07-18 | ~30天 | P3，自动化探针 | Skills Index持续degraded，45条评论但尚未修复 |

### 待合并的关键PR提醒

| PR | 积压天数 | 为什么需要关注 |
|-----|---------|---------------|
| [#27724](https://github.com/NousResearch/hermes-agent/pull/27724) | ~91天 | BusyBox grep兼容性修复，影响Alpine/容器环境 |
| [#45809](https://github.com/NousResearch/hermes-agent/pull/45809) | ~65天 | Cron作业超时上限，用户对cron失控的痛点持续存在 |
| [#68271](https://github.com/NousResearch/hermes-agent/pull/68271) | ~28天 | TUI技能密钥提示路由错误，跨会话安全问题 |

---

*本报告基于2026-08-17的GitHub数据自动生成。数据来源：NousResearch/hermes-agent公共仓库。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

好的，作为AI智能体与个人AI助手领域开源项目分析师，根据您提供的 PicoClaw GitHub 数据，我为您生成了 **2026年8月17日** 的项目动态日报。

---

### PicoClaw 项目动态日报 (2026-08-17)

#### 1. 今日速览

PicoClaw 项目今日活跃度中等，核心聚焦于**安全加固（SSRF防护）与功能扩展**两方面。虽然无新版本发布，但过去24小时内共有3个新Issue和5个PR更新，显示社区参与度稳定。当前最值得关注的是由 `SashaMIT` 提交的针对多个平台（Weixin/WeCom/OneBot等）的SSRF漏洞修复系列PR，这批PR悬置已一周，**建议维护者优先评审合并**，以消除潜在的安全风险。同时，社区对新的集成需求（如OAuth 2.1、Telegram表格渲染、Exa搜索提供商）表现出兴趣。

#### 2. 版本发布

今日无新版本发布。

#### 3. 项目进展

今日最关键的进展是 `#3193` 被**关闭**（该PR曾为simplex频道添加支持）。虽然这并非合并，但关闭状态可视为项目维护者对特定功能导向的阶段性决策结果。

此外，待合并列表中的 **PR #3322、#3323、#3324**（均由 SashaMIT 提交）构成了一个完整的SSRF安全加固系列，涉及OneBot、QQ、Telegram、Discord、LINE、Slack、WeCom、Weixin等几乎所有渠道的媒体下载路径。该系列修复尚未被合并，但一旦通过，将显著提升项目的网络安全韧性，是项目稳定性的一次重大跨越。

#### 4. 社区热点

今日讨论热度最高的是Issue **#3302 [Feature] Support OAuth 2.1**，共获得3条评论。该Issue请求为MCP服务器支持OAuth 2.1，并明确引用了旧Issue #2546，说明这是多用户持续关注的核心痛点。用户诉求在于改进连接远程MCP服务器时的身份验证流程，以提高安全性和易用性。此需求被标记为 “Nice-to-Have”，但结合近期行业标准演进，若开发资源允许，建议纳入下一版本路线图进行可行性评估。

#### 5. Bug 与稳定性

今日报告了一个新Bug，严重程度分级如下：

- **高 (P1)**: **[BUG] Slack does not attach image media content (#3338)**。报告明确指出 Slack 媒体上传必然失败，错误为 `file size cannot be 0`。根因是 `SendMedia` 调用 slack-go SDK 时未设置 `FileSize` 参数。**该Bug目前暂无对应修复PR**，影响所有通过 Slack 渠道发送含媒体内容的用户，建议尽快指派开发者修复。

- **中 (P2)**: **[安全修复PR系列] ( #3322, #3323, #3324 )** 中描述的 SSRF 漏洞。虽未报告为致命Bug，但描述表明当前在多个频道（如QQ、Telegram、Discord等）下载媒体时存在被定向到内网地址的潜在风险。尽管已有修复方案，但没有合并上线前，此问题仍潜伏在现有版本中，属于安全隐患。

#### 6. 功能请求与路线图信号

来自社区的功能请求主要涉及连接性与交互体验：

- **外部服务集成**:
  - **[Feature] Support OAuth 2.1 for MCP servers (#3302)**：建议采用标准的 OAuth 2.1 认证流程。
  - **[PR] Add native Exa web search provider (#3299)**：该 PR 仍在待合并状态，旨在将 Exa 搜索引入 `tools.web` 提供商列表，丰富用户的联网搜索选项。
- **客户端交互优化**:
  - **[Feature] Render Telegram tables with rich messages (#3325)**：利用 Telegram Bot API 10.1的新特性展示原生表格，改善结构化数据的可读性。

综合来看，社区在积极推动“更多上游服务集成”和“更丰富消息格式支持”，这些可能被纳入版本规划的重点考量方向。

#### 7. 用户反馈摘要

- **开发痛点（SSRF安全）**：来自开发者 `SashaMIT` 的反馈指出，现有代码在多渠道媒体下载逻辑中对重定向未做安全校验，平台实测存在可被利用的安全风险，体现了资深用户对安全架构的高要求。
- **功能缺失**：Slack Bug (#3338) 的提交者 `octavioturra` 直接反馈了“发送图片必失败”的糟糕体验，这是一类直接影响日常使用的严重功能缺失。
- **交互体验**：Issue #3325 的提交者 `As-tsaqib` 对Telegram渠道中表格展示为纯文本/代码块的表现不满意，反映了用户在追求更原生、更美观的消息渲染效果。

#### 8. 待处理积压

- **高风险积压PR**：**[安全修复] PR #3322, #3323, #3324**。这些修复方案已存在一周（直至2026-08-16仍为打开状态），关联所有频道，安全等级高，**强烈建议维护者立即抽出时间进行Code Review并合并，解除SSRF安全警报**。

- **功能请求搁置**：**[Feature] PR #3299 (Exa web search provider)**。该PR已悬置近一月（since 2026-07-26），若功能无冲突且代码质量合格，存在被遗忘的风险，建议维护者明确该功能的去留，及时合入或给出调整意见。

- **长期功能诉求**：**[Feature] Issue #3302 (OAuth 2.1)**。该需求有3条评论，且并非孤立提出（关联#2546），但因为标为增强类功能，优先级可能较低。为了避免社区抱怨“提了不处理”，建议维护者在该Issue下给出相关回复或并线到明确的路线图中。

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报

**日期：2026-08-17**  
**数据窗口：2026-08-16 ~ 2026-08-17**


## 1. 今日速览

NanoClaw 在过去 24 小时内展现出**高产出的收敛态势**：共 32 条 PR 更新，其中 13 条已合并/关闭（含 6 条 core-team 的架构级 PR），19 条仍在审核或待合并。Issue 侧仅 1 条，且为误报关闭，社区问题反馈面较窄，说明近期合并的稳定性修复正在生效。值得关注的是，昨日闭合并入了一批**跨会话上下文管理、消息传递流水线（delivery pipeline）重构、权限策略增强**的核心改动，项目正在朝"多会话、多代理（agent）协同"方向稳步推进。社区侧呈现"贡献者驱动的功能迭代 + 零用户投诉"的健康状态。


## 2. 版本发布

**无新版本发布。**

> 注意：近期 PR 中多次提到 **migration 022**（`messaging_groups.detached_at` 列），若为数据库架构变更，建议维护者尽快切一个 0.x 预发布版本，避免社区 fork 自行合入导致 migration 冲突。


## 3. 项目进展

今日合并/关闭的 13 条 PR 中，核心进展集中在 **core-team 的 6 条架构级合入**，标志着项目正从"单会话单代理"向"多会话、多实例、多代理"架构演进：

- **跨会话上下文模块**（[#3257](https://github.com/nanocoai/nanoclaw/pull/3257)）：消息在兄弟会话间 fan-out（扇出）为 `session-echo` 上下文行，DM 会话自动回溯填充，为多会话协同打下基础。
- **会话分离状态**（[#3256](https://github.com/nanocoai/nanoclaw/pull/3256)）：`messaging_groups.detached_at` 列 + migration 022，拒绝向已脱离的会话投递消息——**避免在 bot 被移出群聊后继续向孤儿会话发送消息的 bug**。
- **投递通道修复**（[#3255](https://github.com/nanocoai/nanoclaw/pull/3255)）：出站投递精确解析发送者自身的 channel 行，修复**多 bot 身份共享一个群聊时投递错乱**的问题。
- **两阶段批量选择器**（[#3254](https://github.com/nanocoai/nanoclaw/pull/3254)）：修复上下文行（trigger=0）积压导致任务行被挤出批次的**唤醒丢失（wake-fired-but-no-work）**问题。
- **单通道投递门**（[#3284](https://github.com/nanocoai/nanoclaw/pull/3284)）：确立"直播流是唯一内容出口"的不变式，**移除持久化去重状态**，简化投递路径。
- **Chat SDK 桥接层增强**（[#3262](https://github.com/nanocoai/nanoclaw/pull/3262)）：DM 线程归一化 + app-context 捕获，为支持复杂 DM surface 的平台做好准备。

此外，**社区贡献的 5 条 PR** 也被合入：
- **权限策略**（[#3260](https://github.com/nanocoai/nanoclaw/pull/3260)）：新增 `decline_notify` 策略——礼貌拒绝未知发件人 + 一行式通知所有者，**免去审批卡片打断**。
- **适配器能力接口**（[#3261](https://github.com/nanocoai/nanoclaw/pull/3261)）：`setTyping` 支持状态行与状态来源（工具自动 vs 代理撰写）、`setThreadTitle`、`setSuggestedPrompts`。
- **通道注册表热启动**（[#3263](https://github.com/nanocoai/nanoclaw/pull/3263)）、**投递批预览钩子**（[#3264](https://github.com/nanocoai/nanoclaw/pull/3264)）、**创建代理静默通知**（[#3265](https://github.com/nanocoai/nanoclaw/pull/3265)）、**注册卡片拦截器**（[#3266](https://github.com/nanocoai/nanoclaw/pull/3266)）——四个 A 系列钩子/接口为上层模块开发提供了更细粒度的介入点。

**整体判断**：项目在"多会话 + 多代理"方向上有明确路线图（PR 标题中 A1-A4、C4、Story 1.1 等编号指向内部任务拆解），今日合入约对应 6-8 个工作日的开发量，推进节奏较快。


## 4. 社区热点

今日无高评论/高互动 Issue 或 PR（数据窗口中评论数为 undefined，但 👍 数均为 0，未见集中讨论）。

分析原因：core-team 的 PR 集中在 8 月 15-16 日提交，且多数已合入，社区成员可能仍在消化代码或等待新版本发布后再体验反馈。**唯一值得关注的是 [#1251](https://github.com/nanocoai/nanoclaw/pull/1251)（OpenMail 邮件频道技能）**，从 3 月 18 日创建至今约 5 个月后重新活跃（8 月 16 日更新），但状态为 CLOSED，推测已合入或弃用——建议确认是否已随某个版本发布。


## 5. Bug 与稳定性

| 严重程度 | Issue/PR | 描述 | 状态 |
|---------|----------|------|------|
| 中 | [#3284](https://github.com/nanocoai/nanoclaw/pull/3284) | 中间环节流式输出与最终结果双通道投递导致内容重复 | ✅ 已合入修复 |
| 中 | [#3254](https://github.com/nanocoai/nanoclaw/pull/3254) | 上下文行积压挤掉任务行，导致"唤醒后无工作可做" | ✅ 已合入修复 |
| 中 | [#3255](https://github.com/nanocoai/nanoclaw/pull/3255) | 多 bot 身份共享群聊时出站投递解析到错误的实例 | ✅ 已合入修复 |
| 中 | [#3281](https://github.com/nanocoai/nanoclaw/pull/3281) | `ncl tasks` 对 pre-2.1.54 遗留会话不可见（#3233） | 🟡 待合并（有 fix PR） |
| 中 | [#2752](https://github.com/nanocoai/nanoclaw/pull/2752) | Discord 入站附件（文本/图片）无法以可读形式传给代理 | 🟡 待合并（有 fix PR） |
| 低 | [#3280](https://github.com/nanocoai/nanoclaw/pull/3280) | `ncl groups config update` 无法通过空字符串将配置置为 NULL | 🟡 待合并（有 fix PR） |
| 低 | [#3282](https://github.com/nanocoai/nanoclaw/pull/3282) | Telegram 配对码粘贴时因空格被拒 | 🟡 待合并（有 fix PR） |
| 低 | [#3283](https://github.com/nanocoai/nanoclaw/pull/3283) | Chat SDK 显示文本被缩短/改写时链接丢失 | ✅ 已合入修复 |

**整体判断**：今日合入的修复集中在**消息投递可靠性和多实例正确性**两个领域，是代理系统稳定运行的关键路径。无崩溃、数据丢失级别的 P0/P1 问题。


## 6. 功能请求与路线图信号

从 PR 标题中的编号体系可以推断出明确的内部路线图，今日合入/活跃的 PR 对应以下方向：

| 编号 | 功能 | 对应 PR | 状态 |
|------|------|---------|------|
| A1 | 通道注册表热启动——新注册适配器可立即激活 | [#3263](https://github.com/nanocoai/nanoclaw/pull/3263) | ✅ 已合入 |
| A2 | 投递批预览钩子——模块可在逐条投递前查看整个批次 | [#3264](https://github.com/nanocoai/nanoclaw/pull/3264) | ✅ 已合入 |
| A3 | 创建代理时可选静默成功通知（保留错误通知） | [#3265](https://github.com/nanocoai/nanoclaw/pull/3265) | ✅ 已合入 |
| A4 | 渠道注册卡片拦截器——模块可消费注册审批流 | [#3266](https://github.com/nanocoai/nanoclaw/pull/3266) | ✅ 已合入 |
| A8+C4 | Chat SDK 桥接 DM surface 增强（上下文捕获 + 线程归一化） | [#3262](https://github.com/nanocoai/nanoclaw/pull/3262) | ✅ 已合入 |
| Story 1.1 | 文档记忆——MCP 工具将 Word/PDF 保存至代理长期记忆 | [#3278](https://github.com/nanocoai/nanoclaw/pull/3278) | ✅ 已合入 |

**尚未合入但值得关注的功能信号**：
- **OpenMail 邮件技能**（[#1251](https://github.com/nanocoai/nanoclaw/pull/1251)）：为代理提供邮件收发能力（频道模式 / 工具模式 + 通知），若合入将显著扩展代理的外部触达面。
- **Discord 附件修复**（[#2752](https://github.com/nanocoai/nanoclaw/pull/2752)）：合并后可让代理真正"阅读" Discord 中粘贴的文本和图片。

**预测**：A 系列（Adapter/Agent 基础设施）+ Story 系列（文档记忆）表明下一版本可能聚焦"代理更深度地参与多渠道、多会话协作"。


## 7. 用户反馈摘要

今日数据窗口中无 Issue 评论内容可提取。但从 PR 本身可看出使用场景与诉求：

- **Discord 重度用户**（[#2752](https://github.com/nanocoai/nanoclaw/pull/2752)）：在 Discord 中粘贴文本被自动转为 `message.txt`，代理只能看到 `[file: message.txt]` 的占位符而无法读取内容，说明**用户期望代理在 Discord 中能直接阅读粘贴的代码/文本**。
- **Telegram 配对体验**（[#3282](https://github.com/nanocoai/nanoclaw/pull/3282)）：Telegram 设置卡片展示的配对码带空格，直接复制后无法识别——**小细节但影响首次部署体验**。
- **多 bot 共室场景**（[#3255](https://github.com/nanocoai/nanoclaw/pull/3255)）：同一群聊中多个 bot 身份时投递错乱，说明有用户在**生产环境中实际运行多 bot 实例**。
- **配置管理体验**（[#3280](https://github.com/nanocoai/nanoclaw/pull/3280)）：用户尝试通过 `--model ""` 清空配置时，空字符串被当真实配置传给运行时——**配置语义不符合直觉**。

**核心诉求**：用户需要代理在真实聊天场景中"看得见、读得懂"内容（不仅仅是消息文本，还有附件与上下文），同时希望配置与部署操作符合直觉。


## 8. 待处理积压

以下为长期未合入、但今日有更新的 PR，建议维护者评估优先级：

| PR | 创建时间 | 已等待 | 内容 | 建议 |
|----|---------|--------|------|------|
| [#1251](https://github.com/nanocoai/nanoclaw/pull/1251) | 2026-03-18 | ~5 个月 | OpenMail 邮件频道技能 | 今日有更新但状态为 CLOSED（可能是误关或已处理），**建议确认是否合入**；若已合入，需在 Release Notes 中说明 |
| [#2752](https://github.com/nanocoai/nanoclaw/pull/2752) | 2026-06-12 | ~2 个月 | Discord 入站附件可达性问题 | 长期未合入，但今日有更新；若有 Discord 用户诉求，**建议优先合入** |
| [#3281](https://github.com/nanocoai/nanoclaw/pull/3281) | 2026-08-16 | < 1 天 | 遗留会话对 `ncl tasks` 不可见 | 指向 bug #3233，**待合并状态，建议维护者尽早 review** |
| [#3282](https://github.com/nanocoai/nanoclaw/pull/3282) | 2026-08-16 | < 1 天 | Telegram 配对码含空格问题 | 小修复，**可快速合入** |
| [#3280](https://github.com/nanocoai/nanoclaw/pull/3280) | 2026-08-16 | < 1 天 | 配置空值语义问题 | 小修复，**可快速合入** |

> 注意：5 个月未动的 PR 突然更新，建议维护者确认社区贡献者的 PR 是否已通过其他途径处理（如被新架构取代），避免 PR 长期悬挂导致贡献者流失。


## 健康度总结

| 维度 | 评分 | 说明 |
|------|------|------|
| 项目活跃度 | ⭐⭐⭐⭐⭐ | 24 小时 32 条 PR 更新，core-team 高频产出 |
| 问题响应速度 | ⭐⭐⭐⭐ | 新报告的 bug 多数当天即有 fix PR |
| 社区贡献参与 | ⭐⭐⭐⭐ | 非 core-team 贡献的 PR 占比 ~50%（8/16） |
| 架构演进清晰度 | ⭐⭐⭐⭐⭐ | A 系列/Story 编号体系明确，路线图可预期 |
| 稳定性风险 | ⭐⭐⭐ | 投递链路存在多个边缘情况 bug，但均在快速修复中 |

**总体判断**：NanoClaw 正处于**架构演进的关键阶段**，core-team 在主线上快速推进，社区贡献者在小修复和体验改进上持续输入。建议维护者关注两点：(1) 尽快发版以固化 migration 022 和投递重构成果；(2) 清理长期悬挂的 PR（如 #1251、#2752），避免社区贡献者等待过久。

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-17

## 1. 今日速览

今日项目活跃度中等偏低。过去24小时内仅有1条新Issue和9条PR活动，其中大部分（7条）为Dependabot自动化依赖更新，人工驱动的变更较少。值得关注的是，Issue #7681（Slack未关联用户连接消息的隐私问题）今日被提出后，作者sergeiest在数小时内即提交了对应的修复PR #7682，响应速度非常快。另有1个核心开发者提交的清理类小PR #7683（移除IronLoop退役网络配置）已被关闭。项目整体处于常规迭代节奏，无重大功能发布或破坏性变更。

- 新增Issue: 1 | 活跃PR: 7 | 合并/关闭PR: 2
- 新版本发布: 无

---


## 2. 版本发布

今日无新版本发布。

---


## 3. 项目进展

### 今日合并/关闭的PR

| PR | 标题 | 变更类型 | 说明 |
|----|------|----------|------|
| [#7683](https://github.com/nearai/ironclaw/pull/7683) | chore: remove retired IronLoop network settings | XS / 清理 | 由核心开发者hanakannzashi提交，移除了已退役的`network_access`配置字段，保留了现有的自动审查/解决行为。属于配置精简，无功能影响。 |
| [#7632](https://github.com/nearai/ironclaw/pull/7632) | chore(deps): bump everything-else group (4 updates) | M / 依赖 | Dependabot合并的依赖批量更新，涉及base64、toml、rstest和jsonschema。 |

### 综合评估

今日合并的2个PR均为低风险变更（1个配置清理、1个依赖更新），没有新功能落地。项目整体的功能性进展主要体现在**进行中的PR**上，特别是：

- [PR #7682](https://github.com/nearai/ironclaw/pull/7682)（修复Slack未关联用户连接引导的隐私问题）已提交待审，若合并将改善跨渠道用户体验。
- [PR #7651](https://github.com/nearai/ironclaw/pull/7651)（自动化无结果抑制）处于XL规模的开发中，涉及自动化的确定性行为改进。

整体而言，项目今日处于"小步快跑"状态，核心逻辑无大变动，依赖保持更新。

---


## 4. 社区热点

今日社区讨论热度低，仅有1条新Issue且暂无评论。最值得关注的动态是：

**[Issue #7681](https://github.com/nearai/ironclaw/issues/7681) — Slack未关联用户连接消息公开可见且需手动往返**

- 作者: sergeiest | 创建于 2026-08-16 | 评论: 0
- 核心痛点：在共享频道中，未关联IronClaw账户的Slack用户@机器人时，收到的引导回复对全频道可见，造成隐私泄露；同时引导流程是一个手动多步骤的往返过程，易使用户放弃连接。
- 值得注意的点：该Issue在提出后数小时内就有对应的修复PR [#7682](https://github.com/nearai/ironclaw/pull/7682) 提交，说明作者同时也是解决方案的提供者（dogfooding），社区响应非常积极。

这条Issue反映了用户对**多渠道接入体验的一致性和隐私保护**有较高期待，是UX方向的重要信号。

---


## 5. Bug 与稳定性

今日无崩溃、回归或严重Bug报告。唯一的Issue #7681（Slack连接引导隐私问题）属UX缺陷而非功能性Bug，已有一对一的修复PR [#7682](https://github.com/nearai/ironclaw/pull/7682) 在审。无其他稳定性相关问题。

---


## 6. 功能请求与路线图信号

### 新增功能请求

**[Issue #7681](https://github.com/nearai/ironclaw/issues/7681)** — 要求Slack未关联用户的连接引导消息**私密发送**（ephemeral message），并提供一键连接链接以减少往返步骤。

### 关联PR与路线图判断

- [PR #7682](https://github.com/nearai/ironclaw/pull/7682) 正是针对上述Issue的实现，改动包含：在共享频道中仅对触发用户可见的私密引导、附带一键连接链接、保留上下文信息。该PR采用L规模标签，若通过审查，将直接进入下一版本。
- [PR #7651](https://github.com/nearai/ironclaw/pull/7651)（自动化无结果抑制）处于开发中，涉及`trigger_create`至`result_delivery`的确定性行为，可能伴随通知策略的调整，值得关注是否会影响现有用户通知频率。

### 判断

Slack UX改进（#7682）大概率进入下个小版本；自动化通知行为（#7651）体量较大（XL），可能在下个中版本中推出。

---


## 7. 用户反馈摘要

今日仅有一条Issue #7681可提取用户反馈，来自作者sergeiest（结合其同时提交修复PR，可推断为深度用户/贡献者）：

- **痛点**：当未关联用户@机器人时，引导回复在共享频道中公开可见——"这不够私密"。用户可能因尴尬而不愿意在团队频道中暴露未完成连接的状态。
- **流程痛点**：现有引导流程需要"先在Web端连接，再回到Slack再发一次消息"，缺乏上下文衔接，用户在过程中容易迷路或放弃（原Issue引用用户反馈："what's the link to connect you?"）。
- **期望**：一键直达的连接链接，且回复仅自己可见。

此外，今日无其他用户评论或反馈活动。

---


## 8. 待处理积压

今日无新增长期未响应项，但以下PR已存在多日且仍待合并，提醒维护者关注：

| PR | 创建日期 | 等待天数 | 状态 | 说明 |
|----|----------|----------|------|------|
| [#7020](https://github.com/nearai/ironclaw/pull/7020) | 08-02 | 14天 | OPEN | tokio-tungstenite 0.29→0.30升级（S size，低风险）。虽为依赖自动更新，但已搁置两周，建议尽快合入避免依赖积压。 |
| [#7406](https://github.com/nearai/ironclaw/pull/7406) | 08-09 | 7天 | OPEN | CI actions组批量更新（M size，中等风险），涉及claude-code-action等，建议排期审查。 |
| [#7262](https://github.com/nearai/ironclaw/pull/7262) | 08-05 | 11天 | OPEN | wasm组依赖更新（wit-component/parser），可能与WebAssembly相关功能保持兼容性，建议及时合入。 |

另外值得关注的是 [PR #7651](https://github.com/nearai/ironclaw/pull/7651)（自动化无结果抑制，XL size），创建于08-14，已有3天，且更新于今日，仍在活跃开发中，无需额外催促。

> 整体判断：项目当前健康度良好，无紧急待处理事项，但自动化依赖PR的积压时间正在拉长，建议定期批量清理，避免跨版本依赖兼容性问题。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

好的，作为 AI 智能体与个人 AI 助手领域开源项目分析师，我为您呈现 LobsterAI 项目 2026-08-17 的深度动态日报。

---

# LobsterAI 项目动态日报 — 2026-08-17

## 1. 今日速览

今日 LobsterAI 项目活跃度中等偏上。过去 24 小时内，Issue 处理量为 10 条（其中 7 条新开/活跃，3 条关闭），PR 处理量为 17 条（其中 8 条待合并，9 条已合并/关闭）。新版本发布为 0。值得注意的是，今日合并/关闭的 PR 中包含了多个高价值的安全加固与核心 Bug 修复，显示维护团队在稳定性和安全性方面投入显著。但同时，社区活跃度更多集中在老旧 Issue 上，可能意味着新用户引导或已知问题的解决速度仍需关注。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日虽无新版本，但合并/关闭的 9 条 PR 中包含多项关键进展，主要集中在**安全加固**和**核心体验修复**，由开发者 `kayo5994` 主导，对项目的健康度贡献显著。

- **安全加固 (已合并)**:
    - **[PR #1831](https://github.com/netease-youdao/LobsterAI/pull/1831)**: **修复敏感日志泄露**。对主进程与 IM 模块的日志进行脱敏，防止 Bearer token、第三方 API key、SSE 内容及命令行中的一次性 authCode 落入日志文件。
    - **[PR #1832](https://github.com/netease-youdao/LobsterAI/pull/1832)**: **修复 IPC 越权访问**。为 `store:*` IPC 通道添加 key 级别的访问控制，避免渲染进程被污染后可直接读写保存在本地的 `auth_tokens` 和 `github_copilot_github_token`。
    - **[PR #1833](https://github.com/netease-youdao/LobsterAI/pull/1833)**: **修复 `shell.openExternal` 任意协议调用**。增加了 scheme 白名单，拒绝 `file:`、`javascript:`、`data:` 等危险协议，防止恶意 markdown 或模型输出引导打开本地文件或执行代码。
- **核心 Bug 修复 (已合并)**:
    - **[PR #1835](https://github.com/netease-youdao/LobsterAI/pull/1835)**: **修复 `continueSession` 重复推送错误**。解决了 Cowork 服务在会话续接失败时，向用户连续推送两条重复系统错误消息的问题，改善了错误提示的友好性。
    - **[PR #1715](https://github.com/netease-youdao/LobsterAI/pull/1715)**: **修复 OpenClaw 服务端代理请求缺失 session_id**。确保多会话并发时，LobsterAI 服务端能正确识别请求来源，是支持多会话稳定运行的关键后端修复。
    - **[PR #1693](https://github.com/netease-youdao/LobsterAI/pull/1693)**: **优化模型设置入口与草稿保留**。将"未配置模型"的提示改为可直接点击的设置按钮，并修复了发送失败导致输入内容丢失的问题，显著提升新用户上手体验。
- **功能增强 (已合并)**:
    - **[PR #1691](https://github.com/netease-youdao/LobsterAI/pull/1691)**: **新增 Agent 模板导入/导出**。支持将自定义 Agent 配置导出为 `.agent.json` 文件，并支持从本地或远程 URL 导入，方便用户在不同设备间共享和迁移 Agent 配置。
    - **[PR #1760](https://github.com/netease-youdao/LobsterAI/pull/1760)**: **新增 Agent 图片头像支持**。在原有 Emoji 头像基础上，允许上传图片作为自定义 Agent 头像，提升 Agent 的辨识度和个性化。

**结论**：项目核心功能持续迭代，稳定性与安全性得到显著增强，同时新功能的导入/导出和图片头像也符合个性化需求趋势。

## 4. 社区热点

今日讨论最为活跃的 Issue 和 PR 是：

- **[Issue #1813](https://github.com/netease-youdao/LobsterAI/issues/1813)「DeepSeek V4 无法使用」 (已关闭, 8条评论)**: 该问题在 4 月提出，今日被标记为 stale 并关闭。评论数高反映出用户对主流模型兼容性的高关注度，模型的快速迭代对客户端适配提出了持续挑战。
- **[Issue #1698](https://github.com/netease-youdao/LobsterAI/issues/1698)「与智企帝王蟹的端口冲突」 (开放中, 3条评论)**: 用户反馈与另一款软件「智企帝王蟹」存在必然的 `gateway` 端口冲突和进程竞争。这反映了用户环境中多 AI 工具并存的真实场景，对软件的协同能力提出了更高要求。

**诉求分析**：社区热点集中于**外部集成兼容性**（与其他软件冲突）和**模型服务适配**（新模型无法使用），说明用户期望 LobsterAI 能成为一个更开放、兼容性更强的平台。

## 5. Bug 与稳定性

今日报告的 Bug 主要集中在以下几个方面，按严重程度排列：

- **高 - 核心功能失效**:
    - **[Issue #1796](https://github.com/netease-youdao/LobsterAI/issues/1796)「Write tool execution always fail」** (已关闭): 用户反馈 Write/Edit 工具连续数日执行失败，严重影响核心操作。虽然已关闭，但未在今日信息中看到关联的修复 PR，建议维护者确认关闭原因及后续跟进情况。
- **中 - 功能异常**:
    - **[Issue #1813](https://github.com/netease-youdao/LobsterAI/issues/1813)「DeepSeek V4 无法使用」** (已关闭): 新模型接入时的协议不兼容问题，已关闭，可能已通过热修复或用户侧配置解决。
    - **[Issue #1783](https://github.com/netease-youdao/LobsterAI/issues/1783)「更新过后diff异常失灵问题」** (开放中): 用户深入分析了 `extractDiffFromToolInput` 函数的 Bug，定位到 `edit` 分支只从顶层查找 `oldText/newText`，导致无法显示 diff。这为修复提供了非常宝贵的线索。
    - **[Issue #1744](https://github.com/netease-youdao/LobsterAI/issues/1744)「Bug report」** (开放中): 用户上传附件「技术支持联系函.docx」失败，可能是文档上传功能或文件格式支持存在问题。
- **低 - 体验问题**:
    - **[Issue #1714](https://github.com/netease-youdao/LobsterAI/issues/1714)「win11安装图标白色无效」** (开放中): Windows 11 下安装概率性出现图标异常。

## 6. 功能请求与路线图信号

今日提出的功能请求多为中长期优化方向，结合现有 PR，可以看到以下信号：

- **模型控制力增强**:
    - **[Issue #1688](https://github.com/netease-youdao/LobsterAI/issues/1688)「调用大模型如何改变其温度/temperature参数」**: 用户希望能在对话中动态调整模型参数，这将使玩家和高级用户能更精细地控制模型输出。
- **连接方式扩展**:
    - **[Issue #1745](https://github.com/netease-youdao/LobsterAI/issues/1745)「请求改进邮箱的连接方式」**: 用户希望支持 Outlook 邮箱的 OAuth2/新式身份验证，以适配主流邮箱服务的安全策略。
- **会话与数据管理**:
    - **[Issue #1797](https://github.com/netease-youdao/LobsterAI/issues/1797)「建议增加对话删除功能」** (已关闭): 用户希望能批量删除无效对话以保持上下文有效。虽然此 issue 已关闭，但相关联动功能值得关注。
- **定时任务增强**:
    - **[Issue #1751](https://github.com/netease-youdao/LobsterAI/issues/1751)「通知方式里文案不对」**: 定时任务通知中的文案错误，虽是小问题，但关系到功能专业性。

**路线图信号**：除了稳定性修复，开发者已合并的 PR 显示对**Agent 管理**（导入/导出、图片头像）和**交互体验**（朗读功能、Skeleton 加载屏、空状态优化）的重视。用户侧的需求，如动态参数调整、邮箱 OAuth2 支持，是下一步可能纳入路线图的方向。

## 7. 用户反馈摘要

- **对安全与稳定性的担忧**：用户对 `Write/Edit` 工具连续失效（[Issue #1796](https://github.com/netease-youdao/LobsterAI/issues/1796)）表达了强烈不满，这类核心功能的稳定性直接决定用户留存。
- **对深入技术分析的认可**：用户 `MiracleOfrRevolutionary` 在 [Issue #1783](https://github.com/netease-youdao/LobsterAI/issues/1783) 中提供了详尽的前端代码级 Bug 分析，展示了用户社群的高技术水平，此类贡献对项目快速定位问题非常有价值。
- **对便捷性的追求**：用户希望获得更流畅的配置体验（如 [Issue #1688](https://github.com/netease-youdao/LobsterAI/issues/1688) 调整参数、[Issue #1745](https://github.com/netease-youdao/LobsterAI/issues/1745) 连接邮箱），表明用户已不满足于基础功能，而是希望将其深度集成到自己的工作流中。

## 8. 待处理积压

以下 Issue 和 PR 长期未获响应或进展缓慢，建议维护者重点关注：

- **[Issue #1698](https://github.com/netease-youdao/LobsterAI/issues/1698)「与智企帝王蟹的 gateway 端口冲突」**: 已开放 4 个月，被标记为 stale。这是一个必现的兼容性问题，影响特定用户群体的多工具协同使用，建议尝试与相关方沟通或提供规避方案。
- **[Issue #1783](https://github.com/netease-youdao/LobsterAI/issues/1783)「更新过后diff异常失灵问题」**: 用户已给出明确的 Bug 定位，但暂无评论回应。此问题直接影响文件编辑功能的可用性，建议开发者根据用户的详细分析尽快复现并修复。
- **[PR #1682](https://github.com/netease-youdao/LobsterAI/pull/1682)「为 AI 回复消息添加朗读功能」**: 已开放 4 个月，等待合并。该功能由外部开发者贡献，实现完整，建议维护者审视后尽快合并，以鼓励社区贡献。

---
**项目健康度评估**：LobsterAI 项目今天表现整体令人鼓舞。核心团队在处理安全问题和关键 Bug 上非常高效，项目在功能和稳定性上取得了实质进步。然而，社区积压的兼容性问题和技术债务（如 diff 失灵）需要尽快排期解决，以避免“问题陈旧化”导致用户流失。建议维护者加强对陈旧 Issue 的响应和处理，维护一个健康的社区反馈闭环。

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis 项目动态日报 — 2026-08-16

## 1. 今日速览

Moltis 项目在过去 24 小时内保持高活跃度，共处理 5 条 Issue（2 开 3 关）和 17 条 PR（16 条已合并/关闭，1 条待合并），无新版本发布。**安全加固与稳定性修复持续落地**：两项安全修复 PR（zip 路径穿越防护、节点配对签名验证）以及多个构建/测试修复已合入；**新功能方面**，zvec 向量数据库内存后端已合并（#1158），MiniMax Code ACP agent 支持作为新 PR 待合入；**项目健康度亮黄灯**：main 分支仍存在一个编译错误（#1201 已修复）及两个文件超行数上限导致 CI 红色（#1202），需尽快清理。整体来看，项目处于快速迭代期，外部贡献者参与度极高（17 条 PR 中 12 条来自非维护者），社区生态活跃。

## 2. 版本发布

无新版本发布。

## 3. 项目进展

今日合并/关闭的 PR 数量较多（16 条），按功能领域归纳如下：

### 安全加固（高优先级）
- **[security] 加固模型与 zip 路径处理**（[#1180](https://github.com/moltis-org/moltis/pull/1180)）— 修复两类可导致任意文件写入的漏洞（恶意 zip 解压路径穿越、HuggingFace 仓库覆盖用户信任文件），防止代码执行风险。
- **[security] 验证节点配对签名**（[#1179](https://github.com/moltis-org/moltis/pull/1179)）— 将 `node.pair.verify` 绑定到服务器签发的待处理请求，调用者不能再自行提供 key 或 challenge，消除中间人攻击面。

### 新功能
- **zvec 向量数据库内存后端**（[#1158](https://github.com/moltis-org/moltis/pull/1158)）— 基于 Zvec + redb 的替代性内存后端，feature-gated，用于配合 llama-cpp server 嵌入模型使用。从 Issue #1132 关联上下文看，这为主会话管理提供了新的存储选项。

### Bug 修复
- **主会话（main）可删除/归档**（[#1182](https://github.com/moltis-org/moltis/pull/1182)）— 关闭 Issue #1132，移除了 `delete_impl` 和 `is_archivable_entry` 中对主会话的 guard。
- **网关编译修复**（[#1201](https://github.com/moltis-org/moltis/pull/1201)）— 修复 `start_background_tasks` 作用域问题，main 分支可正常编译。
- **推送 fanout 测试修复**（[#1203](https://github.com/moltis-org/moltis/pull/1203)）— 使用暂停时钟运行测试，消除全量套件负载下的竞态。
- **gogcli 路径更新**（[#1191](https://github.com/moltis-org/moltis/pull/1191)）— `moltis sandbox build` 因 gogcli 迁移到 openclaw org 而失败，已修复。
- **wacrawl 安装元数据修复**（[#1192](https://github.com/moltis-org/moltis/pull/1192)）— 同步更新至 openclaw org。
- **macOS bash 3.2 兼容**（[#1194](https://github.com/moltis-org/moltis/pull/1194)）— 修复 `just local-validate-full` 在 macOS 上因空数组展开导致崩溃的问题。
- **recovery phrase 规范化哈希**（[#1186](https://github.com/moltis-org/moltis/pull/1186)）— vault 解锁时对助记词做规范化（去连字符、大写）后再哈希，使存储哈希与派生 KEK 保持一致。
- **CalDAV list_events 时间范围修复**（[#1147](https://github.com/moltis-org/moltis/pull/1147)）— 使用 RFC 4791 `calendar-query` REPORT 替代全量拉取，提高 CalDAV 事件查询效率与准确性。
- **channel activity log 可见性设置**（[#1093](https://github.com/moltis-org/moltis/pull/1093)）— 支持 `all`/`errors_only`/`off` 三档可见性，用户级覆盖通道级。

### 基础设施与集成
- **Slack 原生实时任务卡片**（[#1195](https://github.com/moltis-org/moltis/pull/1195)）— 在 Slack 响应流中渲染原生计划/任务卡片，使用不透明 per-run ID 保护隐私。
- **持久化日历/频道/邮件连接器**（[#1190](https://github.com/moltis-org/moltis/pull/1190)）— 新增 provider-neutral 连接器持久化、原子快照、调度与本地全文搜索；支持只读的 CalDAV、Gmail、Himalaya v2 和频道历史数据集。
- **依赖更新**（[#1200](https://github.com/moltis-org/moltis/pull/1200)）、（[#1184](https://github.com/moltis-org/moltis/pull/1184)）— postcss、js-yaml、undici 安全更新。

**待合并 1 条**：[#1204](https://github.com/moltis-org/moltis/pull/1204) 新增 MiniMax Code ACP agent，已在默认可执行文件检测中加入。

## 4. 社区热点

今日开放讨论较少，社区热点集中在以下方面：

- **[#1202](https://github.com/moltis-org/moltis/issues/1202) — Format CI gate 红色**：`scripts/check-file-size.sh` 对 `store.rs`（1799 行）和 `admin.rs`（1531 行）超出行数限制报错，两条 PR 源自同一提交（9b47001a），阻断 main 分支 CI。该问题直接影响到社区开发者的提交流程，需要尽快修正。
- **[#1205](https://github.com/moltis-org/moltis/issues/1205) — Heartbeat 忽略活动时段配置**：Heartbeat 在配置的 active hours 之外仍持续运行，影响用户资源消耗与隐私预期。
- **安全 PR 获得维持性社区关注**：安全领域三项修复（zip 路径穿越、配对签名、recovery phrase 哈希）均来自外部贡献者（tsauvajon、pxmpsdev），反映社区对 Moltis 安全基线的重视。

## 5. Bug 与稳定性

按严重程度排列今日报告的 Bug：

| 严重程度 | Issue | 描述 | 状态 |
|---------|-------|------|------|
| **高** | [#1202](https://github.com/moltis-org/moltis/issues/1202) | main 分支 CI 红色：两个文件超过 1500 行限制 | **无修复 PR**，需拆分文件 |
| **中** | [#1205](https://github.com/moltis-org/moltis/issues/1205) | Heartbeat 忽略配置的 active hours 持续运行 | **无修复 PR**，新开 Issue |
| **中** | [#1193](https://github.com/moltis-org/moltis/issues/1193) | 推送 fanout 超时断言在全量套件负载下竞态失败 | ✅ **已关闭**（#1203 修复） |
| **低** | [#1189](https://github.com/moltis-org/moltis/issues/1189) | Sandbox 构建因 gogcli URL 错误失败 | ✅ **已关闭**（#1191 修复） |
| **低** | [#1132](https://github.com/moltis-org/moltis/issues/1132) | "main" session 无法删除/归档 | ✅ **已关闭**（#1182 修复） |

**残留风险提示**：在 main 分支修复（#1201）合入且文件大小问题（#1202）解决之前，CI 仍处于不通状态；#1202 需要拆分为多个模块或调整行数限制，目前无对应 PR。

## 6. 功能请求与路线图信号

今日无新的纯功能请求 Issue，但两个新方向信号值得关注：

- **MiniMax Code ACP agent 支持**（[#1204](https://github.com/moltis-org/moltis/pull/1204)）：外部贡献者提交，将 MiniMax Code 集成到默认 agent 检测与注册表中。若合入，将扩展 Moltis 对多种代码助手的支持范围。
- **持久化连接器 + Slack 实时任务卡片**（[#1190](https://github.com/moltis-org/moltis/pull/1190)、[#1195](https://github.com/moltis-org/moltis/pull/1195)）：两个外部贡献者（penso）提交的新功能合入，说明社区对生产级连接器（CalDAV/Gmail/邮件）与协作工具原生集成（Slack 卡片）有较强需求。

## 7. 用户反馈摘要

- **外部贡献者主动修复安全与稳定性问题**：tsauvajon 在 [#1179](https://github.com/moltis-org/moltis/pull/1179) 明确写道：“I'd like to use Moltis, but I've got a couple of security fixes I'd like to get in before doing so.” 表明用户在评估使用前会关注安全基线，且愿意回馈修复代码。
- **社区对测试稳定性的关注**：Lstarsky0 在 [#1193](https://github.com/moltis-org/moltis/issues/1193) 中报告了跨平台（macOS）下测试竞态问题，并主动提交两个相关修复 PR（#1203、#1201），体现了社区对 CI 质量的较高要求。
- **项目治理顺畅性待改进**：Lstarsky0 在 [#1202](https://github.com/moltis-org/moltis/issues/1202) 和 [#1201](https://github.com/moltis-org/moltis/pull/1201) 中指出 main 分支存在编译错误和文件行数超标问题，两者短时间内均未被维护者发现，可能影响外部贡献者的开发效率。

## 8. 待处理积压

以下 Issue/PR 长期未得到响应或合入，建议维护者关注：

- **[#1204](https://github.com/moltis-org/moltis/pull/1204)** — MiniMax Code ACP agent（2026-08-16 创建，待合并）
- **[#1202](https://github.com/moltis-org/moltis/issues/1202)** — Format CI gate 红色（2026-08-16 创建，无修复 PR）
- **[#1205](https://github.com/moltis-org/moltis/issues/1205)** — Heartbeat 忽略 active hours（2026-08-16 创建，无修复 PR）

> 注：以上条目均为今日新开，暂无"长期未响应"的积压问题。但建议维护团队关注 **#1202** 与 **#1201** 的关联性——#1201 修复后 main 分支编译通过，但 CI 仍会因文件超限而红色，需要一并处理才能恢复正常开发流程。

---

*数据来源：[Moltis GitHub 仓库](https://github.com/moltis-org/moltis)，统计窗口为 2026-08-16T00:00:00Z 至 2026-08-17T00:00:00Z（UTC）。*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw 项目动态日报 — 2026-08-17

> CoPaw（agentscope-ai/CoPaw）分析与建议基于 GitHub 公开数据生成。

---

## 1. 今日速览

过去24小时内 CoPaw 社区活跃度处于**高位**，共产生 9 条 Issue 动态与 9 条 PR 动态。其中，**7 个新 PR 集中提交**（多为 first-time-contributor），并伴随 3 个 Issue 被关闭，显示出社区贡献热情高涨、项目维护节奏紧凑。值得关注的是，**多个 PR 直指已报告的 Bug 并给出针对性修复**，今日暂无新版本发布，也暂未见 PR 被合并，项目正处于**提交密集、待合并积压**的窗口期。整体来看，项目健康度良好，但因大量修复集中在 24 小时内涌入，维护者未来 48 小时的 Review 压力较大。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日无 PR 被合并或关闭，暂无法从合并视角总结功能增量。但从 PR 提交内容看，项目即将迎来一波**体验修复与功能增强**：

- **[#6940] 原生 DataPaw 应用运行时与持久分析工作区** — 该 PR 已标记 `ready-for-human-review`，是近期最重量级的功能提交之一。若被合并，将标志着 CoPaw 从纯 Web 体验向**原生桌面分析应用**延伸，属里程碑级进展。详见 [PR #6940](https://github.com/agentscope-ai/QwenPaw/pull/6940)
- **5 个由 suantea 提交的修复类 PR**（[#7064](https://github.com/agentscope-ai/QwenPaw/pull/7064)、[#7066](https://github.com/agentscope-ai/QwenPaw/pull/7066)、[#7069](https://github.com/agentscope-ai/QwenPaw/pull/7069)、[#7070](https://github.com/agentscope-ai/QwenPaw/pull/7070)、[#7071](https://github.com/agentscope-ai/QwenPaw/pull/7071)）分别修复了 cron 更新不同步、OAuth2 refresh_token 轮换未持久化、历史消息图片裂图、OpenAI Responses API 下 view_video 静默失败、view_video 硬编码 2MB 上限等一系列问题。若全部合并，将一次性修复 5 个已知 Bug，显著提升稳定性。
- **[#6302] 统一 Provider 发现、模型元数据与路由** — 长时间挂起的架构级 PR 仍在推进中，今日有更新，见 [PR #6302](https://github.com/agentscope-ai/QwenPaw/pull/6302)。
- **[#7073] Skill 名称去重逻辑** — Ferrum360 提交了工作区与内置同名 Skill 重复加载的修复方案，见 [PR 对应 Issue #7073](https://github.com/agentscope-ai/QwenPaw/issues/7073)。

---

## 4. 社区热点

今日讨论聚焦于 **Bug 反馈与修复的联动**，以及**针对数据分析和办公场景的深度功能需求**。最活跃的讨论集中在以下条目：

- **[issue #7063] Agent 执行工具调用时必现崩溃**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/7063)）— 该 issue 在一天内关闭并有 3 条评论，反馈了 `async for` 遍历 coroutine 的 TypeError 问题，属于影响核心功能的严重 Bug。
- **[issue #7003] Memory for QwenPaw agents — 97.5% fewer tokens (ViBo)**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/7003)）— 该 issue 提出了基于 ViBo 方案将记忆 token 压缩 97.5% 的 Proposал，3 条评论讨论热度不减，反映出用户对**长会话成本**的焦虑。
- **[PR #6940] DataPaw 原生应用运行时**（[链接](https://github.com/agentscope-ai/QwenPaw/pull/6940)）— 尽管为 PR，但因其带有多张截图且是重量级功能，其引发的关注度不低于热门 Issue。用户对**持久化分析工作区**的需求可见一斑。

---

## 5. Bug 与稳定性

今日报告的 Bug 按严重程度排列如下：

| 严重程度 | Issue | 问题简述 | 是否有修复 PR |
|---------|-------|---------|-------------|
| **严重** | [#7063](https://github.com/agentscope-ai/QwenPaw/issues/7063) (已关闭) | 工具调用时必现崩溃：`_acting` 返回 coroutine 却用 `async for` 遍历，触发 TypeError | 已关闭，修复方案待确认 |
| **中等** | [#7074](https://github.com/agentscope-ai/QwenPaw/issues/7074) | 正常运行高频崩溃，需刷新页面才能恢复 | 暂无 |
| **中等** | [#7065](https://github.com/agentscope-ai/QwenPaw/issues/7065) | 多轮讨论后无法回看早期聊天记录 | 暂无 |
| **较低** | [#6471](https://github.com/agentscope-ai/QwenPaw/issues/6471) (已关闭) | APScheduler Cron 任务在事件循环空闲后 misfire | 已关闭，未见对应修复 PR |
| **较低** | [#7052](https://github.com/agentscope-ai/QwenPaw/issues/7052) | 插件 API 无法隐藏 system_prompt | 暂无，属于功能增强 |

此外，以下**已有对应修复 PR 的 Bug** 值得关注（来自今日新提交的 PR 链）：

- **历史消息图片裂图**：已由 [PR #7069](https://github.com/agentscope-ai/QwenPaw/pull/7069) 修复。
- **view_video 在 OpenAI Responses API 下静默失败**：已由 [PR #7070](https://github.com/agentscope-ai/QwenPaw/pull/7070) 修复。
- **view_video 硬编码 2MB 上限导致大视频被省略**：已由 [PR #7071](https://github.com/agentscope-ai/QwenPaw/pull/7071) 修复。
- **OAuth2 刷新令牌轮换未持久化，导致远期认证失败**：已由 [PR #7066](https://github.com/agentscope-ai/QwenPaw/pull/7066) 修复。
- **cron update 后顶层文本不同步**：已由 [PR #7064](https://github.com/agentscope-ai/QwenPaw/pull/7064) 修复。

---

## 6. 功能请求与路线图信号

- **[issue #7062] 支持 Agent/会话级 reasoning_effort 覆盖**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/7062)）— 用户希望不同角色（快速问答 vs 深度研究）使用不同思考强度。这属于**精细化模型控制**方向，与 [#6302 的模型路由 PR](https://github.com/agentscope-ai/QwenPaw/pull/6302) 方向一致，**极有可能在模型路由重构完成后的下一版本中支持**。
- **[issue #7068] 文件查看器支持更多语言（C#/Shader）**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/7068)）— 面向游戏开发场景的轻量需求，实现成本低，有较大概率被纳入后续小版本。
- **[issue #7052] 插件 API 增加 system_prompt 权限**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/7052)）— 企业用户希望在插件交互界面隐藏公司的提示词，这涉及**权限隔离设计**，属于安全/合规方向，优先级可能视企业客户反馈而定。
- **[PR #6940] DataPaw 原生应用运行时**（[链接](https://github.com/agentscope-ai/QwenPaw/pull/6940)）— 从截图和描述看，该功能已进入 Ready for Review 阶段，**极有可能成为下一版本的核心卖点**。

---

## 7. 用户反馈摘要

- **核心痛点集中在“多轮对话/长会话”体验**：多位用户反馈无法回看历史聊天（[#7065](https://github.com/agentscope-ai/QwenPaw/issues/7065)）、崩溃后需刷新页面（[#7074](https://github.com/agentscope-ai/QwenPaw/issues/7074)）、以及每次请求发送全部记忆导致 token 成本高昂（[#7003](https://github.com/agentscope-ai/QwenPaw/issues/7003)）。
- **企业/办公场景用户对数据安全和提示词保护有明确诉求**（[#7052](https://github.com/agentscope-ai/QwenPaw/issues/7052)）。
- **个人开发者贡献积极**：今日 7 个 PR 中有 6 个来自首次贡献者，且均为针对性修复，说明项目的 Issue 标注和文档质量对新手较为友好。
- **对视频处理能力有期待**：PR #7070 和 #7071 的提交表明用户希望在 CoPaw 中更可靠地使用本地视频作为模型输入，且对 provider 的容量上限有感知（如 Volcengine Ark 配置的 50MB inline cap）。

---

## 8. 待处理积压

- **[PR #6302] 统一 Provider 发现、模型元数据与路由**（[链接](https://github.com/agentscope-ai/QwenPaw/pull/6302)）— 自 7-21 创建至今近一个月未合并，涉及模型路由的核心架构重构，可能是当前最重要的待办事项。建议维护者评估其依赖链，避免后续功能重复实现。
- **[issue #6471] Cron 任务 misfire**（[链接](https://github.com/agentscope-ai/QwenPaw/issues/6471)）— 虽已关闭，但未见到对应的修复 PR 或 release note，建议确认修复落地情况，避免用户升级后仍遭遇此问题。
- **[PR #6940] DataPaw 原生应用运行时**（[链接](https://github.com/agentscope-ai/QwenPaw/pull/6940)）— 已标记 `ready-for-human-review`，但今日尚无 Review 动态。该 PR 依赖 [专用 infra repo](https://github.com/)，需评估其引入的依赖范围与维护成本。

---

*本日报由 AI 分析师根据 GitHub 公共数据自动生成，仅供项目健康度参考，不构成对任何个人或组织的评价。*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw 项目动态日报 — 2026-08-17

> 数据窗口：2026-08-16 至 2026-08-17 | 数据来源：GitHub Issues/PR 活动

---

## 1. 今日速览

项目活跃度极高，过去24小时内有 48 条 Issue 更新与 50 条 PR 更新，但大部分为追踪器（Tracker）与大型 RFC 的滚动态更新，并非全新提交。今日无新版本发布，但有 2 个 Issue 关闭、4 个 PR 合并/关闭，其中 **PR #9580（HTTP 出口安全加固，P1）** 合并是今日最重要的里程碑。社区讨论集中在 5 个 RFC 类问题上（评论数 14–23），讨论焦点已经从单一功能转向治理流程（工作泳道、维护者决策队列）与跨领域架构统一（附件架构、聊天补全协议、供给者安全态势）。值得警惕的是，出现了两个与并行运行测试门禁相关的测试稳定性回归（#9965、#10013），已有针对性修复 PR 在途，但测试基础设施的稳定性仍是近期风险点。

---

## 2. 版本发布

今日无新版本发布。最近一次版本为 0.8.4（依据 #6808 中的版本标记推断）。

---

## 3. 项目进展

> 基于今日关闭/合并的 PR 与显著推进的追踪器。

**已合并（显著里程碑）：**

- **PR #9580 — `fix(security): harden built-in HTTP egress on the shared network guard`**（P1，合并于 2026-08-16）
  这是插件出口策略的基石（ADR-013 方向），将网络分类原语下沉到 `zeroclaw-infra::net_guard`，并加固内置 HTTP 出口边界。**影响：** 该合并为后续两个 P1 PR（#9582 出口策略强制、#9584 CLI 授权仪式）铺平了道路，出口安全三步走已走完第一步。该 PR 同时是 #9137、#9109、#10046 的依赖前置。
  
- **PR #9416 — `docs(tools): document AllToolsResult.tools as pre-filter registry`**（XS，已合并）
  澄清了工具注册表过滤语义，消除 `tools` 与 `unfiltered_tool_arcs` 之间的文档歧义。低风险，文档补全。

**值得关注的进行中 PR（可能有重大进展）：**

- **#9808 — `chore(deps): bump the rust-all group with 46 updates`** — 大规模依赖升级，涉及 clap、tokio、serde 等核心库。此 PR 若合并会造成广泛的破坏面，需要重点测试。
- **#9547 — `chore(channels): upgrade CPAL to 0.18`** — Voice Wake 通道的音频库升级，涉及 API 迁移。

**整体评估：** 项目正处在从「功能扩张」转向「安全加固与治理规范化」的阶段。`#6808`（工作泳道/Board 自动化）和 `#8692`（维护者决策队列）等治理型追踪器被持续更新，说明维护团队在刻意收紧合并节奏与决策流程。

---

## 4. 社区热点

> 基于评论数排序，反映社区最关心的争议与技术方向。

**#6808 — RFC: Work Lanes, Board Automation, and Label Cleanup**（23 条评论，Rev. 25，治理型追踪器）
围绕工作流路由与标签清理的治理 RFC，已进入「已批准 / 推广中」阶段。社区关注点在于标签系统的精简与维护者工作量降低。这表明项目开始严肃对待自身的**元工作流**效率。

**#8603 — RFC: ZeroClaw Chat Completions profile**（22 条评论，P2，高风险）
社区最集中的功能声音之一：希望 ZeroClaw 暴露 OpenAI Chat Completions 兼容协议，以接入 Open WebUI、LobeChat、Continue.dev、Aider、LangChain 等生态。若该 RFC 落地，ZeroClaw 将不再只是一个通道网关，而是一个标准 API 服务器，**可能成为 0.9 版本最重要的功能**。

**#9488 — RFC: Unified attachment architecture for web chat and channels**（17 条评论，P2，高风险）
统一 Web 聊天与各渠道的附件处理架构。目前各渠道附件处理分散，维护成本高；该 RFC 提案通过后有望显著降低渠道间行为差异。目前状态为 Proposed。

**#6954 / #6971 — 内部启动 Agent 轮次的溯源/绑定契约 & 安全态势与凭据边界**（各 14 条评论，P2，高风险）
一个解决系统自身触发的对话的溯源与回复契约问题；另一个统一定义凭据边界、沙箱、渠道授权的全景安全策略。两者均处于 revision 阶段，说明维护者正在认真回应社区对**安全边界定义混乱**的抱怨。

**#8692 — Maintainer decision queue for RFCs and design issues**（13 条评论）
一个主动暴露维护者决策瓶颈的追踪器。社区可在此看到哪些 RFC 等待裁决。这是一种很好的透明度实践。

---

## 5. Bug 与稳定性

> 按严重程度排列。S1 = 阻塞；S2 = 降级；S3 = 轻微。

| 严重度 | Issue | 描述 | 状态 | Fix PR |
|---|---|---|---|---|
| **S1** | [#10013](https://github.com/zeroclaw-labs/zeroclaw/issues/10013) | Edge TTS 取消测试在并行加载下可能漏掉假子进程启动，导致 `Parallel Runtime Test` job 间歇性失败 | 已接受 | 无专门 PR，可能与 #10011 相关 |
| **S1** | [#9965](https://github.com/zeroclaw-labs/zeroclaw/issues/9965) | 运行时写入的可执行测试固件在并行运行时门禁下遭遇 ETXTBSY | 已接受 | [#10011](https://github.com/zeroclaw-labs/zeroclaw/issues/10011)（Task，进行中） |
| **S2** | [#10037](https://github.com/zeroclaw-labs/zeroclaw/issues/10037) | `POST /api/cron` 静默将无效 `session_target` 存为 `isolated`，与 `cron_add` 工具的严格校验行为不一致 | 进行中/已接受 | 无 |
| **S2** | [#10020](https://github.com/zeroclaw-labs/zeroclaw/issues/10020) | Agentic 独立 delegate 忽略目标 `thinking` 策略 | 进行中/已接受 | 无 |
| **S2** | [#9953](https://github.com/zeroclaw-labs/zeroclaw/issues/9953) | SOP 步骤 schema 校验拒绝双重编码输出对象而非解包 | 已关闭 | 已解决（关闭） |
| **S2** | [#9811](https://github.com/zeroclaw-labs/zeroclaw/issues/9811) | `/health` 报告从未连接过的频道为健康（Telegram token 无效时仍报 healthy） | 已接受 | 无，但值得关注——健康状态不可信是运维层面的 S1 隐患 |
| **S2** | [#9655](https://github.com/zeroclaw-labs/zeroclaw/issues/9655) | 审批卡片无位置信息，同一条消息的多张卡片在点击前无法区分 | 已接受 | 无 |

**测试基础设施风险提示：** #9965 与 #10013 均指向并行运行时门禁（`Parallel Runtime Test`）在 master 上间歇性失败。这类问题若不快速修复会侵蚀 CI 可信度，进而拖慢所有 PR 合并速度。当前 #10011 正在替换运行时写入可执行文件的测试方式。

---

## 6. 功能请求与路线图信号

> 按纳入下一版本的可能性排序。

| 功能 | Issue/PR | 信号强度 | 分析 |
|---|---|---|---|
| **OpenAI Chat Completions 兼容层** | [#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)（RFC，22 评论） | ⭐⭐⭐⭐⭐ | 评论数最高、涉及生态工具最广，一旦落地将带来大量新用户。已有若干 P2 标签，但 RFC 尚未批准。预计 0.9 或 1.0 关键候选 |
| **统一附件架构** | [#9488](https://github.com/zeroclaw-labs/zeroclaw/issues/9488)（RFC，17 评论） | ⭐⭐⭐⭐ | 跨 Web 与渠道的附件一致性，直接影响 Telegram/Signal 媒体体验。仍处 Proposed |
| **Gemini Live 语音通道** | [#8780](https://github.com/zeroclaw-labs/zeroclaw/issues/8780)（RFC，v2 已改版） | ⭐⭐⭐ | 已重写为 broker 契约。需求真实（语音场景），但依赖 Gemini 生态，优先级可能受制于供给商合作 |
| **Swift 临时 Agent 洪泛（swarm TUI）** | [#10025](https://github.com/zeroclaw-labs/zeroclaw/issues/10025)（RFC，新开） | ⭐⭐ | 今日新开，尚需观察。若与规划中的控制平面（GoalTaskRecord）打通，可能成为有趣的轻量编排方案 |
| **SOP 里程碑 5/5** | [#8288](https://github.com/zeroclaw-labs/zeroclaw/issues/8288)（Tracker） | ⭐⭐⭐⭐ | 多 PR 配合推进已在进行，是既定路线图。预计通过 #8288 持续跟踪 |
| **按日期范围的 Cron 条件调度** | [#7887](https://github.com/zeroclaw-labs/zeroclaw/issues/7887)（已接受，P3） | ⭐⭐ | 已接受但 P3，短期不会优先 |

**路线图信号总结：** 0.8.x 当前重点是**安全加固**（出口策略三步走）与**治理规范化**（RFC 决策队列）。0.9 的主要方向则聚焦于**互操作性**（Chat Completions 协议、统一附件架构）与**语音能力**（Gemini Live）。

---

## 7. 用户反馈摘要

> 从 Issues 评论与行为模式中提炼的真实用户声音。

- **生态系统接入诉求强烈：** #8603 的 22 条评论显示，用户希望 ZeroClaw 对接 Open WebUI、LobeChat、Continue.dev 等工具，说明其用户群体中开发者/AI 工程师占比高，希望将 ZeroClaw 作为统一后端而非孤立网关。社区诉求是「不要重造客户端协议」。

- **安全配置负担重，可观测性不足：** #6971（安全态势 RFC）与 #9621（遥测 RFC）均指向同一痛点：运维者不知道自己当前的安全策略是什么、某个功能是否真的有人在用。这驱动了 #8692 决策队列与 #9621 遥测提案的活跃讨论，可视为对「黑盒配置过多」的总体反馈。

- **渠道行为不一致（群聊会话、附件处理、媒体）：**
  - `#9772`（Telegram 群聊 per_user_session toggle）与 `#9655`（审批卡片混淆）暴露了同一类问题：多渠道不断复制逻辑导致行为漂移。用户 Jason 在 #9655 的评论中明确指出「如果不盯着卡片，你根本不知道哪张对应哪个工具调用」。
  - `#9488`（统一附件架构）与 `#7891`（Signal 媒体支持）则进一步说明：附件/媒体在各渠道的碎片化实现已成为社区共识性问题。

- **并行测试假阳性引发信任下降：** #9965 的评论中维护者表示该失败是环境问题而非代码问题，但 S1 的标签（并行门禁间歇失败）意味着每次 CI 失败都要人工排查，社区已开始表达对 CI 红绿灯的「狼来了」疲劳感。

- **Delegate 模式用户对「子 Agent 是否遵守父会话策略」敏感：** #10020 的快速响应（新开 1 天内即获 accepted 标签）表明这是维护者认为真实存在的问题，而非边缘用例。

---

## 8. 待处理积压

> 长期未闭合或需维护者决策的条目，按风险/影响排序。

- **#6808 — RFC: Work Lanes, Board Automation, and Label Cleanup**（[链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)，已 88 天）
  这是一份典型的高维护成本追踪器——共修订了 25 次。尚未看到明确的落地 PR，建议维护者给出阶段性的时间表或拆分计划，避免成为「永久进行中」的盖子。

- **#9609（若存在）— 注意：** 数据快照未显示，跳过。

- **#8692 — Maintainer decision queue**（[链接](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)，已 43 天）
  该队列本身就是等待裁决的 RFC 集合。当前至少有 8 个 RFC 挂着 `needs-maintainer-review` 标签（如 #8603、#9488、#6971、#9621 等）。维护者需优先处理至少 3 个高评论 RFC，否则社区会产生「提案石沉大海」的失望情绪。

- **#6165 — RFC: Lighter core through external integrations**（[链接](https://github.com/zeroclaw-labs/zeroclaw/issues/6165)，已 112 天，14 条评论，`status:no-stale`）
  提出将非核心集成移出默认 core，与 #9853（移除 aardvark-sys 和 zeroclaw-robot-kit）方向一致，但尚无正式决策。该提案执行周期长且敏感（涉及删除），建议在 #8692 队列中明确裁决。

- **#9811 — /health 报告未连接频道为健康**（[链接](https://github.com/zeroclaw-labs/zeroclaw/issues/9811)，已 9 天，已接受）
  从运维视角看这是 S1 级误报（健康指标不可信），目前仅标记 accepted 但无 assignee、无 fix PR，建议尽快安排。

- **信号：** #10013（#9965 的姊妹）与 #10011 有紧密依赖，合并 #10011 前不要关闭 #10013。

---

**总体健康度评估：**

| 维度 | 状态 | 说明 |
|---|---|---|
| 社区活跃度 | 🟢 高 | 48 Issues / 50 PRs，评论总量可观 |
| 安全态势 | 🟡 加固中 | 出口策略三步走已迈出第一步，但仍有两个 P1 在途 |
| 测试稳定性 | 🔴 警示 | 并行门禁间歇失败（#9965/#10013）为当前最大技术债 |
| RFC 决策效率 | 🟡 中等 | 决策队列已建立，但积压明显 |
| 新功能推进 | 🟢 正常 | Swarm RFC 新开、CPAL 升级在途，无停滞迹象 |

**维护者关注优先级建议：** ① 合并 #10011 修复测试稳定性 → ② 在 #8692 中尽快裁决 #8603 与 #9488 两个高热度 RFC → ③ 为 #9811（/health 误报）指派负责人或将 fix 计划写入里程碑。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*