# OpenClaw 生态日报 2026-08-06

> Issues: 500 | PRs: 500 | 覆盖项目: 13 个 | 生成时间: 2026-08-06 01:16 UTC

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

# OpenClaw 项目动态日报 — 2026-08-06

## 1. 今日速览

过去 24 小时项目维持高热度的社区活跃度：共 500 条 Issue 更新、500 条 PR 更新，其中 57 条 Issue 被关闭、70 条 PR 被合并/关闭。今日无新版本发布。社区讨论重心仍集中在**会话状态管理（session-state）**与**消息丢失（message-loss）**两大顽疾上，多起 P0/P1 级问题的标签集中在 `impact:session-state`、`impact:message-loss` 和 `impact:crash-loop`。值得关注的是，今日出现了两条针对 **P0 级数据安全** 的 Issue（#119090 媒体误删、#119263 数据库迁移失败），需维护者优先响应。项目整体处于"高活跃、高积压、修复跟进速度尚可"的状态。


## 2. 版本发布

今日无新版本发布。上一个版本为 2026.7.2（b4f01af），目前已有多起用户反馈升级后遇到的问题（见下文 Bug 章节）。


## 3. 项目进展

今日共合并/关闭 70 条 PR。较值得关注的进展包括：

- **PR #118796 [已关闭/被取代] fix(session): require a real context snapshot for CLI usage**（[链接](https://github.com/openclaw/openclaw/pull/118796)）— 由 clawsweeper[bot] 自动生成，修复 #118772 中 CLI 上下文快照不准确导致过早压缩的问题。虽被 #118792 取代，但表明针对上下文压缩的修复已有明确方向。
- **PR #119792 [已关闭/被取代] fix(backup): skip ephemeral coordinator lock databases**（[链接](https://github.com/openclaw/openclaw/pull/119792)）— 修复 `openclaw backup create --verify` 在网关运行中因零字节锁数据库而失败的问题，属实用的运维修复。
- **PR #118792 [待合并] fix(agents): never persist cumulative usage as session context snapshot (#118772)**（[链接](https://github.com/openclaw/openclaw/pull/118792)）— 修复 `sessionEntry.totalTokens` 被多轮工具循环的累计用量污染、导致过早压缩的关键问题。
- **PR #119783 [新开] fix(venice): replay Gemini tool signatures by turn occurrence**（[链接](https://github.com/openclaw/openclaw/pull/119783)）— 修复 Venice Gemini 工具调用因签名回放错误而失败的兼容性问题。

总体来看，今日合入的 PR 偏小步快走，以增量修复为主，无重大架构变更。


## 4. 社区热点

今日讨论热度最高（评论数最多）的议题集中在以下几处：

**① Issue #116201 [P1] Realtime voice work can retain unbounded provider and consult state**（59 条评论，[链接](https://github.com/openclaw/openclaw/issues/116201)）— 今日社区讨论的绝对焦点。实时语音会话在慢速/阻塞/突发性 provider 行为下会无限积累 consult 状态、provider 帧和预生成音频，缺乏硬性所有权边界。59 条评论说明此问题影响面广、复现路径复杂，社区在积极补充触发条件和复现细节，等待维护者给出产品层面的决策（已挂 `needs-product-decision`）。

**② Issue #7707 [P2] Feature Request: Memory Trust Tagging by Source**（27 条评论，[链接](https://github.com/openclaw/openclaw/issues/7707)）— 社区对"记忆投毒"（memory poisoning）攻击面的关注度持续走高。该 issue 自 2 月提出后长期活跃，请求按来源（用户指令/网页抓取/第三方技能）对记忆条目打信任标签。这已是连续多日的高评论量 issue，表明用户对安全防护的功能需求相当迫切。

**③ Issue #44925 [P1] Subagent completion silently lost**（25 条评论，[链接](https://github.com/openclaw/openclaw/issues/44925)）— 子代理任务在超时/失败时静默丢失结果，无重试、无通知、无自动重启。Telegram 论坛机器人场景下多个失败模式叠加，社区讨论集中在复现路径的补充与对错误码（E31/E42/E45）含义的猜测。

**④ Issue #118846 [已关闭] Gateway main thread saturated by plugin-metadata snapshot + fs statting**（19 条评论，[链接](https://github.com/openclaw/openclaw/issues/118846)）— 已关闭，说明问题已定位并处理。


## 5. Bug 与稳定性

按严重程度排列：

### 🔴 P0 — 数据安全级

- **Issue #119090 [P0] managed media cleanup fails open and permanently deletes a session's generated media**（[链接](https://github.com/openclaw/openclaw/issues/119090)）— **已关闭**。当会话存储不可读（权限/I/O/锁库）时，媒体清理会"失败开放"，将所有媒体误判为未引用并永久删除。标签含 `clawsweeper:bulk-filed`，属于批量上报。已关闭说明已修复，但数据已删的用户无法挽回。
- **Issue #119263 [P0] Agent DB v14→v15 migration fails: 'no such column: entry_valid'; gateway refuses to start**（[链接](https://github.com/openclaw/openclaw/issues/119263)）— 从 2026.7.1 升级到 2026.7.2 后数据库迁移失败，`openclaw doctor --fix` 无法修复，网关拒绝启动。已有 fix PR 关联（`clawsweeper:linked-pr-open`），等待合并。

### 🟠 P1 — 影响核心功能

- **Issue #44925 [P1] Subagent completion silently lost — no retry, no notification**（[链接](https://github.com/openclaw/openclaw/issues/44925)）— 25 条评论，社区持续关注中。仍无 fix PR。
- **Issue #86519 [P1] Agent repeats identical replies 2-10x on Telegram after 5.20 update**（[链接](https://github.com/openclaw/openclaw/issues/86519)）— 消息重复发送，5.22 部分缓解但仍未完全修复，已挂 `needs-live-repro`。
- **Issue #113306 [P1] SQLite snapshot restore lacks end-to-end crash and identity guarantees**（[链接](https://github.com/openclaw/openclaw/issues/113306)）— 快照恢复可能报告成功但目录/身份守卫未落盘。仍待维护者处理。
- **Issue #85251 [P1] Codex app-server emits notification:turn/started then goes silent**（[链接](https://github.com/openclaw/openclaw/issues/85251)）— 嵌入式运行卡死至 stuck-session recovery 窗口（默认 360s）。仍开放。
- **Issue #112423 [P1] Large SQLite transcript cleanup blocks the gateway event loop**（[链接](https://github.com/openclaw/openclaw/issues/112423)）— 大转录归档在网关线程上执行完整物化/压缩/IO，阻塞事件循环。仍开放。
- **Issue #106231 [P1] Loop detection blocks exec but does not terminate stuck agent run**（[链接](https://github.com/openclaw/openclaw/issues/106231)）— 循环检测只拦截工具调用但会话仍无限运行。已有关联 PR。
- **Issue #109490 [P1] codex app-server: turn interrupted after client-delegated message tool result**（[链接](https://github.com/openclaw/openclaw/issues/109490)）— 承诺的工作永不执行，7.1 引入的回归。仍开放。
- **Issue #116022 [P1] beta.5 /new reuses stable session ID and cannot recover retired Codex binding tombstone**（[链接](https://github.com/openclaw/openclaw/issues/116022)）— 已关联 PR，等待合并。
- **Issue #90098 [P1] Stack-safe large attachment handling for Control UI and gateway**（[链接](https://github.com/openclaw/openclaw/issues/90098)）— 大 PDF 上传导致堆栈溢出，已关联 PR。
- **Issue #117358 [P1] Post-turn compaction ignores compaction/reset boundaries and delays completed replies**（[链接](https://github.com/openclaw/openclaw/issues/117358)）— 回归问题，已关联 PR。
- **Issue #119557 [P2] chat delta throttle has no trailing flush**（[链接](https://github.com/openclaw/openclaw/issues/119557)）— 150ms 节流器只有前沿触发，被抑制的块可能永远不被投递。已关联 PR。

### 🟡 P2 — 功能受损/体验问题（选择）

- **Issue #51429 [P2] 工作路径被硬编码合并发布**（[链接](https://github.com/openclaw/openclaw/issues/51429)）— 中文社区报告的路径硬编码问题，12 条评论，至今仍开放，已挂 `needs-product-decision`。
- **Issue #77306 [P2] qqbot 消息重复发送**（[链接](https://github.com/openclaw/openclaw/issues/77306)）— QQ 渠道消息因 hook 在 WebChat 回放时触发而重复发送。仍开放。
- **Issue #97616 [P1] OpenClaw leaks unreaped hook/tool child processes**（[链接](https://github.com/openclaw/openclaw/issues/97616)）— 僵尸进程累积导致运行时性能退化。仍开放。
- **Issue #53540 [P1] Embedded runner "Network connection lost" on large tool call parameters**（[链接](https://github.com/openclaw/openclaw/issues/53540)）— 大型工具调用参数生成超过底层请求超时。仍开放。


## 6. 功能请求与路线图信号

今日社区提出的功能需求中，以下方向值得关注：

**🔐 安全与信任（社区呼声最高）**
- **Issue #7707 Memory Trust Tagging by Source**（[链接](https://github.com/openclaw/openclaw/issues/7707)）— 27 条评论，连续多日高热度。社区对记忆投毒攻击的担忧真实且紧迫。目前无对应 PR，但已挂 `needs-security-review` 和 `needs-product-decision`，方向明确。
- **PR #113111 fix(whatsapp): label voice transcripts as untrusted**（[链接](https://github.com/openclaw/openclaw/pull/113111)）— 与 #7707 同属"来源信任"主题，将 WhatsApp 语音转写标记为不可信来源。该 PR 已开两日，虽小但方向正确。

**☁️ 云部署支持**
- **Issue #13597 [P2] Add comprehensive AWS deployment guide (EC2, ECS, Lambda)**（[链接](https://github.com/openclaw/openclaw/issues/13597)）— 自 2 月起长期开放，获得 4 个 👍，始终无进展且未关闭。云部署文档缺失是用户采纳的重要阻碍。

**📊 可观测性与诊断**
- **PR #107937 fix: include plugin LLM calls in usage diagnostics**（[链接](https://github.com/openclaw/openclaw/pull/107937)）— 解决插件调用 `runtime.llm.complete` 时的 token 用量缺失问题，利于运维成本追踪。
- **Issue #44289 Generate secretref reference docs from secret target registry metadata**（[链接](https://github.com/openclaw/openclaw/issues/44289)）— 文档同步自动化。

**🔧 运维体验**
- **PR #91726 feat(gateway): add POST /api/mcp/servers/:id/reload endpoint**（[链接](https://github.com/openclaw/openclaw/pull/91726)）— 解决 Composio MCP 工具列表变更无通知、需手动重载的问题。该 PR 6 月已开，仍待 proof。
- **Issue #50205 [Feature]: Support configurable request labels for Gemini API calls (GCP billing tracking)**（[链接](https://github.com/openclaw/openclaw/issues/50205)）— GCP 计费成本归因需求，5 条评论，方向明确。

**🧩 渠道能力扩展**
- **Issue #53654 Discord: Support messageUpdate and messageDelete events**（[链接](https://github.com/openclaw/openclaw/issues/53654)）— 3 个 👍，6 条评论。编辑后重处理、删除后取消的需求，对 Discord 用户有实际价值。


## 7. 用户反馈摘要

来自 Issues 评论的真实用户声音：

**😤 挫折点：消息重复/丢失反复出现**
- Telegram 重复回复（#86519）："升级到 5.22 后从 8-10 次降到 2-3 次，但仍未修好" —— 用户 w3-design1 的挫败感清晰可见。
- QQ 渠道重复发送（#77306）："`message_sending` hook 在 WebChat 历史回放时被触发" —— 触发条件已定位但修复未落地。
- 子代理结果静默丢失（#44925）："任务失败完全没有通知，我们直到用户投诉才知道" —— 用户 IIIyban 对可观测性缺失的抱怨。

**😠 对代码质量的不信任**
- **Issue #51429** 中用户标题直指"有人把工作路径 hardcode 进代码而且居然被合并发布了"，获 12 条评论但至今未获维护者正面回应，社区对 PR 审查质量的质疑正在积累。

**🧐 对安全风险的实际担忧**
- **Issue #7707** 的评论中，用户 LumenLantern 具体描述了攻击场景：恶意网页中隐藏的指令被记忆系统吸收后长期影响后续行为。社区对该方向的讨论已从"要不要做"转向"怎么做"。

**🙏 功能诉求的耐心等待**
- **Issue #13597** AWS 部署指南，4 个 👍 + 7 条评论，自 2 月开至今无动静，用户 trevorgordon981 感叹"云部署文档缺失是采纳的最大阻碍"。
- **Issue #53654** Discord 编辑/删除事件支持，用户 sws-apps 在评论中描述了实际工作流中的痛点："编辑后不能重新触发 agent，删除后 agent 仍在继续处理"。


## 8. 待处理积压

以下为长期未获有效响应或迟迟未关闭的重要事项，建议维护者重点关注：

| Issue/PR | 创建时间 | 状态 | 优先级 | 备注 |
|---|---|---|---|---|
| [#51429 工作路径硬编码](https://github.com/openclaw/openclaw/issues/51429) | 2026-03-21 | OPEN | P2 | 中文社区强烈关注，12 条评论，至今无维护者回复。社区对代码审查质量的信任正在流失 |
| [#7707 记忆信任标签](https://github.com/openclaw/openclaw/issues/7707) | 2026-02-03 | OPEN | P2 | 27 条评论持续增长，安全方向需求强烈，已挂 `needs-product-decision` 但无时间表 |
| [#13597 AWS 部署指南](https://github.com/openclaw/openclaw/issues/13597) | 2026-02-10 | OPEN | P2 | 4 个 👍 + 7 条评论，5 个月无实质进展 |
| [#44134 Google Antigravity 误封](https://github.com/openclaw/openclaw/issues/44134) | 2026-03-12 | OPEN | P2 | 工具 schema 频繁重载触发反滥用检测，导致账号被封。影响真实用户生产环境 |
| [#70903 文件级 provider 冷却](https://github.com/openclaw/openclaw/issues/70903) | 2026-04-24 | OPEN | **P0** | 用户充值后仍被冷却数小时，已挂 `ux-release-blocker` 但状态仍为 stale |
| [#119263 DB v14→v15 迁移失败](https://github.com/openclaw/openclaw/issues/119263) | 2026-08-04 | OPEN | **P0** | 升级即不可用，已关联 PR，需尽快合并发布 |
| [PR #91726 MCP reload endpoint](https://github.com/openclaw/openclaw/pull/91726) | 2026-06-09 | OPEN | P2 | 悬挂 2 个月，等待真实行为证明 |

---

**报告总结**：OpenClaw 今日维持高活跃度，但数据安全（媒体误删、DB 迁移失败）和消息可靠性（重复/丢失）仍是压垮用户信任的两座大山。社区对安全功能的迫切需求（记忆信任、来源标记）和代码审查质量的质疑值得维护者正视。建议优先处理两条 P0 问题（#119263、#70903），并对长期无响应的 #51429 做出正面回应。

---

## 横向生态对比

好的，这是基于您提供的多份项目日报生成的横向对比分析报告。

---

## 个人 AI 智能体开源生态横向对比分析报告 (2026-08-06)

### 1. 生态全景

当前个人 AI 助手与自主智能体开源生态正处于**高强度的功能迭代与稳定性加固并行的阶段**。主流项目均面临由**会话状态管理、消息可靠性和数据安全**引发的相似“成长烦恼”，这表明智能体从演示走向生产环境的核心挑战正在从单一模型能力转向复杂的系统工程设计。与此同时，生态正从“纯对话”向 **Agent 工作台** 演进，**WebUI 交互、多模态支持、MCP 工具扩展及云部署能力**成为吸引用户的关键差异化方向。社区对**安全与信任**（如记忆投毒、来源标记）的呼声高涨，预示着下一阶段的竞争焦点将从功能完备性转向**可信、可审计的智能体行为**。

### 2. 各项目活跃度对比

| 项目 | Issues 更新 | PRs 更新 | 版本发布 | 健康度 / 状态评估 |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 (关闭57) | 500 (合并/关闭70) | 无 | **高活跃，高积压**。P0级数据安全问题突出，社区讨论热度极高，修复跟进速度尚可。 |
| **Hermes Agent** | 50 (新开) | 50 (待合并) | 无 | **高活跃，合并阻塞**。处于密集开发期，0合并/50待合并存在高风险，Telegram功能对齐战役声势浩大。 |
| **IronClaw** | 43 | 50 (合并部分) | **v1.1.0-rc.1** | **高活跃，健康**。Bug Bash 产出丰富，功能与基础设施双线推进，但存在“AI幻觉”类新问题。 |
| **ZeroClaw** | 50 | 50 | 无 | **高活跃，评审积压**。大量 RFC 与待合并 PR，安全相关占比高，但 P1 级修复合并效率需提升。 |
| **LobsterAI** | 2 (新开) | 13 (合并12) | **2026.8.5** | **高活跃，效率极高**。PR 合并率达 92%，版本迭代稳定，但对新 Issue 响应存在延迟。 |
| **CoPaw** | 25 (关闭6) | 50 (合并21) | 无 | **中高活跃，迭代期**。处于 v2.1 高频率修复期，多个严重 Bug（如 PYTHONHOME 注入）待响应。 |
| **NanoBot** | 4 | 16 (合并8) | 无 | **中高活跃，反馈闭环快**。Issue 和 PR 响应速度良好，功能与稳定性双线推进。 |
| **NanoClaw** | 2 | 12 (合并2) | 无 | **中活跃，稳定加固期**。聚焦基础设施一致性（如DB写入规范），生态扩展（技能）持续。 |
| **PicoClaw** | 0 | 4 | 无 | **低活跃，功能积累期**。无重大用户报障，但存在构建阻断 PR 与超长待合并 PR。 |
| **NullClaw** | 0 | 2 | 无 | **低活跃，平稳维护期**。高质量 bugfix PR 等待 review，项目处于低噪音、高价值产出状态。 |
| **TinyClaw / Moltis / ZeptoClaw** | N/A | N/A | N/A | **无活动**。过去24小时处于静默状态。 |

### 3. OpenClaw 在生态中的定位

- **优势：** OpenClaw 是生态中**社区规模最大、活跃度最高**的项目（每日 500+ Issue/PR 更新），这使其成为发现问题、碰撞需求最集中的平台。社区反馈机制对 Bug 分类（如 `impact:session-state`）非常成熟，是事实上的生态“风向标”。
- **技术路线差异：** 与 NanoClaw、PicoClaw 等明确聚焦于“OpenClaw 兼容”不同，OpenClaw 本身走的是**功能全面、架构扩展性优先**的路线，其庞大的 Issue 和 PR 数量也反映了其功能的广度和复杂度。相比之下，Hermes Agent 侧重于 **Telegram 官方 API 的完整对齐**，而 IronClaw 则在 **标准化消息框架** 和 **配置即代码（Configuration-as-Code）** 上进行更深度的架构探索。
- **社区规模对比：** 尽管 Hermes Agent 等项目的活跃度也极高，但 OpenClaw 的核心参照地位无可撼动。其问题（如消息丢失、子代理状态）往往是整个生态共同面临的挑战，其他项目（如 NanoClaw、CoPaw）的更新日志中频繁出现“修复 OpenClaw 兼容性问题”即可佐证。

### 4. 共同关注的技术方向

1.  **会话状态与消息可靠性（涉及：OpenClaw, Hermes Agent, CoPaw, NullClaw）**
    - **具体诉求：** 解决消息在复杂会话（多轮工具调用、子代理、多Profile）中的丢失、重复、错乱问题。例如，OpenClaw 的子代理结果静默丢失（#44925）和 Hermes 的委派子上下文穿透（#71941）都属于此类。

2.  **记忆安全与来源信任（涉及：OpenClaw, CoPaw）**
    - **具体诉求：** 社区对“记忆投毒”攻击的担忧日益增长，强烈要求对记忆条目标注来源（用户/网页/第三方）以建立信任层级。OpenClaw 的 #7707 和 CoPaw 的技能管理 Bug 都指向了“如何让 Agent 在不可信环境中安全地学习和使用信息”这一核心议题。

3.  **MCP 生态的可靠性与健壮性（涉及：OpenClaw, NanoBot, CoPaw, IronClaw）**
    - **具体诉求：** 多个项目报告了与 MCP 工具相关的问题，包括：工具调用错误信息被错误吞没（NanoBot #5237）、MCP 工具会规律性失效（CoPaw #6732）、以及 Agent 对 MCP 服务器状态产生“幻觉”（IronClaw #7246/#7247）。这表明 MCP 的接入已从“能用”阶段进入“好用、可靠”的阶段。

4.  **WebUI 与交互体验的“工作台化”（涉及：NanoBot, CoPaw, PicoClaw, Hermes Agent）**
    - **具体诉求：** 用户不再满足于简单的聊天窗口。NanoBot 的 Quick/Temporary Chat 和共享终端、CoPaw 的 Live artifact canvas、以及 OpenClaw 对 AWS 部署指南的呼声，都表明用户期望 Agent 能成为集成开发、运维和协作的一体化工作平台。

### 5. 差异化定位分析

| 维度 | OpenClaw | Hermes Agent | IronClaw | NanoBot | CoPaw | LobsterAI |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **功能侧重** | 功能全面，社区驱动 | Telegram 深度集成与对齐 | 企业级 MCP 扩展与标准化 | WebUI 交互体验与隐私（临时会话） | 多模型回退与技能按需加载 | 桌面客户端体验与企业级功能 |
| **目标用户** | 普通开发者至高级用户 | Telegram 重度用户 | 企业用户与开发者 | 追求 UI/UX 和隐私的用户 | 中国用户（WeChat），多模型深度用户 | 桌面端用户，企业用户 |
| **技术架构** | 高复杂度事件驱动，插件众多 | 庞大单体仓库，模块化重构中 | 标准化消息框架，配置即代码 | 模块化，注重轻量级部署 | 前后端分离，强调 Tauri 桌面端 | 与 OpenClaw 生态兼容，专注桌面与 NIM 集成 |
| **关键差异** | 生态核心，词汇/标准制定者 | 特定平台的极致体验 | 从底层构建企业级标准 | 对话体验与隐私设计的创新者 | 深耕中文市场和 multi-agent 韧性 | 企业级账号体系与桌面交互的融合 |

### 6. 社区热度与成熟度

- **快速迭代期（高活跃，功能与 Bug 齐飞）：** **OpenClaw, Hermes Agent, IronClaw, ZeroClaw**。这些项目处于快速扩张阶段，社区贡献踊跃，但也因此面临大量 Bug 报告和合并积压。它们正通过大版本（如 IronClaw v1.1.0-rc.1）努力将新功能转化为稳定能力。
- **质量巩固期（中高活跃，平衡功能与稳定）：** **CoPaw, NanoBot, NanoClaw, LobsterAI**。这些项目在经历高速增长后，开始重点关注稳定性修复、架构简化和反馈闭环（如 LobsterAI 高 PR 合并率、NanoBot 的快速 Bug 修复）。
- **低活跃观察期（低活跃，蓄力或停滞）：** **PicoClaw, NullClaw, TinyClaw, Moltis, ZeptoClaw**。这些项目可能处于维护模式，或正在积累下一次功能发布的能量。它们通常体量较小，但社区氛围可能更专注。

### 7. 值得关注的趋势信号

1.  **“AI 幻觉”已从对话内容蔓延至系统状态认知：** 多个项目（IronClaw、NanoBot）报告 Agent 会虚构“连接已建立”、“任务运行中”或误判“工具调用成功”等系统状态。这将成为智能体可靠性面临的**新前沿挑战**，需要 Agent 自身具备更强的“工具调用结果验证”和“状态确认”机制。
2.  **安全与信任成为功能开发的“一等公民”：** 从记忆来源标记（OpenClaw #7707）、Shell 命令策略分层（ZeroClaw #7155）到敏感文件保护（ZeroClaw #9776），安全不再只是修补漏洞，而是被前置于架构设计之中。这标志着一个**成熟生态的诞生**。
3.  **多模态与附件处理成为基础能力：** 多个项目（NanoClaw #2528, IronClaw #6257, CoPaw #6696）都在解决图片、PDF、音频等附件在跨渠道传递和处理中的问题。这表明“理解用户发送的任何文件”正在从高级功能变为**用户对 AI 助手的基础预期**。
4.  **可观测性和诊断工具需求激增：** 面对复杂的会话状态和工具调用，开发者和用户都迫切希望看到 Agent 的“思考过程”和“执行日志”。OpenClaw 的 `openclaw doctor`、NanoBot 的 `nanobot api status` 以及多个项目对 Usage 统计的改进，都印证了对**透明度**的空前需求。

---

**结论：** 个人 AI 智能体生态正经历“从野蛮生长到精耕细作”的转型。头部项目在快速构建庞大功能版图的同时，正被复杂性问题反噬；而腰部项目则通过聚焦特定场景（如 Telegram、WebUI）或强调稳定性（高合并率）来寻找差异化破局点。对于技术决策者而言，选择哪个平台不仅要看功能广度，更要评估其社区治理能力、Bug 响应速度和架构的长期演进方向。未来的赢家将是那些能**驾驭复杂性并提供可信、可靠、可解释的智能体行为**的项目。

---

## 同赛道项目详细报告

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot 项目动态日报

**日期：** 2026-08-06  
**数据窗口：** 过去 24 小时（截至 2026-08-05）

---

## 1. 今日速览

NanoBot 项目在过去 24 小时内保持中高活跃度：共 4 条 Issue 更新（全部为新增/活跃，暂无关闭）和 16 条 PR 更新（8 条待合并、8 条已合并/关闭），无新版本发布。值得关注的是，PR 密集区集中在 WebUI 交互体验、内存/会话管理、以及频道集成（Matrix、WhatsApp、Mattermost）三个方向，且今日关闭的 PR 中有两条 P1 优先级的修复（会话访问授权回归、MST 新搜索 Provider 集成），显示项目在稳定性加固和功能扩张双线推进。Issue 方面有一个较早报告（7月28日创建）的 WhatsApp 音频发送 Bug 仍在持续讨论，另有两条新报 Bug（MCP 错误信封处理、/goal 循环回复）均已有对应修复 PR 在途，反馈闭环速度良好。

---

## 2. 版本发布

**无新版本发布。** 当前无 Release 动态，可关注后续合并批次。

---

## 3. 项目进展

今日有 **8 条 PR 被合并/关闭**，以下是值得关注的重要合并：

### 🎯 高优先级合并（P1）

| PR | 标题 | 影响 |
|---|---|---|
| [#5234](https://github.com/HKUDS/nanobot/pull/5234) | feat(agent): integrate mst-python as a metasearch provider | **新功能落地**：引入 Meta-Search Tool（MST）作为新的 Web 搜索 Provider，聚合 DuckDuckGo、Google、Brave、Bing 等多引擎结果并使用 RRF 融合，显著提升搜索覆盖率。 |
| [#5238](https://github.com/HKUDS/nanobot/pull/5238) | refactor(session): remove request-scoped access grants | **架构简化与 Bug 修复**：移除 #5211 引入的请求级 `Tool.available()` 权限层，删除 `SessionAccessScope` 授权抽象，会话工具可搜索/读取当前用户所有持久化会话。简化权限模型、消除潜在授权不一致问题。 |

### 📦 中优先级合并（P2）

| PR | 标题 | 影响 |
|---|---|---|
| [#5203](https://github.com/HKUDS/nanobot/pull/5203) | fix(whatsapp): detect outbound media content before dispatch | **Bug 修复**：WhatsApp 外发媒体不再仅依赖文件扩展名判断类型，改为内容识别（libmagic），支持 M4A/AAC 等格式 alias，不支持的音频格式自动作为文档发送。 |
| [#5233](https://github.com/HKUDS/nanobot/pull/5233) | feat(mattermost): separate group policy for threads and expose in WebUI | **功能增强**：新增 `groupPolicyInThread` 配置，允许话题和主频道设置不同 @ 提及要求，并在 WebUI 中暴露配置入口。 |
| [#5249](https://github.com/HKUDS/nanobot/pull/5249) | refactor(webui): improve visual consistency | **UI 一致性重构**：统一菜单/弹窗/对话框表面层级，压平 Skills 和 Channels 布局，移除持久化消息的重复动画，自动检测时区。 |
| [#5250](https://github.com/HKUDS/nanobot/pull/5250) | fix(webui): feather clipped activity edges | **UI 修复**：为裁剪的 Agent 活动面板添加方向感知的渐变羽化效果，自动跟踪底部时保持最新行清晰可见。 |
| [#5254](https://github.com/HKUDS/nanobot/pull/5254) | feat: add provider-native request switches | **功能增强**：WebUI 新增 Provider 原生请求开关——OpenAI Codex Fast 模式、OpenAI/DeepSeek 联网搜索、xAI Grok X Search，直接修改 `extraBody` 字段。 |
| [#5184](https://github.com/HKUDS/nanobot/pull/5184) | feat(webui): add Quick Chat and Temporary Chat | **功能合并**：Quick Chat（固定会话身份、不入话题列表）和 Temporary Chat（连接级、内存历史、可选受限工作区）双模式落地，被标记为 conflict 后关闭，将由 #5252 等后续 PR 承接。 |

> **整体评价：** 项目在 WebUI 交互层（Quick Chat / Temporary Chat）、Provider 扩展（MST）、以及稳定性修复（Session 权限简化）三个方向均有实质推进。特别是 #5238 的权限模型简化，降低了长期维护成本，是架构层面的一次正确收敛。

---

## 4. 社区热点

### 🔥 最热 Issue：[#5149](https://github.com/HKUDS/nanobot/pull/5149) — WhatsApp 音频发送 Bug（评论 4 条）

- **作者：** mxnbf | 创建 7月28日 | 最后更新 8月5日
- **核心问题：** NanoBot 无法通过 WhatsApp 发送音频消息（接收正常）。日志显示 ffmpeg 处理警告（`[neonize.utils.ffmpeg WARNING]`），疑似媒体类型识别或编码环节异常。
- **热度分析：** 该 Issue 持续一周未关闭，但关联 PR [#5203](https://github.com/HKUDS/nanobot/pull/5203) 已于今日合并（内容识别替代扩展名判断），预计该 Issue 即将被验证关闭。社区关注点在于**媒体文件类型判断的准确性**——不止音频，可能是所有外发媒体的通用问题。

### 🔥 最热 PR（按潜在影响）：[#5234](https://github.com/HKUDS/nanobot/pull/5234) — 合并的 MST 搜索 Provider

- 虽非讨论最热，但其作为新 Provider 的合入，是社区对**搜索能力增强**长期诉求的回应，且今日正式落地。

> **社区诉求总结：** 近期讨论集中在**多引擎搜索聚合**、**WebUI 交互细节**（Quick/Temp Chat、视觉一致性）、以及**频道适配的边角问题**（Matrix 空 body、WhatsApp 媒体类型）。社区对 UI/UX 打磨和 Provider 扩展的期待明显高于新增频道集成。

---

## 5. Bug 与稳定性

按严重程度排列：

| 严重度 | Issue/PR | 描述 | Fix PR 状态 |
|---|---|---|---|
| **P1** | [#5237](https://github.com/HKUDS/nanobot/issues/5237) | **MCP 错误信封被吞**：MCP Server 返回业务错误（`isError=false` 但内容为 `{"code": 404, "msg": "data not exist"}`）时，Agent 将其视为成功调用，LLM 无法得知失败而陷入等待直至 tool_timeout | ⚠️ 暂无 fix PR，需设计层解决 |
| **P1** | [#5256](https://github.com/HKUDS/nanobot/issues/5256) | **/goal 循环回复**：单个 /goal 消息产生数十条近乎相同的回复，原因是持续目标模式绕过 `_MAX_INJECTION_CYCLES` 上限，模型在等待用户时反复注入"继续工作"提示 | ✅ 已有 fix PR：[#5257](https://github.com/HKUDS/nanobot/pull/5257)（为持续目标增加空闲时延续上限，P2 待合） |
| **P2** | [#5149](https://github.com/HKUDS/nanobot/issues/5149) | **WhatsApp 音频无法发送**：接收正常但发送失败 | ✅ 已修复：[#5203](https://github.com/HKUDS/nanobot/pull/5203) 今日合并（内容识别替代扩展名） |
| **P2** | — | 已合并的权限模型修复（[#5238](https://github.com/HKUDS/nanobot/pull/5238)）：移除 #5211 引入的请求级 Tool 权限层，消除潜在授权不一致 | ✅ 已合并 |

> **风险提示：** MCP 错误信封问题（#5237）目前无对应修复 PR，且涉及 Agent 对工具调用的**正确性判断**，属于设计层面缺陷（`isError` 语义过于简单），建议维护者尽快给出方案，避免 MCP 生态用户踩坑。

---

## 6. 功能请求与路线图信号

### 新功能请求（今日新增）

| Issue/PR | 功能 | 信号强度 |
|---|---|---|
| [#5251](https://github.com/HKUDS/nanobot/issues/5251) | **WebUI 支持 MCP Apps 宿主**（`io.modelcontextprotocol/ui`），让 MCP Server 可在 WebUI 内嵌交互界面（表单、按钮等） | 🟡 中——基于已有 MCP client 能力的自然扩展，但涉及 WebUI 框架较大改动 |
| [#5259](https://github.com/HKUDS/nanobot/pull/5259) | **Memory-only 临时会话**：#5252 的叠加 PR，明确临时聊天状态仅在进程内存中，不写入会话历史/WebUI 转写/自动记忆 | 🟢 高——临时会话的隐私边界明确化，企业用户关注 |
| [#5253](https://github.com/HKUDS/nanobot/pull/5253) | **共享项目终端**：WebUI 与 Agent 共享一个项目级 PTY（基于 xterm.js），支持回放/重连/重启 | 🟢 高——Agent 交互式操作场景的重要增强 |
| [#5255](https://github.com/HKUDS/nanobot/pull/5255) | **真实 API 服务状态**：WebUI 区分"Gateway 未启动"和"外部 `nanobot serve` 在跑"，新增 `nanobot api status` 命令 | 🟡 中——运维友好性改进 |

### 路线图信号判断

- **Temporary Chat 系列**（#5184 → #5252 → #5259）已形成清晰的**三个连续 PR** 依赖链，且今日 #5184 关闭、#5252/#5259 在途，说明该功能将于**下一版本落地**，且包含"受限工作区访问+内存级状态"的隐私设计。
- **MCP Apps（#5251）** 目前仅停留在 Issue 层面，无关联 PR。若 MCP 生态继续升温，此项可能在下季度进入规划。
- **共享项目终端（#5253）** 和 **Provider 原生开关（#5254 已合并）** 表明项目正从"纯对话"向 **Agent 工作台** 方向演进。

---

## 7. 用户反馈摘要

### 真实痛点

1. **WhatsApp 媒体类型误判**（#5149）：用户期望"发送音频文件"能得到正确投递，实际因扩展名判断缺陷而失败。**使用场景：** 通过 WhatsApp 与 NanoBot 交换语音备忘录。修复方向（内容识别）获得用户认可。
2. **MCP 错误被静默吞掉**（#5237）：用户描述"LLM 永远不知道调用失败了"，导致 Agent 在错误路径上反复重试直至超时。**痛点核心：** 工具调用的可观测性不足，`isError` 单一布尔值无法表达业务级错误。
3. **/goal 模式的循环轰炸**（#5256）：用户收到"数十条重复回复"，只能手动干预或等模型自我识别为循环后取消。**痛点核心：** 持续目标模式下缺少空闲检测与回复节流。

### 满意/积极反馈信号

- 今日 8 条 PR 被合并，无明显 revert 或后续冲突报告，说明代码质量与测试覆盖稳定。
- #5238（权限模型简化）和 #5234（MST Provider）均为较大功能/重构，合并后社区未见负面反馈。

---

## 8. 待处理积压

### 🟥 需维护者重点关注

| 项目 | 说明 |
|---|---|
| [#5237](https://github.com/HKUDS/nanobot/issues/5237) | **P1 MCP 错误信封问题，无 fix PR**。已存在 2 天，涉及 Agent 工具调用正确性，是 MCP 用户的基础设施级 Bug，建议尽快排期。 |
| [#5149](https://github.com/HKUDS/nanobot/issues/5149) | 虽然 #5203 已合并，但 Issue 尚未关闭。建议维护者主动验证并关闭，避免 stale issue 积累。 |

### 🟨 长期未响应观察

| 项目 | 说明 |
|---|---|
| — | 当前无超过 2 周未响应的 Issue 或 PR，项目维护响应速度整体良好。 |

---

**报告生成时间：** 2026-08-06 00:00 UTC  
**数据覆盖窗口：** 2026-08-05 00:00 UTC — 2026-08-05 23:59 UTC  
**数据来源：** [HKUDS/nanobot](https://github.com/HKUDS/nanobot) GitHub 仓库

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent 项目动态日报 — 2026-08-06

## 1. 今日速览

过去 24 小时项目活跃度极高：50 条新开 Issues 与 50 条待合并 PR 全部处于活跃状态，无关闭/合并记录，说明团队当前处于密集开发与提交阶段。高频更新集中在三个方向：**repo 级 god-file 分解重构**（史诗级任务 #78647 驱动，今日新增多个 PR 切片）、**Telegram 平台功能补齐战役**（Bot API 10.2 对齐、30+ 个相关 issue），以及**会话状态持久化与稳定性修复**（多个 P2 级别 bug 的 fix PR 已提交待合并）。值得注意的是本日 PR 合并数为 0，存在合并积压风险，但 PR 持续迭代更新（多数 PR 今日有 push），表明代码审查与修订正在推进。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日虽无 PR 合并，但多项关键 PR 持续收到更新，显示功能开发与修复正在积极迭代。以下为今日活跃推进的重要改动：

### 架构重构（god-file 分解战役推进中）

- **[#79127] refactor(web): extract custom-endpoints routes into web_routers/custom_endpoints** — `web_server.py` 的 R3-C1 切片，13 个自定义端点从巨型文件迁移至独立 APIRouter，纳入 epic #78647 的 repo 级分解。作者：andrexibiza
- **[#79708] refactor(cli): extract status-bar/skill-command mixins from cli.py (shard s2)** — CLI 提取第二波，字节级保真、零行为变更。作者：andrexibiza
- **[#79800] refactor(slack): extract messaging family into SlackMessagingMixin (adapter.py god-file slice R2)** — Slack 适配器消息族提取至独立 mixin。作者：andrexibiza

### 功能新增与增强

- **[#79811] fix(persistence): persist provider in model_config on model switch** — 修复模型切换时 provider 丢失问题，确保会话恢复时正确重建设备路由。作者：RelaxJonh
- **[#79808] feat(cron): enforce required skills via cron.required_skills** — cron 任务新增必需技能校验，防止任务输出依赖缺失技能。作者：apoapostolov
- **[#78356] feat(plugins/memory-tencentdb): upgrade to v2.0.0 + fix(auxiliary): Aliyun MaaS /compatible-mode/v1** — 腾讯云记忆插件升级至 v2.0.0，同步修复阿里云 MaaS 兼容模式。作者：linwenxiang725-ship-it

### 跨平台修复

- **[#79810] fix(ui-tui,desktop): make terminal-setup and Intl tests pass on Windows** — 修复 Windows 上 TUI 测试路径分隔符假设和桌面端 Intl 硬编码 en-US 的问题。作者：mrmixx-max
- **[#79805] fix(desktop): recover attach and /compress after stale session drop** — 睡眠唤醒或后端重启后会话恢复机制补充。作者：xxxigm

### 基础设施与安全

- **[#79809] fix: patch desktop and TUI dependency advisories** — Electron 升至 41.10.3、brace-expansion 至 5.0.9、undici 至 6.28.0，修复已知安全通告。作者：MohsinHashmi-DataInn

---

## 4. 社区热点

### 🔥 Telegram 功能对齐战役引发广泛关注

今日评论热度最高的议题集中于和rexibiza 发起的 **Telegram Feature Parity & Alignment Campaign (Bot API 10.2)** 系列，30+ 个 issue 组成的大规模元任务（meta-issue #78791）。该战役参照 Bot API 10.2 官方文档，逐一盘点 Hermes Telegram 插件未覆盖的 API 面，涉及：支付与 Stars（#78775）、礼物系统（#78776）、游戏 API（#78777）、Web Apps（#78778）、Passport（#78779）、内联键盘变体（#78781）、命令范围（#78782）、机器人身份（#78783）、托管机器人（#78785）、商务账号（#78786）等。

**背后诉求**：开发者期望 Hermes 的 Telegram 插件达到与官方 Bot API 完整对齐的水平，消除 "文档有但 Hermes 不支持" 的功能缺口。值得注意的是大量 issue 被标记为 `duplicate` 或 `needs-decision`，说明该战役的组织方式仍在磨合中。

### 热议 Issue TOP 3

1. **[#78647] Epic: Shard all 20 god files — repo-wide god-file decomposition**（14 评论）— 仓库级巨型文件分解史诗任务，定义了 "所有 god file 必须分解、不可回退" 的仓库政策，是当前重构浪潮的总纲领。
2. **[#77780] lifecycle_guard crashes on `ValueError: embedded null byte`**（12 评论）— 网关生命周期守卫解析 heredoc/`-c` 载荷时因空字节崩溃，直接影响所有终端命令。P2 严重级别。
3. **[#54962] Extract Gateway Platform Routing from gateway/run.py**（11 评论）— `gateway/run.py` 858KB 巨型文件，社区持续呼吁拆分事件循环与负载解析逻辑。

### 热门 PR

- **[#75352] fix(state): safely reclaim finished-thread WAL readers**（今日有更新）— 长生命周期 SessionDB 累积 WAL 文件描述符问题，多个 sweeper 标签（risk-session-state/compatibility/blast-broad）表明影响面广。
- **[#73363] fix(cron): deliver each profile's cron via its own adapter in multiplex**（今日有更新）— 多 profile 模式下 cron 输出错误路由至 default 适配器的问题，修复二级 profile 定时任务投递。

---

## 5. Bug 与稳定性

### P2 级别（高优先级）

| Issue/PR | 描述 | 状态 |
|---|---|---|
| [#77780] Bug: lifecycle_guard 崩溃 (`ValueError: embedded null byte`) | 网关生命周期守卫处理 heredoc/`-c` 载荷时崩溃，**影响所有终端命令执行** | 仍开放，无关联 fix PR |
| [#71941] Bug: 委派子上下文穿透共享终端快照 | `HERMES_DELEGATED_CHILD_CONTEXT` 预期只对委派子进程可见，但缓存共享导致后续普通调用也看到该上下文，**存在会话状态污染风险** | 仍开放，sweeper: risk-session-state |
| [#75352] PR: 安全回收已结束线程的 WAL readers | 长期运行的 SessionDB 对每个接触过读路径的线程保留强引用 WAL reader，**文件描述符持续累积** | PR 已提交待合并（P2, needs-decision） |
| [#79717] PR: 修复 fresh-tail 上下文溢出重试循环 | 压缩反复运行但无法将受保护消息缩小至 provider 窗口内，导致无限重试 | PR 已提交待合并（P2, 对应 #64382） |
| [#69242] PR: Discord 原生斜杠命令正确路由至 profile_routes | multiplex_profiles 模式下 `/profile` 和 `/model` 错误回退至 default | PR 已提交待合并（P2, 修复 #69178） |
| [#73608] PR: 桌面端从 $sessionStates 读取会话消息 | refresh/regenerate/restore-checkpoint 在活动 runtime ID 下静默失败，根因是读取了过期的全局 $messages | PR 已提交待合并（P2, 修复 #68734） |
| [#73093] PR: MiniMax 工具 schema 清洗 | MiniMax M3 拒绝标准 JSON Schema 构造（`boolean`、`default`、`anyOf`/`null`），触发 HTTP 400 | PR 已提交待合并（P2） |

### P3 级别

- **[#79801] PR: LSP 陈旧客户端清理** — `_get_or_spawn` 中陈旧客户端未移除导致重复进程，已提交 fix
- **[#79220] Bug: 成本标签 2dp 导致 $0.00 显示** — 低于 $1/Mtok 的模型单次调用成本显示为 $0.00（显示 bug 非计算 bug），无 fix PR
- **[#78130] PR: 作用域凭据锁冲突归属到持有 profile** — 多 profile 下无法定位锁冲突来源，影响运维效率
- **[#79809] PR: 依赖安全通告修复** — Electron/brace-expansion/undici 升级
- **[#79694] PR: Telegram 文本附件 UTF-8 BOM 规范化** — 西里尔字母文本附件被错误识别编码
- **[#79799] PR: Slack 自由响应频道消息确认** — 消息被处理但缺少 ack 确认

### 需要关注的稳定性风险

- **会话状态（session-state）类问题今日高度集中**：至少 6 个 issue/PR 携带 `sweeper:risk-session-state` 标签，涵盖委派上下文穿透（#71941）、WAL reader 累积（#75352）、桌面消息读取陈旧数据（#73608）、压缩循环（#79717）、cron profile 路由（#73363）等。建议维护团队对 session-state 链路做专项审查。
- **合并积压**：50 个 PR 待合并且今日无合并记录，其中包括多个 P2 级别的修复，若长期积压可能导致修复冲突或重复工作。

---

## 6. 功能请求与路线图信号

### 强烈路线图信号：Telegram 全面对齐

Bot API 10.2 对齐战役（#78791 元任务 + 30 余子任务）作为系统性功能补齐行动，大概率会进入近期版本规划。当前已有多项相关 PR 提交（如 #79694 Telegram 文本附件修复），说明战役已从 issue 收集进入实施阶段。重点功能方向：

- **支付与商业化**：sendInvoice/Telegram Stars 对账/礼物系统（#78775, #78776, #78689）— 带有 `area/billing` 标签，表明商业化路线已有规划
- **内联模式与 Web Apps**：answerInlineQuery/WebApp 按钮/预准备消息（#78774, #78778）
- **指令与身份管理**：setMyCommands 全 scope/机器人身份/菜单按钮（#78782, #78783, #78789, #78790）
- **键盘与交互**：回复键盘/内联按钮变体（#78780, #78781）
- **新 API 面**：托管机器人（#78785）、商务账号（#78786）、Passport（#78779）、游戏（#78777）

### 其他值得关注的功能信号

- **cron.required_skills 强制校验**（PR #79808）：cron 任务创建时强制校验依赖技能存在，表明框架对任务输出质量的管控意识增强
- **memory-tencentdb v2.0.0**（PR #78356）：腾讯云记忆插件大版本升级，MemoryCore v2 功能入驻，同时修复阿里云 MaaS 兼容模式，多云记忆存储支持在推进
- **桌面端体验持续修复**：新会话归属 Home 项目（#77857）、会话恢复（#79805）、Windows 测试修复（#79810），桌面端稳定性和用户体验是持续关注点

### 可能进入下一版本的功能预判

结合已有 PR 与 issue 讨论热度，以下功能大概率进入下个版本范围：

| 功能 | 来源 | 判断依据 |
|---|---|---|
| Telegram 内联模式 + Web Apps | #78774/#78778 | 战役核心项，与在线电商/工具场景强关联 |
| 会话 provider 持久化 | PR #79811 | 已提交修复，直接改进模型路由体验 |
| LSP 陈旧客户端清理 | PR #79801 | 已提交修复，影响开发体验 |
| WAL reader 回收 | PR #75352 | P2 且已提交，长期运行的稳定性关键 |

---

## 7. 用户反馈摘要

### 常见痛点

1. **Telegram 功能覆盖不全**：用户在 #78773-#78791 系列评论中反复指出的核心痛点是 Hermes 的 Telegram 插件与官方 Bot API 存在明显差距，尤其是缺少支付、内联模式、Web Apps 等常用能力，导致部分场景无法落地。和rexibiza 在多个 issue 中强调 "文档锚点已列，Hermes 零命中"。

2. **多 profile 路由混乱**：#73363 和 #69242 反映的共性是 multiplex_profiles 模式下各 profile 的执行与投递链路不一致——cron 输出走 default 适配器、Discord 斜杠命令回退 default、凭据锁冲突无法定位——多租户场景下路由可预期性不足。

3. **会话状态不易预测**：#71941（委派上下文穿透）、#73608（桌面读取过期消息）表明会话状态在缓存共享、全局/局部状态混用场景下容易出现不可预期的行为。

4. **Windows 与国际化支持不完善**：#79810 发现 TUI 测试硬编码 POSIX 路径分隔符、桌面端 Intl 硬编码 en-US，#79694 反映 Telegram 发送 Cyrillic 附件存在编码问题——非 POSIX/非英语用户受影响。

### 使用场景洞察

- **多 profile 部署**：社区有相当数量的用户将 Hermes 部署为多 profile（多租户/多机器人）架构，他们对 profile 隔离性、路由正确性要求极高，相关问题响应积极
- **Telegram 作为主要交互界面**：大量 issue 围绕 Telegram 提出，暗示 Telegram 插件是 Hermes 用户主力使用的前端之一
- **低频成本模型用户**：#79220 反映采用低价位模型的用户对成本显示精度有感知需求

### 明确的正面反馈

- github #79811 的 PR 描述中用户主动补充了测试步骤，反馈链路完整
- #77857（新会话归 Home）修复方式获得用户好评："new conversation now lands in the Home bucket" 是社区期待的修正行为

---

## 8. 待处理积压

### 高优先级积压（建议维护者优先关注）

| 项目 | 类型 | 标签 | 备注 |
|---|---|---|---|
| [#77780] lifecycle_guard 空字节崩溃 | Bug (P2) | comp/tools, comp/cron | **影响所有终端命令**，社区 12 条评论，尚无 fix PR 关联，建议尽快定位 |
| [#71941] 委派子上下文穿透共享终端 | Bug (P2) | sweeper: risk-session-state | 会话状态污染风险，评论提出复现路径，等待响应 |
| [#54962] gateway/run.py 858KB 分解 | 重构 (P3) | comp/gateway | 社区持续呼吁（11 评论），与 epic #78647 对齐后应纳入计划 |
| [#75352] WAL readers 回收 | PR (P2) | needs-decision | 已提交 7 天+，多个 sweeper 标签，需要核心维护者决策 |

### 长期未响应的功能请求

| 项目 | 类型 | 标签 | 备注 |
|---|---|---|---|
| [#78689] Telegram 付费广播支持 | 功能 (P3) | area/billing | 商业功能需求，战役中标为 duplicate，需合并决策 |
| [#78773] DirectMessagesTopic 解析 | 功能 (P3) | sweeper: risk-session-state | 战役子任务，与 session-state 风险关联 |
| [#78788] 未知/空数据 callback query 响应 | 功能修复 (P3) | sweeper: risk-message-delivery | 用户可见的客户端 spinner 永不消失问题 |

### 合并积压风险

0 合并/50 待合并的比例处于不健康区间。当前待合并 PR 中包含多个 P2 级别修复（#75352、#73363、#69242、#73608、#73093、#79717），建议维护者尽快安排审查合并周期，避免：
- 修复之间产生冲突
- 功能分支长时间偏离 main 导致集成困难
- 社区贡献者等待周期过长影响参与积极性

---

*本日报基于 Hermes Agent GitHub 仓库 2026-08-06 公开数据生成，数据来源：NousResearch/hermes-agent Issues & PRs。所有链接指向原始 GitHub 页面。*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw 项目动态日报

**日期：2026-08-06**  
**数据来源：github.com/sipeed/picoclaw**


## 1. 今日速览

今日 PicoClaw 项目整体活跃度偏低，24 小时内无新 Issue 报告、无新版本发布，Issue 侧处于静默状态。PR 侧更新相对活跃，共 4 条动态，其中 1 条已关闭（#926），3 条处于开放待合并状态（#3318、#3200、#1951）。需特别注意的是，今日关闭的 #926 为一项 **Antihropic OAuth 登录功能增强 PR**，因已并入其他 PR 而关闭，并不代表废弃；三项待合并 PR 分别涉及前端锁文件修复、模型兜底链配置和安装脚本迁移，均指向工程质量改进与功能完善。综合来看，项目当前处于 **功能整合与稳定性优化阶段**，社区反馈渠道畅通但暂无重大用户报障。

> 活跃度评级：★★☆☆☆（低活跃，PR 侧有持续维护动作）


## 2. 版本发布

**无新版本发布。** 上一个版本信息请参见仓库 Releases 页面。当前多项 PR 待合并，预计下一个版本发布时将会集中纳入。


## 3. 项目进展

今日共有 1 条 PR 关闭、3 条 PR 处于开放待合并状态，各项进展如下：

### 🔒 已关闭（并入其他 PR）

**[PR #926] feat(auth): add Anthropic OAuth setup-token login** — `[CLOSED, type: enhancement, domain: provider]`  
作者：BallerIsLeet | 创建 2026-02-28 | 关闭于 2026-08-05  
🔗 https://github.com/sipeed/picoclaw/pull/926

该 PR 实现了 **Anthropic OAuth setup token 登录支持**，包括 `--setup-token` 命令行标志、交互式登录菜单、使用量（5 小时/7 天）展示以及 OAuth token 流式传输支持。PR 状态为已关闭，建议维护者确认其变更是否已完整并入其他分支，避免功能丢失。

### 📌 待合并（3 条）

| PR | 主题 | 创建时间 | 状态 |
|----|------|----------|------|
| [#3318](https://github.com/sipeed/picoclaw/pull/3318) | fix(web): repair unparseable pnpm-lock.yaml | 2026-08-05 | OPEN |
| [#3200](https://github.com/sipeed/picoclaw/pull/3200) | feat(models): add configurable default fallback chain | 2026-07-01 | OPEN |
| [#1951](https://github.com/sipeed/picoclaw/pull/1951) | chore: move installation scripts from docs repo to here | 2026-03-24 | OPEN |

**项目整体向前迈进的步调**：三项待合并 PR 分别在**构建稳定性**（#3318）、**模型路由灵活性**（#3200）和**安装体验优化**（#1951）三个维度做出改进。其中 #3200 的 fallback chain 功能已持续开放超过一个月，建议维护者尽快安排 review，该功能对生产环境的多模型容灾具有重要意义。


## 4. 社区热点

今日社区讨论热度整体偏低，无评论密集的 Issue 或 PR。相对值得关注的 PR 为：

**PR #926（Antihropic OAuth 登录）** — 虽已关闭，但作为今日唯一关闭的 PR，且涉及**认证方式扩展**这一重要功能方向，值得社区关注其后续合并情况。该 PR 从 2026-02 月持续至 08 月，历经约 5 个月，反映了社区对**替代 API Key 的认证方式**存在持续需求。

🔗 https://github.com/sipeed/picoclaw/pull/926

**背后的诉求分析**：API Key 的管理和轮换一直是 AI 工具使用的痛点，OAuth setup-token 模式可显著改善这一体验。若该功能确认被纳入主线，预计将获得较大范围的社区好评。


## 5. Bug 与稳定性

今日无新增 Bug 报告，但存在一条已提交的构建稳定性修复 PR：

**[PR #3318] fix(web): repair unparseable pnpm-lock.yaml** — `[OPEN]`  
作者：nuestraai | 创建 2026-08-05  
🔗 https://github.com/sipeed/picoclaw/pull/3318

- **严重程度**：🔴 高（构建阻断）
- **问题描述**：`web/frontend/pnpm-lock.yaml` 中 `semver@7.8.5` 被重复列出（一次在 `packages:` 下，一次在 `snapshots:` 下），违反 YAML 规范导致 pnpm 拒绝解析锁文件，错误信息：`ERR_PNPM_BROKEN_LOCKFILE: duplicated mapping key (3577:3)`。
- **影响范围**：Web 前端依赖安装/构建流程，影响所有依赖 pnpm 安装的开发者和 CI 流水线。
- **修复状态**：已有修复 PR 待合并，但尚未获得维护者 review。

> ⚠️ **建议**：该 PR 虽小但直接阻断前端构建，建议维护者优先处理。


## 6. 功能请求与路线图信号

当前无新功能请求 Issue，但以下开放 PR 暗示了明确的路线图方向：

### 🔮 值得关注的路线图信号

| PR | 功能方向 | 开放时长 | 信号强度 |
|----|----------|----------|----------|
| [#3200](https://github.com/sipeed/picoclaw/pull/3200) | **可配置默认 Fallback 链**（支持设置默认模型、添加备用模型、排序、持久化） | 36 天 | ⭐⭐⭐ 高 |
| [#926](https://github.com/sipeed/picoclaw/pull/926) | **Antihropic OAuth 登录**（替代 API Key） | 约 5 个月 | ⭐⭐⭐ 高 |
| [#1951](https://github.com/sipeed/picoclaw/pull/1951) | **安装脚本迁移至主仓库** | 约 4.5 个月 | ⭐⭐ 中 |

**判断**：#3200 的 fallback chain 功能与当前 AI 工具多模型调用的主流实践高度契合。随着模型供应商增多、稳定性要求提高，**模型自动降级与容灾**正成为刚需。参考同领域项目（如 OpenRouter、LiteLLM 等）的路线图节奏，预计 #3200 和 #926 很可能被纳入下一版本（v0.x 或 v1.x），建议维护者给出明确的时间表。


## 7. 用户反馈摘要

今日无新增 Issue 评论，以下反馈来自近期 PR 描述中的隐含信号：

| 来源 | 用户诉求 | 场景 |
|------|----------|------|
| PR #926 | 希望在 Anthropic 服务中使用 **OAuth setup token** 而非传统 API Key，并可在 `auth status` 中直接查看 5 小时/7 天用量 | 企业/重度用户，关注成本管控与密钥安全 |
| PR #3200 | 希望在 Web UI 中 **可视化配置模型的默认调用链与兜底顺序**，通过后端 API 持久化保存 | 多模型接入的用户，需要灵活的容灾策略 |
| PR #1951 | 希望将安装脚本从 docs 仓库迁移至主仓库，**简化安装入口**，避免跨仓库跳转 | 新用户首次部署体验 |

**共性痛点**：用户在**认证便捷性**和**模型调用可靠性**两个方向上有明确诉求，且都希望**通过 UI/CLI 而非手动编辑配置文件**来完成操作。目前暂无明确的不满情绪反馈。


## 8. 待处理积压

以下 PR 长期未获得维护者响应或合并，建议重点关注：

### 🕐 超长待合并 PR

| PR | 主题 | 开放时长 | 最后活动 | 优先级建议 |
|----|------|----------|----------|------------|
| [#1951](https://github.com/sipeed/picoclaw/pull/1951) | chore: move installation scripts from docs repo to here | **约 4.5 个月**（2026-03-24） | 2026-08-05（有更新） | ⭐ 中 |
| [#3200](https://github.com/sipeed/picoclaw/pull/3200) | feat(models): add configurable default fallback chain | **约 36 天**（2026-07-01） | 2026-08-05（有更新） | ⭐⭐⭐ 高 |
| [#3318](https://github.com/sipeed/picoclaw/pull/3318) | fix(web): repair unparseable pnpm-lock.yaml | **1 天**（2026-08-05） | 2026-08-05 | ⭐⭐⭐ 高（构建阻断） |

### 📋 维护建议

1. **立即处理**：[#3318](https://github.com/sipeed/picoclaw/pull/3318) 为构建阻断级修复，建议 24 小时内 review 并合并。
2. **本周内安排**：[#3200](https://github.com/sipeed/picoclaw/pull/3200) 功能价值高且已开放超一个月，建议安排 reviewer 进行代码审查。
3. **本月内解决**：[#1951](https://github.com/sipeed/picoclaw/pull/1951) 涉及安装体验改进，建议明确是否接纳，避免长期悬置导致社区 contributor 流失。
4. **确认需求**：[#926](https://github.com/sipeed/picoclaw/pull/926) 虽已关闭，建议确认其变更是否已并入其他分支，并存档关闭原因（如 "superseded by #xxxx"），方便社区追溯。


## 项目健康度评估

| 维度 | 状态 | 说明 |
|------|------|------|
| Issue 响应 | 🟢 良好 | 无新增待响应 Issue，存量已处理 |
| PR 合并效率 | 🟡 中等 | 1 条关闭（并入他处），3 条待合并，最长等待 4.5 个月 |
| 构建稳定性 | 🔴 存在风险 | pnpm-lock.yaml 损坏，已有修复但未合并 |
| 版本迭代节奏 | 🟡 偏慢 | 当前无新版本发布，多项功能待集中释放 |
| 社区活跃度 | 🟡 偏低 | 24h 无新 Issue，PR 侧有维持性更新 |

**整体评价**：项目处于**功能积累期**，当前无重大用户报障，但需警惕**PR 积压时间过长**可能导致的外部贡献者流失风险。建议维护者加速 #3318 和 #3200 的合并节奏，以维持社区贡献动力。


*本日报由 AI 自动生成，数据截至 2026-08-06。所有链接均指向 GitHub 原始内容。*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw 项目动态日报 — 2026-08-06

## 今日速览

NanoClaw 项目今日活跃度**较高**，核心聚焦于**稳定性修复与基础设施一致性**。过去24小时内有 2 条活跃 Issue（均涉及安装与文件访问问题）和 12 条 PR 更新，其中 2 条 PR 已合并/关闭，10 条待合并。值得关注的是，核心团队成员（Joi、glifocat、apelosi）提交了多条针对**数据库写入规范**、**容器环境变量传递**和**通道启动超时**的关键修复，表明项目正处于**主动加固既有功能**的阶段。此外，社区贡献者贡献了多个技能类 PR（Tavily MCP、add-why、Dial 集成），体现了生态扩展的持续活力。

---

## 项目进展

今日**合并/关闭**的 2 条 PR 展示了项目在任务执行层面的重要调整：

| PR | 类型 | 关键点 |
|---|---|---|
| [#3187](https://github.com/nanocoai/nanoclaw/pull/3187)（已关闭） | 修复 | 在 agent-runner 中禁用内置的 `SendMessage` 能力，从而保证**代理间消息传递机制**不被内置方法遮蔽，为多代理协作扫清障碍。 |
| [#3175](https://github.com/nanocoai/nanoclaw/pull/3175)（已关闭） | 修复 | 将 command-gate 拒绝通知从直接写 `outbound.db` 改为通过 delivery adapter 路由，**消除双写入者的数据损坏风险**。 |

**重大架构方向**：`outbound.db` 的单一写入者规则被反复强调（同时在 PR #3192 和 #3175 中出现），表明项目在数据持久化层的规范上正进行**严格的自查与自纠**，这对容器环境下的数据完整性至关重要。

此外，已合并的 [#3187](https://github.com/nanocoai/nanoclaw/pull/3187) 为**多代理通信**铺平了道路，而 [#3175](https://github.com/nanocoai/nanoclaw/pull/3175) 则从根源上修复了潜在的数据竞争条件，这两项合并均为项目带来了实质性的健康度提升。

---

## 版本发布

**无新版本发布。**

---

## 社区热点

### 热点Issue：#2528 — Signal 通道附件不可达（[链接](https://github.com/nanocoai/nanoclaw/issues/2528)）
- **讨论热度**：虽评论数仅 1，但 Issue 自 5 月创建以来持续被更新（最新更新于 8 月 5 日），且其问题描述直接关联到今日新提交的 PR **#3156**。
- **用户诉求**：用户希望 Agent 能像处理文本一样无缝处理图片/PDF 附件，这是**多模态交互**的基础需求。

### 关联分析
[PR #3156](https://github.com/nanocoai/nanoclaw/pull/3156)（`fix(agent-runner): carry channel attachments to providers as structured parts`）正是针对此痛点——将通道附件转为结构化 parts 传递给模型。**Issue 与 PR 之间的呼应**表明该项目对用户反馈有较好的响应机制，修复方向明确。

### 热点PR：#3192 / #3175 — 数据库写入规范
- 同一位作者 Joi 先后提交了相同主题的 PR（#3175 已关闭、#3192 最新待合并），说明该修复可能经历了迭代或需要重新评审。这通常是核心维护者对代码质量严苛把关的表现，但也可能意味着**修复尚未完全收敛**。

---

## Bug 与稳定性

| 严重程度 | Issue/PR | 状况 | 已有修复？ |
|---|---|---|---|
| **高** | [#2528](https://github.com/nanocoai/nanoclaw/issues/2528) Signal 图像/PDF附件无法被容器内 Agent 读取 | 阻塞多模态交互 | **有** — 关联 PR #3156 已在待合并列表 |
| **中** | [#2006](https://github.com/nanocoai/nanoclaw/issues/2006) 全新 Debian 12 LXC 安装时 Docker socket 权限被拒 | 安装流程缺陷，影响新用户上手 | **无明确修复 PR** — 已持续 3 个多月，需要维护者介入 |
| **中** | [PR #3191](https://github.com/nanocoai/nanoclaw/pull/3191) WhatsApp 登出后 `setup()` 无限期挂起，阻塞宿主启动 | 死锁风险，影响多云部署稳定性 | **有** — 已提交修复但待合并 |
| **低** | [PR #3192](https://github.com/nanocoai/nanoclaw/pull/3192) `outbound.db` 双写入者的数据损坏风险 | 架构一致性隐患 | **有** — 已提交修复但待合并 |

> **最紧迫问题**：Issue #2006（安装时权限问题）已存在超 100 天且无明确修复方向，这可能在持续**损耗新用户信任度**，值得项目组优先关注。

---

## 功能请求与路线图信号

从今日 PR 动态中，可观察到以下新功能信号：

| 信号 | 对应PR | 类型 | 前景判断 |
|---|---|---|---|
| **Tavily MCP 工具技能** | [#3190](https://github.com/nanocoai/nanoclaw/pull/3190) | 搜索能力扩展 | 高概率纳入 — 符合“补充 Agent 工具生态”的主线，且为标准 Utility skill |
| **add-why 技能** — 解释单条消息为何如此处理 | [#3189](https://github.com/nanocoai/nanoclaw/pull/3189) | 可解释性增强 | 中概率 — 提升用户调试体验，属于锦上添花 |
| **Dial 通道集成** | [#3050](https://github.com/nanocoai/nanoclaw/pull/3050) | 新渠道 | 低概率（近期）— 大功能集成需较长 review 周期，但方向明确 |
| **清理过期 MCP 技能**（移除 Qodo 和 Google MCP） | [#3172](https://github.com/nanocoai/nanoclaw/pull/3172) | 技能精简 | 高概率 — 避免过时技能干扰用户体验 |

**路线图判断**：围绕“MCP 工具集扩展”和“通道网关健壮性”两个方向，项目仍在持续推进。**建议**：`Tavily MCP`（#3190）与 `add-why`（#3189）均为低风险高价值的 Utility skill，预计在不远的版本中会合入。

---

## 用户反馈摘要

- **多模态需求迫切**：`#2528` 的用户在 Signal 场景下期望图片/PDF 可被直接读取，反映出用户将聊天工具视为 Agent 的“眼睛”，对附件解析有刚需。
- **安装体验是软肋**：`#2006` 中用户卡在安装过程的权限环节，且**恢复路径未触发**，说明容错机制仍不完善。这类问题对开发者社区“试错成本”影响极大，需优先修复。
- **代理间通信是高频诉求**：PR #3187（禁用内置 SendMessage）说明有人在实际使用多代理架构，且受限于现有约束。该合入将直接**解锁协作场景**。
- **社区对“规范化”贡献热情高**：多个 PR 标注了 `follows-guidelines` 标签，且贡献者们自行补充了类型清单（`Feature skill`/`Utility skill`），体现 NanaClaw 的社区维护文化已逐步成熟。

---

## 待处理积压

**重点提示维护者关注**：

| 条目 | 存活时长 | 类型 | 备注 |
|---|---|---|---|
| [#2006](https://github.com/nanocoai/nanoclaw/issues/2006) Debian 12 LXC 安装权限失败 | **> 100天** | 安装阻断 | 有评论但无 PR 指向，建议核心团队尽快指派 |
| [#2346](https://github.com/nanocoai/nanoclaw/pull/2346) 未知斜杠命令按普通聊天处理 | **> 85天** | 功能修复 | 有明确解决方案，但长期搁置，可能已在内部实现中 |
| [#3050](https://github.com/nanocoai/nanoclaw/pull/3050) Dial 通道集成 | 21天 | 新功能 | 大型 PR，等待整体规划评审，可能随下个大版本合入 |

> **风险提示**：若 Issue #2006 持续无响应，可能引发新用户负面传播；建议在此基础上补充更友好的安装引导或错误提示，以降低失败率。

---

*数据口径：基于 2026-08-05 的 GitHub 动态，日报生成于 2026-08-06。*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw 项目动态日报

**日期：2026-08-06** | **数据窗口：2026-08-05 至 2026-08-06**


## 1. 今日速览

NullClaw 项目今日处于**平稳维护期**，整体活跃度中等偏下。过去 24 小时内无新 Issue 提交、无版本发布，但出现了 2 条高质量 PR（#984、#985），均由同一贡献者提交，聚焦于**运行时稳定性**与**渠道轮询可靠性**两大核心痛点。两条 PR 均处于待合并状态，尚未获得官方 review。值得关注的是，两条 PR 分别针对 Issue #976（运行时栈溢出）与 #972（频道静默断连），说明近期社区反馈的稳定性问题正在被积极修复。项目目前无阻塞性危机，处于“低噪音、高价值产出”的状态。


## 2. 版本发布

**今日无新版本发布。**

最新 Release 无变化。注意两条待合并 PR 均为 bugfix 类型，预计合入后将进入下一个 patch 版本（如 v0.x.y+1）。


## 3. 项目进展

今日无 PR 被合并或关闭，但 2 条高价值修复 PR 已提交并等待审核：

| PR | 标题 | 解决的问题 | 状态 |
|----|------|-----------|------|
| [#985](https://github.com/nullclaw/nullclaw/pull/985) | `fix(runtime): give the agent turn path a 16 MiB stack` | Agent 对话路径栈溢出（Issue [#976](https://github.com/nullclaw/nullclaw/issues/976)） | 待合并 |
| [#984](https://github.com/nullclaw/nullclaw/pull/984) | `fix(channels): let poll failures age out a dead polling thread` | Telegram/Matrix 频道静默断连（Issue [#972](https://github.com/nullclaw/nullclaw/issues/972)） | 待合并 |

**关键发现**：PR #985 揭示了一个**根因级别的配置事故** —— `SESSION_TURN_STACK_SIZE` 被错误地别名为 `HEAVY_RUNTIME_STACK_SIZE`（2 MiB），导致所有执行 `SessionManager.processMessage*()` / `Agent.turn()` 的线程栈空间严重不足。作者建议将其提升至 16 MiB，这是一个**直击核心架构**的修复。

项目当前处于“修复积压期”，两条 PR 的合入将直接解决两个长期存在的稳定性痛点，但需维护者尽快 review。


## 4. 社区热点

今日无高热度讨论（无评论、无 👍 增长）。但 **PR #985 值得重点关注**，因为它揭示了 `SessionManager` 中的一个底层配置错误。实际上，栈溢出通常是间歇性触发——只在深层递归或大帧局部变量时崩——这解释了为何问题可能已存在一段时间而未被发现。建议维护者优先 review 此 PR，因为它直接影响 AI agent 对话的可靠性。


## 5. Bug 与稳定性

今日共 2 条与稳定性相关的修复，均为**中高严重程度**：

| 严重程度 | 问题描述 | 影响范围 | 修复 PR | 状态 |
|---------|---------|---------|---------|------|
| 🔴 高 | **Agent 对话栈溢出**（[#976](https://github.com/nullclaw/nullclaw/issues/976)）：`SESSION_TURN_STACK_SIZE` 被错误别名至 2 MiB，导致 agent turn 路径在高负载或复杂对话时崩溃 | 所有使用 agent 对话功能的用户 | [#985](https://github.com/nullclaw/nullclaw/pull/985)（16 MiB 栈） | 待合并 |
| 🟡 中 | **Telegram/Matrix 频道静默断连**（[#972](https://github.com/nullclaw/nullclaw/issues/972)）：空闲一夜后频道不可用，agent 仍响应，需重启 gateway 恢复 | Telegram/Matrix 渠道用户 | [#984](https://github.com/nullclaw/nullclaw/pull/984)（失败轮询超时回收） | 待合并 |

两条 PR 的根因分析都做得非常扎实（代码级定位），贡献者 @raskevichai 的专业度值得肯定。目前均未获得官方 review 或 merge。


## 6. 功能请求与路线图信号

今日无新功能请求。从已有 PR 反推路线图信号：

- **PR #985** 与 **PR #984** 均为修复类，且属于社区主动提交并通过 `Closes #xxx` 关联了既有 Issue，表明项目的 **Issue 驱动开发流程正在良性运转**。
- 栈大小从 2 MiB → 16 MiB 的调整，暗示项目对**复杂 agent 对话场景**的支持是其重点方向。
- 渠道稳定性修复表明 **Telegram/Matrix 集成质量** 是当前社区关注焦点。


## 7. 用户反馈摘要

今日无评论数据可供提炼。基于 PR 所关联的 Issue 推断：用户核心痛点集中在 **长时间运行后的静默故障**（过夜后频道失联）与**对话深度增加时的崩溃**。考虑到栈溢出只在复杂对话场景出现，这类反馈大概率来自高频或重度使用者，说明基础功能已稳定，**社区正转向对高级场景可靠性的诉求**。


## 8. 待处理积压

**当前最需要维护者关注的 2 条 PR**（均已超过 24 小时未获 review）：

> ⚠️ **优先级建议**：这两条 PR 修复的是同一实验性代码库中的核心问题（运行时栈 + 渠道轮询），建议维护者在下一个工作周期内优先 review。若测试通过，建议在同一次发布中一并合入。

| 编号 | 类型 | 标题 | 等待时长 | 关联 Issue |
|------|------|------|---------|-----------|
| [#985](https://github.com/nullclaw/nullclaw/pull/985) | PR (bugfix) | `fix(runtime): give the agent turn path a 16 MiB stack` | >24h | [#976](https://github.com/nullclaw/nullclaw/issues/976) |
| [#984](https://github.com/nullclaw/nullclaw/pull/984) | PR (bugfix) | `fix(channels): let poll failures age out a dead polling thread` | >24h | [#972](https://github.com/nullclaw/nullclaw/issues/972) |

另有 2 个关联 Issue 等待被关闭（#976、#972），将在对应 PR 合入后自动解决。


## 📊 项目健康度评估

| 维度 | 评分 | 说明 |
|------|------|------|
| **代码质量** | ⭐⭐⭐⭐ | 两条 PR 均有清晰的根因分析和代码级定位 |
| **维护响应** | ⭐⭐⭐ | 无新的 Issue 积压，但 PR 等待 review 时间略长 |
| **社区活跃** | ⭐⭐ | 今日仅 1 位贡献者活跃，无讨论互动 |
| **稳定性趋势** | ⭐⭐⭐⭐ | 两条关键 bugfix 已在路上，预计合入后稳定性显著提升 |

**总体评价**：项目处于“稳定中推进”阶段。社区贡献者正在主动修复深层架构问题，但维护者需加速 review 节奏，避免挫伤贡献者积极性。


*报告生成时间：2026-08-06 | 数据来源：NullClaw GitHub 仓库*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw 项目动态日报 — 2026-08-06

## 1. 今日速览

过去 24 小时项目活跃度极高：43 条 Issue 更新（其中 33 条新开或活跃）、50 条 PR 更新（30 条待合并），以及 1 个新版本发布（v1.1.0-rc.1，8 月 3 日发布）。社区活动集中于 bug_bash 系列测试报告（多为 P1/P2 级问题）、MCP 集成可靠性、以及设计系统（Design System）提案的持续推进。值得关注的是，新一轮 bug bash 暴露了多个与 MCP 认证、连接状态验证相关的"AI 幻觉"类问题，值得维护团队优先处理。

---

## 2. 版本发布

**ironclaw-v1.1.0-rc.1**（2026-08-03 发布）

Release Notes 要点：
- **扩展覆盖面**：支持注册任意托管的 MCP 服务器、支持通过 IronHub 深度链接安装扩展
- **持久化文件附件**：可跨渠道传递文件附件
- **Slack `/ironclaw` 斜杠命令**：新增 Slack 交互入口
- **错误信息可读性提升**：对失败场景的报错信息做了全面优化

⚠️ **注意**：此为 1.0.0 后的首个候选版本，涉及较多新功能，建议用户在非生产环境先行验证。

---

## 3. 项目进展（今日合并/关闭的重要 PR）

| PR | 说明 | 状态 |
|---|---|---|
| [#7260](https://github.com/nearai/ironclaw/pull/7260) | 回移 MCP 出口和日志可读性修复 | 🔀 已合并 |
| [#7261](https://github.com/nearai/ironclaw/pull/7261) | 修复发布 canary 临时路径问题（#7256 引入） | 🔀 已合并 |
| [#7196](https://github.com/nearai/ironclaw/pull/7196) | WASM 组依赖升级（3 项更新） | 🔀 已合并 |
| [#6831](https://github.com/nearai/ironclaw/pull/6831) | **标准化消息框架**：16 个核心操作、13 个保留操作名、规范错误码分类法 | ✅ 已合并 |
| [#7244](https://github.com/nearai/ironclaw/issues/7244) | 修复 main 分支 CI 失败（20260804） | ✅ 已关闭 |

**关键进展**：#6831 的合入标志着 Reborn 版本消息传递机制进入标准化阶段，为后续多端一致性交付奠定基础。CI 稳定性持续修复，但 #7209 指出回归测试门禁仍存在前端断言风格识别缺陷，可能继续阻塞前端 PR。

---

## 4. 社区热点（高讨论量 Issues/PRs）

| 编号 | 标题 | 评论数 | 热度分析 |
|---|---|---|---|
| [#3036](https://github.com/nearai/ironclaw/issues/3036) | [EPIC] Configuration-as-Code for IronClaw Reborn | 7 | 作为 EPIC 讨论热度最高，反映用户对声明式配置的强烈需求 |
| [#7194](https://github.com/nearai/ironclaw/issues/7194) | feat(outbound): admin-allowed shared channel as outbound delivery target | 3 | 涉及 Slack 渠道交付扩展，与 v1.1.0 功能方向一致 |
| [#7204](https://github.com/nearai/ironclaw/issues/7204) | webui(chat): composer focus papercuts | 2 | WebChat v2 交互细节优化，用户对 UX 打磨需求持续存在 |
| [#7209](https://github.com/nearai/ironclaw/issues/7209) | CI 回归门禁无法识别前端断言风格 | 2 | **关键阻塞项**，直接影响前端 PR 合入效率 |

**趋势判断**：讨论集中在"配置化/可编程性"（#3036）、"渠道扩展"（#7194）和"CI 基础设施"（#7209）三大方向。

---

## 5. Bug 与稳定性

### 🔴 P1 级（需立即处理）

| Issue | 描述 | 修复 PR |
|---|---|---|
| [#7247](https://github.com/nearai/ironclaw/issues/7247) | AI 错误声称 GitHub 已连接（实际未验证认证状态） | 无 |
| [#7246](https://github.com/nearai/ironclaw/issues/7246) | AI 幻觉自动化任务运行状态（实际无此自动化） | 无 |

### 🟡 P2 级（计划中）

| Issue | 描述 | 修复 PR |
|---|---|---|
| [#7249](https://github.com/nearai/ironclaw/issues/7249) | Slack DM 执行结果被错误投递到 Telegram | 无 |
| [#7251](https://github.com/nearai/ironclaw/issues/7251) | Agent 猜测 MCP 认证类型而非主动发现 | 无 |
| [#7250](https://github.com/nearai/ironclaw/issues/7250) | DeepWiki MCP 对网络错误给出误导性认证建议 | 无 |
| [#7248](https://github.com/nearai/ironclaw/issues/7248) | 无效自定义 MCP 端点被接受，导致运行失败 | [#7253](https://github.com/nearai/ironclaw/pull/7253)（open，XL） |
| [#6257](https://github.com/nearai/ironclaw/issues/6257) | PDF 附件 MIME 类型错误（"Invalid value (attachments.mime_type)"） | 无 |

### 🟢 其他

- [#7254](https://github.com/nearai/ironclaw/issues/7254)：Slack 反馈线程附件无法读取——影响产品反馈流程
- [#7231](https://github.com/nearai/ironclaw/issues/7231)：AI 审查文本写 "APPROVE" 但未提交正式 GitHub approval，导致 PR 持续被合并门禁阻塞→**建议维护者关注 bot 审查机制**

---

## 6. 功能请求与路线图信号

| 功能需求 | 相关 Issue/PR | 可能纳入版本 |
|---|---|---|
| **Configuration-as-Code**（租户蓝图） | [#3036](https://github.com/nearai/ironclaw/issues/3036) | v1.2.0+（EPIC 规划中） |
| **管理型 Agent 作为 UserId Subject** | [#6578](https://github.com/nearai/ironclaw/issues/6578) | 规划中 |
| **IronHub 深度集成** | [#6731](https://github.com/nearai/ironclaw/issues/6731) | v1.1.0（进行中） |
| **技能系统重构**：模型自主选择技能 | [#6941](https://github.com/nearai/ironclaw/issues/6941) + [#6938](https://github.com/nearai/ironclaw/pull/6938) + [#6745](https://github.com/nearai/ironclaw/pull/6745) | v1.1.0（两个 XL PR 待合并） |
| **Storybook + AI 设计系统** | [#7038](https://github.com/nearai/ironclaw/issues/7038) + [#7039](https://github.com/nearai/ironclaw/pull/7039) + [#7043](https://github.com/nearai/ironclaw/pull/7043) + [#7257](https://github.com/nearai/ironclaw/pull/7257) | 规划中 |
| **Web Debug Inspector** | [#7218](https://github.com/nearai/ironclaw/issues/7218) | 规划中 |

**信号**：v1.1.0 聚焦 MCP 扩展性和技能系统；后续版本将走向声明式配置与设计系统治理。

---

## 7. 用户反馈摘要

- **PDF 生成/发送报错**（[#6257](https://github.com/nearai/ironclaw/issues/6257)）：用户反馈 "Invalid value (attachments.mime_type)" 错误，疑似类型判断问题，阻碍了 PDF 文件正常使用。
- **Slack 附件读取失败**（[#7254](https://github.com/nearai/ironclaw/issues/7254)）：产品反馈流程中，用户无法通过 Slack 附件向 IronClaw 传递复现文件，导致 triage 流程受阻。
- **跨渠道通知异常**（[#7249](https://github.com/nearai/ironclaw/issues/7249)）：Slack DM 执行结果误投递到 Telegram，用户对渠道路由的准确性提出质疑。
- **Agent 状态幻觉**（[#7246](https://github.com/nearai/ironclaw/issues/7246)、[#7247](https://github.com/nearai/ironclaw/issues/7247)）：Agent 在未验证实际状态时虚构"运行中/已连接"信息，属于**信任破坏型问题**，需在模型层或工具层加以约束。

---

## 8. 待处理积压（需维护者关注）

| 类型 | 编号 | 标题 | 持续时长 | 备注 |
|---|---|---|---|---|
| EPIC | [#3036](https://github.com/nearai/ironclaw/issues/3036) | Configuration-as-Code | 100 天 | 评论活跃但无明确排期 |
| EPIC | [#6731](https://github.com/nearai/ironclaw/issues/6731) | IronHub 集成 | 10 天 | v1.1.0 范围内，需加速 |
| PR | [#6938](https://github.com/nearai/ironclaw/pull/6938) | 模型选择技能（XL） | 6 天 | 依赖 #6745，处于栈底 |
| PR | [#6745](https://github.com/nearai/ironclaw/pull/6745) | 技能可选择/可安装（XL） | 9 天 | 同上，为前置依赖 |
| Issue | [#7245](https://github.com/nearai/ironclaw/issues/7245) | reborn_services.rs 超 6,400 行需拆分 | 1 天 | 架构规则要求跟踪 |
| Issue | [#7209](https://github.com/nearai/ironclaw/issues/7209) | CI 回归门禁前端断言识别缺陷 | 1 天 | **高优**，阻塞前端 PR 合入 |
| Issue | [#7231](https://github.com/nearai/ironclaw/issues/7231) | AI 审查未提交正式 approval | 1 天 | **高优**，导致 PR 合并阻塞 |

---

**项目健康度评估**：🟢 **活跃且健康** — 社区反馈渠道畅通（bug_bash 测试产出丰富），功能开发与基础设施加固双线推进。需重点关注 P1 级 AI 幻觉问题与 CI 门禁缺陷，其次是技能系统两个 XL PR 的合入进度。

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI 项目日报 — 2026-08-06

> 网易有道开源 AI 智能体/个人助手框架 | [GitHub 仓库](https://github.com/netease-youdao/LobsterAI)


## 1. 今日速览

今日项目活跃度较高，PR 通道表现亮眼：24 小时内 12 条 PR 被合并/关闭，仅 1 条待合并，合并率达到 **92%**，说明维护团队响应迅速、开发节奏紧凑。当日发布了 **2026.8.5 版本**，主要包含原生每日签到体验、企业级账号隔离鉴权等新功能。值得一提的是一项**关于文本渲染引擎的深度技术分析**——社区用户针对 `nimGateway.ts` 中 `teamTypeNum` 硬编码错误的深入定位（Issue #1200）在时隔数月后重新获得关注，侧面印证了该问题对实际用户的影响仍在持续。但同样需要关注的是，今日新提交的 2 个 Bug（#2441、#2440）均指向**系统提示词注入与技能配置管理**的深层设计问题，或对后续版本迭代方向有较大影响。


## 2. 版本发布

### [LobsterAI 2026.8.5](https://github.com/netease-youdao/LobsterAI/releases) — 8月5日发布

**新功能**
- **原生每日签到体验**（PR #2408）：新增 activity 模块的原生每日签到功能，提升启动页/活动页的交互流畅度
- **企业级账号隔离**（PR #2409）：隔离账号维度的鉴权与服务流，为多租户/企业场景提供更清晰的权限边界

**风格与优化**
- 包含若干 style 调整（未展开说明）

**迁移注意事项**：企业版用户需关注账号鉴权流程的变化——本次隔离可能影响自定义鉴权中间件或服务端 API 的调用方式，建议企业部署用户在升级前审查账号服务相关集成代码。


## 3. 项目进展

今日 12 条 PR 被合并/关闭，重点进展集中在**窗口生命周期管理**、**搜索功能升级**和**OpenClaw 运行时稳定性**三个方向。

**核心功能推进**

- **对话搜索入口升级**（[PR #2435](https://github.com/netease-youdao/LobsterAI/pull/2435)，`feat(cowork): add title-bar conversation search`）：在标题栏新增会话搜索按钮，复用侧边栏搜索图标与既有检索流程，统一初始化路径。该 PR 涉及 renderer/docs/cowork 三个模块，是一个跨领域的功能增强，对重度用户的消息检索效率有明显提升

- **窗口生命周期加固**（[PR #2437](https://github.com/netease-youdao/LobsterAI/pull/2437)，`fix(main): harden window lifecycle and shutdown against hangs`）：为 OpenAI 兼容代理和 HTML 预览服务器增加了 shutdown 的 drain 定时器与硬截止时间，解决 keep-alive 连接阻塞应用退出；主窗口激活改为等待首帧渲染后再执行，避免焦点/二次实例的队列 show 请求悬挂。该项修复显著改善 Windows/macOS 上“退出卡死”的用户体验

- **OpenClaw 网关锁文件竞态修复**（[PR #2436](https://github.com/netease-youdao/LobsterAI/pull/2436)，`fix(openclaw): prevent gateway lock poisoning from self-restart races`）：修复两个竞态条件——LobsterAI 强制 kill 网关进程时可能落在锁文件写入中途，以及网关自重启的竞态，两者都曾导致网关 respawn 持续失败达 30 秒。对依赖 OpenClaw 网关的用户而言这是一个**重要的稳定性修复**

**活动/海报与依赖更新**
- 多条活动模块海报更新/精简（[PR #2432](https://github.com/netease-youdao/LobsterAI/pull/2432)、[#2433](https://github.com/netease-youdao/LobsterAI/pull/2433)、[#2438](https://github.com/netease-youdao/LobsterAI/pull/2438)、[#2439](https://github.com/netease-youdao/LobsterAI/pull/2439)），涉及世界杯最终奖励弹窗关闭、海报素材替换与关闭图标适配
- 依赖更新合并：`cross-env` 10.1.0（[#1279](https://github.com/netease-youdao/LobsterAI/pull/1279)）、`react-dom` 19.2.4（[#1280](https://github.com/netease-youdao/LobsterAI/pull/1280)）、`vite` 8.0.9（[#1281](https://github.com/netease-youdao/LobsterAI/pull/1281)）


## 4. 社区热点

今日最受关注的是 **Issue #1200**（NIM 超大群群名获取 Bug）：

- [Issue #1200](https://github.com/netease-youdao/LobsterAI/issues/1200) — `[Bug] NIM 超大群消息中 teamTypeNum 硬编码错误导致群名无法正确获取`
  - 作者：MaoQianTu | 创建于 2026-04-01 | 更新于 2026-08-05 | 评论：1
  - **热度信号**：这是一个 4 月提交的 issue，今日重新活跃，表明该 Bug 仍对用户造成困扰
  - **背后诉求**：用户指出 `nimGateway.ts` 第 917 行 `fetchTeamName` 调用时 `teamTypeNum` 值与 V2NIM SDK 枚举定义不一致——superTeam 类型被传成了普通 team 值，普通群则被传为 p2p 值，导致超大群 @ 机器人时群名无法获取、显示为原始 ID。用户已附带精确的行号、代码映射和修复方案（一行修改），诉求明确：尽快合入


## 5. Bug 与稳定性

今日报告了 2 个新 Bug，另有 1 个长期 Bug 获得新关注。按严重程度排列：

**高 — 系统提示词重复注入**（[Issue #2440](https://github.com/netease-youdao/LobsterAI/issues/2440)，新提交）
- 桌面端每个新会话首条用户消息中注入的 `[LobsterAI system instructions]` 块，**78% 内容与 `AGENTS.md` 托管段逐字重复**
- 影响：模型冗余读取相同指令，增加 token 消耗，可能稀释系统提示词的注意力权重
- 已有 PR：❌ 无

**高 — 技能开关静默失效**（[Issue #2441](https://github.com/netease-youdao/LobsterAI/issues/2441)，新提交）
- 双问题叠加：技能开关按目录名写入，OpenClaw 按 frontmatter name 匹配，不一致时开关失效；且 `openclaw.json` 被整文件覆盖，用户无持久精简入口
- 影响：用户无法按预期控制每次新对话的系统提示词内容
- 已有 PR：❌ 无

**中 — NIM 超大群群名获取错误**（[Issue #1200](https://github.com/netease-youdao/LobsterAI/issues/1200)，4月提交，今日重现活跃）
- 定位明确、修复方案简单（一行修改），见 [PR #1201](https://github.com/netease-youdao/LobsterAI/pull/1201)
- 状态：关联 PR #1201 仍处于 OPEN 状态，**维护者尚未响应**


## 6. 功能请求与路线图信号

**已有对应 PR 推进的方向**

- **对话搜索能力增强**：PR #2435 新增标题栏搜索按钮，回应了用户对消息检索效率的潜在需求，预计在下一版本（2026.8.5+）中可用
- **系统提示词精简**：Issue #2441 明确提出用户需要“持久地精简每次新对话的系统提示词”的能力，当前只报了 Bug，但设计缺口暗示后续版本可能引入更灵活的 prompt 管理机制

**可能被纳入后续版本的方向**

- 基于 #2441 中提到的“用户无持久精简入口”问题，未来可能新增 **openclaw.json 局部覆盖/管理界面**，而非整文件覆写
- 基于 #2440 的重复注入问题，后续版本可能引入 **system prompt 生成去重机制**，避免同一指令多次注入


## 7. 用户反馈摘要

| 来源 | 用户声音 | 分析 |
|------|----------|------|
| [#2440](https://github.com/netease-youdao/LobsterAI/issues/2440) | “同一套指令让模型读了两遍” | 用户对 token 浪费和模型注意力稀释的担忧，说明对成本和质量都有要求 |
| [#2441](https://github.com/netease-youdao/LobsterAI/issues/2441) | “用户没有办法持久地精简进入每次新对话的系统提示词” | 用户希望精细控制会话上下文，是高级用户的需求信号 |
| [#1200](https://github.com/netease-youdao/LobsterAI/issues/1200) | 提供了完整定位（行号、枚举映射、修复代码） | 用户愿意深入源码排查并给出修复方案，说明技术型用户群体活跃，也侧面反映该 Bug 对真实场景影响明显 |

整体来看，今日用户反馈集中在**提示词管理和消息链路稳定性**两个维度，用户对代码定位能力较强，反馈质量较高。


## 8. 待处理积压

**需维护者重点关注的长期未响应项：**

1. **[PR #1201](https://github.com/netease-youdao/LobsterAI/pull/1201)（对应 Issue #1200）— 已开放 4 个月**
   - NIM 群名获取 Bug 的修复 PR，一行修改、风险极低，但长期未合入
   - 今日该 Issue 重新获得评论，说明用户仍在遭遇此问题，建议尽快合入或回应

2. **依赖更新系列 PR（#1279、#1280、#1281）— 4 月创建，今日刚关闭**
   - 这三条 PR 在今日被关闭，推测可能是由 dependabot 自动关闭或手动合入；若为手动关闭而非合并，需确认依赖升级的推进方式


## 项目健康度评估

| 指标 | 状态 |
|------|------|
| PR 合并率 | 92%（12/13），十分健康 |
| Issue 响应速度 | 新 Issue 尚未有维护者回应，响应延迟存在 |
| 版本发布节奏 | 约每周一版，节奏稳定 |
| 社区参与度 | 用户能深入源码定位问题（#1200），社区技术氛围好 |
| 风险项 | 长期未响应的 Bug 修复 PR（#1201）与今日新报的两个提示词管理 Bug 可能成为后续版本迭代的瓶颈 |

**一句话总结**：LobsterAI 今日 PR 流转高效、新版本如期发布，但提示词注入与技能配置的深层设计缺口（#2440、#2441）值得团队优先关注，同时建议尽快合入等待已久的 #1201 一行修复。

---

*报告生成时间：2026-08-06 | 数据来源：GitHub API*

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

# CoPaw 项目动态日报 — 2026-08-06

## 1. 今日速览

CoPaw 项目过去 24 小时社区活跃度较高：共产生 25 条 Issue 更新（19 条活跃，6 条已关闭）和 50 条 PR 更新（29 条待合并，21 条已合并/关闭）。当日无新版本发布。值得关注的信号有三：一是多位用户同时反馈 **WeChat iLink 频道的一次性 context_token 被 typing indicator 消耗**（#6696）以及**审批提示在纯 WeChat 场景下不可达**（#6695，已关闭），说明该频道的审批与消息机制存在设计缺陷；二是 **DeepSeek 等 thinking 模式上游的 reasoning_content 回传问题**（#6707）持续引发多个 PR 修复（#6675、#6721），表明该问题已严重影响使用 thinking 模式的大量用户；三是 **MCP 工具规律性失效**（#6732）和 **v2.1.0b1 桌面版 PYTHONHOME 注入导致 Python 子进程崩溃**（#6697）两个新上报的严重 Bug 值得关注。整体来看，项目正处于 v2.1 迭代的高频修复期。

---

## 2. 版本发布

今日无新版本发布。

---

## 3. 项目进展

今日合并/关闭的 PR 主要集中在**稳定性修复**与**功能收尾**两个方向，以下为关键合并：

### 功能落地
- **[#5598] feat(console): 添加 LLM 回退配置 UI**（已合并）— 为用户提供了在 Agent 配置页和全局模型设置页配置模型回退候选列表的界面，配合此前合入的后端逻辑（#5597），**LLM 模型故障自动回退功能已完整落地**。该功能原为长线开发（6/29 开启），今日完成合并。
- **[#5597] feat(backend): 按 Agent 和全局的 LLM 模型回退**（已合并）— 见上，后端支持在重试耗尽后按顺序切换到候选备份模型。
- **[#5462] feat(console): 新增全局响应式工具类**（已合并）— 为移动端适配提供共享样式方案，减少重复代码。
- **[#6718] feat: 统一应用市场展示**（已合并）— 应用市场栏目 UI 统一。
- **[#5447] fix(channel): 控制台错误时 yield AgentResponse 以解锁 UI**（已合并）— 修复模型/运行时错误导致 UI 无限等待的问题。

### 关键修复
- **[#6675] fix: 强制 DeepSeek 模型回传 reasoning_content**（已合并，first-time-contributor）— 修复滚动上下文压缩导致 ThinkingBlock 被剥离后，上游 API 拒绝请求的问题（对应 Issue #6667、#6541）。该 PR 经过约 24 小时的 Review 后今日合入，目前是 thinking 模式最关键的修复之一。
- **[#6713] fix(router): 敏感目录排除增加审计可见性**（已合并）。

### 正在待合并的重点 PR
- **[#6723] fix(provider): 过期能力缓存条目 + 模型切换时清缓存**（OPEN）— 针对 OpenRouter 多模态探测错误覆盖能力配置的问题。

---

## 4. 社区热点

### 最热议题 TOP 3

| 排名 | 议题 | 类型 | 评论数 | 状态 |
|------|------|------|--------|------|
| 1 | **[#6684] 频道重试功能增强请求** | 功能增强 | 4 | OPEN |
| 2 | **[#6436] 自动模型路由（The Right Model for Every Message）** | 功能增强 | 3 | OPEN |
| 3 | **[#6480] nohup/& 导致 Agent 卡住** | 问题咨询 | 2 | OPEN |

- **#6684「频道重试功能」**：用户使用自建 Matrix 服务，QwenPaw 服务重启后快于 Matrix 服务导致连接失败，且无重试/健康检测机制，每次都必须手动重新保存频道才能恢复。这是**基础设施依赖场景下的韧性缺口**，反馈具有代表性——不仅是 Matrix，任何存在启动依赖关系的自建服务都可能受影响。
- **#6436「自动模型路由」**：用户提出按消息特点自动路由到最合适的模型（简单对话→小模型，图片→视觉模型，复杂推理→大模型），而非每个 Agent 锁定单一模型。该需求横跨模型路由、能力探测、成本控制等多个模块，目前仍是 OPEN 状态，但已经积累了一定关注度。
- **#6480「nohup 执行命令卡住」**：用户反馈 `execute_shell_command` 工具执行含 `nohup` 或尾部 `&` 的命令后，Agent 永远不会回到 idle 状态。这是 shell 工具设计的边界问题。

---

## 5. Bug 与稳定性

### 严重程度：高

| Issue | 描述 | 状态 | 关联 PR |
|-------|------|------|---------|
| [#6697] | **v2.1.0b1 桌面版向子进程注入 PYTHONHOME → 所有 Python 子进程崩溃**（`encodings ModuleNotFoundError`）。影响：Windows Tauri 桌面版升级后所有衍生 Python 进程不可用。 | OPEN | 暂无 |
| [#6732] | **MCP 工具规律性失效**：每隔数小时 MCP 工具无法被调用，报"未注册/不存在"，重启 Docker 容器后恢复。核心后端稳定性问题。 | OPEN | 暂无 |
| [#6731] | **execute_shell_command 崩溃**：模型传入 sandbox_config 参数时，dataclass replace() 报错，工具必然崩溃。2.0.1 和 main 分支均存在。 | OPEN | 暂无 |
| [#6696] | **WeChat iLink：一次性 context_token 被 typing indicator 消耗** → 回复被拒（ret=-2），"working"指示器卡住。 | OPEN | 待定 |

### 严重程度：中

| Issue | 描述 | 状态 | 关联 PR |
|-------|------|------|---------|
| [#6726] | 长会话大量工具调用后报 400："tool 角色的消息必须响应 precede 的 tool_calls" 消息。Tauri 桌面版 2.0.0。 | OPEN | 暂无 |
| [#6708] | 上游网关在 SSE 流内以 503 错误事件报告故障，QwenPaw 不重试直接判定失败。 | OPEN | [PR #6714] 已提交修复 |
| [#6707] | thinking 模式上游 + 含工具调用的会话历史 → 400 invalid_request_error（reasoning_content 回传失败）。 | OPEN | [PR #6675] 已合入；[PR #6721] 待合并 |
| [#6698] | v2.1.0b1 浏览器 SDK 的 open() 总是报 WireProtocolError：Target crashed。 | OPEN | 暂无 |
| [#6687] | OpenRouter 多模态探测覆盖文档声明能力，误报 false。 | OPEN | [PR #6723] 已提交修复 |

### 严重程度：中低（已关闭或已有修复）
- **[#6700] 超大工具输出导致历史会话加载卡死**（CLOSED）— 建议输出截断与历史消息分页，已获响应。
- **[#6695] 纯 WeChat 场景下审批提示不可达**（CLOSED）— 已修复，但引发了后续 [#6728] 关于中文审批按钮的需求。

---

## 6. 功能请求与路线图信号

### 高潜力（有 PR 或已有修复支撑）

| 功能请求 | 对应 PR/状态 | 信号强度 |
|----------|--------------|----------|
| [#6699] **按需加载技能（On-Demand Skill Loading）** — 27+ 技能时 prompt 消耗 8k-10k tokens（占系统提示 25-30%），强烈建议按需加载。**多个用户连续提出，且已有关联的 skills 池重构（#6650）刚合入，按需加载是自然延展。** | 暂无对应 PR，但 [#6650] 的合入（PR #6729 也在验证该功能）已重构技能池 API，为按需加载铺路。 | ★★★★ |
| [#6707] **thinking 模式 reasoning_content 回传修复** | 已合入 [#6675]，[#6721]（AgentScope 消息重试）待并。 | ★★★★（已修复） |
| [#6436] **自动模型路由** | 暂无 PR，但 LLM 回退功能（#5597/#5598）已合入，自动路由是回退机制的自然延伸。 | ★★★ |
| [#6708] **SSE in-stream 错误重试** | [PR #6714] 待合并。 | ★★★（已修复） |

### 中等潜力

| 功能请求 | 说明 | 信号强度 |
|----------|------|----------|
| [#6724] **MCP 工具可配置超时** — MCPClientConfig 无 timeout 字段，call_tool 无上界，可能导致整个 turn 无限挂起。 | 明确的设计缺口，预计会被纳入 v2.1.x。 | ★★★ |
| [#6728] **WeChat 审批支持中文按钮** | 紧随 #6695 修复后的自然诉求，China-first 用户群需求明确。 | ★★ |
| [#6730] **Live artifact canvas — 侧栏渲染 Agent 生成的 HTML** | 工作区产物需离开聊天查看体验不佳；已有 PR #6719（持久化 workspace artifact 卡片）作为前奏。 | ★★ |
| [#6684] **频道重试/健康检测功能** | 自建服务场景的韧性需求，已有 4 条评论讨论。 | ★★ |

---

## 7. 用户反馈摘要

**正面反馈：**
- 无明确正面评价，但 #5598/#5597（LLM 回退）从 6/29 开发至今日合入，属于社区长期期待的功能，用户 `yaozy2020` 连续多个 PR 都在推进此方向。

**核心痛点（按声量排序）：**

1. **WeChat 频道审批与消息机制**（#6695/#6696/#6728 三位用户重叠）：审批提示在纯 WeChat 场景不可达→修复后按钮是英文→用户要求中文。此三连 Issue 表明 WeChat 是中国用户高频渠道，但审批交互设计并未充分适配。
2. **Thinking 模式（DeepSeek 等）与工具调用的兼容性**（#6707/#6675/#6721）：用户 `ChaosG` 连续上报多个 thinking 模式下的深水区 Bug，包括 reasoning_content 回传、SSE 错误重试、长会话工具调用历史等。说明当前 thinking 模式在复杂场景下仍不稳。
3. **桌面版 v2.1.0b1 稳定性回归**（#6697/#6698）：PYTHONHOME 注入和浏览器 SDK 崩溃两个问题都是 Windows 桌面版的**新引入**问题，用户 `AT8051` 连续上报两条。Beta 质量有待提升。
4. **技能功能消耗过大**（#6699）：`Ferrum360` 的量化分析（27 技能消耗 8k-10k tokens）为后续按需加载提供了清晰的数据论据。

---

## 8. 待处理积压

### 高优先级（重大 Bug 无 PR）

- **[#6697] v2.1.0b1 桌面版注入 PYTHONHOME 导致 Python 子进程全部崩溃** — 涉及桌面版核心功能（任何 Python 子进程调用均失败），且无关联 PR，建议维护者优先响应。
- **[#6732] MCP 工具规律性失效** — 影响 MCP 工具链核心可用性，用户重启容器才能恢复，需要排查是否与长连接超时或注册表同步有关。

### 中优先级（功能增强长期未响应）

- **[#6470]（如有）** — 今日数据中未发现超过 7 天无响应的 PR。**最长的待合并 PR 为 [#6302] feat: unify provider discovery（7/21 开启）**，已积压 16 天且仍为 OPEN，涉及 Provider 发现、模型元数据、路由的架构级重构，建议维护者给出明确 Review 时间表。
- **[#6580] test(e2e): 新增 Sprint4/5 覆盖（15 个用例）** — 7/30 开始待合并，测试覆盖完善工作节奏偏慢。
- **[#6669] fix(desktop): 稳定 Chrome 原生消息与 Windows 恢复锁定** — 涉及 Windows 启动失败修复，已待合并 2 天。

### 需关注的长期 OPEN 功能请求

- **[#6436] 自动模型路由** — 7/24 创建至今 13 天无维护者回复，社区讨论 3 条。LLM 回退功能合入后，建议重新评估此需求的技术可行性。

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

过去24小时无活动。

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

## ZeroClaw 项目动态日报 — 2026-08-06

---

### 1. 今日速览

ZeroClaw 项目目前处于 **高活跃度、密集评审期**。过去 24 小时内 Issues 和 PR 更新各 50 条，绝大多数为需维护者评审的 RFC 和待合并 PR，表明项目正处于 **架构设计收敛与实现并行的阶段**。值得关注的是：安全相关的 RFC/PR 占比较高（认证、shell 策略、路径禁用、WhatsApp 权限），且多个 P1/P2 级 Bug 在本日报周期内被新开或推进。此外，新开 Bug 的提交时间集中在 8 月 5 日，可能存在一次集中的质量反馈波次。当前没有新版本发布，v0.8.5 稳定线仍在推进中（截止 8 月 30 日）。

---

### 3. 项目进展

今日无 PR 被合并（唯一关闭的 PR #9750 为作者主动关闭，随后被 #9773 取代）。但以下 PR 的推进值得关注：

- **[#9777] fix(channels): accept Signal source UUID senders** — Audacity88 针对 #9774 提交修复，使 `sourceUuid` 发送者可被识别。🔗 [PR #9777](https://github.com/zeroclaw-labs/zeroclaw/pull/9777)
- **[#9776] feat(security): extend forbidden_paths with workspace-relative glob patterns** — 将 #8424 RFC 落地，新增 `ForbiddenPatternSet` 结构体。🔗 [PR #9776](https://github.com/zeroclaw-labs/zeroclaw/pull/9776)
- **[#9748] fix(runtime): prevent stale provider refreshes** — 通过 per-session generation counter 修复会话替换时的竞态条件（#9719）。🔗 [PR #9748](https://github.com/zeroclaw-labs/zeroclaw/pull/9748)
- **[#9773] fix(service): bound launchd daemon logs** — 替代 #9750，将 macOS 启动代理日志限制在 8 MiB 以内。🔗 [PR #9773](https://github.com/zeroclaw-labs/zeroclaw/pull/9773)
- **[#9420] fix(anthropic): support stored OAuth profiles** — 大型 XL 级 PR，实现 Anthropic 存储型 OAuth profile 支持，配套 RFC #9464 正在评审中。🔗 [PR #9420](https://github.com/zeroclaw-labs/zeroclaw/pull/9420)

**关闭的 Issues 值得注意**：
- **[#9462] zeroclaw-plugins lib tests never execute in CI** — 已关闭，CI 测试缺口已修复。🔗 [Issue #9462](https://github.com/zeroclaw-labs/zeroclaw/issues/9462)
- **[#6350] WhatsApp Web allowed-numbers bypassed** — 已关闭，但 #9397 表明同类问题仍在跟进。🔗 [Issue #6350](https://github.com/zeroclaw-labs/zeroclaw/issues/6350)

---

### 4. 社区热点

| 排名 | Issue/PR | 评论数 | 核心诉求 |
|-------|----------|--------|-----------|
| 1 | [#6808] RFC: Work Lanes & Board Automation | 18 | 通过标签自动化和工作泳道简化维护路由，已持续迭代 24 个修订版 |
| 2 | [#8303] RFC: Goal mode v1 | 18 | 需要跨多轮 agent 会话的持久化有界任务执行能力 |
| 3 | [#8603] RFC: Chat Completions profile | 16 | 社区强烈希望支持 OpenAI 兼容协议（Open WebUI、LobeChat 等） |
| 4 | [#7155] RFC: Shell 命令确认层级 | 16 | 高风险 shell 命令需要 allow/ask/deny 策略（类 Claude Code） |
| 5 | [#7141] RFC: 可插拔入站认证 | 12 | 统一身份认证与 canonical principals |

**分析**：最热门的讨论集中在 **协议兼容性（#8603）** 与 **安全策略（#7155、#7141）** 两个方向。值得注意的是，[#8603] 讨论的 OpenAI Chat Completions 兼容协议如果落地，将直接解锁 Open WebUI 和 LobeChat 等主流前端接入，这可能是社区最高呼声的功能之一。

---

### 5. Bug 与稳定性

**P1（严重）**：

- **[#9775] OpenRouter streaming 丢失 provider_extra** — 新开，S1 级，`stream_chat` 路径未调用 `merge_extra_body`，导致所有配置的 provider_extra 被静默丢弃。**尚无修复 PR**。🔗 [Issue #9775](https://github.com/zeroclaw-labs/zeroclaw/issues/9775)
- **[#9774] Signal 通道静默丢弃 sourceUuid-only 发送者** — 新开，S1 级，影响手机号隐私用户。**已有修复 PR #9777**。🔗 [Issue #9774](https://github.com/zeroclaw-labs/zeroclaw/issues/9774)
- **[#9768] daemon reload 信号错误** — 新开，S2 级，文档建议的操作会直接杀死 daemon（SIGUSR1 未实现为 reload）。🔗 [Issue #9768](https://github.com/zeroclaw-labs/zeroclaw/issues/9768)
- **[#9697] ZeroCode 无法连接 Task Scheduler 启动的 daemon** — 已接受，S3 级。🔗 [Issue #9697](https://github.com/zeroclaw-labs/zeroclaw/issues/9697)

**P2（中等）**：

- **[#9771] zeroclaw-gateway clippy -D warnings 失败** — 新开，死代码问题。🔗 [Issue #9771](https://github.com/zeroclaw-labs/zeroclaw/issues/9771)
- **[#9769] withheld-capability 通知在日志持久化关闭时不可见** — 新开，安全告警可达性问题。🔗 [Issue #9769](https://github.com/zeroclaw-labs/zeroclaw/issues/9769)
- **[#9328] verifiable-intent 约束评估未验证证书链** — 已接受，安全漏洞。🔗 [Issue #9328](https://github.com/zeroclaw-labs/zeroclaw/issues/9328)

**已修复/已关闭**：
- **[#9652] config set 拒绝带连字符的 cron key** — 已关闭。🔗 [Issue #9652](https://github.com/zeroclaw-labs/zeroclaw/issues/9652)
- **[#9335] 支持 data-wrapped OpenAI 兼容响应** — 已关闭。🔗 [Issue #9335](https://github.com/zeroclaw-labs/zeroclaw/issues/9335)

---

### 6. 功能请求与路线图信号

**可能进入 v0.8.5/v0.9.0 的功能方向**：

- **OpenAI 兼容 API 层**（#8603，评论 16）— 目前只有 WebSocket/ACP/webhook，社区对标准 REST 接口的需求非常强烈。若实现，将大幅降低第三方工具接入门槛。
- **workspace 内敏感文件保护**（#8424 RFC + #9776 PR）— 已进入实现阶段，通过 glob 模式扩展 `forbidden_paths`。
- **Anthropic 存储型 OAuth profiles**（#9464 RFC + #9420 PR）— 实现已完成，等待维护者确认契约。
- **Goal mode v1**（#8303，评论 18）— 跨 agent turn 的持久化任务执行框架，是更复杂自主行为的基石。
- **Shell 命令策略分层**（#7155，评论 16）— 已收到 Rev 3 更新，按 @Audacity88 的 Phase 0 缩小了范围。

---

### 7. 用户反馈摘要

**明确痛点**：

- **成本问题**：[#9631] 用户反映通过 OpenRouter 代理时，每次请求重复发送 system prompt 和工具 schema，导致费用显著升高，期望通过稳定 `session_id` 触发 prompt caching。
- **配置不一致**：[#9652] 用户在按照文档操作时发现 `config set` 与 `config list/get` 对同一 key 的行为不一致（已修复）。
- **安全可见性**：[#9769] 安全相关的 `vi_verify` 被屏蔽后，在关闭日志持久化时用户无法感知该能力已被禁用。
- **渠道可靠性**：[#6350] WhatsApp 通道在 LID 联系人场景下静默丢消息，且日志中无任何报错，用户难以排查。

---

### 8. 待处理积压

以下 Issue/PR 长期未获维护者响应，需关注：

- **[#9464] RFC: Anthropic stored-profile OAuth alias contract** — 已等待近 10 天，等待维护者确认契约细节，关联大 PR #9420 也在排队。🔗 [Issue #9464](https://github.com/zeroclaw-labs/zeroclaw/issues/9464)
- **[#6909] RFC: 桌面屏幕交互与控制** — 已存在 73 天，虽为 P2，但多次更新，需要维护者明确方向。🔗 [Issue #6909](https://github.com/zeroclaw-labs/zeroclaw/issues/6909)
- **[#8424] RFC: Workspace-relative forbidden path patterns** — 已存在 39 天，已有实现 PR #9776，等待评审合并。
- **[#8748] 需维护者推进的多个 P2 RFC**：如 #9246（ZeroCode 迁移配置保留）、#8832（插件看板）、#6954（内部 turn 的 provenance）——均标记 `needs-maintainer-review` 且更新于 8 月 5-6 日，但未见维护者响应。

---

### 项目健康度评估

| 维度 | 状态 |
|------|------|
| 活跃度 | ⭐⭐⭐⭐⭐ 极高（50 Issues + 50 PRs / 24h） |
| 安全性 | ⚠️ 需关注（3 个新增安全相关 bug，多个安全 RFC 等待评审） |
| 合并效率 | ⭐⭐ 低（今日无合并，49 个 PR 待合并） |
| 社区参与 | ⭐⭐⭐⭐ 高（多用户提交新 Issue，评论活跃） |
| 沟通效率 | ⚠️ 多个 Issue 标记 `needs-author-action` 但长时间未更新 |

**最大风险**：PR 合并积压达 49 条，其中包含 3 个 P1 级修复（#9737、#9678、#9428），可能导致安全修复延迟上线。项目处于 v0.8.5 稳定线推进期（8 月 30 日截止），建议维护者优先评审安全相关的待合并 PR。

</details>

---
*本日报由 [agents-radar](https://github.com/Augustrains/agents-radar) 自动生成。*